
Grip 窗口可用于播放支持 WAV 或 Ogg 文件的 CD。你可以使用显示底部的按钮来播放或暂停、跳进或后退、退出 CD。切换按钮让你缩小显示尺寸，从而节省桌面空间。点击切换器可以更改标题、艺术家和曲目信息。

## 使用 cdabelgen 创建 CD 标签

你可以使用 `cdabelgen` 命令创建标签并适应 CD 盒。你可以获取关于 CD 的信息，`cdabelgen` 会生成一个可以打印的 PostScript 文件。`cdabelgen` 包还带有图形（位于 `/usr/share/cdabelgen`），你可以将其整合到标签中。这里有一个 `cdabelgen` 命令的示例，它生成 PostScript 格式的 CD 标签（位于单行或使用反斜杠分成多行）：

```bash
$ cdabelgen -c "20th Century Collection" \
s "Jon Nexus" \
-i "Heart of Mine%20th Century Man%..." \
-o cover.ps
```

在这个示例中，`-c "20th Century Collection"` 识别 CD 的标题，`-s "Jon Nexus"` 指定艺术家。曲目在 `-i` 选项之后，每行由 % 分隔。输出文件发送到 `cover.ps`。使用 `-o` 选项查看并打印结果，使用 `env` 命令例如：

```bash
$ envie cover.ps
```

此示例的结果如图 4-7。你需要使用 `cdabelgen` 命令包含 CD 标签的标题和歌曲名称，并运行程序几次以获得正确的。当你准备好打印标签时，点击 Print All（全部打印）打印标签。

### 图 4-7
使用 `cdabelgen` 生成 CD 盒标签并使用 `evince` 打印它们。

![](img/8f71f83ce3d8e208bf71b5b6c9a753bd_138_0.png)

## 电视、视频和数字成像处理

### 获取电视卡。摄像头

第一个且可能是最大的技巧是获取一个 Linux 支持的电视卡或摄像头。当你从该设备获取视频输出后（通常从 `/dev/video0` 获取），你可以尝试一些应用程序开始使用。

## 第二部分：运行 Linux 桌面

第一个且可能是最大的技巧是获取一个 Linux 支持的电视卡或摄像头。当你从该设备获取视频输出后（通常从 `/dev/video0` 获取），你可以尝试一些应用程序开始使用。

（注：原文后续部分存在大量重复的 OCR 错误文本，已根据要求提取核心逻辑内容。）

## 第二部分：运行 Linux 桌面

## 获取支持的摄像头

与对电视采集卡的支持类似，摄像头的支持通过 Video4L2 接口提供的。如需检查你的摄像头是否受支持，请查看 `/src/linux*/ Documentation` 目录；`video4linux` 子目录中描述了一些并行端口摄像头；大多数支持的摄像头列列在 `usb` 目录中。

### 提示

经过研究，我购买了一台罗技 QuickCam Pro 3000。这款摄像头的驱动程序是为飞利 USB 摄像头制作的，但它适用于罗技（Logitech）、三星（Samsung）、创意实验室（Creative Labs）和 Askew 的摄像头。使用这些摄像头所需的 `pwc` 驱动在大多数 Linux 发行版中都可用。

支持的 USB 摄像头会自动检测，因此当你插上它们时，必要的模块会自动加载。启动 Ekika（在命令行输入 `ekiga`），你应该能在 Linux 桌面上看到来自 Ekika 的视频。

你可以通过正确执行以下命令来检查摄像头是否正常工作：

```
## lsmod
pwc 79588 0
videoev 30208 3 pwc,tuner,bttv
compat_ioctl32 59072 2 pwc,bttv
```
