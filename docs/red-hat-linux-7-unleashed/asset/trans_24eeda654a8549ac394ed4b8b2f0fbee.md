

Dale Carstensen 在 `comp.laser-printers` 新闻组中分享的用于将 Apple LaserWriter Plus 的串行端口速度提升至 19200 的内容：

```
#!/
statusdict begin 25 scbatch 0 ne exch 19200 ne or
{ serverdict begin exitserver} {pop end stop} ifelse
statusdict begin
25 19200 0 setscbatch
end % note
```

该命令中包含实际的 CTRL-D 字符

有关 LaserWriter 的更多信息，请参阅 Adobe 的 PostScript 语言参考手册 *RedBook* 中的附录 D，或者浏览 `comp.laser-printers` 以获取有关设置激光打印机的提示。此外，还请阅读 `/usr/share/ghostscript/5.50` 目录下的文件 `Pstiles.htm`，以了解 Ghostscript 发行版中包含的众多 PostScript 打印机实用程序的信息。

然而，大多数桌面用户将打印机连接到并口（平行端口），因此我将首先集中在 `/dev/lp` 上。

### 我在 Linux 下应该使用什么打印机？

几乎任何使用计算机串行端口或并行端口的打印机都应该能正常工作。人们可能会认为，PostScript 打印机是 Linux 的最佳搭配，因为许多与 Linux 配套使用以及从其他 UNIX 系统移植过来的程序和文本工具都输出 PostScript 格式的图形和文本。然而，使用 Linux（以及 Red Hat 的 Linux 发行版）的另一个绝佳理由在于，通过软件的魔力，你那台 99 美元的喷墨打印机也可以打印 PostScript 文档——甚至支持彩色。这太划算了！

### **新的 PPA 打印机支持！**

即使是使用 Printing Performance Architecture (PPA) 的打印机，例如 HP 720、820 或 1000 系列打印机，过去这些打印机需要仅适用于 Windows 的专用软件驱动程序，现在也得到支持了！多亏了 Tim Norman 的早期努力，即使是 HP 710C、712C、720C、722C、820Cs、820Cs、1000CSe 和 1000Cxi 打印机用户现在也能享受打印功能了。Red Hat Linux 现在集成了支持过滤器，提供了多种颜色模式。有关安装支持的详细信息，请参阅本章中“`printtool`—Red Hat Linux 打印系统管理器”部分。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_660_0.png)

### Ghostscript 打印支持

使用 Linux 时，您会发现许多不同的流行打印机都获得了极好的支持。Red Hat Linux 附带了一个名为 `printtool` 的特殊配置工具，直接支持 100 多种打印机。随 Red Hat Linux 附带的 Ghostscript 解释器是许多用户 Linux 打印功能的组成部分，并支持 100 多种不同的打印机。表 19.2 列出了 Ghostscript 驱动和支持的打印机。

你还可以通过直接调用带有 `--help` 命令行选项的 `gs` 解释器，来验证 Red Hat 发行版中 Ghostscript 内置的打印机设备，如下所示：

```
# gs --help
```

`gs` 命令将输出几行关于命令行用法的帮助文本，然后列出编译好的或内置的打印机和图形设备。你还可以通过运行 `gs` 然后在 X11 会话期间使用 `device_names =` 命令来获取此输出，如下所示：

```
# gs
GNU Ghostscript 5.50 (2000-2-13)
Copyright (C) 1998 Aladdin Enterprises, Menlo Park, CA. All rights reserved.
This software comes with NO WARRANTY: see the file COPYING for details.
Loading NimbusRomReg-Regu font from /usr/share/fonts/default/Type1/n021003l.pfb... 2184672 863369 1450640
152624 0 done.
Loading NimbusSanL-Regu font from /usr/share/fonts/default/Type1/n019003l.pfb... 2465960 1103598 1450640
158396 0 done.
GS>> device_names =
[/dn]650c /mjs50c /necp6 /lpb310 /la50 /x11alpha /hlz70 /oki_jet /lp8000 /lp2563 /lp2000 /lwlo /lj5gray /lj100 /tek4696 /lj250 /oki182 /imagen /cljet5 /pr201 /t4693d4 /lg850 /lipsx3 /x11mono /ljjet3d /fmp /stcolor /ljs4v /applebmp /x11gray2 /ljjet2p /djs05] /sj48 /lips4 /la75plus /x11cmyka /laserjet /m6000c /oce9050 /lpb320 /la70 /x11cmyk /ljjet4pj /dct500c /jo700v2c /m8510 /escapepg /iwlk /x11 /decl1250 /deskjet /xes ...
```

请注意，将会打开一个空白的 X11 窗口（因为解释器期望显示 PostScript 图形或文档）；请忽略该窗口并在 `gs` 命令行中输入命令。按下回车后，您将看到内置驱动程序列表（此处未显示所有输出）。有关支持打印机的最新列表和其他信息，请参见 Ghostscript 主页：[http://www.cs.wisc.edu/-ghost/printer.html](http://www.cs.wisc.edu/-ghost/printer.html)。

| 驱动 | 打印机 |
| :--- | :--- |
| ap3250 | Epson AP3250 |
| appledmp | Apple 点阵打印机, ImageWriter |
| bj10e | Canon BJ10e |
| bj200 | Canon BJC-210, 240, 250, 70, 200 |
| bj600 | Canon BJC-600, 610, 4000, 4100, 4200, 4300, 4550, 210, C2500240, 70 |
| bjc800 | BJC-800, 7000 |
| cd5kjet | HP DeskJet 500C |
| cdj500 | HP DeskJet 400, 500C, 540C, 690C, 693C |
| cdj550 | HP DeskJet 550C, 560C, 600, 660C, 682C, 683C, 693C, 694C, 850, 870C |
| cdjcolor | (cdj500 支持打印机的 24 位彩色) |
| cdjmono | HP DeskJet 500C, 510, 520, 540C, 693C |
| cp50 | Mitsubishi CP50 打印机 |
| deskjet | HP DeskJet, Plus |
| djet500 | HP DeskJet 500, Portable |
| djet500c | HP DeskJet 500C |
| dnj650c | HP DesignJet 650C |
| epson | Epson 点阵 |
| eps9mid | Epson 兼容 9 针 |
| eps9high | Epson 兼容 9 针 |
| epsonc | Epson LQ-2550, Fujitsu 2400, 2400, 1200 |
| hl7x0 | Brother HL 720, 730 |
| ibmpro | IBM Proprinter |
| imagen | Imagen ImPress |
| iwhi | Apple ImageWriter (高分辨率) |
| iwlo | Apple ImageWriter (低分辨率) |
| iwlq | Apple ImageWriter LQ |
| jptp3852 | IBM Jprintfa |
| la50 | DEC LA50 |
| la70 | DEC LA70 |
| la75 | DEC LA75 |
| la75plus | DEC LA75plus |
| lhp8 | Canon LBP-III |
| lips3 | Canon LIPS III |
| lj250 | DEC LJ250 |
| lj4dith | HP DeskJet 600, LaserJet 4 |
| ljet2p | HP LaserJet II d, III, III |
| ljet3 | HP LaserJet III |
| ljet3d | HP LaserJet III d |
| ljet4 | HP DeskJet 600, 870Cse; LaserJet 4, 5, 5L, 6L, OKi 410ex |
| ljptplus | HP LaserJet Plus, NEC SuperScrip 860 |
| ln03 | DEC LN03 |
| lp2563 | HP 2563B |
| lq8000 | Epson LP-8000 |
| lq850 | Epson LQ850, Canon BJ300 |
| m8510 | C. Itoh M8510 |
| necp6 | NEC P6, P6+, P60 |
| nwp533 | Sony NWP533 |
| oce9050 | OCE 9050 |
| oki182 | Okidata MicroLine 182 |
| okibm | Okidata IBM 兼容 |
| paintjet | HP PaintJets |
| pj | HP PaintJet XL |
| pjax | HP PaintJet XL |
| pjt300 | HP PaintJet XL300, HP DeskJet 600, 1200C, 1600C |
| r4081 | Ricoh 4081, 6000 激光打印机 |
| sj48 | Starlet 48 |
| sparc | SPARCprinter |
| stcolor | Epson Stylus Color, Color II, 500, 600, 800 |
| st800 | Epson Stylus 800 |
| t4693d2 | Texitronix 4693d (2 位) |
| t4693d4 | Texitronix 4693d (4 位) |
| t4693d8 | Texitronix 4693d (8 位) |
| tek4696 | Texitronix 4695/4696 |
| uniprint | Canon BJC 610, HP DeskJet 550C, NEC P2X, Epson Stylus Color, II, 500, 600, 800, 1520 |
| xes | Xerox XES 2700, 3700, 4045 |

Ghostscript 有几种重要用途，例如显示 PostScript 文档。但当你使用 Red Hat Linux 打印时，Ghostscript 用于将程序的 PostScript 输出转换为你打印机可用的、可打印的形式，例如打印机控制语言。通常，如果你拥有的打印机支持某种形式的打印机控制语言 (PCL)，就不应该有问题。

### 我如何打印？

在为 Linux 设置打印机之前（尤其是如果它是并口打印机），你应该做的第一件事之一是确保打印机工作正常。首先，检查打印机是否已插上、开启并连接到计算机的并口。直通并口电缆通常不会造成问题，但如果你将 CD-ROM、QuickCam、SCSI 适配器、磁带驱动器或 SyQuest 驱动器连接到直通电缆，请不要指望能同时使用打印机。

初学者，请尝试这段简单代码：

```
# ls >/dev/lp0
```

很可能你的打印机会启动且打印头移动，但当你查看打印输出时，你可能会看到一种阶梯效应，每个单词在一行上，横跨页面移动。别担心——这是正常的，这表明你至少可以访问打印机。在本章后面，你将了解如何微调打印设置。

### 新的并口驱动程序

Red Hat Linux 使用 Linux 内核 2.2.16 版本。与以前的 2.0 版本内核不同，最近的 2.2.X 及更新的内核采用不同的方法来处理并口的初始化、识别和配置。在旧版内核中，并口支持专门旨在提供打印机支持，并被“硬编码”在内核中。这种方法无法满足市场上众多并口设备的需求。新方法使用多个并口内核模块，抽象计算机硬件的通信，以更好地支持更广泛的设备并提供新功能，例如使用多个设备。

正如分发的那样，Red Hat Linux 在 `/etc/modules.conf` 中包含默认的并口内核模块配置。这一行启用低级别并口 `parport` 内核模块，尝试自动检测任何连接的打印机或设备：

```
alias parport_lowlevel parport_pc
```

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_664_0.png)

