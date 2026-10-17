
28 = `/dev/fd2h1440` 3.5 1440K 高密度

124 = `/dev/fd2h1600` 3.5 1600K 高密度

# 390 附录 B

| 设备 | 大尺寸 | 说明 |
| :--- | :--- | :--- |
| 44 = `/dev/fd/u168` | 3.5" | 1680 高密度 |
| 60 = `/dev/fd/u172` | 3.5" | 1722 高密度 |
| 76 = `/dev/fd/u174` | 3.5" | 1743 高密度 |
| 96 = `/dev/fd/u176` | 3.5" | 1760 高密度 |
| 116 = `/dev/fd/u184` | 3.5" | 1840 高密度 |
| 100 = `/dev/fd/u192` | 3.5" | 1920 高密度 |
| 32 = `/dev/fd/u288` | 3.5" | 2280 超密度 |
| 104 = `/dev/fd/u320` | 3.5" | 3200 超密度 |
| 108 = `/dev/fd/u352` | 3.5" | 3520 超密度 |
| 112 = `/dev/fd/u384` | 3.5" | 3840 超密度 |

36 = `/dev/fd/Compaq 2880` 驱动器：过时？

注意：设备名称中的字母（d, q 或 u）表示驱动器类型：5.25" 双倍密度 (d)，5.25" 四倍密度 (q)，5.25" 高密度 (h) 或 3.5" (任何型号，u)。对于 3.5" 设备，大写的 D、H 和 E 已弃用，因为驱动器类型并不重要。

- + 2 字符 留给 `pty` <tty@athena.mit.edu>

- + 块 MFM, RLL 和 IDE 硬盘/CD-ROM

  0 = `/dev/hda` 主设备（或 CD-ROM）

  64 = `/dev/hdb` 从设备（或 CD-ROM）

对于分区，请在整个磁盘设备号上添加：

  0 = `/dev/hd0` 整个磁盘

  1 = `/dev/hd1` 第一个分区

  2 = `/dev/hd2` 第二个分区

  3 = `/dev/hd3` 第三个分区

  4 = `/dev/hd4` 第四个分区

  5 = `/dev/hd5` 逻辑分区

  6 = `/dev/hd6` 第二逻辑分区

  7 = `/dev/hd7` 第三个分区

  63 = `/dev/hd63` 第63 个分区

- + 4 字符 TTY 设备

  0 = `/dev/console` 控制台设备

  1 = `/dev/tty1` 第一个虚拟控制台

  63 = `/dev/tty63` 第63 个虚拟控制台

  64 = `/dev/tty80` 第一个串口端口

  127 = `/dev/tty63` 第64 个串口端口

  128 = `/dev/ttyp0` 伪终端主

  191 = `/dev/ptysf` 第64 个伪终端主

  192 = `/dev/ttyp0` 伪终端从设备

- + 0 = `/dev/st0` 第一个 SCSI 带

  1 = `/dev/stl` 第二个 SCSI 带

# 附录 B

128 = `/dev/nst0` 第一个 SCSI 带，关闭时不弹出

129 = `/dev/nst1` 第二个 SCSI 带，关闭时不弹出

- + 块 多磁盘设备

  0 = `/dev/md0` 第一个设备组

  1 = `/dev/md1` 第二个设备组

多设备驱动用于跨多个物理磁盘扩展文件系统。

- + 10 字符 非串口鼠标，杂项

  0 = `/dev/logibm` 总线鼠标

  1 = `/dev/psaux` PS/2 风格鼠标

  2 = `/dev/importb` Import 鼠标

  3 = `/dev/atimb` 总线鼠标

  4 = `/dev/jvm` J-鼠标

  4 = `/dev/amigouse` Amiga 鼠标 (68k)

  5 = `/dev/atarmouse` Atari 鼠标 (68k)

  128 = `/dev/beep` Fancy蜂鸣器设备

  129 = `/dev/modreq` 内核加载请求

也使用了后缀 `-mouse` 代替 `-bm` 或 `-aux`。

- + 11 块 SCSI-ROM 设备

  0 = `/dev/sr0` 第一个 SCSI-ROM

  1 = `/dev/sr1` 第二个 SCSI-ROM

也使用了前缀 `/dev/scd` 代替 `/dev/sr`，这可能是合理的。

- + 12 字符 QIC-02 带

  2 = `/dev/ntpqic11` QIC-11，关闭时不弹出

  3 = `/dev/tpqic11` QIC-11，关闭时不弹出

  4 = `/dev/ntpqic24` QIC-24，关闭时不弹出

  5 = `/dev/tpqic24` QIC-24，关闭时不弹出

  6 = `/dev/ntpqic120` QIC-120，关闭时不弹出

  7 = `/dev/tpqic120` QIC-120，关闭时不弹出

  8 = `/dev/ntpqic150` QIC-150，关闭时不弹出

  9 = `/dev/tpqic150` QIC-150，关闭时不弹出

指定的设备名称是建议性的——如果这些设备有“标准”名称，请告诉我。

- + 块 MSCDEX-ROM 回调支持

  0 = `/dev/dos_cd0` 第一个 MSCDEX-ROM

  1 = `/dev/dos_cd1` 第二个 MSCDEX-ROM

# Linux 分配设备

...

- + 13 字符 PC 扬声器 `/dev/pcmixer` 模拟 `/dev/mixer`

  0 = `/dev/dsp` 模拟 `/dev/mixer`

  1 = `/dev/dcsp` 模拟 `/dev/dsp` (8位)

  4 = `/dev/pcaudio` 模拟 `/dev/audio`

  5 = `/dev/dcsp16` 模拟 `/dev/dsp` (16位)

- + 块 8位 MFM/RL/IDE 控制器

  0 = `/dev/xda` 第一个 XT 整个磁盘

  64 = `/dev/xdb` 第二个 XT 整个磁盘

分区处理方式与 IDE 磁盘相同（见主设备号 3）。

# 14 字符 声卡

0 = `/dev/mixer` 调音器控制

1 = `/dev/sequencer` 音频序列器

2 = `/dev/midi00` 第一个 MIDI 端口

3 = `/dev/dsp` 数字音频

4 = `/dev/audio` 兼容 Sun 的数字音频

6 = `/dev/sndstat` 声卡状态信息

8 = `/dev/sequencer` 序列器 --备用设备

16 = `/dev/mixer1` 第二个声卡

17 = `/dev/ttyp0` 第一个伪终端主

18 = `/dev/midi0` 第一个 MIDI 端口

19 = `/dev/ptysf` 第64 个伪终端主

20 = `/dev/audio1` 数字音频

  33 = `/dev/ptmgr` 序列器管理器

  34 = `/dev/midi0` 第三个 MIDI 端口

- + 块 BIOS 驱动器支持

  0 = `/dev/hda` 第一个硬盘整个磁盘

  64 = `/dev/hdb` 第二个硬盘整个磁盘

  128 = `/dev/hdc` 第三个硬盘整个磁盘

  192 = `/dev/hdd` 第四个硬盘整个磁盘

分区处理方式与 IDE 磁盘相同（见主设备号 3）。

# 15 字符 摇杆

  0 = `/dev/js0` 第一个摇杆

  1 = `/dev/js1` 第二个摇杆

- + 块 Sony-31A/CD-ROM

  0 = `/dev/sonycd31a` CD-ROM

# 16 字符 留给扫描仪

- + 块 GoldStar-ROM

  0 = `/dev/gsc` GoldStar CD-ROM

# 17 字符 Chase 串口

# 附录 B

  0 = `/dev/ttyH0` 第一个 Chase 端口

  1 = `/dev/ttyH1` 第二个 Chase 端口

...

- 块 Optics Storage-ROM（开发中）

  0 = `/dev/optdd` Optics-ROM

- + 18 字符 Chase 串口 --备用设备

  0 = `/dev/cuh` ttyH0 的呼叫设备

  1 = `/dev/cuhl` ttyH1 的呼叫设备

...

- 块 Sanyo CD-ROM（开发中）

  0 = `/dev/sany` Sanyo CD-ROM

- + 19 字符 Cyclades 串口

  32 = `/dev/ttyC0` 第一个 Cyclades 端口

...

  63 = `/dev/ttyC31` 第32 个 Cyclades 端口

这些设备从 0 开始是合理的...

- 块 Double 压缩磁盘

  0 = `/dev/double0` 第一个压缩磁盘

...

  7 = `/dev/double7` 第八压缩磁盘

  128 = `/dev/cdouble0` 第一个压缩磁盘的镜像

  135 = `/dev/cdouble7` 第八压缩磁盘的镜像

镜像设备的含义请参 Double 文。

- + 20 字符 Cyclades 串口 --备用设备
