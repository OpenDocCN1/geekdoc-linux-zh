![](bbox=[0.09, 0.09, 0.5, 0.34])

**FIGURE 9-10**  
If the topic is not known, the user can select it from the combo box.

# NOTE

# What About No Topics?

If no topics are available in the subject, and the subject owner tries to add a question, the script should prompt the owner to first add a topic. This fail-safe technique is used in the code for this project.

Create a new file called _addquestion.php_ and add the following code:

```
<?php
session_start();
require("db.php");
require("functions.php");
```

Only logged-in users should use this page, so check if a user is logged in and then redirect any users who are trying to post questions but have not logged in:

```
require("functions.php");

if(!$ _SESSION['SESS_USERNAME']) {
    header("Location: " . $config_basedir . "login.php");
}
```