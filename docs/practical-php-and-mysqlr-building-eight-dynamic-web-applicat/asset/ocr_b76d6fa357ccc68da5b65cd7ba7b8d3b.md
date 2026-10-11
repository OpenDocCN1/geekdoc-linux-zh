```
$sql = "SELECT * FROM logins WHERE username = '" . $_POST['username'] . "' AND password = '" . $_POST['password'] . "';"
```

```
$result = mysql_query($sql);
$numrows = mysql_num_rows($result);
```

The SQL statement is created to check if the username in the *logins* table is equal to the username box in the form and if the *password* field is equal to the password box in the form. The query is then run, and the rows are counted. The number of lines returned from the query indicates whether the details typed were correct. If the details are correct, a single row is returned—no more, no less. If no rows are returned, the details do not match.

Add the following code:

```
$numrows = mysql_num_rows($result);

if($numrows == 1) {
    $row = mysql_fetch_assoc($result);
    session_register("USERNAME");
    session_register("USERID");

    $_SESSION['USERNAME'] = $row['username'];
    $_SESSION['USERID'] = $row['id'];

    header("Location: " . $config_basedir);
}
else {
    header("Location: " . $config_basedir . "/login.php?error=1");
}
```

In the case where the login details are valid, a new session is created. When using PHP sessions, you must register your session variables. The *session_register()* lines create two variables, called *USERNAME* and *USERID*.

# NOTE
Be Constant When Naming Variables

Naming session variables in uppercase is not mandatory, but it’s useful because this helps them to stand out in your code as different types of variables.