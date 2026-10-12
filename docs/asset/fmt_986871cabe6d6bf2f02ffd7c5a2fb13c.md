
### 8.2 BRITTY

这是一个用于运行串口盲文器的程序。它经过广泛测试和使用，支持多种类型的硬件（参见下文 Linux 手册）。

维护者是 `Nikhil Nair <nn201@cus.cam.ac.uk>`。其他参与此的人有 `Nicholas Petre <nico@cam.org>` 和 `Stephanie Dyon <doyons@umontreal.ca>`。可以向他们发送任何反馈。

作者们似乎正在支持许多设备，所以如果你有设备可以考虑联系他们。他们无疑需要设备的编程信息，如果你能联系你的制造商，他们更有可能帮助你。

一个简要的功能列表（来自他们的 `README` 文件）让你感兴趣：

- 标准屏幕查看功能的完整实现。
- 广泛的可选功能，包括闪烁光标和大写字母、用于休闲的屏幕释放、定位显示文本的属性显示、超链接等。
- “智能”光标路由。这允许在文本编辑器中移动光标而无需移动盲文显示器。
- 剪切粘贴功能。这对于复制长文件名、复杂命令等特别有用。
- 在线功能。
- 支持多种盲文编码。
- 模块化设计允许相对容易地添加其他盲文显示器的驱动，甚至（希望）移植到 Unix 类平台。

```
Title: emacspeak - 基于 Emacs 的语音接口

版本: 4.0

日期: 30MAY96

描述: emacspeak 是让盲人人士使用软盲文显示器访问 Unix 控制台的系统（详见 README 文件）。emacspeak 构建在 Emacs 之上。当你加载了 emacspeak 后启动 emacs，你将对所做的一切获得反馈。你的体验取决于你如何使用 Emacs。

关键词：障碍 访问 视障 语音

作者：raman@adobe.com (T. V. Raman)

维护者：jrv@vanandt (Jim Vanandt)
```

### 8. 软件包

主站点：`sunline.unc.edu/apps/speech`
`124kb` `emacspeak-4.0.tgz`

替代站点：
原始站点：`http://cs.cornell.edu/pub/raman/emacspeak/emacspeak.tar.gz/Info/People/raman/emacspeak.tar.gz`
`123kb` `DECTalk Express` 或 `DEC` 多媒体合成器，`GNU Emacs 19` (`19.23` 或更高版本) 以及 `TCL 7.3` (扩展 `TCL`)。

策略：`GPL`

```
Title: BRITTY - 使用软盲文显示器的用户的 Unix 访问软件

版本: 1.0.2, 17SEP96

日期: 17SEP96

描述：BRITTY 是一个为使用软盲文显示器的用户提供 Unix 控制台访问的守护（完整解释参见 README 文件）。

BRITTY 仅与文本模式应用程序配合。
```

# 1924

# 目录

我们希望这个系统能够扩展以支持其他的盲文显示器，甚至可能支持其他类 `Unix` 平台。

关键词：
盲文控制台访问、视障人士、盲人
`nn201@cus.cam.ac.uk` (`Nikhil Nair`)
`nico@cus.cam.ac.uk` (`Nicolas Pitre`)
`doyon@jps.umontreal.ca` (`Stephanie Doyon`)
`jbrowden@bcs.org.uk` (`James Bowen`)

作者：
维护者：
`nn201@cus.cam.ac.uk` (`Nikhil Nair`)
主站: `sunsite.edu/~pub/Linux/system/Access`
`110kb` `brtty-1.0.2.tar.gz` (包含 `README` 文件)
`6kb` `brtty-1.0.2.README`
`1kb` `brtty-1.0.2.lsm`

平台：
运行在 `PC` 或 `DEC Alpha` 上的 `Linux` (内核 `1.1.92` 或更高版本)。
不支持图形界面。
支持的盲文显示器（仅限串口通信）：
- `Tiemen B.V.`: `CombiBraille 25/45/85`；
- `Alva B.V.`: `ABT3xx` 系列；
- `Telesensory Systems Inc.`: `PowerBraille 40` (非 `65/80`), `Navigator 20/40/80` (仅限最新固件版本)。

复制策略：`GPL`
结束

### 8.3 Screen

`Screen` 是一项标准软件，允许在同一个终端上同时运行许多不同的程序。它已经过增强，可以直接支持某些盲文终端（来自 `Telesensory` 的终端）。

### 8.4 Rrsynth

这是 `Linux` 软件地图中列出的一个语音合成器。对于视障人士来说，它的工作效果看起来并不理想。使用硬件，或者对其进行改进……一个免费的语音合成器将非常有用。

### 8.5 xocr

`xocr` 是一个为 `Linux` 实现光学字符识别（`OCR`）的包。与 `Rrsynth` 一样，我不认为这个包可以作为视障人士唯一的输入手段。我怀疑其使用的算法意味着它需要有人进行监督，以确保读取内容正确。我非常希望被证明是错的。

### 8.6 xzoom

`xzoom` 是一个屏幕放大器，与 `xmag` 类似，但性能足够出色，对视障人士非常有用。`xzoom` 的主要缺点是它无法对自身下方进行放大、某些关键控制与 `fwm`（普通的 `Linux` 窗口管理器）不兼容，并且它的默认配置无法在网络上运行（可以通过花费一些费用来修复）。尽管如此，它非常优秀。它支持连续放大，让你能够例如上下滚动文档，同时保持你正在阅读的部分处于放大状态。或者，你可以在屏幕上移动一个小框，放大内容并让你搜索想要查看的区域。`xzoom` 也可以从普通的 `RedHat` 站点获取 `rpm` 包，这对于使用 `rpm` 系统（带有 `RedHat`）的人来说非常容易。

```
Begin3

Title: 0.1

Entered-date: Mar 30 1996

Description: xzoom 可以放大（按整数值）、旋转

（按 90 度的倍数）并关于 X11 屏幕上的

X 或 Y 轴进行镜像，并在其窗口中显示。

Keywords: X11 缩放大镜

Author: Itai Nahson <nahshon@best.com>

Maintained-by: Itai Nahson <nahshon@best.com>

Primary-site: sunsite.nc.edu

probably in /pub/Linux/X11/xutils/xzoom-0.1.tgz

Platforms: Linux+11. 仅支持 8 位深。

仅在 Linux 1.3.* 与 XSVGA 3.1.2 驱动测试过：需要 XSHM 扩展。

copying-policy: Free

End
```

### 8.7 NFBtrans

`nfbtrans` 是由美国盲人协会（`National Federation for the Blind`）分发的多级盲文翻译程序。它的免费发布是为了有人能改进它。涵盖的语言包括美国英语、英国英语、西班牙语、俄语、世界语、德语、希伯来圣经语，可以通过编写翻译表添加其他语言。还涵盖了一些计算机和数学公式。我已经成功让它在 `Linux` 上编译，但由于目前没有盲文打印机，我还没有对其进行测试。

`nfbtrans` 可以 `<ftp://nfb.org/nfb/braille/nfbtrans/>` 获取。下载后，你需要对其进行编译。

#### 8.7.1 在 Linux 上编译 NFBtrans

我联系了 `nfbtrans` 的补丁开发者，他说他已经包含了它，所以如果你获取的版本高于 `740`，你可能不需要进行任何特殊操作。只需遵循包中包含的说明即可。

```
unzip -L NFBTR740.ZIP   #或者你有的任何文件名

mv Makefile Makefile
```

接下来将以下内容保存到文件（例如 `patch-file`）

```
*** nfpatch.c.orig      Tue Mar 12 11:37:28 1996
--- nfpatch.c      Tue Mar 12 11:37:06 1996
********************
*** 185,190 ****
--- 185,193 ---
  return (finfo.st_size);
} /* filelength */

+ #ifndef linux
+ /* 假设所有行 usleep 应该被
+ done properly */
#ifdef SYSVR
void usleep(nsec)
 int usec;
********************
*** 195,200 ****
--- 198,204 ---
UKP } /* usleep */
#endif
#endif
```
```
void beep(count)
 int count;
```

然后运行

```
patch < patch-file
```

然后输入

```
make
```

程序应该就能编译。

### 8.8 UnWindows
