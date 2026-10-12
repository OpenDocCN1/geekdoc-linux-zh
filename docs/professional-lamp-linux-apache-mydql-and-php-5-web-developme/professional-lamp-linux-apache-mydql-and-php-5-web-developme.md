## LAMP 高级指南





### 作者简介

**Jason Gerner** 目前在辛辛那堤从事网页开发人员的工作，空闲时间通常用来抱怨对网页标准支持不足以及滥用 XML。他经常可以在 PHPBuilder.com 的讨论论坛中找到，他是那里的版主。

**Elizabeth Naramore** 拥有来自俄亥俄州迈阿密大学的组织行为学学士学位，自 1997 年起开始开发网站。她的主要焦点是 PHP/MySQL、电子商务以及自由写作和教学。她的文章可以看到在 PHPBuilder.com 和国际 PHP 杂志上。她是 OINK-PUG（俄亥俄州、印第安纳州、北肯塔基州 PHP 用户组）的自豪成员，她住在俄亥俄州辛辛那堤，与她的丈夫和两个小孩一起生活。

从奥克兰大学获得一个无人感兴趣的数学学位后，**Morgan L. Owens** 在 IT 行业摸爬滚打，成为内联网和互联网环境中基于 Web 应用的后台网页开发人员和程序员。他仍然住在奥克兰，但暗示如果为了正确的职业，他可能——可能——考虑搬家。

**Matt Warden** 开发基于 Web 的应用程序已超过六年。他的工作主要专注于设计和实施 LAMP 应用程序，供其他企业内部使用以提高生产力。最近，Matt 一直使用 AJAX 提供基于 Web 的替代方案，以实现通常只有原生桌面解决方案才能提供的生产力提升。目前，Matt 是俄亥俄州辛辛那堤 Signal US Communications 的主开发人员。

### 制作人员

| 角色 | 姓名 |
| :--- | :--- |
| **执行编辑** | Carol Long |
| **高级采购编辑** | Debra Williams Cauley |
| **开发编辑** | Brian MacDonald |
| **贡献者** | William Barnett, Wm. Christopher Mastin |
| **技术编辑** | Jason Gerner, Elizabeth Naramore |
| **制作编辑** | Kenyon Brown |
| **校对编辑** | Kathryn Duggan |
| **编辑经理** | Mary Beth Wakefield |
| **制作经理** | Tim Tate |
| **副总裁兼执行集团出版人** | Richard Swadley |
| **副总裁兼执行出版人** | Joseph B. Wikert |
| **项目协调员** | Kristie Rees |
| **图形和制作专家** | Carrie Foster, Lauren Goddard, Denny Heger, Barbara Moore, Alicia B. South |
| **质量控制技术人员** | Amanda Briggs, John Greenough, Jessica Kramar, Joe Niesen |
| **媒体开发专家** | Angie Denny, Kate Jenkins, Steve Kudirka, Kit Malone, Travis Silvers |
| **媒体开发协调员** | Laura Atkinson |
| **校对和索引** | TECHBOOKS 制作服务 |

### 致谢

感谢我可爱的妻子在过去几年里的包容和支持。我还要感谢我的合著者们的出色工作以及他们在这个项目上花费的时间。此外，感谢 Wiley 的人给我们机会，并特别感谢 Brian 的巨大帮助以及他对我们的信任。—*Jason Gerner*

我想感谢我的父母，他们总是让我觉得很酷，尽管我并且永远都会是一个书呆子。我还要感谢我的丈夫和孩子们，在我压力大的时候照顾我，并作为我的幽默调剂。也要感谢 Jason 和 Brian 让我们的书得以出版。—*Elizabeth Naramore*

我要感谢 HIT Studios 的 Scott 以及其余的团队成员，特别是他们向我介绍了这个叫“PHP”的东西；感谢我的合著者们，尽管他们看了我的写作风格后仍然邀请我参与这个项目；感谢科罗拉多大学的 Karl Gustafson，多年前给我的一个建议，尽管他毫无疑问不知道我在说什么；以及我的朋友和家人，他们真的是我的生命支持系统——特别是我的祖母 Doris Madeline Rachael Shipton (1918–2005)。—*Morgan L. Owens*

特别感谢 Sam Foster，在我们最初试图确定 XMLHTTP 和 XMLHttpRequest 对象使用的最佳实践时，他通过电子邮件与我合作，当时关于这个主题的资料非常少。他的想法启发了 RemoteConnection 对象设计的许多方面。—*Matt Warden*




### 引言

围绕LAMP的所有炒作到底是怎么回事？“LAMP”是什么，我又该如何拥有一个？这些问题将在本书的页面中得到解答。在这种情况下，LAMP代表*Linux、Apache、MySQL和PHP*，并被证明是开发企业级Web应用最快的增长方式之一。所有这些包都是开源的，因此你基本上可以随意使用它们：唯一的限制是你自己的想象力。此外，使用开源技术，你不仅有业界最优秀的头脑协作提供出色的包，如果遇到问题，你还能得到开源社区其余成员的庞大支持。读完本书后，你对LAMP的知识将得到扩展，并可以在开发动态网站时将其付诸实践。由于目前这是唯一一本可获得的进阶LAMP书籍，且是Irox专业系列的一部分，你可以放心，书中包含的信息将帮助你成为更好的编码者，并领先于其他人。

需要注意的是，尽管“LAMP”一词在更广泛的定义中也可以包含*Perl*和*Python*，但我们在本书中选择了专注于*PHP*。

本书的目标是帮助初中级Web开发者更进一步，为他们配备更高级的每个模块的知识。我们在书中为你提供工具，让你能够“跳出框框”思考，并为旧问题找到新的解决方案。

### 本书适合谁？

本书适合那些希望将网站提升到下一个级别的有一定经验的Web开发者。如果你对使用开源工具运行动态、引人入胜的网站感兴趣，你会在这里找到你需要的东西。我们假设阅读本书的人在这些领域有一定的基本经验：

- Web服务器技术
- OO编码
- 数据库结构、设置和交互（检索、修改和添加数据）
- 设置用户和权限
- 安装新软件
- 使用命令行

虽然如果你拥有一个当前熟悉的*LAMP*设置会有帮助，但这并非必需。只要你熟悉安装新软件，就可以轻松地将*Apache、MySQL*和*PHP*一起安装。也有软件包可以一次性为你完成这三个模块的安装，例如*XAMPP*（可在<http://www.apachefriends.org/en/xampp.html>获取）。

读完本书后，你将能够自信地克服任何LAMP障碍，为可能希望编写的未来应用拥有一些很棒的新想法，或以新的效率和力量重构你的一些旧代码。



### 本书涵盖内容

本书涵盖了多种主题：

- PHP 5.0 新特性的指南
- 对 PHP 中面向对象（OOP）的深入讨论
- 代码效率、基准测试以及结果优化
- 为最佳性能配置 PHP
- 高级 MySQL 查询
- Apache 技巧与窍门
- 本地和远程站点安全
- 使用高级 PHP 扩展
- 常见的 PEAR 包
- Ajax 和 PHP
- 晦涩的 PHP 命令
- CMS（内容管理系统）的比较与解析
- 博客程序包
- 从其他编程语言过渡的指南
- 缓存引擎

### 使用本书所需条件

本书旨在配合 Linux 机器使用，但书中的许多信息同样适用于 Windows 用户。你需要 PHP、MySQL 和 Apache 来完成书中的练习。这三个都是开源程序，因此你可以免费下载和使用。你还需要一个文本编辑器来输入代码。最后，你需要一个网络浏览器，如 Internet Explorer、Netscape Navigator、Firefox、Safari 或 Opera，来查看你的网页。

正如任何程序员都知道的那样，软件在不断改进和调试。虽然我们在出版时使用了模块的最新最佳版本，但这些版本很可能很快就会过时。重要的是，你要访问 PHP、Apache 和 MySQL 的源网站，以获取最新更新版本和最近的发布说明。在使用应用程序开发网站时，我们建议你始终使用最新稳定版本。使用未经充分测试的软件版本可能会对你的应用程序造成危险，并会在代码中留下漏洞。对于新学习者也是如此——你应该在应用程序的稳定版本上学习，而不是在测试版（beta version）上学习。

在本书撰写时，最新稳定版本如下：

- **PHP：** 版本 5.0.4（可在 `http://www.php.net` 获取）
- **Apache：** 版本 2.0.54（可在 `http://www.apache.org` 获取）
- **MySQL：** 版本 4.1.12（可在 `http://www.mysql.com` 获取）

本书的后续版本将针对这些程序的变化和改进进行说明。

### 排版约定

为了帮助你最大限度地利用文本内容并跟踪当前发生的事情，我们在整本书中使用了一些约定。

> **像这样的方框包含重要且不可忽视的信息，这些信息与周围文本直接相关。**

*当前讨论的技巧、提示、窍门和附带说明会以斜体形式偏移放置，如下所示。*

关于文本中的样式：

- 当我们引入重要单词时，我们会*突出显示*它们。
- 我们展示 URL 的方式如下：`http://www.mysite.com`
- 我们在文本中展示代码的方式如下：`persistence.properties`
- 我们以两种不同方式展示代码：

> 在代码示例中，我们用灰色背景突出显示新代码和重要代码。

灰色高亮不适用于在当前背景下不那么重要的代码，或之前已经展示过的代码。

### 源代码

在按书中的示例进行操作时，你可以选择手动输入所有代码，或者使用随书附带的源代码文件。本书中使用的所有源代码均可在 `http://www.wrox.com` 上下载。进入网站后，只需找到书名（使用搜索框或书名列表之一），然后单击书籍详情页面上的“下载代码”链接，即可获取本书的所有源代码。

*由于许多书标题相似，通过 ISBN 搜索可能最方便。本书的 ISBN 是 0-7645-9723-X。*

下载代码后，只需使用你喜欢的压缩工具解压缩即可。或者，你可以访问 Wrox 代码下载主页 `http://www.wrox.com/dynamic/books/download.aspx`，查看本书及其他所有 Wrox 书籍的可用代码。

### 勘误表

我们尽全力确保文本或代码中没有错误。然而，人无完人，错误难免发生。如果你发现我们书中的错误，如拼写错误或代码故障，我们将非常感激你的反馈。提交勘误信息可以节省其他读者数小时的挫败感，同时你也将帮助我们提供更高质量的信息。

要找到本书的勘误页面，请前往 `http://www.wrox.com`，并使用搜索框或书名列表之一找到书名。然后，在书籍详情页面上，单击“书籍勘误”链接。在此页面上，你可以查看所有已提交并由 Wrox 编辑发布的本书勘误信息。在 `www.wrox.com/misc-pages/booklist.shtml` 还提供了一份完整的书籍列表，其中包含每本书勘误信息的链接。

如果你在书籍勘误页面上没有发现“你的”错误，请前往 `www.wrox.com/contact/techsupport.shtml` 并填写那里的表格，将发现的错误发送给我们。我们会检查信息，并酌情在书籍勘误页面发布消息，并在后续版本中修复问题。

### p2p.wrox.com

为了进行作者和同行讨论，请加入 `p2p.wrox.com` 的 P2P 论坛。论坛是一个基于 Web 的系统，允许你发布与 Wrox 书籍及相关技术相关的信息，并与其他读者和技术用户互动。论坛提供订阅功能，当论坛有新帖子时，可以将你感兴趣的主题通过电子邮件发送给你。Wrox 作者、编辑、其他行业专家以及你的同伴读者都会在这些论坛上出现。

在 `http://p2p.wrox.com` 上，你会找到许多不同的论坛，它们不仅有助于你阅读本书，也有助于你开发自己的应用程序。要加入论坛，只需按以下步骤操作：

1. 前往 `p2p.wrox.com` 并单击“注册”链接。
2. 阅读使用条款并单击“同意”。
3. 填写加入所需的必填信息以及你希望提供的任何可选信息，然后单击“提交”。
4. 你将收到一封电子邮件，其中包含有关如何验证你的帐户并完成加入流程的信息。

你可以不加入 P2P 就阅读论坛中的消息，但为了发布自己的消息，你必须加入。

一旦加入，你就可以发布新消息并回复其他用户发布的消息。你可以随时在 Web 上阅读消息。如果你希望将特定论坛的新消息通过电子邮件发送给你，请单击论坛列表中论坛名称旁边的“订阅此论坛”图标。

有关如何使用 Wrox P2P 的更多信息，请务必阅读 P2P 常见问题解答（FAQS），以获取关于论坛软件工作原理以及许多特定于 P2P 和 Wrox 书籍的常见问题的答案。要阅读常见问题解答，请单击任何 P2P 页面上的 FAQ 链接。

# 专业 LAMP

## PHP5 有什么新特性？

那么 PHP5 的大新闻是什么？如果你熟悉 PHP4，你可能知道面向对象编程以及 PHP4 如何处理它。如果你不熟悉 PHP，但熟悉其他编程语言，你可能会发现 PHP5 对面向对象原则的实现很熟悉。幸运的是，随着 PHP5 的发布，事情变得更加简单。然而，除了“更好的面向对象编程”处理之外，还有其他改进和变化，例如 php.ini 中更多的配置选项，以及一系列新的数组相关和其他函数。本章概述了这些变化。

### 面向对象的变化

以下变化涉及 OOP 模型及相关特性和主题。这些变化中的大多数在第 2 章中有更详细的介绍，但这里也简要概述以供你快速参考。

### 传递对象

PHP5 中 OOP 变化的一个重大影响是变量作为参数传递给函数的方式。在 PHP4 中，默认情况下变量是按值传递的，而不是按引用传递的，除非使用语法 `& $varname` 另行注明。在 PHP5 中，默认是按引用分配值。

### 异常

简而言之，异常是出错时发生的过程。当程序遇到意外错误时，它不会完全停止，你现在可以更多地控制程序在遇到该错误时应如何执行。你可能熟悉 PHP4 中可用的 `set_error_handler( )` 函数。如果不熟悉，这个函数的目的是定义一个用户函数用于错误处理。然而，它的实现有很多限制。例如，如果错误类型是 `E_ERROR`、`E_PARSE`、





# 第 1 章

## Try/Catch/Throw

`E_CORE_ERROR`、`E_CORE_WARNING`、`E_COMPILE_ERROR`、`E_COMPILE_WARNING` 以及大部分的 `E_STRICT`。此外，如果错误发生在 `set_error_handler()` 函数脚本之前，该函数将永远不会被调用。PHP5 带来了处理异常的新框架。

如果你之前有 C++ 或 Java 等语言的编程经验，你肯定听说过“try”、“catch”和“throw”这些术语。当发生错误时，异常会被“抛出”。可能会引发错误的代码被放在 `try/catch` 块中，尝试运行（在 `try` 下），如果抛出异常，则会被“捕获”并应采取用户定义的操作（在 `catch` 下）。`try/catch/throw` 块的语法如下：

```php
<?php

try
{
    $error_message = 'Hello, I am an error.';
    throw new Exception($error_message);
}
catch (Exception $e)
{
    echo 'Exception caught: ',  $e->getMessage(), "\n";
}
?>
```

## 内置异常类

你刚才看到的类 `Exception` 也是 PHP5 的一项改进，并且默认是内置的。在 PHP5 中，你现在可以获取已抛出异常的信息，并使用该数据做出适当的反应。处理并存储该数据的内置异常类如下所示：

```php
<?php

class Exception
{
    protected $message = 'Exception Thrown';
    protected $code = 0;
    protected $file;
    protected $line;

    function __construct($message = null, $code = 0) {
    }
    final function getMessage();
    final function getCode();
    final function getFile();
    final function getLine();
    final function getTrace();
    final function getTraceAsString();
    final function __toString();
}
?>
```

## PHP5 有什么新变化？

仔细看看 *Exception* 类：

| 成员或方法名 | 代表内容 |
| --- | --- |
| $message | 异常消息；默认值可以设置为你喜欢的任何内容 |
| $code | 用户定义的代码 |
| $file | 发生错误的文件名 |
| $line | 发生错误的行号 |
| getMessage() | 返回 $message |
| getCode() | 返回 $code |
| getFile() | 返回 $file |
| getLine() | 返回 $line |
| getTrace() | 返回包含 `debug_backtrace()` 函数信息的数组 |
| getTraceAsString() | 返回与 `getTrace()` 函数相同的结果，但以格式化字符串形式呈现 |
| toString() | 一种 PHP5 魔术方法，当与 print 或 echo 一起使用时，允许对象被格式化为字符串 |

在前面的 try/catch/throw 示例中，我们使用内置 *exception* 类中的 *getMessage()* 函数来返回并显示错误消息是什么。

## 扩展内置异常类

显然，内置异常类是该类最通用的形式。虽然它在很多情况下非常有用，但有时你可能希望以更有针对性的方式处理异常。例如，在发送电子邮件时，如果收件人的电子邮件地址为空，你并不会收到 PHP 错误。除非你在监控 *sendmail* 日志，否则你可能不会知道你的电子邮件未被发送。这是一个有用的信息，因此你可以轻松地使用 *extends* 关键字扩展内置类，如下所示：

```php
<?php

class emailException extends Exception
{
    function __construct($message)
    {
        echo "There was an error sending your email: <br \>";
        echo $message;
    }

    function sendEmail($to, $subject, $message)
    {
        if ($to == NULL)
        {
            throw new emailException('Recipient email address is NULL');
        }
        mail($to, $subject, $message);
    }

    try
    {
        sendEmail('', 'Exception Testing', 'We are testing the exception handling in PHP5');
    }
    catch (emailException $e)
    {
        echo 'in file <strong>' . $e->getFile() . '</strong>';
        echo ' on line <strong>' . $e->getLine() . '</strong>';
    }
}
?>
```

这将产生以下结果：

```text
There was an error sending your email:
Recipient email address is NULL in file /usersites/email_exception.php on line 11
```

你能够访问存储在内置异常类中的文件名和行信息，但你还可以添加更详细的错误消息以用于调试目的。

## set_exception_handler() 函数

默认情况下，任何未捕获的异常都会导致致命错误并停止脚本执行。PHP5 允许你使用 `set_exception_handler()` 函数清理任何未捕获的异常。类名、错误消息和回溯会被传递给 `set_exception_handler()` 函数，但你也可以访问内置异常类的信息。该函数的用法如下：

```php
<?php
function lastResort ($e)
{
    echo 'Previously uncaught exception being caught from ' . get_class($e);
    echo ' in file: ' . $e->getFile() . ' on line ' . $e->getLine();
}
set_exception_handler('lastResort');
throw new Exception();
?>
```

你的结果将类似于这样：

```text
Previously uncaught exception being caught from Exception in file:
/usersites/set_exception_handler.php on line 9
```

请注意，你必须在使用 `set_exception_handler()` 函数时给你的函数名加上引号；否则你会收到一个通知，说你正在尝试使用未定义的常量。

#### 接口

PHP5 增加了接口，允许你将类绑定到多个位置。它们由空函数（将在实现类中定义）和你想要应用到实现类的任何常量组成。接口的所有实现类都必须提供接口中定义的每个方法的实现，从而确保你代码的未来用户知道预期有哪些方法。

接口将在第 2 章中更详细地讨论。

## 迭代器

通过标准公共库（SPL），你可以访问一组全新的类和接口，允许你操作和利用迭代器。SPL 是一个扩展，默认情况下在 PHP 中编译和可用，基本上是一个供你使用的接口和类库。下一节将讨论 `Iterator` 类本身。你会发现许多函数与数组函数类似。

### 主要迭代器接口

`Iterator` 类是一个内置接口，允许你循环遍历任何可以用 `foreach()` 语句循环遍历的内容——例如，文件目录、查询结果或数据数组。它具有某些固有功能：

- `Iterator::current()`: 返回当前元素。
- `Iterator::key()`: 返回当前元素的键。
- `Iterator::next()`: 将指针移动到下一个元素。
- `Iterator::valid()`: 在调用 `next()` 或 `rewind()` 后验证是否存在元素。

通过预定义通用的 `Iterator` 功能，这些功能都有助于你使用迭代使代码更强大、更高效。关于 `Iterator` 接口最重要的一点是，它是其他 `Iterator` 类的构建块之一。

### 其他迭代器类

以下各节简要描述了一些继承自 `Iterator` 类的主要类。关于以下任何类的更详细信息以及更全面的列表，可以在在线 SPL 文档中找到：`http://www.php.net/~helly/php/ext/spl/main.html`。

#### DirectoryIterator

顾名思义，`DirectoryIterator` 是一个实现了 `Iterator` 的 `Iterator` 类，允许你处理文件目录。该类中包含一个强大的函数集，可以获取关于每个文件的信息，如修改时间和日期、文件大小、文件类型、文件所有者、文件的完整路径以及与文件关联的权限（仅举几例）。

#### RecursiveIterator

`RecursiveIterator` 类有助于递归迭代，即函数自动重复调用直到达到特定标准。随该类提供的函数帮助你确定是否存在子迭代器，以及这些子迭代器可能是什么。

#### ArrayIterator

利用 `ArrayIterator` 内置类，你可以在迭代对象时修改数组的值和键。它允许你在每次迭代中操作数组。诸如 `append()`、`copy()` 和 `seek()` 等函数使程序员能够超越常规的一组数组函数来操作数组。

迭代器正在不断改进和增强，你可以预期在 PHP 5.1 中看到一些重大变化。

## 构造函数和析构函数

在 PHP4 中，你可以通过将方法命名为与类名相同来立即在类中调用方法。在 PHP5 中，有一个新的“魔术方法”名称用于此目的，称为 `__construct()`。通过在类中包含此方法，当对象创建时它将自动被调用。

同样，当类中包含魔术方法 `__destruct()` 时，对象将被销毁。此方法在调用时销毁对象。如果不再引用你的对象，或者到达 PHP 脚本的末尾，`__destruct()` 方法也将被调用。

第 2 章包含对构造函数和析构函数的更深入讨论。

## 访问修饰符

你现在可以通过 PHP5 的三个新关键字 `public`、`private` 和 `protected` 来控制类成员和方法的可见性级别。方法被标记为 public、private 或 protected。

以下是 `private`、`protected` 和 `public` 关键字的简要总结（你可以在第 2 章中阅读有关这些属性的更多信息）：

- *Public*：这些成员和方法可用于整个脚本。它们可以从对象内部或外部引用。
- *Protected*：被标识为 protected 的成员或方法仅可从对象内部或继承类中访问。
- *Private*：Private 方法和成员仅可从对象本身内部访问，任何继承类都无法访问。

#### final 关键字

`final` 关键字可以与类或类内的方法一起使用。当与类一起使用时，此关键字阻止任何其他类继承它。当与方法一起使用时，它防止任何继承类重写该方法，从而有效确保其永久性，并保护它们免受其他程序员甚至你自己的影响。




### static 关键字

将一个成员或方法声明为 static（静态）会将其绑定到其所在的类，而不是类的某个对象或实例。静态成员和方法可以在整个脚本中访问。

关于 static 关键字的使用，有一些重要的注意事项。首先，不应该在类内部使用 `$this->varName` 语法来访问变量，而应使用 `self::varName`。在前面的示例中，你从不同的函数中访问了 `self::$count` 成员，但由于静态成员对类内部的任何部分都可用，因此你仍然使用了 `self::$` 语法。其次，当在类外部访问静态成员时，应使用 `className::varName` 语法。同样，当在类内部的任何地方访问静态方法时，应使用 `self::methodName()`；当在类外部访问时，应使用 `className::methodName()`。

关于 static 关键字的用法在第 2 章中进行了更详细的讨论。

## abstract 关键字

当你有一个高层类，并且知道它需要被更具体的低层类继承时，就会使用 abstract（抽象）关键字。例如，你可以按以下方式使用抽象类和抽象方法：

```php
<?php

abstract class getToday {
    public $today = getdate();

    abstract function showCalendar();
}

class monthlyCalendar extends getToday {
    function showCalendar() {
        //show this month's calendar
    }
}

class dailyCalendar extends getToday {
    function showCalendar() {
        //show today's daily calendar
    }
}

class yearlyCalendar extends getToday {
    function showCalendar() {
        //show the calendar for this year
    }
}
?>
```

这个抽象类基本上说的是“创建一个日历，但你必须在子类中指定具体类型”。如你所见，第一个类中的 `showCalendar()` 函数是故意留空且抽象的，因为该类应该被扩展，并基于被调用的继承类显示合适的日历。`getToday()` 类是不完整的，是抽象化的完美候选对象。

抽象方法（就像接口中的那些）实际上是空的，需要在子类中进一步实现。

使用抽象类的一些规则包括：

- 如果你有一个抽象方法，整个类也必须定义为抽象类。
- 你无法实例化一个抽象类。
- 你可以将一个类定义为抽象类，即使其中不包含任何抽象方法。
- 实现了抽象方法的继承类必须具有与其父类相同（或较弱）的可见性。

在第 2 章中，我们将更详细地讨论抽象化。

## 内置方法重载函数

与 PHP4 不同，在 PHP4 中你需要使用 `overload()` 函数来强制进行重载检查，而 PHP5 原生允许你重载任何不符合预期的方法或成员引用，从而有效地让你控制接下来发生的事情。新的魔法方法 `__get()`、`__set()` 和 `__call()` 用于重载，如下所示：

```php
<?php

class overload {

function __get($property) {
    //check to see if the property exists within the class
    //and if not, do something we want it to
    //such as show an error. Otherwise return
    //a value.
}

function __set($property, $value) {
    //check to see if the property exists within the class
    //and if it does, set it to the value being passed
    //otherwise do something we want it to, such
    //as show an error.
}

function __call($method, $array_of_arguments) {
    //check to see if method exists within the class
    //and if not, do something such as defer it to
    //another class containing the method or
    //print an error statement.
}
}
?>
```

第 2 章将更详细地讨论重载。

## 新函数

以下是 PHP5 中所有新函数的综合列表，需要扩展的函数除外：

- array_combine()：将两个数组合并为一个，使用一个数组作为值，另一个作为键。
- array_diff_assoc()：确定两个或多个数组之间的差异，通过附加的键比较来确定，由指定函数决定。
- array_udiff()：通过使用指定函数进行数据比较，确定两个或多个数组之间的差异。
- array_udiff_assoc()：确定两个或多个数组之间的差异，具有附加的键比较，并使用指定函数进行数据比较。
- array_udiff_uassoc()：确定两个或多个数组之间的差异，使用指定函数进行附加的键比较，并使用指定函数进行数据比较。
- array_intersect()：确定两个或多个数组之间的交集，使用指定函数进行数据比较。
- array_intersect_assoc()：确定两个或多个数组之间的交集，具有附加的键比较，并使用指定函数进行数据比较。
- array_intersect_uassoc()：确定两个或多个数组之间的交集，使用指定函数进行附加的键比较，并使用指定函数进行数据比较。
- array_walk_recursive()：递归地对数组的每个元素应用一个指定函数。
- convert_uudecode()：解码 uuencoded 字符串。
- convert_uuencode()：对字符串进行 uuencode 编码。
- curl_copy_handle()：复制 cURL 句柄及其所有偏好设置。
- date_sunrise()：基于给定的纬度、经度、天顶角和 GMT 偏移量返回日出时间。
- date_sunset()：基于给定的纬度、经度、天顶角和 GMT 偏移量返回日落时间。
- dba_key_split()：将字符串表示中的索引拆分为数组表示。
- dbase_get_header_info()：返回 dBase 数据库的列结构信息。
- dbx_fetch_row()：从查询结果中获取行，但如果查询中未设置 DBX_RESULT_UNBUFFERED，则失败。
- fbsql_set_password()：更改命名用户的密码。
- file_put_contents()：等同于打开文件、写入文件和关闭文件。
- ftp_alloc()：向 FTP 服务器发送 `ALLO` 命令，该命令为上传的文件预留空间。
- get_declared_interfaces()：返回脚本中声明的任何接口。
- get_headers()：返回服务器响应 HTTP 请求时发送的标头。
- headers_list()：返回已发送（或准备发送）的响应标头列表。
- http_build_query()：根据给定的数组构建 URL 编码的查询字符串。
- ibase_affected_rows()：返回受前一个查询影响的行数（Interbase）。
- ibase_backup()：在服务管理器中启动备份任务并立即返回（Interbase）。
- ibase_commit_ret()：提交事务，然后返回而不关闭它（Interbase）。
- ibase_db_info()：返回有关数据库的信息（Interbase）。
- ibase_drop_db()：删除一个数据库（Interbase）。
- ibase_errcode()：返回一个错误代码（Interbase）。
- ibase_free_event_handler()：释放已注册的事件处理程序（Interbase）。
- ibase_gen_id()：递增并返回递增后的值（Interbase）。
- ibase_maintain_db()：在数据库服务器上执行维护命令（Interbase）。
- ibase_name_result()：为结果集命名（Interbase）。
- ibase_num_params()：返回命名查询中的参数数量（Interbase）。
- ibase_param_info()：从命名查询中返回参数信息（Interbase）。
- ibase_restore()：在服务管理器中启动恢复任务并立即返回（Interbase）。
- ibase_rollback_ret()：回滚事务而不关闭它（Interbase）。
- ibase_server_info()：返回有关数据库的信息（Interbase）。
- ibase_service_attach()：连接到服务管理器（Interbase）。
- ibase_service_detach()：与服务管理器断开连接（Interbase）。
- ibase_set_event_handler()：注册一个用户定义的函数，在特定事件后调用（Interbase）。
- ibase_wait_event()：等待数据库发布事件（Interbase）。
- iconv_mime_decode()：解码 MIME 头字段。
- iconv_mime_decode_headers()：同时解码多个 MIME 头字段。




iconv_mime_encode()：创建 MIME 头部字段。

iconv_strlen()：返回字符串的字符数。

iconv_strpos()：在字符串中查找指定字符首次出现的位置。

iconv_strrpos()：在字符串的指定范围内查找指定字符最后一次出现的位置。

iconv_substr()：返回字符串的一部分。

idate()：将本地时间/日期格式化为整数。

imagefilter()：对图像应用指定滤镜。

image_type_to_extension()：返回图像文件的扩展名。

imap_getacl()：返回指定邮箱的 ACL（访问控制列表）。

ldap_sasl_bind()：使用 SASL 将资源绑定到 LDAP 目录。

mb_list_encodings()：返回所有受支持的编码的数组。

pcntl_getpriority()：返回 pid 的优先级。

pcntl_wait()：暂停当前进程，直到子进程退出，并返回子进程的 id。

pg_version()：在数组中返回客户端、协议和服务器的版本。

php_strip_whitespace()：从源代码中移除注释、空白和换行符，并返回结果。

proc_nice()：根据给定的增量值改变当前进程的优先级。

pspell_config_data_dir()：设置语言数据文件的位置。

pspell_config_dict_dir()：设置主要单词列表的位置。

setrawcookie()：等同于 setcookie()，但不值不对值进行 URL 编码。

snmp_read_mib()：读取并解析 MIB 文件到活动的 MIB 树中。

sqlite_fetch_column_types()：从给定表中返回适用的列类型。

str_split()：将字符串拆分为字符数组。

stream_copy_to_stream()：在流之间复制数据，并返回复制的数据量。

stream_get_line()：类似于 fgets()，但允许使用指定分隔符。

stream_socket_accept()：接受来自之前使用 stream_socket_server() 函数创建的套接字的连接。

stream_socket_client()：打开到 Internet 或 Unix 域目的地的流。

stream_socket_get_name()：返回套接字连接的名称。

stream_socket_recvfrom()：从套接字接收数据，直到指定长度。

stream_socket_sendto()：向指定套接字发送数据，无论其是否已连接。

stream_socket_server()：在指定服务器上创建流。

## 第 1 章

- `strpos()`：在字符串中搜索给定字符列表中的任意一个字符，并返回从首次匹配成功实例开始的字符串剩余部分。
- `substr_compare()`：使用指定偏移量及可选的大小写敏感性比较两个字符串。
- `time_nanosleep()`：将脚本的执行延迟指定的秒数和纳秒数。

有关这些函数的更多信息，请访问源网站 http://www.php.net。

### PHP5 的其他更改

除了对象面向编程（OOP）更改的清单和大量可用的新函数外，PHP5 的发布还进行了其他一些改进。

### 配置更改

在 PHP5 中，php.ini 配置文件有许多更改。这些在第五章中会有更详细的讨论，但这里列出了一个列表供您参考：

- mail.force_extra_parameters
- register_long_arrays
- session.hash_function
- session.hash_bits_per_character
- zend.zel_compatibility_mode

通过这些新指令，您可以对 PHP 环境施加更多控制，从而在编码时获得更大的自由度。

### MySQLi

正如大家所知，MySQLi 与 PHP 搭配使用，非常适合交付数据库驱动的动态网站。因此，MySQLi（MySQL improved，即改进的 MySQL）扩展的发布使每个人的生活变得更加轻松。

### 配置设置

php.ini 中有几个新的 MySQLi 配置设置。以下是简要说明：

- `mysqli.max_links`：设置每个进程的 MySQL 最大连接数。
- `mysqli.default_port`：设置连接 MySQL 服务器的默认 TCP/IP 端口。
- `mysqli.default_socket`：设置连接 MySQL 服务器的默认套接字名称。
- `mysqli.default_host`：设置连接 MySQL 服务器的默认主机名。
- `mysqli.default_user`：设置连接 MySQL 服务器的默认用户名。
- `mysqli.default_pw`：设置连接 MySQL 服务器的默认密码。

PHP5 有什么新功能？

#### 内置类和属性

随着 mysqli 扩展而来的是一组新的内置类和属性，您可以在 PHP 脚本中访问这些类和属性。如果您的脚本是面向过程而非面向对象的，这些新方法也可以作为函数使用。要以面向过程的方式调用函数，只需在方法名前使用 mysqli_ 语法即可。例如，若要通过 OOP 创建新连接，您将键入以下内容：

```php
<?php
$connect = new mysqli("server", "user", "pass", "dbname");
//call methods through the mysqli class
$connect->close();
?>
```

若要使用传统的面向过程编程实现相同功能，您将键入以下内容：

```php
<?php
$connect = mysqli_connect ("server", "user", "pass", "dbname");
//call functions using mysqli_ prefix
mysqli_close($connect);
?>
```

以下章节描述了 PHP5 中固有的函数类型。

##### class mysqli

该类处理基本的 MySQL 连接。该类的构造函数创建一个新 PHP/MySQL 连接，从而创建一个新的 mysqli 对象。您可以使用该类来操纵或检索有关当前连接的信息，或执行基本查询功能。

该类可用的方法有：

- auto_commit：切换事务是否自动提交到数据库。
- change_user：切换到另一个用户。
- character_set_name：返回默认字符集。
- close：关闭数据库连接。
- commit：将事务提交到数据库。
- connect：打开到 MySQL 数据库服务器的新连接（也是 mysqli 构造函数）。
- debug：使用 Fred Fish 调试库进行调试。
- dump_debug_info：使用 Fred Fish 调试库转储调试信息。
- get_client_info：检索有关客户端的信息。
- get_host_info：检索有关连接的信息。
- get_server_info：检索有关 MySQL 服务器的信息。
- get_server_version：检索当前 MySQL 服务器版本。
- info：返回关于最近执行的查询的信息。
- init：在调用 real_connect 函数之前初始化对象。
- kill：终止 MySQL 线程。
- more_results：查找之前调用的 multi_query 的结果。
- multi_query：执行一个或多个查询。
- next_result：返回之前调用的 multi_query 的下一个结果。
- options：更改或设置 real_connect 对象的连接选项。
- ping：Ping 服务器连接，如果没有连接则重新连接。
- prepare：准备单个 SQL 查询语句以供执行。
- query：执行查询。
- real_connect：连接到 MySQL 数据库服务器，并允许设置额外的选项或参数。
- real_escape_string：返回转义字符串，以便在 SQL 语句中有效使用。
- rollback：回滚当前事务。
- select_db：选择指定数据库作为活动数据库。
- set_charset：设置要使用的字符集。
- ssl_set：设置 SSL 参数，启用安全连接。
- stat：返回有关系统状态的信息。
- stmt_init：初始化语句，以便与 mysqli_stmt_prepare 一起使用。
- store_result：从上一个查询传输结果集。
- thread_safe：返回是否给予线程安全。
- use_result：从上一个查询传输非缓冲结果集。

该类可用的属性如下：

- affected_rows：获取上一个 MySQL 操作受影响的行数。
- client_info：以字符串形式返回 MySQL 客户端版本。
- client_version：以整数形式返回 MySQL 客户端版本。
- errno：返回最近一次函数调用的错误代码。
- error：返回最近一次函数调用的错误字符串。
- field_count：返回最近一次查询的列数。





host_info：返回表示连接类型字符串。

info：获取最近执行查询的相关信息。

insert_id：返回上一个查询中使用的自动生成 ID。

protocol_version：返回使用的 MySQL 协议版本。

sqlstate：返回包含上一个错误 SQLSTATE 错误代码的字符串。

thread_id：返回当前连接的线程 ID。

warning_count：返回执行前一个 SQL 语句期间产生的警告数量。

##### mysqli_stmt

此类处理预处理语句，即由 MySQL 服务器临时存储以备使用的 SQL 语句。预处理语句的一个示例是 "SELECT * FROM customer WHERE lastname = ?"。然后，当你准备执行该语句时，你只需填入 lastname 的值即可。请注意，当你在过程式编程中将这些方法作为函数使用时，你需要在方法名称前加上 mysqli_stmt_ 前缀（例如 mysqli_stmt_close）。

此类可用的方法如下：

- bind_param：将变量绑定到预处理语句。
- bind_result：将变量绑定到预处理语句以存储结果。
- close：关闭预处理语句。
- data_seek：在语句结果集中定位到任意一行。
- execute：执行预处理语句。
- fetch：将预处理语句的结果获取到绑定变量中。
- free_result：释放给定语句句柄的存储结果内存。
- prepare：准备 SQL 查询。
- reset：重置预处理语句。
- result_metadata：从预处理语句获取结果集以获取元数据信息。
- send_long_data：分块发送数据。
- store_result：将预处理语句的完整结果集缓冲到内存中。

此类可用的属性如下：

- affected_rows：返回上次语句执行影响的行数。
- errno：返回上一个语句函数的错误代码。
- error：返回上一个语句函数的错误消息。
- param_count：返回给定预处理语句的参数数量。
- sqlstate：返回包含上一个语句函数 SQLSTATE 错误代码的字符串。

# 第 1 章

##### mysql_result

此类表示从数据库查询获得的结果集。您使用此类来操作和显示查询结果。

此类可用的方法如下：

- close：关闭结果集（在过程式编程中称为 mysqli_free_result）。
- data_seek：移动内部结果指针。
- fetch_field：从结果集中获取列信息。
- fetch_fields：从结果集中获取所有列的信息。
- fetch_field_direct：获取指定列的列信息。
- fetch_array：将结果行作为关联数组、数字数组或两者兼有检索出来。
- fetch_assoc：将结果行作为关联数组检索出来。
- fetch_object：将结果行作为对象检索出来。
- fetch_row：将结果行作为枚举数组检索出来。
- field_seek：将结果指针移动到指定的字段偏移量处。

此类可用的属性如下：

- current_field：返回当前字段指针的偏移量。
- field_count：返回结果集中的字段数量。
- lengths：返回列长度的数组。
- num_rows：返回结果集中的行数。

如您所见，新的 mysqli 类可以帮助您编写更高效的代码，并为您提供对 PHP 4 中可用的 MySQL 函数的额外灵活性和控制能力。

## XML 支持

PHP5 在 XML 库方面比 PHP4 有了改进。有几个使用 libxml2 编写的新 XML 扩展，旨在提高标准化和维护性：

- **DOM**：这组新函数取代了 PHP4 中的 DOMXML 函数。它们已被重新设计，以符合 W3C 发布的 DOM Level 2 标准。
- **XSL**：以前被称为 XSLT 扩展，该扩展使用 W3C 的 XSL 样式表作为标准，协助将一个 XML 文件转换为另一个文件。
- **SimpleXML**：这组函数允许您简单轻松地提取 XML 文件中的数据。然后，您可以使用通用的数组迭代器 foreach() 来操作、显示和比较属性和元素。

## PHP5 的新特性？

- SOAP：SOAP 扩展允许您编写 SOAP 服务器和客户端，并且需要安装 GNOME XML 库（libxml）。

第 8 章将更详细地讨论 XML 扩展。

## Tidy 扩展

PHP5 现在支持 Tidy 库，该库可在 http://tidy.sourceforge.net/ 获取。它协助开发人员清理和完善 HTML 代码。该扩展可在位于 http://pecl.php.net/package/tidy 的 PECL 库中获取。若要查看可用的 Tidy 函数和类的完整列表，您可以访问 http://us2.php.net/tidy 处的 PHP 手册。

### SQLite

尽管 SQLite 是在 PHP4 的后期版本中引入的，但它针对 PHP5 进行了改进。SQLite 类似于一个迷你 SQL 服务器。PHP5 内置了众多类和方法，并随 PHP5 的安装一起捆绑提供。有关 SQLite 的更多信息，请访问其源网站：http://sqlite.org。

### 摘要

虽然 PHP5 对 OOP 模型的重新设计无疑是比 PHP4 最大且最好的改进，但还有许多其他方面也得到了改进，以使 PHP 开发人员的处境稍微轻松一些。

PHP 的一个最优秀方面在于，它始终通过渐进式改进不断变革和成长，正如任何开源语言应该做的那样。构成 PHP5 的这些小幅改进将帮助您更好地使用 MySQL，简化您的代码，并让您更好地访问 XML 的强大功能。然而，最大且最好的改进是 OOP 模型的引入。使用 OOP 而不是过程式编程将从根本上改变您思考代码的方式。在下一章中，您将了解如何充分利用 PHP 中的这个新模型。

# 2

### PHP5 OOP

当您开始一个新项目时，您必须考虑的第一件事就是代码的结构。无论您是在编写像在线联系表单这样简单的东西，还是像全功能内容管理系统这样复杂的东西，您组织代码的方式都会影响最终产品的性能和可维护性。

当使用 PHP 这样的语言时，您可以走两条主要路线：过程式编程和面向对象编程（简称 OOP）。每种策略都有其自身的优缺点。

### 过程式编程与 OOP

过程式编程通常强调编写尽可能简洁的代码，并直接针对最终结果进行编码。换句话说，大多数过程式编程使用有针对性的函数组，直接解决手头的问题——通常不多也不少。在大多数情况下，这能让您获得极其高效且高性能的应用程序。这种方法的一个缺点是缺乏可维护性。如果项目变得足够大，开发人员可能最终需要维护大量单独的函数，在某些情况下，不同函数的逻辑可能会变得令人困惑地相似。

另一方面，面向对象编程（OOP）强调抽象关系和相关的功能层次结构。类似的功能可以共享一个共同的核心，从而使维护变得更加容易。代码复用率也会增加，因为您可以轻松地将抽象的基础功能适应于新任务。OOP 还可以辅助大型程序设计，帮助封装和分类系统各部分所需的不同功能集。然而，这种组织和模块性可能带来代价。如果您的面向对象系统设计不良，它实际上可能比任何替代方案都更难维护。通常，面向对象设计的极端模块化和“代码繁重性”可能会导致性能不佳。





一旦你克服了由糟糕的面向对象设计引起的问题，你会发现使用一套自定义的 PHP 对象，甚至是一个完整的 APL（抽象编程语言）来创建系统，能带来大多数开发者都会感激的益处。至此，你可以开始了解 PHP5 是如何实现面向对象编程的。

### 基本类定义

面向对象 PHP 中的基本代码单元是*类*。简而言之，类是一种将相关功能和数据封装在一个实体中的方式。这种封装可用于向外部代码隐藏内部操作，并有助于简化与数据的外部交互。类是一组代码的*正式描述*，如果你愿意的话，可以把它看作是一种程序化配方。类本身，就像配方一样，只是一组指令的集合，并不是可以直接使用的东西——你不会直接吃掉配方本身，对吧？要使用类，你需要创建该类的一个实例，称为*对象*——这类似于使用配方来制作一道你实际可以吃的菜。类定义了一组代码的特性和行为，而对象则是这组命令的个别实例。

理解类的一种简单方法是将类代码与物理对象联系起来。很多时候，类会代表这些现实世界中的对象。你可能会有一个名为 CAR（汽车）的类，它有一个名为 occupants（乘客）的属性，该属性可能用于追踪车内的人数。它甚至可能包含一个名为 brake()（制动）的方法，该方法将执行与其同名的任务。像许多现实世界中的物品一样，类具有描述单个对象的属性组合，在 OOP（面向对象编程）中称为*属性*，以及它们可以执行的一组动作，在面向对象世界中称为*方法*。

### 定义类

在 PHP5 中定义类是一个相对直接的过程——与定义函数非常相似，只是关键字不同：

```php
class Circle { // 类代码放在这里 }
```

此代码通过使用 `class` 关键字，后跟类名，以及一组大括号来定义一个简单的类。

在标准的 PHP5 类中，类定义主要有两个部分——属性和方法。属性表示对象中持有的数据，而方法则使用这些数据执行操作。

### 属性

在 PHP5 中创建类时，属性是你将存储对象所表示的各种数据片段的地方。

在 PHP5 中定义属性非常简单，如下所示：

```php
visibility $property_name;
```

在此定义中，`visibility` 表示属性的代码可见性，它是三个值之一：`public`（公共）、`private`（私有）或 `protected`（受保护）。这三个关键字的含义将在本章后面进行讨论。

属性定义的第二部分，`property_name` 只是你希望属性拥有的名称。

例如，假设你想创建一个名为 `Circle` 的类。你可能想要有一个公共属性来保存半径，如下所示：

```php
class Circle
{
    public $radius;
}
```

可选地，你可以在定义中为属性指定初始值。假设你希望 `Circle` 的初始半径设置为 10；你可以这样做：

```php
class Circle
{
    public $radius = 10;
}
```

然后，每次创建 `Circle` 对象时，它都会以初始半径 10 开始。

### 方法

你创建了属性来在对象内部存储数据，现在你需要创建一种方式来操作这些数据。要执行这些操作，你将在类内部创建函数，称为*方法*。

在 PHP5 中定义方法与在代码的其他地方创建标准函数非常相似：

```php
visibility function function_name (parameters)
{
    // 方法实现放在这里
}
```

与属性定义类似，方法定义需要一个可见性组件。除了可见性前缀外，方法的定义与标准 PHP 函数完全相同——只需使用 function 关键字，后跟函数名称，然后是括号内可选的参数列表。

再次使用 `Circle` 示例，你将添加一个方法来计算圆的面积：

```php
class Circle
{
    public $radius;

    public function calcArea($radius)
    {
        return pi() * pow($radius, 2);
    }
}
```

你简单地创建了一个名为 `calcArea()` 的方法，它接收一个参数 `$radius`，并返回给定半径的圆的面积。

既然你已经创建了这些属性和方法，你需要一种方式来实际使用你的属性和方法。这就引入了*实例化*。

### 使用类：实例

为了访问类的属性并使用类的方法，你需要先实例化该类，或创建该类的实例。当类被实例化时，它会返回该类类型的*单个对象*，你可以使用它。在 PHP5 中，对象实例是使用 **new** 关键字创建的，如下所示：

```php
$c = new Circle();
```

一旦对象被创建，通过“箭头”运算符（连字符后立即跟一个大于号）访问个别属性和方法，如下面的代码所示：

```php
<?php

class Circle
{
    public $radius;

    public function calcArea($radius)
    {
        return pi() * pow($radius, 2);
    }
}

// 创建 Circle 的新实例
$c = new Circle();

// 修改属性
$c->radius = 5;

// 使用一个方法
echo 'The area of the circle is ' . $c->calcArea(5);
?>
```

如果你运行此代码，你会看到类似以下内容：

```
The area of the circle is 78.539816339745
```

查看代码，你会看到从定义类 Circle 开始。然后，你添加了实例化对象的代码：

```php
// 创建 Circle 的新实例
$c = new Circle();
```

最后，你将 `$radius` 属性更改为值 5，并计算了给定半径为 5 的圆的面积：

```php
// 修改属性
$c->radius = 5;

// 使用一个方法
echo 'The area of the circle is ' . $c->calcArea($c->radius);
```

仔细观察前面那段代码，你可能注意到了你在半径属性使用方式上有些笨拙。你显式地设置了半径属性，但随后又将该属性重新作为 calcArea 方法的参数的显式值使用。由于对象内部知道半径属性，因此没有理由显式地将它提供给 calcArea() 方法。为了消除提供半径参数的要求，并使用对象自己的内部半径属性，你需要一种方法来访问它。PHP 为我们提供了一个名为 $this 的引用来实现这样的目标。使用特别命名的变量 $this 就像引用一个实例化的对象，但 $this 引用的是包含它的对象。

修改 Circle 类，如下所示：

```php
<?php

class Circle
{
    public $radius;

    public function calcArea()
    {
        return pi() * pow($this->radius,  2);
    }
}

// 创建 Circle 的新实例
$c = new Circle();

// 修改属性
$c->radius = 5;

// 使用一个方法
echo 'The area of the circle is ' . $c->calcArea();
?>
```

运行代码将产生与上一个例子完全相同的结果——唯一的变化发生在你使用 calcArea() 方法的方式上。由于你在方法内部引用了 Circle 对象的半径属性，因此你不再需要函数定义和方法调用中的参数。

### 可见性

PHP5 面向对象模型的一个新特性是能够为所有类属性和方法指定可见性级别。使用这些新的可见性关键字，你可以向外部代码隐藏类的某些部分，并公开你希望所有人都能访问的其他功能。PHP5 提供三个用于类的可见性级别：public（公共）、private（私有）和 protected（受保护）。

public 可见性意味着属性或方法可供所有希望访问它的外部代码使用。如果未指定方法的可见性，则默认为 public 可见性。

将类成员指定为 private 意味着该属性或方法仅在所属的类定义内部可见。同一类中的所有其他方法都可以访问该私有成员，但该特定类之外的任何代码都不能访问。




# 第 2 章

最后，`protected` 关键字指定该属性或方法仅在定义类内部，以及继承自该定义类的其他类中可用。关于扩展和继承类的讨论将在本章后续部分进行。

> 在 PHP5 下重用 PHP4 类时，务必记住：使用 `var` 关键字定义属性（例如 `var $propertyName`）将被视为 public（公开）属性，并且会发出 E_STRICT 警告。

为类成员指定可见性非常简单，只需在属性或方法声明前添加适当的前缀即可。在你之前定义的 Circle 类中，所有类成员都被定义为 public。现在，你将要改变其中一些旧的类成员为 private，并添加一些新的方法。

```php
<?php
class Circle
{
    private $center = array('x' => 0, 'y' => 0);
    private $radius = 1;

    public function setRadius($radius)
    {
        $this->radius = $radius;
    }
    public function setCenter($x, $y)
    {
        $this->center['x'] = $x;
        $this->center['y'] = $y;
    }
    public function calcArea()
    {
        return pi() * pow($this->radius, 2);
    }
}
?>
```

没有将属性保留为 public，而是将其更改为 private，并创建了函数来设置它们的值。在此类简单情况下，这样做可能有点大材小用，但如果你扩展该应用程序，设置函数可以用于在设置内部值之前对数据进行复杂的计算。这种分离还可以通过验证外部提供的值，允许内部数据变更前增加一层对私有成员的保护。

你可以使用以下代码来使用你修改后的类：

```php
<?php
$c = new Circle();
$c->setCenter(0,0);
$c->setRadius(10);

echo "The area of the circle is " . $c->calcArea() . "\n";

// Attempt to access a private property
echo "The private value of radius is " . $c->radius;
?>
```

如果你运行此代码，你会看到类似以下内容：

```
The area of the circle is 314.15926535898
Fatal error: Cannot access private property Circle::$radius in /www/plamp/ch02/02-002.php on line 31
```

可以看到，它与你之前使用 Circle 类没有太大不同，但由于 public/private 的指定，现在你必须使用方法来访问 `$center` 和 `$radius` 属性，而不是直接访问这些属性。注意当你试图在最后直接访问一个私有成员时发生了什么——发生了一个致命错误。

### 构造器和析构器

在处理类的某些情况下，你可能希望拥有一种方法，以便在对象创建时自动执行操作。你可能想要初始化对象参数或自动调用类方法。也许你希望对象检查本地环境，以确保必要的资源可用，甚至建立初始连接。对于这种情况，PHP 提供了构造器。

构造器不过是一个特殊命名的方法，当对象被实例化时自动调用。在 PHP5 中，要实现构造器，你只需要实现一个名为 `__construct` 的方法。例如：

```php
<?php
class Circle
{
 public function __construct()
 {
 // Perform actions when object is created
 echo "A circle object is being created.\n";
 }
}
$c = new Circle();
?>
```

当你执行这段代码时，你会看到以下内容：

```
A circle object is being created.
```

正如预期的那样，定义在构造器方法内部的代码在对象实例化时自动执行。

> 你仍然可以在 PHP5 中使用 PHP4 风格的构造器（与类同名的方法），但新风格的 `__construct` 方法更受推荐。

与标准方法和函数一样，构造器也可以处理参数。要将参数传递给构造器，在创建对象时，将它们包含在括号内，如下所示：

```php
<?php

class Circle
{
    public $radius;

    public function __construct($r)
    {
        // Perform actions when object is created
        echo "A circle object is being created.\n";
        $this->radius = $r;
    }
}

$c = new Circle(10);
?>
```

在这个例子中，你在创建对象时简单地提供了一个半径参数——在此例中为 10——它由构造器自动解释，进而设置圆在实例化时的半径。

既然你已经有了一种在对象创建时执行操作的方法，接下来我们将看看一种在对象销毁时执行额外操作的方法。PHP5 现在包含了一种特殊方法，当对象被销毁时会被调用，逻辑上称为析构器。当移除对对象的所有引用时，或者在你的代码中手动销毁对象时，会调用对象的析构器。析构器通常用于各种清理任务，例如关闭数据库连接和释放文件句柄。要创建析构器，向你的类添加一个方法，并将其命名为 `__destruct`：

```php
<?php

class Circle
{
    public function __construct()
    {
        // Perform actions when object is created
        echo "A circle object is being created.\n";
    }

    public function __destruct()
    {
        // Perform actions when object is destroyed
        echo "A circle object is being destroyed.\n";
    }
}

$c = new Circle();

// Destroy the circle object
unset($c);
?>
```

运行此代码会给你：

```
A circle object is being created.
A circle object is being destroyed.
```

注意你看到析构器内部放置的消息，而不需要做任何事情。这是因为当脚本执行结束时，PHP 会自动清理对所有对象的引用，从而自动调用对象的析构器。

最后一件需要记住的事情是，与可以拥有参数的构造器不同，析构器不能有任何参数。

### static 关键字

有时在使用面向对象编程时，你可能需要访问类的一个方法，但不需要创建一个完整的对象。为了满足这一需求，PHP5 提供了 `static` 关键字。`static` 关键字是 PHP5 新增的特性，它允许类属性和方法在不实例化类的情况下可用。要使类成员成为静态的，只需在可见性修饰符与属性或方法定义之间添加 `static` 关键字，如下所示：

```php
<?php

class Circle
{
    public static function calcArea($r)
    {
        return pi() * pow($r, 2);
    }
}
?>
```

要使用新创建的静态属性，你只需使用类名，后跟两个冒号，然后是属性名或方法调用：

```php
<?php
$r = 5;
echo "Given a radius of " . $r .
     ", a circle has the area " . Circle::calcArea($r);
?>
```

在浏览器中运行此代码会产生类似以下的结果：

```
Given a radius of 5, a circle has the area 78.539816339745
```

然而，使用静态方法存在一些限制。静态方法不能通过 `$this->` 改变或访问对象变量或方法；它们只能直接访问类中的其他静态属性和方法。

为了访问同一类中的其他静态变量，你可以使用 `self` 关键字，并配合双冒号使用。使用 `self::` 类似于 `$this->`，但仅适用于静态成员。如果你想修改 `Circle` 类以使用静态方法和属性，你可能会做一些类似以下的事情：

```php
<?php
class Circle
{
    private static $radius;

    public static function setRadius($r)
    {
        self::$radius = $r;
    }

    public static function getRadius()
    {
        return self::$radius;
    }
}

Circle::setRadius(5);
echo "Our statically accessed circle has a radius of " .
       Circle::getRadius() . ".\n";
?>
```

快速运行一遍 PHP5 引擎会产生以下内容：

> Our statically accessed circle has a radius of 5.

### 类常量

随着 PHP5 中改进的对象模型，类常量的概念也被引入了 PHP。类常量类似于普通的 PHP 常量，但仅在类的定义内部可用。与标准 PHP 常量一样，它们的值只能被设置为一次标量值——一个简单的数字或字符串——任何试图将常量设置为函数结果的尝试都会导致错误。

在使用类常量时，请记住它们的访问方式类似于静态成员——要访问类常量，必须使用双冒号（`::`）语法。要定义类常量，请在常量名称前使用 `const` 关键字，如下面的代码所示：

```php
<?php
class Circle
{
    const pi = 3.14159265359;

    public function getPi()
    {
        return self::pi;
    }
}

echo "The value of Pi in our Circle class is " . Circle::pi . "\n";
$c = new Circle();
?>
```



# 第 2 章

运行此代码会产生以下结果：

```
The value of Pi in our Circle class is 3.14159265359
To recap, the value of Pi in our Circle class is 3.14159265359
```

在这个示例中，你创建了类常量 Pi，它的值令人惊讶地是数学常数 Pi。然后，你在 `getPi()` 方法中使用了 `$self::` 引用来返回该常量的值。需要注意的是，在访问 `self::Pi` 时，名称 Pi 前面没有美元符号。类常量不使用美元符号前缀，而标准的类变量则使用。

> 创建 Pi 常量仅仅是作为一个示例。PHP 已经内置了一个 `pi()` 函数来返回 Pi 的值。

### 赋值与克隆

你可能已经知道，在标准 PHP 中，将数据赋值给变量有两种方式：按值赋值和按引用赋值。第一种，按值赋值，在设置变量的简单值或复制其他变量时最为常用：

```
$a = 5;
$b = $a;
```

这里你使用的是按值赋值。当 `$a` 的值改变时，`$b` 保持不变；当你赋值 `$b = $a` 时，你只是创建了 `$a` 值的一个副本，并将该值赋给了 `$b`。

然而，按引用赋值略有不同。请看以下示例：

```
$a = 5;
$b =& $a;
```

在这个示例中，你使用 `=&` 运算符进行按引用赋值。在这种情况下，当 `$a` 的值改变时，`$b` 也会随之改变——因为 `$b` 通过引用被赋值为 `$a` 的值，两个变量都指向内存中的同一位置，当该内存中的值改变时，两个变量都会随之改变。

在 PHP5 中，所有对象默认都是按引用赋值的。这种行为与 PHP4 不同，PHP4 默认是按值赋值，除非使用了引用运算符 (`&=`)。在 PHP5 中，如果你想创建一个对象的副本，而不是使用引用，你必须使用 `clone` 语句，如下所示：

```php
<?php

class Circle
{
    public $radius = 10;
}

// 创建原始对象并设置其参数
$original = new Circle();

// 创建克隆的（按引用赋值的）对象
$cloned = clone $original;
$assigned = $original;

// 现在，修改原始的半径值：
$original->radius = 5;

// 显示所有三个对象的状态
echo "\nOriginal:\n";
print_r($original);

echo "\nAssigned:\n";
print_r($assigned);

echo "\nCloned:\n";
print_r($cloned);
?>
```

这段代码将产生以下输出：

```
Original:
Circle Object
(
        [radius] => 5
)

Assigned:
Circle Object
(
        [radius] => 5
)

Cloned:
Circle Object
(
        [radius] => 10
)
```

你可以看到，`$assigned` 指向 `$original` 对象，但因为你克隆了 `$cloned`，从而创建了 `$original` 的一个独立副本，所以当你修改 `$original` 时，它的值不会改变。

### 继承与接口

在 PHP5 中使用面向对象的优点之一，是它允许你将代码分解为逻辑块，以便促进复用。这些经过精心编写的代码块，可以在许多不同的项目中反复使用，让程序员自由编写针对特定问题的代码。

在面向对象编程中，有几种方式可以指定一组方法和属性以便在多个类中使用。第一种，*继承*，允许你定义一组属于基类的属性和方法，并作为更具体类的构建块。第二种，*接口*，允许你规定类必须实现的方法列表。

### 继承

假设你正在创建一个代码库，专门用于操纵不同的几何形状。你在本章中一直使用的 `Circle` 类可以是该库的一部分。在为不同形状——方形、圆形、三角形等——创建不同类时，你可能会发现你在重复所有形状中相似或相同的方法。这是一个使用继承的好机会。

#### `extends` 关键字

假设所有的几何形状类都要画在网格上。因此，它们都需要某种原点 $(x, y)$。你可以在每个不同的类中包含一个原点属性，或者使用 `extends` 关键字，通过继承在一个共享位置定义该属性。为此，你将创建一个名为 `Shape` 的类，它将作为你可能创建的所有几何类的父类。每个具体的几何形状类——无论是 `Circle`、`Square`、`Ellipse` 还是 `Star`——都有一套 `Shape` 提供的基础功能。理解这种父子关系的一个简单方法是使用“*is a*（是一种）”这个短语。在这个例子中，`Circle` *是一种* `Shape`，就像 `Square` *是一种* `Shape`，以及 `Triangle` *是一种* `Shape`。

要使用你的父类 `Shape`，你可以做类似以下的事情：

```php
<?php

class Shape
{
    public $origin = array('x'=>0, 'y'=>0);
}

class Circle extends Shape
{
    public $radius;
}

$c = new Circle();
print_r($c->origin);
?>
```

运行此代码会产生以下结果：

```
Array
(
    [x] => 0
    [y] => 0
)
```

正如你所见，你创建了一个名为 `Shape` 的基类，它定义了一个通用的 `origin` 属性。通过在 `Circle` 的类定义中使用 `extends` 关键字，`Shape` 的所有属性和方法都成为了 `Circle` 对象的一部分。因为 `Circle` 是 `Shape` 的子类，你可以获取 `$origin` 的值，尽管它在 `Circle` 中并未明确定义——它是从 `Shape` 继承来的。

扩展基类时，可以重新定义存在于父类（基类）中的属性和方法。例如：

```php
<?php

class Shape
{
    public $origin = array('x'=>0, 'y'=>0);  
}

class Circle extends Shape
{
    public $origin = 'New origin';
}

$c = new Circle();
print_r($c);
?>
```

这段代码将输出以下内容：

```
Circle Object
{
   [origin] => New origin  
}
```

通过在子类中重新定义基本属性 `$origin`，新定义隐藏了父类的值。方法的行为也是类似的——在子类中重新定义方法会覆盖父方法的功能。例如，请看以下代码：

```php
<?php

class Shape
{
    public $origin = array('x'=>0, 'y'=>0);  
    public function getOrigin()
    {
        return $this->origin;  
    }
}

class Circle extends Shape
{
    public function getOrigin()
    {
        return array('x'=>1, 'y'=>1);  
    }
}

$c = new Circle();
print_r($c->getOrigin());
?>
```

在这个示例中，定义在 `Shape` 父类中的 `getOrigin()` 方法在 `Circle` 子类中被重新定义。当在实例化的 `Circle` 对象上调用 `getOrigin()` 时，它返回 `1,1` 作为原点，而不会调用基类 `Shape` 中的 `getOrigin()` 方法。重新定义的方法会掩盖父类或类中同名的方法。

#### final 关键字

在某些情况下，你希望禁止子类重新定义基类中存在的成员。你可以使用 `final` 关键字来防止属性和方法被重新定义：

```php
class Shape
{
    final public $origin = array('x'=>0, 'y'=>0);
}

class Circle extends Shape
{
    public $origin = 'This is invalid.';
}

$c = new Circle();
?>
```

如果你尝试运行此代码，会发生致命错误：

```
Fatal error: Cannot declare property Shape::$origin final, the final modifier is  
allowed only for methods in /www/plamp/ch02/02-008.php on line 5
```

由于你在基类中 `$origin` 的定义中使用了 `final` 关键字，当你试图在 `Circle` 子类中重新定义它时，导致了致命错误。

请注意，对于属性而言，`final` 关键字并不禁止改变其值——只禁止重新定义。

#### 使用 parent:: 引用

在某些情况下，在子类中重新定义属性或方法后，你可能想引用基类中的原始属性或方法。为了实现这一点，你可以将 `parent` 关键字与前面关于静态成员章节中看到的 `::`（双冒号）结合使用。例如：





# 第 2 章

```php
<?php

class Shape
{
    public function draw()
    {
        echo "Shape::draw() has been called.\n";
    }
}

class Circle extends Shape
{
    public function draw()
    {
        echo "Circle::draw() has been called.\n";
        parent::draw();
    }
}

$c = new Circle();
$c->draw();
?>
```

运行时将显示以下内容：

```
Circle::draw() has been called.
Shape::draw() has been called.
```

在此示例中，你定义了一个继承自基类 `Shape` 的子类 `Circle`。由于你在子类中创建了新的 `draw()` 方法，因此使用 `parent::draw()` 来调用父类中同名函数。以这种方式调用父类方法是在子类中重写基类方法时的常见做法，并且在构造器中调用父类构造器时也非常常用——否则基类的构造器不会被自动调用。

#### 抽象类

在编程或设计过程中，你可能会发现存在诸如 `Shape` 这样的类，这些类需要被创建以赋予子类相同的属性或方法，但本身永远不需要被实例化。之前使用的 `Shape` 类是成为抽象类的完美候选者——你永远不会想直接创建 `Shape` 对象，但对于提供更具体的几何对象子类的功能而言，它是必不可少的。对于这种情况，可以使用 `abstract` 关键字。

当一个类被定义为 `abstract` 时，其他类可以继承它，但它本身不能被实例化。例如：

```php
<?php
abstract class Shape
{
    public $origin = array('x'=>0, 'y'=>0);
}

class Circle extends Shape
{
    // Circle implementation
}

$c = new Circle();
print_r($c->origin);

$s = new Shape();
print_r($s->origin);
?>
```

运行这段代码，你应该会看到类似以下内容：

```
Array
(
    [x] => 0
    [y] => 0
)

Fatal error: Cannot instantiate abstract class Shape in /www/plamp/ch02/02-010.php
on line 17
```

正如通过运行此示例所见，Circle 类如预期地从 Shape 继承，但当你试图单独实例化 Shape 时，发生了致命错误。

既然你已经快速了解了 PHP 中的继承，让我们看看另一种规定对象行为的方式：接口。

#### 接口

PHP5 中另一个新的面向对象特性是创建和使用接口的能力。简而言之，接口是一种指定类必须显式实现哪些方法的方式。这在处理许多相互关联的对象且这些对象依赖于彼此特定方法时非常有用。

通过使用接口，你可以为不同的可互换类指定一组特定的方法。这样，如果你需要替换程序中类包含的功能，你只需要确保替换类实现原始类所暴露的相同接口或函数组即可。

例如，你可能有一个包含方法 `calculateInterest()` 的业务类。在某个时候，你可能希望有多种计算利息的方式，因此你为希望使用的每种算法创建不同的类。假设所有类都实现了一致的接口——即定义 `calculateInterest()` 的接口——那么这些类现在都应该在程序中是可互换的。

在 PHP5 中，使用 *interface* 关键字定义接口，并使用 *implements* 关键字实现接口，如下所示：

```php
interface TwoDimensionalOperations
{
   public function calculateArea();
}

class Circle implements TwoDimensionalOperations
{
   public function calculateArea()
   {
      // Implementation of calculateArea, specific to this Circle class
   }
}
```

通过创建 *interface* *TwoDimensionalOperations*，你随后可以为不同的形状（如 Circle、Square、Triangle、Pentagon 等）创建类，这些类都实现该接口。这样，你可以确信通过实现 *TwoDimensionalOperations*，你的所有形状类都将拥有 *calculateArea* 方法。

使用接口时，重要的是记住以下几点。首先，如果一个类实现了接口但未定义该接口中的方法，将发生致命错误。其次，接口中定义的所有方法都必须具有 public 可见性。

在 PHP5 中，一个类可以同时继承一个基类并实现一个接口：

```php
class Circle extends Shape implements TwoDimensionalOperations
{
   // Circle implementation
}
```

另一个巧妙的小技巧是，接口可以使用 *extends* 关键字从其他接口继承：

```php
interface GeometricOperations
{
    public function getOrigin();
}

interface TwoDimensionalOperations extends GeometricOperations
{
    public function calculateArea();
}

class Circle extends Shape implements TwoDimensionalOperations
{
    // Implement the required methods
    public function getOrigin()
    {
        // Circle->getOrigin() implementation
    }
    public function calculateArea()
    {
        // Circle->calculateArea() implementation
    }
}
```

在这个小示例中，你很容易在基类 Shape 中创建一个方法，并简单地将其扩展到子类 Circle。这种方法虽然可行，但存在局限性，因为 PHP 中的类只能继承一个基类。

然而，PHP5 类可以实现多个接口，用逗号分隔：

```php
interface GeometricOperations
{
    public function getOrigin();
}

interface TwoDimensionalOperations
{
    public function calculateArea();
}

class Circle implements TwoDimensionalOperations, GeometricOperations
{
    // Implement the required methods
    public function getOrigin()
    { // Circle->getOrigin() implementation
    }
    public function calculateArea()
    { // Circle->calculateArea() implementation
    }
}
```

结合继承、多重接口以及接口继承，你可以使用简单的构建模块构建一些复杂且功能强大的应用程序。

#### 魔术方法

为了在使用面向对象编程时使事情变得更简单，PHP5 提供了一组所谓的“魔术方法”。这些魔术方法是所有类的特殊命名方法，在某些场景下会被自动调用。

本章中你已经见过两个魔术方法：`__construct` 和 `__destruct`。它们分别在对象被实例化或被销毁时对应地被调用。PHP5 包含一组魔术方法——你可以实现它们为你的类提供特殊功能。三个魔术方法——`__call`、`__get` 和 `__set`——都允许你访问对象中未显式定义的方法和属性。第六个，`__toString()`，定义了当对象直接被用作字符串时会发生什么。

##### __call

魔术方法 `__call` 允许你在对象的未定义方法被调用时提供动作或返回值。`__call` 魔术方法可用于模拟方法重载，或者在调用对象的未定义方法时提供平滑的错误处理。`__call` 接受两个参数：方法名称以及传递给未定义方法的参数数组。

例如：

```php
<?php

class Circle
{
    public function __call($m, $a)
    {
        echo "The method " . $m . " was called.\n";
        echo "The arguments were as follows:\n";
        print_r($a);
    }
}

$c = new Circle();
$c->undefinedmethod(1, 'a', 2, 'b');
?>
```

运行这段代码时，你会看到类似以下内容：

```
The method undefinedmethod was called.
The arguments were as follows:
Array
(
    [0] => 1
    [1] => a
    [2] => 2
    [3] => b
)
```

这里你定义了一个 `__call` 函数来处理对 `undefinedmethod` 方法的调用。如预期那样，它接收逗号分隔的参数列表并将其转换为数组，该数组由 `$a` 参数捕获。

##### __get 和 __set

魔术方法 `__get` 和 `__set` 允许你指定自定义函数，用于存储和检索类中尚未定义的属性数据。

`__get` 接受一个参数，即属性名称，而 `__set` 需要两个：属性名称和新值。





执行前面的代码时，PHP 会立即识别出该类中不存在名为 'nonexistent' 的属性。由于命名属性不存在，`__set()` 方法会被调用，随后将值赋给新创建的类属性，从而你可以看到以下内容：

> 我们不存在的属性值：5

在这个示例中，你创建了魔术方法 `__get` 和 `__set` 来处理任何未定义的属性访问，并接着使用了一个名为 `nonexistent` 的未定义属性。

##### __sleep

当你使用 PHP 类来存储需要在页面之间或长时间段内持久保存的数据时，你可以使用你喜欢的持久化方法（文件、数据库、会话变量或 Cookie）来存储对象，但对象必须首先准备好。

当你重新读取要存储的对象数据时，请使用 `serialize()` 函数。`serialize()` 函数接受任何复杂的数据结构并将其转换为字符串，该字符串可以使用你选择的方法进行存储。相反地，若要取回你持久化的数据，请使用 `unserialize()` 函数。`unserialize()` 函数接受你的序列化字符串并将其转换回原来的复杂结构。

为了给开发人员在处理对象序列化时提供更大的灵活性，提供了 `__sleep` 和 `__wakeup` 魔术方法。

如果在类中定义了 `__sleep` 魔术方法，它会在对象被序列化之前自动调用。该方法对于关闭数据库连接和清理对象资源极其有用。

`__sleep` 方法还可以返回一个包含要序列化的属性名称或对象值的数组，这在处理大型对象时非常有用。只有必要的数据会被序列化，而其他数据可以被忽略。

##### __wakeup

`__wakeup` 魔术方法执行与 `__sleep` 方法完全相反的操作。当调用 `unserialize()` 时，`__wakeup` 会被自动调用，这对于重置对象值、恢复连接以及其他初始化任务很有帮助。

下面来看一个简单的 `__sleep` 和 `__wakeup` 实际运行的示例。这个示例需要两个文件。第一个文件，你将创建为 `page1.php`：

```php
<?php
session_start();

class Circle
{
    public $radius;

    public $origin = array('x'=>0, 'y'=>0);
    
    public function __sleep()
    {
        echo 'zzzzz';
        return array('radius','origin');
    }

    public function __wakeup()
    {
        echo 'good morning!';
    }
}

$c = new Circle();
$c->radius = 5;
$c->origin['x'] = 3;
$c->origin['y'] = 4;

echo 'Preparing to sleep.....';
$_SESSION['c'] = serialize($c);
echo '<br /><a href="page2.php">Wake the object</a>';
?>
```

第二个文件命名为 `page2.php`：

```php
<?php
session_start();

class Circle
{
    public $radius;

    public $origin = array('x'=>0, 'y'=>0);

    public function __sleep()
    {
        echo 'zzzzz';
        return array('radius','origin');
    }

    public function __wakeup()
    {
        echo 'good morning!';
    }

    echo 'Rise and shine....';
    $C = unserialize($_SESSION['c']);

    echo '<br />The contents of our Circle object are:<br />';
    echo 'Radius: ' . $C->radius . '<br />'; 
    echo 'Origin: (' . $C->origin['x'] . ',' . $C->origin['y'] . ')';
?>
```

在浏览器中加载第一个页面 page1.php，你应该会看到类似于图 2.1 的内容。

![](img/ab27c6ac898db1f934d39fa127b14657_66_0.png)

点击链接，你会被导向 page2.php，在那里你应该会看到类似于图 2.2 的内容。

![](img/ab27c6ac898db1f934d39fa127b14657_67_0.png)

在第一个文件 page1.php 中，你启动了会话以便将对象存储在会话变量中；然后继续创建圆类的类定义：

```php
<?php
session_start();

class Circle
{
    public $radius;
    public $origin = array('x'=>0, 'y'=>0);

    public function __sleep()
    {
        echo 'zzzz';
        return array('radius','origin');
    }

    public function __wakeup()
    {
        echo 'good morning!';
    }
}
```

请注意，你在这里同时创建了 `__sleep` 和 `__wakeup` 的函数。在这种情况下创建 `__wakeup` 方法并不是必须的，但如果你稍后将类定义移动到一个*include*文件中，你所要做的只是剪切和粘贴。还要注意，你在 `__sleep` 中返回了一个字符串数组。这些字符串与 Circle 内部的属性名称相匹配，告诉序列化函数你希望序列化对象的哪些部分，并忽略其他所有部分。

然后你继续实例化圆对象，更改其部分值，将其序列化为会话变量，最后提供一个链接前往 *page2.php*：

```php
$c = new Circle();
$c->radius = 5;
$c->origin['x'] = 3;
$c->origin['y'] = 4;

echo 'Preparing to sleep.....';

$_SESSION['c'] = serialize($c);

echo '<br /><a href="page2.php">Wake the object</a>';
?>
```

查看 *page2.php*，你再次以启动会话的调用开始，并拥有与前一页相同的类定义。在反序列化对象时，该对象的类定义*必须*在调用 *unserialize()* 函数之前存在，无论是直接输入在文件本身中，还是通过 *include* 或 *require* 语句包含进来。

进入 *page2.php* 的核心内容，你从前一页设置的会话变量中反序列化数据，并将一些新重建对象的属性回显到屏幕上：

```php
echo 'Rise and shine.....';

$c = unserialize($_SESSION['c']);

echo '<br />The contents of our Circle object are:<br />';
echo 'Radius: ' . $c->radius . '<br />';
echo 'Origin: (' . $c->origin['x'] . ', ' . $c->origin['y'] . ' )';
?>
```

##### __toString

可以构建到类中的最后一个魔术方法是 `__toString`。正如你可能猜测的那样，`__toString` 返回一个自定义的字符串值，当对象被转换为字符串时会自动使用该值。请看以下示例：

```php
<?php

class Circle
{
    public function __toString()
    {
        return "Automatic string value for Circle";
    }
}

$c = new Circle();
echo "The value of $c is: ";
echo $c;
?>
```

执行这段代码时，会产生以下结果：

> The value of $c is: Automatic string value for Circle

在这个示例中，你添加了 `__toString()` 魔术方法，并在对象被回显到屏幕时使用它来提供值。请注意，在之前的 echo 语句中，你并没有简单地将对象拼接到字符串的末尾，也没有将其包含在双引号字符串内部。

如果你简单地将对象与另一个字符串包含在同一个 echo 语句中，究竟会发生什么？请看以下代码（更改部分已高亮显示）：

```php
<?php

class Circle
{
    public function __toString()
    {
        return "Automatic string value for Circle";
    }
}

$c = new Circle();
echo "The value of $c is: " . $c;
?>
```

运行这段代码时，你会看到以下内容：

> The value of $c is: Object id #1

这绝对不是你所期望的！它没有返回 `__toString()` 方法的值，而是返回了 $c 的对象 id — 与你未定义 `toString()` 时看到的效果完全一样。`__toString()` 魔术方法仅在与 echo 或 print 直接配合使用时才会被调用 — 如果存在其他字符串或强制转换，则会返回对象 id。

### 摘要

正如你所见，PHP5 为你的项目带来了改进得多的对象模型。无论你决定坚持面向过程的编程，偶尔尝试一下面向对象编程（OOP），完全投身于 OOP 路线，还是在两者之间找到一条路径，希望本章中你看到的一些内容能让你继续开始使用 PHP5 的新 OOP 构建你自己的系统。

从这里开始，你将离开 OOP，进入 PHP 语言中一些较深奥的角落。你可能已经知道数组在 PHP 中有多强大，但你可能并不清楚 PHP 有多少函数可以让你利用这种力量。一旦你掌握了这些，我们将向你介绍流（streams）的概念，这将让你可以使用一组通用的函数来处理网络资源和本地文件。





# 3 更晦涩难懂的 PHP

PHP 的一个突出特性是它拥有庞大的内置函数集合，这甚至是在你开始添加可选扩展之前就已经如此。这 arguably 是一种缺陷，因为它使得在特定情况下决定使用哪个函数变得更加困难。许多函数的行为非常相似，以至于有时很难看清它们为何要作为独立的函数存在，比如 `split()` 还是 `preg_split()`？`str_replace()` 还是 `strtr()`？`ksort()`、`asort()`、`rsort()`、`natsort()`、`usort()` 还是 `uksort()`？`strftime()` 还是 `date()`？本书不会深入探讨函数命名或参数顺序缺乏规范性的问题，也不会探讨某些函数仅仅是其他函数别名这一事实。

PHP 函数集存在重叠的一个原因是其早期作为 Perl 后来是 C 语言库的简单封装。熟悉这些语言函数库的用户会发现，它们的 PHP 对应函数使用了相同的名称和调用约定，并叠加了 PHP 的内存管理和类型处理机制。扩展加剧了这种情况——随着不同的 DBMS 暴露出不同的 API，PHP 为它支持的每个 DBMS 引入了不同的函数集。当两个扩展都提供针对两个类似事物的函数时，PHP 会同时提供这两个函数。

随着 PHP 在更多样化的平台上实现并集成到更多样化的环境中，平台无关的函数实现开始被引入。因此，既存在 `rand()`（使用构建 PHP 的 C 编译器提供的任何伪随机数生成器），也存在 `mt_rand()`（在所有平台上具有相同的行为）。与此同时，PHP 开发者致力于向后兼容性；即使引入了新机制，他们也会尽力保留旧的机制，以防有人依赖它们。

因此，PHP 的函数列表激增，像一块在太小模具中膨胀的面包一样鼓胀。据最后一次统计，PHP 手册有 3,630 个函数条目，分布在 129 个章节中，其中 855 个列在手册描述为“核心”的 30 个章节中，或者是捆绑的，需要显式的配置开关才能禁用。这些数字已经过时了。

实际结果是，许多 PHP 程序员像英语使用者一样——他们只使用该语言的一小部分。语言中有些部分他们可能根本用不上。但在 PHP 的一些鲜为人知的角落中，有一些函数没有获得它们应得的关注。这些函数最迟从 PHP 版本 4.3.2 开始就存在于 PHP 中——许多自 PHP 4 早期就已存在。尽管如此，它们常常被忽视，即使它们是手头任务的理想选择。其中一些似乎只在关于它们的教程中被使用。它们绝非该语言唯一的晦涩特性。相反，它们代表了 PHP 环境中一些更强大的核心功能，也是近期版本活跃开发的领域。

本章旨在纠正这种不公正的一部分。

### 数组函数与回调

数组函数允许你访问和操作数组的内容，而无需先将其提取出来。你希望对数组的“每个元素”执行的大多数，如果非全部的话，操作都可以使用这些函数完成，而不需要额外的 `for` 或 `foreach` 循环基础设施。此外，许多数组操作任务需要考虑到整个数组。排序就是这里的明显例子：如果你不看遍数组的所有元素以找到最小元素，就无法将最小元素移到数组的开头。任何尝试编写相当高效的排序算法的人都知道，这项任务并不简单。

由于 PHP 的开发者无法预测你想对数组做的所有事情，大多数数组函数以及相关的数组或数组都接受一个称为回调的额外参数，它指定另一个函数，该函数根据数组函数的作用，用于操纵数组元素，或将它们彼此或与你指定的某个标准进行比较。这样，PHP 只需要提供数组操作更抽象方面的实现，如映射和遍历，而留给你自由提供你选择的具体细节。

回调实际上对于抽象功能非常有用，以致于一组函数被提供出来，允许在几乎任何情况下使用它们。完全可以设想（尽管有些理想化），实现你自己的 OOP 架构，其中对象的“方法”表示为回调的数组。

### 使用回调

考虑以下脚本：

```php
$input_file = file('generic.txt');
foreach($input_file as $k=>$line)
{
    $input_file[$k] = rtrim($line);
}
```

你正在将文本文件作为单行数组加载。PHP 不会丢弃末尾的换行符，所以既然它们已经完成了任务，你想自己丢弃它们。写一个完整的循环并在其中使用两个额外的变量显得冗长。首先，你必须记住 `$line` 是被复制的，所以 `$line=rtrim($line)` 不会起作用，这意味着你必须通过数组和键引用原始值。或者，记住通过编写 `foreach($input_file as &$line)` 来将 `$line` 声明为引用。这两者中的任何错误都意味着最终数组的行不会被修剪。

现在考虑这个：

```php
$input_file = array_map('trim', file('generic.txt'));
```

这行代码达到了相同的效果。`file()` 返回一个包含 `generic.txt` 行的数组；`array_map()` 对数组的每个元素应用函数 `trim()`，并返回结果“修剪过”的数组。

有几个函数抽象了迭代数组的最常见原因，减少了编写循环和其他流程控制语句的需求。虽然仅仅为了写单行代码而写单行代码可能导致难以阅读的代码，但减少程序中的“移动部件”数量有助于降低错误的发生率。

当你有一个数组，并且需要依次对每个元素执行任务时，`array_map()` 和 `array_walk()` 值得考虑。还有其他函数以类似的方式使用所谓的回调函数，省去你自己对数组的每个元素调用函数的麻烦。

回调有两种形式。第一种，也是最常见的，是它只是一个包含函数名的字符串。在上一行代码中，它是 '`trim`'。

> 它必须是一个函数，这就是为什么 *PHP* 手册特别指出 `echo`、`empty`、`include`、`array` 等不是函数的原因。将 'include' 作为你的回调传递会失败。这些被排除的原因是因为它们在解析期间受到特殊对待，并拥有自己的内部结构。

第二种类型的回调用于指定类和对象方法。两者都由两个元素的数组表示，其中第二个元素是方法名，存储为字符串。如果第一个元素是一个对象，那么回调引用该对象的方法：`array($object, 'method')` 引用 `$object->method()`。另一方面，如果第一个元素是一个字符串或字符串变量，那么回调引用命名类的静态方法：`array('thing_factory', 'create_new')` 引用静态的 `thing_factory::create_new()` 方法。

```php
// 在 array_map() 中使用对象的方法作为回调。
// $untidy_array 的每个元素依次传递给 $parser->tidy()，
// 并返回值存储在 $tidied_array 中。
$tidied_array = array_map(array($parser, 'tidy'), $untidy_array);

// 在 array_map() 中使用静态类方法作为回调。
// $untidy_array 的每个元素依次传递给 Parser::tidy()，
// 并返回值存储在 $tidied_array 中
$tidied_array = array_map('Parser', 'tidy'), $untidy_array);
class Parser {
    // 一个示例方法，从单行文本中修剪尾部空白
    // 和以 '#' 开头的 shell 风格注释。
    static function strip_comments($element) {
        $element = preg_replace('/#(.*)$/', '', $element);
        $element = rtrim($element);
        return $element;
    }
}
```




}
$shell_script = file('foo.sh');
$tidied_script = array_map(array('Parser', 'strip_comments'), $shell_script);

在类内部以及对象中，魔术的 self 和 $this 可以在回调中正常工作，表现正如你所期望的那样：`array($this, 'method')` 和 `array('self', 'method')` 将分别被解释为指向 `$this->method()` 和 `self::method()`。关于不允许静态函数使用 $this 等常规限制依然适用。例如：

```
// An object is able to use its own methods in array callbacks, // both on arguments passed to it and on its own properties.
$tidied_code = array_map(array($this, 'tidy'), $this->code_array);
// Class methods are also accessible as callbacks within the class.
```

如果你想检查某个给定的 $variable 的内容是否确实指定了一个可调用函数或方法，布尔函数 `is_callable($variable)` 可以说明这一点。

#### array_map()

你刚才看到了 array_map() 最简单的应用之一，但它可以做得更多。

最重要的是，它可以同时操作多个数组。假设你有两个数组——$arr1 和 $arr2——你想要构建一个由 `func($arr1[0], $arr2[0])`、`func($arr1[1], $arr2[1])`、... `func($arr1[n], $arr2[n])` 组成的数组。作为循环的代码可能类似于以下内容：

```
$new_array = array(); 
for($i=0, $limit=max(count($arr1), count($arr2)); $i<$limit; $i++) { 
    $arg1 = isset($arr1[$i]) ? $arr1[$i] : null; 
    $arg2 = isset($arr2[$i]) ? $arr2[$i] : null; 
    $new_array[$i] = func($arg1, $arg2); 
}
```

请注意，当数组长度不同时，需要测试以确保循环不会因 `func()` 的参数耗尽而运行失败。

现在将其与使用 array_map() 产生的等效代码进行对比：

```
$new_array = array_map('func', $arr1, $arr2);
```

如果那样不起作用，你有权在 bugs.php.net 上提交报告。而且，六个月后当你回来查看代码时，哪一个更难重新熟悉？

array_map() 的另一个技巧源于它能够将 null 作为回调。在这种情况下，其行为可以描述为“接收一堆事物的数组，并返回一堆事物数组的数组”。每个数组的第 0 个元素组合成一个数组，成为结果数组的第 0 个元素；每个数组的第一个元素组合成一个数组，成为结果数组的第一个元素；以此类推。换句话说，如果你将其数组参数视为矩阵的列，`array_map(null, ...)` 返回转置矩阵。这实际上是如果你被允许使用 'array' 作为回调时，`array_map('array', $arr1, $arr2)` 所期望得到的结果。

这个技巧也不局限于每次只能组合两个数组。如果回调函数需要 $n$ 个参数，那么 `array_map()` 需要传入 $n$ 个数组。因此，如果你有一个接受六个参数的函数，以及一组六元组（sextets）的数组，每个六元组你都希望运行该函数并收集所有结果到一个新数组中，`array_map()` 将适用。

> 严格来说，有两个对 `array_map()` 的调用。第一个使用 null 回调，将原始数组 [0…n] [0…5] 取出来并返回转置数组 [0…5] [0…n]，第二个使用回调函数作用于 array[0]、array[1]、… array[5] 的连续元素。

`array_map()` 有两个明显的限制。首先，回调后的每个参数必须是数组。如果你想在整整一个数组的运算中使用单个变量（例如，将数组的所有值限制为某个最大值），那么你必须执行以下操作之一：

- 在全局范围内声明该变量，并在回调函数内部使用 global（这不是最吸引人的选项）
- 使用 `array_fill()` 制作一个重复项的数组（仅当你不介意在变量的独立副本上执行操作，或者变量是一个按引用传递的对象或资源时才有用）
- 最终还是回到使用循环
- 使用其他函数：具体来说，是 `array_walk()`
- 使用编写 OOP 时可考虑的一个选项：将回调设为方法，将变量设为对象的属性

另一个明显的限制是你需要预先知道要映射在一起的数组数量，并在函数调用中明确列出它们所有。你可以通过将输入数组的对应元素包装进一个合并数组的单个元素中，并将该数组的元素传递给回调函数来绕过此问题。但这需要重写回调函数，或者在无法重写时，编写一个包装函数来解包合并的元素并将内容传递给真正的回调。你会意识到，那样做后你就回到了原点。幸运的是，PHP 也提供了解决方案，即本章后面介绍的 `call_user_func_array()`。

#### array_walk()

想象一下，你正在使用 GD Lib 图形绘制扩展来绘制图表，并且有很多数据点需要用不同大小和颜色的圆圈来指示。位置和半径已经按比例缩放到图像坐标，颜色已经分配并通过图像调色板索引（由 `imagecolorallocate()` 返回的）识别。你被提供一个数据点数组，每个元素分别包含 $x$ 坐标、$y$ 坐标、半径和颜色。例如，

```
$data_points = array(
    array(10, 10, 5, $palette['black']),
    array(10, 20, 5, $palette['black']),
    array(20, 13, 5, $palette['darkolivegreen']),
    ...
);
```

查看 PHP 手册，适当的函数似乎是 `imageellipse()`。你的数据与其参数之间的唯一区别在于它期望宽度和高度，而提供的数据只包含半径。但这只是微不足道的区别。首先，定义一个函数：

```
function imagedatapoint($image, $datapoint) 
{ 
    $width = $height = $datapoint[2]*2; 
    imageellipse($image, $datapoint[0], $datapoint[1], $width, $height, 
        $datapoint[3]); 
}
```

然后调用它。

```
foreach($datapoints as $datapoint) 
{ 
    imagedatapoint($image, $datapoint); 
}
```

这实际上相当简单。如果每个数据点是一个关联数组或对象，并且通过名称标识其组件，`imagedatapoint()` 当然会更具可读性。你可以问的一个问题是，为什么要在函数外部有循环？事实上，在图表上绘制多个数据点的可能性比只绘制一个更大。以下是一个示例：

```
function imagedatapoints($image, $datapoints) 
{ 
    foreach($datapoints as $datapoint) 
    { 
        $width = $height = $datapoint[2]*2; 
        imageellipse($image, $datapoint[0], $datapoint[1], $width, $height, 
            $datapoint[3]); 
    } 
}
```

那么 `array_walk()` 可能会怎么做呢？首先，它使用一个回调函数。这实际上是上一个循环的主体。

```
function imagedatapoint($datapoint, $key, $image) 
{ 
    $width = $height = $datapoint[2]*2; 
    imageellipse($image, $datapoint[0], $datapoint[1], $width, $height, 
        $datapoint[3]); 
}
```

然后它进行以下调用：

```
array_walk('imagedatapoint', $datapoints, $image);
```

与 `array_map()` 不同，`array_walk()` 针对原始数组的引用进行操作。因此，如果回调函数按引用接收其数组元素参数，函数可以修改元素的值，并且更改将反映回传递给 `array_walk()` 的数组中。

#### array_filter() 和 preg_grep()

`array_filter()` 的操作很容易从其名称推断出来：给定一个数组，它返回满足给定条件的数组元素，该条件以返回布尔值的函数的回调形式提供（想想 SQL 查询中的 WHERE 子句）。一系列 `array_filter()` 调用可能比单个遍历数组的循环更容易理解，该循环充满了各种测试和分支，旨在决定是否保留特定元素并构建由成功元素组成的新数组。然而，类似于 `array_map()` 的局限性也适用于 `array_filter()`，除了输入数组和回调之外，它不接受任何额外参数。

```
function is_a_square_number($n)
{
    // Fail values unsuitable for sqrt().
    if(!is_numeric($n))
        return false;
    if($n<0)
        return false;

    $square_root = sqrt($n);
    return ($square_root == intval($square_root));
}

$numbers = array(-1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, '!');
$squares = array_filter($numbers, 'is_a_square_number');
// $squares now contains the array (0, 1, 4, 9, 16);
```

由于过滤包含特定模式的字符串是数组过滤任务中如此常见的子类，并且正则表达式在描述此类模式时也常常很有用，PHP 提供了一个专门针对该任务的函数。`preg_grep()`（正如名称所暗示，是 PCRE 函数之一，行为类似于 grep 程序）。它不使用回调函数（而是使用正则表达式），但它为 `array_filter()` 和下一节函数之间做了一个很好的过渡。以下是 `preg_grep()` 语句的示例：

```
// This use of preg_grep takes a listing of the current directory, and retains only
// those file names that end with four digits followed by ".jpg" or ".jpeg".
$images = preg_grep('/\d{4}\.jpe?g$/', scandir('.'));
```

> 对于使用类似 shell 的语法根据更简单的标准过滤目录列表的函数，请参见 glob() 函数。

#### preg_replace_callback()

`preg_replace()` 使用的语法包含 `e` 修饰符开关。当你使用此修饰符时，给定的替换文本被视为 PHP 代码并进行评估，以确定实际的替换文本应该是什么。但试图塞入所有必要的代码很容易变得麻烦。因此，`preg_replace_callback()` 被实现，使得你只需提供一个回调，而无需直接将替换代码写入函数调用中。这可以极大地简化复杂的正则表达式。由于回调函数可以包含任意数量的字符串处理和模式识别代码，`preg_replace_callback()` 中使用的正则表达式只需复杂到足以保证找到所有期望的匹配项，即使某些不需要的匹配项也通过了即可。进一步的测试可以在回调中完成；如果进一步的测试失败，回调只需返回原样匹配即可。（但请注意，如果不需要的匹配项恰好与



# 第 3 章

对于后续期望的匹配项，后者将被遗漏。`preg_replace_callback()` 并不知晓后续测试是否“成功”。

例如，在将电子邮件地址匹配并包装在 `mailto:` 链接中时，如果你想彻底处理，可能会得出一些令人望而生畏的正则表达式。分阶段处理要容易得多。你可以简单地先尝试定位 @ 字符，且其两侧均为非空白字符，如下所示：

```
preg_replace_callback('/\S@\S+/', $text, 'wrap_emails');
```

并将验证匹配字符串确实是电子邮件地址的重任留给回调函数：

```
function wrap_emails($possible_match)
{
    $possible_email = $possible_match[0]; // 回调函数将接收一个数组
    if(is_rfc822_compliant($possible_email)) // 一个假设的函数，
        // 执行所有繁琐的工作
        return '<a href="mailto:'.$possible_email.'">'.$possible_email.'</a>';
    else
        return $possible_email; // 不是电子邮件，原样返回该子串。
}
```

`preg_replace_callback()` 的另一个使用示例是在模板系统中。使用 `preg_replace_callback()` 仅在模板中识别占位符，将其匹配项传递给回调函数后，该函数会进一步仔细检查这些占位符——这一任务因以下事实而变得更容易：它们已经被某个函数从模板的其余部分中分离出来，且该函数同时也在跟踪它们在模板中的来源位置。下面是一个示例：

```
function include_templates($template_name)
{
    if(is_string($template_file))
        $template_file = $template_name;
    else
        $template_file = $template_name[1].'.tpl'; 
    $template = file_get_contents($template_file);
    return preg_replace_callback('/{\include:(\S*)([\s\}\}]*)\}/', 'include_templates', $template);
}
```

这个递归函数假设你的模板文件扩展名均为 `.tpl`，且你在模板中用于包含 foo.tpl 的语法是 {include: foo}。不用说，如果 foo.tpl 本身也包含其他文件，你希望那些包含的文件也能被一并引入。

如果传递给该函数的是一个字符串，则该字符串被解释为模板文件的名称。如果传递的是数组（原因稍后将会明了），则所需的文件名是数组的第二个元素，并在其后附加 `.tpl`。随后，命名文件的内容被读入 `$template`。（这里几乎没有进行错误检查。）

对 `preg_replace_callback()` 的调用会在 `$template` 中搜索匹配 {include: foo} 语法的字符串。包含这些匹配字符串的数组（其中第 0 个元素包含整个匹配字符串，第 1 个元素包含第一个括号内的子字符串），将依次被传递给 `include_templates()`，该函数从数组中提取模板文件的名称，并在调用 `preg_replace_callback()` 后，返回模板文件的内容——其中所有（`{include: foo}` 部分均被相应模板文件的内容所替换）。

遗憾的是，没有 `preg_match_callback()` 或 `preg_match_all_callback()`。但由于回调函数可以执行任何操作，它也可以将传递给它的匹配项存储在某个地方（例如全局变量，或者更优选地是类或对象属性）。然后，它只需返回其参数的第 0 个元素，即可使 `preg_replace_callback()` 将匹配的子串替换为其本身，保持不变。因此，一个地址收集对象可能包含一个像下面这样工作的方法。

```
function collect_email($possible_match)
{
    $possible_email = $possible_match[0];
    if(self::is_rfc822_compliant($possible_email))
        $this->emails = $possible_email;
    return $possible_email; // 原样返回匹配项
}
```

无论上述方法是否存储电子邮件地址，它都原样返回该地址。因此，`preg_replace_callback()` 将把匹配的子串替换为其本身，从而保持原始文本完整。

#### call_user_func_array() 和 call_user_func()

回顾一下在 `array_map()` 章节末尾讨论过的两个明显局限。第一个局限通过 `array_walk()` 解决了。第二个是你需要预先知道究竟有多少个数组要一起映射，并在函数调用中显式列出它们。有时你可能直到运行时才知道这一点。在我的一个程序中，我处理一个数值矩阵（大小可变），它被存储为行的数组（每一行本身也是一个数组），我需要对其进行转置（最终得到一个列的数组）。我可以写一个双重嵌套循环，一个用于迭代行，另一个用于在每一行内迭代，类似如下代码：

```
$transposed_matrix = array();
for($row=0, $row_count=count($matrix); $row<$row_count; $row++)
{
    for($column=0, $column_count=count($matrix[$row]); $column<$column_count; $column++)
    {
        $transposed_matrix[$column][$row] = $matrix[$row][$column];
    }
}
```

即使在编写那个示例代码时，我也不得不停下来好几次，以确保我的行和列方向正确，但通过编写以下代码也可以实现预期效果：

```
$temp = $matrix;
array_push(null, &$temp);
$transposed_matrix = call_user_func_array('array_map', &$temp);
unset($temp);
```

`call_user_func_array()` 是另一个接收回调的函数。它的第二个参数是一个数组，其中列出了要传递给回调函数的所有参数（如果你从回调函数内部调用 `func_get_args()`，得到的也是同一个数组）。为了举例说明，假设 `$matrix` 是 `((1,2), (3,4))`，并跟踪其发生过程：

```
$matrix = array(array(1,2), array(3,4));
$temp = $matrix;
array_push(null, $temp);
$transposed_matrix = call_user_func_array('array_map', $temp);
```

`array_map()` 的第一个参数是回调函数的名称，因此将 `$temp` 的第一个参数设为该回调（在这种情况下，是一个空回调）。这就是为什么我需要 `temp` 变量；`array_push()` 修改的是原始数组，而不是返回一个副本。我本来可以使用 `$transposed_matrix` 本身代替 `$temp` 来冒险操作，从而省去该变量及最后的 `unset()`。这样做是危险的，因为它会稍微降低代码的可读性（将变量作为某事物（`array_map()` 的参数列表），然后在两行后用于完全不同的事物（`array_map()` 调用的结果）。

```
$temp=array(null, array(1,2), array(3,4));
$transposed_matrix=call_user_func_array('array_map', $temp);
```

下面是手动执行 `call_user_func_array()` 的结果。

```
$transposed_matrix=array_map(null, array(1,2), array(3,4));
```

因此，看待 `call_user_func('foo', array(arguments))` 操作的一种方式，就是将其视为接收一个数组并用 `foo(arguments)` 替换 `array(arguments)`。

为了完成示例，评估 `array_map()` 调用：

```
$transposed_matrix=array(array(1,3), array(2,4));
```

`call_user_func_array()` 的实际意义在于，你可以将函数的所有参数存储在一个数组中，而无需知道参数的数量（请记住，许多 PHP 函数接受可变数量的参数，你的函数也可以做到），也无需手动将数组中的每个元素取出并插入到函数调用中。

这个名字稍显冗长的原因还在于，存在一个 `call_user_func()` 函数。它不像 `call_user_func_array()` 那样将回调及其参数作为数组接收，而是显式地接收回调及其参数。正如你可以将 PHP 视为将 `call_user_func_array('foo', array(arguments))` 转换为 `foo(arguments)` 一样，`call_user_func('foo', arguments)` 转换为 `foo(arguments)` 时无需使用中间数组。

听起来它可能有效等同于将 'foo' 放入变量 `$func` 中，然后编写 `$func(...)`。对于普通函数来说，确实如此。但对于对象方法，情况则不同。请试试：

```
<?php

class foo
{

public function bar($a, $b)
{

echo "I'm here! $a! $b! And all that!";
}

}
```




其结果是一个致命错误：PHP 要求函数名必须是一个字符串。与其使用变量函数，不如编写以下代码：

```php
call_user_func($x, '1066', '42');
```

然后你就得到了期望的结果：

```
我来了！1066！42！还有这些！
```

### create_function()

还有最后一道关卡需要克服。到目前为止，提到的所有回调都是预先存在的、写入原始代码中的函数。然而，有时候这还不够好。有时，直到回调需要的那一刻，我们才确切知道函数的形式；或者也许仅仅是因为不想为一个只会执行一次的特定任务而保留整个函数。如果能有一种方式在运行时定义函数；或者更明确地说，不是通过回调的名称而是直接定义，那该多好。

其实已经有方法了：构建一个包含函数文本的字符串，将其包裹在“function whatever (…)”中，然后对它调用 eval()。但问题可能会出现。你必须记住，由于函数只能声明一次，该字符串只能被求值一次；你还必须记住给每个这样的函数一个独特的名称——whatever0()、whatever1() 等等——因此，如果这种创建行为可能会执行多次，那么在执行求值的函数、方法或类中的某处就需要一个某种计数器（可能是静态变量）。当然，如果你还在代码的其他地方这样做，你需要确保在不同地方生成的函数名称不会冲突。一种优雅的方法是拥有一个单一的“函数创建函数”，并使用一个单一的静态变量来防止命名空间冲突，将函数文本传递给该函数，让它计算出一个合适的名称，求值生成的定义，并返回生成的名称作为回调。实际上，你需要传递两个字符串——一个是函数体，另一个是参数列表——它将对结果执行 eval (“function whatever($n_arguments)” $body))。存在可能已经有一个名为 whatever1() 的函数，因此当你的函数试图创建一个新的函数名时，它必须检查是否已定义。还有可能它创建了一个名为 whatever1() 的函数，却没有意识到在程序后续部分你将试图创建另一个名为 whatever1() 的函数。唯一预防这种冲突的方法是强制编码标准，规定不允许声明具有特定形式名称的函数。

但别费那个事了。这样一个函数已经存在，并且它的工作方式正如刚刚描述的那样，还有一个额外的细微之处，可以防止与你自己的函数发生命名空间冲突。PHP 的 create_function() 创建一个匿名函数，这意味着它不出现在 get_defined_functions() 生成的列表中。然而，它确实有一个名称（即使是匿名者也有名字——你只是不知道而已）。首先，在解析和编译时它有一个名称：在它自己的“心智”中（即魔术常量 _FUNCTION_ 的值），它把自己视为 _lambda_func。（术语“lambda 函数”与“匿名函数”同义，源于一种叫做 Lambda 演算的 1936 年计算模型，经由 LISP 引入）一旦它被创建，就有它在程序中其余部分所知的名称，这正是 `create_function()` 作为字符串返回并准备好用作回调的内容。`create_function()` 返回的第一个字符串是 *lambda_1*；第二个是 *lambda_2*，依此类推。好吧，那么*如果*你定义了一个名为 `lambda_1` 的函数，然后使用 `create_function()` 会发生什么？一个是覆盖另一个，出现错误，还是匿名函数被称为 `lambda_2`()？如果这些选项出现在多项选择题中，你可以排除第一个，因为它违反了 PHP 关于函数不可变性本身的规则，剩下的选择是 B 或 C。然而，正确答案是 D，以上皆非。

```php
<?php
function lambda_1($a)
{
    return $a;
}
$anonymous_function = create_function('$a', 'return strev($a);');
echo "匿名函数被命名为 $anonymous_function。\n";
$use_this = 'lambda_1';
echo $use_this('generic string'), "\n";
$use_this = $anonymous_function;
echo $use_this('generic string'), "\n";
?>
```

运行此代码将得到以下结果：

```
    匿名函数被命名为  lambda_1.
    generic string
    gnirts cireneg
```

那么，如果它们具有相同的名称，PHP 是如何知道使用哪一个的？简单的事实是它们*并不*相同。如果你仔细观察代码示例输出的排版和上一段文字，你会发现匿名函数的名称似乎以空格开头。实际上，它不是空格，而是空字符 \x00。这很狡猾；不可能声明具有这种形式名称的函数，也不可能*调用*具有这种名称的函数，因为在两种情况下，源代码中的 NUL 都被 PHP 的词法分析器视为空白而忽略。然而，知道这一点使得手动构造匿名函数的名称字符串字面量成为可能（使用类似 `chr(0)`.'lambda_n' 的代码，或者允许直接插入 NUL 的编辑器）。不过，这可能收益不大，因为一旦你丢弃了原始字符串或*你丢失了*哪个变量包含哪个匿名函数名称的记录，就得你自己弄清楚你想要第三个、第五个还是第 750 个这样的函数。如果你为数组中的每个元素创建不同的匿名函数，即使它们在功能上是相同的，你最终也可能拥有数百个这样的东西。（PHP 并不试图将一个匿名函数与另一个进行比较以查看它们是否包含相同的代码，就像它不试图对普通函数这样做一样；此外，如果你在循环中创建函数，很可能存在部分代码从一次迭代到另一次迭代有所变化——否则，为什么要放在循环中？）如果你能追踪这类事物——例如，假设你以某种方式知道你的 750 个函数将从 10 到 759 编号——那么你不需要保留一个包含所有名称的 750 个字符串数组，通过编写以下代码可以重新创建它：

```php
function recreate_function($lambda)
{
    return chr(0).'lambda_'.$lambda;
}
$lambda_functions = array_map('recreate_function', range(10,759));
```

### 关于数组函数的最后观察

就列出的函数数量而言，数组函数是手册函数列表中最庞大的章节之一：仅略逊于文件系统函数，且紧随字符串处理之后。即使有了回调所允许的抽象程度，为什么会有这么多？并且使用它们如何有助于代码质量？

#### 如此多的数组函数

在 PHP3 和 PHP4 整个过程中，数组函数列表中存在着明显的缺口。有一个函数允许你使用自定义的“小于、大于或等于”定义来对数组进行排序，但没有一个单独的数组函数让你使用自定义的“相同”定义来移除一个数组中与另一个数组元素“相同”的所有元素。在 PHP 的连续版本中，这些缺口正被识别出来，并实现新的函数来填补它们。

一个主要因素要追溯到章节开头提到的功能重叠。拥有两个行为非常相似的函数会导致突出它们之间差异的方式不同。有一个函数用于排序数组，还有一个函数使用回调来排序数组。有一个函数按键排序，还有一个函数使用回调按键排序。自然会问的问题是，这些差异对于其他数组函数是否有意义。

如果你想象所有可能的函数都是某个广阔空间中的单点，现有的函数提供了一组参考点，可以用来绘制空间图表。拥有 sort() 和 usort() 暗示了向提供回调移动的想法；从这些出发，ksort() 和 uksort() 暗示你可以独立地向“按键而非按值”的方向移动。既然这些方向已经被指出，拥有 array_diff() 不可避免地会暗示带有回调的 array_udiff()、“按键的 array_diff()”，以及当然带有回调的按键 array_udiff()。PHP5 实现了许多这些新函数，例如 array_udiff()，还有许多其他在 CVS 版本中，即使尚未在稳定版本中。

“正交”意味着直角；换句话说，尽可能远离平行。由于 PHP 的早期函数中有很多彼此非常相似，在“函数空间”中指向“几乎平行的方向”，使用它们将暗示其他几乎平行的函数（例如，array_intersect_assoc() 和 array_intersect_uassoc()），导致 PHP 函数密集聚集的函数空间区域。数组函数形成了这样一个密集的集群。你肯定会发现，为了有效使用它们，你不需要熟悉 PHP 所有的数组函数，并且一致地应用几个尽可能互不相关的函数的简单组合，将为你带来所有需要的功能。这就是正交性。哪几个函数由你决定。

#### 一个接一个的数组函数

当使用一系列数组函数来操纵数组内容时，与在循环中直接在数组元素上执行操作相比，操纵执行顺序存在明显差异。这可能会对程序内存要求等考虑产生重大影响。

考虑这个简短的例子：

```php
$array = array_map('do_something_fancy', $array);
```





# 第 3 章

这等同于：

```php
foreach ($array as $value) {
    $value = do_something_fancy($value);
}
```

在前者的情况下，在 `array_map()` 求值之后，会有短暂的一段时间存在*两个*数组。当然，在赋值完成后，`$array` 的旧版本会被丢弃，内存也会被回收，但这要等到赋值完成且对原始数组的引用计数降至零时才会发生。如果数组很大，所需的额外空间可能会非常可观，会分配大块的内存，然后在稍短的时间后*其他*大块内存被*释放*。显然，如果输出数组进入的变量与输入数组不同，则不会发生释放，并且数组函数实现中的一次性经济型分配可能比在 `$new_array[] = do_something_fancy($value)` 中发生的逐步逐元素操作更高效。显然，尽可能情况下，应当先应用可能输出比输入更短数组的函数（如 `array_filter()`、`array_udiff()` 等），再应用那些不能的函数，因为这可以减少后续函数的工作量。

如果有一系列返回数组的 `array_*` 类型函数，每个都使用前一个的结果，这种大批量的来回操作对 PHP 的内存管理和操作系统来说都会变得相当繁琐。通过编写类似以下的代码，可以在一定程度上（但仅仅是*某种程度*上）避免这种情况：

```php
array_walk(
    array_map(
        'do_something_fancy',
        array_filter(
            array_map('nothimg_fancy', $array),
            'purge'
        ),
        'traverse', 'sideways'
    );
```

而不是这样：

```php
$array = array_map('nothimg_fancy', $array');
$array = array_filter($array, 'purge');
$array = array_map('do_something_fancy', $array);
array_walk($array, 'traverse', 'sideways');
```

但如果你说前者更容易阅读，没有人会相信你。除此之外，函数的出现顺序与其应用的顺序是相反的。诚然，传递给函数的参数顺序缺乏一致性这一点无助于改善外观。关于它最好的说法是，它有助于在运行时抑制错误——如果你不小心将 `array_map` 错打成 `array_filter`，PHP 会在运行时抱怨 `第一个参数，'$array'` 应该是 NULL 或有效的回调。

#### glob()

你可能会经常发现自己需要做的任务之一是按特定模式读取目录中的文件——例如所有文本文件或图像文件。这可能比将文件存储在文件系统中，在别处维护这些文件的列表，然后不得不保持这两者同步要简单得多。

而且，同一目录中可能存在其他类型的文件。这是一个非常常见的任务，以至于任何 shell 接口都提供“通配符匹配”（globbing）——你可以列出 *.png，删除 temp* 等。在 PHP 4.3 之前，实现相同效果的典型方法会用到 `readdir()`，并且，基于手册中该函数用法的示例，最终得到的代码看起来像这样：

```php
$filelist = array();
if ($handle = opendir('directory')) {
    while (false != ($file = readdir($handle))) {
        if (substr($file, -4) == '.txt') {
            $filelist[] = $file;
        }
    }
    closedir($handle);
}
```

PHP 5 引入了 `scandir()`，它封装了整个 `opendir()/readdir()/循环()/closedir()` 过程，将过滤文件名的工作留到最后，在这个例子中，可以使用 `preg_grep()` 像这样处理：

```php
$filelist = preg_grep('/^.*\.txt$/', scandir('directory'));
```

但由于 PHP 4.3，甚至这样也是不必要的复杂。通过使用与 shell 类似的通配符语法，其中“?”代表*任何单个字符*，“*”代表“任意字符串”，你可以使用在 shell 中使用的相同语法来执行相同的文件名过滤。`$filelist = glob('*.txt', 'directory');`

`glob()` 函数有几个可选标志，可以通过按位或（bitwise-OR）组合在一起以调整函数的行为。例如，如果相关目录混合了 JPEG 和 PNG 文件（以及其他类型的零星混合，当然还有不可避免的 . 和 .. 目录），可以设置 `GLOB_BRACE` 标志，并将用于通过扩展名识别这些文件的替代通配符模式作为花括号内的逗号分隔列表传递给 `glob()`：

```php
$filelist = glob('{*.jpg,*.jpeg,*.png}', 'directory', GLOB_BRACE);
```

### PHP 流

从 PHP 4.3 开始，PHP 的 URL 封装器（允许你在通常预期文件名的地方使用 URL 的东西）已被扩展为通用的文件交互基本机制。这带来的一个结果是，你现在几乎可以在任何适合使用本地文件路径的上下文中使用 URL。（一些专门方面，如配置设置，不受此限制；例如，你不能在包含路径中使用 URL。）这包括第三方扩展使用的文件访问函数，PHP 现在将本地文件访问视为通过 `file:///` URL 的请求。

其行为像一个文件——你可能可以从中读取字节，向其写入字节，跳转到其中的特定字节位置，询问有多少字节，等等。注意“可能”（may be）的使用——正如有些文件是只读的，有些是只写的，流也可能是只读或只写的，而有些流是即时生成数据的，因此没有明确定义的“文件偏移量”、“文件大小”甚至“文件结尾”的对应物。其理念是，流的使用者无需了解他们处理的数据是如何存储或处理的；他们只是读取和写入。与例如 Java 相比，最显著的局限性是 PHP 流都是**字节**流。要流式传输其他内容——特别是对象——你需要序列化将其转换为可以通过流传输的东西。这是 PHP 松散类型再次产生影响的体现：由于每个流都是字节流，任何流都可以用于任何地方（无论其是否合理）。

#### 创建和使用流

构建流封装器只需将某些方法添加到流对象中，并使用 `stream_wrapper_register()` 将其标识为封装器。

`stream_wrapper_register()` 带有两个参数调用。第一个是 `protocol`（协议），它只是一个名称，指示在打开流时要使用的封装器——即在 URL 中被称为 `scheme`（方案）的部分。它是 URL 中 `://` 之前的部分，即 HTTP URL 中的 `http`，FTP URL 中的 `ftp`，以及文件 URL 中的 `file`。例如，如果你实现了一个流并将其注册为协议 `funky`，那么你就可以使用 `fopen("funky://...", "r+")` 来启用从 funky 流中读取。`fopen()` 和其他文件系统函数默认使用的协议是 `file`，这就是你很少看到 `file://` `/path.ext` 的原因，因为 `path/file.ext` 具有相同的效果。

第二个参数是一个包含实现你的封装器的类名的字符串。

自然地，封装器方法的完整列表在手册中有说明。主要的方法如下：

-   `stream_open()`：此函数包含新流的启动代码——初始化变量、打开其自身的流等。你用四个参数调用此函数。前两个是与相应的 `fopen()` 调用相同的路径和模式值。（对于第三方扩展，合适的选项将被计算并提供。）第三个参数可能包含最多两个标志：`STREAM_USE_PATH` 表示如果需要查找指定文件，你应该搜索 PHP 的 `include_path`，而 `STREAM_REPORT_ERRORS` 指示是否由流负责在流无法打开或其他错误发生时触发任何错误，或者是否这些将在更上层处理（在这种情况下，你的流不应报告任何错误）。`STREAM_USE_PATH` 仅在你实际上*正在*本地文件系统中寻找某物时相关，无论是请求的文件，还是你的流使用的辅助文件。如果你的流是只读的，如果请求的模式是写入（`w`、`r+`、`a`、`a+`），它应该返回 `FALSE`（并可能触发警告），类似地，对于只写流也是如此。
-   PHP 手册提到了“fopen_with_path()”，但截至 5.0.3 版本，该函数不存在。`include_path` 配置设置当然可以通过 `ini_get()` 访问。
-   `stream_read()`：如果流无法读取，这应该返回 `FALSE`。否则，它应该最多返回请求的字节数。作为封装器的作者，你有责任确保任何相关状态（包括任何文件指针）在对该方法的连续调用之间得以维持。你被允许返回少于请求的字节数（尽管空字符串可能被解释为指示流的结束）。





-   **stream_write()**: 同样，此函数仅应在流确实可写入时调用。流对象有责任跟踪从一次写入到下一次写入之间执行的操作。你无需写入所有接收到的字节；如有必要，可以截断数据。无论如何，此方法应返回已写入的字节数（如果完全无法写入，则返回 0）。这个数字应以接收到的字节数来表示。执行 base64 编码的流将为每接收三个字节返回四个字节。如果被要求写入 "abc"，它会写入 “YWJj”，但仍返回 3。此返回值是为了方便调用者使用，因为按定义，调用者本不该深入了解“被调用者”的操作细节。如果你写入的字节数少于请求的数量，由调用者决定是否重试，但你的流无论如何可能都需要保留一些数据。base64 编码器就是这种情况的一个例子：被传入 "ab" 后，它能够写入 “YWI”，但 “b” 的最后两个位必须保留，直到流等待下一个输入字节或调用 stream_close()。此编码器应返回 1，并期望在下一次 stream_write() 调用中再次传入 “b”。另一种机制是编码器除非至少有三个字节可编码，否则不输出任何内容，并且它一次只编码（并输出）三个输入字节的倍数。为了使其正常工作，流需要声称已写入所有传入的字节，即使实际上并未做到，并希望没有人发现其这种策略。否则，调用者可能会因为传入 "ab" 时返回 0 而生气并反复尝试，而编码器却在等待第三个字节，但该字节永远不会到达。

-   **stream_eof()**: 可读流随时可能被询问流数据是否已到达末尾（特别是在 stream_read() 因某种原因返回空字符串之后）。因此，这只是一个布尔函数，如果流已到达末尾则返回 "true"。

-   **stream_close()**: 流对象有责任清理需要清理的内容，关闭其自身的任何流，等等。回到 base64 编码器，流很有可能剩余一到两个字节，这些字节将永远无法成为三元组的一部分。因此，安全做法是最终编码这些字节并写出，用相应数量的 = 符号进行填充。

这些是打开和关闭流以及读写流的基础知识。流包装器还有其他方法，如果适合协议，则应实现它们，以涵盖随机访问、目录控制等任务。

当流打开时，stream_open() 会被调用，其第一个参数是包含协议的完整路径。这主要是为了让你可以使用 parse_url() 将路径分解为各个组件，因此最好将你的流名称格式设计为在适当的地方使用传统的 URL 语法（scheme://username:password@host:port/path?query#fragment）。顺便说一句，这也意味着同一个流类可以处理多种协议，但这最好通过子类化处理。

#### 流的两个示例

为了巩固上一节中的概念，这里有两个简单的流类。第一个维护一个日志文件，记录通过它访问的文件的活动，而第二个用于选择地理航空摄影集合的一部分。

# 第 3 章

#### 文件访问日志记录器

考虑以下代码：

```php
<?php
class logged_stream
{
    private $stream;
    private $log_stream;
    private $bytes_read=0, $bytes_written=0;
    private $user;

    function stream_open($path, $mode, $options, &$opened_path)
    {
        static $modes = array(
            'r' => 'reading',
            'r+' => 'reading and writing',
            'w' => 'writing',
            'w+' => 'writing and reading',
            'a' => 'appending',
            'a+' => 'appending and reading',
            'x' => 'creation and writing',
            'x+' => 'creation, writing and reading');
        $path = substr($path, 9);
        $this->user = substr($path, 0, strpos($path, '@'));
        $path = substr($path, strpos($path, '@')+1);
        $this->stream = fopen($path, $mode, $options&STREAM_USE_PATH);
        $this->log_stream = fopen($path . '.log', 'a');
        if(!($this->log_stream))
        {
            if($options&STREAM_REPORT_ERRORS)
            {
                trigger_error('Logged stream: Unable to open log file',
                              E_USER_WARNING);
            }
            return false;
        }
        if(!($this->stream))
        {
            if($options&STREAM_REPORT_ERRORS)
            {
                trigger_error('Logged stream: file `$path` could not be opened',
                              E_USER_WARNING);
            }
            return false;
        }
        $binary = strpos($mode, 'b')!==false;
        if($binary)
            $mode = str_replace('b', '', $mode);
        list($micro, $sec) = explode('.', microtime());
        $date = date('Y-m-d H:i:s', substr($micro, 1));
        fwrite($this->log_stream, 'File opened for ' . $modes[$mode] . '
            ' . ($binary?" in binary mode by ':" by ") . $this->user . ' at ' . $date . "\n");
        return true;
    }

    function stream_close()
    {
        fclose($this->stream);
        list($micro, $sec) = explode(' ', microtime());
        $date = date('Y-m-d H:i:s') . substr($micro, 1);
        fwrite($this->log_stream, 'File closed by ' . $this->user . ' at ' . $date . "\n");
        fwrite($this->log_stream, "Total bytes read: " . $this->bytes_read . "\n");
        fwrite($this->log_stream, "Total bytes written: " . $this->bytes_written . "\n");
        fwrite($this->log_stream, "\n");
        fclose($this->log_stream);
    }

    function stream_read($count)
    {
        ob_start();
        debug_print_backtrace();
        $backtrace = ob_get_clean();
        fwrite($this->log_stream, $backtrace);
        $read = fread($this->stream, $count);
        $this->bytes_read += strlen($read);
        return $read;
    }

    function stream_write($data)
    {
        $read = fwrite($this->stream, $data);
        $this->bytes_written += strlen($read);
        return $read;
    }

    function stream_eof()
    {
        return feof($this->stream);
    }

    function stream_tell()
    {
        return ftell($this->stream);
    }

    function stream_seek($offset, $whence=null)
    {
        return fseek($this->stream, $offset, $whence);
    }

    function stream_flush()
    {
        return true;
    }

    function stream_stat()
    {
        return fstat($this->stream);
    }

    function unlink($path)
    {
        $log_stream = fopen($path.'.log', 'a');
        if(!$log_stream)
        {
            trigger_error('Logged stream: Unable to open log file. File not deleted.', E_USER_WARNING);
            return false;
        }
        $success = unlink($path);
        list($micro, $sec) = explode(' ', microtime());
        $date = date('Y-m-d H:i:s') . substr($micro, 1);
        if($success)
            fwrite($log_stream, "File $path deleted at $date\n");
        else
            fwrite($log_stream, "Unable to delete file $path at $date\n");
        fclose($this->log_stream);
        return $success;
    }

    function rename($from_path, $to_path)
    {
        $from_log_stream = fopen($from_path.'.log', 'a');
        $to_log_stream = fopen($to_path.'.log', 'a');
        if(!$from_log_stream || !$to_log_stream)
        {
            trigger_error('Logged stream: Unable to open log file. File not renamed.',
                          E_USER_WARNING);
            return false;
        }
        $success = rename($from_path, $to_path);
        list($micro, $sec) = explode(' ', microtime());
        $date = date('Y-m-d H:i:s') . substr($micro, 1);
        if($success)
        {
            fwrite($from_log_stream, "File $from_path renamed to $to_path at $date\n");
            fwrite($to_log_stream, "File $to_path renamed from $from_path at $date\n");
        }
        else
        {
            fwrite($from_log_stream, "Unable to rename $from_path as $to_path at $date\n");
            fwrite($to_log_stream, "Unable to rename $from_path as $to_path at $date\n");
        }
        fclose($from_log_stream);
        fclose($to_log_stream);
        return $success;
    }
}
?>
```

该包装器通过调用 stream_wrapper_register('logged', 'logged_stream') 进行注册。你可以通过调用类似 $fp=fopen('logged://eric@documents/benchmarks.txt'); 的内容来使用 "logged" 流。这旨在表示用户 "eric" 将操作 documents/benchmarks.txt，并且要求记录该事件：

```php
$path = substr($path, 9);
$this->user = substr($path, 0, strpos($path, '@'));
$path = substr($path, strpos($path, '@')+1);
```




### 更晦涩的 PHP

流的活动始于 `stream_open()`。前三个 `substr()` 调用分离出 URL 中 `logged://` 部分以及用户名。剩余部分即为实际请求的资源 URL：

```php
$this->stream = fopen($path, $mode, $options & =~STREAM_REPORT_ERRORS);
$this->log_stream = fopen($path . '...log', 'a');
```

日志流打开资源本身（关闭了 `STREAM_REPORT_ERRORS` 标志，因为那些错误将由该流处理），同时也打开一个用于追加写作的日志文件。在这个例子中，为了简化，资源仅仅是另一个名称与请求的相同但带有额外 `.log` 扩展名的流。在实际应用中，日志记录会以其他方式进行，因为（一方面）这种机制对只读流会失败，但这类问题可以通过编写一个新的流类并以其自己的协议名注册来解决。第二个 `fopen()` 调用将使用该协议，之后的事情则是新类的问题。

之后，两个流会被检查以确保它们确实已打开。如果任一失败，则触发错误并返回 `FALSE`。

流在返回 `true` 之前最后执行的操作是向新打开的日志文件写入一行内容，说明流何时、以何种方式、由谁打开。

该类的大部分功能只是将相应的文件操作直接传递给其正在记录日志的流。`stream_read()` 和 `stream_write()` 增加了额外任务，即统计来回传递的字节数，而 `rename()` 则会记录文件的新名称（如果它作为已记录流打开，它将拥有自己的日志文件）。

最后，`stream_close()` 在关闭其两个流之前，写入时间和每个方向传输的总字节数。

### 地理信息系统（GIS）照片数据库查询

新西兰土地信息署（LINZ，http://www.linz.govt.nz/）维护着该国 2.5 米分辨率的照片图集。这些航拍照片经过比例尺调整和平移，使其垂直轴和水平轴分别精确对应南北方向和东西方向，从而形成所谓的“正射影像”。照片以 8000 × 6000 像素的图像形式提供，对应 3.2 × 2.4 平方公里的地面范围。四张这样的照片足以涵盖奥克兰市。合并为单个灰度 PNG 后，整个城市的图像大小为 115MB。

现在想象一个在线服务，用户输入奥克兰市内某点的经纬度和半径，服务返回相应的图像。最直接的方法可能是加载整个城市的图像并复制相关部分。但由于图像尺寸过大，这是不可行的（请记住，115MB 是 PNG 压缩后的尺寸；未压缩时，约 1.92 亿个像素各占一个字节）。

另一种方法是以未压缩形式存储影像（LINZ 提供未压缩的 TIFF 文件），并编写一个程序，仅从一个或多个文件中定位和读取相关字节（对于一个城市是 1.92 亿字节，但对于整个国家则多得多，需要存储大量原始数据以便随时访问），而无需将全部内容加载到内存中。这无疑是两种方案中更好的一个，但它并不适合 PHP，主要因为在读取字节并组装最终图像时，速度是一个重要考量。用 C 语言编写的自定义扩展更为合适。由于当前讨论关注的是 PHP 的流封装器接口，这种方案并不是特别有启发性的。

第三种方案由第二种方案引申而来。未压缩的影像可以存储在多个随机访问文件中。但如果文件足够小，就可以考虑以压缩形式存储并在需要时整体加载。那么，问题就简化为确定哪些文件满足特定请求，并将它们拼接成所需的图像。这就是以下流封装器实现的方案：

```php
<?php
/**
 * 正射影像流使用新西兰土地信息署维护的正射影像数据集。
 * 照片集遵循地形图 260 系列；使用的坐标是新西兰地图网格
 * （NZMG），这是一个该国特有的系统。
 *
 * 航拍照片的分辨率为每像素 2.5 米，精度为 ±12.5 米。
 */

class orthophoto_stream
{
    // 这是将回流给流的处理结果生成的 PNG 数据。
    private $png_data;

    // 用于 ftell() 函数 / stream_tell() 方法。
    private $data_length;

    function stream_open($path, $mode, $options, &opened_path)
    {
        // 这是一个只读流
        if (preg_match('/^[wa]/', $options)) return false;
        $path = parse_url($path);
        $coordinates = $path['host']; // 这里找坐标有点奇怪，但请参见
                                      // 本章节末尾的说明。
        if (strlen($coordinates) != 21) return false;
        if (strspn($coordinates, '0123456789') != 21) return false;
        list($northing, $easting, $radius) = sscanf($coordinates, '%07d%07d%07d');

        $full_image_size = ceil($radius * 2 * 100 / 250);

        $full_image = imagecreate($full_image_size, $full_image_size);
        $black = imagecolorallocate($full_image, 0, 0, 0);
        // 我们使用黑色作为未映射区域的背景。
        imagefill($full_image, 0, 0, $black);

        $maximum_northing = $northing + $radius;
        $minimum_northing = $northing - $radius;
        $maximum_easting = $easting + $radius;
        $minimum_easting = $easting - $radius;
        $topmost_tile_northing = floor($minimum_northing / 250) * 250;
        $bottommost_tile_northing = ceil($maximum_northing / 250) * 250;
        $leftmost_tile_easting = floor($minimum_easting / 250) * 250;
        $rightmost_tile_easting = ceil($maximum_easting / 250) * 250;

        for ($tile_northing = $bottommost_tile_northing;
            $tile_northing <= $topmost_tile_northing;
            $tile_northing += 250) {
            for ($tile_easting = $leftmost_tile_easting;
                $tile_easting <= $rightmost_tile_easting;
                $tile_easting += 250) {
                $full_image_x = 100 * ($tile_easting - $minimum_easting) / 250;
                $full_image_y = 100 * ($maximum_northing - $tile_northing) / 250;
                $tile_name = sprintf('%07d%07d.png', $tile_northing, $tile_easting);
                if (!file_exists('tiles/' . $tile_name)) continue;
                $tile = imagecreatefrompng('tiles/' . $tile_name);
                imagecopy($full_image, $tile, $full_image_x, $full_image_y, 0, 0, 100, 100);
                imagedestroy($tile);
            }
        }

        ob_start();
        imagepng($full_image);
        imagedestroy($full_image);
        $this->png_data = ob_get_contents();
        ob_end_clean();
        $this->data_length = strlen($this->png_data);
        return true;
    }

    function stream_close()
    {
        $this->png_data = null;
    }

    function stream_read($bytes)
    {
        if (strlen($this->png_data) == 0) return false;
        $return = substr($this->png_data, 0, $bytes);
        $this->png_data = substr($this->png_data, $bytes);
        return $return;
    }

    function stream_write() {}

    function stream_eof()
    {
        return $this->png_data == 0;
    }

    function stream_tell()
    {
        return $this->data_length - strlen($this->png_data);
    }

    function stream_seek()
    {
        return false;
    }

    function stream_flush()
    {
        return false; // 我们不存储数据，真傻。
    }

    function stream_stat()
    {
        return false;
    }

    // 我们将流封装器注册放在这里，连同它注册的封装器，
    // 以免每次包含文件时都忘记注册。
    // 这当然假设我们永远不会受诱惑将相同的封装器协议
    // （nzm）用于不同类型的流。
}

stream_wrapper_register('nzm', 'orthophoto_stream');
```

如代码最后一行所述，该类以“nzm”协议注册。这里实现的 `nzm` URL 的完整格式为 `nzm://nnnnnnnnnnnneeeerrrrr`，其中七个数字分别指定北纬（对于奥克兰，是 6460000 到 6489750 之间的米数）、东经（2650000 到 2689750 之间的米数）和半径（也以米为单位，但要求超过 20000 没有意义，因为那是整个 16 x 12 公里图像的对角线长度）。

位置之所以用“北纬”和“东经”而不是经纬度来表示，是因为地球既不是一个完美的球体，甚至也不是一个特别对称的椭球体，因此从一个系统转换到另一个系统绝非简单。本例中使用的新西兰地图网格是通过经验确定的，得到的经纬度/北纬/东经映射涉及计算六阶复变量多项式之类的问题。（测量局办公室的精确规范作为 OSG 技术报告 4.1 提供，可从 LINZ 网站获取。）这与本例的目标无关，就像将地标和送货地址映射到坐标的练习一样无关。同样，输入数据验证的问题，包括将半径限制在比 20 公里更合理的范围内，也无关。所有这些具体任务都应在到达这个阶段之前处理，且尽可能具有广泛适用性。

影像以一系列 PNG 文件形式存储，每个文件 100 x 100 像素，对应现实世界中的 250 x 250 米，因此总共有 19,200 个这样的文件。每个文件以其西南角（左下角）的北纬和东经命名。北径向北方增加，东径向东方增加。由于北纬和东经本身以米为单位（这就是它们的用途），`6470002660000.png` 北侧的图块将是 `64702502660000.png`，东侧的图块则是 `6470002660250.png`。图块的位置已设定，使得它们所知的北纬和东经都是 250 的倍数。由于父图像也具有此属性，其尺寸也是 100 像素的倍数，因此这些图块恰好覆盖父图像。

同样，大部分工作在 `stream_open()` 中完成，确定请求图像的大小、其左下角像素所在的图块，以及垂直和水平方向上需要多少个图块。使用 GD Lib 创建新图像（由于影像是灰度的，因此没有使用 `imagecreate(truecolor)` 变体 `imagecreatetruecolor()` 的必要）具有预期的尺寸，然后通过嵌套循环从磁盘读取适当的图块并将其复制到正在处理的图像中。在任意时刻为存储图像数据所消耗的总内存足以容纳正在处理的图像和一个 100 x 100 像素的图块。




`stream_open()` 的最后一个动作是将组装好的 GD Lib 图像转换为 PNG 数据。这通过一种简单的方式实现：要求 GD Lib 将图像输出为 PNG，并使用输出缓冲区来捕获结果。

每次调用 `stream_read()` 都会返回另一部分 PNG 数据，并丢弃已经返回过的部分。

由于这是一个由即时生成数据组成的只读流，因此剩余的大部分流访问方法都没有意义。关于数据可以说的一点是还剩多少可供读取，这使得 `stream_tell()` 可以被定义。

使用此类代码的人无需了解它将 `nzmg://` 请求与响应匹配的具体操作。就其关心的内容而言，`nzmg://6482089266771200500` 只是另一个文件，恰好包含一张中央奥克兰 1 公里宽快照的 PNG 图像。

但请等一下。如果它只是 PNG 数据，而且只是一个文件，那么从所有实际目的来看，它就是一个 PNG 文件。确实如此。下面是一个使用该封装类的示例。假设类位于自己的 `orthophoto_stream.php` 文件中，且假设纬度和经度已经转换为北向和东向坐标，并且半径不会太大或太小。

```php
include_once('orthophoto_stream.php'); // 类必须先声明
                                    // 然后才能使用，当然。
function display_orthophoto($northring, $easting, $radius)
{
	$filename = sprintf('nzmg://64807%d0%d8%d', $northring, $easting, $radius);
	
	// 所有基于流的操作都在这里发生。
	$image = imagecreatefrompng($filename);
	
	// 进行一点后处理，使这段代码超越平凡。
	// 绘制一个指定半径的圆（图像毕竟是方形的），并在中心放置一个十字。
	// 我们需要找到图像的白色值
	$white = imagecolorexact($image, 255, 255, 255);
	if ($white == -1) // 好吧，它还不存在。
	$white = imagecolorallocate($image, 255, 255, 255);
	// 圆以图像为中心，大小刚好能触及边缘。
	$imageSize = imagesx($image);
	$middle = $imageSize >> 1;
	imageellipse($image, $middle, $middle, $imageSize, $imageSize, $white);
	imageline($image, $middle, $middle - 5, $middle, $middle + 5, $white);
	imageline($image, $middle - 5, $middle, $middle + 5, $white);
	imagestring($image, 0, 0, 0,
		'Sourced from Orthophoto R11 Auckland Crown Copyright Reserved.',
		$white);
	imagepng($image);
	imagedestroy($image);
}
```

不用说，这个示例是在实际使用和教育用途之间做出的妥协，`orthophoto_stream` 类还有许多可以改进的方向。

# 第 3 章

其中一个方向是，提供的 21 位数字文件名可以附加一个扩展名，以指示所需的图像格式，而不是固定生成 PNG。其他方向包括更现实（或至少更灵活）的存储机制，用户可以通过包含主机名和路径的更完善的 URL 来控制。还要考虑将部分读取工作移入 `stream_read()`，从而减少在任何给定时间需要保留的图像数据量。（然而请注意，由于 GD Lib 缓冲区只处理完整图像，你需要编写自己的代码来输出图像数据，该数据是正确的，但在等待未来输入之前仍不完整。）

如果你遵循 RFC 3986 中定义的流资源命名 URL 系统，并参考 RFC 2718 中的指南，你会受益匪浅。事实上，可能已经有一个正在使用的命名方案与你的应用程序相匹配。（官方注册表由互联网号码分配机构在 http://www.iana.org/assignments/uri-schemes/ 维护。）如果有，请使用它。这样，你的应用程序将来就能与其他使用相同方案的应用程序协作，而无需额外的 URL 转换层来粘合它们。（实际上，对于任何数据格式或通信协议也是如此——如果世界其他地方已经对你想要的东西达成了公认标准，就使用它，省去自己创建新标准的时间和精力。）

> 请注意，所有 PHP URL 都要求在使用方案名称后使用 `://`，无论是否涉及命名权限（主机），因为 PHP 使用该字符序列来区分 URL 和局部文件路径。在 RFC 3986 的术语中，PHP 仅实现了“hier-part”组件给出的四个生成式中的第一个，并将“naming-authority”组件设为可选。符合 RFC 的变通方法是将使用 `://`，隐式地将本地主机指定为命名权限。

###### 总结

这是对 PHP 原生函数集中一些利用较少领域的简要介绍。通过使用这些功能，你的代码可以更紧凑、更可靠，同时不牺牲可读性。数组函数通常可以替代有时复杂的循环，将任务简化为单行代码和一个可以捕获并存储在库中以便重用的辅助函数。函数处理函数允许你在运行时不仅决定要使用哪个函数（switch 语句可以做到这一点），还可以决定要从哪些函数中选择，甚至从头创建函数。流允许你隐藏外部数据读写实现细节，使程序的其他部分能够将其视为另一个文件。

PHP 总是有新功能被添加——新的初始化设置以微调其操作，新参数增强现有函数的实用性（甚至久经考验的函数 `str_replace()` 在 PHP5 中也被赋予了新参数），新函数，甚至整个新的函数类别。这使得学习 PHP 成为一个持续的过程，总有一些你还不了解的东西。

![](img/ab27c6ac898db1f934d39fa127b14657_98_0.png)

# 第 4 章：高级 MySQL

大多数动态网站的关键要素之一是为其提供数据的数据库。从简单的新闻页面到复杂的出版系统或 CMS，数据库在管理网站内容方面发挥着核心作用。为了使网站顺利运行，了解数据库系统的一些技巧和诀窍是很有帮助的。在本章中，你将学习如何创建数据库，管理访问系统的各种用户账户，以及组合和优化你的 SQL 代码以执行复杂和精细的查询。

### 回顾基础

在着手更高级的功能之前，让我们快速回顾一下 MySQL 的使用。假设你刚接手一个新客户，一家汽车经销商。经销商的经理希望你创建一个网站，帮助他们跟踪汽车库存。没问题，你说，然后坐下来开始规划他们的 Web 应用程序。

在规划过程中，你想出了一个简单的多表数据库方案来存储他们汽车场地的数据。为了这些练习的目的，你决定创建类似于图 4.1 的数据库表。

你创建的是一个非常简单的数据库结构，涉及四个表。在 `New_Vehicles` 表中，显然你要存储新汽车的数据。可以为每辆库存汽车指定里程、价格、颜色和描述等属性。`Used_Vehicles` 表的结构与 `New_Vehicles` 几乎相同，但旨在存储你可能猜到的是二手车的记录。`Used_Vehicles` 表额外提供了几列，用于指示车辆是否经过认证或带有保修，以及一列用于里程。最后两个表 `Make` 和 `Model` 存储该经销商销售的各种品牌的通用制造商和型号名称。

**制造商（Makes）**

| 列 | 类型 |
| :--- | :--- |
| make_id | int |
| make_name | varchar(100) |

**型号（Models）**

| 列 | 类型 |
| :--- | :--- |
| model_id | int |
| model_name | varchar(200) |
| make_id | int |

**New_Vehicles**

| 列 | 类型 |
| :--- | :--- |
| vehicle_id | int |
| model_id | int |
| modelyear | int |
| price | decimal(10,2) |
| color | varchar(200) |
| description | text |

**Used_Vehicles**

| 列 | 类型 |
| :--- | :--- |
| vehicle_id | int |
| model_id | int |
| modelyear | int |
| mileage | int |
| price | decimal(10,2) |
| color | varchar(200) |
| certified | tinyint |
| warranty | tinyint |
| description | text |

*图 4.1*

### 创建数据库

你需要做的第一件事是在 MySQL 中创建数据库和表。首先，在命令行启动你的 MySQL 客户端，或者如果你有其他更习惯使用的程序，并且可以直接输入 MySQL 命令，请随意使用它。

```bash
shell$ mysql
```

这将打开 MySQL 监视器，其外观应类似于以下内容（如果你正在使用命令行客户端）：

```text
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 2 to server version: 4.1.11-1og
Type 'help;' or '\h' for help. Type '\c' to clear the buffer.
mysql>
```

在许多情况下，你需要使用登录名和密码来访问 MySQL 客户端。为此，只需在 `mysql` 命令末尾添加 `-u username -p`，MySQL 就会提示你输入密码，如下所示：

```bash
shell$ mysql -u username -p
```




#### 高级 MySQL

使用 MySQL 命令行客户端是熟悉 MySQL 大多数命令和功能性的绝佳方式，而这些功能在图形用户界面（GUI）客户端中通常会被自动化处理。

输入以下命令以创建数据库，并将其命名为“VehicleInventory”：

```sql
mysql> CREATE DATABASE VehicleInventory;
```

既然已经创建了数据库，你就需要将其他查询的剩余部分设置为活动数据库：

```sql
mysql> USE VehicleInventory;
```

接下来，为你的数据库创建表。在 MySQL 中创建表的基本 SQL 语句是：

```sql
CREATE TABLE tablename (column_definitions);
```

为了创建四个车辆信息表，你可以使用以下内容：

```sql
mysql> CREATE TABLE Makes (make_id int PRIMARY KEY AUTO_INCREMENT, make_name varchar(100));
mysql> CREATE TABLE Models (model_id int PRIMARY KEY AUTO_INCREMENT, model_name varchar(200), make_id int);
mysql> CREATE TABLE New_Vehicles (vehicle_id int PRIMARY KEY AUTO_INCREMENT, model_id int, modelyear int, price decimal(10,2), color varchar(200), description text);
mysql> CREATE TABLE Used_Vehicles (vehicle_id int PRIMARY KEY AUTO_INCREMENT, model_id int, modelyear int, mileage int, price decimal(10,2), color varchar(200), certified tinyint, warranty tinyint, description text);
```

简而言之，你只需使用 MySQL 的 CREATE TABLE 命令，后接表名，然后用括号列出列名和类型即可。你还会注意到，每个表都添加了一个自增主键，这有助于在你添加行后唯一地识别它们。

### 添加信息

既然表已经创建好了，你需要向其中添加一些数据。为此，你将使用 INSERT 语句。MySQL 的 INSERT 命令通常遵循以下格式：

```sql
INSERT INTO tablename (column_list) VALUES (new_values);
```

首先向 Makes 表添加一些初始数据：

```sql
INSERT INTO Makes (make_id, make_name) VALUES (1, 'Ford'), (2, 'Honda'), (3, 'Volkswagen'), (4, 'Toyota'), (5, 'Chevrolet');
```

这里，使用了基本的 SQL INSERT 语法，但增加了一点变化。在 MySQL 中，你可以指定一组以逗号分隔的列值，而不仅仅是单组值，从而一次性填充多行。通常情况下，在向 Makes 表插入数据时可能会省略 make_id 列——自增 ID 会自动为它们分配数字。在这种情况下，你指定了 ID，这样你稍后添加到其他表中的行将拥有有效的外键。

使用以下内容向其余表添加数据（记住，你可以从 www.wrox.com 下载此代码，如果你愿意的话可以省去一些打字工作）：

```sql
INSERT INTO Models (model_id, model_name, make_id) VALUES (1, 'Explorer', 1), (2, 'Accord', 2), (3, 'Golf', 3), (4, 'Tacoma', 4), (5, 'Corvette', 5);
INSERT INTO New_Vehicles (model_id, modelyear, color, description) VALUES
(1, 2005, 'Dark Blue', 'Popular SUV; great for moving people or cargo across town, or wherever your adventures may take you.'),
(NULL, 2004, 'Graphite Pearl', 'Last of the 2004 stock! Must sell! Loaded, all options!'),
(4, 2005, 'Radiant Red', 'Come drive this terrific truck! 4WD, extended cab, many options.'),
(5, 2005, 'Daytona Sunset Orange Metallic', 'The all new C6 Corvette, the next generation of classic American sports cars. 400HP V8; Very fast!'),
(1, 2005, 'Dark Blue', 'Popular SUV; great for moving people or cargo across town, or wherever your adventures may take you.');
INSERT INTO Used_Vehicles (model_id, modelyear, color, mileage, certified, warranty, description) VALUES
(1, 2000, 'White', 64800, 0, 0, 'Good condition; One owner; 4WD, V6'),
(2, 2003, 'Deep Green Pearl', 27300, 0, 1, 'Excellent condition, off-lease vehicle; Must see!'),
(3, 2004, 'Reflex Silver', 3800, 1, 1, 'R32 Limited edition; Low miles; Understated and surprisingly functional; Loaded.'),
(4, 1993, 'Red', 152000, 0, 0, 'Runs decent; 4WD; Tinted windows, aftermarket stereo; Needs a little TLC.');
```

请注意，添加到 New_Vehicles 表的第二辆车的 *model_id* 是一个 NULL 值。你稍后会明白原因。

### 检索信息

你花了大量时间创建数据库表并填充数据；现在是时候将其中一些数据取回来了。为此，你将使用 SELECT 语句。SELECT 的简化形式看起来像这样：

```sql
SELECT [column_names] FROM [table] WHERE [criteria]
```

例如，如果你想获取二手车颜色列表，可以使用类似以下内容：

```sql
SELECT color FROM Used_Vehicles;
```

这将返回以下内容：

| color |
| :--- |
| White |
| Deep Green Pearl |
| Reflex Silver |
| Red |

或者，也许你想要列出 2001 年款之前所有车辆的里程数：

```sql
SELECT mileage, modelyear FROM Used_Vehicles WHERE modelyear < 2001;
```

运行此查询显示以下内容：

| mileage | modelyear |
| :--- | :--- |
| 64800 | 2000 |
| 152000 | 1993 |

这很简单，但如果你发现了一个错误，并希望修改现有记录怎么办？

### 更新信息

要更新信息，你使用 UPDATE 语句。UPDATE 语句的通用形式看起来像这样：

```sql
UPDATE [table] SET [column]= (value) WHERE [criteria]
```

回到车辆库存示例，假设有一天车行的经理在查看库存时，发现其中一辆车的里程数记录有误。为了将其更改为正确的值，你可以使用以下查询：

```sql
UPDATE Used_Vehicles SET mileage=66000 WHERE vehicle_id=1;
```

在这种情况下，车辆 ID 1 对应于之前 INSERT 语句中添加的二手福特探险者（Ford Explorer）自动分配到的自增 ID。

### 删除信息

假设车行的销售开始增加，一些最近的交易要求从数据库中删除某些车辆。在这种情况下，你将使用 DELETE 语句：

```sql
DELETE FROM [table] WHERE [criteria];
```

上一例中里程数被修正的那辆二手福特探险者今天卖掉了。要从 Used_Vehicles 表中移除它，你只需执行以下操作：

```sql
DELETE FROM Used_Vehicles WHERE vehicle_id=1;
```

这应该涵盖了 MySQL 使用的基础知识，是时候转向更强大的查询了。

### 多表查询

你设置了车辆库存，并且可以使用基础知识对单个表执行简单查询。但你可能想看到更多内容——甚至是一个将每辆车的品牌和型号与其单独记录关联起来的查询。为此，你会使用连接（Joins）。

在 SQL 中，连接是一种根据指定列将一个或多个表链接在一起的方法。在 MySQL 中，最常用的是两种类型的连接：内连接（inner joins）和外连接（outer joins）。

### 内连接

*内连接*是一种将两个表组合在一起的方法，基于每行共有的通用值。当你在 SELECT 查询中执行内连接时，你只需在 FROM 子句中指定要连接的表，并提供提示说明它们有哪些共同列。MySQL INNER JOIN 语法的通用抽象如下所示：

```sql
SELECT [column_names] FROM [table1] INNER JOIN [table2] ON [table1.column] = [table2.column]
```

使用假设的车行库存，你希望结果中返回每辆车的型号，并与每辆车的特定信息一起显示。为了实现这一点，你的查询看起来可能如下所示：

```sql
SELECT Models.model_name, New_Vehicles.color, New_Vehicles.modelyear FROM Models INNER JOIN New_Vehicles ON Models.model_id = New_Vehicles.model_id;
```

在数据库中运行此查询会产生以下结果：

| model_name | color | modelyear |
| :--- | :--- | :--- |
| Explorer | Dark Blue | 2005 |
| Tacoma | Radiant Red | 2005 |
| Corvette | Daytona Sunset Orange Metallic | 2005 |

你会注意到在 SELECT 查询中，select 列表中的每一列都以前缀了其所属的表名。虽然这在技术上并非必须，但为了避免同名列之间的冲突，通常这是一个好主意。如果你有这样的冲突而忽略了表前缀，会发生什么？看看这个例子：

```sql
SELECT model_id, model_name, color, modelyear FROM Models INNER JOIN New_Vehicles ON Models.model_id = New_Vehicles.model_id;
```

如你所见，表前缀已被移除，并且 model_id 列也被添加到了列表中（因为它存在于两个表中）。现在尝试运行该查询。你会得到以下错误：

```
ERROR 1052 (23000): Column 'model_id' in field list is ambiguous
```

尝试使用存在于两个表中的列名而不使用表前缀，每当执行查询时都会抛出此类错误。

如果你碰巧喜欢 SQL 查询的简洁性，请放心——有一种简单的方法可以缩短所有这些表前缀。在 FROM 子句中，你可以为调用的每个表指定一个表 *别名*，如下所示：

```sql
SELECT [column_names] FROM [table1] alias1 INNER JOIN [table2] alias2 ON [alias1.column] = [alias2.column]
```




# 高级 MySQL 技巧

由于表别名可以短至一个字母，你可以极大地缩短你的库存查询：

```sql
SELECT m.model_name, n.color, n.modelyear FROM Models m INNER JOIN New_Vehicles n
ON m.model_id = n.model_id;
```

觉得还不够简洁？嗯，还有另一种整理连接（Join）的方法。MySQL 提供了 `USING` 语句，可以替代 `ON` 语句来关联表。当两个用于连接的列恰好具有完全相同的列名时，使用 `USING` 语句。带有 `USING` 的通用内连接形式如下所示：

```sql
SELECT [列名] FROM [表1] INNER JOIN [表2] USING (列列表)
```

因为 New_Vehicles 表和 Models 表都有一个 model_id 列，你可以在连接中使用 `USING` 语句：

```sql
SELECT m.model_name, n.color, n.modelyear FROM Models m INNER JOIN New_Vehicles n
USING (model_id);
```

在某些情况下，你需要在查询中连接两个以上的表。MySQL 可以轻松处理这种情况——你只需按想要的评估顺序将连接语句依次排列即可。在车辆库存数据库中，你需要使用多个连接来返回每个车辆记录及其制造商标识，如下所示：

```sql
SELECT ma.make_name, mo.model_name, n.color, n.modelyear FROM Makes ma INNER JOIN
Models mo USING (make_id) INNER JOIN New_Vehicles n USING (model_id);
```

运行此查询后，你应该看到以下结果：

| make_name | model_name | color | modelyear |
| --- | --- | --- | --- |
| Ford | Explorer | Dark Blue | 2005 |
| Toyota | Tacoma | Radiant Red | 2005 |
| Chevrolet | Corvette | Daytona Sunset Orange Metallic | 2005 |

正如你所见，Makes 表基于 make_id 与 Models 表进行了连接，然后该连接的结果又与 New_Vehicles 表进行连接，从而在一个查询中得出了制造商、车型和车辆信息。

在进入下一组连接之前，你应该知道还有另一种执行内连接的方式。第二种方式简单地通过逗号分隔的列表指定多个表，并使用 `WHERE` 语句来指定表之间如何关联。这种内连接的通用形式如下所示：

```sql
SELECT [列名] FROM 表1, 表2 WHERE 表1.列 = 表2.列
```

如果使用这种内连接形式来提取新车辆、制造商和车型列表之前的查询，它会看起来像这样：

```sql
SELECT ma.make_name, mo.model_name, n.color, n.modelyear
FROM Makes ma, Models mo, New_Vehicles n
WHERE ma.make_id = mo.make_id AND mo.model_id = n.model_id;
```

在你的 MySQL 客户端中执行此查询，将返回以下结果：

| make_name | model_name | color | modelyear |
| --- | --- | --- | --- |
| Ford | Explorer | Dark Blue | 2005 |
| Toyota | Tacoma | Radiant Red | 2005 |
| Chevrolet | Corvette | Daytona Sunset Orange Metallic | 2005 |

正如你所见，返回的结果与使用显式内连接时完全相同。如果你省略了 `WHERE` 子句中的项会发生什么？尝试运行此查询：

```sql
SELECT mo.model_name, n.color, n.modelyear
FROM Models mo, New_Vehicles n;
```

针对我们的车辆库存运行此查询会产生以下结果（注意 `Makes` 表已被排除）：

| model_name | color | modelyear |
| --- | --- | --- |
| Accord | Dark Blue | 2005 |
| Golf | Dark Blue | 2005 |
| Tacoma | Dark Blue | 2005 |
| Corvette | Dark Blue | 2005 |
| Explorer | Dark Blue | 2005 |
| Accord | Graphite Pearl | 2004 |
| Golf | Graphite Pearl | 2004 |
| Tacoma | Graphite Pearl | 2004 |
| Corvette | Graphite Pearl | 2004 |
| Explorer | Graphite Pearl | 2004 |
| Accord | Radiant Red | 2005 |
| Golf | Radiant Red | 2005 |
| Tacoma | Radiant Red | 2005 |
| Corvette | Radiant Red | 2005 |
| Explorer | Radiant Red | 2005 |
| Accord | Daytona Sunset Orange Metallic | 2005 |
| Golf | Daytona Sunset Orange Metallic | 2005 |
| Tacoma | Daytona Sunset Orange Metallic | 2005 |
| Corvette | Daytona Sunset Orange Metallic | 2005 |
| Explorer | Daytona Sunset Orange Metallic | 2005 |
| Accord | Dark Blue | 2005 |
| Golf | Dark Blue | 2005 |
| Tacoma | Dark Blue | 2005 |
| Corvette | Dark Blue | 2005 |
| Explorer | Dark Blue | 2005 |

这不太对劲。在这种情况下实际发生的是一种称为交叉连接（Cross Join）的不同类型的连接。交叉连接仅仅是每个表中所有匹配结果的组合。在这种情况下，Models 表中有五个车型，因此其中每一行都与 New_Vehicles 表中的每一行进行了匹配。发生这种情况仅仅是因为你省略了 `WHERE` 语句，而该语句为 MySQL 提供了如何关联记录的提示。如前所述，你在这个查询中没有包含 Makes 表——如果包含了，由于数据库中有五个不同的制造商，结果行将是原来的五倍长。

#### 外连接

虽然大多数复杂的链接都可以通过内连接实现，但有些情况下它们受到限制。如果数据库行未为被链接的列定义值，它将被内连接忽略。在车辆库存示例中，每次使用内连接链接 Models 表查询时，只返回了三行。New_Vehicles 表中的第四辆车被忽略了，因为其 model_id 值为 null。你需要一种方法，无论是否指定了 model_id 都返回所有行，如果指定了 model_id，则执行请求的连接。对于这样的任务，MySQL 提供了外连接（Outer Joins）。

MySQL 中有两种主要类型的外连接：左外连接和右外连接。它们的行为完全相同，唯一的区别在于允许哪个表不包含匹配项。外连接的通用形式与内连接非常相似。请看左外连接的简化版本：

```sql
SELECT [列名] FROM 表1 LEFT OUTER JOIN 表2 USING (列列表)
```

左外连接使用共同的列名将“右”表（table2）与“左”表（table1）进行匹配，但如果“左”表包含的值与“右”表中的任何值都不匹配，它仍会返回行。右外连接的行为相同，但两个表的角色互换（右表允许存在不匹配的值）。

在车辆库存示例中，如果你希望返回一组行，包含所有新车辆，无论其 model_id 如何，你可能会使用以下内容：

```sql
SELECT mo.model_name, n.color, n.modelyear FROM New_Vehicles n LEFT OUTER JOIN Models mo USING (model_id);
```

使用此查询查询车辆库存数据库会产生以下结果：

| model_name | color | modelyear |
|---|---|---|
| Explorer | Dark Blue | 2005 |
| NULL | Graphite Pearl | 2004 |
| Tacoma | Radiant Red | 2005 |
| Corvette | Daytona Sunset Orange Metallic | 2005 |
| Explorer | Dark Blue | 2005 |

这与你之前查看的一个早期内连接查询非常相似，但增加了第二行——来自 2004 年款的 Graphite Pearl。由于在 Models 表中没有匹配项，MySQL 对无法确定的行中的值返回 NULL——在这种情况下，是 model_name。




# 第 4 章

然而，外连接和内连接并不非得互相隔离。两者可以在单个查询中结合使用，从而生成强大的多表连接，且对要求所有行数据完全匹配这一条件较为宽松。若要提取新车辆的颜色、制造商、型号和年份列表（包括未指定型号的车辆），请执行类似以下查询：

```sql
SELECT ma.make_name, mo.model_name, n.color, n.modelyear FROM New_Vehicles n LEFT OUTER JOIN Models mo USING (model_id) LEFT OUTER JOIN Makes ma USING (make_id);
```

在车辆库存数据库上运行此查询将返回以下结果：

| make_name | model_name | color | modelyear |
| --- | --- | --- | --- |
| Ford | Explorer | Dark Blue | 2005 |
| NULL | NULL | Graphite Pearl | 2004 |
| Toyota | Tacoma | Radiant Red | 2005 |
| Chevrolet | Corvette | Daytona Sunset Orange Metallic | 2005 |
| Ford | Explorer | Dark Blue | 2005 |

请注意，在此查询中，表的连接顺序至关重要。第一个连接生成的结果表在连接第三个表时，将作为内部临时表使用。

#### 联合（Unions）

到目前为止，你在车辆库存数据库上执行的查询仅返回一种类型车辆的记录，即新车或二手车。如果你想要获取数据库中所有车辆的列表，而不管其之前的所有权状态如何该怎么办？起初，你可能认为只需将两个表都添加到查询中即可；但这会导致交叉连接（cross join），这并不完全是你想要的结果。在这种情况下，你需要使用联合（Unions）。

MySQL 中的联合是一种将多个表作为单一记录集返回的方法，而无需将它们合并。联合类似于 PHP 中的字符串拼接（concatenation）——它们只是将额外的行追加到第一个表的末尾。MySQL 中联合的通用形式如下所示：

```sql
(SELECT [column names] FROM [table1]) UNION (SELECT [column names] FROM [table2])
```

简单来说，联合是通过用 UNION 关键字将两个独立的 SELECT 语句连接在一起来实现的。在代码抽象中，每个 SELECT 语句周围都加了括号。虽然这不是必须的，但这是一个很好的习惯，有助于在视觉上区分两个查询。

假设你想返回车辆库存中所有车辆的列表，无论它们是新车还是二手车。请使用类似以下查询：

```sql
(SELECT color, modelyear, model_id FROM New_Vehicles) UNION (SELECT color, modelyear, model_id FROM Used_Vehicles);
```

如果你在 MySQL 中运行此查询，你应该会看到以下结果：

![](img/ab27c6ac898db1f934d39fa127b14657_108_0.png)

请注意，该查询精确指定了你想从每个表中返回的列，且列列表中的列数在表间必须匹配。如果你为每个表选择了不同数量的列会发生什么？看看这个查询，其中你将选择每个表中的所有记录（Used_Vehicle 表比 New_Vehicles 表拥有更多的列）：

```sql
(SELECT * FROM New_Vehicles) UNION (SELECT * FROM Used_Vehicles);
```

尝试在数据库上运行此查询，它将返回以下内容：

```
ERROR 1222 (21000): The used SELECT statements have a different number of columns
```

MySQL 会迅速返回错误，告知你列列表长度不同。列列表中的任何列组合都是有效的，只要每个列表中的列数相同即可。如果每个对应位置的列名称不同，MySQL 在返回行时将使用第一个列表中的列名。请查看以下查询：

```sql
(SELECT coler FROM New_Vehicles) UNION (SELECT modelyear FROM Used_Vehicles);
```

当查询数据库时，它将显示以下内容：

![](img/ab27c6ac898db1f934d39fa127b14657_108_1.png)

不出所料，MySQL 使用了第一个列列表中的列名 `coler`。然而，这个例子说明了将来可能引起混淆的一个点。`coler` 在表中的列类型被设置为 varchar，而 `modelyear` 的列类型是 int。在对这两个表执行联合时，MySQL 忽略列类型并愉快地组合了表。在大多数情况下这可能不是问题，但如果你正在 MySQL 外部强制执行引用完整性（例如在 PHP 中），如果外部代码期望特定类型的返回数据，而 MySQL 发送了像这样混合的结果，可能会出现冲突。

所有车辆的颜色和年份的简单列表固然不错，但汽车经销商的老板期待你做得更多。除了返回颜色和年份外，你还需要提供制造商和型号。你准备愉快地为你的新联合表添加必要的连接，使用可能像这样的查询：

```sql
(SELECT color, modelyear, model_id FROM New_Vehicles) UNION (SELECT color, modelyear, model_id FROM Used_Vehicles) LEFT OUTER JOIN Models USING (model_id) LEFT OUTER JOIN Makes USING (make_id);
```

看起来不错，你心想，直到你在 MySQL 上运行它并得到这个：

```
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'LEFT OUTER JOIN Models USING (model_id)' LEFT OUTER JOIN Makes USING (make_id)' at line 1
```

发生了什么？UNION 操作本身并不等同于来自表的普通结果集，因此你不能简单地附加必要的连接来查找额外信息。此外，你没有指定任何地方返回 `make_name` 或 `model_name`。解决方案是：你需要将所有的连接和额外的返回列添加到构成 UNION 的每个 SELECT 语句中。

```sql
(SELECT ma.make_name, mo.model_name, n.color, n.modelyear FROM New_Vehicles n LEFT OUTER JOIN Models mo USING (model_id) LEFT OUTER JOIN Makes ma USING (make_id)) UNION (SELECT ma.make_name, mo.model_name, u.color, u.modelyear FROM Used_Vehicles u LEFT OUTER JOIN Models mo USING (model_id) LEFT OUTER JOIN Makes ma USING (make_id));
```

在 MySQL 中运行这个庞大的查询，你会看到以下结果：

| make_name | model_name | color | modelyear |
|-----------|------------|-------|-----------|
| Ford | Explorer | Dark Blue | 2005 |
| NULL | NULL | Graphite Pearl | 2004 |
| Toyota | Tacoma | Radiant Red | 2005 |
| Chevrolet | Corvette | Daytona Sunset Orange Metallic | 2005 |
| Honda | Accord | Deep Green Pearl | 2003 |
| Volkswagen | Golf | Reflex Silver | 2004 |
| Toyota | Tacoma | Red | 1993 |

最终你得到的是经销商场地上所有车辆的简明列表，包括其制造商、型号、颜色和年份。你将此功能实现在库存应用程序中并发送给经销商审批，但你还未完成。像许多客户一样，经销商老板很善变，并且再次改变了关于车辆列表需要包含哪些字段的主意。这次，你需要返回数据库中所有车辆的所有信息。你已经知道 New_Vehicles 表和 Used_Vehicles 表的列数不同，那么 UNION 如何满足要求？答案其实非常简单。你只需对缺失列指定 NULL（或你偏好的任何其他值），如下所示：

```sql
(SELECT ma.make_name, mo.model_name, n.color, n.modelyear, n.price, n.description, NULL, 1 FROM New_Vehicles n LEFT OUTER JOIN Models mo USING (model_id) LEFT OUTER JOIN Makes ma USING (make_id)) UNION (SELECT ma.make_name, mo.model_name, u.color, u.modelyear, u.price, u.description, u.certified, u.warranty FROM Used_Vehicles u LEFT OUTER JOIN Models mo USING (model_id) LEFT OUTER JOIN Makes ma USING (make_id) \G
```

运行此查询，你将看到以下内容：

```
*************************** 1. row ***************************
make_name: Ford
model_name: Explorer
color: Dark Blue
modelyear: 2005
price: NULL
description: Popular SUV; great for moving people or cargo across town, or wherever
your adventures may take you.
NULL: NULL
1: 1
```

```
*************************** 2. row ***************************
make_name: NULL
model_name: NULL
color: Graphite Pearl
modelyear: 2004
price: NULL
description: Last of the 2004 stock! Must sell! Loaded, all options!
NULL: NULL
1: 1
```

```
*************************** 3. row ***************************
make_name: Toyota
model_name: Tacoma
color: Radiant Red
modelyear: 2005
price: NULL
description: Come drive this terrific truck! 4WD, extended cab, many options.
NULL: NULL
1: 1
```

```
*************************** 4. row ***************************
make_name: Chevrolet
model_name: Corvette
color: Daytona Sunset Orange Metallic
modelyear: 2005
price: NULL
description: The all new C6 Corvette, the next generation of classic American
sportscars. 400HP V8; Very fast!
NULL: NULL
1: 1
```

```
*************************** 5. row ***************************
make_name: Honda
model_name: Accord
color: Deep Green Pearl
modelyear: 2003
price: NULL
description: Excellent condition, off-lease vehicle; Must see!
NULL: 0
1: 1
```

```
*************************** 6. row ***************************
make_name: Volkswagen
model_name: Golf
```



# 第 4 章

make_name: 丰田
model_name: R32
color: 反射银
modelyear: 2004
price: NULL
description: R32 限量版；低里程；低调且 surprisingly 实用；配置丰富。
NULL: 1
1: 1

make_name: 丰田
model_name: Tacoma
color: 红色
modelyear: 1993
price: NULL
description: 运行尚可；四驱；深色车窗，售后音响；需要稍加维护。
NULL: 0
1: 0

你首先会注意到，结果看起来与你之前的结果略有不同。这是因为查询末尾使用了 `\G` 终止符，它使 MySQL 以垂直方式显示结果（否则表格对于本书来说会太宽）。除此之外，所有信息都完整无缺。在 *New_Vehicles* 表中，针对缺失的“certified”列指定的 **NULL** 值存在，由于所有新车都有保修，你指定的占位符值 1 也存在。你将更改发送给客户端，他们对此感到满意（至少暂时如此）。

### 全文搜索

到目前为止，车场老板们已经对你能够精确查询他们所需信息、提供各种列表以提高销售人员生产力的能力印象深刻——但他们仍然想要更多。他们现在想要一种通过关键字搜索汽车库存的方法。他们的搜索需求并不复杂，但在 **WHERE** 子句中进行简单的 **LIKE** 比较是无法完成这项任务的。

你需要的功能恰好内置于 **MySQL** 中——全文搜索。全文搜索在 **MySQL** 中默认启用，允许你对指定的任何文本列执行自然语言搜索。不过，你不能随意开始进行全文搜索——你必须先做一些准备工作。

#### 启用全文搜索

在 **MySQL** 中启用全文搜索只需简单地创建表列上的索引。你可以用两种方式做到这一点：在创建表时，作为 **CREATE TABLE** 命令的一部分；或者在表的生命周期后期。

##### 创建启用全文搜索的新表

你要创建的第一个全文索引将成为一个全新表的一部分。要在创建表时指定全文索引，你只需在列定义的末尾指定全文索引和要索引的列列表：

```
CREATE TABLE tablename (column\_specs, FULLTEXT (columns\_to\_index) )
```

你可以在 **FULLTEXT** 列列表中指定单列，或以逗号分隔的列表指定多列。现在是时候在 `VehicleInventory` 数据库中实际创建一个启用全文搜索的表了：

```
CREATE TABLE testft (testint int, testvc varchar(50), testtxt text, FULLTEXT (testvc, testtxt) );
```

你刚刚创建了一个新表，在 **testvc** 和 **testtxt** 列上建立了全文索引。

#### 修改现有表以支持全文搜索

修改现有表以支持全文搜索稍微麻烦一些，但也不算太复杂。要为现有表添加全文搜索功能，你使用 MySQL 的 **ALTER TABLE** 命令，如下所示：

```
ALTER TABLE tablename ADD FULLTEXT (columns)
```

现在为 `New_Vehicles` 表添加全文索引：

```
ALTER TABLE New_Vehicles ADD FULLTEXT (description);
```

完成后，是时候充分利用这些索引了。

#### 使用全文搜索进行查询

在启用了全文索引的 MySQL 表中进行搜索是一个相对轻松的过程。你只需在 **WHERE** 子句中使用 **MATCH()** 函数，如下所示：

```
SELECT [columns] FROM [table] WHERE MATCH ([indexed_columns]) AGAINST ('keyword')
```

在 **MATCH** 的参数列表中，你可以指定任意数量的列，只要它们是全文索引的一部分即可。

回到车辆库存数据库，是时候对新车辆列表执行搜索了。要搜索单词“options”（选项），你可以使用以下内容：

```
SELECT vehicle_id, description FROM New_Vehicles WHERE MATCH (description) AGAINST ('options');
```

应该返回以下内容：

| vehicle_id | description |
|:---:|:---|
| 2 | Last of the 2004 stock! Must sell!! Loaded, all options! |
| 3 | Come drive this popular truck! 4WD, extended cab, many options. |

全文搜索的另一个巧妙之处在于它可以按相关性对条目进行排序，并返回相关性分数。要利用相关性数据，你可以在 **SELECT** 列表和 **ORDER BY** 子句中使用 **MATCH() . . . AGAINST()** 函数，如下所示：

```
SELECT MATCH (description) AGAINST('options') AS relevance, description FROM
New_Vehicles WHERE MATCH (description) AGAINST('options') ORDER BY MATCH
(description) AGAINST('options') \G
```

返回以下内容：

```
*************************** 1. row **************************
relevance: 0.38341856002808
description: Last of the 2004 stock! Must sell! Loaded, all options!
*************************** 2. row **************************
relevance: 0.38341856002808
description: Come drive this popular truck! 4WD, extended cab, many options.
```

#### 局限性

在使用全文搜索时，必须牢记几个局限性。首先，MySQL 仅支持 MyISAM 表类型的全文索引（将在下一节中介绍）。其次，在大多数情况下，如果你在一个以上的列上创建全文索引，则提供给 `MATCH()` 的列列表必须与你创建全文索引时指定的列表完全相同。最后，MySQL 默认的最低单词/标记长度为四个字符。如果你尝试对少于四个字母的关键字进行全文搜索匹配，将不会返回任何结果。

要更改默认的最低全文单词长度，请确保你的 MySQL 配置文件（*my.cnf*）中存在以下内容：

```
[mysqld]
ft_min_word_len=3
```

你可以使用任何整数作为最小长度（本例中设置为 3）。

### InnoDB 表

使用 MySQL 的优势之一是你不必局限于特定的数据存储引擎。什么是存储引擎？作为服务器，MySQL 为用户提供了一致的接口和查询语言，但它实际上如何存储数据的方式与其解耦紧密程度较低。MySQL 中的不同存储引擎提供了存储和访问数据的不同方式，从可靠的默认 MyISAM，到内存 Heap 表的极速性能，以及介于两者之间的所有中间状态。你可以使用的最灵活、功能最强大的表类型之一是 InnoDB。由芬兰赫尔辛基的 InnoBase Oy 创建的 InnoDB 存储引擎，为 MySQL 提供了安全且高效的数据存储和处理方式，并赋予了 MySQL 一些 MyISAM 或大多数其他表类型所不具备的额外功能。

#### InnoDB 优势

虽然默认的 MyISAM 表类型提供了存储简单数据结构的成熟且快速的方式，但它缺乏许多开发者希望具备的一些功能——而 InnoDB 可以提供。自 MySQL 4.0 以来默认可用，InnoDB 表允许你使用事务、行级锁定，以及最重要的，外键约束。

外键约束提供了一种在关联表之间维护引用完整性的方法。在 `VehicleInventory` 数据库中，`New_Vehicles` 和 `Used_Vehicles` 表包含一个用于指定车辆型号（进而指定制造商）的 `model_id` 列。可以对外键约束应用于 `model_id` 列，以确保不能向该列插入任何不存在于 `ModelList` 表中的值。在默认的 MyISAM 表类型中，MySQL 无法自动执行此类规则，而在较大的数据库中，这可能导致表中出现大量无效值。InnoDB 为 MySQL 提供了一种执行此类规则的方法，从而确保数据始终保持相关性。

> *受外键约束的列仅允许引用表中存在的值，有一个例外：NULL。在其他受外键控制的列中，允许使用 NULL 值。*

#### InnoDB 劣势

不幸的是，InnoDB 的优势伴随着一些特别令人烦恼的问题。首先，InnoDB 表不支持全文搜索。当你决定是否使用 InnoDB 时，你必须始终考虑未来对全文索引的需求，以及对于特定表而言，这与引用完整性相比哪个更重要。

其次，InnoDB 存储引擎在 `AUTO_INCREMENT` 列方面受到轻微限制。创建表时，InnoDB 表不允许你指定自增序列的初始值。这未必是决定性的障碍，但在设计数据库架构时需要考虑这一点。

### 使用 InnoDB

了解 InnoDB 存储引擎的最佳方法是让它发挥实际作用。现在，你将通过从头创建新表以及修改另一个表来启用 InnoDB 引擎。之后，你将尝试外键的不同方面。

#### 从头创建 InnoDB 表

使用 InnoDB 存储引擎创建新表与创建标准 MyISAM 表几乎没有区别。唯一的關鍵区别是你必须在创建表命令的末尾指定 `ENGINE`：

```
CREATE TABLE tablename (column_definitions) ENGINE=InnoDB;
```

很简单，对吧？在你的 MySQL 数据库中实际试一试：

```
CREATE TABLE innodtest (innocol int) ENGINE=InnoDB;
```

如果一切顺利，你应该看到以下内容：

```
Query OK, 0 rows affected
```

至此，你便创建了一个简单的 InnoDB 表。




# 第 4 章

#### 将现有的 MyISAM 表转换

从头创建一个新的 InnoDB 表固然很好，但你手头有一些表非常希望使用 InnoDB 存储引擎。你需要一种方式将这些表从默认的 MyISAM 表类型转换过来。幸运的是，在 MySQL 中更改表的存储引擎是一个简单的任务——只需使用 `ALTER TABLE` 命令并重新指定表的引擎即可。要将 *New_Vehicles* 表（当前使用默认的 MyISAM 表类型）进行转换，请使用以下命令：

```sql
ALTER TABLE New_Vehicles ENGINE=InnoDB;
```

对数据库运行此命令，你将看到以下内容：

```
ERROR 1214 (HY000): The used table type doesn’t support FULLTEXT indexes
```

MySQL 并没有如你预期那样转换你的表，而是给出了一个错误信息。如前所述，MySQL 中的 InnoDB 表目前不支持全文索引。如果你尝试将定义了全文索引的 MyISAM 表转换为 InnoDB，你将收到此消息。为了完成本练习，你需要删除全文索引才能转换该表：

```sql
ALTER TABLE New_Vehicles DROP INDEX description;
```

现在你应该能够继续转换该表了：

```sql
ALTER TABLE New_Vehicles ENGINE=InnoDB;
```

这次，你的查询应该成功，并且你会看到类似以下的内容：

```
Query OK, 4 rows affected (0.76 sec)
Records: 4  Duplicates: 0  Warnings: 0
```

#### 外键

你不会无缘无故将表从 MyISAM 切换到 InnoDB，而在大多数情况下，外键是一个很好的理由。一旦你设置好 InnoDB 表，添加外键以强制实施引用完整性只是时间问题。虽然表面上听起来很简单，但在创建外键时有许多选项需要考虑。

创建外键的 `ALTER TABLE` 命令最基础的格式看起来像这样：

```sql
ALTER TABLE [tablename] ADD CONSTRAINT [key_name] FOREIGN KEY ([indexed_column])
REFERENCES [foreign_table] ([id_column])
```

开始时，你告诉 MySQL 要更改哪个表，以及要做什么（添加外键）。使用 `CONSTRAINT [key_name]`，你可以可选地为键指定一个名称，如果你计划将来修改该键，这通常是个好主意。需要引用完整性的列名紧随其后，放在括号中。之后是 `REFERENCES` 关键字、将被检查的外部表名称，以及该外部表中要引用的特定列。

将此应用于车辆库存数据库，向 *New_Vehicles* 表添加一个名为 *refmd1* 的外键，以将 *model_id* 列与 *Models* 表中的 *model_id* 列进行对比：

```sql
ALTER TABLE New_Vehicles ADD CONSTRAINT refmd1 FOREIGN KEY (model_id) REFERENCES
Models (model_id);
```

在 MySQL 中运行此命令，你将看到类似以下内容：

```
ERROR 1005 (HY000): Can't create table './vehicleinventory/#sql-1591_2.fm' (errno: 150)
```

这次错误信息在追踪原因方面并不像我们希望的那么有帮助。在这种情况下，错误抛出是因为涉及外键的其中一个表没有使用 InnoDB 引擎。你已经将 *New_Vehicles* 表转换为 InnoDB，但 *Models* 表仍然是 MyISAM。为了正确创建外键，涉及的两个表都需要使用 InnoDB 引擎，因此你必须相应地更改它们：

```sql
ALTER TABLE Models ENGINE=InnoDB;
```

然后添加外键：

```sql
ALTER TABLE New_Vehicles ADD CONSTRAINT refm1 FOREIGN KEY (model_id) REFERENCES Models (model_id);
```

现在你的外键正在保护 *New_Vehicles* 中的 *model_id* 列免受错误数据的影响……或者它是这样吗？确定这一点的最佳方法是测试它。尝试向 *New_Vehicles* 插入一行数据，使用一个完全错误的 *model_id*：

```sql
INSERT INTO New_Vehicles (model_id) VALUES (12345);
```

当你尝试执行此查询时，它应该返回以下内容：

```
ERROR 1216 (23000): Cannot add or update a child row: a foreign key constraint fails
```

正如预期的那样，外键检查发现该值不在 *Models* 表中，并拒绝允许插入该行。你设法阻止了带有不良数据的新行，但那些正在被修改的现有行呢？尝试此查询：

```sql
UPDATE New_Vehicles SET model_id=12345 WHERE vehicle_id=1;
```

正如你所见，外键也会阻止错误的更新：

```
ERROR 1216 (23000): Cannot add or update a child row: a foreign key constraint fails
```

因此，外键成功地保护了表免受有害的 INSERT 和 UPDATE 操作，但当 *Models* 表中的值发生变化时会发生什么？请查看以下查询，其中你尝试更改一个现有的 *model_id*：

```sql
UPDATE Models SET model_id=123 WHERE model_id=1;
```

当你运行此查询时，你应该会得到以下错误：

```
ERROR 1217 (23000): Cannot delete or update a parent row: a foreign key constraint fails
```

这个错误仅仅反映了简单 InnoDB 外键相关的另一种行为：如果被引用列的值存在于引用表中，则不能修改该被引用列。如果这不是你想要的行为怎么办？幸运的是，你可以将外键的更新和删除行为指定为五种不同选项之一：RESTRICT、CASCADE、SET NULL、NO ACTION 和 SET DEFAULT。以下是每种行为含义的简要说明：

-   **RESTRICT** 是默认行为。被引用的值不能被更改或删除。
-   **CASCADE** 允许任何更新向下传播到引用表。如果你更新了 Models 表中的 model_id，它将级联到 New_Vehicles 表并更新任何相应的行。请注意，这也适用于删除（如果指定了）——删除父表中的一行将自动删除子表中引用该值的所有行。
-   **SET NULL** 在更新父值时将子表中的值更改为 NULL。
-   **NO ACTION** 只是告诉数据库允许对父表的更改，并对子表不做任何操作。
-   **SET DEFAULT** 在父值被更改或删除时，将子表中的值更改为其 DEFAULT 值。

实现这些行为只需在外键定义的末尾添加所需的 `ON DELETE` 或 `ON UPDATE` 子句，如下所示：

```sql
ALTER TABLE [tablename] ADD CONSTRAINT [key_name] FOREIGN KEY ([indexed_column])
REFERENCES [foreign_table] ([id_column]) ON UPDATE [update behavior] ON DELETE
[delete behavior]
```

要将现有键更改为支持不同的更新和删除行为，你必须先删除旧键，然后使用新行为重新创建外键。要将 New_Vehicles 表的外键更改为级联任何更新，并在删除模型时设置为 NULL，请使用以下内容：

```sql
ALTER TABLE New_Vehicles DROP FOREIGN KEY refmdl;
ALTER TABLE New_Vehicles ADD CONSTRAINT refmdl FOREIGN KEY (model_id) REFERENCES
Models (model_id) ON UPDATE CASCADE ON DELETE SET NULL;
```

现在，每当 Models 表中的 model_id 发生变化时，新值就会传播到 New_Vehicles 中使用原始值的所有行。请亲自查看：

```sql
UPDATE Models SET model_id=123 WHERE model_id=1;
SELECT * FROM New_Vehicles \G
```

更新将成功，并返回类似以下内容：

```
*************************** 1. row ***************************
vehicle_id: 1
model_id: 123
price: NULL
color: Dark Blue
description: Poplar SUV; great for moving people or cargo across town, or wherever
your adventures may take you.
modelyear: 2005
*************************** 2. row ***************************
vehicle_id: 2
model_id: NULL
price: NULL
color: Graphite Pearl
description: Last of the 2004 stock! Must sell! Loaded, all options!
modelyear: 2004
*************************** 3. row ***************************
vehicle_id: 3
model_id: 4
price: NULL
color: Radiant Red
description: Come drive this popular truck! 4WD, extended cab, many options.
modelyear: 2005
*************************** 4. row ***************************
vehicle_id: 4
model_id: 5
price: NULL
color: Daytona Sunset Orange Metallic
description: The all new C6 Corvette, the next generation of classic American sports cars. 400HP V8; Very fast!
modelyear: 2005
```

#### 从 InnoDB 转换回 MyISAM

你体验了 InnoDB 表和外键，但你决定更希望拥有全文搜索功能。转回 MyISAM 是一个相对无痛的过程。通常它只涉及两个步骤：移除任何 InnoDB 特有的功能，如外键，并使用 `ALTER TABLE` 将存储引擎类型改回 MyISAM。要将 New_Vehicles 表转回 MyISAM，请执行以下操作：

```sql
ALTER TABLE New_Vehicles DROP FOREIGN KEY refmid1;
ALTER TABLE New_Vehicles ENGINE=MyISAM;
```

此时，New_Vehicles 表已改回使用 MyISAM 存储引擎，你再次获得在该表上添加和使用全文索引的能力。

### 访问控制

作为 MySQL 数据库管理员，你将承担的最重要的任务之一是控制谁可以访问系统以及他们可以访问哪些资源。在大多数情况下，你每个数据库只需要少数几个用户帐户，而且你需要创建的帐户应该只授予执行其任务所需的最小访问权限。幸运的是，MySQL 提供了多种方式来控制谁有权访问你的系统以及具体哪些资源。

### 用户管理

为了帮助控制数据库中的用户帐户，MySQL 提供了几种维护用户帐户的方式。无论是协作开发者的帐户、精通技术的客户端帐户，还是系统的基于 Web 的前端，每个用户都需要专门授权以访问他们所需的资源。





# 第 4 章

为实际应用场景配置数据库时，你需要做的第一件事之一就是设置用户或系统本身可能需要的一些账户。为了在数据库中为用户设置专门的访问权限，你需要了解 MySQL 可以控制访问的不同层级。MySQL 4.1 在权限方面可以区分四种不同的访问级别：全局级别、数据库级别、表级别和列级别。

全局级别权限是最强大的权限，适用于运行在 MySQL 实例上的所有数据库。通常，这类权限保留给管理员账户，因为应用程序或最终用户极少需要访问数据库服务器操作的所有方面。

数据库级别权限如其名称所示，应用于数据库级别。数据库级别访问通常由特定数据库或应用程序的管理员使用，它赋予了用户对指定特定数据库的完全控制权。

表级别权限按表为基础进行应用。你可以为用户在特定表或一组表上创建或移除访问权限。这种访问控制级别通常在配置数据库以便应用程序直接访问时使用——应用程序只需对每个表拥有特定类型的访问权限，而不需要更多。

列级别权限是 MySQL 提供的最精细的控制级别。正如你所料，它控制对给定表中特定列或列组的访问。

#### 使用 GRANT

现在你理解了 MySQL 访问系统的不同范围，是时候看看如何实际控制权限了。

为了创建用户账户并添加权限，MySQL 提供了 **GRANT** 命令。**GRANT** 命令相对简单，只要你知道你授予的是什么访问权限以及授予给谁。**GRANT** 命令的通用语法如下：

```
GRANT [privileges] ON [resource] TO [identity]
```

让我们花一点时间剖析 **GRANT**。命令的第一部分 **GRANT [privileges]** 是你指定在资源（稍后指定）上允许哪些权限的地方。下表展示了一些你可以使用的更常见的权限。

| 权限 | 提供内容 |
| :--- | :--- |
| ALL [PRIVILEGES] | 设置所有简单权限，但不包括 GRANT OPTION |
| ALTER | 允许使用 ALTER TABLE |
| CREATE | 允许使用 CREATE TABLE |
| DELETE | 允许使用 DELETE |
| DROP | 允许使用 DROP TABLE |
| INDEX | 允许使用 CREATE INDEX 和 DROP INDEX |
| INSERT | 允许使用 INSERT |
| SELECT | 允许使用 SELECT |
| UPDATE | 允许使用 UPDATE |
| USAGE | “无权限”的同义词；用户可以登录但仅此而已 |

命令的第二部分 ON [resource] 是你指定要提供访问权限的数据库级别和项目的地方。要在全球级别授予访问权限，你指定 `*.*` 作为资源，如下所示：

```
GRANT [privileges] ON *.* TO [identity] ...
```

在授予数据库级别访问权限时，你指定数据库名称，后跟 `.*`。例如，如果你想授予对 testdb 数据库的访问权限，你可以使用类似以下内容：

```
GRANT [privileges] ON testdb.* TO [identity] ...
```

要为数据库内的特定表创建权限，你提供数据库名称，后跟表名（用点号分隔）。如果你试图指定 testdb 数据库中 testtable 表的访问权限，你可能会使用类似以下内容：

```
GRANT [privileges] ON testdb.testtable TO [identity] ...
```

授予列级别权限与前三个逻辑层级的向下 progression 略有不同。在授予列级别权限时，你必须在列表中每个权限后的括号内指定列列表，如下所示：

```
GRANT SELECT (column1), INSERT (column1) ON testdb.testtable TO [identity] ...
```

在指定列级别权限时，你必须在 ON 之后使用完整的表级别语法，否则 MySQL 将返回错误。

GRANT 命令的最后一个关键部分 TO [identity] ...，是你指定访问权限授予给谁，以及用户必须满足的任何可选要求才能获得此访问权限的地方。为了满足 GRANT 的 TO ... 部分，你最少必须提供用户名/主机组合。在 MySQL 中，每个不同的用户必须至少为其用户名和 localhost 设置基本的使用权限。例如：

```
GRANT USAGE ON *.* TO testuser@localhost
```

这里，用户 'testuser' 在全局范围内被授予了基本的使用访问权限，这等同于完全没有访问权限，但用户现在已被系统识别。一旦创建了 localhost 账户，你可以为相同用户名在任何指定的远程主机上创建额外的访问语句：

```
GRANT SELECT ON testdb.* TO testuser@192.168.1.2
```

需要注意的是，如果你尝试为没有 localhost 条目的用户创建远程访问账户，MySQL 不会抱怨。但是，你的应用程序可能会抱怨——它们可能无法远程连接，而且在刚开始熟悉 MySQL 访问系统时，这是一个常见的令人头痛的问题。

在大多数情况下，用户账户在登录时也要求密码是很重要的。在通过 GRANT 创建账户时添加密码，请在 GRANT 命令末尾添加短语 `IDENTIFIED BY ‘password’`，如下所示：

```
GRANT [privileges] ON [resource] TO [identity] IDENTIFIED BY ‘[password]’;
```

> 你不需要在将密码用作 GRANT 命令中的密码之前预先加密它——MySQL 在将其存储在系统中之前会自动加密密码。

既然你已经看到了一些如何使用 GRANT 的通用示例，你可以尝试在一个实际数据库上操作。你将向车辆库存数据库添加三个用户。一个用户将获得整个数据库的完全访问权限。第二个用户将获得 New_Vehicles 表的 SELECT、UPDATE、INSERT 和 DELETE 访问权限。第三个也是最后一个用户将仅获得 New_Vehicles 表中 color 列的 SELECT 访问权限。

首先，创建拥有数据库中所有权限的用户：

```
GRANT ALL PRIVILEGES ON VehicleInventory.* TO testuser1@localhost IDENTIFIED BY ‘testpass1’;
```

接下来，创建具有有限全表权限的用户：

```
GRANT SELECT, INSERT, UPDATE, DELETE ON VehicleInventory.New_Vehicles TO testuser2@localhost IDENTIFIED BY ‘testpass2’;
```

最后，创建第三个具有极其有限访问权限的用户：

```
GRANT SELECT (color) ON VehicleInventory.New_Vehicles TO testuser3@localhost IDENTIFIED BY ‘testpass3’;
```

#### 使用 REVOKE

现在你可以使用 GRANT 命令创建用户和权限，但你仍然需要一种方法来撤销权限。为此，你使用 REVOKE。REVOKE 命令看起来几乎与 GRANT 命令完全相同：

```
REVOKE [privileges] ON [resource] FROM [identity]
```

注意 REVOKE 和 GRANT 语法之间唯一的实际区别：使用 FROM 代替 TO，并且不需要添加 IDENTIFIED BY 短语。

为了快速查看 REVOKE 在实时数据库上的操作，请尝试以下查询：

```
REVOKE ALL PRIVILEGES ON VehicleInventory.New_Vehicles FROM testuser2@localhost;
```

在这简单的一击之中，你抹去了 testuser2 账户拥有的任何权限。

在撤销权限时，你通常必须列出用户拥有明确权限的特定表、数据库和列。如果你使用的是 MySQL 4.1.2 或更高版本，你可以用一个简洁的命令快速清除用户在任何权限级别的所有权限：

```
REVOKE ALL PRIVILEGES, GRANT OPTION FROM [identity]
```

如果你想从系统中彻底删除 `testuser3`，你会发送以下内容：

```
REVOKE ALL PRIVILEGES, GRANT OPTION FROM testuser3@localhost;
```

#### GRANT 和 REVOKE 的替代方案

如果出于某种原因，你不想使用 GRANT 或 REVOKE 命令，你可以手动创建用户并直接将权限应用于 MySQL 访问表。

MySQL 将不同级别的用户权限存储在内建的 `mysql` 数据库中的四个主要表中。这四个主要访问表中的每一个都对应四种不同的访问级别。

在全局级别，有一个 `user` 表，其结构如下：

| 字段 | 类型 |
| :--- | :--- |
| Host | varchar(60) |
| User | varchar(16) |
| Password | varchar(41) |
| Select_priv | enum('N','Y') |
| Insert_priv | enum('N','Y') |
| Update_priv | enum('N','Y') |
| Delete_priv | enum('N','Y') |
| Create_priv | enum('N','Y') |
| Drop_priv | enum('N','Y') |
| Reload_priv | enum('N','Y') |
| Shutdown_priv | enum('N','Y') |
| Process_priv | enum('N','Y') |
| File_priv | enum('N','Y') |
| Grant_priv | enum('N','Y') |
| References_priv | enum('N','Y') |
| Index_priv | enum('N','Y') |
| Alter_priv | enum('N','Y') |
| Show_db_priv | enum('N','Y') |
| Super_priv | enum('N','Y') |
| Create_tmp_table_priv | enum('N','Y') |
| Lock_tables_priv | enum('N','Y') |
| Execute_priv | enum('N','Y') |

> 表格续见下页




# 第 4 章

| 字段 | 类型 |
|:---|:---|
| Repl_slave_priv | enum('N','Y') |
| Repl_client_priv | enum('N','Y') |
| ssl_type | enum('','ANY','X509','SPECIFIED') |
| ssl_cipher | Blob |
| x509_issuer | Blob |
| x509_subject | Blob |
| max_questions | int(11) unsigned |
| max_updates | int(11) unsigned |
| max_connections | int(11) unsigned |

用户表（user table）包含系统中所有用户的列表，以及该用户可能拥有的任何全局权限。与访问权限相关的关键字段是所有后缀为 `_priv` 的列。请注意，所有权限列的默认值均为 `no`。

数据库表（db table）保存数据库级别访问权限的记录。db 表的结构如下：

| 字段 | 类型 |
|:---|:---|
| Host | varchar(60) |
| Db | varchar(64) |
| User | varchar(16) |
| Select_priv | enum('N','Y') |
| Insert_priv | enum('N','Y') |
| Update_priv | enum('N','Y') |
| Delete_priv | enum('N','Y') |
| Create_priv | enum('N','Y') |
| Drop_priv | enum('N','Y') |
| Grant_priv | enum('N','Y') |
| References_priv | enum('N','Y') |
| Index_priv | enum('N','Y') |
| Alter_priv | enum('N','Y') |
| Create_tmp_table_priv | enum('N','Y') |
| Lock_tables_priv | enum('N','Y') |

只有当用户需要显式的数据库级别权限时，才会在此表中显示。

另一个表 `tables_priv` 存储表级别操作的权限：

| 字段 | 类型 |
|:---|:---|
| Host | char(60) |
| Db | char(64) |
| User | char(16) |
| Table_name | char(64) |
| Granter | char(77) |
| Timestamp | timestamp |
| Table_priv | set('Select', 'Insert', 'Update', 'Delete', 'Create', 'Drop', 'Grant', 'References', 'Index', 'Alter') |
| Column_priv | set('Select', 'Insert', 'Update', 'References') |

与 db 表类似，用户只有在其需要表级别权限时才会出现在此表中。

最后一个表 `columns_priv` 包含列级别的访问定义，其结构如下：

| 字段 | 类型 |
|:---|:---|
| Host | char(60) |
| Db | char(64) |
| User | char(16) |
| Table_name | char(64) |
| Column_name | char(64) |
| Timestamp | timestamp |
| Column_priv | set('Select', 'Insert', 'Update', 'References') |

为什么你需要知道这些表的详细细节？如果你想在不使用 `GRANT` 或 `REVOKE` 的情况下添加或移除访问权限，就必须针对这些核心表使用标准的 `INSERT`、`UPDATE` 和 `DELETE` 命令。

首先创建数据库中的用户，无论访问级别如何，他们必须存在于 user 表中：

```sql
INSERT INTO mysql.user (Host, User, Password) VALUES ('localhost', 'testuser6', 
PASSWORD('testpass6') );
```

请注意，这里使用了 `PASSWORD()` 函数，而在 `GRANT` 语法中则不使用。`GRANT` 命令会自动使用 `PASSWORD()` 函数加密密码；像这样手动插入则不会，因此你必须自己进行加密。

要添加访问权限，只需在相应的表中插入一行，并为所需的每个权限列指定 Y。要授予你新创建的用户在 `VehicleInventory` 数据库上的数据库级别 `SELECT`、`UPDATE`、`INSERT` 和 `DELETE` 权限，请使用以下命令：

```sql
INSERT INTO mysql.db (Host, Db, User, Select_priv, Insert_priv, Update_priv, Delete_priv) VALUES ('localhost', 'VehicleInventory', 'testuser6', 'Y', 'Y', 'Y', 'Y');
```

如果你需要撤销用户权限，只需对所需的表执行 `DELETE` 操作。要移除 `testuser6` 的数据库级别权限，请使用此查询：

```sql
DELETE FROM mysql.db WHERE Host='localhost' AND User='testuser6';
```

完全从数据库中移除用户稍微复杂一点。你必须首先移除授予该用户的所有权限，然后才可以使用 `DELETE` 命令将其从用户表中移除。

为了让 MySQL 感知到你刚刚手动更改的权限，你必须重新加载权限表：

```sql
FLUSH PRIVILEGES;
```

如果在进行访问更改后没有刷新权限，那么 MySQL 在下一次重启之前不会反映这些更改。这适用于你对任何访问级别做出的任何手动权限更改——使用 `GRANT` 或 `REVOKE` 不需要重新加载权限表。

#### 服务器限制

在更大范围内限制服务器访问的另一种方式是实际上限制服务器整体的远程访问。如果你的数据库仅为直接登录该机器上的用户提供服务，则几乎没有必要让服务器接受远程网络连接。若要阻止 MySQL 监听传入的网络连接，请确保 MySQL 配置文件（通常是 `my.cnf`）的 `[mysqld]` 部分中存在以下内容：

```ini
[mysqld]
skip-networking
```

将该语句添加到配置文件中，然后重启 MySQL 服务器进程，即可禁用对 MySQL 的任何传入流量。如果你的网络和服务器安全至关重要，且只有本地账户需要访问权限，这种措施很重要。

### 分析数据库

虽然你使用数据库的时间大部分将花在添加、更新、检索和删除数据上，但有时你需要立即了解数据库结构本身的信息。幸运的是，MySQL 提供了一些易于使用的信息工具，以及分析和优化数据库的简单方法。

#### 高级 MySQL

在 **MySQL** 命令 shell 内部，你可以使用几个共享前缀 `SHOW` 的常见命令，以获取有关数据库当前状态的各种信息。以下部分描述了一些常见的 `SHOW` 命令。

##### SHOW COLUMNS

`SHOW COLUMNS` 命令返回表中所有列及其属性的列表。`SHOW COLUMNS` 的一般格式如下：

```sql
SHOW COLUMNS FROM [table] FROM [database]
```

如果你想要获取 `New_Vehicle` 表中所有列的列表，可以使用以下内容：

```sql
SHOW COLUMNS FROM New_Vehicles FROM VehicleInventory;
```

这将返回以下内容：

| 字段 | 类型 | 允许空值 | 键 | 默认值 | 额外信息 |
| --- | --- | --- | --- | --- | --- |
| vehicle_id | int(11) |  | PRI | NULL | auto_increment |
| model_id | int(11) | YES |  | NULL |  |
| price | decimal(10,2) | YES |  | NULL |  |
| color | varchar(200) | YES |  | NULL |  |
| description | text | YES |  | NULL |  |
| modelyear | int(11) | YES |  | NULL |  |

在返回的输出中，`Field` 列包含每个列的名称，`Type` 显示列数据类型，`Null` 指定是否允许列中包含 `NULL` 值，`Key` 指示每个列属于什么键或索引类型，`Default` 显示指定的默认列值，`Extra` 显示给予每个列的任何特殊处理。请注意，此命令在功能上与 MySQL 的 `DESCRIBE [table]` 命令完全相同。

##### SHOW CREATE TABLE

你可能希望了解可以使用什么命令来创建给定的表。为此，你可以使用 `SHOW CREATE TABLE` 命令：

```sql
SHOW CREATE TABLE [table name]
```

要获取用于创建你的 `New_Vehicles` 表的创建命令，请发送：

```sql
SHOW CREATE TABLE New_Vehicles \G
```

针对 `VehicleInventory` 数据库运行此命令将得到以下结果：

```
*************************** 1. row ***************************
Table: New_Vehicles
Create Table: CREATE TABLE `New_Vehicles` (
`vehicle_id` int(11) NOT NULL auto_increment,
`model_id` int(11) default NULL,
`price` decimal(10,2) default NULL,
`color` varchar(200) default NULL,
`description` text,
`modelyear` int(11) default NULL,
PRIMARY KEY (`vehicle_id`)
) ENGINE=MyISAM DEFAULT CHARSET=latin1
```

然后可以在新的数据库中进入整个 CREATE TABLE 命令，以创建 New_Vehicles 表结构的精确副本。

##### SHOW DATABASES

SHOW DATABASES 命令做的正是它看起来做的事情——它显示系统中当前登录账户可访问的所有数据库。只需运行该命令：

```sql
SHOW DATABASES;
```

它将返回当前用户可访问的数据库列表：

```
+--------------------+
| Database           |
+--------------------+
| VehicleInventory |
| mysql              |
+--------------------+
```

##### SHOW GRANTS

SHOW GRANTS 命令列出授予特定用户账户的所有访问权限。例如，要查看在 VehicleInventory 数据库中授予 testuser1 账户的所有访问权限，请使用以下内容：

```sql
SHOW GRANTS FOR `testuser1`@'localhost' \G
```

这将返回以下内容：

```
*************************** 1. row ***************************
Grants for testuser1@localhost: GRANT USAGE ON *.* TO `testuser1`@'localhost'
IDENTIFIED BY PASSWORD '*E69S70P2322D3DC1F956C48199FEB21FF2D7D984'
*************************** 2. row ***************************
Grants for testuser1@localhost: GRANT ALL PRIVILEGES ON `vehicleinventory`.* TO
`testuser1`@'localhost'
*************************** 3. row ***************************
Grants for testuser1@localhost: GRANT SELECT, SELECT (description), INSERT
description), UPDATE (description) ON `vehicleinventory`.`used_vehicles` TO
`testuser1`@'localhost'
```




#### 数据库维护

您已创建好车辆库存数据库，并将其投入生产环境，配置了搜索功能，客户对结果表示满意。现在是时候放松一下了吗？

未必。您可能还需要考虑另一件事，以最小化生产数据库发生灾难性数据丢失时的成本。您需要的是备份。

#### 创建备份

在 MySQL 中创建备份非常容易，这得益于系统附带的一套出色的客户端工具。要创建备份，您可以使用 `mysqldump` 实用程序。您需要做的第一件事是退出 MySQL 客户端（如果需要的话），并回到标准的 shell 提示符：

```
mysql> exit
```

回到命令提示符后，只需调用 `mysqldump` 命令行工具即可。对于大多数数据库备份，以下通用格式即可满足需求：

```
mysqldump --opt database name > backupfile.sql
```

这里您正在调用 `mysqldump` 命令，并告诉它将名为 `database name` 的数据库导出到名为 `backupfile.sql` 的文件中。此外还包含 `--opt` 选项，该选项告诉备份实用程序使用一组通用选项，以输出一种有助于 MySQL 更准确恢复文件格式。

> 如需了解更多的 `mysqldump` 选项，请在命令提示符下输入 `man mysqldump`。

要备份车辆库存数据库，请使用以下命令：

```
mysqldump --opt VehicleInventory > vi_backup.sql
```

> 与 `mysql` 命令行客户端一样，如果您需要提供用户名和密码，请确保在数据库名称之前相应地使用 `-u` 和 `-p` 参数。

现在，您已在 `vi_backup.sql` 文件中拥有一个完整的数据库创建脚本。您可以随时归档此文件，将其恢复到其他服务器，刻录到 CD 或 DVD 上，或执行其他您喜欢的操作。

#### 从备份中恢复数据库

如果服务器崩溃、遭到黑客攻击，或者您只是想在生产数据库中获取一份副本用于开发环境测试，您需要知道如何恢复数据库备份。在 MySQL 中，这非常简单，您可以使用 MySQL 命令行客户端，如下所示：

```
mysql database name < backupfile.sql
```

因此，要恢复 `VehicleInventory` 数据库，请使用以下命令：

```
mysql VehicleInventory < vi_backup.sql
```

请注意，恢复目标数据库的名称必须是系统中已实际存在的数据库。如果您想要将备份恢复到新表中，只需登录 `mysql` 客户端，创建一个您所需名称的空数据库，退出客户端，然后按所需方式恢复备份即可。

###### 总结

希望本章中的信息能帮助您设置复杂的数据库模式，使用复杂的查询，并维护整个系统。掌握了这些基本工具，您将很少遇到无法克服的数据库障碍。作为开发人员，您可能会发现自己在命令行界面花费的时间更少，而更多地在诸如 PhpMyAdmin 或 MySQL AB 自己的 MySQL Administrator GUI 工具上工作。只要这些工具有输入原始命令的方式，您在本章中看到的原始命令和查询都可以应用于其中。您对执行管理和数据操作任务的具体 SQL 的理解，也将有助于您理解任何 GUI MySQL 应用程序中任何文本字段、单选按钮和复选框背后正在发生的事情——或者甚至是在您的 PHP 应用程序本身中。

# 第 5 章

### PHP 配置

当使用 LAMP 技术时，很少有事情比 PHP 的配置方式对编码决策产生更大的影响。任何 PHP 安装的核心都是配置文件 `php.ini`。该文件中的设置可以极大地影响您的应用程序编码方式、服务器性能以及安全性。本章告诉您需要查找和更改哪些设置，以改善您的 PHP 安装，并提供一组脚本来自动根据您的喜好准备 PHP 环境和配置设置。

### 修改 `php.ini`

如前所述，`php.ini` 文件是配置 PHP 安装的主要工具。本节介绍了许多您应该设置的配置指令，以及几个在 PHP 5 中新增的指令。

### 推荐的配置指令

配置 PHP 时，为了确保系统安全并以最快速度运行，需要牢记许多设置：

-   `register_globals = off`：将旧的 PHP 代码迁移到新系统时最常见的问题之一是 PHP 如何处理表单数据和变量。在旧版本的 PHP 中，表单字段会自动转换为与 PHP 引擎同名的全局变量。虽然有些人觉得这很方便，但由于命名和使用上的混淆，它最终成为了安全风险。自 PHP 4.2.0 起，`register_globals` 的默认值为 `off`。您应保持此设置为 `off`，并使用 `$_GET`、`$_POST` 和 `$_COOKIE` 超全局变量，而不是依赖自动创建的变量。

    在开发应用程序时，保持 `register_globals` 设置为 `off` 尤为重要，因为您无法确定任何最终可能部署该应用程序的生产服务器的设置。

-   `display_errors = off`：虽然在开发环境中并非必要且实际上是一种负担，但在生产或公共 Web 服务器上的任何 PHP 应用程序中，将 `display_errors` 设置为 `off` 是个好主意。关闭 `display_errors` 可阻止 PHP 向用户的 Web 浏览器显示任何解析或运行时错误。终端用户看到的任何错误都可能揭示应用程序的内部工作机制，这对希望攻击您网站的恶意人员来说可能是有用的信息。
    -   在开发或调试情况下，保持 `display_errors` 开启以辅助调试是完全可接受的。
-   `log_errors = on`：此设置通常与 `display_errors` 配合使用，告诉 PHP 将通常显示在屏幕上的所有错误记录到文件中。您可以使用该文件进行后续分析或调试，或者使用自己选择的工具定期自动通知网站管理员。
-   `error_log = filename` 或 `error_log = syslog`：`error_log` 指令告诉 PHP 在启用 `log_errors` 时将错误发送到何处。您可以指定 PHP 写入错误的文件名，或者指定 `syslog`，它将错误发送到系统日志守护进程。
-   `error_reporting = E_ALL`：此指令只是告诉 PHP 报告它遇到的所有错误、警告和通知。默认情况下，PHP 显示除通知外的所有内容。显示通知通常是个好主意，尤其是在开发期间，因为它可以帮助您追踪未初始化的变量和其他微小的代码漏洞。
-   `magic_quotes_gpc = off`：`magic_quotes_gpc` 指令告诉 PHP 是否在加载脚本时自动转义输入/表单数据。虽然此设置旨在节省时间，但如果您决定更换数据库，或者使用不使用反斜杠转义特殊字符的数据库，它实际上可能会引发问题。如果您认为有一天可能会更换数据库系统，或者目前使用混合数据库环境甚至根本不使用数据库，最好将此设置为 `off`。
-   `variables_order = “GPCS”`：将 `variables_order` 设置为 `GPCS` 会告诉 PHP 不要自动生成通常保存环境变量的 `$_ENV` 数组——通常在 `variables_order` 设置为 `EGPCS` 时设置。此设置仅出于性能原因推荐，如果您仍需访问环境变量，可以使用 `getenv()` 函数。
-   `allow_call_time_pass_reference = off`：此指令可能不会影响所有代码，但它可以帮助您防止代码因未来版本的 PHP 而过时。将 `allow_call_time_pass_reference` 设置为 `off` 可防止您强制通过引用传递函数参数。如果在此设置关闭时尝试通过引用传递参数（使用 `&` 前缀），系统将生成一个警告。虽然这对生产服务器目前并非关键问题，但在开发应用程序时使用此设置是个好习惯，以确保它们与 PHP 的未来版本兼容。
-   `asp_tags = off`：虽然这在大多数设置中通常不是问题，但如果使用 ASP 风格标签（`<% %>`）而非标准 PHP 标签（`<?php ?>`），当您应用程序移动到具有不同 `asp_tags` 设置的服务器时，最终可能会成为问题。虽然不是关键要求、性能问题或安全问题，但在开发期间保持 `asp_tags` 设置为 `off` 是个好主意，以避免后来的代码兼容性问题。
-   `short_open_tag = off`：与将 `asp_tags` 设置为 `off` 一样，将 `short_open_tag` 设置为 `off` 也有助于确保您的应用程序能够在不同的服务器上通用工作，而不是因简单的配置差异而损坏。





使用 `short_open_tag = off` 的另一个好处是，你可以在脚本中使用 `<?xml ?>` 语句，例如 XML 文档声明。如果将 `short_open_tag` 设置为 on，并试图使用 `<?xml`，则会尝试将 `<? ?>` 包裹内的任何内容解析为 PHP，并抛出错误。

- `zlib.output_compression = on`：将 `zlib.output_compression` 设置为 on 会指示 PHP 在将输出数据发送给最终用户之前，使用 zlib 库对输出数据进行压缩。这与在 Apache 中使用 `mod_gzip` 或 `mod_deflate` 的效果类似：输出字节数减少，从而改善互联网上的传输时间。

### 初次接触 PHP5

除了 PHP5 引入的极大地改进的对象模型外，还新增了一些配置设置。PHP5 新增的配置项如下：

- `mail.force_extra_parameters`
- `register_long_arrays`
- `session.hash_function`
- `session.hash_bits_per_character`
- `zend.zend_compatibility_mode`

以下部分将描述这些新指令。

#### mail.force_extra_parameters

此新指令允许你在 `mail()` 函数中指定要传递给 `Sendmail` 的具体值。通常使用 `mail()` 函数时，你可以传递一个第五个参数，用于向 `Sendmail` 发送额外的命令行参数。当此指令被设置时，`mail()` 第五个参数中指定的任何 `Sendmail` 命令行参数都会被 `mail.force_extra_parameters` 中设置的值自动覆盖。

*mail.force_extra_parameters 设置的任何值在发送邮件时始终会被使用——即使在安全模式下，其中 mail() 的第五个参数是被禁止的。*

#### register_long_arrays

通常，当网站提交表单时，PHP 会获取表单中每个字段的值，并根据表单的方法（`GET` 或 `POST`）将它们放入两个大数组中。如果表单使用 `GET` 提交，则名为 `$HTTP_GET_VARS` 的数组会被填充表单值，每个字段在数组中都有对应的命名索引，此外还有一个名为 `$_GET` 的相同数组，其中持有相同的值。这种重复主要是为了向后兼容——超全局变量 `$_GET` 和 `$_POST` 直到 PHP 4.1.0 才引入，因此许多旧应用程序仍在使用旧的 `$HTTP_*_VARS` 数组。

如果你的应用程序完全没有使用旧样式的数组，出于性能考虑，你应该将此设置为 `off`。

#### session.hash_function

过去，当 PHP 为用户创建新的会话和会话 ID 时，你无法控制使用什么算法来创建会话 ID。有了 `session.hash_function`，你可以选择两种用于创建会话 ID 的哈希算法之一。

将此选项设置为 0 会告诉 PHP 使用 MD5 对会话 ID 进行哈希处理（128 位）。如果你想使用 SHA-1（160 位），则将值设置为 1。

#### session.hash_bits_per_character

为了进一步配置会话 ID，你可以使用 `session.hash_bits_per_character` 来指定在将会话 ID 转换为可读值时，每个字符中存储多少位。选项如下：

- 0: 0-9, a-f
- 5: 0-9, a-v
- 6: 0-9, a-z, A-Z, "-" 和 "+"

#### zend.zend_compatibility_mode

最后一个新的配置设置 `zend.zend_compatibility_mode`，仅仅指定是否要启用与 Zend 引擎 1（PHP4）的兼容性。

### PHP 运行时的配置

直接检查并更改 `php.ini` 中指令的设置通常是监控和修改安装环境的快速且简单的解决方案，但很多时候你无法停机进行更改，或者你需要在脚本运行时了解某个设置。本章这部分的技术将帮助你在服务器仍然运行时进行更改。

#### 获取当前运行时设置

如果你需要知道安装的确切 PHP 版本，PHP 提供了 `phpversion()` 函数，它返回一个列出完整安装版本的字符串。例如：

```php
<?php
echo "The current version of PHP installed is: " . phpversion();
?>
```

这将输出类似以下内容：

```text
The current version of PHP installed is: 5.0.4
```

#### 检索配置设置

有时，简单的版本检查信息不够，你需要更多关于 PHP 配置方式的信息，但你无法直接访问 `php.ini`。要查找运行时配置设置，你有三个主要选择：`ini_get()`、`get_cfg_var()` 和 `ini_get_all()`。

第一个选项 `ini_get()`，将给定的字符串与当前运行时配置进行检查。如果设置匹配，则返回该设置的值；如果未找到匹配项，则返回空字符串：

```php
<?php
echo 'Error reporting: ' . ini_get('error_reporting') . "\n" .
     'Register globals: ' . ini_get('register_globals') . "\n" .
     'Nonexistent setting: ' . ini_get('nonexistent') . "\n";
?>
```

运行此代码应产生类似以下的输出：

```text
Error reporting: 2047
Register globals:
Nonexistent setting:
```

请注意，在这种情况下，错误报告的值实际上是常量 `E_ALL` 的数值等效值。但是 `register_globals` 的值在哪里呢？当 `ini_get()` 返回 `php.ini` 认为是布尔值（off 或 on，0 或 1，yes 或 no）时，它会自动转换它们。“off” 或 “no” 的值会自动转换为 “0”；“yes” 或 “on” 的值会自动变为 “1”。

检索配置设置的第二个选项 `get_cfg_var()`，其行为与 `ini_get()` 几乎相同，只是它直接从 `php.ini` 获取值，而不是来自当前运行时环境。除非你在代码中更改了配置变量（稍后详细介绍），否则值通常应与 `ini_get()` 返回的值匹配。例如，以下代码：

```php
<?php
echo 'Error reporting: ' . get_cfg_var('error_reporting') . "\n" .
     'Register globals: ' . get_cfg_var('register_globals') . "\n" .
     'Nonexistent setting: ' . get_cfg_var('nonexistent') . "\n";
?>
```

除非设置已在活动脚本中更改，否则此代码将产生与以下代码相同的输出：

```php
<?php
echo 'Error reporting: ' . ini_get('error_reporting') . "\n" .
     'Register globals: ' . ini_get('register_globals') . "\n" .
     'Nonexistent setting: ' . ini_get('nonexistent') . "\n";
?>
```

获取配置信息的第三种方式 `ini_get_all()`，像放大版的 `ini_get()`。它不是指定单个值来查找，而是返回一个包含所有已注册配置选项的数组。其返回值也不仅仅限于当前设置——`ini_get_all()` 返回在 `php.ini` 中设置的全局值、当前时刻存在的局部值，以及更改该设置所需的访问级别。

看看这个简单的例子：

```php
<?php
print_r( ini_get_all() );
?>
```

执行此代码，你会得到类似以下的输出：

```text
Array
(
    [allow_call_time_pass_reference] => Array
        (
            [global_value] =>
            [local_value] =>
            [access] => 6
        )

    [allow_url_fopen] => Array
        (
            [global_value] => 1
            [local_value] => 1
            [access] => 4
        )

    [always_populate_raw_post_data] => Array
        (
            [global_value] => 0
            [local_value] => 0
            [access] => 6
        )

    [arg_separator.input] => Array
        (
            [global_value] => &
            [local_value] => &
            [access] => 6
        )

    ...
```

请注意，此输出已大幅简略——实际返回的数组包含超过 150 个不同的项目。还要注意，一些值是空字符串，例如 `allow_call_time_pass_reference` 的全局值和局部值。当 `ini_get_all()` 返回每个设置时，对于 off/on 值，它使用与 `ini_get()` 执行相同的值转换。





# 第 5 章

#### 扩展信息

既然你已经能够获取有关运行时设置的信息，现在是时候学习如何检查扩展及其属性了。PHP 提供了三个内置函数来查找已加载扩展的信息。

第一个是 `extension_loaded()`，它简单地检查给定的扩展是否已加载。你只需提供扩展的名称，它就会返回一个布尔值，指示该扩展是否可用，如下所示：

```php
<?php
if (extension_loaded('mysql'))
{
    echo "MySQL is available.\n";
}
else
{
    echo "MySQL is NOT available.\n";
}

if (extension_loaded('fakesql'))
{
    echo "Fake SQL is available.\n";
}
else
{
    echo "Fake SQL is NOT available.\n";
}
?>
```

运行此代码时，你应该看到以下内容：

MySQL is available.
Fake SQL is NOT available.

如果你需要一次知道多个扩展的状态，PHP 提供了 `get_loaded_extensions()`。与 `ini_get_all()` 类似，`get_loaded_extensions()` 返回所有已加载扩展的数组。考虑以下代码：

```php
<?php
print_r(get_loaded_extensions());
?>
```

根据你的当前配置，可能会增减几个扩展，这应该会生成类似以下的输出：

```text
Array
(
    [0] => xml
    [1] => tokenizer
    [2] => standard
    [3] => SQLite
    [4] => SPL
    [5] => sockets
    [6] => SimpleXML
    [7] => session
    [8] => posix
    [9] => pgsql
    [10] => pcre
    [11] => mysqli
    [12] => mysql
    [13] => iconv
    [14] => gd
    [15] => exif
    [16] => dom
    [17] => ctype
    [18] => calendar
    [19] => bz2
    [20] => bcmath
    [21] => zlib
    [22] => openssl
    [23] => libxml
)
```

一旦你知道某个扩展可用，你可能想了解该特定模块的更多详细信息。要获取某扩展提供的所有函数列表，请使用 `get_extension_funcs()`。与前一些信息性命令一样，它返回一个可用值的数组，但在这种情况下，它提供的是给定扩展的函数列表。例如：

```php
<?php

print_r(get_extension_funcs('simplexml'));

?>
```

运行这段代码应该给出 SimpleXML 扩展提供的所有函数列表：

```text
Array
(
    [0] => simplexml_load_file
    [1] => simplexml_load_string
    [2] => simplexml_import_dom
)
```

#### 魔术引号

如本章前面所述，PHP 允许一种称为“魔术引号”的特殊数据处理机制。当启用魔术引号时，PHP 会自动通过在前面添加反斜杠来转义任何特殊字符——单引号、双引号、NULL——以防止在数据库中使用这些字符串时出现问题。

实际上，PHP 可以自动转义字符串的地方有两个：来自 Web 表单或请求的输入数据，或者来自任何返回任何数据的功能的自动处理。每个替换都由其自己的配置指令控制。输入数据的自动转义由 magic_quotes_gpc 指令控制，而来自任何函数的转义由 magic_quotes_runtime 设置控制。由于这两者都是关键操作，如果忽视它们可能会“弄脏”你的数据，PHP 提供了两个函数来快速确定每个设置当前的状态：用于输入数据的 get_magic_quotes_gpc()，以及用于函数处理器的 get_magic_quotes_runtime()。这两个函数都不需要参数，如果设置启用则返回 1，如果禁用则返回 0。运行此代码：

```php
<?php
    echo "Magic quotes GPC: " . get_magic_quotes_gpc() . "\n";
    echo "Magic quotes runtime: " . get_magic_quotes_runtime() . "\n";
?>
```

根据你当前的配置，你会看到类似以下内容：

```text
Magic quotes GPC: 0
Magic quotes runtime: 0
```

#### 动态更改配置

现在你可以在代码中实时检查配置设置和扩展属性，但如果有不符合你期望的情况，你打算怎么办？利用一些内置的 PHP 函数，你可以改变 PHP 在某些情况下的行为。

#### 没那么神奇的引号

如果你和我一样，你可能不喜欢启用 magic_quotes_runtime，因为它会破坏所有函数的输出。虽然它可以被视为一种便利，但通常只会碍事，并迫使你到处使用 stripslashes() 或 addslashes()。要更改它，你可以使用 set_magic_quotes_runtime()。参数为“1”会打开自动替换；值为“0”则关闭它。

```php
<?php
    // Turn on magic_quotes_runtime
    set_magic_quotes_runtime(1);

    // Turn off magic_quotes_runtime
    set_magic_quotes_runtime(0);
?>
```

不幸的是，magic_quotes_gpc 却不能这么说——你无法在运行时更改其值（稍后会更详细地讨论这一点）。

#### 移除时间限制

如果你发现自己处于脚本运行时间比 PHP 允许的稍长的情况，你有两个选择：优化你的代码使其更快，或者告诉 PHP 稍微多一点耐心。也许你已经尽可能多地优化了代码，而默认的 30 秒超时仍然太快了。

现在是时候让 PHP 在超时前多等待一会儿了。为此，你使用 `set_time_limit()`，并简单地指定你的脚本允许运行的秒数：

```php
<?php

// Set the timeout at one minute
set_time_limit(60);
?>
```

如果你无法准确猜测你的脚本需要多长的时间框架，并且*绝对确定*你没有无限循环，你可以通过将值设置为 `zero` 来完全移除超时：

```php
<?php

// Will run forever if you're not careful
set_time_limit(0);
?>
```

当你使用 `set_time_limit()` 时，有两件事需要注意。首先，如果你的服务器以安全模式运行 PHP，使用 `set_time_limit()` 将不起作用。你必须要么禁用安全模式，要么更改 `php.ini` 中的全局值。其次，每当调用 `set_time_limit()` 时，它会将内部计时器重置为 0。如果你的脚本已经运行了 15 秒，并且你将超时设置为 20 秒，它不会在再运行 5 秒后退出——它会将计数器重置为 0 并重新计数 20 秒，总共 35 秒。

#### 更改指令

如果你只是想更改任何随机的运行时配置设置怎么办？为此，你可以使用函数 `ini_set()`。使用 `ini_set()` 时，只需传递设置的名称和新值。如果函数成功，它将返回旧值；否则，它将返回 false。运行此代码：

```php
<?php

echo "Setting error_reporting to E_STRICT...\n";

$old = ini_set('error_reporting', E_STRICT);

echo "Old value was: " . $old . "\n";
?>
```

你应该看到以下内容：

```text
Setting error_reporting to E_STRICT...
Old value was: 2047
```

如果你决定不再想要更改后的值，你可以使用 `ini_restore()` 来恢复脚本开始执行时的原始值：

```php
<?php

echo "Setting error_reporting to E_STRICT...\n";

$old = ini_set('error_reporting', E_STRICT);

echo "Old value was: " . $old . "\n" .
     "New value is: " . ini_get('error_reporting') . "\n";

ini_restore('error_reporting');

echo "The value is once again: " . ini_get('error_reporting') . "\n";

?>
```

这次运行代码时，它应该成功恢复旧值：

```text
Old value was: 2047
New value is: 2048
The value is once again: 2047
```

在你肆意更改设置之前，你需要意识到在脚本执行过程中实际可以更改的设置是有限制的。如果你还记得之前展示 `ini_get_all()` 的时候，每个配置指令的数组返回了三个值：

```text
...
[allow_call_time_pass_reference] => Array
    (
        [global_value] =>
        [local_value] =>
        [access] => 6
    )
...
```

第三个值，access，指示配置指令实际可以在哪里被更改。为 access 提供的数字实际上是以下任何值的总和：

| 值 | 含义 |
| :----: | :------------------------------------------- |
| 1     | 指令可以在用户脚本中设置。 |
| 2     | 指令可以在 `php.ini`、`.htaccess` 或 `httpd.conf` 中设置。 |
| 4     | 指令可以在 `php.ini` 或 `httpd.conf` 中设置。 |
| 7     | 条目可以在任何地方设置。 |

在示例指令中，allow_call_time_pass_reference 的 access 值为 6，意味着该指令只能在 php.ini、.htaccess 或 httpd.conf 中更改。需要牢记的关键点是，如果设置的 access 值为 2、4 或 6，则无法在脚本执行期间更改。任何尝试这样做的行为都会自动返回 false。




### 自动化版本与功能检查

了解在运行时评估和更改设置的各种方法很有帮助，但在所有脚本或页面中确保跨系统和应用程序的环境一致性可能很繁琐。一种可能的解决方案是将所有版本和扩展检查放入一个独立的脚本中，并在每个页面的顶部引入或包含该脚本。这种方法运行良好，但保持该验证脚本更新很快会变得麻烦。在下一节中，你将查看一个简单的环境检查脚本的变体——它使用一个易于修改的配置文件，并且只需几行代码即可调用。

这组脚本由三个主要代码块和一个简单的配置文件组成。首先，查看该配置文件，在本例中称为 `reqs.xml`：

```xml
<requirements>
    <packages>
        <package name="gd" />
        <package name="mysql" />
        <package name="pgsql" />
    </packages>
    <environment>
        <setting name="register_globals" value="off" />
        <php minversion="5.0.0" />
    </environment>
</requirements>
```

如果你有任何 XML 经验，你会认出这是一组简单的标签，用于建立站点配置。在主要的外围 `<requirements>` 标签内，有两个主要部分。

第一部分 `<packages></packages>` 保存了应用程序所需的所有扩展的列表。每个扩展通过 `<package />` 空标签指定，属性 `name=""` 指定扩展的名称。扩展的名称应与前文提到的 `get_loaded_extensions()` 返回的名称匹配。

第二部分包含定义特定应用程序设置（默认在 `php.ini` 中找到）和 PHP 自身版本要求的定义。每个 `<setting />` 标签可以对应一个 PHP 运行时配置设置。`name=""` 属性匹配配置设置的名称，`value=""` 属性保存将在 `php.ini` 中使用的任何值。`<php />` 标签允许你为应用程序指定版本要求——在 `minversion=""` 属性中指定最低版本，在相应的 `maxversion=""` 属性中指定最高版本（未显示）。

在 `reqs.xml` 的这个示例中，GD、MySQL 和 PostgreSQL 扩展被列为必需，允许的 PHP 最低版本为 5.0.0，并且 `register_globals` 指令必须设置为 off。

> **注意：** 在本示例中指定最低版本 5.0.0 在技术上是多余的——由于不同的对象模型，下面介绍的结构将仅在 PHP 5.0 及更高版本上运行。

### PHP 配置

配置检查器中的下一个文件是 `class.ConfigManager.php`，它充当脚本的中心控制点：

```php
<?php
class ConfigManager
{
    public $configfile = 'reqs.xml';
    public $configtype = 'xml';
    public $errors;
    
    public function __construct($configfile = null, $configtype = null)
    {
        if ($configfile)
        {
            $this->configfile = $configfile;
        }
        if ($configtype)
        {
            $this->configtype = $configtype;
        }
    }
    
    public function processConfig()
    {
        switch ($this->configtype)
        {
            case 'xml':
                require_once 'class.XMLConfigProcessor.php';
                $proc = new XMLConfigProcessor($this->configfile);
                $this->errors = $proc->process();
                break;
        }
        echo nl2br($this->errors);
    }
}
?>
```

这个类的第一部分应该相当直观。它通过声明类 `ConfigManager` 开始，并声明三个公共属性：

```php
<?php
class ConfigManager
{
    public $configfile = 'reqs.xml';
    public $configtype = 'xml';
    public $errors;
```

第一个属性 `configfile` 保存你将使用的配置文件的名称。该配置文件的默认值设置为 `reqs.xml`，因此，除非你使用不同的文件名，否则无需显式设置此属性。`configtype` 属性用于指定配置类型。在这种情况下，提供默认值 `xml` 以表示你的配置是 XML 格式。最后一个属性 `errors` 仅仅是后续处理过程中遇到的任何错误消息的占位符。

接下来是类的构造函数方法：

```php
public function __construct($configfile = null, $configtype = null)
{
    if ($configfile)
    {
        $this->configfile = $configfile;
    }
    if ($configtype)
    {
        $this->configtype = $configtype;
    }
}
```

虽然此构造函数中没有真正神奇的事情发生，但它确实允许在创建对象时传递配置文件和类型，并使用这些值设置相应的属性。

`ConfigManager` 中的最后一个方法是一切魔术发生的地方：

```php
public function processConfig()
{
    switch ($this->configtype)
    {
        case 'xml':
            require_once 'class.XMLConfigProcessor.php';
            $proc = new XMLConfigProcessor($this->configfile);
            $this->errors = $proc->process();
            break;
    }
    
    echo nl2br($this->errors);
}
```

`processConfig()` 方法首先确定配置类型，然后根据配置类型调用必要的代码并利用组件对象。目前，`processConfig` 中只指定了一种类型，即处理 XML 配置文件的类型。随着新配置处理器类型的创建，可以添加任意数量的额外情况。如果你希望在数据库中以存储配置，你可以设计自己的数据库配置处理对象，然后在此 `switch` 中添加一个情况，以调用新类中的任何处理方法。

请注意，`XMLConfigProcessor` 的类文件在此时引入，而不是在文件开头或类的更早位置引入。这样，只有当需要时才解析类文件，有助于减少如果使用不同配置类型时的额外处理。要使用 `XMLConfigProcessor`，只需实例化对象，将配置文件名传递给构造函数，最后调用处理配置的方法（将在本章后面详细介绍）。

这组文件中的下一个文件是一个简单的接口，用于定义任何配置处理类应支持的一组方法：

```php
<?php
interface ConfigProcessor
{
   public function checkExtensions();
   public function checkPHP();
   public function checkConfig();
   public function process();
}
?>
```

这个相当直观——这里定义的四个方法将规定任何配置类型的所有处理类的通用功能。前三个方法 `checkExtensions()`、`checkPHP()` 和 `checkConfig()` 主要用作实现类的内部方法，最后一个方法 `process()` 旨在作为触发其他三个方法的主要公共方法。

配置检查工具的最后一个文件是 `class.XMLConfigProcessor.php`，正如你可能从文件名猜到的，它处理 XML 配置文件：

```php
<?php
require_once 'interface.ConfigProcessor.php';

class XMLConfigProcessor implements ConfigProcessor
{
   public   $xmlfile;
   private $message = '';
   private $xml;

   public function __construct($xmlfile = null)
   {
      if ($xmlfile)
      {
         $this->xmlfile = $xmlfile;
      }
   }

   public function process()
   {
      // 检查所需的库
      if (!$this->checkDeps() or
          !$this->checkConfigAccess())
      {
          return $this->message;
      }

      $this->xml = simplexml_load_file($this->xmlfile);

      if (!$this->checkPHP() or
          !$this->checkExtensions() or
          !$this->checkConfig())
      {
          return $this->message;
      }
   }

   private function checkConfigAccess()
   {
      $returnValue = false;

      // 检查配置文件是否存在且可读
      if (file_exists($this->xmlfile) and
          is_readable($this->xmlfile))
      {
         $returnValue = true;
      }
      else
      {
         $this->message .= "Warning: " .
             "Could not access config file.\n";
      }

      // 清除缓存的文件系统查询
      clearstatcache();

      return $returnValue;
   }

   private function checkDeps()
   {
      $returnValue = true;

      // 检查 SimpleXML
      if (!extension_loaded('SimpleXML'))
      {
         $returnValue = false;
         $this->message .= "Warning: " .
             "SimpleXML extension not available.\n";
      }

      return $returnValue;
   }

   public function checkExtensions()
   {
      $returnValue = true;

      // 检查所有列出的扩展
      // ... (代码继续)
   }
}
?>
```




# 第 5 章

### PHP 配置

```php
$exts = $this->xml->xpath('/packages/package');
foreach ($exts as $ext)
{
    if (!extension_loaded($ext['name']))
    {
        $returnValue = false;
        $this->message .= "Warning: " .
            $ext['name'] .
            " extension not available.\n";
    }
}
return $returnValue;

public function checkPHP()
{
    // Check if PHP requirement is present
    if (count($phpreq = $this->xml->xpath('/environment/php')) == 0)
    {
        return true;
    }

    // Flatten element array
    $phpreq = $phpreq[0];

    // Check minimum version
    if ($phpreq['minversion'] and
        version_compare(PHP_VERSION,
                        $phpreq['minversion']) < 0)
    {
        $this->message .= "Warning: " .
            "PHP version is less than " .
            $phpreq['minversion'] . "\n";
        return false;
    }

    // Check maximum version
    if ($phpreq['maxversion'] and
        version_compare(PHP_VERSION,
                        $phpreq['maxversion']) > 0)
    {
        $this->message .= "Warning: " .
            "PHP version is greater than " .
            $phpreq['maxversion'] . "\n";
        return false;
    }

    return true;
}

public function checkConfig()
{
    $returnValue = true;

    // Get all config values
    $cfg = ini_get_all();

    // Cycle through setting elements
    $settings = $this->xml->xpath('/environment/setting');
    foreach ($settings as $setting)
    {
        $value = $setting['value'];
        // Convert boolean values to ini_get() values
        switch (strtolower($value))
        {
            case 'off':
            case '0':
            case 'false':
            case 'no':
                $value = '';
                break;
            case 'on':
            case 'true':
            case 'yes':
                $value = '1';
                break;
        }

        // Flatten name
        $name = (string) $setting['name'];

        // Check config value, set if needed
        if (!array_key_exists($name, $cfg) or
            ($value !=
             $cfg[$name]['local_value']) and
            ini_set($name, $setting['value']) === false)
        {
            $returnValue = false;
            $this->message .= "Warning: " .
                              "not set to the required value of: " .
                              $name .
                              $setting['value'] . "\n";
        }
    }

    return $returnValue;
}
?>
```

类的开头相当正常——包含接口文件，开始类，并定义一些属性。第一个属性 `$xmlFile` 用于保存 XML 配置文件的文件名。第二个属性 `$message` 将用于捕获在处理文件时生成的任何错误消息。第三个也是最后一个属性 `$xml` 将保存由 PHP 的 SimpleXML 扩展创建的 XML 对象。在属性定义之后，是一个简单的构造函数，如果在实例化时传入了文件名，它会设置 `xmlFile` 的值：

```php
<?php

require_once 'interface.ConfigProcessor.php';

class XMLConfigProcessor implements ConfigProcessor
{

    public $xmlfile;
    private $message = '';
    private $xml;

    public function __construct($xmlfile = null)
    {
        if ($xmlfile)
        {
            $this->xmlfile = $xmlfile;
        }
    }
```

紧跟在构造函数之后的 `process()` 方法是从类外部调用的主要方法。它包含了对类中所有其他组件方法的调用，这些方法用于检查 XML 配置文件中的各个要求和部分。

在 `process()` 的第一部分，你检查配置文件是否可访问，以及 PHP 安装是否具备此类正常运作所需的一切条件：

```php
public function process()
{
    // Check for needed libraries
    if (!$this->checkDeps() or
        !$this->checkConfigAccess())
    {
        return $this->message;
    }
```

如果这些检查中任何一个失败，该方法应终止并返回遇到的任何错误消息。

接下来，使用 SimpleXML 扩展将配置文件的内容加载到一个 XML 对象中，确切地说是一个 `simplexml_element` 对象。这个 `simplexml_object` 可以用于轻松遍历 XML 并在需要时提取标签和属性：

```php
$this->xml = simplexml_load_file($this->xmlfile);
```

最后，`process()` 调用了 `ConfigProcessor` 接口的其余三个方法，以检查 PHP 版本、可用扩展和配置设置：

```php
if (!$this->checkPHP() or
    !$this->checkExtensions() or
    !$this->checkConfig())
{
    return $this->message;
}
```

下一个遇到的方法是 `checkConfigAccess()`。该方法检查 XML 配置文件是否实际存在于文件系统中，如果存在，则进一步检查其是否可读。如果文件不存在或不可读，则会向 `message` 属性添加一条错误消息。请注意，在方法末尾调用了 `clearstatcache()`。PHP 会缓存 `file_exists()` 和 `is_readable()` 的结果，因此，完成后清除结果缓存是个好主意，以防止后续出现异常结果：

```php
private function checkConfigAccess()
{
    $returnValue = false;

    // Check to see if config file exists and is readable
    if (file_exists($this->xmlfile) and
        is_readable($this->xmlfile))
    {
        $returnValue = true;
    }
    else
    {
        $this->message .= "Warning: " .
                          "Could not access config file.\n";
    }

    // Clear cached filesystem lookups
    clearstatcache();

    return $returnValue;
}
```

接下来是 `checkDeps()`。顾名思义，该方法检查类本身的依赖项。对于 `XMLConfigProcessor`，唯一的非标准 PHP 要求是 SimpleXML 扩展的可用性。如果你之后决定修改此类以使用 XML 解析器函数或 DOM XML 扩展（例如），你会需要向该方法添加相应的检查。

要检查 SimpleXML，你只需使用本章前面介绍过的 `extension_loaded()` 函数。如果 SimpleXML 不可用，则向错误消息堆栈中添加另一条错误消息：

```php
private function checkDeps()
{
    $returnValue = true;

    // Check for SimpleXML
    if (!extension_loaded('SimpleXML'))
    {
        $returnValue = false;
        $this->message .= "Warning: " .
                          "SimpleXML extension not available.\n";
    }

    return $returnValue;
}
```

现在，是时候动手整理一下你的 XML 配置文件了。在 `checkExtensions()` 中，你需要做的第一件事是收集配置文件中列出的所有扩展。如前所述，每个包都作为 `<package />` 标签列出，并包含在一组外围的 `<packages></packages>` 标签内。要获取所有这些包的列表，你使用 SimpleXML 的 `xpath()` 方法：

```php
public function checkExtensions()
{
    $returnValue = true;

    // Check for all listed extensions
    $exts = $this->xml->xpath('/packages/package');
```

`xpath()` 方法接受一个表示元素在文档层次结构中的位置（其 Xpath 路径）的字符串，并返回一个 `simplexml_element` 对象数组——在本例中，每个对象代表一个单独的 `<package />` 标签。

一旦你拥有了包标签的数组，只需遍历它们，检查每一个是否可用。由于包名存储在每个 `<package />` 标签的 `name=""` 属性中，你可以使用括号语法和内部的字符串，像访问数组键值一样来访问这些值。再次使用 `extension_loaded()` 函数来检查每个包，如果不可用，则向错误消息堆栈中添加一条消息：

```php
foreach ($exts as $ext)
{
    if (!extension_loaded($ext['name']))
    {
        $returnValue = false;
        $this->message .= "Warning: " .
            $ext['name'] .
            " extension not available.\n";
    }
}

return $returnValue;
```

下一个来自 `ConfigProcessor` 接口的实现方法是 `checkPHP()`。该方法检查 PHP 本身的版本，以确定应用程序是否可以在该版本上运行。在方法开始时，你首先使用 SimpleXML 的 `xpath()` 方法再次检查配置文件中是否存在 PHP 版本要求：

```php
public function checkPHP()
{
    // Check if PHP requirement is present
    if (count($phpreq = $this->xml->xpath('/environment/php')) == 0)
    {
        return true;
    }
```




# 第 5 章

如果发现 PHP 版本要求，然后将 `xpath()` 返回的 `simplexml_elements` 数组替换为数组中的第一个（也是希望唯一的）对象：

```php
// 扁平化元素数组
$phpreq = $phpreq[0];
```

PHP 版本检查可以分配两个属性：一个指定允许的最小 PHP 版本，另一个指定最大版本。对于最小和最大版本，首先检查属性是否存在，然后使用内置的 `version_compare()` 函数，并结合 `phpversion()` 函数。`version_compare()` 函数接受两个参数，每个参数都是一个“PHP 标准化”的版本号字符串，例如 5.0.4 或 5.0.5RC1。如果第一个参数较低，函数返回 −1；如果第二个参数较低，它返回 +1；如果两个参数相等，它返回 0：

```php
// 检查最小版本
if ($phpreq['minversion'] and
    version_compare(phpversion(),
                   $phpreq['minversion']) < 0)
{
    $this->message .= "Warning: " .
                     "PHP version is less than " .
                     $phpreq['minversion'] . "\n";
    return false;
}

// 检查最大版本
if ($phpreq['maxversion'] and
    version_compare(phpversion(),
                   $phpreq['maxversion']) > 0)
{
    $this->message .= "Warning: " .
                     "PHP version is greater than " .
                     $phpreq['maxversion'] . "\n";
    return false;
}

return true;
```

既然您已经检查了所需的扩展，并调查了安装的 PHP 版本是否受您的应用程序支持，那么您需要检查运行时配置，以确保环境与您编码所针对的环境相匹配。在 `checkConfig()` 中，您首先使用 `ini_get_all():` 将所有配置设置收集到一个数组中：

```php
public function checkConfig()
{
    $returnValue = true;

    // 获取所有配置值
    $cfg = ini_get_all();
```

一旦获取了所有当前的运行时设置，您将需要从 XML 配置文件中收集所有 `<setting/>` 标签值的列表。为此，您将再次使用 SimpleXML 的 `xpath()` 函数：

```php
    // 遍历设置元素
    $settings = $this->xml->xpath('/environment/setting');
```

获取所有设置元素的数组后，您需要遍历它们，并检查运行时配置以查看它们是否匹配。在直接比较两者之前，您需要将 XML 配置文件中的每个值转换为与 `ini_get_all()` 的预期结果相匹配。通常，在 `php.ini` 中设置值时，可以使用几种不同的值来表示“真”或“假”。对于真，可以使用 `on`、`true`、`yes` 或 `1`；假由 `off`、`false`、`no` 或 `0` 表示。如前所述，使用 `ini_get()` 或 `ini_get_all()` 返回设置时，表示开或真的值以 `1` 返回，但表示关或假的值将以空字符串 `""` 返回。为了确保 XML 配置值匹配，无论使用哪个 `php.ini` 指示，您可以使用简单的 `switch`：

```php
    foreach ($settings as $setting) {
        $value = $setting['value'];
        // 将布尔值转换为 ini_get() 值
        switch (strtolower($value)) {
            case 'off':
            case '0':
            case 'false':
            case 'no':
                $value = '';
                break;
            case 'on':
            case 'true':
            case 'yes':
                $value = '1';
                break;
        }
    }
```

接下来，您获取配置变量的名称。由于像数组一样访问属性会返回一个 `simplexml_element` 对象，您需要显式将其转换为字符串，以便稍后与字符串值进行比较：

```php
    // 扁平化名称
    $name = (string) $setting['name'];
```

既然您已经拥有了 XML 配置文件中指定的设置名称和值，就可以将其与运行时设置进行比较。首先，您检查运行时配置数组中是否存在该配置设置，然后将其与 XML 文件中的值进行比较。更进一步，如果设置存在但不匹配，尝试使用 `ini_set()` 更改当前的运行时配置变量。如果设置不匹配且无法在运行时更改该设置，则会产生错误消息，并且函数将返回 false：

```php
    // 检查配置值，必要时进行设置
    if (!array_key_exists($name, $cfg) or
        ($value !=
        $cfg[$name]['local_value']) and
        ini_set($name, $setting['value']) === false)
    {
        $returnValue = false;
        $this->message = "Warning: " .
            $name .
            " not set to the required value of: "
            . $setting['value'] . ".\n";
    }
    return $returnValue;
}
?>
```

既然您已经有了这个小型的类层次结构和配置文件来检查运行时环境，您需要实际在脚本中调用它们。在以下 test.php 代码中，您可以看到调用配置检查器是多么简单：

```php
<?php

// 检查 PHP 环境
require_once 'class.ConfigManager.php';
$cfg = new ConfigManager('reqs.xml', 'xml');
$cfg->processConfig();

?>
```

您所要做的只是包含主 ConfigManager 类文件，创建一个新的 ConfigManager 对象，在实例化时传入文件名和类型，并调用 processConfig() 方法以实际检查设置。

### 摘要

希望你现在已经熟悉了一些不同的配置设置和函数，它们可以为你的应用程序注入活力。了解运行时设置的价值通常可以帮助避免难以诊断的 bug，并且能够在运行时更改这些值可以使你的应用程序足够灵活，以应对不同的配置。这种知识和力量，加上自动配置检查，应有助于使你的应用程序在面对不熟悉的服务器可能带来的未知麻烦时尽可能稳健。

### Apache 技巧

本章暂时不再讨论 PHP，转而讨论一些你可能不知道的 Apache 特性。你已经知道 Apache 是可用最流行且功能强大的 Web 服务器，PHP 被设计为与 Apache 协同工作，但你可能不知道你可以扩展 Apache 本身，使你的网站运行得更高效。与其开源性质相符，有许多出色的模块可供 Apache 使用，这些模块扩展了其功能，并为你作为网站管理员提供有用的特性。

本章讨论了其中的三个模块。Mod_rewrite 使你能提供 URL 替换以适应网站变化，但如果正确使用它，你可以利用它来保护你的网站并使其对搜索引擎更友好。Mod_speling 帮助纠正访问你网站的游客无意中犯下的拼写错误。Mod_deflate 使你在向用户发送内容时能够对其进行压缩，从而为你节省带宽费用。Mod_auth_mysql 通过利用用户数据库和 Apache 的身份验证功能，让你可以加强网站安全性。Mod_ssl 允许你加密流向 Web 服务器和从 Web 服务器流出的数据。最后，mod_dav 允许你将 Apache Web 服务器用作分布式文件库。

#### URL 重写

如果你把世界上所有的 Web 开发人员和服务器管理员召集起来，让他们列出可用于 Apache 的最重要的模块列表，很可能 mod_rewrite 会出现在那个列表中——而且有充分的理由。

对于不熟悉的人，Mod_rewrite 是一个提供 URL 重写功能的 Apache 模块。虽然这听起来很简单，但实际上 mod_rewrite 是 Apache 模块中的瑞士军刀。你可以用 mod_rewrite 做什么？除了显而易见的简单 URL 重写之外，mod_rewrite 赋予你保持查询字符串输入安全的能力，保持你的网站对搜索引擎友好，使你的 URL 对用户友好，在重构后保留“旧”URL，并停止热链接。你会发现 mod_rewrite 可以迅速变得不仅仅是一个简单的 URL 更改机器人。

![](img/ab27c6ac898db1f934d39fa127b14657_154_0.png)




## 第 6 章

##### 启用 *mod_rewrite*

在你着手设置 *mod_rewrite* 之前，首先需要检查它是否已经安装。在命令行中，输入：

```shell
/path/to/httpd -l
```

> 显然，请替换为 Apache 中 *httpd* 的实际路径。

如果在列表中看到 *mod_rewrite.c*，说明它已经被编译进了 Apache。如果没有，请检查它是否作为 Apache 的动态模块存在：

```shell
ls /path/to/apache/modules/
```

如果在文件列表中存在 *mod_rewrite.so*，那么 Apache 可以通过对本章节稍后展示的 *httpd.conf* 文件进行少量调整来加载该模块。如果它既没有编译进 Apache，也没有作为共享对象可用，你可以使用操作系统自带的包管理系统来安装它，或者如果你是动手类型，也可以重新编译 Apache 以包含 *mod_rewrite*。

在 Apache 中启用功能时，你通常有两种选择：静态构建到 Apache 二进制文件中，或编译模块为可加载的共享对象。如果将模块静态构建到 Apache 中，它们可以在没有额外配置指令的情况下使用，但模块在 Apache 运行时始终处于活动状态并消耗内存，即使你并不需要它。将模块编译为可加载的共享对象允许你保持 Apache 二进制文件的精简，去除你可能需要也可能不需要的“可选”项目，但它们必须在 *httpd.conf* 中手动配置。两种方法都是完全可以接受的，但如果你不确定选择哪种，共享模块路线因其灵活性而成为热门选择。

在从源代码构建时将 *mod_rewrite* 静态构建到 Apache 中时，请确保你的 configure 文件包含 *--enable-rewrite*，如下所示：

```shell
./configure \
--enable-rewrite \
# ...以及你使用的任何其他 configure 设置
```

如果你选择了动态模块路线，只需在启用 *mod_rewrite* 的那一行末尾添加 *=shared*：

```shell
./configure \
--enable-rewrite=shared \
# ...以及你使用的任何其他 configure 设置
```

然后，只需简单地制作并安装服务器到你的系统。如果你将 *mod_rewrite* 静态构建到 Apache 中，你可以通过重新运行 *httpd -l* 来确认你的重新配置是否成功。如果 *mod_rewrite.c* 出现，说明它已成功添加到 Apache 二进制文件中。

相反，如果你选择了动态模块，请首先检查它是否确实存在于 Apache 模块目录中，文件名为 *mod_rewrite.so*。

```shell
ls /path/to/apache/modules/
```

假设一切顺利，并且 `mod_rewrite.so` 存在于模块目录中，你需要在 httpd.conf 中启用它，方法是取消注释任何现有行，或添加一个新行，如下所示：

```
LoadModule rewrite_module modules/mod_rewrite.so
```

> 不要对任何静态构建到 Apache 中的模块使用 LoadModule 行——仅用于动态共享对象。对静态模块使用 LoadModule 只会产生错误。

在对 httpd.conf 完成所有必要的更改后，重启 Apache。既然你已经成功安装了 mod_rewrite，现在需要查看用于利用 mod_rewrite 的不同配置设置。

#### RewriteRule

Mod_rewrite 提供了少量配置指令，可以提供广泛的重写功能，从非常简单的重定向，到复杂的多规则模式匹配替换。每个重写 URL 的核心是 RewriteRule 指令。

##### RewriteRule 用法

无论你的重写需求多么复杂，你至少需要一个 RewriteRule 来执行转换。RewriteRule 指令的基本格式如下：

```
RewriteRule pattern substitution [flag(s)]
```

RewriteRule 的行为类似于 PHP 的 preg_replace 函数：它接收一个正则表达式模式，将其与传入的 URL 进行匹配，然后使用你定义的规则为 URL 提供替换内容。

在构建用于匹配的正则表达式模式时，你可以使用以下令牌：

| 模式 | 含义 |
| :-- | :-- |
| ^ | 脱字符表示行或字符串的开头。 |
| $ | 美元符号表示行或字符串的结尾。 |
| . | 点号匹配任何单个字符。 |
| (a \| b) | 使用“管道”字符作为逻辑“或”，模式 (a \| b) 匹配 a 或 b。 |
| (... ) | 括号将部分分组为子匹配。 |
| [abc] | 在括号对内部列出值，匹配给定列表或范围内的任何值。模式 [abc] 匹配单个字母 a、b 或 c，而模式 [a-z] 匹配小写字母 a 到 z 中的任何一个。 |
| [^abc] | 在范围开头使用脱字符，匹配范围中未列出的任何值。模式 [^abc] 匹配除 a、b 或 c 以外的任何字符；模式 [^a-z] 匹配除小写字母 a 到 z 以外的所有内容。 |

| 模式 | 含义 |
| :--- | :--- |
| a? | 问号使前一个字符恰好匹配零次或一次。 |
| a* | 星号指示 Apache 匹配前一个字符零次或多次——无限制。 |
| a+ | 使用加号使前一个字符匹配一次或多次——无限制。 |
| a(n) | 花括号内的单个数值使前一个字符恰好匹配指定的次数。 |
| a(n,) | 后跟逗号的单个数值使前一个字符至少匹配 n 次，但可能更多。 |
| a(n,m) | 花括号中的两个数值指定至少 n 次匹配，但不超过 m 次匹配。 |
| !(pattern) | 逻辑“非”由模式前的感叹号表示。用于在 URL 不匹配给定模式时应用规则。 |
| \char | 反斜杠作为转义字符，使你可以匹配通常是正则表达式令牌的字符，如 `^`、`.`、`*`、`{`、`\`、`(`、`)` 等。 |
| \d | 匹配任何十进制数字。 |
| \w | 匹配任何“单词”字符——通常是任何字母、数字或下划线字符。 |

例如，你最近可能用新的、更最新版本的网站部分替换了旧的部分，且使用了不同的 URL。为了自动将旧结构中的任何 URL 重定向到新位置的索引，你可能会使用类似以下内容：

```
RewriteEngine On
RewriteBase /

# 将旧目录的请求重写到新索引
RewriteRule ^olddirectory/ newdirectory/index.php [R,NC,L]
```

此规则告诉 Apache 对指向 olddirectory/ 文件夹中任何文件的请求，以 newdirectory 文件夹中的 index.php 作为响应。末尾的标志指定重定向到新 URL，匹配时忽略大小写，并停止处理可能匹配请求 URL 的其他任何规则——这些标志将在本章后续部分涵盖。

使用 mod_rewrite 的更常见用途之一是提供对搜索引擎友好——以及对人工输入友好——的 URL，同时仍然使用标准的带有 HTTP GET 参数附加在请求中的 PHP 文件。为了帮助说明这种场景，请首先创建以下 PHP 文件：

```php
<?php
$category = '';
$item = '';
if (isset($_GET['cat']))
{
    $category = $_GET['cat'];
}
if (isset($_GET['item']))
{
    $item = $_GET['item'];
}
echo "Category: " . $category . "<br />\n" .
       "$item: " . $item . "<br />\n";
?>
```

将此文件保存为 *catalog.php*，位于你网站的根文件夹中。

通常，如果你想调出此文件并让它识别给定的类别或项目值，你必须在查询字符串中提供值，如下所示：

```
http://www.domain.com/catalog.php?cat=categoryValue&item=itemValue
```

不幸的是，一些搜索引擎不会编录具有上述 URL 的动态页面。此外，指定每个变量的额外语法对于手动输入 URL 的人来说可能是一种负担。为了改善这种情况，你可以使用 mod_rewrite。在与 *catalog.php* 文件相同的目录中的 .htaccess 文件中（或在需要时在服务器的 httpd.conf 文件中）添加以下指令：

```
RewriteEngine On
# 将 /category/item/ 重写到 catalog.php
RewriteRule ^(\w+)/(\w+)//?$ catalog.php?cat=$1&item=$2
```

> *为了在 per-directory 配置文件 (.htaccess) 中使用 mod_rewrite 指令，必须在 httpd.conf 中为这些目录启用 Options FollowSymLinks 或 Option SymLinksIfOwnerMatch 指令。*

现在，由于 mod_rewrite 的魔力，你可以使用 URL 中的目录而不是查询字符串来访问类别和项目记录：

```
http://www.domain.com/categoryValue/itemValue/
```

请注意，前述 URL 中引用的相应目录实际上并不存在—— mod_rewrite 截获请求并将其转换为附加查询字符串的 PHP 请求，然后该请求通过 PHP 引擎解析。另一件需要记住的事情：如果前述目录确实存在并且此处显示的 RewriteRule 处于活动状态，Apache 仍将完全忽略实际路径并按照计划进行 URL 重写。

查看 mod_rewrite 配置中的几行，你从一个简单的声明开始：

```
RewriteEngine On
```

为了使用 mod_rewrite，你必须告知 Apache 你希望在给定的配置区域中启用该模块——例如 .htaccess 文件，或 httpd.conf 中的 `<Directory>` 部分。*RewriteEngine* 的值可以是 *On* 或 *Off*。

下一关键行只是一个用于匹配传入 URL 的正则表达式，以及用于替代它的新 URL：

```
# 将 /category/item/ 重写到 catalog.php
RewriteRule ^(\w+)/(\w+)//?$ catalog.php?cat=$1&item=$2
```




# 第 6 章

该模式通过 `\w` 模式匹配每一级目录中仅包含有效“单词”字符的两级目录请求。然后，它将这两个目录的值用作 PHP 脚本中的类别和项目编号。与 PHP 的 PCRE 语法类似，你可以使用以 $ 开头的反向引用来引用原始模式中的子匹配。反向引用是一种简单的方法，可以直接将前一个模式中的子匹配包含在替换字符串中。再次查看该规则：

```apache
# Rewrite /category/item/ to catalog.php
RewriteRule    ^(\w+)/\w+/?$    catalog.php?cat=$1&item=$2
```

在针对 URL 匹配的正则表达式中，恰好定义了两个子匹配：即表示目录的两个“单词”字符分组。在替换字符串中，使用反向引用 $1 和 $2 来自动包含第一个和第二个子匹配的值，分别对应。反向引用简单地从 1 开始计数，对应第一个子匹配。

使用简单的 RewriteRule 还能做什么其他技巧？你实际上可以将它用作 PHP 脚本的初步类型检查层。在某些情况下，你可能需要从查询字符串变量中获取一个数字，例如页码或项目编号。如果你希望绝对确定你使用的是数字，而不是某些潜在的恶意内容——如 SQL 注入攻击——你有两种选择。

第一种也是最常用的方法是在 PHP 脚本中添加额外代码，以实际检查 $_GET 参数是否确实包含一个数字。例如，你可能有这样的 URL：

```text
http://www.domain.com/article.php?page=2
```

像这样的 URL 通常出现在分页内容中，通常位于页面导航链接中。在加载文章指定页面的代码某处，你可能会看到以下内容：

```php
<?php
if (isset($_GET['page']) and is_numeric($_GET['page']))
{
  $page = $_GET['page'];
}
else
{
  $page = 1;
}
// And so on....
?>
```

上面的代码首先检查特定 $_GET 值（在此例中为 'page'）的存在，然后检查传递的值是否确实是一个数字——如果不是，则分配默认值 1。

这种类型检查是个好主意，有助于保护你的 PHP 脚本免受那些试图破坏你网站的“脚本小子”的攻击。不幸的是，这变得有些繁琐，因为你的 PHP 脚本需要检查值是否已设置，以及它是否确实是一个数字。

使用 mod_rewrite，你可以从 PHP 代码中消除类型检查——你所要做的只是确保模式仅匹配数字值：

```apache
RewriteEngine On
# Ensure only numeric values for the page
RewriteRule ^article/([0-9]+)/?    article.php?page=$1
RewriteRule ^article/[^0-9]/?      article.php?page=1
```

第一个 RewriteRule 检查形式为 article/page/ 的任何有效 URL，并将给定的请求转换为对 PHP 脚本的调用。第二个 RewriteRule 旨在捕获所有调用文章但页码值无效的格式错误的 URL。任何此类请求都会自动分配为文章的第一页。

在上一组 RewriteRules 中有两点需要注意。首先，两个规则按顺序处理；处理不会在第一个规则处停止，而是继续处理所有给定的规则。其次，重定向到 article.php 脚本是内部处理的——根本没有向客户端发送任何 HTTP 重定向/移动状态码。为了改变这些默认行为，你可以在每个规则的末尾使用一组标志。

##### RewriteRule 标志

为了控制 mod_rewrite 处理和每个 RewriteRule 的方式，你可以添加一组 15 种不同的标志，跟在每个规则之后。标志包含在方括号内，并提供多个标志，并用逗号分隔的列表提供——所有标志都在一组公共的方括号内。例如：

```apache
# Rewrite /category/item/ to catalog.php
RewriteRule  ^(\w+)/(\w+)/?   catalog.php?cat=$1&item=$2  [NC,R,L]
```

###### nocase|NC

类似于 PHP PCRE 语法中的 i 标志，nocase 标志使模式不区分大小写。例如，以下两个模式是相同的：

```apache
RewriteRule  ^([a-zA-Z]+)/?    catalog.php?cat=$1
RewriteRule  ^([a-zA-Z]]/?     catalog.php?cat=$1  [NC]
```

###### redirect|R|code

通常，mod_rewrite 在重写 URL 时使用内部 Apache 重定向，这种重定向对用户是不可见的。如果你想要进行正式的重定向，并附带 HTTP 状态码，可以使用 redirect 或 R 标志。默认情况下，redirect 标志发送 HTTP 302 临时移动代码，如下面的规则所示：

```apache
RewriteRule ^article/(\d+)/?   article.php?page=$1  [R]
```

如果你希望将状态代码更改为 HTTP 301 永久移动，或者 300 到 400 之间的任何其他状态代码，只需将代码添加在 redirect 标志的末尾：

```apache
RewriteRule ^article/(\d+)/?   article.php?page=$1  [R=301]
```

###### forbidden|F

类似于 redirect 标志，使用 forbidden 标志会立即向客户端发送 HTTP 403 禁止访问响应。当同一规则同时存在 redirect 标志和 forbidden 标志时，forbidden 标志将具有优先级（重定向将被忽略，发送 403）。

###### gone|G

另一种 HTTP 状态码控制标志，*gone*，发送 HTTP 410 已删除响应，通知客户端该页面不再存在。当结合使用时，*gone* 标志优先于 *redirect* 标志，但不优先于 *forbidden* 标志。

###### last|L

为了在找到成功匹配后停止处理 RewriteRules，你可以使用 *last* 标志。在之前处理文章页码的示例中，即使第一个规则成功匹配，规则处理仍会继续到第二个规则（但不会找到匹配项）。要在第一个规则匹配后停止处理，你可以简单地使用 *last* 标志：

```apache
RewriteEngine On
# Ensure only numeric values for the page
RewriteRule ^article/([0-9]+)/?  article.php?page=$1 [L]
RewriteRule ^article/[^0-9]/?  article.php?page=1  [L]
```

###### next|N

*next* 标志会在规则列表的开头重新启动重写过程。当规则被重新处理时，匹配的 URL 不是来自客户端的原始请求，而是使用 *next* 标志时内部重写后的 URL。例如：

```apache
RewriteRule  ^article/(\d+)/?  article.php?page=$1
RewriteRule  ^catalog/(\w+)/?  catalog.php?cat=$1  [N]
RewriteRule  ^catalog/(\w+)/(\w+)/? catalog.php?cat=$1&item=$2
```

在这个例子中，如果调用的 URL 匹配第二个规则，例如 http://localhost/catalog/stuff/，重写过程将在该点停止处理，并自动使用新替换的 URL catalog.php?cat=stuff 从规则集的开头重新启动。替换后的 URL 本身会通过整个规则集进行过滤。

使用 *next* 标志时应小心，因为可能会出现无限循环。

###### chain|C

如果你希望将一组规则视为一个相关的单元，类似于 PHP 中的 *try* ... *catch* 语法，你可以使用 *chain* 标志。使用 *chain* 标志时，如果规则匹配，处理按预期继续并忽略 *chain* 标志。如果规则不匹配且存在 *chain* 标志，则所有链接在一起的后续规则将作为一个整体被跳过。例如，如果第一个不匹配，以下规则集将跳过到最后一个规则：

```apache
RewriteRule  ^article/(\d+)/?  article.php?page=$1 [C]
RewriteRule  ^catalog/(\w+)/?  catalog.php?cat=$1  [C]
RewriteRule  ^catalog/(\w+)/(\w+)/?  catalog.php?cat=$1&item=$2

# Skip to this rule if any of the above don't match
RewriteRule  ^article/(\d+)/?  error.php
```

###### skip|$=number

当当前规则匹配时，此标志允许你跳过接下来的若干条规则。虽然 `skip` 标志的行为与 `chain` 标志相似，但它们的行为完全相反——`skip` 在成功匹配时跳转；`chain` 在匹配失败时跳转。

###### type|T=mime-type

如果你想覆盖文档发送的 MIME 类型，可以使用 `type` 标志。例如，如果你有一批 `.xhtml` 文件，希望使用正确的 XHTML MIME 类型而不是 text/HTML 来提供它们，可以使用以下代码：

```apache
RewriteRule  ^.+.xhtml$  -  [T=application/xhtml+xml]
```

###### cookie|CO=name:value:domain[:lifetime[:path]]

如你可能推断的那样，`cookie` 标志会在客户端浏览器上设置一个 cookie。三个必需字段——`name`、`value` 和 `domain`——分别指定 cookie 的名称、cookie 的值以及设置 cookie 的 `domain`。可选的 `lifetime` 参数代表 cookie 的有效期，以分钟为单位。`path` 参数设置 cookie 的路径。

例如，如果你想设置一个名为 `prevvisit` 的 cookie 来表示用户之前访问过主页（因此不应该被启动画面打扰），你可以使用此代码：

```apache
RewriteRule  ^index\.php$  -  [CO=prevvisit:true:domain.com]
```

###### env|E=var:value

`env` 标志允许你将环境变量 `var` 设置为提供的值。该值也可以包含正则表达式反向引用（$1 和 $n）以实现更复杂的变量控制。可以在一组标志中设置多个环境变量——只需像其他标志列表一样用逗号分隔即可。

###### qsappend|QSA

在大多数使用 `mod_rewrite` 的情况下，当执行重写时，提供给原始 URL 的任何查询字符串都会被丢弃。如果你希望保留这些信息而不是丢弃它们，可以使用 `qsappend` 标志。使用此标志时，重写引擎只是获取原始查询字符串并将其附加到重写中提供的任何新查询字符串。例如：

```apache
RewriteRule  ^index\.php$  index.php?foo=bar  [QSA]
```

如果使用 URL `index.php?moo=cow`，该规则会将 `index.php` 文件更改为 `index.php?foo=bar&moo=cow`。

如果原始 URL 中的查询字符串参数与 `RewriteRule` 中的参数名称相同，则原始值优先。




## 第 6 章

### noescape\NE

当 *mod_rewrite* 执行转换时，它会采取多种措施确保重写 URL 中的特殊字符在执行内部或外部重定向之前被转义。例如：

```apache
RewriteRule ^somedir/? index.php?page=foo\%3b [R]
```

基于此规则，Apache 会按请求将 *somedir/* 目录重定向，而 *page* 的 `$_GET` 值将是 *foo\%3b* 的“安全”转义值——*mod_rewrite* 对 `\%3b` 值进行了转义，而不是将其替换为其分号替代字符。若要告诉 *mod_rewrite* 避免任何自动转义，请启用 **noescape** 标志：

```apache
RewriteRule ^somedir/? index.php?page=foo\%3b [R,NE]
```

基于此规则，*page* 查询字符串参数的新值将为 *foo*。

### passthrough\PT

当你希望将 *mod_rewrite* 与其他提供类似 URL 处理功能的 Apache 模块（如 *mod_alias*）结合使用时，请使用 **passthrough** 标志。例如，如果你想将 */foo/* 重写为指向 */bar/*，然后使用 *mod_alias* 将 */bar/* 转换为 */baz/*，你可能会尝试以下设置：

```apache
RewriteRule ^/foo /bar
Alias /bar /baz
```

不幸的是，由于 Apache 内部处理 URL 的方式，上述写法无法正常工作。要使其生效，请添加 **passthrough** 标志：

```apache
RewriteRule ^/foo /bar [PT]
Alias /bar /baz
```

一般经验法则是：如果你使用多个 URL 转换模块来处理文件，请使用 **passthrough**。

### nosubreq\NS

使用 **nosubreq** 标志可以强制重写引擎在请求实际上是内部子请求时跳过该规则。在同时使用 PHP 和 Apache 时，很少需要此标志的情况。然而，在某些 CGI 脚本实例中，此标志会发挥作用。更多信息，请参阅 Apache 手册中关于 *RewriteRule* 的章节：`http://httpd.apache.org/docs/2.0/mod/mod_rewrite.html#rewriterule`。

### proxy\P

**proxy** 标志告诉重写引擎立即停止处理该规则集，并强制请求通过 Apache 代理模块 *mod_proxy* 处理。

鉴于 *RewriteRule* 受到了如此多的关注，你可能会认为它是 *mod_rewrite* 的主要动力。实际上，其最佳角色是与 *RewriteCond* 组成的动态双人组的一部分。

##### RewriteCond

*RewriteCond* 指令的行为很像 PHP 的 `if()` 语句：它将字符串与模式或条件进行测试。如果输入匹配模式或字符串，则紧跟在 *RewriteCond* 指令后面的 *RewriteRule* 将被处理。*RewriteCond* 的一般格式如下：

```apache
RewriteCond TestString CondPattern
```

*TestString* 是你正在评估的字符串，而 *CondPattern* 是要检查的正则表达式或比较值。

##### RewriteCond 用法

*RewriteCond* 最常见的用法是将输入字符串与正则表达式匹配，类似于 *RewriteRule*。但是，当你使用 *RewriteCond* 时，你可以访问大量的服务器变量，因此你的输入字符串可以比简单的文件名匹配更复杂。下表列出了可用于 *RewriteCond* 的服务器变量。

以下是 HTTP 头部变量：

| 变量 | 描述 |
| :--- | :--- |
| HTTP_USER_AGENT | 列出浏览器识别信息的字符串，例如：Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322) |
| HTTP_REFERER | 由用户的浏览器报告的上一个访问过的页面 |
| HTTP_COOKIE | 请求中包含的任何 cookie 字符串 |
| HTTP_FORWARDED | 如果请求由代理服务器处理，则包含任何转发信息 |
| HTTP_HOST | 请求中引用的主机名 |
| HTTP_PROXY_CONNECTION | HTTP Proxy-Connection 头部内容 |
| HTTP_ACCEPT | 返回 Accept 头部值；指示浏览器可以处理的内容类型，以及哪些类型具有优先权 |

以下是请求变量：

| 变量 | 描述 |
| :--- | :--- |
| REMOTE_ADDR | 请求该文件的用户的 IP 地址。 |
| REMOTE_HOST | 请求该文件的用户的主机名。 |
| REMOTE_USER | 请求该文件的人员的用户名，由浏览器报告。 |
| REMOTE_IDENT | 用于标识目的的变量。可能包含用户名。 |
| REQUEST_METHOD | 请求中使用的方法，如 GET 或 POST。 |

以下是其他请求变量：

| 变量 | 描述 |
| :--- | :--- |
| SCRIPT_FILENAME | 请求文件的完整本地路径。 |
| PATH_INFO | 添加到 URL 末尾的任何额外路径信息。 |
| QUERY_STRING | 请求的任何查询字符串或 GET 参数，通常是带有参数的 GET 请求中问号之后的任何内容。 |
| AUTH_TYPE | 用于验证用户使用的认证类型。 |

以下是服务器变量：

| 变量 | 描述 |
| :--- | :--- |
| DOCUMENT_ROOT | 网站的根目录，如 `DocumentRoot` 指令中指定 |
| SERVER_ADMIN | 服务器管理员的电子邮件地址，如使用 `ServerAdmin` 指令指定 |
| SERVER_ADDR | 服务器的主机名或 IP 地址 |
| SERVER_PORT | 请求中指定的服务器端口号 |
| SERVER_PROTOCOL | 请求协议（如 `HTTP/1.1`）的名称和版本 |
| SERVER_SOFTWARE | 服务器软件（Apache）的名称 |

以下是时间变量：

| 变量 | 描述 |
| :--- | :--- |
| TIME_YEAR | 请求的当前年份 |
| TIME_MON | 请求的当前月份 |
| TIME_DAY | 请求的当前日期 |
| TIME_HOUR | 请求的当前小时 |
| TIME_MIN | 请求的当前分钟 |
| TIME_SEC | 请求的当前秒 |
| TIME_WDAY | 当前星期几 |
| TIME | 当前时间 |

以下是各种特殊变量：

| 变量 | 描述 |
| :--- | :--- |
| API_VERSION | Apache 模块 API 的版本（与 Apache 版本号不同，但密切相关）；主要用于模块开发（内部） |
| THE_REQUEST | 完整的 HTTP 文件请求字符串，包括方法、请求的文件以及使用的 HTTP 版本 |
| REQUEST_URI | HTTP 请求中请求的资源 |
| REQUEST_FILENAME | 匹配 HTTP 请求项的完整本地文件系统路径 |
| IS_SUBREQ | 正在处理的请求是否是内部子请求；如果请求是子请求，值为“true”，否则为“false” |
| HTTPS | 值为“on”表示正在使用 SSL/TLS，“off”表示未使用 |

要使用该长列表中的任何变量，请将变量名放在花括号中，并以百分号作为前缀，如下所示：

```apache
%{SCRIPT_FILENAME}
```

为了查看 *RewriteCond* 的作用，首先重写 *RewriteRule* 以利用 *RewriteCond*。旧规则如下：

```apache
# Rewrite /category/ to catalog.php
RewriteRule ^(/\w+)?/?$ catalog.php?cat=$1&item=$2
```

要使用 *RewriteCond* 结合 *RewriteRule* 实现相同的目标，请使用以下代码：

```apache
# Rewrite /category/item/ to catalog.php
RewriteCond %{SCRIPT_FILENAME} ^(/\w+)?/(\w+)?/?$
RewriteRule .* catalog.php?cat=$1&item=$2
```

注意服务器变量 `SCRIPT_FILENAME` 是如何用作测试输入字符串的。将这些服务器变量与 *RewriteCond* 结合 *RewriteRule* 使用，你可以想出一些有趣的组合。以下代码检查用户的浏览器是否可以接受 XHTML MIME 类型，如果可以，则更改为 .html 文件发送的 MIME 类型头部：

```apache
RewriteCond %{HTTP_ACCEPT} application/xhtml+xml
RewriteRule .*.html$ - [T=application/xhtml+xml]
```

*RewriteCond* 的另一个有用功能是能够链接多行内容。当连续列出多个 *RewriteCond* 语句时，它们都像编程中的 AND（与）一样被处理——末尾的 *RewriteRule* 只有在所有 *RewriteCond* 匹配都返回 true 时才会处理。上一组规则可以使用多个 *RewriteCond* 语句重写，如下所示：

```apache
RewriteCond %{HTTP_ACCEPT} application/xhtml+xml
RewriteCond %{SCRIPT_FILENAME} \.html$
RewriteRule .*$ - [T=application/xhtml+xml]
```

除了标准的字符串与正则表达式比较外，你实际上可以使用 *RewriteCond* 进行简单的比较和系统检查条件。要将你的输入字符串与另一个简单字符串进行比较，可以使用以下作为你的条件模式：

```apache
<CondPattern
>CondPattern
=CondPattern
```




## 第 6 章

每个指令分别检查输入字符串是否小于、大于或等于 `CondPattern`。例如，如果你想让网站在给定年份后禁止访问某个区域，可以使用以下代码：

```
RewriteCond %{TIME_YEAR} >2005
RewriteRule .* - [F]
```

除了这些简单的比较运算符外，你还可以使用另外六种条件检查来评估文件和目录的状态：

| 比较运算符 | 含义 |
|---|---|
| -d (is directory) | 测试是否存在匹配测试字符串的目录 |
| -f (is regular file) | 测试是否存在匹配测试字符串的常规文件 |
| -s (is regular file with size) | 测试是否存在匹配测试字符串且大小大于 0 字节的常规文件 |
| -l (is symbolic link) | 测试是否存在匹配测试字符串的符号链接 |
| -f (is existing file via subrequest) | 在考虑服务器所有访问控制后，测试常规文件是否可访问；使用内部子请求来执行检查（会影响性能） |
| -U (is existing URL via subrequest) | 在考虑服务器所有访问控制后，测试 URL 是否可访问；使用内部子请求来执行检查（会影响性能） |

例如，要检查图像是否存在且实际包含一些数据，可以使用以下代码：

```
RewriteCond %{REQUEST_FILENAME} \.jpg$
RewriteCond %{REQUEST_FILENAME} !-s
RewriteRule .* - [G]
```

第一个条件检查是否调用了 .jpg 文件，第二个条件实际检查文件是否不存在或大小为 0 字节。注意条件模式 `!-s` 前使用感叹号。`RewriteCond` 中的任何条件模式都可以在前面加感叹号，从而否定该条件——这与 PHP 条件中感叹号的作用相同。

##### RewriteCond 标志

为了更好地控制 `RewriteCond`，提供了一些与 `RewriteRule` 标志类似的标志。

###### nocase|NC

与在 `RewriteRule` 中使用的同名标志一样，`nocase` 指定要评估的正则表达式是不区分大小写的。

###### or next| OR

多个 RewriteCond 指令的默认链式方法是使用逻辑与（AND）。如果使用 or next 标志，则两个连接的 RewriteCond 使用逻辑或（OR）进行比较。

虽然 RewriteRule 和 RewriteCond 指令提供了 mod_rewrite 的大部分功能，但还有一些其他关键指令可以帮助你控制重写并解决问题。

### Apache 技巧

#### RewriteBase

在大多数情况下，你的网站 URL 不会与你的物理文件系统布局匹配。你的网站根目录几乎从不位于本地文件系统的根目录（/）处。在 Apache 服务器的正常运行中，这通常不是问题；但在使用 RewriteRule 时，这可能变得非常棘手。RewriteBase 允许你为一系列 URL 重写指定基础或前缀路径。

为了完全理解 RewriteBase 的理由，请查看以下用于重写一组简单文件的示例规则集：

```
RewriteEngine On

RewriteRule ^foo\.html$ bar.html [R]
```

假设你的 Web 根目录由本地文件系统的 /www 文件夹提供（即你的 DocumentRoot 设置为 /www）。如果你尝试在目录访问文件 (.htaccess) 中使用前面的规则，实际上会导致请求被错误地重写——而不是返回你期望的 http://www.domain.com/bar.html 文件，你会得到 http://www.domain.com/www/ bar.html。为什么会这样？以下是 Apache 内部发生情况的简化版本：

请求：/www/foo.html（本地物理路径）

重写过程：
/www/foo.html -> foo.html（移除目录前缀）
foo.html -> bar.html（应用 RewriteRule）
bar.html -> /www/bar.html（重新应用目录前缀）
/www/bar.html -> http://www.domain.com/www/bar.html
（将域名前缀应用于 URL，发送到浏览器）

为了解决这个问题，你只需在规则集中添加一个 RewriteBase 语句：

```
RewriteEngine On
RewriteBase /

RewriteRule ^foo\.html$ bar.html [R]
```

#### RewriteLog

为了亲眼目睹 mod_rewrite 实际发生的内部情况，请尝试 RewriteLog 指令。你可以使用 RewriteLog 来指定一个日志文件，内部重写处理的运行记录将被发送到该文件中。

要在其他默认 Apache 日志文件旁边启用重写日志，使用以下代码：

```
RewriteLog "logs/rewrite_log"
```

在指定重写日志的路径时，你可以使用绝对路径和相对路径。如果使用相对路径，它将以 httpd.conf 中 _ServerRoot_ 设置为基准。

请注意，_RewriteLog_ 指令是按服务器应用的，因此必须放在 httpd.conf 中的服务器配置或虚拟主机容器内——不允许在 <Directory> 部分或 .htaccess 文件中使用。

#### RewriteLogLevel

要控制重写日志记录的详细程度，可以使用 _RewriteLogLevel_ 指令。给定 0 到 9 之间的数字，其中 9 表示最详细，你可以控制记录多少内部处理。设置为 0 将完全禁用日志记录，而大于 2 的设置仅用于调试——在较高设置下可能会降低 Apache 的速度。

如果你希望更深入地了解 mod_rewrite 的工作原理，请查看 Apache 在线手册中的 mod_rewrite 部分：

```
http://httpd.apache.org/docs-2.0/mod/mod_rewrite.html
```

#### URL 拼写检查

有了 mod_rewrite 的力量，对于格式错误或更改的 URL，你几乎可以处理任何情况，那拼写错误呢？当然，你可以为网站中的每个文件列出一个巨大的可能拼写错误列表，并编写大约一千条 RewriteRule，但这并不是必须的。为了解除你“简单”拼写检查的负担，Apache 附带了 mod_spelling 模块（是的，它真的只拼写了一个 't'）。使用 mod_spelling，你可以将处理 URL 拼写错误的任务移交给 Apache，它将自动尽力确定用户打算加载哪个文件。

要使用 mod_spelling，首先检查它是否已作为静态构建模块可用：

```
/path/to/httpd -l
```

如果你在列表中看不到 mod_spelling . c，请检查 Apache 模块目录中的 mod_spelling . so：

```
ls /path/to/apache/modules
```

如果你没有找到静态库或动态模块，你需要自己构建它们。与之前一样，你可以选择将该模块静态构建到 Apache 本身，或将其构建为动态模块。

要构建静态版本，请更改你的 configure 命令以包含 mod_spelling，如下所示：

```
./configure \
--enable-spelling \
# ...以及你使用的其他 configure 设置
```

如果你更喜欢使用动态模块，只需在 mod_spelling 行中添加 --enable-spelling=shared：

```
./configure \
--enable-spelling=shared \
# ...以及你使用的其他 configure 设置
```

configure 脚本运行后，使用 make 和 make install 构建和安装新的二进制文件和模块是一件简单的事。如果你选择为 mod_spelling 使用动态模块，你需要执行一个额外的步骤。要在 httpd.conf 文件中启用 mod_spelling 作为动态模块，请取消注释或添加以下行：

```
LoadModule speling_module modules/mod_spelling.so
```

完成更改后，重启 Apache。如果 Apache 错误日志中没有显示错误，则说明你已成功为服务器添加了 mod_spelling 功能。

要实际使用拼写检查，请在全局服务器配置部分、虚拟主机部分、<Directory> 部分或简单的 .htaccess 文件中添加以下指令：

```
CheckSpelling on
```

配置 mod_spelling 仅涉及 CheckSpelling 指令——值为“on”启用拼写检查，“off”禁用任何检查，这是默认行为。

要查看 mod_spelling 的实际效果，请在你选择的目录中启用 CheckSpelling，然后在该目录中创建名为 info.php 的以下脚本：

```
<?php phpinfo(); ?>
```

到现在为止，你应该能认出这是标准的 PHP 信息转储输出，但与其使用正确的 info.php URL 加载文件，不如尝试使用稍微拼错的名字，如 ingo.php。启用 mod_spelling 后，Apache 会执行快速的 HTTP 301 重定向到它对你意图的最佳猜测，而不是提供 404 Not Found 冷盘。

### 内容压缩

如果我们告诉你，只需花几分钟进行 Apache 配置，就可以大幅削减你的每月带宽使用量？你可能认为这是谎言，但事实恰恰相反——你只需要内容压缩和几个配置指令。

什么是内容压缩？当网页通过互联网下载时，默认情况下，组成页面标记、图像、样式表和其他内容的位和字节大部分是未压缩的




## 第 6 章

状态。你编写的 HTML 会像保存时一样直接发送，包括所有空白字符。内容压缩允许你透明地压缩页面标记，并通过互联网将其发送到用户的浏览器，在那里它会在渲染到屏幕之前被静默解压。另一种理解方式是将其类比为通过电子邮件发送压缩文件。你可以将一个大型的多媒体文件作为普通附件直接发送到电子邮件中，但通常你会先将文件压缩为 zip 或 tar.gz 归档再发送，以帮助缩短下载消息和附件所需的时间。

在 Apache 中使用内容压缩非常简单。你只需要 `mod_deflate`，它包含在 Apache 源代码中，在构建 Apache 时很容易作为模块编译进来。

#### 使用 mod_deflate

与之前讨论的模块一样，你需要做的第一件事是检查该模块是否可用，它是 Apache 的静态部分，还是作为一个动态模块：

```
/path/to/httpd -l
ls /path/to/apache/modules/
# ...以及你可能使用的任何其他 configure 设置
```

如果在第一个命令的输出中看到 `mod_deflate.c`，或在第二个命令的输出中看到 `mod_deflate.so`，说明你已经可以访问 `mod_deflate`，并且可以跳过下一步中重建 Apache 的步骤。

如果你在两个命令的结果中都没有看到 `mod_deflate`，你需要将其静态构建到 Apache 二进制文件中，或者作为动态模块添加。要从源代码静态地将 `mod_deflate` 包含在 Apache 中，你只需在运行 `configure` 时添加以下内容：

```
./configure \
    --enable-deflate
```

如果你希望使用动态可加载模块，只需在启用 `mod_deflate` 的行末尾添加 `shared`：

```
./configure \
    --enable-deflate=shared \
    # ...以及你可能使用的任何其他 configure 设置
```

显然，如果你计划在运行 `configure` 时包含其他指令，也需要添加它们。配置完源代码后，执行常规的 `make` 和（作为 root）`make install`。

如果你将 `mod_deflate` 构建为动态模块，你必须使用 `LoadModule` 在 `httpd.conf` 中启用该模块：

```
LoadModule deflate_module modules/mod_deflate.so
```

然后重启 Apache 以使更改生效。

构建并启用 `mod_deflate` 后，告诉 Apache 使用 `mod_deflate` 以及要压缩的文件类型就变得很简单了。为此，你需要编辑你的 `httpd.conf` 文件，或创建或修改你想使用压缩的目录中的 `.htaccess` 文件——如果可用，前者是推荐的方法。

### Apache 技巧

要在 Apache 中全局启用压缩，请将以下内容添加到你的 httpd.conf 中：

```
AddOutputFilterByType DEFLATE text/*
AddOutputFilterByType DEFLATE application/ms*
AddOutputFilterByType DEFLATE application/vnd*
AddOutputFilterByType DEFLATE application/postscript
```

然后你只需重启 Apache，就可以让内容压缩运行起来了。

所有这些配置指令具体是什么意思呢？其实很简单——在 Apache 2.x 中，`AddOutputFilterByType` 指令的作用正如字面意思所示：它告诉 Apache 在将响应发送回最终用户的浏览器之前，将输出通过给定的过滤器（在本例中为 `mod_deflate`）进行处理。前面的示例代码告诉 Apache 在任何基于文本的文件（`text/*`）、任何 Microsoft 文档，如 Word 或 Excel 文件（`application/ms*` 和 `application/vnd*`），以及任何 PostScript 文件，如 Adobe Illustrator 或 EPS 绘图（`application/postscript`）上使用 `DEFLATE` 过滤器 `mod_deflate`。任何你喜欢的文档类型都可以通过使用文档 MIME 类型和通配符的组合，类似于示例中的方式，简单地添加到 `mod_deflate` 的过滤列表中。

如果你只想压缩纯文本和 HTML 文件，请使用以下内容：

```
AddOutputFilterByType DEFLATE text/plain
AddOutputFilterByType DEFLATE text/html
```

如果你想压缩 Apache 提供的每一个文件怎么办？使用另一个 Apache 指令 `SetOutputFilter`，你可以告诉 Apache 将每个文件都通过 `mod_deflate` 发送：

```
SetOutputFilter DEFLATE
```

然而，在大多数服务器配置中，这不是一个很好的主意。实际上，有一些文件类型从压缩中获益不大，还有一些在压缩后会变得对最终用户来说无法读取。在大多数情况下，没有理由压缩图像格式，因为最常用的网络格式已经具有某种内置的压缩形式。此外，PDF 也是压缩过的，绝对不应该通过 `mod_deflate` 进行过滤，因为它们在 Acrobat Reader 中将变得不可读。

> 需要注意的是，Netscape Navigator 4.x 版本无法可靠地解压任何除了 text/html 之外的文件类型，且特定版本的 Netscape Navigator 4.x 无法解压任何文件类型。

为了进一步调整你选择的文件类型的压缩设置，`mod_deflate` 提供了以下部分中描述的配置指令。

##### DeflateCompressionLevel

`DeflateCompressionLevel` 设置用于缩小文件的压缩级别，范围为 1 到 9。压缩级别 1 产生最快的压缩，但压缩程度最低（文件较大），而压缩级别 9 使用最慢的压缩，但生成的文件大小小得多。在决定使用哪个级别时，你必须确定对你来说什么是更重要的——节省处理器周期还是节省下载时间。默认的压缩级别 6 通常是两者之间的良好折衷。

##### DeflateFilterNote

如果你希望日志文件显示访问日志中每个请求文件的压缩比，请使用 DeflateFilterNote。*DeflateFilterNote* 接受日志标记的名称作为其值——即 *Apache* 中指定的命名标记。然后可以使用 *DeflateFilterNote* 来利用 *Apache* 的 *LogFormat* 指令自定义日志输出。

##### DeflateWindowSize

这指定了 zlib 压缩窗口大小，用于压缩文件。值范围从 1 到 15，其中 1 产生较少的压缩，15 产生最大的压缩。DeflateWindowSize 的默认值是 15。

##### mod_deflate 工作效果如何？

为了查看 mod_deflate 节省字节的能力，本示例使用 Apache 提供一个大小适中的 HTML 页面，分别开启和关闭 mod_deflate 进行测试。在这个示例中，使用的是 Wrox P2P 社区论坛（位于 http://p2p.wrox.com）的主页。该页面的原始 HTML 标记——仅 HTML 部分——重达 47172 字节。请查看下表，了解它在三种不同压缩级别下通过 mod_deflate 后的表现：

| 压缩级别 | 传输字节数 | 原始大小百分比 | 近似下载时间 (56k) |
| :---------------- | :---------------- | :------------ | :-------------------------- |
| 原始       | 47172 字节      | 100% 原始大小 | 11.7 秒                    |
| 默认 (6)     | 7621 字节      | 16.2% 原始大小 | 3.8 秒                    |
| 级别 1       | 9050 字节      | 19.2% 原始大小 | 4.1 秒                    |
| 级别 9       | 7581 字节      | 16.1% 原始大小 | 3.8 秒                    |

如你所见，使用 mod_deflate 与提供原始的未压缩 HTML 相比显然具有优势——通过连接发送的文件大小减少了近 84%。还请注意，使用最大压缩级别 9 仅比默认级别 6 好一点点，因此在这种情况下，可能可以安全地坚持使用默认压缩级别 6，以节省处理器的几个周期。

许多网站混合了 HTML、媒体和相关脚本文件，因此诸如照片博客或在线购物中心等网站可能无法在每个提供的文件上都获得巨大的文件节省，但节省的每一字节在月底都会累积成巨大的带宽减少。以文字为主的网站，如博客和新闻门户，将真正受益于内容压缩，因为这些站点使用的大多数带宽都是纯文本——这些文本会通过 mod_deflate 进行传输。

##### 为 PHP 脚本启用压缩

你可能在问 PHP 文件怎么办？在许多情况下，没有必要对 PHP 文件使用压缩，在某些情况下，这甚至会对输出产生不利影响。

如果你的 PHP 脚本输出实际的图像或 PDF 为例，你不会希望 Apache 仅仅因为文件扩展名碰巧是 .php 就盲目地压缩输出。




在某些情况下，可能已经为所有 PHP 脚本启用了输出缓冲和压缩。要确定这一点，请检查配置变量 `output_handler` 的值，或在 `php.ini` 中查看 `output_handler` 和 `zlib.output_compression` 的值。

要在 PHP 中启用输出压缩，请执行以下操作：

1. 如有需要，请在您的机器上安装 zlib 库。
2. 根据需要配置 PHP 源代码，确保包含 `--with-zlib`，然后正常进行`编译/安装`。
3. 修改您的 `php.ini` 使其包含以下行：
   ```ini
   output_buffering = Off
   output_handler =
   zlib.output_compression = On
   ```
4. 重启 Apache 以使新更改生效。

### 在 Apache 中使用 MySQL

到现在为止，您已经使用 Apache 和基本身份验证创建了一个或两个安全区域，对于大多数情况而言，这可能已经足够了。然而，您可能会发现，虽然使用 Apache 进行基本身份验证很简单，但在控制和定制的程度上略显局限。对于许多此类情况，实际上可以将 Apache 基本身份验证与通过 MySQL 的关系数据库的强大功能相结合。为了这一目的，存在 `mod_auth_mysql` Apache 模块。

与标准的 Apache 基本身份验证类似，`mod_auth_mysql` 可以按目录控制访问，并可以在 `.htaccess` 文件和 `httpd.conf` 中的 `<Directory>` 部分内进行配置。与标准的 Apache 基本身份验证不同的是，所有用户凭据都存储在数据库中，而不是平面文件中。

#### 设置数据库

安装和配置 `mod_auth_mysql` 涉及几个步骤，其中第一步是创建必要的数据库结构以存储用户数据。首先加载您喜欢的 MySQL 客户端，并创建数据库。例如：

```sql
CREATE DATABASE apacheauth;
```

接下来，创建一个 Apache 用于访问凭据的用户：

```sql
GRANT SELECT ON apacheauth.* TO apache@localhost IDENTIFIED BY 'apachepass';
```

现在数据库用户已经创建，是时候添加一个用于保存登录信息的表了。先从一个仅保存用户名和密码的简单表开始：

```sql
USE apacheauth;
CREATE TABLE user_info (
   user_name varchar(50) NOT NULL,
   user_password varchar(50) NOT NULL,  
   PRIMARY KEY (user_info)
);
```

您可以随意命名表和列。在上面的示例中，使用 `user_info` 作为表名，并使用 `user_name` 和 `user_password` 作为登录名/密码组合，因为这些是 mod_auth_mysql 识别的默认名称。

> 在 mod_auth_mysql 的后续版本中，密码的默认列是 user_password，而不是模块文档中所述的 user_passwd。

接下来，创建一个初始测试用户账户，以便稍后在测试身份验证时使用：

```sql
INSERT INTO user_info (user_name, user_password)  
VALUES ('testuser', SHA1('testpass'));
```

> 请注意，在该语句中对密码使用了 SHA1() 函数，而不是 PASSWORD() 函数。使用 mod_auth_mysql 时，您可以使用几种密码加密方法——本例恰好使用了 SHA1。

#### 安装模块

一旦您建立了数据库表，就需要实际下载 mod_auth_mysql 的源代码，可从 http://modauthmysql.sourceforge.net 获取。截至本文撰写之时，当前版本为 2.9.0，因此您需要下载 mod_auth_mysql-2.9.0.tar.gz。

下载模块源代码后，解压该 tar 包：

```bash
tar -xzvf mod_auth_mysql-2.9.0.tar.gz
```

解压 tar 包后，切换目录到新创建的源代码文件夹：

```bash
cd mod_auth_mysql-2.9.0
```

要从下载的源代码构建模块，您实际上将直接使用 Apache 的 apxs 命令。执行以下命令，使用您系统中 apxs 二进文件的路径；此处使用默认的 Apache 位置 /usr/local/apache2/bin：

```bash
/usr/local/apache2/bin/apxs -c -lmysqlclient -lm -lz mod_auth_mysql.c
```

如果构建成功，您应该看到几行编译信息，且没有错误。相反，如果您遇到关于缺少 mysql.h 文件的错误，以及一系列与 MySQL 相关的错误，您可能需要手动指定 MySQL 库和包含文件的路径。使用 MySQL 的默认位置，您的命令可能如下所示：

```bash
/usr/local/apache2/bin/apxs -c -lmysqlclient -lm -lz \
-L /usr/local/mysql/lib/mysql \
-I /usr/local/mysql/include/mysql \
mod_auth_mysql.c
```

要安装新编译的模块，您需要以 root 身份执行以下命令。照常操作，将 `apxs` 的路径更改为指向您的 `apxs` 二进文件：

```bash
/usr/local/apache2/bin/apxs -i mod_auth_mysql.la
```

您需要执行的下一个安装任务是找到在 httpd.conf 中加载模块所需的命令。为此，打开您的 httpd.conf 文件，添加一个合适的位置来插入模块定义——通常在配置文件的末尾，或其他 `LoadModule` 语句旁边——并添加以下内容：

```apache
LoadModule mysql_auth_module modules/mod_auth_mysql.so
```

最后，重启 Apache。

#### 配置和使用

一旦您的数据库表准备就绪且模块已安装，剩下的就是告诉 Apache 需要保护什么了。与标准的 Apache 基本身份验证类似，您需要找到一些配置指令，放在 httpd.conf 的 <Directory> 部分中，或者在您可以选择保护的目录中创建一个 .htaccess 文件。

告诉 Apache 针对您的 MySQL 数据库验证用户凭据通常至少涉及以下内容：

```apache
AuthName   "<zone name>"
AuthType   Basic
AuthMySQLDB  dbname
AuthMySQLUser  userid
AuthMySQLPassword  password
AuthMySQLEnable On
require  valid-user
```

这些指令的前两行和最后一行对您来说应该已经熟悉。它们简单地定义了受保护区域的名称、身份验证类型，以及检查资源中找到的任何有效用户均允许访问。其他行告诉 Apache 在哪里查找身份验证信息。您并没有向 Apache 提供包含每个有效用户密码的文件名，而是提供了数据库信息——数据库名称、用户名和密码——以便 `Apache` 和 `mod_auth_mysql` 知道去哪里查找。第六行 `AuthMySQLEnable On` 只是告诉 Apache 实际使用 `mod_auth_mysql`——这是一种在不完全卸载或移除模块的情况下禁用 `MySQL` 身份验证的方法。

要使用您之前创建的身份验证表，您会在 <Directory> 或 .htaccess 定义中添加以下内容：

```apache
AuthName   "MySQLAuth"
AuthType   Basic
AuthMySQLDB  apacheauth
AuthMySQLUser  apache
AuthMySQLPassword  apachepass
AuthMySQLEnable On
AuthMySQLPwEncryption  sha1
require  valid-user
```

在这里，您正在告诉 Apache 和 mod_auth_mysql 针对您的 apacheauth 数据库验证用户。Apache 将使用您之前创建的 apache 账户登录数据库，并且您还在告诉 mod_auth_mysql 在将给定密码与数据库中的值匹配之前，先用 SHA1 对其进行哈希处理。

此时，您应该能够通过 Web 浏览器登录到受保护的区域，提供添加到 user_info 表中的用户凭据 (testuser:testpass)，并成功在该目录中进行身份验证。

虽然本例相当简单且精简，但 mod_auth_mysql 实际上提供了大量的配置选项，因此您可以针对几乎任何情况进行自定义身份验证。以下各节描述了一些配置选项。

##### AuthMySQLEnable On | Off

这会启用或禁用 mod_auth_mysql 身份验证，而无需直接从 Apache 中移除或卸载该模块。

##### AuthMySQLHost localhost | hostname | ipaddress

这是 MySQL 数据库服务器的主机名或 IP 地址。如果您的环境在不同机器上运行 Apache 和 MySQL，您将需要使用此设置。默认值为 `localhost`，因此同时运行 Apache 和 MySQL 的机器通常可以忽略此设置。

##### AuthMySQLPort port_number

这是 MySQL 正在监听的 TCP/IP 端口。MySQL 的默认端口值为 3306，但可以更改。此选项的默认值也是 3306，因此仅当 MySQL 正在非标准端口上监听时才需要指定此选项。

##### AuthMySQLSocket socket_file_path

这是在 UNIX 机器上访问 MySQL 所使用的 UNIX 套接字文件。默认值是 `/tmp/mysql.sock`，与 `AuthMySQLPort` 一样，仅在非标准安装中需要使用。

##### AuthMySQLUser userid

这是用于访问保存身份验证信息的 MySQL 数据库的用户 ID。大多数数据库系统不允许用户或 Apache 进程在没有正确的 userid/密码组合的情况下访问数据库，因此请将此设置与 `AuthMySQLPassword` 一起设置为具有访问身份验证表的非 root 用户账户。至少，该用户需要对身份验证表具有 `SELECT` 访问权限。

##### AuthMySQLPassword password

与 `AuthMySQLUser` 配合使用，此选项指定访问 MySQL 身份验证表的用户账户的密码。

##### AuthMySQLDB dbname

这是 MySQL 中保存身份验证表的数据库名称。如果未指定名称，将使用默认值 `test`。





# Apache 实用技巧

##### AuthMySQLUserTable *table\_name*

这是数据库中用于存储用户名和密码的表的名称。如果未指定表，则使用默认值 user\_info。

##### AuthMySQLNameField *column\_name*

这是用户表（*AuthMySQLUserTable*）中用于存储用户名的列的名称。在 MySQL 中创建表时，请确保该列具有索引或键，以确保每个值都是唯一的。列的长度由你在 MySQL 中决定。默认值是 user\_name。

##### AuthMySQLUserCondition

当 *mod\_auth\_mysql* 执行用户查找时，它会执行一个简单的 SQL SELECT 语句，包含执行匹配所需的任何条件。*AuthMySQLUserCondition* 字段允许你指定在 SQL 语句的 WHERE 子句中使用的额外参数。

##### AuthMySQLPasswordField *column\_name*

这是用户表中用于存储用户密码的列的名称。MySQL 中该列的长度至少应与加密后的密码哈希值一样长。*AuthMySQLPasswordField* 的默认值是 user\_password。

##### AuthMySQLPwEncryption *none* | *crypt* | *scrambled* | *md5* | *aes* | *sha1*

这是数据库中编码密码时使用的加密方法，具体如下：

- none：无加密/明文
- crypt：UNIX crypt() 加密
- scrambled：MySQL PASSWORD() 加密
- md5：MD5 哈希
- aes：高级加密标准 (AES) 加密
- sha1：安全哈希算法 (SHA1)

如果未指定值，则使用默认值 *crypt*。

使用 AES 密码加密时，请确保 MySQL 用户表中的密码字段是 BLOB 类型，而不是 CHAR、VARCHAR 或 BINARY 类型。除非列类型是 BLOB 的变体之一，否则 MySQL 会去除加密密码中多余的编码字符——这将导致你永远无法将给定的密码与数据库中的值进行匹配。

##### AuthMySQLSaltField

这允许你指定用于加密密码时的“盐值”的三个值之一。值为 `<>` 时，*mod\_auth\_mysql* 将使用密码本身作为盐字段。值为 `<string>` 时，使用 *string* 的值作为盐字段。任何未被小于/大于号包围的字符串都被视为数据库列的名称，该列的值将用作盐字段。

# 第 6 章

##### AuthMySQLGroupTable

当 Apache 被指示检查组而不是单个用户（*require group* 与 *require valid-user*）时，这用于设置包含组信息的表的名称。

##### AuthMySQLGroupCondition

与 *AuthMySQLUserCondition* 类似，该指令允许你指定条件语句，以包含在匹配用户组时的 *WHERE* 子句中。

##### AuthMySQLGroupField

这是数据库中包含组名称的字段名称。当使用 Apache 的 *require group* 指令匹配组时，会用到此字段。

##### AuthMySQLAuthoritative

这告诉 Apache 在 MySQL 身份验证失败时是否回退到其他模块。

### Apache 与 SSL

使用 *htpasswd* 或 *mod_auth_mysql* 通过基本身份验证保护你的 web 文件夹会增加安全性。不幸的是，寻求入侵你系统的严重黑客可以消除由基本身份验证提供的这一层额外安全性。问题在于：当你在标准服务器上使用基本身份验证时，用户名和密码实际上是从客户端未加密地传输到服务器的。精通网络的黑客可能会监控你的机器和服务器之间的传输，并嗅探出飞速经过的明文密码。

解决方案：加密客户端和服务器之间的通信。在 Apache 中，这可以通过使用 *Secure Sockets Layer* (SSL) 来实现。Apache 中的 SSL 以 *mod_ssl* 的形式出现，它是一个允许 Apache 控制的网站启用 SSL 的 Apache 模块，允许任何与 Apache 的通信使用广泛的加密方案进行加密。

要在 Apache 中启用 SSL，首先检查 SSL 是否包含在你现有的 Apache 二进制文件中，或者是否作为可加载模块：

```bash
/path/to/httpd -l
ls /path/to/apache/modules/
```

如果你没有在第一条命令的输出中看到 *mod_ssl.c*，或在 Apache 模块列表中没有看到 *mod_ssl.so*，你需要自己构建 Apache SSL 功能。要静态启用 SSL，在从源代码构建 Apache 时，在你的 *configure* 脚本中添加 *-enable-ssl*：

```bash
./configure \
  --enable-ssl \
  # ...以及你使用的其他 configure 设置
```

如果你想使用动态模块，只需在启用 SSL 的行末尾添加 #shared：

```bash
./configure \
  --enable-ssl=shared \
  # ...以及你使用的其他 configure 设置
```

然后，使用 make 和 make install 构建并安装新的 Apache 二进制文件和模块。如果你将 Apache 构建为动态模块，请在全局配置部分中添加以下行，在 httpd.conf 中启用它：

```apache
LoadModule ssl_module modules/mod_ssl.so
```

现在你可能注意到加粗的提示应替换为你自己的适当值。此外，请确保你输入的通用名称（Common Name）是你服务器的真实完全限定域名，例如 `www.yourserver.com`。

命令完成并回答所有提示后，你将有两个新文件：`privkey.pem`，它是用于签署证书的私钥，以及 `testcert.csr`，即证书请求。下一步是删除在上一步创建的密钥中的密码短语。如果不删除密码短语，每次启动 Apache 时都必须输入它。虽然这可能看起来像是额外的安全性，但实际上是个麻烦，因为它阻止了 Apache 在服务器遭受电源故障或你频繁重启 Apache 时完全重启。

要删除密码短语，请使用以下命令：

```bash
openssl rsa -in privkey.pem -out testcert.key
```

然后它会提示你输入在上一个命令最开始使用的相同密码短语：

```text
Enter pass phrase for privkey.pem:
writing RSA key
```

下一步是将证书请求转换为已签署的证书：

```bash
openssl x509 \
-in testcert.csr \
-out testcert.cert \
-req \
-signkey testcert.key \
-days 3650
```

然后它会显示：

```text
Signature ok
subject=/C=US/ST=Ohio/L=Cincinnati/O=TestSSL/OU=SSL Testing
Department/CN=www.example.com/emailAddress=youremail@example.com
Getting Private key
```

你在这里做的是使用 `openssl` 命令请求一个 X.509 证书，使用 `testcert.scr` 证书请求作为输入，并将生成的证书保存为 `testcert.cert`，该证书使用私钥 `testcert.key` 进行自签名，有效期为 10 年。

现在你拥有了自签名的服务器证书和密钥，你需要将两者都复制到 Apache 可以使用的目录位置：

```bash
mkdir -p /etc/apache/ssl.crt
mkdir -p /etc/apache/ssl.key
```





cp testcert.cert /etc/apache/ssl.crt/testcert.crt

cp testcert.key /etc/apache/ssl.key/testcert.key

然后，创建一个目录来存放你的新 SSL 网站：

mkdir -p /wwwssl

你可以使用任何喜欢的路径，甚至是现有的路径——请记住或写下你使用的路径，因为在稍后配置 Apache 时你会需要它。

最后，创建一个简单的信息文件，以便在测试 SSL 时有所展示：

echo "<?php phpinfo(); ?>" > /wwwssl/index.php

现在你的密钥已就位，SSL 网站根目录已创建，你需要在 httpd.conf 中启用 SSL 功能。如果你当前的 httpd.conf 文件包含一行写着“Include /etc/apache/ssl.conf”或类似的内容，那么任何 SSL 更改都应该在指定的 ssl.conf 文件中执行。否则，你可以直接在 httpd.conf 文件中进行修改，或者添加你自己对 ssl.conf 文件的引用，并在那里进行修改。

在你的 SSL 配置文件或配置段中，你需要确保以下项在全局配置作用域中可用（而不是在虚拟服务器或目录配置段中）：

Listen 443

接下来，你需要重用现有的 VirtualHost 段来处理 443 端口（如果存在），或者创建一个新的段，其中包含以下指令：

<VirtualHost _default_:443>

#### Server Certificate:
SSLCertificateFile /etc/apache/ssl.crt/testcert.crt

#### Server Private Key:
SSLCertificateKeyFile /etc/apache/ssl.crt/testcert.key

SSLEngine On

DocumentRoot "/wwwssl" # 使用你之前创建的 SSL 目录

Servername www.example.com
ServerAdmin youremail@example.com

</VirtualHost>

然后，一旦对配置文件进行了更改，请重启 Apache。如果你在浏览器中使用 https:// URL（例如 https://www.example.com）加载你的新 SSL 站点，你会收到证书无效的提示（因为它是自签名的）。点击“确定”，你应该能看到 phpinfo() 函数的输出。如果没有显示任何内容，或者浏览器无法连接到服务器，请检查 Apache 错误日志中是否有相关的错误消息——很可能只是一个简单的拼写错误。

> 要进一步调整 mod_ssl，并获取可用于 mod_ssl 的所有配置指令的完整列表，请访问 [http://httpd.apache.org/docs/2.0/mod/mod_ssl.html](http://httpd.apache.org/docs/2.0/mod/mod_ssl.html)。

### Apache 作为文件仓库

使用 Apache 比较酷的功能之一是将其用作简单的在线文件仓库，通过 WebDAV 实现。WebDAV（Web 分布式创作和版本控制）使 Apache 能够让用户将启用的目录视为其计算机上的远程目录或驱动器。类似于 Windows 共享或 NFS 导出，WebDAV 允许远程编辑和存储访问，只是使用 HTTP 作为传输层，而不是像 SMB 和 NFS 那样使用专门的 TCP 协议或端口。

要理解 WebDAV 如何作为共享驱动器工作，直接查看其实际运行过程会更容易理解，因此接下来，你将启用随 Apache 提供的 mod_dav 并进行测试。首先，与其他模块一样，检查 mod_dav 是否已经静态编译到 Apache 中，或者是否存在为可加载模块：

/path/to/httpd -l
ls /path/to/apache/modules

正如你可能猜到的那样，如果在 `httpd -l` 输出中没有看到 `mod_dav.c`，或者在文件列表中没有看到 `mod_dav.so`，你需要使用 Apache httpd 源代码自行构建它。要将 mod_dav 静态添加到 Apache 二进制文件中，请确保 configure 命令中存在 `--enable-dav` 和 `--enable-dav-fs`：

./configure \
--enable-dav \
--enable-dav-fs \
# ...以及你使用的其他 configure 设置

要将 mod_dav 构建为共享对象，只需在两个 DAV 相关行的末尾添加 `shared`：

./configure \
--enable-dav=shared \
--enable-dav-fs=shared \
# ...以及你使用的其他 configure 设置

然后使用 `make` 和 `make install` 构建并安装新的二进制文件和模块。

如果你决定使用 mod_dav 的动态模块，你需要在 httpd.conf 中启用它们，使用以下行：

LoadModule dav_module modules/mod_dav.so
LoadModule dav_fs_module modules/mod_dav_fs.so

为了实际存储 WebDAV 文件仓库的位置，你可以创建一个新目录，或者使用你选择的现有目录。你应该将 WebDAV 文件夹放在启用了 SSL 的网站根目录中，或者如果你计划使用基本身份验证来限制对 WebDAV 文件夹的访问，请确保稍后启用 SSL。基本身份验证以明文发送用户名和密码，因此你希望启用受保护目录的 SSL，以加密基本身份验证请求。如果需要，创建新的文件夹，并创建一个临时文件添加到 WebDAV 文件夹中：

mkdir -p /wwwssl/dav
echo "Testing DAV" > /wwwssl/dav/testing.txt

当用户访问你的 WebDAV 文件夹时，你将通过数据库或 htpasswd 文件对他们进行身份验证，以防止互联网上的匿名用户占满你的硬盘。首先，创建一个 htpasswd 文件来存储有效用户的密码，并使用 testdav 的用户账户对其进行初始化：

mkdir -p /davauth
/path/to/htpasswd -c /davauth/dav.htpasswd testdav

当提示输入密码时，输入你选择的密码。接下来，在 /wwwssl/dav 文件夹中创建一个 `.htaccess` 文件以强制执行基本身份验证。`.htaccess` 文件应包含以下内容：

AuthName "DAV Test"
AuthType Basic
AuthUserFile "/davauth/dav.htpasswd"
require valid-user

最后，在你的 httpd.conf 中创建一个 Directory 条目，以启用给定目录的 WebDAV 和基本身份验证：

<Directory "/wwwssl/dav">
    AllowOverride AuthConfig
    Dav On
</Directory>

然后你可以重启 Apache，WebDAV 将为你的 HTTPS 站点的 /dav/ 文件夹启用，可以通过类似 https://www.example.com/dav 的地址访问。你可以尝试在 Web 浏览器中加载此 URL，但其行为与普通非 DAV 网络目录没有区别。要使用你的 WebDAV URL 的功能，你需要使用支持 WebDAV 的软件。

jEdit、NuSphere 的 PHPEd 和 Macromedia Dreamweaver 等编辑器以及其他编辑器在一定程度上都支持 WebDAV。如果你手头没有这些编辑器，请不要担心——大多数现代操作系统实际上都支持在其文件资源管理器/浏览器工具中原生挂载 WebDAV 共享。

要使用操作系统的文件浏览器访问你的 WebDAV 共享，请按照适用于你操作系统的上述部分中的说明进行操作。

#### Windows 2000/XP

要在 Windows 2000 或 XP 下设置 WebDAV，你需要按照以下顺序运行“添加网络位置”向导：

- 1. 转到“我的网络位置”，双击“添加网络位置”，如 6.1 图所示。
- 2. 当出现“添加网络位置向导”时，单击“下一步”以显示服务提供商列表。选择“选择其他网络位置”选项，如 6.2 图所示，然后单击“下一步”。

# 第 6 章

![](img/ab27c6ac898db1f934d39fa127b14657_185_0.png)

图 6.1

![](img/ab27c6ac898db1f934d39fa127b14657_185_1.png)

图 6.2

- 3. 在“Internet 或网络地址”字段中输入你的 WebDAV 目录的 URL，如 6.3 图所示。然后单击“下一步”。

![](img/ab27c6ac898db1f934d39fa127b14657_186_0.png)

图 6.3

- 4. 在 SSL 安全警报对话框中单击“是”。之所以发出警告，是因为你使用的是自签名证书——这与之前尝试访问启用 SSL 的网站时看到的警告相同。
- 5. 然后系统会提示你输入用户名和密码以访问 DAV Test 域。输入创建 .htpasswd 文件时使用的值。
- 6. 然后系统提示你为网络位置命名，以便稍后轻松识别该位置。将网络位置的名称输入为 **My WebDAV**。
- 7. 现在你的 WebDAV 位置应该设置好了，你将看到“完成添加网络位置向导”屏幕。勾选“当我点击完成时打开此网络位置”复选框，如 6.4 图所示。
- 8. 然后系统会再次提示你接受自签名 SSL 证书并输入用户名和密码。接受该证书并输入你在第 5 步中使用的凭据。
- 9. 然后你应该会在标准的 Windows 资源管理器窗口中看到 WebDAV 共享的内容，如 6.5 图所示。
- 10. 像标准驱动器或文件夹一样使用你的 My WebDAV 共享——你可以像操作本地文件夹一样在 WebDAV 共享中添加、编辑和删除文件。





# 第 6 章

![](img/ab27c6ac898db1f934d39fa127b14657_187_0.png)

图 6.4

![](img/ab27c6ac898db1f934d39fa127b14657_187_1.png)

图 6.5

### Apache 技巧

#### Mac OS X

要在 Mac OS X 下设置 WebDAV，请执行以下操作：

- 1. 从 Finder 菜单中选择“前往”>“连接服务器”，或者直接在 Finder 窗口中按下 Command-K。这将弹出如图所示的“连接服务器”窗口（见图 6.6）。在“服务器地址”栏中输入您的 WebDAV 共享的 URL，然后点击“连接”。

![](img/ab27c6ac898db1f934d39fa127b14657_188_0.png)

图 6.6

- 2. 系统会提示您接受自签名 SSL 证书。点击“继续”。
- 3. 将显示 DAV Test 域的 用户名和密码 提示框。输入您之前创建 Htpasswd 文件时使用的用户名和密码。
- 4. 映射后的 WebDAV 驱动器现在应该像普通的已挂载网络卷一样显示在 Finder 中，如图 6.7 所示。现在您应该能够像使用任何标准本地或网络卷一样使用它。

![](img/ab27c6ac898db1f934d39fa127b14657_188_1.png)

图 6.7

### 摘要

在本章中，您已经看到添加几个 Apache 模块可以极大地提高您站点的性能。它告诉您如何简化 URL 重定向，修复用户拼写错误，压缩您的内容以节省带宽，创建基于 Web 的文件共享，并使用 MySQL 和 SSL 保护您的站点安全。这种可扩展性是使 Apache 不仅仅是一个普通 Web 服务器的关键所在。

在您探索了此处讨论的模块的潜力之后，您应该去研究您可以在 httpd.apache.org 和 sourceforge.net 找到的其他模块。在那里，您会发现可以针对其他数据库进行用户身份验证、提高 Perl 等其他语言性能、将 Apache 用作代理服务器等模块。如您所见，有各种用途的 Apache 模块。

虽然本章向您介绍了一种保护站点安全的新方法，但下一章将正面解决安全问题。

# 7
## 站点安全

安全是每位站点管理员最关心的问题之一——如果它不是，它应该成为首要关注点。将您的站点置于公共互联网上，相当于向各种入侵者发出公开邀请，您需要能够处理他们，无论您的站点多么小或多专业。幸运的是，PHP 可以帮助您保护您的站点和您的用户数据。如上一章所述，您可以使用 Apache 来控制身份验证，但您也可以使用 PHP 内置函数创建自己的身份验证系统。本章展示您如何做到这一点后，将引导您了解您可能遇到的一些更常见的攻击类型，并展示一些防止它们的简单方法。

### 控制访问

当您考虑保护网站安全时，最先浮现在脑海中的第一件事可能就是限制访问的方法。如果坏家伙无法访问 Web 应用程序，它就是安全的，对吧？当您选择保护敏感文件和脚本的方法时，您有一些选择，有些是 Apache 内置的，有些是基于 PHP 的，有些则是两者的混合。

#### Apache 控制的身份验证

锁定网站的最简单方法是使用基本身份验证（Basic Authentication），这在第 6 章中已经介绍过。通过使用 .htaccess 和密码文件的组合，您可以快速限制对您网站特定文件夹的访问。这种方法有许多优点。

首先，它非常容易实现。作为 Apache 默认安装的标准配置，简单的基于目录的基本身份验证可以轻松通过 .htaccess 或 <Directory> 条目进行设置。

使用内置 Apache 身份验证的缺点是什么？维护复杂的受限制文件夹和用户层级可能是一个麻烦事。如果您拥有大量用户或组，以及相当多的受保护目录，确保正确的用户在正确的组中，拥有对正确资源的访问权限，并使用最新的密码等，很快就会变成一场噩梦。

使用 Apache 进行简单身份验证，如果您正在处理多个负载均衡或镜像 Web 服务器，也可能是一个问题。因为用户凭据存储在每台机器上，您可能会处于文件不一致的状态——一些密码文件可能包含不同数量的用户、不同的密码，或其他问题。

作为 Apache 简单基于文件身份验证的替代方案，您也可以使用 mod_auth_mysql Apache 模块，这在第 6 章中也有介绍。使用 mod_auth_mysql 可以集中管理用户名/密码存储，并且还能提供复杂的权限匹配能力——而不仅仅是标准 Apache 基本身份验证中的简单用户名匹配。

与 Apache 简单身份验证一样，mod_auth_mysql 依赖于在 .htaccess 文件或 httpd.conf 中的 <Directory> 条目中指定的访问权限。如果您无法更改 Apache 配置，且您的主机不允许使用 .htaccess 文件，您就需要寻找其他方法。这时，基于 PHP 的身份验证就派上用场了。

### PHP 控制的身份验证

如果 Apache 控制的身份验证不可行，您实际上可以利用 PHP 的强大功能来模拟标准基本身份验证。通过发送正确的响应头并检查正确的服务器变量，您可以从头开始构建自己的基本身份验证系统，它的强大程度将不亚于 mod_auth_mysql，甚至更强。

为了展示如何使用 PHP 进行基本身份验证，您将设置一个简单的数据库作为用户凭据的存储库。然后 PHP 将检查用户名和密码是否与该数据库匹配；最终用户看到的只是标准的基本身份验证提示。

##### 创建身份验证数据库

首先，在 MySQL 中创建一个名为 WebAuth 的数据库：

```sql
CREATE DATABASE WebAuth;
USE WebAuth;
```

接下来，为身份验证系统创建一个 MySQL 登录名，并赋予其对您刚刚创建的数据库的只读访问权限：

```sql
GRANT SELECT ON WebAuth.* TO WebAuth@localhost IDENTIFIED BY 'AuthPass';
```

现在，设置用于存储用户名和密码的表。在这个例子中，该表将只存储用户名和密码的哈希值，但如果您愿意，可以轻松添加其他任何访问标准的额外字段。

```sql
CREATE TABLE Users (username varchar(50) PRIMARY KEY,  
passwd_md5 varchar(32) NOT NULL,  
passwd_sha1 varchar(40) NOT NULL);
```

请注意，我们没有简单地创建一个字段来存储用户的原始文本密码，而是创建了存储用户密码单向哈希值的字段。这样做确保密码仍然可以与在密码提示处输入的值进行比较，但使得那些在数据库被入侵时试图破解密码的人极其困难。如果您熟悉 MD5 或 SHA1，您知道它们都是单向哈希算法。在密码经过其中任何一种算法哈希处理后，几乎不可能确定原始密码。

> MD5 接受输入字符串并创建原始输入的 128 位“唯一”指纹或哈希值。
>
> SHA1 的行为类似，但稍微更安全一些，生成 160 位“唯一”指纹。

您可能已经注意到，前面的讨论并没有绝对地说这两个方案提供的唯一性或防篡改哈希值。直到最近，MD5 和 SHA1 都被认为是除了最安全数据之外的所有数据哈希处理的合理解决方案，SHA1 也是如此。当使用暴力破解时，没有一种加密方案是 100% 无法破解的。密码生成程序可以遍历每个字符的每个组合和每个密码长度，直到最终找到一个与算法生成的哈希值匹配的输入字符串。

然而，最近密码分析学的进展证明，MD5 可以通过找到一个产生相同输出哈希值的输入来更快地被攻破，即使输入字符串并不匹配——这是 MD5 的固有弱点。SHA1 最近也受到了攻击，随着处理能力的增加，暴力破解哈希值所需的时间迅速缩短。

为了对抗 MD5 中看到的任何类型的碰撞攻击，您创建 Users 表来同时存储密码的 MD5 和 SHA1 哈希值。这样做实际上使任何碰撞攻击尝试都徒劳无功——即使入侵者设法找到与 MD5 哈希值匹配的输入字符串，除非它是真实的密码，否则它不会与 SHA1 哈希值匹配。

为了使数据库对身份验证脚本有用，您需要至少添加一个用户：

```sql
INSERT INTO users VALUES ('testuser', MD5('testpass'), SHA1('testpass'));
```

注意在添加密码时使用了内置的 MySQL 函数 MD5() 和 SHA1()。

##### PHP 基本身份验证脚本

一旦数据库设置完成，创建以下脚本，并将其保存为 `phpauthbasic.php`：

```php
<?php
// 定义数据库常量
define('AUTH_HOST', 'localhost');
define('AUTH_USER', 'WebAuth');
define('AUTH_PASS', 'AuthPass');
define('AUTH_DB', 'WebAuth');

function attempt_auth() {
// 发送身份验证头
header('WWW-Authenticate: Basic realm="Protected by PHP"');
header('HTTP/1.0 401 Unauthorized');
```

167





# 第 7 章

```php
    }

    function check_login($username, $password)
    {
        $ret = false;

        if ($username && $password)
        {
            // Check if login matches database values
            $conn = mysql_connect(AUTH_HOST, AUTH_USER, AUTH_PASS);

            if (mysql_select_db(AUTH_DB, $conn))
            {
                // Search for matches
                $result =
                mysql_query("SELECT COUNT(username) AS ucount
                            FROM Users
                            WHERE username='" . addslashes($username) . "'
                            AND passwd_md5='" . md5($password) . "'
                            AND passwd_sha1='" . sha1($password) . "'
                            ", $conn);

                // Check if a match was found
                if (($row = mysql_fetch_array($result)) && $row['ucount'])
                {
                    $ret = true;
                    $_SESSION['username'] = $username;
                }
            }

            // Close connection
            mysql_close($conn);
        }

        return $ret;
    }

    session_start();

    // Check if using valid credentials
    if (!(isset($_SESSION['username']) ||
          (isset($_SERVER['PHP_AUTH_USER']) &&
           check_login($_SERVER['PHP_AUTH_USER'],
                       $_SERVER['PHP_AUTH_PW']))))
    {
        // Show login prompt
        attempt_auth();
        echo 'Authorization Required';
        exit;
    }
    ?>
```

这一切意味着什么？来看看是什么让这个脚本运转起来的。

你要做的第一件事是为数据库连接定义一些常量：

```php
<?php

// Define database constants
define('AUTH_HOST', 'localhost');
define('AUTH_USER', 'WebAuth');
define('AUTH_PASS', 'AuthPass');
define('AUTH_DB', 'WebAuth');
```

接下来是 `attempt_auth()` 函数的定义。该函数只是向浏览器发送响应头，告诉它尝试进行基本身份验证登录，并将在登录提示中显示给定的域作为安全区域：

```php
function attempt_auth()
{
    // Send authentication headers
    header('WWW-Authenticate: Basic realm="Protected by PHP"');
    header('HTTP/1.0 401 Unauthorized');
}
```

在 `attempt_auth()` 之后是 `check_login()` 函数的定义。在这里，传入的用户名和密码将实际与之前创建的 WebAuth 数据库中存储的值进行比对。首要任务是确保已传入用户名和密码，并连接数据库将 WebAuth 设为活动状态：

```php
function check_login($username, $password)
{
    $ret = false;
    if ($username && $password)
    {
        // Check if login matches database values
        $conn = mysql_connect(AUTH_HOST, AUTH_USER, AUTH_PASS);
        if (mysql_select_db(AUTH_DB, $conn))
        {
```

建立数据库连接后，你执行查询以检查用户名/密码是否匹配：

```php
// Search for matches
$result =
mysql_query("SELECT COUNT(username) AS account
FROM users
WHERE username='$username'
AND password='" . md5($password) . "'
AND pswd_sha1='" . sha1($password) . "'
", $conn);
```

### 站点安全性

为了构建此查询，必须首先使用 `addslashes()` 转义用户名，以帮助避免任何 SQL 注入攻击（稍后讨论）。此处使用了 PHP 函数 `md5()` 和 `sha1()`，但如果你愿意，也可以轻松使用 MySQL 的等价函数——它们应产生完全相同的结果：

```php
    // Search for matches
    $result =
        mysql_query("SELECT COUNT(username) AS count
        FROM users
        WHERE username = '" . addslashes($username) . "'
        AND passwd_md5 = MD5('" . addslashes($password) . "')
        AND passwd_sha1 = SHA1('" . addslashes($password) . "')
        ", $conn);
```

你可能已经注意到，在密码上添加了 `addslashes()` 函数作为包装器，而在之前 PHP 执行密码哈希的情况下并不存在这种情况。这再次是为了防止任何 SQL 注入攻击，甚至是一些简单的错误，即用户密码中可能包含撇号的情况。当首先使用 PHP 对密码进行哈希处理时，没有必要使用 `addslashes()` 转义结果，因为 `md5()` 和 `sha1()` 函数产生的输出仅由十六进制值组成——撇号或其他危险字符不可能溜进来。

要完成 `check_login()` 函数，将返回占位符设置为 true，并创建一个会话变量，稍后在脚本中使用它以避免不必要的重复查询：

```php
    // Check if a match was found
    if (($row = mysql_fetch_array($result)) && $row['account'])
    {
        $ret = true;
        $_SESSION['username'] = $username;
    }

    // Close connection
    mysql_close($conn);
}

return $ret;
```

接下来进入脚本中实际首次解释的代码，你开始初始化会话数据：

```php
    session_start();
```

然后，你首先检查来自 `check_login()` 的会话变量是否已设置。如果尚未设置——意味着该用户尚未通过身份验证——检查 PHP `AUTH_USER` 服务器变量并调用 `check_login()` 函数。当 PHP 尝试使用基本身份验证获取登录信息时，服务器变量 `PHP_AUTH_USER` 和 `PHP_AUTH_PW` 均存在。如果它们未设置，则用户尚未被提示输入登录信息。在这种情况下，如果没有传入登录信息，或者之前传入的凭据无效，你希望提示用户输入登录信息。如果未找到有效的用户信息，将调用 `attempt_auth()`，用户将再次获得登录的机会。只有当且仅当用户在登录提示中点击“取消”时，才会显示“Authorization Required”消息：

```php
    // Check if using valid credentials
    if ((!isset($_SESSION['username']) ||
        (!isset($_SERVER['PHP_AUTH_USER']) &&
           check_login($_SERVER['PHP_AUTH_USER'],
                        $_SERVER['PHP_AUTH_PW']))))
    {
        // Show login prompt
        attempt_auth();
        echo 'Authorization Required';
        exit;
    }
    ?>
```

为了测试 PHP 身份验证，你可以简单地尝试在浏览器中加载此脚本，但最好将其包含在你创建的任何标准 PHP 页面中。你可以使用以下代码将此授权测试作为简单的包含进行测试：

```php
<?php

require_once 'phpauthbasic.php';

echo "Authentication Successful!";

?>
```

当你尝试在浏览器中加载此脚本时，请使用 `testuser`/`testpass` 组合，或者你最初添加到 `users` 表中的任何凭据。如果用户名和密码正确，你应该看到一条漂亮的“Authentication Successful!”消息；如果你点击取消，你将得到令人恐惧的“Authorization Required”消息。

现在你看到了它的工作方式，你可能会认为使用这种方法没有任何理由不这么做。但正如你在决定如何编写应用程序时会做出的许多选择一样，这种方法存在一些缺点。

在使用此身份验证方法之前，必须满足两个主要要求。

-   首先，`safe_mode` 必须在 `php.ini` 中未启用。启用时，`safe_mode` 会阻止创建 `PHP_AUTH_USER` 和 `PHP_AUTH_PW` 服务器变量。如果这些变量不存在，无论使用的凭据是否真正有效，脚本都将不断重新显示登录提示，直到用户点击取消为止。快速确定 `safe_mode` 是否确实启用的方法：脚本的 uid 会添加到登录提示中域信息的末尾。

-   其次，此方法不能与 Apache 的基本身份验证系统一起使用。这适用于同一脚本级别或任何父目录下的任何 Apache 控制的访问（`.htaccess`）。如果启用了两个身份验证系统，Apache 系统将获得初始优先权。会发生的情况是，用户最初可以使用 Apache 基本身份验证的有效凭据登录，随后是 PHP 身份验证提示。然而，此时 HTTP 实际上已经清除了浏览器针对 Apache 控制的身份验证状态——这是 HTTP 401 响应的结果。由于浏览器不再针对 Apache 经过身份验证，它将重新提示输入 Apache 级别的凭据，然后回到 PHP 凭据，如此循环，直到用户在浏览器中点击“取消”或“停止”。




#### PHP 表单身份验证

如果 PHP 基本身份验证（Basic Authentication）对你来说不是可行的解决方案，或者你不喜欢浏览器登录面板的外观，请不要担心；你还有另一个选项。与其依赖浏览器自带的标准内置登录窗口，你可以轻松创建自己的登录表单，甚至可以复用之前大部分 PHP 身份验证代码。将以下内容输入到 `phpauthforms.php` 文件中。请注意，其中大部分内容直接提取自你之前使用的 `phpauthbasic.php` 文件：

```php
<?php
// Define database constants
define('AUTH_HOST', 'localhost');
define('AUTH_USER', 'WebAuth');
define('AUTH_PASS', 'AuthPass');
define('AUTH_DB',   'WebAuth');

function check_login($username, $password)
{
   $ret = false;

   if ($username && $password)
   {
      // Check if login matches database values
      $conn = mysql_connect(AUTH_HOST, AUTH_USER, AUTH_PASS);

      if (mysql_select_db(AUTH_DB, $conn))
      {
         // Search for matches
         $result =
              mysql_query('SELECT COUNT(username) AS ucount
                           FROM Users
                           WHERE username="' . addslashes($username) . '"'
                           '  AND passwmd5="'   . md5($password)     . '"'
                           '  AND passwd_sha1="' . sha1($password)    . '"',
                           $conn);

         // Check if a match was found
         if (($row = mysql_fetch_array($result)) && $row['ucount'])
         {
            $ret = true;
            $_SESSION['username'] = $username;
         }
      }

      // Close connection
      mysql_close($conn);
   }

   return $ret;
}

session_start();
// Check if using valid credentials
if (! (isset($_SESSION['username']) || 
check_login($_POST['username'],
$_POST['passwd'])))
{
?>
<form method="post" action="testforms.php">
<label for="username">Username:</label>
<input type="text" id="username" name="username" maxlength="50" /><br />
<label for="passwd">Password:</label>
<input type="password" id="passwd" name="passwd" /><br />
<input type="submit" value="Log in" />
</form>
<?php
}
```

发生了什么变化？实际上并没有太多。关键的修改是在文件的末尾进行的：

```php
// Check if using valid credentials
if (! (isset($_SESSION['username']) || 
check_login($_POST['username'],
$_POST['passwd'])))
{
    exit;
}
```

与检查服务器变量 `PHP_AUTH_USER` 和 `PHP_AUTH_PW` 不同，你通过 HTTP POST 检查传递的登录凭据，其名称为 `username` 和 `passwd`。然后，就像基本身份验证示例一样，如果登录无效或未提供，则会向用户显示登录提示。在这种情况下，`attempt_auth()` 函数已被移除，在它原来被调用的位置，取而代之的是一个简单的 HTML 表单：

```php
?>
<form method="post" action="testforms.php">
<label for="username">Username:</label>
<input type="text" id="username" name="username" maxlength="50" /><br />
<label for="passwd">Password:</label>
<input type="password" id="passwd" name="passwd" /><br />
<input type="submit" value="Log in" />
</form>
<?php
exit;
}
```

# 第 7 章

若要使用此身份验证方法，你只需在想要保护的任意页面顶部包含此脚本即可。将此文件命名为 *testforms.php*（它必须与之前使用的表单的目标相匹配）：

```php
<?php
require_once 'phpauthforms.php';
echo "Authentication Successful";
?>
```

那么这种方法的优势是什么？首先是兼容性。使用简单的基于表单的 PHP 身份验证在几乎任何情况下都能正常工作，无论是否启用了 *safe_mode*，或者 Apache 是否使用其自身的 `.htaccess` 身份验证。这种解决方案唯一的实际缺点是，你必须自己编写登录表单，并按照你想要的方式设置样式，而不是依赖浏览器/操作系统来为你完成这些工作。

#### 其他访问限制

除了通过用户名和密码限制访问外，你还可以使用 PHP 检查其他用户参数。一个常见的检查变量是用户的源 IP 地址。通过引用服务器变量 `$_SERVER['REMOTE_ADDR']`，你可以确保只有特定的 IP 范围被允许查看资源，或者相反，你可以阻止特定的 IP 地址。如果你正在为企业内网创建网站，你可以将访问限制在内部 IP 地址（假设你的网络使用了内部 IP）。例如，你可以决定只有 10.0.1.x 网络的成员可以查看网站的特定区域。另一个例子是 BBS 网站或网络论坛。很多时候，如果某人正在论坛发布垃圾信息，它们需要按 IP 地址禁止特定用户。

另一个值得检查的服务器变量是 `$_SERVER['HTTP_REFERER']` 变量。该变量持有之前查看的页面名称，可以帮助你消除某些类型的网络攻击。假设你创建了一个简单的表单，用于将数据保存到数据库、发送电子邮件，或者任何依赖有效用户输入的操作。你甚至可能付出了巨大努力来执行客户端输入验证，并指定了表单的最大长度。不幸的是，来自 Web 客户端的任何预期输入都可以轻松地通过外部表单进行破坏。任何站点攻击者都可以轻松复制你的表单 HTML 标记，然后根据需要对其进行修改——无论是用于信息收集、跨站脚本、SQL 注入，还是其他任何事情。

他们所需要做的只是制作该表单的副本，使其能够向你的站点提交不当数据，将其托管在他们自己的机器上，但使用绝对 URL 作为方法来向你的表单提交。当使用隐藏表单变量时，以及在 `php.ini` 中启用了 *register_globals* 时，这种类型的攻击可能会特别有害。

通过检查 `HTTP_REFERER` 值，只要确保输入来自你网站上的实际页面，你就可以消除大多数伪造表单攻击。

要查看 `HTTP_REFERER` 检查和 `REMOTE_ADDR` 验证的实际示例，请查看以下代码：

```php
<?php
// Check the referer
if (!preg_match('/http:\/\/localhost|
' (www\.example\.com/i/',
$_SERVER['HTTP_REFERER'] ))
{
    echo 'Invalid referer! ' .
    'We don't take kindly to spoofed forms in these parts.';
}

// Check to see if request came from internal users
if ( !preg_match( '/ (10\.\d(1,3)\.\d(1,3)\.\d(1,3))|
'( 172\.16\.\d(1,3)\.\d(1,3) )|
'( 192\.168\.\d(1,3)\.\d(1,3) ) /i' ,
$_SERVER['REMOTE_ADDR'] })
{
    echo 'Invalid client address! ' .
    'Who let YOU in here?';
}
?>
```

这段代码首先检查引用页面，以确保它来自 localhost 或预期的域（假设你已将其更改为匹配你自己的域），然后检查用户的 IP 地址，以确保它来自内部/私有 IP 范围。

PHP 可以做的另一件有助于限制某些类型访问的事情是，提供 CAPTCHA 图像用于注册表单。CAPTCHA 的全称是 "Completely Automatic Public Turing Test to Tell Computers and Humans Apart"（完全自动公共图灵测试，用于区分计算机和人类），这是一种测试，通常会在图像中呈现略带扭曲的文本。其想法是，尽管外观扭曲，但人类应该能够识别出文本实际内容，而计算机则不能。许多免费电子邮件和公告板网站使用此类技术来阻止自动机器人脚本注册滥用服务（例如发送垃圾邮件等）。

尽管目前处于 alpha 开发阶段，PHP Pear 库中的 `Text_CAPTCHA` 包提供了实现 CAPTCHA 功能的简单接口。可以在 http://pear.php.net/package/Text_CAPTCHA 找到 `Text_CAPTCHA`。

如果你想尝试 `Text_CAPTCHA`，你可以简单地使用 `pear install` 命令安装它：

```bash
pear install -f Text_CAPTCHA
```

你需要使用 `-f` 标志强制安装，因为 `Text_CAPTCHA` 目前不被 Pear 团队视为稳定版本，所以普通的非强制安装将会失败。还要注意，`Text_CAPTCHA` 依赖于 `Text_Password` 和 `Image_Text`（也是 alpha 版本）Pear 包，因此如果你还没有它们，你需要先安装这些包。

一旦它们都安装完毕，创建以下内容作为 `captchatest.php`：

```php
<?php
// Include the Pear class
require_once('Text/CAPTCHA.php');

// Set the options for the generated text;
$options = array(
```



# 第 7 章

## 站点安全

当你在浏览器中运行这段代码时，你应该看到类似图 7.1 的效果。

![](img/ab27c6ac898db1f934d39fa127b14657_201_0.png)

```php
'font_size' => 25,
'font_path' => './../',
'font_file' => 'VerMono.ttf'
);

// Create a CAPTCHA object
$c = Text_CAPTCHA::factory('Image');

// Initialize the CAPTCHA object with random text
$r = $c->init(250,100, null, $opts);

// Check if CAPTCHA object is valid
if (PEAR::isError($r)) {
    echo 'CAPTCHA Generation failed.';
    exit;
}

// Generate the PNG CAPTCHA image
$png = $c->getCAPTCHAasPNG();

// Show the image in the browser
header('Content-type: image/png');
echo $png;
```

Text_CAPTCHA 是如何知道你想要使用的字符串的？它并不知道。当你初始化验证码对象时，你传入的测试字符串是 `null`：

```php
// Initialize the CAPTCHA object with random text
$r = $cap->init(250,100, null, $opts);
```

如果你想显式地设置由 Text_CAPTCHA 渲染的文本字符串，只需将输入字符串从 `null` 更改为你想要的值：

```php
// Initialize the CAPTCHA object with random text
$r = $cap->init(250,100, 'computers be gone!', $opts);
```

在你的 PHP 脚本中，其他需要检查的关键点包括本地文件名及其访问方式。请查看以下代码：

```php
<?php

$contents = file_get_contents('/path/to/content/' . $_POST['file']);

echo $contents;

?>
```

这种类型的代码经常出现在许多自制的内容管理系统（CMS）或某种自定义文档检索脚本中。不幸的是，它存在巨大的安全风险。如果攻击者提交文件值 `../../../../../etc/passwd` 会发生什么？如果服务器没有妥善锁定——而许多服务器并没有——系统密码文件的内容将会直接回显到屏幕上。

你可以采取几个简单的步骤来帮助防止此类攻击。首先，如果你能控制 Apache Web 服务器，请确保它以非特权用户身份运行。无论 Apache 以哪个用户身份运行——apache、nobody、www，都无所谓——请确保该用户没有权限访问除合法网站文件以外的任何文件。

其次，确保你转义文件路径中提供的父目录访问点，如下所示：

```php
<?php
$file = str_replace('../../', '', $_POST['file']);
$contents = file_get_contents('/path/to/content/' . $file);

echo $contents;

?>
```

如果可能，最好是给你的转义文件名加上路径前缀。这样，如果攻击者为文件值提供了绝对路径，它仍然会相对于指定文件夹运行。

### 网站攻击

每当你在公共互联网上发布一个站点时，它就面临被攻击的风险。虽然没有任何应用程序能真正达到 100% 的安全，因为新的漏洞利用和黑客技术每天都在被发现，但有一些类型的攻击你可以在 PHP 脚本中相对容易地加以防范。

#### 滥用 register_globals

如果每一篇谈论 `register_globals` 的文章、书籍或文档片段都没有将其灌输到你的脑中，那么这里再次强调：将 `register_globals` 设置为 `on` 是一场等待发生的灾难。

如果你不熟悉 `register_globals`，它是 php.ini 中的一个设置，用于控制具有与表单元素或 Cookie 相同名称的变量的自动填充。在本章前面创建的登录表单中，有一个名为 `username` 的字段。通常，在禁用 `register_globals` 的情况下，在表单提交后访问 `username` 字段的唯一方法是使用 `$_POST` 或 `$_GET` 数组，具体取决于表单的方法。当启用 `register_globals` 时，`username` 字段可以通过 `$_POST` 或 `$_GET` 再次访问，但也可以作为 `$username` 使用。

自 PHP 4.2.0 以来，`register_globals` 的默认值是 *off*，但通常 Web 主机为了提供与假定存在且依赖 `register_globals`=`on` 的旧脚本的兼容性，会重新启用 `register_globals`。不幸的是，这为恶意用户提供了主要的攻击途径。当启用 `register_globals` 时，PHP 按照 `variables_order` 设置中指定的顺序评估环境、表单、`cookie` 和服务器变量。如果服务器使用“推荐”的设置文件，首先设置 `GET` 变量，然后设置 `POST` 并覆盖任何匹配的 `GET` 值。接着设置 `cookie` 值，随后是服务器变量，覆盖之前设置的任何匹配值。

虽然这种行为看起来很方便，但使用克隆表单或伪造的 Cookie 信息很容易对其进行利用。关于它可能被如何利用的例子，请查看以下 PHP 代码：

```php
<?php
    if (user_is_admin())
    {
        $access_level = 10;
    }
    show_menu($access_level);
    // ... and so on ...
?>
```

在这种假设情况下，脚本调用 `user_is_admin()` 函数来确定用户是否为管理员。如果是，`$access_level` 变量会被设置为 10，并且可以想象，随后脚本中可能会显示完整的管理人员界面。

如果启用了 `register_globals`，请求文件并将期望的访问级别附加到查询字符串中是一件极其简单的事情，如下所示：

```
http://www.example.com/file.php?access_level=10
```

现在，如果脚本被调用并附加了该 `access_level`，无论用户是否真的是管理员，由于 `register_globals` 以及 PHP 不要求变量初始化，`$access_level` 变量会在脚本开始时自动设置为 10。

幸运的是，避免此类陷阱相对容易。请确保在禁用 `register_globals` 的情况下编写代码，使用正确的 `$_GET` 和 `$_POST` 超全局变量，初始化可能不安全的变量，并确保在开发和测试站点时将 `error_reporting` 设置为 `E_ALL`。

如果你无法在 php.ini 中禁用 `register_globals`，如果 Apache 中正确启用了该功能，你可以使用 `.htaccess` 文件将其关闭：

```
php_flag register_globals off
```

#### SQL 注入攻击

另一种具有更高潜在破坏性的脏数据攻击是 SQL 注入攻击。与 `register_globals` 攻击结合使用，或者仅仅通过普通的 Web 表单，SQL 注入攻击就是在本应输入无害数据的地方插入恶意 SQL 语句。

SQL 注入利用的是输入清洗和数据验证的缺失——即在 PHP 构建的 SQL 查询中盲目使用数据。请查看以下访问本章前面创建的 WebAuth 数据库的例子：

```php
<?php
$username = $_POST['username'];
$conn = mysql_connect(AUTH_DB, AUTH_USER, AUTH_PASS);
mysql_select_db(AUTH_DB, $conn);
$sql = "SELECT * FROM Users WHERE username='" . $username . "'";
mysql_close($conn);
?>
```

看起来相当无害，对吧？你会期望它愉快地接受表单发送的 `username` 变量值，并查找与该特定用户名相关的所有列。这段代码的问题在于 SQL 查询。注意 `$username` 变量在发送到数据库之前没有任何形式的验证、清洗或准备。在大多数情况下，你可能不会注意到任何异常，而且它几乎不会抛出错误。

然而，当在发送表单的用户名字段中输入以下值时，事情会迅速变得恶劣：

```
'; DELETE FROM Users; SELECT '0wmjD' AS username FROM Users WHERE '1'='1
```

仔细观察这个值正在发生什么。它首先终止 `$username` 变量附加之前的查询部分，删除 `Users` 表中的所有信息，然后执行攻击者选择的查询，只是为了结束查询并匹配最终的单引号。




# 第 7 章

当将“恶意”的用户名值替换到原始查询中时，实际生效的命令集合看起来会像这样：

```
SELECT * FROM Users WHERE username='';
DELETE FROM Users;
SELECT 'Ow3d' AS username FROM Users WHERE ''=''
```

如果发送给 SQL 服务器 的数据没有像本例中那样进行转义，可能会发生各种不良情况。想象一下，如果中间那条命令是 `DROP DATABASE` 或 `GRANT` 命令——那将是一场灾难。这个例子只是 SQL 注入攻击可能发生情况的简化版，但它应该能让你尝到这种攻击可能对你的数据和系统完整性造成的破坏味道。

与困扰 PHP 脚本的许多常见问题一样，只要稍加规划并遵循彻底的代码卫生实践，SQL 注入在某种程度上是可以预防的。如果将 `magic_quotes_gpc` 设置为开启状态，PHP 会帮你处理表单数据中“危险”字符的转义问题。当启用 `magic_quotes_gpc` 时，PHP 会在你甚至能在脚本中触及它们之前，自动转义任何转义字符（如撇号）。不幸的是，这种行为会应用于所有 GET、POST 和 cookie 变量，无论它们是否会在 SQL 语句中使用——而且大多数时候，这可能会让你感到些许烦恼。

为了确保你的数据只在你需要的时候被转义，请在 `php.ini` 中关闭 `magic_quotes_gpc`，并对所有传递给 MySQL 的数据使用 `addslashes()`。`addslashes()` 函数会自动转义任何危险字符，从而防止你的输入使 MySQL 崩溃——无论是针对 SQL 注入攻击，还是含有特殊字符（如带撇号的姓氏）的合法数据。

作为第二道防线，请确保你在 PHP 中访问数据库所使用的用户仅拥有维持应用程序运行所需的最小权限。在之前的 SQL 注入攻击中，删除所有用户记录的操作实际上会失败——因为在该章开始时设置用户时，只授予了 SELECT 权限。

SQL 注入攻击的一个相对概念是文件系统执行攻击，应以类似的方式对待。任何未清理的输入数据如果成为 `system()` 或 `exec()` 调用的一部分，都应被视为可疑对象，因为它们很容易像 SQL 注入攻击那样，将一系列恶意的系统命令串联起来。

#### 跨站脚本

虽然 SQL 注入和对 `register_globals` 的滥用主要涉及脏输入数据的使用，但还有另一种依赖动态输出不干净的攻击方式——跨站脚本。

通常缩写为 XSS 的跨站脚本，是指利用未过滤的动态输出，攻击者能够添加或修改页面生成的标记。最常见的情况是，在页面的输出数据中添加一小段 JavaScript，随后它会做一些阴险的事情，比如诱骗其他用户泄露其登录凭据或信用卡信息，或者可能泄露 cookie 或会话信息，以便立即入侵账户。

## 站点安全

为了更好地理解攻击的确切流程，请考虑以下场景：

- 1. 攻击者在博客或其他网站上填写评论表单。评论中包含了一个恶意脚本。
- 2. 这些评论在页面上显示，脚本保持完整且处于激活状态。
- 3. 一名无辜的用户访问该站点，并阅读攻击者的评论，其中可能包含也可能不包含一个可点击的链接。
- 4. 通过点击攻击者的链接或仅仅访问页面，用户会被要求验证私人信息，例如用户名或密码。
- 5. 用户不知不觉地提交了私人信息，认为这是他们正在访问的合法站点所请求的。
- 6. 用户被盗的信息被路由到互联网上的其他位置，要么存储起来以便后期分析，要么将新信息通知给攻击者。

这怎么可能发生呢？当“受信任”的网站在将特殊字符作为输出或标记发送之前未正确清除这些字符时，跨站脚本就起作用了。在 Web 环境中，这意味着动态输出中存在的以下字符：小于号 `<`、大于号 `>`、与号 `&`、单引号和双引号，以及任何 UTF-8 字符。

幸运的是，在处理动态输出清洗时，PHP 提供了多种选项供你选择：

- `htmlspecialchars()`：转义与号、小于号、大于号、单引号和双引号，使其成为大多数动态生成的 HTML 的合适选择。
- `htmlentities()`：类似于 `htmlspecialchars()`，但 `htmlentities()` 除了 `htmlspecialchars()` 涵盖的五个核心字符外，还会转义任何具有 HTML 实体等价物的特殊字符。
- `strip_tags()`：从字符串中移除所有 HTML 和 PHP 标签。你甚至可以提供一个允许的标签列表，以便白名单“安全”的标签（如格式标签），并移除任何更危险的标签，如 `<script>`。
- `utf8_decode()`：将 UTF-8 编码的字符转换为等效的 ISO-8859-1 字符。

### 其他考虑

除了直接影响你编写的代码或服务器配置的问题外，在应用程序的设计、开发和维护过程中，还必须考虑一些其他问题。

最容易解决的问题之一是保持系统更新并应用所有最新补丁。如果你的操作系统有更新核心系统软件的自动化方法，通常利用它是一个好主意。许多最近的 Web 服务器漏洞实际上是利用了旧版软件中的缺陷——病毒和蠕虫编写者通常利用厂商发布的关于最近服务器补丁的信息，编写他们知道会影响旧版本的恶意代码。

更新系统时也不应忽略的另一组对象是随 PHP 安装的 PEAR 和 PECL 包。两者都可以通过一条简单命令轻松更新：`pear upgrade-all`。关键在于定期运行该命令，或者更好的是，将其添加为 cron 任务。

在编写应用程序时，你可以做几件小事来降低 `register_globals` 漏洞或 SQL 攻击的可能性。首先，确保在使用前初始化所有变量；这样就绝无可能让表单或查询字符串变量偷偷溜进来。其次，确保在生产 Web 服务器上关闭任何错误报告输出。通过禁用错误消息的显示，当发生错误时（如 SQL 查询中的语法错误，或 SQL 服务器的主机名或 IP 地址），敏感信息可能泄露的风险就会消失。

还有一些其他有助于维护站点安全的事情，并不完全是你可以输入或配置的。黑客入侵你站点的一种可能方式涉及一点点社会工程学，以及很少甚至没有实际的计算机入侵。如果你是网站的管理员，负责创建用户登录和故障排除，你就处于一个非常严肃的角色，如果没有适当的保障措施，该角色可能被利用。在许多情况下，黑客只需要致电网站管理员，假装是一个忘记密码的用户即可。如果管理员向这个不幸的用户泄露了用户名或密码，黑客立即就拥有了网站的合法登录凭据，而不需要任何网络嗅探或暴力破解攻击。

另一个对站点安全大有裨益的小事是在开发周期中进行频繁的代码/同行评审。通过让你的同事或同行检查你的代码，反之亦然，你可以在代码真正面对公众之前，尽早揭露许多明显的安全问题。

最后，通过频繁访问诸如 Secunia (http://secunia.com/)、CVE (http://www.cve.mitre.org/) 和 CERT (http://www.cert.org/) 等安全相关站点以及其他站点，确保你紧跟最新的安全和漏洞新闻。

### 摘要

如你所见，在处理由 PHP 驱动的网站安全性时，有许多事情需要考虑。如果你保持严格的数据清洗实践，确保所有信息在进入和离开系统时都是有效的，你的网站将抵御绝大多数简单的攻击者。




# 第 8 章：PEAR 与 PECL

开源的核心理念，当然是通过协作努力来实现伟大的事业。无数贡献者及其努力之间存在的协同效应，推动着开源项目不断突破日益扩展的边界。然而，这种巨大且多元化的努力也带来了可能阻碍该运动成功的挑战。这些挑战包括组织、协调和方向。如果没有组织，编写代码就不会有标准，也没有系统的方法来整合软件包。如果没有协调，代码片段就会分散在广阔的互联网中，极有可能迷失在编写糟糕的 HTML 页面之间，再也无人问津。如果没有方向，就没有对未来的展望，也没有能让有志的贡献者兴奋的 resources。简而言之，那就只是一群技术宅在编写和重写与所有人相同的代码片段，每个人都各自为政，生活在自己的“计算气泡”中。然而，众所周知，人无完人（每个人都不是孤岛），这正是 PEAR 和 PECL 团队发挥作用的地方，它们提供急需的组织、协调和方向，以便开发者在长远来看都能成为更好的编程者。

通过为开发者提供用于完成常见任务的现成脚本，例如连接数据库或与 XML 文档交互，PEAR 和 PECL 软件包可以为您节省大量的编码时间和麻烦。

虽然两者都完成了类似的任务，但 PEAR 和 PECL 之间存在根本差异，本章将对此进行详细说明。

### 什么是 PEAR？

PEAR（PHP 扩展和代码库）旨在作为流浪但有用的类的家园。顾名思义，它是一个代码软件包库，可能由一个或多个文件组成，并完成诸如创建 HTML 表单、处理日期和图片、或连接数据库并执行查询等常见任务。由于这些是每个编程者都会不时使用的功能，它们成为了 PEAR 软件包的绝佳候选者。

由于开发并发布 PEAR 软件包有一套严格的编码标准，程序员可以确信一个软件包的外观和感觉与其他软件包保持一致。当您熟悉如何使用它们时，您将开始知道要寻找什么以及代码是如何结构的。PEAR 软件包还以其广泛的注释要求和命名约定而闻名，这是许多开源程序严重缺乏的，留给您艰巨的任务去试图理清别人的逻辑。

所有新软件包在纳入 PEAR 发行列表之前，都必须经过 PEP（PEAR 提案系统）。这一四步流程确保每个软件包都经过准确性、可靠性和相关性的严格审查。如果您想了解有关 PEP 的更多信息，可以访问网站 `http://pear.php.net/pepr`。

### 什么是 PECL？

PECL（PHP 扩展社区库）是 PEAR 的衍生项目，主要用于容纳不再随 PHP 默认安装捆绑的功能组。截至 PHP 5，这些扩展可以从常规 PHP 下载中单独下载和安装。但需要注意的是，目前驻留在 PECL 中的一些扩展现在已经随默认安装捆绑（例如 SQLite），或者是 PHP 核心团队以外的人员提交的扩展，从未与 PHP 捆绑在一起（例如 POP3）。

由于大多数 PECL 扩展曾经是 PHP 标准函数列表的一部分，标准规定它们必须使用 PHP 的编码标准编写（而不是 PEAR 的标准）。虽然公众仍然可以提交软件包，但提交流程包括由 pecl-dev 邮件列表进行预先批准。

### 探索 PEAR

在您深入 PEAR 世界之前，您应该知道，由于它是一个基于类的系统，为了正确使用这些软件包，您应该对 PHP 中的 OOP（面向对象编程）相当熟悉。如果您是一个坚定的基于函数的编程者，最好通过快速教程或简要回顾本书第 2 章来磨练您的 OOP 技能。

您首先需要的就是 PEAR 软件包本身，它使您可以轻松地安装或升级新的 PEAR 软件包。幸运的是，这个管理器已预装于 PHP5（以及 4.3.0 及以上版本），并将在安装、管理和升级其他 PEAR 软件包时使您的生活更轻松。主要的 PEAR 软件包还包含一组错误处理函数，使您可以轻松检测和管理工作时遇到的错误。

#### PEAR 管理器

如前所述，PEAR 管理器的主要目的是协助您管理其他 PEAR 软件包并与之协作。它附带了一组您可以从命令行运行的命令（可能需要或不需要 root 访问权限）。您可以在此处找到完整列表 `http://pear.php.net/manual/en/installation.cli.php`，但下表突出了供您参考的主要命令：

| 命令 | 作用 |
| :--- | :--- |
| bundle [package name] | 下载并解压 PECL 扩展 |
| download [package name] | 下载软件包而不安装它 |
| download-all | 下载所有可用的软件包 |
| info [package name] | 显示软件包的信息 |
| install [package name] | 下载并安装软件包 |
| list | 列出已安装的软件包 |
| list-all | 列出所有软件包 |
| list-upgrades | 列出已安装软件包的可用升级 |
| uninstall [package name] | 卸载并删除软件包 |
| upgrade [package name] | 升级软件包 |
| upgrade-all | 升级所有已安装的软件包 |

要使用任何命令，只需在命令前加上 `pear`，如下所示：

```text
pear info XML-RPC
```

如您所见，这将为您提供名为 `XML-RPC` 的 `PEAR` 软件包的信息。

还有一些 PEAR 配置变量，您可以对其进行控制。这些主要与目录信息和用户偏好相关，通常默认值是可以接受的。您可以访问 `http://pear.php.net/manual/en/installation.cli.php` 获取完整列表。然而，下表列出了其中一些更常见的变量：

| 变量名 | 代表的含义 | 默认值 |
| :--- | :--- | :--- |
| bin_dir | 存放可执行文件的目录 | /usr/bin |
| ext_dir | 存放已加载扩展的目录 | . |
| php_dir | 存放 PHP 安装的目录 | /usr/lib/php |
| preferred_state | 要下载的优先软件包状态（stable, beta, alpha, devel, or snapshot） | stable |

要查看您当前的设置，请使用 `config-show`（或 `config-get` 用于查看单个变量的值）命令，如下所示：

```text
pear config-show
```

这会显示每个配置变量的描述、变量名称以及当前的设置。要更改设置，请使用 config-set 命令，例如：

```text
pear config-set preferred_state devel
```

config-help 命令向您显示有关特定配置变量的更多信息。

#### 安装软件包

其他几个 PEAR 软件包随 PHP 5 预装，您可以通过运行以下命令（从 root 登录）找到完整列表：

```text
pear list
```

这将为您提供已安装软件包的列表、已安装的版本以及发布状态（stable, beta, 等等）。如果您想安装其他软件包，以下各部分简要概述了安装过程。

##### CLI 安装

如果您有 root 访问权限，只需输入以下命令即可安装任何新软件包：

```text
pear install [package name]
```

该命令会跳转到 PEAR 网站，下载您指定的软件包（当然不包括括号），并在您的机器上安装它。

##### FTP 安装

如果您没有命令行访问权限，或者您当前的 Web 主机不提供您想要的 PEAR 软件包，您可以通过完成以下两步来安装软件包：

- 1. 直接从 PEAR 网站下载压缩的软件包，在本地解压，并将文件上传到您的网站（将它们保存在 var/www/www.yourdomain.com/includes 目录中）。您也可以上传压缩文件，并在主机服务器上解压它（同样，保存到 var/www/www.yourdomain.com/includes 目录）。
- 2. 修改您的 php.ini 文件以匹配刚才使用的包含路径。

```text
include_path = "..:/www/includes"
```

您可能还需要在每个访问该软件包的脚本中包含一行，如下所示：

```php
<?php
ini_set("include_path", '/var/www/www.yourdomain.com/includes/'. PATH_SEPARATOR . ini_get("include_path"));

// 此处为 PHP 脚本的其余部分。
?>
```

您的软件包现在已经安装并准备就绪。




#### 使用已安装的包

一旦安装了该包，其使用和访问都非常简单。只需在脚本开头包含一行必要的文件引用，如下所示：

```php
<?php require_once("HTML/QuickForm.php");
//you are now able to access and reference classes, methods and properties
//contained in the quickform.php file to easily create HTML forms.
?>
```

### 简单快捷的 PEAR 包

截至今日，目前有 318 个 PEAR 包可供使用，涵盖多种领域，并且每天都在增加新的包。虽然本书不会讨论所有这些包，但以下章节将介绍其中一些较常用的包，并突出显示您可能需要确保已安装的包。此外，请记住，这些章节会保持简单，但如果您需要更健壮的功能，也会为您指引正确的方向。

#### Auth_HTTP

此包的目的是提供一个类似于 Apache .htaccess 登录框的身份验证系统。它是一种保护网站某区域密码的简单便捷方式。请注意，此包依赖于更健壮的 PEAR::Auth，而 PEAR::Auth 又依赖于 PEAR::DB 包，因此，Auth_HTTP 包要正常运行，必须先安装这两者。

Auth_HTTP 的简单用法如下：

```php
<?php require_once("Auth/HTTP.php");

$auth = new Auth_HTTP('DB::', 'mysqli://username:password@localhost/databasename');

$auth->start();
?>
```

首先，您包含 Auth/HTTP.php 文件，从而获得对该正确包的访问权限。然后，您使用如上所述的参数实例化一个新的 Auth_HTTP 对象。因为您实际上使用的是 PEAR::DB 包来登录数据库，所以您可以更改所使用的数据库类型，并命名其他选项，如套接字、路径、端口号等。尽管本章稍后将简要讨论此包，但 PEAR::DB 包的详细描述可以在 http://pear.net/manual/en/package.Database.db.php 找到。接下来，您调用 start() 函数启动身份验证过程，您的页面即受密码保护。

当然，这在改进和自定义方面留下了很大的空间，您可以更进一步，要求身份验证过程从数据库中的表中查找用户。您可以通过使用 $authOptions 变量来指定登录选项：

# 第 8 章

```php
<?php

require_once ("Auth/HTTP.php");

$AuthOptions = array(
        // use the same data source name (database login info) as in previous example
        'dsn'=>'mysql://username:password@localhost/databasename',

        //specify the database table that contains user info
        'table'=>'users',

        //specify the column that holds the username
        'usernamecol'=>'username',

        //specify the column that holds the passwords
        'passwordcol'=>'password',

        //specify the encryption type used
        'cryptType'=>'md5',
        );

$a = new Auth_HTTP ("DB", $AuthOptions);
        //specify the name of your realm
$a->setRealm('Registered Users Only');
        //specify the error message seen by the user if authentication fails
$a->setCancelText('<h2>Access Denied.</h2>');

$a->start();

        //check to see if the user is authorized
if ($a->getAuth ()) 
        {
                // body of authorized text goes here.
                echo "Hi there, authorized user!";
        };
?>
```

如您所见，这提供了一种非常简便的用户身份验证方式。要在其他页面上检查授权，只需使用 getAuth() 函数即可。

Auth_HTTP 包还有其他您可以指定的参数，而 Auth 包则提供了一个非常健壮的基于 HTML 表单的身份验证系统。您可以分别在 http://pear.php.net/manual/en/package.authentication.auth-http.php 和 http://pear.php.net/manual/en/package.authentication.auth.php 阅读有关这些包的更多信息。

#### Date

虽然 PHP 提供了返回日期和时间信息的内置函数，但此 PEAR 包为您提供了一种简便的方法，将这些信息转换为常用的结果，例如本月剩余天数、当前星期几等。

此包可用的函数非常多，我们为每个函数提供示例将是一件困难的事。但是，以下章节介绍了 Date 类中一些较常用的方法。访问 `http://pear.php.net/package/Date/docs/latest/Date/Date.html` 可以查看方法的完整列表。

##### Date 类

此类出现在主 date.php 文件中，并提供以下方法供您使用：

- Date: 构造函数，创建一个新的日期对象。
- addSeconds: 向日期添加特定秒数。
- addSpan: 向日期添加时间段。
- after: 确定一个日期是否晚于另一个日期。
- before: 确定一个日期是否早于另一个日期。
- convertTZ: 将日期转换为另一个时区。
- equals: 确定两个日期和/或时间是否完全相等。
- format: 根据用户指定格式格式化日期。
- getDate: 以特定格式返回日期。
- getDay: 返回日期对象中该月的天数。
- getDayName: 以字符串格式返回日期对象的星期几名称。
- getDayOfWeek: 以整数格式返回日期对象的星期几。
- getDaysInMonth: 返回日期对象所在月的天数。
- getHour: 返回日期对象的小时。
- getMinute: 返回日期对象的分钟。
- getMonth: 以整数格式返回日期对象的月份。
- getMonthName: 以字符串格式返回日期对象的月份名称。
- getNextDay: 返回日期对象第二天 的日期。
- getNextWeekday: 返回日期对象下一个工作日的日期。
- getPrevDay: 返回日期对象前一天 的日期。
- getPrevWeekday: 返回日期对象上一个工作日的日期。
- getQuarterOfYear: 以整数格式返回日期对象所在的季度。
- getSecond: 返回日期对象的秒数。
- getTime: 返回自 Unix 纪元以来的秒数。
- getWeekOfYear: 以整数格式返回日期对象所在的年份中的周数。
- getWeeksInMonth: 返回日期对象所在月 的周数。
- getYear: 返回日期对象的年份。
- inDaylightTime: 确定时间/日期是否处于夏令时。
- isLeapYear: 确定日期对象的年份是否为闰年。
- setDate: 设置日期对象的日期。
- setDay: 设置日期对象的天数。
- setHour: 设置日期对象的小时。
- setMinute: 设置日期对象的分钟。
- setMonth: 设置日期对象的月份。
- setSecond: 设置日期对象的秒数。
- setTZ: 设置日期对象的时区。
- setYear: 设置日期对象的年份。

以上全部来自 Date 类。还有两个其他类被 date 类使用，但也可以直接使用；它们是 Date_Span 和 Date_TimeZone 类。如果比 Date 类能提供的功能（例如返回所有可用时区的列表，或确定服务器默认时区）需要更具体的功能，它们内部包含许多特定方法。

##### 快速示例

以下是一个简单示例，展示了使用 Date 包输出诸如今年剩余周数等信息是多么容易：

```php
<?php
require_once('date.php');

$currweek = new Date();

$weeksleft = 52 - ($currweek->getWeekOfYear());
echo "There are " . $weeksleft . " weeks left in the year.";
?>
```

如您所见，当您试图完成更复杂的日期计算或处理时区时，如此简单的东西确实可以让您的生活更容易。

#### DB

这是允许您轻松连接和查询数据库的 PEAR 包。还有许多其他与数据库相关的包可供您参考。例如，MDB 与 DB 类似，但提供了更多



可移植性。DB 应能在您的标准配置上运行，但如果您遇到兼容性问题，还可以尝试其他方案。实际上，PEAR 专门设立了一个用于处理数据库的包类别，可以通过 `http://pear.php.net/packages.php?catpid=7&catname=Database` 找到。

在接下来几个示例中，您需要以下信息：

- `MySQL`：您的数据库类型
- `testdatabase`：数据库名称
- `testtable`：数据库表
- `username`：访问数据库的用户名
- `password`：用户的密码
- `localhost`：服务器名称
- `field1, field2`：您将要查询的字段

这将有助于在自定义安装包时“填空”。

##### 连接数据库

为了连接到数据库，您需要向新的数据库对象传递正确的数据源名称 (DSN)。语法如下：

```php
<?php
require_once("db.php");
$dsn = "mysql://username:password@localhost/testdatabase";
$db = DB::connect($dsn);
if (PEAR::isError($db)) {
    die($db->getMessage());
}
echo "Connected successfully. Now what?";
?>
```

如您所见，这就是连接所需的全部，更重要的是，它报告了过程中可能发生的任何错误。再次说明，请随意访问官方 PEAR 文档以获取关于连接数据库时可设置的各种选项（如端口号或协议）的详细说明。此文档可在 `http://pear.php.net/manual/en/package.database.db.intro-connect.php` 找到。现在，试着查询想象中的表中想象中的字段。

##### 查询数据库

要查询数据库，您需要传递表名和所需的过滤器，因此输入以下内容：

```php
<?php
require_once("db.php");
$dsn = "mysql://username:password@localhost/testdatabase";

$db = DB::connect($dsn);
if (PEAR::isError($db)) {
    die($db->getMessage());
}

//query
$res =& $db->query('SELECT * FROM testtable');

//display number of rows
echo "There were " . $res->numRows() . " rows found.";

//display one column of results, or by row number
while ($row =& $res->fetchRow()) {
    echo $row[0] . "\n";
}

//display more than one field of results
//also switching Associative mode
while ($res->fetchInto($row, DB_FETCHMODE_ASSOC)) {
    echo $row['field1'] . "," . $row['field2'] . "\n";
}
?>
```

这只是该包的一个示例。您还能用它做很多其他事情，例如获取多个查询的结果集，以及自动准备和执行常用的 SQL 语句。

#### HTML_CSS 和 HTML_Page

这些包允许您动态创建 CSS 样式表，并轻松地将它们集成到新的 HTML 页面中。HTML_Page 还可以为您执行其他功能，但本示例专注于创建新的 CSS 样式表：

```php
<?php
require_once('HTML/CSS.php');
require_once('HTML/Page.php');

$css = new HTML_CSS();

//set the styles
$css->setStyle('body', 'background-color', '#FF00CC');
$css->setStyle('body', 'color', '#ffffff');
$css->setStyle('h1', 'text-align', 'center');
$css->setStyle('h1', 'font', '16pt erdama');
$css->setStyle('p', 'font', '12pt verdana');

//create a new page
$p = new HTML_Page();

$p->setTitle("Testing the CSS");

$p->addStyleDeclaration($css, 'text/css');
$p->addBodyContent('<h1>Wow, this background is really bright!</h1>');
$p->addBodyContent('<p>This should wake you up.</p>');

$p->display();
?>
```

使用简单的 if 或 switch 语句，您可以使用类似上述内容来动态创建样式表，依据可以是个人的授权级别、使用的浏览器或操作系统类型、时间或日期，或者您能想到的任何其他因素。

#### HTML_QuickForm

该包的目的是快速轻松地创建 HTML 表单。它易于使用，但相对功能强大，并允许您进行相当多的自定义。请看看一个快速示例：

```php
<?php
    require_once ("HTML/QuickForm.php");
    
    //create a new form object
    $form = new HTML_QuickForm('firstForm');
    
    //add two input fields; this is completely customizable
    $form->addElement('text', 'name', 'Your full name:', array('size' => 50,
        'maxlength' => 255));
    $form->addElement('text', 'email', 'Your email address:', array('size' => 50,
        'maxlength' => 255));
    
    //add a submit button
    $form->addElement('submit', null, 'Send');
    
    //add validation rules of our choosing
    //using addRule('field_to_be_validated', 'error_message to be displayed',
    // 'validation_type',
    $form->addRule('name', 'Empty Name Field', 'required', null, 'client');
    $form->addRule('email', 'Empty Email Address', 'required', null, 'client');
    $form->addRule('email', 'Incorrect Format for Email Address', 'email', null,
        'client');
    
    //check to make sure input followed all our rules
    //if so, put all form elements into an array for us
    //for sake of example, let's print the values
    if ($form->validate()) {
        $elements=$form->exportValues();
        print_r ($elements);
        exit;
    }
    
    //show the form
    $form->display();
?>
```

通过这个小程序，您已创建一个用户表单，验证了必填字段（以及电子邮件字段），并将输入收集到一个整洁的小数组中供您使用。您可以设置任意数量的规则，以确保脚本验证必填字段是否已输入，格式是否正确（数字、字母等），并且如您前面所见，还可以检查诸如正确格式的电子邮件字段等项。您还可以设置默认值以及您能在表单中实现的其他任何功能（如上传文件和使用图像作为“提交”按钮）。

#### HTML Table

您可以使用此包轻松输出数据表，数据来源可以是数据库查询结果集中的数据，或者是仅存放在某个数组中等待您释放的数据。快速看看一个示例，以了解这个包是多么易用：

```php
<?php

require_once ("HTML/Table.php");

//set up attributes for our table, using common HTML attributes as
//array keys and their values as array values
$attributes = array("width" => "50%", "border" => "1");

//create a new table object
$table = new HTML_Table($attributes);

//configure table
//AutoGrow is for an unknown number of rows
//AutoFill inserts text for every empty cell
//Because we are pretending not to be sure how big our table will be, we
//will set this option to true.
$table -> setAutoGrow(true);
$table -> setAutoFill("-");


//get some data for our table
$rows = array(
	'0' => array("Number One", "Number Two", "Number Three"),
	'1' => array("Numero Uno", "Numero Dos", "Numero Tres"),
);

//populate the table
for($nr = 0; $nr < count($rows); $nr++) {
	//the header row comes first
	$table -> setHeaderContents( $nr+1, 0, (string)$nr);
	for($i = 0; $i < 3; $i++) {
		if("" != $rows[$nr][$i])
		//the cell contents come next
		$table -> setCellContents( $nr+1, $i+1, $rows[$nr][$i]);
	}
}

//set background for every other row
//skip the first row so we use a value of 1 to start
$altRow = array("bgcolor"=>"#FFFCCC");
$table -> altRowAttributes(1, null, $altRow);

//set header info for each cell of the table
//based on coordinates, 0,0 is top left cell.
//the third value is the contents to be shown
$table -> setHeaderContents(0, 0, " ");
$table -> setHeaderContents(0, 1, "Field 1");
$table -> setHeaderContents(0, 2, "Field 2");
$table -> setHeaderContents(0, 3, "Field 3");

//set attributes for the header rows and first column
//first row and column = 0 .
$ShrAttrs = array("bgcolor" => "#FFF6AD");
$table -> setRowAttributes(0, $ShrAttrs, true);
$table -> setColAttributes(0, $ShrAttrs);

//send it to the browser
echo $table -> toRTML();

?>
```

您可以想象，根据用户输入或数据库结果创建表格是多么容易，以及通过改变这里那里的几个变量所能实现的自定义程度。

#### 还有其他什么？

请浏览完整的 PEAR 包列表（可在 http://pear.php.net/packages.php 找到），您将会开始欣赏 PEAR 社区的广度与深度。可用的优秀包如此之多，本书篇幅有限，无法涵盖所有内容。为了简要列出除本章讨论过的之外更实用的主题，这里提供一些列举：

- 基准测试
- 缓存
- 配置
- 加密
- 事件
- 文件格式
- 文件系统
- Gtk 组件
- HTTP
- 图像
- 国际化
- 日志记录




- 邮件
- 数学
- 网络
- 数字
- 支付
- 流
- 系统
- 文本
- 工具和实用程序
- 验证
- Web 服务
- XML

### 探索 PECL

虽然 PECL 没有 PEAR 那么庞大，但这并不意味着它没有价值。与 PEAR 相比，可用包的文档和功能范围更为有限。许多 PECL 包仍处于测试阶段，属于实验性质；因此，使用这些包可能需要一些适应过程。然而，PECL 中确实包含一些非常有用且有时是特定用途的包，我们将简要查看其中一些更受欢迎的包，以让您了解它们包含的内容。如果您希望获得关于 PECL 包的更详细解释，我们在第 10 章中已经对 PDFLib 进行了说明。

#### Fileinfo

Fileinfo PECL 包是 PECL 站点上的热门下载之一，并且其实用性极高。借助此扩展，您可以获取文件的各种信息，例如 *MIME* 类型。此包可以从 http://pecl.php.net/Fileinfo 下载。

此包的文档相对有限，这与许多 PECL 包的情况相同；不过，PHP Wiki（http://www.wiki.cc/php/Fileinfo）上有一篇简短的 Wiki 文档提及了此包。

#### PDO

截至本文撰写时，PDO 仍处于测试阶段，被视为实验性功能，但它对 PHP 未来在数据库交互方面的发展具有巨大潜力。此包的目的是与 Data Objects 进行交互，并允许您轻而易举地更改数据库类型。无需使用特定于数据库的函数（例如 *mysql*_*connect* 或 *pg*_*connect*）进行编码，您可以创建一个新的 PDO 对象，它会为您处理这些事项。然后，只需在对象实例化期间更改一个参数，即可从 *MySQL* 切换到 Postgres（或许多其他数据库）。您可以从 http://pecl.php.net/package/PDO 下载 PDO。

随着 PDO 影响的扩大，其文档也在增加。PHP 手册（http://us3.php.net/manual/en/ref_pdo.php）中有关于此扩展的文档，此外在前文提到的 PHP Wiki（http://www.wiki.cc/php/PDO_Basics）上也有相关内容。

#### Xdebug

这是另一个热门的 PECL 下载，可在 http://pecl.php.net/package/Xdebug 获取。其功能是通过提供有关代码、激活、执行和变量值的信息，协助 PHP 开发人员调试脚本。它还提供内存分配和保护，防止无限循环，以及堆栈和函数跟踪。

此包的文档比其他包更为详尽；它甚至拥有自己的网站 http://www.xdebug.org。

### 摘要

至此，您应该已经做好了深入研究 PEAR 和 PECL 的准备，并且能够停止反复编写和重写相同的代码。一旦您熟悉了 PEAR 和 PECL 的设置，也许您会将一些已编写的代码贡献出来，加入那些备受推崇的贡献者行列，将其作为新包分享给大众。

## 代码效率

您提供页面的速度越快，您的网站就越能在不造成用户延迟的情况下处理更多业务。本章介绍了提高网站性能的方法，以及如何确定哪些方法可能最有效。

“在更短的时间内提供更多内容”是其中的基本原理。正如有些汽车爱好者会在每一个空闲时刻深入汽车的内部，试图将四分之一英里的时间再缩短零点一秒一样，也有网站开发人员想要将登录页面的显示时间再缩短一毫秒。事情可以做得过头！

您不希望把时间浪费在无人会察觉的改进上，因此本章的第一部分将介绍几个小案例，用以说明即使巨大的改进有时也可能带来微乎其微的差异，微小的改进又能带来多大的区别，以及在动手修改之前了解整个系统的重要性。

您的程序运行在 PHP 上，PHP 运行在您的 Web 服务器上，并与您的 DBMS 通信，而这两者都运行在您的操作系统上，操作系统又运行在物理硬件上。后续部分将审视所有这些层面，寻找改进机会并确定需要改进之处。

最后，这里还将介绍一些微小的杂项代码调整，它们可能为登录页面节省一毫秒时间。之所以在此提出，是因为如果您从一开始就了解并使用这些技巧，日后就不会因诱惑而花费时间去修改现有代码以引入这些技巧，从而浪费时间本应用于其他更有价值的地方。

### 为什么要这么做？

首先要问自己的问题是“我*需要*做什么吗？”如果您还没有开始编码，那么答案显然是“是的”——花点时间规划您的程序应该做什么，并尝试感知其性能可能拖慢的地方。但如果您有一个正在运行的网站，并且您很想通过调整使其运行得更快，请问自己这样做是否真的值得费这个劲。它是否运行得太慢，不合您的心意？是哪一部分？您的调整会使其变快吗？快多少？而且您确定在这个过程中不会弄坏什么东西吗？通过考虑这些问题，您可以避免在毫无收益的事情上浪费大量时间和精力，如果运气好，还能发现一个微小更改就能带来巨大的性能提升。

### 以小事获大益

在我曾经工作过的一个公司，有一台用于生成报告的计算机。软件是 Windows NT4 和 Microsoft Access 97（那是 2004 年），安装的内存为 32MB，打印报告简直是一场耐心的考验。当它重复显示屏幕时，您可以去喝杯咖啡。有人提议升级一台新电脑，因为它“太慢了”。

“简单”的答案——无需分析即可得出的结论——将是用最新版本的 Windows 和 Access 替换现有机器，然后设置网络用户账户，并花一天时间应对此类升级似乎不可避免的火情（故障）。但随后进行了一次分析，方法是按 Ctrl-Alt-Delete 调出 NT 的任务管理器及其进程列表，查看当计算机被用于生成报告时每个进程花费了多少时间。（如果您不熟悉 Windows 中的此过程，可以想象一个使用 GUI 表格控件的简化版 top(1) 命令。）

列表中引人注目的条目是“System Idle Process”（系统空闲进程）。该条目从未低于 85%。在 20 分钟的操作中，处理器实际上只有三分钟是在执行任务；其余时间它都在等待内存（RAM）和磁盘之间的交换。如果*不是*受到其可怜的 32MB RAM 的拖累，这台计算机的运行速度可以比现在快六倍以上。256MB 就足以消除瓶颈；报告的生成时间将短于走到打印机的时间；芯片比新机器和新软件许可证便宜得多；而且，安装过程不会损失一整天，停机时间将只有大约五分钟。

### 以小博大的误区

在 C 语言中，一个常见的习惯是用 `a<<3` 代替 `a*8` 来将一个变量乘以 8。这当然有效，因为在二进制中，乘以 8（或 2）等同于将所有位向左移动 3 位（因为 3=lg(8)）。这可以应用于 PHP 吗？简短回答是肯定的。但正如在 C 语言中一样，节省的时间是以纳秒计的。例如，在我 2.6 GHz 的 P4 处理器上，PHP 5.0.3 的差异是 50ns，而 4.3.11 是 3.3ns，版本间唯一的显著差异在于位移的速度。您的结果可能有所不同。顺便说一句，`8*$a` 比 `$a*8` 更快。

在需要定期执行数百万次此类乘法的环境中（频率高到现代 C 编译器都能自行识别 `a*8` 并将其转换为 `a<<3`，*无论如何*如此），追求这样的节省是有意义的，但这并非基于 Web 的应用程序的典型情况。更重要的是，在 PHP 中，这两个“等价”操作在极端情况下具有不同的行为：位移总是产生整数结果（结果可能为 0 甚至为负：1073741824<<1=-2147483648 且 -2147483648<<1=0），而乘法在必要时会返回双精度浮点数以容纳结果（1073741824*2=2147483648 且 2147483648*2=4294967296）。此外，请记住，虽然*乘法*的优先级高于加法，但位移的优先级*更低*：表达式是 `$a+$b*8`，而非 `$a+$b<<3`。





这一切值得吗？将操作写成乘法需要多长时间，写成位移又需要多长时间？验证你所写内容的正确性需要多久？修复因极端情况下的不同行为或忘记优先级差异等问题而产生的 bug 需要多长时间？未来修改代码（例如，将乘以 8 改为乘以 9）又需要多少时间呢？（你不能只搜索 8 的实例；你还必须搜索 3 的实例，而且你为什么没有使用命名常量？）该操作需要执行多少次，才能节省下与你花费确保使用更快选项的时间相同的成本——这里一纳秒，那里一纳秒？而在该操作被执行那么多次之前，还要经过多长时间？

关键在于**你的**时间比**计算机的**时间更有价值。比你的时间更有价值的在线时间是访问你网站的访客的时间。因此，不要浪费时间试图从页面处理时间中省下一纳秒：即使是在异常高负荷使用下，网站访客也察觉不到这种差异。

### 比较字符串速度 —— 基准测试示例

PHP 提供了多种方式组合字符串字面量和变量，以及三种引用字符串的方法。这三种引用方法是使用单引号、双引号以及 heredoc 语法。将变量插入字符串可以通过使用连接运算符、双引号或 heredoc 字符串中的变量插值，以及 C 风格的字符串格式化函数来实现。时不时地，会有好奇的程序员询问哪种方法更“好”。“好”的定义方式不止一种：它更快吗？它使源代码更易读吗？它更简单且更少出错吗？就可读性和简洁性而言，争论双方旗鼓相当：如果其中一种方法*明显*优于其他方法，那么自然选择会让大型应用程序中的资深开发人员 exclusively 使用这种优越方法。多年来，似乎没有发生这种选择，这表明差异并不足以出现在行业范围内的最佳实践文档或编码标准中。

单引号字符串是否*比*双引号字符串*更快*，则更容易量化。如果你被迫给出肯定或否定的答案，那么最安全的说法是“是”，但现实中事情比这复杂得多。

就像关于现实世界的任何问题一样，不先获取一些事实就无法回答。作为一个初步实验，你可以编写以下内容：

```php
$variable = 'string';

$start = microtime(true);
for($i=0; $i<1000000; ++$i) {
    $string = "this string has a $variable embedded into it";
}
$elapsed = microtime(true);
for($i=0; $i<1000000; ++$i) {
    $string = "this string has a "."$variable." inserted into it";
}
$finish = microtime(true);

echo "Variable interpolation required ",$finish-$start," seconds for one million iterations.\n";
echo "Variable concatenation required ",$finish-$1sttime," seconds for one million iterations.\n";
```

第一次运行此脚本时，我得到的插值和连接时间分别为 6.81 秒和 1.72 秒。然而第二次运行，时间却为 6.58 秒和 1.71 秒。这种变异性是由于我运行的计算机不仅仅是在运行该脚本。它还有其他时间需求，而这些其他需求所花费的时间也被计入该脚本完成所需的时间。当脚本第一次运行时，操作系统必须为 PHP、脚本及其数据组织内存空间，其中一些组织是在脚本运行期间发生的（然而，大部分组织会在脚本开始执行之前完成，因此不会体现在计时中）。但紧随其后的第二次运行，环境里已经有一个合适的空闲空间块，因此启动速度要快得多。

结果是你不能只信任一次运行的结果；计时波动的方式太多了，其中许多是你无法控制的。需要的是运行该脚本——从头到尾——多次，并取结果的平均值。对于插值，10 次运行的时间在 6.57 到 6.86 秒之间，平均为 6.77 秒；而对于连接，范围在 1.65 到 1.71 秒之间，平均为 1.70 秒。如果你愿意，可以对数据施加更多的统计火力，但似乎很明显，连接比插值快大约四倍。

但这还不是全部。如果时间取决于字符串的长度，或者被连接或插值的变量数量呢？难道我们不应该测试这些方面的变化吗？

以下是一个用于运行此类测试的命令行 PHP 程序。它不是测量连接或插值变量时的时间本身，而是写入一个单独的 PHP 脚本，然后通过命令行调用它，从而不仅测量脚本本身的时间，还包括启动 PHP、加载脚本和关闭所花费的时间。它对一系列初始字符串大小（64 到 26176 个字符，步长为 512）和插值/连接数量（0 到 100）执行此操作。每个实验执行五次，并将平均运行时间写入单个日志文件。如果两万五千个独立实验太多了（可能需要大约四个小时），那么可以根据喜好缩小范围，但应保持对每个大小/数量组合的多次测试并取平均值。如代码所示，它测量的是变量插值——取消注释第 59 行并注释掉第 58 行（即 str_replace() 调用）将其改为测量连接：

```php
<?php
function generate_test($string)
{
    $code = '<?php
$interpolated="badgers!";

for($i=0; $i<100; ++$i)
    $string = "".$string."";
?>';
    $temp_file = tempnam('', 'xx_test');
    $fp = fopen($temp_file, 'wb');
    fwrite($fp, $code);
    fclose($fp);
    return $temp_file;
}

function run($file)
{
    $average_runtime = 0;
    for($runs=0; $runs<5; ++$runs)
    {
        $start = microtime(true);
        shell_exec("php -f $file"); // If necessary, supply path information here
        $end = microtime(true);
        $average_runtime += $end-$start;
    }
    return $average_runtime/5;
}

$log = fopen('logfile.txt','wb');
for($string_size=1<<6; $string_size<=26176; $string_size+=512)
{
    $generic_string = str_repeat("wibble splunge!\n", $string_size);
    $real_string_size = 16*$string_size;
    $all_positions = range(0,$real_string_size-1);
    for($num_variable_interpolations=0; $num_variable_interpolations<=100;
        ++$num_variable_interpolations)
    {
        echo $string_size,"\t",$num_variable_interpolations,"\n";
        $string = $generic_string;
        if($num_variable_interpolations==0)
            $positions = array();
        else
            $positions = array_rand($all_positions,$num_variable_interpolations);
        if(count($positions)==1) $positions = array($positions);
        foreach($positions as $position)
        {
            $string = substr($string,0,$position).'${'.substr($string,$position);
        }
        $string = str_replace('${','${interpolated}', $string);
        $string = str_replace('$','*.interpolated.*', $string);
        $file = generate_test($string);
        $runtime = run($file);
        unlink($file);
        fwrite($log,
            $string_size,"\t",$num_variable_interpolations,"\t",$runtime,"\n");
    }
}
fclose($log);
?>
```

从代码中最后一个 `fwrite()` 调用，你可以推断出保存数据的格式：每个实验一行，包含字符串的大小（插入变量之前）、被插入的变量数量以及秒数。然后你可以将此数据读取到你喜欢的数据分析或绘图软件中进行探索。





所得到的时间与字符串长度和变量数量的关系图在拼接（参见图 9.1）和插值（参见图 9.2）之间看起来非常不同。

![](img/ab27c6ac898db1f934d39fa127b14657_229_0.png)
![](img/ab27c6ac898db1f934d39fa127b14657_229_1.png)

在这些图表中，你首先可能看到的是，当在双引号字符串中进行插值时，变量数量几乎无关紧要。有一些迹象表明，当变量数量是 32 的倍数时，处理速度特别慢。由于改变变量数量是在内层循环中完成的，因此在运行时，针对*特定*变量数量的实验是在间隔很宽的时间点进行的，排除了除了一些可疑的外部来源造成的瞬态延迟以外的所有干扰。

当变量数量非常小时，比较这两个图表，首先看到拼接速度*下降*一开始是不寻常的，其次插值速度*急剧上升*。仔细检查后发现，当变量数量为 0 时，双引号字符串和单引号字符串的速度相同，只有当有变量需要插值时，双引号字符串才会变慢。这是因为双引号字符串在程序加载期间，即在词法分析过程中会被扫描变量。这是一次性的开销，甚至可能低于我们最初的预期：单引号字符串和双引号字符串的内容都必须被扫描*无论如何*，以定位转义序列和字符串的实际结尾。唯一的实际区别是，当存在变量时，扫描双引号字符串会连续生成多个标记。

总体而言，两个图表的形状具有显著区别。这种差异可以通过使用“大O 表示法”来形式化，该表示法用于在程序分析中描述算法的“规模”或“速度”，以问题的给定规模来表示。虽然它可以给出精确的技术定义，但只需将 $O(f(n))$ 理解为意味着当 $n$ 变得越来越大时，算法行为的图形“看起来像” $f(n)$ 的图形就足够了。

O(f(n)) 是函数 g(n) 的集合，使得存在正常数 c 和 n₀，对于所有 n≥n₀，有 0≤g(n)≤cf(n)。

在这种情况下，双引号插值的图形不随*v*（即正在插值的变量数量）变化，而仅与*l*（字符串长度）呈线性关系（也就是说，当字符串长度翻倍时，速度减慢一倍）。在大O 表示法中，这将被描述为 O(f)。单引号拼接的图形则更复杂。如果你固定字符串长度，并观察随着变量数量变化的图形单个切片（如图 9.1 中从左侧到峰值顶部边缘所示的切片），它在*v*方面看起来相当线性。固定变量数量并允许字符串长度变化（从峰值向右上延伸的山脊线），其曲线弯曲方式暗示了一条抛物线。总体而言，这两种影响似乎是相乘的，给出大O 描述为 O(*flv*)。

从长远来看，*l* 增长得比 $l^2v$ 慢，事实上，对于具有许多变量的长字符串，插值*比*拼接更快。然而，对于较短的字符串或较少的变量，拼接仍然胜出。

大O 表示法只关注随着问题规模变大，程序在长期中的表现，忽略仅在问题小实例中出现 的因素。请记住，当没有变量参与时，两种方法同样快速（因为两者都由单个字符串组成），但单引号拼接在稍快之后再次变慢，而双引号插值一旦引入单个变量就会急剧变慢，且从未恢复。大O 说*从长远来看*，变量插值比拼接快，但你需要拥有数千字节的字符串和数十个变量才能实际看到这种情况发生。

你可以看到，即使在这个非常简单的例子中，仅考虑两个因素，在寻求“最佳”的最终答案时，也存在大量的细微差别。你甚至可以针对这个相对简单的例子进行更深入的调查，而对于更复杂的问题，在得出结论之前你可能必须这样做。但在这里结束这个例子是一个很好的地方，除了指出在所有记录实验中最慢的时间是 3.7 秒。

# 第 9 章

### 反直觉的结果

与 C 不同，C 被转换为机器代码，这与你实际编写的代码没有太大区别（该语言被描述为“装有宏大妄想的汇编语言”），你的 PHP 程序是由 PHP 引擎模拟的虚拟机运行的。当涉及到性能调优时，这可能会带来困难，因为预测哪些方法有效而哪些无效变得更加困难。这将在稍后详细讨论，但此刻你不妨思考一下以下测试代码的结果：

```php
<?php
$j=0;
$start_test_1 = microtime(true);
for($i=0; $i<1000000; $i++) $j++;
$end_test_1 = microtime(true);

$j=0;
$start_test_2 = microtime(true);
for($i=0; $i<1000000; $i++) ++$j;
$end_test_2 = microtime(true);

$j=0;
$start_test_3 = microtime(true);
for($i=0; $i<1000000; ++$i) $j++;
$end_test_3 = microtime(true);

$j=0;
$start_test_4 = microtime(true);
for($i=0; $i<1000000; ++$i) ++$j;
$end_test_4 = microtime(true);

$test_1 = $end_test_1 - $start_test_1;
$test_2 = $end_test_2 - $start_test_2;
$test_3 = $end_test_3 - $start_test_3;
$test_4 = $end_test_4 - $start_test_4;

echo "Postincrementing I and J one million times: ",
     $test_1, " seconds.\n";
echo "Postincrementing I and preincrementing J one million times: ",
     $test_2, " seconds.\n";
echo "Preincrementing I and postincrementing J one million times: ",
     $test_3, " seconds.\n";
echo "Preincrementing I and J one million times: ",
     $test_4, " seconds.\n";
?>
```

### 基准测试与性能分析

有许多技术和工具用于估算程序速度，在着手加速网站的任何任务之前、期间和之后都应使用这些工具，以免浪费时间做出没有明显差异的更改，或者更糟糕的是，使网站变慢。大致来说，它们可以分为两个主要类别：基准测试是你在进行实验以确定在真正实施之前选择最佳方法时所做的，而*性能分析*涵盖的是你对实际事物进行的实验，以查看其实际表现如何。显然，这两者之间有相当大的重叠；许多技术和工具是相同的（因为工具不一定*关心*你使用的代码是自然的还是合成的）。在操作系统和 PHP 层面都存在工具来辅助你进行这些工作。

#### PEAR Benchmark

你在上一节中已经看过基准测试的例子。它们是临时构建的，但它们共有的基本思想足够通用，以至于值得抽象为一个独立的类：

- 1. 启动计时器（记录当前时间）。
- 2. 做某事。
- 3. 停止计时器（再次记录当前时间）。
- 4. 比较停止时间和开始时间以确定经过的时间。
- 5. 重复步骤 1--4 很多次，累积持续时间。
- 6. 查看结果。

一个明显的增强是给计时器加上标签，以便可以同时启动和停止多个计时器。如果计时器还能包含有关它们在覆盖的代码特定部分所花费时间的信息，那就更好了。PEAR 基准测试类提供了所有这些功能。PEAR 和 PEAR 软件包的安装在第 8 章中介绍；因此，你已处理了这部分，并准备好继续使用它。

要使用 Benchmarking 类重复初始字符串构建实验，你可以编写以下内容：

```php
<?php
require 'Benchmark/Timer.php';
$variable = 'string';
$timer = new Benchmark_Timer();
$timer->start();
for($i=0; $i<1000000; ++$i)
{
    $string = "this string has a $variable embedded into it";
}
$timer->setMarker('lapt ime');
for($i=0; $i<1000000; ++$i)
{
    $string = "this string has a " . $variable ." inserted into it";
}
$timer->setMarker('finish');
echo "Variable interpolation required "$timer->timeElapsed('Start','lapt ime',"
```





# 第 9 章

`一百万次迭代所需的秒数。\n";
echo *需要变量拼接，*Timer->timeLapsed('lap time', 'finish'),*
一百万次迭代所需的秒数。\n";

$timer->stop();
$timer->display();`

Benchmark/Iterate 继承自 Benchmark/Timer，并提供了一个 run() 方法，你可以传入想要测试的函数名称。在选择其中一个时，需要注意两件事。一是调用函数本身需要花费一点时间。二是 Benchmark/Iterate 会保留每个独立实验的计时数据。进行大量实验意味着需要一个大数组，这就是为什么下面的代码只运行一万次实验而不是一百万次：

`<?php

require 'Benchmark/Iterate.php';

$variable = 'string';

function interpolate($variable)
{
    $string = "this string has a $variable embedded into it";
}

function concatenate($variable)
{
    $string = "this string has a ". $variable." inserted into it";
}

$interpolation_benchmark = new Benchmark_Iterate;
$concatenation_benchmark = new Benchmark_Iterate;

$interpolation_benchmark->run(10000, 'interpolate', 'string');
$concatenation_benchmark->run(10000, 'concatenate', 'string');

$interpolation_result = $interpolation_benchmark->get();
$concatenation_result = $concatenation_benchmark->get();
?>`

这两个结果变量是数组：$interpolation_result['iterations'] 记录测试运行的次数，而 $interpolation_result['mean'] 记录平均值（如果系统可用，Benchmark 类会使用 benchm 函数在计算该值时保持精度）。取消这两个元素的设置后，你会得到一个包含每次迭代所有单独耗时的数值索引数组，以便你可以执行你认为相关的其他统计测试。

#### top 和 ab

之前提到的 NT4/Access 报告生成器轶事来自 Windows 世界，并提到了其任务管理器的使用。随 Unix 类型操作系统提供的进程监控工具名为 top，它提供的信息丰富得多。与此同时，Apache 发行版包含了 ab ApacheBench 程序，它可以测试你网站的尖端性能：你究竟能以多快的速度提供内容？并排使用这两者通常很有启发性：使用 `ab` 查看你的性能表现，使用 `top` 查看为了获得该性能投入了多少努力。

当然，你需要在 Web 服务器本身上运行 `top`，`ab` 可以在同一位置运行，但出于公平起见，值得从局域网上的另一台机器运行它（如果在比局域网更远的地方运行，会引入额外的延迟，阻碍你尝试对服务器进行压力测试）。例如，你可以在工作站上打开一个终端窗口并 `ssh` 到 Web 服务器，在工作站上运行 `ab`，在服务器上运行 `top`，让两个终端窗口并排显示。

简而言之，`ab` 是一个处于高速状态的 http 客户端。典型的调用方式是连续请求同一页面一千次，从而模拟一千个用户几乎同时访问它。它收集有关服务器响应这些请求所花费时间的统计数据，以及是否有请求未能满足。看看这个例子：

```
ab -n1000 -c10 http://bowman/page2test.php
```

这个命令告诉 `ab` 总共请求 `page2test.php` 一千次，最多有十个请求并发运行。因此，它发出十个请求，一旦其中一个得到满足并接收到响应，它就开始第十一个，直到达到总数才停止。

在完成一千次请求后，它会呈现一份统计报告。这些统计包括总运行时间、响应大小、发出的请求数量及失败的请求数量、请求发送的速度（对应于请求被满足的速率）、响应本身以 bps 为单位的提供服务速度，以及平均和最慢响应所需的时间。

对于基准测试而言，调整总请求参数 `-n` 并不那么重要；这只需要至少等于 `-c`，并且足够大以便总体统计数据得以平滑，没有测试开始时的瞬态行为干扰结果。调整并发参数 `-c` 更具信息量。从 `-c1` 开始（除非你真的想坐等那么久，否则你设置的 `-c` 越低，`-n` 也可以设置得越低），你可以查看服务器是否一次只能响应一个请求。随着你增加 `-c`，并发请求的数量增加，你可以观察服务器是否能处理不断增加的负载。作为一个例子，随桌面版 Microsoft Windows 提供的 IIS 版本被限制为最多 10 个并发请求。一旦 `-c` 超过 10，你开始得到失败的请求。是的，你可以使用 ApacheBenchmark 测试其他服务器；从某种意义上说，它被称为 "Apache" 是因为它是 Apache Group 的产品。随着负载增加，传输速率会下降，请求发送的速率会增加，最终请求开始失败。如果你感到幸灾乐祸，你可以模拟被 Slashdot 攻击：用 `n_100000_c1000` 攻击你的服务器，并看着它出问题。

与此同时，在另一个终端窗口中是服务器对正在发生的事情的看法。当你运行 `top` 时，首先要看的是负载平均值。给出的三个数字分别是过去一分钟、5 分钟和 15 分钟内活动的进程（即正在运行或等待运行的进程，相对于当前空闲的进程）的平均数量。如果把服务器想象成银行，处理器想象成柜员，进程想象成人，那么负载平均值就代表了正在被服务或排队的人的数量。显然，如果柜员不够，就会有很多越来越不耐烦的人。同样，过高的负载平均值意味着进程花费了太多时间排队等待运行机会。因此，发起这些进程的请求的人也在等待结果，他们或他们的浏览器甚至可能会放弃——这对于你的网站来说不是一个好迹象。

理想情况下，你希望负载平均值略低于服务器的处理器数量，保留一些余量以处理异常重的负载。短暂的激增是可以容忍的，但前提是它们是短暂的。15 分钟的负载根本不应该激增；如果发生了，则表明当服务器忙碌时它太忙了，并且正在形成需要很长时间才能处理完毕的积压。足以显著影响 15 分钟平均值的尖峰无法快速解决。

在 top 的显示中，负载平均值下方是每个处理器的活动级别，以百分比给出。这也应该保持相当低，以应对 Slashdot 效应或最新蠕虫病毒的攻击尝试。如果机器是专用 Web 服务器，那么在没有任何内容提供服务时处理器出现显著活动可能表明它正在做不应该做的事情。检查进程列表本身，看看哪些进程正在使用处理器。你可能可以移除其中一些。仅仅提供静态网页或文件的站点几乎不会经历任何 CPU 负载——20 世纪 80 年代的处理器完全有能力以磁盘读取数据的速度传输数据——但动态生成的页面确实会在这一点上经历瓶颈。

另一方面，即使 CPU 几乎处于空闲状态，服务器也可能已满负荷运行。回想一下 Windows 报告生成器的事件，当时简单的任务花费了很长时间，而处理器 85% 的时间都在原地踏步，并确定问题在于机器中的 RAM 太少。

在 top 的 CPU 使用率报告下方，是关于可用内存数量、已用内存数量以及 RAM 和交换文件中剩余空闲内存数量的报告。你希望尽可能少地依赖交换文件，理想情况下完全不用。

#### 硬件改进

那么，你决定网站运行缓慢。你分析了正在发生的事情，现在准备好着手改进状况。最深刻的改进可能来自于记住你的服务器存在于现实世界中，并受物理定律的约束。你无法改变物理定律；你只能适应它们。

首先要查看的是你与外部世界的连接。你需要那里有一根足够大的管道。如果你的服务器负载较轻但网络流量已达到最大值，那么你的连接就是瓶颈。

解决那个问题后，检查处理器。如果它持续在其范围的上限运行，那么升级可能会给你带来更多的喘息空间。你的机器有多久了？两年？你可能会发现新机器比当前机器快两倍多。当然，更换电脑是你能够做出的最根本、充满风险且几乎肯定昂贵的改变。如果可以的话，只需把新机器搬进来，将电缆从旧机器移到新机器，进行硬盘移植，然后启动即可。但事情似乎从来不会那么简单。

如果处理器相当空闲，但内存紧张，那么增加 RAM 是你的下一个优先事项。除了流量最大或数据库最大的站点外，512MB 对于所有站点来说都绰绰有余，这些站点的数据库通常由 MySQL 缓存在 RAM 中以提高访问速度。

对于主要提供静态页面或文件的站点，RAM 比处理器速度更重要——将数据块从机器的一部分移动到另一部分非常简单，因此能够快速计算如何移动它并不像能够一次性移动大量数据那样重要。





磁盘访问是一个相对缓慢的过程。请考虑升级为具有更高吞吐量的更快硬盘。如果当前硬盘容量即将用尽，请考虑添加额外硬盘，而非将所有内容迁移到更大的单一硬盘中。即使*你尚未*接近当前硬盘的容量上限，获取额外硬盘并将内容分布在这些硬盘上也能改善访问时间。多个磁盘的读写磁头将同时运作，且不需要像单个大容量硬盘的磁头那样移动那么远的距离。磁盘的转速需求也相应降低。

#### Web 服务器优化

就其本质而言，Apache 高度可配置，拥有许多可用于优化其行为某一侧面的设置。有些设置能减少 Apache 所需的内存，而另一些则旨在减少每个进程执行的工作量。

启动 Apache 时，它首先会启动半打（确切数字当然可配置）`httpd` 实例。这些进程负责实际处理 HTTP 请求。服务器本身所做的全部工作就是管理这些子进程，根据需要启动新进程或停止现有进程。每个实例大约消耗 1MB RAM（很难给出更精确的数值，但这是一个合理的经验值），然后静待请求。如果请求数量超过现有实例数，系统将启动新实例；若后续活动减弱，则多余的实例将被关闭。偶尔，即使有足够的工作负荷，某个 `httpd` 实例也会被关闭。这允许操作系统回收可能从 `httpd` 进程本身或其使用的任何模块中泄漏的内存。当然，`httpd` 进程也可能单纯崩溃，此时该特定请求将失败，但另有一个实例待命，以防请求重试。这是 Apache 以这种方式运行的关键原因：它使服务器在崩溃后仍能继续运行。

控制此行为的配置选项位于 `httpd.conf` 中，或可添加到该文件：

- `MaxClients`：这是你准备好在任何单一时刻支持的最大 `httpd` 进程数，即并发处理的最大客户端请求数。考虑到每进程 1MB 的经验值，将此值设置得高于你的 RAM 容量没有意义。事实上，你会在此之前耗尽 RAM。它们仍会继续工作，但将依赖慢得多的虚拟内存，导致磁盘与 RAM 之间发生大量烦人的交换。
  - 也不希望此设置过低；如果请求数量超过此数值，部分请求将被遗漏，并等待其他请求完成。如果延迟过长，客户端将放弃，请求将被报告为失败。
- `MaxRequestsPerChild`：当 `httpd` 实例服务达到此数量的请求后，无论当前服务器负载如何，它都会被关闭，以防服务器或已安装模块中存在未修复的内存泄漏，导致实例因内存膨胀而失败。由于操作系统无法意识到这种大小增加是不必要的，Apache 必须介入以任意方式关闭进程。此指令控制该事件发生的频率。除非你使用的是有 bug 的实验性或开发中的模块，否则将此限制设置为 100,000 不会产生负面影响。使用 `top` 监控每个 `httpd` 进程的 RAM 消耗；如果它们似乎不受控制地增长，请将限制降低 10 倍。继续监控并在必要时降低。同时关注整个系统的行为，因为如果此数值降得过低，将花费太多时间用于启动和停止子请求，此时你需要尝试找出导致问题的模块。

# 第 9 章

- **StartServers** 和 **MinSpareServers**：StartServers 指定启动 Apache 时初始化的 httpd 实例数。一个合适的数值是你网站通常处理的并发请求数。MinSpareServers 则为此数值再加上几个。由于启动新实例涉及工作开销，你不希望服务器在处理请求全速运行时启动新实例，因此保持一些空闲是有益的。

当收到网页请求时，通常随后会有来自同一客户端的其他资源（样式表、内联图像等）的额外请求，以及可能的后续页面请求。在期间保持客户端与服务器之间的连接是有意义的，以避免在几毫秒后立即向同一客户端打开新连接而造成的浪费，并发现有一个 httpd 实例准备接受请求（这通常就是处理上一个连接且现在处于空闲状态的那个实例）。现代 HTTP 1.1 标准提供了此选项——称为“Keep_Alive”——现代版本的 Apache 默认遵循此选项（如常），具体取决于 Apache 配置文件中的设置。

- **KeepAlive**：默认为 On，你通常没有理由将其关闭。
- **MaxKeepAliveRequests**：一旦客户端与服务器之间建立连接，处理该连接的 httpd 实例将最多为此客户端处理此数量的请求。这可以设置得相当高——约 100。很少有页面请求后跟随一百个附加请求的情况，但确实可能发生：用户从加载的第一个页面开始，可能迅速打开半打其他页面。将此选项设置得很高不会造成太多麻烦，因为客户端通常从自身关闭连接；在未关闭的情况下，以下配置指令生效。
- **KeepAliveTimeout**：如果当前连接在此秒数内没有来自客户端的请求，服务器将假设客户端因任何原因离开而未正确关闭连接。你网站与客户端之间的带宽越高，此数值可以越低。拨号用户的带宽是瓶颈，降低了请求发送速率，因此连续请求之间可能有 30–45 秒。此数值的下限约为 10–15 秒。

为了记录流量，Apache 可以使用反向 DNS 查找请求来源 IP 的主机名。这使日志更易于人工阅读，但这已是其全部作用。与此同时，请求正在等待 DNS 服务器的响应，在收到响应之前无法继续。最好仅在日志文件中存储 IP 本身，将查找工作留给如 Apache 的 logresolve 工具等，在你真正需要时进行。

- **HostnameLookups**。此设置决定是在服务器日志中记录主机名（On）还是 IP 地址（Off）。

与此相关的是，你在允许或拒绝连接时使用域名还是 IP。同样，在你的 .htaccess 文件中使用 `allow from .example.com` 或 `deny from .example.com` 意味着必须执行反向 DNS 以查找来源 IP 所属的域名（然后执行正向 DNS 查找以确认该 IP 确实属于所声称的域名）。因此，允许或拒绝特定 IP 地址范围而非域名更为有效。但请记住，DNS 的一半意义在于特定域名并非永久绑定到特定 IP 地址，名称可以迁移到其他主机和其他 IP 地址。

谈到 .htaccess，当 Apache 被要求读取文件时，它将检查文件系统路径（而非 URL 描述的路径）中每个目录的 .htaccess，直至并包括系统根目录。如果路径较长，则涉及大量查找，因此保持路径较短有帮助。如果（你无疑如此）将整个网站存储在单一文档树中，而非散布在系统各处，那么让 Apache 搜索高于该树根目录没有意义。access.conf 文件提供手段来告知 Apache 此情况。首先，声明在系统根目录向下不允许任何 .htaccess 文件覆盖设置，然后声明在网站的文档树中可以尊重 .htaccess 文件：

```apache
<Directory />
    AllowOverride None
</Directory>
<Directory /www/siteroot>
    AllowOverride All
</Directory>
```

如果你根本不使用 .htaccess 文件，请说明此情况，Apache 将不会浪费时间查找：

```apache
<Directory /www/siteroot>
    AllowOverride None
</Directory>
```

mod_gzip 是一个可以加速输出过程的 Apache 模块。如今大多数浏览器内置 gzip 库，并能[解]压 gzip 压缩数据在接收时。此类浏览器将在其请求头中包含此效果的声明。作为回报，安装了 mod_gzip 的 Apache 将发送压缩响应。压缩/解压步骤引入了延迟，但对于高可压缩文档（英文文本压缩率约 30%，HTML 约 60%），带宽节省不容忽视。

否则，移除所有实际不使用的模块。例如，如果你不使用 .htaccess 文件，则禁用 mod_access。PHP 扩展及其调用的库同理；如果不使用 SimpleXML 扩展，请禁用它。

#### PHP 优化

一旦优化了硬件、数据库和 Apache，你就可以专注于调整实际代码。此时你能为自己做的最佳准备是选择并坚持一致的编码标准。你花在解读所写代码上的时间越少，花在查找其他提高效率技巧上的时间就越多。

##### 编码标准

你网站的访客优先。你的工作是投入精力，尽可能快速地向他们提供所需信息。另一方面，你的时间比计算机更有价值——实际上更昂贵——。

如果你能以额外 1 毫秒的处理时间为代价节省 5 分钟的工作，这是一项良好的投资，即使在页面处理完成后仍将继续产生回报





# 第 9 章

三十万次。你可以把那五分钟投入到更有价值的事情上，比如看看是否有办法在处理页面时节省*二十*毫秒。这不仅仅是关于能否尽可能快地满足用户请求——考虑到服务器与浏览器之间所有潜在的延迟可能性，更快的速度可能并非决定性因素。（如果你有一个极其繁忙的网站，但即便如此，如前文所述，你的瓶颈很可能在别处。）关键在于，如果你能让现有页面运行得更快，你就可以开始思考该页面还能为你的网站受众做些什么。

但你如何实现这种工作量的转移？如果仅仅把更多任务交给计算机，而你自己并未因此减轻任何负担，那是远远不够的。节省编程时间的一个关键方法是编写代码时，尽量让阅读代码变得轻松便捷。

现在，很少有议题比诸如缩进多少、哪些部分需要缩进、大括号应该放在哪里，以及`else`是否应与相邻的大括号写在同一行（例如：`} else {`）这类问题更容易引发激烈争论。事情可能会变得很难看。即使你最终决定了这些问题，你仍然需要决定诸如变量、函数、对象和类的命名约定；是将方法声明为*protected static* 还是 *static protected*（如果你需要进行查找和替换，这一点至关重要）；是声明`global $foo;`、使用`SCLOVALS['foo']`（或`$GLOBALS['foo']`），还是彻底禁止使用全局用户变量；以及注释放在哪里、注释中写什么；更不用说其他实质性议题，例如代码如何分割到不同的文件中。

避免使用“代码美化器”——*这类程序接收一个源代码文件，并根据某套标准重新格式化后返回。至少，不要依赖它们。你的代码一开始就应该是优美的；否则，你就没有理解制定标准的意义。如果你有一些旧代码或来自其他地方、标准不同的代码，希望将其与你自己的标准保持一致，或者希望你的代码符合他人的标准，可以使用它们。但不要指望愉快地敲出一堆乱麻，然后指望事后用美化器把它变漂亮。*

##### PEAR 编码标准

厘清至少部分混乱的一种方法是采用现有的风格指南。虽然你可以采用为语法相似语言（如 C、C++ 或 Java）开发的指南，但契合度可能并不理想。例如，你的变量命名方式与函数命名方式并不一定需要截然分开；前者已经通过$号加以区分了。相反，你可以采用特定的 PHP 标准，其中最广泛采用的标准是 PEAR 手册第 4 章中描述的标准。

除非你正在构建一个由公众提交代码的库（就像 PEAR 本身那样），否则完全照搬 PEAR 风格可能并不合适。例如，PEAR 风格要求每个源文件以一个注释块开头，其中说明作者、许可证等事项。对于一个不会分发的大型内部应用程序，分发许可毫无意义，也没必要在每个文件中列出所有开发人员。然而，PEAR 标准可以作为一个起点。

##### 大括号与缩进

关于大括号应该放在哪里的争论旷日持久且没有定论，以至于至少有一种语言（Python）特意设计来避免使用大括号。Eric S. Raymond 在《Jargon File》（4.4.7 版）中，“缩进风格”条目下列出了四种风格，以下将介绍这些风格及其名称，并附加几种其他风格。

## 代码效率

- **K&R 风格**——如 C 语言的设计者及权威参考书作者 Kernighan 和 Ritchie 所使用——也被称为“唯一正确的大括号”风格：

```php
for($i=0; $i<100; $i++) {
    if($foo[$i]!=0) {
        //… .etc.
    }
}
```

- **Allman 或 BSD 风格**：大量的 BSD 内核源代码由 Eric Allman 编写，他在工作中使用了这种风格：

```php
for($i=0; $i<100; $i++) {
    if($foo[$i]!=0) {
        //... .etc.
    }
}
```

- **Whitesmith 风格**得名于一家商业 C 编译器，该编译器以这种方式格式化代码：

```php
for($i=0; $i<100; $i++)
{
    if($foo[$i]!=0)
    ... .etc.
}
```

- **GNU 风格**被自由软件基金会使用（几乎 exclusively 仅用于此风格）：

```php
for($i=0; $i<100; $i++) {
    if($foo[$i]!=0)
    { ... .etc. }
}
```

- Allman 风格的一个更紧凑的版本如下：

```php
for($i=0; $i<100; $i++)
{
    if($foo[$i]!=0) { ... .etc. }
}
```

- Allman 风格的一个更紧凑的版本是这个：

```php
for($i=0; $i<100; $i++)
{
    if($foo[$i]!=0) { ... .etc. }
}
```

这六种风格都可以通过选择使用制表符还是空格，或每个缩进层级的宽度来变化。通常，四个或八个空格（或宽度为八个字符的制表符）最为常见，而制表符常不受欢迎，因为不同人使用的制表符宽度不同。任何在一种制表符宽度下看起来正常的空格和制表符混合方式，在另一种宽度下很可能看起来不正常，从而导致所谓的“制表符损坏”，代码行和行片段出现在各种看似随机的缩进位置。

最后一种风格是一个骗局：如果你要对齐开括号和闭括号所在的列，至少应该确保你对齐的是*匹配的*开括号和闭括号对，否则这种对齐只是具有误导性。如果节省行数那么重要，你不如使用 LISP 风格的缩进：

```php
for($i=0; $i<100; $i++)
if{$foo[$i]=0}
{...etc.}
```

PEAR 规定使用 K&R 风格的缩进，每个缩进层使用四个空格，不使用制表符字符。排除制表符字符的原因当然是制表符损坏的影响；但了解制表符损坏的成因可以大大有助于防止它。

制表符损坏发生在你假设制表符具有特定宽度时。以下代码片段使用制表符进行缩进，且编辑器设置为每个制表符等于四个空格：

```c
/**********************
* Big Flashy        *
* Box comment       *
*
* Just Because (TM) *
**********************/
for($i=0; $i<100; $i++)
{
if (($a==$1 || $b=$1)
&&
($c!=$1 || $d!=$1))
{
echo "Either $a or $b is equal to $1, ";
echo "and either $c or $d is not.";
}
}
```

在设置为使用八空格制表符的编辑器中，它会显示为：

```c
/**********************
* Big Flashy        *
* Box comment       *
*
* Just Because (TM) *
**********************/
for($i=0; $i<100; $i++)
{
if (($a==$1 || $b=$1)
&&
($c!=$1 || $d!=$1))
(
  
  echo "Either $a or $b is equal to $i, *";  
  
  echo "and either $c or $d is not.*";  
  
)
```

你首先看到的是，“Big Flashy Box”注释通常弊大于利。它们往往是制表符损坏的最大受害者，这颇具讽刺意味，因为它们本应是专门为人类阅读设计的部分，而机器并不关心格式的细节。

如果你确实想使用制表符进行缩进，那么经验法则是：它们只应用于缩进，任何额外的对齐任务都应使用空格。在上一个例子中，用于将 if 测试的第二行和第三行与第一行对齐的额外制表符——这在四空格制表符下工作良好——在变成八空格制表符后，导致它们被推得太靠右。在制表符之后，本应使用四个空格来匹配“if (“这四个字符，而不是第三个制表符。

通常，源代码中唯一的制表符应位于行首；它们不应紧跟在任何其他字符之后。这两个例外情况是：确实需要字面上的制表符字符，或者你正在使用“紧凑 Allman”风格，在这种情况下，单个制表符用于分隔 `{` 和随后的语句。

你可能注意到，所有描述的风格——排除骗局——都将闭合大括号放在单独的行上。这在代码列表中的效果是在语句块结束和后续代码之间引入一个可见的间隙，在某些方面类似于英文文本中的段落分隔。因此，你可以认为 K&R 或紧凑 Allman 比 Allman“更好”，因为它没有将语句块与其引入结构（如 for、if、switch 等）分开。根据 Raymond 的说法，为 K&R 辩护的主要理由是它在垂直空间上更经济，允许一次在屏幕上显示更多的代码。显然，紧凑 Allman 同时具备这两者优点，同时仍允许匹配的大括号对齐。

##### 减少嵌套层级

如果嵌套大括号的数量过多，识别哪个开大括号与哪个闭大括号配对会变得令人困惑。大多数 IDE 和一些较好的语言敏感文本编辑器能够找到这些配对，而不会被注释或字符串字面量中出现的大括号混淆，但仍然极有可能你需要通过肉眼定位它们（例如，当你漏掉了其中一个时）。阅读代码时，你经常会看到闭大括号后跟随微小的注释，如 `/ * end for * /` 或 `/ * if ($i==0) * /`，试图以此提供帮助。然而，明智地使用 break 和 continue 语句有助于减少嵌套深度。这样做不仅减少了代码向页面右侧偏移的趋势，还减少了带括号块的数量和大小，从而减少了括号的总数，并使每对匹配的括号更靠近，便于快速目视识别。

例如，前面的缩进风格示例是这样编写的：for 循环的主体完全由单个 if 语句组成——如果 if 语句的测试失败，那么在该次循环迭代中什么都不会发生，处理继续到下一次迭代。这样表达后，你可以看出循环的等效实现如下：




# 第 9 章

```php
for ($i=0; $i<100; $i++)
{
  if ($foo [$i] !=0)
    continue;
  //...etc.
}
```

请注意，`if` 语句中的测试条件已被取反，并且循环剩余部分的缩进层级减少了一级。这也可以用于降低测试的复杂性。回想一下前面讨论中的另一个例子：

```php
for ($i=0; $i<100; $i++)
{
  if (($a==$i || $b==$i)
      &&
     ($c!=$i || $d!=$i))
  {
    echo "Either $a or $b is equal to $i, ";
    echo "and either $c or $d is not.";
  }
}
```

你可以立刻看出，这是另一种循环内部只有一个 `if` 语句的情况，因此可以改写为如下形式：

```php
for ($i=0; $i<100; $i++)
{
  if (! (($a==$i || $b==$i) && ($c!=$i || $d!=$i)))
    continue;
  echo "Either $a or $b is equal to $i, ";
  echo "and either $c or $d is not.";
}
```

通过运用一点布尔代数，该测试条件可以简化为：

```php
if (($a!=$i && $b!=$i) || ($c==$i && $d==$i))
```

因此，如果 `$a` 和 `$b` 都不等于 `$i`，或者 `$c` 和 `$d` *都*等于 `$i`，循环将执行 `continue`。但是，如果你先测试 `$a` 和 `$b` 是否都不等于 `$i`，你就可以立即知道是否应该继续执行，而无需继续检查 `$c` 或 `$d`。因此，可以将测试拆分为两个独立的语句：

```php
for ($i=0; $i<100; $i++)
{
  if ($a!=$i && $b!=$i)
    continue;
  if ($c==$i && $d==$i)
    continue;
  echo "Either $a or $b is equal to $i, ";
  echo "and either $c or $d is not.";
}
```

由于 PHP 允许 `continue` 或 `break` 接受一个参数，以表达需要跳过或终止多少层循环，因此在 C 或 Java 中需要使用额外变量来携带嵌套循环中是否应终止循环信息的情况下，或者使用 `goto` 跳转到外层循环后的标签时（除了 Java，因为它没有 `goto` 结构），可以使用简单的 `continue` 或 `break`。你可以这样写：

```text
$position = null;
for($i=0; $i<100; $i++)
{
    for($j=0; $j<100; $j++)
    {
        if($array[$i][$j]==$what_we_wanted)
        {
            $position = array($i,$j);
            break 2;
        }
    }
}
if(null===$position) // $what_we_wanted was not found.
```

而不是这样写：

```text
$position = null;
$found_what_we_wanted = false;
for($i=0; $i<100; $i++)
{
    for($j=0; $j<100; $j++)
    {
        if($array[$i][$j]==$what_we_wanted)
        {
            $position = array($i,$j);
            $found_what_we_wanted = true;
            break;
        }
    }
    if($found_what_we_wanted)
        break;
}
if(null===$position) // $what_we_wanted was not found.
```

关于 `continue` 和 `break` 的最后一点观察是，常见的做法是将这些语句与决定是否执行它们的那个测试条件写在同一行，特别是当这些测试条件简短且简单时。因此，你可能需要考虑采用或允许这种书写方式：

```text
if($a==$1 && $b!=$1) continue;
if($c==$1 && $d==$1) continue;
```

*关于使用相等运算符 `==` 的插曲是，常见的拼写错误是本来想使用 `==` 却误用了 `=`。在某些情况下，你可以保护自已免受由此类误用赋值代替比较所导致的 bug 的影响。当将变量与函数的结果或字面量值进行比较时，如果你将变量放在相等运算符的右侧，误将运算符本身写成 `=` 而不是 `==` 会导致解析错误：`null===$position` 是无效语法。这些错误比那些由本不该发生的赋值和未正确进行的比较所导致的微妙错误更容易调试。*

### 注释

除了 PEAR 强制要求的作者和许可信息外，顶部注释中还可以包含代码功能的概要。如果概要较长，在其前面添加一两行摘要来综合该概要，将有助于后来想要了解该文件用途的开发者。

PEAR 还建议你使用 Javadoc 风格的注释，以便易于转换为文档。在这一点上，与任何其他风格问题一样，观点也是分歧的。反对的一个理由是，由于它们带来的额外格式化，使得注释本身在源代码中更难阅读。另一种观点认为，既然每一个公开可访问的方法都应该以这种方式进行注释，这就鼓励了那些实际上既不构成注释也不构成文档的有效但无意义的注释：

```cpp
/*
 * Gets the number of elements in this Bundle.
 *
 * @return number of elements in this Bundle.
 */
public function Count()
{
    return count($this->elements);
}
```

但注释应有的作用是记录代码的 *意图*。如果代码本身构建良好，它自身就能很好地记录它 *做了什么*。它不会记录的是 *为什么要这样写*。

#### 命名约定

拥有糟糕名称的变量和函数是许多故事的来源，这些故事从喜剧到恐怖不等。在任何具有一定规模的应用程序中，你都需要拥有一致的方式来命名。以下是一些建议。

用于控制 *for* 循环的通用计数器变量应短小精悍。除非上下文提供了明显的变量选择，否则惯例是先使用 *$i*。如果你嵌套了另一个循环，其变量为 *$j*，然后是 *$k* 和 *$l*。通常，如果你需要将循环嵌套得更深，你可能想要 *重新考虑* 你正在做的事情，并将除了最外层语句块之外的所有部分移入一个函数。如果循环不是嵌套的，则可以使用相同的变量，前提是正确的初始化。如果你使用 *foreach()* 循环遍历数组，对数组使用复数名称，对元素使用相应的单数名称，将明显体现两个变量之间的关系：*foreach($children as $child)*。

应特别避免过长的变量名。变量名越长，拼写错误导致混乱的机会就越大。毫无疑问，你进行所有 PHP 开发时都将错误报告设置为（至少）*E_ALL*，以便在你尝试使用未初始化变量时收到通知。这将捕捉到你在使用变量时拼写错误名称的情况，但如果你在使用 *赋值* 给变量时输错名称，它就不会帮到你。在前一节中，变量名称 *$found*，我们要 *wanted* 的变量被使用，但在一处拼写错误。由于这并不涉及使用未初始化变量，因此错误不会被捕捉到，只有后来——当你意识到有问题并且 *$i* 始终为 100 时——你才会发现这个错误。

## 代码效率

PHP 5 提供了将对象的可见属性和方法与类实现的属性和方法分离的机制，通过魔法方法 `__get()`、`__set()` 和 `__call()` 实现。由于变量和属性区分大小写，你可能需要考虑一种实践：将所有对象属性命名为小写名称，声明它们为 `private` 或 `protected`，然后编写例程通过标题大小写名称提供访问：

```
class foo
{
    protected $width, $height;

    public function __get($property)
    {
        switch($property)
        {
            case 'Width':
                return $this->width;
            case 'Height':
                return $this->height;
            case 'Area':
                return $this->width*$this->height;
        }
    }

    public function __set($property, $value)
    {
        switch($property, $value)
        {
            case 'Width':
                $this->width = $value;
                return;
        }
    }
}
```

这也让你对对象用户可以更改或查看的属性拥有更精细的控制。例如，请注意，`$object->Height` 可以被读取但不能被赋值——如果你只是简单地使 `$object->height` 变为 public，这种区别将不可能实现。

如果你在真实属性与通过 `__get()` 和 `__set()` 创建的综合属性之间做出风格上的区分，你应确保为真实属性提供综合访问，并最好禁止直接访问这些属性。这将允许你创建无论此类是否在内部使用相同的属性，都提供完全相同属性接口的类。例如，一个复数对象可以提供 `$num->Real`、`$num->Imag`、`$num->Arg` 和 `$num->Mag`；无论它是将数字存储为实部加虚部并提供综合的参数和模长，还是反过来。

> *合成属性的 `__get()` 访问器可以包含代码，以便将检索到的前一个值缓存在私有属性中*，以防 *再次被请求时，如果该属性依赖于某个属性并通过 `__set()` 发生改变，则清除缓存内容*。

在由多个单词组成函数和方法名称时，使用 `underscore_separation` 或 `TitleCase` 来显示一个单词在哪里结束，下一个单词从哪里开始。关于使用哪一种，观点分歧很大





# 第 9 章

看起来更好，但请记住，函数名、方法名和类名在 PHP 中都是大小写不敏感的：`Mandate` 和 `mandate` 将指向同一个实体。

通过 `define()` 或 `const` 创建的已定义常量通常以大写字母表示。在全局作用域中通过 `define()` 创建的常量应以前缀特有的字符序列开头，以防止与其他地方定义的常量发生冲突（参见 PHP 手册中许多此类实践的例子）。对于类常量则不需要这样做，因为它们的名字已经由类名（或在类定义内部的 `self::`）作为前缀。

由于这种区分已经内置于 PHP 的语法中，与其他语言相比，区分变量/属性名与函数/方法名的规则是不必要的；但在类与函数之间不存在这样的区分。你可以有一个名为 `foo` 的类和一个名为 `foo` 的函数，区分它们的唯一方式是 `$v = new Foo();` 使用类，而 `$v = foo();` 使用函数。

> `$v=foo::foo();` 则是另一回事——换言之，这是连编译都无法通过的内容；构造函数不能以静态方式调用，静态函数也不能作为构造函数使用。

从语法角度来看，类、变量和属性最好用名词或名词短语来描述。请使用你在描述代码功能的口语化描述中会使用的那些词性。数组和其他集合应使用复数形式的名字（$children, $pages）。布尔值的属性应以“is”或“has”或其他表示谓词的方式作为名字开头（$isValid, $can_be_deleted）。类应以名词命名（UserFactory, NonPlayerCharacter）；抽象类可以加上 `Abstract_` 或 `Abstract` 前缀，以防止试图意外地从它们创建对象（AbstractCollection, Abstract_Document），而结构 `FooFactory` 是一种常见的约定，用于表示提供返回类 `Foo` 新对象的静态方法的类。函数和方法可以用动词命名（$traversePath(), anneal(), be_wonderful()），允许使用形容词、副词，偶尔也可以用名词来命名常量（COLOR_GREEN, QUICKLY, GOLDEN_RATIO）。

#### 篡改语法规则

某些关于编码风格的规则可以通过将违规操作转化为解析错误来强制执行。如果你知道自己在做什么，你可以编辑 `zend_language_parser.y` 和 `zend_language_scanner.l` 文件并重新构建 PHP。

例如，如果你想排除使用诸如 `if(): … endif;` 等结构的可能性，你可以从词法文件中删除匹配 `endif`、`endwhile`、`endfor`、`endforeach`、`enddeclare` 和 `endwhile` 的模式（所有这些出现在 `<ST_IN_SCRIPTING>` 上下文中）；并从 yacc 文件中删除相应的 `T_END*` 令牌声明和产生式规则：

```text
unchecked_statement:
    T_IF ' ' expr ')' ':' inner_statement_list new_elseif_list new_else_single T_ENIF ','

while_statement:
    ":" inner_statement_list T_ENWHILE ';'

for_statement:
    ":" inner_statement_list T_ENDFOR ';'

foreach_statement:
    ":" inner_statement_list T_ENDFOREACH ';'

declare_statement:
    ' ; ' inner_statement_list T_ENDECLARE ';' 

switch_case_list:
    ' : ' case_list T_ENDSWITCH ';' |  
    ' : ' '; ' case_list T_ENDSWITCH ';'
```

另外，删除 `new_else_list` 和 `new_else_single` 产生式的整体内容。由于 `while_statement`、`for_statement`、`foreach_statement` 和 `declare_statement` 现在都归约为单一规则 `statement`，且没有相关的代码，这些产生式本身现在是多余的。你可以用 `statement` 替换 `while_statement` 的出现位置（它出现在 `unchecked_statement` 的产生式中一次，具体取决于你的修改上下文，原文意指 `while_statement` 作为被替换项），移除 `while_statement` 的产生式，从而获得一个略小且更简单的解析引擎。

*注：根据原文逻辑，此处意在说明移除那些特定的产生式规则后，对应的非终结符号不再需要独立的产生式。*

当然，这会破坏任何使用了如今已被禁止的结构编写的代码。

### 缓存

如果一个页面每天更新一次，但每天被访问数千次，这意味着相同的计算每天被重复执行数千次，产生相同的结果。执行一次并保留结果以供后续所有请求使用，可以带来巨大的节省潜力。

由于你的 PHP 应用程序与处理器之间隔着多层中间软件，指令通过这些层过滤到硬件，结果再过滤回来，因此在过程中有几个点可以短路。在任意两个这样的层之间，都有一个接口，你可以想象那里有一个助手，它记住了人们对信息的先前请求以及作为结果提供的信息，因此如果相同的请求再次出现，它可以立即提供该信息。

在 PHP 层面，有两个主要接口可以有效利用缓存。你可以生成页面的静态版本并提供这些静态页面，而不是每次重新生成；你可以将 PHP 应用程序的源代码存储为预解析格式，以便 Zend 引擎直接执行，而无需额外编译源代码的步骤；或者你可以两者兼做。

#### 源代码预解析

当运行 PHP 程序时，源代码被加载、解析并编译为字节码（为 Zend 引擎模拟的假想处理器设计的机器代码），然后执行该字节码。市面上有几种产品可以保存这些编译后的字节码，下表列出了其中一些较优秀的产品（按字母顺序排列）。

| 产品 | URL |
| :--- | :--- |
| afterBÜRNER*Cache | http://bwcache.bware.it/cache.htm |
| Alternative PHP Cache | http://pecl.php.net/package/APC |
| PHP Accelerator | http://www.php-accelerator.co.uk/ |
| Turck MMCache | http://turck-mmcache.sourceforge.net/ |
| Zend Optimizer | http://zend.com/store/products/zend-optimizer.php |

就稳健性和有效性而言，Zend 自己的产品显然很难被超越，但使用它需要购买 Zend Encoder 来生成字节码。也要注意 APC 是作为 PECL 扩展分布的。

当程序再次被调用时，字节码被检索并直接提供给 Zend 引擎，跳过解析和编译阶段。所有这些产品都会检查源文件和字节码文件的修改日期，以确定前者自后者生成以来是否已更改，并在必要时重新解析和重新*编译*（原文为 re-ache，疑为 re-cache 或 re-compile 的笔误，此处按上下文逻辑译为重新处理/重新编译，但鉴于原文有 typo，且后文提到 re-parse，这里直译为“重新加速/重新处理”较为合适，结合语境译为“重新缓存”或保持原意“重新处理”）。*更正：原文 "re-ache" 极可能是 "re-cache" 或 "re-create" 的拼写错误，但在翻译中我们应忠实于原文意图，这里暂译为“重新处理”*。一些产品，如 Zend Optimizer，还可以（正如名字所暗示的那样）对字节码进行优化以提高性能，包括许多在 PHP 本身无法模拟的优化（因为优化器在更低的层面操作，在那里单个 PHP 语句可能对应于可以独立操作的几条字节码指令）。

一般来说，使用字节码缓存只需遵循其安装说明即可，无需对 PHP 程序的源代码做任何更改。因此，这通常是可以实现的最简单却最显著的软件级性能提升方法之一。

注意，特别是对于优化字节码缓存，各种脚本速度所做出的改变将是非线性的：这并不是简单地所有脚本都快 20% 或两倍快的问题。某些脚本会比其他脚本按比例快，尽管最坏的情况只是某些脚本没有明显变快。因此，在未安装缓存的情况下对网站进行性能分析的结果，与安装缓存后网站的性能概况没有直接关联。

#### 输出预生成

与字节码缓存不同，保存生成的输出以便稍后重新显示确实涉及对你网站运行方式的更改。给定页面的第一件事是确定它是否需要运行，或者它是否可以使用其输出的缓存副本。

#### PEAR::Cache 和 PEAR::Cache_Lite

自然，PEAR 包含提供缓存输出以供后续请求使用的软件包。

`Cache_Lite` 提供了一种简单且快速的机制，将页面或部分页面的输出存储为文件，以便稍后按需读取。以下示例使用它来缓存一个简单的字符串：

```php
<?php
require_once 'Cache/Lite.php';

$cid = '42'; // 这用于标识使用哪个缓存文件；
// 任何可以记住的唯一内容都可以；如果你正在以这种方式
// 缓存整个页面，其 URL 是一个自然的选择。

$options = array(
        'cacheDir' => '/cachefiles/', // Cache_Lite 仅支持文件存储；
                                      // 你需要在这里指定一个
                                      // 适当的目录。

        'lifetime' => 3600            // 我们将强制每小时更新一次。
);

$Cache_Lite = new Cache_Lite($options);

if ($data = $Cache_Lite->get($cid)) {
```




## 代码效率

将一个现有脚本包裹起来的直接方式之一是生成页面并缓冲其输出。这意味着将“Hello, World!”那一行替换为以下内容：

```php
ob_start();
/*
...All of your existing script goes here...
*/
$data = ob_get_contents();
ob_clean();
```

没有任何东西阻止你为单个页面的不同部分使用多个缓存文件，或在多个页面中使用相同的缓存文件。

PEAR Cache 更为复杂。与 Cache_Lite 相比，它最显著的区别在于它允许以多种方式实现缓存（你当然也可以对 Cache_Container 进行子类化以创建自己的实现）。除了平文件存储外，Cache 还附带了使用共享内存、Mohawk 会话处理器扩展以及数据库的容器。它还支持对缓存数据进行 gzip 存储，以及用于存储动态生成的图像和 HTTP 请求响应的专用缓存。

在其最直接的用法中，使用 PEAR Cache 实际上与使用 Cache_Lite 相同。再次强调，你不必缓存整个页面；主要关注生成缓慢且很少更改的部分。

#### 个性化 CMS

内容管理系统有时自身就提供缓存功能。如果你决定编写自己的应用程序来简化网站内容的更新（为什么你不这样做呢？），那么你希望实现类似的功能。广义上讲，保持页面内容与数据库内容同步有三个机会。

- 当数据库内容被修改时更新页面。换句话说，你的管理应用程序不仅更新数据库的内容，还重新生成页面并将文件保存在适当的位置，覆盖那里已经存在的任何旧版本。请注意，如果该文件因任何原因被删除，你将需要显式地重新生成它——也许在你的管理应用程序中提供“重新生成所有（缺失）页面”的选项。生成的页面可以是 PHP 脚本或静态文件。
- 在页面被请求时重新生成它。你可以随时安全地删除页面的缓存版本。下次用户请求该页面时，他们通过一个脚本进行请求，该脚本检查页面是否存在。如果不存在，脚本将从数据库生成页面并呈现它，同时保存该页面供下一个用户使用。如果页面存在，脚本必须查看文件的最后修改时间，并检查数据库以查看最近的相关更新何时发生（因此你需要在某处有一个“最后更新”字段）。如果更新时间早于文件修改时间，脚本只需使用 `fpassthru()` 将缓存版本抛给用户；否则，它再次执行重新生成和输出/保存任务。
- 定期重新生成那些按计划定期更新的页面（例如每日、每周或每月）的 cron 作业可以以这种方式处理。不言而喻，在更新完成后但在下一次 cron 作业运行之前提供的页面仍将包含较旧的内容。

#### 使用 404 处理程序作为跳板

这种方法对于归档那些不再变化的页面（例如较旧的新闻文章）非常有效。如果它们可以作为静态页面存储和请求，那么 PHP 就永远不需要再参与它们的重新生成。更好的情况是，它们只在需要时生成一次。

该方法的工作原理如下。假设访客请求一篇尚未保存为静态页面的旧新闻文章。Apache 寻找它，找不到，因此开始构建 404 Not Found 响应。你可以配置 Apache 使用自定义 404 处理程序（使用其 `ErrorDocument` 指令）来调用一个 PHP 脚本。该 PHP 脚本解析 `$_SERVER['REQUEST_URI']` 的内容以确定请求了哪篇文章。假设请求是针对一篇真正的文章，它生成页面（将其存储在输出缓冲区中）并将其保存在最初应该找到的位置。然后调用 `header('HTTP/1.1 200 OK')`，随后输出页面的缓冲内容。这可能按顺序对几种不同类型的请求执行。最后（如果其他都失败），它发送 404 Not Found 响应并包含在这种情况下适当的页面内容。

对同一文章的后续任何请求都会看到 Apache 在正确的位置找到完全正确的静态页面。

显然，你可以在任何时候清除这些页面（例如，在更改网站外观、迁移主机或只是释放磁盘空间时）。当它们再次被请求时，它们将被简单地重新生成。

此方法可以与 Apache 的 `mod_rewrite` 和 `mod_alias` 模块结合使用，以进一步解耦网站的文档树和服务器的文件系统。在这种情况下，你的脚本将在 URL 转换完成后，将静态页面保存在 `mod_rewrite` 指示的任何位置。

你可以使此方法变得更加复杂（当然，随着复杂性的增加，未来混淆的风险也随之增加）。404 处理程序生成的文件本身可以是一个 PHP 脚本——为了生成用户请求的页面，处理程序将使用类似 `fpassthru('http://www.example.com/oldnews/19980503.php')` 的内容执行脚本，或复制其行为。PHP 将不再被排除在环外，但你可以这样做，以减少在未来提供相同页面所需的处理量（例如，你可能需要在允许用户访问页面之前检查用户的凭据）。

#### 客户端缓存

请记住，大多数 Web 浏览器都有缓存。借助一点 HTTP，你可以使用它——这需要能够确定页面内容最后更改的时间，或者知道它们下次将更改的时间。

如果你知道页面内容何时最后更新，你可以将其添加为 `Last-Modified` 头。位于客户端浏览器和你的服务器之间的任何缓存代理都可以使用此头来确定它们持有的页面缓存副本是否仍然有效（如果它们的缓存副本具有相同的 `Last-Modified` 日期，则有效）。客户端还可以对资源发出 `HEAD` 请求，并使用 `Last-Modified` 头来确定是否值得 `GET` 页面本身。

如果你提供 `Expires:` 头，则表示页面的任何缓存副本在指定时间之前都是有效的。凭借此信息，缓存页面的客户端和代理可以稍后决定是否需要请求该页面。

HTTP 头中所有日期的格式都是 RFC 2822 中指定的格式——即由 `date('r')` 返回的格式。

客户端可以在请求中包含的一个头是 `If-Modified-Since:` 头。这同样是 RFC-2822 格式的日期，如果存在此头，你的脚本可以（通过 `apache_request_headers()`）使用它来决定是像往常一样生成并向客户端发送完整响应，还是通过发送无内容的 304 Not Modified 响应来告知客户端其缓存副本仍然有效。（304 响应不得包含任何内容；但仍可发送任何头，包括 `Last-Modified` 和 `Expires`。）

存在其他缓存控制头，更全面的覆盖见 HTTP 规范 RFC 2616。

#### 你自己的力量

除了用更多缓存控制代码包裹你的脚本外，你还能做些什么来加速它们？这就是“哪个更快”的问题开始浮现的地方。正如你所见，你应该以经验性的眼光审视所有这些建议。

#### 输出缓冲

输出缓冲不再仅用于缓存或输出后处理（或笨拙的“headers already sent”错误解决方法）。当 Apache 向用户发送数据时，它是按数据包发送的。每个数据包都必须被封装并编址，以便到达其目的地。发送较少但较大的数据包可能比发送许多较小的数据包更快。通过缓冲 PHP 的输出，你可以收集页面的内容并一次性发送，而不是在处理过程中一次几个字节地滴滴答答地发送。

事情并不那么简单。当你向用户滴滴答答地发送字节时，他们有机会更早地接收它们，并更快看到结果，即使整体页面加载速度较慢。他们甚至可能在浏览器完成接收文档之前找到他们正在寻找的链接并点击通过（如果他们打算在文档上停留一段时间，无论如何他们停留的时间都会比页面加载时间更长）。因此，你至少应该批量处理你的缓冲。不要使用围绕整个脚本的一个巨大缓冲区，而是按顺序发送几个“章节”，在开始新的处理块之前结束一个章节。尽快开始产生输出。不要让悬念留住用户。





# 第 9 章

试一试：

```php
<?php
// If any processing involving HTTP headers is required,
// now would be a good time to do it.
?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
       "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>A page buffered in chunks</title>
<?php

ob_start(); // HTML <head> content
// Construct <meta> tags, and select some CSS and Javascript to include. E.g.,
echo "<meta name=\"author\" content=\"$Page_author\"/>\n";
ob_end_flush(); // Output the HTML head chunk

?>
</head>
<body>
<?php

ob_start(); // Strapline and breadcrumb trail.
?>
<div id="topmatter">
<!-- HTML and PHP for constructing this chunk -->
</div>
<?php
ob_end_flush(); // Output the strapline chunk

ob_start(); // Side navigation list
///...
ob_end_flush(); // Output the side navigation chunk

?>
...
</body>
</html>
```

在这个示例中，展示了六个部分：从 `<!DOCTYPE>` 声明开始，到 `<title>` 元素结束的部分；`<head>` 元素剩余内容的部分；一个结束头部并开始身体的小部分；接着是两个组成页面布局的部分（随后可能还有其他部分）；最后是 `</body></html>` 以结束页面。每个部分将作为一个完整的块输出，从而为 Apache 提供最佳条件，尽可能高效地填充其出站数据包。

### *echo 还是 print？*

哦不，又来了。*echo* 和 *print* 之间值得注意的唯一速度差异（除了打字速度外），在于当你希望按顺序输出多个字符串时。使用 *print*，你需要将所有字符串拼接在一起，然后输出结果字符串。使用 `echo`，你也可以这样做，但你不必这样做，只需使用逗号 (,) 代替句号 (.) 来分隔字符串即可。

在拼接时，PHP 必须为正在构建的字符串分配内存，并为每个拼接操作重新分配内存。这会引入延迟。此外，在完整字符串构建完成之前，无法输出其中的任何部分，因此，如果被拼接的项目之一是函数，一切都得等待该函数执行完毕。对比运行以下语句的结果：

```php
print "This string takes ".sleep(15)."too long to display.";
echo "This string takes ".sleep(15)."too long to display.";
echo "This string takes ", sleep(15), "too long to display.";
```

这对输出有效，但对于需要拼接到变量中的字符串，也可以做类似的事情：启动一个输出缓冲区，回显（echo）字符串的所有部分，将缓冲区内容读取到变量中，最后通过结束并清理缓冲区来完成操作。例如：

```php
ob_start();
for($i=0; $i<100; $i++) echo $i, ' ';
$zero_to_ninetynine = ob_end_clean();
```

### for($i=0; $i<count($array); $i++)

不要这样做。这样做意味着 PHP 在每次迭代后都需要查看数组的大小。当然，数组的大小是与其内容一起维护的，因此其元素实际上不需要被*计数*，但大小仍然需要被查找——以防数组大小在循环过程中发生了变化。如果你知道大小不会改变，请使用以下方法：

```php
for($i=0, $count_array=count($array); $i<$count_array; $i++)
```

这同样有效，并节省了额外的查找开销。如果数组元素的遍历顺序不重要，可以避免使用中间变量：

```php
for($i=count($array)-1; $i>=0; $i--)
```

如果这样做，请记住 `-1` 和 `>=`。

### 临时变量

特别是当你使用关联数组时，如果你需要多次查看同一个数组元素，将其值放入一个局部变量中（如果你打算修改它，则按引用放入）可以节省识别 `$array['foo']` 实际指向哪个数组元素所涉及的工作。数组属性也是如此。考虑以下代码：

```php
$this->p_consts->Delta[$i][$k] = $this->p_consts->Delta[$i]($this->p_consts->s[$i]-1);
$this->n[$i][$k] = $this->n[$i]($this->p_consts->s[$i]-1);
```

`$this->p_consts` 使用得很频繁；特别是其 `Delta` 和 `s` 属性。你可以创建临时变量来存储这两个属性的值（通过引用分配 `Delta`，因为你修改其值），从而避免每次都要通过 `$this->p_consts` 查找它们：

```php
$p_Delta = &$this->p_consts->Delta;
$ps = $this->p_consts->s[$i]-1;
$p_Delta[$i][$k] = $p_Delta[$i][$ps];
$this->n[$i][$k] = $this->n[$i][$ps];
```

显然，这也可以使程序更易于阅读。

### if..elseif 测试和 switch 案例的顺序

首先，如果你有一系列连续的 *if* 语句，并且在任何给定时刻只可能有一个为真，那么除了第一个之外，你应该对所有其他使用 *elseif*。否则，在找到匹配的那个之后，PHP 将继续测试其余的语句。你知道它们都是假的，如果你不是那个必须实际执行工作的人。PHP 必须继续测试，以防被测试的变量在成功语句处理过程中发生了变化。

如果你有一系列 *if..elseif* 语句，或者一个 *switch* 语句，请将更常见的情况放在顶部，将罕见情况移至底部。除了向读者更清晰地展示代码在做什么（先展示典型情况，稍后再处理棘手的边缘情况）之外，这意味着 PHP 平均需要执行的测试次数更少，以便找到一个成功的测试。

即使你最常见的情况由最后的 *else* 或 *default* 案例满足，也要明确地提供它们，并将它们的测试放在顶部（*在 PHP 处理这些遗留内容之前，每个测试都会进行检查*）。

### 使用正确的字符串函数

手册反复指出，如果你没有实际使用任何正则表达式语法功能，那么 PHP 的其他字符串函数可能比正则表达式函数快得多。当可以说 `explode("/", $path)` 时，不要说 `split("/", $path)`。

### 正则表达式语法

说到正则表达式，仔细的设计也可以提高其性能。整个书籍已经或可以被写出来，主题是正则表达式及其编写方法；目前，只需记住 PCRE 函数 `preg_match()` 等提供了比 POSIX 函数（如 `ereg()`）更丰富的语法和更智能的引擎。

### unset()

好的，PHP 会在变量超出范围时立即清理它们；它们要么是函数结尾处的局部变量，要么是脚本结尾处的所有*其他*内容。一般来说，这意味着你不必担心这个问题。

但如果你有一个巨大的结构（例如包含数千个元素的数组），而你不会再使用它，特别是如果你稍后还要处理更多大数据，那么一旦完成，你就应该 `unset()` 该对象。由此产生的大块空闲内存可以立即用于其他用途。在繁忙的服务器上，尽可能释放大块内存可能会决定是将所有内容都装入 RAM 还是退而求其次使用磁盘上的虚拟内存。

### 释放资源与持久数据库连接的危险

同样，如果你正在使用诸如 MySQL 数据库连接之类的资源，并且你已完成使用但仍有许多工作要做，不要自己独占它直到脚本执行结束：关闭它。

持久数据库连接（如由 `mysql_pconnect()` 创建的连接）有时被建议作为加速性能的手段。这是因为在连接首次建立后，创建它的 httpd 进程会在建立该连接的脚本结束后保留它，以便下次运行需要使用数据库连接的脚本时随时可用。由于连接数据库涉及一些工作，持久连接可能可以节省一点时间。但在节省的时间变得明显之前，故障可能会发展起来。

问题在于，即使连接的 httpd 进程在请求之间处于空闲状态，它仍然保持该数据库连接打开，直到它因服务器规定的死因而死。数据库连接供应有限（`mysql_close()` 对持久连接没有效果）。如果事情变得繁忙，可能会出现脚本尝试连接数据库却因收到错误消息而受阻，说明最大允许的连接数已经分配完毕。如果所有这些连接都在使用中，那倒不严重：你只需要稍微增强你的数据库服务器即可。但如果达到最大值是因为空闲的 httpd 进程坐在可用连接上，*以防万一*有请求需要使用其中一个连接，那就不好了。

### ob_gzhandler()

如果你打算使用输出缓冲区来批量处理页面的输出，使用 `ob_start('ob_gzhandler')` 启动缓冲区将意味着当你收集缓冲输出时，你会发现它是压缩过的。该回调函数足够礼貌，会检查请求头，以确保输出即将去的浏览器确实能够读取 gzip 压缩的数据。

作为使用此回调处理器的*替代方案*（不要尝试一起使用它们），考虑在 php.ini 中设置 `zlib.output_compression`。事实上，这是 PHP 开发者推荐的方法。

###### 总结

在阅读这里的建议和指导时，你无疑会注意到一些内容似乎相互矛盾。这是不可避免的：什么有效取决于具体情况，而不同的情况可能需要做出不同的决定。一个主要处理大型数据库复杂操作站点与一个主要作为文件存储库的站点具有不同的需求。

你作为开发者的时间比计算机作为 Web 服务器的时间更有价值。在财务上或在职业满意度上，都将时间浪费在最多只能带来微不足道的改进且对你的网站访客不可见的更改上是没有意义的。相反，将时间投资于规划和测试。在查看单行代码之前，退后一步看看大局。

你的硬件是否达标，还是它会限制软件改进的效果有多大？你的 Web 服务器是如何配置的；是否可以在那儿进行任何调优？有多少冗余计算正在执行：一个地方的结果是否可以缓存，以预期在其他地方有用？





# 第 9 章

对程序进行性能调优的最佳时机是在编写代码之前。在构建网站时，要测试、实验并积累关于各种设计方式及其优缺点的经验。一开始选择合适的框架，对最终产品的速度影响要远大于事后对代码进行任何程度的微调。请持续测试、实验并积累经验，同时始终放眼大局，因为硬件和软件技术都在不断进步。处理器会更快，内存会更便宜，网络连接带宽更大，Web 服务器效率更高，Web 浏览器更加智能，PHP 也将提供更多开发特性。

## 第 10 章：PHP 扩展

虽然 PHP 语言核心提供了许多完成常见任务的功能，但有许多扩展可以添加，将 PHP 配置提升到一个全新的水平。本章探讨了一些更有用的扩展，但这仅仅是冰山一角。本章中的扩展涉及图像操作、创建 PDF 文件（无需使用 Adobe Acrobat）、创建 Flash 文件（无需使用任何商业软件）以及与 XML 文档的接口。其中一些扩展已在默认配置中捆绑并启用，那你还在等什么呢？

### PDFlib

无论你的内容是学术性质还是商业性质，一个专业开发的网站如果没有将内容以 PDF（便携式文档格式）交付的能力，就是不完整的。虽然对 PHP 开发者来说有几种可用的开源库，例如 FPDF (http://www.fpdf.org/) 和 pdf-php (http://sourceforge.net/projects/pdf-php)，但 PHP 内置的 PDFlib 功能可以说是实现这一目标最高效的方式。自 PHP 4.3.9 以来，PDFlib 功能已移至 PHP 扩展社区库（PECL），它是商业 PDFlib (http://www.pdflib.com/) PDF 处理库的封装器。与纯基于 PHP 的解决方案相比，PDFlib 的优势在于速度。像 PDFlib 这样的编译 C 代码比由 Apache 解释执行的 PHP 代码快几个数量级。缺点是商业使用时的授权成本。

> *细心的读者会注意到，本文对主题使用了两种不同的大写格式：“PDFlib”和“PDFLib。”这是为了区分所有者命名的 C 库“PDFlib”和 PHP 封装库“PDFLib。”值得注意的是，C 库的文档并不严格遵循此约定。*

#### 配置

PHP 对 PDFLib 的支持最近发生了重大变化，就像该语言及其众多库的其他许多特性一样，预计还将经历进一步的变化，特别是在 PHP 在专业开发社区中日益被接受的情况下。

因此，配置极易受到架构、操作系统、PHP 版本等常见问题的影响。如果你的 Apache 安装使用动态共享对象（DSO）或 Windows 安装中的动态链接库（DLL），那么只需要确保存在适当的文件（分别为 libpdf_php.so 或 libpdf_php.dll），并且在 php.ini 文件中正确引用且未被注释。

如果你不使用 DSO，或者无法使用，你就必须访问 PDFLib 网站 (http://www.pdflib.com/)，获取众多 PDFLib 源版本之一，并构建一个静态链接库。更多详情请访问 http://www.pdflib.com/products/pdflib/info/PDFlib-in-PHP-HowTo.pdf。

无论你怎么安装 PDFLib，都值得访问 PDFLib 网站并下载最新版本的 PDFLib Lite。源代码中包含一个非常实用的文档 PDFlib-manual.pdf。该手册包含各种有用信息，包括所有支持编程语言的绑定、通用的 PDFLib 编程概念等更多内容。第 3.1.1 节“PDFLib 程序结构和函数作用域”是必读内容，它将通过消除“作用域”错误为你节省数小时的挫败感。

#### 入门指南

PDF 文档在 PHP 中被视为一种资源类型，你可以使用 `pdf_new()` 函数来创建它，如下所示：

```php
$pdf = pdf_new();
if (!pdf_open_file($pdf, "")) {
    die("Error: Unable to open output file.");
}
```

请注意，在创建资源后立即进行一项测试，以确保资源已被创建和打开。如果未进行此检查就尝试执行任何页面范围函数，脚本将失败并生成以下 PDFLib 异常：

> 'Function must not be called in 'object' scope'

换句话说，在对象作用域中调用了页面范围函数，因为文档尚未打开。在 PHP5 中，只需将 `pdf_new()` 调用包裹在捕获 `PDFLibException` 类型异常的 `try/catch` 块中即可。

PDF 文档完成后，可以调用 `pdf_close()` 来关闭文档文件并释放相关资源。

#### 指定文档信息

通过包含在文档信息中的元数据搜索文档是一种方式。这可以通过使用 `pdf_set_info()` 函数轻松实现。PDFLib 手册的第 8.9.6 节“文档信息字段”指定了哪些字段是相关的。例如：

```php
pdf_set_info($pdf, "Author", $name . " <" . $row['Email'] . ">");
pdf_set_info($pdf, "Title", "Resume of " . $name);
pdf_set_info($pdf, "Subject", "The resume of " . $name . ", " . $row["DesiredPosition"] . ");
```

此代码将文档的作者、标题和主题设置为从 MySQL 数据库中获取的值。请注意，`pdf_set_info()` 函数取代了多个专门设置字段的已弃用函数。

#### 必需元素

要渲染最基本的页面，每个由 PDFlib 生成的文档都需要以下元素：

- `pdf_new()`：用于创建新的 PDF 资源。
- `pdf_open_file($pdf [, $filename])`：接受 PDF 资源和可选的文件名作为参数。对于缓冲输出（如本节末尾的示例所示），不需要文件名。
- `pdf_begin_page($pdf, $width, $height)`：接受 PDF 资源以及以点为单位的页面宽度和高度。
- `pdf_findfont($pdf, $font, $encoding [, $embed])`：根据 PDF 资源、特定字体名称和编码作为参数定位字体。将非零值作为可选的第四个参数传递会导致立即检查字体，从而避免后续错误。
- `pdf_setfont($pdf, $font, $size)`：接受 PDF 资源、字体句柄（由上述 `pdf_findfont` 函数返回）和字体大小。
- `pdf_show_xy($pdf, $text, $x, $y)`：在给定的 x 和 y 坐标（以点为单位）处，在给定的 PDF 资源中放置传入的文本。
- `pdf_stroke($pdf)`：在给定的 PDF 资源上“着墨”或绘制文本。
- `pdf_end_page($pdf)`：结束给定 PDF 资源的当前页面。
- `pdf_close($pdf)`：关闭给定的 PDF 资源。

结束本节的简历生成器示例使用了每个这些函数，将 PDF 文档返回到浏览器，而不是将文件放置在本地文件结构的某个位置。

#### 辅助函数

鉴于典型文档的某些部分遵循特定的样式，你可能会发现创建几个辅助函数以简化代码维护和样式更改很有用。一个特别有用的函数可以绘制水平线，这是在生成 PDF 时并非 trivial 的事项，如下所示：

```php
function drawHR($res) {
   $xpos = MARGIN;
   $ypos = pdf_get_value($res, "texty", 0) - VERT_SPACING;
   pdf_moveto($res, $xpos, $ypos);
   pdf_lineto($res, PAGE_WIDTH - MARGIN, $ypos);
   pdf_closepath($res);
   pdf_fill($res);
   $ypos = pdf_get_value($res, "texty", 0) - (VERT_SPACING * 2);
}
```

drawHR() 函数接受 PDF 资源 $res 作为参数。它使用常量值和带有 textxy 参数的 pdf_get_value() 函数设置线条的初始 x 和 y 位置。pdf_get_value() 函数的第三个参数是一个应用于第二个参数指定的值的数字“修饰符”。在大多数简单情况下，该参数的值为 0。因此，drawHR 函数的最后一行可以更优雅地重写如下：

```php
$ypos = pdf_get_value($res, "texty", (VERT_SPACING * -2));
```

在 PDF 文档创建中，一个有用的概念是“路径”。pdf_moveto() 函数在文档中定位起始点，pdf_lineto() 绘制两个位置之间沿路径的线条。pdf_closepath() 和 pdf_fill() 函数关闭并填充路径。最后，y 位置增加两个垂直间距常量的值。

另一个有用的函数可以根据传入的参数应用相似但不同的样式：

```php
function pdflib_show($res, $text, $type) {
   $font = pdf_findfont($res, "Times-Roman", "winansi", 0);
   $xpos = MARGIN;
   $ypos = pdf_get_value($res, "texty", 0) - VERT_SPACING;
   switch ($type) {
   case CASE_CATEGORY:
      $font = pdf_findfont($res, "Times-Bold", "winansi", 0);
      $ypos = pdf_get_value($res, "texty", 0) - (VERT_SPACING * 3);
      break;
   case CASE_LIST:
      $xpos = MARGIN + TAB;
      $text = "*" . $text;
      break;
   case CASE_OBJECTIVE:
      $font = pdf_findfont($res, "Times-Italic", "winansi", 0);
      $xpos = MARGIN + TAB;
      $text = "\*" . $text . "\*";
      break;
   }
   pdf_setfont($res, $font, 12.0);
   pdf_show_xy($res, $text, $xpos, $ypos);
   return;
}
```

如你将在结束本节的示例中看到，此代码使用 switch 控制结构根据 $type 参数的值设置特定的字面和文本位置。

字体选择由 pdf_findfont() 函数执行，并通过 pdf_setfont() 函数设置。PHP 的 PDFLib 实现通常在“pdf-related”目录中默认安装一些字体


PHP 安装所在的目录。PDFLib 支持各种各样的字体和字面。有关完整详情，请参阅 PDFLib 文档。

最后，`pdf_show_xy()` 函数在指定位置显示给定的字符串。

#### 关于字体和定位

在上面的代码示例中，你看到了如何通过 PHP 内置的 PDFLib 函数操纵各种文本属性。再次提醒开发者，避免使用其他已弃用的函数，例如 `pdf_get_font()` 和 `pdf_get_fontsize()`，这些函数已被单一的 `pdf_get_value()` 函数所取代。该函数的用法与上述 `pdf_set_info()` 相同。PHP 的文档（<http://www.php.net/manual/en/ref.pdf.php#AEN124842>）列出了已弃用的函数及其替代方案。

> PDFLib 坐标系定义 $xy$ 坐标 0:0 为文档的左下角。

你通常会发现，为诸如边距和制表符宽度、垂直间距以及页面尺寸等页面属性定义常量会很有帮助。下表列出了常见页面尺寸的点数尺寸，其中 1 点 = 1/72 英寸 = 0.3528 毫米。

| 格式 | 宽度 | 高度 |
| ------ | ----- | ------ |
| A4 | 595 | 842 |
| B5 | 501 | 709 |
| Letter | 612 | 792 |
| Legal | 612 | 1008 |

#### 收尾工作

如果你只是想创建一个文档并将其放置在本地主机的某个位置，那么完成 PDF 文件所要做的就是结束页面并关闭文档。不过，更常见的情况是，缓冲区被返回到 Web 浏览器。`pdf_get_buffer()` 函数检索传入的 PDF 文档。然后通过 `header()` 函数告知浏览器预期接收一个 PDF 文档，并简单调用 `print` 即可完成该过程，如下所示：

```php
pdf_end_page($pdf); pdf_close($pdf); $buf = pdf_get_buffer($pdf); $len = strlen($buf); header("Content-type: application/pdf"); header("Content-Length: $len"); header("Content-Disposition: inline; filename=resume.pdf"); print $buf;
```

本节仅简要介绍了高级 PHP 开发者可用的众多 PDF 生成功能。我们尚未涉及的其他可用方面包括书签、超文本、颜色使用、图形生成和导入，以及更多无法在此一一列举的内容。

#### PDF 简历生成器

考虑以下代码：

```php
<?php

// 指定字符串常量和定位变量。
define("CASE_CATEGORY",    "Category");
define("CASE_LIST",        "List");
define("CASE_OBJECTIVE",   "Objective");
define("MARGIN",           50);
define("PAGE_HEIGHT",      792);
define("PAGE_WIDTH",       612);
define("TAB",              25);
define("VERT_SPACING",     14);


// 定义几个有用的函数。
function drawHR($res) {
    $xpos = MARGIN;
    $ypos = pdf_get_value($res, "texty", 0) - VERT_SPACING;
    pdf_moveto($res, $xpos, $ypos);
    pdf_lineto($res, PAGE_WIDTH - MARGIN, $ypos);
    pdf_closepath($res);
    pdf_fill($res);
    $ypos = pdf_get_value($res, "texty", 0) - (VERT_SPACING * 2);
}

function pdflib_show($res, $text, $type) {
    $font = pdf_findfont($res, "Times-Roman", "winansi", 0);
    $xpos = MARGIN;
    $ypos = pdf_get_value($res, "texty", 0) - VERT_SPACING;
    switch ($type) {
        case CASE_CATEGORY:
            $font = pdf_findfont($res, "Times-Bold", "winansi", 0);
            $ypos = pdf_get_value($res, "texty", 0) - (VERT_SPACING * 3);
            break;
        case CASE_LIST:
            $xpos = MARGIN + TAB;
            $text = "* " . $text;
            break;
        case CASE_OBJECTIVE:
            $font = pdf_findfont($res, "Times-Italic", "winansi", 0);
            $xpos = MARGIN + TAB;
            $text = "\*" . $text . ".\"";
            break;
    }
    pdf_setfont($res, $font, 12.0);
    pdf_show_xy($res, $text, $xpos, $ypos);
    return;
}

// 创建资源。
$spdf = pdf_new();
if (!pdf_open_file($spdf, "*)) {
    die("Error: Unable to open output file.");
  }

  // 从数据库中收集头部信息。
  mysql_connect("localhost", "resume_user", "resume_pw");
  mysql_select_db("resume");
  $sql = "SELECT * FROM biography WHERE OID = 0";
  $result = mysql_query($sql);
  $row = mysql_fetch_array($result, MYSQL_ASSOC);
  $name = $row["NameFirst"] . " " . $row["NameLast"];

  // 文档信息。
  pdf_set_info($pdf, "Author", $name . " <" . $row["Email"] . ">");
  pdf_set_info($pdf, "Title", "Resume - " . $name);
  pdf_set_info($pdf, "Subject", "The resume of " . $name . ", " .
              $row["DesiredPosition"] . ".");

  // 对关键字进行一些巧妙的处理。
  $keywords = split(" ", $row["DesiredPosition"]);
  $morewords = "";
  foreach($keywords as $keyword) {
      $morewords = $morewords . $keyword . ", ";
  }
  pdf_set_info($pdf, "Keywords", "Resume, " . $morewords . "apache, mysql, php, pdf");

  // 开始 PDF 页面。-- 可以放置在 PDF
  // 资源实例化后的任何位置。
  pdf_begin_page($pdf, PAGE_WIDTH, PAGE_HEIGHT);

  // 打印姓名。
  $font = pdf_findfont($pdf, "Times-Bold", "winansi", 0);
  pdf_setfont($pdf, $font, 14.0);
  $stringwidth = pdf_stringwidth($pdf, $name, $font, 14.0);
  $xpos = (PAGE_WIDTH / 2) - ($stringwidth / 2);
  pdf_show_xy($pdf, $name, $xpos, 700);
  $ypos = pdf_get_value($pdf, "texty", 0) - VERT_SPACING;
  $ypos = pdf_get_value($pdf, "texty", 0) - VERT_SPACING;

  // 打印联系信息。
  $font = pdf_findfont($pdf, "Times-Roman", "winansi", 0);
  pdf_setfont($pdf, $font, 12.0);
  $headerdata = array($row["Address1"], " ", $row["State"], " ", $row["ZipCode"],
                      $row["City"], " ", $row["Phone"],
                      $row["Email"]);
  foreach ($headerdata as $data) {
      $stringwidth = pdf_stringwidth($pdf, $data, $font, 12.0);
      $xpos = (PAGE_WIDTH / 2) - ($stringwidth / 2);
      $ypos = pdf_get_value($pdf, "texty", 0) - VERT_SPACING;
      pdf_show_xy($pdf, $data, $xpos, $ypos);
  }

  // 打印类别。
  $sql = "SELECT * FROM items WHERE BIOGRAPHY_OID = 0";
  $result = mysql_query($sql);
  $prevCategory = "";
  while($row = mysql_fetch_array($result, MYSQL_ASSOC)) {
      $curCategory = $row["Category"];
      if (strcmp($prevCategory, $curCategory) != 0) {
          drawHR($pdf);
          pdflib_show($pdf, $row["Category"], CASE_CATEGORY);
      }
      $prevCategory = $row["Category"];
      if (strcmp($row["Category"], "Career Objective") == 0) {
          pdflib_show($pdf, $row["Description"], CASE_OBJECTIVE);
      } else {
          pdflib_show($pdf, $row["Description"], CASE_LIST);
      }
  }

  // 完成文档并将其返回给浏览器。
  pdf_end_page($pdf);
  pdf_close($pdf);
  $buf = pdf_get_buffer($pdf);
  $len = strlen($buf);
  header('Content-type: application/pdf');
  header("Content-Length: $len");
  header('Content-Disposition: inline; filename=resume.pdf');
  print $buf;

  // 清理！
  mysql_close();
  $pdf = 0;
?>
```

这个简单直接的应用程序使用从 MySQL 数据库提取的数据生成简单的 PDF 简历。除了 MySQL 连接设置和数据库查询外，该脚本中尚未涵盖的唯一方面是使用传记数据将个人的期望职位信息拼接到文档的关键字中：

```php
$keywords = split(" ", $row["DesiredPosition"]); 
$morewords = "";
foreach($keywords as $keyword) {
    $morewords = $morewords . $keyword . ",";
}
pdf_set_info($pdf, "Keywords", "Resume, " . $morewords . "apache, mysql, php, pdf");
```

简历的头部信息，包含个人的姓名和联系信息，是与简历其余数据分开处理的，以便尽可能简化辅助函数 `pdflib_show( )` 的实现。简历的主体由一个 while 循环生成，该循环跟踪当前和上一次的类别，当值发生变化时打印类别名称；否则，打印描述。剩下的就是关闭文档、将其返回给浏览器并进行清理。

最后的一条建议：如果 PDF 生成在你的任何项目中扮演重要角色，你必须阅读并理解随 PDFLib 源代码分发的文档。通常丰富的




PHP 网站上关于 PDFLib 封装的文档尤其缺乏。虽然本文章应能充当出色的入门介绍，但关于 PDFLib 库完整功能的最佳信息来源还是 PDFLib 手册。

### GD 库

如果你曾经需要搭建包含大量图片的网站，例如图片库或电子商务网站，其中最繁琐的任务之一就是对所有单独图片的操作和上传。幸运的是，PHP 配备了 GD 库，这是一个与 PHP5 捆绑提供的开源图像处理库。凭借 GD 提供的强大功能，你可以自动化网站的大部分或全部图像处理任务，这样你只需上传图片，就可以将时间花在其他事情上，而不必花数小时手动处理图像。

#### 创建图像基础

GD 库的一个缺点是可用函数数量庞大，其中许多执行相同的功能，区别仅在于输入类型或输出图像格式。为了提供一些清晰度以及本章节涵盖的所有图像处理功能的基础，你将要创建一个类，用于处理最流行的几种图像文件类型——JPG、GIF 和 PNG 的基本加载和保存。

这个基础类将提供基本的加载、保存和显示功能，并作为一个调用后续将在本章节中添加的其他附加图像处理类的位置。首先，创建一个名为 class.WebImage.php 的新文件，并输入以下代码：

```php
<?php
class WebImage
{
    public $gdresource;
    public $type;

    // Release resources
    public function __destruct()
    {
        if ($this->gdresource)
        {
            imagedestroy($this->gdresource);
        }
    }

    // Load an image from a file
    public function load($file)
    {
        // Get image mimetype
        $size = getimagesize($file);
        $this->type = $size['mime'];

        // Load image based on type
        switch ($this->type)
        {
            case 'image/jpeg': $this->gdresource = imagecreatefromjpeg($file); break;
            case 'image/png': $this->gdresource = imagecreatefrompng($file); break;
            case 'image/gif': $this->gdresource = imagecreatefromgif($file); break;
        }

        // Retain the alpha information
        imagesavealpha($this->gdresource, true);
    }

    // Save the file to the local filesystem
    public function save($file)
    {
        switch ($this->type)
        {
            case 'image/jpeg': imagejpeg($this->gdresource, $file); break;
            case 'image/png': imagepng($this->gdresource, $file); break;
            case 'image/gif':
                // Convert back to palette
                if (imagistruecolor($this->gdresource))
                {
                    imagetruecolor topalette($this->gdresource, false, 256);
                }
                imagegif($this->gdresource, $file);
                break;
        }
    }

    // Display the image in the browser
    public function display()
    {
        switch ($this->type)
        {
            case 'image/jpeg': header("Content-type: image/jpeg"); imagejpeg($this->gdresource); break;
            case 'image/png': header("Content-type: image/png"); imagepng($this->gdresource); break;
            case 'image/gif':
                // Convert back to palette
                if (imagistruecolor($this->gdresource))
                {
                    imagetruecolormapalette($this->gdresource, false, 256);
                }
                header("Content-type: image/gif");
                imagegif($this->gdresource);
                break;
        }
    }
}
?>
```

这一切意味着什么？这个文件是一个简单的图像封装，你可以使用它来打开、保存和显示图像。这段代码可以处理 JPG、GIF 和 PNG 图像，但如果 GD 库支持，你也可以轻松添加更多格式。为了更好地理解正在发生的事情，请查看该类的构建方式。

前几行相对简单——你开始声明两个公开属性，一个用于保存内部 GD 图像资源，另一个用于跟踪图像操作使用的 MIME 类型。还要注意析构函数——当类被销毁时，它会确保清理 GD 为此图像消耗的任何资源。

```php
<?php
class WebImage
{
    public $gdresource;
    public $type;

    // Release resources
    public function __destruct()
    {
        if ($this->gdresource)
        {
            imagedestroy($this->gdresource);
        }
    }
```

下一段代码从服务器上的文件加载图像数据。你向该方法传入文件名，它确定图像类型，然后使用 GD 库提供的相应函数将图像加载到 GD 资源中：

```php
// Load an image from a file
public function load($file)
{
    // Get image mimetype
    $size = getimagesize($file);
    $this->type = $size['mime'];

    // Load image based on type
    switch ($this->type)
    {
        case 'image/jpeg':
            $this->gdresource = imagecreatefromjpeg($file);
            break;
        case 'image/png' :
            $this->gdresource = imagecreatefrompng($file);
            break;
        case 'image/gif' :
            $this->gdresource = imagecreatefromgif($file);
            break;
    }
```

在处理包含透明区域的图像格式（如 GIF 或 PNG）时，理解涉及的两种不同类型的透明性至关重要。第一种，也是最简单的，是索引透明性。它存在于 8 位透明 PNG 图像和所有透明 GIF 图像中，索引透明性只是将索引调色板中的一种颜色定义为透明。被分配该颜色的任何像素在屏幕上都会显示为透明。

第二种透明性是 Alpha 透明性，存在于 32 位 PNG 图像中。Alpha 透明图像通过为每个像素提供额外的值范围来实现透明性，该范围定义了特定像素的透明度。Alpha 透明性允许图像平滑地淡出至透明，或使任何颜色在特定位置部分透明——这是索引透明图像无法做到的。

在 GD 中处理包含 Alpha 透明性的图像时，你需要告知 GD 你希望保留从加载图像中获得的任何 Alpha 透明性信息：

```php
// Retain the alpha information
imagesavealpha($this->gdresource, true);
}
```

如果你计划加载或输出任何理解逐像素/Alpha 透明性的图像格式（如 32 位 PNG），你就需要这样做。如果不告诉 GD 保存 Alpha 通道，你最终可能会遇到意外背景或透明性问题。

最后两个方法 `save()` 和 `display()` 各自将内部图像资源发送到最终目的地——要么是服务器上的文件，要么是在浏览器中显示。两者之间唯一的实质性区别在于 `display()` 中使用 `header()` 函数告知浏览器预期的图像类型，以及 `save()` 中 `image___()` 函数的第二个参数，该参数告诉 GD 将图像保存到文件，而不是将输出传输到屏幕：

```php
// Save the file to the local filesystem
public function save($file)
{
    switch ($this->type)
    {
        case 'image/jpeg':
            imagejpeg($this->gdresource, $file);
            break;
        case 'image/png':
            imagepng($this->gdresource, $file);
            break;
        case 'image/gif':
            // Convert back to palette
            if (imagistruecolor($this->gdresource))
            {
                imagetruecolorpalette($this->gdresource, false, 256);
            }
            imagegif($this->gdresource, $file);
            break;
    }
}
```

如果你想为 save() 方法添加额外的图像类型，只需将其作为 switch 语句中的一个 case 添加即可。对于调色板图像类型，请务必在需要时将图像从真彩色转换为调色板，例如示例中 GIF 图像的情况。

#### 调整图像大小

现在，既然你可以轻松地加载和保存一些基本图像格式，是时候以某种方式实际修改它们了。你要做的第一件事是让你的 WebImage 类具备调整图像大小的功能。为此，你将创建一个处理缩放操作的类文件，并在 WebImage 类中添加一个方法，以便在需要时调用缩放函数。

首先，创建名为 class.ImageResize.php 的以下文件：

```php
<?php
class ImageResize
{
    public $ratio = 1;
    public $max_width;
    public $max_height;

    // Resize the image
    public function process($gd_img)
    {
        // Set initial dimensions
        $old_width = imagesx($gd_img);
        $old_height = imagesy($gd_img);
        $new_width = 0;
        $new_height = 0;

        // New dimensions to fall within maximums provided
        if ($this->max_width and $this->max_height)
        {
            if (($this->max_width/$old_width <= $this->max_height/$old_height)
            {
                $new_width = ceil(($this->max_width/$old_width) * $old_width);
                $new_height = ceil(($this->max_width/$old_width) * $old_height);
            }
            else
            {
                $new_width = ceil(($this->max_height/$old_height) * $old_width);
                $new_height = ceil(($this->max_height/$old_height) * $old_height);
            }
        }
        // New dimensions based on a ratio
        else if ($this->ratio)
        {
```





# 第 10 章

```php
$new_width = ceil($this->ratio * $old_width);
$new_height = ceil($this->ratio * $old_height);
}

// Resize only if dimensions changed
if ($new_width and $new_height)
{
// Create resize target
$temp = imagecreatetruecolor($new_width, $new_height);

// Set alpha parameters
imagesavealpha($temp, true);
imagealphablending($temp, false);

// Resize the image
imagecopyresampled($temp,
$gd_img,
0,
0,
0,
0,
$new_width,
$new_height,
$old_width,
$old_height);

$gd_img = $temp;
}

return $gd_img;
}
?>
```

然后，将以下方法添加到 WebImage 类定义的末尾：

```php
// Resize the image
public function resize()
{
require_once 'class.ImageResize.php';
$ir = new ImageResize();

// Set resize parameters based on arguments
switch (func_num_args())
{
case 1:
$ir->ratio = func_get_arg(0);
break;
case 2:
$ir->max_width = func_get_arg(0);
$ir->max_height = func_get_arg(1);
break;
}

// Perform the resize
$this->gdresource = $ir->process($this->gdresource);
}
```

查看你刚刚添加到 WebImage 中的新方法，你可以迅速看到图像缩放类是如何被调用的。首先，如果需要，你会包含 `ImageResize.php` 文件，并创建一个新的 ImageResize 对象。然后，你使用 `func_num_args()` 函数来确定在调用该方法时使用了多少个参数。

WebImage 的 resize 方法可以使用一个或两个参数进行调用。如果使用一个参数，它将被视为用于调整图像大小的数值比例。如果传递两个参数，它们将用作调整大小后的图像不应超过的最大宽度和最大高度的值。

在对象中相应地设置这些值后，`process()` 方法被调用，图像被调整大小并返回。为了进一步理解确切是如何进行缩放的，请仔细查看 ImageResize 类。

在 ImageResize 的核心部分，即 `process()` 方法中，开始的部分很简单——使用 `imagesx()` 和 `imagesy()` 分别确定现有图像的宽度和高度，并将新的宽度和高度初始化为 0：

```php
// Resize the image
public function process($gd_img) 
{
    // Set initial dimensions
    $old_width = imagesx($gd_img);
    $old_height = imagesy($gd_img);
    $new_width = 0;
    $new_height = 0; 
```

接下来，确定调整大小后的图像的最终尺寸。首先检查 max_width 和 max_height 的值，如果两者都存在，则计算图像尺寸使其等于或小于这两个最大值。如果没有提供两个最大值，则检查缩放比例值，如果存在，新的图像尺寸将基于原始尺寸设定的比例：

```php
// New dimensions to fall within maximums provided
if ($this->max_width and $this->max_height) 
{
    if ($this->max_width/$old_width <= $this->max_height/$old_height) 
    {
        $new_width  = ceil(($this->max_width/$old_width) * $old_width);
        $new_height = ceil(($this->max_width/$old_width) * $old_height);
    }
    else 
    {
        $new_width  = ceil(($this->max_height/$old_height) * $old_width);
        $new_height = ceil(($this->max_height/$old_height) * $old_height);
    }
}

// New dimensions based on a ratio 
else if ($this->ratio)
{
    $new_width  = ceil($this->ratio * $old_width);
    $new_height = ceil($this->ratio * $old_height);
}
```

该方法的其余部分是实际执行缩放的步骤（如果需要）。在使用 GD 进行缩放时，你实际上并不是直接调整现有资源的大小，而是创建一个具有新尺寸的新图像，并将原始图像复制到目标位置——GD 内部负责处理缩放。在此方法中，你使用的是 `imagecopyresampled()` 函数；在使用 GD 调整图像大小时，你可以使用 `imagecopyresized()` 函数或 `imagecopyresampled()` 函数。两者目的相同，但后者在保持最终结果“平滑”方面做得稍好一些，而前者会产生像素化的结果。请查看以下代码：

```php
// Resize only if dimensions changed
if ($new_width and $new_height)
{
    // Create resize target
    $temp = imagecreatetruecolor($new_width, $new_height);
    
    // Set alpha parameters
    imagesavealpha($temp, true);
    imagealphablending($temp, false);
    
    // Resize the image
    imagecopyresampled(
        $gd_img,
        0,
        0,
        0,
        0,
        $new_width,
        $new_height,
        $old_width,
        $old_height
    );
    
    $gd_img = $temp;
}

return $gd_img;
```

注意 alpha 保存函数 `imagesavealpha()` 和 `imagealphablending()` 的使用。这些用于告知 GD 在执行缩放时保留并使用源图像的 alpha 透明度信息。如果你忽略 alpha，透明 GIF 或 PNG 中可能存在的任何透明度都可能被破坏。

最后，在方法末尾，返回 GD 图像资源。

#### 旋转图像

除了在服务器端调整图像大小外，常见的图像编辑需求还包括在上传后旋转图像的能力。为了实现此操作，你将像之前一样创建另一个图像操作类文件，并添加另一个方法在 `WebImage` 中调用该功能。

首先，创建一个名为 `class.ImageRotate.php` 的文件，并在其中创建以下图像旋转类：

```php
<?php

class ImageRotate
{
    public $rotation = 0;

    // Rotate the image
    public function process($gd_img)
    {
        if ($this->rotation)
        {
            // Get "filler" background color
            $color = imagecolorallocate($gd_img, 255, 255, 255);

            // Rotate the image
            $gd_img = imagerotate($gd_img, $this->rotation, $color);
        }

        return $gd_img;
    }
}
?>
```

然后，将以下方法添加到 WebImage 类定义中：

```php
// Rotate the image
public function rotate($degrees)
{
    require_once 'class.ImageRotate.php';

    $ir = new ImageRotate();

    // Set rotate parameters
    $ir->rotation = $degrees;

    // Perform the rotation
    $this->gdresource = $ir->process($this->gdresource);
}
```

这个比缩放方法简单一些，但非常相似。WebImage 的 `rotate()` 方法接受一个参数：你要旋转图像的角度。与 `resize()` 类似，`rotate()` 包含必要的类文件，设置旋转参数，然后执行旋转。

在 ImageRotate 内部，这相当简单。`process()` 方法检查是否提供了旋转值，然后获取一种颜色用作背景色。如果你旋转 90、180 或 270 度，你不会看到该颜色，但如果你使用其他任何值，图像将扩展以包围倾斜后的原始图像，背景色将填充旋转源未覆盖的区域。设置颜色后，使用 `imagerotate()` 函数旋转图像：

```php
// Rotate the image
public function process($gd_img)
{
    if ($this->rotation)
    {
        // Get "filler" background color
        $color = imagecolorallocate($gd_img, 255, 255, 255);

        // Rotate the image
        $gd_img = imagerotate($gd_img, $this->rotation, $color);
    }

    return $gd_img;
}
```

当然，最后在末尾返回图像资源。

#### 添加说明文字

接下来是简单图像功能系列的下一项：为图像添加说明文字——图像底部变暗的区域，上面叠加说明或简短文字。这是一种微妙的方式，用于包含和显示关于图像或其背景的一些信息，而无需将文本与图像分开，也不至于碍事。

首先，遵循 ImageResize 和 ImageRotate 的示例，创建一个名为 `class.ImageCaption.php` 的文件：

```php
<?php

class ImageCaption
{
    public $caption = '';
    public $fontfile = '';
    public $fontsize = 10;
    public $padding = 5;
    public $drawline = true;

    // Caption the image
    public function process($gd_img)
    {
        if ($this->caption and $this->fontfile)
        {
            // Get text box height
            $text_box = imagegetbbox($this->fontsize,
                                     0,
                                     $this->fontfile,
                                     $this->caption);
            $text_height = $text_box[3] - $text_box[5];
            $text_underscoreline = $text_box[3];

            // Get some image dimensions
            $img_x = imagesx($gd_img);
            $img_y = imagesy($gd_img);

            // Draw background shading
            imagealphablending($gd_img, true);
            ...
```





```php
$rect_color = imagecolorallocatealpha($gd_img, 0, 0, 0, 75);
imagefilledrectangle($gd_img,
                     0,
                     $img_y - $text_height - {$this->padding * 2},
                     $img_x,
                     $img_y,
                     $rect_color);

// Draw caption text
$text_color = imagecolorallocate($gd_img, 255, 255, 255);
imagefttext($gd_img,
            $this->fontsize,
            0,
            $this->padding,
            $img_y - $text_underbaseline - $this->padding,
            $text_color,
            $this->fontfile,
            $this->caption);

// Draw shading border if requested
if ($this->drawline)
{
    $line_color = imagecolorallocatealpha($gd_img,
                                          200,
                                          200,
                                          200,
                                          75);
    imageline($gd_img,
               0,
               $img_y - $text_height - {$this->padding * 2} - 1,
               $img_x,
               $img_y - $text_height - {$this->padding * 2} - 1,
               $line_color);
}
return $gd_img;
}
?>
```

接下来，与之前一样，在 WebImage 类定义的末尾添加一个新方法，如下所示：

```php
// Add a caption to the image
public function caption($text,
                       $font,
                       $size = null,
                       $padding = null,
                       $drawline = null)
{
    require_once 'class.ImageCaption.php';

    $ic = new ImageCaption();

    // Set size, padding, line if needed
    if ($size)
    {
        $ic->fontsize = $size;
    }
    if ($padding != null)
    {
        $ic->padding = $padding;
    }
    if ($drawline != null)
    {
        $ic->drawline = $drawline;
    }

    // Set font, caption
    $ic->fontfile = $font;
    $ic->caption = $text;

    // Perform the captioning
    $this->gdresource = $ic->process($this->gdresource);
}
```

当你调用 `WebImage` 的 `caption()` 方法时，最多可以使用五个参数。前两个是必需的，分别指定要在字幕中显示的文本，以及用于字幕文本的 TrueType 字体文件（`.ttf`）的文件名。其他参数设置字体的像素大小、文本周围填充的像素量，以及是否要在字幕上方绘制一条淡淡的线条。该方法包含所需的类定义文件，整理参数值，然后调用 `ImageCaption` 的 `process()` 方法。

`process()` 所做的就是确定要写入的文本尺寸以及目标图像本身的尺寸。为了获取渲染文本的尺寸，使用了 `imagettfbbox()`。`imagettfbbox()` 接受四个参数：字体大小、字体角度、用于渲染文本的 TrueType 字体文件以及文本本身。在确定文本边界框信息后，实际高度被设置为 `$text_height`，并确定文本相对于基线下沉的量——对于像小写字母 *g* 和 *p* 这样的字母。代码如下：

```php
// Caption the image
public function process($gd_img)
{
    if ($this->caption and $this->fontfile)
    {
        // Get text box height
        $text_box = imagettfbbox($this->fontsize,
                                0,
                                $this->fontfile,
                                $this->caption);
        $text_height = $text_box[3] - $text_box[5];
        $text_underbaseline = $text_box[5];

        // Get some image dimensions
        $img_x = imagesx($gd_img);
        $img_y = imagesy($gd_img);
```

接下来，在图像上绘制一个背景阴影框，以提供一个较暗的区域，帮助显示稍后将在方法顶部写入的白色文本。首先，告知 GD 在目标图像上正确混合透明度。然后，使用 `imagecolorallocatealpha()` 获取一个颜色资源——在这种情况下是黑色（0,0,0），大约 60% 的透明度（alpha 通道的范围是 0–127）。最后，使用半透明黑色颜色在图像底部绘制一个填充矩形，其高度足以覆盖完整的字体高度以及可能指定的填充量：

```php
// Draw background shading
imagealphablending($gd_img, true);
$rect_color = imagecolorallocatealpha($gd_img, 0, 0, 0, 75);
imagefilledrectangle($gd_img,
  0,
  $img_y - $text_height - ($this->padding * 2),
  $img_x,
  $img_y,
  $rect_color);
```

在图像上绘制背景矩形后，是时候在顶部添加字幕文本了。只需为文本分配一种颜色——在这种情况下是白色——然后使用 `imagettftext()` 在图像上绘制文本：

```php
// Draw caption text
$text_color = imagecolorallocate($gd_img, 255, 255, 255);
imagettftext($gd_img,
  $this->fontsize,
  0,
  $this->padding,
  $img_y - $text_underbaseline - $this->padding,
  $text_color,
  $this->fontfile,
  $this->caption);
```

`imagettftext()` 函数使用八个参数：要添加文本的图像资源、字体大小、文本角度、开始绘制文本的 x 坐标、文本基线/底部的 y 坐标、文本颜色、.ttf 字体文件名，以及要渲染的实际文本，按此顺序排列。

字幕的最后部分仅使用半透明浅灰色和 `imageline()` GD 函数在字幕框的顶部绘制一条淡淡的边框：

```php
// Draw shading border if requested
if ($this->drawline)
{
  $line_color = imagecolorallocatealpha($gd_img,
    200,
    200,
    200,
    75);

  imageline($gd_img,
    0,
    $img_y - $text_height - ($this->padding * 2) - 1,
    $img_x,
    $img_y - $text_height - ($this->padding * 2) - 1,
    $line_color);
}
```

# 第 10 章

```php
)
return $gd_img;
```

#### 添加 Logo

你要添加到 `WebImage` 类的最后一项功能是能够在图像上放置 logo 或水印。

首先创建 `class.ImageLogo.php` 文件：

```php
<?php

class ImageLogo
{
    public $logoFile;
    public $ratio = 1;
    public $location = array('x' => '', 'y' => '');
    public $padding = 0;

    public function process($gd_img)
    {
        if ($this->logoFile)
        {
            require_once 'class.WebImage.php';

            // Load the logo
            $logo = new WebImage();
            $logo->load($this->logoFile);

            // Resize logo if needed
            if ($this->ratio and $this->ratio != 1)
            {
                $logo->resize($this->ratio);
            }

            // Determine logo placement (x)
            switch ($this->location['x'])
            {
                case 'l':
                    $logo_x = $this->padding;
                    break;
                case 'r':
                    $logo_x = imagesx($gd_img) -
                              $this->padding -
                              imagesx($logo->gdresource);
                    break;
                default:
                    $logo_x = round((imagesx($gd_img) / 2) -
                                    (imagesx($logo->gdresource) / 2));
            }

            // Determine logo placement (y)
            switch ($this->location['y'])
            {
                case 't':
                    $logo_y = $this->padding;
                    break;
                case 'b':
                    $logo_y = imagesy($gd_img) -
                              $this->padding -
                              imagesy($logo->gdresource);
                    break;
                default:
                    $logo_y = round((imagesy($gd_img) / 2) -
                                    (imagesy($logo->gdresource) / 2));
            }

            // Copy the logo onto the main image
            imagecopy($gd_img,
                      $logo->gdresource,
                      $logo_x,
                      $logo_y,
                      0,
                      0,
                      imagesx($logo->gdresource),
                      imagesy($logo->gdresource));
        }
        return $gd_img;
    }
}
?>
```

接下来，在 WebImage 类定义的末尾添加 logo() 方法：

```php
public function logo($logoFile,
$loc_x = null,
$loc_y = null,
$padding = null,
$ratio = null)
{
require_once 'class.ImageLogo.php';

$il = new ImageLogo();

// Set logo file
$il->logoFile = $logoFile;

// Set location, padding, and ratio if needed
if ($loc_x !== null)
{
$il->location['x'] = $loc_x;
}
if ($loc_y !== null)
{
$il->location['y'] = $loc_y;
}
```



	if ($padding !== null)
	{
		$il->padding = $padding;
	}
	if ($ratio !== null)
	{
		$il->ratio = $ratio;
	}

	// Perform the logo placement
	$this->gdresource = $il->process($this->gdresource);
	}
```

与添加到 WebImage 的其他操作处理方法类似，`logo()` 简单地接收提供的参数——标志文件名、位置 x、位置 y、像素填充量以及标志的缩放比例——在 ImageLogo 中设置所需的属性，并处理标志的应用。

在 ImageLogo 的 `process()` 函数内部，你可以确切看到标志应用过程中发生了什么。`process()` 方法首先创建其自身的内部 WebImage 对象，用于加载标志文件并在需要时对其进行缩放。创建并加载 WebImage 后，如果指定了比例，则会对标志图像进行缩放：

```php
public function process($gd_img)
{
	if ($this->logo_file)
	{
		require_once 'class.WebImage.php';

		// Load the logo
		$logo = new WebImage();
		$logo->load($this->logo_file);

		// Resize logo if needed
		if ($this->ratio and $this->ratio != 1)
		{
			$logo->resize($this->ratio);
		}

		// Determine logo placement (x)
		switch ($this->location['x'])
		{
			case 'l':
				$logo_x = $this->padding;
				break;
			case 'r':
				$logo_x = imagesx($gd_img) -
						$this->padding -
						imagesx($logo->gdresource);
				break;
			default:
				$logo_x = round((imagesx($gd_img) / 2) -
						(imagesx($logo->gdresource) / 2));
		}

		// Determine logo placement (y)
		switch ($this->location['y'])
		{
			case 't':
				$logo_y = $this->padding;
				break;
			case 'b':
				$logo_y = imagegy($gd_img) -
						$this->padding -
						imagegy($logo->gdresource);
				break;
			default:
				$logo_y = round((imagegy($gd_img) / 2) -
						(imagegy($logo->gdresource) / 2));
		}

		// Copy the logo onto the main image
		imagecopy($gd_img,
			$logo->gdresource,
			$logo_x,
			$logo_y,
			0,
			0,
			imagesx($logo->gdresource),
			imagegy($logo->gdresource));
	}

	return $gd_img;
}
```

请注意，这里使用的是 `imagecopy()` 而不是 `imagecopymerge()`。`imagecopymerge()` 函数似乎更适合此任务，它甚至提供了合并标志并设置透明度的功能——这对于某些水印效果非常有用。不幸的是，`imagecopymerge()` 有一个讨厌的习惯，会破坏源标志图像本身的大部分透明信息，因此如果你想为图像制作一个淡淡的半透明水印，最好直接在标志图像本身添加透明度，并使用 `imagecopy()`，而不是使用不透明图像和 `imagecopymerge()`。

#### 测试运行

为了全面测试这一系列图像处理代码，你需要几样东西：一个要处理的主图像、一个用作标志叠加的图像，以及一个 TrueType 字体文件。准备好这三样东西后，创建一个 PHP 脚本，使用你创建的类来操作这些图像。首先只需加载你的图像，并在浏览器中显示它：

```php
<?php

require_once 'class.WebImage.php';

$img = new WebImage();
$img->load('base.png');
$img->display();
?>
```

在浏览器中加载此文件，它应该显示你的图像，如图 10.1 所示。

![](img/ab27c6ac898db1f934d39fa127b14657_283_0.png)

**图 10.1**

如果你想在保存或显示之前更改图像的类型，只需在 `WebImage` 对象中设置图像类型即可：

```php
<?php

require_once 'class.WebImage.php';

$img = new WebImage();
$img->load('base.png');
$img->type = 'image/gif';
$img->display();

?>
```

要调整图像大小，请调用 WebImage 的 resize() 函数。以下代码使用了 0.75 的比例：

```php
<?php

require_once 'class.WebImage.php';

$img = new WebImage();
$img->load('base.png');
$img->resize(0.75);
$img->display();

?>
```

输出的一个示例如图 10.2 所示。

![](img/ab27c6ac898db1f934d39fa127b14657_284_0.png)

接下来，旋转你的图像。以下代码使用 180 度进行旋转：

```php
<?php
require_once 'class.WebImage.php';

$img = new WebImage();
$img->load('base.png');
$img->rotate(180);
$img->display();
?>
```

在浏览器中加载脚本，其外观如图 10.3 所示。

![](img/ab27c6ac898db1f934d39fa127b14657_285_0.png)

**图 10.3**

现在，为图像添加标题。此示例使用字体“Fuji Wide Normal”，但你可以使用任何你手头可用的字体，只要它是 TrueType 字体文件 (.ttf)：

```php
<?php
require_once 'class.WebImage.php';
$img = new WebImage();
$img->load('base.png');
$img->caption('An example of plantlife found on Maui.',
    'FUJIWIDR.TTF',
    15,
    5,
    true);
$img->display();
?>
```

如果一切按计划进行，你应该会看到类似图 10.4 的效果。

![](img/ab27c6ac898db1f934d39fa127b14657_286_0.png)

**图 10.4**

# 第 10 章

最后，尝试应用图像标志。在此示例中，你将在图像的右下角放置一个标志，位于标题框之上：

```php
<?php

require_once 'class.WebImage.php';

$img = new WebImage();
$img->load('base.png');
$img->caption('An example of plantlife found on Maui.',
	'FUJIWIDR.TTF',
	13,
	5,
	true);

$img->logo('logo.png', 'e', 'b', 5, 0.3);
$img->display();
?>
```

现在，应该会显示一个标志，略微缩放，位于右下角，带有 5px 的填充量，如图 10.5 所示。

![](img/ab27c6ac898db1f934d39fa127b14657_287_0.png)

**图 10.5**

由此可见，使用 GD 库并不难，它允许你对图像拥有相当多的灵活性和控制权。还有许多其他更高级的功能可以使用，所有这些都可以在 PHP 手册的 GD 部分找到（http://www.php.net/gd）。

### Ming

Ming 是一个第三方 PHP 扩展，允许用户在不实际使用 Macromedia Flash 工作室的情况下创建 Shockwave Flash 文件。Ming 提供的功能并不总是与 Macromedia Flash 中可用的功能相同，这是因为使用 PHP 和 Ming 创建 Flash 文件的方式特性所致。Ming 确实提供了一种低成本创建 Flash 文件的方法，并允许在需要时动态创建内容。

#### 关于 Ming

动态创建的 Flash 文件的实用性有时可能会被人忽视，特别是因为你无法像使用 Macromedia Flash Studio 的人那样对内容布局进行精确的视觉控制。此外，Ming 的功能集仅限于 Flash 4 版本，这比最新可用版本落后了好几个版本。但是，能够编写脚本来创建应用并为其添加动态内容，这是使用 Macromedia Flash Studio 无法做到的。这在需要 Flash 功能但又希望为用户个性化内容的分发场景中非常有用。

Ming 本身实际上是一个第三方扩展，已经为它编写了 PHP 包装扩展，因此在构建二进制文件时需要将其编译到 PHP 二进制文件中。关于如何在 PHP 中安装 Ming 的说明可以在 PHP 网站上找到（http://www.php.net/ming）。有关 Ming 本身的更多信息可以在 SourceForge.Net 上的 Ming 站点找到（http://ming.sourceforge.net）。互联网上还有许多教程和示例，可以帮助说明 Ming 的功能，并提供适合用作构建 Flash 影片基础的代码片段。

Ming 在 PHP 中实现为对象，因此在 PHP 中任何时候使用 Ming 创建 shockwave 文件时，至少需要实例化一个 SWFmovie 对象。以下是使用 Ming 和 PHP 生成的一个非常简单的文件的代码。要运行此代码，请将其插入到一个没有其他内容的 PHP 文件中，然后在安装了 Flash 插件的 web 浏览器中查看该文件：

```php
<?php
header('Content-type: application/x-shockwave-flash');
$a=new SWFmovie();
$a->setDimension(100,100); //width and length in that order
$a->setBackground(0,0,255); // red, green, and blue integers
$a->output();
?>
```

这并不会生成很多内容，但它会在你的浏览器中生成一个巨大的蓝色屏幕。检查代码，你可以看到使用 Ming 创建的任何 Flash 文件都需要包含的一些必要部分。第一行告诉 PHP 设置 Content-type 头，以便浏览器知道这是一个 shockwave 文件并加载相应的插件。下一行实际创建 SWFMovie 对象的实例。接下来的两行是可选的，但如果没有它们，将很难知道生成了什么，因为它们设置了 shockwave 文件的大小并将其背景设为蓝色。最后一行告诉 PHP 将 Ming 生成的文件输出到浏览器。真正需要做的唯一一件事




在此需要确保的是，在输出电影之前设置正确的 `Content-type` 请求头，并确保没有向浏览器发送其他内容，例如多余的行或空白字符。

只能存在一个 `SWFMovie` 对象实例，但你可以在一个 `SWFMovie` 对象中包含多个迷你电影。为了实现这一点，你需要使用另一个对象，即 `SWFSprite` 对象。该对象具有与 `SWFMovie` 对象相似的特性和属性，但不受限于每部电影只能有一个。这种设计的优势在于，你可以在同一个 Flash 电影中同时显示多个动画。每个动画甚至可以以不同的速率运行，并且具有不同的时长。

Flash 文件使用*帧*，就像电影或动画中的帧一样。`SWFMovie` 和 `SWFSprite` 对象都具有用于添加新帧的功能。帧的用处在于，你可以通过将不同对象包含在特定帧中，从而在屏幕上显示它们。这意味着，如果你希望同时显示两个或更多对象，它们需要拥有共同的帧。一旦对象被添加到某个帧中，其后所有的帧都包含该对象，直到该对象从电影中移除为止。此外，就像电影或动画一样，你可以向前或向后移动，也可以使用 `SWFAction` 对象跳转到特定帧。这种对帧的使用提供了一种更好的方式来组织对象，并在你的 Flash 电影中生成时间轴。

Ming 和 Flash 都使用一种可能与你习惯不同的坐标系。Flash 使用的距离单位是 twip（缇）。twip 被定义为恰好 1 英寸的 $\frac{1}{1440}$ 或 1 点的 $\frac{1}{20}$。这个度量单位通常简化为 1 像素等于 20 twip 单位，以便于转换。然而，这可能是一个任意值，因为 Flash 播放器会将电影缩放至播放器窗口本身的大小。幸运的是，Ming 中包含的 `SWFBitmap` 对象具有确定图像在 twip 单位下大小的功能。因此，如果你需要基于图像大小来设置电影维度，只需创建 `SWFBitmap` 对象，读取其宽度和高度值，然后基于此设置电影本身的维度。电影的维度并不一定需要在显示之前设置。

#### Ming 中的对象

PHP 总共提供了 13 种对象，用于通过 Ming 生成 Flash 文件。你可以组合使用这些对象，创建具有多种复杂功能的 Flash 文件。它们如下所示：

-   `SWFAction` 对象允许你在 Flash 文件中添加超越简单图像显示的逻辑和功能。使用 `SWFAction`，你可以移动图像和形状以实现游戏等功能，也可以读取和设置 Flash 文件中对象的属性。此外，你可以包含一些 ActionScript 脚本，这是 Flash 版本的 JavaScript，与之非常相似。该对象通常与 `SWFButton` 对象一起使用，以在用户按下按钮时执行某些操作。常用的操作是根据用户的响应在 Flash 电影中显示特定帧。
-   `SWFBitmap` 对象允许将图像添加到 Flash 文件中。不过，存在一些限制，因为只有非渐进扫描 JPEG 图像和 DBL（“define bits lossless”，定义无损位）图像可以以此方式添加。其他图像需要使用其他扩展（如 GD）或通过系统调用工具转换为这些格式之一。此对象常与 `SWFSprite` 和 `SWFShape` 对象一起使用。
-   `SWFButton` 对象向你的 Flash 文件添加一个按钮。此按钮可用于触发 `SWFAction` 对象的操作。它响应常见的鼠标操作，如下MouseDown、mouseUp 和 rollover。可以为按钮添加形状以改变其外观。
-   `SWFDisplayItem` 对象允许在将形状、文本对象、精灵或按钮添加到电影后，通过引用其添加后返回的句柄来操作该项目。扭曲、缩放和移动项目等都是可能的操作。
-   `SWFFill` 对象通过 `SWFShape` 对象的 `addFill` 方法生成。它允许通过旋转、扭曲和缩放形状填充来转换填充效果。
-   `SWFFont` 对象加载字体以供 `SWFText` 对象使用。该字体可以是字体定义块（FDB）或浏览器定义的字体引用。
-   `SWFGradient` 对象创建渐变，然后可以通过 `SWFShape` 方法 `addFill()` 使用。
-   `SWFMorph` 将取两个形状，并将第一个形状变形为第二个形状。这可用于一些基本动画。
-   `SWFMovie` 对象是其他所有对象正常工作所必需的唯一对象，因为它是实际将 Flash 文件写入文件或浏览器的对象。
-   `SWFShape` 对象生成形状。形状实际上是通过传递由虚拟画笔绘制的坐标来绘制的。通过合适的坐标，几乎可以生成任何形状。此外，如前所述，它与 `SWFBitmap` 对象一起使用，以向电影添加图像文件。
-   `SWFSprite` 对象通过向对象添加帧来生成“电影片段”或动画。帧包含其他对象之一，例如 `SWFShape`。单个帧中可以有多个 `SWFSprite` 对象，以便可以看到两个动画同时进行。与仅使用 `SWFMovie` 对象相比，将图像添加到 `SWFSprite` 对象的优势在于它更好地封装了对象，便于操作。
-   `SWFText` 对象在 Flash 动画中显示文本。如果你只需要显示少量静态信息，使用 `SWFText` 对象的替代方法是直接使用图像，而不是使用 Flash 来书写文本。
-   `SWFTextField` 类似于 `SWFText` 对象，但有一些不同。`SWFTextField` 对象不能旋转或扭曲，但可以用作表单输入。

#### 创建 Flash 显示

再添加几行代码，你就可以将前面的示例扩展为稍具吸引力的内容：

```php
<?php
header('Content-type: application/x-shockwave-flash');
$m = new SWFMovie(0);
$m->setDimension(100,100); //width and length in that order
$m->setBackground(0,0,255); // red, green, and blue integers

$s = new SWFShape();  //generate a shape object
$s->setLine(4, 30, 60, 100); //set the line width to 4 along
// with red, green, and blue integer values
$s->setLineFill($s->addFill(300, 200, 100));
//set the color of the shape with red, green
// and blue integer values
$s->movePenTo(20, 20);
//move our imaginary pen to a new location
$s->drawLineTo(20, 80);
//draw lines to a new set of points
$s->drawLineTo(80, 80);
$s->drawLineTo(80, 20);
$s->drawLineTo(20, 20);
$m->add($s); //add the shape to the movie

$m->nextFrame(); //advance a frame in the movie
$m->output(); //output everything to the browser
?>
```

第 10 章

该电影生成的输出并不特别，但它演示了一些重要对象的一些基本方法。输出结果应该是蓝色背景，中间有一个绿色正方形。

为了更深入地展示 Ming 的功能，你将使用它生成一个幻灯片演示。为了简化操作，你将使用尺寸和形状完全相同的图像，并且所有图像都有明确的命名。创建一个新文件并包含以下代码行：

```php
<?php
//create a movie object
$movie = new SWFMovie();
//set the background to white
$movie->setBackground(255, 255, 255);

//images to display
$images = array("1.jpg", "2.jpg", "3.jpg");

$bitmapImage = new SWFBitmap(fopen($images[0], "r+b"));
$w = $bitmapImage->getWidth();
$h = $bitmapImage->getHeight();
```

创建一个 `SWFSprite`，它将作为幻灯片中的迷你电影，实际上将由用户控制。为了防止它只是显示所有图像，向其添加了一个默认的 `stop()` 操作。此外，电影的大小是根据图像大小计算的，并预留了额外空间以便在图像下方添加按钮。代码如下：

```php
//create a sprite which will act as a mini movie
$sprite = new SWFSprite();
//add stop action to the first frame
$sprite->add(new SWFAction("stop();"));

//set the size of the movie with extra space for buttons
$movie->setDimension((1*$w),(1.5*$h+30));
```




现在，需要将每张图片添加到精灵中，通过遍历数组可以轻松实现这一点。首先，每张图片被转换为 SWFBitmap 对象，然后作为填充添加到 SWFShape 对象中。在形状的周围绘制一条线后，该形状会被添加到 SWFSprite 对象中，随后 SWFSprite 对象进入下一帧：

```php
//loop through all of the images
for($i=0; $i<count($images);$i++){

//create a bitmap from an image
$bitmapImage = new SWFBitmap(open($images[$i], "rb"));

//create a shape object to hold the image
$shape = new SWFShape();

//generate the fill for the shape of the image
$fill = $shape->addFill($bitmapImage);

//add the fill to the shape
$shape->setRightFill($fill);

//draw a line around the shape to set the size
$shape->drawLine($w, 0);
$shape->drawLine(0, $h);
$shape->drawLine(-$w, 0);
$shape->drawLine(0, -$h);

//add the shape to the sprite so that it is displayed
$sprite->add($shape);

//generate a new frame and go to it
$sprite->nextFrame();
}
```

由于精灵不会自动返回到第一帧，因此需要在最后一帧添加一个动作，使其跳转到第一帧。gotoFrame() 动作接受一个帧号作为参数；此处使用帧 0，因为它是精灵中的第一帧。然后，精灵中会再添加一帧，以确保所有内容都包含在 SWFSprite 对象中：

```php
//goto frame 0
$sprite->add(new SWFAction('gotoFrame(0);'));
//again generate a new frame
$sprite->nextFrame();
```

现在精灵已经制作完成，需要将其添加到 SWFMovie 对象中。当将其添加到电影时，它会返回一个句柄，该句柄可以作为对精灵的引用，以便对其进行控制。为其分配一个名称，并使用该句柄将精灵移动到指定位置：

```php
//add the sprite and get its handler
$handler = $movie->add($sprite);
//we can name the sprite now with the handler
$handler->setName("images");
//we can move the sprite also with the handler
$handler->moveTo(0,2);
```

# 第 10 章

为了创建一个用于控制幻灯片的按钮，需要创建一个新的 SWFShape 对象并为其添加一个按钮图像：

```php
//create a shape again
$shape = new SWFShape();
//create another bitmap this time for a button image
$btmmapImage = new SWFBitmap(fopen("button.jpg", "rb"));
$fill = $shape->addFill($btmmapImage);
$shape->setRightFill($fill);
//create the border around the shape
$shape->drawLine(0, 0);
$shape->drawLine(0, $h);
$shape->drawLine(-$w, 0);
$shape->drawLine(0, -$h);
```

实例化一个 SWFButton 对象，并将按钮形状添加到该 SWFButton 对象中。还为按钮设置了默认标志，这使得程序可以根据按钮是否被按下以及鼠标是否悬停在按钮上来执行操作。另外，还向按钮添加了一个动作，用于将精灵移动到下一帧。

```php
//now actually create a button object
$button = new SWFButton();
//add the shape to the button with all of its default flags which are
//all actually predefined integer values
$button->addShape($shape, SWFBUTTON_HIT |
SWFBUTTON_UP | SWFBUTTON_DOWN |
SWFBUTTON_OVER);
//add an action to go to the next frame
//on the sprite. The sprite is referenced by "/images"
$button->addAction(new SWFAction("setTarget('/images');
nextFrame();"), SWFBUTTON_MOUSEDOWN);
```

然后将按钮添加到电影中，并返回句柄。接着，将按钮移动到图片正下方，并为电影添加一帧。然后生成必要的浏览器头信息，并输出该电影。

```php
//add the button to the movie and save the returned handler
$handler = $movie->add($button);
//use the handler to move the button below the images
$handler->moveTo(0,$h+3);
$movie->nextFrame();
//send the appropriate header to the browser
header('Content-Type:application/x-shockwave-flash');
//output the movie to the browser
$movie->output();
?>
```

在使用 Ming 时，有几件事需要注意。首先，当你直接输出到浏览器时，必须在调用 SWFMovie 对象的 output() 方法之前发送 Content-Type 头。这会发送正确的 HTTP 头信息，使浏览器知道需要加载 Shockwave Flash 插件。这也导致了另一种可能发生的错误：输出除了 Content-Type 头以外的任何内容，例如空行。输出除头和电影本身之外的其他内容会导致文件损坏，从而使浏览器无法正确显示该文件。此外，预先构想好最终输出的大致布局也很有帮助。为了有助于布局使用 Ming 创建的 Flash 电影，你可以使用提供坐标系的图形程序，或者干脆使用普通的方格纸。

### SimpleXML

如今，XML 无处不在，因此提供一种简单的方式来获取和解析这些文件是有道理的。幸运的是，PHP 为我们提供了一个用于利用 XML 数据的 XML 接口，即一个简单易用的扩展：SimpleXML。SimpleXML 默认已安装，但如果你不打算使用它，建议在 php.ini 中禁用它。需要注意的是，SimpleXML 也需要 PHP5。

正如名称所示，该扩展的目的是在非常基本的层面上访问 XML 文档。为了说明实现这一点的简便性，创建一个包含海滨租赁信息的虚拟 XML 文件（该文件将用于所有示例）：

```xml
<?xml version="1.0" ?>
<rentals>
<description>
<name>The Bayfront</name>
<type>condo</type>
<view>oceanfront</view>
<space>1200 square feet</space>
<location>Wrightsville Beach</location>
<price>1000 per week</price>
<bed_bath>3 bedrooms, 2 bathrooms</bed_bath>
</description>
<description>
<name>Paradise</name>
<type>house</type>
<view>oceanfront</view>
<space>1000 square feet</space>
<location>Wrightsville Beach</location>
<price>900 per week</price>
<bed_bath>2 bedrooms, 2 bathrooms</bed_bath>
</description>
</rentals>
```

既然你已经有了 XML 文件，获取信息并将其放入对象中（使用 simplexml_load_file() 函数），以便对其进行操作：

```php
<?php
if (file_exists('beachfront.xml')) {
    $data = simplexml_load_file('beachfront.xml');
    print_r($data);
}
?>
```

你可以遍历该对象并妥善地显示结果（或者至少以更可读的格式显示）。在 simple.php 中添加以下更改：

```php
<?php
if (file_exists('beachfront.xml')) {
    $data = simplexml_load_file('beachfront.xml');

    foreach($data as $main) {
        echo "<hr>";
        foreach ($main as $k => $v) {
            echo $k . ": " . $v . "<br />";
        }
    }
}
?>
```

除了 simplexml_load_file() 之外，还有一系列与 SimpleXML 扩展配合使用的其他函数。simplexml_load_string() 将 XML 文档作为字符串加载。你必须首先将其内容赋值给一个变量；然后可以使用 simplexml_load_string() 函数将变量的内容解析为对象供你使用。如果你想要操作你的对象，然后将其内容以 XML 文件的形式显示回浏览器，可以使用 $obj->asXML() 函数。如果你需要查看元素的属性或对象任何节点的子节点，attributes() 和 children() 函数会很有帮助。如果你想将 DOM 文档中的 DOM 节点转换为 SimpleXMLElement 对象，simplexml_import_dom() 函数会很有帮助。

xpath() 函数允许你在 XML 文档中搜索特定的字符串。它使用 W3C 的 XPath 来评估 XML 文档中的每个节点，之所以被称为“XPath”是因为搜索关键词类似于文件的路径，因为每个元素都以类似的方式嵌套。如果你希望阅读更多关于 XPath 的内容，请访问 W3C 关于此主题在 http://www.w3.org/TR/xpath 上的文档。

如果你只想执行最简单的查询，这就足够了，如下面的示例所示：

```php
<?php
if (file_exists('beachfront.xml')) {
    $data = simplexml_load_file('beachfront.xml');

    //find and list all the “locations” in our XML file
    //”locations” are under “descriptions” which are under “rentals”
    $find = $data->xpath('/rentals/description/location');

    while (list(, $v) = each($find)) {
        echo $v. "\n";
    }
}
?>
```

此脚本将给出 XML 文件中介名为“location”的所有节点的值。如果你想进一步深入查询，就必须使用另一种方法。记住，这是 SimpleXML，而不是 ComplexXML。

SimpleXML 提供了一种非常快速且直接的方法来访问简单的 XML 文档。它并不允许太多的灵活性，并且仅适用于最简单的 XML 文件。例如，如果你尝试在内容中包含 HTML 代码的 XML 文件上运行这些函数，会遇到问题。除此之外，与当前可用的许多其他 XML/PHP 接口相比，这个要容易使用得多。





### 摘要

尽管本章只涉及其中的一小部分，但可供使用的 PHP 扩展还有很多。完整的列表可在 PHP 手册（[http://www.php.net](http://www.php.net)）中找到。以下是一些你可能需要特别关注的扩展：

- CURL（客户端 URL 库函数）：允许你使用除 http 之外的许多不同协议（如 SSL、FTP 和 gopher）连接到页面。
- DOM：使用 DOM API 与 XML 文档交互，并随 PHP 默认安装一起提供。
- SOAP：使用 GNOME XML 库启用创建 SOAP 服务器和客户端。
- ZIP 扩展（Bzip2, rar, Zip, Zlib）：启用读取 zip 文件，每个扩展处理不同类型的压缩文件。

通过对 PHP 扩展的这种初步体验，我们希望你能有信心去探索 PHP 中那些鲜为人知但同样有用的功能。

# 11 AJAX

典型的 Web 应用程序通过表单与用户进行交互。服务器向客户端发送一个表单，用户输入响应，然后表单被提交回服务器进行处理。表单处理完成后，服务器会响应一个新的完整页面，该页面的构成通常取决于用户上一次的表单提交。在与用户的每次交互中，都需要一个全新的页面。此类应用程序必须使用带宽，即使这些元素在前面的响应中已发送到客户端，但每次页面请求时都会传输恒定的页面元素（例如站点导航）。此外，此类应用程序比桌面应用程序慢，因为在处理一个交互的结果以及新页面加载完成之前，Web 应用程序是无响应的。

AJAX（Asynchronous JavaScript and XML）指的是一组技术，允许创建胖客户端 Web 应用程序，在这种应用中，应用程序处理的相关较大比例责任被交给客户端。具体来说，AJAX 应用程序通常使用 XHTML 和 CSS 进行语义标记和展示，使用 XML 格式化将在客户端和服务器之间交换的数据，并使用 JavaScript 与服务器通信并操作文档对象模型（DOM）。使用 AJAX 时，客户端和服务器之间的通信可以仅限于数据，因为客户端具备处理展示和用户交互所需的必要功能。此外，这种通信是异步进行的，且无需刷新页面。这使得应用程序的客户端部分即使在数据与服务器交换时也能保持响应状态。如果用户执行了一个需要向服务器发送请求的操作，该请求可以发送，并且应用程序可以在等待响应的同时处理进一步的交互（甚至可以发出更多请求）。这一概念在图 11.1 中有所说明。

今天最流行的 AJAX 应用可能是谷歌的 GMail（[http://www.gmail.com](http://www.gmail.com)），这是一款基于 Web 的电子邮件客户端。在传统的基于 Web 的电子邮件客户端中，用户的几乎所有操作都会导致整个页面或框架的刷新。由于 GMail 采用了 AJAX，页面永远不会刷新。相反，接口是通过基于用户与应用程序的交互以及与 GMail 服务器的 XML 通信，利用 JavaScript 操作 DOM 来动态更新的。例如，这允许用户撰写电子邮件，点击发送，并在 GMail 服务器处理实际发送的消息时继续阅读其电子邮件。在读取其余电子邮件时，该用户将收到一条状态消息，表明消息已成功发送。

### 传统 Web 应用程序

![](img/ab27c6ac898db1f934d39fa127b14657_299_0.png)

### AJAX Web 应用程序

![](img/ab27c6ac898db1f934d39fa127b14657_299_1.png)

图 11.1

### 历史

AJAX 本身并不新鲜；其背后的理念也是如此。事实上，过去已经开发并使用了许多无需页面刷新即可与服务器通信的方法。

### 图像源技巧

JavaScript 允许使用 Image 对象动态加载图像。当创建一个图像并设置其 src 属性时，浏览器会发送对该图像的请求，并尝试将响应封装在图像对象中。开发人员已使用此方法通过将 src 属性设置为服务器端脚本的 URI，并将数据通过查询字符串传递给服务器，从而实现与服务器的单向通信。服务器端脚本随后可能会更新数据存储。通常，响应中不会返回任何图像，但这并不会造成问题，因为开发人员并未将 Image 对象用于其预期目的。

这种技术的优点包括：

- 它允许在不刷新的情况下向服务器发送数据。
- 它可以通过读取对象的属性来确定请求何时完成。

然而，它也有一些缺点：

- 它无法从服务器接收非图形数据（通信是单向的）。
- 它无法检测或处理在尝试通信期间可能发生的 HTTP 错误。

### 隐藏框架

许多开发人员发现图像源技巧不够用，需要能够在发送数据的同时接收来自服务器的信息。由此出现了隐藏框架的使用。在这种技术中，开发人员使用一个没有可见性的框架（根据框架集设置，将高度或宽度设为 0）作为载体。隐藏框架只不过是一个拥有最少 HTML 元素集合加一个脚本元素的页面。脚本元素通常只是数组和变量的定义，其值已由服务器写入。因此，控制器框架（即那个可见的框架）可以将这个框架的 location 属性设置为服务器端脚本的位置，并可选择通过查询字符串向其发送数据。然后浏览器发出此请求。服务器端脚本处理查询字符串中传递的任何信息，然后以有效的 JavaScript 语法写入数据。查看以下代码以了解大致思路。

```php
<?php
$username = $_GET['username'];
?>
...
<script type="text/javascript">
top.usernameOK = <?php echo isUsernameAvailable($username); ?>;
top.usernameAlts = new Array(<?php echo implode(',', getSimilarNames($username)); ?>);
top.frames[1].readVars();
</script>
...
```

*此代码位于隐藏通信框架中。在此代码示例中，写入一个布尔值以指示通过查询字符串传递给脚本的用户名的可用性。当浏览器的 JavaScript 引擎执行此脚本时，它将把该布尔值存储在名为 usernameOK 的 JavaScript 变量中。还正在向输出写入一个用户名替代项数组。在 PHP 中，该数组被连接成一个以逗号分隔的单个字符串，以符合 JavaScript 数组语法。（getSimilarNames 函数也需要将每个数组值加引号。）*

当隐藏框架加载 JavaScript 时，它会触发控制器框架，该框架随后可以访问由服务器端脚本写入的变量值，即 top.usernameOK 和 top.usernameAlts：

```javascript
<script type="text/javascript">
function readVars()
{
    alert(top.usernameOK);
    alert(top.usernameAlts);
}
self.readVars = readVars;
</script>
```

*此代码位于控制器框架中。将代码封装在一个由隐藏通信框架调用的函数中，是触发通过加载隐藏框架来检索数据的一种方法。*

这种技术的优点包括：

- 它允许在不刷新整个页面的情况下向服务器发送和接收数据。
- 一旦数据可用，它就可以触发主应用程序的数据检索。
- 它易于使用和调试，因为应用程序使用的数据在隐藏框架的源代码中清晰可见。
- 它可以接收图形数据，但对 JavaScript 变量作为图像源的支持在浏览器中仅部分支持（例如，IE 只喜欢像这样分配 XBM 图像数据）。
- 由于框架加载会添加浏览器历史记录条目，用户可以按后退按钮。但是，后退按钮的行为可能不符合用户的预期。

缺点包括：

- 它引入了可用性问题，例如无法轻松收藏应用程序状态。
- 它可以通过在超时后重新提交请求来部分检测通信错误。
- 隐藏框架的内容很容易受到用户的操纵（这始终是一个关注点，但使用隐藏框架技术时，用户更容易做到这一点）。
- 每个隐藏框架在给定时只能分派一个请求（如果响应很重要，这是一个缺点）。

### 隐藏 IFRAME

与隐藏框架技术相似的是隐藏 IFRAME 技术。不是使用框架集内的隐藏框架，该方法使用一个不可见的 IFRAME 元素，改变其源位置以向服务器发出请求并接收响应。谷歌地图使用这种技术在不刷新页面的情况下与服务器通信。



该技术具有以下优势：

- 它具备隐藏帧技术的所有优点。
- 根据 IFRAME 源位置的变化方式，你可以对后退按钮的行为拥有更多的控制权。

其缺点包括：

- 它存在与隐藏帧技术类似的用户体验问题。
- 它可以通过在超时后重新提交请求来部分检测通信错误。
- 在给定时间内，只能针对每个隐藏 IFRAME 发送一个请求（如果响应很重要，这是一个缺点）。
- 在通过编程方式添加 IFRAME 元素以及源位置更改后引用 IFRAME 中包含的文档响应方面，各浏览器之间存在严重的差异。

### XMLHTTP 和 XMLHttpRequest

即使是现在被称为“AJAX”的方法也并非新鲜事物。微软版本的接口 XMLHTTP 自 1998 年底 IE 5.0 的预览版以来，一直以 ActiveX 对象的各种形式存在（IE 5.0 的最终版本发布于 1999 年 3 月）。多年来，各公司一直在 IE 独占环境中利用这种开发模式。在 Mozilla 浏览器产品 1.0 版发布前不久，一个原生对象（模仿微软接口并命名为 XMLHttpRequest）已经可用。最近，Safari（从 1.2 版开始）、Opera（从 8 版开始）和 Konqueror 也都包含了名为 XMLHttpRequest 的兼容接口。

在过去几个月里，XMLHTTP 及其变体的使用急剧增加。谷歌在 Google Suggest 和 Google Gmail 产品中对这项技术的采用，主要是导致这种开发方法普及到大众的主要原因。此外，Adaptive Path 发布的一篇文章创造了“AJAX”这个术语，使开发人员能够用一个统一的名称来指代这一组技术，从而促进了该主题的交流与认知。

#### 接口

以下是 XMLHTTP 和 XMLHttpRequest 接口的相关方法，这些方法在大多数浏览器中均得到支持：

- `abort()`：中止请求。
- `getResponseHeader(key)`：返回名为 `key` 的 HTTP 响应头的值。
- `open(method, uri, [async, [username, [password]]])`：将 HTTP 请求方法设置为 `method`，将请求 URI 设置为 `uri`。可选地，它设置标志以指示是否异步处理请求为 `async`，并在必要时设置用于身份验证的用户名和密码。`method` 属性通常要么是 `get` 要么是 `post`。如果你正在请求中推送数据，使用 `post` 是合适的（参见 `send()` 方法）。在几乎所有情况下，`async` 应保留其默认值 `true`。
- `overrideMimeType(type)`：强制将响应解释为服务器发送了名为 `type` 的 mime 类型。此方法在 IE 中不可用。如果修改服务器以发送特定 mime 类型不切实际，这可能很有用。这必须在调用 `send()` 之前调用。它还可以用于避免 Mozilla 的一个 bug，该 bug 有时会导致浏览器在处理非 XML 响应时挂起。
- `send(requestContent)`：发送 HTTP 请求。参数 `requestContent` 用于方法为 `post` 的请求（参见 `open()` 方法），代表请求体。如果请求是异步的，此方法立即返回。早期版本的 Mozilla 在发送字符串作为请求内容时存在困难。对于 `get` 请求，`requestContent` 应为 `null`。对于 `post` 请求，它必须是 `null`、字符串或 DOM Document 对象。如果是后者，该对象将被序列化。此参数的内容包含在请求体中，因此服务器可以访问它。
- `setRequestHeader(key, value)`：将 `value` 的值分配给名为 `key` 的 HTTP 请求头。此方法必须在调用 `open()` 之后且调用 `send()` 之前调用。

`open()` 和 `send()` 方法处理接口的主要功能。`open()` 方法设置请求的各种参数，如 HTTP 请求方法（`get` 或 `post`）和请求 URL。请求 URL 通常是服务器上脚本的相对位置以用于调用。你可以使用完全限定的 URI，但由于安全限制，URI 的域必须包含发出请求的 JavaScript 所在的页面的域。这意味着，如果你希望从位于其他域名的第三方数据源（例如天气数据源）获取数据，你必须通过位于你服务器上的服务器端脚本来代理这些请求。

`open()` 方法中的可选 `async` 参数决定了 `send()` 方法的行为。如果设置为 `true`（或保留其默认值），`send()` 方法将发出 HTTP 请求并立即返回。这意味着，在调用 `send()` 之后的 JavaScript 代码行将无论所发出请求的响应如何都会执行。相反，响应处理由事件的触发来触发，并由事件处理器处理。这个特性是 AJAX 中的第一个 A，它允许你开发行为类似于桌面应用程序的应用程序。此事件处理的具体细节通过接口的属性设置：

- `onreadystatechange`：当触发 `ReadyStateChange` 事件时调用的函数（即当 `readyState` 属性发生变化时）。此属性的值应是一个 JavaScript 函数。确保不要带括号引用该函数，否则函数将被调用，且此属性的值最终将成为函数的返回值，而不是函数本身。
- `readyState`：只读。这是一个表示请求当前状态的整数。此属性的可能值范围从 0 到 4，表示进度逐渐增加。值为 4 表示请求已完成且响应已完全处理。当 `readyState` 至少为 2 时，头和状态可用。
- `responseText`：只读。这是作为文本的响应体。对于从 `readyState` 为 3 开始的成功请求，它非空。在 `readyState` 为 4 时，`responseText` 完全填充。
- `responseXML`：只读。这是解析为 text/xml 内容并打包为 DOM Document 对象的响应体。对于 `readyState` 为 4 的成功请求，它非空。
- `status`：只读。这是整数 HTTP 响应状态码。200 表示成功响应。有关其他可能的状态码，包括众多错误代码，请参阅 HTTP/1.1 RFC 的 6.1.1 节（http://www.rfc-editor.org/rfc/rfc2616.txt）。

除了 `responseText` 和 `responseXML` 之外，这些属性主要涉及确定是否已接收响应以及何时接收。这是必要的，因为我们的请求是异步的，这意味着你不能根据执行顺序或时间依赖任何特定代码行处响应的可用性。相反，异步通信依赖于事件驱动模型进行处理。`readyState` 属性包含一个指示请求进度的值。每次此值变化时，都会触发 `ReadyStateChanged` 事件。如果已定义，`onreadystatechange` 处理器则被调用来处理 `ReadyStateChanged` 事件。请注意，对于给定的请求，`readyStateChange` 事件至少会触发四次。在大多数情况下，除了最后一个事件外，你对这些事件都不感兴趣，即当 `readyState` 属性从 3（加载）变为 4（完成）时。然而，`readyState` 为 4 并不意味着请求成功。它仅表明所有操作已完成。你仍然必须检查 `status` 属性以了解请求的成功情况。例如，服务器在处理请求期间可能遇到了错误。如果 `status` 属性的整数值为 200（OK），则请求成功，预期的响应应在 `responseXML` 或 `responseText` 中可用。如果这听起来有点令人困惑，没关系：接下来你将深入一些代码，一切都会明朗起来。

#### 与接口协作

由于该接口在不同环境中名称不同，并且针对不同浏览器实例化方式不同（在 Internet Explorer 中，因为接口是 ActiveX 对象，而在 Mozilla、Safari、Konqueror 和 Opera 中则是另一种方式），创建请求对象比你可能预期的要稍微复杂一些。此处所示的代码是一种绕过这些浏览器差异的基本方法。如果你研究过 AJAX 的实现，你很可能会看到与此非常相似的代码。

```javascript
<script type="text/javascript"> 
function getXMLHTTP() {
  var req = false;
  // first, try to instantiate the native object
  if (window.XMLHttpRequest) {
    try {
      req = new XMLHttpRequest();
    }
    catch(e) {}
  }
  // otherwise, try instantiating the ActiveX
  // object for IE.
  else if (window.ActiveXObject) {
    // just because creation of ActiveX objects
    // is supported, doesn't mean the XMLHttpRequest
    // object is available. So, let's try it.
    try {
      // try instantiating the newer version
      req = new ActiveXObject("Msxml2.XMLHTTP");
    }
    catch(e) {
      try {
        // otherwise, try the older version
        req = new ActiveXObject("Microsoft.XMLHTTP");
      }
      catch(e) {}
    }
  }
  // req will either be the reference to the
```





# 第 11 章

这段代码隐藏了在实例化 XMLHTTP 和 XMLHttpRequest 接口时浏览器的差异，并返回可用的版本。

如前所述，接收 XMLHTTP 请求的响应是通过触发事件和调用相应的事件处理器来处理的。下面的一组代码展示了处理 ReadyStateChange 事件触发的典型方式，并仅针对感兴趣的事件采取措施：

```javascript
<script type="text/javascript">
function handleReadyStateChange() {
    if (!request) return; // ignore unless complete
    if (request.readyState == 4) { // ignore unless successful.
        // You might choose to handle errors
        // rather than ignore them.
        if (request.status == 200) {
            // act on the response
            var xmlbody = request.responseXML;
            request = false;
            processResponse(xmlbody);
        }
    }
}
</script>
```

此函数被分配为 onreadystatechange 处理器，并在 ReadyStateChange 事件触发时调用。它会忽略所有 readyState 不是 4（完成）且 HTTP 状态码不是 200（OK）的事件。完整且成功响应的 XML 主体被提取并传递给另一个函数进行处理。请注意，在获取 XML 主体后，request 对象被设置为 false。这是为了避免 Opera 浏览器中的一个 bug，该 bug 会导致当 readyState 变为 4 时有时触发多个 ReadyStateChange 事件。这可能会导致对单个响应多次执行操作。

#### 处理响应

前几节中的代码相对标准。AJAX 应用的复杂性通常在于解释响应并根据其内容采取适当的操作。通常，适当的操作是通过 JavaScript 进行 DOM 操作。例如，如果你向服务器发出请求以检查用户名是否可用，并且服务器响应了此处所示的 XML 响应，那么你可能希望向用户显示一条消息，表明他或她需要选择不同的用户名。你还可能希望根据 XML 响应中包含的备选方案提供建议：

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<usernameResults>
    <username value="jessica" available="false" />
    <username value="jess" available="true" />
    <username name="jessica2005" available="true" />
    <username name="jessie" available="true" />
</usernameResults>
```

在此 XML 响应中，服务器指示该用户名不可用。此外，服务器还建议了可用的用户名变体。

你可以采用的传达此信息给用户的一种方法是使用 JavaScript 的 alert() 函数打开一个对话框。然而，一种更用户友好的方法可能是使用 DOM 操作在页面的某个部分添加一个 DIV 或 UL 元素。这提供了一种侵入性更小的消息形式，允许用户继续他正在与应用进行的交互，并在其方便时处理该消息。以下代码展示了如何遍历 XML 树并适当操作的示例：

```javascript
<script type="text/javascript">
function processResponse(oXML) {
    // exit if xml is undefined or doesn't have a documentElement
    if (!oXML) return;
    if (!oXML.documentElement) return;

    var doc = oXML.documentElement;

    // return a nodeList of all elements named username
    var unames = doc.getElementsByTagName('username');
    var msgs = new Array();

    // iterate through the username nodeList
    for (var i = 0; i < unames.length; i++) {
        var u = unames.item(i);
        var username = u.getAttribute('value');
        var availability = u.getAttribute('available');

        // make the available attribute more user-friendly
        if (availability == 'true') {
            availability = 'available';
        } else {
            availability = 'not available';
        }

        msgs[msgs.length] = 'Username ' + username + ' is ' + availability;
    }

    // create an unordered list element
    var ul = document.createElement('ul');
    ul.id = 'msg';

    // for each message, create a list item element and a text node containing
    // the message. The text node is a child node of the list item element, and the
    // list item is a child node of the unordered list element.
    for (var k = 0; k < msgs.length; k++) {
        var li = document.createElement('li');
        var txt = document.createTextNode(msgs[k]);
        li.appendChild(txt);
        ul.appendChild(li);
    }

    // obtain a reference to the maindiv element
    // and insert our new unordered list just before it
    var maindiv = document.getElementById('maindiv');
    maindiv.parentNode.insertBefore(ul, maindiv);
}
</script>
```

此函数处理来自请求 responseXML 属性的 XML，并添加一个 ul 元素到 DOM。

如你所见，DOM 操作可以非常复杂。这个特定响应的优点是，无论它们在 XML 响应中的位置如何，你都可以收集 username 元素。通常，你不能直接做到这一点，你必须对 XML 响应的预期结构有一个概念，或者至少知道各种元素如何对应于其他元素。如果 XML 格式曾经被修改，这可能会导致问题。在 XML 元素级别而非响应级别附加响应处理器，在抽象整个 XML 文档细节方面显示出一些前景，允许客户端脚本专注于与该特定 DOM 操作相关的局部结构。

例如，你可能希望在单独的 DOM 元素中显示备选用户名，在这种情况下，你需要区分具有或没有 usernamealts 父元素的 username 元素。然而，你不需要知道 XML 文档的其余部分是如何结构化的，以及这些 username 元素在文档树中的位置。实现这种想法需要 XML 元素名称与处理器函数之间的映射。特定实现的细节超出了本章的范围，但有文章对该主题进行了更深入的研究。

### AJAX 库

如果这一切看起来令人不知所措，不要害怕。由于 AJAX 作为一种开发方法并不完全新鲜，有很多可用的库可以处理繁琐的工作。最近，随着对 AJAX 兴趣的重新燃起，可用库的数量正在急剧增加，现有库也在迅速成熟。

#### SAJAX

SAJAX ([http://www.modernmethod.com/sajax/](http://www.modernmethod.com/sajax/)) 是简单 AJAX 工具包，它在 PHP（以及许多其他语言）中具有服务器端实现。本质上，使用该库，你可以在 PHP 中定义函数并通过 XMLHttpRequest 从客户端调用它们。启用特定函数以进行远程过程调用只需要一个 SAJAX 函数调用：sajax_export('phpFunctionName')。

不幸的是，当涉及到必要的 DOM 操作时，SAJAX 帮不上忙。事实上，由于 SAJAX 将响应视为文本并使用给定元素的 innerHTML 属性直接将响应插入文档（这通常被认为劣于 DOM 操作），除非你实现自己的字符串解析算法，否则无法进行 DOM 操作。在 SAJAX 常见问题解答页面（[http://www.modernmethod.com/sajax/faq.php](http://www.modernmethod.com/sajax/faq.php)），开发人员将“不过度抽象”列为一个特性。XMLHTTP 通信的许多方面可以从抽象中受益匪浅，因此你可能将 SAJAX 在这方面缺乏视为一个缺点。尽管如此，SAJAX 提供了一种简化客户端对 AJAX 请求的服务器端处理以及客户端处理 XMLHTTP 请求对象实例化和发出必要请求的方法。

#### CPAINT

CPAINT ([http://cpaint.sourceforge.net/](http://cpaint.sourceforge.net/)) 是跨平台异步接口工具包。它支持纯文本和 XML 响应类型。此外，它对直接检索响应为 JavaScript 对象也有一些支持。该库成熟且正在积极开发。

CPAINT 从函数调用为你生成 XML，结果是一种 somewhat 非语义的结构。另外，由于某些未知原因，生成的 XML 元素全部是大写的。如果你提供给元素的名字不是全大写，库会将其转换为全大写。库使用文档有点难以理解，但每个部分都解释得很好，并为每个部分提供了一个琐碎的示例以帮助理解其思想。

#### JPSPAN

JPSPAN ([http://jspspan.sourceforge.net](http://jspspan.sourceforge.net)) 的主要目标是弥合 JavaScript 和 PHP 之间的差距。它允许无缝导入 PHP 类到 JavaScript。这意味着你可以在 PHP 中定义一个类，并像它是一个原生 JavaScript 对象一样调用其方法。在幕后，JPSPAN 正在向服务器发出请求以远程执行方法。其他库提供类似的功能，但它们与 JPSPAN 提供的抽象程度相比相形见绌。JPSPAN 的文档和示例代码丰富且清晰。两者都是 wiki 格式，因此是不断增长的。代码本身清晰易读，就像它生成的 XML 一样。此外，目前正在开发初步工作以将 JPSPAN 嵌入 PHP 框架，使开发 fat-client 应用变得更加容易。

该库不减轻 DOM 操作任务，但它很好地抽象了 XML-HTTP 的使用。不幸的是，它似乎支持 Opera 存在问题，但它很好地支持 Mozilla 基础浏览器和微软的 IE。此外，根据应用程序的不同，JavaScript 和 PHP 之间的桥接可能不会带来多少好处，而只是用对象和原生 JavaScript 访问替代了 XML 树遍历。由于创建 PHP 类的原生 JavaScript 版本涉及额外的开销，收益可能不抵成本。然而，由于出色的抽象使用，JPSPAN 可以允许你几乎完全忽略 PHP 类如何被提供给 JavaScript 的细节，并将注意力集中在应用程序本身的功能上。

还有许多其他支持 PHP 的 AJAX 库。你可以在 [http://www.ajaxpatterns.org/AJAXframeworks](http://www.ajaxpatterns.org/AJAXframeworks) 了解有关各种 AJAX 库的更多信息。

### 何时不使用 AJAX

对 AJAX 的爆炸性兴趣是一把双刃剑。Macromedia 的 Flash 产品的使用也经历过类似的繁荣。客户因为它看起来酷而要求它。与 Flash 一样，AJAX 引入了可用性和可访问性问题，其中许多在传统 Web 应用中已经是已解决的问题。





# 第 11 章

例如，AJAX 应用程序存在于一个 URI 命名空间中。换句话说，当用户与应用程序交互时，URI 不会改变。这是合理的，因为这是 AJAX 的主要卖点之一：能够在不刷新当前页面或导航到其他页面的情况下更改应用程序状态。然而，这使得浏览器的“后退”按钮失效，甚至可能导致用户完全离开你的应用程序。

1999 年，著名的可用性专家雅各布·尼尔森（Jakob Nielsen）发表了一篇文章，指出了网页设计的十大错误。第一大错误就是破坏浏览器“后退”按钮的功能。根据尼尔森的说法，“后退”按钮是继超链接使用之后“第二有用的导航功能”。确实存在一些变通方法，可以部分复制“后退”按钮的功能。

另一个相关的可用性问题涉及无法为特定的应用程序状态添加书签。在传统应用中，应用程序状态通常对应于单个 URL，因此可以添加书签。例如，当用户在产品目录中导航到特定产品的详情页时，用户可能希望将此页面加入书签以便稍后查看。此外，用户可能希望朋友查看该产品并尝试通过电子邮件发送该 URI。破坏这种书签功能可能会对口碑营销的效果产生重大影响。现有的变通方法允许解决等式的一半，即接收给定的 URI 并将其转发到你的 AJAX 应用程序以重建所需的应用程序状态。然而，由于对于任何给定状态，地址栏中都不包含该 URI，这种方法仍然无法解决向用户准确说明如何为当前应用程序状态添加书签的问题。浏览器的书签功能变得毫无用处，应用程序必须提供其他书签方式，通常涉及非标准的用户界面元素。

试图解决这些可用性和无障碍问题的工作正在进行中，并且取得了进展。然而，经常被忽视的问题是：可用性问题是否是技术使用不当的结果？Flash 的可用性问题就是这种情况：开发人员试图用 Flash 文件实现完整的基于 Web 的应用程序。导致可用性问题的不是 Flash 技术本身，而是这种误用。AJAX 的误用也是如此。在恢复特定应用程序状态没有太大意义的应用程序中，该技术做得非常出色。Google GMail 就是一个很好的例子。在基于 Web 的电子邮件客户端中为特定状态添加书签的价值非常小。表单应用程序（如 Google Suggest）是另一个很好的例子。没有必要在 Google Suggest 中为状态添加书签。基于 Web 的客户端从为特定应用程序状态添加书签的能力中获得的益处微乎其微。相反，如果无法为状态添加书签，产品目录将遭受巨大损失。如果无法为特定文章的显示添加书签，内容管理系统的可用性也将遭受巨大损失。

将 AJAX 技术应用于任何传统 Web 应用程序的诱惑是可以理解的。然而，许多传统 Web 应用程序会受到 AJAX 使用的损害。从 AJAX 中自然受益的应用程序的共同点在于它们传统上是桌面应用程序。GMail 是电子邮件客户端的基于 Web 的版本，该客户端此前作为桌面应用程序运行效果最好（实际上，传统电子邮件 Web 应用程序出现的唯一真正原因是可以从任何地方访问它）。Google Suggest 的行为非常类似于传统上在桌面应用程序中发现的表单控件。除了 Java Applet 和类似解决方案外，这些应用程序几乎排他地是桌面应用程序。开发人员曾尝试制作聊天应用程序的纯标记和 JavaScript 版本，但这些应用程序无法与它们的原生对应物相提并论。

虽然确实存在例外，但一个好的经验法则是，AJAX 非常适合将传统的桌面应用程序或其元素创建为基于 Web 的版本。它为 Web 应用程序开辟了新的可能性，但不一定对传统可能性有益。在决定是否使用 AJAX 时应小心，并询问自己 AJAX 对你正在开发的应用程序是否*有益*。如果你遇到需要复杂变通方法的严重可用性问题，那么 AJAX 可能不是合适的开发模型。

除了可用性问题外，还有支持方面的问题。拥有一个依赖 AJAX 且没有为旧浏览器提供任何回退支持的应用程序，可能会阻挡很大一部分潜在用户群。即使对于当前浏览器，一些公司出于安全原因也要求部分或完全禁用 JavaScript。如果应用程序不能优雅降级并提供传统 Web 应用程序功能作为安全网，这些用户也会被阻挡在你的应用程序之外。这是否可接受将取决于你应用程序的性质，因为对于某些应用程序，提供传统版本是不现实的。其可接受性也将取决于你预期的受众及其可能的浏览器选择。

### 进一步的信息

有关本章讨论主题的更多信息，可以在以下资源中找到：

- 动态 HTML 和 XML：XMLHttpRequest 对象。Apple, Inc.
  - http://developer.apple.com/internet/webcontent/xmlhttpreq.html
- XMLHttpRequest：维基百科，自由的百科全书。
  - http://en.wikipedia.org/wiki/XMLHttpRequest
- AJAX：维基百科，自由的百科全书。
  - http://en.wikipedia.org/wiki/AJAX
- XMLHttpRequest：XULPlanet.com。
  - http://xulplanet.com/references/objref/XMLHttpRequest.html
- XML 扩展：Mozilla 基金会。
  - http://www.mozilla.org/xmlextras/
- AJAX 模式：
  - http://www.ajaxpatterns.org/
- AJAX Matters：
  - http://www.ajaxmatters.com/

### 摘要

在本章中，你学习了如何使用 AJAX 将 Web 应用程序的大部分处理工作转移到客户端。你还了解到，AJAX 并非某种新趋势，实际上是几种较旧技术的产物，每种技术都有某些使其不那么理想的缺点。本章向你展示了如何使用 AJAX 接口，以及如何处理客户端的响应。它还介绍了一些你可以使用的 AJAX 库，甚至讨论了你不应该使用 AJAX 的情况。

# 第 12 章

## 缓存引擎

你已尽力清理代码并减少 PHP 脚本中的处理负载，但似乎始终无法使页面足够快以满足用户满意的需求。是时候放弃了吗？并非如此——你可以从 LAMP 环境中获得更多的性能，而缓存引擎将帮助你实现这一点。

在处理 PHP5 的不同缓存解决方案时，你有几个选择。一些设置实际上会缓存内部编译的 PHP 脚本，其他的缓存生成的输出，还有其他的缓存中间数据处理对象。本章向你介绍几个缓存引擎，并帮助你决定哪一个最适合你。

### Alternative PHP Cache (APC)

Alternative PHP Cache（替代 PHP 缓存），或称 APC，是一种 PHP 操作码缓存引擎，现在作为 PECL/PEAR 存储库的一部分免费提供。APC 起源于 Daniel Cowgill 和 George Schlossnagle，并由 Community Connect, Inc. 发布。在 PHP5 发布后，Yahoo! 修改了 APC 以支持新的 Zend 引擎，此后它已成为 PECL 的一部分。

APC 的工作原理是从 PHP 运行时引擎获取编译的代码，并将其存储在共享内存中以便后续访问。每次下载脚本时，APC 首先检查共享内存中的版本，然后再重新编译和执行位于磁盘上的脚本。由于 PHP 不需要每次重新编译脚本，它可以极大地加快响应时间——在某些情况下，速度可以提升四倍或更多。

APC 可以作为动态共享对象（DSO）安装，也可以静态编译到 PHP 中。下一节将向你展示如何安装 DSO 版本，因为它不需要你重新编译 PHP，并且提供了随时添加或删除 DSO 的灵活性。





#### 安装 APC

首先，从 PECL 网站获取最新版本的 APC 源代码副本：`http://pecl.php.net/package/APC`。

一旦你获得了 tar/gzip 格式的源代码副本，解压该包并进入新创建的源代码文件夹：

```bash
tar -xvzf APC-3.0.5.tgz
cd APC-3.0.5
```

接下来，在源代码文件夹中运行 phpize。请务必使用安装 PHP 时附带的 phpize 的正确路径：

```bash
/usr/local/bin/phpize
```

当 phpize 运行时，你应该看到类似于以下内容的输出：

```text
Configuring for:
PHP Api Version:     20031224
Zend Module Api No:  20041030
Zend Extension Api No:       220040412
```

phpize 完成后，运行以下 configure 脚本，同样替换为你自己的 php-config 和 apxs 程序的正确路径：

```bash
./configure \
--enable-apc \
--enable-apc-mmap \
--with-apxs=/usr/local/apache2/bin/apxs \
--with-php-config=/usr/local/bin/php-config
```

然后，构建共享对象：

```bash
make
```

构建完成后，安装 DSO（以 root 身份运行）：

```bash
make install
```

此时，你的 PHP 扩展文件夹中应该有一个 apc.so 的副本。

要完成安装，将以下内容添加到 php.ini 文件的 extensions 部分，然后重启 Apache：

```ini
extension="apc.so"
```

#### 配置 APC

在大多数情况下，APC 使用的默认配置应该就足够了，但如果你想要调整缓存以适应你的需求或系统，可以使用 php.ini 中的以下指令：

## 缓存引擎

| 指令 | 默认值 | 设置位置 | 描述 |
|---|---|---|---|
| `apc.enabled` | `1` (启用) | php.ini, httpd.conf, .htaccess, 和用户脚本 | 使用值 `1` 或 `0` 相应地启用或禁用 APC。在 php.ini 中，此设置只有在 APC 被静态编译到 PHP 中时才真正有用——当你像之前那样安装 APC 时，你可以简单地注释掉 `extension="apc.so"` 这一行。然而，此设置在用户脚本和 .htaccess 文件中是可修改的，因此你可以使用它在单个脚本和目录中启用/禁用缓存引擎。 |
| `apc.shm_segments` | `1` | php.ini 和 httpd.conf | 使用数值，你可以指定 APC 使用的共享内存段数。许多操作系统对每个共享内存段可以变得多大都有一个限制，通常很低。如果 APC 内存不足，增加此值将导致 APC 使用更多段，以帮助绕过操作系统限制。 |
| `apc.shm_size` | `30` | php.ini 和 httpd.conf | APC 共享内存段的大小，以 MB 为单位。根据操作系统不同，可能存在大小限制，通常较低。查阅你的操作系统文档以获取有关其共享内存段大小的更多信息。 |
| `apc.optimization` | `0` (关闭) | php.ini, httpd.conf, .htaccess, 和用户脚本 | 这是一个实验性设置，该指令控制 APC 内置的优化器。此设置的值越大，优化器的激进度越高。值 `0` 完全禁用优化。 |
| `apc.num_files_hint` | `1000` | php.ini 和 httpd.conf | 此设置向 APC 提供关于你的网站通常提供多少个独立源文件的提示。 |
| `apc.ttl` | `0` | php.ini 和 httpd.conf | 定义每个缓存条目在缓存中允许存在的时间（以秒为单位），在此之后允许新条目覆盖它。如果保持为 `0`，缓存可能会填满过时的条目，阻止新条目被缓存。 |
| `apc.gc_ttl` | `3600` | php.ini 和 httpd.conf | 定义每个缓存条目在垃圾收集列表中保留的时间（以秒为单位）。作为在服务器进程死亡，导致缓存文件滞留在缓存中的情况下的故障安全机制。值 `0` 禁用此功能。 |
| `apc.cache_by_default` | On | `php.ini` 和 `httpd.conf` | 控制所有文件的缓存。使用此指令来禁用默认的所有脚本缓存，允许你使用下面的 `apc.filters` 指令来更精细地控制哪些文件实际上被缓存。 |
| `apc.filters` | `""` (空字符串) | `php.ini` 和 `httpd.conf` | 允许你定义一个由逗号分隔的正则表达式列表，用于过滤哪些文件被缓存。使用 POSIX 扩展正则表达式——类似于 PHP 的 `ereg` 函数——你指定一个正则表达式列表以将某些脚本排除在缓存之外。任何匹配列表中模式的文件名将不会被缓存，除非该模式以 `+` 开头，在这种情况下它们将由 APC 缓存。在创建正则表达式时，假设是相对文件路径，而不是绝对路径。 |
| `apc.slam_defense` | 0 (禁用) | `php.ini` 和 `httpd.conf` | 使用 0 到 100 的数字定义，该指令指定服务器进程跳过缓存之前未缓存文件的概率。主要用于极其繁忙的 Web 服务器，`apc.slam_defense` 用于对抗多个服务器线程试图在同一时间缓存同一文件时的竞态条件。 |

#### 移除 APC

如果你安装 APC 后不再需要它，可以遵循这些简单步骤将其从你的 PHP 安装中移除。

首先，在 `php.ini` 文件中查找并删除 `extension="apc.so"` 行。或者，你可以只将其注释掉：

```ini
;extension="apc.so"
```

此时，你可以重启 Apache，APC 将不再在 PHP 中激活。如果你想要彻底从机器上清除 DSO，可以在 Apache 重启后删除 PHP 扩展目录中的 `apc.so` 文件。

### eAccelerator

eAccelerator 是另一个编译状态 PHP 缓存引擎，类似于 APC。eAccelerator 是流行的 PHP4 TurckMMCache 缓存引擎的分支，是一个免费的编码器和优化器，目前由 Frank Alcantara 和 SourceForge 程序员团队维护。

除了作为 PHP 优化器和缓存引擎外，你还可以使用 eAccelerator 对你的 PHP 脚本进行编码，这样你可以将编码后的版本重新分发到安装了 eAccelerator 的客户端，而不用担心源代码被窥探。

> 与其他 PHP 编码解决方案一样，当文件使用 eAccelerator 编码时，几乎不可能使用标准工具对其进行解密。然而，可以使用 PHP 引擎本身的调试器和反汇编器进行逆向工程，但通常这种努力并不值得可能的回报。

#### 安装 eAccelerator

与 APC 一样，eAccelerator 可以作为一个 DSO 安装，使用以下过程。首先，下载源代码副本，可在 http://eaccelerator.net/ 获取。

> 不幸的是，目前 eAccelerator 与 PHP 的 CGI 二进制版本不兼容。如果你运行 CGI 二进制版本，本节仅作为参考信息。

解压你下载的 tarball，然后进入新创建的目录：

```bash
tar -xvzf eaccelerator-0.9.3.tar.gz
cd eaccelerator-0.9.3
```

在此目录中运行你的 phpize 副本（再次，相应更改路径）：

```bash
/usr/local/bin/phpize
```

然后，配置源代码并构建二进制文件：

```bash
./configure \
--enable-eaccelerator=shared \
--with-php-config=/usr/local/bin/php-config
make
```

构建完成后，以 root 身份安装 DSOs：

```bash
make install
```

接下来，你需要为 eAccelerator 放置临时文件提供一个位置。在 /tmp 文件夹中创建一个 eaccelerator 目录：

```bash
mkdir /tmp/eaccelerator
chmod 0777 /tmp/eaccelerator
```

最后，将以下内容添加到 php.ini，然后重启 Apache：

```ini
extension="eaccelerator.so"
```

#### 配置 eAccelerator

与 APC 类似，默认选项在大多数情况下可能就足够了，但如果不足，你可以访问以下 php.ini 指令：





# 第 12 章

## 缓存引擎

| 指令 | 默认值 | 设置位置 | 描述 |
| --- | --- | --- | --- |
| eaccelerator.shm_size | 0 | php.ini 和 httpd.conf | 定义 eAccelerator 用于缓存脚本的共享内存量（以兆字节为单位）。值为 0 时，表示 eAccelerator 将使用操作系统的默认值。 |
| eaccelerator.cache_dir | /tmp/eaccelerator | php.ini 和 httpd.conf | 指定磁盘缓存目录，如果 eAccelerator 配置为使用磁盘缓存。 |
| eaccelerator.enable | 1 (启用) | php.ini、.htaccess 和用户脚本 | 允许相应地使用数值 1 和 0 来启用或禁用 eAccelerator。此设置可以在用户脚本和 .htaccess 文件中更改，因此你可以使用它在单个脚本和目录中启用/禁用缓存引擎。 |
| eaccelerator.optimizer | 1 (启用) | php.ini、httpd.conf、.htaccess 和用户脚本 | 启用 eAccelerator 的内部代码优化引擎。值为 1 时启用优化器，值为 0 时禁用。此设置可以在用户脚本和 .htaccess 文件中更改，因此你可以使用它在单个脚本和目录中启用/禁用优化引擎。 |
| eaccelerator.debug | 0 (关闭) | php.ini 和 httpd.conf | 切换调试日志的开启和关闭。 |
| eaccelerator.check_mtime | 1 | php.ini 和 httpd.conf | 此设置控制 eAccelerator 是否检查文件的修改时间以判断其是否已更改。启用的值 1 指示 eAccelerator 如果 PHP 脚本已更改，则自动重新编译该脚本。 |
| eaccelerator.filter | "" (空字符串) | php.ini、httpd.conf、.htaccess 和用户脚本 | 此指令允许你指定一个以空格分隔的列表，指示哪些文件应处理以及哪些文件不应由 eAccelerator 处理。该列表由带有通配符匹配的文件名组成（例如，*.php *.pht）。若要忽略特定的匹配项，请在相关模式前加上感叹号。 |

| 指令 | 默认值 | 设置位置 | 描述 |
| :--- | :--- | :--- | :--- |
| `eaccelerator_shm_max` | `0` (无限制) | `php.ini` 和 `httpd.conf` | 指定使用 `eaccelerator_put()` PHP 函数放入共享内存的数据的最大大小。数值以字节为单位指定，值为 0 表示禁用限制。 |
| `eaccelerator_shm_ttl` | `0` (从不删除过时脚本) | `php.ini` 和 `httpd.conf` | 定义脚本在 `eAccelerator` 共享内存中保持缓存状态的秒数，超过该时间后允许为了新请求而从缓存中移除。值为 0 表示不应移除项目，这可能导致共享内存缓存最终填满，从而阻止对新请求进行缓存。 |
| `eaccelerator_shm_prune_period` | `0` (从不删除过时项目) | `php.ini` 和 `httpd.conf` | 类似于 `shm_ttl` 设置，此指令控制从共享内存缓存中收集过时脚本。与作为缓存中单个脚本的超时不同，`shm_prune_period` 通过仅在 `shm_prune_period` 中定义的时间经过后移除过时项目来工作。此值以秒数表示，值为 0 指示 `eAccelerator` 不要尝试移除过时项目。 |
| `eaccelerator_shm_only` | `0` (两者都使用) | `php.ini` 和 `httpd.conf` | 启用和禁用（0 或 1）磁盘缓存。值为 0 指示 `eAccelerator` 同时使用共享内存和基于文件的磁盘缓存，而值为 1 指示 `eAccelerator` 仅使用共享内存。 |
| `eaccelerator_compress` | `1` (启用压缩) | `php.ini`、`httpd.conf`、`.htaccess` 和用户脚本 | 此指令启用和禁用输出内容压缩，类似于 Apache 的 `mod_deflate` 或 PHP 的 `gzip` 输出缓冲。 |
| `eaccelerator_compress_level` | `9` (最大压缩) | `php.ini`、`httpd.conf`、`.htaccess` 和用户脚本 | 此设置控制使用 `eaccelerator_compress` 中启用的输出压缩时所使用的压缩级别。最大值 9 使用高压缩，导致传输的文件大小更小，而较低的值会降低压缩并增加传输大小。 |

| 指令 | 默认值 | 设置位置 | 描述 |
|---|---|---|---|
| eaccelerator.sessions eaccelerator.content | | php.ini 和 httpd.conf | 你可以使用此指令告诉 eAccelerator 你希望它存储会话数据和内容的位置。值为 shm_and_disk 指示缓存引擎在共享内存和磁盘位置存储会话数据和内容。将其设置为 shm，它将使用共享内存作为主要存储位置，如果共享内存已满，则回退到磁盘存储。shm_only 表示你希望仅使用共享内存且从不使用磁盘回退。值 disk_only 的行为完全相反：它表示你希望仅使用磁盘存储而不使用共享内存。 |

#### 移除 eAccelerator

移除 eAccelerator 非常简单，只需删除或注释掉 php.ini 中相应的扩展行，如下所示：

```php
;extension="accelerator.so"
```

若要永久从系统中移除 eAccelerator，请从 PHP 扩展目录中删除 eaccelerator.so 文件。

> 有关 eAccelerator 的更多信息，请访问 http://eaccelerator.net。

### Zend 优化器

不逊于可用的少数免费 PHP 缓存解决方案，Zend——驱动 PHP 的 Zend 引擎的创建者——发布了它们自己的代码优化器，而且是免费的。Zend 优化器的作用与 APC 和 eAccelerator 类似：它缓存 PHP 脚本的编译状态，从而在后续请求中实现更快的执行。

除了加速 PHP 脚本的性能外，Zend 优化器还允许你在服务器上运行由 Zend Encoder 或 Zend SafeGuard Suite 编码的脚本。

#### 安装 Zend 优化器

与大多数竞争缓存解决方案相比，安装 Zend 优化器稍显容易，因为它附带了一个方便的身份配置和设置向导。

首先，从 http://zend.com/store/products/zend-optimizer.php 下载适合你系统的软件包。

然后，解压存档，并进入新创建的目录：

```bash
tar -xvzf ZendOptimizer-2.5.10a-linux-glibc21-i386.tar.gz
cd ZendOptimizer-2.5.10a-linux-glibc21-i386
```

以 root 身份运行安装向导：

```bash
./install.sh
```

运行向导，在提示时指定必要的路径。通常提供的默认值就足够了。确保在询问时选择正确版本的 Apache（本书撰写时基于 Apache 2）。

向导会对你的 php.ini 文件进行备份，并创建一个指向 Zend 修改后的 php.ini 文件的新符号链接。

在向导结束时，你可以选择自动重启 Apache，或者按你的选择退出向导并手动重启 Apache。

#### 配置 Zend 优化器

与 APC 和 eAccelerator 一样，你有几个指令可用于调整 Zend 优化器的运行：

| 指令 | 默认值 | 设置位置 | 描述 |
| --- | --- | --- | --- |
| zend_optimizer.optimization_level | 15 (所有优化) | php.ini 和 httpd.conf | 确定由 Zend 优化器执行的优化级别。优化器可以对每个脚本执行四次不同的传递，通过组合以下值来控制：<br>0: 无传递 <br>1: 传递 1 <br>2: 传递 2 <br>4: 传递 3 <br>8: 传递 4 <br>你只需将每次传递的数字相加即可得到你的优化传递设置。例如，值 11 将执行传递 1、传递 2 和传递 4 (1+2+8)。 |
| zend_optimizer.enable_loader | 1 (启用) | php.ini 和 httpd.conf | 你可以使用此指令在不卸载的情况下启用或禁用 Zend 优化器。值为 0 禁用优化器；1 启用它。 |

#### 移除 Zend 优化器

要移除 Zend 优化器，你首先必须删除其为 php.ini 创建的符号链接。然后，将备份的原始 php.ini 文件恢复到其原位置。此时你可以重启 Apache，Zend 优化器将不再处于活动状态。如果你愿意，你可以删除 Zend 优化器文件——其默认位置是 /usr/local/Zend。

### JPCache

内存/磁盘缓存解决方案领域的另一个条目是 JPCache。与 APC 和 eAccelerator 不同，JPCache 无需编译为 DSO 或静态构建到 PHP 本身。JPCache 实际上是用 PHP 编写的，并使用标准 *include* 和 *require* 语句使用。

JPCache 通过将 PHP 脚本生成的输出存储到磁盘或 SQL 服务器中工作，而不是保存每个脚本的编译状态。通过以此方式缓存输出，并结合 gzip 内容压缩，你可以实现高达 80% 或更多的带宽节省。

#### 安装 JPCache

要开始使用 JPCache，你需要做的第一件事是从 http://www.jpcache.com 下载最新版本的副本。

接下来，提取 tar/gzip 存档：

```bash
tar -xzvf jpcache.v2.tgz
```

此目录的内容现在包含你使用 JPCache 所需的脚本。将此文件夹放在任何你喜欢的位置，只要 Apache 运行的用户可以访问即可。记下该位置的完整路径，因为配置缓存时你需要它。

在你的 JPCache 文件夹的根目录中，编辑 jpcache.php 文件。更改以下行以指向你放置 jpcache 文件夹的位置：

```php
$includedir = '/path/to/jpcache-files';
```

例如，如果你将提取的 jpcache 文件夹移动到 /www/jpcache，你将使用以下值：

```php
$includedir = '/www/jpcache';
```

接下来，编辑 jpcache-config.php 文件。最重要的是，你需要取消注释指示你希望使用什么类型的缓存存储（文件或 MySQL）的行。对于此示例，取消注释基于文件的存储选项：

```php
$JPCACHE_TYPE = 'file';
```





另一个需要更改的设置是 `$JPCACHE_USE_GZIP` 的值。该选项可以启用 gzip 内容压缩，但不幸的是，由于 JPCache 近期版本中存在一个 bug，在某些浏览器中输出可能会出现损坏。出于安全考虑，请将此值设置为 0：

```php
JPCACHE_USE_GZIP = 0;
```

同时请注意控制文件缓存位置的设置 `$JPCACHE_DIR`，其默认值为 `/tmp/jpcache`。你需要实际创建 `$JPCACHE_DIR` 设置中列出的文件夹，因此在命令提示符下执行以下操作：

```bash
mkdir /tmp/jpcache
chmod 0777 /tmp/jpcache
```

最后，使用以下 PHP 脚本测试缓存系统，请注意使用 JPCache 文件夹所在路径的相应位置：

```php
<?php
require '/path/to/jpcache.php';
echo time();
phpinfo();
?>
```

注意页面顶部的 UNIX 时间戳。每次重新加载页面时，它应该保持不变——这意味着 JPCache 正在提供缓存版本，而不是每次都重新处理脚本。

#### 配置 JPCache

除了之前提到的三个配置选项外，你还有十四个额外的配置变量可以修改以适应你的需求。完整的配置选项列表如下：

| 配置选项 | 默认值 | 描述 |
| :------------------ | :------ | :---------- |
| `$JPCACHE_TYPE` | 无——你必须在使用 JPCache 之前设置此变量。 | 要告诉 JPCache 使用基于文件或数据库的存储来存储缓存数据，请使用 `$JPCACHE_TYPE`。值为 `file` 告诉 JPCache 使用磁盘存储，而值为 `mysql` 会导致缓存数据存储在 MySQL 数据库中。 |
| `$JPCACHE_TIME` | 900 | 使用数值定义，此变量告诉 JPCache 在缓存中保留页面多久（以秒为单位）。负值会完全禁用页面缓存，而值为 0 则告诉 JPCache 无限期地保留页面缓存。 |
| `$JPCACHE_DEBUG` | 0（关闭） | 使用 0 表示关闭，1 表示开启，`$JPCACHE_DEBUG` 控制是否启用调试。 |
| `$JPCACHE_IGNORE_DOMAIN` | 1（忽略域） | 如果你的 Web 服务器只提供一组内容，你可以将此值设置为 1（开启），使 JPCache 忽略文件名中的任何域名前缀。当关闭时，JPCache 将搜索与完整 URL（包括域名）匹配的文件。 |
| `$JPCACHE_ON` | 1（启用） | 此变量仅控制是否启用 JPCache。 |
| `$JPCACHE_USE_GZIP` | 1（开启） | 要启用 GZIP 输出压缩（类似于 Apache 的 mod_deflate 或 PHP 自身的 GZIP 输出缓冲），请将此值设置为 1。请注意，由于 JPCache 近期版本中的一个 bug，使用 JPCache 的 GZIP 压缩时，在某些浏览器中输出可能会损坏。如果你的脚本在启用此设置后返回乱码或缺失的内容，请尝试禁用此设置以查看情况是否得到纠正。 |
| `$JPCACHE_POST` | 0（禁用） | 此变量控制 JPCache 中的 HTTP POST 缓存。设置为 0 以禁用，设置为 1 以启用。 |
| `$JPCACHE_GC` | 1 | 要控制 JPCache 垃圾回收例程的积极程度，你可以将数值赋值给 `$JPCACHE_GC`。数值范围从 0 到 100，表示对某个缓存项目执行垃圾回收的概率百分比。 |
| `$JPCACHE_GZIP_LEVEL` | 9（最大压缩） | 当使用 JPCache 内置的 GZIP 输出压缩时，你可以使用此变量来控制输出流的压缩级别。数值范围从 9（意味着高压缩率和较小的输出大小）到 1（意味着低压缩率和较大的传输大小）。 |
| `$JPCACHE_CLEANKEYS` | 1（哈希存储键） | 当 JPCache 创建脚本输出的缓存副本时，它使用每个脚本的唯一键将输出存储为文件名或数据库记录。默认情况下，JPCache 对标识符进行哈希处理，使确定特定缓存条目的来源变得困难，类似于 `'jp_c-b4c58a486a92288023bfa06140fa2'`。如果需要，你可以告诉 JPCache 不要对每个脚本的缓存标识符进行哈希处理，从而让你能够轻松确定每个缓存脚本的身份。禁用哈希后，脚本标识符将更像 `_directory_file_name_extension_HTTMethod=n_p__...` |
| `$JPCACHE_DIR` | `/tmp/jpcache` | 使用此变量设置 JPCache 存储基于文件的缓存数据的目录。JPCache 存储缓存文件的位置需要可被 Apache 进程用户写入。 |
| `$JPCACHE_FILEPREFIX` | `jpc-` | 当 JPCache 在磁盘缓存中创建缓存文件时，它可以使用在此指定的文件名前缀，以避免与现有文件发生冲突。 |
| `$JPCACHE_DB_HOST` | `localhost` | 当使用数据库作为缓存存储位置时，你需要设置 JPCache 连接和使用数据库时使用的变量。此变量设置 JPCache 将连接的数据库主机。 |
| `$JPCACHE_DB_DATABASE` | `jpcache` | 此变量设置存储缓存数据的 MySQL 数据库的名称。 |
| `$JPCACHE_DB_USERNAME` | `sqluser` | 要设置存储数据库中的缓存信息时使用的用户名，请设置 `$JPCACHE_DB_USERNAME`。 |
| `$JPCACHE_DB_PASSWORD` | `passwd` | 与 `$JPCACHE_DB_USERNAME` 配合使用，此变量设置数据库连接密码。 |
| `$JPCACHE_DB_TABLE` | `CACHEDATA` | JPCache 缓存数据存储所在的表名称位于 `$JPCACHE_DB_TABLE` 中。要创建该表，你可以在 MySQL Monitor 或你首选的 MySQL 管理工具中执行以下命令：`CREATE TABLE CACHEDATA ( CACHEKEY varchar(255) NOT NULL, CACHEEXPIRATION int(11) NOT NULL, GZDATA blob, DATASIZE int(11), DATAACR int(11), PRIMARY KEY (CACHEKEY) );` 当然，你需要更改数据库表的名称以匹配你在 `$JPCACHE_DB_TABLE` 中指定的值，反之亦然。 |
| `$JPCACHE_OPTIMIZE` | `1 (执行 OPTIMIZE TABLE)` | 在垃圾回收周期完成后，你可以指示 JPCache 对 `$JPCACHE_DB_TABLE` 中指定的表执行自动 MySQL `OPTIMIZE TABLE` 命令。 |

#### 移除 JPCache

要移除 JPCache，你需要搜索所有 PHP 脚本，并移除对 `jpcache.php` 文件的任何 `include` 或 `require` 引用。移除引用后，你可以安全地删除 JPCache 目录。

*有关 JPCache 的更多信息，请访问 `http://www.jpcache.com`。*

### memcached

与 APC、eAccelerator 和 JPCache 提供的输出缓存系统不同，memcached 系统依靠后端对象的缓存来实现速度提升。memcached 是一个由 Danga Interactive 创建分布式内存对象缓存系统，该团队负责运营 LiveJournal.com。memcached 不是缓存页面输出或编译后的 PHP 操作码，而是缓存各种代码对象，最重要的是数据库结果对象和数据模型实体。

这种缓存解决方案与本章中的其他系统略有不同——memcached 实际上需要其守护进程始终处于运行状态。然后，PHP 可以使用其 memcached 函数集来访问和使用内存中的对象缓存。

#### 安装 memcached

要安装 memcached，首先从 `http://www.danga.com/memcached/` 获取守护进程的源代码副本。

然后解包 `tar`/`gzip` 存档，并更改到新建的文件夹目录：

```bash
tar -xzvf memcached-1.1.12.tar.gz
cd memcached-1.1.12
```

接下来配置并构建源代码。如果 configure 报告任何缺失的库（例如 libevent），请按照各自的说明下载并安装这些库；然后重新运行 configure 脚本，再构建 memcached。

```bash
./configure
make
```

然后，以 root 身份安装 memcached 守护进程：

```bash
make install
```

最后你需要做的是实际启动守护进程。以下命令启动守护进程，使用 128MB 的 RAM，监听 IP 地址 127.0.0.1 上的 11211 端口：

```bash
/usr/local/bin/memcached -d -m 128 -l 127.0.0.1 -p 11211
```





如果你决定永久使用 memcached，请确保将启动 memcached 的命令添加到你所选择的任何启动设施或脚本中，以便机器每次启动时都能自动加载。

现在 memcached 守护进程已经在运行了，你需要准备让 PHP 使用该缓存系统。从 `http://pecl.php.net/package/memcache` 下载 memcached PECL 模块。

解压缩归档文件并进入新目录：

```bash
tar -xzvf memcache-1.4.tgz
cd memcache-1.4
```

运行 `phpize`，然后配置并制作 DSO：

```bash
phpize
./configure
make
```

以 root 身份安装模块：

```bash
make install
```

最后，将以下行添加到你的 php.ini 中，并重启 Apache：

```ini
extension="memcache.so"
```

#### 使用 memcached

为了使用 memcached，你安装的 PHP DSO 为 Memcache 对象提供了以下方法：

- **Memcache::add**

  `bool Memcache::add ( string key, mixed var [, int flag [, int expire]] )`

此方法将一个变量或对象添加到内存缓存中，由 *key* 标识。如果具有相同 *key* 的值已存在于内存缓存中，则返回 *FALSE*。如果你希望在将值放入内存缓存之前对其进行压缩，请将 `MEMCACHE_COMPRESSED` 作为标志提供，否则可以省略或设置为 0。为 *expire* 提供的任何值都告诉 memcached 何时开始允许从缓存中移除该项。*expire* 的值为 0 表示该值应无限期缓存。

> *只有变量和对象可以存储在内存缓存中，而资源则不能。*

- **Memcache::close**

  `bool Memcache::close ( void )`

此方法关闭与 memcached 服务器的任何非持久连接。如果在关闭连接时发生错误，则返回 *FALSE*。

- **Memcache::connect**

  `bool Memcache::connect ( string host [, int port [, int timeout]] )`

此方法创建并打开到运行在 host 上的 memcached 服务器的连接。port 参数指定 memcached 使用的 TCP 端口，默认为 11211，timeout 指定在尝试连接时等待多长时间后返回 FALSE。成功时返回 true，失败时返回 FALSE。

- **Memcache::decrement**

  `int Memcache::decrement ( string key [, int value] )`

当在内存缓存中存储简单的数值时，你实际上可以使用 decrement() 方法将匹配 key 的值减少所提供的 value。如果未指定递减值，则缓存值减 1。此方法在失败时返回 FALSE，成功时返回该项的新值。

- **Memcache::delete**

  `bool Memcache::delete ( string key [, int timeout] )`

此方法从内存缓存中删除由 key 标识的项。提供 timeout 值会导致该项在提供的秒数后被删除。失败时返回 FALSE，成功时返回 TRUE。

- **Memcache::flush**

  `bool Memcache::flush ( void )`

此方法告诉 memcached 立即设置缓存中所有项的过期时间。一旦调用此方法，缓存中的任何项都可以被新键覆盖，但内存不会释放，直到这种情况发生。此方法在成功时返回 TRUE，在失败时返回 FALSE。

- **Memcache::get**

  `string Memcache::get ( string key )`
  `string Memcache::get ( array keys )`

此方法检索存储在内存缓存中的一项或多项，匹配给定的 key 或 key 数组。成功时，根据匹配输入参数提供的 key 数量，返回字符串或数组；如果没有找到匹配输入参数的 key，则返回 FALSE。

- **Memcache::getStats**

  `array Memcache::getStats ( void )`

这返回一个包含有关内存缓存状态各种信息（如当前和总连接数、缓存项数以及服务器正常运行时间）的数组。

- **Memcache::getVersion**

  `string Memcache::getVersion ( void )`

这返回一个包含 memcached 服务器版本号字符串，或者在发生错误时返回 FALSE。

## 缓存引擎

- **Memcache::increment**

  `int Memcache::increment ( string key [, int value ] )`

与 decrement() 方法类似，increment() 允许你轻松地在内存缓存中直接更改简单的数值——在此情况下，将存储的变量增加 value，如果未提供值则增加 1。成功时返回新值，失败时返回 FALSE。

- **Memcache::pconnect**

  `bool Memcache::pconnect ( string host [, int port [, int timeout]] )`

此方法创建并打开到 memcached 服务器的持久连接，类似于 MySQL 持久连接。参数与 connect() 相同：host 指定 memcached 服务器的主机名或 IP 地址，port 指定 memcached 的监听端口，timeout 指定连接超时时间。

- **Memcache::replace**

  `bool Memcache::replace ( string key, mixed var [, int flag [, int expire]] )`

此方法在缓存对象中搜索与 key 匹配的项，如果找到，则用值 var 替换它。与 add() 和 set() 一样，replace() 可以提供标志以请求在存储值时进行压缩，并且还可以为新值提供可选的过期时间。此方法在成功时返回 TRUE，在失败时返回 FALSE。

- **Memcache::set**

  `bool Memcache::set ( string key, mixed var [, int flag [, int expire]] )`

此方法将值 var 存储在内存缓存中，即使存在与 key 匹配的现有项。参数与 add() 和 replace() 相同。成功时返回 TRUE，失败时返回 FALSE。

你可以以与 MySQLi 方法类似的方式使用这些方法——你连接到 memcached 服务器，将数据输入缓存并进行处理，然后断开连接。以下简单示例将一个 Circle 对象存储在内存缓存中：

```php
<?php

class Circle
{
    public $radius;
    public function area()
    {
        return pi() * pow($this->radius, 2);
    }
}

$memc = new Memcache();
$memc->connect('10.0.0.20', 11211);

$c = new Circle();
$c->radius = 15;

$memc->set('circle1', $c);

$stats = $memc->getStats();

$memc->close();

print_r($stats);
?>
```

如果你运行此脚本，它将打印一个包含当时内存缓存统计信息的数组。如果是你第一次运行该脚本，或者是你服务器上第一次使用 memcached，你的 curr_items 值应为 1，反映新添加的 Circle 对象。

```text
Array
(
    [pid] => 1379
    [uptime] => 4148
    [time] => 1124758570
    [version] => 1.1.12
    [rusage_user] => 0.030000
    [rusage_system] => 0.010000
    [curr_items] => 1
    [total_items] => 8
    [bytes] => 77
    [curr_connections] => 1
    [total_connections] => 9
    [connection_structures] => 2
    [cmd_get] => 0
    [cmd_set] => 8
    [get_hits] => 0
    [get_misses] => 0
    [bytes_read] => 605
    [bytes_written] => 1856
    [limit_maxbytes] => 134217728
)
```

#### 移除 memcached

与其他 DSO 缓存解决方案一样，你可以通过注释或删除 php.ini 中的相应行并重启 Apache 来快速禁用 memcache 功能。此时，你可以从 PHP 扩展目录中删除 memcache.so，并从系统二进制文件夹（之前安装到的位置，很可能是 /usr/local/bin 或 /usr/bin）中删除 memcached 守护进程。

### 同时使用不同的缓存引擎

现在，你的头脑中可能正在思考，你开始好奇：“如果我同时使用多个缓存引擎会怎样？”好吧，正如你所料，选择合适的互补解决方案可以略微提高性能，但有些组合对你没有任何好处。

JPCache 和 memcached 可以与其他组件很好地配合，但 APC、eAccelerator 和 Zend Optimizer 在某种程度上是互斥的。虽然它们可能加载得很好，在执行 PHP 脚本时不抛出任何错误，但使用操作码缓存的组合几乎没有理由。这三种在某种程度上提供大致相同的功能，因此使用多个操作码缓存只会导致系统速度仅达到最慢缓存的速度。

尝试只选择一个操作码缓存解决方案，并尝试将其与 memcached 和 JPCache 结合使用。加入你首选的内容压缩方案——JPCache 内置的内容压缩仍然太不稳定——你就拥有了一台精干且强大的组合缓存服务机器。

### 选择你的缓存引擎

那么，哪种缓存解决方案最适合你？也许最好首先评估你系统的需求，并寻找当前或即将成为瓶颈的地方。如果你的脚本中充满了重量级的类和对象，或者你经常从数据库中拉取大量重复数据，memcached 将是提高性能的最佳选择。如果你的网站代码生成相对静态的页面——你没有使用过多的用户个性化或其他高度动态元素——你应该考虑使用 JPCache。如果数据层不是你的主要瓶颈，但你的 PHP 代码可能需要一些通用的性能调整，那么其中一个操作码缓存引擎会帮助你。如果你不确定使用哪个优化器/缓存，一个安全的押注是 APC。虽然它在底层引擎加速或 Zend Optimizer 可能提供的优化方面可能有所欠缺，但它通过高度定制性和良好的支持来弥补——毕竟，它是 PECL 仓库的一部分。

###### 总结

无论你选择哪种缓存解决方案，本章讨论的任何系统都有能力显著提高你 LAMP 配置的性能。通过适当的维护和配置，你的缓存解决方案将使你能够同时为更多用户提供服务，并帮助你防范某天可能遇到的任何 DOS 攻击或 Slashdot 效应。




## 13

## 内容管理系统

内容管理系统（CMS）协助软件或 Web 开发者组织任何协作流程及其最终成果，并促进其进行。“内容管理”这一术语大致不仅指文件的签入和签出，还包括信息的通用共享，例如公共日历、Wiki 等。最早的内容管理系统大约出现在 1975 年，当时大型机开始普及，对电子出版的需求也真正开始兴起。这些最早版本的系统基本上只不过是通用的存储库，允许多个用户参与同一个项目。

随着计算机系统变得越来越复杂，有效管理内容的需求也变得更加复杂。随着互联网的成熟，CMS 浪潮也随之而来。如今，CMS 的数量多到数不胜数。本章的目标是帮助你在这一堆混乱中理清思路，从而确定你是否需要 CMS，哪种类型的 CMS 适合你的项目，以及如何利用 CMS 来提高你的效率。

### CMS 类型

CMS 形态各异，基本上可以管理由个人团队正在处理的任何事物。从管理简单的静态网站内容，到允许跨互联网进行协作文档编写（Wiki），CMS 执行许多功能。CMS 软件包通常可以分为两大类：企业级 CMS 和 Web CMS。

#### 企业级 CMS

这些功能强大的软件包通常是综合解决方案，为企业或公司级别的使用提供有效的内容管理。它们旨在帮助公司提高效率、降低成本，提高准确性和功能性，同时减少人为错误和缩短客户响应时间。

它们可以整合公司功能，如运输和交付系统、发票、员工和人力资源问题、客户关系，以及文档管理和事务性（销售）系统。企业级 CMS 将数据管理延伸到用户级别，使许多用户都能为这个巨大的集成整体贡献自己的一份力量。部署这些复杂系统的软件公司以提供高度定制化的公司级解决方案为荣，而软件通常标有相当高昂的价格。

##### Web CMS/门户

Web CMS 软件包主要是为 Web 使用而创建的。它们可以包含众多功能，或者围绕某一特定功能构建。它们允许用户更新常见网站的某些部分，或在网站“社区”中进行协作。Web CMS 通过快速、轻松地为网站带来功能，使开发者的工作变得轻松，并允许主要开发者在开发和维护网站时放心地让其他人参与，而不用担心偏离标准。本章将重点介绍开源 Web CMS 软件包，特别是 PHP/MySQL 软件包。

Web CMS 类别的一个子集是群件（Groupware）。这类软件包在内部网络或互联网上运行，设计目的是允许用户（通常是为同一家公司工作，处理相同项目的用户）之间的协作。它们通常提供项目管理、文件签入和签出、日历系统、电子邮件和内部论坛等功能。

##### 开源 Web CMS 软件包

Web CMS 的常见功能包括：

- **静态网页更新**：在不改变网站外观和感觉的情况下更新内容。
- **网络日志（博客）**：在线日记。
- **Wiki**：协作文档项目。
- **出版物**：新闻文章的发布和组织。
- **受管理的 learning 环境**：基于 Web 的学习。
- **事务性 CMS**：电子商务功能。
- **图像和文件画廊**：用于公开使用的图像或文件的汇编。
- **论坛**：促进用户之间讨论的公告板系统。
- **聊天室**：用户之间的实时聊天。
- **RSS 源**：允许用户下载内容。
- **投票**：允许用户就某个主题进行投票。
- **日历系统**：基于 Web 的多用户日历。

还有许多其他功能可以被视为属于 CMS 领域，但这些是主要功能，也是本章关注的重点。

首先，让我们来看看一些更全面的开源 CMS 软件包。

##### 全能型 Web CMS

就像那些将你的假期打包成一套精致套餐的豪华热带度假胜地一样，这些综合型 Web CMS 可以做得多或少，随你喜欢。以下部分介绍了当前可用的一些较流行的软件包，尽管在诸如 http://www.sourceforge.net 等网站上可以找到大量此类软件包。本文不会详细介绍这些软件包的安装过程，因为你过去可能在这方面已经有过一些经验。但是，如果安装有任何特殊注意事项，将会予以注明。此外，在安装这些软件包之前，你需要确保 LAMP 系统的各个方面都运行正常。

大多数全能型 Web CMS 具有常见的功能，如更改用户权限、修改站点布局、更改服务器设置等。需要提到的一点是，许多所谓的综合 CMS 软件包缺乏事务性 CMS 接口（电子商务购物车）。

#### ExponentCMS

ExponentCMS 可在 http://www.exponentcms.org 获取。在撰写本文时，最新版本是 0.96.3，本节也是基于此版本。在 Exponent/Sourceforge 界面 http://sourceforge.net/projects/exponent/ 上，你可以找到链接到屏幕截图、文档、贡献以及标准 Sourceforge 信息的地方。

###### 安装说明

安装相对简单，在安装前你需要知道的是需要创建一个数据库。这适用于远程和本地安装。你还需要设置用户名和密码，因为在安装过程中会要求你提供这些信息。

##### 一般概述/默认安装

安装此 CMS 后，你会获得几个默认“激活”的功能。这些功能包括：

- 地址簿：组织联系信息。
- 管理控制面板：易于使用的站点管理界面。
- 日历系统：通过不同的视图跟踪事件。
- 联系表单：允许网站访问者与你联系。
- 图像管理器：与其他模块配合以管理站点上的图像。
- 预览链接：让在站点上工作的人预览他们的作品。
- 私人消息中心：允许用户相互发送电子邮件或私人消息。
- 资源管理器：组织和显示上传的文件。
- 文本模块：显示文本并跟踪修订版本。
- 网络日志/在线日记管理器：组织博客条目。

“未激活”的功能（那些你可以简单地开启的功能）包括：

- **横幅管理器**：管理横幅广告活动和点击跳转。
- **内容轮换器**：每次用户访问站点时显示不同的图像或文本。
- **Flash 动画管理器**：组织 Flash 动画。
- **表单模块**：管理站点上的任何表单。
- **HTML 模板管理器**：管理上传的 HTML 模板。
- **登录模块**：允许用户登录站点。
- **多站点管理器**：允许你创建和管理其他站点。
- **导航器**：管理导航系统。
- **新闻源系统**：组织和显示新闻文章。
- **搜索**：允许用户搜索站点。
- **UI 切换器**：给予具有正确权限的用户从用户切换到管理员的能力。

通过易于使用的管理员模块管理器，你可以点击按钮激活或禁用其中任何模块。

其他模块可从 http://www.sourceforge.net 下载。使用扩展上传管理器，安装模块非常容易；你甚至不需要解压它们。这些扩展包括：

- **文章管理器**：组织和显示站点上的文章。
- **公告板**：管理站点论坛。
- **常见问题解答**：管理站点的 FAQ 部分。
- **图像画廊**：允许用户排序和查看图像。
- **列表管理器**：组织和管理列表，如房地产列表。
- **页面显示器**：允许你上传和显示动态生成的页面（如 PHP）。
- **幻灯片**：管理站点上的幻灯片。

除了安装、激活和禁用站点模块外，作为站点管理员，你还可以通过管理界面导入数据（如 csv 格式的用户列表）。这使你可以轻松地从其他系统或内部数据库进行转换。

该软件还嵌入了 WYSIWYG HTMLArea 编辑器，使你的作者和贡献者可以轻松地添加文本。作为管理员，你还可以控制 HTMLArea 工具栏，从而确定你的用户有哪些文本选项。

##### 自定义默认设置

与大多数其他 CMS 软件包一样，你可以在管理控制面板中更改用户设置。使用 Exponent CMS，你可以基于用户和内容设置审批策略，尽管这个 CMS 是以模块为中心而非以用户为中心的。例如，你可以为 Calendard 模块创建审批策略




## 内容管理系统

仅当其他管理员至少两次批准请求的更改后，这些更改才会显示。虽然你可以为模块向用户或组分配权限，但这是通过每个特定模块进行的，而不是通过用户界面。没有各种级别的用户访问权限——要么用户是管理员，要么不是。此外，虽然你可以查看哪些用户对哪些模块有权限，但你无法查看单个用户负责的所有模块。

此外，Exponent CMS 在管理界面的 Configure Site（配置站点）区域中提供了一些对设置的控制。

##### 数据库设置

你可以在 MySQL 和 PostgreSQL 之间切换，当然也可以更改数据库名称、用户名、密码、端口以及任何表前缀名称。

##### 显示设置/主题

站点预先打包了若干主题，但通过编辑相应文件（或从头创建自己的主题）来创建自己的主题也非常简单。除非你喜欢重新造轮子，否则我们的建议是选择最接近你想要布局的主题，并在此基础上进行编辑。每个示例主题底部（在“管理主题”页面下）都有一个链接，允许你查看该主题的完整文件列表，使你能够轻松查看需要修改哪些文件以满足你的需求。

在此部分中，你还可以更改对其他贡献者的引用方式，以及向网站访客显示日期和时间的方式。

##### 通用配置设置

在此部分下，你可以自定义页面标题、元标签和关键词，以及语言选择。你还可以开启/关闭用户注册，启用 CAPTCHA（计算机自动化公开图灵测试，用于区分计算机和人类）测试以防止机器人注册，并控制会话超时和 SSL 设置。

##### SMTP 设置

这是设置你的 SMTP 端口、用户名、密码、身份验证方法等等的地方。如果你愿意，也可以在此处切换到 `php_mail()` 函数。

##### 其他插件

除了激活/停用预安装的模块以及安装新提供的模块外，大众还提供了一份相当多的其他贡献列表。这可以通过 Exponent 的 Sourceforge 界面站点在 http://www.sourceforge.net 的“Tracker”贡献部分获得。它包括一些相当有用的插件，例如添加水平下拉导航，因此请务必查看一下。

##### 更改模块的布局和外观

虽然使用 ExponentCMS 添加和删除模块很容易，但在页面上移动它们更容易。然而，使模块看起来彼此不同证明是一项挑战。

# 第 13 章

##### 优缺点

该套件的优点是：

- 更改模块的布局和位置证明是一项简单的任务，且具有所见即所得（WYSIWYG）的特性。此外，你可以打破传统的两列或三列布局，并为所有三个传统列添加子列。
- 文本模块会跟踪修订，并允许你通过单击立即查看或恢复旧版本。如果能显示*谁*进行了修订就更好了，但也许该功能将在未来的版本中提供。
- 预览功能让你可以看到你的更改对站点外观的影响，而无需注销管理员身份。
- 与其他一些侧重于功能驱动的内容管理系统（CMS）相比，主题更具神秘感和设计驱动性。

一个缺点在于用户管理——管理员无法看到单个用户拥有的所有权限或模块职责。例如，如果 Bob 要去度假，你想将 Bob 的模块分配给其他人，没有简单的方法可以看到 Bob 能够做什么以及他可以修改哪些模块。

CMS 位于 Sourceforge 前 10 名“最活跃”下载列表上是有原因的。ExponentCMS 是迄今为止最易于管理的开源 CMS。然而，其优势更多在于幕后，因为其重点不一定在于与访问大众站点的互动性，而在于管理员可以控制的核心贡献者群体。如果你在寻找一个外观良好的“开箱即用”站点，ExponentCMS 应该在你的评估名单上。

#### XOOPS

XOOPS（eXtensible Object Oriented Portal System，可扩展面向对象的门户系统）是另一个流行的综合 CMS，可在 Sourceforge 或 http://www.xoops.org 上获取。最新版本是 2.1.1，这里讨论的就是该版本（实际上这是 2.2 版本的预发布版，因此请记住这一点）。

###### 安装说明

XOOPS 团队编写了一份非常全面的安装指南，不仅指导你完成安装和设置过程，还为你提供了有关文件将放在哪里以及原因的详细开发信息。你应该阅读这份文档——它可以在 http://docs.xoops.org/modules/xdocman/index.php?doc=xu-002&lang=en 找到。

在安装之前需要注意几件事：

- 解压缩 tar 文件后，你需要将 html 文件夹复制到网站根目录（如 htdocs 或 public_html）。XOOPS 团队建议你将该文件夹重命名为 xoops，但这真的取决于你。
- 如果你正在远程服务器上安装，你需要在安装之前创建数据库、用户和密码。如果你正在本地安装，安装向导将为你完成此任务。
- 一旦你解压缩了文件，你需要对以下目录和文件执行 chmod 操作以使它们可写：
  - uploads/
  - cache/
  - templates_c/
  - mainfile.php
- 为了让 XOOPS 安装向导正确完成过程，你的浏览器必须启用 Cookie 和 Javascript。

##### 概览/默认安装

有几个功能是默认激活的：

- **横幅管理**：管理横幅广告和点击通过。
- **图像管理器**：管理图像以及谁可以上传它们。
- **表情符号**：管理“表情符号”及其显示方式。
- **头像**：管理头像。
- **评论管理器**：管理用户发布的评论。
- **用户管理**：编辑、电子邮件、搜索、更改用户级别。
- **模块**：管理模块（如“谁在线”和“最新评论”）。

默认安装的唯一模块是系统管理员模块。作为包的一部分默认提供（但需要逐个安装）的其他模块包括：

- **联系我们**：向网站管理员发送消息。
- **下载**：组织上传的文件，并允许用户对其进行排名。
- **链接**：链接管理器。
- **论坛**：站点论坛（由 phpBB 组创建）。
- **新闻**：管理用户提交的新文章。
- **版块**：允许管理员发布站点不同的版块。
- **常见问题解答**：管理站点的常见问题解答。
- **头条新闻**：来自其他站点新闻的 RSS 源。
- **成员列表**：显示站点的注册用户。
- **合作伙伴**：组织和显示合作伙伴网站。
- **投票**：管理在线调查和投票。

##### 自定义默认安装

截至撰写本文时，XOOPS 网站上有超过 300 个附加模块可供下载。有一个模块几乎可以做你想做的任何事情，包括交易功能（购物车），这在同类 CMS 中并不常见。

在管理控制面板的系统管理员部分下，你会发现以下区域，可以进一步自定义你的安装：

- **头像**：允许你为用户上传可用的头像。
- **横幅**：管理你的横幅广告，并提供点击通过率和哪些横幅处于活动状态的统计数据。
- **模块**：提供添加新模块的界面并确定它们在站点上的布局。
- **评论**：允许你查看、编辑和删除评论。
- **查找用户**：不允许自定义站点，但提供广泛的搜索界面来筛选用户。
- **组**：这是你将用户分配给不同组并为该组设置权限的地方。权限位于系统、模块和块级别，并允许管理或访问权限。
- **图像管理器**：管理图像库。
- **邮件用户**：不允许自定义站点，但允许你向用户发送电子邮件。
- **模块**：允许你安装并激活或停用可用模块。
- **偏好设置**：提供站点的一般自定义，并分为几个类别：
  - **通用设置**：允许你更改站点名称、标语、管理员电子邮件地址、默认语言、起始页模块、服务器和默认时区、默认主题（只为你安装了三个）、用户主题、匿名用户用户名单、gzip 压缩、cookie 和会话信息、站点是否完全下线、站点下线时的自定义消息、IP 地址、SSL 设置、被禁止的 IP 地址以及配置缓存设置。
  - **用户信息设置**：允许你设置密码和用户名设置、用户将属于的默认组、头像设置、被禁止的用户名（如“admin/”）以及更改注册免责声明。
  - **元标签和页脚**：允许你设置元标签信息，如关键词、描述、机器人、评级、作者、版权以及页脚信息。
  - **词汇审查选项**：允许你审查不需要的词并用你选择的词替换它们。
  - **搜索选项**：允许你开启或关闭全局搜索设置，并要求用户驱动的搜索具有最小关键词长度。
  - **邮件设置**：允许你配置邮件服务器设置和邮件方法。





##### 表情符号
控制论坛中的表情符号，并允许您创建自己的表情符号。

##### 模板
允许您将模板上传到站点。

##### 用户等级
控制论坛的用户等级系统，并允许您为定义的某些级别配置最低发帖数量。

##### 编辑用户
允许您删除用户并编辑其信息——昵称、姓名、电子邮件、URL、时区、即时通讯信息、位置、职业、兴趣、签名、评论功能、通知、等级、密码和组。

##### 优势与劣势

该包中最出色的部分包括：

- 庞大的用户群和支持论坛使开发人员能够轻松找到问题的解决方案或排除故障区域。
- 单词审查选项是一个不错的优势。
- 由于论坛模块由 phpBB 小组开发，论坛控制功能高度可定制且细节丰富。

可能需要改进的领域包括：

- 尽管核心文档非常详尽，但附加模块的文档却相当缺乏。由于附加功能可能占网站很大一部分，这可能会让没有经验的人感到沮丧。
- 默认安装仅包含三种主题，考虑到如此庞大的支持和用户基础，理应可以有更多预装的主题。

XOOPS 因其潜力而受欢迎，尽管你必须愿意解读其他人的代码，并且有时间的余裕来微调你的安装以符合你的特定需求。虽然它作为“开箱即用”的解决方案并不是很出色，但只要你愿意并有能力花些时间编写代码，它几乎可以完成你需要的任何任务。它非常面向用户，允许你作为管理员将环境控制得一丝不苟，甚至细到“表情符号”。如果你专注于与任何造访你网站的人创建一个互动社区，你应该对 XOOPS 进行第二次审视。

#### phpWebsite

phpWebsite 可以在 http://phpwebsite.appstate.edu 获取。在撰写本文时，phpWebsite 的最新版本是 0.10.01，并将作为本文讨论的基础。

###### 安装说明

阿巴拉契亚州立大学（phpWebsite 的创造者）的友好人士已经设置了一个命令行安装过程，允许你直接从 phpWebsite 站点进行安装。你也可以分部分下载应用程序（核心、主题包等）并自行安装。

# 第 13 章

在安装之前，有几件事需要注意：

- 你需要安装以下 PEAR 库才能运行核心应用程序：
    - Benchmark
    - DB
    - Date
    - HTML_BBCodeParser
    - HTML_Common
    - HTML_Form
    - HTML_Table
    - HTML_Template_IT
    - Mail
    - Mail_Mime
    - Net_CheckIP
- 如果可能，在安装前你需要以 root 身份登录。脚本会检测你是否不是 root 用户，并设置带有某些安全限制的应用程序。如果你尝试切换用户，它将保留原始设置，而不会执行 root 安装。
- 你必须拥有 wget，否则安装程序将无法运行。

##### 一般概述/默认安装

对你立即可用且处于活动状态的模块包括：

- **Apache 控制器：** 允许管理员更改 Apache 设置。
- **帮助系统：** 帮助管理员导航系统。
- **语言管理员：** 管理站点使用的语言。
- **布局管理器：** 管理你的站点布局。
- **站点搜索：** 搜索站点。
- **用户管理器：** 审批用户以在站点进行不同级别的修改。
- **公告：** 管理发布在站点上的公告。
- **区块生成器：** 允许你创建和管理区块。
- **分支创建器：** 管理在主站点下创建的衍生站点。
- **Calendarr：** 站点的 Calendarr。
- **评论管理器：** 管理评论。
- **调试器：** 协助管理员定位和修复错误。
- **文档：** 文件管理器。
- **常见问题解答：** 管理站点常见问题解答。
- **链接管理器：** 组织并显示链接。
- **菜单管理器：** 管理动态菜单。
- **模块生成器：** 允许你创建自己的模块。
- **笔记：** 向站点用户发送电子邮件。
- **Web 页面：** 管理站点上的静态页面。
- **表单生成器：** 创建表单。
- **相册：** 组织和管理在线图片库。
- **留言板：** 管理论坛。
- **RSS 新闻源：** 管理信息源。
- **投票：** 管理在线调查和投票。
- **骨架模块：** 用作模板的示例模块。
- **管理统计：** 跟踪最活跃的模块和用户。

##### 自定义默认安装

与所有 CMS 包一样，其精髓在于修改默认安装，使其真正符合你的需求。

添加、删除和编辑用户及其权限可以在管理控制面板的用户管理部分完成。在这里，你可以设置是否允许用户注册，以及他们是否需要在参与论坛等活动之前获得批准。你还可以创建自己的身份验证脚本或使用本地数据库来验证用户。如果赋予用户管理员状态，你可以控制他或她可以访问哪些模块，以及可以在该模块内执行哪些特定功能。例如，用户可以创建投票，但不能编辑、删除或列出投票。

可以更改模块的布局，但与其他一些功能相比，操作起来并不那么简单。你可以更改每个特定模块的外观，这是一个不错的功能。

HTML 页头信息（元标签、关键字等）在管理控制面板的布局管理部分控制。这有点出乎意料。

目前，`http://www.sourceforge.net` 上还有 21 个其他主题供你使用并下载。

##### 优势与劣势

该包中最吸引人的功能包括：

- 管理员可以获取大量的统计信息，这使得微调站点变得更加容易。
- 创建自己的授权脚本的能力是一个不错的功能。
- 管理员可以单独更改框和模块的外观，因此同一页面上的所有框不必看起来相同。
- 允许非常详细的用户权限，这使得查看谁被允许做什么变得简单明了。
- 默认模块非常全面，使开发人员构建综合站点的工作量减少。

唯一的缺点是，目前，该系统不允许打破传统的两列或三列布局。

phpWebsite 是一个不错的“中庸”CMS，平衡了高水平的内置功能和高度的用户交互性。如果你正在寻找一个能够支持中等规模贡献者群体，并仍能促进访客交互性的包，那么这可能就是适合你的 CMS。

#### TikiWiki

该软件可以在 http://www.tikiwiki.org 获取，在撰写本文时，当前可用版本为 1.9.0。

###### 安装说明

如果你使用的是旧版本的 PHP（4.3 之前）或 MySQL（4.0.1 之前），那么你应特别关注“要求和设置”文档，该文档可以在 http://doc.tikiwiki.org/tiki-index.php?page=requirements+and+setup 找到。其他注意事项包括：

- PDF 生成模块需要安装 php-xml 包。
- 由于使用了会话，请确保你的 php.ini 文件具有以下设置：
    - `session.save_handler = files`
    - `session.save_path = /tmp`（用于本地安装）

你还需要在安装之前创建数据库和用户/密码。安装包可以从该网站下载，或者如果你正在安装到远程服务器，安装页面上有一个单独的链接，标题为 InstallWithOnlyFTPAccess，这是适合你的方法。

##### 默认安装

有几个功能是默认激活的：

- **游戏**：允许用户在你的网站上玩游戏并跟踪游戏统计信息。
- **分类**：管理任何模块都可以归类的分类。
- **日历**：允许用户查看带有事件的日历。
- **MyTiki**：为登录用户提供他们自己的界面，具有日历、网页邮件、菜单和记事本等功能，并允许管理员开启或关闭用户功能。
- **投稿**：允许用户提交文章。
- **自动链接**：允许输入到文本中的 URL 自动提交到链接目录。
- **搜索与全文搜索**：允许用户搜索你的网站。
- **HTML 页面**：管理可编辑的 HTML 代码块，以便在整个网站中重用。

318





## 内容管理系统

- **帮助系统：** 管理帮助台。
- **Galaxia 工作流引擎：** 允许管理复杂的工作流流程。
- **Wiki（维基）：** 协作文档系统；还允许授权用户创建和编辑静态 HTML 页面的内容，并提供所见即所得的 HTML 编辑器和拼写检查器等高级功能。
- **文章：** 组织和管理文章。
- **博客：** 博客管理。
- **目录：** 对链接进行分类的链接管理器。
- **文件库：** 组织和管理上传的文件。
- **常见问题解答：** 管理网站的常见问题解答。
- **地图：** 允许显示交互式地图。
- **追踪器：** 为你管理和组织自定义数据。
- **热门词：** 允许你将网站上的特定词嵌入为链接。
- **联系我们：** 一个允许用户联系你的简便表单。
- **统计：** 管理每个可能激活模块的网站统计数据。
- **引荐统计：** 管理引荐网站的统计数据。
- **调试器控制台：** 协助开发人员调试网站。

其他预装但只需点击按钮即可激活的功能包括：

- **评论：** 允许用户评论网站各处的图像、文章和其他内容。
- **图片库：** 允许用户对图像进行排名、查看和上传。
- **新闻阅读器：** 新闻 RSS 源。
- **投票：** 管理在线投票。
- **测验：** 允许用户进行测验并评分。
- **精选链接：** 管理在你的 Tiki 站点内打开的链接；跟踪链接统计。
- **横幅：** 管理横幅活动和点击。
- **新闻通讯：** 管理网站的新闻通讯广播并允许用户订阅。
- **论坛：** 管理论坛。
- **喊话框：** 允许用户在动态窗口中显示短行文本。
- **调查：** 管理在线调查。
- **年鉴：** 允许你显示为一年中每天定制的图像和文本。
- **实时支持系统：** 允许用户向实时帮助台寻求帮助。
- **Babelish 翻译：** 允许用户翻译网站的各个部分。
- **集成器：** 允许你将外部 HTML 页面导入网站。
- **禁止系统：** 允许你轻松禁止用户。
- **用户功能：** 允许用户加入书签、跟踪文件、向其他用户发送消息以及执行其他操作。

##### 自定义默认安装

网站的 Admin（管理）部分有几个提供自定义功能的子部分。它们是：

- **功能**：在此部分，管理员可以激活和停用功能，并更改网站的整体布局。
- **常规偏好设置**：在这里，你可以更改主题，更改或创建自定义主页，设置语言偏好，设置操作系统类型，更改 PHP 错误报告级别，设置网站关闭时的自定义消息，限制网站用户数量和负载，设置缓存偏好，设置新链接的打开方式，控制所有组是否可以看到所有模块，设置是否将管理页面浏览量计入统计，更改菜单显示，设置服务器配置，设置会话偏好，管理日期/时间格式，并更改管理密码。
- **用户注册和登录**：此区域专门用于允许你控制用户注册和登录过程的各个方面，从身份验证到密码要求，再到 HTTP/S 设置，甚至是 TikiWiki 使用的 PEAR::Auth 模块的设置。
- **已启用功能的配置（例如 Wiki）**：对于你在“功能”屏幕上启用的各种功能，你将能够访问各个部分以进一步自定义其设置。由于 Wiki 是该项目早期的重点，Admin 站点的这一部分提供了大量的控制、可定制性和功能。简而言之，你可以转储、恢复和附加文件，控制数据库和评论设置，导出，配置链接格式并设置 Wiki 文档保留的信息（版本控制、用户数据、日期、链接、状态等）。你还可以管理版权保护、Wiki 历史并配置监视。你可以打开和关闭的一些 Wiki 功能包括：
  - 邮件输入
  - 沙箱
  - 最近更改
  - 历史
  - 排名
  - 撤销
  - 多重打印
  - PDF 生成
  - 评论
  - 拼写检查器
  - 编辑冲突警告
  - 独立缓存
  - 脚注
  - 使用 WikiWords
  - 自动等宽文本

其他可用功能（文章、博客、图片库等）也允许一定程度的自定义，但没有 Wiki 部分那么详细。

##### 优点和缺点

TikiWiki 的优点包括：

- 文档和支持社区非常广泛，与其他许多开源 CMS 包一样。
- 强大的 Wiki 自定义使在线协作变得容易。
- 默认安装附带 35 个主题，它们都是基本的 CSS 文件，便于进一步自定义。
- 每个可能的激活模块都有详尽的统计数据。
- 这个 CMS 是最全面的之一；它几乎包含了所有可以想到的模块（除事务性功能外），并且无需安装额外的插件或附加组件即可轻松进行自定义。

关于缺点，Galaxia 工作流有点复杂，需要单独阅读才能理解系统是如何设置以及如何为你工作的。这也可能成为 TikiWiki 的一个优点，因为一旦你能够驾驭该系统，它可以为你提供管理复杂项目的非常全面的工具。

使用此软件，你可以快速提供用户想要的任何功能。事实上，通过此软件可用的功能如此之多，初级 web 开发人员可能会因为“因为能所以做”而使用太多模块。我们的建议是，如果你确切知道你的网站需要什么，并且如果你有大量将参与网站实际内容贡献的用户，你应该肯定考虑这个 CMS。

#### 其他

还有许多其他可用的开源 CMS 包。以下几个值得提及的是：

- **Mambo**：可在 http://www.mamboserver.com 获取。这是一个流行的 CMS，提供基本的预安装功能，下载量巨大。该项目促进了一个健康的支持系统，用户基础相对易于管理，而无需深入代码。
- **Drupal**：可在 http://www.drupal.org 获取。这是另一个专注于功能而非形式（外观）的流行 CMS。附带几个主题，但不深入代码，自定义受限。一个不错的功能是“最近系统事件”，它在管理员登录时显示，使管理员可以 easily 看到发生的事件。
- **PHP-Nuke**：可在 http://www.phpnuke.org 获取。这是最古老的基于 PHP/MySQL 的 CMS 之一。它自 2000 年以来就存在，拥有最大的 CMS 支持社区之一。它目前仍在开发中，但坏消息是它不再免费——你现在需要支付最低费用才能下载最新版本。如果你愿意成为 PHP-Nuke 精英的一员，你也可以加入 PHP-Nuke 俱乐部（需另付费）。
- **Postnuke**：可在 http://www.postnuke.com 获取。另一个“老牌子但依然好用”的 CMS，它在 PHP-Nuke 之后不久推出，因此得益于其广泛的用户和开发人员社区。有许多可用的附加组件、语言包和用户论坛，可帮助你自定义这个 CMS 包。

### 微型 CMS

你可能只想要较大 CMS 包中的一项功能来用于你自己的网站。幸运的是，你也拥有可用的微型 CMS 包。这些“迷你”CMS 包有一个特定目的，例如博客或维基。如果你只需要网站上的一个功能，它们是完美的解决方案。接下来的部分简要介绍了这些包。

最受欢迎的两个微型 CMS 包是博客和维基。因此，这些领域受到了更多的关注。

#### 博客的魔力

研究表明，博客及其读者的流行度正在增加。PEW Internet & American Life Project 的一项研究表明，2002 年，只有 3% 的互联网用户拥有博客。2003 年，这一数字增加到 5%，而 2004 年，这一数字上升到 7%。将此乘以仅在美国估计的 1.2 亿互联网用户，这意味着相当大量的博客写作活动。

不仅人们在写博客，而且越来越多的人花时间阅读它们。Hostway, Inc. 在 2005 年 4 月的一项调查显示，大约 30% 的受访者阅读过博客，分析师预测这一数字在未来几年将大幅增长。

##### 为什么要写博客？

写博客的原因有很多，从个人到政治到企业议程不一而足。这种免费、即时、互动的通信机制是分享观点和想法的完美论坛。博客可以是关于任何事情的，其非正式的性质吸引了几乎所有人。

博客的存在是为了：

- **分享政治观点**：许多政治家和高调的政治活动家正在使用博客来接触大众并促进他们自己的议程。
- **进一步实现企业目标**：公司开始搭上这股潮流，提供关于其产品和服务的博客。一些是由消费者自己写的。一些公司正在使用博客来通知其忠实的读者即将发布的产品或其他公司新闻。
- **分享个人观点**：在这个拥挤的星球上，在这个拥挤的互联网上，有时人们只是想被听到。也许他们想与来自世界各地的亲朋好友分享他们当前的经历。或者他们可能有一些想与初学者分享的专家建议。在程序员的世界里，你可能有一些代码片段要分享，或者你想告诉其他人的酷产品或链接。列表还在继续。




## 内容管理系统

##### WordPress

WordPress 是一个出色的“开箱即用”博客套件，提供了极佳的自定义能力和功能。它可在 http://www.wordpress.org 获取，本文撰写时的当前版本为 1.5.11。

###### 安装说明

安装此套件极其简单且快速。在安装之前，请确保您正在运行 PHP 4.1+ 和 MySQL 3.23.23+，并且已创建数据库以及用户名/密码。您所需的其他文档便位于 http://www.wordpress.org 网站上，方便您查阅。

###### 功能概述

WordPress 为您的博客提供了多种功能和自定义领域，包括：

- **用户注册系统**：允许您授权其他用户发布、编辑和删除您站点中的博客内容，并拥有 10 个不同级别的用户访问权限。您还可以要求在草稿发布之前执行“审批”流程。
- **静态内容页面**：允许您向站点添加静态页面，并通过 WordPress 界面进行管理。
- **添加链接或博客滚**：您可以通过 WordPress 界面管理和组织外部链接。
- **主题**：默认安装中内置了 35 个主题，并且您可以通过下载近 150 个额外主题轻松自定义博客的外观和感觉。
- **评论系统**：允许您接受、审查和修改用户发布的评论，并包含垃圾邮件拦截功能以防止垃圾帖子出现。访客还可以通过 Trackback 和 Pingback 在他们自己的网站上对您的博客发表评论。
- **隐藏帖子**：允许您对某些仅由您自己或创建该帖子的作者可见的帖子进行密码保护。
- **导入数据**：允许您从其他流行的博客套件（包括 MovableType、Blogger 和许多其他套件）中导入数据。
- **RSS 源**：允许其他人联合发布您的博客。
- **邮件发文**：允许您通过电子邮件系统提交博客帖子。

这个博客套件还有其他不错的功能，例如完全符合标准、易于升级，以及使用 Texturize 引擎美化纯 ASCII 文本。

###### 总结

一旦深入接触 WordPress 套件，您会发现它文档齐全、安装简便、易于配置和自定义，且功能强大。如果您有任何问题或麻烦，它还有一个优秀的支持和开发社区。如果您只是想创建站点上的博客，WordPress 几乎无可匹敌。

##### Serendipity

另一个出色且结构良好的博客是 Serendipity，可在 `http://www.s9y.org` 下载。其开发团队拥有一些重量级的 PHP 开发者，包括 Sterling Hughes、George Schlossnagle、Wez Furlong 和 Sebastian Bergmann 等人。它也是许多核心 PHP 开发者的首选博客套件。

###### 安装说明

与 Wordpress 一样，安装是一项快速且简单的工作。您应该运行 PHP 4 或更高版本，以及 `MySQL`、`PostgreSQL` 或 `SQLite` 作为您的数据库。唯一需要注意的其他事项是，记得在安装后限制文件权限，具体方法见其位于 `http://www.s9y.org/index.php?node=36` 的详尽安装文档中。

###### 功能概述

Serendipity 提供与 Wordpress 相似的功能，例如允许管理员设置用户权限，使并非所有用户都能发布博客条目，以及审核评论或启用 CAPTCHA 以防止垃圾邮件。使用 Serendipity，您可以向博客帖子添加图片、更改站点主题、导入和导出数据，并为他人提供 trackback 和 pingback 以引用您的帖子。与 Wordpress 类似的还有符合标准的代码和可提供的 RSS 源。

一些 Wordpress 中不太显而易见的额外功能包括：

- 可选的 Wysiwyg 编辑器：HTMLArea、FCKeditor、xinha、TinyMCE
- 支持 `MySQL`、`PostgreSQL` 和 `SQLite`
- 多用户博客：一次 serendipity 安装可以为独立网络日志提供服务。

###### 总结

Serendipity 简单、整洁且稳固。如果您正在寻找一个只做它应该做的事情且非常可靠的博客，Serendipity 是一个绝佳的选择。

#### Wiki

就像程序员、编码人员和网络开发者都使用软件来管理软件包的开发和部署一样，他们也开始使用 wiki 来协作并创建综合文档来补充这些软件包。

##### Wiki 的起源

根据维基百科，*wiki* 一词源于夏威夷语术语 *wiki wiki*，意为“快速或非正式”，特别是在指代檀香山机场的公交车时。这个短语由 Howard (“Ward”) Cunningham 早在 1995 年创造，作为对波特兰模式仓库的引用，这是一个软件开发想法的协作。

随着互联网扩展到大众，wiki 概念的普及程度大幅上升，特别是在开源社区，许多人承担社区责任，持续改进现有产品。文档是使用户理解应用程序功能或能力的重要组成部分。

Wiki 站点不仅限于支持开源项目，还可以作为几乎任何事物的通用参考指南。有爱好导向的 wiki、语言 wiki、游戏 wiki——可以想象，您几乎可以为任何主题创建 wiki。

##### MediaWiki

其中一个较流行的套件，也是维基百科背后的智力支持，是 MediaWiki。它可在 http://wikipedia.sourceforge.net 获取。本文撰写时的最新版本是 1.4.4，这里将以此为重点进行讨论。

###### 安装说明

在安装 MediaWiki 之前，您应注意以下几点：如果您拥有 root 访问权限，则无需在安装前创建数据库。如果您在远程服务器上安装，则需要在安装前自行创建数据库。此外，在文件解压后，您需要 chmod 配置目录，使其可写。安装完成后，您还需要重置权限。

完整的安装指南可在 MediaWiki 网站上找到：http://meta.wikimedia.org/wiki/MediaWiki_User%27s_Guide:_Installation。

###### 功能概述

由于该站点的目的是跟踪不断发展的文本库，因此它具有管理用户、其输入和版本控制的优异功能。可用的一般功能包括：

- **用户自定义和访问**：用户可以通过编辑自己的模板来自定义自己的时间界面，设置诸如时区和每页结果数量等偏好。管理员可以向用户组分配不同级别的权限，开启或关闭他们编辑、移动、贡献或上传文件等能力。
- **搜索功能**：站点访客可以对站点包含的所有文章进行全文搜索。
- **报告**：可以生成提供特定使用统计、文章和链接、文章活动和流行度、图像、用户等统计信息的报告。
- **编辑文章**：用户可以决定只编辑文章的一部分，如果发生编辑冲突，文章可以合并，用户可以在提交前预览他们的编辑，并为用户提供编辑工具栏以方便编辑过程。
- **文章组织**：文章可以分类和子分类到无限的类别中。
- **文本和链接控制**：用户在提交文本更改或输入新文本时可以使用受限或完整 HTML 代码。嵌入式超链接也可以进行管理。
- **监视列表**：此功能协助管理员和用户跟踪用户的编辑和贡献。它可以显示特别感兴趣的文章、最近的更改以及哪些用户贡献最多。此功能甚至提供文章编辑前和编辑后的并排视图，并突出显示更改，以便读者轻松识别更改。





# 第 13 章

- **多媒体功能：** 用户可以上传其他类型的文件，包括图像、声音文件、数学公式和图表。
- **多语言支持：** 目前支持众多语言，并具备在不同语言的文章之间建立链接的能力。

如需查看此软件包中所有可用功能和特性的完整列表，请访问位于 http://meta.wikimedia.org/wiki/MediaWiki_feature_list 的 MediaWiki 功能列表。

###### 总结

只需访问维基百科（http://www.wikipedia.org）就能完全掌握使用 MediaWiki 所能完成的所有事项。它功能强大、高度可定制，并且是现有最健壮的 Wiki 软件包之一。

##### DocuWiki

另一个 Wiki 软件包是 DocuWiki，可从 http://www.splitbrain.org/go/dokuwiki 获取。使其与其他 Wiki 不同的地方在于它使用扁平文件，从而免除了用户对数据库的依赖。

###### 安装说明

DocuWiki 是另一个开源软件包，提供“开箱即用”的安装体验——只需解压并更改权限即可安装。根据位于 http://wiki.splitbrain.org/wiki%3AInstall 的详细安装说明，你唯一需要做的操作是创建一个空的日志文件。

###### 功能概览

该 Wiki 提供了许多功能，包括：

- **区块编辑**：允许用户仅编辑页面的某一部分。
- **版本对比**：提供两个版本文档之间的彩色高亮差异显示。
- **用户访问控制**：允许管理员为用户分配权限。
- **图像上传**：允许用户在 Wiki 文档中包含图像。
- **多语言支持**：提供对不同语言的支持。
- **签入/签出**：防止编辑冲突

###### 总结

该 Wiki 唯一缺乏的是与数据库相关的功能，例如页面跟踪和引用统计。与其他一些 Wiki 软件包不同，它也不提供备份工具或允许用户对贡献进行评论。除此之外，这是一个简单而稳固的 Wiki 软件包，是一个极佳的选择，特别是当你无法访问数据库时。

#### 其他微型 CMS 软件包

尽管本章迄今为止主要关注博客和 Wiki，但你可能已经开发了一个网站，需要“插入”一些额外的功能。有许多专用的 CMS 可以简化你的工作，并让你无需从头编写代码即可轻松增强网站。

一些更流行的微型 CMS 软件包包括：

- **发布/新闻管理 CMS：** FusionNews，可从 `http://www.fusionphp.net` 获取
- **学习管理环境 CMS：** Moodle，可从 `http://www.moodle.org` 获取
- **事务处理 CMS：** osCommerce 或 ZenCart，分别可从 `http://www.oscommerce.com` 和 `http://www.zencart.com` 获取
- **图像画廊：** Coppermine，可从 `http://coppermine.sourceforge.net` 获取
- **论坛：** phpBB，可从 `http://www.phpBB.com` 获取
- **聊天室：** phpmyschat，可从 `http://phpmyschat.sourceforge.net` 获取
- **投票/调查：** PrestoPoll，可从 `http://prestopoll.sourceforge.net` 获取
- **日历系统：** WebCalendar，可从 `http://www.k5n.us/webcalendal.php` 获取

#### 其他有用资源

还有其他地方可以帮你梳理混乱的局面——这些地方专门致力于比较、评估并追踪市面上众多的 CMS。仅列出以下几个供你起步参考：

- **OpenSourceCMS：** `http://www.opensourcecms.com`。该网站旨在让你对市面上几乎任何 PHP/MySQL CMS 进行“试运行”，让你亲眼看到每个 CMS 提供哪些功能、管理界面运行得如何以及 CMS 本身的深度和广度。这个网站有几个很好的地方：首先，你不必花时间安装整个软件包仅为了演示软件；其次，他们只展示那些可在远程服务器（无需 root 权限）以及主服务器本身上可用的 CMS。如果某个 CMS 未出现在列表中，那么要么是他们无法轻松安装它（这是另一个不错的过滤条件），要么是他们尚未知晓该 CMS。该网站还提供了其他用户的评论，以完全客观的观点进行评价。

使用此网站唯一的缺点是，当你正在使用该软件时，其他人也在同时“玩弄”该软件，这会导致评估结果有趣且可能出现意外结果。幸运的是，服务器每两小时刷新一次演示软件，因此最终你将能够看到一个“干净”的副本。

- **CMSReview：** `http://www.cmsreview.com`。这是一个综合性的 CMS 网站，提供了关于如何确定公司 CMS 需求以及在哪里寻找 CMS 顾问的优质资源，并且如果你遇到任何不熟悉的专业术语，还提供了一个指向 CMS 术语表的便捷链接。
- **CMSMatrix：** `http://www.cmsmatrix.org`。如果你希望在一个公平的基础上比较众多 CMS 软件包（无论是开源还是非开源），这将是一个很好的资源。它比较直接且深入，但包含大量信息。
- **CMSWire：** `http://www.cmswire.com`。这个新闻导向的 CMS 网站让你了解最新的 CMS 发展趋势以及各行业中 CMS 的使用趋势。如果你致力于保持在 CMS 世界的前沿，你可能想要获取该网站的 RSS 源。

### 摘要

希望本章为你提供了足够的见解，以便对 CMS 软件包做出明智的选择。正如所示，有众多开源解决方案可以满足几乎任何需求，从非常全面的到非常特定和量身定制的。虽然很多时候，选择合适的 CMS 取决于个人偏好，但你至少有了一个出发点，可以据此形成这些主观意见。

![Image](img/ab27c6ac898db1f934d39fa127b14657_354_0.png)

# 语言翻译

### 注释

**PHP**

```php
// Single-line comment
```

```php
/*
   Multi-line comment
   */
```

**ASP/VBScript**

```vb
' Single-line comment
```

**ASP.NET/C#**

```csharp
// Single-line comment
```

```csharp
/*
   Multi-line comment
   */
```

**JSP/Java**

```java
// Single-line comment
```

```java
/*
   Multi-line comment
   */
```

# 附录 A

## 变量类型

- **PHP**：弱类型
- **ASP/VBScript**：弱类型
- **ASP.NET/C#**：强类型
- **JSP/Java**：强类型

## 变量声明

- **PHP**
  ```php
  $variable = value;
  ```
- **ASP/VBScript**
  ```vb
  Dim variable
  ```
- **ASP.NET/C#**
  ```csharp
  type variable;
  ```
- **JSP/Java**
  ```java
  type variable;
  ```

## 常量声明

- **PHP**
  ```php
  define('NAME', value);
  ```
- **ASP/VBScript**
  ```vb
  Const name = value
  ```
- **ASP.NET/C#**
  ```csharp
  const type name = value;
  ```
- **JSP/Java**
  ```java
  visibility final type = value;
  ```

## 创建数组

**PHP**

```php
$name = array(elem1, elem2, elem3);

$name = array('key1' => elem1, 'key2' => elem2, 'key3' => elem3);
```

**ASP/VBScript**

```vb
Dim name(length)
```

**ASP.NET/C#**

```csharp
type[] name = new type[length];
```

**JSP/Java**

```java
type[] name = new type[length];
```

## 引用数组元素

**PHP**

```php
$name[index]

$name['key']
```

**ASP/VBScript**

```vb
name(index)
```

**ASP.NET/C#**

```csharp
name[index]
```

**JSP/Java**

```java
name[index]
```

## 条件评估

**PHP**

```php
if (condition) {
...
} elseif (condition) {
...
} else {
...
}
```

**ASP/VBScript**

```vb
If condition Then
...
Elseif condition Then
...
Else
...
End if
```

**ASP.NET/C#**

```csharp
if (condition) {
...
} else if (condition) {
...
} else {
...
}
```

**JSP/Java**

```java
if (condition) {
...
} else if (condition) {
...
} else {
...
}
```

## 多重选择

**PHP**

```php
switch (expr) {
case value1:
...
break;
case value2:
...
break;
default:
...
}
```

**ASP/VBScript**

```vb
Select Case expr
Case value1
...
Case value2
...
Case Else
...
End Select
```




# 附录 A

### 语言转换

## 切换语句

**ASP.NET/C#**
```csharp
switch (expr) {
  case value1:
    ...
    break;
  case value2:
    ...
    break;
  default:
    ...
    break;
}
```

**JSP/Java**
```java
switch (expr) {
  case value1:
    ...
    break;
  case value2:
    ...
    break;
  default:
    ...
    break;
}
```

## 循环：While

**PHP**
```php
while (expr) {
  ...
}
```

**ASP/VBScript**
```vb
While expr
  ...
Wend
```

**ASP.NET/C#**
```csharp
while (expr) {
  ...
}
```

**JSP/Java**
```java
while (expr) {
  ...
}
```

## 循环：Do... While

**PHP**
```php
do { ... } while (expr);
```

**ASP/VBScript**
```vb
Do ... Loop Until expr
```

**ASP.NET/C#**
```csharp
do { ... } while (expr);
```

**JSP/Java**
```java
do { ... } while (expr);
```

## 循环：For

**PHP**
```php
for (expr1; expr2; expr3) { ... }
```

**ASP/VBScript**
```vb
For expr1 To expr2 Step expr3 ... Next
```

**ASP.NET/C#**
```csharp
for (expr1; expr2; expr3) { ... }
```

**JSP/Java**
```java
for (expr1; expr2; expr3) { ... }
```

## 循环：For Each

**PHP**
```php
foreach (array as $item) {
...
}

foreach (array as $key => $item) {
...
}
```

**ASP/VBScript**
```vb
For Each item In array
...
Next
```

**ASP.NET/C#**
```csharp
for (type item in array) {
...
}
```

**JSP/Java**
```java
for (Iterator item; item.hasNext(); ) {
...
}
```

## 循环：终止

**PHP**
```php
break;
```

**ASP/VBScript**
```vb
Exit Do
Exit For
```
*（没有退出 While 循环的方法。）*

**ASP.NET/C#**
```csharp
break;
```

**JSP/Java**
```java
break;
```

## 循环：进入下一轮

**PHP**
```php
continue;
```

**ASP/VBScript**
不支持

**ASP.NET/C#**
```csharp
continue;
```

**JSP/Java**
```java
continue;
```

## 函数/方法声明

**PHP**
```php
function name (args) {
  ...
}
```

**ASP/VBScript**
```vb
Function name (args)
  ...
End Function

Sub name (args)
  ...
End Sub
```

**ASP.NET/C#**
```csharp
visibility returnType name (args) {
  ...
}
```

**JSP/Java**
```java
visibility returnType name (args) {
  ...
}
```

## 返回函数值

**PHP**
```php
return value;
```

**ASP/VBScript**
```vb
FunctionName = value
```

**ASP.NET/C#**
```csharp
return value;
```

**JSP/Java**
```java
return value;
```

## 使用命名空间分组类

**PHP**
不支持

**ASP/VBScript**
不支持

**ASP.NET/C#**
```csharp
namespace Name {
...
}
```

**JSP/Java**
```java
package name;
```

## 类可见性关键字

**PHP**
public, private, protected

**ASP/VBScript**
public, private

**ASP.NET/C#**
public, private, protected, internal

**JSP/Java**
public, private, protected, package

## 基类定义

**PHP**
```php
class ClassName {
...
}
```

**ASP/VBScript**
```vb
Class ClassName
...
End Class
```

**ASP.NET/C#**
```csharp
visibility class ClassName {
...
}
```

**JSP/Java**
```java
visibility class ClassName {
...
}
```

## 声明类属性

**PHP**
```php
visibility name;
```

**ASP/VBScript**
```vb
visibility name
```

**ASP.NET/C#**
```csharp
visibility type name;
```

**JSP/Java**
```java
visibility type name;
```

## 调用同一类中的方法

**PHP**
```php
$this->method();
```

**ASP/VBScript**
```vb
Me.method
```

**ASP.NET/C#**
```csharp
this.method();
```

**JSP/Java**
```java
this.method();
```

## 类构造器

**PHP**
```php
function __construct() {
...
}
```

**ASP/VBScript**
```vb
Private Sub Class_Initialize()
...
End Sub
```

**ASP.NET/C#**
```csharp
visibility ClassName() {
...
}
```

**JSP/Java**
```java
public ClassName() {
...
}
```

## 类析构器

**PHP**
```php
function __destruct() {
...
}
```

**ASP/VBScript**
```vb
Private Sub Class_Terminate()
...
End Sub
```

**ASP.NET/C#**
```csharp
visibility ~ClassName() {
...
}
```

**JSP/Java**
```java
protected void finalize() { ... }
```

## 使用静态类方法

**PHP**
```php
ClassName :: StaticMethod();
```

**ASP/VBScript**
不支持

**ASP.NET/C#**
```csharp
ClassName.StaticMethod();
```

**JSP/Java**
```java
ClassName.StaticMethod();
```

## 创建对象

**PHP**
```php
$obj = new ClassName();
```

**ASP/VBScript**
```vb
Set obj = New ClassName
```

**ASP.NET/C#**
```csharp
type obj = new ClassName();
```

**JSP/Java**
```java
type obj = new ClassName();
```

## 类继承

**PHP**
```php
class ClassName extends BaseClass { ... }
```

**ASP/VBScript**
不支持

**ASP.NET/C#**
```csharp
visibility class ClassName : BaseClass {
...
}
```

**JSP/Java**
```java
visibility class ClassName extends BaseClass {
...
}
```

## 调用父类方法

**PHP**
```php
parent::method();
```

**ASP/VBScript**
不支持

**ASP.NET/C#**
```csharp
base.method();
```

**JSP/Java**
```java
super.method();
```

## 声明抽象类

**PHP**
```php
abstract class AbstractClass {
...
}
```

**ASP/VBScript**
不支持

**ASP.NET/C#**
```csharp
abstract class AbstractClass {
...
}
```

**JSP/Java**
```java
visibility abstract class AbstractClass {
...
}
```

## 停止子类化

**PHP**
```php
final class EndClass {
...
}
final visibility function MethodName() {
...
}
```

**ASP/VBScript**
不支持

**ASP.NET/C#**
```csharp
sealed class EndClass {
...
}
sealed visibility type MethodName() {
...
}
```

**JSP/Java**
```java
visibility final class EndClass {
...
}
visibility final type MethodName () {
...
}
```

## 接口声明

**PHP**
```php
interface InterfaceName {
...
}
```

**ASP/VBScript**
不支持

**ASP.NET/C#**
```csharp
visibility interface InterfaceName {
...
}
```

**JSP/Java**
```java
visibility interface InterfaceName {
...
}
```

## 类使用接口

**PHP**
```php
class ClassName implements InterfaceName {
...
}
```

**ASP/VBScript**
不支持

**ASP.NET/C#**
```csharp
visibility class ClassName : InterfaceName {
...
}
```

**JSP/Java**
```java
visibility class ClassName implements InterfaceName {
...
}
```

## 包含外部文件

**PHP**
```php
include('filename');
include_once('filename');
require('filename');
require_once('filename');
```

**ASP/VBScript**
```html
<!-- #include 'filename' -->
```

**ASP.NET/C#**
包含由不同方法处理，包括传统的 ASP 包含方式（如上）。

**JSP/Java**
```jsp
<%@ include file="filename" %>
```

## 异常处理

**PHP**
```php
try { ... } catch (ExceptionType $e) { ... }
```

**ASP/VBScript**
没有特别支持

**ASP.NET/C#**
```csharp
try { ... } catch (ExceptionType e) { ... } finally { ... }
```

**JSP/Java**
```java
try { ... } catch (ExceptionType e) { ... } finally { ... }
```

## 抛出异常

**PHP**
```php
throw new ExceptionType(args);
```

**ASP/VBScript**
```vb
Err.Raise number
```

**ASP.NET/C#**
```csharp
throw new ExceptionType(args);
```

**JSP/Java**
```java
throw new ExceptionType(args);
```

## HTTP POST 值

**PHP**
```php
$_POST (array)
```

**ASP/VBScript**
```vb
Request.Form (collection)
```

**ASP.NET/C#**
```csharp
System.Web.HttpRequest.Form (NameValueCollection)
```

**JSP/Java**
```java
request.getParameter() (method lookup)
```

## HTTP GET 值

**PHP**
```php
$_GET (array)
```

**ASP/VBScript**
```vb
Request.QueryString (collection)
```

**ASP.NET/C#**
```csharp
System.Web.HttpRequest.QueryString (NameValueCollection)
```

**JSP/Java**
```java
request.getParameter() (method lookup)
```

### 服务器变量

**PHP**
```php
$_SERVER (array)
```

**ASP/VBScript**
```vb
Request.ServerVariables (collection)
```

**ASP.NET/C#**
```csharp
System.Web.HttpRequest.ServerVariables (NameValueCollection)
```

**JSP/Java**
```java
request.getVariable() (method lookup; different method per server variable)
```

# 附录 B

## 替代工具

每当热门 PHP 工具的讨论出现时，对话通常围绕文本编辑器或编码 IDE 展开。哪种拥有最好的语言支持、语法高亮、代码解析等等？不幸的是，由于过分关注文本编辑器，一些优秀的非编码工具有时会被忽视。与其重复通常关于一个编辑器优于另一个编辑器的争论，本附录向你展示了一些你可以在开发周期中使用的工具——那些不会立即生成代码的工具，但你可能发现它们在整体开发过程中占据着关键位置。

### MySQL 工具

当你管理 MySQL 数据库时，你通常有两个主要选择作为管理工具：标准的命令行工具集，或图形界面。尽管许多老练的系统管理员持相反态度，使用图形工具完成工作绝对没有任何问题。虽然命令行接口提供了对数据库的无限控制权，但它无法与良好的图形用户界面在帮助促进管理工作流程方面的速度和清晰度相媲美。

如果你在寻找一套好的基于 GUI 的 MySQL 管理工具，你只需要看看 MySQL AB 自己的 MySQL Administrator 和 MySQL Query Browser。

#### MySQL Administrator

MySQL Administrator 是一个功能丰富的 GUI 管理工具，用于维护 MySQL 数据库。主要界面如 figure B.1 所示。




# 附录 B

![](img/ab27c6ac898db1f934d39fa127b14657_373_0.png)

MySQL Administrator 允许你执行以下操作：

- 查看实时服务器信息，包括连接信息和统计、内存统计、MySQL 内部变量及配置设置的值等。
- 查看不同的服务器日志：错误日志、慢查询日志、通用日志（仅限本地主机）。
- 控制 MySQL 进程本身（仅限本地主机）。
- 执行备份和还原操作，甚至安排定期备份。
- 管理服务器的用户访问权限和特权。
- 使用内置的 MySQL 表编辑器创建和编辑完整的数据库，包括表。

MySQL Administrator 适用于 Windows、Linux 和 Mac OS X；MySQL Administrator 可从 MySQL 网站免费下载：http://www.mysql.com/products/administrator/。

#### MySQL 查询浏览器

MySQL Query Browser 是一个图形用户界面（GUI），允许你针对 MySQL 数据库测试和运行各种查询。从某种意义上说，它是命令行客户端的增强版 GUI，你可以参考图 B.2。你还可以像使用标准电子表格程序或桌面数据库应用程序一样使用 MySQL Query Browser——你可以调出数据行，并在查询浏览器中直接编辑它们。除了输入和执行查询以及操作数据之外，它还包含 MySQL Administrator 中的 MySQL 表编辑器，允许你以可视化方式创建和编辑数据库和表。

![](img/ab27c6ac898db1f934d39fa127b14657_374_0.png)

Windows、Linux 和 Mac OS X 版本可在 MySQL 处获取：[http://www.mysql.com/products/query-browser/](http://www.mysql.com/products/query-browser/)。

现在你的应用程序已经启动并运行，服务器也已针对峰值性能进行了调整。但你的数据库查询是否尽可能精简高效？找出答案的唯一方法是使用基准测试工具。

# 附录 B

大多数 MySQL 基准测试工具的运行方式大致相同：你提供一个要运行的查询，该工具将运行该查询大量次数，通常使用并发连接。通过对某些“较重”的查询（通常可在 MySQL 慢查询日志中找到）进行彻底的测试和实验，你可以改善应用程序瓶颈处的执行时间和服务器负载。

#### MySQL Super Smack

MySQL Super Smack 最初由 Sasha Pacheco 开发，是一个独立的压力测试工具，用于 MySQL 和 PostgreSQL。MySQL Super Smack 接受一个或多个包含查询的文件，并以指定的并发连接数，对每个查询对目标数据库进行预定义次数的猛烈攻击。

MySQL Super Smack 可在 http://vegan.net/tony/supersmack/ 获取。

#### MyBench

MyBench 是由 MySQL 专家 Jeremy Zawodny 创建的基于 Perl 的基准测试工具。与 MySQL Super-Smack 一样，它可用于向目标 MySQL 机器发送大量连接和查询，并给出其承受攻击表现的清晰结果。由于它是用 Perl 编写的，你可以轻松地按意愿进行修改和扩展。缺点是大的测试批次可能会占用机器资源，因此最好将此工具运行在目标 MySQL 服务器以外的另一台机器上，以避免结果受到污染。

MyBench 可在 Jeremy Zawodny 的网站获取：http://jeremy.zawodny.com/mysql/mybench/。

### 版本控制

你可能需要考虑在你的开发生命周期或工作流中引入某种形式的版本控制系统，如果你还没有的话。版本控制系统提供了一种在开发过程中存储代码历史快照的方法，并允许多个开发人员将文件检入和检出仓库，从而控制代码库的演变。当今使用最广泛的两款开源版本控制系统是 CVS 和 Subversion。

CVS 和 Subversion 都是支持相同基本功能的版本控制系统：文件版本的历史记录，以及支持多开发人员及检入/检出功能。CVS 自 1989 年以来一直存在，是许多开发人员的长期最爱。Subversion 较新，最初出现于 2000 年末，但由于其功能集超出了在 CVS 中找到的“标准”功能，因此正迅速吸引拥趸。诸如原子提交、“安全”的文件重命名、文件和目录复制以及 WebDAV 支持等功能，是许多开发人员如今选择 Subversion 的一些原因。如果你正在寻找一个功能健壮且客户端和服务器端支持良好的功能集，Subversion 可能是你最好的选择。如果你追求稳定性、记录以及在许多开发工具中内置的支持，CVS 可能更受青睐——尽管最近越来越多的开发包正在获得 Subversion 支持。

## 替代工具

无论你选择哪种，尽早部署某种版本控制都是个好主意——它使多开发人员项目更容易管理，并可以在新代码实际上导致新的严重 bug 或回归问题时提供安全保障。

CVS 可在 https://www.cvshome.org/ 获取。

Subversion 可在 http://subversion.tigris.org/ 获取。

### UML 工具

如果你深入系统架构和设计领域，很有可能你最终会与 UML 打交道。如果你不熟悉 UML，简而言之，它是一种对应用程序或其他系统的结构、行为、架构和流程进行建模和表示的方法。你可以使用 UML 对系统或应用程序的不同方面进行图解，包括类结构、用户交互、对象交互、流程等，类似于你可能使用 Visio、Kivio 或其他相关工具制作的流程图和其他图表。

UML 有九种图表类型，但从开发人员的角度来看，其中最重要的一种是类图。类图有助于你规划你的各种类以及这些类之间的关系。

如果你在 PHP 工作流中使用 UML，你有几个工具可供选择——一些流行的免费工具是 ArgoUML 和 Umbrello。

#### ArgoUML

ArgoUML 是由 Tigris.org 社区创建的基于 Java 的 UML 编辑器。它支持八种主要的 UML 图表类型，可以帮助你快速规划对象、关系和行为。从 PHP 开发人员角度来看，ArgoUML 的主要功能之一是它能够自动从 UML 类图生成有效的 PHP5 类骨架（以及 C#、Java、C++ 和 PHP4），如图 B.3 所示。

你只需在 UML 中创建你的类图，并告诉 ArgoUML 要生成什么代码以及在哪里生成代码，这样你就节省了键入类结构的时间，让你能够直接进入代码的核心：实现。ArgoUML 还提供有关你类结构的机器生成建议，并具备集成的待办事项列表。

ArgoUML 可作为桌面 Java 应用程序获取，既可通过下载获取，也可通过 JavaWebStart 从互联网运行，网址为 http://argouml.tigris.org/。

![](img/ab27c6ac898db1f934d39fa127b14657_377_0.png)

图 B.3

#### Umbrello

Umbrello 是另一种 UML 图解应用程序，类似于 ArgoUML。Umbrello 现在是 KDE 开发人员工具包的一部分，支持许多主要的 UML 图表类型，包括类图、用例图、状态图和序列图。从 1.4 版本开始，Umbrello 可以生成 PHP5 类骨架，以及几种其他编程语言的代码，如图 B.4 所示。

![](img/ab27c6ac898db1f934d39fa127b14657_378_0.png)

图 B.4

Umbrello 可作为 KDE 桌面环境的一部分找到（3.2 或更高版本，Linux），或者你可以直接从 Umbrello 网站（针对 KDE/Linux）下载，网址为 http://uml.sourceforge.net/。

### 索引

## 符号和数字

**{} (花括号)**
- 缩进标准，214–217
- 减少嵌套级别，217–220

**: (冒号)**
- 与类常量 (`:;`)，28–29
- 在 PHP URL 中方案名后 (`://`)，72
- 与 *self* 关键字 (`::`)，7, 27–28

**$ (美元符号)**
- 未用于类常量 (PHP)，29
- `$this` 引用变量 (PHP)，23, 50

**:: (双冒号)。参见** **: (冒号)**

**= (等号) 在相等运算符与赋值运算符中，** 219

**404 处理程序，缓存与，** 226

**" (双引号)**
- 在 `set_exception_handler()` 内的函数名称中，5
- 与字符串的速度，201–205

**‘ (单引号)，与字符串的速度，** 201–205

**/ (斜杠)**
- MySQL 查询的 `/G` 终止符，86
- 在 PHP URL 中方案名后 (`://`)，72

## A

**ab** ApacheBench 程序，208–209

**abort() 方法 (AJAX)，** 277

**abstract 类 (PHP)**
- abstract 关键字，7
- 示例，7–8
- 语言翻译，341–342
- 命名约定，222
- 概述，34–35
- 使用规则，8

**abstract 关键字 (PHP)，** 7

**访问控制 (Apache)。参见** **认证**

**访问控制 (MySQL)**
- `GRANT` 和 `REVOKE` 的替代方案，97–100
- `columns_priv` 表，99, 100
- db 表，98–99, 100
- `GRANT` 命令，94–96
- 重新加载特权表，100
- `REVOKE` 命令，96–97
- 服务器限制，100
- `tables_priv` 表，99, 100
- 用户管理，93–100
- user 表，97–98, 99–100

**访问控制 (PHP)**
- 基本认证，166–171
- 注册表单中的 CAPTCHA 图像，175–177




### 访问控制

- **访问控制（PHP）（续）**
    - 表单身份验证，172–174
    - `HTTP_REFERER` 值，174–175
    - `REMOTE_ADDR` 值，174
    - 服务器变量，174–175
- **访问修饰符（PHP）。另见特定修饰符**
    - Circle 类示例，24–25
    - 语言翻译，337
    - PHP5 增强功能，6
    - 由其指定的可见性，23–24
- `addslashes()` 函数（PHP），113

### AJAX（异步 JavaScript 和 XML）

- 可访问性问题，283–285
- JPCPAINT 库，283
- 描述，273
- DOM 操作，273，281–282
- 更多信息，285
- Google 的 Gmail 应用程序，273
- 处理 `ReadyStateChange` 事件，280
- 处理响应，280–282
- 历史，274–277
- JSPAN 库，283
- 方法，277–278
- 属性，278–279
- JSAJAX 库，282–283
- 支持问题，285
- 与传统 Web 应用的对比，273，274
- 易用性问题，283–285
- 处理浏览器差异，279–280
- XMLHTTP 和 XMLHttpRequest 接口，277–282

### Alcantara, Frank（eAccelerator 维护者），290

### Allman 缩进风格，215–216

### Alpha 透明度，244

### ALTER TABLE 语句（MySQL），87，90–91，92

### 替代 PHP 缓存。另见 APC

### 分析数据库（MySQL），100–102

### 匿名函数（PHP），57–58

### Apache。另见 URL 重写（Apache）

- 使用 MySQL 进行身份验证，129，149–154，166
- 基本身份验证，154，165–166
- 内容压缩，145–149
- 404 处理程序与缓存，226
- `mod_alias`，226
- `mod_auth_mysql`，129，149，150–154
- `mod_dav`，129，158
- `mod_deflate`，129，146–148
- `mod_proxy`，138
- `mod_rewrite`，226
- `mod_spelling`，129，144–145
- `mod_ssl`，129，154–155
- 作为在线文件存储库，158–163
- PDFLib 配置，234
- 性能改进，211–213
- SSL 配置，154–157
- URL 拼写检查，144–145

### ApacheBench 程序（*ab*），208–209

### APC（替代 PHP 缓存）

- 配置，288–290
- 历史，287
- 安装，288
- 与其他缓存引擎的对比，305
- 概述，287
- 移除，290
- 适用场景，305
- 网站，288

### 数组函数（PHP）。另见回调（PHP）

- `array_filter()`，53
- `array_map()`，49，50–51
- `array_walk()`，49，51–52
- 为大多数函数提供回调，48
- `call_user_func_array()`，55–56
- 描述，48
- 序列的内存需求，59–60
- `preg_grep()`，53
- `preg_replace_callback()`，53–55
- 使用回调，48–50
- 种类和数量，59
- `array_filter()` 函数（PHP），53
- `ArrayIterator` 类（PHP），6
- `array_map()` 函数（PHP），49，50–51，55–56

### 数组（PHP）。另见数组函数（PHP）

- 检查大小、性能等，229
- 语言翻译，331
- 命名约定，222
- 临时变量与性能，229–230

### array_walk() 函数（PHP），49，51–52

### ASP。另见语言翻译

### ASP.NET。另见语言翻译

### ASP 风格标签，php.ini 设置，106–107

### 按值赋值与按引用赋值（PHP），29

### 异步 JavaScript 和 XML。另见 AJAX

### atempt_auth() 函数（PHP），169–170

### 身份验证

- 使用 Apache 和 MySQL，149–154
- 使用 Apache 和 SSL，154–157
- Apache 基本身份验证，154，165–166
- Auth_HTT.PEAR 包，187–188
- PHP 控制，166–177
- 使用 WebDAV，159

### Auth_HTT.PEAR 包，187–188

### AUTO_INCREMENT 列（MySQL），89

## B

- 不同运行结果各异，202
- 字符串速度示例，201–205

### Benchmarking 类（PEAR），207–208

### 博客

- Micro CMSs
- 博客流行度，322
- 博客原因，322
- Serendipity，324
- WordPress，323

### 花括号（{}）

- 缩进标准，214–217
- 减少嵌套级别，217–220

### BSD 缩进风格，215–216

### Bzip2 扩展（PHP），271

### 备份（MySQL），103–104

### 基本身份验证（Apache）

- 实现，165
- 局限性，154
- 使用 MySQL，149–154，166
- PHP 控制身份验证，166，171
- 不适用场景，165–166

### 基本身份验证（PHP）

- Apache 控制身份验证，166，171
- 创建身份验证数据库，166–167
- phpauthbasic.php 脚本，167–171
- 测试，171

### 基准测试

- ab ApacheBench 程序，208–209
- 定义，206–207
- MyBench MySQL 工具，350
- PEAR Benchmarking 类，207–208

## C

- C# 另见语言翻译

### 缓存（PHP）

- APC 缓存引擎，287–290
- 选择缓存引擎，305
- 客户端端，227
- CMS 提供的功能，225–226
- eAccelerator 缓存引擎，290–294
- *Expires*：头部，227
- JPCache 缓存引擎，296–300
- memcached 缓存引擎，300–304
- 输出预生成，224–226
- PEAR 包，224–225
- 性能优势，223
- 源码预解析，223–224
- 使用 404 处理程序，226
- 联合使用不同缓存引擎，304–305
- Zend Optimizer 缓存引擎，294–296

### calcArea() 方法，21

### _call() 魔术方法（PHP），8–9，38

### 回调（PHP）

- 用于抽象功能，48
- 用于 **array_filter() 函数**，53
- 用于 **array_map** 函数，空回调，50–51
- 用于 **array_walk() 函数**，52
- 用于 **call_user_func_array() 函数**，55–56

### 回调（PHP）（续）

- create_function() 函数，57–58
- 新的实现可能，59
- preg_replace_callback() 函数，53–55
- 为大多数数组函数提供，48
- 使用 self 关键字，50
- 指定类和对象方法，49–50
- 包含函数名称的字符串，49
- 使用 $this 引用变量，50
- 使用，48–50

### 调用方法和函数

- __construct() 魔术方法，6
- 语言翻译，338–339，341
- 通过魔术方法重载，8–9
- 程序化（MySQL），13
- call_user_func() 函数，56–57
- call_user_func_array() 函数，55–56

### CAPTCHA（完全自动公共图灵测试，用于区分计算机和人类），175–177

### caption() 方法（WebImage 类），251–252

### CASCADE 选项（MySQL），92

### case 语句，语言翻译，332–333

### CERT 网站，182

### check_login() 函数（PHP），170–171

### Circle 类示例

- 抽象 Shape 类，34–35
- __call() 魔术方法，38
- 使用 clone 语句，29–30
- 构造函数，25–26
- 定义，20
- 析构函数，26–27
- __get() 和 __set() 魔术方法，39
- 继承自 Shape 类，31–33
- 用于 memcached 缓存引擎，303–304
- 方法，21
- parent:: 引用，34
- 属性，21
- __sleep() 和 __wakeup() 魔术方法，40–43
- 使用 static 关键字，27–28
- toString() 魔术方法，44
- 在其中指定可见性，24–25

### 类常量（PHP），28–29

### 类（PHP）。另见特定类

- 抽象类，7–8，34–35，222，341–342
- 基础知识，20–23
- 类常量，28–29
- 描述，20
- 使用 final 关键字，6
- 实例化，22–23
- 语言翻译，337–342
- 命名约定，222

### CLI，使用其安装 PEAR，186

### 客户端 URL 库函数（CURL）扩展（PHP），271

### 客户端端缓存，227

### clone 语句（PHP），29–30

### 关闭流（PHP），63

### CMSMatrix 网站，328

### CMSReview 网站，327

### CMSs（内容管理系统）

- 全包 Web CMSs，309–322
- 博客包，322–324
- 提供的缓存，225–226
- 描述，307
- DocuWiki，326
- Drupal，321
- 企业级 CMSs，307–308
- ExponentCMS，309–312
- Mambo，321
- MediaWiki，325–326
- Micro CMSs，322–328
- 开源 Web CMS 包，308
- PHP-Nuke，321
- phpWebsite，315–318
- Postnuke，322
- 资源，327–328
- Serendipity，324
- TikiWiki，318–321
- Web CMSs，描述，308
- wiki 包，324–326
- Wordpress，323
- XOOPS，312–315

### CMSWire 网站，328

### 代码效率。另见性能编码标准（PHP）

- 花括号和缩进，214–217
- 注释，216，217，220
- 通过解析错误强制执行，222–223
- 命名约定，220–222
- 概述，213–214
- PEAR，214
- 减少嵌套级别，217–220

### 冒号（:）

- 用于类常量（::），28–29
- 用于 PHP URL 中的方案名之后（://），72
- 与 self 关键字一起使用（::），7，27–28

### columns_priv 表（MySQL），99，100

### 注释

- Big Flashy Box 风格，216，217
- 编码标准，220
- Javadoc 风格，220
- 语言翻译，329
- 使用 Tab 字符进行缩进，216，217

### 完全自动公共图灵测试，用于区分计算机和人类（CAPTCHA），175–177

### 压缩内容。另见内容压缩（Apache）

### 连接，基准测试速度，201–205

### 条件语句

- 语言翻译，331–336
- 性能，230

### config-help 命令（PEAR 管理器），186

### ConfigManager.php 类

- 代码列表，117
- configfile 属性，118
- configtype 属性，118
- 构造函数方法，118
- 声明，117
- errors 属性，118
- processConfig 方法，118–119

### ConfigProcessor 接口（PHP），119

### config-set 命令（PEAR 管理器），186

### config-show 命令（PEAR 管理器），185–186

### 配置检查器（PHP）

- ConfigManager.php 类，117–119
- ConfigProcessor 接口，119
- reqs.xml 文件，116
- test.php 代码，128
- XMLConfigProcessor.php 类，119–128

### 配置变量（PEAR），185

### 配置 PHP。另见 php.ini 配置文件；运行时配置（PHP）

### const 关键字（PHP），29

### 常量

- 类常量（PHP），28–29
- 语言翻译，330
- 命名约定，222

### __construct() 魔术方法（PHP）

- Circle 类示例，25–26
- ConfigManager.php 类，118
- 描述，37
- 概述，6，25–26
- 与 PHP4 构造函数的对比，25
- XMLConfigProcessor.php 类，122–123

### 构造函数（PHP）

- Circle 类示例，25–26
- __construct() 魔术方法，6，25–26
- 语言翻译，339
- 概述，25–26
- PHP4 构造函数，25

### 内容压缩（Apache）

- 配置指令，147–148
- 描述，145–146
- mod_deflate 的有效性，148
- 对应的 httpd.conf 文件，146–147
- 必要性，145
- 用于 PHP 脚本，148–149
- 使用 mod_deflate，146–148

### 内容管理系统。另见 CMSs

### 转换表

- 从 InnoDB 到 MySQL，93
- 从 MySQL 到 InnoDB，90




### 坐标系

- **坐标系**
    - Ming 扩展（PHP），264
    - PDFLib 扩展（PHP），237
- **Coppermine CMS**，327
- **使用 clone 语句复制对象（PHP），29–30**
- Cowgill, Daniel（APC 创建者），287
- **CPAINT（跨平台异步接口工具包）**，283
- **CREATE DATABASE 语句（MySQL）**，75
- **CREATE TABLE 语句（MySQL）**
    - 用于 Apache 认证示例，149–150
    - 启用全文搜索，86–87
    - 概述，75
    - 用于 PHP 认证示例，166–167
- *create_function()* 函数，57–58
- **交叉连接（MySQL）**，81, 82
- **跨平台异步接口工具包（CPAINT）**，283
- **跨站点脚本（XSS）**，180–181
- **CSS 样式表**
    - AJAX 使用，273
    - PEAR 包，192–193
- **CURL（客户端 URL 库函数）扩展（PHP）**，271
- **CVE 网站**，182
- **CVS 版本控制系统**，350–351
- **D**
- **数据对象，用于集成的 PDO PEAR 包**，196–197
- **数据库分析（MySQL）**，100–102
- **数据库维护（MySQL）**，103–104
- **与数据库相关的包（PEAR）**
    - Auth_HTTP，187–188
    - DB，190–192
    - HTML_Table，194–195
    - PEAR::Auth，187, 188
    - PEAR::DB，187
    - 相关网站，191
- **数据库（MySQL）**。参见 *MySQL*
- **Date PEAR 包**，189–190
- **DB PEAR 包**，190–192
- **db 表（MySQL）**，98–99, 100
- **调试脚本。用于调试的 Xdebug PECL 包**，197
- *DeflateCompressionLevel 指令（Apache 的 mod_deflate）*，147
- *DeflateFilterNote 指令（Apache 的 mod_deflate）*，148
- *DeflateWindowSize 指令（Apache 的 mod_deflate）*，148
- **DELETE 语句（MySQL）**，77, 92
- **删除数据库信息（MySQL）**，77, 92
- *__destruct()* *魔术方法（PHP）, 6, 26–27, 37*
- **析构函数（PHP）**
    - Circle 类示例，26–27
    - 使用 *__destruct()* 魔术方法，6, 26–27
    - 语言翻译，339–340
    - 概述，26–27
- **指令（PHP）**。参见 *php.ini 配置文件*
- **目录**
    - 自动重定向 URL 到，132
    - 为 SSL 网站创建，157
    - 使用 *glob()* 进行模式匹配读取，60–61
    - 用于 WebDAV 文件存储库，158
- *DirectoryIterator 类（PHP）*，5
- **磁盘访问，性能相关**，211
- *display()* 方法（*WebImage 类*），244
- **DocuWiki 微型 CMS**，326
- **美元符号（$）**
    - 不用于类常量（PHP），29
    - *$this 引用变量（PHP）*，23, 50
- **DOM（文档对象模型）**
    - AJAX 操作，273, 281–282
    - DOM 扩展（PHP），16, 271
- **双冒号（::）。参见 冒号（:）**
- do... *while 循环，语言翻译*，334
- *drawHR()* 函数（PDFLib），236
- **Drupal CMS**，321

- **DSO（动态共享对象）**
    - 安装 APC 作为 DSO，287, 288
    - 安装 eAccelerator 作为 DSO，291
    - 安装 memcached 作为 DSO，301
    - PDFLib 配置，234

- **E**
- **eAccelerator 缓存引擎**
    - 配置，291–294
    - 安装，291
    - 与其他缓存引擎的比较，305
    - 概述，290–291
    - 移除，294
    - 网站，291

- **echo 语句（PHP）**
    - 与 print 语句对比，228–229
    - 与 __toString() 魔术方法结合使用，44

- **emailException 类，3–4**
- **企业级 CMS，307–308。另见 CMS（内容管理系统）**
- **等号（=）在相等运算符与赋值运算符中的区别，219**
- **错误消息，php.ini 设置，106**
- **Exception 类（PHP），2–4**

- **异常（PHP）**
    - 描述，1
    - 使用 Exception 类，2–4
    - 语言翻译，344–345
    - PHP5 的变更与增强，1–5
    - 与 set_error_handler() 函数对比，1–2
    - 使用 try/catch/throw 块，2, 234, 344–345

- **Expires: 头部，缓存相关，227**

- **ExponentCMS**
    - 附加模块，310
    - 自定义默认设置，310–311
    - 默认功能，309
    - “非活动”功能，309
    - 安装，309–310
    - 优缺点，311
    - 网站，309, 310

- **extends 关键字（PHP）**
    - emailException 示例，3–4
    - 继承相关，31–33
    - 接口相关，36–37
    - 概述，3, 31–33

- **可扩展面向对象的门户系统。参见 XOOPS**
- **extension_loaded() 函数（PHP）**
    - 概述，111
    - 在 XMLConfigProcessor.php 类中，124, 125
- **外部文件，用于包含的语言翻译，343–344**

- **F**
- **胖客户端 Web 应用程序。参见 AJAX（异步 JavaScript 和 XML）**
- **文件访问记录器示例**
    - 代码清单，64–66
    - 注册流包装器，66
    - stream_close() 函数，67
    - stream_open() 函数，67
    - stream_read() 函数，67
    - stream_write() 函数，67
    - 使用记录的流，66–67

- **使用 Apache 的文件存储库。参见 WebDAV（基于 Web 的分布式创作与版本控制）**
- **FileInfo PECL 包，196**
- **final 关键字（PHP），6, 33**
- **Flash 文件（Shockwave）。参见 Ming 扩展（PHP）**
- **FLUSH PRIVILEGES 命令（MySQL），100**
- **for 循环**
    - 无需此循环的数组函数，48
    - 语言翻译，335
- **foreach 循环**
    - 无需此循环的数组函数，48
    - 使用 array_walk() 函数避免，49, 51–52
    - 语言翻译，335

- **外键约束（MySQL）**
    - 优点，89
    - 使用 *ALTER TABLE* 语句创建，90–91, 92
    - 命名，90
    - *NULL* 值相关，89
    - 指定行为的选项，92
    - 与 *UPDATE* 语句相关，91–93

- **表单（HTML），相关 PEAR 包，193–194**
- **表单（PHP）**
    - 用于登录认证，172–174
    - *php.ini* 设置，105, 107
- **404 处理程序，缓存相关，226**
- **帧（Ming），264**
- **FTP，使用其安装 PEAR，186**
- **全文搜索（MySQL）**
    - 修改现有表以支持，87
    - 创建启用全文搜索的新表，86–87
    - 局限性，88
    - 指定最小全文单词长度，88
    - InnoDB 不支持，89
    - 使用 *SELECT* 语句，87–88
- **函数（MySQL），过程化调用，13**
- **函数（PHP）。另见 数组函数**
- **（PHP）：特定函数**
    - 匿名函数，57–58
    - *ArrayIterator* 类，6
    - 回调，49
    - 检查扩展及其属性，111–112
    - 检查已安装版本，108
    - 检查魔术引号设置，113
    - *Exception* 类，3
    - *Iterator* 类，5
    - 语言翻译，336–337
    - 命名约定，220, 221–222
    - PHP5 新增，91–92
    - 在运行时获取配置设置，109–110
    - 种类繁多，47
- **FusionNews CMS，327**

## G

- *G* **MySQL 查询终止符，86**
- **GD 库扩展（PHP）**
    - 添加字幕，250–254
    - 添加标志，254–257
    - 透明度与 alpha，244
    - 创建图像基础，241–245
    - 描述，241
    - *ImageCaption* 类，250–254
    - *ImageLogo* 类，254–257
    - *ImageResize* 类，245–248
    - *ImageRotate* 类，249–250
    - 透明度与 index，244
    - 手册，263
    - 调整图像大小，245–248
    - 旋转图像，248–250
    - 测试，257–261
- *WebImage* **用于其的基类，241–245,** 246–247, 249, 251–252
- *WebImage* 类，255–256
- ***__get()** *魔术* 方法（PHP）**
    - *Circle* 类示例，39
    - 示例，8
    - 概述，38–39
- ***get_cfg_var()** 函数（PHP），109*
- ***get_defined_functions()** 函数（PHP），57*
- ***get_extension_funcs()** 函数（PHP），112*
- ***get_loaded_extensions()** 函数（PHP），111–112, 116*
- ***get_magic_quotes_gpc()** 函数（PHP），113*
- ***get_magic_quotes_runtime()** 函数（PHP），113*
- ***getMetaTags()** 函数（PHP），2, 3*
- ***getResponseHeader()** 方法（AJAX），277*
- **GIS 摄影数据库查询示例**
    - 解决方案方法，67–68
    - 代码清单，68–70
    - nzmg 协议，70
    - 图像 PNG 文件，70, 71–72




### GD 库的 ImageLogo 类
- stream_open() 函数，第 70~71 页
- stream_read() 函数，第 71 页
- stream_tell() 函数，第 71 页
- 数据库相关网站，第 67 页
- glob() 函数 (PHP)，第 60~61 页
- GMail 应用程序 (Google)，第 273 页
- GNU 缩进风格，第 215 页
- GRANT 命令 (MySQL)
  - 用于 Apache 访问凭据，第 149 页
  - 创建列级权限，第 95 页
  - 为特定表创建权限，第 95 页
  - 用于极度受限的访问，第 96 页
  - 授予所有权限，第 96 页
  - 授予有限的整表权限，第 96 页
  - IDENTIFIED BY 子句，第 96 页
  - ON 子句，第 95 页
  - 用于 PHP 身份验证示例，第 166 页
  - 权限，第 94~95 页
  - 语法，第 94 页
  - TO 子句，第 95 页

### httpd.conf 文件
- 启用 SSL 功能，第 157 页
- HostnameLookups 选项，第 212 页
- KeepAlive 选项，第 212 页
- KeepAliveTimeout 选项，第 212 页
- MaxClients 选项，第 211 页
- MaxKeepAliveRequests 选项，第 212 页
- MaxRequestsPerChild 选项，第 211 页
- MinSpareServers 选项，第 212 页
- 用于 mod_auth_mysql，第 151~152 页
- 用于 mod_dav，第 158 页
- 用于 mod_deflate (Apache)，第 146~147 页
- 用于 mod_ssl，第 155 页
- 性能相关，第 211~212 页
- StartServers 选项，第 212 页
- 用于 WebDAV 身份验证，第 159 页

### H
- 硬盘，性能相关，第 211 页
- 用于性能的硬件改进，第 210~211 页
- 使用隐藏框架技术避免页面刷新，第 275~276 页
- 使用隐藏 IFRAME 技术避免页面刷新，第 276~277 页
- .htaccess 文件
  - 用于 mod_auth_mysql，第 151~152 页
  - 性能相关，第 213 页
  - 用于关闭 register_globals 指令，第 179 页
  - 用于 WebDAV 身份验证，第 159 页
- HTML_CSS PEAR 包，第 192~193 页
- HTML_Page PEAR 包，第 192~193 页
- HTML_QuickForm PEAR 包，第 193~194 页
- HTML_Table PEAR 包，第 194~195 页
- HTTP GET 值，第 345 页
- HTTP POST 值，第 345 页
- IFRAME 元素，隐藏，第 276~277 页
- 使用图像源技巧避免页面刷新，第 275 页
- imagealphablending() 函数
  - (ImageResize 类)，第 248 页
- GD 库的 ImageCaption 类
  - 代码列表，第 250~251 页
- imageline() 函数，第 253~254 页
- imageftext() 函数，第 253 页
- process() 方法，第 252~253 页
- imagecopy() 函数 (ImageLogo 类)，第 257 页
- imagecopymerge() 函数 (GD 库)，第 257 页
- imagecopyresampled() 函数
  - (ImageResize 类)，第 248 页
- imagecopyresized() 函数 (ImageResize 类)，第 248 页
- imageline() 函数 (ImageCaption 类)，第 253~254 页
- GD 库的 ImageLogo 类
  - 代码列表，第 254~255 页
  - imagecopy() 函数，第 257 页
  - process() 方法，第 256~257 页

### GD 库的 ImageResize 类
- 代码列表，第 245–246 页
- imagealphablending() 函数，第 248 页
- imagecopyresampled() 函数，第 248 页
- imagecopyresized() 函数，第 248 页
- imagesavealpha() 函数，第 248 页
- process() 方法，第 247–248 页

### GD 库的 ImageRotate 类
- 第 249–250 页

### imagesavealpha() 函数
- ImageResize 类，第 248 页
- WebImage 类，第 244 页

### imagerftext() 函数
- (ImageCaption 类)，第 253 页

### implements 关键字
- (PHP)，第 36, 37 页

### 编码缩进标准
- 第 214–217 页

### 索引透明性
- 第 244 页

### info 命令
- (PEAR 管理器)，第 185 页

### 继承
- (PHP)
  - 抽象类，第 7–8, 34–35 页
  - 描述，第 31 页
  - extends 关键字，第 31–33 页
  - final 关键字，第 6, 33 页
  - 语言转换，第 340–341 页
  - parent:: 引用，第 33–34 页
  - 在子类中重新定义属性和方法，第 32–33 页
  - static 关键字，第 7 页

### ini_get() 函数
- (PHP)，第 109 页

### ini_get_all() 函数
- (PHP)
  - 访问指令的值，第 115 页
  - 概述，第 109, 110 页
  - 在 XMLConfigProcessor.php 类中，第 126, 127 页

### ini_set() 函数
- (PHP)，第 114–115, 127–128 页

### 初始化属性
- (PHP)，第 21 页

### 内连接
- (MySQL)
  - 表别名，第 78–79 页
  - 按评估顺序链接，第 79 页
  - 用于逗号分隔的表列表，第 79–81 页
  - 定义，第 78 页
  - 局限性，第 81 页
  - 与外连接结合，第 82 页
  - 语法，第 78 页
  - 表前缀，第 78–79 页
  - 使用 statement，第 79 页
  - where 子句，第 79, 80, 81 页

### Innobase Oy 公司
- 第 88 页

### InnoDB 表
- (MySQL)
  - 优点，第 88–89 页
  - 将 MyISAM 表转换为，第 90 页
  - 转换为 MyISAM 表，第 93 页
  - 从头创建表，第 89 页
  - InnoDB 存储引擎的发展，第 88 页
  - 缺点，第 89 页
  - 外键约束，第 88–89, 90–93 页

### insert 语句
- (MySQL)，第 75–76 页

### 安装
- APC 缓存引擎，第 288 页
- DocuWiki 微型 CMS，第 326 页
- eAccelerator 缓存引擎，第 291 页
- ExponentCMS，第 309–310 页
- JPacache 缓存引擎，第 296–297 页
- MediaWiki 微型 CMS，第 325 页
- memcached 缓存引擎，第 300–301 页
- Ming 扩展 (PHP)，第 263 页
- mod_auth_msql (Apache)，第 150–151 页
- PEAR 包，第 186 页
- phpWebsite CMS，第 315–317 页
- Serenidipity 博客微型 CMS，第 324 页
- TikiWiki CMS，第 318–320 页
- WordPress 博客微型 CMS，第 323 页
- Xoops CMS，第 312–313 页
- Zend Optimizer 缓存引擎，第 294–295 页

### 实例化
- 类，第 22–23 页
- SWFMovie 对象 (Ming)，第 263 页

### interface 关键字
- (PHP)，第 36 页

### 接口实现
- (PHP)
  - 描述，第 35 页
  - 使用 extends 关键字，第 36–37 页
  - 实现，第 36, 37 页
  - 语言转换，第 342–343 页
  - 一个类实现多个接口，第 37 页
  - 概述，第 35–37 页
  - PHP5 变更，第 5 页
  - 用途，第 35 页

### Internet 数字分配机构
- 第 72 页

### 互联网资源
- AJAX 信息，第 285 页
- apache mod_ssl 信息，第 157 页
- APC 缓存引擎，第 288 页
- Auth_HTTP PEAR 包信息，第 188 页
- CMS 资源，第 327–328 页
- CPAINT，第 283 页
- CVS 版本控制系统，第 351 页
- DocuWiki 微型 CMS，第 326 页
- Drupal CMS，第 321 页
- eAccelerator 缓存引擎，第 291 页
- ExponentCMS，第 309, 310 页
- FileInfo PECL 包，第 196 页
- PHP 手册中的 GD 部分，第 263 页
- Google 的 Gmail 应用程序，第 273 页
- Internet 数字分配机构，第 72 页
- JavaWebStart 网站，第 351 页
- JPCache 缓存引擎，第 296, 300 页
- JSPAN，第 283 页
- 新西兰土地信息网站，第 67 页
- Mambo CMS，第 321 页
- MediaWiki 微型 CMS，第 325 页
- memcached 缓存引擎，第 300, 301 页
- 微型 CMSs，第 323, 324, 325, 326, 327 页
- Ming 信息，第 263 页
- MyBench 工具，第 350 页
- MySQL Administrator 工具，第 348 页
- MySQL Query Browser 工具，第 349 页
- MySQL Super Smack 工具，第 350 页
- PDF 开源库，第 233 页
- PDFLib 扩展 (PHP)，第 233, 234 页
- PDFLib Lite 扩展 (PHP)，第 234 页
- PDO PECL 包，第 196, 197 页
- PEAR 配置变量，第 185 页
- PEAR 数据库包，第 191 页
- PEAR 管理器命令，第 184 页
- PEAR 包，第 195 页
- PEAR::DB 包，第 187 页
- PEPr 网站，第 184 页
- PHP Wiki 网站，第 196 页
- PHP-Nuke CMS，第 321 页
- phpWebsite CMS，第 315 页
- Postnuke CMS，第 322 页
- S AJAX 信息，第 282 页
- 安全相关网站，第 182 页
- Serendipity 博客微型 CMS，第 324 页
- SourceForge 网站，第 263, 353 页
- SQLite 信息，第 17 页
- Subversion 版本控制系统，第 351 页
- Tidy 库，第 17 页
- TikiWiki CMS，第 318 页
- Umbrello UML 工具，第 353 页
- WordPress 博客微型 CMS，第 323 页
- WROX 网站，第 76 页
- Xdebug PECL 包，第 197 页
- XOOPS，第 312 页
- Zend Optimizer，第 295 页

### 解释
- 基准测试速度，第 201–205 页

### Iterator 类
- (PHP)，第 5 页

### Iterators
- (PHP)，第 5–6 页

## J
- Java. 参见 语言转换
- Javadoc 风格注释，第 220 页
- JavaScript. 另见 AJAX (异步 JavaScript 和 XML)
  - 隐藏框架技术，第 275–276 页
  - 图像源技巧，第 275 页
- JavaWebStart 网站，第 351 页
- JPCache 缓存引擎
  - 配置，第 297–299 页
  - 安装，第 296–297 页
  - 与其他缓存引擎配合，第 305 页
  - 概述，第 296 页
  - 移除，第 300 页
  - 适用情况，第 305 页
  - 网站，第 296, 300 页
- JSPAN AJAX 库，第 283 页
- JSP. 参见 语言转换

## K & R (Kernighan 和 Ritchie) 缩进风格
- 第 215, 216, 217 页

## K
- K & R (Kernighan 和 Ritchie) 缩进风格，第 215, 216, 217 页

## L
- 新西兰土地信息网站，第 67 页

### 语言转换
- 抽象类声明，第 341–342 页
- 数组创建，第 331 页
- 数组元素引用，第 331 页
- 基类定义，第 338 页
- 调用同一类中的方法，第 338–339 页
- 调用父类方法，第 341 页
- 类构造函数，第 339 页
- 类析构函数，第 339–340 页
- 类继承，第 340–341 页
- 类属性声明，第 338 页
- 使用接口的类，第 343 页
- 类可见性关键字，第 337 页
- 注释，第 329 页
- 条件评估，第 331–332 页
- 常量声明，第 330 页
- 异常处理，第 344 页
- 函数/方法声明，第 336 页
- 使用命名空间对类进行分组，第 337 页
- HTTP GET 值，第 345 页
- HTTP POST 值，第 345 页
- 包含外部文件，第 343–344 页
- 接口声明，第 342–343 页
- 循环，进入下一轮，第 336 页
- 循环，do...while，第 334 页
- 循环，for，第 334 页
- 循环，foreach，第 335 页
- 循环，终止，第 335 页
- 循环，while，第 333 页
- 多重选择，第 332–333 页
- 对象创建，第 340 页
- 返回函数值，第 336–337 页
- 服务器变量，第 345–346 页
- 静态类方法使用，第 340 页
- 停止子类化，第 342 页
- 抛出异常，第 344–345 页
- 变量声明，第 330 页
- 变量类型化，第 330 页

### 左外连接
- (MySQL)，第 81, 84 页

### load() 函数
- (WebImage 类)，第 243–244 页

### 日志文件
- 用于监控日志的 emailException 类，第 3–4 页
- 文件访问记录器示例，第 63–67 页
- 用于 URL 重写的日志 (Apache)，第 143–144 页

### logo() 方法
- (WebImage 类)，第 255–256 页

### 循环
- 不需要循环的数组函数，第 48 页
- 用于避免循环的 array_walk() 函数，第 49, 51–52 页
- for 循环，第 48, 335 页
- foreach 循环，第 48, 49, 51–52, 335 页
- 语言转换，第 333–336 页

## M
- Mac OS，WebDAV 设置，第 163 页
- Macromedia Flash 与 Ming 对比，第 263 页

### 魔术方法 (PHP)
- 用于访问未显式定义的方法和属性，第 37 页
- __call()，第 8–9, 38 页
- __construct()，第 6, 25–26, 37 页
- __destruct()，第 6, 26–27, 37 页
- __get()，第 8, 38–39 页
- 用于重载，第 8–9 页
- 概述，第 37 页
- __set()，第 8, 38–39 页
- __sleep()，第 39, 40–43 页
- __toString()，第 43–44 页
- __wakeup()，第 40–43 页

### 魔术引号 (PHP)
- 检查 php.ini 设置，第 113 页
- 禁用，第 106, 113 页
- 概述，第 112–113 页
- 用于 php.ini 设置，第 106, 113 页

第 366 页



### 索引

-   维护数据库 (MySQL)，103–104
-   Mambo CMS，321
-   MediaWiki 微型 CMS，325–326
-   memcached 缓存引擎
    -   守护进程，300
    -   安装，300–301
    -   Memcache 对象方法，301–303
    -   与其他缓存引擎配合使用，305
    -   概述，300
    -   用于该引擎的 PECL 模块，301
    -   移除，304
    -   使用，301–304
    -   网站资源，300, 301
-   **内存 (RAM)**
    -   与性能相关，200, 210–211
    -   与一系列数组函数相关，59–60
-   **方法 (MySQL)**
    -   过程式调用，13
    -   mysqli 类，13–14
    -   mysqli_result 类，16
    -   mysqli_stmt 类，15
-   **AJAX 接口的方法，277–278**
-   **方法 (PHP)。另见 (PHP) 函数；(PHP) 魔术方法；具体方法和函数**
    -   抽象方法，8
    -   定义，21
    -   描述，20, 21
    -   配合 final 关键字使用，6
    -   语言翻译，336, 338–339, 340, 341
    -   命名约定，221–222
    -   在子类中重新定义，32–33
    -   配合 static 关键字使用，7, 27–28
    -   流包装器方法，62–63
-   **微型 CMS**
    -   博客包，322–324
    -   DocuWiki，326
    -   MediaWiki，325–326
    -   其他软件包，327
    -   Serendipity，324
    -   Wiki 软件包，324–326
    -   WordPress，323
-   **Ming 扩展 (PHP)**
    -   与 Macromedia Flash 的比较，263
    -   对应的 Content-Type 头部，268
    -   坐标系，264
    -   创建 Flash 展示，265–269
    -   帧，264
    -   安装，263
    -   对象，263, 264–265
    -   直接输出到浏览器，268–269
    -   概述，263–264
    -   简单示例，263–264
    -   幻灯片演示示例，266–269
    -   更多信息的网站，263
-   **mod_alias (Apache)，226**
-   **mod_auth_mysql (Apache)**
    -   优势，166
    -   AuthMySQLAuthitative 指令，154
    -   AuthMySQLDB 指令，151, 152
    -   AuthMySQLDBEnable 指令，151, 152
    -   AuthMySQLGroupCondition 指令，154
    -   AuthMySQLGroupField 指令，154
    -   AuthMySQLGroupTable 指令，154
    -   AuthMySQLHost 指令，152
    -   AuthMySQLNameField 指令，153
    -   AuthMySQLPasswordField 指令，151, 152
    -   AuthMySQLPasswordField 指令，153
    -   AuthMySQLPort 指令，152
    -   AuthMySQLPwEncryption 指令，151, 153
    -   AuthMySQLSaltField 指令，153
    -   AuthMySQLSocket 指令，152
    -   AuthMySQLUser 指令，151, 152
    -   AuthMySQLUserCondition 指令，153
    -   AuthMySQLUserTable 指令，153
    -   AuthName 指令，151
    -   AuthType 指令，151
    -   对应的数据库设置，149–150
    -   描述，129
    -   对应的 .htaccess 文件，151–152
    -   对应的 http.conf 文件，151–152
    -   安装，150–151
    -   安全所需的最少指令，151
-   **mod_dav (Apache)，129, 158**

-   **mod_deflate (Apache)**
    -   构建和启用，146
    -   使用其进行内容压缩，146–148
    -   DeflateCompressionLevel 指令，147
    -   DeflateFilterNote 指令，148
    -   DeflateWindowSize 指令，148
    -   描述，129
    -   有效性，148
    -   对应的 httpd.conf 文件，146–147
-   **mod_rewrite (Apache)。另见 URL 重写 (Apache)**
    -   功能，129
    -   将站点文档树与服务器文件系统解耦，226
    -   描述，129
    -   启用，130–131, 133
    -   RewriteBase 指令，143
    -   RewriteCond 指令，139–143
    -   RewriteLog 指令，143–144
    -   RewriteLogLevel 指令，144
    -   RewriteRule 指令，131–138
-   **mod_speling (Apache)，129, 144–145**
-   **mod_ssl (Apache)，129, 154–155。另见 使用 Apache 的 SSL (安全套接字层)**
-   Moodle CMS，327
-   乘法运算符，与性能相关，200–201
-   MyBench MySQL 工具，350
-   my.cnf 配置文件 (MySQL)，88, 100
-   MyISAM 表 (MySQL)
    -   从 InnoDB 转换，93
    -   转换为 InnoDB，90
    -   作为默认存储引擎，88
-   MySQL。另见 SELECT 语句 (MySQL)
    -   访问控制，93–100
    -   表的别名，78–79
    -   ALTER TABLE 语句，87, 90–91, 92
    -   替代工具，347–350
    -   分析数据库，100–102
    -   配合 Apache 认证使用，129, 149–154, 166
    -   基础知识，73–77
    -   columns_priv 表，99, 100
    -   创建备份，103
    -   创建数据库，74–75
    -   创建表，75, 86–87
    -   交叉连接，81
    -   db 表，98–99, 100
    -   删除数据库信息，77, 92
    -   示例数据库表，73–74
    -   外键约束，88–89, 90–93
    -   全文搜索，86–88
    -   查询结束符 /G，86
    -   GRANT 命令，94–96
    -   内连接，78–81, 92
    -   InnoDB 表，88–93
    -   在表中插入数据，75–76
    -   维护数据库，103–104
    -   监视器，74
    -   MyBench 工具，350
    -   my.cnf 配置文件，88
    -   MyISAM 表，88, 90, 93
    -   MySQL Administrator 工具，347–348
    -   MySQL Query Browser 工具，349–350
    -   MySQL Super Smack 工具，350
    -   外连接，81–82
    -   查询多个表，77–86
    -   重新加载权限表，100
    -   从备份恢复，103–104
    -   检索数据库信息，76–77
    -   REVOKE 命令，96–97
    -   服务器限制，100
    -   设置当前活动数据库，75
    -   SHOW COLUMNS 命令，101
    -   SHOW CREATE TABLE 命令，101–102
    -   SHOW DATABASES 命令，102
    -   SHOW GRANTS 命令，102
    -   启动命令行客户端，74
    -   tables_priv 表，99, 100
    -   并集，82–86
    -   更新数据库信息，77, 91–92
    -   USE 语句，75
    -   用户管理，93–100
    -   user 表，97–98, 99–100
    -   UPDATE 语句，79
    -   WHERE 子句，79, 80, 81
-   mysqli 类，13–15
-   MySQLi (增强型 MySQL)，12–16
-   mysqli_connect() 函数，与性能相关，231
-   mysqli_result 类，16
-   mysqli_stmt 类，15

## N

-   命名空间
    -   通过 create_function() 函数避免冲突，57–58
    -   语言翻译，337
-   命名约定，220–222
    -   嵌套，减少层级，217–220
    -   网络连接，与性能相关，210
-   NEW 关键字 (PHP)，22–23
-   NO ACTION 选项 (MySQL)，92
-   NULL 值
    -   (PHP) array_map() 函数的回调，50–51
    -   (MySQL) InnoDB 外键约束与，89
    -   (MySQL) 并集中缺失列的情况，84–86
-   create_function() 函数名称中的 NULS，58

## O

-   面向对象编程。另见 OOP；PHP5 OOP
-   对象 (PHP)
    -   通过实例化类创建，20, 22–23
    -   描述，20
    -   语言翻译，340
    -   与 OOP 相比的现实世界例子，20
    -   对应的 $this 引用变量，23
-   ob_start('ob_gzhandler') 函数，231
-   onreadystatechange 属性 (AJAX)，278, 279
-   OOP (面向对象编程)。另见 PHP5 OOP
    -   PHP5 中的更改，1–9
    -   与过程式编程的比较，19–20
-   open() 方法 (AJAX)，277
-   开源运动，183
-   打开
    -   MySQL 命令行客户端，74
    -   流 (PHP)，62, 63
-   OpenSourceCMS 网站，327
-   osCommerce CMS，327
-   外连接 (MySQL)
    -   通用形式，81
    -   与内连接组合使用，82
    -   左连接与右连接，81
    -   与并集组合使用，84
-   输出缓冲，与性能相关，227–228, 231
-   与 (PHP) 魔术方法相比的 overload() 函数，8
-   overrideMimeType() 方法 (AJAX)，278

## P

-   Pachev, Sasha (MySQL Super Smack 的创造者)，350
-   parent 关键字 (PHP)，33–34
-   变量传递，PHP5 的更改，1
-   PDF (便携式文档格式)
    -   开源库，233
    -   用于该格式的 PDFLib 扩展，233–241
    -   用于该格式的 PDFlib 函数，233
    -   PDF 简历生成应用程序，238–241
    -   pdf_close() 函数 (PDFLib)，234
    -   pdf_closepath() 函数 (PDFLib)，236
    -   pdf_fill() 函数 (PDFLib)，236
    -   pdf_findfont() 函数 (PDFLib)，236
    -   pdf_get_buffer() 函数 (PDFLib)，237
    -   pdf_get_value() 函数 (PDFLib)，236, 237
-   PDFLib 扩展 (PHP)
    -   完成 PDF 文件，237
    -   配置，234
    -   坐标系，237
    -   drawHR() 函数，236
    -   字体函数，236–237
    -   入门指南，234
    -   辅助函数，235–237
    -   路径函数，236




### PDFLib 扩展 (PHP) (续)

- PDF 简历生成器示例，238–241
- `pdf_close()` 函数，234
- `pdf_get_value()` 函数，236
- 与 PDFlib 函数对比，233
- PDFlib-manual.pdf 手册，234
- `pdf_new()` 函数，234
- `pdf_set_info()` 函数，236
- `pdf_show_xy()` 函数，237
- 性能优势，233
- 必需元素，235
- 指定文档信息，235
- 网站，233, 234

### PDFlib 函数 (PHP)

- 辅助函数，235–237
- 迁移至 PCL，233
- 与 PDFLib 扩展对比，233

### PDFLib Lite 扩展 (PHP)

- 234
- PDFLib-manual.pdf，234
- `pdf_lineto()` 函数 (PDFLib)，236
- `pdf_moveto()` 函数 (PDFLib)，236
- `pdf_new()` 函数 (PDFLib)，234
- `pdf_setopt()` 函数 (PDFLib)，236
- `pdf_set_info()` 函数 (PDFLib)，235
- `pdf_show_xy()` 函数 (PDFLib)，237

### PDO PECL 包

- 196–197

### PEAR (PHP 扩展和仓库)

- 提供的 APC 缓存引擎，287
- Auth_HTTP 包，187–188
- Benchmarking 类，207–208
- 检查预装包，186
- 编码标准，214
- 配置变量，185
- Date 包，189–190
- DB 包，190–192
- 描述，183–184
- HTML_CSS 包，192–193
- HTML_Page 包，192–193
- HTML_QuickForm 包，193–194
- HTML_Table 包，194–195
- 安装包，186
- 推荐的 Javadoc 风格注释，220
- 指定的 K&R 缩进风格，216
- 通过补丁保持更新，182
- phpWebsite CMS 库，316
- 可用包，187, 195–196
- PEAR 管理器，184–186
- PEAR::Auth，187, 188
- PEAR::Cache 和 PEAR::Cache_Lite 包，224–225
- PEAR::DB 包，187
- PEP (PEAR 提案系统)，184
- 使用已安装的包，187

### PEAR 提案系统 (PEP)

- 184

### PEAR::Auth 包

- 187, 188

### PEAR::Cache 和 PEAR::Cache_Lite 包

- 224–225

### PEAR::DB 包

- 187

### PECL (PHP 扩展社区库)

- 提供的 APC 缓存引擎，287, 288
- 描述，184, 196
- Fileinfo 包，196
- 通过补丁保持更新，182
- memcached 缓存引擎模块，301
- 其中的 PDFLib 函数，233
- PDO 包，196–197
- Xdebug 包，197

### PEP (PEAR 提案系统)

- 184

### 性能

- ab ApacheBench 程序，208–209
- Apache Web 服务器改进，211–213
- 基准测试定义，206–207
- 基准测试，字符串速度示例，201–205
- 缓存与性能，223–227
- 检查数组大小与性能，229
- 条件语句与性能，230
- `echo` 与 `print` 对比及性能，228–229
- 硬件改进，210–211
- 内存与性能，200
- 乘法运算符与性能，200–201
- NT4/Access 报表生成器轶事，200
- `ob_start('ob_gzhandler')` 与性能，231
- 输出缓冲与性能，227–228, 231
- 概述，231-232
- PDFlib 函数与 PDFLib 扩展对比及性能，233
- PEAR Benchmarking 类，207-208
- 持久数据库连接与性能，231
- PHP 编码标准，213-223
- 为性能规划程序，199-201
- 性能分析定义，207
- 正则表达式语法与性能，230
- 释放资源与性能，231
- 临时变量与性能，229-230
- 字符串函数与性能，230
- 字符串与性能，201-205
- `top` 进程监控工具，208-210
- 性能调优的反直觉结果，206
- `unset()` 函数与性能，230

### 持久数据库连接、性能

- 231

### PHP

另见：语言翻译；PHP5 OOP 变更与增强；PHP5 OOP

- 数组函数与回调，48-60
- 身份验证，166-177
- 自动化版本和功能检查，116-128
- 动态更改配置，113-115
- 检查扩展及其属性，111-112
- 编码标准，213-223
- `glob()` 函数，60-61
- 列出已安装版本，108
- 获取当前运行时设置，108-113
- 脚本输出压缩，148-149
- 运行时检索配置设置，109-110
- 流，61-72
- 其中的函数种类和数量，47

### PHP 配置

另见：php.ini 配置文件；运行时配置 (PHP)

### PHP 扩展和仓库

另见：PEAR

### PHP 扩展社区库

另见：PECL

### PHP 扩展

另见：PEAR (PHP 扩展和仓库)；PECL (PHP 扩展社区库)；特定扩展

- CURL，271
- DOM，16, 271
- `extension_loaded()` 函数，111, 124, 125
- 获取信息的相关函数，111-112
- GD 库，241-263
- Ming，263-269
- PDFlib，233-241
- PDFLib Lite，234
- SimpleXML，16, 269-270
- SOAP，17, 271
- Tidy 库，17
- PHP5 中新的 XML 扩展，16-17
- XSL，16
- ZIP 扩展，271

### PHP Wiki 网站

- 196

### phpaubasic.php 脚本

- `attempt_auth()` 函数，169-170
- `check_login()` 函数，170-171
- 代码列表，167-168
- 为数据库连接定义的常量，169
- 包含在标准 PHP 页面中，171
- 测试，171

### phpaubforms.php 脚本

- 172-174

### phpBB CMS

- 327

### PHP 控制的身份验证

- 与 Apache 控制的身份验证对比，166, 171
- 创建身份验证数据库，166-167
- Basic Authentication 的缺点，171
- 表单身份验证，172-174
- 其他访问限制，174-177
- 用于 Basic Authentication 的 `phpaubsic.php` 脚本，167-171
- 用于表单身份验证的 `phpaubforms.php` 脚本，172-174
- 测试 Basic Authentication，171

### PHP5 变更与增强

- abstract 关键字，7–8
- 访问修饰符，6
- 构造函数和析构函数，6
- 异常，1–5
- final 关键字，6
- 接口，5
- 迭代器，5–6
- 用于重载的魔术方法，8–9
- MySQLi 扩展，12–16
- 新函数，10–12
- OOP 变更，1–9
- 概述，1, 17
- 传递变量，1
- php.ini 配置文件变更，12, 107–108
- SQLite 改进，17
- static 关键字，7
- Tidy 库扩展，17
- XML 支持，16–17

### PHP5 OOP

- abstract 关键字，7–8
- 访问修饰符，6, 23–25
- 赋值与克隆对比，29–30
- 变更与增强，1–9
- 类基础，20–23
- 类常量，28–29
- 构造函数，6, 25–26
- 定义类，20
- 析构函数，6, 26–27
- 异常，1–5
- final 关键字，6
- 继承，31–35
- 实例化类，22–23
- 接口，5, 31, 35–37
- 迭代器，5–6
- 魔术方法，6, 8–9, 37–44
- 方法，21
- 概述，45
- 属性，20–21
- static 关键字，7, 27–28
- 可见性，23–25

### php.ini 配置文件

- 指令的访问值，115
- allow_call_time_pass_reference 指令，106, 115
- 用于 APC 缓存引擎，288–290
- asp_tags 指令，106
- 使用 ini_set() 更改指令，114–115
- display_errors 指令，106
- 用于 eAccelerator 缓存引擎，291–294
- error_log 指令，106
- error_reporting 指令，106
- 用于 JPCache 缓存引擎，297–299
- log_errors 指令，106
- magic_quotes_gpc 指令，106, 113
- magic_quotes_runtime 指令，113
- mail.force_extra_parameters 指令，107
- MySQLi 设置，12
- 输出压缩设置，149
- 用于 PHP 身份验证示例，171
- PHP5 改进，12, 107–108
- 推荐配置指令，105–107
- register_globals 指令，105, 116
- register_long_arrays 指令，107
- 运行时检索设置，109–110
- safe_mode 指令，171
- session.hash_bits_per_character 指令，108
- session.hash_function 指令，108
- short_open_tag 指令，106–107
- variables_order 指令，106
- 用于 Zend Optimizer 缓存引擎，295
- zend.zel_compatibility_mode 指令，108
- zlib.output_compression 指令，107, 149

### phpmychat CMS

- 327

### PHP-Nuke CMS

- 321

### phpversion() 函数

- 108, 126

### phpWebsite CMS

- 自定义默认设置，317
- 默认功能，316–317
- 安装，315–317
- PEAR 库，316
- 优缺点，317–318
- 网站，315

### pi() 函数 (PHP)

- 29

### 便携式文档格式

另见：PDF

### Postnuke CMS

- 322

### preg_grep() 函数

- 53

### preg_replace_callback() 函数

- 53–55

### PrestoPoll CMS

- 327

### print 语句 (PHP)

- 与 echo 语句对比，228–229
- 配合 `__toString()` 魔术方法，44

### private 关键字 (PHP)

- 6, 23

### privkey.pem 文件 (SSL)

- 156

### process() 方法

- ImageCaption 类，252–253
- ImageLogo 类，256–257
- ImageResize 类，247–248
- ImageRotate 类，249–250

### processConfig 方法 (PHP)

- 118–119

### 处理器、性能

- 210

### 性能分析定义

- 207

### 属性 (MySQL)

- mysqli 类，14–15
- mysqli_result 类，16
- mysqli_stmt 类，15

### 属性 (PHP)

- Circle 类示例，21
- 定义，20–21
- 描述，20
- 初始化，21
- 语言翻译，338
- 命名约定，221, 222
- 真实与合成属性，221
- 在子类中重新定义，32–33
- 配合 static 关键字，27
- 配合 this 引用变量，23

### protected 关键字 (PHP)

- 6, 24

### public 关键字 (PHP)

- 6, 23, 24

## Q

### 查询多个表 (MySQL)

- 内连接，78–81
- 外连接，81–82
- 联合，82–86

### 引号

- 用于函数名称内部
- set_exception_handler()，5
- 字符串速度与性能，201–205

## R

### RAM (内存)

- 与性能，200, 210–211
- 一系列数组函数，59–60

### rar 扩展 (PHP)

- 271

### Raymond, Eric S. (Jargon File 作者)

- 214

### readir() 函数 (PHP)

- 61

### 读取

- 目录 (PHP)，60–61
- 流 (PHP)，62

### readyState 属性 (AJAX)

- 278, 279

### recreate function() 函数

- 58

### RecursiveIterator 类 (PHP)

- 6

### register_globals 指令

- 编码以降低被利用的可能性，179, 182
- 利用方式，178–179
- 用于关闭的 .htaccess 文件，179
- HTTP_REFERER 值，174
- 推荐配置，105, 116

### 正则表达式

- 与性能，230
- 配合 RewriteRule 指令 (Apache 的 mod_rewrite)，133–134

### reqs.xml 配置文件，用于配置检查器 (PHP)

- 116

### resize() 函数 (WebImage 类)

- 246–247, 259

### responseText 属性 (AJAX)

- 278

### responseXML 属性 (AJAX)

- 278

### RESTRICT 选项 (MySQL)

- 92

### REVOKE 命令 (MySQL)

- 96–97



### RewriteBase 指令（Apache 的 mod_rewrite 模块）
- 143

### RewriteCond 指令（Apache 的 mod_rewrite 模块）
- 基本格式，139
- 多行链式连接，141
- 比较和系统检查条件，141–142
- 比较运算符，142
- HTTP 头变量，139
- nocase 或 NC 标志，142
- ornex 或 OR 标志，143
- 请求变量，139–140
- 服务器变量，140
- 特殊变量，140–141
- 时间变量，140
- 用法，139–142
- 使用变量，141

### RewriteLog 指令（Apache 的 mod_rewrite 模块）
- 143–144

### RewriteLogLevel 指令（Apache 的 mod_rewrite 模块）
- 144

### RewriteRule 指令（Apache 的 mod_rewrite 模块）
- 自动将 URL 重定向到新目录，132
- 基本格式，131
- 链式或 C 标志，136
- Cookie 或 CO 标志，137
- 启用 mod_rewrite，130–131, 133
- env 或 E 标志，137
- 禁止或 F 标志，135
- 已消失或 G 标志，136
- 用于对人类输入友好的 URL，132–133
- 最后或 L 标志，136
- 下一个或 N 标志，136
- 不区分大小写或 NC 标志，135
- 不转义或 NE 标志，138
- 无子请求或 NS 标志，138
- 透传或 PT 标志，138
- 代理或 P 标志，138
- qsaappend 或 QSA 标志，137
- 重定向或 R 标志，135
- 配合正则表达式使用，133–134
- 用于对搜索引擎友好的 URL，132–133
- 跳过或 S 标志，137
- 标志的语法，135
- 用于其的令牌，131–132
- 类型或 T 标志，137
- 作为 PHP 脚本的类型检查层，134–135
- 用法，131–135

- 右外连接（MySQL），81
- rotate() 函数（WebImage 类），249
- 运行时配置（PHP）。另见配置检查器（PHP）
  - 自动化版本和功能检查，116–128
  - 使用 ini_set() 更改指令，114–115
  - 动态更改，113–115
  - 禁用魔术引用，113
  - 获取当前运行时设置，108–113
  - 移除时间限制，113–114

## S

- SAJAX（简单 AJAX 工具包），282–283
- save() 方法（WebImage 类），244–245
- scandir() 函数（PHP），61
- Schlossnagle, George（APC 创造者），287
- 临时变量，以及性能，229–230
- 脚本（PHP）
  - 压缩（Apache），148–149
  - mod_rewrite 作为（Apache）的类型检查层，134–135
  - 用于调试的 Xdebug PECL 包，197
- Secunia 网站，182
- Apache 与安全套接字层。另见 Apache 与 SSL
- 安全性。另见身份验证；网站安全
- SELECT 语句（MySQL）
  - 配合交叉连接使用，81
  - 用于全文搜索，87–88
  - \G 终止符用于垂直显示，86
  - 配合内连接使用，78–81, 82

### stream_open() 函数（PHP）
- 配合外连接使用，81–82
- 简单形式，76–77
- 配合并集使用，82–86

### self 关键字（PHP）
- 7, 27–28, 50

### send() 方法（AJAX）
- 278

### Sendmail 程序
- 3–4, 107

### Serendipity 博客 Micro CMS
- 324

### 服务器变量
- 访问控制，174–175
- 语言翻译，345–346
- RewriteCond 指令（Apache 的 mod_rewrite 模块），140

- 会话，php.ini 设置，108
- SET DEFAULT 选项（MySQL），92
- \_\_set() 魔术方法（PHP），8, 38–39
- SET NULL 选项（MySQL），92
- set_error_handler() 函数（PHP），1–5
- set_exception_handler() 函数（PHP），4–5
- set_magic_quotes_runtime() 函数（PHP），113
- setRequestHeader() 方法（AJAX），278
- set_time_limit() 函数（PHP），114

### Shape 类示例
- 作为抽象类，34–35
- Circle 类从中继承，31–33

### Shockwave Flash 文件。另见 Ming 扩展（PHP）
- 5

### SHOW COLUMNS 命令（MySQL）
- 101

### SHOW CREATE TABLE 命令（MySQL）
- 101–102

### SHOW DATABASES 命令（MySQL）
- 102

### SHOW GRANTS 命令（MySQL）
- 102

### 简单 AJAX 工具包（AJAX）
- 282–283

### SimpleXML 扩展（PHP）
- 概述，16, 269–270
- xpath() 方法，125, 127

### 单引号 (\')，字符串的速度以及
- 201–205

### 网站安全。另见身份验证
- 使用 Apache 进行访问控制，165–166
- 使用 PHP 进行访问控制，166–177
- 用于其的代码/同行审查，182
- 跨站脚本（XSS），180–181
- 保持补丁更新，181–182
- register_globals 漏洞利用，178–179, 182
- 社会工程学以及，182
- SQL 注入攻击，179–180, 182
- 网站攻击，178–181
- 用于更多信息的网站，182

### 斜杠 (/)
- \G 终止符用于 MySQL 查询，86
- PHP URL 中方案后半部分之后 (://)，72
- \_\_sleep() 魔术方法（PHP），39, 40–43

### SOAP 扩展（PHP）
- 17, 271

### SourceForge 网站
- 263, 353

- 拼写检查 URL（Apache），144–145
- splay（标准公共库），5
- SQL 注入攻击，179–180, 182

### SQLite
- 17

### Apache 与 SSL（安全套接字层）
- 检查 Apache 中是否启用了 SSL，154
- 为 SSL 网站创建目录，157
- 创建自签名证书和密钥，155–156
- 在 Apache 中动态启用 SSL，155
- 在 httpd.conf 中启用 SSL 功能，157
- 更多信息，157
- 用于测试的信息文件，157
- 用于其的 mod_ssl，129, 154–155
- privkey.pem 文件，156
- 移除密码短语，156
- 在 Apache 中静态启用 SSL，154
- testcert.csr 文件，156
- 测试，157
- 端口 443 的 VirtualHost 部分，157

### ssl.conf 文件
- 157

### 标准公共库（SPL）
- 5

### static 关键字（PHP）
- 7, 27–28

### status 属性（AJAX）
- 278, 279

### stream_close() 函数（PHP）
- 63, 67

### stream_eof() 函数（PHP）
- 63

### stream_open() 函数（PHP）
- 文件访问记录器示例，67
- GIS 照片数据库查询示例，70–71
- 概述，62, 63

### stream_read() 函数（PHP）
- 文件访问记录器示例，67
- GIS 照片数据库查询示例，71
- 概述，62

### 流（PHP）
- 构建流包装器，62–63
- 定义，61–62
- 文件访问记录器示例，63–67
- GIS 数据库查询示例，67–72
- PHP 中仅允许字节流，62
- 概述，61–62
- 用于命名流资源的 URL 系统，72
- 包装器方法，62–63

### stream_tell() 函数（PHP）
- 71

### stream_wrapper_register() 函数（PHP）
- 62

### stream_write() 函数（PHP）
- 63, 67

### 字符串（PHP）
- 对其速度的基准测试，201–205
- 性能与字符串函数，230
- \_\_toString() 魔术方法，43, 44

### stripslashes() 函数（PHP）
- 113

### 子类化
- 用于停止的语言翻译，342
- 在子类中重新定义属性和方法，32–33

- Subversion 版本控制系统，350–351
- SWFAction 对象（Ming），264
- SWFBitmap 对象（Ming），264, 267
- SWFButton 对象（Ming），264, 268
- SWFDisplayItem 对象（Ming），265
- SWFFill 对象（Ming），265
- SWFFont 对象（Ming），265
- SWFGradient 对象（Ming），265
- SWFMorph 对象（Ming），265
- SWFMovie 对象（Ming），263, 264, 267
- SWFShape 对象（Ming），265, 267, 268
- SWFSprite 对象（Ming），264, 265, 266–267
- SWFText 对象（Ming），265
- SWFTextField 对象（Ming），265

- switch 语句，用于其的语言翻译，332–333
- 合成属性命名约定，221

## T

- 避免使用制表符进行缩进，216–217
- tables_priv 表（MySQL），99, 100
- testcert.csr 文件（SSL），156
- $this 引用变量（PHP），23, 50
- Tidy 库扩展（PHP），17
- Tigris.org 社区，351
- TikiWiki CMS
  - 自定义默认设置，320–321
  - 默认功能，318–319
  - “非活动”功能，319–320
  - 安装，318–320
  - 优缺点，321
  - 网站，318

- top 进程监视器实用程序，208–210
- \_\_toString() 魔术方法（PHP），43, 44
- try/catch/throw 块（PHP）
  - 语言翻译，344–345
  - 用于 pdf_new() 函数，234
  - 语法，2

## U

- Umbrello UML 工具，352–353

### UML 图
- ArgoUML 工具，351–352
- 概述，351
- Umbrello 工具，352–353

### 并集（MySQL）
- 不同长度的列列表以及，83
- 连接与，82
- 描述，82
- 不同名称的表列以及，83
- \G 终止符用于查询，86
- 配合连接使用，84
- 缺失列的 NULL 值，84–86




### unset() 函数、性能与，230
### UPDATE 语句 (MySQL)，77，91–92

### URL 重写 (Apache)

- 自动将 URL 重定向到新的目录，132
- 避免自动转义，138
- 将 mod_rewrite 与其他模块结合使用，138
- 控制日志记录的详细程度，144
- 启用 mod_rewrite，130–131，133
- 强制请求通过代理模块，138
- 用于对人类输入友好的 URL，132–133
- 使模式不区分大小写，135
- 覆盖 MIME 类型，137
- 保留查询字符串，137
- RewriteBase 指令，143
- RewriteCond 指令，139–143
- RewriteLog 指令，143–144
- RewriteLogLevel 指令，134
- RewriteRule 指令，131–138
- 用于对搜索引擎友好的 URL，132–133
- 发送 HTTP 403 禁止访问响应，135
- 发送 HTTP 410 已删除响应，136
- 设置 Cookie，137
- 设置环境变量，137
- 跳过规则，137，138
- 指定基础路径或前缀路径，143
- 指定用于处理的日志文件，143–144
- 从规则列表的开始处启动处理过程，136
- 成功匹配后停止处理，136
- 考虑内部子请求，138
- 测试字符串是否匹配模式或条件，139–143
- 作为 PHP 脚本的类型检查层，134–135
- 使用代码块，136
- 使用带有 HTTP 状态码的正式重定向，135

### URL。另请参阅 [URL 重写 (Apache)](https://example.org/url_rewriting_apache)

- 流资源命名指南，72
- 其中的 PHP 约定，72
- 拼写检查 (Apache)，144–145
- USE 语句 (MySQL)，75，149

### 用户管理 (MySQL)

- GRANT 和 REVOKE 的替代方案，97–100
- 列，priv 表，99，100
- db 表，98–99，100
- GRANT 命令，94–96
- 概述，93–94
- 重新加载权限表，100
- REVOKE 命令，96–97
- 表，priv 表，99，100
- user 表，97–98，99–100

### 用户 (MySQL)，97–98，99–100

- 使用 USING 语句进行内连接 (MySQL)，79

## V

- **var 关键字 (PHP4)，24**

### 变量 (PHP)

- 按值赋值与按引用赋值，29
- 克隆，29–30
- 语言翻译，330
- 命名约定，220，222
- 传递，PHP5 中的更改，1
- php.ini 设置，105，106
- **VBScript**。另请参阅 [语言翻译](https://example.org/language_translation)
- **版本控制系统**，350–351
- 可见性关键字。另请参阅 [访问修饰符 (PHP)](https://example.org/access_modifiers_php)

## W

- **wakeup() 魔术方法 (PHP)，40–43**

### Web CMS。另请参阅 [CMS（内容管理系统）](https://example.org/cms_content_management_systems)

- 全能型 Web CMS，309–322
- 描述，308
- Drupal，321
- ExponentCMS，309–312
- Mambo，321
- 微型 CMS，322–328
- 开源包，308
- PHP-Nuke，321
- phpWebsite，315–318
- Postnuke，322

### Web CMS（续）

- TikiWiki，318–321
- XOOPS，312–315

**WebCalendar CMS，327**

**WebDAV（基于 Web 的分布式创作和版本管理）**

- 身份验证，159
- 将 mod_dav 构建为共享对象，158
- 静态构建 mod_dav，158
- 检查 mod_dav 是否已启用，158
- 描述，158
- 用于文件仓库的目录，158
- 支持该协议的编辑器，159
- httpd.conf 文件中针对 mod_dav 的条目，158
- Mac OS 设置，163
- Windows 2000/XP 设置，159–162

**GD 库的 WebImage 类**

- 功能，241
- caption() 方法，251–252
- 代码列表，241–243
- display() 方法，244
- imagesavealpha() 函数，244
- load() 函数，243–244
- logo() 方法，255–256
- 公有属性，243
- resize() 函数，246–247，259
- rotate() 函数，249
- save() 方法，244–245
- 语言翻译中的 while 循环，333

**Whitesmith 缩进风格，215**

**wiki 微型 CMS**

- DocuWiki，326
- MediaWiki，325–326
- 术语起源，324
- 概述，323–324

**Windows 2000/XP 的 WebDAV 设置，159–162**

**WordPress 博客微型 CMS，323**

**编写流 (PHP)，63**

**WROX 网站，76**

## X

**Xdebug PECL 包，197**

**XHTML，AJAX 的使用，273**

**XML。另请参阅 [AJAX（异步 JavaScript 和 XML）](https://example.org/ajax_asynchronous_javascript_xml)**

- 配置检查器 (PHP)，116–128
- 更多信息，285
- PHP5 支持，16–17
- SimpleXML 扩展 (PHP)，16，125，127，269–270

**XMLConfigProcessor.php 类**

- checkConfig() 函数，126–128
- checkConfigAccess() 方法，124
- checkDepts() 方法，124
- checkExtensions() 方法，125
- checkPHP() 方法，125–126
- 代码列表，119–122
- 构造函数，122–123
- 其中的 extension_loaded() 函数，124，125
- 其中的 ini_get_all() 函数，126，127
- 其中的 ini_set() 函数，127–128
- $message 属性，122
- 其中的 phpversion() 函数，126
- process() 方法，123
- 其中的 SimpleXML xpath() 方法，125，127
- version_compare() 函数，126
- $xml 属性，122
- $xmlfile 属性，122

**XMLHTTP 和 XMLHttpRequest 接口 (AJAX)**

- 更多信息，285
- 处理 ReadyStateChange 事件，280
- 处理响应，280–282
- 历史，277
- 方法，277–278
- 属性，278–279
- 处理浏览器差异，279–280

**XOOPS（可扩展面向对象门户系统）**

- 自定义默认设置，314–315
- 默认功能，313
- 安装，312–313
- 可用的其他模块，313
- 优缺点，315
- 网站，312

**xpath() 方法 (SimpleXML)，125，127**

**XSL 扩展 (PHP)，16**

**XSS（跨站点脚本），180–181**

## Z

- Zowodny, Jeremy (MySQL 专家)，350
- ZenCart CMS，327
- **Zend Engine 1**，其中的 php.ini 设置，**108**

**Zend Optimizer 缓存引擎**

- 配置，295
- 安装，294–295
- 其他缓存引擎，305
- 概述，294
- 移除，296
- 适用情况，305
- 网站，295

**ZIP 扩展 (PHP)，271**

**Zlib 库 (PHP)，107**

![](img/ab27c6ac898db1f934d39fa127b14657_405_0.png)

### 随时随地携带您的图书馆。

现在，无论您身在何处，都可以在线访问 70 多本完整的 Wrox 书籍！您订阅 **Wrox 参考库** 后，即可获取所有的图表、描述、屏幕截图和代码示例。为了在需要答案的时间和地点获取帮助，请访问 wrox.books24x7.com 并立即订阅！

查找书籍主题：
- ASP.NET
- C# / C++
- 数据库
- 通用
- Java
- Mac
- Microsoft Office
- .NET
- 开源
- PHP/MySQL
- SQL Server
- Visual Basic
- Web
- XML

![](img/ab27c6ac898db1f934d39fa127b14657_405_1.png)

www.wrox.com
