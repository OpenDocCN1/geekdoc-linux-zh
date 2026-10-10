
以下目录应为 `/var` 的子目录：

```
/var
|- log
|- catman
|- lib
|- local
|- named
|- nis
|- preserve
|- run
|- lock
|- tmp
+- spool
    |- at
    |- cron
    |- lpd
    |- mail
    |- mqueue
    |- rwho
    |- smail
    |- uucp
    +- news
```

诸如 wtmp 和 lastlog 等系统日志文件位于 `/var/log`。`/var/lib` 目录还包含 RPM 系统数据库。格式化手册页位于 `/var/catman`，锁定文件位于 `/var/lock`。`/var/spool` 目录包含若干个子目录，供需要存储数据文件的各类系统使用。

### 10.1.2 Red Hat Linux 中的 /usr/local

在 Red Hat Linux 中，`/usr/local` 的预期用途与 FSSTND 规范中指定略有不同。FSSTND 规定 `/usr/local` 应作为存储那些需要避免系统软件升级影响的软件的位置。由于通过 RPM 系统和 Glint 从 Red Hat 进行的系统升级是安全的，因此你不需要通过将这些文件放入 `/usr/local` 来保护它们。相反，我们建议你使用 `/usr/local` 来安装仅限于你本地机器使用的软件。

例如，假设你通过只读 NFS 从 *beavis* 挂载了 `/usr`。如果你想要安装某个软件包或程序，但不被允许向 *beavis* 写入数据，你应该将其安装在 `/usr/local` 下。稍后，如果你成功说服了 *beavis* 的系统管理员在 `/usr` 上安装该程序，你可以将其从 `/usr/local` 卸载。

## 10.2 Red Hat 的特殊文件位置

除了位于 `/var/lib/rpm` 的与 RPM 系统相关的文件外（参见第 7 章），还有两个其他特殊位置是专门为 Red Hat Linux 的配置和操作保留的。

控制面板及相关工具会在 `/usr/lib/rhs` 中放置大量内容。这里可能没有任何你愿意手动编辑的东西。它们主要是小型脚本、位图和文本文件。

另一个位置 `/etc/sysconfig` 存储配置信息。此目录中文件的主要使用者是在启动时运行的脚本。你可以手动编辑这些文件，但最好使用正确的控制面板工具。

## 10.3 用户、组和用户专用组

传统上，管理用户和组是一件繁琐的事情。Red Hat Linux 提供了一些工具和约定，使用户和组的管理更加简便且实用。

管理用户和组的最简单方法是通过控制面板中的用户和组模块（关于控制面板的详细信息请参见第 8 章，关于用户和组模块的详细信息请参见 8.1 节）。

你也可以使用 `adduser` 在命令行创建新用户。

### 10.3.1 标准用户

表 10.3.1 列出了安装过程中设置的标准用户（这基本上就是 `/etc/passwd` 文件）。此表中的组 ID (GID) 是该用户的*主要组*。关于组的使用详情，请参见 10.3.3 节。

| 用户 | UID | GID | 主目录 | Shell |
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

![](img/06353bca937b38b02602dcfb58824d72_158_0.png)

### 10.3.2 标准组

表 10.3.2 列出了由安装过程设置的标准组（这基本上就是 *etc/group* 文件）。

| 组 | GID | 成员 |
| :--- | :--- | :--- |
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

图 10.2：标准组

### 10.3.3 用户专用组

Red Hat Linux 使用用户专用组（UPG）方案，这使得 UNIX 组的使用变得非常容易。UPG 方案没有添加或更改标准 UNIX 组处理方式中的任何内容。它只是提供了一种处理组的新约定。每当创建新用户时，默认情况下，该用户拥有一个唯一的组。该方案的工作方式如下：

- **用户专用组**：每个用户都有自己专属的主要组，且只有该用户是该组的成员。

- **umask = 002**：传统的 UNIX umask 是 022，它防止其他用户和*用户主要组的其他成员*修改该用户的文件。由于在 UPG 方案中每个用户都有自己的专用组，因此这种“组保护”是不需要的。umask 为 002 将防止用户修改其他用户的私有文件。umask 在 /etc/profile 中设置。

- **目录上的 SGID 位**：如果你在目录上设置了 SGID 位（通过 *chmod g+s directory*），则在该目录中创建的文件将具有该目录的组属性。

大多数计算站点喜欢为每个主要项目创建一个组，并将人员分配到他们所在的组中。然而，传统上的文件管理比较困难，因为当某人创建文件时，该文件由其所属于的主要组拥有。当一个人参与多个项目时，很难使文件归属于与该相关的项目组。在 UPG 方案中，组会自动根据项目逐个分配给文件，这使得组项目管理的非常简单。

假设你有一个名为 *devel* 的大项目，有许多人在 *devel* 目录中编辑 devel 文件。创建一个名为 *devel* 的组，使用 *chgrp* 将 *devel* 目录的所有权更改为 *devel*，并将所有 devel 用户添加到 *devel* 组中。现在，所有 devel 用户都可以编辑 devel 文件并在 *devel* 目录中创建新文件，且这些文件将始终保持其 *devel* 组属性。因此，它们始终可以供其他 devel 用户编辑。

如果你有多个类似 *devel* 的项目，以及参与多个项目的用户，这些用户在项目间移动时将永远不需要更改他们的 umask 或组。每个项目主目录上的 SGID 位会“选择”正确的组。

由于每个用户的 HOME 目录都归该用户及其专用组所有，因此在 HOME 目录上设置 SGID 位是安全的。不过，默认情况下，文件创建时使用用户的主要组，因此 SGID 位将是冗余的。

### 用户专用组的理由

由于 UPG 方案是新的，许多人对此有疑问，并想知道其必要性。以下是该方案的理论依据。

- 你希望有一群人共同处理一组文件，例如 /usr/lib/emacs/site-lisp 目录中的文件。你信任少数人在那里进行操作，但当然不是所有人都可以。
- 因此你输入：
  ```
  chown -R root.emacs /usr/lib/emacs/site-lisp
  ```
  并将合适的用户添加到该组。
- 为了让用户实际能在该目录中创建文件，你输入：
  ```
  chmod 775 /usr/lib/emacs/site-lisp
  ```
- 但当用户创建新文件时，它会被分配给用户默认组的属性（通常是 users）。为了防止这种情况，你输入
  ```
  chmod 2775 /usr/lib/emacs/site-lisp
  ```
  这会导致该目录中创建的所有内容都具有“emacs”组属性。
- 但新文件需要设置为 664 权限，以便 emacs 组中的其他用户能够编辑它。为此，你需要将默认 umask 设置为 002。
- 嗯，这一切都运行良好，除非你的默认组是“users”，那么你在主目录中创建的每个文件都将对“users”（通常是所有人）中的每个人可写。
- 为了解决这个问题，你为每个用户指定一个“专用组”作为其默认组。

在此处，通过设置默认 umask 为 002 并赋予每个人一个专用默认组，你可以轻松地设置用户可利用的组，而无需进行任何“魔法”操作。只需创建组，添加用户，并对该组目录执行上述的 chown 和 chmod 操作即可。

