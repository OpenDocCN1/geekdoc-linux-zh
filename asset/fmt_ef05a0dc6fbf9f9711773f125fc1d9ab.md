
4. 将 `Output` 更改为 `"Disk"`。

5. 点击 `Configure`。

6. 输入（或选择）一个目录进行写入。

7. 将 MP3 文件加载到 XMMS，将音量设置为 100% 并关闭 EQ。

8. 点击 `Play` —— XMMS 会显示播放，但听不到音乐。

9. 确保将 `Output` 改回以听 MP3。

在 `mpg123` 中写入 stdout：

1. 运行 `mpg123 -s audio01.wav`

XMMS 以 WAV 格式写入，而 `mpg123` 将 MP3 转换为原始 PCM 数据。两种格式都可以创建音频。如果你使用 WAV 文件，会在每个轨道开头注意到一个小标记。你可以使用 SoX（可以从 `audio/sox` 端口或包安装）简单地移除 WAV 文件的头：

```
% sox -t wav -r 44100 -w track.raw
```

关于使用刻录机的更多信息请阅读第 17.6 节。

## 7.4 视频播放

贡献：Ross Lippert。

视频播放是一个全新的、快速发展的领域。请耐心。在决定之前，你应该了解你的显卡型号以及它使用的芯片。虽然 Xorg 和 FreeBSD 支持各种显卡，但低端机器的性能较差。在 X11 运行时，使用你的命令 `xdpyinfo(1)` 获取支持的扩展列表：

### 7.4.1 确定能力

在 X11 下有几种显示视频的方法。真正有效很大取决于硬件。其次，X11 中的视频渲染是一个备受关注的话题，随着每个 Xorg 或 FreeBSD 版本，可能会有改进。

常见视频接口列表：

- X11：使用共享内存的普通 X11 输出。
- XVideo：支持任何 X11 drawable 的扩展。
- SDL：简单的多媒体层。
- DGA：图形访问。
- SVGAbi：低级控制台图形。

#### 7.4.1. XVideo

Xorg 和 FreeBSD 4.X 有一个 XVideo（也称为 Xvideo, xv）扩展，允许通过特殊加速直接在 drawable 对象中显示视频。此扩展在低端机器上提供了很好的播放效果。

要检查扩展是否正在运行，使用 `xvinfo`：

```
% xvinfo
如果结果如下，则你的卡支持 XVideo：
X-Video Extension version 2.2
screen #0
Adaptor #: "Savage Streams Engine"
number of ports: 1
port base: 43
operations supported: PutImage
supported visuals:
dep 16, visual 0x22
dep 16, visual 0x23
number of attributes: 5
"XV_COLORKEY" (range 0 to 16777215)
client attribute
client attribute (current value is 2110)
"XV_BRIGHTNESS" (range -128 to 127)
client attribute
client attribute (current value is 0)
"XV_CONTRAST" (range 0 to 255)
client attribute
client attribute (current value is 128)
"XV_SATURATION" (range 0 to 255)
client attribute
client attribute (current value is 128)
"XV_HUE" (range -180 to 180)
client attribute
client attribute (current value is 0)
maximum XVimage size: 1024 x 1024
Number of image formats: 7
id: 0x3555559 (YUY)
guid: 59555932-0000-8000-00aa038971
bits per pixel: 16
number of planes: 1
type: YUV (packed)
id: 0x5231569 (YV12)
guid: 59563132-0000-8000-00aa038971
bits per pixel: 12
```

在 FreeBSD 5.X 上，使用 `devfs(5)` 有一组略不同的推荐链接：

```
# ln -sf /dev/acd0 /dvd
# ln -sf /dev/acd0 /rdvd
```

注意，由于使用了 `devfs(5)`，手动创建的此类链接在重启系统后不会存在。为了在启动系统时自动创建符号链接，请向 `/etc/devfs.conf` 中添加以下行：

```
link acd0 dvd
link acd0 rdvd
```

此外，DVD 解密需要调用特殊的 ROM 函数，这需要设备的写入权限。所讨论的部分依赖于以下内核选项才能正确编译。在尝试编译之前：

```
options CPU_ENABLE_SSE
```

为了增强共享内存 X11 接口，建议增加某些 `sysctl(8)` 变量的值：

```
kern.ipc.shmmax=6710884
kern.ipc.shmall=32768
```

平面数: 3

类型: YUV (平面)

id: 0x0323449 (I420)

guid: 49343230-0000-0010-8000-aa00389b71

每像素比特: 12

平面数: 3

类型: YUV (平面)

id: 0x36315652 (RV16)

guid: 52563135-0000-0000-000000000000

每像素比特: 16

平面数: 1

类型: RGB (打包)

深度: 0

红、绿、蓝掩码: 0xf1, 0xe0, 0x7c0

id: 0x35531652 (RV15)

guid: 52563136-0000-0000-000000000000

每像素比特: 16

平面数: 1

类型: RGB (打包)

深度: 0

红、绿、蓝掩码: 0xf1, 0xe70, 0xf80

id: 0x31313259 (Y211)

guid: 59323131-0000-0010-8000-aa00389b71

每像素比特: 6

平面数: 3

类型: YUV (打包)

id: 0x0

guid: 00000000-0000-0000-000000000000

每像素比特: 0

平面数: 0

类型: (打包)

深度: 1

红、绿、蓝掩码: 0x0, 0x0, 0x0

另请请注意，列出的格式（YUV2、YUV12 等）并不在每个 XVideo 的实现中都存在，它们的缺失可能会阻碍播放器。

如果结果看起来如下：

+ - X-Video Extension version 2.2

screen #0

未发现的适配器

那么你的显卡可能不支持 XVideo。

如果你的显卡不支持 XVideo，这意味着你的显示器将更难满足渲染视频的计算需求。尽管如此，根据你的显卡和处理器，你可能仍然获得满意的体验。你应该在高级阅读部分的第 7.4.3 节阅读有关提高性能的方法。

## 第 7 章 多媒体

### 7.4.1.2 简单多媒体层

简单多媒体层（SDL）旨在作为 Microsoft Windows、BeOS 和 UNIX 之间的移植层，允许开发跨平台应用程序，并使其能够高效地利用音频和图形。SDL 层提供了对硬件的低级抽象，这种抽象有时比 X11 接口更高效。

可以在 `devel/sdl12` 找到 SDL。

### 7.4.1.3 直接图形访问

直接访问（Direct Access，DGA）是一个 X11 扩展，允许程序跳过 X 服务器直接修改帧缓冲区。由于它依赖于低级内存映射来实现这种共享，使用它的程序必须以 root 身份运行。

DGA 扩展可以通过 `dga(1)` 进行测试和基准测试。当 `dga` 运行时，每当按下键时它都会更改显示器的颜色。使用 `q` 退出。

### 7.4.2 处理视频的端口和包

本节讨论了 FreeBSD Ports 集合中可用于视频播放的软件。视频播放是软件开发非常活跃的领域，各种应用程序的能力很大程度上源于这里提供的描述。

首先，重要的是，许多运行在 FreeBSD 上的视频应用程序是作为 Linux 应用程序开发的。这些许多许多应用程序仍然处于 beta 质量。你在 FreeBSD 视频包上可能会遇到的一些问题包括：

- 1. 应用程序无法播放另一个应用程序产生的文件。
- 2. 应用程序无法播放自身产生的文件。
- 3. 在两台不同的机器上的同一个应用程序，在每台机器上重新编译后，播放同一个文件的方式不同。
- 4. 一个看似微不足道的过滤器（如缩放图像大小）会由于有错误的缩放程序导致糟糕的伪影。
- 5. 应用程序频繁转储（dump core）。
- 6. 文档未随端口一起安装，可以在网上或端口的工作目录下找到。
