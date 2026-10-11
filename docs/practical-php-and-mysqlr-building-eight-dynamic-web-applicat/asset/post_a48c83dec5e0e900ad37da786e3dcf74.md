
of release (such as a Debian Package, RPM, Windows ZIP, Mac OS X disk image, and so on) from the homeproject_releasetypes table. Finally, the homeproject_screenshots table stores the names of the screenshots for each release.

![](img/c75d0c4fa51711b62f211459ae794f3f_396_0.png)

## FIGURE 10-2
The database is fairly straightforward.

### NOTE

### Making Your Tables Stand Out

The reusable component uses the same database as the application that is hosting it. To indicate which tables are which, each table in the reusable component project uses the prefix `homeproject_`. This is an intentional choice so that when this application is deployed in an existing Web site, the tables that are part of the application can be identified easily. As an example, take a look at the following list of tables:

- admins
- customers
- blogentries
- homeproject_projects
- homeproject_releaserversions

You can quite easily identify which tables are part of the application.

## Implementing the Database

Start phpMyAdmin. Create a new database called *phphomeproject* and add the following tables:

### The *homeproject_projects* Table

- *id*. Make this an `MEDIUMINT` and turn on `auto_increment`. Set this field as a primary key.
- *name*. Make this a `VARCHAR` with a length of 100.
- *about*. Make this a `TEXT`.
- *pathname*. Make this a `VARCHAR` with a length of 30.

### The *homeproject_releaseversions* Table

- *id*. Make this an `INT` and turn on `auto_increment` in the `Extras` column. Set this field as a primary key.
- *project_id*. Make this an `INT`.
- *version*. Make this a `VARCHAR` and set the size to 20.

### The *homeproject_releasestypes* Table

- *id*. Make this a `TINYINT` and turn on `auto_increment`. Set this field as a Primary Key.
- *type*. Make this a `VARCHAR` and set the size to 20.

### The *homeproject_releasefiles* Table

- *id*. Make this an `INT` and turn on `auto_increment`. Set this field as a primary key.
- *type_id*. Make this a `TINYINT`.
- *date*. Make this a `DATETIME`.
- *version_id*. Make this an `INT`.
- *filename*. Make this a `VARCHAR` with a length of 50.

### The *homeproject_screenshots* Table

- *id*. Make this an `INT` and turn on `auto_increment`. Set this field as a primary key.
- *project_id*. Make this an `INT`.
- *name*. Make this a `VARCHAR` with a length of 50.

## Inserting Sample Data

With a solid set of tables ready to go, you can now add some sample data. Remember, do not fill in a number in the *id* column, which *auto_increment* does for you automatically. Feel free to add your own sample data, or use the suggested information described in the following sections.

### Sample Data for the homeproject_projects Table

Add a project such as the one shown in Table 10-1.

**TABLE 10-1** This table contains the main project details.

| NAME | ABOUT | PATHNAME |
| :--- | :--- | :--- |
| My Project | This is an example project that demonstrates how a project is managed inside this re-usable project management application. | myproject |

The pathname field provides a unique string to refer to the project. This is used in a few parts of the Web application—most notably in the URL, such as `localhost/sites/homeproject/<pathname>/`.

### Sample Data for the homeproject_releaseversions Table

Add version numbers as shown in Table 10-2.

**TABLE 10-2** Because a version number could have multiple releases, store the version numbers in a dedicated table.

| PROJECT_ID | VERSION |
| :--- | :--- |
| 1 | 0.1 |
| 1 | 0.2 |

### Sample Data for the homeproject_releasestypes Table

Add three records, using the following names:

- Tarball
- Debian Package
- Windows ZIP

### Sample Data for the `homeproject_releasefiles` Table

Add two records to this table, using the correct `version_id` and `type_id`. The `filename` field should contain the name of the release file (such as `myrelease.tar.gz`). When you later create the `releases` directory, remember to place a file in the directory with the same filename.

### Sample Data for the `homeproject_screenshots` Table

Add a few records into the table, using the correct `project_id`. The `name` field should contain the name of the screenshot (such as `myscreenshot.png`). When you create the `screenshots` directory later, remember to include images with the same name.

## Using Directories Intelligently

Unlike previous projects in the book, `phphomeproject` makes extensive use of directories to determine specific types of functionality. The project has three main directories: `base`, `admin`, and `project`.

The base directory, such as `www.mysite.com/projects`, is the base projects directory on the Web site. This directory contains the different files that form `phphomeproject`. This directory also includes an `index.php` file, which lists the projects on the server so that the user can select which project to view.

A project directory, such as `www.mysite.com/projects/myproject`, is a subdirectory inside the base directory. This directory contains a single `index.php` file (which includes the files from the base directory, as shown in Figure 10-1). The project also contains two subdirectories: `releases` (which stores software releases) and `screenshots` (which stores screenshots).

The `admin` directory is the directory the site administrator uses to adjust project settings. This directory is also found within the base directory, such as `www.mysite.com/projects/admin`, and contains a number of files for managing the site.

## Creating the Directories

First, create the base directory and call it `homeproject`. Then create the `admin` subdirectory.

For each project you also need to create a subdirectory inside `homeproject`. The name of the directory should be the same as the pathname field in the `homeproject_projects` table. If you added the My Project record as was done in this example, create a directory called `myproject`. Inside `myproject` create the `releases` and `screenshots` subdirectories. Be sure that both `releases` and `screenshots` have write access to them.

You should now have the following directories:

- homeproject
  - admin
  - myproject
    - releases
    - screenshots

![](img/c75d0c4fa51711b62f211459ae794f3f_400_0.png)

## STARTING TO CODE: BUILDING THE BACKBONE

Developing *phphomeproject* requires two core areas:

- Viewable project information. This is the area that Web site visitors see. Visitors can view project information, downloads, and screenshots.
- Project administration. This is the interface for configuring projects; only the site administrator accesses this interface.

In this project, you will implement the project viewing area first and then move on to create the administration area. Before you begin, you will create some of the structural files (configuration file, functions, and so on).

Because this project is available as a re-usable component, you should use a separate configuration file for the settings specific to the project. Inside the *homeproject* directory, create *phphomeproject.php* and then add the code shown in Example 10-1.

EXAMPLE 10-1 The configuration file is separate from the main configuration file of your Web site.

```php
<?php

$dbhost = "localhost";
$dbuser = "root";
$dbpassword = "";
$dbdatabase = "phphomeproject";

$config_headerfile = "http://localhost/sites/homeproject/header.php";
$config_footerfile = "http://localhost/sites/homeproject/footer.php";

$config_projecturl = "http://localhost/sites/homeproject/";
$config_projectdir = "/opt/lampp/htdocs/sites/homeproject/";

$config_projectadminbasedir = "http://localhost/sites/homeproject/admin/";
$config_projectadminfilename = "admin.php";

$config_projectscreenthumbssize = 300;
?>
```

In addition to the normal database settings, this configuration file includes a number of other options:

- `$config_headerfile` and `$config_footerfile`. The location of the header and footer files in the Web application.
- `$config_projecturl`. The URL where you can find phphomeproject.
- `$config_projectdir`. The directory that includes phphomeproject. Use this directory when copying new releases and screenshots to the releases and screenshots directories.
- `$config_projectadminbasedir`. The location of the admin directory.
- `$config_projectadminfilename`. The name of the file (such as admin.php) used to access the admin functionality.
- `$config_projectscreenthumbssize`. The width to which thumbnails should be set when viewing screenshots.

It is important to remember that you are developing phphomeproject in a separate directory, which is independent of an existing Web site. When phphomeproject is deployed in an application, these settings need to be changed to reflect the existing site (for example, changing `$config_projecturl` to `http://www.mysite.com/projects/`). You will deploy the site later in the chapter.
