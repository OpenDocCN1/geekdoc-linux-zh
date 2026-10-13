
```
ok dealias
screen /iommu,e0000000/sbus,e000100/cpisix2,0
disk5 /iommu/sbus/espdmaf,400000/espf,800000/sd0,0
floppy /obio/SUNW,fdtw
scsi /iommu/sbus/espdmaf,400000/espf,800000/sd3,0
net-au /iommu/sbus/ledmaf,400010:aui/le0,c000000
net-tpe /iommu/sbus/ledmaf,400010:tpe/le0,c000000
disk /iommu/sbus/espdmaf,400000/espf,800000/sd3,0
cdrom /iommu/sbus/espdmaf,400000/espf,800000/sd0,d
tape /iommu/sbus/espdmaf,400000/espf,800000/st4,0
tape0 /iommu/sbus/espdmaf,400000/espf,800000/st6,0
tape1 /iommu/sbus/espdmaf,400000/espf,800000/st5,0
disk3 /iommu/sbus/espdmaf,400000/espf,800000/sd3,0
disk2 /iommu/sbus/espdmaf,400000/espf,800000/sd2,0
disk1 /iommu/sbus/espdmaf,400000/espf,800000/sd1,0
disk0 /iommu/sbus/espdmaf,400000/espf,800000/sd0,1
tty /obio/zio,100000:b
ttya /obio/zio,100000:a
keyboard1 /obio/zio,0:force
keyboard /obio/zio,0
```

除非创建永久别名，否则用户定义的别名会在系统重置后丢失。如果你想创建永久别名，可以手动存储在名为 `nvram` 的非易失性内存（NVRAM）分区中，或者使用 `nvalias` 和 `nunalias` 命令。下一节描述了如何在 Sun 系统上配置 NVRAM 中的永久设置。

# OpenBoot 非易失性内存 (NVRAM)

系统配置变量存储在系统的 NVRAM 中。这些 OpenBoot 变量决定了启动配置和通信特性。你可以修改配置变量的值，任何更改都会保留。表 2.7 描述了 OpenBoot 变量、默认值及其功能。

## 表 2.7 NVRAM 变量

| 变量 | 默认 | 描述 |
| --- | --- | --- |
| auto-boot? | true | 通电后自动启动。 |
| boot-command | boot | 启动时执行的命令。 |
| boot-device | net | 启动设备。 |
| boot-file | | 传递给启动程序的参数。 |
| diag-device | disk | 诊断启动设备。 |
| diag-file | | 传递给启动程序的参数。 |
| diag-switch? | false | 如果为真，以诊断模式运行。 |
| fcode-debug? | false | 如果为真，包含 FCode 名称。 |
| input-device | keyboard | 控制台输入设备。 |
| nvramrc | | NVRAM 的内容。 |
| oem-banner | | 自定义 OEM 横幅（通过 oem-banner? 启用）。 |
| oem-banner? | false | 如果为真，使用自定义 OEM 横幅。 |

### 第一节 第一部分

### 表 2.7 继续 NVRAM 变量

| 变量 | 默认 | 描述 |
|---|---|---|
| oem-logo | 无默认 | 字节数组自定义 OEM 标志（通过 oem-logo? 启用）。以十六进制显示。 |
| oem-logo? | false | 如果为真，使用自定义 OEM 标志；否则使用 Sun 标志。 |
| output-device | screen | 控制台输出设备（通常为 tty 或 tttyb）。 |
| sbus-probe-list | 0123 | 探测哪些 SBus 槽以及探测顺序。 |
| screen-#columns | 80 | 屏幕列数（字符）。 |
| screen-#rows | 34 | 屏幕行数（行）。 |
| security-#badlogins | 无默认 | 密码错误的尝试次数。 |
| security-mode | none | 固件安全级别（选项：none、command 或 for）。 |
| security-password | 无默认 | 固件安全密码（从不显示）。 |
| use-nvramrc | false | 如果为真，在系统启动期间执行 NVRAM 中的命令。 |

> 较的 SPARC 系统因为使用较旧版本的 OpenBoot，可能会使用不同的默认值或不同的配置变量。如前，本文描述的是 OpenBoot 版本 3。

可以使用表 2.8 中列出的命令查看并更改 NVRAM 配置变量。

## 表 2.8 查看或修改配置变量

| 命令 | 描述 |
|---|---|
| password | 设置密码。 |
| printenv | 显示每个变量的当前值和默认值。要显示命名变量的当前值，输入 `printenv <parameter name>`。 |
| setenv variable value | 将变量设置为给定的十进制或文本值。更改是永久的，但通常在重置后才生效。 |

## 第 2 章 OPENBOOT 65

### 命令变量

- `set-default` 将变量值重置为工厂默认值。
- `set-defaults` 将所有变量值重置为工厂默认值。

以下示例说明了表 2.8 中命令的用法。

所有命令均在 `ok` OpenBoot 提示符下输入。

```
ok printenv
```

系统响应如下：

| 变量名 | 值 | 默认值 |
|---|---|---|
| tpe-link-test? | true | true |
| scsi-initiator-id | true | 7 |
| keyboard-click? | false | false |
| keymap | | |
| tty-rts-dtr-off | false | false |
| tty-ignore-cd | true | true |
| tty-rts-dtr-off | false | false |
| tty-ignore-cd | 9600,8,n,1,- | 9600,8,n,1,- |
| tty-mode | 9600,8,n,1,- | 9600,8,n,1,- |
| pciat-probe-list | 1,2,3,4 | 1,2,3,4 |
| pcib-probe-list | 1,2,3 | 1,2,3 |
| mfg-mode | off | off |
| diag-level | max | max |
| #power-cycles | | 69 |
| system-board-serial# | | |
| system-board-date | | |
| fcode-debug? | false | false |
| output-device | screen | screen |
| input-device | keyboard | keyboard |
| load-base | 16384 | 16384 |
| boot-command | boot | boot |
| auto-boot? | false | true |
| watchdog-reboot? | false | false |
| diag-file | | |
| diag-device | net | net |
| boot-file | | |
| boot-device | disk:a disk net | disk net |
| local-mac-address? | false | false |
| ansi-terminal? | true | true |

### 第一节 第一部分

根据你系统中运行的 OpenBoot 版本，`printenv` 命令可能会显示略有不同的结果。为此，我使用了一个运行 OpenBoot 3.15 版本的系统。

| | | |
|---|---|---|
| screen-#columns | 80 | 80 |
| screen-#rows | 34 | 34 |
| silent-mode? | false | false |
| use-nvramrc | false | false |
| nvramc | | |
| security-mode | none | | |
