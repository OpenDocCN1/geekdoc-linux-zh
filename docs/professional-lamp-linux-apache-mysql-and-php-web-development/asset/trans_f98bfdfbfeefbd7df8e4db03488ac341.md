
# 第 1 章

E_CORE_ERROR、E_CORE_WARNING、E_COMPILE_ERROR、E_COMPILE_WARNING 以及大部分 E_STRICT 错误。此外，如果错误发生在 set_error_handler() 函数脚本之前，该函数将永远不会被调用。PHP5 带来了处理异常的新框架。

## 尝试/捕获/抛出

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

## 内置异常类

你刚才看到的 Exception 类也是 PHP5 的一项改进，并且是默认内置的。有了 PHP5，你现在可以获取已抛出异常的信息，并使用这些数据做出适当的响应。处理并存储该数据的内置异常类如下所示：

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

仔细查看 Exception 类：

| 成员或方法名称 | 代表内容 |
| :--- | :--- |
| $message | 异常消息；默认值可以设置为任何你喜欢的内容 |
| $code | 用户定义的代码 |
| $file | 发生错误的文件名 |
| $line | 发生错误的行号 |
| getMessage() | 返回 $message |
| getCode() | 返回 $code |
| getFile() | 返回 $file |
| getLine() | 返回 $line |
| getTrace() | 返回一个数组，其中包含来自 debug_backtrace() 函数的信息 |
| getTraceAsString() | 返回与 getTrace() 函数相同的结果，但以格式化字符串形式返回 |
| toString() | PHP5 魔术方法，允许在与 print 或 echo 配合使用时将对象格式化为字符串 |

在上面的 try/catch/throw 示例中，我们使用了内置异常类中的 getMessage() 函数来返回并显示错误消息内容。

### 扩展内置异常类

显然，内置异常类是该类的最通用形式，虽然它在许多情况下非常有用，但有时你可能希望以更具体处理异常。例如，在发送邮件时，如果收件人的电子邮件地址为空，你并不会收到 PHP 错误。除非你监控你的 sendmail 日志，否则你可能不会知道你的邮件未被发送。这将是非常有用的信息，因此你可以使用 extends 关键字轻松地扩展内置类，如下所示：

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

### set_exception_handler() 函数

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

## 迭代器

通过标准公共库（SPL），你可以访问一整套新的类和接口，允许你操作和利用迭代器。SPL 是一个编译并默认可在 PHP 中使用的扩展，它基本上是一个供你使用的接口和类库。下一节讨论 `Iterator` 类本身。你会注意到许多函数与数组函数相似。

### 主要迭代器接口

`Iterator` 类是一个内置接口，允许你遍历任何可以用 `foreach()` 语句遍历的东西——例如，文件目录、查询结果或数据数组。它具有某些固有函数：

- `Iterator::current()`: 返回当前元素。
- `Iterator::key()`: 返回当前元素的键。
- `Iterator::next()`: 将指针移动到下一个元素。
- `Iterator::valid()`: 验证在调用 `next()` 或 `rewind()` 后是否存在元素。

通过预定义通用的 `Iterator` 功能，这些都有助于你使用迭代使代码更强大、更高效。`Iterator` 接口最重要的一点是它是其他 SPL 类的构建块之一。

### 其他迭代器类

以下部分简要描述了一些继承自 `Iterator` 类的主要类。有关以下任何类的更详细信息以及更全面的列表，可以在在线 SPL 文档中找到：`http://www.php.net/~helly/php/ext/spl/main.html`。

### DirectoryIterator

顾名思义，`DirectoryIterator` 是一个实现了 `Iterator` 的 `Iterator` 类，允许你处理文件目录。此类中包含一组强大的函数，可以获取每个文件的信息，例如修改时间和日期、文件大小、文件类型、文件所有者、文件的完整路径以及与文件关联的权限（仅举几例）。

