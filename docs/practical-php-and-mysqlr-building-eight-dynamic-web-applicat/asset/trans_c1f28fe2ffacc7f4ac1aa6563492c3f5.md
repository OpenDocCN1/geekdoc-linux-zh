

## 访问数据库

在基础目录（phpomeoproject）中，创建 *db.php* 并添加示例 10-2 中显示的连接代码。

### 示例 10-2
此文件与其他项目并无不同。

```php
<?php
    require("phpomeoprojectconfig.php");
    $db = mysql_connect($dbhost, $dbuser, $dbpassword);
    mysql_select_db($databatabase, $db);
?>
```

## 创建函数

除了前几个项目中的 *pf_fix_slashes()* 和 *pf_check_number()* 外，本项目还使用两个自定义函数。在基础目录中，创建一个名为 *functions.php* 的新文件，并添加配置文件：

```php
<?php
    require("phpomeoprojectconfig.php");
    
    // 添加 pf_protect_nonadmin_page():
    function pf_protect_nonadmin_page() {
        if(basename($_SERVER['SCRIPT_NAME']) != "index.php") {
            echo "<h1>Error</h1>";
            echo "You cannot access this page directly. Please go to the main project pages directly.";
            exit;
        }
    }
```

*pf_protect_nonadmin_page()* 函数用于保护单个页面免受直接访问。如果你查看图 10-1，你会看到诸如 *download.php* 等页面被包含在 *project-main.php* 中，而 *project-main.php* 又被包含在 *index.php* 中。显然，你不希望用户直接访问 *download.php*。此函数只是检查当前页面的名称是否与 *index.php* 不同。如果是，则显示错误。目前，此函数硬编码为 *index.php*，因此你可能希望调整此代码以使其适用于并非名为 *index.php* 的文件。

使用类似的技术来保护管理页面：

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

这里唯一的区别是，该函数检查管理页面被设置为什么名称。你不能假设管理页面应该称为 *index.php*，因为 *admin* 目录中的 *index.php* 文件可能管理网站的另一个部分。为了解决这个问题，该函数引用了配置文件中的 $config_projectadminfilename 设置。

该函数的第一行使用 **global** 关键字来访问函数作用域之外的变量，并在 **if** 语句中检查该变量。

### 注意
**理解变量作用域**

变量作用域是让许多语言新手感到困惑的问题。基本概念是，变量在其创建的块的作用域内是可访问的。在大多数脚本中，这没有问题，因为变量是在函数外部创建的，因此任何代码都可以访问它。

然而，当你使用函数时，只有函数知道在其内部创建的变量。要在函数外部访问该变量，你需要在使用它之前添加这一行：

```php
global <variableName>
```

变量现在可以访问了。

添加你已知且喜爱的函数：

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

## 主项目

跳转到项目的目录（例如 *myproject* 目录），并根据示例 10-3 中的代码创建 *index.php*。

### 示例 10-3
此文件加载 *project_main.php*，它管理加载哪些功能。

```php
<?php
$project = substr(dirname($SCRIPT_NAME),
    strrpos(dirname($SCRIPT_NAME), "/") + 1);

require("../phphomeprojectconfig.php");
require("../project_bar.php");


require("../project_main.php");
?>
```

此文件的第一行获取当前项目的名称。为此，从 URL 中切出项目路径名称（例如，从 www.mysite.com/projects/myproject/ 中切出 *myproject*）。这可以用于稍后收集关于项目的信息。

然后包括三个文件：主配置文件（*phphomeprojectconfig.php*）、菜单选项（*project_bar.php*）和主应用程序页面（*project_main.php*）。这些文件通过在每个文件前加上前缀 `../` 从前一个目录访问。

![](img/c75d0c4fa51711b62f211459ae794f3f_405_0.png)

## 部署 *phphomeproject*

站点管理员使用 *phphomeproject* 文件在现有的 Web 应用程序内部部署 *phphomeproject*。管理员只需在侧边菜单栏代码（如以前项目中的 *bar.php*）中包含 *project_bar.php*，然后在页面的主体中包含 *project_main.php*。

在接下来的部分中，你将创建刚刚包含的这些文件。

## 查看菜单选项

创建 *project_bar.php* 并添加示例 10-4 中的菜单选项代码。

### 示例 10-4
此文件可以部署在现有设计中，以便轻松地在任何地方显示菜单。

```html
<h1>Options</h1>
<ul>
<li><a href="index.php">Home</a></li>
<li><a href="index.php?func=download">Download</a></li>
<li><a href="index.php?func=screenshots">Screenshots</a></li>
</ul>
```

此文件包含一个简单的无序列表，其中包含不同的选项。每个选项链接到 *index.php*，但向 func GET 变量传递不同的设置。*project_main.php* 处理此变量，并显示相关的功能。

## 访问项目的功能

当用户点击其中一个菜单选项时，project_main.php 充当中间人，提取 func 变量，并提供正确的页面。

为此，func 通过 switch 语句运行。switch 为可用的不同选项提供 case 块。如果不存在 func 变量，或者 func 包含 case 块不满足的内容，则执行 default 块。

在基础目录中创建 project_main.php 并开始添加代码：

```php
<?php
require('db.php');

$sql = "SELECT * FROM homeproject_projects WHERE pathName = '' . $project . ''";
$result = mysql_query($sql);
$row = mysql_fetch_assoc($result);

// Here you run a query to select any projects in which pathname is equal to the directory name held in $project ($project was created in index.php).
```

设置变量：

```php
$row = mysql_fetch_assoc($result);
$project_id = $row['id'];
$project_name = $row['name'];
```

创建两个变量（稍后由用户）来存储项目 id 和名称。

打开 switch 并添加第一个 case 块：

```php
$project_name = $row['name'];
switch($_GET['func']) {
    case 'download':
        require('download.php');
        break;
```

如果用户点击 Download 链接，func 被设置为 download，并且执行该块。download.php 页面被包含在该块内部。

为 Screenshots 链接添加一个类似的块：

```php
break;
case 'screenshots':
    require('screenshots.php');
    break;
```

添加 `default` 块以捕获任何其他情况：

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

你构建了一个返回项目的查询，然后简单地打印项目的名称并显示描述。

最后，关闭 `switch`：

```php
break;
}
?>
```

当你查看 My Project 时，你应该看到一个与图 10-3 中所示的视图没有太大不同的视图。

![](img/c75d0c4fa51711b62f211459ae794f3f_407_0.png)

**图 10-3** 相当无趣的设计可以在应用程序部署到具有现有设计的现有站点时替换。

## 下载发布版本

发布版本是软件项目中最重要的方面。如果你的发布版本难以访问、不稳定或不可用，很少有人会费心下载和使用它们。

该应用程序以非常简单的方式管理发布版本，如图 10-4 所示。

