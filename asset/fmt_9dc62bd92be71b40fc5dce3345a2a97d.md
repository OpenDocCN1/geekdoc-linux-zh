
如果没有列出 `--update` 选项，设置将不会更新。如果改用 `--test`，设置将不会更新，但会在摘要报告中显示列出的更改。`--test` 选项也可以单独在不带任何其他选项的情况下使用，以显示当前的认证设置。如果改用 `-probe`，将通过 DNS 和其他服务对网络进行系统配置探测。如果找到任何信息，将将其显示。如果没有找到，则不显示任何信息。

如果启用某服务，请确保使用 `-ldapserver=<server>` 和 `ldbasedn=<dn>` 指定其所需的设置。命令行版本旨在是非非交互式的，如果你没有为服务提供必要信息，将会出现错误消息或警告。该服务将不会启用或启动。在依赖脚本或 kickstart 文件中的命令工作之前，请务必测试所有使用的命令。

## 表 12.3 authconfig 命令行选项

| 命令行选项 | 说明 |
| --- | --- |
| `-help` | 显示所有命令行选项和简要描述。 |
| `-enableshadow` | 启用影子密码（默认）。 |
| `-disableshadow` | 禁用影子密码。 |
| `-enablemd5` | 启用 MD5 密码（默认）。 |
| `-disablemd5` | 禁用 MD5 密码。 |
| `-enlenis` | 为用户信息启用 NIS。 |
| `-disableris` | 为用户信息禁用 NIS。 |
| `-nisdomain=<domain>` | 启用 NIS 时指定 NIS 域。 |
| `-nisserver=<server>` | 启用 NIS 时指定 NIS 服务器。 |
| `-enableldap` | 为用户信息提供 LDAP。 |
| `-disableldap` | 为用户信息禁用 LDAP。 |
| `-enableldapauth` | 为认证提供 LDAP。 |
| `-disableldapauth` | 禁用 LDAP 认证。 |
| `-ldapserver=<server>` | 启用 LDAP 时提供 LDAP 服务器。 |
| `-ldbasedn=<dn>` | 启用 LDAP 时提供 LDAP 基 DN。 |
| `-enableaptis` | 在 LDAP 中启用 TLS TLS。 |
| `-disableaptis` | 在 LDAP 中禁用 TLS。 |
| `-ldloadcacert=<url>` | 启用 LDAP 时从提供的 URL 加载 CA 证书。 |
| `-enablesmartcard` | 启用智能卡认证。 |
| `-disablesmartcard` | 禁用智能卡认证。 |
| `-enrequiresmartcard` | 要求智能卡认证。 |
| `-disrequiresmartcard` | 不要求智能卡认证。 |
| `-smartcardmodule=<module>` | 启用时指定要使用的智能卡模块。 |
| `-smartcardaction=<action>` | 设置移除智能卡时的动作。将 `<action>` 设置为 0 以锁定或设置为 1 以忽略。 |
| `-enablekerbs5` | 启用 Kerberos 认证。 |
| `-disablekerbs5` | 禁用 Kerberos 认证。 |
| `-krb5kdc=<server>` | 启用 Kerberos 认证时设置 Kerberos KDC。 |

## 表 12.3 续

| 命令行选项 | 说明 |
|--- |--- |
| `-krb5adminserver=<server>` | 启用 Kerberos 认证时设置 Kerberos 管理服务器。 |
| `-krb5realm=<realm>` | 启用 Kerberos 认证时设置 Kerberos 域。 |
| `-enablekrb5kcdns` | 启用使用 DNS 确定 Kerberos KDC。 |
| `-disablekrb5kcdns` | 禁用使用 DNS 确定 Kerberos KDC。 |
| `-enablekrb5kcdns` | 启用使用 DNS 确定 Kerberos KDC。 |
| `-disablekrb5kcdns` | 禁用使用 DNS 确定 Kerberos KDC。 |
| `-enablekrb5kcdns` | 启用使用 DNS 确定 Kerberos KDC。 |
| `-disablekrb5kcdns` | 禁用使用 DNS 确定 Kerberos KDC。 |
| `-enablesmb` | 启用 Samba 认证。 |
| `-disablesmb` | 禁用 Samba 认证。 |
| `-smservers=<servers>` | 启用 Samba 时设置服务器。 |
| `-smbworkgroup=<workgroup>` | 启用 Samba 时设置工作组。 |
| `-enablewinbind` | 为用户信息启用 Winbind。 |
| `-disablewinbind` | 为用户信息禁用 Winbind。 |
| `-enablewinbindauth` | 为认证启用 Winbind。 |
| `-disablewinbindauth` | 禁用 Winbind 认证。 |
| `-smsecurity=<mode>` | 为 Winbind 设置安全模式。必须是 user, server, domain, 或 ads 之一。 |
| `-smrealm=<realm>` | 当安全设置为 ads 时为 Winbind 设置域。 |
| `-smbidmapuid=<range>` | 当安全设置为 domain 或 ads 时，提供从最低到最高的 UID 范围分配给 Winbind。 |
| `-smbidmapgid=<range>` | 当安全设置为 domain 或 ads 时，提供从最低到最高的 GID 范围分配给 Winbind。 |
| `-winbindseparator=<char>` | 未启用 winbind 时，设置创建的用户名中域和用户部分的字符。 |
| `-winbindtemplatehomedir=<dir>` | 为 Winbind 创建的用户设置目录。例如 `/home/$U`。 |
| `-winbindtemplateprimarygroup=<group>` | 为 Winbind 创建的用户设置主组，例如 nobody 组。 |
| `-winbindtemplateshell=<shell>` | 为 Winbind 创建的用户设置登录 shell，例如 `/bin/false`。 |
| `-enablewinbindusedefaultdomain` | 启用 Winbind，没有域的用户是域用户。 |

# 第 13 章

### 本章内容

## 网络文件共享

- 网络文件系统 (NFS)
- Samba 文件共享

在企业计算环境中，在计算机之间共享文件，或允许多个用户访问中央服务器上的同一组文件，并让所有更改对所有用户立即可可见是常见操作。在纯 UNIX 环境中，包括仅由红帽企业文件系统 (NFS) 组成的环境。如果希望在红帽企业 Linux 和微软 Windows 系统之间共享文件，可以使用 Samba 来实现连接。

## 网络文件系统

NFS，或网络文件系统（Network File System），是一种用于在公共网络上的计算机之间共享文件的服务器-客户端协议。它适用于多种基于 UNIX 的操作系统，而不仅仅是 Linux。服务器和客户端不需要使用相同的操作系统。客户端系统只需要运行与 NFS 服务器 兼容的 NFS 客户端即可。

NFS 服务器向客户端系统导出一个或多个目录，客户端系统将一个或多个共享目录挂载到称为挂载点（mount points）的本地目录。挂载共享内容后，所有的 I/O 操作都会写回服务器，所有客户端都能感知到变化，就像这些变化发生在本地文件系统中一样。不需要手动刷新，因为客户端访问远程文件系统就像访问本地系统一样。访问通过客户端 IP 地址授予或限制。

NFS 的一个优势是客户端将远程文件系统挂载到目录，从而允许用户使用与访问本地文件相同的方法访问它。此外，由于访问是通过 IP 地址授予的，不需要用户名和密码。然而，存在安全风险需要考虑：NFS 服务器对客户端系统上的用户一无所知。来自 NFS 服务器的文件在挂载时保留其文件权限、用户 ID (UID) 和组 ID (GID)。如果客户端使用不同的用户和组 IDset，文件所有权将发生变化。

例如，如果一个文件在 NFS 服务器上由用户 ID 500 所有，则该文件以相同的用户 ID 导出到客户端。如果用户 ID 500 在 NFS 服务器上的映射 bsf 映射到远程客户端上的用户 akf，则用户 akf 将拥有远程客户端上的该文件。因此，NFS 服务器及其所有客户端使用相同的用户数据库至关重要，这样无论使用哪台机器访问文件，用户和组 ID 都是一致的。管理员可以在网络上分配用户和组 ID，但如果网络用户超过几位，这将是一项繁琐且耗时的任务。一种更出错且易于管理的方法是第 12 章“身份管理”中讨论的 NIS。

NFS 没有自己的日志文件。相反，NFS 使用的命令（如 `rpc.mount` 客户端请求）记录在系统日志文件 `/var/log/messages` 中。来自 nfsd 的内核消息也会记录在该文件中。

## NFS 和 SELINux

默认情况下，此策略通过将 `nfs_export_all_ro` 和 `nfs_export_all_rw` SELINux 布尔值设置为 1 来允许 NFS 连接到服务器。

如果你在使用 SELINux 的同时通过 NFS 共享主目录，必须在每个连接到提供主目录的 NFS 服务器的客户端上将 `use_nfs_home_dirs` 布尔值设置为 1。以 root 身份执行以下命令：
