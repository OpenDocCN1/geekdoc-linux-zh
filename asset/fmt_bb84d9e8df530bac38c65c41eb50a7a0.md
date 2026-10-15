
## 练习 6-5：修改和删除组账户

本练习应在 `server1` 上以 `root` 身份完成。

在此练习中，你将把 `linuxadm` 组更改为 `sysadm` 并将 GID 改为 `6000`。你将把 `user200` 的主组改为 `sysadm`。最后，你将删除 `sysadm` 组并验证这些操作。

- 1. 将 `linuxadm` 的名称改为 `sysadm`：

```root
root@server1 ~]## groupmod -n sysadm linuxadm
```

- 2. 将 `sysadm` 的 GID 改为 `6000`：

```root
root@server1 ~]## groupmod -g 6000 sysadm
```

- 3. 确认上述操作：

```root
root@server1 ~]## grep /etc/group
sysadm:x:6000:user1,user200
root@server1 ~]## grep linuxadm /etc/group
root@server1 ~]## _
```

输出确认了上述两个操作。新组名为为 `sysadm`，新 GID 为 `6000`。成员关系保持不变。还要注意，`linuxadm` 组已不再存在。第二个命令对它没有返回任何内容。

- 4. 删除 `sysadm` 组并确认：

```bash
[root@server1 ~]# groupdel sysadm
[root@server1 ~]# grep sysadm /etc/group
[root@server1 ~]#
```

第二个命令没有返回内容，确认组已成功删除。

## 切换用户和以超级用户身份执行操作

在真实的 Linux 环境中，你总是以普通用户登录。普通用户在系统上拥有有限权限。他们的配置文件允许他们高效且安全地完成日常工作。这样做是为了保护整个系统功能并防止意外问题。有时，普通用户需要切换到另一个用户的身份以该用户的身份执行任务，或者成功执行需要高权限的命令。Linux 提供了两个基本工具来支持用户在这两种情况下。

## 切换（或替换）用户

尽管你可以直接以 `root` 身份登录系统，但这并不是推荐的做法。相反，请使用普通用户账户登录，并在时切换到 `root` 账户。这样更安全并能确保系统的安全和保护。除了变成 `root`，你还可以切换到另一个用户账户。无论哪情况，你都需要知道目标用户的密码。`su` 命令具有切换到其他用户账户的能力。

要从 `user1`（假设你以 `user1` 登录）切换到 `root` 而不执行目标用户的启动脚本（启动脚本将在本章后面的部分介绍），请运行 `su` 命令并在提示时输入 `root` 用户密码：

```bash
[user1@server1 ~]$$ su
```

按下 `Ctrl+d` 组合键返回 `user1` 命令提示符。然后运行带有连字符字符（`-`）的 `su` 命令，以确保也执行目标用户的启动脚本，从而提供与真实登录相似的环境：

```bash
[user1@server1 ~]$ su -
```

要切换到不同的用户账户（例如 `user100`），请使用命令指定目标用户的名称。你必须在提示时输入目标用户的密码。

```bash
[user1@server1 ~]$ su - user100
```

RHEL 提供了两个工具——`whoami` 我是谁）和 `logname` 登录名称），它们显示用户的当前身份（切换到目标用户后）以及最初登录用户的身份。让我们看看在切换到 `user100` 后它们报告了什么：

```bash
[user1@server1]$]$ su user100
Password:
[user100@server1 ~]$ whoami
user100
[user100@server1 ~]$ logname
user1
```

`whoami` 命令返回有效的（当前）用户名（`user100`），`logname` 命令报告用户的真实（原始）用户名（`user1`）。要在不切换到该用户的情况下以不同用户发布命令，请对 `su` 使用 `-c` 选项。例如，带有 `--list-services` 选项的 `firewall-cmd` 命令需要超级用户权限。`user1` 可以如下所示使用 `su` 并执行此特权命令以获得所需结果：

```bash
[user1@server1 ~]$ su -c 'firewalld-cmd --list-services'
```

`root` 用户可以切换到系统中存在的任何用户账户，无需提示该用户的密码。

虽然 *su* 命令确实提供了灵活性便利性，但不建议切换到 *root* 账户来执行特权操作。Linux 中有一种更优的方法应该被使用。下一节将对其进行介绍。

## 以超级用户身份执行（或以替换用户身份执行）

在生产 Linux 服务器上，有必要的步骤来确保用户能够顺利地执行分配的任务。在大多数情况下，这需要对某些工具和功能拥有特权访问，而 *root* 用户通常被允许运行这些内容。

RHEL 为普通用户提供了运行特权命令或访问非所有文件的权限，而无需知道 *root* 密码。这允许根据需求为单个用户或用户组灵活地分配特定命令或一组命令。这些用户在执行这些命令时，可以使用名为 *sudo*（超级用户身份执行，即替换用户身份执行）的工具。用户会被提示输入自己的密码，如果正确，命令将为他们成功执行。*sudo* 工具设计用于根据 `/etc/sudoers` 文件或包含目录 `/etc/sudoers.d` 中的文件定义提供受保护的管理功能访问。它还可以允许用户或用户组运行属于其他用户的脚本和应用程序。

任何需要管理命令或非所有文件特权访问的普通用户都定义在 *sudoers* 文件中。该文件可以使用 *visudo* 命令进行编辑，该命令会创建文件的副本作为 *sudoers.tmp* 并应用更改。

`sudo` 命令会将成功的身份验证和命令数据记录到 `/var/log/secure` 文件中，记录的名为执行命令的实际用户（而不是 `root`）。

`sudoers` 文件包含几个示例并附有简要说明。查看这些示例对于进一步理解是一个好主意。

现在，普通用户 `user1` 已被添加到 `sudoers` 配置文件中，在书中接后的示例和练习中，你将在适当的地方使用该账户配合 `sudo`。

## 所有者用户和所属组

在 Linux 中，每个文件和目录都有一个所有者。默认情况下，创建者拥有所有权，但根据需要，可以将其更改并分配给不同的用户。

同样，每个用户都是一个或多个组的成员。组是具有共同权限需求的用户集合。默认情况下，所有者的组会被分配给文件或目录。

让我们以 `user1` 的身份在其家目录下创建一个 `file1`，并显示该文件的详细列表：

```
[user1@server1 ~]$ touch file1
[user1@server1 ~]$ ls -l file1
-rw-rw-r-- 1 user1 0 1000 0 Sep 17 15:00 file1
```

输出表明 `file1` 的所有者是 `user1`，它属于 `user1` 组。如果你想查看相应的 UID 和 GID，可以在命令中指定 `-n` 选项：

```
[user1@server1 ~]$ ls -ln file1
-rw-rw-r-- 1 1000 1000 0 Sep 17 15:00 file1
```

Linux 提供了 `chown` 和 `chgrp` 命令，可以更改文件和目录的所有者和所属组；然而，你必须拥有 `root` 用户权限才能进行这些修改。

## 练习 6-6：修改文件所有者和所属组

此练习应在 `server1` 上以 `user1` 身份执行，并在需要的地方使用 `sudo`。

在此练习中，你将首先在 `user1 /tmp` 下创建一个文件 `file10` 和一个目录 `dir10`，然后通过两次独立的事务将 `file10` 的所有者更改为 `user100`，将所属组更改为 `dba`。然后，你将同时将 `file10` 的所有者更改为 `user200`，所属组更改为 `user100`。最后，你将递归地更改目录 `user200:dba` 的两个属性。确保在必要时使用 `sudo`。

- 1. 进入 `/tmp` 目录并创建 `file10` 和 `dir10`：

```
[user1@server1 ~]$ cd /tmp
[user1@server1 tmp]$ touch file10
[user1@server1 tmp]$ mkdir dir10
```

- 2. 检查并验证两个属性是否已设置为 `user1`：

```
[user1@server1 tmp]$ ls -l file10
-rw-r--r-- 1 user user100 0 Sep 17 15:15 file10
[user1@server1 tmp]$ ls -ld dir10
drwxr-xr-x. 2 user user1 6 Sep 17 15:15 dir10
```

- 3. 将所有者设置为 `user100` 并确认：
