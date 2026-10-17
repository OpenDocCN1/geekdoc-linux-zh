
| 选项 | 说明 |
| --- | --- |
| -c | 指定即使遇到错误，删除过程也将继续。 |
| -x | 指定 LDAP 目录用户使用简单身份验证，而不是使用 SASL。 |
| -D bindname | 使用区分名称 `binddn` 绑定到目录。 |
| -d debuglevel | 将调试信息级别指定为指定的 `debuglevel` 值。 |
| -f | 指定从指定的数据文件读取输入，而不是从标准输入。 |
| -W | 提示进行简单身份验证。 |
| -h ldapthost | 指定运行 LDAP 服务器的备用主机。 |
| -p ldapport | 指定 LDAP 服务器监听的备用端口。 |
| -r | 指定删除过程是递归的。如果指定的 DN 不是目录树（DIT）中的叶子节点，`ldapdelete` 工具将删除该 DN 及其层级，而无需提示用户。 |
| -l | 启用 SASL 交互模式。 |

例如，以下命令删除了 new-moon.com 中用户 peter 的条目：

```bash
ldapdelete -x -h 192.168.0.202 -D "cn=Manager,dc=newmoon,dc=com" -r "cn=peter,dc=newmoon,dc=com" -W
```

上述命令将产生以下结果：

输入 LDAP ：

# 搜索信息

在数据以组织的方式存储在 LDAP 目录之后，下一个任务是定义一种可以轻松检索信息的机制。要搜索 LDAP 目录中的信息，可以使用 `ldapsearch` 工具。`ldapsearch` 工具的语法如下：

```bash
ldapsearch [options] [search filter] [attributes list]
```

在上述语法中：

- `options`: 指定可以与 `ldapsearch` 命令配合使用的选项。
- `search filter`: 指定一个 LDAP 搜索过滤器来定义搜索标准。
- `attributes list`: 指定在搜索请求结果中返回的属性列表。

表 17-14 列出了可以用于 `ldapsearch` 工具过滤搜索的常用选项：

## 表 17-14 用于 ldapsearch 工具的选项

| 选项 | 说明 |
| --- | --- |
| -S attribute | 根据指定的属性对条目进行排序。默认情况下条目不进行排序。 |
| -d debuglevel | 将 LDAP 调试级别指定为属性 `debuglevel`。 |
| -f file | 从指定文件中读取行，并对每行执行 LDAP 搜索。 |
| -x | 指定使用简单身份验证模式而不是 SASL。 |
| -D binddn | 指定区分名称 `binddn` 以绑定到目录。 |
| -W | 提示进行简单身份验证。 |
| -b base | 指定搜索的基底。 |
| -s scope | 指定搜索范围（base, sub 或 onelevel）。 |
| -v version | 指定 LDAP 版本。 |
| -l attribute | 指定要返回的属性。 |
| -L | 以 LDIF 格式显示输出。 |

# 实现目录复制

有时目录的性能会下降。考虑一种情况：一个启用目录的应用程序使用目录服务器的程度极大，以至于客户端无法响应其他启用目录的应用程序和客户端请求。为了解决此类问题，你可以配置一个从属服务器作为主目录服务器的副本。

要创建 OpenLDAP 服务器的副本，你需要一个正在运行的 OpenLDAP 服务器。要复制服务器，你需要执行以下步骤：

- 1. 停止主 OpenLDAP 服务器的 `slapd` 守护进程。
- 2. 为了在从 OpenLDAP 服务器中启用复制，请编辑主 OpenLDAP 服务器的 `slapd.conf` 文件。
- 3. 将数据库文件从主 OpenLDAP 服务器复制到从 OpenLDAP 服务器。
- 4. 编辑从 OpenLDAP 服务器的 `slapd.conf` 文件。
- 5. 启动从 OpenLDAP 服务器的 `slapd` 守护进程。
- 6. 启动主 OpenLDAP 服务器的 `slapd` 守护进程。
- 7. 启动主 OpenLDAP 服务器的 `slurpd` 守护进程。

## 配置并准备主 OpenLDAP 服务器用于复制

在配置主 OpenLDAP 服务器进行复制之前，你需要停止主服务器的 `slapd` 守护进程。这是必要的，以便 `slapd.conf` 文件中的更改也能反映在目录服务器的配置设置中。

`slurpd` 是一个 OpenLDAP 复制守护进程，用于同步主服务器和从服务器的数据库。`slurpd` 守护进程通过读取主 OpenLDAP 服务器的复制日志文件并将更改传播到所有从服务器来同步 OpenLDAP 的数据库。如果从服务器宕机，`slurpd` 守护进程会定期尝试连接它以更新其数据库。以下步骤解释了主从服务器的 `slapd` 守护进程和 `slurpd` 守护进程如何协同工作以复制数据：

- 1. 一个 OpenLDAP 客户端启动并连接到从属 `slapd` 守护进程。
- 2. 连接到从属 `slapd` 守护进程后，OpenLDAP 客户端向从属 `slapd` 守护进程提交一个修改操作（modify operation）。
- 3. 从属 `slapd` 向 OpenLDAP 客户端返回一个引用（referral）以响应所请求的修改操作。
- 4. OpenLDAP 客户端使用该引用将修改操作发送给主 `slapd` 守护进程。
- 5. 主 `slapd` 守护进程执行修改操作，然后将更改写入其复制日志文件并向客户端返回成功代码。
- 6. 主服务器的 `slurpd` 进程注意到复制日志文件中追加了一个新条目，读取复制日志条目，并将更改发送给从属 `slapd`。
- 7. 从属 `slapd` 执行修改操作并向 `slurpd` 进程返回成功代码。

如果 OpenLDAP 客户端最初就帮助连接到了主 `slapd`，那么客户端不需要向从属 `slapd` 守护进程发送请求。客户端直接从主服务器获取成功代码。

要配置主服务器记录更改，你需要在 `slapd.conf` 文件的数据库部分添加以下两个指令：

- `replogfile`
- `replica`

### replogfile 指令

`replogfile` 指令用于指定 `slurpd` 守护进程记录更改的日志文件名。

要指定日志文件名，请编辑 `slapd.conf` 文件，如下所示：

```conf
## 指定日志文件的位置
replogfile /var/ldap/slapd.replog
```

在前面的代码中，`/var/ldap/slapd.replog` 代表记录主服务器数据库中执行的所有更改的文件。主服务器使用 `/var/ldap/slapd.replog` 文件将主服务器上执行的更改发送到从属 `slapd` 守护进程。如果 `replogfile` 指令未取消注释，ldap 服务将自动激活 `slurpd` 守护进程。

### replica 指令

`replica` 指令用于指定接收更改的从服务器的详情。

你可以使用 `replica` 指令指定以下配置参数：

- `host`: 指定副本的主机名。
- `port number`: 指定副本的端口号。
- `suffix`: 指定要复制的分区。
- `binddn`: 指定副本 OpenLDAP 服务器的绑定 DN。你需要确保 `binddn` 参数的值具有对副本 OpenLDAP 服务器的写权限。

#### 红 Hat Linux-- 学习指南

- `credentials`: 指定向副本发送更改所需的凭据信息。使用 `credential` 参数指定密码，用于用于到从服务器的简单绑定（simple binds）或 SASL 绑定。你可以指定 `simple` 和 `SASL` 作为 `bindmethod` 参数的值。
- `bindmethod`: 指定将主 OpenLDAP 服务器绑定到副本的绑定方法。
- `tls`: 指定是否启用了传输层安全（TLS）协议以进行安全复制。

要指定从服务器的详情，请编辑 `slapd.conf` 文件，如下所示：

```conf
## 在主 LDAP 服务器中指定 replica 参数
replica
host=192.168.0.205:389
binddn=cn=replica,dc=newmaine,dc=com
bindmethod=simple credentials=password
```

前面的代码指定了副本的主机名以及向从服务器发送更改所需的绑定信息。

## 配置并准备从属 OpenLDAP 服务器用于复制

在配置好主 OpenLDAP 服务器后，你需要配置从服务器。要配置从服务器进行复制，你需要执行以下任务：

- 初始化从服务器
- 编辑从服务器的 `slapd.conf` 文件

### 初始化副本的数据库
