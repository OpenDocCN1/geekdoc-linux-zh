
# JCHEMPAINT LINUS 之声

通过选择“文件 | 另存为图像”绘制 PNG、BMP 或 SVG 图形。或者，你也可以通过选择“工具 | 创建 SMILES”输出绘图的 SMILES 字符串。这意味着你可以通过一个或多个服务（如 Inspiration [6]）携带表示的化学化合物。

JChemPaint 可以从“文件 (SDF)”格式导入结构 [7]，这是一种以 `.sdf` 结尾的常用文件格式，用于交换化学信息。此外，各种化合物还以 IUPAC 国际化学标识符（InChI）数字 [8] 显示，它是以字符串形式表示的分子（与 SMILES 不同），或者以抽象结构服务（CAS）编号 [9] 显示，这是由美国化学会在数据库中管理的每个分子的唯一标识符。这两种表示法都与 SMILES 竞争。

![](img/d241cea1a8a6d96778bcc3ba9ab74512_80_0.png)

## 结论

JChemPaint 的独特之处在于，在 Linux 上或通用的免费软件中，没有更好的替代品。某些常用格式允许你检索其他在线服务的绘图信息。但此程序仍处于开发的早期阶段。在我们的实验室中，我们无法绘制带有内部圆形的环。不过，这些结构以模板的形式可用。此外，由于未处理上述 JChemPaint 的错误，某些操作会导致糟糕的 Java 异常。JChemPaint 是一个非常有用的编辑器，可以创建化学化合物的吸引人的 2D 视图。

> 作者

Anjela Minosi 在 Fiverr 上以 pczenminosi 的昵名为你提供 IT 服务。她提供的服务包括清理、分析和数据视觉化。

## 信息

- [1] JChemPaint: https://jchempaint.github.io
- [2] VSEPR: https://en.wikipedia.org/wiki/VSEPR_
- [3] SMILES: https://en.wikipedia.org/wiki/Simplified_molecular_input_line_system
- [4] CML: https://en.wikipedia.org/wiki/Chemical_Markup_Language
- [5] MDL MOL: https://en.wikipedia.org/wiki/Chemical_table_file_Molfile
- [6] Molinspiration: https://www.molinspiration.com/cgi-bin/properties
- [7] SDF: https://file.info/extension/sdf
- [8] InChI: https://iupac.org/who-we-are/divisions/division-details/inchi/
- [9] CAS Registry Number: https://www.cas.org/support/documentation/chemical-substances/facts

图 7：在插入原子时，你可以让它们吸附到位置。这意味着它们会紧挨在一起

LINUX-MAGAZINE.COM | LINUXPROMAGAZINE.COM 第 265 期 2022年12月 81

# 通过特版书籍提升你的技能！

从我们的特版书籍库中了解 Shell、LibreOffice、Linux 等内容。

Linux Magazine 团队创建了一系列单本书籍，让你深入研究你感兴趣的话题。提供纸质或数字格式供选择。

查看完整库！

shop.linuxnewmedia.com

作者：ANA4220

![](img/d241cea1a8a6d96778bcc3ba9ab74512_82_0.png)

# Figma：易于设计

有些人聚在在一起。他们想要一些简单的东西来帮助他们反复迭代用户界面。他们尝试了 Figma，正因为它的绘图与它的社交功能（包括备注和白板）并存。原型设计与设计 BY 作者：GRAHAM MORRISON

在发誓会被 AI 生成的图像打动后，Graham 这个月一直在与 Stable Diffusion 搏斗，直到它就像某个神谕或真理的先知。

当 Adobe 宣布将以 200 亿美元收购 Figma（设计师的首选工具）时，最初是震惊，随后是冲去寻找替代品，这并不是一项简单的任务。坦率地说，有几个替代品。最强大的是 Pen，它是一个优秀的设计工具，但只能通过浏览器运行。这就是 Akira 派上用场的地方。Akira 是一个处于开发初期的开源 Linux 工具。还有许多工作需要完成，该项目明确指出不应在生产环境中使用。Akira 已经具备功能，并能够很好地支持可能来自新用户涌入的更多资源。界面会让人很熟悉。

JChemPaint 是一个非常实用的编辑器，可以创建化学化合物的吸引人的 2D 视图。

> 作者

Anjela Minosi 在 Fiverr 上以 pczenminosi 的昵名为你提供 IT 服务。她提供的服务包括清理、分析和数据视觉化。

# LINUX 图籍 FOSSPICKS

## 音频有声书

### audio-activator (音频激活器)

Amazon 的 Audio 平台主要是一个有声书的订阅和列表服务。尽管它来自 Amazon 且主要以订阅为主，但实际上非常好用。得益于它的图书业务，它有海量的库供选择，而且书籍的音频和旁白非常出色。Audio 与其他订阅服务的另一个区别在于，当你选择了一本书时，你将始终能够访问它。详细来说，无论你是否继续订阅，你都拥有这本有声书。如果你获得免费有声书的机会，这会特别有用。

在接受并选择书籍后，即使在取消订阅后你也可以访问这些书籍。正如你可能意识到的，有声书受到 DRM 的保护，在 Amazon 或网页门户之外将无法访问。这个 audio-activator 可以大有所帮助。

Audio 是一个命令行工具，旨在帮助你在不需要 Amazon 软件的情况下访问你的有声书。它不需要你的账户凭据，也不会泄露你的个人数据。这些数据可以用于解密 Audible 允许从其网页门户下载的 AAX 文件。当你运行脚本时，系统会要求输入 Amazon 用户名和密码。之后，你输入。Chrome 或 Chromium 将启动连接。Firefox 可以配合可选标志使用。当验证成功后，你将获得一个认证令牌。使用此令牌解密文件并将其流到你的音频系统或解密后的文件中。这是备份有声书的极佳方法，并让你可以在任何不支持的系统上播放它们。

使用 audio-activator 备份你的有声书，并在你喜欢的播放器上收听它们。

#### 项目网站

https://github.com/in/Audible-NG/audio-activator

## 查看器

### Chafa

它不仅缺少了传统的命令行，还缺少动画。不仅仅是闪烁的颜色或潜在的颜色，而是像桌面应用程序一样在屏幕上实际移动它们。考虑到基于文本界面的局限性（这是原本无法实现的），Chafa 成功地仅通过文本处理保持了简单性，而且它可以在你喜爱的终端中完美渲染显示你想要的任何图像。它通过将图像和动画转换为 ANSI X3 64 命令和 ANSI/Unicode 字符。生成的图像和动画分辨率比你对命令行的预期要高得多，在不需要切换回桌面的情况下查看文件确实非常有用。

最简单的情况下，Chafa 接受单个参数作为图像或动画文件的路径。这将与你的命令行一起作为输出。色彩还原将取决于你终端的能力，但默认为 24 位输出，并可以通过额外的参数轻松增强。还有其他选项可以帮你获得最佳效果，例如转换图像的字体大小，或者通过字体与图像的比例水平或垂直地拉伸或缩小图像。在这里，当然还有进一步的选项可以手动缩放图像，或让图像尽可能地使用空间。

Chafa 是 "character art facade"（字符艺术门面）的缩写，它可以在终端上显示静态图像和动画。当你只使用 Chafa 来帮助在命令行中查看图像时，你可能以你在桌面上期望的质量查看动画。如果你一天中大部分时间花在命令行界面上，那么这是一个必不可少的工具。

#### 项目网站

https://github.com/hjpanssonson/chafa

## 笔记

### FeatherNotes (羽毛笔记)

有很多笔记应用程序，但大多数都在尝试做一些不寻常的事情——无论是通过快捷键记笔记、在命令行中、通过小部件或通过手机 App 记录。FeatherNotes 有其独特之处，但它是一个很棒的笔记本。FeatherNotes 是一个基于 Qt 的管理器，具有丰富的编辑器、支持嵌入图像、卓越的搜索功能和隐私保护。主应用程序窗口打开非常像一个简单的管理器，左侧是层级视图，右侧是编辑器。你可以开始创建笔记……

# FOSSPICKS LINUX VOICE

## Steam 兼容性工具

### Luxtorpeda

Valve 的 Steam Deck 正在为 Linux 带来许多新用户，并重新定义了一些被忽视的旧项目。Luxtorpeda 就是其中之一。虽然它对于在 Steam Deck 上玩旧游戏的人来说非常有用，但 Luxtorpeda 也适用于任何在 PC 上通过 Steam 玩游戏的人。它自称为 Steam 生态外游戏和标题的“兼容性工具”。我们拥有所有的游戏，并希望将其整合到 Steam 中，使其成为一个简单的游戏启动场所，并帮助通过远程流传输或 Steam Link 此类游戏。这在 Steam Deck 上尤为重要，因为默认情况下只运行 Steam 客户端。添加额外的游戏需要大量的时间和研究。你需要在 Steam 页面中了解这些游戏是如何启动的，以及它们需要哪些工具，而 Luxtorpeda 通过配置工具来运行任何游戏，为你完成这一切。这些包括大多数旧版《雷神战士2》(Quake II)、《绝地骑士》(Jedi Knight)、《炼狱》(Hexen)、《上古卷轴》(Morrowind)、《毁灭战士》(Doom) 和《毁灭战士3》(Doom 3)。Luxtorpeda 会为你设置好，它将为所有游戏安装并配置 Linux 原生客户端，以获得最佳性能。

Luxtorpeda 是一个与 Box86 和 Roberta 都相关的项目，这两者在 Steam 内部为 DOS 和 ScummVM 集成提供了原生 Linux 支持，并从这些构建的游戏中流出。之后，你的 Steam 游戏只需要由 Luxtorpeda 配置，而不是使用默认的任何引擎。无论是在 Linux 桌面版还是 Steam Deck 上，Luxtorpeda 都会为你的游戏运行并创建最优的安装和配置，效果非常出色。

#### 项目网站

https://github.com/dreamer/luxtorpeda

## 类宝可梦游戏

### Pokete

原版《俄罗斯方块》的优点之一是它源自 DOS 甚至更早期的机器，可以在任何设备上运行。当经理没看你时，它是极佳的五分钟消遣。虽然我们的电脑现在强大了许多倍，但这种基于文本的简单性仍然不可比拟，这使得 Pokete 如此吸引人。正如你可能猜到的，这是一款松散基于收集宝可梦理念的游戏，但这使其非常适合在你执行必要的更新时，溜进 tmux 会话的背景中。你扮演 Pokete 训练师的角色，带着回合制、8 位音乐、小镇上的治愈中心和收集精神环游世界。Pokete 是在廉价休息时间里游玩的一场很棒冒险。

你可以进入战斗，使用物品栏中的物品，或使用你的 Pokete 卡组。所有选项对宝可梦收集者来说都是很熟悉的。在战斗期间，你可以切换并展示对手侧的特征。在 Pokete 之间移动并面对面地收集非常有趣，让你变得更强大以应对更多冒险。

## 使用 Heimer 思导图构建你的想法

### 绘制树节点

思维导图帮助你以清晰的树状结构组织思路。Heimer 可以帮助你绘制这些树。

**作者：TIM SCHÜRMANN**
