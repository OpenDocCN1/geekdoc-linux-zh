
用户 Dylan 虽然存在于 Windows 2000 域中，但在他执行 `cifslogin` 命令之前，他无法访问 `/phome` 目录。如果他知道 Hilary 的密码，他本可以在 `cifslogin w2kserv hilary` 中指定另一个 Windows 2000 账户名。然而，由于他没有这样做，`cifslogin` 假设远程用户也是 dylan。此外，注意上面的输出，dylan 似乎拥有 Hilary 目录。这是因为家目录共享对“所有人”具有“完全控制”权限。但 NTFS 权限会覆盖共享权限，因此如果 NTFS 权限禁止，dylan 就无法写入该目录目录。

### 12.5.3 PAM 和 CIFS/9000 客户端

我们在第 8 章“用户身份验证”中描述了 PAM NTLM，并指出通过使用它，你可以避免使用 `cifslogin`。让我们回顾一下如何操作。

1. 编辑 PAM NTLM 配置文件 `/etc/opt/cisclient/pam/smb.conf`。你设置 `workgroup` 参数（该参数实际上是你的 Windows 2000 域），然后设置 `password server` 参数（这是你的域控制器名称）。在我们的示例中如下所示：

```
==================== Global Settings ==================

[global]

# workgroup = NT-Domain-Name or Workgroup-Name, eg: REDHAT4

workgroup = BOOK
```

# Use password server option only with security = server or
password server = w2kserv
Domain user map = /etc/opt/cisclient/pam/domain_user.map

正如我在配置文件中做的那样，你可能想通过 `domain user map` 参数指定用户映射文件。我的映射文件只包含一个映射：从 root 到 Administrator 的映射。

2. 编辑全局 HP-UX PAM 配置文件 `/etc/pam.conf`。如果你只想在用户登录到运行公共桌面环境 (CDE) 的控制台时进行 NTLM 验证，请在相应部分将 `libpam_unix.1` 条目更改为 `libpam_ntlm`。对于密码验证和支持无密码过期的更改，仅更改身份验证管理（dtlogin 和 dtaction）和密码管理（dtlogin 和 dtaction）部分。如果你确实需要密码过期支持，请更改账户管理（passwd, dtlogin, dtaction）部分。以下是一个示例：

```
# PAM configuration

#

# Authentication management

# auth required libpam_unix.1

login auth required libpam_unix.1

dtlogin auth required libpam_ntlm

dtaction auth required libpam_ntlm

ftp auth required libpam_unix.1

#

# Account management

# auth account required libpam_unix.1

login account required libpam_unix.1

dtlogin account required libpam_ntlm

dtaction account required libpam_ntlm

su account required libpam_unix.1

#

# Session management

# auth session required libpam_unix.1

login session required libpam_unix.1

dtlogin session required libpam_ntlm

dtaction session required libpam_ntlm

su session required libpam_unix.1

#

# Password management

# auth password required libpam_unix.1

login password required libpam_unix.1

dtlogin password required libpam_ntlm

dtaction password required libpam_ntlm

passwd password required libpam_unix.1
```
