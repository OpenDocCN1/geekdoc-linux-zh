
# LAMP 高级指南

## 作者简介

**Jason Gerner** 目前在辛辛那提交日工作，从事网页开发，并利用业余时间抱怨缺乏对 web 标准的支持以及滥用 XML。他经常出没于 PHPBuilder.com 的讨论区，并在那里担任版主。

**Elizabeth Naramore** 在迈阿密大学（俄亥俄州）获得组织行为学学士学位，自 1997 年以来一直在开发网站。她的主要工作涉及 PHP/MySQL、电子商务以及自由写作和教学。她的文章可在 PHPBuilder.com 和 *国际 PHP 杂志* 上阅读。她是 OINK-PUG（俄亥俄州、印第安纳州、北肯塔基州 PHP 用户组）的自豪成员，与丈夫和两个年幼的孩子住在俄亥俄州辛辛那提。

**Morgan L. Owens** 从奥克兰大学毕业，获得了一个没人感兴趣的数学学位后，在 IT 行业辗转，成为基于 Intranet 和 Internet 环境的基于 Web 应用的后台 Web 开发人员和程序员。他仍住在奥克兰，但建议为了合适的职业，他或许——或许——会考虑搬家。

**Matt Warden** 开发基于 Web 的应用程序已超过六年。他的工作主要侧重于设计和实施 LAMP 应用程序，供其他企业内部使用以提高生产力。最近，Matt 一直使用 AJAX 提供一种基于 Web 的替代方案，以获得通常只有通过原生桌面解决方案才能获得的生产力提升。目前，Matt 是位于俄亥俄州辛辛那提的 Signal US Communications 的首席开发人员。

## 制作团队

**执行编辑**

Carol Long

**高级获取编辑**

Debra Williams Cauley

**开发编辑**

Brian MacDonald

**贡献者**

- William Barnett
- Wm. Christopher Mastin

**技术编辑**

- Jason Gerner
- Elizabeth Naramore

**制作编辑**

Kenyon Brown

**校对编辑**

Kathryn Duggan

**编辑经理**

Mary Beth Wakefield

**制作经理**

Tim Tate

**副总裁兼执行集团出版人**

Richard Swadley

**副总裁兼执行出版人**

Joseph B. Wikert

**项目协调员**

Kristie Rees

**图形与制作专员**

- Carrie Foster
- Lauren Goddard
- Denny Hager
- Barbara Moore
- Alicia B. South

**质量控制技术员**

- Amanda Briggs
- John Greenough
- Jessica Kramer
- Joe Niesen

**媒体开发专员**

- Angie Denny
- Kate Jenkins
- Steve Kudirka
- Kit Malone
- Travis Silvers

**媒体开发协调员**

Laura Atkinson

**校对和索引**

TECHBOOKS Production Services

## 致谢

感谢我可爱的妻子在过去几年里的包容和支持。我还要感谢我的合著者们出色的工作以及他们在这个项目上花费的时间。此外，感谢 Wiley 的同事们给我们机会，以及 Brian 巨大的帮助和对我们的信任。 — *Jason Gerner*

我想感谢我的父母，尽管我是一个且永远会是一个极客，但他们总让我感觉很酷。我还要感谢我的丈夫和孩子们，在我压力大时照顾我，并充当我的快乐源泉。也要感谢 Jason 和 Brian 帮助我们的书顺利完稿。 — *Elizabeth Naramore*

我想感谢 Scott 以及 HIT Studios 的其他团队成员，尤其是把我引入了这个“PHP”领域；感谢我的共同作者们，即使看到我的写作后还邀请我参与这个项目；感谢科罗拉多大学的 Karl Gustafson，他多年前给过我一条建议，尽管他肯定不知道我在说什么；以及我的亲友，他们真的就是我的生命支持系统——特别是我的祖母 Doris Madeline Rachael Shipton (1918–2005)。 — *Morgan L. Owens*

特别感谢 Sam Foster，在我们最初尝试确定 XMLHTTP 和 XMLHttpRequest 对象使用的最佳实践时，他通过电子邮件与我合作，当时关于该主题的资料非常少。他的想法启发了 RemoteConnection 对象设计的许多方面。 — *Matt Warden*

## 引言

围绕 LAMP 的所有喧闹究竟是为了什么？这个“LAMP”是什么，我又该如何获取它？这些问题将在本书的篇章中得到解答。在这种情况下，LAMP 代表 Linux、Apache、MySQL 和 PHP，并已被证明是开发企业级 Web 应用程序增长最快的方式之一。所有这些包都是开源的，因此你基本上可以自由地按照自己的意愿使用它们；唯一的限制是你自己的想象力。此外，使用开源技术，你不仅可以得到行业内最优秀的人才共同努力提供出色的软件包，如果遇到困难，你还能得到庞大的开源社区的大力支持。读完本书后，你将拥有更广泛的 LAMP 知识，并可以在开发动态网站时将其付诸实践。由于这目前是唯一可用的高级 LAMP 书籍，并且是 Apress 专业系列的一部分，你可以确信书中的信息将帮助你成为更好的程序员，并领先于其他人一步。

需要注意的是，虽然“LAMP”一词在更广泛的定义中也可以包括 Perl 和 Python，但我们在本书中选择了专注于 PHP。

本书的目标是引导初中级 Web 开发者更进一步，为他们配备关于这些模块中每一个的更高级别的知识。我们在这本书中提供工具，让你能够“跳出框框”思考，并为老问题找到新的解决方案。

### 本书适合谁？

本书适合有一定经验的 Web 开发者，他们希望将他们的网站提升到下一个层次。如果你有兴趣使用开源工具来运行一个动态、令人兴奋的 Web 站点，你会在这里找到你需要的东西。我们假设阅读本书的人在以下领域具有一些基本经验：

- Web 服务器技术
- 面向对象（OO）编码
- 数据库结构、设置和交互（检索、修改和添加数据）
- 设置用户和权限
- 安装新软件
- 使用命令行

虽然拥有一个熟悉的当前 LAMP 环境会有帮助，但这并不是必须的。只要你对安装新软件熟悉，你就可以轻松地将 Apache、MySQL 和 PHP 一起安装。还有一些软件包可以一次性完成这三个模块的安装，例如 XAMPP（可在 <http://www.apachefriends.org/en/xampp.html> 获取）。

读完本书后，你将能够自信地克服任何 LAMP 障碍，为未来可能希望编写的应用程序获得一些很棒的新想法，或者以新的效率和力量重构你的一些旧代码。

## 本书涵盖的内容

本书涵盖了多种主题：

- PHP 5.0 新特性指南
- PHP 中面向对象编程（OOP）的深入讨论
- 代码效率、基准测试及结果优化
- 配置 PHP 以实现最佳性能
- 高级 MySQL 查询
- Apache 技巧与窍门
- 本地和远程站点安全
- 使用高级 PHP 扩展
- 常见的 PEAR 包
- Ajax 与 PHP
- 晦涩难懂的 PHP 命令
- CMS（内容管理系统）的比较与解析
- 博客包
- 从其他编程语言过渡的指南
- 缓存引擎

## 使用本书所需条件

本书设计用于 Linux 机器，但书中的大部分信息同样适用于 Windows 用户。你需要 PHP、MySQL 和 Apache 来完成本书中的练习。这三个都是开源程序，因此你可以免费下载和使用。你还需要一个文本编辑器来输入代码。最后，你需要一个网页浏览器，如 Internet Explorer、Netscape Navigator、Firefox、Safari 或 Opera，来查看你的网页。

正如任何程序员都知道的，软件一直在不断被改进和调试。虽然我们在出版时使用了最新和最棒的模块版本，但这些版本可能很快就会过时。重要的是，你应访问 PHP、Apache 和 MySQL 的源网站，以获取最新版本和近期发布说明。在开发使用应用程序的网站时，我们建议你始终使用最近的稳定版本。使用尚未经过充分测试的软件版本可能会对你的应用程序造成危险，并导致你的代码中出现 bug。这对新手也是如此——你应该在应用程序的稳定版本上学习，而不是在 beta 版本上。

编写本书时有效的最新稳定版本如下：

- **PHP：** 版本 5.0.4（可于 http://www.php.net 获取）
- **Apache：** 版本 2.0.54（可于 http://www.apache.org 获取）
- **MySQL：** 版本 4.1.12（可于 http://www.mysql.com 获取）

本书的后续版本将在这些程序有变更和改进时进行更新。

## 约定

为了帮助你最大程度地从文本中获益并跟上发生的事情，我们在全书中使用了一些约定。



> 像这样的方框包含重要且不可遗忘的信息，这些信息与周围文本直接相关。

针对当前讨论的技巧、提示、窍门和题外话会缩进并置于斜体中，如下所示。

关于文本中的样式：

- 当我们引入重要词汇时会将其加粗显示。
- 我们展示 URL 的方式如下：http://www.mysite.com
- 我们在文本中展示代码的方式如下：`persistence.properties`
- 我们以两种不同的方式呈现代码：

```
In code examples we highlight new and important code with a gray background.
```

灰色高亮不用于在当前背景下重要性较低的代码，或之前已展示过的代码。

## 源代码

当你浏览本书中的示例时，你可以选择手动输入所有代码，或使用随书附带的源代码文件。本书中使用的所有源代码均可在 http://www.wrox.com 下载。到达网站后，只需使用搜索框或其中一个标题列表找到书名，然后点击书籍详情页面中的“下载代码”链接，即可获取本书的所有源代码。

由于许多书名相似，通过 ISBN 搜索可能最为便捷。本书的 ISBN 是 0-7645-9723-X。

下载代码后，只需使用你喜欢的解压缩工具进行解压。或者，你可以访问位于 http://www.wrox.com/dynamic/books/download.aspx 的 Wrox 代码下载主页面，查看本书及所有其他 Wrox 书籍可用的代码。

## 勘误表

我们竭力确保文本或代码中没有错误。然而，人无完人，错误难免发生。如果你发现我们书中有任何错误，如拼写错误或有缺陷的代码，我们将非常感激你的反馈。提交勘误信息不仅可能为另一位读者节省数小时的烦恼，同时也帮助我们提供质量更高的信息。

要找到本书的勘误页面，请访问 `http://www.wrox.com`，并使用搜索框或其中一个标题列表找到书名。然后，在书籍详情页面，点击“书籍勘误”链接。在此页面上，你可以查看已提交并由 Wrox 编辑发布的本书所有勘误信息。包含每本书勘误链接的完整书籍列表也可在 `www.wrox.com/misc-pages/booklist.shtml` 找到。

如果你未在书籍勘误页面找到“你的”错误，请访问 `www.wrox.com/contact/techsupport.shtml` 并完成该处的表格，将你发现的错误发送给我们。我们将检查信息，并在适当时将消息发布到书籍的勘误页面，并在今后的版本中修正该问题。

## p2p.wrox.com

为了与作者和同行进行讨论，请加入 `p2p.wrox.com` 的 P2P 论坛。论坛是一个基于网页的系统，供你发布与 Wrox 书籍及相关技术相关的消息，并与其他读者和技术用户互动。论坛提供订阅功能，当你选择感兴趣的主题有新帖子发布时，会通过电子邮件通知你。Wrox 作者、编辑、其他行业专家以及你的同行读者都活跃在这些论坛上。

在 `http://p2p.wrox.com`，你会发现许多不同的论坛，不仅有助于你阅读本书，也有助于你开发自己的应用程序。要加入论坛，只需遵循以下步骤：

1. 前往 `p2p.wrox.com` 并点击“注册”链接。
2. 阅读使用条款并点击“同意”。
3. 填写必填信息以及你希望提供的任何可选信息，然后点击“提交”。
4. 你将收到一封电子邮件，其中包含验证你的账户并完成加入流程的信息。

你可以不加入 P2P 而在论坛中阅读消息，但要发布自己的消息，你必须加入。

加入后，你可以发布新消息并回复其他用户发布的消息。你可以随时在网页上阅读消息。如果你希望收到特定论坛新消息的电子邮件通知，请点击论坛列表中论坛名称旁边的“订阅此论坛”图标。

有关如何使用 Wrox P2P 的更多信息，请务必阅读 P2P 常见问题解答（FAQs），以了解关于论坛软件工作原理的答案，以及许多与 P2P 和 Wrox 书籍相关的常见问题。要阅读 FAQs，请点击任何 P2P 页面上的“FAQ”链接。

## 专业 LAMP

# 第 1 章

## PHP5 有什么新特性？

PHP5 到底有什么大不了的？如果你对 PHP4 有经验，你可能知道面向对象编程以及 PHP4 是如何处理这一点的。如果你不熟悉 PHP，但熟悉其他编程语言，你可能会发现 PHP5 对面向对象原则的实现很熟悉。幸运的是，随着 PHP5 的发布，事情变得更加容易了。然而，除了“更好的面向对象编程”处理外，还有其他改进和变化，例如 `php.ini` 中更多的配置选项以及大量新的数组相关和其他函数。本章将为你概述这些变化。

## 面向对象的变化

以下变化涉及 OOP 模型及相关功能和主题。这些变化中的大部分在第 2 章中有更详细的介绍，但这里也简要概述供你快速参考。

### 传递对象

PHP5 中 OOP 变化的一大影响是变量作为参数传递给函数的方式。在 PHP4 中，默认情况下，变量是按值传递而不是按引用传递，除非使用 `&$varname` 语法另行注明。在 PHP5 中，默认是按引用分配值。

### 异常

简而言之，异常是出错时发生的过程。现在，当程序遇到意外错误时，它不会完全停止，你可以对程序在该错误发生时应该做什么行使更多的控制权。你很可能熟悉 PHP4 中可用的 `set_error_handler()` 函数。如果你不熟悉，这个函数的目的是定义一个用于错误处理的用户函数。然而，其实现有许多局限性。例如，如果错误类型是 `E_ERROR`、`E_PARSE`、

`E_CORE_ERROR`、`E_CORE_WARNING`、`E_COMPILE_ERROR`、`E_COMPILE_WARNING` 以及大部分 `E_STRICT` 错误。此外，如果错误发生在 `set_error_handler()` 函数脚本之前，该函数将永远不会被调用。PHP5 带来了处理异常的新框架。

#### 尝试/捕获/抛出

如果你有过 C++ 或 Java 等语言的编程经验，你肯定听说过“try（尝试）”、“catch（捕获）”和“throw（抛出）”这些术语。当发生错误时，会“抛出”一个异常。可能会引起错误的代码被放入 try/catch 块中，在 try 部分尝试运行，如果抛出异常，则被“捕获”（在 catch 部分），并应执行用户定义的操作。try/catch/throw 块的语法如下：

```php
<?php
try
{
    $error_message = 'Hello, I am an error.';
    throw new Exception($error_message);
} catch (Exception $e)
{
    echo 'Exception caught: ', $e->getMessage(), "\n";
}
?>
```

#### 内置异常类

你刚才看到的 `Exception` 类也是 PHP5 的一项改进，并且是默认内置的。有了 PHP5，你现在可以获取已抛出异常的信息，并使用这些数据做出适当的响应。处理并存储该数据的内置异常类如下所示：

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

仔细查看 `Exception` 类：

| 成员或方法名称 | 代表内容 |
| :--- | :--- |
| `$message` | 异常消息；默认值可以设置为任何你喜欢的内容 |
| `$code` | 用户定义的代码 |
| `$file` | 发生错误的文件名 |
| `$line` | 发生错误的行号 |
| `getMessage()` | 返回 `$message` |
| `getCode()` | 返回 `$code` |
| `getFile()` | 返回 `$file` |
| `getLine()` | 返回 `$line` |
| `getTrace()` | 返回一个数组，其中包含来自 `debug_backtrace()` 函数的信息 |
| `getTraceAsString()` | 返回与 `getTrace()` 函数相同的结果，但以格式化字符串形式返回 |
| `toString()` | PHP5 魔术方法，允许在与 `print` 或 `echo` 配合使用时将对象格式化为字符串 |

在上面的 try/catch/throw 示例中，我们使用了内置异常类中的 `getMessage()` 函数来返回并显示错误消息内容。

### 扩展内置异常类



显然，内置异常类是该类的最通用形式，虽然它在许多情况下非常有用，但有时你可能希望以更具体处理异常。例如，在发送邮件时，如果收件人的电子邮件地址为空，你并不会收到 PHP 错误。除非你监控你的 `sendmail` 日志，否则你可能不会知道你的邮件未被发送。这将是非常有用的信息，因此你可以使用 `extends` 关键字轻松地扩展内置类，如下所示：

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
        sendEmail("", "Exception Testing",
                  "We are testing the exception handling in PHP5");
    } catch (emailException $e)
    {
        echo "in file <strong>" . $e->getFile() . "</strong>";
        echo " on line <strong>" . $e->getLine() . "</strong>";
    }
}
?>
```

这将产生以下结果：

```
There was an error sending your email:
Recipient email address is NULL in file /usersites/email_exception.php on line 11
```

你可以访问存储在内置异常类中的文件名和行信息，但你还可以添加更详细的错误消息以便进行调试。

### `set_exception_handler()` 函数

默认情况下，任何未被捕获的异常都会导致致命错误并停止脚本执行。PHP5 提供了通过 `set_exception_handler()` 函数清理任何未捕获异常的机会。类名、错误消息和回溯会被传递给 `set_exception_handler()` 函数，但你也可以访问内置异常类的信息。该函数的使用方式如下：

```php
<?php

function lastResort($e)
{
    echo "Previously uncaught exception being caught from " . get_class($e);
    echo " in file: " . $e->getFile() . " on line " . $e->getLine();
}

set_exception_handler("lastResort");

throw new Exception();
```

你的结果将类似于以下内容：

```
Previously uncaught exception being caught from Exception in file:
/usersites/set_exception_handler.php on line 9
```

## PHP5 有什么新功能？

请注意，你必须在 `set_exception_handler()` 函数内用引号将函数名括起来；否则你将收到一个通知，提示你正在尝试使用未定义的常量。

## 接口

接口已被添加到 PHP5，允许你将类绑定到多个位置。它们由空函数（将在实现类中定义）和你希望应用于实现类的任何常量组成。接口的所有实现类都必须提供接口中定义的每个方法的实现，从而确保你代码的未来使用者知道预期有哪些方法。

接口在第 2 章中进行了更详细的讨论。

### 迭代器

通过标准公共库（SPL），你可以访问一整套新的类和接口，允许你操作和利用迭代器。SPL 是一个编译并默认可在 PHP 中使用的扩展，它基本上是一个供你使用的接口和类库。下一节讨论 `Iterator` 类本身。你会注意到许多函数与数组函数相似。

#### 主要迭代器接口

`Iterator` 类是一个内置接口，允许你遍历任何可以用 `foreach()` 语句遍历的东西——例如，文件目录、查询结果或数据数组。它具有某些固有函数：

- `Iterator::current()`: 返回当前元素。
- `Iterator::key()`: 返回当前元素的键。
- `Iterator::next()`: 将指针移动到下一个元素。
- `Iterator::valid()`: 验证在调用 `next()` 或 `rewind()` 后是否存在元素。

通过预定义通用的 `Iterator` 功能，这些都有助于你使用迭代使代码更强大、更高效。`Iterator` 接口最重要的一点是它是其他 SPL 类的构建块之一。

#### 其他迭代器类

以下部分简要描述了一些继承自 `Iterator` 类的主要类。有关以下任何类的更详细信息以及更全面的列表，可以在在线 SPL 文档中找到：`http://www.php.net/~helly/php/ext/spl/main.html`。

#### `DirectoryIterator`

顾名思义，`DirectoryIterator` 是一个实现了 `Iterator` 的 `Iterator` 类，允许你处理文件目录。此类中包含一组强大的函数，可以获取每个文件的信息，例如修改时间和日期、文件大小、文件类型、文件所有者、文件的完整路径以及与文件关联的权限（仅举几例）。

#### `RecursiveIterator`

`RecursiveIterator` 类有助于实现递归迭代，即自动重复调用函数直至满足特定条件。该类的函数可帮助你判断是否存在子迭代器，以及这些子迭代器可能是什么。

#### `ArrayIterator`

使用 `ArrayIterator` 内置类，你可以在迭代对象的同时修改 `array` 的值和键。它允许你在每次迭代时操作数组。诸如 `append()`、`copy()` 和 `seek()` 等函数使开发者能够以超出常规数组函数集的方式处理数组。

迭代器正在不断得到改进和增强，你可以预期在 PHP 5.1 中看到一些重大变化。

### 构造方法与析构方法

在 PHP4 中，你可以通过将方法命名为与类名相同的方式，在类中立即调用该方法。在 PHP5 中，为此目的引入了一个新的“魔术方法”名称，即 `__construct()`。在类中包含此方法后，当对象创建时会自动调用它。

同样，如果在类中包含魔术方法 `__destruct()`，对象将被销毁。此方法在被调用时销毁对象。如果没有更多对对象的引用，或者到达 PHP 脚本的末尾时，`__destruct()` 方法也会被调用。

第 2 章将更深入地讨论构造方法和析构方法。

### 访问修饰符

现在，你可以使用 PHP5 新增的三个关键字来控制类成员和方法的可见性级别：`public`、`private` 和 `protected`。方法和成员被标记为 `public`、`private` 或 `protected`。

以下是关于 `private`、`protected` 和 `public` 关键字的简要总结（你可以在第 2 章阅读有关这些特性的更多内容）：

- `Public`（公开）：这些成员和方法对整个脚本可用。它们可以在对象内部或对象外部引用。
- `Protected`（受保护）：标识为受保护的成员或方法仅在对象内部或继承类中可用。
- `Private`（私有）：私有方法和成员仅在对象本身内部可用，对任何继承类都不可用。

### `final` 关键字

`final` 关键字可与类或类内的方法一起使用。当与类一起使用时，此关键字阻止任何其他类继承该类。当与方法一起使用时，它阻止任何继承类重写该方法，从而有效确保其永久性，并保护它们不受其他程序员甚至你自己的影响。

### `static` 关键字

将成员或方法声明为 *static*（静态）会将其绑定到它所属的类，而不是类的任何单个对象或实例。静态成员和方法可在整个脚本中访问。



关于使用 `static` 关键字有一些重要的注意事项。首先，不要使用 `$this->varName` 语法从类内部访问变量，而应使用 `self::$varName`。在之前的示例中，你从一个不同的函数中访问了 `self::$count` 成员，但由于静态成员对类内部的一切都可用，因此仍然使用了 `self::` 语法。其次，当从类外部访问静态成员时，应使用语法 `className::$varName`。同样，当在类内部任何地方访问静态方法时，应使用 `self::methodName()`；当从类外部访问时，应使用 `className::methodName()`。

关于使用 `static` 关键字的更详细讨论将在第 2 章中进行。

### abstract 关键字

当你有一个高级类，知道它将被更具体、更低的类继承时，使用 abstract 关键字。例如，你可以如下使用抽象类和方法：

```php
<?php
    abstract class getToday {
        public $today = getdate();
        abstract function showCalendar();
    }
    class monthlyCalendar extends getToday {
        function showCalendar() {
            //显示本月的日历
        }
    }
    class dailyCalendar extends getToday {
        function showCalendar() {
            //显示今天的每日日历
        }
    }
    class yearlyCalendar extends getToday {
        function showCalendar() {
            //显示今年的日历
        }
    }
?>
```

这个抽象类基本上说“创建一个日历，但然后在子类中指定其类型”。如你所见，第一个类中的 `showCalendar()` 函数被故意留空并设为抽象，因为该类应该被扩展，并根据调用的继承类显示适当的日历。`getToday()` 类是不完整的，是抽象化的完美候选者。抽象方法（如同接口中的方法）实际上是空的，需要在子类中进一步实现。

使用抽象类时的一些规则包括：

- 如果你有抽象方法，整个类也必须定义为抽象。
- 你不能实例化抽象类。
- 你可以将一个类定义为抽象类，即使它不包含任何抽象方法。
- 实现抽象方法的继承类必须具有与其父类相同（或更弱）的可见性。

在第 2 章中，我们将更详细地讨论抽象。

### 内置方法重载函数

与 PHP4 不同，在 PHP4 中你必须使用 `overload()` 函数来强制进行重载检查，而 PHP5 原生允许你对任何不符合预期的方法或成员引用进行重载，从而有效地让你控制接下来发生的事情。新的魔术方法 `__get()`、`__set()` 和 `__call()` 用于重载，如下所示：

```php
<?php

class overload {

  function __get($property) {
    //检查属性是否存在于类中
    //如果不存在，执行我们想要执行的操作
    //例如显示错误。否则返回
    //一个值。
  }

  function __set($property, $value) {
    //检查属性是否存在于类中
    //如果存在，将其设置为传入的值
    //否则执行我们想要执行的操作，例如
    //显示错误。
  }

  function __call($method, $array_of_arguments) {
    //检查方法是否存在于类中
    //如果不存在，执行某些操作，例如将其委托给
    //包含该方法的另一个类或
    //打印错误语句。
  }
}
?>
```

第 2 章将更详细地讨论重载。

### 新函数

以下是 PHP5 中所有新函数的综合列表，不包括那些需要扩展的函数：

- `array_combine()`: 将两个数组合并为一个，使用其中一个数组作为值，另一个数组作为键。
- `array_diff_uassoc()`: 通过命名字典确定两个或多个数组之间的差异，并进行额外的键比较。
- `array_udiff()`: 通过使用命名字典进行数据比较，确定两个或多个数组之间的差异。
- `array_udiff_assoc()`: 通过使用命名字典进行数据比较，并进行额外的键比较，确定两个或多个数组之间的差异。
- `array_udiff_uassoc()`: 通过使用命名字典进行额外的键比较，以及通过命名字典进行数据比较，确定两个或多个数组之间的差异。
- `array_intersect()`: 通过使用命名字典进行数据比较，确定两个或多个数组之间的交集。
- `array_intersect_assoc()`: 通过使用命名字典进行数据比较，并进行额外的键比较，确定两个或多个数组之间的交集。
- `array_intersect_uassoc()`: 通过使用命名字典进行额外的键比较，以及通过命名字典进行数据比较，确定两个或多个数组之间的交集。
- `array_walk_recursive()`: 对数组的每个元素递归地应用命名字典。
- `convert_uudecode()`: 解码 uuencoded 字符串。
- `convert_uuencode()`: 对字符串进行 uuencode 编码。
- `curl_copy_handle()`: 复制 cURL 句柄及其所有偏好设置。
- `date_sunrise()`: 基于给定的纬度、经度、天顶角和 GMT 偏移量返回日出时间。
- `date_sunset()`: 基于给定的纬度、经度、天顶角和 GMT 偏移量返回日落时间。
- `dba_key_split()`: 将字符串表示中的索引拆分为数组表示。
- `dbase_get_header_info()`: 返回 dBase 数据库的列结构信息。

# 第 1 章

- `dbx_fetch_row()`: 从查询结果中获取行，但如果查询中未设置 DBX_RESULT_UNBUFFERED，则执行将失败。
- `fbsql_set_password()`: 更改指定用户的密码。
- `file_put_contents()`: 等效于打开文件、写入文件并关闭文件的操作。
- `ftp_alloc()`: 向 FTP 服务器发送 ALLO 命令，该命令为上传文件预留空间。
- `get_declared_interfaces()`: 返回脚本中已声明的任何接口。
- `get_headers()`: 返回服务器响应 HTTP 请求时发送的头部信息。
- `headers_list()`: 返回已发送（或准备发送）的响应头列表。
- `http_build_query()`: 根据给定的数组返回 URL 编码的查询字符串。
- `ibase_affected_rows()`: 返回受上一个查询影响的行数（Interbase）。
- `ibase_backup()`: 在服务管理器中启动备份任务并立即返回（Interbase）。
- `ibase_commit_ret()`: 提交事务，但不关闭它然后返回（Interbase）。
- `ibase_db_info()`: 返回关于数据库的信息（Interbase）。
- `ibase_drop_db()`: 删除数据库（Interbase）。
- `ibase_errcode()`: 返回错误代码（Interbase）。
- `ibase_free_event_handler()`: 释放已注册的事件处理程序（Interbase）。
- `ibase_gen_id()`: 增量增加并返回增加后的值（Interbase）。
- `ibase_maintain_db()`: 在数据库服务器上执行维护命令（Interbase）。
- `ibase_name_result()`: 为结果集命名（Interbase）。
- `ibase_num_params()`: 返回命名查询中的参数数量（Interbase）。
- `ibase_param_info()`: 返回命名查询的参数信息（Interbase）。
- `ibase_restore()`: 在服务管理器中启动恢复任务并立即返回（Interbase）。
- `ibase_rollback_ret()`: 回滚事务但不关闭它（Interbase）。
- `ibase_server_info()`: 返回关于数据库的信息（Interbase）。
- `ibase_service_attach()`: 连接到服务管理器（Interbase）。
- `ibase_service_detach()`: 断开与服务管理器的连接（Interbase）。



- `ibase_set_event_handler()`：注册用户定义的函数，以便在特定事件发生后调用（Interbase）。
- `ibase_wait_event()`：等待数据库发布的事件（Interbase）。
- `iconv_mime_decode()`：解码 MIME 头字段。
- `iconv_mime_decode_headers()`：同时解码多个 MIME 头字段。
- `iconv_mime_encode()`：创建 MIME 头字段。
- `iconv_strlen()`：返回字符串的字符数。
- `iconv_strpos()`：在字符串中查找指定字符第一次出现的位置。
- `iconv_strrpos()`：在字符串的指定范围内查找指定字符最后一次出现的位置。
- `iconv_substr()`：返回字符串的一部分。
- `idate()`：将本地时间/日期格式化为整数。
- `imagefilter()`：对图像应用命名过滤器。
- `image_type_to_extension()`：返回图像文件的扩展名。
- `imap_getacl()`：返回指定邮箱的 ACL。
- `ldap_sasl_bind()`：使用 SASL 将资源绑定到 LDAP 目录。
- `mb_list_encodings()`：返回所有支持编码的数组。
- `pcntl_getpriority()`：返回 `pid` 的优先级。
- `pcntl_wait()`：暂停当前进程，直到子进程退出并返回子进程的 id。
- `pg_version()`：以数组形式返回客户端、协议和服务器的版本。
- `php_strip_whitespace()`：从源代码中移除注释、空白符和换行符，并返回结果。
- `proc_nice()`：通过给定的增量改变当前进程的优先级。
- `psapi_config_data_dir()`：设置语言数据文件的位置。
- `psapi_config_dict_dir()`：设置主单词列表的位置。
- `setrawcookie()`：等效于未经过 URL 编码值的 `setcookie()`。
- `snmp_read_mib()`：读取并解析 MIB 文件到活动的 MIB 树中。
- `sqlite_fetch_column_types()`：从给定表中返回适用的列类型。
- `str_split()`：将字符串拆分为字符数组。
- `stream_copy_to_stream()`：在流之间复制数据并返回复制的数据量。
- `stream_get_line()`：与 `fgets()` 类似，但允许指定命名分隔符。
- `stream_socket_accept()`：接受来自之前使用 `stream_socket_server()` 函数创建的套接字的连接。
- `stream_socket_client()`：打开到 Internet 或 Unix 域目的地的流。
- `stream_socket_get_name()`：返回套接字连接的名称。
- `stream_socket_recvfrom()`：从套接字接收数据，直到指定长度。
- `stream_socket_sendto()`：向指定套接字发送数据，无论其是否已连接。
- `stream_socket_server()`：在指定服务器上创建流。
- `strpbrk()`：在字符串中搜索给定字符列表中的任意字符，并从第一次成功匹配处返回字符串的剩余部分。
- `substr_compare()`：使用命名偏移量和可选的大小写敏感性比较两个字符串。
- `time_nanosleep()`：延迟脚本执行指定秒数和纳秒数。

有关这些函数的更多信息，可在源地址中找到，http://www.php.net。

# PHP5 的其他更改

除了面向对象编程（OOP）更改的清单和大量可用的新函数外，PHP5 的发布中还做出了其他改进。

## 配置更改

在 PHP5 中，`php.ini` 配置文件有许多更改。这些将在第 5 章中详细讨论，但这里列出一个列表供您参考：

- `mail.force_extra_parameters`
- `register_long_arrays`
- `session.hash_function`
- `session.hash_bits_per_character`
- `zend.zel_compatibility_mode`

通过这些新的指令，你可以对 PHP 环境施加更多控制，从而赋予你在编码方面更多的自由度。

## MySQLi

众所周知，MySQLi 与 PHP 搭配良好，能够构建数据库驱动的动态网站。因此，MySQLi（MySQL 改进版）扩展的发布使每个人的工作都变得更加容易。

### 配置设置

`php.ini` 中有几个新的 MySQLi 配置设置可用。以下是简要说明：

- `mysqli.max_links`：设置每个进程的最大 MySQL 连接数。
- `mysqli.default_port`：设置连接到 MySQL 服务器的默认 TCP/IP 端口。
- `mysqli.default_socket`：设置连接到 MySQL 服务器的默认套接字名称。
- `mysqli.default_host`：设置连接到 MySQL 服务器的默认主机名。
- `mysqli.default_user`：设置连接到 MySQL 服务器的默认用户名。
- `mysqli.default_pw`：设置连接到 MySQL 服务器的默认密码。

**内置类和属性**

`mysqli` 扩展带来了一组新的内置类和属性，您可以在 PHP 脚本中访问这些类和属性。如果脚本是面向过程而非面向对象的，这些新方法也可以作为函数使用。要以面向过程的方式调用函数，只需在方法名前使用 `mysqli_` 语法即可。例如，使用 OOP 创建新连接时，您需要输入以下内容：

```php
<?php
    $connect = new mysqli("server", "user", "pass", "dbname");
    //call methods through the mysqli class
    $connect->close();
?>
```

要使用传统的面向过程编程实现相同的功能，您需要输入以下内容：

```php
<?php
    $connect = mysqli_connect("server", "user", "pass", "dbname");
    //call functions using mysqli_ prefix
    mysqli_close($connect);
?>
```

以下部分描述了 PHP5 中固有的函数类型。

#### class mysqli

该类处理基本的 MySQL 连接。该类的构造函数创建一个新的 PHP/MySQL 连接，从而创建一个新的 `mysqli` 对象。您可以使用该类来操作或检索当前连接的信息，或执行基本查询功能。

该类可用的方法包括：

- `autocommit`：切换事务是否自动提交到数据库。
- `change_user`：切换到其他用户。
- `character_set_name`：返回默认字符集。
- `close`：关闭数据库连接。
- `commit`：将事务提交到数据库。
- `connect`：打开到 MySQL 数据库服务器的新连接（也是 `mysqli` 的构造函数）。
- `debug`：使用 Fred Fish 调试库进行调试。
- `dump_debug_info`：使用 Fred Fish 调试库转储调试信息。
- `get_client_info`：检索客户端信息。

## 第 1 章

- `get_host_info`：获取连接信息。
- `get_server_info`：获取 MySQL 服务器信息。
- `get_server_version`：获取当前 MySQL 服务器版本。
- `info`：返回最近执行的查询的信息。
- `init`：在调用 `real_connect` 函数之前初始化一个`对象`。
- `kill`：终止一个 MySQL 线程。
- `more_results`：查找之前调用的`multi_query`的结果。
- `multi_query`：执行一个或多个查询。
- `next_result`：返回之前调用的`multi_query`的下一个结果。
- `options`：更改或设置`real_connect` `对象`的连接选项。
- `ping`：ping 服务器连接，如果没有连接则重新连接。
- `prepare`：准备一条 SQL 查询语句以便执行。
- `query`：执行查询。
- `real_connect`：连接到 MySQL 数据库服务器，并允许设置额外的选项或`参数`。
- `real_escape_string`：返回转义字符串，以便在 SQL 语句中有效使用。
- `rollback`：回滚当前事务。



- `select_db`：将指定的数据库选为活动数据库。

- `set_charset`：设置要使用的字符集。

- `ssl_set`：设置 SSL `参数`，以启用安全连接。

- `stat`：返回系统状态信息。

- `stmt_init`：为使用 `mysqli_stmt_prepare` 初始化语句。

- `store_result`：从上一个查询传输 `结果集`。

- `thread_safe`：返回是否提供线程安全性。

- `use_result`：从上一个查询传输未缓冲的 `结果集`。

该类可用的属性如下：

- `affected_rows`：获取前一个 MySQL 操作影响的行数。

- `client_info`：以字符串形式返回 MySQL 客户端版本。

- `client_version`：以整数形式返回 MySQL 客户端版本。

- `errno`：返回最近一次函数调用的错误代码。

- `error`：返回最近一次函数调用的错误字符串。

- `field_count`：返回最近一次查询的列数。

- `host_info`：返回表示所使用连接类型的字符串。

- `info`：获取最近执行的查询的信息。

- `insert_id`：返回上一个查询中使用的自动生成 id。

- `protocol_version`：返回使用的 MySQL 协议版本。

- `sqlstate`：返回包含最后一个错误的 SQLSTATE 错误代码的字符串。

- `thread_id`：返回当前连接的线程 ID。

- `warning_count`：返回前一个 SQL 语句执行期间产生的警告数量。

### PHP5 中的新特性

### mysqli_stmt

该类处理预编译语句，即被 MySQL 服务器临时存储直到需要使用为止的 SQL 语句。预编译语句的一个示例是 "SELECT * FROM customer WHERE lastname = ?"。然后，当你准备好执行该语句时，你只需要填入 lastname 的值即可。请注意，当你以函数形式在过程式编程中使用这些方法时，你会在方法名称前使用 `mysqli_stmt_` 前缀（`mysqli_stmt_close`）。

该类可用的方法如下：

- `bind_param`：将变量绑定到预编译语句。

- `bind_result`：将变量绑定到预编译语句以存储结果。

- `close`：关闭预编译语句。

- `data_seek`：在语句结果集中定位到任意行。

- `execute`：执行预编译语句。

- `fetch`：将预编译语句的结果获取到绑定变量中。

- `free_result`：释放给定语句句柄的存储结果内存。

- `prepare`：准备一个 SQL 查询。

- `reset`：重置预编译语句。

- `result_metadata`：从预编译语句中获取元数据信息的结果集。

- `send_long_data`：分块发送数据。

- `store_result`：从预编译语句中缓冲完整的结果集。

该类可用的属性如下：

- `affected_rows`：返回上一次语句执行影响的行数。

- `errno`：返回最后一个语句函数的错误代码。

- `error`：返回最后一个语句函数的错误消息。

- `param_count`：返回给定预编译语句的参数数量。

- `sqlstate`：返回包含最后一个语句函数的 SQLSTATE 错误代码的字符串。

### mysqli_result

该类表示从数据库查询中获得的结果集。你使用该类来操纵和显示查询结果。

该类可用的方法如下：

- `close`：关闭结果集（在过程式编程中称为 `mysqli_free_result`）。

- `data_seek`：移动内部结果指针。

- `fetch_field`：从结果集中获取列信息。

- `fetch_fields`：从结果集中获取所有列的信息。

- `fetch_field_direct`：获取指定列的列信息。

- `fetch_array`：将结果行作为关联数组、数字数组或两者兼有地获取。

- `fetch_assoc`：将结果行作为关联数组获取。

- `fetch_object`：将结果行作为对象获取。

- `fetch_row`：将结果行作为枚举数组获取。

- `field_seek`：将结果指针移动到指定的字段偏移量。

该类可用的属性如下：

- `current_field`：返回当前字段指针的偏移量。

- `field_count`：返回结果集中的字段数量。

- `lengths`：返回列长度数组。

- `num_rows`：返回结果集中的行数。

如你所见，新的 `mysqli` 类可以帮助你编写更高效的代码，并为你在 PHP 4 中可用的 MySQL 功能提供额外的灵活性和控制权。

### XML 支持

PHP5 在 PHP4 的 XML 库方面有所改进。有几个新的 XML 扩展是使用 libxml2 编写的，以改进标准化和维护：

- DOM：这组新函数替代了 PHP4 中的 DOM/Xml 函数。它们已重新调整为符合 W3C 发布的 DOM Level 2 标准。

- XSL：前身为 XSLT 扩展，该扩展有助于使用 W3C 的 XSL 样式表作为标准将一个 XML 文件转换为另一个。

- SimpleXML：这组函数允许你简单轻松地从 XML 文件中提取数据。然后你可以使用常见的数组迭代器 `foreach()` 来操纵、显示和比较属性和元素。

- SOAP：SOAP 扩展允许你编写 SOAP 服务器和客户端，并且要求安装 GNOME XML 库（libxml）。第 8 章详细讨论了 XML 扩展。

### Tidy 扩展

PHP5 现在支持 Tidy 库，该库可在 http://tidy.sourceforge.net/ 获取。它协助开发人员清理和完善 HTML 代码。该扩展在 PEAR 库中可用，地址为 http://pear.php.net/package/tidy。要获取可用的 Tidy 函数和类的完整列表，你可以访问位于 http://us2.php.net/tidy 的 PHP 手册。

### SQLite

尽管 SQLite 是在 PHP4 的后续版本中引入的，但它为 PHP5 进行了改进。SQLite 类似于一个迷你 SQL 服务器。许多类和方法已被内置到 PHP5 中，并随 PHP5 的安装捆绑在一起。要了解有关 SQLite 的更多信息，请访问源网站：http://sqlite.org。

#### 总结

虽然 PHP5 中 OOP 模型的重新设计无疑是 PHP4 最大且最好的改进，但还有许多其他方面也得到了改进，以使 PHP 程序员的生活稍微容易一些。

PHP 的其中一个最佳方面是它通过增量改进不断变化和成长，这是任何开源语言所应有的。构成 PHP5 的小改进将帮助你更好地处理 MySQL，帮助你简化代码，并让你更好地访问 XML 的强大功能。不过，最大且最好的改进是 OOP 模型的引入。使用 OOP 而不是过程式编程将彻底改变你思考代码的方式。在下一章中，你将了解如何从 PHP 中的这个新模型中获得最大收益。

## 2 PHP5 面向对象编程

当你开始一个新项目时，你必须考虑的首要事项之一就是代码的结构。无论你编写的是像在线联系表单这样简单的内容，还是功能齐全的全文内容管理系统这样复杂的系统，你如何组织代码都将影响最终产品的性能和可维护性。

当你使用 PHP 这样的语言时，主要有两条路径可供选择：过程式编程和面向对象编程（简称 OOP）。每种策略都有其自身的优势和局限性。

## 过程式编程与面向对象编程

过程式编程通常强调编写尽可能简洁的代码，并直接针对最终结果进行编码。换句话说，大多数过程式编程使用有针对性的函数组来直接解决手头的问题——通常不多也不少。在大多数情况下，这能让你获得极其高效且高性能的应用程序。这种方法的缺点之一是缺乏可维护性。如果项目变得足够大，开发人员可能最终需要维护大量的独立函数，而且在某些情况下，不同函数的逻辑可能会变得令人困惑地相似。

另一方面，面向对象编程（OOP）强调抽象关系和相关功能层次结构。类似的功能可以共享一个公共核心，从而大大简化维护工作。代码重用性也得到提高，因为你轻松地适应抽象的基础功能用于新任务。OOP 还有助于大规模程序设计和帮助封装和分类系统各部分所需的不同功能集合。然而，这种组织和模块化可能有一定代价。如果你的面向对象系统设计不佳，实际上可能比任何替代方案都更难维护。通常，面向对象设计极端的模块化和“代码重量”会导致性能不佳。

一旦你克服了由不良面向对象设计引起的问题，你会发现使用自定义的 PHP 对象集，甚至完整的 API 来创建系统可以带来大多数开发人员都会感激的好处。既然如此，你现在可以开始了解 PHP5 如何实现面向对象编程了。

## 基本类定义



面向对象 PHP 代码的基本单位是类。简而言之，类是一种将相关功能和数据封装在单个实体中的方法。这种封装可用于隐藏内部操作免于外部代码，并简化与数据的外部交互。类是代码分组的形式描述，如果你愿意的话，可以看作是一个程序化食谱。类本身，就像食谱一样，只是一组指令，而不是可以直接使用的东西——你不会直接吃掉食谱本身，对吧？为了使用类，你将创建该类的实例，称为对象——类似于使用食谱制作一道你可以实际食用的菜肴。类定义一组代码的特性和行为，而对象则是该组指令的单独实例。

理解类的一种简单方法是将类代码与物理对象联系起来。很多时候，类会代表这些现实世界的对象。你可能有一个名为`Car`（汽车）的类，它具有一个叫`occupants`（乘客）的属性，该属性可能用于跟踪车中的人数。它甚至可能包含一个名为`brake()`（刹车）的方法，该方法将执行与其同名任务。像许多现实世界物品一样，类拥有描述单个对象的属性组合，在面向对象编程中称为属性，以及它们可以执行的一系列操作，在面向对象世界中称为方法。

### 定义类

在 PHP5 中定义类是一个相对简单的过程——与定义函数非常相似，只是使用的关键字不同：

```php
class Circle
{
    // 类代码在此处
}
```

这段代码使用`class`关键字，后跟类名和一组花括号，定义了一个简单的类。

在标准的 PHP5 类中，类定义主要有两个部分——属性和方法。属性表示对象中持有的数据，而方法则使用这些数据执行操作。

### 属性

在 PHP5 中创建类时，属性是存储对象所代表的各种数据片段的地方。

在 PHP5 中定义属性就像下面这样简单：

```php
visibility $property_name;
```

在此定义中，`visibility`代表属性的代码可见性，它是三个值之一：`public`、`private`或`protected`。这三个关键字的含义将在本章后续部分讨论。

属性定义的第二部分，`property_name`只是你希望属性拥有的名称。

例如，假设你想创建一个名为`Circle`的类。你可能想要一个公共属性来保存半径，如下所示：

```php
class Circle
{
    public $radius;
}
```

可选地，你可以在属性定义中指定初始值。假设你想让`Circle`的初始半径设为10；你可以这样做：

```php
class Circle
{
    public $radius = 10;
}
```

然后，每次创建`Circle`对象时，它都会以初始半径10开始。

### 方法

你已创建属性在对象中保存数据，现在你需要创建一种操作这些数据的方法。为了执行这些操作，你将在类内部创建函数，称为方法。

在 PHP5 中定义方法与在代码其他位置创建标准函数非常相似：

```php
visibility function function_name (parameters)
{
    // 方法实现在此处
}
```

与属性定义类似，方法定义需要一个可见性组件。除了可见性前缀外，方法的定义与标准 PHP 函数完全相同——只需使用`function`关键字，后跟函数名，然后是括号内可选的参数列表。

再次使用`Circle`示例，你将添加一个计算圆面积的方法：

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

你简单地创建了一个名为`calcArea()`的方法，它接受参数`$radius`，并返回给定半径的圆的面积。

既然你创建了这些属性和方法，现在需要一种方式来实际使用你的属性和方法。引入实例化。

### 使用类：实例

为了访问类的属性并使用其方法，你需要先实例化该类，或者创建该类的实例。当类被实例化时，它会返回该类型的一个独立对象，你可以使用它。在 PHP5 中，对象实例使用`new`关键字创建，如下所示：

```php
$c = new Circle();
```

一旦创建对象，通过使用“箭头”运算符（连字符后紧跟大于号）访问单个属性和方法，如下面的代码所示：

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

   // 更改属性
   $c->radius = 5;

   // 使用方法
   echo '圆的面积是 ' . $c->calcArea(5);
?>
```

如果你运行代码，你会看到类似以下内容：

```
圆的面积是 78.539816339745
```

查看代码，你会看到首先定义类`Circle`。然后，你添加了实例化对象的代码：

```php
// 创建 Circle 的新实例
$c = new Circle();
```

最后，你将`$radius`属性更改为值5，并计算半径为5的圆的面积。

```php
// 更改属性
$c->radius = 5;

// 使用方法
echo '圆的面积是 ' . $c->calcArea($c->radius);
```

### PHP5 OOP

仔细观察前面的代码片段，你可能会注意到在使用`radius`属性时有一些不太顺手的之处。你显式地设置了`radius`属性，然后又将该属性作为`calcArea`方法参数的显式值复用。既然对象内部已经知道`radius`属性，那么就没有理由再向`calcArea()`方法显式提供它。为了消除提供`radius`参数的要求并改用对象内部的`radius`属性，你需要一个方法来访问它。PHP 为我们提供了一个名为`$this`的引用来实现这一目标。使用这个特殊命名的变量`$this`就如同引用一个已实例化的对象，但`$this`引用的是包含它的那个对象。

修改`Circle`类，如下所示：

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
echo 'The area of the circle is ' . $c->calcArea();

?>
```

运行这段代码将产生与之前示例完全相同的结果——唯一的改变在于你使用`calcArea()`方式。由于你在方法内部引用了`Circle`对象的`radius`属性，因此不再需要在函数定义和方法调用中包含该参数。

### 可见性

PHP5 OOP 模型的新特性之一，就是能够为所有类属性和方法指定可见性级别。使用这些新的可见性关键字，你可以将类的某些部分对外部代码隐藏，同时暴露你希望对所有代码开放访问的其他功能。PHP5 提供了三种在类中使用的可见性级别：`public`、`private`和`protected`。

`public`可见性意味着属性或方法对所有希望访问它的其他代码都可用。如果未指定方法的可见性，则默认为`public`。

将类成员指定为`private`意味着该属性或方法仅在所属的类定义内部可见。同一类中的所有其他方法都可以访问私有成员，但该特定类外部的任何代码都不能。

最后，`protected`关键字指定属性或方法仅在定义类以及任何扩展或继承自定义类的其他类中可用。章节的后半部分将讨论类的扩展和继承。

> 在 PHP5 下重用 PHP4 类时，重要的是要记住，使用`var`关键字定义的属性（例如`var $propertyName`）将被视为`public`，并且会发出 E_STRICT 警告。

为类成员指定可见性很容易，只需在属性或方法声明前加上相应的前缀即可。在之前定义的`Circle`类中，所有类成员都被定义为`public`。现在你将把一些旧的类成员更改为`private`，并添加一些新方法。



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
```

没有将属性保持为 `public`，而是将它们更改为 `private`，并创建函数来设置它们的值。在像这样简单的情境下，这样做可能有点过度，但如果扩展应用程序，`set` 函数可以在设置内部值之前对数据执行复杂计算。这种分离还可以通过在允许内部数据更改之前验证外部提供的值，从而为私有成员增加一层保护。

你可以使用以下代码来使用你修改后的类：

```php
$c = new Circle();
$c->setCenter(0, 0);
$c->setRadius(10);

echo "The area of the circle is " . $c->calcArea() . "\n";

// 尝试访问私有属性
echo "The private value of radius is " . $c->radius;
?>
```

如果你运行这段代码，你会看到类似以下的输出：

```
The area of the circle is 314.15926535898
Fatal error: Cannot access private property Circle::$radius in /www/plamp/ch02/02-002.php on line 31
```

如你所见，这与你之前使用 `Circle` 的方式并没有太大不同，但由于 `public`/`private` 的指定，你现在必须使用方法来访问 `$center` 和 `$radius` 属性，而不是直接访问这些属性。注意在末尾尝试直接访问私有成员时发生的情况——会引发一个致命错误。

### 构造器和析构器

在处理类的一些情况下，你可能希望有一种方式在对象创建时自动执行操作。你可能想要初始化对象参数或自动调用类方法。也许你希望对象检查本地环境以确认必要的资源可用，或者甚至建立初始连接。对于这些情况，PHP 提供了 `constructors`（构造器）。

构造器不过是一个特殊命名的方法，在对象实例化时自动调用。在 `PHP5` 中，要实现构造器，你只需实现一个名为 `__construct` 的方法即可。例如：

```php
<?php
class Circle
{
    public function __construct()
    {
        // 在对象创建时执行操作
        echo "A circle object is being created.\n";
    }
}

$c = new Circle();
?>
```

执行这段代码时，你会看到以下内容：

```
A circle object is being created.
```

正如预期，定义在构造器方法内部的代码在对象实例化时自动执行了。

> 你仍然可以使用 PHP4 风格的构造器（与类同名方法）在 `PHP5` 中，但新式的 `__construct` 方法更受推荐。

像标准方法和函数一样，构造器也可以处理参数。为了向构造器传递参数，你在创建对象时将其包含在括号内，如下所示：

```php
<?php

class Circle
{
    public $radius;

    public function __construct($r)
    {
        // 在对象创建时执行操作
        echo "A circle object is being created.\n";
        $this->radius = $r;
    }
}

$c = new Circle(10);
?>
```

在这个例子中，你只是在创建对象时简单地提供了一个半径参数——本例中为 10——构造器会自动解析它，进而在实例化时设置圆的半径。

既然你已经有了一种在对象创建时执行操作的方法，接下来我们将看一种在对象销毁时执行额外操作的方式。`PHP5` 现在包含一个在对象销毁时调用的特殊方法，逻辑上称为析构器（`destructor`）。当移除对对象的所有引用，或在代码中手动销毁对象时，对象的析构器会被调用。析构器通常用于各种清理任务，例如关闭数据库连接和释放文件句柄。要创建析构器，请向你的类添加一个方法，并将其命名为 `__destruct`：

```php
<?php

class Circle
{
    public function __construct()
    {
        // 在对象创建时执行操作
        echo "A circle object is being created.\n";
    }

    public function __destruct()
    {
        // 在对象销毁时执行操作
        echo "A circle object is being destroyed.\n";
    }
}

$c = new Circle();

// 销毁 circle 对象
unset($c);
?>
```

运行这段代码将得到：

```
A circle object is being created.
A circle object is being destroyed.
```

注意，你看到析构器内部放置的消息，而无需做任何额外操作。这是因为 PHP 在脚本执行结束时自动清理对对象的所有引用，从而自动调用对象的析构器。

最后需要记住的一点是，与可以有参数的构造器不同，析构器不能有参数。

## Static 关键字

有时在使用面向对象编程时，你可能需要访问类的方法，但不需要创建一个完整的对象。为了满足这一需求，`PHP5` 提供了 `static` 关键字。`static` 关键字是 `PHP5` 的新功能，它允许在不实例化类的情况下使类属性和方法可用。要使类成员静态化，只需在可见性和属性或方法定义之间加上 `static` 关键字，如下所示：

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

要使用新创建的静态属性，你只需使用类名，后跟两个冒号，然后是属性名或方法调用：

```php
$r = 5;
echo "Given a radius of " . $r .
     ", a circle has the area " . Circle::calcArea($r);
?>
```

在浏览器中运行这段代码会产生类似以下的结果：

> Given a radius of 5, a circle has the area 78.539816339745

然而，使用静态方法有一些限制。静态方法不能通过 `$this->` 更改或访问对象变量或方法；它们只能直接访问类中的其他静态属性和方法。

为了在同一类中访问其他静态变量，你可以使用 `self` 关键字，配合双冒号使用。使用 `self::` 类似于 `$this->`，但它仅用于静态成员。如果你想修改 `Circle` 类以使用静态方法和属性，你可能可以做一些类似于以下的事情：

## 第 2 章

## 类常量

伴随着 `PHP5` 中改进的面向对象模型，类常量的概念被引入 PHP。类常量类似于普通的 PHP 常量，但仅在类的定义中可用。与标准 PHP 常量类似，它们的值只能被设置一次，且必须为标量值——一个简单的数字或字符串——任何试图将常量设置为函数结果的尝试都会导致错误。

在使用类常量时，请记住它们的行为类似于静态成员，在访问方式上也是如此——要访问类常量，必须使用双冒号 (`::`) 语法。要定义类常量，请在常量名称前使用 `const` 关键字，如下面的代码所示：



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

运行此代码将产生以下输出：

The value of Pi in our Circle class is 3.14159265359

To recap, the value of Pi in our Circle class is 3.14159265359

在这个例子中，你创建了类常量 `pi`，它惊人地保存了数学常量 Pi 的值。然后，你在 `getPi()` 方法中使用了 `self::` 引用，以返回该常量的值。需要注意的是，在访问 `self::pi` 时，名称 `pi` 前面缺少美元符号。类常量不使用美元符号前缀，而标准的类变量则需要使用。

*你创建一个 Pi 常量仅仅是作为一个示例。PHP 已经内置了一个 `pi()` 函数，用于返回 Pi 的值。*

### 赋值与克隆

如你已知的那样，在标准 PHP 中，将数据赋值给变量有两种方式：按值赋值（assignment by value）和按引用赋值（assignment by reference）。第一种，按值赋值，通常在为变量设置简单值或复制其他变量时使用：

```php
$a = 5;
$b = $a;
```

这里你正在使用按值赋值。当 `$a` 的值改变时，`$b` 保持不变；当你执行 `$b = $a` 时，你只是创建了 `$a` 值的一个副本，并将该值赋给 `$b`。

然而，按引用赋值略有不同。请看以下示例：

```php
$a = 5;
$b = & $a;
```

在这个例子中，你使用 `= &` 运算符按引用赋值。在这种情况下，当 `$a` 的值改变时，`$b` 也会改变——因为 `$b` 通过引用被赋予了 `$a` 的值，这两个变量指向内存中的同一位置，当该内存位置的值改变时，两个变量都会随之改变。

在 PHP5 中，默认情况下所有对象都是按引用赋值的。这种行为不同于 PHP4，PHP4 默认按值赋值，除非使用引用运算符 (`= &`)。在 PHP5 中，如果你想创建一个对象的副本，而不是使用引用，必须使用 `clone` 语句，如下所示：

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

如你所见，`$assigned` 引用了 `$original` 对象，但由于你克隆了 `$cloned`，从而创建了 `$original` 的一个分离副本，当修改 `$original` 时，其值不会改变。

## 继承与接口

使用 PHP5 进行面向对象编程（OOP）的一个好处是，它允许你将代码分解为逻辑块，以促进重用。如果编写得当，这些块可以在许多不同的项目中反复重用，使程序员能够专注于编写针对其试图解决的问题的特定代码。

在 OOP 中，有几种方法可以指定一组方法和属性以供多个类使用。第一种，*继承*（inheritance），允许你定义一组属于基类的基本属性和方法，并将其用作更具体类的构建块。第二种，*接口*（interfaces），允许你规定类必须实现的方法列表。

### 继承

假设你正在创建一个代码库，用于操作不同的几何图形。你在本章中一直使用的 `Circle` 类可能是该代码库的一部分。在为不同的形状（正方形、圆形、三角形等）创建不同的类时，你可能会发现自己在复制所有形状之间相似或相同的方法。这是一个使用继承的好机会。

### extends 关键字

假设所有几何形状类都将在网格上绘制。因此，它们都需要某种*原点*（origin）点 (x,y)。你可以将*原点*属性包含在每个不同的类中，或者使用 `extends` 关键字，通过继承在一个共享位置定义该属性。为此，你将创建一个名为 `Shape` 的类，它将作为你可能创建的所有几何类父类。每个具体的几何形状类——无论是 `Circle`、`Square`、`Ellipse` 还是 `Star`——都拥有由 `Shape` 提供的一组基本功能。理解这种父子关系的一个简单方法是使用短语“*is a*”（是一种）。在这个例子中，`Circle is a Shape`（圆形是一种形状），就像 `Square is a Shape`（正方形是一种形状）和 `Triangle is a Shape`（三角形是一种形状）一样。

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

运行此代码将产生以下输出：

Array

(

    [x] => 0

    [y] => 0

)

如你所见，你创建了一个名为 `Shape` 的基类，它定义了一个通用的 `origin` 属性。通过在 `Circle` 的类定义中使用 `extends` 关键字，`Shape` 的所有属性和方法都成为 `Circle` 对象的一部分。由于 `Circle` 是 `Shape` 的子类，你可以获取 `$origin` 的值，尽管它未在 `Circle` 中显式定义——它是从 `Shape` 继承而来的。

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

Circle Object

(

    [origin] => New origin

)

通过在子类中重新定义基属性 `$origin`，新定义隐藏了父类的值。方法的行为方式相同——在子类中重新定义它们会覆盖父类方法的功能。例如，请看以下代码：

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
            // Content continues from next page
        }
    }
```

return array('x'=>1, 'y'=>1);

}

}

$c = new Circle();

print_r($c->getOrigin());

?>



在这个示例中，`Shape`父类中定义的`getOrigin()`方法在`Circle`子类中被重新定义。当在实例化的`Circle`对象上调用`getOrigin()`时，它返回原点为1,1，而不会调用父类`Shape`中的`getOrigin()`方法。重新定义的方法会屏蔽父类或类中同名的方法。

## final 关键字

在某些情况下，您可能希望禁止子类重新定义基类中已存在的成员。您可以使用`final`关键字来防止属性和方法被重新定义：

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

如果您尝试运行此代码，将会发生致命错误：

```
Fatal error: Cannot declare property Shape::$origin final, the final modifier is
allowed only for methods in /www/plamp/ch02/02-008.php on line 5
```

由于您在基类定义中对`$origin`使用了`final`关键字，当您在`Circle`子类中尝试重新定义它时，会导致致命错误。

请注意，对于属性而言，`final`关键字并不禁止更改其值——仅禁止重新定义。

## 使用 parent:: 引用

在某些情况下，当您在子类中重新定义了某个属性或方法后，您可能需要引用基类中原始的该属性或方法。为了实现这一点，您可以使用`parent`关键字，并配合您在前面静态成员章节中看到的`::`（双冒号）。例如：

```php
<?php

class Shape
{
public function draw()
{
echo 'Shape::draw() has been called.\n';
}
}

class Circle extends Shape
{
public function draw()
{
echo 'Circle::draw() has been called.\n';
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

在这个示例中，您定义了一个子类`Circle`，它继承自基类`Shape`。由于您在子类中创建了一个新的`draw()`方法，因此使用`parent::draw()`来调用父类中的同名函数。以这种方式调用父类方法是重写子类中基类方法时的常见做法，并且在构造函数中调用父类构造函数时也非常常用——否则基类的构造函数不会被自动调用。

## 抽象类

在编程或设计过程中，您可能会发现像`Shape`这样的类需要创建，以便为子类提供相同的属性或方法，但本身从未需要被实例化。您之前使用的`Shape`类是成为抽象类的完美候选者——您永远不希望直接创建`Shape`对象，但对于几何对象的更具体的子类来说，提供这些功能是必要的。针对这种场景，有一个`abstract`关键字。

当一个类被定义为`abstract`时，其他类可以继承它，但它本身不能被实例化。例如：

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

运行此代码，您应该看到类似以下的内容：

```
Array
(
[x] => 0
[y] => 0
)

Fatal error: Cannot instantiate abstract class Shape in
/www/plamp/ch02/02-010.php on line 17
```

通过运行此示例可以看出，`Circle`类按预期从`Shape`继承，但当您尝试单独实例化`Shape`时，发生了致命错误。

既然您已经快速了解了 PHP 中的继承，不妨看看规定对象行为的另一种方式：接口。

## 接口

PHP5 中另一个新的面向对象特性是创建和使用接口的能力。简而言之，接口是一种指定类必须显式实现哪些方法的方式。这在处理许多相互依赖且依赖于彼此特定方法的互连对象时非常有用。

通过使用接口，您可以为不同的可互换类指定一组特定的共享方法。这样，如果您需要替换程序中某个类内的功能，只需确保替换类实现与原始类暴露的相同接口或函数组即可。

例如，您可能有一个包含`calculateInterest()`方法的业务类。在某个时刻，您可能希望有多种计算利息的方式，因此您为每种希望使用的算法创建不同的类。假设所有这些类都实现了一致的接口——即定义了`calculateInterest()`的接口——那么这些类中的每一个现在都应该在程序中是可互换的。

在 PHP5 中，接口使用`interface`关键字定义，并使用`implements`关键字实现，如下所示：

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

通过创建`interface TwoDimensionalOperations`，您可以为不同的形状创建类——圆形、方形、三角形、五边形等——它们都实现该接口。这样，您可以确保通过实现`TwoDimensionalOperations`，所有的形状类都将拥有一个`calculateArea`方法。

在使用接口时，牢记以下几点很重要。首先，如果一个类实现了接口但没有定义该接口中的方法，将会发生致命错误。其次，接口中定义的所有方法必须具有`public`可见性。

使用 PHP5，一个类可以同时继承基类并实现接口：

```php
class Circle extends Shape implements TwoDimensionalOperations
{
    // Circle implementation
}
```

另一个巧妙之处在于，接口可以使用`extends`关键字从其他接口继承：

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

在这个小例子中，您本来可以很容易地在基类`Shape`内部创建一个方法，并简单地将其扩展到子类`Circle`。虽然这种方法是可行的，但由于 PHP 中的类只能继承一个基类，因此这种方法受到限制。

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

结合继承和多个接口，以及继承的接口，您可以使用简单的构建块构建一些非常复杂且功能强大的应用程序。

## 魔术方法

为了在使用面向对象编程时使事情变得更加容易，PHP5 提供了一些所谓的“魔术方法”。这些魔术方法是所有类中特殊命名的方法，在特定场景中会被自动调用。

到目前为止，本章中您已经看到两个魔术方法，`__construct` 和 `__destruct`。它们分别在对象被实例化或销毁时被调用。PHP5 包含一些您可以实现的魔术方法，为您的类提供特殊功能。三个魔术方法—— `__call`、`__get` 和 `__set`——都允许您访问对象中未显式定义的方法或属性。第六个，`__toString()`，定义了当对象直接用作字符串时发生的事情。

## 第 2 章

### `__call`

魔术方法 `__call` 允许你在对象调用未定义方法时提供动作或返回值。`__call` 魔术方法可用于模拟方法重载，甚至可以在对象调用未定义方法时提供平滑的错误处理。`__call` 接受两个参数：方法名称以及传递给未定义方法的参数数组。例如：

```php
<?php

class Circle
{
    public function __call($m, $a)
    {
        echo "The method " . $m . " was called.\n".
             "The arguments were as follows:\n";
        print_r($a);
    }
}

$c = new Circle();
$c->undefinedmethod(1, 'a', 2, 'b');
?>
```

当你运行此代码时，你会看到类似以下内容：

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

在这里，你定义了一个 `__call` 函数来处理对 `undefinedmethod` 方法的调用。正如预期的那样，它接收逗号分隔的参数列表，并将其转换为数组，该数组被存储在 `$a` 参数中。

### `__get` 和 `__set`

魔术方法 `__get` 和 `__set` 允许你指定自定义函数来存储和检索类中尚未定义的属性中的数据。

`__get` 接受一个参数，即属性名称，而 `__set` 需要两个参数：属性名称和新值。

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
$c->nonexistant = 5;
echo "The value of our nonexistant property: " . $c->nonexistant;
?>
```

当你执行上述代码时，PHP 会立即识别出类中不存在名为 'nonexistant' 的属性。由于该命名属性不存在，`__set()` 方法被调用，然后将值赋给类中新创建的属性，从而允许你看到以下内容：

```
The value of our nonexistant property: 5
```

在这个示例中，你创建了魔术方法 `__get` 和 `__set` 来处理任何未定义属性的访问，并继续使用了名为 `nonexistant` 的未定义属性。

### `__sleep`

当你使用 PHP 类来存储必须在页面之间或长时间段内持久存在的数据时，你可以使用你最喜爱的持久化方法（文件、数据库、会话变量或 cookie）来存储对象，但对象必须首先做好准备。

当你重新读取要存储的对象数据时，请使用 `serialize()` 函数。`serialize()` 函数接受任何复杂数据结构并将其转换为字符串，可以使用你的选择方法存储该字符串。相反，要检索你的持久化数据，请使用 `unserialize()` 函数。`unserialize()` 函数接受你的序列化字符串并将其转换回原来的复杂结构。

为了给开发人员在处理对象序列化时提供更大的灵活性，提供了 `__sleep` 和 `__wakeup` 魔术方法。

如果在类中定义了 `__sleep` 魔术方法，它会在对象被序列化之前自动调用。该方法对于关闭数据库连接和清理对象资源非常有用。

`__sleep` 方法还可以返回一个包含要序列化的名称或对象值的数组，这在处理大型对象时非常有用。只有必要的数据会被序列化，而其他数据可以被忽略。

### `__wakeup`

`__wakeup` 魔术方法执行与 `__sleep` 方法完全相反的操作。当调用 `unserialize()` 时，会自动调用 `__wakeup`，这对于重置对象值、恢复连接以及其他初始化任务很有帮助。

看一下 `__sleep` 和 `__wakeup` 的简单示例。这个示例需要两个文件。第一个文件，你将其创建为 `page1.php`：

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

第二个文件，你将其命名为 `page2.php`：

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

    echo 'Rise and shine.....';

    $c = unserialize($_SESSION['c']);

    echo '<br />The contents of our Circle object are:<br />';
    echo 'Radius: ' . $c->radius . '<br />';
    echo 'Origin: (' . $c->origin['x'] . ',' . $c->origin['y'] . ')';
?>
```

将第一个文件 `page1.php` 加载到浏览器中，你应该看到类似于图 2.1 的内容。

![](img/fd2e7361878181c2b12e30301ff3e182_66_0.png)

**图 2.1**

点击链接，你将进入 `page2.php`，在那里你应该看到类似于图 2.2 的内容。



![](img/fd2e7361878181c2b12e30301ff3e182_67_0.png)

**图 2.2**

在第一个文件 `page1.php` 中，你开始会话，以便将对象存储在会话变量中；然后继续创建圆的类定义：

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

        return array('radius', 'origin');
    }

    public function __wakeup()
    {
        echo 'good morning!';
    }
}
```

注意，你在这里创建了 `__sleep` 和 `__wakeup` 两个函数。在这种情况下创建 `__wakeup` 方法并不是必需的，但如果你后来将类定义移动到一个包含文件中，你只需要剪切和粘贴即可。还要注意，你在 `__sleep` 中返回一个字符串数组。这些字符串与 `Circle` 中的属性名称匹配，并告诉序列化函数你要序列化对象的哪些部分，并忽略其他部分。

然后你继续实例化圆对象，更改其中一些值，将其序列化为会话变量，最后提供一个链接前往 `page2.php`：

```php
$c = new Circle();
$c->radius = 5;
$c->origin['x'] = 3;
$c->origin['y'] = 4;

echo 'Preparing to sleep....';

$_SESSION['c'] = serialize($c);

echo '<br /><a href="page2.php">Wake the object</a>';
?>
```

查看 `page2.php`，你再次以启动会话的调用开始，并使用与前一个页面相同的类定义。在反序列化对象时，在调用 `unserialize()` 函数之前，该对象的类定义 *必须* 存在，无论是直接在文件中输入，还是通过 `include` 或 `require` 语句包含。

深入 `page2.php` 的核心部分，你从在前一个页面设置的会话变量中反序列化数据，并将新创建对象的一些属性输出到屏幕上：

```php
echo 'Rise and shine....';

$c = unserialize($_SESSION['c']);

echo '<br />The contents of our Circle object are:<br />';
echo 'Radius: ' . $c->radius . '<br />';
echo 'Origin: (' . $c->origin['x'] . ', ' . $c->origin['y'] . ')';
?>
```

### __toString

可以内置到类中的最后一个魔术方法是 `__toString`。你可以猜到，`__toString` 返回一个自定义字符串值，该值在对象被转换为字符串时自动使用。请查看以下示例：

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
echo "The value of \$c is: ";
echo $c;
?>
```

执行此代码将产生以下结果：

> The value of $c is: Automatic string value for Circle

在这个示例中，你添加了 `__toString()` 魔术方法，并在使用它时，在对象被输出到屏幕时提供了值。注意，你并没有简单地在该 `echo` 语句中将对象连接到字符串的末尾，也没有将其包含在双引号字符串内。

如果你只是在一个 `echo` 语句中将对象与其他字符串一起包含会发生什么？请查看以下代码（更改部分已突出显示）：

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
echo "The value of \$c is: " . $c;
?>
```

当你运行此代码时，你会看到以下内容：

> The value of $c is: Object id #1

这肯定不是你预期的结果！它没有返回 `__toString()` 方法的值，而是返回了 `$c` 的对象 id——这与如果你没有定义 `__toString()` 所看到的完全相同。`__toString()` 魔术方法只有在直接用于 `echo` 或 `print` 时才会被调用——如果存在任何其他字符串或强制类型转换，将返回对象 id。

## 摘要

如你所见，PHP5 为你的项目带来了功能大幅改进的对象模型。无论你决定坚持使用面向过程的编程、偶尔涉足面向对象编程（OOP）、完全投身于 OOP，还是找到介于两者之间的路径，希望本章中你看到的一些内容能帮助你着手开始使用 PHP5 的新 OOP 构建自己的系统。

从这里开始，你将远离 OOP，深入 PHP 语言中一些较为晦涩的角落。你可能已经知道数组在 PHP 中有多么强大，但你可能并不清楚 PHP 拥有多少函数来让你利用这种力量。一旦你掌握了这一点，我们将向你介绍流（streams）的概念，这将让你能够使用一组通用的函数来处理网络资源和本地文件。

![](img/fd2e7361878181c2b12e30301ff3e182_72_0.png)

## 更晦涩的 PHP

PHP 的一个显著特征是其庞大的内置函数集合，甚至在开始添加可选扩展之前也是如此。这在某种程度上可以说是一个缺陷，因为它使得在特定情况下决定使用哪个函数变得更加困难。许多函数的行为如此相似，以至于有时很难看出为什么它们要作为独立的函数存在。是使用 `split()` 还是 `preg_split()`？使用 `str_replace()` 还是 `strtr()`？使用 `ksort()`、`asort()`、`rsort()`、`natsort()`、`usort()` 还是 `uksort()`？使用 `strftime()` 还是 `date()`？这本书不会深入讨论关于函数命名或缺乏参数顺序规范的问题，以及许多函数仅仅是其他函数别名的事实。

PHP 函数集重叠的一个原因是其早期作为 Perl 库以及后来 C 库的包装器而存在。熟悉这些语言函数库的用户会发现他们的 PHP 对应版本使用相同的名称和调用约定，并叠加了 PHP 的内存管理和类型处理。扩展功能加剧了这种情况——不同的 DBMS 暴露不同的 API，PHP 为它支持的每个 DBMS 引入了不同的函数集。当两个扩展都声称拥有针对两个相似事物的函数时，PHP 就提供了两者。

随着 PHP 在更多种类的平台和环境中被更广泛地实施和构建，平台无关的函数实现开始被引入。因此，既存在 `rand()`（它使用 PHP 构建所在的 C 编译器提供的任何伪随机数生成器），也存在 `mt_rand()`（它在所有平台上行为完全一致）。与此同时，PHP 开发者致力于向后兼容性；即使引入新机制，他们也会尽最大努力保留旧机制，以防有人依赖它们。

因此，PHP 的函数列表激增，膨胀得像一块放在太小模具里正在发酵的面包。据最后统计，PHP 手册有 3,630 个函数条目，分布在 129 个章节中，其中 855 个列在手册描述为“核心”的 30 个章节中（或捆绑在一起，需要显式配置开关才能禁用）。这些数字已经过时。

实际结果是，许多 PHP 程序员就像英语使用者一样——他们只使用语言的一小部分子集。语言中有部分他们可能根本用不到。但在 PHP 的深奥之处中，隐藏着一些未得到应有关注的函数。这些是至少自 PHP 4.3.2 版本以来就存在的函数——许多自 PHP 4 早期就已存在。尽管如此，它们经常被忽略，即使它们是当前任务的最佳选择。其中一些似乎只在关于它们的教程中被使用。它们绝不是该语言中唯一的晦涩特性。相反，它们代表了 PHP 环境中最强大的核心功能之一，并且是近期版本中活跃开发的领域。

本章旨在纠正这种不公。

## 数组函数和回调

数组函数允许你访问和操作数组的内容，而无需先提取它们。你可能希望对“数组的每个元素”执行的大部分（如果不是全部）操作都可以使用这些函数完成，而不需要 `for` 或 `foreach` 循环的额外基础设施。此外，许多数组操作任务需要考虑整个数组。排序是一个明显的例子：如果不查看数组的所有元素以找到最小元素，你就无法将最小元素移动到数组的开头。任何尝试编写合理高效的排序算法的人都知道，这项任务并非微不足道。



由于 PHP 开发者无法预测你想对数组做什么，大多数数组函数，以及相关的数组，都接受一个称为回调（callback）的额外参数，它指定了另一个函数的名称。根据数组函数的功能，该函数将用于操作数组元素，或将它们相互比较或与你指定的某个标准进行比较。这样，PHP 只需提供数组操作更抽象方面的实现，例如映射和遍历，让你可以自由地提供你选择的具体细节。
事实上，回调在抽象功能方面非常有用，以至于提供了一些函数，使其几乎可以在任何情况下使用。实施你自己的 OOP 架构完全是可以想象的（尽管有些堂吉诃德式），其中对象的“方法”表示为回调数组。

## 使用回调

考虑以下脚本：

```php
$inup_file = file('generic.txt');
foreach($inup_file as $k=>$line)
{
   $inup_file[$k] = rtrim($line);
}
```

你正在将文本文件加载为单行字符串数组。PHP 不会丢弃末尾的换行符，所以既然它们已经完成使命，你想自己去掉它们。编写整个循环并在其中使用两个额外变量似乎很啰嗦。首先，你必须记住 `$line` 是副本，所以 `$line=rtrim($line);` 不起作用，这意味着你必须通过数组和键回到原始值。要么那样做，要么记得通过编写 `foreach($inup_file as &$line)` 将 `$line` 声明为引用。任何错误都意味着最终数组的行不会修剪。
现在考虑这个：

```php
$input_file = array_map('trim', file('generic.txt'));
```

这行代码达到了相同的效果。`file()` 返回包含 `generic.txt` 行的数组；`array_map()` 将函数 `trim()` 应用于该数组的每个元素，并返回修剪后的结果数组。
有几个函数抽象了遍历数组的最常见原因，减少了编写循环和其他流程控制语句的需求。虽然仅仅为了写单行代码而写单行代码可能导致难以阅读的代码，但减少程序中的“活动部件”有助于减少错误的发生。
当你有一个数组，需要对每个元素依次执行任务时，`array_map()` 和 `array_walk()` 值得考虑。还有其他函数以类似的方式使用所谓的回调函数，以省去你自己对数组每个元素调用函数的麻烦。
回调有两种形式。第一种，也是最常见的，是包含函数名称的字符串。在上一行代码中，它是 `'trim'`。
> 它必须是一个函数，这就是为什么 PHP 手册强调指出 `echo`、`empty`、`include`、`array` 等*不是*函数。传递 `'include'` 作为你的回调将失败。排除它们的原因是它们在解析期间受到特殊对待，拥有自己的内部结构。
第二种回调用于指定类和对象方法。两者都由双元素数组表示，其中第二个元素是作为字符串存储的方法名称。如果第一个元素是一个对象，则回调引用该对象的方法：`array($object, 'method')`。另一方面，如果第一个元素是字符串或字符串变量，则回调引用指定类的静态方法：`array('thing_factory', 'create_new')` 引用静态的 `thing_factory::create_new()` 方法。

```php
// 在 array_map() 中使用对象的方法作为回调。
// $untidy_array 的每个元素依次传递给 $parser->tidy()，
// 并返回值存储在 $tidied_array 中
$tidied_array = array_map(array($parser, 'tidy'), $untidy_array);

// 在 array_map() 中使用静态类方法作为回调。
// $untidy_array 的每个元素依次传递给 Parser::tidy()，
// 并返回值存储在 $tidied_array 中
$tidied_array = array_map(array('Parser', 'tidy'), $untidy_array);

class Parser
{
// 一个示例方法，修剪单行文本末尾的空格和
// 以‘#’开头的 shell 风格注释。
static function strip_comments($Element)
{
$Element = preg_replace('/#(.*)$/', '', $Element);
$Element = rtrim($Element);
return $Element;
}
}
```

```php
$shell_script = file('foo.sh');
$tidied_script = array_map(array('Parser', 'strip_comments'), $shell_script);
```

在类和对象中，魔术词 `self` 和 `this` 在回调中也能正常工作，其行为符合预期：`array($this, 'method')` 和 `array($work, 'method')` 分别被解释为引用 `$this->method()` 和 `self::method()`。关于诸如静态函数不允许使用 `$this` 等常规限制依然适用。例如：

```php
// An object is able to use its own methods in array callbacks,
// both on arguments passed to it and on its own properties.
$tidied_code = array_map(array($this, 'tidy'), $this->code_array);

// Class methods are also accessible as callbacks within the class.
```

如果你想检查给定的 `$variable` 的内容是否确实指定了一个可调用的函数或方法，布尔函数 `is_callable($variable)` 将说明这一点。

## array_map()

你刚刚看到了 `array_map()` 最简单的应用之一，但它的应用范围远不止于此。
最重要的是，它可以同时操作多个数组。假设你有两个数组——`$arr1` 和 `$arr2`——并且你想构建一个由 `func($arr1[0], $arr2[0])`、`func($arr1[1], $arr2[1])`、……、`func($arr1[n], $arr2[n])` 组成的数组。用循环实现这一点的代码大致如下：

```php
$new_array = array();
for($i=0, $limit=max(count($arr1), count($arr2)); $i<$limit; $i++)
{
    $arg1 = isset($arr1[$i]) ? $arr1[$i] : null;
    $arg2 = isset($arr2[$i]) ? $arr2[$i] : null;
    $new_array[$i] = func($arg1, $arg2);
}
```

注意，为了确保当数组长度不同时，循环不会因 `func()` 缺少参数而运行出错，需要进行上述测试。
现在，将其与使用 `array_map()` 产生的等效代码进行比较：

```php
$new_array = array_map('func', $arr1, $arr2);
```

如果这不起作用，你有权向 bugs.php.net 提交报告。而且，六个月后当你回过头来看你的代码时，哪一个需要更长的时间重新熟悉？
`array_map()` 可以实现的另一个技巧源于它可以接受 `null` 作为回调。在这种情况下，其行为可以描述为“接收一堆事物数组，返回一堆事物数组的数组”。每个数组的第 0 个元素组合成一个单独数组，成为结果数组的第 0 个元素；每个数组的第一个元素组合成一个单独数组，成为结果数组的第一个元素；以此类推。换句话说，如果你将其数组参数视为矩阵的列，`array_map(null, ...)` 返回的是转置矩阵。这实际上就是如果你被允许使用 `array` 作为回调时，你所期望的 `array_map('array', $arr1, $arr2)` 的行为。
这个技巧不仅限于一次只组合两个数组。如果回调函数需要 *n* 个参数，那么 `array_map()` 需要传入 *n* 个数组。因此，如果你有一个接受六个参数的函数，以及一个由六元组组成的数组，你想对每个六元组运行该函数，并将所有结果收集到一个新数组中，`array_map()` 将非常适用。
> 严格来说，这里有两处 `array_map()` 调用。第一处使用 null 回调，接收原始的 `array[0..n] [0..5]` 并返回转置的 `array[0..5] [0..n]`；第二处将回调函数应用于 `array[0], array[1], ...array[5]` 的连续元素。



`array_map()` 有两个明显的局限性。首先，回调后的每个参数都必须是数组。如果你想在整整一个数组的操作中使用单个变量（例如将数组中的所有值限制在某个最大值以内），则必须执行以下操作之一：

- 在全局作用域中声明该变量，并在回调函数内部使用 `global`（这不是最吸引人的选项）
- 使用 `array_fill()` 创建一个由副本组成的数组（仅当你不介意操作在变量的独立副本上执行，或者变量是按引用传递的对象或资源时才有用）
- 退而求其次，最终使用循环
- 使用不同的函数：具体来说，是 `array_walk()`
- 使用一种在编写面向对象代码时可考虑的选项：将回调设为方法，将变量设为对象的属性

另一个明显的局限性是，你需要预先知道要一起映射多少个数组，并在函数调用中显式列出它们。你可以通过将输入数组的对应元素包装到一个单一数组的单个元素中，然后将该数组的元素传递给回调函数来绕过这个问题。但这需要重写回调函数，或者在无法重写时编写一个包装函数来解包合并后的元素，并将其内容传递给真正的回调。你会意识到，这样做后你又回到了起点。幸运的是，PHP 也提供了一种解决方案，即本章后面介绍的 `call_user_func_array()`。

### array_walk()

想象一下，你正在使用 GD Lib 图形绘制扩展来绘制图表，并且你有许多数据点需要用不同大小和颜色的圆圈来表示。位置和半径已经缩放到图像坐标，颜色也已分配，并由图像调色板索引标识（由 `imagecolorallocate()` 返回）。你收到一个数据点数组，每个元素依次包含 *x* 坐标、*y* 坐标、半径和颜色。例如：

```php
$_data_points = array(
   array(10,10,5, $palette['black']),
   array(10,20,5, $palette['black']),
   array(20,13,5, $palette['darkolivegreen']),
   ...
);
```

#### 第 3 章

查阅 PHP 手册，合适的函数似乎是 `imageellipse()`。你的数据和它的参数之间的唯一区别在于，它期望宽度和高度，而提供的数据只包含半径。但这是一个微不足道的区别。首先，定义一个函数：

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

这实际上相当直接明了。当然，如果每个数据点是一个关联数组或对象——通过名称标识其组件，`imagedatapoint()` 会更易读。你可以问的一个问题是，为什么将循环放在函数外部？确实，你更有可能在图表上绘制多个数据点，而不仅仅是一个。这是一个示例：

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

但 `array_walk()` 可能如何实现呢？首先，它使用一个回调函数。这实际上就是之前循环的循环体。

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

与 `array_map()` 不同，`array_walk()` 作用于原始数组的引用。因此，如果回调函数按引用获取其数组元素参数，则该元素的值可以被函数修改，且更改将反映回传递给 `array_walk()` 的数组中。

### array_filter() 和 preg_grep()

从名称即可轻松推断出 `array_filter()` 的操作：给定一个数组，它返回该数组中满足给定条件的元素。该条件以一个回调形式提供，该回调是一个返回布尔值的函数（想想 SQL 查询中的 WHERE 子句）。一系列 `array_filter()` 调用可能比单个遍历数组的循环更容易理解，后者通常充满了各种测试和分支，旨在判断是否保留某个给定元素，并构建包含成功元素的新数组。然而，类似于 `array_map()` 的局限性也适用于此，即除了输入数组和回调外，它不接受其他额外参数。

```php
function is_a_square_number($n)
{
    // 对于不适合 sqrt() 的值，直接失败。
    if(!is_numeric($n))
        return false;
    if($n<0)
        return false;
    $square_root = sqrt($n);
    return ($square_root == intval($square_root));
}

$numbers = array(-1,0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,'!');
$squares = array_filter($numbers, 'is_a_square_number');
// 此时 $squares 包含数组 (0,1,4,9,16);
```

由于过滤包含特定模式的字符串是数组过滤任务中常见的子类，且正则表达式在描述此类模式时也常常很有用，PHP 提供了一个专门用于此任务的函数：`preg_grep()`（正如名称所暗示的那样，它是 PCRE 函数之一，行为类似于 grep 程序）。它不使用回调函数（而是使用正则表达式），但它为从 `array_filter()` 到下一节函数的功能提供了一个不错的过渡。以下是 `preg_grep()` 语句的一个示例：

```php
// 此处的 preg_grep 使用获取当前目录列表，并仅保留
// 那些以四位数字后跟 ".jpg" 或 ".jpeg" 结尾的文件名。
$images = preg_grep('/\d{4}\.jpe?g$/', scandir('.'));
```

> 若要使用类似 shell 的语法根据更简单的条件过滤目录列表，请参阅 `glob()` 函数。

### preg_replace_callback()

`preg_replace()` 使用的语法包含 `/e` 修饰符开关。当使用此修饰符时，给定的替换文本被视为 PHP 代码并进行求值，以确定实际的替换文本应该是什么。但在尝试将所有必要的代码塞进去时，这很容易变得棘手。因此，实现了 `preg_replace_callback()`，使得您只需提供回调，而无需将替换代码直接写入函数调用中。这可以大大简化复杂的正则表达式。由于回调函数可以包含任意数量的字符串处理和模式识别代码，因此 `preg_replace_callback()` 中使用的正则表达式只需足够复杂，以保证找到所有期望的匹配项，即使有些不需要的匹配项通过。进一步的测试可以在回调中进行；如果进一步测试失败，回调只需原样返回匹配项即可。（但请注意，如果不需要的匹配项恰好与后续的期望匹配项重叠，那么后者将被漏掉。`preg_replace_callback()` 并不关心后续测试是否“成功”）。

例如，为了将电子邮件地址包裹在 `mailto:` 链接中而进行匹配，如果您想要彻底检查，可能会得出一些令人畏惧的正则表达式。分阶段处理方法要容易得多。您可以从尝试定位 `@` 字符开始，其两侧为非空白字符，如下所示：

```php
preg_replace_callback('/([^\s@]/@([^\s@]/)', $text, 'wrap_emails');
```

并让回调承担验证匹配字符串是否真的是电子邮件的繁重工作：



```php
function wrap_emails($possible_match) { 
    $possible_email = $possible_match[0]; 
    // 回调将接收一个数组 
    if (is_rfc822_compliant($possible_email)) 
        // 一个假设的函数， 
        // 执行所有繁琐的工作 
        return '<a href="mailto:' . $possible_email . '">' . $possible_email . '</a>'; 
    else 
        return $possible_email; 
    // 不是电子邮件，原样返回子字符串。 
}
```

使用 `preg_replace_callback()` 的第二个示例是模板系统。通过 `preg_replace_callback()` 仅识别模板中的插槽，其传递给匹配项的回调函数随后会仔细检查插槽——这一任务因插槽已由也跟踪其在模板中来源位置的函数从模板其余部分中隔离出来而变得更容易。这里有一个示例：

```php
function include_templates($template_name) { 
    if (is_string($template_file)) 
        $template_file = $template_name; 
    else 
        $template_file = $template_name(1) . '.tpl'; 
    $template = file_get_contents($template_file); 
    return preg_replace_callback('/\((include: \S*(\^\S\))*/)', 'include_templates', $template); 
}
```

这个递归函数假设您的所有模板文件扩展名均为 `.tpl`，且您在模板中用于包含 `foo.tpl` 的语法是 `(include: foo)`。不用说，如果 `foo.tpl` 本身包含包含项，您也希望将这些包含项包括在内。

如果向该函数传递一个字符串，则该字符串被解释为模板文件的名称。如果传递一个数组（原因很快就会清楚），则期望的文件名是数组的第二个元素，并附加 `.tpl`。然后，指定文件的内容被读取到 `$template` 中。（这里几乎没有错误检查。）

对 `preg_replace_callback()` 的调用会在 `$template` 中搜索匹配 `(include: foo)` 语法的字符串。包含匹配字符串的数组（其中第 0 个元素包含整个匹配字符串，第 1 个元素包含第一个带括号的子字符串）随后逐个传递给 `include_templates()`，该函数从数组中提取模板文件名，并在调用 `preg_replace_callback()` 后，返回模板文件的内容——所有 `(include: foo)` 部分都已被对应模板文件的内容替换。

不幸的是，没有 `preg_match_callback()` 或 `preg_match_all_callback()`。但由于回调函数可以执行任何操作，它也可以将已传递给它的匹配项存储在某处（也许是全局变量，或者更好是类或对象属性）。然后，它可以简单地返回其参数的第 0 个元素，导致 `preg_replace_callback()` 用自身替换任何匹配的子字符串，保持不变。因此，电子邮件收集对象可能包含一个像这样工作的方法。

```php
function collect_email($possible_match)
{
    $possible_email = $possible_match[0];
    if(self::is_rfc822_compliant($possible_email))
        $this->emails = $possible_email;
    return $possible_email; // 原样返回匹配项
}
```

无论上述方法是否存储电子邮件地址，它都会原样返回它。因此，`preg_replace_callback()` 将用自身替换匹配的子字符串，保持原始文本不变。

### `call_user_func_array()` 和 `call_user_func()`

回顾在 `array_map()` 部分末尾讨论的 *两个* 明显局限性。第一个已由 `array_walk()` 解决。第二个是您需要预先知道有多少个数组正在一起映射，并在函数调用中明确列出它们所有。有时，您直到运行时才知道这一点。在我的一个程序中，我拥有一个数值矩阵（大小可变），存储为行的数组（每行本身也是一个数组），我需要转置它（以便最终得到列的数组）。我可以编写一个双重嵌套循环，一个用于遍历行，另一个用于在每行内遍历，类似于这样：

```php
$transposed_matrix = array();
for($row=0, $row_count=count($matrix); $row<$row_count; $row++)
{
    for($column=0, $column_count=count($matrix[$row]), $column<$column_count;
        $column++)
    {
        $transposed_matrix[$column][$row] = $matrix[$row][$column];
    }
}
```

即使在编写上述示例代码时，我也不得不暂停几次，以确保我的行和列方向正确，但通过编写以下代码即可实现期望的效果：

```php
$temp = $matrix;
array_push(null, $temp);
$transposed_matrix = call_user_func_array('array_map', $temp);
unset($temp);
```

`call_user_func_array()` 是另一个接受回调的函数。其第二个参数是一个数组，列出了要传递给回调函数的所有参数（这与您在回调函数内部调用 `func_get_args()` 时得到的数组相同）。为了举例说明，假设 `$matrix` 是 `{(1,2), (3,4)}`，并跟随发生的情况：

# 第 3 章

```php
$matrix = array(array(1, 2), array(3, 4));
$temp = $matrix;
array_push(null, $temp);
$transposed_matrix = call_user_func_array('array_map', $temp);
```

`array_map()` 的第一个参数是回调函数的名称，因此将 `$temp` 的第一个参数设置为该回调函数（在本例中，这是一个为 null 的回调函数）。这就是为什么我需要 temp 变量；`array_push()` 修改的是原始数组，而不是返回一个副本。我本可以冒险直接使用 `$transposed_matrix` 本身来代替 `$temp`，从而省去这个变量和最后的 `unset()`。之所以说这是冒险的，是因为这样做会略微降低代码的可读性（一方面将变量创建视为 `array_map()` 的列表参数，而两行代码后却将其用于完全不同的用途，即 `array_map()` 调用的结果）。

```php
$temp = array(null, array(1,2), array(3,4));
$transposed_matrix = call_user_func_array('array_map', $temp);
```

下面是手动执行 `call_user_func_array()` 的结果。

```php
$transposed_matrix = array_map(null, array(1,2), array(3,4));
```

因此，看待 `call_user_func('foo', array(arguments))` 工作原理的一种方式，就是将其视为获取一个数组，并用 `foo(arguments)` 替换其中的 `array(arguments)`。

为了完成这个示例，我们来评估 `array_map()` 的调用结果：

```php
$transposed_matrix = array(array(1,3), array(2,4));
```

`call_user_func_array()` 的实际意义在于，你可以将函数的所有参数存储在一个单独的数组中，而无需知道参数的数量（考虑到许多 PHP 函数接受可变数量的参数，你自己的函数也可以这样做），也无需手动将数组中的每个元素取出并插入到函数调用中。



之所以采用这样一个略显冗长的名称，是因为还有一个 `call_user_func()` 函数。与接收回调及其参数作为数组不同，它*显式地*接收回调及其参数。正如你可以将 PHP 看作是将 `call_user_func_array('foo', array(arguments))` 转换为 `foo(arguments)` 一样，`call_user_func('foo', arguments)` 在不使用中间数组的情况下直接转换为 `foo(arguments)`。

听起来这似乎与将 `'foo'` 放入变量 `$func`，然后编写 `$func(...)` 在效果上是相同的。对于普通函数而言，确实如此。但对于对象方法来说，情况则截然不同。试一试：

```php
<?php
class foo
{
    public function bar($a, $b)
    {
        echo "I'm here! $a! $b! And all that!";
    }
}

$t = new foo;
$x = array($t, 'bar');
$x('1066', '42');
?>
```

结果是一个致命错误：PHP 要求函数名必须是字符串。因此，不能像变量函数那样直接调用，而是必须编写以下代码：

```php
call_user_func($x, '1066', '42');
```

然后你才能得到所需的结果：

```text
I’m here! 1066! 42! And all that!
```

### create_function()

还有最后一道障碍需要克服。到目前为止，提到的所有回调都是预先存在的、写入原始代码中的函数。然而，有时这还远远不够。有时，直到函数作为回调被需要的那一刻，我们才确切知道函数应采取何种形式；或者，也许只是不想为了一个只执行一次的具体任务而在代码中放置一个完整的函数。如果能有一种方法在运行时定义函数，或者显式地定义而不是通过回调名称来定义，那该多好。

其实已经有了：构建一个包含函数文本的字符串，将其包裹在 `function whatever(...){ }` 中，然后对其进行 `eval()`。但可能会出现一些问题。你必须记住，由于函数只能声明一次，该字符串只能被评估一次；你必须记得给每个这样的函数赋予一个唯一的名称——`whatever0()`、`whatever1()` 等等——如果这种创建操作可能会执行多次，那么在包含该评估过程的函数、方法或类中某处就需要一个计数器（可能是一个静态变量）。当然，如果你在代码的多个地方这样做，你需要确保在不同位置生成的函数名不会冲突。一种优雅的做法是拥有单个“创建函数的函数”，它使用单个静态变量来防止命名空间冲突，并传入函数的文本，让它计算出适当的名称，评估生成的定义，并返回生成的名称作为回调。实际上，你会希望传入两个字符串——一个用于函数体，另一个用于参数列表——然后它会执行 `eval("function whatever\$n\$arguments) {$body} ");`。有可能已经存在一个名为 `whatever1()` 的函数，因此当你的函数试图创建一个新的函数名时，它必须检查该名称是否尚未定义。此外，还可能存在一种可能性，即它创建了一个名为 `whatever1()` 的函数，而未意识到在程序的后续部分，你也会试图创建一个名为 `whatever1()` 的函数。防止这种情况的唯一方法是强制执行编码标准，规定不允许声明具有特定形式名称的函数。

但请别麻烦。这样的函数已经存在，并且其工作方式与刚才描述的完全一致，此外还有一个细微之处，可以完全避免与你自己的函数发生命名空间冲突。PHP 的 `create_function()` 创建一个匿名函数，这意味着它不会出现在由 `get_defined_functions()` 生成的列表中。然而，它确实*拥有*一个名称（即使是匿名的人也有名字——你只是不知道而已）。首先，有它在解析和编译期间的名称：在它自己的逻辑中（即魔术常量 `_FUNCTION_` 的值），它认为自己叫 `_lambda_func_`。（术语“lambda 函数”与“匿名函数”同义，源自 1936 年称为 Lambda 演算的计算模型，并通过 LISP 传播。）一旦创建完成，就有它在程序其余部分所知的名称，这正是 `create_function()` 实际返回的字符串，准备就绪可直接用作回调。从 `create_function()` 返回的第一个字符串是 `" \0lambda_1"`；第二个是 `" \0lambda_2"`，以此类推。好吧，如果你定义了一个名为 `lambda_1` 的函数，然后使用 `create_function()` 会发生什么？是一个覆盖另一个，还是会出现错误，或者匿名函数被命名为 `lambda_2`？如果这些选项出现在多项选择测试中，你可以排除第一个选项，因为它违反了 PHP 关于函数不可变性自身的规则，留下选项 B 或 C。然而，正确答案是 D，以上皆非。

```php
<?php
function lambda_1($a)
{
    return $a;
}
$anonymous_function = create_function('$a', 'return strrev($a);');
echo "The anonymous function has been named $anonymous_function.\n";
$_use_this = 'lambda_1';
echo $_use_this('generic string'), "\n";
$_use_this = $anonymous_function;
echo $_use_this('generic string'), "\n";
?>
```

运行这段代码将得到以下结果：

```text
The anonymous function has been named  lambda_1.
generic string
gnirtsirec
```

那么，如果它们同名，PHP 如何知道该使用哪一个？简单的事实是它们并不同名。如果你仔细查看代码示例输出和上一段文字的排版，匿名函数的名称看起来是以空格开头的。实际上，它不是空格，而是 null 字符 `0x00`。这很狡猾：你无法声明一个具有这种形式名称的函数，也无法调用这样一个名称的函数，因为在两种情况下，源代码中的 NUL 都会被 PHP 的词法分析器忽略为空白字符。然而，知道这一点使得手动通过字符串字面量构建匿名函数的名称成为可能（使用诸如 `chr(0) . 'lambda_n'` 的代码，或使用允许直接插入 NUL 的编辑器）。不过，这可能没什么好处，因为一旦你丢弃了原始字符串，或者你忘记了哪个变量包含哪个匿名函数的名称，你就得自己弄清楚你想要的是第 3 个、第 5 个还是第 750 个这样的函数。如果你为数组中的每个元素创建一个不同的匿名函数，即使它们在功能上是相同的，你也很容易积累几百个这样的函数。（PHP 不会尝试比较两个匿名函数以查看它们是否包含相同的代码，就像它不会对此类普通函数那样做一样；而且，如果你在一个循环中创建函数，很可能有一些部分每次迭代都会发生变化——否则，为什么要用循环来做呢？）如果你能跟踪这些事情——例如，以某种方式知道你的 750 个函数的编号是从 10 到 759——那么你不需要保留一个包含所有名称的 750 个字符串的数组，可以通过编写以下代码重新创建它们：

```php
function recreate_function($lambda)
{
    return chr(0) . 'lambda_' . $lambda;
}
$lambda_functions = array_map('recreate_function', range(10,759));
```

# 更冷门的 PHP

## 关于数组函数的最后观察

就函数数量而言，数组函数构成了手册函数列表中最大的章节之一：仅略逊于文件系统函数，且与字符串处理函数的数量相差不远。尽管回调允许大量的抽象，为什么会有这么多函数？并且使用它们如何有助于提高代码质量？

## 如此多的数组函数

在 PHP3 和 PHP4 的整个发展历程中，数组函数列表中存在明显的空白。曾经有一个函数允许你使用自定义的“小于、大于或等于”定义来对数组进行排序，但没有任何一个数组函数允许你使用自定义的“相同”定义，从一个数组中移除所有与另一个数组中元素“相同”的元素。随着 PHP 版本的迭代，这些空白被识别出来，并实现了新的函数来填补它们。

一个主要因素追溯到本章开头提到的功能重叠。拥有两个行为非常相似的函数会导致它们在如何被强调方面存在差异。存在一个用于对数组进行排序的函数，还有一个使用回调对数组进行排序的函数。存在一个按键排序的函数，还有一个使用回调按键排序的函数。自然的问题是，这些差异对于其他数组函数是否有意义。



如果你想象所有可能的函数是某个巨大空间中的单个点，现有的函数提供了一组参考点，通过这些点可以绘制出这个空间。拥有 `sort()` 和 `usort()` 暗示了提供回调的趋势；从中可以看出，`ksort()` 和 `uksort()` 表明你可以独立地向“按键”而非按`值`的方向移动。既然这些方向已经被指出，拥有 `array_diff()` 不可避免地会暗示带有回调的 `array_udiff()`、“按键的 array_diff()”，以及当然带有回调的按键 `array_udiff()`。PHP5 已经实现了许多这些新函数，如 `array_udiff()`，还有许多其他函数在 CVS 版本中，如果尚未包含在稳定版本中。

“正交”意味着直角；换句话说，尽可能远离平行。由于 PHP 的早期函数中有许多彼此非常相似，以至于它们在“函数空间中指向几乎平行的方向”，使用它们会暗示其他几乎平行的函数（例如 `array_intersect_assoc()` 和 `array_uintersect_uassoc()`），从而导致 PHP 函数密集聚集的区域。数组函数就形成了这样一个密集的集群。你肯定会发现，要有效使用它们，并不一定需要熟悉 PHP 的所有数组函数，并且一致地应用少量尽可能互不相关的函数的简单组合，就能获得你所需的所有功能。这就是正交性。*哪几个*函数由你决定。

## 一个接一个的数组函数

当使用一系列数组函数来操纵数组内容时，与在循环中直接对数组元素进行操纵相比，操作执行的顺序有显著不同。这可能影响诸如程序内存需求等考量。

考虑这个简短的例子：

```php
$array = array_map('do_something_fancy', $array);
```

这等价于：

```php
foreach($array as $value)
{
    $value = do_something_fancy($value);
}
```

在前者中，在 `array_map()` 评估之后有一个短暂的瞬间，此时存在**两个完整的数组**。当然，在赋值之后，`$array` 的旧版本被丢弃，内存被回收，但这要等到赋值完成且对原始数组的引用计数降为零时才会发生。如果数组很大，所需的额外空间可能很显著，大块的内存被分配，然后短时间内*其他*大块内存被*释放*。自然，如果输出数组进入与输入数组不同的变量，释放就不会发生，而由 `array_map()` 函数实现执行的一次性经济型分配可能比 `$new_array[] = do_something_fancy($value);` 中发生的逐元素零散活动更有效率。显然，当可能时，应当优先应用那些可以输出比输入更短数组的函数，如 `array_filter()`、`array_udiff()` 和其他函数，因为它们可以减少后续函数的工作量。

如果有一系列返回数组的 `array_` 类型函数，每个函数使用前一个函数的结果，这种批量往返对于 PHP 的内存管理和操作系统来说可能会变得相当乏味。可以通过编写类似以下内容来在一定程度上（但仅限*一定*程度）避免这种情况：

```php
array_walk(
    array_map(
        'do_something_fancy',
        array_filter(
            array_map('nothing_fancy', $array),
            'purge'
        )
    ),
    'traverse', 'sideways'
);
```

而不是这样：

```php
$array = array_map('nothing_fancy', $array);
$array = array_filter($array, 'purge');
$array = array_map('do_something_fancy', $array);
array_walk($array, 'traverse', 'sideways');
```

但没人会相信前者更容易阅读。除此之外，函数的出现顺序与应用顺序相反。诚然，参数传递给函数的顺序看起来没有任何一致性，这无助于外观。你能说的最好之处是，它有助于抑制运行时错误——如果你不小心将 `array_map` 误拼为 `array_filter`，PHP 会在运行时抱怨“第一个参数 `$array` 应该是 NULL 或有效的回调”。

## glob()

你经常会发现自己需要做的任务之一是遍历目录中名称符合特定模式的文件——例如所有文本文件或图像文件。这可以比将文件存储在文件系统中，在其他地方维护这些文件的列表，然后保持两者同步更简单。

而且可能同一目录中还有其他类型的文件。这是一个如此常见的任务，任何 shell 接口都提供“globbing”——你可以列出 *.png，删除 temp_* 等。在 PHP 4.3 之前，实现相同效果的典型方法会使用 `readdir()`，并且根据手册中该函数用法的示例，最终得到类似这样的结果：

```php
$flist = array();
if ($handle = opendir('directory'))
{
    while (false != ($file = readdir($handle)))
    {
        if (substr($file, -4) == '.txt')
        {
            $flist[] = $file;
        }
    }
    closedir($handle);
}
```

PHP 5 引入了 `scandir()`，它封装了整个 `opendir()` / `readdir()` / `loop()` / `closedir()` 流程，将过滤文件名的工作留到最后，在这个例子中，可以通过 `preg_grep()` 像这样处理：

```php
$flist = preg_grep('/\.txt$/', scandir('directory'));
```

但自从 PHP 4.3 起，即使这样也是不必要的复杂。通过使用类似的 shell globbing 语法，其中 ? 代表'任何单个字符'，* 代表“任何字符串”，你可以使用与在 shell 中相同的语法来执行相同的文件名过滤。`$flist = glob('*.txt', 'directory');`

`glob()` 函数有几个可选标志，可以按位或运算一起使用以调整函数行为。例如，如果相关目录包含混合的 JPEG 和 PNG 文件（当然还有杂乱无章的其他类型，以及不可避免的 . 和 .. 目录），可以设置 `GLOB_BRACE` 标志，并将通过扩展名识别这些文件的替代 glob 模式作为逗号分隔的列表放在花括号中传递给 `glob()`：

```php
$flist = glob('{*.jpg,*.jpeg,*.png}', 'directory', GLOB_BRACE);
```

## PHP 流

从 PHP4.3 开始，PHP 的 URL 包装器（允许你在通常期望文件名的地方使用 URL 的机制）已被扩展为通用的文件交互基本机制。这一结果之一是，你几乎可以在任何本地文件路径合适的地方使用 URL。（一些专门方面，如配置设置，除外：例如，你不能在 include 路径中包含 URL。）这包括第三方扩展使用的文件访问函数，PHP 现在将本地文件访问视为通过 `file://` URL 的请求。

另一个结果是，在 PHP5 中，通过所谓的流接口向 PHP 开发者暴露构建自定义流包装器的接口变得可行。

熟悉 Java 或 C++ 的程序员已经熟悉流的概念；出现在 K Desktop Environment 中的 kioslaves 是另一个例子。在 PHP 中，流是一个对象

### 第 3 章

它表现得像一个文件——你可能可以从中读取字节、向其中写入字节、定位到其中的特定字节位置、询问总共有多少字节，等等。注意这里使用了“可能（may be）”一词——正如有些文件是只读的，有些是只写的，流（stream）也可能是只读或只写的；而有些流会实时生成数据，因此并不存在明确定义的“文件偏移量”、“文件大小”甚至“文件结尾”的类比概念。其理念在于，流的使用者无需了解他们所处理的数据是如何存储或处理的；他们只需进行读写操作即可。与 Java 等语言相比，最显著的局限性在于 PHP 的流全部是*字节*流。若要传输其他内容（特别是对象），你需要使用序列化将其转换为能够通过流传输的形式。这再次体现了 PHP 弱类型的特点：既然每个流都是字节流，那么任何流都可以被用于任何地方（无论这在逻辑上是否合理）。

#### 创建和使用流

构建一个流包装器（stream wrapper）很简单，只需向流对象添加特定的方法，并使用 `stream_wrapper_register()` 将其标识为包装器即可。



`stream_wrapper_register()`接受两个参数。第一个参数是*协议*（protocol），它仅仅是一个名称，指示在打开流时将要使用的包装器——在 URL 术语中被称为*方案*（scheme）。它是 URL 中`//`之前的部分，例如 HTTP URL 中的`http`，FTP URL 中的`ftp`，以及文件 URL 中的`file`。例如，如果你实现了一个流并将其注册为协议`foo://`，那么你就可以执行`fopen("foo://.", "r")`来启用从 foonly 流中读取数据。`fopen()`和其他文件系统函数默认使用的协议是`file`，这就是为什么你几乎看不到`file://path/ext`这种写法，因为`path/file.ext`具有相同的效果。

第二个参数是一个字符串，包含实现你的包装器的类名。

当然，完整的包装器方法列表可以在手册中找到。主要的方法如下：

- `stream_open()`：此函数包含新流的启动代码——初始化变量、打开其自身的流等。你调用此函数时传递四个参数。前两个参数与对应的`fopen()`调用中的路径和模式值相同。对于第三方扩展，相应的选项将被计算并提供。）第三个参数可能包含两个标志：`STREAM_USE_PATH`表示如果需要，应该搜索 PHP 的包含路径（include path）以找到指定的文件；`STREAM_REPORT_ERRORS`表示如果流无法打开或发生其他错误，是流本身负责触发错误，还是这些情况将在上层处理（如果是后者，你的流就不应报告任何错误）。`STREAM_USE_PATH`仅在你确实在本地文件系统中查找某物时才相关，无论它是请求的文件还是你的流使用的辅助*文件*。如果你的流是只读的，那么当请求的模式是写入模式（`w`, `r+`, `a`, `a+`）时，它应返回`FALSE`（并可能触发警告），只写流则类似。

> *PHP 手册提到了“fopen_with_path()”，但截至 5.0.3 版本，此函数并不存在。include_path 配置项当然可以通过 ini_get() 获取。*

- `stream_read()`：如果流无法读取，此函数应返回`FALSE`。否则，它应返回不超过请求字节数的数据。作为包装器的作者，你有责任确保在连续调用此方法之间维护任何相关的状态，包括任何文件指针。你允许返回少于请求的字节数（尽管空字符串可能会被解释为指示流的结尾）。

### 更晦涩的 PHP

- `stream_write()`：同样，仅当流实际可写时才应调用此函数。流对象负责跟踪从一次写入到下一次写入之间发生了什么。你不需要写入*所有*传递给你的字节；如果有必要，你可以截断数据。无论如何，此方法应返回*实际*写入的字节数（如果完全无法写入，则包括 0）。这个数字应基于其接收的字节数来衡量。执行 base64 *编码*的流在收到每三个字节时会返回四个字节。如果要求写入 "abc"，它会写入 "YWJJ" 但返回 3。这个返回值是为了调用者的利益，毕竟，从定义上讲，调用者不应该深入了解“调用者”的操作细节。如果你写入的字节少于请求的数量，由调用者决定是否重试，但你的流可能需要保留一些数据。base64 编码器就是这种情况的一个例子：传入 "ab" 后，它能够写入 "YWJ"，但 "b" 的最后两位必须保留，直到流等待下一个输入字节或`stream_close()`。此时，该编码器应返回 1 并期望在下一次`stream_write()`调用中再次传入 "b"。另一种机制是，除非编码器拥有至少三个要编码的字节，否则不输出任何内容，然后它每次只编码（并输出）三个输入字节的倍数。为了让这有效，流需要*声称*它写入了所有传入的字节，即使它*实际上*没有这样做，并希望没有人发现其欺骗行为。否则，调用者可能会因为传入 "ab" 时返回 0 而感到不满并尝试重试，再重试，而此时编码器正等待第三个永远不会看到的字节。

- `stream_eof()`：可以随时询问可读流是否已到达流数据的末尾（特别是在`stream_read()`因某种原因返回空字符串之后）。因此，这只是一个布尔函数，如果已到达流的末尾则返回 "true"。

- `stream_close()`：流对象负责清理任何需要清理的内容，关闭其自身的流，等等。回到 base64 编码器，流留有最后一两个字节且永远不会成为三字节组一部分的可能性超过一半。因此，最终对它们进行编码并写出是安全的，用相应数量的 = 号进行填充。

以上就是打开和关闭流以及读写的基本知识。流包装器还有其他方法，如果适合该协议，则应实现这些方法，涵盖随机访问、目录控制等任务。

当流被打开时，`stream_open()`的第一个参数是*完整*的路径，包括协议。这主要是为了让你可以使用`parse_url()`将路径分解为其组成部分，因此建议在设计你的流名称格式时，在适当的地方使用传统的 URL 语法（scheme://username:password@host:/path?query#fragment）。顺带一提，这也意味着同一个流类可以处理多个协议，但这最好通过子类化处理。

### 流的两个示例

为了巩固上一节中的概念，这里有两个简单的流类。第一个维护一个日志文件，记录通过它访问的文件的活动，而第二个用于从地理航空照片集合中选择部分。

#### 文件访问日志

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
    if(!$this->log_stream)
    {
        if($options&STREAM_REPORT_ERRORS)
        {
            trigger_error('Logged stream: Unable to open log file',
                E_USER_WARNING);
        }
        return false;
    }
    if(!$this->stream)
    {
        if($options&STREAM_REPORT_ERRORS)
        {
            trigger_error('Logged stream: file `'.$path.'` could not be opened',
                E_USER_WARNING);
        }
        return false;
    }
    $binary = strpos($mode, 'b')!==false;
    if($binary)
        $mode = str_replace('b', '', $mode);
    list($micro, $sec) = explode('.', microtime());
    $date = date('Y-m-d H:i:s', substr($micro, 1));
    fwrite($this->log_stream, 'File opened for '.$modes[$mode].
        ($binary?' in binary mode by ': ' ')." by ".$this->user.' at '.$date."\n");
    return true;
}
```

# 第 3 章



```php
function stream_close()
{
    fclose($this->stream);
    list($micro, $sec) = explode(' ', microtime());
    $date = date('Y-m-d H:i:s').substr($micro, 1);
    fwrite($this->log_stream, 'File closed by '.$this->user.' at '.$date."\n");
    fwrite($this->log_stream, "Total bytes read: "."$this->bytes_read."\n");
    fwrite($this->log_stream, "Total bytes written: "."$this->bytes_written."\n");
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
    $this->bytes_read+=strlen($read);
    return $read;
}

function stream_write($data)
{
    $read = fwrite($this->stream, $data);
    $this->bytes_written+=strlen($read);
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
        trigger_error('Logged stream: Unable to open log file. File not deleted.',
            E_USER_WARNING);
        return false;
    }
    $success = unlink($path);
    list($micro, $sec) = explode(' ', microtime());
    $date = date('Y-m-d H:i:s').substr($micro, 1);
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
    $date = date('Y-m-d H:i:s').substr($micro, 1);
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
```

通过调用 `stream_wrapper_register('logged', 'logged_stream')` 可以注册此封装器。你可以通过类似 `$fp = fopen('logged://eric@documents/benchmarks.txt')` 的语句来使用“logged”（已记录）流。这旨在表明用户“eric”将要对 `documents/benchmarks.txt` 进行操作，并且你需要记录这一事件：

```php
$path = substr($path, 9);
$this->user = substr($path, 0, strpos($path, '@'));
$path = substr($path, strpos($path, '@')+1);
```

## 更晦涩的 PHP

流的活跃活动始于 `stream_open()`。前三个 `substr()` 调用切分了 URL 中的 `logged://` 部分，然后是用户名。剩余部分即为实际请求的资源 URL：

```php
$this->stream = fopen($path, $mode, $options=&STREAM_REPORT_ERRORS);
$this->log_stream = fopen($path.'..log', 'a');
```

日志流打开资源本身（关闭 `STREAM_REPORT_ERRORS` 标志，因为这些错误将由当前流处理），并读取一个日志文件以进行追加写入。在此示例中，为了简单起见，资源仅是一个额外的 `.log` 扩展名的流，其名称与请求的名称相同。在更实际的环境中，日志记录会以其他方式进行，因为（首先）这种机制对于只读流会失败，但可以通过编写一个新的流类并在其专用的协议名称下注册来解决此问题。第二个 `fopen()` 调用将使用此协议，之后的任何问题都是新类的问题。

之后，检查这两个流以确保它们确实已打开。如果任一流失败，则触发错误并返回 `FALSE`。

流在返回 true 之前执行的最后一件事是向新打开的日志文件写入一行，说明流已打开、如何打开、由谁打开以及打开时间。

该类的大部分功能仅是将相应的文件操作直接传递给它所记录日志的流。`stream_read()` 和 `stream_write()` 增加了计数来回传输字节的任务，而 `rename()` 则记录文件的新名称（如果它作为已记录流打开，它将拥有自己的日志文件）。

最后，`stream_close()` 在关闭其自身的两个流之前，会写入时间和每个方向传输的总字节数。

### GIS 摄影数据库查询



新西兰土地信息局（[http://www.linz.govt.nz/](http://www.linz.govt.nz/)）维护着该国的 2.5 米分辨率摄影图集。这些航拍照片已经过比例缩放和定向，使其垂直和水平轴分别严格指向南北和东西方向，从而形成所谓的“正射影像”。照片以 8000 × 6000 像素大小的图像形式提供，对应 3.2 × 2.4 平方公里的地面区域。四张这样的照片就足以涵盖奥克兰市。作为单个灰度 PNG 合并时，整个城市的图像大小为 115MB。

现在想象一下在线服务，用户提供奥克兰内某点的纬度和经度，以及一个半径，服务则返回相应的图像。最直接的方法是加载整个城市的图像，并复制相关部分。但由于图像的大小，这是不可行的（请记住，115MB 仅指其压缩为 PNG 文件时的大小：解压后，1.92 亿个像素大约每个占一个字节）。

另一种方法是将图像存储为未压缩形式（LINZ 提供未压缩的 TIFF 文件图像），并编写一个程序，可以从一个或多个文件中仅定位和读取相关字节（对于一个城市是 1.92 亿字节，但对于整个国家则多得多，因此需要存储大量原始数据以便随时访问），而不必将全部数据加载到内存中。这当然是两个选项中更好的一个，但它并不适合 PHP，主要是在读取字节并组装最终图像时的速度考虑。用 C 编写的自定义扩展程序将更合适。既然当前的讨论着眼于 PHP 的流封装器接口，这种解决方案就不会特别具有启发性。

第三种解决方案由第二种方案所暗示。未压缩的图像可以存储在多个随机访问文件中。但如果文件足够小，就有可能考虑以压缩形式存储它们，并在需要时整体加载。那么，问题仅仅是确定哪些文件满足给定请求，并将它们拼接以生成所需的图像。这就是以下流封装器实现的方法：

```php
/**
 * The orthophoto stream uses the Orthophoto dataset maintained by
 * Land Information New Zealand. The phototest follows the Topographic
 * Map 260 series; coordinates used are those of the New Zealand
 * Map Grid (NZMG), a system unique to that country.
 *
 * Aerial photos have a resolution of 2.5m per pixel, with an
 * accuracy of +/-2.5m.
 */
class orthophoto_stream
{
    // This is the generated PNG data that will be fed
    // back by the stream.
    private $png_data;

    // For the ftell() function / stream_tell() method.
    private $data_length;

    function stream_open($path, $mode, $options, & $opened_path)
    {
        // This is a read-only stream
        if (preg_match('/\\w\\/', $options)) return false;
        $path = parse_url($path);
        $coordinates = $path['host']; // Silly place to find it, but see
        // the note at the end of the section.
        if (strlen($coordinates) != 21) return false;
        if (strpos($coordinates, '0123456789') != 21) return false;
        list($northing, $easting, $radius) = sscanf($coordinates, '%0?d%0?d%0?d');
        $full_image_size = ceil($radius * 2 * 100 / 250);

        $full_image = imagecreate($full_image_size, $full_image_size);
        $black = imagecolorallocate($full_image, 0, 0, 0);
        // We use black as a background for unmapped regions.
        imagefill($full_image, 0, 0, $black);

        $maximum_northing = $northing + $radius;
        $minimum_northing = $northing - $radius;
        $maximum_easting = $easting + $radius;
        $minimum_easting = $easting - $radius;
        $bottommost_tile_northing = floor($minimum_northing / 250) * 250;
        $topmost_tile_northing = ceil($maximum_northing / 250) * 250;
        $leftmost_tile_easting = floor($minimum_easting / 250) * 250;
        $rightmost_tile_easting = ceil($maximum_easting / 250) * 250;

        for ($tile_northing = $bottommost_tile_northing;
             $tile_northing <= $topmost_tile_northing;
```

# 更冷门的 PHP



```php
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
imagecopy($full_image, $tile, $full_image_x, $full_image_y, 0, 0, 100, 100);
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
$return = substr($this->png_data, 0, $bytes);
$this->png_data = substr($this->png_data, $bytes);
return $return;
}

function stream_write(){}
function stream_eof()
{
return $this->png_data == 0;
}

function stream_tell()
{
return $this->data_length-strlen($this->png_data);
}

function stream_seek()
{
return false;
}

function stream_flush(){
    return false; // We don't store data, silly.
}

function stream_stat() 
{ 
    return false; 
} 

// We put the stream wrapper registration here, with the wrapper it 
// registers, to save the hassle of remembering to register it every 
// time we include the file. 
// 
// This of course assumes that we're never tempted to use the same 
// wrapper protocol (nzmg) for different types of stream. 
stream_wrapper_register('nzmg', 'orthophoto_stream');
```

# 第 3 章

正如代码最后一行所示，该类被注册为“`nzmg`”协议。此处实现的 `nzmg` URL 的完整格式为 `nzmg:///nnnnnnneeeeeeeerrrrrrr`，其中七位数字分别指定北向坐标（对于奥克兰而言，是 6460000 到 6489750 之间的某个米数）、东向坐标（2650000 到 2689750 之间的米数）以及半径（同样以米为单位，虽然要求超过 20000 米的半径几乎没有意义，因为那是整个 16 × 12 公里图像的斜边长度）。

之所以使用“北向坐标”和“东向坐标”而不是经纬度来表示位置，是因为地球既不是一个完美的球体，甚至也不是一个特别对称的椭球体，因此二者之间的转换绝非易事。本示例中采用的新西兰地图网格（New Zealand Map Grid）是通过经验确定的，由此产生的经纬度与北向/东向坐标的映射涉及诸如求值六度复杂多项式等操作。（土地测量官办公室发布的精确规范可作为 OGS 技术报告 4.1 获取，并可在 LINZ 网站上下载。）这与本示例的目标无关，就像将地标和投递地址映射到坐标这一练习一样无关。同样，输入数据验证的问题（包括将半径限制在比 20 公里更合理的范围内）也与此无关。所有此类具体任务都应在达到此阶段之前处理，每一项都应尽可能具有广泛的适用性。

图像存储为一系列 PNG 文件，每个文件尺寸为 100 × 100 像素，对应现实世界中的 250 × 250 米，因此总共有 19,200 个这样的文件。每个文件的命名根据其西南角（左下角）的北向坐标和东向坐标。北向坐标向上增加，东向坐标向右增加。由于北向坐标和东向坐标本身以米为单位测量（这就是它们的用途），位于 `647000202660000.png` 正北方的瓦片将是 `64702502660000.png`，而位于正东方的瓦片将是 `6470002660250.png`。这些瓦片的位置安排使得它们已知的北向坐标和东向坐标都是 250 的倍数。由于父图像也具有此属性，且其尺寸也是 100 像素的倍数，因此这些瓦片精确覆盖了父图像。

同样，大部分工作都在 `stream_open()` 中完成，它确定请求图像的大小、其左下角像素所在的瓦片，以及垂直和水平方向需要的瓦片数量。使用 GD 库创建一个新图像（由于图像是灰度的，因此没有必要使用 truetype），尺寸为此处所需的尺寸，然后通过一对嵌套循环从磁盘读取适当的瓦片，并将它们复制到正在进行的图像中。在任何时间点，用于存储图像数据的总内存量足以容纳进行中的图像和一个 100 × 100 像素的瓦片。

`stream_open()` 的最后一步是将组装好的 GD 库图像转换为 PNG 数据。这是通过一种简单的方法实现的：要求 GD 库将图像输出为 PNG，并使用输出缓冲来捕获结果。

每次调用 `stream_read()` 都会返回另一块 PNG 数据，并丢弃已经返回的部分。

由于这是一个由实时生成数据组成的只读流，因此剩余的大部分流访问方法都没有意义。关于数据可以说的一点是还剩多少可读内容，这使得可以定义 `stream_tell()`。

使用该类的代码无需了解它是如何将 `nmgz://` 请求与响应匹配的。就它关心的而言，`nmgz://648208926677120000500` 只是另一个文件，恰好包含奥克兰中心区 1 公里宽快照的 PNG 图像。

但请等一下。如果它只是 PNG 数据，而且只是一个文件，那么从各方面来看，*它只是一个 PNG 文件*。确实如此。下面是使用此封装器的一个示例。假设该类位于其自己的 `orthophoto_stream.php` 文件中，并且假设经纬度已转换为北向坐标和东向坐标，并且半径不会太大或太小。



```php
include_once('orthophoto_stream.php'); // 当然，在使用之前必须声明该类。
function display_orthophoto($northing, $seasting, $radius)
{
  $filename = sprintf('nmgz://%07d%07d', $northing, $seasting, $radius);

  // 所有基于流的操作都在这里发生。
  $image = imagecreatefrompng($filename);

  // 一点后处理，以使代码超越琐碎。
  // 绘制一个指定半径的圆（图像毕竟是方形的），并在中心放置一个十字。
  // 我们需要找到图像的白色值
  $white = imagecolorsearch($image, 255, 255, 255);
  if($white==-1) // 好的，它之前不存在。
    $white = imagecolorallocate($image, 255, 255, 255);
  // 圆以图像中心为圆心，且大小刚好足以
  // 触及边缘。
  $imagesize = imageX($image);
  $middle = $imagesize>>1;
  imageellipse($image, $middle, $middle, $imagesize, $imagesize, $white);
  imageline($image, $middle, $middle+5, $middle, $middle-5, $white);
  imageline($image, $middle+5, $middle, $middle-5, $middle, $white);
  imagestring($image, 0, 0, 0, 0,
              'Sourced from Orthophoto R11 Auckland Crown Copyright Reserved.',
              $white);
  imagepng($image);
  imagedestroy($image);
}
```

不用说，这个示例是在实际用途和教学用途之间达成的妥协，`orthophoto_stream`类在很多方面都有改进的空间。

其中一个方面是，提供的21位数字文件名可以附加一个扩展名来指示所需的图像格式，而不是固定生成PNG。其他方面包括更现实（或至少更灵活）的存储机制，用户可以通过更完善的URL（包括主机名和路径）来控制。还要考虑将部分耗时工作移至`stream_read()`中的可能性，从而减少任何给定时间需要保留的图像数据量。（但请注意，由于GD库只缓冲完整图像，你将需要编写自己的代码来输出图像数据，这些数据在等待未来输入以完成之前是正确但不完整的。）

如果你遵循`RFC 3986`中定义的流资源命名URL系统，并参考`RFC 2718`中的指南，你会对自己很有帮助。事实上，可能已经存在一个与你应用程序相匹配的命名方案。（官方注册表由互联网号码分配机构维护，位于`http://www.iana.org/assignments/uri-schemes`）。如果存在，请使用它。这样，你的应用程序将来可以与使用相同方案的其他应用程序协作，而无需额外的URL转换层将它们粘合在一起。（实际上，对于任何数据格式或通信协议也是如此——如果世界其他地方已经拥有你想要的标准，就使用它，节省自己创建新标准的时间和精力。）

> 请注意，所有PHP URL都要求在协议名称后使用`://`，无论是否涉及命名权威（主机），因为PHP使用该字符序列来区分URL和本地文件路径。用`RFC 3986`的术语来说，PHP仅实现“hier-part”组件给出的四个产生式中的第一个，并将“naming-authority”组件设为可选。符合RFC的变通方法是使用`:///`，隐含指定本地主机作为命名权威。

#### 总结

这是对PHP原生函数集中一些较为冷门区域的简要介绍。通过利用这些功能，你的代码可以在不牺牲可读性的情况下变得更加紧凑和可靠。数组函数通常可以替代有时复杂的循环，将任务简化为一行代码和一个可以捕获并存储在库中以便重用的辅助函数。函数处理函数允许你在运行时不仅决定你想使用哪个函数（`switch`语句可以做到这一点），还可以决定你希望从这个列表中选择的函数，甚至从头创建函数。流允许你隐藏外部数据读取或写入的实现细节，允许程序的其余部分将其视为另一个文件。

PHP始终在添加新功能——用于微调其操作的新的初始化设置、增强现有功能实用性的新参数（即使是久负盛名的函数`str_replace()`在PHP5中也被赋予了新参数）、新函数，甚至全新的函数类别。所有这些使得学习PHP成为一项持续的过程，总有一些你尚未了解的东西。

## 4 高级 MySQL

大多数动态网站的关键要素之一是为其提供数据的数据库。无论是简单的新闻页面，还是复杂的发布系统或CMS，数据库在站点内容管理中都发挥着核心作用。为了让站点平稳运行，了解一些数据库系统的技巧和窍门非常有帮助。在本章中，你将学习如何创建数据库，管理访问系统的各种用户账户，以及如何组合和优化SQL代码以执行复杂和精细的查询。

## 基础知识回顾

在深入研究高级功能之前，我们先快速回顾一下MySQL的用法。假设你刚接到一个新客户，一家汽车经销商。经销商的经理希望你创建一个网站，帮助他们跟踪汽车库存。没问题，你说着便坐下来开始规划他们的Web应用程序。

在规划过程中，你设计了一个简单的多表数据库方案，用于存储他们的汽车场地数据。为了便于练习，你决定创建类似图4.1的数据库表。

你创建了一个非常简单的数据库结构，涉及两个表。在`New_Vehicles`表中，显然存储的是新车的数据。可以为库存中的每辆车指定里程、价格、颜色和描述等属性。`Used_Vehicles`表的结构与`New_Vehicles`几乎相同，但旨在存储二手车（正如你可能猜到的那样）的记录。`Used_Vehicles`表还有几个额外的列，用于指示车辆是否经过认证或拥有保修，以及一个里程列。最后两个表，`Make`和`Model`，存储经销商销售的各种品牌的通用制造商和型号名称。

![](img/fd2e7361878181c2b12e30301ff3e182_99_0.png)

### 创建数据库

你需要做的第一件事是在MySQL中创建数据库和表。首先启动命令行中的MySQL客户端，或者如果你有其他更熟悉的程序，可以直接输入MySQL命令，不妨使用那个。

```
shell$ mysql
```

这将打开MySQL监视器，其外观应类似于以下内容（如果你使用的是命令行客户端）：

> 欢迎使用MySQL监视器。命令以`;`或`\g`结尾。
> 
> 你的MySQL连接id为2，服务器版本：4.1.11-log
> 
> 
> 
> 输入`'help;'`或`'\h'`获取帮助。输入`'\c'`清除当前缓冲区。
> 
> mysql>

在许多情况下，你需要使用登录名和密码来访问MySQL客户端。为此，只需在`mysql`命令末尾添加`-u username -p`，MySQL就会提示你输入密码，如下所示：

```
shell$ mysql -u username -p
```

使用MySQL命令行客户端是熟悉MySQL大多数命令和功能的好方法，这些功能在图形界面客户端中通常会被自动化处理。

输入以下命令来创建数据库，并将其命名为“VehicleInventory”：

```
mysql> CREATE DATABASE VehicleInventory;
```

既然你已经创建了数据库，就需要将其设置为后续查询的活动数据库：

```
mysql> USE VehicleInventory;
```

接下来，为你的数据库创建表。在MySQL中创建表的基本SQL语句如下：

```
CREATE TABLE tablename (column_definitions);
```

要创建四个车辆信息表，可以使用以下内容：



```
mysql> CREATE TABLE Makes (make_id int PRIMARY KEY AUTO_INCREMENT, make_name varchar(100) );
mysql> CREATE TABLE Models (model_id int PRIMARY KEY AUTO_INCREMENT, model_name varchar(200), make_id int );
mysql> CREATE TABLE New_Vehicles (vehicle_id int PRIMARY KEY AUTO_INCREMENT, model_id int, modelyear int, price decimal(10,2), color varchar(200), description text );
mysql> CREATE TABLE Used_Vehicles (vehicle_id int PRIMARY KEY AUTO_INCREMENT, model_id int, modelyear int, mileage int, price decimal(10,2), color varchar(200), certified tinyint, warranty tinyint, description text );
```

简而言之，我们只需使用 MySQL 的 `CREATE TABLE` 命令，后面跟着表名，然后在括号中列出列名和类型。你还会注意到每个表都添加了一个自动递增的主键，以便在添加行后帮助你唯一地标识这些行。

### 添加信息

既然你已经创建了表，就需要向其中添加一些数据。为此，你将使用 `INSERT` 语句。MySQL 的 `INSERT` 命令通常遵循以下格式：

```
INSERT INTO tablename (column_list) VALUES (new_values);
```

首先，向 `Makes` 表添加一些初始数据：

```
INSERT INTO Makes (make_id, make_name) VALUES (1, 'Ford'), (2, 'Honda'), (3, 'Volkswagen'), (4, 'Toyota'), (5, 'Chevrolet');
```

这里使用了基本的 SQL `INSERT` 语法，但增加了一点变化。在 MySQL 中，你可以指定一组以逗号分隔的列值，而不是仅一组值，以便一次填充多行。通常，在向 `Makes` 表插入数据时，你可能会省略 `make_id` 列——自动递增的 ID 会自动为它们分配数字。在这种情况下，你指定了 ID，以便稍后添加到其他表的行具有有效的外键。

使用以下内容向其余表添加数据（记住，你可以从 `www.wrox.com` 下载此代码，如果你想节省打字功夫的话）：

```
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
(4, 1993, 'Red', 152000, 0, 0, 'Runs decent; 4WD; Tinted windows, aftermarket stereo; Needs a little TLC.'
)
```

请注意，你添加到 `New_Vehicles` 表中的第二辆车的 `model_id` 值为 `NULL`。稍后你会明白原因。

### 检索信息

你花了那么多时间创建数据库表并填充数据；现在是时候把一些数据取回来了。为此，你将使用 `SELECT` 语句。`SELECT` 的简化形式看起来像这样：

```
SELECT [column_names] FROM [table] WHERE [criteria]
```

例如，如果你想检索二手车颜色的列表，可以使用类似以下内容：

```
SELECT color FROM Used_Vehicles
```

这将返回以下内容：

| color        |

|--------------|

| White        |

| Deep Green Pearl |

| Reflex Silver |

| Red          |

或者，也许你想要列出 2001 年款之前所有汽车的里程数：

```
SELECT mileage, modelyear FROM Used_Vehicles WHERE modelyear < 2001;
```

运行此查询显示以下内容：

| mileage | modelyear |

| :--- | :--- |

| 64800 | 2000 |

| 152000 | 1993 |

很简单，但如果你发现错误，并想要更改现有记录怎么办？

### 更新信息

要更新信息，你使用 `UPDATE` 语句。`UPDATE` 语句的通用形式如下：

```
UPDATE [table] SET [column]=[value] WHERE [criteria]
```

回到车辆库存示例，假设有一天，汽车场地的经理在查看库存时，发现其中一辆车的里程记录有误。为了将其更改为正确值，你可能会使用以下查询：

```
UPDATE Used_Vehicles SET mileage=66000 WHERE vehicle_id=1;
```

在这种情况下，车辆 ID 1 对应于之前 `INSERT` 语句中添加的二手福特探险者（Ford Explorer）自动递增分配的 ID。

### 删除信息

假设的汽车场地销售开始增长，一些最近的销售额需要从数据库中移除一些车辆。在这种情况下，你将使用 `DELETE` 语句：

```
DELETE FROM [table] WHERE [criteria];
```

那辆里程记录有误的二手福特探险者今天卖掉了。要将其从 `Used_Vehicles` 表中移除，你只需执行以下操作：

```
DELETE FROM Used_Vehicles WHERE vehicle_id=1;
```

这应该涵盖了 MySQL 使用的基础知识，是时候进入更强大的查询了。

### 多表查询

你已经建立了车辆库存，可以使用基础知识对单个表执行简单查询。但你希望看到更多——甚至是一个将每辆车的制造商和型号与其单独记录关联起来的查询。为此，你将使用 `连接`（joins）。

#### 内连接

在 SQL 中，连接（join）是通过指定的一列或多列将两个或更多表关联起来的方式。在 MySQL 中，最常使用的两种连接类型是内连接和外连接。



# 内连接

内连接是一种将两个表基于每行共同共享的值进行组合的方法。当你在 `SELECT` 查询中执行内连接时，只需在 `FROM` 子句中指定要连接的表，并提供提示说明它们有哪些共同列。MySQL `INNER JOIN` 语法的通用抽象形式如下：

```
SELECT [column_names] FROM [table1] INNER JOIN [table2] ON [table1.column] = [table2.column]
```

## 示例场景

使用假设的汽车经销商库存场景，你希望每个车辆的具体信息旁边都能返回该车辆型号。为了实现这一点，你的查询大致如下：

```
SELECT Models.model_name, New_Vehicles.color, New_Vehicles.modelyear FROM Models INNER JOIN New_Vehicles ON Models.model_id = New_Vehicles.model_id;
```

对数据库运行此查询将产生以下结果：

| model_name | color | modelyear |
| :--- | :--- | :--- |
| Explorer | 深蓝色 | 2005 |
| Tacoma | 亮红色 | 2005 |
| Corvette | 戴通纳日落橙色 | 2005 |

你会注意到，在 `SELECT` 查询中，选择列表中的每个列都带有其所属表的名称前缀。虽然这在技术上不是必需的，但这是一个避免同名列之间冲突的好习惯。如果你存在这样的冲突并且忽略了表前缀，会发生什么？请看这个例子：

```
SELECT model_id, model_name, color, modelyear FROM Models INNER JOIN New_Vehicles ON Models.model_id = New_Vehicles.model_id;
```

如你所见，表前缀已被移除，但 `model_id` 列也被添加到了列表中（因为它在两个表中都存在）。现在尝试运行该查询。你会得到以下错误：

```
ERROR 1052 (23000): Column 'model_id' in field list is ambiguous
```

当你尝试使用在两个表中都存在的列名，而没有使用表前缀时，执行该查询时会抛出此类错误。

## 使用表别名

如果你更喜欢简洁的 SQL 查询，别担心——有一种简单的方法可以缩短所有这些表前缀。在 `FROM` 子句中，你可以为调用的每个表指定一个 `别名`，如下所示：

```
SELECT [column_names] FROM [table1] alias1 INNER JOIN [table2] alias2 ON [alias1.column] = [alias2.column]
```

由于表别名可以短至单个字符，你可以大幅缩短库存查询：

```
SELECT m.model_name, n.color, n.modelyear FROM Models m INNER JOIN New_Vehicles n ON m.model_id = n.model_id;
```

## 使用 USING 语句

还不够简短？好吧，还有另一种整理连接的方法。MySQL 提供了 `USING` 语句，用于替代 `ON` 语句来链接你的表。当两个连接列恰好拥有完全相同的列名时，使用 `USING` 语句。带有 `USING` 的内连接通用形式如下：

```
SELECT [column names] FROM [table1] INNER JOIN [table2] USING (column list)
```

由于 `New_Vehicles` 表和 `Models` 表都有一个 `model_id` 列，你可以在连接中使用 `USING` 语句：

```
SELECT m.model_name, n.color, n.modelyear FROM Models m INNER JOIN New_Vehicles n USING (model_id);
```

## 多表连接

在某些情况下，你需要在查询中连接两个以上的表。MySQL 可以轻松地处理这一点——你只需要按照希望评估的顺序将连接链接在一起。在车辆库存数据库中，你需要使用多个连接来返回每辆车的制造商及其记录，如下所示：

```
SELECT ma.make_name, mo.model_name, n.color, n.modelyear FROM Makes ma INNER JOIN Models mo USING (make_id) INNER JOIN New_Vehicles n USING (model_id);
```

当你运行此查询时，应该看到以下内容：

| make_name | model_name | color | modelyear |
| :--- | :--- | :--- | :--- |
| Ford | Explorer | 深蓝色 | 2005 |
| Toyota | Tacoma | 亮红色 | 2005 |
| Chevrolet | Corvette | 戴通纳日落橙色金属漆 | 2005 |

如你所见，`Makes` 表基于 `make_id` 连接到 `Models` 表，然后该连接的结果再与 `New_Vehicles` 表连接，从而在一个查询中提供制造商、型号和车辆信息。

## 隐式内连接

在继续下一组连接之前，你应该知道还有另一种执行内连接的方法。第二种方法只是在逗号分隔的列表中指定多个表，并使用 `WHERE` 语句来指定表如何关联。这种类型内连接的通用形式如下：

```
SELECT [column names] FROM table1, table2 WHERE table1.column = table2.column
```

如果你使用这种内连接形式来上一个查询中提取新车、制造商和型号的列表，它会看起来像这样：

```
SELECT ma.make_name, mo.model_name, n.color, n.modelyear FROM Makes ma, Models mo, New_Vehicles n WHERE ma.make_id = mo.make_id AND mo.model_id = n.model_id;
```

在你的 MySQL 客户端中执行此查询，将返回以下内容：

| make_name | model_name | color | modelyear |
| :--- | :--- | :--- | :--- |
| Ford | Explorer | 深蓝色 | 2005 |
| Toyota | Tacoma | 亮红色 | 2005 |
| Chevrolet | Corvette | 戴通纳日落橙色金属漆 | 2005 |

如你所见，返回了与使用显式内连接时完全相同的结果。如果你省略了 `WHERE` 子句中的项目会发生什么？试试这个查询：

```
SELECT mo.model_name, n.color, n.modelyear FROM Models mo, New_Vehicles n;
```

对我们的车辆库存运行此查询会产生以下结果（注意 `Makes` 表已被排除）：

| model_name | color | modelyear |
| :--- | :--- | :--- |
| Accord | 深蓝色 | 2005 |
| Golf | 深蓝色 | 2005 |
| Tacoma | 深蓝色 | 2005 |
| Corvette | 深蓝色 | 2005 |
| Explorer | 深蓝色 | 2005 |
| Accord | 石墨珍珠色 | 2004 |
| Golf | 石墨珍珠色 | 2004 |
| Tacoma | 石墨珍珠色 | 2004 |
| Corvette | 石墨珍珠色 | 2004 |
| Explorer | 石墨珍珠色 | 2004 |
| Accord | 亮红色 | 2005 |
| Golf | 亮红色 | 2005 |
| Tacoma | 亮红色 | 2005 |
| Corvette | 亮红色 | 2005 |
| Explorer | 亮红色 | 2005 |
| Accord | 戴通纳日落橙色金属漆 | 2005 |
| Golf | 戴通纳日落橙色金属漆 | 2005 |
| Tacoma | 戴通纳日落橙色金属漆 | 2005 |
| Corvette | 戴通纳日落橙色金属漆 | 2005 |
| Explorer | 戴通纳日落橙色金属漆 | 2005 |
| Accord | 深蓝色 | 2005 |
| Golf | 深蓝色 | 2005 |
| Tacoma | 深蓝色 | 2005 |
| Corvette | 深蓝色 | 2005 |
| Explorer | 深蓝色 | 2005 |



这不太正确。在这种情况下实际发生的是另一种称为`交叉连接`（`cross join`）的连接。`交叉连接`仅仅是每个表中每个匹配结果的组合。在这种情况下，`Models`表中有五个型号，因此这些行中的每一行都与`New_Vehicles`表中的`每一行`进行了匹配。这发生仅仅是因为你省略了`WHERE`语句，而该语句提供了关于如何链接记录的提示给`MySQL`。如前所述，你没有让`Makes`表参与此查询——如果参与了，由于你的数据库中有五个不同的制造商，结果行数将是原来的五倍。

### 外连接

虽然大多数复杂的链接可以使用内连接实现，但在某些情况下它们会受到限制。如果数据库行没有为被链接的列定义值，它将被内连接忽略。在车辆库存示例中，每次你使用内连接链接`Models`表时，只返回了三行。`New_Vehicles`表中的第四辆车被忽略，因为其`model_id`的值为`null`。你需要一种方法，无论是否指定了`model_id`，都返回所有行；如果指定了`model_id`，则执行请求的连接。对于这种任务，`MySQL`提供了`外连接`（`outer joins`）。

`MySQL`中有两种主要类型的外连接：左外连接和右外连接。它们的行为完全相同，唯一的不同在于允许哪个表不包含匹配项。外连接的通用形式与内连接非常相似。看这个简化的左外连接版本：

```
SELECT [column names] FROM table1 LEFT OUTER JOIN table2 USING [column list]
```

左外连接使用通用列名将“右”表（`table2`）与“左”表（`table1`）进行匹配，但如果“左”表包含“右”列中没有匹配项的值，它仍将返回行。右外连接的行为相同，但两个表的角色互换（允许在右表中存在不匹配的值）。

在车辆库存示例中，如果你想返回一组行，其中所有新车都返回，无论其`model_id`如何，你可能使用以下代码：

```
SELECT mo.model_name, n.color, n.modelyear FROM New_Vehicles n LEFT OUTER JOIN Models mo USING (model_id);
```

使用此查询查询车辆库存数据库将产生以下结果：

| model_name | color | modelyear |
| :--- | :--- | :--- |
| Explorer | 深蓝色 | 2005 |
| NULL | 石墨珍珠色 | 2004 |
| Tacoma | 亮红色 | 2005 |
| Corvette | 戴通纳日落橙色金属漆 | 2005 |
| Explorer | 深蓝色 | 2005 |

这与你之前查看的内连接查询之一非常相似，但增加了第二行——2004 年款的石墨珍珠色。因为在`Models`表中没有匹配项，`MySQL`为无法确定的行值返回`NULL`——在这种情况下，是`model_name`。

## 第 4 章

然而，外连接和内连接并不一定需要相互隔离。可以将两者结合在单个查询中，从而生成强大的多表连接，这些连接对要求所有行都必须匹配所有数据的要求较为宽松。为了获取新车颜色、品牌、型号和年份的列表（包括那些未指定型号的车辆），请执行类似的查询：

```
SELECT ma.make_name, mo.model_name, n.color, n.modelyear FROM New_Vehicles n LEFT OUTER JOIN Models mo USING (model_id) LEFT OUTER JOIN Makes ma USING (make_id);
```

针对车辆库存数据库运行此查询后，将返回以下内容：

| make_name | model_name | color | modelyear |
| --- | --- | --- | --- |
| Ford | Explorer | Dark Blue | 2005 |
| NULL | NULL | Graphite Pearl | 2004 |
| Toyota | Tacoma | Radiant Red | 2005 |
| Chevrolet | Corvette | Daytona Sunset Orange Metallic | 2005 |
| Ford | Explorer | Dark Blue | 2005 |

请注意，在这个查询中，表连接的顺序很重要。第一个连接产生的结果表在对第三个表进行连接时，将用作内部临时表。

### 联合查询

到目前为止，你在车辆库存数据库上执行的查询仅返回一种类型车辆的记录，即新车或二手车。如果你想要获取数据库中所有车辆的列表，无论其之前的所有权状态如何，该怎么办？起初，你可能会认为只需将两个表都添加到查询中即可；但这会导致交叉连接——这显然不是你所寻求的结果。对于这种情况，你需要使用联合查询。

`MySQL`中的联合查询是一种将多个表作为单个记录集返回的方法，而不将它们合并。联合查询类似于`PHP`中的连接（`concatenation`）——它们只是将额外的行附加到第一个表的末尾。`MySQL`中联合查询的通用形式如下：

```
(SELECT [column_names] FROM [table1]) UNION (SELECT [column_names] FROM [table2])
```

简而言之，联合查询是通过使用关键字`UNION`将两个独立的`SELECT`语句连接在一起来实现的。在代码抽象中，括号放在每个`SELECT`语句周围。虽然不是必须的，但为了更好地在视觉上区分这两个查询，这通常是个好主意。

假设你想返回车辆库存中所有车辆的列表，无论它们是新车还是二手车。使用类似于以下查询的方法：

```
(SELECT color, modelyear, model_id FROM New_Vehicles) UNION (SELECT color, modelyear, model_id FROM Used_Vehicles);
```

如果在`MySQL`中运行此查询，你应该会看到以下内容：

```
+-----------------------------+----------+----------+
| color                       | modelyear | model_id |
+-----------------------------+----------+----------+
| Dark Blue                   | 2005     | 1        |
| Graphite Pearl              | 2004     | NULL     |
| Radiant Red                 | 2005     | 4        |
| Daytona Sunset Orange Metallic | 2005  | 5        |
| Deep Green Pearl            | 2003     | 2        |
| Reflex Silver               | 2004     | 3        |
| Red                         | 1993     | 4        |
+-----------------------------+----------+----------+
```

请注意，该查询明确指定了要从每个表返回哪些列，并且列表中的列数必须在各表之间匹配。如果你对每个表选择不同数量的列会发生什么？看看这个查询，它将选择每个表中的所有记录（`Used_Vehicle`表比`New_Vehicles`表有更多的列）：

```
(SELECT * FROM New_Vehicles) UNION (SELECT * FROM Used_Vehicles);
```

尝试在数据库上运行此查询，它将返回以下内容：

```
ERROR 1222 (21000): The used SELECT statements have a different number of columns
```

`MySQL`迅速返回一个错误，告诉你你的列列表长度不同。列表中的列的任何组合都是有效的，只要每个列表中的列数相同即可。如果在列列表的对应位置有名称不同的列，`MySQL`在返回行时将使用第一个列表中的列名。看看以下查询：

```
(SELECT color FROM New_Vehicles) UNION (SELECT modelyear FROM Used_Vehicles);
```

当查询数据库时，它将显示以下内容：



```
+-------------------------------+
| color                         |
+-------------------------------+
| Dark Blue                     |
| Graphite Pearl                |
| Radiant Red                   |
| Daytona Sunset Orange Metallic |
| 2003                          |
| 2004                          |
| 1993                          |
+-------------------------------+
```

正如预期的那样，MySQL 使用了第一个列列表中的 `color` 列名。然而，这个例子说明了未来可能出现的一个混淆点。表中 `color` 列的类型被设置为 `varchar`，而 `modelyear` 列的类型是 `int`。在对这两个表执行联合查询时，MySQL 忽略了列类型，并愉快地合并了这两个表。这在大多数情况下可能并不一定有问题，但如果你正在 MySQL 之外强制执行引用完整性（比如在 `PHP` 中），那么如果外部代码期望特定类型的返回数据，而 MySQL 发送了像这样的混合结果，可能会发生冲突。

虽然所有车辆颜色和车型年份的简单列表不错，但车行老板对你期望更多。除了返回颜色和车型年份外，你还需要提供品牌和型号。你高兴地在新联合表中添加了必要的连接，使用的查询可能如下所示：

```
SELECT color, modelyear, model_id FROM New_Vehicles) UNION (SELECT color, modelyear, model_id FROM Used_Vehicles) LEFT OUTER JOIN Models USING (model_id) LEFT OUTER JOIN Makes USING (make_id);
```

你以为看起来不错，直到你在 MySQL 上运行它并得到以下结果：

```
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near ‘LEFT OUTER JOIN Models USING (model_id) LEFT OUTER JOIN Makes USING (make_id)’ at line 1
```

发生了什么？`UNION` 操作本身并不等同于来自表的正常结果集，因此你无法简单地附加必要的连接来查找额外信息。此外，你没有指定在任何地方返回 `make_name` 或 `model_name`。解决方案：你需要将所有的连接和额外的返回列添加到组成 `UNION` 的每个 `SELECT` 语句中。

```
(SELECT ma.make_name, mo.model_name, n.color, n.modelyear FROM New_Vehicles n LEFT OUTER JOIN Models mo USING (model_id) LEFT OUTER JOIN Makes ma USING (make_id)) UNION (SELECT ma.make_name, mo.model_name, u.color, u.modelyear FROM Used_Vehicles u LEFT OUTER JOIN Models mo USING (model_id) LEFT OUTER JOIN Makes ma USING (make_id));
```

在 MySQL 中运行这个相当大的查询，你将看到以下内容：

| make_name | model_name | color | modelyear |
| --- | --- | --- | --- |
| Ford | Explorer | Dark Blue | 2005 |
| NULL | NULL | Graphite Pearl | 2004 |
| Toyota | Tacoma | Radiant Red | 2005 |
| Chevrolet | Corvette | Daytona Sunset Orange Metallic | 2005 |
| Honda | Accord | Deep Green Pearl | 2003 |
| Volkswagen | Golf | Reflex Silver | 2004 |
| Toyota | Tacoma | Red | 1993 |

最终你得到的是车行中所有车辆的简洁列表，包括其品牌、型号、颜色和车型年份。你将此功能实现到你的库存应用程序中，并将其发送给经销商以获得批准，但你还没完。和许多客户一样，经销商老板善变，并且再次改变了他对车辆列表中需要哪些字段的看法。这次，你需要返回数据库中所有车辆的所有信息。你已经知道 `New_Vehicles` 表和 `Used_Vehicles` 表具有不同数量的列，那么 `UNION` 将如何起作用？实际上，答案相当简单。你只需要为对应表中缺失的任何列指定 `NULL`（或你喜欢的任何其他值），如下所示：

```
(SELECT ma.make_name, mo.model_name, n.color, n.modelyear, n.price, n.description, NULL, 1 FROM New_Vehicles n LEFT OUTER JOIN Models mo USING (model_id) LEFT OUTER JOIN Makes ma USING (make_id)) UNION (SELECT ma.make_name, mo.model_name, u.color, u.modelyear, u.price, u.description, u.certified, u.warranty FROM Used_Vehicles u
```

`LEFT OUTER JOIN` 车型表 `mo` `USING (model_id)` `LEFT OUTER JOIN` 制造商表 `ma` `USING (make_id)` `\G`

运行此命令后，你将看到以下内容：



你首先会注意到的是，结果看起来与之前的结果略有不同。这是因为查询末尾使用了 `\G` 终止符，它使 MySQL 以垂直方式显示结果（否则，表格对这本书来说太宽了）。除此之外，所有信息都存在且准确无误。在 `New_Vehicles` 表中为缺失的 `certified` 列指定的 `NULL` 值存在，以及你指定的占位值 `1` 也存在，因为所有新车都有保修。你将这些更改发送回客户端，他们对此感到满意（至少暂时是这样）。

```
*************************** 1. 行 ***************************
make_name: Ford
model_name: Explorer
color: Dark Blue
modelyear: 2005
price: NULL
description: Popular SUV; great for moving people or cargo across town, or wherever your adventures may take you.
NULL: NULL
1: 1
*************************** 2. 行 ***************************
make_name: NULL
model_name: NULL
color: Graphite Pearl
modelyear: 2004
price: NULL
description: Last of the 2004 stock! Must sell! Loaded, all options!
NULL: NULL
1: 1
*************************** 3. 行 ***************************
make_name: Toyota
model_name: Tacoma
color: Radiant Red
modelyear: 2005
price: NULL
description: Come drive this terrific truck! 4WD, extended cab, many options.
NULL: NULL
1: 1
*************************** 4. 行 ***************************
make_name: Chevrolet
model_name: Corvette
color: Daytona Sunset Orange Metallic
modelyear: 2005
price: NULL
description: The all new C6 Corvette, the next generation of classic American sportscars. 400HP V8; Very fast!
NULL: NULL
1: 1
*************************** 5. 行 ***************************
make_name: Honda
model_name: Accord
color: Deep Green Pearl
modelyear: 2003
price: NULL
description: Excellent condition, off-lease vehicle; Must see!
NULL: 0
1: 1
*************************** 6. 行 ***************************
make_name: Volkswagen
model_name: Golf
color: Reflex Silver
modelyear: 2004
price: NULL
description: R32 Limited edition; Low miles; Understated and suprisingly functional; Loaded.
    NULL: 1
    1: 1
******************* 7. 行 *********************
make_name: Toyota
model_name: Tacoma
color: Red
modelyear: 1993
price: NULL
description: Runs decent; 4WD; Tinted windows, aftermarket stereo; Needs a little TLC.
    NULL: 0
    1: 0
```

# 全文搜索

到目前为止，汽车经销商对这些精确查询所需能力印象深刻，并提供各种列表来帮助提高销售人员的生产力——但他们仍然想要更多。他们现在希望有一种按关键字搜索汽车库存的方式。他们的搜索需求并不复杂，但简单的 `LIKE` 比较在 `WHERE` 子句中根本无法完成任务。

你需要做的事情恰好内置于 MySQL 中——全文搜索。全文搜索在 MySQL 中默认启用，允许你对指定的任何文本列执行自然语言搜索。不过，你不能随意在数据库中开始全文搜索——你必须先做一些准备工作。

## 启用全文搜索

在 MySQL 中启用全文搜索只是简单地在一个表的列上创建索引。你可以用两种方法之一来完成：在创建表时，作为 `CREATE TABLE` 命令的一部分，或者在表的生命周期中稍后添加。

### 创建启用全文搜索的新表

你要创建的第一个全文索引将是一个全新表的一部分。要在建表时指定全文索引，你只需在列定义末尾指定全文索引和索引列列表即可：

```
CREATE TABLE 表名 (列定义, FULLTEXT (要索引的列))
```

你可以在 `FULLTEXT` 列列表中指定单个列，或指定逗号分隔的多个列。是时候在 `VehicleInventory` 数据库中实际创建一个具有全文搜索功能的表了：

```
CREATE TABLE testft (testint int, testvc varchar(50), testtxt text, FULLTEXT (testvc, testxt));
```

你刚刚创建了一个新表，并在 `testvc` 和 `testtxt` 列上建立了全文索引。

### 修改现有表以支持全文搜索

修改现有表以支持全文搜索稍微复杂一点，但也没多难。要为现有表添加全文搜索功能，你使用 MySQL 的 `ALTER TABLE` 命令，如下所示：

```
ALTER TABLE 表名 ADD FULLTEXT (列)
```

现在为 `New_Vehicles` 表添加全文索引：

```
ALTER TABLE New_Vehicles ADD FULLTEXT (description);
```

完成后，是时候好好利用这些索引了。

## 使用全文搜索进行查询

在启用了全文索引的 MySQL 表中进行搜索是一个相对轻松的过程。你只需在 `WHERE` 子句中使用 `MATCH()` 函数，如下所示：

```
SELECT [列] FROM [表] WHERE MATCH ([索引列]) AGAINST ('关键字')
```

在 `MATCH` 的参数列表中，你可以指定任意数量的列，只要它们是全文索引的一部分即可。

回到车辆库存数据库，是时候对新车列表进行搜索了。要搜索单词 `options`，你可以使用以下内容：

```
SELECT vehicle_id, description FROM New_Vehicles WHERE MATCH (description) AGAINST ('options');
```

这应该返回以下内容：

| vehicle_id | description |
| :--- | :--- |
| 2 | Last of the 2004 stock! Must sell! Loaded, all options! |
| 3 | Come drive this popular truck! 4WD, extended cab, many options. |

全文搜索的另一个巧妙技巧是可以按相关性对结果排序，并返回相关性得分。为了利用相关性数据，你可以在 `SELECT` 列表和 `ORDER BY` 子句中都使用 `MATCH()...AGAINST()` 函数，如下所示：

```
SELECT MATCH (description) AGAINST('options') AS relevance, description FROM
New_Vehicles WHERE MATCH (description) AGAINST ('options') ORDER BY MATCH
(description) AGAINST('options') \G
```

返回以下内容：



```
*************************** 1. 行 **********************
relevance: 0.38341856002808
description: Last of the 2004 stock! Must sell! Loaded, all options!
*************************** 2. 行 **********************
relevance: 0.38341856002808
description: Come drive this popular truck! 4WD, extended cab, many options.
```

### 局限性

使用全文搜索时，你必须记住一些局限性。首先，MySQL 仅支持 MyISAM 表类型的全文索引。其次，在大多数情况下，如果你在一个以上的列上创建全文索引，则提供给 `MATCH()` 的列列表必须与你创建全文索引时指定的列表完全相同。最后，MySQL 默认的最低单词/标记长度为四个字符。如果你尝试用少于四个字母的关键字进行全文搜索，将不会返回任何结果。

要更改默认的最低全文单词长度，请确保你的 MySQL 配置文件 `my.cnf` 中存在以下内容：

```
[mysqld]
ft_min_word_len=3
```

你可以使用任何整数作为最低长度。

## InnoDB 表

使用 MySQL 的一个优点是，你的数据存储不受限于特定的存储引擎。什么是存储引擎？MySQL 作为一个服务器，为用户提供了一致的接口和查询语言，但与它实际在磁盘上存储数据的方式只是松耦合。MySQL 中不同的存储引擎提供了不同的数据存储和访问方式，从可靠的默认 MyISAM，到内存堆表的高速，以及中间的所有变体。你可以使用的最灵活和强大的表类型之一是 InnoDB。由芬兰赫尔辛基的 Innobase Oy 创建的 InnoDB 存储引擎，为 MySQL 提供了一种安全和高效的数据存储和处理方式，并赋予了 MySQL 一些 MyISAM 或大多数其他表类型不具备的额外功能。

### InnoDB 的优势

尽管默认的 MyISAM 表类型提供了一种成熟且快速的方法来存储简单的数据结构，但它缺乏许多开发人员所需的一些功能——而 InnoDB 可以提供。自 MySQL 4.0 起默认可用，InnoDB 表使你能使用事务、行级锁定，以及最关键的，外键约束。

## 高级 MySQL

外键约束提供了一种在关联表之间维护引用完整性的方法。在 `VehicleInventory` 数据库中，`New_Vehicles` 表和 `Used_Vehicles` 表包含一个 `model_id` 列，用于指定每辆车车型，进而确定其制造商。可以在 `model_id` 列上应用外键约束，以确保任何插入该列的值都必须在 `Models` 表中已经存在。在默认的 MyISAM 表类型中，MySQL 无法自动强制执行此类规则，在大型数据库中，这可能导致表中出现大量无效值。InnoDB 为 MySQL 提供了一种强制执行此类规则的方法，从而确保数据始终保持相关性。

> 外键约束列仅允许在引用表中存在的值，但 NULL 是一个例外。其他受外键控制的列允许值为 NULL。

### InnoDB 的缺点

不幸的是，InnoDB 的优点伴随着一些特别麻烦的问题。首先，InnoDB 表不支持全文搜索。在决定是否使用 InnoDB 时，你总是必须考虑未来对全文索引的需求，以及在特定表上，这是否比引用完整性更重要。

其次，InnoDB 存储引擎在 `AUTO_INCREMENT` 列方面略有局限。创建 InnoDB 表时，不允许指定自增序列的初始值。这不一定是一个阻碍因素，但在设计数据库模式时值得牢记。

### 使用 InnoDB

了解 InnoDB 存储引擎的最佳方式是让它投入工作。接下来，你将通过从零开始创建新表以及修改现有表来启用 InnoDB 引擎。之后，你将实验外键的不同方面。

#### 从零创建 InnoDB 表

使用 InnoDB 存储引擎创建新表与创建标准 MyISAM 表几乎没有区别。唯一的关键区别是，你必须在创建表命令的末尾指定 `ENGINE`：

```sql
CREATE TABLE tablename (column_definitions) ENGINE=InnoDB;
```

很简单，对吧？在你的 MySQL 数据库中实际尝试一下：

```sql
CREATE TABLE innodtest (innocol int) ENGINE=InnoDB;
```

如果一切顺利，你应该看到以下内容：

```text
Query OK, 0 rows affected
```

就这样，你创建了一个简单的 InnoDB 表。

#### 转换现有 MyISAM 表

从零开始创建新的 InnoDB 表固然很好，但你手头有一些表，你希望它们能使用 InnoDB 存储引擎。你需要一种方法将这些表从默认的 MyISAM 表类型转换过来。幸运的是，在 MySQL 中更改表的存储引擎是一个简单的任务——只需使用 `ALTER TABLE` 命令并重新指定表的引擎即可。要将当前使用默认 MyISAM 表类型的 `New_Vehicles` 表进行转换，使用以下命令：

```sql
ALTER TABLE New_Vehicles ENGINE=InnoDB;
```

在你的数据库上运行此命令，你将看到：

```text
ERROR 1214 (HY000): The used table type doesn't support FULLTEXT indexes
```

MySQL 没有按预期转换你的表，而是给出了错误消息。如前所述，InnoDB 表目前在 MySQL 中不支持全文索引。如果你尝试将定义了全文索引的 MyISAM 表转换为 InnoDB，你将收到此消息。为了完成此练习，你需要删除全文索引以便转换该表：

```sql
ALTER TABLE New_Vehicles DROP INDEX description;
```

现在你应该能够继续转换该表：

```sql
ALTER TABLE New_Vehicles ENGINE=InnoDB;
```

这次，你的查询应该成功，并看到类似以下内容：

```text
Query OK, 4 rows affected (0.76 sec)
Records: 4  Duplicates: 0  Warnings: 0
```

## 外键

如果没有好的理由，你不会将表从 MyISAM 切换到 InnoDB，而在大多数情况下，外键就是一个很好的理由。一旦设置了 InnoDB 表，只需向表添加外键即可强制执行引用完整性。虽然听起来很简单，但在创建外键时有许多选项需要考虑。

创建外键的 `ALTER TABLE` 命令最基本格式看起来像这样：

```sql
ALTER TABLE [tablename] ADD CONSTRAINT [key_name] FOREIGN KEY ([indexed_column])
REFERENCES [foreign_table] ([id_column])
```

首先，你告诉 MySQL 要修改哪个表以及执行什么操作。使用 `CONSTRAINT [key_name]`，你可以选择性地给键命名，如果计划在未来修改该键，这通常是个好主意。需要引用完整性的列名随后在括号中列出。之后是 `REFERENCES` 关键字，被检查的外部表名称，以及该外部表中要引用的特定列。

将此应用于车辆库存数据库，向 `New_Vehicles` 表添加名为 `refmdl` 的外键，以将 `model_id` 列与 `Models` 表中的 `model_id` 列进行比对：

```sql
ALTER TABLE New_Vehicles ADD CONSTRAINT refmdl FOREIGN KEY (model_id)
REFERENCES Models (model_id);
```

在 MySQL 中运行此命令，你将看到类似以下内容：

```text
ERROR 1005 (HY000): Can't create table './vehicleinventory/#sql-1951_2.frm' (errno: 150)
```

这次错误消息在追踪原因方面不如预期有帮助。在这种情况下，抛出错误是因为外键涉及的某个表未使用 InnoDB 引擎。你已经将 `New_Vehicles` 表转换为 InnoDB，但 `Models` 表仍然是 MyISAM。为了正确创建外键，涉及的两个表都需要使用 InnoDB 引擎，因此必须相应地更改它们：

```sql
ALTER TABLE Models ENGINE=InnoDB;
```

然后添加外键：

```sql
ALTER TABLE New_Vehicles ADD CONSTRAINT refmdl FOREIGN KEY (model_id) REFERENCES Models (model_id);
```



现在，你的外键正在保护 `New_Vehicles` 中的 `model_id` 列免受错误数据的侵害……真的吗？确定这一点最简单的方法是测试它。尝试使用一个明显错误的 `model_id` 向 `New_Vehicles` 插入一行：

```sql
INSERT INTO New_Vehicles (model_id) VALUES (12345);
```

当你尝试执行此查询时，它应该返回以下内容：

```text
ERROR 1216 (23000): Cannot add or update a child row: a foreign key constraint fails
```

正如预期，外键检查发现该值不在 `Models` 表中，并拒绝允许插入该行。你成功阻止了任何包含不良数据的新行，但正在修改的现有行呢？试试这个查询：

```sql
UPDATE New_Vehicles SET model_id=12345 WHERE vehicle_id=1;
```

你会发现，外键也阻止了错误的更新：

```text
ERROR 1216 (23000): Cannot add or update a child row: a foreign key constraint fails
```

因此，外键成功地保护该表免受有害的 `INSERT` 和 `UPDATE` 操作，但当 `Models` 表中的值发生变化时会发生什么？查看以下查询，其中你尝试更改现有的 `model_id`：

```sql
UPDATE Models SET model_id=123 WHERE model_id=1;
```

运行此查询时，你应该得到以下错误：

```text
ERROR 1217 (23000): Cannot delete or update a parent row: a foreign key constraint fails
```

## 第 4 章

这个错误简单地反映了简单 `InnoDB` 外键关联的另一种行为：如果被引用列的值存在于引用表中，则不能修改该被引用列。如果这种行为不是你想要的怎么办？幸运的是，你可以指定外键的更新和删除行为为五种不同选项之一：`RESTRICT`（限制）、`CASCADE`（级联）、`SET NULL`（置空）、`NO ACTION`（无操作）和 `SET DEFAULT`（置默认值）。以下是每种行为含义的简要说明：

- `RESTRICT` 是默认行为。被引用的值不能被更改或删除。
- `CASCADE` 允许任何更新传播到引用表。如果你在 `Models` 表中更新了 `model_id`，它将级联到 `New_Vehicles` 表并更新任何相应的行。注意，这也适用于删除（如果指定）——在父表中删除一行将自动删除子表中引用该值的所有行。
- `SET NULL` 在更新父值时将子表中的值更改为 `NULL`。
- `NO ACTION` 简单地告诉数据库允许对父表的更改，并对子表不做任何操作。
- `SET DEFAULT` 当父值被更改或删除时，将子表中的值更改为其 `DEFAULT` 值。

实现这些行为只需在外国键定义的末尾添加所需的 `ON DELETE` 或 `ON UPDATE` 子句即可，如下所示：

```sql
ALTER TABLE [tablename] ADD CONSTRAINT [key_name] FOREIGN KEY ([indexed_column])
REFERENCES [foreign_table] ([id_column])
ON UPDATE [update_behavior] ON DELETE [delete_behavior]
```

要将现有键更改为支持不同的更新和删除行为，你首先需要删除旧键，然后使用新行为重新创建外键。要将 `New_Vehicles` 表的外键更改为级联任何更新，并在删除车型时置为 `NULL`，使用以下命令：

```sql
ALTER TABLE New_Vehicles DROP FOREIGN KEY refmdl;
ALTER TABLE New_Vehicles ADD CONSTRAINT refmdl FOREIGN KEY (model_id)
REFERENCES Models (model_id) ON UPDATE CASCADE ON DELETE SET NULL;
```

现在，每次 `Models` 表中的 `model_id` 被更改时，新值都会传播到 `New_Vehicles` 中使用原始值的所有行。请自行查看：

```sql
UPDATE Models SET model_id=123 WHERE model_id=1;
SELECT * FROM New_Vehicles \G
```

更新将成功，并返回类似以下内容：

```text
*************************** 1. row ***************************
 vehicle_id: 1
 model_id: 123
 price: NULL
 color: Dark Blue
 description: Poplar SUV; great for moving people or cargo across town, or wherever your adventures may take you.
 modelyear: 2005
```

### 数据库查询输出（第 2-4 行）

- **第 2 行**
  - `vehicle_id`: 2
  - `model_id`: NULL
  - `price`: NULL
  - `color`: 石墨珍珠色
  - `description`: 2004 年库存最后一台！必须售出！配置齐全，所有选装包！
  - `modelyear`: 2004

- **第 3 行**
  - `vehicle_id`: 3
  - `model_id`: 4
  - `price`: NULL
  - `color`: 辐射红
  - `description`: 来试驾这款热门卡车吧！四驱，加长驾驶室，众多选装配置。
  - `modelyear`: 2005

- **第 4 行**
  - `vehicle_id`: 4
  - `model_id`: 5
  - `price`: NULL
  - `color`: 戴通纳日落橙金属漆
  - `description`: 全新 C6 科尔维特，经典美式跑车的下一代，400 马力 V8 发动机；极速快！
  - `modelyear`: 2005

#### 从 InnoDB 转换回 MyISAM

你刚刚尝试了 `InnoDB` 表和外部键，但你发现还是更希望拥有全文搜索功能。改回 `MyISAM` 是一个相对轻松的过程。通常只需两步：移除任何 `InnoDB` 特有的功能（如外部键），并使用 `ALTER TABLE` 将存储引擎类型更改回 `MyISAM`。要将 *New_Vehicles* 表转换回 `MyISAM`，请执行以下操作：

```sql
ALTER TABLE New_Vehicles DROP FOREIGN KEY refmdl;
ALTER TABLE New_Vehicles ENGINE=MyISAM;
```

此时，*New_Vehicles* 表已恢复使用 `MyISAM` 存储引擎，你再次获得在该表上添加和使用全文索引的能力。

## 控制访问权限

作为 `MySQL` 数据库管理员，你最重要的工作之一就是控制谁可以访问系统，以及他们可以访问哪些资源。在大多数情况下，每个数据库只需要少量的用户账户，而你创建的那些账户也应仅授予执行其任务所需的最小权限。幸运的是，`MySQL` 提供了多种方式来控制谁可以访问你的系统以及具体的资源。

### 用户管理

为了帮助控制数据库中的用户账户，`MySQL` 提供了几种维护用户账户的方法。无论是协作者、技术熟练的客户，还是基于 Web 的系统前端，每个用户都需要获得针对其所需资源的专门授权的访问权限。

### 第 4 章

在配置用于实际环境的数据库时，你需要做的第一件事之一，就是设置用户或系统本身可能需要的任何账户。为了在数据库中为用户设置专门访问权限，你需要了解 `MySQL` 可控制访问权限的不同级别。`MySQL 4.1` 可以区分权限方面的四个不同访问级别：全局级别、数据库级别、表级别和列级别。

- **全局级别权限**是最强大的，适用于 `MySQL` 实例上运行的所有数据库。通常这类权限保留给管理员账户，因为应用程序或最终用户需要访问数据库服务器操作所有方面的情况很少见。
- **数据库级别权限**顾名思义，仅适用于数据库级别。数据库级别访问通常由特定数据库或应用程序的管理员使用，并且拥有对指定数据库进行完全控制的能力。
- **表级别权限**按表适用。你可以为特定表或一组表的特定用户创建或移除访问权限。这种级别的访问控制在配置数据库供应用程序直接访问时经常使用——应用程序仅需对每个表进行特定类型的访问，而不需要更多。
- **列级别权限**是 `MySQL` 提供的最精细的控制级别。正如你所料，它控制对给定表中特定列或列组的访问。

### 使用 GRANT

现在你理解了 `MySQL` 访问系统的作用范围变化，是时候看看如何实际控制权限了。



为了创建用户账户并添加权限，MySQL 提供了 `GRANT` 命令。只要你清楚你要授予什么访问权限以及授予给谁，使用 `GRANT` 命令相对简单。`GRANT` 命令的通用语法如下：

```sql
GRANT [privileges] ON [resource] TO [identity]
```

让我们花点时间剖析一下 `GRANT`。命令的第一部分 `GRANT [privileges]` 是你指定在资源上（稍后指定）允许什么权限的地方。下表展示了一些你可以使用的更常见的权限。

| 权限 | 提供 |
| :--- | :--- |
| ALL [PRIVILEGES] | 设置除 GRANT OPTION 以外的所有简单权限 |
| ALTER | 允许使用 ALTER TABLE |
| CREATE | 允许使用 CREATE TABLE |
| DELETE | 允许使用 DELETE |
| DROP | 允许使用 DROP TABLE |
| INDEX | 允许使用 CREATE INDEX 和 DROP INDEX |
| INSERT | 允许使用 INSERT |
| SELECT | 允许使用 SELECT |
| UPDATE | 允许使用 UPDATE |
| USAGE | “无权限”的同义词；用户可以登录但不再多 |

命令的第二部分 `ON [resource]` 是你指定要提供哪些数据库级别和项目的地方。要在全局级别授予访问权限，你指定 `*.*` 作为资源，如下所示：

```sql
GRANT [privileges] ON *.* TO [identity] . . .
```

在数据库级别授予访问权限时，你指定数据库名称，后跟 `.*`。例如，如果你想要授予对 `testdb` 数据库的访问权限，你会使用类似以下的语句：

```sql
GRANT [privileges] ON testdb.* TO [identity] . . .
```

要为数据库内的特定表创建权限，你提供数据库名称，后跟表名（用点分隔）。如果你试图指定 `testdb` 数据库中 `testtable` 的访问权限，你可能会使用类似这样的语句：

```sql
GRANT [privileges] ON testdb.testtable TO [identity] . . .
```

授予列级别权限与之前三个层级的逻辑递进略有不同。在赋予列级别权限时，你必须在使用列表中的每个权限后的括号内指定列列表，如下所示：

```sql
GRANT SELECT (column1), INSERT (column1) ON testdb.testtable TO [identity] . . .
```

> **注意：** 在指定列级别权限时，你必须在 `ON` 后使用完整的表级别语法，否则 MySQL 将返回错误。

`GRANT` 命令的最后一个关键部分 `TO [identity]...` 是你指定访问权限将授予谁，以及用户获得此访问权限必须满足的任何可选要求。为了满足 `GRANT` 的 `TO...` 部分，你至少必须提供用户名/主机组合。在 MySQL 中，每个不同的用户 `must` 必须为其用户名和 `localhost` 设置至少基本的使用权限。例如：

```sql
GRANT USAGE ON *.* TO testuser@localhost
```

此处用户 `'testuser'` 已在全球范围内被授予基本使用权限，这相当于没有任何访问权限，但该用户现在已被系统知晓。一旦创建了一个 `localhost` 账户，你可以在指定的任何远程主机上为相同用户名创建额外的访问语句：

```sql
GRANT SELECT ON testdb.* TO testuser@192.168.1.2
```

需要注意的是，如果你在创建远程访问账户之前没有先为某个用户创建 `localhost` 条目，MySQL 不会抱怨。然而，你的应用程序可能会抱怨——它们可能无法远程连接，而在刚开始熟悉 MySQL 访问系统时，这是一个常见的令人头疼的问题来源。

在大多数情况下，要求用户账户在登录时也提供密码非常重要。在使用 `GRANT` 创建账户时添加密码，只需在 `GRANT` 命令末尾添加短语 `IDENTIFIED BY 'password'`，如下所示：

```sql
GRANT [privileges] ON [resource] TO [identity] IDENTIFIED BY '[password]';
```

> **注意：** 在将密码用于 `GRANT` 命令之前，你无需预先加密密码——MySQL 会在将密码存储到系统中之前自动加密密码。

既然你看到了一些关于如何使用 `GRANT` 的通用示例，你可以在真实数据库上尝试一下。你将为车辆库存数据库添加三个用户。一个用户将获得整个数据库的完全访问权限。第二个用户将获得对 `New_Vehicles` 表的 `SELECT`、`UPDATE`、`INSERT` 和 `DELETE` 访问权限。第三个也是最后一个用户将获得对 `New_Vehicles` 表中 `color` 列的 `SELECT` 访问权限。首先，创建拥有数据库中所有权限的用户：

```sql
GRANT ALL PRIVILEGES ON VehicleInventory.* TO testuser1@localhost IDENTIFIED BY 'testpass1';
```

接下来，创建具有受限表级权限的用户：

```sql
GRANT SELECT, INSERT, UPDATE, DELETE ON VehicleInventory.New_Vehicles TO testuser2@localhost IDENTIFIED BY 'testpass2';
```

最后，创建第三个具有极其有限访问权限的用户：

```sql
GRANT SELECT (color) ON VehicleInventory.New_Vehicles TO testuser3@localhost IDENTIFIED BY 'testpass3';
```

### 使用 REVOKE

现在你可以使用 `GRANT` 命令创建用户和权限，但你仍然需要一种方法来撤销权限。为此，你使用 `REVOKE`。`REVOKE` 命令看起来几乎与 `GRANT` 命令完全相同：

```sql
REVOKE [privileges] ON [resource] FROM [identity]
```

注意 `REVOKE` 和 `GRANT` 语法之间仅有的两个主要区别：使用单词 `FROM` 代替 `TO`，以及无需添加 `IDENTIFIED BY` 短语。

要在实时数据库中快速查看 `REVOKE` 的效果，请尝试以下查询：

```sql
REVOKE ALL PRIVILEGES ON VehicleInventory.New_Vehicles FROM testuser2@localhost;
```

仅凭这简短的一步，你就撤销了 `testuser2` 账户拥有的所有权限。

在撤销权限时，通常你必须列出用户拥有明确权利的具体表、数据库和列。如果你使用的是 MySQL 4.1.2 或更高版本，你可以使用一条快捷命令快速清除用户在任何权限级别的所有权限：

```sql
REVOKE ALL PRIVILEGES, GRANT OPTION FROM [identity]
```

## GRANT 和 REVOKE 的替代方案

如果你想从系统中彻底移除 `testuser3`，你需要发送以下命令：

```sql
REVOKE ALL PRIVILEGES, GRANT OPTION FROM testuser3@localhost;
```

如果出于某种原因，你不希望使用 GRANT 或 REVOKE 命令，你可以手动创建用户，并直接将权限应用于 MySQL 访问表。

MySQL 在内置的 mysql 数据库中的四个主要表中存储不同级别的用户权限。这四个主要访问表中的每一个都对应四个不同的访问级别。

在全局级别，有一个 user 表，其结构如下：

| 字段 | 类型 |
| --- | --- |
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

| Repl_slave_priv | enum('N','Y') |

| Repl_client_priv | enum('N','Y') |

| ssl_type | enum('ANY','X509','SPECIFIED') |

| ssl_cipher | Blob |

| x509_issuer | Blob |

| x509_subject | Blob |

| max_questions | int(11) unsigned |

| max_updates | int(11) unsigned |

| max_connections | int(11) unsigned |

`user` 表包含系统中所有用户的列表，以及该用户可能拥有的任何全局权限。与访问权限相关的关键字段是所有后缀为 `_priv` 的列。请注意，所有权限列的默认值均为 `no`。

`db` 表保存数据库级别访问权限的记录。`db` 的结构如下：

| 字段 | 类型 |
| --- | --- |
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

只有当用户需要显式的数据库级别权限时，才会出现在此表中。

另一个表，`tables_priv`，保存表级别操作的权限：

| 字段 | 类型 |
| --- | --- |
| Host | char(60) |
| Db | char(64) |
| User | char(16) |
| Table_name | char(64) |
| Granter | char(77) |
| Timestamp | timestamp |
| Table_priv | set('Select', 'Insert', 'Update', 'Delete', 'Create', 'Drop', 'Grant', 'References', 'Index', 'Alter') |
| Column_priv | set('Select', 'Insert', 'Update', 'References') |

与 `db` 表类似，只有当用户需要表级别权限时，用户才会出现在此表中。

最后一个表，`columns_priv`，包含列级别的访问定义，其结构如下：

| 字段 | 类型 |
| --- | --- |
| Host | char(60) |
| Db | char(64) |
| User | char(16) |
| Table_name | char(64) |
| Column_name | char(64) |
| Timestamp | timestamp |
| Column_priv | set('Select', 'Insert', 'Update', 'References') |

为什么你需要知道这些每个表的内部细节？如果你想在不使用 `GRANT` 或 `REVOKE` 的情况下添加或移除访问权限，你必须针对这些核心表使用标准的 `INSERT`、`UPDATE` 和 `DELETE` 命令。

首先要在数据库中创建一个用户，无论访问级别如何，该用户必须存在于 `user` 表中：

```sql
INSERT INTO mysql.user (Host, User, Password) VALUES ('localhost', 'testuser6', PASSWORD('testpass6'));
```

请注意，这里使用了 `PASSWORD()` 函数，而在 `GRANT` 语法中不使用。`GRANT` 命令会自动使用 `PASSWORD()` 函数对密码进行加密；像这样的手动插入不会这样做，因此你必须自己加密它。

要添加访问权限，只需向相应的表插入一行，将每个所需的权限列指定为 Y。要为新建用户授予 VehicleInventory 数据库的数据库级别 SELECT、UPDATE、INSERT 和 DELETE 权限，请使用以下命令：

```sql
INSERT INTO mysql.db (Host, Db, User, Select_priv, Insert_priv, Update_priv, Delete_priv) VALUES ('localhost', 'VehicleInventory', 'testuser6', 'Y', 'Y', 'Y', 'Y');
```

如果你需要撤销用户权限，只需在所需的表上执行 DELETE。要移除 testuser6 的数据库级别权限，请使用此查询：

```sql
DELETE FROM mysql.db WHERE Host='localhost' AND User='testuser6';
```

完全从数据库中移除用户稍微复杂一点。你必须先移除授予该用户的所有权限，然后可以使用 DELETE 命令将其从用户表中移除。

为了让 MySQL 意识到你刚刚手动更改的权限，你必须重新加载权限表：

```sql
FLUSH PRIVILEGES;
```

如果在更改访问权限后没有刷新权限，直到下次重启时 MySQL 才会反映这些更改。这适用于你对任何访问级别手动进行的任何权限更改——使用 `GRANT` 或 `REVOKE` 不需要重新加载权限表。

## 服务器限制

限制服务器访问的另一种方式，在更大规模上，实际上是限制服务器整体的远程访问。如果你的数据库仅服务于直接登录机器的用户，那么让服务器接受远程网络连接的需求很小。要停止 MySQL 监听传入的网络连接，请确保以下内容存在于 MySQL 配置文件（通常是 `my.cnf`）的 `[mysqld]` 部分中：

```ini
[mysqld]
skip-networking
```

将该语句添加到配置文件中，然后重新启动 MySQL 服务器进程，将禁用任何传入 MySQL 的流量。如果你的网络和服务安全性很重要，并且只有本地账户需要访问，那么这种措施非常重要。

## 分析数据库

尽管你使用数据库的时间大部分将花费在添加、更新、检索和删除数据上，但偶尔你需要立即了解数据库结构本身的信息。幸运的是，MySQL 提供一些易于使用的信息工具，以及分析和优化数据库的简单方法。

在 MySQL 命令 shell 内部，你可以使用几个共享前缀 `SHOW` 的常见命令，以获取关于数据库当前状态的各种信息。以下部分描述了一些更常见的 `SHOW` 命令。

### SHOW COLUMNS

`SHOW COLUMNS` 命令返回表中所有列及其属性的列表。`SHOW COLUMNS` 的一般格式如下：

```sql
SHOW COLUMNS FROM {table} FROM {database}
```

如果你想获取 `New_Vehicle` 表中所有列的列表，你可以使用以下命令：

```sql
SHOW COLUMNS FROM New_Vehicles FROM VehicleInventory;
```

这将返回以下内容：

| 字段 | 类型 | Null | 键 | 默认 | 额外 |
| --- | --- | --- | --- | --- | --- |
| `vehicle_id` | `int(11)` |  | PRI | `NULL` | `auto_increment` |
| `model_id` | `int(11)` | YES |  | `NULL` |  |
| `price` | `decimal(10,2)` | YES |  | `NULL` |  |



| `color` | `varchar(200)` | YES |  | `NULL` |  |

| `description` | `text` | YES |  | `NULL` |  |

| `modelyear` | `int(11)` | YES |  | `NULL` |  |

在返回的输出中，`Field`列包含每列的名称，`Type`显示列的数据类型，`Null`指定是否允许在列中存在`NULL`值，`Key`指示每列属于什么键或索引类型，`Default`显示指定的默认列值，`Extra`显示对每列给出的任何特殊处理。请注意，此命令在功能上与 MySQL 的`DESCRIBE {table}`命令完全相同。

### SHOW CREATE TABLE

你可能希望了解可以使用什么命令来创建给定的表。为此，你可以使用`SHOW CREATE TABLE`命令：

```sql
SHOW CREATE TABLE {table name}
```

要获取创建你的`New_Vehicles`表的`create`命令，请发送：

```sql
SHOW CREATE TABLE New_Vehicles \G
```

对`VehicleInventory`数据库运行此命令，你会得到：

```
*************************** 1. row ***************************
Table: New_Vehicles
Create Table: CREATE TABLE `New_Vehicles` (
```

# 第 4 章

```sql
‘vehicle_id’ int(11) NOT NULL auto_increment,
‘model_id’ int(11) default NULL,
‘price’ decimal(10,2) default NULL,
‘color’ varchar(200) default NULL,
‘description’ text,
‘modelyear’ int(11) default NULL,
PRIMARY KEY (‘vehicle_id’)
) ENGINE=MyISAM DEFAULT CHARSET=latin1
```

然后将这条完整的`CREATE TABLE`命令输入到一个新的数据库中，即可创建`New_Vehicles`表结构的精确副本。

### SHOW DATABASES

`SHOW DATABASES`命令的作用正如它的名称所示——它显示当前登录账户有权访问的系统中的所有数据库。只需运行该命令：

```sql
SHOW DATABASES;
```

它将会返回当前用户可访问的数据库列表：

+--------------------+
| Database           |
+--------------------+
| VehicleInventory   |
| mysql              |
+--------------------+

### SHOW GRANTS

`SHOW GRANTS`命令列出授予特定用户账户的所有访问权限。例如，要查看`VehicleInventory`数据库中授予`testuser1`账户的所有访问权限，请使用以下命令：

```sql
SHOW GRANTS FOR ‘testuser1’@‘localhost’\G
```

返回结果如下：

```text
*************************** 1. row ***************************
Grants for testuser1@localhost: GRANT USAGE ON *.* TO ‘testuser1’@‘localhost’
IDENTIFIED BY PASSWORD ‘*E69570EP2322D3DC1F956C48199FEB21FF2D7D984’
*************************** 2. row ***************************
Grants for testuser1@localhost: GRANT ALL PRIVILEGES ON ‘vehicleinventory’.* TO
‘testuser1’@‘localhost’
*************************** 3. row ***************************
Grants for testuser1@localhost: GRANT SELECT, SELECT (description), INSERT
(description), UPDATE (description) ON ‘vehicleinventory’ .‘used_vehicles’ TO
‘testuser1’@‘localhost’
```

# 高级 MySQL

## 数据库维护

您已经创建了车辆库存数据库，将其投入生产环境，设置了搜索功能，并且客户对结果感到满意。是时候坐下来放松一下了，对吗？

并不完全如此。您可能还需要考虑另一件事，以帮助最大程度地降低生产数据库灾难性丢失的成本。您需要的是备份。

### 创建备份

得益于系统附带的一组优秀的客户端工具，在 MySQL 中执行备份非常容易。要创建备份，您可以使用`mysql_dump`工具。首先，如果需要，您需要退出 MySQL 客户端，回到标准的 shell 提示符下：

```
mysql> exit
```

一旦您回到命令提示符，只需调用`mysql_dump`命令行工具即可。对于大多数数据库备份，以下通用格式即可适用：

```
mysqldump --opt databasename > backupfile.sql
```

在这里，您调用了`mysqldump`命令并指示其将名为`databasename`的数据库转储到名为`backupfile.sql`的文件中。同时还提供了`--opt`选项，该选项指示备份工具使用一组通用选项，这些选项输出的格式有助于 MySQL 更准确地恢复文件。

> `要查看更多的 mysqldump 选项，请在命令提示符下键入 man mysqldump。`

要备份车辆库存数据库，请使用以下命令：

```
mysqldump --opt VehicleInventory > vi_backup.sql
```

> `与 mysql 命令行客户端一样，如果需要提供用户名和密码，请确保在数据库名称之前相应地使用 -u 和 -p。`

现在，您在文件`vi_backup.sql`中拥有了一个完整的数据库创建脚本。您可以按需归档此文件、将其恢复到不同的服务器、将其刻录到 CD 或 DVD 上，或者执行您喜欢的其他操作。

### 从备份中恢复数据库

万一服务器崩溃、被黑客攻击，或者您只是想在开发环境中测试生产数据库的副本，您将不得不知道如何恢复数据库备份。在 MySQL 中，这极其简单，因为您可以使用 MySQL 命令行客户端，如下所示：

```
mysql databasename < backupfile.sql
```

因此，要恢复`VehicleInventory`数据库，请使用：

```
mysql VehicleInventory < vi_backup.sql
```

请注意，恢复目标数据库的名称必须是系统中已经实际存在的数据库。如果您希望将备份恢复到一个新数据库，只需登录到`mysql`客户端，创建一个具有所需名称的空数据库，退出客户端，然后根据需要恢复您的备份。

#### 总结

希望借助本章的信息，您将能够去设置复杂的数据库架构，使用复杂的查询，并维护整个系统。掌握这些基本工具后，您将能够克服极少数的数据库障碍。您可能会发现在作为开发者的角色中，您花在命令行界面上的时间会更少，而花在 PhpMyAdmin 或`MySQL AB’s`自家的`MySQL Administrator GUI`工具上的时间会更多。只要这些工具具有输入原始命令的方式，您在本章中看到的原始命令和查询就应该适用于其中任何一种工具。您对执行管理任务和数据处理任务的确切 SQL 的理解，也将帮助您理解 GUI MySQL 应用程序中任何文本框、单选按钮和复选框背后正在发生的事情——或者在您自己的 PHP 应用程序中正在发生的事情。

# 第 5 章

## PHP 配置

当您使用 LAMP 技术时，很少有事物比 PHP 的配置方式更影响您的编码决策。任何 PHP 安装的核心是配置文件`php.ini`。该文件中的设置会极大地影响您编写应用程序的方式、服务器的性能表现，甚至其安全性。本章告诉您应该查看和更改哪些设置，以改善您的 PHP 安装，并提供了一组脚本来自动将您的 PHP 环境和配置设置准备得符合您的喜好。

## 修改 php.ini

如前所述，`php.ini`文件是配置 PHP 安装的主要工具。本节介绍了一些您应该设置的配置指令，以及几个在 PHP5 中新增的指令。

### 推荐的配置指令

配置 PHP 时，有一些设置需要牢记，以保持系统的安全并以最快速度运行：



# PHP 配置建议

- `register_globals = off`：将旧的 PHP 代码迁移到新系统时，最常见的问题之一是 PHP 如何处理表单数据和变量。在较早版本的 PHP 中，表单字段会自动转换为与 PHP 引擎共享相同名称的全局变量。虽然有些人认为这很方便，但由于命名和使用混淆，它最终成为了安全风险。自 PHP 4.2.0 起，`register_globals` 的默认值已设置为 off。您应该保持此设置为 `off`，并使用 `$_GET`、`$_POST` 和 `$_COOKIE` 超全局变量，而不是依赖自动创建的变量。

在开发应用程序时，保持 `register_globals` 设置为 `off` 尤为关键，因为您无法确定任何最终可能运行该应用的生产服务器的设置。

- `display_errors = off`：虽然在开发环境中这不是必需的，实际上是一个负担，但对于任何位于生产或公共 web 服务器上的 PHP 应用程序，将 `display_errors` 设置为 off 是一个好主意。关闭 `display_errors` 可禁止 PHP 在用户的 web 浏览器中显示任何解析错误或运行时错误。终端用户看到的任何错误都可能揭示应用程序的内部工作原理，这对任何希望攻击您站点的恶意个人来说可能是有用的信息。

- 在开发或调试情况下，完全可以将 `display_errors` 保持开启，以辅助调试。

- `log_errors = on`：此设置通常与 `display_errors` 一起使用，指示 PHP 将通常显示在屏幕上的所有错误记录到文件中。您可以将该文件用于后续分析或调试，或使用您选择的工具定期自动通知 webmaster。

- `error_log = filename or error_log = syslog`：`error_log` 指令告诉 PHP 在启用 `log_errors` 时将错误发送到哪里。您可以指定一个文件名，PHP 将把错误写入该文件；或者指定 `syslog`，它将把错误发送到系统日志守护程序。

- `error_reporting = E_ALL`：此指令简单地告诉 PHP 报告其遇到的所有错误、警告和通知。默认情况下，PHP 显示除通知之外的所有内容。显示通知通常是个好主意，特别是在开发期间，因为它可以帮助您跟踪未初始化的变量和其他小的代码漏洞。

- `magic_quotes_gpc = off`：`magic_quotes_gpc` 指令告诉 PHP 在加载脚本时是否应自动转义输入/表单数据。虽然此设置旨在节省时间，但如果您决定切换数据库，或使用不使用反斜杠转义特殊字符的数据库，它实际上可能会引发问题。如果您认为有一天可能会切换数据库系统，或者当前使用混合数据库环境甚至根本不使用数据库，将其设置为 off 是个好主意。

- `variables_order = “GPCS”`：将 `variables_order` 设置为 `GPCS` 告诉 PHP 不要自动生成通常用于保存环境变量的 `$_ENV` 数组——通常在 `variables_order` 设置为 `EGPCS` 时设置。此建议仅出于性能原因，如果您仍然需要访问环境变量，可以使用 `getenv()` 函数。

- `allow_call_time_pass_reference = off`：此指令可能不会影响所有代码，但它可以帮助防止您的代码因 PHP 的某个未来版本而变得过时。将 `allow_call_time_pass_reference` 设置为 off 可以防止您强制函数参数通过引用传递。如果在此设置关闭时尝试通过引用传递参数（使用 `&` 前缀），将生成一个警告。虽然这对生产服务器目前不是关键问题，但在开发应用程序时使用此设置是个好习惯，以确保它们与 PHP 的未来版本兼容。

- `asp_tags = off`：虽然在大多数设置上这通常不是问题，但如果使用 ASP 风格的标签（`{$%}`）而不是标准的 PHP 标签（`{<php ?>}`），如果您将应用程序移动到具有不同 `asp_tags` 设置的服务器上，最终可能会成为一个问题。虽然这不是关键要求、性能问题或安全问题，但在开发期间保持 `asp_tags` 设置为 off 是个好主意，以避免以后出现可爱的兼容性问题。

- `short_open_tag = off`：与将 `asp_tags` 设置为 off 一样，将 `short_open_tag` 设置为 off 也有助于确保您的应用程序在不同服务器上普遍可用，而不是因为简单的配置差异而被破坏。

使用 `short_open_tag = off` 的另一个好处是，你可以在脚本中使用 `<?xml ?>` 语句，例如 XML 文档序言。如果 `short_open_tag` 被设置为 `on`，并且你试图使用 `<?xml`，它会将 `<? ?>` 包装器内的任何内容都尝试解析为 PHP，并抛出错误。

- `zlib.output_compression`：将 `zlib.output_compression` 设置为 on 会指示 PHP 在发送给最终用户之前使用 zlib 库压缩输出数据。这与在 Apache 中使用 `mod_gzip` 或 `mod_deflate` 的效果类似：输出的字节数减少，从而改善了互联网上的传输时间。

## PHP5 的新特性

除了 PHP5 中引入的改进的巨大对象模型外，还增加了一些新的配置设置。PHP5 的新增内容如下：

- `mail.force_extra_parameters`

- `register_long_arrays`

- `session.hash_function`

- `session.hash_bits_per_character`

- `zend.zel_compatibility_mode`

以下部分描述了这些新指令。

### mail.force_extra_parameters

这个新指令允许你在 `mail()` 函数中指定传递给 `Sendmail` 的具体值。通常在使用 `mail()` 函数时，你可以传递第五个参数，向 `Sendmail` 发送额外的命令行参数。当此指令被设置时，`mail()` 第五个参数中指定的任何 `Sendmail` 命令行参数都会被 `mail.force_extra_parameters` 中设置的值自动覆盖。

*无论何时发送邮件，设置的 `mail.force_extra_parameters` 的值始终会被使用——即使在安全模式下，`mail()` 的第五个参数也被禁用时也是如此。*

### register_long_arrays

通常，当网站提交表单时，PHP 会获取表单各字段的值，并根据表单的方法 `GET` 或 `POST` 将它们放入两个大型数组中。如果表单是使用 `GET` 提交的，一个名为 `$HTTP_GET_VARS` 的数组将填充表单值，每个字段在数组中都有一个对应的命名索引，此外还有一个名为 `$_GET` 的相同数组，其中包含相同的值。这种重复主要是为了向后兼容性——超全局变量 `$_GET` 和 `$_POST` 直到 PHP 4.1.0 才被引入，因此许多旧应用程序仍然使用旧的 `$HTTP_***_VARS` 数组。

如果你的应用程序根本不使用旧式的数组，出于性能原因，你应该将此设置为 `off`。

## 第 5 章

### session.hash_function

过去，当 PHP 为用户创建新会话和会话 ID 时，你无法控制用于创建会话 ID 的算法。使用 `session.hash_function`，你可以选择用于创建会话 ID 的两种哈希算法之一。

将此选项设置为 0 指示 PHP 使用 MD5 对会话 ID 进行哈希处理（128 位）。如果你想要使用 SHA-1（160 位），你会将值设置为 1。

### session.hash_bits_per_character

为了进一步配置会话 ID，你可以使用 `session.hash_bits_per_character` 来指定在将会话 ID 转换为可读值时，每个字符存储多少位。选项如下：

- 4 : 0-9, a-f

- 5 : 0-9, a-v

- 6 : 0-9, a-z, A-Z, `"`, `'`

### zend.zel_compatibility_mode

最后一个新的配置设置 `zend.zel_compatibility_mode` 简单指定是否要启用与 Zend Engine 1 (PHP4) 的兼容性。

## PHP 运行时配置

直接检查和修改 `php.ini` 中指令的设置通常是监控和修改安装的快速简便方法，但很多时候你无法停机进行更改，或者你需要在脚本运行时知道某个设置。本章这部分介绍的技术将帮助你在服务器仍在运行时进行修改。

### 获取当前运行时设置

如果你需要知道已安装的 PHP 的确切版本，PHP 提供了 `phpversion()` 函数，它返回一个列出完整已安装版本的字符串。例如：

```php
<?php
echo "The current version of PHP installed is: " . phpversion();
?>
```

这将输出类似以下内容的内容：



> The current version of PHP installed is: 5.0.4

### 检索配置设置

有时候，简单的版本检查提供的信息不够，你需要更多关于 PHP 配置方式的信息，但你无法直接访问 `php.ini`。要查找运行时配置设置，你有三个主要选择：`ini_get()`、`get_cfg_var()` 和 `ini_get_all()`。

第一个选项 `ini_get()` 将给定字符串与当前运行时配置进行检查。如果设置匹配，则返回该设置的值；如果未找到匹配项，则返回空字符串：

```php
<?php
echo 'Error reporting: ' . ini_get('error_reporting') . "\n" .
     'Register globals: ' . ini_get('register_globals') . "\n" .
     "Nonexistant setting: " . ini_get('nonexistant') . "\n";
?>
```

运行此代码应产生类似以下内容的输出：

```
Error reporting: 2047
Register globals:
Nonexistant setting:
```

请注意，在这种情况下，错误报告的值实际上是常量 `E_ALL` 的数值等价物。但 `register_globals` 的值在哪里呢？当 `ini_get()` 返回 `php.ini` 认为的布尔值（`off` 或 `on`，`0` 或 `1`，`yes` 或 `no`）时，它会自动转换它们。任何“off”或“no”的值自动转换为“0”；任何“yes”或“on”的值自动变为“1”。

检索配置设置的第二个选项 `get_cfg_var()` 的行为与 `ini_get()` 几乎相同，除了它直接从 `php.ini` 拉取值，而不是当前的运行时环境。除非你在代码中更改了配置变量（稍后会有更多说明），否则值通常应与 `ini_get()` 返回的值匹配。例如，请考虑以下代码：

```php
<?php
echo 'Error reporting: ' . get_cfg_var('error_reporting') . "\n" .
     'Register globals: ' . get_cfg_var('register_globals') . "\n" .
     "Nonexistant setting: " . get_cfg_var('nonexistant') . "\n";
?>
```

除非某个设置在活动脚本中被更改，否则此代码将产生与以下内容相同的输出：

```php
<?php
echo 'Error reporting: ' . ini_get('error_reporting') . "\n" .
     'Register globals: ' . ini_get('register_globals') . "\n" .
     "Nonexistant setting: " . ini_get('nonexistant') . "\n";
?>
```

获取配置信息的第三种方法 `ini_get_all()` 像放大版的 `ini_get()`。它不再指定单个值来查找，而是 `ini_get_all()` 返回一个包含所有已注册配置选项的数组。它返回的值也不仅限于当前设置——`ini_get_all()` 返回在 `php.ini` 中设置的全局值、当前时刻存在的本地值以及更改设置所需的访问级别。

看看这个简单的例子：

```php
<?php
print_r(ini_get_all());
?>
```

执行此代码，你会得到类似以下内容的结果：

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
)
```

请注意，此输出已被大幅简略——实际返回的数组包含超过 150 个不同的项。另外请注意，某些值是空字符串，例如 `allow_call_time_pass_reference` 的全局和本地值。当 `ini_get_all()` 返回每个设置时，它使用与 `ini_get()` 执行的值转换相同的方式，涉及 `off`/`on` 值。

## 扩展信息

既然你已经能够获取关于运行时设置的信息，现在是时候学习如何检查扩展及其属性了。PHP 为你提供了三个内置函数来查找已加载扩展的相关信息。

第一个函数是 `extension_loaded()`，它仅用于检查给定的扩展是否已加载。你只需提供扩展的名称，它会返回一个布尔值，指示该扩展是否可用，如下所示：

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

当你运行这段代码时，你应该会看到以下内容：

```
MySQL is available.
Fake SQL is NOT available.
```

如果你需要同时了解多个扩展的状态，PHP 提供了 `get_loaded_extensions()`。与 `ini_get_all()` 类似，`get_loaded_extensions()` 返回一个包含所有已加载扩展的数组。请考虑以下代码：

```php
<?php

print_r(get_loaded_extensions());

?>
```

根据你的当前配置，这应该会产生类似以下的输出（可能或多或少有几个扩展）：

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
    [9] => pgsasl
    [10] => pcre
    [11] => mysql
    [12] => mysqli
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

一旦你知道某个扩展可用，你可能希望了解更多关于该特定模块的信息。要获取扩展提供的所有函数的列表，请使用 `get_extension_funcs()`。与之前的一些信息性命令类似，它返回一个可用值的数组，但在这种情况下，它提供的是给定扩展的函数列表。例如：

```php
<?php
print_r(get_extension_funcs('simplexml'));
?>
```

运行这段代码应该给出 SimpleXML 扩展提供的所有函数列表：

```
Array
(
    [0] => simplexml_load_file
    [1] => simplexml_load_string
    [2] => simplexml_import_dom
)
```

## 魔术引号



如本章前面所述，PHP 允许一种称为“魔术引号”的特殊数据处理机制。当启用魔术引号时，PHP 会自动转义任何特殊字符——单引号、双引号、NULL——通过在它们前面添加反斜杠，以防止在数据库中使用字符串时出现问题。

实际上，PHP 可以在两个地方自动转义字符串：来自 Web 表单或请求的输入数据，或者来自任何返回任何数据的函数的自动转义。每个替换操作都由其自身的配置指令控制。输入数据的自动转义由 `magic_quotes_gpc` 指令控制，而任何函数的转义则由 `magic_quotes_runtime` 设置控制。

由于这两者都是关键操作，如果忽视可能会导致数据“污染”，PHP 提供了两个函数来快速确定每个设置的当前状态：`get_magic_quotes_gpc()` 用于输入数据，`get_magic_quotes_runtime()` 用于函数处理。这两个函数都不需要参数，如果设置已启用则返回 1，如果禁用则返回 0。运行这段代码：

```php
<?php

echo "Magic quotes GPC: " . get_magic_quotes_gpc() . "\n"
     "Magic quotes runtime: " . get_magic_quotes_runtime() . "\n";

?>
```

根据你的当前配置，你会看到类似以下内容：

```
Magic quotes GPC: 0
Magic quotes runtime: 0
```

## 动态更改配置

你现在可以在代码中实时检查配置设置和扩展属性，但如果某些地方不符合你的喜好，你会怎么做？通过一些内置的 PHP 函数，你可以更改 PHP 在某些情况下的行为。

### 不那么神奇的引号

如果你像我一样，可能不喜欢启用 `magic_quotes_runtime`，因为它会破坏所有函数的输出。虽然它可以被视为一种便利，但通常它只会碍事，并迫使你到处使用 `stripslashes()` 或 `addslashes()`。要更改此设置，可以使用 `set_magic_quotes_runtime()`。参数“1”开启自动替换；值“0”关闭它：

```php
<?php

// Turn on magic_quotes_runtime
set_magic_quotes_runtime(1);

// Turn off magic_quotes_runtime
set_magic_quotes_runtime(0);

?>
```

不幸的是，对于 `magic_quotes_gpc` 不能这么说——你不能在运行时更改其值（这一点稍后会有更多说明）。

### 移除时间限制

如果你发现自己处于脚本运行时间稍长于 PHP 允许的情况，你有两个选择：优化代码使其更快，或者告诉 PHP 更有耐心一些。也许你已经尽可能优化了代码，但默认的 30 秒超时仍然太快了。

是时候让 PHP 在超时之前再等待一会儿了。要做到这一点，使用 `set_time_limit()`，并简单指定允许脚本运行的秒数：

```php
<?php

// Set the timeout at one minute
set_time_limit(60);
?>
```

如果你无法准确猜测脚本需要多长时间，并且绝对确定没有无限循环，你可以通过将值设置为零来完全移除超时：

```php
<?php

// Will run forever if you're not careful
set_time_limit(0);
?>
```

当你使用 `set_time_limit()` 时，有两件事需要注意。首先，如果你的服务器在安全模式下运行 PHP，使用 `set_time_limit()` 将不起作用。你必须禁用安全模式，或者更改 `php.ini` 中的全局值。其次，每当调用 `set_time_limit()` 时，它会内部计时器重置为 0。如果脚本已运行了 15 秒，你将超时设置为 20 秒，它不会在再 5 秒后退出——它将计数器重置为 0，并重新计数 20 秒，总共 35 秒。

### 更改指令

如果你只想更改任何随机的运行时配置设置怎么办？要做到这一点，可以使用函数 `ini_set()`。使用 `ini_set()`，只需传入设置名称和新值即可。如果函数成功，它将返回旧值；如果不成功，它将返回 `false`。运行这段代码：

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

如果你决定不再想要更改后的值，可以使用 `ini_restore()` 来恢复脚本开始执行时的原始值：

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

在你开始随意更改设置之前，你需要意识到在脚本执行期间可以更改的设置是有限制的。如果你还记得之前展示 `ini_get_all()` 时，每个配置指令的数组返回了三个值：

```
... 
[allow_call_time_pass_reference] => Array
    (
        [global_value] =>
        [local_value]  =>
        [access]   => 6
    )
...
```

第三个值 `access` 指示该配置指令实际可以在哪里更改。提供给 `access` 的数字实际上是以下任何值的总和：

| 值 | 含义 |

| :--- | :--- |

| 1 | 该指令可以在用户脚本中设置。 |

| 2 | 该指令可以在 php.ini、.htaccess 或 httpd.conf 中设置。 |

| 4 | 该指令可以在 php.ini 或 httpd.conf 中设置。 |

| 7 | 该条目可以在任何地方设置。 |

在上面的示例中，`allow_call_time_pass_reference` 的 access 值为 6，意味着该指令只能在 `php.ini`、`.htaccess` 或 `httpd.conf` 中更改。需要记住的关键点是，如果设置的 access 值为 2、4 或 6，则不能在脚本执行期间更改。任何此类尝试都会自动返回 `false`。

## 自动化的版本与功能检查

了解在运行时评估和更改设置的各种方式固然有用，但试图在所有脚本或页面中确保系统和应用程序环境的一致性可能很棘手。一种可能的解决方案是将所有版本和扩展检查放在一个独立的脚本中，并在每个页面的顶部包含或引入该脚本。这种方法完全可行，但保持该验证脚本的更新很快就会变得繁琐。在下一节中，你将看到一个简单环境检查脚本的变体——它使用了一个易于修改的配置文件，并且只需几行代码即可调用。

这组脚本由三个主要的代码块和一个简单的配置文件组成。首先，查看这个示例中名为 `reqs.xml` 的配置文件：

```xml
<reqs>
    <packages>
        <package name="gd" />
        <package name="mysql" />
        <package name="pgsql" />
    </packages>

    <environment>
        <setting name="register_globals" value="off" />
        <php minversion="5.0.0" />
    </environment>
</reqs>
```

如果你有任何 XML 经验，你会认出这是一组简单的标签，它们被分组以建立站点配置。包裹在主封闭标签 `<reqs>` 内部，有两个主要部分。



第一部分 `<packages></packages>` 保存了你的应用程序所需的所有扩展的列表。每个扩展通过使用 `<package />` 空标签指定，其中 `name=""` 属性指定扩展的名称。扩展的名称应与前面提到的 `get_loaded_extensions()` 返回的名称相匹配。

第二部分包含定义特定应用程序设置的定义，这些设置默认在 `php.ini` 中找到，以及 PHP 本身的版本要求。每个 `<setting />` 标签都可以对应一个 PHP 运行时配置设置。`name=""` 属性与配置设置的名称匹配，`value=""` 属性保存了在 `php.ini` 中使用的任何值。`<php />` 标签允许你为应用程序指定版本要求——最小版本在 `minversion=""` 属性中指定，最大版本在相应的 `maxversion=""` 属性中指定（未显示）。

在这个 `reqs.xml` 示例中，GD、MySQL 和 PostgreSQL 扩展被列出的必需项，允许的 PHP 最小版本为 5.0.0，并且 `register_globals` 指令必须设置为 `off`。

> 在这个示例中指定最小版本 5.0.0 在技术上是不必要的——由于不同的对象模型，下面展示的结构体类结构将只在 PHP 5.0 及更高版本上运行。

## PHP 配置

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

这个类的第一部分应该相当直观。它首先声明类 `ConfigManager`，并声明三个公共属性：

```php
<?php

class ConfigManager
{
    public $configfile = 'reqs.xml';
    public $configtype = 'xml';
    public $errors;
}
?>
```

第一个属性 `configfile` 保存了你将要使用的配置文件的名称。该配置文件的默认值设置为 `reqs.xml`，因此除非你使用不同的文件名，否则不需要显式设置此属性。`configtype` 属性是指定配置类型的地方。在这种情况下，提供了默认值 `xml` 以表明你的配置采用 XML 格式。最后一个属性 `errors` 只是稍后处理过程中遇到的任何错误信息的占位符。

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

虽然这个构造函数中没有发生什么真正惊人的事情，但它确实允许在创建对象时传入配置文件和类型，并使用这些值设置相应的属性。

`ConfigManager` 中的最后一个是所有魔法发生的地方：

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

`processConfig()` 方法首先确定配置的类型，然后根据配置类型调用必要的代码并利用组件对象。目前，`processConfig` 中只指定了一种类型，即处理 XML 配置文件的类型。随着新配置处理器类型的创建，可以添加任意数量的额外案例。如果你希望将配置存储在数据库中，你可以设计自己的数据库配置处理对象，然后在此 `switch` 中添加一个调用新类中任何处理方法的案例。

注意，`XMLConfigProcessor` 的类文件是在此时包含的，而不是在文件开头或类中更早的位置。这样，只有当需要时才会解析该文件，有助于减少如果使用了不同配置类型时的多余处理。要使用 `XMLConfigProcessor`，只需实例化对象，将配置文件名传递给构造函数，最后调用处理配置的方法（本章后续会有更详细的说明）。

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

这部分相当直观——这里定义的四个方法将为任何配置类型的处理类规定通用功能。前三个方法——`checkExtensions()`、`checkPHP()` 和 `checkConfig()`——主要是作为实现类的内部方法，而最后一个方法 `process()` 旨在作为触发其他三个方法的主要公共方法。

配置检查工具中的最后一个文件是 `class.XMLConfigProcessor.php`，正如你可能从文件名猜测的那样，它处理 XML 配置文件：



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

    public function process()
    {
        // Check for needed libraries
        if (!$this->checkDeps() or
            !$this->checkConfigAccess())
        {
            $message = 'Failed to process XML file.\n';
            // ...
            return $this->message;
        }

        $this->xml = simplexml_load_file($this->xmlfile);

        if (! $this->checkPHP() or
            ! $this->checkExtensions() or
            ! $this->checkConfig())
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
        $ReturnValue = true;

        // Check for SimpleXML
        if (!extension_loaded('SimpleXML'))
        {
            $ReturnValue = false;
            $this->message .= "Warning: " .
                "SimpleXML extension not available.\n";
        }

        return $returnValue;
    }

    public function checkExtensions()
    {
        $ReturnValue = true;

        // Check for all listed extensions
        // ...
    }
}
?>
```

## PHP 配置

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
```

类名的开头相当普通——你包含接口文件，开始类，并定义一些属性。第一个属性 `XmlFile` 用于保存你的 XML 配置的**文件名**。第二个属性 `Message` 将用于捕获在处理文件时创建的任何错误消息。第三个也是最后一个属性 `Xml`，将保存一个由 PHP 的 SimpleXML 扩展创建的 XML 对象。在属性定义之后是一个简单的构造函数，如果在实例化期间传递了**文件名**，它会设置 `xmlFile` 的值：

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

    public function process()
    {
        // Check for needed libraries
        if (!$this->checkDeps() or
            !$this->checkConfigAccess())
        {
            return $this->message;
        }

        $this->xml = simplexml_load_file($this->xmlfile);

        if (!$this->checkPHP() or
            $this->checkExtensions() or
            !$this->checkConfig())
        {
            return $this->message;
        }
    }
```

构造函数之后的 `process()` 方法是从类外部调用的主方法。它包含了对类中所有其他组件方法的调用，这些方法检查 XML 配置文件中的各个要求和部分。

在 `process()` 的第一部分中，你会检查配置文件是否可访问，以及 PHP 安装是否具备该类正常运行的所有必要条件。如果其中任何一个检查失败，该方法应该终止并返回遇到的任何错误消息。

接下来，SimpleXML 扩展用于将配置文件的内容加载到一个 XML 对象中，准确地说是一个 `simplexml_element` 对象。这个 `simplexml_object` 可用于轻松遍历 XML 并根据需要提取标签和属性。

最后，`process()` 调用了来自 `ConfigProcessor` 接口的其余三个方法，以检查 PHP 版本、可用的扩展和配置设置。

你接下来遇到的方法是 `checkConfigAccess()`。此方法用于检查 XML 配置文件是否实际存在于文件系统上，如果存在，则进一步检查它是否可读。如果文件不存在或不可读，则向 `message` 属性添加一条错误消息。请注意，在方法的末尾调用了 `clearstatcache()`。`file_exists()` 和 `is_readable()` 的结果会被 PHP 缓存，因此在完成工作后清除结果缓存是个好主意，以防止后续出现错误的结果：



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

接下来是 `checkDeps()`。顾名思义，此方法检查类本身的依赖项。对于 `XMLConfigProcessor` 来说，唯一非标准的 PHP 要求是 `SimpleXML` 扩展的可用性。例如，如果你后来决定修改此类以使用 XML Parser 函数或 DOM XML 扩展，你需要在此方法中添加相应的检查。

为了检查 `SimpleXML`，你只需使用本章前面介绍的 `extension_loaded()` 函数即可。如果 `SimpleXML` 不可用，则将另一条错误消息添加到消息堆中：

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

现在该动手处理一下你的 XML 配置文件了。在 `checkExtensions()` 中，你需要做的第一件事是收集配置文件中列出的所有扩展。如前所述，每个包都在外层 `<packages></packages>` 标签中作为一个 `<package />` 标签列出。要获取所有这些包的列表，你需要使用 `SimpleXML` 的 `xpath()` 方法：

```php
public function checkExtensions()
{
    $returnValue = true;

    // Check for all listed extensions
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
}
```

`xpath()` 方法接收一个表示元素在文档层级中位置（即 Xpath 路径）的字符串，并返回一个 `simplexml_element` 对象的数组——在这种情况下，每个对象代表一个单独的 `<package />` 标签。

一旦你有了包标签的数组，你只需遍历它们，检查每个包是否可用。由于包名称存储在每个 `<package />` 标签的 `name=" "` 属性中，你可以使用方括号语法和字符串作为键，类似于数组键的方式访问其值。再次使用 `extension_loaded()` 函数来检查每个包，如果不可用，则向消息堆中添加一条错误消息。

从 `ConfigProcessor` 实现的下一个方法是 `checkPHP()`。此方法检查 PHP 本身的版本，以查看应用程序是否可以在该版本上运行。在方法开始时，你首先再次使用 `xpath()` `SimpleXML` 方法，以检查配置文件中是否存在 PHP 版本要求：



```php
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
    $settings = $this->xml->xpath('environment/setting');
    foreach ($settings as $setting) {
        $value = $setting['value'];
        // Convert boolean values to ini_get() values
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

        // Flatten name
        $name = (string) $setting['name'];

        // Check config value, set if needed
        if (!array_key_exists($name, $cfg) or
            ($value !=
               $cfg[$name]['local_value']) and
            ini_set($name, $setting['value']) === false)) {
            $returnValue = false;
            $this->message .= "Warning: " .
                              "not set to the required value of: "
                              . $name .
                              . $setting['value'] . ".\n";
        }
    }

    return $returnValue;
}
```

## 第 5 章

如果发现 PHP 版本要求，则用从 `xpath()` 返回的 `simplexml_elements` 数组中的第一个（也是希望唯一的）对象来替换该数组：

```php
// 扁平化元素数组
$phpreq = $phpreq[0];
```

PHP 版本检查可以分配两个属性：一个指定允许的最小 PHP 版本，另一个指定最大版本。对于最小和最大版本，你首先需要检查属性是否存在，然后使用内置的 `version_compare()` 函数，并结合 `$phpversion()` 函数。`version_compare()` 函数接受两个参数，每个参数都是一个“PHP 标准化”的版本号字符串，例如 5.0.4 或 5.0.5RC1。如果第一个参数较低，该函数返回 −1；如果第二个参数较低，它返回 +1；如果两个参数相等，它返回 0：

```php
// 检查最小版本
if ($phpreq['minversion'] and
    version_compare($phpversion(),
                    $phpreq['minversion']) < 0)
{
    $this->message = "Warning: " .
                     "PHP version is less than " .
                     $phpreq['minversion'] . ".\n";

    return false;
}
// 检查最大版本
if ($phpreq['maxversion'] and
    version_compare($phpversion(),
                    $phpreq['maxversion']) > 0)
{
    $this->message = "Warning: " .
                     "PHP version is greater than " .
                     $phpreq['maxversion'] . ".\n";

    return false;
}

return true;
```

现在你已经检查了所需的扩展，并调查了已安装的 PHP 版本是否受你的应用程序支持，你需要检查运行时配置，以确保环境与你编写代码时所针对的环境相匹配。在 `checkConfig()` 中，你首先使用 `ini_get_all()` 将所有配置设置收集到一个数组中：

```php
public function checkConfig()
{
    $returnValue = true;

    // 获取所有配置值
    $cfg = ini_get_all();
}
```

### PHP 配置

一旦你获取了所有当前的运行时设置，你就需要收集 XML 配置文件中所有 `<setting />` 标签值的列表。为此，你再次使用 SimpleXML 的 `xpath()` 函数：

```php
// 遍历设置元素
$settings = $this->xml->xpath('/environment/setting');
```

在你获取所有 `setting` 元素的数组后，你需要遍历它们，并检查运行时配置以查看它们是否匹配。在直接比较两者之前，你需要将 XML 配置文件中的每个值转换为与 `ini_get_all()` 的预期结果相匹配。通常在 `php.ini` 中设置值时，你可以使用几种不同的值来表示“true”或“false”。对于 true，你可以使用 `on`、`true`、`yes` 或 `1`；false 由 `off`、`false`、`no` 或 `0` 表示。如前所述，在使用 `ini_get()` 或 `ini_get_all()` 返回设置时，表示 on 或 true 的值将返回为 `1`，但 off 或 false 的值将返回为空字符串 `""`。为了确保 XML 配置值无论使用哪种 `php.ini` 指示都相匹配，你可以使用一个简单的 `switch`：



```php
foreach ($settings as $setting)
{
    $value = $setting['value'];
    // 将布尔值转换为 ini_get() 的值
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
        case '1':
            $value = '1';
            break;
    }
}
```

接下来，你获取配置变量的名称。由于像数组一样访问属性返回一个 `simplexml_element` 对象，你需要将其显式转换为 `string` 以便稍后与 `string` 值进行比较：

```php
// 扁平化名称
$name = (string) $setting['name'];
```

现在你已经拥有了 XML 配置文件中要求的设置的名称和值，你可以将其与运行时设置进行比较。首先，你检查该配置设置是否存在于运行时配置数组中，然后将其与 XML 文件中的值进行比较。再进一步，如果该设置存在但不匹配，请尝试使用 `ini_set()` 更改当前的运行时配置变量。如果设置不匹配 *且* 你无法在运行时更改该设置，系统将生成一条错误消息，并且该函数将返回 `false`：

```php
// 检查配置值，如需要则设置
if (!array_key_exists($name, $cfg) or
    ($value !=
        $cfg[$name]['local_value']) and
    ini_set($name, $setting['value']) === false))
{
    $returnValue = false;
    $this->message = "Warning: " .
        $name .
        " not set to the required value of: " .
        $setting['value'] . "\n";
}
return $returnValue;
}
```

现在你已经拥有了这个由类和配置文件组成的小型层次结构来检查运行时环境，你需要在脚本中实际调用它们。在下面的 test.php 代码中，你可以看到调用配置检查器是多么简单：

```php
<?php

// 检查 PHP 环境
require_once 'class.ConfigManager.php';
$cfg = new ConfigManager('reqs.xml', 'xml');
$cfg->processConfig();
```

你所需要做的就是包含主要的 `ConfigManager` 类文件，创建一个新的 `ConfigManager` 对象，在实例化时传递文件名和类型，并调用 `processConfig()` 方法来实际检查设置。

## 摘要

希望你现在已经熟悉了一些可以为你的应用程序注入生命力的不同的配置设置和函数。了解运行时设置的价值通常有助于避免难以诊断的 bug，而能够在运行时更改值可以使你的应用程序足够灵活，以应对各种配置。这种知识和力量，结合自动配置检查，应有助于使你的应用程序在面对不熟悉的服务器可能带来的未知麻烦时，尽可能具有“厚脸皮”（即健壮性）。

## 6 Apache 技巧

本章暂时不再谈论 PHP，转而讨论一些你可能不知道的 Apache 特性。你已经知道 Apache 是最流行和最强大的 Web 服务器，并且 PHP 是设计为与 Apache 协同工作的，但你可能不知道你可以扩展 Apache 本身，以使你的站点运行得更有效。秉承其开源的本性，有许多优秀的模块可供 Apache 使用，这些模块扩展了其功能，并为作为站点管理员的你提供了有用的特性。

本章讨论了其中三个模块。`Mod_rewrite` 允许你提供 URL 替换以适应站点更改，但如果你正确使用它，你可以用它来保护你的站点并使其对搜索引擎更友好。`Mod_speling` 帮助纠正访问你站点的访客无意中犯的拼写错误。`Mod_deflate` 允许你在向用户发送内容时对其进行压缩，从而为你节省带宽费用。`Mod_auth_mysql` 让你通过利用用户数据库的功能结合 Apache 的身份验证来加强你站点的防护。`Mod_ssl` 允许你加密流向你的 Web 服务器和从其流出的数据。最后，`mod_dav` 允许你将你的 Apache Web 服务器用作分布式文件存储库。

## URL 重写

如果你召集世界上所有的 Web 开发人员和管理员，让他们列出可以与 Apache 一起使用的最重要模块，那么 `mod_rewrite` 一定会出现在那个列表中——这是有充分理由的。

`Mod_rewrite`，对于不熟悉的人来说，是一个提供 URL 重写功能的 Apache 模块。虽然这听起来可能很简单，但实际上 `mod_rewrite` 是 Apache 模块的瑞士军刀。你可以用 `mod_rewrite` 做什么？除了显而易见的简单 URL 重写之外，`mod_rewrite` 让你能够保持查询字符串输入的安全，使你的站点对搜索引擎友好，使你的 URL 对用户友好，在重新构建后保留“旧”URL，并阻止盗链。你会发现 `mod_rewrite` 很快就会不仅仅是一个简单的 URL 更改机器人。

# 第 6 章

### 启用 mod_rewrite

在着手配置 mod_rewrite 之前，你需要做的第一件事是检查它是否已经安装。在命令行中输入：

```
/path/to/httpd -l
```

*显然，请替换为你自己 Apache 的 httpd 路径。*

如果你看到 `mod_rewrite.c` 被列出，说明它已经编译进了 Apache。如果没有，请检查它是否作为 Apache 的动态模块存在：

```
ls /path/to/apache/modules/
```

如果文件列表中存在 `mod_rewrite.so`，则可以通过稍后在本节中展示的 `httpd.conf` 文件的少量调整，让 Apache 将其作为模块加载。如果它既没有编译进 Apache，也不作为共享对象可用，你可以使用操作系统提供的任何包管理系统来安装它；或者，如果你是更喜欢动手的类型，你可以自己重新编译 Apache 以包含 mod_rewrite。

在 Apache 中启用功能时，通常有两种选择：将其静态构建到 Apache 二进制文件中，或者将模块编译为可加载的共享对象。当将模块静态构建到 Apache 中时，它们无需额外的配置指令即可使用，但无论你是否需要该模块，只要 Apache 在运行，该模块就会一直处于激活状态并消耗内存。将模块构建为可加载的共享对象可以保持你的 Apache 二进制文件精简，不包含任何你可能需要也可能不需要的“*可选*”项，但需要在 `httpd.conf` 中手动配置。两种方法都可以接受，但如果你不确定选择哪种，共享模块路径因其灵活性而成为一种流行的选择。

在从源码构建 Apache 时，若要静态构建 mod_rewrite，请确保你的 configure 文件包含 `--enable-rewrite`，例如：

```
./configure \
--enable-rewrite \
# ...以及你使用的任何其他 configure 设置
```

如果你选择了动态模块路径，只需在启用 mod_rewrite 的行末尾添加 =shared：

```
./configure \
--enable-rewrite=shared \
# ...以及你使用的任何其他 configure 设置
```

然后，只需简单地制作并安装服务器到你的系统即可。如果你静态构建了 mod_rewrite，可以通过重新运行 `httpd -l` 来确认你的重新配置是否成功。如果 `mod_rewrite.c` 出现，说明它已成功添加到 Apache 二进制文件中。

相反，如果你选择了动态模块，首先检查它是否实际存在于 Apache 模块目录中，作为一个名为 `mod_rewrite.so` 的文件。

```
ls /path/to/apache/modules/
```

假设一切顺利，且 `mod_rewrite.so` 存在于模块目录中，你需要在 `httpd.conf` 中启用它，方法是取消注释现有行或添加类似以下的新行：

```
LoadModule rewrite_module modules/mod_rewrite.so
```

> 不要对任何静态编译进 Apache 的模块使用 `LoadModule` 行——仅限动态共享对象。对静态模块使用 `LoadModule` 只会生成错误。



在对 `httpd.conf` 完成所有必要的更改后，重启 Apache。既然你已成功安装了 `mod_rewrite`，你需要查看用于利用 `mod_rewrite` 的不同配置设置。

### RewriteRule

`mod_rewrite` 提供了一组配置指令，可以提供广泛的重写功能，从非常简单的重定向到复杂的多规则模式匹配替换。每个重写 URL 的核心都是 `RewriteRule` 指令。

#### RewriteRule 用法

无论你的重写需求多么复杂，你至少需要一个 `RewriteRule` 来执行转换。`RewriteRule` 指令的基本格式如下：

```
RewriteRule pattern substitution [flag(s)]
```

`RewriteRule` 的行为类似于 PHP 的 `preg_replace` 函数：它接受一个正则表达式模式，将其与传入的 URL 匹配，然后使用你定义的规则为 URL 提供替换内容。

在构建用于匹配的正则表达式模式时，你可以使用以下标记：

| 模式 | 含义 |
| :--- | :--- |
| `^` | 脱字符号表示行或字符串的开始。 |
| `$` | 美元符号表示行或字符串的结束。 |
| `.` | 点号匹配任何单个字符。 |
| `(a\|b)` | 使用“管道”字符作为逻辑“或”，模式 `(a\|b)` 匹配 `a` 或 `b`。 |
| `(\u002e\u002e\u002e)` | 括号将部分分组为子匹配。 |
| `[abc]` | 在括号内列出值匹配列表中或范围内给定的任何值。模式 `[abc]` 匹配单个字母 `a`、`b` 或 `c`，而模式 `[a-z]` 匹配从 `a` 到 `z` 的任何小写字母。 |
| `[^abc]` | 在范围开始处使用脱字符号匹配范围中*未*列出的任何值。模式 `[^abc]` 匹配除 `a`、`b` 或 `c` 以外的任何字符；模式 `[^a-z]` 匹配除小写 `a` 到 `z` 以外的所有内容。 |
| `a?` | 问号匹配前一个字符恰好零次或一次。 |
| `a*` | 星号指示 Apache 匹配前一个字符零次或多次——没有限制。 |
| `a+` | 使用加号匹配前一个字符一次或多次——没有限制。 |
| `a{n}` | 花括号内的单个数值匹配前一个字符恰好指定的次数。 |
| `a{n,}` | 单个数值后跟逗号匹配前一个字符至少 n 次，但可能更多。 |
| `a{n,m}` | 花括号中的两个数值指定至少 n 次匹配，但最多 m 次匹配。 |
| `!(pattern)` | 逻辑“非”由模式前的感叹号表示。用于在 URL 不匹配给定模式时应用规则。 |
| `\char` | 反斜杠作为转义字符，使你能够匹配通常是正则表达式标记的字符，例如 `\.`, `\*`, `\[`, `\^` 等。 |
| `\d` | 匹配任何十进制数字。 |
| `\w` | 匹配任何“单词”字符——通常是任何字母、数字或下划线字符。 |

例如，你最近可能用较新的、较新的版本替换了网站的一个旧部分，并使用了不同的 URL。为了自动将旧结构中的任何 URL 重定向到新位置的索引，你可以使用类似以下内容：

```
RewriteEngine On
RewriteBase /
# 将旧目录的请求重写到新索引
RewriteRule ^olddirectory/ newdirectory/index.php [R,NC,L]
```

此规则指示 Apache 对 `olddirectory/` 文件夹中任何文件的所有请求都使用 `newdirectory` 文件夹中的 `index.php` 进行响应。末尾的标志指定重定向到新 URL，匹配时忽略大小写，并停止处理可能匹配请求 URL 的其他规则——这些标志将在本章后续部分介绍。

使用 `mod_rewrite` 的更常见用途之一是提供对搜索引擎友好——以及对人工输入友好——的 URL，同时仍然使用标准的带有 HTTP GET 参数附加在请求中的 PHP 文件。为了帮助说明这种场景，请从创建以下 PHP 文件开始：

```
<?php
$category = '';
$item = '';
if (isset($_GET['cat']))
{
    $category = $_GET['cat'];
}
if (isset($_GET['item'])) { 
  $item = $_GET['item']; 
} 
echo "Category: " . $category . "<br />\n" . 
"Item: " . $item . "<br />\n";
?>
```

将此文件保存为网站根文件夹中的 `catalog.php`。

通常，如果你想调出此文件并让它识别给定的类别或项目值，你必须提供查询字符串中的值，如下所示：

```
http://www.domain.com/catalog.php?cat=categoryvalue&item=itemvalue
```

不幸的是，一些搜索引擎不会索引像上面这样的带有动态 URL 的页面。此外，指定每个变量的额外语法对于任何手动输入 URL 的人来说都可能是一种负担。为了解决这种情况，你可以使用 `mod_rewrite`。在你的 `catalog.php` 文件所在的目录中的 `.htaccess` 文件中（如果需要，也可以在服务器的 `httpd.conf` 文件中）添加以下指令：

```
RewriteEngine On 
# 将 /category/item/ 重写为 catalog.php 
RewriteRule ^\w+/\w+/?$ catalog.php?cat=$1&item=$2
```

> 要在目录级配置文件（`.htaccess`）中使用 `mod_rewrite` 指令，必须在 `httpd.conf` 中为目录启用 `Options FollowSymLinks` 或 `Options SymLinksIfOwnerMatch` 指令。

现在，由于 `mod_rewrite` 的神奇魔力，你可以使用 URL 中的目录而不是查询字符串来访问类别和项目记录：

```
http://www.domain.com/categoryvalue/itemvalue/
```

请注意，前面 URL 中引用的对应目录实际上并不存在——`mod_rewrite` 拦截请求并将其转换为带有查询字符串的 PHP 请求，然后通过 PHP 引擎进行解析。另一件需要记住的事情：如果前面的目录实际存在，且此处显示的 `RewriteRule` 处于活动状态，Apache 仍将完全忽略真实路径并按计划进行 URL 重写。

查看 `mod_rewrite` 配置中的行，你从一个简单的声明开始：

```
RewriteEngine On
```

为了使用 `mod_rewrite`，你必须通知 Apache 你希望在给定的配置区域（例如 `.htaccess` 文件或 `httpd.conf` 中的 `<Directory>` 部分）启用该模块。`RewriteEngine` 接受 `On` 或 `Off` 作为其值。

下一个关键行只是一个用于匹配传入 URL 的正则表达式，以及用于替代它的新 URL：

```
# 将 /category/item/ 重写为 catalog.php 
RewriteRule ^\w+/\w+/?$ catalog.php?cat=$1&item=$2
```

### 第6章

该模式寻找两级目录请求，使用 `\w` 模式仅为每个目录匹配有效的“单词”字符。然后，它将这两个目录的值分别用作 PHP 脚本中的分类和项目编号。与 PHP 的 PCRE 语法一样，你可以使用以 `$` 为前缀的反向引用（backreferences）来指代原始模式中的子匹配项。反向引用是一种简单的方法，可以直接将前一个模式的子匹配项包含在替换字符串中。再次查看该规则：

```
# Rewrite /category/item/ to catalog.php
RewriteRule   ^(/\w+)/(\w+)/?$  catalog.php?cat=$1&item=$2
```

在匹配 URL 的正则表达式中，恰好定义了两个子匹配项：这两个“单词”字符的分组，指示目录。在替换字符串中，反向引用 `$1` 和 `$2` 被用来自动对应地包含第一个和第二个子匹配项的值。反向引用简单地从 1 开始计数，这对应于第一个子匹配项。

你还能用简单的 `RewriteRule` 玩出什么花样？实际上，你可以将其作为 PHP 脚本的一种基本类型检查层。在某些情况下，你可能会从查询字符串变量中获取一个数字，例如页码或项目编号。如果你想绝对确保你使用的是数字，而不是更恶意的东西——比如 SQL 注入攻击——你有两个选择。

第一种也是最常用的方法是在 PHP 脚本中添加额外的代码，以实际检查 `$_GET` 参数是否确实包含一个数字。例如，你可能会看到这样的 URL：

```
http://www.domain.com/article.php?page=2
```

像这样的 URL 通常出现在分页内容中，一般在页面导航链接中。在加载指定文章页面的某处代码中，你可能会看到以下内容：



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

// 以此类推....
?>
```

上述代码首先检查特定的 `$_GET` 值（在本例中为 `'page'`）是否存在，然后检查传递的值是否确实是数字——如果不是，则赋值为默认值 `1`。

这种类型检查是个好主意，有助于保护你的 PHP 脚本免受那些想要破坏你网站的不肖之徒（script kiddies）的攻击。不幸的是，这可能会变得有些繁琐，因为你的 PHP 脚本需要检查值是否已设置，以及它是否确实是一个数字。

使用 `mod_rewrite`，你可以从 PHP 代码中消除类型检查——你要做的只是确保模式仅匹配数字值：

# Apache 技巧

```
RewriteEngine On
# 确保 page 的值仅为数字
RewriteRule ^article/([0-9]*)/? article.php?page=$1
RewriteRule ^article/[^0-9]*/? article.php?page=1
```

第一条 `RewriteRule` 检查任何形如 `article/page/` 的有效 URL，并将给定的请求转换为对该 PHP 脚本的调用。第二条 `RewriteRule` 设置为捕获所有请求文章但提供了无效页码值的格式错误的 URL。任何此类请求都会自动分配为该文章的第一页。

在上一组 `RewriteRule` 中，有两点需要注意。首先，两条规则是按顺序处理的；处理过程不会在第一条规则处停止，而是继续处理所有给定的规则。其次，重定向到 `article.php` 脚本是在内部处理的——根本不会向客户端发送 HTTP 重定向/移动状态码。为了改变这些默认行为，你可以在每条规则的末尾使用一组标志（flags）。

## RewriteRule 标志

为了控制 `mod_rewrite` 处理和执行每条 `RewriteRule` 的方式，你可以添加一组 15 种不同的标志，放在每条规则之后。标志包含在方括号内，可以提供多个标志，以逗号分隔列表的形式——全部位于同一对方括号内。例如：

```
# Rewrite /category/item/ to catalog.php
RewriteRule ^(\w+)\\/(\w+)\\/? catalog.php?cat=$1&item=$2 [NC, R,L]
```

### nocase | NC

类似于 PHP PCRE 语法中的 `i` 标志，`nocase` 标志使模式不区分大小写。例如，以下两个模式是相同的：

```
RewriteRule ^([A-Za-z-]+)/? catalog.php?cat=$1
RewriteRule ^([a-z]+)/? catalog.php?cat=$1 [NC]
```

### redirect | R [=code]

通常，`mod_rewrite` 在重写 URL 时使用内部的 Apache 重定向，这种重定向对用户是隐形的。如果你想要执行正式的重定向，并附带 HTTP 状态码，你可以使用 `redirect` 或 `R` 标志。默认情况下，`redirect` 标志发送 HTTP 302 Moved Temporarily 代码，如下面规则所示：

```
RewriteRule ^article/(\d+)\\/? article.php?page=$1 [R]
```

如果你希望将状态码更改为 HTTP 301 Moved Permanently，或者 300 到 400 之间的任何其他状态码，你只需将代码添加到 `redirect` 标志的末尾：

```
RewriteRule ^article/(\d+)\\/? article.php?page=$1 [R=301]
```

### forbidden | F

类似于 `redirect` 标志，使用 `forbidden` 标志会立即向客户端发送 HTTP 403 Forbidden 响应。当同一条规则中同时存在 `redirect` 标志和 `forbidden` 标志时，`forbidden` 标志将具有优先级（重定向将被忽略，发送 403）。

### gone | G

另一个 HTTP 状态码控制标志，`gone`，发送 HTTP 410 Gone 响应，以告知客户端该页面不再存在。当组合使用时，`gone` 标志的优先级高于 `redirect` 标志，但低于 `forbidden` 标志。

### last | L

要在找到成功匹配后停止 `RewriteRules` 的处理，你可以使用 `last` 标志。在之前处理文章页码的示例中，即使第一条规则匹配成功，规则处理仍会继续到第二条规则（但不会找到匹配项）。要在第一条规则匹配后停止处理，你可以简单地使用 `last` 标志：

```
RewriteEngine On
# 确保 page 的值仅为数字
RewriteRule ^article/([0-9]*)/?  article.php?page=$1 [L]
RewriteRule ^article/([0-9]*)/?  article.php?page=1  [L]
```

### next | N

`next` 标志在规则列表的开头重新开始重写过程。当规则被重新处理时，匹配的 URL 不再是来自客户端的原始请求，而是在使用 `next` 标志时所处的内部重写 URL。例如：

```
RewriteRule  ^article/(\d+)/?  article.php?page=$1
RewriteRule  ^catalog/(\w+)/?  catalog.php?cat=$1  [N]
RewriteRule  ^catalog/(\w+)/(\w+)/? catalog.php?cat=$1&item=$2
```

在此示例中，如果调用了匹配第二条规则的 URL，例如 `http://localhost/catalog/stuff`，重写过程将在此处停止处理，并自动使用新的替换 URL `catalog.php?cat=stuff` 在规则集开头重新开始。该替换 URL 随后本身将经过整个规则集的过滤。

使用 `next` 标志时应谨慎，因为可能会出现无限循环。

### chain | C

如果你希望将一组规则视为一个相关的整体，类似于 PHP 中的 `try...catch` 语法，你可以使用 `chain` 标志。使用 `chain` 标志时，如果规则匹配，处理将按预期继续并忽略 `chain` 标志。如果规则不匹配且存在 `chain` 标志，则所有通过 chain 链接在一起的后续规则将作为一个整体块被跳过。例如，以下一组规则如果在第一条规则不匹配的情况下，将跳转到最后一行规则：

```
RewriteRule  ^article/(\d+)/?  article.php?page=$1 [C]
RewriteRule  ^catalog/(\w+)/?  catalog.php?cat=$1  [C]
RewriteRule  ^catalog/(\w+)/(\w+)/? catalog.php?cat=$1&item=$2

# 如果上述任何一条规则不匹配，则跳至此规则
RewriteRule  ^article/(\d+)/?  error.php
```

### skip | S=number

此标志允许你在当前规则匹配时跳过接下来的指定数量的规则。虽然 `skip` 标志的行为与 `chain` 标志相似，但其表现完全相反——`skip` 在匹配成功时跳转；`chain` 在匹配失败时跳转。

### type | T=mime-type

如果你想覆盖文档发送的 MIME 类型，可以使用 `type` 标志。例如，如果你有一批 `.xhtml` 文件，希望使用正确的 XHTML MIME 类型（`application/xhtml+xml`）而不是 `text/HTML` 来提供它们，可以使用以下代码：

```
RewriteRule ^.+\.xhtml$ - [T=application/xhtml+xml]
```

### cookie | CO=name:value:domain[:lifetime[:path]]

`cookie` 标志，正如你可能推断的那样，会在客户端浏览器上设置一个 `cookie`。三个必需字段——`name`（名称）、`value`（值）和 `domain`（域）——分别指定 cookie 的名称、cookie 的值以及设置 cookie 的域。可选的 `lifetime`（生命周期）参数代表 cookie 的生存时间，以分钟为单位。`path`（路径）参数设置 cookie 的路径。

例如，如果你想设置一个名为 `previous visit` 的 cookie，以表明用户之前访问过主页（因此不应再被闪屏困扰），可以使用此代码：

```
RewriteRule ^index\.php$ - [CO=prevvisit:true:domain.com]
```

### env | E=var:value



`env`标志允许你将环境变量`var`设置为提供的值。该值也可以包含正则表达式反向引用（`$1`和`$n`），以便进行更复杂的变量控制。可以在一组标志中设置多个环境变量——只需像标志列表中的其他项一样用逗号分隔即可。

### `qsa` | `append` | `QSA`

在使用`mod_rewrite`的大多数情况下，当你执行重写时，提供给原始 URL 的任何查询字符串内容都会被丢弃。如果你想保留该信息而不是丢弃它，可以使用`qsa|append`标志。使用此标志时，重写引擎只是获取原始查询字符串并将其附加到重写中提供的任何新查询字符串之后。例如：

```
RewriteRule ^index\.php$ index.php?foo=bar [QSA]
```

此规则将使用 URL `index.php?moo=cow`修改`index.php`文件，使其变为`index.php?foo=bar&moo=cow`。

如果原始 URL 中的查询字符串参数与`RewriteRule`中的参数同名，则原始值具有优先级。

### `noescape` | `NE`

当`mod_rewrite`执行转换时，它会竭尽全力确保重写 URL 中的特殊字符在执行任何内部或外部重定向之前都经过转义。例如：

```
RewriteRule  ^some dir/?  index.php?page=foo\%3b  [R]
```

根据此规则，Apache 会按要求重定向`some dir/`目录，并且`$_GET`中`page`的值将是`foo\%3b`的“安全”转义值——`mod_rewrite`转义了`\%3b`的值，而不是将其替换为分号。要告诉`mod_rewrite`避免任何自动转义，你可以使用`noescape`标志：

```
RewriteRule  ^some dir/?  index.php?page=foo\%3b  [R, NE]
```

根据此规则，`page`查询字符串参数的新值将是`foo;`。

### `passthrough` | `PT`

当你希望将`mod_rewrite`与其他提供类似 URL 处理功能的 Apache 模块（如`mod_alias`）结合使用时，请使用`passthrough`标志。例如，如果你想将`/foo`重写为指向`/bar`，然后使用`mod_alias`将`/bar`转换为`/baz`，你可能会尝试以下方法：

```
RewriteRule  ^/foo  /bar
Alias  /bar  /baz
```

不幸的是，由于 Apache 内部处理 URL 的方式，按原样编写它是行不通的。要使其生效，请添加`passthrough`标志：

```
RewriteRule  ^/foo  /bar  [PT]
Alias  /bar  /baz
```

一个通用的经验法则是，如果你使用多个 URL 转换模块来处理文件，请使用`passthrough`。

### `nosubreq` | `NS`

使用`nosubreq`标志强制重写引擎在请求实际上是内部子请求时跳过某条规则。当同时使用 PHP 和 Apache 时，很少有真正需要此标志的情况。然而，在某些 CGI 脚本实例中，这个标志会发挥作用。更多信息，请参阅 Apache 手册中关于`RewriteRule`的部分：[http://httpd.apache.org/docs/2.0/mod/mod_rewrite.html#rewriterule](http://httpd.apache.org/docs/2.0/mod/mod_rewrite.html#rewriterule)。

### `proxy` | `P`

`proxy`标志告诉重写引擎立即停止处理规则集，并强制请求通过 Apache 代理模块`mod_proxy`。

鉴于对`RewriteRule`的关注，你可能会认为它是`mod_rewrite`背后的主要推动力。实际上，它最好的角色是与`RewriteCond`组成的动态双人组的一部分。

## `RewriteCond`

`RewriteCond`指令的行为非常类似于 PHP 的`if ( )`语句：它将一个字符串与模式或条件进行测试。如果输入匹配该模式或字符串，则紧跟在`RewriteCond`指令之后的`RewriteRule`将被处理。`RewriteCond`的一般格式如下：

`RewriteCond TestString CondPattern`

`TestString`是你评估的字符串，而`CondPattern`是要检查的正则表达式或比较值。

### `RewriteCond`用法

`RewriteCond`最常见的用法是将输入字符串与正则表达式进行匹配，类似于`RewriteRule`。然而，当你使用`RewriteCond`时，你可以访问大量服务器变量，因此你的输入字符串可以比简单的文件名匹配更复杂。下表列出了可在`RewriteCond`中使用的服务器变量。

以下是 HTTP 头部变量：

| VARIABLE | DESCRIPTION |
|---|---|
| HTTP_USER_AGENT | 列出浏览器识别信息的字符串，例如：Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1;, NET CLR 1.1, 4322) |
| HTTP_REFERER | 用户访问的前一个页面，由其浏览器报告 |
| HTTP_COOKIE | 请求中的一部分 Cookie 字符串 |
| HTTP_FORWARDED | 如果请求由代理服务器处理，则包含任何转发信息 |
| HTTP_HOST | 请求中引用的主机名 |
| HTTP_PROXY_CONNECTION | HTTP Proxy-Connection 标头的内容 |
| HTTP_ACCEPT | 返回 Accept 标头的值；指示浏览器可以处理何种类型的内容，以及哪些类型具有优先权 |

以下是请求变量：

| VARIABLE | DESCRIPTION |
|---|---|
| REMOTE_ADDR | 请求文件的用户的 IP 地址。 |
| REMOTE_HOST | 请求文件的用户的主机名。 |
| REMOTE_USER | 请求文件的人员的用户名，由浏览器报告。 |
| REMOTE_IDENT | 为识别目的设置的变量。可能包含用户名。 |
| REQUEST_METHOD | 请求中使用的方法，例如 GET 或 POST。 |

## 第 6 章

| VARIABLE | DESCRIPTION |
|---|---|
| SCRIPT_FILENAME | 请求文件的完整本地路径。 |
| PATH_INFO | 添加到 URL 末尾的任何额外路径信息。 |
| QUERY_STRING | 请求的任何查询字符串或 GET 参数，通常指带参数的 GET 请求中问号后面的所有内容。 |
| AUTH_TYPE | 用于验证用户身份的认证类型。 |

以下是服务器变量：

| VARIABLE | DESCRIPTION |
|---|---|
| DOCUMENT_ROOT | 网站的根文件夹，由 DocumentRoot 指令指定 |
| SERVER_ADMIN | 服务器管理员的电子邮件地址，使用 ServerAdmin 指令指定 |
| SERVER_ADDR | 服务器的主机名或 IP 地址 |
| SERVER_PORT | 请求中指定的服务器端口号 |
| SERVER_PROTOCOL | 请求协议的名称和版本，例如 HTTP/1.1 |
| SERVER_SOFTWARE | 服务器软件名称（Apache） |

以下是时间变量：

| VARIABLE | DESCRIPTION |
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

| VARIABLE | DESCRIPTION |
|---|---|
| API_VERSION | Apache 模块 API 的版本（与 Apache 版本号不同，但密切相关）；主要用于模块开发（内部使用） |
| THE_REQUEST | 完整的 HTTP 文件请求字符串，包括方法、请求的文件和使用的 HTTP 版本 |
| REQUEST_URI | HTTP 请求中请求的资源 |
| REQUEST_FILENAME | 匹配 HTTP 请求的项目的完整本地文件系统路径 |
| IS_SUBREQ | 正在处理的请求是否为内部子请求；如果请求是子请求，值为 "true"，否则为 "false" |
| HTTPS | 值为 "on" 表示正在使用 SSL/TLS，"off" 表示未使用 |



要使用该列表中的任何变量，你需要将变量名放在花括号中，并以前缀百分号开头，如下所示：

```
%(SCRIPT_FILENAME)
```

要查看 `RewriteCond` 的实际操作，首先重写一条 `RewriteRule` 以利用 `RewriteCond`。旧规则如下所示：

```
# 将 /category/ 重写为 catalog.php
RewriteRule ^(\w+)?/ catalog.php?cat=$1&item=$2
```

要使用 `RewriteCond` 与 `RewriteRule` 结合来实现相同的目标，请使用以下方法：

```
# 将 /category/item/ 重写为 catalog.php
RewriteCond %(SCRIPT_FILENAME) /(\w+)/?(\w+)/?$
RewriteRule .+ catalog.php?cat=$1&item=$2
```

注意服务器变量 `SCRIPT_FILENAME` 是如何用作测试输入字符串的。结合使用这些服务器变量将 `RewriteCond` 与 `RewriteRule` 结合起来，你可以想出一些有趣的组合。以下示例检查用户浏览器是否可以接受 XHTML MIME 类型，如果是，则更改为 `.html` 文件发送的 MIME 类型头：

```
RewriteCond $(HTTP_ACCEPT) application/xhtml+xml
RewriteRule .+.html$ - [T=application/xhtml+xml]
```

`RewriteCond` 的另一个有用功能是能够多行链接。当在一行中列出多个 `RewriteCond` 语句时，它们都像编程中的 AND 一样被处理——只有当所有 `RewriteCond` 匹配都返回 true 时，末尾的 `RewriteRule` 才会被处理。上一组规则可以使用多个 `RewriteCond` 语句重写，如下所示：

```
RewriteCond $(HTTP_ACCEPT) application/xhtml+xml
RewriteCond %(SCRIPT_FILENAME) \.html$
RewriteRule .+ - [T=application/xhtml+xml]
```

除了标准的字符串与正则表达式比较之外，你实际上可以使用 `RewriteCond` 进行简单的比较和系统检查条件。要将输入字符串与另一个简单字符串进行比较，你可以使用以下条件模式：

```
<CondPattern
>CondPattern
=CondPattern
```

## 第 167 页

这些检查分别判断输入字符串是否小于、大于或等于 `CondPattern`。例如，如果你想让网站的特定区域在特定年份之后被禁止访问，你可以使用以下代码：

```apache
RewriteCond %{TIME_YEAR} >2005
RewriteRule .* - [F]
```

除了这些简单的比较运算符外，你还可以访问另外六个条件检查，用于评估文件和目录的状态：

| 比较运算符 | 含义 |
| --- | --- |
| -d (is directory) | 测试是否存在与测试字符串匹配的目录 |
| -f (is regular file) | 测试是否存在与测试字符串匹配的常规文件 |
| -s (is regular file with size) | 测试是否存在与测试字符串匹配的常规文件，且其大小大于 0 字节 |
| -l (is symbolic link) | 测试是否存在与测试字符串匹配的象征性链接 |
| -r (is existing file via subrequest) | 测试在考虑了服务器所有访问控制后，常规文件是否可访问；使用内部子请求来执行检查（会影响性能） |
| -U (is existing URL via subrequest) | 测试在考虑了服务器所有访问控制后，URL 是否可访问；使用内部子请求来执行检查（会影响性能） |

例如，为了检查图像是否存在并且确实包含一些数据，你可以使用以下代码：

```apache
RewriteCond %{REQUEST_FILENAME} \.jpg$
RewriteCond %{REQUEST_FILENAME} !-s
RewriteRule .* - [G]
```

第一个条件检查是否调用了 `.jpg` 文件，第二个条件实际检查文件是否不存在或大小为 0 字节。注意在 `-s` 条件模式前使用了感叹号。`RewriteCond` 中使用的任何条件模式都可以加上感叹号前缀，从而对其取反——这与 PHP 条件中感叹号的用法相同。

### RewriteCond 标志

为了进一步控制 `RewriteCond`，提供了一些类似于 `RewriteRule` 标志的标志。

#### nocase|NC

与用于 `RewriteRule` 的同名标志一样，`nocase` 指定要评估的正则表达式是不区分大小写的。

#### ornext|OR

多个 `RewriteCond` 指令的默认链接方法是使用逻辑 AND。如果使用 `ornext` 标志，则两个连接的 `RewriteCond` 将通过逻辑 OR 进行比较。

虽然 `RewriteRule` 和 `RewriteCond` 指令提供了 `mod_rewrite` 的大部分功能，但仍有一些其他关键指令可以帮助你控制重写并解决问题。

### RewriteBase

在大多数情况下，你的网站 URL 不会与你的物理文件系统布局相匹配。你网站的根目录几乎永远不会位于本地文件系统的根目录（`/`）。在 Apache 服务器的正常操作中，这通常不是问题；但在使用 `RewriteRule` 时，这会变得非常棘手。`RewriteBase` 允许你为一组 URL 重写指定基础路径或前缀路径。

为了完全理解 `RewriteBase` 的原因，请查看以下用于重写一组简单文件的示例规则集：

```apache
RewriteEngine On
RewriteRule ^foo\.html$ bar.html [R]
```

假设你的 Web 根目录由本地文件系统 `/www` 文件夹提供（即，你的 `DocumentRoot` 设置为 `/www`）。如果你尝试在目录级访问文件（`.htaccess`）中使用前面的规则，实际上会导致请求被错误地重写——你得到的不是预期的 `http://www.domain.com/bar.html` 文件，而是 `http://www.domain.com/www/bar.html`。这是为什么？以下是 Apache 内部发生情况的简化版本：

```text
请求: /www/foo.html (本地物理路径)

重写过程:
/www/foo.html -> foo.html (目录前缀被移除)
foo.html -> bar.html (应用 RewriteRule)
bar.html -> /www/bar.html (重新应用目录前缀)
/www/bar.html -> http://www.domain.com/www/bar.html
               (将域前缀应用于 URL，发送给浏览器)
```

为了解决这个问题，你只需在规则集中添加一个 `RewriteBase` 语句：

```apache
RewriteEngine On
RewriteBase /
RewriteRule ^foo\.html$ bar.html [R]
```

### RewriteLog

为了对 `mod_rewrite` 的实际运行情况有一手了解，请尝试 `RewriteLog` 指令。你可以使用 `RewriteLog` 指定一个日志文件，内部重写处理过程的实时记录将被发送到该文件。

## 第 6 章

为了在其他默认 Apache 日志文件旁边启用重写日志，请使用以下内容：

```apache
RewriteLog "logs/rewrite_log"
```

在指定重写日志的路径时，你可以使用绝对路径和相对路径。如果使用相对路径，它将相对于 `httpd.conf` 中的 `ServerRoot` 设置。

请注意，`RewriteLog` 指令是按服务器应用的，因此必须放置在 `httpd.conf` 内的服务器配置或虚拟主机容器中——它不允许在 `<Directory>` 部分或 `.htaccess` 文件中使用。

### RewriteLogLevel

为了控制重写日志记录详略程度，你可以使用 `RewriteLogLevel` 指令。给定一个 0 到 9 的数字，其中 9 是最详细的，你可以控制记录多少内部处理。设置为 0 会完全禁用日志记录，而大于 2 的任何值应仅用于调试——在较高设置下它可能会拖慢 Apache 的速度。

如果你想深入了解 `mod_rewrite` 的工作原理，请查看 Apache 在线手册中的 `mod_rewrite` 部分：

```text
http://httpd.apache.org/docs-2.0/mod/mod_rewrite.html
```

### URL 拼写检查



有了 `mod_rewrite` 的强大功能，对于格式错误或更改的 URL，你几乎没有无法处理的情况，但拼写错误呢？当然，你可以为网站中的每个文件列出大量的可能拼写错误，并编写大约一千条 `RewriteRule`，但这并不是必须的。为了减轻你“简单”拼写检查的负担，Apache 附带了 `mod_spelling` 模块（是的，它确实只有一个“T”）。使用 `mod_spelling`，你可以将处理 URL 拼写错误的任务交给 Apache，它会尽最大努力确定用户 `intended` 要加载的文件。

要使用 `mod_spelling`，首先检查它是否已经作为静态构建模块对 Apache 可用：

```bash
/path/to/httpd -l
```

如果你在列表中没有看到 `mod_spelling.c`，请检查 Apache 模块目录中的 `mod_spelling.so`：

```bash
ls /path/to/apache/modules
```

如果你既找不到静态库也找不到动态模块，你需要自己构建它们。与以前一样，你可以选择将模块静态构建到 Apache 本身，或将其构建为动态模块。

要构建静态版本，请修改你的 `configure` 命令以包含 `mod_spelling`，如下所示：

```bash
./configure \
  --enable-spelling \
# ...以及你使用的任何其他 configure 设置
```

如果你更喜欢使用动态模块，只需在 `mod_spelling` 行中添加 `--shared`：

```bash
./configure \
  --enable-spelling=shared \
# ...以及你使用的任何其他 configure 设置
```

在 `configure` 脚本之后，使用 `make` 和 `make install` 构建和安装新的二进制文件和模块是一件简单的事情。如果你选择为 `mod_spelling` 使用动态模块，你需要多做一步。要启用 `mod_spelling` 作为动态模块，请在你的 `httpd.conf` 文件中取消注释或添加以下行：

```apache
LoadModule spelling_module modules/mod_spelling.so
```

更改完成后，重启 Apache。如果 Apache 错误日志中没有显示任何错误，那么你已经成功地将 `mod_spelling` 功能添加到你的服务器中。

要实际使用拼写检查，请将以下指令添加到全局服务器配置部分、你的虚拟主机部分、`<Directory>` 部分或简单的 `.htaccess` 文件中：

```apache
CheckSpelling on
```

配置 `mod_spelling` 仅涉及 `CheckSpelling` 指令——值为“on”启用拼写检查，“off”禁用任何检查，这是默认行为。

要查看 `mod_spelling` 的工作状态，在你选择的目录中启用 `CheckSpelling`，然后在该目录中创建名为 `info.php` 的以下脚本：

```php
<?php phpinfo(); ?>
```

至此，你应该能认出这是标准的 PHP 信息转储输出，但不要使用正确的 `info.php` URL 加载文件，而是尝试使用略微拼写错误的名称（如 `ingo.php`）加载。启用 `mod_spelling` 后，Apache 会执行快速的 HTTP 301 重定向到它认为你最可能 `intended` 的内容，而不是提供冰冷的 404 Not Found。

## 内容压缩

如果我们告诉你，只需几分钟的 Apache 配置，你就可以大幅减少每月的带宽使用量，你会怎么想？你可能认为这是谎话，但事实确实如此——你只需要内容压缩和几个配置指令。

什么是内容压缩？当网页通过互联网下载时，默认情况下，构成页面标记、图像、样式表和其他内容的比特和字节主要处于未压缩状态

## 第 6 章

状态。你编写的 HTML 会直接按照保存时的原样发送，包括所有的空白字符。内容压缩允许你透明地压缩页面标记并将其通过互联网发送到用户的浏览器，在渲染到屏幕之前，它会在此处被静默解压。另一种思考方式是与通过电子邮件发送压缩文件相关联。你可以像普通附件一样轻松地将大型文档或多媒体文件直接作为邮件附件发送，但很多时候，你会在发送前将文件压缩为 `zip` 或 `tar.gz` 归档文件，以帮助缩短下载消息和附件所需的时间。

在 Apache 中使用内容压缩非常简单。你只需要 `mod_deflate`，它随 Apache 源代码提供，并且在构建 Apache 时可以轻松编译为模块。

### 使用 mod_deflate

与前面讨论的模块一样，你首先需要检查该模块是否可用，无论是作为 Apache 的静态部分，还是作为动态模块：

```bash
/path/to/httpd -l
ls /path/to/apache/modules/
# ...以及你可能使用的任何其他 configure 设置
```

如果在第一个命令的输出中看到 `mod_deflate.c`，或在第二个命令的输出中看到 `mod_deflate.so`，你就已经可以使用 `mod_deflate` 了，并且可以跳过下一步重建 Apache 的操作。

如果你在任一命令结果中都没有看到 `mod_deflate`，你需要将其静态构建到 Apache 二进制文件中，或者作为动态模块添加。如果你希望在使用源代码构建 Apache 时静态包含 `mod_deflate`，你只需在运行 `configure` 时添加以下内容即可：

```bash
./configure \
--enable-deflate
```

如果你希望使用动态可加载模块，只需在启用 `mod_deflate` 的行的末尾添加 `=shared`：

```bash
./configure \
--enable-deflate=shared \
# ...以及你可能使用的任何其他 configure 设置
```

显然，如果你计划在运行 `configure` 时包含其他指令，你也必须添加它们。配置完源代码后，执行常规的 `make` 和（作为 root）`make install`。

如果你将 `mod_deflate` 构建为动态模块，你需要在 `httpd.conf` 中使用 `LoadModule` 启用该模块：

```apache
LoadModule deflate_module modules/mod_deflate.so
```

然后重启 Apache 以使更改生效。

构建并启用 `mod_deflate` 后，让 Apache 使用 `mod_deflate` 以及要压缩哪些文件类型就变得很简单了。为此，你需要编辑你的 `httpd.conf` 文件，或者创建或修改你要使用压缩的目录中的 `.htaccess` 文件——如果可用，前一种方法是首选。

要在 Apache 中全局启用压缩，请在你的 `httpd.conf` 中添加以下内容：

```
AddOutputFilterByType DEFLATE text/*
AddOutputFilterByType DEFLATE application/ms*
AddOutputFilterByType DEFLATE application/vnd*
AddOutputFilterByType DEFLATE application/postscript
```

然后你只需重启 Apache，内容压缩即可正常运行。

所有这些配置指令具体是什么意思？其实很简单——在 Apache 2.x 中，`AddOutputFilterByType` 指令完全如其名称所示：它告诉 Apache 在将响应交给最终用户的浏览器之前，让输出通过给定的过滤器（在这种情况下是 `mod_deflate`）。前面的示例代码告诉 Apache 对基于文本的文件（`*text/*`）、任何 Microsoft 文档（如 Word 或 Excel 文件，`*application/ms/*` 和 `*application/vnd/*`）以及任何 PostScript 文件（如 Adobe Illustrator 或 EPS 绘图文件，`*application/postscript*`）使用 DEFLATE 过滤器（`mod_deflate`）。你喜欢的任何文档类型都可以通过简单地组合文档的 MIME 类型和通配符（类似于示例）来添加到 `mod_deflate` 的过滤列表中。

如果你只想压缩纯文本和 HTML 文件，请使用以下指令：

```
AddOutputFilterByType DEFLATE text/plain
AddOutputFilterByType DEFLATE text/html
```

如果你希望压缩 Apache 提供的所有内容呢？使用另一个 Apache 指令 `SetOutputFilter`，你可以告诉 Apache 将每个文件都通过 `mod_deflate`：

```
SetOutputFilter DEFLATE
```



然而，在大多数服务器配置中，这不是一个好主意。事实上，有一些文件类型从压缩中无法受益，有些文件在压缩后甚至会导致最终用户的数据损坏。在大多数情况下，没有必要压缩图像格式，因为最常用的 Web 格式已经内置了某种形式的压缩。此外，PDF 也是压缩过的，绝对不应该通过 `mod_deflate` 进行过滤，否则它们将在 Acrobat Reader 中变得无法阅读。

> 需要注意的是，Netscape Navigator 4.x 版本无法可靠地解压除 `text/html` 以外的任何文件类型，且特定版本的 Netscape Navigator 4.x 根本无法解压任何文件类型。

为了进一步调整你选择的文件类型的压缩，`mod_deflate` 提供了以下部分描述的配置指令。

### DeflateCompressionLevel

`DeflateCompressionLevel` 设置用于缩小文件的压缩级别，范围从 1 到 9。压缩级别 1 提供最快的压缩速度，压缩率最低（文件较大），而压缩级别 9 使用最慢的压缩速度，但生成的文件大小小得多。在决定使用哪个级别时，你必须确定对你来说哪个更重要——节省处理器周期还是节省下载时间。默认的压缩级别 6 通常是两者之间的良好折中方案。

### DeflateFilterNote

如果你希望日志文件显示访问日志中每个请求文件的压缩比，请使用 `DeflateFilterNote`。`DeflateFilterNote` 接受一个日志标记名称作为其值——使用 `DeflateFilterNote` 给出的命名标记可用于使用 Apache 的 `LogFormat` 指令自定义日志输出。

### DeflateWindowSize

这指定了用于压缩文件的 zlib 压缩窗口大小。值范围为 1 到 15，1 提供较少的压缩，15 提供最多的压缩。`DeflateWindowSize` 的默认值为 15。

### mod_deflate 的效果如何？

为了查看 `mod_deflate` 的节省字节的能力，此示例使用 Apache 提供了一个中等大小的 HTML 页面，分别在有和没有启用 `mod_deflate` 的情况下进行测试。在此示例中，用于 Wrox P2P 社区论坛（位于 `http://p2p.wrox.com`）的首页。该页面的原始 HTML 标记——仅指 HTML——重达 47172 字节。请查看下表，了解它在三种不同压缩级别下通过 `mod_deflate` 后的表现：

| 压缩级别 | 传输字节数 | 占原始大小百分比 | 近似下载时间 (56k) |
| :--- | :--- | :--- | :--- |
| 原始 | 47172 字节 | 原始 100% | 11.7 秒 |
| 默认 (6) | 7621 字节 | 原始 16.2% | 3.8 秒 |
| 级别 1 | 9050 字节 | 原始 19.2% | 4.1 秒 |
| 级别 9 | 7581 字节 | 原始 16.1% | 3.8 秒 |

如你所见，使用 `mod_deflate` 显然比提供未压缩的原始 HTML 更有优势——它可以消除通过连接发送的文件大小的近 84%。还要注意，使用最大压缩级别 9 仅比默认级别 6 略胜一筹，因此在这种情况下，坚持使用默认压缩级别 6 来为处理器节省几个周期可能是安全的。

许多网站混合了 HTML、媒体和相关脚本文件，因此像摄影博客或在线购物商城这样的网站可能无法在每个提供的文件上都获得巨大的文件节省，但每节省一个字节在月底都可能转化为巨大的带宽节省。以文本为主的网站，如博客和新闻门户，将真正受益于内容压缩，因为这些网站利用的大部分带宽都是纯文本——这些文本会通过 `mod_deflate`。

#### 为 PHP 脚本启用压缩

你可能在问 PHP 文件怎么办？在许多情况下，没有必要对 PHP 文件使用压缩，在某些情况下，这对输出甚至有害。

如果你的 PHP 脚本输出实际的图像或 PDF，例如，你不会希望 Apache 盲目地压缩输出，仅仅因为文件扩展名碰巧是 `.php`。

在某些情况下，输出缓冲和压缩可能已针对所有 PHP 脚本启用。要确定这一点，请检查配置变量 `output_handler` 的值，或者在 `php.ini` 中查找 `output_handler` 和 `zlib.output_compression` 的值。

要在 PHP 中启用输出压缩，请执行以下操作：

- 如有必要，请在您的机器上安装 `zlib` 库。
- 根据需求配置 PHP 源代码，确保包含 `--with-zlib`，然后正常进行 `编译`/`安装`。
- 修改您的 `php.ini` 以包含以下内容：

```text
output_buffering = Off
output_handler =
zlib.output_compression = On
```

- 重启 Apache 以使新的更改生效。

## 将 MySQL 与 Apache 结合使用

到目前为止，您已经使用 Apache 和基础身份验证创建了一个或两个安全区域，对于大多数情况而言，这可能已经足够。然而，您可能会发现，虽然 Apache 的基础身份验证很简单，但您可以纳入的控制和自定义程度有点过于有限。对于许多此类情况，您可以实际使用 Apache 基础身份验证与通过 MySQL 使用关系数据库功能性的组合。为了实现这种目的，存在 `mod_auth_mysql` Apache 模块。

与标准的 Apache 基础身份验证类似，`mod_auth_mysql` 可以按目录控制访问权限，并且可以配置在 `.htaccess` 文件内部以及 `httpd.conf` 中的 `<Directory>` 部分内。与标准的 Apache 基础身份验证不同，所有用户凭据存储在数据库中，而不是存储在平面文件中。

### 设置数据库

安装和配置 `mod_auth_mysql` 涉及几个步骤，第一步是创建必要的数据库结构以容纳用户数据。首先，打开您喜欢的 MySQL 客户端，并创建数据库。例如：

```sql
CREATE DATABASE apacheauth;
```

接下来，创建一个供 Apache 访问凭据使用的用户：

```sql
GRANT SELECT ON apacheauth.* TO apache@localhost IDENTIFIED BY 'apachepass';
```

现在数据库用户已创建，是时候添加一个表来存储登录信息了。暂时从一个仅包含用户名和密码的简单表开始：

```sql
USE apacheauth;
CREATE TABLE user_info (
user_name varchar(50) NOT NULL,
user_password varchar(50) NOT NULL,
PRIMARY KEY (user_info)
);
```

您可以随意命名表和列。在上面的示例中，`user_info` 用作表名，`user_name` 和 `user_password` 用作登录/密码组合，因为这些是 `mod_auth_mysql` 识别的默认名称。

> 在 `mod_auth_mysql` 的后续版本中，`password` 的默认列是 `user_password`，而不是模块文档中所述 的 `user_passwd`。

接下来，创建一个初始测试用户帐户，以便在后续测试身份验证时使用：

```sql
INSERT INTO user_info (user_name, user_password)
VALUES ('testuser', SHA1('testpass'));
```

> 请注意，语句中对密码使用了 `SHA1` 函数，而不是 `PASSWORD()` 函数。使用 `mod_auth_mysql` 时，您可以使用几种密码加密方法——本例碰巧使用的是 `SHA1`。

### 安装模块

一旦数据库表设置好，您需要实际下载 `mod_auth_mysql` 的源代码，可从 `http://modauthmysql.sourceforge.net` 获取。在撰写本文时，当前版本为 `2.9.0`，因此您应该下载 `mod_auth_mysql-2.9.0.tar.gz`。

下载模块源代码后，解压 tar 包：

```bash
tar -xvzf mod_auth_mysql-2.9.0.tar.gz
```

解压 tar 包后，更改目录到 newly created source folder（新创建的源文件夹）：

```bash
cd mod_auth_mysql-2.9.0
```

要从下载的源代码构建模块，您实际上将直接使用 Apache 的 `apxs` 命令。使用系统中 `apxs` 二进制文件的路径执行以下命令；此处使用的是默认 Apache 位置 `/usr/local/apache2/bin`：

```bash
/usr/local/apache2/bin/apxs -c -lmySQLclient -lm -lz mod_auth_mysql.c
```



如果构建成功，您应该看到几行编译信息，并且没有错误。相反，如果您遇到关于缺失 `mysql.h` 文件的错误，以及一系列与 `MySQL` 相关的错误，您可能需要手动指定 `MySQL` 库和包含文件的路径。使用 `MySQL` 的默认位置，您的命令可能如下所示：

```bash
/usr/local/apache2/bin/apxs -c -lmySQLclient -lm -lz \
-L /usr/local/mysql/lib/mysql \
-I /usr/local/mysql/include/mysql \
mod_auth_mysql.c
```

要安装新编译的模块，您需要以 root 身份执行以下命令。通常，请将 `apxs` 的路径更改为指向您的 `apxs` 二进制文件：

```bash
/usr/local/apache2/bin/apxs -i mod_auth_mysql.la
```

接下来需要执行的安装任务是，添加必要的命令以在 `httpd.conf` 中加载模块。为此，打开您的 `httpd.conf` 文件，找到一个合适的位置来添加模块定义——通常位于配置文件的最末尾，或其他 `LoadModule` 语句旁边——并添加以下内容：

```apache
LoadModule mysql_auth_module modules/mod_auth_mysql.so
```

最后，重启 Apache。

### 配置与使用

一旦数据库表准备好且模块安装完毕，剩下的就是告知 Apache 需要保护什么。与标准的 Apache 基础身份验证一样，您需要将一些配置指令添加到 `httpd.conf` 中的 `<Directory>` 部分，或者在你要保护的目录中创建一个 `.htaccess` 文件。

告知 Apache 对照您的 `MySQL` 数据库验证用户凭据通常至少涉及以下内容：

```apache
AuthName"<zone name>"
AuthType Basic
AuthMySQLDB dbname
AuthMySQLUser userid
AuthMySQLPassword password
AuthMySQLEnable On
require valid-user
```

这些指令的前两行和最后一行应该对您来说已经熟悉。它们简单定义了受保护区域的名称、身份验证类型，以及允许在检查的资源中找到任何有效用户访问。其他行告知 Apache 在哪里可以找到身份验证信息。而不是为 Apache 提供包含每个有效用户密码的文件名称，您提供数据库信息——数据库名称、用户名和密码——以便 Apache 和 `mod_auth_mysql` 知道在哪里查找。第六行，`AuthMySQLEnable On`，简单告知 Apache 实际使用 `mod_auth_mysql`——这是一种在没有完全卸载或移除模块的情况下禁用 `MySQL` 身份验证的方法。

要使用您之前创建的身份验证表，您将在 `<Directory>` 或 `.htaccess` 定义中添加以下内容：

```apache
AuthName"MySQLAuth"
AuthType Basic
AuthMySQLDB apacheauth
AuthMySQLUser apache
AuthMySQLPassword apachePASS
AuthMySQLEnable On
AuthMySQLPwEncryption sha1
require valid-user
```

这里，您正在告知 Apache 和 `mod_auth_mysql` 对照您的 `apacheauth` 数据库对用户进行身份验证。Apache 将使用您之前创建的 `apache` 帐户登录数据库，同时您还在告知 `mod_auth_mysql` 在将其与数据库中的值进行匹配之前，使用 `SHA1` 对给定的密码进行哈希处理。

此时，您应该能够通过 Web 浏览器登录您的受保护区域，提供添加到 `user_info` 表的 `testuser:testpass` 用户凭据，并在该目录中成功通过身份验证。

虽然这个示例相当简单且精简，但 `mod_auth_mysql` 实际上提供了大量的配置选项，因此您可以为几乎任何情况自定义您的身份验证。下面的章节描述了部分配置选项。

#### AuthMySQLEnable On | Off

这将启用或禁用 `mod_auth_mysql` 身份验证，而无需您直接从 Apache 中移除或卸载模块。

#### AuthMySQLHost localhost | hostname | ipaddress

这是 `MySQL` 数据库服务器的主机名或 IP 地址。如果您的环境在不同机器上运行 Apache 和 `MySQL`，您将需要使用此项。默认值是 `localhost`，因此同时运行 Apache 和 `MySQL` 的机器通常可以忽略此设置。

#### AuthMySQLPort port_number

这是 `MySQL` 正在监听的 TCP/IP 端口。`MySQL` 的默认值是端口 `3306`，但可以更改。此选项的默认值也是 `3306`，因此仅当 `MySQL` 在非标端口上监听时，才需要指定此选项。

#### AuthMySQLSocket socket_file_path

这是用于在 UNIX 机器上访问 `MySQL` 的 UNIX socket 文件。默认值是 `/tmp/mysql.sock`，与 `AuthMySQLPort` 类似，它仅在非标安装中需要使用。

#### AuthMySQLUser userid

这是用于访问保存身份验证信息的 `MySQL` 数据库的用户 ID。大多数数据库系统不会允许用户或 Apache 进程在没有正确的 `userid` / `password` 组合的情况下访问数据库，因此将此与 `AuthMySQLPassword` 一起设置为一个对身份验证表具有访问权限的非 root 用户帐户。至少，该用户需要对身份验证表具有 `SELECT` 访问权限。

#### AuthMySQLPassword password

与 `AuthMySQLUser` 配合使用，此选项指定访问 `MySQL` 身份验证表的用户帐户的密码。

#### AuthMySQLDB dbname

这是 `MySQL` 中保存身份验证表的数据库名称。如果未指定名称，将使用默认值 `test`。

#### AuthMySQLUserTable *table_name*

这是数据库中存储用户名和密码的表名。如果未指定表，则使用默认值 `user_info`。

#### AuthMySQLNameField *column_name*

这是用户表 `AuthMySQLUserTable` 中存储用户名的列名。在 `MySQL` 中创建表时，请确保该列具有索引或键，以确保每个值都是唯一的。该列的 *长度* 由您在 `MySQL` 中决定。默认值为 `user_name`。

#### AuthMySQLUserCondition

当 `mod_auth_mysql` 执行用户查找时，它会执行一个简单的 SQL `SELECT` 语句，其中包含执行匹配所需的任何条件。`AuthMySQLUserCondition` 字段允许您指定用于 SQL 语句 `WHERE` 子句的额外参数。

#### AuthMySQLPasswordField *column_name*

这是用户表中存储用户密码的列名。`MySQL` 中该列的长度应至少与加密密码哈希值一样长。`AuthMySQLPasswordField` 的默认值为 `user_password`。

#### AuthMySQLPwEncryption `none` | `crypt` | `scrambled` | `md5` | `aes` | `sha1`

这是在对数据库中密码进行编码时使用的加密方法，具体如下：

- `none`：无加密/明文
- `crypt`：UNIX `crypt()` 加密
- `scrambled`：`MySQL` `PASSWORD()` 加密
- `md5`：MD5 哈希
- `aes`：高级加密标准 `AES` 加密
- `sha1`：安全哈希算法 `SHA1`

如果未指定值，则使用默认值 `crypt`。

在使用 `AES` 密码加密时，请确保 `MySQL` 用户表中的密码字段是 `BLOB` 类型，而不是 `CHAR`、`VARCHAR` 或 `BINARY` 类型。除非列类型是 `BLOB` 变体之一，否则 `MySQL` 将从加密密码中删除多余的编码字符——这将导致永远无法将给定的密码与数据库值匹配。

#### AuthMySQLSaltField

这允许您指定三个值之一，用作加密密码时的“盐值”。值为 `<>` 表示 `mod_auth_mysql` 使用密码本身作为盐字段。值为 `<string>` 表示使用 `string` 的值作为盐字段。任何未由小于号/大于号包围的字符串都被视为数据库列的名称，该列的值用作盐字段。

## Chapter 6

#### AuthMySQLGroupTable

当 Apache 被告知检查组而不是单个用户 `require group` 对比 `require valid-user` 时，此指令用于设置包含组信息的表名。

#### AuthMySQLGroupCondition



类似于 `AuthMySQLUserCondition`，此指令允许您指定在匹配用户组时包含在 `WHERE` 子句中的条件语句。

### AuthMySQLGroupField
这是数据库中包含组名的字段的名称。当使用 Apache 的 `require group` 指令匹配组时，会使用此字段。

### AuthMySQLAuthoritative
这告诉 Apache 在 MySQL 身份验证失败时是否回退到其他模块。

## Apache 和 SSL

通过使用 `htpasswd` 或 `mod_auth_mysql` 使用基本身份验证来保护您的 Web 文件夹可以提高安全性。不幸的是，基本身份验证提供的额外安全层可能会被旨在入侵系统的严重黑客消除。问题在于：当您在标准服务器上使用基本身份验证时，用户名和密码实际上是从客户端未加密地传输到服务器的。精通网络的黑客可能会监控您的机器和服务器之间的传输，并嗅探到明文密码。

解决方案：加密客户端和服务器之间的通信。在 Apache 中，这可以通过使用安全套接字层 (SSL) 来实现。Apache 中的 SSL 以 `mod_ssl` 的形式出现，这是一个 Apache 模块，它使 Apache 控制的网站支持 SSL，允许任何与 Apache 之间的通信使用广泛的加密方案进行加密。

要在 Apache 中启用 SSL，首先检查 SSL 是否包含在现有的 Apache 二进制文件或可加载模块中：

```bash
/path/to/httpd -l
ls /path/to/apache/modules/
```

如果在第一个命令输出中没有看到 `mod_ssl.c`，或在 Apache 模块列表中没看到 `mod_ssl.so`，则需要自己构建 Apache 的 SSL 功能。要静态启用 SSL，请在从源代码构建时向 Apache `configure` 脚本添加 `-enable-ssl`：

```bash
./configure \
--enable-ssl \
# ...以及您使用的任何其他 configure 设置
```

## Apache 技巧

如果您想使用动态模块，只需在启用 SSL 的行末尾添加 `#shared`：

```bash
./configure \
    --enable-ssl=shared \
    # ...以及您使用的任何其他 configure 设置
```

然后，使用 `make` 和 `make install` 构建并安装新的 Apache 二进制文件和模块。如果您将 Apache 构建为动态模块，请在 httpd.conf 的全局配置部分添加以下行以启用它：

```apache
LoadModule ssl_module modules/mod_ssl.so
```

现在您可能已经注意到，粗体提示应替换为您自己的适当值。此外，请确保您输入的共同名称 (Common Name) 是服务器的真实完全限定域名，例如 www.yourserver.com。

命令完成并回答所有提示后，您将得到两个新文件：`privkey.pem`（用于签署证书的私钥）和 `testcert.csr`（证书请求）。下一步是从上一步创建的密钥中移除口令。如果不移除口令，您每次启动 Apache 时都必须输入它。虽然这可能看起来像是额外的安全性，但实际上是个麻烦，因为如果您的服务器遭遇断电或您频繁重启 Apache，它会阻止 Apache 完全重启。

要移除口令，请使用以下命令：

```bash
openssl rsa -in privkey.pem -out testcert.key
```

这将提示您输入在上一个命令开始时使用的相同口令：

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

这将显示：

```text
Signature ok
subject=/C=US/ST=Ohio/L=Cincinnati/O=TestSSL/OU=SSL Testing
 Department/CN=www.example.com/emailAddress=youremail@example.com
Getting Private key
```

您这里所做的使用 openssl 命令请求了一个 X.509 证书，使用 testcert.csr 证书请求作为输入，并将生成的证书保存为 testcert.cert，该证书使用私钥 testcert.key 自签名，有效期为 10 年。

既然您已经拥有了自签名的服务器证书和密钥，您需要将两者都复制到 Apache 可以访问的位置：

```bash
mkdir -p /etc/apache/ssl.crt
mkdir -p /etc/apache/ssl.key
```

## Apache 技巧

将证书和密钥复制到 Apache 的相应目录中：

```
cp testcert.cert /etc/apache/ssl.crt/testcert.crt
cp testcert.key /etc/apache/ssl.key/testcert.key
```

然后，创建一个目录来容纳你的新 SSL 网站：

```
mkdir -p /wwwssl
```

你可以使用任意喜欢的路径，甚至可以使用现有的路径——只需记住或写下你使用的是什么，因为之后在配置 Apache 时你需要用到它。

最后，创建一个简单的信息文件，以便在测试 SSL 时有所展示：

```bash
echo "<?php phpinfo(); ?>" > /wwwssl/index.php
```

现在你的密钥已就位，SSL 网络根目录已创建，你需要在 httpd.conf 中启用 SSL 功能。如果你的当前 httpd.conf 文件包含一行写着“Include /etc/apache/ssl.conf”或类似内容的行，那么你应该在指定的 ssl.conf 文件中进行任何 SSL 更改。否则，你可以直接在 httpd.conf 文件中进行更改，或者添加对你自己的 ssl.conf 文件的引用，并在那里进行更改。

在你的 SSL 配置文件或部分中，你需要在**全局配置作用域**中（而不是在虚拟服务器或目录配置部分中）拥有以下项：

```
Listen 443
```

接下来，你需要复用现有的 VirtualHost 部分来处理端口 443（如果存在），或者创建一个包含以下指令的新部分：

```apache
<VirtualHost _default_:443>
    # Server Certificate:
    SSLCertificateFile /etc/apache/ssl.crt/testcert.crt

    # Server Private Key:
    SSLCertificateKeyFile /etc/apache/ssl.key/testcert.key

    SSLEngine On

    DocumentRoot "/wwwssl" # 使用你之前创建的 SSL 目录
    ServerName www.example.com
    ServerAdmin youremail@example.com
</VirtualHost>
```

然后，在对配置文件进行更改后，重启 Apache。如果你在浏览器中使用 https:// URL（例如 https://www.example.com）加载你的新 SSL 网站，你会收到证书无效的提示（因为它是自签名的）。点击确定，你应该能看到你的 `phpinfo()` 函数的输出。如果没有显示任何内容，或者浏览器无法连接服务器，请检查 Apache 错误日志中是否有相关的错误消息——很可能只是一个简单的拼写错误。

> 要进一步调整 `mod_ssl`，并获取你可以用于 `mod_ssl` 的所有配置指令的完整列表，请访问 [http://httpd.apache.org/docs/2.0/mod/mod_ssl.html](http://httpd.apache.org/docs/2.0/mod/mod_ssl.html)。

## 第 6 章

## 将 Apache 用作文件库

使用 Apache 可以做的一件很酷的事情是将其用作一个简单的在线文件库，使用 WebDAV。WebDAV 代表 Web 分布式创作和版本控制（Web-based Distributed Authoring and Versioning），它允许 Apache 将用户启用的目录视为其计算机上的远程目录或驱动器。类似于 Windows 共享或 NFS 导出，WebDAV 允许远程编辑和存储访问，只是使用 HTTP 作为传输层，而不是像 SMB 和 NFS 这样的专用 TCP 协议或端口。



要了解 WebDAV 如何作为共享驱动器工作，最简单的方法是直接看到它的实际操作，因此接下来，你将启用随 Apache 附带的 `mod_dav`，并进行测试。首先，与其他模块一样，检查 `mod_dav` 是否已经静态编译到 Apache 中，或者作为可加载模块存在：

```
/path/to/httpd -l
ls /path/to/apache/modules
```

正如你可能猜到的，如果在 `httpd -l` 输出中没有看到 `mod_dav.c`，或者在文件列表中没有看到 `mod_dav.so`，你需要使用 Apache httpd 源代码自行构建它。要将 `mod_dav` 静态添加到 Apache 二进制文件中，请确保 `configure` 命令中存在 `--enable-dav` 和 `--enable-dav-fs`：

```
./configure \
--enable-dav \
--enable-dav-fs \
# ...以及你使用的任何其他 configure 设置
```

要将 `mod_dav` 构建为共享对象，只需在两个 DAV 相关行的末尾添加 `=shared`：

```
./configure \
--enable-dav=shared \
--enable-dav-fs=shared \
# ...以及你使用的任何其他 configure 设置
```

然后使用 `make` 和 `make install` 构建并安装新的二进制文件和模块。

如果你决定使用 `mod_dav` 的动态模块，你需要使用以下行在 `httpd.conf` 中启用它们：

```
LoadModule dav_module  modules/mod_dav.so
LoadModule dav_fs_module modules/mod_dav_fs.so
```

为了有一个实际存储 WebDAV 文件库的地方，你可以创建一个新目录，或使用你选择的现有目录。你应该将 WebDAV 文件夹放在你的已启用 SSL 的网络根目录内，或者如果你计划使用基本身份验证来限制对 WebDAV 文件夹的访问，请确保稍后启用 SSL。基本身份验证以明文发送用户名和密码，因此你需要启用 SSL 来保护受保护目录以加密基本身份验证请求。如有需要，创建新文件夹，并创建一个虚拟文件以添加到 WebDAV 文件夹中：

```
mkdir -p /wwwssl/dav
echo "Testing DAV" > /wwwssl/dav/testing.txt
```

当用户访问你的 WebDAV 文件夹时，你需要针对数据库或 `htpasswd` 文件对他们进行身份验证，以防止互联网上所有匿名用户占满你的硬盘。首先，创建一个 `htpasswd` 文件来存储有效用户的密码，并使用 `testdav` 的用户帐户对其进行初始化：

```
mkdir -p /davauth
/path/to/htpasswd -c /davauth/dav.htpasswd testdav
```

当提示输入密码时，输入你选择的密码。接下来，在 `/wwwssl/dav` 文件夹中创建一个 `.htaccess` 文件以强制基本身份验证。`.htaccess` 文件应包含以下内容：

```
AuthName "DAV Test"
AuthType Basic
AuthUserFile "/davauth/dav.htpasswd"
require valid-user
```

最后，在 `httpd.conf` 中创建一个 `Directory` 条目，以启用 WebDAV 和给定目录的基本身份验证：

```
<Directory "/wwwssl/dav">
  AllowOverride AuthConfig
  Dav On
</Directory>
```

然后你可以重启 Apache，WebDAV 将为你的 HTTPS 网站的 `/dav/` 文件夹启用，可以通过类似 `https://www.example.com/dav/` 的地址访问。你可以尝试在 Web 浏览器中加载此 URL，但它与标准的非 DAV Web 目录的行为没有区别。要使用你的 WebDAV URL 的功能，你需要使用支持 WebDAV 的软件。

`jEdit`、`NuSphere` 的 `PHPEd` 和 `Macromedia Dreamweaver` 等编辑器都支持某种程度的 WebDAV。如果你没有这些编辑器可用，不要担心——大多数现代操作系统实际上在其文件浏览器/浏览器工具中本地支持 WebDAV 共享的挂载。

要使用操作系统的文件浏览器访问你的 WebDAV 共享，请遵循前面各部分中适用于你的操作系统的说明。

### Windows 2000/XP

要在 Windows 2000 或 XP 下设置 WebDAV，你需要运行“添加网络位置”向导，步骤如下：

1. 转到“网络邻居”，双击“添加网络位置”，如图 6.1 所示。

![](img/fd2e7361878181c2b12e30301ff3e182_185_0.png)

图 6.1

2. 当出现“添加网络位置向导”时，单击“下一步”以显示服务提供程序列表。选择“选择其他网络位置”选项，如图 6.2 所示，然后单击“下一步”。

![](img/fd2e7361878181c2b12e30301ff3e182_185_1.png)

图 6.2

3. 在“Internet 或网络地址”字段中输入你的 WebDAV 目录的 URL，如图 6.3 所示。然后单击“下一步”。

![](img/fd2e7361878181c2b12e30301ff3e182_186_0.png)

图 6.3

4. 在 SSL 安全警告对话框中单击“是”。发出警告是因为你正在使用自签名证书——这与你之前尝试访问 SSL 启用的网站时看到的警告相同。

5. 然后系统会提示你输入用户名和密码以访问 DAV Test 域。输入创建 `htpasswd` 文件时使用的值。

6. 然后系统会提示你为网络位置命名，以便稍后轻松识别该位置。输入 `My WebDAV` 作为网络位置名称。

7. 现在你的 WebDAV 位置应该已经设置好，你会看到“完成添加网络位置向导”屏幕。勾选“单击完成时打开此网络位置”复选框，如图 6.4 所示。

8. 然后系统会再次提示你接受自签名 SSL 证书并输入用户名和密码。接受证书并输入你在步骤 5 中使用的凭据。

9. 然后你应该能在标准的 Windows 资源管理器窗口中看到 WebDAV 共享的内容，如图 6.5 所示。

10. 将 `My WebDAV` 共享用作标准驱动器或文件夹——你可以像操作本地文件夹一样在 WebDAV 共享上添加、编辑和删除文件。

## 第 6 章

![](img/fd2e7361878181c2b12e30301ff3e182_187_0.png)

![](img/fd2e7361878181c2b12e30301ff3e182_187_1.png)

### Mac OS X

要在 Mac OS X 下配置 WebDAV，请执行以下操作：

- 1. 从 Finder 菜单中选择“前往➔连接服务器”，或者直接在 Finder 窗口中输入 Command-K。这将打开如图 6.6 所示的“连接服务器”窗口。在“服务器地址”字段中输入 WebDAV 共享的 URL，然后单击“连接”。

![](img/fd2e7361878181c2b12e30301ff3e182_188_0.png)

- 2. 系统会提示你接受自签名 SSL 证书。单击“继续”。

- 3. 会出现针对 DAV Test 域的用户名和密码提示。输入你之前创建 `Htpasswd` 文件时使用的用户名和密码。

- 4. 映射的 WebDAV 驱动器现在应该像常规挂载的网络卷一样显示在 Finder 中，如图 6.7 所示。现在你应该能够像使用任何标准本地或网络卷一样使用它。

![](img/fd2e7361878181c2b12e30301ff3e182_188_1.png)

#### 总结

在本章中，你看到了添加几个 Apache 模块如何可以显著地提高你网站的性能。它告诉你如何简化 URL 重定向，修复用户输入错误，压缩内容以节省带宽，创建基于 Web 的文件共享，以及使用 MySQL 和 SSL 保护你的网站安全。这种可扩展性使得 Apache 不仅仅是一个普通的 Web 服务器。

在你探索了这里讨论的模块的潜力之后，你应该进一步研究可以在 `httpd.apache.org` 和 `sourceforge.net` 上找到的其他模块。你会发现那里的模块可以对其他数据库进行用户身份验证，加速 Perl 等语言的性能，使用 Apache 作为代理服务器等等。正如你所看到的，Apache 有各种用途的模块。

虽然本章介绍了一种保护网站的新方法，但下一章将直接解决安全问题。

## 第 7 章

# 网站安全



安全是每个网站管理员最关心的问题之一——如果没有，那也应该是。将你的网站放置在公共互联网上是对各种入侵者的公开邀请，你需要能够处理他们，无论你的网站有多小或多专业。幸运的是，PHP 可以帮助你保护你的网站和你用户的数据。如前几章所述，你可以使用 Apache 来控制身份验证，但你也可以使用 PHP 内置函数创建自己的身份验证系统。本章将向你展示如何做，然后带你了解你可能遇到的一些更常见的攻击类型，并展示一些防止它们的简单方法。

## 控制访问

当你考虑保护网站安全时，最先想到的方法之一可能是限制访问。如果坏人无法访问 Web 应用程序，它就是安全的，对吗？当选择保护敏感文件和脚本的方法时，你有几个选择，有些内置于 Apache，有些基于 PHP，有些则是两者的混合。

### Apache 控制的身份验证

锁定网站最简单的方法是使用基本身份验证，这在第 6 章中已经介绍过。使用 `.htaccess` 和密码文件的组合，你可以快速限制对网站任意文件夹的访问。这种方法有许多优点。

主要的是，它极其容易实现。Apache 默认安装时标准附带，简单的按目录基本身份验证可以很容易地通过 `.htaccess` 或 `<Directory>` 条目设置。

使用内置 Apache 身份验证的缺点是什么？维护复杂的受限文件夹和用户的层级结构可能很麻烦。如果你有大量用户或组，以及相当多的受保护目录，确保正确的用户在正确的组中，拥有正确的资源访问权限，使用当前的密码等，很快就会变成一场噩梦。

如果使用多个负载均衡或镜像 Web 服务器，简单的 Apache 身份验证也可能成为问题。因为用户凭据存储在每台机器上，你可能会处于文件不一致的状态——某些密码文件可能包含不同数量的用户，不同的密码，或其他问题。

作为使用 Apache 简单基于文件身份验证的替代方案，你还可以使用 `mod_auth_mysql` Apache 模块，这也在第 6 章中介绍过。使用 `mod_auth_mysql` 集中管理你的用户名/密码存储，并且赋予你复杂的权限匹配能力——不像标准的 Apache 基本身份验证那样只是简单的用户名匹配。

与 Apache 简单身份验证一样，`mod_auth_mysql` 依赖于 `.htaccess` 文件中指定的访问权限或 `httpd.conf` 中的 `<Directory>` 条目。如果你无法更改 Apache 配置，且你的主机不允许 `.htaccess` 文件，你需要找到另一种方法。这里就引入了基于 PHP 的身份验证。

### PHP 控制的身份验证

如果 Apache 控制的身份验证不可行，你实际上可以使用 PHP 的功能来模拟标准基本身份验证。通过发送适当的响应头，并检查正确的服务器变量，你可以从头构建自己的基本身份验证系统，并且它将与 `mod_auth_mysql` 拥有相同的强大功能，甚至更多。

为了展示如何使用 PHP 进行基本身份验证，你将设置一个简单的数据库作为用户凭据的存储库。然后 PHP 将针对该数据库检查用户名和密码；最终用户看到的只是标准的基本身份验证提示。

#### 创建身份验证数据库

首先在 MySQL 中创建一个名为 `WebAuth` 的数据库：

```sql
CREATE DATABASE WebAuth;
USE WebAuth;
```

接下来，为身份验证系统创建一个 MySQL 登录，并给予它对你刚创建的数据库的只读访问权限：

```sql
GRANT SELECT ON WebAuth.* TO WebAuth@localhost IDENTIFIED BY 'AuthPass';
```

现在，设置用于存储用户名和密码的表。在这个例子中，该表将仅存储用户名和密码的哈希值，但如果你愿意，你可以轻松添加其他字段以容纳你想要的任何其他访问标准。

```sql
CREATE TABLE Users (username varchar(50) PRIMARY KEY,
passwd_md5 varchar(32) NOT NULL,
passwd_sha1 varchar(40) NOT NULL);
```

请注意，你并不是简单地创建一个字段来存储用户的明文密码，而是创建字段来存储用户密码的单向哈希值。这样做确保了密码仍然可以与密码提示中输入的值进行比较，但如果数据库被入侵，这使得尝试破解密码的人极其困难。如果你对 MD5 或 SHA1 熟悉，你会知道它们都是单向哈希算法。在使用其中任何一个算法对密码进行哈希处理后，几乎不可能确定原始密码。

> `MD5` 接受输入字符串并创建原始输入的 128 位“唯一”指纹，或哈希值。
>
> `SHA1` 表现得类似，但安全性稍高，生成 160 位的“唯一”指纹。

你可能注意到，前面的讨论并未绝对地提及这两种方案提供的唯一性或无懈可击的哈希处理。直到最近，MD5 一直被认为是所有除最安全数据外哈希处理的合理解决方案，而 SHA1 也是如此。当使用暴力破解时，这两种加密方案都不是 100% 不可破解的。一个密码生成程序可以遍历每个字符和每个密码长度的所有组合，直到最终找到与这两种算法之一生成的哈希值匹配的输入字符串。

然而，密码分析的最新进展已经证明，MD5 可以通过找到产生相同输出哈希值的输入来更快地被攻破，即使输入字符串并不匹配——这是 MD5 固有的弱点。SHA1 最近也受到了攻击，并且随着处理能力的增加，暴力破解哈希所需的时间迅速减少。

为了对抗 MD5 中看到的任何类型的碰撞攻击，你创建了 `Users` 表来存储密码的 MD5 和 SHA1 哈希值。这样做实际上使任何碰撞攻击尝试都变得徒劳——即使入侵者设法找到了与 MD5 哈希值匹配的输入字符串，除非它是真实的密码，否则它不会匹配 SHA1 哈希值。

为了使数据库对身份验证脚本有用，你需要添加至少一个用户：

```sql
INSERT INTO users VALUES ('testuser', MD5('testpass'), SHA1('testpass'));
```

请注意，在添加密码时使用了内置的 MySQL 函数 `MD5()` 和 `SHA1()`。

### 一个 PHP 基本身份验证脚本

一旦你的数据库设置好，创建以下脚本，并将其保存为 `phpauthbasic.php`：

```php
<?php
// Define database constants
define('AUTH_HOST', 'localhost');
define('AUTH_USER', 'WebAuth');
define('AUTH_PASS', 'AuthPass');
define('AUTH_DB', 'WebAuth');

function attempt_auth()
{
    // Send authentication headers
    header('WWW-Authenticate: Basic realm="Protected by PHP"');
    header('HTTP/1.0 401 Unauthorized');
}
```

## 第 7 章

### 代码实现



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
    exit();
}
?>
```

这一切意味着什么？来看看是什么让这段脚本运转起来的。

## 配置数据库常量

你要做的第一件事是为数据库连接定义一些常量：

```php
<?php

// Define database constants

define('AUTH_HOST', 'localhost');

define('AUTH_USER', 'WebAuth');

define('AUTH_PASS', 'AuthPass');

define('AUTH_DB', 'WebAuth');
```

## `attempt_auth()` 函数

接下来是 `attempt_auth()` 的函数定义。该函数只需向浏览器发送响应头，告知其尝试进行 Basic 认证登录，并将给定的 realm（域）作为登录提示中的安全区域显示：

```php
function attempt_auth()
{
  // Send authentication headers
  header('WWW-Authenticate: Basic realm="Protected by PHP"');
  header('HTTP/1.0 401 Unauthorized');
}
```

## `check_login()` 函数定义

在 `attempt_auth()` 之后是 `check_login()` 的函数定义。这里将实际检查传入的用户名和密码，并与之前创建的 `WebAuth` 数据库中存储的值进行比对。首要任务是确保传入了用户名和密码，并连接到数据库，将 `WebAuth` 设为活动数据库：

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

### 执行匹配查询

建立数据库连接后，执行查询以检查用户名/密码是否匹配：

```php
// Search for matches
$result =
mysql_query("SELECT COUNT(username) AS account
FROM users
WHERE username='$username'
AND password=md5('$password')
AND passwd_sha1='$sha1'", $conn);
```

要构建此查询，必须首先使用 `addslashes()` 转义用户名，以帮助避免任何 SQL 注入攻击（后文将讨论）。这里使用了 PHP 函数 `md5()` 和 `sha1()`，但如果你愿意，也可以轻松地使用 MySQL 的等效函数——它们应该会产生完全相同的结果：

```php
// Search for matches
$result =
mysql_query("SELECT COUNT(username) AS count
FROM users
WHERE username='" . addslashes($username) . "'
AND passwd_md5=MD5('" . addslashes($password) . "')
AND passwd_sha1=SHA1('" . addslashes($password) . "')",
$conn);
```

你可能已经注意到，`addslashes()` 函数被添加为密码的包装器，而在之前 PHP 进行密码哈希的情况下并没有这样做。这再次是为了防止 SQL 注入攻击，甚至防止用户在密码中包含单引号等简单错误导致的错误。当首先使用 PHP 对密码进行哈希处理时，无需使用 `addslashes()` 转义结果，因为 `md5()` 和 `sha1()` 函数产生的输出仅由十六进制值组成——不可能有单引号或其他危险字符混入。

### 完成 `check_login()`

为了完成 `check_login()` 函数，将返回占位符设置为 `true`，并创建一个稍后在脚本中使用的会话变量，以避免不必要的重复查询：

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
}
```

## 脚本主流程

进入脚本中实际首先被解释的代码，你首先初始化会话数据：

```php
session_start();
```

然后，你首先检查来自 `check_login()` 的会话变量是否已设置。如果尚未设置——意味着用户尚未通过身份验证——检查 PHP `USER` 和 `PHP_AUTH_PW` 服务器变量，并调用 `check_login()` 函数。当 PHP 尝试使用 Basic 认证获取登录信息时，服务器变量 `PHP_AUTH_USER` 和 `PHP_AUTH_PW` 都存在。如果未设置，说明用户尚未被提示输入登录信息。在这种情况下，如果没有传入信息且之前传入的凭据无效，你希望提示用户输入登录信息。如果未找到有效的用户信息，则调用 `attempt_auth()`，用户将获得再次登录的机会。只有当用户在登录提示上点击“取消”时，才会显示“Authorization Required”消息：



```php
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

要测试 PHP 身份验证，你可以尝试在浏览器中加载此脚本，但更好的做法是将其包含在你创建的任何标准 PHP 页面中。你可以使用以下代码将该授权作为一个简单的包含项进行测试：

```php
<?php

require_once 'phpauthbasic.php';

echo "Authentication Successful!";
?>
```

当你尝试在浏览器中加载此脚本时，请使用 `testuser/testpass` 组合，或者你最初添加到 `users` 表中的任何凭据。如果用户名和密码正确，你应该看到一个漂亮的“Authentication Successful!”（认证成功！）消息；如果你点击“取消”，你会看到令人担忧的“Authorization Required”（需要授权）消息。

既然你看到它是这样工作的，你可能会认为没有理由不使用这种方法。但正如你在决定如何编写应用程序时所做出的许多选择一样，这种方法也有一些缺点。

在身份验证方法生效之前，必须满足两个主要要求。首先，`php.ini` 中的 `safe_mode` 必须未启用。当启用时，`safe_mode` 会阻止创建 `PHP_AUTH_USER` 和 `PHP_AUTH_PW` 服务器变量。如果这些变量不存在，无论使用的凭据是否真正有效，脚本都会不断重新显示登录提示，直到用户点击“取消”。判断 `safe_mode` 是否确实启用的快速方法是：登录提示中 realm 信息的末尾会附加脚本的 uid。

其次，此方法不能与 Apache 的 Basic 认证系统一起使用。这适用于与脚本相同级别或任何父目录上的任何 Apache 控制的访问（`htaccess`）。如果两个身份验证系统都启用，Apache 系统将获得初始优先权。发生的情况是，用户最初可以使用 Apache Basic 认证的有效凭据登录，随后出现 PHP 身份验证提示。然而，在此时，HTTP 实际上已经通过 401 响应清除了浏览器针对 Apache 控制的认证状态。由于浏览器不再针对 Apache 进行认证，它将重新提示输入 Apache 级别的凭据，然后回到 PHP 凭据，如此循环，直到用户在浏览器中点击“取消”或“停止”。

# 第 7 章

## PHP 表单认证

如果 PHP 基本认证对你来说不是一个可行的解决方案，或者你不喜欢浏览器登录窗口的样式，请不要担心；你还有另一个选择。除了依赖浏览器内置的标准登录窗口，你可以轻松创建自己的登录表单，甚至可以使用大部分之前的 PHP 认证代码。将以下内容保存为 `phpAuthForms.php`。注意，其中大部分代码直接取自之前使用过的 `phpAuthBasic.php` 文件：

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
                    mysql_query("SELECT COUNT(username) AS ucount
                    FROM Users
                    WHERE username=\"" . addslashes($username) . "\"
                    AND passwd_md5=\"" . md5($password) . "\"
                    AND passwd_sha1=\"" . sha1($password) . "\"",
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
if (!(isset($_SESSION['username']) ||
      check_login($_POST['username'],
                  $_POST['passwd'])))
{
?>
<form method="post" action="testforms.php">
  <label for="username">Username:</label>
  <input type="text" id="username" name="username" maxlength="50" />
  <label for="passwd">Password:</label>
  <input type="password" id="passwd" name="passwd" />
  <input type="submit" value="Log in" />
</form>
<?php
}
?>
```

有什么变化？实际上并没有太多。主要的修改在文件末尾：

```php
// Check if using valid credentials
if (!(isset($_SESSION['username']) ||
      check_login($_POST['username'],
                  $_POST['passwd'])))
{
```

你不再检查服务器变量 `PHP_AUTH_USER` 和 `PHP_AUTH_PW`，而是检查通过 HTTP POST 传递的登录凭据，名为 `username` 和 `passwd`。然后，与基本认证示例类似，如果登录无效或未提供，则向用户显示登录提示。在这种情况下，`attempt_auth()` 函数已被移除，而在它原本被调用的地方，是一个简单的 HTML 表单：

```php
?>
<form method="post" action="testforms.php">
  <label for="username">Username:</label>
  <input type="text" id="username" name="username" maxlength="50" />
  <label for="passwd">Password:</label>
  <input type="password" id="passwd" name="passwd" />
  <input type="submit" value="Log in" />
</form>
<?php
    exit;
}
?>
```



要使用这种认证方法，你只需将此类脚本包含在任何你想要保护的页面顶部即可。将此文件命名为 `testforms.php`（它必须与之前使用的表单目标相匹配）：

```php
<?php

require_once 'phpauthforms.php';

echo "Authentication Successful!";
?>
```

那么这种方法的优点是什么？首先是兼容性。使用简单的基于表单的 PHP 认证几乎适用于任何情况，无论是否启用 `safe_mode`，或者 Apache 是否使用其自身的 `.htaccess` 认证。这种解决方案唯一的真正缺点是，你必须自己编写登录表单，并按需进行样式设置，而不是依赖浏览器/操作系统来完成这项工作。

## 其他访问限制

除了通过用户名和密码限制访问外，你还可以使用 PHP 检查其他用户参数。一个常见的检查变量是用户的源 IP。通过引用服务器变量 `$_SERVER['REMOTE_ADDR']`，你可以确保只有特定的 IP 范围可以查看资源，或者相反，你可以屏蔽特定的 IP。如果你正在为公司内网创建网站，你可以将访问权限限制在内部 IP（假设你的网络使用了它们）。例如，你可以决定只有 10.0.1.x 网络的成员才能查看你网站的特定区域。另一个例子是 BBS 站点或网络论坛。通常，如果某人（例如）在论坛上发送垃圾信息，它们需要按 IP 封禁特定用户。

另一个值得检查的服务器变量是 `$_SERVER['HTTP_REFERER']` 变量。此变量保存了之前查看的页面的名称，可以帮助你消除某些类型的网络攻击。假设你创建了一个简单的表单，用于将数据保存到数据库、发送电子邮件或任何依赖有效用户输入的操作。你可能已经付出了很大努力来执行客户端输入验证，并指定了表单的最大长度。不幸的是，任何你可能期望从 Web 客户端接收的输入都可以通过外部表单轻松被破坏。任何网站攻击者都可以轻松复制你的表单 HTML 标记，然后按其需要修改它——无论是用于信息收集、跨站脚本、SQL 注入，还是其他任何目的。

他们所需要做的只是制作该表单的副本，以便向你的网站提交不当数据，将其托管在他们自己的机器上，但使用绝对 URL 作为方法将其发布到你的表单。当使用隐藏表单变量且在 `php.ini` 中启用了 `register_globals` 时，这种攻击可能特别有害。

通过检查 `HTTP_REFERER` 值，你可以消除大多数欺骗性表单攻击，只要你确保输入确实来自你网站上的页面即可。

若要查看 `HTTP_REFERER` 检查和 `REMOTE_ADDR` 验证的示例，请查看以下代码：

```php
<?php

// Check the referrer
if (!preg_match('/^http:\/\/(localhost)|' .
'(www\.example\.com)/i',
            $_SERVER['HTTP_REFERER']) )
        {
            echo 'Invalid referer! '
                  "We don't take kindly to spoofed forms in these parts.\n";
        }
        // Check to see if request came from internal users
        if ( !preg_match('/\b(\d{1,3}\.\d{1,3}\.\d{1,3})\b' .
                    '(172\.16\.\d{1,3}|192\.168\.\d{1,3}|' .
                    '$_SERVER['REMOTE_ADDR'])))
        {
            echo 'Invalid client address! '
                  "Who let YOU in here?\n";
        }
        ?>
```

此代码首先检查引用页面，以确保其来自 localhost 或预期域名（假设你已将其更改为匹配你自己的域名），然后检查用户的 IP 地址，以确保其来自内部/私有 IP 范围。

PHP 能做的另一件事，有助于限制某些类型的访问，是为注册表单提供 CAPTCHA 图像。CAPTCHA，即“用于区分计算机和人类的完全自动公共图灵测试”，是一种测试，通常会在图像中显示稍微扭曲的文本。其想法是，尽管外观扭曲，人类应该能够弄清楚文本实际说了什么，而计算机则不能。许多免费电子邮件和公告板站点使用这种技术来防止自动机器人脚本注册并利用服务发送垃圾信息等。

尽管目前处于 alpha 开发阶段，PHP Pear 仓库中的 `Text_CAPTCHA` 包提供了实现 CAPTCHA 功能的简单接口。`Text_CAPTCHA` 可在 http://pear.php.net/package/Text_CAPTCHA 找到。

如果你想尝试 `Text_CAPTCHA`，你可以简单地使用 `pear install` 命令安装它：

```bash
pear install -f Text_CAPTCHA
```

你需要使用 `-f` 标志来强制安装，因为 Pear 团队目前认为 `Text_CAPTCHA` 不稳定，所以普通的非强制安装将会失败。另外请注意，`Text_CAPTCHA` 依赖于 `Text_Password` 和 `Image_Text`（也是 alpha 版）Pear 包，因此如果你尚未安装这些包，需要先安装它们。

安装好所有包后，创建以下文件作为 `captchatest.php`：

```php
<?php

// Include the Pear class
require_once('Text/CAPTCHA.php');

// Set the options for the generated text;
$opts = array(
```

# 第 7 章

'font_size' => 25,

'font_path' => './../',

'font_file' => 'VerdanaMono.TTF'

);

// 创建 CAPTCHA 对象

$cap = Text_CAPTCHA::factory('Image');

// 使用随机文本初始化 CAPTCHA 对象

$r = $cap->init(250,100, null, $opts);

// 检查 CAPTCHA 对象是否有效

if (PEAR::isError($r))

{

 echo 'CAPTCHA 生成失败。';

 exit;

}

// 生成 PNG 格式的 CAPTCHA 图像

$png = $cap->getCAPTCHAasPNG();

// 在浏览器中显示图像

header('Content-type: image/png');

echo $png;

?>
```

当你在浏览器中运行这段代码时，你应该看到类似图 7.1 的内容。

![](img/fd2e7361878181c2b12e30301ff3e182_201_0.png)

`Text_CAPTCHA` 是如何知道你想要使用什么字符串的？它并不知道。当你初始化 CAPTCHA 对象时，你将 `null` 作为测试字符串传入：

```
// 使用随机文本初始化 CAPTCHA 对象
$r = $cap->init(250,100, null, $opts);
```

如果你想显式设置 `Text_CAPTCHA` 要渲染的文本字符串，只需将输入字符串从 `null` 更改为你想要的值：

```
// 使用随机文本初始化 CAPTCHA 对象
$r = $cap->init(250,100, 'computers be gone!', $opts);
```

在你的 PHP 脚本中需要检查的其他关键点包括本地文件名及其访问方式。请查看以下代码：

```
<?php

$content = file_get_contents('/path/to/content/' . $_POST['file']);

echo $content;

?>
```

这种代码经常可以在许多自制的 CMS 系统或某种自定义文档检索脚本中找到。不幸的是，这是一个巨大的安全风险。如果攻击者为 `file` 提交了值 `../../../../../etc/passwd` 会发生什么？如果服务器没有正确加固——很多服务器都没有——系统密码文件的内容将被直接回显到屏幕上。

你可以采取一些简单的步骤来帮助防止这种攻击。首先，如果你可以控制 Apache Web 服务器，请确保它作为一个非特权用户运行。无论 Apache 以什么用户身份运行——apache、nobody、www，都无所谓——确保该用户没有权限访问除合法网站文件以外的任何文件。

其次，确保你转义文件路径中提供的任何父目录访问点号，如下所示：



```
<?php
$File = str_replace('../', '', $_POST['file']);
$Content = file_get_contents('/path/to/content/' . $File);

echo $Content;

?>
```

如果可能的话，将转义后的文件名与其路径前缀连接起来也是一个好主意。这样，如果攻击者为文件值提供了绝对路径，它仍然会相对于指定的文件夹进行行为处理。

# 网站攻击

每当你在公共互联网上发布一个网站时，它就面临着被攻击的风险。虽然没有任何应用程序能够真正达到 100% 的安全，因为新的漏洞利用和黑客技术每天都在被发现，但有一些攻击类别你可以相对容易地在 PHP 脚本中进行防御。

## 滥用 register_globals

如果关于 `register_globals` 的每篇文章、书籍或任何文档描述都没有让你深刻意识到这一点，那么这里再次强调：将 `register_globals` 设置为开启状态是一场等待发生的灾难。

如果你不熟悉 `register_globals`，它是 `php.ini` 中的一个设置，用于控制自动填充与表单元素或 Cookie 同名的变量。在本章前面创建登录表单中，有一个名为 `username` 的字段。通常，当 `register_globals` 被禁用时，在表单提交后访问 `username` 字段的唯一方法是使用 `$_POST` 或 `$_GET` 数组，具体取决于表单的方法。当 `register_globals` 启用时，`username` 字段除了可以通过 `$_POST` 或 `$_GET` 访问外，还可以作为 `$username` 变量直接访问。

从 PHP 4.2.0 开始，`register_globals` 的默认值是关闭的，但许多 Web 主机为了提供与那些假设存在并依赖 `register_globals=on` 的旧脚本的兼容性，会重新启用 `register_globals`。不幸的是，这为恶意用户提供了主要的攻击途径。当 `register_globals` 启用时，PHP 按照 `variables_order` 设置中指定的顺序评估环境、表单、Cookie 和服务器变量。如果服务器使用“推荐”的设置文件，GET 变量首先被设置，然后 POST 被设置并覆盖任何匹配的 GET 值。接下来设置 Cookie 值，随后是服务器变量，覆盖之前设置的任何匹配值。

虽然这种行为看起来很方便，但很容易通过克隆的表单或伪装的 Cookie 信息被利用。关于它可能如何被利用的例子，请查看以下 PHP 代码：

```
<?php
if (user_is_admin())
{
    $access_level = 10;
}
show_menu($access_level);
// ... 等等 ...
?>
```

在这种假设的情况下，脚本调用 `user_is_admin()` 函数来确定用户是否是管理员。如果是，则 `$access_level` 变量被设置为 10，并且在随后的脚本中可能会显示完整的管理界面。

如果 `register_globals` 已启用，只需在请求文件时将你期望的访问级别附加到查询字符串中即可，例如：

http://www.example.com/file.php?access_level=10

## 站点安全

现在，如果脚本以添加的 `access_level` 调用，无论用户是否真的是管理员都不重要——由于 `register_globals` 以及 PHP 不要求变量初始化，脚本开始时 `$access_level` 变量会自动被设置为 10。

幸运的是，避免此类陷阱相对容易。确保你在禁用 `register_globals` 的情况下编码，使用正确的 `$_GET` 和 `$_POST` 超全局变量，初始化可能不安全的变量，并确保在开发和测试站点时将 `error_reporting` 设置为 `E_ALL`。

如果你无法在 `php.ini` 中禁用 `register_globals`，你可以在 Apache 正确配置的情况下使用 `.htaccess` 文件来关闭它：

```
php_flag register_globals off
```

### SQL 注入攻击

另一种脏数据攻击，但潜在破坏性远大于前者，是 SQL 注入攻击。与 `register_globals` 攻击结合使用，或仅使用普通的 Web 表单，SQL 注入攻击实际上就是在通常应该只是无害数据的地方插入恶意的 SQL 语句。

SQL 注入利用了缺乏输入清理和数据验证——即在 PHP 构建的 SQL 查询中盲目使用的数据。请查看以下示例，它将访问你在本章前面创建的 WebAuth 数据库：

```
<?php

$username = $_POST['username'];

$conn = mysql_connect(AUTH_DB, AUTH_USER, AUTH_PASS);
mysql_select_db(AUTH_DB, $conn);

$sql = "SELECT * FROM Users WHERE username='" . $username . "'";

mysql_close($conn);

?>
```

看起来无害，对吧？你希望它能愉快地接受从表单发送的任何 `username` 变量值，并查找与该特定用户名相关的所有列。这段代码的问题在于 SQL 查询：请注意 `username` 变量在发送到数据库之前没有经过任何验证、清理或预处理。在大多数情况下，你可能不会注意到任何异常，而且它很少甚至从不抛出错误。

然而，当发送表单的 `username` 字段中输入以下值时，情况会迅速变得恶劣：

```
'; DELETE FROM Users; SELECT 'Ow3rd' AS username FROM Users WHERE '1'='1'
```

仔细观察这个值正在发生什么。它首先终止了查询中在附加 `username` 变量之前的部分，删除了 `Users` 表中的所有信息，然后执行攻击者选择的查询，只是为了关闭查询并匹配最终的后撇号。

当将“邪恶”的 username 值替换到原始查询中时，有效的命令集将如下所示：

```
SELECT * FROM Users WHERE username='';
DELETE FROM Users;
SELECT 'Ow3d' AS username FROM Users WHERE ''=''
```

当发送到 SQL 服务器的数据没有像本例中那样进行转义时，可能会出现各种糟糕的情况。想象一下，如果中间命令是 DROP DATABASE 或 GRANT 命令，那将是多么严重的损害——这是一个糟糕的局面。这个例子是 SQL 注入攻击中可能发生的情况的一个相当简化的案例，但它应该能让你领略到它对数据完整性和系统完整性可能造成的破坏。

与困扰 PHP 脚本的许多常见问题一样，SQL 注入通过一点规划彻底的代码审计实践可以在一定程度上预防。如果配置了 `magic_quotes_gpc` 为开启状态，PHP 在转义表单数据中的“危险”字符方面有你的一臂之力。当 `magic_quotes_gpc` 启用时，PHP 会自动转义任何转义字符，例如后撇号，甚至在你脚本中接触到它们之前。不幸的是，这种行为应用于所有 `GET`、`POST` 和 Cookie 变量，无论它们是否将用于 SQL 语句——大多数时候这可能有点烦人。

为了确保你的数据仅在需要时转义，请在 `php.ini` 中关闭 `magic_quotes_gpc`，并对所有传递给 MySQL 的数据使用 `addslashes()`。`addslashes()` 函数会自动转义任何危险字符，使你的输入不会使 MySQL 出现故障——既针对 SQL 注入攻击，也针对包含特殊字符（如带后撇号的姓氏）的合法数据。

作为第二道防线，确保你在 PHP 中访问数据库的用户仅拥有维持应用程序运行所需的最小权限。在之前的 SQL 注入攻击中，删除所有用户记录实际上会失败——在章节开始时设置该用户时，只授予了 `SELECT` 权限。

SQL 注入攻击的亲戚，文件系统执行攻击，应类似地对待。任何未清理的输入数据，如果成为 `system()` 或 `exec()` 调用的一部分，都应被视为可疑的，因为它们可以像 SQL 注入攻击那样，轻易地通过类似的方式链接在一起，组成一组恶意的系统命令。

### 跨站脚本

虽然 SQL 注入和 `register_global` 滥用主要涉及脏输入数据的使用，但还有另一种攻击依赖于动态输出的不纯净——跨站脚本。

通常缩写为 XSS，跨站脚本是利用未过滤的动态输出，其中攻击者有能力添加或更改页面的生成标记。最常见的情况是在页面输出中添加一小段 JavaScript，然后执行某些不轨行为，例如欺骗另一个用户透露其登录凭据或信用卡信息，或者可能泄露 Cookie 或会话信息以立即实现账户劫持。

# 站点安全性

为了更好地理解攻击的确切流程，请考虑以下场景：

- 1. 攻击者在博客或其他网站上填写评论表单。恶意脚本被包含在评论中。
- 2. 这些评论在页面上显示，脚本保持完整且处于活动状态。



- 3. 一位无辜的用户访问该站点，阅读攻击者的评论，这些评论中可能包含也可能不包含可点击的链接。

- 4. 通过点击攻击者的链接，或仅仅是访问该页面，用户会被要求验证私人信息，例如用户名或密码。

- 5. 用户不知情地提交了私人信息，以为这是正在访问的合法站点所要求的。

- 6. 用户被盗取的信息被路由到互联网上的其他位置，以便稍后进行分析，或者攻击者会通过新信息收到通知。

这是如何发生的？当“受信任”的网站在将特殊字符作为输出或标记发送之前未对其进行适当的清理时，跨站脚本攻击就会变得有效。在网络环境中，这意味着小于符号 `<`、大于符号 `>`、和号 `&`、单引号和双引号，以及动态输出中存在的任何 UTF-8 字符。

幸运的是，PHP 在清理动态输出时为您提供了一系列可供选择方案：

- `htmlspecialchars()`：转义任何和号、小于号、大于号、单引号和双引号，使其成为大多数动态生成的 HTML 的合适选择。

- `htmlentities()`：与 `htmlspecialchars()` 类似，但 `htmlentities()` 除了 `htmlspecialchars()` 涵盖的核心五个字符外，还会转义*任何*具有 HTML 实体等效物的特殊字符。

- `strip_tags()`：从字符串中移除所有 HTML 和 PHP 标签。您甚至可以提供一个允许标签的列表，从而可以白名单化“安全”标签（如格式标签），并移除任何更具危险性的标签（如 `<script>`）。

- `utf8_decode()`：将 UTF-8 编码的字符转换为等效的 ISO-8859-1 字符。

### 其他注意事项

除了直接影响您编写的代码或服务器配置的问题外，在应用的设计、开发和维护过程中，还必须考虑另外几个问题。

最容易解决的问题之一是保持系统最新并应用所有最新的补丁。如果您的操作系统有自动更新核心系统软件的方法，通常是一个好主意去利用它。许多最近的 Web 服务器漏洞实际上是利用了旧版本软件中的缺陷——病毒和蠕虫编写者通常使用供应商发布的关于最近服务器补丁的信息来编写他们知道会影响旧版本的恶意代码。

另一个在更新系统时也不应被忽视的群体是随 PHP 安装的 PEAR 和 PECL 包。两者都可以通过一个简单的命令轻松更新：`pear upgrade-all`。关键在于定期运行该命令，或者更好的是，将其添加为 cron 任务。

在编写应用程序时，您可以采取一些小措施来降低 `register_globals` 漏洞或 SQL 注入攻击的可能性。首先，确保在使用前初始化所有变量；这样就不会有表单或查询字符串变量偷偷混入的机会。其次，确保在生产 Web 服务器上关闭任何错误报告输出。通过禁用错误消息的显示，当发生错误（例如 SQL 查询中的语法错误，或 SQL 服务器的主机名或 IP 地址）时，不会泄露敏感信息。

还有一些其他有助于维护站点安全的事情，并不完全是您输入或配置的内容。黑客访问您站点的一种可能方式涉及一点社会工程学，并且几乎没有或没有实际的计算机入侵。如果您是网站的管理员，负责创建和排查用户登录问题，您处于一个非常严肃的角色，如果没有适当的保护机制，可能会被利用。在许多情况下，黑客只需要做的就是致电网站管理员，假装是一个忘记了他或她密码的用户。如果管理员泄露了该不幸用户的用户名或密码，黑客就立即拥有了该网站的合法登录凭证，而不需要任何网络嗅探或暴力破解攻击。

另一个对站点安全有很大帮助的小习惯是在开发周期内进行频繁的代码/同行评审。通过让同事或同行检查您的代码，反之亦然，您可以帮助在许多明显的安全问题在代码实际面向公众之前很早就暴露出来。

最后，确保您通过访问 Secunia (`http://secunia.com/`)、`CVE` (`http://www.cve.mitre.org/`) 和 CERT (`http://www.cert.org/`) 等安全相关网站以及其他网站，保持对最新安全和漏洞消息的了解。

## 摘要

如您所见，在处理 PHP 驱动的网站安全性时，需要考虑的事项相当多。如果您保持严格的数据清理实践，确保所有进出系统的信息都是有效的，您的站点将能够抵御大多数简单的攻击者。

# 第 8 章

## PEAR 和 PECL

开源的潜在概念是，*当然*，通过协作努力来实现伟大的事情。无数贡献者及其努力之间存在的协同效应推动开源项目不断突破其边界。然而，伴随着这种巨大且多样化的努力而来的是可能会阻碍运动成功的挑战。这些挑战包括组织、协调和方向。如果没有组织，代码编写就不会有标准，也不会有系统的方法来组装软件包。如果没有协调，代码片段将分散在整个互联网上，很可能迷失在写得糟糕的 HTML 页面之间，永远无法被人类看到。如果没有方向，就不会有对未来的展望，也没有让有抱负的贡献者感到兴奋的资源。简而言之，将只是一群技术人员在独立行动，在各自小小的“计算机气泡”中编写和重写与其他人相同的代码片段。然而，众所周知，没有人是孤岛，这就是 PEAR 和 PECL 小组发挥作用的地方，它们提供急需的组织、协调和方向，以便开发者从长远来看都能成为更好的编码者。

通过为开发者提供现成的脚本以完成常见任务，例如连接到数据库或与 XML 文档接口，PEAR 和 PECL 包可以为您节省大量的编码时间和烦恼。

虽然它们都完成类似的任务，但 PEAR 和 PECL 确实存在根本差异，本章将详细解释这些差异。

## 什么是 PEAR？

PEAR（PHP 扩展和存储库）旨在充当迷失的有用类的家园。顾名思义，它是一个代码包存储库，可能由一个或多个文件组成，用于完成常见任务，例如创建 HTML 表单、处理日期和图像，或连接数据库并运行查询。由于这些是每个编码者都会不时使用的功能，因此它们非常适合成为 PEAR 包。

由于开发并发布 PEAR 包有一套严格的编码标准，编码者可以放心，一个包的外观和感受将与其他包保持一致。随着您熟悉它们的使用，您将开始知道要查找什么以及代码是如何构建的。PEAR 包还以其广泛的注释要求和命名约定而闻名，这是许多开源程序严重缺乏的，迫使您承担尝试理解他人逻辑的艰巨任务。

所有新包在包含在 PEAR 分发列表中之前，都必须经过 PEP（PEAR 提案系统）。这一四步过程确保每个包都经过准确性、可靠性和相关性的仔细审查。如果您想了解更多关于 PEP 的信息，可以访问网站 `http://pear.php.net/pepr`。

## 什么是 PECL？

PECL（PHP 扩展社区库）是 PEAR 的一个衍生项目，主要用于容纳那些不再与 PHP 默认安装捆绑在一起的函数组。从 PHP 5 开始，这些扩展可以从常规 PHP 下载中单独下载和安装。但请注意，目前位于 PECL 中的一些扩展现在已经与默认安装捆绑在一起（如 SQLite），或者是 PHP 核心团队外部某人提交的扩展，从未与 PHP 捆绑在一起（如 POP3）。

由于大多数 PECL 扩展曾经是 PHP 标准函数列表的一部分，标准规定它们使用 PHP 的编码标准编写（与 PEAR 的标准不同）。虽然公众仍可以提交包，但提交流程需要事先获得 `pecl-dev` 邮件列表的批准。

## 探索 PEAR

在您深入 PEAR 的世界之前，您应该意识到，由于它是一个基于类的系统，为了正确使用这些包，您对 PHP 中的面向对象编程（OOP）应该相当熟悉。如果您是一位硬核的基于函数的编码者，建议您通过快速教程或简要复习本书的第 2 章来磨练您的 OOP 技能。

您需要的第一样东西是 PEAR 包本身，它使您可以轻松安装或升级新的 PEAR 包。幸运的是，这个管理器随 PHP（版本 4.3.0 及以上）预安装，在您安装、管理和升级其他 PEAR 包时会让您更轻松。主要的 PEAR 包还包括一组错误处理函数，使您可以轻松检测和管理在使用 PEAR 包时遇到的错误。

### PEAR 管理器

正如前面所述，PEAR 管理器的主要目的是协助您管理和使用其他 PEAR 包。随之而来的是一组可以从命令行运行的命令（可能需要或不需要 root 访问权限）。可以在 `http://pear.php.net/manual/en/installation.cli.php` 上找到完整列表，但下表突出了供您参考的主要命令：

## PEAR 命令参考

| 命令 | 功能说明 |
| :--- | :--- |
| `bundle [包名]` | 下载并解压一个 PEAR 扩展 |
| `download [包名]` | 下载某个包但不安装 |
| `download-all` | 下载所有可用的包 |
| `info [包名]` | 显示某个包的信息 |
| `install [包名]` | 下载并安装某个包 |
| `list` | 列出已安装的包 |
| `list-all` | 列出所有包 |
| `list-upgrades` | 列出已安装包中可执行的升级 |
| `uninstall [包名]` | 卸载并删除某个包 |
| `upgrade [包名]` | 升级某个包 |
| `upgrade-all` | 升级所有已安装的包 |

若要使用上述任何命令，只需在命令前加上 `pear`，例如：

```bash
pear info XML-RPC
```

如你所见，这将显示名为 XML-RPC 的 PEAR 包的信息。



此外，还有一些 PEAR 配置变量可供你控制。这些变量主要涉及目录信息和用户偏好设置，大多数情况下默认值即可接受。你可以访问 `http://pear.php.net/manual/en/installation.cli.php` 查看完整列表。不过，下表列出了其中一些更常见的变量：

| 变量名 | 代表含义 | 默认值 |
| :--- | :--- | :--- |
| `bin_dir` | 存放可执行文件的目录 | `/usr/bin` |
| `ext_dir` | 存放加载扩展的目录 | `./` |
| `php_dir` | 存放 PHP 安装程序的目录 | `/usr/lib/php` |
| `preferred_state` | 要下载的首选包状态（stable、beta、alpha、devel 或 snapshot） | `stable` |

若要查看当前设置，请使用 `config-show` 命令（或仅查看单个变量值时使用 `config-get`），例如：

```bash
pear config-show
```

这将显示每个配置变量的描述、变量名以及当前设置。若要更改设置，请使用 `config-set` 命令，例如：

```bash
pear config-set preferred_state devel
```

`config-help` 命令会显示关于特定配置变量的更多信息。

## 安装包

PHP 5 预装了其他几个 PEAR 包，你可以通过运行以下命令（需 root 登录）查找完整列表：

```bash
pear list
```

这将列出已安装的包、已安装的版本以及发布状态（stable、beta 等）。如果你想安装其他包，以下各节将简要概述安装流程。

### CLI 安装

如果你有 root 权限，只需输入以下命令即可安装任何新包：

```bash
pear install [包名]
```

此命令会跳转到 PEAR 网站，下载你指定的包（当然不包括方括号），并将其安装到你的机器上。

### FTP 安装

如果你没有命令行访问权限，或者你当前的 Web 主机未提供你所需的 PEAR 包，你还可以通过完成以下两步来安装包：

- 直接从 PEAR 网站下载压缩包，在本地解压，并将文件上传到你的 Web 站点（保存在 `/var/www/www.yourdomain.com/includes` 目录中）。你也可以上传压缩文件并在主机服务器上解压（同样放入 `/var/www/www.yourdomain.com/includes` 目录）。
- 修改你的 `php.ini` 文件，使其匹配刚才使用的包含路径。

```ini
include_path = ".:./www/includes*"
```

你还可以在每个访问该包的脚本中包含一行代码，例如：

```php
<?php
ini_set("include_path", "/var/www/www.yourdomain.com/includes/" . PATH_SEPARATOR . ini_get("include_path"));

// PHP 脚本的其余部分。
?>
```

此时，你的包已安装完毕，可以使用了。

### 使用已安装的包

一旦包安装完成，使用和访问它就非常简单。只需在脚本开头包含一行引入必要文件的代码，如下所示：

```php
<?php
require_once("HTML/QuickForm.php");

// 现在你可以访问并引用 quickform.php 文件中包含的类、方法和属性，从而轻松创建 HTML 表单。
?>
```

### 简易快速的 PEAR 包

截至目前，已有 318 个 PEAR 包可用于各种领域，而且每天都在增加。虽然本书不会讨论所有这些包，但以下各节将介绍其中一些更常见的包，并突出显示你很可能需要确保已安装的那些。请记住，这些部分保持简洁，但若你需要更强大的功能，它们也会为你指明方向。

#### Auth_HTTP

此包的目的是提供一个类似于 Apache .htaccess 登录框的身份验证系统。这是一种保护网站特定区域密码的简单且便捷的方法。请注意，此包依赖于更强大的 `PEAR::Auth`，而 `PEAR::Auth` 又依赖于 `PEAR::DB` 包，因此在使用 `Auth_HTTP` 包之前，必须安装这两个包。

`Auth_HTTP` 的简单用法如下：

```php
<?php
require_once("Auth/HTTP.php");

$a = new Auth_HTTP("DB", "mysqli://username:password@localhost/databasename");
$a->start();
?>
```

首先，你引入文件 `Auth/HTTP.php`，这使你能够访问正确的包。然后，你使用上述参数实例化一个新的 `Auth_HTTP` 对象。由于你实际上使用的是 `PEAR::DB` 包登录数据库，因此你可以更改使用的数据库类型，并命名其他选项，例如套接字、路径、端口号等。虽然本章稍后将简要讨论此包，但 `PEAR::DB` 包的详细说明可在 `http://pear.php.net/manual/en/package.database.db.php` 找到。接下来，你通过调用 `start()` 函数开始身份验证过程，此时你的页面就受到了密码保护。

当然，这还有很多改进和自定义的空间，你可以更进一步，要求身份验证过程从数据库中的某个表查找用户。你可以通过使用 `$authOptions` 变量来指定登录选项：

```php
<?php
require_once("Auth/HTTP.php");

$AuthOptions = array(
	//使用与前面示例相同的数据源名称（数据库登录信息）
	'dsn'=>'mysqli://username:password@localhost/databasename',

	//指定包含用户信息的数据库表
	'table'=>'users',

	//指定存放用户名的列
	'usernamecol'=>'username',

	//指定存放密码的列
	'passwordcol'=>'password',

	//指定使用的加密类型
	'cryptType'=>'md5',
);

$a = new Auth_HTTP("DB", $AuthOptions);

//指定你的区域名称
$a->setRealm('仅注册用户');

//指定身份验证失败时用户看到的错误消息
$a->setCancelText('<h2>访问被拒绝。</h2>');

$a->start();

//检查用户是否经过授权
if($a->getAuth())
{
	//授权后的文本主体在此处。
	echo "你好，授权用户！";
}
?>
```

由此可见，这提供了一种非常简便的用户身份验证方式。若要检查其他页面的授权状态，只需使用 `getAuth()` 函数即可。

`Auth_HTTP` 包还有其他可以指定的参数，而 `Auth` 包则提供了非常强大的基于 HTML 表单的身份验证系统。你可以在 `http://pear.php.net/manual/en/package.authentication.auth-http.php` 和 `http://pear.php.net/manual/en/package.authentication.auth.php` 分别阅读有关这些包的更多信息。

### Date

尽管 PHP 提供了返回日期和时间信息的内置函数，但此 PEAR 包为你提供了一种便捷的方法，将这些信息转换为常用结果，例如本月剩余天数、当前星期几等。

此包可用函数众多，我们无法为每个函数提供示例。然而，以下各节介绍了 `Date` 类中一些更常用的方法。请访问 `http://pear.php.net/package/Date/docs/latest/Date/Date.html` 查看方法综合列表。

#### Date 类

此类位于主文件 `date.php` 中，并为你提供以下方法：

- `Date`：构造函数方法，创建一个新的日期对象。
- `addSeconds`：向日期添加特定数量的秒数。
- `addSpan`：向日期添加时间跨度。
- `after`：确定一个日期是否晚于另一个日期。
- `before`：确定一个日期是否早于另一个日期。
- `convertTZ`：将日期转换为另一个时区。
- `equals`：确定两个日期和/或时间是否完全相等。
- `format`：根据用户规范格式化日期。
- `getDate`：以特定格式返回日期。
- `getDay`：返回日期对象的月份中的日。
- `getDayName`：以字符串格式返回日期对象在一周中的星期几。
- `getDayOfWeek`：以整数格式返回日期对象在一周中的星期几。
- `getDaysInMonth`：返回日期对象所在月份的天数。
- `getHour`：返回日期对象的小时。
- `getMinute`：返回日期对象的分钟。
- `getMonth`：以整数格式返回日期对象的月份。



- `getMonthName`：以字符串格式返回日期对象的月份。
- `getNextDay`：返回日期对象之后那天的日期。
- `getNextWeekday`：返回日期对象之后那个工作日的日期。
- `getPrevDay`：返回日期对象之前那天的日期。
- `getPrevWeekday`：返回日期对象之前那个工作日的日期。
- `getQuarterOfYear`：以整数格式返回日期对象所在的季度。

## 第 8 章

- `getSecond`：返回日期对象的秒数。
- `getTime`：返回自 Unix 纪元（1970 年 1 月 1 日）以来经过的秒数。
- `getWeekOfYear`：以整数格式返回日期对象对应的年份中的第几周。
- `getWeeksInMonth`：返回日期对象所在月份包含的周数。
- `getYear`：返回日期对象对应的年份。
- `inDaylightTime`：确定当前日期/时间是否处于夏令时。
- `isLeapYear`：确定日期对象的年份是否为闰年。
- `setDate`：设置日期对象的日期。
- `setDay`：设置日期对象的日。
- `setHour`：设置日期对象的小时。
- `setMinute`：设置日期对象的分钟。
- `setMonth`：设置日期对象的月份。
- `setSecond`：设置日期对象的秒。
- `setTZ`：设置日期对象所在的时区。
- `setYear`：设置日期对象的年份。

以上就是 `Date` 类的所有内容。还有两个其他类由 `Date` 类使用，但它们也可以直接使用；它们是 `Date_Span` 和 `Date_TimeZone` 类。如果你需要比 `Date` 类提供的功能更具体的东西，比如返回所有可用时区的列表，或者确定服务器的默认时区，这些类中包含了许多特定的方法。

### 快速示例

以下是一个快速示例，展示了使用 `Date` 包输出诸如一年中剩余周数等信息是多么简单：

```php
<?php
require_once("date.php");

$currweek = new Date();

$weeksleft = 52 - ($currweek->getWeekOfYear());
echo "There are " . $weeksleft . " weeks left in the year.";
?>
```

如你所见，当你试图完成更复杂的日期计算或处理时区时，如此简单的操作确实可以极大地简化你的工作。

### DB

这是 PEAR 包，允许你轻松连接和查询数据库。还有许多其他与数据库相关的包可供参考。例如，`MDB` 与 `DB` 类似，但提供了更多的可移植性。`DB` 应该在标准配置下工作，但如果你遇到兼容性问题，可以尝试其他替代方案。事实上，PEAR 专门致力于一个处理数据库的包类别，可以在 `http://pear.php.net/packages.php?catpid=7&catname=Database` 找到。

在接下来的几个示例中，你需要以下信息：

- `MySQL`：你的数据库类型
- `testdatabase`：数据库名称
- `testtable`：数据库表
- `username`：访问数据库的用户名
- `password`：用户的密码
- `localhost`：服务器名称
- `field1`、`field2`：你将查询的字段

这将帮助你在自定义包的安装时“填空”。

#### 连接数据库

为了连接到数据库，你必须向新的数据库对象传递正确的数据源名称（DSN）。语法如下：

```php
<?php
require_once('db.php');

$dsn = 'mysql://username:password@localhost/testdatabase';

$db = DB::connect($dsn);
if (PEAR::isError($db)) {
    die($db->getMessage());
}

echo 'Connected successfully. Now what?';
?>
```

如你所见，连接只需要这些步骤，更重要的是，它会报告过程中可能发生的任何错误。再次说明，请随时查阅官方 PEAR 文档，获取有关连接数据库时可设置的各种选项的详细说明，例如端口号或协议。该文档可在 `http://pear.php.net/manual/en/package.database.db.intro-connect.php` 获取。现在尝试查询假想表中的假想字段。

#### 查询数据库

要查询数据库，你需要传递表名和你期望的过滤器，因此输入以下内容：

```php
<?php
require_once('db.php');

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
//also switching AssocIative mode
while ($res->fetchInto($row, DB_FETCHMODE_ASSOC)) {
    echo $row['field1'] . "," . $row['field2'] . "\n";
}
?>
```

这只是该包的一个样本。你还可以用它做很多事情，例如从多个查询中获取结果集，以及自动准备和执行常用的 SQL 语句。

### HTML_CSS 和 HTML_Page

这些包允许你动态创建 CSS 样式表，并轻松地将它们合并到新的 HTML 页面中。`HTML_Page` 还能为执行其他功能，但本示例专注于创建一个新的 CSS 样式表：

```php
<?php
require_once('HTML/CSS.php');
require_once('HTML/Page.php');

$css = new HTML_CSS();

//set the styles
$css->setStyle('body', 'background-color', '#FF00CC');
$css->setStyle('body', 'color', '#ffffff');
$css->setStyle('h1', 'text-align', 'center');
$css->setStyle('h1', 'font', '16pt verdana');
$css->setStyle('p', 'font', '12pt verdana');

//create a new page
$p = new HTML_Page();
$p->setTitle("Testing the CSS");

$p->addStyleDeclaration($css, 'text/css');
$p->addBodyContent('<h1>Wow, this background is really bright</h1>');
$p->addBodyContent('<p>This should wake you up.</p>');

$p->display();
?>
```

使用简单的 `if` 或 `switch` 语句，你可以使用类似这样的内容，根据人员的授权级别、正在使用的浏览器或操作系统类型、时间或日期，或者你可以想到的任何其他条件，动态创建样式表。

### HTML QuickForm

该包的目的就是快速且轻松地创建 HTML 表单。它易于使用，但相对健壮，并允许相当程度的自定义。看看一个快速示例：



```php
<?php
    require_once ("HTML/QuickForm.php");

    //create a new form object
    $form = new HTML_QuickForm('firstForm');

    //add two input fields; this is completely customizable
    $form->addElement('text', 'name', 'Your full name', array('size' => 50,
        'maxlength' => 255));
    $form->addElement('text', 'email', 'Your email address', array('size' => 50,
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

通过这个小程序，你创建了一个用户表单，验证了必需字段（包括电子邮件字段），并将输入收集到一个整洁的小数组中供你使用。你可以设置任意数量的规则，让你的脚本确保输入了必需字段，它们是否具有正确的格式（数字、字母等），并且如前所述，检查诸如格式正确的电子邮件字段之类的内容。你还可以设置默认值以及你可以使用表单实现的其他任何功能（例如上传文件并使用图像作为“提交”按钮）。

### HTML Table

使用这个包，你可以轻松输出数据表格，无论是从数据库查询的结果集中获取的数据，还是位于某个数组中等待你解放的数据。快速查看一个示例，看看这个包使用有多简单：

```php
<?php

require_once ( "HTML/Table.php" );

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
$table -> setAutoFill(true);

//get some data for our table
$rows = array(
 '0' => array("Number One", "Number Two", "Number Three"),
 '1' => array("Numero Uno", "Numero Dos", "Numero Tres"),
);

//populate the table
for($nr = 0; $nr < count($rows); $nr++) {
 //the header row comes first
 $table -> setHeaderContents( $nr+1, 0, (string)$nr );
 for($i = 0; $i < 3; $i++) {
  if("" != $rows[$nr][$i])
 //the cell contents come next
 $table -> setCellContents( $nr+1, $i+1, $rows[$nr][$i] );
 }
}

//set background for every other row
//skip the first row so we use a value of 1 to start
```

```php
$altRow = array("bgcolor"=>"#FFFFCC");
$table -> altRowAttributes(1, null, $altRow);

//set header info for each cell of the table
//based on coordinates, 0,0 is top left cell.
//the third value is the contents to be shown
$table -> setHeaderContents(0, 0, " ");
$table -> setHeaderContents(0, 1, "Field 1");
$table -> setHeaderContents(0, 2, "Field 2");
$table -> setHeaderContents(0, 3, "Field 3");

//set attributes for the header rows and first column
//first row and column = 0.
$hrAttrs = array("bgcolor" => "#FFFF4D");
$table -> setRowAttributes(0, $hrAttrs, true);
$table -> setColAttributes(0, $hrAttrs);

//send it to the browser
echo $table->toHTML();
?>
```

你可以想象，基于用户输入或数据库查询结果来创建表格是多么简单，而且只需在这些地方改变几个变量，你就能实现高度的自定义。

### 还有什么其他内容？

去查看一下 PEAR 包的完整列表（位于 `http://pear.php.net/packages.php`），你将开始欣赏 PEAR 社区的广度与深度。可用的优秀包如此之多，以至于本书篇幅有限，无法涵盖所有包。除了本章讨论的内容外，以下是一些更有用的主题简要列表：

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

## 第 8 章

## 探索 PECL

虽然 PECL 不像 PEAR 那样广泛，但这并不意味着它没有价值。可用包的文档和功能范围比 PEAR 有限。许多 PECL 包仍处于测试阶段，具有实验性质；因此，使用这些包可能需要一些适应过程。然而，PECL 中包含了一些非常有用的（即使不是非常具体的）包，我们将快速查看其中一些更流行的包，以让你了解它们的功能。如果你想要对 PECL 包进行更详细的解释，我们在第 10 章中对 PDFLib 做了这样的处理。

### Fileinfo



Fileinfo PECL 包是 PECL 站点上下载量最高的包之一，而且它非常实用。通过这个扩展，你可以获取关于文件的各种信息，例如 MIME 类型。可以从 `http://pecl.php.net/Fileinfo` 下载此包。

该包的文档有限，这与其他许多 PECL 包的情况类似；然而，PHP Wiki（`http://www.wiki.cc/php/Fileinfo`）上有一篇简略涉及此包的 Wiki 文档。

### PDO

在撰写本文时，PDO 仍处于测试阶段并被视为实验性的，但它对 PHP 数据库交互的未来极具潜力。该包的目的是与数据对象接口配合，允许你随时更改数据库类型。你不再需要使用针对特定数据库的函数（例如 `mysql_connect` 或 `pg_connect`）进行编码，而是可以创建一个负责处理这些事务的新 PDO 对象。然后，只需在对象实例化期间更改一个参数，即可从 MySQL 切换到 Postgres（或许多其他数据库）。你可以从 `http://pecl.php.net/package/PDO` 下载 PDO。

随着 PDO 影响范围的扩大，其文档也在增加。在 PHP 手册（`http://us3.php.net/manual/en/ref_pdo.php`）以及前面提到的 PHP Wiki（`http://www.wiki.cc/php/PDO_Basics`）中都有关于此扩展的文档。

### Xdebug

这是另一个可以在 `http://pecl.php.net/package/Xdebug` 获取的热门 PECL 包。其功能是通过提供关于代码、激活、执行和变量值的宝贵信息，协助 PHP 开发人员调试脚本。它还提供了内存分配、防止无限循环，以及堆栈和函数跟踪功能。

与其他包相比，该包的文档更加详尽；它甚至拥有自己的网站，地址为 `http://www.xdebug.org`。

#### 总结

现在你应该已经具备了深入研究 PEAR 和 PECL 的条件，能够停止反复重写相同的代码。一旦你熟悉了 PEAR 和 PECL 的配置，也许你会将一些你编写的代码提交给大众作为新包，从而跻身于享有盛誉的贡献者行列。

## 9

## 代码效率

你提供页面的速度越快，你的网站在用户体验到延迟的情况下就能支持更多的并发。本章介绍了提高网站性能的方法，以及识别哪些方法可能最有效。

“用更少的时间展示更多页面”是其基本原理，但就像有汽车爱好者把所有空闲时间都花在钻进汽车内部试图从四分之一英里中再省下十分之一秒一样，也有网站开发人员希望将登录页面的显示时间再减少一毫秒。事情做过了头！

你不想在无人察觉的改进上浪费时间，因此本章的第一部分将展示两个案例，以说明即使巨大的改进有时差异也可能很小，微小的改进却能带来巨大差异，以及在动手之前理解整个系统是多么有价值。

你的程序运行在 PHP 上，PHP 运行在你的 Web 服务器上，并与你的 DBMS 通信，它们都运行在你的操作系统上，而操作系统运行在物理硬件上。随后的部分将寻找所有这些方面中改进的机会，并确定哪些需要改进的技术。

最后，还有几个微小的杂项代码调整，可能会让登录页面的显示快上毫秒。之所以在此列出，是因为如果你从一开始就知道并使用它们，就不会在以后试图花时间去修改现有代码引入这些调整，那将是时间的浪费，而这段时间本可以更好地用于其他事情。

## 为什么要麻烦？

需要问自己的第一个问题是“我*需要*做什么吗？”如果你还没开始编码，答案显然是“需要”——花时间规划你的程序应该做什么，并尝试培养一种感觉，了解其性能可能在哪些地方会拖慢。但如果你有一个正在运行且你试图调优以使其更快的网站，请自问这样做是否真的值得折腾。运行速度是否太慢不符合你的要求？哪部分？你的调优会让它更快吗？快多少？并且你确定在过程中不会弄坏什么东西吗？通过考虑其中一些问题，你可以避免在无益的事情上浪费大量时间和精力，如果幸运的话，你会发现一个微不足道的更改能为你带来巨大的性能提升。

### 用很少换取很多

在我以前工作的一家公司里，有一台用于生成报告的计算机。软件是 Windows NT4 和 Microsoft Access 97（这是在 2004 年），安装的内存只有 32MB，打印报告是一项耐心的考验。当它重绘屏幕时，你可以去喝杯咖啡。人们谈论升级新电脑，因为它“太慢了”。

“简单”的答案——无需分析就能得出的答案——是替换现有机器为一台新电脑，安装最新版本的 Windows 和 Access，然后设置网络用户账户，并花一天时间处理此类升级不可避免地引发的混乱。但进行了分析，方法是按下 Ctrl-Alt-Delete 并调出 NT 的任务管理器及其进程列表，查看在计算机用于生成报告时每个进程花费了多少时间。（如果你不熟悉 Windows 中的这个过程，想象一下使用 GUI 表格小部件的简化版 `top(1)`。）

列表中最显著的特征是条目“System Idle Process”（系统空闲进程）。它从未低于 85%。在二十分钟的运行中，处理器*实际上在做某事*只有三分钟；其余时间它都在等待内存交换于 RAM 和磁盘之间。计算机*本可以*比现在快六倍以上，*要是*它没有被仅有的 32MB 内存所拖累的话。256MB 就足以移除瓶颈；报告的生成时间将短于你走到打印机的时间；芯片会比新机器和新软件许可证便宜得多；并且安装导致的停机时间将从一天缩短到大约五分钟。

### 用很多换取很少

在 C 语言中，一个常见的习惯用法是将 `a<<3` 写为代替 `a*8`，用于将变量乘以八。这当然有效，因为在二进制中，乘以 8（或 2³）等同于将所有位向左移动 3（即 lg(8)）位。这能应用于 PHP 吗？简短的回答是肯定的。但与在 C 中一样，节省的是纳秒级别。例如，在我的 2.6 GHz P4 上，差异在 PHP5.0.3 中是 50ns，在 4.3.11 中是 3.5ns，版本之间唯一的显著差异在于位移速度。你的结果可能会有所不同。顺便说一句，`8*5` 比 `5<<3` 更快。

虽然在需要定期执行数百万次此类乘法的环境（频繁到现代 C 编译器可以自行识别 `a*8` 并将其转换为 `a<<3`，*无论如何*都是如此）中*榨取*这样的节省是*有道理的*，但这对于基于 Web 的应用程序并不典型。更重要的是，在 PHP 中，两个“等效”操作在极端情况下具有*不同*的行为：位移总是产生整数结果（可能为 0 甚至负数：`1073741824<<1==-2147483648` 和 `-2147483648<<1==0`），而如果需要容纳结果，乘法将返回双精度浮点数（`1073741824*2==2147483648` 和 `2147483648*2==4294967296`）。此外，你必须记住，虽然*乘法*的优先级高于加法，但位移的优先级*较低*：它是 `5+$a+$b*8`，但却是 `5+($a<<3)`。

## 代码效率

这一切都值得吗？你花多长时间将操作写成乘法，又花多长时间写成按位移位？你花了多长时间来验证你写的是正确的？修复因极端情况下的行为差异或优先级差异遗忘等导致的问题需要多长时间？未来花在修改代码（比如将乘以 8 改为乘以 9）上的时间呢？（你不能只搜索 8 的实例；你还必须搜索 3 的实例，而且为什么你不使用命名常量？）该操作需要执行多少次才能节省与你花时间确保使用更快选项相同的时间量——这里的纳秒，那里的纳秒？并且该操作被执行这么多次之前需要多久？

重点在于，你的时间比计算机的时间更有价值。比你的时间更有价值的在线时间是访问你网站的访客的时间。因此，不要浪费时间去试图将页面处理时间缩短几纳秒：即使在异常繁重的使用下，网站访客也注意不到这种差异。

## 比较字符串速度——基准测试示例

PHP 有几种将字面量字符串与变量结合的方式，以及三种引号字符串的方法。这三种引号方法分别是使用单引号、双引号和 heredoc 语法。将变量插入字符串可以通过使用连接运算符、双引号和 heredoc 引号字符串中的变量插值，以及 C 风格的字符串格式化函数来实现。时不时地，好奇的程序员会问哪种方法是“更好”的。“更好”可以有多种定义：它更快吗？它使源代码更具可读性吗？它更简单且更不容易出错吗？就可读性和简洁性而言，辩论势均力敌：如果某一种方法明显优于其他方法，那么自然选择会让大型应用程序的资深开发者使用这种优越的方法而排除所有其他方法。多年来似乎没有发生这种选择的事实表明，这些差异并不显著到足以出现在行业范围内的最佳实践文档或编码标准中。

单引号字符串是否比双引号字符串快要容易量化得多。如果你被迫给出是或否的回答，那么最安全的说法是“是”，但现实情况比这更复杂。

与任何关于现实世界的问题一样，不先获取一些事实是无法回答的。作为一个初始实验，你可以编写以下代码：



```php
<?php
$variable = 'string';

$start = microtime(true);
for($i=0; $i<1000000; ++$i)
{
    $string = "this string has a $variable embedded into it";
}
$laptimie = microtime(true);
for($i=0; $i<1000000; ++$i)
{
    $string = "this string has a "$variable." inserted into it";
}
$finish = microtime(true);

echo "Variable interpolation required ', $laptimie-$start,' seconds for one million iterations.\n";
echo "Variable concatenation required ', $finish-$laptimie,' seconds for one million iterations.\n";
?>
```

第一次运行此脚本时，我得到的插值和连接时间分别为 6.81 秒和 1.72 秒。然而，第二次运行，我得到的时间是 6.58 秒和 1.71 秒。这种变异性是由于我运行的计算机正在做的事情不仅仅只是运行脚本。它对时间有其他需求，它花费在这些其他需求上的时间被计入了该脚本完成所需的时间。当脚本第一次运行时，操作系统必须为 PHP、脚本及其数据组织内存空间，其中一些组织在脚本运行时发生（然而，其中大部分在脚本开始执行之前就已经发生了，因此不会出现在计时中）。但紧随其后的第二次运行，将处于一个已经有合适的空闲空间块的环境中，因此启动速度快得多。

这就意味着你不能信任仅运行一次的结果：计时波动的方式太多，而其中许多是你无法控制的。必要的是运行脚本——从头到尾——多次，并取结果的平均值。对于插值，10 次运行的时间在 6.57 到 6.86 秒之间，平均值为 6.77；对于连接，范围是 1.65 到 1.71，平均值为 1.70。如果你喜欢，你可以对数据投入更多的统计火力，但它似乎很清楚连接比插值快大约四倍。

但这并不是全部。如果时间取决于字符串*有多长*，或者有多少*多少个*变量正在被连接或插值呢？我们不应该也测试*这些*的变化吗？

以下是一个命令行 PHP 程序，用于运行此类测试。它并不计时*自身*在连接或插值变量时的时间，而是写入一个*单独的* PHP 脚本，然后通过命令行调用它，从而不仅计时脚本本身，还包括启动 PHP、加载脚本和关闭所花的时间。它针对一系列初始字符串大小（64 到 26176 个字符，步长为 512）和插值/连接数量（0 到 100）进行实验。它每个实验执行五次，并将平均运行时间写入单个日志文件。（如果两万五千个单独实验太多（它可能需要*大约*四个小时左右的时间），则可以按需缩小范围，但应该保留对每个大小/数量组合测试多次并取结果平均值的做法。如所写，它计时变量插值——取消注释第 59 行并注释第 58 行（即 `str_replace()` 调用）将其改为计时连接：

```php
<?php
function generate_test($string)
{
  $code = '<?php
  $interpolated="$badgers!";

  for ($i=0; $i<100; ++$i)
    $string = "".$string."";
  ?>';
  $temp_file = tempnam('', 'xuntest');
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

$log = fopen('logfile.txt', 'wb');
for($string_size=1<<6; $string_size<=26176; $string_size=+1<<9)
{
    $generic_string = str_repeat("wibble splunge!\n", $string_size);
    $real_string_size = 16* $string_size;
    $all_positions = range(0, $real_string_size-1);
    for($num_variable_interpolations=0; $num_variable_interpolations<100;
        ++$num_variable_interpolations)
    {
        echo $string_size, "\t", $num_variable_interpolations, "\n";
        $string = $generic_string;
        if($num_variable_interpolations==0)
            $positions = array();
        else
            $positions = array_rand($all_positions, $num_variable_interpolations);
        if(count($positions)==1) $positions = array($positions);
        foreach($positions as $position)
        {
            $string = substr($string,0,$position) . '$' . substr($string,$position);
        }
        $string = str_replace('$', '{interpolated}', $string);
        // $string = str_replace('$', '.', 'interpolated', $string);
        $file = generate_test($string);
        $runtime = run($file);
        unlink($file);
        fwrite($log,
            $string_size, "\t", $num_variable_interpolations, "\t", $runtime, "\n");
    }
}
fclose($log);
?>
```

从代码中的最后一个 `fwrite()`，你可以推断出保存数据的格式：每个实验一行，由字符串大小（插入变量之前）、插入变量的数量和秒数组成。然后你可以将此数据读取到你首选的数据分析或绘图软件中进行探索。

## 第 9 章

时间相对于字符串长度和变量数量的结果图，在拼接（见图 9.1）和插值（见图 9.2）中看起来大相径庭。

![](img/fd2e7361878181c2b12e30301ff3e182_229_0.png)

![](img/fd2e7361878181c2b12e30301ff3e182_229_1.png)

也许在这些图表中你首先能注意到的是，当在双引号字符串中进行插值时，变量的数量几乎无关紧要。迹象表明，当变量数量是 32 的倍数时，处理速度特别慢。由于改变变量数量是通过内层循环进行的，对于给定变量数量的实验是在运行期间广泛间隔的时间点执行的，排除了除外部来源的异常及时瞬态延迟之外的所有因素。

比较变量数量非常小时的两张图表，首先不寻常的是看到拼接的速度最初会下降，其次是插值速度急剧上升。仔细检查后发现，当变量数量为 0 时，双引号和单引号字符串速度相同，只有当有变量需要插值时，双引号字符串才会变慢。这是因为双引号字符串在程序加载期间，即在词法分析阶段，会被扫描以寻找变量。这是一次性的开销，甚至比我们要初以为的还要小：无论单引号还是双引号字符串的内容都必须被扫描，以便定位转义序列和字符串的实际结尾。唯一的真正区别是，当存在变量时，扫描双引号字符串会按顺序生成多个标记。



总体而言，两个图表的形状具有独特性。这种差异可以通过使用“大 O 表示法”来形式化，该表示法用于在程序分析中描述算法相对于给定问题规模的“大小”或“速度”。虽然它可以给出严格的技术定义，但只需将 `O(f(n))` 理解为意味着算法行为的图形在 `n` 变得越来越大时“看起来像” `f(n)` 的图形即可：

```
O(f(n)) = 满足存在正常数 c 和 n₀ 使得对所有 n≥n₀ 有 0≤g(n)≤cf(n) 的函数 g(n) 的集合
```

在这种情况下，双引号插值的图形不随 `v`（被插值的变量数量）变化，仅随 `l`（字符串长度）线性变化（也就是说，当字符串长度翻倍时，速度变为两倍慢）。用大 O 表示法描述，这就是 `O(l)`。单引号拼接的图形更复杂。如果你固定字符串长度，并观察随着变量数量变化的图形单一切片（这种切片在图 9.1 中显示在图形顶部边缘从左到峰值处），它看起来相对于 `v` 相当线性。如果固定变量数量并允许字符串长度变化（从峰值向右下方延伸的脊线），它会弯曲成暗示抛物线的形状。总体而言，这两种影响似乎相乘，给出了大 O 描述 `O(Pv)`。

从长远来看，`I` 的增长速度慢于 `P*v`，事实上，对于包含许多变量的长字符串，插值比拼接更快。然而，对于较短的字符串或较少的变量，拼接仍然占优。

大 O 表示法只关心随着问题规模变大时程序在长远会发生什么，忽略了仅在小问题实例中出现的因素。你会记得，当没有变量参与时，两种方法速度相同（因为都只包含单个字符串），但单引号拼接会稍微加速然后再变慢，而双引号插值一旦引入单个变量就会急剧变慢，并且不会恢复。大 O 表示法说，从长远来看，变量插值比拼接更快，但你必须拥有多千字节且包含数十个变量的字符串才能实际看到这种情况。

你可以看到，即使在这个非常简单的例子中，仅考虑两个因素，在寻求“最佳”的明确答案时，潜在细微差别也很多。在这个相对琐碎的例子中，你可以进行更深入的调查，而对于更复杂的问题，在得出任何结论之前，你通常必须这样做。但这里是结束这个例子的一个好时机，除了注意到在所有记录的实验中最慢的时间是 3.7 秒之外。

### 反直觉的结果

与 C 不同，C 会被转换为机器代码，这与你实际写的内容并没有太大差别（该语言被描述为“带有野心的汇编器”），你的 PHP 程序是由 PHP 引擎模拟的虚拟机运行的。在性能调优方面，这可能造成困难，因为预测什么有效什么无效变得更加困难。这将在后面讨论，但现在你可能希望思考以下测试代码的结果：

```php
<?php
$3=0;
$start_test_1 = microtime(true);
for($i=0; $i<1000000; $i++) $3++;
$end_test_1 = microtime(true);

$3=0;
$start_test_2 = microtime(true);
for($i=0; $i<1000000; $i++) ++$3;
$end_test_2 = microtime(true);

$3=0;
$start_test_3 = microtime(true);
for($i=0; $i<1000000; ++$i) $3++;
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

有许多技术和工具用于估计程序的速度，它们应在启动加速站点的任务之前、期间和之后使用，以免你花时间在没有任何显著差异的更改上，或者更糟糕地，减慢你的站点速度。从广义上讲，它们可以分为两个主要类别：*基准测试*是你在实际实施某事之前进行实验以确定最佳方法时所做的，而性能分析涵盖你在真实事物上进行的实验，以查看其实际表现如何。显然，两者之间有很大的重叠；许多技术和工具是相同的（因为工具并不一定关心你正在使用的代码是自然的还是合成的）。在操作系统和 PHP 层面都存在帮助你进行这些工作的工具。

### PEAR 基准测试

你已经在上一节中看到基准测试的例子。它们是临时构建的，但它们共同的基本思想足够普遍，值得被抽象为一个独立的类：

- 启动计时器（记录当前时间）。
- 执行某些操作。
- 停止计时器（再次记录当前时间）。
- 将停止时间与启动时间进行比较，以确定经过的持续时间。
- 大量重复步骤 1–4，累积持续时间。
- 查看结果。

对此的一个明显增强是为计时器添加标签，这样多个计时器可以独立启动和停止。同样好的是，如果计时器还能包含关于它们覆盖的代码特定部分所花费时间的信息。PEAR 基准测试类提供所有这些功能。PEAR 和 PEAR 包的安装在第 8 章中介绍；因此你已经处理好了这一点，并准备好开始使用它。

要使用基准测试类重复最初的字符串构建实验，你可以编写以下代码：

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
$timer->setMarker('lptime');
for($i=0; $i<1000000; ++$i)
{
    $string = "this string has a .".$variable." inserted into it";
}
$timer->setMarker('finish');

echo "Variable interpolation required "$timer->timeElapsed('Start','lptime'),"
```

# 第 9 章

```php
seconds for one million iterations.\n";
echo "Variable concatenation required *,".Timer->timeElapsed('laptops','finish'),"
seconds for one million iterations.\n";

$timer->stop();
$timer->display();
```

`Benchmark/Iterate` 继承自 `Benchmark/Timer`，并提供了一个 `run()` 方法，你需要将希望测试的函数名称传入该方法。在选择使用哪一个时，有两点需要考虑。其中一点是，调用函数本身需要花费一点时间。另一点是 `Benchmark/Iterate` 会为每次单独的实验保留其计时结果。进行大量实验意味着需要一个很大的数组，这就是为什么下面的代码只运行了一万次实验而不是一百万次：



```php
<?php
require 'Benchmark/Iterate.php';

$variable = 'string';

function interpolate($variable)
{
    $string = "this string has a $variable embedded into it";
}

function concatenate($variable)
{
    $string = "this string has a *,".$variable."* inserted into it";
}

$interpolation_benchmark = new Benchmark_Iterate;
$concatenation_benchmark = new Benchmark_Iterate;

$interpolation_benchmark->run(10000, 'interpolate', 'string');
$concatenation_benchmark->run(10000, 'concatenate', 'string');

$interpolation_result = $interpolation_benchmark->get();
$concatenation_result = $concatenation_benchmark->get();
?>
```

这两个结果变量都是数组：`$interpolation_result['iterations']` 记录了测试运行的次数，而 `$interpolation_result['mean']` 记录了平均值。`Benchmark` 类如果可用会使用 `bmchat` 函数以在计算此值时保持准确性。取消设置这两个元素后，你会剩下一个按数字索引的数组，其中包含每次迭代的单个时间，以便你可以执行你认为相关的其他统计测试。

### top 和 ab

之前提到的 NT4/Access 报告生成器 anaconda 源自 Windows 世界，并提到了其任务管理器的使用。随类 Unix 操作系统附带进程监控工具名为 `top`，它提供的信息量要丰富得多。同时，Apache 发行版包含了 `ab` ApacheBench 程序，它测试你网站的“尖头”部分：你能多快地提供服务？并排使用这两者往往很有启发性：用 `ab` 来查看你的性能表现如何，用 `top` 来查看为了获得该性能投入了多少努力。

当然，你需要在 web 服务器本身上运行 `ab`；`ab` 可以在同一位置运行，但为了公平起见，值得在本地网络的另一台机器上运行它。在比本地网络更远的地方运行会引入额外的延迟，阻碍你压力测试服务器的尝试。例如，你可以打开工作站上的终端窗口并 `ssh` 到 web 服务器；在工作站上运行 `ab`，在服务器上运行 `top`，两个终端窗口并排显示。

简单来说，`ab` 是一个加速版的 http 客户端。典型的调用方式是让它连续紧密地请求同一页面一千次，从而模拟一千个用户几乎同时访问。它收集关于服务器响应这些请求所花费时间的统计信息，以及是否有请求未能得到满足。看看这个例子：

```bash
ab -n1000 -c10 http://bowman/page2test.php
```

这条命令告诉 `ab` 总共请求 `page2test.php` 一千次，最多有十个请求并发运行。因此，它发出十个请求，一旦其中一个请求得到满足且响应已接收，它就发出第十一个请求，直到总数达到为止，不会松懈。

在发出它的一千个请求后，它会展示一份它所收集统计信息的报告。这些包括整个运行的总时间、响应的大小、进行了多少个请求以及有多少个失败、它能够多快地发出请求。对应于请求得到满足的速率、响应本身以 bps 为单位的传输速度，以及平均响应和最慢响应所花费的时间。

对于基准测试来说，调整总请求参数 `-n` 的重要性相对较低；这个参数只需要至少与 `-c` 一样大，并且足够大以使整体统计结果平滑，避免测试开始时的瞬态行为干扰结果。调整并发参数 `-c` 则更有信息量。从 `-c1` 开始，你将 `-c` 设得越低，除非你真的愿意等待那么久，否则可以将 `-n` 设得越低，你可以看到服务器是否能够一次响应一个请求。随着你增加 `-c`，并发请求的数量增加，你可以观察服务器是否处理得了不断增加的负载。举个例子，随桌面版 Microsoft Windows 附带的 IIS 版本被限制为最多 10 个并发请求。一旦 `-c` 超过 10，你将开始收到失败的请求。是的，你可以使用 ApacheBenchmark 测试其他服务器；在某种程度上，它被称为“Apache”是因为它是 Apache Group 的产品。随着负载增加，传输速率会下降，发出请求的速率会增加，最终请求开始失败。如果你感到施虐欲大发，可以模拟被 Slashdot 攻击的效果：用 `n100000 -c1000` 攻击你的服务器，看着它“腹股沟疝”。

同时，在另一个终端窗口里是服务器视角下正在发生的事情。当你运行 `top` 时，首先要看的是负载平均值。给出的三个数字分别是过去 1 分钟、5 分钟和 15 分钟内活动进程的平均数量。即正在运行或等待运行，而不是当前空闲的进程。如果把服务器想象成银行，处理器想象成出纳员，进程想象成顾客，那么负载平均值就代表了正在被服务或排队等候的人数。显然，如果出纳员不够多，排队的人会变得越来越多且越来越烦躁。同样，过高的负载平均值意味着进程花了太多时间在排队等待运行机会。因此，发起这些进程的请求者也不得不等待结果，他们或他们的浏览器甚至可能放弃——这对你的网站形象不好。

理想情况下，你希望负载平均值略低于服务器处理器数量，以便保留一些余量来处理异常高的负载。短暂的激增是可以容忍的，前提是它们确实短暂。15 分钟负载值不应出现激增；如果出现了，这表明当服务器忙碌时它忙得过头了，并且正在形成一个需要很长时间才能处理完的积压。足以显著影响 15 分钟平均值的尖峰无法被迅速解决。

在 `top` 的显示中，负载平均值下方是每个处理器的活动水平，以百分比表示。这也应该保持在相对较低的水平，以便为 Slashdot 效应或最新蠕虫的攻击尝试留出余地。如果机器是专用的 web 服务器，那么当没有提供服务时处理器持续的活动可能暗示它正在做不该做的事情。检查进程列表本身，查看哪些进程正在使用处理器。你可能能够移除其中一些。一个只提供静态网页或文件的网站几乎不会产生任何 CPU 负载——一台 1980 年代风格的处理器完全有能力以磁盘读取速度传输数据——但动态生成的页面确实会在此处遇到瓶颈。

另一方面，即使 CPU 几乎空闲，服务器也可能在满负荷运行。回想一下 Windows 报告生成器的轶事，当时简单的任务花费了永远的时间，而处理器 85% 的时间都在“玩拇指”，最终确定问题在于机器内存 `RAM` 太少。

在 `top` 的 CPU 使用率报告下方是可用内存、已用内存以及 `RAM` 和交换文件 `swap file` 中剩余空闲内存的报告。你希望尽可能少地依赖交换文件，理想情况下完全不依赖。

## 硬件改进

所以，你决定网站运行缓慢。你已经剖析了发生的事情，现在准备着手改进。最深刻的改进来自于记住你的服务器存在于现实世界，并受物理定律支配。你无法改变物理定律：你必须适应它们。

首先要检查的是你对外部世界的连接。你需要一根粗大的管道。如果你的服务器负载较轻但网络流量已达最大值，那么你的连接就是瓶颈。

解决那个问题后，检查处理器。如果它始终运行在其范围的上限，那么升级可能为你提供更多喘息空间。你的机器有多旧？两年？你可能会发现一台新机器比当前的快两倍以上。当然，更换计算机是你所能做的最基础、风险最大且几乎肯定昂贵的改变。如果能把新机器搬进来，把旧机器的线缆换到新机器上，进行硬盘移植，然后启动就好了，那该多好。但事情似乎从来不会那么顺利。

如果处理器相当空闲，但内存紧张，那么增加 `RAM` 是你的下一个优先事项。除了流量最大的站点或拥有最大数据库的站点，这些数据库通常由 `MySQL` 缓存在 `RAM` 中以加快访问速度外，`512MB` 对于所有站点都绰绰有余。

对于主要提供静态页面或文件的站点，`RAM` 比处理器速度更重要——从机器的一部分将数据块移动到另一部分非常简单，因此能够快速计算出如何移动它，不如能够一次性移动大量数据重要。

磁盘访问是一个相对缓慢的过程。建议升级到吞吐量更大的快速硬盘。如果你的当前硬盘容量即将用尽，那么与其将所有数据迁移到一个更大的硬盘上，不如考虑增加额外的硬盘。即使你的当前硬盘尚未接近满容量，增加额外硬盘并在其上分布内容也可能提升访问速度。各磁盘的读写磁头将同时工作，且磁头需要移动的距离会比单个大容量硬盘上的磁头短。磁盘的转速也不需要达到那么高。

## Web 服务器优化

`Apache` 天生具有高度可配置性，有许多设置可供调整，以优化其行为的某个方面或另几个方面。有些设置可以减少 `Apache` 所需的内存量，而另一些则旨在减少每个进程执行的工作量。



启动 Apache 时，它做的第一件事就是启动六个（确切数字当然可配置）`httpd` 实例。这些是实际处理 HTTP 请求的进程。服务器本身所做的只是管理这些子进程，根据需要启动新进程并停止现有进程。每个实例大约占用 1 MB RAM（很难精确估算，但这是一个合理的经验值），然后静待请求到来。如果收到的请求数量超过现有实例数，就会启动新实例；如果稍后系统空闲，多余的实例将被关闭。偶尔，即使有足够的工作量，某个 `httpd` 实例也可能被强制关闭。这允许操作系统回收 `httpd` 进程本身或其使用的任何模块中可能泄漏的内存。当然，`httpd` 进程也可能直接崩溃，此时该特定请求将会失败；但另一个实例将处于待命状态，以便在请求重试时处理。Apache 采用这种工作方式的一个关键原因就在于此：即使服务器崩溃后，它也能继续运行。

控制此行为的配置选项位于 `httpd.conf` 中或可添加到该文件中：

- `MaxClients`：这是你准备在同一时间支持的最大 `httpd` 进程数，因此也是并发处理的客户端请求的最大数量。根据每进程 MB 的经验值，将此值设置得高于你的 RAM 量没有意义。实际上，你会在此之前就耗尽 RAM。虽然它们仍会继续工作，但会依赖速度慢得多的虚拟内存，并且会在磁盘和 RAM 之间进行大量令人厌烦的交换。

  这个设置也不应过低；如果请求数量超过此数值，部分请求将被遗漏，不得不等待其他请求完成。如果延迟时间过长，客户端将放弃连接，请求会被报告为失败。

- `MaxRequestsPerChild`：当 `httpd` 实例处理完此数量的请求后，无论当前服务器负载如何，它都会被关闭，以防服务器或已安装模块中存在的未修复内存泄漏导致该实例因“肥胖”（内存膨胀）而失败。由于操作系统无法判断大小增加是不必要的，Apache 必须主动介入，定期关闭进程。此指令控制该操作发生的频率。除非你正在使用可能含有 bug 的实验性或在开发中的模块，否则应该可以将其限制设置为 100,000 而不会产生不良影响。使用 `top` 监控每个 `httpd` 进程的 RAM 使用情况；如果发现内存增长失控，请将限制缩小 10 倍。继续监控并根据需要进一步降低。同时要关注整个系统的行为，因为如果此数值降得过低，启动和停止子请求所浪费的时间将过多，此时你需要尝试隔离出导致问题的模块。

- `StartServers` 和 `MinSpareServers`：`StartServers` 指定启动 Apache 时初始化的 `httpd` 实例数量。一个好的数值是你网站通常处理的同时请求数。`MinSpareServers` 应设为该数值再加几个。由于启动新实例涉及一定的工作量，你不希望服务器在已经全力处理请求时还要去做这件事，因此保持一些备用实例是明智的。

当请求一个网页时，通常随后会来自同一客户端的额外请求以获取辅助资源（样式表、内联图像等），以及后续的其他页面请求。在客户端和服务器之间保持连接是合理的，以避免刚关闭连接又立即在同一客户端上打开新连接（几百毫秒后），并且发现某个 `httpd` 实例准备好接受请求（这通常恰好就是处理前一个连接且现在空闲的实例）。现代 HTTP 1.1 标准提供了此选项——称为“Keep_Alive”——现代版本的 Apache 默认遵循此选项（一如既往，具体取决于 Apache 配置文件中的设置）。

- `KeepAlive`：默认开启，通常你几乎没有理由关闭它。

- `MaxKeepAliveRequests`：一旦客户端和服务器之间建立连接，处理该连接的 `httpd` 实例将最多为该客户端服务此数量的请求。此值可以设置得相当高——大约 100。很少有页面请求会跟随一百个辅助请求，但确实可能发生用户加载第一个页面后快速打开另外半个打页面的情况。将此选项设置得较高不会造成太大问题，因为客户端通常会主动断开连接；在客户端未主动断开的情况下，以下配置指令将生效。

- `KeepAliveTimeout`：如果当前连接在此秒数内没有来自客户端的请求，服务器将假定客户端因某种原因离开了，而没有正确关闭连接。你的网站和客户端之间的带宽越高，此数值可以设置得越低。拨号用户的带宽是瓶颈，会降低请求速率，因此连续请求之间可能有 30–45 秒的时间差。此数值的下限应约为 10–15 秒。

在记录流量日志方面，Apache 可以使用反向 DNS 来查找请求源 IP 的主机名。这使通过肉眼阅读日志稍微容易一些，但仅此而已。与此同时，请求正在等待 DNS 服务器的响应，在收到响应之前无法继续。你最好只是在日志文件中存储 IP 本身，将查找工作留给如 Apache 的 `logresolve` 实用程序，以便在你真正需要时才进行。

- `HostnameLookups`：这决定在服务器日志中记录主机名（On）还是 IP 地址（Off）。

与此相关的是你在允许或拒绝连接时是使用域名还是 IP。同样，如果在你的 `.htaccess` 文件中使用 `allow from .example.com` 或 `deny from .example.com`，就必须执行反向 DNS 来确定源 IP 属于哪个域名（然后还要进行正向 DNS 查找以确认该 IP 确实如声称的那样属于该域名）。因此，在这里，允许或拒绝特定的 IP 地址范围而非域名更为有效。但请记住，DNS 功能的一半意义在于特定域名并非永久绑定到特定 IP 地址，域名可以转移到不同的主机和不同的 IP 地址上。

## 代码效率

说到 `.htaccess`，当 Apache 被要求读取一个文件时，它会检查文件系统路径（而非 URL 描述的路径）中每个目录下的 `.htaccess` 文件，直到系统根目录。如果路径很长，查找次数就会很多，因此缩短路径是有好处的。如果（你肯定是这样的）将整个网站存储在单个文档树中，而不是分散在系统各处，那么让 Apache 搜索到该树根目录以上的内容就没有意义。`access.conf` 文件提供了通知 Apache 这一情况的手段。首先，你声明从系统根目录向下任何地方都不允许 `.htaccess` 文件覆盖设置，然后紧接着声明在你的网站文档树中可以遵循 `.htaccess` 文件：

```apache
<Directory />
    AllowOverride None
</Directory>
<Directory /www/site/roott>
    AllowOverride All
</Directory>
```

如果你根本不使用 `.htaccess` 文件，请明确说明，这样 Apache 就不会浪费时间查找它们：

```apache
<Directory /www/siteroot>
    AllowOverride None
</Directory>
```

Apache 的一个可以加速输出流的模块是 `mod_gzip`。如今大多数浏览器都内置了 gzip 库，可以在接收数据时进行 [解] 压缩 gzip 压缩的数据。此类浏览器的请求头中会包含相关声明。作为回报，安装了 `mod_gzip` 的 Apache 将发送压缩响应。压缩/解压缩步骤会引入延迟，但对于高可压缩性文档（英文文本压缩率约为 30%，HTML 约为 60%），带宽节省的效果不容小觑。

此外，移除所有你实际不使用的模块。例如，如果你不使用 `.htaccess` 文件，请禁用 `mod_access`。PHP 扩展及其调用的库也是如此；如果你不打算使用 SimpleXML 扩展，请禁用它。

## PHP 优化

一旦你优化了硬件、数据库和 Apache，就可以专注于调整你的实际代码。此时你能为自己做的最好准备是选择并坚持一套一致的编码标准。你花在试图解读自己编写内容上的时间越少，就有越多时间可以考虑其他提高效率的技巧。

### 编码标准

网站访问者优先。你的工作是将精力投入到尽可能快速地向他们提供所需的信息。另一方面，你的时间比计算机的时间更有价值——事实上，更*昂贵*。

如果你能用多花费 1 毫秒处理时间的代价为自己节省 5 分钟的工作，那么这是一项良好的投资，即使在页面处理完成后仍能继续产生回报。

# 第 9 章

三十万次。你可以将这五分钟投入到更具生产力的事情上，例如*看看是否有办法在处理页面时节省 20 毫秒。这不仅仅是关于能否尽可能快地满足用户请求——考虑到你的服务器和他们的浏览器之间存在的所有延迟机会，单纯的速度可能并不是那么重要的因素。（如果你的网站非常繁忙，但如果真是如此，正如你所见，你的瓶颈很可能在别处。）关键在于，如果你能让现有的页面运行得更快，你就可以开始思考该页面还能为你的网站受众做些什么。

但是，如何完成这种工作量的转移呢？如果无法为你减轻任何工作负担，仅仅是在计算机上堆砌更多东西是不够的。节省编程时间的一个关键方法是以一种尽可能让阅读代码毫不费力的方式来编写代码。



现在，很少有像缩进多少、哪些部分需要缩进、大括号应该放在哪里，以及 `else` 是否应该与相邻的大括号出现在同一行（例如像这样 : ) `else {`）这样的问题更可能引发激烈的争论。事情可能会变得很糟糕。而且，即使你做出了这些决定，你仍然必须决定诸如变量、函数、对象和类的命名约定；是否将方法声明为 `protected static` 还是 `static protected`（如果你需要进行查找和替换，这就很重要了）；是使用 `global $foo;`、使用 `GLOBALS['foo']`，还是直接禁止使用全局用户变量；以及在哪里放置注释以及在其中写什么内容；更不用说如何划分代码文件等更实质性的问题。

> 避免使用“代码美化器”——*即接收源代码文件并根据一组标准重新格式化后返回的程序。至少，不要依赖它们。你的代码一开始就应该很漂亮；否则，你就忽略了制定标准的意义。如果你手头有旧代码或来自其他地方、标准不同的代码，并且希望将其与你自己（或他人）的标准保持一致，那么可以使用它们。但不要指望以后可以用美化器来清理，从而肆无忌惮地写出一堆乱码。*

### PEAR 编码标准

理顺至少一部分这种混乱的方法是采用现有的风格指南。虽然你可以采用为类似 C、C++ 或 Java 这样语法相似的语言开发的指南，但适配性可能并不理想。例如，你为变量命名的方式不需要与为函数命名的方式有显著区别；前者已经通过 `$` 符号加以区分了。相反，你可以采用 PHP 特定的标准，其中最广泛使用的是 PEAR 手册第 4 章中描述的标准。

除非你正在构建一个由公众提交代码组成的代码库（PEAR 本身的情况就是这样），否则严格遵循 PEAR 风格可能并不合适。例如，PEAR 风格要求每个源文件以一个注释块开头，其中说明作者和许可协议等信息。对于一个不会分发的内部大型应用程序来说，分发许可证毫无意义，也没有必要在每个文件中列出所有开发人员。然而，PEAR 标准可以作为一个起点。

### 大括号与缩进

关于大括号放置位置的争论已经持续了很长时间且没有定论，以至于至少有一种语言（Python）被故意设计来避免使用它们。Eric S. Raymond 在*术语文件*（Jargon File，版本 4.4.7）中关于“缩进风格”的条目中列出了四种风格，这里将描述它们及其名称，并附上另外几种风格。

#### 代码效率

K&R 风格——如 C 语言的设计者、该语言权威参考书作者 Kernighan 和 Ritchie 所使用的风格——也被称为“One True Brace”风格：

```
for($i=0; $i<100; $i++) {
    if($foo[$i]==0) {
        //...etc.
    }
}
```

在 Allman 或 BSD 风格中，大量 BSD 内核源代码是由 Eric Allman 编写的，他在编写这些代码时使用了这种风格：

```
for($i=0; $i<100; $i++)
{
    if($foo[$i]==0)
    {
        //...etc.
    }
}
```

Whitesmith 风格是以一种以这种方式格式化代码的商业 C 编译器命名的：

```
for($i=0; $i<100; $i++)
{
    if($foo[$i]==0)
    {
        ...etc.
    }
}
```

GNU 风格（几乎完全由自由软件基金会使用）如下：

```
for($i=0; $i<100; $i++)
{
    if($foo[$i]==0)
    {
        ...etc.
    }
}
```

Allman 风格的一个更紧凑的版本如下：

```
for($i=0; $i<100; $i++)
{
    if($foo[$i]==0)
    {
        ...etc.
    }
}
```

Allman 风格的一个更紧凑的版本是这个：

```
for($i=0; $i<100; $i++)
{
    if($foo[$i]==0)
    {
        ...etc.
    }
}
```

通过选择使用制表符还是空格，或者每层缩进有多宽，这六种风格都可以有所变化。通常，四个或八个空格（或宽度为八个空格的制表符）是最常见的，而制表符常常受到排斥，因为不同的人使用不同宽度的制表符。在任何一种宽度下看起来正确的空格和制表符混合，在另一种宽度下可能看起来不对，从而导致所谓的“制表符损坏”，代码行和片段呈现出各种看似随机的缩进。

最后一种风格是一个恶作剧：如果你要将左右大括号对齐到列中，至少应该确保对齐的是*成对的*左右大括号，否则这种对齐只是具有误导性。如果节省行数如此重要，你不妨使用 LISP 风格的缩进：

```
for($i=0; $i<100; $i++)
  {if($foo[$i]==0)
  {…etc.}}
```

PEAR 规定使用 K&R 风格缩进，每级缩进使用四个空格，且不使用制表符。排除制表符的原因当然是制表符损坏的影响；但了解制表符损坏的原因可以大大有助于预防它。

当你假设制表符具有特定宽度时，就会发生制表符损坏。下面的代码是使用制表符进行缩进的，在一个设置为每个制表符使用四个空格的编辑器中编写：

```
/***********************
*  Big Flashy        *
*  Box comment         *
*
*  Just Because (TM)   *
**********************/
for($i=0; $i<100; $i++)
{
    if ( ($a=$i || $b=$i)
        &&
        ($c!=$i || $d!=$i))
    {
        echo "Either $a or $b is equal to $i, ";
        echo "and either $c or $d is not.";
    }
}
```

而在一个配置为使用八个空格宽度的制表符的编辑器中，它会显示如下：

```
/***********************
*  Big Flashy        *
*  Box comment         *
*
*  Just Because (TM)   *
**********************/
for($i=0; $i<100; $i++)
{
        if ( ($a=$i || $b=$i
        &&
        ($c!=$i || $d!=$i)))
{
    echo "Either $a or $b is equal to $i, ";
    echo "and either $c or $d is not.";
}
```

首先可以看到，大型醒目方框注释（Big Flashy Box comments）通常带来的麻烦大于其价值。它们通常是制表符损坏的最大受害者，这具有讽刺意味，因为它们本应是专门供*人类*阅读的部分，而机器并不在意格式的细微差别。

如果你确实想要使用制表符进行缩进，那么经验法则是它们应仅用于*缩进*，而额外的对齐任务应使用空格。在上面的例子中，用于将 `if` 测试的第二行和第三行与第一行对齐的额外制表符——在四个空格宽的制表符下工作正常——当变成八个空格宽的制表符时，导致它们向右推进得太多。制表符之后应该使用*四个空格*（在制表符*之后*）来匹配四个字符 `"if ("`。

一般来说，源代码中唯一的制表符应该位于行首；它们后面不应该跟随任何其他字符。这两个例外情况是，当确实需要字面上的制表符字符时，或者当你使用“紧凑 Allman”风格时，在这种情况下，会使用一个单独的制表符将 `{` 与其后的语句分隔开。

你可能已经注意到，所有描述的样式（恶作剧除外）都将闭合大括号单独放在一行上。这对代码列表的影响是在语句块的结束部分和后续代码之间引入了一个可见的间隙，在某些方面类似于英文文本中的段落分隔。因此，你可以认为 K&R 或紧凑 Allman 风格“优于” Allman 风格，因为它没有将语句块与其引入的结构（`for`、`if`、`switch` 等）分开。根据 Raymond 的说法，K&R 风格辩护的主要理由是其对垂直空间更加经济，允许屏幕上同时容纳更多的代码。显然，紧凑 Allman 风格同时具备这两个优点，同时仍然允许左右大括号对齐。

### 减少嵌套层级

如果嵌套的大括号数量过多，就很难确定哪个左大括号与哪个给定的右大括号配对。大多数 IDE 和一些较好的支持语法的文本编辑器能够找到这种配对，而不会被注释或字符串字面量中出现的大括号弄糊涂，但你仍然很可能想要通过肉眼定位它们（例如，当你漏掉了其中一个时）。在阅读代码时，你经常会看到右大括号后面跟着像 `/* end for *j*/` 或 `/* end if ($i==0) */` 这样的小注释，试图提供帮助。然而，明智地使用 `break` 和 `continue` 语句可以帮助减少嵌套深度。这样做不仅可以减少代码向页面右侧漂移的趋势，还可以减少带括号块的数量和大小，从而减少括号的数量，并使每对匹配的括号更靠近，以便更快地通过肉眼识别。



例如，前面缩进风格的示例是这样编写的：`for`循环的主体完全由单个`if`语句组成——如果`if`语句的测试失败，那么在该次迭代中什么也不会发生，处理将继续到下一次迭代。这样表述时，你可以看到，该循环的等效实现如下：

## 第 9 章

```php
for($i=0; $i<100; $i++)
{
    if($foo[$i]!=0)
        continue;
    //…etc.
}
```

请注意，`if`语句中的条件测试已被取反，并且循环剩余部分的缩进深度减少了一级。这种技术还可以用于降低测试条件的复杂度。回顾之前讨论中的另一个示例：

```php
for($i=0; $i<100; $i++)
{
    if ( ($a==$i || $b==$i)
            &&
        ($c!=$i || $d!=$i) )
    {
        echo "Either $a or $b is equal to $i, ";
        echo "and either $c or $d is not.";
    }
}
```

你可以立即看出，这是另一种循环内部仅有一个`if`语句的情况，因此可以改写如下：

```php
for($i=0; $i<100; $i++)
{
    if(!(($a==$i || $b==$i) && ($c!=$i || $d!=$i)))
        continue;
    echo "Either $a or $b is equal to $i, ";
    echo "and either $c or $d is not.";
}
```

通过运用一点布尔代数，该测试条件可以简化为：

```php
if( ($a!=$i && $b!=$i) || ($c==$i && $d==$i) )
```

也就是说，如果`$a`和`$b`都不等于`$i`，或者`$c`和`$d`都等于`$i`，那么循环将继续执行。但如果你测试`$a`和`$b`是否都不等于`$i`，你就可以立即知道是否需要继续循环，而不必再去查看`$c`或`$d`。因此，可以将该测试拆分为两条独立的语句：

```php
for($i=0; $i<100; $i++)
{
    if($a!=$i && $b!=$i)
        continue;
    if($c==$i && $d==$i)
        continue;
    echo "Either $a or $b is equal to $i, ";
    echo "and either $c or $d is not.";
}
```

由于PHP允许`continue`或`break`接受一个参数来表示跳过多少层循环，因此在C或Java中需要通过在嵌套循环内部携带额外变量来表示是否应终止循环，或使用`goto`跳转到外层循环之后的标签（除了Java，因为它没有`goto`结构）的情况下，PHP可以简单地使用`continue`或`break`。你可以这样写：

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
if(null===$position) // $what_we_wanted was not found.
```

而不是这样写：

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
    if($found_what_we_wanted)
        break;
}
if(null===$position) // $what_we_wanted was not found.
```

关于`continue`和`break`的最后一点观察是，一种常见的做法是将这些语句与决定其是否执行的测试条件写在同一行，尤其是当这些测试条件简短且简单时。因此，你可能希望考虑采用或允许这种写法：

```php
if($a==$i && $b!=$i) continue;
if($c==$i && $d==$i) continue;
```

> *关于使用相等运算符`==`的补充说明：一个常见的拼写错误是将本意为`==`的地方写成了`=`。在某些情况下，你可以通过这种方式保护自己免受由此产生的bug困扰。当将变量与函数结果或字面值进行比较时，如果你将变量写在相等运算符的右侧，不小心将运算符本身写成`=`而不是`==`会导致解析错误：`"null===$position"`是无效语法。这些错误比那些由于不当赋值或未正确比较而产生的细微错误更容易调试。*

## 注释

除了PEAR强制规定的作者身份和许可证详情外，顶部注释中可以包含的其他内容还有对其包含代码功能概述（synopsis）。如果概述很长，在开头添加一行或两行的摘要来总结该概述，将有助于后续想要了解该文件用途的开发者。

PEAR还建议你应该使用javadoc风格的注释，以便它们能轻松转换为文档。在这一点上，意见和其他风格问题一样分歧严重。反对的观点是，由于它们吸引了大量的额外格式化标记，使得注释本身在源代码中更难阅读。另一种观点是，当人们论证每个公开可访问的方法都应该以这种方式注释时，这种做法鼓励了*空洞的无用*注释，这些注释实际上既没有起到注释的作用，也没有对文档做出贡献：

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

但任何注释都应该做的事情是记录代码的*意图*。如果代码本身构建良好，它自己就能很好地记录它是*做什么的*。它不会记录的是*为什么*要这样写。

### 命名约定

命名不佳的变量和函数是各种故事（从喜剧到恐怖）的丰富来源。在任何有一定长度的应用程序中，你都需要拥有一套一致的命名系统。以下是一些提示。

用于控制`for`循环的通用计数变量应该简短且优雅。除非上下文提供了明显的变量选择，否则惯例是首先使用`$i`。如果你嵌套另一个循环，其变量为`$j`，接着是`$k`，然后是`$l`。通常，如果你需要将循环嵌套得更深，你可能想要*重新考虑*你正在做的事情，并将除最外层块以外的所有语句移入一个函数中。如果循环不是嵌套的，那么只要正确初始化，它们可以使用相同的变量。如果你使用`foreach()`循环遍历数组，使用复数形式作为数组名称，使用对应的单数形式作为元素名称，将使两个变量之间的关系变得明显：`foreach($children as $child)`。

应特别避免过长的变量名。变量名越长，出现拼写错误导致混乱的可能性就越大。毫无疑问，你所有的PHP开发都设置了*错误报告*为*(至少)*`E_ALL`，这样每次你尝试使用未初始化的变量时都会收到通知。这会捕捉到你在使用变量时*拼写*错误的情况，但如果是在*赋值*给变量时*拼写*错误，它就无法帮助你了。在前一节中，使用了变量名`$found_what_we_wanted`，但在某处*拼写*错了。这个错误不会被捕捉到，因为它不涉及使用未初始化的变量，只有当你意识到有问题并且`$i`始终值为100时——才会发现这个错误。

### 代码效率

PHP 5提供了机制，通过魔术方法`__get()`、`__set()`和`__call()`，将对象的可见属性和方法与其实现类的属性和方法分离开来。由于变量和属性的首尾大小写有区别，你可能希望考虑将所有对象属性命名为小写名称，声明为`private`或`protected`，然后编写例程通过首字母大写的名称提供访问：



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

这还使你能更精细地控制对象用户可能修改或查看的属性。例如，请注意 `$object->Height` 可以被读取但不能赋值——这种区别如果简单地使 `$object->height` 公开则无法实现。

如果你在通过 `__get()` 和 `__set()` 创建的真实属性和合成属性之间做出风格上的区分，你应该确保为真实属性提供合成访问权限，并且最好禁止直接访问这些属性。这将允许你创建类，无论每个此类是否在内部使用相同的属性，都提供完全相同的属性接口。例如，复数对象可以提供 `$num->Real`、`$num->Imag`、`$num->Arg` 和 `$num->Mag`；无论它是将数字存储为实部加虚部并合成提供辐角和模长，还是反之亦然。

> 合成属性的 `__get()` 访问器可以包含代码，将之前获取的值缓存在私有属性中，以防再次被请求；当它依赖的属性通过 `__set()` 被修改时，清空缓存内容。

在由多个单词构建函数和方法名称时，使用 `underscore_separation` 或 `TitleCase` 来显示一个单词在哪里结束，下一个单词在哪里开始。关于哪种

# 第 9 章

虽然看起来更美观，但请记住，函数、方法和类名都是以不区分大小写的方式处理的：`Mandate` 和 `mandate` 将引用同一个实体。

使用 `define()` 或 `const` 创建的常量通常以全大写形式标识。在全局作用域中使用 `define()` 创建的常量，前面应加上一些独特的字符序列，以防止与其他地方可能定义的其他常量发生冲突（参见 PHP 手册中关于此实践的许多示例）。对于类常量而言，这并非必需，因为它们的名字已经由类名（或类定义中的 `self::`）作为前缀。

由于这种区分已经内置于 PHP 的语法中，与其他语言相比，区分变量/属性名与函数/方法名的规则是不必要的；但类和函数之间没有这种区分。你可以有一个名为 `Foo` 的类和一个名为 `Foo` 的函数，区别的唯一方法是 `$v = new Foo();` 使用类，而 `$v = Foo();` 使用函数。

```php
$v = Foo();
Foo(); // 其他事情——具体来说，是无法编译的东西；构造函数不能静态调用，静态函数不能是构造函数
```

从语法角度来看，类、变量和属性最好用名词或名词短语来描述。使用你在描述代码功能时所用的相应词性。数组和其他集合应命名为复数形式（`$children`、`$pages`）。布尔值属性的名称应以“is”或“has”开头，或使用其他表示谓词的方式（`$isValid`、`$can_be_deleted`）。类应命名为名词（`UserFactory`、`NonPlayerCharacter`）；抽象类可以加上前缀 `Abstract_` 或 `Abstract`，以防止意外尝试从中创建对象（`AbstractCollection`、`Abstract_Document`），而 `FooFactory` 结构是一种常见的约定，用于表示提供返回类 `Foo` 的新对象的静态方法的类。函数和方法可以用动词命名（`traversePath()`、`anneal()`、`be_wonderful()`），允许使用形容词、副词，偶尔使用名词来命名常量（`COLOR_GREEN`、`QUICKLY`、`GOLDEN_RATIO`）。

## 破解语法

一些编码风格规则可以通过将违规操作转换为解析错误来强制执行。如果你知道自己在做什么，可以编辑 `zend_language_parser.y` 和 `zend_language_scanner.l` 文件并重新构建 PHP。

例如，如果你想排除使用诸如 `if() : … endif;` 等结构的可能性，那么你可以从词法文件（lex file）中移除匹配 `endif`、`endwhile`、`endfor`、`endforeach`、`enddeclare` 和 `endswitch`（所有这些都在 `<ST_IN_SCRIPTING>` 上下文中出现）的模式；并从 yacc 文件中移除相应的 `T_END*` 令牌声明以及产生式规则：

```yacc
unticked_statement:
    T_IF (' expr ') ':' inner_statement_list new_elseif_list new_else_single T_ENDIF ';'

while_statement:
    ':' inner_statement_list T_ENDWHILE ';'

for_statement:
    ':' inner_statement_list T_ENDFOR ';'

foreach_statement:
    ':' inner_statement_list T_ENDFOREACH ';'

declare_statement:
    ':' inner_statement_list T_ENDDECLARE ';'

switch_case_list:
    ':' case_list T_ENDSWITCH ';'
    ';' ';' case_list T_ENDSWITCH ';'
```

同时移除 `new_else_list` 和 `new_else_single` 产生式的全部内容。由于 `while_statement`、`for_statement`、`foreach_statement` 和 `declare_statement` 现在都归约到单个规则 `statement`，且没有关联代码，这些产生式本身现在是冗余的。你可以将 `while_statement` 的出现替换为 `statement`（它出现在 `unticked_statement` 的产生式中，出现一次）而不会产生不良影响，移除 `while_statement` 的产生式，并在此过程中获得一个更小、更简单的解析引擎。

当然，这将破坏任何使用现在被禁止的结构编写的代码。

## 代码效率

### 缓存

如果一个页面每天更新一次，但每天被访问数千次，这意味着相同的计算被反复执行，产生相同的结果，每天执行数千次。只执行一次并保留结果以供后续所有请求使用，具有巨大的节省潜力。

由于你的 PHP 应用程序通过几层中间软件与处理器隔离，指令过滤穿过它们到达硬件，结果又过滤回来，有几个潜在的地方可以短路这个过程。在任何两层之间，都有一个接口，你可以想象一个助手，他记得之前人们请求的信息以及提供的相关信息，因此如果相同的请求再次到来，他可以立即提供该信息。

在 PHP 层面，缓存有效的两个主要接口。你可以生成页面的静态版本并代替每次重新生成来提供这些版本，或者你可以将 PHP 应用程序的源代码存储在预解析格式中，以便 Zend 引擎直接执行而无需编译源代码的额外步骤，或者你可以两者都做。

#### 源码预解析

当运行 PHP 程序时，源代码被加载、解析并编译为字节码（针对由 Zend 引擎模拟的假想处理器的机器代码），然后执行该字节码。市面上有几种产品可以获取该编译的字节码并将其保存；以下是一些较好的产品的选择（按字母顺序排列）：

| 产品 | 网址 |
| :--- | :--- |
| BW Cache | http://bwcache.bware.it/cache.htm |
| Alternative PHP Cache | http://pecl.php.net/package/APC |
| PHP Accelerator | http://www.php-accelerator.co.uk/ |
| Turck MMCache | http://turck-mmcache.sourceforge.net/ |
| Zend Optimizer | http://zend.com/store/products/zend-optimizer.php |



就稳健性和有效性而言，Zend 自己的产品显然很难被超越，但使用它需要购买 Zend Encoder 来生成字节码。请注意，APC 是作为 PECL 扩展分发的。

当再次调用程序时，字节码被检索并直接提供给 Zend 引擎，跳过解析和编译阶段。所有这些产品都会检查源文件和字节码文件的修改日期，以确定源文件自生成字节码以来是否已更改，如有必要则重新解析和重新编译。一些产品，如 Zend Optimizer，还可以（顾名思义）对字节码执行优化以提高性能，包括许多在 PHP 本身中无法模拟的优化（因为优化器在较低的层级操作，其中单个 PHP 语句可能对应于几个可以独立操作的字节码指令）。

一般来说，使用字节码缓存只是遵循其安装说明的问题，无需对 PHP 程序的源代码进行更改。因此，这通常是软件层面性能提升中最简单但也很显著的一种方法。

请注意，特别是在使用优化字节码缓存的情况下，各种脚本速度的变化是非线性的：并不仅仅是每个脚本运行速度提高 20% 或快两倍的问题。有些脚本会比其他脚本按比例运行得更快，最坏的情况是某些脚本没有可测量的速度提升。因此，在未安装缓存的情况下对站点进行性能分析的结果，与安装缓存后站点的性能概况没有关联。

### 输出预生成

与字节码缓存相反，保存生成的输出以便稍后重新显示确实涉及到站点操作方式的变化。特定页面需要做的第一件事是确定它是否需要运行，或者是否可以使用其输出的缓存副本。

### PEAR::Cache 和 PEAR::Cache_Lite

自然，PEAR 包含提供后续请求缓存输出的软件包。

`Cache_Lite` 提供了一种简单快捷的机制，将页面或部分页面的输出存储为文件，以便稍后需要时读取。以下示例使用它来缓存一个简单的字符串：

```php
<?php
require_once 'Cache/Lite.php';

$Id = '42'; // 这用于识别使用哪个缓存文件；
// 任何可以从访问中记住的唯一标识符都可以；
// 如果你正在以这种方式缓存整个页面，
// 其 URL 是一个自然的选择。

$options = array(
    'cacheDir' => '/cachefiles/', // Cache_Lite 仅执行文件存储：
    // 你需要在此指定
    // 一个适当的目录。

    'lifetime' => 3600
    // 我们将强制每小时更新一次。
);

$Cache_Lite = new Cache_Lite($options);

if ($data = $Cache_Lite->get($Id)) {
```

## 代码效率

```php
// 已找到缓存副本
} else {
// 缓存中无副本；生成其内容
// 并存储到 $data 中。
$data = "Hello, World!"; // 这同样也可以是一个完整的页面。
// 完成后，将其保存到缓存中。
$Cache_Lite->save($data);
}
// 无论哪种情况，页面的输出都在 $data 中。我假设有人希望
// 看到它...
echo $data;
```

围绕现有脚本封装的最直接方法是生成页面并缓冲其输出。这意味着将“Hello, World!”行替换为以下内容：

```php
ob_start();
/*
...所有现有脚本放置在此处...
*/
$data = ob_get_contents();
ob_clean();
```

没有什么能阻止你对单个页面的不同部分使用多个缓存文件，或在多个页面中使用相同的缓存文件。

PEAR Cache 更加复杂。与 `Cache_Lite` 相比，它最显著的区别在于它允许以多种方式实现缓存（并且你始终可以子类化 `Cache_Container` 来创建自己的实现）。除了扁平文件存储外，Cache 还附带使用共享内存、Mowabk Session Handler 扩展以及数据库的容器。它还提供了缓存数据的 gzip 存储，以及用于存储动态生成图像和 http 请求响应的专用缓存。

以最直接的形式，使用 PEAR Cache 实际上与使用 `Cache_Lite` 相同。同样，你无需缓存整个页面；主要关注那些生成缓慢且很少变更的部分。

### 个性化内容管理系统

内容管理系统有时本身就提供缓存功能。如果你决定为自己编写一个应用程序，以便更轻松地更新网站内容（为什么不这样做呢？），那么你可能会希望执行相同的操作。广义来说，保持页面内容与数据库内容同步有三种机会。

- 在数据库内容更改时更新页面。换句话说，你的管理应用程序除了更新数据库内容外，还会重新生成页面并将文件保存在适当的位置，覆盖已有的旧版本。请注意，如果文件因任何原因被删除，你需要显式地重新生成它——也许在你的管理应用程序中提供“重新生成所有（缺失的）页面”的选项。生成的页面可以是 PHP 脚本或静态文件。
- 在页面被请求时重新生成。你可以随时安全地删除页面的缓存版本。下一次用户请求该页面时，是通过一个脚本来查看该页面是否存在。如果不存在，脚本会根据数据库生成页面并提供给用户，同时保存以供下一个用户使用。如果页面存在，脚本必须查看文件的最后修改时间，并检查数据库以确定最近相关更新发生的时间（因此你需要在某个地方有一个“最后更新时间”字段）。如果更新早于文件修改时间，脚本只需使用 `fpassthru()` 将缓存版本发送给用户；否则，它再次执行重新生成和输出（保存）任务。
- 定期重新生成按固定时间表更新（例如每日、每周或每月）页面的 cron 任务可以按此方式处理。不用说，在更新完成后但 cron 任务下次运行之前提供的页面仍将包含较旧的内容。

### 将 404 处理程序用作蹦床

这种方法对于归档不再变更的页面非常有效，例如旧新闻文章。如果它们可以作为静态页面存储和请求，那么 PHP 就再也不会参与其重新生成了。更好的做法是，仅在需要时才（一次性）生成它们。

该方法的工作原理如下。假设一位访客请求一篇尚未保存为静态页面的旧新闻文章。Apache 查找它，但未找到，因此开始构建 404 Not Found 响应。你可以配置 Apache 使用自定义 404 处理程序（使用其 `ErrorDocument` 指令）来调用 PHP 脚本。该 PHP 脚本解析 `$_SERVER['REQUEST_URI']` 的内容以确定请求的是哪篇文章。假设请求是一篇真实的文章，它生成页面（将其存储在输出缓冲区中）并将其保存在最初应该找到的位置。然后它调用 `header('HTTP/1.1 200 OK')`，随后是页面的缓冲内容。这可能是按顺序为几种不同类型的请求执行的。如果所有其他方法都失败了，它最终以发送 404 Not Found 响应结束，并包含在该情况下适当的页面内容。

后续对同一文章的请求将使 Apache 在完全正确的位置找到正确的静态页面。

显然，你可以随时清除这些页面（例如，在更改网站外观、迁移主机或只是释放磁盘空间时）。如果再次请求它们，它们将简单地被重新生成。

此方法可以与 Apache 的 `mod_rewrite` 和 `mod_alias` 模块结合使用，以进一步将站点的文档树与服务器的文件系统解耦。在这种情况下，你的脚本将在 `mod_rewrite` 完成 URL 转换后，将静态页面保存在由其指示的位置。

可以对此进行更复杂的处理（当然，随着复杂性的增加，日后混淆的风险也会增加）。由 404 处理程序生成的文件本身可以是一个 PHP 脚本——为了生成用户请求的页面，处理程序要么使用类似 `fpassthru('http://www.example.com/oldnews/19980503.php')` 的东西执行脚本，要么复制其行为。PHP 不再被排除在循环之外，但你可以通过这样做来减少未来提供相同页面所需的处理量（例如，你可能需要在允许用户访问页面前检查其身份验证）。

### 客户端缓存

请记住，大多数网络浏览器都有缓存。通过一点 HTTP，你可以利用它——这需要能够确定页面内容最后一次更改的时间，或者知道它们下次何时将更改。

如果你知道页面内容上次更新的时间，你可以将其作为 Last-Modified 头添加。客户端浏览器和你的服务器之间的任何缓存代理都可以使用此头来决定它们持有的任何页面缓存副本是否仍然有效（如果其缓存副本具有相同的 Last-Modified 日期，则有效）。客户端还可以对资源发出 HEAD 请求，并使用 Last-Modified 头来决定是否值得 GET 页面本身。

如果你提供 Expires: 头，你是在表示该页面的任何缓存副本在指定时间之前都是有效的。掌握这一点后，缓存该页面的客户端和代理可以稍后决定是否仍要请求该页面。

对于 HTTP 头中的所有日期，格式是 RFC 2822 中指定的格式——即由 `date('r')` 返回的格式。



客户端可能在请求中包含的一个头是 `If-Modified-Since:` 头。这也是一个 RFC-2822 格式的日期，如果存在，你的脚本可以通过 `apache_request_headers()` 使用它来决定是像往常一样生成并发送完整响应给客户端，还是通过发送无内容的 `304 Not Modified` 响应来告知客户端其缓存副本仍然有效。（`304` 响应不得包含任何内容；仍然可以发送任何头，包括 `Last-Modified` 和 `Expires`。）

存在其他缓存控制头，更全面的说明在 HTTP 规范 RFC 2616 中给出。

### 你自己的代码

除了将脚本包裹在更多缓存控制代码中，你还能做什么来加速它们？这就是开始提出“哪个更快”的问题的地方。正如你所见，你应该以经验主义的眼光审查所有这些建议。

### 输出缓冲

输出缓冲不再仅仅用于缓存或输出后处理（或笨拙的“headers already sent”错误变通方法）。当 Apache 将数据发送给用户时，它是分包发送的。每个数据包都必须封装并编址以便到达其目的地。发送较少但较大的数据包可能比发送许多较小的数据包更快。通过缓冲 PHP 的输出，你可以收集页面的内容并一次性发送出去，而不是在处理过程中每隔几个字节就滴流式地发送。

事情并不那么简单。当你向用户滴流式发送字节时，他们有机会更早地接收到它们，并更快地看到结果，即使页面整体加载速度较慢。他们甚至可能找到正在寻找的链接并在浏览器完成接收文档之前就点击跳转（如果他们打算在该文档上停留一段时间，无论如何他们停留的时间都会比页面加载时间长）。因此，你至少应该批量处理你的缓冲。不要在整个脚本周围使用一个大缓冲区，而是依次发送几个“章节”；在一个新处理块开始之前结束一个章节。一旦可行，就开始产生输出。不要让悬而未决的状态让用户感到焦虑。

## 第 9 章

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
<title>A page buffered in chapters</title>
<?php

ob_start(); // HTML <head> content
// Construct <meta> tags, and select some CSS and Javascript to include. E.g.,
echo "<meta name=\"author\" content=\"${Page_author}\">
"
;
ob_end_flush(); // Output the HTML head chapter

?>
</head>
<body>
<?php

ob_start(); // Strapline and breadcrumb trail.
?>
<div id="topmatter">
<!-- HTML and PHP for constructing this chapter -->
</div>
<?php
ob_end_flush(); // Output the strapline chapter

ob_start(); // Side navigation list
// ... 
ob_end_flush(); // Output the side navigation chapter

?>
... 
</body>
</html>
```

在这个示例中，展示了六个部分：从 `<!DOCTYPE>` 声明开始，到 `<title>` 元素结束的部分；`<head>` 元素其余内容对应的部分；完成 head 并开启 body 的小部分；随后是组成页面布局的两个部分（假设还有其他部分）；最后是 `</body></html>` 以结束页面。每个部分都会作为一个完整的块输出，从而为 Apache 提供最佳条件，使其能够尽可能高效地填充其发送的数据包。

### echo 还是 print？

哦不，又来了。`echo` 和 `print` 之间值得注意的速度差异（除了打字速度外）主要在于你需要依次输出多个字符串时。如果使用 `print`，你需要将它们全部拼接在一起，然后输出生成的字符串。使用 `echo` 也可以这样做，但你不必这么做，只需使用逗号 `,` 而不是点号 `.` 来分隔字符串即可。

在进行字符串拼接时，PHP 需要为正在构建的字符串分配内存，并且每次执行拼接操作时都要重新分配内存。这会引入延迟。此外，在构建整个字符串完成之前，字符串的任何部分都无法输出，因此如果被拼接的项之一是函数，那么一切都必须等待该函数执行完毕。请比较运行以下语句的结果：

```php
print "This string takes ".sleep(15)."too long to display.";
echo "This string takes ".sleep(15)."too long to display.";
echo "This string takes ", sleep(15), "too long to display.";
```

这种方法适用于输出，但对于需要拼接到变量中的字符串，也可以采用类似的方法：启动一个输出缓冲区，使用 `echo` 输出字符串的所有片段，将缓冲区内容读取到变量中，最后结束并清理缓冲区。例如：

```php
ob_start();
for($i=0; $i<100; $i++) echo $i,' ';
$zero_to_ninetynine = ob_end_clean();
```

### for($i=0; $i<count($array); $i++)

不要这样做。这样做意味着 PHP 必须在每次迭代后检查数组的大小。没错，数组的大小是与其内容一起维护的，因此实际上不需要`计数`其元素，但仍需查询大小——以防数组在循环过程中发生了变化。如果你知道它不会变化，请使用以下方法：

```php
for($i=0, $count_array=count($array); $i<$count_array; $i++)
```

这就既有效又节省了额外的查找。如果数组元素遍历的顺序不重要，则可以使用中间变量来避免这种情况：

```php
for($i=count($array)-1; $i>=0; $i--)
```

如果你这样做，请记住 `-1` 和 `>=`。

### 临时变量

特别是当你使用关联数组时，如果你要多次查看同一个数组元素，将其值放入局部变量中（如果你打算修改它，则按引用分配）可以节省查找 `$array['foo']` 实际指向哪个数组元素所涉及的开销。数组属性也是如此。考虑以下代码：

```php
$this->p_consts->Delta[$i][$k] = $this->p_consts->Delta[$i]($this->p_consts->s[$i]-1);
$this->n[$i][$k] = $this->n[$i]($this->p_consts->s[$i]-1);
```

`$this->p_consts` 使用频率相当高；特别是其 `Delta` 和 `s` 属性。你可以创建临时变量来存储这两个属性的值（因为你要修改其值，所以按引用分配 `Delta`），从而避免每次都需要通过 `$this->p_consts` 进行查找：

```php
$p_Delta = &$this->p_consts->Delta;
$ps = $this->p_consts->s[$i]-1;
$p_Delta[$i][$k] = $p_Delta[$i][$ps];
$this->n[$i][$k] = $this->n[$i][$ps];
```

显然，这也可以使程序更易读。

### if...else if 测试和 Switch 案例的顺序

首先，如果你有一系列连续的 `if` 语句，并且在任何给定时间只有一个可能为真，那么除了第一个之外，你应该对所有其他语句使用 `else if`。否则，在找到匹配项后，PHP 将继续测试剩余部分。*你知道它们都将为假，但真正执行工作的人不是你。* PHP 必须继续测试，以防被测变量在处理成功语句期间发生了变化。

如果你有一系列 `if...else if` 语句或 `switch` 语句，请将更常见的情况放在顶部，将罕见情况移到底部。除了向读者提供代码功能的更清晰视图（通过先说明典型情况，之后再处理复杂的边缘情况）之外，这意味着 PHP 平均需要执行更少的测试才能找到一个成功的测试。

即使你最常用的情况由最后的 `else` 或 `default` 案例满足，也请显式提供它们，并将它们的测试放在顶部（*每个测试都会在 PHP 处理此类剩余部分之前进行检查*）。

### 使用正确的字符串函数



手册反复指出，如果你没有实际使用正则表达式语法的任何功能，那么 PHP 的其他字符串函数可能比正则表达式函数快得多。当你可以说 `explode(" /", $path)` 时，不要说 `split(" /", $path)`。

### 正则表达式语法

说到正则表达式，谨慎的设计也能提高其性能。整本书甚至多本书都可以且已经写过关于正则表达式及其编写方法的论述；目前，只需记住，PCRE 函数 `preg_match()` 等提供了比 `ereg()` 等 POSIX 函数更丰富的语法和更智能的引擎。

### unset()

好吧，PHP 会在变量 *超出作用域* 时立即清理变量；要么是函数末尾的局部变量，要么是脚本末尾的 *其他所有内容*。一般来说，这意味着你不必担心这个问题。
但如果你有一个巨大的结构（例如包含成千上万个元素的数组），你不再会再次使用它，特别是如果你马上就要处理更多的大数据，那么你应该在完成工作后立即 `unset()` 该结构。由此产生的大块空闲内存可以立即用于其他用途。在繁忙的服务器上，在可能的情况下释放大块内存，可能会决定是让所有东西都装入 RAM 还是 resort 到磁盘上的虚拟内存。

### 释放资源和持久数据库连接的危险

同样，如果你正在使用诸如 MySQL 数据库连接之类的资源，并且你已完成使用但仍有大量工作要做，不要为了脚本执行的剩余时间而独占它：关闭它。
持久数据库连接（例如由 `mysql_pconnect()` 创建的连接）有时被建议作为加速性能的手段。这是因为在连接第一次建立后，创建它的 httpd 进程在建立该连接的脚本结束后仍会保留该连接，以便在下一次运行需要数据库连接的脚本时使用。由于连接数据库涉及一些工作，持久连接可能会节省一点时间。但在节省的时间变得明显之前，可能会出现故障。
问题在于，即使已连接的 httpd 进程可能位于请求之间，它仍会保持该数据库连接打开，直到它死于服务器指定的死亡。数据库连接是有限的资源（`mysql_close()` 对持久连接没有效果）。很可能发生的是，如果情况变得繁忙，脚本可能尝试连接数据库，但会收到错误消息而被拒绝，说最大允许的连接数已经分配。如果所有连接都在使用中，那就不会那么糟糕：你只需稍微加强数据库服务器即可。但如果最大连接数是因为空闲的 httpd 进程占据可用连接（以防出现需要其中之一的请求）而达到，那就麻烦了。

### `ob_gzhandler()`

如果你打算使用输出缓冲来批量处理页面输出，使用 `ob_start('ob_gzhandler')` 启动缓冲区意味着，当你收集缓冲输出时，会发现它已被压缩。回调函数礼貌地检查请求头，以确保输出前往的浏览器确实能够阅读 gzip 压缩的数据。
作为使用该回调处理器的 *替代方案*（不要试图同时使用两者），考虑在 `php.ini` 中设置 `zlib.output_compression`。事实上，这是 PHP 开发人员推荐的方法。

#### 总结

在阅读这里的建议和指导时，你无疑会注意到有些似乎相互矛盾。这是不可避免的：什么有效取决于具体情况，而不同的情况可能需要做出不同的决定。大量操作大型数据库的网站与主要以文件存储为目的的网站需求不同。
作为开发人员，你的时间比计算机作为 Web 服务器的时间更有价值。从经济角度或工作满意度角度来看，将时间浪费在那些最好只能带来微小改进且对网站访客不可见的更改上，完全是没有意义的。相反，将时间投资于规划与测试。在查看单行代码之前，退一步看大局。
你的硬件是否合格，还是它会限制软件改进的效果有多大？你的 Web 服务器是如何配置的；是否可以进行调整？有多少冗余计算被执行：一个地方的结果是否可以在其他地方预期有用时进行缓存？

# 第 9 章

进行性能调整的最佳时机是在编写代码之前。在构建站点时，测试、实验并积累关于各种设计方式及其优缺点的经验。在开始时选择正确的框架对最终产品的速度产生的影响，远大于事后对代码进行的任何量级的调整。请保持测试、实验和积累经验，并始终关注全局，因为硬件和软件技术都在不断进步。处理器会更快，内存会更便宜，网络连接会更宽裕，Web 服务器会更高效，Web 浏览器会更先进，PHP 也会有更多可供开发的功能。

## 第 10 章：PHP 扩展

尽管 PHP 语言的核心提供了许多完成常用任务的功能，但还有许多扩展可以添加，以提升 PHP 配置的整体水平。本章探讨了一些更实用的扩展，但这仅仅是冰山一角。本章中的扩展涉及图像处理、创建 PDF 文件（无需使用 Adobe Acrobat）、创建 Flash 文件（无需使用任何商业软件）以及与 XML 文档交互。其中一些扩展已在默认配置中捆绑并启用，你还在等什么？

### PDFLib

无论您的内容是学术性质还是商业性质，一个专业开发的网站若缺乏以 PDF（便携式文档格式）交付内容的能力，则是不完整的。虽然 PHP 开发者可以使用几种开源库，例如 FPDF（[http://www.fpdf.org/](http://www.fpdf.org/)）和 pdf-php（[http://sourceforge.net/projects/pdf-php](http://sourceforge.net/projects/pdf-php)），但 PHP 内置的 PDFLib 功能 arguably 是最高效的方式。自 PHP 4.3.9 起，PDFlib 函数已移至 PHP 扩展社区库（PECL），它是商业 PDFLib（[http://www.pdflib.com/](http://www.pdflib.com/)）PDF 处理库的一个包装器。PDFLib 相对于纯 PHP 解决方案的优势在于速度。像 PDFLib 这样编译后的 C 代码比由 Apache 解释的 PHP 代码快几个数量级。缺点是商业使用的许可成本。

> *细心的读者会注意到，此文本对该主题有两种不同的大写方式：“PDFLib”和“PDFlib”。这是为了将拥有者命名为“PDFlib”的 C 库与 PHP 包装库“PDFLib”区分开来。值得注意的是，C 库的文档并未严格遵循此约定。*

#### 配置

PHP 对 PDFLib 的支持最近发生了重大变化，并且像语言的许多其他特性和其众多库一样，预计还会发生进一步的变化，尤其是在 PHP 在专业开发社区中越来越被接受的情况下。
因此，配置极易受架构、操作系统、PHP 版本等常见问题的影响。如果您的 Apache 安装使用动态共享对象（DSO）或 Windows 安装中的动态链接库（DLL），那么只需确保相应的文件存在（分别为 `libpdf_php.so` 或 `libpdf_php.dll`），并在 `php.ini` 文件中正确引用且未被注释即可。
如果您不使用 DSO，或者无法使用，则您需要访问 PDFLib 网站（[http://www.pdflib.com/](http://www.pdflib.com/)），获取 PDFLib 源代码的多种版本中的最新版本之一，并构建一个静态链接库。有关更多详细信息，请访问 [http://www.pdflib.com/products/pdflib/info/PDFlib-in-PHP-HowTo.pdf](http://www.pdflib.com/products/pdflib/info/PDFlib-in-PHP-HowTo.pdf)。
无论您如何安装 PDFLib，访问 PDFLib 网站并下载最新版本的 PDFLib Lite 都是值得的。随源代码提供的非常有帮助的文档 `PDFlib-manual.pdf` 包含各种有用的信息，包括所有支持编程语言的绑定、通用的 PDFLib 编程概念等。第 3.1.1 节“PDFLib 程序结构和函数作用域”是必读内容，它将为您节省数小时的挫败感，从而消除“作用域”错误。

#### 入门

PDF 文档在 PHP 中被称为资源类型，您使用 `pdf_new()` 函数创建它，如下所示：

```php
$pdf = pdf_new();
if (!pdf_open_file($pdf, "")) {
    die("Error: Unable to output file");
}
```

请注意，资源创建后立即进行一项测试，以确保资源已创建并打开。如果未执行此检查就尝试使用任何页面作用域函数，脚本将失败，并产生以下 PDFLib 异常：
> Function must not be called in 'object' scope
换句话说，由于文档尚未打开，因此在对象作用域中调用了页面作用域函数。在 PHP5 中，只需将 `pdf_new()` 调用包裹在一个捕获 `PDFLibException` 类型异常的 `try/catch` 块中即可。
在 PDF 文档完成后，您可以调用 `pdf_close()` 来关闭文档文件并释放关联的资源。

#### 指定文档信息

通过包含在文档信息中的元数据搜索文档是一种手段。这可以轻松地使用 `pdf_set_info()` 函数来实现。PDFLib 手册的第 8.9.6 节“文档信息字段”规定了哪些字段是相关的。例如：



```php
pdf_set_info($pdf, "Author", $name . " <" . $row['Email'] . ">");

pdf_set_info($pdf, "Title", "Resume = " . $name);

pdf_set_info($pdf, "Subject", "The resume of " . $name . ", " . $row['DesiredPosition'] . ".");
```

此代码将文档的作者、标题和主题设置为从 MySQL 数据库中检索的值。请注意，`pdf_set_info()`函数取代了若干专门设置特定字段的已弃用函数。

### 必要元素

为了渲染最基本的页面，每个由 PDFlib 生成的文档都需要以下元素：

- `pdf_new()`：需要创建一个新的 PDF 资源。
- `pdf_open_file($pdf [, $filename])`：接受 PDF 资源和可选的文件名作为参数。对于缓冲输出（如本节末尾的示例），文件名是不必要的。
- `pdf_begin_page($pdf, $width, $height)`：接受 PDF 资源以及页面的宽度和高度（以点为单位）作为参数。
- `pdf_findfont($pdf, $font, $encoding [, $embed])`：给定 PDF 资源、特定字体名称和编码作为参数来定位字体。将非零值作为可选的第四个参数传递将导致立即检查字体，从而避免后续错误。
- `pdf_setfont($pdf, $font, $size)`：接受 PDF 资源、字体句柄（由上述`pdf_findfont`函数返回）和字体大小。
- `pdf_show_xy($pdf, $text, $x, $y)`：将传递的文本放置在给定的 PDF 资源中给定的 x 和 y 坐标处（以点为单位）。
- `pdf_stroke($pdf)`：“墨水”或在给定的 PDF 资源上绘制文本。
- `pdf_end_page($pdf)`：完成给定 PDF 资源的当前页。
- `pdf_close($pdf)`：关闭给定的 PDF 资源。

本节末尾的简历生成器示例使用这些函数中的每一个，将 PDF 文档返回给浏览器，而不是将文件放置在本地文件结构的某处。

### 辅助函数

鉴于典型文档的某些部分遵循特定样式，您可能会发现创建几个辅助函数来简化代码维护和样式变更是有用的。其中一个特别有用的函数将绘制一条水平线，这在生成 PDF 时并非微不足道，如下所示：

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

`drawHR()`函数接受 PDF 资源`$res`作为参数。它使用常量值和具有`texty`参数的`pdf_get_value()`函数来设置线的初始 x 和 y 位置。`pdf_get_value()`函数的第三个参数是一个应用于由第二个参数指定的值的数字“修正器”。在最简单的情况下，此参数的值通常为 0。因此，`drawHR`函数的最后一行可以更优雅地写成：

```php
$ypos = pdf_get_value($res, "texty", (VERT_SPACING * -2));
```

在创建 PDF 文档时，需要掌握的一个有用概念是`path`（路径）。`pdf_moveto()`函数在文档中定位起点，`pdf_lineto()`沿着两个位置之间的路径画一条线。`pdf_closepath()`和`pdf_fill()`函数关闭并填充路径。最后，y 位置增加两倍垂直间距常量。

另一个有用的函数可能会根据传递的参数应用相似但不同的样式：

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
            $text = "* " . $text;
            break;
        case CASE_OBJECTIVE:
            $font = pdf_findfont($res, "Times-Italic", "winansi", 0);
            $xpos = MARGIN + TAB;
            $text = "*" . $text . "*";
            break;
    }
    pdf_setfont($res, $font, 12.0);
    pdf_show_xy($res, $text, $xpos, $ypos);
    return;
}
```

如您将在本节末尾的示例中看到，此代码使用`switch`控制结构根据`$type`参数的值设置特定的字体和文本位置。

字体选择由`pdf_findfont()`函数执行，并通过`pdf_setfont()`函数设置。PHP 的 PDFlib 实现通常在“pdf-related”目录中默认安装几个字体，在

PHP 安装所在的目录。PDFLib 支持多种字体和字形。请参阅 PDFLib 文档以获取完整详细信息。

最后，`pdf_show_xy()`函数会在指定位置显示给定的字符串。

### 关于字体和定位

在前面的代码示例中，你看到了如何通过 PHP 内置的 PDFLib 函数操作各种文本属性。同样，开发者需谨慎使用其他已弃用的函数，例如已被单一的`pdf_get_value()`函数替代的`pdf_get_font()`和`pdf_get_fontsize()`。该函数的使用方法与前述的`pdf_set_info()`完全相同。PHP 文档（<http://www.php.net/manual/en/ref.pdf.php#AEN124842>）列出了已弃用的函数及其替代方案。

> *PDFLib 坐标系将文档左下角的 xy 坐标定义为 0:0。*

你通常会发现为诸如边距、制表宽度、垂直间距和页面尺寸等页面属性定义常量会很有帮助。下表列出了常见页面尺寸的点数维度，其中 1 pt = 1/72 英寸 = 0.3528 毫米。

| 格式 | 宽度 | 高度 |
|---|---|---|
| A4 | 595 | 842 |
| B5 | 501 | 709 |
| Letter | 612 | 792 |
| Legal | 612 | 1008 |

### 收尾工作

如果你只是想创建一个文档并将其放在本地主机的某个位置，完成 PDF 文件只需结束页面并关闭文档即可。但更常见的情况是，缓冲区会返回给 Web 浏览器。`pdf_get_buffer()`函数用于检索传入的 PDF 文档。然后，通过`header()`函数通知浏览器即将接收到一个 PDF 文档，简单地调用`print`即可完成整个过程，如下所示：

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

本部分仅简要介绍了高级 PHP 开发者可用的众多 PDF 生成功能。我们尚未涉及的其他可用功能包括书签、超文本、颜色使用、图形生成和导入，以及这里无法一一列举的更多功能。

### PDF 简历生成器

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
    $font = pdflib_findfont($res, "Times-Roman", "winansi", 0);
    $xpos = MARGIN;
    $ypos = pdf_get_value($res, "texty", 0) - VERT_SPACING;

    switch ($type) {
        case CASE_CATEGORY:
            $font = pdf_findfont($res, "Times-Bold", "winansi", 0);
            $ypos = pdf_get_value($res, 'texty', 0) - (VERT_SPACING * 3);
            break;
        case CASE_LIST:
            $xpos = MARGIN + TAB;
            $text = "*" . $text;
            break;
        case CASE_OBJECTIVE:
            $font = pdf_findfont($res, "Times-Italic", "winansi", 0);
            $xpos = MARGIN + TAB;
            $text = "*" . $text . "*";
            break;
    }
    pdf_setfont($res, $font, 12.0);
    pdf_show_xy($res, $text, $xpos, $ypos);
    return;
}

// 创建资源。
$pdf = pdf_new();
if (!pdf_open_file($pdf, "")) {
    die("Error: Unable to open output file.");
}

// 从数据库收集头部信息。
mysql_connect("localhost", "resume_user", "resume_pw");
mysql_select_db("resume");
$sql = "SELECT * FROM biography WHERE OID = 0";
$result = mysql_query($sql);
$row = mysql_fetch_array($result, MYSQL_ASSOC);
$name = $row["NameFirst"] . " " . $row["LastName"];

// 文档信息。
pdf_set_info($pdf, "Author", $name . " " . $row["Email"] . "<>");
pdf_set_info($pdf, "Title", "Resume - " . $name);
pdf_set_info($pdf, "Subject", "The resume of " . $name . ", "
    . $row["DesiredPosition"] . ".");

// 对关键词做一些巧妙的处理。
$keywords = split(" ", $row["DesiredPosition"]);
$morewords = "";
foreach($keywords as $keyword) {
    $morewords = $morewords . $keyword . ", ";
}
pdf_set_info($pdf, "Keywords", "Resume, " . $morewords . "Apache, MySQL, PHP, PDF");

// 开始 PDF 页面。 -- 可以放在 PDF 资源实例化后的任何位置。
pdf_begin_page($pdf, PAGE_WIDTH, PAGE_HEIGHT);

// 打印姓名。
$font = pdf_findfont($pdf, "Times-Bold", "winansi", 0);
pdf_setfont($pdf, $font, 14.0);
$stringwidth = pdf_stringwidth($pdf, $name, $font, 14.0);
$xpos = (PAGE_WIDTH / 2) - ($stringwidth / 2);
pdf_show_xy($pdf, $name, $xpos, 700);
$xpos = pdf_get_value($pdf, "textx", 0);
$ypos = pdf_get_value($pdf, "texty", 0) - VERT_SPACING;

// 打印联系信息。
$font = pdf_findfont($pdf, "Times-Roman", "winansi", 0);
pdf_setfont($pdf, $font, 12.0);
$headerdata = array(
    $row["Address"],
    $row["City"] . ", " . $row["State"] . " " . $row["ZipCode"],
    $row["Phone"],
    $row["Email"]
);
foreach ($headerdata as $data) {
    $stringwidth = pdf_stringwidth($pdf, $data, $font, 12.0);
    $xpos = (PAGE_WIDTH / 2) - ($stringwidth / 2);
    $ypos = pdf_get_value($pdf, "texty", 0) - VERT_SPACING;
    pdf_show_xy($pdf, $data, $xpos, $ypos);
}

// 打印分类。
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

// 结束文档并将其返回给浏览器。
pdf_end_page($pdf);
pdf_close($pdf);
$buf = pdf_get_buffer($pdf);
$len = strlen($buf);
header("Content-type: application/pdf");
header("Content-Length: $len");
header("Content-Disposition: inline; filename=resume.pdf");
print $buf;

// 清理工作！
mysql_close();
$pdf = 0; 
?>
```



这个简洁的应用程序使用从 MySQL 数据库中提取的数据生成一个简单的 PDF 简历。除了 MySQL 连接设置和数据库查询外，这个脚本中尚未涵盖的唯一方面是使用传记数据将个人期望职位的信息拼接到文档的关键词中：

```php
$keywords = split(" ", $row["DesiredPosition"]); 
$morewords = "";
foreach($keywords as $keyword) {
  $morewords = $morewords . $keyword . ", ";
}
pdf_set_info($pdf, "Keywords", "Resume, " . $morewords . "Apache, MySQL, PHP, PDF");
```

简历的头部信息，包含个人的姓名和联系信息，被单独处理，与简历其余数据分开，以便尽可能简化辅助函数 `pdflib_show()` 的实现。简历的主体由一个 `while` 循环生成，该循环跟踪当前和之前的分类，当值改变时打印分类名称；否则，打印描述。剩下的工作就是关闭文档，将其返回给浏览器，并进行清理。

最后一点建议：如果 PDF 生成在你的任何项目中都扮演着重要角色，你必须阅读并理解随 PDFLib 源代码分发的文档。通常丰富的

## GD 库

关于 PHP 网站上 PDFLib 封装器的文档特别匮乏。虽然本文可以作为一篇极佳的入门介绍，但若要全面了解 PDFLib 库的功能，没有比 PDFLib 手册更好的信息来源了。

如果你曾经需要建立一个包含大量图片的网站，例如图片画廊或电商网站，那么最繁琐的任务之一就是处理并上传所有单张图片。幸运的是，PHP 配备了 GD 库，这是一个随 PHP5 捆绑提供的开源图像处理库。凭借 GD 提供的丰富功能，你可以自动执行网站图像处理任务中的许多甚至全部步骤，这样你只需上传图片，将时间花在其它工作上，而不必整日忙着搬运图片。

### 创建图像基础

GD 库的一个缺点在于其可用的函数数量庞大，其中许多功能相同，仅在输入类型或输出图像格式上有所不同。为了提供清晰度以及本章涵盖的所有图像处理功能的基础，你将创建一个类，该类处理几种最流行图像文件类型 —— JPG、GIF 和 PNG —— 的基本加载和保存。

这个基础类将提供基本的加载、保存和显示功能，并将作为后续章节中你将添加的其他附加图像处理类调用的中心位置。首先，创建一个名为 `class.WebImage.php` 的新文件，并输入以下代码：

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
        // Get image mime type
        $size = getimagesize($file);
        $this->type = $size['mime'];

        // Load image based on type
        switch ($this->type)
        {
            case 'image/jpeg':
                $this->gdresource = imagecreatefromjpeg($file);
                break;
            case 'image/png':
                $this->gdresource = imagecreatefrompng($file);
                break;
            case 'image/gif':
                $this->gdresource = imagecreatefromgif($file);
                break;
        }

        // Retain the alpha information
        imagesavealpha($this->gdresource, true);
    }

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
                if (imageistruecolor($this->gdresource))
                {
                    imagergtopalette($this->gdresource, false, 256);
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
            case 'image/jpeg':
                header('Content-type: image/jpeg');
                imagejpeg($this->gdresource);
                break;
            case 'image/png':
                header('Content-type: image/png');
                imagepng($this->gdresource);
                break;
            case 'image/gif':
                // Convert back to palette
                if (imageistruecolor($this->gdresource))
                {
                    imagergtopalette($this->gdresource, false, 256);
                }
                header('Content-type: image/gif');
                imagegif($this->gdresource);
                break;
        }
    }
}
?>
```

这一切意味着什么？这个文件是一个朴素的图像封装器，你可以用它来打开、保存和显示图像。这段代码可以处理 JPG、GIF 和 PNG 图像，但假设 GD 库支持的话，你完全可以轻松添加更多类型。为了更好地理解正在发生的事情，请查看该类是如何构建的。

开头几行相对简单明了——你通过声明两个公共属性开始，一个用于保存内部 GD 图像资源，另一个用于跟踪图像操作要使用的 MIME 类型。同时注意析构函数——当类被销毁时，它会确保清理 GD 为该图像消耗的任何资源。

下一部分代码从服务器上的文件加载图像数据。你向该方法传递文件名，它会确定图像类型，然后使用 GD 库提供的相应函数将图像加载到 GD 资源中：



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
        case 'image/png': 
            $this->gdresource = imagecreatefrompng($file); 
            break;
        case 'image/gif': 
            $this->gdresource = imagecreatefromgif($file); 
            break;
    }
}
```

在处理包含透明区域（如 GIF 或 PNG）的图像格式时，理解其中涉及的两种不同透明类型非常重要。第一种也是最简单的，是索引透明。它存在于 8 位透明 PNG 图像和所有透明 GIF 图像中，索引透明仅将索引调色板中的一种颜色定义为透明。被分配该颜色的任何像素在屏幕上都会显示为透明。

第二种透明类型是 Alpha 透明，存在于 32 位 PNG 图像中。Alpha 透明图像通过为每个像素提供一个额外的数值范围来实现透明，该范围定义了该特定像素的透明度。Alpha 透明允许图像平滑地淡出至透明，或在特定位置让任何颜色部分透明——这是索引透明图像无法做到的。

在处理 GD 中包含 Alpha 透明的图像时，你需要告知 GD 希望保留从已加载图像中的任何 Alpha 透明信息：

```php
    // Retain the alpha information
    imagesavealpha($this->gdresource, true);
}
```

如果你计划加载或输出任何理解逐像素/Alpha 透明的图像格式，如 32 位 PNG，就需要这样做。如果不告知 GD 保存 Alpha 通道，最终输出中可能会出现意外的背景或透明度问题。

最后两个方法 `save()` 和 `display()` 将内部图像资源发送到最终目的地——要么是服务器上的文件，要么是在浏览器中显示。这两个方法之间唯一的实质区别是 `display()` 中使用 `header()` 函数告知浏览器预期的图像类型，以及 `save()` 中 `image__()` 函数的第二个参数，它告诉 GD 将图像保存到文件，而不是将输出管道到屏幕：

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
                if (imageistruecolor($this->gdresource))
                {
                    imagergtopalette($this->gdresource, false, 256);
                }
                imagegif($this->gdresource, $file);
                break;
        }
    }
```

如果你想为 `save()` 方法添加额外的图像类型，只需将它们作为 `switch` 中的 `case` 添加即可。对于调色板图像类型，务必根据需要像示例中 GIF 图像的情况那样，将图像从真彩色转换为调色板。

### 调整图像大小

现在你已经可以轻松加载和保存一些基本图像格式，是时候对它们进行某种改变。你要做的第一件事是让 `WebImage` 类具备调整图像大小的功能。为此，你将创建一个处理调整大小操作的类文件，并在 `WebImage` 类中添加一个方法来在需要时调用调整大小函数。

首先，创建名为 `class.ImageResize.php` 的以下文件：

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
            if (($this->max_width/$old_width <= $this->max_height/$old_height))
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
            // Code continues...
        }
    }
}
?>
```

## 第 10 章

```php
$new_width = ceil($this->ratio * $old_width);
$new_height = ceil($this->ratio * $old_height);
}

// 仅在尺寸发生变化时执行缩放
if ($new_width and $new_height)
{
	// 创建缩放目标
	$temp = imagecreatetruecolor($new_width, $new_height);

	// 设置 alpha 参数
	imagesavealpha($temp, true);
	imagealphablending($temp, false);

	// 缩放图像
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
```

然后，将以下方法添加到你的 `WebImage` 类定义的末尾：



```php
// 缩放图像
public function resize()
{
	require_once 'class.ImageResize.php';
	$ir = new ImageResize();

	// 根据参数设置缩放参数
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
    // 执行缩放
    $this->gdresource = $ir->process($this->gdresource);
    }
```

查看你刚刚添加到 `WebImage` 中的新方法，你可以快速了解图像缩放类是如何被调用的。首先，根据需要包含 `imageResize.php` 文件，并创建一个新的 `ImageResize` 对象。然后，使用 `func_num_args()` 函数来确定调用方法时使用多少个参数。

`WebImage` 的 `resize` 方法可以使用一个或两个参数进行调用。如果使用一个参数，则将其视为用于缩放的数值比例。如果传递了两个参数，则它们被用作最大宽度和最大高度的值，缩放后的图像将不超过这些值。

在对象中相应地设置这些值之后，调用 `process()` 方法，图像会被缩放并返回。要进一步了解具体的缩放机制，请更仔细地查看 `ImageResize` 类。

在 `ImageResize` 的核心部分 `process()` 方法中，开始部分很简单——分别使用 `imagesx()` 和 `imagesy()` 确定现有图像的宽度和高度，并将新宽度和新高度初始化为 0：

```php
// 缩放图像
public function process($gd_img)
{
    // 设置初始尺寸
    $old_width = imagesx($gd_img);
    $old_height = imagesy($gd_img);
    $new_width = 0;
    $new_height = 0;

    // 新尺寸应在提供的最大值范围内
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
    // 基于比例的新尺寸
    else if ($this->ratio)
    {
        $new_width  = ceil($this->ratio * $old_width);
        $new_height = ceil($this->ratio * $old_height);
    }
```

方法的其余部分是在需要时执行实际缩放的地方。在 GD 中缩放时，你实际上并不是直接缩放现有资源，而是创建一个具有新尺寸的新图像，并将原图像复制到目标位置——GD 会在内部处理缩放。在此方法中，你使用的是 `imagecopyresampled()` 函数；在使用 GD 缩放图像时，你可以使用 `imagecopyresized()` 函数或 `imagecopyresampled()` 函数。两者都达到相同的目的，但后者在保持最终结果“平滑”方面做得稍好一点，而前者往往会导致像素化的结果。请查看：

```php
// 仅在尺寸发生变化时执行缩放
if ($new_width and $new_height)
{
    // 创建缩放目标
    $temp = imagecreatetruecolor($new_width, $new_height);

    // 设置 alpha 参数
    imagesavealpha($temp, true);
    imagealphablending($temp, false);

    // 缩放图像
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

注意 alpha 保存函数 `imagesavealpha()` 和 `imagealphablending()` 的使用。它们用于通知 GD 在执行缩放时保留并使用源图像的 alpha 透明度信息。如果你忽略 alpha，透明 GIF 或 PNG 中可能存在的任何透明度都可能被破坏。

最后，在方法末尾，返回 GD 图像资源。

### 旋转图像

除了在服务器端缩放图像外，常见的图像编辑需求还包括在图像上传后旋转图像的能力。为了实现此操作，你将像之前一样创建另一个图像操作类文件，并添加另一个方法来调用 `WebImage` 中的功能。

首先，创建一个名为 `class.ImageRotate.php` 的文件，其中包含以下图像旋转类：

```php
<?php

class ImageRotate
{
    public $rotation = 0;

    // 旋转图像
    public function process($gd_img)
    {
        if ($this->rotation)
        {
            // 获取“填充”背景颜色
            $color = imagecolorallocate($gd_img, 255, 255, 255);

            // 旋转图像
            $gd_img = imagerotate($gd_img, $this->rotation, $color);
        }

        return $gd_img;
    }
}
?>
```

然后，将以下方法添加到 `WebImage` 类定义中：

```php
// 旋转图像
public function rotate($degrees)
{
    require_once 'class.ImageRotate.php';

    $ir = new ImageRotate();

    // 设置旋转参数
    $ir->rotation = $degrees;

    // 执行旋转
    $this->gdresource = $ir->process($this->gdresource);
}
```

这比缩放方法稍简单，但非常相似。`WebImage` 的 `rotate()` 方法接受一个参数：你想要旋转图像的度数。与 `resize()` 类似，`rotate()` 包含必要的类文件，设置旋转参数，然后执行旋转。

在 `ImageRotate` 内部，它相当直接。`process()` 方法检查是否提供了旋转值，然后获取一种用作背景色的颜色。如果你旋转 90、180 或 270 度，你看不到该颜色；但如果你使用其他值，图像将扩大以包围新的倾斜原始图像，背景色将填充旋转源未覆盖的任何区域。设置颜色后，使用 `imagerotate()` 函数旋转图像：

```php
// 旋转图像
public function process($gd_img)
{
    if ($this->rotation)
    {
        // 获取“填充”背景颜色
        $color = imagecolorallocate($gd_img, 255, 255, 255);

        // 旋转图像
        $gd_img = imagerotate($gd_img, $this->rotation, $color);
    }

    return $gd_img;
}
```

当然，图像资源在末尾返回。

### 添加标题



接下来是简单图像功能系列中的下一项：为图像添加标题——图像底部的一个变暗区域，上面叠加了标题或简短的文字说明。这是一种微妙的方式，用于包含和显示有关图像或其上下文的一点信息，而无需将文本与图像分开，也不至于碍事。

首先，遵循 `ImageResize` 和 `ImageRotate` 的示例，创建一个名为 `class.ImageCaption.php` 的文件：

```php
<?php

class ImageCaption
{
    public $caption = '';
    public $fontfile = '';
    public $fontsize = 10;
    public $padding = 5;
    public $drawline = true;

    // 为图像添加标题
    public function process($gd_img)
    {
        if ($this->caption and $this->fontfile)
        {
            // 获取文本框高度
            $text_box = imageftbbox($this->fontsize, 0,
                $this->fontfile,
                $this->caption);
            $text_height = $text_box[3] - $text_box[5];
            $text_baseline = $text_box[3];

            // 获取某些图像尺寸
            $img_x = imagesx($gd_img);
            $img_y = imagesy($gd_img);

            // 绘制背景阴影
            imagealphablending($gd_img, true);
```
# 第 10 章

```php
$rect_color = imagecolorallocatealpha($gd_img, 0, 0, 0, 75);
imagefilledrectangle($gd_img,
0,
$img_y + $text_height - ($this->padding * 2),
$img_x,
$img_y,
$rect_color);

// Draw caption text
$text_color = imagecolorallocate($gd_img, 255, 255, 255);
imagettftext($gd_img,
$this->fontsize,
0,
$this->padding,
$img_y + $text_underbaseline - $this->padding,
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
$img_y + $text_height - ($this->padding * 2) - 1,
$img_x,
$img_y + $text_height - ($this->padding * 2) - 1,
$line_color);
}

return $gd_img;
}
?>
```

然后，像之前一样，在 `WebImage` 类定义的末尾添加一个新方法，如下所示：

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

当你调用 `WebImage` 的 `caption()` 方法时，最多可以使用五个参数。前两个参数是必需的，分别指定要显示在标题中的文本以及用于标题文本的 TrueType 字体（.ttf）文件名。其他参数用于设置字体大小、文本周围的像素填充量，以及是否绘制一条标题上方的细线。该方法包含所需的类定义文件，整理参数值，然后调用 `ImageCaption` 的 `process()` 方法。

`process()` 方法的作用确定要写入的文本以及目标图像本身的尺寸。为了获取渲染后的文本尺寸，使用了 `imagettfbbox()`。`imagettfbbox()` 接受四个参数：字体大小、字体角度、用于渲染文本的 TrueType 字体文件，以及文本本身。确定文本边界框信息后，将实际高度设置为 `$text_height`，并确定文本基线以下的深度——对于像小写 g 和 p 这样的字母。代码如下：



```php
// Caption the image
public function process($gd_img)
{
    if ($this->caption and $this->fontfile)
    {
        // Get text box height
        $text_box = imagettfbbox($this->fontsize, 0, $this->fontfile, $this->caption);
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
    }
    return $gd_img;
}
?>
```

接下来，在图像上绘制一个带背景阴影的矩形框，提供一个较暗的区域，以便稍后在该方法中将白色文本叠加显示在上面。首先，通知 GD 在目标图像上正确混合透明度。然后，使用 `imagecolorallocatealpha()` 获取一个颜色资源——在这种情况下是黑色 (0,0,0)，透明度约为 60%（alpha 通道的范围是 0–127）。最后，使用半透明黑色颜色，在图像底部绘制一个填充矩形，其高度需要覆盖完整的字体高度以及可能指定的任何填充：

在背景矩形绘制到图像上之后，是时候在顶部添加标题文本了。只需为文本分配一个颜色——在这种情况下是白色——然后使用 `imagettftext()` 在图像上绘制文本：

`imagettftext()` 函数使用八个参数：要添加文本的图像资源、字体大小、文本角度、开始绘制文本的 x 位置、文本基线/底部的 y 位置、文本颜色、.ttf 字体文件名，以及要渲染的实际文本，按此顺序排列。

标题功能的最后一部分使用半透明浅灰色和 `imageline()` GD 函数，在标题框的顶部绘制一条细边框：

### 添加 Logo

你要添加到 `WebImage` 类的最后一项功能是能够在图像上放置 logo 或水印。

首先创建 `class.ImageLogo.php` 文件：



```php
<?php

class ImageLogo
{
    public $logfile;
    public $ratio = 1;
    public $location = array('x' => '', 'y' => '');
    public $padding = 0;

    public function process($gd_img)
    {
        if ($this->logfile)
        {
            require_once 'class.WebImage.php';

            // Load the logo
            $logo = new WebImage();
            $logo->load($this->logfile);

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
                $logo_x = imagexs($gd_img) -
                          $this->padding -
                          imagexs($logo->gdresource);
                break;
            default:
                $logo_x = round((imagexs($gd_img) / 2) -
                                 (imagexs($logo->gdresource) / 2));
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
                      imagex($logo->gdresource),
                      imagey($logo->gdresource));

            return $gd_img;
        }
    }
}
?>
```

接下来，将 `logo()` 方法添加到 `WebImage` 类定义的末尾：

```php
public function logo($logofile,
                    $loc_x = null,
                    $loc_y = null,
                    $padding = null,
                    $ratio = null)
{
    require_once 'class.ImageLogo.php';

    $il = new ImageLogo();

    // Set logo file
    $il->logfile = $logofile;

    // Set location, padding, and ratio if needed
    if ($loc_x !== null)
    {
        $il->location['x'] = $loc_x;
    }
    if ($loc_y !== null)
    {
        $il->location['y'] = $loc_y;
    }
    // ... (code continues)
}
```

# 第 10 章

```php
if ($padding != null)
{
    $il->padding = $padding;
}
if ($ratio != null)
{
    $il->ratio = $ratio;
}

// Perform the logo placement
$this->gdresource = $il->process($this->gdresource);
}
```

与添加到 `WebImage` 的其他操作处理方法类似，`logo()` 方法只是接收提供的参数——标志文件名称、位置 x、位置 y、以像素为单位的填充值以及标志的缩放比例——设置 `ImageLogo` 中所需的属性，并处理标志的应用。

在 `ImageLogo` 的 `process()` 函数内部，你可以确切地看到标志应用过程中发生的事情。`process()` 方法首先创建它自己的内部 `WebImage` 对象，该对象将用于加载标志文件，并在必要时进行缩放。在创建并加载 `WebImage` 后，如果指定了比例，则标志图像会被缩放：

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
    }
}
```

接下来，确定标志的放置位置。标志可以放置在九个位置之一——即三种水平位置和三种垂直位置的任何组合。对于水平位置，可以使用值 `l`、`r` 和 `m` 来指定左对齐、右对齐或居中对齐。垂直位置的类似——`t` 代表顶部，`b` 代表底部，`m` 代表中间/居中：



```php
// Determine logo placement (x)
switch ($this->location{'x'})
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
        $logo_y = imagey($gd_img) -
                  $this->padding -
                  imagey($logo->gdresource);
        break;
    default:
        $logo_y = round((imagey($gd_img) / 2) -
                        (imagey($logo->gdresource) / 2));
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
          imagey($logo->gdresource));
}

return $gd_img;
```

请注意，这里使用的是 `imagecopy()` 而不是 `imagecopymerge()`。`imagecopymerge()` 函数似乎更适合此任务，甚至提供了合并标志并设置其透明度的功能——这对于某些水印效果非常有用。不幸的是，`imagecopymerge()` 有一个坏习惯，即会破坏源标志图像本身的大部分透明信息，因此，如果你想要为图像制作一个淡淡的半透明水印，最好在标志图像本身添加透明度，并使用 `imagecopy()`，而不是使用不透明图像和 `imagecopymerge()`。

### 测试效果

为了充分测试这一组图像处理代码，你需要几样东西：一个要处理的主图像、一个用作标志叠加层的图像，以及一个 TrueType 字体文件。一旦这三样东西准备就绪，创建一个 PHP 脚本来使用你用图像创建的类。首先简单地加载你的图像，并在浏览器中显示它：

```php
<?php

require_once 'class.WebImage.php';

$img = new WebImage();
$img->load('base.png');
$img->display();
?>
```

在浏览器中加载此文件，它应该会显示你的图像，如图 10.1 所示。

![](img/fd2e7361878181c2b12e30301ff3e182_283_0.png)

图 10.1

如果你想在保存或显示图像之前更改图像类型，只需在 `WebImage` 对象中设置图像类型即可：

```php
<?php

require_once 'class.WebImage.php';

$img = new WebImage();
$img->load('base.png');
$img->type = 'image/gif';
$img->display();

?>
```

要调整图像大小，请调用 `WebImage` 的 `resize()` 函数。以下代码使用了 0.75 的比例：

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

![](img/fd2e7361878181c2b12e30301ff3e182_284_0.png)

图 10.2

接下来，旋转你的图像。以下示例使用 180 度进行旋转：

```php
<?php
    require_once 'class.WebImage.php';
    $img = new WebImage();
    $img->load('base.png');
    $img->rotate(180);
    $img->display();
?>
```

在浏览器中加载该脚本，效果如图 10.3 所示。

![](img/fd2e7361878181c2b12e30301ff3e182_285_0.png)

图 10.3

现在，为图像添加标题。此示例使用字体 "Fuji Wide Normal"，但你可以使用任何你手头可用的字体，只要它是 TrueType 字体文件（.ttf）：

```php
<?php
require_once 'class.WebImage.php';
$img = new WebImage();
$img->load('base.png');
$img->caption('An example of plantlife found on Maui.',
'FUJIWRDR.TTF',
15,
5,
true);
$img->display();
?>
```

如果一切顺利，你应该会看到类似图 10.4 的效果。

![](img/fd2e7361878181c2b12e30301ff3e182_286_0.png)

最后，试用图像标志应用功能。在此示例中，你将在图像右下角、标题框上方放置一个标志：

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

现在，应该会出现一个略微缩小的标志，位于右下角，带有 5px 的填充，如图 10.5 所示。

![](img/fd2e7361878181c2b12e30301ff3e182_287_0.png)

如你所见，使用 GD 库并不难，并且允许对图像进行大量的灵活性和控制。还有许多其他更高级的功能可以使用，它们都可以找到 PHP 手册的 GD 部分（http://www.php.net/gd）。

## Ming

`Ming` 是 PHP 的一个第三方扩展，允许用户创建 Shockwave Flash 文件，而无需实际使用 Macromedia 的 Flash 工作室。`Ming` 提供的功能并不总是与 Macromedia Flash 中可用的功能相同，这是由使用 PHP 和 `Ming` 创建 Flash 文件的性质决定的。`Ming` 确实提供了一种创建 Flash 文件的方法，成本低廉，并且允许在需要时动态创建内容。

### 关于 Ming

对于某些人来说，动态创建的 Flash 文件的实用性可能会降低，特别是因为使用 Macromedia Flash Studio 的用户所采用的那种对内容布局的精确视觉控制，你无法拥有。此外，`Ming` 的功能集仅限于 Flash 版本 4，这比最新版本落后了好几个版本。但是，能够通过脚本创建并添加动态内容到应用程序中，这是使用 Macromedia Flash Studio 无法做到的。这在需要 Flash 功能但又希望为用户个性化内容的情况下分发内容时非常有用。



Ming 本身实际上是一个第三方扩展，已经为其编写了 PHP 包装扩展，因此需要在构建二进制文件时编译到 PHP 二进制文件中。Ming 与 PHP 的安装说明可以在 PHP 网站上找到（http://www.php.net/ming）。有关 Ming 本身的更多信息可以在 SourceForge.net 上的 Ming 站点找到（http://ming.sourceforge.net）。互联网上还有许多教程和示例，可以帮助说明 Ming 的功能，并提供适合用作构建 Flash 电影基础的代码片段。

Ming 在 PHP 中实现为对象，因此每次使用 PHP 中的 Ming 创建 shockwave 文件时，你至少需要实例化一个 `SWFMovie` 对象的实例。以下是使用 Ming 和 PHP 生成的一个非常简单的文件的一些代码。要运行此代码，请将其插入到一个不包含其他内容的 PHP 文件中，然后在安装了 Flash 插件的 web 浏览器中查看该文件：

```php
<?php
  header('Content-type: application/x-shockwave-flash');
  $a = new SWFMovie();
  $a->setDimension(100, 100); // width and length in that order
  $a->setBackgroundColor(0, 0, 255); // red, green, and blue integers
  $a->output();
?>
```

这并不会生成太多内容，但确实在浏览器中产生了一个巨大的蓝色屏幕。检查代码，你可以看到使用 Ming 创建的任何 Flash 文件都需要包含的一些必要部分。第一行告诉 PHP 设置 `Content-type` 头，以便浏览器知道这是一个 shockwave 文件并加载相应的插件。下一行实际上创建了 `SWFMovie` 对象的实例。接下来的两行是可选的，但没有它们，将很难判断是否生成了内容，因为它们设置了 shockwave 文件的大小并使背景变为蓝色。最后一行告诉 PHP 将 Ming 生成的文件写入浏览器。真正需要做的唯一事情是

务必在此处设置正确的 `Content-type` 请求头，然后再输出电影文件，同时确保没有向浏览器发送其他任何内容，例如多余的字符或空白。

`SWFMovie` 对象只能有一个实例，但你可以在一个 SWF 电影对象中嵌入多个微型电影。为了做到这一点，你需要使用另一个对象，即 `SWFSprite` 对象。该对象具有与 `SWFMovie` 对象相似的特性和属性，但不再受限于每部电影只能有一个。其优势在于，你可以让多个动画在同一部 Flash 电影中同时显示。这些动画甚至可以以不同的速率运行，并且持续时间也各不相同。

Flash 文件使用*帧*，就像电影或动画中的帧一样。`SWFMovie` 和 `SWFSprite` 对象都提供了向其添加新帧的函数。帧非常有用，因为你可以通过将不同对象包含在特定帧中，从而在屏幕上显示这些对象。这意味着，如果你希望同时显示两个或更多对象，它们必须拥有一个公共帧。一旦某个对象被添加到某个帧中，之后每一个帧都将包含该对象，直到该对象从电影中被移除。同样，就像电影或动画一样，你可以向前或向后跳转，也可以使用 `SWFAction` 对象跳转到特定帧。这种帧的使用方式为在 Flash 电影中组织对象以及生成时间线提供了更好的方式。

Ming 和 Flash 都使用一种坐标系，这可能与你习惯的坐标系不同。Flash 使用的距离单位是 twip。twip 被定义为精确的 $1/1440$ 英寸或 $1/20$ 点大小。这种度量单位通常会被简化，以便更容易转换为 20 个 twip 单位对应 1 个像素值。然而，这可以是一个任意值，因为 Flash 播放器会将电影缩放至播放器窗口自身的大小。幸运的是，Ming 中包含的 `SWFBitmap` 对象具有确定图像 twip 尺寸的功能。因此，如果你需要一个尺寸基于图像大小的电影，你只需创建一个 `SWFBitmap` 对象，读取其宽度和高度值，然后根据这些值设置电影本身的尺寸。电影的尺寸不一定非要在显示之前设置，可以在即将显示前的最后时刻再设置。

### Ming 中的对象

PHP 通过 Ming 提供了 13 种对象用于生成 Flash 文件。你可以组合使用这些对象来创建具有广泛功能性的许多复杂 Flash 文件。它们如下所示：

- `SWFAction` 对象允许你为 Flash 文件添加逻辑和功能，而不仅仅是简单的图像显示。使用 `SWFAction`，你可以移动图像和形状以用于游戏等功能，以及读取和设置 Flash 文件中对象的属性。此外，你还可以包含一些 ActionScript 脚本，这是 Flash 版本的 JavaScript，且非常相似。该对象通常与 `SWFButton` 对象一起使用，以在用户按下按钮时执行某些操作。常见的操作是根据用户的响应在 Flash 电影中显示特定帧。
- `SWFBitmap` 对象允许将图像添加到 Flash 文件中。不过，存在一些限制，因为只有非渐进扫描 JPEG 图像和 DDL（“define bits lossless”，定义位无损）图像才能以此方式添加。其他任何图像都需要使用其他扩展（例如 GD）或通过系统调用工具转换为这两种格式之一。此对象经常与 `SWFSprite` 和 `SWFShape` 对象一起使用。
- `SWFButton` 对象向 Flash 文件添加一个按钮。该按钮可用于启动 `SWFAction` 对象的操作。它对常见的鼠标操作（如鼠标按下、鼠标释放和鼠标划过）做出反应。可以为按钮添加形状以改变其外观。
- `SWFDisplayItem` 对象允许在形状、文本对象、精灵或按钮被添加到电影后，通过引用其添加后返回句柄来对其进行操纵。诸如倾斜、缩放和移动项等操作都是可能的操作。
- `SWFFill` 对象由 `SWFShape` 对象的 `addFill` 方法生成。它允许通过旋转、倾斜和缩放形状的填充来变换填充效果。
- `SWFFont` 对象加载供 `SWFText` 对象使用的字体。该字体可以是字体定义块（FDB）或浏览器定义的字体引用。
- `SWFGradient` 对象创建渐变，然后该渐变可由 `SWFShape` 方法 `addFill()` 使用。
- `SWFMorph` 将接受两个形状，并将第一个形状变形为第二个形状。这可用于一些基本的动画。
- `SWFMovie` 对象是唯一一个其他所有对象正常运作所必需的对象，因为它是实际将 Flash 文件写入文件或浏览器的对象。
- `SWFShape` 对象生成形状。该形状实际上是通过传递坐标，并使用虚拟画笔绘制出来的。借助正确的坐标，几乎可以生成任何形状。此外，如前所述，它与 `SWFBitmap` 对象一起使用，用于向电影中添加图像文件。
- `SWFSprite` 对象通过向该对象添加帧来生成“电影片段”或动画。一个帧包含其他对象之一，例如 `SWFShape`。单个帧中可以包含多个 `SWFSprite` 对象，从而可以看到两个动画同时运行。与仅使用 `SWFMovie` 对象相比，将图像添加到 `SWFSprite` 对象的优势在于，它更好地封装了对象以便于操纵。
- `SWFText` 对象在 Flash 动画中显示文本。如果你只需要显示少量静态信息，使用 `SWFText` 对象的替代方案是直接改用图像代替 Flash 来书写文本。
- `SWFTextField` 类似于 `SWFText` 对象，但有几个不同之处。`SWFTextField` 对象不能被旋转或倾斜，但可以充当表单输入项。

### 创建 Flash 显示

通过再写几行代码，你可以将前面的示例扩展为看起来稍微有趣一些的东西：



```php
<?php
header('Content-type: application/x-shockwave-flash');
$s=new SWFMovie();
$s->setDimension(100,100);  //width and length in that order
$s->setBackgroundColor(0,0,255); // red, green, and blue integers

$s = new SWFShape();  //generate a shape object
$S->setLine(4, 30, 60, 100);  //set the line width to 4 along
// with red, green, and blue integer values
$S->setLeftFill($S->addFill(300, 200, 100));
// /set the color of the shape with red, green
// and integer values
$S->movePenTo(20, 20);

//move our imaginary pen to a new location
$g->drawLineTo(20, 80);
//draw lines to a new set of points
$g->drawLineTo(80, 80);
$g->drawLineTo(80,20);
$g->drawLineTo(20,20);
$a->add($g);  //add the shape to the movie

$a->nextFrame();  //advance a frame in the movie
$a->output();  //output everything to the browser
?>
```

由该电影生成的输出本身并没有什么特别之处，但它展示了一些重要对象的几种基本方法。输出结果应该是蓝色背景，中间有一个绿色方块。

为了更深入地举例说明 Ming 的功能，你将使用它生成一个幻灯片放映。为了使事情更容易，你将使用大小和形状完全相同的图像，并且所有图像都将使用明确的名称。创建一个新文件并包含以下代码行：

```php
<?php
//create a movie object
$movie = new SWFMovie();

//set the background to white
$movie->setBackground(255, 255, 255);
```

在初始设置之后，你需要添加图像引用以包含在幻灯片放映中。这里使用了一个简单的图像名称数组，但这可以扩展为直接从目录读取，甚至从数据库读取。此外，在本示例中，假设所有图像的高度和宽度均为 200 像素。为了简化电影尺寸设置和代码扩展，创建了一个图像的实例来读取其宽度和高度，尽管示例中所有图像的大小都应设为 200 × 200 像素。试一试：

```php
//images to display
$images = array("1.jpg", "2.jpg", "3.jpg");

$bitmapImage = new SWFBitmap(fopen($images[1], "r+b"));
$w = $bitmapImage->getWidth();
$h = $bitmapImage->getHeight();
```

创建一个 `SWFSprite`，它将充当幻灯片放映中的微型电影，并且实际上是受用户控制的对象。为了防止它仅仅显示所有图像，为其添加了一个默认的 `stop()` 操作。此外，电影的大小是根据图像大小计算的，并额外预留了空间以便在图像下方添加按钮。代码如下：

```php
//create a sprite which will act as a mini movie
$sprite = new SWFSprite();
//add stop action to the first frame
$sprite->add(new SWFAction("stop();"));

//set the size of the movie with extra space for buttons
$movie->setDimension((1*$w), (1.5* $h +3));
```

现在，需要将每个图像都添加到精灵中，这可以通过遍历数组轻松实现。首先，每个图像都被转换为 `SWFBitmap` 对象，然后作为填充色添加到 `SWFShape` 对象中。在图形周围画好一条线后，将其添加到 `SWFSprite` 对象中，然后 `SWFSprite` 对象进入下一帧：

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

由于精灵不会自动返回到第一帧，因此需要在最后一帧添加一个动作，使其跳转到第一帧。`gotoFrame()` 动作接受一个帧号作为参数；这里使用 `frame 0`，因为它是精灵中的第一帧。随后，为了确保持完整内容都包含在 `SWFSprite` 对象中，还会向精灵添加另一帧：

```php
//goto frame 0
$sprite->add(new SWFAction('gotoFrame(0);'));
//again generate a new frame
$sprite->nextFrame();
```

现在精灵已创建完成，需要将其添加到 `SWFMovie` 对象中。当它被添加到电影时，会返回一个句柄，该句柄可作为对精灵的引用，以便对其进行控制。为其分配一个名称，并使用该句柄将精灵移动到指定位置：

```php
//add the sprite and get its handler
$handler = $movie->add($sprite);
//we can name the sprite now with the handler
$handler->setName("images");
//we can move the sprite also with the handler
$handler->moveTo(0,2);
```

# 第 10 章

为了创建一个用于控制幻灯片放映的按钮，你需要创建一个新的 `SWFShape` 对象，并为其添加一个按钮图像。

```php
//create a shape again
$shape = new SWFShape();
//create another bitmap this time for a button image
$btmMapImage = new SWFBitmap(open("button.jpg", "rb"));
$fill = $shape->addFill($btmMapImage);
$shape->setRightFill($fill);
//create the border around the shape
$shape->drawLine(0, 0);
$shape->drawLine(0, $h);
$shape->drawLine(-$w, 0);
$shape->drawLine(0, -$h);
```

实例化一个 `SWFButton` 对象，并将按钮形状添加到该 `SWFButton` 对象中。同时，也为按钮设置了默认标志，这允许程序根据按钮是否被按下以及鼠标是否悬停在按钮上来执行操作。此外，还为按钮添加了一个动作，用于将精灵移动到下一帧。



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
$button->addAction(new SWFACTION("setTarget('/images')
;nextFrame();"), SWFBUTTON_MOUSEDOWN);
```

随后，该按钮被添加到电影中，并返回其句柄。接着，将按钮移动到图像下方，并向电影添加一个新帧。然后生成必要的浏览器头信息，并输出电影：

```php
//add the button to the movie and save the returned handler
$handler = $aMovie->add($button);
//use the handler to move the button below the images
$handler->moveTo(0, $h+3);
$aMovie->nextFrame();
//send the appropriate header to the browser
header('Content-Type:application/x-shockwave-flash');
//output the movie to the browser
?>
$aMovie->output();
?>
```

在使用 Ming 时，有几点需要记住。首先，当你直接输出到浏览器时，必须在调用 `SWFMovie` 对象的 `output()` 方法之前发送 `Content-Type` 头。这会发送正确的 HTTP 头，以便浏览器知道加载 Shockwave Flash 插件。这会导致另一个可能出现的错误：输出 `Content-Type` 头以外的任何内容，例如空行。输出头部和电影文件本身以外的内容会导致文件损坏，从而使得浏览器无法正确显示该文件。此外，对最终输出样式有一个大致的布局规划也会有帮助。为了协助使用 Ming 创建的 Flash 电影的布局，你可以使用提供坐标系图形程序，或者仅仅使用方格纸。

## SimpleXML

如今 XML 无处不在，因此拥有一个简单的方法来检索和解析这些文件也就合情合理了。幸运的是，PHP 提供给我们了一个用于利用 XML 数据简单易用的扩展：SimpleXML。SimpleXML 默认已安装，但如果你不打算使用它，建议在 `php.ini` 中禁用它。需要指出的是，SimpleXML 还需要 PHP5。

顾名思义，该扩展的目的是在非常基本的层面上访问 XML 文档。为了说明实现此目的有多简单，创建一个虚构的 XML 文件，其中包含海滨租住的信息（此文件将在所有示例中使用）：

```xml
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
```

既然已经有了 XML 文件，获取信息并将其放入对象中（使用 `simplexml_load_file()` 函数），以便对其进行操作：

```php
<?php
    if (file_exists('beachfront.xml')) {
        $data = simplexml_load_file('beachfront.xml');
        print_r($data);
    }
?>
```

你可以遍历该对象并美观地显示结果（或者至少是以更易读的格式显示）。在 `simple.php` 中添加以下更改：

```php
if (file_exists('beachfront.xml')) {
    $data = simplexml_load_file('beachfront.xml');

    foreach($data as $main) {
        echo "<hr>";
        foreach ($main as $k => $v) {
            echo $k . ":" . $v . "<br />";
        }
    }
}
```

除了 `simplexml_load_file()` 之外，还有很多其他函数与 SimpleXML 扩展配套使用。`simplexml_load_string()` 将 XML 文档作为字符串加载。你首先需要将其内容赋值给一个变量；然后可以使用 `simplexml_load_string()` 函数将变量的内容解析为对象以供使用。如果你想要操作对象，然后将内容以 XML 文件的形式输出回浏览器，你可以使用 `$objectname->asXML()` 函数。如果你需要查看元素的属性或对象任何节点的子节点，`attributes()` 和 `children()` 函数非常有用。如果你想从 DOM 文档中获取一个 DOM 节点并将其转换为 SimpleXMLElement 对象，`simplexml_import_dom()` 函数很有帮助。

`xpath()` 函数允许你通过 XML 文档搜索特定的字符串。它使用 W3C 的路径来评估 XML 文档中的每个节点，并被称为“XPath”，因为搜索关键字类似于文件的路径，因为每个元素都类似嵌套。如果你想进一步了解 XPath，请访问 W3C 关于此主题的资料 `http://www.w3.org/TR/xpath`。

如果你想执行最简单的查询，这是足够的，如下例所示：

```php
if (file_exists('beachfront.xml')) {
    $data = simplexml_load_file('beachfront.xml');

    //find and list all the 'locations' in our XML file
    //*locations* are under *descriptions* which are under *rentals*
    $find = $data->xpath('/rentals/description/location');

    while (list(, $v) = each($find)) {
        echo $v. "\n";
    }
}
```

此脚本将为你提供 XML 文件中名为“location”节点的所有值。如果你想进一步扩展查询，你必须使用另一种方法。记住这是 SimpleXML，而不是 ComplexXML。

SimpleXML 提供了一种非常快速且直接的方式来访问简单的 XML 文档。它允许的功能有限，且仅适用于最简单的 XML 文件。例如，你尝试在包含 HTML 代码内容的 XML 文件上运行这些函数时会遇到问题。否则，与其他可用的 XML/PHP 接口相比，处理起来要简单得多。

## 摘要

还有许多其他的 PHP 扩展可供使用，尽管本章只涵盖了其中的一小部分。完整的列表可以在 PHP 手册（`http://www.php.net`）中找到。您可能需要关注的一些扩展包括：

- `CURL`（客户端 URL 库函数）：除了 http 之外，允许您使用许多不同的协议（如 SSL、FTP 和 gopher）连接页面。



- `DOM`：通过 DOM API 与 XML 文档交互，并随 PHP 默认安装包一起提供。
- `SOAP`：使用 GNOME xml 库启用创建 SOAP 服务器和客户端。
- `ZIP` 扩展（Bzip2, rar, Zip, Zlib）：启用读取 zip 文件，每个扩展处理不同类型的压缩文件。

通过这种对 PHP 扩展的初步体验，我们希望您能充满信心地去探索 PHP 那些鲜为人知但同样有用的功能。

## 11 AJAX

典型的 Web 应用程序通过表单与用户交互。服务器向客户端发送表单，用户输入响应，然后表单提交回服务器进行处理。表单处理完成后，服务器响应一个新的完整页面，其内容通常取决于用户最近的表单提交。在每次与用户的交互中，都需要一个全新的页面。此类应用程序必须使用带宽，在每次页面请求时传输恒定的页面元素（例如站点导航），即使这些元素在之前的响应中已经发送给客户端。此外，此类应用程序比桌面应用程序慢，因为 Web 应用程序在处理某次交互的结果以及新页面加载之前是无响应的。

AJAX（异步 JavaScript 和 XML）指的是一组技术，允许创建富客户端 Web 应用程序，其中应用程序处理的相当大一部分责任交给客户端。具体来说，AJAX 应用程序通常使用 XHTML 和 CSS 进行语义标记和呈现，使用 XML 格式化将在客户端和服务器之间交换的数据，并使用 JavaScript 与服务器通信并操作文档对象模型（DOM）。在使用 AJAX 时，客户端和服务器之间的通信可以仅限于数据，因为客户端具备处理呈现和用户交互所需的必要功能。此外，这种通信是异步进行的，且无需刷新页面。这使得应用程序的客户端部分即使在与服务器交换数据时也能保持响应状态。如果用户执行了需要向服务器发送请求的操作，请求可以被发送，而应用程序可以在等待响应的同时处理进一步的交互（甚至可以发出更多请求）。这一概念在图 11.1 中展示。

当今最流行的 AJAX 应用可能是 Google 的 GMail（http://www.gmail.com），这是一个基于 Web 的电子邮件客户端。在传统基于 Web 的电子邮件客户端中，用户的几乎每个操作都会导致整个页面或框架刷新。由于 GMail 采用了 AJAX，页面永远不会刷新。相反，接口通过基于用户与应用程序的交互以及与 GMail 服务器的 XML 通信，使用 JavaScript 操作 DOM 来动态更新。这使得例如用户可以撰写邮件，点击发送，然后在 GMail 服务器处理发送消息的实际过程时继续阅读他们的邮件。在阅读其余邮件时，他会收到一条状态消息，指示消息已成功发送。

![](img/fd2e7361878181c2b12e30301ff3e182_299_0.png)

## 历史

AJAX 本身并不新鲜；其背后的理念也不是。事实上，过去已经开发并使用了多种方法来在不刷新页面的情况下与服务器通信。

### 图像源技巧

JavaScript 允许使用 `Image` 对象动态加载图像。当创建一个图像并设置其 `src` 属性时，浏览器会发送对该图像的请求，并尝试将响应打包到 `image` 对象中。开发人员利用这一点，通过将 `src` 属性设置为服务器端脚本的 URI，并在查询字符串中将数据传递给服务器，从而实现与服务器的一次性通信。服务器端脚本随后可能更新数据存储。通常，响应中不会返回图像，但这不会造成问题，因为开发人员并未将 `Image` 对象用于其预期目的。

这种技术的优点包括：

- 允许在不刷新的情况下向服务器发送数据。
- 可以通过读取对象的属性来确定请求何时完成。

然而，它也有一些缺点：

- 它无法从服务器接收非图形数据（通信是单向的）。
- 它无法检测或处理在尝试通信期间可能发生的 HTTP 错误。

### 隐藏框架

许多开发人员发现图像源技巧不足，除了发送数据外，还需要从服务器接收信息。于是出现了使用隐藏框架的技术。在这种技术中，开发人员使用一个不可见的框架（通过将高度或宽度设置为 0，具体取决于框架集）作为载体。隐藏框架无非是一个具有最小 HTML 元素集加上脚本元素的页面。脚本元素通常只是数组和变量的定义，其值由服务器写入。因此，控制器框架（可见的那个）可以将此框架的 location 属性设置为服务器端脚本的位置，并可选地通过查询字符串向其发送数据。然后浏览器发出此请求。服务器端脚本处理查询字符串中传递的任何信息，然后以有效的 JavaScript 语法写入数据。查看以下代码以了解基本思路。

```php
<?php
$username = $_GET['username'];
?>
...
<script type="text/javascript">
  top.usernameOK = <?php echo isUsernameAvailable($username); ?>;
  top.usernameAlts =
    new Array(<?php echo implode(',', getSimilarNames($username)); ?>);
  top.frames[1].readVars();
</script>
...
```

这段代码位于隐藏通信框架中。在这个代码示例中，写入一个布尔值以指示通过查询字符串传递给脚本的用户名是否可用。当浏览器的 JavaScript 引擎执行此脚本时，它会将该布尔值存储在名为 `usernameOK` 的 JavaScript 变量中。还向输出写入一个用户名替代数组。在 PHP 中，数组被连接为单个逗号分隔的字符串，以符合 JavaScript 数组语法。(`getSimilarNames` 函数还需要用引号包裹每个数组值。)

当隐藏框架加载 JavaScript 时，它会触发控制器框架，后者可以访问由服务器端脚本写入的变量值，如 `top.usernameOK` 和 `top.usernameAlts`：

```html
<script type="text/javascript">
function readVars()
{
    alert(top.usernameOK);
    alert(top.usernameAlts);
}
self.readVars = readVars;
</script>
```

这段代码位于控制器框架中。将代码封装在一个由隐藏通信框架调用的函数中，是触发通过加载隐藏框架检索数据的一种方法。

这种技术的优点包括：

- 允许在不刷新整个页面的情况下向服务器发送 *以及接收* 数据。
- 一旦数据可用，即可触发主应用程序检索数据。
- 使用和理解简单，因为应用程序使用的所有数据都清楚地显示在隐藏框架的源代码中。
- 它可以接收图形数据，但浏览器对作为图像源的 JavaScript 变量的支持仅部分支持（例如，IE 只喜欢像这样分配的 XBM 图像数据）。
- 由于框架加载会在浏览器历史中添加条目，用户可以使用后退按钮。但是，后退按钮的行为可能不是用户预期的那样。

而缺点包括：

- 它引入了可用性问题，例如无法轻松收藏应用程序状态。
- 它可以通过在超时后重新提交请求来部分检测通信错误。
- 隐藏框架的内容很容易受到用户的操纵（这始终是一个顾虑，但对于用户来说，使用隐藏框架技术这样做相对更容易）。
- 在每个隐藏框架中，给定时间只能发出一个请求（如果响应很重要，这是一个缺点）。

### 隐藏 IFRAME

与隐藏框架技术类似的是隐藏 IFRAME 技术。与其在框架集中使用隐藏框架不同，此方法使用不可见的 IFRAME 元素，通过更改其源位置来向服务器发出请求并接收响应。Google Maps 使用此技术在不刷新页面的情况下与服务器通信。

这种技术的优点如下：

- 它具备隐藏框架技术的所有优点。
- 根据更改 IFRAME 源位置的方式，你可以对后退按钮的行为拥有稍多的控制权。

而其缺点包括：

- 它也面临着与隐藏框架技术类似的可用性问题。
- 它可以通过在超时后重新提交请求来部分检测通信错误。
- 在给定时刻，每个隐藏 IFRAME 只能分派一个请求（如果响应非常重要，这是一个缺点）。
- 在如何以编程方式添加 IFRAME 元素以及在更改源位置后如何引用 IFRAME 中包含的文档响应方面，各浏览器之间存在严重差异。

## XMLHTTP 和 XMLHttpRequest

即便如今被称为“AJAX”的技术也并非新颖。微软的该接口版本 XMLHTTP，自 1998 年后期 IE 5.0 的预览版发布以来，一直作为 ActiveX 对象以各种形式可用（IE 5.0 的最终版于 1999 年 3 月发布）。多年来，许多公司已在仅支持 IE 的环境中利用这一开发模式。在 Mozilla 浏览器产品 1.0 版本发布前不久，一个原生对象（仿照微软的接口设计并命名为 `XMLHttpRequest`）已经可用。近期，Safari（自 1.2 版起）、Opera（自 8 版起）和 Konqueror 也包含了符合标准的接口，同样名为 `XMLHttpRequest`。



在过去几个月里，`XMLHTTP`及其变体的使用量急剧增加。Google 在其 Google Suggest 和 Google GMail 产品中采用该技术，是向大众介绍这种开发方法的主要原因。此外，Adaptive Path 发表的一篇文章提出了“AJAX”这一术语，使得开发者可以用一个统一的名称来指代这组技术，从而促进了该主题的交流与认知度。

## 接口

以下是 `XMLHTTP` 和 `XMLHttpRequest` 接口中相关且在绝大多数浏览器中受支持的方法：

- `abort()`：中止请求。
- `getResponseHeader(key)`：返回名为 `key` 的 HTTP 响应头的值。
- `open(method, uri, [async, [username, [password]]])`：将 HTTP 请求方法设置为 `method`，将请求 URI 设置为 `uri`。可选地，它设置指示是否异步处理请求的标志为 `async`，并在必要时设置用于身份验证的用户名和密码。`method` 属性通常是 `get` 或 `post`。如果你正在通过请求推送数据，使用 `post` 是合适的（参见 `send()` 方法）。在几乎所有情况下，`async` 应保持其默认值 `true`。
- `overrideMimeType(type)`：强制将响应解释为仿佛服务器发送了指定 `type` 的 MIME 类型。此方法在 IE 中不可用。当无法更改服务器以发送特定 MIME 类型时，此方法非常有用。必须在调用 `send()` 之前调用此方法。它还可用于避免 Mozilla 的一个 bug，该 bug 有时会导致浏览器在处理非 XML 响应时挂起。
- `send(requestContent)`：发送 HTTP 请求。参数 `requestContent` 用于方法为 `post` 的请求（参见 `open()` 方法），代表请求体。如果请求是异步的，此方法立即返回。早期版本的 Mozilla 在发送字符串作为请求内容时存在困难。对于 `get` 请求，`requestContent` 应为 `null`。对于 `post` 请求，它必须是 `null`、字符串或 DOM Document 对象。如果是后者，该对象将被序列化。此参数的内容包含在请求体中，因此服务器可以访问它。
- `setRequestHeader(key, value)`：将 `value` 的值分配给名为 `key` 的 HTTP 请求头。此方法必须在调用 `open()` 之后且调用 `send()` 之前调用。

`open()` 和 `send()` 方法处理接口的主要功能。`open()` 方法设置请求的各种参数，如 HTTP 请求方法（`get` 或 `post`）和请求 URL。请求 URL 通常是服务器上待调用脚本的相对位置。如果你愿意，也可以使用完全限定的 URI，但由于安全限制，URI 的域名必须包含发出请求的 JavaScript 的页面所在域名相匹配。这意味着，如果你希望获取位于其他域名上的第三方数据源的数据（例如天气数据源），你必须通过位于你服务器上的服务端脚本来代理这些请求。

`open()` 方法的可选参数 `async` 决定了 `send()` 方法的行为。如果设置为 `true`（或保留其默认值），`send()` 方法将发出 HTTP 请求并立即返回。这意味着在调用 `send()` 之后的 JavaScript 代码行将无论发出请求的响应如何都会执行。相反，响应处理由事件触发，由事件处理器处理。此功能是 AJAX 中第一个 A，它允许你开发行为类似桌面应用程序的应用。此事件处理的具体细节通过接口的属性设置：

- `onreadystatechange`：当 ReadyStateChange 事件触发（即当 `readyState` 属性改变时）时被调用的函数。此属性的值应是一个 JavaScript 函数。确保不要用括号引用该函数，否则函数会被调用，该属性的值最终会变成函数的返回值，而不是函数本身。
- `readyState`：只读。这是一个整数，表示请求的当前状态。此属性的可能值范围为 0 到 4，表示进展程度递增。值为 4 表示请求已完成且响应已完全处理。当 `readyState` 至少为 2 时，响应头和状态可用。
- `responseText`：只读。这是作为文本的响应体。对于成功的请求，从 `readyState` 为 3 开始，它非 `null`。当 `readyState` 为 4 时，`responseText` 完全填充。
- `responseXML`：只读。这是解析为 `text/xml` 内容并打包为 DOM Document 对象的响应体。对于 `readyState` 为 4 的成功请求，它非 `null`。
- `status`：只读。这是整数的 HTTP 响应状态码。`200` 表示成功的响应。有关其他可能的状态码，包括多种错误代码，请参见 HTTP/1.1 RFC 的 6.1.1 节（`http://www.rfc-editor.org/rfc/rfc2616.txt`）。

## AJAX

除 `responseText` 和 `responseXML` 外，这些属性主要涉及确定是否以及何时收到响应。这是必要的，因为我们的请求是异步的，意味着你无法基于执行顺序或时间依赖任何特定代码行处响应的可用性。相反，异步通信依赖于事件驱动模型进行处理。`readyState` 属性包含一个指示请求进度的值。每次该值改变时，都会触发 `readyStateChange` 事件。如果定义了 `onreadystatechange` 处理器，则会调用它来处理 `ReadyStateChange` 事件。请注意，对于给定的请求，`readyStateChange` 事件至少会触发四次。在大多数情况下，除了最后一个事件（当 `readyState` 属性从 3（加载）变为 4（完成）时），你对这些事件都不感兴趣。然而，`readyState` 为 4 并不意味着**请求成功**。它仅表明所有操作已完成。你仍然必须检查 `status` 属性以了解请求是否成功。例如，服务器可能在处理请求时遇到错误。如果 `status` 属性的整数值为 `200`（OK），则请求成功，预期的响应应存在于 `responseXML` 或 `responseText` 中。如果这听起来有点令人困惑，没关系：接下来你将深入查看一些代码，一切将会明了。

## 与接口交互

由于该接口在不同浏览器中具有不同的名称，并且在 Internet Explorer 中（因为接口是 ActiveX 对象）和 Mozilla、Safari、Konqueror 及 Opera 中分别以不同方式实例化，创建请求对象的过程比你想象的稍微复杂一些。这里展示的代码是一种处理这些浏览器差异的基本方法。如果你研究过 AJAX 的实现，很可能见过与此非常相似的代码。

```javascript
function getXMLHTTP() {
var req = false;
// first, try to instantiate the native object
if(window.XMLHttpRequest) {
try {
req = new XMLHttpRequest();
}
catch(e) {}
}
// otherwise, try instantiating the ActiveX
// object for IE.
else if(window.ActiveXObject) {
// just because creation of ActiveX objects
// is supported, doesn't mean the XMLHTTP
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
// req will either be the reference to the`
```

# 第 11 章

```javascript
// interface or false on failure.
return req;
}
</script>
```

这段代码隐藏了在实例化 `XMLHttpRequest` 和 `XMLHttpRequestRequest` 接口时浏览器之间的差异，并返回当前可用的任何版本。

如前所述，对 `XMLHttpRequest` 请求的响应接收是通过触发事件和激活相应的事件处理程序来处理的。下面这组代码展示了处理 ReadyStateChange 事件触发的典型方式，并且只在你感兴趣的事件上执行操作：



```javascript
<script type="text/javascript">
function handleReadyStateChange() {
  if (!request) return;
  // ignore unless complete readyState
  if (request.readyState == 4) {
    // ignore unless successful.
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

该函数被指定为 `onreadystatechange` 处理程序，并在 `ReadyStateChange` 事件触发时被调用。它忽略所有 `readyState` 不为 `4`（完成）以及 HTTP 状态码不为 `200`（OK）的事件。完整且成功响应的 XML 主体被提取并传递给另一个函数进行处理。请注意，在获取 XML 主体后，请求对象被设置为 `false`。这是为了避免 Opera 浏览器中的一个 bug，该 bug 有时会在 `readyState` 变为 `4` 时触发多个 `ReadyStateChange` 事件。这可能导致对单个响应多次执行操作。

## 处理响应

前面各节中的代码相对标准。AJAX 应用的复杂性通常在于解释响应并根据其内容采取适当的操作。通常，适当的操作是通过 JavaScript 对 DOM 进行操纵。例如，如果你向服务器发出请求以检查用户名是否可用，而服务器回复了此处所示的 XML 响应，那么你可能希望向用户显示一条消息，指示他或她需要选择不同的用户名。你可能还希望基于 XML 响应中包含的备选方案提供建议：

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<usernameResult>
  <username value="jessica" available="false" />
  <username value="jess" available="true" />
  <username name="jessica2005" available="true" />
  <username name="jessie" available="true" />
</usernameResult>
```

在这个 XML 响应中，服务器指示该用户名不可用。此外，服务器还建议了一些可用的用户名变体。

向用户传达这些信息的一种方法可能是使用 JavaScript 的 `alert()` 函数打开一个对话框。然而，一种更用户友好的方法可能是使用 DOM 操纵在页面的某一部分添加一个 `DIV` 或 `UL` 元素。这提供了一种侵入性更小的消息形式，并允许用户继续他正在与你的应用进行的任何交互，并在他方便的时候处理该消息。以下代码提供了如何遍历 XML 树并适当操作的一个示例：

```javascript
<script type="text/javascript">
function processResponse(oXML) {
  // exit if xml is undefined or
  // doesn't have a documentElement
  if (!oXML) return;
  if (!oXML.documentElement) return;
  var doc = oXML.documentElement;
  // return a nodeList of all elements
  // named username
  var unames = doc.getElementsByTagName('username');
  var msgs = new Array();
  // iterate through the username nodeList
  for (var i = 0; i < unames.length; i++) {
    var u = unames.item(i);
    var username = u.getAttribute('value');
    var availability = u.getAttribute('available');
    // make the available attribute
    // more user-friendly
    if (availability == 'true') {
      availability = 'available';
    } else {
      availability = 'not available';
    }
    msgs[msgs.length] = 'Username ' + username + ' is ' + availability;
  }
  // create an unordered list element
  ul = document.createElement('ul');
  ul.id = 'msg';
  // for each message, create a list item
  // element and a text node containing
  // the message. The text node is a child
  // node of the list item element, and the
  // list item is a child node of the
  // unordered list element.
  for (var k = 0; k < msgs.length; k++) {
    var li = document.createElement('li');
    var txt = document.createTextNode(msgs[k]);
    li.appendChild(txt);
    ul.appendChild(li);
  }
  // obtain a reference to the main div element
  // and insert our new unordered list just before it
  var maindiv = document.getElementById('maindiv');
  maindiv.parentNode.insertBefore(ul, maindiv);
}
</script>
```

该函数处理来自请求 `responseXML` 属性的 XML，并向 DOM 添加一个 `UL` 元素。

正如你所见，DOM 操纵可能相当复杂。这个特定响应的优势在于，你可以收集用户名元素，无论它们在 XML 响应中的位置如何。通常，你无法直接做到这一点，你必须对 XML 响应的预期结构有一个了解，或者至少知道各种元素与其他元素的对应关系。如果 XML 格式发生任何修改，这可能会引起问题。将响应处理程序附加到 XML *元素* 级别，而不是响应级别，在抽象整个 XML 文档的细节方面显示出一些前景，允许客户端脚本专注于与该特定 DOM 操纵相关的局部结构。

例如，你可能希望在单独的 DOM 元素中显示替代的用户名，在这种情况下，你需要区分那些有或没有 `usernamealts` 父元素的用户名元素。然而，你不需要知道 XML 文档的其余部分是如何结构的，以及这些用户名元素在文档树中的位置在哪里。实现这个想法需要 XML 元素名称和处理函数之间的映射。这种实现的细节超出了本章的范围，但有一些文章更深入地探讨了这一主题。

## AJAX 库

如果这一切看起来令人不知所措，不要害怕。因为 *AJAX* 作为一种开发方法并不是全新的，有大量可用的库可以处理这些繁琐的工作。最近，随着对 *AJAX* 兴趣的复兴，可用的库数量急剧增加，现有的库也在迅速成熟。

### SAJAX

`SAJAX` (http://www.modernmethod.com/sajax/) 是简单的 AJAX 工具包，它在 PHP（以及许多其他语言中）有一个服务器端实现。本质上，使用该库，你可以在 PHP 中定义函数并通过 `XMLHTTP` 请求从客户端调用它们。要使给定函数支持远程过程调用，只需要调用一个 *SAJAX* 函数：`sajax_export('phpFunctionName')`。



不幸的是，当涉及到必要的 DOM 操纵时，`SAJAX` 并不能提供帮助。事实上，由于 `SAJAX` 将响应视为文本，并使用给定元素的 `innerHTML` 属性直接将响应插入到文档中（这通常被认为不如 DOM 操纵好），除非你自己实现字符串解析算法，否则无法进行 DOM 操纵。在 `SAJAX` 的常见问题解答页面（`http://www.modernmethod.com/sajax/faq.php#ml`）上，开发者将“不过度抽象”列为一个特性。`XMLHTTP` 通信的许多方面可以从抽象中受益匪浅，因此你可能认为 `SAJAX` 缺乏抽象是一个缺点。尽管如此，`SAJAX` 提供了一种简化客户端 AJAX 请求的服务器端处理以及客户端实例化 `XMLHTTP` 请求对象和发出必要请求的处理的方法。

### CPAINT

`CPAINT` (`http://cpaint.sourceforge.net/`) 是跨平台异步接口工具包。它支持纯文本和 `XML` 响应类型。此外，它还支持将响应直接作为 JavaScript 对象检索。该库成熟且积极开发中。

`CPAINT` 从函数调用中为你生成 `XML`，结果是某种非语义结构。另外，出于某种未知原因，生成的 `XML` 元素都是大写的。如果你提供的元素名称不是全大写的，该库会将其转换为全大写。库使用的文档有点难读，但每个部分都解释得很好，并为每个部分提供了一个简单的示例，帮助你理解其思想。

### JPSPAN

`JPSPAN` (`http://jpspan.sourceforge.net`) 的主要目标是弥补 JavaScript 和 PHP 之间的差距。它允许无缝将 PHP 类导入到 JavaScript 中。这意味着你可以在 PHP 中定义一个类，并像调用本地 JavaScript 对象一样调用其方法。在幕后，`JPSPAN` 正在向服务器发出请求以远程执行方法。其他库提供类似的功能，但它们无法接近 `JPSPAN` 所提供的抽象。`JPSPAN` 的文档和示例代码丰富且清晰。两者都是 wiki 格式，因此不断增长。代码本身干净易读，就像它生成的 `XML` 一样。此外，目前正在开发将 `JPSPAN` 嵌入 PHP 框架的初步工作，以使其更容易开发富客户端应用程序。

该库并没有减轻 DOM 操纵任务，但它确实很好地抽象了 `XML-HTTP` 的使用。不幸的是，它似乎存在支持 Opera 的问题，但它很好地支持基于 Mozilla 的浏览器和微软的 IE。此外，根据你的应用程序，JavaScript 和 PHP 之间的桥接可能对你没有多大好处，只是用对象和本地 JavaScript 访问替代了 `XML` 树遍历。由于创建 PHP 类的本地 JavaScript 版本涉及额外的开销，好处可能并不抵得上成本。然而，由于对抽象的出色利用，`JPSPAN` 可以让你几乎完全忽略 PHP 类如何提供给 JavaScript 的细节，并将注意力集中在应用程序本身的功能上。

还有许多其他支持 PHP 的 AJAX 库。你可以在 `http://www.ajaxpatterns.org/AJAXFrameworks` 了解各种 AJAX 库的更多信息。

## 何时不使用 AJAX

对 AJAX 的爆炸性兴趣是一把双刃剑。Macromedia 的 Flash 产品的使用也曾出现过类似的繁荣。客户因为 Flash 看起来很酷而要求使用它。与 Flash 一样，AJAX 引入了可用性和可访问性问题，其中许多问题在传统 Web 应用程序中已经得到解决。

## 第 11 章

例如，AJAX 应用程序存在于一个统一的 URI 命名空间中。换句话说，当用户与应用程序交互时，URI 并不会改变。这是合理的，因为这是 AJAX 的主要卖点之一：无需刷新当前页面或跳转到其他页面即可更改应用程序状态。然而，这使得浏览器的后退按钮变得毫无用处，甚至可能导致用户彻底离开你的应用程序。

1999 年，著名可用性专家雅各布·尼尔森（Jakob Nielsen）发表了一篇文章，指出了 Web 设计的十大错误。其中第一大错误是破坏了浏览器后退按钮的功能。根据尼尔森的说法，在超链接之后，后退按钮是“使用频率第二高的导航功能”。确实存在一些变通方法，可以部分复制后退按钮的功能。

另一个相关的可用性问题与无法书签特定的应用程序状态有关。在传统应用程序中，应用程序状态通常对应于单个唯一的 URI，因此可以被书签。例如，当用户浏览产品目录并进入特定产品的详情页面时，用户可能希望为此页面添加书签以便稍后查看。此外，用户可能希望让朋友查看该产品，并尝试通过电子邮件发送该 URI。破坏此书签功能可能会严重影响口碑广告的有效性。存在变通方法可以实现这一功能的一半，即接收给定的 URI 并将其转发给你的 AJAX 应用程序以重建所需的应用程序状态。然而，由于对于任何给定的状态，地址栏中并不包含此 URI，这种方法仍然无法解决告知用户如何确切书签当前应用程序状态的问题。浏览器的书签功能变得毫无用处，应用程序必须提供其他书签手段，通常涉及非标准的用户界面元素。

为了解决这些可用性和可访问性问题的工作正在进行，并且取得了进展。然而，经常被忽视的问题是：可用性问题是技术使用不当的结果吗？Flash 的可用性问题就是这样：开发人员试图使用 Flash 文件来实现基于 Web 的完整应用程序。导致可用性问题的不是 Flash 技术本身，而是这种误用。AJAX 的误用也是如此。在那些恢复给定应用程序状态意义不大的应用程序中，该技术表现非常出色。谷歌的 GMail 就是一个很好的例子。在基于 Web 的电子邮件客户端中，书签给定状态的价值微乎其微。表单增强功能，如 Google Suggest，是另一个很好的例子。在 Google Suggest 中，无需书签状态。基于 Web 的客户端也不会从书签特定应用程序状态的能力中获益良多。相比之下，如果书签状态的能力被破坏，产品目录将遭受巨大损失。如果无法书签特定文章的显示，内容管理系统的可用性也会受到严重影响。

将 AJAX 技术应用到任何传统 Web 应用程序的诱惑是可以理解的。然而，许多传统 Web 应用程序使用 AJAX 后会受到损害。那些自然倾向于从 AJAX 中受益的应用程序的共同点是它们传统上都是桌面应用程序。GMail 是电子邮件客户端的基于 Web 的版本，而电子邮件客户端之前作为桌面应用程序表现最佳（事实上，传统基于 Web 的电子邮件应用程序出现的真正原因是能够随时随地访问）。Google Suggest 的行为非常像传统桌面应用程序中的表单控件。除了 Java applet 和类似解决方案外，应用程序几乎专门是桌面应用程序。开发人员曾尝试制作聊天应用程序的纯标记和 JavaScript 版本，但这些应用程序与其原生版本相比并不逊色。

虽然肯定存在例外，但一个好的经验法则是：AJAX 适合将传统桌面应用程序或其元素转化为基于 Web 的版本。它为 Web 应用程序开辟了新的可能性，但并不一定有利于传统功能。在决定是否使用 AJAX 时应谨慎，并自问 AJAX 对你正在开发的应用程序是否*有益*。如果你遇到了需要复杂变通方法才能解决的重大可用性问题，那么 AJAX 很可能不是合适的开发模式。

除了可用性问题外，还有支持方面的问题。拥有一个依赖 AJAX 且没有为旧浏览器提供回退支持的应用程序，可能会阻挡住很大一部分潜在用户群。即使是对于当前浏览器，一些公司出于安全原因也*要求*部分或完全禁用 JavaScript。如果应用程序不能良好降级并提供传统 Web 应用程序功能作为安全网，这些用户也将被阻挡在你的应用程序之外。这是否可接受将取决于你的应用程序性质，因为对于某些应用程序，提供传统版本并不实际。其可接受性还取决于你预期的受众及其可能的浏览器选择。

## 更多信息

本章中讨论的主题的更多信息可以在以下资源中找到：

- Dynamic HTML and XML: The XMLHttpRequest Object. Apple, Inc. <http://developer.apple.com/internet/webcontent/xmlhttpreq.html>

- XMLHTTP: Wikipedia, the free encyclopedia. <http://en.wikipedia.org/wiki/XMLHttpRequest>

- AJAX: Wikipedia, the free encyclopedia. <http://en.wikipedia.org/wiki/AJAX>

- XMLHttpRequest: XULPlanet.com. <http://xulplanet.com/references/objref/XMLHttpRequest.html>

- XML Extras: The Mozilla Foundation. <http://www.mozilla.org/xmlextras/>

- AJAX Patterns: <http://www.ajaxpatterns.org/>

- AJAX Matters: <http://www.ajaxmatters.com/>

## 摘要



在本章中，你学习了如何使用 AJAX 将 Web 应用程序的大部分处理工作推送到客户端。你还了解到，AJAX 并不是一种新的趋势，实际上是几种较旧技术的产物，每种技术都有一些使其不如理想的缺点。本章展示了如何使用 AJAX 接口，以及如何处理和客户端响应。它还介绍了一些你可以使用的 AJAX 库，甚至讨论了你不应该使用它的情况。

# 第 12 章 缓存引擎

你已尽力清理代码并减少 PHP 脚本中的处理负载，但似乎仍无法使页面足够快以让用户满意。是时候放弃了吗？还不完全是——你可以从 LAMP 配置中获得更多性能提升，而缓存引擎将帮助你实现这一点。

在处理 PHP5 的不同缓存解决方案时，你有几种选择。一些配置实际缓存内部编译的 PHP 脚本，其他缓存生成的输出，还有一些缓存中间数据处理对象。本章向你介绍几种缓存引擎，并帮助你决定哪一种适合你。

## Alternative PHP Cache

Alternative PHP Cache，简称 APC，是一种 PHP 操作码缓存引擎，现在作为 PECL/PEAR 仓库的一部分免费提供。APC 起源于 Daniel Cowgill 和 George Schlossnagle，并由 Community Connect, Inc. 发布。在 PHP5 发布后，Yahoo! 修改了 APC 以支持新的 Zend 引擎，自此它成为 PECL 的一部分。

APC 通过从 PHP 运行时引擎获取编译后的代码并将其存储在共享内存中以供后续访问来工作。每次下载脚本时，APC 首先检查共享内存中是否有版本，然后再重新编译并执行磁盘上的脚本。由于 PHP 无需每次都重新编译脚本，因此可以大大加快响应时间——在某些情况下，速度提升可达四倍或更多。

APC 可以作为动态共享对象 `DSO` 安装，也可以静态编译到 PHP 中。以下部分向你展示如何安装 DSO 版本，因为它不需要你重新编译 PHP，并且提供了随时添加或移除 DSO 的灵活性。

### 安装 APC

首先，从 PECL 网站获取最新版本的 APC 源代码副本：`http://pecl.php.net/package/APC`。

一旦你获取了 tar/gzip 格式的源代码副本，请解包并切换到新创建的源代码目录中：

```bash
tar -xzvf APC-3.0.5.tgz
cd APC-3.0.5
```

接下来，在源代码目录中运行 `phpize`。请务必使用与你安装环境匹配的 `phpize` 的正确路径（它是 PHP 自带的）：

```bash
/usr/local/bin/phpize
```

当 `phpize` 运行时，你应该看到类似以下的输出：

```text
Configuring for:
PHP Api Version:    20031224
Zend Module Api No:  20041030
Zend Extension Api No: 220040412
```

`phpize` 完成后，运行以下 configure 脚本，再次替换为你 `php-config` 和 `apxs` 程序的适当路径：

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

构建完成后，安装 DSO（以 root 权限执行）：

```bash
make install
```

此时，你的 PHP 扩展目录中应该有一个 `apc.so` 的副本。

要完成安装，请将以下内容添加到 `php.ini` 文件的扩展部分，然后重启 Apache：

```ini
extension="apc.so"
```

### 配置 APC

在大多数情况下，APC 使用的默认配置就足够了，但如果你想根据需求或系统微调缓存，可以在 `php.ini` 中使用以下指令：

#### 缓存引擎

| 指令 | 默认值 | 设置位置 | 描述 |
|---|---|---|---|
| `apc.enabled` | 1 (启用) | `php.ini`, `httpd.conf`, `.htaccess` 和用户脚本 | 相应地使用值 1 或 0 来启用或禁用 APC。如果在 `php.ini` 中，这个设置仅在 APC 被静态编译进 PHP 时才真正有用——如前所述安装 APC 时，你只需注释掉 `extension="apc.so"` 这一行即可。然而，该设置可以在用户脚本和 `.htaccess` 文件中更改，因此你可以用它来在单独的脚本和目录中启用/禁用缓存引擎。 |
| `apc.shm_segments` | 1 | `php.ini` 和 `httpd.conf` | 使用数值，你可以指定 APC 使用的共享内存段数量。许多操作系统对每个共享内存段的大小有限制，通常较低。如果 APC 内存不足，增加此值将使 APC 使用更多的段，以帮助绕过操作系统限制。 |
| `apc.shm_size` | 30 | `php.ini` 和 `httpd.conf` | APC 共享内存段的大小，以 MB 为单位。根据操作系统的不同，可能存在大小限制，通常较低。请查阅你的操作系统文档以获取有关共享内存段大小的更多信息。 |
| `apc.optimization` | 0 (关闭) | `php.ini`, `httpd.conf`, `.htaccess` 和用户脚本 | 这是一个实验性设置，该指令控制 APC 的内置优化器。随着该设置值的增加，优化器的激进度也会增加。值为 0 时完全禁用优化。 |
| `apc.num_files_hint` | 1000 | `php.ini` 和 `httpd.conf` | 此设置向 APC 提供有关你的网站定期提供的独立源文件数量的提示。 |
| `apc.ttl` | 0 | `php.ini` 和 `httpd.conf` | 定义每个缓存条目允许在缓存中持久存在的秒数，在此之后允许较新的条目覆盖它。如果保持为 0，缓存可能会填满过期的条目，从而阻止较新的条目被缓存。 |
| `apc.gc_ttl` | 3600 | `php.ini` 和 `httpd.conf` | 定义每个缓存条目在垃圾收集列表中保留的秒数。作为一种安全措施，用于处理服务器进程死亡导致缓存文件滞留在缓存中的情况。值为 0 时禁用此功能。 |
| `apc.cache_by_default` | On | `php.ini` 和 `httpd.conf` | 控制所有文件的缓存。使用此指令禁用所有脚本的默认缓存，允许你使用下面的 `apc.filters` 指令来更精确地控制哪些文件实际上被缓存。 |
| `apc.filters` | "" (空字符串) | `php.ini` 和 `httpd.conf` | 允许你定义一个逗号分隔的正则表达式列表，用于过滤哪些文件被缓存。使用 POSIX 扩展正则表达式——类似于 PHP 的 `ereg` 函数——你指定一个正则表达式列表来排除某些脚本不被缓存。任何匹配列表中模式的文件名都不会被缓存，除非模式以 `+` 开头，在这种情况下它们将被 APC 缓存。创建正则表达式时，假设相对文件名路径，而不是绝对路径。 |
| `apc.slam_defense` | 0 (禁用) | `php.ini` 和 `httpd.conf` | 使用 0 到 100 的数字定义，此指令指定服务器进程跳过缓存先前未缓存文件的可能性。`apc.slam_defense` 主要用于极其繁忙的 Web 服务器，用于解决多个服务器线程试图同时缓存同一文件时的竞态条件。 |

### 移除 APC

如果在安装 APC 后你不再需要它，你可以遵循以下简单步骤将其从 PHP 安装中移除。

首先，搜索并删除 `php.ini` 文件中的 `extension="apc.so"` 行。或者，你可以直接将其注释掉：

```ini
;extension="apc.so"
```

此时，你可以重启 Apache，APC 将不再在 PHP 中处于活动状态。如果你希望彻底从机器上清除 DSO，可以在重启 Apache 后，从 PHP 扩展目录中删除 `apc.so` 文件。

## eAccelerator

`eAccelerator` 是另一种编译状态 PHP 缓存引擎，类似于 APC。`eAccelerator` 是流行的 PHP4 TurckMMCache 缓存引擎的一个分支，目前由 Frank Alcantara 和 SourceForge 程序员团队维护的一款免费编码器和优化器。

除了作为 PHP 优化器和缓存引擎，你还可以使用 `eAccelerator` 来编码你的 PHP 脚本，这样你就可以将编码后的版本分发给安装了 `eAccelerator` 的客户端，而无需担心源代码被窥探。

与其他 PHP 编码解决方案一样，*当文件使用 `eAccelerator` 编码后，使用标准工具几乎不可能解密。然而，可以通过针对 PHP 引擎本身的调试器和反汇编器进行逆向工程，但通常这种努力与其可能获得的回报相比并不值得。*

### 安装 eAccelerator



与 `APC` 类似，`eAccelerator` 可以安装为 `DSO`，使用以下流程。首先，下载源代码副本，可从 `http://eaccelerator.net/` 获取。

> 不幸的是，*此时 `eAccelerator` 与 `PHP` 的 `CGI` 二进制版本不兼容。如果你运行的是 `CGI` 二进制版本，本节仅供参考。*

解包你下载的 `tarball`，然后进入新创建的目录：

```bash
tar -xzvf eaccelerator-0.9.3.tar.gz
cd eaccelerator-0.9.3
```

在此目录中运行你的 `phpize` 副本（再次，根据情况修改路径）：

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

构建完成后，以 `root` 权限安装 `DSO`：

```bash
make install
```

接下来，你需要为 `eAccelerator` 提供一个存放临时文件的地方。在 `/tmp` 文件夹中创建一个 `eaccelerator` 目录：

```bash
mkdir /tmp/eaccelerator
chmod 0777 /tmp/eaccelerator
```

最后，将以下内容添加到 `php.ini`，然后重启 `Apache`：

```ini
extension="eaccelerator.so"
```

### 配置 eAccelerator

与 `APC` 类似，默认选项在大多数情况下可能已经足够，但如果不够，你可以访问以下 `php.ini` 指令：

## 第 12 章

### 缓存引擎

| 指令 | 默认值 | 配置位置 | 描述 |
|---|---|---|---|
| `eaccelerator.shm_size` | 0 | `php.ini` 和 `httpd.conf` | 定义 `eAccelerator` 用于缓存脚本的共享内存量（以兆字节为单位）。值为 0 时，指示 `eAccelerator` 使用操作系统的默认值。 |
| `eaccelerator.cache_dir` | `/tmp/eaccelerator` | `php.ini` 和 `httpd.conf` | 指定如果使用磁盘缓存，则用于磁盘缓存的目录。 |
| `eaccelerator.enable` | 1 (启用) | `php.ini`, `.htaccess` 和用户脚本 | 允许通过数值 1 和 0 分别启用和禁用 `eAccelerator`。此设置可以在用户脚本和 `.htaccess` 文件中更改，因此你可以用它来在单个脚本和目录中启用/禁用缓存引擎。 |
| `eaccelerator.optimizer` | 1 (启用) | `php.ini`, `httpd.conf`, `.htaccess` 和用户脚本 | 启用 `eAccelerator` 的内部代码优化引擎。值为 1 时启用优化器，值为 0 时禁用。此设置可以在用户脚本和 `.htaccess` 文件中更改，因此你可以用它来在单个脚本和目录中启用/禁用优化引擎。 |
| `eaccelerator.debug` | 0 (关闭) | `php.ini` 和 `httpd.conf` | 切换调试日志的开启和关闭。 |
| `eaccelerator.check_mtime` | 1 | `php.ini` 和 `httpd.conf` | 此设置控制 `eAccelerator` 是否检查文件的修改时间以查看其是否已更改。启用值 1 会指示 `eAccelerator` 在 `PHP` 脚本发生更改时自动重新编译该脚本。 |
| `eaccelerator.filter` | "" (空字符串) | `php.ini`, `httpd.conf`, `.htaccess` 和用户脚本 | 此指令允许你指定一个空格分隔的列表，指示哪些文件应和不应由 `eAccelerator` 处理。该列表由具有通配符匹配的简单文件名组成（例如，"*.php *.phtml*"）。若要忽略特定的匹配项，请在相关模式前加感叹号。 |
| `eaccelerator_shm_max` | 0 (无限制) | `php.ini` 和 `httpd.conf` | 指定使用 `eaccelerator_put()` `PHP` 函数放入共享内存的数据的最大尺寸。数值以字节指定，值 0 禁用限制。 |
| `eaccelerator.shm_ttl` | 0 (从不删除过期脚本) | `php.ini` 和 `httpd.conf` | 定义脚本在 `eAccelerator` 共享内存中保持缓存状态的秒数，在此之前允许将其从缓存中移除以便为新请求腾出空间。值 0 表示不应移除项，这可能导致共享内存缓存最终填满并阻止新请求被缓存。 |
| `eaccelerator.shm_prune_period` | 0 (从不删除过期项) | `php.ini` 和 `httpd.conf` | 类似于 `shm_ttl` 设置，此指令控制从共享内存缓存中收集过期脚本。它不是作为缓存中单个脚本的超时，而是通过仅在 `shm_prune_period` 中定义的值已过期的情况下移除过期项来工作。此值以秒数表示，值 0 指示 `eAccelerator` 不要尝试移除过期项。 |
| `eaccelerator_shm_only` | 0 (使用两者) | `php.ini` 和 `httpd.conf` | 启用和禁用（0 或 1）磁盘缓存。值 0 指示 `eAccelerator` 同时使用共享内存和基于文件的磁盘缓存，而值 1 指示 `eAccelerator` 仅使用共享内存。 |
| `eaccelerator_compress` | 1 (启用压缩) | `php.ini`, `httpd.conf`, `.htaccess` 和用户脚本 | 此指令启用和禁用输出内容压缩，类似于 `Apache` 的 `mod_deflate` 或 `PHP` 的 `gzip` 输出缓冲。 |
| `eaccelerator_compress_level` | 9 (最大压缩) | `php.ini`, `httpd.conf`, `.htaccess` 和用户脚本 | 此设置控制在 `eaccelerator_compress` 中启用输出压缩时使用的压缩级别。最大值 9 使用高压缩，导致传输的文件尺寸更小，而较低的值会降低压缩并增加传输尺寸。 |
| `eaccelerator.sessions` | `shm_and_disk` | `php.ini` 和 `httpd.conf` | 你可以使用此指令告诉 `eAccelerator` 你希望它在哪里存储会话数据和内容。值 `shm_and_disk` 指示缓存引擎在共享内存和磁盘位置都存储会话数据和内容。设置为 `shm`，它将使用共享内存作为主要存储位置，如果共享内存已满则回退到磁盘存储。`shm_only` 表示你希望仅使用共享内存且不使用磁盘回退。`disk_only` 的行为完全相反：它表示你希望仅使用磁盘存储且不使用共享内存。 |

### 移除 eAccelerator

移除 `eAccelerator` 很简单，只需删除或注释掉 `php.ini` 中相应的扩展行，如下所示：

```text
;extension="eaccelerator.so"
```

要从系统中永久移除 `eAccelerator`，请从 `PHP` 扩展目录中删除 `eaccelerator.so` 文件。

> *有关 `eAccelerator` 的更多信息，请访问* [`http://eaccelerator.net`](http://eaccelerator.net)。

## Zend Optimizer

为了不被市面上少数免费的 `PHP` 缓存解决方案所超越，`Zend`——即驱动 `PHP` 的 `Zend` 引擎的创建者——发布了他们自己的代码优化器，并且它是免费的。`Zend Optimizer` 的作用方式与 `APC` 和 `eAccelerator` 类似：它缓存 `PHP` 脚本的编译状态，从而加快后续请求的执行速度。

除了加速 `PHP` 脚本的性能外，`Zend Optimizer` 还允许你在服务器上运行由 `Zend Encoder` 或 `Zend SafeGuard Suite` 编码的脚本。

### 安装 Zend Optimizer

安装 `Zend Optimizer` 比大多数竞争性的缓存解决方案更容易，因为它附带了一个便捷的安装配置向导。

首先，从 [`http://zend.com/store/products/zend-optimizer.php`](http://zend.com/store/products/zend-optimizer.php) 下载适合你系统的软件包。

然后，解压缩归档文件，并进入新建的目录：



```bash
tar -xzvf ZendOptimizer-2.5.10a-linux-glibc21-i386.tar.gz
cd ZendOptimizer-2.5.10a-linux-glibc21-i386
```

以 root 用户运行安装向导：

```bash
./install.sh
```

运行向导，在提示时指定必要的路径。提供的默认值通常就足够了。当被问及 Apache 版本时，确保你选择了正确的版本（本书编写时基于 Apache 2）。

向导会创建 `php.ini` 文件的备份副本，并创建一个指向经过 Zend 修改的 `php.ini` 文件的新符号链接。

在向导结束前，你可以选择让 Apache 自动重启，或者如果你愿意，退出向导并手动重启 Apache。

### 配置 Zend Optimizer

与 APC 和 eAccelerator 一样，你有几个指令可用于调整 Zend Optimizer 的操作：

| 指令 | 默认值 | 配置位置 | 描述 |
| :-- | :-- | :-- | :-- |
| `zend_optimizer.optimization_level` | 15 (所有优化) | `php.ini` 和 `httpd.conf` | 确定 Zend Optimizer 执行的优化级别。优化器可以对每个脚本执行四个不同的遍历，通过组合以下值来控制：<br> - 0: 无遍历 <br> - 1: 遍历 1 <br> - 2: 遍历 2 <br> - 4: 遍历 3 <br> - 8: 遍历 4 <br> 你只需将每个遍历的数值相加即可得到你的优化遍历设置。例如，值 11 将执行遍历 1、遍历 2 和遍历 4 (1+2+8)。 |
| `zend_optimizer.enable_loader` | 1 (启用) | `php.ini` 和 `httpd.conf` | 你可以使用此指令在不卸载 Zend Optimizer 的情况下启用或禁用它。值 0 禁用优化器；值 1 启用它。 |

### 移除 Zend Optimizer

要移除 Zend Optimizer，你必须首先删除它为 `php.ini` 创建的符号链接。然后，将备份的原始 `php.ini` 文件恢复到其原位置。此时你可以重启 Apache，Zend Optimizer 将不再处于活动状态。如果你愿意，可以删除 Zend Optimizer 文件——其默认位置是 `/usr/local/Zend`。

## JPCache

内存/磁盘缓存解决方案领域的另一项条目是 JPCache。与 APC 和 eAccelerator 不同，JPCache 不需要编译为 DSO 或静态构建到 PHP 本身中。JPCache 实际上是用 PHP 编写的，并使用标准的 `include` 和 `require` 语句。

JPCache 通过将 PHP 脚本生成的输出存储到磁盘或 SQL 服务器中，而不是保存每个脚本的编译状态，从而工作。通过以这种方式缓存输出，并结合 gzip 内容压缩，你可以实现高达 80% 或更多的带宽节省。

### 安装 JPCache

要开始使用 JPCache，你需要做的第一件事是下载最新版本的副本，地址为 [http://www.jpcache.com](http://www.jpcache.com)。

接下来，提取 tar/gzip 归档文件：

```bash
tar -xzvf jpcache.v2.tgz
```

此目录的内容现在包含你需要用来使用 JPCache 的脚本。将此文件夹放在你喜欢的任何位置，只要它可被 Apache 运行的用户访问即可。记下该位置的完整路径，因为你在配置缓存时需要它。

在你的 JPCache 文件夹的基础目录中，编辑 `jpcache.php` 文件。将以下行更改为指向你放置 jpcache 文件夹的位置：

```php
$includedir = "/path/to/jpcache-files";
```

例如，如果你将提取的 jpcache 文件夹移动到 `/www/jpcache`，你将使用以下值：

```php
$includedir = "/www/jpcache";
```

接下来，编辑 `jpcache-config.php` 文件。最重要的是，你需要取消注释指示你希望使用何种类型的缓存存储（文件或 MySQL）的行。对于这个示例，取消注释基于文件的存储选项：

```php
$JPCACHE_TYPE = 'file';
```

## 缓存引擎

另一个需要更改的设置是 `$JPCACHE_USE_GZIP` 的值。这启用了 gzip 内容压缩，但不幸的是，由于 JPCache 最近版本中的一个 bug，在某些浏览器中输出可能会损坏。为了安全起见，请将此值设为 0：

```bash
$JPCACHE_USE_GZIP = 0;
```

此外，请注意控制文件缓存位置设置 `$JPCACHE_DIR`，其默认值为 `/tmp/jpcache`。您需要实际创建 `$JPCACHE_DIR` 设置中列出的文件夹，因此在命令提示符下执行以下操作：

```bash
mkdir /tmp/jpcache
chmod 0777 /tmp/jpcache
```

最后，使用以下 PHP 脚本测试缓存系统，使用将 JPCache 文件夹放置位置的路径：

```php
<?php
require '/path/to/jpcache.php';
echo time();
phpinfo();
?>
```

注意页面顶部的 UNIX 时间戳。每次重新加载页面时，它都应该保持不变——JPCache 正在提供缓存版本，而不是每次都重新处理脚本。

### 配置 JPCache

除了前面提到的三个配置选项外，您还有十四个额外的配置变量可以修改以满足您的需求。完整的配置选项列表如下：

| 配置选项 | 默认值 | 描述 |
| :--- | :--- | :--- |
| `$JPCACHE_TYPE` | 无——使用 JPCache 前*必须*设置此变量。 | 要告诉 JPCache 使用基于文件或数据库的存储来存储缓存数据，请使用 `$JPCACHE_TYPE`。值为 `file` 表示告诉 JPCache 使用磁盘存储，而值为 `mysql` 则使缓存数据存储在 MySQL 数据库中。 |
| `$JPCACHE_TIME` | 900 | 使用数值定义，此变量告诉 JPCache 在缓存中保留页面多长时间（以秒为单位）。负值完全禁用页面缓存，而值 0 告诉 JPCache 无限期保留页面缓存。 |
| `$JPCACHE_DEBUG` | 0 (关闭) | 使用 0 表示关闭，1 表示开启，`$JPCACHE_DEBUG` 控制是否启用调试。 |
| `$JPCACHE_IGNORE_DOMAIN` | 1 (忽略域名) | 如果 Web 服务器仅提供一组内容，您可以将此值设为 1 (开启)，使 JPCache 忽略文件名中的任何域名前缀。当关闭时，JPCache 搜索缓存中与完整 URL 匹配的文件，包括域名。 |
| `$JPCACHE_ON` | 1 (启用) | 此变量简单地控制 JPCache 是否启用。 |
| `$JPCACHE_USE_GZIP` | 1 (开启) | 要启用 GZIP 输出压缩，类似于 Apache 的 `mod_deflate` 或 PHP 自身的 GZIP 输出缓冲，请将此值设为 1。请注意，由于 JPCache 最近版本中的一个 bug，使用 JPCache 的 GZIP 压缩时，在某些浏览器中输出可能会损坏。如果您的脚本在此功能启用时返回乱码或缺失内容，请尝试禁用此设置，看看情况是否得到修正。 |
| `$JPCACHE_POST` | 0 (禁用) | 此变量控制 JPCache 中的 HTTP POST 缓存。设为 0 以禁用，1 以启用。 |
| `$JPCACHE_GC` | 1 | 要控制 JPCache 垃圾回收例程的激进程度，您可以为 `$JPCACHE_GC` 分配数值。取值范围为 0 到 100，表示对缓存项目发生垃圾回收的概率百分比。 |
| `$JPCACHE_GZIP_LEVEL` | 9 (最大压缩) | 当使用 JPCache 内置的 GZIP 输出压缩时，您可以使用此变量来控制输出流的压缩级别。取值范围从 9（意味着高压缩和较小的输出大小）到 1（意味着较低压缩和较大的传输大小）。 |
| `$JPCACHE_CLEANKEYS` | 1 (哈希存储键) | 当 JPCache 创建脚本输出的缓存副本时，它使用每个脚本的唯一键将输出存储在文件名或数据库记录中。默认情况下，JPCache 对标识符进行哈希处理，使其难以确定特定缓存条目的来源，例如 `fpc-b4c588a4868e02288029b86d061401a2`。如果需要，您可以告诉 JPCache 不对每个脚本的缓存标识符进行哈希处理，从而允许您轻松确定每个缓存脚本的身份。禁用哈希后，脚本标识符将更像 `_directory_file_name_extension_HTTMethod#n_n_`。 |



| `$JPCACHE_DIR` | `/tmp/jpcache` | JPCache 存储其基于文件的缓存数据的目录由这个变量设置。JPCache 存储缓存文件的位置需要由 Apache 进程用户可写。 |
| `$JPCACHE_FILEPREFIX` | `jpc-` | 当 JPCache 在磁盘缓存中创建缓存文件时，它可以使用在此指定的文件名前缀，以避免与现有文件冲突。 |
| `$JPCACHE_DB_HOST` | `localhost` | 当使用数据库作为缓存存储位置时，您需要为 JPCache 设置用于连接和使用数据库的变量。此变量设置 JPCache 将连接的数据库主机。 |
| `$JPCACHE_DB_DATABASE` | `jpache` | 此变量设置存储缓存数据的 MySQL 数据库的名称。 |
| `$JPCACHE_DB_USERNAME` | `sqluser` | 要设置存储数据库中的缓存信息时使用的用户名，请设置 `$JPCACHE_DB_USERNAME`。 |
| `$JPCACHE_DB_PASSWORD` | `passwd` | 与 `$JPCACHE_DB_USERNAME` 配合使用，此变量设置数据库连接密码。 |
| `$JPCACHE_DB_TABLE` | `CACHEDATA` | JPCache 缓存数据存储在 `$JPCACHE_DB_TABLE` 指定的表中。要创建表，您可以在 MySQL Monitor 或您首选的 MySQL 管理工具中执行以下命令： `CREATE TABLE CACHEDATA ( CACHEKEY varchar (255) NOT NULL, CACHEEXPIRATION int(11) NOT NULL, GZDATA blob, DATASIZE int (11), DATACRC int (11), PRIMARY KEY (CACHEKEY) )` 当然，您需要更改数据库表的名称以匹配您在 `$JPCACHE_DB_TABLE` 中指定的值，反之亦然。 |
| `$JPCACHE_OPTIMIZE` | 1 (执行 OPTIMIZE TABLE) | 垃圾回收周期完成后，您可以指示 JPCache 对 `$JPCACHE_DB_TABLE` 中指定的表执行自动的 MySQL OPTIMIZE TABLE 命令。 |

### 移除 JPCache

要移除 JPCache，您需要搜索所有 PHP 脚本并删除任何对 `jpcache.php` 文件的 `include` 或 `require` 引用。删除引用后，您可以安全地删除 JPCache 目录。

有关 JPCache 的更多信息，请访问 `http://www.jpcache.com`。

## memcached

与 APC、e_Accelerator 和 JPCache 提供的输出缓存系统不同，memcached 系统依赖于后端对象的缓存来提供速度提升。memcached 是由 Danga Interactive（负责 LiveJournal.com 的团队）创建的一个分布式内存对象缓存系统。memcached 不缓存页面输出或编译后的 PHP 操作码，而是缓存各种代码对象，最重要的是数据库结果对象和数据模型实体。

这种缓存解决方案与本章节中的其他系统略有不同——memcached 实际上需要始终运行其自身的守护进程。然后，PHP 可以使用其 memcached 函数集来访问和使用内存对象缓存。

### 安装 memcached

要安装 memcached，首先从 `http://www.danga.com/memcached/` 获取守护进程源代码的副本。

然后解压缩 tar/gzip 归档文件，并更改目录到新创建的文件夹：

```bash
tar -xvzf memcached-1.1.12.tar.gz
cd memcached-1.1.12
```

接下来配置和构建源代码。如果 configure 报告任何缺失的库（例如 libevent），请根据各自的说明下载并安装它们；然后重新运行 configure 脚本，再构建 memcached。

```bash
./configure
make
```

然后，以 root 身份安装 memcache 守护进程：

```bash
make install
```

最后您需要做的是实际启动守护进程。以下命令使用 128MB 内存启动守护进程，在 IP 127.0.0.1 上监听端口 11211：

```bash
/usr/local/bin/memcached -d -m 128 -l 127.0.0.1 -p 11211
```

## 缓存引擎

如果你决定永久使用 memcached，请确保将启动 memcached 的命令添加到你偏好的启动设施或脚本中，以便机器每次启动时都能自动加载。

现在，既然 memcached 守护进程已经运行，你需要准备 PHP 以使用该缓存系统。请从 `http://pecl.php.net/package/memcache` 下载 memcached PECL 模块。

解压归档文件并进入新目录：

```
tar -xzvf memcache-1.4.tgz
cd memcache-1.4
```

运行 `phpize`，然后配置并编译 DSO：

```
phpize
./configure
make
```

以 root 用户身份安装该模块：

```
make install
```

最后，将以下行添加到你的 php.ini 中，并重启 Apache：

```
extension="memcache.so"
```

### 使用 memcached

为了使用 memcached，你安装的 PHP DSO 为 Memcache 对象提供了以下方法：

- `Memcache::add`

  `bool Memcache::add ( string key, mixed var [, int flags [, int expire]] )`

  此方法将一个变量或对象添加到内存缓存中，由标记 `key` 标识。如果内存缓存中已经存在具有相同 `key` 的值，则返回 `FALSE`。如果你希望在将值放入内存缓存之前对其进行压缩，请提供 `MEMCACHE_COMPRESSED` 作为标志，否则可以省略或设置为 0。为 `expire` 提供的任何值都告诉 memcached 何时应该从缓存中移除该项。`expire` 的值为 0 表示该值应该被无限期缓存。

  只有变量和对象可以存储在内存缓存中，而资源不可以。

- `Memcache::close`

  `bool Memcache::close ( void )`

  此方法关闭与 memcached 服务器的任何非持久连接。如果在关闭连接时发生错误，则返回 `FALSE`。

- `Memcache::connect`

  `bool Memcache::connect ( string host [, int port [, int timeout]])`

  此方法创建并打开到运行在 host 上的 memcached 服务器的连接。port 参数指定 memcached 使用的 TCP 端口，默认为 11211，而 timeout 指定在尝试连接时等待多长时间才返回 FALSE。成功时返回 true，失败时返回 FALSE。

- `Memcache::decrement`

  `int Memcache::decrement ( string key [, int value])`

  当在内存缓存中存储简单数值时，你可以实际使用 decrement() 方法将通过 key 匹配的值减少指定的 value。如果未指定递减值，则缓存的值减少 1。此方法在失败时返回 FALSE，或在成功时返回该项的新值。

- `Memcache::delete`

  `bool Memcache::delete (string key [, int timeout])`

  此方法从内存缓存中删除由 key 标识的项。为 timeout 提供值会导致该项在指定的秒数后被删除。失败时返回 FALSE，成功时返回 TRUE。

- `Memcache::flush`

  `bool Memcache::flush ( void )`

  此方法告诉 memcached 立即设置缓存中所有项的过期时间。一旦调用此方法，缓存中的任何项都可以被新键覆盖，但在发生这种情况之前，内存不会被释放。此方法在成功时返回 TRUE，或在失败时返回 FALSE。

- `Memcache::get`

  `string Memcache::get ( string key )`

  `string Memcache::get ( array keys )`

  此方法检索存储在内存缓存中的项或各项，与给定的 key 或 key 数组匹配。根据提供的匹配 key 的数量，它在成功时返回字符串或数组，如果未找到匹配输入参数的 key，则返回 FALSE。

- `Memcache::getStats`

  `array Memcache::getStats ( void )`



此方法返回一个数组，其中包含有关内存缓存状态的各种信息，例如当前和总连接数、缓存项数量以及服务器运行时间。

- `Memcache::getVersion`

  `string Memcache::getVersion ( void )`

  此方法返回一个包含 memcached 服务器版本号的简单字符串，如果发生错误则返回 FALSE。

- `Memcache::increment`

  `int Memcache::increment ( string key [, int value] )`

  与 `decrement()` 方法类似，`increment()` 允许你轻松地在内存缓存中直接更改简单数值——在这种情况下，将存储的变量增加 `value`，如果没有提供值则增加 1。成功时返回新值，失败时返回 FALSE。

- `Memcache::pconnect`

  `bool Memcache::pconnect ( string host [, int port [, int timeout]] )`

  此方法创建并打开到 memcached 服务器的持久连接，类似于 MySQL 持久连接。参数与 `connect()` 相同：`host` 指定 memcached 服务器的主机名或 IP 地址，`port` 指定 memcached 的监听端口，而 `timeout` 指定连接超时时间。

- `Memcache::replace`

  `bool Memcache::replace ( string key, mixed var [, int flag [, int expire]] )`

  此方法在缓存对象中搜索与 `key` 匹配的项，如果找到，则用值 `var` 替换它。与 `add()` 和 `set()` 类似，`replace()` 可以提供标志以请求在存储值时进行压缩，并且还可以为新值提供可选的过期时间。此方法在成功时返回 TRUE，失败时返回 FALSE。

- `Memcache::set`

  `bool Memcache::set ( string key, mixed var [, int flag [, int expire]] )`

  此方法将值 `var` 存储在内存缓存中，即使存在与 `key` 匹配的预存项也是如此。参数与 `add()` 和 `replace()` 的相同。成功时返回 TRUE，失败时返回 FALSE。

你可以以类似 MySQLi 方法的方式使用这些方法——你连接到 memcached 服务器，处理进出缓存的数据，然后断开连接。以下简单示例将 `Circle` 对象存储在内存缓存中：

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

$memc->set('circel', $c);

$stats = $memc->getStats();

$memc->close();

print_r($stats);
?>
```

如果你运行此脚本，它将输出一个数组，其中包含当时内存缓存的统计信息。如果你是第一次运行该脚本，或者第一次在服务器上 memcached 被使用，你的 `curr_items` 值应为 1，反映了新添加的 `Circle` 对象。

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

与其他 DSO 缓存解决方案一样，你可以通过注释掉或从 `php.ini` 中删除相应的行并重启 Apache 来快速禁用 memcache 功能。此时，你可以从 PHP 扩展目录中删除 `memcache.so`，并从系统二进制文件夹（之前安装的位置，通常是 `/usr/local/bin` 或 `/usr/bin`）中删除 memcached 守护进程。

## 同时使用不同的缓存引擎

此时，你脑海中可能正在运转着齿轮，开始好奇：“如果我同时使用多个缓存引擎会发生什么？”嗯，正如你可能猜测的那样，正确选择互补的解决方案可以略微提高性能，但有些组合对你没有好处。

`JPCache` 和 `memcached` 可以与其他模块很好地共存，但 `APC`、`eAccelerator` 和 `Zend Optimizer` 在某种程度上是互斥的。虽然它们可能都能正常加载，并且在执行 PHP 脚本时不会抛出任何错误，但没有多少理由（甚至没有理由）使用操作码缓存的组合。这三者在某种方式或另一种方式上提供大致相同的功能，因此使用多个操作码缓存只会导致系统速度最慢的缓存决定整体速度。

尽量只选择一种操作码缓存解决方案，并尝试将其与 `memcached` 和 `JPCache` 结合使用。加入你偏好的内容压缩解决方案——`JPCache` 内置的内容压缩仍然有太多的 bug——你就得到了一台精干且强大的组合缓存服务机器。

## 选择你的缓存引擎

那么，哪种缓存解决方案最适合你？也许最好先评估你系统的需求，并寻找当前或即将成为瓶颈的地方。如果你正在处理在脚本中快速飞进飞出的重量级类和对象，或者频繁地从数据库中提取大量重复数据，`memcached` 将是你在某些性能提升方面的最佳选择。如果你的网站代码生成相对静态的页面——你没有使用过度的用户个性化或其他高度动态元素——你应该考虑使用 `JPCache`。如果数据层不是真正的瓶颈，但你的 PHP 代码可能需要一些通用的性能调整，那么其中一种操作码缓存引擎将帮助你。如果你不确定使用哪种优化器/缓存，`APC` 是一个安全的赌注。它可能缺乏低级引擎的加速或 `Zend Optimizer` 可能提供的优化，但它通过高度可定制性得到了弥补，并且支持良好——毕竟它是 PECL 仓库的一部分。

## 摘要

无论你选择哪种缓存解决方案，本章讨论的任何系统都有潜力显著提高你的 LAMP 配置的性能。通过适当的关注和配置，你的缓存解决方案将允许你同时服务更多的用户，并帮助你防范某天可能遇到的任何 DOS / Slashdot 效应。

## 13 内容管理系统

内容管理系统（CMS）帮助软件或 Web 开发者组织和促进任何协作过程及其最终成果。“内容管理”一词松散地指代不仅包括文件的检入和检出，还包括信息的通用共享，例如公共日历、维基等。最早的内容管理系统出现在 1975 年左右，当时大型机和电子出版的需求真正开始普及。这些最早的版本基本上只是通用的存储库，允许多个用户参与同一项目。

随着计算机系统变得越来越复杂，有效管理内容的需求也变得日益复杂。随着互联网的成熟，CMS 的浪潮也随之而来。现在的 CMS 数量多到让你数不过来（意指数量极多）。本章的目标是试图拨开迷雾，帮助你确定是否需要 CMS，哪种类型的 CMS 适合你的项目，以及如何使用 CMS 来提高效率。

## CMS 的类型

CMS 形态各异，基本上可以管理由个人团队工作的任何内容。从管理简单的静态网站内容，到允许在互联网上进行协作文档编写（维基），CMS 执行许多功能。CMS 软件包通常可以分为两大类：企业级 CMS 和 Web CMS。

### 企业级 CMS

这些功能强大的软件包通常是综合解决方案，为企业或公司层面提供有效的内容管理。它们旨在帮助公司提高效率、降低成本、增加准确性和功能性，同时减少人为错误和缩短客户响应时间。

它们可以集成企业功能，如运输和交付系统、开票、员工和人力资源问题、客户关系管理、文档管理和事务（销售）系统。企业级 CMS 将数据管理降低到用户级别，使得许多用户可以在一个非常大的集成整体中添加他们自己的一小部分。部署这些复杂系统的软件公司自豪地提供高度定制的全公司解决方案，软件通常附带相对高昂的价格标签。

### Web CMS/门户



Web CMS 软件包主要是为在网络上使用而创建的。它们可以集成多种功能，或者围绕一个特定的核心功能。它们允许用户更新公共网站的某些部分，或在网站“社区”中进行协作。Web CMS 通过快速轻松地为用户提供功能，使开发者的生活更轻松，并允许首席开发者放心地将其他人纳入网站开发和维护，而不必担心偏离标准。本章将重点关注开源 Web CMS 软件包，特别是 `PHP/MySQL` 软件包。

Web CMS 类别的一个子集是群件。这种类型的软件包运行在内联网或互联网上，旨在允许用户之间进行协作，通常是为同一家公司工作，从事相同项目。它们通常提供项目管理、文件检入和检出、日历系统、电子邮件和内部论坛等功能。

## 开源 Web CMS 软件包

Web CMS 的常见功能包括：
- **静态网页更新**：在不改变网站外观和感觉的情况下更新内容。
- **网络日志（博客）**：在线日记。
- **维基**：协作文档项目。
- **出版物**：新闻文章的发布和组织。
- **托管学习环境**：基于 Web 的学习。
- **事务性 CMS**：电子商务功能。
- **图像和文件库**：供公开使用的图像或文件汇编。
- **论坛**：促进用户之间讨论的公告板系统。
- **聊天室**：用户之间的实时聊天。
- **RSS 源**：允许用户下载内容。
- **投票**：允许用户对某个主题进行投票。
- **日历系统**：基于 Web 的多用户日历。

还有其他许多功能可以视为属于 CMS 范畴，但这些是主要功能，也是本章关注的重点。

首先，请查看一些更全面的开源 CMS 软件包。

### 全包式 Web CMS

就像豪华的热带度假村将你的假期打包成一个整洁的一站式套餐一样，这些综合性的 Web CMS 可以做得很少或很多，随你喜好。以下部分将介绍一些可用的更流行的软件包，虽然像 `http://www.sourceforge.net` 这样的网站上有大量此类软件包。本文不详细介绍这些软件包的安装过程，因为你在这方面可能已经有一些经验。然而，如果安装有任何特殊注意事项，将会如实说明。此外，在安装这些软件包之前，你需要确保 `LAMP` 系统的所有方面都正常工作。

大多数全包式 Web CMS 都具有共同的功能，如更改用户权限、修改站点布局、更改服务器设置等。值得一提的是，许多所谓的综合性 CMS 软件包缺乏事务性 CMS 接口，用于电子商务的购物车。

### ExponentCMS

`ExponentCMS` 可以在 `http://www.exponentcms.org` 上找到。截至本文写作时，最新版本是 `0.96.3`，本节基于此版本。在 `http://sourceforge.net/projects/exponent/` 的 Exponent/Sourceforge 界面上，你可以找到截图、文档、贡献以及标准的 Sourceforge 信息的链接。

#### 安装说明

安装相对简单，安装前你唯一需要知道的是你需要创建一个数据库。这适用于远程和本地安装。你还需要设置一个用户名和密码，因为在安装过程中会被要求提供这些信息。

#### 一般概述/默认安装

安装此 CMS 后，你会获得几个默认“激活”的功能。它们是：
- **地址簿**：组织联系人信息。
- **管理控制面板**：易于使用的界面，用于管理网站。
- **日历系统**：以不同视图跟踪事件。
- **联系表单**：允许访问者联系你。
- **图像管理器**：与其他模块配合管理网站上的图像。
- **预览链接**：让在网站上工作的人员预览他们的工作。
- **私人消息中心**：允许用户相互发送邮件或私人消息。
- **资源管理器**：组织和显示上传的文件。
- **文本模块**：显示文本并跟踪修订版本。
- **网络日志/在线日记管理器**：组织博客条目。

“未激活”的功能，你可以简单开启的功能是：
- **横幅管理器**：管理横幅广告活动和点击跳转。
- **内容轮换器**：每次用户访问网站时显示不同的图像或文本。
- **Flash 动画管理器**：组织 Flash 动画。
- **表单模块**：管理网站上的任何表单。
- **HTML 模板管理器**：管理上传的 HTML 模板。
- **登录模块**：允许用户登录网站。
- **多站点管理器**：允许你创建和管理其他网站。
- **导航器**：管理导航系统。
- **新闻源系统**：组织和显示新闻文章。
- **搜索**：允许用户搜索网站。
- **UI 切换器**：赋予具有正确权限的用户从用户切换到管理员的能力。

通过易于使用的管理模块管理器，你可以一键激活或禁用这些模块中的任何一个。

其他模块可以从 `http://www.sourceforge.net` 下载。使用扩展上传管理器，安装模块很容易；你甚至不需要解压它们。这些扩展包括：
- **文章管理器**：组织和显示网站上的文章。
- **公告板**：管理网站论坛。
- **FAQ**：管理网站的常见问题解答部分。
- **图像库**：允许用户排序和查看图像。
- **列表管理器**：组织和管理工作列表，如房地产列表。
- **页面显示器**：允许你上传并显示动态生成的页面，如 `PHP`。
- **幻灯片**：管理网站上的幻灯片播放。

除了安装、激活和禁用网站模块外，作为网站管理员，你可以通过管理界面导入数据，如 `CSV` 格式的用户列表。这使你能够轻松地从其他系统或内部数据库进行转换。

该软件还嵌入了所见即所得 `WYSIWYG` `HTMLArea` 编辑器，使你的作者和贡献者更容易添加文本。作为管理员，你还可以控制 `HTMLArea` 工具栏，从而决定用户拥有哪些文本选项。

#### 自定义默认设置

与大多数其他 CMS 软件包一样，你可以在管理控制面板中更改用户设置。在 `Exponent CMS` 中，你可以基于用户和内容设置审批策略，尽管此 CMS 侧重于模块而非用户。例如，你可以为日历模块创建审批策略，但前提是需要其他管理员至少两次批准，之后才会显示所请求的更改。虽然你可以将某个模块的权限分配给用户或群组，但这需要通过每个特定模块进行，而不是通过用户界面。不存在多种级别的用户访问权限——用户要么是管理员，要么不是。此外，虽然你可以查看哪些用户拥有哪些模块的权限，但你无法看到单个用户负责的所有模块。

此外，`Exponent CMS` 允许你通过管理界面中的 `Configure Site` 区域对设置进行一定控制。

#### 数据库设置

你可以在 `MySQL` 和 `PostgreSQL` 之间切换，当然也可以修改数据库名称、用户名、密码、端口以及任何表前缀名称。

#### 显示设置/主题

站点预装了若干主题，但通过编辑相应文件，或从头创建自己的主题，创建自己的主题也相当容易。除非你特别喜欢重新发明轮子，否则我们的建议是选择一个最接近你期望布局的主题，并在此基础上进行编辑。在每个示例主题的底部，在 `Manage Themes` 页面下都有一个链接，允许你查看该主题的完整文件列表，这使你能够轻松地看到需要修改哪些文件以适应你的需求。

在此部分中，你还可以更改对其他网站贡献者的引用方式，以及向网站访客显示日期和时间的方式。

#### 通用配置设置

在此部分下，你可以自定义页面标题、元标签和关键词，以及语言选择。你还可以开启/关闭用户注册，启用 `CAPTCHA` 计算机自动化公共图灵测试，用于区分计算机和人类，以防止机器人注册，并控制会话超时和 `SSL` 设置。

#### SMTP 设置

这是设置你的 `SMTP` 端口、用户名、密码、认证方法等的地方。如果你愿意，也可以在此切换到 `php_mail()` 函数。

#### 其他扩展

除了激活/停用预装模块以及安装提供的新模块外，大众还提供了一份相当庞大的其他贡献列表。这可以通过 `Exponent` 的 Sourceforge 接口网站 `http://www.sourceforge.net` 获取，位于 `Tracker > Contributions` 部分。它包括一些非常实用的扩展，例如添加水平下拉导航，因此请务必查看一下。

#### 更改模块的布局和外观

虽然使用 `ExponentCMS` 添加和删除模块非常容易，但在页面上移动它们甚至更容易。然而，让模块彼此外观不同却颇具挑战性。

#### 优点和缺点

该包的优势在于：
- 更改模块的布局和位置证明是一项容易的任务，且具有所见即所得 `WYSIWYG` 的特性。此外，你可以打破传统的两列或三列布局，并为所有三个传统列添加子列。
- 文本模块会跟踪修订版本，并允许你立即一键查看或恢复旧版本。如果能显示*谁*做了修订就更好了，也许该功能会在未来版本中提供。
- 预览功能让你可以看到更改对站点外观的影响，而无需注销管理员身份。
- 主题比起某些其他 CMS 中以功能为导向的方式，更偏晦涩和以设计为导向。

一个缺点是用户管理——管理员无法看到个别用户拥有的所有权限或模块职责。例如，如果 Bob 要去度假，你想把 Bob 的模块分配给别人，但没有简单的方法来查看 Bob 有什么能力以及他可以修改哪些模块。



CMS 出现在 Sourceforge“最活跃”下载排行榜前 10 是有原因的。ExponentCMS 是*远远*最容易管理的开源 CMS。然而，其优势更多体现在幕后，因为其重点不一定在于与大量访问站点的用户进行互动，而在于管理员可以控制的核心贡献者群体。如果你在寻找一个外观漂亮的“开箱即用”站点，ExponentCMS 应该在你的评估列表中。

### XOOPS

XOOPS（可扩展面向对象的门户网站系统）是另一个流行的综合性 CMS，可在 Sourceforge 或 `http://www.xoops.org` 上获取。最新版本是 2.1.1，这里讨论的就是该版本（这实际上是版本 2.2 的预发布版，请牢记这一点）。

#### 安装说明

XOOPS 团队编写了一份非常综合的安装指南，不仅指导你完成安装和设置过程，还向开发者提供了关于文件将放置在何处以及原因的详细信息。你应该阅读这份文档——你可以在 `http://docs.xoops.org/modules/xdocman/index.php?doc=xu-002&lang=en` 找到它。

在安装前需要指出的几点：

- 解压缩 tar 文件后，你需要将 html 文件夹复制到网站根目录（如 `htdocs` 或 `public_html`）。XOOPS 团队建议你将该文件夹重命名为 `xoops`，但这完全取决于你。
- 如果你在远程服务器上安装，需要在安装之前创建数据库、用户和密码。如果你在本地安装，安装向导将为你完成此任务。
- 解压缩文件后，你需要对以下目录和文件执行 `chmod` 操作，使它们可写：
  - `uploads/`
  - `cache/`
  - `templates_c/`
  - `mainfile.php`
- 为了 XOOPS 安装向导正确完成过程，你的浏览器必须启用 cookies 和 javascript。

#### 总体概览/默认安装

有几个功能默认是激活的：

- **横幅管理**：管理横幅广告和点击跳转。
- **图像管理器**：管理图像以及谁可以上传它们。
- **表情符号**：管理“表情符号”及其显示方式。
- **头像**：管理头像。
- **评论管理器**：管理用户发布的评论。
- **用户管理**：编辑、发送电子邮件、搜索用户、更改用户等级。
- **块**：管理块（如“谁在线”和“最新评论”）。

默认安装的唯一模块是系统管理模块。包中默认可用的其他模块（但需要逐一安装）包括：

- **联系我们**：向网站管理员发送消息。
- **下载**：组织上传的文件，并允许用户对其排名。
- **链接**：链接管理器。
- **论坛**：站点论坛（由 phpBB 组创建）。
- **新闻**：管理用户提交的文章。
- **版块**：允许管理员发布站点的不同版块。
- **常见问题**：管理站点的常见问题。
- **头条**：来自其他网站的新闻 RSS 源。
- **成员列表**：显示站点的注册用户。
- **合作伙伴**：组织和展示合作伙伴站点。
- **投票**：管理在线调查和投票。

#### 自定义默认安装

截至本文撰写时，XOOPS 网站上提供超过 300 个附加模块可供下载。有一个模块几乎可以实现你想要的任何功能，包括交易功能（购物车），这在同类 CMS 中并不常见。

在管理控制面板的系统管理部分，你将找到以下可以进一步自定义你安装的区域：

- **头像**：允许你为用户上传可用的头像。
- **横幅**：管理你的横幅广告，并提供点击率统计和哪些横幅是活动的信息。
- **块**：提供用于添加新块并确定其在站点上布局的接口。
- **评论**：允许你查看、编辑和删除评论。
- **查找用户**：不允许自定义站点，但提供用于筛选用户的广泛搜索接口。
- **群组**：这是你将用户分配到不同群组并设置该群组权限的地方。权限在系统、模块和块级别，并允许授予管理员或访问权限。
- **图像管理器**：管理图像图库。
- **邮件用户**：不允许自定义站点，但允许你向用户发送电子邮件。
- **模块**：允许你安装并激活或停用可用模块。
- **偏好设置**：提供站点的一般自定义，并细分为几个类别：
  - **通用设置**：允许你更改站点名称、标语、管理员电子邮件地址、默认语言、起始页面的模块、服务器和默认时区、默认主题（只为你安装了三个）、用户主题、匿名用户的用户名、gzip 压缩、cookie 和会话信息、站点是否完全关闭、站点关闭时的自定义消息、IP 地址、SSL 设置、被禁用的 IP 地址以及配置缓存设置。
  - **用户信息设置**：允许你设置密码和用户名设置、用户所属的默认群组、头像设置、被阻止的用户名（如“admin”），并修改注册免责声明。
- **元标签和页脚**：允许你设置元标签信息，如关键词、描述、robots、评级、作者、版权，以及页脚信息。
- **屏蔽词语选项**：允许你屏蔽不需要的词并将它们替换为你选择的词。
- **搜索选项**：允许你开启或关闭全局搜索设置，并要求用户驱动搜索的最小关键词长度。
- **邮件设置**：允许你配置邮件服务器设置和邮件方法。

#### 表情符号

控制论坛的表情符号，并允许您创建自己的表情符号。

#### 模板

允许您向网站上传模板。

#### 用户等级

控制论坛的用户等级系统，并允许您配置您在特定级别定义的最小帖子数。

#### 编辑用户

使您可以删除用户并编辑他们的信息——昵称、姓名、电子邮件、网址、时区、即时消息信息、位置、职业、兴趣、签名、评论能力、通知、等级、密码和组。

#### 优势与劣势

该套件的最佳部分包括：

- 庞大的用户基础和支持论坛使开发人员能够轻松找到问题的解决方案或排查有问题的区域。
- 文字审查选项是一个不错的福利。
- 由于论坛模块由 phpBB 组开发，论坛控制高度自定义且详细。

可以改进的地方包括：

- 虽然核心文档很全面，但附加模块的文档非常缺乏。由于附加功能可能构成网站的一大组成部分，这对于没有经验的人来说可能会令人沮丧。
- 默认安装只包含三个主题，鉴于如此庞大的支持和用户基础，理所当然地认为可以预装更多的主题。

XOOPS 因其潜力而流行，尽管您必须愿意解读他人的代码，并有奢侈的时间来微调您的安装以符合您的特定需求。虽然它作为一个“开箱即用”的解决方案并不出色，但如果您愿意并能够花一些时间编写代码，它可以完成您需要的几乎任何事情。它非常以用户为导向，允许您作为管理员控制用户的环境，甚至一直到“表情符号”。如果您专注于与任何访问您网站的人创建互动社区，您应该再次审视 XOOPS。

### phpWebsite

phpWebsite 可在 `http://phpwebsite.appstate.edu` 获取。撰写本文时 phpWebsite 的最新版本是 0.10.01，这也将是此处讨论的基础。

#### 安装说明

阿帕拉契州立大学（phpWebsite 的创建者）的友好人士已经设置了一个命令行安装过程，允许您直接从 phpWebsite 网站安装。您也可以分部分下载应用程序（核心、主题包等）并自行安装。

安装前需要注意以下几点：

- 您需要安装以下 PEAR 库才能运行核心应用程序：
  - `Benchmark`
  - `DB`
  - `Date`
  - `HTML_BBCodeParser`
  - `HTML_Common`
  - `HTML_Form`
  - `HTML_Table`
  - `HTML_Template_IT`
  - `Mail`
  - `Mail_Mime`
  - `Net_CheckIP`
- 如果可能，在安装前您需要以 root 身份登录。脚本将检测您是否不是 root 用户，并设置带有某些安全限制的应用程序。如果您尝试切换用户，它将保留原始设置，并且不会进行 root 安装。
- 您必须拥有 `wget`，否则安装程序将无法运行。

#### 总体概述/默认安装

立即可用并处于激活状态的模块有：

- **Apache 控制器**：允许管理员更改 Apache 设置。
- **帮助系统**：帮助管理员导航系统。
- **语言管理员**：管理网站上要使用的语言。
- **布局管理器**：管理网站的布局。
- **网站搜索**：搜索网站。
- **用户管理器**：批准用户进行网站的各种修改级别。
- **公告**：管理发布在网站上的公告。
- **区块制作器**：允许您创建和管理区块。
- **分支创建器**：管理在主站点下创建的衍生站点。
- **日历**：网站的日历。
- **评论管理器**：管理评论。
- **调试器**：协助管理员定位和修复错误。
- **文档**：文件管理器。
- **常见问题**：管理网站的常见问题解答。
- **链接管理器**：组织和显示链接。
- **菜单管理器**：管理动态菜单。
- **模块制作器**：允许您创建自己的模块。
- **笔记**：向网站用户发送电子邮件。
- **网页**：管理网站上的静态页面。
- **表单生成器**：创建表单。
- **照片集**：组织和管理在线图像库。
- **公告板**：管理论坛。
- **RSS 新闻源**：管理信息源。



- **投票**：管理在线调查和投票。
- **骨架模块**：用作模板的示例模块。
- **管理员统计**：跟踪哪些模块和用户最活跃。

### 自定义默认安装

与所有 CMS 套件一样，其魅力在于修改默认安装以真正符合您的需求。

添加、删除和编辑用户及其权限可以在**用户管理**部分的**管理控制面板**下完成。在此，您可以设置是否允许用户注册，以及他们是否需要在参与论坛等活动之前得到批准。您还可以创建自己的身份验证脚本或使用本地数据库来验证用户。如果用户被授予管理员状态，您可以控制他或她有权访问哪些模块，以及该模块内可以执行哪些特定功能。例如，用户可以创建投票，但不能编辑、删除或列出投票。

更改模块的布局是可能的，但不像 phpWebsite 的其他一些功能那样容易操作。您可以更改每个特定模块的外观，这是一个不错的功能。

HTML 头部信息（meta 标签、关键字等）在**布局管理**部分的**管理控制面板**下控制。这是有些出乎意料的。

目前共有 21 个其他主题可供您在 `http://www.sourceforge.net` 上下载和使用。

### 优势与劣势

该套件最具吸引力的特性包括：

- 管理员可以获得大量的统计信息，这使得微调网站更容易。
- 能够创建自己的授权脚本是一个不错的特性。
- 管理员可以单独更改框和模块的外观，因此同一页面上的所有框不必看起来相同。
- 允许非常详细的用户权限，使得查看谁被允许做什么变得简单明了。
- 默认模块广泛，使开发人员构建综合性网站的工作量更少。

唯一的缺点是，目前系统不允许打破传统的两列或三列布局。

phpWebsite 是一个不错的“中间道路”CMS，平衡了高水平的内置功能和高度的用户交互性。如果您正在寻找一个可以支持中等规模贡献者群体，同时促进访客交互性的套件，那么这可能就是适合您的 CMS。

## TikiWiki

该软件可在 `http://www.tikiwiki.org` 获取，撰写本文时可用的当前版本是 1.9.0。

### 安装说明

如果您使用的是旧版本的 PHP（早于 4.3）或 MySQL（早于 4.0.1），那么您希望特别关注“要求和设置”文档，该文档可在 `http://doc.tikiwiki.org/tiki-index.php?page=requirements+and+setup` 找到。其他需要注意的要点是：

- PDF 生成模块需要安装 `php-xml` 包。
- 由于使用了会话，请确保您的 `php.ini` 文件具有以下设置：

```
session.save_handler = files
session.save_path = /tmp (for local installation)
```

在安装之前，您还需要创建数据库以及用户/密码。安装包可以从网站下载，或者如果您正在安装到远程服务器，安装页面上有一个单独的链接，名为 `InstallWithOnlyFTPAccess`，这是适合您的正确方法。

### 默认安装

有几个功能是默认激活的：

- 游戏：允许用户在您的网站上玩游戏并跟踪游戏统计信息。
- 类别：管理任何模块都可以归入的类别。
- 日历：允许用户查看带有事件的日历。
- MyTiki：为登录的用户提供他们自己的界面，具有日历、网络邮件、菜单和记事本等功能，并允许管理员开启或关闭用户功能。
- 提交：允许用户提交文章。
- 自动链接：允许输入到文本中的 URL 自动提交到链接目录。
- 搜索与全文搜索：允许用户搜索您的网站。
- HTML 页面：管理可重用的 HTML 代码块，以在整个网站中重复使用。

## 第 13 章

### TikiWiki 功能

- **帮助系统**：管理帮助中心。
- **Galaxia 工作流引擎**：允许管理复杂的工作流过程。
- **Wiki**：协作文档系统；同时允许授权用户创建和编辑静态 HTML 页面的内容，并提供所见即所得（WYSIWYG）HTML 编辑器和拼写检查器等高级功能。
- **文章**：组织和管理文章。
- **博客**：网络日志管理。
- **目录**：对链接进行分类的链接管理器。
- **文件库**：组织和管理上传的文件。
- **常见问题解答**：管理站点的常见问题解答（FAQ）。
- **地图**：允许显示交互式地图。
- **追踪器**：为你管理和组织自定义数据。
- **热词**：允许你从站点上的特定单词嵌入链接。
- **联系我们**：一个便于用户与你联系的简易表单。
- **统计**：管理站点统计信息，尽可能涵盖所有活跃模块。
- **引用站点统计**：管理来自引用站点的统计信息。
- **调试控制台**：协助开发人员调试站点。

其他预安装但只需单击按钮即可激活的功能包括：

- **评论**：允许用户评论站点上的图像、文章和其他内容。
- **图像库**：允许用户排名、查看和上传图像。
- **新闻阅读器**：新闻的 RSS 源。
- **投票**：管理在线投票。
- **测验**：允许用户参加测验并得到评分。
- **特色链接**：管理在你的 Tiki 站点内打开的链接；跟踪链接统计信息。
- **横幅**：管理横幅广告活动和点击次数。
- **通讯**：管理站点的通讯广播，并允许用户订阅。
- **论坛**：管理论坛。
- **喊话框**：允许用户在动态窗口中显示简短的文本行。
- **调查**：管理在线调查。
- **历法**：允许你显示根据每年每一天定制的图像和文本。
- **在线支持系统**：允许用户向在线帮助中心请求帮助。
- **Babelish 翻译**：允许用户翻译站点的一部分。
- **集成器**：允许你将外部 HTML 页面导入站点。
- **封禁系统**：允许你轻松封禁用户。
- **用户功能**：允许用户书签、跟踪文件、向其他用户发送消息以及执行其他操作。

### 自定义默认安装

站点的管理部分有几个用于提供自定义功能的子部分。它们是：

- **功能**：在此部分中，管理员可以激活和停用功能，并更改站点的一般布局。
- **通用偏好设置**：在这里，你可以更改主题，更改主页或创建自定义主页，设置语言偏好，设置操作系统类型，更改 PHP 错误报告级别，设置站点停机时的自定义消息，限制站点用户数量和负载，设置缓存偏好，设置新链接的打开方式，控制所有组是否查看所有模块，设置是否将管理员页面浏览量计入统计，更改菜单显示，设置服务器配置，设置会话偏好，管理日期/时间格式，并更改管理员密码。
- **用户注册和登录**：此区域专门用于让你控制用户注册和登录过程的方方面面，从身份验证到密码要求，到 HTTP/S 设置，甚至包括 TikiWiki 使用的 `PEAR::Auth` 模块的设置。
- **已启用功能的配置（例如，Wiki）**：对于你通过“功能”屏幕启用的各种功能，你将能够访问这些独立部分以进一步自定义其设置。由于 Wiki 是早期项目的重点，站点管理部分的此区域提供了大量的控制、可定制性和功能。简而言之，你可以转储、恢复和附加文件，控制数据库和评论设置，导出，配置链接格式并设置为 Wiki 文档保留哪些信息（版本控制、用户数据、日期、链接、状态等）。你还可以管理版权保护、Wiki 历史记录并配置监视。你可以开启或关闭的一些 Wiki 功能包括：

  - 邮件输入
  - 沙盒
  - 最后更改
  - 历史记录
  - 排名
  - 撤销
  - 多重打印
  - PDF 生成
  - 评论
  - 拼写检查器
  - 编辑冲突警告
  - 独立缓存
  - 脚注
  - 使用 `WikiWords`
  - 自动等宽文本

其他可用功能（文章、博客、图像库等）也允许一定程度的自定义，但远不如 Wiki 部分那样详细。

### 优点和缺点

TikiWiki 的优点包括：

- 文档和支持社区非常广泛，就像许多其他开源 CMS 软件包一样。
- 强大的 Wiki 自定义使在线协作变得容易。
- 默认安装附带 35 个主题，它们是基本的 CSS 文件，使进一步的自定义变得容易。
- 尽可能为每个活跃模块提供广泛的统计信息。
- 这个 CMS 是最全面的之一；它几乎附带了所有可设想的模块（除了交易功能），使你可以轻松自定义，而无需安装额外的插件或附加组件。

对于缺点，**Galaxia 工作流** 有点复杂，需要单独阅读才能理解系统是如何设置的以及它如何为你工作。这也可以成为 TikiWiki 的一个优点，因为一旦你能够理清该系统，它可以为你提供一个管理复杂项目的非常全面的工具。

使用此软件，你可以快速提供用户希望拥有的任何内容。事实上，通过此软件可用的功能如此之多，业余网络开发人员可能会受诱惑使用太多模块，“因为他们可以这样做”。我们的建议是，如果你确切知道你想要在网站中实现什么，并且如果你有大量用户将参与实际站点内容的贡献，你绝对应该看看这个 CMS。

## 其他

还有许多其他可用的开源 CMS 软件包。一些值得一提的包括：

- **Mambo**：可在 `http://www.mamboerver.com` 获取。这是一个流行的 CMS，提供基本的预安装功能，拥有大量下载量。该项目培养了一个健康的支持系统，且用户基础相对容易管理，无需深入代码。



### Drupal
可在 `http://www.drupal.org` 获取。这是另一个流行的 CMS，侧重于功能而非形式。包含一些主题，但在不深入代码的情况下自定义是有限制的。一个不错的功能是“最近的系统事件”，当管理员登录时显示，允许管理员轻松查看其他人一直在做什么。

### PHP-Nuke
可在 `http://www.phpnuke.org` 获取。这是最古老的基于 PHP/MySQL 的 CMS 之一。它自 2000 年以来一直存在，拥有如果不算最大的，也是最庞大的 CMS 支持社区之一。它目前仍在开发中，但坏消息是它不再免费——你现在需要支付最低费用才能下载最新版本。如果你希望成为 PHPNuke 精英的一员，你也可以加入 PHPNuke 俱乐部（需支付另一笔费用）。

### Postnukle
可在 `http://www.postnukle.com` 获取。这也是“老古董但好用”的产品之一，这个 CMS 在 PHP-Nuke 之后不久推出，因此得益于其庞大的用户和开发人员社区。有许多插件、语言包和用户论坛可供协助你自定义这个 CMS 软件包。

## 微型 CMS

你可能只想要更大 CMS 软件包中的某一项功能在你的自己的站点上。幸运的是，你也有可用的微型 CMS 软件包。这些“迷你”CMS 软件包具有一个特定目的，例如博客或 wiki。如果你只需要站点上的一个功能，它们是完美的解决方案。以下章节简要介绍了这些软件包。

最流行的两个微型 CMS 软件包是博客和 wiki。这就是为什么更多地关注这些领域的原因。

### 博客的魔力

研究表明，博客及其读者的 popularity 正在增加。PEW Internet & American Life Project 的一项研究表明，在 2002 年，只有 3% 的互联网用户拥有博客。在 2003 年，这一数字增加到 5%，而在 2004 年，这一数字上升到 7%。将这个数字乘以仅在美国估计的 1.2 亿互联网用户，这意味着有相当多的博客活动在进行中。

不仅人们在写博客，而且越来越多的人花时间阅读它们。Hostway, Inc. 在 2005 年 4 月的一项调查显示，大约 30% 的受访受访者阅读过博客，分析师预测未来几年这一数字将大幅增长。

### 为什么要写博客？

写博客有很多原因，它们涵盖从个人到政治到公司议程的方方面面。这种免费、即时、互动的沟通机制是分享观点和想法的完美论坛。博客可以是关于任何事情的，其非正式的性质几乎吸引每个人。

博客的存在是为了：
- **分享政治观点**：许多政治家和知名政治活动家正在使用博客来接触大众并推广他们自己的议程。
- **进一步实现企业目标**：企业开始跟进这一趋势，提供关于其产品和服务的博客。一些是由消费者自己撰写的。一些企业使用博客来通知其忠实的读者即将推出的产品发布，或公司的其他新闻。
- **分享个人观点**：在这个拥挤的星球上，在这个拥挤的互联网上，有时人们只是希望被听到。也许他们想与全球各地的朋友和家人分享他们当前的经历。或者也许他们有想要与初学者分享的专家建议。在编码者的世界中，你可能有一个想要分享的代码片段，或者一个你想告诉别人的酷炫产品或链接。列表还在继续。

## WordPress

WordPress 是一个出色的“开箱即用”博客软件包，提供了极佳的自定义性和功能性。它可以在 `http://www.wordpress.org` 获取，撰写本文时的当前版本为 1.5.11。

### 安装说明

此软件包的安装极其简单快捷。安装前，请确保你正在运行 PHP 4.1+ 和 MySQL 3.23.23+，并且已创建好数据库以及用户名/密码。你所需的其他文档都方便地存放在 `http://www.wordpress.org` 网站上。

### 功能概览

WordPress 为您的博客提供了许多功能以及自定义领域，包括：
- **用户注册系统**：允许你授权其他用户在你的网站上发布、编辑和删除博客文章，拥有 10 个不同级别的用户访问权限。你还可以要求在草稿发布之前进行“审批”流程。
- **静态内容页面**：允许你向网站添加静态页面，并通过 WordPress 界面进行管理。
- **添加链接或博客滚雪球（blogrolls）**：你可以通过 WordPress 界面管理和组织外部链接。
- **主题**：默认安装目前内置了 35 个主题，另有近 150 个额外主题可供你下载，以轻松自定义博客的外观和感觉。
- **评论系统**：允许你接受、审核和修改用户发布的评论，并包含垃圾邮件拦截器以防止垃圾帖子弹出。访客还可以通过 Trackback 和 Pingback 在他们自己的网站上对你的博客发表评论。
- **隐藏帖子**：允许你对某些帖子设置密码保护，这些帖子只能由你或创建它们的作者查看。
- **数据导入**：允许你从其他流行的博客软件包（包括 MovableType、Blogger 等）导入数据。
- **RSS 源**：允许其他人联合分发你的博客。
- **电子邮件发布**：允许你通过电子邮件系统提交博客文章。

这个博客软件包还有其他不错的功能，如完全符合标准、升级简便，以及使用 Texturize 引擎美化从纯 ASCII 到丰富格式的文字。

### 总结

一旦深入研究 WordPress 软件包，你会发现它的文档完善、安装容易、配置和自定义简单，且功能强大。如果你有任何问题或困难，它还有一个出色的支持和开发社区。如果你只是想在你的网站上创建一个博客，WordPress 是难以超越的选择。

## Serendipity

另一个出色且结构良好的博客系统是 Serendipity，可以在 `http://www.s9y.org` 下载。它的开发团队中包括一些重量级的 PHP 专家，包括 Sterling Hughes、George Schlossnagle、Wez Furlong 和 Sebastian Bergmann 等人。它也是许多核心 PHP 开发者的首选博客软件包。

### 安装说明

与 Wordpress 类似，安装是一项快速简便的工作。你应该运行 PHP 4 或更高版本，并使用 MySQL、PostgreSQL 或 SQLite 作为数据库。唯一需要牢记的是，在安装完成后要记得限制文件权限，如他们在 `http://www.s9y.org/index.php?node=36` 提供的详尽安装文档中所述。

### 功能概览

Serendipity 提供与 Wordpress 类似的功能，例如允许管理员设置用户权限，使得并非所有用户都能发布博客条目，以及对评论进行审查或启用 CAPTCHA 以防止垃圾信息。使用 Serendipity，你可以为博客文章添加图片，更改网站主题，导入和导出数据，并提供 trackback 和 pingback 以便他人引用你的文章。与 Wordpress 相似的是，它的代码符合标准，并提供 RSS 源供他人使用。

一些 Wordpress 中不太常见的高级功能包括：
- 可选的 Wysiwyg 编辑器：HTMLArea、FCKeditor、xinha、TinyMCE
- 支持 MySQL、PostgreSQL 和 SQLite
- 多用户博客：一个 serendipity 安装可以服务多个独立的博客网站。

### 总结

Serendipity 简单、干净且稳健。如果你在寻找一个只做本职工作且非常可靠的博客，Serendipity 是一个极佳的选择。

## Wiki

正如程序员、编码人员和 Web 开发人员使用软件来管理软件包的开发和部署一样，他们也开始转向 wiki 来协作并创建全面的文档，以补充这些软件包。

### Wiki 的起源

根据维基百科的说法，*wiki* 一词基于夏威夷语术语 *wiki wiki*，意为“快速或非正式”，特别是当提到火奴鲁鲁机场的巴士时。该短语由 Howard（“Ward”）Cunningham 在 1995 年提出，作为波特兰模式仓库（Portland Pattern Repository）的参考，这是一个软件开发思想的协作项目。

随着互联网发展到覆盖大众，wiki 概念的人气大幅增长，特别是在开源社区中，许多人承担了社区责任，不断改进现有产品。文档是使用户理解应用程序的功能或能力的重要组成部分。

Wiki 网站不仅限于支持开源项目，还可以作为几乎任何事物的通用参考指南。有爱好类的 wiki、语言类的 wiki、游戏类的 wiki——你完全可以为任何主题创建一个 wiki。

### MediaWiki

较为流行的软件包之一，也是维基百科背后的引擎，是 MediaWiki。它可在 `http://wikipedia.sourceforge.net` 获取。撰写本文时的最新版本是 1.4.4，并将是此处讨论的重点。

#### 安装说明

在安装 MediaWiki 之前，你应注意以下几点：如果你拥有 root 权限，则在安装前不需要创建数据库。如果你正在远程服务器上安装，则需要在安装前自行创建数据库。此外，在文件解压后，你需要对 config 目录执行 `chmod` 操作，使其可写。安装完成后，你还需要重置权限。



完整的安装指南可在 MediaWiki 网站上找到：`http://meta.wikimedia.org/wiki/MediaWiki_User%27s_Guide:_Installation`。

### 功能概览

由于该网站的目的是跟踪不断演变的文本内容，它拥有管理用户、用户输入和版本控制的一些出色功能。可用的通用功能包括：

- **用户自定义和访问**：用户可以通过编辑自己的模板、设置时区和每页结果数量等偏好来自定义自己的时间界面。管理员可以为不同的用户组分配不同级别的权限，开关他们编辑、移动、贡献或上传文件的能力。
- **搜索能力**：网站访问者可以对网站上包含的所有文章进行全文搜索。
- **报告**：可以生成提供特定统计信息的报告，如使用情况、文章和链接、文章活动和热度、图像、用户等。
- **文章编辑**：用户可以选择只编辑文章的一部分，如果发生编辑冲突，文章可以合并，用户可以在提交前预览其编辑，用户可以使用编辑工具栏来促进编辑过程。
- **文章组织**：文章可以分类和子分类到无限数量的类别中。
- **文本和链接控制**：用户提交文本更改或输入新文本时可以使用受限或完整的 HTML 代码。嵌入的超链接也可以进行管理。
- **监视列表（Watchlist）**：此功能协助管理员和用户跟踪用户的编辑和贡献。它可以显示特定感兴趣的文章、最近的更改以及哪些用户贡献最多。此功能甚至提供编辑前后文章的并排视图，并突出显示更改，以便读者可以轻松识别变更。

![](img/fd2e7361878181c2b12e30301ff3e182_350_0.png)

## 第 13 章

- **多媒体功能：** 用户可以上传其他类型的文件，包括图像、声音文件、数学公式和图表。
- **多语言支持：** 目前支持多种语言，并且具备在不同语言的文章之间建立链接的能力。

有关此包中所有可用功能和特性的完整列表，请访问 `http://meta.wikimedia.org/wiki/MediaWiki_feature_list` 上的 MediaWiki 功能列表。

### 总结

只要访问一次维基媒体（`http://www.wikipedia.org`），你就能完全掌握可以使用 MediaWiki 实现的所有功能。它具有高度功能性、可定制性，是现有最稳健的 wiki 软件包之一。

### DocuWiki

另一个 Wiki 包是 DocuWiki，可在 `http://www.splitbrain.org/go/dokuwiki` 获取。它与其他 wiki 的不同之处在于使用扁平文件，从而使用户摆脱了对数据库的依赖。

#### 安装说明

DocuWiki 是另一个开源包，提供“开箱即用”的安装——只需解压缩并更改权限即可安装。根据位于 `http://wiki.splitbrain.org/wiki%3AInstall` 的详细安装说明，你唯一需要做的是创建一个空的日志文件。

#### 功能总体概述

此 wiki 提供了许多功能，包括：

- **章节编辑：** 允许用户只处理页面的某一部分。
- **版本比较：** 提供两个文档版本之间的高亮彩色差异。
- **用户访问控制：** 允许管理员为用户分配权限。
- **图像上传：** 允许用户将图像包含在 wiki 文档中。
- **多语言支持：** 提供对不同语言的支持。
- **检入/检出：** 防止编辑冲突。

#### 总结

此 wiki 缺少的是与数据库相关的功能，例如页面跟踪和引用统计。与其他一些 wiki 包不同，它也不提供备份实用程序或允许用户对贡献进行评论。除此之外，这是一个简单且可靠的 wiki 包，是一个绝佳的选择，特别是当你无法访问数据库时。

虽然本章迄今主要集中在博客和 wiki 上，但你可能已经开发了一个站点，并需要“插入”一些附加功能。有许多专注于特定领域的 CMS 可以使你的生活更轻松，并允许你无需从头编写代码即可轻松增强你的站点。

一些更流行的微型 CMS 包包括：

- **出版/新闻管理 CMS**：FusionNews，位于 `http://www.fusionphp.net`
- **管理式学习环境 CMS**：Moodle，位于 `http://www.moodle.org`
- **交易型 CMS**：osCommerce 或 ZenCart，分别位于 `http://www.oscommerce.com` 和 `http://www.zencart.com`
- **图像画廊**：Coppermine，位于 `http://coppermine.sourceforge.net`
- **论坛**：phpBB，位于 `http://www.phpBB.com`
- **聊天室**：phpmychat，位于 `http://phpmychat.sourceforge.net`
- **投票/调查**：PrestoPoll，位于 `http://prestopoll.sourceforge.net`
- **日历系统**：WebCalendar，位于 `http://www.k5n.us/webcalendar.php`

### 其他微型 CMS 包

### 其他有用的资源

还有其他地方可以供你筛选优劣——那些致力于比较、评估和跟踪市面上众多 CMS 的地方。以下是让你起步的几项资源：

- **OpenSourceCMS**：`http://www.opensourcecms.com`。该网站旨在让你对几乎所有现有的 PHP/MySQL CMS 进行“试运行”，让你亲身体验每个 CMS 提供的功能、管理屏幕的功能表现以及 CMS 本身的深度和广度。关于这个网站有两点很棒：首先，你不需要花费时间去安装整个包只是为了解演示软件；其次，他们仅展示那些可以在远程服务器（无 root 权限）以及主服务器上可用的 CMS。如果某个 CMS 未列入列表，则要么是他们无法轻松安装它（这是另一个不错的过滤条件），要么是他们尚未知晓。该网站还包含其他用户的评论，以提供完全客观的观点。

使用此网站唯一的缺点是，当你在使用时，也有其他人同时在“摆弄”该软件，这会导致有趣的评估结果以及可能的意外结果。幸运的是，服务器每两小时刷新一次演示软件，因此最终你将能看到一个“干净”的副本。

- **CMSReview**：`http://www.cmsreview.com`。这是一个全面的 CMS 网站，提供了关于如何确定公司 CMS 需求以及在哪里寻找 CMS 顾问的丰富资源，并附带一个指向 CMS 术语表的链接，以防你遇到任何不熟悉的术语。
- **CMSMatrix**：`<http://www.cmsmatrix.org>`。如果你希望以公平的方式比较众多 CMS 包（无论是否开源），这将是一个绝佳的资源。它非常详细，但包含大量信息。
- **CMSWire**：`<http://www.cmswire.com>`。这个较新的 CMS 网站让你了解各行业中最新的 CMS 开发动态和 CMS 使用趋势。如果你致力于处于 CMS 世界的前沿，你可能需要获取该网站的 RSS 源。

## 摘要

我们希望本章能让你获得足够的洞察力，以便对 CMS 包做出明智的选择。正如所示，有许多开源解决方案可以满足几乎任何需求，从非常综合的到非常定制和具体的。虽然很多时候，选择合适的 CMS 归结为个人偏好，但你现在至少有了一个起点，可以基于此形成这些主观观点。

# 附录 A

## 语言翻译

## 注释

```php
// 单行注释
/* 多行注释 */
```

```vbscript
' 单行注释
```

```csharp
// 单行注释
/* 多行注释 */
```

```java
// 单行注释
/* 多行注释 */
```

## 变量类型

| 语言 | 类型机制 |
| :--- | :--- |
| PHP | 松散 |
| ASP/VBScript | 松散 |
| ASP.NET/C# | 强类型 |
| JSP/Java | 强类型 |

## 变量声明

**PHP**

```php
$variable = value;
```

**ASP/VBScript**

```vbscript
Dim variable
```

**ASP.NET/C#**

```csharp
type variable;
```

**JSP/Java**

```java
type variable;
```

## 常量声明

**PHP**

```php
define('NAME', value);
```

**ASP/VBScript**

```vbscript
Const name = value
```

**ASP.NET/C#**

```csharp
const type name = value;
```

**JSP/Java**

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

## 引用数组元素

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

```vbscript
If condition Then

ElseIf condition Then

Else

End If
```

**ASP.NET/C#**

```csharp
if (condition) {

} else if (condition) {

} else {

}
```

**JSP/Java**

```java
if (condition) {

} else if (condition) {

} else {

}
```

## 多选分支

**PHP**

```php
switch (expr) {
case value1:

break;
case value2:

break;
default:

}
```

**ASP/VBScript**

```vbscript
Select Case expr
Case value1

Case value2

Case Else

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

## 循环：While

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

## 循环：Do... While

**PHP**

```
do {
...
} while (expr);
```

**ASP/VBScript**

```
Do
...
Loop Until expr
```

**ASP.NET/C#**

```
do {
...
} while (expr);
```

**JSP/Java**

```
do {
...
} while (expr);
```

## 循环：For

**PHP**

```
for (expr1; expr2; expr3) {
...
}
```

**ASP/VBScript**

```
For expr1 To expr2 Step expr3
...
Next
```

**ASP.NET/C#**

```
for (expr1; expr2; expr3) {
...
}
```

**JSP/Java**

```
for (expr1; expr2; expr3) {
...
}
```

## 循环：For Each

**PHP**

```
foreach ($array as $item) {
...
}

foreach ($array as $key => $item) {
...
}
```

**ASP/VBScript**

```
For Each item In array
...
Next
```

**ASP.NET/C#**

```
for (type item in array) {
...
}
```

**JSP/Java**

```
for (Iterator item; item.hasNext();) {
...
}
```

## 循环：终止

**PHP**

```
break;
```

**ASP/VBScript**

```
Exit Do
Exit For
```

（没有退出 While 循环的方法。）

**ASP.NET/C#**

```
break;
```

**JSP/Java**

```
break;
```

## 循环：进入下一轮

**PHP**

```
continue;
```

**ASP/VBScript**

```
Not supported
```

**ASP.NET/C#**

```
continue;
```

**JSP/Java**

```
continue;
```

## 函数/方法声明

**PHP**

```
function name (args) {
...
}
```

**ASP/VBScript**

```
Function name (args)
...
End Function

Sub name (args)
...
End Sub
```

**ASP.NET/C#**

```
visibility returnType name (args) {
...
}
```

**JSP/Java**

```
visibility returnType name (args) {
...
}
```

## 返回函数值

**PHP**

```
return value;
```

**ASP/VBScript**

```
FunctionName = value
```

**ASP.NET/C#**

```
return value;
```

**JSP/Java**

```
return value;
```

## 使用命名空间对类进行分组

**PHP**

Not supported

**ASP/VBScript**

Not supported

**ASP.NET/C#**

```
namespace Name { ... }
```

**JSP/Java**

```
package name;
```

## 类可见性关键字

**PHP**

`public, private, protected`

**ASP/VBScript**

`public, private`

**ASP.NET/C#**

`public, private, protected, internal`

**JSP/Java**

`public, private, protected, package`

## 基类定义

**PHP**

```
class ClassName {
…
}
```

**ASP/VBScript**

```
Class ClassName
…
End Class
```

**ASP.NET/C#**

```
visibility class ClassName {
…
}
```

**JSP/Java**

```
visibility class ClassName {
…
}
```

## 声明类属性

**PHP**

```
visibility name;
```

**ASP/VBScript**

```
visibility name
```

**ASP.NET/C#**

```
visibility type name;
```

**JSP/Java**

```
visibility type name;
```

## 调用同类中的方法

**PHP**

```
$this->method();
```

**ASP/VBScript**

```
Me.method
```

**ASP.NET/C#**



```
this.method();
```

**JSP/Java**

```
this.method();
```

## 类构造函数

**PHP**

```
function __construct() {
    ...
}
```

**ASP/VBScript**

```
Private Sub Class_Initialize()
    ...
End Sub
```

**ASP.NET/C#**

```
visibility ClassName() {
    ...
}
```

**JSP/Java**

```
public ClassName() {
    ...
}
```

## 类析构函数

**PHP**

```
function __destruct() {
    ...
}
```

**ASP/VBScript**

```
Private Sub Class_Terminate()
    ...
End Sub
```

**ASP.NET/C#**

```
visibility ~ClassName() {
    ...
}
```

**JSP/Java**

```
protected void finalize() {
    ...
}
```

## 使用静态类方法

**PHP**

```
ClassName::StaticMethod();
```

**ASP/VBScript**

Not supported

**ASP.NET/C#**

```
ClassName.StaticMethod();
```

**JSP/Java**

```
ClassName.StaticMethod();
```

## 创建对象

**PHP**

```
$obj = new ClassName();
```

**ASP/VBScript**

```
Set obj = New ClassName
```

**ASP.NET/C#**

```
type obj = new ClassName();
```

**JSP/Java**

```
type obj = new ClassName();
```

## 类继承

**PHP**

```
class ClassName extends BaseClass {
    ...
}
```

**ASP/VBScript**

Not supported

**ASP.NET/C#**

```
visibility class ClassName : BaseClass {
... 
}
```

**JSP/Java**

```
visibility class ClassName extends BaseClass {
... 
}
```

## 调用父类方法

**PHP**

```
parent::method();
```

**ASP/VBScript**

Not supported

**ASP.NET/C#**

```
base.method();
```

**JSP/Java**

```
super.method();
```

## 声明抽象类

**PHP**

```
abstract class AbstractClass {
... 
}
```

**ASP/VBScript**

Not supported

**ASP.NET/C#**

```
abstract class AbstractClass {
... 
}
```

**JSP/Java**

```
visibility abstract class AbstractClass {
...
}
```

## 停止子类化

**PHP**

```
final class EndClass {
...
}

final visibility function MethodName() {
...
}
```

**ASP/VBScript**

Not supported

**ASP.NET/C#**

```
sealed class EndClass {
...
}

sealed visibility type MethodName() {
...
}
```

**JSP/Java**

```
visibility final class EndClass {
...
}

visibility final type MethodName () {
...
}
```

## 接口声明

**PHP**

```
interface InterfaceName {
...
}
```

**ASP/VBScript**

Not supported

**ASP.NET/C#**

```
visibility interface InterfaceName { ... }
```

**JSP/Java**

```
visibility interface InterfaceName { ... }
```

## 类使用接口

**PHP**

```
class ClassName implements InterfaceName { ... }
```

**ASP/VBScript**

Not supported

**ASP.NET/C#**

```
visibility class ClassName : InterfaceName { ... }
```

**JSP/Java**

```
visibility class ClassName implements InterfaceName { ... }
```

## 包含外部文件

**PHP**

```
include('filename');
include_once('filename');
require('filename');
require_once('filename');
```

**ASP/VBScript**

```
<!-- #include 'filename' -->
```

**ASP.NET/C#**

包含操作通过多种方法处理，包括传统的 ASP 包含（如上所示）

**JSP/Java**

```
<%@ include file="filename" %>
```

## 异常处理

**PHP**

```
try {
...  
} catch (ExceptionType $e) {
...  
}
```

**ASP/VBScript**

未特别支持

**ASP.NET/C#**

```
try {
...  
} 
catch (ExceptionType e) {
...  
} 
finally {
...  
}
```

**JSP/Java**

```
try {
...  
} 
catch (ExceptionType e) {
...  
} 
finally {
...  
}
```

## 抛出异常

**PHP**

```
throw new ExceptionType(args);
```

**ASP/VBScript**

```
Err.Raise number
```

## HTTP POST 值

**PHP**

`$_POST`（数组）

**ASP/VBScript**

`Request.Form`（集合）

**ASP.NET/C#**

`System.Web.HttpRequest.Form`（NameValueCollection）

**JSP/Java**

`request.getParameter()`（方法查找）

## HTTP GET 值

**PHP**

`$_GET`（数组）

**ASP/VBScript**

`Request.QueryString`（集合）

**ASP.NET/C#**

`System.Web.HttpRequest.QueryString`（NameValueCollection）

**JSP/Java**

`request.getParameter()`（方法查找）

## 服务器变量

**PHP**

`$_SERVER`（数组）

**ASP/VBScript**

`Request.ServerVariables` (collection)

**ASP.NET/C#**

`System.Web.HttpRequest.ServerVariables` (NameValueCollection)

**JSP/Java**

`request.getVariable()`（方法查找；每个服务器变量使用不同的方法）

# 附录 B

## 替代工具

每当讨论流行的 PHP 工具时，话题通常集中在文本编辑器或编码 IDE 上。哪种拥有最好的语言支持、语法高亮、代码解析等？不幸的是，由于过分关注文本编辑器，一些优秀的非编码工具有时会被忽视。除了重述一种编辑器优于另一种编辑器的常规论点外，本附录展示了你在开发周期中可以使用的一些工具——那些不会立即产生代码，但你可能发现它们在整体开发过程中占据关键位置的工具。

### MySQL 工具



当你管理 MySQL 数据库时，管理工具通常有两个主要选项：标准的命令行工具集，或图形界面。尽管许多资深的系统管理员持不同态度，但使用图形工具来完成任务绝对没有任何问题。虽然命令行界面提供了对数据库的无限控制，但它无法匹敌良好的图形用户界面在促进管理工作流程方面的速度和清晰度。

如果你在寻找一套优秀的基于 GUI 的 MySQL 管理工具，不需要再寻找，MySQL AB 自己的 MySQL Administrator 和 MySQL Query Browser 就是很好的选择。

# 附录 B

![](img/fd2e7361878181c2b12e30301ff3e182_373_0.png)

**图 B.1**

## MySQL Administrator

MySQL Administrator 是一个功能丰富的 GUI 管理工具，用于维护 MySQL 数据库。主要界面如图 B.1 所示。

MySQL Administrator 允许您执行以下操作：

- 查看实时服务器信息，包括连接信息和统计信息、内存统计信息、MySQL 内部变量和配置设置的值等。
- 查看不同的服务器日志：错误日志、慢查询日志、通用日志（仅限本地主机）。
- 控制 MySQL 进程本身（仅限本地主机）。
- 执行备份和恢复操作，甚至可以安排定期备份。
- 管理服务器的用户访问权限和特权。
- 使用内置的 MySQL 表编辑器创建和编辑完整的数据库，包括表。

MySQL Administrator 可用于 Windows、Linux 和 Mac OS X；MySQL Administrator 可以从 MySQL 网站免费下载：`http://www.mysql.com/products/administrator/`。

## MySQL Query Browser

MySQL Query Browser 是一个图形用户界面（GUI），允许您针对 MySQL 数据库测试和运行各种查询。从某种意义上说，它是命令行客户端的增强版 GUI 版本，正如您在图 B.2 中看到的那样。您还可以将 MySQL Query Browser 用作标准的电子表格程序或桌面数据库应用程序——您可以调出数据行，并直接在查询浏览器中对其进行编辑。除了输入和执行查询以及操作数据外，它还包含 MySQL Administrator 中的 MySQL 表编辑器，允许您可视化和编辑数据库和表。

![](img/fd2e7361878181c2b12e30301ff3e182_374_0.png)

**图 B.2**

Windows、Linux 和 Mac OS X 版本可从 MySQL 网站获取：`<http://www.mysql.com/products/query-browser/>`。

现在，您的应用程序已经上线并运行，您的服务器也已调整至最佳性能。但是，您的数据库查询是否已经尽可能精简高效？唯一确定的方法是使用基准测试工具。

大多数 MySQL 基准测试工具的工作方式大致相同：您提供一个要运行的查询，该工具会运行该查询大量次数，通常使用并发连接。通过彻底测试和实验您的一些“较重”的查询（通常可以在 MySQL 慢查询日志中找到），您可以提高应用瓶颈处的执行时间和服务器负载。

### MySQL Super Smack

MySQL Super Smack 最初由 Sasha Pachev 开发，是一个用于 MySQL 和 PostgreSQL 的独立压力测试工具。MySQL Super Smack 接收一个或多个包含查询的文件，并以指定的并发连接数对目标数据库进行预定义次数的“轰炸”测试。

MySQL Super Smack 可从以下地址获取：`<http://vegan.net/tony/supersmack/>`。

### MyBench

MyBench 是由 MySQL 专家 Jeremy Zawodny 创建的一个基于 Perl 的基准测试工具。与 MySQL Super-Smack 类似，它可以向目标 MySQL 机器发送大量连接和查询，并给出明确的关于其抵抗这种攻击效果的结果。由于它是用 Perl 编写的，您可以轻松地对其进行修改和扩展。缺点是，大批量测试可能会占用机器资源，因此最好在不同于目标 MySQL 服务器的另一台机器上运行此工具，以免污染结果。

MyBench 可在 Jeremy Zawodny 的网站获取：`<http://jeremy.zawodny.com/mysql/mybench/>`。

## 版本控制

您可能希望在开发生命周期或工作流中考虑某种形式的版本控制系统，如果您还没有使用的话。版本控制系统提供了一种在开发过程中存储代码历史快照的方法，并允许多个开发人员将文件签入和签出仓库，从而控制代码库的演变。当前最常用的两个开源版本控制系统是 CVS 和 Subversion。

CVS 和 Subversion 都是支持相同基本功能的版本控制系统：文件版本的历史记录，以及支持多开发人员签入/签出功能。CVS 自 1989 年就已存在，并一直是许多开发人员的首选。Subversion 出现得较晚，首次亮相于 2000 年底，但由于其功能集扩展超出了 CVS 中常见的“标准”功能，因此正迅速获得追随者。功能如原子提交、“安全”的文件重命名、文件和目录复制以及 WebDAV 支持是许多开发人员如今选择 Subversion 的一些原因。如果您正在寻找功能强大且客户端和服务器端都有良好支持的功能集，Subversion 可能是您的最佳选择。如果您正在寻找稳定性、使用记录以及许多开发工具内置的支持，CVS 可能更可取——尽管越来越多的开发软件包最近正在获得 Subversion 支持。

无论您选择哪个，尽早引入某种版本控制都是个好主意——它使多开发人员项目更容易管理，并可以为新代码实际上导致新的恶性 bug 或回归问题时提供一张安全网。

CVS 可在 `https://www.cvs_home.org/` 获取。

Subversion 可在 `http://subversion.tigris.org/` 获取。

## UML 工具

如果您深入系统架构和设计领域，很有可能您会在某个时候遇到 UML。如果您不熟悉 UML，简而言之，它是一种用于建模和表示应用程序或其他系统的结构、行为、架构和流程的方法。您可以使用 UML 对系统或应用程序的不同方面进行图表化，包括类结构、用户交互、对象交互、流程等，类似于您可能使用 Visio、Kivio 或其他相关工具制作的流程图和其他图表。

UML 有九种图表类型，但从开发人员的角度来看，其中最重要的是类图。类图帮助您规划您的各种类以及这些类之间的关系。

如果您在 PHP 工作流中使用 UML，您手头有几款工具——一些流行的免费工具是 ArgoUML 和 Umbrello。

### ArgoUML

ArgoUML 是一个由 Tigris.org 社区创建的基于 Java 的 UML 编辑器。它支持八种主要的 UML 图表类型，并可以帮助您快速规划对象、关系和行为。从 PHP 开发人员的角度来看，ArgoUML 的主要功能之一是它能够从 UML 类图自动生成有效的 PHP5 类骨架（以及 C#、Java、C++ 和 PHP4），如图 B.3 所示。

您只需在 UML 中创建类图，并告诉 ArgoUML 要生成代码的位置，这就为您节省了输入类结构的时间，让您能够专注于代码的核心：实现。ArgoUML 还提供关于您的类结构的机器生成建议，并集成了待办事项列表。

ArgoUML 作为桌面 Java 应用程序可用，既可以从 Internet 下载并运行，也可以通过 JavaWebStart 在 `http://argouml.tigris.org/` 获取。

![](img/fd2e7361878181c2b12e30301ff3e182_377_0.png)

### Umbrello

Umbrello 是另一个 UML 图表应用程序，类似于 ArgoUML。Umbrello 现在是 KDE 开发人员工具包的一部分，支持许多主要的 UML 图表类型，包括类图、用例图、状态图和顺序图。从 1.4 版本开始，Umbrello 可以生成 PHP5 类骨架，以及几种其他编程语言的代码，如图 B.4 所示。

![](img/fd2e7361878181c2b12e30301ff3e182_378_0.png)

**图 B.4**

Umbrello 可作为 KDE 桌面环境（3.2 或更高版本，Linux）的一部分找到，或者您可以直接从 Umbrello 网站（针对 KDE/Linux）下载，网址为 `http://uml.sourceforge.net/`。

# 索引

## 符号和数字

- `{ }`（**花括号**）

  - 缩进标准，214–217
  - 减少嵌套级别，217–220

- `:`（**冒号**）

  - 与类常量一起使用（`:`），28–29
  - PHP URL 中的方案名称后（`://`），72
  - 与 `self` 关键字一起使用（`::`），7，27–28

- `S`（**美元符号**）

  - 未与类常量一起使用（PHP），29
  - `$this` 引用变量（PHP），23，50



- `::`（双冒号）。参见 : （冒号）

- `=`（等号）在相等运算符与赋值运算符中，219

- `404` 处理器，缓存相关，226

- `"`（双引号）

  - 在 `set_exception_handler()` 内的函数名称中，5
  - 字符串速度相关，201–205

- `'`（单引号），字符串速度相关，201–205

- `/`（斜杠）

  - MySQL 查询的终止符 `/g`，86
  - PHP URL 中的方案名称后（`://`），72

## A

- **ab**

  - `ApacheBench` 程序，208–209
  - `abort()` 方法（AJAX），277

- **抽象类（PHP）**

  - 用于的 `abstract` 关键字，7
  - 示例，7–8
  - 语言翻译，341–342
  - 命名约定，222
  - 概述，34–35
  - 使用规则，8

- `abstract` 关键字（PHP），7

- **访问控制（Apache）。** 参见 **身份验证**

- **访问控制（MySQL）**

  - `GRANT` 和 `REVOKE` 的替代方案，97–100
  - 用于的 `columns_priv` 表，99，100
  - 用于的 `db` 表，98–99，100
  - 用于的 `GRANT` 命令，94–96
  - 重新加载权限表，100
  - 用于的 `REVOKE` 命令，96–97
  - 服务器限制，100
  - 用于的 `tables_priv` 表，99，100
  - 用户管理，93–100
  - 用于的 `user` 表，97–98，99–100

- **访问控制（PHP）**

  - 基本身份验证，166–171
  - 注册表单中的 CAPTCHA 图像用于，175–177

# 索引

### 访问控制（PHP）（续）

- 表单认证，172–174
- `HTTP_REFERER` 值，174–175
- `REMOTE_ADDR` 值，174
- 服务器变量，174–175

### 访问修饰符（PHP）

参见具体修饰符

- `Circle` 类示例，24–25
- 语言翻译，337
- PHP5 增强功能，6
- 指定可见性，23–24

### `addslashes()` 函数（PHP）

113

### `AJAX` (Asynchronous JavaScript and XML)

- 可访问性问题，283–285
- `CPaint` 库，283
- 描述，273
- `DOM` 操作，273, 281–282
- 更多信息，285
- Google 的 `Gmail` 应用，273
- 处理 `ReadyStateChange` 事件，280
- 处理响应，280–282
- 历史，274–277
- `JPSpan` 库，283
- 方法，277–278
- 属性，278–279
- `SAJAX` 库，282–283
- 支持问题，285
- 与传统 Web 应用的对比，273, 274
- 可用性顾虑，283–285
- 处理浏览器差异，279–280
- `XMLHTTP` 和 `XMLHttpRequest` 接口，277–282

### `Alcantara, Frank` (AAceleware 维护者)

290

### `Alien Indentation` 风格

215–216

### `Alpha` 透明

244

### `ALTER TABLE` 语句 (MySQL)

87, 90–91, 92

### 替代 PHP 缓存

参见 `APC`

### 数据库分析 (MySQL)

100–102

### 匿名函数 (PHP)

57–58

### `Apache`

参见 URL 重写 (Apache)

- 与 MySQL 配合进行身份验证，129, 149–154, 166
- Basic Authentication，154, 165–166
- 内容压缩，145–149
- 404 处理器与缓存，226
- `mod_alias`，226
- `mod_auth_mysql`，129, 149, 150–154
- `mod_dav`，129, 158
- `mod_deflate`，129, 146–148
- `mod_proxy`，138
- `mod_rewrite`，226
- `mod_spelling`，129, 144–145
- `mod_ssl`，129, 154–155
- 作为在线文件存储库，158–163
- `PDFLib` 配置，234
- 性能优化，211–213
- 启用 SSL，154–157
- URL 拼写检查，144–145

### `ApacheBench` 程序 (`ab`)

208–209

### `APC` (Alternative PHP Cache)

- 配置，288–290
- 历史，287
- 安装，288
- 与其他缓存引擎的配合，305
- 概述，287
- 移除，290
- 适用场景，305
- 网站，288

### 数组函数 (PHP)

参见回调函数 (PHP)

- `array_filter()`，53
- `array_map()`，49, 50–51
- `array_walk()`，49, 51–52
- 大多数函数提供了回调，48
- `call_user_func_array()`，55–56
- 描述，48
- 一系列函数的内存需求，59–60
- `preg_grep()`，53
- `preg_replace_callback()`，53–55
- 使用回调，48–50
- 类型和数量，59

### `array_filter()` 函数 (PHP)

53

### `ArrayIterator` 类 (PHP)

6

### `array_map()` 函数 (PHP)

49, 50–51, 55–56

### 回调函数 (PHP)

- 用于抽象功能，48
- 用于 `array_filter()`，53
- 用于 `array_map` 函数，null 回调，50–51
- 用于 `array_walk()` 函数，52
- 用于 `call_user_func_array()` 函数，55–56

### 数组 (PHP)

参见 数组函数 (PHP)

- 检查大小，性能影响，229
- 语言翻译，331
- 命名约定，222
- 临时变量与性能，229–230

### `array_walk()` 函数 (PHP)

49, 51–52

### `ASP`

参见 语言翻译

### `ASP.NET`

参见 语言翻译

### `ASP` 风格标签

`php.ini` 设置，106–107

### 按值赋值与按引用赋值 (PHP)

29

### Asynchronous JavaScript and XML

参见 `AJAX`

### `attempt_auth()` 函数 (PHP)

169–170

### 身份验证

- 使用 Apache 和 MySQL，149–154
- 使用 Apache 和 SSL，154–157
- Apache Basic Authentication，154, 165–166
- 用于此目的的 `Auth_HTTP` PEAR 包，187–188
- PHP 控制，166–177
- 使用 WebDAV，159

### `Auth_HTTP` PEAR 包

187–188

### `AUTO_INCREMENT` 列 (MySQL)

89

## B

### 备份 (MySQL)

103–104

### Basic Authentication (Apache)

- 实现，165
- 局限性，154
- 与 MySQL 配合，149–154, 166
- 与 PHP 控制的身份验证配合，166, 171
- 不适用场景，165–166

### Basic Authentication (PHP)

- 与 Apache 控制的身份验证配合，166, 171
- 创建身份验证数据库，166–167
- 用于此目的的 `phpauthbasic.php` 脚本，167–171
- 测试，171

### 基准测试

- `ab` `ApacheBench` 程序，208–209
- 定义，206–207
- `MyBench` MySQL 工具，350
- PEAR 基准测试类，207–208
- 不同运行的结果差异，202
- 字符串速度示例，201–205

### 基准测试类 (PEAR)

207–208

### 博客

`Micro CMS`

- 流行程度，322
- 原因，322
- `Serendipity`，324
- `WordPress`，323

### 大括号 ({})

- 缩进标准，214–217
- 减少嵌套级别，217–220

### `BSD`

缩进风格，215–216

### `Bzip2` 扩展 (PHP)

271

## C



### C#

参见 语言翻译

### 缓存 (PHP)

- APC 缓存引擎，287–290

- 选择缓存引擎，305

- 客户端，227

- CMS 提供的机制，225–226

- eAccelerator 缓存引擎，290–294

- Expires: 头，227

- JPCache 缓存引擎，296–300

- memcached 缓存引擎，300–304

- 输出预生成，224–226

- PEAR 包，224–225

- 性能优势，223

- 源代码预解析，223–224

- 使用 404 处理器，226

- 同时使用不同的缓存引擎，304–305

- Zend Optimizer 缓存引擎，294–296

### `calcArea()` 方法

21

### `__call()` 魔术方法 (PHP)

8–9, 38

### `create_function()` 函数

参见 回调函数 (PHP)，57–58

### 预计将有新的实现

参见 回调函数 (PHP)，59

### `preg_replace_callback()` 函数

参见 回调函数 (PHP)，53–55

### 为大多数数组函数提供

参见 回调函数 (PHP)，48

### 配合 self 关键字使用

参见 回调函数 (PHP)，50

### 指定类和对象方法

参见 回调函数 (PHP)，49–50

### 包含函数名称的字符串

参见 回调函数 (PHP)，49

### 配合 `$this` 引用变量使用

参见 回调函数 (PHP)，50

### 使用

参见 回调函数 (PHP)，48–50

### 调用方法或函数

- 用于此目的的 `construct()` 魔术方法，6

- 语言翻译，338–339, 341

- 使用魔术方法重载，8–9

- 过程式调用 (MySQL)，13

- `call_user_func()` 函数，56–57

- `call_user_func_array()` 函数，55–56

### CAPTCHA (Completely Automated Public Turing Test to Tell Computers and Humans Apart)

175–177

### `caption()` 方法 (`WebImage` 类)

251–252

### CASCADE 选项 (MySQL)

92

### case 语句

语言翻译，332–333

### CERT 网站

182

### `check_login()` 函数 (PHP)

170–171

### Circle 类示例

- 抽象 Shape 类，34–35

- 配合 `call()` 魔术方法使用，38

- 配合 `clone` 语句使用，29–30

- 构造函数，25–26

- 定义，20

- 析构函数，26–27

- 配合 `get()` 和 `set()` 魔术方法使用，39

- 从 Shape 类继承，31–33

- 用于 memcached 缓存引擎，303–304

- 方法，21

- `parent::` 引用，34

- 属性，21

- 配合 `sleep()` 和 `wakeup()` 魔术方法使用，40–43

- 配合 `static` 关键字使用，27–28

- 配合 `ToString()` 魔术方法使用，44

- 在其中指定可见性，24–25

### 类常量 (PHP)

28–29

### 类 (PHP)

参见具体类

- 抽象类，7–8, 34–35, 222, 341–342

- 基础知识，20–23

- 类常量，28–29

- 描述，20

- 配合 `final` 关键字使用，6

- 实例化，22–23

- 语言翻译，337–342

- 命名约定，222

### CLI

使用 CLI 安装 PEAR，186

### 客户端 URL 库函数 (CURL) 扩展 (PHP)

271

### 客户端缓存

227

### `clone` 语句 (PHP)

29–30

### 关闭流 (PHP)

63

### CMSMatrix 网站

328

### CMSReview 网站

327

### CMS (Content Management Systems)

- 全功能 Web CMS，309–322

- 博客包，322–324

- 提供的缓存机制，225–226

- 描述，307

- DocuWiki，326

- Drupal，321

- 企业级 CMS，307–308

- ExponentCMS，309–312

- Mambo，321

- MediaWiki，325–326

- Micro CMS，322–328

- 开源 Web CMS 包，308

- PHP-Nuke，321

- phpWebsite，315–318

- Postnuke，322

- 资源，327–328

- Serendipity，324

- TikiWiki，318–321

- Web CMS，描述，308

- **WordPress**，323

- **XOOPS**，312–315

- **CMSWire 网站**，328

- **代码效率。参见 性能编码标准（PHP）**

  - 花括号和缩进，214–217

  - 注释，216, 217, 220

  - 通过解析错误强制执行，222–223

  - 命名约定，220–222

  - 概述，213–214

  - PEAR，214

  - 减少嵌套级别，217–220

- **冒号 (:)**

  - 用于类常量 (::)，28–29

  - PHP URL 方案名称后 (://)，72

  - 用于 self 关键字 (self::)，7, 27–28

- **`columns_priv` 表 (MySQL)**，99, 100

- **注释**

  - Big Flashy Box 风格，216, 217

  - 编码标准，220

  - Javadoc 风格，220

  - 语言翻译，329

  - 用于缩进的制表符，216, 217

- **完全自动公共图灵测试，用于区分计算机和人类 (CAPTCHA)**，175–177

- **压缩内容。参见 内容压缩 (Apache)**

- **字符串连接，速度基准测试**，201–205

- **条件语句**

  - 语言翻译，331–336

  - 与性能相关，230

- **`config-help` 命令 (PEAR 管理器)**，186

- **`ConfigManager.php` 类**

  - 代码清单，117

  - `configfile` 属性，118

  - `configtype` 属性，118

  - 构造方法，118

  - 声明，117

  - `errors` 属性，118

  - `processConfig` 方法，118–119

- **`ConfigProcessor` 接口 (PHP)**，119

- **`config-set` 命令 (PEAR 管理器)**，186

- **`config-show` 命令 (PEAR 管理器)**，185–186

- **配置检查器 (PHP)**

  - `ConfigManager.php` 类，117–119

  - `ConfigProcessor` 接口，119

  - `reqs.xml` 文件，116

  - `test.php` 代码，128

  - `XMLConfigProcessor.php` 类，119–128

- **配置变量 (PEAR)**，185

- **配置 PHP。参见 php.ini 配置文件；运行时配置 (PHP)**

- **`const` 关键字 (PHP)**，29

- **常量**

  - 类常量 (PHP)，28–29

  - 语言翻译，330

  - 命名约定，222

- **`__construct()` 魔术方法 (PHP)**

  - Circle 类示例，25–26

  - `ConfigManager.php` 类，118

  - 描述，37

  - 概述，6, 25–26

  - 与 PHP4 构造器的区别，25

  - `XMLConfigProcessor.php` 类，122–123

- **构造器 (PHP)**

  - Circle 类示例，25–26

  - 使用 `__construct()` 魔术方法，6, 25–26

  - 语言翻译，339

  - 概述，25–26

  - PHP4 构造器，25

- **内容压缩 (Apache)**

  - 配置指令，147–148

  - 描述，145–146

  - `mod_deflate` 的有效性，148

  - 用于此的 `httpd.conf` 文件，146–147

  - 需求，145

  - 用于 PHP 脚本，148–149

  - 使用 `mod_deflate`，146–148

- **内容管理系统。参见 CMSs 表转换**

  - InnoDB 到 MyISAM，93



- `MyISAM` 到 `InnoDB`，90

## 坐标系

- `Ming` 扩展 (`PHP`)，264

- `PDFLib` 扩展 (`PHP`)，237

- `Coppermine CMS`，327

- `使用 clone 语句复制对象 (PHP)`，29–30

- `Cowgill, Daniel (APC 创造者)`，287

- `CPAINT (跨平台异步接口工具包)`，283

- `CREATE DATABASE` 语句 (`MySQL`)，75

- `CREATE TABLE` 语句 (`MySQL`)，75

  - 用于 Apache 身份验证示例，149–150
  - 启用全文搜索，86–87
  - 概述，75
  - 用于 PHP 身份验证示例，166–167
  - `create_function()` 函数，57–58

- `交叉连接 (MySQL)`，81, 82

- `跨平台异步接口工具包 (CPAINT)`，283

- `跨站脚本 (XSS)`，180–181

- `CSS` 样式表
  - AJAX 的使用，273
  - 用于此的 PEAR 包，192–193

- `cURL (客户端 URL 库函数)` 扩展 (`PHP`)，271

- `CVE` 网站，182

- `CVS` 版本控制系统，350–351

## D

- `数据对象，用于集成的 PEAR PDO 包`，196–197

- `数据库分析 (MySQL)`，100–102

- `数据库维护 (MySQL)`，103–104

- `数据库相关包 (PEAR)`
  - `Auth_HTTP`，187–188
  - `DB`，190–192
  - `HTML_Table`，194–195
  - `PEAR::Auth`，187, 188
  - `PEAR::DB`，187
  - 相关网站，191

- `数据库 (MySQL)`。参见 `MySQL`

- `Date PEAR 包`，189–190

- `DB PEAR 包`，190–192

- `db` 表 (`MySQL`)，98–99, 100

- `调试脚本，用于此的 Xdebug PECL 包`，197

- `DeflateCompressionLevel` 指令 (`Apache` 的 `mod_deflate`)，147

- `DeflateFilterNote` 指令 (`Apache` 的 `mod_deflate`)，148

- `DeflateWindowSize` 指令 (`Apache` 的 `mod_deflate`)，148

- `DELETE` 语句 (`MySQL`)，77, 92

- `删除数据库信息 (MySQL)`，77, 92

- `destruct()` 魔术方法 (`PHP`)，6, 26–27, 37

- `析构函数 (PHP)`
  - `Circle` 类示例，26–27
  - 使用 `destruct()` 魔术方法，6, 26–27
  - 语言翻译，339–340
  - 概述，26–27

- `指令 (PHP)`。参见 `php.ini` 配置文件

- `目录`
  - 自动重定向 URL，132
  - 为 SSL 网站创建，157
  - 使用 `glob()` 进行模式匹配读取，60–61
  - 用于 WebDAV 文件仓库，158

- `DirectoryIterator` 类 (`PHP`)，5

- `磁盘访问，与性能相关`，211

- `display()` 方法 (`WebImage` 类)，244

- `DocuWiki Micro CMS`，326

- `美元符号 ($)`
  - 不用于类常量 (`PHP`)，29
  - `$_this` 引用变量 (`PHP`)，23, 50

- `DOM (文档对象模型)`
  - AJAX 操作，273, 281–282
  - `DOM` 扩展 (`PHP`)，16, 271

- `双冒号 (::)`。参见 `冒号 (:)`
  - `do...while` 循环，语言翻译，334

- `drawHR()` 函数 (`PDFLib`)，236

- `Drupal CMS`，321

360

## E

- `eAccelerator` 缓存引擎
  - 配置，291–294
  - 安装，291
  - 其他缓存引擎及此，305
  - 概述，290–291
  - 移除，294
  - 网站，291

- `DSO (动态共享对象)`
  - 安装 `APC` 作为 `DSO`，287, 288
  - 安装 `eAccelerator` 作为 `DSO`，291
  - 安装 `memcached` 作为 `DSO`，301
  - `PDFLib` 配置及此，234

- `eXtensible Object Oriented Portal System`。参见 `XOOPS`

- `extends` 关键字 (`PHP`)
  - `emailException` 示例，3–4
  - 继承及此，31–33
  - 接口及此，36–37
  - 概述，3, 31–33

- `extension_loaded()` 函数 (`PHP`)
  - 概述，111
  - 在 `XMLConfigProcessor.php` 类中，124, 125

- `外部文件，用于包含的语言翻译`，343–344

- `echo` 语句 (`PHP`)
  - 与 `print` 语句对比，228–229
  - 与 `__toString()` 魔术方法一起使用，44

- `emailException` 类，3–4

- `企业级 CMS`，307–308。另参见 `CMS (内容管理系统)`

- `等号 (=)` 在相等运算符与赋值运算符中，219

- `错误消息，php.ini 设置`，106

- `Exception` 类 (`PHP`)，2–4

- `异常 (PHP)`
  - 描述，1
  - 用于此的 `Exception` 类，2–4
  - 语言翻译，344–345
  - `PHP5` 变更与增强，1–5
  - 与 `set_error_handler()` 函数对比，1–2
  - 用于此的 `try/catch/throw` 块，2, 234, 344–345

- `Expires: 头，与缓存相关`，227

- `ExponentCMS`
  - 额外模块，310
  - 自定义默认设置，310–311
  - 默认功能，309
  - “非活动”功能，309
  - 安装，309–310
  - 优势与劣势，311
  - 网站，309, 310

## F

- `胖客户端 Web 应用程序`。参见 `AJAX (异步 JavaScript 和 XML)`

- `文件访问日志记录器示例`
  - 代码清单，64–66
  - 注册流封装器，66
  - `stream_close()` 函数，67
  - `stream_open()` 函数，67
  - `stream_read()` 函数，67
  - `stream_write()` 函数，67
  - 使用日志记录流，66–67

- `使用 Apache 的文件仓库`。参见 `WebDAV (基于 Web 的分布式创作和版本管理)`

- `FileInfo PEAR 包`，196

- `final` 关键字 (`PHP`)，6, 33

- `Flash 文件 (Shockwave)`。参见 `Ming` 扩展 (`PHP`)

- `FLUSH PRIVILEGES` 命令 (`MySQL`)，100

- `for` 循环
  - 不需要的数组函数，48
  - 语言翻译，335

- `foreach` 循环
  - 不需要的数组函数，48
  - 用于避免此的 `array_walk()` 函数，49, 51–52
  - 语言翻译，335

## G

- `外键约束 (MySQL)`
  - 优势，89
  - 使用 `ALTER_TABLE` 语句创建，90–91, 92
  - 命名，90
  - 与 `NULL` 值相关，89
  - 指定行为选项，92
  - 与 `UPDATE` 语句相关，91–93

- `表单 (HTML)`，用于此的 PEAR 包，193–194

- `表单 (PHP)`
  - 用于登录身份验证，172–174
  - `php.ini` 设置，105, 107

- `404 处理器，与缓存相关`，226

- `框架 (Ming)`，264

- `FTP`，使用此安装 PEAR，186

- `全文搜索 (MySQL)`
  - 修改现有表以支持此，87
  - 创建启用此的新表，86–87
  - 局限性，88
  - 最小全文词长指定，88
  - `InnoDB` 不支持，89
  - 用于此的 `SELECT` 语句，87–88



### **函数 (MySQL)，过程式调用**，13

### **函数 (PHP)。另参见 数组函数 (PHP): 特定函数**
- 匿名，57–58
- `ArrayIterator` 类，6
- 回调及此，49
- 检查扩展及其属性，111–112
- 检查已安装版本，108
- 检查魔术引号设置，113
- `Exception` 类，3
- `Iterator` 类，5
- 语言翻译，336–337
- 命名约定，220, 221–222
- PHP5 新增，91–92
- 运行时检索配置设置，109–110
- 多样性与数量，47

### **FusionNews CMS**，327

### `/*G` 用于 MySQL 查询的终止符，86

### **GD 库扩展 (PHP)**
- 添加字幕，250–254
- 添加徽标，254–257
- alpha 透明度及此，244
- 创建图像基础，241–245
- 描述，241
- `ImageCaption` 类，250–254
- `ImageLogo` 类，254–257
- `ImageResize` 类，245–248
- `ImageRotate` 类，249–250
- 索引透明度及此，244
- 手册，263
- 调整图像大小，245–248
- 旋转图像，248–250
- 测试，257–261
- 用于此的 `WebImage` 基类，241–245, 246–247, 249, 251–252
- `WebImage` 类，255–256

### `__get()` 魔术方法 (PHP)
- `Circle` 类示例，39
- 示例，8
- 概述，38–39

- `get_cfg_var()` **函数 (PHP)，109**
- `get_defined_functions()` **函数 (PHP)，57**
- `get_extension_funcs()` 函数 (PHP)，112
- `get_loaded_extensions()` **函数 (PHP)，111–112, 116**
- `get_magic_quotes_gpc()` **函数 (PHP)，113**
- `get_magic_quotes_runtime()` **函数 (PHP)，113**
- `getMessage()` **函数 (PHP)，2, 3**
- `getResponseHeader()` **方法 (AJAX)，277**

### **GIS 摄影数据库查询示例**
- 解决方案方法，67–68
- 代码清单，68–70
- nznq 协议，70
- 用于图像的 PNG 文件，70, 71–72

## G

- `stream_open()` 函数，70–71
- `stream_read()` 函数，71
- `stream_tell()` 函数，71
- 数据库网站，67
- `glob()` 函数 (PHP)，60–61
- GMail 应用程序 (Google)，273
- GNU 缩进风格，215

### GRANT 命令 (MySQL)
- 用于 Apache 访问凭证，149
- 创建列级权限，95
- 为特定表创建权限，95
- 用于极度受限的访问，96
- 授予所有权限，96
- 授予有限的表级权限，96
- IDENTIFIED BY 短语，96
- ON 子句，95
- 用于 PHP 身份验证示例，166
- 权限，94–95
- 语法，94
- TO 子句，95

## H

### httpd.conf 文件
- 启用 SSL 功能，157
- HostnameLookups 选项，212
- KeepAlive 选项，212
- KeepAliveTimeout 选项，212
- MaxClients 选项，211
- MaxKeepAliveRequests 选项，212
- MaxRequestsPerChild 选项，211
- MaxSpareServers 选项，212
- 用于 mod_auth_mysql，151–152
- 用于 mod_dav，158
- 用于 mod_deflate (Apache)，146–147
- 用于 mod_ssl，155
- 与性能相关，211–212
- StartServers 选项，212
- 用于 WebDAV 身份验证，159

- 硬盘，与性能相关，211
- 用于性能提升的硬件改进，210–211
- 隐藏框架技术以避免页面刷新，275–276
- 隐藏 IFRAME 技术以避免页面刷新，276–277

### .htaccess 文件
- 用于 mod_auth_mysql，151–152
- 与性能相关，213
- 用于关闭 register_globals 指令，179
- 用于 WebDAV 身份验证，159

- HTML_CSS PEAR 包，192–193
- HTML_Page PEAR 包，192–193
- HTML_QuickForm PEAR 包，193–194
- HTML_Table PEAR 包，194–195
- HTTP GET 值，345
- HTTP POST 值，345

## I

- IFRAME 元素，隐藏，276–277
- 图像源技巧以避免页面刷新，275

### `imagealphaBlending()` 函数
- (`ImageResize` 类)，248

### GD 库的 ImageCaption 类
- 代码列表，250–251
- `imageline()` 函数，253–254
- `imagegettext()` 函数，253
- `process()` 方法，252–253
- `imagecopy()` 函数 (`ImageLogo` 类)，257
- `imagecopymerge()` 函数 (GD 库)，257
- `imagecopyresampled()` 函数
  - (`ImageResize` 类)，248
- `imagecopyresized()` 函数 (`ImageResize` 类)，248
- `imageline()` 函数 (`ImageCaption` 类)，253–254

### GD 库的 ImageLogo 类
- 代码列表，254–255
- `imagecopy()` 函数，257
- `process()` 方法，256–257

### GD 库的 ImageResize 类
- 代码列表，245–246
- `imagealphaBlending()` 函数，248
- `imagecopyresampled()` 函数，248
- `imagecopyresized()` 函数，248
- `imagesavealpha()` 函数，248
- `process()` 方法，247–248

- GD 库的 ImageRotate 类，249–250

### `imagesavealpha()` 函数
- `ImageResize` 类，248
- `WebImage` 类，244

- `imagerotate()` 函数 (`ImageCaption` 类)，253

- `implements` 关键字 (PHP)，36, 37

- 编码的缩进标准，214–217

- 索引透明度，244

- `info` 命令 (PEAR 管理器)，185

### 继承 (PHP)
- 抽象类与，7–8, 34–35
- 描述，31
- `extends` 关键字与，31–33
- `final` 关键字与，6, 33
- 语言翻译，340–341
- `parent::` 引用，33–34
- 在子类中重新定义属性和方法，32–33
- `static` 关键字与，7

- `ini_get()` 函数 (PHP)，109

### `ini_get_all()` 函数 (PHP)
- 访问指令的值，115
- 概述，109, 110
- 在 `XMLConfigProcessor.php` 类中，126, 127

- `ini_set()` 函数 (PHP)，114–115, 127–128

- 初始化属性 (PHP)，21

### 内连接 (MySQL)
- 表别名，78–79
- 按评估顺序链式处理，79
- 逗号分隔的表列表用于，79–81
- 定义，78
- 局限性，81
- 与外连接结合使用，82
- 语法，78
- 表前缀用于，78–79
- 配合 USING 语句使用，79
- 配合 WHERE 子句使用，79, 80, 81

- Innobase Oy 公司，88

### InnoDB 表 (MySQL)
- 优点，88–89



- 将 `MyISAM` 表转换为，90
- 转换为 `MyISAM` 表，93
- 从头创建表，89
- `InnoDB` 存储引擎的开发，88
- 缺点，89
- 外键约束，88–89, 90–93
- `INSERT` 语句 (`MySQL`)，75–76
- 安装
  - `APC` 缓存引擎，288
  - DocuWiki 微内容管理系统，326
  - eAccelerator 缓存引擎，291
  - ExponentCMS，309–310
  - JPCache 缓存引擎，296–297
  - MediaWiki 微内容管理系统，325
  - memcached 缓存引擎，300–301
  - Ming 扩展 (`PHP`)，263
  - mod_auth_mysql (`Apache`)，150–151
  - `PEAR` 包，186
  - phpWebsite CMS，315–317
  - Serendipity 博客微内容管理系统，324
  - TikiWiki CMS，318–320
  - WordPress 博客微内容管理系统，323
  - Xoops CMS，312–313
  - Zend Optimizer 缓存引擎，294–295
- 实例化
  - 类，22–23
  - `SWFMovie` 对象 (`Ming`)，263
- `interface` 关键字 (`PHP`)，36
- 接口 (`PHP`)
  - 描述，35
  - 使用 `extends` 关键字，36–37
  - 实现，36, 37
  - 语言翻译，342–343
  - 一个类对应多个接口，37
  - 概述，35–37
  - `PHP5` 变更，5
  - 用途，35
- 互联网编号分配机构，72
- 互联网资源
  - `AJAX` 信息，285
  - Apache mod_ssl 信息，157
  - `APC` 缓存引擎，288
  - Auth_HTTP `PEAR` 包信息，188
  - CMS 资源，327–328
  - CPAIN_，283
  - CVS 版本控制系统，351
  - DocuWiki 微内容管理系统，326
  - Drupal CMS，321
  - eAccelerator 缓存引擎，291
  - ExponentCMS，309, 310
  - Fileinfo `PECL` 包，196
  - `PHP` 手册中的 `GD` 章节，263
  - Google 的 Gmail 应用程序，273
  - 互联网编号分配机构，72
  - JavaWebStart 网站，351
  - JPCache 缓存引擎，296, 300
  - JSPAN，283
  - 新西兰土地信息网，67
  - Mambo CMS，321
  - MediaWiki 微内容管理系统，325
  - memcached 缓存引擎，300, 301
  - 微内容管理系统，323, 324, 325, 326, 327
  - Ming 信息，263
  - MyBench 工具，350
  - MySQL Administrator 工具，348
  - MySQL Query Browser 工具，349
  - MySQL Super Smack 工具，350
  - PDF 开源库，233
  - PDFLib 扩展 (`PHP`)，233, 234
  - PDFLib Lite 扩展 (`PHP`)，234
  - `PDO` `PECL` 包，196, 197
  - `PEAR` 配置变量，185
  - `PEAR` 数据库包，191
  - `PEAR` 管理器命令，184
  - `PEAR` 包，195
  - `PEAR::DB` 包，187
  - PEPr 网站，184
  - `PHP` Wiki 网站，196
  - `PHP-Nuke` CMS，321
  - phpWebsite CMS，315
  - Postruke CMS，322
  - Sajax 信息，282
  - 与安全性相关的网站，182
  - Serendipity 博客微内容管理系统，324
  - SourceForge 网站，263, 353
  - SQLite 信息，17
  - Subversion 版本控制系统，351
  - Tidy 库，17
  - TikiWiki CMS，318
  - Umbrello UML 工具，353
  - WordPress 博客微内容管理系统，323
  - WROX 网站，76
  - Xdebug `PECL` 包，197
  - XOOPS，312
  - Zend Optimizer，295
- 插值，基准测试速度，201–205
- `iterator` 类 (`PHP`)，5
- 迭代器 (`PHP`)，5–6

## J
- Java。参见 *语言翻译*
- JavaDoc 风格注释，220
- JavaScript。另见 *AJAX (Asynchronous JavaScript and XML)*
  - 隐藏框架技术，275–276
  - 图像源技巧，275
- JavaWebStart 网站，351
- JPCache 缓存引擎
  - 配置，297–299
  - 安装，296–297
  - 与其他缓存引擎配合使用，305
  - 概述，296
  - 移除，300
  - 适用场景，305
  - 网站，296, 300
- JSPAN `AJAX` 库，283
- JSP。参见 *语言翻译*

## K&R（Kernighan 和 Ritchie）缩进风格
- K&R（Kernighan 和 Ritchie）缩进风格，215、216、217
- 停止子类化，342
- 抛出异常，344–345
- 变量声明，330
- 变量类型定义，330

## L
- Land Information New Zealand 网站，67
- **语言翻译**
  - 抽象类声明，341–342
  - 数组创建，331
  - 数组元素引用，331
  - 基类定义，338
  - 在同类中调用方法，338–339
  - 调用父类方法，341
  - 类构造函数，339
  - 类析构函数，339–340
  - 类继承，340–341
  - 类属性声明，338
  - 类使用接口，343
  - 类可见性关键字，337
  - 注释，329
  - 条件求值，331–332
  - 常量声明，330
  - 异常处理，344
  - 函数/方法声明，336
  - 使用命名空间对类进行分组，337
  - HTTP GET 值，345
  - HTTP POST 值，345
  - 包含外部文件，343–344
  - 接口声明，342–343
  - 循环，进入下一轮，336
  - 循环，do…while，334
  - 循环，for，334
  - 循环，foreach，335
  - 循环，终止，335
  - 循环，while，333
  - 多选选择，332–333
  - 对象创建，340
  - 返回函数值，336–337
  - 服务器变量，345–346
  - 静态类方法的使用，340
- **左外连接 (`MySQL`)，81、84**
- **load() 函数 (`WebImage` 类)，243–244**
- **日志文件**
  - 用于监控日志的 `emailException` 类，3–4
  - 文件访问记录器示例，63–67
  - 用于 URL 重写 (`Apache`)，143–144
- **logo() 方法 (`WebImage` 类)，255–256**
- **循环**
  - 不需要循环的数组函数，48
  - 使用 `array_walk()` 函数避免循环，49、51–52
  - for 循环，48、335
  - foreach 循环，48、49、51–52、335
  - 语言翻译，333–336

## M
- Mac OS，为其设置 WebDAV，163
- Macromedia Flash 与 Ming 对比，263
- **魔术方法 (`PHP`)**
  - 用于访问未显式定义的方法和属性，37
  - `__call()`，8–9、38
  - `__construct()`，6、25–26、37
  - `__destruct()`，6、26–27、37
  - `__get()`，8、38–39
  - 用于重载，8–9
  - 概述，37
  - `__set()`，8、38–39
  - `__sleep()`，39、40–43
  - `__toString()`，43–44
  - `__wakeup()`，40–43
- **魔术引用 (`PHP`)**
  - 检查 `php.ini` 设置，113
  - 禁用，106、113
  - 概述，112–113



- 相关 `php.ini` 设置，106、113
- `维护数据库 (MySQL)`，103–104
- `Mambo CMS`，321
- `MediaWiki` 微型 CMS，325–326
- `memcached` 缓存引擎
  - 守护进程，300
  - 安装，300–301
  - `Memcache` 对象方法，301–303
  - 其他缓存引擎与之对比，305
  - 概述，300
  - 相关 PECL 模块，301
  - 移除，304
  - 使用，301–304
  - 相关网站，300、301
- `内存 (RAM)`
  - 性能与内存的关系，200、210–211
  - 一系列数组函数与内存的关系，59–60
- `方法 (MySQL)`
  - 过程式调用，13
  - `mysqli` 类，13–14
  - `mysqli_result` 类，16
  - `mysqli_stmt` 类，15
- `AJAX` 接口的方法，277–278
- `方法 (PHP)`。参见 `函数 (PHP)`；`魔术方法 (PHP)`；特定方法和函数
  - 抽象方法，8
  - 定义，21
  - 描述，20、21
  - 配合 `final` 关键字使用，6
  - 语言翻译，336、338–339、340、341
  - 命名约定，221–222
  - 在子类中重新定义，32–33
  - 配合 `static` 关键字使用，7、27–28
  - 流封装方法，62–63
- `微型 CMS`
  - 博客包，322–324
  - `DocuWiki`，326
  - `MediaWiki`，325–326
  - 其他包，327
  - `Sereidipity`，324
  - `Wiki` 包，324–326
  - `WordPress`，323
- `Ming` 扩展 (`PHP`)
  - 相关 `Content-Type` 头部，268
  - 坐标系，264
  - 创建 `Flash` 显示，265–269
  - 帧，264
  - 安装，263
  - 与 `Macromedia Flash` 对比，263
  - 对象，263、264–265
  - 直接输出到浏览器，268–269
  - 概述，263–264
  - 简单示例，263–264
  - 幻灯片演示示例，266–269
  - 进一步信息网站，263
- `mod_alias (Apache)`，226
- `mod_auth_mysql (Apache)`
  - 优势，166
  - `AuthMySQLAuthoritative` 指令，154
  - `AuthMySQLDB` 指令，151、152
  - `AuthMySQLDBEnable` 指令，151、152
  - `AuthMySQLGroupCondition` 指令，154
  - `AuthMySQLGroupField` 指令，154
  - `AuthMySQLGroupTable` 指令，154
  - `AuthMySQLHost` 指令，152
  - `AuthMySQLNameField` 指令，153
  - `AuthMySQLPasswordField` 指令，151、152
  - `AuthMySQLPasswordField` 指令，153
  - `AuthMySQLPort` 指令，152
  - `AuthMySQLPwEncryption` 指令，151、153
  - `AuthMySQLSaltField` 指令，153
  - `AuthMySQLSocket` 指令，152
  - `AuthMySQLUser` 指令，151、152
  - `AuthMySQLUserCondition` 指令，153
  - `AuthMySQLUserTable` 指令，153
  - `AuthName` 指令，151
  - `AuthType` 指令，151
  - 相关数据库设置，149–150
  - 描述，129
  - 相关 `.htaccess` 文件，151–152
  - 相关 `http.conf` 文件，151–152
  - 安装，150–151
  - 最低安全指令要求，151
- `mod_dav (Apache)`，129、158
- `mod_deflate (Apache)`
  - 构建和启用，146
  - 使用进行内容压缩，146–148
  - `DeflateCompressionLevel` 指令，147
  - `DeflateFilterNote` 指令，148
  - `DeflateWindowSize` 指令，148
  - 描述，129
  - 有效性，148
  - 相关 `httpd.conf` 文件，146–147
- `mod_rewrite (Apache)`。参见 `URL` 重写 (`Apache`)
  - 功能，129
  - 将站点文档树与服务器文件系统解耦，226
  - 描述，129
  - 启用，130–131、133
  - `RewriteBase` 指令，143
  - `RewriteCond` 指令，139–143
  - `RewriteLog` 指令，143–144
  - `RewriteLogLevel` 指令，144
  - `RewriteRule` 指令，131–138
- `mod_spelling (Apache)`，129、144–145
- `mod_ssl (Apache)`，129、154–155。参见 `Apache` 中的 `SSL`（Secure Sockets Layer）
- `Moodle CMS`，327
- 乘法运算符，性能与乘法运算符的关系，200–201
- `MyBench MySQL` 工具，350
- `my.cnf` 配置文件 (`MySQL`)，88、100
- `MyISAM` 表 (`MySQL`)
  - 从 `InnoDB` 转换，93
  - 转换为 `InnoDB`，90
  - 作为默认存储引擎，88
- `MySQL`。参见 `SELECT` 语句 (`MySQL`)
  - 访问控制，93–100
  - 表的别名，78–79
  - `ALTER TABLE` 语句，87、90–91、92
  - 替代工具，347–350
  - 数据库分析，100–102
  - 与 `Apache` 身份验证集成，129、149–154、166
  - 基础，73–77
  - `columns_priv` 表，99、100
  - 创建备份，103
  - 创建数据库，74–75
  - 创建表，75、86–87
  - 交叉连接，81
  - `db` 表，98–99、100
  - 删除数据库信息，77、92
  - 示例数据库表，73–74
  - 外键约束，88–89、90–93
  - 全文搜索，86–88
  - 查询的 `/G` 终止符，86
  - `GRANT` 命令，94–96
  - 内连接，78–81、92
  - `InnoDB` 表，88–93
  - 向表中插入数据，75–76
  - 维护数据库，103–104
  - 监视，74
  - `MyBench` 工具，350
  - `my.cnf` 配置文件，88
  - `MyISAM` 表，88、90、93
  - `MySQL Administrator` 工具，347–348
  - `MySQL Query Browser` 工具，349–350
  - `MySQL Super Smack` 工具，350
  - 外连接，81–82
  - 查询多个表，77–86
  - 重新加载权限表，100
  - 从备份恢复，103–104
  - 检索数据库信息，76–77
  - `REVOKE` 命令，96–97
  - 服务器限制，100
  - 设置活动数据库，75
  - `SHOW COLUMNS` 命令，101
  - `SHOW CREATE TABLE` 命令，101–102
  - `SHOW DATABASES` 命令，102
  - `SHOW GRANTS` 命令，102
  - 启动命令行客户端，74
  - `tables_priv` 表，99、100
  - 联合，82–86
  - 更新数据库信息，77、91–92
  - `USE` 语句，75
  - 用户管理，93–100
  - `user` 表，97–98、99–100
  - 使用语句，79
  - `WHERE` 子句，79、80、81
- `MySQL Administrator` 工具，347–348
- `MySQL Query Browser` 工具，349–350
- `MySQL Super Smack` 工具，350

# 索引

- `mysqli` 类，13–15
- `MySQL`（`MySQL` 改进版），12–16



# N

- `mysqli_pconnect()` 函数，性能相关，231
- `mysqli_result` 类，16
- `mysqli_stmt` 类，15

## 命名空间

- 通过 `create_function()` 函数避免冲突，57–58
- 语言翻译，337
- 命名规范，220–222
- 嵌套，减少嵌套层级，217–220
- 网络连接，性能相关，210

- `new` 关键字（PHP），22–23
- `NO ACTION` 选项（MySQL），92

## NULL 值

- `array_map()` 函数的回调（PHP），50–51
- 与 InnoDB 外键约束相关（MySQL），89
- 用于联合查询中缺失的列（MySQL），84–86

- `create_function()` 函数名称中的 NULS，58

# O

- 面向对象编程。参见 OOP；PHP5 OOP

## 对象（PHP）

- 通过实例化类创建，20, 22–23
- 描述，20
- 语言翻译，340
- 与 OOP 中的现实世界对比 20
- 该对象的 `$this` 引用变量，23

- `ob_start('ob_gzhandler')` 函数，231
- `onreadystatechange` 属性（AJAX），278, 279

## OOP（面向对象编程）

另参见 PHP5 OOP
- PHP5 中的更改，1–9
- 与过程式编程的比较，19–20

- `open()` 方法（AJAX），277
- 开源运动，183

## 打开

- MySQL 命令行客户端，74
- 流（PHP），62, 63

- OpenSourceCMS 网站，327
- osCommerce CMS，327

## 外连接（MySQL）

- 通用形式，81
- 与内连接的组合，82
- 左连接与右连接，81
- 与联合查询的组合，84

- 输出缓冲，性能相关，227–228, 231
- `overload()` 函数与魔术方法（PHP），8
- `overrideMimeType()` 方法（AJAX），278

# P

- Pachev, Sasha（MySQL Super Smack 创造者），350
- `parent` 关键字（PHP），33–34
- 变量传递，PHP5 中的更改，1

## PDF（便携式文档格式）

- 开源库，233
- 用于 PDFLib 扩展，233–241
- 用于 PDFlib 函数，233
- PDF 简历生成器应用，238–241

- `pdf_close()` 函数（PDFlib），234
- `pdf_closepath()` 函数（PDFLib），236
- `pdf_fill()` 函数（PDFlib），236
- `pdf_findfont()` 函数（PDFlib），236
- `pdf_get_buffer()` 函数（PDFlib），237
- `pdf_get_value()` 函数（PDFlib），236, 237

## PDFLib 扩展（PHP）

- 完成 PDF 文件，237
- 配置，234
- 坐标系，237
- `drawHR()` 函数，236
- 字体函数，236–237
- 入门指南，234
- 辅助函数，235–237
- 路径函数，236
- PDF 简历生成器示例，238–241
- `pdf_close()` 函数，234
- `pdf_get_value()` 函数，236
- PDFlib 函数与此处的比较，233
- 用于此处的 PDFLIB-manual.pdf，234
- `pdf_new()` 函数，234
- `pdf_set_info()` 函数，235
- `pdf_show_xy()` 函数，237
- 此处的性能优势，233
- 必需元素，235
- 指定文档信息，235
- 网站，233, 234

## PDFlib 函数（PHP）

- 辅助函数，235–237
- 已移至 PECL，233
- 与 PDFlib 扩展的比较，233

- PDFlib Lite 扩展（PHP），234
- PDFLIB-manual.pdf，234
- `pdf_lineto()` 函数（PDFlib），236
- `pdf_moveto()` 函数（PDFlib），236
- `pdf_new()` 函数（PDFlib），234
- `pdf_setfont()` 函数（PDFlib），236
- `pdf_set_info()` 函数（PDFlib），235
- `pdf_show_xy()` 函数（PDFlib），237

- PDO PECL 包，196–197

## PEAR（PHP 扩展和仓库）

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
- 推荐的 Javadoc 风格注释，220
- 指定的 K & R 缩进风格，216
- 使用补丁保持更新，182
- 用于 phpWebsite CMS 的库，316
- 可用的包，187, 195–196
- PEAR 管理器，184–186
- `PEAR::Auth`，187, 188
- `PEAR::Cache` 和 `PEAR::Cache_Lite` 包，224–225
- `PEAR::DB` 包，187
- PEP r（PEAR 提案系统），184
- 使用已安装的包，187

- PEAR 提案系统（PEP r），184
- `PEAR::Auth` 包，187, 188
- `PEAR::Cache` 和 `PEAR::Cache_Lite` 包，224–225
- `PEAR::DB` 包，187

## PECL（PHP 扩展社区库）

- 提供的 APC 缓存引擎，287, 288
- 描述，184, 196
- Fileinfo 包，196
- 使用补丁保持更新，182
- memcached 缓存引擎模块，301
- 其中的 PDFlib 函数，233
- PDO 包，196–197
- Xdebug 包，197

- PEP r（PEAR 提案系统），184

## 性能

- `ab` ApacheBench 程序，208–209
- Apache Web 服务器改进，211–213
- 基准测试，定义，206–207
- 基准测试，字符串速度示例，201–205
- 缓存相关，223–227
- 检查数组大小相关，229
- 条件语句相关，230
- `echo` 与 `print` 相关，228–229
- 硬件改进，210–211
- 内存相关，200
- 乘法运算符相关，200–201
- NT4/Access 报表生成器轶事，200
- `ob_start('ob_gzhandler')` 相关，231
- 输出缓冲相关，227–228, 231
- 概述，231–232
- PDFlib 函数与 PDFLib 扩展相关，233
- PEAR Benchmarking 类，207–208
- 持久数据库连接相关，231
- PHP 编码标准，213–223
- 为性能规划程序，199–201
- 性能剖析，定义，207
- 正则表达式语法相关，230
- 释放资源相关，231
- 临时变量相关，229–230
- 字符串函数相关，230
- 字符串相关，201–205
- `top` 进程监控实用程序，208–210
- 性能调优的直观结果，206
- `unset()` 函数相关，230

- 持久数据库连接，性能相关，231

## PHP

另参见语言翻译；PHP5 OOP 更改和增强；PHP5 OOP
- 数组函数和回调，48–60
- 身份验证，166–177
- 自动版本和功能检查，116–128
- 动态更改配置，113–115
- 检查扩展及其属性，111–112
- 编码标准，213–223
- `glob()` 函数，60–61
- 列出已安装版本，108
- 获取当前运行时设置，108–113
- 脚本的输出压缩，148–149
- 在运行时检索配置设置，109–110
- 流，61–72



- 其中的函数多样性和数量，47

- PHP 配置。参见 `php.ini` 配置文件；运行时配置（PHP）

- PHP 扩展和仓库。参见 `PEAR`

- PHP 扩展社区库。参见 `PECL`

- PHP 扩展。另参见 `PEAR`（PHP 扩展和仓库）；`PECL`（PHP 扩展社区库）；特定扩展

  - `CURL`，271

  - `DOM`，16, 271

  - `extension_loaded()` 函数，111, 124, 125

  - 用于获取其信息的函数，111–112

  - `GD` 库，241–263

  - `Ming`，263–269

  - `PDFlib`，233–241

  - `PDFLib Lite`，234

  - `SimpleXML`，16, 269–270

  - `SOAP` 17，271

  - `Tidy` 库，17

  - PHP5 中新增的 XML 扩展，16–17

  - `XML`，16

  - `ZIP` 扩展，271

- PHP Wiki 网站，196

- `phpauthbasic.php` 脚本

  - `attempt_auth()` 函数，169–170

  - `check_login()` 函数，170–171

  - 代码列表，167–168

  - 为数据库连接定义的常量，169

  - 包含在标准 PHP 页面中，171

  - 测试，171

- `phpauthforms.php` 脚本，172–174

- `phpBB` CMS，327

- PHP 控制的身份验证

  - 与 Apache 控制的身份验证，166, 171

  - 创建身份验证数据库，166–167

  - Basic 身份验证的缺点，171

  - 表单身份验证，172–174

  - 其他访问限制，174–177

  - `phpauthbasic`，167–171

  - 用于表单身份验证的 `phpauthforms.php` 脚本，172–174

  - 测试 Basic 身份验证，171

### PHP5 更改和增强

- PHP5 更改和增强

  - `abstract` 关键字，7–8

  - 访问修饰符，6

  - 构造器和析构函数，6

  - 异常，1–5

  - `final` 关键字，6

  - 接口，5

  - 迭代器，5–6

  - 用于重载的魔术方法，8–9

  - `MySQLi` 扩展，12–16

  - 新函数，10–12

  - OOP 更改，1–9

  - 概述，1, 17

  - 变量传递，1

  - `php.ini` 配置文件更改，12, 107–108

  - `SQLite` 改进，17

  - `static` 关键字，7

  - `Tidy` 库扩展，17

  - XML 支持，16–17

### PHP5 OOP

- `abstract` 关键字，7–8

- 访问修饰符，6, 23–25

- 赋值与克隆，29–30

- 更改和增强，1–9

- 类基础，20–23

- 类常量，28–29

- 构造器，6, 25–26

- 定义类，20

- 析构器，6, 26–27

- 异常，1–5

- `final` 关键字，6

- 继承，31–35

- 实例化类，22–23

- 接口，5, 31, 35–37

- 迭代器，5–6

- 魔术方法，6, 8–9, 37–44

- 方法，21

- 概述，45

- 属性，20–21

- `static` 关键字，7, 27–28

- 可见性，23–25

### php.ini 配置文件

- 指令的访问值，115

- `allow_call_time_pass_reference` 指令，106, 115

- 用于 `APC` 缓存引擎，288–290

- `asp_tags` 指令，106

- 使用 `ini_set()` 更改指令，114–115

- `display_errors` 指令，106

- 用于 `eAccelerator` 缓存引擎，291–294

- `error_log` 指令，106

- `error_reporting` 指令，106

- 用于 `JPCache` 缓存引擎，297–299

- `log_errors` 指令，106

- `magic_quotes_gpc` 指令，106, 113

- `magic_quotes_runtime` 指令，113

- `mail.force_extra_parameters` 指令，107

- `MySQLi` 设置，12

- 输出压缩设置，149

- 用于 PHP 身份验证示例，171

- PHP5 改进，12, 107–108

- 推荐的配置指令，105–107

- `register_globals` 指令，105, 116

- `register_long_arrays` 指令，107

- 在运行时检索设置，109–110

- `safe_mode` 指令，171

- `session.hash_bits_per_character` 指令，108

- `session.hash_function` 指令，108

- `short_open_tag` 指令，106–107

- `variables_order` 指令，106

- 用于 `Zend Optimizer` 缓存引擎，295

- `zend.ze1_compatibility_mode` 指令，108

- `zlib.output_compression` 指令，107, 149

- `phpmychat` CMS，327

- `PHP-Nuke` CMS，321

- `phversion()` 函数，108, 126

## P

- `phpWebsite` CMS

  - 自定义默认设置，317

  - 默认功能，316–317

  - 安装，315–317

  - 用于 `PEAR` 库，316

  - 优缺点，317–318

  - 网站，315

- `pi()` 函数 (PHP)，29

- 便携式文档格式 (Portable Document Format)。参见 `PDF`

- `Postnuke` CMS，322

- `preg_grep()` 函数，53

- `preg_replace_callback()` 函数，53–55

- `PrestoPoll` CMS，327

- `print` 语句 (PHP)

  - 与 `echo` 语句的比较，228–229

  - 与 `__toString()` 魔术方法，44

- `private` 关键字 (PHP)，6, 23

- `privkey.pem` 文件 (SSL)，156

- `process()` 方法

  - `ImageCaption` 类，252–253

  - `ImageLogo` 类，256–257

  - `ImageResize` 类，247–248

  - `ImageRotate` 类，249–250

- `processConfig` 方法 (PHP)，118–119

- 处理器，性能与，210

- 性能分析，定义，207

- 属性 (MySQL)

  - `mysqli` 类，14–15

  - `mysqli_result` 类，16

  - `mysqli_stmt` 类，15

- 属性 (PHP)

  - `Circle` 类示例，21

  - 定义，20–21

  - 描述，20

  - 初始化，21

  - 语言翻译，338

  - 命名约定，221, 222

  - 真实与合成属性，221

  - 在子类中重新定义，32–33

  - 与 `static` 关键字，27

  - 这是引用变量，23

- `protected` 关键字 (PHP)，6, 24

- `public` 关键字 (PHP)，6, 23, 24

## Q

- 查询多个表 (MySQL)

  - 内连接，78–81

  - 外连接，81–82

  - 联合，82–86

- 引号 ("")
  - 用于函数名称内部
  - `set_exception_handler()`，5
  - 字符串速度与引号，201–205

## R

- RAM (内存)

  - 性能与，200, 210–211

  - 系列数组函数与，59–60

- `rar` 扩展 (PHP)，271

- Raymond, Eric S. (Jargon File 作者)，214

- `readdir()` 函数 (PHP)，61

- 读取

  - 目录 (PHP)，60–61

  - 流 (PHP)，62

- `readyState` 属性 (AJAX)，278, 279

- `create_function()` 函数，58

- `RecursionTerminator` 类 (PHP)，6

- `register_globals` 指令

  - 编码以减少被利用的可能性，179, 182

  - 漏洞利用，178–179

  - 用于关闭的 `.htaccess` 文件，179



- 与 `HTTP_REFERER` 值，174

- 推荐配置，105, 116

- **正则表达式**

  - 性能与，230

  - 与 `RewriteRule` 指令 (Apache 的 `mod_rewrite`)，133–134

- **用于配置检查器的 `reqs.xml` 文件 (PHP)，116**

- **`resize()` 函数 (`WebImage` 类)，246–247, 259**

- `responseText` 属性 (`AJAX`)，278

- `responseXML` 属性 (`AJAX`)，278

- `RESTRICT` 选项 (`MySQL`)，92

- `REVOKE` 命令 (`MySQL`)，96–97

## W

- `RewriteBase` 指令 (Apache 的 `mod_rewrite`)，143

- `RewriteCond` 指令 (Apache 的 `mod_rewrite`)

  - 基本格式，139

  - 将多行链接在一起，141

  - 比较和系统检查条件，141–142

  - 比较运算符，142

  - HTTP 头变量，139

  - 大小写不敏感或 NC 标志，142

  - 或下一个或 OR 标志，143

  - Request 变量，139–140

  - Server 变量，140

  - 特殊变量，140–141

  - Time 变量，140

  - 用法，139–142

  - 使用变量，141

- `RewriteLog` 指令 (Apache 的 `mod_rewrite`)，143–144

- `RewriteLogLevel` 指令 (Apache 的 `mod_rewrite`)，144

- `RewriteRule` 指令 (Apache 的 `mod_rewrite`)

  - 自动重定向 URL 到新目录，132

  - 基本格式，131

  - 链式或 C 标志，136

  - cookie 或 CO 标志，137

  - 启用 `mod_rewrite`，130–131, 133

  - env 或 E 标志，137

  - Forbid 或 F 标志，135

  - gone 或 G 标志，136

  - 用于人类友好的 URL，132–133

  - last 或 L 标志，136

  - next 或 N 标志，136

  - 大小写不敏感或 NC 标志，135

  - noescape 或 NE 标志，138

  - nosubreq 或 NS 标志，138

  - passthrough 或 PT 标志，138

  - proxy 或 P 标志，138

  - qsa ppend 或 QSA 标志，137

  - redirect 或 R 标志，135

  - 与正则表达式，133–134

  - 用于搜索引擎友好的 URL，132–133

  - skip 或 S 标志，137

  - 标志的语法，135

  - 用于，131–132

  - type 或 T 标志，137

  - 作为 PHP 脚本的类型检查层，134–135

  - 用法，131–135

## R

- 右外连接 (`MySQL`)，81

- `rotate()` 函数 (`WebImage` 类)，249

- 运行时配置 (`PHP`)。另见 配置检查器 (`PHP`)

  - 自动化版本和功能检查，116–128

  - 使用 `ini_set()` 更改指令，114–115

  - 动态更改，113–115

  - 禁用 magic quotes，113

  - 获取当前运行时设置，108–113

  - 移除时间限制，113–114

## S

- `SAJAX` (Simple AJAX Toolkit)，282–283

- `save()` 方法 (`WebImage` 类)，244–245

- `scandir()` 函数 (`PHP`)，61

- Schlossnagle, George (APC 创建者)，287

- `scratch` 变量，性能与，229–230

- 脚本 (`PHP`)

  - 用于 (Apache) 压缩，148–149

  - 作为类型检查层的 `mod_rewrite` (Apache)，134–135

  - 用于调试的 Xdebug PEGIL 包，197

- Secunia 网站，182

- 带 Apache 的安全套接字层。参见 带 Apache 的 SSL

- 安全性。参见 身份验证；站点安全

- `SELECT` 语句 (`MySQL`)

  - 与交叉连接，81

  - 用于全文搜索，87–88

  - `/G` 终止符用于垂直显示，86

  - 与内连接，78–81, 82

  - `stream_open()` 函数 (`PHP`)

    - 与外连接，81–82

    - 简单形式，76–77

    - 与联合，82–86

- `self` 关键字 (`PHP`)，7, 27–28, 50

- `send()` 方法 (`AJAX`)，278

- Sendmail 程序，3–4, 107

- Serendipity 博客 Micro CMS，324

- 服务器变量 (`PHP`)

  - 与访问控制，174–175

  - 语言翻译，345–346

  - `RewriteCond` 指令 (Apache 的 `mod_rewrite`)，140

- 会话，`php.ini` 设置，108

- `SET DEFAULT` 选项 (`MySQL`)，92

- `__set()` `__`魔术方法 (`PHP`)，8, 38–39

- `SET NULL` 选项 (`MySQL`)，92

- `set_error_handler()` 函数 (`PHP`)，1–5

- `set_exception_handler()` 函数 (`PHP`)，4–5

- `set_magic_quotes_runtime()` 函数 (`PHP`)，113

- `setRequestHeader()` 方法 (`AJAX`)，278

- `set_time_limit()` 函数 (`PHP`)，114

- Shape 类示例

  - 作为抽象类，34–35

  - Circle 类继承自，31–33

- Shockwave Flash 文件。参见 Ming 扩展 (`PHP`)

- `SHOW COLUMNS` 命令 (`MySQL`)，101

- `SHOW CREATE TABLE` 命令 (`MySQL`)，101–102

- `SHOW DATABASES` 命令 (`MySQL`)，102

- `SHOW GRANTS` 命令 (`MySQL`)，102

- Simple AJAX Toolkit (`AJAX`)，282–283

- SimpleXML 扩展 (`PHP`)

  - 概述，16, 269–270

  - `xpath()` 方法，125, 127

- 单引号 (`''`)，字符串速度与，201–205

- 站点安全。另见 身份验证

  - 使用 Apache 进行访问控制，165–166

  - 使用 PHP 进行访问控制 166–177

  - 用于代码/同行评审，182

  - 跨站脚本攻击 (XSS)，180–181

  - 通过补丁保持更新，181–182

  - `register_globals` 漏洞利用，178–179, 182

  - 社会工程学与，182

  - SQL 注入攻击，179–180, 182

  - 网站攻击，178–181

  - 用于进一步信息的网站，182

- 斜杠 (`/`)

  - `/G` 终止符用于 MySQL 查询，86

  - 在 PHP URL (`://`) 方案部分后，72

- `__sleep()` `__`魔术方法 (`PHP`)，39, 40–43

- `SOAP` 扩展 (`PHP`)，17, 271

- SourceForge 网站，263, 353

- 拼写检查 URL (Apache)，144–145

- `SPL` (Standard Public Library)，5

- SQL 注入攻击，179–180, 182

- `SQLite`，17

- 带 Apache 的 SSL (Secure Sockets Layer)

  - 检查是否在 Apache 中启用了 SSL，154

  - 创建 SSL 网站目录，157

  - 创建自签名证书和密钥，155–156

  - 在 Apache 中动态启用 SSL，155

  - 在 `httpd.conf` 中启用 SSL 功能，157

  - 进一步信息，157

  - 用于测试的信息文件，157

  - 用于的 `mod_ssl`，129, 154–155



- `private_key.pem` 文件，156

- 移除密码短语，156

- 在 Apache 中静态启用 SSL，154

- `testsuite.csr` 文件，156

- 测试，157

- 用于 443 端口的 VirtualHost 部分，157

- `ssl.conf` 文件，157

- **Standard Public Library (SPL)**，5

- **static** 关键字 (PHP)，7, 27–28

- **status** 属性 (AJAX)，278, 279

- `stream_close()` 函数 (PHP)，63, 67

- `stream_eof()` 函数 (PHP)，63

- `stream_open()` 函数 (PHP)

  - 文件访问日志记录器示例，67

  - GIS 摄影数据库查询示例，70–71

  - 概述，62, 63

## `stream_read()` 函数 (PHP)

- 文件访问日志记录器示例，67

- GIS 照片数据库查询示例，71

- 概述，62

## 流 (PHP)

- 构建流包装器，62–63

- 定义，61–62

- 文件访问日志记录器示例，63–67

- GIS 数据库查询示例，67–72

- PHP 中仅允许字节流，62

- 概述，61–62

- 用于命名流资源的 URL 系统，72

- 包装器方法，62–63

## `stream_tell()` 函数 (PHP)

71

## `stream_wrapper_register()` 函数 (PHP)

62

## `stream_write()` 函数 (PHP)

63, 67

## 字符串 (PHP)

- 速度基准测试，201–205

- 性能与字符串函数，230

- `__toString()` 魔术方法，43, 44

## `stripSlashes()` 函数 (PHP)

113

## 子类化

- 停止的语言翻译，342

- 在子类中重新定义属性和方法，32–33

- Subversion 版本控制系统，350–351

- `SWFAction` 对象 (Ming)，264

- `SWFBitmap` 对象 (Ming)，264, 267

- `SWFButton` 对象 (Ming)，264, 268

- `SWFDisplayItem` 对象 (Ming)，265

- `SWFFill` 对象 (Ming)，265

- `SWFFont` 对象 (Ming)，265

- `SWFGradient` 对象 (Ming)，265

- `SWFMorph` 对象 (Ming)，265

- `SWFMovie` 对象 (Ming)，263, 264, 267

- `SWFShape` 对象 (Ming)，265, 267, 268

- `SWFSprite` 对象 (Ming)，264, 265, 266–267

- `SWFText` 对象 (Ming)，265

- `SWFTextField` 对象 (Ming)，265

- `switch` 语句，语言翻译，332–333

- 合成属性命名规范，221

## T

- 避免使用制表符进行缩进，216–217

- `tables_priv` 表 (MySQL)，99, 100

- `testcert_csr` 文件 (SSL)，156

- `$this` 引用变量 (PHP)，23, 50

- Tidy 库扩展 (PHP)，17

- TigriS.org 社区，351

## TikiWiki CMS

- 自定义默认设置，320–321

- 默认功能，318–319

- “非活动”功能，319–320

- 安装，318–320

- 优点与缺点，321

- 网站，318

- `top` 进程监控工具，208–210

- `__toString()` 魔术方法 (PHP)，43, 44

- `try/catch/throw` 代码块 (PHP)

    - 语言翻译，344–345

    - 针对 `pdf_new()` 函数，234

    - 语法，2

## U

- Umbrello UML 工具，352–353

## UML 图

- ArgoUML 工具，351–352

- 概述，351

- Umbrello 工具，352–353

## 并集 (MySQL)

- 不同长度的列列表及其相关说明，83

- 交叉连接与并集的区别，82

- 描述，82

- 不同名称的表列及其相关说明，83

- 查询的 `/G` 终止符，86

- 与连接组合使用，84

- 缺失列的 NULL 值，84–86

## Web CMSs

- `unset()` 函数，性能与，230

- `UPDATE` 语句 (MySQL)，77, 91–92

- URL 重写 (Apache)

    - 自动重定向 URL 到新目录，132

    - 避免自动转义，138

    - 将 `mod_rewrite` 与其他模块结合使用，138

    - 控制日志记录的详细程度，144

    - 启用 `mod_rewrite`，130–131, 133

    - 强制请求通过代理模块，138

    - 用于对人友好的 URL，132–133

    - 使模式不区分大小写，135

    - 覆盖 MIME 类型，137

    - 保留查询字符串，137

    - `RewriteBase` 指令，143

    - `RewriteCond` 指令，139–143

    - `RewriteLog` 指令，143–144

    - `RewriteLogLevel` 指令，143

    - `RewriteRule` 指令，131–138

    - 用于对搜索引擎友好的 URL，132–133

    - 发送 HTTP 403 Forbidden 响应，135

    - 发送 HTTP 410 Gone 响应，136

    - 设置 cookies，137

    - 设置环境变量，137

    - 跳过规则，137, 138

    - 指定基础路径或前缀路径，143

    - 指定用于处理的日志文件，143–144

    - 在规则列表开头开始处理过程，136

    - 在成功匹配后停止处理，136

    - 考虑内部子请求，138

    - 测试字符串是否符合模式或条件，139–143

    - 作为 PHP 脚本的类型检查层，134–135

    - 使用代码块，136

    - 使用带有 HTTP 状态码的 format redirect，135

- URLs。另见 URL 重写 (Apache)

    - 命名流资源的指南，72

    - PHP 对此的约定，72

    - 拼写检查 (Apache)，144–145

- `USE` 语句 (MySQL)，75, 149

- 用户管理 (MySQL)

    - `GRANT` 和 `REVOKE` 的替代方案，97–100

    - 用于此的 `columns_priv` 表，99, 100

    - 用于此的 `db` 表，98–99, 100

    - 用于此的 `GRANT` 命令，94–96

    - 概述，93–94

    - 重新加载权限表，100

    - 用于此的 `REVOKE` 命令，96–97

    - 用于此的 `tables_priv` 表，99, 100

    - 用于此的 `user` 表，97–98, 99–100

- 表 (MySQL)，97–98, 99–100

- 内部连接的 `USING` 语句 (MySQL)，79

## V

- `var` 关键字 (PHP4)，24

- 变量 (PHP)

    - 按值赋值与按引用赋值，29

    - 克隆，29–30

    - 语言翻译，330

    - 命名规范，220, 222

    - 传参，PHP5 对此的更改，1

    - 此的 `php.ini` 设置，105, 106

- VBScript。另见语言翻译

- 版本控制系统，350–351

- `visibility` 关键字。另见访问修饰符 (PHP)

## W

- `_wakeUp()` 魔术方法 (PHP)，40–43

- Web CMSs。另见 CMSs (内容管理系统)

    - 全方位 Web CMSs，309–322

    - 描述，308

    - Drupal，321

    - ExponeCMS，309–312

    - Mambo，321

    - 微型 CMSs，322–328

    - 开源包，308

    - PHP-Nuke，321

    - `phpWebsite`，315–318

    - Postnuke，322

    - TikiWiki，318–321

    - XOOPS，312–315

- WebCalendar CMS，327

- WebDAV (基于 Web 的分布式创作和版本控制)

    - 身份验证，159

    - 将 `mod_dav` 构建为共享对象，158



- 静态构建 `mod_dav`，158

- 检查 `mod_dav` 是否已启用，158

- 描述，158

- 用于文件存储库的目录，158

- 支持它的编辑器，159

- `mod_dav` 的 `httpd.conf` 文件条目，158

- Mac OS 设置，163

- Windows 2000/XP 设置，159–162

- 用于 GD 库的 WebImage 类

    - 功能，241

    - `caption()` 方法，251–252

    - 代码列表，241–243

    - `display()` 方法，244

    - `imagesavealpha()` 函数，244

    - `load()` 函数，243–244

    - `logo()` 方法，255–256

    - 公共属性，243

    - `resize()` 函数，246–247, 259

    - `rotate()` 函数，249

    - `save()` 方法，244–245

    - `while` 循环，语言风格，333

- Whitesmith’s 缩进风格，215

- wiki 微型 CMSs

    - DocuWiki，326

    - MediaWiki，325–326

    - 术语起源，324

    - 概述，323–324

    - Windows 2000/XP，用于此的 WebDAV 设置，159–162

- WordPress 博客微型 CMS，323

- 写入流 (PHP)，63

- WROX 网站，76

## X

- Xdebug PECL 包，197

- XHTML，其 AJAX 用法，273

- XML。另见 AJAX (异步 JavaScript 和 XML)

    - 配置检查器 (PHP)，116–128

    - 更多信息，285

    - PHP5 对此的支持，16–17

    - SimpleXML 扩展 (PHP)，16, 125, 127, 269–270

    - `XMLConfigProcessor.php` 类

        - `checkConfig()` 函数，126–128

        - `checkConfigAccess()` 方法，124

        - `checkDeps()` 方法，124

        - `checkExtensions()` 方法，125

        - `checkPHP()` 方法，125–126

        - 代码列表，119–122

        - 构造函数，122–123

        - 其中的 `extension_loaded()` 函数，124, 125

        - 其中的 `ini_get_all()` 函数，126, 127

        - 其中的 `ini_set()` 函数，127–128

        - `$message` 属性，122

        - 其中的 `phpversion()` 函数，126

        - `process()` 方法，123

        - 其中的 SimpleXML `xpath()` 方法，125, 127

        - `version_compare()` 函数，126

        - `$xml` 属性，122

        - `$xmlfile` 属性，122

- XMLHTTP 和 XMLHttpRequest 接口 (AJAX)

    - 更多信息，285

    - 处理 ReadyStateChange 事件，280

    - 处理响应，280–282

    - 历史，277

    - 方法，277–278

    - 属性，278–279

    - 处理浏览器差异，279–280

- XOOPS (可扩展对象门户系统)

    - 自定义默认设置，314–315

    - 默认功能，313

    - 安装，312–313

    - 可用的其他模块，313

    - 优点与缺点，315

    - 网站，312

- `xpath()` 方法 (SimpleXML)，125, 127

- XSL 扩展 (PHP)，16

- XSS (跨站脚本)，180–181

## Z

- Zawodny, Jeremy (MySQL 专家)，350

- ZenCart CMS，327

- Zend Engine 1，其 `php.ini` 设置，108

- Zend Optimizer 缓存引擎

    - 配置，295

    - 安装，294–295

    - 其他缓存引擎及与其的配合，305

    - 概述，294

    - 移除，296

    - 适用场景，305

    - 网站，295

- ZIP 扩展 (PHP)，271

- Zlib 库 (PHP)，107

![image](img/fd2e7361878181c2b12e30301ff3e182_405_0.png)

## 随时随地携带你的图书馆。

现在，无论你在哪里，都可以在线访问 70 多本完整的 Wrox 书籍！订阅 Wrox 参考图书馆后，所有的图表、说明、屏幕截图和代码示例都可供使用。为了随时随地获取答案，请访问 `wrox.books24x7.com` 并立即订阅！

### 查找以下主题的书籍

- ASP.NET

- C#/C++

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
