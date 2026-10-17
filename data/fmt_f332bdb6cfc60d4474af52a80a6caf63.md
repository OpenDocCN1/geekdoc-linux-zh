
# 43. X Window 系统

## 43.6. 配置

### 启动与诊断

现在可以启动 `X` 了。对于 `XFree86` 版本 3.3，运行 `/usr/X11R6/bin/XFree86_VGA -cc 0`；对于 `XFree86` 版本 4，运行 `/usr/X11R6/bin/XFree86 -cc 0`。这两者都会打印出包含状态行的……确认你的 `25.175` 选择是否正确。这是速度（单位赫兹），取决于你的显卡，它是配置 16 色显示的唯一变量。你现在应该有一个工作的显示器。它的优点是始终有效。

### 43.6.2 即插即用操作

`XFree86` 版本 4 支持“即插即用”。只需运行 `/usr/X11R6/bin/XFree86 -configure` 即可生成 `XF86Config` 文件。你可以将此文件复制到 `/etc/X11/X86Config` 并立即启动 `X`。然而，得到的文件可能并非最优。详情请阅读。

### 43.6.3 正确的 X 配置

让 `X` 运行的一种简单可靠的方法是以下步骤（如果失败，则需要阅读上述文档）。还有一个名为 `Xconfig` 的工具提供了用户友好的界面。

- 备份你的 `/etc/X11/X86Config`。
- 在控制台运行 `SuperProbe`。它会使屏幕空白并输出你使用的是什么显卡。
- 运行 `xf86config`。通过所有选项进行猜测。你可以将显示器设置为 `31.5`, `35.5`；如果没有其他选项，垂直同步可以设置为 `50-90`。从数据库中选择（检查 `SuperProbe` 输出）——此时不要运行 `X`。
- `xf86config` 命令应该已经给你一个可以使用的 `/etc/X11/X86Config`。不需要再次运行它。你会注意到该部分被分为：

```
Section "<section-name>"
<config-line>
<config-line>
```

搜索 "Monitor" 部分。在稍后的位置你会看到许多这样的行：

```
640x480 @ 60 Hz, 31.5 kHz hsync
Modeline "640x480" 25.175 640 666 760 800 480 491 525
#800x600 @ 56 Hz, 35.5 kHz hsync
Modeline "800x600" 36 800 824 896 1024 600 601 603 625
#1024x768 @ 87 Hz interlaced, 35.5 kHz hsync
Modeline "1024x768" 44.9 1024 1048 1208 1264 768 784 817 Interlace
```

我们正在为不同的显示器和屏幕分辨率设置内容。选择一个太快的可能会坏旧显示器，并在屏幕上产生大量乱码。我们将消除上述三个以外的所有内容；我们可以通过用 `#` 注释它们或完全删除这些行来实现（你可能想先备份文件）。你可以让 `X` 来选择匹配显示器能力的正确 `Modeline`，但这并不总是有效。我喜欢显式选择一组 `Modelines`。如果你在 `XF86Config` 中没有找到模型，可以使用这个作为你的显示器：

| Key | Value |
| :--- | :--- |
| `Section` | `"Monitor"` |
| `Identifier` | `"My Monitor"` |
| `VendorName` | `"Unknown"` |
| `ModelName` | `"Unknown"` |
| `HorizSync` | `30-90` |
| `VertRefresh` | `50-90` |
| `Modeline` | `"*320x200"` `18` `400` `416` `512` `528` `592` `384` `388` `404` `-HSync` `-VSync` |
| `Modeline` | `"*400x300"` `20,160` `512` `528` `592` `640` `385` `301` `302` `Doublescan` |
| `Modeline` | `"*640x800"` `25,175` `640` `666` `760` `800` `480` `491` `525` |
| `Modeline` | `"*800x1000"` `31,500` `824` `896` `1024` `600` `601` `603` `625` |
| `Modeline` | `"1024x768"` `44.9` `1024` `1048` `1208` `1264` `768` `784` `817` `Interlace` |
| `EndSection` | |

分别禁用图形硬件加速、硬件光标支持和视频显存 pixmap 缓存。后者指的是使用显卡的未闲内存进行中间操作。如果你的显示器出现闪烁或伪影，你应该尝试这些选项。

7. 你的“Screen”（屏幕）部分应该正确排序“Monitor”（显示器）部分中指定的模式。它应该分别使用你的“Device”（设备）部分和单个“Monitor”部分，即“My Video Card”和“My Monitor”。注意 `XFree86` 3.3 版本不接受 `DefaultDepth` 选项。

| Key | Value |
| :--- | :--- |
| `Identifier` | `"My Screen"` |
| `Device` | `"My Video Card"` |
| `Monitor` | `"My Monitor"` |
| `DefaultDepth` | `16` |

```
Subsection "Display"
ViewPort 0 0
Virtual 1024 768
Depth 16
Modes "1024x768" "800x600" "640x480" "512x384" "400x300" "320x240"
EndSubsection "Display"

Subsection "Display"
ViewPort 0 0
Virtual 1024 768
Depth 24
Modes "1024x768" "800x600" "640x480" "512x384" "400x300" "320x240"
EndSubsection "Display"

Subsection "Display"
ViewPort 0 0
Virtual 1024 768
Depth 8
Modes "1024x768" "800x600" "640x480" "512x384" "400x300" "320x240"
EndSubsection "Display"
```

8. 此时，你需要运行 `X` 程序本身。对于 `XFree86` 3.3 版本，每个视频卡都有一个独立的包，以及一个编译了相应驱动程序代码的独立二进制文件。这些二进制文件的格式为 `/usr/X11R/bin/XF86-cardname`。对于 `Debian` 可以通过命令 `dpkg -l 'server-*'` 找到相关包，`RedHat` 6 使用 `rpm -qa | grep XFree*`（或 CD-ROM 中的 `RedHat/RPMS/XFree86-*`）。你可以运行它：

```
/usr/X11R/bin/XFree86-<card> -bpp 16
```

这会将显示深度设置为 `16`，即每个像素的比特数，这对应颜色数量。

## 43.7 视觉效果 (Visuals)

对于 `XFree86` 4 版本，卡支持被编译为独立的模块 `/usr/X11R6/lib/modules/drivers/cardname_drv.o`。单一可执行文件 `/usr/X11R6/bin/XFree86` 会根据“Device”部分中的 `Driver "cardname"` 行加载相应的模块。添加此内容后，你可以运行：

```
/usr/X11R6/bin/XFree86
```

其中深度由“Screen”部分中的 `DefaultDepth 16` 行设置。你可以通过用你的显卡名称 `grep` 模块来找到使用哪种驱动。这与我们在第 473 页处理内核模块的操作类似。

- 9. 一个好主意是创建一个脚本 `/etc/X11/X.sh`，其中包含你想要运行的服务器的 `-bpp` 选项。例如：

```
#!/bin/sh
exec /usr/X11R6/bin/<server> -bpp 16
```

- 10. 然后你可以将 `/usr/X11R6/bin/X` 软链接到此脚本。将 `/etc/X11/X` 链接到此脚本也是值得的，因为某些配置会在那里查找它。`X` 不应该可能除你想要的方式之外启动。通过在命令行运行 `X` 来双重检查。

`X` 引入了 `visual`（视觉效果）的概念。`visual` 是用于在屏幕上表示颜色的硬件方法。有两种常见类型和四种特殊类型：
