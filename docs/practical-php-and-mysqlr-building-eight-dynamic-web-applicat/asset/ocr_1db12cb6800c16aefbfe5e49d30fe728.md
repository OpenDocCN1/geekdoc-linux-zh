When the user has successfully logged in, two session variables are created: `SESS_USERNAME` and `SESS_USERID`. These variables are used throughout the code to check if a user is logged in and refer to the user's username and id. Before you can actually log in, though, you need to create the user's control panel.

# Displaying the Control Panel

When the user has successfully logged into the system, the page redirects to a control panel that shows a number of options available to that specific user. This page looks like the one shown in Figure 9-7.

![](bbox=[0.07, 0.32, 0.91, 0.66])

**FIGURE 9-7** The control panel provides a place to show relevant options for specific users.

This page provides links to a number of different features related to an owned subject. These features include the ability to add questions, remove ownership, and moderate submitted questions. This functionality is spread over a number of pages, which are discussed later.

Create a new file called *userhome.php* and add the following code:

```
<?php

session_start();
require("config.php");
```