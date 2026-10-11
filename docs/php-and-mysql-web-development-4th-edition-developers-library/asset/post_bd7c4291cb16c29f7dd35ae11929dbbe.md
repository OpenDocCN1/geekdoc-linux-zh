
## Chapter 9 Writing MySQL Programs Using PHP

### 9.2.1.2 Displaying and Entering Scores

Now that we have support in place for extracting Web input parameters conveniently, we can use that support for writing *score\_entry.php*. That script needs to be able to communicate information from one invocation of itself to the next. We'll use a parameter called *action* for this, which can be obtained as follows when the script executes:

```php
$action = script_param('action');
```

If the parameter isn't set, that means the script is being invoked for the first time. Otherwise, it can test the value of *$action* to find out what to do. The general framework for *score\_entry.php* looks like this:

```php
#!/usr/bin/php

# score_entry.php - Score Entry script for grade-keeping project

require_once 'sampdb_pdo.php';

# define action constants
define('SHOW_INITIAL_PAGE', 0);
define('SOLICIT_EVENT', 1);
define('ADD_EVENT', 2);
define('DISPLAY_SCORES', 3);
define('ENTER_SCORES', 4);

# ... put input-handling functions here ...

$title = 'Grade-Keeping Project -- Score Entry';
html_begin($title, $title);

$dbh = sampdb_connect();

# determine what action to perform (the default is to
# present the initial page if no action is specified)
$action = script_param('action');
if (is_null($action))
    $action = SHOW_INITIAL_PAGE;

switch ($action)
{
case SHOW_INITIAL_PAGE:     # present initial page
    display_events($dbh);
    break;
case SOLICIT_EVENT:         # ask for new event information
    solicit_event_info();
    break;
case ADD_EVENT:             # add new event to database
    add_new_event($dbh);
    display_events($dbh);
    break;
case DISPLAY_SCORES:        # display scores for selected event
    display_scores($dbh);
    break;
case ENTER_SCORES:          # enter new or edited scores
    enter_scores($dbh);
    display_events($dbh);
    break;
default:
    die("Unknown action code ($action)\n");
}

$dbh = NULL; # close connection

html_end();
?>
```

The $action variable can take on several values, which we test in the switch statement. In PHP, switch is much like its C counterpart; it's used here to determine which action to take and to call the functions that implement the action. To avoid having to use literal action values, the switch statement refers to symbolic action names that are set up earlier in the script using PHP's `define()` construct.

Let's examine the functions that handle these actions one at a time. The first one, `display_events()`, presents a list of allowable events by retrieving rows of the `grade_event` table from MySQL and displaying them. Each row of the table lists the event ID, date, and event category (test or quiz). The event ID appears in the page as a hyperlink that you can select to edit the scores for that event. Following the event rows, the function adds one more row containing a link that enables a new event to be created:

```php
function display_events($dbh)
{
    print("Select an event by clicking on its number, or select\n");
    print("New Event to create a new grade event:<br /><br />\n\n");
    print("<table border=\"1\">\n");

    # Print a row of table column headers
    print("<tr>\n");
    display_cell('th', 'Event ID');
    display_cell('th', 'Date');
    display_cell('th', 'Category');
    print("</tr>\n");

    # Present list of existing events. Associate each event id with a
    # link that will show the scores for the event.
    $stmt = "SELECT event_id, date, category
              FROM grade_event ORDER BY event_id";
    $sth = $dbh->query($stmt);

    while ($row = $sth->fetch())
    {
        print("<tr>\n");
        $uri = sprintf("%s?action=%d&event_id=%d",
                       script_name(),
                       DISPLAY_SCORES,
                       $row['event_id']);
        display_cell('td',
                     "<a href=\"$uri\">" . $row['event_id'] . "</a>",
                     FALSE);
        display_cell('td', $row['date']);
        display_cell('td', $row['category']);
        print("</tr>\n");
    }

    # Add one more link for creating a new event
    print("<tr align='center'>\n");
    $uri = sprintf("%s?action=%d",
                  script_name(),
                  SOLICIT_EVENT);
    display_cell('td colspan="3"',
                 "<a href=\"$uri\">Create New Event</a>",
                 FALSE);
    print("</tr>\n");

    print("</table>\n");
}
```

The URLs for the hyperlinks that re-invoke `score_entry.php` are constructed using `script_name()`, a function that figures out the script's own pathname. `script_name()` is useful because it enables you to avoid hardwiring the name of the script into the code. (If you write the name literally, the script will break if you rename it.) `script_name()` can be found in the `samp/db_pdo.php` file.

`script_name()` is somewhat similar to `script_param()` in that it accesses a PHP superglobal array. However, it uses a different array because the script name is part of the information supplied by the Web server, not as part of the input parameters.

```php
function script_name()
{
    return ($_SERVER["SCRIPT_NAME"]);
}
```

The `display_cell()` function used by `display_events()` generates cells in the event table:

```php
# Display a cell of an HTML table. $tag is the tag name ('th' or 'td'
# for a header or data cell), $value is the value to display, and
# $encode should be true or false, indicating whether or not to perform
# HTML-encoding of the value before displaying it. $encode is optional,
# and is true by default.
function display_cell($tag, $value, $encode = TRUE) {
    if (strlen($value) == 0) { # is the value empty/unset?
        $value = '&nbsp;';
    } else if ($encode) { # perform HTML-encoding if requested
        $value = htmlentities($value);
    }
    print "<$tag>$value</$tag>\n";
}
```

If you select the “Create New Event” link in the table that `display_events()` presents, `score_entry.php` is re-invoked with an action of `SOLICIT_EVENT`. That triggers a call to `solicit_event_info()`, which displays a form that enables you to enter the date and category for the new event:

```php
function solicit_event_info() {
    print ("<form method='post' action='".script_name()."'>\n"
           . "<input type='hidden' name='action' value='"
             . ADD_EVENT . "'>\n");
    print 'Enter information for new grade event:<br /><br />\n';
    print 'Date: \n';
    print "<input type='text' name='date' value='' size='10'> \n\n";
    print '<br />\n';
    print 'Category: \n';
    print "<input type='radio' name='category' value='T' checked='checked'>\n";
    print " Test \n";
    print "<input type='radio' name='category' value='Q'>\n";
    print " Quiz \n";
    print "<input type='submit' name='submit' value='Submit'> \n\n";
    print '</form>\n';
}
```

The form generated by `solicit_event_info()` contains an edit field for entering the date, a pair of radio buttons for specifying whether the new event is a test or a quiz, and a Submit button. The default event category is 'T' (test). The script writes out literal HTML to construct the form here. For later scripts in this chapter, we'll develop a set of helper functions that generate form elements.

When you fill in this form and submit it, `score_entry.php` is invoked again, this time with an `action` value equal to `ADD_EVENT`. The `add_new_event()` function then is called to enter a new row into the `grade_event` table:

```php
function add_new_event($dbh)
{
    $date = script_param('date');       # get date and event category
    $category = script_param('category'); # entered by user

    if (empty($date)) # make sure a date was entered, and in ISO 8601 format
        die("No date specified\n");
    if (!preg_match('/^\d{4}-\d{1,2}-\d{1,2}$/', $date))
        die("Please enter the date in ISO 8601 format (CCYY-MM-DD)\n");
    if ($category != 'T' && $category != 'Q')
        die("Bad event category\n");

    $stmt = "INSERT INTO grade_event (date, category) VALUES(?, ?)";
    $sth = $dbh->prepare($stmt);
    $sth->execute(array($date, $category));
}
```

`add_new_event()` uses the `script_param()` library routine to access the parameter values that correspond to the date and category fields in the new-event entry form. Then it performs some minimal safety checks:

- The date should not be empty, and it should have been entered in ISO 8601 format. The `preg_match()` function performs a pattern match for ISO 8601 format: `preg_match('/^\d{4}-\d{1,2}-\d{1,2}$/', $date)`

  Single quotes are used here to prevent interpretation of the dollar sign and the backslash as special characters. The test is true if the date consists of three sequences of digits separated by non-digit characters. That's not bullet-proof, but it's easy to add to the script, and it catches many common errors.

- The event category must be one of the values allowed in the `category` column of the `grade_event` table ('T' or 'Q').

For additional safety, you might want to enable input data restrictions by setting the `SQL` mode before inserting the data. For example:

```php
$dbh->exec('SET sql_mode = "TRADITIONAL"');
```

If the parameter values look okay, `add_new_event()` enters a new row into the `grade_event` table. The statement-execution code uses placeholders to make sure the data values are quoted properly for insertion into the query string. After executing the statement, `add_new_event()` returns to the main part of the script (the `switch` statement), which displays the event list again so that you can select the new event and begin entering scores for it.
