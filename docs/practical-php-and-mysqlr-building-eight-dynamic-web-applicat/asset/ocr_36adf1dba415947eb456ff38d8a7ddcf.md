# EXAMPLE 5-3 Continued

```
```
}
else {
  header("Location: " . $config_basedir . "/admin.php?error=1");
}
}
else {
  require("header.php");
  echo "<h2>Admin login</h2>";
  
  if($_GET['error']) {
    echo "Incorrect login, please try again!";
  }
}
```
```
<form action="<?php echo pf_script_with_get($SCRIPT_NAME); ?>" method="post">
  <table>
    <tr>
      <td>Username</td>
      <td><input type="text" name="username"></td>
    </tr>
    <tr>
      <td>Password</td>
      <td><input type="password" name="password"></td>
    </tr>
    <tr>
      <td></td>
      <td><input type="submit" name="submit" value="Login!"></td>
    </tr>
  </table>
</form>
```
```
<?php
}
require("footer.php");
?>
```
```

The code here differs in only two ways:

+   • When the admin is successfully identified, the session variable registered is ADMIN, as opposed to USERNAME.