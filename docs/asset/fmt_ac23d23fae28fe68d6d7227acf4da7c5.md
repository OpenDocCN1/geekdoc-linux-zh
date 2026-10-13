
如果输出仍然显示，运行 `sndconfig` 声卡配置程序来设置你的声卡。

# 笔记本电脑视频问题解决

笔记本电脑的安装通常是最难执行的类型，因为构建笔记本电脑的组件通常使用专用硬件，或修改标准 PC 组件，以便将 PC 功能挤入笔记本的有限空间内，或满足重量、电源或功能需求。更糟糕这些实际担忧的是，为了保护秘密，这些工程决策很少公开记录。因此，你通常必须使用试错法并依赖他人的经验。

![](img/d1fb1ff3244ecb66d002a5e633e6f729_802_0.png)

少数笔记本电脑制造商积极支持 Linux。例如，IBM 在特定的笔记本电脑上预装了 Linux，专门的 Linux 硬件供应商也是如此。缺乏支持令人沮丧，但在制造商能够开发 Windows 驱动的同时开发 Linux 驱动之前，在笔记本电脑上安装 Linux 将继续是一个挑战。

从 CD-ROM 或软磁盘尝试图形化 Red Hat Linux 安装时，你可能会看到笔记本屏幕变空白无法继续。在这种情况下，尝试基于文本安装可能会有效——如果安装程序无法使用你的视频硬件，强制进行图形化安装很少奏效。对于某些笔记本电脑，如果你在启动提示符输入以下参数，图形化安装程序可能会运行：

```bash
boot: linux vga=2
```

同样，你可以使用以下参数尝试所有可能的 VGA 模式：

```bash
boot: linux vga=ask
```

在完全放弃之前，请查看 Linux 和笔记本电脑的权威参考：Linux Laptop 网站，http://www.cs.utexas.edu/users/kharker/linux-laptop/。

# SIGNAL 7 和 SIGNAL 11 问题

人们在安装 Red Hat Linux 时遇到的最混乱的问题可能是类似于致命信号 11 或致命信号 7 的错误消息。信号 11 和 7 表示内存或系统数据线存在硬件问题。Red Hat Linux 不会导致此类错误。相反，它揭露了问题，因为 Linux 内核通常会将硬件推到能力的极限，远超 DOS 或 Windows，往往会暴露出标准的硬件缺陷。

你应该如何处理？要要做的是检查你是否拥有来自 Red Hat 的最新安装镜像。如果最新镜像仍然失败，问题可能是硬件。常见的嫌疑对象包括损坏的 RAM 芯片或缺陷的 CPU 缓存。尝试在 BIOS 中关闭 CPU 缓存，看看问题是否消失。同样，尝试在系统的内存槽中调换内存，以查看错误是与插槽还是内存有关。如果这不能解决问题，Signal 11 网站 http://www.bitwizardard.nl/sig11/ 可能会对你有帮助。如果所有其他方法都失败了，请将系统送到电脑维修店让他们测试硬件，并强调 RAM 和可能的 CPU 缓存需要使用硬件测试器进行测试。

# 解决文件系统问题

本节中的提示帮助你解决在处理 Linux 文件时可能遇到的常见问题。

# 无法删除文件

如果你想删除或重命名文件，请使用 `ls` 命令验证你是否有权限执行操作。如果你收到类似于 `rdir: directory empty` 的错误消息，请确保你的当前目录不在文件系统上。

## 第 28 章：故障排除与问题解决

例如，如果 `/` 位于 `/dev/sdb` 且系统添加了一个较低 SCSI ID 的新驱动器，那么之前的 `/dev/sdb` 驱动器将变为 `/dev/sdc`。这种变化会导致 `mount` 命令在尝试挂载 `/` 时产生错误。分区标签解决了这个问题，因为 `mount` 尝试尝试挂载由其标签标识的分区，而不是尝试挂载 `/dev/sd1` 并期望它是 `/`。这个想法在理论上是非常棒的，只要你保持分区标签少于 16 个字符。Red Hat 的更新包含针对 `mount` 和 `e2fsprops` 的错误修复，修复了这两个程序。

## 避免每次系统重启时都进行文件系统检查

如果你每次启动系统时都不得不运行 `fsck`，最可能的疑点是你最后一次关机时分区没有被正确卸载。你可以做的最重要的事情是确保正确地关闭机器。关机通过两种方法之一完成：

- 如果你处于文本模式——运行级别 3——你应该以 root 身份登录并输入以下命令：
  `# sync;sync;sync;shutdown -r now`
- 如果你使用图形化登录——运行级别 5——系统 → 停止（Halt）。最后，你会看到显示“Power Down”的行，表示可以关闭机器了。

在任何情况下，如果你正在运行 APM，Linux 会尝试使用 BIOS 停止机器。

## 让 Zip 驱动器工作

要让连接到并行端口的 Iomega Zip 驱动器工作，请使用以下步骤：

1. 编辑 `/etc/conf.modules` 并添加以下行：
  `alias parport_lowlevel parport_pc`
  `alias scsi_hostadapter ppa`
2. 以 root 身份登录并运行以下命令：
  `# modprobe ppa`

如果你在使用 IDE Zip 驱动器时遇到问题，首先检查驱动器中是否有磁盘，并确保你将其挂载为分区 4 而不是 1；例如，使用 `/dev/hdc4` 而不是 `/dev/hdc1`。此原因是 Macintosh 使用分区 4 作为其数据分区，如果数据在另一个分区上，它就会出现问题。

## 解决网络问题

如果你无法访问网络上的主机，请确保在 `/etc/resolv.conf` 中至少列有一个名称服务器。如果外部系统无法连接到你的系统，请记住 `hosts.allow` 和 `hosts.deny` 文件的读取和应用顺序。启动 Internet 服务的程序会查询 `/etc/hosts.allow`。如果 TCP wrappers 没有找到匹配的规则，它将应用 `/etc/hosts.deny` 中的第一个匹配规则（如果有的话）。如果两个文件都不包含匹配项，则允许访问。

如果你是从较早版本升级的 Red Hat Linux，可能看起来你没有保留网络服务配置文件的内容。然而，事实并非如此。配置文件被重命名为带有 `.rpmsave` 扩展名的文件，可以在网络服务的目录中找到它们。例如，你可能会发现旧的 `/etc/http/conf/httppd.conf` 文件被重命名为 `/etc/http/conf/httppd.conf.rpmsave`。应该将更改复制到新版本的配置文件中。

- 带有 `.rpm` 扩展的文件是不属于已升级或安装的 RPM 软件包的配置文件。
- 带有 `.rpmsave` 扩展的文件是属于已升级或安装的 RPM 软件包的配置文件。
- 带有 `.rpmnew` 扩展的文件表示由升级的软件包安装的新版本文件。

受影响的网络服务配置文件包括但不限于：

- `/etc/http/conf/httpd.conf`
- `/etc/samba/smb.conf`
- `/etc/sendmail.cf`
- `/etc/named.conf`
- `/etc/dhcp.conf`

为了避免不幸的事故和不必要的恐慌，请在升级或安装最新版本的 Red Hat Linux 之前备份你的数据。第 22 章向你展示了如何备份 Red Hat 系统![](img/d1fb1ff3244ec66d002a5e63e6f729.png)

## 使用调制解调器上网

如果你在让调制解调器工作遇到困难，请首先通过检查 http://hardware.redhat.com/ 硬件列表来验证其受支持。接下来，查看系统是否检测到了调制解调器，并确保它与其他资源没有冲突。你可以使用以下命令进行检查：

```
# cat /proc/ioports
0000-003f : dma1
0020-003f : pic1
0040-005f : timer
0060-006f : keyboard
0070-007f : rtc
00a0-00bf : pic2
00c0-00df : dma2
00f0-00ff : fpu
0170-0177 : idel
01f0-01f7 : ide0
0220-022f : soundaster
02f8-02ff : serial(auto)
0330-0333 : UART
0376-0376 : idel
03c0-03df : vga
03f6-03f6 : ide0
03f8-03ff : serial(auto)
d000-d0d7 : eth0
d800-d807 : ide0
d808-d80f : idel
```

```
# cat /proc/interrupts
CPU
0: 1296380 XT-PIC timer
1: 30736 XT-PIC keyboard
2: 0 XT-PIC cascade
5: 1 XT-PIC soundaster
8: 1 XT-PIC rtc
0: 73593 XT-PIC eth0
2: 159669 XT-PIC PS/2 Mouse
3: 1 XT-PIC fpu
4: 246863 XT-PIC ide0
5: 584998 XT-PIC idel
```
