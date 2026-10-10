
## 摘要

正如我们之前所见，Kismet 的数据格式非常适合将该数据集成到与地图相关的工具和程序中。在本章中我们已经演示过，获取、安装和配置这些工具和程序相对容易；此外，它能带来一些非常积极的结果。无论您只是想将 Kismet 数据上传到 WiGLE，还是配置一个带有语音播报的复杂 GpsDrive 环境，只需稍加额外努力，这一切都触手可及。

## 解决方案快速指南

### GPSMap / KisMap
- GPSMap 是一款原生的 Kismet 工具，旨在将网络叠加显示在从在线资源下载的地图上。
- 由于缺乏地图来源，GPSMap 被修补以包含 Expedia（欧洲），并且可以修补以使用 Google 地图。
- GPSMap 目前正在被重写，并被 KisMap 取代。

### WiGLE
- WiGLE 是一个在线数据库，包含超过 1500 万个已记录的无线网络，其中大多数带有地理坐标。
- WiGLE 让您能够访问 SSID 和制造商统计信息、八位字节和信道使用统计信息，以及一个可浏览的全球网络地图。
- 您可以查询 WiGLE 获取总体统计信息，或者仅查询您上传的信息（前提是您使用个人账户上传了它）。

### WiGLE Google Map
- WiGLE Google Map 是一个基于 Web 的工具，在 Google 地图上显示 WiGLE 数据。

### IGiGLE
- IGiGLE 是一个基于 Windows 的程序，它查询 WiGLE 数据库，下载数据，然后将其转换为 .KML 以便在 Google Earth 中显示。
- IGiGLE 可以通过区域（纬度/经度）或邮政编码下载数据。

### GpsDrive
- GpsDrive 是一个导航系统，在地图上显示 Kismet 数据。
- GpsDrive 需要 SQL 支持来存储 Kismet 网络数据。
- GpsDrive 支持 *festival*（和 *flite*）用于语音播报。

### 替代方案
- Kismet Earth 在 Google Earth 上显示 Kismet 数据。
- OpenStreetMap 是一个使用用户贡献的 GPS 数据编制的可编辑世界地图。

## 使用 Kismet 和 BackTrack 进行 Wardriving

本章的解决方案：
- 获取 BackTrack
- 配置 Kismet
- 使用 Kismet 进行 Wardriving
- 管理您的结果

## 引言

本章的目标是解释并演示在使用 BackTrack（一种实时 Linux 发行版）配合 Kismet 进行 wardriving 的过程。重点在于我们将使用实时 CD，因此无需安装，且只需进行少量配置。这对于那些运行 Windows 系统、需要使用 Kismet 但不想安装整个 Linux 发行版的用户也非常有用。同样重要的是要注意，wardriving 只是使用实时 CD 运行 Kismet 的一个例子。其他可能性包括流氓接入点（AP）检测或网络的图形化映射。

## 获取 BackTrack

本节将重点介绍通过下载（直接下载或种子）获取 BackTrack，然后将其刻录到 CD 上。

### 下载 BackTrack

如果您还没有 BackTrack，您需要下载它。将您的浏览器指向 http://www.remote-exploit.org/backtrack_download.html 以找到 BackTrack 的下载页面（参见图 10.1）。

**图 10.1 Remote-Exploit.org BackTrack 下载页面**

![](img/d6ac176c353d2b7687c1186a140180a1_243_0.png)

BackTrack 2 和 BackTrack 3 Beta 均可用。由于 BackTrack 3 Beta 的 bug 很少且相对稳定，因此推荐此版本（并将其作为本章的重点）。此外，BackTrack 3 Beta 有两个版本：一个是约 700 MB 的 CD 映像版本（本章使用此版本），另一个是更大的（约 1 GB）用于通用串行总线（USB）闪存驱动器的版本，该版本包含一些额外的（但对于我们的目的而言并非必需的）模块。

您可以直接通过超文本传输协议（HTTP）或文件传输协议（FTP）从十个不同的镜像站点下载，或者使用种子下载。如果您有时间，建议（也是更礼貌的做法）使用种子下载，这样可以分享一部分带宽。下载完 ISO 后，务必检查文件的 MD5 哈希值。如果刻录的 CD 不能正常工作，这将为您节省后续的一些麻烦。您可以在 http://www.pc-tools.net/win32/md5sums/ 找到一个简单的消息摘要 5（MD5）哈希计算器（参见图 10.2，其中插入了 BT3b 的哈希值）。只需将 MD5 计算结果与 Remote-Exploit 下载页面上发布的哈希值进行匹配，以确认您的文件是原始文件的真实副本，未受篡改或错误影响。

**图 10.2 确认 MD5 哈希值**

![](img/d6ac176c353d2b7687c1186a140180a1_244_0.png)

### 将 BackTrack 刻录到 CD

您下载的文件是一个 ISO，即 CD 映像文件。要使用 BackTrack，您需要使用市面上可用的众多 CD 刻录程序之一将 ISO 刻录到 CD 上。一个良好且易于使用的例子是程序 *DeepBurner*。可以在 [http://www.deepburner.com/](http://www.deepburner.com/) 找到免费版本（DeepBurner Free）。

虽然本章并不打算作为刻录 CD 的教程，但只需遵循打开 DeepBurner 时启动的向导即可。选择项目类型（刻录 ISO 映像），浏览并选择您的映像文件（bt3b141207.iso），选择您的 CD 写入驱动器和写入速度，最后点击“刻录 ISO”（参见图 10.3）。就是这么简单。

> **提示**
> 虽然您的 CD 驱动器可能支持高速刻录（40 倍速及以上），但建议以较慢的速度刻录 BackTrack——尽可能慢（4 倍速或 8 倍速）。出于某种原因，在较高的刻录速度下会出现更多问题，而较低的速度效果更佳。

**图 10.3 使用 DeepBurner 将 BackTrack 刻录到 CD**

![](img/d6ac176c353d2b7687c1186a140180a1_245_0.png)

## 配置 Kismet

本节将重点介绍启动 BackTrack 并配置 Kismet。

### 启动 BackTrack

要启动 BackTrack，插入 CD 并重启计算机，务必确保 BIOS 设置为从 CD 启动。BackTrack 将完成启动过程。在图形启动菜单中，选择第一个选项，这将使用 KDE 图形桌面启动 BackTrack。任务栏左侧的小黑色终端窗口图标将打开一个控制台窗口。

### 无线网卡配置

也许最重要的要求是一张受 Kismet 支持的无线网卡（参见 Kismet 文档第 12 节“捕获源”，位于 http://www.kismetwireless.net/documentation.shtml，以查看受支持的卡片列表）。话虽如此，如果您启动 BackTrack 并在提示符处直接输入 kismet，您很可能会遇到 Kismet 最常见的错误之一，即配置捕获源失败（参见图 10.4）。

![](img/d6ac176c353d2b7687c1186a140180a1_246_0.png)

![](img/d6ac176c353d2b7687c1186a140180a1_246_1.png)

在您决定放弃之前（遗憾的是，有些人确实会这样做），请阅读错误消息以了解 Kismet 未能启动的原因。在这种情况下，没有启用任何捕获源。如您所料，这是一个致命错误。我们还可以从该错误中推断出，我们可以通过 kismet.conf 文件或命令行指定捕获源来解决此问题。

### kismet.conf

要在 kismet.conf 文件中启用捕获源，请使用您喜欢的文本编辑器（在本例中，我们使用 nano）编辑 /usr/local/etc/kismet.conf（参见图 10.5）。

**图 10.5 编辑 kismet.conf**

![](img/d6ac176c353d2b7687c1186a140180a1_247_0.png)

向下滚动大约一页，找到以以下内容开头的部分：

```
# Sources are defined as:
```

务必通读该部分的注释，了解所需内容：源类型、接口和名称。关于源类型和驱动程序，请参考 Kismet 文档第 12 节“捕获源”。接口由 Linux 定义，并取决于特定的卡片（在本例中，我们使用的是 Atheros 卡片，它使用 ath/wifi 接口）。您还可以在特定的源类型列表中查找此信息。最后，名称是您任意选择的；它只是一个标签。

### 命令行

要从命令行启用捕获源，请使用 -c 开关启动 Kismet，并跟随您在 kismet.conf 文件中使用的相同语法：sourcetype、interface 和 name：

```
ht~# kismet -c madwifi, gw wifi 0, Atheros
```

### 日志文件配置

默认情况下，Kismet 会将其日志文件保存到您启动 Kismet 的位置。例如，如果您在 /root（作为 root 用户登录时的默认目录）启动 Kismet，日志文件将保存在那里。在硬盘安装中，这可能没问题。然而，当启动实时 CD 时，这些文件仅存储在临时 RAM 盘中，并且会在系统关机后消失。在这种情况下，您有两个选择：要么在关机前将文件复制到闪存驱动器（或其他设备）；或者更好的是，从闪存驱动器启动 Kismet，以便文件自动保存在那里。USB 驱动器通常挂载为 sda#，因此只需 cd 到 /mnt/sda1（或正确的编号），并从那里启动 Kismet。

### 其他配置问题

虽然使用 Kismet 不需要全球定位系统（GPS）接收器，但如果您想要位置数据，则是必需的。如果您使用 Kismet 进行 wardriving，GPS 接收器就成了必需品。要配置 Kismet 使用 GPS，您首先需要支持 NMEA 的 GPS 接收器（几乎所有接收器都支持）。其次，您需要启动 GPSD 并将其指向您的 GPS 接收器的路径。要找到接收器的正确路径，插入您的 GPS 并查看 dmesg 的结果（对于 USB 设备，您可以尝试 /dev/ttyUSB0 或 /dev/tts/USB0）：

```
ht~# gpsd -P /dev/tts/USB0
```

您不会收到任何反馈，但可以输入 `ps aux | grep gpsd` 以确保进程已启动。要确认 GPSD 正在工作，请 Telnet 到本地主机 2947 端口并输入 R=1；您应该会看到滚动显示的当前经纬度 NMEA 字符串。

