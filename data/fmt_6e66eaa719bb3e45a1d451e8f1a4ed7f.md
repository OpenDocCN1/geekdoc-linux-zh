
```sudo dd if=LibreELEC-Generic.x86_64-8.1.img of=/dev/sdX bs=4M status=progress```

- 2. 等待过程完成。这可能需要几分钟。

![](img/63f12be029370b8891d876ebe7b9f412_430_0.png)

> 这种接口只有`一种方式`可以正确插入，但它有四种插法。如果你是在放置好位置之后通过摸索来尝试插入，插错光纤缆的概率将增加到 75%，你还有可能损坏插头或插座的风险。插的时候眼睛看清楚！

![](img/63f12be029370b8891d876ebe7b9f412_430_1.png)

> 这就是光纤“toslink”接口的样子，我用它连接到我的放大器。你可以在过去20年内制造的任何接收机背面找到它，并选择立体声接收机。

## 第 3 ：设置 Asustor 迷你电脑

连接你的电视和网络：

- `HDMI 线：` 将其从迷你电脑连接到电视。
- `以太线：` 连接以太线以便它可以连接到你服务器的 ZFS 存储池。
- `光纤音频线：` 使用它将音频输出到你的立体声系统。确保你正确插入光纤线；它不像 USB-C 线，它只有一个方向可以插入，而它有四种可能的插入方式。这意味着当你盲目摸索插入时，只有 25% 的机会插对。这几率太低了。请注意插头和插座！
- `电源线：` 最后插上此线，因为 asustor flashstor 迷你电脑在连接电源后会自动启动。

## 开启机器后疯狂按 F2 进入 BIOS。

![](img/63f12be029370b8891d876ebe7b9f412_431_0.png)

![](img/63f12be029370b8891d876ebe7b9f412_431_1.png)

### 第 4 步：进入 LibreELEC 安装并进行安装

- 1. 将可启动的 USB 驱动器插入你的迷你电脑。
- 2. 重启系统，在机器启动后尽可能快速反复 `F2` 进入 BIOS/UEFI 设置。
- 3. 使用方向键并按回车进入 `boot`（启动）菜单。
- 4. 将 USB 驱动器设置为为主启动设备。
- 5. 在 BIOS 中，禁用干扰 Linux 安装的 TPM 和 `secure boot`（安全启动）选项。这与我们在指南早期在 Intel NUC 上安装 `pfSenseense` 的操作类似。
- 6. 保存更改并重启，LibreELEC 将从 USB 驱动器启动。按 `F10` 将退出 BIOS 并保存你的更改。

如果你在阅读这些说明后，通过将 LibreELEC 镜像写入你的操作系统而删除了整台电脑，恭喜你！你和我一样笨。几乎是。别再那样做了。

![](img/63f12be029370b8891d876ebe7b9f412_431_2.png)

![](img/63f12be029370b8891d876ebe7b9f412_432_0.png)

![](img/63f12be029370b8891d876ebe7b9f412_432_1.png)

![](img/63f12be029370b8891d876ebe7b9f412_432_2.png)

### 第 5 步：在 Asustor 上安装 LibreELEC

我们将删除所有 Asustor 的软件并将其替换。这个过程将少不到90 秒，并且

接下来，我们安装 LibreELEC，它仅足以运行 Kodi。

- 1. `启动并安装：` 按照提示将 LibreELEC 安装到内部 eMMC 上。
- 2. 选择你想要安装它的的驱动器，对于 Asustor Flashstor 来说，这将是 `/dev/mmcblk0` 设备。那是 ASUS 软件安装所在的内存；我们正在删除它以安装 LibreELEC & KODI。
- 3. 你完成了。就这样。在不到 90 秒内搞定——太棒了 :)

> 注意：如果你没有在 Asustor Flashstor 迷你电脑中安装任何新的 NVMe 驱动器，或者没有安装任何新的 NVMe 驱动器，那么应该只会显示一个设备供安装，那就是位于 `/dev/mmcblk0` 的内部 EMMC。如果你安装了新的 NVMe SSD，它们将以 `/dev/nvme1` 的形式显示，x 是数字。![](img/63f12be029370b8891d876ebe7b9f412_433_0.png)

![](img/63f12be029370b8891d876ebe7b9f412_433_1.png)

![](img/63f12be029370b8891d876ebe7b9f412_433_2.png)

![](img/63f12be029370b8891d876ebe7b9f412_433_3.png)

1. 点击侧侧的“电影”（Movies）或“电视节目”（TV shows）。
2. 点击“添加视频”（Add Videos）
3. 点击显示 <None> 的地方添加地址
4. 添加 Samba 共享：使用 IP 地址和共享路径来添加您的媒体内容。对于我们设置的服务器，您将按照以下方式访问 ZFS 池：

```
smb://192.168.5.2/archive
```

安全提示：在我的个人设置中，当我为用于客户端的媒体目录设置 Samba 时，我喜欢创建一个单独的只读用户，供观看电影、视频、电视等使用。

这样做的原因是，如果我使用的软件有一个删除按钮我不小心点到了，或者当我在看东西时我的猫走在我的键盘/遥控器上，或者软件有 Bug/故障等，我不会丢失我的媒体内容。这里是我自己 Samba 配置的一个示例：

```
[television]

comment = television shows

path = /dev/drive/television

browable = yes

read only = no

write list = louis, kodi

directory mask = 0775

force user = louis

force group = group

inherit permissions = yes

init acl = yes

mask acl = yes
```
