
## 备份架构

在虚拟化策略中，采用利用虚拟化系统（Linux）和主机系统（z/VM）特性的技术可以结合了这两者的优点。利用 CP、CMS 和 Linux 自有的功能可以实现极佳的复制方法。此处显示的方法适用于 EXT2 或 EXT3 文件系统。如果您正在使用 Oracle ASM 文件系统，则必须考虑其他因素。本节不涵盖 ASM 相关问题。虽然缺乏某些功能（例如执行 Linux 文件层级归档的能力），但在 z/OS 系统的辅助下进行备份和恢复是 z/VM 和 Linux 部署中的一种流行选择。许多 z/VM 环境对磁带驱动器、磁带库或机器人磁带系统的访问有限（或没有）。

许多 z/VM 和 Linux 部署已经拥有运行 z/OS 的现有主机，并配备了备份/恢复软件、程序和策略。

z/OS 有两种配置可以访问由 z/VM 系统拥有的 DASD：

1. 一个 z/OS LPAR 与 z/VM LPAR(s) 位于同一个 CEC 中。z/OS LPAR 通过 IOCDS 编码访问 z/VM DASD。

2. z/VM LPAR(s) 和 z/OS LPAR 位于不同的 CEC 上。在这种情况下，DASD 存储单元本身双路连接到两个 CEC。每个 CEC 的 IOCDS 编码均配置为查看同一个 DASD。

一个拥有 Oracle 虚拟机的大型客户使用了两个独立 CEC 的配置。第 143 页的图 7-8 显示了备份架构。

![](img/5b458d26d6ded58c4d2c82af59a3d71c_164_0.png)

图 7-8 备份架构

备份的步骤为：

1. z/VM LPAR 中的 CMS 服务机在预设时间从远程系统以 root 用户身份向每台 Linux 机器发布控制台命令。远程系统是一个服务 LPAR。

   - a. 服务机 `SIGBKUP` 由基于计时器的程序作为 `WAKEUP` 启动。

   - b. 使用 CP 次级控制台输入功能，通过 `CP SEND` 命令向每个待备份的 Linux 客户发布命令。

2. Linux 机器处理控制台命令 `PREFLASH`。`PREFLASH` 是一个 `bash` 脚本：

   - a. 静置 Oracle。每周一次通过 `dbora stop` 停止数据库。其他时间，执行热备并使用 `alter database begin backup` 命令停止数据库。

     > 注意：在使用 `alter database begin backup` 静置 Oracle 且数据库使用 ext3 文件系统跨越多个柱面卷时，存在一个极短的 I/O 不一致窗口。数据库有可能无法恢复到良好状态。然而，在这种情况下，使用 `alter database suspend` 代替 `alter database begin` 将提供一个干净的环境。

   - b. 多次执行 `sync` 命令。在每台机器上多次执行 `sync` 命令以确保磁盘已更新。Linux 会在内存中缓存文件更新，`sync` 命令可以将内存缓冲的任何数据写入磁盘。

3. 服务 LPAR 上的 CMS 服务器机现在将：

   - a. 连接到包含 Linux 虚拟机 minisk 的所有 DASD 的完整卷。包含生产机器 Oracle 数据的 minisk 每天备份一次。包含可执行文件等系统数据的 minisk 备份频率较低（更改率低）。

   - 备份由机器池（即生产、开发、实验室等）完成。

   - c. 链接到完整卷的目标部分。

   - c. 从柱面 1 到最后一个柱面从源卷到目标卷执行 `FLASHCOPY`。`FLASHCOPY` 不需要柱面 0，因为没有 minisk 起于柱面 0，通过这种方式可以保留目标卷上的标签。

对属于 Linux 机器的每个 minisk 进行查找，并准备一份完整卷列表。`SIGBKUP` 连接到虚拟地址为 `380E` 的源 `SYSDUMP1` minisk，以及 `388E` 的目标。示例 7-13 显示了该列表。

### 示例 7-13 minisk 列表

| `VPCX81 380E` | 3390 | `SYSDUMP1` | 0 | 3338 | 3339 | `FC380E` | `ZODNXX1` | `CPCMS` |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
