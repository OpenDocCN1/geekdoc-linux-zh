
Linux 启动参数在内核启动之前从外部提供额外信息。在典型的 Linux 系统中，内核通过引导加载程序 `LILO` 或 `GRUB` 启动。因此，Linux 启动参数也可能有不同的名称，例如 `LILO` 参数、`GRUB` 参数或引导程序参数。如果你使用 `LILO` 引导程序，`LILO` 配置文件会在安装期间创建，并在安装后进行修改。该文件包含了计算机上安装的所有操作系统的列表，以及它们应该从中启动的分区。启动参数可以在 `LILO` 启动提示符处手动输入，也可以存储在 `LILO` 配置文件中，如果你使用 `LILO` 引导程序，这两种方式均可。在 `LILO` 启动提示符处，你可以输入系统标签（代表操作系统），然后是操作系统接受的任何参数，如下例所示。

```
LILO: root=/dev/hda1
LILO: windows
```

在上面的示例中，第一行表示系统标签 `linux` 和 `Windows` 分别是操作系统。你可以在配置文件中为这些标签赋予任何名称。当你输入系统标签时，`LILO` 会尝试启动该操作系统。参数 `root=/dev/hda1` 被传递给内核，内核将其解释为启动时应使用 `/dev/hda1` 文件系统作为根文件。

另一方面，`GRUB` 是一种更高级的引导程序，它为用户提供了一个预启动命令行环境（如果用户选择这样启动，将启动过程变得非常灵活）。`GRUB` 配置信息存储在 `/boot/grub/grub.conf` 文件中，并创建一个名为 `/boot/grub/menu.lst` 的链接。该文件中的信息保存在 `MBR`（引导程序所在位置）中，用于在启动时显示操作系统列表。列表 2.2 显示了典型的 `GRUB` 配置文件的样子。在此列表中，Linux 的多个条目表示我们可以根据需要启动不同的 Linux 内核版本。通常，如果通过 `Red Hat Upgrade Agent` 升级内核，这些条目将由 Agent 自动添加。这给了我们启动不同内核版本的选项。每当对此配置文件进行任何更改时，都需要使用类似于此处所示的命令重新安装 `GRUB` 引导程序（此处显示通用命令行的语法），而第二行表示引导程序安装在主硬盘 `/dev/hda` 的 `MBR` 中。

### 列表 2.2

```
[root@etslinux root] grub-install <device>
[root@etslinux root] grub-install /dev/hda
```

```
default=0
timeout=10
splash=(hd0,2)/boot/splash.xpm.gz
title Red Hat Linux (2.4.20-9)
root (hd0,2)
kernel /boot/vmlinuz
```

（注：第43-44页的 OCR 文本在代码块中包含严重损坏/重复。已根据提供的上下文和标准 `GRUB` 语法进行了逻辑清理。）

Linux 启动参数在内核启动之前从外部提供额外信息。在典型的 Linux 系统中，内核通过引导加载程序 `LILO` 或 `GRUB` 启动。因此，Linux 启动参数也可能有不同的名称，例如 `LILO` 参数、`GRUB` 参数或引导程序参数。

# 内核模块

我们已经了解到模块内核使得系统编程更容易为新设备提供驱动或更新当前驱动。事实上，每个高级组件（如文件系统或设备驱动）都可以用模块实现。有命令可以询问模块是否已加载、将模块加载到已运行的内核中、从内核中卸载模块以及检查模块之间的依赖关系。

在 Linux 提示符处执行 `lsmod` 命令可以显示内核中加载的所有模块。

```
[root@linux]#lsmod
```

加粗字母表示命令行窗口中典型的启动提示符。启动提示符可以根据我们的意进行更改，我们将在本章稍后部分讨论这一点。

典型输出所示列表 2.3。

### 列表 2.3

| 模块 | 大小 | 使用情况 |

| :--- | :--- | :--- |

| sd_mod | 13584 | 0 |

# 企业级 Linux 应用开发

| 模块 | 大小 | 已使用 | 被使用模块 |

| :--- | :--- | :--- | :--- |

| sb | 9236 | 1 | (autoclean) |

| sb_lib | 44750 | 0 | (autoclean) [sb] |

| uart401 | 8420 | 0 | (autoclean) [sb_lib] |

| sound | 74388 | 1 | (autoclean) [sb_lib uart401] |

| soundcore | 6532 | 5 | (autoclean) [sb_lib sound] |

| radeon | 93976 | 1 | |

| apgpart | 43072 | 3 | (autoclean) |

| parport_pc | 19108 | 1 | (autoclean) |

| lp | 8996 | 0 | (autoclean) |

| parport | 37152 | 1 | (autoclean) [parport_pc lp] |

| autofs | 13348 | 0 | (autoclean) |

| 3c59x | 30640 | 1 | |

| ipt_REJECT | 3736 | 6 | (autoclean) |

| iptable_filter | 2412 | 1 | (autoclean) |

| ip_tables | 14936 | 2 | [ipt_REJECT] |

| ide-scsi | 10512 | 0 | |

| scsi_mod | 10716 | 2 | [ide-scsi] |

| ide-cd | 33608 | 0 | |

| cdrom | 33696 | 0 | [ide-cd] |

| mousedev | 5524 | 1 | |

| keydev | 22244 | 0 | |

| input | 5888 | 0 | |

| usb-ci | 26188 | 0 | |

| usscore | 7702 | 1 | |

| ext3 | 7036 | 6 | |

| jbd | 52212 | 6 | |

## 面向 Windows程序员的 Linux 35

![](img/1c052d580a194876cd94f43b32c39cf4_50_0.png)

图 2.8 详细列表视图下的 Konqueror 内容。

作为一个浏览器，`Konqueror` 符合 `HTML 4.0` 标准，支持 `ECMA Script/JavaScript`、`Java` applets、级联样式表（`CSS`）以及安全套接层（`SSL`）协议。你可以配置 `Konqueror` 浏览器设置以满足你的需求。通过选择菜单中的 `Settings → Konqueror...` 可以显示配置屏幕。在显示的窗口中，你可以对设置进行选择，例如外观和 `HTML/Java/JavaScript/插件` 相关选项、策略与管理、样式表等。当 `Konqueror` 作为文件管理器使用时，你可以将项目从 `Konqueror` 窗口拖放到另一个 `Konqueror` 窗口、另一个应用程序或桌面上。当作为浏览器使用时，你可以将图像和 `HTML` 链接拖动并丢弃到早先定义的目标对象上。你可以从 `Konqueror` 菜单调用“查找文件”（`Find Files`）对话框，该对话框嵌入在 `Konqueror` 窗口内。图 2.9 显示了 `SuSE Linux 8.1/8.2` 桌面上的 `Konqueror` 窗口，图 2.10 显示了嵌入的“查找文件”对话框。

如前所述，`Konqueror` 可以作为浏览器查看网页。图 2.11 显示了 `Konqueror` 窗口中查看的网页。

## 36 面向企业的 Linux 应用开发

![](img/1c052d580a194876cd94f43b32c39cf4_51_0.png)

图 2.9 SuSE Linux 8.1 桌面上的 Konqueror 窗口。

![](img/1c052d580a194876cd94f43b32c39cf4_51_1.png)

图 2.10 嵌入“查找文件”对话框的 Konqueror 窗口。

## 面向 Windows程序员的 Linux

## 37

![](img/1c052d580a194876cd94f43b32c39cf4_52_0.png)

图 2.11 作为浏览器的 Konqueror。

除了 `Konqueror` 之外，Linux 系统还带有另一个名为 `Mozilla™` 的源浏览器，它源自 `Netscape® Navigator`，并由虚拟组织 `www.mozilla.org` 维护。此外，`Mozilla` 还带有一个排版工具（`composer`），可以 `WYSIWYG`（所见即所得）样式编辑或创建网页。虽然你设计网页的方式类似于在文字处理器中创建文档，但排版器会在后台自动编写 `HTML` 代码。这让你能够轻松地为互联网开发 `HTML` 页面、内网应用程序或为你的应用程序开发 `HTML` 风格的帮助指南。

## Shell 提示符（The Shell Prompt）
