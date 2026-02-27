# Reflected XSS into attribute with angle brackets HTML-encoded(PortSwigger)

## 📌 Description

This lab contains a reflected cross-site scripting vulnerability in the search blog functionality where angle brackets are HTML-encoded.



## 🎯 Objective

To solve this lab, perform a cross-site scripting attack that injects an attribute and calls the alert function.



## 🔎 Recon

I typed something random to see the page's source code and see how what I wrote was passed through the page's source code.

Example:
I typed "test" in the text field.

And my input appeared in a value tag like this: value="test"


## 💥 Exploitation

I tested a few payloads and after a while, the one that worked was: "onmouseover="alert(1)

And the script executed successfully, confirming the vulnerability.



## 🧠 Lessons Learned

This lab reinforced how improper output handling can lead to client-side code execution.
