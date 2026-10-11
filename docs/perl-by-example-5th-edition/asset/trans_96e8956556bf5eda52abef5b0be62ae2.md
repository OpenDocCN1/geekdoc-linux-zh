

## 解释

- 1 使用 `-V` 选项的 Perl 会显示版本、配置和库信息。在 Mac/UNIX 命令行提示符下，会打印 `@INC` 数组。路径中的第一个元素是 5.18 版本标准 Perl 库的完整路径。包含单词 *site* 或 *linux*（如果使用 Solaris UNIX 则为 solaris）的路径名用于站点特定的库例程和模块，最后的点代表当前工作目录。需要删除空行。最后的点很重要。Perl 在搜索这些文件时，将包含存储在（当前工作）目录（文件夹）中的任何库。
- 2 这是查看 `@INC` 数组中列出的库目录的另一种方式。（`$` 是 shell 提示符。）

**设置 `PERL5LIB` 环境变量。** 如果你使用的是 UNIX/Linux 操作系统，要向 `@INC` 数组添加新的路径元素，你可以在启动初始化文件中设置 `PERL5LIB` 环境变量。

在 C 和 TC shell 的 *`.login`* 中：

```
setenv PERL5LIB "directory path"
```

在 Bourne、Korn 和 Bash shell 的 *`.profile`* 中：

```
PERL5LIB="directory path"; export PERL5LIB
```

如果你使用的是 Windows，请进入命令窗口并输入：

```
set PERL5LIB = c:\path\to\directory
```

或者进入 *Start* 菜单，然后到 *Settings*，再到 *Advanced System Properties*，接着是 *Environment Variables*，最后选择 *New*。

为了让你的自定义库例程优先于 `@INC` 数组中列出的那些，你可以在程序中的以下行：

```
BEGIN { unshift(@INC, "."); }
```

*Unshift* 使点被添加到 @INC 数组的前部，使你的当前工作目录成为搜索路径中的第一个元素。如果你的库在另一个目录中，请使用其完整路径名而不是点。（注意 *BEGIN* 代码块会尽可能早地执行，甚至在解析所在文件的其余部分之前执行，确保在编译时更新 @INC 数组。）

## lib 声明

*lib* 声明用于在编译时更新 @INC 数组。当使用一个未在标准 @INC 位置找到的模块时，这是必要的。这与 `BEGIN { unshift @INC, @directory_list() }` 相同。

```
use lib (directory list);
use lib ('C:/bin/perl/lib/Junk');
```

当 *lib* 模块首次加载时，它会将 @INC 的当前值记录在一个数组 `@LIB::ORIG_INC` 中。要将 @INC 恢复为原始值，可以使用 `@INC = @LIB::ORIG_INC`。当使用标准 Perl 库中提供的其中一个模块（那些以 *.pm* 结尾的文件）时，必须首先确保 @INC 数组包含指向你的库分布的完整路径名，并且在使用模块名称时包含 use 函数。

如果你想了解某个特定模块是如何工作的，可以使用 *perldoc* 命令来获取文档。（*perldoc* 命令对于库中较旧的 *.pl* 文件不起作用。）例如，如果你想知道关于 *Moose.pm* 模块的信息，在命令行输入：

```
perldoc Moose
```

然后 *Moose.pm* 模块的文档将被显示。如果你输入：

```
perldoc lib
```

则 *lib.pm* 声明的文档将被显示。

### 13.2.2 包和 .pm 文件

标准 Perl 库中大多数以 *.pl* 结尾的库例程都是在 Perl 4 时代编写的，并且已被弃用。它们由包含在包内或声明在子例程内的子例程组成。库文件仍然存在于旧版本的 Perl 中，但大部分已被模块或 *.pm* 文件所取代。为了包含并执行来自标准 Perl 库（例如最近弃用的 *.pl* 文件）或来自任何其他脚本的 Perl 代码的例程，请使用 *require* 或 *use* 函数，类似于 C 语言的 *#include* 语句。要查看最新模块列表，请访问 http://perldoc.perl.org/perlmodlib.html。

*require* 函数。*require* 函数检查库是否已经包含，这与较旧的 *eval* 和 *do* 函数（它们是包含文件的旧方法）不同。如果没有参数，则包含 `$_` 变量的值。如果 @INC 数组没有指向库的正确路径，*require* 将失败，并显示如下消息：

> Can't locate pwd.pl in @INC at package line 3.

*require* 函数在运行时将文件加载到程序中。要请求库模块的特定版本，请使用：

```
require 5.010
require 5.6.1
```

![](img/8556abcb353c0991f12099420ec28735_450_0.png)

## 格式

![](img/8556abcb353c0991f120991f12099420ec28735_450_1.png)

```
require VERSION
require Expr
require
```

如果正在请求的文件不是模块，请引用正在加载的文件，如下所示：

```
require "myfile.pl";
```

如果该文件是模块，则无需引号即可请求。例如，*Exporter.pm* 模块的用法如下：

```
require Exporter;
```

*use* 函数（模块和声明）。*use* 函数允许在**编译**时将 Perl 模块和声明导入到你的程序中。如果模块文件名没有 *.pm* 扩展名，*use* 函数将不导入该模块。*require* 函数执行相同的操作，但不执行导入，并在*运行时*加载模块。

*模块* 是库中遵循某些约定行为的一个文件。标准 Perl 库中的模块以 *.pm* 扩展名结尾。它们也可以在子目录中找到。例如，模块 *BigFloat* 在文件 *BigFloat.pm* 中找到，而该文件位于名为 *Math* 的子目录中。要使用在子目录中找到的模块，目录名后跟两个冒号和模块名称，例如 *Math::BigFloat.pm*（虽然使用两个冒号使得 *BigFloat.pm* 看起来像是在名为 *Math* 的包中，但在此上下文中，两个冒号用于分隔 *Math* 目录/文件夹和模块。冒号随后会被转换为 UNIX 类型操作系统的前向斜杠和 Windows 系统的反斜杠。）

*声明*，以小写字母拼写，是编译器的指令，规定你的程序应以某种方式行事，如果没有，程序将做出相应反应；例如，warnings 将发出警告，strict 会导致程序中止，等等。一些常见的声明有 lib, utf8, feature, strict, subs 和 diagnostics。关于模块和声明的列表，请参见附录 A 中的表 A.4 和 A.5，“Perl 内置、声明、模块和调试器”。

在面向对象术语中，子例程被称为方法。如果你收到使用术语 method 的诊断信息，暂时只需将方法视为美化了的子例程。该库中的许多模块使用面向对象的 Perl。本章讨论的模块不需要理解对象。有关如何使用面向对象模块的完整讨论，请参见第 14 章，“祝福那些东西！（面向对象的 Perl）”。

## 格式

```
use Module;
use Module (list);
use Directory::Module;
use pragma (list);
no pragma;
```

如果你试图使用一个不存在的模块，你可能会看到像下面这样的错误显示：

Can't locate SomeModule.pm in @INC (@INC contains: /Library/Perl/5.16/darwin-thread-multi-2level /Library/Perl/5.16 /Network/Library/Perl/5.16/darwin-thread-multi-2level /Network/Library/Perl/5.16 /Library/Perl/Updates/5.16.2/darwin-thread-multi-2level /Library/Perl/Updates/5.16.2 /System/Library/Perl/5.16/darwin-thread-multi-2level /System/Library/Perl/5.16 /System/Library/Perl/Extras/5.16/darwin-thread-multi-2level /System/Library/Perl/Extras/5.16 .) at testest line 1.
BEGIN failed--compilation aborted at testest line 1.

## 使用 PERL 包含你自己的库

以下示例展示了如何创建你自己的库函数并使用 use 函数将它们包含在 Perl 脚本中。在包含用户定义的例程或向库添加例程时，请务必将 `1;`（一个非零值）作为例程的最后一行包含进来。如果你没有将库文件的最后一行返回为真值，require 函数将产生如下类型的错误：

Average.pm did not return a true value at user.plx line 3.

## 示例 13.6

```
(The midterm Script)
# Program name: midterm
# This program will call a subroutine from another file
use strict;
use warnings;
1 use lib qw(/home/ellie/perl/mylib);
2 use Average;
```

