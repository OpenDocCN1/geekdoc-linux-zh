
`/lib/modules/-uname*/kernel/drivers/addon/qla2200/`

### 5.6.4 加载 FASST HBA 驱动

以下章节分别解释了如何为 Red Hat 和 SuSE 加载 FASST HBA 驱动。

#### Red Hat
编辑 `/etc/modules.conf` 以确保 IBM FASST 模块在任何本地 SCSI 模块之后加载。注意示例中 ServeRAID 模块 `ips` 在 IBM FASST 模块之前加载。您的 `modules.conf` 文件应该类似于以下：

```
alias eth0 bcm5700

alias scsi_hostadapter ips

alias scsi_hostadapter2 qla2300

alias scsi_hostadapter3 qla2300
```

还应添加以下行以支持每个适配器连接多个 SCSI 设备（Red Hat Enterprise Linux 默认支持最多 40 个 LUN）：

```
options scsi_mod max_scsi_luns=128
```

保存 `modules.conf` 并退出。运行 `depmod -a` 更新 `modules.dep` 文件。

您可以通过输入以下命令手动加载光纤 HBA 模块：

```
modprobe qla2300
```

或者，您可以通过作为 ramdisk 镜像的一部分使其在启动时加载。使用以下类型构建一个随机 ramdisk 镜像：

```
mkinitrd /boot/<hostname>.img <kernel version>
```

在我们的案例中，输入了内容：

```
modprobe /initrd-storage-2.4.9-e.12summit.img 2.4.9-e.12sum
```

编辑 `/etc/grub.conf`，使引导程序知道使用新的 ramdisk 镜像。加载新 ramdisk 镜像的相关内核条目如下。此时，您也可以编辑默认项，将您的新内核和 ramdisk 镜像设置为默认值。建议在更改默认值之前测试其是否成功启动。

关闭服务器并连接 SAN 或将 SAN 上线。完成后，重启服务器。（作为重新加载 IBM FASST 模块的替代方案，使用 `modprobe -r qla2300`）附加 SAN 并重新加载 IBM FASST 模块（`modprobe qla2300`）。

如果您将连接 FASST，可以继续查看第 137 页的 5.8 部分“配置 FASST”。

#### SuSE
编辑 `/etc/sysconfig/kernel`并在 `INITRD_MODULES` 字符串后添加 `qla2x00`，其中 `x` 代表 2 或 3：

```
INITRD_MODULES="aic7xxx reiserfs qla2300"
```

下次运行 `depmod -a`。脚本 `/sbin/mk_initrd` 将此作为输入。通过启动 `mk_initrd`，将在 `/boot` 文件夹中构建新版本的初始 ramdisk。尽管这很方便，您希望构建一个新的 ramdisk 而不是替换现有的。在重启之前，您应该将内核参数 `max_scsi_luns=128` 添加到 `initub.conf` 或 `lilo.conf` 中。这是必要的，因为内核不允许全范围的 LUN（大多数默认版本如此）。如果您正在使用 LILO，请运行 `/sbin/lilo` 以提交更改。

您可以通过输入以下命令手动加载光纤 HBA 模块：

```
modprobe qla2300
```

关闭服务器并连接 SAN 或将 SAN 上线。完成后，重启服务器。（作为关闭服务器的替代方案，您可以卸载 IBM FASST 模块（`modprobe -r qla2300`），附加 SAN 并重新加载 IBM FASST 模块（`modprobe qla2300`）。

如果您将连接 FASST，可以继续查看第 137 页的 5.8 部分“配置 FASST”。

### 5.6.5 连接到 ESS

Linux 驱动程序未提供连接到 ESS 时使用的多路径驱动程序（如其他所示）。然而，可以使用 IBM 提供的名为 Storage Device Driver (`SDD`)的多路径扩展来实现冗余路径和负载均衡。`SSD` 的特别优势是它可以独立于 HBA 设备驱动程序运行。因此，以下内容适用于任何兼容 ESS 的 HBA。`SSD` 在 `/dev` 系统中引入了一个名为 `vpath` 的新树。这是 `SSD` 不支持 LVM 的原因之一。在 LVM 中，`/dev` 目录的组件是硬编码的。`SSD` 由一个驱动程序和一个服务器守护进程组成。服务器守护进程始终后台运行（在安装 `SSD` 驱动程序后自动启动）。它定期扫描路径以指示故障。路径可以具有 `OPEN`、`CLOSE DEAD`、`DEAD` 和 `INVALID` 状态。`SSD` 服务器根据表 5-2 回收路径并更改其状态。

严格来说，请注意通过交换机连接到多个 ESS 端口的单光纤通道适配器主机系统被认为是多路径连接，但并不足够（`SDD` 将不会提供多路径功能，*此处原文不完整*）。

| Command | Description |
| --- | --- |
| sdd restart | 卸载 SDD 驱动程序（需要当前正在使用的 vpath 设备），然后加载 SDD 驱动程序并自动为磁盘设备配置多路径访问 |

## 使用多命令进行 SDD 配置

若要在系统上加载并配置 SDD，请手动切换到目录 `/opt/IBMSdd` 并输入命令 `insmod modulename`（在我们的案例中，对于 SuSE SLES 8，模块名为 `sdd-mod.o-2.4.19.SuSE-152.k_smp-2.4.19-233`）。

如果您不知道确切的内核版本，请使用命令 `uname -a` 列出内核版本。

要验证 SDD sdd-mod 驱动是否已加载，请输入 `cat /proc/modules`。

要验证驱动程序是否正确加载，请输入 `lsmod`。图 5-20 显示了预期输出示例。

| linux:/etc ~ lsmod | Size Used by | Tainted: P |
| --- | --- | --- |
| videov | 6272 | 0 (autoclean) |
| ide-cd | 30564 | 0 (autoclean) |
| isa-smp | 32608 | 0 (unused) |
| ipv6 | 183636 | -1 (autoclean) |
| sdd-mod | 355256 | 0 |
| st | 29260 | 0 (autoclean) (unused) |
| sr_mod | 14520 | 0 (autoclean) (unused) |
| cdrom | 29120 | 0 (autoclean) [Ide-cd sr_mod] |
| sg | 30272 | 0 (autoclean) |
| joydev | 6112 | 0 (unused) |
| evdev | 4800 | 0 (unused) |
| input | 3448 | 0 [Joydev evdev] |
| usb-uhci | 24492 | 0 (unused) |
| usscore | 64832 | 1 [usb-uhci] |
| af_packet | 15112 | 1 (autoclean) |
| bcm5700 | 83592 | 1 |
| lvm-mod | 68192 | 0 (autoclean) |
| qla2300 | 202944 | 0 |
| aic7xxx | 129752 | 2 |

图 5-20 加载的 SDD 模块

切换到 `/opt/IBMSdd/bin` 目录并如图 5-21 所示输入 `cfgvpath query`。

```
linux:/opt/IBMSdd/bin # cfgvpath query

dev/sda ( 8, 0) host=1 ch=0 id=13 lun=0 vid=IBM-ESXS pid=ST318452LC

serial=xxxxxxxxxxxx

ctrl_flag=0 ch=0 ctrl_nbr=0 df_ctrl=0 X

dev/sdb ( 8, 16) host=2 id=0 lun=0 vid=IBM pid=2105800

serial=70024678

dev/sdc ( 8, 32) host=3 id=0 lun=0 vid=IBM pid=2105800

ctrl_flag=0 ch=0 ctrl_nbr=0 df_ctrl=0
```
