

# 安装后配置问题的故障排排除

将音频 CD 转换为 .wav 格式，每个轨道都保存在一个单独的文件中。其他工具只需要知道设备名称，例如 /dev/scd1，如下所示：

```
# cdparania -dev/scd1 -B
cdparania III release 9.8 (March 23, 2001)
(C) 2001 Monty <monty@xiph.org> and Xiphophorous
```

向 paranoia@xiph.org 报告 bug
http://www.xiph.org/paranoia/

无法禁用内核命令转换层
正在从扇区 0 刻录（轨道 1 [00:00]）
到 扇区 234821（轨道 8 [06:01.04]）

正在输出到 track01.cdda.wav

> 注意
Red Linux 使用 `cdrdao` 命令，它可以创建“一次性刻录”（DAO）音频和 CD-ROM。Linux 驱动程序和各种驱动器支持的其他 CD 刻录类型包括“单轨道一次性”（Track-At-Once）和“会话一次性”（Session-At-Once），它们会在刻录过程的不同阶段开启或关闭驱动器的激光。

在本例中使用了 CDRW 设备名称，再次，音频 CD 的所有轨道将被提取并保存为 .wav 音频文件。Red Linux 还带了其他图形客户端，如 xine、grip 和 xdroast，可以使用它们创建或复制音频 CD。刻录 CD 的更多细节，请参见第 26 章。

# 安装后配置问题的故障排除

随着 Linux 的不断发展，它变得越来越具有容错性，这意味着如果在启动过程中遇到错误，这些错误也不会导致内核或启动完全失败。通常，你的计算机可能看起来运行良好，即使某些设备或进程没有正常工作。此类问题的来源可能包括未加载的模块、未启动的服务，或以非优化水平使用的设备（例如高驱动器速度）。

你可以在 `dmesg` 输出或 `/var/log/messages` 文件中找到问题的线索，后者是一个可以使用任何编辑器查看的简单文本文件。在安装或配置新硬件后，花点时间查看此文件；你会发现它显示了系统启动和启动服务的进度。这些消息是由内核、由 `/etc/rc.d/rc.sysinit` 其他软件以及 Red Hat 的运行级别脚本生成的。你可能会发现

# 第 4 章 安装后配置

一眼看上去是错误，但某些错误并不是真的问题（例如，配置了某个硬件但你的系统中不存在）。

在排除错误消息时，记住“Google 是你的朋友”。只需复制错误消息的部分或全部，并将信息粘贴到 http://www.google.com/linux/ 和 http://marc.theamsgroup.com/ 的搜索框中。你可能会找到带有相关信息的页面链接，帮助你解决问题。你可能不是第一个遇到该问题的人。阅读 `modules.conf` 的手册页并仔细阅读 `/usr/src/linux-2.4/Documentation/devices.txt`（以及其他文件）将对你排除任何问题有很大帮助。

记住一次解决一个问题，并在修改任何系统文件之前，始终创建一个备份副本。不要使用常见的 `.bak` 扩展名，因为该扩展名会被覆盖。这里有一个复制文件的好方法：

```
# cp filename filename.original
```

当从备份恢复时，不要重命名文件，只需复制它，如下：

```
# cp filename.original filename
```

（当这些技巧节省了你无数小时的沮丧时间时，请通过为你的朋友购买这本书来感谢我们。）

# 相关的 Hat 和 Linux 命令

在 Red Hat Linux 中执行安装后配置任务时，你将使用这些命令：

- apm—查看或使用电源管理设置和命令
- cardctl—控制 PCMIA 插槽和服务
- cda2wav—从音频源提取音频文件
- cdaudio—从音频 CD 提取音频文件
- drecord—获取 SCSI 设备信息并刻录 CD-ROM
- chconfig—控制每个 Linux 运行级别的服务
- dmesg—查看 Linux 内核报告的信息
- insmod—将内核模块加载到内存
- internet-druid—Red Hat 的图形化 X，通过配置拨号来检测和配置调制调器
- kbdconfig—为 Linux 配置键盘
- kppp—KDE 的 PPP 连接可以检测并使用调制调器
- lsmod—查看已加载的内核模块
- mouseconfig—为 Linux 配置指向设备
- nsys—控制启动时启动的服务

# 参考

- redhat-config-date—Red Hat 的图形化日期时间
- redhat-config-soundcard—Red Hat 的图形化声卡工具
- redhat-config-keyboard—Red Hat 的图形化键盘映射
- redhat-config-mouse—Red Hat 的图形化指针工具
- redhat-config-xfree86—Red Hat 的 X 配置
- sensors—获取系统的功率、风扇速度和 CPU 温度
- setserial—从命令行配置串口
- sndconfig—为 Red Hat 配置声卡

# Linux 键盘与控制台 HOWTO

以及 Brouwer 关于键盘和控制台问题的巨著；包含许多故障排除技巧。
- http://www.avocent.com/Cybex/Public/nsf—KVM 切换器的产品详情。
- http://www.luv.asn/au/virtualconsoles.html—在 Linux 中使用虚拟终端。
- http://www.synaptics.com/products/touchpad.cfm—关于 TouchPad板设备的信息。
- http://www.compass.com—Linux TouchPad 驱动程序网站。
- http://www.alsa-project.org—高级 Linux 音频架构（ALSA）主页，一组用于 Linux 的替代驱动程序。
- http://www.opensource.com—Linux 的商业声学驱动。
- /usr/src/linux-2.4/Documentation/power/pci.txt—Patrick 关于内核和 PCI 硬件支持的 PCI 管理路由的文档。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/Serial—使用现代方法 Linux 的最新 HOWTO 之一。
- http://www.ibiblio.org/pub/Linux/docs/HOWTO/Serial—David S. Lawyer 的串口 HOWTO，包含关于 Linux 和端口使用的额外信息。
- http://www2.lm-sensors.nu/cvs/doc/FAQ—关于 Linux 软件的信息。
- pcmia-cs.sourceforge.org—Linux 最新 PCMCIA 驱动程序的源码。
- http://www.tuxedo.org/--232—关于 IEEE 232 标准的教程。

# 第 4 章 安装后配置

- http://www.qbik.com/usb/The232—关于 USB 232 的网站。
- http://www.linuxnetmag.com/en/issue5/mdevs1.html—关于使用 devices.txt 信息的简短文章。
- http://www.faqchest.com/search/TheSmartWay——聪明地提问。
- http://groups.google.com/Usenet—Usenet 组。
- http://www.tuxedo.org/--r/fags/smart-questions—聪明提问。
- http://cs.vt.edu/~tjohnson/pinouts/—接脚线信息集。
- http://www.artstechnica.com/guide/building/bios-1.html—Technica 关于 BIOS 选项的精彩讨论。
- http://www.yourvote.com/pci/PCI Vendors and Devices—使用供应商 ID 获取未知 PCI 设备的信息。
- http://mandrakeforum.com/article.php?sid=2242&mode=thread&0&thold=0—配置未列显示器的教程。

