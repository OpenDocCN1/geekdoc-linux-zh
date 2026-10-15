

Listing 29.7 shows the new script.

```php
<?php
    include("DB.php");
    $dsn = "mysql://ubuntu:alm65z@10.0.0.1/dentists";
    $conn = DB::connect($dsn);

    if (DB::isError($conn)) {
        echo $conn->getMessage() . "\n";
    } else {
        echo "Connected successfully!\n";
    }

    $result = $conn->query("SELECT ID, Name FROM patients;");

    while ($result->fetchInto($row, DB_FETCHMODE_ASSOC)) {
        extract($row, EXTR_PREFIX_ALL, 'pat');
        echo "$pat_ID is $pat_Name\n";
    }
?>
```

前半部分与之前的脚本完全相同，所有新操作都在成功连接后执行。

遵循“能自己清理就不要交给 PHP”的说法，当前脚本存在问题。我们没有清理查询结果，也没有关闭数据库连接。如果这段代码在运行数分钟的较长脚本中使用，这将是巨大的资源浪费。幸运的是，我们可以通过调用 `$result->free()` 和 `$conn->disconnect()` 来释放与这两者相关的内存。如果我们在脚本末尾添加这两个函数调用，脚本就完整了。

### Reference

- http://www.phpbuilder.net—一个大型 PHP 脚本和教程网站，你可以在那里学习新技术并与其他 PHP 开发者聊天。
- http://www.zend.com—由两位 PHP 核心开发者创立的公司的主页。Zend 开发并销售专有软件，包括功能强大的 IDE 和代码缓存，以帮助 PHP 开发者。
- http://pear.php.net/—PEAR 项目的家园，包含大量可下载尝试的软件，并且对所有内容都有详尽的文档。
- http://www.phparch.com/—PHP 杂志有很多，但 *PHP Architect* 可能领先。 它会免费在线发布部分文章，其论坛也很不错。

关于 PHP 的优质书籍比比皆是，选择也非常丰富。对于初学者来说，最佳选择是 *PHP and MySQL Web Development*（Sams Publishing），ISBN 0-672-32672-8。对于一本简洁、直截了当涵盖 PHP 各方面的书籍，请查看 *PHP in a Nutshell*（O'Reilly）。最后，对于高级开发者，你可以参考 *Advanced PHP Programming*（Sams Publishing），ISBN 0-672-32561-6。

## CHAPTER 30 C/C++ Programming Tools for Ubuntu

学习如何使用 C 或 C++ 这样的计算机语言可能比学习 shell 脚本更复杂、更困难。你必须学会以机器资源和计算机内部操作方式为思维方式，考虑到操作系统、语言语法和各种开发工具，而不是以用户导向的命令为思维方式。

当然，学习 C 或 C++ 的主要好处是 Linux 及其几乎所有相关软件都是开源的——如果程序不能按你想要的方式工作，你可以修改它！你也可以在几乎所有 Linux 程序的源代码中找到大量“隐藏”的文档，这些文档存在于程序员注释中。

本章重点介绍 Linux 的 C 和 C++ 相关工具，例如 GNU C 编译器集合（GCC）系统，以及 GNOME 和 K 桌面环境（KDE）的原型设计环境。这里介绍的信息介绍了用于编译 C 和 C++ 程序的一些命令，以及相关编程工具的信息。

### IN THIS CHAPTER

- Programming in C with Linux
- Elements of the C/C++ Language
- Using the C Programming Project Management Tools Provided with Ubuntu
- Using the GNU C Compiler
- A Simple C Program
- Graphical Development Tools
- Reference

### Programming in C with Linux

C 是最常与类 UNIX 操作系统如 Linux 或 BSD 关联的编程语言。自 1970 年代以来，UNIX 操作系统及其应用程序的大部分都是用 C 编写的。由于 C 语言不直接依赖于任何特定的硬件架构，UNIX 是最早的可移植操作系统之一。换句话说，构成 UNIX 的大部分代码并不知道也不关心其

