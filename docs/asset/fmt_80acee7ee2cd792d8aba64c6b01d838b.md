
```
# useradd -D
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=-
SHELL=/bin/bash
SKEL=/etc/skel
```

你也可以使用 `-D` 选项来更改默认值。当带有此标志运行时，`useradd` 不会实际创建新用户账户；相反，它会将额外提供的选项作为新默认值保存到 `/etc/login.defs` 中。并不是所有的 `useradd` 选项都可以与 `-D` 选项结合使用。你只能使用表 4-3 中列出的少数选项。

## 表 4-3

更改用户默认值的 `useradd` 选项

| 选项 | 说明 |

|---|---|

| `-b default_home` | 设置创建用户主目录的默认目录。将 `default_home` 替换为要使用的目录名称 (`-b garage`)。通常是 `/home`。 |

| `-e default_expire_date` | 设置用户账户禁用的默认过期日期。`default_expire_date` 值应替换为 `MM/DD/YYYY` 格式的日期 (`+ 10/15/2007`)。 |

| `-f default_inactive` | 设置密码过期后账户被禁用的天数。将 `inactive` 替换为代表天数的数字 (`- f`)。 |

| `-g default_group` | 设置新用户所属的默认组。通常 `useradd` 会创建一个与用户名称和 ID 相同的组。将 `default_group` 替换为要使用的组名 (`- g bears`)。 |

| `-s default_shell` | 为新用户设置默认 `shell`。通常是 `/bin/bash`。将 `default_shell` 替换为想作为新用户默认 `shell` 的 `shell` 完整路径 (`- s /bin/ash`)。 |

要设置任何默认值，请先给出 `D` 选项，然后添加你想要设置的默认值。例如，要将默认主目录位置设置为 `/home/everyone` 并将默认 `shell` 设置为 `/bin/tcsh`，请输入以下内容：

```
# useradd -D -b /home/everyone -s /bin/tcsh
```

除了设置用户默认值外，管理员还可以创建默认文件，并将其复制到每个用户的主目录中备用。这些文件可以登录脚本和 `shell` 配置文件（如 `.bashrc`）。

其他对于处理用户账户非常有用的命令，包括 `usermod`（修改现有账户的设置）和 `userdel`（删除现有用户账户）。

# 配置硬件

在理想的世界里，安装并启动 Linux 后，你所有的硬件都能被快速检测到并供访问。尽管许多 Linux 系统可以做到这一点，但有时你必须采取特殊步骤才能让计算机硬件正常工作。此外，可移动 USB 和 FireWire 设备（光盘、DVD、闪存器、数码相机和移动硬盘）的使用日益增加，这使得 Linux 执行以下操作至关重要：

- 高效管理插拔的硬件。
- 以不同的方式查看同一台硬件（例如，可以将打印机视为传真机、扫描仪和存储设备，同时也视为打印机）。

如果你使用的是包含 2.6 内核的 Linux 系统（大多数 Linux 系统的最新版本），新功能使得硬件设备的检测和管理发生了巨大变化。内核中或与其相关的特性包括 `udev`（根据插拔动态地命名和创建设备）以及 `hotplug` 和 `hal`（将硬件变化信息传递给用户空间）。诸如 `stab-sync` 和 `gnome-volume-manager` 等功能被用于响应硬件变化（例如，挂载设备或启动应用程序来读取设备）。

如果这一切听起来有点困惑，不要担心。它们的设计实际上是为了让你作为 Linux 用户的生活更轻松。基于 2.6 内核构建的功能最终结果是 Linux 中的设备处理变得：

- 更加自动——对于大多数常见硬件，当硬件设备连接或断开时，会添加访问硬件的接口，以便 Linux 可以访问。硬件的存在这一事实。
- 更加灵活——对于大多数常见硬件，当硬件设备连接或断开时，会添加访问硬件的接口，以便 Linux 可以访问。硬件的存在这一事实。
- **数码相机**——连接数码相机后，相机的内容将显示在 Konqueror 窗口中。你可以在该目录中复制、移动或执行其他操作。

# 使用可加载模块

如果你的电脑上有未被正确检测到的硬件，你可能需要为该硬件手动加载模块。Linux 提供了一组命令，用于加载、卸载和获取硬件模块信息。

如果你安装了 Linux 内核源码，可用驱动程序的源码文件存储在 `/usr/src/linux*/drivers/` 目录的子目录下。你可以通过两种方式找到这些驱动程序的信息：

- `make xconfig`——以 `/usr/src/linux*` 为当前目录，在终端或桌面输入 `make xconfig`。选择你需要的模块类别，然后点击“帮助”（Help）获取你感兴趣的驱动程序。出现的帮助信息包含了驱动程序的描述。
- `Documentation`——`/usr/src/linux*/Documentation` 目录包含许多描述内核方面和相关细节的纯文本文件。

模块编译完成后，它们会被安装在 `/lib/modules/` 子目录下。目录的名称基于内核的当前发布号。此目录中的模块可以根据需要加载和卸载。

# 列出已加载的模块

要查看当前加载到电脑运行内核中的模块，请使用 `lsmod` 命令。例如下：

> 注意
>
> 如果你没有安装 Linux 系统，请尝试启动 KNOPPIX 并使用 `lsmod` 列出你的模块。如果所有硬件均工作正常，请查看此模块列表。当你永久安装 Fedora 或其他 Linux 系统时，如果 CD 驱动器、调制解调器、显卡或其他硬件无法正常工作，可以使用模块列表来确定应该使用并加载哪个模块，如下一节所述。

```
# lsmod
Module Size Used by
snd_seq_oss 38912 0
snd_seq_midi_event 9344 1 snd_seq_oss
snd_seq 67728 4
snd_seq_oss,snd_seq_midi_event
snd_seq_device 8328 2 snd_seq_oss,snd_seq

autofs 16512 0
e2k_pci 9056 0
8390 13568 1 ne2k_pci
ohci1394 41860 0
ieee1394 284464 1 ohci1394

floppy 65712 0

sg 36120 0

scsi_mod 124600 1 sg

parport_pc 39724 0

parport 47336 1 parport_pc

exttext3 128424 2

jbd 866040 1 ext3
```

此输出显示了 Linux 系统上加载的各种模块，包括几个用于支持 ALSA 音频系统的模块，其中一些提供了 OSS 兼容性（`snd_seq_oss`）。

要查找任何已加载模块的信息，请使用 `modinfo` 命令。例如，你可以输入：

```
# modinfo -d snd-seq-oss

"OSS-compatible sequencer module"
```

并不是所有模块都有描述。但在这种情况下，`snd-seq_oss` 模块被描述为 OS 兼容的序器模块。你还可以使用 `-a` 选项查看模块作者，或使用 `-n` 查看对象文件的表示。作者信息包含驱动程序创建者的电子邮件地址，因此如果你对它有任何问题或疑问，可以联系作者。

# 加载模块

你可以使用 `modprobe` 命令将任何编译并安装（到 `/lib/modules` 目录）的模块加载到运行的内核中。加载模块的一个原因是为了临时使用它（例如，加载一个模块以支持你想访问的软盘上的特殊文件系统）。另一个原因是识别无法自动检测的特定硬件所使用的模块。

以下是使用 `modprobe` 命令加载 `parport` 模块的示例，它提供了与多个设备共享并行端口的核心功能：

```
# modprobe parport
```

在加载 `parport` 后，你可以加载 `parport_pc` 模块来定义通过接口提供的 PC 风格端口。`parport_pc` 模块允许你可选地定义与共享并行端口的设备相关的地址和 IRQ。例如：

在此示例中，一个设备被识别为地址 `0x3bc`，且该设备的 IRQ 是自动检测的。

`modprobe` 命令临时加载模块——它们在下次重启时会消失。要将模块永久添加到你的系统中，请将 `modprobe` 命令添加到启动时运行的启动脚本之一。

`modprobe` 的替代方案是 `insmod` 命令。然而，使用 `modprobe` 的优点是 `insmod` 只加载你请求的模块，而 `modprobe` 会尝试加载你请求的模块所依赖的其他模块。

# 移除模块

使用 `rmmod` 命令从运行的内核中移除模块。例如，从当前内核移除 `parport_pc` 模块，请输入：

```
rmmod parport_pc
```
