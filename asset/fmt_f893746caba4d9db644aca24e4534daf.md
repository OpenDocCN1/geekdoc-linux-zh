
# 13.3.2 为黄金镜像配置 LDAP 自动挂载

在本节中，我们将关闭控制器并启动黄金镜像来配置运行在 LINUX2 上的 LDAP 认证和 `/home/` 自动挂载。启动会话并启动黄金镜像：

```
Red Hat Enterprise Server release 4.9 (Final)
Kernel 2.6.18-el5 on s390
login: root
Password:
Last login: Fri Dec 15 09:49 from 9.56
shutdown -h

==> ipl
```

## 配置 LDAP

你可以使用 `authconfig-tui` 命令（图形界面下可以使用 `authconfig`）修改认证设置。使用 Tab 键在字段间移动，使用空格键更改选择，使用 Enter 键选择：

```bash
# authconfig-tui
```

+---------------------+--------------------+

| User Information    | Authentication                   |

|---------------------|------------------|

|[*] Cache Information |[*] Use MD5 passwords                 |

|[*] Use local         |[*] Use Shadow passwords             |

|[*] LDAP             |[*] LDAP Authentication         |

|[*] NIS              |[*] Use kerberos                  |

|[*] Use Winbind      |[*] SMB Authentication              |

|                                     |[*] Use Winbind Authentication       |

|                                     |[*] Local authorization is sufficient |

+---------------------+--------------------+

|                     | Cancel               | Next               |

在 Information 下，选择 Cache information 和 Use LDAP。在 Authentication 下，选择 LDAP Authentication 和 Local authorization is sufficient。当你切换到 Next 按钮时按 Enter 键

将 Server 值指向 LDAP 服务器。在本示例中，它是 `ldap://12.5.32/`。设置 Base DN 为你的后缀值。在本示例中，它是 `dc=it,dc=ibm,dc=com`。点击 OK。

你的客户端现在指向 LDAP 服务器。使用 `id ldapuser1` 进行测试：

```bash
# id ldapuser1
uid=500(ldapuser1) gid=500(ldapuser1) groups=500(ldapuser1)
context=root:system_r:unconfined_t:s0:s0:c0.102
```

认证也允许 LDAP。通过启动另一个 LDAP 服务器的 SSH 会话并以 `ldapuser1` 登录进行测试：

```
login as: ldapuser1
ldapuser1@12.5.32 password:
```

当你拥有 `ldapuser1` 会话时，这表明认证工作正常。

## 配置自动挂载

现在 SSH 到黄金镜像以配置自动挂载器。在 `/etc/auto.master` 底部添加 `/home` 条目：

```bash
# /etc/auto.master
/nfs /etc/auto.controller
home /etc/auto.home
```

创建文件 `/etc/auto.home` 并其中添加一行：

```bash
# /etc/auto.home
* /12.5.32:/home/
```

星号 (`*`) 用作通配符表示本地子目录。和符号 (`&`) 用于远程系统名或远程子目录。任何本地目录名都会替换 `&` 字符。

最后，重启 `autofs` 并使用 `su` 登录 `ldapuser1` 进行测试。你会发现 `/home/ldapuser1` 已从 LDAP 服务器挂载：

```bash
# service autofs restart
Stopping automount: [ OK ]
Starting automount: [ OK ]
$ su ldapuser1
$ pwd
/home/ldapuser1
$ mount | grep ldapuser1

12.5.32:/home/ldapuser1 /home/ldapuser1 type nfs (rw,addr=12.5.32)
```

你已经配置了自动挂载器，在登录时挂载远程 LDAP 用户的主目录。

关闭黄金镜像并启动控制器 (200)。使用 `clone.sh` 脚本创建一个新的虚拟机。启动新虚拟机的 SSH 会话，进行 LDAP 认证并使用 NFS 自动挂载 `/home/`。

# 13.4 救援 Linux 系统

本节描述了如何为了故障排除将你的 Linux 服务器引导到不同的模式。在需要更高级的故障排除时，将 Linux 引导到单用户模式并进入救援环境。

## 13.4.1 进入单用户模式

当你需要恢复 root 密码或在引导 Linux 进入默认运行时遇到问题时，单用户模式会很有帮助。要进入单用户模式，首先从 320 控制台 IPL 你的 Linux 服务器。你将看到类似所示的消息：

```
zIPL v1.3.2 interactive boot menu
0. default (linux)
1. linux
Note: VM users please use '#cp vmsg <input>'
Please choose (default will boot in 15 seconds):
```

使用 `#cp vmsg` 命令引导所需的菜单选项（零，在本示例中），跟随数字 1 进入单用户模式：

```
==> cp vmsg 0 1
```

在经过初始内核启动消息后，你应该看到：

INIT: Entering level: 1

Entering non-interactive startup

Telling INIT to go to single user mode.

INIT: Going single user

INIT: Sending processes the TERM signal

INIT: Sending processes the KILL signal

sh-000#

在单用户模式下，你以 root 用户身份登录。你可以使用 `passwd` 命令设置 root 密码。`/etc/fstab` 中的所有文件系统已挂载，但网络尚未启动。要退出单用户模式，你可以输入 `reboot`，或者输入 `init 3` 继续引导。

## 13.4.2 进入救援环境

如果你遇到根文件系统错误或其他阻止你进入单用户模式的问题，可以进入 `rescue` 环境。该环境在内存中加载 Linux 镜像，并且不会尝试挂载根文件系统。

要进入救援环境，请启动交互式 Linux 安装。执行以下步骤在 LINUX03 上进入救援环境：

- 1. 登录 LXNMAINT。将 RHEL EXEC 复制到一个名为 RESCUE EXEC 的新文件，并将用户的 PAM-RHS 文件复制到新文件（在本例中为 LINUX03 RESCUE）：

```
== copy rh15z exec d rescue =
== copy linux03 pam-rh5 d = rescue =
```

- 2. 接下来，编辑 RESCUE EXEC 以使其指向新的 LINUX03 救援文件：

```
== edit RESCUE EXEC

00005 "PUN RHEL5      KERNEL * (NOH)
00006 "PUN userid()   RESCUE * (NOH)
00007 "PUN RHEL5      INITRD * (NOH)

==== file
```

- 3. 编辑 LINUX03 救援文件，将任何 kickstart 或 VNC 行替换为救援命令行：

```
== edit LINUX03 rescue
ramdisk_size=40000 root=/dev/ram0 ip=off
CMMSOFILE=LINUX03-RHS
rescue
```
