# ## Prevent Session Hijacking

The following steps will help prevent many types of session hijacking techniques:

+   -   Allow random session IDs to successfully authenticated users.
+   -   Consider storing encrypted information in the cookie, so that it is not possible for end users to manipulate it.
+   -   Pass all cookie information using SSL.

# ## Hidden HTML Elements

Hidden HTML elements are static values contained in web forms. These values are not displayed to end users. The following HTML code can be used to set a hidden element:

```
<INPUT  NAME="shippingcharges"  TYPE=HIDDEN  VALUE="5.25">
```

Poorly designed web applications trust hidden HTML tags in order to pass information across the end user’s session. In this case, a malicious user may download the HTML form and change the preceding HTML code to

```
<INPUT  NAME="shippingcharges"  TYPE=HIDDEN  VALUE="-99">
```

After submitting the modified form, a value of −99 for the *shippingcharges* field would be passed to the vulnerable web application. If the web application blindly accepts this value, and if the target were an e-commerce web site, the user may end up with a credit placed on his or her credit card!

# ## Do Not Trust Hidden HTML Elements

Web application developers should not trust the values of hidden HTML elements. It is a good idea to perform web application reviews to ensure that hidden HTML element values are not being trusted.

# ## Source Code Comments

During the development phase of web applications, it is common for programmers to place comments within the CGI or HTML source code. These comments help developers share details with fellow programmers. Source code comments may contain critical information such as passwords to database servers. Sometimes, such comments are overlooked when the web application is put into production: