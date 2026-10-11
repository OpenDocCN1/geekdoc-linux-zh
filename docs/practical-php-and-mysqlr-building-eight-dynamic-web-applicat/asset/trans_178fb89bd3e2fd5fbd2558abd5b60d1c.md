
诚挚问候，

```php
$<config sitename Administrator
_MESSAGE _;
mail($mail_email, "Ownership request for " . $mail_subject . " denied!", $mail_body);
$de1sql = "DELETE FROM mod_subowner WHERE id = " . $val1id . 
```

## 移除所有权

在未来的某个时候，很可能有主题的所有者没有时间或意愿继续做出贡献。在这种情况下，你需要确保所有者在必要时可以轻松地将主题设为无人管理（即放弃所有权）。

为了使其尽可能简单，你在控制面板中添加了一个移除所有权的选项，如 9-17 图所示。

为了将主题设为无人管理，使用传递到页面的主题 ID 运行一个查询，将 *subjects* 表中的 `owner_id` 字段更改为 0。然而，在此查询执行之前，会显示另一个确认问题，以防止误操作。

![](img/c75d0c4fa51711b62f211459ae794f3f_389_0.png)

此脚本中使用的代码与 *deletesubject.php* 中的几乎相同。创建一个名为 *removesubown.php* 的新文件，并添加示例 9-10 中所示的代码。

### 示例 9-10 将主题设为无人管理，即将 owner_id 字段设置为 0。

```php
<?php

session_start();
require("db.php");
require("functions.php");

if( !$_SESSION['SESS_USERNAME'] ) {
  header("Location: " . $config_basedir . "login.php");
}

if( pf_check_number( $_GET['subject']) == TRUE) {
  $validsubject = $_GET['subject'];
}
else {
  header("Location: " . $config_basedir);
}

if( $_GET['conf']) {
  $supsql = "UPDATE subjects SET owner_id = 0 WHERE id = " .
  $validsubject . " ;" ;
  mysql_query($supsql);

  header("Location: " . $config_basedir . "userhome.php");
}
else {
  require("header.php");

  echo "<h1>Are you sure that you want to drop this subject?</h1>";
  echo "<p>[<a href='removesubown.php?conf=1&subject=" .
  $validsubject . ">Yes</a>] [<a href='userhome.php'>No</a>]";
}

require("footer.php");
?>
```

## 摘要

编写 CMS（内容管理系统）绝非易事，能走到这一步是你学习过程中的一个真正成就（当然，除非你只是跳过所有工作直接来到这一页体验成果）。该项目包含许多不同的部分，将这些部分整合在一起并维护一个易于使用的应用程序是一个真正的挑战。

与设计类似，CMS 永远不会完成；它们只会被放弃。然而，这个项目仍然有许多功能可以实现。为了继续你的开发，看看你能否添加以下功能：

- 内容编辑。编写功能，使用户能够编辑主题、话题和问题。
- 用户间消息传递。如果一个用户可以给另一个用户发送消息，那将非常有用。
- 删除问题和评论的功能。将内容删除功能扩展至删除问题和评论。
- 将评论合并到问题中的功能。当问题变得对回答该问题有直接帮助时，拥有一个易于使用的系统将评论合并到主要答案中将是很有用的。

*此页特意留白*

# 第 10 章
构建可重用的项目

网络开发者的生活变得越来越艰难。随着涌入网络并使用互联网进行各种用途的人群激增，网络开发者面临着比以往更多的要求。这不仅意味着需要更广泛的应用程序，而且开发的复杂性也在增加。即使是小型企业拥有驱动其主要业务需求的大型复杂网络应用程序也不少见。

解决此问题的方法之一是编写可重用的代码。那些在 IT 行业摸爬滚打好几年的人可能熟悉“可重用”这个流行词，在许多情况下，它确实是有意义的。

以下列表描述了在应用程序中重用现有代码的几种方式：

- **PEAR。** PHP 扩展和应用存储库（PEAR）提供了一个巨大的扩展目录，可以轻松安装和使用。每个 PEAR 模块都是用 PHP 编写的。
- **PECL。** PHP 扩展社区库（PECL）包含一系列需要编译的 PHP 扩展。这些扩展为 PHP 提供了全新的功能，并且速度非常快。
- **其他预制应用程序。** 许多人重用压缩好的项目，可以将其解压到你的网络应用程序中，以满足某些特定功能。一个例子是 Magpie RSS 解析器。

在本章中，你将编写一个旨在嵌入现有网站的应用程序。在此过程中，你将探索编写易于安装、重用和实现的软件所带来的众多挑战。

## 项目概览

对于许多开发者来说，编写解决非常具体任务的小工具并不罕见。这些小型工具通常不值得拥有自己的 SourceForge 账号，甚至不需要像 Trac（http://www.edgewall.com/trac/）这样复杂的项目管理系统。相反，理想的解决方案包括一种简单的程序下载方式和查看截图的途径。为了满足这些要求，你将创建 *phphome-project* 工具。哦，力量。

在应用程序内查看项目时，用户将能够查看以下内容：

- 可用项目。
- 每个版本中的版本范围和下载发布。
- 截图。

这些是大多数网络冲浪者在*探索*软件时寻找的核心功能。

为了使应用程序可重用，需要考虑它是如何工作的以及设置的难易程度。如果不先坐下来强烈地理解各个部分如何拼接在一起，编写可重用的应用是很难做到的，甚至是不可能的。

此应用程序的基本概念是每个项目都有自己的 *project* 目录（如 www.foo.com/projects/myproject/ 或 www.foo.com/projects/ *myotherproject*/）。站点管理员手动创建这些项目目录。

当创建新项目时，会发生两个操作：

- 新项目被添加到数据库。
- 项目目录被创建并填充用于查看和维护内容的文件。

为了尽可能灵活，将此应用程序嵌入现有网站应该非常简单——就像将单个文件包含到普通网页中一样简单（如 *<?php require(”thisapp.php”); ?>*）。但你将如何在不使其变得极其复杂和臃肿的情况下，将所有功能塞进一个页面？

解决此问题的方案如 10–1 图所示。

为了最佳地解释此过程，以下列表列出了从用户访问网站那一刻起发生的事情：

- 用户访问 www.mysite.com/projects/myproject/ 网络地址，并加载 *index.php* 文件。在头部文件和尾部文件之间，包含了一个名为 *project-main.php* 的文件。
- *project-main.php* 文件检查是否存在 `func` GET 变量。如果存在，则使用 *switch* 语句包含相关文件。例如，如果用户点击下载链接，则 `func=download` 作为 `GET` 变量附加。
- 在 *project-main.php* 中的 *switch* 语句中，包含相关文件。在 `func=download` 的情况下，包含 *download.php*；它包含用于显示可用下载的代码。

通过主 *index.php* 文件包含 *project-main.php*，后者又包含诸如 *download.php* 这样的文件，最终的下载功能在 *index.php* 文件中显示给用户。这使得更容易将功能分散到不同的页面，并且 URL 看起来干净且一致。

![](img/c75d0c4fa51711b62f211459ae794f3f_395_0.png)

## 构建数据库

你要创建的数据库如 10-2 图所示。

应用程序内的项目存在于 *homeproject_projects* 中。项目的发布组织在版本中（存储在 *homeproject_releaseversions* 中），实际的发布（下载文件）在 *homeproject_releasefiles* 中描述。*homeproject_releasefiles* 中的每个条目都引用其父版本，来自 *homeproject_releaseversions*。除了父版本外，发布文件还存储 type_

