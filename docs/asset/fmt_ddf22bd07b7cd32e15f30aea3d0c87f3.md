
使用 LiveCD 检查虚拟化的一种方法。从该介质启动（并可能在 BIOS 中作了相应更改）后，查看 `/proc/cpu`。如果你在该文件中看到 `vmx` (Intel) 或 `svm` (AMD) 标志，则系统支持虚拟化。有关在 Ubuntu 中创建虚拟机的更多信息，请参阅第 2 章，该章节有专门介绍。当你看到以下提示时，必须在超时前按 `ESC` 键以查看菜单：

```
GRUB Loading stage 1
GRUB loading, please wait...
Press 'ESC' to enter the menu...
```

选项非常直观。第一个选项启动 Ubuntu Server 内核。第二个选项在单用户模式下启动相同的内核。第三个选项旨在运行 `memtest`（它也可以通过 BIOS 菜单可用），进行 RAM 循环以检测错误。如果你安装了新内核，该内核和之前安装的内核通常都在 GRUB 菜单中可用。

### Ubuntu 服务器管理

![img/2cf881509dedde88e348cefb7020_14_0.png 4-3. 典型的 GRUB 菜单](img/2cf881509dedde88e348cefb7020_14_0.png)

图 4-3. 典型的 GRUB 菜单

以下示例中的代码段来自 Ubuntu Server 上的 GRUB 配置文件，不包含注释（你可以自行阅读）。要检查你自己系统中该文件的版本，请打开 `/boot/grub/menu.lst`。第一个活动指令指向第一个代码段作为默认项。换句话说，如果你在 3 秒内未做出选择（如 `timeout` 指令所示），GRUB 将自动选择第一个代码段。

```
default 0
timeout 3
```

注意，如果你设置 `default 1`，则默认选择被设置为第二个代码段。尽管后面的指令被注释掉了，但菜单默认是隐藏的。如果你不想隐藏菜单，请添加 `hidden` 指令。

# 第 4 章：启动过程与救援模式

默认设置 GRUB 菜单为白底黑字。可以更改颜色，如下述指令所示：

```
color cyan/blue white/blue
```

密码选项非常重要；如果你不用密码保护 GRUB 菜单，获得访问的黑客就可以将本地系统设置为任何运行级别（`runlevel`），包括无需密码即可提供管理权限的级别。你可以使用此类指令以明文设置密码：

```
password somepassword
```

> 提示：我强烈建议对 GRUB 菜单进行密码保护。我建议你对 Ubuntu 发行版中配置的“恢复模式”代码段也进行密码保护。

## 作为对比

作为对比，下一个段落如其标题所示，与 Novell 的 SUSE Linux 发行版有关。`boot` 目录是第一块硬盘的第八个分区，正如其标题所示。内核命令行引用了 `/boot/vmlinuz` 中的内核，这证实了 `/boot` 目录并不位于独立的分区上。

```
title SUSE Linux Enterprise Server 10 (/dev/sda8)
root (hd0,7)
kernel /boot/vmlinuz root=/dev/sda8 vga=0x314 splash=silent showopts
initrd /boot/initrd
savedefault
boot
```

SUSE 和 Ubuntu 风格段落之间的差异非常细微：在 SUSE 段落中，顶层目录（`/`）和 `/boot` 目录都在第一块硬盘的同一个分区上。由于它们挂载在分区上，内核和初始 RAM 磁盘文件是从 `/boot/vmlinuz` 和 `/initrd` 文件读取的。`vga=0x314` 是一个帧缓冲区模式，在启动过程中使用。有关帧缓冲区模式的更多信息，请参见 http://.org/HOWTO/Framebuffer-HOWTO.html。正如 `splash=silent` 所示，启动过程中不会出现 SUSE 启动屏幕。`showopts` 选项是间接的；此处列出的选项在启动过程中处于激活。`saveddefault` 选项现在通常被忽略；默认的 `boot` 选项使用段落列出的设置启动启动过程。

要了解更多信息，请查看 Red Hat 如何配置 GRUB 段落。以下命令启动了我安装的 Red Hat Enterprise Linux 5：

```
title Red Hat Enterprise Linux Server (2.6.18-8.1.8.e15)
root (hd0,2)
kernel /vmlinuz-2.6.18-8.1.8.e15 root=LABEL=/ rhgb quiet
initrd /initrd-2.6.18-8.1.8.e15.img
```

`boot` 目录的显示格式与基于 Ubuntu 的段落相同；在这种情况下，它位于第一块硬盘的第三个分区上。由于该分区专门用于 `boot` 目录，内核指令固定了本地目录中指定的内核文件。与 Ubuntu 段落一样，`ro` 意味着顶层目录（`/`）以只读方式挂载，直到系统启动完成。该顶层目录（`/`）与 `LABEL=` 标签关联，功能类似于 Ubuntu 使用 `UUID` 的方式。`rhgb` 选项与 Red Hat 图形启动相关；`quiet` 指令意味着启动过程中隐藏的消息。

最后，检查如何从 GRUB 启动 Windows 系统：

```
title Windows XP Media Center Edition
root (hd0,1)
chainloader +1
boot
```

### Ubuntu 服务器管理

`root (hd0,1)` 指令的工作原理与其他 Ubuntu 根指令类似。在这种情况下，它指向第一块硬盘的第二个分区。`chainloader +1` 指令指向指定分区的起始处偏移一个扇区，这就是微软启动加载程序接管的地方。

> 注意：稍后在“救援与单用户模式”章节中，我将向你如何利用 GRUB 菜单从某些类型的启动故障中恢复以及更多内容。

## 内核与硬件检测

一旦系统从 GRUB 启动到指定的 Linux 内核，内核就会加载到系统中并准备好处理后续操作。该过程记录在*内核环形缓冲区*（`kernel ring buffer`）中，可以通过 `dmesg` 命令或 `/var/log/dmesg` 查看。虽然这是一个大文件，但你至少应该了解通过它可用功能的基本知识，因为它可以帮助诊断启动问题。

内核环形缓冲区的详细信息随 BIOS、连接的硬件、电源管理方案而异。某些特性列在表 4-1 中；但它们可能会以不同的顺序出现——或者在系统上完全不出现，取决于所描述的版本。表 4-1 的信息收集自我的台式机和笔记本系统，以及运行中的 VMware Server。

利用这些知识，你可以使用 `grep` 命令等过滤工具在内核环形缓冲区中搜索问题。例如，如果检测到硬件出现问题，可以在内核环形缓冲区中搜索设备文件、相关的硬件规格甚至硬件地址。

但在你登录 Linux 之前，必须启动服务、配置终端、挂载分区并完成其他任务。这就是一个名为 Upstart 的较新系统的职责范围。

### Upstart、RC 脚本与服务

如果你最近安装了新版本的 Linux，可能会大吃一惊。Ubuntu 发行版中没有 `/etc/init.ab` 配置。Upstart 是 System V init 程序，旨在满足最新的即插即用热插环境的需求。在启动过程中，Upstart 对于挂载在便携和网络设备上的系统特别有用。

> 注意：本节假设你对服务和运行级别（`runlevels`）有一些基础知识；因此，这里的某些解释对于较新的 Linux 管理员来说太简单了。有关运行级别和脚本管理的信息，请参见第 7 章。

作为对 Upstart 成功的证明，Red Hat 从 200 年春季发布的 Fedora 9 开始采用它替代 System V init。

### 表 4-1：典型的内核缓冲区类型

| 关键字 | 描述 |
| --- | --- |
| Kernel | 指定版本和 |
| RAM | 详细的运行级别 |
| Zone | 解码后的消息 |
| ACPI or APM | 高级配置与 |
| Kernel line | 选项 |
| CPU | 默认值 |
| SELinux or AppArmor | 信息 |
| pnp | 启动过程 |
| TCP | 设置 |
| ISA | {计算机架构 |
| SATA | 串口技术 |
| Mounted filesystems | 关于... |

### Upstart 脚本

内核环形缓冲区的详细信息随 BIOS、连接的硬件、电源管理方案而异。某些特性列在表 4-1 中；但它们可能会以不同的顺序出现——或者在系统上完全不出现，取决于所描述的版本。表 4-1 的信息收集自我的台式机和笔记本系统，以及运行中的 VMware Server。

利用这些知识，你可以使用 `grep` 命令等过滤工具在内核环形缓冲区中搜索问题。例如，如果检测到硬件出现问题，可以在内核环形缓冲区中搜索设备文件、相关的硬件规格甚至硬件地址。
