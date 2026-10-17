
点击 VPN 屏幕顶部面板上的网络图标。悬停在 `VPN Connections`（VPN 连接）上，并选择 `Configure VPN`（配置 VPN），如图 28.3 所示。

![](img/2a083394994f21b612810fd7c32a8def_617_0.png)

图 28.3 Network Manager 让配置 VPN 客户端变得简单。

点击 `Add`（添加）以创建新的 VPN 连接。

从列表中选择你的 VPN 连接类型。如果你不确定连接类型，请尝试你认为正确的类型；如果不起作用，回来编辑连接以尝试另一种类型。

点击 `Create`（创建）。

输入有关你的 VPN 连接的信息。你需要输入服务器的网关 IP 地址、你的账户用户名和密码、可能还有组名和组密码，以及查找证书机构 (CA) 文件所在的位置。在某些情况下，你可能需要点击 `Advanced`（高级）按钮以输入其他详情，例如加密方法、NAT 穿透等。输入信息后，点击 `Save`（保存）。

要开始使用此 VPN 连接，请使用图 28.3 相同的菜单，但这次是从列表中选择你的 VPN 连接，在你的示例中显示为 `Main VPN Connection`（主 VPN 连接）。

# 虚拟专用网络 (VPN)

我们使用 OpenVPN 设置简单的服务器。高级配置可能会变得复杂，但如果你只需要一个基础服务器，很容易上手。

从 Ubuntu 软件仓库安装 `openvpn`。

接下来的几步为你的 OpenVPN 创建公钥基础结构 (PKI)。

设置证书机构以生成你自己的证书和密钥。

```
matthew@seymour:- $ cd /etc/openvpn
matthew@seymour:- $ mkdir easy-rsa
matthew@seymour:- $ cp -r /usr/share/doc/openvpn/examples/easy-rsa/* /etc/openvpn/easy-rsa/
```

生成证书机构：

```
matthew@seymour:- $ source vars
matthew@seymour:- $ clean-all
matthew@seymour:- $ init-ca
```

生成服务器证书：

```
matthew@seymour:- $ gen-req server
```

构建 Diffie-Hellman 参数：

```
matthew@seymour:- $ gen-dh -out dh2048.pem
```
![](img/2a083394994f21b612810fd7c32a8def_618_0.png)

签名服务器证书：

```
matthew@seymour:- $ sign-req -ca.key server
```

生成客户端证书密钥：

```
matthew@seymour:- $ gen-req client
```

签名客户端证书：

```
matthew@seymour:- $ sign-req -ca.key client
```

现在，将必要的文件复制到 `/etc/openvpn`：

```
matthew@seymour:- $ cp ca.crt server.crt server.key dh2048.pem /etc/openvpn/
```

编辑 `/etc/openvpn/server.conf` 以指向并使用你创建的证书，修改这些行。将 `yourservername` 替换为你的服务器名称。保持其他默认值。

```
# server.conf (示例)
ca ca.crt
cert server.crt
key server.key
dh dh2048.pem
```

启动你的服务器：

```
matthew@seymour:- $ sudo /etc/init.d/openvpn start
```

为客户端创建一个配置文件：

```bash
# client
ca ca.crt
cert client.crt
key client.key
```

将客户端文件移动到客户端机器上：

```
matthew@seymour:- $ sudo cp ca.crt client.crt client.key /etc/openvpn/
```

编辑 `/etc/openvpn/client.conf` 以指向服务器的 IP：

```
# client.conf (示例)
remote your_server_ip 1194
ca ca.crt
cert client.crt
key client.key
```

连接客户端：

```
matthew@seymour:- $ sudo openvpn --config /etc/openvpn/client.conf
```

# 第 29 章 管理关系型数据库服务

## 本章内容

## 管理关系型数据库服务

- 数据库基础简述
- 选择数据库：MySQL 对比 PostgreSQL
- 配置 MySQL
- 配置 PostgreSQL
- 参考文献

本章介绍了 MySQL 和 PostgreSQL，这是 Ubuntu 存储库中提供的两种数据库系统。你将学习到这些系统的功能、这两个程序之间的对比较，以及如何考虑它们的优缺点。这些信息可以帮助你决定为组织的数据库需求选择并部署哪种数据库。

## 与 MySQL 相似的内容

2009 年 4 月，Oracle 宣布将收购 MySQL 的所有者 Sun 微系统公司。该交易于 2010 年完成。在短期内，这实际上并没有产生任何影响，但数据库界正在密切关注 MySQL 将发生什么变化，且至少有两个小组对代码进行了分叉（fork），以确保该数据库在保持活跃开发的同时依然免费且开源。这些小组已经发布并正在致力于 MariaDB (https://mariadb.org/)、Drizzle (http://drizzle.org/) 和 Percona Server (http://www.percona.com/software/percona-server)。虽然目前还没有人确切知道会发生什么，但我们建议关注 MySQL 的项目和其他潜在的替代方案，以防最坏的担心变为现实——即 Oracle 认为免费的 MySQL 与其付费数据库产品竞争过于激烈，从而杀掉或削弱该项目。有趣的是，一些相当大的 Linux 发行版和组织已经放弃了 MySQL，例如 Fedora、OpenSense 和 Wikipedia（它们现在都在使用 MariaDB）。好消息是，你从本章中学到的关于 MySQL 的任何知识可能都完美适用于提到的其他选项。

## 第 29 章 管理关系型数据库服务

组织的数据库管理员 (DBA) 有几项职责，这些职责根据组织的规模、运营情况、支持人员等有所不同。根据组织的具体结构，如果你是该组织的 DBA，你的职责可能包括以下内容：

- **安装和维护数据库服务器**——你可能需要安装和维护数据库软件。维护可能安装补丁以及在适当的时间升级软件。作为 DBA，你需要对系统拥有 root 权限，并知道如何管理软件（见第第 9 章“管理软件”）。你还需要意识到内核、文件系统以及其他安全问题。
- **安装和维护数据库客户端**——数据库客户端是用于本地或通过网络远程访问数据库的程序（你将在本章稍后的“数据库客户端”部分学习更多内容）。你的职责可能包括在用户的系统中安装和维护这些客户端程序。本章讨论了如何从 Linux 命令行以及通过图形界面数据库工具安装和使用这些客户端。
- **管理账户和用户**——账户和用户管理包括从数据库中添加和删除用户、分配和管理密码等。在本章中，你将学会如何为 MySQL 和 PostgreSQL 授予和撤销用户权限以及密码。
- **确保数据库安全**——为了确保数据库安全，你需要确保只有授权人员可以访问数据库，并通过权限确保能够访问数据库的人无法执行不该的操作。在本章中，你将学习如何管理安全 Shell (SSH)、Web 和本地图形用户界面 (GUI) 客户端访问数据库。规划和监督定期备份组织的数据库并从这些备份中恢复数据是数据库安全的另一个关键环节。
- **确保数据完整性**——在存储在服务器磁盘存储上的所有信息中，数据库的变化是最关键的。确保数据完整性涉及规划多用户访问，并确保当一个一个用户同时对数据库进行更改时，更改不会丢失或重复。

## 数据库基础简述

本章讨论的软件在 Linux 下的数据库服务基于客户端/服务器模型。数据库客户端通常用于输入数据以及查询或显示来自服务器的结果。你可以使用命令行或图形客户端访问正在运行的服务器。数据库通常有两种形式：平文件和关系型。平文件数据库可以简单只是一个文本文件，使用空格、制表符或其他字符来分隔信息的部分内容。简单平文件数据库的一个例子是 `/etc/passwd` 文件。另一个例子是简单的地址簿，可能像这样：

doe-Anytown-NY-12345-555

你可以使用 `grep`、`awk` 和 `perl` 等标准工具从这种原始数据库中搜索和提取信息。虽然这对于小型的小数据平文件数据库可能效果良好，但这种类型的平文件数据库有以下几个局限性：
