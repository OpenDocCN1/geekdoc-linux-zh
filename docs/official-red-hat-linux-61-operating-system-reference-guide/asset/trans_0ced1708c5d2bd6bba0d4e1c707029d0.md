

route, shutdown, swapoff, swapon, update

## /usr 目录

/usr 目录用于存放可在整个站点共享的文件。/usr 目录通常拥有独立的分区，且应支持只读挂载。以下目录应为 /usr 的子目录：

```
/usr
├─ X11R6
├─ bin
├─ dict
├─ doc
├─ etc
├─ games
├─ include
├─ info
├─ lib
├─ libexec
├─ local
├─ man
├─ sbin
├─ share
└─ src
```

X11R6 目录用于 X 窗口系统（在 Red Hat Linux 中为 XFree86），bin 用于可执行文件，doc 用于杂项文档（非 man 手册页文档），etc 用于站点范围的配置文件，include 用于 C 头文件，info 用于 GNU info 文件，lib 用于库文件，man 用于 man 手册页，sbin 用于系统管理二进制文件（那些不属于 /sbin 的文件），src 用于源代码。

## /usr/local 目录

FHS（文件系统标准）规定：

> “/usr/local 层次结构供系统管理员在安装本地软件时使用。它必须保证在系统软件更新时不会被覆盖。它可以用于在机器组之间共享的程序和数据，但这些内容不能存放在 /usr 中。”

/usr/local 目录在结构上与 /usr 目录类似。它具有以下子目录，其用途与 /usr 目录中的相应子目录相似：

- /usr/local
  - bin
  - doc
  - etc
  - games
  - info
  - lib
  - man
  - sbin
  - src

## /var 目录

由于 FHS 要求能够将 /usr 挂载为只读，因此任何需要写入日志文件或使用交换分区或锁目录的程序，最好将这些内容写入 /var 目录。FHS 指出 /var 用于：

> “...可变数据文件。这包括交换分区目录和文件、管理及日志数据，以及瞬态和临时文件。”

以下目录应为 /var 的子目录：

- /var
  - catman
  - lib
  - local
  - lock
  - log
  - named
  - nis
  - preserve
  - run
  - spool
    - anacron
    - at
    - cron
    - fax
    - lpd
    - mail
    - mqueue
    - news
    - rwhe
    - samba
    - slrnpull
    - squid
    - up2date
    - uucp
    - uucppublic
    - vbox
    - voce
  - tmp

系统日志文件，如 `wtmp` 和 `lastlog`，存放于 `/var/log` 中。`/var/lib` 目录还包含 RPM 系统数据库。格式化后的 man 手册页存放于 `/var/catman`，锁文件存放于 `/var/lock`。`/var/spool` 目录包含若干子目录，供需要存储数据文件的各个系统使用。

## 2.1.2 Red Hat Linux 中的 /usr/local

在 Red Hat Linux 中，`/usr/local` 的预定用途与 FHS 规定略有不同。FHS 规定 `/usr/local` 应存放那些需要在系统软件升级过程中保持安全的软件。由于来自 Red Hat 的系统升级通过 RPM 系统和 Gnome-RPM 安全地进行，因此无需通过将文件放在 `/usr/local` 中来保护它们。相反，我们建议使用 `/usr/local` 来存放本机特有的软件。

例如，假设你通过只读 NFS 从 *beavis* 挂载了 `/usr`。如果你希望安装某个软件包或程序，但无权向 *beavis* 写入数据，那么你应该将其安装在 `/usr/local` 下。日后，如果你成功说服 *beavis* 的系统管理员在 `/usr` 中安装该程序，你就可以从 `/usr/local` 中将其卸载。

## 2.2 Red Hat 特殊文件位置

除了位于 `/var/lib/rpm` 中与 RPM 系统相关的文件（有关 RPM 的更多信息请参见第 6 章 *使用 RPM 进行软件包管理*）之外，还有两个其他特殊位置，它们被保留用于 Red Hat Linux 的配置和运行。

控制面板及相关工具将许多脚本、位图和文本文件放在 `/usr/lib/rhs` 中。这里可能没有什么需要你编辑的内容。另一个位置 `/etc/sysconfig` 存储配置信息。该目录中文件的主要使用者是启动时运行的脚本。虽然可以手动编辑这些文件，但最好使用相应的控制面板工具。

## 2.3 用户、组和用户私有组

传统上，管理用户和组是一项繁琐的工作，但 Red Hat Linux 提供了一些工具和约定，使得用户和组的管理变得更加容易。

虽然你可以通过 shell 提示符使用 `useradd` 来创建新用户，但管理用户和组最简单的方式是通过 `Linuxconf`（参见第 3 章 *系统配置*）。

接下来，我们将讨论管理用户和组的基本结构。

### 2.3.1 标准用户

在表 2–1 *标准用户* 中，你可以找到安装过程设置的标准用户（这基本上是 `/etc/passwd` 文件）。该表中的 **组 ID**（GID）是用户的 *主组*。有关组的使用详情，请参见第 2.3.3 节 *用户私有组*。

| **用户** | **UID** | **GID** | **主目录** | **Shell** |
| :------- | :------ | :------ | :----------------- | :-------- |
| root     | 0       | 0       | /root              | /bin/bash |
| bin      | 1       | 1       | /bin               |           |
| daemon   | 2       | 2       | /sbin              |           |
| adm      | 3       | 4       | /var/adm           |           |
| lp       | 4       | 7       | /var/spool/lpd     |           |
| sync     | 5       | 0       | /sbin              | /bin/sync |
| shutdown | 6       | 0       | /sbin              | /sbin/shutdown |
| halt     | 7       | 0       | /sbin              | /sbin/halt |
| mail     | 8       | 12      | /var/spool/mail    |           |
| news     | 9       | 13      | /var/spool/news    |           |
| uucp     | 10      | 14      | /var/spool/uucp    |           |
| operator | 11      | 0       | /root              |           |
| games    | 12      | 100     | /usr/games         |           |
| gopher   | 13      | 30      | /usr/lib/gopher-data |         |
| ftp      | 14      | 50      | /home/ftp          |           |
| nobody   | 99      | 99      | /                  |           |

### 2.3.2 标准组

在表 2–2 *标准组* 中，你可以找到安装过程设置的标准组（这基本上是 `/etc/group` 文件）。

**表 2–2 标准组**

| 组 | GID | 成员 |
| --- | --- | --- |
| root | 0 | root |
| bin | 1 | root, bin, daemon |
| daemon | 2 | root, bin, daemon |
| sys | 3 | root, bin, adm |
| adm | 4 | root, adm, daemon |
| tty | 5 | |
| disk | 6 | root |
| lp | 7 | daemon, lp |
| mem | 8 | |
| kmem | 9 | |
| wheel | 10 | root |
| mail | 12 | mail |
| news | 13 | news |
| uucp | 14 | uucp |
| man | 15 | |
| games | 20 | |
| gopher| 30 | |
| dip | 40 | |
| ftp | 50 | |
| nobody| 99 | |
| users | 100 | |
| floppy| 19 | |

### 2.3.3 用户私有组

Red Hat Linux 采用**用户私有组**（UPG）机制，这使得 UNIX 组的使用变得更加容易。UPG 机制并未在标准 UNIX 处理组的方式上增加或更改任何内容。它只是提供了一种处理组的新约定。每当创建新用户时，默认情况下，他或她拥有一个独特的组。该机制的工作方式如下：

*用户私有组*
每个用户都有自己的主组，且只有该用户是此组的成员。
*umask = 002*

传统的 UNIX umask 为 022，它防止其他用户以及 *用户主组的其他成员* 修改用户的文件。由于在 UPG 机制中每个用户都有自己私有的组，因此这种“组保护”是不需要的。umask 设为 002 可以防止用户修改其他用户的私有文件。umask 在 /etc/profile 中设置。

#### 目录上的 setgid 位

如果在目录上设置了 setgid 位（使用 chmod g+s 目录），那么在该目录中创建的文件，其组将设置为该目录的组。

大多数 IT 组织喜欢为每个主要项目创建一个组，并将人员分配到他们应该所在的组中。然而，传统上文件管理比较困难，因为当某人创建一个文件时，该文件由其所属的主组拥有。当一个人参与多个项目时，将正确的文件关联到正确的所有权组就变得很困难。在 UPG 机制中，组会根据项目自动分配给文件，这使得管理群组项目变得非常简单。

假设你有一个名为 *devel* 的大型项目，许多人正在 *devel* 目录中编辑 *devel* 文件。创建一个名为 *devel* 的组，使用 chgrp 将 *devel* 目录更改为 *devel* 组，并将所有 *devel* 用户添加到 *devel* 组中。现在，所有 *devel* 用户都可以编辑 *devel* 文件并在 *devel* 目录中创建新文件，这些文件将始终保持其 *devel* 组。因此，它们始终可以被其他 *devel* 用户编辑。

如果你拥有像 *devel* 这样的多个项目，并且有参与多个项目的用户，那么这些用户在从一个项目切换到另一个项目时，永远不需要更改他们的 umask 或组。每个项目主目录上的 setgid 位会“选择”适当的组。

由于每个用户的主目录由该用户及其私有组拥有，因此在主目录上设置 setgid 位是安全的。但是，默认情况下，文件以用户的主组创建，因此 setgid 位是多余的。

#### 用户私有组的理由

虽然 UPG 对于 Red Hat Linux 6.2 并不新颖，但许多人仍然对此存有疑问，例如为什么需要 UPG。以下是该机制的理由。

