
## 列表 10.22：采用 `usermod` 将账户添加到组

```
$ sudo groups DAdams
DAdams
$ sudo usermod -a -G Project42 DAdams
$ sudo groups DAdams
DAdams : Project42
$
```

注意列表 10.22，`usermod` 命令将用户添加到组中。`-a` 标志确保用户被追加到组，而不是替换成员身份。`-G` 标志指定组名。要将用户从组中移除，请使用 `usermod` 命令并配合 `-G` 标志列出用户应该保留的组列表。

环境文件实际上是 `shell` 脚本。`Shell` 脚本在第 25 章中有详细介绍。接下来的章节将带你了解各种可用的环境文件。

## 理解用户条目

在用户的家目录 `$HOME` 中可以找到四个潜在的环境文件。对于默认登录或交互式 `shell`，将运行以下列表中找到的第一个文件，并忽略其余文件：

- `.bash_profile`
- `.bash_login`
- `.profile`

通常情况下，第四个文件 `.bashrc` 会从上述列表中找到的文件被调用并运行。然而，每当启动一个非交互式 `shell` 时，都会运行 `.bashrc` 文件。

在列表 10.25 中，在 `Fedora Workstation` 发行版上，系统会检查用户的目录以查找所有环境文件。请注意，其中两个文件未被找到。因此，该系统仅使用了 `.bash_profile` 和 `.bashrc` 文件。

### 列表 10.25：检视用户账户的环境文件

```
$ pwd
/home/Christine
$ ls .bash_profile .bash_login .profile .bashrc
ls: cannot access '.bash_login': No such file or directory
ls: cannot access '.profile': No such file or directory
.bash_profile .bashrc
$
```

> 在引用用户账户的环境文件时，通常会使用表示用户家目录的环境文件符号。例如，你可能会看到 `.bashrc` 环境文件被称为 `$HOME/.bashrc` 或 `~/.bashrc` 文件。

如果你想持久化地修改你 `shell` 的主提示符 (`$PS1`)，可以通过通过向你的其中一个本地环境配置文件添加修改内容来实现。列表 10.26 显示了在 `Fedora Workstation` 发行版上 `PS1` 变量的修改。

### 列表 10.26：持久化设置用户账户的 shell 提示符

```
$ grep PS1 .bash_profile
PS1="To infinity and beyond: "
$
```

注意列表 10.26 中，用户的配置被设置为 `$`。`$HOME/.bash_profile` 中的新提示符设计在文件被运行之前不会生效，这可以通过手动执行，也可以在用户注销并重新登录 `shell` 时自动完成。

这些单独的用户环境文件通常从 `/etc/skel/` 目录填充，取决于你的账户配置设置。对于未来的账户，你可以对骨架环境文件进行更改。请记住，任何可以访问命令行界面的人都有修改其自己的文件的能力。因此，对于需要应用于所有用户的环境配置，最好在全局环境文件之一创建一个全局条目，接下去将介绍这些文件。

## 掌握全局条目

全局配置文件会修改所有启动 `Bash shell` 的用户的工作环境和 `shell` 会话。如前所述，这些文件中的全局条目可以通过账户用户向其 `$HOME` 环境文件添加用户条目来修改。

全局环境文件包括以下内容：

- `/etc/profile` 文件
- `/etc/bash` 目录下的文件
- `/etc/bashrc` 或 `/etc/bash.bashrc`

你的 Linux 系统是否拥有 `/etc/bashrc` 或 `/etc/bash.bashrc` 取决于你运行的是哪个发行版。其中任何一个文件通常都会用户的 `$HOME/.bashrc` 调用。

建议不要为了全局环境需求而修改 `/etc/profile` 或其他文件，而是给它一个 `.sh` 文件扩展名，并将其放置在 `/etc/profile.d/` 目录中。`/etc/profile.d/` 目录下的所有 `.sh` 文件都会通过 `/etc/profile` 环境文件在登录 `Bash shell` 时运行。

现在你已经知道如何在本地和全局设置用户环境的持久化更改。接下来，我们将探索如何监控这些用户。

## 查询用户

几个实用工具允许你审计哪些用户正在访问系统，以及过去访问过系统的用户。你还可以验证当前正在使用的账户名，并查看有关用户账户的各种信息。

### 探索 whoami 工具

`whoami` 命令将显示你当前正在使用哪个账户。虽然这看起来可能很傻，但知道你当前正在使用什么账户很重要，特别是当你的组织有共享账户，或者你使用的发行版允许交互式登录 `root` 账户时。

共享用户账户以及直接登录 `root` 账户被认为是不安全的做法。如果你需要超级用户账户访问权限，最好获得 `sudo` 权限。`sudo` 命令在第 15 章中有详细介绍。

`whoami` 命令在列表 10.27 中演示。注意它只显示当前用户账户的名称。

### 列表 10.27：使用 whoami 工具

```
$ whoami
Christine
$
```

### 理解 who 命令

`who` 命令提供的数据比本身多一点，它显示所有关于你自己的账户的信息，或者查看系统上的每个当前用户。示例在列表 10.28 中所示。

### 列表 10.28：使用 who 命令

```
$ who
user1 tty2  2018-10-03 13:12
Christine pts/0  2018-10-03 14:10 (192.168.0.102)
$
$ who am i
Christine pts/0  2018-10-03 14:10 (192.168.0.102)
$
$ who mom likes
Christine pts/0  2018-10-03 14:10 (192.168.0.102)
$
```

# 第 10 章 管理用户和组

### 列表 10.32: 使用 last 命令（续）

| 用户 | Tty | 登录时间 | 空闲时间 |
|---|---|---|---|
| `Rich` | `tty3` | 10月4日 09:56 | 仍在登录 |
| `Christen` | `pts/1` | 192.168.0.102 | 10月4日 09:14 | 仍在登录 |
| `user` | `tty1` | `tty2` | 10月4日 09:10 | 仍在登录 |
| `reboot` | `system boot` | `4.17.12-200.fc28` | 10月4日 09:09 | 正在运行 |
| `Christen` | `pts/0` | 192.168.0.102 | 10月3日 14:10 - 15:32 (01:22) | |
| `user` | `tty2` | | 10月3日 13:12 - 15:33 (02:21) |

```
-
tmp begins Thu Jul 26 16:30:32 2018
$ 
```

请注意，`/var/log/wtmp` 文件通常由 `cron` 工具进行轮转，该工具在第 26 章中介绍过。如果你需要从旧的 `wtmp` 文件获取信息，可以使用 `-f` 选项。例如，你可以输入 `last -f /var/log/wtmp` 来查看来自 `/var/log/wtmp.1` 文件的数据。

`last` 命令以及这些节中介绍的其他工具对于审计当前用户和检查你自己的账户身份非常有帮助。它们是你的 Linux 管理工具箱中的许多其他工具。

# 管理磁盘空间使用

防止文件系统被文件填满并导致程序或系统问题的一种方法是限制用户的磁盘空间使用设置限制。这是通过配额（`quotas`）实现的。Linux 可以对用户可以创建的文件数量设置上限，或者限制单个用户消耗的总文件系统空间。这些限制不仅适用于用户账户，也适用于组。

![](img/0c1e7d2699b9d354c8d2f84669d18d73_359_0.png)

> Linux 系统通过它们的 `inode` 编号实现文件数量配额。在第 3 章中，我们提到过文件 `inode`（索引）编号。通常每个文件有一个 `inode` 编号，除非该文件是硬链接。

在特定文件系统上启用配额基本上有四个步骤。你需要使用超级用户权限来完成这些步骤。步骤如下：

1. 修改 `/etc/fstab` 文件以启用文件系统配额支持。
2. 如果文件系统已经挂载，请卸载并重新挂载。如果文件系统未挂载，则挂载它。
3. 创建配额文件。
4. 用户或组配额限制和宽限。

# 管理磁盘空间使用

必要的 `/etc/fstab` 修改非常简单。你只需要编辑文件并在文件系统的挂载选项（第四字段）中同时添加 `usrquota` 或 `grpquota`。示例见列表 10.33。

### 列表 10.33: 在 /etc/fstab 中设置文件系统配额

```
$ grep /dev/sdb1 /etc/fstab
/dev/sdb1 /home/user1/QuotaFST ext4 defaults,usrquota,grpquota 0 0
```

一旦修改了 `/etc/fstab` 文件，如果文件系统已经挂载，你需要通过 `mount` 命令将其卸载。然后你可以使用 `mount -a` 命令重新挂载系统，这将会挂载 `/etc/fstab` 文件列出的任何未挂载的文件系统。示例见列表 10.34。

### 列表 10.34: 重新挂载启用配额的文件系统

```
# mount /dev/sdb1
# mount | grep /dev/sdb1
/dev/sdb1 on /home/user1/QuotaFST type ext4 (rw,relatime,seclabel,quota,usrquota,grpquota,data=ordered)
```

注意列表 10.34，你可以通过使用 `mount` 命令和 `grep` 工具来检查挂载是否成功。还要注意，挂载的文件系统同时启用了 `usrquota`（用户配额）和 `grpquota`（组配额）。

一旦文件系统正确挂载并启用配额支持，你就可以创建执行限制所需的配额文件。这是通过 `quotacheck` 选项实现的，该选项通过扫描文件系统创建所需的文件，记录任何当前的配额使用情况。`-u` 选项创建 `quota.user` 文件，`-g` 选项创建 `aquota.group` 文件。因此，如果你只实现用户配额而不是组配额，可以省略 `-g` 选项，反之亦然。使用 `quotacheck` 的示例见列表 10.35。

### 列表 10.35: 使用 quotacheck 创建用户和组配额文件

```
# quotacheck -cug /home/user1/QuotaFST
# ls /home/user1/QuotaFST
aquota.group aquota.user lost+found
```

如果你在多个文件系统上设置配额，可以一次性发出 `quotacheck` 命令。只需配合其他选项使用 `-a` 选项，它就会为 `/etc/mtab` 文件指定为当前挂载的任何启用配额的文件系统创建所需的配额文件。

当配额文件创建后，你开始使用 `edquota` 工具为用户账户和组创建配额限制。要编辑用户配额，使用 `-u` 选项（默认选项），要编辑组配额，使用 `-g` 选项。编辑用户配额的片段示例见列表 10.36。

### 列表 10.36: 使用 edquota 创建用户和组配额文件

```
# edquota -u user1
Disk quotas for user1 (uid 1000):
Filesystem blocks hard inodes soft hard
/dev/sdb1 212 4096 6144 2 0 0
```

当你输入 `edquota` 命令时，你会被放入用于配额文件的 `vim (vi)` 编辑器中，除非你已经将 `EDITOR` 环境变量指向另一个文本编辑器。在配额文件中，有两个你无法永久修改的预设限制：`blocks`（已用数据块）和 `inodes`（当前文件数量）。这是因为这些信息是在之前运行 `quotacheck` 命令时获得的，而不是通过 `edquota` 工具设置的。

然而，你可以修改块和 `inode` 的软限制（`soft limits`）和硬限制（`hard limits`）。当你设置硬限制时，你是在设置用户填充数据的最大块数。当你设置 `inode` 限制时，你是在设置用户可以创建的文件总数。一旦用户达到其中任何一个限制，该账户在该特定文件系统上将不再有可用的磁盘空间或文件创建。注意，如果设置为 `0`，则禁用该限制。

软限制（`Soft limits`）要更人性化。一旦用户设置了软限制，你可以超过此限制运行一段时间。这被称为宽限期（`grace period`）。

一旦你修改了用户（或组）配额，你需要为任何设置的软限制建立宽限期。要此此，请使用 `edquota -t` 命令。这些宽限期适用于所有用户组。示例见列表 10.37。

### 列表 10.37: 使用 edquota 设置软限制宽限期

```
# edquota -t
Grace period before enforcing soft limits for users:
Time units may be days, hours, minutes, or seconds
Filesystem Block grace Inode grace
/dev/sdb1 7days 7days
```

# 摘要

管理 Linux 系统的用户帐户和组成员关系涉及许多关键部分。你需要理解账户创建过程以及所使用的文件。当需要对特定用户进行身份验证问题进行故障排除时，你必须掌握整个机制。此外，能够使用各种实用程序识别不同的用户也会有所帮助。

用户账户可以组合到不同的组中，这提供了额外的访问权限。这些组成员关系是授权的一部分，用户借此进入各种文件和目录。了解组管理的关键领域对于适当的 Linux 系统管理至关重要。

通过适当的验证和授权用户组机制保护系统之外，你还可以防止文件系统被过度使用。特别是设置文件系统用户和组配额将提供额外的保护。

## 考试要点

描述管理用户账户的参与者。`/etc/login.defs` 和 `/etc/default/useradd` 文件配置了 `useradd` 命令默认行为的各种设置。由于这些文件中的指令设置随发行版的不同而异，因此在使用 `useradd` 工具创建账户之前查阅这些文件是明智的。创建账户时，`/etc/passwd`、`/etc/shadow` 和 `/etc/group` 文件都会被修改。根据用户帐户配置，可能会创建用户主目录并从 `/etc/skel/` 复制文件到其中。

总结组的管理。涉及创建、修改和删除组的命令是 `groupadd`、`groupmod` 和 `groupdel` 命令。这些命令会对 `/etc/group` 文件进行修改。如果你需要将用户添加到某个组，则需要使用 `usermod` 实用程序。用户可以使用 `newgrp` 程序轻松地从帐户的默认组切换到该帐户所属成员的另一个组。可以通过 `group` 和 `get` 命令以及查看 `/etc/group` 文件对组成员关系进行审计。

列出环境文件。`Bash shell` 使用环境变量来存储有关 `shell` 会话和工作环境的信息。这些变量通过环境文件设置。运行哪些环境文件取决于用户登录系统的方式以及该帐户所属的发行版。用户环境文件是以点（`.`）开头的隐藏文件，可能是 `.bash_profile`、`.bash_login`、`.profile` 和 `.bashrc` 文件。全局文件可能包括 `/etc/bashrc`、`/etc/bash.bashrc`、`/etc/profile` 以及 `/etc/profile.d/` 目录下的文件。

解释查询用户帐户信息的各种方法。你可以使用多种实用程序来确定当前登录帐户的用户以及未登录用户的帐户信息。`who` 命令有三种变体，即 `whoami`、`who` 和 `w` 实用程序。`id` 程序用于将 `UID` 和 `GID` 节点匹配到特定的用户帐户。该命令不仅有助于查看系统何时重启，还可以查看用户当前是否已登录系统，或者帐户上次被访问的时间。

描述如何管理文件系统使用配额。在系统上设置用户帐户或组配额限制之前，你必须通过 `/etc/fstab` 文件中的 `usrquota` 和 `grpquota` 选项在文件系统上启用配额。一旦文件系统被卸载然后重新挂载，你就可以通过 `quotacheck` 实用程序创建所需的用户和/或组文件。完成后，通过 `edquota` 命令设置用户或组限制。你还可以通过 `repquota` 程序查看和/或验证配额。

## 复习题

1. 下列字段包含在 `/etc/passwd` 文件记录中？（选择多项）。
    - A. 用户帐户的用户名
    - B. 密码
    - C. 密码更改日期
    - D. 特殊标记
    - E. `UID`

2. 下列字段包含在 `/etc/shadow` 文件记录中？（选择多项）。
    - A. 密码过期日期
    - B. 帐户过期日期
    - C. 密码
    - D. 注释
    - E. 默认 `shell`

3. 哪个字段在 `/etc/passwd` 和 `/etc/shadow` 文件记录中包含相同的数据？
    - A. 密码
    - B. 帐户过期日期
    - C. `UID`
    - D. `GID`
    - E. 用户帐户的用户名

4. 下列哪些命令允许你查看 `/etc/passwd` 文件中 `Nuhura` 帐户的记录数据？（选择多项）。
    - A. `getent Nuhura passwd`
    - B. `cat /etc/passwd`
    - C. `passwd Nuhura`
    - D. `grep Nuhura /etc/passwd`
    - E. `getent passwd Nuhura`

5. 使用 `useradd -D` 命令查看账户创建配置指令。该命令从哪个文件中提取其显示的信息？
    - A. `/etc/passwd` 文件
    - B. `/etc/shadow` 文件
    - C. `/etc/group` 文件
    - D. `/etc/login.defs` 文件
