
### 递归更改权限

这个示例展示了这种方法的关键优势。使用字母表示法需要分两步——先 `chmod go-w` 然后是 `chmod -r`（或 `chmod g=r` 和 `chmod o=`）——而使用数字表示法只需要一个命令。出于这个原因，你经常看到高级 Linux 用户使用表示法，因为它更快且似乎更精确。

#### chmod -R

你现在可能已经注意到许多 Linux 命令允许你将它们递归应用于文件和目录，`chmod` 也不例外。`-R`（或 `--recursive`）选项允许你在几秒钟更改数百个文件的权限，只需确保这是你想要做的。

```bash
$ pwd

/home/scott

$ ls -l

-rw-r--r-- 1 scott scott ... libby.jpg

drwxr-xr-x 2 scott scott ... pictures/

-rw-r--r-- 1 scott scott ... vacation.jpg

drwxr-xr-x 2 scott scott ... documents/

-rw-r--r-- 1 scott scott ... report.txt
```

如果你运行 `chmod -R 644 pictures`，它将递归地更改目录及其所有文件的权限。

```bash
$ chmod -R 644 pictures

$ ls -l

drw-r--r-- 2 scott scott ... pictures/

-rw-r--r-- 1 scott scott ... vacation.jpg
```

注意，这会导致目录失去可执行权限，因此你将无法进入该目录。要修复此，你需要为目录添加执行权限：

```bash
$ chmod -R 755 pictures

$ ls -l

drwxr-xr-x 2 scott scott ... pictures/

-rw-r--r-- 1 scott scott ... vacation.jpg
```

如果你只想递归地更改文件而不影响目录，可以使用 `find` 命令：

```bash
$ find pictures -type f -exec chmod 644 {} +

$ ls -l

drwxr-xr-x 2 scott scott ... pictures/

-rw-f--r-- 1 scott scott ... vacation.jpg
```

在第 10 章“find 命令”中了解更多信息。

### 设置并清除 suid

#### chmod u[+-]s

在“理解权限基础”部分中，你查看了多种可能的权限。你关注的是 `r`、`w` 和 `x`，因为它们是最常见的，但其他权限在某些时候派得上用场。

与 `suid` 密切相关的 `sgid` 可以同时应用于文件和目录。对于文件，`sgid` 就像 `suid`，区别在于用户可以使用组权限而不是所有者权限来执行文件。例如，在你的系统中，`crontab` 命令可能被设置为 `sgid`，这样用户就可以请求 `cron` 为他们运行程序，但使用的是受限的 `crontab` 组而不是强大的 `root` 用户。

```bash
$ ls -l /usr/bin/crontab

-rwsr-sr-x 1 root crontab ... /usr/bin/crontab
```

作为普通用户，你不太可能更改程序为 `suid`。大多数这与 `root` 拥有的程序有关，但在偶尔需要使用时，了解它仍然是好事。

## 第二部分：文件操作

假设你有三个用户：`Alice`、`Bob` 和 `Carol`，他们都是 `admins` 组的成员。`Alice` 的用户名是 `alice`，她的主组也是 `alice`，这在 Linux 系统中是非常常见的现象。`Bob` 和 `Carol` 遵循相同的模式，他们的用户名和主组分别为 `bob` 和 `carol`。如果 `Alice` 在 `admins` 组共享的目录中创建一个文件，该文件的所有者和所属组将是 `alice`，这意味着 `admins` 组的其他成员无法对其进行写入。当然，`Alice` 在创建新文件后可以运行 `chown`（`chown admins document`），但这会变得极其繁琐。

然而，如果将共享目录设置为 `sgid`，那么在该目录下创建的任何新文件所有者仍然是创建它的用户，但在这种情况下，组是 `admins`。结果是，`Bob` 和 `Carol` 也可以读取和编辑该共享目录中的任何文件，而且减少了繁琐程度。

惊讶的是，你可以使用字母或数字设置 `sgid`。使用字母时，`sgid` 就像 `suid` 一样，只是使用了 `s`。让我们看看应用于目录的 `sgid`，但请记住，相同的过程也适用于文件。

```
$ ls -lf

drwxr-xr-x 11 admins ... /bin/

$ chmod g+s bin

$ ls -lf

drwxr-xr-x 11 admins ... /bin/
```

### 注意

你可能会同时看到 `s` 和 `S` 来表示设置了 `sgid`。如果你在设置 `sgid` 之前组已经有了执行权限（`x`），则你会看到 `s`；如果你在设置 `sgid` 之前组没有执行权限，则你会看到 `S`。最终结果是相同的，但大小写可以了原始的权限状态。

移除 `sgid` 几乎与添加它完全相反。

```
$ ls -lf

drwxr-xr-x 11 admins ... /bin/

$ chmod g-s bin

$ ls -lf

drwxr-xr-x 11 admins ... /bin/
```

如果你还没有读过之前的章节“设置和清除 suid”，请回去读一下，因为它解释了出现在所有者权限数字之前的那个神秘的第四位。在 `suid` 的情况下，该数字是 `4`；对于 `sgid`，数字是 `2`。

```
$ ls -lf

drwxr-xr-x 11 admins ... /bin/

$ chmod 2755 bin

$ ls -lf

drwxr-xr-x 11 admins ... /bin/
```

你通过移除 `suid` 的相同移除 `sgid`：在开头使用一个 `0`，这会让 `sgid` 消失。

```
$ ls -lf

drwxr-sr-x 11 scott admins ... bin/

$ chmod 0755 bin

$ ls -lf

drwxr-xr-x 11 scott admins ... bin/
```

### 注意

你知道在 `sgid` 目录中创建新文件会发生什么，但请注意其他文件系统进程也会受到 `sgid` 的影响。如果你用 `cp` 将文件复制到 `sgid` 目录，它将获得该目录的组。然而，如果你用 `mv` 将文件移动到 `sgid` 目录，它将保留当前的组所有权，而不会获得目录组的所有权。最后，如果你使用 `mkdir` 在 `sgid` 目录内部创建一个新目录，它不仅会继承拥有 `sgid` 目录的组，本身也会变成 `sgid`。

### 设置并清除粘滞位（Sticky Bit）

```
chmod [+]-t
```

除了这是一个朗朗上口的短语外，粘滞位是什么？在 Unix 的旧时代，如果一个可执行文件设置了粘滞位，操作系统就知道该文件将不断运行，因此会将其保留在交换空间中，以便快速高效地访问。Linux 是一个更现代的系统，因此当在文件上设置粘滞位时它会忽略它。

这意味着粘滞位用于目录。在文件夹中设置粘滞位后，除非用户是文件的所有者或粘滞位目录的所有者，否则无法删除或重命名该文件夹中的文件。如果没有设置粘滞位且文件夹对其他人可写，这意味着那些用户可以删除和重命名其中的任何文件。粘滞位防止了这种情况发生。你最常看到它的地方是 `/tmp` 目录，它设计上对所有人可写，但 `/tmp` 内部的单个文件和文件夹受粘滞位的保护，其他用户无法操作。

```
$ ls -t /

drwxrwt 12 root root ... tmp

[结果截断]
```

### 注意

你可能会同时看到 `a` 和 `T` 来表示设置了粘滞位。如果你在设置粘滞位之前世界已经有了执行权限（`x`），则你会看到 `t`；如果你在设置粘滞位之前世界没有执行权限，则你会看到 `T`。结果是相同的，但大小写可以了原始的权限状态。

与本章中许多其他使用 `chmod` 的示例一样，可以使用字母或数字设置粘滞位。

```
$ ls -lF

drwxrxr-x 2 scott family ... libby_pix/

$chmod +t libby_pix

$ ls -lF

drwxrxr-t 2 scott family ... libby_pix/
```
