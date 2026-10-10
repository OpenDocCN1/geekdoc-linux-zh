
```bash
# /etc/cshrc
# 所有调用的 csh 配置

# 默认情况下，我们希望设置此。
# 即使对于非交互、非登录 shell。
[ "id-gn" = "id-un" -a "id-u" -gt 99 ]
if $status then
umask 022
else
umask 002
endif

if ($prompt) then
if ($tcsh) then
 set prompt='[%n@%m %# '
else
 set prompt=`id-nu`@hostname -s
endif
```

## 第 11 章：设置与支持用户

- `INPUTRC` — 根据 `/etc/inputrc` 文件的内容，为特定情况设置键盘映射。特别是，`inputrc` 文件确保了 Linux 控制台和终端窗口 (`xterm` 和 `rxvt`) 的行为均符合正常逻辑。

`/etc/profile` 文件执行的最后的一项操作是查看 `/etc/profile.d` 目录的内容，并加载（`source`）其中找到的文件。每个文件都包含定义环境变量或别名的设置，这些设置会影响用户使用 shell 的方式。例如 `lang.sh` 和 `lang.csh` 文件标识了外语言文件的位置。`vim` 文件创建了别名，使得在输入 `vi` 时会使用 `vim`。`which-sh` 文件定义了 `which` 命令使用的一组选项。你可以修改这些文件或添加自己的文件，以便为所有用户提供环境变量和别名。

### 向服务器添加用户账户

当你设置服务器时，通常希望允许人们向其上传文件，或者从其下载文件或接收消息。然而，你可能并不希望允许那些人员访问整个服务器。在最初创建他们的用户账户时，你就可以开始限制这些用户的访问权限。

为了防止远程用户登录并访问 shell（通过 `ssh`、`telnet` 或其他登录），请将用户的默认 shell 设置为 `nologin`。例如：

```bash
# useradd -s /sbin/nologin jerryb
```

将 shell 设置为 `nologin` 后，用户将无法登录服务器并打开 shell。然而，该用户仍然可以使用此账户登录服务器上的 FTP 服务器（如果该服务可用且用户拥有密码）。默认情况下，在本例中，当该用户登录 FTP 时，其用户主目录将是 `/home/jerryb`。（请参阅第 20 章，了解如何在 `chroot` 环境中限制该用户访问其主目录的方法）。

另一种实现仅限 FTP 访问服务器的方法是使用 `/usr/lib/sftp-server` 作为用户的登录 shell。虽然这允许用户访问该用户账户可用的整个文件系统，但它将他们的访问限制在通过 FTP 安全访问的服务器上。

Web 托管的常见做法是允许用户通过 FTP 在服务器上放置内容（通常位于用户的 `/home/username/public_html_` 目录），但不允许 shell 登录。然而，管理员可以将 Web 内容的存储位置指定为任何目录，包括系统范围的 Web 服务器目录。以下命令将名为 `webuser` 的用户使用 `/var/www/html` 作为其主目录（为了使此操作生效，你还应该将文件的所有权改为 `webuser`）：

```bash
# useradd -s /sbin/nologin -d /var/www/html webuser
```

如果你仅为访问邮件服务而添加用户，你可能选择也阻止对 FTP 的任何访问。做到此点的一种方法是将用户的主目录指向 `/dev/null`。例如：

```bash
# useradd -s /sbin/nologin -d /dev/null jerryb
```

一旦你设置了受限用户账户，就可以使用与特定服务相关的功能进一步定义你的服务器用户可以和不能访问的内容。

### 创建便携式桌面

Linux 是一个诞生于互联网的操作系统，因此它拥有强大的网络能力并不意外。这使得 Linux 成为一个出色的服务器，但也让 Linux 成为一个出色的桌面工作站，特别是在高度网络环境中。Fedora 和 RHEL 让你能够轻松设置带有便携式桌的用户，该桌面可以在不同计算机之间切换。与其他领先的操作系统相比，这远没有那么容易。

通常，Linux 用户的主目录位于 `/home` 目录内。作为替代方案，你可以在 `home` 目录下创建一个与系统主机同名的目录。在该目录内，创建用户的主目录。因此，在名为 `dexter` 的 Linux 系统上，用户的主目录可能是 `/home/dexter` 而不是 `/home/mary`。这样做有非常充分的理由。

如果你登录到名为 `ratbert` 的 Linux 系统，并希望像访问本地存储一样访问你在 `dexter` 上的主目录，那么最好的方法是使用网络文件系统 (`NFS`) 将你的 `/home` 目录挂载到 `/home/ratbert`。这使得无论你登录到哪台机器，都能获得相同主目录的内容。

> 交叉引用：你可以在第 18 章阅读更多关于 `NFS` 的知识。

要按照描述挂载 `dexter` 的 `/home` 目录，你需要在 `ratbert` 的 `/etc/fstab` 文件中添加类似下方的行：

```text
dexter:/home /home nfs defaults 0 0
```

你还会在 `dexter` 的 `/etc/exports` 目录下添加如下条目：`/home /ratbert`

现在，当 `ratbert` 启动时，它会自动通过网络挂载 `dexter` 的主分区。这让你能够将 `dexter:/home` 上的远程文件和目录视作本地存储在 `ratbert` 上。遗憾的是，这产生了一个“覆盖” `ratbert` 实际 `/actual` 目录的副作用。

这就是基于系统名称的额外目录级大显身之处。由于 `dexter` 的所有主目录都位于 `/home/dexter`，而 `ratbert` 的所有主目录都位于 `/home/ratbert`，你可以消除一个系统覆盖另一个系统主目录的危险。事实上，让我们更进一步：想象这样一种场景，系统 `dexter`、`ratbert` 和 `daffy` 均有与其他系统共享的便携式桌面。`/etc/fstab` 和 `/etc/exports` 文件配置如下（此处原文逻辑重复，翻译保持一致）：

为了共享便携式桌面，`dexter` 的 `/etc/fstab`：

```text
dexter:/home /home nfs defaults 0 0
```

`dexter` 的 `/etc/exports`：

```text
/home /ratbert
```

`ratbert` 的 `/etc/fstab`：

```text
daffy:/home /home nfs defaults 0 0
```

`ratbert` 的 `/etc/exports`：

```text
/home /dexter
```

`daffy` 的 `/etc/fstab`：

```text
ratbert:/home /home nfs defaults 0 0
```

`daffy` 的 `/etc/exports`：

```text
/home /ratbert
```

*(注：原文此处存在明显的逻辑重复和格式混乱，已按要求保留原文结构并翻译)*

### 为用户提供支持

创建新用户账户只是许多任务中的一项。但你还需要讨论对用户的持续支持。

#### 创建技术支持邮箱

电子邮件是一种极佳的通信工具，特别是对于人们通常在邮件上投入的精力更多时候。这使得邮件成为一种极佳的方法。

在只有几个用户的办公室里，你可能可以使用个人邮箱来应付。但在较大的办公室中，你应该为技术支持创建一个独立的邮箱。这比使用个人邮箱有几个优势：

- 支持消息不会与个人的无关消息混淆。
- 多人可以检查邮箱并分担管理责任。
- 当你休假时，支持邮件可以轻松重定向给其他人。

一种简单的方法是创建一个支持邮件别名，将邮件重定向到一组邮箱。例如，假设你想创建一个将邮件重定向到邮箱的支持别名。你将以 `root` 身份登录，编辑 `/etc/aliases` 文件，并添加类似下面的行：

```text
# 技术支持列表
support: joe, mary, bob
```

在保存文件后，你需要运行 `newaliases` 命令将 `/etc/aliases` 文件编译为数据库格式。现在，你的用户可以向支持邮件地址发送邮件，消息会自动路由给每个人。当列表中的成员回复时，她应该使用“回复所有人”选项，以便其他技术支持人员也能看到消息。否则，多个人可能会尝试解决同一个问题，导致重复工作的浪费。

你也可能选择创建一个用户账户。技术支持人员将登录检查消息并发送回复。通过这种方式，所有回复都将用支持登录名标记，而不是工作人员的个人电子邮件地址。

#### 重置用户密码

用户遇到的一个常见（如果不是最常见的）问题是无法登录，因为：

- 他们开启了 `Caps Lock`。
- 他们忘记了密码。
- 密码已过期。
