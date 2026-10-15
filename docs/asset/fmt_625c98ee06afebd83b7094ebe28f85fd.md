
# 任何以 `;`（分号）或 `#`（井号）开头的行
都是注释会被忽略。在示例中，我们将使用 `#` 作为注释，并使用 `;` 用于你可能希望启用的配置文件部分

```
### 全局设置
```
############################ [global]

# workgroup = NT 域名或工作组名称，例如：REDHAT4

workgroup = BOOK

# 仅在设置 security = server 或 domain 时使用 password server 选项

password server = w2kserv
```

一旦你配置了 `/etc/opt/cifsclient/pam/smb.conf`，然后就可以更改 `/etc/pam.conf` 中的参数。对于每个应用程序，你必须指定 `/usr/lib/security/libpam_ntlm.1` 认证模式。例如，在我其中一个系统中，我配置了 PAM 为 CDE 登录 (`dtlogin`)、`CDE` 操作 (`dtaction`) 和密码管理使用 NTLM。此外，我的 `/etc/pam.conf` 如下：

```
#
# PAM 配置
#
# 账户管理
#
dtaction account required /usr/lib/security/libpam_ntlm.1
dtlogin account required /usr/lib/security/libpam_ntlm.1
ftp account required /usr/lib/security/libpam_unix.1
login account required /usr/lib/security/libpam_unix.1
 account required /usr/lib/security/libpam_unix.1
OTHER account required /usr/lib/security/libpam_unix.1
#
# 认证管理
#
dtaction auth required /usr/lib/security/libpam_ntlm.1
dtlogin auth required /usr/lib/security/libpam_ntlm.1
ftp auth required /usr/lib/security/libpam_unix.1
login auth required /usr/lib/security/libpam_unix.1
suth auth required /usr/lib/security/libpam_unix.1
OTHER auth required /usr/lib/security/libpam_unix.1
#
# 密码管理
#
dtaction password required /usr/lib/security/libpam_ntlm.1
dtlogin password required /usr/lib/security/libpam_ntlm.1
login password required /usr/lib/security/libpam_unix.1
passwd password required /usr/lib/security/libpam_ntlm.1
OTHER password required /usr/lib/security/libpam_unix.1
#
# 会话管理
#
dtaction session required /usr/lib/security/libpam_ntlm.1
dtlogin session required /usr/lib/security/libpam_ntlm.1
login session required /usr/lib/security/libpam_unix.1
OTHER session required /usr/lib/security/libpam_unix.1
```

## PAM Kerberos

正如你所见，`dtaction` 和 `dtlogin` 应用程序指定了 `libpam_ntlm`。这允许我登录 CDE（见图 8–2）。一旦我登录，就可以运行 `passwd` 命令：如果我执行了 `passwd` 命令，`passwd` 将在 Windows 2000 域控制器上更改我的密码。如果我想访问 Windows 2000 服务器上的共享，我不需要先运行 `cflogin` 工具，因为我已经通过 NTLM 完成了身份验证。换句话说，我的交互式登录发生在 CDE 登录屏幕；我的网络登录发生在 CDE 登录界面（图 8–2 `CDE 登录界面`）。

这种认证，HP-UX 支持 Kerberos，基于 PAM 认证模块。

### 8.3.1 配置 HP-UX KDC 和应用程序服务器

你需要安装 MIT Kerberos 版本以使 HP-UX 系统成为 KDC 或应用程序服务器。这样做将为你提供重要的工具（如 `kadmin` 和 `ktutil`）。你可以从 `web.mit.edu/kerberos/www/` 获取发行。对于 KDC，你需要配置以下文件：

- `/usr/local/var/krb5dc/kdc.conf`
- `/etc/pam.conf`
- `/etc/krb5.conf`
- `/etc/services`

#### 8.3.1.1 `/usr/local/var/krb5dc/kdc.conf`

此文件包含 KDC 参数，仅适用于 KDC。以下是发布说明中的示例 `kdc.conf`。请根据你的环境进行修改。

```
[kdcdefaults]

kdc_defaults = 88,750

[realms]

REALM.HP_COM = {

database_name = /usr/local/var/krb5dc/principal

admin_keytab = /usr/local/var/krb5dc/kadm5.keytab

acl_file = /usr/local/var/krb5dc/kadm5.acl

dict_file = /usr/local/var/krb5dc/kadm5.dict

key_stash_file = /usr/local/var/krb5dc/.k5.REALM.HP_COM

kadmind_port = 749

max_life = 10h 0m 0s

max_renewable_life = 7d 0h 0s

master_key_type = des-cbc-crc

supported_enctypes = des-cbc-crc:normal

}
```

使 HP-UX 系统成为 KDC 还有额外的步骤。更多信息请参阅 MIT 发行版附带的指南以及 HP 的 PAM Kerberos 发布说明（可用 `docs.com`）。然而，最好使用 Windows 2000 域控制器作为 KDC，因为其默认安装了 Kerberos 并配置了域。

#### 8.3.1.2 `/etc/pam.conf`

你的 HP-UX 应用程序服务器是运行 Telnet 服务 (`telnetd`)、`Ftp` (`ftp`) 或类似程序的主机。因此，例如，如果你想通过 Telnet 连接到另一个系统，必须确保该系统配置为使用 Kerberos 认证。如果你

## PAM Kerberos

当你使用 CDE 登录本地工作站时，Kerberos 会执行你的身份验证，此时你必须配置 `dtlogin` 使用 Kerberos。你通过编辑 `/etc/pam.conf` 并为每个服务指定 PAM Kerberos 认证模块 `/usr/lib/security/pam_krb5.1/` 来配置这些服务。以下是登录和 `ftp` 的示例：
```
