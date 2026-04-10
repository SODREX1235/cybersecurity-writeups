# SQL injection vulnerability in WHERE clause allowing retrieval of hidden data (PortSwigger)


## 📌 Description
This lab contains a SQL Injection vulnerability in the product category filter. When the user selects a category, the application performs a SQL query that filters only for products that have been launched (released = 1).

## 🎯 Objective
To solve the lab, perform a SQL injection attack that causes the application to display one or more unreleased products.

## 🔎 Recon
While browsing the site and selecting a category (e.g., "Gifts"), I noticed that the URL filters products via the category parameter.
According to the lab description, the query executed internally by the database is:
SELECT * FROM products WHERE category = 'Gifts' AND released = 1

I realized that the category value is inserted directly into the query without proper sanitization, which allows "breaking" the original logic of the query.

## 💥 Exploitation
To explore the vulnerability, I used Burp Suite to intercept the request when a category filter was applied.

I intercepted the request containing the category parameter.

I modified the parameter value to: ' OR 1=1 --

The final query on the server became:
SELECT * FROM products WHERE category = '' OR 1=1 --' AND released = 1

The use of ' closed the original string's quote, the OR 1=1 created a condition that is always true (forcing all items to be displayed), and the -- commented out the rest of the original query, nullifying the filter that hid unreleased products (AND released = 1).

After forwarding the modified request, the page displayed all products in the database, including the unreleased ones, solving the lab.

## 🧠 Lessons Learned
This lab reinforces the importance of never trusting user input. SQL queries should be built using 
Prepared Statements (parameterized queries) instead of concatenating strings directly, preventing malicious commands from altering the database logic.
