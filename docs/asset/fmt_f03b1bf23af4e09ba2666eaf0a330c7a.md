
此 PDF 并在 docs.kali.org 自动生成 - 2013年8月19日

![](img/a9ef2e82e60ca0e2c1f6c67b184f6420_53_0.png)

接下来，你需要选择时区，然后将向分分区选项。为了快速运行，我们将使用“引导式 - 使用整个磁盘”并按照提示一路完成，以创建新的分区设置。

# KALI LINUX

## Linux 官方文档

此 PDF 并在 docs.kali.org 自动生成 - 2013年8月19日

![](img/a9ef2e82e60ca0e2c1f6c67b184f6420_54_0.png)

为了减少网络带宽，默认将选择一小部分软件包。如果你想添加不同的服务或功能，这就是你进行选择的区域。

# KALI LINUX

## Kali Linux 官方文档

此 PDF 并在 docs.kali.org 自动生成 - 2013年8月19日

```
[ ] 软件选择
目前仅安装了系统核心。要根据你的需求调整系统，你可以选择安装以下一个或多个预定义的软件集合。

选择要安装的软件：

[ ] Debian 桌面环境
[*] Web 服务器
[*] 打印服务器
[*] SQL 数据库
[ ] DNS 服务器
[ ] 文件服务器
[ ] 邮件服务器
[*] SSH 服务器
[ ] 桌面
[*] 标准系统实用程序

<继续>

<Tab> 移动: <Space> 选择: <Enter> 激活按钮
```

此时此时，安装程序将下载它所需的所有软件包并将它们安装到系统上。取决于你的互联网连接速度，这可能需要一些时间。最后，你将会被提示安装 GRUB 以完成安装。

# KALI LINUX

## Kali Linux 官方文档

此 PDF 并在 docs.kali.org 自动生成 - 2013年8月19日

![](img/a9ef2e82e60ca0e2c1f6c67b184f6420_56_0.png)

## 安装后操作

现在你已经完成了 Kali Linux 的安装，是时候对你的系统进行定制了。我们网站的 Kali 通用部分提供了更多信息，你也可以在我们的用户论坛中找到如何充分利用 Kali 的技巧。

# Kali Linux 网络 PXE 安装

## 设置 PXE 服务器

通过网络 (PXE) 启动和安装 Kali 对于没有 CDROM 或 USB 端口的单台笔记本电脑非常有用，适用于支持预填充（pre-seeding）的企业部署。

首先，我们需要安装 `dnsmasq` 来提供 DHCP/TFTP。

```bash
apt-get install dnsmasq
```

在 `dnsmasq.conf` 中，我们需要定义以下内容：

```bash
dhcp-range=192.168.1.50,192.168.1.150,255.255.255.0
dhcp-option=3,192.168.1.1
dhcp-option=6,192.168.1.2
```

配置后，需要重启 `dnsmasq`：

```bash
service dnsmasq restart
```

切换到 TTY，这将显示为一个带有登录提示的黑屏幕。我们需要以 `root` 身份登录并按照如下步骤停止 `gdm3` 服务。

```
service gdm3 stop
```

如果您使用的是 64 位的 Kali 系统，您可能想要安装 `ia32-libs` 软件包，以便 NVIDIA 安装程序能够安装 32 位库，尽管这是可选的。如果您选择不这样做，只需在安装程序询问您是否要安装 32 位库时简单地选择 `no` 即可。

```
dpkg --add-architecture i386
apt-get update
apt-get install ia32-libs
```

假设您已将 NVIDIA 驱动下载到 `/root/` 目录，我们需要赋予其执行权限并运行它。

```
chmod 755 NVIDIA-Linux-x86_64-310.44.run
./NVIDIA-Linux-x86_64-310.44.run
```

一旦安装程序完成，您应该重启电脑。系统重新启动后，您可能会看到 NVIDIA 启动界面，这表明驱动程序已正确安装，但情况并非总是如此。为了检查驱动程序是否正常工作，请执行以下命令。

# KALI LINUX

## 官方 Kali Linux 文档

此 PDF 在 docs.kali.org 上自动生成 - 2013年8月19日

```
root@kali:~# glxinfo | grep -i "direct rendering"
direct rendering: Yes
```

虽然利用 Kali 包含的 Cuda 工具超出了本文的范围，但检查并确保它们正常工作始终是一个好主意。以下命令使用 `Oclhashcat-plus` 配合软件包中包含的一些示例文件。

```
cd /usr/share/oclhashcat-plus/
./cudaHashcat-plus.bin -t 32 -a 7 example.hash ?a?a?a example.dict
cudaHashcat-plus v0.14 by atom starting...
```

- Hashes: 共 6494 个，6494 个唯一摘要

- Bitmaps: 16 位，65536 个条目，0xffffff 掩码，262144

- Workload: 256 次循环，80 个加速器

- Watchdog: 温度中止触发器设为 90c

- Watchdog: 温度保持触发器设为 80c

- Device #1: GeForce G210M, 511MB, 146Mhz, 2MCU

- Device #2: GeForce 9400M, 253MB, 1100Mhz, 2MCU

- Device #1: Kernel , /kernels/4318/m0000_a1.sm_12.64.ptx

- Device #2: Kernel , /kernels/4318/m0000_a1.sm_11.64.ptx

为 `example.dict` 生成的数据语句：121028 个单词，129988 个单词，129988 个密钥空间

```
27b7965af0346604148f2a455fe52:mo0000
a48dd0f09abafake632f88e3c641b5f:ap2300000
7becb9427f3ab85ff816f2a88f36a:sail00
1459ccf0940e63051d5a875a88acaaf:pigi00
3baa30486516a5d1260eb521a873bc0:ek110
7a872202667f1f548568596ce999f:davi0123456789
98c627ca129e64dff3bf0fbaabc66:fire0man
```

如您上方输出所示，显卡已被识别，且密码正在成功恢复。

# Kali Linux VirtualBox 虚拟机

如果您决定在 VirtualBox 中安装 Kali Linux，您将需要按照下面的说明来成功安装 Linux 增强功能（Guest Additions）工具。

您必须使用 `4.2.xx` 或更高版本 的 `VirtualBox`，以利用改进之处，包括兼容性更新以及核心应用程序和增强功能稳定性的提升。

## 在 Kali Linux 中安装 VirtualBox 增强功能

为了实现与宿主机系统良好的鼠标和屏幕集成以及文件夹共享，您将需要安装 VirtualBox 增强功能。

一旦进入了 Kali Linux 虚拟机，请打开终端窗口并执行以下命令安装 Linux 内核头。

```
apt-get update && apt-get install -y linux-headers-$(uname -r)
```

完成后，您现在可以挂载增强功能 CD 盘。这可以通过从 VirtualBox 菜单选择“设备”并选择“安装增强功能”来实现。这将 GuestAdditions iso 挂载到您 Kali Linux 虚拟机的虚拟光驱器中。当提示自动运行 CD 时，点击“取消”按钮。

![](img/a9ef2e82e60ca0e2c1f6c67b184f6420_66.png)

从终端窗口，从增强功能 CD 盘将 `VboxAdditions.run` 文件复制到您的本地系统路径，确保它是可执行的并运行它。

```
cp /media/cd-rom/VboxAdditions.run /root/
chmod 755 /root/VboxAdditions.run
cd /root
./VboxAdditions.run
```

# Kali Linux

## 官方 Kali Linux 文档

此 PDF 在 docs.kali.org 上自动生成 - 2013年8月19日

![](img/a9ef2e82e60ca0e2c1f6c67b184f6420_67.png)

重启 Kali Linux 虚拟机以完成增强功能的安装。您现在应该拥有完整的鼠标和屏幕集成，以及与宿主机共享文件夹的能力。

## 与宿主机共享文件夹
