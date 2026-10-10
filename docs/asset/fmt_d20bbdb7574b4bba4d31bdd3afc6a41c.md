
- 可以访问许多不同的文件系统（`ext3`、`文件分配表 (FAT)`、`VFAT` 等）。

- 在你安装 Linux 后可以进行动态配置。

- 主配置文件为 `/etc/grub.conf`。

- GRUB 启动菜单为 `/boot/grub/menu.1st.`。

## GRUB 配置文件和命令

GRUB 是一个动态可配置的引导加载程序应用程序，允许在安装后对系统进行更改，以确保成功的启动过程、设备更改或 Linux 内核修改。GRUB 应用程序允许对三个重要的配置文件进行更改。

第一个文件 `/etc/grub.conf` 包含用于查找和加载 GRUB 阶段 2 的磁盘信息，如图 3.1 所示。该文件指示 GRUB 阶段 1 查找用于加载的 GRUB 阶段 2 (`/boot/grub/stage2`)。

第二个文件 `/boot/grub/menu.list` 是一个功能作为 GRUB 菜单的文件。它包含关于启动的分区和操作系统的内容、内核的加载、建立不同的默认内核以及其他启动选项的修改，如图 3.2 所示。本章稍后介绍的“启动问题排除”章节提供了 GRUB 提示符，用于输入可以动态修改 Linux 内核加载和运行级别过程的命令。

`/boot/grub/menu.list` 文件用于修改和/或选择不同内核和其他功能的选项如表 3.1 所示

```bash
linux-01vc:/etc # cat grub.conf
setup --stage2=/boot/grub/stage2 --force-lba (hd0,1) (hd0,0)
quit
linux-01vc:/etc #
```

![](img/53450e0f522134e838a034ce98470308_32_0.png)

```bash
linux-01vc:/boot/grub # cat menu.list
# Modified by YAST2. Last modification on May 11 12:50:48 UTC 2009
default 0
  timeout 0
##Yast
  rootmenu generic_sbr
    qfedmenu (hd0,1)/boot/message
##Yast
```

第一个文件 `/etc/grub.conf` 包含用于查找和加载 GRUB 阶段 2 的磁盘信息，如图 3.1 所示。该文件指示 GRUB 阶段 1 查找用于加载的 GRUB 阶段 2 (`/boot/grub/stage2`)。

第二个文件 `/boot/grub/menu.list` 是一个功能作为 GRUB 菜单的文件。它包含关于启动的分区和操作系统的内容、内核的加载、建立不同的默认内核以及其他启动选项的修改，如图 3.2 所示。本章稍后介绍的“启动问题排除”章节提供了 GRUB 提示符，用于输入可以动态修改 Linux 内核加载和运行级别过程的命令。

`/boot/grub/menu.list` 文件用于修改和/或选择不同内核和其他功能的选项如表 3.1 所示

| 选项 | 描述 |
| :--- | :--- |
| `default` | 指定要启动的默认项。 |
| `timeout` | 指定在加载默认项之前等待的秒数。 |
| `root` | 指定根文件系统的分区。 |
| `kernel` | 指定内核镜像及其参数。 |
| `initrd` | 指定初始内存磁盘。 |

最后一个文件 `/boot/grub/device.map` 是一个唯一文件，其目的是将设备名称映射到 GRUB/BIOS 设备命名规范，如下：

```
(fd0)/dev/fd0
(hd0)/dev/sda
```

GRUB 是一个可执行程序（称为 GRUB Shell），可以通过根提示符访问，并提供以下功能：

- 检查磁盘顺序
- 查看其他引导程序
- 查看硬盘分区详情
- 修改分区设置
- 启动自定义配置文件
- 在启动过程中对系统进行密码保护

使用此命令，你可以在将其应用到系统之前安装或测试 GRUB 配置设置。要实施对 GRUB 配置 `device.map` 的更改，请从 Linux 提示符执行以下命令以重新加载 `device.map` 并执行 `/etc/grub.conf` 中列出的命令。

```bash
grub -batchfile</etc/grub.conf
```

在某些情况下，你可能需要在运行中的系统上将 GRUB 预安装应用程序重新安装到硬盘上。要完成此任务，你可以使用 `grub-install` 命令，如图 3.3 所示。该命令将 GRUB 安装到 MBR 或其他分区，并检查错误。

```
grub-install /dev/sda
```

## 运行级别 (RUNLEVELS)

本节介绍了 `init` 程序的功能和七个运行级别。

### init 命令

`init` 命令负责执行运行级别，是启动过程的最后一步。它将通过进程 ID 1 来标识。它负责启动在 `/etc/inittab` 文件定义的系统进程。

### 运行级别 (Runlevels)

运行级别是特殊的脚本，通过执行 root 管理和用户访问的各种服务或进程来定义计算机系统的启动或停止。通过特权用户运行 `teleinit` 或 `init` 来更改运行级别，这会向 `init` 发送相应的信号。

共有七种不同的运行级别，编号从 0 到 6，尽管运行级别 4 并不经常使用。

![](img/53450e0f522134e838a034ce98470308_35_0.png)

了解运行级别及其每个级别的设计用途非常重要，最重要的描述如下：

- 0 终止所有程序并关闭系统。
- 1 用于单用户模式；也可以使用 s 或 S。
- 2 用于不带网络连接的多用户模式。
- 3 用于带网络连接的多用户模式，并在命令行模式下启动。
- 5 启动带有网络连接的运行级别，并启动图形形图形化用户界面 (GUI)。
- 6 重启系统。

大多数系统将默认运行级别设置为 3 或 5。

为了执行运行级别，`/etc/init.d` 目录中有两类脚本，通过符号链接进行调用。第一组脚本由 `init` 命令执行，在系统启动过程中或每当你启动关闭过程时启动。这些脚本包含在 `/etc/initab` 文件中，如图 3.4 所示。默认运行级别位于 `/etc/initabb`。默认运行级别项在文件中的格式如下：

```
id:5:initdefault:
```

对于图 3.4 所示的文件，运行级别配置为在多用户模式下启动，并提供网络连接和窗口管理器的 X 支持。该文件还指示了搜索要执行特定服务或程序的子目录。对于默认运行级别，`/etc/init.d/rc5d` 是包含默认和服务程序脚本的目录。每个运行级别都包含在运行级别启动和停止时执行的脚本。包含用于停止运行级别的脚本的文件以大写字母 "S" 开头。第二组以 "K" 开头的脚本在运行级别从一个切换到另一个时每次都会执行。调用 `/etc/init.d/rc` 文件是为了确保脚本按正确的顺序执行。

## 启动问题排排除

```
linux-01vc:home/LinuxExpert1 # grub-install /dev/sda

GRUB GRUB 0.97 (640K lower / 3072K upper memory)

[ Minimal BASH-like line editing is supported. For the first word, TAB
lists possible commands. 在其他任何地方按 TAB 会列出设备/文件名的可能补全项。
grub-install --device=/sda=/boot/grub/stage2 --force (hd0,1) (hd0,0)
Checking if "/boot/grub/stage1"... yes
Checking if "/boot/grub/stage2"... yes
Checking if "/boot/grub/stage_5" exists... yes
Running "/boot/grub/stage_5" (hd0,1)\... failed (这不是致命错误)
Running "/boot/grub/stage_5" (hd0,1)\... failed (这不是致命错误)
Running "install -Force la --stage2=/boot/grub/stage2 /boot/grub/stagel (hd0,1) /boot/grub/stage2 p /boot/grub/ub... successful.
Done.
grub> quit
linux-01vc:home/LinuxExpert1 #
```

图 3.3

Grub-install /dev/sda。
