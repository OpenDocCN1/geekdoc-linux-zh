
- 第 11 行 `database` 选项标记新数据库定义的开始。该选项的值取决于用于存储数据库的后端。在我们的示例 `slapd.conf` 中，使用 `bdb` (Berkeley DB) 作为数据库类型。其他支持的后端类型有 `dbm`、`sql`、`tcl` 和 `meta`。某些数据库后端在表 25-2 中描述。

- 第12 行 `suffix` 指令指定传递给特定后端的查询 DN。它定义了 LDAP 服务器提供信息或作为权威机构的域。此条目应反映你组织的命名结构。

- 第 13 行 `rootdn` 指令指定 LDAP 目录超级用户的 DN。该用户对于 LDAP 目录而言，正如 UNIX/Linux root 用户之于 Linux 系统。此处指定的用户在对数据库的操作上不受任何访问控制或管理限制。此处指定的 DN 在目录中不存在。

- 第 17 行 `rootpw` 指令指定 `rootdn` 指令所指定 DN 的密码。不用说，这里应该使用非常强/良好的密码。密码可以用明文形式指定（非常非常糟糕的主意），也可以指定密码的哈值。`slapppasswd` 程序可以生成密码哈值。

- 最后，第 22 行 `directory` 指令指定数据库文件及关联索引的路径。

在浏览了 `slapd.conf` 中的几个重要指令后，我们现在将进行一些更改以适应你的环境：

1. 以 root 身份登录系统时，切换到 OpenLDAP 的工作目录。输入：

```bash
[root@serverA ~]# cd /etc/openldap/
```

| 数据库后端 | 说明 |
| :--- | :--- |
| bdb | Berkeley DB 实例定义。这是推荐的后端类型。它使用 Berkeley DB 存储数据。 |
| ldbm | LDAP 类型。配置简单但不如 bdb 后端持久。它使用 Berkeley、GNU DB 和 MDB 存储数据。 |
| sql | 使用 SQL 数据库存储数据。 |
| ldap | 用于将请求转发到另一个 LDAP 服务器。 |
| meta | 元目录后端。它是 LDAP 类型的改进。它通过一组远程 LDAP 服务器执行代理操作。 |
| monitor | 存储 slapd 守护进程的状态。 |
| null | 对此数据库类型的操作但不执行任何操作。这相当于在 Linux/Unix 中向 /dev/null 发送。 |
| passwd | 使用系统的明文 /etc/passwd 文件提供用户帐户信息。 |
| tcl | 一个使用嵌入 slapd 的 Tcl 解释器的实验性后端。 |
| perl | 使用嵌入 slapd 的 Perl 解释器。 |

**表 25-2.** OpenLDAP 数据库后端

2. 通过重命名对现有的 `slapd.conf` 文件进行备份。这样在出错时你可以始终恢复到它。

```bash
[root@serverA openldap]# mv slapd.conf slapd.conf.original
```

3. 使用文本编辑器创建一个新的 `/etc/openldap/slapd.conf` 文件，内容如下文：

```config
include /etc/ldap/schema/core.schema
include /etc/ldap/schema/cosine.schema
include /etc/ldap/schema/inetorgperson.schema
include /etc/ldap/schema/nis.schema
pidfile /var/run/openldap/slapd.pid
```

580 Linux 系统管理：初学者指南

```
argssfile      /var/run/openldap/slapd.args
database        bdb
suffix         "cn=example,dc=org"
rootdn          "cn=Manager,dc=example,dc=org"
#n# 下方的哈希密码是使用命令生成的：
# "slapppasswd -s test"。运行该命令并将输出粘贴在此处。
rootwp [SHA]gJeYeBdBxcI1-bfgMpmvFFVJqdG5CjdP
directory      /var/lib/ldap
```

4. 保存对文件的更改并退出编辑器。

# 启动和停止 slapd

在设置好 slapd 的配置文件后，下一步将启动守护进程。在 Fedora 系统上启动它非常简单。首先，我们使用使用 `service` 命令来检查守护进程的状态。

```bash
[root@serverA ~]# service ldap status
slapd is stopped
```

示例输出显示该守护进程目前没有运行。使用此命令启动它：

```bash
[root@serverA openldap]# service ldap start
```

如果你发现 LDAP 服务已经在运行，可以改用 `service` 命令并使用 `restart` 选项，如下：

```bash
[root@serverA ~]# service ldap restart
```

> 提示：如果你在类 Red Hat 发行版（如 Fedora）上启动 slapd 服务时，收到关于 /var/lib/ldap 目录下不存在 DB_CONFIG 的警告信息，可以使用发行版附带的示例 DB_CONFIG 文件来修复此问题。该示例文件存储在 /etc/openldap/ 之下，复制并重命名该文件的命令为：

```bash
[root@serverA ~]# cp /etc/openldap/DB_CONFIG.example /var/lib/ldap/DB_CONFIG
```

> 提示：注意 OpenLDAP 配置文件的权限。例如，在 Fedora 或 RHEL 系统上，如果 "ldap" 用户无法读取 slapd.conf 文件，slapd 守护进程将拒绝启动。此外，数据库目录（/var/lib/ldap）的内容必须由用户 "ldap" 所有，以避免奇怪的错误。

如果你希望 slapd 服务在下次系统重启时自动启动，请输入

```bash
[root@serverA openldap]# chconfig ldap on
```

第 25 章：LDAP 581

# 配置 OpenLDAP 客户端

在 LDAP 世界中，客户端的概念需要一些时间来适应。几乎任何资源或进程都可以是 LDAP 客户端。幸运或不幸的是，每组客户端都有其特定的配置文件。OpenLDAP 客户端的配置文件通常命名为 `ldap.conf`，但根据客户端的具体问题，它们存储在不同的目录中。

OpenLDAP 客户端配置文件的两个常见位置是 `/etc/openldap/` 目录和 `/etc` 目录。使用 OpenLDAP 库（由 `openldap*.rpm` 包提供）的客户端程序——如 `ldapadd`、`ldapsearch`、Sendmail 和 Evolution——会使用 `/etc/openldap/ldap.conf` 文件（如果该文件存在）。`ns_ldap` 库则使用 `/etc/ldap.conf` 作为配置文件。

在本节中，我们将为 OpenLDAP 客户端工具设置配置文件。该配置文件非常直观；我们只需要更改其中的一个指令即可。

用任何文本编辑器打开 `/etc/openldap/ldap.conf` 文件，并更改列表中的这一行

```
# BASE dc=example, dc=com
```

修改如下所示

```
BASE dc=example, dc=org
```

> 提示：如果你从服务器以外的主机使用客户端工具，在 /etc/openldap/ldap.conf 文件中你可能想要更改的特定变量/指令是 `HOST` 指令。它应该设置为远程 LDAP 服务器的 IP 地址。但由于我们直接在 LDAP 服务器本身上使用 LDAP 客户端，我们将 HOST 指令留在了默认值 `HOST 127.0.0.1`。

# 创建目录目

LDAP 数据交换格式 (LDIF) 用于以文本格式表示 LDAP 目录中的条目。如前，LDAP 中的数据以这种格式呈现和交换。LDIF 文件中的数据可以操作、添加、删除和更改存储在 LDAP 目录中的信息。条目的格式为：

```
dn: <distinguished name>
<attribute_description>: <attribute_value>
<attribute_description>: <attribute_value>
dn: <yet another distinguished name>
<attribute_description>: <attribute_value>
<attribute_description>: <attribute_value>
...
```

Linux 系统管理：初学者指南

LDIF 文件的格式略为严格。你应该记住以下几点：

- 同一个 LDIF 文件中的多个条目由空行隔开。
