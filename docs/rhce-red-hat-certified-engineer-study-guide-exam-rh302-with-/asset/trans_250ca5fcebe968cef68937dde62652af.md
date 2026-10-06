

# 更多信息

关于 TCP wrappers 的更多信息，请参阅 man 页面 hosts_access (5) 和 hosts_options (5)。现在，请通过完成练习 22.2 来了解 TCP wrappers 的工作原理。

# 练习 22.2

## 指定 TCP Wrappers

TCP wrappers 是网络安全策略中的重要元素，通常应为连接到非本地网络的主主机实施。要查看 TCP wrappers 如何工作，请执行以下步骤：

- 1. 指定一个拒绝对本地主机 telnet 访问的 TCP wrapper。验证来自本地主机的访问是否被拦截，但在其他地方未被拦截。
- 2. 指定一个拒绝对本地主机以外其他主机 telnet 访问的 TCP wrapper。验证来自本地主机的访问未被拦截，但在其他地方被拦截了。

在执行所需的操作时，你可以参考相关章节和其他资源。但是，在参加 RHCE 考试之前，请确保你能够在不借助此类帮助的情况下实现 TCP wrappers。

# 网络信息服务 (NIS)

NIS 的安全性并不高；例如，访问 NIS 服务器的用户可以获取服务器 NIS 映射（maps）的完整内容。Sun 的 NIS+ 设施更安全。然而，红帽 Linux 仅支持 NIS+ 客户端；不支持 NIS 服务器。

与 NIS 相关的红帽软件包 (RPM) 为有：

- ybind，NIS 客户端
- ypserv，NIS 服务器
- yp-tools，有用的 NIS 工具和实用

此外，NIS 需要 portmap 服务。文件 /etc/nsswitch.conf 指定了 NIS 配置。NIS 服务器在 /var/yp/domain 中存储关于域的信息；NIS 客户端在 /var/yp/binding 中存储信息。
你可以轻松判断一个主机是否由 NIS 管理。执行命令

domainname

如果该主机是 NIS 域的一部分，该命令将报告域的名称。

# NIS 命令

在 NIS 客户端使用的最重要的命令和程序中：

- ybind: 查找 NIS 信息并存储在 /var/yp/binding
- ypwch: 返回 NIS 服务器名称
- ypcat: 打印指定映射中的键
- yppoyll: 打印指定映射的版本号，并识别该映射所在的服务器
- ypmatch: 打印指定映射的选定键
- yppassword: 修改 NIS 密码

在 NIS 服务器使用的最重要的命令和程序中有：

- ypserv: NIS 守护进程的可执行名称
- makedbm: 从文本文件创建映射数据库
- yppush: 通知从服务器映射更新
- yppasswdd: 处理 NIS 密码更改的守护进程有关这些命令的更多信息，请参阅相关的 man 页面。

# NIS 配置

主要的 NIS 配置文件是 /etc/nsswitch.conf。以下是该文件随红帽 Linux 分发的的内容：

```
# /etc/nsswitch.conf
## 一个示例名称服务切换配置文件。此文件
# 应该将最常用的服务排在
# 开头。
# 条目 '[NOTFOUND=return]' 意味着如果上一个条目的搜索
# 没有结果，则停止条目搜索。请注意，如果搜索是因为
# 其他原因失败（例如没有 NIS 服务器响应），
# 则搜索将继续到下一个条目。
# 合法的条目是：
```

```
# nisplus or nis      使用 NIS+ (NIS 版本 3)
# nis or yp            使用 NIS (NIS 版本 2),
#                      也称为 YP
# dns                  使用 DNS（域名
#                      服务)
# files                使用本地文件
# db                   使用本地数据库
#                      (.db) 文件
# compat               以兼容模式使用 NIS
# [NOTFOUND=return]    如果目前未找到
#                      则停止搜索
```

```
# 若要使用 db，将 "db" 放在 "files" 之前，对于
# 你希望在数据库中首先查找的条目
# 示例：
#passwd               db files nisplus nis
#shadow               db files nisplus nis
#group                db files nisplus nis
```

passwd: files nisplus nis
shadow: files nisplus nis
group: files nisplus nis

#hosts: db files nisplus dns
hosts: files nisplus dns

services: nisplus [NOTFOUND=return] files
networks: nisplus [NOTFOUND=return] files
protocols: nisplus [NOTFOUND=return] files
rpc: nisplus [NOTFOUND=return] files
ethers: nisplus [NOTFOUND=return] files
netmasks: nisplus [NOTFOUND=return] files
bootparams: nisplus [NOTFOUND=return] files

netgroup: nisplus

publickey: nisplus

automount: files nisplus
alias: files nisplus

第二个的 NIS 配置文件是 /etc/yp.conf。以下是 /etc/yp.conf 文件随红帽 Linux 分发的内容。

```
# /etc/yp.conf - ybind 配置文件
# # 有效条目为
#
#domain NISDOMAIN server HOSTNAME
# 为域 NISDOMAIN 使用 server HOSTNAME
#
#domain NISDOMAIN broadcast
# 为域 NISDOMAIN 使用 broadcast
#
#ypserver HOSTNAME
# 为域 NISDOMAIN 使用 server
# 服务器地址必须列在 /etc/hosts 中。
#

```除了注释行外，每行都命名了一个 NIS 映射并指定了获取键的来源。表 22.1 总结了 NIS 映射，表 22.2 总结了用于指定来源的关键字。

# 表 22.1 NIS 映射

| NIS 映射 | 默认共享 | 描述 |
| --- | --- | --- |
| aliases | no | 别名 |
| ethers | no | 以太网地址 |
| group | yes | 用户组 |
| hosts | yes | 主机名和 IP 地址 |
| netgroup | yes | 主机用户列表 |
| networks | yes | 网络名称和 IP 地址 |
| passwd | yes | 用户账户信息 |
| protocols | yes | 网络协议 |
| publicck | no | 用于 secure_rpc 的键 |
| rpc | yes | RPC 调用名称 |
| services | yes | 网络服务 |
| shadow | no | 密码 |

# 表 22.2 NIS 来源

| 来源 | 描述 |
| --- | --- |
| compat | 兼容旧版本标准库的 NIS |
| db | 本地数据库 |

# 表 22.2 NIS 来源（继续）

| 来源 | 描述 |
| --- | --- |
| dns | DNS |
| files | 本地文件 |
| nis | NIS |
| nisplus | NIS+ |

更多关于 NIS 的信息，请参见 NIS HOWTO，作者为 Thorsten Kukuk，/usr/doc/HOWTO/NIS-HOWTO。

# 轻量级目录访问协议 (LDAP)

轻量级目录访问协议 (LDAP) 提供了存储任意信息的数据库。因此，LDAP 可以用于多种用途。其中，在结合安全套层 (SSL) 时，LDAP 可以提供比 NIS 更安全的替代方案。例如，带有 SSL 的 LDAP具有加密数据传输和访问控制列表 (ACL)，用于指定哪些用户可以访问存储在 LDAP 数据库中的信息。与依赖刷新间隔来通知从服务器存储映射的变化不同，LDAP 可以更新推送到客户端。LDAP 包含在 openldap 软件包中，它提供了

slapd 运行在 389 端口的 LDAP 守护进程
slur 复制 LDAP 数据库的 LDAP 守护进程

主要的 LDAP 配置文件是 /etc/openldap/slapd.conf。有关 LDAP 的更多信息，请查看 /usr/doc/openldap-* 下的文件以及 LDAP 网站 www.openldap.org 上的可用文档。另查看以下与 LDAP 相关的页面：

- centipede
- chlog2replog
- edb21dif

