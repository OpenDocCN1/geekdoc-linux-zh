
为了在 vi 编辑器中访问 /etc/sudoers，请运行 visudo 命令。以下指令默认处于活动状态，允许 root 用户完全访问管理命令：

```
root    ALL=(ALL) ALL
```

其他用户也可以获得管理访问权限。例如，如果你想允许用户 boris 拥有完全的管理访问权限，请将以下指令添加到 /etc/sudoers：

```
boris    ALL=(ALL) ALL
```

在这种情况下，boris 运行管理命令所需要做的就是在命令前加上 sudo 命令。例如，如果 boris 运行以下命令，在指定的服务启动之前，他会被提示输入自己的普通用户密码。

```
$ sudo service vsftpd start
Password:
```

另外，你也可以允许特殊用户无需密码即可获得管理访问权限。如注释所建议，/etc/sudoers 中的以下指令将允许 wheel 组的所有成员无需密码即可运行管理命令：

```
%wheel    ALL=(ALL) NOPASSWD: ALL
```

但你不必允许完全的管理访问。例如，如果你想允许 %users 组中的用户关闭本地系统，请激活以下指令：

```
%users    localhost=/sbin/shutdown -h now
```

在许多 Linux 配置文件中，指令前面的 % 符号指定一个组。即使 users 组的 GID 为 100，让普通用户成为该组的成员也是可以接受的。例如，注释中显示的另一条指令指定了 %sys 组成员可以运行的一组命令：

```
%sys ALL = NETWORKING, SOFTWARE, SERVICES, STORAGE, DELEGATING, PROCESSES,
LOCATE, DRIVERS
```

每条指令都可以与一组命令关联。例如，sys 组中的用户被允许运行 NETWORKING 指令，他们可以运行以下指令关联的命令：

```
Cmnd Alias NETWORKING = /sbin/route, /sbin/ifconfig, /bin/ping, /sbin/dhclient,
/usr/bin/net, /sbin/iptables, /usr/bin/rfcomm, /usr/bin/wvdial, /sbin/lwconfig,
/sbin/mii-tool
```

类似地，你可以使用以下指令设置一个 netadmin 用户组，允许他们运行这些命令：

```
%netadmin ALL = NETWORKING
```

这假设 netadmin 等组存在于 /etc/group 和 /etc/gshadow 文件中。

## Other Administrative Users

各种服务可以配置自己的管理用户组。例如，查看 /etc/cups/cupsd.conf 文件中的以下指令：

```
SystemGroup sys root
```

使用 SystemGroup 列出的组成员在 RHEL 6 打印服务器上获得管理权限。

> exam watch
> 
> CUPS 不再是一个缩写，以避免与“UNIX”一词作为商标相关的担忧。CUPS 仍然是默认 Linux 打印服务器的名称。

## CERTIFICATION OBJECTIVE 8.03

## User and Shell Configuration

每个用户在登录到 Red Hat Enterprise Linux 系统时都有一个环境。环境定义了 Linux 查找要运行的程序的目录、登录提示的外观、终端类型等。本节解释如何为本地用户配置默认环境。

所有系统范围的 shell 配置文件都保存在 /etc 目录中。这些文件是 bashrc、profile 以及 /etc/profile.d 目录中的脚本。这些文件和脚本由每个用户主目录中的隐藏文件补充，正如前面所述。

让我们来看看这些文件。

## Home Directories and /etc/skel

当使用标准命令如 `useradd` 或 User Manager 等实用程序创建新用户时，一组默认的配置文件会从 `/etc/skel` 目录复制到用户的主目录。

## Home Directory

主目录是用户登录到 RHEL 系统时开始的位置。大多数用户的主目录是 `/home/username`，其中 `username` 是用户的登录名。每个用户通常应该对其自己的主目录具有写权限，因此每个用户都可以自由读取和写入自己的文件。

## /etc/skel

`/etc/skel` 目录包含新账户的默认环境文件。`useradd` 命令和 Red Hat User Manager 将这些文件复制到新用户的主目录。`/etc/skel` 的内容可能有所不同。虽然该目录中的标准文件是隐藏的，但管理员可以为新用户添加更多文件。`/etc/skel` 目录中一个副本的标准文件在表 8-9 中描述。

**TABLE 8-9**
Standard files in the `/etc/skel` Directory

| 文件 | 用途 |
|------|---------|
| `.bashrc` | 此基本 bash 配置文件可能包含对通用 `/etc/bashrc` 配置文件的引用。可以包含在 bash shell 启动时运行的命令。一个例子是别名，如 `rm='rm -i'`。 |
| `.bash_logout` | 此文件在退出 bash shell 时执行，可以包含适用于此目的的命令，例如清除屏幕的命令。 |
| `.bash_profile` | 配置 bash 启动环境。添加环境变量或修改用户账户 PATH 中的目录的合适位置。 |
| `.gnome2/` | 包含 GNOME 桌面环境设置 |
| `.kde/` | 指定 K 桌面环境设置。如果未安装 KDE，则不会添加到 `/etc/skel` 并且不会复制到用户主目录。 |
| `.mozilla/` | 包含与 Mozilla 项目开发的 Firefox 网络浏览器相关的选项。 |

> **exam watch**
> Linux 包含许多以点 (`.`) 开头的隐藏文件。要列出这些文件，请运行 `ls -a` 命令。例如，如果你想列出 /etc/skel 目录中的所有文件，请运行 `ls -a /etc/skel` 命令。

如果你在 RHEL 上安装了超过标准软件包集的软件包，/etc/skel 目录中可能会出现额外的配置文件和子目录。例如，某些软件包的安装可能在此目录中包含与 emacs 和 z shell (sh) 相关的配置文件。

作为系统管理员，你可以编辑这些文件或在 /etc/skel 中放置自定义文件。

propagated to the new users' home directories.

## /etc/bashrc

/etc/bashrc 文件用于系统范围的别名和函数。用你选择的文本编辑器打开此文件。阅读此文件中的每一行。即使你不理解编程命令，你也可以看到此文件为每个用户设置了以下 bash shell 参数。例如：

- 它分配 `umask` 的值，该值创建新创建文件的默认权限。它为 root 和系统用户（用户 ID 低于 200）提供一组权限，为普通用户提供另一组权限。（正式来说，RHEL 为普通用户保留所有高于 500 的用户 ID；但这在 `/etc/bashrc` 中未反映。）
- 它分配并定义提示符，即你在命令提示符处光标前看到的内容。
- 它包含 `/etc/profile.d/` 目录中 `*.sh` 文件的设置。

此处的设置由每个用户主目录中的 .bashrc 文件补充。设置由每个用户主目录中的 .bash_profile 和 .bash_logout 文件补充。

## /etc/profile and /etc/profile.d

/etc/profile 文件用于系统范围的环境和启动文件。

文件的第一部分设置用于搜索命令的 PATH。`pathmunge` 命令会向 PATH 添加额外目录。（除非你使用 Korn shell，否则忽略 ksh 变通方案段。）然后它导出 PATH。

USER、LOGNAME、MAIL、HOSTNAME、HISTSIZE 和 HISTCONTROL 变量，最后运行 /etc/profile.d 目录中的脚本。你可以使用 echo $variable 命令检查这些变量中的任何一个的当前值。

## /etc/profile.d

/etc/profile.d 目录设计用于包含由 /etc/profile 文件执行的脚本。以下是文件的部分列表；扩展名为 .sh 的文件适用于默认的 bash shell：

```
colorls.csh  gnome-ssh-askpass.csh  udisks-bash-completion.sh
colorls.sh   gnome-ssh-askpass.sh   vim.csh
cvs.csh      lang.csh               vim.sh
cvs.sh       lang.sh                which2.csh
glib2.csh    less.csh               which2.sh
glib2.sh     less.sh
```

在大多数情况下，有两个版本的脚本，针对不同的 shell 环境进行了定制。查看 /etc/profile.d 目录中的文件。你可以看到该目录中以 .sh 结尾的任何脚本都作为 /etc/profile 的配置的一部分包含在内。具有其他扩展名的脚本，例如 .csh，与不同的命令 shell 相关。

## EXERCISE 8-4

## Another Way to Secure a System

帮助保护系统安全的另一种方法是更改新文件和目录的默认权限。在本练习中，你将重新配置系统以从其他用户或组中删除默认文件的访问权限。

- 1. 备份 /etc/bashrc 文件的当前版本。
- 2. 在文本编辑器中打开 /etc/bashrc 文件。文件中两行设置 umask。根据它们上面的 if 语句选择其中一行。看看你是否能确定分配给普通（非 root）用户的 umask 值。
- 3. if 语句测试用户 ID (UID) 和组 ID (GID) 是否相同，并且 UID 大于 199。（在 RHEL 上，你可以——但不必——将其更改为 499。）

