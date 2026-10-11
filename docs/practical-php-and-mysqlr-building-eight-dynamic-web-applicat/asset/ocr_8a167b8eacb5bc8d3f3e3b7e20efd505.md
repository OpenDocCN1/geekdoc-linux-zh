```
$validforum = $_GET['id'];
}
else {
$validforum = 0;
}
```

Check if the user is logged in, and if not, deny access:

```
else {
$validforum = 0;
}

if(isset($_SESSION['USERNAME']) == FALSE) {
header("Location: " . $config_basedir . "/login.php?ref=newpost&id=" . $validforum);
}
```

Now you can process the form. You need to first check which SQL statement you build:

+   - If the page was passed an id GET variable, use $validforum in the INSERT statement.
+   - If the page was not passed the variable, use the id from the drop-down combo box that was added to the form.

Here is the code:

```
if(isset($_SESSION['USERNAME']) == FALSE) {
header("Location: " . $config_basedir . "/login.php?ref=newpost&id=" . $validforum);
}

if($_POST['submit']) {
if($validforum == 0) {
$topicsql = "INSERT INTO topics(date, user_id, forum_id, subject)
VALUES(NOW()
, " . $_SESSION['USERID']
, " . $_POST['forum']
, " . $_POST['subject']
.")";
} else {
$topicsql = "INSERT INTO topics(date, user_id, forum_id, subject) VALUES(NOW()
, " . $_SESSION['USERID']
, " . $validforum
, " . $_POST['subject']
.")";
}
}
```