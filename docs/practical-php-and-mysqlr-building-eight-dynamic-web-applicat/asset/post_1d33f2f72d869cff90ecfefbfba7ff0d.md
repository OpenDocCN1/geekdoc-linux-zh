
## Accessing the Database

In the base directory (phpomeoproject), create *db.php* and add the connection code shown in Example 10-2.

### EXAMPLE 10-2
This file is no different from other projects.

```php
<?php
    require("phpomeoprojectconfig.php");
    $db = mysql_connect($dbhost, $dbuser, $dbpassword);
    mysql_select_db($databatabase, $db);
?>
```

## Creating the Functions

This project uses two custom functions in addition to *pf_fix_slashes()* and *pf_check_number()* from previous projects. In the base directory, create a new file called *functions.php* and add the configuration file:

```php
<?php
    require("phpomeoprojectconfig.php");
    
    // Add pf_protect_nonadmin_page():
    function pf_protect_nonadmin_page() {
        if(basename($_SERVER['SCRIPT_NAME']) != "index.php") {
            echo "<h1>Error</h1>";
            echo "You cannot access this page directly. Please go to the main project pages directly.";
            exit;
        }
    }
```

The *pf_protect_nonadmin_page()* function protects individual pages from direct access. If you refer to Figure 10-1, you can see that a page such as *download.php* is included in *project-main.php*, which is in turn included in *index.php*. Naturally, you don't want users to access *download.php* directly. This function simply checks to see if the name of the current page is different from *index.php*. If so, an error is displayed. Currently, this function is hard coded to *index.php*, so you might want to adjust this code to work with files not called *index.php*.

Use a similar technique to protect the admin pages:

```php
    exit;
}
}

function pf_protect_admin_page() {
    global $config_projectadminfilename;

    if(basename($_SERVER['SCRIPT_NAME'])
    != $config_projectadminfilename) {
        echo "<h1>Error</h1>";
        echo "You cannot access this page directly. Please go to the admin pages directly.";
        exit;
    }
}
```

The only difference here is that the function checks what the name of the admin page is set to. You can’t assume that the admin page should be called *index.php*, because the *index.php* file in an *admin* directory may administer a different part of the site. To solve this problem, the function refers to the $config_projectadminfilename setting in the configuration file.

The first line of the function uses the **global** keyword to access a variable outside the scope of the function, and the variable is checked in the **if** statement.

### NOTE
**Understanding Variable Scope**

Variable scope is a problem that confuses many newcomers to a language. The basic concept is that a variable is accessible within the scope of whatever block in which it was created. This is fine in most scripts because the variable was created outside of a function and is therefore accessible by anything.

When you use a function, however, only the function knows about the variable created inside it. To access the variable outside the function, you need to add this line before you use it:

```php
global <variableName>
```

The variable is now accessible.

Add the functions you already know and love:

```php
exit;
}
}

function pf_fix_slashes($string) {
    if (get_magic_quotes_gpc() == 1) {
        return($string);
    }
    else {
        return(addslashes($string));
    }
}

function pf_check_number($value) {
    if(!isset($value) == FALSE) {
        $error = 1;
    }

    if(is_numeric($value) == FALSE) {
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

## The Main Project

Jump to a project's directory (such as the *myproject* directory) and from the code in Example 10-3, create *index.php*.

### EXAMPLE 10-3
This file loads in *project_main.php*, which manages which features are loaded.

```php
<?php
$project = substr(dirname($SCRIPT_NAME),
    strrpos(dirname($SCRIPT_NAME), "/") + 1);

require("../phphomeprojectconfig.php");
require("../project_bar.php");


require("../project_main.php");
?>
```

The first line in this file grabs the name of the current project. To do this, the project path name is cut out of the URL (for example, cutting out *myproject* from www.mysite.com/projects/myproject/). This can be used later to gather information about the project.

Three files are then included: the main configuration file (*phphomeprojectconfig.php*), the menu options (*project_bar.php*), and the main application page (*project_main.php*). These files are accessed from the preceding directory by including the prefix `../` with each file.

![](img/c75d0c4fa51711b62f211459ae794f3f_405_0.png)

## Deploying *phphomeproject*

The site administrator uses the *phphomeproject* file to deploy *phphomeproject* inside an existing Web application. The admin simply includes *project_bar.php* in the side menu bar code (such as *bar.php* in previous projects) and then includes *project_main.php* in the main body of the page.

In the next sections, you will create the files that you have just included.

## Viewing Menu Options

Create *project_bar.php* and add the menu options with the code in Example 10-4.

### EXAMPLE 10-4
This file can be deployed in an existing design to display the menu anywhere easily.

```html
<h1>Options</h1>
<ul>
<li><a href="index.php">Home</a></li>
<li><a href="index.php?func=download">Download</a></li>
<li><a href="index.php?func=screenshots">Screenshots</a></li>
</ul>
```

This file contains a simple unordered list with the different options. Each option links to *index.php* but passes a different setting to the func GET variable. This variable is processed by *project_main.php*, and the relevant functionality is displayed.

## Accessing the Project’s Features

When a user clicks one of the menu options, project_main.php acts the middleman, pulls off the func variable, and serves the correct page.

To do this, func is run through a switch statement. The switch provides case blocks for the different options available. If no func variable is present, or if func contains something that a case block does not satisfy, the default block is executed.

Create project_main.php in the base directory and begin adding the code:

```php
<?php
require('db.php');

$sql = "SELECT * FROM homeproject_projects WHERE pathName = '' . $project . ''";
$result = mysql_query($sql);
$row = mysql_fetch_assoc($result);

// Here you run a query to select any projects in which pathname is equal to the directory name held in $project ($project was created in index.php).
```

Set up the variables:

```php
$row = mysql_fetch_assoc($result);
$project_id = $row['id'];
$project_name = $row['name'];
```

Two variables (user later) are created to store the project id and name.

Open the switch and add the first case block:

```php
$project_name = $row['name'];
switch($_GET['func']) {
    case 'download':
        require('download.php');
        break;
```

If the user clicks the Download link, func is set to download and the block is executed. The download.php page is included inside the block.

Add a similar block for the Screenshots link:

```php
break;
case 'screenshots':
    require('screenshots.php');
    break;
```

Add the `default` block that catches any other situation:

```php
break;

default:
    $sql = "SELECT * FROM homeproject_projects
          WHERE pathname = " . $project . "';
    $result = mysql_query($sql);
    $row = mysql_fetch_assoc($result);

    echo "<h1>" . $row['name'] . "</h1>";
    echo "<p>" . $row['about'] . "</p>";

break;
```

You construct a query that returns the project and then simply prints the name of the project and displays the description.

Finally, close the `switch`:

```php
break;
}
?>
```

When you view My Project, you should be presented with a vision not vastly different from the one shown in Figure 10-3.

![](img/c75d0c4fa51711b62f211459ae794f3f_407_0.png)

**FIGURE 10-3** The rather uninteresting design can be replaced when the application is deployed in an existing site with its existing design.

## DOWNLOADING RELEASES

Releases are by far the most important aspect in a software project. If your releases are difficult to access, unstable, or unusable, it is unlikely that many people will bother to download and use them.

The application manages releases in a very simple way, as shown in Figure 10-4.
