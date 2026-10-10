

## 热门推荐

### AI 图像生成器
### Imaginer
版本：0.2.0
网页：https://imaginer.codeberg.page

如今，AI 图像生成风靡一时。使用 Imaginer，你可以借助图像生成 AI 算法的强大能力，直接在桌面上创作出富有艺术感的作品。

该软件在某些发行版的软件源中可用，但最好从 Flathub 获取与发行版无关的版本，命令为 `flatpak install flathub io.codeberg.Imaginer`。

该应用界面简洁直观。要调用 AI 大师的服务，请在提示词（Prompt）字段中输入关键词或文本提示，然后点击“想象”（Imagine）按钮。

应用会将提示词传递给 AI 图像生成服务，该服务施展“魔法”并生成一张图像。

你可以通过添加负向提示词来优化效果。这组额外的关键词会告知 AI 图像生成引擎哪些细节不再生成。例如，在负向提示词中输入“低质量”（low quality），以确保引擎只生成高质量的作品。

你还可以要求应用自动保存生成的图像，在“保存位置”（Save Location）部分指定保存路径。建议在生成图像前定义保存位置，因为该应用没有提供在图像生成后手动保存的机制。

Imaginer 的一大亮点是它不受限于单一的 AI 图像生成引擎。你可以从众多服务中进行选择，包括 Open AI、Stable Diffusion、Analog Diffusion、Anything、Portrait Plus、Nitro Diffusion、Open Journey 和 Waitfu Diffusion。

通过汉堡菜单进入“偏好设置”（Preferences），启用你想使用的服务。启用后，你可以从“提供商”（Providers）列表中选择该服务。

![](img/5cfcf2f4448dccdd1c5c2a2851544557_87_0.png)

> 可以将正向提示词和负向提示词视为图像生成的“宜”与“忌”。

### ASCII 图像
### Letterpress
版本：1.3.0
网页：https://gitlab.com/gregormi/Letterpress

ASCII 艺术已经褪去了往日的光泽，其流行度也不再像拨号上网和 BBS 时代那样（好吧，老朋友！——编辑注），但它仍然拥有粉丝。正如 ASCII 爱好者所记得的那样，生成 ASCII 图像曾耗费大量的时间和精力。Letterpress 让你重温那段辉煌岁月，且无需流汗，它可以将你的照片转换为 ASCII 图像。

该应用可在 Flathub 上获取，可通过 `flatpak install flathub io.gitlab.gregormi.ASCIIImages` 进行安装。安装后，你可以从发行版的应用菜单中运行它，或使用 `flatpak run io.gitlab.gregormi.ASCIIImages` 命令运行。

Letterpress 的动力来自 jp2a，这是一个 ASCII 转换引擎。你可以使用它将任何 JPEG 或 PNG 图像转换为 ASCII 艺术。

使用该应用非常简单。只需从你的电脑中加载任意照片到 Letterpress，可以通过“打开文件”（Open File）按钮浏览文件系统，或者直接将图像拖放到应用界面中。随后，Letterpress 施展“魔法”，在几秒钟内输出该图像的 ASCII 版本。

完成后，你可以从底部栏选择 ASCII 字符的宽度，然后将结果下载到 TXT 文件中。该应用还提供将其保存到剪贴板的选项，之后你可以将其粘贴到任何你想去的地方。

虽然使用该应用很简单，但要获得有意义的图像却要麻烦得多。Letterpress 如其宣传的那样工作，用 128 个 ASCII 字符之一替换原始图像中的像素。然而，根据源图像复杂度的不同，生成的 ASCII 图像并不总是清晰可辨。对于某些图像，增加图像宽度就能起到作用，使输出在视觉上更具吸引力。

![](img/5cfcf2f4448dccdd1c5c2a2851544557_87_1.png)

> 猜猜这是什么图片比赛！告诉我们你觉得它是什么，我们将发送给你我们的专属赞美！

### 国际象棋游戏
**cli-chess**
版本：1.0.0
网页：https://github.com/trevorbayless/cli-chess/

这款软件来自我们的一位读者，他开发了一款名为 cli-chess 的终端国际象棋游戏。该游戏围绕一个国际象棋引擎开发，支持离线玩不仅限于普通国际象棋，还支持多种 Lichess 变体，包括 Crazyhouse（疯狂象棋）、King of the Hill（高地王座）、Three-check（三将死）等。此外，你可以使用 cli-chess 在 Lichess.org 服务器上与其他玩家在线对战，并观看 Lichess TV 的直播。该游戏用 Python 编写，可以使用 Pip 包管理器通过 `pip install cli-chess` 安装。安装完成后，输入 `cli-chess` 即可开始游戏。你可以使用键盘导航菜单并选择你想玩的变体。做出选择后，按 F1 键开始游戏。默认情况下，游戏会发起与计算机的标准国际象棋对局。

进入游戏后，你不能用方向键或鼠标移动棋子。相反，你必须使用 SAN（标准代数记号法）或 LAN（长代数记号法）来走棋，例如 c6（兵到 G6）、Be2（象到 E2）或 Nxe7（马吃 E7 位置的棋子）。为帮助你走棋，游戏会在棋盘旁边标注坐标。

为了与其他玩家在线对战，你首先需要为你的 Lichess 账户创建一个 API 令牌，然后将其传递给游戏以帮助其与服务进行身份验证。启动你的浏览器并登录你的 Lichess 账户，然后按照项目网站上的链接生成供 cli-chess 身份验证使用的 Lichess API 令牌。最后，复制该令牌并通过 `cli-chess --token <your-token>` 传递给游戏。

![](img/5cfcf2f4448dccdd1c5c2a2851544557_88_0.png)

> 你可以增加终端字体大小，以便使棋盘显示得更大。

### 游乐园模拟器
**OpenRCT2**
版本：0.4.4
网页：https://openrct2.io

谁没想过拥有一个游乐园呢？使用 OpenRCT2，你就可以做到。游戏让你负责建造和维护你自己的公园。

你可以轻松地在任何 Linux 发行版上使用官方 AppImage 安装游戏，命令为 `flatpak install flathub io.openrct2.OpenRCT2`。

OpenRCT2 是《过山车大亨 2》（RollerCoaster Tycoon 2，简称 RCT2）的开源重制版本。它试图提供 RCT2 的所有内容，以及许多增强功能和附加特性。它还需要来自原版《过山车大亨 2》（ET 或 GoG）或《过山车大亨 经典版》的文件才能运行。

如果你拥有 GoG 版本的 RCT2，你必须安装 Innoextract 来从安装程序中提取内容。这可以在大多数发行版的官方软件源中找到，在 Fedora 上可通过 `sudo dnf install innoextract` 安装，在 Ubuntu 上可通过 `sudo apt install innoextract` 安装。创建一个文件夹用于存放提取的文件，并将 RCT2 安装程序可执行文件移入其中。使用 Innoextract 导出安装程序可执行文件的内容，例如 `innoextract setup_rollercoaster_tycoon2_2.0.0.6.exe`。当你启动 OpenRCT2 时，系统会询问 RCT2 安装位置，因此你应该指向提取文件夹中的内容。

![](img/5cfcf2f4448dccdd1c5c2a2851544557_88_1.png)

游戏内容包括建造和维护一个拥有游乐设施、商店和其他设施的游乐园。你的目标是合理布局，以娱乐游客并获利。

它允许两种类型的游戏玩法模式。在“情景”（Scenario）模式下，玩家必须在规定时间内完成特定挑战；而在“沙盒”（Sandbox）模式下，你拥有更大的灵活性，可以无限制地建造你的游乐园。

> OpenRCT2 并不难掌握，但对于没玩过 RCT2 的人来说，可能会显得有点具挑战性。

### CPU 控制器
### Boost Changer
版本：5.0.2
网页：https://github.com/nbebaw/boostchanger

Boost Changer 是一个简单的小工具，帮助你修改处理器频率。它最初仅适用于 Intel CPU，但最新版本也可以修改 AMD 处理器的频率。

它以与发行版无关的 AppImage 形式提供。你可以从官网获取最新发布版本，然后使用 `chmod` 命令赋予其可执行权限，例如 `chmod +x boostchanger-5.0.2.AppImage`。然后双击该 AppImage 或在终端中通过 `./boostchanger-5.0.2.AppImage` 启动它。

该应用界面简单。起始页面是一个仪表板，显示有关你安装环境的各种信息，如发行版名称、运行中的内核版本和正常运行时间，以及包括 CPU、内存、磁盘类型、大小和供应商在内的硬件详细信息。

真正的“魔法”发生在“CPU 设置”部分，你可以从左侧导航菜单切换到该部分。在这里，你可以从四个预定义的自解释模式中选择：节能（Power Save）、平衡（Balance）、性能（Performance）和极致（Ultra）。

![](img/5cfcf2f4448dccdd1c5c2a2851544557_89_0.png)

请注意，尽管该应用不需要 root 权限即可运行，但一旦你选择一个模式，就会弹出一个窗口要求输入超级用户密码。然后“能源性能”参数将更改以反映当前启用的模式。

开发者指出，Boost Changer 并非旨在替代 TLP 和 PowerTOP 等其他电池寿命优化工具。相反，该应用可以被视为一个图形前端，用于通过 sysfs 伪文件系统快速修改 CPU 时钟速度。还要注意，该应用目前仅适用于真实 CPU，不适用于虚拟硬件。

> 使用 Boost Changer 修改 CPU 时钟速度，以最大化性能或节省能源。

### PDF 编辑器
### PDF Mix Tool
版本：1.1.1
网页：https://scarpetta.eu/pdfmixtool/

如果你经常处理 PDF 文件，那么 PDF Mix Tool 是你工具箱里的一款实用工具。

该应用使你能对 PDF 文件执行常见的编辑操作，例如合并两个或多个 PDF 文件、更改 PDF 中页面的方向、从 PDF 中提取页面或图像，等等。

PDF Mix Tool 在大多数发行版的软件源中可用。使用 Debian 系发行版（如 Ubuntu）的用户可通过 `sudo apt install pdfmixtool` 获取，而使用 Fedora 及其衍生版的用户可使用 `sudo dnf install pdfmixtool` 安装该应用。如果你的发行版没有该应用的最新版本，你也可以从 Flathub 或 Snap Store 获取。

该应用界面相当直观。所有支持的操作都列在左侧栏。首先选择你感兴趣的操作。根据所选操作，你会在右侧面板中看到相关选项。例如，如果你选择“合并 PDF 文件”选项，应用会要求你指向你想合并的 PDF 文件。添加完所有你想合并的文件后，你可以使用“上移”和“下移”按钮重新排列它们的顺序。完成后，点击“生成 PDF”以创建新的合并 PDF。

![](img/5cfcf2f4448dccdd1c5c2a2851544557_89_1.png)

类似地，要从 PDF 中提取页面，请选择“提取页面”选项，指向相关的 PDF 文件，然后选择你要提取的页面。你可以将提取的页面保存为单独的 PDF 文件或单个 PDF。“删除页面”选项的操作方式相同，但它会移除指定的页面。

另一个有趣的选项是“页面布局”部分，你可以用它来更改 PDF 中页面的方向。[1]

> 除了编辑 PDF，你还可以使用该应用将 PDF 文件转换为小册子。

