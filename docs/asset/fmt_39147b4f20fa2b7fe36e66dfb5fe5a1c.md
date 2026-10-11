
# BeagleBone Black Kali Linux – 预构建版本

以下指令将帮助您在 BeagleBone Black 上安装 Kali Linux

- 1. 准备一个快速的 8 GB 微 SD 卡来安装 Kali Linux。我们推荐使用 Class10 类 SD 卡。
- 2. 从 https://www.offensive-security.com/kali-linux-arm-images/ 下载适用于 BeagleBone Black 的 Kali Linux ISO。
- 3. 现在您可以使用 `dd` 工具将此镜像写入 SD 卡。在我们展示的示例中，我们将把 Kali Linux 安装在路径为 `/dev/sdb` 的 SD 卡上。您可以根据自己的需求更改此。

注意：这将擦除您 SD 卡上的所有内容。选择错误的磁盘设备还可能导致设备的固态硬盘被擦除。

```
root@kali:~ dd if=kali-2.1.2-bbb.img of=/dev/sdb bs=512k
```

注意：这将擦除您 SD 卡上的所有内容。选择错误的磁盘设备还可能导致设备的固态硬盘被擦除。

`dd` 操作完成后，您可以在保持 SD 卡插入的情况下启动 BeagleBone Black。您可以使用用户名 ‘root’ 和密码 'toor' 登录 Kali 桌面。

注意：Kali Linux 的所有 ARM 镜像都预配置了相同的公钥。因此，建议在安装完成后尽快更改公钥。您可以使用以下命令进行操作。

```
root@kali:~ rm /etc/ssh/ssh_host_*
root@kali:~ dpkg-reconfigure openssh-server
root@kali:~ service ssh restart
```

## BeagleBone Black Kali Linux – 自定义构建

如果您是一个喜欢冒险并喜欢软件开发的人，并想要对 ODROID-XU3 的 Kali Linux 镜像进行一些自定义（例如更改内核配置），可以访问 https://gitlab.com/ilinux/build-scripts/kali-arm 查看适用于 ARM 设备的 Kali 脚本。使用的脚本是 `bbb.sh`。

## Kali Linux – HP Chromebook

HP Chromebook 是一款 ARM 设备，同样是一款超便携式笔记本电脑。为它制作 Kali 镜像是一项挑战，但最终实现了。HP Chromebook 具有以下配置：

- 1. 1.7 GHz 双核 Exynos 5250 处理器
- 2. 2GB 内存。

HP Chromebook 可以使用外部 SD 卡进行 Kali Linux 安装，使内部磁盘安全安全不受影响。

### Chromebook 上的 Kali – 用户说明

以下指令将帮助您在 Chromebook 上安装 Kali Linux。

- 1. 准备一个良好的快速 8 GB USB 闪盘来安装 Kali Linux。
- 2. 通过将 Chromebook 置于开发者模式启用 USB 启动。
- 3. 从 https://www.offensive-security.com/kali-linux-arm-images/ 下载适用于 HP Chromebook 的 Kali Linux ISO。
- 4. 现在您可以使用 `dd` 工具将此镜像写入 SD 卡。在我们展示的示例中，我们将把 Kali Linux 安装在路径为 `/dev/sdb` 的 SD 卡上。您可以根据自己的需求更改此。

> 注意：这将擦除您 SD 卡上的所有内容。选择错误的磁盘设备还可能导致设备的固态硬盘被擦除。

```
dd if=kali-chromebook.img of=/dev/sdb bs=512k
```

此过程可能需要一段时间，具体取决于您的设备速度和镜像大小。

完成 Kali Linux 安装所需的时间取决于 SD 卡的速度和 Kali Linux 镜像的大小。

`dd` 操作完成后，您可以在插入 USB 闪盘的情况下启动 HP Chromebook。当出现启动提示时，按下 CTRL+U 将进入 Kali。

### HP Chromebook 上的 Kali – 开发者指令

如果您是一个喜欢冒险并喜欢软件开发的人，并想要对 ODROID-XU3 的 Kali Linux 镜像进行一些自定义（例如更改内核配置），可以访问 https://github.com/ilinux/build-scripts/kali-arm 查看适用于 ARM 设备的 Kali 脚本。使用的脚本是 `chromebook-arm`。

## Kali Linux – CuBox

CuBox 是一款 ARM 设备，成本低，且由社区支持。价格实惠让它受欢迎。

可以使用外部 SD 卡为 CuBox 进行 Kali Linux 安装。

### CuBox 上的官方 Kali – 易用版

这些指令将帮助您在。

- 1. 准备一个快速的 8 GB SD 卡以在上面上安装 Kali Linux。
- 2. 从 https://www.offensive-security.com/kali-linux-arm-images/ 下载适用于 CuBox 的 Kali Linux ISO。
- 3. 现在您可以使用 `dd` 工具将此镜像写入 SD 卡。在我们展示的示例中，我们将把 Kali Linux 安装在路径为 `/dev/sdb` 的 SD 卡上。您可以根据自己的需求更改此。

注意：这将擦除您 SD 卡上的所有内容。选择错误的磁盘设备还可能导致设备的固态硬盘被擦除。

```
root@kali:~ dd if=kali-1.0.3-cubox.img of=/dev/sdb bs=512k
```

此过程可能需要一段时间，具体取决于您的设备速度和镜像大小。

完成 Kali Linux 安装所需的时间取决于 SD 卡的速度和 Kali Linux 镜像的大小。

`dd` 操作完成后，您可以在保持 SD 卡插入的情况下启动 CuBox。您可以使用用户名 ‘root’ 和密码 ‘toor’ 登录 Kali 桌面。

### CuBox 上的 Kali – 长版本

如果您是一个喜欢冒险并喜欢软件开发的人，并想要对三星 ARM Chromebook 2 的 Kali Linux 镜像进行一些自定义（例如更改内核配置），可以访问 https://gitlab.com/kalilinux/build-scripts/kali-arm 查看适用于 ARM 设备的 Kali 脚本。使用的脚本是 `cuboxsh`。

## Kali Linux – ODROID U2

ODROID U2 是一款 ARM 设备，硬件较为复杂。

### ODROID U2 上的 Kali – 用户说明

以下指令将帮助您在 ODROID U2 上安装 Kali Linux。

- 1. 准备一个快速的 8 GB微 SD 卡来安装 Kali Linux。我们推荐使用 Class10 类 SD 卡。
- 2. 从 https://www.offensive-security.com/kali-linux-arm-images/ 下载适用于 ODROID U2 的 Kali Linux ISO。
- 3. 现在您可以使用 `dd` 工具将此镜像写入 SD 卡。在我们展示的示例中，我们将把 Kali Linux 安装在路径为 `/dev/sdb` 的 SD 卡上。您可以根据自己的需求更改此。

注意：这将擦除您 SD 卡上的所有内容。选择错误的设备还可能导致设备的固态硬盘被擦除。

```
dd if=kali-$vers-odroid.img of=/dev/sdb bs=1M
```

此过程需要一些时间，取决于你的设备速度和镜像大小。

完成 Kali Linux 安装的时间取决于 SD 卡的速度和 Kali Linux 镜像的大小。

在 `dd` 操作完成后，你可以在保持 SD 卡插插入状态下启动 ODROID U2。你可以使用用户名 'root' 和密码 'toor' 登录 Kali 桌面。

### ODROID U2 上的 Kali Linux – 开发者指南

如果你是一个乐于冒险并喜欢钻研软件开发的人，并想要对 ODROID U2 的 Kali Linux 镜像进行一些自定义（例如更改内核配置），你可以访问 https://gitlab.com/kalilinux/build-scripts/kali-arm 查看适用于 ARM 设备的 Kali 脚本。应使用的脚本是 `odroid-u2.sh`。

## 第 6 章

## 安装故障排除

### Kali Linux 安装失败

Kali Linux 安装可能由于多种原因失败。ISO 文件下载不完整或损坏、目标系统磁盘空间不足等都是导致 Kali Linux 安装失败的某些原因。在本章中，你将学习遇到的常见错误以及如何进行故障排除。我们将介绍“红屏”错误，这种错误通常在 Kali Linux 安装失败时遇到，它是发生问题的指示。

红屏内容如下：
