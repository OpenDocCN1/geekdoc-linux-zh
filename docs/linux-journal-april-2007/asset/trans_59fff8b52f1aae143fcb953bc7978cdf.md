

你的四个选项，尽管措辞不同，但与你启动时看到的选项是一样的。如果你选择**交互式**（Interactive），系统会提示你备份的来源。在继续之前，值得注意的是，Mondo Rescue 背后的理念是提供当一切丢失时的灾难恢复手段，这就是为什么备份被创建为可启动的（磁带、CD 等）。如果遇到重大灾难，这棒极了，但如果只是小灾难呢，比如不小心删除了老板的邮件文件夹？你肯定不希望停用一个正在运行的生产系统，即使他邮件文件夹中唯一重要的信息只是一个足球博彩的统计数据。幸运的是，你可以交互式地将文件或文件夹恢复到一个正在运行的系统中。以下是操作方法。

在命令行中输入 `monderestore`。会出现一个基于 ncurses 的界面，询问你的启动盘、CD 或软盘。只需按回车键，你就会到达文件目录。

程序可能需要几秒钟时间提取文件目录，但很快你会看到一个从根目录开始的文件和文件夹列表。使用方向键，你可以上下导航列表。在这个屏幕的底部，有标记为 Less、More、Toggle、RegEx、Cancel 和 OK 的文本按钮（图 8）。要展开文件夹或目录，光标向右移动，移动到 More 按钮，然后按回车。要选择一个文件或文件夹进行恢复，光标再次向右移动到 Toggle 按钮，然后按回车。文件名左侧会出现一个星号。再次按回车键以取消选择。要继续在文件列表中搜索，光标向左移动经过 Less 按钮，你可以再次上下滚动列表。

在你问之前，我没有提到 RegEx 按钮的原因是，这仍然是一个正在开发中的功能，目前它实际上什么也不做。

一旦你选择了所有要恢复的内容，光标移动到 OK 按钮，然后按回车。会弹出一个警告，询问你是否对选择满意。按“是”以继续恢复。在下一个屏幕中，选择一个恢复路径。如果你想就地恢复（并将覆盖当前文件），接受默认值，即根目录。通常，你会希望将文件恢复到另一个位置，并在对其内容满意后将其移回原处。如果是这种情况，请输入另一个路径，然后按回车。下一个屏幕（图 9）标有“正在从存档恢复”，并提供了恢复过程的良好报告。

![](img/3c4d8a97b5d96c835281dc0dacbc8551_31_0.png)

![](img/3c4d8a97b5d96c835281dc0dacbc8551_31_1.png)

该对话框显示当前正在搜索的 tarball 包所在的磁盘、完成百分比以及在你所有文件恢复之前预计剩余的时间。就这样了。你至关重要的文件（丢失时它们都很重要）已经恢复了。

再一次，朋友们（mes amis），时钟显示确实该结束了。我相信你从这项工作中感到满意和放松。当 François 最后一次为你斟满酒杯时，我应该指出 Mondo Rescue 的开发正在进行中，并且有一个乐于助人且热情的用户基础，准备帮你解决可能遇到的任何问题。花一点时间访问支持页面，并加入 Mondo Rescue 站点上的邮件列表，你不仅会感到更轻松，还会因为知道你的数据可以被恢复而睡得很安稳。请举起你们的酒杯，朋友们，让我们都为彼此的健康干杯。祝酒（A votre santé）！祝好胃口（Bon appétit）！

Marcel Gagné 是一位居住在安大略省滑铁卢的获奖作家。他是 Addison-Wesley 出版的新书《Moving in Free Software》（全新版本）的作者，这是他第六本书。他还定期在电视上作为“呼叫帮助”（Call for Help）节目的 Linux 专家亮相。Marcel 也是一名飞行员，曾是前 40 名骰子玩家，撰写科幻小说和奇幻小说，并且养了一只凶萌的折纸霸王龙。你可以通过电子邮件 mgagne@56siam.com 与他联系。你可以在他的网站 www.marcelgagne.com 发现许多其他事情（包括很棒的 Wine 技巧）。

# 资源

- Mondo Rescue: [www.mondorescue.com](http://www.mondorescue.com)
- Marcel 的网站: [www.marcelgagne.com](http://www.marcelgagne.com)
- WFL-LUG，Marcel 的在线 Linux 用户组: [www.marcelgagne.com/wfltlugform.html](http://www.marcelgagne.com/wfltlugform.html)

## EmperorLinux

...Linux 与笔记本电脑的交汇点

![](img/3c4d8a97b5d96c835281dc0dacbc8551_32_0.png)

### 便携

自 1999 年以来，EmperorLinux 一直为大学、公司、政府实验室和个人 Linux 爱好者提供预装 Linux 系统的笔记本电脑。我们的笔记本电脑从全功能的超便携机型到桌面替代机型不等。所有系统均提供为期一年的 Linux 电话和电子邮件技术支持，并适用完整的制造商保修条款。

#### Toucan T60/T60ws

- Lenovo ThinkPad T60/T60ws
- 最高 15.4" WSXGA+ 分辨率 1680x1050
- ATI Mobility FireGL V5200
- 1833–2333 MHz Core 2 Duo
- 512 MB–4 GB 内存
- 60–120 GB 硬盘
- CDRW/DVD 或 DVD+RW
- 5.2–6 磅
- 10/100/1000 Mbps 以太网
- 802.11a/b/g (54Mbps) WiFi
- 起价 $1950

![](img/3c4d8a97b5d96c835281dc0dacbc8551_32_1.png)

### 强大

EmperorLinux 专门从事在由 IBM、Lenovo、Dell、Sony 和 Panasonic 制造的众多优质笔记本电脑上安装 Linux 的工作。我们将您选择的 Linux 发行版定制到您的笔记本电脑，并提供以下支持：以太网、无线、X-server、ACPI 电源管理、USB、EVDO、PCMCIA、FireWire、CD/DVD/CDRW、声音等。

#### Rhino D820/M90

- Dell Latitude D820/Precision M90
- 最高 17" WUXGA 分辨率 1920x1200
- nVidia Quadro FX 3500M 显卡
- 1667 – 2333 Mhz Core 2 Duo
- 512 MB–4 GB 内存
- 40–160 GB 硬盘
- CDRW/DVD 或 DVD+RW
- 6.3–8.6 磅
- 802.11a/b/g (54Mbps) WiFi
- ExpressCard/EVDO
- 起价 $1455

![](img/3c4d8a97b5d96c835281dc0dacbc8551_32_2.png)

### 独特

EmperorLinux 提供具有独特功能的 Linux 笔记本电脑。加固型的 Panasonic 笔记本电脑专为恶劣环境设计：跌落、振动、沙砾、雨水及其他极端情况。ThinkPad 平板电脑与其他笔记本电脑类似，具备 LCD 数字化仪，支持笔式输入，既可用作鼠标，也支持压感书写和屏幕绘图。

#### Raven X60 Tablet

- Lenovo ThinkPad X60 Tablet
- 12.1" SXGA+ 分辨率 1400x1050
- 1667–1833 MHz Core Duo
- 1–4 GB 内存
- 80–120 GB 硬盘
- 4 磅
- 笔/触控笔屏幕输入
- 动态屏幕旋转
- 手写识别
- 提供 X60s 笔记本电脑
- 起价 $2300

![](img/3c4d8a97b5d96c835281dc0dacbc8551_32_3.png)

www.EmperorLinux.com 1-888-651-6686

# 在 Apache 中显示图像目录

迈向基于 Web 的图像管理 Shell 脚本的第一步。

![](img/3c4d8a97b5d96c835281dc0dacbc8551_33_0.png)

DAVE TAYLOR

坦白说，由 Apache 和其他 Web 服务器生成的目录列表很糟糕。

大多数时候，我编写 shell 脚本是为了解决我认为的轻量级问题。是的，我承认，如果你需要预测天气、对 50,000 个数据点进行地理映射或创建一个在线购物车，shell 脚本可能不是最佳工具！

尽管如此，当我在日常工作中遇到简化问题的困难或机会时，我首先想到的工具就是 shell 脚本。对你们中的一些人来说，可能是 Perl 或一些花哨的 PHP 代码，但由于任何能在 Linux 命令行上输入命令的人都可以开始编写脚本，我必须说我仍然认为 shell 脚本是一个好的起点。

令人惊讶的是，在短短一段代码中能完成多少工作，这个月我分享了一个拼凑起来的脚本，旨在解决你 Web 服务器上的一个常见问题——一个巨大的“Images”目录。

## Apache 目录列表

坦白说，由 Apache 和其他 Web 服务器生成的目录列表很糟糕。它们基本上就是 `ls -l`，没有额外信息，没有预览，什么都没有。大多数时候这并不重要，因为你的网站大部分可能是无缝的，用户不会接触到后端。

但是，你收集网站上所有图像、图形和照片的那个目录很可能情况不同。无论它被称为“Images”、“Graphics”、“Photos”、“Art”还是别的什么，你的目录很可能和我的一样：拥有 1,400 个图形文件。

如果文件名具有高度助记性，基于文本的列表功能是有用的，但展示所有图像的缩略图及其名称，而不仅仅是文件大小和最后修改日期，岂不是很实用？

这就是这个脚本的作用，和所有实际作为 CGI 脚本运行的脚本一样，它必须首先立即推送适当的头部信息：

```sh
#!/bin/sh

echo "Content-type: text/html"
echo ""
```

既然头部信息已经处理完毕，其余的内容可以在循环中生成。事实上，脚本的初始骨架版本只是重复了你 Web 服务器中已有的文件列表功能：

```sh
for name in *
do
    echo "$name <br>"
done
```

当然，这个输出并不是很有趣。至少，你可以更改它使文件名可点击：

```html
echo "<a href=$name>$name</a><br>"
```

但即使那样也并不是特别有趣。让我们添加一些条件代码，使图像显示出来，而其他内容仅生成链接。不过，与其测试文件名，不如做点更有趣的事情，使用不为人知的命令 `file`。

当你遍历典型图像目录的内容时，你期望得到类似以下的输出：

```text
$ file *

aol-safety-menu.png:       PNG image data, 161 x 230, 8-bit/color RGB, non-interlaced
apple-ipod-enter-code.png: PNG image data, 268 x 202, 8-bit/color RGB, non-interlaced
archos-av700.png:          PNG image data, 567 x 294, 8-bit/color RGB, non-interlaced
empty.jpg:                 empty
hentai-manga-example.gif:  GIF image data, version 89a, 358 x 313
index.cgi:                 Bourne shell script, text executable
teenage1.jpg:              JPEG image data, JFIF standard 1.02, aspect ratio, 100 x 100
```

不错的命令，不是吗？它包括图像类型、尺寸、深度以及它能确定的其他特性。

最重要的是，请注意“XX image data”（XX 图像数据）在这些图像中一致出现，无论是 PNG、JPG 还是 GIF 图像。通过使用这一点，我们可以避免 JPG 与 JPEG、JPG 与 jpg、GIF 与 Gif 等所有麻烦。

现在，这个小循环看起来像这样：

```sh
for name in *
do
    if [ ! -z "$(file $name | grep 'image data')" ] ; then
        echo "$name <br>"
```

