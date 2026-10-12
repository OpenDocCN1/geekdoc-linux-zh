
## 使用 `tar` 执行增量备份

增量备份仅包含自上次以来修改的文件。组织根据需要有不同的备份策略。例如，某些公司发现每周五一次全备并在期间进行增量备份就足够；另一些公司需要更频繁地进行全备。创建增量备份的语法与全备相同，如果快照已存在，`tar` 工具将检查它以确定哪些文件发生了变化。

1. 如果必要，启动 VMware Player，启动一个 openSUSE 虚拟机，并打开终端窗口。
2. 输入 `mkdir Act6-4` 并按回车，然后输入 `cd Act6-4` 并按回车。
3. 输入 `touch math english` 并按回车。
4. 输入 `tar -vf $HOME/backup0.tar -V "This is a full backup of the Act6-4 directory" --listed-incremental=$HOME/act6-4.snap *` 并按回车。此命令比你之前输入的命令长得多，请仔细检查以确保字符和空格正确。存档文件使用绝对路径（`$HOME/backup.tar`）。`$HOME` 是指定你主目录绝对路径的环境变量。`--listed-incremental=$HOME/act6-4.snap *` 如前所述创建一个快照文件。末尾的 `*` 是通配符，告诉 `tar` 工具归档目录中的所有文件。
5. 输入 `cd` 并按回车。要列出成员并显示卷头，输入 `tar -vf backup0.tar` 并按回车。
6. 输入 `cd Act6-4` 并按回车。要模拟目录更改，输入 `touch science` 并按回车。
7. 输入 `tar -vf $HOME/backup1.tar -V "This is an incremental backup of the Act6-4 directory" --listed-incremental=$HOME/act6-4.snap *` 并按回车。此命令与第 4 步中的命令相似，但文件名不同。存档文件（`backup1.tar`）是自上次备份（在 `backup0.tar` 中创建）以来所有更改内容的备份。
8. 输入 `tar -vf backup1.tar` 并按回车。`backup1.tar` 的成员有哪些？
9. 输入 `cd Act6-4` 并按回车。
10. 要模拟系统崩溃，输入 `rm *` 并按回车，删除 Act6-4 目录中的所有文件。
11. 要提取 `backup0.tar` 存档的内容，输入 `tar -xvf $HOME/backup0.tar` 并按回车。
12. 要提取 `backup1.tar` 存档的内容，输入 `tar -xvf $HOME/backup1.tar` 并按回车。
13. 输入 `ls -l` 并按回车。所有文件都恢复了吗？
14. 让虚拟机保持运行并打开终端窗口，以便进行后续活动。

## `cpio` 工具

`cpio` (in/out) 工具使用 `ls` 或 `find` 命令的结果来生成要归档的文件。它以三种模式运行：输出 (copy-out)、输入 (copy-in) 和 旁传 (copy-pass)。在输出模式下，它根据 `ls` 或 `find` 命令的输出创建存档。在输入模式下，它从存档中提取文件。在 旁传模式下，它将文件从一个目录复制到另一个目录；换句话说，它将输出和输入结合起来，而不创建存档。

## 标准输入、标准输出和重定向

在学习如何创建管道之前，你需要理解标准输入、标准输出和重定向之间的区别。在 Linux 中，默认的标准输入是键盘。例如，`pwd`、`cd` 和 `ls` 等命令是通过输入它们来执行的。`<` 符号用于将输入从键盘重定向。大多数情况下，预期输入来自键盘，因此你不会看到输入重定向。然而，它对于不直接打开文件的命令很有用，例如 `mail` 命令（在第 12 章中有更详细介绍）。你可以使用标准重定向将文本文件的内容电子邮件给系统上的另一个用户，如下所示；`letter.txt` 文件的内容变为 `mail` 命令的输入：

```
mail user < letter.txt
```

默认的标准输出是屏幕。例如，`ls` 命令的输出显示在屏幕上。你可以使用输出运算符，例如 `>`（大于”）将命令的输出重定向到文件，或使用 `|`（“管道”符号）将一个命令的输出作为另一个命令的输入。以下示例显示了将 `ls` 命令的输出重定向到 `home_listing` 文件而不是显示输出：

```
ls > home_listing
```

以下示例显示了如何使用命令查看 `home_listing` 文件的内容：

```
cat home_listing

Act6-1

Act6-2

Act6-3

Act6-4

act6-4.snap
```

你之前用过的另一个重定向运算符是管道符号（`|`），在以下示例中使用：

```
ls | more
```

### 输出模式

这种 `cpio` 模式与 `-o` 或 `--create` 选项一起使用，通过将 `ls` 或 `find` 的输出作为存档输入来创建存档。以下示例显示了使用此命令归档当前目录下的所有文件：

```
ls | cpio -o > files.cpio
```

在此示例中，`ls` 命令的结果用于确定在 `files.cpio` 中归档哪些文件。你可以通过添加 `-v` 选项来显示已归档的文件，如下所示：

```
ls | cpio -ov > files.cpio
```

以下示例显示了使用 `find` 命令的结果归档 `/home/user1` 目录下的所有文件 | 使用 `-v` 选项显示正在归档的文件：

```
find /home/user1 | cpio -ov > home.cpio
```

# 第 6 章 管理数据：备份与恢复过程

### 输入模式

这种拷贝模式用于提取存档。回提取存档。以下示例显示了使用 `cpio` 工具提取文件：

```
cpio -iv < files.cpio
```

### 旁传模式

这种模式将文件从一个目录复制到另一个目录；换句话说，它将输出和输入结合而不创建存档。以下示例显示了使用此命令复制文件：

```
cpio -dmv < files.cpio
```
