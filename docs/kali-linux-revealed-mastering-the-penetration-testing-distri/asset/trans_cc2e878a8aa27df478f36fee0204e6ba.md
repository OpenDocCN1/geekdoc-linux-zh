

## 2.1.4. 在 DVD-ROM 或 U 盘上复制映像

PGP/GPG 安全模型非常独特。任何人都可以用任何身份生成任何密钥，但你只会信任那些由你已信任的其他密钥签名的密钥。当你签名一个密钥时，你证明你见过该密钥的持有者，并且你知道与之相关的身份是正确的。并且你定义了你所信任的初始密钥集合，显然其中包括你自己的密钥。

该模型有其自身的局限性，因此你可以选择通过 HTTPS（或从密钥服务器）下载 Kali 的公钥，并仅仅决定信任它，因为其指纹与我们在多个地方（包括本书稍上方）公布的内容匹配：

```
$ wget -q -O - https://www.kali.org/archive-key.asc | gpg --import
[...]
$ gpg --keyserver hkp://keys.gnupg.net --recv-key ED444FF07D8D0BF6
gpg: key ED444FF07D8D0BF6: public key "Kali Linux Repository <dev@kali.org>" imported
gpg: Total number processed: 1
gpg: imported: 1 (RSA: 1)
[...]
$ gpg --fingerprint 7D8D0BF6
[...]
Key fingerprint = 44C6 513A 8E4F B303 0875 F758 ED44 4FF0 7D8D 0BF6
[...]
```

获取密钥后，你可以使用它来验证分发映像的校验和。让我们下载包含校验和（SHA256SUMS）的文件及其关联的签名文件（SHA256SUMS.gpg），并验证签名：

```
$ wget http://cdimage.kali.org/current/SHA256SUMS
[...]
$ wget http://cdimage.kali.org/current/SHA256SUMS.gpg
[...]
$ gpg --verify SHA256SUMS.gpg SHA256SUMS
gpg: Signature made Thu 16 Mar 2017 08:55:45 AM MDT
gpg: using RSA key ED444FF07D8D0BF6
gpg: Good signature from "Kali Linux Repository <dev@kali.org>"
```

如果你收到“Good signature”（良好签名）消息，你可以信任 SHA256SUMS 文件的内容，并使用它来验证你下载的文件。否则，存在问题。你应该审查是否从合法的 Kali Linux 镜像站点下载了文件。

注意，只要下载的 ISO 文件位于同一目录下，你可以使用以下命令行来验证下载的文件是否具有与 SHA256SUMS 中列出的相同校验和：

```
$ grep kali-linux-2017.1-amd64.iso SHA256SUMS | sha256sum -c
kali-linux-2017.1-amd64.iso: OK
```

如果没有收到“OK”响应，那么下载的文件与 Kali 团队发布的文件不同。该文件不可信，不应使用。

除非你想在虚拟机中运行 Kali Linux，否则 ISO 映像本身用途有限。你必须将其刻录到 DVD-ROM 或复制到 U 盘上，才能将机器引导进入 Kali Linux。

我们将不会介绍如何将 ISO 映像刻录到 DVD-ROM 上，因为该过程因平台和环境而异，但在大多数情况下，右键单击 `.iso` 文件会显示一个上下文菜单项，用于执行 DVD-ROM 刻录应用程序。试试看！

> **警告**
> 在本节中，你将学习如何使用 Kali Linux ISO 映像覆盖任意磁盘。在启动操作之前，请务必仔细检查目标磁盘，因为一次错误很可能导致数据完全丢失，并可能对你的设置造成无法修复的损害。

### 在 Windows 上创建可引导的 Kali USB 驱动器

作为前提条件，你应该下载并安装 *Win32 Disk Imager*：

- https://sourceforge.net/projects/win32diskimager/

将你的 U 盘插入 Windows PC，并记下与其关联的驱动器标识符（例如，“E:\").

启动 *Win32 Disk Imager*，选择你想要复制到 U 盘上的 Kali Linux ISO 文件。验证所选设备的字母是否与分配给 U 盘的字母一致。一旦你确定已选择了正确的驱动器，点击 *Write*（写入）按钮，并确认你要覆盖 U 盘的内容，如图 2.2“工作中的 Win32 Disk Imager”[第 20 页]所示。

![](img/46e3313ea1bb2892f314630a4f0677b8_46_0.png)

复制完成后，从 Windows 系统中安全弹出 USB 驱动器。现在你可以使用该 USB 设备引导 Kali Linux。

### 在 Linux 上创建可引导的 Kali USB 驱动器

在 Linux 环境中创建可引导的 Kali Linux USB 驱动器很容易。GNOME 桌面环境在许多 Linux 发行版中默认安装，它附带了一个 Disks 工具（位于 gnome-disk-utility 软件包中，该工具已安装在标准 Kali 映像中）。该程序显示一个磁盘列表，当你插入或拔出磁盘时，该列表会动态刷新。当你在磁盘列表中选中你的 U 盘时，详细信息会出现，帮助你确认你选择了正确的磁盘。注意，你可以在标题栏中找到其设备名称，如图 2.3“GNOME Disks”[第 21 页]所示。

![](img/46e3313ea1bb2892f314630a4f0677b8_47_0.png)

图 2.3 GNOME Disks

点击菜单按钮，并在显示的弹出菜单中选择 Restore Disk Image...（恢复磁盘映像...）。选择你之前下载的 ISO 映像，点击 Start Restoring...（开始恢复...），如图 2.4“Restore Disk Image Dialog”[第 21 页]所示。

![](img/46e3313ea1bb2892f314630a4f0677b8_47_1.png)

图 2.4 Restore Disk Image Dialog

在它将映像复制到 U 盘完成之前（图 2.5“映像恢复进度”[第 22 页]），你可以享受一杯咖啡。

![](img/46e3313ea1bb2892f314630a4f0677b8_48_0.png)

**图 2.5** *映像恢复进度*

### 从命令行创建可引导的 USB 驱动器

虽然图形化过程相当简单直观，但对于命令行用户来说，操作也同样容易。

当你插入 U 盘时，Linux 内核会检测到它并为其分配一个名称，该名称会打印在内核日志中。你可以通过检查 dmesg 返回的日志来找到其名称。

```
$ dmesg
[...]
[234743.896334] usb 1-1:2: new high-speed USB device number 6 using ehci-pci
[234743.990761] usb 1-1:2: New USB device found, idVendor=06ac, idProduct=0820
[234743.990771] usb 1-1:2: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[234743.990774] usb 1-1:2: Product: Store'n'go
[234743.990777] usb 1-1:2: Manufacturer: Verbatim
[234743.990780] usb 1-1:2: SerialNumber: 0390627052AF897
[234743.998185] usb-storage 1-1:2.0: USB Mass Storage device detected
[234743.992037] scsi host7: usb-storage 1-1:2:1.0
[234744.993818] scsi 7:0:0:0: Direct-Access VBTM Store'n'go 6.51 [—]
[234744.994425] sd 7:0:0:0: Attached accessible generic scsi type 0
[234744.995753] sd 7:0:0:0: [sdb] 3903487 512-byte logical blocks: (2.00 GB / 1.86 GiB)
[234744.996663] sd 7:0:0:0: [sdb] Write Protect is off
[234744.996669] sd 7:0:0:0: [sdb] Mode Sense: 45 00 00 08
[234744.997518] sd 7:0:0:0: [sdb] No Caching mode page found
[234744.997524] sd 7:0:0:0: [sdb] Assuming drive cache: write through
[234745.009375] sdb: sdb1
[234745.015113] sd 7:0:0:0: [sdb] Attached SCSI removable disk
```

现在你知道 U 盘作为 /dev/sdb 可用，你可以使用 dd 命令继续复制映像：

```
# dd if=kali-linux-light-2017.1-amd64.iso of=/dev/sdb
2070784+0 records in
2070784+0 records out
1060241408 bytes (1.1 GB, 1011 MiB) copied, 334.175 s, 3.2 MB/s
```

注意，该操作需要 root 权限才能成功，你还应确保 U 盘未被使用。也就是说，你应该确保其任何分区都没有被挂载。该命令还假设它在托管 ISO 映像的目录下运行，否则需要提供完整路径。

供参考，`if` 代表"input file"（输入文件），`of` 代表"output file"（输出文件）。`dd` 命令从输入文件读取数据并将其写回输出文件。它不显示任何进度信息，因此你必须耐心等待它完成工作（该命令耗时超过半小时并不罕见）。如果你想双重检查命令是否正在工作，请查看 U 盘上的写入活动 LED。上面显示的统计信息仅在命令完成后显示。在 OS X/macOS 上，你还可以在操作期间按 CTRL+T 获取关于复制的统计信息，包括已复制的数据量。

### 在 OS X/macOS 上创建可引导的 Kali USB 驱动器

OS X/macOS 基于 UNIX，因此创建可引导 Kali Linux USB 驱动器的过程与 Linux 过程类似。一旦你下载并验证了你选择的 Kali ISO 文件，请使用 `dd` 将其复制到你的 U 盘上。

要识别 U 盘的设备名称，运行 `diskutil list` 以列出系统上可用的磁盘。接下来，插入你的 U 盘并再次运行 `diskutil list` 命令。第二个输出应该会列出额外的磁盘。通过比较两个命令的输出，你可以确定 U 盘的设备名称。查找标识你的 USB 磁盘的新行，并记下 `/dev/diskX`，其中 X 代表磁盘 ID。

你应该确保 U 盘未被挂载，这可以通过显式的 unmount 命令实现（假设 `/dev/disk6` 是 U 盘的设备名称）：

```
$ diskutil unmount /dev/disk6
```

现在继续执行 `dd` 命令。这次，添加一个补充参数 `bs` 用于块大小。它定义了从输入文件读取然后写入输出文件的块的大小。

```
# dd if=kali-linux-light-2017.1-amd64.iso of=/dev/disk6 bs=1M
1811+0 records in
1811+0 records out
1060241408 bytes transferred in 327.061 secs (3242328 bytes/sec)
```

就这样。你的 U 盘现已就绪，你可以从中引导或使用它来安装 Kali Linux。

![](img/46e3313ea1bb2892f314630a4f0677b8_49_0.png)

¹http://support.apple.com/kb/ht1310

