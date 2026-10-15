
学习命令行的首要技能之一是导航虚拟目录结构，以及创建和删除目录。理解如何查看文件、创建文件、复制和移动文件以及删除文件都是重要的技能。下述章节描述了如何使用命令完成这些任务。

## 查看和创建文件

查看文件名称及其各种`元数据`的最基本命令是列表（`list`）命令。

执行该命令时，你使用`ls`以及任何需要的选项或参数。

```
ls [OPTION] [FILE]...
```

## 处理文件和目录

在`list`命令的语法结构中，`[OPTION]`意味着有各种选项（也称为`开关`/`switches`），你可以添加它们来显示不同的元数据。括号表示这些开关是可选的。`[FILE]`参数表示你可以在命令的末尾添加目录或文件名，以查看特定文件或虚拟目录结构位置内文件的元数据。正如括号所所示，它是完全可选的。

> 注意：语法结构描述了 `Linux` 系统手动页中的许多命令行命令，这些手动页也称为`man 页`/`man pages`。如需查找特定命令的语法结构，请查看其 `man` 页（例如 `man *ls*`）并查看 `Synopsis`（概览）部分。

当你不带任何额外的参数或选项执行`ls`命令时，它会列出`当前工作目录`内所有文件和子目录的名字，如列表 3.1 所示。

### 列表 3.1 使用 `ls` 和 `pwd` 命令

```
$ ls

Desktop Downloads Pics Public Videos

Documents Music Project47.txt Templates

$

$ pwd

/home/Christine

$
```

你的工作目录是登录进程在虚拟目录结构中的当前位置。你可以通过执行`pwd`命令来确定此位置的目录名称，列表 3.1 中也是如此。

要显示文件和目录名称以外的元数据，你需要为`list`命令添加各种选项。表 3.1 显示了一些最常用的选项。

### 表 3.1 `ls` 命令常用的选项

| 短格式 | 完整格式 | 描述 |
| --- | --- | --- |
| -a | --all | 显示所有文件和子目录名称，包括隐藏文件 |
| -d | --directory | 显示目录自身的元数据而不是其内容。 |
| -F | --classify | 使用指示代码（`*`、`=`、`>`、`@` 或 `\|`）对每个文件的类型进行分类。 |
| -i | --inode | 显示所有文件和子目录名称及其关联索引节点。 |

第 3 章 管理文件、目录和文本

# 表 3.1 `ls` 命令常用的选项（续）

| 短格式 | 完整格式 | 描述 |
| --- | --- | --- |
| -l | N/A | 显示文件和子目录元数据，包括文件类型、文件访问权限、硬链接数、文件所有者、文件组、修改日期和时间以及文件名 |
| -R | N/A | 显示目录内容，并对于原始目录树中的任何子目录，连续显示其内容（递归地） |

表 3.1 包含了需要记忆的`ls`命令选项，因为你会经常使用它们。然而，尝试各种`ls`命令和选项的组合是值得的。花时间在 `man` 页中查阅`ls`命令的选项。例如，你可以尝试`-lh`选项组合，如列表 3.2 所示，它使文件大小更具人类可读性。当你尝试各种命令选项时，不仅能为 `Linux` 认证考试做更充分的准备，还能找到你特定需求的组合。

### 列表 3.2 探索 `ls -lh` 命令

```
$ pwd
/home/Christine/Answers
$
$ ls -l
total 32
drwxr-xr-x. 2 Christine Christine 6 Aug 19 17:34 Everything
drwxr-xr-x. 2 Christine Christine 6 Aug 19 17:34 Life
-rw-r--r-- 1 Christine Christine 29980 6 Aug 19 17:37 Project42.txt
drwxr-xr-x. 2 Christine Christine 6 Aug 19 17:34 Universe
$
$ ls -lh
total 32K
drwxr-xr-x. 2 Christine Christine 6 Aug 19 17:34 Everything
drwxr-xr-x. 2 Christine Christine 6 Aug 19 17:34 Life
-rw-r--r-- 1 Christine Christine 30K 6 Aug 19 17:37 Project42.txt
drwxr-xr-x. 2 Christine Christine 6 Aug 19 17:34 Universe
$
```

请注意，某些发行版默认包含了`ls -l`（两个小写 `l`）的别名，列表 3.3 在一个 `CentOS` 发行版中进行了演示。`Linux` 命令行中的别名只是代表另一个（通常是复杂的）命令的短命令。你可以通过在命令行输入`alias`来查看你的进程拥的所有当前别名。

### 列表 3.3 探索 `ll` 命令

```
$ ls -l
total 32
drwxrxr-x. 2 Christine Christine 6 Aug 19 17:34 Everything
drwxrxr-x. 2 Christine Christine 6 Aug 19 17:34 Life
-rw-r--r-- 1 Christine Christine 29900 Aug 19 17:37 Project42.txt
drwxrxr-x. 2 Christine Christine 6 Aug 19 17:34 Universe
$
$ ll
total 32
drwxrxr-x. 2 Christine Christine 6 Aug 19 17:34 Everything
drwxrxr-x. 2 Christine Christine 6 Aug 19 17:34 Life
-rw-r--r-- 1 Christine Christine 29900 Aug 19 17:34 Project42.txt
$
```

`touch` 命令允许你创建空文件。它的主要目的是更新时间戳。出于学习目的，如列表 3.4 所示它是很有用的。

```
$ pwd
/home/Christine/Answers
$
$ touch Project43.txt Project44.txt Project45.txt
$ ls -l
```

要创建目录，请使用`mkdir` 命令。要创建多个目录，只需列出空格分隔的名字。

### 列表 3.5 探索 `mkdir` 命令

```
$ pwd
/home/Christine/Answers
$
$ mkdir Directory1 Directory2
$ ls -F
Directory1/
Directory2/
```

当你尝试使用`mkdir` 命令构建目录树时请注意。在没有父目录（`Projects`）的情况下无法创建子目录（`42`）。`mkdir` 命令的`-p` 选项允许你覆盖这种行为，如列表 3.6 所示。

```
$ pwd
/home/Christine/Answers
$
$ mkdir Projects/42
mkdir: cannot create directory 'Projects/42': No such file or directory
$ mkdir -p Projects/42
$ ls -F Projects
42/
```

## 复制和移动文件

复制、移动和重命名文件及目录是基本技能。完成这些任务的命令之间存在需要了解的细微差别。

要在本地复制文件或目录，请使用`cp` 命令。执行此命令时，你使用`cp` 配合任何所需的选项或参数。命令的基本语法结构如下：

```
cp [OPTION]... SOURCE DEST
```

命令选项如结构所示并非必需的。然而，源（`SOURCE`）和目标（`DEST`）是必须的，如列表 3.7 中的基础`cp` 命令示例所示。

### 列表 3.7 使用 `cp` 命令

```
$ pwd
/home/Christine/SpaceOpera/Emphasis
$
$ ls
```

## 列表 3.7: 使用 `cp` 命令（续）

```
melodrama.txt
$
$ cp melodrama.txt space-warfare.txt
$
$ ls
melodrama.txt space-warfare.txt
$
$ cp melodrama.txt
```

在列表 3.7 中，第一次使用`cp` 命令时同时指定了源文件和目标。因此没有发生任何问题。然而，第二次使用`cp` 命令时缺少了目标文件名。这导致源文件没有被复制并生成了错误信息。

有几个实用的`cp` 命令选项。许多选项可以帮助你避免犯严重错误，例如意外覆盖文件或其权限。表 3.2 显示了一些最常用的选项。

## 表 3.2 `cp` 命令的常用选项

| 短格式 | 长格式 | 描述 |
| :--- | :--- | :--- |
| -a | --archive | 执行递归复制并保留所有文件的原始属性，如权限、所有者和时间戳 |
| -f | --force | 强制覆盖与 `DEST` 具有相同的任何现有目标文件 |
