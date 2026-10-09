
## 14. 保护 Linux
### 使用 Tripwire 检测入侵
**数据文件：**
tripwire-2.4.1.2-src.tar.bz2

**开始之前**

1.  在 srvA 上，你已在命令行界面（CLI）中以 root 身份登录。
2.  显示第一个终端。
3.  在命令提示符下，输入 `cp /085039Data/Securing_Linux/tripwire-2.4.1.2-src.tar.bz2 /etc` 将 tripwire-2.4.1.2-src.tar.bz2 文件复制到 /etc 目录。
4.  输入 `cd /etc` 切换到 etc 目录。
5.  输入 `bunzip2 tripwire-2.4.1.2-src.tar.bz2` 解压该文件。
6.  输入 `tar -xvf tripwire-2.4.1.2-src.tar` 解包该文件。
7.  输入 `cd tripwire-2.4.1.2-src` 切换到 `/etc/tripwire-2.4.1.2-src` 目录。
8.  输入命令 `sed -i -e 's@TWDB="${prefix}@TWDB="/var@' install/install.cfg && ./configure --prefix=/usr --sysconfdir=/etc/tripwire && make` 将 Tripwire 数据库和报告安装到 `/var/lib/tripwire` 目录。
9.  输入 `make install && cp -v policy/*.txt /usr/doc/tripwire` 创建 Tripwire 安全密钥，安装二进制文件，并将 Tripwire 示例策略文件复制到程序的文档目录中。
10. 按 **Enter** 键查看协议。
11. 输入 *accept* 接受协议。
12. 输入 **y** 并按 **Enter** 键继续安装。
13. 如有必要，输入 **site#1** 作为站点密钥密码。
14. 如有必要，输入 **loc#1** 作为本地密钥密码。
15. 输入 **site#1** 作为站点密钥密码（输入两次）。输入 **y** 以覆盖 policyguide.txt 文件。
16. 清除终端屏幕。

**场景：**

你需要保护 /etc 目录中的配置文件，例如 initab、fstab、passwd 和 shadow。对这些文件的任何错误修改都可能损坏你的服务器，因为它们包含有关服务器的关键信息。因此，你希望特别小心，保护这些文件不被入侵者修改。

### 执行的操作

### 执行方法

1. 自定义 Tripwire 配置和策略文件。
   - a. 导航到 /etc/tripwire 目录。
   - b. 打开 twpol.txt 文件。
   - c. 定位以 “HOSTNAME” 开头的行。
   - d. 按 O 切换到插入模式并移至新行。
   - e. 输入 SIG_HI = 100; 定义一个新变量并为其赋值。
   - f. 按 Esc 切换到命令模式。
   - g. 搜索文本 rulename = “Tripwire Data Files”
   - h. 按 O 切换到插入模式并移至新行。
   - i. 在新行中，输入 severity = $(SIG_HI),
   - j. 输入 emailto = root ,
   - k. 按 Esc 切换到命令模式。
   - l. 保存并关闭文件。
   - m. 清除屏幕。
2. 运行配置脚本。
   - a. 输入 `twadmin --create-polfile --site-keyfile /etc/tripwire/site.key /etc/tripwire/twpol.txt` 以创建策略文件和密钥文件。
   - b. 输入 **site#1** 作为站点密钥密码。
   - c. 如有必要，再次输入站点密钥密码。
   - d. 如有必要，再次输入本地密钥密码。
   - e. 如有必要，输入站点密钥密码两次以签署配置和策略文件。
   - f. 观察策略文件是否已创建。
   - g. 更改 `twcfg.txt` 和 `twpol.txt` 文件的权限，以便只有你可以读取和修改这些文件。
3. 初始化 Tripwire 数据库。
   - a. 输入 `tripwire --init` 开始初始化数据库。
   - b. 输入 **loc#1** 作为本地密码。
   - c. 输入 `/usr/sbin/twprint -m d --print-dbfile` 创建数据库。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_739_0.png)

4. 使用 Tripwire 检查系统文件的完整性。
   - a. 运行 `tripwire` 程序并指定 `--check` 选项以创建报告。
   - b. 输入 `ls /var/lib/tripwire/report` 检查报告是否已创建。
   - c. 观察到显示扩展名为 `twr` 的文件。
   - d. 输入 `/usr/sbin/twprint -m r --twrfile /var/lib/tripwire/report/srvA-<yyyymmdd>-<hhmmss>.twr | less` 查看报告。
   - e. 查看完两页后，按 `q` 返回命令行。
   - f. 清除屏幕。

## 第 14 课 后续练习

在本课中，你考察了用于保护连接网络的 Linux 系统的各种选项。你配置了加密；保护了用户帐户；实施了 iptables 和安全审计；并检测了入侵。现在你将能够允许或限制用户访问网络资源，并通过有效保护机密数据来 safeguard 你的网络。

1. **你将使用哪种加密方法来保护数据？为什么？**
   *答案可能有所不同，但可能包括：要使用的加密方法取决于要传输数据的类型和敏感度以及通信模式。如果要在 Internet 上传输数据，必须使用适当的加密方法，例如密钥。*
2. **你将如何检测网络中的入侵？**
   *答案可能有所不同，但可能包括：通过实施入侵检测系统（IDS），如 Tripwire、Snort 或 Nessus。*

# 15 管理硬件

课时：2 小时 10 分钟

## 课程目标

在本课中，你将管理 Linux 机器相关的硬件。

你将：

- 识别常见的硬件组件和资源。
- 配置电源管理。
- 配置可移动硬件。
- 配置大容量存储设备。
- 管理逻辑卷。
- 配置磁盘配额。

## 引言

你配置了各种服务并确保网络安全。在处理 Linux 时，会出现与硬件相关的问题。在本课中，你将管理硬件。

作为 Linux 管理员，你需要定期升级硬件组件。通过添加、移除、管理和故障排除硬件，你可以确保系统高效运行。

本课涵盖以下 CompTIA Linux+ (2009) 认证目标的全部或部分：

- 主题 A
  - 目标 2.7
- 主题 C
  - 目标 1.11
  - 目标 2.7
- 主题 D
  - 目标 1.2
- 主题 E
  - 目标 1.2
- 主题 F
  - 目标 2.7

## 主题 A

### 识别常见的硬件组件和资源

市场上有各种计算机硬件和外围组件。然而，并非所有组件都与 Linux 兼容。在本主题中，你将识别 Linux 常见的硬件组件和资源。

在安装任何操作系统之前，你需要将所有硬件和外围组件到位。然而，并非所有硬件都与所有系统兼容。透彻了解每个组件及其在 Linux 系统内的工作方式，对于其成功安装至关重要。

### 硬件组件

![](img/477ccb2f05b6ba1b2d563ea74f18c197_743_0.png)

Linux 系统的基本硬件组件包括中央处理器（CPU）/浮点单元（FPU）处理器、硬盘、内存、网络适配器和视频卡。额外的组件包括 CD-ROM 驱动器、声卡、调制解调器、USB 设备、FireWire 设备、PCMCIA/Cardbus 卡、打印机和扫描仪。

### 硬件资源

![](img/477ccb2f05b6ba1b2d563ea74f18c197_743_1.png)

硬件资源，如 IRQ、DMA、内存地址和小型计算机系统接口（SCSI）ID，可能会导致 Linux 系统中的系统配置冲突。为防止此类冲突，请查阅文档以确定设备资源应设置为何值。你并不总是可以更改这些设置，但如果可能，请更改设置以确保设备之间不冲突。

### SCSI 类型

SCSI 发音为 “skuzzy”，是一组将外围设备连接到计算机的标准。它是硬盘和 CD-ROM 驱动器的流行格式。它具有快速的传输速率，并且可以处理多个设备。有许多 SCSI 类型，每种类型都有自己的规范。

| SCSI 类型 | 总线宽度和最大吞吐量 |
|---|---|
| SCSI-1 | 8 位，5 MB/秒 |
| Wide SCSI | 16 位，10 MB/秒 |
| Wide Ultra SCSI | 16 位，40 MB/秒 |
| Fast SCSI | 8 位，10 MB/秒 |
| Fast Wide SCSI | 16 位，20 MB/秒 |
| Ultra SCSI | 8 位，20 MB/秒 |
| Ultra2 SCSI | 8 位，40 MB/秒 |
| Ultra3 SCSI | 16 位，160 MB/秒 |
| Ultra 320 SCSI | 16 位，320 MB/秒 |
| Ultra-640 SCSI | 16 位，640 MB/秒 |

