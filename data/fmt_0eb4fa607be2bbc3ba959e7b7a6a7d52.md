
```
$ ls
Desktop Documents Downloads Pictures Public Templates
Videos
$ ls -a
Desktop gnome2_private .lesshst Public
Documents Downloads gnome local Templates
.bash_history gnupg mozilla Videos
.bash_logout emacs gstreamer-0.10 Music xsession-errors
.bash_profile .esdh .gtk-bookmarks Pictures zshrc
fsync.log .gvs Pictures
.bashrc
$ uname
Linux
$ uname -a
Linux mydesktop 5.3.7-301.fc3.x86_64 #1 Mon Oct 21 19:18:58 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
$ date
Wed 04 Mar 2020 09:06:25 PM EST
$ date +%d/%m/%y
04/03/20
$ date +%A, %B, %Y
Wednesday, March 04, 2020
```

`ls` 命令本身会显示当前目录下的所有文件和目录。通过添加 `-a`，你还可以看到目录中的隐藏文件（那些以点开头的文件）。`uname` 命令显示你正在运行的系统类型（Linux）。当你添加 `-a` 时，还可以看到主机名、内核发行版本和内核版本。

## 第三章：使用 Shell

`date` 命令具有特殊类型的选项。单独使用 `date` 只是打印当前的日期和时间，如上所示。但 `date` 命令支持一个特殊的 `+` 格式选项，它可以让你以不同的格式显示日期。输入 `date --help` 查看你可以使用的不同格式指示符。

尝试使用 `id` 命令来感受你当前的 Linux 环境，如下文所示。

当你登录到 Linux 系统时，Linux 将你视为具有特定的身份，其中包括你的用户名、组名、用户 ID (`uid`) 和组 ID (`gid`)。Linux 还会跟踪你的登录会话：你何时登录、空闲了多久，以及在哪里登录的。

要查找有关你身份的信息，请如下所示使用 `id` 命令：

```
$ id
uid=1000(chris) gid=1000(chris) groups=1005(sales), 7(lp)
```

在这个示例中，用户 chris 由数字用户 (`uid`) 1000 表示。chris 的主组名为 chris，其组 ID (`gid`) 为 1000。Fedora 和红帽企业 Linux (`Red Hat Enterprise Linux`) 的主组名与其用户名相同是正常现象。用户 chris 还属于其他组 sales (`gid` 1005) 和 lp (7)。这些名称和数字代表了 chris 访问计算机资源的权限。

> 注意：启用了安全增强型 Linux (`SELinux`) 的 Linux 发行版（如 Fedora 和红帽）会在 `id` 输出的末尾显示额外信息。该输出可能像所示：
>
> context=unconfined_u:unconfined_r:unconfined_t:s0-c0.c1023
>
> `SELinux` 提供了一种紧密锁定 Linux 系统安全性的方法。如果你想学习 `SELinux`，请参阅第 24 章“使用 `SELinux` 增强 Linux 安全性”。

你可以使用 `id` 命令找到有关当前登录会话的信息。`-u` 选项表示添加有关空闲时间和进程 ID (`PID`) 的信息，而 `-H` 则请求打印头部信息：

```
$ id -UH
NAME  TIME                IDLE PID COMMENT
chris tty         Jan 13 20:57      2019
```

此 `id` 命令的输出显示用户 chris 登录在 tty1（这是连接到计算机的显示器上的第一个虚拟控制台），他的会话于 1 月 13 日 20:57 开始。IDLE 时间显示 shell 在没有输入任何命令的情况下已打开了多久（点表示它当前处于激活状态）。PID 显示用户登录 shell 的进程 ID。如果用户是从网络上的另一台计算机登录的，COMMENT 将显示远程计算机的名称；如果该用户使用的是终端窗口（例如 :0.0），则将显示本地 X 显示器的名称。

### 查找命令

现在你已经有了一些命令，你可能好奇它们位于哪里以及 shell 是如何找到它们的。当你输入一个命令时，shell 会在 `PATH` 变量列出的目录中搜索它。如果未在这些目录中找到该命令，shell 将报错。要查看 `PATH` 中包含哪些目录，请输入：

```bash
$ echo $PATH
```

输出将是冒号分隔的目录列表。shell 会按照它们列出的顺序搜索这些目录。如果命令在多个目录中存在，将执行第一个列出的那个。

要确定命令的位置，你可以使用 `type` 命令。该命令提供了有关命令如何被解释的信息：它是别名、shell 保留字、内置命令还是文件系统命令。例如，查找 bash 命令的位置，输入：

```bash
$ type bash
bash is /bin/bash
```

# 第二部分：成为 Linux 高级用户

> 提示：有时你运行一个命令时，会收到错误消息，提示未找到命令或拒绝运行该命令的权限。如果未找到命令，请检查命令拼写是否正确，以及该命令是否位于你的 `PATH` 变量中。如果拒绝运行该命令的权限，该命令可能在 `PATH` 变量中但不可执行。此外请记住大小写是敏感的，输入 `CAT` 或 `Cat` 都无法找到 `cat` 命令。

如果一个命令不在你的 `PATH` 变量中，你可以使用 `locate` 命令来找到它。使用 `locate`，你可以搜索你所访问的系统任何部分。（某些文件只有 root 用户可以访问）。例如，如果你想找到某个命令的位置，可以输入以下内容：

```
$ locate chage
/usr/bin/chage
/usr/sbin/lchage
/usr/share/man/fr/man1/chage.1.gz
/usr/share/man/it/man1/chage.1.gz
/usr/share/man/man1/chage.1.gz
/usr/share/man/man1/chage.1.gz
/usr/share/man/man1/lchage.1.gz
/usr/share/man/pl/lchage.1.gz
/usr/share/man/ru/man1/chage.1.gz
/usr/share/man/sv/man1/chage.1.gz
/usr/share/man/tr/man1/chage.1.gz
```

注意，`locate` 不仅找到了命令，还找到了 `locate` 本身以及针对不同语言的 chage 相关的各种 man 页。`locate` 命令可以查找你所有的文件，而不只是包含命令的目录。（如果 `locate` 没有找到最近添加到系统的文件，请以 root 身份运行 `updatedb` 来更新 locate 数据库。）

在接下来的章节中，你将学习使用额外的命令。现在，我想让你更熟悉 shell 本身是如何工作的。因此，接下来我将讨论回溯命令、使用变量和创建别名的功能。

# 使用命令历史记录回溯命令

在 shell 会话中重复之前运行过的命令非常方便。重复一个你输错的长且复杂的命令行可以节省你的很多麻烦。幸运的是，一些 shell 功能允许你回溯之前的命令、编辑这些行或完成部分输入的命令行。

shell 历史记录是你之前输入过的命令列表。在 bash shell 中使用 `history` 命令，你可以查看之前的命令。然后通过各种 shell 功能，你可以从该列表中回溯单个命令行并按你的意愿进行修改。

## 第 3 章：使用 Shell

本节的其余部分描述了如何进行命令行编辑、如何完成命令行的部分，以及如何回溯并处理历史列表。

### 命令行编辑

如果你在命令行上输入了错误，bash shell 确保你不需要删除整行并重新开始。同样，你可以回溯之前的命令行并修改元素以创建一个新命令。

默认情况下，bash shell 使用基于 emacs 编辑器的命令行编辑。输入 `man emacs` 来阅读相关内容（如果你感兴趣的话）。如果你熟悉 emacs，你可能已经知道了所描述的大部分快捷键。

> 提示
>
> 如果你更倾向于使用 vi 命令来编辑 shell 命令行，你可以轻松地实现这一点。在你的家目录下的 `.bashrc` 文件中添加以下行：
>
> ```
> set -o vi
> ```
>
> 下次你编辑时，就可以使用 vi 来编辑你的命令行了。

为了进行编辑，你可以使用控制键、meta 键和箭头键的组合。例如，Ctrl+F 是按住 Ctrl 键并输入 f。Alt+F 是按住 Alt 键并输入 f。（你的键盘可能是 Meta 键或 Esc 键而不是 Alt 键。在 Windows 键盘上可以使用 Windows 键。）

尝试一下命令行编辑，输入以下内容：
