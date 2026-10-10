
构建插件后，你可以通过 Mozilla 内部的 `帮助>关于插件` 来验证插件已正确安装。你应该看到类似于 4.7 所示的图像。

![](img/a03699af5597de6a12a449cc2aa3_74.png)

# Plugin 5.1.3 处理 QuickTime 媒体播放器

文件名 `plugger.so`
插件版本 5.1.1，由 Fredrik Hubbe (`hubbe.net`) 编写。有关如何配置的文档，请访问插件主页或查看 `man` 页（类型 `plugger`）。目前处理 141 MIME 类型。

编译文件：
`plugger 5.1.3`
帮助二进制文件：
`plugger 5.1.3`
控制二进制文件：
`plugger-controller`
办公助手：
`plugger-helper`

| 格式 | 说明 | 支持 |
| :--- | :--- | :--- |
| videocodec | MPEG 视频 | mpeg, mpg, mpe |
| video/x-mpeg | MPEG 视频 | mpeg, mpg, mpe | 是 |
| video/x-mpeg2 | MPEG2 视频 | mp2, mv2 | 是 |
| videomvideo | AVI 视频 | |

你可以看到，`Plugin` 可以显示许多格式，是多媒体内容与播放器之间的胶接层。为了验证插件是否运行正常，如果某些测试没有显示或播放，你将需要配置必要的工具让它们播放。

## 4.1.8 如何听 MP3？

非 Web 内容可以使用许多不同的 MP3 播放器听。有很多播放器，但最常见的是：

+ - `KsCD` (KDE)
- `mplayer`
- `XMMS`
- `mpg321`
- `mpg123`
- `AlsaPlayer`

当在 Web 上遇到 MP3 时，插件将首先尝试通过 `mpg123` 播放，然后继续到 `mpg321`, `mplayer`, `xmms`，

## 4.1 插件

如果未找到前面的播放器，则依次使用 `alsaplayer`、`amp`、`maplay`，最后是 `mpeg3player`。所有这些工具都可播放本地内容，也可以播放基于 Web 的内容。如果你想使用保存的播放列表或 `.m3u` 文件，那么你将受限于只能使用 `mpg123`、`mpg321` 或 `xxms` 播放器。

通过 `Plugger` 在 Web 浏览器中使用 `xxms` 播放播放列表 (`.m3u` 文件）存在问题；但 `xxms` 在命令行中运行运行良好。

### 4.1.9 我如何显示流媒体内容？

正如之前所讨论的，`RealPlayer` 之外还有许多流媒体格式可供选择。非常常见的格式是 Media Player 使用的微软格式，我们将在下文中讨论；然而，有许多格式和工具，Mozilla 并没有足够的插件来显示所有内容。其中就观看虚拟教室媒体所需的插件。但对于这些用户来说，通过使用 `CrossOver Office`、`VMware` 等工具，看到了曙光。我们将在第 5 章中详细描述这些工具。如果你使用的是基于 Java 的 Web 工具，则进一步受限于只能使用 Mozilla 或 VMware，因为 Java 内容无法通过 Wine 显示。

然而，如果你想看流电影，那么 `Plugger` 插件会加载 `mplayer` 来处理内容，或者你可以获取 `mplayer` 插件。为了简单起见，`Plugger` 是更好的选择；让它调出合适的工具即可。

### 4.1.10 我如何查看或收听微软播放的内容？

要收听 Microsoft Media Player 内容，你可以使用 Microsoft Media Player，它仅通过 `CrossOver Office` 和 `VMware` 提供。然而，在许多情况下，`mplayer` 运行得良好；你甚至可以为 `xxms` 使用 WMA 插件。

`CrossOver Office` 和 `VMware` 提供了许多可以显示微软专有应用程序的内容，将在 4.1.12 节中讨论。

### 4.1.11 我如何查看或收听各种类型的内容？

在几乎大多数查看或收听多媒体内容的情况下，`Plugger` 插件都能弥补差距。表 4.2 给出了内容类型以及使用哪种播放器来查看或收听指定的 MIME-类型内容。在某些情况下，可以使用多个一个程序；列表按偏好顺序显示。例如，如果你经常播放 QuickTime 内容，你将需要安装 `mplayer`；如果 `mplayer` 不可用，则必须有 `xanim` 才能显示此内容。需要注意的是，在某些情况下，由于版权或法律考虑，Red Hat 从其提供的基础操作系统程序中移除了某些功能。`xmms` 就是其中一个具有限制的程序。

#### 表 4.2 内容类型及用于查看/收听它们的播放器

| MIME 类型 | 描述 | 后缀 | 程序 |
|---|---|---|---|
| video/mpeg | MPEG 视频 | mpeg, mpg, mpeg | mplayer |
| video/x-mpeg | MPEG 视频 | mpeg, mpg, mpeg | mtp xanim |
| video/x-mpeg2 | MPEG2 视频 | mpv2, mp2ve | |
| video/msvideo | AVI 视频 | avi | mplayer |
| video/x-msvideo | AVI 视频 | avi | xanim |
| application/x-drm-v2 | Windows 媒体 | asf | |
| application/x-mplayer2 | Windows 媒体 | wmv, asf, mov | |
| application/x-mplayer2 | WMV | wmv | |
| application/x-quicktimeplayer | Quicktime | mov | |
| video/x-ms-asf | Windows 媒体 | asf, asx | |
| video/x-ms-asf-plugin | Windows 媒体 | asf, asx, wma. wax, wmv, wvx | |
| video/x-ms-wm | MSNBCPlayer | asf | |
| video/x-ms-wmv | Windows 媒体 | wmv | |
| video/x-ms-vwx | Windows 媒体 | wvx | |
| video/sgi-movie | SGI 视频 | movie, mov, mv | |
| video/x-sgi-movie | SGI 视频 | movie, mov, mv | |

## 4.1 插件（重复的章节标题）

#### 表 4.2 内容类型及用于查看/收听它们的播放器（续）

| MIME 类型 | 描述 | 后缀 | 程序 |
|---|---|---|---|
| video/x-theora | 带有视频的 OGG 流 | | mplayer |
| video/theora | 带有视频的 OGG 流 | | |
| video/ogg | 带有视频的 OGG 流 | | |
| video/x-ogg | 带有视频的 OGG 流 | ogm, ogv | | |
| video/quicktime | Quicktime 视频 | mov, qt | mplayer |
| video/x-quick-time | Quicktime 视频 | mov, qt | xanim |
| video/dl | DL 视频 | dl | | |
| video/x-dl | DL 视频 | dl | | |
| video/sgi-movie | SGI 视频 | movie, movi, mv | | |
| video/x-sgi-movie | SGI 视频 | movie, movi, mv | | |
| video/anim | IFF 视频 | iff, anim5, anim3, anim7 | | |
| video/x-anim | IFF 视频 | iff, anim5, anim3, anim7 | | |
| video/x-fli | IFF 视频 | iff,,c | | |
| video/x-fli | |  | |c | | |
| audio/mid | MIDI | | | | | | |
| audio/x-mid | | | | | | | | |
| audio/midi | | | | | | | | |
| audio/x-midi | | | | | | | | |

#### 表 4.2 内容类型及用于查看的播放器（续）

| MIME 类型 | 描述 | 后缀 | 程序 |
|---|---|---|---|
| audio/mp3 | | | | | | | | |
| audio/x-mp3 | | | | | | | | |
| audio/mpeg2 | | | | | | | | |
| audio/x-mpeg2 | | | | | | | | |
| audio/mpeg3 | | | | | | | | | |
| audio/x-mpeg3 | | | | | | | | |
| audio/fl | | | | | | | | | |
| audio/x-fl | | | | | | | | | |
| audio/ms | | | | | | | | | |
| audio/x-ms | | | | | | | | | |
| audio/wav | | | | | | | | | |
| audio/x-wav | | | | | | | | | |
| audio/wmv | | | | | | | | | | |
| audio/x-wmv | | | | | | | | | | |
| audio/mov | | | | | | | | | | |
| audio/x-mov | | | | | | | | | | |
| audio/asf | | | | | | | | | | |
| audio/x-asf | | | | | | | | | | |
| audio/asx | | | | | | | | | | |
| audio/x-asx | | | | | | | | | | |
| audio/wax | | | | | | | | | | |
| audio/x-wax | | | | | | | | | | |
| audio/wvx | | | | | | | | | | |
| audio/x-wvx | | | | | | | | | | |
| audio/ogg | | | | | | | | | | |
| audio/x-ogg | | | | | | | | | | | |
| audio/ogm | | | | | | | | | | | |
| audio/x-ogm | | | | | | | | | | | |
| audio/ogv | | | | | | | | | | | |
| audio/x-ogv | | | | | | | | | | | |
| audio/qt | | | | | | | | | | | |
| audio/x-qt | | | | | | | | | | | |
| audio/dl | | | | | | | | | | | |
| audio/x-dl | | | | | | | | | | | |
| audio/mov | | | | | | | | | | | | |
| audio/x-mov | | | | | | | | | | | | |
| audio/anim | | | | | | | | | | | | |
| audio/x-anim | | | | | | | | | | | | |
| audio/iff | | | | | | | | | | | | |
| audio/x-iff | | | | | | | | | | | | | |
| audio/anim5 | | | | | | | | | | | | | |
| audio/x-anim5 | | | | | | | | | | | | | |
| audio/anim3 | | | | | | | | | | | | | |
| audio/x-anim3 | | | | | | | | | | | | | |
| audio/anim7 | | | | | | | | | | | | | |
| audio/x-anim7 | | | | | | | | | | | | | |

#### 表 4.2 内容类型及用于查看的播放器（续）

| MIME 类型 | 描述 | 后缀 | 程序 |
|---|---|---|---|
| audio/mid | | | |
| audio/x-mid | | | |
| audio/midi | | | |
| audio/x-midi | | | |
| audio/fli | | | |
| audio/x-fli | | | |
| audio/ms | | | |
| audio/x-ms | | | |
| audio/wav | | | |
| audio/x-wav | | | |
| audio/wmv | | | |
| audio/x-wmv | | | |
| audio/mov | | | |
| audio/x-mov | | | |
| audio/asf | | | |
| audio/x-asf | | | |
| audio/asx | | | |
| audio/x-asx | | | |
| audio/wax | | | |
| audio/x-wax | | | |
| audio/wvx | | | |
| audio/x-wvx | | | |
| audio/ogg | | | |
| audio/x-ogg | | | |
| audio/ogm | | | |
| audio/x-ogm | | | |
| audio/ogv | | | |
| audio/x-ogv | | | |
| audio/qt | | | |
| audio/x-qt | | | |
| audio/dl | | | |
| audio/x-dl | | | |
| audio/mov | | | |
| audio/x-mov | | | |
| audio/anim | | | |
| audio/x-anim | | | |
| audio/iff | | | |
| audio/x-iff | | | |
| audio/anim5 | | | |
| audio/x-anim5 | | | |
| audio/anim3 | | | |
| audio/x-anim3 | | | |
| audio/anim7 | | | |
| audio/x-anim7 | | | |

## 4.1 插件

用于查看/收听这些的内容类型和播放器（续）

| MIME 类型 | 描述 | 后缀 | 程序 |
|---|---|---|--|
| application/photoshop | Photoshop 图像 | psd | xvroot display (imagemagick) |
| application/photoshop | Photoshop 图像 | psd | xli & imagagick xloadimage & imagagick |
| image/x-xcf | Gimp 图像 | xcf | xvroot display (imagemagick) |
| image/xcf | Gimp 图像 | xcf | xli & xcfotnpnm |
| application/x-gimp | Gimp 图像 | xcf | xloadimage & xcf-topnmp |
| application/gimp | Gimp 图像 | xcf | |
| application/pdf | PDF 文件 | pdf | acroread |
| application/x-pdf | PDF 文件 | pdf | gv xpdf |
| text/pdf | PDF 文件 | pdf | |
| text/x-pdf | PDF 文件 | pdf | |
| application/x-dvi | DVI 文件 | dvi | xvvi |
| application/x-postscript | PostScript 文件 | ps | gv ghostview |
| application/postscript | PostScript 文件 | ps | pageview ghostscript |

## 表 4.2 用于查看/收听这些的内容类型和播放器（续）

| MIME 类型 | 描述 | 后缀 | 程序 |
|---|---|---|--|
| application/rtf | 富文本格式 | rtf | owriter |
| application/msword | Microsoft Word 文档 | doc, dot | abiword |
| application/msword | Microsoft Word 文档 | doc, dot | sdtcpv |
| application/vnd.sun.writer | OpenOffice.org Writer 文档 | sxw | |
| application/vnd.sun.writertemplate | OpenOffice.org Writer 模板文档 | stw | |
| application/vnd.sun.writerglobal | OpenOffice.org Writer 全局文档 | xsg | |
| application/vnd.stardivision.writer | StarWriter 文档 | sdw | |
| application/x-starwriter | StarWriter 文档 | sdw | |
| application/vnd.stardivision.writer-global | StarWriter 全局文档 | sgl | |
| application/wordperfect.1 | WordPerfect 5.1 文档 | wp | |

## 表 4.2 用于查看/收听这些的内容类型和播放器（续）

| MIME 类型 | 描述 | 后缀 | 程序 |
| --- | --- | --- | --- |
| application/vnd.ms-excel | Microsoft Excel 文档 | xls, xlb | oocalcl |
| application/vnd.sun.xml.calc | OpenOffice.org Calc 文档 | sxc | gnumeric |
| application/vnd.sun.xml.calc.template | OpenOffice.org Calc 模板文档 | stc | sdtcpv |
| application/vnd.stardivi.calc | StarCalc 文档 | sdc | |
| application/x-starcalc | StarCalc 文档 | sdc | |
| application/vnd.lotus-1-2-3 | Lotus 1-2-3 文档 | 123, wkl | |
| application/vnd.sun.xml.impress | OpenOffice.org Impress 文档 | sxi | ooimpress |
| application/vnd.sun.xml.impress.template | OpenOffice.org Impress 模板文档 | sti | |
| application/vnd.stardivision.impression | StarImpress 文档 | sdd | |
| application/vnd.stardivision.impress.packed | StarImpress 打包文档 | sdp | |
| application/x-starimpress | StarImpress 文档 | sdd | |
| application/vnd.ms-powerpointpoint | Microsoft Power-Point 幻灯片放映 | ppt | |

## 表 4.2 用于查看/收听这些的内容类型和播放器（续）

| MIME 类型 | 描述 | 后缀 | 程序 |
|---|---|---|--|
| application/vnd.sun.xml.draw | OpenOffice.org Draw 文档 | sxd | oodraw |
| application/vnd.sun.xml.draw.template | OpenOffice.org Draw 模板文档 | std | |
| application/vnd.stardivision.draw | StarDraw 文档 | sda | |
| application/x-stardraw | StarDraw 文档 | sda | |
| application/vnd.sun.xml.math | OpenOffice.org Math 文档 | sxm | oomath |
| application/vnd.stardivision.math | StarMath 文档 | smf | |
| application/x-starmath | StarMath 文档 | smf | |
| chemical/x-pdb | 蛋白质数据库文件 | pdb | molecule (xscreen-saver) |
| model/x-pdb | 蛋白质数据库文件 | pdb | |

## 表 4.2 用于查看/收听这些的内容类型和播放器（续）

| MIME 类型 | 描述 | 后缀 | 程序 |
|---|---|---||-|
| model/vrml | 虚拟现实建模语言 | vrl, vrml | vrweb |
| model/x-vrml | 虚拟现实建模语言 | vrl | |
| world/vrml | 虚拟现实建模语言 | vrl, vrml | |
| world/x-vrml | 虚拟现实建模语言 | vrl | |
| x-world/vrml | 虚拟现实建模语言 | vrl, vrml | |
| x-world/vrml | 虚拟现实建模语言 | vrl | |
| application/x-troff | MAN 页面 | man | nroff |

为了让某些 MIME 类型正常工作，需要对 `/etc/plugerrc-5.0` 配置文件进行一些小更改。Video/MPEG 需要以下更改；加载速度可能会慢，因为移除 `-cache` 选项会影响性能，但它不会提前终止。将这些行：
```
