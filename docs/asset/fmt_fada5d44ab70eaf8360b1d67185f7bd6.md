
## 1. PHP错误处理机制

所有PHP错误处理函数都以相同的参数调用：

- 第一个参数指示遇到问题的严重程度。`$severity`将是以下之一：
  - `E_USER_ERROR`
  - `E_USER_WARNING`
  - `E_USER_NOTICE`
  - `E_WARNING`
  - `E_NOTICE`
- 第二个参数（`$errstr`）包含错误的文本。
- 第三个和第四个参数（`$filename`和`$lineeno`）指示发生的地方。
- 最后一个参数是一个包含错误发生函数中的变量名和值的数组。

你真正想要的是一个在出现问题时通过电子邮件主动通知你的PHP程序。

你可以使用错误处理函数提供的值来解决问题，但有时你需要更多细节。列表54-4中的`err_handler()`函数提供了错误消息、文件名和行号，但列表54-5显示了新版本的`err_handler()`，它提供了更多细节。当你调试PHP代码时使用新版本，当事情看起来运行良好（这是一个技术术语）时使用原始版本。

列表54-4显示了一个短的PHP函数，它可以拦截错误、警告和非正式消息，并将描述问题的电子邮件发送给你选择的收件者。

## 2. 列表54-4：从PHP发送错误消息

```php
function my_err_handler($severity, $errmsg, $filename, $lineno, $context) {

    $err_text = "At " . date("Y-m-d H:i:s (T)");

    $err_text .= " an error occurred at line " . $lineno . ".";

    $err_text .= " of file " . $filename . "\n\n";

    $err_text .= " The text of the error message is:\n";

    $err_text .= $errmsg . "\n";

    mail("my-email@example.com", "PHP Script Error", $err_text);

}
```

## 3. 列表54-5：从PHP发送详细错误消息

```php
function my_err_handler($severity, $errmsg, $filename, $lineno, $context) {

    $err_text = "At " . date("Y-m-d H:i:s (T)");

    $err_text .= " an error occurred at line " . $lineno . ".";

    $err_text .= " of file " . $filename . "\n\n";

    $err_text .= " The text of the error message is:\n";

    $err_text .= $errmsg . "\n";

    ob_start(); // 将输出重定向到临时缓冲区

    print_r(debug_backtrace()); // 生成（并格式化）栈跟踪

    $err_text .= " Stack trace follows:\n";

    $err_text .= ob_get_contents(); // 将栈跟踪添加到邮件正文中

    ob_end_clean(); // 并清理临时缓冲区

    mail("my-email@example.com", "PHP Script Error", $err_text);

}
```

## 4. 第55章 在Perl中使用DDD图形化调试技术

通过以下方式节省时间：

- 使用`DDD`调试`Perl`程序
- 使用数据窗口跟踪变量值
- 使用断点监控你的代码
- 使用回溯日志（`Backtrace log`）查看你的堆栈内容

`Perl`经常被称为“互联网的粘胶带”。如果你需要编写实用程序或脚本，`Perl`是一个你可以信赖的标准。在使用`Perl`时，如何节省时间呢？使用一个好的调试器！除非你的代码在第一次运行时就完美无缺，否则你将花费时间在调试器窗口后，解决脚本中的各种小问题。

`Linux`提供了优秀的开源调试器`DDD`（数据显示调试器）。`DDD`是不同命令行调试器的图形化前端，它通过明确和简化程序调试过程来为你节省时间。`DDD`不仅可以调试`Perl`，还可以调试`C`、`C++`、`Java`和其他编程语言。

你可以使用`DDD`中的源代码窗口来一目了然地查看源码；你甚至可以定义断点并看到程序将停止的小标记。`DDD`还提供了一个易操作的按钮界面来单步执行程序，进入查看完整代码或跳过子程序。

通过`DDD`，你可以为程序中的变量创建图形化显示，并在单步执行程序时更改它们的值。`DDD`通过提供有关程序状态的易读信息来帮助你完成调试任务。易于访问的帮助菜单确保了你不仅拥有技术信息，还有关于调试程序的建议（以防你卡住）。

市面上有很多关于`Perl`编程语言的优秀书籍。我们能想到的最节省时间的方法就是对一种开源调试器进行快速介绍，它将节省你的时间并让你的生活变得轻松。在这项技术中，我们为你介绍`DDD`，它是对过去命令行调试器的一种巨大改进。

## 5. 使用DDD调试Perl代码

如果你编写过许多`Perl`程序，你可能已经熟悉`Perl`的源码级调试器。要在`Perl`调试器的控制下运行程序，请使用`-d`选项，如下所示：

```bash
$ perl -d program.pl
```

点击并听到运转声后，调试器出现并等待命令。如果你输入`h`并按回车，你将会看到一个有用但令人生畏的页面，如列表55-1所示。

不要慌；即使你是一个经验丰富的`Perl`老兵（而且你有足够的心理阴影证明这一点），你也会喜欢`DDD`，这个数据显示调试器。`DDD`是许多不同调试器（`DB`、`DBX`、`Perl`调试器，甚至是`Python`调试器）的图形前端。

## 6. 安装并启动DDD

大多数发行版都包含`DDD`，因此安装和运行非常简单。要安装并启动`DDD`调试器，请按照以下步骤操作：

1. 打开终端并使用`su`命令赋予自己超级用户权限。

2. 插入并挂载发行媒体。

3. 移动到包含`RPM`包的目录并输入以下命令：

```bash
# rpm -Uhv ddd-version.rpm
```

4. 要在`DDD`调试器的控制下运行程序，请使用此命令：

```bash
$ ddd --perl /usr/bin/perl.xpl
```

`DDD`打开，在主窗口前显示“每日提示”（`Tip of the Day`）和一个信息窗口。

如果你的发行媒体没有包含`DDD` RPM包，可以从`www.gnu.org/software/ddd`下载RPM包副本。

## 7. 主窗口

`DDD`将主窗口分为三个垂直堆叠的窗格，如图55-1所示：

- 顶部窗格名为“数据窗口”（`data window`），显示变量。（最初数据是空的，但我们稍后会展示如何向其中放入内容。）
- 中间窗格名为“源码窗口”（`source window`），显示你正在执行的代码。你可以定义断点并看到程序停止的位置。
- 底部窗格名为“控制台”（`console`），是你输入命令的地方。

## 8. 技术55：使用DDD调试器Perl

**列表55-1：调试器命令**

| 查看源码 | 控制执行 |
| :--- | :--- |
| 跟踪 | 单步执行 |
| 选项 | 重启 |
| 搜索 | 继续执行 |
| 帮助 | 跳过子程序 |
| 显示 | 堆栈跟踪 |
| 设置断点 | 退出 |

## 9. 查看源码并单步执行

要单步执行源码，按`F5`（或点击菜单上的单步按钮）。`DDD`会执行单行代码并将绿色箭头移动到下一行。

当你设置断点时，代码左侧会出现一个红色停止标记。

## 10. 修改断点

在调试程序过程中，你可能会发现需要禁用或完全删除断点。要修改断点，右键点击停止标记并选择“属性”（`Properties`）。属性对话框打开（见图55-3）。

## 11. 为断点分配命令

你可以为断点分配条件以简化其功能。例如，如果你只想在`$headline`未定义时中断，请在“条件”字段中输入以下命令，然后点击“应用”：

```
defined($headline)
```
