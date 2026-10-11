is set to another value (typically 0), the question is awaiting moderation from the owner of the subject.

Finally, add a comment for the first question in the comments table, as shown in Table 9-4.

**TABLE 9-4** Comments are a useful way to provide additional information for a question.

| QUESTION_ID | TITLE | COMMENT | USER_ID |
| :--- | :--- | :--- | :--- |
| 1 | Book recommendation | If you want to learn about vari-ables in more detail, refer to Variable Foo Machine by Foo Bar. | 2 |

### Sample Data for the *mod_subowner* Table
Leave this table empty.

# # STARTING TO CODE

To get started, create a new project directory and create the config/header/footer and main index files. First, copy *db.php* from a previous project to the current directory and then create a new file called *config.php* and add the code shown in Example 9-1.

> **EXAMPLE 9-1** The configuration file is virtually the same as in previous projects.

```
```php
<?php

$dbohost = "localhost";
$dbuser ="root";
$dbpassword = "";
$database = "faq";

$config_basedir = "http://localhost/sites/faq/";

$config_sitename = "You ask the questions";
?>
```
```