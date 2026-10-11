
# 编辑 PATH

`PATH` shell 环境变量向用户呈现系统可执行文件的路径名。你可以使用 `printenv` 或 `env` 命令，连同 `fgrep` 命令快速查看当前的 `PATH` 定义，如下所示：

```bash
$ env | fgrep PATH
...
PATH=/usr/local/bin:/usr/bin:/usr/X11R6/bin:/bin:/usr/lib/java/bin:/usr/games/bin:/usrX/games:/opt/gnome/bin:/opt/kde/bin:/usr/openwin/bin:.
```

请注意，并非所有的 `PATH` 定义都显示在这里。你可能有一个或多个额外的环境变量定义了特定的 `PATH`（例如 `MANPATH` 变量，它指向系统上各种手册页目录）。

Linux 系统上的命令通常根据用途组织到不同的目录中。例如，传统的用户路径包括 `/bin`、`/usr/bin`、`/usr/local/bin`、`/usr/X11R6/bin`，甚至主目录中的 `bin`。root 操作员的路径通常包括 `/sbin`、`/usr/sbin`，甚至 `/usr/local/sbin`。还可以定义和添加其他路径到用户的环境中。如果软件安装在系统的其他位置，例如 `/opt` 目录（软件包的默认位置）或诸如 Applixware 或 StarOffice 之类的办公套件，这将特别有用。

## 表 14.1 Linux 用户命令

| 命令 | 描述 |
| :--- | :--- |
| ac | 显示用户的连接时间 |
| adduser | 指向 useradd 的符号链接 |
| alter_user | 修改用户账户信息 |
| autolog | 注销空闲用户 |
| chage | 设置用户密码过期时间 |
| crontab | 维护用户的 crontab 文件 |
| edquota | 更改或编辑用户配额 |
| finger | 用户信息查询程序 |
| ftpwho | 显示当前 ftp 用户进程 |
| last | 打印最后登录用户的列表 |
| loginame | 显示用户的登录名 |
| newusers | 使用批处理文件批量更新和创建新用户 |
| nologin | 不允许非 root 用户登录 |
| passwd | 更改用户密码 |
| su | 以 root 或其他用户身份执行命令 |
| su1 | 以 root 操作员身份执行单个命令 |
| userdel | 移除用户账户及相关文件 |
| usermod | 修改用户账户 |
| userpasswd | 允许更改密码的 GUI 工具 |
| users | 显示当前登录的用户 |
| who | 显示已登录的用户 |
| whoami | 显示用户 ID |

### 管理用户组

作为用户，如果你未能将 `/sbin` 目录添加到你的 `PATH` 环境变量中，你会立刻察觉。例如，尝试像这样使用 `ismod` 命令：

```bash
$ ismod
bash: ismod: command not found
```

将新的 `PATH` 追加到你现有的 `PATH` 中非常简单。例如，如果你使用的是 `bash` shell，可以使用其内置的 `export` 命令，如下所示：

```bash
$ export PATH=$PATH:/usr/local/bin
```

在此示例中，`/usr/local/bin` 目录被追加到了现有的 `PATH` 变量末尾。重新定义 `PATH` 时要小心，以免丢失 `/bin` 或 `/usr/bin` 路径！不过，如果你确实丢失了，只需注销并重新登录即可（因为使用 `export` 命令所做的更改不是永久性的）。然而，当你以 root 身份在系统范围内进行修改时，务必仔细避免编辑错误。

系统级的 `PATH` 变量可能在多个位置定义，但在许多系统中，通常使用 `/etc/profile` 文件。在 SuSE Linux 中，编辑 `/etc/profile.local` 文件以添加自定义的 `PATHs`。

在 Linux 系统中，用户组用于关联用户集合。你可以使用组标识来允许不同用户组访问不同的文件。组定义在系统的 `/etc/group` 文件中，所有新用户默认分配给名为 `users` 的组（组 ID 为 100）。

作为 SuSE 系统管理员，你可以使用 `gpasswd` 命令来创建新组并分配成员。这是因为 SuSE Linux 使用影子组（shadow group），这是一种比 LinuxPPC 2000 更安全的组系统。尽管在 SuSE Linux 系统中组列在 `/etc/group` 中，但组的成员身份隐藏在一个由 root 拥有的名为 `/etc/gshadow` 的文件中。

在 LinuxPPC 2000 系统中，你只需查看 `/etc/group` 即可看到组和成员。该文件可能看起来像这样（部分）：

```text
root::0:root
bin::1:root,bin,daemon
daemon::2:root,bin,daemon
gys::3:root,bin,adm
adm::4:root,adm,daemon

wheel::10:root
users::100:
```

通过添加新条目来创建新组和成员。例如，如果你创建一个名为 `admin` 的组，并希望用户 `bball`、`fsmith` 和 `dcohen` 成为成员，请创建一个看起来像这样的新条目：

```text
admin::700:bball,fsmith,dcohen
```

数字条目是一个新的组 ID，在你的系统中必须是唯一的。对于 SuSE Linux，类似的方法如下列命令序列所示：

```bash
# echo "admin:700:" >> /etc/group
# newgrp admin
# gpasswd -a bball admin
Adding user bball to group admin
# gpasswd -a fsmith admin
Adding user fsmith to group admin
# gpasswd -a luser admin
Adding user luser to group admin
# gpasswd admin
Changing the password for group admin
New Password:
Re-enter new password:
```

前两个命令创建新的 `admin` 组定义。接下来，向 `admin` 添加三个成员。最后，为该组分配一个密码。可以使用 `gpasswd` 及其 `-r` 选项，后跟组名来删除组。

使用 `groups` 命令来检查你的组成员身份。例如：

```bash
# groups
admin users uucp dialout audio video
```

要在新组中工作，使用 `newgrp` 命令，后跟你的某个组名，如下所示：

```bash
# newgrp admin
```

按回车键后，你将在新组中工作。要返回默认的 `users` 组，在 shell 提示符下输入 `exit` 并按回车键。

要将文件的组属性更改为新组，你必须是该文件的所有者，或者是将拥有该文件的新组的成员。

### 使用权限

每个 Linux 文件都有三种类型的权限：读、写和执行。你可能有读取文件的权限，但如果没有写权限，你就无法更改或删除它。另一方面，你可能对目录有执行权限，但如果没有读权限，你将无法看到其内容（但你可能能够编辑或删除你拥有的内部文件！）。

#### 更改文件权限

可以使用 `ls` 命令来检查文件权限，包括目录权限。例如，如果你使用 `touch` 命令创建一个文件，然后像这样使用 `ls` 命令：

```bash
$ touch file
$ ls -l file
-rw-r--r-- 1 bball users 0 Apr 5 16:41 file
```

`-rw-r--r--` 表示法指定了用户、组和全局（或世界）权限。此字段表示法也可以用数字表示，例如 644。用户权限为 `rw-`，即 $4+2$。组和全局权限为 `r--`，即 4。在此示例中，作为所有者，你可以读取和写入该文件。名为 `users` 组的成员和其他任何人都只能读取该文件。这三组权限在整个 Linux 文件系统中使用，并通过各种组合用于限制或分配读、写和执行权限。

你还可以查看目录或各种设备的权限。例如：

```bash
$ ls -ld foo2
drwxr-xr-x 2 bball users . 4096 Apr 5 16:52 foo2
$ ls -l /dev/tty80
crw-rw---- 1 root uucp 4, 64 Oct 4 2000 /dev/tty80
$ ls -l /dev/hda1
brw-rw---- 1 root disk 3, 1 Oct 4 2000 /dev/hda1
```
