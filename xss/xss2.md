# Stored XSS into anchor href attribute with double quotes HTML-encoded (PortSwigger)

## 📌 Description

This lab contains a stored cross-site scripting (XSS) vulnerability in the comment functionality. The value inserted in the Website field is reflected inside an anchor href attribute.

## 🎯 Objective

To solve this lab, submit a comment that triggers the alert function when the comment author name is clicked.

## 🔎 Recon

First, I navigated to one of the blog posts and submitted a comment.

In the Website field, I entered a random alphanumeric string such as:

test123abc

Using Burp Suite, I intercepted the request and sent it to Repeater.

Then, I refreshed the blog post page while interception was enabled and sent that request to Repeater as well.

By analyzing the second request response in Repeater, I noticed that the value entered in the Website field was reflected inside an anchor tag:

<a href="test123abc">username</a>

This confirmed that user input was being inserted directly into the href attribute.

## 💥 Exploitation

Since the input was reflected inside the href attribute, I repeated the process and submitted another comment, but this time I replaced the Website value with the following payload:

javascript:alert(1)

After submitting the comment, the application stored the payload and generated the following link:

<a href="javascript:alert(1)">username</a>

When the author name above the comment was clicked, the browser executed the JavaScript code and triggered the alert box.

This confirmed the stored XSS vulnerability and successfully solved the lab.

## 🧠 Lessons Learned

This lab demonstrates how inserting user-controlled input into HTML attributes without proper validation or sanitization can lead to stored XSS vulnerabilities.
