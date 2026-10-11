
它具有良好的前瞻性，支持新型 DDR4 内存，并配备了强大的集成 Intel HD Graphics 530 GPU。在未安装独立显卡的情况下，Intel Core i7-6700K 在 Heaven 基准测试中达到了 79 fps 的平均帧率，最低帧率为 5.6 fps。相比之下，当安装 GTX 950 GPU 时，Heaven 基准测试的平均帧率为 39 fps，最低帧率为 20.4 fps。

我们还在《地铁：最后的曙光》（Metro Last Light）中测试了 GTX 950。这是一款画面要求极高且是首款在 Linux 平台上发售的 AAA 级第一人称射击游戏。在全 1080p 分辨率下，GTX 950 在大部分测试时间内保持在 50 fps 左右，提供了流畅的游戏体验。然而，我们发现当画面繁忙时帧率会突然降至 36 fps——尽管图形设置已设为最高。

如果您希望获得更稳定的帧率，可以降低部分图形细节，画质依然会很棒。这肯定比 Intel Core i7-6700K 上的集成显卡要好，后者在《地铁：最后的曙光》中仅达到 21 fps——而且当时游戏还在最低图形设置下运行。

## 安装 GPU
显然，如果您想玩画面要求高的大型游戏，独立显卡是您购物清单上的必备品。安装显卡相对简单。您只需关闭机器，打开侧板以接触主板。显卡插入主 PCIe 插槽 - 请参考主板手册（如果您不确定，也可以进行快速在线搜索，不过大多数主板都有清晰的标签）。

Alienware 是进入 Steam Box 业务的知名品牌之一。

组装 PC 的一大优点是，很难将某个部件插到错误的端口或插槽中——它们根本插不进去。PCIe 插槽一端有一个小杠杆，按下这些杠杆有助于在想要移除或更换显卡时将其弹出，因此在安装时您可能需要倾斜显卡，使卡上的小切口位于杠杆下方。您还必须确保 PC 机箱上有一个空隙，以便在安装显卡后能够接触到其端口。为了制造空隙，大多数机箱允许您拧下薄金属格栅以访问显卡端口。找到与即将安装显卡的 PCIe 插槽对齐的格栅，使用螺丝刀拧下固定它的螺丝——但请确保保留好这些螺丝。取下格栅盖板，然后将显卡插入 PCIe 插槽。现在使用之前保留的螺丝将显卡固定到位。许多显卡——尤其是更强大的那些——需要连接电脑电源（PSU），因此请检查显卡是否有一或两个 PCIe 六针和八针插座。您的电源应有一根带有匹配连接器的线缆。如果没有，显卡通常会附带 Molex 转接头，但我们建议如果您的电源没有这些接口则进行升级。现在您可以合上 PC，将显示器连接到显卡并开机。一切顺利的话，您的 PC 应该会启动并显示您正在运行的发行版的桌面环境。拥有最多 Linux 游戏资源的 Steam 运行在基于 Debian 的系统上，但官方仅支持使用 Unity、GNOME 或 KDE 桌面的 Ubuntu。我们曾在其他基于 Debian 的发行版、Mageia 和 Arch 上成功运行 Steam，但为了本文的简便性，我们使用的是最新版本的 Ubuntu。

由于 Linux 游戏玩家的不断增长，Canonical 和 Nvidia 已合作使显卡驱动的安装变得更容易。当加载 Ubuntu 时，您应该会看到一条弹出消息，提示“有限制驱动程序可用”。点击此消息，将打开一个窗口，列出您可以安装的一系列驱动程序。您的系统推荐的驱动程序将被高亮显示，但值得检查一些驱动程序，因为其中包含有关驱动是专有还是开源的信息。您也可以从终端安装驱动程序。打开终端并输入 `sudo ubuntu-drivers devices`。

这将为您提供一系列可能的驱动程序，例如对于 Nvidia 显卡，它可能列出：
- `driver : xserver-xorg-video-nouveau - distro free builtin`
- `driver : nvidia-304 - distro non-free`
- `driver : nvidia-331 - distro non-free recommended`

如果我们想安装 Nvidia 最新官方专有驱动——即 Ubuntu 推荐的驱动——则输入 `sudo apt-get install nvidia-331` 进行安装。您可能会注意到这不是 Nvidia 最前沿的专有驱动，但它很可能可以运行大多数独立游戏。对于画面要求更高的游戏，如 *《中土世界：魔多之影》*，您需要更新的驱动。过去，这意味着要么从 Nvidia 手动下载并安装驱动——这对于大多数新手来说可能意味着过多的 *Terminal*（终端）操作——要么添加并启用额外的软件源（repos）以保持更新。后一种选择过去意味着依赖第三方软件源（例如用于最新稳定版的 ppa:pasabuntu-x-swat/x-updates），但在一项令人兴奋且近期的进展中，Ubuntu 已建立了一个官方 PPA，专门供想要最新驱动的 Linux 游戏玩家使用。要获取它们，请使用以下命令添加并启用 PPA：
`$ sudo add-apt-repository ppa:graphics-drivers/ppa`
`sudo apt-get update`

要升级到或安装最新驱动，请使用 `sudo apt-get install nvidia-current`。如果您担心这些驱动会导致系统崩溃——新发布的 Nvidia 驱动通常可能出现初期问题——我们建议坚持使用 x-swat PPA。要回滚 PPA 所做的更改，请使用 `sudo ppa-purge ppa_name`。

如果您拥有 AMD 显卡并希望安装最新官方驱动，则可以下载并安装 AMD Catalyst 程序，它提供了一个易于使用的图形界面来安装最新驱动。如果您之前安装过 AMD 显卡，则需要通过打开终端并输入 `sudo aticonfig --uninstall` 来移除旧驱动。现在在终端中输入 `sudo /amd-driver-installer-x86.x86.x86_64.run`。在提到“amd-driver-installer-x86.x86.x86_64.run”的地方，您应该再次确认 AMD 网站上（[http://support.amd.com](http://support.amd.com)）针对您的显卡是否有更新的驱动。将会打开一个窗口供您完成安装。提个醒，在稍后更新内核之前，请记住先移除专有驱动。

## 游戏服务
现在您的 Linux 机器已准备好玩游戏，一个大问题是您可以从哪里获取游戏？Steam 是显而易见的选择，因为它拥有大量游戏，且类型和风格混合得相当不错。它还具有一些相当不错的功能，如跨平台游玩，因此您可以购买 Linux 游戏，如果该游戏与 Windows 或 Mac 兼容，您也可以在那些操作系统上玩它，而无需购买另一份副本。Steam 上的许多游戏还支持云存档，您可以将进度保存在一台机器上，切换到另一台机器并从中断处继续游玩。

要在 Ubuntu 中安装 Steam，您可以在软件中心中搜索它，或者打开终端并输入 `sudo apt-get update` 然后 `sudo apt-get install steam` 来安装 Steam。安装完成后，您需要登录或注册一个 Steam 账号。之后，通过 Steam 购买、下载和安装游戏就变得轻而易举了。

Good Old Games（GOG）是另一个现在支持 Linux 的优秀服务。虽然通过 Steam 购买并不那么直接，但它的 GoG Galaxy 应用程序借鉴了许多 Steam 客户端的元素（但目前不可用于 Linux，您必须使用启动器），但它也有自己的优点，例如它只销售无 DRM 的游戏，并保证游戏在受支持的平台上运行，否则退款。另外，正如您可能从名字猜到的，它最初专注于老游戏，将它们重新打包以在新硬件和操作系统上运行。当然，它也包含新游戏，您可以访问并下载 [www.gog.com](http://www.gog.com) 上的游戏。

我们通常也建议看看 Desura（[www.desura.com](http://www.desura.com)），它拥有许多 Linux 独立游戏——既包括免费的也包括付费的——但 Desura 的母公司已于六月申请破产。除了 Humble Bundle 提供协助（[www.humblebundle.com](http://www.humblebundle.com)），后者也是 Linux 游戏的另一个优质来源外，目前尚未有关于 Desura 未来的官方消息。该网站仍在运行，因此是否购买的抉择在于您。无论您决定使用哪个游戏服务，您现在都应该拥有一台完全准备好游玩最新最棒游戏的 Linux 机器。

## 趣味游戏

![](img/420a7272a6efa239082a35eeadd9bc1d_76_0.png)

Ubuntu 中的 **额外驱动**（Additional Drivers）系统使安装新的开源或专有图形驱动程序变得很简单。

![](img/420a7272a6efa239082a35eeadd9bc1d_76_1.png)

Nvidia **GTX 950** 是一款性价比极高的显卡，虽然如果您想要更强的性能，您需要多花一点钱。

![](img/420a7272a6efa239082a35eeadd9bc1d_76_2.png)

您需要注册一个免费的 Steam 账号才能登录该服务。

> 如果您想玩大型游戏，专用显卡是必买项。

### Steam 机器

Valve，即 Steam 平台背后的公司，一直承诺通过 Steam 机器颠覆我们在客厅玩游戏的方式。这些紧凑的游戏 PC 旨在取代游戏主机，如 Xbox One 和 PlayStation 4。运行 SteamOS（Valve 基于 Debian 的发行版）的首批可商业购买的主机应在十一月发售——希望届时您阅读本杂志时已可购买。Steam 机器由多种制造商生产，如 Asus 和 Alienware，并且形状和尺寸各异。这意味着如果您不想自己组装游戏机，应该能找到一款适合您需求——和预算——的产品。价格从 449 美元（约 292 英镑——大致相当于 PlayStation 4 的价格，但性能强大得多）到 4,999 美元（约 3,256 英镑）用于 Falcon Northwest 的 Tiki（带花岗岩底座）。您可以访问 Valve 自己的 Steam 网站 http://store.steampowered.com/ sale/steam_machines 了解有关 Steam 机器的更多信息并进行购买。如果您更喜欢使用控制器而非键盘和鼠标玩游戏，许多 USB 控制器在 Linux 和 SteamOS 上均可即插即用，甚至包括微软的 Xbox 360 控制器。Valve 还为其 Steam 控制器（40 美元）打造了独特的设备，据称该设备可以轻松控制通常使用鼠标和键盘操作的游戏手柄。

