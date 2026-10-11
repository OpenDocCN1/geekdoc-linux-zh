![](bbox=[0.1, 0.11, 0.9, 0.39])

**FIGURE 11-2** The interface is simple and efficient, but will be added to later in the chapter.

# ## Handling User Logins

Like many other projects in this book, user login functionality is an essential feature. The code and functionality for user logins in this project is also virtually identical to the code in the other projects in this book. Much of this should be familiar to you, but if not, head back and play with some of the previous projects.

The core difference with this login incarnation is that you used encrypted passwords when you added the users. When the user was created, the md5() MySQL command was used to hash the password. To validate the user who types his username and password into the login form, you first hash the password entered into the form and then compare both hashed passwords. If they match, the password is valid.

*Create userlogin.php* and add the form:

```
`<form action="<?php echo $SCRIPT_NAME ?>" method="post"> <table> <tr> <td>Username</td> <td><input type="text" name="username"></td> </tr> <tr> <td>Password</td> <td><input type="password" name="password"></td>`
```