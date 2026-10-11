
## Accessing Releases

**FIGURE 10-4**
Accessing releases is simple.

![](img/c75d0c4fa51711b62f211459ae794f3f_408_0.png)

The releases are grouped by version numbers, and each available download is displayed as one of the different types of packages (Tarball, Debian Package, Windows ZIP, and so on).

Create *download.php* and begin adding the code:

```php
<?php
    require("project_functions.php");
    pf_protect_nonadmin_page();
```

You first include the *project_functions.php* file and then use `pf_protect_nonadmin_page()` to protect the page from direct use.

Run a query to grab the release versions:

```php
pf_protect_nonadmin_page();

$sql = "SELECT * FROM homepageproject_releaserversions WHERE project_id = " . $project_id . " ORDER BY id DESC";
$result = mysql_query($sql);
```

```php
echo "<h1>Download</h1>";
```

In this case, you ask for all versions in which the *id* field matches `$project_id` (set in *project_main.php*) and then order the results in descending (reverse) order. You use descending order because it is likely that the most recently added versions are the latest versions.

Iterate through each version, displaying the version number as you go:

```php
echo "<h1>Download</h1>";
while($vrow = mysql_fetch_assoc($result)) {
    echo "<h2>" . $vrow['version'] . "</h2>";
```

Run a query to gather the releases for each version:

```php
echo "<h2>" . $verrow['version'] . "</h2>";
$sql2= "SELECT homepage_project_releasefiles.filename,homepage_project_releasefiles.date, homepage_project_releasetypes.type FROM homepage_project_releaseversions INNER JOIN homepage_project_releasefiles ON homepage_project_releasefiles.version_id = homepage_project_releaseversions.id INNER JOIN homepage_project_releasetypes ON homepage_project_releasetypes.type_id = homepage_project_releasetypes.id WHERE homepage_project_releaseversions.id = " . $verrow['id'];
$result = mysql_query($sql2);
$numrows = mysql_num_rows($result);
```

This query performs two inner joins, connecting the *homepage_project_releaseversions* table to the *homepage_project_releasefiles* table and then to the *homepage_project_releasetypes* table. The query returns the filename, date, and type of the release.

Display the results:

```php
$numrows = mysql_num_rows($result);

echo "<ul>";

if($numrows == 0) {
    echo "<li><strong>No releases!</strong></li>";
} else {

while($verrow = mysql_fetch_assoc($result)) {
echo "<li><a href='releases/".$verrow['filename'] . "'>Download the " . $verrow['type'] . "</a> (<i>Released " . date("D jS F Y g.iA", strtotime($verrow['date'])) . "</i>)</a>";
}

echo "</ul>";
}
```

## Viewing Screenshots

If the user clicks the Screenshots link, the func GET variable contains screenshots and screenshots.php is loaded into project_main.php.

Create screenshots.php and add the code shown in Example 10-5.

### EXAMPLE 10-5 Displaying screenshots is as simple as iterating through the query results.

```php
<?php
    require("project_functions.php");
    pf_protect_nonadmin_page();

    $sql = "SELECT * FROM homeproject_screenshots WHERE project_id = " . $project_id . ";";
    $result = mysql_query($sql);
    $numrows = mysql_num_rows($result);

    echo "<h1>" . $project_name . " Screenshots</h1>";
    if($numrows == 0) {
        echo "No screenshots!";
    } else {
        while($row = mysql_fetch_assoc($result)) {
            echo "<a href='screenshots/" . $row['name'] . "'><img src='./screenshots/" . $row['name'] . "' width='" . $config_projectscreenshotthumbsize . "'></a>";
            echo "<br><br>";
        }
    }
?>
```

The first few lines protect the file from direct access (as you did earlier) and then a query gathers all screenshots for the current project. A check is made to see if any rows were returned. If none came back, No screenshots! is displayed; otherwise, the images are listed. Each image displays at the width set in $config_projectscreenshotthumbsize and links to the full-size image.

With a couple of screenshots available, you should see something similar to Figure 10-5 in your browser.

# My Project Screenshots

![](img/c75d0c4fa51711b62f211459ae794f3f_411_0.png)

![](img/c75d0c4fa51711b62f211459ae794f3f_411_1.png)

FIGURE 10-5 Screenshots are reduced in size visually to fit more on the page.

## Available Projects Viewer

So far in your development, the user needs to specify the pathname of the project so that he can go to www.mysite.com/projects/<projectname> to view it. It would be useful to provide a simple page that sits in the www.mysite.com/projects/ directory to display a list of projects available for viewing.

Create *index.php* in the directory and add the code shown in Example 10-6.

### EXAMPLE 10-6 This page is a useful starting point for showcasing your projects.

```php
<?php
    require("phphomeprojectconfig.php");

    if(file_exists($config_headerfile)) {
        include($config_headerfile);
    }

    require("db.php");

    echo "<h1>Projects</h1>";
    echo "<p>I have created the following project(s):</p>";

$projsql = "SELECT * FROM homeproject_projects;";
$projresult = mysql_query($projsql);

while($projrow = mysql_fetch_assoc($projresult)) {
    echo "<h2>" . $projrow['name'] . "</h2>";
    echo "<p>" . $projrow['about'] . "</p>";
    echo "<p><ul><li><a href=" . $config_projecturl . "/" . $projrow['pathname'] . ">View this project</a></li></ul></p>";
}

if(file_exists($config_headerfile)) {
    include($config_footerfile);
}
?>
```

The code performs a query to gather all available projects and then displays the name of each project as well as some information and a link to the project information page. The URL to the project page is constructed by concatenating the project name and `$config_projecturl` variables.

## Checking If a File Exists

The `file_exists()` function is used to check if header/footer files exist at the location specified in the project configuration file (`phphomeproject.php`). If they do exist, they are included.

Remember throughout this project that you are not assuming that header/footer files exist; as such, you need to check their availability.

## Administering Projects

With the viewing of projects complete, you can now focus on creating the ability to administer a project. These administration pages are similar to previous projects in the book—a series of Web forms that add information to the database.

Before you begin, create an `admin` directory inside the main project directory. All of the administration files are created in this new directory.

Create a new file called `admin.php` and then add the code shown in Example 10-7.

### EXAMPLE 10-7 OK, I was lying about the huge amount of code……

```php
<?php

    require("project_admin.php");

?>
```

### NOTE

### Dealing with Header Files

In this project, there has been no assumption that header/footer files exist. Although they have no impact on the code if unavailable, when they do exist, the header redirects are a little tricky.

If you were to include the header file before you include `project_admin.php` in `admin.php` and then click the Downloads link, an error would occur. This happens when you have added the download and as such the page tries to redirect.

To manage this problem, include the header file in the individual blocks in `project_admin.php`.

This file simply includes the `project_admin.php` file. In the previous sections, you included `project_main.php` and then used that file as a middleman to manage which files are loaded for which menu options. The same technique is used here.

Create `project_admin.php` and start adding the code:

```php
<?php

    session_start();
    require("../p/home/projectconfig.php");
    require_once("../project_functions.php");

    pf_protect_admin_page();

    require("../db.php");
```

You first include the config, functions, and database settings and then protect the page.
