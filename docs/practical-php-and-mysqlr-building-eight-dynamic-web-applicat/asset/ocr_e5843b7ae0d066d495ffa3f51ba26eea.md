# User Registrations

Before you support user and administrator logins, you first must create support on the site for people to register a username. This page should authenticate users automatically.

When a user registers, this is the process:

+   - The user goes to the registration page and fills in a username, enters the password twice, and types an email address.
+   - The user is sent a verification email.
+   - The user checks his email account and clicks the link in the email to verify the registration.
+   - The account is activated.

Implementing this process in code is straightforward:

+   - The user goes to the registration page and fills in the details.
+   - When the form is submitted, a check is made to see if the passwords match. If they don't, the user is asked to correct the form.
+   - If the passwords match, the username is checked against the database to see if the name has already been taken. If it has, the user is asked to choose another username.
+   - If the username has not been taken, a random string is generated and the username, password, email address, and random string are added to the database. Note that the “active” field in the database is left at 0 because the account is currently inactive.
+   - An email is constructed with a URL that has GET variables containing the email address and random string. This email is then mailed to the address provided by the user.
+   - When the user clicks the link in the email, the page in the link checks the database to see if there is a record with the email address and random string provided. If there is, the active field is set to 1, and the account is activated.

To get started, create a new file called *register.php* and add the form:

```
<h2>Register</h2>
 To register on the <?php echo $conf_forumname; ?> forums, fill in the form below.
<form action="<?php echo $SCRIPT_NAME; ?>" method="POST">
<table>
<tr>
<td>Username</td>
```