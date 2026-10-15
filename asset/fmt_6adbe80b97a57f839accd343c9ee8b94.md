
```
UDEV[132407.004453] add /bus/usb_storage

KERNEL[132407.005798] add /devices/pci0000:0000:0000:11.0/0002:04.0/usb1-1/1-1:11.0/host33

UDEV[132407.007385] add /devices/pci0000:0000:0000:11.0/0002:04.0/usb1-1/1-1:11.0/host33 (scsi)

KERNEL[132408.008331] add /devices/pci0000:0000:0000:11.0/0002:04.0/usb1-1/1-1:11.0/host33:0:0 (scsi)

KERNEL[132408.008355] add /devices/pci0000:0000:0000:11.0/0002:04.0/usb1-1/1-1:11.0/host33:0:0 (scsi)

KERNEL[132408.008363] add /devices/pci0000:0000:0000:11.0/0002:04.0/usb1-1/1-1:11.0/host33:0:0:0 (scsi_disk)

KERNEL[132408.008370] add /devices/pci0000:0000:0000:11.0/00020002.04.0/usb-1/1-1:11.0/host33:0:0:0:0 (scsi_device)

KERNEL[132408.009221] add /devices/pci0000:0000:0000:11.0/0002:04.0/usb1-1/1:11.0/host33/target33:0:0:0:0 (bsg)

UDEV[132408.009408] add /devices/pci0000:0000:0000:11.0/0002:04.0/usb/1-1/1-1:1.0/host/target33:0:0 (scsi)

UDEV[132408.010073] add /devices/pci0000:0000:0000:11.0/000204.0/usb/1-1/1-1:1.0/host/target33:0:3:0:0 (scsi)

UDEV[132408.010937] add /devices/pci0000:0000:0000:11.0/0002:04.0/usb/1-1/1-1:1.0/host/target33:0:3:0:0/scsi_device/33:0:0 (scsi_device)

UDEV[132408.011628] add /devices/pci0000:0000:0000:11.0/000204.0/usb/1-1/1-1:1.0/host/target33:0:0:0/sc/_disk (scsi_disk)
```

# 管理内核模块

Linux 内核通常会自动加载所需的设备驱动，但你可能需要手动加载适当的内核模块。一些命令用于管理内核模块。表格 16.2 提供了概述。

加载内核模块的另一种方法是通过 `/etc/modules-load.d` 目录。在该目录中，你可以创建文件来自动加载未通过 udev 方法加载的模块。

## 第 16 章：基础内核管理

### 表 16.2 Linux 内核模块管理概述

| 命令 | 用途 | 备注 |
|---|---|---|
| `lsmod` | 列出已加载的内核模块 | 关键知识点 |
| `modinfo` | 显示内核模块信息 | |
| `modprobe` | 加载内核模块，包括其依赖项 | |
| `modprobe -r` | 卸载内核模块，并考虑内核模块的依赖关系 | |

处理内核模块时使用的第一个命令是 `lsmod`。该命令列出当前正在使用的内核模块，包括被此特定模块使用的模块。列表 16.5 显示了 `lsmod` 命令的前10行输出。

#### 列表 16.5 使用 `lsmod` 列出已加载的模块

```
root@server1 udev]# lsmod | head

Module Size Used

ipt_MASQUERADE 12880 3

xt_CHECKSUM 12549 1

ip6_rpfilter 12546 1

target_core_pscsi 18810 0

target_core_file 18030 0

target_core_iblock 18177 0

iscsi_target_mod 278732 1

target_core_mod 299412 5 target_core_iblock,target_core_pscsi,iscsi_target_mod,target_core_file

ip6_REJECT 12939 2
```

> 提示：许多 Linux 命令在不同的列中显示输出，并不清楚哪一列是哪种信息。这些命令中的大多数在命令输出的第一行都有一个头行。因此，如果你不确定某个命令看到的内容，可以将命令的输出通过到 `head` 来查看是否有头文件，或者将命令输出通过到 `less`，这允许你轻松地向上翻到命令输出的第一行。

如果你想获取有关特定内核模块的更多信息，可以使用 `modinfo` 命令。它提供了关于特定内核模块的完整信息，包括两个有趣的部分：`alias`（别名）和 `parms`（参数）。模块别名是另一个用于标识该模块的名称。`parms` 行指的是在加载模块时可以设置的参数。（在本章稍后的“管理内核模块参数”部分中，你将学习如何处理内核参数。）列表 16.6 显示了 `modinfo` 命令的部分输出。

#### 列表 16.6 使用 `modinfo` 显示模块信息

```
root@server1 udev# modinfo e1000

filename:       /lib/modules/3.10.0-123.el7.x86_64/kernel/drivers/net/ethernet/intel/e1000/ko

version:        3.7.21-kAPI

license:        GPL

description:    Intel(R) PRO/1000 Network Driver

author:         Intel Corporation, <linux.nics@intel.com>

srcversion:     BBDA267AB1A3DD6045C0D

alias:          pci:0000086d00002e6sv*sd*bc*sc*i*

depends:

intree:         3.10.0-123.el7.x86_64 SMP mod_unload modversions

signer:         CentOS Linux kernel signing key

sig_key:        BC:83D0:FE:70:C2:FB:AE:1C:58:BA:EB:A9:E5:93:61:FC:F4

sig_hashalgo:   sha256

par:            TxDescriptors:Number of transmit descriptors (array of int)

par:            RxDescriptors:Number of receive descriptors (array of int)

par:            Speed:Speed setting (array of int)

par:            Duplex:Duplex setting (array of int)

par:            AutoNeg:Advertised auto-negotiation setting (array of int)

par:            FlowControl:Flow setting (array of int)

par:            XsumRX:Disable or enable Checksum offload (array of int)

par:            TxIntDelay:Transmit Delay (array of int)

par:            TxAbsIntDelay:Transmit Interrupt Delay (array of int)

par:            RxIntDelay:Receive Interrupt Delay (array of int)

par:            RxAbsIntDelay:Receive Interrupt Delay (array of int)

parm: InterruptThrottleRate:Throttling Rate (array of int)

parm: SmartDownEnable:PHY power down (array of int)
```
