
## 30.4.4.1. 初始化 NIS 映射

NIS 映射是从 NIS 主服务器上 `/etc/yp` 中的配置文件生成的，其中有一个例外：`/etc/master.passwd`。这是为了防止密码传播到 NIS 域中的所有服务器。因此，在初始化 NIS 映射之前，请配置主密码文件：

```
# cp /etc/master.passwd /var/yp/master.passwd
# cd /var/yp
# vi master.passwd
```

建议同时删除所有系统账户条目，以及任何不需要传播到 NIS 客户端的用户账户，例如 `root` 和任何其他管理员账户。

**注意**

请确保 `/var/yp/master.passwd` 既不是组可读也不是世界可读的，将其权限设置为 `600`。

完成此任务后，初始化 NIS 映射。FreeBSD 包含了执行此操作的 `ypinit(8)` 脚本。在为主服务器生成映射时，包含 `-m` 并指定 NIS 域名：

```
ellington# ypinit -m test-domain
```

`Server Type: MASTER Domain: test-domain`

创建 YP 服务器将需要你回答几个问题。所有问题将在过程开始时询问。

你希望此过程在遇到非致命错误时退出吗？[y/n: n] n

好的，请记住返回并手动重做任何失败的操作。否则，某些功能可能无法工作。

此时，我们必须构建一个这些域 YP 服务器的列表。

`rod.darktech.org` 已知为主服务器。

请继续添加任何从服务器，每行一个。完成列表后，输入 `<control D>`。

`master server : ington`

`next host to add: ^D`

当前的 NIS 服务器列表所示：

`ellington`

`coltrane`

这正确吗？[y/n: y] y

[..映射生成过程的输出..]

NIS 映射更新完成。

`ellington` 已被设置为 YP 主服务器，没有任何错误。

这将从 `/var/yp/Makefile.dist` 创建 `/var/yp/Makefile`。默认情况下，这假设环境是一个只有 FreeBSD 客户端的单 NIS 服务器。由于 `test-domain` 有一个从服务器，请编辑 `/var/yp/Makefile` 中的这一行，使其以注释 `#` 开头：

```
NOPUSH = "True"
```

## 30.4.4.2. 添加新用户

每当创建一个新用户时，必须重建 NIS 映射。要在 `test-domain` 中添加新用户，请在主服务器上运行这些命令：

```
# useradd jsmith
# ypmap jsmith
```

## 30.4.4.5. 设置从服务器

设置 NIS 从服务器，像设置主服务器一样编辑 `/etc/rc.conf`。使用 `-s`（代表从）而不是 `-m`（代表主），如例所示：

```coltrane# ypinit -s ington test-domain
```

`Server Type: SLAVE Domain: test-domain Master: ington`

创建 YP 服务器将需要你回答几个问题。所有问题将在过程开始时询问。

你希望此过程在遇到非致命错误时退出吗？[y/n: n] n

好的，请记住返回并手动重做任何失败的操作。否则，某些功能可能无法工作。将不再有更多问题。剩余过程将需要几分钟来从 `ington` 复制数据库。

`Transferring netgroup...`

`ypxfr: Exiting: Map successfully transferred`

`Transferring netgroup.byuser...`

`ypxfr: Exiting: Map successfully transferred`

`Transferring netgroup.byhost...`

`ypxfr: Exiting: Map successfully transferred`

`Transferring master.passwd.byuid...`

`ypxfr: Exiting: Map successfully transferred`

`Transferring passwd.byuid...`

`ypxfr: Exiting: Map successfully transferred`

`Transferring passwd.byname...`

`ypxfr: Exiting: Map successfully transferred`

`Transferring group.bygid...`

`ypxfr: Exiting: Map successfully transferred`

`Transferring group.byname...`

`ypxfr: Exiting: Map successfully transferred`

`Transferring services.byname...`

`ypxfr: Exiting: Map successfully transferred`

`Transferring rpc.bynumber...`

`ypxfr: Exiting: Map successfully transferred`

`Transferring rpc.byname...`

`ypxfr: Exiting: Map successfully transferred`

`Transferring protocols.byname...`

`ypxfr: Exiting: Map successfully transferred`

记得有效地更新映射版本。

这将在从机服务器上生成一个名为 `/var/yp/test-domain` 的目录，其中包含 NIS 主服务器映射的副本。在每个从机服务器上添加这些 `/etc/crontab` 条目，可以强制从机将其映射与主服务器的映射同步：

```
20 * * * root /usr/libexec/ypxfr passwd.byname
21 * * * * root /usr/libexec/ypxfr passwd.byuid
```

这些条目并非强制性，因为主服务器会自动尝试将任何映射更改推送到从机。然而，由于客户端可能依赖从机服务器提供正确的密码信息，建议强制频繁更新密码映射。这在繁忙的网络中为重要，因为映射更新可能并不总是完成。

要完成配置，在从机服务器上运行 `/etc/netstart` 以启动 NIS 服务。

## 30.4.6. 设置 NIS 客户端

NIS 客户端使用 `ybind(8)` 绑定到 NIS 服务器。该守护进程在本地网络上广播 RPC 请求。

这些请求指定了客户端上配置的域名。如果相同域名内的 NIS 服务器接收到其中一个广播，它将响应 `ybind`，`ybind` 将记录服务器的地址。如果有多个可用服务器，客户端将使用 r 服务器的地址进行响应，并将所有的 NIS 请求重导至该服务器。客户端将定期自动 ping 服务器以确保其仍然可用。如果在合理时间内未收到回复，`ybind` 将将域名标记为未绑定（unbound）并开始再次广播，希望找到另一个服务器。

要将 FreeBSD 机器配置为 NIS 客户端：

- 1. 编辑 `/etc/rc.conf` 并添加以下行，以便在网络启动期间设置 NIS 域名并启动 `ybind(8)`：

```
nisdomainname="test-domain"
nis_client_enable="YES"
```

- 2. 要从 NIS 服务器导入所有可能的密码条目，请使用 `wipw` 从 `/etc/master.passwd` 中删除一个账户以外的所有用户账户。在删除账户时，请记住至少应保留一个本地账户，且该账户应该是 `wheel` 组的成员。如果 NIS 出现问题，可以使用此本地账户进行远程登录、成为超级用户并修复问题。在保存编辑之前，在 `::` 末尾添加以下行：

```
+::::::::
```

此行配置客户端，为在 NIS 服务器密码映射中具有有效账户的用户在客户端上提供账户。通过修改此行配置 NIS 客户端的方法有很多。第 30 章. 网络服务器

一种方法在第 30.4.8 节“使用 Netgroups”中描述。如需更详细的阅读，请参考 O'Reilly Media 出版的《Managing NFS and NIS》一书。

- 3. 要从 NIS 服务器导入所有可能的组条目，请向 `/etc/group` 添加此行：

```
+:*:
```

要立即启动 NIS 客户端，请以超级用户执行以下命令：

```
# /etc/netstart
```

```
# service ybind start
```

完成这些步骤后，在客户端上运行 `ypcat passwd` 应显示服务器的 passwd 映射。

## 30.4.7. NIS 安全

由于 RPC 是基于广播的服务，在相同域名内运行 `ypbind` 的系统都可以检索 NIS 映射的内容。为了防止未经授权的事务，`ypserv(8)` 支持一项“securenets”功能，可用于限制对一组主机的访问。默认情况下，此信息存储在 `/var/yp/securenets` 中，除非启动 `ypserv(8)` 时使用了 `-p` 和备用路径。它包含由空格分隔的网络规范和网络掩码条目。以 `#` 开头的行被视为注释。一个 `securenets` 示例可能如下：

```
# 允许来自本地主机的连接 -- 强制

127.0.0.1 255.255.255.255

# 允许来自任何主机的连接

# 在 192.168.128.0 网络上

192.168.128.0 255.255.255.0

# 允许来自 10.0.0.0 到 10.0.15.255 之间的任何主机的连接
# 这包含了 testlab 中的机器

10.0.0.0 255.255.240.0
```

如果 `ypserv(8)` 收到匹配这些规则之一的地址的请求，它将正常处理请求。如果地址未匹配规则，请求将被忽略并记录警告消息。如果 `securenets` 不存在，`ypserv` 将允许来自任何主机的连接。

第 14.4 节“TCP Wrapper”是提供 `securenets` 的另一种访问控制机制。虽然任何访问控制机制都增加了安全性，但它们都容易受到“IP 欺骗”攻击。所有与 NIS 相关的流量都应在防火墙处拦截。使用 `securenets` 的服务器可能无法为具有过旧 TCP/IP 实现的合法 NIS 客户端提供服务。某些这些实现。某些

1392

某些这些实现。某些...

able, baker, ...

实习生

# 表 30.3. 附加系统

| 机器名称(s) | 描述 |
| :--- | :--- |
| war, death, famine, pollution | 仅允许 IT 员工登录这些服务器。 |
| pride, greed, envy, wrath, lust, sloth | 允许 IT 部门的所有成员登录这些服务器。 |
| one, two, three, four, ... | 员工使用的普通工作站。 |
| trashcan | 一台没有任何关键数据的极旧机器。甚至允许实习生使用此系统。 |

使用 netgroups 配置此场景时，每个用户都会被分配给一个或多个 netgroup，然后对该 netgroup 的所有成员进行允许或禁止登录设置。当添加新机器时，必须为所有 netgroups 定义登录限制。当添加新用户时，必须将该账户添加到一个或多个 netgroups 中。如果 NIS 的设置得当当，则只需要对一处中央配置进行修改，即可授予或拒绝对机器的访问。

第一步是初始化 NIS netgroup 映射。在 FreeBSD 中，默认不会创建此映射。在 NIS 主服务器上，使用编辑器创建一个名为 `/var/yp/netgroup` 的映射。

572

# 第 30 章. 网络服务器

此示例创建了四个 netgroup，分别代表 IT 员工、IT 学徒、普通员工和实习生：

`IT_EMP (,alpha,test-domain) (beta,test-domain)`

`IT_APP (,charlie,test-domain) (,delta,test-domain)`

`(,golf,test-domain)`

`INTERNS (,able,test-domain) (,baker,test-domain)`

每个条目配置一个 netgroup。条目中的第一列是 netgroup 的名称。每组括号代表一个或多个用户的用户组，或者另一个 netgroup 的名称。在指定用户时，每个组内部三个逗号分隔的字段表示：

- 1. 代表用户的其他字段有效的主机(s)名称。如果未指定主机名，则该条目在所有主机上均有效。
- 2. 属于此 netgroup 的账户名称。
- 3. 该账户的 NIS 域。账户可以从其他域导入到 netgroup。

如果一个组包含多个用户，请用空格分隔每个用户。此外，每个字段可能包含通配符。详见 `netgroup(5)`。

不应使用长度超过 8 个字符的 netgroup 名称。名称对大小写敏感，在 netgroup 名称中使用大写字母是区分用户、机器和 netgroup 的简单方法。

某些非 FreeBSD NIS 客户端无法处理包含超过 15 个条目的 netgroup。可以通过创建几个包含 15 个或更少用户的子 netgroup，以及一个由这些子组组成的实际 netgroup 来绕过此限制，例如所示：

`BIGGRP1 (joe1,domain) (joe2,domain) (joe3,domain) [...]`

`BIGGRP2 (joe16,domain) (joe17,domain) [...]`

`BIGGRP3 (joe31,domain) (joe32,domain)`

`BIGGROUP BIGGRP1 BIGGRP2 BIGGRP3`

如果单个 netgroup 中存在超过 225 个（15  15）用户，请重复此过程。

激活并分发新的 NIS 映射：

```
root# cd /var/yp
```

```
ellington# make
```

这将生成三个 NIS 映射：`netgroup`、`netgroup.byhost` 和 `netgroup.byuser`。使用 `ypcat(1)` 的 map 选项检查新的 NIS 映射是否可用：

`ellington% ypcat -k netgroup`

`ellington% ypcat -k netgroup.byhost`

`ellington% ypcat -k netgroup.byuser`

`ypscat` 命令的输出应该类似于 `/var/yp/netgroup` 的内容。第二个命令仅在创建了特定主机的 netgroup 时才会产生输出。第三个命令用于获取某个用户的 netgroup 列表。

要配置客户端，请使用 `vipw(8)` 指定 netgroup 的名称。例如，在名为 `war` 的服务器上，替换此行：

```
+::::::
```

为：

```
+@IT_EMP::::::
```

这指定了 netgroup `IT_EMP` 中定义的用户会被导入到系统的密码数据库中，并且仅允许这些用户登录此系统。

573

使用 Netgroups

此配置也适用于 shell 的 `~` 函数以及所有在用户名和数字用户 ID 之间转换的程序。换句话说，`cd ~ user` 将无法工作，`ls -l` 将显示数字 ID 而不是用户名，而 `find . -user joe -print` 将失败并显示消息 No such user。为了修复此问题，导入所有用户条目但不允许他们登录服务器。这可以通过添加额外行来实现：

```
+::::::/usr/sbin/nologin
```

此行配置客户端导入所有条目，但将这些条目中的 shell 替换为 `/usr/sbin/nologin`。

确保额外行位于 `+@IT_EMP::::::` 之后。否则，从 NIS 导入的所有用户账户都将使用 `/usr/sbin/nologin` 作为登录 shell，导致没有人能登录系统。

要配置不那么重要的服务器，请将 `/etc/passwd` 中的旧行替换为：

```
+@IT_EMP::::::
```

```
+@USERS::::::
```

```
+::::::/usr/sbin/nologin
```

NIS 支持从其他域创建 netgroups，这在策略发生变化时非常有用。例如，可以创建一个名为 `BIGSRV` 的 netgroup 来定义重要服务器，另一个名为 `SMALLSRV` 的 netgroup 用于不重要的服务器，第三个名为 `USERBOX` 的 netgroup 用于工作站。NIS 映射的新条目如下：

```
# 先定义用户组
IT_EMP (,alpha,test-domain) (beta,test-domain)
IT_APP (,charlie,test-domain) (,delta,test-domain)
DEPT1 (,echo,test-domain) (foxtrot,test-domain)
DEPT2 (,golf,test-domain) (hotel,test-domain)
DEPT3 (,india,test-domain) (juliet,test-domain)
ITINTERN (,kilo,test-domain) (lima,test-domain)
D_INTERNS (,able,test-domain) (,baker,test-domain)

# 现在，根据角色定义一些组
USERS DEPT1 DEPT2 DEPT3
BIGSRV IT_EMP IT_APP
SMALLSRV IT_EMP ITINTER
USERBOX IT_EMP INTERN
```

这种定义登录限制的方法在定义机器组时非常有效。遗憾的是，这是例外。通常需要根据机器定义登录限制。特定机器 netgroup 是处理策略变化的另一种可能性。建议使用主机名的全大写版本作为 netgroup 的名称：

```
+@BOXNAME::::::
+::::::/usr/sbin/nologin
```
