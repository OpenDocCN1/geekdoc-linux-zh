

# 第 13 章 轻量级目录访问协议 (LDAP)

系统将提示你输入并重新输入密码，程序会将生成的加密密码打印到终端。

接下来，将新创建的密码复制到 `/etc/openldap/slapd.conf` 的其中一个 `rootpw` 行中，并移除哈希符号 (#)。

完成后，该行看起来应该类似于下面的示例：

```
rootpw {SSH}vv2y+i6V6esasazIv70SSnNAJE18bb2u
```

# 警告

LDAP 密码（包括 `/etc/openldap/slapd.conf` 中的 `rootpw` 指令）将以未加密的形式在网络上传输，除非你启用了 TLS 加密。

如要启用 TLS 加密，请查看 `/etc/openldap/slapd.conf` 中的注释并参考 `slapd.conf` 的帮助页。

为了增加安全性，在填充 LDAP 目录后，应通过替换哈希符号 (#) 来注释 `rootpw` 指令。

在本地使用 `/usr/sbin/slappadd` 命令行工具填充 LDAP 目录时，不需要使用 `rootpw` 指令。

# 重要

你必须是 root 用户才能使用 `/usr/sbin/slappadd`。然而，目录服务器是以 `ldap` 用户身份运行的。因此，目录服务器将无法修改由 slappadd 创建的任何文件。要解决此问题，在使用 slappadd 后，请输入以下命令：

```
chown -R ldap /var/lib/ldap
```

# 13.7. 配置系统使用 OpenLDAP 进行验证

本节简要介绍了如何配置 Red Linux 系统使用 OpenLDAP 进行验证。除非你是 OpenLDAP 专家，否则你可能需要比这里更多的文档。更多信息请参考第 13.9 节“附加资源”。

### 安装必要的 LDAP 包

首先，你应该确保在 LDAP 服务器和 LDAP 客户端机器上安装了相应的软件包。LDAP 服务器需要 `openldap-servers` 包。

所有 LDAP 客户端机器都需要安装 `openldap`、`openldap-clients` 和 `nss_ldap` 包。

### 编辑配置文件

- 在服务器上，编辑 LDAP 服务器上的 `/etc/openldap/slapd.conf` 文件，以确保它符合你组织的特定要求。有关编辑 slapd.conf 的说明，请参考第 13.6.1 节“编辑 /etc/openldap/slapd.conf”。
- 在客户端机器上，`/etc/openldap/ldap.conf` 和其他文件都需要包含你组织的正确服务器和搜索基信息。
执行此操作的最简单的方法是运行身份配置工具 (authconfig-gtk)，并在“User Information”选项卡下选择“LDAP Support”。
你也可以手动编辑这些文件。
- 在客户端机器上，必须编辑 `/etc/nsswitch.conf` 以使用 LDAP。
执行此操作最简单的方法是运行身份配置工具 (authconfig-gtk)，并在“User Information”选项卡下选择“LDAP Support”。
如果手动编辑 `/etc/nsswitch.conf`，在相应的行中添加 `ldap`。

例如：
password: files ldap
shadow: files ldap
group: files ldap

# 13.7.1. PAM 和 LDAP

要让启用 PAM 的应用程序使用 LDAP 进行验证，请运行身份配置工具 (authconfig-gtk)，并在“Authentication”选项卡下选择“LDAP Support”。有关更多配置 PAM 的信息，请参阅第 14 章“可插认证模块 (PAM)”以及 PAM 的帮助页。

# 13.7.2. 将旧身份信息迁移到 LDAP 格式

`/usr/share/openldap/migration/` 目录包含一组 shell 和 Perl 脚本，用于将信息迁移到 LDAP 格式。

首先，修改 `common.conf` 文件以反映你的域名。默认 DNS 域名应从默认值更改为类似的内容：

```
$DEFAULT_MAIL_DOMAIN = "your_company";
```

默认基准 (base) 也应更改为类似的内容：

```
$DEFAULT_BASE = "dc=your_company, dc=com";
```

将用户数据库迁移为 LDAP 可读格式的任务由安装在同一目录下的迁移脚本完成。参考表 13-1，决定运行哪个脚本来迁移你的用户数据库。

| 现有名称服务 | LDAP 是否运行？ | 使用的脚本 |
|---|---|---|
| /etc file files | yes | migrate_all_online.sh |
| /etc file files | no | migrate_all_offline.sh |
| NetInfo | yes | migrate_all_netinfo_online.sh |
| NetInfo | no | migrate_all_netinfo_offline.sh |
| NIS (YP) | yes | migrate_all_nis_online.sh |
| NIS (YP) | no | migrate_all_nis_offline.sh |

表 13-1. LDAP 迁移脚本

根据你现有的名称服务运行相应的脚本。

> 注意
> 你必须在系统中安装 Perl 才能使用其中一些脚本。

`/usr/share/openldap/migration/` 中的 `README` 和 `migration-tools.txt` 文件提供了有关如何迁移信息的详细信息。

# 13.8. 升级到 OpenLDAP 2.0 版本

在 OpenLDAP 2.0 中，`ldap` LDAP 服务器使用的磁盘存储格式已发生变化。如果你正从 Red Linux 7.0 或更早版本升级 LDAP，你需要使用以下命令提取目录并将将其导入 LDIF 文件：

```
ldbmcat -n > <ldif_file>
```

在上述命令中，将 `<ldif_file>` 更改为输出文件名。接下来输入以下命令将此文件导入 OpenLDAP 2.0：

```
slappadd -l <ldif_file>
```

> 重要
> 你必须是 root 用户才能使用 `/usr/sbin/slappadd`。然而，目录服务器是以 `ldap` 用户身份运行的。因此，目录服务器将无法修改由 `slappadd` 创建的任何文件。要解决此问题，在使用 slappadd 后，请输入以下命令：

```
chown -R ldap /var/lib/ldap
```

# 13.9. 其他资源

有更多关于 LDAP 的信息。在系统上配置 LDAP 之前，请查看这些资源，特别是 OpenLDAP 网站和 LDAP HOWTO。

# 13.9.1. 已安装文档

- LDAP 帮助页 — `ldap` 页面提供了对 LDAP 的良好介绍。各种守护进程和工具也有相应的帮助页。
- `/usr/share/docs/openldap-<versionnumber>` 包含通用的 README 文档和杂信息。

# 13.9.2. 有用网站

- http://www.ldap.org/ OpenLDAP 项目主页。该网站包含了大量关于配置 OpenLDAP 的信息。
- http://www.redhat.com/mirrors/LDAP/HOWTO/LDAP-HOWTO.html 一个较旧但仍有价值的 LDAP HOWTO。
- http://www.padl.com/ nss_ldap 和 pam_ldap 等其他有用 LDAP 工具的开发者。
- http://www.kingsmountain.com/ldapRoad.shtml Jeff Hodges 的 LDAP Map 链接了关于 LDAP 协议的多个常用问题解答和最新动态。
- http://www.webtechniques.com/archives/2000/05/wilcox 关于在 LDAP 中管理组的有用视角。
- http://www.ldapman.org/articles 提供了对 LDAP 的良好介绍的文章，包括设计目录树和自定义目录结构的方法。

# 13.9.3. 相关书籍

- *Implementing LDAP*，作者 Mark Wilcox；Wrox Press, Inc.
- *Understanding and Deploying LDAP Directory Services*，作者 Tim Howes 等；Macmillan Technical Publishing

# III. 安全参考

使用安全协议是维护系统完整性的关键部分。本部分描述了用于用户验证、网络访问控制、安全网络通信和入侵检测的关键工具。有关加固 Red Hat Linux 系统的更多信息，请参考《Red Hat Linux 安全指南》。

# 目录

+ 14. 可插认证模块 (PAM) ................................................................ 197
+ 15. TCP Wrappers 和 xinetd.................................................................. 205
+ 16. iptables............................................................................................... 219
+ 17. Kerberos........................................................................................................ 229
+ 18. SSH 协议.............................................................................................. 237
+ 19. Tripwire...................................................................................................... 245

