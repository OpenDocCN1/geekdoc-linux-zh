
# 配置 OpenLDAP

根据你想对目录进行的操作，配置目录服务器可能非常痛苦，也可能是一个简单的过程。如果你在全新的部署上工作，不需要担心遗留问题或现有用户，设置目录通常很容易。对于具有现有基础设施的环境，必须采取额外的预防措施。

> 警告：如果你在需要担心后兼容性、遗留架构、现有用户或现有数据的环境中部署 LDAP，建议谨慎对待 OpenLDAP 的推出。在某些情况下，这需要几个月的规划。规划应包括在测试系统中进行大量的测试和实际模拟。

## pam_ldap 和 nss_ldap 模块

`pam_ldap` 模块为 Linux/Unix 主机提供了针对 LDAP 目录进行身份验证的方法。该模块由 PADL 软件公司开发。它允许 PAM 感知应用程序使用存储在 LDAP 目录中的信息对用户进行身份验证。PAM 感知应用程序的示例包括登录程序、某些邮件服务器、文件传输协议 `FTP` 服务器、`OpenSSH` 和 `Samba`。
`nss_ldap` 模块是一组 C 库扩展，允许应用程序通过查询 LDAP 目录来查找用户、组、主机和其他信息。该模块允许应用程序使用 LDAP 以及使用传统方法（如平面文件或 NIS）查找信息。该模块也由 PADL 软件公司开发。
在 Fedora 系统、`RHEL` 和 `CentOS` 上，这些模块由 `nss_*.rpm` 包提供。在需要用 LDAP 替代传统身份验证机制的系统上，需要这些模块。

首先，通过输入以下命令检查该包是否已经安装：

```
[root@fedora-server ~]# rpm -q nss_ldap

nss_ldap-*
```

如果你发现该包尚未安装，可以使用 `yum` 命令快速安装它：

```
[root@fedora-server ~]# yum -y install nss_ldap
```

配置 LDAP 目录服务时，另一个需要考虑的重要因素是目录的结构。例如，在继续之前，你应该对这些问题有所答案：

- 你的机构中有哪些组织部门？
- 结构将根据哪些边界进行构建？
- 你想要存储在目录中的信息敏感程度如何？
- 是否需要一个或多个 LDAP 服务器？

## 配置 slapd

`slapd.conf` 文件是 `slapd` 守护进程的配置文件。在 Fedora 和类 RedHat 发行版中，该文件的完整路径为 `/etc/ldap/slapd.conf`。在本节中，我们将剖析 Fedora 系统自带的默认配置文件，并讨论其中一些有趣的要点。请注意，其余的大部分讨论将将在 Fedora 发行版上继续。

> 在类 Debian 发行版中，`slapd` 的配置文件位于 `/etc/ldap/slapd.conf`。

以下是 `slapd.conf` 文件的截断版本。请注意，原始文件中的大多数注释条目已被删除，还有我们在此不想处理的一些其他配置指令。仅显示了与我们当前配置相关的精简版文件。每行开头都添加了行号以便阅读。

```
1) # 选项选项的详细信息请参阅 slapd.conf(5)。

2) # 此文件不应对世界可读。

3) #

4) include /etc/ldap/schema/core.schema

5) include /etc/ldap/schema/cosine.schema

6) include /etc/ldap/schema/inetorgperson.schema

7) include /etc/ldap/schema/nis.schema

8) #

9) pidfile /var/run/openldap/slapd.pid

10) argsfile /var/run/openldap/slapd.argsfile

11) database bdb

12) suffix "dc=my-domain,dc=com"

13) rootdn "cn=Manager,dc=my-domain,dc=com"

14) # 明文密码，特别是对于 rootdn

15) # 应避免。详细信息请参阅 slappwd(8) 和 slapd.conf(5)。

17) rootpw {crypt}jFYNSCNctByG

18) #

19) # 在运行 slapd 之前，数据库目录必须存在，且

20) # 应该只能被 slapd 和 slapap 工具访问。

21) # 建议模式为 700。

22) directory /var/lib/ldap
```

根据上述列表：

- 第 1–3 行是注释条目。井号 `#` 之后的任何文本都是注释。
- 第 4–7 行是 `include` 语句。`include` 语句用于指示 `slapd` 从指定的文件读取额外的配置信息。在这种情况下，引入的额外文件是存储在 `/etc/openldap/schema/` 目录下的指定 OpenLDAP schema。至少必须存在 `core.schema` 文件。
- 在第 9 行中，`pidfile` 指令指向存放 `slapd` 进程 ID 的文件路径。
- 在第 10 行中，`argsfile` 指令用于指定文件路径，该文件可存储运行 `slapd` 的命令行选项。
- 在第 11 行中，`database` 选项标记了一个新数据库实例定义的开始。该选项的值取决于用于存储数据库的后端。在示例 `slapd.conf` 文件中，使用 `bdb` `Berkeley DB` 作为数据库类型。其他支持的后端类型包括 `ldbm`、`sql`、`tcl` 和 `meta`。表 26-2 描述了一些数据库后端。
- 在第 12 行中，`suffix` 指令定义了传递给此特定端的查询的 DN 后缀。它定义了 LDAP 服务器提供信息或对 LDAP 服务器具有权威性的域。此条目应被更改以反映你机构的命名结构。
- 在第 13 行中，`rootdn` 指令定义了 LDAP 目录超级用户的 DN。该用户对于 LDAP 目录而言，就像 UNIX/Linux root 用户对于 Linux 系统一样。此处指定的用户在对相关数据库的操作上不受任何访问控制或管理限制。此处指定的 DN 不需要存在于目录中。
- 在第 17 行中，`rootpw` 指令指定了 `rootdn` 所指定 DN 的密码。不用说，这里应该使用非常强/良好的密码。密码可以用明文指定，非常非常糟糕的主意，也可以指定密码的哈希值。可以使用 `slappwd` 程序生成密码哈希。
- 最后，在第 22 行中，`directory` 指令指定包含数据库和关联索引的 BDB 文件的路径。

在浏览 `slapd.conf` 文件中的几个重要指令后，我们现在对文件进行几处更改，以为我们的环境进行定制：

1. 当以 root 身份登录系统时，切换到 OpenLDAP 的工作目录：

```
[root@fedora-server ~]# cd /etc/openldap/
```

| 数据库后端类型 | 描述 |
| :--- | :--- |
| bdb | BDB 数据库。 |
| ldbm | Ldbm 数据库。 |
| sql | SQL 数据库。 |
| tcl | Tcl 数据库。 |
| meta | 元数据库。 |

2. 备份 `slapd.conf` 文件，以便在需要时可以恢复：

```
[root@fedora-server ~]# cp slapd.conf slapd.conf.bak
```

3. 清空 `slapd.d` 目录内容：

```
[root@fedora-server ~]# rm -rf /etc/openldap/slapd.d/*
```

4. 创建一个新的软链接：

```
[root@fedora-server ~]# mkdir /etc/openldap/slapd.d

[root@fedora-server ~]# ln -s /etc/openldap /etc/openldap/slapd.d
```

5. 编辑 `slapd.conf` 并修改配置：

```
[root@fedora-server ~]# vi /etc/openldap/slapd.conf
```

6. 确保目录的权限正确：

```bash
[root@fedora-server ~]# chmod -R 700 /etc/openldap/slapd.d
```

7. 检查配置是否正确：

```
[root@fedora-server ~]# slapd -t
```

8. 启动 `slapd` 守护进程：

```
[root@fedora-server ~]# slapd -D
```

9. 停止 `slapd` 守护进程：

```
[root@fedora-server ~]# killall slapd
```
