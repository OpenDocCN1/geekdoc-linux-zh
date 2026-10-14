

当您选择“引导加载程序安装”选项卡时，您会看到图 11-5 所示的内容。

![](img/9129877170834ca9d5fdac5319bf5f12_395_0.png)

图 11-5

- **Boot Loader Type**—您可以使用此选项在 GRUB 和 LILO 之间切换。会弹出一个对话框让您指定此更改应如何执行。
- **Boot Loader Location**—您可以使用此选项定义引导加载程序的安装位置。
- **Boot Loader Installation Details**—此选项提供专门的配置选项，例如激活某个分区或更改磁盘顺序以对应 BIOS 中的顺序。
- **Other**—选择此选项时，会打开一个下拉列表，其中包含以下附加选项：
  - **Edit Configuration Files**—此选项可让您显示并编辑配置文件（`/boot/grub/device.map`、`/boot/grub/menu.lst` 或 `/etc/grub.conf`）。
- *Propose New Configuration*—此选项会生成新的配置建议。其他分区上找到的旧版 Linux 或其他操作系统将被包含在引导菜单中，使您能够启动 Linux 或其旧引导加载程序。后者会带您进入第二个引导菜单。
- *Start from Scratch*—此选项可让您从头创建整个配置。不会生成任何建议。
- *Reread Configuration from Disk*—如果您已进行一些更改且对结果不满意，此选项可让您重新加载当前配置。
- *Propose and Merge with Existing GRUB Menus*—如果在其他分区安装了其他操作系统和旧版 Linux，则菜单将从新 SUSE Linux 的条目、其他系统的条目以及旧引导加载程序菜单的所有条目生成。

  此过程可能需要一些时间，且仅在 GRUB 下可用。
- *Restore MBR from Hard Disk*—此选项会恢复保存在硬盘上的 MBR。
- *Write Bootloader Boot Code to Disk*—选择此选项可将引导加载程序代码写入磁盘。

要完成引导加载程序的配置，请选择“完成”以保存配置更改。

## 直接将系统引导到 Shell

GRUB 引导加载程序的引导屏幕可让您输入修改 Linux 内核行为的参数。

GRUB 引导屏幕底部是 **Boot Options** 字段。要添加引导选项，请选择一个操作系统并在 Boot Options 字段中输入额外的引导选项。

一种访问无法正常启动的系统的方法是为 init 进程设置不同的程序。通常，Linux 内核会尝试查找名为 init 的程序并将其作为第一个进程启动。随后所有其他进程都由 init 启动。

使用引导参数 init=new_init_program，您可以更改内核加载的第一个程序。例如，通过输入引导参数 init=/bin/bash，系统将直接启动到 bash shell。

您将直接以 root 身份登录，无需输入密码。
您可以使用此 shell 访问文件系统并修复错误配置。

![](img/9129877170834ca9d5fdac5319bf5f12_396_0.png)

根据 Linux 系统的不同，引导到 shell 后根文件系统可能以只读方式挂载。在这种情况下，您需要使用以下命令重新挂载文件系统，以便更改配置文件：

```
mount -o remount,rw,sync -t filesystem_type device_name
mount_point
```

在 bash 提示符下输入 exec /sbin/init 将用 init 程序替换 shell，并继续引导过程直至达到默认运行级别。

如果您想防止如上所述访问机器，可以更改引导配置，要求在编辑内核命令行之前输入密码。

在 /boot/grub/menu.lst 文件中，常规选项中的以下行可确保文件后面部分定义的选项（title SLED 10 等）只能以未修改的形式被选中：

```
Password secret
```

使用额外的内核参数需要密码 secret。由于图形引导菜单可能被用来规避密码功能，因此在配置文件中出现 password 条目时它会自动被禁用。

GRUB 还可以处理以如下方式生成的 MD5 加密密码：

```
da10:~ # grub-md5-crypt
Password:
Retype password:
$1$FTeTk1$qaV.tOrzbg3EYAgVfNup40
```

此字符串可以用以下语法复制到 /boot/grub/menu.lst 文件中：

```
password --md5 $1$FTeTk1$qaV.tOrzbg3EYAgVfNup40
```

title 部分中的 lock 参数可用于在选择这些 title 条目之前强制进行密码查询。

```
title Floppy
    lock
    chainloader (fd0)+1
```

现在只有在输入密码后才能在引导菜单中选择 Floppy。参数 password 也可用于单个 title 条目中，以为这些 title 条目定义特殊密码。

请注意，密码功能仅能适度增强安全性，因为它无法防止从其他介质（如 SLED 10 救援系统）启动计算机然后访问硬盘上的文件。

![](img/9129877170834ca9d5fdac5319bf5f12_397_0.png)

如果您想为每个服务（postfix、sshd 等）决定是否在引导时启动它，请在引导提示符下使用 confirm 参数。

![](img/9129877170834ca9d5fdac5319bf5f12_397_1.png)

## 练习 11-1：管理引导加载程序

在本练习中，您将练习引导到 shell 并修改 /boot/grub/menu.lst。

在引导提示符下输入 init=/bin/bash，修改 /boot/grub/menu.lst 以要求在修改内核参数之前输入密码，并测试新的 GRUB 配置。

![](img/9129877170834ca9d5fdac5319bf5f12_398_0.png)

如果使用 USB 键盘，此练习将无法工作，因为 USB 驱动程序通常在 init 过程的后期阶段才加载。如果您的机器配备了 USB 键盘，则需要将模块添加到初始 RAM 磁盘中才能使此练习工作。

要使用 USB 键盘完成此练习，请先执行以下步骤：
在终端窗口中输入 `lsmod` 以了解加载了哪些 USB 模块。然后启动 YaST，选择 **System > /etc/sysconfig Editor**。展开 **System > Kernel** 子部分。在 **INITRD_MODULES** 中添加使用的模块，例如 `usbhid uhci_hcd ehci_hcd`。关闭对话框。
在终端窗口中（以 root 身份）输入 `mkinitrd`。

### 完成此练习的详细步骤

1. 从 GNOME 桌面，选择 Computer > Shutdown > Restart。
2. 当显示引导菜单时，按 Spacebar 停止计时器。
3. 在 Boot Options 字段中输入 `init=/bin/bash` 然后按 Enter。
4. 使用 vi 编辑 `/boot/grub/menu.lst`。
   在以 gfxmenu 开头的行前加上注释符号（#）。在其下方添加以下行：

```
password secret
```

5. （可选）为避免在配置文件中以明文形式保存密码，您可以使用 MD5-Hash 代替。您可以在 vi 中使用以下命令创建并将其包含在文件中：

按 Esc

```
:r! echo -e "secret\nsecret" | grub-md5-crypt
```

按 Enter

grub-md5-crypt 的输出中的几行将被包含在文件中，包括您密码的 MD5-hash。

删除 grub-md5-crypt 输出中的行，只保留包含哈希的行。如果文件中仍有“password secret”行，也将其删除。

在哈希所在行的开头写入 `password --md5`，使该行看起来如下：

```
password --md5 $1$t9kdK1$jjuACbOwF18QVFv3C17b.v0
```

![](img/9129877170834ca9d5fdac5319bf5f12_398_1.png)

您的哈希值将与此处给出的不同。

通过按 Esc 并输入 `:wq` 保存文件。
6. 将根文件系统挂载为只读：

```
mount -o remount,ro /
```

如果在下一步重置计算机时文件系统以读写方式挂载，则计算机重新启动时将需要进行文件系统检查。
7. 重置计算机。
   您会注意到启动屏幕现在看起来不同，因为您关闭了图形菜单。
8. 如果您想编辑内核命令行，请按 **p** 然后输入步骤 4 和 5 中使用的密码。简短的帮助文本会告知您可用的选项。
9. 按 **b** 引导计算机。
10. 撤销 `/boot/grub/menu.lst` 中的更改：
    a. 以 geeko 登录，打开终端窗口，并 `su -` 切换到 root（密码 `n0v3ll`）。
    b. 使用 vi 打开 `/boot/grub/menu.lst`，在以 `password` 开头的行开头加上注释符号，并删除以 `gfxmenu` 开头的行前的注释符号。保存文件并通过按 Esc 并输入 `:wq` 关闭 vi。

## 目标 3—管理运行级别

管理运行级别是 Linux 系统管理的重要组成部分。在本目标中，您将学习运行级别是什么、init 程序的作用以及如何配置和更改运行级别：

- The init Program and Linux Runlevels
- init Scripts and Runlevel Directories
- Change the Runlevel

### The init Program and Linux Runlevels

为了理解 Linux 系统初始化和管理，您需要研究以下内容：

- The init Program
- The Runlevels
- init Configuration File (`/etc/inittab`)

**The init Program** 系统由 `/sbin/init` 初始化，它由内核作为系统的第一个进程启动。

此进程或其子进程之一启动所有其他进程。此外，由于 init 是最后一个运行的进程，它可确保所有其他进程正确结束。这意味着 init 控制系统的整个启动和关闭过程。

由于这一优先地位，信号 9（SIGKILL），通常可用于结束所有进程，对 init 无效。

init 的配置文件是 `/etc/inittab`。根据此文件中的条目，init 启动各种脚本。所有这些脚本都位于 `/etc/init.d/` 目录中。

`/etc/inittab` 中的配置一部分是系统在引导后使用的运行级别。

