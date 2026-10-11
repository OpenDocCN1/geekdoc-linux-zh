
用户密码设置为无。
你也可以通过 `SWAT` 程序的网页界面执行此操作。

## 使用 `smbpasswd` 修改密码

比起网页界面更喜欢命令行的用户可以使用 `smbpasswd` 命令更改它们的 Samba 密码。该程序的工作原理与普通密码程序类似，但默认不会更新 `/etc/passwd`；相反，它会更新 Samba 的用户/密码数据库。`smbpasswd` 使用标准的 Windows 协议/语义与服务器进行有关密码更改的通信。因此，通过使用正确的组合

通过参数和选项，你可以诱导该工具在基于 Linux 的宿主机上更改远程原生 Windows 服务器上的用户密码！

要更改用户 `yyang` 的 Samba 密码，请执行此命令：

```
[root@server ~]# smbpasswd yyang

New SMB password:

Retype new SMB password:
```

Samba 可以配置为允许普通用户自行运行 `smbpasswd` 命令来管理自己的密码；唯一的限制是他们必须知道之前的/旧的密码。

提示：可以配置多个基于 Web 的前端界面，以允许用户自行管理密码。例如，`Webmin` 就有一个专门用于此目的模块。

# 使用 Samba 针对 Windows 服务器进行身份验证

到为止，我们讨论的都是 Samba/Linux 世界中的 Samba。或者从字面上说，我们一直都在 Samba 的原生环境中使用它，在那个环境中，它是自己领域的主宰和主人（这并非双关语）。这意味着我们的 Samba 服务器结合基于 Linux 的服务器，负责所有的用户身份验证和授权问题。

我们在本章较早创建的简单 Samba 有它自己的用户数据库（`dat`），将 Samba 用户映射到真实的 Linux/UNIX 用户。这使得 Samba 用户创建的任何文件和目录都具有适当的所有权上下文。但如果我们想要部署的 Samba 服务器的环境是使用 Windows 服务器来管理域内的所有用户呢？而且我们又不想在 Samba 中设置一个独立的用户数据库？这就需要 `winbind` 守护进程。

注意：`Samba4` 是最后也是下一代的 Samba。在许多增强功能中，`Samba4` 原生实现了与 Active Directory（AD）兼容的域控制器，支持 AD 登录和身份协议（Kerberos、LDAP、RPC 等）。这意味着所有当前的 Windows 客户端都可以透明地加入到基于 Linux/UNIX 的 `Samba4` 域，其表现将与作为原生 Windows AD 域的成员完全一样。

## `winbind` 守护进程

`winbind` 守护进程用于从原生 Windows 服务器解析用户账户（用户和组）信息。它也可以用于解析其他系统信息。它可以通过使用 `pam_winbind`（一个与 `winbind` 守护进程交互以帮助通过 Windows NTLM 认证验证用户身份的 PAM 模块）、`ntlm_auth` 工具（一个用于允许外部访问 `winbind` 的 NTLM 认证运行的工具）以及 `libnss_winbind`（`winbind` 的名称服务切换库）来实现。

设置基于 Linux 的机器以咨询 Windows 服务器获取用户身份验证需求的步骤非常简单。它们可以总结如下：

1. 如果尚未安装，请安装 `winbind` 软件。
2. 使用正确的指令配置 Samba 的配置文件（`smb.conf`）。
3. 将 `winbind` 添加到 Linux 系统的名称服务设施（`/etc/nsswitch.conf`）。
4. 将 Linux/Samba 服务器加入 Windows 域。
5. 进行测试。

这里我们展示了一个示例场景，其中名为 `serverA` 的 Linux 服务器将使用 Windows 服务器满足其用户身份验证需求。Samba 服务器将作为 Windows 域成员运行。Windows 服务器运行着 Windows 200x Server 操作系统，并且是一个域控制器（作为 WINS 服务器）。其 IP 地址为 `192.168.1.100`。域控制器以混合模式运行（混合模式操作提供了与 Windows NT 类型域以及 Windows 200x 类型域的向后兼容性）。Windows 域名为 `WINDOW-DOMAIN`。

我们刻意地注释掉了此示例 Samba 配置中的所有定义，因为你必须创建或指定自己的配置（本章的前几个部分介绍了如何执行此操作）。让我们更详细地分解这个过程：

1. 首先，如果尚未安装，请安装 `winbind` 包。在基于 RPM 的系统（如 Fedora、CentOS 或 openSE）上，你可以通过执行此命令安装它：

```
[root@fedora-server ~]# yum -y install samba-winbind
```

在基于 Debian 的发行版（如 Ubuntu）上，你可以使用此命令安装包：

```
master@ubuntu-server:~$ sudo apt-get install samba-winbind
```

2. 接下来，创建一个类似所示的 `smb.conf` 文件：

```ini
#Sample smb.conf file

[global]

workgroup = WINDOW-DOMAIN

security = DOMAIN

username map = /etc/samba/smbusers

log file = /var/log/samba/%m

smb ports = 139 445

name resolve order = wins bcast hosts

wins server = 192.168.1.100

idmap uid = 10000-20000

idmap gid = 10000-20000

template shell = /bin/bash

winbind separator = +

## Share definitions

## [homes]

## comment = Home Directories

## browseable = no

## writable = yes
```

3. 编辑 Linux 上的 `/etc/nsswitch.conf` 文件，使其包含如下内容：

```text
passwd: files winbind

shadow: files winbind

group: files winbind
```

4. 在 Fedora、RHEL 和 CentOS 发行版上，使用命令启动 `winbind`：

```
[root@fedora-server ~]# service winbind start

Starting Winbind services: [ OK ]
```

或者在运行 `systemd` 的 Linux 上，你可以使用 `systemctl` 命令启动 `winbind`：

```
[root@fedora-server ~]# systemctl start winbind.service
```

在 Debian 的发行版上，你可以通过执行此命令启动进程：

```bash
ubuntu-server:-$ /etc/init.d/winbind
```

5. 使用 `net` 命令将 Samba 服务器加入域。假设 Windows 账户密码为 `windows_administrator_password`，输入以下内容：

```bash
## net rpc join -U root$ windows_administrator_password

Joined domain WINDOW-DOMAIN
```

这里，具有加入权限的 Windows 账户密码为 `windows_administrator_password`。

6. 使用 `wbinfo` 工具列出 Windows 域中的所有用户，确保一切正常：

```bash
## wbinfo -u
```
