
## 一般选项

首先，有一般选项：

- `color` `white/blue black/light-gray`。启动管理器菜单的颜色。
- `default` `0`。第一个条目（编号从 0 开始）是默认启动条目，如果在键盘上没有选择其他条目，则会自动启动该条目。
- `timeout` `8`。默认启动条目在 8 秒后自动启动。
- `gfxmenu` `(hd0,0)/boot/message`。此定义图形菜单的存储位置。

## 操作系统相关选项

一般选项之后，是可用于 GRUB 启动的各种操作系统的相关选项。

- `title` `title`。每个操作系统的条目都以 `title` 开头。
- `root` `(hd0,0)`。随后的条目相对于采用 GRUB 语法给出的此硬盘分区（在此示例中为第一个硬盘上的第一个分区）。使用此条目后，在后续的如 `kernel` 等条目中，无需指定分区。

关于硬盘和分区的指定，请注意以下几点：

GRUB 不区分 IDE 和 SCSI 硬盘。被 BIOS 识别为第一块硬盘的硬盘被指定为 `hd0`，第二块硬盘为 `hd1`，依此类推。

第一块硬盘上的第一个分区称为 `hd0,0`，第二个分区为 `hd0,1`，依此类推。

- `kernel` `/boot/vmlinuz`。此条目描述了内核的位置，相对于上面指定的分区。其后跟随内核参数，如 `root=/dev/hda1`、`vga=normal` 等。
- `initrd` `/boot/initrd`。此条目设置初始 RAM 磁盘（在 SLES 10 中为 `initramfs`）的位置，相对于上面指定的 `root (hd0,0)`。`initrd` 包含在内核访问硬盘之前所需的硬件驱动程序（例如 IDE 或 SCSI 控制器的驱动程序）。

以下是配置文件 `/boot/grub/menu.lst` 的一个示例：

```
# Modified by YaST2. Last modification on Mon May 15 08:38:29 UTC 2006

# color white/blue black/light-gray
# default 0
# timeout 8
gfxmenu (hd0,1)/boot/message

###Don't change this comment - YaST2 identifier: Original name: linux###
title SUSE Linux Enterprise Server 10
root (hd0,1)
kernel /boot/vmlinuz root=/dev/sda2 vga=0x317 resume=/dev/sda1
	splash=silent showopts
initrd /boot/initrd

###Don't change this comment - YaST2 identifier: Original name: floppy###
title Floppy
chainloader (fd0)+1

###Don't change this comment - YaST2 identifier: Original name: failSafe###
title FailSafe -- SUSE Linux Enterprise Server 10
root (hd0,1)
kernel /boot/vmlinuz root=/dev/sda2 vga=normal showopts ide=nodma
	apm=off acpi=off noresume noemp noapic maxcpus=0 edd=off 3
initrd /boot/initrd
```

## 使用 YaST 配置 GRUB

虽然您可以使用 YaST（引导加载程序配置模块）来简化引导加载程序的配置，但除非您理解其背后的概念，否则不应尝试使用该模块。

若要启动 YaST 引导加载程序模块，请启动 YaST，输入 root 密码，然后选择 **System > Boot Loader**（系统 > 引导加载程序），或者在终端窗口中通过 root 用户输入 `yast2 bootloader` 直接启动引导加载程序模块。

将显示以下内容：

![](img/63e88022bf135307e3eac051ad238b5b_235_0.png)

![](img/63e88022bf135307e3eac051ad238b5b_235_1.png)

当选择 **Section Management**（部分管理）选项卡时，您将看到系统的当前 GRUB 设置。有一个 **Def**（默认）列，指示在启动系统时哪个条目被选为默认。

当您选择 Add（添加）时，您会获得四个选择：

![](img/63e88022bf135307e3eac051ad238b5b_236_0.png)

四个 **Section Types**（部分类型）都在左侧的帮助文本中进行了说明。

当您选择 **Clone Selected Section**（克隆选定的部分）并单击 **Next**（下一步）时，对话框中会填充所选部分中的值。对于接下来的两个选项，对话框相同，但行为空：

### 图 5-4

![](img/63e88022bf135307e3eac051ad238b5b_237_0.png)

最后一个选项 Other System (Chainloader)（其他系统（链式加载器））的对话框提供了一个用于部分名称的字段，以及一个用于加载另一个引导加载程序的设备。

当您在引导加载程序设置对话框（图 5-2）中选择 **Edit**（编辑）时，会打开相同的对话框，您可以在其中更改现有设置。

若要删除条目，请选中该条目，然后单击 **Delete**（删除）。

### 图 5-5

当您选择 **Boot Loader Installation**（引导加载程序安装）选项卡时，您将看到以下对话框：

![](img/63e88022bf135307e3eac051ad238b5b_238_0.png)

- **Boot Loader Type**（引导加载程序类型）。您可以使用此选项在 GRUB 和 LILO 之间切换。一个对话框允许您指定执行此更改的方式。
- **Boot Loader Location**（引导加载程序位置）。您可以使用此选项定义是将引导加载程序安装在 MBR 中，还是在引导扇区中（如果可用），或者在软盘上。使用 Others（其他）来指定不同的位置。
- **Boot Loader Installation Details**（引导加载程序安装详情）。此选项提供了专门的配置选项，如激活特定分区或更改磁盘顺序以对应 BIOS 中的序列。
- **Other**（其他）。当您选择此项时，会打开一个包含以下额外选择的下拉菜单：
  - **Edit Configuration Files**（编辑配置文件）。显示并编辑配置文件（`/boot/grub/device.map`、`/boot/grub/menu.lst` 或 `/etc/grub.conf`）。
    - 注意：SLES 10 上的 `/etc/grub.conf` 包含安装引导加载程序所需的信息（`grub --batch < /etc/grub.conf`），而 RHEL 上的相同文件内容与 `/boot/grub/menu.lst` 相同。
  - **Propose New Configuration**（建议新配置）。此选项会生成一个新的配置建议。在其他分区上找到的旧版 Linux 版本或其他操作系统将包含在启动菜单中，使您可以启动 Linux 或其旧引导加载程序。后者会带您进入第二个启动菜单。
  - **Start from Scratch**（从头开始）。此选项允许您从头开始创建整个配置。不会生成任何建议。
  - **Reread Configuration from Disk**（从磁盘重新读取配置）。如果您已经进行了一些更改并对结果不满意，可以使用此选项重新加载当前配置。
  - **Propose and Merge with Existing GRUB Menus**（建议并与现有 GRUB 菜单合并）。如果其他分区中安装了其他操作系统和旧版 Linux，则菜单将从新 SUSE Linux 的条目、其他系统的条目以及旧引导加载程序菜单的所有条目生成。此过程可能需要一些时间，并且仅适用于 GRUB。
  - **Restore MBR from Hard Disk**（从硬盘恢复 MBR）。将恢复保存在硬盘上的 MBR。

配置引导加载程序完成后，通过选择 **Finish**（完成）保存配置更改。

## 直接引导系统进入 Shell

GRUB 引导加载程序的启动屏幕允许您传递修改 Linux 内核的参数，以便在内核实际加载之前进行修改。

GRUB 启动屏幕底部有一个 Boot Options（启动选项）字段。若要添加启动选项，请选择一个操作系统，并在 Boot Options 字段中输入额外的启动选项。
