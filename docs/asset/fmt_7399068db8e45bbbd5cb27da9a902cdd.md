
这些命令通常在一行输入——在这里为了格式考虑将其分开了。

在这些命令中，请将 `hostname` 替换为运行 LDAP 服务器的系统主机，确保 `-D` 选项指定的凭据与你 LDAP 服务器的 root 用户匹配，并将 `passwd` 替换你在 OpenLDAP 服务器配置文件 `/etc/openldap/slapd.conf` 中定义的 `rootpw` 项中设置的密码。

遵循这些步骤后，你就可以准备更新客户端系统以使用 LDAP 身份验证（当然还要进行测试）。

# 更新客户端系统使用 LDAP 身份验证

在每个想要新 LDAP 身份验证服务器的系统上，必须执行以下操作：

- 1. 确保已安装 `openldap`、`openldap-clients` 和 `nss_ldap` 软件包。
- 2. 运行 `/usr/bin/authconfig` 命令，并在身份配置屏幕的“User Information”（用户信息）部分选择 LDAP，并在“Authentication”（身份验证）部分选择 Use LDAP for Authentication。图 34-5 显示了选中正确选项的屏幕。
- 3. 选择 Next（下一步）并按回车继续到下一个屏幕，并在整个部分输入 LDAP 服务器的正确主机名和区分名称（distinguished name），示例中使用了适当的基条目：
  ```
  host ldap.vonhagen.org
  base dc=vonhagen,dc=
  ```
  图 34-6 显示了此处适用于本示例的选项的屏幕。选择 OK 并按回车退出 `authconfig` 程序。
- 4. 检查 `/etc/ldap.conf` 文件，确保它包含你在 `authconfig` 程序中输入的 LDAP 设置。如果输入的值没有正确传播到此文件，请手动设置。
- 5. 检查 `/etc/pam.d/system-auth` 文件，确保 LDAP 身份验证信息的条目已正确添加。该文件应该如下所示：
  ```
  auth required /lib/security/$ISA/pam-env.so

  auth sufficient /lib/security/$ISA/pam-unix.so like nullock

  auth sufficient /lib/security/$ISA/pam-ldap.so use_first_pass

  auth required /lib/security/$ISA/pam-deny.so

  account required /lib/security/$ISA/pam-unix.so broken-shadow

  account sufficient /lib/security/$ISA/pam-succeed.if.so use < 100

  quiet

  account [default=auth] success=ok user_unknown=ignore]

  /lib/security/$ISA/pam-ldap.so

  account required /lib/security/$ISA/pam-permit.so

  password requisite /lib/security/$ISA/pam-cracklib.so retry=3

  password sufficient /lib/security/$ISA/pam-unix.so nullock

  use_authok md5 shadow

  password sufficient /lib/security/$ISA/pam-ldap.so use_authtok

  password required /lib/security/$ISA/pam-deny.so

  session required /lib/security/$ISA/pam-limits.so

  session required /lib/security/$ISA/pam-unix.so

  session optional /lib/security/$ISA/pam-ldap.so
  ```
  图 34-5 在 `authconfig` 中选择 LDAP 身份验证。
- 6. 修改你的 `/etc/nwitch.conf` 文件，指定密码、shadow 和组信息首先在 LDAP 中查找。以下是正确的条目：
  ```
  passwd: ldap files

  shadow: ldap files

  group: ldap files
  ```
  这告诉告诉名称服务切换（Name Service Switch）首先检查 LDAP，然后回退到检查客户端系统上的显式密码、shadow 和组文件。

当你下一次在客户端系统登录时，它将联系你的 LDAP 服务器获取身份验证信息。

图 34-6 显示了此处适用于本示例的选项的屏幕。

# 866 第34 章

- `krb5-libs` — 包含 Kerberos 客户端和服务器所需的共享库。
- `krbafs-utils` — 提供 AFS 分布式文件系统的核心实用程序版本，这些程序链接到 krbafs 库。
- `krb5-devel` — 包含用于开发和编译使用 krb5 库的应用的头文件和静态库。
- `krbafs` — 提供 krbafs 共享库，允许程序通过使用 Kerberos 4 凭证获取 AFS 分布式文件系统的令牌，并需要访问 os AFS 库。
- `krb5-auth-dialog` — 包含一个弹出对话框，当用户的 Kerberos 票据即将过期时发出警告并允许他们进行续期。
- `krb5-devel` — 包含开发和编译 Kerberos 5 应用所需的头文件和库。
- `pam_krb5` — 提供一个启用 Kerberos 认证的 PAM（可插拔认证模块）。此包还包含一个 PAM (`pam_krb5afs`)，可以为 AFS 分布式文件系统获取令牌。

> 注意：Red Hat Linux 提供的 Kerberos 软件包并非唯一的可用 Kerberos 实现。其他免费获取的 Kerberos 版本包括Heimdal 项目 (http://www.pdc.kt.se/heimdal)、Shishi 项目 (http://josefson.org/shishi) 以及 MIT Kerberos 母校的原始实现 (http://web.mit.edu/kerberos/www)。

## 核心 Kerberos 实用程序

本节重点介绍与 Kerberos 认证最常用的实用程序。有关这些过程的任何额外信息，请通过使用 `man` 命令查询它们的在线参考信息。所有这些实用程序都位于 Fedora Core 或 RHEL 系统的 `/usr/kerberos/bin` 目录下：

- `destroy` — 删除并移除当前用户的令牌。
- `kinit` — 允许你为指定用户手动获取令牌。
- `klist` — 列出当前用户或指定用户的令牌。
- `destroy` — 删除令牌。

`/bin` 目录也包含 `ftp`、`rcp`、`rsh`、`telnet` 等常用程序的 Kerberos 版本。在使用了 Kerberos 的系统上，你应该将 `/usr/bin/kerberos` 目录放在用户的默认 `PATH` 中，且排于 `/usr/bin` 和 `/bin` 等标准系统目录之前。

## 安装和配置 Kerberos 服务器

在准备用作主密钥发行中心（KDC）的系统上安装了 `krb5-libs`、`krb5-server` 和 `krb5-workstation` 软件包后，配置 Kerberos 环境的第一步是设置你的主密钥发行中心。操作过程如下：

1. 编辑你环境的通用 Kerberos 配置文件 `/etc/kerb5.conf`。该文件识别你 Kerberos 域（realm）中的 KDC 和管理服务器，并为你的内域、Kerberos 应用以及映射到你 Kerberos 域的现有主机名提供默认值。以下是用于该域的 `/etc/kerb5.conf` 示例：
  ```
  [logging]

  default = FILE:/var/log/kerb5-libs.log

  kdc = FILE:/var/log/kerb5kdc.log

  admin_server = FILE:/var/log/kadmind.log

  [libdefaults]

  default_realm = VONHAGEN.ORG

  dns_lookup_realm = false

  dns_lookup_kdc = false

  ticket_lifetime = 24h

  forwardable = yes

  [realms]

  VONHAGEN.ORG = {

  kdc = kerberos.vonhagen.org:88

  admin_server = kerberos.vonhagen.org:749

  default_domain = vonhagen.org

  }

  [domain_realm]

  vonhagen.org = VONHAGEN.ORG

  vonhagen.org = VONHAGEN.ORG

  [kdc]

  profile = /var/kerberos/kerb5kdc/kdc.conf

  [appdefaults]

  pam = {

  debug = false

  ticket_lifetime = 36000

  renew_lifetime = 36000

  forwardable = true

  kerb4_convert = false

  }
  ```
  由 `krb5-server` 软件包安装的 `/etc/krb5.conf` 文件提供的默认值是合理的，但你必须将所有的 `EXAMPLE.COM` 更改为你的域名称，并将所有的 `example.com` 更改为你的域名（在上面的示例中分别为 `VONHAGEN.ORG` 和 `vonhagen.org`）。你必须确保在你在 `[realms]` 部分中识别为默认 KDC 和管理服务器的系统上，所有客户端都存在 DNS 或 `/etc/hosts` 条目。

2. 编辑密钥发行中心配置文件 `/var/kerberos/krb5kdc/kdc.conf`。该文件的配置在 `/etc/ker5.conf` 文件的 `[kdc]` 部分提供。与 `/etc/ker5.conf` 文件一样，你必须对该文件进行的主要更改是将 `EXAMPLE.COM` 实例更改为你的域名称，在下面的示例中为 `VONHAGEN.ORG`：
  ```
  [dcdefaults]

  acl_file = /var/kerberos/krb5kdc/kadm5.acl

  dict_file = /usr/share/dict/

  admin_server = /var/kerberos/krb5kdc/masterkey

  db_mode = noauth

  [realms]

  VONHAGEN.ORG

  masterkey = /var/kerberos/krb5kdc/masterkey

  supported_encypes = des-crc,des-hmac
  ```

3. 使用 `krb5_util` 命令创建数据库和你的存储文件（stash file）。存储文件是主密钥的加密副本，用于自动验证 KDC。系统将提示你输入两次主密码。
  ```
  # /var/kerberos/sbin/krb5_util create -r VONHAGEN.ORG -s

  Initializing database '/var/kerberos/krb5kdc/principal'

  You will be prompted for the master password.

  Enter master key:

  Re-enter master key:
  ```
  该命令在指定的defaults指定的目录下创建各种文件：数据库文件（principal）、数据库锁文件（principal.lock）和存储文件（kstash）。

4. 编辑 ACL 定义文件 `/var/kerberos/krb5kdc/kadm5.acl`，将默认域（EXAMPLE.COM）更改为你创建的域（示例中为 `VONHAGEN.ORG`）。该文件的默认条目以 `*/admin` 开头，赋予任何管理权限的用户对 Kerberos 数据库的完全访问权限。更新此文件后，其内容所示：
  ```
  */admin@VONHAGEN.ORG
  ```
  Kerberos 管理权限非常细致，允许你为某些用户授予不同级别的管理权限。查看 `/usr/share/doc/krb5-server` 中的 Kerberos 文档可获得更多关于在此文件中表示不同级别 Kerberos 权限的详细信息。如果你随后想为具有管理权限的用户细化权限，你应该在 `/var/kerberos/krb5kdc/kadm5` 中为该用户创建一个条目。

5. 使用 `kadmin.local` 命令将你的每个系统管理员添加到 Kerberos 数据库。`kadmin.local` 命令是标准 `kadmin` 程序的 Kerberos 版本，它不会首先验证 Kerberos 数据库，因此用于启动 KDC 上的 Kerberos。以下示例为用户 `vwh` 添加了管理实例：
  ```
  # /usr/kerberos/sbin/kadmin.local

  kadmin.local: addprinc vwh/admin

  WARNING:: no policy specified for vwh/admin@VONHAGEN.ORG; defaulting to no policy

  Enter password for principal "vwh@VONHAGEN.ORG"

  Re-enter password for principal "vwh@VONHAGEN.ORG"

  Principal "vwh@VONHAGEN.ORG" created.
  ```

6. 为你刚刚创建的 principal 的非管理版本添加一个标准用户实体，并退出 `kadmin.local` 工具，如下例所示。添加标准 principal 可以启用通过关联实体的默认认证。你最终需要为每个想要使用 Kerberos 进行身份验证的用户创建一个 principal。大多数站点通过编写脚本（在创建标准用户账户时创建 Kerberos principal）来实现。

# 870 第 34 章

```bash
kadmin.local: addprinc vwh

WARNING: no policy specified for vwh@VONHAGEN.ORG; defaulting to no policy

Enter password for principal "vwh@VONHAGEN.ORG"

Re-enter password for principal "vwh@VONHAGEN.ORG"

Principal "vwh@VONHAGEN.ORG" created.

kadmin.local: quit
```

7. 现在，好戏开始了！使用以下命令启动 Kerberos 相关服务：
  ```bash
  # /sbin/service krb5kdc start
  # /sbin/service admin start
  # /sbin/service krb524 start
  ```
  此时，你已经准备好安装并启动 Kerberos 客户端了，将见下一节。在进行任何操作之前，你应该使用 `klist` 命令显式地为之前创建的管理实体请求一个票据，以验证你的服务器可以处理票据。然后你可以使用 `klist` 命令验证其内容，并使用 `kdestroy` 命令将其销毁（以便清理）。下面的示例显示了这一序列：
  ```bash
  $ klist

  Password for vwh@VONHAGEN.ORG:

  $ klist

  Ticket cache: FILE=/tmp/krb5cc_0

  Default principal: vwh@VONHAGEN.ORG

  Valid starting Expires Service principal

  05/03/05 22:09:04 05/04/05 22:09:04 krbtgt/VONHAGEN.ORG /VONHAGEN.ORG

  Kerberos 4 ticket cache: /tmp/tkt0

  klist: You have no tickets cached

  $ kdestroy
  ```

## 启用 Kerberos 客户端和应用程序

将系统设置为 Kerberos 客户端非常简单：

1. 从 KDC 复制 `/etc/krb5.conf` 文件到客户端。
2. 启用一个示例应用程序。使用 `krb-telnet`（经典 telnet 程序的 Kerberos 感版本）作为测试应用程序。`krb-telnet` 服务器由你系统的 `inet` 守护进程管理。要启用 `krb-telnet`，请修改 `/etc/xinetd.d/krb-telnet` 文件，将 `disable` 项从 `yes` 改为 `no`，如下例所示：
  ```bash
  # default: off
  # description: The Kerberized telnet server accepts normal telnet
  ```
