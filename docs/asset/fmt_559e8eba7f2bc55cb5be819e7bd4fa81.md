
#### 8.4.2 HACMP 配置

在本节中，我们简要讨论了 `HACMP` 实施之前的规划阶段。在本节中，我们将介绍在共享磁盘集群配置中实际设置 `HACMP` 的概述。有关更多详细信息以及设置 `HACMP` 和 `DB2` 的逐步指南，请参考以下文档：

- `IBM DB2 Universal Database Edition for AIX and HACMP/ES` `ftp://ftp.software.ibm.com/software/data/paps/papers/db2exe-aihacmp.pdf`
- `DB2 UDB V8.1 ESE and high availability on AIX with HACMP 4.4.1: A mutual scenario` `http://www.ibm.com/developerworks/db2/library/techarticle/dm-0407nikoloulou/`

##### 检查网络连接

以下是涉及 `AIX` 逻辑卷的一些术语：

- 卷组（`VG`）
- 逻辑卷（`LV`）
- 日志文件系统（`JFS`）
- 文件系统（`FS`）

执行以下步骤来设置共享磁盘资源：

1. 检查两个节点的网络接口上是否配置了 `IP` 地址。
2. 检查 `/etc/hosts` 文件是否包含所有 `IP` 地址条目，且这些标签被 `HACMP` 使用。
3. 使用 `host` 命令验证名称解析是否正常。如果有问题，请检查并修改 `/etc/hosts` 文件。
4. 检查串口网络连接。

配置共享磁盘的：

- 卷组（`VG`）
- 逻辑卷（`LV`）
- 日志文件系统（`JFS`）
- 文件系统（`FS`）
