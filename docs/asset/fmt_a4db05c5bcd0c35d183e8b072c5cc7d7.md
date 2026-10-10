
- **STMicroelectronics 网络摄像头**（`stvi680` 驱动程序） — 此驱动程序支持包含 STMicroelectronics（http://www.st.com）`STV0680B` 芯片 USB 版本的摄像头。摄像头包括 Aiptec PenCam 和 Nisio Quickpix 2（供应商/产品 ID `0553/0202`）。有关驱动程序的信息，请参阅 Linux STV0680 USP 支持页面（http://stvi680-usb.sourceforge.net）。

- **UltraCam 网络摄像头**（`ultracam` 驱动程序） — 支持如 IBM UltraPort Camera II 等摄像头。请参阅 `ultracam` 驱动程序页面（http://www.gwtwin.org/cam/source/）以获取有关驱动程序的信息。

- **Vacam 网络摄像头**（`vicam` 驱动程序） — 3Com HomeConnect USB Webcam 受此驱动程序支持。请参阅该驱动程序的项目页面以获取更多信息（http://homeconnectusb.sourceforge.net）。

### 第二部分：使用 Fedora

**Winbond 网络摄像头**（`*w9968c* *f*` 驱动程序） — 支持来自 Winbond Electronics 的 `W9968cf` JPEG USB 双模式摄像头芯片。使用该芯片的摄像头包括 ADG-5000 Aromra Digi Pen、Ezonics EZ-802 EZ Mega Cam 和 Pretc DigiPen-480。请参阅 *Linux* *Projects* 网站（http://www.linux-projects.org）以获取更多信息。

查阅以下网站，以获取在 *Linux* 中受支持和不受支持的摄像头更完整的列表。但请记住，这些摄像头的所有驱动程序可能无法在 *Fedora* 的最新内核中正常工作。

- Linux USB 设备驱动程序（http://www.linux-usb.org/devices.html）

- Linux 网络摄像头（http://302found.com/linux-webcams/）

我在本章示例中使用的 Logitech QuickCam Pro 300 摄像头与 *Fedora* 附带的 *pwc* 驱动程序配合良好。为了确认其正常工作，我运行了 *lsmod* 命令，查看 *pwc* 驱动程序是否已加载并与 *videodev* 模块关联：

```bash
# lsmod
pwc                 43392    0
compat_ioctl32      5569  1 pwc
videodev            5120  1 pwc
```

为了查看关于 *pwc* 模块的信息（该模块特定于此摄像头），我输入了以下 *modinfo* 命令：

```bash
# modinfo -p pwc
dev:hint:Device node hints
leds:LED on,off time in milliseconds
compression:Preferred compression quality. Range 0 (uncompressed) to 3 (high compression)
power save:Turn power save feature in camera on or off
trace:For debugging purposes
mbufs:Number of external (mmap'ed) image buffers
bhufs:Number of internal frame buffers to reserve

fps:Initial frames per second. Varies with model, useful range 5-30
size:Initial image size. One of sqcif, qgif, qcif, sif, cif, vga
```

#### 运行 Ekiga

要启动 *Ekiga*，请选择 *应用程序* \( *互联网* \( *IP* *电话*、*VOIP* *和* *视频会议*。要从终端窗口启动 *Ekiga*，请输入 `ekiga`。如果未安装，你可以从随本书附带的 DVD 安装 `ekiga` 软件包。首次运行 *Ekiga* 时，将启动 *Ekiga* *配置* *向导*。该向导允许你输入以下信息：

- **个人数据** — 你的名字、姓氏、电子邮件地址、备注和位置。你还可以选择是否要在 *Ekiga* ILS 目录中列出你的信息。

- **连接类型** — 指示你的互联网连接速度（56K 调制解调器、ISDN、DSL/电缆或局域网）。

- **音频管理器** — 通常你应选择 ALSA 作为音频管理器。

- **视频管理器和设备** — 通常你应选择 Video4Linux 作为视频管理器，并将你的摄像头选为输入设备。

> 注意：如果以后想要重新配置 Ekiga，请运行以下命令以清除旧设置：`ekiga-config-tool --clean`。在运行该配置工具之前，确保已停止所有 Ekiga 实例。此外，请务必关闭面板应用程序，即使已停止 Ekiga，它可能仍在运行。再次运行 `ekiga` 以重新输入你的设置。

图 7-10 显示了 Ekiga 窗口，右侧为历史记录日志。

![](img/c78bdcb5b7842a0d73dcc98921f872a2_312_0.png)

在打开的 Ekiga 窗口中，你可以点击 rolozox 图标打开通讯录。从通讯录中，选择 Ekiga 白页。通过在搜索过滤器中输入姓名，你可以按名字、姓氏、电子邮件地址或位置搜索可能连接到 Ekiga 服务器的人员。从出现的列表中选择一个人，如果对方接受你的呼叫，你就可以开始视频会议。历史记录选项卡显示你的活动日志。

#### 使用 Cheese 拍摄摄像头视频和快照

Fedora 的 GNOME 桌面包含一个用于从摄像头拍摄快照和视频的新应用程序。使用受支持的摄像头（前文已描述），你可以使用新的 Cheese 应用程序（http://www.gnome.org/projects/cheese）通过几次简单的鼠标点击来捕获摄像头的图像。

要安装 Cheese，请以 root 用户身份在终端中输入以下内容：

```bash
# yum install cheese
```

然后，在连接摄像头的情况下，可以从 GNOME 菜单中选择“应用程序 → 声音与视频 → Cheese 摄像头摄影棚”，或者在终端窗口中输入 `cheese` 来启动 Cheese。图 7-11 展示了 Cheese 窗口的示例。

![](img/c78bdcb5b7842a0d73dcc98921f872a2_313_0.png)

**图 7-11：** 使用 Cheese 从你的摄像头拍摄照片或视频。

当你的摄像头输出实时显示在 Cheese 窗口顶部时，你可以使用“照片”或“视频”按钮选择要捕获的内容。中间按钮用于切换，让你选择“拍张照片”或“开始录制”。对于照片，你有三秒钟的暂停时间来准备拍摄。对于视频，录制开始，当你捕获完想要的内容时，需要点击“停止录制”。

在抓取图像或视频之前，你可以选择“特效”来改变图像，以产生诸如黑白、绿巨人（所有东西都变绿）、一些奇怪的变形或眩晕效果等效果。选择“无特效”可关闭特殊效果。

你抓取的每张照片或视频都由窗口底部的缩略图表示。右键点击你选择的图像，你可以选择打开它、保存它、将其移到回收站、通过电子邮件发送或将其导出到 F-Spot 应用程序。你还可以选择“设为账户照片”，使该图像成为登录屏幕、用户切换器小部件或屏幕保护程序窗口中你的用户账户上显示的图像。

#### 播放视频

视频录制（编码）和播放（解码）仍然是开源软件中潜在诉讼风险最高的领域之一。一方面，复杂视频格式的专利持有者可能会要求开源编解码器支付版税（即使该软件是从零开始编写的）。另一方面，电影行业（该行业曾对发布他们本希望保持机密的加密技术 DeCSS 的行为发起攻击）旨在防止商业电影的开源解码。问题在于，允许你在 Linux 中播放电影的同一种技术也可以被用于复制和分享这些电影。

> **注意：** 编解码器（Codec）是 COder/Decoder（编码器/解码器）或 COmpressor/DECompressor（压缩器/解压缩器）的首字母缩写，具体取决于你问谁。无论如何，编解码器使得在计算机上处理和编码音频与视频成为可能。

与音频录制一样，如果你是从零开始，在撰写本文时，存在一种名为 Theora（http://www.theora.org）的开源编解码器，你可以使用它而无需支付任何版税。前提是你拥有正在录制的内容的所有权，你可以自由分发该内容，并允许他人播放它。（详情参见侧边栏“将视频转换为 Theora”。）

#### 将视频转换为 Theora
