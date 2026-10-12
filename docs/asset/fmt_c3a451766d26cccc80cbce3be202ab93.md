
```bash
[root@localhost]# ls /dev/*; echo "--------------------\ sleep 60; ls /dev/sd*
/dev/sda /dev/sda2 /dev/sdc /dev/sde /dev/sdf1
------------------------------------
/dev/sda /dev/sda2 /dev/sdc /dev/sde /dev/sdf1 /dev/sdg1
/dev/sda /dev/sdb /dev/sdd /dev/dde /dev/sdg
```

如从前面的输出所示，`udev` 守护进程自动为我的 USB 盘创建了 `/dev/sdg` 文件。如果我移除或拔出 USB 盘，`/dev/sdg` 设备文件也会被删除。

你可以通过调整位于 `/etc/udev/rules.d` 目录下的规则文件，来创建这些设备文件的方式。一个典型的 `/etc/udev/rules.d` 目录看起来如下所示：

```bash
[root@localhost]# ls /etc/udev/rules.d
60-fprint-autospend.rules 90-alsa.rules
60-pcmcia.rules 90-hal.rules
60-raw.rules 97-bluetooth-serial.rules
60-vboxadd.rules 98-kexec.rules
70-persistent-cd.rules 99-fuse.rules
70-persistent-net.rules
```

每个文件都有一组规则，`udev` 守护进程按顺序读取这些文件（文件名中的数字的作用就是创建这种顺序）。`99-fuse.rules` 文件可以覆盖 `90-hal.rules` 文件中的另一个规则。

在考试中，了解 `udev` 规则的位置就足够了。在现实中，你并不经常更改规则，但如果你想要自定义 `/dev` 目录中文件的创建方式，了解一些基础知识是有帮助的。

以下是一个为基于 IDE 的 DVD 驱动器创建设备文件的规则示例：

```
SUBSSTEM="block", KERNEL="hdc", SYMLINK="dvd"
```

上述规则意味着“如果内核报告了一个‘hdc’设备，则创建一个‘block’文件（而不是‘character’文件），并为‘hdc’设备添加一个名为‘dvd’的符号链接文件”。

还有其他可能的设置；例如，下一行创建了设备文件，但将文件的所有者设置为 root 用户，并将文件的组设置为 admin 组：

```
SUBSSTEM="block", KERNEL="hdc", SYMLINK="dvd" OWNER="root", GROUP="admin"
```

当设备被添加到系统时，你可以在添加新设备之前执行 `udevadm monitor` 命令，观察 `udev` 如何处理新设备：

```bash
udevadm monitor # udevadm monitor
monitor 将打印接收以下内容的事件：
\UDEV - udev 在处理规则后发送的事件
KERNEL - 内核的 uevent
```

```text
KERNEL[147195929.2758721] add /devices/pci0000:0000:00.06/usb1/1-1 (usb)
1-1/1-1.0 (usb)
KERNEL[147195929.279805] add /devices/pci0000:0000:00.06/usb1/1-1/1-1.0
KERNEL[147195929.285720] add /devices/pci0000:0000:00.06/usb1/1-1/1-1.0/host11 (scsi)
KERNEL[147195929.285757] add /devices/pci0000:0000:00.06/usb1/1-1/1-1.0/host11 (scsi_host)
UDEV[147195929.319982] add /devices/pci0000:0000:00.06/usb1/1-1
```

对于 LPIC-2 考试，你应该意识到在某些较旧的 Linux 发行版中，`udevmonitor` 命令的功能与 `udev monitor` 命令相同。

> 注意：`dmesg` 命令被列为 201.3 节的考试目标（本章涵盖的内容）。`dmesg` 命令在第 16 章中有详细介绍，因此未包含在本章中。

### 考试准备任务

### 复习所有关键主题

复习本章最重要的主题，这些主题在页面外边页用“关键主题”图标标记。表 4-3 列出了这些关键主题的参考以及它们所在的页码。

**表 4-3** 第 4 章关键主题

| 关键元素 | 描述 | 页码 |
| :--- | :--- | :--- |
| 段落 | `/lib/modules` 目录和 `uname` 命令 | 65 |
| 段落 | `depmod` 命令 | 66 |
| 段落 | `lsmod` 命令 | 67 |
| 段落 | `insmod` 命令 | 69 |
| 段落 | `modprobe` 命令 | 70 |
| 段落 | `rmmod` 命令 | 71 |
| 段落 | `modinfo` 命令 | 72 |
| 段落 | `/etc/udev/rules.d` 目录 | 73 |
| 段落 | `udevadm` 命令 | 73 |
| 段落 | `/etc/udev/rules.d` 文件 | 74 |
| 段落 | udev 配置 | 76 |
| 段落 | 列出设备 | 77 |
| 段落 | `udev` 命令 | 81 |
| 段落 | 列出设备 | 82 |
| 段落 | udev 系统 | 85 |

### 定义术语

定义本章中的以下术语并在词表中检查你的答案：

- 通用总线 (`USB`)
- 外围组件接口 (`PCI`)

### 复习题

复习题的答案在附录 A。

1. 哪个命令显示当前加载的模块？
   a. `ls`
   b. `modprobe`
   c. `insmod`
   d. `ismod`

2. 哪些命令可以将模块加载到内存？（多选）
   a. `rmmod`
   b. `ismod`
   c. `modprobe`
   d. `insmod`

3. 哪些命令可以从内存中卸载模块？（多选）
   a. `rmmod`
   b. `ismod`
   c. `modprobe`
   d. `insmod`

4. 哪个目录包含可以修改的内核参数？
   a. `/proc/`
   b. `/kern/`
   c. `/par/`
   d. `/sys/`

5. 填空将 `/proc/sys/dev/cdrom/lock` 文件设置为 0：

6. 哪个命令显示所有内核参数？
   a. `sysctl -a`
   b. `sysctl -l`
   c. `sysctl -k`
   d. `sysctl -p`

7. 要指定模块别名，需要编辑哪个目录下的文件？
   a. `/etc/modules`
   b. `/etc/modules.`
   c. `/etc/modprobe`
   d. `/etc/modprobe`

8. `lspci` 命令的哪个选项可以显示处理设备的内核模块名称？

1. 哪些项通常在运行级别（`runlevel`）5 中被启用？（选择所有适用项。）
   a. 多用户
   b. 网络
   c. `GUI`
   d. 单用户模式

2. 哪个文件决定了 `SysV-init` 系统的默认运行级别？
   a. `/etc/init.d`
   b. `/etc/rc.d`
   c. `/etc/inittab`
   d. 以上都不是

3. 在基于 Debian 的系统中，哪条命令允许你将新脚本添加到启动过程过程？
   a. `update-rc.d`
   b. `telinit`
   c. `init`
   d. `systemd`

4. 你应该将脚本添加到哪个目录中，以便使用 `chkconfig` 命令将其加入启动过程？
   a. `/etc/init`
   b. `/etc/rc.d`
   c. `/etc/init.d`
   d. `/etc/rc`

5. `telinit` 命令的哪个选项允许你在等待特定秒数后切换到另一个运行级别？
   a. `-s`
   b. `-w`
   c. `-t`
   d. `-p`

## 基础主题

### SysV-init 进程

当操作系统启动时，服务或守护进程也会启动。启动哪些服务取决于多个配置设置，这些设置可以由系统管理员进行管理。

目前 Linux 发行版正在使用三种不同的启动技术：`SysV-init`、`Upstart` 和 `Systemd`。这些技术已经流行并被应用于大多数 Linux 发行版，但这些技术目前不在 `LPIC-2` 考试的范围内。因此，本章将专门关注 `SysV-init`。
