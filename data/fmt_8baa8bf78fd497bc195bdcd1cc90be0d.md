
`echo 1 > /proc/sys/kernel/sysrq`

这将 `sysrq` 文件的值从 0（关闭）更改 1（开启）。系统请求键的目的是允许通过简单的键组合立即指示内核执行许多重要活动，如立即关闭或重启系统、同步所有文件系统或将重要信息转储到控制台。此功能在使用开发内核或遇到系统冻结时最有用。然而，对于无人值守控制台，这是一个安全风险，Red Hat Linux 默认关闭它。参考 `/usr/src/linux-2.4/Documentation/sysrq.txt` 获取更多关于系统请求键的信息。

少数 `/proc/sys/` 配置文件包含多个值。为了正确向它们发送新值，在通过 `echo` 命令传递的每个值之间放置空格字符，例如所示：
```
echo 4 2 45 > /proc/sys/kernel/acct
```

![85ce181a0f26bec69ad7f04bbf6fe_188_0.png]

你使用 `echo` 命令进行的任何配置更改在系统重启时都会消失。要让你的配置更改在系统启动时生效，请确保对系统启动文件进行相应的更改。

### `/proc/sys/` 目录
`/proc/sys/` 目录包含多个控制运行中内核不同方面的子目录。

#### `/proc/sys/dev/`
此目录为系统上的特定设备提供参数。大多数系统至少有两个目录，`cdrom` 和 `raid`，但自定义内核可以有其他目录，例如 `parport`，它提供了在多个设备之间共享一个并行端口。`cdrom` 目录包含一个名为 `info` 的文件，它揭示了许多重要的光驱参数，如列表 6-14 所示。

**列表 6-14：`cat /proc/dev/cdrom/info` 的输出**
```
CD-ROM information, Id: cdrom.c 3.12 2000/10/18

drive name:           hdc

drive speed:          32

drive # of slots:      1

Can close tray:       1

Can open tray:        1

Can lock tray:        1

Can change speed:     1

Can select disk:      0

Can read multisession: 1

Can read MCN:         1

Reports media changed: 1

Can play audio:       1

Can write CD-R:      0

Can write CD-RW:     0

Can read DVD:        0

Can write DVD-R:     0

Can write DVD-RAM:    0
```
