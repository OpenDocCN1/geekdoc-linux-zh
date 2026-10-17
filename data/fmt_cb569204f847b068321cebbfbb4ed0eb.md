
### 解释

- 1. 这是包声明。包以它所在的文件名命名，即 `Carp.pm`，版本 1.26。（`carp`、`croak` 和 `confess` 函数生成错误消息，如 `die` 和 `warn`。区别在于，使用 `carp` 和 `croak` 时，错误在调用例程中调用错误的行报告，而 `confess` 打印出显示生成错误的子程序链的堆栈回溯。它在调用所在行打印其消息。）
- 2, 3 需要 `Exporter.pm` 模块来实现其导入例程，该例程使子程序和变量对本模块用户的命名空间可用。`@ISA` 数组包含 `Exporter.pm` 模块的名称，允许继承必要的 Exporter 方法供本模块的用户使用。（参见 14.4 节中的 `@ISA`，“继承。”）
- 4 `@EXPORT` 数组列出了将导出到使用该模块的程序的命名空间的子程序 `confess`、`croak` 和 `carp`，无论命名空间的所有者是否想要它们。（将不需要的符号放入其他命名空间的过程称为命名空间污染。）
- 5 为防止命名空间污染，Perl 提供了 `@EXPORT_OK` 数组，它被赋予了一个变量和子程序列表（`click`、`verbose`、`longmess` 和 `shortmess`），这些符号仅在用户要求时导出；也就是说，如果他不要它们，他就不会得到它们。
- 6 `@EXPORT_FAIL` 数组列出了无法导出的符号。
- 7 出现在 `EXPORT` 列表中的子程序在此定义。

## 13.2.5 如何“使用”标准 Perl 库中的模块

以下示例演示了如何使用标准 Perl 库中的 `Carp.pm` 模块。使用模块的第一步是阅读文档。请使用 `perldoc` 命令来完成此操作。

`use` 指令确保在编译时加载请求的模块。如果模块名称后跟有一个列表，则该列表表示将从模块导出并在你的程序中使用（导入）的符号。在 `Carp.pm` 模块中，其中一个函数名为 `croak`。如果被请求，用户可以不通过 `::` 语法完全限定符号名称（`Carp::croak`）而直接调用 `croak` 函数。

![](img/8556abcb353c0991f12099420ec28735_460_0.png)

### 示例 13.9（续）

（输出）
你开了多少英里？ 100
你用了多少加仑汽油？ 我不知道
在 `croak.plx` 第 11 行，`<STDIN>` 第 2 行：里程和加仑数必须是数字
你开了多少英里？ 100
你用了多少加仑汽油？ 0
在 `croak.plx` 第 26 行，`<STDIN>` 第 4 行：除以零是非法值
在 `croak.plx` 第 20 行调用了 `main:check(0)`
在 `croak.plx` 第 15 行调用了 `main:mileage(100, 0)`

### 解释

- `Carp` 模块被使用在（加载到）当前包 `main` 中。该模块的 `@EXPORT` 列表包括 `confess`、`croak` 和 `carp`。除非另有说明，模块用户将自动导入这些子程序名称。
- 模块用户必须请求 `cluck` 子程序，因为它列在 `Carp` 的 `@EXPORT_OK` 数组中。如果未在此列中列出，Perl 会发送包含（你需要声明 `cluck` 吗？）的语法错误。
- 检查用户输入是否为数值。
- 如果其中一个输入值不是数字，`cluck` 将发送警告，但不会导致程序退出。
- 调用用户定义的 `mileage` 函数，并传入两个参数。
- 此函数用于检查 `$gallons` 的值是否不为零。此处仅用于演示 `croak` 方法如何报告函数被调用处的错误。
- 调用 `croak` 函数时附带一个错误消息。`croak` 函数是从 `Carp` 模块导入的。如果 `$gas` 的值为 0，程序将终止。错误消息会报告程序终止的行号，以及包名称、子程序名称和调用该子程序的行号。

## 13.2.6 使用 Perl 创建你自己的模块

以下示例说明了如何在一个单独的 `.pm` 文件中创建一个模块，并在另一个程序中使用该模块。虽然该模块本身看起来与其他任何包无异，但它额外包含了 `Exporter` 模块、`@EXPORT`、`@EXPORT_OK` 和 `%EXPORT_TAGS`，以便列出并导出符号。在导出列表时，尽量避免导出 Perl 内置函数的名称。在以下示例中，函数名为 `nap` 而不是 `sleep`。如果你的函数命名为 `sleep`，内置的 `sleep` 函数将被你的函数覆盖，这可能会对疏忽的用户产生未预料到的后果。有关模块创建的指南，请参阅 `perlmadb.pl`。若要查看用于创建 CPAN 扩展和模块的骨架模块，请参阅 `Module::Starter` 或 `Dist::Zilla`。这两个都可以在 `perlcode.perl.org` 或通过 `perldoc` 命令找到。

有许多网站讨论模块命名的风格指南。请参阅 [https://pause.perl.org/](https://pause.perl.org/) 上的“模块命名（The Naming of Modules）”。同时检查 [perldoc.perl.org/perlmodstyle.html](http://perldoc.perl.org/perlmodstyle.html)。在命名模块时，请考虑谁将使用你的模块并赋予其背景信息。仅仅因为你知道它是做什么的，并不意味着其他人也知道。良好的文档也是模块创建的重要组成部分。我们在第 14.5 节“旧式文档——记录模块”中涵盖了文档。以下示例是一个面向函数的模块，它利用 *`Exporter.pm`* 模块将变量和子程序名称导出给模块用户。这里展示了该模块及其用户。

### 示例 13.10

```perl
# (The MyPet/Cat.pm Module)

package MyPet::Cat;

use strict;

use warnings;

our $VERSION="0.01"; # The version number for the Cat.pm module

use Exporter qw(import); # Simplified import

#require Exporter;

#our @ISA=qw(Exporter);

our @EXPORT=qw(eat); # Default is to eat

our @EXPORT_OK=qw(speak nap play); # Exported on demand

our %EXPORT_TAGS = ('all'=>[ qw(speak nap play eat)]); # Export a collection

sub name{ # Not on the export lists

my $name = shift;

return $name;

}

sub speak{

return "Meowwww\n";

}

sub eat{

return "likes fish\n";

}

sub nap {

return "ZZzzzzzz\n";

}

sub play {

return "catch a mouse!\n";

}

1;
```

### 示例 13.10（续）

```perl
use MyPet::Cat qw(:all);

use MyPet::Cat;

my $petname = MyPet::Cat::name("Sneaky");

print "$petname ", eat();

print "$petname likes to ", play(), "\n";

print nap(), "\n";

print speak();
```
