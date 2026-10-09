

3. `# mksysb /dev/rmt0` 创建备份。
4. `# chdev -l rmt0 -a block_size=<blocksize>` 重置磁带块大小。

# 分布式系统安装

如果安装或更新单个系统还不是足够的问题，那么想象一下在多系统环境中反复执行这一过程吧！在许多情况下，这些系统既代表磁盘配置，也代表非磁盘配置。

# NFS 安装支持

在具有现有 AIX 系统的网络环境中，将产品和维护映像复制到文件系统 `/inst.images`。通过 NFS 将此文件系统导出到每个远程站点。此方法需要在每台机器上重复安装过程。它提供了在每个系统上自定义更新的能力。

# 创建参考系统

为了减少更新多个磁盘系统所需的时间和精力，可以创建一个单一的参考系统映像，以便在每台机器上进行克隆。

1. 更新并调整一个代表基础配置的系统。
2. 将您不想备份的文件系统列表放入 `/etc/exclude.rootvg` 文件中，并使用 `-i` 和 `-e` 选项运行 `mksysb`。

   ```bash
   # echo /inst.images >> /etc/exclude.rootvg
   # mksysb -i -e /inst.images/image_name
   ```

3. 在非网络环境中，将 `mksysb` 输出定向到可移动媒体。如果可用的网络访问，则将输出映像定向到文件系统 `/inst.images`。
4. 在支持 NFS 和 TCP/IP 的网络环境中创建网络安装管理器。

# 网络安装管理器 (NIM)

网络安装管理器（NIM）促进了分布式网络环境中所有参与 AIX 机器软件安装和维护的中心化管理。这作为介绍词怎么样？NIM 还可以远程自定义、启动并在每个 NIM 管理的工作站上运行诊断。NIM 基于 IP，使用 BOOTP、TFTP 和 NFS 协议向每个 NIM 客户端分发引导映像和软件。NIM 可用于任何支持 TCP/IP 协议的网络，并支持中央服务器上的多种网络接口类型。正如你可能猜到的那样，NIM 是一个非常复杂的工具，但有一个 Easy Setup SMIT 选项，它使用最常见的配置进行设置，即 `smitty nim_config.env`。Easy Setup 非常好，但对于新手来说，我们需要添加更多细节来入门。

1. 首先，在运行 `smitty nim_config.env` 之前创建 `/tftpboot` 文件系统。
   要创建 `/tftpboot` 文件系统并安装 NIM 软件，请使用以下命令序列：

   ```bash
   # mkivs -y 'lv' rootvg 1
   # crfs -v jfs -d lv -m /tftpboot -A yes
   # mount /tftpboot
   # chfs -a size=120000 /tftpboot
   # df -k /tftpboot
   # installp -qaX -d <device> bos.sysmgt.nim.master
   bos.sysmgt.nim.spot
   # smitty nim_config.env
   ```

2. 使用上述命令序列创建 `/tftpboot` 文件系统并安装 NIM 文件集。

   ![](img/82f851021955589d82b22750fb3b1646_124_0.png)

3. 使用 `smitty nim_config.env` 从 CD-ROM 配置 NIM 主节点。

   ![](img/82f851021955589d82b22750fb3b1646_125_0.png)

4. 使用 `smitty nim_mac` 定义客户端机器。
5. 使用 `smitty nim_res` 创建 `mksysb` 映像并定义 `mksysb` 资源。
6. 使用 `smitty nim_bosinst` 从 `mksysb` 映像安装独立客户端。
7. 启动客户端。

   ![](img/82f851021955589d82b22750fb3b1646_125_1.png)

NIM 环境由两种系统类型组成：NIM 主节点和一个或多个 NIM 客户端。NIM 主节点集中协调网络中所有 NIM 客户端的管理功能。主服务器必须是一个独立的工作站，具有足够的存储资源，为所有受管客户端提供引导映像和共享产品对象树（SPOT）。NIM 主服务器必须安装 NIM 运行所需的 AIX 网络和管理员（spmgr）文件集。每组客户端只有一个 NIM 主节点。NIM 客户端可以是任何无盘、无状态和独立工作站的混合，只要它们与 NIM 主节点有网络连接即可。

NIM 支持三种类型的客户端：

- **独立（Stand-alone）**：具有本地 AIX 和 LPP 副本的机器
- **无盘（Diskless）**：网络文件系统、分页和转储；用于网络引导的引导 ROM
- **无状态（Stateless）**：网络文件系统；本地分页和转储；用于网络引导的引导 ROM；性能优于无盘配置

组成 NIM 支持的 AIX 文件集打包在 `bos.sysmg` 中。`bos.sysmg.nim.master` 文件集用于构建 NIM 主服务器。`bos.sysmg.nim.client` 文件集安装在每个独立的 NIM 客户端上。文件集 `bos.sysmg.nim.spot` 用于为 NIM 无盘和无状态客户端类型创建 SPOT 文件集。

NIM 主节点将识别每个受管客户端和网络类型所需的信息作为对象存储在 ODM 数据库中。这就是管理 NIM 环境时大部分难点所在。提供了用于列出、更新和验证 NIM ODM 对象及关系的命令；但在实践中，处理 ODM 并不像操作人类可读的表那样简单直接。NIM 主节点必须维护将机器对象链接到网络对象、网络对象链接到网络对象（路由）以及机器对象链接到机器对象的关系。用于更新和验证 NIM ODM 对象及关系的常用 NIM 命令包括 `nim`、`nimconfig`、`nimrelclient` 和 `lsnim`。

我的建议是使用 SMIT 来配置和管理 NIM；你可以使用基于 Web 的系统管理器，但它是一个 java 资源消耗大户，使用速度非常慢。SMIT 面板在提醒你所有必须与 NIM 对象关联的属性方面做得好得多，以确保维持正确的对象间关系。尽管可以使用 `lsnim` 快速检查 ODM 内容，但其余操作请使用 SMIT。在以下关于设置 NIM 环境的讲解中，我将使用 SMIT。

# 信息和支持

- 1-800-CALL-AIX
- 1-800-IBM-4FAX
- 1-800-237-5511

# 问题支持

| 命令 | 描述 |
|---|---|
| `IBMink.advantis.com` | Internet 远程终端 `IBMLink` |

# 维护级别和历史

| 命令 | 描述 |
|---|---|
| `oslevel` | AIX `3.2.4+` 版本和发行级别 |
| `uname -v -r` | 显示版本和发行级别 |
| `lslpp -a -h <product>` | 列出维护历史 |

# 打包

| 命令 | 描述 |
|---|---|
| 文件集 (Fileset) | 特定功能软件集 |
| 包 (Package) | 通用功能文件集 |
| 授权产品 (Licensed product) | 发行包集合 |
| 捆绑 (Bundle) | 文件集、包和维护的分组 |

# 备份 rootvg

| 命令 | 描述 |
|---|---|
| `mksysbfile` | 为 `mksysb` 创建 image.data 文件 |
| `mksysb /dev/rmt0/<t>` | 将 rootvg 备份到磁带 |

# 维护安装

| 命令 | 描述 |
|---|---|
| `smit install` | 基本安装面板 |
| `smit install_latest` | 选择性安装面板 |
| `smit install_all` | 安装所有产品 |
| `bfbcreate -qv -d <media> -f <disk-path>` | 将维护复制到磁盘 |
| `installp -qa -d <media-path> -X all` | 应用 (APPLY) 更新 |
| `installp -r8 -X all` | 拒绝 (REJECT) 更新 |
| `installp -c -g -X all` | 提交 (COMMIT) 更新 |
| `installp -u <fileset>` | 卸载 (DEINSTALL) 文件集 |
| `installp -C <fileset>` | 清理 (CLEAN UP) 失败的安装 |

# NIM 相关

| 命令 | 描述 |
|---|---|
| `smit nimconfig` | 配置并启动 NIM 主节点 |
| `smit nim_mknet` | 创建 NIM 网络对象 |
| `smit nim_mkroute` | 定义 NIM 网络路由 |
| `smit nim_mkmac` | 创建客户端网络对象 |
| `smit nim_mkres` | 创建 lpp_source |
| `smit nim_alloc` | 创建 bos.inst 资源 |
| `lsnim` | 列出 NIM 定义的对象 |
| `bootinfo -q` | 检查 IPL ROM 仿真 |
| `bosboot -r` | 创建 IPL ROM 媒体 |
| `smit nim_alloc` | 在客户端创建 bos_inst 资源 |
| `smit nim_perms` | 设置主节点推送权限 |
| `smit nim_mac_op` | 选择客户端和资源 |
| `smit nim_mkgrp` | 创建 NIM 客户端组 |
| `smit bos_inst` | 推送安装独立客户端 |
| `smit nim_install` | 从客户端拉取安装 |
| `smit dksl_init` | 初始化无盘客户端 |
| `smit nim_mac_op lpchck` | 验证安装 |
| `smit nim_backup_db` | 备份 NIM 配置 |
| `smit nim_restore_db` | 恢复 NIM 配置 |
| `smit nim_client_op` | 远程操作 NIM 客户端 |
| `smit nim_unconfig` | 取消配置 NIM 主节点 |

# 检查清单

以下是安装和维护要点的检查清单：

- 每次安装 AIX 时，请仔细遵循安装指南。
- 配置操作系统和生产文件系统，以从磁盘空间中获得最佳性能。
- 如果您正在安装全新的 P-Series 或 RISC System/6000，请预安装基础操作系统（BOS）和产品运行时环境的一部分。
- 通过使用 SMIT 安装快速路径（FastPath）或使用 `installp` 命令来管理授权程序产品（LPP）的安装。
- 监控非 LPP 产品的安装。
- 当系统不再需要某个应用程序时，您可以通过 SMIT 软件维护实用程序将其移除。
- 应用维护级别（ML）补丁。
- 为新安装设置默认的系统和环境变量。
- 识别分布式系统安装步骤。
- 识别 DocSearch 关键字。
- 识别软件安装/维护信息和支持程序。

