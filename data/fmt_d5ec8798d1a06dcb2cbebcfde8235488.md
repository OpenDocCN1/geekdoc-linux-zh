
`/*`

* 将字符串 s2 拷贝到 s1。s1 必须足够大

* return s1

 */

`char` `strcpy(s1, s2)`

`register` `char` *s1, *s2;

{

    `register` `char` os1;

    os1 = s1;

    `while` (*s1++ = *s2++)

    ;

    `return`(os1);

}
```

```c
/* 将 source 拷贝到 dest。拷贝 '\0' 后停止，
并返回指向 dest 末尾 '\0' 的指针。这样我们的调用者
就可以向 dest 字符串拼接内容，而无需再次调用 strlen。 */
`char` *`strcpy`(dest, source)
`char` *dest;
`char` *source;
{}
```

```c
`while` ((*dest++ = *source++)) != '\0'
  /* void body */
  `return` (dest - 1);
```

a. 你想出多少种方法将光标移动到拼写错误处？
b. 一旦光标在错误处或附近，你能想出多少种修复方法？
c. 是否有方法可以在不显式导航/搜索的情况下修复错误？你能想出多少种？
d. 第 2 行和第 3 行颠倒了。你能想出多少种方法纠正这种状况？
e. 你如何导航光标到拼写错误处？
f. 一旦光标在错误处或附近，你能想出多少种修复方法？
g. 第 2 行和第 3 行颠倒了。是否有面向视觉的方法来修复它们？
h. 是否有视觉方法可以修正多个错误（类似于 META-）？

# 本章内容

- 背景 542
- Shell 基础 543
- 命令的分离与分组 547
- 重定向标准错误 552
- noclobber: 避免覆盖文件 554
- 作业控制 554
- 操作目录栈 557
- 进程 560
- 参数与变量 566
- 历史记录 588
- 编辑命令行 591
- 别名 602
- 命令行扩展 606

1. 虽然本章侧重于 Bourne Again Shell，但本章大部分内容也适用于 Z Shell。章节注明了 zsh 或 tsh 的实现与 bash 的不同之处；在适当的情况下会将你指向书中讨论该替代实现的地方。第 13 章详细探讨了 Bourne Again 和 Z Shell 编程。

## 本章涵盖了哪些 Shell？

本章侧重于 Bourne Again Shell (`bash`)，并在 TC Shell 或 Z Shell 与其不同之处提供了注释和页码引用。具体而言，“编写简单的 Shell 脚本”（第 544 页）、“分离与分组命令”（第 547 页）和“进程”（第 560 页）适用于三种主要的 Shell。

在单用户模式下，请始终将 Bourne Again Shell 作为你的主要根 Shell。所有的 Shell 脚本都是编写在 Bourne Again Shell 下运行的；如果你在启动系统或进行系统维护、管理或修复工作时需要单用户模式，熟悉这个 Shell 是一个好主意。

在不重复第 5 章第 157 页“文件名生成/路径名”内容的情况下，本章扩展了第 5 章描述的 Shell 交互功能，解释了如何创建和运行简单的 Shell 脚本，引入了 Shell 编程的基本方面，并描述了命令行扩展。第 14 章涵盖了 TC 和 Z Shell 编程的交互式用法，第 15 章探索了 Bourne Again Shell 中缺失的一些 Z Shell 特性，并提出了更具挑战性的 Shell 问题。

所有高级 Shell 章节（12–15）都会根据情况讨论每种 Shell，并为特定 Shell 中某个主题的更详细信息提供页码引用。符号表示某个特定工具、内置命令或变量属于哪一个。

## 如果你对这些内容是新手

你可能想推迟阅读本章的“作业控制”部分（第 554 页）及章节，直到你能熟练创建和运行简单的 Shell 脚本。但是，你应该阅读“参数与变量”（第 566 页）。除了用户创建的变量外，Shell 还维护了几个控制 Shell 重要特性的关键变量。

## 背景

Bourne Again Shell 基于 Bourne Shell（一种早期的 UNIX Shell，书中将其称为原始 Bourne Shell 以免混淆），它由以下编写：

- 1. 请参阅第 26 页的“Shell 标识符”以解释 Shell 符号。

## Shell 编程

由于许多用户更倾向于 Bourne Again Shell 的编程语言而非 TC Shell，而且它与 Z Shell 编程语言共享许多共同特性，接下来的章节将详细描述 `bash`（以及 `zsh`）编程。

由 AT&T 贝尔实验室的 Steve Bourne 编写。多年来，原始 Bourne Shell 得到了扩展，并且是许多商业版本 UNIX 提供的基础 Shell。

由于其长期且成功的历史，Bourne Shell 已被用于编写许多管理 UNIX 系统的 Shell 脚本。其中一些脚本在 GNU/Linux 中以 Bourne Again Shell 脚本的形式出现。尽管 Bourne Shell 中没有许多扩展和功能，但 `bash` 保持了与 Bourne Shell 的兼容性，因此你可以在 `bash` 下运行 Bourne Shell 脚本。传统的 Bourne Shell 称为 `sh`。GNU/Linux 中的 `sh` 是 `bash` 的符号链接，因此需要 Bourne Shell 的脚本仍然可以运行。

System V 引入了 Korn Shell (`ksh`)，由 David Korn 编写。Bourne Again Shell 的功能（如命令别名和命令行特性）是基于 Korn Shell 中类似的的特性。如果你熟悉 Korn Shell，你可能更喜欢使用第 15 章讨论的 Z Shell，因为它与 Korn Shell 非常相似。

POSIX 标准化小组定义了 Shell 功能的标准（POSIX 1003.2）。Bourne Again Shell 提供了符合此 POSIX 标准要求的特性。目前正努力让 Bourne Again Shell 完全符合 POSIX 标准。在此期间，当你使用 `--posix` 选项调用 `bash` 时，Bourne Again Shell 的行为将更贴近 POSIX 要求。

## Shell 基础

本节涵盖了变量和赋值语句，以及如何编写简单的 Shell 脚本并使其可执行。

## 赋值语句

Bourne Again、TC 和 Z Shell 允许你创建和使用变量。三种 Shell 命名和引用变量的规则是类似的（第 566 页）。

### 444 第 12 章 Shell II：Bourne Again Shell

在 Bourne Again 和 Z Shell 中，你使用以下语法为变量赋值：

```
VARIABLE=value
```

等号 (`=`) 符号两侧都不能有空格。如果你想在变量值中包含空格，请给值加上引号并对空格加引号。

在所有三种 Shell 中，通过在变量名前面加美元符号并括在大括号中来引用变量的值，例如 `${VARIABLE}`。除非变量后面紧跟着字母、数字或下划线，否则大括号是可选的。此外，Bourne Again Shell 通过位置引用其命令行上的参数，使用特殊变量 `$1`, `$2`, `$3` 直到 `$9`。如果你想引用第九之后的参数，必须使用大括号，例如 `$[10]`。命令名称存储在 `$0` 中。

你可以使用 `unset` 内置命令取消（删除变量的值和属性）一个变量

![](img/aa8214d49e1cf50152c432845129fb3b_593_0.png)

```
$ unset PREF SUFF
```

Bourne Again Shell 允许你在命令行上放置变量赋值。这些赋值对于命令 Shell 是局部的，因为它们仅适用于该命令。以下命令带有 `TEMPDIR=~/temp` 的值运行 `my_script`：

```
$ TEMPDIR=~/temp my_script
```
