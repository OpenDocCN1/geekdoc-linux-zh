
| `/vol/dev/aliases/cdrom0` | 为主 CD-ROM 驱动器介质提供字符设备访问的目录 |

| `/vol/dev/dsk/` | 提供 CD-ROM 缓冲或块设备访问的目录 |

| `/vol/dev/rds/` | 提供 CD-ROM 字符或原始设备访问的目录 |

| `/cdrom/cdrom0` | CD-ROM 驱动器 0介质缓冲设备的符号链接 |

| `/floppy/floppy0` | 软盘驱动器 0介质缓冲设备的符号链接 |

进程在插入包含可识别文件系统的可移动介质时，会自动挂载 CD-ROM 和文件系统。当插入 CD 时，`vold` 会自动将 CD-ROM 文件系统挂载到 `/vol/dev` 目录。然而，对于软盘，在您执行 `vold` 命令之前不会自动挂载。`vold` 命令指示 `vold` 检查每个设备以确定是否插入了新介质。由于软盘驱动器的硬件限制，对于软盘不要像 CD 那样持续轮询。对软盘进行持续轮询会导致机械动作并导致驱动器过早损坏。

进程在卷管理器之后。它由 `/etc/init.d/volmgt` 脚本自动启动。`vold` 在启动时读取 `/etc/vold.conf` 配置文件。`vold.conf` 包含了 `vold` 使用的卷管理器信息。

### 表 7.9

### 卷管理器

| 参数字段 | 描述 |

| :--- | --- |

| device | 可移动设备的类型。合法值为 `cdrom` 和 `floppy`。 |

| type | 设备的能力。 |

| special | 指定设备。通常以 `/dev` 开头。 |

| shared_object | 程序的名称。`/usr/lib/void`。 |

| sym | 指向设备的符号。 |

| options | 用户、组和模式权限。 | 第 7 章 SOLARIS 文件系统：高级主题 259

### 表 7.10

### VOLD.CONF 操作

| 参数 | 描述 |

| :--- | --- |

| insert|eject|notify | 触发事件的介质动作。 |

| regex | 此 Bourne shell 正表达式将匹配 `/vol` 文件系统中受此事件影响的每个条目。 |

| [options] | 指定运行的用户或组名事件（可选）。 |

| `<program>` | 匹配正则时运行的可执行程序的完整路径。 |

| program_args | 程序的参数。 |

挂载完成后，将执行与媒体类型相关的操作。该操作允许其他程序知道有新介质可用。例如，挂载 CD-ROM 或软盘的默认操作是启动文件管理器。

这些操作在配置文件 `/etc/rmmount.conf` 中进行了描述。以下是默认的 `/etc/rmmount.conf` 文件的示例：

```
# @(#)rmmount.conf 1.10     00/02/14 SMI
#
# 可移动介质挂载器配置文件。
```

```
# File system identification
ident udfs ident_udfs.so cdrom floppy rdisk
ident hfs ident_hfs.so cdrom
ident ufs ident_ufs.so cdrom floppy rdisk pcmem
ident pcsfs ident_pcsfs.so floppy rdisk pcmem
```

```
# Actions
action cdrom action_filemgr.so
action floppy action_filemgr.so
action rdisk action_filemgr.so
```

```
# Mount
mount * hfs udfs ufs -nosuid
```

3. 如果用户执行 `eject` 命令，`vold` 会看到介质事件并执行与该事件相关的操作。在这种情况下，它会运行 `/usr/sbin/rmmount unmount mounted systems`，并执行 `/etc/rmmount.conf` 中调用的与媒体类型相关的操作。如果文件系统处于“忙”状态（即包含活动进程的工作目录），则 `eject` 操作将失败。

系统管理员可以修改 `vold.conf` 以指定当发生介质事件（如弹出或插入）时应调用哪个程序。如果修改了 `vold.conf` 配置文件，必须重新让 `vold` 读取 `/etc/vold.conf`。可以通过以下方式停止并重新启动 `vold` 来实现。输入以下命令：

```
/etc/init.d/volmg stop
```

然后输入：

```
/etc/init.d/volmg start
```

其他几个命令也可以帮助你管理系统上的卷管理器。它们描述在表 7.11 中。

## 表 7.11 卷管理器命令

| 命令 | 描述 |

|---|---|

| `rmount` | 可移动介质挂载器。由 `void` 用于在安装了 CD 或软盘时自动挂载 `/cdrom` 和 `/floppy`。 |

| `volcancel` | 取消用户访问特定 CD-ROM 或软盘文件系统的请求。此命令由系统管理员发出，如果包含文件的可移动介质当前不在驱动器中，则它非常有用。 |

| `volcheck` | 系统管理员执行此命令来检查驱动器是否安装了介质。默认情况下，它检查由 `/dev/disksk` 指向的驱动器。 |

| `volmissing` | 此操作在 `void.conf` 中指定；当尝试访问已不在驱动器中的 CD 或软盘时，会通知用户。 |

| `void` | 卷管理器守护进程，由 `/etc/void.conf` 控制。 |

某些情况下，卷管理看起来比它带来的价值更麻烦。要禁用卷管理，请删除（或重命名）文件 `/etc/rc2/s92volmgmt`。然后插入 `/etc/init.volmgmt stop`。如果你想在 CD 上开启卷管理但在软盘上关闭，可以使用 `#` 注释掉 `void.conf` 文件中 "Devices to Use" 和 "Actions" 部分的条目：

- # Devices to use

- #use cdrom drive /dev/dsk/* s2 dev_cdrom.so cdrom%

- #use floppy drive /dev/diskette[0-9] dev_floppy floppy%

- #use pcmem drive /dev/dsk/* s2 dev_pcmem.so pcmem%d forload=true

- #use rmscsi drive /dev/dsk/* s2 dev_rmscsi.so rmscsi%d

- # Actions

- #insert dev/diskette[0-9]* user=root /usr/sbin/rmmount

- #insert dev/dsk/* user=root /usr/sbin/rmmount

- #eject dev/diskette[0-9]* user=root /usr/sbin/rmmount

- eject dev/dsk/* user=root /usr/sbin/rmmount

- notify rdsk/* group=tty user=root /usr/lib/void/volmissing -p

随着对 `/etc/vold.conf` 做出更改，当 `void` 守护进程启动时，它将只管理 CD-ROM 而不管理软盘。

`vold` 是很挑剔的。了解这一点是防止 `void` 崩溃或由于某些原因无法运行关键。在 PC 等电脑上，你可以顺利地弹出 CD-ROM。在 Solaris 上，`void` 并不健壮，因此系统管理员在使用卷管理器时需要遵循几条基本规则：

- 对于所有涉及 CD-ROM 和软盘的操作，始终使用 `void` 命令。使用表 5.11 中列出的命令来完成你的任务。

- 在按下盒子外的按钮弹出 CD-ROM 磁盘之前，务必输入 `eject eject`。这是为了确保读取器中已经没有 CD 了。

- 当机器内已有 CD 时，千万不要按下弹出 CD 的按钮。这将导致 `void` 停止工作。再次，请使用 `eject eject` 命令。

- 如果你无法通过 `/etc/init.d/volmgr` 脚本停止或启动 `void`，你需要重启系统让 `void` 恢复工作。

### 逐步详解

### 7.1 使用可移动介质 GUI

我发现使用软盘最可靠的方法是通过 CDE（公共桌面环境）中的可移动介质 GUI。如果通过介质管理器而不是命令行使用软盘，问题似乎会降到最低。按照以下步骤操作：

- 打开位于屏幕底部的 CDE 面板的文件管理器 GUI，如图 7.1 所示。（img/792518004e741c5a034392e81_298_0.png）文件管理器将会出现。

- 2. 点击菜单栏中的“文件”（File）菜单，如图 7.2 所示。（img/792518004e741c5a034392e81_298_1.png）图 7.2 文件管理器。将下拉菜单。
