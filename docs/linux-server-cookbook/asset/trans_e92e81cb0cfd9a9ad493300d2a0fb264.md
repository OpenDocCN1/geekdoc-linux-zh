

# 表 4.1：/etc/login.defs 中的选项

| 选项 | 值 |
|---|---|
| PASS_WARN_AGE | 7 |
| UID_MIN | 1000 |
| UID_MAX | 60000 |
| SYS_UID_MIN | 201 |
| SYS_UID_MAX | 999 |
| GID_MIN | 1000 |
| GID_MAX | 60000 |
| SYS_GID_MIN | 201 |
| SYS_GID_MAX | 999 |
| CREATE_HOME | yes |
| USERGROUPS_ENAB | yes |
| ENCRYPT_METHOD | SHA512 |

在安装 Linux 发行版时，会配置一个 Linux 标准基础（LSB）。该基础包含预定义的用户和组数量，其中大多数具有历史意义，但在现代系统中并不使用。表 4.2 显示了新安装的 Ubuntu Server 中配置的用户：

## 表 4.2：Ubuntu Server 中创建的默认用户

| 用户名 | UID | 主 GID | 用户信息 | 主目录 | Shell |
|---|---|---|---|---|---|
| root | 0 | 0 | root | /root | /bin/bash |
| daemon | 1 | 1 | daemon | /usr/sbin | /usr/sbin/nologin |
| bin | 2 | 2 | bin | /bin | /usr/sbin/nologin |
| sys | 3 | 3 | sys | /dev | /usr/sbin/nologin |
| sync | 4 | 65534 | sync | /bin | /bin/sync |
| games | 5 | 60 | games | /usr/games | /usr/sbin/nologin |
| man | 6 | 12 | man | /var/cache/man | /usr/sbin/nologin |
| lp | 7 | 7 | lp | /var/spool/lpd | /usr/sbin/nologin |
| mail | 8 | 8 | mail | /var/mail | /usr/sbin/nologin |
| news | 9 | 9 | news | /var/spool/news | /usr/sbin/nologin |
| uucp | 10 | 10 | uucp | /var/spool/uucp | /usr/sbin/nologin |
| proxy | 13 | 13 | proxy | /bin | /usr/sbin/nologin |
| www-data | 33 | 33 | www-data | /var/www | /usr/sbin/nologin |
| backup | 34 | 34 | backup | /var/backups | /usr/sbin/nologin |
| list | 38 | 38 | Mailing List Manager | /var/list | /usr/sbin/nologin |
| irc | 39 | 39 | ircd | /run/ircd | /usr/sbin/nologin |
| gnats | 41 | 41 | Gnats Bug-Reporting System (admin) | /var/lib/gnats | /usr/sbin/nologin |
| nobody | 65534 | 65534 | nobody | /nonexistent | /usr/sbin/nologin |

用户 *nobody* 是一个特殊用户，当某些服务不想使用专用用户来运行应用程序时会使用它。安装过程中也会创建一个名为 *nobody* 的组，正如 *表 4.3* 中显示的 Ubuntu Server 中创建的默认组所示：

## 表 4.3：Ubuntu Server 中创建的默认组

| 组 | GID | 组 | GID | 组 | GID | 组 | GID |
|---|---|---|---|---|---|---|---|
| root | 0 | news | 9 | floppy | 25 | irc | 39 |
| daemon | 1 | uucp | 10 | tape | 26 | src | 40 |
| bin | 2 | man | 12 | sudo | 27 | gnats | 41 |
| sys | 3 | proxy | 13 | audio | 29 | shadow | 42 |
| adm | 4 | kmem | 15 | dip | 30 | utmp | 43 |
| tty | 5 | dialout | 20 | www-data | 33 | video | 44 |
| disk | 6 | fax | 21 | backup | 34 | plugdev | 46 |
| lp | 7 | voice | 22 | operator | 37 | staff | 50 |
| mail | 8 | cdrom | 24 | list | 38 | games | 60 |

## 用户账户的最佳实践

对于人类用户账户，建议保护账户使用强密码并应用过期规则。如果可能，也建议禁用密码登录（例如在 SSH 中），改为仅使用 SSH 私钥/公钥进行登录。

保持每个系统所需用户的列表非常重要，并移除系统不需要的用户，以避免密码泄露或漏洞，这些都可能影响我们的基础设施。另一件需要跟踪的重要事情是用户和组的归属映射，从而确保用户不属于他不应该加入的组。

使用 *Ansible* 等工具自动化用户的管理和维护，将有助于管理员保持系统安全且易于维护。

## 管理用户的命令

### 命令 id

这个简单的命令显示有关用户及其所属组的信息。可以在不输入任何参数的情况下执行此命令以获取执行该命令的用户的**信息**。此外，通过指定一个用户作为参数，用户可以查看该用户的组信息。命令 `id` 的常用选项显示在 *表 4.4* 中：

| 选项 | 描述 |
|:---------------------------------------|:----------------------------------------------------|
| -g, --group | 仅打印有效组 ID |
| -G, --groups | 打印所有组 ID |
| -u, --user | 仅打印有效用户 ID |

*表 4.4：* *命令 id 的常用选项*

在 *图 4.1* 中，展示了不带选项和参数但带有其他用户参数以及使用前述选项的输出示例，如下所示：

```bash
agonzalez@ubuntu:~$ id
uid=1000(agonzalez) gid=1000(agonzalez) groups=1000(agonzalez),4(adm),24(cdrw),27(sudo),30(dip),46(plugdev),110(lxd)
agonzalez@ubuntu:~$ id root
uid=0(root) gid=0(root) groups=0(root)
agonzalez@ubuntu:~$ id -u
1000
agonzalez@ubuntu:~$ id -g
1000
agonzalez@ubuntu:~$ id -G
1000 4 24 27 30 46 110
```

*图 4.1：* *使用命令 id 的输出示例*

### 命令 useradd 和 adduser

命令 **useradd** 是在所有 Linux 发行版中可用的命令，旨在创建用户。某些发行版，例如 Ubuntu Server，提供了一个工具 **adduser** 来帮助用户交互式地输入用户信息。在一些其他发行版中，例如 Red Hat Enterprise Linux，执行命令 **adduser** 时会调用命令 **useradd**。

默认值（在文件 /etc/default/useradd 中指定）可以使用命令 `useradd -D` 列出，如图 4.2 所示：

```bash
root@ubuntu:~# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/sh
SKELETON=/etc/skel
CREATE_MAIL_SPOOL=no
```

*图 4.2：命令 useradd 的默认选项示例*

此命令唯一需要的参数是要创建的用户名。命令 **useradd** 的常用选项显示在 *表 4.5* 中：

| 选项 | 描述 |
| :--- | :--- |
| -C, --comment COMMENT | 通常用于指定用户的完整姓名。 |
| -d, --home-dir HOME_DIR | 用户的主目录，而不是使用 /home/<username> |
| -g, --gid GROUP | 用户的主组名或组 ID。 |
| -G, --groups GROUP1,GRP2 | 用户的辅助组列表，用逗号分隔。 |
| -k, --skel SKEl_DIR | 使用的骨架目录，而不是 /etc/skel。 |
| -m, --create-home | 如果用户的主目录不存在，则创建它。 |
| -r, --system | 创建系统账户而不是普通用户。GID 将不同。 |
| -s, --shell SHELL | 用户登录 Shell 的路径。 |
| -u, --uid UID | 用户 ID 的数值。对于迁移用户很有用。 |
| -U, --user-group | 创建一个与用户同名的组，并将其设置为用户的主组。 |

*表 4.5：命令 useradd 的常用选项*

在 *图 4.3* 中，创建了一个名为 **testuser** 的用户，指定了前表中的一些选项，以及使用命令 *id* 的选项：

```bash
root@ubuntu:~# useradd -c "Test User" -G syslog -m testuser
root@ubuntu:~# id testuser
uid=1001(testuser) gid=1001(testuser) groups=1001(testuser),113(syslog)
```

*图 4.3：使用 useradd 创建用户 testuser 的示例。*

命令 **adduser**，当作为单独工具可用时，通常不使用任何选项。然而，常用选项在表 4.6 中描述：

| 选项 | 描述 |
|---|---|
| --home DIR | 主目录，而不是默认目录。 |
| --shell SHELL | 默认 Shell，而不是默认的 Shell。 |
| --no-create-home | 不创建主目录。 |
| --gecos GECOS | 指定用户信息 |
| --gid ID | 指定主组 ID 或名称。 |

*表 4.6：命令 adduser 的常用选项*

*图 4.4* 显示了使用命令 **adduser** 时的输出和交互：

```bash
root@ubuntu:~# adduser testuser2
Adding user 'testuser2' ...
Adding new group 'testuser2' (1002) ...
Adding new user 'testuser2' (1002) with group 'testuser2' ...
Creating home directory '/home/testuser2' ...
Copying files from '/etc/skel' ...
New password:
Retype new password:
passwd: password updated successfully
Changing the user information for testuser2
Enter the new value, or press ENTER for the default
Full Name []: Test User2
Room Number []:
Work Phone []:
Home Phone []:
Other []:
Is the information correct? [Y/n]
```

*图 4.4：使用 adduser 创建用户 testuser2 的示例*

### 命令 usermod

命令 **usermod** 允许在创建用户后修改用户的大部分参数。唯一需要的参数是要修改的用户名。常用选项与 **useradd** 类似，描述在表 4.7 中：

| 选项 | 描述 |
|---|---|

