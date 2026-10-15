
http://www.pathname.com/fhs/

## 10.1.1 FSSTND 概述

这里提到的目录和文件是 FSSTND 文档中指定目录的一个子集。请检查最新的 FSSTND 文档以获取最新、最完整的信息。

### /etc 目录

`/etc` 目录保留用于本地机器的配置文件。`/etc` 中不应存放任何二进制文件。过去放在 `/etc` 中的二进制文件现在应该放入 `/sbin` 或可能放入 `/bin`。

X11 和 skel 目录应该是 `/etc` 的子目录：

#### /etc

- `X11`
- `skel`

`X11` 目录用于存放 X11 配置文件，例如 `XF86Config`。`skel` 目录用于存放“骨架（skeleton）”用户文件，这些文件是在首次创建用户时用于填充家目录的文件。

### /lib 目录

`/lib` 目录应该只包含执行 `/bin` 和 `/sbin` 中二进制文件所需的库。

### /sbin 目录

`/sbin` 目录用于存放 root 用户使用的可执行文件，且仅限于启动和挂载 `/usr` 以及执行系统恢复操作所需的可执行文件。FSSTND 规定：

## 10.1 文件系统结构

`/sbin` 通常包含启动系统所必需的文件，以及 `/bin` 中的二进制文件。在 `/usr` 已知挂载（在没有问题的情况下）之后执行的任何程序都应该放在 `/usr/sbin` 中。仅限本地的系统管理二进制文件应该放在 `/usr/local/sbin` 中。

至少以下程序应该位于 `/sbin` 中：

```
clock, getty, init, update, mkswap, swapon, swapoff,
halt, reboot, shutdown, fdisk, fsck.*, mkfs.*, lilo,
arp, ifconfig, route
```

### /usr 目录

`/usr` 目录用于存放整个站点共享的文件。`/usr` 目录通常有自己的分区，并且应该是可只读挂载的。以下目录应该是 `/usr` 的子目录：

| /usr |
| :--- |
| X11R6 |
| bin |
| dict |
| doc |
| etc |
| games |
| include |
| info |
| lib |
| local |
| man |
| sbin |
| share |
| src |

`X11R6` 目录用于 X Window 系统（在 Red Hat Linux 上的 XFree86），`bin` 用于可执行文件，`doc` 用于随机的非 man 页文档，`etc` 用于站点范围的配置文件，`include` 用于 C 头文件，`info` 用于 GNU info 文件，`lib` 用于库，`man` 用于 man 手页，`sbin` 用于系统管理二进制文件（那些不属于 `/sbin` 的文件），`src` 用于源代码。

### /usr/local 目录

FSSTND 规定：

> “`/usr/local` 层次级结构供系统管理员在本地安装软件时使用。它需要确保在系统软件更新时不会被覆盖。它可以用于在组机器之间共享但在 `/usr` 中未找到的程序和数据。”

`/usr/local` 目录的结构与 `/usr` 目录相似。它具有以下子目录，其用途与 `/usr` 目录中的子目录相似：

| /usr/local |
| :--- |
| bin |
| doc |
| etc |
| games |
| include |
| info |
| lib |
| man |
| sbin |
| src |

### /var 目录

由于 FSSTND 要求能够以只读方式挂载 `/usr`，因此任何写入日志文件或需要缓存（spool）或锁目录的程序可能将它们写入 `/var` 目录。FSSTND 规定 `/var` 是

> "... 变量数据文件。这包括缓存目录和文件、管理和日志数据，以及瞬性和临时文件。”

## 10.1 文件系统结构

以下目录应该是 `/var` 的子目录：

| /var |
| :--- |
| log |
| catman |
| lib |
| local |
| named |
| nis |
| preserve |
| run |
| lock |
| tmp |
| spool |
| at |
| cron |
| lpd |
| mail |
| mqueue |
| rwho |
| smail |
| uuccp |
| news |

系统日志文件如 `wtmp` 和 `lastlog` 放在 `/var/log`。`/var/lib` 目录包含 RPM 系统数据库。格式化后的 man 页放在 `/var/catman`，锁文件放在 `/var/lock`。`/var/spool` 目录拥有各种需要存储数据文件的系统子目录。

### 10.1.2 Red Hat Linux 中的 /usr/local

在 Red Hat Linux 中，`/usr/local` 的预期用途与 FSSTND 规定的略不同。FSSTND 规定 `/usr/local` 应该确保在系统软件更新时不会被覆盖。由于 Red Hat 软件是通过 RPM 安全地更新的，你不需要将文件放在 `/usr/local` 来保护它们。相反，我们建议将 `/usr/local` 用于本地软件。

## 10. 系统管理

例如，假设你通过只读方式挂载了 `/usr`。如果有一个程序是你想要安装的，但被允许写入 beavis...（此处由于原文存在大量重复无效文本，已按指令要求进行处理并翻译）。

## 10.3. 用户、组和用户专用组

`umask` = `002` 传统的 UNIX `umask` `022` 会防止其他用户以及用户主组的其它成员修改用户的文件。由于在 UPG 方案中，每个用户都有自己的私有组，因此不需要“组保护”。`002` 的 `umask` 将防止用户修改其他用户的私有文件。该 `umask` 在 `/etc/profile` 中设置。

**目录上的 SGID 位** 如果你对目录设置了 SGID 位（通过 `chmod g+s directory`），则在该目录中创建的文件，其所属组将设置为该目录的所属组。

大多数计算站点都倾向于为每个主要项目创建一个组，并将人员分配到他们需要加入的组中。然而，传统的这种管理方式一直很困难，因为当有人创建一个文件时，该文件属于他/她所属的主组。当一个人处理多个项目时，很难让文件属于与该项目关联的组。在 UPG 方案中，组是根据每个项目为基础自动分配给文件的，这使得管理小组项目变得非常简单。

假设你有一个名为 `devel` 的大项目，许多人正在 `devel` 目录中编辑 `devel` 文件。创建一个名为 `devel` 的组，使用 `chgrp devel directory` 将目录更改为 `devel`，并将所有 `devel` 用户加入 `devel` 组。现在，所有 `devel` 用户都能够编辑 `devel` 文件并在 `devel` 目录中创建新文件，这些文件将始终保留 `devel` 组。因此，它们始终可以被其他用户编辑。

你有像 `devel` 这样的多个项目，并且用户正在处理多个项目，这些用户在不同项目之间切换时永远不需要更改他们的 `umask` 或组。每个项目主目录上的 SGID 位会“选择”正确的组。

每个用户的 HOME 目录由该用户及其私有组所有，在 HOME 目录上设置 SGID 位是安全的。但是，默认情况下，文件是用用户的主组创建的，因此 SGID 位是多余的。

### 用户专用组的原理

由于 UPG 方案是新的，许多人对它有疑问，并想知道为什么有必要。以下是该方案的原理。

- 你希望一组人在一组文件上工作，例如在 `/usr/lib/emacs/site-lisp-directory` 中。你信任几个人可以在那里折腾，但显然不是所有人。

- 于是你输入：

```
chown -R root.emacs /usr/lib/emacs/site-lisp
```

并将适当的用户添加到该组。

- 为了允许用户实际上在你进入的目录中创建文件，你输入：

```
chmod 775 /usr/lib/emacs/site-lisp
```

- 但当用户创建一个新文件时，它会被分配给用户的默认组（通常是 users）。为了防止这种情况，你输入：

```
chmod 2775 /usr/lib/emacs/site-lisp
```
