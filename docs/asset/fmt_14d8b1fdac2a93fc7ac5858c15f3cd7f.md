
| `cm206.s` | 所有 SCSI 控制器，支持带有 cm260 适配器的 Philips/LMS cm260 CD-ROM |

| `dtc3280.s` | DTC (Data Technology.) 3180/3280 |

| `eata_dma.s` | DPT EATA-DMA（如 PM2011, PM2021, PM2041, PM3021B, PM2012B, PM2022, PM2122, PM2322, PM2042, PM3122, PM3222, PM3332, PM2024, PM2124, PM2044, PM2144, PM3233） |

| `eata_isa.s` | DPT EATA-ISA（如 PM2011B/9X, PM2021A/9X, PM2012A, PM2012B, PM2022A/9X, PM2122A/9X, PM2322A/9X） |

| `eata_plo.s` | DPT EATA-PIO（PM2001 and PM2012A） |

| `fdomain.s` | Future Domain TMC-160 |

| `goldstars.s` | 所有 SCSI 控制器，支持 Goldstar R420 CD-ROM（有时在 Reveal Multimedia Kit 中出售） |

| `in2000.s` | Always IN2000 |

| `iomega.s` | IOMEGA PPA3 并口 SCSI（也支持 ZIP 驱动器的端口） |

| `mcd.s` | 所有 SCSI 控制器，标准非 IDE Mitsumi CD-ROM |

| `mcdxs.s` | 所有 SCSI 控制器，增强型非 IDE Mitsumi CD-ROM |

| `n53c406a.s` | NCR 53c406a |

| `n_5380.s` | NCR 5380 and 53c400 SCSI |

| `n_53c7xx.s` | NCR 53c7xx, 53c8xx SCSI（大多数 NCR PCI SCSI 控制器使用此驱动） |

| `optics.s` | 所有 SCSI 控制器，支持 Optics Spectrum/Studio 8000 AT CD-ROM（“Dolphin”驱动器） |

| `pas16.s` | Pro Audio Spectrum/Studio 16 SCSI |

| `qlog_fas.s` | ISA/VLB/PCMCIA Qlogic FastSCSI（也支持基于 Qlogic FASXXX 芯片的 Control Concepts 卡） |

| `isp` | 支持所有 Qlogic PCI SCSI 控制器，PCI-basic 由 AMD SCSI 驱动支持 |

| `sanyo.s` | 所有 SCSI 控制器，支持 Sanyo CDR-H94A CD-ROM |

| `sbpcid.s` | 所有 SCSI 控制器，支持 Matsushita, Kotobuki, Panasonic, Creative Labs (SoundBlaster), Longshine, 以及 TEAC 非 IDE CD-ROM |

| `scsinet.s` | 所有 SCSI 控制器，支持全以太网 |

| `seagate.s` | Seagate ST01/ST02 and Future Domain TMC-885/950 SCSI |

| `trantor.s` | Trantor T128/T128FT228 |

| `ultrastr.s` | UltraStor 14F, 24F, and 34F SCSI |

| `ustor14f.s` | UltraStor 14F and 34F SCSI |

你需要其中一个来在你的系统上启动 Linux 以便进行安装。由于各种 Linux 驱动程序之间可能发生冲突，提供了多个启动镜像。尽可能使用驱动程序最少的镜像以增加成功概率。

初看，表 3.1 和表 3.2 可能会让人困惑。为了解决这个问题，表 3.3 提供了一个实用的指南，你可以根据安装介质和硬盘格式匹配首选镜像（**粗体**）和备用镜像（*斜体*）。

### 表 3.3 选择启动镜像图

| 安装介质 | IDE 目标 | SCSI 目标 | MFM 目标 |
|---|---|---|---|
| 硬盘 | `bare.i` | 使用一个 SCSI 启动镜像 | `xt.i` |
| SCSI CD-ROM | 使用一个 SCSI 启动镜像 | 使用一个 SCSI 启动镜像 | |
| IDE/ATAPI CD-ROM | `bare.i` | 使用一个 SCSI 启动镜像 | |
| Aztech, Orchid, Okan, Wearnes, Conrad, CyCDROM-nonIDE CD-ROM | `aztech.i` | `aztech.s` | |

# 第 3 章：安装 Linux 和网络组件

### 表 3.3 选择启动盘镜像图表（续）

| 安装媒介 | IDE 目标 | SCSI 目标 | MFM 目标 |
|---|---|---|---|
| 索尼 CDU31a, 索尼 CDU33a CD-ROM | `cdu31a.i` | `cdu31a.s` | |
| 索尼 CDU531, 索尼 CDU535 CD-ROM | `cdu535.i` | `cdu535.s` | |
| 飞利/LMS cm206 CD-ROM | `cm206.i` | `cm206.s` | |
| 金星 R420 CD-ROM | `goldstar.i` | `goldstar.s` | |
| 三美非 IDE CD-ROM | `mcdx.i`, `mcdx.i` | `mcdx.s`, `mcdx.i` | |
| Optics Storage 8000 ATIT CD-ROM ("Dolphin") | `optics` | `optics` | |
| 产洋 CDR-H94A CD-ROM | `sanyo.i` | `sanyo.s` | |
| 松下、胜利树、松下、创新科技 (SoundBlaster)、长星和 TEAC 非 IDE CD-ROM | `sbpcd.i` | `sbpcd.s` | |
| NFS | `net.i` | `scsinet.i` | |
| 磁带 | `bare.i` (用于软磁盘磁带);如需用于 SCSI，请使用下列表 SCSI 启动盘 | 使用下列表 SCSI 控制器启动盘 | `xt.i` (用于软磁盘磁带); |

SCSI 控制器启动盘：`7000fast.s`, `advansys.s`, `aha542.s`, `aha542.s`, `aha140.s`, `aha24x.s`, `am53c974.s`, `busologic.s`, `dtc3280.s`, `eata_dma.s`, `eata_isa.s`, `eata_pio.s`, `fdomain.s`, `in2000.s`, `iomega.s`, `n53c406a.s`, `n_5380.s`, `n_537xx.s`, `pas16.s`, `qlog_fas.s`, `qlog_isp.s`, `seagate.s`, `trantor.s`, `ultrastr.s`, `utor4f`.

### 选择合适的根盘镜像

在选择合适的启动盘后，你需要选择合适的根盘（rootdisk）。选择非常有限，因此你不需要在选择上花费太多精力。根盘存储在 `ROOTDSKS` 目录中，并兼容 3.5 英寸或 5.25 英寸高密度软。

你的根盘镜像选择列在表 3.4。

### 表 3.4 根盘选择

| 文件名 | 用途 |
| --- | --- |
| `COLOR.GZ` | 此镜像包含一个全屏彩色安装程序，应被视为“默认”根盘镜像。然而，此版本的安装系统存在一些已知错误——特别是，它不容忍在屏幕之间输入了额外的按键。总的来说，这可能是你想要使用的文件。 |
| `UMSDOS.GZ` | 这与 `COLOR` 磁盘类似，但使用 UMSDOS 安装——这是一种允许你将 Linux 安装到现有 MS-DOS 分区目录下的文件系统。该文件系统没有原生 Linux 文件系统快。仅凭这一点，任何运行 Linux 网络服务器的人都应该避免 UMSDOS。 |
| `TEXT.GZ` | 这是一个源自以前 Slackware 版本中脚本的文本版安装程序。 |
| `TAPE.GZ` | 此镜像旨在支持从磁带安装。请参阅本章稍后的“从磁带安装”章节。 |

> 注意，这些文件的扩展名为 `.GZ`，表示文件已用 GNU zip 压缩。Linux 的某些其他发行版要求在使用前对文件进行解压，但这里并不需要。启动盘上的内核将检测到根盘是压缩的，并在将其加载到内存时自动解压磁盘。这允许 1.44MB 和 1.2MB 软驱器都使用 1.44MB 的未压缩镜像大小。

大多数用户将使用 `COLOR.GZ` 根盘镜像。

### 创建软磁盘

对于这一步，你需要两张高密度软盘。软盘上的内容并不重要，但它们必须经过格式化——请注意，此过程将完全擦除软盘上存储的任何内容。你可能还需要格式化第三张高密度软盘，供稍后准备系统时安装程序使用。
