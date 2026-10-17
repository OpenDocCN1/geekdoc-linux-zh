
```
$ sed -n '2,3p' filename
```

其中 `filename` 是文件的名称。在我们的示例中，需要注意的几点：

- 因为我们只使用了一个操作，所以省略了 `-e` 选项。
- 我们将命令列在单引号内，这告诉 `sed` 引号内的所有内容都是同一个操作的一部分。
- 我们指定了让 `sed` 处理的某些行。如果没有指定行，`sed` 假设它将处理整个文件。

当然，打印并不是 `sed` 可用的唯一操作。和大多数 UNIX 命令一样，`sed` 可以配合管道和其他命令一起使用。如果你想获得更多更多关于 `sed` 的信息，我们建议你查阅附录 A 中的参考文献。你也可以从手册页获取更多关于 `sed` 的信息：

```
gilbert:~$ man sed
```

### 表 5.7 Sed 操作

| 操作 | 结果 |
| --- | --- |
| a\string | 添加字符串。 |
| c\string | 将指定的行改为指定的字符串。 |
| d | 删除指定的行或字符串。 |
| i | 在指定的行之前插入指定的字符串。 |
| l | 列出文件或其部分——很有用，因为它会显示用于格式化的普通字符； |

## 使用 Ghostscript 打印

在 Linux 下打印并不直观（由于它会显示用于格式化的普通字符，这很有用）。和大多数 UNIX 命令一样，`sed` 可以配合管道和其他命令一起使用。如果你想获得更多关于 `sed` 的信息，我们建议你查阅附录 A 中的参考文献。你也可以从手册页获取更多关于 `sed` 的信息：

```
gilbert:~$ man sed
```

### 使用 Ghostscript 打印

在 Linux 下打印并不直观（由于它会显示用于格式化的普通字符，这很有用）。要要启动解释器，使用以下命令：

```
gilbert:~$ man sed
```

其中 `filename(s)` 是文件名。

# 第 5 章：Linux 应用

| 名称 | 打印机 |
| :--- | :--- |
| lp2563 | HP 2563B 线式打印机 |
| m8510 | C.Itoh M8510 打印机 |
| necp6 | 分辨率为 360 x 360 DPI 的 NEC P6/P6+ 打印机 |
| nwp533 | Sony Microsystems NWP533 激光打印机（仅限 Sony） |
| oce9050 | OCE 9050 打印机 |
| oki182 | Okidata MicroLine 182 |
| okibm | Okidata MicroLine IBM 打印机 |
| paintjet | 备用 H-P Paintjet 彩色打印机 |
| pj | HP Paintjet XL 驱动 |
| pjetxl | 替代 H-P Paintjet XL 驱动 |
| pjxl | HP Paintjet XL 彩色打印机 |
| pjxl300 | HP Paintjet XL300 彩色打印机；也适用于 Paintjet 1200C |
| r4081 | Ricoh 4081 激光打印机 |
| sj48 | Starjet 48 喷墨打印机 |
| sparc | SPARCPR |
| st800 | Epson Stylus 800 打印机 |
| stcolor | Epson Stylus Color |
| t4693d2 | Tektronix 4693d 彩色打印机，R/G/B 每通道 2 位 |
| t4693d4 | Tektronix 4693d 彩色打印机，R/G/B 每通道 4 位 |
| t4693d8 | Tektronix 4693d 彩色打印机，R/G/B 每通道 8 位 |
| tek4696 | Tektronix 4695/4696 喷墨绘图仪 |
| tifferle | TIFF "CCITT RLE 1-dim"（无行结束符的 Group 3 传真） |
| tiff3 | TIFF Group 3 传真（带行结束符） |
| tiff32d | TIFF Group 3 2-D 传真 |
| tiff4 | TIFF Group 4 传真 |
| xes | Xerox XES 打印机（2700, 3700, 4045 等） |

Ghostscript 还支持许多图形文件格式，如表 5.9 所示。

## 表 5.9 Ghostscript 支持的图形文件格式

| 格式 | 解释 |
| :--- | :--- |
| bit | 纯位图，单色 |
| bitrgb | 纯位图，RGB |
| bitcmyk | 纯位图，CMYK |
| bmpmono | 单色 MS Windows .BMP 文件格式 |
| bmp16 | 4 位（EGA/VGA）.BMP 文件格式 |
| bmp256 | 8 位（256色）.BMP 文件格式 |
| bpm16 | 24 位 .BMP 文件格式 |
| cgmmono | 单色（黑白）CGM（仅低级输出） |
| cgm8 | 8 位（256色）CGM（仅低级输出） |
| cgm24 | 24 位彩色 CGM（仅低级输出） |
| cif | 用于 VLSI 的 CIF 文件格式 |
| mgrmono | 1 位单色 MGR 设备 |
| mgrgray2 | 2 位灰阶 MGR 设备 |
| mgrgray4 | 4 位灰阶 MGR 设备 |
| mgrgray8 | 8 位灰阶 MGR 设备 |
| mgr4 | 4 位（VGA）彩色 MGR 设备 |
| mgr8 | 8 位彩色 MGR 设备 |
| pcxmono | PCX 文件格式，单色（1 位黑白） |
| pcxgray | PCX 文件格式，8 位灰阶 |
| pcx16 | PCX 文件格式，4 位平面格式（EGA/VGA） |
| pcx256 | PCX 文件格式，8 位块状色彩 |
| pcx24b | PCX 文件格式，24 位彩色（3 个 8 位平面） |
| pbm | 便端口位图（纯格式） |
| pbmraw | 便端口位图（原始格式） |
| pgm | 便端口灰度图（纯格式） |
| pgmraw | 便端口灰度图（原始格式） |
| pgnm | 便端口灰度图（纯格式），尽可能优化为 PBM |
| pgnraw | 便端口灰度图（原始格式），尽可能优化为 PBM |
| pnm | 便端口像素图（纯格式）（RGB），尽可能优化为 PGM 或 PBM |
| pnmraw | 便端口像素图（原始格式）（RGB），尽可能优化为 PGM 或 PBM |
| ppm | 便端口像素图（纯格式）（RGB） |
| ppmraw | 便端口像素图（原始格式）（RGB） |
| psmono | PostScript（Level I）单色图像 |
| sgirgb | SGI RGB 像素图格式 |
| tiff24nc | TIFF 24 位 RGB，不压缩（NeXT 标准格式） |
| tiffzw | TIFF LZW（标签 = 5）（单色） |
| tiffpack | TIFF PackBits（标签 = 32）（单色） |

这些信息收集自 Ghostscript 页面：http://www.cs.utisc/~ghostscript/。

# 294 第 5 章：Linux 应用程序

表 5.10 Midnight Commander 命令行选项

| 选项 | 结果 |
|---|---|
| -b | 将显示从彩色切换为黑白。 |
| -c | 将显示从黑白切换为彩色。 |
| -C arg | 将颜色更改为 arg。 |
| -d | 禁用鼠标支持。 |
| -f | Midnight Commander 可以带有指定的搜索路径构建；此选项可显示这些路径。 |
| -V | 显示当前版本号。 |
| -x | 通知 Midnight Commander 正在运行于 xterm 窗口，支持 screen 模式和鼠标转义序列。 |

Midnight Commander 在功能方面也非常复杂（换句话说，它的功能非常多，而且并不总是显而易见的），因此在花费大量时间尝试研究它之前，最好先检阅 Midnight Commander 的在线文档。你可以通过查阅它的 man 页（帮助文档）来获取 Midnight Commander 的完整描述：

```
gilbert:$ man mc
```

或者

```
gilbert:$ xman
```

## Xfm

`xfm` 是 Midnight Commander 的 X Window 对应程序，它以图形界面展示你的应用程序和文件。

在使用 `xfm` 之前，你需要运行一个名为 `xfm.install` 的短脚本文件来配置它：

```
gilbert:$ xfm.install
```

这会将配置文件复制到你的家目录中。

# 第 5 章：Linux 应用程序 295
