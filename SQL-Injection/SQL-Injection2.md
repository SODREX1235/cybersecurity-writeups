# SQL Injection Vulnerability Allowing Login Bypass (PortSwigger)


## 📌 Description
This lab features a login form vulnerable to SQL Injection. The application fails to properly sanitize the input fields, allowing an attacker to manipulate the backend database query and gain unauthorized access.

## 🎯 Objective
The goal is simple but critical: bypass the authentication mechanism and log in to the application as the administrator user without knowing their password.

## 🔎 Recon
During the reconnaissance phase, I focused on the login functionality. Typically, a login query looks something like this behind the scenes:

SELECT * FROM users WHERE username = 'user_input' AND password = 'password_input'

I hypothesized that if the username field was vulnerable, I could "truncate" the rest of the query. By doing this, I could trick the database into ignoring the password check entirely.

## 💥 Exploitation
To execute the attack, I used Burp Suite to capture and manipulate the login request in real-time.

I navigated to the login page and entered a random username and password.

I intercepted the POST /login request using Burp Suite's Proxy.

I modified the username parameter to: administrator'--

I left the password field with a dummy value (it doesn't matter what's in there now).

The Logic Behind the Payload
The final query executed by the server became:
SELECT * FROM users WHERE username = 'administrator'--' AND password = '...'

administrator: Tells the database exactly which account I want to access.

': Closes the string for the username field.

--: This is the SQL comment indicator. It tells the database to ignore everything that follows it—effectively "deleting" the AND password = ... part of the query.

Because the database only processed the first part of the condition (which was true), the application authenticated me as the admin.

## 🧠 Lessons Learned
This lab is a perfect example of why Identity and Access Management (IAM) should never rely on raw string concatenation.
