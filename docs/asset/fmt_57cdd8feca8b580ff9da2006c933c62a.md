
- d. `/etc` 文件

## 问题 26

以下哪项是虚拟文件系统的名称，该文件系统由多个以交错方式分配和使用的分区组成？

- a. RAID 1
- b. 条带化
- c. 串联
- d. 热备用

## 问题 27

以下哪些是可以在 `/etc/syslog.conf` 文件中指定的有效操作？（请选择所有适用的选项。）

- ☐ a. 文件名
- ☐ b. 感叹号（`!`）
- ☐ c. 主机名
- ☐ d. 用户帐户名

## 问题 28

以下哪些命令可用于确定共享的 NFS 资源？（请选择所有适用的选项。）

- ☐ a. `share`
- ☐ b. `dfmounts`
- ☐ c. `dfshares`
- ☐ d. `mountall`
- ☐ e. `mount`

## 问题 29

以下哪项是生成用于创建 NIS 映射的数据文件的最佳过程？

- ○ a. 编辑 `/etc` 文件以删除 NIS 不需要的任何信息。
- ○ b. 将 `/etc` 文件复制到某个目录，并清理该副本以用于构建 NIS 映射。
- ○ c. 使用 `makedbm` 命令创建一组新的数据文件。
- ○ d. 对每个映射运行 `buildmap` 命令，并在提示时输入相应的数据。

## 问题 30

指出 Custom JumpStart 安装用来定义系统或系统组在安装时应使用哪个配置文件的文件。

## 问题 31

输入用于描述将数据写入多个磁盘以提高性能并克服磁盘限制这一技术的术语。

## 问题 32

指出用于创建 CacheFS 日志的命令。

## 问题 33

指出用于使 NFS 资源无法挂载的命令。

## 问题 34

输入用于向 RBAC 数据库添加角色的命令的名称。

## 问题 35

Solaris 8 操作系统支持五种类型的名称服务。其中四种是 `/etc` 文件、DNS、NIS 和 NIS+。请输入第五种名称服务的名称。

## 问题 36

以下哪项是 syslog 消息最严重的级别？

- a. alert
- b. notice
- c. emerg
- d. crit

## 问题 37

以下哪条命令用于配置 NIS 主服务器？

- a. `ypinit -m`
- b. `ypinit -c`
- c. `ypinit -s`
- d. `nisclient`
- e. `nisinit -c`

## 问题 38

在系统引导期间或使用 `mountall` 命令时，哪个文件用于自动挂载 NFS 资源？

- a. `/etc/dfs/dfstab`
- b. `/etc/vfstab`
- c. `/etc/mnttab`
- d. `/etc/dfs/sharetab`

## 问题 39

以下哪个路径名与卷管理器相关联？

- a. `/dev/dsk`
- b. `/dev/vx/dsk`
- c. `/dev/md/dsk`
- d. `/dev/ds/dsk`

## 问题 40

指出包含域中系统以太网地址的 NIS+ 表的名称。

## 问题 41

说出用于添加新 NIS 映射的命令的名称。

## 第 42 题

你使用 `domainname` 命令通过 `/etc` 文件为系统设置域名，但系统重启后域名丢失。为什么？

- a. 域名必须在每次重启后重新输入。
- b. 你没有使用 `-p` 命令行参数使域名永久生效。
- c. 你忘了编辑 `/etc/defaultdomain` 文件并输入域名。

## 第 43 题

哪个 `/etc` 文件包含一份服务器（及路径）列表，这些服务器为网络/安装客户端提供引导、根和交换区域？

- a. bootparams
- b. ethers
- c. timezone
- d. hosts
- e. vfstab

## 第 44 题

指出可以使用 Web 浏览器访问 NFS 资源的与 NFS 相关的协议。

## 第 45 题

下列哪个命令用于检查和修复文件系统？

- a. `mount`
- b. `newfs`
- c. `fsck`
- d. `format`

## 第 46 题

在下列哪个系统运行级别下会启动 NFS 服务器程序？（选择所有适用的项）

- [ ] a. 0
- [ ] b. s
- [ ] c. 2
- [ ] d. 3
- [ ] e. 6

## 第 47 题

下列哪些是 Solaris 8 软件组？（选择所有适用的项）

- [ ] a. 完整发行版
- [ ] b. 完整发行版加 OEM 系统支持
- [ ] c. 最终用户支持
- [ ] d. 开发人员系统支持

## 第 48 题

说出支持单点登录的图形化管理工具的名称。

## 第 49 题

下列哪些功能包含在 Volume Manager 中但不包含在 DiskSuite 中？（选择所有适用的项）

- [ ] a. 图形化管理工具
- [ ] b. 命令行实用程序
- [ ] c. 性能分析工具
- [ ] d. 动态在线调整

## 第 50 题

输入与 `setup_install_server` 命令一起用来设置引导服务器的命令行参数。

## 第 51 题

输入用于配置 syslog 设施的文件名。

## 第 52 题

下列哪项不是 AdminSuite 提供的工具？

- a. 数据库管理器
- b. 存储管理器
- c. 网络客户端管理器
- d. 串行端口管理器

## 第 53 题

哪个文件应始终包含当前共享的 NFS 资源？

- a. `/etc/nfs/nfstab`
- b. `/etc/nfs/shares`
- c. `/etc/dfs/dfstab`
- d. `/etc/dfs/sharetab`

## 第 54 题

下列哪个路径名与标准 Solaris 文件系统相关联？

- a. `/dev/dsk`
- b. `/dev/vx/dsk`
- c. `/dev/md/dsk`
- d. `/dev/ds/dsk`

## 第 55 题

指出用于捕获并记录来自系统组件和用户程序的消息的设施。

## 第 56 题

下列哪些是可以在 profile 或 class 文件中定义的关键字？（选择所有适用的项）

- [ ] a. `install_type`
- [ ] b. `cluster`
- [ ] c. `package`
- [ ] d. `system_type`

## 第 57 题

下列哪些安装客户端使用简单文件传输协议（Trivial FTP）通过网络获取可引导映像？（选择所有适用的项）

- [ ] a. 仅 Intel 客户端
- [ ] b. 仅 SPARC 客户端
- [ ] c. Intel 和 SPARC 客户端均可
- [ ] d. 与安装服务器不在同一子网上的任何客户端

## 第 58 题

按从高到低的顺序排列 TCP/IP 网络模型的五层。

- a. 1. 网络层或网际层
- b. 2. 数据链路层
- c. 3. 物理层
- d. 4. 应用层
- e. 5. 传输层

## 第 59 题

为了支持故障转移，应在 `/etc/fstab` 文件中指定下列哪些 NFS 挂载选项？（选择所有适用的项）

- [ ] a. 只读（`ro`）
- [ ] b. 读写（`rw`）
- [ ] c. 不允许中断（`nointr`）
- [ ] d. 公布为公共资源（`public`）

## 第 60 题

指出 `share` 命令中用于允许远程 root 访问 NFS 共享资源的命令行参数。

## 第 61 题

下列哪些与交换空间相关的操作可以由 `swap` 命令执行？（选择所有适用的项）

- [ ] a. 创建交换空间
- [ ] b. 添加交换空间
- [ ] c. 列出交换空间
- [ ] d. 删除交换空间

## 参考答案 II

![](img/b957f979417d9f16274c2eb52c8f2c9f_483_0.png)

1. `add_to_install_server`
2. a, b, c, d
3. c
4. a
5. a, b, c, d
6. b
7. a, c
8. a
9. NFS 客户端
10. a-7, b-4, c-2, d-5, e-1, f-6, g-3
11. b, d
12. a, b, c
13. a, b, c, d
14. a, b, c, d, e
15. c
16. c, f
17. a, b, d
18. c
19. c
20. 表
21. b, d
22. d
23. a, c
24. a, c, d
25. c
26. b
27. a, c, d
28. a, c
29. b
30. 规则
31. 条带化
32. cachefslog
33. unshare
34. roleadd
35. FNS
36. c
37. a
38. b
39. b
40. ethers
41. makedbm
42. c
43. a
