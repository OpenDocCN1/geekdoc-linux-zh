Chapter 9 Writing MySQL Programs Using PHP

# ### 9.2.1.2 Displaying and Entering Scores

Now that we have support in place for extracting Web input parameters conveniently, we can use that support for writing *score\_entry.php*. That script needs to be able to communicate information from one invocation of itself to the next. We'll use a parameter called *action* for this, which can be obtained as follows when the script executes:

```
```python
$action = script_param ('action');
```
```

If the parameter isn't set, that means the script is being invoked for the first time. Otherwise, it can test the value of *$action* to find out what to do. The general framework for *script\_entry.php* looks like this:

```
```php
#!/php

# score_entry.php - Score Entry script for grade-keeping project

require_once 'sampdb_pdo.php';

# define action constants
define ('SHOW_INITIAL_PAGE', 0);
define ('SOLICIT_EVENT', 1);
define ('ADD_EVENT', 2);
define ('DISPLAY_SCORES', 3);
define ('ENTER_SCORES', 4);

# ... put input-handling functions here ...

$title = 'Grade-Keeping Project -- Score Entry';
html_begin ($title, $title);

$dbh = sampdb_connect ();

# determine what action to perform (the default is to
# present the initial page if no action is specified)
$action = script_param ('action');
if (is_null ($action))
    $action = SHOW_INITIAL_PAGE;

switch ($action)
{
case SHOW_INITIAL_PAGE:     # present initial page
    display_events ($dbh);
    break;
case SOLICIT_EVENT:         # ask for new event information
    solicit_event_info ();
    break;
case ADD_EVENT:             # add new event to database
    add_new_event ($dbh);
```
```