
那些拥有非 Intel 时代的 Power Mac（例如带有 G3 和 G5 处理器的机器）的用户可能知道，之前的 Ubuntu 版本提供过 PowerPC 版本。遗憾的是，Ubuntu 7.0 Feity Dawn 不再是这样了。这意味着如果你是 Power Mac 用户，你将不得不使用用于 PowerPC 的非官方 Ubuntu 发布版（https://wiki.ubuntu.com/PowerPCdownloads/）。欲需更多信息，请查看 https://wiki.ubuntu.com/PowerPCFAQ/ 上的常见问题解答（FAQ）。
当然，如果你使用的是基于 Intel 的 Mac，你就走运了：书中附带的光盘将在你的 Mac 上运行。毕竟，i386 中的这个 i 代表的就是 Intel。

# 谈论 Ubuntu

值得注意的是，在处理 Ubuntu 时，你会接触到很多奇怪的短语，特别是在互联网上搜索信息时。我指的是一些看似不协调的短语，例如 Warty Warthog（顽皮野猪）、Gary Hedgehog（加里豪鼠）、Breezy Badger（微风鼬）、Dapper Drake（时髦鸭子）、Edgy Feisty（前卫挑剔）、Fawn（小鹿）、Gutsy Gibbon（勇敢长臂猿）、Hardy Heron（坚韧鹭鹤）、Intrepid Ice（勇敢冰）、Jasper Jalapako（贾斯珀辣椒）、Karma Kola（业力快乐）、Lucid Lynx（明晰猞猁）、Maverick Meerkat（特立猫鼬）、Natty Narwhal（自然海角）和 Oneric Ocel（梦幻猫猫）。这些是 Ubuntu 自 2004 年首次出现以来每个发布版本的独特名称。你需要记住重要的是当前的发布版本，即书中光盘上的版本：版本 12.04，被称为 Precise Pangolin（精确猴）。
你可能还会遇到其他几种 Ubuntu 主题变体。这些有 Kubuntu，一个基于 KDE 的 Ubuntu 版本；Edubuntu，一个专门为教室设计的 Ubuntu 特别版本；Xubuntu，基于 XFCE 桌面的轻量级 Ubuntu 版本；Lubuntu，另一个基于 LXDE 桌面环境的轻量级 Ubuntu 版本；Ubuntu Studio，一种旨在“创意人士”的 Ubuntu 新口味，它包含了一套强大的图形、视频和音乐应用程序。还有两个特殊版本：Mythuntu，专门为带有 MythTV 的家庭影院 PC 设计，以及 UbuntuTV，为创建基于电视的在线流和观看环境而设计。

# 我接下来该去哪里？

现在你对 Linux 和 Ubuntu 世界有了更多了解，并且手里拿着光盘，是时候开始行动了。如果你已经在你的机器上安装了 Ubuntu，只需翻到第 3 章即可。不过，如果你的机器还没有 Linux，是时候让它转转，看看你喜不喜欢它了。所以现在，跨上马鞍，系好马刺，直接进入下一章。是时候成为一名企鹅主义者了！

# 2

## 涉水与潜水

运行以及（如果你喜欢的话）安装 Ubuntu

![](img/d35fa962e6f9664d66dc83916f426418_48_0.png)

正如我提到的，Ubuntu 的巨大优点之一是它是以光刻 CD（live CD）的形式提供的，这意味着你可以在安装之前尝试它……或者如果你愿意，也可以完全不安装。更好的一点是，与 Ubuntu 的早期版本不同，如果你选择安装，你不需要额外的安装光盘——光刻 CD 和安装光盘二合一。而在“好、更好、最好”的范围内，最棒的一点是，从光刻 CD 安装实际上比你处理过的任何安装过程都要容易得多，而且它为你提供了多种处理方法。
在本章中，我将涵盖从光刻 CD 启动和运行 Ubuntu 的基础，然后假设你已经染上了 Linux 病毒，将介绍在硬盘上安装 Ubuntu 作为你操作系统的那些痛苦较少的步骤，既可以在传统的双启动设置中安装在硬盘的独立分区上（Windows 也有自己的分区），也可以对于冒险精神稍低的用户，从 Windows 系统内部进行安装。
如果你的电脑没有 CD 驱动器，不要担心，你仍然可以加入。请查看附录 A 了解如何从 USB 闪存盘运行或安装 Ubuntu。无论你最终如何操作，让我们把这本书用起来，让 Ubuntu 运行起来吧。

### 尝试下水

为了体验 Ubuntu 的核心内容

你可以直接将 Ubuntu 安装在 Windows 的 C 盘上，就像安装其他任何 Windows 程序一样。安装完成后，每当你启动机器时，你都可以从 Windows 启动加载程序选择启动 Windows 还是进入 Ubuntu。你的 Windows 系统将保持不变；你不需要对硬盘进行分区，而且以后出于任何原因你想卸载 Ubuntu，也可以像删除其他 Windows 应用程序一样进行操作。对于胆量不足的人来说，这是一个非常棒的方法。
诚然，这种方法可以被描述为一种半而求之的，因为它不能带给你像独立安装 Ubuntu 那样获得的完整体验。它没有完整的 Ubuntu 安装程序那么稳健，而且安装时间较长，因为 Wubi 需要从互联网下载安装文件（光盘中没有正确的文件）。但这是一个非常好的折中方案——它的运行实际上比 Ubuntu Live 光盘会话更快、更易用且更有趣。你还有一个额外的好处，即可以保存文件和设置，这意味着你可以跟随书中描述的任何操作。
如果这种替代性的安装方法对你没有吸引力，请跳转到第 17 页的“放手投入——在 Windows 之外安装 Ubuntu”。如果你已经下定主心并想了解一下这个 Wubi 安装器，请将浏览器指向 http://wubi.sourceforge.net/。另一方面，如果你已经决定 Wubi 安装器可以满足你的需求，这里是你需要执行的操作：
- 1. 在 Windows 运行期间，将带有此书的 Ubuntu Live 光盘插入电脑的驱动器。系统会自动弹出一个类似于图 2-2 中的窗口。
![](img/d35fa962e6f9664d66dc83916f426418_51_0.png)
图 2-2：在 Windows 内部自动启动的 Ubuntu Live 光盘
- 2. 在窗口中，点击“Install inside Windows”（在 Windows 内安装）按钮。Ubuntu 安装程序将会出现（图 2-3）。
![](img/d35fa962e6f9664d66dc83916f426418_52_0.png)
图 2-3：选择在 Windows 内安装 Ubuntu
- 1. 使用 **Installation drive**（安装驱动器）选项指定你想要放置 Ubuntu 文件的位置。确保该驱动器上有足够的空间！
2. Windows 和 Linux 不能共享同一个磁盘空间，因此你需要为 Ubuntu 专门留一些空间（稍后会讨论如何通过卸载 Ubuntu 轻松回收这些空间）。通过从 Installation size（安装大小）下拉列表中选择大小，来决定你想在 Ubuntu 中使用的可用磁盘空间。小于 10GB 的空间都可能受到限制。
3. 将 Desktop（桌面）环境设置为默认值（Ubuntu），然后选择用户名和密码。反复点击 Install（安装）按钮，直到你对选择感到满意。
4. 如果此时你的机器尚未连接到互联网，你会被要求连接网络。如果需要，请进行连接，如果出现警告窗口，请点击 **Retry**（重试）。
此时，Wubi 将开始下载它所需的文件，以便在你的 Windows 环境中创建一个可引导的 Ubuntu 安装。根据你的连接速度，这可能需要一些时间；需要下载大约 1GB（约 1000MB）的数据。
完成所有完成后，你将看到一个类似于图 2-4 的窗口，要求你重启。
5. 选择 **Reboot now**（立即重启）并点击窗口中的 **Finish**（完成）按钮，之后你的机器将重启。在重启之前，不要忘记从光驱驱动器中取出 Ubuntu 光盘；否则电脑将尝试从光盘启动。
6. 当机器重启时，你将看到 Windows 启动加载程序，一个带有白字的黑屏，它允许你决定启动 Windows 还是 Ubuntu。使用下方向键选择 **Ubuntu**，然后按 ENTER。
![](img/d35fa962e6f9664d66dc83916f426418_53_0.png)
图 2-4：Ubuntu 已完成其在 Windows 内安装的第一阶段。
你的机器将开始 Ubuntu 启动过程，这对你来说应该是全新的领域。一旦 Ubuntu 桌面出现，Ubuntu 将开始为你进行设置；这可能需要一些时间，取决于机器的速度。完成后，你将进入登录界面（图 2-5）；现在可以翻到第 3 章了，因为这里已经完成了。
![](img/d35fa962e6f9664d66dc83916f426418_53_1.png)
图 2-5：Ubuntu 登录界面
如果你决定不想在机器上保留 Ubuntu，可以通过进入 Windows 控制面板、选择“添加或删除程序”，然后选择删除来从 Windows 内部将其移除。

### 彻底的投入——在 Windows 之外安装 Ubuntu

如果你的机器上还没有安装 Windows，可以跳过本节。如果已经安装了，你就必须决定是否要保留它。
