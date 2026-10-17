
X11R6 目录用于 X 窗口系统（在 Red Hat Linux 中为 XFree86），`bin` 用于可执行文件，`doc` 用于杂项非手册页文档，`etc` 用于站点范围的配置文件，`include` 用于 C 头文件，`info` 用于 GNU info 文件，`lib` 用于库，`man` 用于手册页，`sbin` 用于系统管理二进制文件（不属于 `/sbin` 的那些），`src` 用于源代码。

### /usr/local 目录

FSSTND 指出：

> “`/usr/local` 层级供系统管理员在本地安装软件时使用。它需要确保在系统软件更新时不会被覆盖。它可用于存放一组机器间可共享但不在 `/usr` 中的程序和数据。”

`/usr/local` 目录的结构与 `/usr` 目录相似。它包含以下子目录，其用途与 `/usr` 目录中的子目录相似：

```
/usr/local
| - bin
| - doc
| - etc
| - games
| - include
| - info
| - lib
| - man
| - sbin
+ - src
```

### /var 目录

由于 FSSTND 要求能够以只读方式挂载 `/usr`，因此任何需要写入日志文件或需要 spool 或锁目录的程序，最好将这些写入 `/var` 目录。FSSTND 指出 `/var` 用于：

> “... 可变数据文件。这包括 spool 目录和文件、管理和日志数据，以及瞬态和临时文件。”

以下目录应该是 `/var` 的子目录：

```
/var
├─ log
├─ catman
├─ lib
├─ local
├─ named
├─ nis
├─ preserve
├─ run
├─ lock
├─ tmp
└─ spool
   ├─ at
   ├─ cron
   ├─ lpd
   ├─ mail
   ├─ mqueue
   ├─ rwho
   ├─ smail
   ├─ uucp
   └─ news
```

系统日志文件，如 `wtmp` 和 `lastlog`，位于 `/var/log`。`/var/lib` 目录还包含 RPM 系统数据库。格式化后的手册页位于 `/var/catman`，锁文件位于 `/var/lock`。`/var/spool` 目录包含用于存储数据文件的各个系统的子目录。

#### 10.1.2 Red Hat Linux 中的 /usr/local

在 Red Hat Linux 中，`/usr/local` 的预期用途与 FSSTND 规范略有不同。FSSTND 指出，`/usr/local` 应作为存放那些需从系统软件升级中保持安全的软件的位置。由于 Red Hat Software 的系统升级通过 RPM 系统和 Glint 安全地进行，因此你不需要通过将文件放在 `/usr/local` 来保护文件。相反，我们建议你使用 `/usr/local` 存放本地计算机专用的软件。

例如，假设你通过只读 NFS 从 `beavis` 挂载了 `/usr`。如果你希望安装某个软件包或程序，但不允许写入 `beavis`，你应该将其安装在 `/usr/local` 下。稍后，如果你成功说服 `beavis` 的系统管理员在 `/usr` 中安装该程序，你可以从 `/usr/local` 中将其卸载。

### 10.2 Red Hat 特殊文件位置

除了位于 `/var/lib/rpm` 的 RPM 系统相关文件（参见第 7 章）外，还有两个其他特殊位置是为 Red Hat Linux 的配置和运行保留的。

控制面板及相关工具将大量内容放置在 `/usr/lib/rhs` 中。这里可能没有什么你希望手动编辑的内容。它主要包含小脚本、位图和文本文件。

另一个位置，`/etc/sysconfig`，存储配置信息。该目录中文件的主要用户是在启动时运行的脚本。虽然可以手动编辑这些文件，但最好使用适当的面板工具。

### 10.3 用户、组和用户私有组

传统上，管理用户和组是一项繁琐的工作。Red Hat Linux 拥有几种工具和约定，使用户和组的管理更容易、更实用。

管理用户和组的最简单方法是通过控制面板的用户和组模块（关于控制面板的详细信息参见第 8 章，关于用户和组模块的详细信息参见第 8.1 节）。

你也可以使用 `adduser` 从命令行创建新用户。

#### 10.3.1 标准用户

表 10.3.1 列出了由安装过程设置的标准用户（这基本上就是 `/etc/passwd` 文件）。此表中的组 ID（GID）是

### 10.3. 用户、组和用户私有组

用户的*主要组*。有关如何使用组的详细信息，请参见第 10.3.3 节。

| 用户 | UID | GID | HOME 目录 | Shell |
| :--- | :--- | :--- | :--- | :--- |
| root | 0 | 0 | /root | /bin/bash |
| bin | 1 | 1 | /bin | |
| daemon | 2 | 2 | /sbin | |
| adm | 3 | 4 | /var/adm | |
| lp | 4 | 7 | /var/spool/lpd | |
| sync | 5 | 0 | /sbin | /bin/sync |
| shutdown | 6 | 0 | /sbin | /sbin/shutdown |
| halt | 7 | 0 | /sbin | /sbin/halt |
| mail | 8 | 12 | /var/spool/mail | |
| news | 9 | 13 | /var/spool/news | |
| uucp | 10 | 14 | /var/spool/uucp | |
| operator | 11 | 0 | /root | /bin/bash |
| games | 12 | 100 | /usr/local/games | |
| gopher | 13 | 30 | /usr/lib/gopher-data | |
| ftp | 14 | 50 | /usr/ths/ftp | |
| nobody | 99 | 99 | /root | |

**图 10.1：标准用户**

#### 10.3.2 标准组

表 10.3.2 列出了安装过程设置的标准组（这基本上是 */etc/group* 文件）。

| 组 | 组 ID | 成员 |
| --- | --- | --- |
| root | 0 | root |
| bin | 1 | root,bin,daemon |
| daemon | 2 | root,bin,daemon |
| sys | 3 | root,bin,adm |
| adm | 4 | root,adm,daemon |
| tty | 5 | |
| disk | 6 | root |
| lp | 7 | daemon,lp |
| mem | 8 | |
| kmem | 9 | |
| wheel | 10 | root |
| mail | 12 | mail |
| news | 13 | news |
| uucp | 14 | uucp |
| man | 15 | |
| games | 20 | |
| gopher | 30 | |
| dip | 40 | |
| ftp | 50 | ftp |
| nobody | 99 | |
| users | 100 | |

**图 10.2：标准组**

### 10.3.3 用户私有组

Red Hat Linux 采用用户私有组（UPG）机制，这使得使用 UNIX 组变得更加容易。UPG 机制并没有在标准 UNIX 处理组的方式中添加或更改任何内容。它只是提供了一种处理组的新约定。每当您创建一个新用户时，默认情况下，该用户拥有一个唯一的组。该机制的工作原理如下：

- **用户私有组** 每个用户都有自己的主要组，且仅该用户是该组的成员。

- **`umask` = 002** 传统的 UNIX `umask` 为 022，它防止其他用户和*用户主要组的其他成员*修改用户的文件。由于在 UPG 机制中每个用户都有自己的私有组，因此不需要这种“组保护”。`umask` 为 002 将防止用户修改其他用户的私有文件。`umask` 在 `/etc/profile` 中设置。

- **目录的 SGID 位** 如果您在目录上设置 SGID 位（使用 `chmod g+s directory`），则在该目录中创建的文件其组将设置为该目录的组。

大多数计算站点喜欢为每个主要项目创建一个组，并将人员分配到他们所在的组中。然而，传统上管理文件很困难，因为当某人创建文件时，该文件归属于其主要组所属的组。当一个人同时处理多个项目时，很难使文件归属于与该项目关联的组。在 UPG 机制中，组是根据项目自动分配给文件的，这使得管理组项目变得非常简单。
