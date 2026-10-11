
## New Topic Creation

The user has clicked the main New Topic link in the `header.php` file, and as such, no forum `id` is passed to the page. The New Topic page should display a drop-down combo box on the form that contains a list of forums that the user can select to post the topic.

The only part of the page that is different is that no `id` is passed to it to determine whether the combo box with the forums should be displayed.

Create a new file called `newtopic.php` and add the following code:

```html
<form action="<?php echo $pf_script_with_get($SCRIPT_NAME); ?>" method="post">
    <table>
        <?php
        if($validforum == 0) {
            $forumsmsql = "SELECT * FROM forums ORDER BY name;";
            $forumsresult = mysql_query($forumsmsql);
            ?>
            <tr>
                <td>Forum</td>
                <td>
                    <select name="forum">
                        <?php
                        while($forumsrow = mysql_fetch_assoc($forumsresult)) {
                            echo "<option value='" . $forumsrow['id'] . "'>" .
                            $forumsrow['name'] . "</option>";
                        }
                        ?>
                    </select>
                </td>
            </tr>
            <?php
        }
        ?>
            <tr>
                <td>Subject</td>
                <td><input type="text" name="subject"></td>
            </tr>
            <tr>
                <td>Body</td>
                <td><textarea name="body" rows="10" cols="50"></textarea></td>
            </tr>
            <tr>
                <td></td>
                <td><input type="submit" name="submit" value="Post!"></td>
            </tr>
    </table>
</form>
```

The usual suspects are present in this forum: the subject, body, and Submit button. At the top of the form, a check is made if `$validforum` is equal to 0. If it is, the combo box is created with the forums inside it. This `$validforum` variable is the result of the usual validation that exists at the top of the page.

Again, the `pf_script_with_get()` function is used on this page.

Add the code at the top of the page:

```php
<?php

session_start();

require("config.php");
require("functions.php");

$db = mysql_connect($dbhost, $dbuser, $dbpassword);
mysql_select_db($dbdatabase, $db);
```

After this initial code, run a quick query to check if any forums exist:

```php
mysql_select_db($dbdatabase, $db);

$forchecksql = "SELECT * FROM forums;";
$forcheckresult = mysql_query($forchecksql);
$forchecknumrows = mysql_num_rows($forcheckresult);

if($forchecknumrows == 0) {
  header("Location: " . $config_basedir);
}
```

The if check redirects the page if there are no rows.

Validate the GET variable:

```php
if($forchecknumrows == 0) {
  header("Location: " . $config_basedir);
}

if(isset($_GET['id']) == TRUE) {
  if(is_numeric($_GET['id']) == FALSE) {
    $error = 1;
  }

  if($error == 1) {
    header("Location: " . $config_basedir);
  }
  else {
    $validforum = $_GET['id'];
  }
}
else {
  $validforum = 0;
}
```

Check if the user is logged in, and if not, deny access:

```php
if(isset($_SESSION['USERNAME']) == FALSE) {
  header("Location: " . $config_basedir . "/login.php?ref=newpost&id=" . $validforum);
}
```

Now you can process the form. You need to first check which SQL statement you build:

- If the page was passed an `id` GET variable, use `$validforum` in the INSERT statement.
- If the page was not passed the variable, use the `id` from the drop-down combo box that was added to the form.

Here is the code:

```php
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

In this code, the `if` checks to see if `$validforum` is equal to 0 (no variable passed to the page), and if it is, one SQL statement is defined; otherwise, the SQL statement in the `else` is defined.

Run the query:

```php
$topicsql = "INSERT INTO
topics(date, user_id, lastpostuser_id, forum_id,
subject) VALUES(NOW()
, " . $_SESSION['USERID']
, " . $_SESSION['USERID']
, " . $validforum
, " . $_POST['subject']
");";
```

```php
mysql_query($topicsql);
$topicid = mysql_insert_id();
```

This example uses a new function called `mysql_insert_id()`. This function returns the generated `id` (the `auto_increment` `id`) from the last `INSERT` statement.

Build and execute the SQL for the `messages` table:

```php
$topicid = mysql_insert_id();
```

```php
$messagesql = "INSERT INTO messages(date,
user_id, topic_id, subject, body) VALUES(NOW()
, " . $_SESSION['USERID']
, " . mysql_insert_id()
, " . $_POST['subject']
, " . $_POST['body']
");";
mysql_query($messagesql);
header("Location: " . $config_basedir . "/viewmessages.php?id=" .
$topicid);
```

```php
}
```

In this code, the page redirects to the `viewmessages.php` page and the `id` from `mysql_insert_id()` is passed as a `GET` variable to it to display the new message.

Build the `else` part of the code that is executed when the submit `POST` variable has not been detected:

```php
header("Location: " . $config_basedir . "/viewmessages.php?id=" . $topicid);
}
else {
    require("header.php");

if($validforum != 0) {
    $namesql = "SELECT name FROM forums ORDER BY name;";
    $nameresult = mysql_query($namesql);
    $namerow = mysql_fetch_assoc($nameresult);

    echo "<h2>Post new message to the " . $namerow["name"] . "
    forum</h2>";
}
else {
    echo "<h2>Post a new message</h2>";
}
```

```html
<form action="<?php echo
pf_script_with_get($SCRIPT_NAME); ?>" method="post">
<table>
```

Here you check if the `$validforum` variable is not equal (!=) to 0 (a valid forum id was passed to the page). This id is used to get the name of the forum and add the heading **Post new message** to the `<forum>` forum. If `$validforum` is equal to 0 (no valid id GET variable was posted to the page), the generic **Post a new message** heading is added.

Finally, add the closing code:

```html
</table>
</form>
```

```php
<?php
}
```

```php
require("footer.php");

?>
```

Your completed page for posting a new message can be seen in Figure 5-10.

![](img/c75d0c4fa51711b62f211459ae794f3f_170_0.png)

**FIGURE 5-10** Posting a new message

### Replying to Threads

Writing a page to reply to threads is fairly simple. The page is passed the topic id as an id GET variable, and this is used to take the content from the form and insert it into the messages table.

Create a file called `reply.php` and add the form:

```html
<form action="<?php echo pf_script_with_get($_SCRIPT_NAME); ?>" method="post">
	<table>
	<tr>
		<td>Subject</td>
		<td><input type="text" name="subject"></td>
	</tr>
	<tr>
		<td>Body</td>
		<td><textarea name="body" rows="10" cols="50"></textarea></td>
	</tr>
	<tr>
		<td></td>
		<td><input type="submit" name="submit" value="Post!"></td>
	</tr>
	</table>
</form>
```

Move to the start of the file and add the introductory code:

```php
<?php

session_start();
require("config.php");
require("functions.php");
```

Run the id GET variable through the usual validation code:

```php
require("config.php");
require("functions.php");

$db = mysql_connect($dbhost, $dbuser, $dbpassword);
mysql_select_db($databases, $db);

if(isset($_GET['id']) == TRUE) {
    if(!is_numeric($_GET['id'])) {
        $error = 1;
    }
    
    if($error == 1) {
        header("Location: " . $config_basedir);
    }
    else {
        $validtopic = $_GET['id'];
    }
}
else {
    header("Location: " . $config_basedir);
}
```

Check that the user is logged in:

```php
else {
    header("Location: " . $config_basedir);
}

if(isset($_SESSION['USERNAME']) == FALSE) {
    header("Location: " . $config_basedir . "/login.php?ref=reply&id=" . $validtopic);
}
```

To process the form, run the INSERT query:

```php
if(isset($_SESSION['USERNAME']) == FALSE) {
    header("Location: " . $config_basedir . "/login.php?ref=reply&id=" . $validtopic);
}
```
