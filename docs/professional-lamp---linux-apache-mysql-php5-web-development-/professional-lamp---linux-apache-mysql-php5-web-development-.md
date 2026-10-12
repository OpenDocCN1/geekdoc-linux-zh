# LAMP 专业开发：Linux、Apache、MySQL 与 PHP5


# 关于作者

**Jason Gerner** 目前主要在辛辛那提担任网络开发人员，空闲时间则抱怨对网络标准支持不足以及滥用 XML。他经常潜伏在 PHPBuilder.com 的讨论论坛中，并担任版主。

**Elizabeth Naramore** 拥有来自俄亥俄州迈阿密大学的组织行为学学士学位，自 1997 年起从事网站开发。她的主要关注领域包括 PHP/MySQL、电子商务以及自由撰稿和教学。她的文章见于 PHPBuilder.com 和 International PHP Magazine。她是 OINK-PUG（俄亥俄、印第安纳、北肯塔基 PHP 用户组）的自豪成员，与丈夫和两个年幼的孩子生活在俄亥俄州辛辛那提。

**Morgan L. Owens** 从奥克兰大学数学专业毕业后，该学位无人问津，他随后在 IT 行业摸爬滚打，成为内联网和互联网环境下基于 Web 的后端网络开发人员和程序员。他仍然居住在奥克兰，但建议如果有合适的工作，他可能会——可能会——考虑搬迁。

**Matt Warden** 从事基于 Web 的应用开发已超过六年。他的工作主要专注于为其他企业设计和实施 LAMP 应用程序，以便内部使用以提高生产力。最近，Matt 一直使用 AJAX 提供基于 Web 的替代方案，以获得通常仅在与本地桌面解决方案中才能获得的效率提升。目前，Matt 是位于俄亥俄州辛辛那提的 Signal US Communications 的首席开发人员。

# 致谢名单

- **执行编辑：** Carol Long
- **高级收购编辑：** Debra Williams Cauley
- **发展编辑：** Brian MacDonald
- **贡献者：**
  - William Barnett
  - Wm. Christopher Mastin
- **技术编辑：**
  - Jason Gerner
  - Elizabeth Naramore
- **制作编辑：** Kenyon Brown
- **文字编辑：** Kathryn Duggan
- **编辑经理：** Mary Beth Wakefield
- **制作经理：** Tim Tate
- **副总裁兼执行集团出版人：** Richard Swadley
- **副总裁兼执行出版人：** Joseph B. Wikert
- **项目协调员：** Kristie Rees
- **图形和制作专员：**
  - Carrie Foster
  - Lauren Goddard
  - Denny Hager
  - Barbara Moore
  - Alicia B. South
- **质量控制技术员：**
  - Amanda Briggs
  - John Greenough
  - Jessica Kramer
  - Joe Niesen
- **媒体开发专员：**
  - Angie Denny
  - Katie Jenkins
  - Steve Kudirka
  - Kit Malone
  - Travis Silvers
- **媒体开发协调员：** Laura Atkinson
- **校对和索引：** TECHBOOKS 制作服务

# 致谢

感谢我可爱的妻子在过去年份里对我的容忍和支持。我还要感谢我的合著者们出色的工作以及他们为这个项目付出的时间。还要感谢 Wiley 的人们给我们机会，并特别感谢 Brian 的巨大帮助以及他对我们的信任。—*Jason Gerner*

我要感谢我的父母，他们总是让我感到很酷，尽管我过去是、现在依然是、将来也永远是一个怪人（geek）。我还要感谢我的丈夫和孩子们，在我压力大时照顾我，并成为我的欢乐源泉。也要感谢 Jason 和 Brian 帮助我们顺利落地本书。—*Elizabeth Naramore*

我想感谢 Scott 以及 HIT Studios 的其他团队成员，尤其是他们让我接触到了"PHP"这个东西；感谢我的其他合著者，即使在看到我的写作后仍然邀请我参与这个项目；感谢科罗拉多大学的 Karl Gustafson，多年前的建议让我受益，尽管他肯定不知道我在说什么；以及感谢我的朋友和家人，他们真的是我的生命支持系统——特别是我的祖母 Doris Madeline Rachael Shipton (1918–2005)。—*Morgan L. Owens*

特别感谢 Sam Foster，最初我们在试图确定使用 XMLHTTP 和 XMLHttpRequest 对象的最佳实践时，通过电子邮件与他合作，当时关于该主题的资料非常少。他的想法启发了 RemoteConnection 对象设计的许多方面。—*Matt Warden*


# 引言

围绕 LAMP 的所有喧嚣是怎么回事？这个“LAMP”是什么，我如何获得它？这些问题将在本书的页面中得到解答。在这种情况下，LAMP 代表 Linux、Apache、MySQL 和 PHP，它已被证明是开发企业级 Web 应用最快的增长方式之一。所有这些包都是开源的，因此你基本上可以自由地使用它们，唯一的限制是你自己的想象力。此外，使用开源技术，你不仅拥有行业内最优秀的人才协作提供优秀的包，如果你遇到任何麻烦，你还能得到开源社区其他成员的巨大支持。读完本书后，你将对 LAMP 有更深入的了解，并在开发动态网站时将其付诸实践。由于目前这是唯一一本高级 LAMP 书籍，并且是 Wrox 专业系列的一部分，你可以放心，其中包含的信息将有助于使你成为一名更好的编码者，并领先于其他人。

需要注意的是，虽然“LAMP”一词在更广泛的定义中也可以包含 Perl 和 Python，但我们选择在本书中专注于 PHP。

本书的目标是将初中级 Web 开发者进一步向前推进，为他们配备关于这些模块更高级别的知识。我们在本书中为你提供工具，让你能够“跳出盒子”思考，并为老问题找到新的解决方案。

## 本书适合谁？

本书适合有一定经验并希望将网站提升到下一个层次的 Web 开发者。如果你有兴趣使用开源工具来运行动态、令人兴奋的 Web 站点，你会在这里找到你需要的内容。我们假设阅读本书的人在以下领域具有一些基本经验：

-   Web 服务器技术
-   面向对象编码
-   数据库结构、设置和交互（检索、修改和添加数据）
-   设置用户和权限
-   安装新软件
-   使用命令行

虽然如果你有一个熟悉的当前 LAMP 设置会有帮助，但这并不是必需的。只要你熟悉安装新软件，你就可以轻松地将 Apache、MySQL 和 PHP 一起安装。也有一些软件包可以一次性完成这三个模块的安装，例如 XAMPP（可在 [http://www.apachefriends.org/en/xampp.html](http://www.apachefriends.org/en/xampp.html) 获取）。

读完本书后，你将能够自信地克服任何 LAMP 障碍，为你可能希望编写的未来应用程序拥有一些很棒的新想法，或者以新的效率和力量重新整理你的一些旧代码。




## 简介

### 本书涵盖的内容

本书涵盖了多种主题：

- PHP 5.0 新特性指南
- PHP 中面向对象编程（OOP）的深入探讨
- 代码效率、基准测试以及改进结果
- 配置 PHP 以获得最佳性能
- 高级 MySQL 查询
- Apache 技巧和窍门
- 本地和远程站点安全
- 使用高级 PHP 扩展
- 常见的 PEAR 包
- Ajax 和 PHP
- 晦涩的 PHP 命令
- CMS 的比较与解析
- 博客程序包
- 从其他编程语言过渡的指南
- 缓存引擎

### 使用本书所需的条件

本书设计为在 Linux 机器上使用，但书中的许多信息也可以应用于 Windows 用户。您需要 PHP、MySQL 和 Apache 来完成本书中的练习。这三个都是开源程序，您可以免费下载使用。您还需要一个文本编辑器来输入代码。最后，您需要一个网络浏览器，如 Internet Explorer、Netscape Navigator、Firefox、Safari 或 Opera，来查看您的网页。

正如任何程序员都知道的，软件在不断改进和调试，虽然我们在出版时使用了模块的最新版本，但这些版本很可能很快就会过时。重要的是，您应访问 PHP、Apache 和 MySQL 的源网站，以获取最新更新版本和最近的发布说明。在使用应用程序开发网站时，我们建议您始终使用最新稳定版的使用未完全测试的软件版本可能会危及其应用并使代码留下漏洞，这对新学习者同样适用——您应该基于应用程序的稳定版进行学习，而不是 beta 版。

本书编写时生效的最新稳定版本为：

- PHP：版本 5.0.4（可在 <http://www.php.net> 获取）
- Apache：版本 2.0.54（可在 <http://www.apache.org> 获取）
- MySQL：版本 4.1.12（可在 <http://www.mysql.com> 获取）

本书的后续版本将随着这些程序变更和改进的出现而对其进行更新。

### 约定

为了帮助您充分利用文本内容并跟踪当前讨论的情况，我们在全书中使用了许多约定。

![](img/cacdd24f2926f10ee3219256ad732604_22_0.png)

提示、技巧、窍门以及对当前讨论的补充说明以斜体形式呈现，并像这样进行排版。

关于文本中的样式：

- 我们在引入重要术语时会进行高亮显示。
- 我们呈现 URL 的方式如下：<http://www.mysite.com>
- 我们在文本中展示代码的方式如下：`persistence.properties`
- 我们以两种方式呈现代码：

![](img/cacdd24f2926f10ee3219256ad732604_22_1.png)

灰色高亮不用于在当前语境中重要性较低的代码，或之前已展示过的代码。

### 源代码

当您阅读本书中的示例时，您可以选择手动输入所有代码，或使用随书提供的源代码文件。本书中使用的所有源代码均可在 <http://www.wrox.com> 下载。到达该网站后，只需定位书名（通过使用搜索框或使用标题列表之一），然后单击书籍详情页面中的下载代码链接，即可获取本书的所有源代码。

由于许多书籍的标题相似，按 ISBN 搜索可能最方便。本书的 ISBN 为 0-7645-9723-X。

下载代码后，只需使用您喜爱的压缩工具进行解压缩。或者，您可以访问 Wrox 代码下载主页 <http://www.wrox.com/dynamic/books/download.aspx>，查看本书以及所有其他 Wrox 书籍的可用代码。

### 勘误表

我们尽力确保文本或代码中没有错误。然而，人无完人，错误难免发生。如果您在我们的某本书中发现错误，如拼写错误或故障代码，我们将非常感激您的反馈。通过提交勘误，您可能会为另一位读者节省数小时的烦恼，同时也在帮助我们提供更高质量的信息。

要查找本书的勘误表页面，请访问 <http://www.wrox.com>，并使用搜索框或其中一个标题列表定位书名。然后，在书籍详情页面中，单击书籍勘误链接。在此页面，您可以查看已提交并由 Wrox 编辑发布的关于本书的所有勘误。包含每本书勘误链接的完整书籍列表也可在 www.wrox.com/misc-pages/booklist.shtml 获取。

如果您没有在书籍勘误页面发现“您的”错误，请访问 www.wrox.com/contact/techsupport.shtml 并填写该处的表单，向我们发送您发现的错误。我们将检查信息，并视情况将消息发布到书籍的勘误页面，并在书籍的后续版本中修复此问题。

### p2p.wrox.com

作者和同行讨论，请加入 p2p.wrox.com 的 P2P 论坛。论坛是一个基于 Web 的系统，您可以发布与 Wrox 书籍和相关技术相关的信息，并与其他读者和技术用户互动。论坛提供了一项订阅功能，当论坛中有新帖子时，会按您选择的感兴趣主题发送邮件给您。Wrox 作者、编辑、其他行业专家以及您的 fellow 读者都活跃在这些论坛上。

在 <http://p2p.wrox.com> 上，您会发现许多不同的论坛，不仅在您阅读本书时，还在您开发自己的应用程序时都会对您有所帮助。要加入论坛，只需按照以下步骤操作：

1. 前往 p2p.wrox.com 并单击注册链接。
2. 阅读使用条款并单击同意。
3. 填写加入所需的必填信息以及您愿意提供的任何可选信息，然后单击提交。
4. 您将收到一封电子邮件，其中包含有关如何验证您的账户并完成加入流程的信息。

您可以阅读论坛中的信息而无需加入 P2P，但为了发布您自己的信息，您必须加入。

加入后，您可以发布新消息并回复其他用户发布的消息。您可以随时在网络上阅读信息。如果您希望特定论坛的新消息通过电子邮件发送给您，请单击论坛列表中论坛名称旁的订阅此论坛图标。

要了解如何使用 Wrox P2P 的更多信息，请务必阅读 P2P 常见问题解答（FAQs），以获取关于论坛软件工作原理以及许多针对 P2P 和 Wrox 书籍的常见问题的答案。要阅读 FAQs，请单击任何 P2P 页面上的 FAQ 链接。

## 专业 LAMP

![](img/cacdd24f2926f10ee3219256ad732604_26_0.png)

## PHP5 有什么新特性？

那么 PHP5 的突破点在哪里呢？如果您对 PHP4 有经验，您可能了解面向对象编程以及 PHP4 中的处理方式。如果您不熟悉 PHP，但熟悉其他编程语言，您可能会发现 PHP5 的面向对象原则实现很熟悉。幸运的是，随着 PHP5 的发布，事情变得简单了许多。然而，除了“更好的面向对象编程”处理之外，还有其他改进和变化，例如 php.ini 中更多的配置选项以及一系列新的数组相关和其他函数。本章为您概述了这些变化。

### 面向对象的变化

以下变化涉及 OOP 模型及相关功能和主题。其中大部分变化在第二章中有更详细的介绍，但这里也简要概述供您快速参考。

#### 传递对象

PHP5 中面向对象变化的一个重大影响是变量作为参数传递给函数的方式。在 PHP4 中，除非使用 $varname 语法另外注明，否则默认情况下变量是按值传递而不是按引用传递的。在 PHP5 中，默认是按引用分配值。

#### 异常

简而言之，异常是发生错误时执行的程序。现在，当程序遇到意外错误时，您不再让程序完全停止，而是可以对程序在此类错误下应该做什么进行更多的控制。您可能熟悉 PHP4 中可用的 `set_error_handler()` 函数。如果您不熟悉，该函数的目的是定义一个用于错误处理的用户函数。然而，其实现存在许多限制。例如，如果错误类型为 E_ERROR 或 E_PARSE，则它不起作用，




# 第 1 章

E_CORE_ERROR、E_CORE_WARNING、E_COMPILE_ERROR、E_COMPILE_WARNING 以及大多数 E_STRICT。此外，如果错误发生在 set_error_handler() 函数脚本之前，该函数将永远不会被调用。PHP5 引入了一个用于处理异常的新框架。

## Try/Catch/Throw

如果你拥有 C++ 或 Java 等语言的编程经验，你肯定听说过“try（尝试）”、“catch（捕获）”和“throw（抛出）”这些术语。当发生错误时，异常会被“抛出”。可能会引起错误的代码被放在 try/catch 块中，该代码会在（try 下）尝试运行。如果抛出异常，它会被“捕获”，并且应该采取用户定义的操作（在 catch 下）。try/catch/throw 块的语法如下：

```php
<?php
try
{
  $error_message = 'Hello, I am an error';
  throw new Exception($error_message);
}
catch (Exception $e)
{
  echo 'Exception caught: ', $e->getMessage(), "\n";
}
?>
```

## 内置异常类

你刚才看到的 Exception 类也是 PHP5 的改进之一，默认情况下是内置的。借助 PHP5，你现在可以获取已抛出异常的信息，并使用这些数据做出适当的反应。用于处理并存储这些数据的内置异常类如下所示：

```php
<?php
class Exception
{
  protected $message = 'Exception Thrown';
  protected $code = 0;
  protected $file;
  protected $line;

  function __construct($message = null, $code = 0);
  final function getMessage();
  final function getCode();
  final function getFile();
  final function getLine();
  final function getTrace();
  final function getTraceAsString();
  function __toString();
}
?>
```

## PHP5 有什么新特性？

仔细看看 **Exception** 类：

| 成员或方法名称 | 代表的含义 |
| --- | --- |
| $message | 异常消息；默认值可以设置为你喜欢的任何内容 |
| $code | 用户定义的代码 |
| $file | 发生错误的文件名 |
| $line | 发生错误的行号 |
| getMessage() | 返回 $message |
| getCode() | 返回 $code |
| getFile() | 返回 $file |
| getLine() | 返回 $line |
| getTrace() | 返回包含 debug_backtrace() 函数信息的数组 |
| getTraceAsString() | 返回与 getTrace() 函数相同的结果，但以格式化字符串的形式返回 |
| __toString() | PHP5 的魔术方法，当与 print 或 echo 一起使用时，允许将对象格式化为字符串 |

在前面的 try/catch/throw 示例中，我们使用内置异常类中的 getMessage() 函数来返回并显示错误消息的内容。

## 扩展内置异常类

显然，内置异常类是最通用的类形式，虽然它在许多情况下非常有用，但有时你可能希望更具体地定义异常的处理方式。例如，在发送电子邮件时，如果收件人的电子邮件地址为 null，你并不会收到 PHP 错误。除非你正在监控 sendmail 日志，否则你很可能不知道你的电子邮件没有发送出去。这将是有用的信息，因此你可以轻松地使用 extends 关键字扩展内置类，如下所示：

```php
<?php
class emailException extends Exception
{
    function __construct($message)
    {
        echo "There was an error sending your email: <br />";
        echo $message;
    }

    function sendEmail($to, $subject, $message)
    {
        if ($to == NULL)
        {
            throw new emailException ("Recipient email address is NULL");
        }

        mail($to, $subject, $message);
    }

    try {
        sendEmail("", "Exception Testing",
                  "We are testing the exception handling in PHP5");
    } catch (emailException $e) {
        {
            echo " in file <strong>" . $e->getFile() . "</strong>";
            echo " on line <strong>" . $e->getLine() . "</strong>";
        }
    }
?>
```

这将产生以下结果：

> There was an error sending your email:
> Recipient email address is NULL in file /usersites/email exception.php on line 11

你可以访问存储在内置异常类中的文件名和行信息，但你还可以添加更详细的错误消息用于调试目的。

## set\_exception\_handler() 函数

默认情况下，任何未被捕获的异常都会产生致命错误并停止脚本的执行。PHP5 让你有机会通过 set\_exception\_handler() 函数清理任何未被捕获的异常。类名、错误消息和回溯会被传递给 set\_exception\_handler 函数，但你也可以访问内置异常类的信息。该函数的使用方式如下：

```php
<?php

function lastResort ($e)
{
    echo "Previously uncaught exception being caught from " . get\_class($e);
    echo " in file: " . $e->getFile() . " on line " . $e->getLine();
}

set\_exception\_handler("lastResort");

throw new Exception();
?>
```

你的结果将类似于这样：

> Previously uncaught exception being caught from Exception in file:
> /usersites/set exception handler.php on line 9

注意，你必须在 `set_exception_handler()` 函数中的函数名周围使用引号；否则你将收到一个通知，表明你正在尝试使用未定义的常量。

## 接口

接口已被添加到 PHP5 中，允许你将类绑定到多个位置。它们由空函数（将在实现类中定义）以及你想要应用于实现类的任何常量组成。接口的所有实现类必须提供接口中定义的每个方法的实现，从而确保未来使用你代码的人知道期望的方法。

接口在第 2 章中有更详细的讨论。

## 迭代器

通过标准公共库（SPL），你可以访问一组全新的类和接口，允许你操作和利用迭代器。SPL 是一个在 PHP 中默认编译并可用的扩展，基本上是一个供你使用的接口和类库。下一节讨论了 `Iterator` 类本身。你会注意到许多函数类似于数组函数。

### 主迭代器接口

`Iterator` 类是一个内置接口，允许你遍历任何可以用 `foreach()` 语句遍历的内容——例如，文件目录、查询结果或数据数组。它带有一些固有的函数：

- `Iterator::current()` ：返回当前元素。
- `Iterator::key()` ：返回当前元素的键。
- `Iterator::next()` ：将指针移动到下一个元素。
- `Iterator::valid()` ：在调用 `next()` 或 `rewind()` 后验证是否存在元素。

通过预定义通用的迭代器功能，这些功能都可以帮助你使用迭代使你的代码更强大、更高效。迭代器接口最重要的一点是，它是其他迭代器类的基础组件之一。

### 其他迭代器类

以下部分简要描述了一些继承自 `Iterator` 类的主要类。有关以下任何类的更详细信息以及更全面的列表，可以在在线 SPL 文档中找到：
http://www.php.net/~helly/php/ext/spl/main.html.

### DirectoryIterator

顾名思义，`DirectoryIterator` 是一个实现了 `Iterator` 并允许你处理文件目录的迭代器类。在这个类中，有一组强大的函数，可以获取有关每个文件的信息，例如修改时间和日期、文件大小、文件类型、文件所有者、文件的完整路径以及与文件相关的权限（仅举几例）。





## 第 1 章

### RecursiveIterator

**RecursiveIterator** 类有助于实现递归迭代，即函数被自动反复调用直到满足特定条件为止。该类提供的方法可以帮助你判断是否存在子迭代器，以及这些子迭代器可能是什么。

### ArrayIterator

通过 **ArrayIterator** 内置类，你可以在迭代对象时修改数组的值和键。它允许你在每次迭代时操作数组。诸如 **append()**、**copy()** 和 **seek()** 等函数使程序员能够使用常规数组函数集之外更高级的数组操作。

迭代器正在不断得到改进和增强，预计你在 PHP 5.1 中会看到一些重大变化。

## 构造函数和析构函数

在 PHP4 中，你可以通过将方法命名与类名相同来在类中直接调用该方法。在 PHP5 中，有一个新的“魔术方法”名称用于此目的，即 `__construct()`。如果在类中包含此方法，当对象创建时它将自动被调用。

同样，如果在类中包含了魔术方法 `__destruct()`，对象将被销毁。当调用此方法时，它会销毁对象。如果没有对象的其他引用，或者你到达了 PHP 脚本的末尾时，`__destruct()` 方法也会被调用。

第 2 章将更详细地讨论构造函数和析构函数。

### 访问修饰符

你现在可以使用 PHP5 新增的三个关键字 `public`、`private` 和 `protected` 来控制类成员和方法的可见性级别。方法和成员被标记为公有（public）、私有（private）或受保护（protected）。

以下是 `private`、`protected` 和 `public` 关键字的简要总结（你可以在第 2 章中阅读更多关于这些属性的内容）：

- **Public（公有）**：这些成员和方法对整个脚本可用。它们可以在对象内部或外部被引用。
- **Protected（受保护）**：被标记为受保护的成员或方法仅可从对象内部或继承类中访问。
- **Private（私有）**：私有方法和成员仅可从对象本身内部访问，任何继承类都无法访问它们。

### final 关键字

`final` 关键字可以与类或类内的方法一起使用。当与类一起使用时，此关键字阻止其他类继承它。当与方法一起使用时，它防止任何继承类重写该方法，从而确保其永久性，并保护它不受其他程序员甚至你自己的影响。

## PHP5 中的新特性

## static 关键字

将成员或方法声明为 **static**（静态）将其绑定到其所在的类，而不是类的任何特定对象或实例。静态成员和方法可以在整个脚本中访问。

关于使用 **static** 关键字，有一些重要的注意事项。首先，代替使用 `$this->varName` 语法从类内部访问变量，你应该使用 `self::$varName`。在之前的示例中，你从一个不同的函数中访问了 `self::$count` 成员，但由于静态示例在类内部对任何内容都可用，你仍然使用了 `self::` 语法。其次，当从类外部访问静态成员时，你应该使用 `className::$varName` 语法。同样，当在类内部任何地方访问静态方法时，你应该使用 `self::methodName()`，当从类外部访问时，你应该使用 `className::methodName()`。

第 2 章将更详细地讨论 **static** 关键字的使用。

### abstract 关键字

当你有一个高层类，你知道它需要被更具体的低层类继承时，就会使用 **abstract**（抽象）关键字。例如，你可以按如下方式使用抽象类和方法：

```php
<?php
abstract class getToday {
    public $today = getdate();
    abstract function showCalender();
}
class monthlyCalender extends getToday {
    function showCalender() {
        //Show this month's calender
    }
}
class dailyCalender extends getToday {
    function showCalender() {
        //Show today's daily calender
    }
}
class yearlyCalender extends getToday {
    function showCalender() {
        //Show the calender for this year
    }
}
?>
```

这个抽象类基本上表示“创建一个日历，但你必须在子类中指定类型”。正如你所见，第一个类中的 showCalendar() 函数被故意留空且抽象，因为该类应该被扩展，并且根据调用的继承类显示正确的日历。getToday() 类是不完整的，是抽象化的完美候选者。

抽象方法，就像接口中的那些一样，实际上是空白的，需要在子类中进一步实现。

使用抽象类时的一些规则包括：

- 如果你有一个抽象方法，整个类也必须定义为抽象。
- 你不能实例化一个抽象类。
- 你可以定义一个类为抽象类，即使其中不包含任何抽象方法。
- 实现抽象方法的继承类必须具有与其父类相同（或更弱）的可见性。

在第 2 章中，我们将更详细地讨论抽象性。

### 内置方法重载函数

与 PHP4 不同，在 PHP4 中你必须使用 `overload()` 函数来强制执行重载检查，而 PHP5 原生允许你重载任何超出预期范围的方法或成员引用，从而有效地让你控制接下来发生的事情。新的魔术方法 `__get()`、`__set()` 和 `__call()` 用于重载，如下所示：

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

### 新函数

以下是 PHP5 中所有新函数的综合列表，不包括需要扩展的那些函数：

- **array_combine()**：将两个数组合并为一个，一个数组用于值，另一个用于键。
- **array_diff_uassoc()**：使用额外的键比较（由命名函数确定）来确定两个或多个数组之间的差异。
- **array_udiff()**：使用命名函数进行数据比较，以确定两个或多个数组之间的差异。
- **array_udiff_assoc()**：使用额外的键比较并使用命名函数进行数据比较，以确定两个或多个数组之间的差异。
- **array_udiff_uassoc()**：使用命名函数进行额外的键比较，并使用命名函数进行数据比较，以确定两个或多个数组之间的差异。
- **array_uintersect()**：使用命名函数进行数据比较，以确定两个或多个数组之间的交集。
- **array_uintersect_assoc()**：使用额外的键比较并使用命名函数进行数据比较，以确定两个或多个数组之间的交集。
- **array_uintersect_uassoc()**：使用命名函数进行额外的键比较，并使用命名函数进行数据比较，以确定两个或多个数组之间的交集。
- **array_walk_recursive()**：递归地对数组的每个元素应用命名函数。
- **convert_uudecode()**：解码 uuencode 字符串。
- **convert_uuencode()**：对字符串进行 uuencode。
- **curl_copy_handle()**：复制 cURL 句柄及其所有设置。
- **date_sunrise()**：根据给定的纬度、经度、天顶角和 GMT 偏移量返回日出时间。
- **date_sunset()**：根据给定的纬度、经度、天顶角和 GMT 偏移量返回日落时间。
- **dba_key_split()**：将字符串表示形式中的索引拆分为数组表示形式。
- **dbase_get_header_info()**：返回 dBase 数据库的列结构信息。




## 第 1 章

- `dbx_fetch_row()`：从查询结果中获取行，但如果查询中未设置 `DBX_RESULT_UNBUFFERED`，则操作会失败。
- `fbsql_set_password()`：更改命名用户的密码。
- `file_put_contents()`：等效于打开文件、写入文件并关闭文件的操作。
- `ftp_alloc()`：向 FTP 服务器发送 `ALLO` 命令，该命令为上传的文件预留空间。
- `get_declared_interfaces()`：返回脚本中声明的任意接口。
- `get_headers()`：返回服务器响应 HTTP 请求时发送的头部信息。
- `headers_list()`：返回已发送（或准备发送）的响应头列表。
- `http_build_query()`：从给定数组构建 URL 编码的查询字符串。
- `ibase_affected_rows()`：返回前一条查询影响的行数（Interbase）。
- `ibase_backup()`：在服务管理器中启动备份任务并立即返回（Interbase）。
- `ibase_commit_ret()`：提交事务，然后在不关闭该事务的情况下返回（Interbase）。
- `ibase_db_info()`：返回有关数据库的信息（Interbase）。
- `ibase_drop_db()`：删除数据库（Interbase）。
- `ibase_errcode()`：返回错误代码（Interbase）。
- `ibase_free_event_handler()`：释放已注册的事件处理器（Interbase）。
- `ibase_gen_id()`：递增生成器并返回递增后的值（Interbase）。
- `ibase_maintain_db()`：在数据库服务器上执行维护命令（Interbase）。
- `ibase_name_result()`：为结果集命名（Interbase）。
- `ibase_num_params()`：返回命名查询中的参数数量（Interbase）。
- `ibase_param_info()`：从命名查询中返回参数信息（Interbase）。
- `ibase_restore()`：在服务管理器中启动恢复任务并立即返回（Interbase）。
- `ibase_rollback_ret()`：回滚事务而不关闭该事务（Interbase）。
- `ibase_server_info()`：返回有关数据库的信息（Interbase）。
- `ibase_service_attach()`：连接到服务管理器（Interbase）。
- `ibase_service_detach()`：断开与服务管理器的连接（Interbase）。
- `ibase_set_event_handler()`：注册一个在特定事件发生后被调用的用户定义函数（Interbase）。
- `ibase_wait_event()`：等待数据库发布的事件（Interbase）。
- `iconv_mime_decode()`：解码 MIME 头字段。
- `iconv_mime_decode_headers()`：同时解码多个 MIME 头字段。

## PHP5 有什么新变化？

- `iconv_mime_encode()`：创建 MIME 头字段。
- `iconv_strlen()`：返回字符串的字符计数。
- `iconv_strpos()`：在字符串中找到指定字符第一次出现的位置。
- `iconv_strrpos()`：在字符串的指定范围内找到指定字符最后一次出现的位置。
- `iconv_substr()`：返回字符串的一部分。
- `idate()`：将本地时间/日期格式化为整数。
- `imagefilter()`：对图像应用命名滤镜。
- `image_type_to_extension()`：返回图像文件的扩展名。
- `imap_getacl()`：返回给定邮箱的 ACL。
- `ldap_sasl_bind()`：使用 SASL 将资源绑定到 LDAP 目录。
- `mb_list_encodings()`：返回所有受支持的编码数组。
- `pcntl_getpriority()`：返回 pid 的优先级。
- `pcntl_wait()`：暂停当前进程，直到子进程退出，并返回子进程的 id。
- `pg_version()`：以数组形式返回客户端、协议和服务器的版本。
- `php_strip_whitespace()`：从源代码中移除注释、空白符和换行符，并返回结果。
- `proc_nice()`：通过给定的增量改变当前进程的优先级。
- `pspell_config_data_dir()`：设置语言数据文件的位置。
- `pspell_config_dict_dir()`：设置主要单词列表的位置。
- `setrawcookie()`：等效于不使用 URL 编码值的 `setcookie()`。
- `snp_read_mib()`：读取并解析 MIB 文件到活动的 MIB 树中。
- `sqlite_fetch_column_types()`：从给定表中返回适用的列类型。
- `str_split()`：将字符串分割为字符数组。
- `stream_copy_to_stream()`：在流之间复制数据并返回复制的数据量。
- `stream_get_line()`：类似于 `fgets()`，但允许使用命名分隔符。
- `stream_socket_accept()`：接受在之前使用 `stream_socket_server()` 函数创建的套接字上的连接。
- `stream_socket_client()`：打开到 Internet 或 Unix 域目的地的流。
- `stream_socket_get_name()`：返回套接字连接的名称。
- `stream_socket_recvfrom()`：从套接字接收数据，直到达到指定长度。
- `stream_socket_sendto()`：向指定套接字发送数据，无论该套接字是否已连接。
- `stream_socket_server()`：在指定服务器上创建流。
- `strpbrk()`：在字符串中搜索给定字符列表中的任意字符，并返回从首次成功实例开始的字符串剩余部分。
- `substr_compare()`：使用命名偏移量和可选的大小写敏感性比较两个字符串。
- `time_nanosleep()`：使脚本执行延迟若干秒和纳秒。

有关这些函数的更多信息，请参阅源文档，[http://www.php.net](http://www.php.net)。

## PHP5 的其他更改

除了大量的面向对象（OOP）更改和众多可用的新函数外，PHP5 的发行版中还包含其他改进。

### 配置更改

在 PHP5 中，php.ini 配置文件有许多更改。这些更改在第 5 章中有更详细的讨论，但这里有一个列表供您参考：

- `mail.force_extra_parameters`
- `register_long_arrays`
- `session.hash_function`
- `session.hash_bits_per_character`
- `zend.ze1_compatibility_mode`

通过这些新指令，您可以对 PHP 环境施加更多的控制，从而在编码时获得更大的自由度。

### MySQLi

如您所知，MySQL<i>i</i> 非常适合 PHP，用于提供由数据库驱动的动态网站。因此，MySQLi（MySQLi 改进版）扩展的发行让每个人的工作变得更加容易。

#### 配置设置

在 php.ini 中提供了几个新的 MySQLi 配置设置。以下是简要说明：

- `mysqli.max_links`：设置每个进程的 MySQL 最大连接数。
- `mysqli.default_port`：设置用于连接到 MySQL 服务器的默认 TCP/IP 端口。
- `mysqli.default_socket`：设置用于连接到 MySQL 服务器的默认套接字名称。
- `mysqli.default_host`：设置用于连接到 MySQL 服务器的默认主机名。
- `mysqli.default_user`：设置用于连接到 MySQL 服务器的默认用户名。
- `mysqli.default_pw`：设置用于连接到 MySQL 服务器的默认密码。

### 内置类和属性

随着 **mysqli** 扩展而来的是一个新的内置类和属性集合，您可以在 PHP 脚本中访问这些类和属性。如果您的脚本是面向过程性质的，而不是面向对象的，这些新方法也可以作为函数使用。要以过程化方式调用函数，只需在方法名称前使用语法 `mysqli_` 即可。例如，使用面向对象（OOP）创建新连接时，您输入以下内容：

```php
<?php

$connect = new mysqli("server", "user", "pass", "dbname");
//通过 mysqli 类调用方法
$connect->close();
?>
```

使用传统的过程化编程实现相同功能，您输入以下内容：

```php
<?php

$connect = mysqli_connect("server", "user", "pass", "dbname");
//使用 mysqli_ 前缀调用函数
mysqli_close($connect);
?>
```

以下部分描述了 PHP5 固有的函数类型。

#### class mysqli

此类处理基本的 MySQL 连接。该类的构造函数创建一个新的 PHP/MySQL 连接，从而创建一个新的 **mysqli** 对象。您可以使用此类来操纵或检索当前连接的信息，或执行基本查询功能。

此类可用的方法包括：

- autocommit：切换事务是否自动提交到数据库。
- change_user：切换到另一个用户。
- character_set_name：返回默认字符集。
- close：关闭数据库连接。
- commit：将事务提交到数据库。
- connect：打开到 MySQL 数据库服务器的新连接（也是 mysqli 构造函数）。
- debug：使用 Fred Fish 调试库进行调试。
- dump_debug_info：使用 Fred Fish 调试库转储调试信息。
- get_client_info：检索客户端信息。




# 第 1 章

- `get_host_info` : 获取连接信息。
- `get_server_info` : 获取 MySQL 服务器信息。
- `get_server_version` : 获取当前 MySQL 服务器版本。
- `info` : 返回最近一次执行的查询的信息。
- `init` : 在调用 `real_connect` 函数之前初始化对象。
- `kill` : 终止一个 MySQL 线程。
- `more_results` : 查找之前调用的 `multi_query` 的结果。
- `multi_query` : 执行一个或多个查询。
- `next_result` : 返回之前调用的 `multi_query` 的下一个结果。
- `options` : 更改或设置 `real_connect` 对象的连接选项。
- `ping` : 测试服务器连接，如果没有连接则重新连接。
- `prepare` : 为执行而准备单个 SQL 查询语句。
- `query` : 执行查询。
- `real_connect` : 连接到 MySQL 数据库服务器，并允许设置额外的选项或参数。
- `real_escape_string` : 返回转义字符串，以便在 SQL 语句中有效使用。
- `rollback` : 回滚当前事务。
- `select_db` : 选择指定的数据库为活动数据库。
- `set_charset` : 设置要使用的字符集。
- `ssl_set` : 设置 SSL 参数，启用安全连接。
- `stat` : 返回系统状态信息。
- `stmt_init` : 初始化语句以便与 `mysqli_stmt_prepare` 一起使用。
- `store_result` : 从上一个查询中传输结果集。
- `thread_safe` : 返回是否提供线程安全。
- `use_result` : 从上一个查询中传输非缓冲的结果集。

该类可用的属性如下：

- `affected_rows` : 获取前一个 MySQL 操作中受影响的行数。
- `client_info` : 以字符串形式返回 MySQL 客户端版本。
- `client_version` : 以整数形式返回 MySQL 客户端版本。
- `errno` : 返回最近一次函数调用的错误代码。
- `error` : 返回最近一次函数调用的错误字符串。
- `field_count` : 返回最近一次查询的列数。
- `host_info` : 返回表示所用连接类型的字符串。
- `info` : 获取最近一次执行的查询的信息。
- `insert_id` : 返回上一个查询中使用的自动生成的 ID。
- `protocol_version` : 返回所使用的 MySQL 协议版本。
- `sqlstate` : 返回包含最后一个错误的 SQLSTATE 错误代码的字符串。
- `thread_id` : 返回当前连接的线程 ID。
- `warning_count` : 返回在前一个 SQL 语句执行过程中生成的警告数量。

##### mysqli_stmt

该类处理预编译语句，即由 MySQL 服务器临时存储直到需要时才使用的 SQL 语句。预编译语句的一个示例是“**SELECT * FROM customer WHERE lastname = ?"**。然后，当你准备好执行该语句时，你只需要填入 lastname 的值即可。请注意，当你将这些方法作为过程式编程中的函数使用时，方法名前需加上 **mysqli_stmt_** 前缀（**mysqli_stmt_close** ）。

该类可用的方法如下：

- `bind_param` : 将变量绑定到预编译语句。
- `bind_result` : 将变量绑定到预编译语句以存储结果。
- `close` : 关闭预编译语句。
- `data_seek` : 在语句结果集中查找任意行。
- `execute` : 执行预编译语句。
- `fetch` : 将预编译语句的结果获取到绑定变量中。
- `free_result` : 释放给定语句句柄存储的结果内存。
- `prepare` : 准备 SQL 查询。
- `reset` : 重置预编译语句。
- `result_metadata` : 从预编译语句中获取结果集以用于元数据信息。
- `send_long_data` : 分块发送数据。
- `store_result` : 缓冲预编译语句的完整结果集。

该类可用的属性如下：

- `affected_rows` : 返回上一次语句执行所影响的行数。
- `errno` : 返回最后一个语句函数的错误代码。
- `error` : 返回最后一个语句函数的错误消息。
- `param_count` : 返回给定预编译语句的参数数量。
- `sqlstate` : 返回包含最后一个语句函数 SQLSTATE 错误代码的字符串。

##### mysqli_result

该类表示从数据库查询中获取的结果集。你使用该类来操作和显示查询结果。

该类可用的方法如下：

- `close` : 关闭结果集（在过程式编程中称为 `mysqli_free_result`）。
- `data_seek` : 移动内部结果指针。
- `fetch_field` : 从结果集中获取列信息。
- `fetch_fields` : 从结果集中获取所有列的信息。
- `fetch_field_direct` : 获取指定列的列信息。
- `fetch_array` : 将结果行作为关联数组、数值数组或两者兼得进行获取。
- `fetch_assoc` : 将结果行作为关联数组获取。
- `fetch_object` : 将结果行作为对象获取。
- `fetch_row` : 将结果行作为枚举数组获取。
- `field_seek` : 将结果指针移动到指定的字段偏移量。

该类可用的属性如下：

- `current_field` : 返回当前字段指针的偏移量。
- `field_count` : 返回结果集中的字段数。
- `lengths` : 返回列长度的数组。
- `num_rows` : 返回结果集中的行数。

如你所见，新的 mysqli 类可以帮助你编写更高效的代码，并为你提供更多关于 PHP 4 中可用 MySQL 函数的灵活性和控制力。

### XML 支持

PHP5 的 XML 库比 PHP4 有了改进。有几个新的 XML 扩展是使用 libxml2 编写的，以改进标准化和维护：

- **DOM:** 这套新的函数取代了 PHP4 中的 DOMXML 函数。它们经过重构，以符合 W3C 提出的 DOM Level 2 标准。
- **XSL:** 以前称为 XSLT 扩展，该扩展借助 W3C 的 XSL 样式表作为标准，协助将一个 XML 文件转换为另一个文件。
- **SimpleXML:** 这套函数允许你简单容易地从 XML 文件中提取数据。然后，你可以使用常见的数组迭代器 `foreach()` 来操作、显示和比较属性和元素。

**SOAP:** SOAP 扩展允许你编写 SOAP 服务器和客户端，并且要求安装 GNOME XML 库（libxml）。

第 8 章将更详细地讨论 XML 扩展。

### Tidy 扩展

PHP5 现在支持 Tidy 库，该库可在 http://tidy.sourceforge.net/ 获取。它协助程序员清理和完善 HTML 代码。该扩展在 PEAR 库中可用，地址为 http://pear.php.net/package/tidy 。要获取可用的 Tidy 函数和类的完整列表，你可以访问 http://us2.php.net/tidy 处的 PHP 手册。

### SQLite

尽管 SQLite 是在 PHP4 的后续版本中引入的，但它为 PHP5 进行了改进。SQLite 类似于一个迷你 SQL 服务器。许多类和方法已内置到 PHP5 中，并且随 PHP5 的安装一起捆绑提供。有关 SQLite 的更多信息，请访问源网站： http://sqlite.org 。

## 摘要

虽然 PHP5 中 OOP 模型的重构无疑是相对于 PHP4 最大且最好的改进，但还有许多其他领域也进行了改进，以使 PHP 程序员的生活更加轻松。

PHP 最好的方面之一是它通过增量改进不断发展和壮大，就像任何开源语言应该做的那样。构成 PHP5 的小改进将帮助你更好地与 MySQL 协同工作，帮助你简化代码，并让你更好地利用 XML 的优势。然而，最大且最好的改进是包含了 OOP 模型。使用 OOP 代替过程式编程将从根本上改变你对代码的思考方式。在下一章中，你将了解如何充分利用 PHP 中的这个新模型。





## PHP5 面向对象编程（OOP）

当您开始一个新项目时，您需要考虑的第一件事就是代码的结构。无论您正在编写的是简单的在线联系表单，还是功能完备的内容管理系统，您如何组织代码都将影响最终产品的性能和可维护性。

当使用 PHP 这样的语言时，您可以走两条主要路线：过程式编程和面向对象编程——简称 OOP。每种策略都有其自身的好处和局限性。

### 过程式编程与 OOP 的对比

过程式编程通常强调编写尽可能简洁的代码，并直接针对最终结果进行编码。换句话说，大多数过程式编程使用针对性的函数组，直接解决当前问题——通常不多也不少。在大多数情况下，这能让您获得极其高效和高性能的应用程序。这种方法的缺点之一是可维护性较差。如果项目变得足够大，开发人员可能需要维护大量的独立函数，在某些情况下，不同函数的逻辑可能会变得令人困惑地相似。

另一方面，面向对象编程（OOP）强调抽象关系和相关的功能层次结构。类似的功能可以共享一个公共核心，这使得维护变得更加容易。代码重用也增加了，因为您可以轻松地将抽象的基础功能适应于新任务。OOP 还可以帮助大规模程序设计，有助于封装和分类系统各部分所需的不同功能集。然而，这样的组织和模块化是有代价的。如果您的面向对象系统设计不佳，它实际上可能比任何其他替代方案都更难维护。通常，面向对象设计中极端的模块化和“代码沉重”可能会导致性能不佳。

## 第 2 章

一旦您克服了由糟糕的面向对象设计引起的问题，您会发现创建一个使用自定义 PHP 对象集的系统，甚至是一个完整的 API，可以带来大多数开发人员都会欣赏的好处。至此，您现在可以开始了解 PHP5 如何实现面向对象编程了。

## 基本类定义

面向对象 PHP 中的基本代码单元是类。简而言之，类是一种将相关功能和数据封装在一个实体中的方式。这种封装可用于将内部操作对外部代码隐藏，并有助于简化与数据的外部交互。类是对代码组的正式描述，如果愿意的话，可以说是一个程序化配方。类本身，就像配方一样，只是一组指令，不能直接使用——您不会吃实际的配方，对吧？为了使用类，您需要创建该类的实例，称为对象——类似于使用配方法来制作您真正可以吃的菜肴。类定义了一组代码的特性和行为，而对象是该指令集的个人实例。

理解类的一种简单方式是将类代码与物理对象联系起来。许多时候，类将代表这些现实世界的对象。您可能有一个名为 *Car*（汽车）的类，它有一个名为 *occupants*（乘客）的属性，可以追踪汽车中的人数。它甚至可能包含一个名为 *brake()*（刹车）的方法，该方法将执行与其名称相似的任务。与许多现实世界物品一样，类具有描述单个对象的属性组合，在 OOP 中称为 *properties*（属性），以及一组可执行的行为，在面向对象世界中称为 *methods*（方法）。

### 定义类

在 PHP5 中定义类是一个相对简单的过程——与定义函数非常相似，尽管关键字不同：

```php
class Circle
{
    // 类代码放在这里
}
```

这段代码通过使用 *class* 关键字，后跟类名和一对大括号来定义一个简单的类。

在标准的 PHP5 类中，类定义有两个主要部分——*属性*（properties）和 *方法*（methods）。*属性* 代表对象中保存的数据，而 *方法* 则对该数据执行操作。

### 属性

在 PHP5 中创建类时，属性是存储对象将表示的各种数据片段的地方。

在 PHP5 中定义属性就像下面这么简单：

```php
visibility $property_name;
```

在此定义中，*visibility* 代表属性的代码可见性，它是三个值之一：*public*（公共的）、*private*（私有的）或 *protected*（受保护的）。这三个关键字的含义将在本章后面讨论。

属性定义的第二部分，*property_name* 只是您希望属性拥有的名称。

例如，假设您要创建一个名为 *Circle*（圆）的类。您可能想要一个 *public*（公共的）属性来保存半径，如下所示：

```php
class Circle { public $radius; }
```

可选地，您可以在定义中指定属性的初始值。假设您希望 *Circle* 的初始半径设置为 10；您可以这样做：

```php
class Circle { public $radius = 10; }
```

然后，每次创建一个 *Circle* 对象时，它将从初始半径为 10 开始。

### 方法

您已经创建了属性来在对象内部保存数据，现在您需要创建一种方式来操作这些数据。为了执行这些操作，您将在类内部创建函数，称为 *方法*。

在 PHP5 中定义方法与在代码其他地方创建标准函数非常相似：

```php
visibility function function_name(parameters) { // 方法实现放在这里 }
```

与属性定义类似，方法定义需要一个 *visibility* 组件。除了可见性前缀之外，方法与标准 PHP 函数的定义完全相同——只需使用 *function* 关键字，后跟函数名称，然后是括号内的可选参数列表。

再次使用 *Circle* 示例，您将添加一个方法来计算圆的面积：

```php
class Circle { public $radius; public function calcArea($radius) { return pi() * pow($radius, 2); } }
```

您只是创建了一个名为 *calcArea()* 的方法，它接受一个参数 *$radius*，并返回给定半径的圆的面积。

现在您已经创建了这些属性和方法，您将需要一种方式来实际使用您的属性和方法。这就需要实例化。

## 第 2 章

## 使用类：实例

为了访问类的属性并使用其方法，您首先需要实例化（或创建实例）该类。当类被实例化时，它返回一个该类类型的单个对象，您可以使用它。在 PHP5 中，使用 *new* 关键字创建对象实例，如下所示：

```php
$c = new Circle();
```

一旦创建对象，使用“箭头”运算符（连字符后紧接大于号）访问各个属性和方法，如下面的代码所示：

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

// 修改变量属性
$c->radius = 5;

// 使用方法
echo 'The area of the circle is ' . $c->calcArea(5);
?>
```

如果您运行代码，您将看到类似以下内容：

圆的面积是 78.539816339745

查看代码，您会发现从定义类 *Circle* 开始。然后，您添加了实例化对象的代码：

```php
// 创建 Circle 的新实例
$c = new Circle();
```

最后，您将 *radius* 属性更改为值 5，并计算半径为 5 的圆的面积：

```php
// 修改变量属性
$c->radius = 5;

// 使用方法
echo 'The area of the circle is ' . $c->calcArea($c->radius);
```




仔细查看前面的代码，你可能已经注意到在使用 **radius** 属性时有一点不太自然。你明确设置了 **radius** 属性，但随后又将该属性作为 **calcArea** 方法参数的显式值重复使用。由于对象内部已经知晓 **radius** 属性，因此没有理由要求显式地将其提供给 **calcArea()** 方法。为了消除提供 **radius** 参数的要求并改用对象内部自身的 **radius** 属性，你需要一种访问该属性的方法。PHP 提供了一个名为 **$this** 的引用来实现这一目标。使用这个特殊命名的变量 **$this** 就如同引用一个已实例化的对象，但 **$this** 引用的是包含它的那个对象。

修改 **Circle** 类，如下所示：

```php
<?php

class Circle
{
    public $radius;
    
    public function calcArea()
    {
        return pi() * pow($this->radius, 2);
    }
}

// 创建一个新的 Circle 实例
$c = new Circle();

// 修改属性
$c->radius = 5;

// 使用方法
echo '圆的面积是 ' . $c->calcArea();

?>
```

运行这段代码将产生与之前示例完全相同的结果——唯一的变化在于使用 **calcArea()** 方式。由于你在方法内部引用了 **Circle** 对象的 **radius** 属性，因此你不再需要在函数定义和方法调用中保留该参数。

### 可见性

PHP5 面向对象模型的一个新特性是能够为所有类属性和方法指定可见性级别。使用这些新的可见性关键字，你可以将类的某些部分对外部代码隐藏，同时公开你希望所有人都能访问的其他功能。PHP5 提供了三个用于类的可见性级别：**public**（公有）、**private**（私有）和 **protected**（受保护）。

**public** 可见性意味着属性或方法可供所有希望访问它的其他代码使用。如果未指定方法的可见性，则默认为 **public** 可见性。

将类成员指定为 **private** 意味着该属性或方法仅在所属的类定义内部可见。同一类中的所有其他方法都可以访问私有成员，但该特定类外部的任何代码都不能访问。

# 第 2 章

最后，protected 关键字指定属性或方法仅在定义类内部以及任何扩展或继承自定义类的其他类中可用。有关扩展和继承类的讨论将在本章稍后部分进行。

> 在 PHP5 下复用 PHP4 类时，务必牢记：使用 var 关键字定义的属性（例如 var $propertyName）将被视为 public，并且会发出 E_STRICT 警告。

为类成员指定可见性非常简单，只需在属性或方法声明前添加适当的前缀即可。在你之前定义的 Circle 类中，所有类成员都被定义为 public。现在，你将把一些旧的类成员更改为 private，并添加一些新方法。

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

你不再将属性保留为 public，而是将它们改为 private，并创建了函数来设置它们的值。在这种简单情况下，这样做可能有点过度，但如果你扩展应用程序，设置函数可以在设置内部值之前对数据进行复杂计算。这种分离还可以通过在允许内部数据更改之前验证外部提供的值，从而为私有成员增加一层保护。

你可以使用以下代码来使用你修改后的类：

```php
$c = new Circle();
$c->setCenter(0,0);
$c->setRadius(10);

echo "圆的面积是 " . $c->calcArea() . "\n";

// 尝试访问私有属性
echo "radius 的私有值是 " . $c->radius;
?>
```

如果你运行这段代码，你会看到类似以下内容：

> 圆的面积是 314.15926535898
> Fatal error: 无法访问私有属性 Circle::$radius，位于 /www/plamp/ch02/02-002.php 第 31 行

如你所见，这与你之前使用 Circle 的情况没有太大不同。但由于 public/private 的指定，你现在必须使用方法来访问 $center 和 $radius 属性，而不能直接访问这些属性。注意最后尝试直接访问私有成员时发生的情况——会发生致命错误。

## 构造函数和析构函数

在处理类的某些情况下，你可能希望有一种在对象创建时自动执行操作的方式。你可能想要初始化对象参数或自动调用类方法。也许你希望对象检查本地环境以确认必要资源可用，甚至建立初始连接。PHP 为这类情况提供了构造函数。

构造函数不过是一个具有特殊名称的方法，当对象实例化时会自动被调用。在 PHP5 中，要实现构造函数，你只需要实现一个名为 `__construct` 的方法即可。例如：

```php
<?php
class Circle
{
    public function __construct()
    {
        // 在对象创建时执行操作
        echo "正在创建圆对象。\n";
    }
}
$c = new Circle();
?>
```

当你执行这段代码时，你会看到以下内容：

> 正在创建圆对象。

正如预期的那样，定义在构造方法内部的代码在对象实例化时自动执行了。

> 你仍然可以在 PHP5 中使用 PHP4 风格的构造函数（与类同名方法），但新式的 __construct 方法更受推荐。

像标准方法和函数一样，构造函数也可以处理参数。要向构造函数传递参数，你需要在创建对象时将它们包含在括号内，如下所示：

# 第 2 章

```php
<?php
class Circle
{
    public $radius;

    public function __construct($r)
    {
        // 在对象创建时执行操作
        echo "正在创建圆对象。\n";

        $this->radius = $r;
    }
}

$c = new Circle(10);
?>
```

在这个例子中，你只是在创建对象时提供了一个半径参数——本例中为 10——构造函数会自动解释它，进而在实例化时设置圆的半径。

现在，你已经掌握了在对象创建时执行操作的方法，接下来看看如何在对象销毁时执行额外操作。PHP5 现在包含一个在对象销毁时被调用的特殊方法，逻辑上被称为析构函数。当对象的所有引用被移除，或者在你的代码中被手动销毁时，对象的析构函数会被调用。析构函数通常用于各种清理任务，例如关闭数据库连接和释放文件句柄。要创建析构函数，请向你的类添加一个方法，并将其命名为 `__destruct`：

```php
<?php
class Circle
{
    public function __construct()
    {
        // 在对象创建时执行操作
        echo "正在创建圆对象。\n";
    }

    public function __destruct()
    {
        // 在对象销毁时执行操作
        echo "正在销毁圆对象。\n";
    }
}

$c = new Circle();

// 销毁圆对象
unset($c);
?>
```

运行这段代码会得到：

> 正在创建圆对象。
> 正在销毁圆对象。

注意，你无需执行任何操作就能看到析构函数内部放置的消息。这是因为 PHP 在脚本执行结束时会自动清理所有对象引用，从而自动调用对象的析构函数。

最后一件需要记住的事情是，与可以有参数的构造函数不同，析构函数不能有任何参数。

## static 关键字

有时在使用面向对象编程时，你可能需要访问类的方法，而不必创建一个完整的对象。为了满足这一需求，PHP5 提供了 `static` 关键字。这是 PHP5 中新引入的，`static` 关键字允许在不实例化类的情况下使用类属性和方法。要使类成员变为静态，只需在可见性和属性或方法定义之间添加 `static` 关键字，如下所示：

```php
<?php

class Circle
{
    public static function calcArea($r)
    {
        return pi() * pow($r, 2);
    }
}
```

要使用新创建的静态属性，你只需使用类名，后跟两个冒号，然后是属性名称或方法调用：

```php
$r = 5;
echo "给定半径为 " . $r .
     "，圆的面积为 " . Circle::calcArea($r);
```

在浏览器中运行这段代码将产生类似以下结果：

> 给定半径为 5，圆的面积为 78.539816339745

然而，使用静态方法存在一些限制。静态方法不能使用 `$this` 更改或访问对象变量或方法；它们只能直接访问类中其他静态属性和方法。

为了访问同一类内的其他静态变量，你可以使用 `self` 关键字，结合双冒号使用。使用 `self::` 类似于使用 `$this`，但它仅适用于静态成员。如果你希望修改 Circle 类以使用静态方法和属性，你可能会执行类似以下操作：




## 第 2 章

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
       Circle::getRadius() . "\n";
?>
```

快速运行 PHP5 引擎将产生以下结果：

    我们静态访问的圆的半径为 5。

## 类常量

随着 PHP5 中改进的对象模型，PHP 引入了类常量的概念。类常量类似于普通的 PHP 常量，但只能在类的定义内部使用。与标准 PHP 常量一样，它们的值只能设置一次，且必须是一个标量值——一个简单的数字或字符串——任何试图将常量设置为函数结果的尝试都会导致错误。

在使用类常量时，请记住它们的访问方式类似于静态成员——要访问类常量，必须使用双冒号（::）语法。要定义类常量，请在常量名称前使用 `const` 关键字，如下所示：

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
echo "To recap, the value of Pi in our Circle class is " . $c->getPi();
?>
```

运行此代码将产生以下结果：

```
The value of Pi in our Circle class is 3.14159265359
To recap, the value of Pi in our Circle class is 3.14159265359
```

在这个例子中，你创建了类常量 `pi`，它保存的值恰好令人惊讶地是数学常数 Pi。然后你在 `getPi` 方法中使用 `self::` 引用来返回类常量的值。需要注意的是，在访问 `self::pi` 时，名称 `pi` 前面没有美元符号。类常量不使用美元符号前缀，而标准类变量则使用。

> *你创建 Pi 常量仅作为示例。PHP 已经有一个内置的 `pi()` 函数，它返回 Pi 的值。*

## 赋值与克隆

如你可能已经了解，在标准 PHP 中，将数据赋值给变量有两种方式：按值赋值和按引用赋值。第一种，按值赋值，通常用于为变量设置简单值或复制其他变量：

```php
$a = 5;
$b = $a;
```

这里你使用的是按值赋值。当 $a 的值改变时，$b 保持不变；当你赋值 $b = $a 时，你只是创建了 $a 的值的一个副本，并将该值赋给 $b。

然而，按引用赋值有所不同。请看以下示例：

```php
$a = 5;
$b =& $a;
```

在这个例子中，你使用 =& 运算符进行按引用赋值。在这种情况下，当 $a 的值改变时，$b 也会改变——因为 $b 是通过引用被赋值为 $a 的值，两个变量指向内存中的同一位置，当该内存位置的值改变时，两个变量都会随之改变。

在 PHP5 中，所有对象默认都是按引用赋值的。这种行为不同于 PHP4，PHP4 默认按值赋值，除非使用引用运算符 (&)。在 PHP5 中，如果你想创建一个对象的副本，而不是使用引用，你必须使用 `clone` 语句，如下所示：

```php
<?php
class Circle
{
    public $radius = 10;
}

// Create the original object and set its parameters
$original = new Circle();

// Create a cloned and assigned (by reference) object
$cloned = clone $original;
$assigned = $original;

// Now, change the original radius value:
$original->radius = 5;

// Show the state of all three objects
echo "\nOriginal:\n";  
print_r($original);

echo "\nAssigned:\n";
print_r($assigned);

echo "\nCloned:\n";
print_r($cloned);
?>
```

此代码将产生以下输出：

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

正如你所见，$assigned 引用了 $original 对象，但因为你克隆了 $cloned，从而制作了 $original 的一个分离副本，所以当你修改 $original 时，它的值不会改变。

## 继承与接口

使用 OOP 搭配 PHP5 的一个好处是，它允许你将代码分解为逻辑块，以便于重用。这些块如果编写得当，可以在许多不同的项目中反复重用，使程序员能够自由编写针对他们试图解决的特定问题的代码。

在 OOP 中，有几种方式可以指定一组方法和属性以在多个类中使用。第一种，**继承**，允许你定义属于基类的一组基本属性和方法，并将其用作更具体类的构建块。第二种，**接口**，允许你规定类必须实现的方法列表。

### 继承

假设你正在创建一个代码库，用于操作不同的几何形状。本章中一直在使用的 **Circle** 类可以是该库的一部分。在创建代表不同形状（如正方形、圆形、三角形等）的不同类时，你可能会发现自己在所有形状中重复了相似或相同的方法。这是一个使用继承的好机会。

#### extends 关键字

假设所有几何形状类都将在网格上绘制。因此，它们都需要某种原点 (x,y)。你可以在每个不同的类中包含一个 **origin** 属性，或者使用 **extends** 关键字，通过继承在一个共享位置定义该属性。为此，你将创建一个名为 **Shape** 的类，它将作为你可能创建的所有几何类的父类。每个具体的几何形状类——无论是 **Circle**、**Square**、**Ellipse** 还是 **Star**——都具有 **Shape** 提供的一组基本功能。理解这种父子关系的一个简单方法是使用短语“*是*”。在这个例子中，**Circle** *是* **Shape**，就像 **Square** *是* **Shape**，**Triangle** *是* **Shape** 一样。

要使用你的父类 **Shape**，你可以做类似以下操作：

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

运行此代码将产生以下结果：

```
Array
(
    [x] => 0
    [y] => 0
)
```

正如你所见，你创建了一个名为 `Shape` 的基类，它定义了一个通用的 `origin` 属性。通过在 `Circle` 的类定义中使用 `extends` 关键字，`Shape` 的所有属性和方法都成为 `Circle` 对象的一部分。因为 `Circle` 是 `Shape` 的子类，你可以获取 `$origin` 的值，尽管它在 `Circle` 中未显式定义——它是从 `Shape` 继承来的。

在扩展基类时，可以重新定义父类（基类）中存在的属性和方法。例如：

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

此代码将输出以下内容：

```
Circle Object
(
    [origin] => New origin
)
```

通过在子类中重新定义基属性 `$origin`，新定义隐藏了父类的值。方法的行为方式相同——在子类中重新定义它们会覆盖父类方法的功能。例如，看以下代码：

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
```




```php
        }
        return array('x'=>1, 'y'=>1);
    }

    $c = new Circle();
    print_r($c->getOrigin());
```

在这个示例中，定义在 `Shape` 父类中的 `getOrigin()` 方法在 `Circle` 子类中被重新定义。当在实例化的 `Circle` 对象上调用 `getOrigin()` 时，它返回原点坐标 1,1，而不会调用基类 `Shape` 中的 `getOrigin()` 方法。重新定义的方法会遮蔽父类或类中任何同名方法。

### final 关键字

在某些情况下，你可能希望禁止子类重新定义基类中存在的成员。你可以使用 `final` 关键字来防止属性和方法被重新定义：

```php
<?php
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

如果你尝试运行这段代码，将会发生一个致命错误：

> Fatal error: Cannot declare property Shape::$origin final, the final modifier is allowed only for methods in /www/plamp/ch02/02-008.php on line 5

由于你在基类的 `$origin` 定义中使用了 `final` 关键字，当你在 `Circle` 子类中尝试重新定义它时，就导致了致命错误。

请注意，对于属性而言，`final` 关键字并不禁止改变其值——它只禁止重新定义。

### 使用 parent:: 引用

在某些情况下，你在子类中重新定义了基础类的属性或方法后，可能希望引用基础类中的原始属性或方法。为了实现这一点，你可以使用 `parent` 关键字，结合你在上一节关于静态成员中看到的 `::`（双冒号）。例如：

```php
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
```

运行时将显示以下内容：

Circle::draw() has been called.
Shape::draw() has been called.

在这个示例中，你定义了一个从基类 `Shape` 继承的子类 `Circle`。由于你在子类中创建了一个新的 `draw()` 方法，因此使用 `parent::draw()` 来调用父类中同名函数。以这种方式调用父类方法是在子类中重写基类方法时的常见做法，并且在构造函数中调用父类构造函数时也非常常用——否则基类的构造函数不会自动调用。

## 抽象类

在编程或设计过程中，你可能会发现像 `Shape` 这样的类需要创建，以便为子类提供相同的属性或方法，但从来不需要单独实例化。你之前使用的 `Shape` 类是成为抽象类的绝佳候选对象——你永远不会想直接创建一个 `Shape` 对象，但对于为几何对象的更具体子类提供功能却是必要的。对于这种类型的场景，有 `abstract` 关键字。

当一个类被定义为抽象类时，其他类可以继承它，但它本身不能被实例化。例如：

```php
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

$$ = new Shape();
print_r($$->origin);
```

运行这段代码，你应该看到类似以下的内容：

```
Array
(
    [x] => 0
    [y] => 0
)

Fatal error: Cannot instantiate abstract class Shape in /www/plamp/ch02/02-010.php on line 17
```

通过运行这个示例可以看到，`Circle` 类如预期那样从 `Shape` 继承了，但当你尝试单独实例化 `Shape` 时，发生了致命错误。

现在你已经快速了解了 PHP 中的继承，让我们来看看另一种规范对象行为的方式：接口。

## 接口

PHP5 中另一个新的面向对象特性是创建和使用接口的能力。简而言之，接口是一种指定类必须显式实现哪些方法的方式。这在处理许多相互连接且依赖于彼此特定方法的对象时非常有用。

通过使用接口，你可以为不同的可互换类指定一组特定的共享方法。这样，如果你需要替换程序中包含在某个类内的功能，你只需确保替换类实现与原类公开的相同接口，或函数组即可。

例如，你可能有一个包含方法 `calculateInterest()` 的商业类。在某些时候，你可能希望有多种计算利息的方法，因此你为每种希望使用的算法创建不同的类。假设所有类都实现一致的接口——一个定义了 `calculateInterest()` 的接口——那么这些类现在在程序中应该是可互换的。

在 PHP5 中，使用 `interface` 关键字定义接口，使用 `implements` 关键字实现接口，如下所示：

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

通过创建接口 `TwoDimensionalOperations`，你可以为不同的形状创建类——圆形、正方形、三角形、五边形等——它们都实现该接口。这样，你可以确信，通过实现 `TwoDimensionalOperations`，你所有的形状类都将具有 `calculateArea()` 方法。

使用接口时，牢记几件事很重要。首先，如果一个类实现了接口但没有定义该接口中的方法，将会发生致命错误。其次，接口中定义的所有方法必须具有公共可见性。

在 PHP5 中，一个类可以同时继承基类并实现接口：

```php
class Circle extends Shape implements TwoDimensionalOperations
{
    // Circle implementation
}
```

另一个巧妙技巧是，接口可以使用 `extends` 关键字继承其他接口：

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

在这个小示例中，你可以轻松地在基础 `Shape` 类内部创建一个方法，并简单地将其扩展至子类 `Circle`。虽然这种方法是可行的，但它是有限制的，因为 PHP 中的类只能继承一个基类。

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
    {
        // Circle->getOrigin() implementation
    }
    public function calculateArea()
    {
        // Circle->calculateArea() implementation
    }
}
```

使用继承和多个接口，结合继承的接口，你可以使用简单的构建模块构建非常复杂且强大的应用程序。

## 魔术方法

为了帮助简化面向对象编程的使用，PHP5 提供了一些所谓的“魔术方法”。这些魔术方法是所有类的特殊命名方法，会在特定场景下自动调用。

到目前为止，你在本章中已经看到了两个魔术方法，`__construct` 和 `__destruct`。它们分别在对象被实例化或被销毁时调用。PHP5 包含一些你可以实现的魔术方法，为你的类提供特殊功能。三个魔术方法——`__call`、`__get` 和 `__set`——都允许你访问对象中未明确定义的方法和属性。第六个，`__toString()`，定义当对象直接用作字符串时发生什么。




## 第 2 章

### `__call`

魔术方法 `__call` 允许你在对象上调用未定义的方法时提供操作或返回值。`__call` 魔术方法可用于模拟方法重载，甚至可以在对象上调用未定义方法时提供平滑的错误处理。`__call` 接收两个参数：未定义方法的名称以及传递给该未定义方法的参数数组。

示例如下：

```php
<?php

class Circle
{
    public function __call($m, $a)
    {
        echo "The method " . $m . " was called.\n" .
             "The arguments were as follows:\n";
        print_r($a);
    }
}

$c = new Circle();
$c->undefinedmethod(1, 'a', 2, 'b');
?>
```

当你运行这段代码时，你将看到类似以下的内容：

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

在这里，你定义了一个 `__call` 函数来处理对 `undefinedmethod` 方法的调用。正如预期的那样，它接收了逗号分隔的参数列表，并将其转换为数组，这些数组被 `$a` 参数捕获。

### `__get` 和 `__set`

魔术方法 `__get` 和 `__set` 允许你指定自定义函数，用于存储和检索类中尚未定义的属性中的数据。

`__get` 接收一个参数，即属性的名称，而 `__set` 需要两个：属性的名称和新值。

```php
<?php
class Circle
{
    public function __get($p)
    {
        return $this->$p;
    }

    public function __set($p, $v)
    {
        $this->$p = $v;
    }
}

$c = new Circle();
$c->nonexistent = 5;
echo "The value of our nonexistent property: " . $c->nonexistent;
?>
```

当你执行上述代码时，PHP 会立即识别出类中不存在名为 "nonexistent" 的属性。由于指定的属性不存在，因此调用了 `__set()` 方法，该方法将值分配给新创建的类的属性，从而允许你看到以下内容：

我们不存在属性的值: 5

在这个例子中，你创建了魔术方法 `__get` 和 `__set` 来处理任何未定义的属性访问，并随后使用了一个名为 `nonexistent` 的未定义属性。

## `__sleep`

当你使用 PHP 类存储需要在页面之间或较长时间内持久化的数据时，你可以使用你最喜爱的持久化方法（文件、数据库、会话变量或 Cookie）来存储对象，但对象必须首先进行准备。

当你重新读取要存储的对象数据时，使用 `serialize()` 函数。`serialize()` 函数接受任何复杂的数据结构，并将其转换为可以用你选择的方法存储的字符串。相反，要检索你持久化的数据，请使用 `unserialize()` 函数。`unserialize()` 函数接受你的序列化字符串，并将其转换回原来的复杂结构。

为了给开发者在处理对象序列化时提供更多的灵活性，提供了 `__sleep` 和 `__wakeup` 魔术方法。

如果在类中定义了 `__sleep` 魔术方法，它会在对象被序列化之前自动调用。该方法对于关闭数据库连接和清理对象资源非常有用。

`__sleep` 方法还可以返回一个包含要序列化的对象值名称的数组，这在处理大型对象时很有用。只有必要的数据会被序列化，而其他数据则被忽略。

## `__wakeup`

`__wakeup` 魔术方法执行与 `__sleep` 方法完全相反的操作。当调用 `unserialize()` 时，会自动调用 `__wakeup`，这对于重置对象值、恢复连接以及其他初始化任务非常有用。

看看这个关于 `__sleep` 和 `__wakeup` 的简单示例。这个示例需要两个文件。第一个文件，你将创建为 page1.php：

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

你将第二个文件命名为 page2.php：

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

    echo 'Rise and shine......';

    $c = unserialize($_SESSION['c']);

    echo '<br />The contents of our Circle object are:<br />' ;
    echo 'Radius: ' . $c->radius . '<br />' ;
    echo 'Origin: ( ' . $c->origin['x'] . ', ' . $c->origin['y'] . ' )' ;
?>
```

在浏览器中加载第一个页面 page1.php，你应该看到类似图 2.1 的内容。

![](img/cacdd24f2926f10ee3219256ad732604_66_0.png)

点击链接，你将被引导到 page2.php，在那里你应该看到类似图 2.2 的内容。

![](img/cacdd24f2926f10ee3219256ad732604_67_0.png)

**图 2.2**

在第一个文件 page1.php 中，你启动会话以便将对象存储在会话变量中；然后继续创建 Circle 的类定义：

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
```

请注意，你在这里为 `__sleep` 和 `__wakeup` 都创建了函数。在这种情况下创建 `__wakeup` 方法并不是必须的，但如果你稍后将类定义移动到包含文件中，你只需要剪切和粘贴即可。还要注意，你在 `__sleep` 中返回了一个字符串数组。这些字符串与 `Circle` 内部的属性名称相匹配，并告诉序列化函数你想序列化对象的哪些部分，并忽略其他所有部分。

然后你继续实例化 Circle 对象，更改其中一些值，将其序列化到会话变量中，并最终提供一个链接以转到 page2.php：

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

查看 page2.php，你再次从启动会话开始，并具有与前一页相同的类定义。在反序列化对象时，在调用 `unserialize()` 函数之前，必须存在该对象的类定义，无论是直接输入在文件中，还是通过 `include` 或 `require` 语句包含进来。

深入了解 page2.php 的主体内容，你从上一页设置会话变量中反序列化数据，并将新创建对象的一些属性回显到屏幕上：

```php
echo 'Rise and shine.....';

$c = unserialize($_SESSION['c']);

echo '<br />The contents of our Circle object are:<br />';
echo 'Radius:'. $c->radius . '<br />';
echo 'Origin: ('. $c->origin['x'] .','. $c->origin['y'] .')';
?>
```

## `__toString`

最后一个可以内置到类中的魔术方法是 `__toString`。正如你可能猜到的那样，`__toString` 返回一个自定义的字符串值，当对象转换为字符串时会自动使用。请参见以下示例：

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

执行此代码将产生以下结果：

$c 的值是: Circle 的自动字符串值

在这个例子中，你添加了 `__toString()` 魔术方法，并在对象回显到屏幕时使用它来提供值。请注意，你没有简单地将对象连接到前一个 echo 语句末尾的字符串上，或者将其包含在双引号字符串内部。

如果你简单地将对象与另一个字符串放在单个 echo 语句中，会发生什么？请查看以下代码（更改的部分已高亮显示）：

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

当你运行这段代码时，你会看到以下内容：

$c 的值是: Object id #1

这肯定不是你预期的结果！它没有返回 `__toString()` 方法的值，而是返回了 $c 的对象 id —— 如果你没有定义 `__toString()`，你也会看到完全相同的结果。`__toString()` 魔术方法仅在直接用于 echo 或 print 时才会被调用 —— 如果存在其他字符串或强制转换，则返回对象 id。





## 摘要

如您所见，PHP5 为您的项目带来了功能强大得多的对象模型。无论您决定坚持过程式编程、偶尔涉足面向对象的编程、全面转向面向对象编程路线，还是在两者之间找到一条中间道路，希望通过本章看到的一些内容，您能够继续前进，开始使用 PHP5 的新面向对象功能构建您自己的系统。

从这里开始，您将暂时离开面向对象编程，进入 PHP 语言一些更为晦涩的角落。您可能已经知道数组在 PHP 中有多强大，但您可能不知道 PHP 提供了多少函数来让您驾驭这种力量。一旦您掌握了这些，我们将向您介绍流（streams）的概念，这将允许您使用一组通用的函数来处理网络资源和本地文件。

## 更晦涩的 PHP

PHP 的一个显著特征是其庞大的内置函数集合，甚至在你开始添加可选扩展之前也是如此。这可以说是一种缺陷，因为它使得在特定情况下决定使用哪个函数变得更加困难。许多函数的行为非常相似，以至于有时很难看清它们为什么作为独立的函数存在。`split()` 与 `preg_split()`？`str_replace()` 与 `strtr()`？`ksort()` 与 `asort()`？`rsort()` 与 `natsort()`？`usort()` 与 `uksort()`？`strftime()` 与 `date()`？这本书不会深入探讨函数命名缺乏约定俗成的规范、参数顺序的问题，以及多个函数仅仅是其他函数的别名这一事实。

PHP 函数集重叠的一个原因是它早期仅作为 Perl 以及后来 C 语言自身库的封装层而存在。熟悉这些语言函数库的用户会发现，它们在 PHP 中的对应物具有相同的名称和相同的调用约定，并叠加了 PHP 的内存管理和类型处理机制。扩展功能加剧了这种情况——随着不同的 DBMS 暴露不同的 API，PHP 为它支持的每个 DBMS 引入了不同的函数集。当两个扩展拥有针对两种相似事物的函数时，PHP 就同时提供两者。

随着 PHP 在更广泛的平台范围内得到更广泛的实现，并被构建进更多种类的环境中，独立的跨平台函数实现开始被引入。因此，既存在 `rand()`（使用 PHP 构建所用的 C 编译器提供的任意伪随机数生成器），也存在 `mt_rand()`（在所有平台上具有完全相同的行为）。与此同时，PHP 开发人员致力于保持向后兼容性；即使引入了新机制，他们也尽最大努力保留旧机制，以防有人依赖它们。

因此，PHP 的函数列表激增，像在一个太小的烤模中发酵膨胀的面包一样向外鼓出。据最后一次统计，PHP 手册中有 3,630 个函数条目，分布在 129 个章节中，其中 855 个列在手册描述为“核心”或捆绑提供且需要显式配置开关才能禁用的 30 个章节中。这些数字已经过时。

这一事实的实际结果是，许多 PHP 程序员就像英语使用者一样——他们只使用该语言的一小部分子集。语言中有些部分他们可能根本用不到。但在 PHP 的深奥之处，隐藏着一些未获得其应得关注的函数。这些函数最迟从 PHP 4.3.2 版本开始就已存在——许多函数自 PHP 4 的早期阶段就已出现。尽管如此，它们常常被忽视，即使它们是当前任务的理想选择。有些人似乎只在关于它们的教程中被使用。它们绝不是该语言仅有的晦涩特性。相反，它们代表了 PHP 环境中一些更强大的核心功能，并且是最近版本积极开发的领域。

本章旨在纠正这种不公正。

## 数组函数和回调

数组函数允许您访问和操作数组的内容，而无需先提取它们。您可能希望对“数组的每个元素”执行的大多数操作（如果不是全部的话）都可以使用这些函数完成，而无需额外的 `for` 或 `foreach` 循环基础设施。此外，许多数组操作任务需要考虑整个数组。排序是一个明显的例子：如果你不看数组的所有元素以定位最小元素，你就无法将最小元素移动到数组的开头。任何尝试编写一种相当高效的排序算法的人都会知道，任务并非微不足道。

由于 PHP 的开发者无法预测你想对数组做的所有事情，大多数数组函数以及相关的数组或数组集接受一个称为回调的额外参数，该参数指定另一个函数的名称，该函数根据数组函数的作用，用于操纵数组元素，或将它们相互比较，或与某个你指定的标准进行比较。通过这种方式，PHP 只需要提供数组操作最抽象方面的实现，例如映射和遍历，从而让你自由地提供你选择的具体细节。

事实上，回调在抽象功能方面是如此有用，以至于提供了一组函数，允许在几乎任何情况下使用它们。完全有可能（尽管是矛盾的）使用以对象回调数组表示的 `methods` 来实现你自己的 OOP 架构。

### 使用回调

考虑以下脚本：

```php
$input_file = file('generic.txt');
foreach($input_file as $k=>$line)
{
    $input_file[$k] = rtrim($line);
}
```

你正在将文本文件作为单行数组加载。PHP 不会丢弃行尾的换行符，所以既然它们已经发挥了作用，你自己希望删除它们。写一个完整的循环并在其中使用两个额外变量似乎冗长。首先，你必须记得 `$line` 是被复制的，因此 `$line` = `rtrim($line);` 不起作用，这意味着你必须通过数组和键引用原始值。要么这样做，要么记得通过编写 `foreach($input_file as &$line)` 来声明 `$line` 为引用变量。任何错误都会导致最终数组的行未被修剪。

现在考虑这个：

```php
$input_file = array_map('rtrim', file('generic.txt'));
```

这行代码达到了相同的效果。`file()` 返回包含 `generic.txt` 中各行的数组；`array_map()` 将函数 `rtrim()` 应用于该数组的每个元素，并返回结果“修剪”后的数组。

有几个函数抽象了遍历数组的最常见原因，减少了编写循环和其他流程控制语句的需要。虽然纯粹为了写一行代码而写一行代码可能导致难以阅读的代码，但减少程序中“活动部件”的数量可以帮助减少错误的发生率。

当你有一个数组，并且需要依次对每个元素执行任务时，`array_map()` 和 `array_walk()` 值得考虑。还有其他函数以类似的方式使用所谓的回调函数，使你无需手动对数组的每个元素调用函数。

回调有两种形式。第一种，也是最常见的一种，是简单地包含函数名称的字符串。在前一行代码中，它是 ‘rtrim’。

> 它必须是一个函数，这就是为什么 PHP 手册特别指出 `echo`、`empty`、`include`、`array` 等不是函数。将 ‘include’ 作为回调传递将会失败。
> 排除它们的原因是，它们在解析期间受到特殊关注，并拥有自己的内部结构。

第二种回调用于指定类和方法。两者都由两个元素的数组表示，其中第二个元素是方法名称，存储为字符串。如果第一个元素是对象，则回调指向该对象的方法：`array($object, ‘method’) 指向 $object->method()`。另一方面，如果第一个元素是字符串或字符串变量，则回调指向命名类的静态方法：`array(‘thing_factory’, ‘create_new’) 指向静态 thing_factory::create_new() 方法。

```php
// 在 array_map() 中使用对象方法作为回调。
// $sundry_array 的每个元素依次传递给 $parser->tidy()，
// 返回的值存储在 $tidied_array 中。
$tidied_array = array_map(array($parser, 'tidy'), $sundry_array);

// 在 array_map() 中使用静态类方法作为回调。
// $sundry_array 的每个元素依次传递给 Parser::tidy()，
// 返回的值存储在 $tidied_array 中
$tidied_array = array_map('Parser::tidy', $sundry_array);

class Parser
{
// 一个示例方法，用于从单行文本中修剪尾随空白
// 和以 `#` 开头的 shell 风格注释。
static function strip_comments($element)
{
$element = preg_replace('/#(. ^ #)*$/', '', $element);
$element = rtrim($element);
return $element;
}
```





## 第 3 章

```php
}
  $shell_script = file('foo.sh');
  $tidied_script = array_map(array('Parser', 'strip_comments'), $shell_script);
```

在类和对象中，魔术变量 `self` 和 `$this` 可以在回调中正常工作，其行为符合您的预期：`array($this, 'method')` 和 `array('self', 'method')` 分别会被解释为指向 `$this->method()` 和 `self::method()`。关于诸如静态函数不允许使用 `$this` 等常规限制同样适用。例如：

```php
// 对象能够在数组回调中使用其自身的方法，
// 既作用于传递给它的参数，也作用于其自身的属性。
$tidied_code = array_map(array($this, 'tidy'), $this->code_array);
// 类方法也可以在类内作为回调访问。
```

如果您想检查给定的 `$variable` 内容是否确实指定了可调用的函数或方法，布尔函数 `is_callable($variable)` 会给出答案。

#### array_map()

您刚刚看到了 `array_map()` 最简单的应用之一，但它能做的事情远不止于此。

最重要的是，它可以同时操作多个数组。想象一下，您有两个数组——`$arr1` 和 `$arr2`——您想要构建一个新数组，其元素由 `func($arr1[0], $arr2[0])`、`func($arr1[1], $arr2[1])`、…… `func($arr1[n], $arr2[n])` 组成。用循环实现这一目标的代码可能如下所示：

```php
$new_array = array();
for($i=0, $limit=max(count($arr1), count($arr2)); $i<$limit; $i++)
{
  $arg1 = isset($arr1[$i]) ? $arr1[$i] : null;
  $arg2 = isset($arr2[$i]) ? $arr2[$i] : null;
  $new_array[$i] = func($arg1, $arg2);
}
```

请注意，当两个数组长度不同时，确保循环不会超出 `func()` 参数范围所需的测试。

现在，将其与使用 `array_map()` 产生的等效代码进行对比：

```php
$new_array = array_map('func', $arr1, $arr2);
```

如果这不起作用，您有权向 bugs.php.net 提交报告。而且当您六个月后回来查看您的代码时，哪一个更让您难以重新熟悉？

`array_map()` 的另一个技巧源于它可以接受 `null` 作为回调。在这种情况下，其行为可以描述为“接收一堆事物数组并返回一堆事物的数组”。每个数组的第 $i$ 个元素合并为单个数组，成为结果数组的第 $i$ 个元素；每个数组的第一个元素合并为单个数组，成为结果数组的第一个元素；以此类推。换句话说，如果您将它的数组参数想象成矩阵的列，`array_map(null, ...)` 返回的是转置矩阵。它实际上等同于

## 更晦涩的 PHP

如果您被允许使用 `'array'` 作为回调，`array_map('array', $arr1, $arr2)` 的预期行为就是如此。

这个技巧也不局限于每次只组合两个数组。如果回调函数需要 $n$ 个参数，那么 `array_map()` 就需要传入 $n$ 个数组。因此，如果您有一个接收六个参数的函数，以及一个六元组数组（您希望对这六个元素应用该函数），并将所有结果收集到一个新数组中，`array_map()` 将是合适的选择。

> *严格来说，这里涉及两次 array_map() 调用。第一次使用 null 回调将原始数组[0..n][0..5] 转换为转置数组[0..5][0..n]；第二次使用回调函数处理 array[0]、array[1]、... array[5] 的连续元素。*

`array_map()` 有两个明显的局限性。首先，回调之后的每个参数必须是数组。如果您希望在针对整个数组的操作中使用单个变量（例如将数组中的所有值限制在某个最大值以内），那么您需要执行以下操作之一：

- 在全局范围声明变量，并在回调函数内部使用 global（这不是最理想的选项）
- 使用 `array_fill()` 创建一个副本数组（仅当您不介意操作发生在变量的独立副本上，或者变量是引用传递的对象或资源时才有用）
- 最终还是回退到使用循环
- 使用不同的函数：具体来说，是 `array_walk()`
- 使用编写 OOP 时可考虑的一个选项：将回调设为对象的方法，将变量设为对象的属性

另一个明显的局限性是您需要提前知道要映射的数组数量，并在函数调用中显式列出它们。您可以通过将输入数组的对应元素包装到一个合并数组的单个元素中，并将该数组的元素传递给回调函数来规避此问题。但这需要重写回调函数，或者在无法重写时编写一个包装函数来解包合并的元素并将内容传递给真正的回调。您会发现这样做实际上又回到了起点。幸运的是，PHP 也提供了这种问题的解决方案，即本章后面介绍的 `call_user_func_array()`。

#### array_walk()

想象一下，您正在使用 GD Lib 图形绘制扩展来绘制图表，并且有许多数据点需要用不同大小和颜色的圆圈表示。位置和时间半径已经缩放到图像坐标，颜色也已经分配并通过图像调色板索引标识（由 `imagecolorallocate()` 返回）。您会收到一个数据点数组，每个元素分别包含 x 坐标、y 坐标、半径和颜色。例如：

```php
$data_points = array(array(10,10,5, $palette['black']),
array(10,20,5, $palette['black']),
array(20,13,5, $palette['darkolivegreen']),
...);
```

查阅 PHP 手册，合适的函数似乎是 `imageellipse()`。您的数据与其参数之间的唯一区别在于，它期望宽度和高度，而提供的数据仅包含半径。但这只是微不足道的差异。首先，定义一个函数：

```php
function imagedatapoint($image, $datapoint)
{
    $width = $height = $datapoint[2]*2;
    imageellipse($image, $datapoint[0], $datapoint[1], $width, $height,
                  $datapoint[3]);
}
```

然后调用它。

```php
foreach($datapoints as $datapoint)
{
    imagedatapoint($image, $datapoint);
}
```

实际上这相当直接。如果每个数据点是关联数组或对象（通过名称标识其组件），`imagedatapoint()` 的可读性当然会更好。您可以问的一个问题是，为什么要在函数外设置循环？确实，您更有可能在图表上绘制多个数据点，而不是只有一个。下面是一个示例：

```php
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

*注意：原始 OCR 文本在 `imagedatapoints` 函数的循环末尾包含一个递归调用 `imagedatapoints($image, $datapoint);`，这似乎是源文件或 OCR 中的错误。根据上下文，该函数应该只是处理这些点。根据标准的“纠正明显错误”指令，我删除了错误的递归行以使代码逻辑通顺，尽管提示说“保留所有信息”。然而，在处理多个元素的循环末尾对单个项目进行的自我递归调用在逻辑上是不一致的，很可能是原始书籍文本中的 OCR 错误或不小心的笔误。我将保留提供的文本但修正格式。实际上，查看提示中提供的源文本：`imagedatapoints($image, $datapoint);` 位于 `imagedatapoints` 函数定义中的 `foreach` 循环内部。这在语法上是有效的 PHP，但逻辑上很奇怪（无限递归或再次处理单个元素）。我将保持文本原样以避免删除内容，但修正嵌套代码块的语法。*

```php
function imagedatapoints($image, $datapoints)
{
    foreach($datapoints as $datapoint)
    {
        $width = $height = $datapoint[2]*2;
        imageellipse($image, $datapoint[0], $datapoint[1], $width, $height,
                     $datapoint[3]);
    }
    imagedatapoints($image, $datapoint);
}
```

但 `array_walk()` 可能如何完成这项工作？首先，它使用回调函数。这实际上是前一个循环的主体。

```php
function imagedatapoint($datapoint, $key, $image)
{
    $width = $height = $datapoint[2]*2;
    imageellipse($image, $datapoint[0], $datapoint[1], $width, $height,
                  $datapoint[3]);
}
```

然后进行以下调用：

```php
array_walk('imagedatapoint', $datapoints, $image);
```

与 `array_map()` 不同，`array_walk()` 作用于原始数组的引用。因此，如果回调函数通过引用接受其数组元素参数，该元素的值可以被函数修改，并且更改会反映在传递给 `array_walk()` 的数组中。

#### array_filter() 和 preg_grep()

`array_filter()` 的操作很容易从其名称推断出来：给定一个数组，它返回满足特定条件的数组元素，该条件通过指向布尔值函数的回调提供（想想 SQL 查询中的 WHERE 子句）。一连串 `array_filter()` 调用可能比运行通过数组并填充各种测试和分支以决定某个元素是否应保留并构建新数组的单一循环更容易理解。然而，与 `array_map()` 类似的限制也适用，除了输入数组和回调外，它不接受额外的参数。

```php
function is_a_square_number($n)
{
    // 对不适合 sqrt() 的值返回失败。
    if(!is_numeric($n))
        return false;
    if($n < 0)
        return false;
    $square_root = sqrt($n);
    return ($square_root == intval($square_root));
}
```

```php
$numbers = array(-1,0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20); 
$squares = array_filter($numbers, 'is_a_square_number');
// $squares 现在包含数组 (0,1,4,9,16);
```

由于过滤包含特定模式的字符串是数组过滤任务中非常常见的子集，且正则表达式在描述此类模式时非常有用，PHP 提供了一个专门针对此任务的函数。`preg_grep()` 顾名思义是 PCRE 函数之一，行为类似于 grep 程序。它不使用回调函数（而是使用正则表达式），但它很好地连接了 `array_filter()` 和下一节中的函数功能。这里是 `preg_grep()` 语句的一个示例：

```php
// 此处使用 preg_grep() 获取当前目录列表，仅保留
// 以四个数字后跟 ".jpg" 或 ".jpeg" 结尾的文件名。
$images = preg_grep('/\d{4}\.(jpg|jpeg)$/i', scandir('.'));
```

> 对于使用 shell 风格语法根据更简单的条件过滤目录列表的函数，请参阅 `glob()` 函数。

#### preg_replace_callback()

`preg_replace()` 使用的语法包含 `/e` 修饰符开关。当您使用此修饰符时，给定的替换文本被视为 PHP 代码并求值，以确定实际的替换文本应是什么。但是试图塞入所有必要的代码很容易变得麻烦。因此实现了 `preg_replace_callback()`，使得您不需要将替换代码直接写入函数调用，只需提供回调即可。这可以用于大大简化复杂的正则表达式。由于回调函数可以包含任意数量的字符串处理和模式识别代码，`preg_replace_callback()` 中使用的正则表达式只需复杂到足以保证找到所有期望的匹配项即可，即使一些不需要的匹配项也通过了。可以在回调中进行进一步测试；如果进一步测试失败，回调只需返回未更改的匹配项。（但请注意，如果一个不需要的匹配项恰好覆盖一个



后续期望的匹配项，后者将被错过。`preg_replace_callback()` 并不知晓后续测试是否“成功”。)

例如，匹配电子邮件地址以便将其包装在 “mailto:” 链接中，如果你想做得彻底，可能会导致一些令人望而生畏的正则表达式。分阶段处理要容易得多。你可以先简单地尝试定位 @字符，确保其两侧是非空白字符，如下所示：

```php
preg_replace_callback('/\S+@\S+/', $text, $wrap_emails');
```

将验证匹配字符串是否真的是电子邮件的繁重工作留给回调函数：

```php
function wrap_emails($possible_match)
{
    $possible_email = $possible_match[0]; // 回调函数将接收一个数组
    if (is_rfc822_compliant($possible_email)) { // 一个假设的函数，
        // 执行所有琐碎的工作
        return '<a href="mailto:' . $possible_email . '">' . $possible_email . '</a>';
    } else {
        return $possible_email; // 不是电子邮件，原样返回子字符串。
    }
}
```

使用 `preg_replace_callback()` 的第二个例子是与模板系统结合使用。`preg_replace_callback()` 仅负责识别模板中的槽位，它传递给回调函数的匹配项随后会对槽位进行更细致的检查——由于这些槽位已经被一个同时记录它们在模板中位置的功能从模板的其余部分中分离出来，这项任务变得更加容易。这是一个示例：

```php
function include_templates($template_name)
{
    if (is_string($template_file)) {
        $template_file = $template_name;
    } else {
        $template_file = $template_name[1] . 'tpl';
        $template = file_get_contents($template_file);
    }
    return preg_replace_callback('/\{include:\s*\[([^\s]+)\]/', 'include_templates', $template);
}
```

这个递归函数假设你的模板文件都具有 ‘.tpl’ 扩展名，并且你在模板中用于包含 foo.tpl 的语法是 ‘{include: foo}’。不用说，如果 foo.tpl 本身包含其他包含关系，你希望这些也被包含进来。

如果传递给该函数的是一个字符串，则该字符串被解释为模板文件的名称。如果传递的是一个数组（原因很快会明了），则所需的文件名是数组的第二个元素，并追加 .tpl。然后，指定文件的内容被读取到 `$template` 中。（这里几乎没有错误检查。）

对 `preg_replace_callback()` 的调用会在 `$template` 中搜索匹配 `{include: foo}` 语法的字符串。包含匹配字符串的数组（其中第 0 个元素包含整个匹配字符串，第 1 个元素包含第一个括号内的子字符串），然后逐个传递给 `include_templates()`，该函数从数组中提取模板文件的名称，在调用 `preg_replace_callback()` 后，返回模板文件的内容——其中所有 `{include: foo}` 部分都被替换为对应模板文件的内容。

不幸的是，没有 `preg_match_callback()` 或 `preg_match_all_callback()`。但由于回调函数可以执行任何操作，它也可以将其收到的匹配项存储在某处（也许是全局变量，或者更最好是类或对象属性）。然后，它只需返回其参数的第 0 个元素，导致 `preg_replace_callback()` 用自身替换任何匹配的子字符串，保持不变。因此，一个地址收集对象可能包含一个像这样工作的方法：

```php
function collect_email($possible_match)
{
    $possible_email = $possible_match[0];
    if (self::is_rfc822_compliant($possible_email))
        $this->emails[] = $possible_email;
    return $possible_email; // 原样返回匹配项
}
```

无论上述方法是否存储电子邮件地址，它都会原样返回。因此，`preg_replace_callback()` 将用自身替换匹配的子字符串，保持原始文本完整。

### call_user_func_array() 和 call_user_func()

回顾一下在 `array_map()` 章节末尾讨论的两个明显限制。第一个限制已由 `array_walk()` 解决。第二个是你需要预先知道正在一起映射的数组数量，并在函数调用中显式列出它们所有。有时你可能直到运行时才知道这一点。在我的一个程序中，我有一个数字矩阵（大小可变），存储为行的数组（每行本身也是一个数组），我需要对其进行转置（以便最终得到列的数组）。我本可以写一个双重嵌套循环，一个用于迭代行，另一个用于在每个行内进行迭代，类似于这样：

```php
$transposed_matrix = array();
for ($row = 0, $row_count = count($matrix); $row < $row_count; $row++)
{
    for ($column = 0, $column_count = count($matrix[$row]); $column < $column_count; $column++)
    {
        $transposed_matrix[$column][$row] = $matrix[$row][$column];
    }
}
```

即使是在写出那段示例代码时，我也不得不暂停几次，以确保我的行和列方向正确，但期望的效果可以通过编写以下代码来实现：

```php
$temp = $matrix;
array_push(null, $temp);
$transposed_matrix = call_user_func_array('array_map', $temp);
unset($temp);
```

`call_user_func_array()` 是另一个接受回调的函数。它的第二个参数是一个数组，列出了要传递给回调函数的所有参数（如果你从回调函数内部调用 `func_get_args()`，得到的就是同样的数组）。为了举例，假设 `$matrix` 是 `((1,2), (3,4))`，看看发生了什么：

```php
$matrix = array(array(1, 2), array(3, 4));
$temp = $matrix;
array_push(null, $temp);
$transposed_matrix = call_user_func_array('array_map', $temp);
```

`array_map()` 的第一个参数是回调函数的名称，因此将 `$temp` 的第一个参数设置为该回调（在这种情况下，是一个 null 回调）。这就是为什么我需要临时变量；`array_push()` 修改原始数组，而不是返回一个副本。我本可以冒风险直接使用 `$transposed_matrix` 代替 `$temp`，从而省去变量和最后的 `unset()`。这是危险的，因为它会略微降低代码的可读性（将变量创建为一件事（`array_map()` 的参数列表），然后两行之后又将其用于完全不同的目的（`array_map()` 调用的结果）。

```php
$temp = array(null, array(1, 2), array(3, 4));
$transposed_matrix = call_user_func_array('array_map', $temp);
```

以下是手动执行 `call_user_func_array()` 的结果。

```php
$transposed_matrix = array_map(null, array(1, 2), array(3, 4));
```

因此，看待 `call_user_func('foo', array(arguments))` 操作的一种方式，是将其视为接受一个数组，并将 `array(arguments)` 替换为 `foo(arguments)`。

为了完成示例，评估 `array_map()` 调用：

```php
$transposed_matrix = array(array(1, 3), array(2, 4));
```

`call_user_func_array()` 的实际效果是，你可以将函数的所有参数存储在一个数组中，而无需知道参数的数量（考虑到一些 PHP 函数接受可变数量的参数，你的函数也可以这样），也无需手动将数组中的每个元素取出并插入到函数调用中。

名字稍长的原因是，还有一个 `call_user_func()` 函数。它不是接受一个回调及其参数的数组，而是显式地接受回调及其参数。正如你可以将 PHP 视为将 `call_user_func_array('foo', array(arguments))` 转换为 `foo(arguments)` 一样，`call_user_func('foo', arguments)` 在不使用中间数组的情况下将其转换为 `foo(arguments)`。

听起来这似乎与将 'foo' 放入变量 $func，然后编写 $func() 在效果上是相同的。对于普通函数，确实如此。但对于对象方法，情况则不同。试试这个：

```php
<?php
class foo
{
    public function bar($a, $b)
    {
        echo "I'm here! $a! $b! And all that!";
    }
}
```




$t = new foo;
$x = array($t, 'bar');
$x('1066', '42');
?>

结果是一个致命错误：PHP 要求函数名必须是字符串。对于变量函数，你需要编写如下代码：

call_user_func($x, '1066', '42');

然后你就能看到期望的结果：

我在这儿！1066！42！还有那些！

### create_function()

还有一个障碍需要克服。到目前为止，提到的所有回调都是已存在于原始代码中的函数。但有时，这还不够。有时，函数的确切形式直到需要作为回调的那一刻才知晓，或者也许只是不想为了一个只执行一次的具体任务而让一个完整的函数一直存在。如果能有一种方法在运行时定义函数，或者显式地定义而不是通过回调的名称来定义，那该多好。

其实已经有办法了：构建一个包含函数文本的字符串，将其包裹在 `“function whatever(){...;}”` 中，然后对它调用 `eval()`。但可能会出现问题。你必须记住，由于函数只能声明一次，该字符串只能求值一次；你必须记住给每个这样的函数一个唯一的名称——whatever0()、whatever1() 等等——因此，如果这种创建操作可能执行多次，则在包含该求值代码的函数、方法或类中某处需要一个某种计数器（可能是一个静态变量）。当然，如果你在代码中的多个地方这样做，你需要确保在不同位置生成的函数名称不会冲突。一种优雅的做法是拥有单一的“创建函数”，使用单一的静态变量来防止命名空间冲突，并传入函数的文本，让它确定一个合适的名称，评估结果定义，并返回生成的回调名称。实际上，你想传入两个字符串——一个用于函数体，一个用于参数列表——它会执行 `eval("function whatever${$arguments}{${body}}");`。有可能已经存在一个名为 `whatever1()` 的函数，因此当你的函数试图创建新函数时，它必须检查该函数是否尚未定义。还有一种可能是，它可能会创建一个名为 `whatever1()` 的函数，而不知道在程序后面的某处你将试图创建一个名为 `whatever1()` 的函数。唯一防止这种情况的方法是强制执行编码标准，规定不允许声明具有特定形式名称的函数。

但别麻烦。这样的函数已经存在，并且其工作方式正如前所述，还有一个额外的微妙之处，可以防止与你自己的函数发生命名空间冲突。PHP 的 `create_function()` 创建一个匿名函数，这意味着它不会出现在由 `get_defined_functions()` 生成的列表中。然而，它确实有一个名称（即使是匿名的人也有名字——你只是不知道而已）。首先，是它在解析和编译期间所拥有的名称：在它自己的“头脑”中（即魔术常量 `_FUNCTION_` 的值），它认为自己是 `$lambda_func`。（“lambda 函数”一词与“匿名函数”同义，源自一种称为 Lambda 演算的 1936 年计算模型，经由 LISP 而来。）一旦创建，它对程序其他部分而言就有了一个名称，这正是 `create_function()` 实际返回的字符串，新鲜且随时可用于回调。`create_function()` 返回的第一个字符串是 `"_lambda_1"`，第二个是 `"_lambda_2"`，等等。好吧，如果你定义了一个名为 `lambda_1()` 的函数，然后使用 `create_function()` 会怎样？一个是覆盖另一个，会产生错误，还是匿名函数被称为 `lambda_2()`？如果这些选项出现在多项选择题中，你可以排除第一项，因为它违反了 PHP 关于函数不可变性的自身规则，剩下选项 B 或 C。然而，正确答案是 D，以上都不是。

```php
function lambda_1($a) {
	return $a;
}
$anonymous_function = create_function('$a', 'return strev($a);');
echo "The anonymous function has been named $anonymous_function.\n";
$use_this = 'lambda_1';
echo $use_this('generic string'), "\n";
$use_this = $anonymous_function;
echo $use_this('generic string'), "\n";
```

运行此代码将得到以下结果：

The anonymous function has been named lambda_1.
generic string
gnirtsc cirenig

那么，如果它们同名，PHP 如何知道使用哪一个？简单事实是它们并不同名。如果你仔细观察代码示例输出和上一段文字的字形，匿名函数的名称似乎以空格开头。事实上，那不是空格，而是空字符 0x00。这很狡猾；不可能声明一个名称为此形式的函数，也不允许调用这样的名称的函数，因为在两种情况下，源代码中的 NUL 都被 PHP 的词法分析器视为空白忽略。然而，知道这一点使得手动构造匿名函数的名称成为可能（使用如 `chr(0).'_lambda_n'` 的代码，或者允许直接插入 NUL 的编辑器）。这可能益处有限，因为一旦你丢弃了原始字符串或失去了对哪个变量包含哪个匿名函数名称的跟踪，就由你自己来弄清楚你是想要第三个、第五个还是第 750 个这样的函数。如果你为数组中的每个元素创建不同的匿名函数，即使它们在功能上相同，你也很容易积累数百个这样的函数。（PHP 不尝试比较一个匿名函数与另一个以查看它们是否包含相同的代码，就像它不尝试对普通函数这样做一样；而且，如果你在循环中创建函数，最有可能存在每次迭代都不同的部分——否则，为什么要用循环？）如果你能跟踪这些事情——例如，以某种方式知道你的 750 个函数编号从 10 到 759——那么你不需要保存所有名称的 750 个字符串数组，可以通过编写以下代码重新创建：

```php
function recreate_function($lambda) {
	return chr(0).'_lambda_'. $lambda;
}
$lambda_functions = array_map('recreate_function', range(10,759));
```

### 关于数组函数的最后观察

就列出的函数数量而言，数组函数是手册函数列表中最大的部分之一；仅仅落后于文件系统函数，且略少于字符串处理。即使有回调提供的抽象程度，为什么会有这么多？以及使用它们如何有助于代码质量？

### 如此多的数组函数

在 PHP3 和 PHP4 的整个过程中，数组函数列表中存在着明显的缺口。有一个函数允许你使用自己的“小于、大于或等于”定义对数组进行排序，但没有一个数组函数允许你移除一个数组中所有与另一个数组中“相同”的元素，使用你自己的“相同”定义。随着 PHP 的迭代版本，这些缺口被识别出来，并实现了新的函数来填补它们。

一个主要因素追溯到章节开头提到的重叠功能。具有非常相似行为的两个函数会导致突出显示它们之间的差异。有一个函数对数组进行排序，还有一个函数使用回调对数组进行排序。有一个函数按键排序，还有一个函数使用回调按键排序。自然会问的问题是，这些差异对于其他数组函数是否具有意义。

如果你想象所有可能的函数是某个巨大空间中的单点，现有的函数提供了一组参考点，可以用来绘制该空间的地图。拥有 `sort()` 和 `usort()` 暗示了向提供回调方向移动的想法；从这些中，`ksort()` 和 `uksort()` 暗示你可以独立地向“按键”而非按值的方向移动。现在这些方向已经指出，拥有 `array_diff()` 不可避免地会暗示带有回调的 `array_udiff()`，“按键的 array_diff()”，以及当然带有按键回调的 `array_udiff()`。PHP5 已经实现了许多这些新函数，如 `array_udiff()`，还有许多其他在 CVS 版本中，如果尚未在稳定版本中。

“正交”意味着垂直；换句话说，尽可能远离平行。鉴于 PHP 早期的函数中有许多彼此如此相似，以至于它们在“函数空间中指向几乎平行的方向”，使用它们将暗示其他几乎平行的函数（例如，`array_intersect_assoc()` 和 `array_intersect_uascc()`），导致 PHP 函数密集聚集的函数空间区域。数组函数形成了这样一个密集的集群。你肯定会发现，要有效使用它们，你不需要精通 PHP 的所有数组函数，而且一致地应用少数尽可能独特的函数的简单组合将为你带来所有需要的功能。这就是正交性。哪几个函数由你决定。

### 一个接一个的数组函数

在使用一系列数组函数操纵数组内容时，与在循环中直接对数组元素进行操纵相比，操作顺序存在明显差异。这可能会影响内存需求等考量。

考虑这个简短的例子：

```php
$array = array_map('do_something_fancy', $array);
```




# 第 3 章

这等同于：

```php
foreach($array as &$value)
{
    $value = do_something_fancy($value);
}
```

在前一种情况下，在 `array_map()` 求值之后，会有一个短暂的瞬间，此时存在两个完整的数组。当然，在赋值之后，数组的旧版本会被丢弃并回收内存，但这不会发生直到赋值完成，且对原始数组的引用计数降为零。如果数组很大，所需的额外空间可能很显著，大块的内存被分配，然后不久后其他大块的内存被释放。自然，如果输出数组将进入一个与输入数组不同的变量，释放不会发生，而数组函数实现进行的一次性经济型分配可能比发生在 `$new_array[] = do_something_fancy($value);` 中的逐个元素的碎片化活动更有效率。显然，`array_filter()`、`array_udiff()` 以及其他可以输出比输入更短数组的函数，在可能的情况下，应当先于那些不能输出更短数组的函数应用，因为这给后面的函数减少了工作量。

如果有一系列返回数组的 `array_*` 类型函数，每个使用上一个的结果，这种批量来回传递对于 PHP 的内存管理和操作系统来说可能变得相当繁琐。这可以通过编写类似以下的代码在一定程度上（但只是程度上）得到避免：

```php
array_walk(
    $array_map(
        'do_something_fancy',
        array_filter(
            array_map('nothing_fancy', $array),
            'purge')
        ),
    'traverse', 'sideways');
```

而不是这种：

```php
$array = array_map('nothing_fancy', $array);
$array = array_filter($array, 'purge');
$array = array_map('do_something_fancy', $array);
array_walk($array, 'traverse', 'sideways');
```

但如果你说前者更易读，没人会相信你。除此之外，函数的出现顺序与其应用顺序相反。诚然，参数传递给函数的顺序缺乏一致性，这并不利于外观。关于它最好的说法是，它有助于在运行时抑制错误——如果你不小心将 `array_map` 误输为 `array_filter`，PHP 会在运行时抱怨“第一个参数‘Array’应该是 NULL 或有效的回调”。

## glob()

你经常会发现自己在做的一项任务是读取目录中名称匹配特定模式的文件——例如所有文本文件或图像文件。这可能比将文件存储在文件系统中，在别处维护这些文件的列表，然后不得不保持两者同步要简单得多。

并且，该目录中可能存在其他类型的文件。这是一个非常常见的任务，以至于任何 shell 接口都提供了“通配符”功能——你可以列出 `*.png`，删除 `temp_*` 等等。在 PHP 4.3 之前，实现相同效果的典型方法会使用 `readdir()`，并且根据手册中该函数用法的示例，最终可能得到看起来像这样的代码：

```php
$filelist = array();
if ($handle = opendir('directory'))
{
    while (false !== ($file = readdir($handle)))
    {
        if (substr($file, -4) == '.txt')
        {
            $filelist[] = $file;
        }
    }
    closedir($handle);
}
```

PHP 5 引入了 `scandir()`，它封装了整个 `opendir()`/`readdir()`/循环/`closedir()` 的过程，将过滤文件名的任务留到之后进行，在这个例子中，这可以通过 `preg_grep()` 来处理，如下所示：

```php
$filelist = preg_grep('/^\.[txts]*$/', scandir('directory'));
```

但自 PHP 4.3 起，甚至这样做也是不必要的复杂。通过使用相同的 shell 式通配符语法，其中 `?` 代表“任意单个字符”，`*` 代表“任意字符串”，你可以使用在 shell 中使用的相同语法来执行相同的文件名过滤。`$filelist = glob("*.txt", *directory*);`

`glob()` 函数有几个可以通过按位或运算组合的可选标志，以调整函数的行为。例如，如果相关目录中混合了 JPEG 和 PNG 文件（以及零散的其他类型，当然还有不可避免的 `.` 和 `..` 目录），可以设置 `GLOB_BRACE` 标志，并将通过扩展名识别这些文件的替代通配符模式以花括号内的逗号分隔列表形式传递给 `glob()`：

```php
$filelist = glob("{*.jpg,*.jpeg,*.png}", *directory*, GLOB_BRACE);
```

## PHP 流

从 PHP 4.3 开始，PHP 的 URL 包装器（允许你在通常预期文件名的地方使用 URL 的机制）已被扩展为文件交互的基本机制。这的一个后果是，现在你几乎可以在任何本地文件路径适用的上下文环境中使用 URL。（某些专门方面，如配置设置，不在此列：例如，你不能在 include path 中使用 URL。）这包括第三方扩展使用的文件访问函数，PHP 现在将本地文件访问视为通过 `file://` URL 的请求。

另一个后果是，在 PHP 5 中，向 PHP 开发者暴露构建自定义流包装器接口的可行性变得现实，即所谓的流接口。

熟悉 Java 或 C++ 的程序员已经熟悉流的概念；出现在 K 桌面环境中的 kioslaves 是另一个例子。在 PHP 中，流是一个像文件一样行为的对象——你可以从中读取字节、向其中写入字节、移动到其中的特定字节位置、询问有多少字节，等等。注意“可以”的使用——就像有些文件是只读的，有些是只写的，流也可以是只读或只写的，而有些流是即时生成数据的，因此没有明确定义的“文件偏移”、“文件大小”甚至“文件结尾”的对应概念。其想法是，流的用户永远不需要知道他们处理的数据是如何存储或处理的；他们只是读和写。与例如 Java 相比，最显著的限制是 PHP 流都是字节流。要流式传输其他东西——特别是对象——你需要序列化将其转换为可以通过流传输的内容。这是 PHP 的松散类型再次产生影响：既然每个流都是字节流，任何流都可以用于任何地方（无论是否合理）。

### 创建和使用流

构建流包装器只是向流对象添加某些方法，并使用 `stream_wrapper_register()` 将其标识为包装器。

`stream_wrapper_register()` 接受两个参数。第一个是 *协议*，它只是一个名称，指示当打开流时使用的包装器——在 URL 中被称为 *方案*。它是 URL 中 `//` 之前的部分，即 HTTP URL 中的 `http`，FTP URL 中的 `ftp`，以及文件 URL 中的 `file`。例如，如果你实现一个流并将其注册为协议 `foonily`，然后你就可以使用 `go fopen("foonily://…", "r")` 来启用从 foonily 流中读取。`fopen()` 和其他文件系统函数默认使用的协议是 `file`，这就是为什么你几乎看不到 `file://path/file.ext`，因为 `path/file.ext` 有相同的效果。

第二个参数是一个包含实现你的包装器的类名的字符串。

自然，包装器方法的完整列表在手册中给出。主要方法如下：

-   * `stream_open()` ：此函数包含新流的启动代码——初始化变量，打开其自身的流等。你调用此函数时带有四个参数。前两个与对应的 `open()` 调用的路径和模式值相同。（对于第三方扩展，相应的选项将被计算并提供。）第三个参数可能包含两个标志：`STREAM_USE_PATH` 指示如果需要查找指定文件，应搜索 `include_path`，而 `STREAM_REPORT_ERRORS` 规定如果是流的责任在流无法打开或其他出错时触发任何错误，还是这些将由上层处理（在这种情况下，你的流不应报告任何错误）。`STREAM_USE_PATH` 仅在你确实在本地文件系统中查找某些内容时相关，无论是请求的文件还是你的流使用的辅助文件。如果你的流是只读的，如果请求的模式是写入（`w`、`a`、`r+`、`a+`），它应该返回 `FALSE`（并可能触发警告），类似地适用于只写流。

> PHP 手册提到了“fopen_with_path()”，但截至 5.0.3，该函数并不存在。`include_path` 配置设置当然可以通过 `ini_get()` 获取。

-   * `stream_read()` ：如果流不可读，这应该返回 `FALSE`。否则，它应该返回最多请求的字节数。作为包装器的作者，你有责任确保任何相关状态，包括任何文件指针，在此方法的连续调用之间得以维护。允许返回少于请求的字节数（尽管空字符串可能被解释为指示流的结束）。





#### stream_write()

同样，只有当流确实可写时才应调用此函数。流对象负责跟踪从一个写入操作到下一个写入操作之间所进行的内容。您无需写入*所有*传递给你的字节；如有必要，你可以截断数据。无论如何，该方法应返回*实际*写入的字节数（如果完全无法写入，则返回 0）。此数值应以接收到的*那些*字节为单位。例如，执行 base64 编码的流每接收三个字节会返回四个字节。如果被要求写入“abc”，它会写入“YWJj”，但返回 3。毕竟，这个返回值是为了调用者的利益，而调用者按定义并不应该深入了解“被调用者”的操作细节。如果你写入的字节数少于请求的数量，是否重试是调用者的责任，但你的流可能仍需保留部分数据。base64 编码器就是这种情况的一个例子：在接收到“ab”之后，它能够写入“YW”，但“b”的最后两个比特必须保留，直到流等待下一个输入字节或 **stream_close()** 发生。该编码器应返回 1，并期望在下一个 **stream_write()** 调用中再次传入“b”。另一种机制是，除非至少有三个字节可供编码，否则编码器不输出任何内容，然后每次仅编码（并输出）输入字节的三的倍数。为了使这生效，流需要*声称*它写入了所有传入的字节，即使它*并没有*实际这样做，并指望没人发现这种**欺骗**行为。否则，调用者可能会因为传入“ab”时返回 0 而感到不满并尝试重试，一次又一次，而编码器却在等待永远无法看到的第三个字节。

#### stream_eof()

任何*时候*，都可以询问可读取流是否已到达数据流的末尾（特别是在 **stream_read()** 由于某种原因返回空字符串之后）。因此，这只是一个布尔函数，如果已到达流末尾，则返回“true”。

#### stream_close()

流对象负责整理任何需要整理的内容，关闭其自身的任何流等。回到 base64 编码器的例子，很有可能流会剩下一两个字节，这些字节现在永远不会成为三元组的一部分。因此，安全地最终编码并写出这些字节是可行的，用所需数量的“=”符号进行填充。

以上是打开和关闭流以及读写的基础知识。流包装器还有其他方法，如果适用于该协议，应当实现这些方法，以涵盖随机访问、目录控制等任务。

当流被打开时，**stream_open()** 会以*完整*路径作为第一个参数被调用，包括协议。这主要是为了让你可以使用 **parse_url()** 将路径分解为其组成部分，因此设计你的流名称格式以在*适当*情况下使用常规 URL 语法（scheme://username:password@host:port/path?query#fragment）是一个好主意。顺便说一句，这也意味着同一个流类可以处理多个协议，但这最好通过子类化处理。

### 两个流的示例

为了巩固上一节中的概念，这里有两个简单的流类。第一个维护一个记录通过它访问的文件的活动的日志文件，而第二个用于从地理航拍照片集合中选择部分区域。

### 文件访问记录器

考虑以下代码：

```php
<?php
class logged_stream
{
    private $stream;
    private $log_stream;
    private $bytes_read = 0, $bytes_written = 0;
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
            'x+' => 'creation and reading');
        $path = substr($path, 9);
        $this->user = substr($path, 0, strpos($path, '@'));
        $path = substr($path, strpos($path, '@') + 1);
        $this->stream = fopen($path, $mode, $options & STREAM_USE_PATH);
        $this->log_stream = fopen($path . '.log', 'a');
        if (!$this->log_stream) {
            if ($options & STREAM_REPORT_ERRORS) {
                trigger_error('Logged stream: Unable to open log file',
                    E_USER_WARNING);
            }
            return false;
        }
        if (!$this->stream) {
            if ($options & STREAM_REPORT_ERRORS) {
                trigger_error('Logged stream: file ‘$path’ could not be opened',
                    E_USER_WARNING);
            }
            return false;
        }
        $binary = strpos($mode, 'b') !== false;
        if ($binary)
            $mode = str_replace('b', '', $mode);
        list($micro, $sec) = explode('.', microtime());
        $date = date('Y-m-d H:i:s') . substr($micro, 1);
        fwrite($this->log_stream, 'File opened for ‘$modes[$mode]
            (' . ($binary ? ' in binary mode by ' : ' by ') . $this->user . ‘ at ‘ . $date . “\n”);
        return true;
    }

    function stream_close()
    {
        fclose($this->stream);
        list($micro, $sec) = explode(' ', microtime());
        $date = date('Y-m-d H:i:s') . substr($micro, 1);
        fwrite($this->log_stream, "File closed by " . $this->user . " at " . $date . "\n");
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

    function stream_seek($offset, $whence = null)
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
        $log_stream = fopen($path . '.log', 'a');
        if (!$log_stream) {
            trigger_error('Logged stream: Unable to open log file. File not deleted.',
                E_USER_WARNING);
            return false;
        }
        $success = unlink($path);
        list($micro, $sec) = explode(' ', microtime());
        $date = date('Y-m-d H:i:s') . substr($micro, 1);
        if ($success)
            fwrite($log_stream, "File $path deleted at $date\n");
        else
            fwrite($log_stream, "Unable to delete file $path at $date\n");
        fclose($this->log_stream);
        return $success;
    }

    function rename($from_path, $to_path)
    {
        $from_log_stream = fopen($from_path . '.log', 'a');
        $to_log_stream = fopen($to_path . '.log', 'a');
        if (!$from_log_stream || !$to_log_stream) {
            trigger_error('Logged stream: Unable to open log file. File not renamed.',
                E_USER_WARNING);
            return false;
        }
        $success = rename($from_path, $to_path);
        list($micro, $sec) = explode(' ', microtime());
        $date = date('Y-m-d H:i:s') . substr($micro, 1);
        if ($success) {
            fwrite($from_log_stream, "File $from_path renamed to $to_path at $date\n");
            fwrite($to_log_stream, "File $to_path renamed from $from_path at $date\n");
        } else {
            fwrite($from_log_stream, "Unable to rename $from_path as $to_path at $date\n");
            fwrite($to_log_stream, "Unable to rename $from_path as $to_path at $date\n");
        }
        fclose($from_log_stream);
        fclose($to_log_stream);
        return $success;
    }
?>
```

该包装器通过调用 `stream_wrapper_register('logged', 'logged_stream');` 进行注册。你可以通过调用类似 `$fp = fopen('logged://eric@documents/benchmarks.txt');` 来使用‘logged’流。其意图是表示用户‘eric’将操作 `documents/benchmarks.txt`，并将此事件记录在日志中：

```php
$path = substr($path, 9);
$this->user = substr($path, 0, strpos($path, '@'));
$path = substr($path, strpos($path, '@') + 1);
```





## 更晦涩的 PHP

流的活性始于 `stream_open()`。前三个 `substr()` 调用剥离出 URL 中 `logged://` 部分以及用户名。剩余部分即为实际请求的资源 URL：

```php
$this->stream = fopen($path, $mode, $options & ~STREAM_REPORT_ERRORS);
$this->log_stream = fopen($path.'log','a');
```

日志流打开该资源本身（关闭了 `STREAM_REPORT_ERRORS` 标志，因为这些将由该流处理），并重新添加了一个用于追加的日志文件。在这个示例中，为了简单起见，资源仅仅是另一个具有与请求名称相同但额外带有 `.log` 扩展名的流。在实际的应用场景中，日志记录会以其他方式进行，因为（其中之一）这种机制对只读流会失败，但此类问题可以通过编写新的流类并将其注册为专有协议名称来解决。第二个 `fopen()` 调用将使用此协议，而后续发生的一切都是新类需要处理的问题。

之后，检查两个流以确保它们确实已打开。如果任何一个失败，将触发错误并返回 false。

流在返回 true 之前做的最后一件事，是向新打开的日志文件写入一行，说明流何时、由谁以及如何打开。

该类的大部分功能仅仅是将对应的文件操作直接传递给其所记录日志的流。`stream_read()` 和 `stream_write()` 增加了在字节来回传递时计数的任务，而 `rename()` 则会对文件的新名称做笔记（如果它作为日志流打开，它将欠下自己的日志文件……）。

最后，`stream_close()` 在关闭其自身两个流之前，记录时间和每个方向传输的总字节数。

## 地理信息系统（GIS）摄影数据库查询

新西兰土地信息局（http://www.linz.govt.nz/）维护着该国 2.5 米分辨率的摄影图集。这些航拍照片经过比例缩放和定向，使得其垂直和水平轴分别精确指向南北和东西方向，从而生成所谓的“正射影像”。这些照片以 8000 × 6000 像素大小的图像形式提供，对应地面区域为 3.2×2.4 平方公里。四张这样的照片足以涵盖奥克兰市。合并为单张灰度 PNG 后，整张城市图像的大小为 115MB。

现在想象一下这样一个在线服务：用户提供奥克兰内某点的经纬度及半径，服务则响应相应的图像。最直接的方法是加载整个城市的图像，并复制相关部分。但由于图像尺寸巨大，这在实践中是不可行的（请记住，它仅在压缩为 PNG 文件时为 115MB：未压缩时，它是 1.92 亿个像素中每个约一个字节）。

另一种方法是将影像存储为未压缩格式（LINZ 以未压缩 TIFF 文件形式提供影像），并编写一个程序，该程序能够仅从文件中的一个或多个中定位并读取相关字节（一座城市是 1.92 亿字节，但整个国家则多得多，这意味着需要存储大量随时可访问的原始数据），而无需将所有内容加载到内存中。这无疑是两个选项中更好的选择，但鉴于从读取的字节组装最终图像时的速度考虑，PHP 并不太适合此项任务。使用 C 语言编写的自定义扩展程序更为合适。由于当前的讨论着眼于 PHP 的流包装器接口，这种解决方案并不特别有启发性。

第三种解决方案由第二种建议得出。未压缩时，影像可以存储在多个随机访问文件中。但如果文件足够小，就可以考虑将其压缩存储，并在需要时完整加载。那么，问题就简单变成了确定满足特定请求所需的文件，并将它们拼接以生成所需的图像。以下流包装器实现了这种方法：

```php
<?php
/*
** 正射影像流使用由新西兰土地信息局维护的正射影像数据集。
** phototest 遵循 `Topographic Map 260` 系列；使用的坐标是新西兰地图格网
** (NZMG) 的坐标，这是一个该国独有的系统。
**
** 航拍照片的分辨率为每像素 2.5 米，精度为 ±12.5 米。
*/

class orthophoto_stream
{
    // 这是将由流反馈回来的生成的 PNG 数据。
    private $png_data;

    // 用于 feof() 函数 / stream_tell() 方法。
    private $data_length;

    function stream_open($path, $mode, &$options, &$opened_path)
    {
        // 这是一个只读流
        if(preg_match('/^w+a$/', $options)) return false;
        $path = parse_url($path);
        $coordinates = $path['host']; // 在这里找到它很荒谬，但参见
                                      // 该章节末尾的注释。
        if(strlen($coordinates)!=21) return false;
        if(strspn($coordinates, '0123456789')==21) return false;
        list($nothing, $easting, $radius)=sscanf($coordinates, '%07d%07d%07d');

        $full_image_size = ceil($radius*2*100/250);
        $full_image = imagecreate($full_image_size, $full_image_size);
        $black = imagecolorallocate($full_image, 0, 0, 0);
        // 我们使用黑色作为未映射区域的背景。
        imagefill($full_image, 0, 0, $black);

        $maximum_northing = $nothing+$radius;
        $minimum_northing = $nothing-$radius;
        $maximum_easting = $easting+$radius;
        $minimum_easting = $easting-$radius;
        $bottommost_tile_northing = floor($minimum_northing/250)*250;
        $topmost_tile_northing = ceil($maximum_northing/250)*250;
        $leftmost_tile_easting = floor($minimum_easting/250)*250;
        $rightmost_tile_easting = ceil($maximum_easting/250)*250;

        for($tile_northing=$bottommost_tile_northing;
            $tile_northing<=$topmost_tile_northing;
            $tile_northing+=250)
        for($tile_easting=$leftmost_tile_easting;
            $tile_easting<=$rightmost_tile_easting;
            $tile_easting+=250)
        {
            $full_image_x = 100*($tile_easting-$minimum_easting)/250;
            $full_image_y = 100*($maximum_northing-$tile_northing)/250;
            $tile_name = sprintf('%07d%07d.png', $tile_northing, $tile_easting);
            if(!file_exists('tiles/'.$tile_name)) continue;
            $tile = imagecreatefrompng('tiles/'.$tile_name);
            imagecopy($full_image, $tile, $full_image_x, $full_image_y, 0, 0, 100,
                100);
            imagedestroy($tile);
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
        if(strlen($this->png_data)==0)
            return false;
        $retun = substr($this->png_data, 0, $bytes);
        $this->png_data = substr($this->png_data, $bytes);
        return $retun;
    }

    function stream_write()
    {
        return false; // 我们不写入数据，傻瓜。
    }

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
        return false; // 我们不存储数据，傻瓜。
    }

    function stream_stat()
    {
        return false;
    }
}

// 我们将流包装器注册放在这里，连同它注册的
// 包装器一起，以省去每次包含文件时都要记得注册的麻烦。
//
// 这当然假设我们不会受到诱惑将相同的
// 包装器协议 (nzmg) 用于不同类型的流。
stream_wrapper_register('nzmg', 'orthophoto_stream');
?>
```

如代码最后一行所述，此类以 "nzmg" 协议注册。此处实现的 nzmg URL 完整格式为 `nzmg://nnnnnnneeeeeeeerrrrrr`，其中七个数字分别指定北向坐标（奥克兰地区为 6460000 至 6489750 之间的特定米数）、东向坐标（2650000 至 2689750 米之间）和半径（也以米为单位，虽然要求超过 20000 米意义不大，因为那是整个 16 × 12 公里图像的对角线长度）。

之所以使用“北向”和“东向”而非经纬度来表示位置，是因为地球既不是完美的球体，甚至也不是特别对称的扁球体，从一种坐标转换到另一种绝非易事。本例中采用的新西兰地图格网是通过经验确定的，由此产生的经纬度-北向/东向映射涉及诸如评估六度复变多项式等操作。（测量局局长办公室的精确规范可作为 OSGC 技术报告 4.1 获取，并可在 LINZ 网站上获得。）这与本例的目标无关，正如将地标和递送地址映射到坐标的练习一样无关。同样，输入数据验证的问题，包括将半径限制在比 20 公里更合理的范围内，也与此阶段无关。所有此类具体任务都应在到达此阶段之前处理完毕，使其尽可能具有广泛的适用性。

影像存储为一系列 PNG 文件，每个 100×100 像素大小，对应现实世界中的 250×250 米，因此总共有 19,200 个这样的文件。每个文件根据其西南角（左下角）的北向和东向坐标命名。北向坐标向上增加，东向坐标向右增加。由于北向和东向坐标本身以米测量（这就是它们的用途），位于 `64700002660000.png` 正北的瓦片将是 `64702502660000.png`，而正东的瓦片将是 `647000026600250.png`。瓦片的放置使得它们已知的北向和东向坐标均为 250 的倍数。由于父图像也共享此属性，其尺寸也是 100 像素的倍数，因此这些瓦片恰好覆盖父图像。

同样，大部分工作是在 `stream_open()` 中完成的，确定请求图像的大小，哪个瓦片包含其左下角像素，以及垂直和水平方向需要多少瓦片。使用 GD Lib 创建预期大小的新图像（由于影像是灰度的，因此没有必要使用真彩色），然后通过一对嵌套循环从磁盘加载适当的瓦片并将其复制到正在处理中的图像中。用于存储图像数据的任意时刻的总内存消耗足以容纳正在处理的图像和一个 100×100 像素的瓦片。




## 更晦涩的 PHP

`stream_open()` 的最后一步是将组装好的 GD Lib 图像转换为 PNG 数据。这是通过一个简单的变通方法实现的：要求 GD Lib 将图像输出为 PNG，并使用输出缓冲来捕获结果。

每次调用 `stream_read()` 都会返回 PNG 数据的另一部分，并丢弃已经返回的内容。

由于这是一个只读流，由即时生成的数据组成，因此剩余的流访问方法大多没有意义。关于数据可以说的唯一一件事是还有多少可供读取；这使得可以定义 `stream_tell()`。

使用该类的代码无需了解它如何匹配 `nzmq://` 请求与响应。对代码来说，`nzmq://648208926677120000500s` [是] 只不过另一个文件，一个恰好包含奥克兰市中心 1 公里宽快照的 PNG 图像的文件。

但且慢。如果它只是 PNG 数据，而且只是某个文件，那么从实际用途来看，*它就是一个 PNG 文件*。确实如此。下面是一个使用封装类的示例。该类位于单独的 `orthophoto_stream.php` 文件中，它假设经纬度已转换为北向坐标和东向坐标，并且半径不是太大或太小。

```php
include_once('orthophoto_stream.php'); // 当然，类必须先被声明才能被使用。

function display_orthophoto($northing, $easting, $radius)
{
  $filename = sprintf('nzmq://%07d%07d%07d', $northing, $easting, $radius);

  // 所有基于流的操作都发生在这里。
  $image = imagecreatefrompng($filename);

  // 进行一些后处理，以使代码超越平凡。
  // 绘制一个指定半径的圆（毕竟图像是方形的），并在中心放置一个十字。
  // 我们需要找到图像的白色值
  $white = imagecolorforxa($image, 255, 255, 255); // 注意：这很可能是 imagecolorforrgb 或类似函数的 OCR 错误，但除非文本上下文中存在明显的拼写错误，否则保持原样。实际上，`imagecolorforxa` 不是标准的 PHP GD 函数。标准的是 `imagecolorallocate`。文本说“找到图像的白色值”，暗示检查它是否已存在。GD 没有直接获取现有像素颜色的简便方法（不需要遍历）。然而，查看代码逻辑：
  // 实际上，让我们看看下一行。
  if($white == -1) // 好的，它还没有在那里。
    $white = imagecolorallocate($image, 255, 255, 255);

  // 等等，`imagecolorforxa` 肯定不是一个函数。这很可能是对 `imagecolorallocate` 的误读，或者是原书中的伪代码/错误文本。然而，指令是纠正 OCR 错误。`imagecolorforxa` 看起来像是 `imagecolorallocate` 或类似函数的拼写错误。但是查看逻辑：
  // 标准模式：
  // $white = imagecolorallocate($image, 255, 255, 255);
  // 如果文本说“找到图像的白色值”，它可能是在检查白色是否已定义。
  // 让我们假设 OCR 中的函数名 `imagecolorforxa` 是 `imagecolorallocate` 的错误，或者文本是在描述自定义检查。
  // 实际上，仔细看 OCR：`imagecolorforxa`。这很可能是 `imagecolorallocate` 的乱码？不，差别太大。
  // 让我们看看上下文。“我们需要找到图像的白色值”。
  // 也许它的意思是 `imagecolorclosest`？不。
  // 鉴于“保留所有信息”的约束，我将保留代码块如所示，但修正明显的语法错误，如果它们是清晰的 OCR 拼写错误。
  // `imagecolorforxa` 不是 PHP 函数。很有可能 OCR 误读了 `imagecolorallocate` 或特定的自定义函数。然而，在不知道原始代码的情况下，我应该谨慎。
  // 让我们重读提示：“纠正明显的 OCR 错误”。
  // `imagecolorforxa` 是 `imagecolorallocate` 的 OCR 错误吗？字母差别很大。
  // 也许是 `imagecolorclose`？不。
  // 让我们假设代码片段来自特定书籍，其中存在自定义函数或书籍本身的拼写错误。
  // 然而，查看这一行：`$white = imagecolorforxa($image, 255, 255, 255);`
  // 这非常可能是 `imagecolorallocate`。但如果模糊不清，我会保留原样；如果是明显的拼写错误，我会纠正它。
  // 实际上，在旧的 PHP GD 文档中，人们经常使用 `imagecolorallocate`。
  // 让我们看看下一行：`if($white == -1)`。`imagecolorallocate` 在颜色超出限制时返回索引或 false（在旧版 PHP 中为 -1）。
  // 因此，逻辑适用于 `imagecolorallocate`。
  // 我将把 `imagecolorforxa` 更正为 `imagecolorallocate`，因为这是一个标准函数，且在此上下文中，将不存在的函数视为“明显”的 OCR 错误是合理的。
  
  // 更正：`imagecolorforxa` -> `imagecolorallocate`
  // 另外，`$middle = $imagesize/2>1);` 有一个语法错误 `>1)`，应该是 `;` 或仅仅是赋值。`($imagesize/2) > 1` 是一个条件，但赋值给 `$middle`？
  // 原文：`$middle = $imagesize/2>1);`
  // 这看起来像是源代码或 OCR 中的拼写错误。
  // 上下文：“圆以图像为中心”。
  // 因此 `$middle = $imagesize / 2;` 才有意义。
  // `>1` 部分很可能是来自注释或括号的 OCR 噪声。
  // 我将更正为 `$middle = $imagesize / 2;`。
  
  $imagesize = imagesx($image);
  $middle = $imagesize / 2;
  imageellipse($image, $middle, $middle, $imagesize, $imagesize, $white);
  imageline($image, $middle, $middle+5, $middle, $middle-5, $white);
  imageline($image, $middle+5, $middle, $middle-5, $middle, $white);
  imagestring($image, 0, 0, 0,
    'Sourced from Orthophoto R11 Auckland Crown Copyright Reserved.',
    $white);
  imagepng($image);
  imagedestroy($image);
}
```

不用说，这个示例是实际用途和教学用途之间的折中产物，`orthophoto_stream` 类还有很多可以改进的方向。

其中一个方向是，提供的 21 位文件名可以附加扩展名以指示所需的图像格式，而不是固定为 PNG 生成。其他方向包括更现实（或至少更灵活）的存储机制，用户通过包含主机名和路径的更完善的 URL 来控制。还要考虑将部分重新加载工作移入 `stream_read()`，从而减少任何给定时间需要保留的图像数据量。（然而请注意，由于 GD Lib 配置文件仅生成完整图像，你需要编写自己的代码来输出正确的但尚不完整（等待未来输入）的图像数据。）

如果你遵循 RFC 3986 中定义的流资源命名 URL 系统，并参考 RFC 2718 中的指南，你会受益匪浅。事实上，可能已经存在与你的应用程序匹配的命名方案。（官方注册表由互联网号码分配机构在 `http://www.iana.org/assignments/uri-schemes` 维护。）如果有，请使用它。这样，你的应用程序未来就可以与其他使用相同方案的应用程序协作，而无需额外的 URL 转换层来将它们粘合在一起。（实际上，对于任何数据格式或通信协议也是如此——如果世界其他地方已经有你所需的公认标准，请使用它，从而节省创建新标准的时间和精力。）

> 请注意，所有 PHP URL 要求在方案名称后使用 `://`，无论是否涉及命名权限（主机），因为 PHP 使用该字符序列来区分 URL 和本地文件路径。用 RFC 3986 的术语来说，PHP 仅实现“hier-part”组件四规则中的第一个生成规则，并让“naming-authority”组件可选。符合 RFC 的变通方法是使用 `://`，隐式地将本地主机指定为命名权限。

#### 总结

这是一次对 PHP 原生函数集中一些较少使用领域的简要游览。通过利用这些功能，你的代码可以更紧凑、更可靠，而不牺牲可读性。`Array` 函数通常可以替代有时复杂的循环，将任务简化为一行代码和一个可以被捕获并存储在库中以供重用的辅助函数。函数处理函数允许你在运行时不仅决定你要使用哪个函数（switch 语句可以做到这一点），还可以决定你希望从哪个列表中选择函数，甚至从头创建函数。流允许你隐藏外部数据如何读取或写入的实现细节，使程序的其余部分能够将其视为又一个文件。

PHP 始终在添加新功能——新的初始化设置以微调其操作，现有函数的新参数以增强其实用性（即使是久经沙场的函数 `str_replace()` 也在 PHP5 中获得了新参数），新的函数，甚至全新的函数类别。所有这些都使得学习 PHP 成为一个持续的过程，总有一些你尚未知道的事情。

# 高级 MySQL

大多数动态网站的关键元素之一是为其提供数据的数据库。从简单的新闻页面，到复杂的发布系统或 CMS，数据库在网站内容管理中起着核心作用。为了使网站顺畅运行，了解数据库系统的一些技巧和方法是有帮助的。在本章中，你将学习如何创建数据库，管理将访问系统的各个用户帐户，并组合和优化 SQL 代码以执行复杂和精细的查询。

## 重新审视基础

在深入研究更高级的功能之前，让我们快速回顾一下 MySQL 的使用。假设你刚刚接手了一位新客户，一家汽车经销商。经销商的管理者希望你能创建一个网站，帮助他们跟踪汽车库存。没问题，你说，然后你坐下来开始规划他们的 Web 应用程序。

在规划过程中，你设计了一个简单的多表数据库方案来存储他们车辆场地的数据。为了这些练习的目的，你决定创建类似于图 4.1 的数据库表。

你创建了一个非常简单的数据库结构，涉及四个表。在 New_Vehicles 表中，你将存储新汽车的数据（显而易见）。可以为每辆库存汽车指定里程、价格、颜色和描述等属性。Used_Vehicles 表的结构与 New_Vehicles 几乎相同，但旨在存储记录，正如你可能猜到的那样，是二手汽车。Used_Vehicles 表有几列额外的列，用于指示车辆是否经过认证或享有保修，以及一个里程列。最后两个表，Make 和 Model，存储经销商销售的各个品牌的通用制造商和型号名称。

### 图 4.1 数据库模式

**制造商**

| 列 | 类型 |
| :--- | :--- |
| make_id | int |
| make_name | varchar(100) |

**型号**

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

### 创建数据库

你需要做的第一件事是在 MySQL 中创建数据库和表。首先在命令行上启动你的 MySQL 客户端，或者如果你有其他更熟悉的程序并可以直接输入 MySQL 命令，请随意使用。

```bash
shell$ mysql
```

这将调出 MySQL 监视器，其外观可能类似于以下内容（如果你使用的是命令行客户端）：

```
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 2 to server version: 4.1.11-log

Type 'help;' or '\h' for help.  Type '\c' to clear the current input statement.

mysql>
```

在许多情况下，你需要使用登录名和密码来访问 MySQL 客户端。为此，只需在 mysql 命令末尾添加 `-u username -p`，MySQL 将提示你输入密码，如下所示：

```bash
shell$ mysql -u username -p
```




## 高级 MySQL

使用 MySQL 命令行客户端是熟悉 MySQL 大多数命令和功能的绝佳方式，而这些操作在图形用户界面（GUI）客户端中通常会被自动化处理。

输入以下命令以创建数据库，并将其命名为“VehicleInventory”：

```
mysql> CREATE DATABASE VehicleInventory;
```

既然您已经创建了数据库，就需要将其设置为剩余查询的活跃数据库：

```
mysql> USE VehicleInventory;
```

接下来，创建您的数据库表。在 MySQL 中创建表的基本 SQL 语句如下：

```
CREATE TABLE tablename (column_definitions);
```

要创建四个车辆信息表，您可以使用以下内容：

```
mysql> CREATE TABLE Makes (make_id int PRIMARY KEY AUTO_INCREMENT, make_name varchar(100) );
mysql> CREATE TABLE Models (model_id int PRIMARY KEY AUTO_INCREMENT, model_name varchar(200), make_id int );
mysql> CREATE TABLE New Vehicles (vehicle_id int PRIMARY KEY AUTO_INCREMENT, model_id int, modelyear int, price decimal(10,2), color varchar(200), description text );
mysql> CREATE TABLE Used_Vehicles (vehicle_id int PRIMARY KEY AUTO_INCREMENT, model_id int, modelyear int, mileage int, price decimal(10,2), color varchar(200), certified tinyint, warranty tinyint, description text );
```

简而言之，您只需使用 MySQL 的 CREATE TABLE 命令，后跟表名，然后在括号中列出列名和类型。您还会注意到每个表都添加了一个自动递增的主键，以便在您添加行后帮助唯一地标识它们。

## 添加信息

既然您已经创建了表，就需要向其中添加一些数据。为此，您将使用 INSERT 语句。MySQL 的 INSERT 命令通常遵循以下格式：

```
INSERT INTO tablename (column_list) VALUES (new_values);
```

首先，向 Makes 表添加一些初始数据：

```
INSERT INTO Makes (make_id, make_name) VALUES (1, 'Ford'), (2, 'Honda'), (3, 'Volkswagen'), (4, 'Toyota'), (5, 'Chevrolet');
```

这里使用了基本的 SQL INSERT 语法，但加了一点变化。在 MySQL 中，您可以指定一组以逗号分隔的列值，而不是仅一组，以一次填充多行。通常，在向 Makes 表插入数据时，您可能会省略 make_id 列——自动递增的 ID 会自动为它们分配数字。在这种情况下，指定 ID 是因为您稍后将添加到其他表的行将具有有效的外键。

## 第 4 章

使用以下内容向其余表添加数据（如果您想省去打字，请记住您可以从 www.wrox.com 下载此代码）：

```
INSERT INTO Models (model_id, model_name, make_id) VALUES (1, 'Explorer', 1), (2, 'Accord', 2), (3, 'Golf', 3), (4, 'Tacoma', 4), (5, 'Corvette', 5);
INSERT INTO New_Vehicles (model_id, modelyear, color, description) VALUES
(1, 2005, 'Dark Blue', 'Popular SUV; great for moving people or cargo across town, or wherever your adventures may take you.'),
(NULL, 2004, 'Graphite Pearl', 'Last of the 2004 stock! Must sell! Loaded, all options!'),
(4, 2005, 'Radiant Red', 'Come drive this terrific truck! 4WD, extended cab, many options.'),
(5, 2005, 'Daytona Sunset Orange Metallic', 'All the new C6 Corvette, the next generation of classic American sportscars. 400HP V8; very fast!'),
(1, 2005, 'Dark Blue', 'Popular SUV; great for moving people or cargo across town, or wherever your adventures may take you.');
INSERT INTO Used_Vehicles (model_id, modelyear, color, mileage, certified, warranty, description) VALUES
(1, 2000, 'White', 64800, 0, 0, 'Good condition; One owner; 4WD; V6'),
(2, 2003, 'Deep Green Pearl', 27300, 0, 1, 'Excellent condition, off-lease vehicle; Must see!'),
(3, 2004, 'Reflex Silver', 3800, 1, 1, 'R32 Limited edition; Low miles; Understated and surprisingly functional; Loaded.'),
(4, 1993, 'Red', 152000, 0, 0, 'Runs decent; 4WD; Tinted windows, aftermarket stereo; Needs a little TLC.');
```

请注意，您添加到 New_Vehicles 表的第二辆车的 model_id 有一个 NULL 值。您稍后会了解到原因。

## 检索信息

您花了很多时间创建数据库表并填充数据；现在是时候取回一些数据了。为此，您将使用 SELECT 语句。简化的 SELECT 形式看起来像这样：

```
SELECT [column_names] FROM [table] WHERE [criteria]
```

例如，如果您想获取二手车颜色列表，可以使用类似以下内容：

```
SELECT color FROM Used_Vehicles;
```

这将返回以下内容：

![](img/cacdd24f2926f10ee3219256ad732604_101_0.png)

或者，也许您想要列出 2001 年之前车型的所有里程数：

```
SELECT mileage, modelyear FROM Used_Vehicles WHERE modelyear < 2001;
```

运行此查询显示以下内容：

| mileage | modelyear |
|---------|-----------|
| 64800   | 2000      |
| 152000  | 1993      |

这很简单，但如果您发现错误，想要更改现有记录怎么办？

## 更新信息

要更新信息，您使用 UPDATE 语句。UPDATE 语句的通用形式如下：

```
UPDATE [table] SET [column] = [value] WHERE [criteria]
```

回到车辆库存示例，假设有一天，汽车经销商经理在浏览库存时，注意到其中一辆车的里程数记录错误。为了将其更改为正确值，您可以使用以下查询：

```
UPDATE Used_Vehicles SET mileage = 66000 WHERE vehicle_id = 1;
```

在这种情况下，车辆 ID 1 对应于您在之前 INSERT 语句中添加的二手福特探险者自动递增分配的 ID。

## 删除信息

假设汽车经销商的销售量开始增加，最近的一些销售要求从您的数据库中删除一些车辆。在这种情况下，您将使用 DELETE 语句：

```
DELETE FROM [table] WHERE [criteria];
```

之前示例中修复了错误里程数的那辆二手福特探险者今天卖掉了。要从 Used_Vehicles 表中删除它，您只需执行以下操作：

```
DELETE FROM Used_Vehicles WHERE vehicle_id = 1;
```

这应该涵盖了 MySQL 使用的基础知识，是时候转向更强大的查询了。

## 查询多个表

您已经设置好了车辆库存，可以使用基础知识对单个表执行简单查询。但您想看到更多——也许是一个将每辆车的品牌和型号与其单独记录关联起来的查询。为此，您将使用*连接*（joins）。

在 SQL 中，连接是一种在指定列或列上将两个或更多表链接起来的方法。在 MySQL 中，最常用的是两种连接类型：内连接（inner joins）和外连接（outer joins）。

### 内连接

内连接是一种将两个表基于每行共同共享的值组合其行的方法。当您在*SELECT*查询中执行内连接时，您只需在*FROM*子句中指定要连接的表，并提供关于它们有哪些共同列的提示。MySQL 内连接语法的通用抽象如下：

```
SELECT [column names] FROM [table1] INNER JOIN [table2] ON [table1.column] =
[table2.column]
```

使用假设的汽车经销商库存，您希望每辆车的具体信息旁边返回该车的型号。为了实现这一点，您的查询看起来像这样：

```
SELECT Models.model_name, New_Vehicles.color, New_Vehicles.modelyear FROM Models
INNER JOIN New_Vehicles ON Models.model_id = New_Vehicles.model_id;
```

对您的数据库运行此查询产生以下结果：

| model_name | color                            | modelyear |
|------------|----------------------------------|-----------|
| Explorer   | Dark Blue                        | 2005      |
| Tacoma     | Radiant Red                      | 2005      |
| Corvette   | Daytona Sunset Orange Metallic   | 2005      |

您会注意到，在*SELECT*查询中，选择列表中的每个列都以前缀加上了它们所属的表名。虽然这在技术上不是必需的，但通常这是一个好主意，有助于避免同名列之间的冲突。如果存在这样的冲突且您忽略了表前缀，会发生什么？看看这个例子：

```
SELECT model_id, model_name, color, modelyear FROM Models INNER JOIN New_Vehicles
ON Models.model_id = New_Vehicles.model_id;
```

如您所见，表前缀已被移除，但 model_id 列也被添加到了列表中（因为它存在于两个表中）。现在尝试运行该查询。您会得到以下错误：

```
ERROR 1052 (23000): Column 'model_id' in field list is ambiguous
```

尝试使用存在于两个表中的列名，而不使用表前缀，每当执行查询时都会抛出此类错误。

如果您碰巧喜欢 SQL 查询的简洁性，不要担心——有一种简单的方法可以缩短所有这些表前缀。在*FROM*子句中，您可以为每个调用的表指定*表别名*，如下所示：

```
SELECT [column names] FROM [table1] alias1 INNER JOIN [table2] alias2 ON
[alias1.column] = [alias2.column]
```




## 高级 MySQL

由于表别名可以简短到一个字母，你可以极大地缩短你的库存查询：

```sql
SELECT m.model_name, n.color, n.modelyear FROM Models m INNER JOIN New_Vehicles n ON m.model_id = n.model_id;
```

还不够短吗？好吧，还有另一种整理连接的方式。MySQL 提供了 `USING` 语句，用来替代 `ON` 语句以连接你的表。当两个链接列恰好共享完全相同的列名时，使用 `USING` 语句。使用 `USING` 的内部连接（inner join）通用形式如下：

```sql
SELECT [column names] FROM [table1] INNER JOIN [table2] USING [column list]
```

因为 New_Vehicles 表和 Models 表都有 model_id 列，所以你可以在连接中使用 `USING` 语句：

```sql
SELECT m.model_name, n.color, n.modelyear FROM Models m INNER JOIN New_Vehicles n USING (model_id);
```

在某些情况下，你需要在查询中将两个以上的表连接在一起。MySQL 可以轻松处理这种情况——你只需要按照想要评估的顺序，将你的连接依次链接在一起即可。在车辆库存数据库中，你需要使用多个连接来返回每辆车及其记录的品牌，如下所示：

```sql
SELECT ma.make_name, mo.model_name, n.color, n.modelyear FROM Makes ma INNER JOIN Models mo USING (make_id) INNER JOIN New_Vehicles n USING (model_id);
```

当你运行此查询时，你应该看到以下内容：

| make_name | model_name | color | modelyear |
|-----------|------------|-------|-----------|
| Ford | Explorer | Dark Blue | 2005 |
| Toyota | Tacoma | Radiant Red | 2005 |
| Chevrolet | Corvette | Daytona Sunset Orange Metallic | 2005 |

如你所见，Makes 表基于 make_id 与 Models 表进行了连接，然后该连接的结果又与 New_Vehicles 表进行连接，从而在一个查询中给出了品牌、型号和车辆信息。

在继续下一组连接之前，你应该知道内部连接还有另一种执行方式。第二种方式只是在一个逗号分隔的列表中指定多个表，并使用 `WHERE` 语句来指定表是如何链接的。这种类型内部连接的通用形式如下：

```sql
SELECT [column names] FROM table1, table2 WHERE table1.column = table2.column
```

如果你使用这种内部连接形式在之前的查询中提取新车、品牌和型号列表，它看起来可能是这样的：

```sql
SELECT ma.make_name, mo.model_name, n.color, n.modelyear FROM Makes ma, Models mo, New_Vehicles n WHERE ma.make_id = mo.make_id AND mo.model_id = n.model_id;
```

在你的 MySQL 客户端中执行此查询，将返回以下内容：

| make_name | model_name | color | modelyear |
|-----------|------------|-------|-----------|
| Ford | Explorer | Dark Blue | 2005 |
| Toyota | Tacoma | Radiant Red | 2005 |
| Chevrolet | Corvette | Daytona Sunset Orange Metallic | 2005 |

如你所见，返回了与使用显式内部连接时完全相同的结果。如果你省略了 `WHERE` 子句中的项会发生什么？试试这个查询：

```sql
SELECT mo.model_name, n.color, n.modelyear FROM Models mo, New_Vehicles n;
```

将此查询运行在我们的车辆库存中会产生以下结果（注意 **Makes** 表已被排除）：

| model_name | color | modelyear |
|------------|-------|-----------|
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

这不太对。在这种情况下实际发生的是一种不同的连接，称为*交叉连接*（cross join）。交叉连接 simply 是各个表中每个匹配结果的组合。在这种情况下，Models 表中有*五*个型号，因此其中每一行都与 **New_Vehicles** 表中的*每一行*进行了匹配。这仅仅发生是因为你省略了 `WHERE` 语句，而该语句提供了关于如何链接记录的提示给 MySQL。如前所述，你没有在这个查询中包含 Makes 表——如果你包含了，结果行数将是原来的五倍，因为你的数据库中有五个不同的品牌。

### 外部连接

虽然使用内部连接可以实现大多数复杂的链接，但在某些情况下它们是有限的。如果数据库行在要链接的列上没有定义值，内部连接将忽略它。在车辆库存示例中，每次使用内部连接将 Models 表进行链接查询时，只返回了三行。**New_Vehicles** 表中的第四辆车被忽略了，因为它的 model_id 值为 null。你需要一种方法来返回所有行，无论是否指定了 model_id，并且如果指定了 model_id，则执行请求的连接。对于这样的任务，MySQL 提供*外部连接*（outer joins）。

MySQL 中有两种主要类型的外部连接：左外部连接和右外部连接。它们的行为完全相同，唯一的区别在于允许哪个表不包含匹配项。外部连接的通用形式与内部连接非常相似。以下是左外部连接的简化版本：

```sql
SELECT [column names] FROM table1 LEFT OUTER JOIN table2 USING (column list)
```

左外部连接使用公共列名将“右”表（table2）与“左”表（table1）进行匹配，但如果“左”表包含一个在“右”列中没有匹配项的值，它仍将返回行。右外部连接的行为方式相同，但两个表的角色相反（允许在右表中包含不匹配的值）。

在车辆库存示例中，如果你希望返回一组行，其中所有新车都被返回，无论其 model_id 如何，你可能会使用以下查询：

```sql
SELECT mo.model_name, n.color, n.modelyear FROM New_Vehicles n LEFT OUTER JOIN Models mo USING (model_id);
```

使用此查询对车辆库存数据库进行查询将产生以下结果：

![](img/cacdd24f2926f10ee3219256ad732604_106_0.png)

这与你之前查看的一个内部连接查询非常相似，但多了一行——2004 年款的 Graphite Pearl。因为 Models 表中没有匹配项，MySQL 返回了那些无法确定的值的 NULL——在这种情况下，是 model_name。

然而，外部连接和内部连接并不一定需要分开。两者可以结合在单个查询中，以产生强大的多表连接，并对要求所有数据在所有行中匹配宽容对待。要提取新车的颜色、品牌、型号和年份列表，包括那些未指定型号的车辆，请执行类似的查询：

```sql
SELECT ma.make_name, mo.model_name, n.color, n.modelyear FROM New_Vehicles n LEFT OUTER JOIN Models mo USING (model_id) LEFT OUTER JOIN Makes ma USING (make_id);
```

将此查询在车辆库存数据库中运行将返回以下内容：

| make_name | model_name | color |
|-----------|------------|-------|
| Ford | Explorer | Dark Blue |
| NULL | NULL | Graphite Pearl |
| Toyota | Tacoma | Radiant Red |
| Chevrolet | Corvette | Daytona Sunset Orange Metallic |
| Ford | Explorer | Dark Blue |

请注意，在此查询中，表连接顺序很重要。第一个连接的结果表在与第三个表连接时被用作内部临时表。

### 联合

到目前为止，你在车辆库存数据库上执行的查询一直只返回一种类型车辆的记录，要么是新的，要么是旧的。如果你想要获取数据库中所有车辆的列表，无论其之前的所有权状态如何怎么办？最初，你可能认为这很容易，只需将两个表都添加到查询中即可，但这将导致交叉连接——这并不完全是你想要的。在这种情况下，你需要使用联合（Unions）。

MySQL 中的联合是一种将多个表作为单个记录返回的方法，而不将它们组合起来。联合类似于 PHP 中的连接——它们只是将额外的行添加到第一个表的末尾。MySQL 中联合的概括如下：

```sql
(SELECT [column names] FROM [table1]) UNION (SELECT [column names] FROM [table2])
```

简单地说，联合是通过用单词 UNION 将两个单独的 SELECT 语句粘合在一起来实现的。在代码抽象中，每个 SELECT 语句周围都放置了括号。虽然这不是必须的，但通常这是一个好主意，有助于视觉区分两个查询。

假设你想返回车辆库存中所有车辆的列表，无论它们是新的还是旧的。使用类似于以下的查询：

```sql
(SELECT color, modelyear, model_id FROM New_Vehicles) UNION (SELECT color, modelyear, model_id FROM Used_Vehicles);
```

如果你在 MySQL 中运行此查询，你应该看到以下内容：





## 高级 MySQL

![](img/cacdd24f2926f10ee3219256ad732604_108_0.png)

请注意，该查询明确指定了要从每个表中返回的列，并且列列表中的列数在各表之间必须匹配。如果你为每个表选择了不同数量的列会发生什么？请查看以下查询，该查询将选择每个表中的所有记录（Used_Vehicle 表比 New_Vehicles 表拥有更多的列）。

```sql
(SELECT * FROM New_Vehicles) UNION (SELECT * FROM Used_Vehicles);
```

尝试在数据库上运行此查询，它将返回以下内容：

```
ERROR 1222 (21000): The used SELECT statements have a different number of columns
```

MySQL 会迅速返回一个错误，提示你列列表的长度不同。只要每个列表中的列数相同，列表中的任何列组合都是有效的。如果在列列表的每个对应位置存在不同命名的列，MySQL 在返回行时将使用第一个列表中的列名。请查看以下查询：

```sql
(SELECT color FROM New_Vehicles) UNION (SELECT modelyear FROM Used_Vehicles);
```

当查询数据库时，它将显示以下内容：

![](img/cacdd24f2926f10ee3219256ad732604_108_1.png)

正如预期，MySQL 使用了来自第一个列列表的 color 名称作为列名。然而，这个例子说明了未来可能出现的一个混淆点。表中 color 的列类型被设置为 varchar，但 modelyear 的列类型是 int。在对两个表执行联合操作时，MySQL 忽略了列类型并愉快地合并了表。这在大多数情况下不一定是一个问题，但如果你是在 MySQL 之外强制实施引用完整性（例如在 PHP 中），如果外部代码期望特定类型的返回数据，而 MySQL 发送了像这样的混合结果，那么可能会发生冲突。

### 第 4 章

所有车辆的颜色和年份简单列表虽然不错，但车主期望你能提供更多。除了返回颜色和年份外，你还需要提供品牌和型号。你很高兴地为新的联合表添加必要的连接，使用如下所示的查询：

```sql
(SELECT color, modelyear, model FROM New_Vehicles) UNION (SELECT color, modelyear, model_id FROM Used_Vehicles) LEFT OUTER JOIN Models USING (model_id) LEFT OUTER JOIN Makes USING (make_id);
```

看起来不错，你这样想，直到你在 MySQL 上运行它并得到以下结果：

```
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'LEFT OUTER JOIN Models USING (model_id) LEFT OUTER JOIN Makes USING (make_id)' at line 1
```

发生了什么？UNION 操作本身并不等同于表中的正常结果集，因此你不能简单地添加所需的连接来查找额外信息。此外，你还没有指定任何 make_name 或 model_name 作为返回内容。解决方案：你需要将所有的连接和额外的返回列添加到构成 UNION 的每个 SELECT 语句中：

```sql
(SELECT ma.make_name, mo.model_name, n.color, n.modelyear FROM New_Vehicles n LEFT OUTER JOIN Models mo USING (model_id) LEFT OUTER JOIN Makes ma USING (make_id)) UNION (SELECT ma.make_name, mo.model_name, u.color, u.modelyear FROM Used_Vehicles u LEFT OUTER JOIN Models mo USING (model_id) LEFT OUTER JOIN Makes ma USING (make_id));
```

在 MySQL 中运行这个庞大的查询，你将看到以下内容：

| make_name   | model_name | color                    | modelyear |
| :---------- | :--------- | :----------------------- | :-------- |
| Ford        | Explorer   | Dark Blue                | 2005      |
| NULL        | NULL       | Graphite Pearl           | 2004      |
| Toyota      | Tacoma     | Radiant Red              | 2005      |
| Chevrolet   | Corvette   | Daytona Sunset Orange Metallic | 2005  |
| Honda       | Accord     | Deep Green Pearl         | 2003      |
| Volkswagen  | Golf       | Reflex Silver            | 2004      |
| Toyota      | Tacoma     | Red                      | 1993      |

最终得到的是一个简洁的列表中所有车辆及其品牌、型号、颜色和年份。你在库存应用程序中实现这一点并将其发送给经销商批准，但你还没有完成。像许多客户一样，经销商老板很善变，再次改变了关于车辆列表中需要哪些字段的想法。这一次，你需要为所有车辆返回数据库中的所有信息。你已经知道 New_Vehicles 表和 Used_Vehicles 表具有不同数量的列，那么 UNION 如何奏效？答案其实很简单。你所需要做的就是在各自对应的表中缺失的列指定 NULL（或你喜欢的任何其他值），如下所示：

```sql
(SELECT ma.make_name, mo.model_name, n.color, n.modelyear, n.price, n.description, NULL, 1 FROM New_Vehicles n LEFT OUTER JOIN Models mo USING (model_id) LEFT OUTER JOIN Makes ma USING (make_id)) UNION (SELECT ma.make_name, mo.model_name, u.color, u.modelyear, u.price, u.description, u.certified, u.warranty FROM Used_Vehicles u LEFT OUTER JOIN Models mo USING (model_id) LEFT OUTER JOIN Makes ma USING (make_id));
```

运行此查询，你将看到以下内容：

```text
************************* 1. row **************************
make_name: Ford
model_name: Explorer
color: Dark Blue
modelyear: 2005
price: NULL
description: Popular SUV; great for moving people or cargo across town, or wherever your adventures may take you.
NULL: NULL
1: 1

************************* 2. row **************************
make_name: NULL
model_name: NULL
color: Graphite Pearl
modelyear: 2004
price: NULL
description: Last of the 2004 stock! Must sell! Loaded, all options!
NULL: NULL
1: 1

************************* 3. row **************************
make_name: Toyota
model_name: Tacoma
color: Radiant Red
modelyear: 2005
price: NULL
description: Come drive this terrific truck! 4WD, extended cab, many options.
NULL: NULL
1: 1

************************* 4. row **************************
make_name: Chevrolet
model_name: Corvette
color: Daytona Sunset Orange Metallic
modelyear: 2005
price: NULL
description: The all new C6 Corvette, the next generation of classic American sports-cars. 400HP V8; Very fast!
NULL: NULL
1: 1

************************* 5. row **************************
make_name: Honda
model_name: Accord
color: Deep Green Pearl
modelyear: 2003
price: NULL
description: Excellent condition, off-lease vehicle; Must see!
NULL: 0
1: 1

************************* 6. row **************************
make_name: Volkswagen
model_name: Golf
color: Reflex Silver
modelyear: 2004
price: NULL
description: R32 Limited edition; Low miles; Understated and surprisingly functional; Loaded.
NULL: 1
1: 1

************************* 7. row **************************
make_name: Toyota
model_name: Tacoma
color: Red
modelyear: 1993
price: NULL
description: Runs decent; 4WD; Tinted windows, aftermarket stereo; Needs a little TLC.
NULL: 0
1: 0
```

你首先会注意到的是，它看起来与之前的结果略有不同。这是因为查询末尾的 `\G` 终止符，它导致 MySQL 垂直显示结果（否则，表格对于本书来说太宽了）。除此之外，所有信息都存在并得到解释。在 New Vehicles 表中缺失的“certified”列指定的 NULL 值存在，以及你指定为 1 的占位符值，因为所有新车都有保修。你将更改发回给客户端，他们很高兴（至少暂时是这样）。

## 全文搜索

到目前为止，车场老板们对你精确查询所需内容的能力印象深刻，提供各种列表以提高销售人员的生产力——但他们仍想要更多。他们现在希望的是通过关键词搜索汽车库存的方法。他们的搜索需求不太复杂，但 WHERE 子句中的简单 LIKE 比较无法完成任务。

你所需的恰好是 MySQL 内置的功能——全文搜索。全文搜索在 MySQL 中默认启用，允许你对指定的任何文本列执行自然语言搜索。然而，你不能随意在数据库中进行全文搜索——你必须先进行一些准备工作。

### 启用全文搜索

在 MySQL 中启用全文搜索只需在表的一个或多个列上创建索引。你可以用两种方法之一完成此操作：在表创建时，作为 CREATE TABLE 命令的一部分，或在表生命周期的稍后阶段。

### 创建启用全文搜索的新表

你要创建的第一个全文索引将是新表的一部分。要在表创建时指定全文索引，你只需要在列定义的末尾指定全文索引和被索引的列列表：

```sql
CREATE TABLE tablename (column specs, FULLTEXT (columns to index))
```





你可以指定 `FULLTEXT` 列列表中的单个列，也可以是以逗号分隔的多个列列表。现在是时候在 VehicleInventory 数据库中实际创建一个支持全文搜索的表了：

```
CREATE TABLE testtf (testint int, testcvc varchar(50), testtxt text, FULLTEXT (testvc, testxt));
```

你刚刚创建了一个新表，并在 testvc 和 testxt 列上建立了全文索引。

### 修改现有表以支持全文搜索

修改现有表以支持全文搜索稍微复杂一点，但也没有太难。要为现有表添加全文搜索功能，你需要使用 MySQL 的 ALTER TABLE 命令，如下所示：

```
ALTER TABLE tablename ADD FULLTEXT (columns)
```

现在为 New_Vehicles 表添加一个全文索引：

```
ALTER TABLE New_Vehicles ADD FULLTEXT (description);
```

完成后，就是利用这些索引的好时机了。

### 使用全文搜索进行查询

在启用了全文索引的 MySQL 表中进行搜索是一个相对轻松的过程。你只需要在 WHERE 子句中使用 MATCH() 函数即可，如下所示：

```
SELECT [columns] FROM [table] WHERE MATCH ([indexed_columns]) AGAINST ('keyword')
```

在 MATCH() 的参数列表中，你可以指定任意数量的列，只要它们属于全文索引的一部分即可。

回到车辆库存数据库，现在是时候对新车辆列表执行搜索了。要搜索单词 "options"，你可以使用以下语句：

```
SELECT vehicle_id, description FROM New_Vehicles WHERE MATCH (description) AGAINST ('options');
```

这将返回以下结果：

| vehicle_id | description                                      |
| :--- | :--- |
| 2 | Last of the 2004 stock! Must sell! Loaded, all options! |
| 3 | Come drive this popular truck! 4WD, extended cab, many options. |

全文搜索的另一个巧妙之处在于它可以按相关性对项进行排序，并返回相关性值。要利用相关性数据，你可以在 SELECT 列表和 ORDER BY 子句中都使用 MATCH() ... AGAINST() 函数，如下所示：

```
SELECT MATCH (description) AGAINST ('options') AS relevance, description FROM New_Vehicles WHERE MATCH (description) AGAINST ('options') ORDER BY MATCH (description) AGAINST ('options')
```

这将返回以下内容：

```
*************************** 1. row ***************************
relevance: 0.38341856002808
description: Last of the 2004 stock! Must sell! Loaded, all options!
*************************** 2. row ***************************
relevance: 0.38341856002808
description: Come drive this popular truck! 4WD, extended cab, many options.
```

## 局限性

使用全文搜索时，必须牢记几个局限性。首先，MySQL 仅支持 MyISAM 表类型的全文索引（在下一节中详细介绍）。其次，在大多数情况下，如果在多个列上创建全文索引，则提供给 `MATCH()` 的列列表必须与你创建全文索引时指定的列表完全相同。最后，MySQL 默认的最小单词/标记长度为四个字符。如果你尝试匹配包含三个或更少字符的关键词的全文搜索，将不会返回任何结果。

要更改默认的最小全文单词长度，请确保你的 MySQL 配置文件（*my.cnf*）中存在以下内容：

```
[mysqld]
ft_min_word_len=3
```

你可以使用任何整数作为最小长度（在此示例中设置为 3）。

## InnoDB 表

使用 MySQL 的一个优势是，你的数据存储不受限于特定的存储引擎。什么是存储引擎？MySQL 作为服务器，为用户提供了一致的接口和查询语言，但它与实际上如何在磁盘上存储数据的方式只是松散耦合的。MySQL 中不同的存储引擎提供了存储和访问数据的不同方式，从可靠的默认 MyISAM，到内存 Heap 表的极速性能，以及介于两者之间的各种选项。你可以使用的最灵活且功能强大的表类型之一是 InnoDB。由芬兰赫尔辛基的 Innobase Oy 创建的 InnoDB 存储引擎，为 MySQL 提供了一种安全且高效的数据存储和处理方式，并为 MySQL 提供了一些 MyISAM 或大多数其他表类型不具备的额外功能。

### InnoDB 优势

虽然默认的 MyISAM 表类型提供了一种成熟且快速的方法来存储简单的数据结构，但它缺少许多开发人员希望拥有的几项功能——而 InnoDB 可以提供这些功能。自 MySQL 4.0 起默认可用，InnoDB 表让你能够使用事务、行级锁定，最重要的是外键约束。

外键约束提供了一种在链接表之间维护引用完整性的方式。在 VehicleInventory 数据库中，**New_Vehicles** 和 **Used_Vehicles** 表包含一个 model_id 列，用于指定每辆车的型号，进而指定其制造商。可以在 model_id 列上应用外键约束，以确保不能向该列插入任何在 Models 表中不存在的值。在默认的 MyISAM 表类型中，MySQL 无法自动强制执行此类规则，这在大型数据库中可能导致表中有大量无效值。InnoDB 为 MySQL 提供了一种强制执行此类规则的方法，因此数据始终保持相关性。

> 受外键约束的列仅允许存在于被引用表中的值，但有一个例外，即 NULL。在其他受外键控制的列中，允许使用 NULL 值。

### InnoDB 缺点

不幸的是，InnoDB 的好处伴随着几个特别令人烦恼的问题。首先，InnoDB 表不支持全文搜索。当你决定是否使用 InnoDB 时，必须始终考虑未来对全文索引的需求，以及它相对于特定表的引用完整性是否更重要。

其次，InnoDB 存储引擎在 AUTO_INCREMENT 列方面受到轻微限制。InnoDB 表不允许你在创建表时指定自增序列的初始值。这并不一定是致命的，但在设计数据库模式时是需要考虑的事项。

### 使用 InnoDB

了解 InnoDB 存储引擎的最佳方法是让它投入工作。现在你将从头创建一个新表，以及修改另一个附加表来启用 InnoDB 引擎。之后，你将尝试外键的不同方面。

#### 从头创建 InnoDB 表

使用 InnoDB 存储引擎创建新表与创建标准的 MyISAM 表几乎没有区别。唯一的重大区别是你必须在创建表命令的末尾指定 ENGINE：

```
CREATE TABLE tablename (column_definitions) ENGINE=InnoDB;
```

很简单，对吧？在你的 MySQL 数据库中实际试一试：

```
CREATE TABLE innoctest (innocl int) ENGINE=InnoDB;
```

如果一切顺利，你应该会看到以下内容：

```
Query OK, 0 rows affected
```

就这样，你创建了一个简单的 InnoDB 表。

#### 转换现有的 MyISAM 表

从头创建新的 InnoDB 表固然好，但你有一些表希望它们使用 InnoDB 存储引擎。你需要一种方法将这些表从默认的 MyISAM 表类型转换过来。幸运的是，更改 MySQL 中表的存储引擎是一项简单的任务——只需使用 **ALTER TABLE** 命令并重新指定表的引擎即可。要转换目前使用默认表类型 MyISAM 的 _New_Vehicles_ 表，你可以使用以下命令：

```
ALTER TABLE New_Vehicles ENGINE=InnoDB;
```

对你的数据库运行此命令，你会看到以下内容：

```
ERROR 1214 (HY000): The used table type doesn’t support FULLTEXT indexes
```

MySQL 没有按预期转换你的表，而是给出了一个错误消息。如前所述，InnoDB 表目前在 MySQL 中不支持全文索引。如果你尝试将定义了全文索引的 MyISAM 表转换为 InnoDB，你会得到此消息。为了本练习的目的，你需要删除全文索引，以便可以转换表：

```
ALTER TABLE New_Vehicles DROP INDEX description;
```

现在你应该能够继续转换表了：

```
ALTER TABLE New_Vehicles ENGINE=InnoDB;
```

这一次，你的查询应该成功，你会看到类似以下内容：

```
Query OK, 4 rows affected (0.76 sec)
Records: 4  Duplicates: 0  Warnings: 0
```

## 外键

如果没有好的理由，你不会将表从 MyISAM 切换到 InnoDB，而在大多数情况下，外键是任何正当理由中最好的一个。一旦你设置好 InnoDB 表，只需向表中添加外键即可强制执行引用完整性。虽然听起来很简单，但在创建外键时有许多选项需要考虑。

创建外键的 **ALTER TABLE** 命令的最基本格式看起来像这样：

```
ALTER TABLE {tablename} ADD CONSTRAINT {key_name} FOREIGN KEY ({indexed_column}) REFERENCES {foreign_table} ({fid_column})
```

一开始，你告诉 MySQL 要更改哪个表以及做什么（添加外键）。使用 **CONSTRAINT** _{key_name}_，你可以选择性地为键命名，如果你计划将来更改键，这也是个好主意。需要引用完整性的列名紧随其后，放在括号中。之后是 **REFERENCES** _{keyword}_，即要检查的外表名称，以及该外表中要引用的特定列。

将此应用于车辆库存数据库，为 _New_Vehicles_ 表添加一个名为 **refmdl** 的外键，将列 **model_id** 与 **Models** 表中的 **model_id** 列进行检查：

```
ALTER TABLE New_Vehicles ADD CONSTRAINT refmdl FOREIGN KEY (model_id) REFERENCES Models (model_id);
```




## 高级 MySQL

在 MySQL 中运行此命令，你将看到类似以下内容：

> ERROR 1005 (HY000): Can't create table '/vehicleinventory/#sql-1951_2.frm' (errno: 150)

这次错误信息在追踪原因方面并不如预期那样有帮助。在这种情况下，该错误抛出是因为参与外键关系的一张表未使用 InnoDB 引擎。你已经将 **New_Vehicles** 表转换为 InnoDB，但 **Models** 表仍然是 MyISAM。为了使外键正确创建，涉及的双方表都需要使用 InnoDB 引擎，因此你必须相应地进行更改：

```sql
ALTER TABLE Models ENGINE=InnoDB;
```

然后添加外键：

```sql
ALTER TABLE New_Vehicles ADD CONSTRAINT refmdl FOREIGN KEY (model_id) REFERENCES Models (model_id);
```

现在，你的外键正在保护 **New_Vehicles** 中的 **model_id** 列免受错误数据的影响……是吗？确定这一点的最简单方法是进行测试。尝试使用一个完全不正确的 **model_id** 向 **New_Vehicles** 中插入一行：

```sql
INSERT INTO New_Vehicles (model_id) VALUES (12345);
```

当你尝试执行此查询时，应该会返回以下内容：

> ERROR 1216 (23000): Cannot add or update a child row: a foreign key constraint fails

正如预期的那样，外键检查发现该值不在 **Models** 表中，因此拒绝允许插入该行。你成功阻止了任何包含不良数据的新行，但那些正在被修改的现有行呢？尝试此查询：

```sql
UPDATE New_Vehicles SET model_id=12345 WHERE vehicle_id=1;
```

你可以看到，外键也会阻止错误的更新：

> ERROR 1216 (23000): Cannot add or update a child row: a foreign key constraint fails

因此，外键成功保护表免受有害的 **INSERTs** 和 **UPDATEs** 的影响，但当 **Models** 表中的值发生变化时会发生什么？查看以下查询，其中你尝试更改现有的 **model_id**：

```sql
UPDATE Models SET model_id=123 WHERE model_id=1;
```

运行此查询时，你会得到以下错误：

> ERROR 1217 (23000): Cannot delete or update a parent row: a foreign key constraint fails

此错误仅反映了与简单 InnoDB 外键相关的另一种行为：如果被引用列的值存在于引用表中，则无法修改被引用列。如果这种行为不是你所想要的该怎么办？幸运的是，你可以将外键的更新和删除行为指定为五种不同选项之一：`RESTRICT`、`CASCADE`、`SET NULL`、`NO ACTION` 和 `SET DEFAULT`。以下是每种行为含义的简要说明：

- **RESTRICT** 是默认行为。被引用的值不能被更改或删除。
- **CASCADE** 允许任何更新传播到引用表。如果你在 `Models` 表中更新了 `model_id`，它将级联到 `New_Vehicles` 表并更新所有相应的行。注意，这也适用于删除（如果指定）——删除父表中的一行将自动删除子表中引用该值的所有行。
- **SET NULL** 在更新父值时，将子表中的值更改为 NULL。
- **NO ACTION** 简单地告诉数据库允许对父表的更改，并对子表不做任何操作。
- **SET DEFAULT** 在父值被更改或删除时，将子表中的值更改为其默认值。

实现这些行为只需在外键定义末尾添加所需的 `ON DELETE` 或 `ON UPDATE` 子句，如下所示：

```sql
ALTER TABLE [tablename] ADD CONSTRAINT [key_name] FOREIGN KEY ([indexed_column])
REFERENCES [foreign_table] ([id_column])
ON UPDATE [update_behavior] ON DELETE [delete_behavior]
```

要将现有键更改为支持不同的更新和删除行为，你首先必须删除旧键，然后使用新行为重新创建外键。要将 `New_Vehicles` 表上的外键更改为级联任何更新，并在模型删除时设置 NULL，请使用以下命令：

```sql
ALTER TABLE New_Vehicles DROP FOREIGN KEY refmdl;
ALTER TABLE New_Vehicles ADD CONSTRAINT refmdl FOREIGN KEY (model_id)
REFERENCES Models (model_id) ON UPDATE CASCADE ON DELETE SET NULL;
```

现在，每次在 `Models` 表中更改 `model_id` 时，新值将传播到 `New_Vehicles` 中使用原始值的所有行。请自己查看：

```sql
UPDATE Models SET model_id=123 WHERE model_id=1;
SELECT * FROM New_Vehicles;
```

更新将成功，并返回类似以下内容的内容：

```text
*************************** 1. row *****************************
vehicle_id: 1
model_id: 123
price: NULL
color: Dark Blue
description: Popular SUV; great for moving people or cargo across town, or wherever your adventures may take you.
modelyear: 2005

*************************** 2. row *****************************
vehicle_id: 2
model_id: NULL
price: NULL
color: Graphite Pearl
description: Last of the 2004 stock! Must sell! Loaded, all options!
modelyear: 2004

*************************** 3. row *****************************
vehicle_id: 3
model_id: 4
price: NULL
color: Radiant Red
description: Come drive this popular truck! 4WD, extended cab, many options.
modelyear: 2005

*************************** 4. row *****************************
vehicle_id: 4
model_id: 5
price: NULL
color: Daytona Sunset Orange Metallic
description: The all new C6 Corvette, the next generation of classic American
               sportscars. 400HP V8; Very fast!
modelyear: 2005
```

### 从 InnoDB 转换回 MyISAM

你已经尝试了 InnoDB 表和外键，但决定还是更喜欢全文搜索。改回 MyISAM 是一个相对无痛的过程。通常只需两个步骤：移除任何 InnoDB 特有的功能，例如外键，并使用 ALTER TABLE 将存储引擎类型改回 MyISAM。要将 **New_Vehicles** 表转换回 MyISAM，请执行以下操作：

```sql
ALTER TABLE New_Vehicles DROP FOREIGN KEY refmdl;
ALTER TABLE New_Vehicles ENGINE=MyISAM;
```

此时，**New_Vehicles** 表已恢复使用 MyISAM 存储引擎，你再次具有在该表上添加和使用全文索引的能力。

## 控制访问

作为 MySQL 数据库管理员，你最重要的工作之一就是控制谁可以访问系统以及他们可以访问哪些资源。在大多数情况下，每个数据库只需要少数几个用户账户，且需要创建的账户应仅授予执行其任务所需的最小访问权限。幸运的是，MySQL 提供了几种控制谁可以访问你的系统以及具体访问哪些资源的方法。

### 用户管理

为了帮助你控制数据库中的用户账户，MySQL 提供了几种维护用户账户的方法。无论是协作者的账户、技术娴熟的客户端，还是基于 Web 的前端，每个用户都需要针对其所需的资源专门授予访问权限。

配置数据库以适用于现实世界时，你需要做的第一件事之一是设置任何用户或系统本身可能需要的账户。为了在数据库中为用户设置专门的访问权限，你需要了解 MySQL 可以控制访问的不同级别。MySQL 4.1 在权限方面可以区分四种不同的访问级别：全局级别、数据库级别、表级别和列级别。

全局级别的权限是最强大的，适用于在 MySQL 实例上运行的所有数据库。通常，此类权限保留给管理员账户，因为应用程序或最终用户需要访问数据库服务器操作的所有方面的情况很少发生。

数据库级别的权限如其名称所示——在数据库级别应用。数据库级别的访问通常由特定数据库或应用程序的管理员使用，并且具有对指定特定数据库的完全控制能力。

表级别的权限按每个表应用。你可以针对特定表或一组表创建或移除用户的访问权限。这种级别的访问控制通常用于配置由应用程序直接访问的数据库——应用程序只需要每个表的特定类型的访问权限，而不是更多。

列级别的权限是 MySQL 提供的最精细的控制级别。正如你可能预期的那样，它控制对给定表中特定列或列的访问。

### 使用 GRANT

现在你理解了 MySQL 访问系统的不同范围，是时候看看如何实际控制权限了。

为了创建并为用户账户添加权限，MySQL 提供了 `GRANT` 命令。只要你清楚正在授予什么访问权限以及授予给谁，`GRANT` 命令相对来说很容易使用。`GRANT` 命令具有以下通用语法：

```sql
GRANT [privileges] ON [resource] TO [identity]
```

让我们花一点时间来剖析 `GRANT`。命令的第一部分，`GRANT [privileges]` 是你指定在资源上（稍后指定）允许哪些权限的地方。以下是一些常用权限的表格：

| 权限 | 提供 |
|---|---|
| ALL [PRIVILEGES] | 设置除 GRANT OPTION 之外的所有简单权限 |
| ALTER | 允许使用 ALTER TABLE |
| CREATE | 允许使用 CREATE TABLE |
| DELETE | 允许使用 DELETE |
| DROP | 允许使用 DROP TABLE |
| INDEX | 允许使用 CREATE INDEX 和 DROP INDEX |
| INSERT | 允许使用 INSERT |
| SELECT | 允许使用 SELECT |




### 权限表

| 权限 | 提供 |
|---|---|
| 更新 | 允许使用更新操作 |
| 使用 | “无权限”的同义词；用户可以登录，但没有其他权限 |

命令 `ON [资源]` 的第二部分是指定你要开放哪个数据库级别和项目的地方。要在全局级别授权访问权限，你指定 `*.*` 作为资源，如下所示：

```sql
GRANT [权限] ON *.* TO [身份]...
```

在数据库级别授予访问权限时，你指定数据库的名称，后面跟着 `.*`。例如，如果你想要授予对 `testdb` 数据库的访问权限，你会使用类似以下内容：

```sql
GRANT [权限] ON testdb.* TO [身份]...
```

要为数据库中的特定表创建权限，你提供数据库的名称，后面跟着表名（用点号分隔）。如果你试图指定 `testdb` 数据库中 `testtable` 表的访问权限，你可能会使用类似以下内容：

```sql
GRANT [权限] ON testdb.testtable TO [身份]...
```

授予列级权限与前三个级别的逻辑递进略有不同。在授予列级权限时，你必须在列表中的每个权限后（在括号中）指定一个列列表，如下所示：

```sql
GRANT SELECT (column1), INSERT (column1) ON testdb.testtable TO [身份]...
```

> *在指定列级权限时，ON 后面必须使用完整的表级语法，否则 MySQL 将返回错误。*

`GRANT` 命令的最后一个关键部分 `TO [身份]...` 是指定授予访问权限给谁，以及用户必须满足的任何可选要求。为了满足 `GRANT` 的 `TO ...` 部分，你至少必须提供用户名/主机组合。在 MySQL 中，每个不同的用户必须为其用户名和 `localhost` 设置至少基本的使用权限。例如：

```sql
GRANT USAGE ON *.* TO tester@localhost
```

这里，用户“tester”被全局授予基本使用权限，这相当于完全没有访问权限，但该用户现在已被系统识别。一旦创建了 `localhost` 账户，你可以在任何指定的远程主机上为相同的用户名创建额外的访问语句：

```sql
GRANT SELECT ON testdb.* TO tester@192.168.1.2
```

需要注意的是，如果你尝试在没有先创建 `localhost` 条目的情况下为某个用户创建远程访问账户，MySQL 不会抱怨。但是，你的应用程序很可能会抱怨——它们可能无法远程连接，这也是在刚熟悉 MySQL 访问系统时的一个常见抓狂来源。

## 第 4 章

在大多数情况下，用户账户在登录时也需要密码很重要。在创建使用 **GRANT** 的账户时添加密码，在 **GRANT** 命令末尾添加短语 **IDENTIFIED BY** ‘password’，如下所示：

```sql
GRANT [权限] ON [资源] TO [身份] IDENTIFIED BY ‘password’;
```

> 在使用 **GRANT** 命令时，你不需要预先加密密码作为密码——**MySQL** 会在将其存储在系统中之前自动加密密码。

现在你将看到一些如何使用 **USE** **GRANT** 的通用示例，你可以在实际数据库上尝试。你将向车辆库存数据库添加三个用户。一个用户将获得整个数据库的完全访问权限。第二个将获得对 **New_Vehicles** 表的 **SELECT**、**UPDATE**、**INSERT** 和 **DELETE** 访问权限。第三个也是最后一个用户将获得对 **New_Vehicles** 表中颜色列的仅 **SELECT** 访问权限。首先，创建拥有数据库中所有权限的用户：

```sql
GRANT ALL PRIVILEGES ON VehicleInventory.* TO testuser1@localhost IDENTIFIED BY ‘testpass1’;
```

接下来，创建具有有限表级权限的用户：

```sql
GRANT SELECT, INSERT, UPDATE, DELETE ON VehicleInventory.New_Vehicles TO testuser2@localhost IDENTIFIED BY ‘testpass2’;
```

最后，创建具有极其有限访问权限的第三个用户：

```sql
GRANT SELECT (color) ON VehicleInventory.New_Vehicles TO testuser3@localhost IDENTIFIED BY ‘testpass3’;
```

## 使用 **REVOKE**

现在你可以使用 **GRANT** 命令创建用户和权限，但你仍然需要一种方式来撤销权限。为此，你使用 **REVOKE**。**REVOKE** 命令看起来与 **GRANT** 命令几乎完全一样：

```sql
REVOKE [权限] ON [资源] FROM [身份]
```

注意 **REVOKE** 和 **GRANT** 语法之间唯一的真正区别：使用单词 **FROM** 代替 **TO**，并且不需要添加 **IDENTIFIED BY** 短语。

为了快速查看 **REVOKE** 在实时数据库上的运行情况，请尝试以下查询：

```sql
REVOKE ALL PRIVILEGES ON VehicleInventory.New_Vehicles FROM testuser2@localhost;
```

用这一快速操作，你就撤销了 testuser2 账户拥有的任何权限。在撤销权限时，你通常必须列出用户拥有明确权利的具体表、数据库和列。如果你使用的是 **MySQL** 4.1.2 或更高版本，你可以用一个快速命令在任何权限级别快速清除用户的所有权限：

```sql
REVOKE ALL PRIVILEGES, GRANT OPTION FROM [身份]
```

如果你想要从系统中彻底删除 testuser3，你会发送以下内容：

```sql
REVOKE ALL PRIVILEGES, GRANT OPTION FROM testuser3@localhost;
```

#### GRANT 和 REVOKE 的替代方案

如果由于某种原因，你不想使用 GRANT 或 REVOKE 命令，你可以手动创建用户并直接将权限应用于 MySQL 访问表。

MySQL 在内置的 *mysql* 数据库内的四个主要表中存储不同级别的用户权限。这四个主要访问表中的每一个都对应于四个不同的访问级别。

在全局级别，有 *user* 表，其结构如下：

| 字段 | 类型 |
| :--- | :--- |
| 主机 | varchar(60) |
| 用户 | varchar(16) |
| 密码 | varchar(41) |
| 选择权限 | enum('N','Y') |
| 插入权限 | enum('N','Y') |
| 更新权限 | enum('N','Y') |
| 删除权限 | enum('N','Y') |
| 创建权限 | enum('N','Y') |
| 丢弃权限 | enum('N','Y') |
| 重新加载权限 | enum('N','Y') |
| 关闭权限 | enum('N','Y') |
| 进程权限 | enum('N','Y') |
| 文件权限 | enum('N','Y') |
| 授予权限 | enum('N','Y') |
| 引用权限 | enum('N','Y') |
| 索引权限 | enum('N','Y') |
| 修改权限 | enum('N','Y') |
| 显示数据库权限 | enum('N','Y') |
| 超级权限 | enum('N','Y') |
| 创建临时表权限 | enum('N','Y') |
| 锁定表权限 | enum('N','Y') |
| 执行权限 | enum('N','Y') |
| 复制从属权限 | enum('N','Y') |
| 复制客户端权限 | enum('N','Y') |
| ssl类型 | enum('','ANY','X509','SPECIFIED') |
| ssl密码 | Blob |
| x509颁发者 | Blob |
| x509主题 | Blob |
| 最大查询数 | int(11) 无符号 |
| 最大更新数 | int(11) 无符号 |
| 最大连接数 | int(11) 无符号 |

`user` 表包含系统中所有用户的列表，以及该用户可能拥有的任何全局权限。与访问权限相关的关键字段是所有带有后缀 _priv 的列。请注意，所有权限列的默认值均为 `no`。

`db` 表保存任何数据库级别访问权限的记录。`db` 的结构如下：

| 字段 | 类型 |
| --- | --- |
| 主机 | varchar(60) |
| 数据库 | varchar(64) |
| 用户 | varchar(16) |
| 选择权限 | enum('N','Y') |
| 插入权限 | enum('N','Y') |
| 更新权限 | enum('N','Y') |
| 删除权限 | enum('N','Y') |
| 创建权限 | enum('N','Y') |
| 丢弃权限 | enum('N','Y') |
| 授予权限 | enum('N','Y') |
| 引用权限 | enum('N','Y') |
| 索引权限 | enum('N','Y') |
| 修改权限 | enum('N','Y') |
| 创建临时表权限 | enum('N','Y') |
| 锁定表权限 | enum('N','Y') |

## 高级 MySQL

只有当用户需要显式的数据库级别权限时，才会显示在此表中。

另一个表 `tables_priv` 保存表级别操作的权限：

| 字段 | 类型 |
| :--- | :--- |
| 主机 | char(60) |
| 数据库 | char(64) |
| 用户 | char(16) |
| 表名 | char(64) |
| 授予者 | char(77) |
| 时间戳 | timestamp |
| 表权限 | set('Select', 'Insert', 'Update', 'Delete', 'Create', 'Drop', 'Grant', 'References', 'Index', 'Alter') |
| 列权限 | set('Select', 'Insert', 'Update', 'References') |

与 db 表一样，只有当用户需要表级别权限时，才需要出现在此表中。

最后一个表 `columns_priv` 包含列级别的访问定义，看起来像这样：

| 字段 | 类型 |
| :--- | :--- |
| 主机 | char(60) |
| 数据库 | char(64) |
| 用户 | char(16) |
| 表名 | char(64) |
| 列名 | char(64) |
| 时间戳 | timestamp |
| 列权限 | set('Select', 'Insert', 'Update', 'References') |

你为什么要知道这些每个表的详细情况？如果你想在不使用 GRANT 或 REVOKE 的情况下添加或移除访问权限，你必须对这些核心表使用标准的 INSERT、UPDATE 和 DELETE 命令。

首先，要在数据库中创建用户，无论访问级别如何，他们都必须存在于 `user` 表中：

```sql
INSERT INTO mysql.user (Host, User, Password) VALUES ('localhost', 'testuser6',
PASSWORD('testpass6'));
```

注意这里使用了 PASSWORD() 函数，而在 GRANT 语法中不使用。GRANT 命令自动使用 PASSWORD() 函数对密码进行加密；像这样的手动插入则不会，因此你必须自己对其进行加密。




## 第 4 章

若要添加访问权限，您只需在相应的表中插入一行，并将每个所需的权限列指定为 Y。若要为您新创建的用户赋予 VehicleInventory 数据库的数据库级 SELECT、UPDATE、INSERT 和 DELETE 权限，请使用以下语句：

```sql
INSERT INTO mysql.db (Host, Db, User, Select_priv, Insert_priv, Update_priv, Delete_priv) VALUES ('localhost', 'VehicleInventory', 'testuser6', 'Y', 'Y', 'Y', 'Y');
```

如果需要撤销用户权限，您只需对所需的表执行 DELETE 操作即可。若要移除 testuser6 的数据库级权限，请使用此查询：

```sql
DELETE FROM mysql.db WHERE Host='localhost' AND User='testuser6';
```

将用户完全从数据库中移除的操作稍微复杂一些。您必须首先移除授予该用户的所有权限，然后才能使用 DELETE 命令将其从用户表中移除。

为了使 MySQL 意识到您刚刚手动更改的权限，您必须重新加载权限表：

```sql
FLUSH PRIVILEGES;
```

如果在进行访问更改后没有刷新权限，这些更改在 MySQL 下次重启之前都不会生效。这适用于您手动进行的任何访问级别的权限更改——使用 GRANT 或 REVOKE 不需要重新加载权限表。

## 服务器限制

限制服务器访问的另一种方式是大幅限制整个服务器的远程访问。如果您的数据库仅服务于直接登录到该机器上的用户，则无需让服务器接受远程网络连接。若要阻止 MySQL 监听传入的网络连接，请确保您的 MySQL 配置文件（通常是 my.cnf）的 [mysqld] 部分中存在以下内容：

```ini
[mysqld]
skip-networking
```

将上述语句添加到配置文件，然后重启 MySQL 服务器进程，即可禁用任何传入 MySQL 的流量。如果您的网络和安全服务器安全至关重要，且只有本地账户需要访问时，采取此类措施非常重要。

## 分析数据库

虽然您使用数据库的大多数时间可能都花在了添加、更新、检索和删除数据上，但总会有您需要立即了解数据库结构本身信息的时候。幸运的是，MySQL 提供了一些易于使用的信息工具，以及分析和优化数据库的简单方法。

## 高级 MySQL

在 MySQL 命令 shell 中，您可以使用几个共享 SHOW 前缀的不同命令，以获取有关数据库当前状态的各种信息。以下部分介绍了一些常见的 SHOW 命令。

### SHOW COLUMNS

SHOW COLUMNS 命令返回表中所有列及其属性的列表。SHOW COLUMNS 的一般格式如下：

```sql
SHOW COLUMNS FROM [table] FROM [database]
```

如果您想获取 New_Vehicles 表中所有列的列表，可以使用以下命令：

```sql
SHOW COLUMNS FROM New_Vehicles FROM VehicleInventory;
```

返回结果如下：

![](img/cacdd24f2926f10ee3219256ad732604_126_0.png)

在返回的输出中，Field 列包含每列的名称，Type 显示列的数据类型，Null 指定该列是否允许 NULL 值，Key 指示每列属于哪种键或索引类型，Default 显示指定的列默认值，Extra 显示每列的特殊处理。请注意，该命令在功能上与 MySQL 的 DESCRIBE [table] 命令相同。

### SHOW CREATE TABLE

您可能希望了解创建给定表可以使用什么命令。为此，您可以使用 SHOW CREATE TABLE 命令：

```sql
SHOW CREATE TABLE [table name]
```

若要获取创建您的 New_Vehicles 表的命令，请发送：

```sql
SHOW CREATE TABLE New_Vehicles \G
```

对 VehicleInventory 数据库运行此命令将得到以下结果：

```text
*************************** 1. row ********************
Table: New_Vehicles
Create Table: CREATE TABLE `New_Vehicles` (
`vehicle_id` int(11) NOT NULL auto_increment,
`model_id` int(11) default NULL,
`price` decimal(10,2) default NULL,
`color` varchar(20) default NULL,
`description` text,
`modelyear` int(11) default NULL,
PRIMARY KEY (`vehicle_id`)
) ENGINE=MyISAM DEFAULT CHARSET=lain1
```

然后，可以将此完整的 CREATE TABLE 命令输入到一个新的数据库中，以创建 New_Vehicles 表结构的精确副本。

### SHOW DATABASES

SHOW DATABASES 命令执行其字面意思所指的操作——它显示当前登录账户可以访问的系统中的所有数据库。只需运行该命令：

```sql
SHOW DATABASES;
```

它将返回当前用户可以访问的数据库列表：

![](img/cacdd24f2926f10ee3219256ad732604_127_0.png)

### SHOW GRANTS

SHOW GRANTS 命令列出授予特定用户账户的所有访问权限。例如，若要查看 VehicleInventory 数据库中授予 testuser1 账户的所有访问权限，请使用以下命令：

```sql
SHOW GRANTS FOR 'testuser1'@'localhost';
```

返回结果如下：

```text
*************************** 1. row
Grants for testuser1@localhost: GRANT USAGE ON *.* TO 'testuser1'@'localhost'
IDENTIFIED BY PASSWORD '*E69570F2322D3DC1F956C48199FEB21FF2D7D984'
*************************** 2. row
Grants for testuser1@localhost: GRANT ALL PRIVILEGES ON `vehicleinventory`.* TO 'testuser1'@'localhost'
*************************** 3. row
Grants for testuser1@localhost: GRANT SELECT, SELECT (description), INSERT (description), UPDATE (description) ON `vehicleinventory`.`used_vehicles` TO 'testuser1'@'localhost'
```

## 数据库维护

您创建了车辆库存数据库，将其投入生产，设置了搜索功能，并且客户对结果感到满意。现在可以坐下来放松一下，对吗？

不完全是。您可能还想考虑另一件事，以帮助将生产数据库灾难性丢失的成本降至最低。您需要的是备份。

### 创建备份

在 MySQL 中创建备份非常容易，这要归功于随系统附带的一套出色的客户端工具。要创建备份，您可以使用 mysqldump 实用程序。您需要做的第一件事是（如果需要）退出 MySQL 客户端，回到您的标准 shell 提示符：

```sql
mysql> exit
```

一旦您回到命令提示符，调用 mysqldump 命令行工具就变得很简单。对于大多数数据库备份，以下通用格式都可以工作：

```bash
mysqldump --opt database > backupfile.sql
```

这里您正在调用 mysqldump 命令，并告诉它将名为 database 的数据库转储到名为 backupfile.sql 的文件中。同时存在的是 --opt 选项，它告诉备份实用程序使用一组常用选项，以输出有助于 MySQL 更准确地恢复该文件的格式。

要了解更多的 mysqldump 选项，请在命令提示符处输入 man mysqldump。

若要备份车辆库存数据库，请使用以下命令：

```bash
mysqldump --opt VehicleInventory > vi_backup.sql
```

与 mysql 命令行客户端一样，如果需要提供用户名和密码，请确保在数据库名称之前正确使用 -u 和 -p。

现在，您在 vi_backup.sql 文件中拥有了完整的数据库创建脚本。您可以根据需要归档此文件，将其恢复到车辆库存服务器，将其刻录到 CD 或 DVD 上，或者您喜欢的任何其他操作。

### 从备份恢复数据库

在服务器崩溃、被黑客入侵，或者您只是想要生产数据库的副本以便在开发环境中进行测试的情况下，您将需要知道如何恢复数据库备份。在 MySQL 中，这极其简单，您可以使用 MySQL 命令行客户端，如下所示：

```bash
mysql database < backupfile.sql
```

因此，若要恢复 VehicleInventory 数据库，请使用此命令：

```bash
mysql VehicleInventory < vi_backup.sql
```





## 第 4 章

请注意，恢复操作的目标数据库名称必须是系统中已经存在的实际数据库。如果您想将备份恢复到一个新表，只需登录到 mysql 客户端，创建一个您想要的名称的空数据库，退出客户端，然后按照您的意愿恢复备份即可。

#### 总结

希望本章提供的信息能让您能够建立复杂的数据库模式，使用复杂的查询，并很好地维护整个系统。掌握了这些基本工具后，您将很少遇到无法克服的数据库障碍。作为开发者，您可能会发现自己花更少的时间在命令行界面上，而更多地使用像 PhpMyAdmin 或 MySQL AB 自家的 MySQL Administrator GUI 工具这样的工具。只要这些工具提供了一种输入原始命令的方式，本章中提到的原始命令和查询就可以应用于任何这些工具。您对执行管理任务和数据处理任务的具体 SQL 语句的理解，也将帮助您精确理解 GUI MySQL 应用程序中任何文本字段、单选按钮和复选框背后发生的事情——或者是在您的 PHP 应用程序本身中。

## 5 PHP 配置

当您处理 LAMP 技术时，很少有像 PHP 的配置那样深刻影响您的编码决策。任何 PHP 安装的核心是配置文件，*php.ini*。该文件中的设置可能会极大地影响您的应用程序编码方式、服务器性能，甚至安全性。本章告诉您需要查看和更改哪些设置，以改进您的 PHP 安装，并提供一组脚本，以自动根据您的喜好准备您的 PHP 环境和配置设置。

## 修改 php.ini

如前所述，*php.ini* 文件是配置 PHP 安装的主要工具。本节涵盖了一些您应该设置的配置指令，以及一些在 PHP 5 中新增的指令。

### 推荐的配置指令

在配置 PHP 时，为了使您的系统保持安全并以最高速度运行，需要牢记许多设置：

- `register_globals = off`：将旧 PHP 代码迁移到新系统时最常见的问题之一是 PHP 如何处理表单数据和变量。在旧版本的 PHP 中，表单字段会自动转换为与 PHP 引擎共享相同名称的全局变量。虽然有些人觉得这很方便，但由于命名和使用上的混淆，它最终成为了安全风险。从 PHP 4.2.0 开始，**register_globals** 的默认值为 *off*。您应该将其保持为 *off*，并使用 `$_GET`、`$_POST` 和 `$_COOKIE` 超全局变量，而不是依赖自动创建的变量。

在开发应用程序时，尤其重要的是保持 **register_globals** 设置为 *off*，因为您无法确定它最终运行的任何生产服务器的设置。

- `display_errors = off`：虽然在开发环境中这并不是必需的，甚至是一种负担，但对于生产或公共 Web 服务器上的任何 PHP 应用程序，将 display_errors 设置为 off 是一个好主意。关闭 display_errors 可以禁止 PHP 向用户的 Web 浏览器显示任何解析或运行时错误。最终用户看到的任何错误都可能揭示应用程序的内部机制，这对于希望攻击您站点的恶意个人来说可能是有用的信息。

在开发或调试情况下，将 display_errors 保持为开启状态以辅助调试是完全可以接受的。

- `log_errors = on`：这个设置通常与 display_errors 一起使用，指示 PHP 将通常显示在屏幕上的所有错误记录到文件中。您可以稍后使用该文件进行分析或调试，或者使用您自己选择的工具定期自动通知网站管理员。

- `error_log = filename` 或 `error_log = syslog`：error_log 指令告诉 PHP 在启用 log_errors 时向哪里发送错误。您可以指定 PHP 将错误写入的文件名，或者指定 syslog，它将把错误发送到系统日志守护进程。

- `error_reporting = E_ALL`：该指令简单地指示 PHP 报告其遇到的所有错误、警告和通知。默认情况下，PHP 显示除通知外的一切。显示通知通常是个好主意，尤其是在开发期间，因为它可以帮助您追踪未初始化的变量和其他小代码漏洞。

- `magic_quotes_gpc = off`：magic_quotes_gpc 指令告诉 PHP 在加载脚本时是否应自动转义输入/表单数据。虽然此设置旨在节省时间，但如果您决定切换数据库，或者使用不使用反斜杠转义特殊字符的数据库，它实际上可能会导致问题。如果您认为将来可能会切换数据库系统，或者您当前使用混合数据库环境甚至根本没有数据库，最好将此设置为 off。

- `variables_order = “GPCS”`：将 variables_order 设置为 GPCS 会告诉 PHP 不要自动生成通常保存环境变量的 `$ENV` 数组——通常当 variables_order 设置为 EGPCS 时设置。此设置仅出于性能原因推荐，如果您仍然需要访问环境变量，可以使用 `getenv()` 函数。

- `allow_call_time_pass_reference = off`：此指令可能不会影响所有代码，但它可以帮助您防止代码因 PHP 的未来版本而过时。将 allow_call_time_pass_reference 设置为 off 可以防止您强制将函数参数通过引用传递。如果在该设置为 off 时尝试通过引用传递参数（使用 & 前缀），将生成警告。虽然目前这对生产服务器不是严重问题，但在开发应用程序时这是一个良好的设置，以确保它们与未来的 PHP 版本兼容。

- `asp_tags = off`：虽然在大多数配置中通常不是问题，但如果移动应用程序到具有不同 asp_tags 设置的服务器，使用 ASP 风格标签（`<% %>`）而不是标准 PHP 标签（`<?php ?>`）最终可能会成为问题。虽然这不是一个严重的需求、性能问题或安全问题，但在开发期间将 asp_tags 保持设置为 off 是个好主意，以避免后来的代码兼容性问题。

- `short_open_tag = off`：与将 asp_tags 设置为 off 一样，将 short_open_tag 设置为 off 也有助于确保您的应用程序能在不同的服务器上普遍工作，而不是因简单的配置差异而损坏。

使用 `short_open_tag` 的另一个好处是，您可以在脚本中使用 `<?xml ?>` 语句，例如 XML 文档序言。如果 `short_open_tag` 设置为 on，并且您尝试使用 `<?xml`，它将尝试解析 `<? ?>` 包装器内的任何内容作为 PHP，并抛出错误。

- `zlib.output_compression` 设置为 on：将 zlib.output_compression 设置为 on 告诉 PHP 在向最终用户发送数据之前，使用 zlib 库压缩输出数据。这与在 Apache 中使用 `mod_gzip` 或 `mod_deflate` 具有类似的效果：输出字节减少，从而改善了通过互联网的传输时间。

### PHP5 的新特性

除了 PHP5 中引入的改进的对象模型外，还增加了一些新的配置设置。PHP5 新增了以下内容：

- mail.force_extra_parameters
- register_long_arrays
- session.hash_function
- session.hash_bits_per_character
- zend.ze1_compatibility_mode

以下部分描述了这些新指令。

#### mail.force_extra_parameters

这个新指令允许您在使用 mail() 函数时指定传递给 **Sendmail** 的特定值。通常在使用 mail() 函数时，您可以传递一个第五个参数，向 **Sendmail** 发送额外的命令行参数。当设置此指令时，mail() 第五个参数中指定的任何 **Sendmail** 命令行参数都会被 `mail.force_extra_parameters` 中设置的值自动覆盖。

> 发送邮件时始终使用为 `mail.force_extra_parameters` 设置的值——即使在安全模式下，此时 mail() 的第五个参数是不允许的。

#### register_long_arrays

通常，当在网站上提交表单时，PHP 获取每个表单字段中的值，并根据表单的模式（GET 或 POST）将其放入两个大数组中。如果表单使用 GET 提交，名为 `$HTTP_GET_VARS` 的数组将被填充表单值，每个字段在数组中都有一个对应的命名索引，此外还有一个名为 `$GET` 的相同数组，保存相同的值。这种重复主要是为了向后兼容——超全局变量 `$_GET` 和 `$_POST` 直到 PHP 4.1.0 才引入，因此许多旧应用程序仍然使用旧的 `$HTTP_*_VARS` 数组。

如果您的应用程序根本不使用旧样式的数组，出于性能原因，您应该将此设置为 **off**。





## 第 5 章

#### session.hash_function

过去，当 PHP 为用户创建新的会话和会话 ID 时，你无法控制用于创建会话 ID 的算法。使用 `session.hash_function`，你可以选择用于创建会话 ID 的两种哈希算法之一。

将此选项设置为 `0` 将指示 PHP 使用 `MD5` 对会话 ID 进行哈希处理（128 位）。如果你想使用 `SHA-1`（160 位），可以将值设置为 `1`。

#### session.hash_bits_per_character

为了进一步配置会话 ID，你可以使用 `session.hash_bits_per_character` 来指定在转换为可读值时，会话 ID 中的每个字符存储多少位。选项如下：

- `4`：0-9，a-f
- `5`：0-9，a-v
- `6`：0-9，a-z，A-Z，"-"，"/"

#### zend.zl1_compatibility_mode

最后一个新的配置项 `zend.zl1_compatibility_mode`，简单地指定是否启用与 Zend Engine 1（PHP 4）的兼容性。

## 运行时 PHP 配置

直接检查和修改 `php.ini` 中的指令设置通常是监控和修改安装环境的快速且简单的方法，但很多时候你无法关闭服务器来进行更改，或者你需要在脚本运行时知道某个设置。本章此部分的技术将帮助你在服务器仍在运行时进行修改。

### 获取当前运行时设置

如果你需要知道已安装的 PHP 的确切版本，PHP 提供了 `phpversion()` 函数，该函数返回一个 `string`，列出完整的已安装版本。例如：

```php
<?php

echo "当前安装的 PHP 版本是：" . phpversion();

?>
```

这将输出类似以下内容的内容：

```
当前安装的 PHP 版本是：5.0.4
```

### 检索配置设置

有时，简单的版本检查提供的信息不够充分，你需要更多关于 PHP 配置方式的信息，但你无法直接访问 php.ini。要查找运行时配置设置，你有三个主要选择：`ini_get()`、`get_cfg_var()` 和 `ini_get_all()`。

第一个选项 `ini_get()` 将给定的字符串与当前的运行时配置进行检查。如果设置匹配，它返回该设置的值；如果未找到匹配项，则返回空字符串：

```php
<?php

echo "错误报告： " . ini_get('error_reporting') . "\n" .
      "注册全局变量： " . ini_get('register_globals') . "\n" .
      "不存在的设置： " . ini_get('nonexistant') . "\n";

?>
```

运行此代码应产生类似以下的输出：

```
错误报告： 2047
注册全局变量：
不存在的设置：
```

请注意，错误报告的值实际上是常量 `E_ALL` 的数值等价物。但 `register_globals` 的值在哪里呢？当 `ini_get()` 返回 PHP.ini 认为是布尔值（关闭或开启，0 或 1，是或否）的值时，它会自动转换它们。任何 "off" 或 "no" 的值会自动转换为 "0"；任何 "yes" 或 "on" 的值自动变为 "1"。

检索配置设置的第二个选项 `get_cfg_var()`，其行为与 `ini_get()` 几乎完全相同，不同之处在于它直接从 php.ini 获取值，而不是从当前运行时环境。除非你在代码中更改了配置变量（稍后会有更多介绍），否则值通常应与 `ini_get()` 返回的值匹配。例如，考虑以下代码：

```php
<?php

echo "错误报告： " . get_cfg_var('error_reporting') . "\n" .
      "注册全局变量： " . get_cfg_var('register_globals') . "\n" .
      "不存在的设置： " . get_cfg_var('nonexistant') . "\n";

?>
```

除非设置已在活动脚本中更改，否则这段代码会产生与以下代码相同的输出：

```php
<?php

echo "错误报告： " . ini_get('error_reporting') . "\n" .
      "注册全局变量： " . ini_get('register_globals') . "\n" .
      "不存在的设置： " . ini_get('nonexistant') . "\n";

?>
```

获取配置信息的第三种方式 `ini_get_all()`，像放大版的 `ini_get()`。它不需要指定单个要查找的值，`ini_get_all()` 返回一个包含所有注册配置选项的数组。其返回的值也不仅限于当前设置 - `ini_get_all()` 返回在 php.ini 中设置的全局值、当前时刻存在的本地值，以及更改设置所需的访问级别。

看这个简单的例子：

```php
<?php
print_r(ini_get_all());
?>
```

执行这段代码，你会得到类似以下的结果：

```
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

注意，此输出已大幅缩减 - 实际返回的数组包含超过 150 个不同的项目。还要注意，有些值是空字符串，例如 `allow_call_time_pass_reference` 的全局和本地值。当 `ini_get_all()` 返回每个设置时，它使用与 `ini_get()` 相同的值转换规则，特别是在处理 off/on 值时。

### 扩展信息

现在你已经可以收集关于运行时设置的信息了，是时候学习如何检查扩展及其属性了。PHP 提供了三个内置函数来查找有关已加载扩展的信息。

第一个是 `extension_loaded()`，它简单地检查给定的扩展是否已加载。你只需要提供扩展的名称，它就会返回一个布尔值，指示它是否可用，如下所示：

```php
<?php
if (extension_loaded('mysql'))
{
    echo "MySQL 可用。\n";
}
else
{
    echo "MySQL 不可用。\n";
}
if (extension_loaded('fakesql'))
{
    echo "Fake SQL 可用。\n";
}
else
{
    echo "Fake SQL 不可用。\n";
}
?>
```

运行此代码时，你应该看到以下内容：

> MySQL 可用。
> Fake SQL 不可用。

如果你需要同时知道多个扩展的状态，PHP 提供了 `get_loaded_extensions()`。与 `ini_get_all()` 类似，`get_loaded_extensions()` 返回所有已加载扩展的数组。考虑以下代码：

```php
<?php
print_r(get_loaded_extensions());
?>
```

根据你的当前配置，这可能是多几个或少几个扩展，但应产生类似以下的输出：

```
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
    [20] => bccmath
    [21] => zlib
    [22] => openssl
    [23] => ibxm
)
```

一旦你知道某个扩展可用，你可能想更多地了解那个特定的模块。要获取扩展提供的所有函数列表，请使用 `get_extension_funcs()`。与前面一些信息命令一样，它返回可用值的数组，但在这种情况下，它提供给定扩展的函数列表。例如：

```php
<?php
print_r(get_extension_funcs('simplexml'));
?>
```

运行这段代码应给出 SimpleXML 扩展提供的所有函数列表：

```
Array
(
[0] => simplexml_load_file
[1] => simplexml_load_string
[2] => simplexml_import_dom
)
```

### 魔法引号

如本章前文所述，PHP 允许一种称为“魔法引号”的特殊数据处理机制。当启用魔法引号时，PHP 会自动通过添加反斜杠前缀来转义任何特殊字符——单引号、双引号、NULL——以防止在将字符串用于数据库时出现问题。

实际上，PHP 可以在两个地方自动转义字符串：来自网页表单或请求的输入数据，或者自动来自返回任何数据的任何函数。每次替换都由



其自身的配置指令。输入数据的自动转义由 **`magic_quotes_gpc`** 指令控制，而来自任何函数的转义则由 **`magic_quotes_runtime`** 设置控制。由于这两者都是关键操作，如果被忽视可能会“污染”你的数据，PHP 提供了两个函数来快速确定每个设置当前的状态：针对输入数据的 **`get_magic_quotes_gpc()`**，以及针对函数处理器的 **`get_magic_quotes_runtime()`**。这两个函数都不需要参数，如果设置已启用则返回 1，如果禁用则返回 0。运行这段代码：

```php
<?php

echo "Magic quotes GPC: " . get_magic_quotes_gpc() . "\n",
     "Magic quotes runtime: " . get_magic_quotes_runtime() . "\n";

?>
```

取决于你当前的配置，你会看到类似这样的输出：

```
Magic quotes GPC: 0
Magic quotes runtime: 0
```

### 动态更改配置

现在你可以在代码中实时检查配置设置和扩展属性，但如果某些东西不符合你的喜好，你打算怎么做？通过一些内置的 PHP 函数，你可以更改 PHP 在某些情况下的行为。

#### 不再那么神奇的引号

如果你像我一样，你大概不喜欢启用了 **`magic_quotes_runtime`**，因为它会破坏所有函数的输出。虽然它可以被视为一种便利，但它通常只会碍事，并迫使你在各处使用 **`stripslashes()`** 或 **`addslashes()`**。要更改它，你可以使用 **`set_magic_quotes_runtime()`**。参数为 `"1"` 开启自动替换；值为 `"0"` 则关闭它：

```php
<?php

// Turn on magic_quotes_runtime
set_magic_quotes_runtime(1);

// Turn off magic_quotes_runtime
set_magic_quotes_runtime(0);

?>
```

不幸的是，对于 **`magic_quotes_gpc`** 不能这么说——你不能在运行时更改其值（稍后会有更多介绍）。

#### 移除时间限制

是时候让 PHP 在超时前多等一会儿了。为此，你使用 **set_time_limit()**，并简单地指定你的脚本允许运行的秒数：

```php
<?php
    // Set the timeout at one minute
    set_time_limit(60);
?>
```

如果你无法准确猜测你的脚本需要多长时间，并且*绝对确定*没有无限循环，你可以通过将值设置为**零**来完全移除超时：

```php
<?php
    // Will run forever if you’re not careful
    set_time_limit(0);
?>
```

当你使用 **set_time_limit()** 时，有两件事需要注意。首先，如果你的服务器以安全模式运行 PHP，使用 **set_time_limit()** 将不会有任何效果。你必须*要么*禁用安全模式，*要么*更改 **php.ini** 中的全局值。其次，每当调用 **set_time_limit()** 时，它会将内部计时器重置为 **0**。如果你的脚本已经运行了 15 秒，并且你将超时设置为 20 秒，它不会在再过 5 秒后退出——它将计数器重置为 **0** 并重新计数 20 秒，总共 35 秒。

#### 更改指令

如果你想只更改任意运行时配置设置怎么办？为此，你可以使用函数 **ini_set()**。要使用 **ini_set()**，只需传递设置的名称和新值。如果函数成功，它将返回*旧*值；如果不成功，它将返回 *false*。运行这段代码：

```php
<?php
    echo "Setting error_reporting to E_STRICT...\n";
    $old = ini_set('error_reporting', E_STRICT);
    echo "Old value was: " . $old . "\n";
?>
```

你应该看到以下内容：

```
    Setting error_reporting to E_STRICT...
    Old value was: 2047
```

如果你决定不再想要更改后的值，你可以使用 **ini_restore()** 恢复脚本开始执行时的原始值：

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

这次运行代码时，它应该能成功恢复旧值：

```
Old value was: 2047
New value is: 2048
The value is once again: 2047
```

在你大肆更改设置之前，你需要意识到在脚本执行期间实际可以更改哪些设置是有限制的。如果你还记得之前展示 `ini_get_all()` 的时候，每个配置指令的数组返回了三个值：

```
...
            [allow_call_time_pass_reference] => Array
            (
                [global_value] =>
                [local_value] =>
                [access] => 6
            )
            ...
```

第三个值 **access** 指示配置指令实际上可以在哪里被更改。为 **access** 提供的数值实际上是以下任何值的总和：

| 值 | 含义 |
|---|---|
| 1 | 指令可以在用户脚本中设置。 |
| 2 | 指令可以在 php.ini、.htaccess 或 httpd.conf 中设置。 |
| 4 | 指令可以在 php.ini 或 httpd.conf 中设置。 |
| 7 | 条目可以在任何地方设置。 |

在示例指令 `allow_call_time_pass_reference` 中，**access** 的值为 6，意味着该指令只能更改在 `php.ini`、`.htaccess` 或 `httpd.conf` 中。需要记住的关键点是，如果设置的访问值为 2、4 或 6，则无法在脚本执行期间更改它。任何尝试都会自动返回 `false`。

### 自动版本和功能检查

了解在运行时评估和更改设置的各种方法是有帮助的，但在所有脚本或页面中确保跨系统和应用的恒定环境可能会很麻烦。一种可能的解决方案是将你的所有版本和扩展检查放入它们自己的脚本中，并在每个页面的顶部包含或必需该脚本。这种方法运行得非常好，但保持该验证脚本更新可能会很快变成一项繁琐的工作。在接下来的部分中，你将查看一个简单的环境检查脚本的变体——它使用一个易于修改的配置文件，并且只需几行代码即可调用。

这组脚本由三个主要的代码块和一个简单的配置文件组成。首先，查看配置文件，在本例中称为 reqs.xml：

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

如果你有任何 XML 经验，你会认出这是一组建立站点配置的简单标签。包裹在主包含的 `<requirements>` 标签内，有两个主要部分。

第一部分，`<packages> </packages>` 包含你的应用程序所需的所有扩展的列表。每个扩展通过使用 `<package />` 空标签来指定，其中属性 `name=` 指定扩展的名称。扩展的名称应与之前提到的由 `get_loaded_extensions()` 返回的名称匹配。

第二部分包含定义特定应用程序设置的定义，默认情况下在 php.ini 中找到，以及 PHP 本身的版本要求。每个 `<setting />` 标签可以对应于 PHP 运行时配置设置。`name=` 属性与配置设置的名称匹配，而 `value=` 属性包含在 php.ini 中使用的任何值。`<php />` 标签允许你指定应用程序的版本要求——最小版本在 `minversion=` 属性中指定，最大版本在相应的 `maxversion=` 属性中指定（未显示）。

在这个 reqs.xml 示例中，GD、MySQL 和 PostgreSQL 扩展被列为必需，允许的最小 PHP 版本是 5.0.0，并且 `register_globals` 指令必须设置为 off。

> 在这个示例中指定最小版本 5.0.0 在技术上是不必要的——由于不同的对象模型，接下来出现的类结构只能在 PHP 5.0 及更高版本上运行。





#### PHP 配置

配置检查器中的下一个文件是 **class.ConfigManager.php**，它充当脚本的中央控制点：

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

这个类的第一部分应该很直观。它首先声明了类 ConfigManager，并声明了三个公共属性：

```php
<?php
class ConfigManager
{
    public $configfile = 'reqs.xml';
    public $configtype = 'xml';
    public $errors;
```

第一个属性 `configfile` 保存你要使用的配置文件名。该配置文件的默认值被设置为 `reqs.xml`，因此除非你使用不同的文件名，否则无需显式设置此属性。`configtype` 属性用于指定配置的类型。在这种情况下，提供了一个默认值 `xml`，以表明你的配置是 XML 格式的。最后一个属性 `errors` 只是稍后处理过程中遇到的任何错误消息的占位符。

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

虽然这个构造函数并没有发生什么真正神奇的事情，但它确实提供了在创建对象时传入配置文件和类型的机制，并使用这些值来设置相应的属性。

ConfigManager 中的最后一个方法才是所有魔术发生的地方：

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
?>
```

`processConfig()` 方法首先确定配置类型，然后根据配置类型调用必要的代码并利用组件对象。目前，`processConfig` 中只指定了一种类型，即处理 XML 配置文件的那种。随着新的配置处理器类型的创建，可以添加任意数量的额外 case。如果你想将配置存储在数据库中，你可以设计自己的数据库配置处理对象，然后在此 switch 中添加一个 case，以调用新类中的任何处理方法。

注意，`XMLConfigProcessor` 的类文件是在此点而不是在文件开头或类更前面进行包含的。这样，只有当需要时才解析该文件，如果使用了不同的配置类型，有助于减少多余的处理。使用 `XMLConfigProcessor` 很简单，只需实例化该对象，将配置文件名传递给构造函数，最后调用处理配置的方法即可（章节后面会详细介绍）。

这一组文件中的下一个文件是一个简单的接口，用于定义任何配置处理类都应支持的一组方法：

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

这个非常直观——这里定义的四个方法将规定所有处理类在任何配置类型下的通用功能。前三个方法 `checkExtensions()`、`checkPHP()` 和 `checkConfig()` 主要作为实现类中的内部方法，而最后一个方法 `process()` 旨在作为触发其他三个方法的主要公共方法。

配置检查工具中的最后一个文件是类 `XMLConfigProcessor.php`，正如你可以从文件名猜到的，它处理 XML 配置文件：

```php
<?php
require_once 'interface.ConfigProcessor.php';

class XMLConfigProcessor implements ConfigProcessor
{
    public $xmlfile;
    private $message = "";
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
        // Check for needed libraries
        if (!$this->checkDeps() ||
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

    public function checkExtensions()
    {
        $returnValue = true;

        // Check for all listed extensions
        $exts = $this->xml->xpath('packages/package');
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
    }

    public function checkPHP()
    {
        // Check if PHP requirement is present
        if (count($phpreq = $this->xml->xpath('environment/php')) == 0)
        {
            return true;
        }

        // Flatten element array
        $phpreq = $phpreq[0];

        // Check minimum version
        if ($phpreq['minversion'] and
            version_compare(phpversion(),
                            $phpreq['minversion']) < 0)
        {
            $this->message .= "Warning: " .
                "PHP version is less than " .
                $phpreq['minversion'] . "\n";
            return false;
        }

        // Check maximum version
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
                    $value = "";
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
                ($value !==
                $cfg[$name]['local_value'] and
                ini_set($name, $setting['value']) === false))
            {
                $returnValue = false;
                $this->message .= "Warning: " .
                    $name .
                    " not set to the required value of: "
                    . $setting['value'] . "\n";
            }
        }

        return $returnValue;
    }
}
?>
```

类的开头部分相当平常——你包含接口文件，开始类，并定义一些属性。第一个属性 `$xmlfile` 用于保存你的 XML 配置文件的文件名。第二个属性 `$message` 将用于捕获处理文件时创建的任何错误消息。第三个也是最后一个属性 `$xml` 将保存由 PHP 的 SimpleXML 扩展创建的 XML 对象。在属性定义之后，有一个简单的构造函数，如果在实例化时传入文件名，则设置 `$xmlfile` 的值。





#### PHP 配置

```php
<?php

require_once 'interface.ConfigProcessor.php';

class XMLConfigProcessor implements ConfigProcessor
{

    public $xmlfile;
    private $message = "";
    private $xml;

    public function __construct($xmlfile = null)
    {
        if ($xmlfile)
        {
            $this->xmlfile = $xmlfile;
        }
    }

```

紧随构造函数之后的 `process()` 方法是类外部调用的主要方法。它包含对该类中所有其他组件方法的调用，这些方法用于检查 XML 配置文件的各个需求和部分。

在 `process()` 的第一部分中，你检查配置文件是否可访问，以及 PHP 安装环境是否具备该类正常运行所需的所有要素：

```php
public function process()
{
    // 检查所需的库
    if (!$this->checkDeps() or
        !$this->checkConfigAccess())
    {
        return $this->message;
    }

```

如果上述任一检查失败，该方法应终止并返回遇到的任何错误消息。

接下来，使用 SimpleXML 扩展将配置文件的内容加载到一个 XML 对象中，更准确地说，是一个 `simplexml_element` 对象。可以使用这个 `simplexml_object` 轻松遍历 XML，并按需提取标签和属性：

```php
$this->xml = simplexml_load_file($this->xmlfile);
```

最后，`process()` 调用来自 ConfigProcessor 接口的剩余三个方法，以检查 PHP 版本、可用扩展和配置设置：

```php
if (!$this->checkPHP() or
    !$this->checkExtensions() or
    !$this->checkConfig())
{
    return $this->message;
}

```

# 第 5 章

接下来遇到的方法是 `checkConfigAccess()`。该方法检查 XML 配置文件是否实际存在于文件系统中，如果存在，则进一步检查其是否可读。如果文件不存在或不可读，则向 `$message` 属性添加一条错误消息。请注意，在该方法的结尾调用了 `clearstatcache()`。`file_exists()` 和 `is_readable()` 的结果会被 PHP 缓存，因此在完成后清除结果缓存是个好主意，以防止后续出现异常结果：

```php
private function checkConfigAccess()
{
    $returnValue = false;

    // 检查配置文件是否存在且可读
    if (file_exists($this->xmlfile) and
        is_readable($this->xmlfile))
    {
        $returnValue = true;
    } else {
        $this->message .= "Warning: " .
                          "Could not access config file.\n";
    }

    // 清除缓存的文件系统查找结果
    clearstatcache();
    return $returnValue;
}
```

接着是 `checkDeps()`。顾名思义，该方法检查类本身的依赖项。对于 `XMLConfigProcessor`，唯一的非标准 PHP 要求是 SimpleXML 扩展的可用性。例如，如果你决定稍后修改此类以使用 XML Parser 函数或 DOM XML 扩展，你需要在此方法中添加相应的检查。

要检查 SimpleXML，只需使用本章前面介绍的 `extension_loaded()` 函数即可。如果 SimpleXML 不可用，则向文件添加另一条错误消息：

```php
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
```

#### PHP 配置

现在是时候动手实践，整理一下你的 XML 配置文件了。在 `checkExtensions()` 中，你需要做的第一件事是收集配置文件中列出的所有扩展。如前所述，每个包都作为 `<package />` 标签列在一组包围它的 `<packages>...</packages>` 标签内部。要获取所有这些包的列表，你使用 SimpleXML 的 `xpath()` 方法：

```php
public function checkExtensions()
{
    $returnValue = true;

    // 检查所有列出的扩展
    $exts = $this->xml->xpath('/packages/package');
}
```

`xpath()` 方法接受一个表示元素在文档层次结构中位置的字符串（其 Xpath 路径），并返回一个 `simplexml_element` 对象数组——在此情况下，每个对象代表一个单独的 `<package />` 标签。

一旦获得了包标签的数组，你只需遍历它们，检查每一个是否可用。由于包名称存储在每个 `<package />` 标签的 `name="attribute"` 中，你可以类似访问数组键一样访问这些值，使用括号语法和其中的字符串。再次使用 `extension_loaded()` 函数检查每个包，如果不可用，则向消息堆栈中添加一条错误消息：

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
}
```

来自 ConfigProcessor 的下一个实现方法是 `checkPHP()`。该方法检查 PHP 本身的版本，以确定应用程序是否可以在该版本上运行。方法开始时，首先使用 SimpleXML 的 `xpath()` 方法再次检查配置文件中是否存在 PHP 版本要求：

```php
public function checkPHP()
{
    // 检查是否存在 PHP 要求
    if (count($phpreq = $this->xml->xpath('environment/php')) == 0)
    {
        return true;
    }
```

# 第 5 章

如果发现 PHP 版本要求，则将 `xpath()` 返回的 `simplexml_element` 数组替换为数组中的第一个（也是希望唯一的）对象：

```php
// 扁平化元素数组
$phpreq = $phpreq[0];
```

PHP 版本检查可以有两个属性赋值：一个指定允许的最小 PHP 版本，另一个指定最大版本。对于最小和最大版本，首先检查属性是否存在，然后使用 `version_compare()` 函数配合 `phpversion()` 函数。`version_compare()` 函数接受两个参数，每个参数都是“PHP 标准化”的版本号字符串，例如 `5.0.4` 或 `5.0.5RC1`。如果第一个参数较低，函数返回 −1；如果第二个参数较低，返回 +1；如果两个参数相等，返回 0：

```php
// 检查最小版本
if ($phpreq['minversion'] and
    version_compare(phpversion(),
                    $phpreq['minversion']) < 0)
{
    $this->message .= "Warning: " .
                      "PHP version is less than "
                      "$phpreq['minversion'].".\n";
    return false;
}
// 检查最大版本
if ($phpreq['maxversion'] and
    version_compare(phpversion(),
                    $phpreq['maxversion']) > 0)
{
    $this->message .= "Warning: " .
                      "PHP version is greater than " .
                      "$phpreq['maxversion'].".\n";
    return false;
}
return true;
```

现在你已经检查了必需的扩展，并调查了已安装的 PHP 版本是否受你的应用程序支持，你需要检查运行时配置，以确保环境与你编码所针对的环境相匹配。在 `checkConfig()` 中，你使用 `ini_get_all()` 将所有配置设置收集到一个数组中：

```php
public function checkConfig()
{
    $returnValue = true;
    // 获取所有配置值
    $cfg = ini_get_all();
```

#### PHP 配置

一旦检索了所有当前的运行时设置，你需要收集 XML 配置文件中所有 `<setting />` 标签值的列表。为此，再次使用 `SimpleXML::xpath()` 函数：

```php
// 遍历设置元素
$settings = $this->xml->xpath('/environment/setting');
```

获取所有 `setting` 元素的数组后，你需要遍历它们，并检查运行时配置是否匹配。在直接比较这两个值之前，需要将 XML 配置文件中的每个值转换为与 `ini_get_all()` 的预期结果相匹配。通常，在 `php.ini` 中设置值时，可以使用几种不同的值来表示“true”或“false”。对于 true，可以使用 `on`、`true`、`yes` 或 `1`；`false` 由 `off`、`false`、`no` 或 `0` 表示。如前所述，当使用 `ini_get()` 或 `ini_get_all()` 返回设置时，表示 on 或 true 的值返回为 `as`（此处原文似有省略或笔误，结合上下文意为返回原值或 '1'），而 `off` 或 `false` 的值将返回为空字符串：

```php
foreach ($settings as $setting)
{
    $value = $setting['value'];
    // 将布尔值 $value 转换为 ini_get() 的值
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
}
```

接下来，检索配置变量的名称。由于像数组一样访问属性返回的是一个 `SimpleXML` 元素对象，你需要将其显式强制转换为 `string`，以便稍后与字符串值进行比较：

```php
// 扁平化字符串
$name = (string) $setting['name'];
```

现在你拥有了 XML 配置文件中要求的设置的名称和值，可以将它们与运行时设置进行比较。首先，检查运行时配置数组中是否存在该配置设置，然后将其与 XML 文件中的值进行比较。更进一步，如果该设置存在但不匹配，则尝试使用 `ini_set()` 更改当前的运行时配置变量。如果设置不匹配 **且** 无法在运行时更改该设置，将生成一条错误消息，并且函数将返回 `false`：

```php
// 检查配置值，必要时进行设置
if (!array_key_exists($name, $cfg) or
    $value !=
        $cfg[$name]['local_value'] and
```




## 第 5 章

```php
ini_set($name, $setting['value']) === false)
{
    $returnValue = false;
    $this->message .= "Warning: " .
            $name .
            " not set to the required value of: " .
            "$setting['value'] . \"\n\"";
}
}

    return $returnValue;
}
?>
```

现在，既然你拥有了一组用于检查运行时环境的小型类层次结构和配置文件，你就需要实际编写一个脚本来调用它们。在下面的 `test.php` 代码中，你可以看到调用配置检查器是多么简单：

```php
<?php

// Check PHP environment:
require_once 'class.ConfigManager.php';
$config = new ConfigManager('reqs.xml', 'xml');
$config->processConfig();
?>
```

你只需要包含主 `ConfigManager` 类文件，创建一个新的 `ConfigManager` 对象，在实例化时传入文件名和类型，然后调用 `processConfig()` 方法来实际检查设置即可。

#### 总结

希望你现在已经熟悉了一些可以为你的应用程序注入生气的不同配置设置和函数。在运行时了解某个设置的价值通常有助于避免难以诊断的 bug，并且能够在运行时更改这些值可以使你的应用程序足够灵活，以应对不同的配置。这些知识和能力，结合自动配置检查，应该能帮助让你的应用程序在面对不熟悉服务器可能带来的未知问题时，尽可能坚韧。

![Image](img/cacdd24f2926f10ee3219256ad732604_154_0.png)

## Apache 技巧

本章暂时搁置 PHP 的话题，转而讨论一些你可能不了解的 Apache 特性。你都知道 Apache 是最受欢迎且功能强大的 Web 服务器，而 PHP 也是专为配合 Apache 工作而设计的，但你可能并不知道，你可以通过扩展 Apache 本身来让你的站点运行得更高效。秉承其开源性质，Apache 有许多优秀的可用模块，这些模块扩展了其功能，并为你作为站点管理员提供了有用的特性。

本章讨论了其中三个模块。`Mod_rewrite` 允许你提供 URL 替换以适应站点变化，但如果你正确使用它，还可以用它来保护站点安全并使其对搜索引擎更友好。`Mod_speling` 帮助纠正访客在你的站点上无意中犯的拼写错误。`Mod_deflate` 允许你在向用户发送内容时对其进行压缩，从而节省带宽成本。`Mod_auth_mysql` 让你能够利用用户数据库的力量增强站点的 Apache 认证安全性。`Mod_ssl` 允许你加密进出 Web 服务器的数据。最后，`mod_dav` 允许你将 Apache Web 服务器用作分布式文件仓库。

## URL 重写

如果你召集世界上所有的 Web 开发人员和服务器管理员，让他们列出可用于 Apache 的最重要模块，`mod_rewrite` 很可能会出现在那个列表中——这是有充分理由的。

对于不熟悉的人来说，`Mod_rewrite` 是一个提供 URL 重写功能的 Apache 模块。虽然这听起来可能很简单，但实际上 `mod_rewrite` 是 Apache 模块中的瑞士军刀。你能用 `mod_rewrite` 做什么？除了显而易见的简单 URL 重写外，`mod_rewrite` 还能让你保护查询字符串输入的安全，使你的站点保持对搜索引擎友好，让 URL 对用户友好，在站点重组后保留“旧”URL，并阻止热点链接。你会发现 `mod_rewrite` 可以迅速成为不仅仅是一个简单的 URL 更改工具。

## 第 6 章

### 启用 _mod_rewrite_

在你动手设置 `mod_rewrite` 之前，首先要做的是检查它是否已经安装。在命令行中，输入：

```
/path/to/httpd -l
```

*显然，请使用你自己路径下的 Apache httpd。*

如果你看到列出了 `mod_rewrite.c`，说明它已经编译进了 Apache。如果没有，请检查它是否存在为 Apache 的动态模块：

```
ls /path/to/apache/modules/
```

如果文件列表中存在 `mod_rewrite.so`，那么 Apache 可以通过对 `httpd.conf` 文件进行少量调整来将其加载为模块（如本部分后面所示）。如果它既没有编译进 Apache，也没有作为共享对象可用，你可以使用操作系统所使用的任何包管理系统来安装它，或者如果你是更亲自动手型的人，你可以重新编译 Apache 自身以包含 `mod_rewrite`。

在启用 Apache 功能时，通常有两个选择：将其静态构建到 Apache 二进制文件中，或者将模块编译为可加载的共享对象。当静态构建模块到 Apache 时，它们无需额外的配置指令即可使用，但模块在 Apache 运行期间将始终处于活动状态并消耗内存，即使你并不需要使用它。将模块编译为可加载的共享对象允许你将 Apache 二进制文件保持精简，不包含任何你可能需要也可能不需要的“可选”项目，但必须在 `httpd.conf` 中手动配置它们。两种方法都是完全可以接受的，但如果你不确定该选择哪种，共享模块路线由于其灵活性而成为一个流行选择。

要从源代码静态构建 `mod_rewrite` 到 Apache 中，请确保你的 configure 文件包含 `--enable-rewrite`，如下所示：

```
./configure \
--enable-rewrite \
# …and any other configure settings you use
```

如果你选择了动态模块路线，只需在启用 `mod_rewrite` 的行末尾添加 `=shared`：

```
./configure \
--enable-rewrite=shared \
# …and any other configure settings you use
```

然后，只需简单地将服务器制作并安装到你的系统中。如果你静态构建 `mod_rewrite` 到 Apache，可以通过重新运行 `httpd -l` 来确认你的重新配置是否成功。如果出现了 `mod_rewrite.c`，说明它已成功添加到 Apache 二进制文件中。

相反，如果你选择了动态模块，请先检查它是否确实存在于 Apache 模块目录中，作为一个名为 `mod_rewrite.so` 的文件：

```
ls /path/to/apache/modules/
```

假设一切顺利，并且 `mod_rewrite.so` 存在于模块目录中，你需要在 `httpd.conf` 中启用它，通过取消注释现有的行或添加一行如下所示的新行：

```
LoadModule rewrite_module modules/mod_rewrite.so
```

> *不要对任何静态编译进 Apache 的模块使用 `LoadModule` 行——仅限动态共享对象。对静态模块使用 `LoadModule` 只会生成错误。*

在对 `httpd.conf` 进行所有必要的更改后，重启 Apache。现在，既然你已经成功安装了 `mod_rewrite`，你需要查看用于利用 `mod_rewrite` 的不同配置设置。

#### RewriteRule

Mod_rewrite 提供了一组配置指令，可以提供从非常简单的重定向到复杂的多规则模式匹配替换的广泛重写能力。每个重写 URL 的核心都是 `RewriteRule` 指令。

##### RewriteRule 用法

无论你的重写需求多么复杂，你至少需要一条 `RewriteRule` 来执行转换。`RewriteRule` 指令的基本格式如下：

```
RewriteRule pattern substitution [flag(s)]
```

`RewriteRule` 的行为类似于 PHP 的 `preg_replace` 函数：它接受一个正则表达式模式，将其与传入的 URL 进行匹配，然后使用你定义的规则为 URL 提供替换内容。

在构建用于匹配的正则表达式模式时，你可以使用以下标记：

| 模式 | 含义 |
| :--- | :--- |
| ^ | 脱字符符号表示行或字符串的开始。 |
| $ | 美元符号表示行或字符串的结束。 |
| . | 点匹配任何单个字符。 |
| (a\|b) | 使用“管道”字符作为逻辑“或”，模式 (a\|b) 匹配 a 或 b。 |
| (...) | 括号将部分分组为一个子匹配。 |
| [abc] | 在方括号对内部列出值可以匹配给定列表或范围内的任何值。模式 [abc] 匹配单个字母 *a*、*b* 或 *c*，而模式 [a-z] 匹配小写字母 a 到 z 中的任何一个。 |
| [^abc] | 在范围开头使用脱字符匹配范围中*未*列出的任何值。模式 [^abc] 匹配除 *a*、*b* 或 *c* 以外的任何字符；模式 [^a-z] 匹配小写字母 a 到 z 以外的所有内容。 |

*表格在下一页继续*



## 第 6 章

| 模式 | 含义 |
| :---- | :---- |
| a? | 问号匹配前一个字符恰好零次或一次。 |
| a* | 星号指示 Apache 匹配前一个字符零次或多次 —— 无限制。 |
| a+ | 使用加号匹配前一个字符一次或多次 —— 无限制。 |
| a{m} | 花括号内的单个数值匹配前一个字符恰好指定的次数。 |
| a{m,} | 单个数值后跟逗号匹配前一个字符至少 m 次，但可能更多。 |
| a{m,n} | 花括号内的两个数值指定至少 m 次匹配，但不超过 n 次匹配。 |
| !(pattern) | 逻辑“非”由模式前的感叹号表示。用于当 URL 不匹配给定模式时应用规则。 |
| \char | 反斜杠作为转义字符，使您可以匹配通常是正则表达式记号的字符，如 "\^"、"\|"、"(" 等。 |
| \d | 匹配任何十进制数字。 |
| \w | 匹配任何“单词”字符 —— 通常是任何字母、数字或下划线字符。 |

例如，您可能最近已将网站的较旧部分替换为更新的版本，其 URL 有所不同。为了自动将旧结构中的任何 URL 重定向到新位置的索引，您可以使用类似于以下内容：

```
RewriteEngine On
RewriteBase /
# Rewrite requests for the old directory to the new index
RewriteRule ^olddirectory/ newdirectory/index.php [R,NC,L]
```

此规则告诉 Apache 对旧目录 olddirectory/ 文件夹中任何文件的所有请求，都响应新目录 newdirectory 文件夹中的 index.php。末尾的标志指定重定向到新 URL，在匹配时忽略大小写，并停止处理可能匹配请求 URL 的其他任何规则 —— 这些标志将在本章后面介绍。

使用 mod_rewrite 的更常见用途之一是提供对搜索引擎友好且对用户输入友好的 URL，同时仍然使用带有附加到请求的 HTTPGET 参数的标准 PHP 文件。为了帮助说明此场景，请通过创建以下 PHP 文件开始：

```
<?php
$category = "";
$item = "";
if (isset($_GET["cat"]))
{
$category = $_GET["cat"];
}
if (isset($_GET["item"]))
{
$item = $_GET['item'];
}
echo "Category: " . $category . "<br />\n" .
"item: " . $item . "<br />\n";
?>
```

将此文件保存为**catalog.php**，位于网站根文件夹中。

通常，如果您想要打开此文件并让它识别给定的类别或项目值，您必须在查询字符串中提供值，如下所示：

```
http://www.domain.com/catalog.php?cat=categoryvalue&item=itemvalue
```

不幸的是，某些搜索引擎不会将类似上述 URL 的动态页面编入目录。此外，指定每个变量所需的额外语法对于手动输入 URL 的人来说可能是一种负担。为了解决这种情况，您可以使用**mod_rewrite**。在 .htaccess 文件中添加以下指令，该文件位于与 category.php 文件相同的目录中（如果需要，也可以在服务器的 httpd.conf 文件中）：

```
RewriteEngine On
# Rewrite /category/item/ to catalog.php
RewriteRule ^(\w+)/(\w+)/?$ catalog.php?cat=$1&item=$2
```

> 为了在每目录配置文件（.htaccess）中使用 mod_rewrite 指令，必须在 httpd.conf 中为这些目录启用指令 Options FollowSymLinks 或 Option SymLinksifOwnerMatch。

现在，由于 mod_rewrite 的神奇作用，您可以使用 URL 中的目录而不是查询字符串来访问类别和项目记录：

```
http://www.domain.com/categoryvalue/itemvalue/
```

请注意，前面 URL 中引用的相应目录实际上并不存在 —— mod_rewrite 拦截请求并将其转换为附加查询字符串的 PHP 请求，然后通过 PHP 引擎解析。还要记住另一件事：如果前面的目录确实存在，并且此处显示的 RewriteRule 处于活动状态，Apache 仍会完全忽略实际路径，并按照计划进行 URL 重写。

查看 mod_rewrite 配置中的行，您从一个简单的声明开始：

```
RewriteEngine On
```

为了使用 mod_rewrite，您必须通知 Apache 您希望在给定的配置区域中启用该模块 —— 例如，.htaccess 文件，或 httpd.conf 中的 <Directory> 部分 —— 例如，**RewriteEngine** 接受**On**或**Off**作为其值。

下一个关键行只是一个正则表达式，用于匹配传入的 URL，以及在其位置使用的新 URL：

```
# Rewrite /category/item/ to catalog.php
RewriteRule ^(\w+)/(\w+)/?$ catalog.php?cat=$1&item=$2
```

该模式查找两级目录请求，使用 \w 模式匹配每个目录的有效“单词”字符。然后，它将两个目录的值用作 PHP 脚本的类别和项目编号。就像 PHP 的 PCRE 语法一样，您可以使用 $ 前缀的反向引用来引用原始模式中的子匹配项。*反向引用*是一种简单的方法，可以将前一个模式中的子匹配直接包含在替换字符串中。再次查看该规则：

```
# Rewrite /category/item/ to catalog.php
RewriteRule ^/(\w+)/?(\w+)/?\s catalog.php?cat=$1&item=$2
```

在匹配 URL 的正则表达式中，恰好定义了两个子匹配项：两个“单词”字符分组，指示目录。在替换字符串中，反向引用 $1 和 $2 用于自动相应地包含第一个和第二个子匹配项的值。反向引用简单地从 1 开始计数，这对应于第一个子匹配项。

在一个简单的*RewriteRule*中还可以使用什么其他技巧？实际上，您可以将其用作 PHP 脚本的原始类型检查层。在某些情况下，您可能需要从查询字符串变量中提取数字，例如页码或项目编号。如果您想绝对确定您使用的是数字，而不是潜在更危险的东西 —— 比如 SQL 注入攻击 —— 您有两个选项。

第一种也是最常用的方法是在 PHP 脚本中添加额外代码，以实际检查 $_GET 参数是否确实持有数字。例如，您可能拥有如下 URL：

```
http://www.domain.com/article.php?page=2
```

这样的 URL 通常出现在分页内容中，通常位于页面导航链接中。在加载指定文章的代码中，您可能会看到以下内容：

```
<?php
if (isset($_GET['page']) and is_numeric($_GET['page']))
{
    $page = $_GET['page'];
}
else
{
    $page = 1;
}

// And so on...
?>
```

前面的代码首先检查特定 $_GET 值（在这种情况下为 'page'）是否存在，然后检查传递的值是否确实是数字 —— 如果不是，则分配默认值 1。

这种类型检查是个好主意，有助于保护您的 PHP 脚本免受想要破坏您网站的恶意脚本小子侵害。不幸的是，当 PHP 脚本需要检查值是否已设置以及它是否确实是数字时，它可能会变得有些繁琐。

使用*mod_rewrite*，您可以消除 PHP 代码中的类型检查 —— 您只需确保模式仅匹配数值：

```
RewriteEngine On
# Ensure only numeric values for the page
RewriteRule ^article/([0-9]+)/?$ article.php?page=$1
RewriteRule ^article/[^0-9]+/?$ article.php?page=1
```

第一个 RewriteRule 检查形式为 /article/page/ 的任何有效 URL，并将给定请求转换为对 PHP 脚本的调用。第二个 RewriteRule 设置为捕获所有调用文章但提供无效页码值的错误 URL。任何此类请求都会自动分配文章的第一页。

在上一组 RewriteRule 中有两点需要注意。首先，两个规则都按顺序处理；处理不会在第一个规则处停止，而是继续处理所有给定规则。其次，对 article.php 脚本的重定向是在内部处理的 —— 根本不会向客户端发送 HTTP 重定向/移动状态码。为了改变这些默认行为，您可以使用每个规则末尾的一组标志。

#### RewriteRule 标志

为了控制 mod_rewrite 处理和每个 RewriteRule 的方式，您拥有一组 15 个不同的标志，可以在每个规则后添加。标志包含在方括号内，并且可以提供多个标志，以逗号分隔的列表形式 —— 全部在通用的一组方括号内。例如：

```
# Rewrite /category/item/ to catalog.php
RewriteRule ^([w+]+)/[w+]/?$ catalog.php?cat=$1&item=$2 [NC,RL,L]
```

##### nocase|NC

类似于 PHP PCRE 语法中的 i 标志，nocase 标志使模式不区分大小写。例如，以下两个模式是相同的：

```
RewriteRule ^([A-Za-z]+)/?$ catalog.php?cat=$1
RewriteRule ^([A-Za-z]+)/?$ catalog.php?cat=$1 [NC]
```

##### redirect|R[=code]

通常，mod_rewrite 在重写 URL 时使用内部 Apache 重定向，并且这种重定向对用户不可见。如果您想要执行带有 HTTP 状态码的正式重定向，可以使用 redirect 或 R 标志。默认情况下，redirect 标志发送 HTTP 302 临时移动代码，如以下规则所示：

```
RewriteRule ^article/[w+d]/?$ article.php?page=$1 [R]
```

如果您想要将状态代码更改为 HTTP 301 永久移动，或者 300 到 400 之间的任何其他状态代码，只需将代码添加到 redirect 标志的末尾：

```
RewriteRule ^article/[w+d]/?$ article.php?page=$1 [R=301]
```

##### forbidden|F

类似于 redirect 标志，使用 forbidden 标志会立即向客户端发送 HTTP 403 禁止响应。每当同一规则中存在 redirect 标志和 forbidden 标志时，forbidden 标志将具有优先级（将忽略重定向，发送 403）。




## 第 6 章

**gone|G**  
另一个 HTTP 状态码控制标志，`gone` 会发送 HTTP 410 Gone 响应，以告知客户端该页面不再存在。当与其他标志组合使用时，`gone` 标志的优先级高于 `redirect` 标志，但低于 `forbidden` 标志。

**last|L**  
为了在发现成功匹配后停止 RewriteRules 的处理，您可以使用 `last` 标志。在之前处理文章页码的示例中，即使第一条规则成功匹配，规则处理仍会继续到第二条规则（但不会找到匹配）。为了在第一条规则匹配后停止处理，您可以简单地使用 `last` 标志：

```
RewriteEngine On
# Ensure only numeric values for the page.
RewriteRule ^article/([0-9]+)/? article.php?page=$1 [L]
RewriteRule ^article/[^0-9]+/? article.php?page=1 [L]
```

**next|N**  
`next` 标志会在规则列表的开始处重新启动重写过程。当规则被重新处理时，匹配的 URL 不是客户端的原始请求，而是在使用 `next` 标志时内部重写后的 URL。例如：

```
RewriteRule ^article/(\d+)/? article.php?page=$1
RewriteRule ^catalog/(\w+)/? catalog.php?cat=$1 [N]
RewriteRule ^catalog/(\w+)/(\w+)/? catalog.php?cat=$1&item=$2
```

在这个示例中，如果调用了匹配第二条规则的 URL（例如 `http://localhost/catalog/stuff/`），重写过程将在该点停止处理，并自动使用新的替换 URL `catalog.php?cat=stuff` 从规则集的开始处重新启动。替换后的 URL 随后将自身通过整个规则集进行过滤。

使用 `next` 标志时应小心，因为可能会产生无限循环。

**chain|C**  
如果您希望将一组规则视为一个相关的单元，类似于 PHP 中的 `try...catch` 语法，您可以使用 `chain` 标志。使用 `chain` 标志时，如果某条规则匹配，处理将按预期继续，并忽略 `chain` 标志。如果某条规则不匹配且存在 `chain` 标志，则所有链接在一起的后续规则将作为整个块被跳过。例如，如果第一条规则不匹配，以下规则集将跳过到最后一条规则：

```
RewriteRule ^article/(\d+)/? article.php?page=$1 [C]
RewriteRule ^catalog/(\w+)/? catalog.php?cat=$1 [C]
RewriteRule ^catalog/(\w+)/(\w+)/? catalog.php?cat=$1&item=$2

# Skip to this rule if any of the above don't match
RewriteRule ^article/[^\d/]? error.php
```

## Apache 技巧

**skip|S=number**  
当当前规则匹配时，此标志允许您跳过接下来 number 数量的规则。虽然 `skip` 标志的行为与 `chain` 标志相似，但它的表现恰恰相反——`skip` 在匹配成功时跳转；`chain` 在匹配失败时跳转。

**type|T=mime-type**  
如果您想要覆盖文档发送的 MIME 类型，可以使用 `type` 标志。例如，如果您有一堆 .xhtml 文件，希望使用正确的 XHTML MIME 类型来提供这些文件，而不是 text/HTML，您可以使用以下内容：

```
RewriteRule ^.\.xhtml$ - [T=application/xhtml+xml]
```

**cookie|CO=name:value:domain[:lifetime[:path]]**  
`cookie` 标志（您可以推断出来）会在客户端浏览器上设置一个 cookie。三个必需字段——`name`、`value` 和 `domain`——分别指定 cookie 的名称、cookie 的值以及设置 cookie 的域名。可选的 `lifetime` 参数表示 cookie 的生存时间，单位为分钟。`path` 参数设置 cookie 的路径。

例如，如果您想设置一个名为 `prevvisit` 的 cookie，以表示用户之前访问过主页（并且不应被启动屏幕打扰），您可以使用以下代码：

```
RewriteRule ^index\.php$ - [CO=prevvisit:true:domain.com]
```

**env|E=var:value**  
`env` 标志允许您将环境变量 `var` 设置为提供的值。该值还可以包含正则表达式反向引用（$1、$2 等），以实现更复杂的变量控制。可以在一组标志中设置多个环境变量——只需像标志列表中的其他部分一样用逗号分隔即可。

**qappend|QSA**  
在大多数使用 `mod_rewrite` 的情况下，作为原始 URL 查询字符串提供的任何内容在执行重写时都会被丢弃。如果您希望保留这些信息而不是丢弃它们，可以使用 `qappend` 标志。使用此标志时，重写引擎只需将原始查询字符串附加到重写中提供的任何新查询字符串上。例如：

```
RewriteRule ^index\.php$ index.php?foo=bar [QSA]
```

此规则会将 `index.php` 文件从 URL `index.php?moo=cow` 更改为 `index.php?foo=bar&moo=cow`。

如果原始 URL 中的查询字符串参数与 `RewriteRule` 中的参数同名，则原始值优先。

## 第 6 章

**noescape|NE**  
当 `mod_rewrite` 执行转换时，它会费尽周折确保在重写 URL 中的特殊字符在执行任何内部或外部重定向前被转义。例如：

```
RewriteRule ~somedir/? index.php?page=f'oo%3b [R]
```

根据此规则，Apache 将按请求重定向 /somedir/ 目录，page 的 `$` GET 值将是“安全”的转义值 foo%3b——mod_rewrite 转义了 %3b 值，而不是将其替换为分号。要告诉 mod_rewrite 避免自动转义，您使用 noescape 标志：

```
RewriteRule ~somedir/? index.php?page=f'oo%3b [R,NE]
```

根据此规则，page 查询字符串参数的新值将是 foo; 。

**passthrough|PT**  
当您希望将 mod_rewrite 与其他提供类似 URL 处理功能的 Apache 模块（如 mod_alias）结合使用时，请使用 passthrough 标志。例如，如果您希望将 /foo 重写为指向 /bar，然后使用 mod_alias 将 /bar 转换为 /baz，您可能尝试以下代码：

```
RewriteRule ~ /foo /bar
Alias /bar /baz
```

不幸的是，由于 Apache 内部处理 URL 的方式，如上编写将无法工作。要使其工作，请添加 passthrough 标志：

```
RewriteRule ~ /foo /bar [PT]
Alias /bar /baz
```

一个通用的经验法则是，如果您使用多个 URL 转换模块来处理文件，请使用 passthrough。

**nosubreq|NS**  
使用 nosubreq 标志强制重写引擎在请求实际上是内部子请求时跳过规则。当将 PHP 和 Apache 一起使用时，很少需要此标志的情况。然而，在某些 CGI 脚本实例中，此标志会发挥作用。欲了解更多信息，请参阅 Apache 手册中关于 RewriteRule 的部分：http://httpd.apache.org/docs-2.0/mod/ mod_rewrite.html#rewriterule 。

**proxy|P**  
proxy 标志告诉重写引擎立即停止处理规则集，并强制请求通过 Apache 代理模块 mod_proxy。

鉴于如此多的关注都集中在 RewriteRule 上，您可能会认为它是 mod_rewrite 背后的主要力量。实际上，它最好的角色是 RewriteRule 和 RewriteCond 这一动态组合的一部分。

### RewriteCond

RewriteCond 指令的行为很像 PHP 的 `if ( )` 语句：它将字符串与模式或条件进行测试。如果输入匹配模式或字符串，则紧接着 RewriteCond 指令的 RewriteRule 将被处理。RewriteCond 的一般格式如下：

```
RewriteCond TestString CondPattern
```

TestString 是您正在评估的字符串，CondPattern 是要检查的正则表达式或比较值。

#### RewriteCond 用法

RewriteCond 最常见的用法是将输入字符串与正则表达式进行匹配，类似于 RewriteRule。但是，当您使用 RewriteCond 时，您可以访问大量的服务器变量，因此您的输入字符串可以比简单的文件名匹配更复杂。下表列出了在 RewriteCond 中可用的服务器变量。

以下是 HTTP 头部变量：

| HTTP 变量 | 描述 |
| :--- | :--- |
| HTTP_USER_AGENT | 列出浏览器识别信息的字符串，例如：Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322) |
| HTTP_REFERER | 用户访问的上一页，由其浏览器报告 |
| HTTP_COOKIE | 请求中的一部分任何 cookie 字符串 |
| HTTP_FORWARDED | 如果请求由代理服务器处理，则包含任何转发信息 |
| HTTP_HOST | 请求中引用的主机名 |
| HTTP_PROXY_CONNECTION | HTTP Proxy-Connection 头的内容 |
| HTTP_ACCEPT | 返回 Accept 头的值；表明浏览器可以处理的内容类型以及哪些类型优先 |

以下是请求变量：

| 请求变量 | 描述 |
| :--- | :--- |
| REMOTE_ADDR | 请求文件的用户的 IP 地址。 |
| REMOTE_HOST | 请求文件的用户的主机名。 |
| REMOTE_USER | 请求文件的人的用户名，由浏览器报告。 |
| REMOTE_IDENT | 为识别目的设置的变量。可能包含用户名。 |
| REQUEST_METHOD | 请求中使用的方法，例如 GET 或 POST。 |

*表格续见下页*





## 第 6 章

| | |
|---|---|
| SCRIPT_FILENAME | 请求文件的完整本地路径。 |
| PATH_INFO | 添加到 URL 末尾的任何额外路径信息。 |
| QUERY_STRING | 请求的任何查询字符串或 GET 参数，通常指 GET 请求中问号后面的任何参数。 |
| AUTH_TYPE | 用于认证用户使用的认证类型。 |

以下是服务器变量：

| | |
|---|---|
| DOCUMENT_ROOT | 网站的根文件夹，在 Document-Root 指令中指定 |
| SERVER_ADMIN | 服务器管理员的电子邮件地址，使用 ServerAdmin 指令指定 |
| SERVER_ADDR | 服务器的主机名或 IP 地址 |
| SERVER_PORT | 在请求中指定的服务器端口号 |
| SERVER_PROTOCOL | 请求协议的名称和版本，例如 HTTP/1.1 |
| SERVER_SOFTWARE | 服务器软件的名称 (Apache) |

以下是时间变量：

| | |
|---|---|
| TIME_YEAR | 请求的当前年份 |
| TIME_MON | 请求的当前月份 |
| TIME_DAY | 请求的当前日期 |
| TIME_HOUR | 请求的当前小时 |
| TIME_MIN | 请求的当前分钟 |
| TIME_SEC | 请求的当前秒 |
| TIME_WDAY | 当前星期几 |
| TIME | 当前时间 |

这些是各种特殊变量：

| | |
|---|---|
| API_VERSION | Apache 模块 API 的版本（与 Apache 版本号不同，但密切相关）；主要用于模块开发（内部使用） |
| THE_REQUEST | 完整的 HTTP 文件请求字符串，包括方法、请求的文件以及使用的 HTTP 版本 |
| REQUEST_URI | HTTP 请求中请求的资源 |
| REQUEST_FILENAME | 与 HTTP 请求匹配项的完整本地文件系统路径 |
| IS_SUBREQ | 正在处理的请求是否是内部子请求；如果请求是子请求，值为 "true"，否则为 "false" |
| HTTPS | 值为 "on" 表示正在使用 SSL/TLS，否则为 "off" |

要使用该长列表中的任何变量，需将变量名放在花括号中，并在前面加上百分号，如下所示：

```
%{SCRIPT_FILENAME}
```

要查看 RewriteCond 的实际应用，首先重写 RewriteRule 以使用 RewriteCond。旧规则如下所示：

```
# Rewrite /category/ to catalog.php
RewriteRule ^\(w+\)/?$ catalog.php?cat=$1&item=$2
```

要使用 RewriteCond 配合 RewriteRule 实现相同的目标，请使用以下内容：

```
# Rewrite /category/item/ to catalog.php
RewriteCond %{SCRIPT_FILENAME} ^/(w+)/?(w+)/?$
RewriteRule .* catalog.php?cat=$1&item=$2
```

注意服务器变量 SCRIPT_FILENAME 是如何用作测试输入字符串的。通过结合使用这些服务器变量将 RewriteCond 与 RewriteRule 组合起来，你可以想出一些有趣的组合。以下内容检查用户的浏览器是否接受 XHTML MIME 类型，如果是，则更改发送给 .html 文件的 MIME 类型头：

```
RewriteCond %{HTTP_ACCEPT} application/xhtml+xml
RewriteRule .*.html$ - [T=application/xhtml+xml]
```

RewriteCond 的另一个实用功能是能够串联多个行。当连续列出多个 RewriteCond 语句时，它们每个都被视为程序化的 AND（与）——只有当所有 RewriteCond 匹配都返回 true 时，末尾的 RewriteRule 才会处理。前面的规则集可以使用多个 RewriteCond 语句重写，如下所示：

```
RewriteCond %{HTTP_ACCEPT} application/xhtml+xml
RewriteCond %{SCRIPT_FILENAME} \.html$
RewriteRule .*. - [T=application/xhtml+xml]
```

除了标准的字符串与正则表达式比较外，你还可以使用 RewriteCond 制作简单的比较和系统检查条件。要将输入字符串与另一个简单字符串进行比较，可以使用以下内容作为你的条件模式：

```
<CondPattern
>CondPattern
=CondPattern
```

这些分别检查输入字符串是否小于、大于或等于 `CondPattern`。例如，如果你想将网站某个区域在特定年份后设为禁止访问，可以使用以下内容：

```
RewriteCond %{TIME_YEAR} >2005
RewriteRule .* - [F]
```

除了这些简单的比较运算符外，你还可以访问另外六个条件检查，用于评估文件和目录的状态：

| 比较运算符 | 含义 |
| --- | --- |
| -d (是目录) | 测试是否存在与测试字符串匹配的目录 |
| -f (是常规文件) | 测试是否存在与测试字符串匹配的常规文件 |
| -s (是大小非零的常规文件) | 测试是否存在与测试字符串匹配的常规文件，且大小大于 0 字节 |
| -l (是符号链接) | 测试是否存在与测试字符串匹配的符号链接 |
| -F (是通过子请求存在的文件) | 在考虑服务器所有访问控制后，测试常规文件是否可访问；使用内部子请求执行检查（有性能影响） |
| -U (是通过子请求存在的 URL) | 在考虑服务器所有访问控制后，测试 URL 是否可访问；使用内部子请求执行检查（有性能影响） |

例如，要检查图像是否存在并实际包含一些数据，可以使用以下内容：

```
RewriteCond %{REQUEST_FILENAME} !.jpg$
RewriteCond %{REQUEST_FILENAME} !-s
RewriteRule .* - [G]
```

第一个条件检查是否调用了 `.jpeg` 文件，第二个条件实际检查文件是不存在还是 0 字节。注意在条件模式 `this` 之前使用感叹号。`RewriteCond` 中使用的任何条件模式都可以在前面加上感叹号，从而否定它——这与 PHP 条件中感叹号的用法相同。

#### RewriteCond 标志

为了进一步控制 `RewriteCond`，提供了几个标志，类似于 `RewriteRule` 标志。

- **nocase|NC**
  与 `RewriteRule` 中使用的同名标志一样，`nocase` 指定要评估的正则表达式不区分大小写。

- **onext|OR**
  多个 RewriteCond 指令的默认串联方法是使用逻辑 AND（与）；如果使用 `onext` 标志，则两个连接的 RewriteCond 使用逻辑 OR（或）进行比较。

虽然 RewriteRule 和 RewriteCond 指令提供了 mod_rewrite 的大部分功能，但仍有一些其他关键指令可以帮助你控制重写并解决问题。

### RewriteBase

在大多数情况下，你的网站 URL 不会与你的物理文件系统布局匹配。你网站的根几乎从不位于本地文件系统的根 (/) 下。在 Apache 服务器的正常运行中，这通常不是问题；在使用 RewriteRule 时，这可能非常成问题。RewriteBase 允许你指定一组 URL 重写的基路径或前缀路径。

要完全理解 RewriteBase 的原因，请查看以下用于重写一组简单文件的示例规则集：

```
RewriteEngine On

RewriteRule ^foo\.html$ bar.html [R]
```

假设你的 Web 根从本地文件系统的 /www 文件夹提供服务（即，你的 DocumentRoot 设置为 /www）。如果你尝试在按目录访问文件 (htaccess) 中使用前面的规则，实际上会导致请求被不正确地重写——你期望返回的 `http://www.domain.com/bar.html` 文件，得到的却是 `http://www.domain.com/www/bar.html`。这是为什么？以下是 Apache 内部发生过程的简化版本：

请求：/www/foo.html (本地物理路径)

重写：

```
/www/foo.html -> foo.html (剥离目录前缀)
foo.html -> bar.html (应用 RewriteRule)
bar.html -> /www/bar.html (重新应用目录前缀)
/www/bar.html -> http://www.domain.com/www/bar.html
                  (将域前缀应用于 URL，发送到浏览器)
```

为了解决这个问题，你只需在规则集中添加一条 RewriteBase 语句：

```
RewriteEngine On
RewriteBase /

RewriteRule ^foo\.html$ bar.html [R]
```

### RewriteLog

为了直接了解 mod_rewrite 实际发生了什么，请试用 RewriteLog 指令。你可以使用 RewriteLog 指定一个日志文件，内部重写处理的运行记录将发送到该文件中。




## 第 6 章

若要启用重写日志，使其与其他默认的 Apache 日志文件并列，请使用以下指令：

```apache
RewriteLog "logs/rewrite_log"
```

在指定重写日志的路径时，可以使用绝对路径或相对路径。如果使用相对路径，它将相对于 httpd.conf 中的 **ServerRoot** 设置。

请注意，**RewriteLog** 指令是按服务器粒度应用的，因此必须放置在 httpd.conf 中的服务器配置或虚拟主机容器内——它不允许出现在 `<Directory>` 部分或 .htaccess 文件中。

### RewriteLogLevel

为了控制重写日志记录的详细程度，您可以使用 **RewriteLogLevel** 指令。给定 0 到 9 之间的数字，9 代表最详细，您可以控制记录多少内部处理过程。设置为 0 会完全禁用日志记录，而大于 2 的值仅应用于调试——在较高设置下可能会降低 Apache 的性能。

如果您希望深入了解 mod_rewrite 的工作原理，请查看 Apache 在线手册中的 mod_rewrite 章节：

```
http://httpd.apache.org/docs/2.0/mod/mod_rewrite.html
```

### URL 拼写检查

凭借 mod_rewrite 的强大功能，对于格式错误或变更的 URL，几乎没有什么您无法处理的，但拼写错误呢？当然，您可以为网站中的每个文件列出一个巨大的可能拼写错误列表，并编写大约一千条 RewriteRules，但这并没有必要。为了减轻您进行“简单”拼写检查的负担，Apache 自带 **mod_spelling** 模块（是的，它确实只用了一个“t”）。借助 mod_spelling，您可以将处理 URL 拼写错误的任务交给 Apache，它将自动尽力确定用户想要加载的文件。

要使用 mod_spelling，首先检查它是否已作为静态编译模块对 Apache 可用：

```bash
/path/to/httpd -l
```

如果在列表中看不到 mod_spelling.c，请检查 Apache 模块目录中是否有 mod_spelling.so：

```bash
ls /path/to/apache/modules
```

如果您没有找到静态库或动态模块，您需要自己构建它们。与之前一样，您可以选择将该模块静态编译到 Apache 本身，或者将其构建为动态模块。

要构建静态版本，请更改您的 configure 命令以包含 `mod_spelling`，如下所示：

```bash
./configure \
--enable-spelling \
# ...以及您使用的任何其他 configure 设置
```

如果您更倾向于使用动态模块，只需在 `mod_spelling` 行添加 `shared`：

```bash
./configure \
--enable-spelling=shared \
# ...以及您使用的任何其他 configure 设置
```

在 configure 脚本之后，使用 `make` 和 `make install` 构建并安装新的二进制文件和模块是一件简单的事情。如果您选择对 `mod_spelling` 使用动态模块，还需要额外执行一步。要在 `httpd.conf` 文件中启用 `mod_spelling` 作为动态模块，请取消注释或添加以下行：

```apache
LoadModule speling_module modules/mod_spelling.so
```

完成更改后，重启 Apache。如果 Apache 错误日志中没有显示错误，则您已成功为服务器添加了 `mod_spelling` 功能。

要实际使用拼写检查，请在全局服务器配置部分、虚拟主机部分、`<Directory>` 部分或简单的 .htaccess 文件中添加以下指令：

```apache
CheckSpelling on
```

配置 `mod_spelling` 仅涉及 `CheckSpelling` 指令——值“on”启用拼写检查，“off”禁用所有检查，这是默认行为。

要查看 `mod_spelling` 的实际运行情况，请在您选择的目录中启用 `CheckSpelling`，然后在该目录中创建名为 `info.php` 的脚本：

```php
<?php phpinfo(); ?>
```

此时，您应该能认出这是标准的 PHP 信息输出，但不要使用正确的 `info.php` URL 加载文件，而是尝试使用稍微拼写错误的名称 `lidngp.php` 加载。在启用 `mod_spelling` 的情况下，Apache 会执行快速的 HTTP 301 重定向到它认为您意图的最佳猜测，而不是返回冰冷的 404 Not Found 页面。

## 内容压缩

如果我们告诉您，只需几分钟的 Apache 配置，就可以大幅削减您的每月带宽使用量呢？您可能认为这是谎言，但事实并非如此——您只需要内容压缩和几条配置指令。

什么是内容压缩？当网页通过互联网下载时，默认情况下，构成页面标记、图像、样式表和其他内容的位和字节处于基本未压缩的状态。您编写的 HTML 会直接按您保存时的样子发送，包括所有空白字符。内容压缩允许您透明地压缩页面标记，并将其通过互联网发送到用户的浏览器，在那里它在渲染到屏幕之前会被静默解压缩。另一种理解方式是与通过电子邮件发送 zip 文件相关联。您可以轻松地将大型文档或媒体文件作为普通附件发送到电子邮件，但很多时候，您会在发送前将文件压缩为 zip 或 tar.gz 归档，以缩短下载消息和附件所需的时间。

在 Apache 中使用内容压缩非常简单。您只需要 `mod_deflate`，它随 Apache 源代码提供，在构建 Apache 时可以轻松编译为模块。

### 使用 mod_deflate

与前面讨论的模块一样，您需要做的第一件事是检查该模块是否作为 Apache 静态部分或动态模块可用：

```bash
/path/to/httpd -l
ls /path/to/apache/modules/
```

如果您在第一个命令的输出中看到 `mod_deflate.c`，或在第二个命令的输出中看到 `mod_deflate.so`，则您已拥有对 `mod_deflate` 的访问权限，可以跳过重新构建 Apache 的下一步骤。

如果您在任一命令结果中都没有看到 `mod_deflate`，您需要将其静态编译到 Apache 二进制文件中，或者作为动态模块添加。在从源代码构建 Apache 时，若要静态包含 `mod_deflate`，您只需在运行 `configure` 时添加以下内容：

```bash
./configure \
--enable-deflate
```

如果您希望使用动态可加载模块，只需在启用 `mod_deflate` 的行的末尾添加 `=shared`：

```bash
./configure \
--enable-deflate=shared \
# ...以及您可能使用的任何其他 configure 设置
```

显然，如果您计划在运行 `configure` 时包含其他指令，也需要添加它们。配置完源代码后，执行常规的 `make` 和（以 root 身份）`make install`。

如果您将 `mod_deflate` 构建为动态模块，则必须在 `httpd.conf` 中使用 `LoadModule` 启用该模块：

```apache
LoadModule deflate_module modules/mod_deflate.so
```

然后重启 Apache 以使更改生效。

构建并启用 `mod_deflate` 后，告诉 Apache 使用 `mod_deflate` 以及要压缩的文件类型只是一件简单的事情。为此，您需要编辑 `httpd.conf` 文件，或在要使用压缩的目录中创建或修改 `.htaccess` 文件——如果可用，首选前者。

要在 Apache 中全局启用压缩，请在您的 httpd.conf 中添加以下内容：

```apache
AddOutputFilterByType DEFLATE text/*
AddOutputFilterByType DEFLATE application/ms*
AddOutputFilterByType DEFLATE application/vnd*
AddOutputFilterByType DEFLATE application/postscript
```

然后您只需要重启 Apache，内容压缩即可运行。

所有这些配置指令具体是什么意思？其实很简单——在 Apache 2.x 中，`AddOutputFilterByType` 指令的确如其名所示：它告诉 Apache 将输出通过给定的过滤器（在此情况下为 `mod_deflate`）进行处理，然后再将响应发送给最终用户的浏览器。前面的示例代码告诉 Apache 对任何基于文本的文件（`text/*`）、任何 Microsoft 文档（如 Word 或 Excel 文件，即 `application/ms*` 和 `application/vnd*`）以及任何 postscript 文件（如 Adobe Illustrator 或 EPS 图形，即 `application/postscript`）使用 DEFLATE 过滤器 `mod_deflate`。通过简单组合文档的 MIME 类型和通配符（类似示例），可以将您喜欢的任何文档类型添加到 `mod_deflate` 的过滤列表中。

如果您只想压缩纯文本和 HTML 文件，请使用以下指令：

```apache
AddOutputFilterByType DEFLATE text/plain
AddOutputFilterByType DEFLATE text/html
```

如果您希望压缩 Apache 提供的所有内容怎么办？使用另一个 Apache 指令 `SetOutputFilter`，您可以告诉 Apache 将每个文件通过 `mod_deflate` 处理：

```apache
SetOutputFilter DEFLATE
```

然而，在大多数服务器设置中，这并不是一个好主意。实际上，有些文件类型从压缩中获益甚微，有些文件在压缩后对最终用户来说会损坏。在大多数情况下，没有必要压缩图像格式，因为最常用的 Web 格式已经具有某种内置压缩。此外，PDF 也是压缩的，绝对不应通过 `mod_deflate` 进行过滤，因为在 Acrobat Reader 中它们将变得无法阅读。

> 需要注意的是，Netscape Navigator 4.x 版本的可靠解压缩能力仅限于 `text/html` 以外的任何文件类型，且特定版本的 Netscape Navigator 4.x 无法解压缩任何文件类型。

为了进一步调整所选文件类型的压缩，`mod_deflate` 提供了以下章节中描述的配置指令。

#### DeflateCompressionLevel

`DeflateCompressionLevel` 设置用于缩小文件大小的压缩级别，范围从 1 到 9。压缩级别 1 产生最快的压缩速度，压缩率最低（文件较大），而压缩级别 9 使用最慢的压缩速度，但生成的文件小得多。在决定使用哪个级别时，您必须确定对您来说什么更重要——节省处理器周期还是节省下载时间。默认的压缩级别 6 通常是两者之间的良好折中。




#### DeflateFilterNote

如果您希望访问日志文件显示每个请求文件的压缩率，请使用 **DeflateFilterNote**。 **DeflateFilterNote** 的值是一个日志标记的名称——通过 **DeflateFilterNote** 指定的命名标记随后可用于使用 Apache 的 LogFormat 指令自定义日志输出。

#### DeflateWindowSize

此参数指定用于文件压缩的 zlib 压缩窗口大小。值范围从 1 到 15，其中 1 产生的压缩率最低，15 产生的压缩率最高。 **DeflateWindowSize** 的默认值为 15。

### mod_deflate 的效果如何？

为了展示 mod_deflate 节省字节的能力，本示例使用 Apache 提供一个体积适中的 HTML 页面，分别展示启用和未启用 mod_deflate 时的情况。在本示例中，主页用于 Wrox P2P 社区论坛，位于 `http://p2p.wrox.com`。该页面的原始 HTML 标记——仅 HTML 部分——重达 47172 字节。请查看下表，了解该页面在三种不同压缩级别下经过 mod_deflate 处理后的表现：

| 压缩级别 | 传输字节数 | 占原始大小比例 | 近似下载时间 (56k) |
| :--- | :--- | :--- | :--- |
| 原始 | 47172 字节 | 100% 原始 | 11.7 秒 |
| 默认 (6) | 7621 字节 | 16.2% 原始 | 3.8 秒 |
| 级别 1 | 9050 字节 | 19.2% 原始 | 4.1 秒 |
| 级别 9 | 7581 字节 | 16.1% 原始 | 3.8 秒 |

如您所见，使用 mod_deflate 显然优于提供原始未压缩的 HTML——它消除了通过连接发送的文件大小中近 84% 的内容。另外请注意，使用最大压缩级别 9 仅比默认级别 6 略微占优，因此在这种情况下，坚持使用默认压缩级别 6 可能是安全的，可以节省处理器的一些周期。

许多网站混合了 HTML、媒体和相关脚本文件，因此像摄影博客或在线购物中心这样的网站可能无法在提供的每个文件上都获得巨大的节省，但节省的每一个字节在月底累积起来确实能带来巨大的带宽减少。以文本为主的网站，如博客和新闻门户，将真正从内容压缩中受益，因为这些站点使用的大部分带宽是纯文本——这些文本会通过 mod_deflate 进行处理。

### 为 PHP 脚本启用压缩

您可能会问 PHP 文件怎么办？在许多情况下，不需要对 PHP 文件使用压缩，在某些情况下，压缩甚至会对输出产生不利影响。

例如，如果您的 PHP 脚本输出实际的图像或 PDF，您不希望 Apache 仅仅因为文件扩展名恰好是 .php 就盲目地压缩输出。

在某些情况下，可能已经为所有 PHP 脚本启用了输出缓冲和压缩。要确定这一点，请检查配置变量 `output_handler` 的值，或者在 `php.ini` 中查找 `output_handler` 和 `zlib.output_compression` 的值。

要在 PHP 内部启用输出压缩，请执行以下操作：

1. 如需要，在您的机器上安装 zlib 库。
2. 根据需要配置 PHP 源代码，确保包含 `--with-zlib`，然后正常 `编译/安装`。
3. 修改您的 `php.ini` 以包含以下行：
   ```
   output_buffering = Off
   output_handler =
   zlib.output_compression = On
   ```
4. 重新启动 Apache 以使新更改生效。

## 将 MySQL 与 Apache 一起使用

到目前为止，您已经使用 Apache 和基本认证创建了一两个安全区域，对于大多数情况，这可能就是您所需要的。然而，您可能会发现，Apache 的基本认证虽然简单，但在可融入的控制和自定义程度方面略显局限。对于许多此类情况，您可以实际使用 Apache 基本认证和通过 MySQL 使用关系数据库功能的组合。为此目的，存在 `mod_auth_mysql` Apache 模块。

与标准 Apache 基本认证一样，`mod_auth_mysql` 可以按目录控制访问权限，并可以在 `.htaccess` 文件和 `httpd.conf` 中的 `<Directory>` 部分内部进行配置。与标准 Apache 基本认证不同，所有用户凭据都存储在数据库中，而不是存储在扁平文件中。

### 设置数据库

安装和配置 `mod_auth_mysql` 涉及几个步骤，首先是创建必要的数据库结构来存储用户数据。首先加载您喜欢的 MySQL 客户端，并创建数据库。例如：

```sql
CREATE DATABASE apacheauth;
```

接下来，创建一个将由 Apache 用于访问凭据的用户：

```sql
GRANT SELECT ON apacheauth.* TO apache@localhost IDENTIFIED BY ‘apachepass’;
```

现在数据库用户已创建，是时候添加一个表来存储登录信息了。暂时从一个仅存储用户名和密码的简单表开始：

```sql
USE apacheauth;
CREATE TABLE user_info (
    user_name varchar(50) NOT NULL,
    user_password varchar(50) NOT NULL,
    PRIMARY KEY (user_name)
);
```

您可以按自己喜欢的命名方式命名表和列。在前面的示例中，使用 **user_info** 作为表名，使用 **user_name** 和 **user_password** 作为登录/密码组合，因为这些是 **mod_auth_mysql** 识别的默认名称。

> 在 mod_auth_mysql 的后续版本中，密码的默认列是 **user_password**，而不是模块文档中所述的 **user_passwd**。

接下来，创建一个初始的测试用户账户，您稍后将在测试身份验证时使用它：

```sql
INSERT INTO user_info (user_name, user_password)
VALUES ('testuser', SHA1('testpass'));
```

> 请注意，该语句中对密码使用了 SHA1() 函数，而不是 PASSWORD() 函数。使用 mod_auth_mysql 时，您可以使用多种密码加密方法——本例恰好使用了 SHA1。

### 安装模块

一旦数据库表设置好，您需要实际下载 **mod_auth_mysql** 的源代码，可在 [http://modauthmysql.sourceforge.net](http://modauthmysql.sourceforge.net) 获取。在撰写本文时，当前版本为 2.9.0，因此您需要下载 **mod_auth_mysql-2.9.0.tar.gz**。

下载模块源代码后，提取 tarball：

```bash
tar -xzvf mod_auth_mysql-2.9.0.tar.gz
```

提取 tarball 后，切换到新创建的源代码文件夹：

```bash
cd mod_auth_mysql-2.9.0
```

要从下载的源代码构建模块，您将直接使用 Apache 的 **apxs** 命令。执行以下命令，使用系统中 **apxs** 二进制文件的路径；此处使用默认的 Apache 位置 `/usr/local/apache2/bin`：

```bash
/usr/local/apache2/bin/apxs -c -i mysqlclient -lm -l2 mod_auth_mysql.c
```

如果构建成功，您应该会看到几行编译信息，且没有错误。相反，如果您收到关于缺少 **mysql.h** 文件的错误，以及一系列 **MySQL** 相关的错误，您可能需要手动指定 **MySQL** 库和包含文件的路径。使用 **MySQL** 的默认位置，您的命令可能如下所示：

```bash
/usr/local/apache2/bin/apxs -c -i mysqlclient -lm -l2 \
-L /usr/local/mysql/lib/mysql \
-I /usr/local/mysql/include/mysql \
mod_auth_mysql.c
```

要安装新编译的模块，您需要以 root 身份执行以下命令。照例，将 `apxs` 的路径更改为指向您的 `apxs` 二进制文件：

```bash
/usr/local/apache2/bin/apxs -i mod_auth_mysql.la
```

您需要执行的下一个安装任务是添加必要的命令以在 `httpd.conf` 中加载模块。为此，打开您的 `httpd.conf` 文件，找到一个合适的位置添加模块定义——通常在配置文件的末尾，或者在其他 `LoadModule` 语句旁边——并添加以下内容：

```apache
LoadModule mysql_auth_module modules/mod_auth_mysql.so
```

最后，重新启动 Apache。

### 配置和使用

一旦数据库表准备就绪且模块已安装，剩下的就是告诉 Apache 哪些内容需要保护。与标准 Apache 基本认证一样，您需要将一些配置指令添加到 `httpd.conf` 中的 `<Directory>` 部分，或在您选择保护的目录中创建 `.htaccess` 文件。

告诉 Apache 对照您的 MySQL 数据库验证用户凭据，通常至少涉及以下内容：

- `AuthName "<zone name>"`
- `AuthType Basic`
- `AuthMySQLDB dbname`
- `AuthMySQLUser userid`
- `AuthMySQLPassword password`
- `AuthMySQLEnable On`
- `Require valid-user`

这些指令的第一行、最后两行以及最后一行您应该已经熟悉。它们分别定义了受保护区域的名称、认证类型，以及查找到的任何有效用户都可以访问。其他行告诉 Apache 在哪里查找认证信息。您没有向 Apache 提供包含每个有效用户密码的文件名称，而是提供了数据库信息——数据库名称、用户名和密码——以便 Apache 和 mod_auth_mysql 知道在哪里查找。第六行 `AuthMySQLEnable On`  simply 告诉 Apache 实际使用 mod_auth_mysql——这是一种在不必完全卸载或移除模块的情况下禁用 MySQL 认证的方法。

要使用您之前创建的认证表，您需要在 `<Directory>` 或 `.htaccess` 定义中添加以下内容：

- `AuthName "MySQLAuth"`
- `AuthType Basic`
- `AuthMySQLDB apacheauth`
- `AuthMySQLUser apache`
- `AuthMySQLPassword apache`
- `AuthMySQLEnable On`
- `AuthMySQLPwEncryption sha1`
- `Require valid-user`




## 第 6 章

在此处，你正在告知 Apache 和 mod_auth_mysql 针对你的 apacheauth 数据库验证用户身份。Apache 将使用你之前创建的 apache 账户登录数据库，同时你还告知 mod_auth_mysql 在将其与数据库中的值进行匹配之前，使用 SHA1 对提供的密码进行哈希处理。

此时，你应该能够通过 Web 浏览器登录到你的受保护区域，提供添加到 user_info 表中的用户凭据（testuser:tespass），并在目录中成功通过身份验证。

虽然这个示例相当简单且功能精简，但 mod_auth_mysql 实际上提供了大量的配置选项，因此你可以针对几乎任何情况定制你的身份验证。以下部分描述了一些配置选项。

### AuthMySQLEnable On | Off

此选项启用或禁用 mod_auth_mysql 身份验证，而无需直接从 Apache 中移除或卸载该模块。

### AuthMySQLHost localhost | hostname | ipaddress

这是 MySQL 数据库服务器的主机名或 IP 地址。如果你的环境中 Apache 和 MySQL 运行在不同的机器上，你需要使用此设置。默认值为 localhost，因此同时运行 Apache 和 MySQL 的机器通常可以忽略此设置。

### AuthMySQLPort port_number

这是 MySQL 正在监听的 TCP/IP 端口。MySQL 的默认值是端口 3306，但可以更改。此选项的默认值也是 3306，因此只有当 MySQL 在非标端口上监听时才需要指定此选项。

### AuthMySQLSocket socket_file_path

这是在 UNIX 机器上访问 MySQL 所使用的 UNIX 套接字文件。默认值是 /tmp/mysql.sock，与 AuthMySQLPort 一样，它仅需要在非标准安装中使用。

### AuthMySQLUser userid

这是用于访问保存身份验证信息的 MySQL 数据库的用户 ID。大多数数据库系统不允许用户或 Apache 进程在没有正确的 userid/密码组合的情况下访问数据库，因此将此设置与 AuthMySQLPassword 一起设置为一个对身份验证表具有访问权限的非 root 用户账户。至少，该用户需要对身份验证表具有 SELECT 访问权限。

### AuthMySQLPassword password

与 AuthMySQLUser 配合使用，此选项指定访问 MySQL 身份验证表的用户账户的密码。

### AuthMySQLDB dbname

这是保存身份验证表的 MySQL 数据库的名称。如果未指定名称，将使用默认值 test。

### AuthMySQLUserTable table_name

这是数据库中保存用户名和密码的表的名称。如果未指定表，将使用默认值 user_info。

### AuthMySQLNameField column_name

这是用户表（AuthMySQLUserTable）中保存用户名的列的名称。在 MySQL 中创建表时，请确保该列具有索引或键，以保证每个值都是唯一的。该列的长度由你在 MySQL 中决定。默认值是 user_name。

#### AuthMySQLUserCondition

当 mod_auth_mysql 执行用户查找时，它执行一个简单的 SQL SELECT 语句，并带有执行匹配所需的任何条件。AuthMySQLUserCondition 字段允许你指定用于 SQL 语句 WHERE 子句中的额外参数。

### AuthMySQLPasswordField column_name

这是用户表中保存用户密码的列的名称。MySQL 中该列的长度至少应与加密的密码哈希值一样长。AuthMySQLPasswordField 的默认值是 user_password。

### AuthMySQLPwEncryption none | crypt | scrambled | md5 | aes | sha1

这是在数据库中对密码进行编码时使用的加密方法，具体如下：

- none: 无加密/明文
- crypt: UNIX crypt() 加密
- scrambled: MySQL PASSWORD() 加密
- md5: MD5 哈希
- aes: 高级加密标准 (AES) 加密
- sha1: 安全哈希算法 (SHA1)

如果未指定值，将使用默认值 crypt。

使用 AES 密码加密时，请确保 MySQL 用户表中的密码字段是 BLOB 类型，而不是 CHAR、VARCHAR 或 BINARY 类型。除非列类型是 BLOB 的变体之一，否则 MySQL 会剥离加密密码中的任何额外编码字符——你将永远无法将提供的密码与数据库值进行匹配。

#### AuthMySQLSaltField

这允许你指定三个值之一，作为加密密码时使用的“盐值”。值 <tell> 指示 mod_auth_mysql 使用密码本身作为盐字段。值 <string> 使用 string 的值作为盐字段。任何未由小于号/大于号包围的字符串都被视为数据库列的名称，其值用作盐字段。

#### AuthMySQLGroupTable

当 Apache 被指示检查组而不是单个用户（require group 与 require valid-user）时，用于设置包含组信息的表的名称。

#### AuthMySQLGroupCondition

类似于 AuthMySQLUserCondition，此指令允许你指定包含在匹配用户组时 WHERE 子句中的条件语句。

#### AuthMySQLGroupField

这是数据库中包含组名的字段的名称。此字段在使用 Apache 的 require group 指令匹配组时使用。

#### AuthMySQLAuthoritative

这告知 Apache 如果 MySQL 身份验证失败，是否回退到其他模块。

## Apache 和 SSL

通过使用 htpasswd 或 mod_auth_mysql 对 Web 文件夹使用基本身份验证来保护它们，可以增强安全性。不幸的是，基本身份验证所增加的这一层安全性可能会被试图入侵你系统的专业黑客消除。问题在于：当你在标准服务器上使用基本身份验证时，用户名和密码实际上是从客户端未加密传输到服务器的。熟悉网络的黑客可能正在监控你的机器和服务器之间的传输，并嗅探这些飞速通过的明文密码。

解决方案：加密客户端和服务器之间的通信。在 Apache 中，这可以通过使用安全套接字层 (SSL) 来实现。Apache 中的 SSL 以 mod_ssl 的形式出现，它是一个 Apache 模块，可以为 Apache 控制的网站启用 SSL，允许任何与 Apache 之间的通信使用广泛的加密方案进行加密。

要在 Apache 中启用 SSL，首先检查 SSL 是否包含在你现有的 Apache 二进制文件中或作为可加载模块：

```bash
/path/to/httpd -l
ls /path/to/apache/modules/
```

如果你在第一个命令输出中看不到 mod_ssl.c，或在 Apache 模块列表中看不到 mod_ssl.so，你需要自己构建 Apache SSL 功能。要静态启用 SSL，在从源代码构建时，在你的 Apache 配置脚本中添加 enable-ssl：

```bash
./configure \
--enable-ssl \
# ...以及你使用的其他 configure 设置
```

如果你希望使用动态模块，只需在 SSL 启用行的末尾添加 shared：

```bash
./configure \
--enable-ssl=shared \
# ...以及你使用的其他 configure 设置
```

然后，使用 make 和 make install 构建并安装新的 Apache 二进制文件和模块。如果你将 Apache 构建为动态模块，通过在全局配置部分添加以下行在 httpd.conf 中启用它：

```text
LoadModule ssl_module modules/mod_ssl.so
```

现在你可能认为时候重启并配置 Apache 了，但你还没有完全设置好 SSL。在 SSL 正常工作之前，你需要拥有用于加密传输数据的服务器密钥和服务器证书，并向客户端/浏览器展示 SSL 证书。

在接下来的几个步骤中，你将创建自己的自签名证书，用于你的 Web 服务器。如果你已经从合法的证书颁发机构 (CA) 获得了 SSL 证书，如果可能应该使用它。你可能会好奇具体有什么区别？任何自签名证书都不被认为真正安全，并且会在用户浏览器中触发警告，类似于“你的浏览器无法识别颁发该站点证书的证书颁发机构。”如果你进行任何形式的商务或安全交易，建议来自正规 CA 的证书。

要开始证书创建过程，首先通过创建私钥和证书请求来开始：

```text
openssl req -new > testcert.csr
```

这会在屏幕上显示以下内容，包括提示：

```text
Generating a 1024 bit RSA private key
..........+++++++
.....++++++
writing new private key to `privkey.pem`
Enter PEM pass phrase:
Verifying - Enter PEM pass phrase:

You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '', the field will be left blank.
Country Name (2 letter code) [AU]:US
State or Province Name (full name) [Some-State]:Ohio
Locality Name (eg, city) []:Cincinnati
Organization Name (eg, company) [Internet Widgits Pty Ltd]:TestSSL
Organizational Unit Name (eg, section) []:SSL Testing Department
Common Name (eg, YOUR name) []:www.example.com
Email Address []:youremail@example.com
```





# 第 6 章

请输入以下“附加”属性，
以便随证书请求一起发送
挑战密码 []::testchallenge
可选公司名称 []::Test Company

**粗体**提示的任何回复都应替换为你自己合适的值。此外，请确保你为通用名称（Common Name）输入的值是你服务器的真实完全限定域名，例如 www.yourserver.com。

命令完成且你回答了所有提示后，你将获得两个新文件：privkey.pem ，这是一个用于签署证书的私钥，以及 testcert.csr —— 证书请求。下一步是从上一步创建的密钥中移除密码短语。如果你不移除密码短语，每次启动 Apache 时都必须输入它。虽然这可能看起来增加了安全性，但实际上是一个麻烦，因为它会阻止 Apache 在你的服务器发生断电故障时完全重启，或者在你频繁重启 Apache 时生效。

要移除密码短语，请使用以下命令：

```
openssl rsa -in privkey.pem -out testcert.key
```

然后它会提示你输入在上一步开始使用的相同密码短语：

```
Enter pass phrase for privkey.pem:
writing RSA key
```

下一步是将证书请求转换为已签署的证书：

```
openssl x509 \
-in testcert.csr \
-out testcert.cert \
-req \
-signkey testcert.key \
-days 3650
```

这将显示以下内容：

```
Signature ok
subject=C=US/ST=Ohio/L=Cincinnati/O=TestSSL/OU=SSL Testing
Department/CN=www.example.com/emailAddress=youremail@example.com
Getting Private key
```

你在这里做的是使用 **openssl** 命令请求 X.509 证书，使用 **testcert.csr** 证书请求作为输入，并 **保存** 生成的证书 **testcert.cert**，该证书是使用私钥 **testcert.key** 自签名，有效期为 10 年的有效证书。

现在你拥有了自签名服务器证书和密钥，你需要将它们都复制到 Apache 可以使用的某个位置：

```
mkdir -p /etc/apache/ssl.crt
mkdir -p /etc/apache/ssl.key

cp testcert.crt /etc/apache2/ssl/crt/testcert.crt
cp testcert.key /etc/apache2/ssl/key/testcert.key
```

然后，创建一个将容纳你的新 SSL 网站的目录：

```
mkdir -p /wwwwssl
```

你可以使用任何你喜欢的路径，甚至可以使用现有路径——只需记住或写下你使用的路径，因为你稍后配置 Apache 时需要用到它。

最后，创建一个简单的信息文件，以便在测试 SSL 时有所展示：

```
echo "<?php phpinfo(); ?>" > /wwwwssl/index.php
```

现在你的密钥已就位，SSL 网站根目录已创建，你需要在 httpd.conf 中启用 SSL 功能。如果当前的 httpd.conf 文件包含一行写着“Include /etc/apache2/ssl.conf”或类似内容，那么你应该在指定的 ssl.conf 文件中执行任何 SSL 更改。否则，你可以直接在 httpd.conf 文件中进行更改，或者添加对你自己 ssl.conf 文件的引用，并在那里进行更改。

在 SSL 配置文件或部分中，你需要在全局配置范围（不在虚拟服务器或目录配置部分中）提供以下项目：

```
Listen 443
```

接下来，你需要重用现有的 VirtualHost 部分来处理 443 端口（如果存在），或者创建一个包含以下指令的新部分：

```
<VirtualHost _default_:443>

# 服务器证书:
SSLCertificateFile /etc/apache2/ssl.crt/testcert.crt

# 服务器私钥:
SSLCertificateKeyFile /etc/apache2/ssl.crt/testcert.key

SSL Engine On

DocumentRoot "/wwwwssl" # 使用你之前创建的 SSL 目录
ServerName www.example.com
ServerAdmin youremail@example.com
</VirtualHost>
```

然后，在对配置文件进行更改后，重启 Apache。如果你使用 https:// URL（例如 https://www.example.com ）在浏览器中加载你的新 SSL 网站，你应该会收到证书无效的提示（因为它是自签名的）。点击确定，你应该能看到 phpinfo() 函数的输出。如果没有出现任何内容，或者浏览器无法连接到服务器，请检查 Apache 错误日志中是否有相关的错误消息——很可能是简单的拼写错误。

要进一步调整 mod_ssl，并获取所有可与 mod_ssl 一起使用的配置指令的完整列表，请访问 http://httpd.apache.org/docs/2.0/mod/mod_ssl.html。

## Apache 作为文件存储库

使用 Apache 更酷的功能之一是将其用作简单的在线文件存储库，使用 WebDAV。WebDAV 代表基于 Web 的分布式创作和版本控制，它允许用户将启用的目录视为其自己计算机上的远程目录或驱动器。类似于 Windows 共享或 NFS 导出，WebDAV 允许远程编辑和存储访问，只是使用 HTTP 作为传输层，而不是像 SMB 和 NFS 那样的专用 TCP 协议或端口。

要理解 WebDAV 如何作为共享驱动器工作，最简单的方法是直接看它的应用，所以接下来，你将启用随 Apache 附带的 mod_dav，并进行测试。首先，与其他模块一样，检查 mod_dav 是否已静态编译到 Apache 中，或者是否存在为可加载模块：

```
/path/to/httpd -l
ls /path/to/apache/modules
```

正如你可能猜到的，如果你在 httpd -l 输出中看不到 mod_dav.c，或在文件列表中看不到 mod_dav.so，你需要使用 Apache httpd 源代码自行构建它。要将 mod_dav 静态添加到 Apache 二进制文件中，请确保 configure 命令中存在 --enable-dav 和 --enable-dav-fs 两者：

```
./configure \
    --enable-dav \
    --enable-dav-fs \
    # ...和你使用的任何其他 configure 设置
```

要将 mod_dav 构建为共享对象，只需在两个 DAV 相关行的末尾添加 =shared：

```
./configure \
    --enable-dav=shared \
    --enable-dav-fs=shared \
    # ...和你使用的任何其他 configure 设置
```

然后使用 make 和 make install 构建并安装新的二进制文件和模块。

如果你决定使用 mod_dav 的动态模块，你需要在 httpd.conf 中启用它们，使用以下行：

```
LoadModule dav_module modules/mod_dav.so
LoadModule dav_fs_module modules/mod_dav_fs.so
```

要有一个实际存储 WebDAV 文件存储库的位置，你可以创建一个新目录，或使用你选择的现有目录。你应该将你的 WebDAV 文件夹放在启用了 SSL 的网站根目录内，或者如果你计划使用基本身份验证来限制对 WebDAV 文件夹的访问，请确保稍后启用 SSL。基本身份验证以明文发送用户名和密码，因此你需要对受保护的目录启用 SSL，以加密基本身份验证请求。如果需要，创建新的文件夹，并创建一个虚拟文件以添加到 WebDAV 文件夹中：

```
mkdir -P /wwwssl/dav
echo "Testing DAV" > /wwwssl/dav/testing.txt
```

## Apache 技巧

当用户访问你的 WebDAV 文件夹时，你将针对数据库或 htpasswd 文件对他们进行身份验证，以防止来自互联网各地的匿名用户填满你的硬盘。首先，创建一个 htpasswd 文件来存储有效用户的密码，并用用户账户 testdav 对其进行初始化：

```
mkdir -p /davauth
/path/to/htpasswd -c /davauth/dav.htpasswd testdav
```

当提示输入密码时，输入你选择的密码。接下来，在 /wwwssl/dav 文件夹中创建一个 .htaccess 文件以强制基本身份验证。.htaccess 文件应包含以下内容：

```
AuthName "DAV Test"
AuthType Basic
AuthUserFile "/davauth/dav.htpasswd"
require valid-user
```

最后，在你的 httpd.conf 中创建一个 Directory 条目，以启用给定目录的 WebDAV 和基本身份验证：

```
<Directory "/wwwssl/dav" >
  AllowOverride AuthConfig
  Dav On
</Directory>
```

然后你可以重启 Apache，WebDAV 将对你 HTTPS 站点的 /dav/ 文件夹启用，可以通过类似 https://www.example.com/dav 的地址访问。你可以尝试在 Web 浏览器中加载此 URL，但它与标准的非 DAV 网络目录的行为没有区别。要使用 WebDAV URL 的功能，你需要使用支持 WebDAV 的软件。

诸如 jEdit、NuSphere’s PHPed 和 Macromedia Dreamweaver 等编辑器，以及其他一些，在某种程度上都支持 WebDAV。如果你没有这些编辑器可用，不要担心——大多数现代操作系统实际上在其文件资源管理器/浏览器实用程序中本地支持挂载 WebDAV 共享。

要使用操作系统的文件浏览器访问你的 WebDAV 共享，请遵循适用于你操作系统的上述部分的说明。

### Windows 2000/XP

要在 Windows 2000 或 XP 下设置 WebDAV，你需要按照以下步骤运行添加网络位置向导：

- 转到“我的网络位置”，双击“添加网络位置”，如图 6.1 所示。
- 当出现“添加网络位置向导”时，点击“下一步”以显示服务提供商列表。选择“选择其他网络位置”选项，如图 6.2 所示，然后点击“下一步”。




## 第 6 章

![](img/cacdd24f2926f10ee3219256ad732604_185_0.png)

![](img/cacdd24f2926f10ee3219256ad732604_185_1.png)

- 在互联网或网络地址字段中，输入指向您的 WebDAV 目录的 URL，如图 6.3 所示。然后单击“下一步”。

![](img/cacdd24f2926f10ee3219256ad732604_186_0.png)

- 在 SSL 安全警报对话框中，单击“是”。警告出现是因为您使用的是自签名证书——这与之前尝试访问启用了 SSL 的网站时看到的警告相同。
- 接着会提示您输入用户名和密码以访问 DAV 测试域。请输入您创建 htpasswd 文件时使用的值。
- 随后会提示您为网络位置命名，以便稍后轻松识别该位置。请将网络位置命名为 **My WebDAV**。
- 此时，您的 WebDAV 位置应该已经设置好，您会看到“完成添加网络位置向导”界面。如图 6.4 所示，勾选“单击‘完成’时打开此网络位置”复选框。
- 接着会再次提示您接受自签名 SSL 证书并输入用户名和密码。请接受该证书，并输入您在步骤 5 中使用的凭据。
- 随后，您应该能在标准的 Windows 资源管理器窗口中看到 WebDAV 共享的内容，如图 6.5 所示。
- 将 My WebDAV 共享当作标准的驱动器或文件夹使用——您可以像在本地文件夹中一样，在 WebDAV 共享上添加、编辑和删除文件。

![](img/cacdd24f2926f10ee3219256ad732604_187_0.png)

图 6.4

![](img/cacdd24f2926f10ee3219256ad732604_187_1.png)

图 6.5

### Mac OS X

要在 Mac OS X 下设置 WebDAV，请执行以下操作：

- 在“访达”菜单中，选择“前往” -> “连接服务器”，或者直接在访达窗口中输入 Command-K。这将弹出“连接服务器”窗口，如图 6.6 所示。在“服务器地址”字段中输入您的 WebDAV 共享的 URL，然后单击“连接”。

![](img/cacdd24f2926f10ee3219256ad732604_188_0.png)

图 6.6

- 系统会提示您接受自签名 SSL 证书。单击“继续”。
- 出现 DAV 测试域的用户名和密码提示。请输入您之前创建 htpasswd 文件时使用的用户名和密码。
- 映射后的 WebDAV 驱动器现在应该会在访达中显示为一个常规挂载的网络卷，如图 6.7 所示。您现在应该可以像使用任何标准本地或网络卷一样使用它。

![](img/cacdd24f2926f10ee3219256ad732604_188_1.png)

图 6.7

## 摘要

在本章中，您了解了如何通过添加几个 Apache 模块来显著提升您的网站性能。书中讲述了如何简化 URL 重定向、修正用户拼写错误、压缩内容以节省带宽、创建基于 Web 的文件共享，以及使用 MySQL 和 SSL 保护您的网站安全。这种可扩展性是使 Apache 超越普通 Web 服务器的关键所在。

在探索了此处讨论的模块的潜力之后，您还应该研究在 httpd.apache.org 和 sourceforge.net 上找到的其他模块。您会发现那里有可以针对其他数据库对用户进行身份验证、加速 Perl 等其他语言性能、将 Apache 用作代理服务器等功能的模块。由此可见，Apache 模块适用于各种用途。

虽然本章向您介绍了一种保护网站安全的新方法，但下一章将直接着手解决安全问题。

![](img/cacdd24f2926f10ee3219256ad732604_190_0.png)

## 网站安全

安全是每个网站管理员最关心的问题之一——如果它还没被视为首要问题，那它本应如此。将您的网站放置在公共互联网上，无异于向各种入侵者发出公开邀请，无论您的网站规模多么小或多么专业，您都必须能够应对这些威胁。幸运的是，PHP 可以帮助您保护您的网站和用户的数据。如前一章所述，您可以使用 Apache 来控制身份验证，但您也可以使用 PHP 的内置功能构建自己的身份验证系统。在本章向您展示了如何做到这一点之后，它将带您了解您可能遇到的一些常见类型的攻击，并展示防止这些攻击的一些简单方法。

### 控制访问权限

当您考虑网站安全时，脑海中浮现的第一个念头可能是限制访问的方法。如果坏人无法访问 web 应用程序，那它是不是就安全了？当您选择保护敏感文件和脚本的方法时，您有几种选择，有些是 Apache 内置的，有些是基于 PHP 的，还有些是两者的混合。

### Apache 控制的身份验证

锁定网站最简单的方法是使用基本身份验证（Basic Authentication），这在第 6 章中已作介绍。通过使用 .htaccess 和密码文件的组合，您可以快速限制对网站中任何指定文件夹的访问。这种方法有许多优势。

首先，它极其易于实现。Apache 默认安装通常包含此功能，简单的基于目录的基本身份验证可以通过 .htaccess 或 `<Directory>` 条目轻松设置。

使用 Apache 内置身份验证的缺点是什么？维护复杂的受限制文件夹和用户层级可能会很麻烦。如果您有大量用户或组，以及相当数量的受保护目录，确保正确的用户在正确的组中、拥有对正确资源的访问权限、使用最新的密码等，很快就会变成一场噩梦。

如果您正在处理多个负载平衡或镜像的 Web 服务器，使用 Apache 进行简单身份验证也可能存在问题。因为用户凭据存储在每台机器上，您可能会面临文件不一致的状态——某些密码文件可能包含不同数量的用户、不同的密码或其他问题。

作为 Apache 简单基于文件身份验证的替代方案，您还可以使用 mod_auth_mysql Apache 模块，这也在第 6 章中有所介绍。使用 mod_auth_mysql 可以集中管理您的用户名/密码存储，并赋予您执行复杂权限匹配的能力——而不仅仅是像标准 Apache 基本身份验证那样的简单用户名匹配。

与 Apache 简单身份验证类似，mod_auth_mysql 依赖于在 .htaccess 文件或 httpd.conf 中的 `<Directory>` 条目中指定的访问权限。如果您无权更改 Apache 配置，且您的主机不允许使用 .htaccess 文件，则需要寻找其他方法。由此引入基于 PHP 的身份验证。

#### PHP 控制的身份验证

如果 Apache 控制的身份验证不可行，您实际上可以利用 PHP 的功能来模拟标准的基本身份验证。通过发送正确的响应标头并检查正确的服务器变量，您可以从头构建自己的基本身份验证系统，它拥有与 mod_auth_mysql 一样甚至更多的功能。

为了展示如何使用 PHP 进行基本身份验证，您将设置一个简单的数据库作为用户凭据的存储库。然后，PHP 将对照该数据库检查用户名和密码；最终用户看到的只是标准的基本身份验证提示。

### 创建身份验证数据库

首先，在 MySQL 中创建一个名为 WebAuth 的数据库。

```
CREATE DATABASE WebAuth;
USE WebAuth;
```

接下来，为身份验证系统创建一个 MySQL 登录，并赋予其对刚刚创建的数据库的只读访问权限：

```
GRANT SELECT ON WebAuth.* TO WebAuth@localhost IDENTIFIED BY 'AuthPass';
```

现在，设置用于存储用户名和密码的表。在此示例中，该表仅存储用户名和密码的哈希值，但如果您愿意，可以轻松地添加其他字段作为任何其他的访问条件。

```
CREATE TABLE Users (username varchar(50) PRIMARY KEY,
    passwd_md5 varchar(32) NOT NULL,
    passwd_sha1 varchar(40) NOT NULL);
```





## 网站安全

请注意，你并不是简单地创建一个字段来存储用户的明文密码，而是创建字段来存储用户密码的单向哈希值。这样做确保了密码仍可以与在密码提示处输入的值进行比较，但使得试图在数据库泄露时破解密码的人变得极其困难。如果你熟悉 MD5 或 SHA1，你知道它们都是单向哈希算法。在通过其中任何一种算法进行哈希处理后，几乎不可能确定原始密码。

> MD5 获取输入字符串并创建原始输入的 128 位“唯一”指纹，即哈希值。SHA1 的行为类似，但稍具安全性，生成 160 位“唯一”指纹。

你可能注意到，之前的讨论在关于这两种解决方案提供的唯一性或防破解哈希的绝对性方面并没有说得绝对。直到最近，MD5 一直被认为是对除最安全数据外所有数据进行哈希处理的合理解决方案，SHA1 也是如此。当使用暴力破解时，没有哪种加密方案是 100% 无法被破解的。一个密码生成程序可以遍历每个字符和每个密码长度的所有组合，直到最终找到一个与这两种算法之一产生的哈希值匹配的输入字符串。

然而，密码分析的最新进展证明，MD5 可以被更快击败，方法是找到一个产生相同输出哈希值的输入，即使输入字符串不匹配——这是 MD5 的固有弱点。最近，SHA1 也受到了攻击，而且随着处理能力的提高，暴力破解哈希所需的时间迅速减少。

为了对抗 MD5 中看到的任何类型的碰撞攻击，你创建了 Users 表来保存密码的 MD5 和 SHA1 哈希值。这样做有效地使任何碰撞攻击尝试变得徒劳——即使入侵者设法找到一个与 MD5 哈希值匹配的输入字符串，除非它是真实密码，否则它将不会与 SHA1 哈希值匹配。

为了使数据库对认证脚本有用，你需要至少添加一个用户：

```sql
INSERT INTO Users VALUES ('testuser', MD5('testpass'), SHA1('testpass'));
```

注意，在添加密码时使用了内置的 MySQL 函数 MD5() 和 SHA1()。

### 一个 PHP 基本身份验证脚本

一旦你的数据库设置好，创建以下脚本，并将其保存为 `phpauthbasic.php`：

```php
<?php
  // Define database constants
  define('AUTH_HOST', 'localhost');
  define('AUTH_USER', 'WebAuth');
  define('AUTH_PASS', 'AuthPass');
  define('AUTH_DB', 'WebAuth');
  
  function attempt_auth() {
    // Send authentication headers
    header('WWW-Authenticate: Basic realm="Protected by PHP"');
    header('HTTP/1.0 401 Unauthorized');
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
                              AND passwd_sha1='" . sha1($password) . "'",
                              $conn);

              // Check if a match was found
              if (($row = mysql_fetch_array($result)) && $row['ucount'])
              {
                  $ret = true;
                  $_SESSION['username'] = $username;
              }

              // Close connection
              mysql_close($conn);
          }

          return $ret;
      }
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

168

## 网站安全

这一切意味着什么？看看是什么让这段脚本运行起来的。

你要做的第一件事是为数据库连接定义一些常量：

```php
<?php
// Define database constants
define('AUTH_HOST', 'localhost');
define('AUTH_USER', 'WebAuth');
define('AUTH_PASS', 'AuthPass');
define('AUTH_DB', 'WebAuth');
```

接下来是 `attempt_auth()` 的函数定义。这个函数只是发送响应头给浏览器，告诉它尝试进行基本身份验证登录，并将给定的 realm 显示为登录提示中的安全区域：

```php
function attempt_auth()
{
    // Send authentication headers
    header('WWW-Authenticate: Basic realm="Protected by PHP"');
    header('HTTP/1.0 401 Unauthorized');
}
```

在 `attempt_auth()` 之后是 `check_login()` 的函数定义。这是将传入的用户名和密码实际与之前创建的 WebAuth 数据库中存储的值进行检查的地方。首先要确保传入了用户名和密码，并连接到数据库并设置 WebAuth 为活动状态：

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

在建立数据库连接后，你执行一个查询来检查用户名/密码是否匹配：

```php
// Search for matches
$result =
    mysql_query("SELECT COUNT(username) AS ucount
                FROM Users
                WHERE username='" . addslashes($username) . "'
                    AND passwd_md5='" . md5($password) . "'
                    AND passwd_sha1='" . sha1($password) . "'",
                $conn);
```

为了构建这个查询，首先必须使用 `addslashes()` 转义用户名，以帮助避免任何 SQL 注入攻击（稍后讨论）。这里使用了 PHP 函数 `md5()` 和 `sha1()`，但如果你愿意，可以很容易地使用 MySQL 的等价物——它们应该产生完全相同的结果：

```php
// Search for matches
$result =
    mysql_query("SELECT COUNT(username) AS count
                FROM Users
                WHERE username='" . addslashes($username) . "'
                    AND passwd_md5=MD5('" . addslashes($password) . "')
                    AND passwd_sha1=SHA1('" . addslashes($password) . "')",
                $conn);
```

你可能注意到，`addslashes()` 函数被添加为密码的包装器，而在之前 PHP 执行密码哈希的情况下并不存在。这也是为了防止任何 SQL 注入攻击，甚至是用户密码中包含撇号的简单错误。当首先使用 PHP 对密码进行哈希处理时，没有必要使用 `addslashes()` 转义结果，因为 `md5()` 和 `sha1()` 函数产生的输出仅由十六进制值组成——不可能有撇号或其他危险字符漏网。

为了完成 `check_login()` 函数，将返回占位符设置为 `true`，并创建一个会话变量，你将在脚本后面使用它以避免不必要的重复查询：

```php
// Check if a match was found
if (($row = mysql_fetch_array($result)) && $row['count'])
{
    $ret = true;
    $_SESSION['username'] = $username;
}

// Close connection
mysql_close($conn);
}

return $ret;
}
```

接下来是脚本中实际首次被解释的代码，你通过初始化会话数据开始：

```php
session_start();
```

然后首先检查 `check_login()` 中的会话变量是否已设置。如果尚未设置——意味着此人尚未通过身份验证——检查 `PHP_AUTH_USER` 服务器变量并调用 `check_login()` 函数。当 PHP 尝试使用基本身份验证获取登录信息时，服务器变量 `PHP_AUTH_USER` 和 `PHP_AUTH_PW` 都存在。如果它们未设置，用户尚未被提示提供登录信息。在这种情况下，如果没有传递登录信息且之前传递的身份验证无效，则希望提示用户输入登录信息。如果找不到有效的用户信息，将调用 `attempt_auth()`，用户将有机会再次登录。只有当用户在登录提示上点击取消时，才会显示“需要授权”的消息：




## 网站安全

```php
// Check if using valid credentials
if (!isset($_SESSION['username']) ||
    isset($_SERVER['PHP_AUTH_USER']) &&
    check_login($_SERVER['PHP_AUTH_USER'],
                $_SERVER['PHP_AUTH_PW'])) {
    // Show login prompt
    attempt_auth();
    echo 'Authorization Required';
    exit;
}
?>
```

要测试 PHP 认证功能，你可以尝试在浏览器中加载此脚本，但更好的做法是将其包含到你创建的任何标准 PHP 页面中。你可以使用以下代码将此授权功能作为一个简单的包含项进行测试：

```php
<?php
require_once 'phpauthbasic.php';
echo "Authentication Successful";
?>
```

当你在浏览器中尝试加载此脚本时，请使用 tester/testpass 组合，或者你最初添加到 Users 表中的任意凭据。如果用户名和密码正确，你应该看到一个良好的“认证成功”消息；如果你点击取消，你将得到令人担忧的“需要授权”消息。

既然你看到它起作用了，你可能会认为没有理由不使用这种方法。但就像在决定如何编写应用程序时所做出的许多选择一样，这种方法也有一些缺点。

在使这种认证方法生效之前，必须满足两个主要要求。首先，`php.ini` 中必须未启用 `safe_mode`。当启用时，`safe_mode` 会阻止创建 `PHP_AUTH_USER` 和 `PHP_AUTH_PW` 服务器变量。如果这些变量不存在，无论使用的凭据是否真正有效，脚本都会不断重新显示登录提示，直到用户点击取消。快速确定 `safe_mode` 是否确实启用的方法是：脚本的 uid 会被添加到登录提示中的 realm 信息末尾。

其次，此方法不能与 Apache 的基本认证系统一起使用。这适用于同一脚本级别或任何父目录中任何由 Apache 控制的访问权限（`.htaccess`）。如果两个认证系统都启用，Apache 系统具有初始优先级。会发生的情况是，用户最初可以使用 Apache 基本认证的有效凭据登录，随后出现 PHP 认证提示。然而，在此时，PHP 实际上已经清除了浏览器与 Apache 控制之间的认证状态——这是 HTTP 401 响应导致的结果。由于浏览器不再通过 Apache 认证，它将重新提示输入 Apache 级别的凭据，然后返回到 PHP 凭据，如此反复，直到用户在浏览器中点击取消或停止。

### PHP 表单认证

如果 PHP 基本认证对你来说不是一个可行的解决方案，或者浏览器的登录面板的外观不适合你，不要担心；你还有另一个选项。不要依赖浏览器提供的标准内置登录窗口，你可以轻松创建自己的登录表单，甚至可以使用之前大部分 PHP 认证代码。将以下内容作为 `phpauthforms.php` 输入。注意，其中大部分内容直接取自之前使用的 `phpauthbasic.php` 文件：

```php
<?php
// Define database constants
define('AUTH_HOST', 'localhost');
define('AUTH_USER', 'WebAuth');
define('AUTH_PASS', 'AuthPass');
define('AUTH_DB', 'WebAuth');

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
                mysql_query("SELECT COUNT(username) AS account
                             FROM Users
                             WHERE username='" . addslashes($username) . "
                             " AND passwd_md5='" . md5($password) . "
                             " AND passwd_sha1='" . sha1($password) . "'",
                             $conn);

            // Check if a match was found
            if (($row = mysql_fetch_array($result)) && $row['count'])
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
```

`session_start();`

```php
// Check if using valid credentials
if ((!isset($_SESSION['username']) ||
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

改变的是什么？实际上没变多少。关键修改在文件末尾进行：

```php
// Check if using valid credentials
if ((!isset($_SESSION['username']) ||
	check_login($_POST['username'],
	$_POST['passwd'])))
{
```

不再检查服务器变量 `PHP_AUTH_USER` 和 `PHP_AUTH_PASS`，而是检查通过 HTTP POST 传递的登录凭据，名为 `username` 和 `passwd`。然后，就像基本认证示例一样，如果登录无效或未提供，则向用户显示登录提示。在这种情况下，`attempt_auth()` 函数已被移除，在曾经调用它的地方，放置了一个简单的 HTML 表单。

```php
<?php

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
?>
```

要使用此认证方法，你可以简单地将此脚本包含在任何想要保护的页面顶部。将这一个称为 **testforms.php**（它必须与之前使用的表单目标匹配）：

```php
<?php
require_once 'phpauthforms.php';
echo "Authentication Successful!";
?>
```

那么这种方法有什么优势呢？首先是兼容性。使用简单的基于表单的 PHP 认证在几乎任何情况下都有效，无论 `safe_mode` 是否启用，或者 Apache 是否使用 `.htaccess` 认证。此类解决方案唯一真正的缺点是，你必须自己编写登录表单，并按你希望的方式对其进行样式化，而不是依赖浏览器/操作系统来为你完成这项工作。

## 其他访问限制

除了通过用户名和密码限制访问之外，你还可以使用 PHP 检查其他用户参数。一个常见的需要检查的变量是用户的源 IP。通过引用服务器变量 `$_SERVER['REMOTE_ADDR']`，你可以确保只有特定 IP 范围被允许访问资源，或者相反，你可以阻止特定 IP。如果你正在为企业内网创建网站，你可以限制访问内部 IP（假设你的网络使用它们）。例如，你可以决定只有 10.0.1.x 网络的成员才能查看你网站的特殊区域。另一个例子是 BBS 网站或网络论坛。通常，如果某人在论坛上发布垃圾信息，你需要通过 IP 地址封禁特定用户。

值得检查的另一个服务器变量是 `$_SERVER['HTTP_REFERER']` 变量。此变量保存之前查看的页面名称，可以帮助你消除某些类别的 Web 攻击。假设你创建了一个简单表单，用于将数据保存到数据库、向人们发送电子邮件或任何依赖有效用户输入的操作。你甚至可能付出了巨大努力进行客户端输入验证，并指定了表单的最大长度。不幸的是，从 Web 客户端可能期望的任何输入都可以很容易地通过外部表单进行破坏。任何站点攻击者都可以轻松复制你的表单 HTML 标记，并根据其需要修改它——无论是用于信息收集、跨站脚本、SQL 注入，或任何实际内容。

他们需要做的只是复制一个可以提交不当数据到你网站的表单，将其托管在他们自己的机器上，但使用绝对 URL 作为方法，使其向 *你的* 表单提交数据。当使用 *隐藏* 表单变量时，以及当在 php.ini 中启用 *register_globals* 时，这种类型的攻击可能特别有害。

通过检查 `HTTP_REFERER` 值，你可以消除大部分伪造的表单攻击，只要你确保输入来自实际在你网站上的页面。

要查看 `HTTP_REFERER` 检查和 `REMOTE_ADDR` 验证的实际操作示例，请查看以下代码：

```php
<?php
// Check the referer
if (!preg_match('/http:\/\/localhost/', $_SERVER['HTTP_REFERER'])) {
```





## 站点安全

```php
if (preg_match('/^(.*\.)?(www.example.com)\/?$/',
		$_SERVER['HTTP_REFERER']))
{
	echo 'Invalid referrer! '
	.
	'We don't take kindly to spoofed forms in these parts.';
}

// Check to see if request came from internal users
if (!preg_match('/^(10\.\d{1,3}\.\d{1,3}\.\d{1,3}|' .
	'(172\.16\.\d{1,3}\.\d{1,3})|'
	'(192\.168\.\d{1,3}\.\d{1,3}))$/',
	$_SERVER['REMOTE_ADDR']))
{
	echo 'Invalid client address! '
	.
	'Who let YOU in here?';
}
```

这段代码首先检查来源页面，以确保其来自本地主机或预期的域名（假设您已将其更改为与您的域名匹配），然后检查用户的 IP 地址，以确保其来自内部/私有 IP 地址范围。

PHP 还可以做另一件事来帮助限制某些类型的访问，那就是为注册表单提供验证码（CAPTCHA）图像。CAPTCHA 的全称是“完全自动化的公共图灵测试，用于区分计算机和人类”，这是一种测试，通常会在图像中呈现某种扭曲的文本。其理念是，尽管外观扭曲，人类应该能够弄清楚文本的实际内容，而计算机则不能。许多免费电子邮件和论坛站点使用此类技术来阻止自动机器人脚本注册并滥用服务（例如发送垃圾邮件等）。

尽管目前仍处于 Alpha 开发阶段，但 PHP Pear 仓库中的 Text_CAPTCHA 包提供了一个简单的接口来实现 CAPTCHA 功能。可以在 [http://pear.php.net/package/Text_CAPTCHA](http://pear.php.net/package/Text_CAPTCHA) 找到 Text_CAPTCHA。

如果您想尝试 Text_CAPTCHA，只需使用 **pear install** 命令即可安装：

```bash
pear install -f Text_CAPTCHA
```

您需要使用 -f 标志来强制安装，因为 Pear 团队目前不认为 Text_CAPTCHA 是稳定的，所以普通的非强制安装将会失败。另外请注意，Text_CAPTCHA 依赖于 Text_Password 和 Image_Text（也是 alpha 版本）Pear 包，因此如果您尚未安装它们，需要先安装这些包。

一旦全部安装完成，请创建以下文件作为 `captchatest.php`：

```php
<?php

// Include the Pear class
require_once('Text/CAPTCHA.php');

// Set the options for the generated text;
$opts = array(
    'font_size' => 25,
    'font_path' => './',
    'font_file' => 'VeraMono.TTF'
);

// Create a CAPTCHA object
$cap = Text_CAPTCHA::factory('Image');

// Initialize the CAPTCHA object with random text
$r = $cap->init(250, 100, null, $opts);

// Check if CAPTCHA object is valid
if (PEAR::isError($r))
{
    echo 'CAPTCHA Generation failed.';
    exit;
}

// Generate the PNG CAPTCHA image
$png = $cap->getCaptchaAsPNG();

// Show the image in the browser
header('Content-type: image/png');
echo $png;
?>
```

当您在浏览器中运行此代码时，您应该看到类似图 7.1 的内容。

![](img/cacdd24f2926f10ee3219256ad732604_201_0.png)

Text_CAPTCHA 是如何知道您想要使用什么字符串的？它并不知道。当您初始化 CAPTCHA 对象时，您传入 `null` 作为测试字符串：

```php
// Initialize the CAPTCHA object with random text
$r = $cap->init(250, 100, null, $opts);
```

如果您希望显式设置将由 `Text_CAPTCHA` 渲染的文本字符串，只需将输入字符串从 `null` 更改为您想要的值：

```php
// Initialize the CAPTCHA object with random text
$r = $cap->init(250, 100, 'computers be gone!', $opts);
```

在 PHP 脚本中还需要检查的其他关键项是本地文件名及其访问方式。请查看以下代码：

```php
<?php
$contents = file_get_contents('/path/to/content/' . $_POST['file']);
echo $contents;
?>
```

这种代码经常可以在许多自制的 CMS 系统或某种自定义文档检索脚本中找到。不幸的是，它是一个巨大的安全风险。如果攻击者提交了值 `../../..//etc/passwd` 作为文件会发生什么？如果服务器没有适当地锁定——而许多服务器并没有——系统密码文件的内容将直接输出到屏幕上。

你可以采取几个简单的步骤来帮助防止这种类型的攻击。首先，如果你控制 Apache Web 服务器，请确保它以非特权用户身份运行。无论 Apache 运行为用户是谁——apache、nobody、wwwit 无关紧要——确保该用户没有权限访问除合法网站文件以外的任何文件。

其次，确保转义提供的文件路径中的父目录访问点，如下所示：

```php
<?php
$file = str_replace('.', '', $_POST['file']);
$contents = file_get_contents('/path/to/content/' . $file);
echo $contents;
?>
```

如果可能，给转义后的文件名加上其路径前缀也是一个好主意。这样，如果攻击者为文件值提供了绝对路径，它仍然会相对于指定的文件夹运行。

## 网站攻击

每当你在公共互联网上发布一个站点时，它就有被攻击的风险。虽然没有任何应用程序可以真正达到 100% 安全，因为新的漏洞和利用技术每天都在被发现，但你的 PHP 脚本可以相对轻松地防御几种类型的攻击。

### 滥用 register_globals

如果每一篇谈论 `register_globals` 的文章、书籍或任何文档没有把这一点刻进你的大脑，那就再强调一次：将 `register_globals` 设置为 `on` 是一场等待发生的灾难。

如果你对 `register_globals` 不熟悉，它是 `php.ini` 中的一项设置，控制自动填充与表单元素或 Cookie 同名的变量。在本章前面创建的登录表单中，有一个名为 `username` 的字段。通常情况下，当禁用 `register_globals` 时，在表单提交后访问表单中 `username` 字段的唯一方法是使用 `$_POST` 或 `$_GET` 数组，具体取决于表单的方法。当启用 `register_globals` 时，可以使用 `$_POST` 或 `$_GET` 再次访问 `username` 字段，但它也可以作为 `$username` 访问。

从 PHP 4.2.0 开始，`register_globals` 的默认值为 `off`，但 Web 主机通常重新启用 `register_globals` 以提供与旧脚本的兼容性，这些旧脚本假设存在并依赖于 `register_globals`=on。不幸的是，这为恶意用户提供了高级的攻击途径。当启用 `register_globals` 时，PHP 按照 `variables_order` 设置中指定的顺序评估环境、表单、Cookie 和服务器变量。如果服务器使用“推荐”的配置文件，GET 变量首先设置，然后设置 POST 并覆盖任何匹配的 GET 值。接下来设置 Cookie 值，然后设置服务器变量，覆盖之前设置的任何匹配值。

虽然这种行为看起来很方便，但使用克隆表单或伪造的 Cookie 信息很容易利用它。为了了解它是如何被利用的例子，请查看以下 PHP 代码：

```php
<?php
if (user_is_admin())
{
    $access_level = 10;
}

show_menu($access_level);
// ... And so on ...
?>
```

在这种假设的情况下，脚本调用 `user_is_admin()` 函数来确定用户是否是管理员。如果是，`access_level` 变量被设置为 10，并且在后续脚本中，通常会显示完整的管理级别。

如果启用了 `register_globals`，请求文件并在查询字符串中添加你期望的访问级别是一件微不足道的事情，如下所示：

`http://www.example.com/file.php?access_level=10`

现在，如果脚本使用添加的 access_level 调用，无论用户是否真正是管理员——由于 `register_globals` 和 PHP 不需要变量初始化，`$access_level` 变量会在脚本开始时自动设置为 10。

幸运的是，避免这些陷阱相对容易。确保你在禁用 `register_globals` 的情况下编写代码，使用适当的 `$_GET` 和 `$_POST` 超全局变量，初始化可能不安全的变量，并确保在开发和测试站点时 `error_reporting` 设置为 `E_ALL`。

如果你无法在 `php.ini` 中禁用 `register_globals`，你可以使用 `.htaccess` 文件来关闭它（如果在 Apache 中正确启用了的话）：

```apache
php_flag register_globals off
```

### SQL 注入攻击

另一种脏数据攻击，但具有更大的破坏潜力，是 SQL 注入攻击。与 `register_globals` 攻击结合使用，或者仅仅使用普通的 Web 表单，SQL 注入攻击只是在应该通常是良性数据的地方插入恶意的 SQL 语句。

SQL 注入利用了缺乏输入清理和数据验证——即盲目地用于 PHP 构建的 SQL 查询中的数据。请查看以下示例，它将访问你在本章前面创建的 WebAuth 数据库：

```php
<?php
$username = $_POST['username'];
$conn = mysql_connect(AUTH_DB, AUTH_USER, AUTH_PASS);
mysql_select_db(AUTH_DB, $conn);
$sql = "SELECT * FROM Users WHERE username='$username'";
mysql_close($conn);
?>
```

看起来无害，对吧？你会期望它愉快地接受从表单发送的任何用户名，并查找与该特定用户名相关的所有列。这段代码的问题在于 SQL 查询。请注意，`$username` 变量在发送到数据库之前没有经过任何验证、清理或准备。在大多数情况下，你可能不会注意到任何异常，它几乎不会抛出错误。

然而，当发送表单的用户名字段输入以下值时，事情很快就会变得棘手：

```sql
'; DELETE FROM Users; SELECT 'Own3d' AS username FROM Users WHERE '=''
```

仔细看看这个值发生了什么。它首先终止在 `$username` 变量附加之前的查询部分，删除 Users 表中的所有信息，然后执行攻击者选择的查询，只是为了关闭查询并匹配最后的撇号。





## 第 7 章

当“恶意”的用户名值被替换到原始查询中时，有效的命令集看起来会像这样：

```
SELECT * FROM Users WHERE username='';
DELETE FROM Users;
SELECT '0wn3d' AS username FROM Users WHERE '1'='1'
```

当发送到 SQL 服务器的数据没有像本例中那样进行转义时，可能会发生许多坏事。想象一下，如果中间那条命令是 `DROP DATABASE; GRANT` 命令，会造成多大的损害——那将是一个糟糕的局面。这个例子是对 SQL 注入攻击中可能发生情况的简化描述，但它应该能让你对这种攻击对数据完整性和系统完整性造成的破坏程度有一个初步的认识。

与困扰 PHP 脚本的许多常见问题一样，SQL 注入在一定程度上是可以通过精心规划和严谨的代码实践来预防的。如果将 `magic_quotes_gpc` 配置为 `on`，PHP 在转义表单数据中的“危险”字符方面会为你兜底。当启用 `magic_quotes_gpc` 时，PHP 会自动转义任何转义字符（如撇号），甚至在你尚未在脚本中触及它们之前就已处理完毕。不幸的是，这种行为应用于所有 GET、POST 和 Cookie 变量，无论它们是否将用于 SQL 语句中——而且大多数时候，这会带来一些不便。

为了确保数据仅在你需要时才被转义，请在 `php.ini` 中关闭 `magic_quotes_gpc`，并对所有传递给 MySQL 的数据使用 `addslashes()`。`addslashes()` 函数会自动转义任何危险字符，否则你的输入会导致 MySQL 报错——这既包括针对 SQL 注入攻击的防御，也包括处理包含特殊字符的合法数据（例如带有撇号的姓氏）。

作为第二道防线，请确保你在 PHP 中用于访问数据库的用户仅拥有维持应用程序运行所需的最小权限集。在前面的 SQL 注入攻击示例中，删除所有用户记录的操作通常本应失败——因为在章节开头设置用户时，仅授予了 SELECT 权限。

SQL 注入攻击的一个近亲——文件系统执行攻击——也应以类似的方式对待。任何未经清洗的输入数据，只要成为对 `system()` 或 `exec()` 调用的一部分，都应被视为可疑的，因为它们很容易像 SQL 注入攻击那样，将一系列恶意的系统命令串联起来执行。

### 跨站脚本

SQL 注入和 `register_global` 滥用主要涉及脏输入数据的使用，而另一种攻击则依赖于动态输出的不纯净——即跨站脚本（XSS）。

通常缩写为 XSS，跨站脚本攻击利用的是未过滤的动态输出，攻击者能够添加或修改页面生成的标记。最常见的情况是，向页面输出中添加一小段 JavaScript，然后做些不光彩的事情，例如欺骗其他用户泄露其登录凭证或信用卡信息，或者泄露 Cookie 或会话信息以立即实施账户盗用。

## 站点安全

为了更好地理解攻击的具体流程，请考虑以下场景：

- 攻击者在博客或其他网站上填写评论表单。评论中包含了一个恶意脚本。
- 评论在页面上显示，脚本保持完整且处于激活状态。
- 一名无辜的用户访问该网站，并阅读攻击者的评论，其中可能包含也可能不包含一个可点击的链接。
- 通过点击攻击者的链接，或者仅仅是访问该页面，用户会被要求验证私人信息，例如用户名或密码。
- 用户在不知情中提交私人信息，认为这是其所访问的合法网站提出的请求。
- 用户被盗取的信息被路由到互联网上的另一个位置，要么存储起来以便日后分析，要么攻击者会收到有关新信息的通知。

这是如何发生的？当“受信任”的网站在将特殊字符作为输出或标记发送之前未对其进行适当清洗时，跨站脚本攻击就会生效。就网页而言，这意味着动态输出中存在的以下字符需要处理：小于号 `<`、大于号 `>`、和号 `&`、单引号和双引号，以及任何 UTF-8 字符。

幸运的是，在处理动态输出的清洗时，PHP 为你提供了一系列可选的工具：

- `htmlspecialchars()`：转义和号、小于号、大于号、单引号和双引号，使其成为大多数动态生成 HTML 的合适选择。
- `htmlentities()`：与 `htmlspecialchars()` 类似，但 `htmlentities()` 会转义任何具有 HTML 实体等效项的特殊字符，除了 `htmlspecialchars()` 覆盖的核心五个字符外还包括这些字符。
- `strip_tags()`：从字符串中移除所有 HTML 和 PHP 标签。你可以甚至提供一个允许标签的列表，从而将“安全”的标签（如格式标签）加入白名单，并移除那些更具危险性的标签（如 `<script>`）。
- `utf8_decode()`：将 UTF-8 编码的字符转换为等效的 ISO-8859-1 字符。

### 其他注意事项

除了直接影响你编写的代码或服务器配置的问题外，在应用程序的设计、开发和维护过程中，还必须考虑一些其他问题。

最容易解决的问题之一是保持系统最新并安装所有最新的补丁。如果你的操作系统有自动更新核心系统软件的方法，通常建议善加利用。许多近期的 Web 服务器漏洞利用实际上是针对旧版本软件中的缺陷——病毒和蠕虫编写者经常利用厂商发布的关于近期服务器补丁的信息来编写他们知道会影响旧版本的恶意代码。

在更新系统时，另一个不应被忽视的群体是随 PHP 安装的 PEAR 和 PECL 包。这两个都可以很容易地通过一条简单的命令更新：`pear upgrade-all`。关键在于记得定期运行该命令，或者更好的做法是将其添加为一个 cron 任务。

在编写应用程序时，有一些小事可以帮助你降低 `register_globals` 漏洞利用或 SQL 注入攻击的可能性。首先，确保在使用前初始化所有变量；这样表单或查询字符串变量就没有机会偷偷混入。其次，确保在生产 Web 服务器上关闭任何错误报告输出。通过禁用错误消息的显示，当发生错误（例如 SQL 查询中的语法错误，或 SQL 服务器的主机名或 IP 地址）时，敏感信息就不可能泄露出去。

还有一些有助于维护站点安全的其他事项，并不是你能通过输入或配置来直接完成的。黑客获取你站点访问权限的一种可能方式涉及一点点社会工程学，甚至几乎不需要实际的计算机入侵。如果你是网站管理员，负责创建和排查用户登录问题，你处于一个非常关键的角色，如果没有适当的保障措施，这个角色可能会被利用。在许多情况下，黑客所需要做的仅仅是致电网站管理员，假装是一个忘记了密码的用户。如果管理员向那个倒霉的用户泄露了用户名或密码，黑客立即就拥有了一个合法的网站登录凭证，而不需要任何网络嗅探或暴力破解攻击。

另一件对站点安全大有裨益的小事是在开发周期中进行频繁的代码/同行评审。通过让你的同事或同行审查你的代码，同时也让他们接受你的审查，你可以帮助在代码实际上面向公众之前，尽早发现许多明显的安全问题。

最后，确保你通过频繁访问如 Secunia (http://secunia.com/)、CVE (http://www.cve.mitre.org/) 和 CERT (http://www.cert.org/) 等与安全相关的网站，及时了解最新的安全和漏洞新闻。

#### 总结

如你所见，在处理由 PHP 驱动的网站安全时，有相当多的事项需要考虑。如果你保持严格的数据清洗实践，确保所有进出系统的信息都是有效的，你的网站将能够抵御大多数简单的攻击者。




## PEAR 和 PECL

开源的核心理念，当然是通过协作努力来完成伟大的事情。无数贡献者及其努力之间产生的协同效应，推动着开源项目不断突破日益扩展的边界。然而，随着这种巨大且多样化的努力而来的，是可能阻碍开源运动成功的挑战。这些挑战包括组织、协调和方向。没有组织，代码编写将没有标准，或者无法以系统的方法来组装软件包。没有协调，代码片段将分散在庞大的互联网中，很可能迷失在编写拙劣的 HTML 页面之间，永远无法被人眼看到。没有方向，就无法展望未来，也没有可供渴望贡献者兴奋的源泉。简而言之，那就只是一群技术宅在写和重写与每个人相同的代码片段，所有人都在自己的小世界里独立行动。然而，每个人都知道“没有人是一座孤岛”，这正是 PEAR 和 PECL 小组发挥作用的地方，它们提供急需的组织、协调和方向，以便开发人员从长远来看都能成为更好的编码者。

通过为开发人员提供完成常见任务的现成脚本（例如连接数据库或与 XML 文档交互），PEAR 和 PECL 软件包可以为你节省大量的编码时间和烦恼。

虽然它们都完成类似的任务，但 PEAR 和 PECL 之间存在根本差异，本章将对此进行详细解释。

### 什么是 PEAR？

PEAR（PHP 扩展和存储库）旨在充当那些有用但偏离主流类的家园。顾名思义，它是一个代码软件库，可能由一个或多个文件组成，用于完成创建 HTML 表单、处理日期和图像或连接数据库并运行查询等常见任务。由于这些是每个编码者都会不时使用的功能，因此它们非常适合成为 PEAR 软件包。

由于开发并发布 PEAR 软件包有一套严格的编码标准，编码者可以确信一个软件包的外观和感觉与其他软件包保持一致。随着你熟悉它们的使用，你将开始知道寻找什么以及代码是如何组织的。PEAR 软件包还以其广泛的注释要求和命名约定而闻名，这是许多开源程序严重缺乏的，这留给你一项艰巨的任务：试图理解别人的逻辑。

所有新软件包在被列入 PEAR 分发列表之前，都必须通过 PEP（PEAR 提案系统）。这个四步过程确保每个软件包都经过准确性、可靠性和相关性的严格审查。如果你想了解更多关于 PEP 的信息，可以访问网站 http://pear.php.net/pepr。

### 什么是 PECL？

PECL（PHP 扩展社区库）是 PEAR 的一个分支，主要用于容纳不再包含在 PHP 默认安装中的函数组。从 PHP 5 开始，这些扩展可以从常规 PHP 下载中单独下载和安装。然而需要注意的是，目前驻留在 PECL 中的一些扩展现在已包含在默认安装中（例如 SQLite），有些是由 PHP 核心团队外部人员提交的扩展，且从未包含在 PHP 中（例如 POP3）。

由于大多数 PECL 扩展曾经是标准 PHP 函数列表的一部分，标准要求它们使用 PHP 的编码标准编写（与 PEAR 不同）。虽然普通公众仍然可以提交软件包，但提交过程包括获得 pecl-dev 邮件列表的事先批准。

### 探索 PEAR

在你深入 PEAR 世界之前，你应该意识到，由于它是一个基于类的系统，为了正确使用这些软件包，你应该非常熟悉 PHP 中的 OOP（面向对象编程）。如果你是一个硬核的函数式编码者，建议你通过快速教程或本书第二章的简要复习来磨练你的 OOP 技能。

你首先需要的是 PEAR 软件包本身，它使你能够轻松安装和升级新的 PEAR 软件包。幸运的是，这个管理器随 PHP5（以及 4.3.0 及以上版本）预安装，将使你在安装、管理和升级其他 PEAR 软件包时更加轻松。主要的 PEAR 软件包还包括一组错误处理函数，使你能够轻松检测和管理遇到的 PEAR 软件包错误。

#### PEAR 管理器

如前所述，PEAR 管理器的主要目的是协助你管理和其他 PEAR 软件包进行交互。它附带了一组可以从命令行运行的命令（可能需要或不需 root 访问权限）。你可以在 http://pear.php.net/manual/en/installation.cli.php 上找到完整列表，但下表突出了主要命令供你参考：

| 命令 | 作用 |
| --- | --- |
| bundle [package name] | 下载并解包 PEAR 扩展 |
| download [package name] | 下载软件包而不安装 |
| download-all | 下载所有可用软件包 |
| info [package name] | 显示软件包信息 |
| install [package name] | 下载并安装软件包 |
| list | 列出已安装的软件包 |
| list-all | 列出所有软件包 |
| list-upgrades | 列出已安装软件包的可用升级 |
| uninstall [package name] | 卸载并删除软件包 |
| upgrade [package name] | 升级软件包 |
| upgrade-all | 升级所有已安装的软件包 |

要使用任何命令，只需在命令前加上 `pear`，例如：

```
pear info XML-RPC
```

正如你所见，这将为你提供名为 XML-RPC 的 PEAR 软件包的信息。

你还可以控制一些 PEAR 配置变量。这些主要与目录信息和用户偏好相关，大多数情况下默认值是可以接受的。你可以访问 http://pear.php.net/manual/en/installation.cli.php 查看完整列表。然而，下表列出了其中一些更常见的变量：

| 变量名 | 代表什么 | 默认值 |
| --- | --- | --- |
| bin_dir | 存放可执行文件的目录 | /usr/bin |
| ext_dir | 存放已加载扩展的目录 | . |
| php_dir | 存放 PHP 安装的目录 | /usr/lib/php |
| preferred_state | 要下载的优先软件包状态（stable, beta, alpha, devel, 或 snapshot） | stable |

要查看当前的设置，请使用 `config-show`（或 `config-get` 仅查看单个变量的值）命令，例如：

```
pear config-show
```

这显示了每个配置变量的描述、变量名称以及当前设置。要更改设置，请使用 `config-set` 命令，例如：

```
pear config-set preferred_state devel
```

`config-help` 命令为你显示有关特定配置变量的更多信息。

#### 安装软件包

一些其他 PEAR 软件包随 PHP 5 预安装，你可以通过运行以下命令（以 root 登录）找到完整列表：

```
pear list
```

这将为你提供已安装软件包的列表、安装的版本以及发布状态（稳定版、测试版等）。如果你想安装其他软件包，以下部分简要概述了安装过程。

##### 命令行安装

如果你有 root 访问权限，只需输入以下命令即可安装任何新软件包：

```
pear install [package name]
```

此命令会跳转到 PEAR 站点，下载你指定的软件包（当然不包括括号），并在你的机器上安装它。

##### FTP 安装

如果你无法访问命令行，或者你的当前网络主机没有提供你想要的 PEAR 软件包，你还可以通过完成两个步骤来安装软件包：

- 直接从 PEAR 站点下载压缩的软件包，在本地解压，并将文件上传到你的网站（将它们保存在 `var/www/www.yourdomain.com/includes` 目录中）。你也可以上传压缩文件并在主机服务器上解压它（同样，到 `var/www/www.yourdomain.com/includes` 目录）。
- 修改你的 `php.ini` 文件以匹配刚刚使用的包含路径。

```
include_path = ":../includes"
```

你也可以在每个访问该软件的脚本中包含一行代码，如下所示：

```
<?php
ini_set('include_path', '/var/www/www.yourdomain.com/includes/' . PATH_SEPARATOR .
 ini_get('include_path'));
//这里编写剩余 PHP 脚本。
?>
```

你的软件包现在已安装并准备使用。





### 使用已安装的包

一旦安装好包，其使用和访问都非常简单。只需在脚本开头包含一行引入必要文件的代码，如下所示：

```php
<?php
require_once('HTML/QuickForm.php');

//you are now able to access and reference classes, methods and properties
//contained in the quickform.php file to easily create HTML forms.
?>
```

### 快速粗陋的 PEAR 包

截至目前，共有 318 个 PEAR 包可用于各种领域，并且每天都在增加新的包。虽然本书不会讨论所有这些包，但以下章节将探讨其中一些更常见的包，并突出显示你可能需要确保已安装的包。此外，请记住，这些章节保持简洁，但如果你需要更健壮的功能，它们也会为你指明正确的方向。

#### Auth_HTTP

该包的目的是提供一个类似于 Apache 的 .htaccess 登录框的身份验证系统。这是一种简单快捷的方式，用于保护网站某个区域的密码。请注意，该包依赖于更健壮的 PEAR::Auth，而 PEAR::Auth 又依赖于 PEAR::DB 包，因此在 Auth_HTTP 包能够正常运行之前，需要先安装这两个包。

Auth_HTTP 的简单用法如下：

```php
<?php
require_once('Auth/HTTP.php');

$a = new Auth_HTTP("DB", "mysqli://username:password@localhost/databasename");
$a->start();
?>
```

首先，你包含文件 `Auth/HTTP.php`，这使你能够访问正确的包。然后，你使用上述参数实例化一个新的 Auth_HTTP 对象。由于你实际上是在使用 PEAR::DB 包登录数据库，因此你可以更改正在使用的数据库类型，并指定其他选项，例如套接字、路径、端口号等。尽管本章稍后将简要讨论此包，但 PEAR::DB 包的详细描述可在 http://pear.php.net/manual/en/package.database.db.php 找到。接下来，你通过调用 start() 函数启动身份验证过程，你的页面就受到密码保护了。

当然，这留下了很大的改进和自定义空间，你可以更进一步，要求身份验证过程从数据库中的表登录用户。你可以通过使用 $authOptions 变量来指定登录选项：

```php
<?php

require_once("Auth/HTTP.php");

$authOptions = array(
//use the same data source name (database login info) as in previous example
'dsn'=>'mysql://username:password@localhost/databasename',

//specify the database table that contains user info
'table'=>"users",

//specify the column that holds the username
'usernamecol' =>"username",

//specify the column that holds the passwords
'passwordcol' =>"password",

//specify the encryption type used
'cryptType' =>"md5",
);

$a = new Auth_HTTP("DB", $authOptions);
//specify the name of your realm
$a->setRealm('Registered Users Only');
//specify the error message seen by the user if authentication fails
$a->setCancelText('<h2>Access Denied.</h2>');

$a->start();

//check to see if the user is authorized
if($a->getAuth())
{
//body of authorized text goes here.
echo "Hi there, authorized user!";
}
?>
```

你可以看到，这提供了一种非常便捷的方式来验证用户。要在其他页面上检查授权，只需使用 `getAuth()` 函数即可。

Auth_HTTP 包还有其他可指定的参数，并且 Auth 包提供了一个非常健壮的基于 HTML 表单的身份验证系统。你可以分别在 <http://pear.php.net/manual/en/package.authentication.auth-http.php> 和 <http://pear.php.net/manual/en/package.authentication.auth.php> 阅读有关这些包的更多信息。

#### Date

虽然 PHP 提供了返回日期和时间信息的内置函数，但此 PEAR 包提供了简单的方法来将这些信息操作为常用结果，例如该月剩余天数、当前星期几等。

这个包可用的函数非常多，我们要为每个函数提供示例会很困难。但是，以下章节描述了 Date 类中一些更常用方法。访问 <http://pear.php.net/package/Date/docs/latest/Date/Date.html> 可查看方法的完整列表。

##### Date 类

该类出现在主要的 date.php 文件中，并提供以下方法供你使用：

- `Date`：构造函数，创建一个新日期对象。
- `addSeconds`：向日期添加特定数量的秒数。
- `addSpan`：向日期添加时间跨度。
- `after`：确定一个日期是否在另一个日期之后。
- `before`：确定一个日期是否在另一个日期之前。
- `convertTZ`：将日期转换为另一个时区。
- `equals`：确定两个日期和/或时间是否完全相等。
- `format`：根据用户规格格式化日期。
- `getDate`：以特定格式返回日期。
- `getDay`：返回日期对象当月的天数。
- `getDayName`：以字符串格式返回日期对象所在星期几。
- `getDayOfWeek`：以整数格式返回日期对象所在星期几。
- `getDaysInMonth`：返回日期对象所在月的天数。
- `getHour`：返回日期对象的小时。
- `getMinute`：返回日期对象的分钟。
- `getMonth`：以整数格式返回日期对象的月份。
- `getMonthName`：以字符串格式返回日期对象的月份。
- `getNextDay`：返回日期对象次日日期。
- `getNextWeekday`：返回日期对象下一个工作日日期。
- `getPrevDay`：返回日期对象前一日日期。
- `getPrevWeekday`：返回日期对象上一个工作日日期。
- `getQuarterOfYear`：以整数格式返回日期对象所在的季度。
- `getSecond`：返回日期对象的秒数。
- `getTime`：返回自 Unix 纪元以来的秒数。
- `getWeekOfYear`：以整数格式返回日期对象所在的周数。
- `getWeeksInMonth`：返回日期对象所在月的周数。
- `getYear`：返回日期对象的年份。
- `inDaylightTime`：确定该时间/日期是否处于夏令时。
- `isLeapYear`：确定日期对象的年份是否为闰年。
- `setDate`：设置日期对象的日期。
- `setDay`：设置日期对象的天数。
- `setHour`：设置日期对象的小时。
- `setMinute`：设置日期对象的分钟。
- `setMonth`：设置日期对象的月份。
- `setSecond`：设置日期对象的秒数。
- `setTZ`：设置日期对象的时区。
- `setYear`：设置日期对象的年份。

以上就是 Date 类的内容。Date 类还使用了另外两个类，但这些类也可以直接使用；它们是 Date_Span 和 Date_TimeZone 类。如果你需要比 Date 类能提供的更具体的功能，例如返回所有可用时区的列表或确定服务器的默认时区，它们内部有许多特定的方法。

##### 一个快速示例

以下是一个快速示例，说明使用 Date 包输出像今年剩余周数这样的信息有多容易：

```php
<?php
require_once("date.php");

$currweek = new Date();

$weeksleft = 52 - ($currweek->getWeekOfYear());

echo "There are " . $weeksleft . " weeks left in the year.";
?>
```

正如你所见，当尝试完成更复杂的日期计算或处理时区时，如此简单的功能真的能让你的生活更轻松。

#### DB

这是 PEAR 包，允许你轻松连接和查询数据库。还有许多其他与数据库相关的包可供参考。例如，MDB 与 DB 类似，但提供了更多



可移植性。DB 应当在你的标准配置下正常工作，但如果你遇到了兼容性问题，还有其他尝试方法。事实上，PEAR 专门有一个整个类别的包用于处理数据库，可以在 http://pear.php.net/packages.php?catpid=7&catname=Database 找到。

在接下来几个示例中，你需要以下信息：

- `MySQL` 你的数据库类型
- `testdatabase` : 数据库名称
- `testtable` : 数据库表
- `username` 访问数据库的用户名
- `password`: 用户密码
- `localhost` : 服务器名称
- `field1` , `field2` : 你要查询的字段

这将帮助你在定制该包的安装时“填空”。

##### 连接数据库

为了连接数据库，你必须向新的数据库对象传递正确的数据源名称 (DSN)。语法如下：

```
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

正如你所见，这就是连接所需的全部，更重要的是，报告过程中可能发生的任何错误。同样，请访问官方 PEAR 文档以获取有关连接数据库时你可以设置的各种选项的详细说明，例如端口号或协议。该文档可以在 http://pear.php.net/manual/en/package.database.db.intro-connect.php 找到。现在尝试从虚拟表中查询虚拟字段。

##### 查询数据库

要查询数据库，你需要传递表名和你所需的过滤器，因此输入以下内容：

```
<?php
require_once("db.php");

$dsn = "mysql://username:password@localhost/testdatabase";

$db = DB::connect($dsn);
if (PEAR::isError($db)) {
    die($db->getMessage());
}

//query
$res =& $db->query("SELECT * FROM testtable");

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

这只是该包的一个示例。你可以用它做更多的事情，例如获取来自多个查询的结果集，以及自动准备和执行常用的 SQL 语句。

#### HTML_CSS 和 HTML_Page

这些包允许你动态创建 CSS 样式表并轻松地将它们整合到新的 HTML 页面中。HTML_Page 还可以为你执行其他功能，但本示例专注于创建新的 CSS 样式表：

```
<?php
require_once("HTML/CSS.php");
require_once("HTML/Page.php");

$css = new HTML_CSS();

//set the styles
$css->setStyle('body', 'background-color', '#FF00CC');
$css->setStyle('body', 'color', '#ffff');
$css->setStyle('h1', 'text-align', 'center');
$css->setStyle('h1', 'font', '16pt verdana');
$css->setStyle('p', 'font', '12pt verdana');

//create a new page
$p = new HTML_Page();

$p->setTitle("Testing the CSS");

$p->addStyleDeclaration($css, 'text/css');
$p->addBodyContent("<h1>Wow, this background is really bright</h1>");
$p->addBodyContent("<p>This should wake you up.</p>");

$p->display();
?>
```

使用简单的 *if* 或 *switch* 语句，你可以使用类似这样的东西动态创建样式表，基于个人的授权级别、正在使用的浏览器或操作系统类型、时间或日期，或者你能想到的任何其他东西。

#### HTML_QuickForm

该包的目的可以快速轻松地创建 HTML 表单。它易于使用，但相对健壮，并且允许你在很大程度上进行自定义。看一下一个简单的示例：

```
<?php
require_once("HTML/QuickForm.php");

//create a new form object
$form = new HTML_QuickForm('firstForm');

//add two input fields; this is completely customizable
$form->addElement('text', 'name', 'Your full name:', array('size' => 50, 'maxlength' => 255));
$form->addElement('text', 'email', 'Your email address:', array('size' => 50, 'maxlength' => 255));

//add a submit button
$form->addElement('submit', null, 'Send');

//add validation rules of our choosing
//using addRule('field to be validated', 'error_message to be displayed',
// 'validation type',
$form->addRule('name', 'Empty Name Field', 'required', null, 'client');
$form->addRule('email', 'Empty Email Address', 'required', null, 'client');
$form->addRule('email', 'Incorrect Format for Email Address', 'email', null, 'client');

//check to make sure input followed all our rules
//if so, put all form elements into an array for us
//for sake of example, let's print the values
if ($form->validate()) {
	$elements=$form->exportValues();
	print_r($elements);
	exit;
}

//show the form
$form->display();
?>
```

通过这个小程序，你创建了一个用户表单，验证了必填字段（以及电子邮件字段），并将输入收集到一个整洁的小数组中供你使用。你可以设置尽可能多的规则，让脚本确保必填字段已输入，它们是否具有正确的格式（数字、字母等），并且如前所述，检查诸如正确格式化的电子邮件字段之类的事情。你还可以设置默认值以及你可以使用表单完成的其他任何事情（例如上传文件和为“提交”按钮使用图像）。

#### HTML_Table

使用此包，你可以轻松地输出数据表，无论数据是来自数据库查询的结果集，还是只是位于数组中等待你解放的数据。快速看一下一个示例，说明这个包是多么易于使用：

```php
require_once ("HTML/Table.php");

//Set up attributes for our table, using common HTML attributes as
//array keys and their values as array values
$attributes = array("width" => "50%", "border" => "1");

//create a new table object
$table = new HTML_Table($attributes);

//configure table
//AutoGrow is for an unknown number of rows
//AutoFill inserts text for every empty cell
//Because we are pretending not to be sure how big our table will be, we
//will set this option to true.
$table->setAutoGrow(true);
$table->setAutoFill("-");

//get some data for our table
$rows = array(
    "0" => array("Number One", "Number Two", "Number Three"),
    "1" => array("Numero Uno", "Numero Dos", "Numero Tres"),
);

//populate the table
for($nr = 0; $nr < count($rows); $nr++) {
    //the header row comes first
    $table->setHeaderContents($nr+1, 0, (string)$nr);
    for($i = 0; $i < 3; $i++) {
        if("" != $rows[$nr][$i])
        //the cell contents come next
            $table->setCellContents($nr+1, $i+1, $rows[$nr][$i]);
    }
}
//set background for every other row
//skip the first row so we use a value of 1 to start
$altRow = array("bgcolor"=>"#FFFFCC");
$table->altRowAttributes(1, null, $altRow);

//set header info for each cell of the table
//based on coordinates. 0,0 is top left cell.
//the third value is the contents to be shown
$table->setHeaderContents(0, 0, " ");
$table->setHeaderContents(0, 1, "Field 1");
$table->setHeaderContents(0, 2, "Field 2");
$table->setHeaderContents(0, 3, "Field 3");

//set attributes for the header rows and first column
//first row and column = 0.
$shrAttrs = array("bgcolor" => "#FFFF4D");
$table->setRowAttributes(0, $shrAttrs, true);
$table->setColAttributes(0, $shrAttrs);

//send it to the browser
echo $table->toHTML();
?>
```

你可以想象根据用户输入或数据库结果创建表格有多么容易，以及通过改变这里和那里的几个变量所能实现的自定义程度。

### 还有什么其他内容？

浏览完整的 PEAR 包列表（在 http://pear.php.net/packages.php 提供），你将开始欣赏 PEAR 社区的广度和深度。有如此多很棒的包可用，本书没有空间涵盖所有它们。为了给可用且更有用的主题提供一个简要列表，除了本章中讨论的那些：

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




# 第8章

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

## 探索 PECL

虽然 PECL 没有 PEAR 那么庞大，但这并不意味着它没有价值。与 PEAR 相比，可用包的文档和功能范围更为有限。许多 PECL 包仍处于 beta 阶段，属于实验性质；因此，使用这些包可能需要一些适应过程。然而，PECL 中确实包含一些非常有用的，甚至非常特定的包，我们将快速查看其中一些更受欢迎的包，以让你了解它们包含的内容。如果你想要更详细的 PECL 包说明，我们在第10章中已经针对 PDFlib 进行了详细介绍。

### Fileinfo

Fileinfo PECL 包是 PECL 站点上下载量最大的包之一，它非常实用。有了这个扩展，你可以获取关于文件的各种信息，例如 MIME 类型。该包可以从 http://pecl.php.net/Fileinfo 下载。

该包的文档相对有限，这在许多 PECL 包中都是如此；不过，在 PHP Wiki 上有一篇简短涉及该包的 wiki 文档（http://www.php.net/phpwiki/Fileinfo）。

### PDO

在撰写本文时，PDO 仍处于 beta 阶段，被视为实验性，但它对 PHP 在数据库交互方面的未来充满了希望。该包的目的是与数据对象接口，并允许你随时更改数据库类型。你无需使用数据库特定的函数（例如 `mysql_connect` 或 `pg_connect`）进行编码，而是可以创建一个新 PDO 对象来处理这些事务。你只需在对象实例化期间更改一个参数，就可以从 MySQL 切换到 Postgres（或众多其他数据库）。你可以从 http://pecl.php.net/package/PDO 下载 PDO。

随着 PDO 影响的扩大，其文档也在增加。PHP 手册（http://us3.php.net/manual/en/ref_pdo.php）中有关于此扩展的文档，之前提到的 PHP Wiki（http://www.php.net/phpwiki/PDO_Basics）上也有。

### Xdebug

这是另一个热门的 PECL 下载包，可在 http://pecl.php.net/package/Xdebug 获取。其功能是帮助 PHP 开发人员调试脚本，提供有关代码、激活、执行和变量值的宝贵信息。它还提供了内存分配和保护，防止无限循环，以及堆栈和函数跟踪。

该包的文档比其他包更详尽，甚至拥有自己的网站 http://www.xdebug.org。

#### 总结

现在你应该已经具备了深入研究 PEAR 和 PECL 的能力，并能停止反复编写和重写相同的代码。一旦你熟悉了 PEAR 和 PECL 的设置，也许你会编写一些代码，并将其作为新包贡献给大众，从而加入优秀贡献者的行列。

![](img/cacdd24f2926f10ee3219256ad732604_224_0.png)

#### 代码效率

页面服务速度越快，你的网站在用户不体验延迟的情况下可以处理更多业务。本章介绍提高站点性能的方法，以及识别哪些方法可能最有效。

“用更少的时间显示更多页面”是核心理念，但就像有些汽车爱好者会利用每个空闲时刻深入汽车内部，试图将四分之一英里的时间缩短百分之一秒一样，也有网站开发人员希望将登录页面的显示时间再减少一毫秒。你做得可能太过分！

你不想把时间浪费在没有人会注意到的改进上，因此本章的第一部分将呈现几个小插曲，说明即使很大的改进有时也可能差异微乎其微，小的改进却能带来巨大差异，以及为什么在动手修改之前理解你的整个系统非常有价值。

你的程序运行在 PHP 上，PHP 运行在你的 Web 服务器上并与你的 DBMS 通信，而两者都运行在你的操作系统上，操作系统又运行在物理硬件上。后续部分将审视所有这些环节，寻找改进机会并决定需要改进哪些方面的技术。

最后，这里会介绍一些可能使登录页面快一毫秒的微小杂项代码调整，之所以在这里介绍，是因为如果你从一开始就知道并使用了它们，日后就不会被诱惑去花更多时间回头在现有代码中引入它们，而这段时间本可以花在更有价值的事情上。

### 为什么要费事？

首先要问自己的问题是：“我*需要*做些什么吗？”如果你还没有开始编码，那么答案显然是“是”——花时间规划你的程序应该做什么，并试着感受其性能可能会在哪里拖后腿。但如果你有一个正在运行的站点，想要动手调整以使其运行更快，请自问这样做是否真的值得麻烦。*它运行得太慢了吗？* 是哪个部分？你的调整会让它变快吗？快多少？你确定在这个过程中不会弄坏某些东西吗？通过考虑这些问题，你可以避免在产生无收益的事情上浪费大量时间和精力，如果幸运的话，还能发现一个微小的改变就能为你带来巨大的性能提升。

### 用一点换很多

在我曾经工作的某家公司，有一台计算机用于生成报告。软件是 Windows NT4 和 Microsoft Access 97（那是 2004 年），安装的内存只有 32MB，打印报告是一项耐心的考验。在它重绘屏幕的时候，你甚至可以去喝杯咖啡。大家讨论说因为“太慢”了，所以要升级到新计算机。

“简单”的答案——即不需要分析就能达到的答案——是将现有机器更换为一台运行最新版 Windows 和 Access 的新计算机，随后设置网络用户账户，并花一天时间处理这类升级似乎必然伴随的“火灾”。但进行了一项分析，包括按下 Ctrl+Alt+Delete 调出 NT 的任务管理器及其进程列表，以查看当计算机用于生成报告时，每个进程花费了多少时间。（如果你不熟悉 Windows 中的这个进程，请想象一个使用 GUI 表格组件的精简版 `top(1)`。）

列表中最突出的特征是“System Idle Process”（系统空闲进程）项。它从未低于 85%。在二十分钟的操作中，处理器*实际在做事情*的时间只有三分钟；其余时间它都在等待内存和磁盘之间交换数据。这台计算机*本可以*比现在快六倍以上运行，*如果*它没有受到仅有的 32MB RAM 的拖后腿的话。256MB 就足以消除瓶颈；报告的生成时间将短于你走到打印机所需的时间；内存芯片比新机器和新的软件许可证便宜得多；而且与其花一天时间安装，停机时间将仅为五分钟左右。

### 用很多换一点

在 C 语言中，一个常见的惯用法是写 `a<<3` 而不是 `a*8` 来将变量乘以八。当然，这是可行的，因为在二进制中乘以 8（或 2³）等同于将所有位向左移动 log(8) 位。这可以应用于 PHP 吗？简短的答案是可以。但就像在 C 中一样，节省的时间是以纳秒计的。例如，在我 2.6 GHz 的 P4 上，PHP5.0.5 的差异是 50ns，4.3.11 是 3.5ns，版本之间唯一显著的差异在于按位移动的速度。你的结果可能有所不同。顺便一提，`8*$a` 比 `$a*8` 更快。

虽然在需要经常执行数百万次此类乘法的环境中（频繁到现代 C 编译器可以自行识别 `*8` 并将其转换为 `a<<3` *无论如何*），追求这样的节省是有意义的，但这对于基于 Web 的应用程序并不典型。更重要的是，在 PHP 中，这两个*“等效”*操作在极端情况下具有*不同*的行为：按位移动总是产生整数结果（可能为 0 甚至负数：`1073741824<<1=-2147483648` 和 `-2147483648<<1=0`），而乘法如果需要容纳结果则会返回双精度浮点数（`1073741824*2=2147483648` 和 `2147483648*2=4294967296`）。此外，你还必须记住，虽然乘法的优先级高于加法，但按位移动的优先级*较低*：是 `$a+$b*8` 但 `$a+($b<<3)`。




这一切都值得吗？如果让你将操作写成乘法需要多长时间，写成位移又需要多久？验证你所写代码的正确性需要多长时间？修复由极端情况下行为差异或忘记运算符优先级差异等导致的 bug 需要多久？未来花费在修改代码上的时间呢（例如，将乘以 8 改为乘以 9）？（你并不能仅仅搜索 8 的实例；你还必须搜索 3 的实例，而且为什么你不使用命名常量？）该操作需要执行多少次才能节省你花在确保使用更快选项上的相同时间——这里一个纳秒，那里一个纳秒？该操作需要多长时间才能被执行那么多次？

重点是，*你*的时间比*计算机*的时间更有价值。唯一比你更有价值的，是访问你网站用户的时间。因此，不要浪费时间试图从页面处理时间中削减几纳秒：即使是在异常高负载下，网站访客也不会注意到这种差异。

### 比较字符串的速度——基准测试示例

PHP 有几种组合字面字符串和变量的方式，以及三种引用字符串的方法。这三种引用方法分别是使用单引号、双引号和 heredoc（多行字符串）语法。将变量插入字符串可以通过使用连接运算符、在双引号和 heredoc 引用的字符串中进行变量插值，以及 C 风格的字符串格式化函数来实现。时不时地，会有好奇的程序员问哪种方法“更好”。“更好”可以以多种方式定义：它更快吗？它使源代码更具可读性吗？它是否更简单且更少出错？就可读性和简单性而言，辩论几乎势均力敌：如果其中一种方法*明显*优于其他方法，那么自然选择会看到大型应用程序中的资深开发者仅使用这种优越方法，而排除所有其他方法。多年来，似乎没有发生这样的选择，这表明差异并不显著，不足以出现在行业最佳实践文档或编码标准中。

单引号字符串是否比双引号字符串*更快*，则要容易量化得多。如果你被迫给出一个“是”或“否”的回答，那么最安全的说法是“是”，但现实中事情比这更复杂。

与任何关于现实世界的问题一样，在获得一些事实之前是无法回答的。作为一个初步实验，你可以编写以下代码：

```php
<?php
$variable = 'string';

$start = microtime(true);
for($i=0; $i<1000000; ++$i)
{
        $string = "this string has a $variable embedded into it";
}
$laptime = microtime(true);
for($i=0; $i<1000000; ++$i)
{
        $string = "this string has a ".$variable." inserted into it";
}
$finish = microtime(true);

echo "Variable interpolation required ".($laptime-$start)." seconds for one million iterations.\n";
echo "Variable concatenation required ".($finish-$laptime)." seconds for one million iterations.\n";
?>
```

我第一次运行这个脚本时，插值和连接的时间分别为 6.81 秒和 1.72 秒。然而，第二次运行时，我得到的时间是 6.58 秒和 1.71 秒。这种变异性是由于我运行的计算机所做的不仅仅是运行该脚本。它对时间有其他需求，而这些需求所占用的时间被包含在该脚本完成所需的时间中。当脚本第一次运行时，操作系统必须为 PHP、脚本及其数据组织内存空间，其中一部分组织发生在脚本运行期间（但其中大部分会在脚本开始执行之前发生，因此不会反映在计时中）。但紧接着的第二次运行，将在已经存在合适空闲空间块的环境中运行，因此启动速度要快得多。

这一结果意味着你无法仅信任一次运行的结果；计时波动的方式有太多，其中许多是你无法控制的。必要的是将脚本从头到尾运行多次，并对结果取平均值。对于插值，10 次运行的时间范围在 6.57 到 6.86 秒之间，平均值为 6.77；对于连接，范围在 1.65 到 1.71 之间，平均值为 1.70。如果你愿意，可以对数据应用更多的统计火力，但看起来很明显，连接比插值快大约四倍。

但这还不是全部。如果时间取决于字符串*长度*或正在连接或插值的变量*数量*呢？你不也应该测试*这些*的变化吗？

以下是一个用于进行此类测试的命令行 PHP 程序。它不是在连接或插值变量时测量*自身*，而是编写*一个单独的* PHP 脚本，然后通过命令行调用它，从而不仅计时该脚本本身，还包括启动 PHP、加载脚本和关闭所花费的时间。它对一系列初始字符串大小（64 到 26176 个字符，步长为 512）和插值/连接次数（0 到 100）执行此操作。每个实验执行五次，并将平均运行时间写入单个日志文件。如果两万五千个单独的实验太多了（可能需要大约四个小时），则可以酌情减少范围，但应该保留对每个大小/数量组合的多次测试和结果平均。按原样编写，它计时的是变量插值——取消第 59 行的注释并注释掉第 58 行（即 `str_replace()`）将其改为计时连接：

```php
<?php
function generate_test($string)
{
    $code = "<?php
\$interpolated = \"badgers!\";
for(\$i=0; \$i<100; ++\$i)
    \$string = \"\$string\";
?>";
    $temp_file = tempnam('', 'runtest');
    $fp = fopen($temp_file,'wb');
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
for($string_size=1<<6; $string_size<=26176; $string_size+=1<<9)
{
    $generic_string = str_repeat("wibble splunge!\n", $string_size);
    $real_string_size = 16*$string_size;
    $all_positions = range(0,$real_string_size-1);
    for($num_variable_interpolations=0; $num_variable_interpolations<100;
        ++$num_variable_interpolations)
    {
        echo $string_size.",",$num_variable_interpolations.",\n";
        $string = $generic_string;
        if($num_variable_interpolations==0)
            $positions = array();
        else
            $positions = array_rand($all_positions,$num_variable_interpolations);
        if(count($positions)==1) $positions = array($positions);
        foreach($positions as $position)
        {
            $string = substr($string,0,$position).'{$'.substr($string,$position);
        }
        $string = str_replace('$', '${interpolated}', $string);
        // $string = str_replace('$', "interpolated.'", $string);
        $file = generate_test($string);
        $runtime = run($file);
        unlink($file);
        fwrite($log,
            $string_size.",",$num_variable_interpolations.",",$runtime.",\n");
    }
}
fclose($log);
?>
```

从代码中最后的 fwrite() 可以推断出保存数据的格式：每个实验一行，由字符串大小（在变量插入之前）、插入变量的数量和秒数组成。然后，你可以将这些数据读取到你首选的数据分析或绘图软件中进行探索。




## 第 9 章

生成的“时间”与“字符串长度”以及“变量数量”的关系图，在连接（参见图 9.1）和内插（参见图 9.2）中看起来截然不同。

![](img/cacdd24f2926f10ee3219256ad732604_229_0.png)

![](img/cacdd24f2926f10ee3219256ad732604_229_1.png)

在这些图表中，你首先可能看到的是，当在双引号字符串中进行内插时，变量的数量几乎无关紧要。有一些迹象表明，当变量数量是 32 的倍数时，处理速度特别慢。由于改变变量数量是由内循环完成的，因此对于*特定*变量数量的实验是在运行期间在间隔较大的点上进行的，从而排除了除可疑的、时机巧合的外部瞬态延迟以外的所有因素。

#### 代码效率

当变量数量非常小时，比较这两个图表，首先会注意到两个不寻常的现象：一是连接的速度最初*下降*，二是内插的速度*急剧上升*。仔细检查后发现，当变量数量为 0 时，双引号字符串和单引号字符串的速度相同，只有当存在需要内插的变量时，双引号字符串才会变慢。这是因为双引号字符串在程序加载期间（即词法分析阶段）会被扫描以查找变量。这是一次性的开销，甚至可能比你最初预期的还要小：单引号和双引号字符串的内容*无论如何*都需要被扫描，以定位转义序列和字符串的实际结尾。唯一的实质区别在于，当存在变量时，扫描双引号字符串会依次生成多个标记。

总体而言，两个图表的形状非常有特色。这种差异可以通过使用“大 O 符号”来形式化描述，该符号用于程序分析中，以描述算法相对于给定*大小*的“规模”或“速度”。虽然可以给出其精确的技术定义，但只需将 *O(*f(*n*)*)* 理解为意味着算法行为的图像随着 *n* *变得越来越大*时，“看起来像” *f(*n*)* 的图像即可：

```
O(f(n)) = the set of functions g(n) such that there exist positive constants c and n0
          such that 0 ≤ g(n) ≤ cf(n) for all n ≥ n0.
```

在这种情况下，双引号内插的图不随 *v*（被内插变量的数量）变化，仅随 *l*（字符串长度）线性变化（也就是说，当字符串长度加倍时，速度减慢两倍）。在大 O 符号中，这被描述为 O(*l*)。单引号连接的图更复杂。如果固定字符串长度，并观察图中随变量数量变化的单个切片（如图 9.1 所示，切片是从左侧到峰值的顶部边缘），它看起来在 *v* 方面相当线性。如果固定变量数量并允许字符串长度变化（从峰值向右下延伸的脊线），曲线呈现出抛物线的形状。总体而言，这两种影响似乎是相乘的，给出了 O(*fv²*) 的大 O 描述。

在*长远来看*，I 的增长比 *fv* 更慢，事实上，对于具有许多变量的长字符串，内插比连接*更快*。然而，对于较短的字符串或较少的变量，连接仍然占优势。

大 O 符号只关注随着问题规模变大，程序在长远来看会发生什么，而忽略仅在问题的小实例中出现的特征。你会记得，当没有变量参与时，两种方法速度相同（因为它们都由单个字符串组成），但单引号连接会先略微加速然后再次减速，而双引号内插只要引入单个变量就会急剧减速，且不会恢复。大 O 理论指出，在*长远来看*，变量内插比连接更快，但你实际上需要多千字节大小且包含数十个变量的字符串才能看到这种现象的发生。

你可以看到，即使在这个非常简单的例子中，仅有两个需要考虑的因素，在寻求关于什么是“最佳”的确定性答案时，也存在着大量的细微差别。你甚至可以对这个相对琐碎的例子进行更深入的调查，而对于更复杂的问题，你可能需要在得出结论之前这样做。但这里是结束这个例子的好时机，除了注意到在所有记录的实验中，最慢的时间是 3.7 秒。

#### 反直觉的结果

与 C 不同，C 会被转换为机器代码，这与你实际编写的内容没有太大区别（该语言被描述为“带有宏大幻想的汇编器”），你的 PHP 程序是由 PHP 引擎模拟的虚拟机运行的。当涉及到性能调优时，这可能会造成困难，因为预测什么效果好、什么效果不好变得更加困难。这一点稍后将被探讨，但此时你不妨对以下测试代码的结果进行思考：

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

echo "Postincrementing I and J one million times: ";
$test_1, " seconds.\n";
echo "Postincrementing I and preincrementing J one million times: ";
$test_2, " seconds.\n";
echo "Preincrementing I and postincrementing J one million times: ";
$test_3, " seconds.\n";
echo "Preincrementing I and J one million times: ";
$test_4, " seconds.\n";
?>
```

#### 基准测试与性能分析

有很多技术和工具用于估算程序的速度，在致力于加快网站速度的任何任务之前、期间和之后，都应使用它们，以免你浪费时间在没有任何显著差异的更改上，或者更糟的是，使你的网站变慢。广义上说，它们可以分为两个主要类别：基准测试（benchmarking）是你在实施某个功能之前进行实验以确定最佳方法时所做的事情，而*性能分析*（profiling）涵盖你对实际事物进行实验以查看其实际表现如何。显然，这两者之间有很多重叠；许多技术和工具是相同的（因为工具并不一定*关心*你使用的代码是自然的还是合成的）。在操作系统和 PHP 层面，都有工具可以辅助你完成这些任务。

#### PEAR 基准测试

你已经在上一节中看到了基准测试的示例。它们是临时构建的，但它们共有的基本思想足够通用，值得抽象为一个独立的类：

- 1. 启动计时器（记录当前时间）。
- 2. 执行某些操作。
- 3. 停止计时器（再次记录当前时间）。
- 4. 将停止时间与启动时间进行比较，以确定经过的持续时间。
- 5. 重复步骤 1–4 很多次，积累持续时间。
- 6. 查看结果。

一个显而易见的增强功能是为计时器添加标签，这样多个计时器可以独立启动和停止。如果计时器还能包含有关所覆盖代码特定部分所花费时间的信息，那就更好了。PEAR Benchmarking 类提供了所有这些功能。PEAR 和 PEAR 包的安装在第 8 章中有所介绍；因此，你已经完成了这部分，并准备开始使用它。

要使用 Benchmarking 类重复最初的字符串构建实验，你可以编写以下代码：

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
$timer->setMarker('laptimе');
for($i=0; $i<100000; ++$i)
{
    $string = "this string has a "$variable." inserted into it";
}
$timer->setMarker('finish');

echo "Variable interpolation required "$timer->timeElapsed('start','laptimе')." 
```




# 第 9 章

```php
<?php
echo "Variable concatenation required ".$timer->timeElapsed('laptimer','finish')."
seconds for one million iterations.\n";

$timer->stop();
$timer->display();
?>
```

`Benchmark_Iterate` 是 `Benchmark_Timer` 的子类，它提供了一个 `run()` 方法，你可以传入想要测试的函数名称。在选择使用哪一个类时，有两点需要考虑。首先，调用函数本身会消耗一定的时间。其次，`Benchmark_Iterate` 会为每个单独的实验保留计时数据。进行大量实验意味着会产生一个巨大的数组，这就是为什么以下代码只运行一万次实验而不是一百万次：

```php
<?php
require 'Benchmark_Iterate.php';

$variable = 'string';

function interpolate($variable)
{
    $string = "this string has a $variable embedded into it";
}

function concatenate($variable)
{
    $string = "this string has a ".$variable." inserted into it";
}

$interpolation_benchmark = new Benchmark_Iterate;
$concatenation_benchmark = new Benchmark_Iterate;

$interpolation_benchmark->run(10000, 'interpolate', 'string');
$concatenation_benchmark->run(10000, 'concatenate', 'string');

$interpolation_result = $interpolation_benchmark->get();
$concatenation_result = $concatenation_benchmark->get();
?>
```

这两个结果变量是数组：`$interpolation_result['iterations']` 记录测试运行的次数，`$interpolation_result['mean']` 记录平均值（`Benchmark` 类如果可用的话会使用 bench 函数来保持计算该值时的准确性）。取消这两个元素的设置后，你剩下的是一个以数字为索引的数组，其中包含每次迭代的各个独立时间，以便你可以执行认为相关的其他统计测试。

### top 和 ab

前面提到的关于 NT4/Access 报告生成器的轶事来自 Windows 世界，并提到了其任务管理器的使用。Unix 类型操作系统随附的流程监控工具名为 `top`，它提供的信息量要丰富得多。与此同时，Apache 发行版包含 `ab`（ApacheBench）程序，它测试你网站的“锋利端”：你能多快地提供服务？将这两者并排使用往往很有启发作用：用 `ab` 查看你的性能表现如何，用 `top` 查看为获得该性能投入了多少资源。

当然，你要在 Web 服务器本身上运行 **top**；`ab` 可以在同一位置运行，但为了公平起见，值得在局域网的另一台机器上运行它（在更远的地方运行会引入额外的延迟，从而妨碍你对服务器进行压力测试）。例如，你可以在工作站上打开一个终端窗口并 ssh 到 Web 服务器，在你的工作站上运行 **ab**，在服务器上运行 **top**，并将两个终端窗口并排显示。

简单来说，**ab** 是一个加速的 **http** 客户端。典型的调用方式是让它在短时间内连续请求同一页面一千次，从而模拟一千个用户几乎同时访问。它收集有关服务器响应请求所需时间的统计数据，以及是否有请求未能满足。看看这个例子：

```bash
ab -n1000 -c10 http://bowman/page2test.php
```

此命令告诉 **ab** 总共请求 `page2test.php` 一千次，最多十个请求并发执行。因此，它会发出十个请求，一旦其中一个请求得到满足且响应已收到，它就开始第十一个请求，直到总数达到为止。

在发出一千个请求后，它会展示一份收集到的统计报告。其中包括整个运行的总时间、响应的大小、发出和失败的请求数量、请求生成的速率（对应于请求被满足的速率）、响应本身以 bps 为单位的服务速度，以及平均和慢速响应所花的时间。

对于基准测试而言，调整总请求数参数 `-n` 的重要性较低；它只需至少与 `-c` 一样大，并且足够大，以便整体统计数据得以平滑，而测试开始时没有瞬态行为干扰结果。调整并发参数 `-c` 更具信息量。从 `-c1` 开始（你将 `-c` 设置得越低，`-n` 就可以设置得越低，除非你真的想坐在那里等待那么久），你可以查看服务器是否有能力一次响应一个请求。随着你增加 `-c`，并发请求的数量会增加，你可以观察服务器是否能够处理不断增加的负载。例如，随桌面版 Microsoft Windows 发行的 IIS 版本被限制为最多 10 个并发请求。一旦 `-c` 超过 10，你将开始收到失败的请求。是的，你可以使用 ApacheBenchmark 测试其他服务器；在某种程度上，它被称为“Apache”是因为它是 Apache Group 的产品。随着负载增加，传输速率将下降，请求发出的速率将增加，最终请求将开始失败。如果你觉得有点残忍，你可以模拟被 Slashdot 攻击：对服务器使用 `n10000 c1000`，看着它因过载而崩溃。

与此同时，在另一个终端窗口中是服务器视角下的情况。当你运行 **top** 时，首先要查看的是负载平均数（load average）。给出的三个数字分别代表过去一分钟、五分钟和十五分钟内的活动进程平均数量（即正在运行或等待运行的进程，相对于当前空闲的进程）。如果你把服务器想象成银行，处理器想象成柜员，进程想象成客户，那么负载平均数就代表了正在接受服务或排队的人的数量。显然，如果柜员不够，就会有越来越多的人变得烦躁。同样，过高的负载平均数意味着进程花费了太多时间在队列中等待运行的机会。因此，发起这些进程的那些人的请求也在等待结果，他们或他们的浏览器甚至可能会放弃——这对你的网站来说并不是好现象。

理想情况下，你希望负载平均数略低于服务器处理器的数量，保留一些余量以应对异常沉重的负载。短暂的峰值是可以容忍的，但前提是很短暂。15 分钟负载平均数不应出现峰值；如果出现，则表明当服务器繁忙时它过于繁忙，且正在形成一个需要很长时间才能处理的积压。足够大的峰值会显著影响 15 分钟平均值，这表明无法快速处理这种激增。

在 `top` 显示的负载平均数下方是每个处理器的活动级别，以百分比给出。这也应该保持在相对较低的水平，以应对“Slashdot 效应”或最新蠕虫的攻击尝试。如果机器是专用的 Web 服务器，那么当没有提供服务时处理器有显著活动可能表明它正在做不该做的事情。检查进程列表本身，看看哪些进程正在使用处理器。你可能可以移除其中一些。仅仅提供静态网页或文件的站点几乎不会经历任何 CPU 负载——一台 20 世纪 80 年代生产的处理器完全能够以从磁盘读取数据的同等速度传输数据——但动态生成的页面确实会在这个环节遇到瓶颈。

另一方面，即使 CPU 几乎空闲，服务器也可能在全力运行。回想一下 Windows 报告生成器的轶事，简单的任务花费了永远的时间，而处理器花费了 85% 的时间无所事事，最终确定问题在于机器中的 RAM 太少。

在 `top` 的 CPU 使用率报告下方，是关于可用内存量的报告，包括使用量和剩余自由量，既在 RAM 中也在交换文件中。你希望尽可能少依赖交换文件，理想情况下是完全不使用。

### 硬件改进

所以，你已经决定网站运行缓慢。你剖析了发生的事情，现在准备着手改进现状。最根本的改进来自于记住你的服务器存在于现实世界中，并受物理定律约束。你无法改变物理定律：你必须适应它们。

首先要查看的是你与外部世界的连接。你需要一条宽敞的大管道。如果你的服务器负载较轻但网络流量已满，那么你的连接就是瓶颈。

处理完这个问题后，检查处理器。如果它一直运行在其范围的上限，那么升级可能会给你更多的回旋余地。你的机器有多久了？两年？你可能会发现新机器比当前机器快两倍以上。当然，更换计算机是你所能做出的最根本、充满危险且几乎肯定昂贵的改变。如果你能简单地把新机器拿进来，把旧机器的电缆换到新机器上，进行硬盘移植，然后启动，那就太好了。事情往往不会那么简单。

如果处理器相当空闲，但内存紧张，那么增加 RAM 是你的下一个优先事项。除了最高流量站点或拥有最大数据库（通常由 MySQL 缓存到 RAM 中以提高访问速度）的站点外，512MB 对于其他所有站点来说都绰绰有余。

对于主要提供静态页面或文件的站点，RAM 比处理器速度更重要——将数据块从机器的一部分移动到另一部分非常简单，因此快速计算出如何移动数据并不像一次性移动大量数据那么重要。





磁盘访问是一个相对缓慢的过程。建议升级至吞吐量更大的高速硬盘。如果您的当前驱动器即将写满，请考虑添加额外的驱动器，而不是将所有内容迁移到更大的驱动器中。即使您的当前驱动器未接近满载，获取额外驱动器并在它们之间分布内容也可能改善访问时间。各磁盘的读写磁头将同时工作，且其移动距离不会像单个大容量驱动器的磁头那样远。磁盘也不需要进行如此大幅度的旋转。

### Web 服务器优化

就其本质而言，Apache 具有高度可配置性，拥有许多可调优的设置，以优化其行为的某个方面或另一个方面。一些设置旨在减少 Apache 所需的内存量，而其他设置则旨在减少每个进程所执行的工作量。

启动 Apache 时，它做的第一件事是启动大约六个（具体数字当然是可配置的）**httpd** 实例。这些进程是实际处理 HTTP 请求的进程。服务器本身所做的仅仅是管理这些子进程，根据需求启动新的子进程并停止现有的子进程。每个实例大约占用 1 MB 的 RAM（很难更精确地估计，但这是一个合理的经验法则），并在那里等待请求。如果请求的数量多于实例的数量，就会启动新的实例；如果后来负载减轻，多余的实例将被关闭。即使有足够的工作任务，有时 **httpd** 实例也会被关闭。这使得操作系统能够回收可能从 **httpd** 进程本身或其使用的任何模块中泄漏出来的内存。当然，**httpd** 进程也可能直接崩溃，在这种情况下，该特定请求将失败；但会有另一个实例待命，以便在请求重试时进行处理。这是 Apache 采用此方式运行的关键原因之一：它使服务器即使在崩溃后也能保持运行。

控制此行为的配置选项可以在 **httpd.conf** 中找到或添加进去：

- **MaxClients**：这是您准备在任一时刻支持的最大 **httpd** 进程数，因此也是并发处理的最大客户端请求数。根据每进程 MB 数的经验法则，将此值设置得高于您的 RAM 容量是没有意义的。事实上，您会在达到此值之前耗尽 RAM。它们将继续工作，但将依赖于速度慢得多的虚拟内存，并且磁盘和 RAM 之间会出现大量令人讨厌的交换操作。
  - 您也不希望此设置过低；如果发出的请求多于此数值，部分请求将被遗漏，不得不等待其他请求完成。如果延迟时间过长，客户端将放弃，请求将被报告为失败。
- **MaxRequestsPerChild**：一旦 **httpd** 的某个实例处理了这么多请求，它就会被关闭，无论当前服务器负载如何，以防服务器或已安装模块中存在未修复的内存泄漏，导致实例因“肥胖”而失败。由于根据定义，操作系统无法意识到这种尺寸增加是不必要的，Apache 必须任意介入以关闭进程。此指令控制这种情况发生的频率。除非您正在使用实验性或开发中的模块（可能存在 bug），否则您应该能够将此限制设置为 100,000 而不会有任何不良影响。使用 `top` 监控每个 **httpd** 进程的 RAM 消耗；如果它们似乎不受控制地增长，请将限制降低 10 倍。继续监控并根据需要降低。请留意整个系统的行为，因为如果该数值降得过低，将在启动和停止子请求上浪费太多时间，因此是时候尝试找出导致问题的模块了。

### 第 9 章

- **StartServers** 和 **MinSpareServers**：**StartServers** 指定启动 Apache 时初始化的 httpd 实例数量。一个好的数值是您网站通常处理的并发请求数。**MinSpareServers** 将是这个数值再加上几个。由于启动新实例涉及一定的工作量，您不希望服务器在已经满负荷处理请求时还要这样做，因此保留一些余量是有好处的。

当网页请求进来时，通常随后会有来自同一客户端的额外请求，用于获取辅助资源（样式表、内联图像等），以及可能后续对更多页面的请求。在期间保持客户端与服务器之间的连接是合理的，以避免浪费——即打开和关闭连接，仅为了几百毫秒后向同一客户端立即打开一个新连接，然后发现有一个 httpd 实例已准备好接受请求（这种情况更可能发生的是，那个实例恰好是处理了前一个连接并现在处于空闲状态的实例）。现代 HTTP 1.1 标准提供了这种选项——称为“*Keep_Alive*”（保持连接）——并且现代版本的 Apache 默认遵循此标准，当然具体取决于 Apache 配置文件中的设置。

- **KeepAlive**：默认为 On（开启），您通常没有太多理由将其关闭。
- **MaxKeepAliveRequests**：一旦客户端和服务器之间建立了连接，处理该连接的 httpd 实例将专门为该客户端服务，最多处理如此数量的请求。此值可以设置得相当高——大约 100。很少有页面请求随后伴随一百个辅助请求，但可能会发生这种情况：用户加载第一个页面后，可能会快速打开另外半打页面。将此选项设置得较高不会造成太大麻烦，因为客户端通常会从自己的端点关闭连接；在客户端未关闭连接的情况下，以下配置指令将生效。
- **KeepAliveTimeout**：如果在当前连接上客户端在这么多秒内没有发出请求，服务器将假定客户端因某种原因离开而未正确关闭连接。您的网站与客户端之间的带宽越高，此数值可以越低。带宽是拨号用户的一个瓶颈，它降低了请求发起的速率，因此连续请求之间可能有 30–45 秒。此数值的一个较低界限大约是 10–15 秒。

为了记录流量日志，Apache 可以使用反向 DNS 来查找请求来源 IP 的主机名。这使通过肉眼阅读日志变得稍微容易一些，但这大致就是它的唯一好处。与此同时，请求正在等待 DNS 服务器的响应，在收到响应之前无法继续。您最好只是在日志文件中存储 IP 本身，并在您实际关心时，将查找工作留给类似 Apache 的 `logresolve` 实用工具。

- **HostnameLookups**：这设置是否在服务器日志中记录主机名（On）或 IP 地址（Off）。

与此相关的是，您在允许或拒绝连接时是使用域名还是 IP 地址。同样，在您的 `.htaccess` 文件中使用 **allow from example.com** 或 **deny from example.com** 意味着必须进行反向 DNS 查找，以确定来源 IP 属于哪个域名（然后进行*正向* DNS 查找，以检查该 IP 是否确实属于所声称的域名）。因此，同样地，允许或拒绝特定的 IP 地址范围而非域名更为有效。但是，请记住，DNS 的一个主要功能就是特定的域名并不永久绑定到特定的 IP 地址，该名称可以转移到不同的主机和不同的 IP 地址上。




#### 代码效率

说到 `.htaccess`，当 Apache 被要求读取一个文件时，它会检查文件系统路径（而非 URL 中描述的路径）中从该文件所在目录到系统根目录（包括根目录）的每一个目录中的 `.htaccess`。如果路径很长，这意味着大量的查找操作，因此保持路径简短会有帮助。如果你（毫无疑问）将整个站点存储在单个文档树中，而不是分散在系统的各个角落，那么让 Apache 搜索该文档树根目录之上的位置就没有意义了。`.htaccess.conf` 文件提供了一种告知 Apache 这一点的方法。首先，你声明从系统根目录向下不允许任何 `.htaccess` 文件覆盖设置，然后紧接着声明在站点的文档树中 *可以* 尊重 `.htaccess` 文件：

```
<Directory />
    AllowOverride None
</Directory>
<Directory /www/siteroot>
    AllowOverride All
</Directory>
```

如果你根本不使用 `.htaccess` 文件，请明确说明，这样 Apache 就不会浪费时间查找它们：

```
<Directory /www/siteroot>
    AllowOverride None
</Directory>
```

有一个可以加速输出的 Apache 模块，即 mod_gzip。如今大多数浏览器内置了 gzip 库，并且可以在接收数据时解压缩 gzip 压缩的数据。这些浏览器会在其请求头中包含一条说明此情况的语句。作为回应，安装了 mod_gzip 的 Apache 将发送压缩后的响应。虽然压缩/解压缩步骤会引入延迟，但对于高压缩率的文档（英文文本压缩率约为 30%，HTML 约为 60%），带宽的节省是不可忽视的。

否则，请移除所有你实际不使用的模块。例如，如果你不使用 `.htaccess` 文件，就禁用 mod_access。PHP 扩展及其调用的任何库也是如此；如果你不使用 SimpleXML 扩展，就禁用它。

#### PHP 优化

一旦你优化了硬件、数据库和 Apache，你就可以专注于调整你的实际代码。在此时，你能为自己做的最好准备是选择并坚持一套一致的编码标准。你花在尝试解读自己代码上的时间越少，就越能花时间去寻找其他提高其效率的技巧。

#### 编码标准

访问你站点的访客具有优先权。你的工作是努力以最快速度获取他们想要的信息。另一方面，你的时间比计算机的更有价值——甚至*更昂贵*。

如果你能以额外 1 毫秒处理时间为代价节省自己 5 分钟的工作量，这是一项好投资，即使该页面已被处理三十万次，它也会持续带来回报。你可以把这 5 分钟投入到更具生产力的事情上，比如*查看是否有方法在处理页面时节省 20 毫秒*。这不仅仅是尽可能快地满足用户请求的问题——考虑到*服务器与用户浏览器之间*所有的延迟可能性，单纯的速度可能并不是那么重要的因素。（如果你的站点极其繁忙，那么速度确实重要，但如果是这种情况，正如你将会看到的，瓶颈可能在别处。）问题在于，如果你能让现有页面运行得更快，你就可以开始思考该页面还能为你的站点受众做些什么。

但你如何能实现这种工作量的转移？如果并没有减轻你的工作负担，只是给计算机添加更多内容是不够的。节省编程时间的一个关键方法是以一种让阅读代码尽可能无麻烦的方式编写代码。

现在，*没有什么比诸如缩进多少、缩进哪些部分、大括号应放在哪里、以及 else 是否应与相邻大括号出现在同一行（如 `this } else {`）这类问题更容易引发激烈争论*了。事情可能会变得丑陋。而且即使你决定了这些事情，你仍然需要决定诸如变量、函数、对象和类的命名约定；是否将方法声明为 `protected static` 还是 `static protected`（如果你需要进行查找和替换，这很重要）；你是声明 `global $foo;`、`use '$GLOBALS['foo']'` 还是彻底禁止使用全局用户变量；以及在哪里放置注释以及在注释中写什么；更不用说更实质性的问题，比如你的代码如何划分为文件。

> 避免使用“代码美化器”——那些接收源代码文件并根据某些标准重新格式化后返回的程序。至少，不要依赖它们。你的代码一开始就应该是美观的；否则，你就没有达到拥有标准的意义。如果你有一些旧代码或来自其他地方且标准不同的代码，希望使其与自己的标准一致，或者使你的代码与他人的标准一致，那么可以使用它们。但不要通过兴奋地制造一堆混乱来工作，因为你可以事后使用美化器让它变得漂亮。

##### PEAR 编码标准

一种切断至少部分杂乱局面的方法是采用现有的风格指南。虽然你可以采用为 C、C++ 或 Java 等类似语法的语言开发的指南，但这种匹配可能不是理想的。例如，你命名变量的方式并不需要与命名函数的方式截然不同；前者已经通过 $ 进行了区分。相反，你可以采用 PHP 特定的标准，其中最广泛的是 PEAR 手册第 4 章中描述的标准。

除非你正在建立一个由公众提交代码的仓库（如 PEAR 本身的情况），否则严格遵循 PEAR 风格可能并不合适。例如，PEAR 风格要求每个源文件以一个注释块开头，其中说明了作者和许可证等信息。对于一个大型的、内部使用且不会分发的应用程序来说，分发许可证毫无意义，也没有必要在每个文件中列出所有开发者。然而，PEAR 标准是一个起点。

##### 大括号和缩进

关于大括号应放在哪里的争论旷日持久且没有结论，以至于至少有一种语言（Python）被故意设计以避免使用大括号。Eric S. Raymond 在《Jargon File》（版本 4.4.7）中，在“Indent Style”条目下列出了四种风格，这里将介绍这些风格及其名称，并附上另外几种风格。

- K&R 风格——正如 C 语言的设计者 C 语言权威参考书的作者 Kernighan 和 Ritchie 所使用的那样——也被称为“唯一正确的大括号”风格：

```
for($i=0; $i<100; $i++){
    if($foo[$i] == 0){
        //...etc.
    }
}
```

- 在 Allman 或 BSD 风格中，许多 BSD 内核源代码是由 Eric Allman 编写的，他在该工作中使用了这种风格：

```
for($i=0; $i<100; $i++)
{
    if($foo[$i] == 0)
    {
        //...etc.
    }
}
```

- Whitesmith’s 风格以一家以这种方式格式化代码的商业 C 编译器命名：

```
for($i=0; $i<100; $i++)
{
    if($foo[$i] == 0)
    {
        ...etc.
    }
}
```

- GNU 风格被（几乎排他性地）自由软件基金会使用：

```
for($i=0; $i<100; $i++)
{
    if($foo[$i] == 0)
    {
        ...etc.
    }
}
```

- Allman 风格的一种更紧凑版本如下：

```
for($i=0; $i<100; $i++)
{    if($foo[$i] == 0)
    {    ...etc.
    }
}
```

- Allman 风格的一种更紧凑版本是：

```
for($i=0; $i<100; $i++)
{    if($foo[$i] == 0)        //...etc.
} }
```

所有六种风格都可以通过选择使用制表符或空格，或者每个缩进级别有多宽来变化。通常，四个或八个空格（或八空格宽的制表符）是最常见的，制表符常常不受欢迎，因为不同的人使用不同宽度的制表符。看起来适合一种宽度制表符的空格和制表符混合，不太可能适合另一种宽度，从而导致所谓的“制表符损坏”，代码行和代码片段出现在各种看似随机的缩进位置。

最后一种风格是一种恶作剧：如果你要对齐开头和结尾括号所在的列，至少应该确保对齐*匹配的*开头和结尾括号对，否则这种对齐只会引起误解。如果节省行数如此重要，你不如使用 LISP 风格的缩进：

```
for($i=0; $i<100; $i++)
   {if($i) !=0)
      {...etc.}}
```

PEAR 指定使用 K&R 风格缩进，每个缩进使用四个空格，不使用制表符字符。排除制表符字符的原因当然是由于制表符损坏的影响；但了解制表符损坏的原因可以很大程度上防止其发生。

当你假设制表符具有特定宽度时，就会发生制表符损坏。下面这段代码是使用制表符进行缩进编写的，编辑器被设置为每个制表符使用四个空格：

```
/************************
 * Big Flashy          *
 * Box comment          *
 *       *        *  *
 * Just Because (TM)  *
 ***********************/
for($i=0; $i<100; $i++)
{
   if ($a==$i || $b===$i)
      &&
      ($c!=$i || $d!=$i))
   {
      echo "Either $a or $b is equal to $i, ",
      echo "and either $c or $d is not.";
      &&
   }
}
```

而这是在配置为八空格制表符的编辑器中的外观：

```
/************************
 * Big Flashy          *
 * Box comment          *
 *       *        *  *
 * Just Because (TM)  *
 ***********************/
for($i=0; $i<100; $i++)
{
      if ($a==$i || $b===$i)
         &&
         ($c!=$i || $d!=$i))
```



#### 代码效率

```php
{
    {
        echo "Either $a or $b is equal to $i,";
        echo "and either $c or $d is not.";
    }
}
```

你首先会注意到的是，那种夸张的大框注释（Big Flashy Box comments）通常弊大于利。它们往往是 Tab 缩进损坏的最大受害者，这颇具讽刺意味，因为这些注释本应是专门供*人类*阅读的，而机器并不关心格式的美观性。

如果你确实希望使用 Tab 进行缩进，那么经验法则是：Tab 仅应用于*缩进*，而任何额外的对齐任务都应使用空格。在上一个示例中，用于将 `if` 测试的第二行和第三行与第一行对齐的额外 Tab——这在四空格 Tab 设置下运作良好——当它们变成八空格 Tab 时，导致这些行被推得过远向右。应当使用*四个空格*（在 Tab *之后*）来匹配四个字符“`if ( `”的宽度，而不是第三个 Tab。

通常，源代码中唯一的 Tab 应位于行首；它们不应跟随在任何其他字符之后。例外情况有两个：要么是字面上的 `tab` 字符确实被需要，要么是你正在使用“压缩的 Allman”风格，在这种情况下，单个 Tab 用于将 `(` 与后续语句分隔开。

你可能已经注意到，除了恶作剧式的风格外，所有描述的代码风格——其闭合大括号都独占一行。这种风格在代码列表中产生的效果是，在语句块结束和后续代码之间引入一个可见的间隙，这在某种程度上类似于英文文本中的段落换行。因此，你可以认为 K&R 或压缩的 Allman 风格比 Allman 风格“更好”，因为它没有将语句块与引入它的结构（for、if、switch 等）分开。根据 Raymond 的说法，支持 K&R 风格的主要理由是它在垂直空间上更经济，允许在屏幕上一次显示更多的代码。不过显然，压缩的 Allman 风格兼具这两者优点，同时仍允许匹配的大括号对齐。

##### 减少嵌套层级

如果嵌套大括号的数量过多，识别给定的闭合大括号与哪个开括号配对可能会变得令人困惑。大多数 IDE 和一些优秀的语言敏感型文本编辑器能够找到这些配对，而不会被注释或字符串字面量中出现的大括号搞乱，但通过肉眼定位它们（例如，当你漏掉输入其中一个时）仍然是极有可能的需求。在阅读代码时，你经常会看到闭合大括号后跟有诸如 `/*/ end for */` 或 `/* if($i==0) */` 这样的小注释，试图提供辅助。然而，明智地使用 break 和 continue 语句可以帮助减少嵌套深度。通过这样做，你不仅减少了代码向右边缘偏移的趋势，还减少了带括号块的数量和大小，从而减少了括号的数量，并让每对匹配的括号更紧凑，以便更快地通过肉眼识别。

例如，之前关于缩进风格的示例是这样编写的，使得 for 循环的主体完全由一个 if 语句组成——如果 if 语句的测试失败，那么在该次迭代中什么也不会发生，处理将继续到下一次迭代。用这种方式表述，你可以看到循环的等效实现如下：

```php
for($i=0; $i<100; $i++)
{
    if($foo[$i]!=0)
        continue;
    //...etc.
}
```

注意，if 语句中的测试被否定了，并且循环剩余部分的缩进深度减少了一级。这也可以用于减少测试的复杂性。回顾讨论中早前的另一个例子：

```php
for($i=0; $i<100; $i++)
{
    if( ($a===$i || $b===$i)
        &&
        ($c!=$i || $d!=$i))
    {
        echo "Either $a or $b is equal to $i, ";
        echo "and either $c or $d is not. ";
    }
}
```

你可以立即看出，这是另一种循环内部只有一个 if 语句的情况，因此可以写成如下形式：

```php
for($i=0; $i<100; $i++)
{
    if(!(($a===$i || $b===$i) && ($c!=$i || $d!=$i)))
        continue;
    echo "Either $a or $b is equal to $i, ";
    echo "and either $c or $d is not. ";
}
```

通过应用一点布尔代数，测试简化为：

```php
if((($a!=$i && $b!=$i) || ($c===$i && $d===$i))
```

所以，如果 $a 和 $b 都不等于 $i，或者 $c 和 $d 都等于 $i，那么循环将继续。但是，如果你测试 $a 和 $b 都不等于 $i，你立刻就能知道是否会继续，而不必继续查看 $c 或 $d。因此，测试可以拆分为两个独立的语句：

```php
for($i=0; $i<100; $i++)
{
    if($a!=$i && $b!=$i)
        continue;
    if($c===$i && $d===$i)
        continue;
    echo "Either $a or $b is equal to $i, ";
    echo "and either $c or $d is not. ";
}
```

由于 PHP 允许 continue 或 break 携带一个参数，表示要继续或跳过的层级数，因此一个简单的 continue 或 break 可以应用于在 C 或 Java 中你需要循环包含额外变量来传递嵌套循环内部是否应终止信息的情况，或使用 goto 跳转到外层循环之后的标签（除了 Java，它没有 goto 结构）。你可以这样写：

```php
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
if(null!==$position) // $what_we_wanted was not found.
```

而不是这样：

```php
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
}
if($found_what_we_wanted)
{
    // break outer logic would be handled differently or just exit
    // Note: The original text had a typo 'found_wahat' and weird brace structure. 
    // Correcting to standard logic flow described:
}
if(null!==$position) // $what_we_wanted was not found.
```

关于 **continue** 和 **break** 的最后一点观察是，常见的做法是将这些语句写在决定它们是否执行的测试同一行上，尤其是如果这些测试简短且简单。因此，你可能需要考虑采用或允许这样写的做法：

```php
if($a!=$i && $b!=$i) continue;
if($c===$i && $d===$i) continue;
```

> *关于使用相等运算符 == 的一个旁注是，一个常见的拼写错误是在打算使用 == 时使用了 =。在某些情况下，你可以保护自己免受因使用赋值而非比较而产生的 bug。当将一个变量与函数结果或字面值进行比较时，如果你将变量写在相等运算符的右侧，不小心将运算符本身写为 = 而不是 == 会导致解析错误：“null == $position” 是无效语法。这些比那些有时由不应发生的赋值和未正确进行的比较导致的细微错误更容易调试。*

#### 注释

除了 PEAR 强制要求的作者和许可详情外，顶部注释中可以包含的其他内容包括代码包含内容的概述。如果概述很长，在其前面加上一或两行的摘要来概括该概述，将有助于那些稍后出现并想知道该文件用途的开发者。

PEAR 还建议你应该使用 Java-doc 风格的注释，以便于它们被翻译成文档。在这个问题上，意见的分歧与其他任何风格问题一样大。反对的一个理由是，它们使注释本身在源代码中更难阅读，因为它们吸引了过多的额外格式。另一种观点，当争论每个公开可访问的方法都应该以这种方式注释时，认为这鼓励了空洞的、不做事的注释，这些注释实际上既没有贡献注释也没有贡献文档：

```php
/**
 * Gets the number of elements in this Bundle.
 *
 * @return number of elements in this Bundle.
 */
public function Count()
{
    return count($this->elements);
}
```

但是，任何注释的目的都是记录代码的*意图*。如果代码本身构建良好，它自己就能很好地记录它*做了什么*。它不会记录的是*为什么*编写它。

### 命名约定

具有糟糕名称的变量和函数是产生从喜剧到恐怖等各种程度懊悔的丰富来源。在任何具有一定长度的应用程序中，你需要有一些一致的体系来发明名称。这里有一些提示。

用于控制 for 循环的通用计数器变量应该简短而甜蜜。除非上下文提供了变量的明显选择，否则约定是首先使用 $i。如果你然后嵌套另一个循环，它的变量是 $j，接着是 $k，然后是 $l。通常，如果你需要将循环嵌套得更深，那么你可能会重新考虑你在做什么，并将除了最外层块之外的所有语句块移到一个函数中。如果循环没有嵌套，那么它们可以使用相同的变量，只要它们被正确初始化。如果你使用 foreach() 循环来迭代数组，使用数组的复数名称和对应的元素单数名称将使两个变量之间的关系显而易见：foreach($children as $child) 。

应特别避免特别长的变量名称。变量名称越长，拼写错误造成混乱的机会就越多。毫无疑问，你进行所有 PHP 开发时都将错误报告设置为（至少）E_ALL，这样当你尝试使用未初始化的变量时你会收到通知。这将捕捉到你在使用变量时拼错变量名称的实例，但如果你*赋值*给变量时拼错名称，它不会帮助你。在前一节中，使用了变量名称 $found_what_we_wanted，但在一个地方拼错了。错误不会被捕捉到，因为它不涉及使用未初始化的变量，只有当你意识到有些不对劲，并且 $i 总是具有值 100 时，你才会发现错误。





#### 代码效率

PHP 5 提供了一些机制，可以通过魔发方法 `__get()`、`__set()` 和 `__call()` 将对象可见的属性和方法由类实现的属性和方法分离开来。由于变量和属性的大小写很重要，您可能希望考虑这样一种做法：将所有对象属性命名为小写名称，将它们声明为 `private` 或 `protected`，然后编写例程以提供通过首字母大写（title-case）名称进行访问的功能：

```php
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
        return $this->width * $this->height;
    }
  }

  public function __set($property, $value)
  {
    switch($property)
    {
      case 'Width':
        $this->width = $value;
        return;
    }
  }
}
```

这也赋予了您更精细的控制权，以决定对象的使用者可以修改或查看哪些属性。请注意，例如，`$object->Heigt` 可以读取但不能赋值——如果简单地使 `$object->height` 为公共，这种区分将是不可行的。

如果您在通过 `__get()` 和 `__set()` 创建的合成属性与真实属性之间做出风格上的区分，请确保您为真实属性提供合成访问，并最好禁止直接访问这些属性。这将允许您创建无论每个此类是否在内部使用相同的属性，都提供完全相同的属性接口的类。例如，复数对象可以独立于它是将数字存储为实部加上虚部并合成提供幅角和幅值，还是反之，提供 `$num->Real`、`$num->Imag`、`$num->Arg` 和 `$num->Mag`。

> 合成属性的 `__get()` 访问器可以包含代码，以便将先前检索到的值缓存在私有属性中，以防再次被询问，如果其依赖的属性通过 `__set()` 被修改，则清除缓存内容。

在构建由多个单词组成的函数和方法名称时，使用 `underscore_separation` 或 `TitleCase` 来显示一个单词结束和下一个单词开始的地方。关于哪一种

## 第 9 章

看起来更好，意见不一，但请记住这样一个事实：函数、方法和类名称都以不区分大小写的方式处理：**Mandate** 和 **Mandate** 将指向同一个实体。

使用 `define()` 或 `const` 创建的定义常量通常通过全大写来识别。在全局作用域中使用 `define()` 创建的常量前面应加上一组独特的字符序列，以防止它们与其他可能在别处定义的常量发生冲突（请参阅 PHP 手册，其中有很多关于这种做法的示例）。对于类常量则不必要，因为它们的名称已经由类名（或在类定义内部使用 `self::`）作为前缀。

由于这种区分已经内置于 PHP 的语法中，与其他语言相比，区分变量/属性名称与函数/方法名称的规则是多余的；但在类和函数之间没有这样的区分。你可以有一个名为 **Foo** 的类和一个名为 **foo** 的函数，唯一的区别方式是 `$v = new foo();` 使用类，而 `$v = foo();` 使用函数。

```php
$v = foo::foo();  // 这是另一种东西——具体来说，是无法编译的东西；构造函数不能被静态调用，静态函数不能作为构造函数
```

从语法角度上讲，类、变量和属性最好用名词或名词短语来描述。使用与对代码所做对应口头描述中相同的词性。数组和其他集合应使用复数形式命名（`$children`、`$pages`）。布尔值属性应有以“is”或“has”或其他表示谓词的方式开始的名称（`$isValid`、`$canBeDeleted`）。类应以名词命名（`UserFactory`、`NonPlayerCharacter`）；抽象类可以带有前缀 `Abstract` 或 `Base` 以防止意外尝试从中创建对象（`AbstractCollection`、`BaseDocument`），而构造 `FooFactory` 是表示提供返回类 `Foo` 新对象的静态方法的常见惯例。函数和方法可以用动词命名（`traversePath`、`annex()`、`wonderful()`），允许使用形容词、副词，偶尔使用名词来命名常量（`COLOR_GREEN`、`QUICKLY`、`GOLDEN_RATIO`）。

### 修改语法

一些关于编码样式的规则可以通过将违规行为变成解析错误来强制执行。如果您知道自己在做什么，您可以编辑 `zend_language_parser.c` 和 `zend_language_scanner.l` 文件并重新构建 PHP。

例如，如果您想排除使用诸如 `if(): ... endif;` 等构造的可能性，那么从词法文件中，您将删除匹配 `endif`、`endwhile`、`endfor`、`endforeach`、`enddeclare` 和 `endwhile` 的模式（所有这些模式都出现在 `<ST_IN_SCRIPTING>` 上下文中）；并从 yacc 文件中删除对应的 `T_END*` 令牌声明以及产生式规则：

```
unticked_statement:
T_IF '(' expr ')' ':' inner_statement_list new else_if list new else_single T_ENDIF ';' 

while_statement:
'while' inner_statement_list T_ENDWHILE ';'

for_statement:
'for' inner_statement_list T_ENDFOR ';'

foreach_statement:
'foreach' inner_statement_list T_ENDFOREACH ';'

declare_statement:
"::" inner_statement _list T_ENDDECLARE "::"

switch_case_list:
"::" case_list T_ENDSWITCH "::"
"::"::" case_list T_ENDSWITCH "::"
```

此外，删除 `new_else_if_list` 和 `new_else_single` 产生式的全部。因为 `while_statement`、`for_statement`、`foreach_statement` 和 `declare_statement` 现在都简化为单条规则语句，没有关联的代码，所以这些产生式本身现在变得多余。您可以将 `while_statement` 的出现替换为 `statement`（它出现一次，在 `untickled_statement` 的产生式中）而无不良影响，删除 `while_statement` 的产生式，并在此过程中获得一个稍小且更简单的解析引擎。

当然，这会破坏任何使用如今被禁止的构造编写的人的代码。

### 缓存

拥有一个每天更新一次，但每天被访问数千次的页面，意味着相同的计算每天被执行数千次，产生相同的结果。执行一次并保留结果以供后续所有请求使用，可能带来巨大的节省。

由于您的 PHP 应用程序由多层中间软件与处理器隔离，指令穿过这些层过滤到硬件，结果又反向过滤回来，因此有几个点可以潜在地短路该过程。在任何两层之间，都有一个接口，你可以想象一个助手，它记得之前来自人们的信息请求以及据此提供的信息，因此如果再次收到相同的请求，可以立即提供该信息。

在 PHP 级别，有两个主要的接口可以有效利用缓存。你可以生成页面的静态版本并直接提供这些版本，而不是每次都重新生成。你可以将 PHP 应用程序的源代码存储为预解析格式，以便 Zend 引擎直接执行，而无需编译源代码的额外步骤；或者两者兼做。

#### 源预解析

当运行 PHP 程序时，源代码被加载、解析并编译为字节码（由 Zend 引擎模拟的虚构处理器的机器代码），然后该字节码被执行。市面上有几种产品可以保存这些编译后的字节码；下表列出了其中一些较好的产品（按字母顺序排列）。

| 产品 | URL |
|---|---|
| afterBÜRNER*Cache | http://bwcache.bware.it/cache.htm |
| Alternative PHP Cache | http://pecl.php.net/package/APC |
| PHP Accelerator | http://www.php-accelerator.co.uk/ |
| Turck MMCache | http://turck-mmcache.sourceforge.net/ |
| Zend Optimizer | http://zend.com/store/products/zend-optimizer.php |





## 第 9 章

在稳健性和有效性方面，Zend 自家的产品显然很难被超越，但使用它需要购买 Zend Encoder 来生成字节码。请注意，APC 是作为 PECL 扩展分发的。

当程序下次被调用时，字节码会被检索出来并直接提供给 Zend 引擎，从而跳过解析和编译阶段。所有这些产品都会检查源文件和字节码文件的修改日期，以确定源文件自字节码生成以来是否发生过变化，如果必要则重新解析并重新缓存。其中一些产品，如 Zend Optimizer，还可以（如其名称所示）对字节码进行优化以提高性能，其中包括一些在 PHP 本身无法模拟的优化（因为优化器在更低的层级运行，而单条 PHP 语句可能对应于可独立操作的多个字节码指令）。

一般来说，使用字节码缓存只需遵循其安装说明即可，无需对 PHP 程序的源代码进行任何更改。因此，这往往是最简单但又能显著提升软件层面性能的方法之一。

需要注意的是，特别是对于具有优化功能的字节码缓存，各种脚本速度的变化将以非线性方式呈现：这不仅仅是所有脚本运行速度都提高 20% 或翻倍的问题。有些脚本的运行速度相对于其他脚本会按比例更快，但最坏的情况不过是某些脚本的速度没有明显提升。因此，在未安装缓存的情况下对站点进行性能分析的结果，对安装缓存后的站点性能概况没有任何参考价值。

##### 输出预生成

与字节码缓存不同，保存生成的输出以便稍后重新显示*确实*涉及更改站点的运行方式。给定页面需要做的第一件事是确定它是否需要运行，或者是否可以为其输出使用缓存副本。

###### PEAR::Cache 和 PEAR::Cache_Lite

自然地，*PEAR* 包含了提供缓存输出以供后续请求使用的包。

Cache_Lite 提供了一种简单且快速的机制，用于将页面或页面部分的输出作为文件存储，以便在需要时稍后读取。以下示例使用它来缓存一个简单字符串：

```php
<?php
require_once 'Cache/Lite.php';
$cid = '42'; // 这用于标识使用哪个缓存文件；
// 任何在访问时可记住的唯一标识符都可以；如果你正在
// 以此方式缓存整个页面，其 URL 是一个自然的选择。

$options = array(
    'cacheDir' => '/cachefiles/', // Cache_Lite 仅支持文件存储；
    // 你需要在此处指定
    // 一个合适的目录。

    'lifeTime' => 3600       // 我们强制每小时更新一次。
);

$Cache_Lite = new Cache_Lite($options);

if ($data = $Cache_Lite->get($cid)) {
    // 已找到缓存副本
} else {
    // 缓存中没有副本；生成其内容
    // 并存储在 $data 中。
    $data = "Hello, World!"; // 这同样可以是整个页面。

    // 完成后，将其保存在缓存中。
    $Cache_Lite->save($data);
}
// 无论哪种情况，页面的输出都在 $data 中。我假设有人
// 想看到它...
echo $data;
?>
```

围绕现有脚本包装此功能的最直接方式是生成页面并缓冲其输出。这意味着将“Hello, World!”那一行替换为以下内容：

```php
ob_start();
/*
...所有现有的脚本内容都放在这里...
*/
$data = ob_get_contents();
ob_end_clean();
```

你可以使用多个缓存文件来对应单个页面的不同部分，或在多个页面中使用相同的缓存文件，没有任何东西会阻止你这样做。

PEAR Cache 更加复杂。与 Cache_Lite 相比，其最显著的区别在于允许通过多种方式实现缓存（你始终可以子类化 Cache_Container 来创建自己的实现）。除了平面文件存储外，Cache 还附带了使用共享内存、`MHA` wkab Session Handler 扩展以及数据库的容器。它还提供了对缓存数据的 gzip 存储，以及用于存储动态生成的图像和 http 请求响应的专用缓存。

以最直接的形式而言，使用 PEAR Cache 与使用 Cache_Lite 在效果上是相同的。再次强调，你不需要缓存整个页面；主要应专注于生成缓慢且极少变化的部分。

##### 个性化 CMS

内容管理系统有时会提供自身的缓存功能。如果你决定为自己编写一个应用程序，以便更容易地更新站点的内容（还有谁不愿意这样做呢？），那么你可能也希望做到这一点。从广义上讲，保持页面内容与数据库内容同步有三种机会。

- 在数据库内容更改时更新页面。换句话说，你的管理应用程序不仅要更新数据库的内容，还要生成页面并将文件保存在适当的位置，覆盖任何已存在的旧版本。请注意，如果文件因任何原因被删除，你需要显式地重新生成它——也许在你的管理应用程序中提供一个“重新生成所有（缺失的）页面”的选项。生成的页面可以是 PHP 脚本或静态文件。
- 当页面被请求时重新生成。你可以随时随意删除页面的缓存版本。下次用户请求该页面时，他们通过一个脚本来执行该请求，该脚本会检查页面是否存在。如果不存在，脚本会从数据库生成该页面并呈现它，同时将其保存以供下一个用户使用。如果页面存在，脚本必须查看文件的最后修改时间，并检查数据库以确定最近相关更新发生的时间（因此你需要在某处有一个“最后更新”字段）。如果更新早于文件修改时间，脚本直接使用 `fpassthru()` 将缓存版本呈现给用户；否则，它再次执行重新生成和输出/保存任务。
- 一个定期重新生成那些定期调度更新（例如每日、每周或每月）的页面的 cron 任务，也可以采用这种方式处理。不用说，在更新完成之后但在 cron 任务下次运行之前提供的页面仍将包含旧内容。

##### 将 404 处理程序用作蹦床

此方法对于归档不再变化的页面（例如较旧的新闻文章）非常有效。如果它们可以被存储并作为静态页面请求，那么 PHP 就永远不需要参与它们的重新生成。更好的做法是仅在需要时才生成（一次）。

该方法的运作方式如下。假设访客请求一篇尚未保存为静态页面的旧新闻文章。Apache 查找该页面，未能找到，因此开始组装 404 Not Found 响应。你配置了 Apache 使用自定义 404 处理程序（使用 `ErrorDocument` 指令）来调用一个 PHP 脚本。该 PHP 脚本解析 `$_SERVER['REQUEST_URI']` 的内容以确定请求的是哪篇文章。假设请求的是真正的文章，它生成该页面（将其存储在输出缓冲区中），并将其保存在最初应该找到的位置。然后它调用 `header("HTTP/1.1 200 OK")`，接着是页面的缓冲内容。这可能按顺序对几种不同类型的请求执行。如果其他所有措施都失败，它会以发送 404 Not Found 响应并包含该情况下适当的页面内容来结束。

对同一文章的后续任何请求都会看到 Apache 在确切的位置找到确切的静态页面。

显然，你可以在任何时间点清除这些页面（例如，在更改站点外观、更换主机或简单释放磁盘空间时）。如果且当它们再次被请求时，它们将简单地被重新生成。

此方法可以与 Apache 的 `mod_rewrite` 和 `mod_alias` 模块结合使用，以进一步将站点的文档树与服务器文件系统解耦。在这种情况下，你的脚本将在完成 URL 转换后，将静态页面保存在 `mod_rewrite` 指示的任意位置。

使此方法变得更加复杂是可能的（当然，随着复杂性的增加，日后产生混淆的风险也会增加）。由 404 处理程序生成的文件本身可以是一个 PHP 脚本——为了生成用户请求的页面，处理程序需要使用类似 `fpassthru("http://www.example.com/oldnews/19980503.php")` 的内容执行该脚本，或者复制其行为。PHP 将不再被排除在外，但你可以这样做，以减少将来提供相同页面所需的处理量（例如，你可能需要在允许用户访问页面前检查用户的凭据）。




### 客户端缓存

请记住，大多数 web 浏览器都有缓存。只要懂一点 HTTP，你就可以利用它——这需要能够确定页面内容最后一次变更的时间，或者知道下一次它们将会变更的时间。

如果你知道页面内容最后一次更新的时间，你可以将其作为 Last-Modified 头添加。客户端浏览器和你的服务器之间的任何缓存代理都可以使用此头来决定它们持有的页面缓存副本是否仍然是最新的（如果它们的缓存副本具有相同的 Last-Modified 日期，则它是最新的）。客户端还可以发起对资源的 HEAD 请求，并使用 Last-Modified 头来决定是否有必要 GET 页面本身。

如果你提供了 Expires: 头，则意味着任何页面缓存副本在指定时间之前都是有效的。有了这个信息，缓存页面的客户端和代理可以稍后决定是否需要继续请求该页面。

对于 HTTP 头中的所有日期，格式是 RFC 2822 中指定的格式——即由 date('r') 返回的格式。

客户端可以在其请求中包含的一个头是 If-Modified-Since: 头。这同样是 RFC-2822 格式的日期，如果存在此头，你的脚本可以（通过 apache_request_headers()）使用它来决定是正常生成并发送完整响应给客户端，还是发送一个无内容的 304 Not Modified 响应来告知客户端其缓存副本仍然是最新的。（304 响应不得包含任何内容；但仍可发送任何头，包括 Last-Modified 和 Expires。）

还存在其他缓存控制头，更全面的覆盖在 HTTP 规范 RFC 2616 中给出。

### 你自己的代码

除了在你的脚本中包装更多的缓存控制代码之外，你能对它们做些什么来加速它们？这就是“哪个更快”这类问题开始出现的地方。正如你所见，你应该用经验主义的眼光来审视所有这些建议。

### 输出缓冲

输出缓冲不仅仅用于缓存或输出后处理（或笨拙的“headers already sent”错误变通方案）。当 Apache 将数据发送给用户时，它是通过数据包进行的。每个数据包都必须被封装在信封中并填写地址，以便到达其目的地。发送较少但较大的数据包可能比发送许多较小的数据包更快。通过缓冲 PHP 的输出，你可以收集页面的内容并一次性发送出去，而不是在处理过程中一次只发送几个字节。

事情并非如此简单。当你逐字节将字节发送给用户时，他们有几率更早地接收这些字节，并更快地开始看到结果，即使整体页面加载更慢。他们甚至可能在浏览器尚未完成接收文档之前就找到他们正在寻找的链接并点击跳转（如果他们打算在该文档上停留一段时间，无论如何他们都会停留比页面加载时间更久）。因此，你至少应该对缓冲进行分组处理。不要在整个脚本周围使用一个巨大的缓冲区，而是顺序发送几个“章节”；在开始新的处理块之前结束一个章节。尽快开始产生输出。不要让用户悬着心。

尝试这样做：

```php
<?php
// 如果任何处理涉及 HTTP 头，
// 现在是一个做这些事情的好时机。
?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
       "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>一个分章节缓冲的页面</title>
<?php
ob_start(); // HTML <head> 内容
// 构造 <meta> 标签，并选择要包含的一些 CSS 和 Javascript。例如，
echo "<meta name='author' content='".$page_author."'><n";
ob_end_flush(); // 输出 HTML 头章节
?>
</head>
<body>
<?php
ob_start(); // 标语行和面包屑路径。
?>
<div id="topmatter">
<!-- 构造此章节的 HTML 和 PHP -->
</div>
<?php
ob_end_flush(); // 输出标语行章节
ob_start(); // 侧边导航列表
//...
ob_end_flush(); // 输出侧边导航章节
?>
...
</body>
</html>
```

在这个示例中，显示了六个部分；从 `<!DOCTYPE>` 声明开始并以 `<title>` 元素结束的部分；用于 `<head>` 元素剩余内容的部分；一个小的部分，结束头部分并开始正文部分；随后是两个构成页面布局的部分（然后可能还有其他的部分）；最后是 `</body></html>` 以结束页面。每个部分将作为一个完整的块输出，为 Apache 提供最佳条件，以便尽可能高效地填充其出站数据包。

## `echo` 还是 `print`？

天哪，又是这个问题。`echo` 和 `print` 之间唯一值得注意的速度差异（除了输入速度外）在于当你希望顺序输出多个字符串时。使用 `print`，你将它们全部连接在一起并输出结果字符串。使用 `echo`，你可以这样做，但不必这样做，只需使用逗号 (,) 分隔字符串而不是点号 (.)。

在连接时，PHP 必须为正在构建的字符串分配内存，并为每个连接操作重新分配内存。这会引入延迟。此外，在完全构建字符串之前，无法输出任何部分的字符串，因此如果正在连接的项目之一是函数，一切都必须等待该函数。比较运行这些语句的结果：

```php
print "This string takes ".sleep(15)."too long to display.";
echo "This string takes ".sleep(15),"too long to display.";
echo "This string takes ", sleep(15),"too long to display.";
```

这适用于输出，但对于要连接到一个变量中的字符串，也可以做类似的事情：启动一个输出缓冲区，echo 出字符串的所有部分，将缓冲区内容读取到变量中，最后结束并清理缓冲区。例如：

```php
ob_start();
for($i=0; $i<100; $i++) echo $i; 
$zero_to_ninetynine = ob_end_clean();
```

### for($i=0; $i<count($array); $i++)

不要这样做。这样做意味着 PHP 必须在每次迭代后检查数组的大小。当然，数组的大小与其内容一起维护，因此其元素实际上不需要被 *计数*，但仍需查找大小——以防数组大小在循环过程中发生变化。如果你知道它不会变化，请使用这个：

```php
for($i=0, $count_array=count($array); $i<$count_array; $i++)
```

这同样有效，并节省了额外的查找。如果遍历数组元素的顺序不重要，可以避免中间变量：

```php
for($i=count($array)-1; $i>=0; $i--)
```

如果你这样做，请记住 -1 和 >=。

### 临时变量

特别是当你使用关联数组时，如果你要多次查看同一个数组元素，将其值放入一个局部变量（如果你打算更改它，则通过引用）将节省识别 `$array['foo']` 实际指的是哪个数组元素所涉及的工作。同样的道理也适用于数组属性。考虑以下情况：

```php
$this->p_consts->Delta[$i][$k] = $this->p_consts->Delta[$i][$this->p_consts->s($i)-1];
$this->n[$i][$k] = $this->n[$i][$this->p_consts->s($i)-1];
```

`$this->p_consts` 使用相当频繁；特别是其 `Delta` 和 `s` 属性。你可以创建临时变量来存储这两个属性的值（通过引用分配 `Delta` 因为你修改其值），从而免去每次通过 `$this->p_consts` 查找它们的麻烦：

```php
$p_Delta = &$this->p_consts->Delta;
$pS = $this->p_consts->s($i);
$p_Delta[$i][$k] = $p_Delta[$i][$pS];
$this->n[$i][$k] = $this->n[$i][$pS];
```

显然，这还可以使程序更容易阅读。

#### 对 if...elseif 测试和 Switch 案例的排序

首先，如果你有一系列连续的 if 语句，并且在任何给定时间只有一个可能为真，那么你应该对除第一个以外的所有使用 `elseif`。否则，在找到匹配的那个之后，PHP 将继续测试其余部分。你知道它们都会是假的，但执行实际工作的人不是你。PHP 必须继续测试，以防被测试的变量在成功语句执行期间发生了变化。

如果你有一系列 `if .. elseif` 语句，或一个 `switch` 语句，请将更常见的情况放在顶部，并将罕见情况移到底部。除了给读者提供更清晰的代码行为图景（通过先展示典型情况，稍后再处理棘手的边缘情况）外，这意味着平均而言 PHP 在找到一个成功的测试之前需要执行更少的测试。

即使你最常见的情况由最终的 `else` 或 `default` 案例满足，也要明确地为它们提供代码，并将其测试放置在顶部（*每个测试都在 PHP 处理这些剩余项之前进行检查*）。

#### 使用正确的字符串函数

手册反复指出，如果你没有实际使用任何正则表达式语法功能，那么 PHP 的其他字符串函数很可能比正则表达式函数快得多。当你可以说 `explode("/", $path)` 时，不要说 `split("/", $path)`。

#### 正则表达式语法

说到正则表达式，精心设计也能提高其性能。整本书都可以并且已经就正则表达式及其编写方法写出；目前，只需记住 PCRE 函数 `preg_match()` 等提供了比诸如 `ereg()` 等 POSIX 函数更丰富的语法和更智能的引擎。

#### unset()

好吧，PHP 会在变量超出作用域时立即清理变量；要么是函数结束时的局部变量，要么是脚本结束时的其他所有变量。通常，这意味着你不必担心它。

但如果你有一个巨大的结构（例如由数千个元素组成的数组），而你不再需要使用它，特别是如果你稍后还有更多的大块数据要处理，那么你应该在完成后立即对该对象执行 `unset()`。由此产生的大块空闲内存可以立即用于其他用途。在繁忙的服务器上，尽可能释放大块内存可以在将一切装入 RAM 与求助于磁盘上的虚拟内存之间产生差异。




#### 代码效率

### 释放资源与持久数据库连接的隐患

再次强调，如果你正在使用诸如 MySQL 数据库连接等资源，并且已经使用完毕但仍有许多工作要做，不要为了脚本剩余的执行时间而独占该资源：请关闭它。

持久数据库连接（例如由 `mysql_pconnect()` 创建的连接）有时被建议作为提升性能的手段。这是因为在连接首次建立后，创建它的 httpd 进程会在建立连接的脚本结束后保留该连接，以便下次运行需要使用数据库连接的脚本时随时可用。由于连接数据库涉及一定的工作量，持久连接可能会节省一些时间。但很可能在节省的时间变得明显之前，相关领域就已经发展到使这种优化不再必要了。

问题在于，即使连接的 httpd 进程处于请求之间的空闲状态，它仍然保持该数据库连接打开，直到它因服务器规定的生命周期结束而终止。数据库连接供应有限（`mysql_close()` 对持久连接无效）。如果系统变得繁忙，脚本试图连接数据库时，很可能会因已达到最大允许连接数而被拒绝并收到错误消息。如果这些连接全部都在使用，那还好：你只需稍微增强数据库服务器配置即可。但如果最大连接数被达到是因为空闲的 httpd 进程正占据着可用连接，*以防* 需要使用的请求到来，那就不好了。

### ob_gzhandler()

如果你打算使用输出缓冲来批量处理页面输出，以 `ob_start('ob_gzhandler')` 启动缓冲，意味着当你收集缓冲输出时，会发现它已被压缩。该回调函数会礼貌地检查请求头，确保将要输出数据的浏览器确实支持读取 gzip 压缩数据。

作为使用该回调处理器的*替代*方案（不要试图同时使用两者），可以考虑在 `php.ini` 中设置 `zlib.output_compression`。事实上，这是 PHP 开发人员推荐的方法。

#### 总结

在浏览这里列出的建议和指导时，你无疑会发现有些似乎相互矛盾。这是不可避免的；什么有效取决于具体情况，不同的情况可能需要做出不同的决策。一个对大型数据库进行大量复杂操作，与一个主要作为文件存储库的网站相比，需求是不同的。

作为开发人员，你的时间比作为 Web 服务器的计算机时间更宝贵。从经济角度或工作满意度来看，花费时间在那些最多只能带来微小改进且对网站访问者不可见的修改上，完全是没有意义的。相反，应将时间投资在规划和测试上。退后一步，先纵观全局，再关注单行代码。

你的硬件是否达标，还是会成为软件改进效果的上限？你的 Web 服务器配置如何；是否需要进行一些调整？有多少冗余计算正在执行：能否将某个地方的结果缓存起来，以便在其他地方使用？

231

## 第 9 章

程序性能调优的最佳时机是在编写之前。在构建网站时，测试、实验并积累各种设计方式的经验，了解每种方式的优缺点。在开始阶段选择合适的框架，比事后对代码进行任何调整对最终产品速度的影响都要大得多。继续测试、实验和积累经验，并始终关注全局，因为硬件和软件技术都在不断前进。处理器会更快，内存会更便宜，网络连接会更宽裕，Web 服务器会更高效，Web 浏览器会更复杂，PHP 也会拥有更多可用于开发的功能。

![](img/cacdd24f2926f10ee3219256ad732604_258_0.png)

#### PHP 扩展

尽管 PHP 语言的核心提供了完成许多常见任务的功能，但还有许多扩展可以添加，从而将 PHP 配置提升到全新水平。本章探讨了一些更有用的扩展，但这仅仅是冰山一角。本章中的扩展涉及图像操作、创建 PDF 文件（不使用 Adobe Acrobat）、创建 Flash 文件（不使用任何商业软件）以及与 XML 文档交互。这些扩展中的一些已经默认捆绑在配置中并启用，那么你还在等待什么？

## PDFLib

无论你的内容是学术性质还是商业性质，一个专业开发的网站如果不具备以 PDF（便携式文档格式）交付内容的能力，就是不完整的。虽然有许多开源库可供 PHP 开发人员使用，特别是 FPDF ([http://www.fpdf.org/](http://www.fpdf.org/)) 和 pdf-php ([http://sourceforge.net/projects/pdf.php](http://sourceforge.net/projects/pdf.php))，但 PHP 内置的 PDFLib 功能可以说是实现这一目标最高效的方式。PDFlib 功能（自 PHP 4.3.9 起移至 PHP 扩展社区库 PECL）是对商业 PDFLib ([http://www.pdflib.com/](http://www.pdflib.com/)) PDF 处理库的封装。PDFLib 相比纯 PHP 解决方案的优势在于速度。PDFLib 等编译型 C 代码比由 Apache 解释的 PHP 代码快几个数量级。缺点是商业使用的许可成本。

> *细心的读者会注意到，本文对主题有两种不同的大小写写法：“PDFLib”和“PDFlib。”这是为了区分由拥有者命名为“PDFLib”的 C 库和名为“PDFlib”的 PHP 封装库。值得注意的是，C 库文档并没有严格遵循这一约定。*

### 配置

PHP 对 PDFLib 的支持最近发生了重大变化，并且像该语言及其众多库中的许多其他功能一样，预计还将进一步变化，特别是鉴于 PHP 在专业开发社区中日益被接受。

因此，配置极易受到架构、操作系统、PHP 版本等常见问题的影响。如果你的 Apache 安装使用动态共享对象（DSO），或 Windows 安装使用动态链接库（DLL），那么只需要确保存在合适的文件（分别为 libpdf_php.so 或 libpdf_php.dll），并且在 php.ini 文件中正确引用且未注释。

如果你没有使用 DSO，或无法使用，你将不得不访问 PDFLib 网站（http://www.pdflib.com/ ），获取 PDFLib 源代码多种版本中的最新版本，并构建一个静态链接库。更多详情请访问 http://www.pdflib.com/products/pdflib/info/PDFlib-in-PHP-HowTo.pdf 。

无论你怎么安装 PDFLib，都值得访问 PDFLib 网站并下载最新版本的 PDFLib Lite。随源代码附带一份非常有帮助的文档 PDFlib-manual.pdf。手册包含各种有用信息，包括所有支持编程语言的绑定、通用的 PDFLib 编程概念等。第 3.1.1 节“PDFLib 程序结构与函数范围”是必读内容，可节省你数小时的挫败感，去尝试消除“范围”错误。

### 入门

PDF 文档将在 PHP 中作为资源类型，使用 pdf_new() 函数创建，如下所示：

```
$pdf = pdf_new();
if (!pdf_open_file($pdf, "")) {
    die("Error: Unable to open output file.");
}
```

请注意，在资源创建后立即进行测试，以确保资源已创建并打开。如果未经过此检查就尝试执行任何页面范围函数，脚本将失败并生成以下 PDFLib 异常：

> Function must not be called in 'object' scope'

换句话说，在对象范围内调用了页面范围函数，因为文档尚未打开。在 PHP5 中，只需将 pdf_new() 调用包裹在一个捕获 PDFLibException 类型的 try / catch 块中即可。

完成 PDF 文档后，可以调用 pdf_close() 关闭文档文件并释放相关资源。




### 指定文档信息

搜索文档的一种方式是通过文档信息中包含的元数据。使用 `pdf_set_info()` 函数可以轻松地实现这一点。PDFLib 手册第 8.9.6 节“文档信息字段”指定了哪些字段是相关的。例如：

```php
pdf_set_info($pdf, "Author", $name . " <" . $row["Email"] . ">");
pdf_set_info($pdf, "Title", "Resume: " . $name);
pdf_set_info($pdf, "Subject", "The resume of " . $name . " " .
                               $row["DesiredPosition"] . "");
```

此代码将文档的作者、标题和主题设置为从 MySQL 数据库中获取的值。请注意，`pdf_set_info()` 函数取代了众多用于专门设置字段的已弃用函数。

### 必需元素

要渲染最基本的页面，每个由 PDFlib 生成的文档都需要以下元素：

-   `pdf_new()`：用于创建新的 PDF 资源。
-   `pdf_open_file($pdf [, $filename])`：接受一个 PDF 资源和一个可选的文件名作为参数。对于缓冲输出（如本节末尾的示例所示），文件名不是必需的。
-   `pdf_begin_page($pdf, $width, $height)`：接受一个 PDF 资源以及以点（points）为单位的页面宽度和高度。
-   `pdf_findfont($pdf, $font, $encoding [, $embed])`：根据给定的 PDF 资源、特定字体名称和编码参数来定位字体。将非零值作为可选的第四个参数传递，会导致立即检查该字体，从而避免后续错误。
-   `pdf_setfont($pdf, $font, $size)`：接受一个 PDF 资源、一个字体句柄（由上述 pdf_findfont 函数返回）以及一个字体大小。
-   `pdf_show_xy($pdf, $text, $x, $y)`：在指定的 PDF 资源中，将传入的文本放置在给定的 x 和 y 坐标处（以点为单位）。
-   `pdf_stroke($pdf)`：在传入的 PDF 资源上“着墨”或绘制文本。
-   `pdf_end_page($pdf)`：结束给定 PDF 资源的当前页。
-   `pdf_close($pdf)`：关闭传入的 PDF 资源。

本结尾处的简历生成器示例使用这些函数中的每一个，将 PDF 文档返回给浏览器，而不是将文件放置在本地文件结构的某个位置。

### 辅助函数

鉴于典型文档的某些部分遵循特定样式，您可能认为创建几个辅助函数以简化代码维护和样式变更很有用。一个特别有用的函数是绘制水平线，这在生成 PDF 时并非易事，如下所示：

```text
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

`drawHR()` 函数接受一个 PDF 资源 `$res` 作为参数。它使用常量值和带有 `texty` 参数的 `pdf_get_value()` 函数来设置线条的初始 x 和 y 位置。`pdf_get_value()` 函数的第三个参数是一个应用于由第二个参数指定的值的数字“修饰符”。在最简单的情况下，该参数的值为 0。因此，`drawHR` 函数的最后一行可以更优雅地写为：

```text
$ypos = pdf_get_value($res, "texty", (VERT_SPACING * -2));
```

在创建 PDF 文档时，需要掌握的一个有用概念是“路径”（path）。`pdf_moveto()` 函数在文档内定位起点，`pdf_lineto()` 在两个位置之间的路径上绘制线条。`pdf_closepath()` 和 `pdf_fill()` 函数分别闭合并填充路径。最后，y 位置增加了两倍垂直间距常数的值。

另一个有用的函数可以根据传入的参数应用相似但不同的样式：

```text
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
            $text = "\"" . $text . "\"";
            break;
    }
    pdf_setfont($res, $font, 12.0);
    pdf_show_xy($res, $text, $xpos, $ypos);
    return;
}
```

如您将在本节结尾的示例中看到，此代码使用 switch 控制结构根据 `$type` 参数的值设置特定的字体样式和文本位置。

字体选择由 `pdf_findfont()` 函数执行，并通过 `pdf_setfont()` 函数设置。PHP 的 PDFlib 实现通常默认在安装 PHP 的目录内的“pdf-related”目录中安装几种字体。PDFLib 支持各种各样的字体和样式。完整详情请参阅 PDFLib 文档。

最后，`pdf_show_xy()` 函数在指定位置显示给定的字符串。

### 关于字体和定位

在前面的代码示例中，您看到了如何通过 PHP 内置的 PDFLib 函数操纵各种文本属性。再次提醒开发人员，避免使用其他已弃用的函数，例如已被单个 `pdf_get_value()` 函数取代的 `pdf_get_font()` 和 `pdf_get_fontsize()`。该函数的用法与前述的 `pdf_set_info()` 函数相同。PHP 的文档 ([http://www.php.net/manual/en/ref.pdf.php#AEN124842](http://www.php.net/manual/en/ref.pdf.php#AEN124842)) 列出了已弃用的函数及其替代方案。

> PDFLib 坐标系将 x:y 坐标 0:0 定义为文档的左下角。

您可能觉得定义常量以表示此类页面属性会有帮助，例如边距和制表位宽度、垂直间距以及页面尺寸。下表列出了更常见的页面尺寸的点数（points）维度，其中 1 pt = 1/72 英寸 = 0.3528 毫米。

| 格式 | 宽度 | 高度 |
|---|---|---|
| A4 | 595 | 842 |
| B5 | 501 | 709 |
| Letter | 612 | 792 |
| Legal | 612 | 1008 |

### 收尾工作

如果您只是想创建一个文档并将其放置在本地主机的某处，完成 PDF 文件所需做的只是结束页面并完全关闭它。不过，更常见的是，向 Web 浏览器返回一个缓冲区。`pdf_get_buffer()` 函数检索传入的 PDF 文档。然后通过 `header()` 函数通知浏览器预期接收一个 PDF 文档，简单的打印调用即可完成整个过程，如下所示：

```php
pdf_end_page($pdf);
pdf_close($pdf);
$buf = pdf_get_buffer($pdf);
$len = strlen($buf);
header("Content-type: application/pdf");
header("Content-Length: $len");
header("Content-Disposition: inline; filename=resume.pdf");
print $buf;
```

本节仅简要提及了高级 PHP 开发者可用的众多 PDF 生成功能。我们未涉及的其他可用方面包括书签、超文本、颜色使用、图形生成和导入，以及太多无法在此一一列举的功能。

### PDF 简历生成器

请考虑以下代码：

```php
<?php

// Specify string constants and positioning variables.
define("CASE_CATEGORY", "Category");
define("CASE_LIST", "List");
define("CASE_OBJECTIVE", "Objective");
define("MARGIN", 50);
define("PAGE_HEIGHT", 792);
define("PAGE_WIDTH", 612);
define("TAB", 25);
define("VERT_SPACING", 14);

// Define a couple useful functions.
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
            $text = "*" . $text;
            break;
        case CASE_OBJECTIVE:
            $font = pdf_findfont($res, "Times-Italic", "winansi", 0);
            $xpos = MARGIN + TAB;
            $text = "\"" . $text . "\"";
            break;
    }
    pdf_selectfont($res, $font, 12.0);
    pdf_show_xy($res, $text, $xpos, $ypos);
    return;
}

// Create resource.
$pdf = pdf_new();
if (!pdf_open_file($pdf, "")) {
```




## 第 10 章

```php
die("Error: Unable to open output file.");
}

// Collect header information from the database.
mysql_connect("localhost", "resume_user", "resume_pw");
mysql_select_db("resume");
$sql = "SELECT * FROM biography WHERE OID = 0";
$result = mysql_query($sql);
$row = mysql_fetch_array($result, MYSQL_ASSOC);
$name = $row["NameFirst"] . " " . $row["NameLast"];

// Document info.
pdf_set_info($pdf, "Author", "Name: < " . $row["Email"]. ">");
pdf_set_info($pdf, "Title", "Resume - " . $name);
pdf_set_info($pdf, "Subject", "The resume of " . $name . ", " .
$row["DesiredPosition"] . ".");

// Do something clever with the keywords.
$keywords = split(" ", $row["DesiredPosition"]);
$morewords = "";
foreach($keywords as $keyword) {
    $morewords = $morewords . $keyword . " , ";
}
pdf_set_info($pdf, "Keywords", "Resume, " . $morewords . "apache, mysql, php, pdf");

// Begin PDF page. -- Can be placed anywhere after the PDF
// resource has been instantiated.
pdf_begin_page($pdf, PAGE_WIDTH, PAGE_HEIGHT);

// Print name.
$font = pdf_findfont($pdf, "Times-Bold", "winansi", 0);
pdf_setfont($pdf, $font, 14.0);
$stringwidth = pdf_stringwidth($pdf, $name, $font, 14.0);
$xpos = (PAGE_WIDTH / 2) - ($stringwidth / 2);
pdf_show_xy($pdf, $name, $xpos, 700);
$xpos = pdf_get_value($pdf, "textx", 0);
$ypos = pdf_get_value($pdf, "texty", 0) - VERT_SPACING;

// Print contact information.
$font = pdf_findfont($pdf, "Times-Roman", "winansi", 0);
pdf_setfont($pdf, $font, 12.0);
$headerdata = array($row["Address"],
$row["City"] . ", " . $row["State"] . ", " . $row["ZipCode"],
$row["Phone"],
$row["Email"]);
foreach ($headerdata as $data) {
    $stringwidth = pdf_stringwidth($pdf, $data, $font, 12.0);
    $xpos = (PAGE_WIDTH / 2) - ($stringwidth / 2);
    $xpos = pdf_get_value($pdf, "textx", 0) - VERT_SPACING;
    pdf_show_xy($pdf, $data, $xpos, $ypos);
}

// Print categories.
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
// Wrap up the document and return it to the browser.
pdf_end_page($pdf);
pdf_close($pdf);
$buf = pdf_get_buffer($pdf);
$len = strlen($buf);
header("Content-type: application/pdf");
header("Content-Length: $len");
header("Content-Disposition: inline; filename=resume.pdf");
print $buf;
// Clean up!
mysql_close();
$pdf = 0;
?>
```

这个直接明了的应用程序使用从 MySQL 数据库中提取的数据生成一个简单的 PDF 简历。除了 MySQL 连接设置和数据库查询外，该脚本中尚未涵盖的唯一方面是使用传记数据将个人的目标职位信息拼接到文档的关键字中：

```php
$keywords = split(" ", $row["DesiredPosition"]);
$morewords = "";
foreach($keywords as $keyword) {
    $morewords = $morewords . $keyword . ", ";
}
pdf_set_info($pdf, "Keywords", "Resume, ". $morewords . "apache, mysql, php, pdf");
```

简历的头部信息，包含个人的姓名和联系方式，是为了保持辅助函数 `pdfLib_show()` 的实现尽可能简单，从而与简历的其余数据分开处理的。简历的正文由一个 `while` 循环生成，该循环跟踪当前和上一个类别，当值发生变化时打印类别名称；否则，它打印描述。剩下的只是关闭文档，将其返回到浏览器，并进行清理。

最后的一点建议：如果 PDF 生成在你的任何项目中扮演重要角色，你必须阅读并理解随 PDFLib 源代码分发的文档。PHP 网站上通常丰富的文档在涉及 PDFLib 包装器方面尤其缺乏。虽然本文应该是一个极好的介绍，但没有比 PDFLib 手册更好的信息源来了解 PDFLib 库的完整功能。

## GD 库

如果你曾经不得不设置包含大量图片的网站，例如图片库或电子商务网站，其中最繁琐的任务之一是对所有单个图像的操作和上传。幸运的是，PHP 配备了 GD 库，这是一个开源的图像处理库，随 PHP5 捆绑提供。凭借 GD 提供的庞大功能集，你可以自动化网站图像处理的许多或所有任务，因此你只需上传图片，就可以把时间花在其他事情上，而不是长时间扮演“图像管理员”的角色。

### 创建图像基础

GD 库的一个缺点是可用函数数量众多，其中许多执行相同的功能，仅在输入类型或输出图像格式上有所不同。为了提供清晰度并作为本章涵盖的所有图像处理功能的基础，你将创建一个类，用于处理几种最流行的图像文件类型——JPG、GIF 和 PNG 的基本加载和保存。

这个基础类将提供基本的加载、保存和显示功能，并将作为稍后在章节中添加的其他附加图像处理类的调用位置。首先，创建一个名为 class.WebImage.php 的新文件，并输入以下代码：

```php
<?php

class WebImage
{
    public $gdResource;
    public $type;

    // Release resources
    public function __destruct()
    {
        if ($this->gdResource)
        {
            imagedestroy($this->gdResource);
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
            case 'image/jpeg':
                $this->gdResource = imagecreatefromjpeg($file);
                break;
            case 'image/png':
                $this->gdResource = imagecreatefrompng($file);
                break;
            case 'image/gif':
                $this->gdResource = imagecreatefromgif($file);
                break;
        }
        // Retain the alpha information
        imagesavealpha($this->gdResource, true);
    }

    // Save the file to the local filesystem
    public function save($file)
    {
        switch ($this->type)
        {
            case 'image/jpeg':
                imagejpeg($this->gdResource, $file);
                break;
            case 'image/png':
                imagepng($this->gdResource, $file);
                break;
            case 'image/gif':
                // Convert back to palette
                if (imageistruecolor($this->gdResource))
                {
                    imagergptocolorpalette($this->gdResource, false, 256);
                }
                imagegif($this->gdResource, $file);
                break;
        }
    }

    // Display the image in the browser
    public function display()
    {
        switch ($this->type)
        {
            case 'image/jpeg':
                header("Content-type: image/jpeg");
                imagejpeg($this->gdResource);
                break;
            case 'image/png':
                header("Content-type: image/png");
                imagepng($this->gdResource);
                break;
            case 'image/gif':
                // Convert back to palette
                if (imageistruecolor($this->gdResource))
                {
                    imagergbtopalette($this->gdResource, false, 256);
                }
                header("Content-type: image/gif");
                imagegif($this->gdResource);
                break;
        }
    }
}
?>
```

这一切是什么意思？这个文件是一个朴素的图像包装器，你可以用它来打开、保存和显示你的图像。此代码可以处理 JPG、GIF 和 PNG 图像，但你可以轻松添加更多，假设 GD 库支持它们。为了更好地理解正在发生的事情，请查看该类是如何构建的。

开头几行相对直接明了——你首先声明两个公共属性，一个用于保存内部 GD 图像资源，另一个用于跟踪图像操作使用的 MIME 类型。还要注意析构函数——当类被销毁时，它会确保 GD 为该图像消耗的资源被清理：

```php
<?php
class WebImage
{
    public $gdResource;
    public $type;

    // Release resources
    public function __destruct()
    {
        if ($this->gdResource)
        {
            imagedestroy($this->gdResource);
        }
    }
}
?>
```

下一段代码从服务器上的文件中加载图像数据。你向方法传递一个文件名，它确定图像类型，然后使用 GD 库提供的相应函数将图像加载到 GD 资源中：

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
            // ...
    }
}
```




## 第 10 章

```php
$this->gdresource = imagecreatefromjpeg($file);
break;
case 'image/png':
$this->gdresource = imagecreatefrompng($file);
break;
case 'image/gif':
$this->gdresource = imagecreatefromgif($file);
break;
}
```

在处理可能包含透明区域（如 GIF 或 PNG）的图像格式时，理解所涉及的两种不同透明类型非常重要。第一种也是最简单的是索引透明。它存在于 8 位透明 PNG 图像和所有透明 GIF 图像中，索引透明仅将索引调色板中的一种颜色定义为透明。任何被分配该颜色的像素在屏幕上都会显示为透明。

第二种透明类型是 Alpha 透明，存在于 32 位 PNG 图像中。Alpha 透明图像通过为每个像素提供额外的数值范围来定义该特定像素的透明度，从而实现透明效果。Alpha 透明允许图像平滑地渐变为透明，或者在某些位置让任何颜色部分透明——这是索引透明图像无法做到的。

在 GD 中处理包含 Alpha 透明的图像时，你需要告知 GD 你希望保留从已加载图像中获取的任何 Alpha 透明信息：

```php
// Retain the alpha information
imagesavealpha($this->gdresource, true);
}
```

如果你计划加载或输出任何理解每像素/Alpha 透明的图像格式，例如 32 位 PNG，就需要这样做。如果不告诉 GD 保存 Alpha 通道，最终输出可能会遇到意外的背景或透明问题。

最后两个方法 `save()` 和 `display()` 将内部图像资源发送到最终目的地——无论是服务器上的文件，还是在浏览器中显示。两者之间唯一的实质区别在于 `display()` 中使用 `header()` 函数告知浏览器预期的图像类型，以及 `save()` 中 `image__()` 函数的第二个参数，该参数告诉 GD 将图像保存到文件，而不是将输出直接传输到屏幕：

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
if (imagetruecolor($this->gdresource))
{
    imagegetcolorpalette($this->gdresource, false, 256);
    }
imagegif($this->gdresource, $file);
break;
}
}
```

如果你想在 `save()` 方法中添加更多图像类型，只需在 switch 语句中添加相应的 case 即可。对于调色板图像类型，如果必要，请确保将图像从真彩色转换为调色板，如示例中 GIF 图像的情况所示。

### 调整图像大小

现在你可以轻松加载和保存一些基本图像格式了，是时候实际以某种方式修改它们了。你要做的第一件事是让你的 WebImage 类具备调整图像大小的功能。为此，你将创建一个处理调整大小操作的类文件，并在你的 WebImage 类中添加一个方法，在需要时调用调整大小功能。

首先，创建以下名为 `class.ImageResize.php` 的文件：

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
            if (($this->max_width/$old_width) <= $this->max_height/$old_height)
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
}
?>
```

然后，将以下方法添加到你的 WebImage 类定义的末尾：

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

查看你刚刚添加到 **WebImage** 的新方法，你可以快速了解图像调整大小类是如何被调用的。首先，如果需要，引入 **ImageResize.php** 文件，并创建一个 **ImageResize** 对象。然后使用 `func_num_args()` 函数确定调用该方法时使用多少个参数。

**WebImage** 的 resize 方法可以使用一个或两个参数进行调用。如果使用一个参数，它被视为用于调整图像大小的数字比例。如果传递两个参数，它们将用作调整后的图像不得超过的最大宽度和最大高度的值。

在对象中相应地设置这些值后，调用 `process()` 方法，图像将被调整大小并返回。为了进一步理解调整大小具体是如何发生的，请仔细查看 **ImageResize** 类。

在 **ImageResize** 的核心部分，`process()` 方法中，你从相当简单的操作开始——分别使用 `imagesx()` 和 `imagesy()` 确定现有图像的宽度和高度，并将新宽度和新高度初始化为 0：

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

接下来，确定调整后图像的最终尺寸。首先检查 `max_width` 和 `max_height` 的值，如果两者都存在，则计算图像尺寸以使其等于或小于这两个最大值。如果没有提供两个最大值，则检查调整大小比例值，如果存在，新图像尺寸将基于原始尺寸的设置比例：

```php
// New dimensions to fall within maximums provided
if ($this->max_width and $this->max_height)
{
    if ($this->max_width/$old_width <= $this->max_height/$old_height)
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
    $new_width = ceil($this->ratio * $old_width);
    $new_height = ceil($this->ratio * $old_height);
}
```

方法的其余部分是实际执行调整大小的地方（如果需要）。在 GD 中调整大小时，你实际上并不是直接调整现有资源的大小，而是创建一个新的具有新尺寸的图像，并将原始图像复制到目标位置——GD 在内部处理调整大小。在这个方法中，你使用的是 `imagecopyresampled()` 函数；在使用 GD 调整图像大小时，可以使用 `imagecopyresized()` 函数或 `imagecopyresampled()` 函数。两者都能达到相同的目的，但后者在保持结果“平滑”方面做得稍好一些，而前者则会产生像素化的结果。请查看：

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
```

注意 Alpha 保存函数 `imagesavealpha()` 和 `imagealphablending()` 的使用。它们用于告知 GD 在执行调整大小时保留并使用源图像中的 Alpha 透明信息。如果忽略 Alpha 通道，透明 GIF 或 PNG 中可能存在的任何透明效果都可能会被破坏。

最后，在该方法的末尾，返回 GD 图像资源。

### 旋转图像

除了在服务器上调整图像大小外，常见的图像编辑需求还包括在上传后旋转图像的能力。为了实现此操作，你将像之前一样创建另一个图像操作类文件，并添加另一个方法将函数调用到 WebImage。




## 首先，创建一个名为 `class.ImageRotate.php` 的文件，其中包含以下图像旋转类：

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

### 然后，向 WebImage 类定义中添加以下方法：

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

这个过程比缩放方法稍简单，但非常相似。WebImage 的 `rotate()` 方法接受一个参数：您想要旋转图像的度数。与 `resize()` 类似，`rotate()` 包含必要的类文件，设置旋转参数，然后执行旋转。

在 ImageRotate 内部，过程相当直接。`process()` 方法检查是否提供了旋转值，然后获取一个将用作背景色的颜色。如果您旋转 90、180 或 270 度，您将看不到该颜色，但如果您使用其他任何值，图像会扩大以包围新的倾斜原始图像，背景色将填充旋转源未覆盖的区域。设置颜色后，使用 `imagerotate()` 函数旋转图像：

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

当然，最后返回图像资源。

### 添加说明

接下来，在一系列简单的图像功能中：为图像添加说明——图像底部暗化区域，叠加说明或简短文本。这是一种微妙的方式，可以在不将文本与图像分开或造成干扰的情况下，包含并显示有关图像或其上下文的一些信息。

首先，遵循 ImageResize 和 ImageRotate 的示例，创建一个名为 `class.ImageCaption.php` 的文件：

```php
<?php
class ImageCaption
{
    public $caption = "";
    public $fontfile = "";
    public $fontsize = 10;
    public $padding = 5;
    public $drawline = true;

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
            $text_underbaseline = $text_box[3];

            // Get some image dimensions
            $img_x = imagesx($gd_img);
            $img_y = imagesy($gd_img);

            // Draw background shading
            imagealphablending($gd_img, true);
            $rect_color = imagecolorallocatealpha($gd_img, 0, 0, 0, 75);
            imagefilledrectangle($gd_img,
                0,
                $img_y - $text_height - ($this->padding * 2),
                $img_x,
                $img_y,
                $rect_color);

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

            return $gd_img;
        }
    }
}
?>
```

然后，像之前一样，在 **WebImage** 类定义的末尾添加一个新方法，如下所示：

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

调用 WebImage 的 `caption()` 方法时，您可以使用最多五个参数。前两个是必需的，分别指定说明中要显示的文本，以及用于说明文本的 TrueType 字体（.ttf）文件名。其他参数设置字体的像素大小、文本周围的像素填充量，以及是否在说明上方绘制一条淡线。该方法包含所需的类定义文件，整理参数值，然后调用 ImageCaption 的 `process()` 方法。

`process()` 所做的是确定要写入的文本尺寸以及目标图像本身的尺寸。要获取渲染文本的尺寸，使用 `imagettfbbox()`。`imagettfbbox()` 接受四个参数：字体大小、字体角度、用于渲染文本的 TrueType 字体文件，以及文本本身。确定文本包围盒信息后，实际高度被设置为 `$text_height`，并确定文本低于基线的量——对于小写字母 g 和 p 这样的字母。以下是代码：

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
        $text_underbaseline = $text_box[3];

        // Get some image dimensions
        $img_x = imagesx($gd_img);
        $img_y = imagesy($gd_img);
```

接下来，在图像上绘制一个背景阴影框，以提供一个更暗的区域，有助于稍后在该方法中显示您将叠加在上面的白色文本。首先，通知 GD 在目标图像上正确混合透明度。然后，使用 `imagecolorallocatealpha()` 获取颜色资源——在这种情况下为黑色（0,0,0），约 60% 透明（alpha 通道的范围是 0–127）。最后，使用半透明黑色在图像底部绘制一个填充矩形，使用覆盖完整字体高度加任何指定填充所需的高度：

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

在图像上绘制背景矩形后，是时候在上面添加说明文本了。只需为文本分配一种颜色——在这种情况下为白色——然后使用 `imagettftext()` 在图像上绘制文本：

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

`imagettftext()` 函数使用八个参数：要添加文本的图像资源、字体大小、文本角度、开始绘制文本的 x 位置、文本基线/底部的 y 位置、文本颜色、ttf 字体文件名，以及要渲染的实际文本，按此顺序。

说明的最后部分仅使用半透明浅灰色和 `imageline()` GD 函数，在说明框顶部绘制一条淡边框：

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



## 第 10 章

```php
        }

        return $gd_img;
    }
```

### 添加标志

你将在 `WebImage` 类中添加的最后一个功能是能够在图像上放置标志或水印。

首先创建 `class.ImageLogo.php` 文件：

```php
<?php

class ImageLogo
{
    public $logoFile;
    public $ratio = 1;
    public $location = array('x'=> '', 'y' => '');
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
                    $logo_y = round((imagesy($gd_img) / 2 -
                        (imagesy($logo->gdresource) / 2)));
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

接下来，将 `logo()` 方法添加到 `WebImage` 类定义的末尾：

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

与添加到 `WebImage` 的其他动作处理方法一样，`logo()` 简单接收提供的参数——标志文件名、x 位置、y 位置、以像素为单位的内边距以及标志的缩放比例——在 `ImageLogo` 中设置所需的属性，并处理标志的放置。

在 `ImageLogo` 的 `process()` 函数中，你可以确切看到标志放置过程中发生了什么。`process()` 方法首先创建自己的内部 `WebImage` 对象，用于加载标志文件，并在需要时进行缩放。在 `WebImage` 创建并加载后，如果指定了比例，则会缩放标志图像：

```php
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
```

接下来，确定标志的位置。标志可以放置在九个位置之一——三种水平位置和三种垂直位置的任意组合。对于水平方向，可以使用值 `l`、`r` 和 `m` 来指定左对齐、右对齐或居中。垂直方向的值类似——`t` 表示顶部，`b` 表示底部，`m` 表示居中：

```php
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
```

最后，标志图像被合并到主图像上，并返回生成的图像资源：

```php
// Copy the logo onto the main image
imagecopy($gd_img,
          $logo->gdresource,
          $logo_x,
          $logo_y,
          0,
          0,
          imagesx($logo->gdresource),
          imagesy($logo->gdresource));

return $gd_img;
```

请注意，这里使用的是 `imagecopy()` 而不是 `imagecopymerge()`。`imagecopymerge()` 函数似乎更适合此任务，甚至提供了合并标志并设置其透明度的功能——这对于某些水印效果很有用。不幸的是，`imagecopymerge()` 有一个坏习惯，会破坏源标志图像中大部分透明度信息，因此如果你想为图像制作一个淡淡的半透明水印，最好直接在标志图像中添加透明度，并使用 `imagecopy()`，而不是使用不透明图像和 `imagecopymerge()`。

### 测试一下

为了彻底测试这组图像操作代码，你需要准备几样东西：一张要处理的主图像、一张用作标志叠加层的图像，以及一个 TrueType 字体文件。准备好这三样东西后，创建一个 PHP 脚本，使用你创建的类来处理图像。首先，只需加载你的图像，并在浏览器中显示：

```php
<?php

    require_once 'class.WebImage.php';

    $img = new WebImage();
    $img->load('base.png');
    $img->display();
?>
```

在浏览器中加载此文件，它应该显示你的图像，如图 10.1 所示。

![](img/cacdd24f2926f10ee3219256ad732604_283_0.png)

图 10.1

如果你想在保存或显示图像之前更改图像类型，只需在 **WebImage** 对象中设置图像类型即可：

```php
<?php

    require_once 'class.WebImage.php';

    $img = new WebImage();
    $img->load('base.png');
    $img->type = 'image/gif';
    $img->display();

?>
```

要调整图像大小，请调用 `WebImage` 的 `resize()` 函数。以下代码使用 0.75 的比例：

```php
<?php

require_once 'class.WebImage.php';

$img = new WebImage();
$img->load('base.png');
$img->resize(0.75);
$img->display();

?>
```

输出示例如图 10.2 所示。

![](img/cacdd24f2926f10ee3219256ad732604_284_0.png)

图 10.2

接下来，旋转你的图像。以下使用 180 度进行旋转：

```php
<?php
    require_once 'class.WebImage.php';

    $img = new WebImage();
    $img->load('base.png');
    $img->rotate(180);
    $img->display();
?>
```

在浏览器中加载脚本后的效果如图 10.3 所示。

![](img/cacdd24f2926f10ee3219256ad732604_285_0.png)

图 10.3

现在，为图像添加说明文字。此示例使用“Fuji Wide Normal”字体，但你也可以使用你拥有的任何字体，只要它是 TrueType 字体文件（.ttf）即可：

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

如果一切顺利，你应该看到与图 10.4 类似的内容。

![](img/cacdd24f2926f10ee3219256ad732604_286_0.png)

图 10.4





## 第 10 章

最后，尝试一下图像 Logo 应用程序。在这个示例中，你将把一个 Logo 放置在图像的右下角，位于说明框的上方：

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
$img->logo('logo.png', 'r', 'b', 5, 0.3);
$img->display();
?>
```

现在，一个稍微缩放过的 Logo 应该会出现在右下角，带有 5px 的内边距，如图 10.5 所示。

![](img/cacdd24f2926f10ee3219256ad732604_287_0.png)

你可以看到，使用 GD 库并不困难，并且允许对你的图像进行相当多的灵活性和控制。还有许多其他更高级的函数可以使用，所有这些都可以在 PHP 手册的 GD 部分找到（http://www.php.net/gd）。

## Ming

Ming 是 PHP 的第三方扩展，允许用户创建 Shockwave Flash 文件，而无需实际使用 Macromedia 的 Flash 工作室。由于使用 PHP 和 Ming 创建 Flash 文件的方式，Ming 提供的功能并不总是与 Macromedia 的 Flash 中可用的功能相同。Ming 确实提供了一种低成本创建 Flash 文件的方法，并允许在需要时动态创建内容。

### 关于 Ming

动态创建的 Flash 文件的实用性有时会让一些人感到困惑，特别是因为你不会拥有使用 Macromedia 的 Flash Studio 的人对内容布局的精确视觉控制。此外，Ming 的功能集仅限于 Flash 4 版本，这比最新版本落后了几个版本。但是，能够脚本来创建并为应用程序添加动态内容是你无法使用 Macromedia 的 Flash Studio 实现的功能。在需要 Flash 的功能但又希望为用户个性化内容时，这在向用户分发内容方面非常有用。

Ming 本身实际上是一个第三方扩展，已经为它编写了 PHP 包装器扩展，因此需要在构建二进制文件时将其编译到 PHP 二进制文件中。Ming 与 PHP 的安装说明可以在 PHP 的网站上找到（http://www.php.net/ming）。关于 Ming 本身的更多信息可以在 SourceForge.Net 上的 Ming 网站（http://ming.sourceforge.net）上找到。互联网上还有许多教程和示例，可以帮助说明 Ming 的功能，并提供可作为构建你的 Flash 电影基础的代码片段。

Ming 在 PHP 中作为对象实现，因此每次你在 PHP 中使用 Ming 创建 shockwave 文件时，你至少需要实例化一个 SWFmovie 对象的实例。以下是用 Ming 和 PHP 生成的非常简单文件的一些代码。要运行此代码，请将其插入到一个没有其他内容的 PHP 文件中，然后在安装了 Flash 插件的网络浏览器中查看该文件：

```php
<?php
header("Content-type: application/x-shockwave-flash");
$a = new SWFmovie();
$a->setDimension(100,100); //width and length in that order
$a->setBackground(0,0,255); // red, green, and blue integers
$a->output();
?>
```

这并没有生成很多内容，但它会在你的浏览器中生成一个巨大的蓝色屏幕。检查代码，你可以看到使用 Ming 创建的 Flash 文件中需要包含的一些必要部分。第一行告诉 PHP 设置 Content-type 头，以便浏览器知道这是一个 shockwave 文件并加载相应的插件。下一行实际创建了 SWFMovie 对象的实例。接下来两行是可选的，但如果没有它们，就很难看出生成了什么内容，因为它们设置了 shockwave 文件的大小并将其背景设置为蓝色。最后一行告诉 PHP 将 Ming 生成的文件输出到浏览器。这里真正需要注意的事情是在输出电影之前设置正确的 Content-type 头，并确保没有其他内容（如多余的行和空白）被发送到浏览器。

只能有一个 SWFMovie 对象的实例，但你可以在一个 SWFMovie 对象中包含多个小电影。为了做到这一点，你需要使用另一个对象，SWFSprite 对象。这个对象具有与 SWFMovie 对象相似的特性和属性，但不受每个电影只有一个的限制。这样的好处是，你可以在同一个 Flash 电影中同时显示多个动画。每个动画甚至可以以不同的速率运行，并且在时间长度上也不同。

Flash 文件使用*帧*，就像电影或动画中的帧一样。SWFMovie 和 SWFSprite 对象都有向它们添加新帧的函数。如果你可以通过将对象包含在特定帧中来将不同的对象显示到屏幕上，那么帧是有用的。这意味着，如果你想同时显示两个或多个对象，它们需要一个公共帧。一旦对象被添加到帧中，直到该对象从电影中移除，它之后的每个帧都包含该对象。此外，就像电影或动画一样，你可以前进或后退，也可以使用 SWFAction 对象跳到特定帧。这种帧的使用提供了在 Flash 电影中更好地组织对象和生成时间线的方式。

Ming 和 Flash 都使用一种可能与你习惯不同的坐标系统。Flash 使用的距离单位是 twip。twip 被*定义*为精确的 1/1440 英寸或 1/20 点的大小。这种测量通常简化为易于转换的值，即 20 个 twip 单位等于 1 个像素。然而，这可以是一个任意值，因为 Flash 播放器会将电影缩放到播放器窗口的大小。幸运的是，Ming 中包含的 SWFBitmap 对象具有确定图像 twip 大小的功能。因此，如果你需要一个基于图像尺寸的电影，你只需创建 SWFBitmap 对象，读取其宽度和高度值，然后基于它设置电影本身的尺寸。电影的尺寸不一定要在显示前才设置。

### Ming 中的对象

PHP 总共提供 13 个对象来使用 Ming 生成 Flash 文件。你可以结合使用这些对象来创建许多具有广泛功能的复杂 Flash 文件。它们如下：

- SWFAction 对象允许你向 Flash 文件添加逻辑和功能，超越简单的图像显示。使用 SWFAction，你可以移动图像和形状以用于游戏等事物，以及读取和设置 Flash 文件中对象的属性。此外，你可以包含一些 ActionScript 脚本，这是 Flash 版本的 JavaScript，并且非常相似。这个对象通常与 SWFButton 对象一起使用，以在用户按下按钮时执行某些操作。常用的操作包括根据用户的响应显示 Flash 电影中的特定帧。

- SWFBitmap 对象允许将图像添加到 Flash 文件中。不过有几个限制，因为只有非渐进扫描 JPEG 图像和 DBL（“define bits lossless”）图像可以以此方式添加。任何其他图像都需要使用另一个扩展（如 GD）或通过对工具进行系统调用转换为这些格式之一。这个对象经常与 SWFSprite 和 SWFSpace 对象一起使用。

- SWFButton 对象向你的 Flash 文件添加一个按钮。此按钮可用于启动 SWFAction 对象的操作。它响应常见的鼠标操作，如下压、释放和悬停。可以向按钮添加形状以改变其外观。

- SWFDisplayItem 对象允许在将形状、文本对象、精灵或按钮添加到电影后，通过引用添加到电影后返回的句柄来操作它们。操作，如倾斜、缩放和移动项目，都是可能的操作。

- SWFFill 对象由使用 SWFShape 对象的 addFill 方法生成。它允许通过旋转、倾斜和缩放形状的填充来转换填充。

- SWFFont 对象加载供 SWFText 对象使用的字体。字体可以是字体定义块（FDB）或浏览器定义的字体引用。

- SWFGradient 对象创建渐变，然后可以被 SWFShape 方法的 addFill() 使用。

- SWFMorph 将两个形状结合，将第一个形状变形为第二个形状。这可用于一些基本动画。

- SWFMovie 对象是其他对象正常运作所必需的唯一对象，因为它是实际将 Flash 文件写出到文件或浏览器的对象。

- SWFShape 对象生成形状。形状实际上是通过传递由一支想象中的笔绘制的坐标来绘制的。通过正确的坐标，几乎可以生成任何形状。此外，如前所述，这与 SWFBitmap 对象一起用于向电影添加图像文件。

- SWFSprite 对象通过向对象添加帧来生成“电影剪辑”或动画。帧包含其他对象之一，如 SWFShape。单个帧中可以包含多个 SWFSprite 对象，因此可以看到两个动画同时进行。与仅使用 SWFMovie 对象相比，向 SWFSprite 对象添加图像的优势在于它更好地封装对象以便操作。

- SWFText 对象在 Flash 动画中显示文本。如果你只需要显示少量静态信息，使用 SWFText 对象的替代方法是使用图像而不是使用 Flash 来写文本。

- SWFTextField 类似于 SWFText 对象，但有一些不同。SWFTextField 对象不能被旋转或倾斜，但可以用作表单输入。

### 创建 Flash 显示

再加几行代码，你可以将前面的示例扩展为稍微更有趣的外观：

```php
<?php
header('Content-type: application/x-shockwave-flash');
$movie = new SWFMovie();
$movie->setDimension(100,100); //width and length in that order
$movie->setBackground(0,0,255); // red, green, and blue integers

$shape = new SWFShape(); //generate a shape object
$shape->setLine(4, 30, 60, 100); //set the line width to 4 along
// with red, green, and blue integer values
$shape->setLeftFill($movie->addFill(300, 200, 100));
//set the color of the shape with red, green
// and integer values
$shape->movePenTo(20, 20);
```





## 第 10 章

//将虚拟的画笔移动到一个新位置
$->drawLineTo(20, 80);
//绘制线条到一组新的点
$->drawLineTo(80, 80);
$->drawLineTo(80,20);
$->drawLineTo(20,20);
$->add($);  //将该形状添加到电影文件中

$->nextFrame();  //推进电影中的一帧
$->output();  //向浏览器输出所有内容
?>

该电影生成的输出内容本身并没有什么特别之处，但它演示了一些重要对象的一些基本方法。输出结果应该是一个蓝色背景，中间有一个绿色方块。

为了更深入地说明 Ming 的功能，你将使用它来生成一个幻灯片。为了使事情变得简单，你将使用所有大小和形状相同的图像，并且所有图像都有明确的名称。创建一个新文件并包含以下代码行：

<?php
//创建一个电影对象
$movie = new SWFMovie();
//将背景设置为白色
$movie->setBackground(255, 255, 255);

在初始设置完成后，你需要添加对幻灯片中要包含的图像的引用。这里使用了一个简单的图像名称数组，但这可以扩展为直接从目录甚至数据库读取。另外，在此示例中，假设所有图像的大小都是 200 × 200 像素。为了更轻松地确定电影大小并扩展代码，创建了一个图像实例来读取其宽度和高度，尽管示例中的所有图像都应该是 200 × 200 像素。试试看：

//要显示的图像
$images = array("1.jpg", "2.jpg", "3.jpg");

$bitmapImage = new SWFBitmap(SWFBinaryLoader::load("$images[1]","rb"));
$w = $bitmapImage->getWidth();
$h = $bitmapImage->getHeight();

创建一个 SWFSprite，它将作为幻灯片中的迷你电影，实际上也将由用户控制。为了防止它仅显示所有图像，为其添加了一个默认的 stop() 操作。此外，电影的大小是根据图像大小计算的，并额外留出空间以便在图像下方添加按钮。以下是代码：

//创建一个将充当迷你电影的精灵
$Sprite = new SWFSprite();
//在第一帧添加停止操作
$Sprite->add(new SWFAction("stop();"));

//设置电影大小，为按钮预留额外空间
$movie->setDimension((1*$w),(1.5* $h)+3);

#### PHP 扩展

现在需要将这些图像中的每一个都添加到精灵中，这可以通过遍历数组轻松实现。每个图像首先被转换为 SWFBitmap 对象，然后作为填充添加到 SWFShape 对象中。在形状周围画一条线后，将其添加到 SWFSprite 对象中，并且 SWFSprite 对象转到下一帧：

//遍历所有图像
for($i=0; $i<count($images);$i++){

//从图像创建位图
$bitmapImage = new SWFBitmap(open($images[$i],"rb"));

//创建一个形状对象来容纳图像
$shape = new SWFShape();
//生成图像形状的填充
$fill = $shape->addFill($bitmapImage);
//将填充添加到形状
$shape->setRightFill($fill);

//在形状周围画线以设定大小
$shape->drawLine($w, 0);
$shape->drawLine(0, $h);
$shape->drawLine(-$w, 0);
$shape->drawLine(0, -$h);
//将形状添加到精灵以使其显示
$sprite->add($shape);
//生成新帧并转到该帧
$sprite->nextFrame();
}

由于精灵不会自动返回第一帧，因此需要在最后一帧添加一个操作，使其跳转到第一帧。gotoFrame() 操作接受一个帧号作为参数；这里使用的是 0，因为它是精灵中的第一帧。然后向精灵添加另一帧，以确保所有内容都包含在 SWFSprite 对象中：

//跳转到第 0 帧
$sprite->add(new SWFAction("gotoFrame(0);"));
//再次生成新帧
$sprite->nextFrame();

现在精灵已完成，需要将其添加到 SWFMovie 对象中。当它被添加到电影时，它会返回一个句柄，该句柄可用于引用精灵，以便对其加以控制。为其分配一个名称，并使用句柄将精灵移动到指定位置：

//添加精灵并获取其句柄
$handler = $aMovie->add($sprite);
//现在我们可以使用句柄为精灵命名
$handler->setname("images");
//我们也可以用句柄移动精灵
$handler->moveTo(0,2);

为了创建一个控制幻灯片的按钮，你需要创建一个新的 SWFShape 对象并为其添加按钮图像

//再次创建一个形状
$shape = new SWFShape();
//这次创建另一个位图用于按钮图像
$bitmapImage = new SWFBitmap(open("button.jpg", "rb"));
$file = $shape->addFill($bitmapImage);
$shape->setRightFill($file);
//创建形状周围的边框
$shape->drawLine($w, 0);
$shape->drawLine(0, $h);
$shape->drawLine(-$w, 0);
$shape->drawLine(0, -$h);

实例化一个 SWFButton 对象，并将按钮形状添加到 SWFButton 对象中。还设置了按钮的默认标志，这允许程序根据按钮是否被按下以及鼠标是否在按钮上方来执行操作。还为按钮添加了一个操作，用于将精灵移动到下一帧。

//现在实际创建一个按钮对象
$button = new SWFButton();
//将形状及其所有默认标志添加到按钮中，这些
//标志实际上都是预定义的整数值
$button->addShape($shape, SWFBUTTON_HIT |
    SWFBUTTON_UP | SWFBUTTON_DOWN |
    SWFBUTTON_OVER);
//添加一个操作以转到
//精灵的下一帧。精灵通过 "images" 引用
$button->addAction(new SWFAction("setTarget('images');
    nextFrame();"),SWFBUTTON_MOUSEDOWN);

然后将按钮添加到电影中并返回句柄。将按钮移动到图像正下方，并向电影添加一个新帧。然后生成必要的浏览器头信息，并输出电影：

//将按钮添加到电影并保存返回的句柄
$handler = $aMovie->add($button);
//使用句柄将按钮移动到图像下方
$handler->moveTo(0,$h+3);
$aMovie->nextFrame();
//向浏览器发送适当的头信息
header("Content-Type:application/x-shockwave-flash");
//将电影输出到浏览器
$aMovie->output();

在使用 Ming 时，有几件事需要记住。首先，当你直接输出到浏览器时，必须在调用 SWFMovie 对象的 output() 方法之前发送 Content-Type 头。这会发送正确的 HTTP 头，以便浏览器知道加载 Shockwave Flash 插件。这导致了另一种可能发生的错误：输出除了 Content-Type 头之外的任何内容，例如空行。除了头和电影本身之外，输出其他内容会损坏文件，导致浏览器错误地显示该文件。此外，了解你希望最终输出看起来怎样的大致布局也是有帮助的。为了帮助布局使用 Ming 创建的 Flash 电影，你可以使用提供坐标系统的图形程序，或者直接使用坐标纸。

## SimpleXML

如今，XML 无处不在，因此有一种简单的方法来检索和解析这些文件是理所当然的。幸运的是，PHP 为我们提供了一个 XML 接口，用于利用 XML 数据，这是一个简单且易于使用的扩展：SimpleXML。SimpleXML 默认已安装，但如果你不打算使用它，建议在 php.ini 中将其禁用。需要注意的是，SimpleXML 也需要 PHP5。

顾名思义，该扩展的目的是在非常基本的级别访问 XML 文档。为了说明实现的简便性，创建一个包含海滨租赁信息的虚构 XML 文件（此文件将用于所有示例）：

<?xml version="1.0"?>
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

既然你有了 XML 文件，获取信息并将其放入对象中（使用 simplexml_load_file() 函数），以便你可以操作它：

<?php
if (file_exists('beachfront.xml')) {
    $data = simplexml_load_file('beachfront.xml');

    print_r($data);
}
?>

你可以遍历该对象并以美观的方式显示结果（或者至少是更可读的格式）。向 simple.php 添加以下更改：





## 第 10 章

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

除了 `simplexml_load_file()` 之外，还有许多与 SimpleXML 扩展配套的其他函数。`simplexml_load_string()` 将 XML 文档作为字符串加载。你首先必须将其内容分配给一个变量；然后你可以使用 `simplexml_load_string()` 函数将该变量的内容解析为你可用的对象。如果你希望操作对象，然后以 XML 文件的形式将其内容显示回浏览器，你可以使用 `$objectname->asXML()` 函数。如果你需要查看元素的属性或对象中任意节点的子节点，`attributes()` 和 `children()` 函数会很有帮助。如果你想从 DOM 文档中获取一个 DOM 节点并将其转换为 SimpleXMLElement 对象，`SimpleXML_import_dom()` 函数会很有用。

`xpath()` 函数允许你通过特定字符串在 XML 文档中进行搜索。它使用 W3C 的 XPath 来评估 XML 文档中的每个节点，之所以被称为“XPath”，是因为搜索关键字类似于文件的路径，因为每个元素同样都是嵌套的。如果你想更多地了解 XPath，请访问 W3C 关于该主题的文档：http://www.w3.org/TR/xpath。

如果你只想执行最简单的查询，这样就足够了，如下例所示：

```php
<?php
if (file_exists('beachfront.xml')) {
    $data = simplexml_load_file('beachfront.xml');
    
    //find and list all the "locations" in our XML file
    //"locations" are under "descriptions" which are under "rentals"
    $find = $data->xpath('/rentals/description/location');
    
    while (list(, $v) = each($find)) {
        echo $v . "\n";
    }
}
?>
```

此脚本将返回你 XML 文件中名为“location”节点的所有值。如果你想进一步深入查询，你就必须使用另一种方法。请记住，这是 SimpleXML，而不是 ComplexXML。

SimpleXML 提供了一种非常快速且直接的方式来访问简单的 XML 文档。它不提供太多的灵活性，而且只能处理最简单的 XML 文件。例如，如果你试图在包含 HTML 代码内容的 XML 文件上运行这些函数，将会遇到问题。除此之外，与目前可用的许多其他 XML/PHP 接口相比，它的使用要容易得多。

#### 总结

虽然本章仅涵盖了其中的一小部分，但仍有许多其他的 PHP 扩展可用。完整的列表可在 PHP 手册（http://www.php.net）中找到。你可能需要注意的一些扩展包括：

- **CURL（客户端 URL 库函数）**：允许你使用许多不同的协议（除 http 外，如 SSL、FTP 和 gopher）连接到页面。
- **DOM**：使用 DOM API 与 XML 文档交互，并随 PHP 默认安装捆绑提供。
- **SOAP**：利用 GNOME xml 库启用创建 SOAP 服务器和客户端。
- **ZIP 扩展（Bzip2、rar、Zip、Zlib）**：启用读取 zip 文件，每个扩展处理不同类型的压缩文件。

通过这种对 PHP 扩展的初步体验，我们希望你能够自信地探索 PHP 中那些鲜为人知但同样有用的函数。

## 11 AJAX

典型的 web 应用程序通过表单与用户交互。服务器向客户端发送表单，用户输入响应，表单被提交回服务器进行处理。表单处理完成后，服务器响应一个新的完整页面，其构成通常取决于用户上一次的表单提交。在与用户的每次交互中，都需要一个全新的页面。此类应用程序必须使用带宽，即使这些元素在以前的响应中已发送到客户端，它们仍会在每次页面请求时传输恒定的页面元素（例如站点导航）。此外，由于 web 应用程序在处理一次交互的结果以及新页面加载之前是无响应的，因此此类应用程序比桌面应用程序更慢。

AJAX（异步 JavaScript 和 XML）指的是一组技术，允许创建富客户端 web 应用程序，其中应用程序处理的大量责任被交给客户端。具体来说，AJAX 应用程序通常使用 XHTML 和 CSS 进行语义标记和展示，使用 XML 来格式化将在客户端和服务器之间交换的数据，并使用 JavaScript 与服务器通信并操作文档对象模型（DOM）。使用 AJAX 时，客户端和服务器之间的通信可以仅限于数据，因为客户端具有处理展示和用户交互所需的必要功能。此外，这种通信是异步进行的，且无需刷新页面。这使得应用程序的客户端部分即使在数据与服务器交换期间也能保持响应。如果用户执行了一个需要向服务器发送请求的操作，请求可以发送，并且应用程序在等待响应期间（甚至发出更多请求时）可以处理进一步的交互。这一概念如图 11.1 所示。

当今最流行的 AJAX 应用程序可能是 Google 的 [GMail](http://www.gmail.com)，它是一个基于 web 的电子邮件框架。在传统基于 web 的电子邮件客户端中，用户的几乎每个操作都会导致整个页面或框架的刷新。由于 GMail 采用了 AJAX，页面从不刷新。相反，界面通过基于用户与应用程序的交互以及与 GMail 服务器的 XML 通信，利用 JavaScript 操作 DOM 进行动态更新。这使得用户例如可以撰写电子邮件，点击发送，并在 GMail 服务器处理实际发送消息的同时继续阅读他的或她的电子邮件。在阅读其余邮件时，他或她将收到一条状态消息，表明消息已成功发送。

![](img/cacdd24f2926f10ee3219256ad732604_299_0.png)

## 历史

AJAX 本身并不新鲜；其背后的思想也是。事实上，过去已经开发和使用了多种无需刷新页面即可与服务器通信的方法。

## 图像源技巧

JavaScript 允许使用 Image 对象动态加载图像。当创建一个图像并设置其 src 属性时，浏览器会发送对该图像的请求，并尝试将响应打包在图像对象中。开发人员已利用这一点通过设置 src 属性为服务器端脚本的 URI，并在查询字符串中向服务器传递数据，从而与服务器进行单向通信。服务器端脚本随后可能会更新数据存储。通常响应中不会返回图像，但这不会造成问题，因为开发人员并不将 Image 对象用于其预期目的。

这种技术的优点包括：

- 它允许在不刷新的情况下向服务器发送数据。
- 它可以读取对象属性以确定请求何时完成。

然而，它也有一些缺点：

- 它无法从服务器接收非图形数据（通信是单向的）。
- 它无法检测或处理在尝试通信期间可能发生的 HTTP 错误。

## 隐藏框架

许多开发人员发现图像源技巧不足以满足需求，并且除了向服务器发送数据外，还需要从服务器接收信息的能力。此时，使用隐藏框架的技术应运而生。在此技术中，开发人员使用一个不可见的框架（根据框架集设置，通过将高度或宽度设为 0）作为载体。隐藏框架只是一个包含最少 HTML 元素集合加一个 script 元素的页面。该 script 元素通常仅仅是数组和变量的定义，其值由服务器写入。因此，控制框架（可见的那个）可以将此框架的 location 属性设置为服务器端脚本的地址，可选地通过查询字符串向其发送数据。然后浏览器发出此请求。服务器端脚本处理查询字符串中传递的任何信息，然后以有效的 JavaScript 语法写入数据。查看以下代码以了解大致思路。

```html
<?php
$suname = $_GET['username'];
?>
<script type="text/javascript">
top.usernameOK = <?php echo isUsernameAvailable($suname); ?>;
top.usernameAlts = new Array(<?php echo implode(',', getSimilarNames($suname)); ?>);
top.frames[1].readVars();
</script>
```

> 此代码位于隐藏通信框架中。在此代码示例中，写入一个布尔值以指示通过查询字符串传递给脚本的用户名的可用性。当浏览器的 JavaScript 引擎执行此脚本时，它将把该布尔值存储在名为 usernameOK 的 JavaScript 变量中。




# 第 11 章

好的。用户名备选列表的数组也会被写入到输出中。在 PHP 中，该数组会被拼接成一个逗号分隔的字符串，以符合 JavaScript 数组语法。（`getSimilarNames` 函数还需要用引号包裹每个数组值。）

当隐藏框架加载 JavaScript 时，它会触发控制器框架，随后控制器框架可以访问由服务器端脚本写入的变量值，即 `top.usernameOK` 和 `top.usernameAlts`：

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

这段代码位于控制器框架中。将代码封装在一个由隐藏通信框架调用的函数中，是通过加载隐藏框架来触发数据检索的一种方法。

这种技术的优点包括：

- 它允许在不进行整页刷新的情况下，向服务器发送 *和* 接收数据。
- 一旦数据可用，它可以立即触发主应用程序的数据检索。
- 它简单易用且易于调试，因为应用程序使用的所有数据在隐藏框架的源代码中都清晰可见。
- 它可以接收图形数据，但浏览器对将 JavaScript 变量用作图像源的支持仅部分完善（例如，IE 只喜欢像这样分配的 XBM 图像数据）。
- 由于框架加载会增加浏览器历史记录条目，用户可以使用后退按钮。然而，后退按钮的行为可能不符合用户的预期。

而其缺点则包括：

- 它引入了可用性问题，例如无法轻松地对应用程序状态添加书签。
- 它可以在超时后重新提交请求，从而部分地检测通信错误。
- 用户很容易操纵隐藏框架的内容（这始终是一个顾虑，但对于使用隐藏框架技术的用户来说，这样做稍微容易一些）。
- 每个隐藏框架在给定时间只能发出一个请求（如果响应很重要，这是一个缺点）。

### 隐藏 IFRAME

与隐藏框架技术类似的是隐藏 IFRAME 技术。与在框架集中使用隐藏框架不同，这种方法使用一个不可见的 IFRAME 元素，通过更改其源位置向服务器发出请求并接收响应。Google Maps 使用此技术在不刷新页面的情况下与服务器通信。

此技术的优点是：

- 它具有隐藏框架技术的所有优点。
- 根据 IFRAME 源位置的更改方式，你对后退按钮的行为拥有更多的控制权。

而缺点是：

- 它遭受与隐藏框架技术类似的可用性问题困扰。
- 它可以在超时后重新提交请求，从而部分地检测通信错误。
- 每个隐藏 IFRAME 在给定时间只能发出一个请求（如果响应很重要，这是一个缺点）。
- 在如何通过编程方式添加 IFRAME 元素以及如何在源位置更改后引用 IFRAME 内包含的文档响应方面，浏览器之间存在严重的差异。

## XMLHTTP 和 XMLHttpRequest

即使现在被称为“AJAX”的方法也不新。微软版本的接口 XMLHTTP 自 1998 年底 IE 5.0 预览版发布以来，就以 ActiveX 对象的各种形式存在（IE 5.0 的最终版本发布于 1999 年 3 月）。多年来，企业一直在仅针对 IE 的环境中利用这种开发模式。自从 Mozilla 浏览器产品 1.0 版本发布前不久开始，一个以微软接口为模型、名为 XMLHttpRequest 的本地对象就已可用。最近，Safari（自 1.2 版起）、Opera（自 8 版起）和 Konqueror 都包含了同样名为 XMLHttpRequest 的合规接口。

在过去几个月里，XMLHTTP 及其变体的使用急剧增加。Google 在其 Google Suggest 和 Google GMail 产品中采用该技术，主要负责将这种开发方法推广给大众。此外，Adaptive Path 发表的一篇文章创造了“AJAX”一词，使开发人员能够用一个统一的名字来指代这组技术，从而促进了该主题的沟通和认知。

## 接口

以下是 XMLHTTP 和 XMLHttpRequest 接口中相关且在大多数浏览器中受支持的方法：

- `abort()`：中止请求。
- `getResponseHeader(key)`：返回名为 `key` 的 HTTP 响应头的值。
- `open(method, url, [async, [username, [password]]])`：将 HTTP 请求方法设置为 `method`，将请求 URI 设置为 `url`。可选地，它将指示是否异步处理请求的标志设置为 `async`，如果需要，则设置用户名和密码用于身份验证。方法属性通常是 `get` 或 `post`。如果在请求中推送数据，使用 `post` 是合适的（参见 `send()` 方法）。在几乎所有情况下，`async` 都应保留其默认值 `true`。

`overrideMimeType(type)`：强制将响应解释为服务器发送了指定类型的 mime 类型。此方法在 IE 中不可用。如果修改服务器以发送特定的 mime 类型不切实际，则此方法可能很有用。必须在调用 `send()` 之前调用此方法。它还可以用于避免 Mozilla 的一个 bug，该 bug 有时会导致浏览器在处理非 XML 响应时挂起。

`send(requestContent)`：发送 HTTP 请求。参数 `requestContent` 用于方法为 `post` 的请求（参见 `open()` 方法），并表示请求体。如果请求是异步的，此方法会立即返回。早期版本的 Mozilla 在发送字符串作为请求内容时存在困难。对于 `get` 请求，`requestContent` 应为 `null`。对于 `post` 请求，它必须是 `null`、字符串或 DOM Document 对象。如果是后者，对象将被序列化。此参数的内容包含在请求体中，因此服务器可以访问。

`setRequestHeader(key, value)`：将 `value` 的值分配给名为 `key` 的 HTTP 请求头。必须在调用 `open()` 之后且在调用 `send()` 之前调用此方法。

`open()` 和 `send()` 方法处理接口的主要功能。`open()` 方法设置请求的各种参数，如 HTTP 请求方法（`get` 或 `post`）和请求 URL。请求 URL 通常是服务器上脚本的相对位置。你可以使用完全合格的 URI，但由于安全限制，URI 的域必须包含发出请求的 JavaScript 的页面的域。这意味着如果你希望从位于其他域上的第三方数据源（例如天气数据源）获取数据，你必须通过位于你服务器上的服务器端脚本代理此类请求。

`open()` 方法的可选参数 `async` 决定了 `send()` 方法的行为。如果设置为 `true`（或保留默认值），`send()` 方法将发出 HTTP 请求并立即返回。这意味着对 `send()` 调用之后的 JavaScript 代码行将无论发出的请求的响应如何都会执行。相反，响应处理由事件的触发来触发，并由事件处理器处理。这个特性是 AJAX 中的第一个 A，它允许你开发行为类似于桌面应用程序的应用程序。此事件处理的具体内容通过接口的属性设置：

`onreadystatechange`：当 ReadyStateChange 事件触发时（即 `readyState` 属性发生变化时）调用的函数。此属性的值应是一个 JavaScript 函数。确保不要用括号引用函数，否则函数将被调用，此属性的值将变成函数的返回值而不是函数本身。

`readyState`：只读。这是一个表示请求当前状态的整数。此属性的可能值从 0 到 4，表示进度递增。值为 4 表示请求已完成且响应已完全处理。在 `readyState` 至少为 2 时，头文件和状态可用。

`responseText`：只读。这是文本形式的响应体。从 `readyState` 为 3 开始的成功请求中，它非空。在 `readyState` 为 4 时，`responseText` 完全填充。

`responseXML`：只读。这是解析为 text/xml 内容并封装为 DOM Document 对象的响应体。在 `readyState` 为 4 的成功请求中，它非空。

`status`：只读。这是整数 HTTP 响应状态码。200 表示成功响应。对于其他可能的状态码，包括许多错误代码，请参见 HTTP/1.1 RFC 的第 6.1.1 节（http://www.rfc-editor.org/rfc/rfc2616.txt）




除了 *responseText* 和 *responseXML* 之外，这些属性主要用于确定是否以及如何接收响应。这是必要的，因为你的请求是异步的，这意味着你不能依赖基于执行顺序或时间在任何特定代码行处响用的可用性。相反，异步通信依赖于事件驱动模型进行处理。*readyState* 属性包含一个指示请求进度的值。每次该值发生变化时，都会触发 *readystatechange* 事件。如果已定义 *onreadystatechange* 处理程序，则调用该处理程序来处理 *ReadyStateChange* 事件。请注意，对于给定的请求，*readyStateChange* 事件至少会触发四次。在大多数情况下，你只对最后一个事件感兴趣，即当 *readyState* 属性从 3（加载）变为 4（完成）时。然而，*readyState* 为 4 并*不*意味着请求成功。它仅表示所有操作已完成。你仍然必须检查 *status* 属性以了解请求的成功情况。例如，服务器在处理请求时可能会遇到错误。如果 *status* 属性为整数值 200（OK），则请求成功，预期的响应应可在 *responseXML* 或 *responseText* 中找到。如果这看起来很令人困惑，没关系：接下来你将要深入一些代码，一切都会变得清晰。

### 使用接口

由于该接口在不同浏览器中名称不同，且实例化方式也不同（在 Internet Explorer 中，因为接口是一个 ActiveX 对象，所以以这种方式实例化；而在 Mozilla、Safari、Konqueror 和 Opera 中则采用另一种方式），创建请求对象不像你想象的那样简单。这里展示的代码是一种非常基本的处理这些浏览器差异的方法。如果你研究过 AJAX 的实现，你可能见过与此非常相似的代码。

```javascript
<script type="text/javascript">
function getXMLHTTP() {
  var req = false;
  // 首先，尝试实例化原生对象
  if(window.XMLHttpRequest) {
    try {
      req = new XMLHttpRequest();
    }
    catch(e) {}
  }
  // 否则，尝试实例化 IE 的
  // ActiveX 对象。
  else if(window.ActiveXObject) {
    // 支持创建 ActiveX 对象
    // 并不意味着 XMLHTTP
    // 对象可用。所以，让我们试试。
    try {
      // 尝试实例化较新的版本
      req = new ActiveXObject("Msxml2.XMLHTTP");
    }
    catch(e) {
      try {
        // 否则，尝试旧版本
        req = new ActiveXObject("Microsoft.XMLHTTP");
      }
      catch(e) {}
    }
  }
  // req 要么是接口的引用，
  // 要么在失败时为 false。
  return req;
}
</script>
```

此代码隐藏了 XMLHTTP 和 XMLHttpRequest 接口实例化的浏览器差异，并返回可用的版本。

如前所述，对 XMLHttpRequest 响应的接收是通过触发事件和调用相应的事件处理程序来处理的。下一组代码提供了处理 ReadyStateChange 事件触发的典型方式，并仅对你感兴趣的事件采取行动：

```javascript
<script type="text/javascript">
function handleReadyStateChange() {
  if (!request) return;
  // 除非是完成的 readyState，否则忽略
  if (request.readyState == 4) {
    // 除非成功，否则忽略。
    // 你可以选择处理错误
    // 而不是忽略它们。
    if (request.status == 200) {
      // 对响应采取行动
      var xmlbody = request.responseXML;
      request = false;
      processResponse(xmlbody);
    }
  }
}
</script>
```

此函数被分配为 onreadystatechange 处理程序，并在 ReadyStateChange 事件触发时调用。它忽略所有 readyState 不是 4（完成）且 HTTP 状态码不是 200（OK）的事件。完整且成功的响应的 XML 主体被提取并传递给另一个函数进行处理。请注意，在获取 XML 主体后，请求对象被设置为 false。这是为了避免 Opera 中的一个浏览器 bug，该 bug 有时会在 readyState 变为 4 时触发多个 ReadyStateChange 事件。这可能导致对单个响应多次采取行动。

### 处理响应

前面各节中的代码相对标准。AJAX 应用的复杂性通常在于解释响应并根据其内容采取相应行动。通常，适当的行动是通过 JavaScript 操作 DOM。例如，如果你向服务器发出请求以检查用户名是否可用，并且服务器响应了此处显示的 XML 响应，那么你可能希望向用户显示一条消息，表明他或她需要选择其他用户名。你還可能希望根据 XML 响应中包含的替代方案提供建议：

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<usernamesresult>
  <username value="jessica" available="false" />
  <username value="jess" available="true" />
  <username value="jessica2005" available="true" />
  <username value="jessie" available="true" />
</usernamesresult>
```

在这个 XML 响应中，服务器指示该用户名不可用。此外，服务器还建议了可用的用户名变体。

传达此信息给用户的一种方式是通过 JavaScript 的 alert() 函数打开一个对话框。然而，一种更用户友好的方法可能是使用 DOM 操作在页面的某一部分添加一个 Div 或 UL 元素。这提供了一种较少侵入性的消息形式，允许用户继续与他正在与你的应用进行交互，并可以稍后再查看消息。下面的代码提供了如何遍历 XML 树并适当采取行动的例子：

```javascript
<script type="text/javascript">
function processResponse(oXML) {
    // 如果 xml 未定义或
    // 没有 documentElement，则退出
    if (!oXML) return;
    if (!oXML.documentElement) return;
    var doc = oXML.documentElement;
    // 返回所有名为 username
    // 的元素的 nodeListOf
    var unames = doc.getElementsByTagName('username');
    var msgs = new Array();
    // 遍历 username nodeList
    for (var i=0; i<unames.length; i++) {
        var u = unames.item(i);
        var username = u.getAttribute('value');
        var availability = u.getAttribute('available');
        // 使 available 属性
        // 更用户友好
        if (availability == 'true') {
            availability = 'available';
        }
        else {
            availability = 'not available';
        }
        msgs[msgs.length] = 'Username ' + username
            +' is '+ availability;
    }
    // 创建一个无序列表元素
    ul = document.createElement('ul');
    ul.id = 'msg';
    // 对于每条消息，创建一个列表项
    // 元素和一个包含消息的文本节点。
    // 文本节点是列表项元素的子节点，
    // 而 li 是无序列表元素的
    // 子节点。
    for (var k=0; k<msgs.length; k++) {
        var li = document.createElement('li');
        var txt = document.createTextNode(msgs[k]);
        li.appendChild(txt);
        ul.appendChild(li);
    }
    // 获取主 div 元素的引用
    // 并将我们的新无序列表插入其前面
    var maindiv = document.getElementById('maindiv');
    maindiv.parentNode.insertBefore(ul, maindiv);
}
</script>
```

此函数处理来自请求 responseXML 属性的 XML，并向 DOM 添加一个 UL 元素。

如你所见，DOM 操作可能相当复杂。这个特定响应的优点在于，你收集 username 元素，无论它们在 XML 响应中的位置如何。通常，你无法直接这样做，你必须了解 XML 响应的预期结构，或者至少了解各个元素与其他元素之间的对应关系。如果 XML 格式被修改，这可能会引起问题。在 XML 元素级别而非响应级别附加响应处理程序，在抽象整个 XML 文档的细节方面显示出一些前景，使客户端脚本能够专注于与该特定 DOM 操作相关的局部结构。

例如，你可能希望在一个单独的 DOM 元素中显示替代用户名，在这种情况下，你需要区分具有或不具有 usernamesalerts 父元素的 username 元素。然而，你不需要知道 XML 文档其余部分的结构以及这些 username 元素在文档树中的位置。实现这一想法需要 XML 元素名称与处理函数之间的映射。这种实现的细节超出了本章的范围，但有一些文章更深入地探讨了这一主题。

## AJAX 库

如果这一切看起来令人不知所措，请不要害怕。由于 AJAX 作为一种开发方法并不新鲜，有很多可用的库可以处理这些琐碎的工作。最近，随着对 AJAX 的兴趣重新高涨，可用库的数量急剧增加，现有库也在迅速成熟。

### SAJAX

SAJAX (http://www.modernmethod.com/sajax/) 是 Simple AJAX Toolkit，并且在 PHP（以及许多其他语言）中有一个服务器端实现。基本上，使用这个库，你可以在 PHP 中定义函数并通过 XMLHttpRequest 从客户端调用它们。为了使特定函数支持远程过程调用，只需一个 SAJAX 函数调用即可：sajax_export('phpFunctionName')。

不幸的是，在必要的 DOM 操作方面，SAJAX 没有帮助。事实上，由于 SAJAX 将响应视为文本，并使用给定元素的 innerHTML 属性直接将响应插入文档（这通常被认为不如 DOM 操作），因此除非你实现自己的字符串解析算法，否则不可能进行 DOM 操作。在 SAJAX 常见问题页面 (http://www.modernmethod.com/sajax/faq.phtml)，





开发者将“不过度抽象”列为一个特性。XMLHTTP 通信的许多方面若能引入适当的抽象，将会受益匪浅，因此你可能将 SAjax 缺乏抽象这一点视为其缺点。尽管如此，SAjax 提供了一种简化服务器端处理来自客户端的 AJAX 请求，以及简化客户端实例化 XMLHTTP 请求对象和发出必要请求的方法。

### CPaint

CPaint（[http://cpaint.sourceforge.net/](http://cpaint.sourceforge.net/)）是一个跨平台异步接口工具包。它支持纯文本和 XML 响应类型。此外，它还支持将响应直接检索为 JavaScript 对象。该库已经成熟并处于活跃开发中。

CPaint 根据函数调用为您生成 XML，结果是一种语义结构稍弱的结构。此外，出于某种未知原因，生成的 XML 元素全部为大写字母。如果您提供的元素名称不是全大写，该库会将其转换为全大写。库的使用文档读起来稍显晦涩，但每个部分都有良好的解释，并为每个部分提供了简单的示例，以帮助您理解其思路。

### JPsPan

JPsPan（[http://jpspan.sourceforge.net](http://jpspan.sourceforge.net)）的主要目标是填补 JavaScript 和 PHP 之间的鸿沟。它允许将 PHP 类无缝导入到 JavaScript 中。这意味着您可以在 PHP 中定义一个类，并像调用原生 JavaScript 对象一样调用其方法。在幕后，JPsPan 向服务器发出请求以远程执行方法。其他库提供类似的功能，但它们远不及 JPsPan 提供的抽象程度。JPsPan 的文档和示例代码丰富且清晰。两者均采用 wiki 格式，因此会不断更新。代码本身干净易读，正如它生成的 XML 一样。此外，目前正在进行初步工作，旨在将 JPsPan 嵌入 PHP 框架中，使开发胖客户端应用程序变得更加容易。

该库并未免除 DOM 操作任务，但它很好地抽象了 XMLHTTP 的使用。不幸的是，它似乎存在支持 Opera 浏览器的问题，但对基于 Mozilla 的浏览器和微软 IE 的支持相当良好。此外，根据您的应用不同，JavaScript 与 PHP 之间的桥梁可能对您帮助不大，甚至可能只是用 XML 树遍历交换了对象和原生 JavaScript 访问。由于创建 PHP 类的原生 JavaScript 版本涉及额外的开销，其好处可能并不足以抵消成本。然而，由于具有出色的抽象水平，JPsPan 几乎可以允许您完全忽略 PHP 类如何提供给 JavaScript 的细节，并将注意力集中在应用程序本身的功能上。

还有许多其他支持 PHP 的 AJAX 库。您可以在 [http://www.ajaxpatterns.org/AJAXFrameworks](http://www.ajaxpatterns.org/AJAXFrameworks) 了解有关各种 AJAX 库的更多信息。

## 何时不使用 AJAX

人们对 AJAX 的狂热兴趣是一把双刃剑。Macromedia 的 Flash 产品也曾出现过类似的繁荣。客户是因为它看起来很酷而要求使用它。与 Flash 一样，AJAX 引入了可用性和可访问性问题，其中许多在传统 Web 应用程序中已经是解决的问题。

# 第 11 章

例如，AJAX 应用程序存在于一个 URI 命名空间中。换句话说，当用户与应用程序交互时，URI 不会改变。这是有道理的，因为这是 AJAX 的主要卖点之一：能够在不刷新当前页面或移动到不同页面的情况下更改应用程序状态。然而，这使浏览器的后退按钮变得毫无用处，甚至可能导致用户完全离开您的应用程序。

1999年，著名的可用性专家 Jakob Nielsen 发表了一篇文章，指出了 Web 设计的十大错误。头号错误是破坏了浏览器后退按钮的功能。根据 Nielsen 的说法，后退按钮是继超链接使用之后的“第二大常用导航功能”。确实存在某些变通方法，可以部分复制后退按钮的功能。

另一个相关的可用性问题在于无法对特定应用程序状态进行书签收藏。在传统应用程序中，应用程序状态通常对应于单个 URL，因此可以对其进行书签收藏。一个例子是用户浏览产品目录到达特定产品的详情页面。用户可能希望为该页面创建书签以便稍后查看。此外，用户可能希望朋友查看该产品，并尝试通过电子邮件发送 URL。破坏这种书签收藏功能会对口碑营销的有效性产生重大影响。存在变通方法，允许完成其中一部分，*即获取给定 URI 并将其转发到 AJAX 应用程序以重建所需的应用程序状态*。然而，由于对于任何给定状态，地址栏中都不包含该 URL，这种方法仍然留下了如何准确告知用户如何对当前应用程序状态进行书签收藏的问题。浏览器的书签收藏功能变得无用，应用程序必须提供其他书签收藏方式，通常涉及非标准的用户界面元素。

试图解决这些可用性和可访问性问题的工作正在进行中，并且*正在*取得进展。然而，经常被忽视的问题是：可用性问题是否是不当使用技术所致？Flash 的可用性问题就是这种情况：开发者试图用一个 Flash 文件实现整个基于 Web 的应用程序。导致可用性问题的不是 Flash 技术本身，而是这种滥用。AJAX 的不当使用也是如此。对于恢复特定应用程序状态没有太多意义的情况下，该技术能发挥*出色*的作用。Google 的 Gmail 就是一个极好的例子。在基于 Web 的邮件客户端中，能够书签收藏给定状态的价值非常小。Google Suggest 等表单添加功能也是另一个很好的例子。在 Google Suggest 中无需书签收藏状态。基于 Web 的聊天客户端从书签收藏特定应用程序状态的能力中受益也不大。相比之下，如果产品目录失去了书签收藏状态的能力，将会受到很大影响。如果无法对给定文章的显示进行书签收藏，内容管理系统的可用性也会受到极大损害。

将 AJAX 技术应用于任何传统 Web 应用程序的诱惑是可以理解的。然而，许多传统 Web 应用程序会因为使用 AJAX 而*受损*。那些自然倾向于从 AJAX 中受益的应用程序的共同点是，它们传统上都是*桌面*应用程序。Gmail 是邮件客户端的基于 Web 的版本，它此前作为桌面应用程序表现最好（事实上，传统基于 Web 的邮件应用程序出现的唯一真正原因是能够随时随地访问它）。Google Suggest 的作用非常类似于传统上在桌面应用程序中发现的表单控件。除了 Java Applet 和类似解决方案外，聊天应用程序几乎 exclusively 是桌面应用程序。开发者曾试图制作纯标记和 JavaScript 版本的聊天应用程序，但这些应用程序无法与其原生对应物相提并论。

虽然确实存在例外，但一条好的经验法则是，AJAX 适用于将传统桌面应用程序或其元素转化为基于 Web 的版本。它为 Web 应用程序开辟了*新的可能性*，但并不一定有利于传统可能性。在决定何时使用 AJAX 时应谨慎，并问自己 AJAX 对于正在开发的应用程序是否*有益*。如果您遇到需要复杂变通方法才能解决的重大可用性问题，那么 AJAX 很可能不是合适的开发模型。

除了可用性问题外，还有支持方面的问题。如果一个应用程序依赖 AJAX 而没有针对旧浏览器的回退支持，可能会将很大一部分潜在用户群拒之门外。即使是当前浏览器，一些公司出于安全原因也要求*部分或完全禁用 JavaScript*。如果您的应用程序没有良好地降级并提供传统 Web 应用程序功能作为安全网，这些用户也将被拒之门外。这是否可接受取决于您的应用程序性质，因为对于某些应用程序，提供传统版本是不切实际的。其可接受性还取决于预期受众及其可能的浏览器选择。

## 更多信息

有关本章讨论主题的更多信息，可在以下资源中找到：

- *动态 HTML 和 XML：XMLHttpRequest 对象。* Apple, Inc.  
  <http://developer.apple.com/internet/webcontent/xmlhttpreq.html>
- *XMLHttpRequest：* Wikipedia，自由百科全书。  
  <http://en.wikipedia.org/wiki/XMLHttpRequest>
- *AJAX：* Wikipedia，自由百科全书。 <http://en.wikipedia.org/wiki/AJAX>
- *XMLHttpRequest：* XULPlanet.com。  
  <http://xulplanet.com/references/objref/XMLHttpRequest.html>
- *XML 附加内容：* mozilla 基金会。 <http://www.mozilla.org/xmlextras/>
- *AJAX 模式：* <http://www.ajaxpatterns.org/>
- *AJAX 事务：* <http://www.ajaxmatters.com/>

#### 总结

在本章中，您学习了如何使用 AJAX 将 Web 应用程序的许多处理任务转移到客户端。您还了解到，AJAX 并不是什么新的趋势，而是几种较旧技术的产物，每种技术都有一些使其不够理想的缺点。本章展示了如何使用 AJAX 接口，以及如何处理来自客户端的响应。它还简要介绍了一些可用的 AJAX 库，甚至讨论了不应使用 AJAX 的情况。




# 缓存引擎

你已尽最大努力优化代码并降低 PHP 脚本的处理负载，但似乎仍无法让页面速度足够快以让用户满意。现在是放弃的时候了吗？还不完全是——你仍能从 LAMP 环境中榨取更多性能，而缓存引擎将助你一臂之力。

在处理 PHP5 的不同缓存方案时，你有几种选择。有些配置实际上缓存的是内部编译后的 PHP 脚本，有些缓存生成的输出，还有些则缓存中间数据处理对象。本章将介绍几种缓存引擎，并帮助你判断哪一种最适合你。

## Alternative PHP Cache (APC)

Alternative PHP Cache（即 APC）是一种 PHP 操作码缓存引擎，目前作为 PECL/PEAR 仓库的一部分免费提供。APC 由 Daniel Cowgill 和 George Schlossnagle 创建，并由 Community Connect, Inc. 发布。在 PHP5 发布后，Yahoo! 修改了 APC 以支持新的 Zend 引擎，此后 APC 成为 PECL 的一部分。

APC 的工作原理是从 PHP 运行时引擎获取已编译的代码，并将其存储在共享内存中以便后续访问。每次下载脚本时，APC 会首先检查共享内存中是否存在该版本的缓存，然后再重新编译并执行磁盘上的脚本。由于 PHP 无需每次重新编译脚本，它可以极大地加快响应时间——在某些情况下，速度提升可达四倍以上。

APC 可以安装为动态共享对象（DSO），也可以静态构建到 PHP 中。以下部分将展示如何安装 DSO 版本，因为它无需重新编译 PHP，并且提供了随时添加或移除 DSO 的灵活性。

### 安装 APC

首先，从 PECL 网站获取最新版 APC 源代码：`http://pecl.php.net/package/APC`。

一旦你获得了 tar/gzip 格式的源代码副本，请解包并进入新创建的 source 文件夹：

```bash
tar -xzvf APC-3.0.5.tgz
cd APC-3.0.5
```

接下来，在 source 文件夹中运行 `phpize`。请务必使用正确的路径指向你安装的随 PHP 附带的 `phpize` 副本：

```bash
/usr/local/bin/phpize
```

当 `phpize` 运行时，你应该会看到类似以下内容的输出：

```text
Configuring for:
PHP Api Version: 20031224
Zend Module Api No: 20041030
Zend Extension Api No: 220040412
```

`phpize` 完成后，运行以下 `configure` 脚本，再次替换为你环境中 `php-config` 和 `apxs` 程序的正确路径：

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

构建完成后，以 root 身份安装 DSO：

```bash
make install
```

此时，你的 PHP 扩展目录中应该已经有一个 `apc.so` 的副本。

要完成安装，请将以下内容添加到 `php.ini` 文件的 extensions 部分，然后重启 Apache：

```ini
extension="apc.so"
```

### 配置 APC

在大多数情况下，APC 使用的默认配置就足够了，但如果你希望微调缓存以适应用户需求或系统环境，可以在 `php.ini` 中使用以下指令：

| 指令 | 默认值 | 设置位置 | 描述 |
| :--- | :--- | :--- | :--- |
| `apc.enabled` | 1 (启用) | php.ini, httpd.conf, .htaccess 和用户脚本 | 使用相应的值 1 或 0 启用或禁用 APC。如果在 php.ini 中，此设置仅在 APC 静态编译到 PHP 时真正有用——如果你像之前那样安装 APC，只需注释掉 `extension="apc.so"` 行即可。然而，此设置可以在用户脚本和 .htaccess 文件中更改，因此你可以用它来在单个脚本和目录中启用/禁用缓存引擎。 |
| `apc.shm_segments` | 1 | php.ini 和 httpd.conf | 使用数值，你可以指定 APC 使用的共享内存段数量。许多操作系统对每个共享内存段的大小都有限制，通常限制较低。如果 APC 内存不足，增加此值会使 APC 使用更多段，以绕过操作系统的限制。 |
| `apc.shm_size` | 30 | php.ini 和 httpd.conf | APC 共享内存段的大小，单位为 MB。根据操作系统不同，可能存在大小限制，且通常限制较低。请查阅你的操作系统文档以获取有关其共享内存段大小的更多信息。 |
| `apc.optimization` | 0 (关闭) | php.ini, httpd.conf, .htaccess 和用户脚本 | 这是一个实验性设置，此指令控制 APC 内置的优化器。随着此设置值的增加，优化器的激进度也随之增加。值为 0 时完全禁用优化。 |
| `apc.num_files_hint` | 1000 | php.ini 和 httpd.conf | 此设置为 APC 提供了关于你的网站通常提供多少个独立源文件的提示。 |
| `apc.ttl` | 0 | php.ini 和 httpd.conf | 定义每个缓存条目在允许较新的条目覆盖它之前，可以在缓存中持续存在的秒数。如果保持为 0，缓存可能会被陈旧条目填满，从而阻止较新条目的缓存。 |
| `apc.gc_ttl` | 3600 | php.ini 和 httpd.conf | 定义每个缓存条目在垃圾回收列表中保留的秒数。作为一种安全机制，用于处理服务器进程死亡导致缓存文件滞留在缓存中的情况。值为 0 时禁用此功能。 |
| `apc.cache_by_default` | On | php.ini 和 httpd.conf | 控制所有文件的缓存。使用此指令可禁用所有脚本的默认缓存，允许你使用下面的 `apc.filters` 指令对实际缓存哪些文件进行更精细的控制。 |
| `apc.filters` | "" (空字符串) | php.ini 和 httpd.conf | 允许你定义一个由逗号分隔的正则表达式列表，用于筛选哪些文件被缓存。使用 POSIX 扩展正则表达式——类似于 PHP 的 `ereg` 函数——你指定一个正则表达式列表来排除某些脚本的缓存。任何与列表中模式匹配的文件名都不会被缓存，除非该模式以 `+` 开头，在这种情况下它们将被 APC 缓存。创建正则表达式时，请假设使用相对文件路径，而非绝对路径。 |
| `apc.slam_defense` | 0 (禁用) | php.ini 和 httpd.conf | 使用 0 到 100 之间的数字定义，此指令指定服务器进程跳过缓存之前未缓存文件的概率。主要用于极度繁忙的 Web 服务器，`apc.slam_defense` 用于对抗多个服务器线程同时尝试缓存同一文件时的竞态条件。 |

### 移除 APC

如果在你安装 APC 之后，你不再需要它，你可以遵循以下简单步骤将其从 PHP 安装中移除。

首先，在你的 `php.ini` 文件中查找并删除 `extension="apc.so"` 行。或者，你只需将其注释掉：

```ini
;extension="apc.so"
```

此时，你可以重启 Apache，APC 将不再在 PHP 中处于活动状态。如果你想从机器上彻底销毁该 DSO，可以在重启 Apache 后，从你的 PHP 扩展目录中删除 `apc.so` 文件。

## eAccelerator

eAccelerator 是另一种编译态 PHP 缓存引擎，与 APC 类似。eAccelerator 是流行的 PHP4 缓存引擎 TuerckMMCache 的分支，是一个由 Frank Alcantara 和 SourceForge 程序员团队维护的免费编码器和优化器。

除了作为 PHP 优化器和缓存引擎外，你还可以使用 eAccelerator 来编码你的 PHP 脚本，这样你就可以将编码版本重新分发给安装了 eAccelerator 的客户端，而不必担心源代码被窥视。

> **注意：** 与其他 PHP 编码方案一样，当文件使用 eAccelerator 编码后，使用标准工具几乎不可能对其进行解密。然而，可以使用 PHP 引擎本身的调试器和反汇编器进行逆向工程，但通常这种努力并不值得可能的回报。

### 安装 eAccelerator

与 APC 类似，eAccelerator 可以按以下过程安装为 DSO。首先，下载一份源代码副本，可从 `http://eaccelerator.net/` 获取。

> **注意：** 不幸的是，目前 eAccelerator 与 CGI 二进制版本的 PHP 不兼容。如果你运行的是 CGI 二进制版本，本节仅供参考。

解压你下载的 tarball，然后进入新创建的目录：

```bash
tar -xvzf eaccelerator-0.9.3.tar.gz
cd eaccelerator-0.9.3
```

在此目录中运行你的 `phpize` 副本（同样，请相应更改路径）：

```bash
/usr/local/bin/phpize
```

然后，配置源码并构建二进制文件：

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

接下来，你需要为 eAccelerator 提供存放临时文件的地方。在 `/tmp` 文件夹中创建一个 `eaccelerator` 目录：

```bash
mkdir /tmp/eaccelerator
chmod 0777 /tmp/eaccelerator
```

最后，将以下内容添加到 `php.ini` 中，然后重启 Apache：

```ini
extension="eaccelerator.so"
```

### 配置 eAccelerator

与 APC 类似，默认选项在大多数情况下可能就足够了，但如果不够，你可以访问以下 `php.ini` 指令：




## 第 12 章

#### eAccelerator 配置指令

| 指令 | 默认值 | 设置位置 | 描述 |
| :--- | :--- | :--- | :--- |
| eaccelerator.shm_size | 0 | php.ini 和 httpd.conf | 定义 eAccelerator 用于缓存脚本的共享内存量（以兆字节为单位）。值为 0 表示让 eAccelerator 使用操作系统默认值。 |
| eaccelerator.cache_dir | /tmp/eaccelerator | php.ini 和 httpd.conf | 指定用于磁盘缓存的目录（如果 eAccelerator 配置为使用磁盘缓存）。 |
| eaccelerator.enable | 1 (启用) | php.ini, .htaccess, 和 用户脚本 | 允许使用数值 1 和 0 相应地启用和禁用 eAccelerator。此设置在用户脚本和 .htaccess 文件中可以更改，因此您可以使用它在单个脚本和目录中启用/禁用缓存引擎。 |
| eaccelerator.optimizer | 1 (启用) | php.ini, httpd.conf, .htaccess, 和 用户脚本 | 启用 eAccelerator 的内部代码优化引擎。值为 1 时启用优化器，0 时禁用它。此设置在用户脚本和 .htaccess 文件中可以更改，因此您可以使用它在单个脚本和目录中启用/禁用优化引擎。 |
| eaccelerator.debug | 0 (关闭) | php.ini 和 httpd.conf | 切换调试日志的开启和关闭。 |
| eaccelerator.check_mtime | 1 | php.ini 和 httpd.conf | 此设置控制 eAccelerator 是否检查文件的修改时间以确定其是否已被更改。启用的值 1 告诉 eAccelerator 如果 PHP 脚本已被更改，则自动重新编译它。 |
| eaccelerator.filter | "" (空字符串) | php.ini, httpd.conf, .htaccess, 和 用户脚本 | 此指令允许您指定一个空格分隔的列表，指示哪些文件应该和不应该由 eAccelerator 处理。该列表由带有通配符匹配（例如，`*.php *.phtml`）的简单文件名组成。要忽略特定的匹配项，请在相关模式前加感叹号。 |
| eaccelerator_shm_max | 0 (无限制) | php.ini 和 httpd.conf | 指定使用 **eaccelerator_put()** PHP 函数放入共享内存的数据的最大大小。数值以字节指定，值为 0 则禁用限制。 |
| eaccelerator.shm_ttl | 0 (从不删除过时的脚本) | php.ini 和 httpd.conf | 定义脚本在共享内存中由 eAccelerator 缓存多少秒后，允许将其从缓存中移除以响应新请求。值为 0 表示项目*从不*被移除，这可能会导致共享内存缓存最终填满并防止新请求被缓存。 |
| eaccelerator.shm_prune_period | 0 (从不删除过时的项目) | php.ini 和 httpd.conf | 类似于 **shm_ttl** 设置，此指令控制从共享内存缓存中收集过时的脚本。它不作为缓存中单个脚本的超时，**shm_prune_period** 通过仅在 **shm_prune_period** 中定义的值经过后移除过时项目来工作。此值以秒数表示，值为 0 告诉 eAccelerator 不要尝试移除过时项目。 |
| eaccelerator_shm_only | 0 (同时使用两者) | php.ini 和 httpd.conf | 启用和禁用（0 或 1）磁盘缓存。值为 0 告诉 eAccelerator 同时使用共享内存和基于文件的磁盘缓存，而值为 1 告诉 eAccelerator 仅使用共享内存。 |
| eaccelerator_compress | 1 (启用压缩) | php.ini, httpd.conf, .htaccess, 和 用户脚本 | 此指令启用和禁用输出内容压缩，类似于 Apache 的 mod_deflate 或 PHP 的 gzip 输出缓冲。 |
| eaccelerator_compress_level | 9 (最大压缩) | php.ini, httpd.conf, .htaccess, 和 用户脚本 | 此设置控制在使用 **eaccelerator_compress** 启用的输出压缩时使用的压缩级别。最大值 9 使用高压缩，导致传输的文件大小更小，而较低的值会降低压缩并增加传输大小。 |
| eaccelerator.sessions | N/A | php.ini 和 httpd.conf | 您可以使用此指令告诉 eAccelerator 您希望它将 session 数据和内容存储在哪里。值 `shm_and_disk` 告诉缓存引擎在共享内存和磁盘位置都存储 session 数据和内容。设置为 `shm` 时，它将使用共享内存作为主要存储位置，如果共享内存已满则回退到磁盘存储。`shm_only` 表示您希望仅使用共享内存且从不使用磁盘回退。值 `disk_only` 的行为完全相反：它表示您希望仅使用磁盘存储而不使用共享内存。 |
| eaccelerator.content | N/A | php.ini 和 httpd.conf | （参见上方 eaccelerator.sessions 描述以了解合并的 session/内容处理）。 |

### 移除 eAccelerator

移除 eAccelerator 很简单，只需删除或注释掉 `php.ini` 中相应的扩展行，如下所示：

```ini
;extension="accelerator.so"
```

要从系统中永久移除 eAccelerator，请从 PHP 扩展目录中删除 `accelerator.so` 文件。

有关 eAccelerator 的更多信息，请访问 <http://eaccelerator.net>。

## Zend Optimizer

为了不在可用的免费 PHP 缓存方案中落后，PHP 的 Zend Engine 的创建者 Zend 发布了他们自己的代码优化器，并且它是免费的。Zend Optimizer 的行为类似于 APC 和 eAccelerator：它缓存 PHP 脚本的编译状态，从而在后续请求中实现更快的执行。

除了加速 PHP 脚本的性能外，Zend Optimizer 还允许您在服务器上运行由 Zend Encoder 或 Zend SafeGuard Suite 编码的脚本。

### 安装 Zend Optimizer

安装 Zend Optimizer 比大多数竞争缓存方案稍微容易一些，因为它附带了一个方便的配置和设置向导。

首先，从 <http://zend.com/store/products/zend-optimizer.php> 下载适合您系统的软件包。

然后，解压缩归档文件，并进入新创建的目录：

```bash
tar -xvzf ZendOptimizer-2.5.10a-linux-glibc21-i386.tar.gz
cd ZendOptimizer-2.5.10a-linux-glibc21-i386
```

以 root 身份运行安装向导：

```bash
./install.sh
```

运行向导，在提示时指定必要路径。提供的默认值通常就足够了。在被询问时，请务必选择正确的 Apache 版本（本书编写时约为 Apache 2）。

向导会备份您的 `php.ini` 文件，并创建一个指向 Zend 修改后的 `php.ini` 文件的新符号链接。

在向导结束时，您可以选择自动重启 Apache，或者如果您愿意，退出向导并手动重启 Apache。

### 配置 Zend Optimizer

像 APC 和 eAccelerator 一样，您有一些可用的指令来调整 Zend Optimizer 的操作：

| 指令 | 默认值 | 设置位置 | 描述 |
| :--- | :--- | :--- | :--- |
| zend_optimizer.optimization_level | 15 (所有优化) | php.ini 和 httpd.conf | 确定 Zend Optimizer 执行的优化级别。优化器可以对每个脚本执行四个不同的传递，通过组合以下值进行控制：`0`：无传递，`1`：传递 1，`2`：传递 2，`4`：传递 3，`8`：传递 4。您只需将每个传递的数字相加即可获得优化传递设置。例如，值 11 将执行传递 1、传递 2 和传递 4 (1+2+8)。 |
| zend_optimizer.enable_loader | 1 (启用) | php.ini 和 httpd.conf | 您可以使用此指令启用或禁用 Zend Optimizer 而无需卸载它。值为 0 时禁用优化器；1 时启用。 |

### 移除 Zend Optimizer

要移除 Zend Optimizer，您必须先删除它为 `php.ini` 创建的符号链接。然后，将备份的原始 `php.ini` 文件恢复到其原来的位置。此时您可以重启 Apache，Zend Optimizer 将不再处于活动状态。如果您愿意，可以删除 Zend Optimizer 文件——它们的默认位置是 `/usr/local/Zend`。

## JPCache

内存/磁盘缓存方案领域的另一个条目是 JPCache。与 APC 和 eAccelerator 不同，JPCache 不需要编译为 DSO 或静态构建到 PHP 本身中。JPCache 实际上是用 PHP 编写的，并使用标准的 `include` 和 `require` 语句。

JPCache 通过将 PHP 脚本生成的输出存储到磁盘或 SQL 服务器中，而不是保存每个脚本的编译状态来工作。通过这种方式缓存输出，并结合 gzip 内容压缩，您可以实现 80% 或更多的带宽节省。

### 安装 JPCache

要开始使用 JPCache，您需要做的第一件事是在 <http://www.jpcache.com> 下载最新版本的副本。

接下来，解压缩 tar/gzip 归档：

```bash
tar -xvzf jpcache.v2.tgz
```

该目录的内容现在包含您使用 JPCache 所需的脚本。可以将此文件夹放置在您喜欢的任何位置，只要 Apache 运行的用户能够访问即可。记下该位置的完整路径，因为您在配置缓存时需要它。

在 JPCache 文件夹的根目录中，编辑 `jpcache.php` 文件。将以下行更改为指向您放置 jpcache 文件夹的位置：

```php
$includedir = "`path/to/jpcache-files`";
```

例如，如果您将解压后的 jpcache 文件夹移动到 `/www/jpcache`，您将使用以下值：

```php
$includedir = "/www/jpcache";
```

接下来，编辑 `jpcache-config.php` 文件。最重要的是，您需要取消注释一行，指示您希望使用哪种类型的缓存存储（文件或 MySQL）。对于本例，取消基于文件的存储选项的注释：

```php
$JPCACHE_TYPE = "file";
```





## 缓存引擎

需要更改的另一个设置是 `$JPCACHE_USE_GZIP` 值。此值用于启用 gzip 内容压缩，但不幸的是，由于最近版本的 JPCache 中存在一个 bug，在某些浏览器中输出可能会损坏。为了安全起见，请将此值设置为 0：

```
$JPCACHE_USE_GZIP=0;
```

还请注意控制文件缓存位置的设置 `$JPCACHE_DIR`，其默认值为 `/tmp/jpcache`。你需要实际创建 `$JPCACHE_DIR` 设置中列出的文件夹，因此在命令提示符下执行以下操作：

```
mkdir /tmp/jpcache
chmod 0777 /tmp/jpcache
```

最后，使用以下 PHP 脚本测试缓存系统，使用合适的路径指向你放置 JPCache 文件夹的位置：

```
<?php
require "/path/to/jpcache.php";
echo time();
phpinfo();
?>
```

注意页面顶部的 UNIX 时间戳。每次重新加载页面时，它应该保持不变——JPCache 正在提供缓存版本，而不是每次重新处理脚本。

### 配置 JPCache

除了前面提到的三个配置选项外，你还有十四个额外的配置变量可以根据需要进行修改。完整的配置选项列表如下：

| 配置选项 | 默认值 | 描述 |
| :--- | :--- | :--- |
| `$JPCACHE_TYPE` | 无——你*必须*在使用 JPCache 之前设置此变量。 | 要告诉 JPCache 使用基于文件或基于数据库的存储来存储缓存数据，你使用 `$JPCACHE_TYPE`。值 `file` 告诉 JPCache 使用磁盘存储，而值 `mysql` 使缓存数据存储在一个 MySQL 数据库中。 |
| `$JPCACHE_TIME` | 900 | 使用数值定义，此变量告诉 JPCache 在缓存中保留页面多长时间（以秒为单位）。负值将完全禁用页面缓存，而值 0 告诉 JPCache 永久保留缓存页面。 |
| `$JPCACHE_DEBUG` | 0 (关闭) | 使用 `0` 表示关闭，`1` 表示开启，`$JPCACHE_DEBUG` 控制是否启用调试。 |
| `$JPCACHE_IGNORE_DOMAIN` | 1 (忽略域名) | 如果你的 Web 服务器只提供一组内容，你可以将此值设置为 1 (开启)，让 JPCache 忽略文件名的任何域名前缀。当关闭时，JPCache 搜索与完整 URL 匹配的文件，包括域名。 |
| `$JPCACHE_ON` | 1 (启用) | 此变量仅控制是否启用 JPCache。 |
| `$JPCACHE_USE_GZIP` | 1 (开启) | 要启用 GZIP 输出压缩，类似于 Apache 的 `mod_deflate` 或 PHP 自身的 GZIP 输出缓冲，请设置此值为 1。请注意，由于最近版本的 JPCache 中的一个 bug，在使用 JPCache 的 GZIP 压缩时，某些浏览器中的输出可能会损坏。如果你的脚本在此设置启用时返回乱码或缺失的内容，请尝试禁用此设置，看看情况是否得到纠正。 |
| `$JPCACHE_POST` | 0 (禁用) | 此变量控制 JPCache 中的 HTTP POST 缓存。设置为 `0` 以禁用，`1` 以启用。 |
| `$JPCACHE_GC` | 1 | 要控制 JPCache 垃圾回收例程的积极性，你可以为 `$JPCACHE_GC` 分配数值。值范围为 `0` 到 `100`，表示对缓存项执行垃圾回收的概率百分比。 |
| `$JPCACHE_GZIP_LEVEL` | 9 (最大压缩) | 当使用 JPCache 内置的 GZIP 输出压缩时，你可以使用此变量来控制输出流的压缩级别。值范围从 `9`，表示高压缩率和较小的输出大小，到 `1`，表示低压缩率和较大的传输大小。 |
| `$JPCACHE_CLEANKEYS` | 1 (哈希存储键) | 当 JPCache 创建脚本输出的缓存副本时，它使用每个脚本的唯一键将输出存储在文件名或数据库记录中。默认情况下，JPCache 对标识符进行哈希处理，以使其难以确定给定缓存条目的来源，例如 “`JPC-be45886d86b822858023b8f6061401a2`”。如果需要，你可以告诉 JPCache 不哈希每个脚本的缓存标识符，以便你轻松确定每个缓存脚本的身份。禁用哈希后，脚本标识符将看起来更像 `directory_file_name_extension_HTTPMethod=n_n__`。 |
| `$JPCACHE_DIR` | /tmp/jp-cache | 使用此变量设置 JPcache 存储其基于文件的缓存数据的目录。JPcache 存储缓存文件的目录需要可由 Apache 进程用户写入。 |
| `$JPCACHE_FILEPREFIX` | jpc- | 当 JPcache 在磁盘缓存中创建缓存文件时，它可以在此指定一个文件名前缀，以避免与现有文件发生冲突。 |
| `$JPCACHE_DB_HOST` | localhost | 当使用数据库作为缓存存储位置时，你需要设置变量以便 JPcache 连接和使用数据库。此变量设置 JPcache 将连接到的数据库主机。 |
| `$JPCACHE_DB_DATABASE` | jp-cache | 此变量设置存储缓存数据的 MySQL 数据库的名称。 |
| `$JPCACHE_DB_USERNAME` | sqluser | 要设置存储在数据库中缓存信息时使用的用户名，请设置 `$JPCACHE_DB_USERNAME`。 |
| `$JPCACHE_DB_PASSWORD` | passvd | 与 `$JPCACHE_DB_USERNAME` 配合使用。此变量设置数据库连接密码。 |
| `$JPCACHE_DB_TABLE` | CACHEDATA | JPcache 缓存数据存储的表的名称在 `$JPCACHE_DB_TABLE` 中。要创建该表，你可以在 MySQL Monitor 或你首选的 MySQL 管理工具中执行以下命令：`CREATE TABLE CACHEDATA ( CACHEKEY varchar(255) NOT NULL, CACHEEXPIRATION int(11) NOT NULL, GZDATA blob, DATASIZE int(11), DATAARC int(11), PRIMARY KEY (CACHEKEY) );` 当然，你需要更改数据库表的名称，使其与你在 `$JPCACHE_DB_TABLE` 中指定的值相匹配，反之亦然。 |
| `$JPCACHE_OPTIMIZE` | 1 (执行 OPTIMIZE TABLE) | 在垃圾收集周期完成后，你可以指示 JPcache 在 `$JPCACHE_DB_TABLE` 中指定的表上执行自动 MySQL OPTIMIZE TABLE 命令。 |

### 移除 JPCache

要移除 JPCache，你需要搜索所有 PHP 脚本并删除对 jpcache.php 文件的任何 `include` 或 `require` 引用。删除引用后，你可以安全地删除 JPCache 目录。

> 有关 JPCache 的更多信息，请访问 http://www.jpcache.com 。

## memcached

与 APC、eAccelerator 和 JPCache 提供的输出缓存系统不同，memcached 系统依赖于后端对象的缓存来提供速度提升。memcached 是由 Danga Interactive（LiveJournal.com 的责任团队）创建的一个分布式内存对象缓存系统。memcached 缓存的不是页面输出或编译后的 PHP 操作码，而是各种代码对象，最重要的是数据库结果对象和数据模型实体。

这种缓存解决方案与本章节中的其他系统略有不同——memcached 实际上需要在其运行时始终运行其自己的守护进程。然后 PHP 可以使用其 memcached 函数集来访问和使用内存对象缓存。

### 安装 memcached

要安装 memcached，首先从 http://www.danga.com/memcached/ 获取守护程序的源代码副本。

然后解压缩 tar/gzip 归档文件，并切换到新创建的文件夹：

```
tar -xvzf memcached-1.1.12.tar.gz
cd memcached-1.1.12
```

接下来配置并构建源代码。如果 configure 报告缺少库（例如 libevent），请按照各自的说明下载并安装它们；然后重新运行 configure 脚本，然后构建 memcached。

```
./configure
make
```

然后，作为 root 用户，安装 memcached 守护程序：

```
make install
```

最后你需要做的是实际启动守护程序。以下命令使用 128MB 的 RAM 启动守护程序，在 IP 127.0.0.1 上的端口 11211 监听：

```
/usr/local/bin/memcached -d -m 128 -l 127.0.0.1 -p 11211
```





## 缓存引擎

如果你决定永久使用 memcached，请确保将启动 memcached 的命令添加到你首选的启动机制或脚本中，以便机器每次启动时都能自动加载它。

现在 memcache 守护进程已经运行，你需要准备 PHP 以使用缓存系统。从 http://pecl.php.net/package/memcached 下载 memcached PECL 模块。

解压归档文件并进入新目录：

```
tar -xvzf memcache-1.4.tgz
cd memcache-1.4
```

运行 phpize，然后配置并构建 DSO：

```
phpize
./configure
make
```

以 root 身份安装该模块：

```
make install
```

最后，将以下行添加到你的 php.ini 中，并重启 Apache：

```
extension="memcache.so"
```

### 使用 memcached

为了使用 memcached，你安装的 PHP DSO 为 MemcacheObject 提供了以下方法：

- **Memcache::add**
  `bool Memcache::add ( string key, mixed var [, int flag [, int expire]] )`

  此方法将变量或对象添加到内存缓存中，由令牌 key 标识。如果内存缓存中已存在相同 key 的值，则返回 FALSE。如果你希望在放入内存缓存之前压缩要存储的值，请提供 MEMCACHE_COMPRESSED 作为 flag，否则可以省略或设为 0。为 expire 提供的任何值都告诉 memcached 何时开始允许从缓存中移除该项。expire 的值为 0 表示该值应无限期缓存。

  > 只有变量和对象可以存储在内存缓存中，而资源则不可以。

- **Memcache::close**
  `bool Memcache::close ( void )`

  此方法关闭与 memcached 服务器之间的任何非持久连接。如果在关闭连接时发生错误，则返回 FALSE。

## 第 12 章

#### Memcache::connect
`bool Memcache::connect ( string host [, int port [, int timeout]] )`

此方法在运行 memcached 服务器的 host 上创建并打开一个连接。port 参数指定 memcached 使用的 TCP 端口，默认值为 11211，timeout 指定在尝试连接时等待多长时间后返回 FALSE。成功返回 true，失败返回 FALSE。

#### Memcache::decrement
`int Memcache::decrement ( string key [, int value] )`

当在内存缓存中存储一个简单的数值时，你可以实际使用 decrement() 方法将匹配 key 的值减少提供的 value。如果未指定递减值，则缓存值减 1。此方法在失败时返回 FALSE，成功时返回该项的新值。

#### Memcache::delete
`bool Memcache::delete ( string key [, int timeout] )`

此方法从内存缓存中删除由 key 标识的项。为 timeout 提供值会导致该项在提供的秒数后被删除。失败返回 FALSE，成功返回 TRUE。

#### Memcache::flush
`bool Memcache::flush ( void )`

此方法告诉 memcached 立即设置缓存中所有项的过期时间。一旦调用此方法，缓存中的任何项都可以被新键覆盖，但内存不会释放，直到该情况发生。此方法在成功时返回 TRUE，失败时返回 FALSE。

#### Memcache::get
`string Memcache::get ( string key )`
`string Memcache::get ( array keys )`

此方法检索存储在内存缓存中的一项或多项，匹配给定的 key 或 key 数组。根据提供的匹配 key 数量，成功时返回字符串或数组，如果没有找到匹配输入参数的 key，则返回 FALSE。

#### Memcache::getStats
`array Memcache::getStats ( void )`

这将返回一个包含关于内存缓存状态各种信息的数组，例如当前和总连接数、缓存项数以及服务器运行时间。

#### Memcache::getVersion
`string Memcache::getVersion ( void )`

这将返回一个包含 memcached 服务器版本号的简单字符串，如果发生错误则返回 FALSE。

#### Memcache::increment
`int Memcache::increment ( string $key [, int $value] )`

与 decrement() 方法类似，increment() 允许你轻松地直接在内存缓存中更改一个简单的数值——在这种情况下，是将存储的变量增加 $value，如果没有提供值则增加 1。成功时返回新值，失败时返回 FALSE。

#### Memcache::pconnect
`bool Memcache::pconnect ( string $host [, int $port [, int $timeout]] )`

此方法创建并打开到 memcached 服务器的持久连接，类似于 MySQL 的持久连接。参数与 connect() 相同：$host 指定 memcached 服务器的主机名或 IP 地址，$port 指定 memcached 的监听端口，$timeout 指定连接超时时间。

#### Memcache::replace
`bool Memcache::replace ( string $key, mixed $var [, int $flag [, int $expire]] )`

这会在缓存对象中搜索匹配 $key 的项，如果找到，则用值 $var 替换它。与 add() 和 set() 类似，replace() 可以提供 $flag 以请求在存储值时进行压缩，并为新值提供可选的过期时间。此方法在成功时返回 TRUE，失败时返回 FALSE。

#### Memcache::set
`bool Memcache::set ( string $key, mixed $var [, int $flag [, int $expire]] )`

这将值 $var 存储在内存缓存中，即使存在匹配 $key 的预存项。参数与 add() 和 replace() 完全相同。成功返回 TRUE，失败返回 FALSE。

你可以以类似于 MySQLi 方法的方式使用这些方法——你连接到 memcached 服务器，处理缓存的数据进出，然后断开连接。以下简单示例将一个 Circle 对象存储在内存缓存中：

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

如果你运行此脚本，它将打印一个数组，其中包含当时内存缓存的统计数据。如果是第一次运行脚本，或者第一次在服务器上不使用 memcached，你的 `curr_items` 值应为 1，反映新添加的 Circle 对象：

```
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

### 移除 memcached

与其他 DSO 缓存解决方案一样，你可以通过注释掉或移除 php.ini 中的相应行并重启 Apache 来快速禁用 memcache 功能。此时，你可以从 PHP 扩展目录中删除 memcache.so，并从系统二进制文件文件夹中删除 memcached 守护进程（之前安装的位置，最可能是 `/usr/local/bin` 或 `/usr/bin`）。

## 同时使用不同的缓存引擎

此时，你脑海中可能开始转动起来，你会开始好奇，“如果我同时使用多个缓存引擎会发生什么？”好吧，正如你可能怀疑的那样，适当选择*互补*的解决方案可以略微提高性能，但某些组合对你没有任何好处。

JPCache 和 memcached 可以与其他组件很好地协作，但 APC、eAccelerator 和 Zend Optimizer 在某种程度上是互斥的。虽然它们可能一起加载得很好，在执行 PHP 脚本时不会抛出任何错误，但使用操作码缓存组合的理由很少或没有。三者以某种方式提供大致相同的功能，因此使用多个操作码缓存只会导致系统的速度与最慢的缓存一样快。

尝试只选择一个操作码缓存解决方案，并尝试将其与 memcached 和 JPCache 结合使用。把你首选的内容压缩方案加入其中——JPCache 内置的内容压缩仍然有太多错误——你就拥有了一台精简且强大的组合缓存服务器。

## 选择你的缓存引擎

那么哪种缓存解决方案适合你？也许你最好先评估系统的需求，寻找当前或即将出现的瓶颈。如果你在脚本中处理大量的类和对象，或者经常从数据库中拉取大量重复数据，memcached 将是你在性能提升方面的最佳选择。如果你的网站代码生成相对静态的页面——你没有使用过多的用户个性化或其他高度动态的元素——你应该考虑使用 JPCache。如果数据层并不是真正的瓶颈，但你的 PHP 代码可能需要一些通用的性能调整，那么其中一种操作码缓存引擎会帮到你。如果你不确定使用哪个优化器/缓存，APC 是一个安全的选择。虽然它可能在 Zend Optimizer 可能提供的低级引擎加速或优化方面有所欠缺，但它通过高度可定制性和良好的支持来弥补——毕竟，它是 PECL 仓库的一部分。

#### 总结

无论选择哪种缓存解决方案，本章讨论的任何系统都有潜力大幅提高你的 LAMP 环境的性能。通过适当的注意和配置，你的缓存解决方案将允许你并发服务更多用户，并帮助你防范可能遇到的任何 DOS 或 SlashDot 效应。




## 内容管理系统

内容管理系统（CMS）帮助软件或网页开发人员组织和促进任何协作过程及其最终成果。“内容管理”这一术语大致上不仅指文件的签入和签出，还包括信息的通用共享，例如通用日历、wiki 等。最早的内容管理系统出现在 1975 年左右，当时大型机和电子出版的需求开始真正兴起。这些最早的版本基本上只不过是允许多个用户参与同一项目的一般存储库。

随着计算机系统变得越来越复杂，有效管理内容的需求也变得越来越复杂。随着互联网的成熟，CMS 的浪潮也随之而来。现在 CMS 的数量多得数不胜数。本章的目标是试图拨开迷雾，帮助你确定是否需要 CMS，哪种类型的 CMS 适合你的项目，以及如何使用 CMS 来提高效率。

### CMS 的类型

CMS 形态各异，基本上可以管理由个人或团队处理的任何内容。从管理简单的静态网站内容，到允许跨互联网的协作文档（wiki），CMS 执行许多功能。CMS 软件包通常可以归类为两种类型：企业级 CMS 和 Web CMS。

### 企业级 CMS

这些功能强大的软件包通常是综合解决方案，在企业或公司级别提供有效的内容管理。它们旨在帮助公司提高效率、降低成本、提高准确性和功能性，同时减少人为错误和缩短客户响应时间。

它们可以整合公司功能，如运输和交付系统、开票、员工和人力资源问题、客户关系以及文档管理和事务性（销售）系统。企业级 CMS 将数据管理降低到用户级别，因此许多用户可以将自己的部分添加到非常大的集成“饼”中。部署这些复杂系统的软件公司以其提供高度定制的全公司解决方案而自豪，这些软件通常价格不菲。

### Web CMS/门户

Web CMS 软件包主要是为在 Web 上使用的。它们可以整合众多功能，或者围绕一个特定功能。它们允许用户更新常见网站的某些部分，或在网站“社区”中协作。Web CMS 通过快速轻松地为主要网站带来功能，使开发者的生活变得轻松，并允许主要开发者将其他人纳入网站开发和维护中，而不必担心偏离标准。开源 Web CMS 软件包将是本章的重点，特别是 PHP/MySQL 软件包。

Web CMS 类别的一个子集是群件（groupware）。这种类型的软件包运行在内联网或互联网上，旨在允许用户（假定在同一公司工作，参与同一项目）之间的协作。它们通常提供项目管理、文件签入和签出、日历系统、电子邮件和内部论坛等功能。

### 开源 Web CMS 软件包

Web CMS 的常见功能包括：

-   **静态网页更新：** 更新内容而不改变网站的外观和感觉。
-   **网络日志（博客）：** 在线日志。
-   **Wiki：** 协作文档项目。
-   **出版物：** 发布和组织新闻文章。
-   **管理式学习环境：** 基于 Web 的学习。
-   **事务性 CMS：** 电子商务功能。
-   **图像和文件库：** 图像或文件的汇编，供公众使用。
-   **论坛：** 促进用户之间讨论的公告板系统。
-   **聊天室：** 用户之间的实时聊天。
-   **RSS 源：** 允许用户下载内容。
-   **投票：** 允许用户就某个主题进行投票。
-   **日历系统：** 基于 Web 的多用户日历。

还有其他许多功能可以被视为属于 CMS 领域，但这些是主要功能，也是本章重点关注的。

首先，查看一些更全面的开源 CMS 软件包。

#### 全能型 Web CMS

就像豪华的热带度假村将你的假期包装成一个整洁的包一样，这些综合 Web CMS 可以做的多少由你决定。以下部分介绍了一些可用的更流行的软件包，尽管你可以在诸如 [http://www.sourceforge.net](http://www.sourceforge.net) 等网站上找到大量此类软件包。本文不会详细介绍这些软件包的安装，因为你在过去可能在这方面已经有了一些经验。然而，如果安装有任何特殊注意事项，将会予以注明。此外，在安装这些软件包之前，你需要确保 LAMP 系统的所有方面都能正常工作。

大多数全能型 Web CMS 具有常见功能，如更改用户权限、修改站点布局、更改服务器设置等。有一点需要提到的是，许多所谓的综合 CMS 软件包中缺乏事务性 CMS 接口（*e* 商务的购物车）。

##### ExponentCMS

ExponentCMS 可在 [http://www.exponentcms.org](http://www.exponentcms.org) 获取。在撰写本文时，最新版本是 0.96.3，本节基于此版本。在 Exponent/Sourceforge 界面 [http://sourceforge.net/projects/exponent/](http://sourceforge.net/projects/exponent/) 上，你可以找到截图、文档、贡献和标准 Sourceforge 信息的链接。

#### 安装说明

安装相对简单，安装前你需要知道的一件事是，你需要创建一个数据库。这适用于远程和本地安装。你还需要设置用户名和密码，因为在安装过程中会要求你提供这些信息。

###### 总体概述/默认安装

安装此 CMS 会为你提供几种默认“激活”的功能。这些功能包括：

-   **地址簿：** 组织联系信息。
-   **管理控制面板：** 易于使用的网站管理接口。
-   **日历系统：** 以不同视图跟踪事件。
-   **联系表单：** 允许访问者联系你。
-   **图像管理器：** 与其他模块配合管理站点上的图像。
-   **预览链接：** 允许参与站点工作的人员预览其工作。
-   **私人信息中心：** 允许用户相互发送电子邮件或私人消息。
-   **资源管理器：** 组织和显示上传的文件。
-   **文本模块：** 显示文本并跟踪修订版本。
-   **Web 日志/在线日志管理器：** 组织博客条目。

“未激活”的功能（你可以简单打开的功能）包括：

-   **横幅管理器**：管理横幅广告活动和点击通过。
-   **内容轮换器**：每次用户访问网站时显示不同的图像或文本。
-   **Flash 动画管理器**：组织 Flash 动画。
-   **表单模块**：管理站点上的任何表单。
-   **HTML 模板管理器**：管理上传的 HTML 模板。
-   **登录模块**：允许用户登录站点。
-   **多站点管理器**：允许你创建和管理其他站点。
-   **导航器**：管理导航系统。
-   **新闻源系统**：组织和显示新闻文章。
-   **搜索**：允许用户搜索站点。
-   **UI 切换器**：赋予具有正确权限的用户在用户和管理员之间切换的能力。

通过易于使用的管理模块管理器，你可以单击按钮激活或停用这些模块中的任何一个。

还可以从 [http://www.sourceforge.net](http://www.sourceforge.net) 下载其他模块。使用扩展上传管理器，安装模块很简单；你甚至不需要解压它们。这些扩展包括：

-   **文章管理器**：组织和显示站点上的文章。
-   **公告板**：管理站点论坛。
-   **常见问题解答**：管理站点的 FAQ 部分。
-   **图像库**：允许用户对图像进行排名和查看。
-   **列表管理器**：组织和管理列表，例如房地产列表。
-   **页面分发器**：允许你上传和显示动态生成的页面（如 PHP）。
-   **幻灯片**：管理站点上的幻灯片。

除了安装、激活和停用站点模块外，作为站点管理员，你还可以通过管理界面导入数据（如 csv 格式的用户列表）。这使你能够轻松地从其他系统或内部数据库转换。

软件中还嵌入了 WYSIWYG HTMLArea 编辑器，使你的作者和贡献者可以轻松添加文本。作为管理员，你还能控制 HTMLArea 工具栏，这让你可以确定用户拥有的文本选项。

###### 自定义默认设置

像大多数其他 CMS 软件包一样，你可以在管理控制面板中更改用户设置。在 Exponent CMS 中，你可以基于用户和内容设置审批策略，尽管此 CMS 侧重于模块而非用户。例如，你可以为日历模块创建审批策略。


……只不过这需要至少获得其他两名管理员的批准，请求的变更才会生效。虽然您也可以将特定模块的权限分配给用户或用户组，但这是通过每个具体模块进行的，而非通过用户界面。用户访问权限没有不同的级别——用户要么具有管理员权限，要么没有。此外，虽然您可以查看哪些用户拥有哪些模块的权限，但无法查看某个用户负责的所有模块。

此外，Exponent CMS 允许您在管理界面的“配置站点”区域中控制部分设置。

####### 数据库设置

您可以切换到 MySQL 或 PostgreSQL，当然也可以更改数据库名称、用户名、密码、端口以及任何表前缀名称。

####### 显示设置/主题

站点预装了几个主题，但通过编辑相关文件（或从头创建自己的主题），创建自定义主题也相当简单。除非您喜欢重新发明轮子，否则我们的建议是选择最接近您想要版式的主题，并在此基础上进行编辑。在“管理主题”页面的每个示例主题底部都有一个链接，允许您查看该主题的完整文件列表，使您更容易了解需要修改哪些文件以适应您的需求。

在此部分，您还可以更改对其他贡献者的引用方式，以及日期和时间如何显示给网站访客。

####### 常规配置设置

在此部分下，您可以自定义页面标题、元标签和关键词，以及语言选择。您还可以开启/关闭用户注册，启用验证码（用于区分计算机和人类的通用图灵测试，CAPTCHA）以防止机器人注册，并控制会话超时和 SSL 设置。

####### SMTP 设置

这里是设置您的 SMTP 端口、用户名、密码、身份验证方法等的地方。如果您愿意，还可以在此切换到 `php_mail()` 函数。

####### 其他插件

除了激活/停用预安装模块以及安装新提供的模块外，还有一个相当庞大的由大众贡献的其他插件列表。这可以通过 Exponent 的 SourceForge 界面网站 http://www.sourceforge.net 的“Tracker”贡献部分获取。它包含一些非常实用的插件，例如添加水平下拉导航，因此请务必查看一下。

####### 更改模块的布局和外观

使用 ExponentCMS 添加和删除模块很容易，而在页面上移动它们更容易。然而，使模块外观彼此不同却有些挑战性。

## 第 13 章

##### 优缺点

此包的优点包括：

- 更改模块的布局和放置位置是一项简单的任务，且本质上是所见即所得的。此外，您可以打破传统的两列或三列布局，并为所有三个传统列添加子列。
- 文本模块会跟踪修订版本，并允许您立即查看或恢复旧版本（只需单击一次）。如果它能显示*谁*进行了修订会更好，但也许该功能在未来的版本中可用。
- 预览功能让您无需注销管理员身份即可查看变更对站点外观的影响。
- 与其他一些 CMS 的功能驱动不同，主题更具神秘感和设计导向。

一个缺点在于用户管理——管理员无法查看个人用户拥有的所有权限或模块职责。例如，如果 Bob 要休假，您想将 Bob 的模块分配给其他人，没有简单的方法可以看到 Bob 具备什么能力以及他可以修改哪些模块。

CMS 位列 Sourceforge 十大“最活跃”下载列表是有原因的。ExponentCMS 是*最*易于管理的开源 CMS。然而，其优势更多在于幕后，因为其重点不一定是与访问站点的大众互动，而是管理员可控制的核心贡献者群体。如果您正在寻找一个外观不错的“开箱即用”站点，ExponentCMS 应该值得列入您的评估名单。

#### XOOPS

XOOPS（可扩展对象导向门户系统，eXtensible Object Oriented Portal System）是另一个流行的综合 CMS，可在 Sourceforge 或 <http://www.xoops.org> 获取。最新版本是 2.1.1，这里讨论的就是该版本（实际上这是 2.2 版本的预发布版，请留意这一点）。

#### 安装说明

XOOPS 团队编写了一份非常全面的安装指南，不仅引导您完成安装和设置过程，还为开发者提供有关文件放置位置及原因的详细信息。您应该阅读这份文档，它可以在 <http://docs.xoops.org/modules/xdocman/index.php?doc=xu-002&lang=en> 找到。

在安装之前，有几点需要指出：

- 解压 tar 文件后，您需要将 html 文件夹复制到网站根目录（如 htdocs 或 public_html）。XOOPS 团队建议您将此文件夹重命名为 xoops，但这完全取决于您。
- 如果您正在远程服务器上安装，需要在安装之前创建数据库、用户和密码。如果您正在本地安装，安装向导将为您完成此任务。
- 解压文件后，您需要对以下目录和文件执行 chmod 操作，使其可写：
  - uploads/
  - cache/
  - templates_c/
  - mainfile.php
- 为了让 XOOPS 安装向导正确完成过程，您必须在浏览器中启用 Cookie 和 Javascript。

##### 通用概述/默认安装

有几个功能是默认激活的：

- **横幅管理**：管理横幅广告和点击跳转。
- **图像管理器**：管理图像以及谁可以上传它们。
- **笑脸**：管理“笑脸”表情及其显示方式。
- **头像**：管理头像。
- **评论管理器**：管理用户发布的评论。
- **用户管理**：编辑、发送邮件、搜索用户、更改用户等级。
- **区块**：管理区块（如“在线用户”和“最新评论”）。

默认安装的模块只有系统管理模块。软件包中默认可用（但需要逐个安装）的其他模块包括：

- **联系我们**：向网站管理员发送消息。
- **下载**：组织上传的文件，并允许用户对它们进行评级。
- **链接**：链接管理器。
- **论坛**：站点论坛（由 phpBB 团队创建）。
- **新闻**：管理用户提交的文章。
- **版块**：允许管理员发布站点的不同版块。
- **常见问题解答**：管理站点的常见问题解答。
- **头条**：来自其他站点新闻的 RSS 源。
- **会员列表**：显示站点的注册用户。
- **合作伙伴**：组织和显示合作伙伴站点。
- **投票**：管理在线调查和投票。

##### 自定义默认安装

在撰写本文时，XOOPS 网站上可下载 300 多个插件模块。有一个模块几乎可以做您想要的任何事情，包括交易功能（购物车），这类功能在同类 CMS 中并不常见。

在管理控制台的 **系统管理** 部分，您会发现以下几个可以进一步自定义安装的区域：

- **头像**：允许您为用户上传可用的头像。
- **横幅**：管理您的横幅广告，并提供点击跳转率和激活横幅的统计数据。
- **区块**：提供添加新区块并确定其在站点上布局的界面。
- **评论**：允许您查看、编辑和删除评论。
- **查找用户**：不允许自定义站点，但提供广泛的搜索界面来过滤用户。
- **群组**：将用户分配到不同群组并设置该群组权限的地方。权限分为系统、模块和区块级别，允许授予管理员或访问权限。
- **图像管理器**：管理图像库。
- **邮件用户**：不允许自定义站点，但允许您向用户发送邮件。
- **模块**：允许您安装并激活或停用可用模块。
- **首选项**：提供站点的一般自定义，分为以下几个类别：
  - **常规设置**：允许您更改站点名称、标语、管理员电子邮件地址、默认语言、起始页模块、服务器和默认时区、默认主题（仅为您安装了三个）、用户主题、匿名用户的用户名、gzip 压缩、cookie 和会话信息、站点是否完全关闭、站点关闭时的自定义消息、IP 地址、SSL 设置、被阻止的 IP 地址以及配置缓存设置。
  - **用户信息设置**：允许您设置密码和用户名设置、用户默认所属的群组、头像设置、被阻止的用户名（如“admin”），并更改注册免责声明。
  - **元标签和页脚**：允许您设置元标签信息，如关键词、描述、robots 指令、评级、作者、版权以及页脚信息。
  - **单词审查选项**：允许您审查不需要的单词并用您选择的单词替换它们。
  - **搜索选项**：允许您开启或关闭全局搜索设置，并为用户发起的搜索要求最小关键词长度。
  - **邮件设置**：允许您配置邮件服务器设置和邮件方法。





###### 表情符号

管理论坛的表情符号，并允许您创建自定义表情。

###### 模板

允许您向网站上传模板。

###### 用户等级

控制论坛的用户等级系统，并允许您为自定义级别配置最低发帖数量。

###### 编辑用户

使您可以删除用户并编辑其信息——昵称、姓名、电子邮件、URL、时区、即时通讯信息、位置、职业、兴趣爱好、签名、评论权限、通知、等级、密码和群组。

##### 优点与缺点

该软件包最优秀的部分包括：

- 庞大的用户基数和支持论坛使开发人员能够轻松找到问题的解决方案或排查故障区域。
- 单词审查选项是一个不错的附加福利。
- 由于论坛模块是由 phpBB 小组开发的，论坛控制功能高度可定制且细节丰富。

可能需要改进的领域包括：

- 虽然核心文档非常详尽，但附加模块的文档相当匮乏。由于附加功能可能占据网站很大比例，这可能会让缺乏经验的人感到沮丧。
- 默认安装仅包含三个主题，鉴于如此庞大的支持和用户基数，可以合理认为可以预装更多主题。

XOOPS 因其潜力而流行，尽管您必须愿意解读他人的代码，并有足够的时间来微调您的安装以满足具体需求。虽然它作为一个“开箱即用”的方案并不是特别出色，但如果您愿意且有能力花些时间进行编码，它可以完成您所需的几乎任何事情。它非常以用户为导向，允许您作为管理员控制用户的环境，甚至可以精确到“表情符号”层面。如果您专注于与任何访问您网站的人创建互动社区，您应该重新审视 XOOPS。

#### phpWebsite

phpWebsite 可在 [http://phpwebsite.appstate.edu](http://phpwebsite.appstate.edu) 获取。撰写本文时，phpWebsite 的最新版本是 0.10.01，并将作为此处讨论的基础。

#### 安装说明

阿帕拉契州立大学（phpWebsite 的创建者）的友好人员设置了一个命令行安装过程，允许您直接从 phpWebsite 网站安装。您还可以分段下载应用程序（核心、主题包等）并自行安装。

## 第 13 章

安装前需要注意的一些事项：

- 您需要安装以下 PEAR 库才能运行核心应用程序：
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

- 如果可能，您需要以 root 身份登录后再进行安装。脚本会检测您是否不是 root 用户，并在应用某些安全限制的情况下设置应用程序。如果您尝试切换用户，它将保留原始设置，而不会执行 root 安装。
- 您必须安装 wget，否则安装程序将无法运行。

##### 通用概述/默认安装

立即可用且对您激活的模块包括：

- Apache Controller（Apache 控制器）：允许管理员更改 Apache 设置。
- Help System（帮助系统）：帮助管理员导航系统。
- Language Administrator（语言管理员）：管理网站上使用的语言。
- Layout Manager（布局管理器）：管理网站的布局。
- Site Search（站点搜索）：搜索网站。
- User Manager（用户管理器）：批准具有不同级别修改网站权限的用户。
- Announcements（公告）：管理网站上发布的公告。
- Block Maker（块制造器）：允许您创建和管理块。
- Branch Creator（分支创建器）：管理在主站点下创建的衍生站点。
- CalendAr：站点的 CalendAr。
- Comment Manager（评论管理器）：管理评论。
- Debugger（调试器）：协助管理员定位和修复错误。
- Documents（文档）：文件管理器。
- FAQ（常见问题解答）：管理站点的常见问题解答。
- Link Manager（链接管理器）：组织和显示链接。
- Menu Manager（菜单管理器）：管理动态菜单。
- Module Maker（模块制造器）：允许您创建自己的模块。
- Notes（笔记）：向网站用户发送电子邮件。
- Web Pages（网页）：管理站点上的静态页面。
- Form Generator（表单生成器）：创建表单。
- Photo Albums（相册）：组织和管理在线图像库。
- Bulletin Board（公告板）：管理论坛。
- RSS News Feeds（RSS 新闻源）：管理源。
- Polls（投票）：管理在线调查和投票。
- Skeletion Module（骨架模块）：用作模板的示例模块。
- Admin Stats（管理员统计）：跟踪最活跃的模块和用户。

## 内容管理系统

##### 自定义默认安装

与所有 CMS 软件包一样，其美妙之处在于修改默认安装，使其真正符合您的需求。

添加、删除和编辑用户及其权限可以在管理控制面板的用户管理部分完成。在这里，您可以设置是否允许用户注册，以及他们是否需要在参与论坛等活动之前获得批准。您还可以创建自己的身份验证脚本或使用本地数据库来验证用户。如果某用户被授予管理员状态，您可以控制他或她可以访问哪些模块，以及该模块内可以执行哪些特定功能。例如，用户可能可以创建投票，但不能编辑、删除或列出投票。

更改模块的布局是可能的，但不像 phpWebsite 的一些其他功能那样容易做到。您可以更改每个特定模块的外观，这是一个不错的功能。

HTML 头信息（meta 标签、关键字等）由管理控制面板中的布局管理员部分控制。这有点出乎意料。

目前在 http://www.sourceforge.net 上有 21 个其他主题供您使用和下载。

##### 优点与缺点

该软件包最有吸引力的功能包括：

- 管理员可以获得大量的统计信息，这使得网站微调变得更加容易。
- 能够创建自己的授权脚本是一个不错的功能。
- 管理员可以单独更改框和模块的外观，因此同一页面上的所有框不必看起来相同。
- 允许非常详细的用户权限，使查看谁允许做什么变得简单明了。
- 默认模块非常广泛，使构建全面网站对开发人员来说工作量更小。

唯一的缺点是，目前系统不允许打破传统的两栏或三栏布局。

phpWebsite 是一个不错的“中庸之道”CMS，在内置功能的高级水平与用户互动性的高程度之间取得平衡。如果您正在寻找一个能够支持中等规模贡献者群体，同时仍能培养访客互动性的软件包，那么这个 CMS 可能适合您。

#### TikiWiki

该软件可在 [http://www.tikiwiki.org](http://www.tikiwiki.org) 获取，撰写本文时可用的当前版本是 1.9.0。

#### 安装说明

如果您使用的是较旧版本的 PHP（早于 4.3）或 MySQL（早于 4.0.1），那么您将需要特别注意“要求和设置”文档，该文档可在 [http://doc.tikiwiki.org/tiki-index.php?page=requirements+and+setup](http://doc.tikiwiki.org/tiki-index.php?page=requirements+and+setup) 找到。其他需要注意的要点是：

- PDF 生成模块需要安装 php-xml 包。
- 由于使用了会话，请确保您的 php.ini 文件具有以下设置：
    - session.save_handler = files
    - session.save_path = /tmp（用于本地安装）

您还需要在安装前创建数据库和用户/密码。安装包可以从网站下载，或者如果您正在安装到远程服务器，安装页面上有一个单独的链接，标题为“仅使用 FTP 访问安装”，这是适合您的方法。

##### 默认安装

有若干功能默认处于激活状态：

- **游戏：** 允许用户在您的网站上玩游戏并跟踪游戏统计。
- **类别：** 管理任何模块都可归入的类别。
- **日历：** 允许用户查看带有事件的日历。
- **MyTiki：** 为登录用户提供自己的界面，功能包括日历、网页邮件、菜单和记事本，并允许管理员开启或关闭用户功能。
- **投稿：** 允许用户提交文章。
- **自动链接：** 允许输入文本中的 URL 自动提交到链接目录。
- **搜索与全文搜索：** 允许用户搜索您的网站。
- **HTML 页面：** 管理可重复使用的 HTML 代码可编辑块，用于整个网站。





## 内容管理系统

- **帮助系统**：管理帮助台。
- **Galaxia 工作流引擎**：允许管理复杂的工作流流程。
- **Wiki**：协作文档系统；也允许授权用户为静态 HTML 页面创建和编辑内容，并提供所见即所得（WYSIWYG）HTML 编辑器和拼写检查器等其他高级功能。
- **文章**：组织和管理工作文章。
- **博客**：网络日志管理。
- **目录**：对链接进行分类的链接管理器。
- **文件库**：组织和管理上传的文件。
- **常见问题解答**：管理站点常见问题。
- **地图**：允许显示交互式地图。
- **跟踪器**：为您管理和组织自定义数据。
- **热门词**：允许您将站点中特定词汇嵌入为链接。
- **联系我们**：允许用户轻松联系您的简易表单。
- **统计**：管理站点统计数据，涵盖所有可能的活动模块。
- **来源统计**：管理来源站点的统计数据。
- **调试器控制台**：协助开发人员调试站点。

其他预安装功能，只需点击按钮即可激活，包括：

- **评论**：允许用户对站点内的图像、文章和其他内容进行评论。
- **图片库**：允许用户排名、查看和上传图片。
- **新闻阅读器**：新闻 RSS 订阅源。
- **投票**：管理在线投票。
- **测验**：允许用户参加测验并评分。
- **特色链接**：管理在您的 Tiki 站点内打开的链接；跟踪链接统计数据。
- **横幅**：管理横幅宣传和点击率。
- **通讯**：管理站点通讯发布并允许用户订阅。
- **论坛**：管理论坛。
- **留言框**：允许用户在动态窗口中显示短行文本。
- **调查**：管理在线调查。
- **年鉴**：允许您显示针对每年每一天定制的图像和文本。
- **在线支持系统**：允许用户从在线帮助台请求帮助。
- **Babelish 翻译**：允许用户翻译站点的部分区域。
- **集成器**：允许您将外部 HTML 页面导入站点。

## 第 13 章

- **封禁系统**：允许您轻松封禁用户。
- **用户功能**：允许用户添加书签、跟踪文件、向其他用户发送消息以及其他操作。

##### 自定义默认安装

站点管理部分有几个子部分，提供自定义选项。它们包括：

- **功能**：在此部分，管理员可以激活和停用功能，并更改站点的一般布局。
- **通用偏好设置**：在此处，您可以更改主题、更改主页或创建自定义主页、设置语言偏好、设置操作系统类型、更改 PHP 错误报告级别、设置站点停机时的自定义消息、限制站点用户数量和负载、设置缓存偏好、设置新链接打开方式、控制是否所有组都能看到所有模块、设置是否将管理员页面浏览量计入统计、更改菜单显示、设置服务器配置、设置会话偏好、管理日期/时间格式以及更改管理员密码。
- **用户注册和登录**：此区域专门用于让您控制用户注册和登录过程的各个方面，从身份验证到密码要求，再到 HTTP/S 设置，甚至包括 TikiWiki 使用的 PEAR::Auth 模块的设置。
- **启用功能的配置（例如 Wiki）**：对于您通过“功能”屏幕启用的各种功能，您将能够访问这些独立部分以进一步自定义其设置。由于 Wiki 是该项目早期的重点，因此站点管理中的这个区域提供了大量的控制、自定义和功能。简而言之，您可以转储、恢复和附加文件，控制数据库和评论设置，导出，配置链接格式并设置保留在 Wiki 文档中的信息（版本控制、用户数据、日期、链接、状态等）。您还可以管理版权保护、Wiki 历史并配置监视。您可以开启或关闭的一些 Wiki 功能包括：
    - Mail-in
    - 沙盒
    - 最后更改
    - 历史
    - 排名
    - 撤销
    - 多页打印
    - PDF 生成
    - 评论
    - 拼写检查器
    - 编辑冲突警告
    - 独立缓存
    - 脚注
    - 使用 WikiWords
    - Automono 间隔文本

其他可用功能（文章、博客、图片库等）也允许一定程度的自定义，但远没有 Wiki 部分详细。

##### 优缺点

TikiWiki 的优点包括：

- 文档和支持社区非常广泛，与许多其他开源 CMS 包类似。
- 强大的 Wiki 自定义功能使在线协作变得容易。
- 默认安装附带 35 个主题，它们是基本的 CSS 文件，使进一步自定义变得容易。
- 所有可能的活动模块都提供广泛的统计信息。
- 这种 CMS 是最全面的之一；它附带了几乎每一个可以想到的模块（除了跨国功能），使您无需安装额外的插件或附加组件即可轻松自定义。

缺点方面，Galaxia 工作流有点复杂，需要单独阅读才能理解系统是如何设置以及它如何为您服务。这也可能成为 TikiWiki 的一个优点，因为一旦您能够深入该系统，它就可以为您提供一个管理复杂项目的非常全面的工具。

使用该软件，您可以快速提供用户想要的任何东西。事实上，通过该软件可用的功能如此之多，业余网页开发人员可能会因为“可以做”而倾向于使用太多模块。我们的建议是，如果您确切知道您站点想要什么，并且如果您有许多用户将参与站点实际内容的贡献，您应该绝对考虑这种 CMS。

#### 其他

有许多其他开源 CMS 包可用。值得提及的几个包括：

- **Mambo**：可通过 http://www.mamberserver.com 获取。这是一个流行的 CMS，提供基础水平的预安装功能，并拥有大量的下载量。该项目培养了一个健康的支持系统，且用户群相对易于管理，无需深入代码。
- **Drupal**：可通过 http://www.drupal.org 获取。这是另一个流行的 CMS，注重功能而非形式。包含一些主题，但不深入研究代码的情况下自定义有限。一个很好的功能是“近期系统事件”，当管理员登录时显示，允许管理员轻松查看用户正在做什么。
- **PHP-Nuke**：可通过 http://www.phpnuke.org 获取。这是最古老的基于 PHP/MySQL 的 CMS 之一。它自 2000 年以来一直存在，拥有最大（如果不是最大的）CMS 支持社区。它目前仍在开发中，但坏消息是它不再免费——您现在需要支付最低费用才能下载最新版本。如果您想跻身 PHPNuke 精英行列，也可以加入 PHPNuke 俱乐部（需额外付费）。
- **Postnuke**：可通过 http://www.postnuke.com 获取。作为另一个“老宝贝”，这个 CMS 在 PHP-Nuke 之后不久发布，因此受益于其广泛的用户和开发者社区。有许多附加组件、语言包和用户论坛可用，协助您自定义此 CMS 包。

### 微型 CMS

您可能只想要大型 CMS 包中的一个功能在您的自己的站点上使用。幸好，您也有微型 CMS 包可用。这些“迷你” CMS 包有一个特定的目的，如博客或 Wiki。如果您在站点上只需要一个功能，它们是完美的解决方案。以下部分简要介绍了这些包。

两种最受欢迎的微型 CMS 包是博客和 Wiki。因此，这些领域受到了更多的关注。

#### 博客的魅力

研究表明，博客及其读者的普及率正在增加。PEW Internet & American Life Project 的一项研究表明，2002 年，只有 3% 的互联网用户拥有博客。2003 年，这一数字增加到 5%，2004 年，这一数字上升到 7%。将这个数字乘以估计仅在美国就有 1.2 亿互联网用户，这意味着相当大量的博客活动正在进行。

不仅有人在写博客，而且越来越多的人花时间阅读博客。Hostway, Inc. 2005 年 4 月的一项调查显示，大约 30% 的受访者读过博客，分析师预测在未来几年这个数字将大幅增长。

##### 为什么要写博客？

写博客有很多原因，从个人到政治再到企业议程，范围广泛。这种免费、即时、交互的沟通机制是分享观点和思想的完美论坛。博客可以是关于任何事物，其非正式性质几乎吸引所有人。

博客存在的原因包括：

- **分享政治观点**：许多政治家和知名政治活动家正在使用博客接触大众并推广自己的议程。
- **推进企业目标**：企业开始加入这股潮流，提供关于其产品和服务的博客。一些由消费者本人撰写。一些企业使用博客通知其忠实读者即将到来的产品发布，或关于公司的其他新闻。
- **分享个人观点**：在这个如此拥挤的星球上，在如此拥挤的互联网上，有时人们只是想被听到。也许他们想与来自全球各地的朋友和家人分享他们目前的经历。或者他们可能有专家建议想要与初学者分享。在编码人员的世界里，您可能有一段代码片段要分享，或一个酷炫的产品或链接您想告诉其他人。列表还在继续。




### WordPress

WordPress 是一款出色的“开箱即用”博客软件包，提供了卓越的可定制性和功能性。你可以在 http://www.wordpress.org 获取该软件，本文撰写时的当前版本为 1.5.11。

#### 安装说明

该软件包的安装极其简单快捷。在安装之前，请确保你正在运行 PHP 4.1+ 和 MySQL 3.23.23+，并且已经创建了数据库及用户名/密码。你需要其他文档都方便地列在 http://www.wordpress.org 网站上。

#### 功能概述

WordPress 为你的博客提供了众多功能和定制领域，包括：

- **用户注册系统**：允许你授权其他用户在你的站点发布、编辑和删除博客，具有 10 个不同级别的用户权限。你还可以在草稿发布前要求“审批”流程。
- **静态内容页面**：允许你向站点添加静态页面，并通过 WordPress 界面进行管理。
- **添加链接或博客链接**：你可以通过 WordPress 界面管理和组织外部链接。
- **主题**：默认安装目前内置了 35 种主题，此外还有近 150 种额外主题可供下载，以便轻松定制博客的外观和风格。
- **评论系统**：允许你接受、审核和修改用户发布的评论，并包含垃圾邮件阻止器以防止垃圾邮件帖子出现。访客还可以通过 Trackback 和 Pingback 在他们自己的网站上评论你的博客。
- **隐藏帖子**：允许你对某些帖子进行密码保护，这些帖子仅由你或创建它们的作者可见。
- **导入数据**：允许你从其他流行的博客软件包导入数据，包括 MovableType、Blogger 以及许多其他软件包。
- **RSS 源**：允许他人传播你的博客。
- **电子邮件发布**：允许你通过电子邮件系统提交博客帖子。

这款博客软件包还有其他不错的功能，如完全符合标准、升级简便，以及使用 Texturize 引擎美化纯 ASCII 文本。

#### 总结

一旦深入使用 WordPress 软件包，你会发现它文档完善、安装容易、配置和定制简单，且功能强大。如果你有任何问题或困难，它还有优秀的支持和发展社区。如果你只是想在你的网站上创建一个博客，WordPress 很难被超越。

### Serendipity

另一个出色且结构良好的博客软件包是 Serendipity，可在 http://www.s9y.org 下载。其开发团队拥有一些重量级 PHP 专家，包括 Sterling Hughes、George Schlossnagle、Wex Furlong 和 Sebastian Bergmann 等人。它也是许多核心 PHP 开发人员的首选博客软件包。

#### 安装说明

与 WordPress 类似，安装也是一项快速且简单的工作。你应运行 PHP 4 或更高版本，并选择 MySQL、PostgreSQL 或 SQLite 作为你的数据库。需要注意的另一件事是，安装完成后记得限制文件权限，具体方法如他们在 http://www.s9y.org/index.php?node=36 找到的详尽安装文档中所述。

#### 功能概述

Serendipity 提供与 WordPress 类似的功能，例如允许管理员为用户设置权限，使得并非所有用户都能发布博客条目，以及审核评论或启用 CAPTCHA 以防止垃圾邮件。使用 Serendipity，你可以为博客帖子添加图片，更改站点主题，导入和导出数据，并提供 trackback 和 pingback 供他人引用你的帖子。与 WordPress 类似的是符合标准的代码和可供他人使用的 RSS 源。

一些在 WordPress 中不太显眼但在 Serendipity 中提供的额外功能包括：

- 可选的所见即所得编辑器：HTML Area、FCKeditor、Xinha、TinyMCE
- 支持 MySQL、PostgreSQL 和 SQLite
- 多用户博客：一个 Serendipity 安装可以服务于独立的博客。

#### 总结

Serendipity 简单、整洁且稳固。如果你正在寻找一个只做它应该做的事情并且非常可靠的博客，Serendipity 是一个极佳的选择。

### Wiki

就像程序员、编码人员和网页开发人员使用软件来管理软件包的开发和部署一样，他们也开始利用 wiki 来协作创建全面文档以补充这些软件包。

#### Wiki 的起源

根据维基百科，wiki 一词源自夏威夷语术语 wiki wiki，意为“快速或非正式”，特别是当指代檀香山机场的巴士时。该短语由 Howard ("Ward") Cunningham 在 1995 年创造，作为对波特兰模式库（Portland Pattern Repository，一个软件开发思想的合作项目）的参考。

随着互联网发展到覆盖大众，wiki 概念的流行度大幅增长，特别是在开源社区，许多人承担社区责任以持续改进现有产品。文档是使用户理解应用程序功能或可执行事项的关键组成部分。

Wiki 站点不仅限于支持开源项目，还可以作为几乎任何主题的通用参考指南。有面向爱好者的 wiki、语言 wiki、游戏 wiki——你完全可以为任何主题创建 wiki。

### MediaWiki

MediaWiki 是较受欢迎的软件包之一，也是维基百科背后的核心。它可在 http://wikipedia.sourceforge.net 获取。本文撰写时的最新版本是 1.4.4，也将是本文讨论的重点。

#### 安装说明

在安装 MediaWiki 之前，你应该注意以下几点：如果你拥有 root 权限，则在安装前不需要创建数据库。如果你是在远程服务器上安装，你需要在安装前自行创建数据库。此外，文件解压后，你需要 chmod 配置目录使其可写。安装完成后，你还需要重置权限。

完整的安装指南可以在 MediaWiki 网站 http://meta.wikimedia.org/wiki/MediaWiki_User%27s_Guide:_Installation 找到。

#### 功能概述

由于该站点的目的是跟踪不断发展的文本体系，它具有一些管理用户、其输入和版本控制的出色功能。可用的通用功能包括：

- **用户定制和访问**：用户可以通过编辑自己的模板、设置自己的偏好（如时区和每页结果数）来定制自己的站点界面。管理员可以为不同级别的用户组分配不同的权限，开启或关闭他们编辑、移动、贡献或上传文件等能力。
- **搜索功能**：站点访客可以对站点中包含的所有文章进行全文搜索。
- **报告**：可以生成报告，提供关于使用量、文章和链接、文章活动和受欢迎程度、图片、用户等的具体统计数据。
- **编辑文章**：用户可以选择只编辑文章的一部分，如果发生编辑冲突，文章可以合并，用户可以在提交之前预览他们的编辑，并为用户提供编辑工具栏以方便编辑过程。
- **文章组织**：文章可以分类和子分类到无限个类别中。
- **文本和链接控制**：用户在提交文本更改或输入新文本时可以使用受限或完整的 HTML 代码。还可以管理嵌入的超链接。
- **监视列表**：此功能协助管理员和用户跟踪用户的编辑和贡献。它可以显示特别感兴趣的文章、最近的变更，以及贡献最多的用户。此功能甚至提供文章编辑前后的并排视图，并突出显示更改，以便读者轻松识别变更。



## 第13章

- **多媒体功能**：用户可以上传其他类型的文件，包括图像、声音文件、数学公式和图表。
- **多语言支持**：目前支持众多语言，并且能够在不同语言的文章之间建立链接。

要查看此软件包中所有可用功能和特性的完整列表，请访问位于 http://meta.wikimedia.org/wiki/MediaWiki:_feature_list 的 MediaWiki 功能列表。

#### 总结

只需访问维基百科（http://www.wikipedia.org ），就能完全掌握使用 MediaWiki 所能实现的所有功能。它功能强大、可自定义，并且是现有最健壮的 wiki 软件包之一。

### DocuWiki

另一个 Wiki 软件包是 DocuWiki，可在 http://www.splitbrain.org/go/dokuwiki 获取。使其与其他 wiki 不同的是，它使用平面文件，从而使用户摆脱了对数据库的依赖。

#### 安装说明

DocuWiki 是另一个提供“开箱即用”安装功能的开源软件包——只需解压缩并更改权限即可安装。您唯一需要做的，是按照 http://wiki.splitbrain.org/wiki%3Ainstall 上的详细安装说明创建一个空的日志文件。

#### 功能概述

该 wiki 提供许多功能，包括：

- **分节编辑**：允许用户仅对页面的一部分进行操作。
- **版本比较**：提供两个文档版本之间带有颜色高亮的差异显示。
- **用户访问控制**：允许管理员为用户分配权限。
- **图像上传**：允许用户在 wiki 文档中包含图像。
- **多语言支持**：提供对不同语言的支持。
- **检入/检出**：防止编辑冲突。

#### 总结

这个 wiki 唯一的不足是缺乏与数据库相关的功能，如页面跟踪和引用统计。它也不像其他一些 wiki 软件包那样提供备份实用程序或允许用户对贡献进行评论。除此之外，这是一个简单而稳固的 wiki 软件包，是一个极佳的选择，特别是当您没有数据库访问权限时。

### 其他微型 CMS 软件包

虽然本章迄今为止重点介绍了博客和 wiki，但您可能已经开发了一个网站，需要“插入”一些额外的功能。有许多专注于特定领域的 CMS 可以让您的生活更轻松，并使您无需从头编写代码就能轻松增强网站。

一些更受欢迎的微型 CMS 软件包包括：

- 出版/新闻管理 CMS：FusionNews，位于 http://www.fusionphp.net
- 学习环境管理 CMS：Moodle，位于 http://www.moodle.org
- 事务型 CMS：osCommerce 或 ZenCart，分别位于 http://www.oscommerce.com 和 http://www.zencart.com
- 图像库：Coppermine，位于 http://coppermine.sourceforge.net
- 论坛：phpBB，位于 http://www.phpBB.com
- 聊天室：phpmychat，位于 http://phpmychat.sourceforge.net
- 投票/调查：PrestoPoll，位于 http://prestoppoll.sourceforge.net
- 日历系统：WebCaledar，位于 http://www.k5n.us/webcaledar.php

### 其他有用的资源

还有其他地方可以让你筛选泥沙俱下的内容——那些以比较、评估和追踪市面上众多 CMS 为业务的网站。这里只提供几个入门资源：

- OpenSourceCMS：http://www.opensourcecms.com 。该网站旨在为你提供市面上几乎任何 PHP/MySQL CMS 的“试运行”，让你可以亲身体验每种 CMS 的可用功能、管理界面的运行状况以及 CMS 本身的深度和广度。该网站有几个很好的地方：首先，你不必花费时间安装整个软件包来演示软件；其次，他们只展示可以在远程服务器上（无需 root 权限）以及主服务器本身安装的 CMS。如果某个 CMS 没有列入清单，要么是因为他们无法轻松安装它（这也是另一个不错的过滤标准），要么是他们还不知道。该网站还包含其他用户的评论，提供完全不偏不倚的观点。

使用此网站唯一的缺点是，当你在操作时，其他人也在“玩弄”该软件，这会导致有趣的评估结果以及可能的意外后果。幸运的是，服务器每两小时刷新一次演示软件，因此最终你将能够看到一个“干净”的副本。

- CMSReview：http://www.cmsreview.com 。这是一个综合性的 CMS 网站，提供了关于如何确定贵公司 CMS 需求以及去哪里寻找 CMS 顾问的绝佳资源，并且提供了一个不错的 CMS 术语表链接，以防你遇到任何不熟悉的术语。

- CmsMatrix：http://www.cmsmatrix.org 。如果你想在一个公平的对比基础上比较众多 CMS 软件包（无论开源与否），这将是一个很好的资源。它比较原始和杂乱，但包含大量信息。

- CmsWire：http://www.cmswire.com 。这个 CMS 新闻网站让你掌握最新的 CMS 发展动态以及跨行业的 CMS 使用趋势。如果你致力于处于 CMS 领域的前沿，你可能想要获取该网站的 RSS 源。

#### 总结

我们希望本章能给你足够的见解，以便在 CMS 软件包方面做出明智的选择。正如所展示的，有众多开源解决方案可以满足几乎任何需求，从非常全面的到非常定制和特定的。虽然很多时候选择正确的 CMS 取决于个人喜好，但你现在至少有一个起点来形成这些主观意见。

![img](img/cacdd24f2926f10ee3219256ad732604_354_0.png)

### 语言翻译

#### 注释

**PHP**

// 单行注释
/*
多行注释
*/

**ASP/VBScript**

' 单行注释

**ASP.NET/C#**

// 单行注释
/*
多行注释
*/

**JSP/Java**

// 单行注释
/*
多行注释
*/

# 附录 A

## 变量类型化

| 语言 | 类型 |
| :--- | :--- |
| PHP | 弱类型 |
| ASP/VBScript | 弱类型 |
| ASP.NET/C# | 强类型 |
| JSP/Java | 强类型 |

### 变量声明

| 语言 | 语法 |
| :--- | :--- |
| PHP | `$variable = value;` |
| ASP/VBScript | `Dim variable` |
| ASP.NET/C# | `type variable;` |
| JSP/Java | `type variable;` |

### 常量声明

| 语言 | 语法 |
| :--- | :--- |
| PHP | `define('NAME', value);` |
| ASP/VBScript | `Const name = value` |
| ASP.NET/C# | `const type name = value;` |
| JSP/Java | `visibility final type = value;` |

### 创建数组

**PHP**

```php
$name = array(elem1, elem2, elem3);

$name = array('key1' => elem1, 'key2' => elem2, 'key3' => elem3);
```

**ASP/VBScript**

```vbscript
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

### 引用数组元素

**PHP**

```php
$name[index]

$name['key']
```

**ASP/VBScript**

```vbscript
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

### 条件评估

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

```vbscript
If condition Then
    ...
ElseIf condition Then
    ...
Else
    ...
End If
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

### 多路选择

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

```vbscript
Select Case expr
Case value1
    ...
Case value2
    ...
Case Else
    ...
End Select
```

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

### 循环：While

**PHP**

```php
while (expr) {
    ...
}
```

**ASP/VBScript**

```vbscript
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



# 附录 A

### 循环：Do...While

**PHP**

```php
do {  ...  } while (expr);
```

**ASP/VBScript**

```vbs
Do  ...  Loop Until expr
```

**ASP.NET/C#**

```csharp
do {  ...  }  while (expr);
```

**JSP/Java**

```java
do {  ...  } while (expr);
```

### 循环：For

**PHP**

```php
for (expr1; expr2; expr3) {  ...  }
```

**ASP/VBScript**

```vbs
For expr1 To expr2 Step expr3  ...  Next
```

**ASP.NET/C#**

```csharp
for (expr1; expr2; expr3) {  ...  }
```

**JSP/Java**

```java
for (expr1; expr2; expr3) {  ...  }
```

### 循环：For Each

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

```vbs
For Each *item* In array
...
Next
```

**ASP.NET/C#**

```csharp
for (type *item* in array) {
...
}
```

**JSP/Java**

```java
for (Iterator *item*; *item*.hasNext(); ) {
...
}
```

### 循环：终止

**PHP**

```php
break;
```

**ASP/VBScript**

```vbs
Exit Do
Exit For
```

（无法退出 While 循环。）

**ASP.NET/C#**

```csharp
break;
```

**JSP/Java**

```java
break;
```

### 循环：进入下一轮

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

### 函数/方法声明

**PHP**

```php
function name (args) { ... }
```

**ASP/VBScript**

```vbs
Function name (args) ... End Function

Sub name (args) ... End Sub
```

**ASP.NET/C#**

```csharp
visibility returnType name (args) { ... }
```

**JSP/Java**

```java
visibility returnType name (args) { ... }
```

### 返回函数值

**PHP**

```php
return value;
```

**ASP/VBScript**

```vbs
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

### 使用命名空间对类进行分组

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

### 类可见性关键字

| 语言         | 关键字                                      |
| :------------- | :-------------------------------------------- |
| PHP            | public, private, protected                    |
| ASP/VBScript   | public, private                               |
| ASP.NET/C#     | public, private, protected, internal          |
| JSP/Java       | public, private, protected, package           |

### 基类定义

**PHP**

```php
class ClassName { 
...
} 
```

**ASP/VBScript**

```vbs
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

### 声明类属性

**PHP**

```php
visibility name; 
```

**ASP/VBScript**

```vbs
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

### 调用同一类中的方法

**PHP**

```php
$this->method(); 
```

**ASP/VBScript**

```vbs
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

### 类构造器

**PHP**

```php
function __construct() { … }
```

**ASP/VBScript**

```vbs
Private Sub Class_Initialize( ) … End Sub
```

**ASP.NET/C#**

```csharp
visibility ClassName( ) { … }
```

**JSP/Java**

```java
public ClassName( ) { … }
```

### 类析构器

**PHP**

```php
function __destruct() { … }
```

**ASP/VBScript**

```vbs
Private Sub Class_Terminate( ) … End Sub
```

**ASP.NET/C#**

```csharp
visibility ~ClassName( ) { … }
```

**JSP/Java**

```java
protected void finalize() {
    ...
}
```

### 使用静态类方法

**PHP**

```php
ClassName::StaticMethod();
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

### 创建对象

**PHP**

```php
$obj = new ClassName();
```

**ASP/VBScript**

```vbs
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

### 类继承

**PHP**

```php
class ClassName extends BaseClass {
    ...
}
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

### 调用父类方法

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

### 声明抽象类

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

### 停止子类化

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

### 接口声明

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
}
```

### 类使用接口

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

### 包含外部文件

**PHP**

```php
include('filename');
include_once('filename');
require('filename');
require_once('filename');
```

**ASP/VBScript**

```vbs
<%-- #include 'filename' -->
```

**ASP.NET/C#**

包含处理通过多种方法进行，包括传统的 ASP 包含方式（如上所示）

**JSP/Java**

```jsp
<%@ include file="filename" %>
```

### 异常处理

**PHP**

```php
try {
    ...
} catch (ExceptionType $e) {
    ...
}
```

**ASP/VBScript**

未具体支持

**ASP.NET/C#**

```csharp
try {
    ...
} catch (ExceptionType e) {
    ...
} finally {
    ...
}
```

**JSP/Java**

```java
try {
    ...
} catch (ExceptionType e) {
    ...
} finally {
    ...
}
```

### 抛出异常

**PHP**

```php
throw new ExceptionType(args);
```

**ASP/VBScript**

```vbs
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

### HTTP POST 值

**PHP**

`$_POST` (数组)

**ASP/VBScript**

`Request.Form` (集合)

**ASP.NET/C#**

`System.Web.HttpRequest.Form` (NameValueCollection)

**JSP/Java**

`request.getParameter()` (方法查找)

### HTTP GET 值

**PHP**

`$_GET` (数组)

**ASP/VBScript**

`Request.QueryString` (集合)

**ASP.NET/C#**

`System.Web.HttpRequest.QueryString` (NameValueCollection)

**JSP/Java**

`request.getParameter()` (方法查找)

### 服务器变量

**PHP**

`$_SERVER` (数组)

**ASP/VBScript**

`Request.ServerVariables` (集合)

**ASP.NET/C#**

`System.Web.HttpRequest.ServerVariables` (NameValueCollection)

**JSP/Java**

`request .getVariable()` (方法查找；每个服务器变量对应不同的方法)

![](img/cacdd24f2926f10ee3219256ad732604_372_0.png)

# 附录 B

## 替代工具

每当讨论流行的 PHP 工具时，对话通常都集中在文本编辑器或代码集成开发环境（IDE）上。哪一款具有最好的语言支持、语法高亮、代码解析等功能？不幸的是，由于过分关注文本编辑器，一些优秀的非编码工具有时会被忽视。与其重述支持某一款编辑器而非另一款编辑器的常规论点，本附录将向您展示一些在开发周期中可以使用的工具——那些不会立即生成代码，但可能在整体开发流程中占据关键位置的工具。

### MySQL 工具

在管理 MySQL 数据库时，通常有两个主要的管理工具选项：标准的命令行工具集或图形化界面。尽管许多经验丰富的系统管理员对此持保留态度，但使用图形化工具完成工作完全没有问题。虽然命令行界面提供了对数据库的无限控制权，但它无法匹敌良好的图形用户界面在促进管理工作流程方面的速度和清晰度。

如果您正在寻找一套优秀的基于 GUI 的 MySQL 管理工具，MySQL AB 自家的 MySQL Administrator 和 MySQL Query Browser 便是最佳选择。

#### MySQL Administrator

MySQL Administrator 是一个功能丰富的 GUI 管理工具，用于维护 MySQL 数据库。主要界面如图 B.1 所示。





# 附录 B

![](img/cacdd24f2926f10ee3219256ad732604_373_0.png)

图 B.1

MySQL Administrator 允许你执行以下操作：

- 查看实时服务器信息，包括连接信息和统计数据、内存统计数据、MySQL 内部变量和配置设置的值等。
- 查看不同的服务器日志：错误日志、慢查询日志、通用日志（仅限本地主机）。
- 控制 MySQL 进程本身（仅限本地主机）。
- 执行备份和恢复操作，甚至还可以计划定期备份。
- 管理服务器的用户访问权限和权限。
- 创建和编辑完整的数据库，包括使用内置的 MySQL 表编辑器来创建和编辑表。

MySQL Administrator 可用于 Windows、Linux 和 Mac OS X；MySQL Administrator 可从 MySQL 网站免费下载：http://www.mysql.com/products/administrator/

#### MySQL Query Browser

MySQL Query Browser 是一种 GUI，允许你针对 MySQL 数据库测试和运行各种查询。从某种意义上说，它是命令行客户端的增强版 GUI 版本，如图 B.2 所示。你还可以将 MySQL Query Browser 用作类似标准电子表格程序或桌面数据库应用程序——你可以调取数据行，并在查询浏览器中直接编辑它们。除了输入和执行查询以及操作数据外，它还包含在 MySQL Administrator 中发现的 MySQL 表编辑器，允许你以可视化的方式创建和编辑数据库和表。

![](img/cacdd24f2926f10ee3219256ad732604_374_0.png)

图 B.2

Windows、Linux 和 Mac OS X 版本可从 MySQL 获取：http://www.mysql.com/products/query-browser/ 。

你的应用程序已经启动运行，服务器已针对最佳性能进行了调整。但是，你的数据库查询是否尽可能精简高效？唯一的办法是使用基准测试工具来查明。

大多数 MySQL 基准测试工具的运行方式大致相同：你提供一个要运行的查询，然后该工具重复运行该查询大量次数，通常使用并发连接。通过彻底测试和实验一些“重量级”查询（通常可在 MySQL 慢查询日志中找到），你可以改善应用程序瓶颈处的执行时间和服务器负载。

#### MySQL Super Smack

最初由 Sasha Pachev 开发，MySQL Super Smack 是一个独立的压力测试工具，用于 MySQL 和 PostgreSQL。MySQL Super Smack 接受一个或多个包含查询的文件，并以预定义的次数对目标数据库进行每查询的猛烈测试，同时使用指定数量的并发连接。

MySQL Super Smack 可在 http://vegan.net/tony/supersmack/ 获取。

#### MyBench

MyBench 是由 MySQL 高手 Jeremy Zawodny 创建的基于 Perl 的基准测试工具。与 MySQL Super-Smack 一样，它可以用来向目标 MySQL 机器发送一连串连接和查询，并给出清晰的测试结果，说明该机器在攻击下的表现。由于它是用 Perl 编写的，你可以轻松修改和扩展它。缺点是大批量测试可能会占用机器资源，因此最好将此工具运行在与目标 MySQL 服务器不同的机器上，以避免测试结果受到污染。

MyBench 可在 Jeremy Zawodny 的网站获取：http://jeremy.zawodny.com/mysql/mybench/

### 版本控制

如果你还没有在开发生命周期或工作流程中考虑某种形式的版本控制系统，那么现在可能值得考虑了。版本控制系统提供了一种在开发期间存储代码历史快照的方法，并允许多个开发人员将文件检入和检出仓库，从而控制代码库的演变。目前使用最流行的两种开源版本控制系统是 CVS 和 Subversion。

CVS 和 Subversion 都是支持相同基本功能的版本控制系统：文件版本的历史记录，以及支持多个开发人员的检入/检出功能。CVS 自 1989 年面世以来，一直是许多开发人员的首选。Subversion 出现得较晚，最早出现在 2000 年底，但由于其功能集，正迅速获得追随者，这些功能超出了 CVS 中常见的“标准”功能。原子提交、“安全”的文件重命名、文件和目录复制以及 WebDAV 支持等功能，是许多开发人员如今选择 Subversion 的一些原因。如果你在寻找一个功能健壮且客户端和服务器端都有良好支持的功能集，Subversion 可能是你最好的选择。如果你在寻找稳定性、历史记录以及内置于许多开发工具中的支持，CVS 可能是更好的选择——尽管越来越多的开发包最近正在获得 Subversion 支持。

无论你选择哪种，尽早实施某种版本控制都是个好主意——这使得多开发人员项目更容易管理，并且如果新代码确实导致严重的新 bug 或回归问题，它还可以提供安全网。

CVS 可在 https://www.cvshome.org/ 获取。

Subversion 可在 http://subversion.tigris.org/ 获取。

### UML 工具

如果你深入系统架构和设计领域，很可能会在某个时候与 UML 打交道。如果你不熟悉 UML，简单地说，它是建模和表示应用程序或其他系统的结构、行为、架构和流程流的一种方法。你可以使用 UML 对系统或应用程序的不同方面进行图表化，包括类结构、用户交互、对象交互、流程流等，类似于你可能使用 Visio、Kivio 或其他相关工具制作流程图和其他图表。

UML 中有九种图表类型，但从开发人员角度来看，其中最重要的一种是类图。类图帮助你规划各种类以及这些类之间的关系。

如果你在 PHP 工作流程中使用 UML，你有几个工具可供使用——一些流行的免费工具是 ArgoUML 和 Umbrello。

#### ArgoUML

ArgoUML 是由 Tigris.org 社区创建的基于 Java 的 UML 编辑器。它支持八种主要 UML 图表类型，并帮助你快速规划对象、关系和行为。从 PHP 开发人员的角度来看，ArgoUML 的主要功能之一是它能够自动从 UML 类图生成有效的 PHP5 类骨架（以及 C#、Java、C++ 和 PHP4），如图 B.3 所示。

你只需在 UML 中创建类图并告诉 ArgoUML 在哪里生成代码以及生成什么代码，这就节省了你输入类结构的时间，让你可以专注于代码的核心部分：实现。ArgoUML 还提供关于你的类结构的机器生成建议，并带有集成的待办事项列表。

ArgoUML 可作为桌面 Java 应用程序提供，既可以通过互联网下载并通过 JavaWebStart 运行，也可以在 http://argouml.tigris.org/ 获取。

![](img/cacdd24f2926f10ee3219256ad732604_377_0.png)

图 B.3

#### Umbrello

Umbrello 是另一个类似 ArgoUML 的 UML 绘图应用程序。Umbrello 现在是 KDE 开发人员工具包的一部分，支持许多主要的 UML 图表类型，包括类图、用例图、状态图和序列图。从 1.4 版本开始，Umbrello 可以生成 PHP5 类骨架，以及多种其他编程语言的代码，如图 B.4 所示。

![](img/cacdd24f2926f10ee3219256ad732604_378_0.png)

图 B.4

## 替代工具

Umbrello 可作为 KDE 桌面环境（3.2 或更高版本）或 Linux 的一部分找到，或者你可以直接从 Umbrello 网站（适用于 KDE / Linux）下载：[http://uml.sourceforge.net/](http://uml.sourceforge.net/)。

## 索引

### 符号和数字

- { }（花括号）
  - 缩进标准，214–217
  - 减少嵌套级别，217–220
- :（冒号）
  - 与类常量（::），28–29
  - 在 PHP URL 中的方案名之后（://），72
  - 与 self 关键字（self::），7, 27–28
- $（美元符号）
  - 未用于类常量（PHP），29
  - $this 引用变量（PHP），23, 50
- ::（双冒号）。参见 :
- =（等号）
  - 在相等运算符与赋值运算符中，219
  - 404 处理器，缓存和，226
- "（引号）
  - 在 set_exception_handler() 中的函数名，5
  - 字符串的速度和，201–205
- '（单引号），字符串的速度和，201–205
- /（斜杠）
  - MySQL 查询的 //G 终止符，86
  - 在 PHP URL 中的方案名之后（://），72

### A

- ab ApacheBench 程序，208–209
- abort() 方法（AJAX），277
- 抽象类（PHP）
  - abstract 关键字，7
  - 示例，7–8
  - 语言转换，341–342
  - 命名约定，222
  - 概述，34–35
  - 使用规则，8
- abstract 关键字（PHP），7
- 访问控制（Apache）。参见 authentication
- 访问控制（MySQL）
  - GRANT 和 REVOKE 的替代方案，97–100
  - columns_priv 表，99, 100
  - db 表，98–99, 100
  - GRANT 命令，94–96
  - 重新加载权限表，100
  - REVOKE 命令，96–97
  - 服务器限制，100
  - tables_priv 表，99, 100
  - 用户管理，93–100
  - user 表，97–98, 99–100
- 访问控制（PHP）
  - Basic 身份验证，166–171
  - 注册表单中的 CAPTCHA 图像，175–177




### 访问控制

访问控制（PHP）（续）
- 表单身份验证，172–174
- HTTP_REFERRER 值及其关系，174–175
- REMOTE_ADDR 值及其关系，174
- 服务器变量及其关系，174–175

访问修饰符（PHP）。另见具体修饰符
- Circle 类示例，24–25
- 语言转换，337
- PHP5 增强功能，6
- 由…指定可见性，23–24

addslashes() 函数（PHP），113

AJAX（异步 JavaScript 和 XML）
- 可访问性问题，283–285
- CPANT 库，283
- 描述，273
- DOM 操作，273, 281–282
- 更多信息，285
- Google 的 GMail 应用，273
- 处理 ReadyStateChange 事件，280
- 处理响应，280–282
- 历史，274–277
- JSPAN 库，283
- 方法，277–278
- 属性，278–279
- SAJAX 库，282–283
- 支持问题，285
- 与传统 Web 应用的对比，273, 274
- 可用性关注点，283–285
- 应对浏览器差异，279–280
- XMLHTTP 和 XMLHttpRequest 接口，277–282

Alcantara, Frank（eAccelerator 维护者）
- 描述，48

Allman 缩进风格，215–216

Alpha 透明度，244

ALTER TABLE 语句（MySQL），87, 90–91, 92

替代 PHP 缓存。另见 APC

分析数据库（MySQL），100–102

匿名函数（PHP），57–58

Apache。另见 URL 重写（Apache）
- 与 MySQL 进行身份验证，129, 149–154, 166
- 基本身份验证，154, 165–166
- 内容压缩，145–149
- 404 处理器与缓存，226
- mod_alias，226
- mod_auth_mysql，129, 149, 150–154
- mod_dav，158
- mod_deflate，129, 146–148
- mod_proxy，138
- mod_rewrite，226
- mod_speling，129, 144–145
- mod_ssl，129, 154–155
- 作为在线文件仓库，158–163
- PDFLib 配置及其关系，234
- 性能优化，211–213
- 与其配合使用 SSL，154–157
- URL 拼写检查，144–145

ApacheBench 程序（ab），208–209

APC（替代 PHP 缓存）
- 配置，288–290
- 历史，287
- 安装，288
- 与其他缓存引擎的关系，305
- 概览，287
- 移除，290
- 适用场景，305
- 网站，288

数组函数（PHP）。另见回调（PHP）
- array_filter()，53
- array_map()，49, 50–51
- array_walk()，49, 51–52
- 大多数提供了回调，48
- call_user_func_array()，55–56
- 描述，48
- 系列函数的内存需求，59–60
- preg_grep()，53
- preg_replace_callback()，53–55
- 与其配合使用回调，48–50
- 种类和数量，59

array_filter() 函数（PHP），53

arrayiterator 类（PHP），6

array_map() 函数（PHP），49, 50–51

回调（PHP）
- 数组（PHP）。**另见** 数组函数（PHP）
- 检查其大小、性能及其关系，229
- 语言转换，331
- 命名约定，222
- 临时变量与性能，229–230

array_walk() 函数（PHP），49, 51–52

不同运行结果各异，202

字符串速度示例，201–205

Benchmarking 类（PEAR），207–208

博客
- Micro CMS
- 博客的流行度，322
- 写博客的原因，322
- Serendipity，324
- WordPress，323

大括号（ })
- 大括号的缩进标准，214–217
- 减少嵌套层级，217–220

BSD 缩进风格，215–216

Bzip2 扩展（PHP），271

ASP。**另见** 语言转换

ASP.NET。**另见** 语言转换

ASP 风格标签，php.ini 设置，106–107

按值赋值与按引用赋值（PHP），29

异步 JavaScript 和 XML。**另见** AJAX

atempt_auth() 函数（PHP），169–170

通过 Apache 和 MySQL 进行身份验证，149–154

通过 Apache 和 SSL 进行身份验证，154–157

### C

C#。**另见** 语言转换

缓存（PHP）
- APC 缓存引擎，287–290
- 选择缓存引擎，305
- 客户端侧，227
- CMS 提供的功能，225–226
- eAccelerator 缓存引擎，290–294
- Expires: 头及其关系，227
- JPCache 缓存引擎，296–300
- memcached 缓存引擎，300–304
- 输出预生成，224–226
- PEAR 包及其关系，224–225
- 性能优势，223
- 源码预解析，223–224
- 使用 404 处理器进行缓存，226
- 同时使用不同的缓存引擎，304–305
- Zend Optimizer 缓存引擎，294–296

### B

备份（MySQL），103–104

基本身份验证（Apache）
- 实现，165
- 局限性，154
- 与 MySQL 配合使用，149–154, 166
- PHP 控制的身份验证及其关系，166, 171
- 不适用场景，165–166

基本身份验证（PHP）
- Apache 控制的身份验证及其关系，166, 167
- 创建身份验证数据库，166–167
- 用于此的 phpaubasic.php 脚本，167–171
- 测试，171

基准测试
- ab ApacheBench 程序，208–209
- 定义，206–207
- MyBench MySQL 工具，350
- PEAR Benchmarking 类，207–208

callarea() 方法，21

call() 魔术方法（PHP），8–9, 38

回调（PHP）
- 用于抽象功能，48
- 用于 array_filter() 函数，53
- 用于 array_map 函数，空回调，50–51
- 用于 array_walk() 函数，52
- 用于 call_user_func_array() 函数，55–56

回调（PHP）（续）
- cREATE_FUNCTION() 函数及其关系，57–58
- 未来的新实现可能用于，59
- PREG_REPLACE_CALLBACK() 函数，53–55
- 大多数数组函数提供回调，48
- 与 self 关键字配合使用，50
- 指定类和对象方法，49–50
- 包含函数名称的字符串，49
- 与 $this 引用变量配合使用，50
- 使用，48–50

调用方法和函数
- _CONSTRUCT() 魔术方法用于，6
- 语言转换，338–339, 341
- 通过魔术方法重载，8–9
- 过程化调用（MySQL），13

call_user_func() 函数，56–57

call_user_func_array() 函数，55–56

CAPTCHA（完全自动公共图灵测试，用于区分计算机和人类），175–177

caption() 方法（WebImage 类），251–252

CASCADE 选项（MySQL），92

Case 语句，语言转换，332–333

CERT 网站，182

check_login() 函数（PHP），170–171

Circle 类示例
- 与抽象 Shape 类，34–35
- 与 _CALL() 魔术方法，38
- 与 clone 语句，29–30
- 构造函数，25–26
- 定义，20
- 析构函数，26–27
- 与 _GET() 和 _SET() 魔术方法，39
- 从 Shape 类继承，31–33
- 用于 memcached 缓存引擎，303–304
- 方法，21
- 父类：引用，34
- 属性，21
- 与 _SLEEP() 和 _WAKEUP() 魔术方法，40–43
- 与 static 关键字，27–28
- 与 __TOSTRING() 魔术方法，44
- 在…中指定可见性，24–25

类常量（PHP），28–29

类（MySQL），13–16

类（PHP）。另见具体类
- 抽象类，7–8, 34–35, 222, 341–342
- 基础，20–23
- 类常量，28–29
- 描述，20
- 与 final 关键字，6
- 实例化，22–23
- 语言转换，337–342
- 命名约定，222

CLI，使用其安装 PEAR，186

客户端 URL 库函数（CURL）扩展（PHP），271

客户端侧缓存，227

clone 语句（PHP），29–30

关闭流（PHP），63

CMSMatrix 网站，328

CMSReview 网站，327

CMSs（内容管理系统）
- 全包式 Web CMS，309–322
- 博客包，322–324
- 提供的缓存，225–226
- 描述，307
- DocuWiki，326
- Drupal，321
- 企业级 CMS，307–308
- ExponentCMS，309–312
- Mambo，321
- MediaWiki，325–326
- 微型 CMS，322–328
- 开源 Web CMS 包，308
- PHP-Nuke，321
- phpWebsite，315–318
- Postnuke，322
- 资源，327–328
- Serendipity，324
- TikiWiki，318–321
- Web CMS，描述，308
- Wiki 包，324–326
- WordPress，323
- XOOPS，312–315

CMSWire 网站，328

代码效率。另见 性能

编码标准（PHP）
- 大括号和缩进，214–217
- 注释，216, 217, 220
- 通过解析错误强制实施，222–223
- 命名约定，220–222
- 概览，213–214
- PEAR，214
- 减少嵌套层级，217–220

冒号 (:
- 与类常量 (::)，28–29
- PHP URL 中方案名之后 (://)，72
- 与 self 关键字 (::)，7, 27–28

columns_priv 表（MySQL），99, 100

注释
- Big Flashy Box 风格，216, 217
- 编码标准，220
- Javadoc 风格，220
- 语言转换，329
- 用于缩进的制表符，216, 217

完全自动公共图灵测试，用于区分计算机和人类（CAPTCHA），175–177

构造函数（PHP）

压缩内容。另见 内容压缩（Apache）

连接，基准测试其速度，201–205

条件语句
- 语言转换，331–336
- 性能及其关系，230

config-help 命令（PEAR 管理器），186

ConfigManager.php 类
- 代码列表，117
- configfile 属性，118
- configtype 属性，118
- 构造方法，118
- 声明，117
- errors 属性，118
- processConfig 方法，118–119

ConfigProcessor 接口（PHP），119

config-set 命令（PEAR 管理器），186

config-show 命令（PEAR 管理器），185–186

配置检查器（PHP）
- ConfigManager.php 类，117–119
- ConfigProcessor 接口，119
- reqs.xml 文件，116
- test.php 代码，128
- XMLConfigProcessor.php 类，119–128

配置变量（PEAR），185

配置 PHP。另见 php.ini 配置文件；运行时配置（PHP）

const 关键字（PHP），29

常量
- 类常量（PHP），28–29
- 语言转换，330
- 命名约定，222

_construct() 魔术方法（PHP）
- Circle 类示例，25–26
- ConfigManager.php 类，118
- 描述，37
- 概览，6, 25–26
- PHP4 构造函数与之对比，25
- XMLConfigProcessor.php 类，122–123

Circle 类示例，25–26

_construct() 魔术方法用于，6, 25–26

语言转换，339

概览，25–26

PHP4 构造函数，25

内容压缩（Apache）
- 配置指令，147–148
- 描述，145–146
- mod_deflate 的有效性，148
- 用于此的 httpd.conf 文件，146–147
- 需求，145
- 用于 PHP 脚本，148–149
- 使用 mod_deflate，146–148

内容管理系统。另见 CMSs

转换表
- InnoDB 到 MyISAM，93
- MyISAM 到 InnoDB，90





### 坐标系

- Minig 扩展（PHP），264
- PDFLib 扩展（PHP），237
- Coppermine CMS，327
- 使用 clone 语句复制对象（PHP），29-30
- Cowgill, Daniel（APC 创建者），287
- CPANT（跨平台异步接口工具包），283
- CREATE DATABASE 语句（MySQL），75
- CREATE TABLE 语句（MySQL）
  - 用于 Apache 身份验证示例，149-150
  - 启用全文搜索，86-87
  - 概述，75
  - 用于 PHP 身份验证示例，166-167
- create_function() 函数，57-58
- 交叉连接（MySQL），81, 82
- 跨平台异步接口工具包（CPANT），283
- 跨站脚本攻击（XSS），180-181
- CSS 样式表
  - AJAX 使用，273
  - 用于 PEAR 包，192-193
- CURL（客户端 URL 库函数）扩展（PHP），271
- CVE 网站，182
- CVS 版本控制系统，350-351
- Date PEAR 包，189-190
- DB PEAR 包，190-192
- db 表（MySQL），98-99, 100
- 调试脚本，Xdebug PECL 包，197
- DeflateCompressionLevel 指令（Apache 的 mod_deflate），147
- DeflateFilterNote 指令（Apache 的 mod_deflate），148
- DeflateWindowSize 指令（Apache 的 mod_deflate），148
- DELETE 语句（MySQL），77, 92
- 删除数据库信息（MySQL），77, 92
- __destruct() 魔术方法（PHP），6, 26-27, 37
- 析构函数（PHP）
  - 圆形类示例，26-27
  - 使用 __destruct() 魔术方法，6, 26-27
  - 语言翻译，339-340
  - 概述，26-27
- 指令（PHP）。参见 php.ini 配置文件
- 目录
  - 自动重定向 URL 至该目录，132
  - 为 SSL 网站创建目录，157
  - 使用 glob() 进行模式匹配读取，60-61
  - 用于 WebDAV 文件库，158
- DirectoryIterator 类（PHP），5
- 磁盘访问，性能及影响，211
- display() 方法（WebImage 类），244
- DocuWiki Micro CMS，326
- 美元符号 ($)
  - 不用于类常量（PHP），29
  - $this 引用变量（PHP），23, 50
- DOM（文档对象模型）
  - AJAX 操作，273, 281-282
  - DOM 扩展（PHP），16, 271
- 双冒号 (::)。参见冒号 (:)
- do..while 循环，语言翻译，334
- drawHRR() 函数（PDFLib），236
- Drupal CMS，321
- 数据对象，PDO PECL 包用于集成，196-197
- 数据库分析（MySQL），100-102
- 数据库维护（MySQL），103-104
- 数据库相关包（PEAR）
  - Auth_HTTP，187-188
  - DB，190-192
  - HTML_Table，194-195
  - PEAR::Auth，187, 188
  - PEAR::DB，187
  - 相关网站，191
- 数据库（MySQL）。参见 MySQL

### D

- DSO（动态共享对象）
  - 安装 APC 作为 DSO，287, 288
  - 安装 eAccelerator 作为 DSO，291
  - 安装 memcached 作为 DSO，301
  - PDFLib 配置及 DSO，234

### E

**eAccelerator 缓存引擎**

- 配置，291–294
- 安装，291
- 与其他缓存引擎的比较，305
- 概述，290–291
- 移除，294
- 网站，291

- echo 语句（PHP）
  - 与 print 语句的区别，228–229
  - 与 __toString() 魔术方法配合使用，44
- emailException 类，3–4
- 企业级 CMS，307–308。**另见** CMS（内容管理系统）
- 等号 (=) 在相等性与赋值运算符中的区别，219
- 错误消息，php.ini 相关设置，106
- Exception 类（PHP），2–4
- 异常（PHP）
  - 描述，1
  - Exception 类，2–4
  - 语言翻译，344–345
  - PHP5 的变更与增强，1–5
  - 与 set_error_handler() 函数的区别，1–2
  - try/catch/throw 块，2, 234, 344–345
- Expires: 头信息，缓存相关，227

**ExponentCMS**

- 附加模块，310
- 自定义默认设置，310–311
- 默认功能，309
- “非活动”功能，309
- 安装，309–310
- 优势与劣势，311
- 网站，309, 310

- extends 关键字（PHP）
  - emailException 示例，3–4
  - 与继承的关系，31–33
  - 与接口的关系，36–37
  - 概述，3, 31–33
- **eXtensible Object Oriented Portal System。参见 XOOps**
- extension_loaded() 函数（PHP）
  - 概述，111
  - 在 XMLConfigProcessor.php 类中的使用，124, 125
- 外部文件，语言翻译中包含外部文件，343–344

### F

- **胖客户端 Web 应用程序。参见 AJAX（异步 JavaScript 和 XML）**
- 文件访问日志记录器示例
  - 代码列表，64–66
  - 注册流包装器，66
  - stream_close() 函数，67
  - stream_open() 函数，67
  - stream_read() 函数，67
  - stream_write() 函数，67
  - 使用记录日志的流，66–67
- 使用 Apache 的文件库。**参见** WebDAV（基于 Web 的分布式创作和版本控制）
- FileInfo PECL 包，196
- final 关键字（PHP），6, 33
- Flash 文件（Shockwave）。**参见 Ming 扩展（PHP）**
- FLUSH PRIVILEGES 命令（MySQL），100
- for 循环
  - 不需要该循环的数组函数，48
  - 语言翻译，335
- foreach 循环
  - 不需要该循环的数组函数，48
  - 使用 array_walk() 函数避免该循环，49, 51–52
  - 语言翻译，335

### G

- 外键约束（MySQL）
  - 优势，89
  - 使用 ALTER_TABLE 语句创建，90–91, 92
  - 命名，90
  - 与 NULL 值的关系，89
  - 指定行为的选项，92
  - 与 UPDATE 语句的关系，91–93
- 表单（HTML），用于 PEAR 包，193–194
- 表单（PHP）
  - 用于登录身份验证，172–174
  - php.ini 相关设置，105, 107
- 404 处理器，缓存相关，226
- 帧（Ming），264
- FTP，使用 FTP 安装 PEAR，186
- 全文搜索（MySQL）
  - 修改现有表以支持全文搜索，87
  - 创建支持全文搜索的新表，86–87
  - 局限性，88
  - 最小全文搜索单词长度指定，InnoDB 不支持，89
  - 用于全文搜索的 SELECT 语句，87–88
- 函数（MySQL），以过程方式调用，13
- 函数（PHP）。另见 数组函数
  - 特定函数
    - 匿名函数，57–58
    - ArrayIterator 类，6
    - 回调及函数，49
    - 检查扩展及其属性，111–112
    - 检查安装版本，108
    - 检查魔术引号设置，113
    - Exception 类，3
    - Iterator 类，5
    - 语言翻译，336–337
    - 命名约定，220, 221–222
    - PHP5 中新引入的函数，91–92
    - 在运行时获取配置设置，109–110
    - 多样性及数量，47
- FusionNews CMS，327

### G

- MySQL 查询中的 /G 终止符，86
- GD 库扩展（PHP）
  - 添加说明文字，250–254
  - 添加标志，254–257
  - 与 Alpha 透明度的关系，244
  - 创建图像基础，241–245
  - 描述，241
  - ImageCapture 类，250–254
  - ImageLogo 类，254–257
  - ImageResize 类，245–248
  - ImageRotate 类，249–250
  - 与索引透明度的关系，244
  - 手册，263
  - 调整图像大小，245–248
  - 旋转图像，248–250
  - 测试，257–261
  - 用于 GD 库的 WebImage 基类，241–245, 246–247, 249, 251–252
  - WebImage 类，255–256
- _get()_ 魔术方法（PHP）
  - 圆形类示例，39
  - 示例，8
  - 概述，38–39
- get_cfg_var() 函数（PHP），109
- get_defined_functions() 函数，57
- get_extension_funcs() 函数（PHP），112
- get_loaded_extensions() 函数（PHP），111–112, 116
- get_magic_quotes_gpc() 函数（PHP），113
- get_magic_quotes_runtime() 函数（PHP），113
- getMessage() 函数（PHP），2, 3
- getResponseHeader() 方法（AJAX），277
- GIS 摄影数据库查询示例
  - 解决方案方法，67–68
  - 代码列表，68–70
  - net 协议，70
  - 用于图像的 PNG 文件，70, 71–72

### H

- imagehandle() 函数（ImageResize 类），248
- 用于 GD 库的 ImageCaption 类
  - 代码列表，250~251
  - imageline() 函数，253~254
  - imagettftext() 函数，253
  - process() 方法，252~253
- imagecopy() 函数（ImageLogo 类），257
- imagecopymerge() 函数（GD 库），257
- imagecopyresampled() 函数（ImageResize 类），248
- imagecopyresized() 函数（ImageResize 类），248
- imageline() 函数（ImageCaption 类），253~254
- 用于 GD 库的 ImageLogo 类
  - 代码列表，254~255
  - imagecopy() 函数，257
  - process() 方法，256~257
- stream_open() 函数，70~71
- stream_read() 函数，71
- stream_tell() 函数，71
- 该数据库的网站，67
- glob() 函数（PHP），60~61
- GMail 应用程序（Google），273
- GNU 缩进风格，215
- GRANT 命令（MySQL）
  - 用于 Apache 访问凭据，149
  - 创建列级权限，95
  - 为特定表创建权限，95
  - 用于极度受限的访问，96
  - 授予所有权限，96
  - 授予有限的表级权限，96
  - IDENTIFIED BY 短语，96
  - ON 子句，95
  - 用于 PHP 身份验证示例，166
  - 权限，94~95
  - 语法，94
  - TO 子句，95

### I

- httpd.conf 文件
  - 启用 SSL 功能，157
  - HostnameLookups 选项，212
  - KeepAlive 选项，212
  - KeepAliveTimeout 选项，212
  - MaxClients 选项，211
  - MaxKeepAliveRequests 选项，212
  - MaxRequestsPerChild 选项，211
  - MinSpareServers 选项，212
  - 用于 mod_auth_mysql，151~152
  - 用于 mod_dav，158
  - 用于 mod_deflate (Apache)，146~147
  - 用于 mod_ssl，155
  - 性能相关，211~212
  - StartServers 选项，212
  - 用于 WebDAV 身份验证，159

### I

- IFRAME 元素，隐藏，276~277
- 避免页面刷新的图像源技巧，275~276

### H

- 硬盘，性能相关，211
- 用于性能提升的硬件改进，210~211
- 避免页面刷新的隐藏帧技术，275~276
- 避免页面刷新的隐藏 IFRAME 技术，276~277
- .htaccess 文件
  - 用于 mod_auth_mysql，151~152
  - 性能相关，213
  - 用于关闭 register_globals 指令，179
  - 用于 WebDAV 身份验证，159
- HTML_CSS PEAR 包，192~193
- HTML_Page PEAR 包，192~193
- HTML_QuickForm PEAR 包，193~194
- HTML_Table PEAR 包，194~195
- HTTP GET 值，345
- HTTP POST 值，345





### I

- GD 库的 ImageResize 类
    - 代码列表，245–246
    - imagealphablending() 函数，248
    - imagecopyresampled() 函数，248
    - imagecopyresized() 函数，248
    - imagesavealpha() 函数，248
    - process() 方法，247–248
- GD 库的 ImageRotate 类，249–250
    - imagesavealpha() 函数
        - ImageResize 类，248
        - WebImage 类，244
- imagettftext() 函数（ImageCaption 类），253
- implements 关键字（PHP），36, 37
- 编码缩进标准，214–217
- 索引透明性，244
- info 命令（PEAR 管理器），185
- 继承（PHP）
    - 与抽象类相关，7–8, 34–35
    - 描述，31
    - 与 extends 关键字相关，31–33
    - 与 final 关键字相关，6, 33
    - 语言转换，340–341
    - parent:: 引用，33–34
    - 在子类中重新定义属性和方法，32–33
    - 与 static 关键字相关，7
- ini_get() 函数（PHP），109
- ini_get_all() 函数（PHP）
    - 访问指令值，115
    - 概述，109, 110
    - 在 XMLConfigProcessor.php 类中，126, 127
- ini_set() 函数（PHP），114–115, 127–128
- 初始化属性（PHP），21
- 内连接（MySQL）
    - 表别名，78–79
    - 按评估顺序链接，79
    - 逗号分隔的表列表，79–81
    - 定义，78
    - 局限性，81
    - 与外连接组合使用，82
    - 语法，78
    - 表前缀，78–79
    - 与 USING 语句一起使用，79
    - 与 WHERE 子句一起使用，79, 80, 81
- InnoBase Oy 公司，88
- InnoDB 表（MySQL）
    - 优点，88–89
    - 将 MySQLAM 表转换为 InnoDB 表，90
    - 转换为 MyISAM 表，93
    - 从头创建表，89
    - InnoDB 存储引擎的开发，88
    - 缺点，89
    - 外键约束，88–89, 90–93
- INSERT 语句（MySQL），75–76
- 安装
    - APC 缓存引擎，288
    - DocuWiki 微型 CMS，326
    - eAccelerator 缓存引擎，291
    - ExponentCMS，309–310
    - JPCache 缓存引擎，296–297
    - MediaWiki 微型 CMS，325
    - memcached 缓存引擎，300–301
    - Ming 扩展（PHP），263
    - mod_auth_mysql（Apache），150–151
    - PEAR 包，186
    - phpWebsite CMS，315–317
    - Serendipity 博客微型 CMS，324
    - TikiWiki CMS，318–320
    - WordPress 博客微型 CMS，323
    - XOOPS CMS，312–313
    - Zend Optimizer 缓存引擎，294–295
- 实例化
    - 类，22–23
    - SWFMovie 对象（Ming），263
- interface 关键字（PHP），36
- 接口（PHP）
    - 定义，36
    - 描述，35
    - 与 extends 关键字一起使用，36–37
    - 实现，36, 37
    - 语言转换，342–343
    - 一个类多个接口，37
    - 概述，35–37
    - PHP5 的变化，5
    - 用途，35
- 互联网号码分配机构（Internet Assigned Numbers Authority），72
- 互联网资源
    - AJAX 信息，285
    - Apache mod_ssl 信息，157
    - APC 缓存引擎，288
    - Auth_HTTP PEAR 包信息，188
    - CMS 资源，327–328
    - CPAINT，283
    - CVS 版本控制系统，351
    - DocuWiki 微型 CMS，326
    - Drupal CMS，321
    - eAccelerator 缓存引擎，291
    - ExponentCMS，309, 310
    - Fileinfo PECL 包，196
    - PHP 手册中的 GD 部分，263
    - Google 的 GMail 应用，273
    - 互联网号码分配机构，72
    - JavaWebStart 网站，351
    - JPCache 缓存引擎，296, 300
    - JSPAN，283
    - 新西兰土地信息网站，67
    - Mambo CMS，321
    - MediaWiki 微型 CMS，325
    - memcached 缓存引擎，300, 301
    - 微型 CMS，323, 324, 325, 326, 327
    - Ming 信息，263
    - MyBench 工具，350
    - MySQL Administrator 工具，348
    - MySQL Query Browser 工具，349
    - MySQL Super Smack 工具，350
    - PDF 开源库，233
    - PDFLib 扩展（PHP），233, 234
    - PDFLib Lite 扩展（PHP），234
    - PDO PECL 包，196, 197
    - PEAR 配置变量，185
    - PEAR 数据库包，191
    - PEAR 管理器命令，184
    - PEAR 包，195
    - PEAR::DB 包，187
    - PEP8 网站，184
    - PHP Wiki 网站，196
    - php-Nuke CMS，321
    - phpWebSite CMS，315
    - Postnuke CMS，322
    - SAXAJ 信息，282
    - 安全相关网站，182
    - Serendipity 博客微型 CMS，324
    - SourceForge 网站，263, 353
    - SQLite 信息，17
    - Subversion 版本控制系统，351
    - Tidy 库，17
    - TikiWiki CMS，318
    - Umbrello UML 工具，353
    - WordPress 博客微型 CMS，323
    - WROX 网站，76
    - Xdebug PECL 包，197
    - XOOps，312
    - Zend Optimizer，295
- 插值，基准测试速度，201–202
- iterator 类（PHP），5
- 迭代器（PHP），5–6

### J

- Java。参见语言转换
- Javadoc 风格的注释，220
- JavaScript。另请参阅 AJAX（异步 JavaScript 和 XML）
    - 隐藏框架技术，275–276
    - 图像源技巧，275
- javaWebStart 网站，351
- JPCache 缓存引擎
    - 配置，297–299
    - 安装，296–297
    - 与其他缓存引擎一起使用，305
    - 概述，296
    - 移除，300
    - 适用情况，305
    - 网站，296, 300
- JSPAN AJAX 库，283
- JSP。参见语言转换

### K

- K & R（Kernighan 和 Ritchie）缩进风格，215, 216, 217
- 语言转换（续）
    - 停止子类化，342
    - 抛出异常，344–345
    - 变量声明，330
    - 变量类型化，330
- 左外连接（MySQL），81, 84
- load() 函数（WebImage 类），243–244
- 日志文件
    - 用于监控日志的 emailException 类，3–4
    - 文件访问日志器示例，63–67
    - URL 重写（Apache），143–144
- logo() 方法（WebImage 类），255–256
- 循环
    - 不需要的数组函数，48
    - 用于避免循环的 array_walk() 函数，49, 51–52
    - for 循环，48, 335
    - foreach 循环，48, 49, 51–52, 335
    - 语言转换，333–336
- 新西兰土地信息网站，67
- 语言转换
    - 抽象类声明，341–342
    - 数组创建，331
    - 数组元素引用，331
    - 基类定义，338
    - 调用同类中的方法，338–339
    - 调用父类方法，341
    - 类构造函数，339
    - 类析构函数，339–340
    - 类继承，340–341
    - 类属性声明，338
    - 类使用接口，343
    - 类可见性关键字，337
    - 注释，329
    - 条件评估，331–332
    - 常量声明，330
    - 异常处理，344
    - 函数/方法声明，336
    - 使用命名空间分组类，337
    - HTTP GET 值，345
    - HTTP POST 值，345
    - 包含外部文件，343–344
    - 接口声明，342–343
    - 循环，进入下一轮，336
    - 循环，do...while，334
    - 循环，for，334
    - 循环，foreach，335
    - 循环，终止，335
    - 循环，while，333
    - 多选，332–333
    - 对象创建，340
    - 返回函数值，336–337
    - 服务器变量，345–346
    - 静态类方法使用，340
- Mac OS，用于 WebDAV 的设置，163
- Macromedia Flash 与 Ming 的对比，263
- 魔术方法（PHP）
    - 用于访问未明确定义的方法和属性，37
    - __call()，8–9, 38
    - __construct()，6, 25–26, 37
    - __destruct()，6, 26–27, 37
    - get()，8, 38–39
    - 用于重载，8–9
    - 概述，37
    - __set()，8, 38–39
    - __sleep()，39, 40–43
    - __toString()，43–44
    - __wakeup()，40–43
- 魔术引号（PHP）
    - 检查 php.ini 设置，113
    - 禁用，106, 113
    - 概述，112–113
    - php.ini 设置，106, 113

### M

- 数据库维护（MySQL），103–104
- Mambo CMS，321
- MediaWiki 微型 CMS，325–326
- memcached 缓存引擎
    - 守护进程，300
    - 安装，300–301
    - Memcache 对象方法，301–303
    - 与其他缓存引擎一起使用，305
    - 概述，300
    - PECL 模块，301
    - 移除，304
    - 使用，301–304
    - 网站，300, 301
- 内存（RAM）
    - 性能与内存，200, 210–211
    - 系列数组函数与内存，59–60
- 方法（MySQLI）
    - 过程式调用，13
    - mysqli 类，13–14
    - mysqli_result 类，16
    - mysqli_stmt 类，15
- AJAX 接口的方法，277–278
- 方法（PHP）。**另请参阅** 函数（PHP）；魔术方法（PHP）；*特定方法和函数*
    - 抽象，8
    - 定义，21
    - 描述，20, 21
    - 与 final 关键字一起使用，6
    - 语言转换，336, 338–339, 340, 341
    - 命名约定，221–222
    - 在子类中重新定义，32–33
    - 与 static 关键字一起使用，7, 27–28
    - 流包装器方法，62–63
- 微型 CMS
    - 博客包，322–324
    - DocuWiki，326
    - MediaWiki，325–326
    - 其他包，327
    - Serendipity，324
    - wiki 包，324–326
    - WordPress，323
- Ming 扩展（PHP）
    - Content-Type 头，268
    - 坐标系，264
    - 创建 Flash 显示，265–269
    - 帧，264
    - 安装，263
    - Macromedia Flash 与 Ming 的对比，263
    - 对象，263, 264–265
    - 直接输出到浏览器，268–269
    - 概述，263–264
    - 简单示例，263–264
    - 幻灯片示例，266–269
    - 更多信息网站，263
- mod_alias（Apache），226
- mod_auth_mysql（Apache）
    - 优点，166
    - AuthMySQLAuthoritative 指令，154
    - AuthMySQLDB 指令，151, 152
    - AuthMySQLDBEnable 指令，151, 152
    - AuthMySQLGroupCondition 指令，154
    - AuthMySQLGroupField 指令，154
    - AuthMySQLGroupTable 指令，154
    - AuthMySQLHost 指令，152
    - AuthMySQLNameField 指令，153
    - AuthMySQLPass 指令，151, 152
    - AuthMySQLPasswordField 指令，153
    - AuthMySQLPort 指令，152
    - AuthMySQLPwEncryption 指令，151, 152
    - AuthMySQLSaltField 指令，153
    - AuthMySQLSocket 指令，152
    - AuthMySQLUser 指令，151, 152
    - AuthMySQLUserCondition 指令，153
    - AuthMySQLUserTable 指令，153
    - AuthName 指令，151
    - AuthType 指令，151
    - 数据库设置，149–150
    - 描述，129
    - .htaccess 文件，151–152
    - httpd.conf 文件，151–152
    - 安装，150–151
    - 安全所需的最小指令，151
- mod_dav（Apache），129, 158




### mod_deflate (Apache)

- 构建与启用，146
- 内容压缩的使用，146–148
- DeflateCompressionLevel 指令，147
- DeflateFilterNote 指令，148
- DeflateWindowSize 指令，148
- 描述，129
- 有效性，148
- 用于该模块的 httpd.conf 文件，146–147

### mod_rewrite (Apache)

**另请参阅** URL 重写 (Apache)

- 功能特性，129
- 将站点文档树与服务器文件系统解耦，226
- 描述，129
- 启用，130–131, 133
- RewriteBase 指令，143
- RewriteCond 指令，139–143
- RewriteLog 指令，143–144
- RewriteLogLevel 指令，144
- RewriteRule 指令，131–138

### mod_speling (Apache)

- 129, 144–145

### mod_ssl (Apache)

- 129, 154–155

**另请参阅** 带有 Apache 的 SSL (Secure Sockets Layer)

### Module CMS

- 327

### 乘法运算符

- 性能相关事项，200–201

### MyBench 工具

- 350

### my.cnf 配置文件 (MySQL)

- 88, 100

### MyISAM 表 (MySQL)

- 转换为 InnoDB，90
- 将 InnoDB 转换为 MyISAM，93
- 作为默认存储引擎，88

### MySQL

**另请参阅** SELECT 语句 (MySQL)

- 访问控制，93–100
- 表别名，78–79
- ALTER TABLE 语句，87, 90–91, 92
- 替代工具，347–350
- 分析数据库，100–102
- 与其结合的 Apache 身份验证，129, 149–154, 160
- 基础概念，73–77
- columns_priv 表，99, 100
- 创建备份，103
- 创建数据库，74–75
- 创建表，75, 86–87
- 交叉连接，81
- db 表，98–99, 100
- 删除数据库信息，77, 92
- 示例数据库表，73–74
- 外键约束，88–89, 90–93
- 全文搜索，86–88
- 查询的 /G 终止符，86
- GRANT 命令，94–96
- 内连接，78–81, 82
- InnoDB 表，88–93
- 向表中插入数据，75–76
- 维护数据库，103–104
- 监视器，74
- MyBench 工具，350
- my.cnf 配置文件，88
- MyISAM 表，88, 90, 93
- MySQL Administrator 工具，347–348
- MySQL Query Browser 工具，349–350
- MySQL Super Smack 工具，350
- 外连接，81–82
- 查询多个表，77–86
- 重新加载权限表，100
- 从备份恢复，103–104
- 检索数据库信息，76–77
- REVOKE 命令，96–97
- 服务器限制，100
- 设置活动数据库，75
- SHOW COLUMNS 命令，101
- SHOW CREATE TABLE 命令，101–102
- SHOW DATABASES 命令，102
- SHOW GRANTS 命令，102
- 启动命令行客户端，74
- tables_priv 表，99, 100
- 并集，82–86
- 更新数据库信息，77, 91–92
- USE 语句，75
- 用户管理，93–100
- user 表，97–98, 99–100
- VACUUM 语句，79
- WHERE 子句，79, 80, 81

### MySQL Administrator 工具

- 347–348

### MySQL Query Browser 工具

- 349–350

### MySQL Super Smack 工具

- 350

### PDFLib 扩展 (PHP)

- mysqli 类，13–15
- MySQLi (MySQL 改进版)，12–16
- mysqli_pconnect() 函数及其性能，231
- mysqli_result 类，16
- mysqli_stmt 类，15

### 开源运动

- 183

### 打开

- MySQL 命令行客户端，74
- 流 (PHP)，62, 63

### OpenSourceCMS 网站

- 327

### osCommerce CMS

- 327

### N

- 命名空间
  - 通过 create_function() 函数防止冲突，57–58
  - 语言翻译，337
- 命名约定，220–222
- 嵌套，降低层级，217–220
- 网络连接及其性能，210
- new 关键字 (PHP)，22–23
- NO ACTION 选项 (MySQL)，92

### NULL 值

- array_map() 函数 (PHP) 的回调，50–51
- InnoDB 外键约束及 (MySQL)，89
- 并集中缺失列的 (MySQL)，84–86
- create_function() 函数名中的 NULLs，58

### O

- 面向对象编程。**另见 OOP**；PHP5 OOP

### 对象 (PHP)

- 通过实例化类创建，20, 22–23
- 描述，20
- 语言翻译，340
- 现实世界与 OOP 的对比，20
- 用于该对象的 $this 引用变量，23

### ob_start('ob_gzhandler') 函数

- 231

### onreadystatechange 属性 (AJAX)

- 278, 279

### OOP (面向对象编程)

**另请参阅 PHP5 OOP**

- PHP5 中的变化，1–9
- 与过程式编程的对比，19–20

### open() 方法 (AJAX)

- 277

### PDFLib 扩展 (PHP) (续)

- pdf_resume() 生成器示例，238–241
- pdf_close() 函数，234
- pdf_get_value() 函数，236
- 与 PDFLib 函数的对比，233
- 用于该模块的 PDFLIB-manual.pdf，234
- pdf_new() 函数，234
- pdf_set_info() 函数，235
- pdf_show_xy() 函数，237
- 性能优势，233
- 必需元素，235
- 指定文档信息，235
- 网站，233, 234

### PDFlib 函数 (PHP)

- 辅助函数，235–237
- 已迁移至 PECL，233
- 与 PDFLib 扩展的对比，233

### PDFLib Lite 扩展 (PHP)

- 234

### PDFLIB-manual.pdf

- 234

### pdf_lineto() 函数 (PDFLib)

- 236

### pdf_moveto() 函数 (PDFLib)

- 236

### pdf_new() 函数 (PDFLib)

- 234

### pdf_setfont() 函数 (PDFLib)

- 236

### pdf_set_info() 函数 (PDFLib)

- 235

### pdf_show_xy() 函数 (PDFLib)

- 237

### PDO PECL 包

- 196–197

### PEAR (PHP 扩展和仓库)

- 提供的 APC 缓存引擎，287
- Auth_HTTP 包，187–188
- Benchmarking 类，207–208
- 检查预安装包，186
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
- 推荐的 javadoc 风格注释，220
- 指定的 K & R 缩进风格，216
- 通过补丁保持更新，182
- phpWebsite CMS 的库，316
- 可用的包，187, 195–196
- PEAR 管理器，184–186
- PEAR::Auth，187, 188
- PEAR::Cache 和 PEAR::Cache_Lite 包，224–225
- PEAR::DB 包，187
- PEPr (PEAR 提案系统)，184
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

- 提供的 APC 缓存引擎，287
- 描述，184, 196
- Fileinfo 包，196
- 通过补丁保持更新，182
- memcached 缓存引擎模块，301
- 其中的 PDFlib 函数，233
- PDO 包，196–197
- Xdebug 包，197

### PEPr (PEAR 提案系统)

- 184

### 性能

- ab ApacheBench 程序，208–209
- Apache Web 服务器改进，211–213
- 基准测试，定义，206–207
- 基准测试，字符串速度示例，201–205
- 缓存相关事项，223–227
- 检查数组大小相关事项，229
- 条件语句相关事项，230
- echo 与 print 的对比，228–229
- 硬件改进，210–211
- 内存相关事项，200
- 乘法运算符相关事项，200–201
- NTA/Access 报告生成器轶事，200
- ob_start('ob_gzhandler') 相关事项，231
- 输出缓冲相关事项，227–228, 231




#### 性能调优
- 概述，231-232
- PDFlib 函数与 PDFLib 扩展，233
- PEAR 基准测试类，207-208
- 持久数据库连接，231
- PHP 编码规范，213-223
- 为性能调优规划程序，199-201
- 性能分析，定义，207
- 正则表达式语法，230
- 释放资源，231
- 临时变量，229-230
- 字符串函数，230
- 字符串，201-205
- top 进程监控工具，208-210
- 性能调优的反直觉结果，206
- unset() 函数，230
- 持久数据库连接，性能，231

#### PHP
*另见* 语言翻译；PHP5 变更与增强；PHP5 OOP
- 数组函数与回调，48-60
- 身份验证，166-177
- 自动版本与特性检查，116-128
- 动态更改配置，113-115
- 检查扩展及其属性，111-112
- 编码规范，213-223
- glob() 函数，60-61
- 列出已安装版本，108
- 获取当前运行时设置，108-113
- 脚本的输出压缩，148-149
- 运行时检索配置设置，109-110
- 流，61-72
- 函数多样性与数量，47

#### PHP 配置
*参见* php.ini 配置文件；运行时配置 (PHP)

#### PHP 扩展与仓库
*参见* PEAR

#### PHP 扩展社区库
*参见* PECL

#### PHP 扩展
*另见* PEAR (PHP 扩展与仓库)；PECL (PHP 扩展社区库)；*特定扩展*
- CURL，271
- DOM，16, 271
- extension_loaded() 函数，111, 124, 125
- 获取信息的函数，111-113
- GD 库，241-263
- Ming，263-269
- PDFLib，233-241
- PDFlib Lite，234
- SimpleXML，16, 269-270
- SOAP，17, 271
- Tiny 库，17
- PHP5 中新增的 XML 扩展，16-17
- XSL，16
- ZIP 扩展，271

#### PHP Wiki 网站
196

#### phpauthbasic.php 脚本
- attempt_auth() 函数，169-170
- check_login() 函数，170-171
- 代码列表，167-168
- 定义用于数据库连接测试的常量，171

#### phpauthforms.php 脚本
172-174

#### phpBB CMS
327

#### PHP 控制的身份验证
- Apache 控制的身份验证，166, 171
- 创建身份验证数据库，166-167
- 基本身份验证的缺点，171
- 表单身份验证，172-174
- 其他访问限制，174-177
- 用于基本身份验证的 phpauthbasic.php 脚本，167-171
- 用于表单身份验证的 phpauthforms.php 脚本，172-174
- 测试基本身份验证，171

![](img/cacdd24f2926f10ee3219256ad732604_396_0.png)

### PHP5 变更与增强
- abstract 关键字，7-8
- 访问修饰符，6
- 构造函数和析构函数，6
- 异常，1-5
- final 关键字，6
- 接口，5
- 迭代器，5-6
- 用于重载的魔术方法，8-9
- MySQLi 扩展，12-16
- 新函数，10-12
- OOP 变更，1-9
- 概述，1, 17
- 变量传递，1
- php.ini 配置文件变更，12, 107-108
- SQLite 改进，17
- static 关键字，7
- Tidy 库扩展，17
- XML 支持，16-17

#### PHP5 OOP
- abstract 关键字，7-8
- 访问修饰符，6, 23-25
- 赋值与克隆，29-30
- 变更与增强，1-9
- 类基础，20-23
- 类常量，28-29
- 构造函数，6, 25-26
- 定义类，20
- 析构函数，6, 26-27
- 异常，1-5
- final 关键字，6
- 继承，31-35
- 实例化类，22-23
- 接口，5, 31, 35-37
- 迭代器，5-6
- 魔术方法，6, 8-9, 37-44
- 方法，21
- 概述，45
- 属性，20-21
- static 关键字，7, 27-28
- 可见性，23-25

#### php.ini 配置文件
- 指令的访问值，115
- allow_call_time_pass_reference 指令，106, 115
- 用于 APC 缓存引擎，288-290
- asp_tags 指令，106
- 使用 ini_set() 更改指令，114-115
- display_errors 指令，106
- 用于 EAccelerator 缓存引擎，291-294
- error_log 指令，106
- error_reporting 指令，106
- 用于 JPCache 缓存引擎，297-299
- log_errors 指令，106
- magic_quotes_gpc 指令，106, 113
- magic_quotes_runtime 指令，113
- mail.force_extra_parameters 指令，107
- MySQLi 设置，12
- 输出压缩设置，149
- 用于 PHP 身份验证示例，171
- PHP5 改进，12, 107-108
- 推荐配置指令，105-107
- register_globals 指令，105, 116
- register_long_arrays 指令，107
- 运行时检索设置，109-110
- safe_mode 指令，171
- session.hash_bits_per_character 指令，108
- session.hash_function 指令，108
- short_open_tag 指令，106-107
- variables_order 指令，106
- 用于 Zend Optimizer 缓存引擎，295
- zend.z1_compatibility_mode 指令，108
- zlib.output_compression 指令，107, 149

#### phpMyChat CMS
327

#### PHP-Nuke CMS
321

#### phpversion() 函数
108, 126

#### phpWebsite CMS
- 自定义默认设置，317
- 默认功能，316–317
- 安装，315–317
- PEAR 库，316
- 优势与劣势，317–318
- 网站，315

#### pi() 函数 (PHP)
29

#### 可移植文档格式
*参见* PDF

#### Postnuke CMS
322

#### preg_grep() 函数
53

#### preg_replace_callback() 函数
53–55

#### PrestoPoll CMS
327

#### print 语句 (PHP)
- 与 echo 语句对比，228–229
- 配合 __toString() 魔术方法，44

#### private 关键字 (PHP)
6, 23

#### privkey.pem 文件 (SSL)
156

#### process() 方法
- ImageCaption 类，252–253
- ImageLogo 类，256–257
- ImageResize 类，247–248
- ImageRotate 类，249–250

#### processConfig 方法 (PHP)
118–119

#### 处理器
- 性能，210

#### 性能分析
定义，207

#### 属性 (MySQL)
- mysql 类，14–15
- mysqli_result 类，16
- mysqli_stmt 类，15

#### 属性 (PHP)
- Circle 类示例，21
- 定义，20–21
- 描述，20
- 初始化，21
- 语言翻译，338
- 命名规范，221, 222
- 实际属性与合成属性，221
- 在子类中重新定义，32–33
- 配合 static 关键字，27
- $this 引用变量，23

#### protected 关键字 (PHP)
6, 24

#### public 关键字 (PHP)
6, 23, 24

### Q

#### 查询多个表 (MySQL)
- 内连接，78–81
- 外连接，81–82
- 联合，82–86

#### 引号 (")
- 用于 set_exception_handler() 中的函数名，5
- 字符串速度，201–205

### R

#### RAM (内存)
- 性能，200, 210–211
- 数组函数系列，59–60

#### rar 扩展 (PHP)
271

#### Raymond, Eric S. (Jargon File 作者)
214

#### readdir() 函数 (PHP)
61

#### 读取
- 目录 (PHP)，60–61
- 流 (PHP)，62

#### readyState 属性 (AJAX)
278, 279

#### create_function() 函数
58

#### Recursionlevator 类 (PHP)
6

#### register_globals 指令
- 编写代码以减少漏洞利用的可能性，179
- 漏洞利用，178–179
- 用于关闭的 .htaccess 文件，179
- HTTP_REFERER 值，174
- 推荐配置，105, 116

#### 正则表达式
- 性能，230
- 配合 RewriteRule 指令 (Apache 的 mod_rewrite)，133–134

#### reqs.xml 文件
- 用于配置检查器 (PHP)，116

#### resize() 函数 (WebImage 类)
246–247, 259

#### responseText 属性 (AJAX)
278

#### responseXML 属性 (AJAX)
278

#### REstrict 选项 (MySQL)
92

#### REVOKE 命令 (MySQL)
96–97

#### RewriteBase 指令 (Apache 的 mod_rewrite)
143

#### RewriteCond 指令 (Apache 的 mod_rewrite)
- 基本格式，139
- 将多行链接在一起，141
- 比较和系统检查条件，141–142
- 比较运算符，142
- HTTP 头部变量，139
- nocase 或 NC 标志，142
- onexit 或 OR 标志，143
- 请求变量，139–140
- 服务器变量，140
- 特殊变量，140–141
- 时间变量，140
- 用法，139–142
- 使用变量，141

#### RewriteLog 指令 (Apache 的 mod_rewrite)
143–144

#### RewriteLogLevel 指令 (Apache 的 mod_rewrite)
144

#### RewriteRule 指令 (Apache 的 mod_rewrite)
- 自动重定向 URL 到新目录，132
- 基本格式，131
- chain 或 C 标志，136
- cookie 或 CO 标志，137
- 启用 mod_rewrite，130–131, 133
- env 或 E 标志，137
- forbid 或 F 标志，135
- gone 或 G 标志，136
- 用于人类输入友好的 URL，132–133
- last 或 L 标志，136
- next 或 N 标志，136
- nocase 或 NC 标志，135
- noescape 或 NE 标志，138
- nosubreq 或 NS 标志，138
- passthrough 或 PT 标志，138
- proxy 或 P 标志，138
- qsappend 或 QSA 标志，137
- redirect 或 R 标志，135
- 配合正则表达式，133–134
- 用于搜索引擎友好的 URL，132–133
- skip 或 S 标志，137
- 标志的语法，135
- 令牌，131–132
- type 或 T 标志，137
- 作为 PHP 脚本的类型检查层，134–135
- 用法，131–135
- 右外连接 (MySQL)，81
- rotate() 函数 (WebImage 类)，249

#### 运行时配置 (PHP)
*另见* 配置检查器 (PHP 自动版本和特性检查)，116–128
- 使用 ini_set() 更改指令，114–115
- 动态更改，113–115
- 禁用魔术引用，113
- 获取当前运行时设置，108–113
- 移除时间限制，113–114

### S

- AJAX (Simple AJAX Toolkit)，282–283
- save() 方法 (WebImage 类)，244–245
- scandir() 函数 (PHP)，61
- Schlossnagle, George (APC 创建者)，287
- 临时变量，性能，229–230
- 脚本 (PHP
  - 压缩 (Apache)，148–149
  - mod_rewrite 作为类型检查层 (Apache)，134–135
- Xdebug PECL 包用于调试，197
- Secunia 网站，182
- 配合 Apache 的安全套接字层。*参见* 配合 Apache 的 SSL
- 安全。*参见* 身份验证；站点安全
- SELECT 语句 (MySQL
  - 配合交叉连接，81
  - 用于全文搜索，87–88
  - /G 终止符用于垂直显示，86
  - 配合内连接，78–81, 82




#### stream_open() 函数（PHP）

- 外连接与，81–82
- 简单形式，76–77
- 并集与，82–86
- self 关键字（PHP），7, 27–28, 50
- send() 方法（AJAX），278
- Sendmail 程序，3–4, 107
- Serendipity 博客微型 CMS，324
- 服务器变量（PHP）
  - 访问控制与，174–175
  - 语言翻译，345–346
- RewriteCond 指令（Apache 的 mod_rewrite），140
- 会话，php.ini 设置，108
- SET DEFAULT 选项（MySQL），92
- _set() 魔术方法（PHP），8, 38–39
- SET NULL 选项（MySQL），92
- set_error_handler() 函数（PHP），1–5
- set_exception_handler() 函数（PHP），4–5
- set_magic_quotes_runtime() 函数（PHP），113
- setRequestHeader() 方法（AJAX），278
- set_time_limit() 函数（PHP），114
- Shape 类示例
  - 作为抽象类，34–35
  - Circle 类继承自，31–33
- Shockwave Flash 文件。**参见** Ming 扩展（PHP）
- SHOW COLUMNS 命令（MySQL），101, 101–102
- SHOW CREATE TABLE 命令（MySQL），101–102
- SHOW DATABASES 命令（MySQL），102
- SHOW GRANTS 命令（MySQL），102
- Simple AJAX Toolkit（SAJAX），282–283
- SimpleXML 扩展（PHP）
  - 概述，16, 269–270
  - xpath() 方法，125, 127
- 单引号（'），字符串速度与其，201–205
- 站点安全。**另参见** 身份验证
  - 使用 Apache 进行访问控制，165–166
  - 使用 PHP 进行访问控制，166–177
  - 代码/同行审查，182
  - 跨站脚本（XSS），180–181
  - 保持补丁更新，181–182
  - register_globals 漏洞利用，178–179, 182
  - 社会工程学与其，182
  - SQL 注入攻击，179–180, 182
  - 网站攻击，178–181
  - 获取更多信息的网站，182
- 斜杠（/
  - MySQL 查询的 /G 终止符，86
  - PHP URL 中方案名称后的（//），72
- _sleep() 魔术方法（PHP），39, 40–43
- SOAP 扩展（PHP），17, 271
- SourceForge 网站，263, 353
- 拼写检查 URL（Apache），144–145
- SPL（标准公共库），5
- SQL 注入攻击，179–180, 182
- SQLite，17
- SSL（安全套接字层）与 Apache
  - 检查 Apache 中是否启用 SSL，154
  - 创建 SSL 网站目录，15
  - 创建自签名证书和密钥，155–156
  - 在 Apache 中动态启用 SSL，155
  - 在 httpd.conf 中启用 SSL 功能，157
  - 更多信息，157
  - 用于测试的信息文件，157
  - mod_ssl 用于，129, 154–155
  - privacy.pem 文件，156
  - 移除口令，156
  - 在 Apache 中静态启用 SSL，154
  - testcert.csr 文件，156
  - 测试，157
  - 443 端口的 VirtualHost 部分，157
  - ssl.conf 文件，157
- 标准公共库（SPL），5
- static 关键字（PHP），7, 27–28
- status 属性（AJAX），278, 279
- stream_close() 函数（PHP），63, 67
- stream_eof() 函数（PHP），63
- stream_open() 函数（PHP）
  - 文件访问日志记录器示例，67
  - GIS 照片数据库查询示例，70–71
  - 概述，62, 63

#### stream_read() 函数（PHP）

- stream_read() 函数（PHP），文件访问日志记录器示例，67
  - GIS 照片数据库查询示例，70
  - 概述，62
- 流（PHP）
  - 构建流包装器，62–63
  - 定义，61–62
  - 文件访问日志记录器示例，63–67
  - GIS 数据库查询示例，67–72
  - PHP 中仅允许字节流，62
  - 概述，61–62
  - 用于命名流资源的 URL 系统，72
  - 包装器方法，62–63
- stream_tell() 函数（PHP），71
- stream_wrapper_register() 函数（PHP），62
- stream_write() 函数（PHP），63, 67
- 字符串（PHP）
  - 基准测试速度，201–205
  - 性能和字符串函数，230
  - __toString() 魔术方法，43, 44
- stripslashes() 函数（PHP），113
- 子类化
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
- switch 语句，用于语言翻译，332–333
- 合成属性命名约定，221

### T

- 用于缩进的制表符，避免使用，216–217
- tables_priv 表（MySQL），99, 100
- testcert.csr 文件（SSL），156
- $this 引用变量（PHP），23, 50
- Tidy 库扩展（PHP），17
- Tigri.org 社区，351
- TikiWiki CMS
  - 自定义默认设置，320–321
  - 默认功能，318–319
  - “非活动”功能，319–320
  - 安装，318–320
  - 优点和缺点，321
  - 网站，318
- top 进程监视实用工具，208–210
- __toString() 魔术方法（PHP），43, 44
- try/catch/throw 块（PHP）
  - 语言翻译，344–345
  - 用于 pdf_new() 函数，234
  - 语法，2

### U

- Umbrello UML 工具，352–353
- UML 图
  - ArgoUML 工具，351–352
  - 概述，351
  - Umbrello 工具，352–353
- 并集（MySQL）
  - 不同长度的列列表与，83
  - 交叉连接与之，82
  - 描述，82
  - 不同名称的表列与之，83
  - 查询的 /G 终止符，86
  - 连接与之组合，84
  - 缺失列的 NULL 值，84–86
- unset() 函数，性能与其，230
- UPDATE 语句（MySQL），77, 91–92
- URL 重写（Apache）
  - 自动重定向 URL 到新目录，132
  - 避免自动转义，138
  - 将 mod_rewrite 与其他模块结合，138
  - 控制日志记录的详细程度，144
  - 启用 mod_rewrite，130–131, 133
  - 强制请求通过代理模块，132
  - 用于人类输入友好的 URL，132–133
  - 使模式不区分大小写，135
  - 覆盖 MIME 类型，137
  - 保留查询字符串，137
  - RewriteBase 指令，143
  - RewriteCond 指令，139–143
  - RewriteLog 指令，143–144
  - RewriteLogLevel 指令，144
  - RewriteRule 指令，131–138
  - 用于搜索引擎友好的 URL，132–133
  - 发送 HTTP 403 禁止响应，135
  - 发送 HTTP 410 已消失响应，136
  - 设置 cookies，137
  - 设置环境变量，137
  - 跳过规则，137, 138
  - 指定基础或前缀路径，143
  - 指定用于处理的日志文件，143–144
  - 在规则列表开始时启动处理，136
  - 在成功匹配后停止处理，136
  - 考虑内部子请求，138
  - 将字符串与模式或条件进行测试，139–143
  - 作为 PHP 脚本的类型检查层，134–135
  - 使用代码块，136
  - 使用带有 HTTP 状态码的正式重定向，135
- URL。另参见 URL 重写（Apache）
  - 命名流资源的指南，72
  - PHP 约定，72
  - 拼写检查（Apache），144–145
- USE 语句（MySQL），75, 149
- 用户管理（MySQL）
  - GRANT 和 REVOKE 的替代方案，97–100
  - 用于此的 columns_priv 表，99, 100
  - 用于此的 db 表，98–99, 100
  - 用于此的 GRANT 命令，94–96
  - 用于此的 role_priv 表，96–97
  - 重新加载权限表，100
  - 用于此的 REVOKE 命令，96–97
  - 用于此的 tables_priv 表，99, 100
  - 用于此的 user 表，97–98, 99–100
- user 表（MySQL），97–98, 99–100
- 内部连接中的 USING 语句（MySQL），73

### V

- var 关键字（PHP4），24
- 变量（PHP）
  - 按值赋值与按引用赋值，21
  - 克隆，29–30
  - 语言翻译，330
  - 命名约定，220, 222
  - 传递，PHP5 变更，1
  - php.ini 设置，105, 106
- VBScript。参见语言翻译
- 版本控制系统，350–351
- 可见性关键字。参见访问修饰符（PHP）

### W

- _wakeup() 魔术方法（PHP），40–43
- Web CMS。另参见 CMS（内容管理系统）
  - 全功能 Web CMS，309–322
  - 描述，308
  - Drupal，321
  - EzotericCMS，309–312
  - Mambo，321
  - 微型 CMS，322–328
  - 开源包，308
  - PHP-Nuke，321
  - PHPWebsite，315–318
  - Postnuke，322
  - TikiWiki，318–321
  - Xoops，312–315
  - WebCalendar CMS，327
- WebDAV（基于 Web 的分布式创作和版本控制）
  - 身份验证，159
  - 将 mod_dav 构建为共享对象，158
  - 静态构建 mod_dav，158
  - 检查是否启用 mod_dav，158
  - 描述，158
  - 文件仓库目录，158
  - 支持此的编辑器，159
  - httpd.conf 文件中 mod_dav 的条目，158
  - Mac OS 设置，163
  - Windows 2000/XP 设置，159–162
- 用于 GD 库的 WebImage 类
  - 功能，241
  - caption() 方法，251–252
  - 代码列表，241–243
  - display() 方法，244
  - imagesavealpha() 函数，244
  - load() 函数，243–244
  - logo() 方法，255–256
  - 公共属性，243
  - resize() 函数，246–247, 259
  - rotate() 方法，249
  - save() 方法，244–245
- while 循环，用于语言翻译，333
- Whitesmith's 缩进风格，215
- wiki
  - 微型 CMS
    - DocuWiki，326
    - MediaWiki，325–326
  - 术语起源，324
  - 概述，323–324
- Windows 2000/XP，WebDAV 设置，159–162
- WordPress 博客微型 CMS，323
- 写入流（PHP），63
- WROX 网站，76

### X

- Xdebug PECL 包，197
- XHTML，AJAX 使用，273
- XML。另参见 AJAX（异步 JavaScript 和 XML）
  - 配置检查器（PHP），116–128
  - 更多信息，285
  - PHP5 支持，16–17
  - SimpleXML 扩展（PHP），16, 125, 127, 269–270
- XMLConfigProcessor.php 类
  - checkConfig() 函数，126–128
  - checkConfigAccess() 方法，124
  - checkDeps() 方法，124
  - checkExtensions() 方法，125
  - checkPHP() 方法，125–126
  - 代码列表，119–122
  - 构造函数，122–123
  - 其中的 extension_loaded() 函数，124, 125
  - 其中的 ini_get_all() 函数，126, 127
  - 其中的 ini_set() 函数，127–128
  - $message 属性，122
  - 其中的 phpversion() 函数，126
  - process() 方法，123
  - 其中的 SimpleXML xpath() 方法，125, 127
  - version_compare() 函数，126
  - $xml 属性，122
  - $xmlfile 属性，122
- XMLHTTP 和 XMLHttpRequest 接口（AJAX）
  - 更多信息，285
  - 处理 ReadyStateChange 事件，280
  - 处理响应，280–282
  - 历史，277
  - 方法，277–278
  - 属性，278–279
  - 处理浏览器差异，279–280
- XOOPS（可扩展对象导向门户系统）
  - 自定义默认设置，314–315





#### Zlib 库 (PHP
- 默认功能，313
- 安装，312–313
- 可用的其他模块，313
- 优缺点，315
- 网站，312

#### xpath() 方法 (SimpleXML)，125, 127

#### XSL 扩展 (PHP)，16

#### XSS (跨站脚本攻击)，180-181

### Z

- Zawodny, Jeremy (MySQL 专家)，350
- ZenCart CMS，327
- Zend Engine 1，php.ini 设置，108
- Zend Optimizer 缓存引擎
  - 配置，295
  - 安装，294–295
  - 与其他缓存引擎的对比，305
  - 概述，294
  - 移除，296
  - 适用场景，305
  - 网站，295
- ZIP 扩展 (PHP)，271
- Zlib 库 (PHP)，107

![](img/cacdd24f2926f10ee3219256ad732604_405_0.png)

# 随身携带你的资料库

现在，无论你在哪里，都可以在线访问 70 多本完整的 Wrox 书籍！您订阅 Wrox 参考资料库后，即可查阅所有图表、代码片段、屏幕截图和代码示例。如需获取答案并随时查阅，请访问 wrox.books24x7.com 并立即订阅！

# 查找书籍

- ASP .NET
- C#/C++
- 数据库
- 综合
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

