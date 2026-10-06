
```
Begin3
Title: emacs - 一个用于 Emacs 的语音输出接口
Version: 4.0
Entered-date: 30MAY96
Description: Emacs 是第一个完整的语音输出系统，它允许无法视物的人士直接在 UNIX 系统上工作。（到目前，视障人士唯一的可用选择是使用会读 PC 作为终端。）Emacs 是在 Emacs 之上构建的。一旦你启动加载的 emacs，你对每一个操作都会得到语音反馈。你的使用体验取决于你使用 Emacs 的熟练程度。在 Emacs 内部没有你做不到的事情。
Keywords: handicap access visually impaired blind speech emacs
Author: raman@adobe.com (T. V. Raman)
Maintained-by: jrv@vanzandt.mv.com (Jim Van Zandt)
Primary-site: sunsite.unc.edu apps/sound/speech
124kb emacs-4.0.tgz
Alternate-site: http://www.cs.cornell.edu/~pub/raman/emacspeak
123KB emacs.tar.gz/Info/People/raman/emacspeak/emacspeak.tar.gz
Platforms: DCTALK Express 或 DEC Multivice 合成器, GNU F3 Emacs 19 (19.23 或更高版本) 和 TCLX 7.3B (扩展 TCL)
```

Copy-policy: GPL

## 8.2 BRLTTY

这是一个用于运行串口盲文终端的程序。它经过了广泛测试，并支持多种不同的硬件（参见 Linux Software Map 条目）。

维护者是 Nikhil Nair <nn201@cam.ac.uk>。其他参与的人有 Nicholas Peter <nico@cam.org> 和 Stephan Doyon <doyons@jp.unimolecular.ca>。请向他们所有人发送任何意见。

作者们似乎渴望获得更多设备的支持，所以如果你有相关设备，请联系他们。他们几乎需要该设备的编程信息，因此如果你能联系你的制造商并获取信息，他们更有可能帮助你。

一个简要列表（来自 README 文件）可以引起你的兴趣：

- 标准屏幕回视功能的完整实现。
- 许多额外的可选功能，包括闪烁的光标和大写字母、用于悠闲查看的屏幕冻结、高亮文本的属性显示、超文本链接等。
- “智能”光标路由。这可以在文本编辑器中轻松移动光标，而无需离开盲文显示器。
- 剪切与粘贴功能。这对于复制长文件名、复杂的命令等特别有用。
- 在线帮助功能。
- 支持多种盲文代码。
- 模块化设计允许相对容易地添加其他盲文显示器的驱动，甚至（希望）移植到其他 Unix 类平台。

## 8. 软件软件包

```
Begin3
Title: BRLTTY - 为盲人提供的 Unix 辅助功能软件 - 使用软盲文终端
Version: 1.0.2, 17SEP96
Entered-date: 17SEP96

Description: BRLTTY 是一个守护进程，为使用软盲文显示器的盲人提供访问 Unix 控制台的权限（完整解释请参见 README 文件）。

BRLTTY 仅对文本模式应用程序有效。

我们希望此系统将扩展到支持其他软盲文显示器，可能甚至支持其他 Unix 类平台。
```

- Keywords: Braille console. access visually impaired blind
- n201@cus.cam.uk (Nikhil Nair)
- nico@cam.com (Nicolas Pitre)
- doyonjs@js.umontontreal.ca (Stephanie Doyon)
- jrowbden@ucs.org.uk (James Bowden)
- Maintained-by: sunsite.unc.edu /pub/Linux/system/Access
- 110kb brltty-1.0.2.gz (包含 README 文件)
- 6kb brltty-1.0.2.README
- 1kb brltty-1.0.2.ism
- Platforms: 运行在 PC 或 DEC Alpha 上的 Linux (v1.92 或更高)，而非 X/Graphics。
- 支持的盲文显示器（仅限串口通信）：
  - Tian B.V.: CombiBraille 25/45/85；
  - Alva B.V.: ABTXX 系列；
  - Telesensory Systems Inc.: PowerBraille 40 (非 65/80)，Navigator 20/40/80 (仅限最新固件版本?)。

Copy-policy: GPL

## 8.3 Screen

Screen 是一个标准软件，允许许多程序在同一个终端上同时运行。它已经增强以支持某些盲文终端（来自 Telesensory 的那些）。

## 8.4 Rsynth

这是 Linux Software Map 中的一个语音合成器。它看起来并不足以视障人士使用。请改用硬件，或者改进它。一个免费的语音合成器将非常有用。

## 8.5 xor

xor 是一个实现 Linux 光学字符识别的包。和 Rsynth 一样，我不认为这可以作为视障人士唯一输入手段的使用。我怀疑使用的算法可能需要观察一下它是否真的有用。我很想证明这一点。

## 8.6 xzoom

xzoom 是一个屏幕放大器，与 xmag 类似，但对视障人士来说足够好用。xzoom 的主要缺点是它无法放大自身，部分键控制与 fwm 兼容，且无法在网络上运行（这可以通过付出代价来修复）。除此之外，它是非常棒。连续放大允许你上下滚动文档，同时保持你正在阅读的部分被放大。或者，你可以在屏幕上移动一个小框，放大并寻找你想查看的内容。xzoom 也有 RedHat 的 rpm 版本，非常方便人们安装。

```
Begin3
Title: xzoom
Version: 0.1
Entered-date: Mar 30 1996
Description: xzoom 可以放大（按整数值）、旋转（按 90 度）并关于 X 或 Y 轴镜像并在窗口中显示。
Keywords: X11 zoom xmag
Author: Ital Nahon <nahon@best.com>
Maintained-by: Ital Nahon <nahon@best.com>
Primary-site: sunite.edu
probably in /pub/Linux/X11/utils/xzoom-```

仅支持 8 位深。需要 SHM 扩展。

Copy-policy: Free

## 8.7 NFtrans

nftrans 是一个多级盲文翻译程序，由盲人联合会（美国）发行。发布它是希望有人能改进它。涵盖的语言有美国英语、英国英语、西班牙语、俄语、德语、希伯来语和希腊语，但可以通过翻译表添加其他语言。我们还成功在 Linux 下编译了它，尽管目前没有盲文设备无法测试。NFtrans 可以从 http://nfb.org/braille/nftrans/ 获取。下载后你需要编译。

### 8.7.1 在 Linux 上编译 NFtrans

我已经把它还给了 NFtrans 的维护者，他说已经包含了它，所以如果你get更高版本，你什么都不需要做。按照包中的指令操作：

```
unzip -L NFBTR.ZIP whatever filename
mv make
```

接下来将以下内容保存到文件（例如 patch-file）：

```
*** nfpatch.c.org Tue Mar 12 11:37:28 1996
--- nfpatch.c Tue Mar 12 11:37:06 1996
***
*** 185,190 ***
--- 185,193 ---
return (finfo.size);
/* filelength */
```

```c
#ifndef linux
/* 足够假设所有 linux 都有 sleep，这应该正确处理 */
#ifdef SYS4
void usleep(usec)
int usec;
***
*** 195,200 ***
--- 198,204 ---
/* usleep * */
#endif
#endif

void beep(count)
int count;
```

然后运行 `patch patch-file`，输入 `make`，程序应该编译。

## 8.8 UnWindows

UnWindows 是一个 X 辅助工具包，为视障（非盲）人士提供许多有用功能。它包括一个屏幕放大器和其他帮助定位光标的自定义工具。UnWindows 可以从 http://ftp.rpi.edu/pub/unwindows 下载。

该包在 Linux 上无法工作，因为它依赖于 SUN 的特殊功能。然而，某些工具是有效的，我成功移植了大部分。这个包可能对某些人感兴趣。我的移植可能会合并到原始版本中，或者在存档中可用（参见 7.3）。剩余无法工作的工具是配置工具。

在我的程序版本中，它们不再自己生成声音，而是调用另一个程序。另一个程序例如：

```
play /usr/lib/games/xboing/sounds/ouch.au
```

这会产生 xboing 噪音，例如它可以在屏幕左边缘这样做。

### 8.8.1 dynamag

dynamag 是一个屏幕放大程序。请参见屏幕放大章节（3.1.2）。该程序在默认发行版中运行。

## 8.8.2 coloreyes

coloreyes 能够轻松找到光标（鼠标）位置。它由一对眼睛组成，始终看向光标方向（像眼睛一样），并根据鼠标远近改变颜色（不像 xeyes）。这在默认发行版中不起，但在相同位置的测试版本似乎有效。

## 8.8.3 border

border 是一个检测光标（鼠标）到达屏幕边缘并根据靠近哪个边缘发出声音的程序。可用的版本使用了 SUN 特有的声音系统。我修改了它，使其运行一个命令，可以是任何 Linux 程序。

## 8.8.4 un-twm

窗口管理器是一个控制 X 屏幕上显示的所有其他窗口（程序）位置的特殊程序。un-twm 是一个特殊版本，光标进入不同窗口时会发出声音。窗口取决于进入了哪个窗口。分发的版本在 Linux 上无法工作，像 border 一样依赖 SUN 音频文件。再次，我已经有一个特殊版本，当你读到这里时它可用了。

# 硬件

## 9.1 盲文终端

这些是可以在普通文本模式下直接读取屏幕内存的盲文终端。它们可以用于 Linux，以实现用户在控制台上可以进行的所有操作，包括在内。然而，它们在普通 Linux 内核的滚动方面存在问题，因此需要应用内核补丁。见 9.1.3。

### 9.1.1 Braillex

Braillex 是一种设计为直接从屏幕内存读取的终端，从而避免了运行异常的 MS-DOS 程序可能带来的任何问题。如果你能看到它，那么这个终端应该以盲文形式显示出来。遗憾的是，在 Linux 中，屏幕处理是由 MS-DOS 完成的，因此必须在某种程度上对其进行修改。

要使用这项工作，你必须应用下文 9.1.3 节中提供的补丁。一旦完成，Braillex 将成为使用 Linux 最实用的终端之一，因为它允许让视力人士通常可以获取的所有信息都能被读出来。

Braillex way两种盲文单元布局（80x1 或 40x2），并有一个名为 IB 2-D 的型号，它还有一个垂直条，用于显示屏幕上所有行的信息（每行屏幕使用 4 个可编程点）。

价格：8

### 9.1.2 Braillterm

“什么是 Braillterm？”

它是一个由 KTS Kommunikations-Technol GmbH 制造的刷新式盲文显示器。它在独特的行内有 80 个盲文单元。每个单元都有 8 个点，通过组合（上/下）来表示一个字符。默认情况下，Braillterm 显示屏幕光标所在的行。我可以使用盲文中的某些功能来查看屏幕上的任何行。” - Jose Volmar Estacio de Souza <jlmar@email.net.br>

Jose 接着说该终端可以在 DOS 下使用串口，但它需要一个特殊的程序。我不知道 Linux 的程序中是否有可以工作的。

和盲文一样，这需要对内核进行一个特殊的补丁才能正常工作。见 9.1.3 节。

价格：23,000,- DM / $15,000。

制造商：Kommunikations-Technol GmbH

供应商：????

### 9.1.3 为 Braillex 和 Braillterm 补丁内核

这可能适用于任何其他直接从屏幕内存读取以便在 MS-DOS 下运行的终端。请发邮件确认你发现的任何终端。此补丁不适用于由 BLRTY 软件驱动的终端，并将使用这些终端的一些功能。

我告诉此补丁适用于所有 1.2.X 版本的内核。它也适用于 1.1.X 到 1.3.72 的内核版本。从 1.3.7 版本开始，不再需要补丁，因为内核可以在 LILO 提示符处使用 'linux no-scroll' 配置为不滚动。更多细节请见 Boot Prompt HMWTO。

```
*** drivers/char/console.c Fri Mar 17 07:03:41 1995
--- drivers/char/console.c	Tue Mar 5 04:34:47 1996
****************
*** 601,605 ****
static void scrap(int currcons, unsigned int, unsigned int b)
{
    int hardscroll = 1;
(b > video_num_lines || t >= b)
--- 601,605 ---
static void scrip(int currcons, unsigned int, unsigned int b)
(
int hardscroll = 0;
if (b > video_num_lines || t >= b)
```

应用方法：

1. 将上述文本保存到文件（例如 say-file）
2. 切换到内核源码的 drivers/char 目录
3. 运行 `patch < say-file`

# 4. 像正常一样编译你的内核

应用这些补丁和补丁后，你应该能够正常地使用盲文终端来读取 Linux 控制台。

换句话说，补丁应该只需将 drivers/char/console.c 文件中第 603 行附近的函数 script 第一行中的 1 改为 0 即可。补丁程序的用处在于它理解这一点，并且它知道当 Linux 在该文件中发生更改时如何进行预测。

如果你想使用完全禁用滚动的更现代内核（而不是我之前提到的启动提示符解决方案），请使用以下补丁。这不适用于 1.3.75 之前的之前的内核。

```
*** console.c*** Fri Mar 15 04:01:45 1996
***console.c*** Thu Apr 4 13:24:48 1996
****************
*** 516,520 ***
unsigned char has_wrapped;
/* all of videomem is data of fg_scroll */
static unsigned char hardscroll_enabled;
! static unsigned char hardscroll_by_init = 0;

void no_scroll(char *str, int *ints)
--- 516,520 ---
unsigned char has_wrapped;
/* all of videomem is data of fg_scroll */
static unsigned char hardscroll_enabled;
! static unsigned char hardscroll_by_init = 1;

void no_scroll(char *str, int *ints)
```

## 9.2 软件驱动的盲文终端

这些终端的工作原理与 CRT 终端（如 vt100）非常接近。语音终端通常连接到串口。在 BTTY 支持的情况下，文档的不同部分可以被读出来（并非所有模型都可用）。语音输出（see Braille）的关键是语音质量。有用功能包括：

- 盲文标签
- 许多语音可以用不同的方式朗读文档部分
- 使用耳机（见 Braille）

9.2.1 Tieman BV.

这是一个比 Braille 更具便携性的显示器。然而，它可以配合 BTTY 使用。有三个版本：25, 45 或 85。这是盲文单元。价格：4600 UKP

制造商：Tieman BV.

供应商：Concept Systems, England

9.2.2 Alva BV.

ABT 系列支持 BTTY。目前已知只有 ABT340 支持。我很想知道是否有人发现这个单元有用。价格：20单元 - 2200 UKP; 40单元 - 4500 UKP; 80单元 - 8000 UKP

制造商：Alva

供应商：Professional Services, Hertfordshire

9.2.3 Telesensory Inc.

由于他们查看了信息，Telesensory 支持 BTTY。有 20, 60 和 85 三种型号。价格：20单元 - 2200 UKP; 40单元 - 4500 UKP; 80单元 - 8000 UKP

制造商：Telesensory Inc.

供应商：Alva

9.2.4 Braille Lite

这是一个比电脑更便携的显示设备。它是一个盲文显示器。然而，它可以配合 BTTY 使用（并非较新版本）。尽可能避免。价格：$6395.00

制造商：Blazie Engineering

## 9.3 语音器

语音器通常连接到 PC 的串口。有用功能包括：

- 盲文标签
- 许多语音可以用不同的方式朗读文档部分
- 使用耳机（并非所有模型都可用）
