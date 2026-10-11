
## Logging Out Users

To log out a user, unregister the three sessions created in the login page. Remember that the menu bar uses sessions to track which options are currently selected, so you can't simply destroy the session. Add the following code from Example 11-6 to userlogout.php.

> **EXAMPLE 11-6** Don't destroy the session, because the menu uses session variables.

```php
<?php
session_start();
require("config.php");

session_unregister("SESS_USERNAME");
session_unregister("SESS_USERID");
session_unregister("SESS_USERLEVEL");

header("Location: " . $config_basedir);
?>
```

## Updating the Sidebar

If a user is logged in, you will want to add a box in the sidebar to indicate that the user is logged in and then also list options available to him. Like some of the previous projects, this appears as a box similar to the one shown in Figure 11-3.

The sidebar displays the options available to the user.

![](img/c75d0c4fa51711b62f211459ae794f3f_458_0.png)

Fire up bar.php, jump to the top of the file, and add the code shown in Example 11-7.

The "visible" class can be used with the table styles shown in the Generic Web sites project.

```php
<?php
session_start();

require("db.php");

echo "<table class='visible' width='100%' cellspacing=0 cellpadding=5>";
echo "<tr><th class='visible'>Login details</th></tr>";
echo "<tr><td>";

if($_SESSION['SESS_USERNAME']) {
    echo "Logged in as <strong>". $_SESSION['SESS_USERNAME'] . "</strong> - <a href='userlogout.php'>Logout</a>";
    echo "</p>";

    if($_SESSION['SESS_USERLEVEL'] > 1) {
        echo "<a href='addstory.php'>Post a new story</a><br />";
    }

    if($_SESSION['SESS_USERLEVEL'] == 10) {
        echo "<a href='addcat.php'>Add a new Category</a><br />";
    }
    echo "</p>";
} else {
    echo "<a href='userlogin.php'>Login</a>";
}

echo "</td></tr>";
echo "</table>";

echo "<h1>Topics</h1>";

$sql = "SELECT * FROM categories WHERE parent = 1";
```

The options in the table are dependent on the level of user logged in. Any level 1 users or above can add stories. If the user is the admin (level 10), he can add categories. (You create the addstory.php and addcat.php pages later.)

## Viewing and Rating Stories

When the user clicks a category and views the list of available stories, each story’s subject links to the page with the full story text. This page not only views the full story, but also includes a feature to allow users who are logged in to rate the story. Now you know if your editors are writing rubbish stories or not.

Ratings are specifically limited to logged-in users. The reason for this limitation is subtle but important. You need to prevent trigger-happy users from voting for the same story more than once. To prevent such abuse, you somehow need to track whether the user has voted. To solve this problem, a number of options are at your disposal, each with advantages and disadvantages:

- Track the user by his session ID. You could store the current session ID in a table and prevent more than one vote from the same ID. This session ID will reliably track a unique user currently viewing the Web site. The problem is that the user could restart the browser to generate a new session ID, thus foiling your system.
- Use cookies. Cookies allow you to store a tiny text file, which you can use to store a small amount of information on the user’s hard disk. The problem with this technique is that the cookies are deleted when the user clears his history so that Aunt Maude doesn’t come across any visited Web sites that would make her blush.
- Only allow voting by users who are logged in. This technique provides a solid means of tracking the user, and there is no way the rating system can be forged. The obvious disadvantage of this method is that the user needs to register with yet another Web site.

Technical decisions such as this are often difficult, with no clear solution available. To ensure that the ratings system remains entirely accurate and free from abuse, you will use the third technique—requiring users to log in.

Before you start writing the code, you should first create some images that can visually depict average ratings of the story. These images should be fairly small (around 20x20 pixels) and convey the three states shown in Figure 11-4.

### FIGURE 11-4

The ratings system consists of three images.

![](img/c75d0c4fa51711b62f211459ae794f3f_460_0.png)

After the average rating has been calculated, it is rounded to the nearest 0.5 (such as 7.5 or 8.0). To display the rating, 10 images are displayed, using the preceding images where needed. As an example, an average rating of 8 would have 8 full and 2 off images. A rating of 6.5 would have 5 full, 1 half, and 3 off images.

Start building the page by creating viewstory.php and then add the introductory and validation code:

```php
<?php
require("config.php");
require("functions.php");

if(pf_check_number($_GET['id']) == TRUE) {
   $validid = $_GET['id'];
} else {
   header("Location: " . $config_basedir);
}

require("header.php");
```

Before getting to the ratings, you need to display the main story text. Run a query to gather this information and then display it:

```php
$sql = "SELECT * FROM stories WHERE id = " . $validid . "";
$result = mysql_query($sql);
$row = mysql_fetch_assoc($result);

echo "<h1> " . $row['subject'] . " </h1>";
echo date("D jS F Y g:iA", strtotime($row['dateposted'])) . " <br />";
echo nl2br($row['body']);
```

When displaying the information, the date is formatted into a readable state and the nl2br() function converts empty lines in the body text to `<br>` tags. This conversion ensures that the blank lines in the original text are retained.

When a story is rated, the ratings table stores the score. Using this table, get the number of ratings as well as the average rating for the story:

```php
$avgsql = "SELECT COUNT(id) AS number, AVG(rating) AS avg FROM ratings WHERE story_id = " . $validid . ";";
$avgresult = mysql_query($avgsql);
$avgrow = mysql_fetch_assoc($avgresult);

echo "<p>";
echo "<strong>Rating:</strong> ";
```

This query uses the COUNT() and AVG() MySQL functions to return the number of votes and the average. The AVG() function returns the average of the field that you specify. In this case, you want the average of the ratings field.

There is a good possibility that not every story has a rating, however, so you need to account for this:

```php
if($avgrow['number'] == 0) {
    echo "No ratings!";
}
```

If ratings exist, round the average up or down as necessary:

```php
else {
    $a = (round($avgrow['avg'] * 2) / 2);
}
```

This line rounds the average with round(), multiplies the result by 2, and then divides by 2 to determine the final rating. This simple little mathematical trick is a good way to get the final value.

Determine if the final result is a 0.5 figure (such as 7.5, as opposed to 8):

```php
else {
  $a = (round($avgrow['avg'] * 2) / 2) ."<br>";
  $a *= 10;
  if($a%5 == 0 && $a%10 != 0) {
    $range = ($a / 10) - 0.5;
  } else {
    $range = $a / 10;
  }
}
```

To calculate if we have .5 value in $a (such as 6.5), first multiply the value of $a by 10 ($a *= 10), and then inside the brackets of the if statement check if $a can be divided by five. If it does, $a is divided by 10 to get to its original value, and 0.5 is subtracted. The resulting $range variable indicates the number of full images to display.

Create a for loop to display each image:

```php
for($i=1;$i<=$range;$i++) {
  echo "<img src=" . $config_basedir . "siteimages/rating_full.png>";
}
```

The for loops between 1 and the value inside $range and then displays rating_full.png each time.

Check if the average is a float again, to see if the half-on image should be added:

```php
if($a%5 == 0 && $a%10 != 0) {
  echo "<img src=" . $config_basedir . "siteimages/rating_half.png>";
}
$a = $a / 10;
```

Calculate how many off images should be displayed by removing the rounded average from 10:
