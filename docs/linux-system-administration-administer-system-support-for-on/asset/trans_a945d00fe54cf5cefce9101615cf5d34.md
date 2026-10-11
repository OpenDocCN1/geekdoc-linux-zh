

veritech 账户的到期日（MM/DD/YY）[]：

以下代码显示了所有正确输入的信息。如果您遇到问题，请按 Ctrl+C 退出。

```
OK, I'm about to make a new account. Here's what you entered so far:

New login name: veritech
New UID: [Next available]
Initial group: users
Additional groups: [none]
Home directory: /home/veritech
Shell: /bin/bash
Expiry date: [no expiration]

This is it... if you want to bail out, hit Control-C. Otherwise, press
ENTER to make the account.
```

下一段代码列出了您可以通过 `finger` 命令获取的信息。我建议尽可能留空这些信息或禁用 `finger`。禁用 `finger` 可防止黑客利用 `finger` 端口 79 或使用 `finger` 来利用您的系统。然而，如果正确使用，`finger` 确实有一些适当的行政用途。例如，您可以获取账户信息，从而立即知道某人是否在线。

```
Making new account...

Changing the user information for veritech
Enter the new value, or press return for the default

    Full Name []: Rick Hunter
    Room Number []:
    Work Phone []: 650.555.1212
    Home Phone []:
    Other []:
```

下一段代码显示了如何输入密码信息。输入密码（请记住：它不应容易被猜中）。与登录密码一样，这个新密码不会在屏幕上回显。

```
Changing password for veritech
Enter the new password (minimum of 5, maximum of 8 characters)
Please use a combination of upper and lower case letters and numbers.

New password:
Re-enter new password:
Password changed.
Done...
```

## 定义 root 访问权限

如果您确实需要 root 访问权限，有两种方法可以在不登录为 root 的情况下使用 root 权限。您可以首先授予某些 root 权限，例如关闭系统或访问可挂载驱动器（CD-ROM、软盘）给特定用户，或者您可以使用 `su` 命令在不登录到特定终端的情况下获得 root 访问权限。

### SUDO 命令

如果您想使用特定的 root 命令，如挂载 CD-ROM 或向 ISP 拨号，可以通过 `sudo` 命令将 root 访问权限分配开来。您可以允许某些用户执行一些超级用户命令。这就像父母允许青少年使用家用旅行车，但不让他们使用野马跑车一样。

`sudo` 用户的信息位于 `/etc/sudoers` 文件中。要编辑此文件，请成为 root 并使用以下命令：

```
# visudo
```

这将创建 `/etc/stmp` 文件，并锁定 `/etc/sudoers` 文件。这也防止该文件被随意编辑。

`/etc/sudoers` 文件的语法如下：

```
Host_Alias   ALIASNAME=hostname
Cmd_Alias    ALIASNAME=commands
username       hostname=commands
```

在 `/etc/sudoers` 文件中，有几个部分需要特别注意。第一部分是主机别名规范。在这里，您可以指定远程主机或服务器。但是，除非您正在安全地管理 NFS，否则我只建议您指定本地机器。

下一部分是命令别名。如果您想要对命令进行分组，这是一个绝佳的方法。例如，如果您希望将关机命令别名为 SHUTDOWN，可以使用诸如 `/etc/halt`、`/etc/shutdown` 和 `/etc/reboot` 等命令。对于拨号，您可以将 `ppp` 命令（`/usr/sbin/ppp-go`、`/usr/sbin/ppp-off`）分组为 PPP。

当您定义了主机和命令后，定义哪些用户可以在哪些主机上拥有哪些权限。

![](img/8ad518fddafc7f5e73715a2604b61d50_262_0.png)

> 请注意您定义的主机。您可能会让未知用户拥有 root 访问权限——这很容易招致利用。

假设您有三台主机：Web 主机、主主机和开发主机。如果您希望用户 *bob* 能够在 Web 主机上使用您的拨号功能，但只希望用户 *judy* 能够在本地关闭您的主主机，那么您的 *`/etc/sudoers`* 文件可能看起来像这样：

```
# This file MUST be edited with the 'visudo' command as root.
#
# See the man page for the details on how to write a sudoers file.
#
# Host alias specification
Host_Alias    MAIN=hub:\
                REMOTE=web,devel
# Cmnd alias specification
Cmnd_Alias    PPP=/usr/sbin/ppp-go,/usr/sbin/ppp-off:\
                SHUTDOWN=/etc/halt,/etc/shutdown,/etc/reboot

# User specification
root    ALL=ALL
bob     REMOTE=PPP
judy    MAIN=SHUTDOWN
```

在 *`/etc/sudoers`* 文件中，该文件使用特定的语法。如果您要对主机、命令或用户使用别名，必须使用全大写字母。别名 *ALL* 和 *NONE* 已经定义。正如前面示例所示，*root* 被定义为在所有主机上拥有所有命令的权限。然而，*bob* 只能在 *REMOTE* 主机上运行 *PPP* 命令，而 *judy* 只能在 *MAIN* 主机上运行 *SHUTDOWN* 命令。您还可以通过拒绝 *NONE* 来禁用用户拥有任何类型的 *su* 访问权限。

![](img/8ad518fddafc7f5e73715a2604b61d50_262_1.png)

> 请记住，允许除管理员以外的任何用户拥有任何形式的 root 访问权限都可能带来安全问题。如果您这样做，您就是在信任您的用户拥有以 root 身份运行命令的权力，而这项权力可能被任何急需完全 root 访问权限的人所利用。好处是，通过这种责任共享所建立的信任工作环境可能会阻止用户尝试获取 root 访问权限。请根据您的最佳判断行事。

## 使用 SU 进行 ROOT 访问

如果您已登录到用户账户，并且只希望在一分钟内获得 root 访问权限，那么退出用户账户、以 root 身份登录、退出 root，然后再登录回用户账户会很不方便。幸运的是，Linux 的 su 命令可以省去这些麻烦：它允许您临时登录到另一个用户的账户，而无需退出当前用户账户。su 命令非常强大，特别是用于获取 root 访问权限。

su 命令默认提供 root 访问权限。例如，如果我用个人账户登录并执行 su，它看起来会像这样：

```
$ su
Password:
bash#
```

系统会提示我输入 root 密码。如果我未正确输入 root 密码，我就无法获得 root 提示符。这种失误可能看起来像这样：

```
$ su
Password:
Sorry.
```

如果您想以特定用户身份登录，请使用 su 命令后跟用户名。

```
$ su stripes
```

如果您在 su 命令后使用连字符（“-”），系统将读取该用户的环境变量来自 .profile 或 .cshrc 文件。当成为 root 用户时，您应尽可能使用连字符，否则您可能会将自己账户的宽松特性应用于以 root 身份执行的操作——这包括您的 Umask 设置和 $PATH 变量。如果您的路径中有一个“点”，而您未使用带连字符的 su，那么 root 的 $PATH 中也将包含一个“点”。因此，在大多数情况下，请使用此命令：

```
$ su -
```

然而，您可以控制谁可以使用 su 命令，以及他们是否需要密码。这在 /etc/suauth 文件中提供。使用 /etc/suauth，您可以拒绝用户使用 su，要求他们使用自己的密码访问，或者完全不需要密码。

/etc/suauth 文件中命令的语法看起来像这样：

```
whoyouwanna t o : who you are : what you can do
```

`/etc/suauth` 的一个示例可以 *阻止* 除 `bob` 以外的所有用户获取 root 访问权限，并允许用户 `dbadmin` 和 `judy` 无需密码即可进入（因为他们是同一人）。`/etc/suauth` 文件真正酷的一点是，您可以定义 `除了某个组或用户以外的所有人` 拥有特定的访问权限。

```
# /etc/suauth file
#
# Only Bob can su to root.
root:ALL EXCEPT USER bob:DENY
#
# Because Judy is our database admin, we should let her
# into her own accounts without having to prompt for
# a password
judy:dbadmin:NOPASS
dbadmin:judy:NOPASS
```

![](img/8ad518fddafc7f5e73715a2604b61d50_264_0.png)

> 我不建议让用户无需密码或使用自己的密码进入 root。即使您信任自己，如果黑客获得了对您账户的访问权限，他们将自动拥有 root 权限。

## 决定谁应该使用您的系统

为了最小化风险，请确保您可以管理系统中开放的所有账户。这意味着只允许需要访问权限的人访问。因为每个账户都是一个入口，而且大多数钥匙（密码）都很容易复制，所以您不希望有太多账户遗留在那里。当您给人访问您系统的权限时，请考虑他们能获得什么好处，以及您可能会获得什么好处（他们可能很棒程序员）。

## 使用旧账户创建后门

如果某个人不再使用系统，而且您不希望任何人远程访问它，请`删除该账户`。旧账户是黑客可以捡到的又一把钥匙，一旦这种情况发生，找出可用的用户账户就变得相当简单。如果您需要保留前用户的文件，请将其移至公共目录，例如 `/usr/local/oldaccounts`，或将它们备份到可移动介质上。

