
![](img/3c4d8a97b5d96c835281dc0dacbc8551_29_3.png)

![](img/3c4d8a97b5d96c835281dc0dacbc8551_30_0.png)

# 专栏

## 使用 LINUX 进行烹饪

PGI 统一二进制™

现在，`PGI™` 编译器可以生成单个 PGI 统一二进制可执行文件，该文件针对 `Intel EM64T` 和 `AMD64` 处理器进行了全面优化，在提供单一 x64 平台的所有优势的同时，使您能够利用 `Intel` 和 `AMD` 的最新创新。作为一套集成且支持多核的软件开发工具的一部分，`PGI Fortran`、`C` 和 `C++` 编译器在 `Linux` 和 `Windows` 之间提供世界级的性能和统一的开发环境。访问 [www.pgroup.com](http://www.pgroup.com) 看看为什么结构分析、计算化学、计算流体动力学和汽车碰撞测试领域领先的独立软件供应商选择 PGI 编译器工具和来构建和优化他们的 64 位应用程序。

![](img/3c4d8a97b5d96c835281dc0dacbc8551_30_1.png)

The Portland Group™

[www.pgroup.com](http://www.pgroup.com)  ++ 01 (503) 682-2806

`The Portland Group, Inc.` 是一家 `STMicroelectronics` 公司。`PGI`、`The Portland Group`、`PGI Unified Binary` 是 `STMicroelectronics` 的商标或注册商标。其他品牌和名称是其各自所有者的财产。

你的四个选项，尽管措辞不同，但与你启动时看到的选项是一样的。如果你选择交互式（`Interactive`），系统会提示你备份的来源。在继续之前，值得注意的是，`Mondo Rescue` 背后的理念是提供当一切丢失时的灾难恢复手段，这就是为什么备份被创建为可启动的（磁带、`CD` 等）。如果遇到重大灾难，这棒极了，但如果只是小灾难呢，比如不小心删除了老板的邮件文件夹？你肯定不希望停用一个正在运行的生产系统，即使他邮件文件夹中唯一重要的信息只是一个足球博彩的统计数据。幸运的是，你可以交互式地将文件或文件夹恢复到一个正在运行的系统中。以下是操作方法。

在命令行中输入 `monderestore`。会出现一个基于 `ncurses` 的界面，询问你的启动盘、`CD` 或软盘。只需按回车键，你就会到达文件目录。

程序可能需要几秒钟时间提取文件目录，但很快你会看到一个从根目录开始的文件和文件夹列表。使用方向键，你可以上下导航列表。在这个屏幕的底部，有标记为 `Less`、`More`、`Toggle`、`RegEx`、`Cancel` 和 `OK` 的文本按钮（图 8）。要展开文件夹或目录，光标向右移动，移动到 `More` 按钮，然后按回车。要选择一个文件或文件夹进行恢复，光标再次向右移动到 `Toggle` 按钮，然后按回车。文件名左侧会出现一个星号。再次按回车键以取消选择。要继续在文件列表中搜索，光标向左移动经过 `Less` 按钮，你可以再次上下滚动列表。

在你问之前，我没有提到 `RegEx` 按钮的原因是，这仍然是一个正在开发中的功能，目前它实际上什么也不做。

一旦你选择了所有要恢复的内容，光标移动到 `OK` 按钮，然后按回车。会弹出一个警告，询问你是否对选择满意。按“是”以继续恢复。在下一个屏幕中，选择一个恢复路径。如果你想就地恢复（并将覆盖当前文件），接受默认值，即根目录。通常，你会希望将文件恢复到另一个位置，并在对其内容满意后将其移回原处。如果是这种情况，请输入另一个路径，然后按回车。下一个屏幕（图 9）标有“正在从存档恢复”，并提供了恢复过程的良好报告。

![](img/3c4d8a97b5d96c835281dc0dacbc8551_31_0.png)

![](img/3c4d8a97b5d96c835281dc0dacbc8551_31_1.png)

该对话框显示当前正在搜索的 `tarball` 包所在的磁盘、完成百分比以及在你所有文件恢复之前预计剩余的时间。就这样了。你至关重要的文件（丢失时它们都很重要）已经恢复了。

再一次，朋友们（`mes amis`），时钟显示确实该结束了。我相信你从这项工作中感到满意和放松。当 `François` 最后一次为你斟满酒杯时，我应该指出 `Mondo Rescue` 的开发正在进行中，并且有一个乐于助人且热情的用户基础，准备帮你解决可能遇到的任何问题。花一点时间访问支持页面，并加入 `Mondo Rescue` 站点上的邮件列表，你不仅会感到更轻松，还会因为知道你的数据可以被恢复而睡得很安稳。请举起你们的酒杯，朋友们，让我们都为彼此的健康干杯。祝酒（`A votre santé`）！祝好胃口（`Bon appétit`）！

`Marcel Gagné` 是一位居住在安大略省滑铁卢的获奖作家。他是 `Addison-Wesley` 出版的新书《`Moving in Free Software`》（全新版本）的作者，这是他第六本书。他还定期在电视上作为“呼叫帮助”（`Call for Help`）节目的 `Linux` 专家亮相。`Marcel` 也是一名飞行员，曾是前 40 名骰子玩家，撰写科幻小说和奇幻小说，并且养了一只凶萌的折纸霸王龙。你可以通过电子邮件 `mgagne@56siam.com` 与他联系。你可以在他的网站 `www.marcelgagne.com` 发现许多其他事情（包括很棒的 `Wine` 技巧）。

### 资源

- `Mondo Rescue`: [www.mondorescue.com](http://www.mondorescue.com)

- `Marcel` 的网站: [www.marcelgagne.com](http://www.marcelgagne.com)

- `WFL-LUG`，`Marcel` 的在线 `Linux` 用户组: [www.marcelgagne.com/wfltlugform.html](http://www.marcelgagne.com/wfltlugform.html)

### `EmperorLinux`

...`Linux` 与笔记本电脑的交汇点

![](img/3c4d8a97b5d96c835281dc0dacbc8551_32_0.png)

#### 便携

自 1999 年以来，`EmperorLinux` 一直为大学、公司、政府实验室和个人 `Linux` 爱好者提供预装 `Linux` 系统的笔记本电脑。我们的笔记本电脑从全功能的超便携机型到桌面替代机型不等。所有系统均提供为期一年的 `Linux` 电话和电子邮件技术支持，并适用完整的制造商保修条款。

##### `Toucan T60/T60ws`

- `Lenovo ThinkPad T60/T60ws`

- 最高 15.4" WSXGA+ 分辨率 1680x1050

- `ATI Mobility FireGL V5200`

- 1833–2333 MHz `Core 2 Duo`

- 512 MB–4 GB 内存

- 60–120 GB 硬盘

- `CDRW/DVD` 或 `DVD+RW`

- 5.2–6 磅

- 10/100/1000 Mbps 以太网

- 802.11a/b/g (54Mbps) WiFi

- 起价 $1950

![](img/3c4d8a97b5d96c835281dc0dacbc8551_32_1.png)

#### 强大

`EmperorLinux` 专门从事在由 `IBM`、`Lenovo`、`Dell`、`Sony` 和 `Panasonic` 制造的众多优质笔记本电脑上安装 `Linux` 的工作。我们将您选择的 `Linux` 发行版定制到您的笔记本电脑，并提供以下支持：以太网、无线、`X-server`、`ACPI` 电源管理、`USB`、`EVDO`、`PCMCIA`、`FireWire`、`CD/DVD/CDRW`、声音等。

##### `Rhino D820/M90`

- `Dell Latitude D820/Precision M90`

- 最高 17" WUXGA 分辨率 1920x1200

- `nVidia Quadro FX 3500M` 显卡

- 1667 – 2333 Mhz `Core 2 Duo`

- 512 MB–4 GB 内存

- 40–160 GB 硬盘

- `CDRW/DVD` 或 `DVD+RW`

- 6.3–8.6 磅

- 802.11a/b/g (54Mbps) WiFi

- `ExpressCard/EVDO`

- 起价 $1455

![](img/3c4d8a97b5d96c835281dc0dacbc8551_32_2.png)

#### 独特

`EmperorLinux` 提供具有独特功能的 `Linux` 笔记本电脑。加固型的 `Panasonic` 笔记本电脑专为恶劣环境设计：跌落、振动、沙砾、雨水及其他极端情况。`ThinkPad` 平板电脑与其他笔记本电脑类似，具备 `LCD` 数字化仪，支持笔式输入，既可用作鼠标，也支持压感书写和屏幕绘图。

##### `Raven X60 Tablet`

- `Lenovo ThinkPad X60 Tablet`

- 12.1" SXGA+ 分辨率 1400x1050

- 1667–1833 MHz `Core Duo`

- 1–4 GB 内存
