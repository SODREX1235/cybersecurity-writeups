# User role controlled by request parameter (PortSwigger)


## 📌 Description

This lab contains an admin panel at /admin that identifies administrators using a forgeable cookie.

## 🎯 Objective

To solve this lab, access the admin panel and use it to delete the user carlos.

## 🔎 Recon

I navigated to /admin and noticed that access to the admin panel was denied.

Then, I went to the login page and logged in using the provided credentials:

wiener:peter

Using Burp Suite, I turned interception on and enabled response interception. After submitting the login form and forwarding the request, I observed that the server response set a cookie:

Admin=false

This indicated that the application was using a client-side controlled cookie to determine administrative privileges.

## 💥 Exploitation

Since the application relied on a forgeable cookie, I modified the response before forwarding it.

I changed:

Admin=false

to:

Admin=true

After forwarding the modified response, I accessed /admin again, and this time the admin panel was accessible.

From there, I located the user carlos and successfully deleted the account, solving the lab.

## 🧠 Lessons Learned

This lab reinforced how dangerous it is to trust client-side data for access control decisions.
