
`/etc/cshrc` 和 `/etc/bashrc` 文件设置了各种 shell 环境选项。如果希望修改或添加系统上为每个用户提供的 shell 环境，`/etc/bashrc` 或 `/etc/cshrc` 文件就是执行此操作的地方。

## 设置系统配置文件

分配给每个用户的最基本信息中的一些是从 `/etc/profile` 文件添加的。因此，如果你想更改以下任何信息，可以从 `/etc/profile` 开始。以下是 `/etc/profile` 中包含的一些值：

- `PATH` — 为 root 用户和所有其他用户分配默认 `PATH`。你可能会更改此值以添加包含所有用户所需应用程序的本地目录的路径。
- `ulimit` — 将用户从 shell 创建的最大允许文件大小设置为无限制。如果你发现用户正在创建巨大的文件，可以使用 `ulimit` 来限制最大文件大小。如 `/etc/profile` 文件中所定义，`ulimit` 对用户可以创建的文件大小不设限制。然而，它确实防止了 core 文件（通常在进程崩溃时创建）的创建。
- Environment variables — 此文件中分配了标准操作所需的 shell 环境变量。这些包括 `USER`（由 `id -un` 命令设置）、`LOGNAME`（与 `USER` 相同）、`MAIL`（设置为 `/var/spool/mail/$USER`）、`HOSTNAME`（设置为 `/bin/hostname`）以及 `HISTSIZE`（将 shell 命令历史设置为 1000 项）。
- `INPUTRC` — 根据 `/etc/inputrc` 文件的内容设置特定情况下的键盘映射。特别是，`inputrc` 文件确保 Linux 控制台和各种终端窗口（`xterm` 和 `rxvt`）都表现正常。

`/etc/profile` 文件做的最后一件事是查看 `/etc/profile.d` 目录的内容并导入它找到的文件。每个文件包含定义环境变量或别名的设置，这些设置会影响用户使用 shell 的方式。例如，`lang.sh` 和 `lang.csh` 文件标识外语文件的位置。`vim` 文件创建别名，使在输入 `vi` 时使用 `vim`。`which-2.sh` 文件定义了 `which` 命令使用的一组选项。你可以修改 `profile.d` 文件或添加自己的文件，以便为所有用户设置环境变量和别名。

## 创建便携式桌面

Linux 是一个诞生于互联网的操作系统，因此它具有强大的网络能力不足为奇。这使得 Linux 成为一台优秀的服务器，但也使 Linux 成为一台优秀的桌面工作站，尤其是在高度网络化的环境中。Red Hat Linux 让你可以轻松地为用户设置便携式桌面，使其在计算机之间跟随用户。与其他领先的桌面操作系统相比，这并不容易。

通常，Red Hat Linux 用户的主目录位于 `/home` 目录内。作为替代方案，在主目录内你可以创建一个以系统主机名为名的目录。在该目录内，创建用户的主目录。因此，在名为 `dexter` 的 Linux 系统上，用户 `mary` 的主目录将为 `/home/dexter/mary` 而不是 `/home/mary`。这样做有一个很好的理由。

如果你已登录 Linux 系统 `ratbert` 并希望像本地存储一样访问 `dexter` 上的主目录，最佳方法是使用网络文件系统 `NFS` 将 `dexter` 的 `/home` 目录挂载到 `ratbert` 上的 `/home`。这样无论登录哪台机器，你的主目录内容都保持一致。

> **交叉引用：** 你可以在第 18 章阅读有关 `NFS` 的更多信息。

按上述描述挂载 `dexter` 的 `/home` 目录，你需要在 `ratbert` 的 `/etc/fstab` 文件中添加类似以下的行：

```
dexter:/home /home nfs defaults 0 0
```

你还需要在 `dexter` 的 `/etc/exports` 文件中添加类似以下条目：

```
/home ratbert
```

现在，`ratbert` 启动时会自动通过网络挂载 `dexter` 的主分区。这使我们能够将 `dexter` 的 `/home` 上的远程文件和目录视为本地存储在 `ratbert` 上。不幸的是，这会产生“覆盖”`ratbert` 实际 `/home` 目录的副作用。

这时基于系统名称的额外目录层就派上用场了。将 `dexter` 的所有主目录放在 `/home/dexter` 中，将 `ratbert` 的所有主目录放在 `/home/ratbert` 中，我们就可以消除一个系统覆盖另一个系统主目录的危险。事实上，让我们再进一步举例：假设系统 `dexter`、`ratbert` 和 `daffy` 都有可移植的桌面并与其他系统共享。每个系统的 `/etc/fstab` 和 `/etc/exports` 文件都应添加以下行。

`dexter` 的 `/etc/exports` 和 `/etc/fstab` 文件如下：

# `/etc/exports` 文件

```
/home/dexter ratbert,daffy
```

# `/etc/fstab` 文件

```
Ratbert:/home/ratbert /home/ratbert nfs defaults 0 0
Daffy:/home/daffy /home/daffy nfs defaults 0 0
```

`ratbert` 的 `/etc/exports` 和 `/etc/fstab` 文件如下：

# `/etc/exports`

```
/home/ratbert dexter,daffy
```

# `/etc/fstab`

```
dexter:/home/dexter /home/dexter nfs defaults 0 0
daffy:/home/daffy /home/daffy nfs defaults 0 0
```

`daffy` 的 `/etc/exports` 和 `/etc/fstab` 文件如下：

# `/etc/exports`

```
/home/daffy ratbert,dexter
```

# `/etc/fstab`

```
Ratbert:/home/ratbert /home/ratbert nfs defaults 0 0
Dexter:/home/dexter /home/dexter nfs defaults 0 0
```

如你所见，每个系统都使用 `NFS` 挂载来自另外两个系统的主目录。用户可以在服务器之间移动，并在每个系统上看到完全相同的桌面。

## 为用户提供支持

创建新用户账户只是众多管理任务中的一项小任务。没有任何一章能够充分讨论用户持续支持所涉及的所有任务。但我与你分享一些提示和流程来减轻这一负担。

### 创建技术支持邮箱

电子邮件是一种很棒的通信工具，尤其是对于工作繁忙的系统管理员来说。人们通常会比留言电话更用心地撰写电子邮件。文本消息在发送前可以编辑以提高清晰度，重要细节也可以从其他来源复制粘贴。这使得电子邮件成为 Red Hat Linux 用户与系统管理员沟通的绝佳方式。

在只有少数用户的办公室里，你可能可以用个人邮箱来收发支持邮件。然而在更大的办公室里，你应该创建一个专门用于技术支持问题的独立邮箱。这比使用个人邮箱有几个优势：

- 支持消息不会与个人、非支持相关的消息混淆。
- 多个人可以检查邮箱并分担管理责任，而无需阅读彼此的个人邮件。
- 当你休假时，支持邮件可以轻松转发到另一个人的邮箱。你的个人邮件仍会发送到你的个人邮箱。

一个简单的解决方案是创建一个支持电子邮件别名，将消息重定向到实际的邮箱或邮箱列表。例如，假设你想创建一个支持别名，将邮件重新分发给支持人员 `Joe`、`Mary` 和 `Bob` 的用户账户。你需要以 root 登录，编辑 `/etc/aliases` 文件，并添加类似以下的行：

```
# Technical support mailing list
support: joe, mary, bob
```

保存文件后，你需要运行 `newaliases` 命令将 `/etc/aliases` 文件重新编译为数据库格式。现在你的用户可以向支持电子邮件地址发送邮件，消息会自动路由到列表中的每个人。当列表中的成员回复该消息时，他或她应使用“全部回复”选项，以便其他支持人员也能看到该消息。否则，多个人可能会尝试解决同一个问题，导致不必要的重复劳动。

你也可以选择创建一个支持用户账户。技术支持人员将登录此账户以检查消息并发送回复。这样，所有回复都将盖上支持登录名，而不是员工的个人电子邮件地址。

### 重置用户的密码

你的用户会遇到的一个常见（如果不是 *最* 常见）问题是无法登录，因为：

- 他们打开了 `Caps Lock` 键。
- 他们忘记了密码。
- 密码已过期。

如果 `Caps Lock` 键未打开，那么你可能需要重置该个人的密码。你无法查找密码，因为 Red Hat Linux 以加密格式存储密码。相反，使用 `passwd` 命令为用户账户分配新密码。告诉用户新密码是什么（最好当面告知），然后设置密码很快过期，以便他或她必须选择一个（希望是更容易记住的新密码）。

如果必须重置用户的密码，请使用 `passwd` 命令。以 root 登录时，输入 `passwd` 后跟你要重置的登录名。系统会提示你输入两次密码。例如，要更改 `mary` 的密码，输入：
```
