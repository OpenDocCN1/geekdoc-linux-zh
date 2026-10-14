
`initrd /boot/initrd`。此项设置了初始内存磁盘（SLES 10 中为 `initramfs`）的位置，相对于上述指定的 `root (hd0,0)`。`initrd` 包含了内核在访问硬盘之前需要的硬件驱动程序（例如 IDE 或 SCSI 控制器的驱动程序）。

# 以下是配置文件的示例

`/boot/grub/menu.lst`:
```
# Modified by YaST2. Last modification on Mon May 15 08:38:29 UTC 2006

color white/blue black/light-gray
default 0
timeout 8
gfxmenu (hd0,1)/boot/message

###Don't change this comment - YaST2 identifier: Original name: linux###
title Suisse Linux Enterprise Server 10
root (hd0,1)
kernel /boot/vmlinuz root=/dev/sda2 vga=0x0317      resume=/dev/sda
plash=silent showopts
initrd /boot/initrd

###Don't change this comment - YaST2 identifier: Original name: floppy###
title Floppy
chainloader (fd0)+1

###Don't change this comment - YaST2 identifier: Original name:
failsafe###
title SafeS -- SUSE Linux Enterprise Server 10
root (hd0,1)
kernel /boot/vmlinuz root=/dev/sda2 vga=normal showopts ide=nodma
apm=off acpi=off noresume nosmp noaptic maxcpus=0 edoff=3
initrd /boot/initrd
```

# 使用 YaST 配置 GRUB

虽然你可以使用 YaST（引导加载程序配置模块）来简化引导加载程序的配置，但在你理解其背后的概念之前，应该谨慎尝试使用该模块。

要启动 YaST 引导加载程序模块，请启动 YaST，输入 root 密码，然后选择 `System > Boot Loader`，或者直接在终端窗口中以 root 身份输入 `yast2 bootloader`。直接启动引导加载程序模块。

# CNI 专用 - 仅允许纸质打印

# 下图所示：

图 7-2

![](img/84d12236ddfe17cc29fd21173b9904ac_325_0.png)

当选择章节管理（Section Management）选项卡时，你可以看到系统当前的 GRUB 设置。有一个“Def”（默认）列，指示在启动系统时哪一个条目被选为默认项。

# CNI 专用 - 仅允许纸质打印

严禁复制本手册的全部或部分内容或分发此类副本。如怀疑有抄袭，请拨打 1-800-PIRATES。

当你选择“添加”（Add）时，会提供四种选择：

# 图 7-3

![](img/84d12236ddfe17cc29fd21173b9904ac_326_0.png)

左侧的帮助文本解释了四个章节中的每一个。

# SUSE Linux Enterprise Server 10 管理

当你选择“复制选中章节”（Clone Selected Section）并点击“下一步”（Next）时，对话框将填充所选章节的值。通过以下两个选项，对话框的内容相同，但行将是空的：

# 图 7-4

![](img/84d12236ddfe17cc29fd21173b9904ac_327_0.png)

最后一个选项“其他系统（链式加载器）”的对话框提供了一个用于章节名称的行以及一个从此处加载另一个引导加载程序的设备。

在引导加载程序设置对话框中（图 7-2）选择“编辑”（Edit），对话框将打开，你可以在其中更改现有设置。

要删除条目，请选中它然后点击“删除”（Delete）。

CNI 专用 - 仅允许纸质打印

严禁复制本手册的全部或部分内容或分发此类副本。如怀疑有抄袭，请拨打 1-800-PIRATES。

7-16

版本 1

当你选择“引导加载程序安装”（Boot Loader Installation）选项卡时，你会看到以下对话框：

# 图 7-5

![](img/84d12236ddfe17cc29fd21173b9904ac_328_0.png)

- **引导加载程序类型（Boot Loader Type）**。你可以使用此选项在 GRUB 和 LILO 之间切换。对话框允许你指定执行操作的方式。
- **引导加载程序位置（Boot Loader Location）**。你可以使用此选项定义是将引导加载程序安装在 MBR、引导分区的扇区（如果可用）还是软磁盘上。使用“其他”（Others）来指定不同的位置。
- **引导加载程序安装细节（Boot Loader Installation Details）**。这提供了专门的配置选项，例如激活特定分区或更改磁盘顺序以对应 BIOS 中的序列。
- **其他（Other）**。当你选择此项时，会打开包含以下附加选项的下拉菜单：
  - **编辑配置文件（Edit Configuration Files）**。显示并编辑配置文件（`/boot/grub/device.map`、`/boot/grub/menu.lst` 或 `/boot/grub.conf`）。
  - **建议新配置（Propose New Configuration）**。此选项会生成一个新的配置建议。旧版本的 Linux 或在其他分区上找到的操作系统将包含在引导菜单中，使你能够启动你的 Linux 或其引导加载程序。后者将带你进入第二个引导菜单。
  - **从头开始（Start from Scratch）**。此选项允许你从头开始创建整个配置。不会生成任何建议。
  - **从磁盘重新读取配置（Reread Configuration from Disk）**。如果你已经执行了一些更改且对结果不满意，可以使用此项重新加载当前配置。
  - **建议新配置。与现有菜单合并（Propose New Configuration. Merge with Existing Menus）**。如果你已经执行了一些更改且对结果不满意，可以使用此项重新加载当前配置。密码确保文件中进一步定义的选项（标题 SLES）无法以被修改的形式被选择。
  - **从头开始（Start from Scratch）**。此选项允许你从头开始创建整个配置。不会生成任何建议。
  - **从磁盘重新读取配置（Reread Configuration from Disk）**。如果你已经执行了一些更改且对结果不满意，可以使用此项重新加载当前配置。
  - **建议新配置。与现有菜单合并（Propose New Configuration. Merge with Existing Menus）**。如果你已经执行了一些更改且对结果不满意，可以使用此项重新加载当前配置。密码确保文件中进一步定义的选项（标题 SLES 10）无法以被修改的形式被选择。
  - **从硬盘恢复（Restore from Hard Disk）**。此选项允许你从硬盘恢复 MBR。这也可以用于修复错误的配置。如果你已经执行了一些更改且对结果不满意，可以使用此项重新加载当前配置。密码确保文件中进一步定义的选项（标题 SLES 10）无法以被修改的形式被选择。

# 直接进入 Shell Shell

引导屏幕允许你在加载内核向内核传递参数。例如，输入 `init=/bin/bash`，系统将直接进入 shell。

如果你想在启动期间决定是否启动每个服务（`postfix`、`sshd` 等），请在引导 提示符处使用“确认”（`confirm`）参数。

密码确保文件中进一步定义的选项（标题 SLES 10）无法以被修改的形式被选择。

在 `/boot/grub/menu.lst` 文件中，行

```
# password secret
```

在通用选项内确保文件中进一步定义的选项无法以被修改的形式被选择。

GRUB 还可以处理通过以下方式生成的 MD5 加密密码：

```
da10:~ # grub-md5-crypt
Password:
Retype password:
$1FftTeK1$qV.tOrz3EYAgVfup40
```

此字符串可以复制到 `/boot/grub/menu.lst` 中，语法如下：

```
password --md5 $1FftTeK1$qV.tOrz3EYAgVfup40
```

标题章节中的锁定（`lock`）参数用于在这些标题条目被选择之前强制进行密码查询。

| 标题 Floppy |
| lock |
| chainloader (fd0)+1 |

在引导菜单中选择 Floppy 只有在输入密码后才是可能的。
