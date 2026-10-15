

该实用程序执行的任务与 ar 命令的 s 键相同。以下是 ranlib 实用程序的简要说明。

### SYNTAX

```
ranlib [archive-list]
```

Purpose: Adds a table of contents to each archive in archive-list

以下 ranlib 命令为 mathlib.a 归档添加目录。ar s mathlib.a 命令也可以用来执行相同的任务。

```
$ ranlib mathlib.a
$
```

## 17.5.6.2 Displaying Library Information

nm 实用程序可用于显示库和目标文件的符号表（名称、类型、大小、入口点等）。该命令为库或目标文件中的每个对象（函数和全局变量）显示一行。此输出告知您库中可用的函数以及这些库函数所依赖的函数。每行输出包括对象的大小（以字节为单位）、对象的类型（数据对象、函数、文件等）、对象的范围以及对象的名称。这些信息对于调试库非常有用。以下是该实用程序的简要说明。

### SYNTAX

```
nm key archive-name [file-list]
```

Purpose: Allows display of the symbol table of the library and object files specified in file-list

常用选项/功能：

- -V Display the version number of the command
- -n Display symbols according to their address and not alphabetically
- -s Display names of the modules that contain the definitions of the symbols

在以下会话中，使用 nm -V 命令显示 nm 命令的版本，并使用 nm mathlib.a 命令显示我们在 17.4 节中创建的 mathlib.a 库的信息。

```
$ nm -V
GNU nm 2.17.50 [FreeBSD] 2007-07-03
Copyright 2007 Free Software Foundation, Inc.
This program is free software; you may redistribute it under the terms of the GNU General Public License.  This program has absolutely no warranty.
```

```
$ nm mathlib.a

input.o:
0000000000000000 T input
                U printf
                U scanf

compute.o:
0000000000000000 T compute
                U pow
%
```

nm 命令的输出显示它包含两个对象模块：input.o 和 compute.o。此外，printf、scanf 和 pow 符号未定义（U），而符号 input 和 compute 位于库中相关对象模块的文本（代码）段中。

nm 和 grep 命令通常一起运行以检索有关特定对象的信息。以下命令演示了对数学库（/usr/lib/libm.a）使用 nm 命令。命令输出显示 pow 函数位于 e_pow.o 模块中。

```
% nm -s /usr/lib/libm.a | grep "pow"
imprecise_pow1 in imprecise.o
pow1 in imprecise.o
powf in e_powf.o
pow in e_pow.o
0000000000000000 T imprecise_pow1
                U pow

0000000000000000 W pow1
e_powf.o:
0000000000000000 T powf
e_pow.o:
0000000000000000 T pow
%
```

## 17.5.7 Version Control

研究表明，软件产品的成本约有三分之二花费在维护上。正如我们之前提到的，软件产品的维护包括纠正性维护和增强。在纠正性维护中，修复部署后发现的错误和 bug。在增强中，产品得到增强以包含更多功能，例如改进的用户界面。无论其类型如何，维护都意味着更改和/或修改产品的源代码并生成新的可执行文件。这意味着使用版本控制系统（VCS）。随着您对源代码的修订，您可能需要撤销对其所做的更改并返回到软件的早期版本。此外，如果个人或程序员团队正在处理某段软件，他们应该能够在本地和自主地维护可编辑（可修改）的版本，以便在方便的时候将它们合并在一起。

Git 和 GitHub 是原子级、分布式、面向内容的 VCS。原子级意味着当您对软件包进行快照时，其中的所有内容都在同一时间点被捕获在快照中。分布式意味着您正在处理整个软件包对所有协作者来说在任何时候都是本地可用的。面向内容意味着当您将软件的不同分支工作合并时，只考虑沿您正在合并的分支的文件中行的内容。这里，内容意味着“有形式”，而上下文意味着“有意义”。Git 在操作您的软件文件和目录时只考虑内容；软件项目的个人、协作者或集成者负责软件包中文件的合并上下文。导致内容冲突的项目不同开发线的合并由 Git 通过几种有用的策略和机制指示，其解决可通过作为 Git 插件提供的许多工具来辅助。但只有编写和测试软件如何工作的人，以及管理该过程的人，才负责解决合并上下文冲突。

## EXERCISE 17.9

给出一个你认为是在修订控制系统中进行内容跟踪的详细示例。然后将该示例与你认为的上下文跟踪进行对比。

Git 作为源代码维护工具，是用于跟踪随时间对一组源代码文件所做的更改的软件数据库。虽然程序员最常使用它来协调对软件源代码的更改，但您可以使用 Git 跟踪任何类型的内容。Git 可以

- Examine the state of your source code project at earlier points in time
- Show the differences among various states of the project, and the files present at those states
- Split the project development into multiple independent lines, called branches, which can evolve separately
- Regularly recombine branches by merging, or reconciling, the changes made in two or more branches
- Allow many people to work on a project simultaneously, sharing and combining their work as needed

Git 是新一代分布式 VCS 的成员。较旧的系统如 SCCS、RCS、CVS 和 Subversion 是集中的，这意味着有一个单一的中央项目内容和历史副本，所有用户都必须参考它。如果中央副本不可用，所有用户必须等待中央副本再次上线。分布式系统如 Git 没有中央副本。每个用户都有一个完整、独立的副本

