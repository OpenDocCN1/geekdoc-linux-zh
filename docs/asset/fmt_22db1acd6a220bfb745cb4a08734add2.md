
虽然在`/proc/sys/`中这样快速设置值在测试期间很有帮助，但在生产系统上的工作效果并不理想。当机器重启时，所有`/proc/sys/`的特殊设置都会丢失。要保留你希望永久生效的设置，将其添加到`/etc/sysctl.conf`文件中。每次系统启动时，`init`程序都会运行`/etc/rc.d/rc`脚本，该脚本执行`sysctl /etc/sysctl.conf`以传递给内核的值。添加到`/etc/sysctl.conf`的任何值都会影响每次系统启动。

## 5.5. 附加资源

以下是关于`proc`系统的更多信息来源。

### 5.5.1. 安装文档

系统中提供了各种关于`/proc/`目录文档：
- `/usr/src/linux-2.4/Documentation/filesystems/proc.txt` —— 关于`/proc/`目录各个方面的限制信息。
- `/usr/src/linux-2.4/Documentation/sysrq.txt` —— 系统请求的概述。
- `/usr/src/linux-2.4/Documentation/sysctl.txt` —— 关于内核（`kernel.txt`）和虚拟内存使用（`vm.txt`）的提示。
- `/usr/src/linux-2.4/Documentation/networking/ip-sysctl.txt` —— 关于 IP 网络选项。
- `/usr/src/linux-2.4/` —— 关于`/proc/`的最权威信息，确保你的系统中安装了 Linux 内核源码并查看`/usr/src/linux-2.4/`目录。

### 5.5.2. 有用网站

- [http://www.linuxhq.org](http://www.linuxhq.org) —— 该网站维护了 Linux 内核、补丁以及各种版本的文档。

# 第 6 章 用户与组

用户和组的管理是 Linux 系统管理的核心任务。每个用户和组都有一个唯一的标识 ID (`UID`) 和组 ID (`GID`)，分别被分配给用户、组以及文件的创建者。系统管理员通过 `root` 用户可以更改文件的读取、写和执行权限。管理用户和组是一项繁琐的任务，但最简单的方法是使用以下工具：
- `useradd`, `usermod`, 和 `userdel` —— 添加和修改用户账户的标准方法。
- `groupadd`, `groupmod`, 和 `groupdel` —— 添加和修改用户组的标准方法。
- `passwd` —— 管理密码的标准方法。
- `pwck`, `pwunconv` —— 用于验证和转换密码的工具。

关于用户和组管理的概述，请参见“用户与组配置”章节。

## 6.2. 标准用户

在`/etc/passwd`文件中，组 ID (`GID`) 是用户的主组。标准组列表如下：

| 用户 | UID | GID | 目录 | Shell |
| :--- | :--- | :--- | :--- | :--- |
| root | 0 | 0 | / | /bin/bash |
| bin | 1 | 1 | /bin | /sbin/nologin |
| daemon | 2 | 2 | /sbin | /sbin/nologin |
| adm | 3 | 4 | /var/adm | /sbin/nologin |
| lp | 4 | 7 | /var/lpd | /sbin/nologin |
| sync | 5 | 0 | /sbin | /bin/sync |
| shutdown | 6 | 0 | /sbin | /sbin/shutdown |
| halt | 7 | 0 | /sbin | /sbin/halt |
| mail | 8 | 12 | /var/sp/mail | /sbin/nologin |
| news | 9 | 13 | /var/sp/news | /sbin/nologin |
| uucp | 10 | 14 | /var/sp/uucp | /sbin/nologin |
| operator | 11 | 0 | /root | /sbin/nologin |
| games | 12 | 100 | /usr/games | /sbin/nologin |
| gopher | 13 | 30 | /usr/lib/gopher-data | /sbin/nologin |
| ftp | 14 | 50 | /var/ftp | /sbin/nologin |
| nobody | 99 | 99 | / | /sbin/nologin |
| rpm | 37 | 37 | /var/lib/rpm | /bin/bash |
| vcsa | 69 | 69 | /dev | /sbin/nologin |
| ntp | 38 | 38 | /etc/ntp | /sbin/nologin |
| canna | 39 | 39 | /var/lib/canna | /sbin/nologin |
| nscd | 28 | 28 | / | /sbin/nologin |
| rpc | 32 | 32 | / | /sbin/nologin |
| postfix | 89 | 89 | /var/sp/postfix | /bin/true |
| named | 25 | 25 | /var/named | /bin/false |
| amanda | 33 | 6 | /var/lib/amanda/ | /bin/bash |
| postgres | 26 | 26 | /var/lib/pgsql | /bin/bash |
| sshd | 74 | 74 | /var/empty/shdd | /sbin/nologin |
| rpcuser | 29 | 29 | /var/lib/nfs | /sbin/nologin |
| nsfnobody | 65534 | 65534 | /var/lib/nfs | /sbin/nologin |
| pvm | 24 | 24 | /usr/share/pvm3 | /bin/bash |
| apache | 48 | 48 | /var | /bin/false |
| xfs | 43 | 43 | /etc/X11/fs | /sbin/nologin |
| desktop | 80 | 80 | /var/lib/menu/kde | /sbin/nologin |

| 用户 | UID | GID | Shell |
| --- | --- | --- | --- | --- |
| gdm | 42 | 42 | /var/qdm | /sbin/nologin |
| mysql | 27 | 27 | /var/lib/mysql | /bin/bash |
| webalizer | 67 | 67 | /var/www/html/usage | /sbin/nologin |
| mailman | 41 | 41 | /var/mailman | /bin/false |
| mailnull | 47 | 47 | /var/spool/mqueue | /sbin/nologin |
| smmsp | 51 | 51 | /var/spool/mqueue | /sbin/nologin |
| squid | 23 | 23 | /var/spool/squid | /dev/null |
| ldap | 55 | 77 | /var/lib/ldap | /bin/false |
| netdump | 34 | 34 | /var/crash | /bin/bash |
| pcap | 77 | 78 | /var/arpwatch | /sbin/nologin |
| ident | 98 | 98 | / | /sbin/nologin |
| privoxy | 100 | 101 | /etc/privoxy | / |
| radvd | 75 | 75 | / | /bin/false |
| fax | 78 | 78 | /var/spool/fax | /sbin/nologin |
| wnn | 49 | 49 | /var/lib/wnn | /bin/bash |

表 6-1. 标准组

## 6.3. 标准组

表 6-2 列出了通过“全选”安装时配置的标准组。组存储在 Red Hat Linux 的 `/etc/group` 文件中。

| 组 | GID | 成员 |
| --- | --- | --- |
| root | 0 | root |
| bin | 1 | root, daemon |
| daemon | 2 | root, daemon |
| sys | 3 | root, adm |
| adm | 4 | root, adm, daemon |
| tty | 5 | |
| disk | 6 | root |
| Ip | 7 | daemon, lp |
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
| ftp | 50 | |
| lock | 54 | |
| nobody | 99 | |
| users | 100 | |
| rpm | 37 | rpm |
| utmp | 22 | |
| floppy | 19 | |
| vcsa | 69 | |
| ntp | 38 | |
| canna | 39 | |
| nscd | 28 | |
| rpc | 32 | |
| postdrop | 90 | |
| postfix | 89 | |
| named | 25 | |
| postgres | 26 | |
| sshd | 74 | |
| rpcuser | 29 | |
| nfsnobody | 65534 | |
| pvm | 24 | |
| apache | 48 | |
| xfs | 43 | |
| desktop | 80 | |
| gdm | 42 | |
| mysql | 27 | |
| webalizer | 67 | |
| mailman | 41 | |
| mailnull | 47 | |
| smmsp | 51 | |
| squid | 23 | |
| ldap | 55 | |
| netdump | 34 | |
| pecap | 77 | |
| ident | 98 | |
| privoxy | 101 | |
| radvd | 75 | |
| fax | 78 | |
| slocate | 21 | |
| wnn | 49 | |

表 6-2. 标准组

## 6.4. 用户私有组

Red Hat Linux 使用用户私有组（UPG）方案，这使得 UNIX 组更容易管理。
每当向系统添加新用户时，都会创建一个 UPG。UPG 的名称与创建它的用户名称相同，且该用户是该 UPG 的唯一成员。

UPG 使得为新创建的文件或目录设置默认权限变得安全，允许该用户及其所属组对该文件或目录进行修改。
决定应用于新创建的文件或目录的权限的设置称为 `umask`，它在 `/etc/bashrc` 文件中配置。传统上，在 UNIX 系统上，`umask` 被设置为 `022`，这只允许创建文件或目录的用户进行修改。在这种方案下，所有用户都无法修改。

### 6.4.1. 组目录

许多组织为每个主要项目创建 X 组，并将其用户分配到该组，如果他们需要访问 X11 文件。首先，使用以下命令创建 emacs 组：
```
