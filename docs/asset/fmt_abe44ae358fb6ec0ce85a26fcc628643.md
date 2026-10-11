
你已经完成了。但你应该注意，你实际上并没有对系统进行任何重大的更改，因为你简单地将 GRUB 重新安装到了 MBR（它以前所在的地方）。通常情况下，你现在应该重启系统以确保一切按预期工作。

> 提示：有一个简单的脚本可以帮助你通过单个命令完成上述练习中详细说明的所有步骤，它就是 `grubinstall` 脚本（参见 `man grub-install`）。这种方法并不总是完美的，GRUB 软件的作者承认这是一种不太安全的路线。但尽管如此——它总是运行得很好。

## 第 6 章 启动与关机

### 初始内存磁盘 (initrd)

你可能对 `initrd` 感兴趣。它用于预加载模块或驱动程序。初始随机访问内存（RAM）磁盘是一个特殊设备或 RAM 的抽象。它在内核启动之前由引导加载程序初始化。

`initrd` 解决的一个典型问题是：当一个文件系统来允许访问文件系统以便加载必要的模块。例如，你的启动分区必须格式化为某些奇特的文件系统（例如 B 树文件系统 [Btrs]、ReiserFS 等），内核没有内置的驱动程序，而模块位于磁盘上。这是一个经典的“有鸡还是有蛋”的问题——即，哪个先？因为你没有文件模块，所以你无法访问文件系统；而因为文件模块位于文件系统中，你又无法获取文件系统模块！

GRUB 的解决方案是为内核提供一个基于 RAM 的结构（镜像），其中包含可加载的模块以获取其余模块。该镜像被执行并存在于 RAM 中，因此它不需要立即访问磁盘文件系统。`initrd` 一词有时与 `initramfs` 通替使用，后者使用稍微不同的机制来解决相同的问题。`initramfs` 是两者中较新且更受青的机制，也是你在大多数现代 Linux 发行版中看到的机制。

### GRUB 2

GRUB 2 是 GRUB Legacy 引导加载程序的继任者。一些 Linux 发行版使用并标准化了 GRUB Legacy，许多主流发行版已采用 GRUB 2。Debian 以及基于 Debian 的发行版（如 Ubuntu、Kubuntu 等）使用 GRUB 2，而基于 RPM 的系统仍在使用 GRUB Legacy。可以合理假设，如果出现了更好的东西，所有人最终都会迁移到 GRUB 2 或其他东西。

GRUB 2 的主要特性以及与 GRUB Legacy 的的一些差异列表 6-1 所示。

## 配置 GRUB 2

GRUB 2 中的主配置文件是 `grub.cfg` (`/boot/grub/grub.cfg`) 或 `/boot/grub2/grub.cfg`。该文件通过调用 `grub2-mkconfig` 命令自动生成并更新。`grub2-mkconfig` 命令解析各种脚本（表 6-1）和 `/etc/grub.d/` 目录以创建 `grub.cfg`。`grub.cfg` 中的项目是系统启动菜单中最终显示内容的良好指示。

### GRUB 2 特性描述

配置文件 GRUB 2 的主配置文件命名为 `grub.cfg`。这与 GRUB Legacy 的配置文件 `menu.lst` 不同。`grub.cfg` 并不是为了直接编辑而设计的。其内容是自动生成的。使用多个文件（脚本）来配置 GRUB 菜单，其中一些文件存储在 `/etc/grub/` 目录下，例如：

- `00_header` 为某些通用 GRUB 变量设置默认值，例如图形模式、默认选择、超时时间等。
- `10_linux` 帮助在当前操作系统的根设备查找所有内核，并为找到的所有内核自动创建相关的 GRUB 条目。
- `30_os-prober` 自动探测可能安装在系统上的其他操作系统。特别是在双启动系统中（例如，在 Linux 上运行的 Windows）。
- `40_custom` 用户可以自定义。

## 第 6 章：启动与关机

使用任何你熟悉的文本编辑器（本示例使用了 `vim` 器），在文件中输入以下文本：

```sh
#!/bin/sh -e

echo "Starting new GRUB2 script creation..."

cat << EOF

menuentry "Change Background Color" {

    set color_normal=white/green

}

EOF
```

- 一旦脚本创建成功，请赋予脚本执行权限：
`fedora-server:- # chmod +x 99_custom.sh`

- 运行 `grub2-mkconfig`，它将解析你刚刚创建的新脚本中的命令，并创建一个更新后的 `/boot/grub2/grub2.cfg` 配置文件：
`fedora-server:- # grub2-mkconfig -o /boot/grub2/grub.cfg`

- 使用 `grep` 命令验证新的 `menuentry` 是否已添加到 `grub.cfg`：
`fedora-server:- # grep -A 4 "99_custom.sh" /etc/grub2/grub2/grub.cfg`
```
### BEGIN /etc/grub2/99_custom.sh ###
Starting new GRUB2 script creation...
menuentry "Change Background Color" {
    set color_normal=white/green
}
### END /etc/grub2/99_custom.sh ###
```

- 一旦确认条目已在 `grub.cfg` 文件中，请重启系统。

当系统重启时，你可以在初始 GRUB 界面按照以下步骤测试你的更改：

- GRUB 菜单出现后，选择“Change Background Color”选项并按回。

- 菜单的颜色应变为 `99_custom.sh` 文件中使用 `color_normal` 指令指定的颜色。请注意，选择此项并不会启动系统。你必须选择一个正确的 `menuentry` 来启动 Linux 操作系统。

## Linux 系统管理：学者指南

> 提示：如果你不想在运行 GRUB 2 引导加载程序程序的系统中自动创建特定的菜单条目，你必须删除或禁用 `/etc/grub.d/` 目录中创建该条目的对应脚本。例如，如果你不想在启动菜单中看到如 Microsoft Windows 等其他非原生操作系统的条目，你需要删除 `/etc/grub.d/30_os-prober`，或者将其设置为不可可执行，然后运行 `grub2-mkconfig` 命令来重新生成 `grub.cfg`，使用此命令：
```bash
# chmod -x /etc/grub.d/30_os-prober

# grub2-mkconfig -o /boot/grub2/grub.cfg
```

## USB GRUB 启动盘

让我们来创建一个可启动的 USB GRUB 2 磁盘。这允许你在由于某种原因无法正常启动系统时，使用 USB 设备启动系统。以下是一些可启动 GRUB 2 USB 磁盘大显用场的示例场景：

- 你的系统目前没有引导加载程序。
- 系统的引导加载程序损坏或损坏（可能是由另一个操作系统造成的）。
- 你想创建一个多系统 USB 介质，用于存储和启动 ISO（CD/DVD-ROM）镜像格式的操作系统。

使用 GRUB 启动盘的通用原理是：你目前的系统有一个无法启动、损坏或不需要的引导加载程序——由于系统无法从硬盘自行启动，你需要另一个介质来引导系统（bootstrap）。为此，你可以使用 GRUB 2 USB 盘、GRUB CD，甚至是软盘（祝你好运能找到带软盘的系统！）。

假设我们已准备好加载目标 USB 设备的所有内容，且 USB 驱动器的块设备为 `/dev/sdb`，我们可以执行以下步骤：

1. 将一个大小适中的 USB 驱动器插入系统相应的端口，然后使用 `fdisk`、`lsusb`、`dmesg` 或 `blkid` 命令验证 Linux 与你的 USB 驱动器关联的块设备文件。我们在这里使用 `blkid` 命令：

```bash
[root@server]# blkid

/dev/sdb1 UUID="176-ef7-459-a4e6-304" TYPE="ext4"
```

2. 使用 ext4 文件系统格式驱动（这将擦除驱动上的数据）：
```bash
[root@server]# mkfs.ext4 /dev/sdb1
```

3. 使用 `grub-install` 工具安装引导加载程序：
```bash
[root@server]# grub-install --root-directory=/dev/sdb1
```

4. 如果你不想使用 GRUB，你也可以选择创建配置：
```bash
[root@server]# grub2-mkconfig -o /boot/grub2/grub.cfg
```

5. 查看设备上创建的文件：
```bash
[root@server]# ls /dev/sdb1
```

6. 完成后，你可以挂载设备：
```bash
[root@server]# mount /dev/sdb1
```
