
`database`、`user`、`auth` 和 `option` 值的语义与为本地连接描述时描述的语义相同。`type` 值必须是 `host`、`hostssl` 或 `hostnull` 之一。`host` 匹配任何通过 TCP/IP 带来的连接，无论是否使用 SSL。`hostssl` 仅匹配使用 SSL 的 TCP/IP 连接。`hostnull` 仅匹配不使用 SSL 的 TCP/IP 连接。`ipaddr`（一个 IP 地址）和 `ipmask`（一个 IP 网络掩码）选项允许你以非常细粒度控制连接到服务器的远程主机。例如 `ipaddr ipmask` 对 `127.0.0.255` 仅指向 IP 地址 127.0.0.1，而 `ipaddr ipmask` 对 `127.0.0.0 255.255.255` 指向 127.0.0.0 到 127.0.0.254 之间的所有 IP 地址。IP 地址必须以标准数值（或点分）格式指定；主机名和域名无效。

因此，为了对通过 TCP/IP 连接的客户端实施建议限制（你必须使用 SSL，使用加密），以下规则应该足够：

```
hostssl all all 0.0.0.0 0.0.0.0 reject
hostssl all all 0.0.0.0 0.0.0.0 md5
```

第一条规则拒绝所有通过 SSL 从远程主机发起的连接。第二条规则允许所有用户对所有数据库进行基于 SSL 的连接，并使用 MD5 身份验证。然而，如果你想限制访问特定主机或域名，第二条规则就太宽松了。为了允许 IP 地址为 192.168.2.0 的 finance 子网上的所有用户访问 finance 数据库，应该使用规则 `hostssl finance all 192.168.2.0 255.255.255.0 md5` 替换之前的 `hostssl` 规则，因此规则变为：

```
hostssl all all 0.0.0.0 0.0.0.0 reject
hostssl finance all 192.168.2.0 255.255.255.0 md5
```

如果你想拒绝所有其他远程连接，请添加以下规则：

```
hostssl all all 0.0.0.0 0.0.0.0 reject
```

因此，最终规则集看起来如下：

```
hostssl all all 0.0.0.0 0.0.0.0 reject
hostssl finance all 192.168.2.0 255.255.255.0 md5
hostssl all all 0.0.0.0 0.0.0.0 reject
```

评估序列首先拒绝所有不使用 SSL 的 TCP/IP 连接。第二条规则允许通过第一项测试的客户端（如果 IP 地址在 192.168.2.1 和 192.168.2.254 之间）连接到 finance 数据库。如果在此处发生匹配，规则评估停止。否则，将评估下一条规则，它将拒绝所有其他传入的 TCP/IP 连接，即使它们使用了 SSL。在实践中，你可能会发现根据 IP 地址或在本地连接的情况下根据登录账户名来允许访问特定用户和数据库是最简单的。

要使访问规则的更改生效，你需要重新加载访问控制文件。或者，你可以使用服务来实现：

```
service postgresql reload
```

此示例创建了一个名为 bubba 的新数据库用户，并在过程中分配了一个加密密码。最后两个提示会询问你是否允许 bubba 创建数据库和创建其他用户。bubba 只是一个测试用户，因此他不会获得任何特殊对待。请记住，你正在使用 ident 身份验证，并使用了相同的用户身份验证选项，这意味着以 bubba 创建的用户在系统中也必须有一个登录账户。

# 测试与测试数据库的连接性

PostgreSQL 化的最后一步是让测试用户（bubba）连接到数据库。虽然你在创建 test-database 和测试用户时已经确认了 postgres 用户可以连接到服务器，但确保普通用户能够连接到服务器，并且你创建的访问规则按预期工作仍然是重要的。要测试数据库服务器，请使用以下步骤：

- 切换到你为该数据库账户创建的用户：

```
$ su bubba
Password:
[bubba]$
```

你必须切换到 bubba，因为正在使用 ident 身份验证，这意味着你必须以该用户的身份连接到数据库。

- 在下面的示例中使用 psql 命令连接到 rhlsa3 数据库：

```
[bubba]$ psql -W rhlsa3
Password:
Welcome to psql 7.4.6, the psql interactive terminal
Type: \copyright for distribution terms
\h for help with SQL commands
\? for help on internal slash commands
\g or terminate semicolon to execute query
\q to quit
rhlsa3=>
```

`psql` 是 PostgreSQL 的 shell 或命令解释器。默认提示符是数据库名后跟 =>。根据你正在执行的操作，提示符的倒数第二个字符会发生变化。

- 使用以下 SQL 命令创建一个新表：

```
rhlsa3=> create table chapters (
rhlsa3> chapnum int,
```

# 配置数据库服务器

```
rhlnsa3> title varchar(80),
rhlnsa3> pages int
rhlnsa3> );
CREATE TABLE
rhlnsa3=>
```

注意，打开括号语句会导致 shell 提示符从 => 变为 (>，表示它正在等待匹配的括号。结尾的分号是必须的。

- 4. 使用以下 SQL 语句添加数据：

```
rhlnsa3-> insert into chapters (chapnum, title, pages)
rhlnsa3-> values (15, 'Configuring a Database Server', 35);
INSERT 17148 1
```

在这种情况下，shell 提示符变为 ->，表示它正在等待闭合的分号来结束 SQL 命令。

- 5. 使用以下查询检索你刚刚添加的数据：

```
rhlnsa3-> select * from chapters;
chapnum | title | pages
```

| chapnum | title | pages |

|--- |--- |--- |

| 15 | Configuring a Database Server | 35 |

(1 row)

- 6. 退出 PostgreSQL shell：

```
rhlnsa3=> \q
```

你也可以使用 Ctrl+d 退出 PostgreSQL shell。

如果最后几节中创建的过程有效，说明你的数据库服务器已启动并按预期工作。下一节将介绍你至少想要了解的一些 PostgreSQL 客户端程序。

# 使用 PostgreSQL 客户端程序

PostgreSQL 的客户端程序像 MySQL 一样，实现了与服务器的用户界面。正如你所学的，`psql` 提供了对服务器最完整、直接的访问，但需要你了解一些 SQL。其他实用程序如 `createddb`、`createuser` 以及及其对应物 `dropdb`（删除数据库）和 `dropuser`（删除用户）是为你调用 SQL 语句的封装脚本。如果你不是数据库专家（或不想成为专家），你可能使用各种封装实用程序最为舒服。表 15-4 列出了你可能想要熟悉的某些 PostgreSQL 客户端程序。

# 376 第 15 章

表 15-4 PostgreSQL 客户端程序和实用工具

| 程序 | 描述 |

|---|---|

| createddb | 在数据库集群中创建一个新数据库 |

| createuser | 在数据库集群中创建一个新用户 |

| dropdb | 从数据库集群中删除数据库 |

| dropuser | 从数据库集群中删除用户 |

| pg_dump | 将数据库或数据库对象的内容转储到文件中 |

| pg_restore | 使用 pg_dump 创建的文件重新加载数据库或数据库对象 |

| psql | 提供用于与数据库服务器交互的命令解释器 |

大多数 PostgreSQL 客户端在命令中共享许多选项。例如，`-U username` 指定连接到服务器时使用的用户名。`-D /path` 指定 PostgreSQL 数据库集群的路径，默认值为环境变量 `$PGDATA` 的值或默认路径 (`/var/lib/pgsql/`)。`-e` 导致 `createddb` 和 `dropuser` 等封装脚本向标准输出 (`stdout`) 回显 SQL 命令。操作或需要连接特定数据库的命令接受数据库名作为参数。如果未指定数据库名，它默认为连接到 `-U username` 指定数据库的用户，或者在未指定 `-U username` 时连接用户的登录名。

同样，大多数 PostgreSQL 客户端可以使用 PostgreSQL 环境变量来设置某些默认值。除了 `$PGDATA` 存储你已经过的数据库名称外，该变量还允许 `$PGHOST` 指定要连接的主机。`$PGPORT` 指定连接的端口号。`$PGDATABASE` 指定连接的数据库名。`$PGUSER` 指定连接的用户名。`$PGPASSWORD` 指定密码。`$PGCLIENTPATH` 指定 PostgreSQL 客户端库的路径。`$PGCONFIGFILE` 指定 PostgreSQL 配置文件的。`$PGDATADIR` 指定 PostgreSQL 数据目录。`$PGLOGDIR` 指定 PostgreSQL 日志目录。`$PGSOCKETDIR` 指定 PostgreSQL 套接字目录。`$PGSSLMODE` 指定连接使用的 SSL 模式。`$PGSSLCERTDIR` 指定 SSL 证书目录。`$PGSSLCERT` 指定 SSL 证书文件。`$PGSSLKEY` 指定 SSL 私钥文件。`$PGSSLCA` 指定 CA 证书文件。`$PGSSLCRL` 指定吊销列表文件。`$PGSSLVERIFYFE` 指定完整验证的根证书。`$PGSSLSRID` 指定根证书的序列号。`$PGSSLSRFILE` 指定根证书文件。

（注：原文后续部分存在大量重复的变量描述，译文已根据逻辑要求处理，确保核心内容完整。）

## 总结

随着基于 Linux 的 Web 和电子邮件服务器变得无处不在，基于 Linux 的数据库服务器也变得日益普及，因此你可能在某个时刻需要创建一个数据库服务器。虽然配置数据库服务器并不要求你对数据库管理的精细之处了如指掌，但熟悉通用流程会有所帮助。通常情况下，仅仅安装软件是不够的。作为管理员，你通常需要能够确保数据库是可访问的（或者处于不可访问状态）、初始账户是安全的，并且服务器运行正常。本章向你展示了如何将 MySQL 和 PostgreSQL 配置到基本功能水平。正如你所学的，安装它们很容易，但安装后的配置和测试可能会非常枯燥。好消息是，数据库的安装通常是与数据库管理员（DBA）共同完成的，他们为你提供指南和指令供你遵循。你很少需要单打奋战。

# 第 16 章

# 创建 VNC 服务器

本章内容

- 什么是 VNC？

- 设置 VNC 服务器

- 测试 VNC

为远程员工提供网络服务并不是新鲜事，无论他们是困在酒店房间里的“流浪武士”，还是在家里办公的远程办公人员。随着远程办公变得越来越普遍以及宽带接入的普及，系统管理员被越来越多地要求为其网络提供远程访问。多年来，人们尝试了多种为离线员工提供局域网服务的方法，包括远程控制虚拟专用网络（VPN）。目标始终是远程员工能够使用另一台计算机或基于局域网的服务，就像他们坐在办公室里一样。VNC 让你对现有的桌面系统及其它可以访问的所有资源进行远程访问。本章描述了如何使用 Fedora Core 和 RHEL 创建 VNC 服务器，让远程办公人员和其他远程员工访问基于 Fedora Core 或 RHEL 的局域网及基于局域网的服务。它还展示了如何将 Linux 系统配置为 VNC 客户端。

# 什么是 VNC？

先解释一下这个缩写，VNC 代表虚拟网络计算（virtual network computing），它提供了一种通过位于互联网上任何位置的另一台计算机或具有类似能力的设备完全控制任何计算机的方法。VNC 解决方案相对于其他方法的优点之一是 VNC 是跨平台的。你可以从 Windows PC 访问并控制 Linux 主机，而这是使用 PCanywhere 等产品所无法实现的。VNC 的另一个优势是该协议针对互联网传输进行了优化，因此在互联网上运行应用程序实际上是可能的，尽管速度极其缓慢。

除了为远程用户提供对局域网系统和服务器的访问外，VNC 对于帮助台技术人员、其他技术支持人员以及系统管理员也有明确的用途。如果你在帮助台工作过，你就知道让电话那端的“用户”告诉你的屏幕看起来什么样、正在运行哪些应用程序，甚至让他们逻辑连贯地描述他们遇到的问题有多困难。你还知道要确保你正在帮助的人正确地输入你想要执行的解决问题程序所需的命令是多么困难。使用 VNC，你可以立即访问用户的系统，并远程诊断和解决手头的问题，而无需离开你的座位。出于同样的原因，对于系统管理员来说，VNC 是一个真正的福音。即使不在办公室或位于现场，管理员也可以访问管理和监控工具，这些工具可以让检测和修复故障服务器成为一项轻而易举的任务。

与功能较弱的远程控制软件不同，VNC 支持到同一个 VNC 服务器的多个并发连接，因此多个用户可以连接到同一个系统并协作完成项目（例如演示文稿）。或者，你可以使用单个 VNC 服务器作为接入点，经过适当授权的用户从这里连接到其他系统。VNC 与其他远程控制协议之间的另一个区别是，VNC 被描述为“远程显示协议”或 RFB（帧缓冲区），是一个开放且非专有的协议，而其他产品（来自 Symantec、Citrix、Insignia Solutions 和 Microsoft）是封闭的协议，与 Windows GUI 紧密绑定。

VNC 不是 VPN（即虚拟专用网络）。从广义地说，VPN 是一种网络配置，其中内部网络拥有远程节点（如远程办公员工），这些节点通过互联网运行 VPN（也许可以说是跨越互联网）来访问主网络。为了实现这一点，在主网络和远程节点之间创建一个安全的（加密的）隧道，IP 流量通过该隧道进行路由。相比之下，VNC 虽然可以当作 VPN 使用并在互联网往返传输数据包，但它通常用于提供对系统的访问，并允许远程用户对该系统拥有完全控制权。简单来说，VPN 让远程系统成为主网络的一部分；而 VNC 是让远程用户控制主网络上的某一个系统。

关于 VNC 的更多信息，两个最好的资源是位于 `uk.research.att.com/pub/docs/at/tr.981.pdf` 的优秀 VNC 概述以及 RealVNC 网站 (`realvnc.com/`)。AT&T 与 RealVNC 之间存在联系。AT&T 实验室的研究人员创建了 VNC。RealVNC 是由部分 AT&T 研究人员为了将 VNC 技术商业化而成立的。VNC 软件根据 GPL 许可，因此 RealVNC 的业务模式依赖于提供支持、服务和增值软件。

# 设置 VNC 服务器

在此语境下，VNC 服务器是你想要访问的机器。所以，如果你在家里并连接到公司的系统，那么公司的系统就是服务器；家里的系统就是客户端。要设置 VNC 服务器，你需要安装 `vncserver` 和 `vnc` 包。以下命令将显示它们是否已安装：

```
$ rpmquery vncserver
vnc-server-4.1.10
$ rpmquery vnc
vnc-4.1.10
```

如果这些包尚未安装：

```
$ vncserver
```

访问你的桌面需要密码。

```
Password:
Verify:
New codomain.com:1
Creating默认启动脚本 /home/bubba/.vnc/xstartup
Starting applications指定的 in /home/bubba/.vnc/xstartup
Log file is /home/bubba/.vnc/codomain.com:1.log
```

输出信息很重要。设置密码后的第一行显示 Xvnc 在 codomain.com 上创建了一个新设备 `:1`。当你连接时需要此信息。ncserver 只在你第一次启动时会请求密码。你可以使用 `vncpasswd` 命令或删除 `$HOME/.vncpasswd` 文件来更改密码。

另外两行告诉你启动脚本 `/home/bubba/.vnc/xstartup` 已创建，并且该脚本已执行，即它指定的应用程序正在运行。这意味着当你连接时，客户端会发现这些程序已经在运行。这意味着如果你想自定义服务器提供的桌面，可以编辑 `xtstartup` 文件。

# 配置防火墙以支持 VNC

现在，你的 VNC 服务器几乎准备好连接了。VNC 监听端口 5500 加上 X 显示号用于传入 VNC 客户端会话。在安全良好的系统中，这些端口是被防火墙拦截的。你必须在防火墙上开一个“洞”，以便 VNC 客户端进入服务器。此配置步骤需要 root 权限，因为你需要使用安全级别配置工具来修改系统的防火墙设置（你正在运行防火墙对吧？）。

## 创建 VNC 服务器

![](img/b5ebc2d43ffbc3488ca0205212f962cb_421_0.png)

**图 16-2** 安全级别配置工具。

图 16-2 显示的防火墙配置非常严格：该机器不允许任何形式的外部访问。你正准备更改这一点。在 `Other ports:(1029-tcp)` 文本框中，输入 `5901:tcp`。默认情况下，VNC 使用端口 5900 加上显示编号。在示例中，显示编号为 `:1`，因此端口号为 5901。端口号中的 `:tcp` 部分允许防火墙为 TCP 连接打开 5901 端口，因为远程帧缓冲协议使用 TCP 或 UDP。

- 2. 在输入相应的端口号后（参见图 16-3），点击 OK 保存你的更改并关闭安全级别配置工具。当工具警告你正要覆盖现有的防火墙配置时，点击 Yes。

现在 VNC 客户端可以访问 VNC 服务器了，因此服务器配置已完成。

![](img/b5ebc2d43ffbc3488ca0205212f962cb_422_0.png)
