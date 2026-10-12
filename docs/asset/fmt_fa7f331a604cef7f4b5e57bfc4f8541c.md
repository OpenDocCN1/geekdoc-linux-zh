
| ::Architecture | 如果 Perl 在 68k 架构上运行，则返回 PowerPC。 |

表 11-4 使用 MacPerl 可以获得的额外信息

## 第 11 节：跨平台函数与问题

`-w` 选项和适当的 `require()` 调用。这两者结合起来应该如下：

```perl
#!/usr/bin/perl
require 5.002;
```

- 2. 接下来，创建一些变量来显示脚本运行在什么操作系统上。在变量声明中，我们使用 `$^O` 变量，如果为真则将该变量设置为 1。否则，它仅包含一个空值。这允许我们在脚本后半部分对系统类型进行快速计算。

注意，在检查 UNIX 时，你只需要查找 Solaris、SunOS 和 Linux，但如果你有其他版本，可以使用表 11-3 中的适当值来编辑此处包含的内容。

一旦设置了变量，你就可以使用 `if` 语句来执行你需要的任务。这些任务涉及正确设置 Netscape 应用程序的路径以便你可以启动它。这意味着我们将为 Windows、Mac OS 和 UNIX 编写部分。你还需要包含一个默认部分，以防运行此脚本的系统不是你编写的类型之一。

```perl
$is_win32 = $0 eq "Win32";
$is_unix = ($0 eq "solaris") or ($0 eq "sunos") or ($0 eq "linux");
$is_macos = $0 eq "MacOS";
```

我们处理的第一个系统是 Windows 系统。为了确保只在 Windows 系统上执行这些任务，我们将 `$is_win32` 变量作为 `if` 语句的条件。

- 1. 一旦确定确实是 Windows 机器，我们首先打印一个免责声明，说明脚本运行假设用户正在使用 Netscape Communicator 4 且其安装在默认位置。免责声明完成后，我们将默认路径存储在 `$default_path` 变量中。到目前为止，我们拥有如下：

```perl
print "\n: This example assumes Netscape Communicator 4.x\n";
print "and the default installation location\n\n";
$default_path = "Program Files\Netscape\Communicator\Program\\";
```

- 2. 接下来，我们提示用户安装 Netscape Communicator 的驱动器。如果你还记得第 1 节，我们可以使用 `STDIN` 读取它，然后使用 `chomp()` 函数移除末尾的回车符。这得到：

```perl
print "Drive Installed On (i.e., c, d, e, etc.): \n";
chomp($drive = $STDIN);
```

- 3. 接下来，我们获取用户输入的驱动器（存储在 `$drive` 变量中）、`$default_path` 变量以及字符串 `netscape.exe`，并将它们拼接起来以获取 Netscape 可执行文件的路径。这个新值存储在名为 `$netscape` 的变量中，稍后由 `system()` 函数调用。脚本此部分的完整代码如下：

```perl
if($is_win32){
  # warning and set $default_path
  print "\nNOTE: This example assumes Netscape Communicator 4.x.\n";
  print "and the default installation location\n\n";
  $default_path = "Program Files\\Netscape\\Communicator\\Program\\";
}
```

```perl
# prompt the user for the drive that Netscape is installed on
print "Drive Installed On (i.e., c, d, e, etc.): \n";
chomp($drive = $STDIN);
```

```perl
# build path to executable and store in $netscape variable
$netscape = $drive . ":\" . $default_path . "netscape.exe";
```

我们处理的下一个系统是 UNIX。如你所见，UNIX 实际上是最容易处理的，因为启动 Netscape 应用程序的大多数问题都是基于路径的而且整个 UNIX 系统都是在路径环境中配置的。我的意思是，作为这些系统的一个用户，你需要的几乎所有应用程序都在 `PATH` 中，所以你不需要指定任何目录信息。

- 1. 与 Windows 系统一样，我们做的第一件事是写一个免责声明。尽管正如我们提到的，Netscape 可执行文件几乎总是位于你的 `PATH` 中，但必须如此程序才能运行。

> 提示
>
> Netscape 可执行文件不在你的 `PATH` 中，但你知道它在系统上吗？尝试在命令行输入 `find -name netscape -print`。一旦找到目录，你就可以将其添加到路径中。请参表 11-1 了解如何操作。

- 2. 第二也是最后一项（我们告诉过你这很短了！）你需要做的仅仅是将我们的 `$netscape` 变量设置为字符串 `netscape`。这完成了我们的 UNIX 部分，它看起来如下：

> 提示
>
> 奇奇为什么这里有一个 `elsif` 语句？记住，我们的程序需要检查几个系统，所以如果第一个 `if` 语句不匹配，我们需要继续评估，这就是我们使用 `elsif` 语句的原因。我们不希望在给定系统上执行多个部分。我们也对 Mac OS 部分执行同样的操作。

```perl
elsif($is_unix) {
  # print warning and set netscape
  print "\nNOTE: This example assumes Netscape Navigator 4.x\n";
  print "is in your PATH\n";
  $netscape = "netscape";
}
```

最后一个系统部分（但不是最后一个程序部分）是 Mac OS 部分。

- 1. 首先，写下免责声明。尽管正如我们提到的，Netscape 可执行文件几乎总是位于你的 `PATH` 中，但必须如此程序才能运行。

- 2. 接下来，我们提示用户安装 Netscape Communicator 的驱动器。如果你还记得第 1 节，我们可以使用 `STDIN` 读取它，然后使用 `chomp()` 函数移除末尾的回车符。

- 3. 接下来，我们获取用户输入的驱动器（存储在 `$drive` 变量中）、`$default_path` 变量以及字符串 `netscape.exe`，并将它们拼接起来以获取 Netscape 可执行文件的路径。这个新值存储在名为 `$netscape` 的变量中。

## 继续进阶

Perl 的主要优势之一是能够在多个平台上运行。Java 和 JavaScript 等语言也将这种平台独立性作为其优势之一。但 Perl 在某些系统上会遇到兼容性问题，你需要留意这些问题。在本模块中，我们介绍了许多此类问题，并向你展示了规避它们的方法，或指出了它们的局限性。

所以，请记住，仅仅因为你的程序在某个系统上无法运行，并不意味着你的代码有问题。你可能是在尝试执行 Perl 解释器在该环境下不支持的操作。

## 掌握检查

- 1. 在所有使用 `$^O` 变量的脚本中，应该包含哪一行代码？

  **A. `use $^;`**

  **B. `require $^;`**

  **C. `demand 5.002;`**

  **D. `require 5.002;`**

- 2. 下列中哪项是 Mac OS 系统的路径分隔符？

  **A. `\*`**

  **B. `/`**

  **C. `::`**

  **D. `:`**

模块 11：跨平台函数与问题 393

## 掌握检查

- 3. 如果你想让某些内容只在 AIX 系统上运行，你应该在 `$^O` 变量中检查哪个字符串？

  - A. `linux`

  - B. `unix`

  - C. `aixix`

  - D. `aixunix`

- 4. 启动提示对话框的 MacPerl 子程序是什么？

  - A. `MacPerl::Ask`

  - B. `MacPerl::Prompt`

  - C. `MacPerl::Dialog`

  - D. `MacPerl::Dialog::Ask`

# 模块 12

# 错误信息与调试

### 本模块目标

- 理解错误信息
- 学习如何使用 Perl 调试器

如果不是因为棘手的问题——错误，程序员的世界将是完美的。在本模块中，我们将讨论最常见的错误，以及如何找到并修复它们。

可能会发生几种不同的错误，但对于新程序员来说，最常见的是语法错误。本模块的第一部分重点关注如何找到这些错误并尽可能容易地纠正它们。
