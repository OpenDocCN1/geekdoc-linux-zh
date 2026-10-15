
```
--nisserver=<server>               默认 NIS 服务器
--enableldap                       默认启用用于用户信息的 LDAP
--disableldap                       默认禁用用于用户信息的 LDAP
--enabledldapauth                   默认启用用于认证的 LDAP
--disableldapauth                   默认禁用用于认证的 LDAP
--ldapserver=<server>               默认 LDAP 服务器主机名或 URI
--ldapbasedn=<dn>                   默认 LDAP 基准 DN (base DN)
--enabledldapstarttls, --enableldapstarttls  启用在 LDAP 中使用 TLS (RFC-2830)
--disableldapstarttls, --disableldapstarttls  禁用在 LDAP 中使用 TLS (RFC-2830)
--enablerfc2307bis                  启用使用 RFC-2307bis 架构进行 LDAP 查找
--disablerfc2307bis                  禁用使用 RFC-2307bis 架构进行 LDAP 查找
--ldapoadcacert=<URL>                从 URL 载入 CA 证书
--enablesmartcard                    默认启用智能卡认证
--disablesmartcard                   默认禁用智能卡认证
--enablerequiresmartcard            默认认证时需要智能卡
--disablereiresmartcard             默认认证时不需要智能卡
--smartcardmodule=<module>          默认使用的智能卡模块
--smartcardaction=0<Lock|1|ignore>   拔出智能卡时要采取的操作
--enablefingerprint                 默认启用使用指纹识别器认证
--disablefingerprint                默认禁用使用指纹识别器认证
--enableecrypts                     启用自动每用户 eecrypts
--disableecrypts                     禁用自动每用户 eecrypts
--enablekerb5                        默认启用 kerberos 认证
--disablekerb5                       默认禁用 kerberos 认证
--krb5kdc=<server>                   默认 kerberos KDC
--krb5adminserver=<server>          默认 kerberos 管理服务器
```

## 第 25 章：配置外部认证与授权

| | |
|---|---|
| `--krb5realm=` | 默认 kerberos 领域 (realm) |
| `--enablekrb5kcdns` | 启用使用 DNS 查找 kerberos KDCs |
| `--disablekrb5kcdns` | 禁用使用 DNS 查找 kerberos KDCs |
| `--enablekrb5mdns` | 启用使用 DNS 查找 kerberos 领域 |

在使用这些工具之一时，会涉及到多个配置文件。了解这些文件的名称对于排查故障非常有帮助：

- `/etc/ldap.conf`：包含 LDAP 客户端的配置。需要此文件来识别应该使用哪个 LDAP 服务器。
- `/etc/krb5.conf`：包含 Kerberos 特有的信息。
- `/etc/sssd/sssd.conf`：包含系统安全守护进程 (`sssd`) 使用的信息。该守护进程在大多数配置中用于检索和缓存用户信息以及认证信息。
- `/etc/nscd.conf`：根据你服务器上安装的软件包，`nslcd` 服务可能用于检索和缓存用户信息，作为 `sssd.conf` 配置文件的替代方案。这不是一个默认配置，但在某些情况下可以使用。

> **提示** Red Hat 在之前的 RHEL 版本中花费了大量精力整合 `sssd` 服务，目前看起来也是如此。在第 6 章“用户和组管理”中，你可以阅读到如何配置服务器以针对使用 LDAP 密码的 LDAP 服务器进行认证。

- `/etc/nsswitch.conf`：指明通过哪些服务获取信息。它包含如 `passwd: sss` 的行，表示先使用本地文件，然后使用 sss。
- `/etc/pam.d/`：包含定义如何处理各种服务的配置文件。
- `/etc/openldap/cacerts`：存储用于验证 SSL 证书的根证书。
- `/etc/sysconfig/authconfig`：包含指定 `authconfig` 如何工作的变量。

## 使用 nsld 或 sssd 作为后端

取决于你使用的工具，结果可能会有所不同。如果你在开始配置认证之前安装了 `sssd` 软件包，则使用 `sssd` 作为认证后端。在其他情况下，可能会发现是 `nsld` 服务在处理认证。在第 6 章中，你学习了如何使用这两个后端服务来配置外部认证。

Red Hat 在 RHEL 中包含了 `sssd` 服务来处理认证。因此，当你配置认证时，必须确保安装了 `sssd` 软件包，以便所有工作都由 `sssd` 处理。为了强制使用 `sssd`，这里有一些额外的提示：

- 在最小化安装的 RHEL 中，由 `sssd` 管理的软件包是不可用的。在使用 `authconfig` 工具之前，请确保至少安装了 `sssd` 软件包。
- 为了避免问题，使用带有图形用户界面 (GUI) 的服务器是一个好主意（你可以从 http://www.rhatcert.com 下载免费的测试环境）。该配置默认使用 `sssd`。
- 在使用 `authconfig` 工具之前，确保已安装 `sssd` 软件包。
- 在使用 `authconfig` 之前，确保 `sssd` 服务正在运行。
- 如果使用 `authconfig`，先设置不带 Kerberos 授权的 LDAP 认证，然后打开工具根据需要配置 Kerberos。

## 第 25 章：配置外部认证与授权 569

## 设置外部认证

要设置外部认证，你可以使用 `authconfig-tui` 或 `authconfig-gtk` 工具。在本节中，你将学习如何使用 `authconfig-tui` 创建配置。练习 25.1 将引导你完成设置配置涉及的不同部分。

## 练习 25.1 设置外部认证

在此练习中，你将为 `labiba.example` 服务器上的 `server1` 配置外部认证。此练习假设你正在使用附录 D“设置身份管理”中描述的 `labiba` 服务器，或者你正在使用从 http://www.rhcert.com 下载的 `labiba` 虚拟机 (VM)。此练习中的所有步骤均在 `server1` 上执行。

- 1. 使用 `ping labiba.example.com` 验证你是否可以通过名称访问 `labiba.example.com` 服务器。如果不通，请在继续之前进行修复：在 DNS 中添加将 `labiba.example.com` 解析到其主机名的条目，或者使用通过 `labiba` 服务器提供的 DNS 服务器。
- 2. 输入 `yum install -y sssd sssd-tools sss-pam-cacerts`。
- 3. 输入 `mkdir /etc/openldap/cacerts`。
- 4. 使用 `scp labiba.example.com:/root/cacert.p12 /etc/openldap/cacerts` 将证书从 IPA 服务器复制到本地服务器。
- 5. 输入 `vim /etc/sysconfig/authconfig`。确保该文件包含以下配置选项：

```
USESSDAUTH=yes

USESSSD=yes

FORCELEGACY=no
```
