
5. 使用什么转义字符串在 shell 提示符中打印日期字符串？

A. `\a`

B. `\d`

C. `\h`

D. `\H`

6. 使用什么转义字符串在 shell 提示符中打印完整主机名？

A. `\a`

B. `\d`

C. `\h`

D. `\H`

7. 使用什么转义字符串在 shell 提示符中打印短主机名？

A. `\a`

B. `\d`

C. `\h`

D. `\H`

8. 使用什么命令在保持所有环境设置的情况下加载另一个 shell 脚本？

A. `. source`

B. `. sh`

C. `. .`

D. `. /`

9. 在 shell 初始化执行 `.profile` 期间，使用什么命令可以显示 "Status OK" 字符串？

A. `. printf "Status OK",`

B. `. printf "Status OK",`

C. `. echo "Status OK",`

D. `. cat "Status OK" > /dev/null`

10. `test` 命令使用哪个参数来判断文件是否为特殊块设备？

A. `-b`

B. `-block`

C. `-blockfile`

D. `-bf`

## 答案

1. C. Bourne shell 初始化脚本的名称是 `.profile`。

2. C. Bourne shell 初始化文件的全站骨架文件名称是 `/etc/skel/local.profile`。

3. A. `TERM=vt220` 将将终端类型的环境变量设置为 `vt220`。

4. A. ASCII 响响字符是 `\a`。

5. B. 日期字符串由 `\d` 表示。

6. D. shell 提示符由 `\H` 设置。

7. C. 短主机名由 `\h` 表示。

8. C. source 命令是 `". "`。

9. C. 命令 `echo "Status OK"` 将显示 "Status OK" 字符串。

10. A. `-b` 用于测试特殊块设备。

# 磁盘配置与命名

在本章中，你将：

- 了解 Solaris 物理设备名称
- 了解 Solaris 逻辑设备名称
- 学习使用 `format` 和 `dmesg` 命令查看系统硬件
- 学习使用 `prtconf` 命令显示系统配置

磁盘配置和命名是一项关键的管理任务。Solaris 提供了多种互补的方案来命名磁盘、文件系统、切和分区，我们将在本章中探讨。

## 物理与逻辑设备名称

理解 Solaris 硬件最具挑战性的方面之一是 Solaris 管理设备使用的名称和引用。Solaris 使用一套非常特定的命名约定将物理设备与操作系统上的实例关联起来。对于新接触 Solaris 的管理员来说，这可能非常困惑。此外，设备也可以通过设备名称引用，该名称是配置后在 `/dev` 目录中创建的文件。例如，某个磁盘的物理设备名称可能是 `/dev/pci@10.0/pci@1.1/ide@3/dad@0,0`，它与文件设备 `/dev/dskc0d0` 关联。在 Windows 中，磁盘仅通过驱动器号命名（C:, D:, E 等），而在 Linux 中，设备文件被简化（例如  为 `/dev/hda`，SCSI 硬盘为 `/dev/sda`）。复杂的 Solaris 逻辑设备名称和物理引用的优点在于，只需查看名称即可轻松解释每个设备的特性。通过上面的磁盘示例，我们可以看到 IDE 硬盘位于 PCI 总线上的目标 0 上。当我们查看系统可用空间时，可以通过设备名称轻松识别同一块磁盘上的切（slices）：

```bash
df -k
Filesystem kbytes used avail capacity Mounted on
/proc 0 0 0 0% /proc
/dev/dsk/c0t0d0s0 192888 615991 1307058 33% /
```

## 第 12 章：磁盘配置与命名

257

```
/sbus0IF,0/SUNW,fas2,880000/sdb,0 25 "sd"
/sbus0IF,0/SUNW,fas2,880000/st2,0 9 "st"
/sbus0IF,0/SUNW,880000/sde,0 28 "sd"
/sbus0IF,0/SUNW,880000/st5,0 12 "st"
/sbus0IF,0/SUNW,880000/sdd,0 27 "sd"
/sbus0IF,0/SUNW,880000/st4,0 11 "st"
/sbus0IF,0/SUNW,880000/sdc,0 29 "sd"
/sbus0IF,0/SUNW,880000/st6,0 13 "st"
/sbus0IF,0/CS2431d,cd00000 0 "audiocs"
/sbus0IF,0/dma0a,8100 0 "dma"
/sbus0IF,0/dma0a,8100/esp,8000 0 "esp"
/sbus0IF,0/dma0a,8100/esp,8000/sd0,0 30 "sd"
/sbus0IF,0/dma0a,8100/esp,8000/sd1,0 31 "sd"
/sbus0IF,0/dma0a,8100/esp,8000/sd2,0 32 "sd"
/sbus0IF,0/dma0a,8100/esp,8000/sd3,0 33 "sd"
/sbus0IF,0/dma0a,8100/esp,8000/sd4,0 34 "sd"
/sbus0IF,0/dma0a,8100/esp,8000/sd5,0 35 "sd"
/sbus0IF,0/dma0a,8100/esp,8000/sd6,0 36 "sd"
/sbus0IF,0/dma0a,8100/esp,8000/sc0,0 14 "st"
/sbus0IF,0/dma0a,8100/esp,8000/st1,0 15 "st"
/sbus0IF,0/dma0a,8100/esp,8000/st2,0 16 "st"
/sbus0IF,0/dma0a,8100/esp,8000/st3,0 17 "st"
/sbus0IF,0/dma0a,8100/esp,8000/st4,0 18 "st"
/sbus0IF,0/dma0a,8100/esp,8000/st5,0 19 "st"
/sbus0IF,0/dma0a,8100/esp,8000/st6,0 20 "st"
/sbus0IF,0/sbusmem6,0 15 "sbus"
/sbus0IF,0/sbusmem8,0 13 "sbus"
/sbus0IF,0/sbusmem8,0 14 "sbus"
/sbus0IF,0/ctbrese1,0 0 "citrix"
/sbus0IF,0/SUNW,hme,8c00000 0 "hme"
/sbus0IF,0/zsf,1000000 1 "zs"
/sbus0IF,0/zsf,1100000 0 "zs"
/sbus0IF,0/SUNW,bppe,cd00000 0 "bpp"
/sbus0IF,0/lebuffer0,40000/10e6,00000 0 "le"
/sbus0IF,0/lebuffer0,40000/10e6,00000 1 "le"
/sbus0IF,0/SUNW,hme,8c00001 1 "hme"
/sbus0IF,0/SUNW,fdwsof,1400000 0 "fd"
/opt/iscar 0 "options"
/pseudo 0 "pseudo"
```

在这里，我们可以看到网络接口 `/sbus/1f0/SUNW,hme,2c80000` 的条目，以及磁盘分区和 SBUS 总线。对于像 Sun Blade 1020 这样的基于 PCI 的系统，输出将如下：

```
/pci1f,0 0 "pcips"
/pci1f,0/isa7,0 "ebus"
/pci1f,0/isa7?dma0a,0,0 "power"
/pci1f,0/isa7?dma0a,0,0 "idadma"
/pci1f,0/isa7/parallel0,378 0 "ecpp"
/pci1f,0/isa7/floppya,0,3f0 0 "fd"
/pci1f,0/isa7/serial02,8 1 "su"
/pci1f,0/isa7/serial03,3f8 0 "su"
/pci1f,0/pmu3 0 "pmbus"
/pci1f,0/pmu3/i2c0 0 "smbus"
/pci1f,0/pmu3/i2c0@30 0 "max1676"
/pci1f,0/pmu3/i2c00/card-reader@40 0 "smi2c"
/pci1f,0/pmu3/i2c00/dimm0a 0 "seeprom"
```

284 Certified Solaris 9.0 System and Network Administrator-in-One Guide

258

```
/pci1f,0/pmu03/fan-control@ 0 "grfans"

/pci1f,0/pmu03/bm0@ 0 "grppm"

/pci1f,0/pmu03/beep@ 0 "grbeep"
```
