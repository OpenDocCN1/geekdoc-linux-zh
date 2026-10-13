
## PCMCIA 设备

PCMCIA 设备是笔记本电脑上常见的读卡器，用于连接调制解调器或无线网卡等外设，尽管它们现在也日益成为许多桌面系统的标准配置。同一个 PCMCIA 设备可以支持多种不同类型的设备，包括网卡、调制解调器、硬盘和蓝牙设备等。除了配置 PCMCIA 卡插槽本身之外，你还可以配置插入其中的特定设备，例如无线网卡。这些配置方式与直接连接到系统的标准设备的配置方式相似。请在 www.tldp.org 网站上查阅 PCMCIA-HOWTO，以获取关于 PCMCIA 卡及其配置详细说明。

对 PCMCIA 设备的支持管理方式类似于服务。与大多数设备模块直接加载不同，这种支持是由 pcmcia 服务脚本加载的，正如网络和服务器等服务由服务脚本加载一样。与其他服务脚本类似，pcmcia 脚本位于 `/etc/rc.d/init.d` 目录中。你可以使用 service 命令通过该脚本手动启用或禁用支持。与任何服务一样，你可以使用服务工具或 chkconfig 来配置 pcmcia 在系统启动时自动运行，并指定运行级别。

```
service pcmcia start
```

在 Red Hat 系统中，基本配置由 `/etc/sysconfig` 目录中的 pcmcia 脚本处理，而不是在 `/etc` 目录中。在这里，你可以设置基本启动选项，例如将 PCMCIA 设置为启用 pcmcia，将 PCIC 指定为卡接口控制器（yenta, socket），以及将 PCIC_OPTS 指定为控制器选项。CORE_OPTS 包含 pcmcia_core 模块的选项，而 CARDMGR_OPTS 包含 cardmgr 守护进程的选项。SCHEME 条目可用于选择方案。

针对不同种类可连接至 pcmcia 设备的详细配置保存在 `/etc/pcmcia` 目录中。在这里你会找到 pcmcia 无线、ISDN、串行、SCSI 和 IDE 硬盘以及蓝牙设备的配置文件。每个设备都有相应的启动脚本和对应的选项文件，例如 wireless 和 wireless.opts、ide 和 ide.opts，以及 bluetooth 和 bluetooth.conf。每个脚本都包含适合配置该设备的命令，例如无线设备的 wfconfig 命令、蓝牙的 hciattach，以及用于更新 IDE 和 SCSI 驱动器分区条目的 updftstab。对应的选项文件将保存相应类型设备的配置设置。bluetooth.opts 文件保存不同种类蓝牙设备的参数，而 wireless.opts 文件列出不同无线网卡的可选选项。shared 文件保存各种启动脚本中使用的函数，例如 add_parts，它将通过调用 add_blkdev 函数来添加 IDE 或 SCSI 硬盘 PCMCIA 设备上的分区等块设备，该函数会检查并挂载该分区。许多脚本将运行 shared 脚本来启用这些函数。

你可以随心所欲地添加和移除 PCMCIA 卡。它们将从支持卡数据库中识别，并使用相应的启动脚本进行配置。这一任务由 cardmgr 守护进程处理，它会扫描 PCMCIA 设备上的插入和移除事件，检测到添加的设备并自动加载适当的内核模块。cardmgr 工具将生成一个 `/var/lib/pcmcia/stab` 文件，该文件将列出插槽编号、设备类别、驱动程序以及使用相同驱动程序的设备的设备编号。一个 stab 条目可以使用设备类别来确定该设备使用哪个启动配置脚本。

```
cardctl eject
```

一个用于家庭环境的方案。对于办公设置，你可以创建一个 office 方案；对于家庭设置，创建一个 home 方案。启动设备时，你可以指定要使用的方案。你可以通过 cardctl 命令和不带参数的 scheme 选项来查看当前正在使用的方案。若要切换到特定方案，请提供 scheme 参数，这将更改该设备的方案。

```
cardctl scheme home
```

![](img/32a48d8db4c23e6e2eb70d1e5034c976_771_0.png)

## 安装声卡、网卡和其他卡

要安装新卡，必须首先配置内核以支持它。大多数卡的支持是以模块形式提供的，这些模块可以动态加载到内核中。安装对卡的支持通常只需加载包含其驱动程序的模块即可。例如，Sound Blaster 声卡的驱动程序位于模块 sb.o 中。加载此模块可使你的声卡在 Linux 上可用。大多数发行版会自动检测系统中安装的卡并加载所需的模块。如果你更换了声卡，Kudzu 会自动检测新卡，并调用 redhat-config-soundcard 进行配置。对于网卡，Kudzu 会调用 redhat-config-network 执行配置。你也可以手动加载所需的模块，并移除冲突的旧模块。本章稍后的“模块”一节描述了此过程。

大多数卡的设备文件已在 `/dev` 目录中为你设置好。例如，你的声卡的设备名称是 `/dev/audio`。网卡的设备名称是网络模块的别名，而不是设备文件。例如，你的以太网卡设备名称以 eth 开头，编号从 0 开始，如系统中第一个以太网卡为 eth0。用于引用特定卡所用模块的别名，例如，3Com Etherlink XL 卡别名 3c59x 网络模块，如果是第一个以太网卡，其别名将为 eth0。模块本身保存在内核的模块目录 `/lib/modules` 中，如上一节所述。

## 声音设备

在 Red Hat 中，你可以使用 redhat-config-soundcard 工具在 Linux 上安装大多数声卡。不同的声音设备列表见表 32-3。某些声卡可能需要更专业的支持。对于声卡，你可以通过列出 `/dev/sndstat` 文件的内容来了解当前的声音配置。你可以通过将声音文件重定向到该卡来测试它，如下所示：

```
cat sample.au > /dev/audio
```

对于 2.4 内核，大多数 Linux 声音驱动程序作为开放声音系统（OSS）的一部分开发，并作为 OSS/Free 免费分发。这些作为 Linux 发行版的一部分安装。OSS 设备驱动程序旨在为所有 Unix 平台（包括 Linux）提供统一的 API。它们支持 Sound Blaster 和 Windows 声音系统兼容的声卡（ISA 和 PCI）。OSS 也可按象征性费用获得，并具备用于设备设置的配置界面。

高级 Linux 声音架构（ALSA）取代了 2.6 Linux 内核中的 OSS，旨在成为 OSS 的更好替代方案，同时保持与它的兼容性。ALSA 提供模块化声音驱动程序、API 和配置管理器。ALSA 是一个 GNU 项目，完全免费；其网站 www.alsa-project.org 包含大量文档、应用程序和驱动程序。目前可用的是 ALSA 声音驱动程序、ALSA 内核 API、支持应用程序开发的 ALSA 库，以及提供驱动程序配置界面的 ALSA 管理器。ALSA 源于 Linux Ultra Sound Project。

表 32-3：声音设备

| 设备 | 描述 |
|---|---|
| /dev/sndstat | 声音驱动程序状态 |
| /dev/audio | 音频输出设备 |
| /dev/dsp | 声音采样设备 |
| /dev/mixer | 控制声卡混音器 |
| /dev/music | 高级音序器 |
| /dev/sequencer | 低级音序器 |
| /dev/midi | 直接 MIDI 端口 |

Linux 乐器数字接口（MIDI）和声音页面，目前位于 www.xdt.com/ar/linux-snd，保存了指向各种声卡 Linux 声音驱动程序的 Web 和 FTP 站点的链接。它们还包括指向 Linux MIDI 和声音软件站点的链接。

