
## 拒绝访问

`deny email_enable` 选项允许你拒绝匿名用户的访问，`banned_file` 选项指定文件（通常为 `vsftpd.banned`）。相反，如果 `vsftpd.user_list` 持有这些用户的地址。`vsftpd.ftusers` 文件列出了那些永远无法访问 FTP 站的用户。这些通常是系统用户，如 `root`、`mail` 和 `nobody`。请参考表 22-3 以获取 `vsftpd` 文件列表。

## 用户访问

`userlist_enable` 选项控制用户的访问，拒绝由 `userlist_file` 选项指定的文件（通常为 `vsftpd.user_list`）中列出的用户访问。相反，如果你想限制访问某些特定用户，你可以更改 `vsftpd.user_list` 文件的含义和用法，以指示仅允许访问的用户，而不是被拒绝访问的用户。要实现这一点，请将 `userlist_deny` 选项设置为 `NO`（其默认值为 `YES`）。只有在 `vsftpd.user_list` 文件中列出的用户将获得访问 FTP 站的权限。

| 文件 | 描述 |
| --- | --- |
| `vsftpd.ftusers` | 始终被拒绝访问的用户列表 |
| `vsftpd.user_list` | 指定被拒绝的用户（如果 `userlist_deny` 为 `NO`，则允许访问） |
| `vsftpd.chroot_list` | 允许访问的本地用户列表（如果 `chroot_local_user` 开启，则拒绝访问） |
| `/etc/vsftpd/vsftpd.conf` | `vsftpd` 配置文件 |
| `/etc/pam.d/vsftpd` | PAM `vsftpd` 脚本 |
| `/etc/rc.d/init.d/vsftpd` | `vsftpd` 服务器脚本，独立模式 |
| `/etc/inetd.d/vsftpd` | Xinetd `vsftpd` 服务器脚本 |

**表 22-3 vsftpd 文件**

## 第六部分：互联网与网络服务

### 用户限制

`ch_list_enable` 选项控制本地用户的访问，允许他们仅访问其主目录，限制系统访问。`chroot_list_file` 选项指定列出允许用户的文件（通常为 `vsftpd.chroot`）。你可以通过 `chroot_local_user` 选项允许本地用户访问。如果设置了此选项，由 `chroot_list_file` 指定的文件将具有相反的含义，列出不允许访问的用户。在下面的示例中，本地用户的访问被限制在 `vsftpd.chroot` 中的用户：

```
chroot_list_enable=YES
chroot_list_file=/etc/vsftpd.chroot_list
```

### 用户认证

`vsftpd` 服务器使用 PAM 服务对通过 FTP 远程访问其账户的本地用户进行认证。在 `vsftpd.conf` 文件，通过 `pam_service_name` 选项指定服务器的 PAM 脚本。

```
pam_service_name=vsftpd
```

在 `/etc/pam.d` 目录下，你将找到一个名为 `vsftpd` 的文件，其中控制 `vsftpd` 服务器访问的条目。PAM 目前配置为对有效账户的用户进行认证，并拒绝对 `/etc/vsftpd.fpusers` 中用户的访问。默认的 `/etc/pam.d/vsftpd` 文件所示：

```
##PAM-1.0
auth required pamfile.so item-user=sense
```

### 命令访问

`recursive_enable` 选项允许用户递归列出子目录。默认情况下，它是关闭的。要启用它，请将 `recursive_enable` 选项设置为 `YES`。`list_mask` 选项允许你指定要列出的子目录。默认是所有子目录。

```
recursive_enable=YES
list_mask=.*
```

`chrootroot` 选项允许将用户限制在其主目录。这通常用于安全目的。要启用它，请将 `chroot_local_user` 选项设置为 `YES`。

```
chroot_local_user=YES
```

## vsftpd 虚拟用户

可以通过利用 PAM 对用户认证来实现虚拟用户。实际上，你是在允许某些用户访问，而无需在 FTP 服务器系统上设置账户。首先，创建一个 PAM 登录数据库文件，供 `/etc/pam.d` 目录下的 PAM 文件使用。然后创建一个虚拟 FTP 用户以及相应的目录，虚拟用户将访问这些目录（详细信息请参阅 `vsftpd.beasts.org`）。然后，在 `vsftpd.conf` 文件中，你可以禁用匿名 FTP：

```
anonymous_enable=NO
local_enable=YES
```

然后启用访客访问：

```
guest_enable=YES
guest_username=virtual
```

# 第六部分：互联网与网络服务

## 专业 FTP 进程：ProFTPD

ProFTPD 基于与 Apache Web 服务器相同的设计，实现了简化的配置结构，并支持虚拟主机等灵活功能。ProFTPD 是一个根据 GNU GPL 协议提供的开源项目。你可以从其网站 `proftpd.org` 下载当前版本。你还可以找到详细的文档，包括常见问题解答（FAQs）、用户手册和示例配置。访问该网站获取新发布和更新。

ProFTPD 设计具有可扩展性，支持可以自定义或由第三方开发者开发的动态模块。目前，已有模块提供 LDAP 和 SQL 身份验证，并有足够的增强模块用于支持用户配额、日志格式和时间限制等功能。

## 安装与启动

如果你使用发行包安装 ProFTPD，所需的配置条目将在你的 `proftpd.conf` 文件中创建。如果你从编译后的源码安装，你可能需要修改提供的默认 `proftpd.conf` 文件中的条目。确保指定的 FTP 用户和组确实存在。

要设置其自动启动的运行级别，可以使用 `chkconfig` 和 `sysrc-conf`。以下命令将 `proftpd` 设置为在运行级别 3 和 5 自动运行：

```bash
chkconfig --35 proftpd on
```

若要在默认级别开启服务，可以使用 `rconf` 或 `services-admin`。

## 身份验证

ProFTPD 中的用户身份验证可以通过 PAM、LDAP 或 SQL 实现。对于 LDAP 或 SQL，你需要加载相应的 ProFTPD 模块。PAM 身份验证是默认选项（有关 LDAP 和 PAM 的更多信息请参见第 30 章）。确保 `/etc/pam.d/ftp` 文件已安装以提供 PAM FTP 支持。ProFTPD 还支持标准密码和无密码登录。通过通过将 `AuthPAMAuthoritative` 指令设置为 `off` 可以关闭默认 PAM 身份验证，允许使用 LDAP 等其他身份验证方法。如果你的服务器通过 IP 掩装技术隐藏在本地网络中，可以使用 `MasqueradeAddress` 来指定其公网主机名，使其真实主机名保持隐藏。

## proftpd.conf 和 .ftaccess

ProFTPD 仅使用位于 `/etc` 目录下的单一配置文件 `proftpd.conf`。配置条目以指令的形式存在。这种格式主要基于 Apache 配置。通过这些指令，你可以输入基本配置信息（如你的服务器名称），或执行更复杂的操作（如实现虚拟 FTP 主机）。该设计足够灵活，允许你为特定目录、用户或组定义配置。

要配置特定目录，你可以在该目录内放置一个带有配置选项的 `.ftaccess` 文件。这些 `.ftaccess` 选项的优先级高于 `proftpd.conf` 目录中的条目。`.ftaccess` 文件的设计类似于 Apache Web 服务器中用于配置特定网站目录的 `.htaccess` 文件。你可以在 ProFTPD 网站（`proftpd.org`）以及作为 ProFTPD 软件包一部分安装在 `/usr/doc` 中的 ProFTPD 文档中找到 ProFTPD 配置参数的完整列表。在创建新配置时，你应该复制一份 `proftpd` 配置文件并进行修改。然后你可以使用 `proftpd` 命令配合 `-c` 选项和文件名测试你的语法。

```bash
proftpd -c new.conf
```
