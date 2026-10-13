
|---|---|

| `insert` | `eject` | `notify` | 触发事件的媒体操作。 |

| `regex` | 此 Bourne shell 正则表达式与受此事件影响的 `/vol` 文件系统中的每个条目进行匹配。 |

| `[options]` | 指定此事件要运行的用户或组名（可选）。 |

| `<program>` | 如果 `regex` 匹配，则要运行的可执行程序的完整路径名。 |

| `program_args` | 程序的参数。 |

在默认的 `vold.conf` 文件中，您会在“要使用的设备”和“操作”部分下看到以下条目：

```
# Devices to use
use cdrom drive /dev/rdsk/c*s2 dev_cdrom.so cdrom%d
use floppy drive /dev/rdiskette[0-9] dev_floppy.so floppy%d
use pcmem drive /dev/rdsk/c*s2 dev_pcmem.so pcmem%d forceload=true
use rmdisk drive /dev/rdsk/c*s2 dev_rmdisk.so rmdisk%d
# Actions
eject dev/diskette[0-9]/* user=root /usr/sbin/rmmount
eject dev/dsk/* user=root /usr/sbin/rmmount
insert dev/diskette[0-9]/* user=root /usr/sbin/rmmount
insert dev/dsk/* user=root /usr/sbin/rmmount
notify rdsk/* group=tty user=root /usr/lib/vold/volmissing -p
remount dev/diskette[0-9]/* user=root /usr/sbin/rmmount
remount dev/dsk/* user=root /usr/sbin/rmmount
```

当 CD 插入到名为 `/dev/dsk/c0t6d0` 的 CD-ROM 时，会发生以下情况：

- 1. `vold` 检测到 CD 已插入，并运行 `/usr/sbin/rmmount` 命令。`rmmount` 是自动在 CD-ROM 和软盘上挂载文件系统的实用程序。它确定介质上是否存在的文件系统类型（如果有）。如果存在文件系统，`rmmount` 会挂载文件系统（对于 CD-ROM，在 `/cdrom0` 中）。
如果介质是只读的（CD-ROM 或写保护标签已设置的软盘），则文件系统以只读方式挂载。如果未识别出文件系统，`rmmount` 不会挂载文件系统。

- 2. 挂载完成后，将执行与媒体类型关联的操作。该操作允许其他程序被通知有新的介质可用。例如，挂载 CD-ROM 或软盘的默认操作是启动文件管理器。
这些操作在配置文件 `/etc/rmmount.conf` 中有描述。以下是默认 `/etc/rmmount.conf` 文件的示例：

```
# @(#)rmmount.conf 1.10      00/02/14 SMI
#
# Removable Media Mounter configuration file.
#
# File system identification
ident udfs ident_udfs.so cdrom floppy rmdisk
ident hsfs ident_hsfs.so cdrom
ident ufs ident_ufs.so cdrom floppy rmdisk pcmem
ident pcfs ident_pcfs.so floppy rmdisk pcmem
# Actions
action cdrom action_filemgr.so
action floppy action_filemgr.so
action rmdisk action_filemgr.so
# Mount
mount * hsfs udfs ufs -o nosuid
```

- 3. 如果用户发出 `eject` 命令，`vold` 会看到媒体事件，并执行与该事件关联的操作。在这种情况下，它运行 `/usr/sbin/rmmount`。`rmmount` 卸载已挂载的文件系统，并执行 `/etc/rmmount.conf` 文件中指出的与媒体类型关联的操作。如果文件系统“忙”（即它包含活动进程的当前工作目录），则 `eject` 操作失败。

系统管理员可以修改 `vold.conf` 以指定在发生媒体事件（如 `eject` 或 `insert`）时应调用哪个程序。如果修改了 `vold.conf` 配置文件，必须通知 `vold` 重新读取 `/etc/vold.conf` 文件。按如下方式停止并启动 `vold` 即可完成此操作。输入以下内容：

```
/etc/init.d/volmgt stop
```

然后输入以下内容：

```
/etc/init.d/volmgt start
```

还有一些其他命令可以帮助您在系统上管理卷管理器。它们在表 7.11 中有描述。

## 表 7.11

### 卷管理器命令

| 命令 | 描述 |

|---|---|

| `rmmount` | 可移动媒体挂载器。`vold` 在安装 CD 或软盘时用于自动挂载 `/cdrom` 和 `/floppy`。 |

| `volcancel` | 取消用户访问特定 CD-ROM 或软盘文件系统的请求。此命令由系统管理员发出，如果包含文件系统的可移动介质当前不在驱动器中，则很有用。 |

| `volcheck` | 系统管理员发出此命令以检查驱动器中是否安装了介质。默认情况下，它检查由 `/dev/diskette` 指向的驱动器。 |

| `volmissing` | 此操作在 `vold.conf` 中指定，如果尝试访问已不在驱动器中的 CD 或软盘，则会通知用户。 |

| `vold` | 卷管理器守护进程，由 `/etc/vold.conf` 控制。 |

对某些人来说，卷管理可能弊大于利。要禁用卷管理，请删除（或重命名）名为 `/etc/rc2.d/S92volmgt` 的文件。然后发出命令 `/etc/init.d/volmgt stop`。如果您希望 CD 上有卷管理但软盘上没有，请在 `vold.conf` 文件的“要使用的设备”和“操作”部分中用 `#` 注释掉条目，如下所示：

```
# Devices to use
use cdrom drive /dev/rdsk/c*s2 dev_cdrom.so cdrom%d
#use floppy drive /dev/rdiskette[0-9] dev_floppy.so floppy%d
use pcmmem drive /dev/rdsk/c*s2 dev_pcmmem.so pcmmem%d forceload=true
# use rmscsi drive /dev/rdsk/c*s2 dev_rmscsi.so rmscsi%d

# Actions
#insert dev/diskette[0-9]/* user=root /usr/sbin/rmmount
insert dev/dsk/* user=root /usr/sbin/rmmount
#eject dev/diskette[0-9]/* user=root /usr/sbin/rmmount
eject dev/dsk/* user=root /usr/sbin/rmmount
notify rdsk/* group=tty user=root /usr/lib/vold/volmissing -p
```

对 `/etc/vold.conf` 所做的更改后，`vold` 守护进程启动时，仅管理 CD-ROM，而不管理软盘。

`vold` 很挑剔。了解这一点是防止 `vold` 因某种原因崩溃或无法工作的关键。与其他计算机，例如 PC 相比，可以毫无问题地弹出 CD-ROM。在 Solaris 中，`vold` 并非那么健壮，因此系统管理员在使用卷管理器时需要遵循一些基本规则：

- 始终对与 CD-ROM 和软盘相关的所有操作使用 `vold` 命令。使用表 5.11 中列出的命令来完成任务。
- 在按下机箱外部的按钮弹出 CD-ROM 磁盘之前，请务必键入 `eject cdrom`。这是为了确保读取器中没有已有的 CD。
- 切勿在机器中已有 CD 时按下按钮弹出 CD。这可能会导致 `vold` 停止工作。同样，请改用 `eject cdrom` 命令。
- 如果无法使用 `/etc/init.d/volmgt` 脚本停止或启动 `vold`，则需要重新启动系统以使 `vold` 正常工作。

## 逐步操作

### 7.1 使用可移动媒体管理器 GUI

我发现使用软盘最可靠的方法是通过 CDE（Common Desktop Environment）中的可移动媒体管理器 GUI。使用软盘时，如果通过媒体管理器 GUI 而不是命令行操作，问题似乎会减少。要使用可移动媒体管理器，请按照以下步骤操作：

1. 从位于屏幕底部 CDE 前控制面板打开文件管理器 GUI，如图 7.1 所示。

![](img/df66a0e1cd473c73297ad9cbd0cb0cb8_300_0.png)
