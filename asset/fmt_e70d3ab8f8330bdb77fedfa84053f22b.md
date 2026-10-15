
| `aha2x4x.s` | Adaptec AIC7xxx (包括 AHA-274x, AHA-2842, AHA-2940, AHA-2940W, AHA-2940U, AHA-2940UW, AHA-2944, AHA-2944WD, AHA-3940, AHA-3940W, AHA-3985, AHA-3985SW) |

| `am53c974.s` | AMD53/79C4 SCSI |

| `aztech.s` | 所有支持的 SCSI 控制器，支持 Aztec268-01A, Orchid CD-3110, Okano/Wearnes CDDI110, Conrad TC, XYCDROM CR520, CR540 |

| `buslogic.s` | Busologic MultiMaster SCSI |

| `cdu31la.s` | 所有支持的 SCSI 控制器，支持 Sony CDU31/33 |

| `cdu535.s` | 所有支持的 SCSI 控制器，支持 Sony CDU531/535 |

| `cm206.s` | 所有支持的 SCSI 控制器，带有 cm260 适配卡的 Philips/LMS cm206 CD-ROM |

| `dtc3280.s` | DTC (Data Technology Corp.) 3180/3280 SCSI |

| `eata_dma.s` | DPT EATA-DMA SCSI (PM2011, PM2021, PM2041, PM3021, PM2021B, PM2022, PM2122, PM2322, PM2042, PM3122, PM3222, PM3332, PM2024, PM2124, PM2044, PM2144, PM3334) |

| `eata_isa.s` | DPT EATA-EISA 支持 (PM2011B/9X, PM2021A/9X, PM2012A, PM2012B, PM2022A/9X, PM2122A/9X, PM2322A/9X) |

| `eata_pio.s` | DPT EATA-PIO SCSI (用于 PM2001 和 PM2012A) |

| `fat32.s` | 类似于 scsis，具有实验性的 FAT32 支持 |

| `fdomain.s` | Future Domain TMC-160 SCSI |

| `goldstar.s` | 所有支持的 SCSI 控制器，Goldstar R420 CD-ROM（有时在 Reveal Multimedia 套件中） |

| `in2000.s` | Always IN2000 |

| `iomega.s` | IOMEGA 并口 |

| `mdx.s` | 所有支持的 SCSI 控制器，非 IDE |

| `n53c06.s` | NCR 5306 |

| `n_5380.s` | NCR 5380 |

| `n53c7xx.s` | NCR 537xx |

| `optics.s` | Optics Storage 8000 AT |

| `qlog_fas.s` | Qlogic FAS |

| `qlog_isp.s` | Qlogic |

| `sanyo.s` | Sanyo CDR-H94A |

| `sbcd.s` | SoundBlaster |

| `scsi.s` | SCSI |

| `scipnp.s` | SCSI-and-play |

| `seinet.s` | 以太网 |

| `trantor.s` | Trantor T128 |

| `ultror.s` | UltraStore F4 |

| `ultrastr.s` | UltraStore F14 |

你需要其中一个镜像来启动 Linux 以便进行安装。由于各种驱动程序可能发生冲突，提供了多个启动磁盘镜像。你应该使用驱动程序尽可能少的一个，以最大化成功机会。

乍看，表 2.1 和表 2.2 可能会让人困惑。为了明确，表 2.3 包含了一个实用的指南，你可以在其中将安装介质和硬盘格式匹配到所需的镜像 `加粗`。

### 表 2.3 启动磁盘镜像表

| 安装介质 | IDE 目标 | SCSI 目标 | MFM 目标 |
| --- | --- | --- | --- |
| 硬盘 | `bare.i` | 使用下列表中的 SCSI 控制器启动磁盘。 | `xt.i` |
| SCSI CD-ROM | 使用下表中的 SCSI 控制器启动磁盘。 | 使用下表中的 SCSI 控制器启动磁盘。 |  |
| IDE/ATAPI CDROM | `bare.i` | 使用下表中的 SCSI 控制器启动磁盘。 |  |
| Aztech, Orchid, Okano, Wearnes, Conrad, CyCD 非 CD-ROM | `aztech.i` | `aztech.s` |  |
| Sony CDU31a, Sony CDU33a CD-ROM | `cdu31a.i` | `cdu31a.s` |  |
| Sony CDU531i, Sony CDU535 CD-ROM | `cdu535.i` | `cdu535.s` |  |
| Philips/LMS cm206 CD-ROM | `cm206.i` | `cm206.s` |  |
| Goldstar R420 CD-ROM | `goldstar.i` | `goldstar.s` |  |
| Mitsumi 非 IDE CD-ROM | `mcdx.i`, `mcdi.i` | `mdxx.s`, `mcdi.s.` |  |
| Optics Storage 8000 AT CD-ROM ("Dolphin") | `optics.i` | `optics.s` |  |

## 第2章：安装 Linux

| 安装介质 | IDE 目标 | SCSI 目标 | MFM 目标 |
|---|---|---|---|
| 松下、Kotobuki、Panasonic、Creative Labs (SoundBlaster)、长星 (Longshine) 和 TEAC 非 IDE CD-ROM | `spcd.i` | `spbpcd.s` |  |
| NFS 磁带 | `net.i` | `bare.i`（用于软盘式磁带）；对于 SCSI，请使用下表中的 SCSI 控制器启动磁盘 | 使用列表中的 SCSI 控制器启动磁盘 | `xt.i`（用于软盘式磁带） |

SCSI 控制器启动磁盘列表如下：

`7000fast.s`, `advansys.s`, `aha152x.s`, `aha1542.s`, `aha1740.s`, `aha24x.s`, `am53c974.s`, `buslogic.s`, `dtc3280.s`, `eata_lma.s`, `eata_isa.s`, `eata_pio.s`, `fdomain.s`, `in2000.s`, `iomega.s`, `n53c46a.s`, `n_5380.s`, `n_53c7xx.s`, `pas16.s`, `qlog_fast.s`, `qlog_isp.s`, `seagate.s`, `transtor.s`, `ultrastr.s`, `utor14f.s`

### 选择合适的根磁盘镜像

在选择合适的启动磁盘后，你需要选择合适的根磁盘。选择非常有限，因此你不需要在这个选择上花费精力。根磁盘存储在 `ROOTDSKS` 目录中，并兼容 3.5 英寸或 5.25 英高密度软盘。

你的根磁盘镜像选择列如表 2.4 所示。

表 2.4 根磁盘选择

| 文件名 | 用途 |
|---|---|
| `COLOR.GZ` | 此镜像包含一个全屏彩色安装程序，应被视为默认根磁盘镜像。此版本的安装系统存在已知的 Bug；但是，特别是，它不会忘记屏幕之间输入的额外按键。这可能是你想要使用的文件。 |
| `UMSDOS.GZ` | 这与彩色磁盘类似，但它使用 UMSDOS 安装，UMSDS 是一种允许你将 Linux 安装到现有 MS-DOS 分区目录的文件系统。这种文件系统没有原生 Linux 文件系统快，但它可以工作，而且你不需要对硬盘重新分区。 |
| `TEXT.GZ` | 这是一个基于文本的安装程序，源自以前 Slack 版本中使用的脚本。 |
| `TAPE.GZ` | 此镜像旨在支持从磁带安装。请参见本章稍后的“从磁带安装”部分。 |
| `PCMCIA.GZ` | 与彩色磁盘类似，但用于通过 PCMCIA 卡（SCSI、以太网或 CD-ROM 驱动器）安装到笔记本电脑的硬盘上。 |

你会注意到这些文件名以 `.GZ` 扩展结尾；这表示文件是用 GNU zip 压缩的。某些旧版本的 Linux 发行版要求在使用前对文件进行解压缩，但现在不再需要了。启动磁盘上的内核将检测到根磁盘是压缩的，并在加载到 RAM 时自动解压缩磁盘。这允许 1.44MB 和 1.2MB 软驱都使用 1.44MB 的未压缩镜像。

大多数用户将使用 `COLOR.GZ` 根磁盘镜像。

### 你应该使用 UMSDOS 吗？

UDOS 文件系统允许你在现有 DOS 分区上的 MS-DOS 目录中安装 Linux。这样做的好处是你不必重新格式化或划分现有的系统。然而，使用该系统有两个缺点。
