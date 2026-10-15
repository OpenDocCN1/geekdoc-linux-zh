

- http://www.jython.org—Python 也有一个出色的基于 Java 的解释器，可使其在其他平台上运行。如果你更喜欢 Microsoft .NET，可以试试 http://www.ironpython.com。
- http://www.pythonline.com—Guido van Rossum 从 *Monty Python’s Flying Circus* 中借用了他语言的名字，因此许多 Python 代码示例都使用了偏斜的 *Monty Python* 引用。访问官方 *Monty Python* 网站以提升你的 Python 知识是强烈推荐的！

关于 Python 的真正优秀书籍很少；不过，你可以在 http://www.python.org/main/PythonBooks 上找到一份可供选择的清单。如果你急于立即挑选一本书，选择 *Learning Python*（O’Reilly，ISBN：0-596-00281-5）不会错。

## CHAPTER 25

## Writing PHP Scripts

## IN THIS CHAPTER

- Introduction to PHP
- Basic Functions
- Handling HTML Forms
- Databases
- Reference

本章将从将其用作 Web 脚本语言和命令行工具的角度，向你介绍 PHP 编程的世界。PHP 最初代表 personal home page，因为它是一组 Perl 脚本，旨在简化访客簿、留言板以及常见于主页上的其他交互式脚本的创建。然而，自那些早期日子以来，它已收到两次重大更新（PHP 3 和 PHP 4），以及 PHP 5 中的一次重大修订，PHP 5 是随 Ubuntu 捆绑的版本。

PHP 成功的一部分在于其与数据库的强大集成——其最早的使用几乎总是利用了数据库后端。然而，在 PHP 5 中，引入了两种新的大型数据存储机制：SQLite，它是一种功能强大且本地的数据库系统；以及 SimpleXML，它是一个应用程序编程接口（API），旨在使 XML 解析和查询变得简单。正如你将随着时间的推移所看到的，PHP 开发人员做得非常出色：SQLite 和 SimpleXML 都易于学习和使用。

### NOTE

许多 PHP 包可通过 synaptic 获得。基本包仅称为 php5，但你可能还想添加诸如 php5-ldap、php5-mysql 或 php5-pgsql 之类的扩展。仅选择你计划使用的扩展；否则会浪费系统资源。

## Introduction to PHP

就其外观而言，PHP 是 Java 和 Perl 的结合体，取两者之长并成功融合为一种语言。Java 部分包括强大的面向对象系统、抛出程序异常的能力，以及两种语言都从 C 借鉴的一般编写风格。借鉴自 Perl 的是“它应该就能工作”的理念，其中易用性优先于严格性。因此，你会在 PHP 中发现很多“做同一件事的方法不止一种”。

### Entering and Exiting PHP Mode

与 PHP 的前身不同，你将 PHP 代码嵌入到 HTML 中，而不是相反。在 PHP 之前，许多网站的大部分内容都是标准的 HTML 页面，链接到 Perl CGI 页面以在需要时进行后端处理。有了 PHP，你的所有页面都能够处理并包含 HTML。

每个 .php 文件都由 PHP 处理，PHP 会查找要执行的代码。PHP 将找到的所有文本都视为 HTML，直到找到以下四种情况之一：

- <?php
- <?
- <%
- <script language="php">

第一个选项是进入 PHP 模式的首选方法，因为它保证能工作。

进入 PHP 模式后，你可以通过使用 ?>（用于 <?php 和 <?）；?> 用于 <%）或 </script>（用于 <script language="php">）退出。这种代码示例演示了进入和退出 PHP 模式：

```
In HTML mode
<?php
echo "In PHP mode";
?>
In HTML mode
In <?php echo 'PHP'; ?> mode
```

### Variables

PHP 中的所有变量都以美元符号（$）开头。与许多其他语言不同，PHP 没有为整数、浮点数、数组或布尔值提供不同类型的变量。它们都以 $ 开头，并且可以互换。因此，PHP 是一种弱类型语言，这意味着你不会声明变量包含特定类型的数据；你只需按需使用它即可。

