
`cd` `/`

`/usr/sbin/shutdown -g0 -i0 y`

```
如果你想在系统关机前给所有用户五分钟的警告或延迟，将 `-g0` 改为 `-g5`。当关机开始时，随着系统进程的终止，你会看到很多消息。最终你会看到这些消息：

系统已关闭。
正在同步文件系统...完成
按任意键继续

现在你可以安全地关闭系统电源了，或者根据提示按任意键重新启动系统。
```

## 启动 Solaris 或 Windows

如果你的磁盘同时拥有 Solaris UNIX 分区和 Windows 分区，你可以启动其中任何一个操作系统，但不能同时运行它们。

如果 Solaris 是最后一个加载的操作系统，它会安装一个很好的启动程序，为你提供运行 Solaris 或 Windows 的选项。当你第一次通电时，很快就会看到如下屏幕：

SunOS - Intel 平台版

当前磁盘分区信息

| 分区编号 | 状态 | 类型 | 起始 | 长度 |
|---|---|---|---|---|
| 1 | | BIOS | 63 | 4192902 |
| 2 | 激活 | SOLARIS | 4192965 | 4257225 |
| 3 | | | | |
| 4 | | | | |

选择你想启动的分区：

此屏幕显示你可以输入 2 运行 Solaris 或输入 1 运行 DOS/Windows。系统将等待 30 秒。如果你不进行选择，它将启动 Solaris。当 Solaris 启动时，你将获得中断正常启动序列的选项。只需忽略这些并让系统自行启动即可：

> > 让 Solaris 自动启动
启动 Solaris 最简单的方法是通电然后离开；它会自行启动。在启动过程中，你会看到很多中断启动的机会。除非你清楚自己在做什么，否则不要这样做。

如果系统硬件发生更改，或要从不同的设备启动，按 `ESC` 中断自动启动过程。

按 `ESC` 在 5 秒后中断自动启动。

正在初始化系统
请稍候...

```
输入      b[file-name] [boot-flags] 以带选项启动

或      i<ENTER>             进入启动解释器

或      <ENTER>               使用默认值启动
```

```
<<< 5 秒后超时 >>>
```

选择 `(b)` 启动或 `(i)` 解释器：

SunOS Release 5.7 Version Generic_06542-02 [UNIX(R) System V Release 4.0]
Copyright 1993-1998, Sun Microsystems, Inc.
正在配置网络接口: `elx10`.
主机名: `morisol`
系统正在启动。请稍候。
检查文件系统
`/dev/rdsk/c0t0ds7`: 洁。
正在启动根守护进程。

在若干其他启动消息之后，你将看到登录提示。系统现在已就绪，你可以登录了。

## 隐藏 Solaris

如果你想防止其他 Windows 用户被 Solaris 的启动选项困扰，你可以通过从 Windows 或 Solaris 运行 `fdisk` 来隐藏 Solaris，然后将 DOS/Windows 分区设置为活动分区。一旦这样操作，系统将只会启动到 DOS/Windows。如果你以后想启动 Solaris，从 Windows 运行 `fdisk` 并将 Solaris 分区设置为活动。然后重启，Solaris 就会启动。

要在 SCSI 磁盘 0 的 Solaris 上运行 `fdisk`，请输入：

```
fdisk /dev/rdsk/c0t0p0
```

你会看到如下屏幕：

**磁盘总大小为 527 磁道
磁道大小为 16065 (512 字节) 块

| 分区 | 状态 | 类型 | 起始 | 结束 | 长度 | % |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | | DOS-BIG | 0 | 260 | 261 | 50 |
| 2 | 激活 | Solaris | 261 | 525 | 265 | 50 |

选择以下其中之一：

+   1. 创建分区
2. 指定活动分区
3. 删除分区
4. 退出（更新磁盘配置并退出）
5. 取消（不更新磁盘配置直接退出）

输入选择：

输入选项 2，然后选择分区 1 以使 DOS/Windows 分区变为活动。
然后输入选项 4 以更新并退出。按照上一节描述关闭 Solaris。当你重启时，只有 Windows 会启动。

# 第三部分 系统管理

## 第 13 章 用户、组和登录

Steve “Mor” Moritsugu 和 Dan Wilson

- 用户信息
- 主目录
- 密码
- 组
- 登录环境
- 在三种不同类型的 UNIX 上创建用户

> 初初学者提示
本章讨论了用户、组、登录以及相关命令。在最后，它展示了如何在三种不同的 UNIX 上创建新账户，这让你了解这些类型 UNIX 之间的差异和相似之处。如果你在家里安装了 UNIX，应该创建一个非 root 用户，仅在必要时使用 root 账户。

### UNIX 用户帐户

在本章的最后一节中，你将看到如何创建一个新用户并将其分配给多个组。在第 14 章“文件权限与系统安全”中，你将看到用户如何对目录和文件设置权限，以便某些用户可以访问而另一些用户不能。查看以下内容：

```
-rw-rw---- 1 mori dbhelper48 Jul 17 .profile

-rw-rw---- 1 lazar integ      48 Jul 29 .csh

-rw-rw---- 1 stall dbhelper    51 Mar 24 .login
```

在本例中，如下：`profile` 属于用户 `mori` 和组 `dbhelper`。`.csh` 属于用户 `lazar` 和组 `integ`。`.login` 属于用户 `stall` 和组 `dbhelper`。

以下是每个用户的：

- 每个用户有一个唯一的用户 ID `UID`。
- 每个用户有一个主组。
- 每个组有一个唯一的组 ID `GID`。
- 每个新文件由创建它的用户所有并属于该用户的组。
- 用户可能属于多个组，以及登录组。
- 每个用户的主目录通常是唯一的，但可能被多个用户共享。

### id 命令

`id` 命令显示关于用户的以下信息：

```
$ id

uid=418(mori) gid=50(group) groups=50(group),102(maint),103(customer),104(mtcopy),108(dtlib),109(mtbackup)

$
```

在本例中，`id` 命令显示：

- 用户名是 `mori`。
- 用户 ID `UID` 是 418。
- 主组是 `group`。
- 组 ID `GID` 是 50。
- 用户属于这些组：`group`, `maint`, `customer`, `mtcopy`, `dtlib`, `mtbackup`。
- `id` 命令显示用户所属每个组的 GID。

### 主目录

系统管理员可以将任何目录分配给用户的主目录。如果你不知道自己的主目录，运行这两个命令：

```
$ cd

$ pwd

/u/mori
```

带参数的 `cd` 命令进入主目录。`pwd` 显示你所在地。在前例中，主目录是 `/u/mori`。
在你的主目录下找到这些文件：

- `.profile`——登录时会自动执行（如果你的默认 shell 是 Bourne shell），或者通常包含初始化代码。
- `.csh`——如果你使用 C shell，登录时会自动执行。
- `.login`——如果你使用 C shell，登录时会自动执行另一个文件。
- `.exrc`——你可以将喜欢的设置命令放入此文件中，以便每次调用 `vi` 编辑器时自动建立。
- `.forward`——如果此文件存在，会将你的邮件转发到指定的用户。如果列出了多个用逗号分隔的名字，你的邮件将被复制并发送给每个人。
- `.hosts`——此文件允许网络中其他系统的用户无需提供密码即可登录你的账户。此文件还允许其他系统的用户无需输入密码即可 `cp` 复制你的文件。
- `.plan`——此文件可以通过 `finger` 命令查看，以便其他用户阅读你放在那里的任何计划，例如九月休假。
- `.project`——与 `.plan` 类似，通过 `finger` 命令可以使用你包含的任何项目信息。

### finger 命令

带有用户名参数的 `finger` 命令显示关于该此类类型信息：

```
finger mori

Login: mori Name: Steve Moritsugu

Directory: /u/mori

Shell: /bin/ksh

On Mon Sep 20 08:35 on tty1 (messages off) from sm

On Mon Sep 20 08:59 on tty14, idle 0:06, (messages off) from sm

No unread mail

Project:

Will be at BIS Oct 15, 2000 teaching a seminar.
```
