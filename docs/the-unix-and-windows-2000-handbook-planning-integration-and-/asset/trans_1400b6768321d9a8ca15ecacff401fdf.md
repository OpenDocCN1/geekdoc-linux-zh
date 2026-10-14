
## 网络信息系统

网络信息系统（NIS）由 Sun Microsystems 开发，用于辅助分布式网络的管理。NIS 提供对 UNIX 工作站所使用的配置文件的集中控制。随后出现了 NIS+，其功能更加丰富。然而，NIS+ 并非在所有主流 UNIX 操作系统上都能运行，因此 NIS 仍被广泛使用。我们将首先介绍 NIS，然后再提供 NIS+ 的相关信息。

NIS 中使用的配置文件被分组到域中。选择 NIS 域名时遵循的一个简单规则是使用你的 DNS 域名。NIS 分发的最常见配置文件总结在表 7.1 中。

| 表 7.1 NIS 文件和映射 |
| 文件 | 信息 | 映射 | DBM 文件 |
| /etc/passwd | 用户 ID、组 ID、密码、名称、Shell、主目录 | Passwd.byname Passwd.byuid | Passwd.byname.dir Passwd.byname.pag Passwd.byuid.dir Passwd.byuid.pag |
| /etc/group | 按用户 ID 列出的组和成员 | Group.by gid Group.by name | Group.by gid Group.by gid.pag Group.by name.dir Group.by name.pag |
| /etc/hosts | 主机名和 IP 地址 | Hosts.byaddr Hosts.by name | Hosts.byaddr.dir Hosts.byaddr.pag Hosts.by name.dir Hosts.by name.pag |
| /etc/networks | 名称和 IP 地址 | Networks.byaddr Networks.by name | Networks.byaddr.dir Networks.byaddr.pag Networks.by name.dir Networks.by name.pag |
| /etc/services | 服务名称、端口号/协议 | Services.by name | Services.by name.dir Services.by name.pag |
| /etc/protocols | 官方协议名称、协议编号和别名 | Protocols.by name Protocols.by number | Protocols.by name.dir Protocols.by name.pag Protocols.by number.dir Protocols.by number.pag |
| netgroup | 主机名、用户名和域名 | Netgroup.by host Netgroup.by user | Netgroup.by host Netgroup.by user |

NIS 将文本文件中包含的信息转换为 NIS 映射。这些映射源自 DBM 数据库文件。DBM 数据库文件由一个键值和与该键关联的信息组成。信息查找通过匹配键值来完成。某些配置文件包含需要生成具有不同键值的多个映射的信息。passwd 文件就是一个很好的例子。UNIX 提供了两个函数来查找用户信息。一个函数使用用户的登录名，另一个函数使用用户的 ID（UID）。NIS 为 passwd 文件生成两个映射，键值分别为登录名（passwd.byname）和 UID（passwd.byuid）。DBM 数据库文件实际上由两个文件组成。哈希索引文件具有 .dir 扩展名，数据文件具有 .pag 扩展名。与顺序扫描 ASCII 文件相比，这可以更快地查找信息。

NIS 使用客户端/服务器模型来分发信息。有一个主服务器在本地文件系统上维护该域的主配置文件（主服务器可以服务多个域）。NIS 映射位于主服务器上的 /var/yp 目录下。对配置文件进行更改后，在 /var/yp 目录中执行 make，为所有更改的文件构建新映射并推送到从服务器。从服务器可以从主服务器“推”域映射，也可以从主服务器“拉”映射。客户端“绑定”到服务器（主服务器或从服务器），并查询服务器以获取映射中包含的信息。

接下来的几节将介绍 NIS 管理的重要基础知识。我们将假设示例网络中未运行 NIS。第一节将介绍设置 NIS 主服务器所需的步骤。第二节将介绍从服务器的创建。第三节将介绍 NIS 客户端的设置并解释绑定过程。最后一节将介绍重要的 NIS 命令。

## NIS 主服务器的创建

NIS 主服务器的安装将分三个步骤介绍。第一步是初始化主服务器的 NIS 映射。第二步是启用 rpc.ypasswdd 守护进程。最后一步是确保 NIS 服务在启动时自动启动。

### 初始化

第一步是仔细选择你的主服务器。这一过程在本章前面已经介绍过。你还需要知道从服务器的名称。NIS 映射基于 UNIX 用来辅助启动过程和限制工作站访问的配置文件。ypinit 或 ypfiles 的手册页包含了将生成 NIS 映射的文件列表。
