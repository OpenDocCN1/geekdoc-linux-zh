
## 使用 Ekiga 进行视频会议和 VOIP

Ekiga 应用程序（前身为 GNOME Meeting）使您能够通过视频、音频和文字消息与网络上的人们进行交流。由于 Ekiga 支持 H.323 协议，您可以使用它与其他视频 conferencing 客户端（例如 Microsoft NetMeeting、Cu-SeeMe 和 Intel VideoPhone）的用户进行通信。除了视频会议外，Ekiga 还支持 VOIP 和 IP 电话业务，以便通过互联网拨打电话。

为了能够发送视频，您需要一个在 Linux 中受支持的 Webcam。尽管并非所有 Webcam 都支持 Linux，但您仍有几十种型号可供选择。以下章节将向您展示如何设置您的 Webcam 并使用 Ekiga 进行视频会议。

### 获取受支持的 Webcam

与电视采集卡的支持类似，Webcam 的支持是通过 Video4Linux 接口提供的。一些受支持的摄像机具有并行端口接口，尽管目前 Linux 中支持的大多数 Webcam 都需要 USB 端口。

寻找在 Linux 上工作的 Webcam 有点冒险。很少（如果有的话）Webcam 附带 Linux 驱动程序或规格说明书，允许开源开发者创建这些驱动程序。已创建的 Webcam 驱动程序通常功能有限，有时在新的内核发布后会出现故障。此外，Webcam 供应商有时会在不更改 Webcam 名称的情况下更换其使用的芯片组。而且，有时同一款 Webcam 也会以不同的名称 marketed。

因此，我不会只是告诉您购买哪款 Webcam，而是告诉您哪些 Webcam 受 Fedora 和 RHEL 自带驱动程序的支持。我建议将此信息作为起点。将此信息与一些您可以进一步研究的网站上的信息结合起来，您应该就能做出最佳的 Webcam 选择。

-   **IBM C-It USB Webcams**（`ibmcam` 驱动程序）— 支持此驱动的 Webcam 曾以 Xirlink C-It、IBM PC Camera、Veo Stingray 和 Envision 123 Digital Camera 等名称出售。在购买这些 Webcam 之一之前，请参阅该驱动的 Web 站点（www.linux-usb.org/ibmcam），以获取更多关于受支持摄像机、使不同型号正常工作的技巧以及这些摄像机工作原理的见解的信息。

-   **Konica Webcams**（`konicaAw` 驱动程序）— 此驱动程序应适用于 Intel YC76 或具有以下供应商或产品代码的任何 USB Webcam：0x04c8 或 0x0720。其中包括 Intel Create and Share Camera Pack。有关驱动程序的信息可从 www.si.org/konica 获取。

-   **OmniVision Webcams**（`ov511` 驱动程序）— 此驱动程序支持的 Webcam 包括基于 OmniVision 摄像机芯片的 USB Webcam（www.ov1.com/producte/asp2.table.asp?id=4）。Webcam 包括 Creative WebCam 3、MediaForte MV300、AVERMedia Webcam 和 D-Link DSB-C300。

-   **Philips USB Webcams**（`pwc` 驱动程序）— 此驱动程序支持多种 Philips USB Webcam，包括 PCA645、PCA646、PCVC675、PCVC680、PCVC690、PCVC730、PCVC740 和 Asky VC010。其中包括几款便宜的 Logitech Webcam，包括 QuickCam Pro 3000。

-   **EndPoints Webcams**（`se401` 驱动程序）— 支持包含 EndPoints SE401 芯片组的 Webcam。这些包括 Kensington VideoCam PC 摄像机（67014、67015、67016 和 67017）以及 Aox se401 摄像机。

-   **SONIX PC Cameras**（`sn9c102` 驱动程序）— 基于 SONIX PC 摄像机控制器的 USB 摄像机受此驱动程序支持。这些包括 Sweex 100K、X-Eye 和 Chicony Twinklecam Webcam。sn9c10x 驱动程序由 Linux Projects 维护（www.linux-projects.org）。

-   **STMicroelectronics Webcams**（`stv680` 驱动程序）— 此驱动程序支持包含 STMicroelectronics STV0680B 芯片 USB 版本的 Webcam（www.st.com）。摄像机包括 Aiptec Pencar 和 Nisic Quickpix 2（供应商/产品 ID 0553/0202）。有关驱动程序的信息，请参阅 Linux STV0680 USB 支持页面（http://stv680-usb.sourceforge.net）。

-   **UltraE!m Webcams**（`ultrae!m` 驱动程序）— 支持 IBM UltraPort Camera II 等 Webcam。有关驱动程序的信息，请参阅 ultrae!m 驱动程序页面（www.gutwin.org/eam/source）。

-   **Vie!m Webcams**（`vie!m` 驱动程序）— 3Com HomeConnect USB Webcam 受此驱动程序支持。有关更多信息，请参阅该驱动程序的项目页面（http://homeeonneetbÿb.sourceforge.net）。

-   **Winbond Webcams**（`w996E` 驱动程序）— 支持 Winbond Electronics 的 W996EF JPEG USB 双模式摄像机芯片。使用该芯片的 Webcam 包括 ADG-5000 Arom! Digi Pen、Ezoniey EZ-802 EZMega Cam 和 Pritee DigiPen-480。有关更多信息，请参阅 Linux Projects 站点（www.linux-projects.org）。

查看以下网站，可以了解在 Linux 中受支持和不受支持的 Webcam 的更完整列表。但请记住，这些 Webcam 中并非所有驱动程序都能在 Fedora 或 RHEL 的最新内核中正常工作。

-   Kamerstòi Linux (www.cs.umu.se/~e00ahs/exjobb/linuxcams.html)
-   Linux USB 设备驱动程序 (www.linux-usb.org/devices.html)

我在本章示例中使用的 Logitech QuickCam Pro 3000 Webcam 与 Fedora 7 附带的 pwc 驱动程序配合工作良好。为了确认其正常工作，我运行了 `lsmod` 命令，查看 pwc 驱动程序是否已加载并与 videodev 模块关联：

```bash
# lsmod
pwc                     43392 0
compat_ioctl32          5569 1 pwc
videodev                5120 1 pwc
```

要查看关于 pwc 模块（特定于此 Webcam）的信息，我输入了以下 `modinfo` 命令：

```bash
# modinfo -p pwc
size:Initial image size. One of sqcif, qgif, qcif, sif, cif, vga
fps:Initial frames per second. Varies with model, useful range 5-30
fbufs:Number of internal frame buffers to reserve
mbufs:Number of external (mmap(1ed) image buffers
trace:For debugging purposes
power_save:Turn power save feature in camera on or off
compression:Preferred compression quality. Range 0 (uncompressed) to 3 (high compression)
leds:LED on,off time in milliseconds
dev_hint:Device node hints
```

### 运行 Ekiga

要启动 Ekiga，请选择 Applications -> Internet -> IP Telephone, VOIP and Video Conferencing。要从终端窗口启动 Ekiga，请输入 `ekiga &`。如果未安装，您可以从随本书附带的 DVD 中安装 `ekiga` 包。首次运行 Ekiga 时，Ekiga 配置向导将启动。该向导允许您输入以下信息：

-   **个人资料** — 您的名、姓、电子邮件地址、备注和位置。您还可以选择是否希望在 Ekiga ILS 目录中列出您的信息。
-   **连接类型** — 指示您的互联网连接速度（56K 调制解调器、ISDN、DSL/电缆、T1/LAN 或自定义）。
-   **音频管理器** — 通常您会选择 ALSA 作为您的音频管理器。
-   **视频管理器和设备** — 通常您会选择 Video4Linux 作为视频管理器，并选择您的 Webcam 作为输入设备。

> **注意：** 如果您以后想重新配置 Ekiga，请运行以下命令以清除旧设置：`ekiga-config-tool --clean`。在运行该配置工具之前，请确保所有 Ekiga 实例都已停止。再次运行 `ekiga` 以重新输入您的设置。

图 8-11 显示了带有右侧历史记录日志的 Ekiga 窗口。

![](img/fb202c163797a743c3c6cf236316bc96_385_0.png)

在打开的 Ekiga 窗口中，您可以点击名片图标打开地址簿。从地址簿中选择 Ekiga 白页。通过在搜索过滤器中输入姓名，您可以按名、姓、电子邮件地址或位置搜索可能连接到 Ekiga 服务器的人。从出现的列表中选择一个联系人，如果对方接受您的呼叫，您就可以开始视频会议。

通过选择 View → Control Panel（视图 → 控制面板），您可以选择在视频窗口下方显示标签页，以调整您的音频水平和视频外观。历史标签页显示您的活动日志。

## 播放视频

视频录制（编码）和播放（解码）仍然是开源软件中最具争议且潜在诉讼最多的领域。一方面，拥有复杂视频格式专利持有者可能会对开源编解码器收取专利费（即使软件是从头编写的）。另一方面，电影行业则针对发布他们曾希望保密的加密技术（DeCSS）的人发起攻击，以防止商业电影的开源解码。问题在于，允许您在 Linux 中播放电影的同一技术也可用于复制和分享它们。

> 注意：Codec 是 COder/DECoder（编码器/解码器）或 COmpressor/DECompressor（压缩器/解压缩器）的缩写，具体取决于您询问的对象。无论哪种情况，编解码器都是使计算机能够处理和编码音频和视频的关键。

与音频录制一样，如果您是从头开始，有一个名为 Theora（www.theora.org）的开源编解码器，截至本书撰写之时，您可以使用它而无需支付任何专利费。只要您拥有您录制的版权所有，您就可以自由分发该内容，并允许他人播放它。

关于包含视频编解码器（除免费的 Theora 外），Red Hat, Inc. 采取了谨慎的态度。虽然 Fedora 和 RHEL 现在包含诸如 Totem 之类的视频播放器

