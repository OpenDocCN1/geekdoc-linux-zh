
> 继续按空格键循环切换服装，直到找到你想要录入的那件。这样一来，如果你发现某件衣服不太合适，可以再次录入该件。另外，如果你将文件添加到 `doll` 文件夹，只需在新的卡片上录入新衣服即可。

![](img/df9a01bf057d58c2401b5edabd6e8829_420_0.png)

最后，将每件衣服打印在纸上，并使用喷雾胶将其贴在每张卡片上。用透明塑料薄膜覆盖卡片，并用锋利的刀片修掉多余部分，将卡片正面朝放在切割垫上。我们的部分卡片如图 18–4 所示。

![](img/df9a01bf057d58c2401b5edabd6e8829_421_0.png)

图 18-4：

人偶衣服 RFID 卡片。

经 Imani Osman 许可复制

## 运行时间

现在是时候真的为人偶穿衣服了。实现此操作的程序位于列表 18–6。

### 列表 18-6：为人偶化妆

```python
#!/usr/bin/python3
# 由 Mike Cook 编写

from rc522rfid import rc522rfid
import pygame
import os

pygame.init() # 初始化图形界面

os.environ['SDL_VIDEO_WINDOW_POS'] = 'center'

pygame.display.set_caption("换装")
pygame.event.set_allowed([pygame.KEYDOWN,pygame.QUIT])
pygame.key.set_repeat(500, 80)

screenWidth = 240
screenHeight = 550
screen = pygame.display.set_mode([screenWidth, screenHeight], 0)
xPlot = [0]
yPlot = [0]
```

与本章中的其他项目一样，我们呈现的只是一个开头，通过简单的在文件夹中放置更多文件，就可以轻松地进行几乎无限制的扩展。就像“换装娃娃”（Dress Up Doll）项目一样，这里有两个程序：一个录入程序和一个播放程序。其思路是录制歌曲的片段，程序将这些片段组合成一首不断变化的歌曲。更重要的是，计算机永远不会忘记农场上的内容，而且每一段歌词都像第一次唱那样充满热情。（在现实生活中，你不能总是说你在唱着《老麦当农的农场》）孩子或父母自己应该至少录制一些样本。

## 制作声音样本

样本可以在笔记本电脑上录制，并通过 USB 闪盘移动到 Pi 上。不过，花一点精力，完全可以在 Pi 本身上完成整个过程。树莓派 Pi 可以录音，但它没有内置接口，因此你必须以 USB 声卡的形式提供一个。你可以以低于 10 美元（约 6 英镑）的价格购买一个，也可以 http://linux.org/RPI_VerifiedPeripherals USB_Sound_Cards 找到其他列表。

最好查看你所使用的特定卡的安装细节。插入并连接麦克风后，进入桌面菜单并选择“偏好”（Preferences）子菜单，然后选择“音频设备”（Audio Devices）。在之后的下拉菜单中选择你的 USB 声卡。

接下来，你需要一些软件来录音。到目前为止，此此工作的免费软件是 Audacity。要在你的 Pi 上安装它，进入终端并输入以下内容：

```
sudo apt-get update
sudo apt-get install audacity
```

Audacity 安装完成后，你就可以从桌面菜单下的“音频与视频”（Sound & Video）项找到它。屏幕如图 18-6 所示。

> 你也可以找到适用于 Macintosh 和 Windows 操作系统的 Audacity 版本。

Audacity 不仅可以录音，还可以进行编辑——甚至添加效果。它的控制就像录音机，有一个圆形的红色录制（Record）按钮和一个方形的停止（Stop）按钮。如果你从未用过它，先试玩一下：只需点击录制按钮说些什么（你会看到绘制出的波形），然后按下停止按钮，按下倒回（Rewind），再按下三角形的播放（Play）按钮。

![](img/df9a01bf057d58c2401b5edabd6e8829_426_0.png)

## Audacity

![](img/df9a01bf057d58c2401b5edabd6e8829_427_0.png)

图 18-6-Audacity。

每当你进行录制时，都需要“修剪”（top and tail）——也就是说删除开头和结尾的静音。在 Audacity 中，使用放大镜图标放大波形，然后拖过开头的静音部分将其高亮。然后只需按下键盘上的 Delete 键即可将其删除。对结尾的静音执行同样的操作。处理好之后，你需要确保样本的开始和结束在零线上（穿过显示波形的中间）。如果不是，你在播放时会听到咔哒声。为了确保它确实开始并结束在零线上，突出样本开头的一小段，从“效果”（Effects）菜单中选择“淡入”（Fade In）。对样本末尾执行相同的操作，但这次选择“淡出”（Fade Out）。最后，选择整个样本并从“效果”菜单中选择“标准化”（Normalize）。勾选前两个选项，点击确定。最后一步确保了所有样本具有相同的整体音量级。

要保存样本，你可以从主菜单选择 `File: Export Audio`（文件：导出音频），然后从右角的下拉菜单中选择 Ogg Vorbis File。输入带有 `.ogg` 扩展的文件名并选择保存。.ogg 格式是 Python 的原生声音格式，支持得最好。关闭 Audacity 窗口，不要管“保存更改”（Save Changes）选项。

所以，在了解如何制作样本后，你需要知道录制哪些样本。在你的工作 RFID 文件夹创建一个名为 `farmSounds` 的文件夹，然后在里面创建一个名为 `fixed` 的文件夹。你将在那里存储歌曲的骨架。

表 18-1 显示了你需要制作的声音样本。

## 表 18-1 老麦当农场的声音样本

| 样本名称 | 唱词 |
| :--- | :--- |
| start | "Old McDonald had a farm ee eye ee eye oh" |
| and | "and on this farm he had some" |
| ee_eye_oh | "ee eye ee eye oh" |
| witha | "with a" |
| here | "here" |
| anda | "and a" |
| there | "there" |
| herea | "here a" |
| therea | "there a" |
| everywhere | "everywhere a" |
| well | "well" |
| end | "Old McDonald had a farm ee eye-e-e, ee eye-e-e, o-o-o-h (and feel free to extend those few notes)" |

回到 `farmSounds` 文件夹，你使用的使用的每种动物需要两个样本。例如，如果你有一只鸡，你需要一个你唱单词“chickens”的样本，命名为 `chicken`，然后是另一个该动物叫声的样本，命名为 `chickenSound`。使用精确的命名非常重要，否则程序将无法工作。

![](img/df9a01bf057d58c2401b5edabd6e8829_428_0.png)

### 列表 18-7：（续）

```python
animalPictures = [pygame.image.load("farmPictures/" + 
    animalNames[i]).convert_alpha() for i in range(0,len(animalNames))]
farmBuilding = pygame.image.load("farmPictures/fixed/" + 
    "farm.png").convert_alpha()
farmFence = pygame.image.load("farmPictures/fixed/" + 
    "fence.png").convert_alpha()
xPlot = [[144,144,144,144,144] for i in range(0,len(animalNames))]
yPlot = [[200,200,200,200,200] for i in range(0,len(animalNames))]
currentType = 0 ; currentA = A
```
