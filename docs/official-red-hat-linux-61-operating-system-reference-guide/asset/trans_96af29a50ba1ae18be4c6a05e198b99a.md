

![](img/eda1471ab4ce718c791c97a85559a478_270_0.png)

关于如何在安装后创建引导磁盘的说明，请参阅 `mkboot-disk` 手册页。如果您对内核进行了任何更改，请务必创建一个新的引导磁盘。

### 10.24 完成安装

完成后，安装程序将显示**Complete**（完成）对话框（如图 10–49 *Complete Dialog*（完成对话框）所示），提示您重新启动计算机。请从软盘驱动器中取出任何软盘（除非您跳过了 LILO 安装，在这种情况下您必须使用安装期间创建的引导磁盘），或者，如果您的系统是从 CD-ROM 引导的，请取出 Red Hat Linux CD。

### 图 10–49 完成对话框

![](img/eda1471ab4ce718c791c97a85559a478_271_0.png)

选择 OK 以重新启动您新安装的系统。在计算机的正常开机自检序列完成后，您应该会看到 LILO 的标准 boot: 提示符，此时您可以执行以下任一操作：

- 按 [Enter] -- 引导 LILO 的默认引导条目（如图 10-25，在 LILO 配置对话框中选择可引导分区所示）。
- 输入引导标签，然后按 [Enter] -- 引导与该引导标签对应的操作系统。
- 等待 -- 在 LILO 超时期间（默认为五秒）结束后，LILO 将自动引导默认引导条目。

采取适当的操作来引导 Red Hat Linux。您应该会看到一两屏信息滚动显示。最终，您应该会看到图形登录屏幕或 login: 提示符。

恭喜！您的 Red Hat Linux 安装已完成！

## 第三部分 附录

## A 通用参数和模块

本附录旨在说明某些驱动程序可能需要的*部分*参数。应当指出的是，在大多数情况下，这些额外参数是不必要的。附录中还包含网络硬件列表以及该硬件所需的关联模块。

请记住，如果您尝试使用的设备需要这些参数之一，且对该设备的支持*未*编译进内核，那么将参数添加到 LILO 引导命令的传统方法将不会起作用。作为模块加载的驱动程序要求在加载模块时指定这些参数。Red Hat Linux 安装程序允许您在加载驱动程序时选择指定模块参数。

### A.1 关于内核驱动的说明

在安装 Red Hat Linux 期间，内核所支持的文件系统和其他驱动程序存在一些限制。然而，安装完成后，系统支持 Linux 下可用的所有文件系统。在安装时，模块化内核支持 (E)IDE 设备（包括 ATA/PI CD-ROM 驱动器）、SCSI 适配器和网卡。此外，还支持所有鼠标、SLIP、CSLIP、PPP、PLIP、FPU 仿真、控制台选择、ELF、SysV IPC、IP 转发、防火墙和流量统计、反向 ARP、QIC 磁带以及并行打印机。

由于 Red Hat Linux 支持在许多不同类型的硬件上进行安装，许多驱动程序（包括 SCSI 适配器、网卡和许多 CD-ROM 的驱动程序）并未内置于安装过程中使用的 Linux 内核中；相反，它们作为**模块**提供，并在安装过程中根据需要加载。如有必要，您在加载这些模块时将有机会为它们指定选项，实际上，这些驱动程序会忽略您在**boot :** 提示符下为其指定的任何选项。

安装完成后，您可能希望重新构建一个包含针对特定硬件配置支持的内核。有关构建自定义内核的信息，请参见第 2.8 节 *Building a Custom Kernel*（构建自定义内核）。请注意，在大多数情况下，自定义构建的内核并非必要。

### A.2 CD-ROM 模块参数

> **请注意**
>
> 并非所有列出的卡片都受到支持。请检查 Red Hat 在 http://www.redhat.com/support/docs/hardware.html 网站上的硬件兼容性列表，以确保您的卡片得到支持。

`hdx=cdrom` 参数是更常用的参数之一，可以在 boot 提示符下输入，因为它处理 IDE/ATAPI CD-ROM 的支持，而这属于内核的一部分。

在下面的表格中，大多数未列出参数的模块要么能够自动探测以找到硬件，要么需要手动更改模块源代码中的设置并重新编译。

表 A–1 硬件参数

| 硬件 | 模块 | 参数 |
| :--- | :--- | :--- |
| ATAPI/IDE CD-ROM 驱动器 | | hdx=cdrom |
| Aztech CD268-01A, Orchid CD-3110, Okano/Wearnes CDD110, Conrad TxC, CyCDROM CR520, CyCDROM CR540 (非 IDE) | aztcdo | aztcd=io_port |
| Sony CDU 31A 或 33A CD-ROM | cdu31a.o | cdu31a=io_port,IRQ[,PAS] cdu31a_port=base_addr cdu31a_irq=irq |
| 配有 cm260 主机适配卡的 Philips/LMS CDROM 206 驱动器 | cm206.o | cm206=io_port,IRQ |
| Goldstar R420 CD-ROM | gscd.o | gscd=io_port |
| ISP16、MAD16 或 Mozart 声卡 CD-ROM 接口 (OPTi 82C928 和 OPTi 82C929)，配 Sanyo/Panasonic、Sony 或 Mitsumi 驱动器 | isp16.o | isp16=io_port, IRQ, dma,drive_type isp16_cdrom_base=io_port isp16_cdrom_irq=IRQ isp16_cdrom_dma=dma isp16_cdrom_type=drive_type |
| Mitsumi CD-ROM，标准版 | mcd.o | mcd=io_port,IRQ |
| Mitsumi CD-ROM，实验版 | mcdx.o | mcdx=io_port_1, IRQ_1, io_port_n, IRQ_n |
| Optics storage 8000 AT CD-ROM "Dolphin" 驱动器；Lasermate CR328A | optcd.o | optcd=io_port |
| 兼容 SB Pro 16 | sbpcd.o | sbpcd=io_port,sb_pro_Setting |
| Sanyo CDR-H94A | sjcd.o | sjcd=io_port sjcd_base=io_port |
| Sony CDU-535 & 531 (某些 Procomm 驱动器) | sonycd535.o | sonycd535=io_port |

以下是这些模块使用的一些示例：

表 A-2 硬件参数配置示例

| 配置 | 示例 |
| :--- | :--- |
| ATAPI CD-ROM，跳线设置为第二个 IDE 通道的主设备 | hdc=cdrom |
| 非 IDE Mitsumi CD-ROM，端口 340，IRQ 11 | mcd=0x340,11 |
| 三个非 IDE Mitsumi CD-ROM 驱动器，使用实验驱动程序，io 端口 300、304 和 320，IRQ 分别为 5、10 和 11 | mcdx=0x300,5,0x304,10,0x320,11 |
| Sony CDU 31 或 33，端口 340，无 IRQ | cdu31=0x340,0 cdu31_port=0x340 cdu31a_irq=0 |
| Aztech CD-ROM，端口 220 | aztcd=0x220 |
| Panasonic 类型 CD-ROM，位于 SoundBlaster 接口，端口 230 | sbpcd=0x230,1 |
| Philips/LMS cm206 和 cm260，IO 340 和 IRQ 11 | cm206=0x340,11 |
| Goldstar R420，IO 300 | gscd=0x300 |
| 位于 MAD16 声卡上的 Mitsumi 驱动器，IO 地址 330 和 IRQ 1，探测 DMA | ispl6=0x330,11,0,Mitsumi |
| Sony CDU 531，IO 地址 320 | sonycd535=0x320 |

**请注意**

大多数较新的 Sound Blaster 卡都带有 IDE 接口。对于这些卡，您无需使用 sbpcd 参数，只需使用 hdcx 参数即可。

### A.3 SCSI 参数

表 A-3 SCSI 参数

| 硬件 | 模块 | 参数 |
| :--- | :--- | :--- |
| NCR53c810/820/720, NCR53c700/710/700-66 | 53c7,8xx.o | |
| AM53/79C974 PC-SCSI 驱动程序 Qlogic PCI-Basic | AM53C974.o | AM53C974=host-scsi-id, target-scsi-id, max-rate, max-offset |
| 大多数带有 "BT" 部件号的 Buslogic（现为 Mylex）卡 | BusLogic.o | BusLogic_Options=option,option,... (请参阅 ..drivers/scsi/ 中的 README.BusLogic) |
| | NCR53c406a.o | ncr53c406a=io_port[, IRQ[, FASTPIO]] ncr53c406a io=io_port irq=IRQ fastpio=FASTPIO |
| Advansys SCSI 卡 | advansys.o | |
| Adaptec AHA 152x | aha152x.o | aha152x=io_base, IRQ, scsi_id, reconnect, parity |
| Adaptec AHA 1542 | aha1542.o | aha1542=io_base, bus0, busoff, dmaspeed |
| Adaptec AHA 1740 | aha1740.o | |
| Adaptec AHA-274x, AHA-284x, AHA-29xx, AHA-394x, AHA-398x, AHA-274x, AHA-274xT, AHA-2842, AHA-2910B, AHA-2920C, AHA-2930/U/U2, AHA-2940/W/U/WW/AU/U2W/U2/U2B/, U2BOEM, AHA-2944D/WD/UD/UWD, AHA-2950U2/W/B, AHA-3940/W/U/WW/, AUW/U2W/U2B, AHA-3950U2D, AHA-3985/U/WW/UW, AIC-777x, AIC-785x, AIC-786x, AIC-787x, AIC-788x, AIC-789x, AIC-3860 | `aic7xxx.o` | aic7xxx=string |
| Data Technology Corp DTC3180/3280 | `dtc.o` | |

