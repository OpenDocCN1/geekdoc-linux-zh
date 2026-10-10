
在上一章中，您学习了如何导航 Linux 文件系统以及如何查看和编辑文件。本章重点介绍 Linux 文件系统上文件的组织方式以及它们的链接和安全机制。首先，您将使用文件系统层次结构标准（Filesystem Hierarchy Standard）来探索标准的 Linux 目录。接下来，您将探索用于管理文件和目录的常用命令，并学习在文件系统上查找文件和目录的方法。最后，您将学习文件和目录的链接、权限、特殊权限以及属性。

## 文件系统层次结构标准

典型 Linux 系统上的成千上万个文件被组织到 Linux 目录树中的目录里。这是一个复杂的系统，过去由于不同的 Linux 发行版可以自由地将文件放置在不同的位置，这使得情况变得更加复杂。这意味着，当您在一个不熟悉的 Linux 系统上查找配置文件时，可能会花费大量时间。为了简化查找特定文件的任务，创建了文件系统层次结构标准（FHS）。

FHS 定义了一组标准的目录，供所有 Linux 和 UNIX 系统使用，以及每个目录中的文件和子目录内容。这确保了由于文件名和位置遵循标准约定，Fedora Linux 用户可以在 SuSE Linux 或 Hewlett-Packard UNIX 计算机上轻松地找到正确的配置文件。FHS 还使 Linux 软件开发者能够在任何发行版上定位 Linux 系统上的文件，从而允许他们创建不特定于某个发行版的软件。

全面理解 Linux 系统上找到的标准目录类型对于定位和管理文件和目录非常有用；FHS 定义的一些标准 UNIX 和 Linux 目录及其描述见表 4-1。这些目录将在本章及后续章节中详细讨论。

![](img/c27875544958897d817484d558c208c8_165_0.png)

要阅读完整的文件系统层次结构标准定义，请访问 http://refspecs.linuxfoundation.org/fhs.shtml。

### 管理文件和目录

如前所述，使用 Linux 系统涉及导航多个目录并操作其中的文件。因此，高效的 Linux 用户必须了解如何根据需要创建目录，将文件或目录从一个目录复制或移动到另一个目录，以及删除文件和目录。这些任务通常被称为文件管理任务。

以下是一个示例，显示了以 root 用户登录的用户看到的目录列表：

```
[root@server1 ~]# pwd
/root
[root@server1 ~]# ls -F
current@ myprogram* project  project12 project2 project4
Desktop/ myscript  project1  project13 project3 project5
[root@server1 ~]#
```

| 目录 | 描述 |
| :--- | :--- |
| /bin | 包含供所有用户使用的二进制命令 |
| /boot | 包含 Linux 内核和引导加载程序使用的文件 |
| /dev | 包含设备文件 |
| /etc | 包含系统特定的配置文件 |
| /home | 是用户主目录的默认位置 |
| /lib | 包含共享程序库（由 /bin 和 /sbin 中的命令使用）以及内核模块 |
| /media | 一个包含用于访问（挂载）可移动媒体设备（如软盘、DVD 和 USB 闪存驱动器）上文件系统的子目录的目录 |
| /mnt | 一个用于临时访问可移动媒体设备上文件系统的空目录 |
| /opt | 存储额外的软件程序 |
| /proc | 包含进程和内核信息 |
| /root | 是 root 用户的主目录 |
| /sbin | 包含系统二进制命令（用于管理） |
| /tmp | 保存程序创建的临时文件 |
| /usr | 包含大多数系统命令和实用程序——包含以下目录：/usr/bin—用户二进制命令 /usr/games—教育程序和游戏 /usr/include—C 程序头文件 /usr/lib—库 /usr/local—本地程序 /usr/sbin—系统二进制命令 /usr/share—与架构无关的文件 /usr/src—源代码 /usr/X11R6—X 窗口系统（有时被 /etc/X11 替代） |
| /usr/local | 是大多数额外程序的位置 |
| /var | 包含日志文件和 spools |

**表 4-1** 由文件系统层次结构标准定义的 Linux 目录

如前面输出所示，此示例系统中只有一个目录（Desktop）、两个可执行文件（myprogram 和 myscript）以及几个与项目相关的文件（project）。虽然这个目录结构并不杂乱，且在终端屏幕上显示为易于阅读的格式，但 Linux 系统上的典型主目录包含更多的文件；典型的 Linux 用户的主目录中可能有超过 100 个文件。因此，根据文件用途将这些文件组织到子目录中是一个好习惯。由于前面输出中 root 用户的主目录中有几个项目文件，您可以创建一个名为 proj_files 的子目录来包含与项目相关的文件，从而减少目录列表的大小。为此，您使用 **mkdir**（make directory）命令，该命令接受指定要创建的目录的绝对或相对路径名的参数。要在当前目录下创建一个 proj_files 目录，您可以使用带有相对路径名的 **mkdir** 命令：

```
[root@server1 ~]# mkdir proj_files
[root@server1 ~]# ls -F
```

```
current@ myprogram* project project12 project2 project4 proj_files/  
Desktop/ myscript* project1 project13 project3 project5
[root@server1 ~]#
```

现在，您可以使用 mv（move）命令将项目文件移动到 proj_files 子目录中。mv 命令至少需要两个参数：源文件/目录和目标文件/目录。例如，要将 /etc/sample1 文件移动到 /root 目录，您可以使用命令 mv /etc/sample1 /root。

如果您想移动多个文件，您为每个要移动的文件包含一个源参数，然后包含目标目录作为最后一个参数。例如，要将 /etc/sample1 和 /etc/sample2 文件移动到 /root 目录，您可以使用命令 mv /etc/sample1 /etc/sample2 /root。

请注意，源（或源）和目标可以是绝对或相对路径名，如果要移动多个文件，源可以包含通配符。例如，要将所有项目文件移动到 proj_files 目录，您可以输入带有源参数 project*（以匹配所有以字母 "proj" 开头的文件）和目标参数 proj_files（到目标目录的相对路径名）的 mv，如下面的输出所示：

```
[root@server1 ~]# mv project* proj_files
[root@server1 ~]# ls -F
current@ Desktop/ myprogram* myscript* proj_files/
[root@server1 ~]# ls -F proj_files
project project1 project12 project13 project2 project3 project4 project5
[root@server1 ~]#
```

在前面的输出中，当前目录列表不再显示项目文件，但 proj_files 子目录的列表表明它们已成功移动。

![](img/c27875544958897d817484d558c208c8_167_0.png)

如果目标是目录的名称，mv 命令将那些文件移动到该目录。如果目标是某个目录中现有文件的文件名，且只有一个源文件，mv 命令将用源覆盖目标。如果目标是某个目录中不存在文件的文件名，mv 命令会在目标目录中创建一个具有该文件名的新文件，并将源文件移动到该文件。

mv 命令的另一个重要用途是重命名文件，这实际上是将文件移动到同一目录但使用不同的文件名。要将前面示例中的 myscript 文件重命名为 myscript2，您可以使用以下 mv 命令：

```
[root@server1 ~]# ls -F
current@ Desktop/ myprogram* myscript* proj_files/
[root@server1 ~]# mv myscript myscript2
[root@server1 ~]# ls -F
current@ Desktop/ myprogram* myscript2* proj_files/
[root@server1 ~]#
```

类似地，mv 命令可以重命名目录。如果源是现有目录的名称，它将被重命名为指定为目标目录名的任何目录名称。
