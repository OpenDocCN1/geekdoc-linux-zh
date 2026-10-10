
分别删除 /etc/shadow 文件中加密密码字段开头的两个 `!` 字符。

另一种常用于锁定用户账户的方法是修改 /etc/passwd 文件中用户账户指定的 shell，将 /bin/bash 改为无效的 shell，例如 /bin/false 或 /sbin/nologin。如果没有有效的 shell，用户就无法使用系统。要以这种方式锁定用户账户，您可以编辑 /etc/passwd 文件并进行相应修改，使用 `usermod` 命令的 `-s` 选项，或者使用 `chsh` 命令。以下示例使用 `chsh` 命令将用户 bobg 的 shell 更改为 /bin/false：

```
[root@server1 ~]# chsh -s /bin/false bobg
Changing shell for bobg.
chsh: Warning: "/bin/false" is not listed in /etc/shells
Shell changed.
[root@server1 ~]# _
```

## 删除用户账户

要删除用户账户，您可以使用 `userdel` 命令并指定用户名作为参数。这将删除 /etc/passwd 和 /etc/shadow 文件中对应该用户账户的条目。此外，您可以为 `userdel` 命令指定 `-r` 选项，以删除该用户的 home 目录及其所有内容。

当用户账户被删除时，之前由该用户拥有的任何文件都将变为由代表已删除用户 UID 的数字所拥有。任何未来被分配相同 UID 的用户账户将成为这些文件的拥有者。

例如，假设用户 bobg 离开了公司。要删除 bobg 的用户账户并显示其旧文件的归属，您可以使用以下命令：

```
[root@server1 ~]# userdel bobg
[root@server1 ~]# ls -la /home/bobg
total 52
drwx------  4 1002  1002  4096 Jul 17 15:37 .
drwxr-xr-x  5 root root  4096 Jul 17 15:37 ..
-rw-r--r--  1 1002  1002  24 Jul 17 15:37 .bash_logout
-rw-r--r--  1 1002  1002  191 Jul 17 15:37 .bash_profile
-rw-r--r--  1 1002  1002  124 Jul 17 15:37 .bashrc
-rw-r--r--  1 1002  1002  5542 Jul 17 15:37 .canna
-rw-r--r--  1 1002  1002  820 Jul 17 15:37 .emacs
-rw-r--r--  1 1002  1002  118 Jul 17 15:37 .gtkrc
-rw-r--r--  3  1002  1002  4096 Jul 17 15:37 .kde
drwxr-xr-x  2 1002  1002  4096 Jul 17 15:37 .xemacs
-rw-r--r--  1 1002  1002  3511 Jul 17 15:37 .zshrc
[root@server1 ~]# _
```

从上述输出中可以看到，bobg 用户的 UID 为 1002。现在假设公司雇佣了 Sue——即用户 sueb——来取代 bobg。您可以将 UID 1002 分配给 Sue 的用户账户。虽然她会有自己的 home 目录 (/home/sueb)，但她也将成为 /home/bobg 中所有 bobg 旧文件以及其他位置旧文件的拥有者。然后，她可以将她需要的文件复制到她自己的 home 目录，并作为其工作职责的一部分删除她不需要的文件。

要创建一个 UID 为 1002 的用户 sueb 并列出 bobg 的 home 目录中文件的归属，您可以使用以下命令：

```
[root@server1 ~]# useradd -u 1002 sueb
[root@server1 ~]# ls -la /home/bobg
total 52
drwx-----   4 sueb   sueb      4096 Jul 17 15:37 .
drwxr-xr-x   5 root   root      4096 Jul 17 18:56 ..
-rw-r--r--   1 sueb   sueb        24 Jul 17 15:37 .bash_logout
-rw-r--r--   1 sueb   sueb       191 Jul 17 15:37 .bash_profile
-rw-r--r--   1 sueb   sueb       124 Jul 17 15:37 .bashrc
-rw-r--r--   1 sueb   sueb       5542 Jul 17 15:37 .canna
-rw-r--r--   1 sueb   sueb       820 Jul 17 15:37 .emacs
-rw-r--r--   1 sueb   sueb       118 Jul 17 15:37 .gtkrc
-rw-r--r--   3 sueb   sueb      4096 Jul 17 15:37 .kde
drwxr-xr-x   2 sueb   sueb      4096 Jul 17 15:37 .xemacs
-rw-r--r--   1 sueb   sueb       3511 Jul 17 15:37 .zshrc
[root@server1 ~]#
```

## 管理组

迄今为止，向系统添加组最简单的方法是编辑 /etc/group 文件。另一种方法是使用 `groupadd` 命令。要向系统添加一个名为 group1 的组并为其分配 GID 492，您可以使用以下命令：

```
[root@server1 ~]# groupadd -g 492 group1
[root@server1 ~]#
```

然后，您可以使用 `usermod` 命令的 `-G` 选项来向组中添加成员。要将用户 mary 添加到该组并查看添加结果，您可以使用以下 `usermod` 命令：

```
[root@server1 ~]# usermod -G group1 mary
[root@server1 ~]# tail -1 /etc/group
group1:x:492:mary
[root@server1 ~]#
```

还存在 `groupmod` 命令，可用于修改组名称和 GID；以及 `groupdel` 命令，可用于从系统中移除组。

要查看您所属的组的列表，只需运行 `groups` 命令即可；要查看每个组的 GID，只需运行 `id` 命令即可。主组在每个命令的输出中总是首先列出。以下输出展示了 root 用户执行这些命令时的示例输出：

```
[root@server1 ~]# groups
root bin daemon sys adm disk wheel
[root@server1 ~]# id
uid=0(root)   gid=0(root)   groups=0(root),1(bin),2(daemon),3(sys),
4(adm),6(disk),10(wheel)
[root@server1 ~]#
```

在上述输出中，root 用户的主组是 root 组。该组作为 root 用户创建的所有文件的组拥有者，如下所示：

```
[root@server1 ~]# touch samplefile1
[root@server1 ~]# ls -l samplefile1
-rw-r--r-- 1 root root 0 Aug 27 19:22 samplefile1
[root@server1 ~]# _
```

要暂时将主组更改为 `groups` 和 `id` 命令输出中列出的其他组，您可以使用 `newgrp` 命令。之后创建的任何新文件都将拥有新的组拥有者。以下输出演示了更改 root 用户的主组如何影响文件归属：

```
[root@server1 ~]# newgrp sys
[root@server1 root]# id
uid=0 (root) gid=3 (sys) groups=0 (root), 1 (bin), 2 (daemon), 3 (sys), 4 (adm), 6 (disk), 10 (wheel)
[root@server1 ~]# touch samplefile2
[root@server1 ~]# ls -l samplefile2
-rw-r--r-- 1 root sys 0 Aug 27 19:28 samplefile2
[root@server1 ~]# _
```

![](img/c27875544958897d817484d558c208c8_483_0.png)

> 如果您使用本节前面描述的组密码，可以使用 `newgrp` 命令将主组更改为您不是其成员的组，前提是在提示时提供相应的组密码。

root 用户可以使用 `newgrp` 命令将其主组更改为任何其他组。

尽管命令行工具通常用于管理用户和组，但您也可以使用图形化工具来创建、修改和删除系统上的用户和组账户。这些工具在后台运行相应的命令行实用工具。要在 Fedora 20 的桌面环境中创建和管理用户和组，您可以在桌面环境中打开终端应用程序，切换到 root 用户，并运行 `system-config-users` 命令以打开图 10-6 中所示的用户管理器实用工具。

![](img/c27875544958897d817484d558c208c8_483_1.png)

**图 10-6 在桌面环境中配置用户和组**

# 章节摘要

- 打印作业在打印到打印机之前会被放入打印队列中。
- 您可以使用 `cupsaccept`、`cupsreject`、`cupsenable` 和 `cupsdisable` 命令来配置打印机的 spooling 或打印设置。
- 使用 `lp` 命令创建打印作业，使用 `lpstat` 命令在打印队列中查看作业，并使用 `cancel` 命令从打印队列中删除作业。
- 您可以使用 `lpadmin` 命令、CUPS Web 管理工具或修改 `/etc/cups/printers.conf` 文件来配置打印机。
- Linux 系统上大多数日志文件存储在 `/var/log` 目录中。
- 系统事件通常由系统日志守护进程 (syslogd) 记录到文件中，或由 systemd 日志守护进程 (journald) 记录到数据库中。
- 您可以使用 `journalctl` 命令查看 journald 数据库的内容。
- 为了节省磁盘空间，日志文件应随时间清理或轮转；logrotate 实用工具可用于轮转日志文件。
- 用户和组账户信息通常存储在 `/etc/passwd`、`/etc/shadow` 和 `/etc/group` 文件中。
- 您可以使用 `useradd` 命令创建用户，使用 `groupadd` 命令创建组。
- 所有用户在登录 Linux 系统之前必须拥有有效的密码。
- 可以使用 `usermod`、`chage`、`chfn`、`chsh` 和 `passwd` 命令修改用户，并使用 `groupmod` 命令修改组。
- `userdel` 和 `groupdel` 命令可分别用于从系统中移除用户和组。

## 关键术语

| 术语 | 描述 |
| :--- | :--- |
| `/etc/cups/cupsd.conf` | 一个包含 cups 守护进程配置的文件。 |
| `/etc/cups/printers.conf` | 一个包含 cups 守护进程打印机配置的文件。 |
| `/etc/default/useradd` | 一个包含用户创建默认值的文件。 |
| `/etc/group` | 包含组定义和成员资格的文件。 |
| `/etc/login.defs` | 一个包含用户创建默认值的文件。 |
| `/etc/logrotate.conf` | logrotate 实用工具用于指定日志文件轮转参数的文件。 |
| `/etc/passwd` | 包含用户账户信息的文件。 |
| `/etc/syslog.conf` | 系统日志守护进程的主配置文件。 |
| `/etc/shadow` | 包含加密密码以及每个用户账户的密码和账户过期参数的文件。 |
