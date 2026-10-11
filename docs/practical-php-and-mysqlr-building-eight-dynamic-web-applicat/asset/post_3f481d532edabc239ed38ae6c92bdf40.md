
# The allow Block

To accept a question, add the allow block:

```php
echo "</table>";
break;

case "allow":
	$validid = set_validid();
	
	$modqsql = "UPDATE questions SET active = 1 WHERE id = "
	.	$validid . "";
	$modq = mysql_query($modqsql);
	
	header("Location: " . $config_basedir .
	"adminmodquestions.php?func=main");
break;
```

This block updates the question and sets the active field to 1 to make the question live. The page then redirects to the main block of *adminmodquestions.php*.

# The deny Block

To deny a question, the process is split into two parts. The first part asks the user if she is sure that she wants to reject the question. See Figure 9-13.

![](img/c75d0c4fa51711b62f211459ae794f3f_368_0.png)

FIGURE 9-13 Before denying a question, be sure this is what the user wants.

Add the code for this section:

```php
header("Location: " . $config_basedir .
"adminmodquestions.php?func=main");
break;

case "deny":
    require("header.php");

    $validid = set_validid();

    echo "<h1>Are you sure that you want to reject this question?</h1>";
    echo "<p><a href=" . $SCRIPT_NAME . "?func=denyconf&id="
    . $validid . ">Yes</a>] [<a href="" . $SCRIPT_NAME
    . "?func=main">No</a>]";
    break;
```

This block provides two links. The No link simply links back to the main section of the current script, and the Yes link links to the denyconf section.

# The denyconf Block

To confirm the cold, hard reality of denying a question, add the denyconf block:

```php
echo "<p><a href=" . $SCRIPT_NAME . "?func=denyconf&id="
. $validid . ">Yes</a>] [<a href="" . $SCRIPT_NAME
. "?func=main">No</a>]";
break;
case "denyconf":
    $validid = set_validid();

    $delsql = "DELETE FROM questions WHERE id = " . $_GET['id']
    . "";
    $delq = mysql_query($delsql);

    header("Location: " . $config_basedir .
    "adminmodquestions.php?func=main");
    break;
```

This block deletes the question from the questions table and then redirects back to the main section to display the other moderated questions.

Finally, close the switch and add the footer file:

```php
header("Location: " . $config_basedir .
"adminmodquestions.php?func=main");
break;
}

require("footer.php");
?>
```

# MANAGING SUBJECTS

Subjects are the core foundation of the content that this project manages, and are very similar to Categories in the blog project in Chapter 4. Managing subjects is something that you naturally only want the administrator to be able to do. If you were to give a regular user the run of the subjects, anything could happen.

The capabilities to add and delete subjects are important pieces of functionality to create, but deleting is a capability with which you should take special care. By using InnoDB tables in MySQL, any accidental deletions of a subject cause all of the child topics and questions to be deleted also. As such, be very careful when working through this section.

## Adding Subjects

Adding a subject to the database is as simple as creating a form and adding the contents of the form to the database. Create a new file called `addsubject.php` and add the following code:

```php
<h1>Add a new subject</h1>
<form action="<?php echo $SCRIPT_NAME; ?>" method="post">
<table cellpadding="5">
<tr>
<td>Subject</td>
<td><input type="text" name="subject"></td>
</tr>
<td>Owner</td>
<td>
```

This code adds a form and a table to lay out the form elements. After adding the subject text box, display a combo box so that a subject owner can be chosen:

```php
<td>Owner</td>
<td>
<select name="owner">
<option value="0">-- No Owner --</option>
<?php
$sql = "SELECT * FROM users ORDER BY username ASC;";
$result = mysql_query($sql);

while($row = mysql_fetch_assoc($result)) {
echo "<option value=" . $row['id'] . " >" . $row["username"] . "</option>";
}
?>
</select>
```

A select box is created, and the first entry (which returns the value 0) is added to provide a No Owner option. The other entries in the select box are added from the query.

Complete the form:

```php
            ?>
            </select>
            </td>
        </tr>
        <tr>
            <td>Description Blurb</td>
            <td><textarea name="blurb" cols=50 rows=10></textarea></td>
        </tr>
        <tr>
            <td></td>
            <td><input type="submit" name="submit" value="Add Subject!"/></td>
        </tr>
    </table>
</form>
```

With the form finished, it's time to process it. Jump to the start of the file and add the following code:

```php
<?php

session_start();

require("db.php");
require("functions.php");

if(isset($_SESSION['SESS_ADMINUSER']) == FALSE) {
    header("Location: " . $config_basedir . "adminlogin.php");
}
```

You first protect the page so that only the administrator can access it. Check if the Submit button was clicked and begin the processing:

```php
    header("Location: " . $config_basedir . "adminlogin.php");
}

if($_POST['submit']) {
    $sbsql = "INSERT INTO subjects(subject, blurb, owner_id) VALUES("
            . "'" .    pf_fix_slashes($_POST['subject'])
            . "',"
            . "'" .    pf_fix_slashes($_POST['blurb'])
            . "',"
            . "" .    $_POST["owner"]
            . "');"
    mysql_query($sbsql);
    header("Location: " . $config_basedir);
}
```

Inside this block an INSERT statement adds the form data to the database. Add the else that encases the main form:

```php
header("Location: " . $config_basedir);
}

else {
require("header.php");
?>
<h1>Add a new subject</h1>
<form action="<?php echo $SCRIPT_NAME; ?>" method="post">
```

Finally, after the form, close the else and add the footer file:

```php
</table>
</form>

<?php
}
require("footer.php");
?>
```

The completed page should look like the one shown in Figure 9-14.

![](img/c75d0c4fa51711b62f211459ae794f3f_372_0.png)

## Deleting Subjects

When logged in as an administrator, a user deletes content by clicking the little *X* links. These links hook up with a page to delete the type of content the *X* is next to. If you take a look at the list of subjects, you will see that the *X* next to each subject links to *deletesubject.php* and passes the script the id of the subject to be deleted.

When *deletesubject.php* is first loaded, the user is prompted to confirm that he wants to delete the subject. If he clicks the Yes link, the page reloads but includes a `conf` GET variable. If this variable is present, the subject is deleted.

**NOTE**

**Cascading Fun and Games**

Remember that when a subject is deleted, all topics and questions within that subject are deleted also. The code for the cascading delete was added when you set up your tables.

Create *deletesubject.php* and add the following code:

```php
<?php
session_start();

require('db.php');
require("functions.php");

if($_SESSION['SESS_ADMIN']) {
    header("Location: " . $config_basedir);
}

if(pf_check_number($_GET['subject']) == TRUE) {
    $validsubject = $_GET['subject'];
}
else {
    header("Location: " . $config_basedir);
}
```

First, the code validates the subject GET variable that was passed to the page. Next a check is made to see if the `conf` GET variable exists (remember that this is added when the user confirms deletion of the subject):

```php
header("Location: " . $config_basedir);
}

if($_GET['conf']) {
    $delsql = "DELETE FROM subjects WHERE id = " . $validsubject . ";";
    mysql_query($delsql);
}
```

```php
header("Location: " . $config_basedir);
} else {
require("header.php");
echo "<h1>Are you sure you want to delete this subject?</h1>";
echo "<p>[<a href="" . $SCRIPT_NAME . "?conf=1&subject=" .
. $validsubject . ">Yes</a>] [<a href="" . $config_basedir .
. ">No</a>]";
}
```

If the variable exists, the subject is deleted and the page redirects back to the base page. Otherwise, the question is displayed.

Finally, add the footer file:

```php
echo "<p>[<a href="" . $SCRIPT_NAME . "?conf=1&subject=" .
$validsubject . ">Yes</a>] [<a href="" . $config_basedir . "">No</a>]";
}

require("footer.php");
?>
```

# MANAGING TOPICS

When adding topics to the system, the script needs to work both for normal users who own subjects and for the administrator. The practical differences between a normal user and the admin are mainly in the subjects to which they have access. The administrator can choose any subject to add to a topic, whereas a normal user can choose only the subjects he owns.

## Adding Topics

Create a new file called `addtopic.php` and start the form:

```php
<h1>Add a new topic</h1>

<form action="<?php echo $SCRIPT_NAME; ?>" method="post">
<table cellpadding="5">
<tr>
<td>Subject</td>
```

To display the selection of subjects in the combo box, add the following code:

```php
<td>Subject</td>
<td>
<?php
if($_SESSION['SESS_ADMINUSER']) {
```
