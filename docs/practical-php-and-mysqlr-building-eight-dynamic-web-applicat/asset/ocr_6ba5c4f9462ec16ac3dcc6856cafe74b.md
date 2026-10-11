With the main design complete, your browser should display something similar to Figure 6-2.

![](bbox=[0.08, 0.18, 0.88, 0.54])

**FIGURE 6-2** The main page provides a simple and clean interface for the shopping cart.

# ## MANAGING USER LOGINS

Users are a critical element in a shopping cart, and tracking both registered and unregistered users is important. Many of the different scripts that form the site have two strands of functionality: one if the user is logged in and one if not.

The login page is similar to the others in the book. Create a file called `login.php` and add the form:

```
<form action="<?php echo $SCRIPT_NAME; ?>" method="POST">
<table>
  <tr>
    <td>Username</td>
    <td><input type="textbox" name="userBox"/>
  </tr>
  <tr>
    <td>Password</td>
    <td><input type="password" name="passBox"/>
  </tr>
  <tr>
    <td></td>
    <td><input type="submit" name="submit" value="Log in"/>
  </tr>
</table>
</form>
```