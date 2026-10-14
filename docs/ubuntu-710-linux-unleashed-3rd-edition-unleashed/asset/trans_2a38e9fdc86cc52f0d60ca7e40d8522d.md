

命令中的连字符；如果省略该连字符，就会保留你的“旧”环境。）要变成另一个用户，请在命令行中指定另一个用户名：

```
$ su - other_user
```

当离开某个身份、返回你通常的用户身份时，请使用 exit 命令。例如，在以普通用户身份登录时，

```
$ su - root
```

系统会提示输入密码：

```
Password:
```

当密码正确输入后，会出现 root 用户的提示符：

```
#
```

要返回普通用户的身份，只需输入

```
# exit
```

这会带你回到普通用户的提示符：

```
$
```

如果你需要允许其他用户以 root 权限访问某些命令，就必须把 root 密码告诉他们，以便他们可以使用 su——这显然不是一个安全的解决方案。下一节将介绍一种更灵活、更安全的方法，允许普通用户执行选定的 root 任务。

## 临时授予 root 权限——sudo 命令

系统上常常需要委派 root 所掌握的部分权限。对于大型系统来说，这很有必要，因为不可能总有某一个人随时可以执行超级用户功能。问题在于 UNIX 权限是一种“全有或全无”的权限。于是 sudo 应运而生，这个应用程序允许分配一个、几个或全部仅限 root 使用的系统命令。

> **注意**
> 如前所述，sudo 命令在 Ubuntu 中无处不在，因为它是默认使用的命令。如果你想进入 root shell，从而免去在每个命令前输入 sudo 的麻烦，只需输入 sudo -i 即可获得 root 提示符。要返回普通用户提示符，请输入 exit 并按回车键。

配置好之后，sudo 的使用很简单。授权用户只需在需要超级用户权限的命令前加上 sudo 即可，如下所示：

```
$ sudo command
```

在获得用户密码后，sudo 会检查 /etc/sudoers 文件，看该用户是否有权执行该特定命令；如果有，sudo 会生成一张有效期为特定时长的“票据”，授权用户使用该命令。然后系统会提示用户输入其密码（以保留问责性并提供一定的安全性），之后该命令就会像由 root 发出一样被执行。在票据有效期内，可以再次使用该命令而无需输入密码。如果未授权用户试图执行 sudo 命令，系统日志会记录该未授权尝试，并发送一封邮件给超级用户。

与 sudo 相关的有三个 man 手册页：sudo、sudoers 和 visudo。第一个介绍命令本身，第二个介绍 /etc/sudoers 文件的格式，第三个介绍如何使用 /etc/sudoers 的特殊编辑器。你应该使用这个特殊编辑命令，因为它会检查文件的解析错误，并锁定文件以防止其他人同时编辑。visudo 命令使用 vi 编辑器，因此你可能需要快速回顾一下第 4 章“使用 vi”一节中的 vi 编辑命令。你可以通过执行以下 visudo 命令来开始编辑：

```
$ sudo visudo
```

默认的 /etc/sudoers 文件如下所示：

```
# /etc/sudoers
#
# This file MUST be edited with the 'visudo' command as root.
#
# See the man page for details on how to write a sudoers file.
# Host alias specification
#
# User alias specification
#
# Cmd alias specification
#
# Defaults

Defaults !lecture,tty_tickets,lfqdn

# User privilege specification
root ALL=(ALL) ALL

# Members of the admin group may gain root privileges
%admin ALL=(ALL) ALL
```

文件中 sudoers 行的基本格式如下：

```
user host_computer=command
```

user 可以是单个用户，也可以是一个组（在名称前加上 % 以标识为组）。host_computer 通常是 ALL（用于网络中的所有主机）或 localhost（用于本机），但也可以引用为子网或任何特定主机。sudoers 行中的 command 可以是 ALL、特定命令列表，也可以是对特定命令的限制（在命令前加上 ! 构成）。sudoers 行可以使用许多选项，也可以使用别名来简化权限分配。同样，sudoers 的 man 手册页会提供详细信息，但这里有几个示例：

如果我们取消下面这一行的注释

```
# %wheel    ALL=(ALL)    NOPASSWD: ALL
```

那么任何加入 wheel 组的用户都可以不输入密码执行任何命令。

假设我们想给用户 john 网络范围内的权限，使其能够通过图形界面添加用户。我们可以添加这一行：

```
john ALL=/usr/sbin/usermod
```

或者只授予她本地电脑上的权限：

```
john 192.168.1.87 /usr/bin/users-admin
```

如果我们想让编辑器组拥有系统范围的权限，并且无需密码即可删除文件：

```
%editors ALL=NOPASSWD: /bin/rm
```

如果我们想给每个用户无需密码即可在 localhost 上挂载 CD 光驱的权限：

```
ALL localhost=NOPASSWD: /sbin/mount /dev/scd0 /mnt/cdrom /sbin/umount /mnt/cdrom
```

在构建 sudoers 文件时也可以使用通配符。也可以使用别名，以便更轻松地定义用户和组。虽然 sudoers 的 man 手册页中包含一些示例，但 http://www.komar.org/pres/sudo/toc.html 提供了一家大型航空航天公司使用 sudo 的说明性注释和评论。sudo 的主页 http://www.sudo.ws/ 也是一个有用的资源，可以提供更多解释和示例。

以下命令会向用户显示他们有权使用的命令列表：

```
$ sudo -l
```

