
## EXAMPLE 8-10 Continued.

```php
    echo $row['name'];
    echo "<p> . $row['description'] . "</p>";
    echo "<p><strong>Date:</strong> " . date("D jS F Y"),
    strtotime($row['date']) . "<br />
    echo "<strong>Time:</strong> " . $row['starttime'] . " - " . $row['endtime'] . "</p>";
}
?>
```

Within this script, you check to see if the **action GET** variable is equal to *getevent*. The *action* variable is used to distinguish among different features on page. You could create another block of code for a different action.

Within the *if*, the record from the *events* table with the same id as the *id GET* variable is returned and displayed. When this functionality is complete, the event information is displayed in the sidebar when the user clicks an item, as shown in Figure 8-6.

![](img/c75d0c4fa51711b62f211459ae794f3f_310_0.png)

**FIGURE 8-6** The dynamic nature of Ajax is not given justice by a static screenshot, but rest assured, it makes the application feel much sleeker.

### Adding a New Event

The mechanics of adding a new event to the calendar is handled in a very similar way to viewing event information—a function is loaded, the request is made, and the event case `<div>` from `bar.php` is updated.

Figure 8-7 shows the interface for this feature.

![](img/c75d0c4fa51711b62f211459ae794f3f_311_0.png)

**FIGURE 8-7** When the user hovers over some empty space in a cell, the background appears gray; the user can then click to access the New Event form.

The first step is to implement the function that is called in the link that you added to the main calendar view in `view.php`. Load `internal_request.js`, and add the function shown in Example 8-11.

**EXAMPLE 8-11** This function uses `open()` to load the script that displays the form.

```javascript
function newEvent(eventdate, error){
    http.open('get', 'neweventform.php?date=' + eventdate + "&error=" +
               error);
    http.onreadystatechange = handleNewEvent;
    http.send(null);
}
```

This function works in a virtually identical fashion to getEvent(), which was covered earlier. The request, however, loads the form (stored in neweventform.php). The function also passes an error code to the page. The handler for this request is handleNewEvent.

Add the handler below the newEvent() function to internal_request.js:

```javascript
function handleNewEvent(){
if(http.readyState == 4){
var response = http.responseText;
document.getElementById('eventcase').innerHTML = response;
}
}
```

This handler works in exactly the same way as the handleEvent() function.

Create the neweventform.php file and add the form, as shown in Example 8-12.

**EXAMPLE 8-12** The Start Time and End Time form controls use for loops to generate the available options.

```php
<?php
if($_GET['error'] == 1){
echo "<p><strong>There is an error in the form. Please correct it and re-submit.</strong></p>";
}
?>
<h1>Add a new event</h1>
<form action="processnewevent.php?date=<?php echo $_GET['date'] ; ?>" method="POST">
<table>
<tr>
<td>Date</td>
<td>
<?php echo "<strong>" . date("D jS F Y", strtotime($_GET['date'])) . "</strong>"; ?>
<input type="hidden" name="date" value="<?php echo $_GET['date']; ?>">
</td>
</tr>
<tr>
<td>Name</td>
<td><input type="text" name="name" size="15"></td>
</tr>
<tr>
<td>Start Time</td>
<td>
<select name="starthour">
<?php
for($i=0;$i<=23;$i++) {
        echo "<option value=" . sprintf("%02d", $i) . ">"
. sprintf("%02d", $i) . "</option>";
    }
?></select>

<select name="startminute">
<?php
    for($i=0;$i<=60;$i++) {
        echo "<option value=" . sprintf("%02d", $i) . ">"
. sprintf("%02d", $i) . "</option>";
    }
?></select>

</td>
</tr>
<tr>
    <td>End Time</td>
    <td>
<select name="endhour">
<?php
    for($i=0;$i<=23;$i++) {
        echo "<option value=" . sprintf("%02d", $i) . ">"
. sprintf("%02d", $i) . "</option>";
    }
?></select>
<select name="endminute">
<?php
    for($i=0;$i<=60;$i++) {
        echo "<option value=" . sprintf("%02d", $i) . ">"
. sprintf("%02d", $i) . "</option>";
    }
?></select>

</td>
</tr>
<tr>
    <td>Description</td>
    <td><textarea cols="15" rows="10" name="description"></textarea></td>
</tr>
<tr>
    <td></td>
    <td><input type="submit" name="submit" value="Add Event"></td>
</tr>
</table>
</form>
```

At the top of the form, a check is made to see if the error GET variable is available. If it is, an error message is displayed.

The script to process the form is *processnewevent.php*. Create this file and begin adding the following code:

```php
<?php
require("db.php");
$error = 0;
if(empty($_POST['name'])) {
$error = 1;
}
if(empty($_POST['description'])) {
$error = 1;
}
if($_POST['starthour'] > $_POST['endhour']) {
$error = 1;
}
if($_POST['starthour'] == $_POST['endhour'] && $_POST['startminute'] == $_POST['endminute']) {
$error = 1;
}
if($error == 1) {
header("Location: " . $config_basedir
. "view.php?error=1&eventdate=" . $_GET['date']);
exit;
}
```

This batch of if statements perform some validation checks. These checks work similarly to previous validation examples—if a check fails, the *$error* variable is created and the page redirects. The checks are made to ensure that the end time is not earlier than the start time and that the start and end time are not the same. A check is also made to ensure that the text boxes are not empty.

Prepare the variables:

```php
$elements = explode("-", $_POST['date']);
$redirectdate = $elements[1] . "-" . $elements[0];
$finalstart = $_POST['starthour'] . ":" . $_POST['startminute'] . ":00";
$finalend = $_POST['endhour'] . ":" . $_POST['endminute'] . ":00";
```

The first line in this block uses explode() to fill the $elements array with the different parts of the date. The second line constructs a variable with just the month and year elements (these elements are used when browsing the months, such as with the arrows in the sidebar).

The second two lines format the times in a format that can work in the TIME database field. This field requires the 00:00:00 format, so each line concatenates the form elements into this format.

Insert the data and use $redirectdate to redirect to the month to which the date was added:

```php
$finalstart = $_POST['starthour'] . ":" . $_POST['startminute'] . ":00";
$finalend = $_POST['endhour'] . ":" . $_POST['endminute'] . ":00";
$insert = "INSERT INTO events(date, starttime, endtime, name, description) VALUES(" . "'".$_POST['date']."' , '" . $finalstart . "', '" . $finalend . "', '" . addslashes($_POST['name']) . "', '" . addslashes($_POST['description']) . "');";
mysql_query($insert);
header("Location: " . $config_basedir . "view.php?date=" . $redirectdate);
```

The feature is now complete.

## Deleting Events

Deleting an event happens when the user clicks the red X block next to an event. Create a new file called delete.php and add the code shown in Example 8-13.

**EXAMPLE 8-13** To delete an event, remove the record from the database.

```php
<?php

require("db.php");

$sql = "DELETE FROM events WHERE id = " . $_GET['id'];
mysql_query($sql);

echo "<script>javascript: history.go(-1)</script>";
?>
```

The usual code for deleting an event from the database is shown here. Then you use a different type of redirect, this time using JavaScript. You could use one of the other types of redirect; this one was used to show you another option.

## SUMMARY

In this project, you created a different type of Web application. Unlike the publicly hosted and accessible applications elsewhere in the book, this project involved creating something used by a single person. This application was also more like a traditional application than some of the other projects, largely due to the Ajax functionality.

Ajax has become a key Web development technology, and the skills you explored here will help you to create more dynamic and flexible Web applications.
