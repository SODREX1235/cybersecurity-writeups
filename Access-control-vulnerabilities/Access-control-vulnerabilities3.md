# User ID controlled by request parameter, with unpredictable user IDs (PortSwigger)


## 📌 Description

This lab demonstrates a horizontal privilege escalation vulnerability where user account access is controlled by a request parameter.

Although the application uses GUIDs (Globally Unique Identifiers) instead of predictable IDs, it still exposes them in other areas of the application, making the access control ineffective.


## 🎯 Objective

To solve this lab, obtain the API key of the user carlos and submit it as the solution.


## 🔎 Recon

I began by exploring the application and looking for references to other users.

While browsing the blog section, I found a post authored by carlos. By clicking on his username, I was redirected to a profile page where the URL contained a GUID parameter:

/profile?id=<GUID>

This revealed that user accounts are identified via GUIDs in the id parameter.

Even though GUIDs are meant to be hard to guess, the application was exposing them publicly through profile links. I saved the GUID associated with carlos.

Next, I logged into my own account using the provided credentials:

wiener:peter

After logging in, I accessed my account page and observed that it also used the same id parameter structure.


## 💥 Exploitation

Since the application relied on the id parameter to determine which account data to display, I tested whether it was vulnerable to horizontal privilege escalation.

I modified the id parameter in the URL:

From my own GUID
To the GUID belonging to carlos
/account?id=<carlos_GUID>

After sending the request, the application returned carlos' account data, including his API key.

This confirmed that the application was not properly validating whether the authenticated user was authorized to access the requested resource.

I then copied the exposed API key and submitted it, successfully solving the lab.


## 🧠 Lessons Learned

This lab highlights a classic case of horizontal privilege escalation, where a user can access another user's data by manipulating request parameters.
