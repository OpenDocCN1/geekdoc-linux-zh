
在 Linux 下，目录是文件。例如，在一个目录中，如果你检查一个目录，你将看到以下内容：

```
drwxr-xr-x root root 4096 Oct 12 10:00 /home/matthew
```

在这个示例中，`d` 表示目录。`rwxr-xr-x` 表示所有者具有读、写、执行权限，而组和其他人只有读取和执行权限。

例如，如果你检查像 `/home` 这样的目录，你将看到以下内容：

```
drwxr-xr-x root root 4096 Oct 12 10:00 /home
```

这显示所有者可以读、写、执行，而组和其他人只能读取和执行。

### 权限操作

权限集仅适用于你（所有者）。你可以通过使用 `chmod`、`-` 和 `aw` 来移除任何所有人的写权限，如下所示：

```
matthew@seymour:-$ chmod a-w readme.txt
matthew@seymour:-$ ls -1 readme.txt
-r-r-r-- 1 matthew 2010-06-30 13:33 readme.txt
```

现在，任何人都可以写入该文件（如果你正处于 `/home` 或 `/tmp` 目录，由于目录权限限制）。要恢复仅适用于你作为所有者的写权限，可以使用加号 `+` 和 `rw` 选项，如下所示：

```
matthew@seymour:-$ chmod u+rw readme.txt
matthew@seymour:-$ ls -1 readme.txt
-rw-r--r-- 1 matthew 2010-06-30 13:33 readme.txt
```

你还可以使用 `chmod` 命令的八进制形式（例如，修改文件的权限，使得只有你作为所有者可以读取和写入文件）。使用如下的 `chmod` 命令和文件：

```
matthew@seymour:-$ chmod 600 readme.txt
matthew@seymour:-$ ls -1 readme.txt
-------- 1 matthew 2010-06-30 13:33 readme.txt
```

如果你剥夺了目录的执行权限，其中的文件可能会被隐藏，并且其他人无法列出或访问它们（当然，root 操作员除外，他拥有访问你系统上任何文件的权限）。通过使用各种权限设置组合，你可以快速方便地建立一个更安全的环境，即使是作为普通用户的 `/home` 目录也是如此。

## 使用 chgrp 管理文件权限

你可以使用 `chgrp` 命令更改文件所属的组：

```
matthew@seymour:-$ chgrp wheel filename
```

## 使用 chown 更改文件权限

你可以使用 `chown` 命令更改文件的所有者：

```
matthew@seymour:-$ chown matthew filename
```

你也可以同时使用 `chown` 命令更改文件的所属组：

```
matthew@seymour:-$ chown matthew:wheel filename
```

## 理解设置用户 ID 和设置组 ID 权限

两种权限类型是“设置用户 ID”（set user ID，称为 suid）和“设置组 ID”（set group ID，称为 sgid）。这些设置在程序中使用时，允许任何运行该程序的用户都拥有该程序的所有者权限或组所有者权限。

### 第 9 章 命令行快速上手

这些设置允许所有人运行该程序，而无需修改每个用户的权限以包含针对该程序的特定权限。

通常与 `su` 权限配合的一个常用命令是 `passwd` 命令：

```
matthew@semourn:-$ ls -l /usr/bin/passwd
-rwxr-xr-x 1 root 42856 2010-01-26 10:09 /usr/bin/passwd
```

此设置允许用户执行该命令（以 root 身份），以修改仅限 root 访问的文件 `/etc/passwd`。

你还可以使用 `chfn` 命令分配权限。该命令允许用户更新或更改 `/etc/passwd` 中的 finger 信息。你通过在三个八进制值前面加上 4（或助记符 a）来完成这种权限修改。

> 其他可能具有 suid 或 guid 权限的文件包括 at, rcp, login, rsh, chage, csh, ssh, crontab, sudo, sendmail, ping, mount 以及若干个 UNIX-to-UNIX 拷贝 (UCP) 实用。许多程序（如游戏）也可能具有此类权限来访问源设备。

具有 suid 或 guid 权限的文件或程序有时会带来安全漏洞，因为它们绕过了普通权限。如果权限扩展到具有固有安全缺陷的可执行二进制文件（命令），此问题会变得更加严重，因为可能导致任何系统用户或入侵者获得 root 权限。在漏洞利用中，这通常发生在用户在意外输入（如长路径名或选项）下使用脆弱的命令时；命令将失败，用户将看到 root 提示符。尽管 Linux 开发者一直在寻找糟糕的编程实践，但新的漏洞总是在被发现，并可能意想不到地出现，特别是在那些没有经过同行开发者审查的新版软件包中。

精明的 Linux 系统管理员会将系统上的 suid 或 guid 文件数量减少到最少。`find` 命令可以用于显示系统上的所有文件：

```
matthew@seourn:-$ sudo find -type f -perm /6000 -exec ls -1 {} \
```

> `find` 命令非常有用，可以用于许多用途，例如在操作或备份操作之前。

注意，这些程序并不非要从你的系统中移除。如果你的用户不需要使用该程序，你可以移除所有人的执行权限。作为 root 操作员，你必须决定是否允许用户在你的系统上挂载和卸载 CD-ROM 或其他媒体。虽然基于 Linux 的操作系统可以配置得易用且方便，但允许像 mount 这样的程序可能不是最佳的安全策略。其他 suid 权限更改的候选对象可能包括 chsh, at 或 charge 命令。

## 文件操作

在家目录中管理文件涉及使用一个或多个易记的命令。

### 使用 touch 创建文件

若要在当前目录下创建一个名为 `filename` 的空文件，请使用以下命令：

```
matthew@seymour:- touch filename
```

若要编辑此文件，你必须使用文本编辑器。第 12 章“自动化任务和 Shell 脚本”中讨论了若干种编辑器。然而，由于文件与时间、日期信息相关，创建一个带有访问记录的空文件有时是有用的的。你也可以使用 `touch` 更新这些信息（称为时间戳），而无需实际访问或修改文件。

你可以通过更改 `touch` 之后的内容在不同位置创建新文件。如果我已经在家目录中，要在 `/home/matthew/randomdirectory` 中创建一个新文件，我可以使用以下命令：

```
matthew@seymour:- touch randomdirectory/newfile
```

或者从任何地方使用绝对路径，我使用这个：

```
matthew@seymour:- touch /home/matthew/randomdirectory/newfile
```

或者从任何地方使用路径快捷方式，我使用以下命令：

```
matthew@seymour:- touch /randomdirectory/newfile
```

### 使用 mkdir 创建目录

若要在当前目录下创建一个名为 `newdirectory` 的空目录，请使用此命令：

```
matthew@seymour:- mkdir newdirectory
```

你可以通过更改 `mkdir` 之后的内容在不同位置创建目录。若要在 `/home/matthew/music` 中创建一个新目录，如果我已经在家目录中，我可以使用以下命令：

```
matthew@seymour:- mkdir music/newdirectory
```

### 156 第 9 章 命令行快速上手

或者从任何地方使用绝对路径，我使用这个：

```
matthew@semour:-$ mkdir /home/matthew/music/newdirectory
```

或者从任何地方使用路径快捷方式，我使用以下命令：

```
matthew@semour:-$ mkdir /music/newdirectory
```

`-p` 参数非常有价值。它允许在父目录不存在时同时创建它们。如果父目录已存在，该命令将正常工作。例如，假设我想创建一个带有两层子目录的新目录。在示例中，music 和 newdirectory 已存在，但要创建 subdir1 和 subdir2：

```
matthew@seymour:-$ mkdir -p /music/newdirectory/subdir1/subdir2
```

### 使用 rmdir 删除目录

若要删除空 `directoryname`，请使用以下命令：

```
matthew@seymour:-$ rmdir directoryname
```

你可以通过更改 `rmdir` 之后的内容在不同位置移除目录。若要在 `/home/matthew/music` 中移除目录，如果我已经在家目录中，我可以使用以下命令：

```
matthew@seymour:-$ rmdir music/directoryname
```

或者从任何地方使用绝对路径，我使用这个：

```
matthew@seymour:-$ rmdir /home/matthew/music/directoryname
```

或者从任何地方使用路径快捷方式，我使用以下命令：

```
matthew@seymour:-$ rmdir /music/directoryname
```

目录必须为空才能使用 `rmdir` 移除。然而，有一种方法可以使用 `rm` 移除包含其内容的目录。

> 警告

使用 `rmdir` 或 `rm` 删除的内容无法轻易恢复，因此请谨慎操作。在删除之前，请务必确定你永远不再需要要删除的内容。只有专业的数据恢复服务可能恢复文件，即使如此代价也高昂。

#### 使用 rm 删除文件或目录

要删除名为 `filename` 的文件，请使用此命令：

```
matthew@seymour:-$ rm filename
```

你可以通过更改 `rm` 之后的内容来删除不同位置的目录。如果我已经在 `/home` 目录下，想要删除 `/home/matthew/randomdirectory` 下的目录，可以使用以下命令：

```
matthew@seymour:-$ rm randomdirectory/filename
```

或者从任何地方使用绝对路径进行操作，我可以使用此命令：

```
matthew@seymour:-$ rm /home/matthew/randomdirectory/filename
```

或者从任何地方使用快捷路径进行操作，可以使用以下命令：

```
matthew@seymour:-$ rm ~/randomdirectory/filename
```

如果你尝试使用 `rm` 删除一个空目录，将收到错误信息：`rm: cannot remove '/':':`。在这种情况下，你必须使用 `rmdir`。然而，你可以使用 `rm` 删除目录及其内容。

> 注意

> 如果你选择删除目录内容，请务必确保该目录的内容是你已知且是不需要的。之后将无法恢复它们。此外，要小心不要产生多余的空格、输错目录名称，或使用 `sudo` 删除你不应该删除的内容。Linux 赋予了你巨大的力量，它会让你使用这种力量而不会对其加质疑；那是人类的工作。

要删除一个目录及其内容，请使用 `-R` 递归开关。此方法适用于许多命令，而不仅仅是 `rm`：

```
matthew@seymour:-$ rm -R /home/matthew/randomdirectory/
```

`randomdirectory` 中的所有内容以及目录本身都将被删除。

#### 使用 mv 移动或重命名文件

在 Linux 中，移动文件和重命名文件是同一件事。无论你是将目录移动到另一个目录，还是在同一目录下从一个文件名移动到另一个文件名，只需要记住一个命令。要将名为 `filename` 的文件从 `~/documents/archive` 移动，请使用此命令：

```
matthew@seymour:-$ mv documents/filename archive
```

注意，目标路径中不包含文件名。此处的目标必须是一个已存在的目录。如果不是，文件将被重命名为所使用的术语。一些示例可以清楚地说明这一点。

要重命名当前目录下的文件，我可以使用以下命令：

```
matthew@seymour:-$ mv oldfilename new
```

要在将文件从 `~/documents` 移动到 `~/archive` 的同时对其重命名，可以使用这个：

```
matthew@seymour:-$ mv documents/oldfilename archive/newfilename
```

或者从任何地方使用绝对路径进行操作，可以使用以下命令：

```
matthew@seymour:-$ mv /home/matthew/documents/oldfilename /home/matthew/archive/newfilename
```

或者从任何地方使用路径快捷方式进行操作，可以使用这个：

```
matthew@seymour:-$ mv ~/documents/oldfilename ~/archive/newfilename
```

#### 使用 cp 复制文件

复制的操作与移动类似，但会在原位置保留副本。要将名为 `filename` 的文件从 `~/documents` 复制到 `~/archive`，请使用此命令：

```
matthew@seymour:-$ cp documents/filename archive
```

注意，目标路径中不包含文件名。此处的目标必须是一个已存在的目录。如果不是，文件将被重命名为所使用的术语。一些示例可以清楚地说明这一点。

要复制当前目录下的文件，可以使用以下命令，效果与 `mv` 完全相同，不同的是操作后两个文件都存在：

```
matthew@seymour:-$ cp oldfilename newfilename
```

要在将文件从 `~/documents` 复制到 `~/archive` 的同时对其重命名，可以使用这个：

```
matthew@seymour:-$ cp documents/oldfilename archive/newfilename
```

或者从任何地方使用绝对路径进行操作，可以使用以下命令：

```
matthew@seymour:-$ cp /home/matthew/documents/oldfilename /home/matthew/archive/newfilename
```

或者从任何地方使用路径快捷方式进行操作，我可以使用这个：

```
matthew@seymour:-$ cp ~/documents/oldfilename ~/archive/newfilename
```

#### 使用 cat 显示文件内容

要在屏幕上查看文本文件 `filename` 的内容，请使用此命令：

```
matthew@seymour:-$ cat filename
```

注意，文本会显示在你的屏幕上，但你无法以任何方式编辑或处理该文本。当你只想知道文件内容但不需要进行任何更改时，这个命令非常方便。终端文本编辑器将在第 10 章“命令行大师课”中介绍。此命令对于短文件效果最好，因为大文件的内容滚动过屏幕的速度太快，来不及阅读。

#### 使用 less 显示文件内容

当你需要从命令行查看较长文本文件的内容时，可以使用 `less`。它会产生分页输出，这意味着输出每次屏幕填满时都会停止。你可以使用上、下方向键以及翻页键和下翻页键来滚动查看文件内容。然后，使用 `q` 退出并返回命令行：

```
matthew@seymour:-$ less filename
```

在 UNIX 早期，有一个程序可以提供更多的分页输出。它是第一个分页输出程序，但不包含向上或向下滚动的能力。`less` 的编写是为了增加这些功能。

#### 使用通配符和正则表达式

Linux 壳（shells）识别许多类型的通配符。例如，要删除当前目录下的所有文件，使用星号 `*`：

```
matthew@seymour:-$ rm *
```

你可以在第 10 章“命令行大师课”以及第 12 章“自动化任务与脚本”中学习更多关于表达式的内容。

## 以 Root 用户工作

Root 或超级用户账户是 UNIX 和 Linux 系统上的一个特殊账户和用户。编辑系统文件需要超级权限。你必须拥有 root 权限才能访问或修改设备（如硬盘）。以 root 身份登录时，一个简单的 `rm` 命令即可破坏系统：

```
matthew@seymour:~ sudo rm -rf /
```

只有在配置系统时才以 root 身份运行 Linux。在 Ubuntu 中，你可以使用 `sudo` 以 root 身份执行单个命令并快速返回用户状态。例如，如果你想编辑文件系统表（描述本地或远程存储设备及其类型、位置的文件），可以这样使用 `sudo`：

```
matthew@seymour:-$ sudo nano -w /etc/fstab
```

按下回车键后，会提示输入密码以获取 root 权限。这个额外的步骤也可以帮助你在操作前先思考。

## 理解和修复 sudo

大多数 Ubuntu 用户在这里不会遇到问题，但有时，喜欢实验的人会在学习过程中破坏东西。本节旨在帮助你首先

### 以 root 身份工作

完全理解 sudo 的工作原理，并当由于某种原因 sudo 对某个特定用户停止工作时，了解如何恢复该用户的 sudo 访问权限。

#### 注意

你通常会知道问题发生了，因为当用户尝试执行带有 `sudo` 命令时，会出现类似这样的错误信息：

```
matthew@seymour:-$ sudo shutdown -h now
[sudo] password for matthew:
```
