

## 更新和审计 NIS 映射

更新默认映射之一（配置主服务器时自动生成的映射）相当简单。编辑相应的源文件，然后从 /var/yp 目录中执行 **make(1)** 命令。要更新的映射名称必须作为命令行参数指定给 **make** 命令。**make** 命令会更新映射，并自动将更新后的映射传播到任何从服务器。以下示例显示了用于更新 hosts 映射并将其传播到从服务器的命令：

```sh
# cd /var/yp
# make hosts
```

要添加新映射（称为*非默认映射*），请在主服务器的 /var/yp 目录中创建包含相应信息的文本文件。然后运行 **makedbm(1M)** 命令来添加该映射。**makedbm** 命令需要两个命令行参数：源文件的名称和要创建的映射的名称。**ypxfr(1M)** 命令用于分发当前在从服务器上不存在的新映射。新映射的名称作为命令行参数指定。以下几行从 apps.txt 源文件创建新映射 apps：

```sh
# cd /var/yp
# makedbm apps.txt apps
# /usr/lib/netsvc/yp/ypxfr apps
```

要更新并传播非默认映射，请编辑源文件，然后运行 **makedbm** 命令重新构建该映射。要传播更新后的映射，请使用 **yppush(1M)** 命令并将映射名称指定为命令行参数。以下几行从 apps.txt 源文件重新构建 apps 映射，并将其传播到从服务器：

```sh
# cd /var/yp
# makedbm apps.txt apps
# /usr/lib/netsvc/yp/yppush apps
```

## 验证 NIS 配置

有多种命令可以访问 NIS 配置信息。您可以使用这些命令来验证客户端配置并检查映射的内容。有关更多详细信息，请参阅*系统参考手册*：

- **ypcat(1)** — 列出指定映射的内容。
- **ypmatch(1)** — 从指定映射中返回与指定键匹配的数据。
- **ypwhich(1)** — 返回 NIS 服务器或映射主服务器的名称。当与 -m 命令行参数一起使用时，ypwhich 命令将返回所有可用映射的列表。

## 网络信息服务增强版（NIS+）

NIS+ 与 NIS 相似，但提供了更多功能。除了提供集中化管理和域数据访问之外，它还支持分层域命名空间，可配置为反映组织的结构；而 NIS 仅提供平面域。NIS 不提供认证，但 NIS+ 提供基于数据加密标准（DES）的认证。此外，NIS 以批量模式传播更新信息，而 NIS+ 会立即传播增量更新。与 NIS 一样，NIS+ 支持可选使用冗余服务器（称为副本服务器）。这些副本服务器提供负载均衡，并在主 NIS+ 服务器发生故障时提供备用服务器。

NIS 将其数据存储在称为映射的文件中；NIS+ 将其数据存储在称为表的文件中。NIS+ 为 NIS 映射中存储的所有数据提供了表，并额外提供了一些用于凭据、时区和自动挂载信息的表。表 19.4 列出了 NIS+ 表。

这些表存储在按域名命名的目录下。该目录包含另外三个目录：ctx_dir.domain（用于 XFN (FNS) 数据）、org_dir.domain（用于存储表）和 groups_dir.domain（用于组信息）。

**表 19.4 NIS+ 表**

| 表 | 描述 |
|---|---|
| auto_home | 用户主目录的位置 |
| auto_master | AutoFS 映射信息 |
| bootparams | 无盘工作站的根分区、交换分区和转储分区的位置 |
| cred | NIS+ 主体的凭据 |
| ethers | 系统的以太网地址 |
| group | 组名、GID 和成员信息 |
| hosts | 主机名和网络（IP）地址 |
| mail_aliases | 邮件地址和别名 |
| netgroup | 域中定义的网络组和成员 |
| netmasks | 与已知网络关联的网络掩码 |
| networks | 网络及其关联名称 |
| passwd | 用户账户的密码信息 |
| protocols | 域中使用的 IP 协议 |
| rpc | 域中使用的 RPC 服务的 RPC 程序号 |
| services | IP 服务及其端口号 |
| timezone | 域中工作站的时区 |

## 练习题

### 问题 1

以下哪种命名服务要求在其使用的每个系统上手动配置数据？

- a. NIS
- b. NIS+
- c. DNS
- d. /etc 文件

答案 d 正确。/etc 文件要求在其使用的每个系统上手动配置数据。所有其他命名服务都提供了更新一个主数据库并将更改传播到需要它们的每个系统的方法。因此，答案 a、b 和 c 不正确。虽然对于少数系统来说，使用 /etc 文件简单快捷，但使用 NIS、NIS+ 或 DNS 可以降低许多系统的维护成本。

### 问题 2

输入一种方法的名称，该方法基于用户凭据限制对 NIS+ 资源的访问。

正确答案是 authentication（认证）。

### 问题 3

以下哪些是 NIS+ 提供的功能？（选择所有适用的选项。）

- a. 认证
- b. 时区支持
- c. 批量传播更新
- d. 分层域体系结构
- e. 平面域体系结构

答案 a、b 和 d 正确。NIS+ 提供认证、时区支持和分层域体系结构。批量传播更新和平面域体系结构是 NIS 的特征。因此，答案 c 和 e 不正确。

### 问题 4

以下哪些命名服务受 Solaris 8 操作系统支持？（选择所有适用的选项。）

- [ ] a. NIS
- [ ] b. NIS+
- [ ] c. FNS
- [ ] d. DNS
- [ ] e. /etc 文件配置

答案 a、b、c、d 和 e 正确。Solaris 8 操作系统支持 NIS、NIS+、FNS、DNS 和 /etc 文件配置。

### 问题 5

以下哪个命令用于配置 NIS 客户端？

- ( ) a. `ypinit -m`
- ( ) b. `ypinit -c`
- ( ) c. `ypinit -s`
- ( ) d. `nisclient`
- ( ) e. `nisinit -c`

答案 b 正确。`ypinit -c` 命令用于配置 NIS 客户端。`ypinit -m` 用于配置主服务器。因此，答案 a 不正确。`ypinit -s` 用于配置从服务器。因此，答案 c 不正确。答案 d 和 e 中的命令不存在。

### 问题 6

以下哪一项*不是*有效的搜索状态消息类型？

- ( ) a. SUCCESS
- ( ) b. NOTFOUND
- ( ) c. TRYLATER
- ( ) d. UNAVAIL

答案 c 正确。TRYLATER 不存在；正确的关键字是 TRYAGAIN。SUCCESS、NOTFOUND 和 UNAVAIL 是有效的搜索状态消息。因此，答案 a、b 和 d 不正确。

### 问题 7

请指出用于提供 DNS 服务的 BIND 程序的名称。

正确答案是 in.named 程序。

### 问题 8

以下哪些是可在 /etc/nsswitch.conf 文件中使用的信息类型关键字？（选择所有适用的选项。）

- [ ] a. **hosts**
- [ ] b. **ipaddr**
- [ ] c. **protocols**
- [ ] d. **services**

答案 a、c 和 d 正确。**hosts**、**protocols** 和 **services** 关键字可用于 /etc/nsswitch.conf 文件。**ipaddr** 不是有效关键字。IP 地址是 hosts 信息的一部分。因此，答案 b 不正确。

### 问题 9

NIS 用来存储 NIS 客户端请求的信息的文件统称为什么？

正确答案是映射（maps）。

### 问题 10

以下哪个命令用于将新的 NIS 映射传播到 NIS 从服务器？

- ( ) a. **yppush**
- ( ) b. **ypupdate**
- ( ) c. **ypprogate**
- ( ) d. **ypxfr**
- ( ) e. **ypmaps**

