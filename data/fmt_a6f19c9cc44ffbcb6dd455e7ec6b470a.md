
```
# /etc/cshrc
#
# csh configuration for all shell invocations.
#
# By default, we want this to get set.
# Even for non-interactive, non-login shells.
[ `id -gn` = `id -un` -a `id -u` -gt 99 ]
if $status then
    umask 022
else
    umask 002
endif

if ($?prompt)
    if ($?tcsh) then
        set prompt='[%n@%m %c]$ '
    else
        set prompt='\`id -nu\`@`hostname -s\`]\$'
    endif
endif
```

`/etc/cshrc` 和 `/etc/bashrc` 文件设置了各种 shell 环境选项。如果你想修改或添加到系统中每个用户的 shell 环境中，`/etc/bashrc` 或 `/etc/cshrc` 文件是执行此操作的地方。

## 设置系统配置文件

分配给每个用户的最基本信息中有一些是从 `/etc/profile` 文件添加的。因此，如果你想更改以下任何信息，可以从 `/etc/profile` 开始。以下是 `/etc/profile` 中包含的一些值：

- `PATH` — 为 root 用户和所有其他用户分配默认的 `PATH`。你可能会更改此值，以添加包含所有用户都需要应用程序的本地目录的路径。
- `ulimit` — 设置用户从 shell 可以创建的最大允许文件大小为无限制。如果你发现用户正在创建巨大的文件，可以使用 `ulimit` 来限制最大文件大小。如 `/etc/profile` 文件中所定义，`ulimit` 不限制用户可创建的文件大小。但是，它确实阻止创建核心文件（通常在进程崩溃时创建）。
- **环境变量** — 标准操作所需的 shell 环境变量在此文件中分配。这些包括 `USER`（由 `id -un` 命令设置）、`LOGNAME`（与 `USER` 相同）、`MAIL`（设置为 `/var/spool/mail/USER`）、`HOSTNAME`（设置为命令 `/bin/hostname` 的输出），以及 `HISTSIZE`（将 shell 命令历史记录设置为 1000 项）。
- `INPUTRC` — 根据 `/etc/inputrc` 文件的内容，在特定情况下设置键盘映射。特别是，`inputrc` 文件确保 Linux 控制台和各种终端窗口（xterm 和 rxvt）的行为正常。

`/etc/profile` 文件所做的最后一件事是查看 `/etc/profile.d` 目录的内容，并引入其找到的文件。每个文件包含定义环境变量或别名的设置，这些设置会影响用户如何使用 shell。例如，`lang.sh` 和 `lang.csh` 文件标识外语文件的位置。`vim` 文件创建别名，使得输入 `vi` 时使用 `vim`。`which-2.sh` 文件定义 `which` 命令使用的一组选项。你可以修改 `profile.d` 文件或添加自己的文件，以为所有用户设置环境变量和别名。

## 创建可移动桌面

Linux 是一个在互联网上诞生的操作系统，因此它具有强大的网络功能并不令人惊讶。这使得 Linux 成为一个出色的服务器，但也使其成为一个出色的桌面工作站，尤其是在高度网络化的环境中。Fedora 让你可以轻松为用户设置可移动桌面，使其能够随用户从一台计算机移动到另一台计算机。与其他领先的桌面操作系统相比，这要容易得多。

通常，Linux 用户的主目录位于 `/home` 目录内。作为一种替代方案，你可以在主目录内创建一个以系统主机名称命名的目录。在该目录内，创建用户的主目录。因此，在一台名为 `dexter` 的 Linux 系统上，用户 `mary` 的主目录将是 `/home/dexter/mary`，而不是 `/home/mary`。这样做有一个非常好的原因。

如果你登录到 Linux 系统 `ratable` 并想要访问 `dexter` 上的主目录，就好像它是本地存储的一样，最好的方法是使用网络文件系统（NFS）将 `dexter` 的 `/home` 目录挂载到 `ratable` 的 `/home` 上。结果是你登录到任何机器时，都可以访问相同的主目录内容。

> 交叉参考：你可以在第 18 章阅读更多关于 NFS 的内容。

要挂载如前所述的 `dexter` 的 `/home` 目录，你将在 `ratable` 的 `/etc/fstab` 文件中添加类似下面的一行：

# 第 11 章：设置与支持用户

```
dexter:/home /home nfs defaults 0 0
```

你还需要在 dexter 的 `/etc/exports` 目录中添加如下条目：

```
/home ratbert
```

现在，当 ratbert 启动时，它会通过网络自动挂载 dexter 的主分区。这使得你可以将 dexter 上 `/home` 目录中的远程文件和目录视为像存储在 ratbert 本地一样进行操作。不幸的是，这会产生一种副作用，即“遮盖”了 ratbert 实际的 `/home` 目录。

这就是基于系统名称的额外目录层发挥作用的时候。由于 dexter 的所有主目录都位于 `/home/dexter`，而 ratbert 的所有主目录都位于 `/home/ratbert`，我们可以消除一个系统遮盖另一个系统主目录的危险。事实上，让我们将这个例子再进一步：想象这样一个场景，其中 dexter、ratbert 和 daffy 这三个系统都拥有与其他系统共享的便携式桌面。每台系统的 `/etc/fstab` 和 `/etc/exports` 文件应添加如下所示的行。

dexter 的 `/etc/exports` 和 `/etc/fstab` 文件如下：

### /etc/exports 文件

```
/home/dexter ratbert,daffy
```

### /etc/fstab 文件

```
ratbert:/home/ratbert /home/ratbert nfs defaults 0 0
daffy:/home/daffy /home/daffy nfs defaults 0 0
```

ratbert 的 `/etc/exports` 和 `/etc/fstab` 文件为：

### /etc/exports

```
/home/ratbert dexter,daffy
```

### /etc/fstab

```
dexter:/home/dexter /home/dexter nfs defaults 0 0
daffy:/home/daffy /home/daffy nfs defaults 0 0
```

daffy 的 `/etc/exports` 和 `/etc/fstab` 文件为：

### /etc/exports

```
/home/dexter ratbert,dexter
```

### /etc/fstab

```
ratbert:/home/ratbert /home/ratbert nfs defaults 0 0
dexter:/home/dexter /home/dexter nfs defaults 0 0
```

如你所见，每个系统都使用 NFS 来挂载另外两个系统的主目录。用户可以在服务器之间穿梭，并在每个系统上看到完全相同的桌面。

## 为用户提供支持

创建新用户账户只是众多管理任务中的一项。没有任何一章能够充分讨论用户持续支持所涉及的所有任务。但我在这里分享一些提示和步骤，以减轻这一负担。

### 创建技术支持邮箱

电子邮件是一种绝佳的沟通工具，对于过度工作的系统管理员来说尤其如此。人们通常会在电子邮件消息中投入比留言语音更多的思考和努力。文本消息可以在发送前进行编辑以提高清晰度，并且可以复制粘贴来自其他来源的重要细节。这使得电子邮件成为 Linux 用户与其系统管理员沟通的绝佳方式。

在只有少数用户的办公室中，你也许可以使用个人邮箱来收发支持电子邮件。然而，在较大的办公室中，你应该创建一个专门用于技术支持问题的独立邮箱。与使用个人邮箱相比，这有几个优点：

- 支持消息不会与非支持相关的个人消息混淆。
- 多人可以检查邮箱并分担管理责任，而无需阅读彼此的私人电子邮件。
- 当你休假时，支持电子邮件可以轻松地重定向到另一个人的邮箱。你的私人电子邮件仍将继续发送到你的私人邮箱。

一个简单的解决方案是创建一个支持电子邮件别名，该别名将消息重定向到实际的邮箱或邮箱列表。例如，假设你想创建一个支持别名，将电子邮件重新分配给支持人员 Joe、Mary 和 Bob 的用户账户。你需要以 root 身份登录，编辑 `/etc/aliases` 文件，并添加类似以下内容的行：

```
# Technical support mailing list
support: joe, mary, bob
```
