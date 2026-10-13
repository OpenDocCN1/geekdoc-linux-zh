
目录内容：总轨道数: 8，(总时间 52:12.72)

1. ( 5:25.67), 2. ( 9:06.65), 3. ( 5:50.68), 4. ( 5:35.57), 5. ( 7:28.35)

6. ( 6:34.60), 7. ( 6:07.15), 8. ( 6:01.05),

## 配置和使用 CD

目录内容：起始扇

1.(  0), 2.( 24442), 3.( 65457), 4.( 91775), 5.( 116957)

6.( 150592), 7.( 180202), 8.( 207742), lead-out( 234822)

`CDINDEX` discid: `SBRXRCIU_.D2SGU1Miq7ksIYYOUE`

`CDDB` discid: `0xe5c3a08`

`CD-Text`: 未检测

`CD-Extra`: 未检测

样本文件大小将为 `552301388` 字节。

正在录制 `3130.09600` 秒立体声，16 位特 @ `44100.0` Hz ->`'audio'`...

百分比_:

100% track 1 录制成功

100% track 2 录制成功

在此示例中，创建了一个名为 `CDDA_DEVICE` 带有设备 SCI 信息的环境变量，并使用 `cdda2raw` 命令将整个音频 CD 的内容提取为 `.wav` 文件格式，每个轨道都保存在一个单独的文件。其他工具可能只需要知道设备名称，例如 `/dev/scd1`，如下：

```
# cdparanoia -d /dev/scd1 -B
cdparanoia III release 9.8 (2001年3月23日)
(C) 2001 Monty <monty@xiph.org> and Xiphophorus
```

向 paranoia@xiph.org 报告错误

http://www.xiph.org/paranoia/

```
无法禁用内核命令转换层
正在从扇区 0 刻录 (轨道 1 [0:00.00])
到扇区 234821 (轨道 8 [6:01.04])
...
```

输出到 `track01.cdda.wav`

> 注意：

> Fedora 还包含了 `cddao` 命令，它可以创建“一次性写入”（DAO）音频和数据 CD-ROM。Linux 驱动程序和各种 CD 驱动器支持的其他录制类型包括“逐轨道写入”（Track-At-Once）和“会话写入”（Session-At-Once），它们会在录制过程的不同阶段开启或关闭驱动器的激光。

在此示例中，使用了 CD-RW 设备名称，同样音频 CD 的所有轨道都将被提取并保存为 `.wav` 音频文件。Red Hat 包含的其他图形化客户端（如 xine、grip 和 xxd）可复制音频和数据 CD。更多信息请参阅第 26 章。

## FEDORA 和 LINUX 命令

在执行安装后任务时，你将使用这些命令：

- `apm`——查看电源管理设置

- `cardctl`——控制 PCMCIA 插槽

- `cd2wav`——从音频 CD 提取音频文件

- `cdparanoia`——从音频 CD 提取音频文件

- `ddrecord`——获取 SCSI 设备信息并刻录 CD-ROM

- `chkconfig`——控制服务

- `dmesg`——查看内核报告

- `internet-Red Hat` 的图形化客户端（如 `systemconfig-network`）检测并配置调制号器

- `kppp`——使用调制号器

- `lsmod`——查看加载的模块

- `mouseconfig`——为 Linux 配置设备

- `ntsys`——控制启动的服务

- `system-config-date`——Red Hat 的图形化日期和时间

- `system-config-display`——图形化配置

- `system-config-soundcard`——Red Hat 的图形化声卡工具

- `system-config-keyboard`——Red Hat 的图形化键盘

- `system-config-mouse`图形化指针工具

- `sensors`——获取系统的电源、风扇速度和 CPU 温度

- `setserial`——从命令行配置串口

- `sndconfig`——为 Fedora 配置声卡

## 参考

- Linux Keyboard and Console HOWTO——Andrew Brouwer 关于键盘和控制台的书；包含许多故障排除提示：http://www.avocent.com/Cybex/Public.nsf/Main——KVM 器的详情。

- http://www.luv.asn.au/overhead/virtualconsololes.html——使用虚拟控制台。

- http://www.synaptics.com/products/touchpad.cfm——关于 TouchPad 设备的信息。

- http://www.compass.com/synaptics——LinuxPad 驱动。

- http://www.x.org/——XOrg 会，X11。

- http://www.alsa-project.org——Advanced Linux Sound 项目首页，Linux 的替代声卡驱动。

- http://www.opensound.com——Linux 的商业驱动。

- `/usr/src/linux-2.4/Documentation/power/pci.txt`——Patrick Michel 关于 Linux 内核和 PCI 硬件支持的文档。

- http://www.tldp.org/Linux/docs/HOWTO/Modem-HOWTO——关于在 Linux 中使用调制号器的最新 HOWTO 之一。

- http://www.tldp.org/Linux/docs/HOWTO/Serial-HOWTO——David S. Lawyer 的 Serial HOWTO，包含关于 Linux 和串口使用的额外信息。

- http://www2.lm-sensors.nu/~lm/cv/lm_sensors2/doc——关于 Linux lm-sensors 的信息。

- http://pcmcia-cs.sourceforge.org——Linux PCMCIA 驱动源。

- http://www.camiresearch.com/Data_Com_Basics/RS232_standard.html——EIA232（原 RS232）标准的描述和教程。

- http://www.qbik.ch/usb/——检查 Linux USB 设备兼容性的地方。

- http://www.linmodems.org——该网站提供了 Linux 下无控制器调制号器的驱动链接。

- http://www.linux1394.org——Linux IEEE 1394 项目首页，包含新信息、驱动链接以及芯片组和设备列表。

- http://www.faqchest.com——FAQchest，可搜索的 FAQ、HOWTO 和邮件列表存档；http://marc.theaimsg.com/ 的替代方案。

- http://groups.google.com/——通过 Google 搜索 Usenet 组；另一个 http://marc.theaimsg.com/ 的替代方案。

- http://www.fokus.gmd.de/research/clone/employees/joerg.schilling/private/cdrecord.html——`cdrecord` 命令及相关工具的首页。

- http://arstechnica.com/guide/building/bios/bios-1.html——ArsTechnica 对 BIOS 选项的极佳讨论。

- http://www.yourvote.com/pci/——列表；使用厂商 ID 获取未知 PCI 设备的信息。

- http://www.linuxnetmag.com/en/issue5/m5devs1.html——关于如何利用 devices.txt 中信息的短文。

## 第 5 章

## Fedora 初步

Fedora Core 为桌面提供了极佳的图形界面（参见第 6 章“X 窗口系统”），以及许多功能强大的图形化管理工具。然而，如果你不知道如何在命令行使用基于文本的程序，有时你无法有效地管理或使用 Linux。在某些情况下以及对于某些软件包，命令行是与运行中的系统交互或重新配置服务器软件的唯一手段。

在本章中，你将学习使用 Linux 的基础知识，以及如何在命令行完成许多例行任务。这些基础操作包括如何读取文本文件或其他文档、列出目录，或移动、复制和重命名文件。新的 Linux 系统管理员将学习使用命令行创建新用户、管理文件权限以及正确重启或关闭 Linux 系统。

本章涵盖的一些基础命令行技能包括：

- 执行例行任务——登录和注销、使用文本控制台、更改密码、列出和导航目录。

- 基础文件管理——创建、重命名或删除文件和目录。

- 基础用户管理——从命令行创建或删除用户。
