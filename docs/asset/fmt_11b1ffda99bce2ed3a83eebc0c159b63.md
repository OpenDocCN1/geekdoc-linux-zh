
`r---rmcd--r---`

NIS+ 表或目录可以向一个或多个类的客户端授予一个或多个访问权限。例如，目录可以授予全局类别读取权限，但仅向组和所有者授予访问（Access）。NIS+ 授权支持灵活且安全的管理。例如，“组”访问权限为 NIS+ 管理提供了更精细的控制。当管理权限变得去中心化时，它可以维护安全和控制。在最初创建 NIS+ 域时，由中央管理人员组成的组可能对跨网络的目录只有修改和创建访问权限。随着域的演变和去中心化，目录可以将这些访问权限授予包含本地和中央管理人员的新组。在保持对现有管理员访问权限的同时扩展访问权限，可以实现控制权的平滑过渡。

当你创建一个对象时，NIS+ 会为该对象分配默认所有者、组和一组访问权限。默认所有者是创建对象的 NIS+ 主体（在这种情况下是你本人）。默认组是 `NIS_GROUP` 环境变量指定的组。默认访问权限集如下所示。

`---rmcd--r---`

你可以通过几种不同的方式更改这些默认值。更改 NIS+ 对象或表项访问权限的一种方法是使用 `nischmod` 命令。要使用 `nischmod` 命令，你必须已经对该对象或项具有修改权限。`nischmod` 命令的语法与 `chmod` 命令的语法非常相似。使用 `+` 运算符添加访问权限，使用 `-` 运算符移除访问权限。例如，你

# NIS+ 更新模型

将使用以下语法为 `esg.eng.starlight.com.` 目录的组添加读取和修改权限。

```
oak% nischmod g+rm esg.eng.starlight.com.
```

请参 `nischmod(1)` 手册页获取更多信息。参见第 148 页的“NIS+ Commands”获取 NIS+ 命令列表。

一旦设置，表对象的访问权限定义了该表对象的安全性。使表中的条目或列更安全的唯一方法是更改表对象本身的访问权限。然而，你可以通过将权限扩展到额外的主体或为现有主体提供额外的访问权限，来对表对象存储的信息提供额外访问。

例如，你的公司可能有一项策略，允许公司内的任何人创建、修改或删除特定电子邮件别名的条目。对所有别名的访问被限制为别名表的所有者。要实现这一点，你需要为别名表本身创建最严格的权限 (`---rmcdmr---r--`)，并对包含特定别名的条目授予自由访问 (`rmcdmcdrmcdmcd`)。

你可以使用 `nistbladm` 命令在创建表时设置表的访问权限，在创建条目时设置条目和列的访问权限，或修改现有表的访问权限。请参阅 `nistbladm(1)` 手册页获取更多信息。

# NIS+ 更新模型

NIS+ 更新模型比 NIS 更新模型更可靠、更高效。NIS+ 在主服务器上存储目录的主副本。零或多个副本服务器存储主副本的副本。当你使用 NIS+ 命令管理 NIS+ 时，更改仅在主服务器的目录上进行。当主服务器接收到对象的更新（无论是目录、组、链接还是表）时，服务器会等待约两分钟以等待其他更新以便捕捉更新。等待期结束后，服务器将更新存储在磁盘和事务日志中，并进行传播。与 NIS 更新在大型组织中通常需要一天或更长时间才能传播不同，NIS+ 增量更新会自动并快速地传播到副本。

NIS+ 更新模型能够更高效地利用网络带宽，因为只有更改从主服务器传输到副本。如果副本已过时，它们可以请求更新的信息。

NIS+ 事务日志模型提供了回滚恢复和 NIS+ 数据库的一致性，即使服务器在更新期间发生故障。NIS+ 主服务器和副本服务器可以使用事务日志将数据库自动修复到故障发生之前的状态。

## NIS 与 NIS+ 的兼容性

NIS+ 提供了一种 NIS 兼容模式。这种模式让运行在 Solaris 操作系统环境下的 NIS+ 服务器能够回答来自 NIS 以及 NIS+ 客户端的请求。在设置好 NIS+ 服务器后，你可以选择 NIS 兼容模式。你不需要对 NIS 客户端进行任何额外的设置或更改。NIS+ 兼容模式是一种允许你逐渐从 NIS 过渡到 NIS+ 的模式。

主服务器与从服务器之间的比较如下：NIS 主服务器仅通过 NIS 从服务器感知；NIS 不知道 NIS+。NIS+ 主服务器仅与 NIS+ 副本服务器交互。NIS+ 不会将 NIS+ 表转换为映射（maps）并将其推送到 NIS 从服务器。

## 命名服务切换

Solaris 提供了 `/etc/nsswitch.conf` 命名服务切换文件，你可以利用它定制单个系统的命名服务策略，以便在 Solaris 环境中使用多个命名服务。你可以通过 `/etc/nsswitch.conf` 文件指定以下配置：

- 对于每种配置信息（如密码或主机 IP 地址），使用哪些命名服务。
- 对于每种信息，使用不同命名服务的顺序。
- 当未找到信息或命名服务不可用时继续搜索的标准。

你可以使用 `/etc/nsswitch.conf` 文件为命名服务的使用设置灵活的策略，并在站点需求变化后描述并更改这些策略。例如，运行 Solaris 环境的系统可以从 DNS 获取其主机信息，其组

## 名称服务切换 (Nameservice Switch)

信息来自 NIS 映射，而其密码信息来自本地的 `/etc/passwd` 文件。

`/etc/nswitch.conf` 文件还简化了从 NIS 迁移到 NIS+ 的过程，因为 Solaris 1.x 和 Solaris 2.x 系统可以作为 Solaris 1.x NIS 服务器的客户端。此外，Solaris 2.x 系统可以同时作为 NIS 和 NIS+ 的客户端，使得这两个系统可以在过渡期间共存。如果你更改了域名，NIS/NIS 域名通常（但并非总是）与 DNS 域名相同。

> **新注意。** Solaris 8 操作系统支持 `/etc/nsswitch.conf` 名称服务切换文件中的打印机数据库。打印机数据库为网络上的打印客户端提供中心化的打印机配置信息。通过打印机数据库和名称服务文件中的相应信息源，打印客户端可以自动访问打印机配置信息，而无需将其添加到自己的系统中。当您向系统添加打印机时，Solaris 打印管理器会配置打印机数据库。

当您安装 Solaris 操作系统时，`/etc` 目录包含一个默认的 `nswitch.conf` 文件以及 `nswitch.files`、`nswitch.nis` 和 `nswitch.libs`。Solaris 8 版本还提供了 `nswitch.dns` 和 `nswitch.ldap`，它们为这些可能的名称服务信息源（文件、NIS、NIS+ 和 LDAP）提供了默认设置。默认的 `nswitch.nis` 文件所示。

```
#
# /etc/nswitch.nisplus:
# 一个可以复制到 /etc/nswitch.conf 的示例文件；它
# 结合文件使用 NIS+ (NIS 第 3 版本)。
# 此文件中的 'hosts:' 和 'services:' 仅在
# /etc/netconfig 文件中针对 "inet" 传输的 nameaddtr_libs 为 "-" 时才使用。
# 以下两行偏离了 /etc/passwd 和 /etc/group 中的 "-" 条目。
password: files nisplus
group: files nisplus
# 查询 /etc 文件，仅当 nisplus 无法用时。
# nisplus [NOTFOUND-return] files
ipodes: files
# 取消下行的注释并注释掉上方行，以便
# 从 ipodes 数据库中搜索所有 IPv4 和 IPv6 地址。注意
# 在搜索主机名之前，会在所有 ipodes 数据库中搜索
# IPv4 地址。要开启此选项，请咨询
# 《网络管理指南》有关使用 IPv6 的更多细节。
# nisplus [NOTFOUND-return] files
# 取消下行的注释并注释掉上方行，以同时使用 DNS
# 和 NIS+。
# 服务查找：对 /etc/resolv.conf 进行 DNS 名称
# 见 resolv.conf(4)
# nisplus dns [NOTFOUND-return] files
# services: nisplus [NOTFOUND-return] files
networks: nisplus [NOTFOUND-return] files
protocols: nisplus *1* files
```

# 146 介绍 NIS+ 环境

```
rpc:      nisplus [NOTFOUND=return] files
ethers: nisplus [NOTFOUND=return] files
netmasks: nisplus [NOTFOUND=return] files
bootparams: nisplus [NOTFOUND=return] files
```
