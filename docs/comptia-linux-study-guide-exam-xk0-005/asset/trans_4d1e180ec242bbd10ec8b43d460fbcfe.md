
另一条通常较为复杂的命令。你可以通过在命令行输入 `alias` 来查看你的进程当前所有的别名。

### **列表 3.3**：探索 `ll` 命令

```
$ ls -l
total 32
drwxrwxr-x. 2 Christine Christine     6 Aug 19 17:34 Everything
drwxrwxr-x. 2 Christine Christine     6 Aug 19 17:34 Life
-rw-r--r--. 1 Christine Christine 29900 Aug 19 17:37 Project42.txt
drwxrwxr-x. 2 Christine Christine     6 Aug 19 17:34 Universe
$
$ ll
total 32
drwxrwxr-x. 2 Christine Christine     6 Aug 19 17:34 Everything
drwxrwxr-x. 2 Christine Christine     6 Aug 19 17:34 Life
-rw-r--r--. 1 Christine Christine 29900 Aug 19 17:37 Project42.txt
drwxrwxr-x. 2 Christine Christine     6 Aug 19 17:34 Universe
```

如果你正在处理大量的文件和目录，有时查看它们的图形化概览会有帮助。如果你无法访问图形化桌面，你仍然可以使用 `tree` 命令在命令行中以伪图形化格式查看内容，如图 3.1 所示。

![](img/c0a399aca0d18f8822d714ad0a173123_112_0.png)

**tree** 命令的输出创建一个分层结构，显示哪些文件与哪些目录相关联，从而更容易理清头绪。

**touch** 命令允许你即时创建空文件。该命令的主要用途是更新文件的时间戳——访问时间和修改时间。然而，就学习目的而言，它很有用，因为它允许你快速创建用于实验的文件，如列表 3.4 所示。

### 列表 3.4：使用 touch 命令

```
$ touch Project43.txt
$ ls
Everything   Life   Project42.txt   Project43.txt   Universe
$ touch Project44.txt Project45.txt Project46.txt
$ ls
Everything   Project42.txt   Project44.txt   Project46.txt
Life         Project43.txt   Project45.txt   Universe
$
```

注意在列表 3.4 中，使用 **touch** 命令你可以一次创建一个或多个文件。要创建多个文件，只需在命令后列出文件名称，用空格分隔。

目录有时被称为*文件夹*。从用户角度来看，目录包含文件，但实际上，目录是一种用于定位其他文件的特殊文件。目录所负责的文件，其部分元数据存储在该目录文件内。这些元数据包括文件名以及与之关联的索引（inode）号。因此，可以通过其管理目录来定位文件。

你可以快速创建目录，但与其使用 **touch**，不如使用 **mkdir** 命令。`**-F**` 选项在 **ls** 命令中将有助于此任务。它会显示任何目录（包括新创建的目录），并在每个目录名称后加上 `/` 指示符。列表 3.5 提供了一些示例。

### 列表 3.5：探索 mkdir 命令

```
$ ls -F
Everything/   Project42.txt   Project44.txt   Project46.txt
Life/         Project43.txt   Project45.txt   Universe/
$ mkdir Galaxy
$ ls -F
Everything/   Life/           Project43.txt   Project45.txt   Universe/
Galaxy/        Project42.txt  Project44.txt  Project46.txt
$
$ pwd
/home/Christine/Answers
$
$ mkdir /home/Christine/Answers/Galaxy/Saturn
$
$ ls -F Galaxy
Saturn/
$
```

要在当前工作目录中创建子目录，只需输入 `mkdir` 命令并跟上下级目录的名称，如列表 3.5 所示。如果你想在一个不同于当前工作目录的位置构建目录，可以使用绝对目录引用，如列表 3.5 中创建 Saturn 目录时所做的那样。

![](img/c0a399aca0d18f8822d714ad0a173123_114_0.png)

如果你在从*当前工作目录*创建目录并进入它们，很容易在目录结构中迷失方向。使用 `cd -` 命令可以快速返回你之前的*当前工作目录*，或者仅使用不带选项的 `cd` 命令返回你的主目录。

在构建目录时，要注意可能会发生一些错误。特别是在尝试创建目录树时，如列表 3.6 所示的示例。

### **列表 3.6：避免使用 `mkdir` 命令时的问题**

```
$ ls -F
Everything/  Life/          Project43.txt  Project45.txt  Universe/
Galaxy/      Project42.txt  Project44.txt  Project46.txt
$
$ mkdir Projects/42/
mkdir: cannot create directory 'Projects/42/': No such file or directory
$
$ mkdir -p Projects/42/
$
$ ls -F
Everything/  Life/          Project43.txt  Project45.txt  Projects/
Galaxy/      Project42.txt  Project44.txt  Project46.txt  Universe/
$
$ ls -F Projects
42/
$
```

注意，当你尝试使用 `mkdir` 命令构建目录 *Projects* 及其 42 子目录时，会发生错误。如果没有父目录（*Projects*）预先存在，就无法创建子目录（42）。`mkdir` 命令的 `-p` 选项允许你覆盖此行为，如列表 3.6 所示，从而成功创建目录树。

![](img/c0a399aca0d18f8822d714ad0a173123_115_0.png)

> 每次发出 `mkdir` 命令后输入 `ls -F` 命令以确保目录已构建是很繁琐的。相反，使用 `mkdir` 命令的 `-v` 选项来接收目录成功构建的验证信息。

## 复制和移动文件

复制、移动和重命名文件和目录是基本技能。在执行这些任务时，命令之间存在一些细微差别，你需要了解这些差别。

要在本地复制文件或目录，请使用 `cp` 命令。要发出此命令，你需要使用 `cp` 以及所需的任何选项或参数。该命令的基本语法结构为：

```
cp [OPTION]... SOURCE DEST
```

如结构所示，命令选项不是必需的。然而，源（*SOURCE*）和目标（*DEST*）是必需的，如列表 3.7 中基本 `cp` 命令示例所示。

### **列表 3.7：** 使用 cp 命令

```
$ pwd
/home/Christine/SpaceOpera/Emphasis
$
$ ls
melodrama.txt
$
$ cp melodrama.txt space-warfare.txt
$
$ ls
melodrama.txt space-warfare.txt
$
$ cp melodrama.txt
cp: missing destination file operand after 'melodrama.txt'
Try 'cp --help' for more information.
$
```

在列表 3.7 中，第一次使用 `cp` 命令时，同时指定了源文件及其目标。因此不会发生问题。然而，第二次使用 `cp` 命令时，缺少目标文件名。这导致源文件未被复制，并生成错误消息。

有几个有用的 `cp` 命令选项。许多选项可以帮助你避免犯严重错误，例如意外覆盖文件或权限。表 3.2 显示了一些常用选项。

### 表 3.2 `cp` 命令的常用选项

| 短选项 | 长选项 | 描述 |
|---|---|---|
| `-a` | `--archive` | 执行递归复制，并保留文件的所有原始属性，如权限、所有权和时间戳。 |
| `-f` | `--force` | 覆盖任何与 *DEST* 同名的预存目标文件。 |
| `-i` | `--interactive` | 在覆盖任何与 *DEST* 同名的预存目标文件前询问。 |
| `-n` | `--no-clobber` | 不覆盖任何与 *DEST* 同名的预存目标文件。 |
| `-R`, `-r` | `--recursive` | 复制目录的内容，并且对于原始目录树中的任何子目录，也递归地复制其内容。 |
| `-u` | `--update` | 仅当源文件较新时，才覆盖与 *DEST* 同名的预存目标文件。 |
| `-v` | `--verbose` | 在命令执行时提供详细的命令操作信息。 |

要复制目录，你需要在 `cp` 命令中添加 `-R`（或 `-r`）选项。该选项执行递归复制。递归复制不仅创建新目录（*DEST*），还复制源目录管理的任何文件、源目录子目录及其文件。列表 3.8 展示了如何执行递归复制以及如何*避免*执行递归复制的示例。

### 列表 3.8：使用 `cp` 命令执行递归复制

```
$ pwd
/home/Christine/SpaceOpera
$
$ ls -F
Emphasis/
$
```

