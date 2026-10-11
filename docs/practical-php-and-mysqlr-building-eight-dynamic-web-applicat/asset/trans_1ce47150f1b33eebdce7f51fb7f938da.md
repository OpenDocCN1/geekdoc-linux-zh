

发布文件（例如 Debian 软件包、RPM、Windows ZIP、Mac OS X 磁盘映像等）取自 homeproject_releasetypes 表。最后，homeproject_screenshots 表存储每个发布的截图名称。

![](img/c75d0c4fa51711b62f211459ae794f3f_396_0.png)

## 图 10-2
数据库结构相当直观。

### 备注

### 让你的表脱颖而出

可复用组件使用与托管它的应用程序相同的数据库。为了指示哪个表属于哪个组件，可复用组件项目中的每个表都使用 `homeproject_` 作为前缀。这是经过深思熟虑的选择，以便当此应用程序部署在现有网站中时，可以轻松识别属于该应用程序的表。例如，查看以下表列表：

- admins
- customers
- blogentries
- homeproject_projects
- homeproject_releaserversions

你可以很容易地识别出哪些表属于该应用程序。

## 实现数据库

启动 phpMyAdmin。创建一个名为 *phphomeproject* 的新数据库，并添加以下表：

### *homeproject_projects* 表

- *id*。将其设为 `MEDIUMINT` 并开启 `auto_increment`。将此字段设置为主键。
- *name*。将其设为长度为 100 的 `VARCHAR`。
- *about*。将其设为 `TEXT`。
- *pathname*。将其设为长度为 30 的 `VARCHAR`。

### *homeproject_releaseversions* 表

- *id*。将其设为 `INT` 并在 `Extras` 列中开启 `auto_increment`。将此字段设置为主键。
- *project_id*。将其设为 `INT`。
- *version*。将其设为 `VARCHAR` 并将大小设置为 20。

### *homeproject_releasestypes* 表

- *id*。将其设为 `TINYINT` 并开启 `auto_increment`。将此字段设为主键。
- *type*。将其设为 `VARCHAR` 并将大小设置为 20。

### *homeproject_releasefiles* 表

- *id*。将其设为 `INT` 并开启 `auto_increment`。将此字段设置为主键。
- *type_id*。将其设为 `TINYINT`。
- *date*。将其设为 `DATETIME`。
- *version_id*。将其设为 `INT`。
- *filename*。将其设为长度为 50 的 `VARCHAR`。

### *homeproject_screenshots* 表

- *id*。将其设为 `INT` 并开启 `auto_increment`。将此字段设置为主键。
- *project_id*。将其设为 `INT`。
- *name*。将其设为长度为 50 的 `VARCHAR`。

## 插入示例数据

当拥有一套稳固的表后，你现在可以添加一些示例数据。请记住，不要在 *id* 列中填入数字，因为 *auto_increment* 会自动为你处理这一点。你可以自由添加自己的示例数据，或者使用以下部分中建议的信息。

### homeproject_projects 表的示例数据

添加一个如表 10-1 所示的项目。

**表 10-1** 此表包含主要项目详情。

| 名称 | 关于 | 路径名 |
| :--- | :--- | :--- |
| 我的项目 | 这是一个示例项目，展示如何在此可复用项目管理应用程序中管理项目。 | myproject |

pathname 字段提供用于引用项目的唯一字符串。这在 Web 应用程序的某些部分中都会用到，最显著的是在 URL 中，例如 `localhost/sites/homeproject/<pathname>/`。

### homeproject_releaseversions 表的示例数据

添加表 10-2 中所示的版本号。

**表 10-2** 因为一个版本号可能有多个发布，所以将版本号存储在专用表中。

| PROJECT_ID | VERSION |
| :--- | :--- |
| 1 | 0.1 |
| 1 | 0.2 |

### homeproject_releasestypes 表的示例数据

添加三条记录，使用以下名称：

- Tarball
- Debian Package
- Windows ZIP

### `homeproject_releasefiles` 表的示例数据

在此表中添加两条记录，使用正确的 `version_id` 和 `type_id`。`filename` 字段应包含发布文件的名称（例如 `myrelease.tar.gz`）。当你稍后创建 `releases` 目录时，请记住在该目录中放置一个具有相同文件名的文件。

### `homeproject_screenshots` 表的示例数据

在表中添加几条记录，使用正确的 `project_id`。`name` 字段应包含截图的名称（例如 `myscreenshot.png`）。当你稍后创建 `screenshots` 目录时，请记住包含具有相同名称的图像。

## 智能使用目录

与书中的以前项目不同，`phphomeproject` 广泛使用目录来确定特定类型的功能。该项目有三个主要目录：`base`、`admin` 和 `project`。

基目录（例如 `www.mysite.com/projects`）是网站上的基础项目目录。此目录包含构成 `phphomeproject` 的不同文件。此目录还包含一个 `index.php` 文件，用于列出服务器上的项目，以便用户可以选择要查看的项目。

项目目录（例如 `www.mysite.com/projects/myproject`）是基目录内的子目录。此目录包含单个 `index.php` 文件（包含基目录中的文件，如图 10-1 所示）。该项目还包含两个子目录：`releases`（存储软件发布）和 `screenshots`（存储截图）。

`admin` 目录是站点管理员用于调整项目设置的目录。此目录也位于基目录内，例如 `www.mysite.com/projects/admin`，并包含用于管理站点的多个文件。

## 创建目录

首先，创建基目录并将其命名为 `homeproject`。然后创建 `admin` 子目录。

对于每个项目，你还需要在 `homeproject` 内部创建一个子目录。该目录的名称应与 `homeproject_projects` 表中的 pathname 字段相同。如果你按照本示例添加了“我的项目”记录，请创建一个名为 `myproject` 的目录。在 `myproject` 内创建 `releases` 和 `screenshots` 子目录。务必确保对 `releases` 和 `screenshots` 都有写入访问权限。

你现在应该拥有以下目录：

- homeproject
  - admin
  - myproject
    - releases
    - screenshots

![](img/c75d0c4fa51711b62f211459ae794f3f_400_0.png)

## 开始编码：构建骨干

开发 *phphomeproject* 需要两个核心领域：

- 可查看的项目信息。这是网站访问者看到的区域。访问者可以查看项目信息、下载和截图。
- 项目管理。这是用于配置项目的界面；只有站点管理员才能访问此界面。

在本项目中，你将首先实现项目查看区域，然后继续创建管理区域。在开始之前，你将创建一些结构性文件（配置文件、函数等）。

由于此项目可作为可复用组件提供，因此你应该为项目特定设置使用单独的配置文件。在 *homeproject* 目录内，创建 *phphomeproject.php*，然后添加示例 10-1 中显示的代码。

**示例 10-1** 配置文件独立于网站的主要配置文件。

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

除了正常的数据库设置外，此配置文件还包括许多其他选项：

- `$config_headerfile` 和 `$config_footerfile`。Web 应用程序中页眉和页脚文件的位置。
- `$config_projecturl`。可以找到 phphomeproject 的 URL。
- `$config_projectdir`。包含 phphomeproject 的目录。在将新发布和截图复制到 releases 和 screenshots 目录时，使用此目录。
- `$config_projectadminbasedir`。admin 目录的位置。
- `$config_projectadminfilename`。用于访问管理功能的文件名称（例如 admin.php）。
- `$config_projectscreenthumbssize`。查看截图时应设置的缩略图宽度。

重要的是要记住，你正在一个独立的目录中开发 phphomeproject，它与现有的网站是独立的。当 phphomeproject 部署在应用程序中时，这些设置需要更改以反映现有的站点（例如，将 `$config_projecturl` 更改为 `http://www.mysite.com/projects/`）。你将在本章稍后部署该站点。

