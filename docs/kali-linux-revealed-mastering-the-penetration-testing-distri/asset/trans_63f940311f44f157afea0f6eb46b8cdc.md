

既然这些镜像已经可用，您在 ARM 设备上安装 Kali 的任务将大大简化。以下是基本步骤：

1. 下载适用于您的 ARM 设备的镜像，并确保校验和与网站上提供的校验和匹配（请参阅第 2.1.3 节“验证完整性和真实性” [第 16 页]，了解如何执行此操作的说明）。请注意，镜像通常采用 xz 压缩；请务必使用 unxz 进行解压。
2. 根据您特定 ARM 设备上可用的存储扩展插槽，获取一张容量至少为 8 GB 的 SD 卡、micro SD 卡或 eMMC 模块。
3. 使用 dd 将下载的镜像复制到存储设备。这与将 ISO 镜像复制到 USB 密钥的过程类似（请参阅第 2.1.4 节“将镜像复制到 DVD-ROM 或 USB 密钥” [第 19 页]）。

   ```bash
   dd if=kali-image.img of=/dev/something bs=512k
   ```

4. 将 SD 卡/eMMC 插入您的 ARM 设备。
5. 启动您的 ARM 设备并登录（用户名为“root”，密码为“toor”）。如果没有连接屏幕，您将不得不找出通过 DHCP 分配的 IP 地址，并通过 SSH 连接到该地址。某些 DHCP 服务器提供工具或 Web 界面来显示当前租约。如果没有此类工具，请使用嗅探器查找 DHCP 租约流量。
6. 修改 root 密码并生成新的 SSH 主机密钥，特别是当设备将在公共网络上长期运行时！步骤相对简单，请参阅“生成新的 SSH 主机密钥” [第 111 页]。
7. 享受您运行 Kali Linux 的新 ARM 设备吧！

### 特殊情况及更详细的文档

这些说明是通用的，虽然适用于大多数设备，但总有例外。例如，Chromebook 需要 *开发者模式*，而其他设备需要按特定的键才能从外部介质启动。

由于 ARM 设备添加相对频繁且规格变化很快，我们在此不会涵盖各种 ARM 设备的具体安装说明。相反，请参阅 Kali 文档网站中专门的“Kali on ARM”部分，以获取有关 Offensive Security 支持的各种 ARM 设备的信息：

http://docs.kali.org/category/kali-on-arm

## 4.5. 安装故障排除

安装程序相当可靠，但您可能会遇到 bug 或面临外部问题，例如：网络问题、镜像源故障以及磁盘空间不足。因此，能够解决安装过程中出现的问题是非常有用的。

当安装程序失败时，它会显示一个用处不大的屏幕，如图 4.26“安装步骤失败” [第 96 页] 所示。

![](img/46e3313ea1bb2892f314630a4f0677b8_122_0.png)

图 4.26 安装步骤失败

在此时，知道安装程序使用多个虚拟控制台是很有帮助的：您看到的主屏幕要么运行在第五个控制台（图形安装程序为 CTRL+Shift+F5），要么运行在第一个控制台（文本安装程序为 CTRL+Shift+F1）。在这两种情况下，第四个控制台（CTRL+Shift+F4）都会显示正在发生的事情日志，您通常可以在那里看到更有用的错误消息，例如图 4.27“安装程序的日志屏幕” [第 97 页] 中显示的消息，它揭示了安装程序磁盘空间耗尽。

```text
Apr 15 19:04:24 main-menu[8331]: (process:5559): line 88:
Apr 15 19:04:24 main-menu[8331]: (process:5559): /lib/partman/active_partition/copy/choices: not found
Apr 15 19:04:24 main-menu[8331]: (process:5559): line 88:
Apr 15 19:04:24 main-menu[8331]: (process:5559): /lib/partman/choose_partition/66partition_tree/do_op
Apr 15 19:04:24 main-menu[8331]: (process:5559): line 88:
Apr 15 19:04:24 main-menu[8331]: (process:5559): /lib/partman/active_partition/copy/choices: not found
Apr 15 19:04:24 main-menu[8331]: (process:5559):
Apr 15 19:04:24 main-menu[8331]: (process:5559): /lib/partman/free_space/50menu_do_option:
Apr 15 19:04:24 main-menu[8331]: (process:5559): line 226:
Apr 15 19:04:24 main-menu[8331]: (process:5559): /lib/partman/active_partition/copy/choices: not found
Apr 15 19:04:24 main-menu[8331]: (process:5559):
Apr 15 19:04:24 main-menu[8331]: (process:5559): /lib/partman/free_space/50menu_do_option:
Apr 15 19:04:24 main-menu[8331]: (process:5559): line 226:
Apr 15 19:04:24 main-menu[8331]: (process:5559): /lib/partman/active_partition/copy/choices: not found
Apr 15 19:04:24 main-menu[8331]: (process:5559):
Apr 15 19:04:24 main-menu[8331]: DEBUG: resolver (libgpgc1): package doesn't exist (ignored)
Apr 15 19:04:24 main-menu[8331]: INFO: Menu item 'live-installer' selected
Apr 15 19:04:24 base-installer: info: Using squashfs support for cdrom/live/filesystems.squashfs
Apr 15 19:04:24 anaconda: Installing squashfs-modules
Apr 15 19:04:24 anaconda[8545]: DEBUG: resolver (kernel-image-4.3.0-kali1-amd64-d1): package doesn't exist (ignored)
Apr 15 19:04:24 anaconda[8545]: DEBUG: retrieving squashfs-modules-4.3.0-kali1-amd64-d1 4.3.3-5ka11a
Apr 15 19:04:24 kernel: [ 165.758382] squashfs: version 4.0 (2009/01/31) Phillip Lougher
Apr 15 19:04:24 kernel: [ 165.764051] loop: module loaded
Apr 15 19:04:45 base-installer: error: The task copying the live system failed (only 9230 out of 135225 files have been copied, last file was 'usr/lib/menu/4x/wbar-menu.xpm')
Apr 15 19:04:45 main-menu[8331]: (process:849:) tar: write error: No space left on device
Apr 15 19:04:45 main-menu[8331]: tar: /w/overlay: Broken pipe
Apr 15 19:04:45 main-menu[8331]: WARNING ***: Configuring 'live-installer' failed with error code 1
Apr 15 19:04:45 main-menu[8331]: WARNING ***: Menu item 'live-installer' failed.
```

**图 4.27 安装程序的日志屏幕**

第二个和第三个控制台（分别为 CTRL+Shift+F2 和 CTRL+Shift+F3）托管 shell，您可以使用它们来更深入地调查当前状况。大多数命令行工具由 BusyBox 提供，因此功能集相当有限，但这足以解决您可能会遇到的大多数问题。

### 可以在安装程序 Shell 中执行的操作

您可以使用 `debconf-get` 和 `debconf-set` 检查和修改 debconf 数据库。这些命令对于测试预置值特别方便。

您可以使用 `cat` 或 `more` 检查任何文件（例如完整的安装日志，位于 `/var/log/syslog` 中）。您可以使用 `nano` 编辑任何文件，包括正在安装到系统上的所有文件。一旦安装过程中的分区步骤完成，根文件系统将挂载在 `/target` 上。

配置网络访问后，您可以使用 `wget` 和 `nc` (netcat) 通过网络检索和导出数据。

一旦您在安装程序主失败屏幕（图 4.26，“安装步骤失败” [第 96 页]）上点击“继续”，您将被返回到一个通常不会看到的屏幕（图 4.28 所示的安装程序主菜单 [第 98 页]），该屏幕允许您依次启动另一个安装步骤。如果您通过 shell 访问成功修复了问题（恭喜！），那么您可以重试失败的步骤。

![](img/46e3313ea1bb2892f314630a4f0677b8_124_0.png)

**图 4.28** *安装程序的主菜单*

如果您无法解决问题，可能需要提交 bug 报告。该报告必须包含安装程序日志，您可以使用主菜单的“保存调试日志”功能获取日志。它提供了多种导出日志的方式，如图 4.29“保存调试日志 (1/2)” [第 99 页] 所示。

![](img/46e3313ea1bb2892f314630a4f0677b8_125_0.png)

**图 4.29** 保存调试日志 (1/2)

最便捷也是我们推荐的方法是让安装程序启动一个 Web 服务器来托管日志文件（图 4.30，“保存调试日志 (2/2)” [第 100 页]）。然后，您可以在同一网络上的另一台计算机上启动浏览器，下载所有日志文件以及您使用每个屏幕上可用的“屏幕截图”按钮拍摄的屏幕截图。

![](img/46e3313ea1bb2892f314630a4f0677b8_126_0.png)

## 4.6. 总结

在本章中，我们重点关注了 Kali Linux 的安装过程。我们讨论了 Kali Linux 的最低安装要求、标准文件系统完全加密文件系统安装过程、允许无人值守安装的预置配置、如何在各种 ARM 设备上安装 Kali Linux，以及在安装失败这一罕见情况下的应对措施。

总结提示：

