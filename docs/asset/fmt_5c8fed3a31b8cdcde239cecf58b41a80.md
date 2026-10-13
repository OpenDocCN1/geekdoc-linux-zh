
| Adapptec AHA-3840U/IW (PCI) | aha3840 |

| Adapptec AHA-3950U2D | aha3950 |

| Adapptec AHA-3960D | aha3960 |

| Adapptec AHA-398x/U/WW (PCI) | aha398x |

| Adapptec AHA-2920A (PCI) 带有 Future Domain Chip组 | fdomain |

| Adapptec AVA-1502E (ISA/VLB) | aha152 |

| Adapptec AVA-1505/1515 (ISA) | aha152 |

| Adapptec AVA-282 (均兼容 Adapptec AHA-152x) | aha152 |

| Advansys BP510/1550 ISA 主总控制器 | advansys |

| Advansys BP5140 ISA 主总控制器 | advansys |

| Advansys BP5142 ISA 主总控制器 PnP (带软驱) | advansys |

| Advansys BP5452 ISA 主总控制器 (带软驱，单通道) | |

| BPA2 EISA 主总控制器 (单通道) | |

| BPA752 EISA 主总控制器 (双通道) | |

| BPA784 VL 主总控制器 (单通道) | |

| BPA880 VL 主总控制器 (双通道) | |

| BPA920 PCI 主总控制器 (双通道) | |

| BPA930/U PCI/Ultra 主总控制器 | |

| BPA940/U PCI 主总控制器 (双通道) | |

| BPA960/U PCI/ULTRA MAC/PC | |

| BPA970/U PCI/Ultra MAC/PC (单通道) | |

| AIC-777x, AIC-785x, AIC-786x, AIC-787x, AIC-788x, AIC-789x, 以及 AIC-3860 | aic7 |

| Always IN2000 (ISA) | in2000 |

| AMD AM53/7C4 | am53 |

# 表 B-1 (续)

| SCSI 控制器 | Linux 驱动模块 |
| :--- | :--- |
| Compaq 64-bit/66MHz PCI 光纤 HBA | cpqfc |
| Domex DMX391D | dmx391d |
| DPT SmartRAID V12O | dpt_i20 |
| DPT PM2001, PM2012A (EATA-PIO) | eata_pio |
| DPT EATA-DMA 控制器 SmartRAID Plus, III/IV 系列 (EISA/EASA/PCI) | eata_hma |
| Data Technology Corp DTC 3180/3280 | dtc |
| DTC 329x (EISA) (兼容 Adaptec 154x) | aha152 |
| Future Domain TMC-1800, TMC-18C50, TMC-18C30, TMC-3670, TMC-16x0, TMC-3260 (PCI) | fdomain |
| Future Domain TMC-8xx, TMC-950 | seagate |
| Future Future Domain PCMCIA SCSI 卡 | fdomain_cs |
| IBM ServerRAID | ips |

ICP-Vortex GDT ISA 和 EISA SCSI 控制器，GDT PCI SCSI 磁盘阵（支持多种 RAID 级别）

IDE/ATAPI 适配器（对 IDE 设备进行 SCSI 仿真，以便 SCSI 驱动访问光驱等 IDE 设备）

Initio IN-9X00/W SCSI 适配器

Initio IN-A1002W SCSI 适配器

Intraserver IT-6200U 双通道 SCSI 适配器（使用 NCR53896芯片）

Omega Logic Maker 并行 SCSI 适配器，嵌入 ZIP Plus 中

Omega PPA3 并行 SCSI 适配器，嵌入 ZIP 驱动器中

# 附录 B：磁盘驱动器

## SCSI 控制器

## Linux 驱动模块

| 设备名称 | 驱动名称/标识符 |
| :--- | :--- |
| OnStream SCSI 带 | |
| Perceptive Solutions PCI-2000I IntelliCache | osst |
| Perceptive Solutions PCI-2220I EIDE RAID | pci2220i |
| Perceptive Solutions PCI-2401I EIDE | pci2000 |
| Pro Audio Spectrum/Studio 16 (ISA) | psi2401i |
| QLogic ISP180/1/160 | pas16 |
| QLogic / Control Concepts ISP2100 SCSI-FCP | qla1280 |
| QLogic Fast SCSI FASA5XX 系列芯片 (ASLV/PCMCIA) | qlogicfc |
| QLogic ISP1020 智能 SCSI 卡 IQ-PCI, IQ-PCI-10, IQ-PCI-D (PCI) | qlogicfas |
| QLogic PMCIA SCSI 卡 | qlogicissp |
| Quantum ISA-200S, ISA-250MG | qlogic_cs |
| fdomain | fdomain |
| Seagate ST-01/ST-02 (ISA) | seagate |
| SoundBlaster SCSI 2-2 (与 Adaptec 152 兼容) (ISA) | aha152x |
| Symbios Logic SYM53C416 芯片 | sym53c16 |
| Symbios Logic SYM53C896 (支持 53XX 控制器系列，除 53C815 以及 53C810 和 53C825 控制器的 16 以下版本) | sym53c8xx |
| Tekram DC-390, DC-390W/U/F (AMD53C974 芯片组) | tmscsim |
| Trantor T128/T128F/T228 (芯片组) | t128 |
| Trantor T130B (NCR 53C400 芯片组) | g_NCR5380 |
| UltraStor 14F (ISA), 24F (EISA), 34F (VLB) | u14-34f |
| Western Digital WD7000-FAST, WD7000-FASST2, WD7000-ASC, WD7000-AX/MX/EX | wd7000 |

## 线缆与终接问题

SCSI 总线需要在末端配备终止器（terminator）才能可靠工作。终止器是一组电阻，用于指示 SCSI 总线的末端。一端是控制器卡本身，它上通常带有终止器。通常，一个 SCSI 设备有两个 SCSI 接口器，这样你可以串联多个外部 SCSI 设备。你应该在链链中的最后一个控制器上放置终止器。

某些 SCSI 控制器——例如 Adaptec AHA 154CX、154CF 和 274x（x 为任意数字）——对你所使用的线缆和终止器类型非常敏感。如果线缆不完美或终止器使用不当，这些 SCSI 卡可能会间歇性故障或完全无法工作。

为了避免过度敏感的 SCSI 卡出现问题，请使用来自信誉良好的的线缆，并使用同一供应商的线缆连接所有 SCSI 设备。线缆应符合 SCSI 2 标准，阻抗应为 132 欧姆（这是线缆的特性；你只需要确保指定值为 132 欧姆即可）。大多数 SCSI 问题都是由于线缆故障或终止不当导致的。在尝试任何操作之前，你应该检查线缆和终止器。

## 所有 SCSI ID 均显示

如果一个 SCSI 设备在所有 SCSI ID 上都出现，你可能配置了与 SCSI 控制器相同的 SCSI ID（通常为 7）。将该设备的 ID 更改另一个值。（许多设备有一个简单的开关来设置 SCSI ID；其他设备需要更改跳线帽。）

## 所有 LUN 均显示

如果一个 SCSI 设备在所有 SCSI 逻辑单元号 (`LUN`) 上都出现，该设备的固件可能存在错误——即设备 SCSI 接口内置的代码。要验证这些错误，请在启动期间使用以下命令行：

```
max_scsi_luns=1
```

如果设备在使用此选项后运行，你可以将其添加到 `/usr/src/linux-2.4/drivers/scsi/scsi_scan.c` 文件名为 `device_list` 的结构体数组的黑名单 SCSI 设备列表中。该结构的定义和数组的部分内容如下：
