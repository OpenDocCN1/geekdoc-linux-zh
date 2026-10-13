

## 受支持的硬件

### 常见 CD-ROM 驱动器

- SCSI CD-ROM 驱动器
  - (摘自 CD-ROM HOWTO) 任何块大小为 512 或 2048 字节的 SCSI CD-ROM 驱动器都应在 Linux 下正常工作；这涵盖了市面上绝大多数 CD-ROM 驱动器。
- EIDE (ATAPI) CD-ROM 驱动器 (IDECD)
  - 几乎所有双倍速、四倍速和六倍速驱动器均受支持，包括：
    - Mitsumi FX400
    - NEC-260
    - Sony 55E

### 专有 CD-ROM 驱动器

- Aztech DAZ68-01A, Orchid CDS-3110, Okano/Wearnes CDD-110, Conrad TXC, CyCDROM CR520ie/CR540ie/CR940ie (AZTCD)
- Creative Labs CD-200 (SBPCD)
- Funai E2550UA/MK4015 (SBPCD)
- GoldStar R420 (GSCD)
- IBM 外部 ISA (SBPCD)
- Kotobuki (SBPCD)
- Lasermate CR328A (OPTCD)
- LMS Philips CM 206 (CM206)
- Longshine LCS-7260 (SBPCD)
- Matsushita/Panasonic CR-521/522/523/562/563 (SBPCD)
- MicroSolutions Backpack 并口驱动器 (BPCD)
- Mitsumi CR DC LU005S (MCD/MCDX)
- Mitsumi FX001D/F (MCD/MCDX)
- Optics Storage Dolphin 8000AT (OPTCD)
- Sanyo CDR-H94A (SJCD)
- Sony CDU31A/CDU33A (CDU31A)
- Sony CDU-510/CDU-515 (SONYCD535)
- Sony CDU-535/CDU-531 (SONYCD535)
- Teac CD-55A SuperQuad (SBPCD)

### Alpha、Beta 驱动

- LMS/Philips CM 205/225/202
  `ftp://metalab.unc.edu/pub/Linux/kernel/patches/cdrom/lmscd0.4.tar.gz`
- NEC CDR-35D (旧版)
  `ftp://metalab.unc.edu/pub/Linux/kernel/patches/cdrom/linux-neccdr35d.patch`
- Sony SCSI 多会话 CD-XA
  `ftp://tsx-11.mit.edu/pub/linux/patches/sony-multi-0.00.tar.gz`
- 并口驱动
  `http://www.torque.net/linux-pp.html`

### 注意事项

所有 CD-ROM 驱动器在读取数据方面的表现应基本相同。音频 CD 播放工具存在各种兼容性问题 (尤其是较新的低端 NEC 驱动器)。一些 Alpha 驱动可能尚不支持音频。

早期 (单倍速) NEC CD-ROM 驱动器可能无法与当前可用的 SCSI 控制器正常配合。

支持 PhotoCD (XA)。Hadmut Danisch 编写的 `hpcdtoppm` 程序可将 PhotoCD 文件转换为可移植位图格式。该程序可从 `ftp://ftp.gwdg.de/pub/linux/hpcdtoppm` 获取，或作为 PBM 工具集的一部分获得。

此外，从 2.1.3x 及更高版本的内核系列开始支持读取视频 CD。内核 2.0.30 有一个补丁可用。

最后，大多数 IDE CD-ROM 换盘器均受支持。

### CD 刻录机

Linux 现在支持许多 CD 刻录机。要获取受支持的 CD 刻录机的最新列表，请查看位于 `http://metalab.unc.edu/LDP/HOWTO/CD-Writing-HOWTO.html` 的 CD-Writing mini-HOWTO，或查看 `http://www.shop.de/cgi-bin/winni/lsc.pl`，或查看 `http://www.gwdg.de:8080/cgi-bin/winni/lsc.pl`。`ftp://metalab.unc.edu/pub/Linux/utils/disk-management/` 中的程序以及 `cdrecord` (`http://www.fokus.gmd.de/research/cc/glone/employees/joerg.schilling/private/cdrecord.html`) 可用于刻录 CD。Linux 的 X-CD-Roast 软件包是使用 CD 刻录机的图形前端。该软件包可在 `ftp://metalab.unc.edu/pub/Linux/utils/disk-management/xcdroast-0.96d.tar.gz` 找到。

- Grundig CDR 100 IPW
- HP CD-Writer+ 7100
- HP SureStore 4020i
- HP SureStore 6020es/i
- JVC XR-W2010
- Kodak PCD 225
- Mitsubishi CDRW-226
- Mitsumi CR-2600TE
- Olympus CDS 620E
- Philips CDD-5210/522, 2000, 2600, 3610
- Pinnacle Micro RCD-5020/5040
- Plextor CDR PX-24CS
- Ricoh MP 1420C
- Ricoh MP 6200S/6201S
- Sanyo CRD-R24S
- Smart and Friendly Internal 2006 Plus 2.05
- Sony CDU 920S/924/926S
- Taiyo Yuden EW-50
- TEAC CD-R50S
- WPI (Wearnes) CDR-632P
- WPI (Wearnes) CDRW-622
- Yamaha CDR-100
- Yamaha CDR-200/200t/200tx
- Yamaha CDR-400t/400tx

## 可移动驱动器

只要控制器受支持，所有 SCSI 驱动器都应能正常工作，包括磁光 (MO)、WORM、软光盘 (floptical)、Bernoulli、Zip、Jaz、SyQuest、PD 等。

Panasonic MO 将 CD-ROM 驱动器与可移动光盘结合在一起。在配置内核时，你必须设置一个开关，才能使这两部分同时工作。

- 并口 Zip 驱动器
  `ftp://gear.torque.net/pub/`
- 并口 Avatar Shark-250
  `http://www.torque.net/parport/`

可移动驱动器的工作方式与硬盘和软盘类似，只需使用 fdisk/mkfs 分区并挂载磁盘即可。如果你的驱动器支持，Linux 还提供驱动器锁定功能。如果磁盘为 MS-DOS 格式，也可以使用 mtools。

CD-R 驱动器需要特殊软件才能工作。请阅读 CD-R Mini-HOWTO。

Linux 支持 512 字节/扇区和 1024 字节/扇区的磁盘。从内核 2.1.32 开始，Linux 还支持 2048 字节/扇区。内核 2.0.30 的补丁可从 http://liniere.gen.u-tokyo.ac.jp/2048.html 获取。

以下设备需要 2048 字节/扇区的支持：

- Fujitsu 磁光磁盘驱动器 M2513

从 pre-patch-2.0.31-3 开始，IDE/ATAPI 内置 Zip 驱动器、软光盘 (floptical) 和 PD 均受支持。

- LS-120 软光盘 (floptical)
- PD-CD

## 鼠标设备

### 受支持

- Microsoft 串口鼠标
- Mouse Systems 串口鼠标
- Logitech Mouseman 串口鼠标
- Logitech 串口鼠标
- ATI XL Inport 总线鼠标
- C&T 82C710 (QuickPort) (Toshiba、TI Travelmate)
- Microsoft 总线鼠标
- Logitech 总线鼠标
- PS/2 (辅助设备) 鼠标

### Alpha、Beta 驱动

- Sejin J-mouse
  ```
  ftp://metalab.unc.edu/pub/Linux/kernel/patches/console/jmouse.1.1.70-jmouse.tar.gz
  ```
- MultiMouse——将多个鼠标设备当作一个鼠标使用
  ```
  ftp://metalab.unc.edu/pub/Linux/X/system/misc/MultiMouse-1.0.tgz
  ```
- Microsoft IntelliMouse

### 注意事项

触摸板设备 (如 Alps Glidepoint) 只要与其他鼠标协议兼容，也能正常工作。

较新的 Logitech 鼠标设备 (Mouseman 除外) 使用 Microsoft 协议，并且三个按钮都能正常工作。尽管 Microsoft 的鼠标设备只有两个按钮，但该协议支持三个按钮。

ATI Graphics Ultra 和 Ultra Pro 上的鼠标端口使用 Logitech 总线鼠标协议。(详见 Busmouse HOWTO。)

## 调制解调器

所有连接到串口的内置调制解调器或外置调制解调器都应能正常工作。遗憾的是，一些制造商制造了仅适用于 Windows 95 的调制解调器。请查阅“Linux 不兼容硬件”以了解 Linux 不兼容的硬件。此外，许多支持闪存升级的调制解调器只有 Win95/NT 的闪存程序，这些调制解调器无法在 Linux 下升级。

少数调制解调器附带 DOS 软件，可在运行时下载控制程序。这些调制解调器通常需要在 DOS 下加载该程序并执行热启动。这类调制解调器最好避免使用，因为今后你将无法在非 PC 硬件上使用它们。

所有 PCMCIA 调制解调器都应能与 PCMCIA 驱动配合工作。

传真调制解调器需要适当的传真软件才能运行。另外，请确保调制解调器的传真部分支持 Class 2 或 Class 2.0。一般而言，UNIX 上的任何传真软件似乎都不支持 Class 1.0。

唯一的例外是 Linux efax 程序，它同时支持 Class 1 和 Class 2 传真调制解调器。在某些情况下，Class 1 调制解调器可能会存在一些 (较小的) 技术问题。如果可以选择，建议你购买 Class 2 调制解调器。

- Digicom Connection 96+/14.4+——DSP 代码下载程序  
  `ftp://metalab.unc.edu/pub/Linux/apps/serialcomm/smdl-linux.1.02.tar.gz`
- Motorola ModemSURFR 内置 56K。如果 IRQ 和端口不是标准配置，请在 RC.SERIAL 中添加几行进行配置。
- ZyXEL U-1496 系列——ZyXEL 1.4，调制解调器/传真/语音控制程序  
  `http://www.pe1chl.demon.nl/ZyXEL/ZyXEL-1.6.tar.gz`
- ZyXEL Elite 2864 系列——调制解调器/传真/语音控制程序  
  `http://www.pe1chl.demon.nl/ZyXEL/ZyXEL-1.6.tar.gz`
- ZyXEL Omni TA 128——调制解调器/传真/语音控制程序  
  `http://www.pe1chl.demon.nl/ZyXEL/ZyXEL-1.6.tar.gz`

Linux 也支持多调制解调器卡。

- Moreton Bay RASTel 多调制解调器卡  
  请查看 `http://www.moreton.com.au/linux.htm` 获取 Linux 驱动。

