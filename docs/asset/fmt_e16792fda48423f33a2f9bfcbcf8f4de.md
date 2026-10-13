
```
[student@servera ~$] su - manager1
Password: redhat
[manager@servera ~$] ls -l /remote/management/
Total 4
-rw-r--r-- 1 root managers 46 Apr 4 01:13 Welcome.txt
[manager@servera ~$] cat /remote/management/Welcome.txt
###Welcome to Management Folder on SERVER###
[manager@servera ~$] echo TEST1 /remote/management/Test.txt
[manager@servera ~$] cat /remote/management/Test.txt
TEST1
[manager@servera ~$] ls -l /remote/operation/
ls: cannot open directory '/remote/operation/': Permission denied
[manager@servera ~$] ls -l /remote/production/
ls: cannot open directory '/remote/production/': Permission denied
[manager@servera ~$] exit
logout
[student@servera ~$]
```

### 3.3. 切换到 `dbuser1` 用户并测试访问。

```
[student@server ~$] su - dbuser1
Password: redhat
[dbuser1@servera ~$] ls -l /remote/production/
Total 4
-rw-r--r-- 1 root production 46 Apr 4 01:13 Welcome.txt
[dbuser1@servera ~$] cat /remote/production/Welcome.txt
###Welcome to Production Folder on SERVER###
[dbuser1@servera ~$] echo TEST2 /remote/production/Test.txt
[dbuser1@servera ~$] cat /remote/production/Test.txt
TEST2
[dbuser1@servera ~$] ls -l /remote/operation/
ls: cannot open directory '/remote/operation/': Permission denied
[dbuser1@servera ~$] ls -l /remote/management/
ls: cannot open directory '/remote/management/': Permission denied
```

### 3.4. 切换到 `controller1` 用户并测试访问。

```
[student@servera ~] su - controller1
Password: redhat
[controller1@servera ~$] ls -l /remote/operation/
total 4
-rw-r--r-- 1 root root 45 Apr 4 01:13 Welcome.txt
[controller1@servera ~$] cat /remote/operation/Welcome.txt
##Welcome to Operation on SERVER###
[controller1@servera ~$] echo TEST3 > /remote/operation/Test.txt
[controller1@servera ~$] cat /remote/operation/Test.txt
TEST3
[controller1@servera ~$] ls -l /remote/management/
ls: cannot open directory '/remote/management/': Permission denied
[controller1@servera ~$] ls -l /remote/production/
ls: cannot open directory '/remote/production/': Permission denied
[controller1@servera ~$] exit
logout
[student@servera ~]
```

### 3.5. 探索 NFS 导出的挂载选项。

```
[student@servera ~] mount | grep nfs
pipe-types servera.lab.example.com:/shares/management on /remote/management nfs (rw,sync)
pipe-types servera.lab.example.com:/shares/production on /remote/production nfs (rw,sync)
pipe-types servera.lab.example.com:/shares/operation on /remote/operation nfs (rw,sync)
```

### 3.6. 以学生用户身份返回工作站机器。

```
[student@servera ~] exit
logout
[student@workstation~]$
```

## Red Hat Linux 启动过程

现代计算机系统是硬件和软件的复杂组合。从关机状态启动到带有登录提示的运行系统，需要许多硬件和软件协同工作。以下列表列出了 Red Hat Linux 启动涉及的任务的高级概述：

- 机器上电。系统固件（UEFI 或旧版 BIOS）运行上电自检 (POST) 并开始初始化硬件。

- 使用 BIOS 或 UEFI 设置进行配置，您通常在启动早期按下特定按键（如 F2）进入设置。

- 系统固件搜索可启动设备，可以是 UEFI 中配置的，也可以通过顺序搜索所有磁盘中的主引导记录 (MBR)。

- 使用 BIOS 或 UEFI 方案进行配置，您通常在启动早期按下特定的组合键（如 F2）进入。

- 系统固件从磁盘读取加载程序，然后将系统控制权交给引导加载程序。在 Red Hat Linux 9 上，引导程序是 GRUB2。

- 使用 `grub-install` 命令配置，将 GRUB2 安装为 BIOS 磁盘的引导程序。您可以使用较短版本的命令 `poweroff` 和 `reboot`，它们是其对应的 `systemctl` 命令的符号链接。

- 系统在 UEFI 上直接执行 `grub2-install` 生成一个新的 `grubx64.efi` 文件，该文件包含安全启动（Secure Boot）所需的签名。

- GRUB2 从 `/boot/grub/grub.cfg` (BIOS) 或 `/boot/efi/EFI/redhat/grub.cfg` (UEFI) 加载配置，并显示菜单，您可以从中选择启动哪个内核。

- 在您选择内核或超时后，引导加载程序从磁盘加载内核和 `initramfs` 并将其放入内存。`initramfs` 是一个包含启动所需的所有硬件内核模块、初始化脚本的存档；在 Red Hat Linux 9 上，`initramfs` 本身包含了一个完整的可运行系统。通过 `/etc/dracut.d/` 目录、`dracut` 命令和 `initrd` 命令配置以初始化 initramfs。引导加载程序接管内核，将内核命令行指定的任何选项传递给内存中 initramfs 的位置。通过 `/etc/grub.d`、`/etc/default/grub` 文件和 `grub2-mkconfig` 命令生成 `/boot/grub2/grub.cfg` 文件。

- 内核初始化所有硬件，因为它可以在 initramfs 中找到作为 PID 1 的驱动程序。在 Red Hat Linux 9 上，`/sbin/init` 是指向带有内核 `init=command-line` 参数配置的 systemd 的链接。

- 来自 `initramfs` 的 `systemd` 实例执行 `initrd` 目标的所有单元。这包括来自 `/sysroot` 目录的磁盘根文件系统。内核将根文件系统从 initramfs 切换（挂载）到通过 `/etc/fstab` 文件配置的根文件系统。

- `systemd` 查找默认目标（通过内核命令行传递或在系统中指定），然后启动符合该目标配置的单元，并解决单元之间的依赖关系。本质上，`systemd` 目标是系统应该激活以达到所需状态的一组单元。这些目标通常启动一个文本 UI 或图形登录界面。通过 `/etc/systemd/default.target` 文件和 `/etc/systemd/` 目录配置。
