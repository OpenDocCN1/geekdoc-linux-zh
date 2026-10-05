
# 第 8 章：操作文件与命令

另一个专门用于删除空目录的命令是 `rmdir`。该目录必须为空才能被删除。如果你尝试在不删除其文件的情况下删除 `work` 目录，系统会显示以下消息：

```
maddog@shamet:~ > rmdir work
rmdir: work: Directory not empty
maddog@shamet:~ > rm -rf work
```

# 我赋予权限

Linux 中的文件和目录拥有所有者，并被分配一组权限。这种所有权和权限系统构成了限制和允许访问文件的基础。权限还可以用于判断一个文件是否可以作为命令执行，以及你如何使用该文件或命令。了解这一点很重要，因为如果你是系统的唯一使用者，那么命令和数据库也会被其他用户（包括 `root`，即超级用户）使用。这些文件的权限允许或禁止你（普通用户）更新这些文件。

使用 `ls -l` 选项可以让你查看文件的权限以及相关信息，例如谁拥有该文件、哪些组的人有权访问或修改文件、文件或目录的大小、文件最后修改的时间以及文件名。

首先，使用 `touch` 命令创建一个文件。`touch` 命令在 UNIX 和 Linux 社区中有许多用途，其中一个用途就是轻松创建一个长度为零的小文件：

```
maddog@shamet:~ > touch partytime
maddog@shamet:~ > ls -l partytime
-rw-r--r-- owner group 0 Oct 31 16:00 partytime
```

`-rw-r--r--` 是 `partytime` 文件的权限；所有者是 `owner`，根据你系统的设置和管理，你可能可能是其他人或其他其他东西。

你可能会好奇如何成为一个文件的所有者。事实上，你创建的任何文件自动成为所有者，这是合理的。作为所有者，你可以更改默认权限以及所有权。如果你更改了文件所有权，就会失去所有权权限。

要更改文件或目录的所有权，请使用 `chown` 命令。（懂了吗？`chown` — change ownership，更改所有权。）假设你决定安定下来，过上更沉静的生活，更符合俳句写作这一新职业。其他人将不得不负责周末的狂欢和通宵派对。因此，你放弃了 `partytime` 文件的所有权：

```
maddog@shamet:~ > chown root parttime
```

这把 `parttime` 的所有者更改为了 `root`。如果你想改回来，可以使用 `chown` 命令，但必须以 `root` 身份执行。

![](img/96a9ce6a13d8d15ed05f867f41574278_173_0.png)

在某些 Linux 安装中，你无法使用 `chown` 命令将文件送给别人。你会收到一条错误消息，提示操作不允许（Operation is not permitted）。一些系统管理员认为 `chown` 命令存在安全风险。因此，只有超级用户才能执行 `chown` 命令。如果你拥有发行版之一（《SuSE Linux For Dummies》光盘就是其中之一）并想把文件给别人，我们建议让对方复制文件，创建一个由他们自己拥有的文件。

文件和用户属于不同的组。在 `parttime` 示例中，组是 `users`。设置组允许让你赋予大量用户（而非所有用户）访问权限。组权限和所有权对于确保特殊项目或工作组的成员能够访问整个组所需的文件非常有用。

要查看系统中可用的哪些组，请查看 `/etc/group` 文件。操作时使用 `more` 命令。你会看到一个类似这样的文件：

```
root::0:root
bin::1:1:root,daemon
nobody::99:
users::100:your-user-name, maddog
floppy:x:19:
...
your-user-name:500:your-user-name
```
