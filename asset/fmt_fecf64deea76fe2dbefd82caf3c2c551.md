
`(2b)|[^b]{2}`

如果你在使用 `egrep` 命令 `grep` 搜索文本文件时使用了这个表达式

### 探索练习 3-6

**预计时间：** 30 分钟
**目标：** 使用 `vi` 编辑器。

**描述：** 你在实践项目 3-5 中安装的 `vim-enhanced` 软件包包含一个短期 30 分钟的使用教程。在命令行提示符处输入 `vimutor` 开始此教程并按照指示操作。

### 探索练习 3-7

**预计时间：** 40 分钟
**目标：** 使用 `vi` 编辑器。

**描述：** 使用 `vi` 编辑器将以下文本输入新文档中。接下来，使用 `vi` 编辑器根据表 3-5、3-6 和 3-7 中的信息以及本章提供的示例修复文件中的错误。

Hi there,
Unfortunately we were not able to make it to your dining room
Unfortunately we were not able to make it to
this year vacationing in Algonquin Park - I especially wished
to see the model of the highland inn and the train station in
the dining rooms.

I have been reading the history of Algonquin Park but
where could I find a description of where the Highland Inn Cache lake.

如果不方便的话，您能否告知我，我不需要等到明年我们访问 Lodge 时再等？

I hope this day finds you well.
Regards,
Elizabeth Mackenzie

### 探索练习 3-8

**预计时间：** 40 分钟
**目标：** 使用 `Emacs` 编辑器。

**描述：** 从 `vi` 编辑器中学到的知识可以轻松转移到 `Emacs` 编辑器中。使用 `Emacs` 编辑器代替 `vi` 执行探索练习 3-7。

## 第3章 探索 Linux 文件系统

## 探索练习 3-9

**预计时间：** 20 分钟
**目标：** 配置持久的 `vi` 环境设置。

**描述：** 当你使用 `vi` 编辑器并在提示符更改环境设置时（例如使用 `:set number` 启用行号），你可以将任何可以在提示符处输入的 `vi` 命令放在家目录下的特殊隐藏文件中，即 `.vimrc` 或 `.exrc`。每次打开 `vi` 编辑器时，它都会查找这些文件并自动执行其中的命令。进入 `vi` 编辑器，除了行号外，寻找两个你想更改的环境设置。然后在你的家目录下创建一个名为 `.exrc` 的新文件，并输入更改这些 `vi` 环境设置的三行内容（不要每行都以 `:` 字符开头，直接输入 `set` 命令——例如 `set number`）。完成后，打开 `vi` 编辑器编辑一个新文件并测试是否有效。

## 第4章 Linux 文件系统管理

## 目标

- 描述文件系统标准 (`FHS`)。
- 解释 Linux 目录的功能。
- 使用标准 Linux 命令管理文件。
- 描述目录权限。
- 解释目录类型。
- 识别标准 Linux 目录。
- 应用标准 Linux 权限。
- 描述目录所有权。
- 学习目录属性。

在上一章中，你学习了导航文件。本章重点关注目录。首先，你探索标准 Linux 目录。接下来，你探索文件、权限和属性。

## 文件系统标准

Linux 上成千上万的文件组织在目录中。文件系统标准 (`FHS`) 的创建是为了简化 Linux 文件的查找。`FHS` 还允许开发人员不受发行版限制创建软件。大多数 Linux 发行版遵循 `FHS`。

## 表 4-1 文件系统标准定义的 Linux 目录

| 目录 | 描述 |
| --- | --- |
| `/bin` | 包含所有用户的二进制命令（在大多数 Linux 系统上，此目录是 `/usr/bin` 的快捷方式） |
| `/boot` | 包含 Linux 内核和引导程序使用的文件 |
| `/dev` | 包含设备文件 |
| `/etc` | 包含系统配置文件 |
| `/home` | 用户目录的默认位置 |
| `/lib` | 包含 `/bin` 和 `/sbin` 命令使用的共享库以及内核模块（在大多数 Linux 系统上，`/lib` 是 `/usr/lib` 的快捷方式，`lib64` 是 `/usr/lib64` 的快捷方式） |
| `/media` | 包含用于访问可移动介质（如 U 盘和闪存器）系统的子目录 |
| `/mnt` | 用于临时访问可移动介质系统的空目录 |
| `/opt` | 存储额外的程序 |
| `/proc` | 包含进程和内核信息 |
| `/sbin` | `root` 用户目录。包含用于管理的系统二进制命令（在大多数 Linux 系统上，此目录是 `/usr/sbin` 的快捷方式） |
| `/sys` | 包含系统硬件配置信息 |
| `/tmp` | 存放程序创建临时文件 |
| `/usr` | 包含大多数系统命令和工具——包含：`/usr/bin`—二进制命令；`/usr/games`—教育程序和游戏；`/usr/include`—C 头文件；`/usr/lib` 和 `/usr/lib64`—库；`/usr/local`—本地程序；`/usr/sbin`—系统命令；`/usr/share`—架构无关的文件；`/usr/share/X11`—Windows 系统（有时由 `/etc/X11` 替换） |

## 管理文件和目录

正如前面提到的，使用 Linux 系统涉及导航子目录并操作其中的文件。因此，Linux 用户必须了解如何创建目录、将文件从一个目录复制或移动到另一个目录，以及删除文件。这些任务通常被称为文件管理。

# CompTIA Linux+ 与 LPIC-1：Linux认证指南

以下是 `root` 用户目录列表的示例：

```
[root@server1 ~]# pwd

/root

[root@server1 ~]# ls -F

myprogram* project12 project2 project4

myscript* project11 project3 project5

[root@server1 ~]#_
```

如上述输出所示，主目录下存在两个可执行文件（`myprogram` 和 `myscript`）以及几个与项目相关的文件（`project*`）。这种结构并不杂乱，主目录包含了许多文件。因此，根据文件的用途将这些文件组织到子目录是一个良好的习惯。由于在上述输出中，几个项目文件位于 `root` 用户的主目录下，你可以创建一个名为 `projfiles` 的目录，将项目相关文件复制进去，从而减少目录列表的大小。要执行此操作，请使用 `mkdir`（创建目录）命令，它接受指定目录绝对路径或相对路径的参数。若要在当前目录下创建一个 `proj_files` 目录，可以使用带有相对路径的 `mkdir` 命令：

```
[root@server1 ~]# mkdir proj_files

[root@server1 ~]# ls -F

myprogram* project12 project2 project4 proj_files/

myscript* project11 project3 project5

[root@server1 ~]#_
```

现在，你可以使用 `mv`（移动）命令将文件移动到 `proj_` 子目录中。该命令至少需要两个参数：源文件/目录和目标文件/目录。例如，要将 `/etc/sample` 移动到 `/root` 目录，可以使用命令 `mv /etc/sample /root`。如果你想移动多个文件，请为每个想要移动的文件包含一个源参数，并将目标目录作为最后一个参数。例如，要将 `/etc/sample` 和 `/etc/sample2` 移动到 `/root` 目录，可以使用命令 `mv /etc/sample /etc/sample2 /root`。注意，源（或多个源）和目标都是绝对路径或相对路径，如果移动了多个文件，源可以使用通配符文件。例如，要将所有项目文件移动到 `proj_files` 目录，你可以输入命令 `mv project* proj_files`（目标目录的相对路径），输出如下所示：

```
[root@server1 ~]# mv project* proj_files

[root@server1 ~]# ls -F

myprogram* myscript* proj_files/

project12 project2 project4

project11 project3 project5

[root@server1 ~]#_
```

在上述输出中，当前目录列表不再显示项目文件，但 `proj_files` 子目录的列表显示它们已成功移动。

如果目标是一个目录名称，`mv` 命令会将这些文件移动到该目录。如果目标是某个目录中已存在的文件名且只有一个源，`mv` 命令将用源覆盖目标。如果源是某个目录中不存在的文件名，`mv` 命令将在目录中以目标名称创建一个新文件并将源文件重命名为该名称。

# 第 4 章 Linux 文件系统管理

`mv` 命令的另一个用途是重命名文件，这简单来说是将文件移动到相同目录但使用不同的文件名。要将之前示例中的文件重命名为 `myscript2`，可以使用以下命令：

```
[server1]# ls -F

myprogram* myscript* proj_files/

[server1]# mv myscript myscript2

myprogram* myscript2* proj_files/

[server1]# ls -F

myprogram* myscript2* proj_files/

[server1]# _
```

同样，`mv` 命令也可以重命名目录。如果源是一个现有目录，它将按照指定的目标名称进行重命名。

`cp` 命令的工作原理类似于复制并粘贴操作，即文件被复制到新目录并从源位置删除。然而，在某些情况下，你可能希望保留源目录中的文件并在目标目录中插入该文件的副本。你可以使用 `cp`（复制）命令来实现此操作。与 `mv` 命令不同，`cp` 命令至少需要两个参数。第一个参数指定要复制的源文件，第二个参数是目标。如果需要将多个文件复制到目标目录，请指定每个源参数，最后一个参数将作为目标。每个文件都可以重命名，并可以包含空格或特殊字符（`.` 指定当前目录）以及 `..`（指定父目录）。如果你想在当前目录（`/root`）中创建 `/etc/hosts` 的副本，请使用相对路径：

```
[server1]# cp /etc/hosts .

[server1]# ls -F

hosts myprogram* myscript* proj_files/
```

等等，我忘记了你也可以在同一目录下创建文件的副本。例如，要在当前目录下创建 `hosts` 文件的副本并查看结果，你可以运行以下命令：

```
[server1]# cp hosts hosts2

[server1]# ls -F

hosts2 myprogram* myscript* proj_files/
```

同样，`mv` 和 `cp` 命令处理目录的方式不同。`mv` 命令重命名目录，而 `cp` 命令创建目录及其内容的新副本。在 Linux 中复制整个文件目录，必须使用带有 `-r` 选项的 `cp` 命令。以下示例演示了在带和不带 `-r` 参数将 `proj_files` 目录及其所有内容复制到 `/home/user` 目录：

```
[root@server1]# ls -F

hosts myprogram* myscript* proj_files/

[root@server1]# cp proj_files /home/user

[root@server1]# cp -r proj_files /home/user

[root@server1]# ls -F

hosts myprogram* myscript* proj_files/
```

*(注：原文示例代码块似乎不完整，此处已根据语境补充了逻辑演示)*

## CompTIA Linux+ 和 LPIC-1：Linux 认证指南

上述文件管理命令被 Linux 用户、开发者和管理员经常使用。表 4-2 显示了这些常用文件管理命令的摘要。

## 表 4-2 常用 Linux 文件管理命令

| 命令 | 说明 |
| --- | --- |
| `mkdir` | 创建目录 |
| `rmdir` | 删除空目录 |
| `mv` | 移动/重命名文件和目录 |
| `cp` | 复制文件和目录，使用 `-r` 或 `-R` 选项 |
| `alias` | 显示 BASH shell 别名 |
| `rm` | 删除文件和目录，使用 `-r` 或 `-R` 选项 |
| `unlink` | 删除文件 |

## 查找文件

在使用上一节提到的文件管理命令之前，你必须知道文件的位置。在目录树中搜索文件最快的方法是使用 `locate` 命令。例如，要查看根目录下所有包含 "initab" 文字或以 "initab" 为名的文件，可以在命令行提示符处输入 `locate initab`，产生如下输出：

```
[root@server1 ~]# locate initab

/etc/initab

/usr/share/archives/lenses/initab.aug

/usr/share/vim/vim80/syntax/initab.vim

[root@server1 ~]#
```

`locate` 命令在一个包含系统所有文件列表的数据库中查找。该数据库像教科书一样建立了索引以便快速搜索，但随着系统中文件的添加和删除（这是经常发生的），它可能会过时。因此，`locate` 命令使用的数据库（`/var/lib/locate/db`）每天会自动更新，也可以通过在命令行提示符处运行 `updatedb` 命令手动更新。你也可以通过将特定目录添加到 `/etc/updatedb.conf` 来排除它们；这是使用 `updatedb` 命令和修剪实现的。例如，要排除 `updatedb` 命令索引 `/etc` 目录，可以在 `/etc/updatedb.conf` 中添加行 `PRUNEPATHS=/etc`。

`locate` 命令搜索系统上的所有文件，但返回的信息太多，无法在屏幕显示。为了让输出更易读，可以使用 `more` 或 `less` 命令来管理输出；如果 `locate initab` 命令产生太多结果，你可以进行更具体的搜索。

在文件系统中查找文件的另一种方法是使用 `find` 命令。`find` 命令从某个目录开始递归搜索目录，或者搜索符合特定标准的文件。`find` 的格式如下：

```
find <起始目录> -criterion <要查找的内容>
```

例如，要查找目录下任何名为 "initab" 的文件，可以使用命令 `find /etc -name initab` 并接收如下输出：

```
[root@server1 ~]# find /etc -name initab

/etc/initab

[root@server1 ~]#
```

你也可以在 `find` 命令中使用元字符；然而，这些通配符必须防止其被严格解释，因为它们只能被 `find` 命令解释。为了做到这一点，请确保任何通配符元字符都包含在引号内。以下输出了使用 `find` 命令配合元字符查找 `/etc` 目录下所有以 "host" 字母开头文件的示例：

```
[root@server1 ~]# find /etc -name "host*"

/etc/hosts

/etc/host.conf

/etc/avahi/hosts

/etc/hostname

[root@server1 ~]#
```

虽然按名称搜索是 `find` 命令最常用的标准，但 `find` 命令也可以使用许多其他标准。要查找从 `/var` 目录开始的大小大于 8192(kil字节)的所有文件，请使用以下命令：

```
[root@server1 ~]# find /var -size +8192k

/var/lib/Packages

/var/lib/rpm/Basenames

/var/lib/Package-list

/var/log/journal/03a4ec8cdcf462af462a7243911116/user-1000.journal

/var/log/journal/03a4ec8cdcf462af462a724391111df6/user-42.journal

/var/log/journal/03a4ec8cdcf462af462a724391111df6/system.journal

/var/cache/Package/36/updates/gen/prestdelta.xml

/var/cache/Package/36/updates/primary_db.sqlite

/var/cache/Package/36/updates/gen/file_ists_db.sqlite

/var/cache/Package/36/updates/gen/updateinfo.xml

/var/cache/Package/36/updates/gen/other_db.sqlite

/var/cache/Package/36/fedora-filenames.solvx

/var/cache/dnf/x86_64/fedora.solvx

/var/cache/dnf/x86_64/updates-filenames.solvx

/var/tmp/kdecache-user1/plasma_theme_internal-system.kccache

/var/tmp/kdecache-user1/plasma_theme_Heisenberg_v19.90.2.kccache

[root@server1 ~]#
```

同样，如果你想查找 `/boot` 目录下的所有目录，可以使用以下命令：

```
[root@server1 ~]# find /boot -type d

/boot/extlinux
```
