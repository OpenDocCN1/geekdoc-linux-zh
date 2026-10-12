
f. 尝试获取故障发生环境中的调试跟踪信息。设置调试级别：

    # echo 6 > /proc/s390dbf/cio_msg/level
    # echo 6 > /proc/s390dbf/cio_trace/level

g. 设置 LCHP 关闭/开启

    # echo "offline" > /sys/devices/css0/chp0.63/status
    # echo "online" > /sys/devices/css0/chp0.63/status

h. 获取 dbginfo。

如果在 LCHP 关闭后状态仍未变更为在线（online）：

a. 再次检查硬件。

b. 强制从 OSA 获取详细信息。（使用 forcelog，即由操作系统工程师获取的错误日志。）确认停机情况发生。

■ 结果与解决方案：硬件问题。
    更换 OSA 卡即可解决该问题。

■ 提示：在共享同一个 OSA 端口的某些 LPAR 中发生了相同的现象。

看起来更可能是硬件问题。

当难以确定是硬件故障还是软件故障时，请复现该问题并获取 s390dbf 信息。

## 8.4.5 启动过程中的 DASD 识别问题

启动过程中 DASD 识别问题的特征如下：

■ 状态：系统重新引导时无法识别 DASD（参见示例 8-14）。

示例 8-14 /var/log/boot.msg

    Couldn't find device with uid 'cPuNQ1-zYo0-3bo5-gxrc-b5VL-Nomg-prT5qf'.
    Couldn't find all physical volumes for volume group vgHPPRRC01arcdest0401.
    /dev/dasdca1: lseek 0 failed: invalid argument
    /dev/dasdca1: lseek 0 failed: invalid argument

■ 环境：System z 上的 SLES9。

■ 收集的信息：

- /var/log/boot.msg
- dbginfo.sh（包含 /var/log/messages）
- siga no
- 独立转储

分析步骤：

- 根据 /var/log/boot.msg，DASD 被识别为无标签（non-label）（示例 8-15）。
- 根据 dbginfo 中的 /proc/partitions，DASD 分区大小异常（示例 8-16）。

示例 8-15 /var/log/boot.msg

    dasd(eckd): 0.0.747f: 3390/OC(CU:3990/01) Cyl:10017 Head:15 Sec:224
    dasd(eckd): 0.0.747f: (4kB blks): 7212240kB at 48kB/trk compatible disk
    dasd1:VOL1/ 0X747f: dasda11
    dasd(eckd): 0.0.77a9: 3390/OC(CU:3990/01) Cyl:10017 Head:15 Sec:224
    dasd(eckd): 0.0.77a9: (4kB blks): 7212240kB at 48kB/trk compatible disk
    dasdca:(non1)/                 : dasdca1

示例 8-16 /proc/partitions

    94 149 7212144 dasdal1
    94 312 7212240 dasdca
    94 313 9223372036854775796 dasdca1
    94 244 7212240 dasdbj

- 从转储中搜索 s390dbf 的 I/O 进程流。
- 由支持中心和开发人员进行搜索。
- DASD 识别功能未能获取卷标信息和分区信息。

结果与解决方案：软件问题。

- 这与在 SLES10 中报告的问题是相同的。
- 使用当前 SLES9 内核的发布补丁。

提示：根据对 /var/log/boot.msg、dbginfo 和转储信息的检查，确定该问题与 SLES10 中的问题相同。

![](img/f332344337ca8bf6846cb313a66ee0b3_284_0.png)

# 安装和配置问题

本章旨在帮助您识别在安装和配置过程中可能遇到的大多数问题。本章将帮助更轻松地确定问题。

本章涵盖以下内容：

- 了解安装过程
- 收集有关安装的信息
- 场景

## 9.1 了解安装过程

在开始安装 Linux 之前，我们需要检查系统要求（例如，内存、网络、磁盘空间）。要了解这些要求的详细信息，请参阅您首选 Linux 发行商的网站，例如：

- [http://www.novell.com](http://www.novell.com)
- [http://www.redhat.com](http://www.redhat.com)

在 System z 上安装 Linux 有两种方式：

- 在 z/VM 下 - 当 Linux 安装在 z/VM 上时，Linux 发行版被视为客户机系统。
- 在 System z LPAR 上 - 当使用 LPAR 安装 Linux 时，允许其使用系统的一部分物理内存。

可以通过图形界面或文本界面在 System z 上安装 Linux。

如果我们决定使用图形用户界面，您可以使用鼠标导航屏幕、输入文本字段或单击按钮。

要运行图形安装，您可以从 Linux 或 Windows@ 工作站机器上使用以下两个选项之一。您还必须拥有另一台正在运行的服务器。

- X11 转发

从您的 Linux 机器上，打开命令提示符并输入以下内容：

    $ ssh -X servername.company

其中：

- -X 是启用 X11 转发的选项。这也可以在配置文件中针对单个主机进行指定。
- servername.company 是即将安装 Linux 的服务器机器（例如，Inx.itsc.ibm.com）。

- VNC 客户端

从您的 Linux 或 windows 机器上，可以使用 VNC 客户端访问服务器并安装 Linux。

**注意：** 在大多数情况下，VNC 选项是最佳解决方案。

至少有四种安装方法可用于安装您的 Linux 发行版：

1. 从硬盘或 DASD 安装。
2. 通过 NFS 安装。
3. 通过 FTP 安装。
4. 通过 HTTP 安装。

当我们使用 NFS、FTP 或 HTTP 方法时，我们需要填写额外的屏幕配置。

**注意：** 对于 SuSE SLES 10 和 RHEL 5.1，我们可以选择层 2 连接来连接到 NFS 和 FTP 服务器。

当我们开始安装时，我们首先在某些包可供安装之前做出一些配置决定。为了安装：

1. 语言选择 - 选择您在安装期间希望使用的语言。

**注意：** 此选择仅适用于安装过程。要配置系统将支持的语言，您必须在语言支持配置面板中进行配置。

2. 磁盘分区设置 - 在此选项中，我们可以选择自动分区或手动磁盘分区。在这里我们配置 Linux 使用的分区大小。参见图 9-1。

![](img/f332344337ca8bf6846cb313a66ee0b3_287_0.png)

**注意：** 对于生产服务器，我们强烈建议使用手动磁盘分区选项。

3. 网络配置 - 配置主机名、网关和 DNS。如果有多块网卡，每个设备都有自己的配置屏幕。参见图 9-2。

![](img/f332344337ca8bf6846cb313a66ee0b3_288_0.png)

图 9-2 配置网络

4. 防火墙配置 - 此时，我们可以决定阻止对计算机的访问。我们可以选择“无防火墙”或“启用防火墙”选项。如果勾选了“启用防火墙”，我们可以允许访问某些服务，例如远程登录（SSH）、文件传输（FTP）、邮件服务器（SMTP）和 Web 服务器（HTTP/HTTps）。参见图 9-3。

![](img/f332344337ca8bf6846cb313a66ee0b3_289_0.png)

**注意：** 如果您愿意，可以在系统安装后启用/禁用这些服务。

5. 在后续屏幕中，我们可以选择支持的语言，设置时区和 root 密码，并选择要安装的包。

![](img/f332344337ca8bf6846cb313a66ee0b3_290_0.png)

此后，Linux 将安装完毕并可以使用。

**注意：** 有关在 S/390 架构上详细安装 Linux 的更多信息，可以在 *IBM z/VM and Linux on IBM System z: Virtualization Cookbook for Red Hat Enterprise Linux 4, SG24-7272* 以及以下地址找到：`http://www.ibm.com/ linux`

## 9.2 收集有关安装过程的信息

**注意：** 本章基于 Red Hat Enterprise Linux 版本 5 编写。当同一主题在 SUSE Linux Enterprise Server 版本 10 中具有不同的文件名或位置时，我们会包含注释。

### 收集安装期间提供的信息

在安装过程中，所有信息都保存在 /root/install.log 文件中，但一旦重启系统，我们就无法访问此文件。在此文件中，我们会遇到关于根据安装选择安装了哪些包及版本的信息。参见示例 9-1。

示例 9-1 /root/install.log 的部分内容

    Installing eel2-devel - 2.16.1-1.el5.s390x
    Installing bug-buddy - 1:2.16.0-2.el5.s390x
    Installing setroubleshoot - 1.8.11-4.el5.noarch
    Installing evolution-data-server-devel - 1.8.0-15.el5.s390
    Installing devhelp - 0.12.9-el5.s390
    Installing gnome-desktop-devel - 2.16.0-1.fc6.s390
    Installing gnome-python2-bonobo - 2.16.0-1.fc6.s390x
    Installing sabayon - 2.12.4-3.el5.s390x
    Installing eel2-devel - 2.16.1-1.el5.s390
    Installing krb5-auth-dialog - 0.7-l.s390x
    Installing gtkhtml3 - 3.12.0-1.fc6.s390x
    Installing orca - 1.0.0-5.el5.s390x
    Installing gnome-python2-gnomevfs - 2.16.0-1.fc6.s390x
    Installing gnome-terminal - 2.16.0-3.el5.s390x
    Installing libgnome-devel - 2.16.0-6.el5.s390
    Installing system-config-date - 1.8.12-1.el5.noarch
    Installing nautilus - 2.16.2-6.el5.s390x
    Installing alacarte - 0.10.0-1.fc6.noarch
    Installing yelp - 2.16.0-13.el5.s390x
    Installing eog - 2.16.0.1-6.el5.s390x
    Installing gnome-applets - 1:2.16.0-1-19.el5.s390x
    Installing ImageMagick - 6.2.8.0-3.el5.4.s390
    Installing gnome-system-monitor - 2.16.0-3.el5.s390x
    Installing im-chooser - 0.3.3-6.el5.s390x
    Installing nautilus-cd-burner - 2.16.0-7.el5.s390x
    Installing evince - 0.6.0-8.el5.s390x
    Installing nautilus-cd-burner - 2.16.0-7.el5.s390
    Installing pirut - 1.2.10-1.el5.noarch
    Installing file-roller - 2.16.0-2.fc6.s390x
    Installing dogtail - 0.6.1-2.el5.noarch
    Installing gnome-power-manager - 2.16.0-7.el5.s390x
    Installing gnome-utils - 1:2.16.0-3.el5.s390
    Installing gnome-session - 2.16.0-6.el5.s390x
