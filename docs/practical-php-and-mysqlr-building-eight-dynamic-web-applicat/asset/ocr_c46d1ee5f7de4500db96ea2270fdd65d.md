```
<?php
}
require("footer.php");
?>
```

Figure 5-9 shows the completed registration form. Now we need to write the code that verifies the registration.

![](bbox=[0.155, 0.3, 0.935, 0.632])

FIGURE 5-9 The registration form

# Verifying the Account

With the verification email sent, you can create the page to which the link in the email points. This page simply decodes the GET variables (the urlencoded email and verifyingstring variables) and then checks if a row in the database matches. If there is a row, the account is activated by setting the active field in the users table to 1.

Create a new page called verify.php and add the initial code that decodes the variables:

```
<?php
require("header.php");
$verifystring = urldecode($_GET['verify']);
$verifyemail = urldecode($_GET['email']);
```