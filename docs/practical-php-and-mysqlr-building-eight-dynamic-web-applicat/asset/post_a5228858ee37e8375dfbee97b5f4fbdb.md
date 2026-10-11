
```php
    echo "</td>";
    echo "<td><a href='questions.php?subject=" . $subject . "&amp;topic=" . $toprow['id'] . ">" . $toprow["name"] . "</a></td>";
    if($_SESSION['SESS_ADMINUSER']) {
        echo "<td><a href='deletetopic.php?subject=" . $toprow['"_subject_id'] . "&amp;topic=" . $toprow['id'] . ">x</a></td>";
    }
}
echo "</tr>";
}
echo "</table>";
}
?>
```

A check is made to see if the **subject GET** variable is present. If it exists, the same mechanism is used to display the list of topics, and each topic links to *questions.php*, in which the subject and topic are passed.

## Creating the Functions

In this project, you use two functions that you create yourself:

- `pf_fix_slashes()`. This function provides a more intelligent method of ensuring that quotes are properly escaped when adding information to the database.
- `pf_check_number()`. This function is a variant of the `pf_validate_number()` function used in previous projects. This version checks if the variable is valid but does not perform any redirection.

Create a new file called `functions.php` and add the first function:

```php
<?php

function pf_fix_slashes($string) {
    if (get_magic_quotes_gpc() == 1) {
        return($string);
    }
    else {
        return(addslashes($string));
    }
}
```

In previous projects, you used **addslashes()** to escape quotes in user input destined for the database. Although this works fine, the function makes the assumption that the **magic_quotes_gpc** option in **php.ini** is turned off. If the option is turned on and you use **addslashes()**, additional slashes are added in front of the slashes that were added by **magic_quotes_gpc**. The result is a visible slash added to your data.

To solve this problem, the new function uses the **get_magic_quotes_gpc()** to check if the feature is turned on or off. If the function returns 1 or TRUE, magic quotes is turned on and the normal string is returned. If magic quotes are turned off, the string is run through **addslashes()** and then returned. This new function ensures that your application can work with magic quotes turned on or off and requires no modification. Sweet, no?

The next function to roll in is **pf_check_number()**:

```php
function pf_check_number($val) { 
    if(isset($val) == FALSE) { 
        $error = 1; 
    } 
    
    if(is_numeric($val) == FALSE) { 
        $error = 1; 
    } 
    
    if($error == 1) { 
        return FALSE; 
    } 
    else { 
        return TRUE; 
    }
}
?>
```

This function is virtually identical to the **pf_validate_number()** function used in previous projects, but the **if** check on **$error** returns FALSE if there is an error and TRUE if there is not.

![](img/c75d0c4fa51711b62f211459ae794f3f_329_0.png)

### NOTE

### Why Use This Slightly Different Function?

Some of the pages in this project have two personalities: one that is triggered with a GET variable and one without. If you used **pf_validate_number()** in these pages, the personality that does not need the GET variable would fail (**pf_validate_number()** checks if the variable is present) and redirect to another page.

The **pf_check_number()** function does not include the redirect functionality. As such, the function can be used to validate a GET variable if it is present.

## Building the Main Page

The next page to create is `index.php`. This script has two main functions:

- If the page is not passed a subject GET variable, the page displays the last 10 questions.
- If the page does have a subject GET variable, information about that specific subject is displayed. This information includes both the name and description of the subject, as well as some statistical information about the number of topics and questions.

Create the file and begin adding the code:

```php
<?php

session_start();

require("config.php");
require("functions.php");

if($_GET['subject']) {
    if(pf_check_number($_GET['subject']) == TRUE) {
        $validsub = $_GET['subject'];
    }
    else {
        header("Location: " . $config_basedir);
    }
}

require("header.php");
```

You checked if the subject GET variable is present and if so, it is run through `pf_check_number()`. If it passes the validation (and returns TRUE), `$validsub` is set to the number. Otherwise, the page re-directs.

Now check if the subject GET variable is present and if so, display the information about the subject:

```php
require("header.php");

if($_GET['subject']) {

    $subsql = "SELECT users.username, subjects.* FROM subjects
              LEFT JOIN users ON subjects.owner_id = users.id
              WHERE subjects.id = " . $validsub . ";";
    $subresult = mysql_query($subsql);
    $subrow = mysql_fetch_assoc($subresult);

    echo "<h1>" . $subrow['subject'] . " Summary</h1>";
```

A query is created to gather the subject information and the username that maps to the `subjects.owner_id` field. In previous projects the join was made using the **WHERE** clause in the SQL, but here you are using the **LEFT JOIN** syntax. The following paragraph describes how the syntax works:

Select the username and subject information (`SELECT users.username, subjects.*`) from the `subjects` table (`FROM subjects`) and then join the `subjects` and `users` tables (`LEFT JOIN users`) with the relevant condition (`ON subjects.owner_id = users.id`) in which the subject id is the same as `$validsub` (`WHERE subjects.id = $validsub`).

When writing joins, you can use a variety of different types of join (**INNER**, **OUTER**, **LEFT**, and **RIGHT**), with **INNER** and **LEFT** as the most common variants. An **INNER** join connects tables with the conditions that you specify. A **LEFT** join performs the same process but also fills in any mismatched fields with **NULL** values. Check the data returned to see if the subject has an owner. If 0 is returned, no owner exists:

```php
echo "<h1>" . $subrow['subject'] . " </h1>";

if ($subrow['owner_id'] == 0) {
    echo "This subject has no owner.";
}
```

### NOTE

### Using the LEFT Join on this Page

The reason for using the **LEFT** join on this page is important. If the `subjects` table has an `owner_id` set to something other than 0, an **INNER** or **LEFT** join can relate the `owner_id` to the `user id` in the `users` table. If, however, the subject has no owner and the `owner_id` is set to 0, an **INNER** join fails because no user with the id 0 exists in the `users` table. When you use a **LEFT** join, this mismatch still returns the data, but the mismatched information is set to **NULL**.

In this project, you use a combination of joins that use the **JOIN** and **WHERE** syntax. This ensures that you are exposed to both methods of creating joins.

If the subject has no owner, check to see if a user is logged in and display a link to the subject ownership page:

```php
if ($subrow['owner_id'] == 0) {
    echo "This subject has no owner.";
}

if($_SESSION['SESS_USERNAME']) {
    echo " If you would like to apply to own this subject, click <a href='applysubowner.php?subject=' . $subject . ">here</a>";
}
```

If the query returns an owner, display the username:

```php
else {
    echo "This subject is owned by <strong>" . $subrow["username"] . "</strong>";
}
```

Display the blurb for the subject in *italic* tags:

```php
echo "<p><i>" . $subrow["blurb"] . "</i></p>";
```

The next step is to gather some statistical information about the subject. Count the number of topics and questions included within the subject:

same as the `subject_id` field in the `topics` table (`ON subjects.id = topics.subject_id`), and then join this to the `questions` table (`LEFT JOIN questions`, in which the topic id is equal to the `topic_id` field in the `questions` table (`ON topics.id = questions.topic_id`)) where the whole query has the subject id of `$validsub` (`WHERE subjects.id = $validsub`) and the question is active (`AND active = 1`).

Display the results of the query in a table:

```php
$toprow = mysql_fetch_assoc($result);

echo "<table class='visible' cellspacing=0 cellpadding=5>";
echo "<tr><th class='visible' colspan=2>Statistics</th></tr>";
echo "<tr>";
echo "<td>Total Topics</td><td>" . $toprow['numtopics'] . "</td>";
echo "</tr>";
echo "<tr>";
echo "<td>Total Questions</td><td>" . $toprow['numquestions'] . "</td>";
echo "</tr>";
echo "</table>";
```

This section should look like Figure 9-2 when it's finished.

![](img/c75d0c4fa51711b62f211459ae794f3f_333_0.png)

**FIGURE 9-2** The sidebar displays the relevant topics for the subject.
