
# service smb start 立即启动 Samba 服务

Starting SMB services: [ OK ]

`service` 命令从 `/etc/init.d` 目录启动脚本（在本例中为 `smb`）。大多数脚本支持 `start` 和 `stop` 选项，同时也支持其他功能。以下是使用 `service` 启动和停止服务的方法：

```
# service smb 显示用法说明（不带选项）
Usage: /etc/init.d/smb [start|stop|try-restart|restart|force-reload|reload|probe]
```

```
# service smb restart 重启 Samba 服务（先停止，后启动）
Shutting down Samba SMB daemon done
Starting Samba SMB daemon done
```

```
# service smb try-restart 重启 Samba 服务（如果已运行）
Checking for Samba SMB daemon done
Shutting down Samba SMB daemon done
```

```
# service smb reload 重新加载 smb.conf 文件中的设置
Reloading Samba SMB daemon done
```

```
# service smb status 检查 Samba 服务是否运行 (smbd)
Checking for Samba SMB daemon done
```

```
# service smb stop 停止 Samba 服务
Shutting down Samba SMB daemon done
```

`/etc/init.d` 中包含的任何 init 脚本都可以通过此命令启动，但并非所有脚本都支持显示的所有功能。然而，大多数脚本可以在不带选项的情况下使用用法说明（如上面的第一个示例）。

虽然 `service` 命令会立即启动运行级别脚本，但要让服务在启动时或运行级别期间自动启动，可以使用 `chkconfig`。通过 `chkconfig`，你可以列出服务并按运行级别开启或关闭它们。

```
# chkconfig smb 开启 Samba 服务
# chkconfig --list 列出运行级别的开启或关闭状态
smb 0:off 1:off 2:off 3:on 4:off 5:on 6:off
# chkconfig --list 列出所有服务并指示开启或关闭
# chkconfig --level 2 smb off 关闭运行级别 2 的 Samba 服务
```

## 第 10 章：系统管理

当 init 脚本被添加到 `/etc/init.d` 时，`chkconfig` 需要感知它的存在。当新的 init 脚本是 rpm 的一部分时，这会自动完成；如果你添加了自己的 init 脚本，则需要手动完成。运行以下命令即可：

```
# chconfig --add mydaemon      将 /etc/init.d/mydaemon 添加到 chconfig
```

虽然你可以使用 `init` 命令更改任何运行级别，包括 `init 0`（关机）和 `init 6`（重启），但也有特定的命令用于停止 Linux。`halt`、`reboot`、`poweroff` 和 `shutdown` 等命令的优势是它们允许你在关机发生之前停止某些功能。例如：

> 警告！如果你打算打算关闭系统，请不要尝试运行这些命令，尤其是在远程系统上。

- `reboot`      重启计算机
- `halt -h`      关机前不向硬盘同步数据
- `halt -h`      关机前将硬盘置于待机模式
- `shutdown 10`  警告用户后十分钟内关机
- `shutdown -r 10`  警告用户后十分钟内重启
- `shutdown 10 Bye'!` 关机前向用户发送自定义消息

除了 `reboot` 和 `init 6` 命令外，你还可以使用旧的 PC 组合键 Ctrl+Alt+Del 重启计算机。如果你想禁用该功能（例如在公共访问电脑上），只需注释掉 `/etc/initittab` 中的以下行即可：

```
ca:ctrlalt:/sbin/shutdown -r -t 4 now
```

### 直接进入内核

通常情况下，一旦内核在你的 Linux 系统上启动，你就不需要对其做太多操作。然而，有一些工具可以检查正在使用的内核并查看有关内核如何启动的信息。此外，如果发生错误或你需要为内核添加额外的支持，也有工具可以完成这些工作。

要确定你的系统运行的是什么内核，请输入：

```
$ uname -r      显示内核版本的名称
2.6.22.5-29-default

$ uname -a      显示所有可用的内核信息
Linux server.domain.com 2.6.22.5-29-default #1 SMP 2007/09/20 15:19:04 UTC i686
1686 1386 GNU/Linux
```

当内核启动时，发生的消息会被放入内核环形缓冲区。你可以使用 `dmesg` 命令显示内核环形缓冲区的内容：

```
$ dmesg |less
Linux version 2.6.22.59-default (geeko@buildhost) (gcc version 4.2.1 (SUSE!) #1 SMP 2007/09/20 15:19:04 UTC
BIOS-provided RAM:
BIOS-E20: 0000000000000000 000000008f00 (usable)
BIOS-E20: 0000000000008f00 00000000a000 (reserved)
BIOS-E20: 0000000000000e00 000000001000 (reserved)
BIOS-E20: 0000000000001000 000007e4e00 (usable)
BIOS-E20: 0000000000007e00 000007ef0500 (ACPI NVS)
BIOS-E20: 0000000000000d70 000007d7700 (usable)
BIOS-E20: 0000000000000d70 000007d7700 (reserved)
BIOS-E20: 00000000000007f0 000007fe2d400 (usable)
```

如果缓冲区填满了，可能不再包含记录的信息。在这种情况下，你可以使用 `/var/log/messages`。你可以翻页这些文件：

```
# cat /var/log/messages* | less /var/log/messages
Aug 5 21:55:46 syslogd[1]: restart.
Aug 6 22:12:03 kernel: eth0: up, 100Mbps, 0x4E1
Aug 6 22:13:06 kernel: eth0: down
Aug 6 22:13:07 kernel: eth0: up, 100Mbps, 0x4E1
Aug 10 05:53:46 kernel: Switching to runlevel: 3
```

在理想情况下，连接到计算机的所有硬件都应该检测并配置相应的 Linux 驱动。某些情况下，检测到了错误的驱动或系统中没有所需的驱动。对于这些情况，Linux 提供了列出加载模块并将其添加到系统的方法。`lsmod` 命令可以查看已加载模块的名称、大小以及哪些其他模块在使用它们。这是一个示例：

| Module | Size | Used by |
|---|---|---|
| parport_pc | 29797 | 1 |
| parport | 38025 | lp,parport_pc |
| snd_ens1371 | 28769 | 1 |
| gameport | 19017 | 1 snd_ens1371 |
| snd_rawmidi | 26561 | 1 snd_ens1371 |
| snd_ac97_codec | 96357 | 1 snd_ens1371 |
| ac97_bus | 6465 | 1 snd_ac97_codec |
| snd_timer | 24773 | 2 snd_seq,snd_pcm |
| soundcore | 11553 | 2 snd |
| e100 | 37193 | 0 |

如果你想了解有关特定模块的信息，可以使用 `modinfo` 命令。这是一个示例：

```
# modinfo snd_ens1371
filename:       /lib/modules/2.6.21-1.3194.fc7/kernel/sound/pci/
snd-ens1371.ko
description:    Ensoniq AudioPCI ESI371+
license:        GPL
```
