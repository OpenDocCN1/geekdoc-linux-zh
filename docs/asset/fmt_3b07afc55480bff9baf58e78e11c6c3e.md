
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
