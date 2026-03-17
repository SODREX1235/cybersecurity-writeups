# Unprotected admin functionality with unpredictable URL (PortSwigger)

## 📌 Description

This lab has an unprotected admin panel. The panel is located at an unpredictable URL, but the location is disclosed somewhere in the application's source code.

## 🎯 Objective

To solve this lab, access the admin panel and use it to delete the user carlos.

## 🔎 Recon

First, I visited the lab home page and inspected the page source using the browser’s developer tools.

While reviewing the source code, I noticed a JavaScript file that contained a reference to an admin panel URL that was not visible in the main interface.

Inside the JavaScript code, the following path was revealed:

/admin-<random-string>

This indicated that the admin panel existed but was hidden using an unpredictable URL rather than proper access control.

## 💥 Exploitation

After discovering the hidden admin path in the JavaScript file, I navigated directly to the disclosed URL.

Once accessed, the admin panel loaded successfully without requiring authentication or authorization checks.

Inside the admin interface, I located the list of users and found the user carlos.

I clicked the Delete option next to the user and removed the account, successfully solving the lab.

## 🧠 Lessons Learned

This lab demonstrates that hiding sensitive functionality behind unpredictable URLs is not a secure access control mechanism.
