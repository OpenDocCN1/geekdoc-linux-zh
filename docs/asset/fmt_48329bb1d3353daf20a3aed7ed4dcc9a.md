
> **警告**：运行 Return to Castle Wolfenstein 需要 NVIDIA 显卡。

图 7-5 是 Return to Castle Wolfenstein 在 Linux 中运行的屏幕截图。

![](img/b22364e57409c2481ba806e4e6b9309c_294_0.png)

## TransGaming 和 CedeGa 游戏

TransGaming Technologies (`www.transgaming.com`) 将当前在 Windows 平台上运行的一些最流行游戏带到 Linux。TransGaming 正在与 WINE 开发者合作开发 CedeGa，这使得你能够在 Linux 上运行许多最初为 Windows 开发的游戏。尽管 TransGaming 正在制作一些独立打包并针对 Linux 优化的游戏，但在大多数情况下，它向你出售的是 CedeGa 的订阅服务，而不是游戏本身。该订阅服务让你保持 CedeGa 持续开发的最新状态，从而能够运行越来越多的 Windows 游戏。

> **注意**：在运行 CedeGa 游戏之前，你可能需要从 `kernel.org` 获取一个原始内核并在系统上启动它。

为了让 Windows 游戏在 Linux 上运行，CedeGa 特别需要开发许多当今游戏所要求的 Microsoft DirectX 功能。此外，还必须克服与 CD 密钥和 Windows 操作系统钩子（`hook`）相关的问题（例如要求 Microsoft Active Desktop）。事实上，CedeGa 订阅的价值部分在于它让你可以投票决定希望 TransGaming 下一步开发哪些游戏。

TransGaming 支持的游戏完整列表，以及它们的流行程度和运行状况的说明，可以在 TransGaming 网站上获取（访问 `www.transgaming.com` 并点击 Games 来查找你感兴趣的游戏）。目前列出的游戏中有超过 100 款被评为 5 分中的 4 分（意味着游戏运行良好，即使不完美）。有七款游戏被评为 5 分（意味着它们运行完美）。

> **注意**：你可以使用 TransGaming 的 CedeGa 软件直接运行 Doom 3。要了解其他产品里程碑的新闻，请访问 TransGaming 主页上的 "Hot off the Press" 链接。

关于 Cedega 4.1 对新游戏的支持及增强功能，请参见发布说明：`http://download.transgaming.com/files/cedega-4.1_releasenotes.txt`。以下是 TransGaming 社区正在使用并据称在 Cedega 中运行良好（评分为 4 或 5）的一些新游戏和热门游戏列表。建议您自行查阅 TransGaming 的列表以了解新增内容和变更：

- 詹姆斯·邦德 007：夜火 (`James Bond 007: NightFire`)
- 创战纪 2.0 (`Tron 2.0`)
- 毁灭公爵 3 (`Doom 3`)
- 魔域豪侠 III (`Warlords Battlecry III`)
- 杀手合约 (`Hitman Contracts`)
- 无尽的任务 2 (`Everquest 2`)
- 铁血联盟 2：野火 (`Jagged Alliance 2: Wildfire`)
- 星际争霸：母巢之战 (`Star Craft: Brood War`)
- 孤岛惊魂 (`Far Cry`)
- 魔兽世界 (`World of Warcraft`)

TransGaming 的网站并非获取关于哪些游戏在 Cedega 4.0.1 下运行良好的信息的唯一途径。Extreme Tech (`www.extremetech.com`) 发现以下游戏在使用 Cedega 4.0.1 时于 Fedora 上也能运行良好：

- 虚幻竞技场 2004 (`Unreal Tournament 2004`)。存在一些显示残留问题，但可以游玩。
- 假面老虎机 (`Masque Slots`)
- 魔兽争霸 3 演示版 (`WarCraft 3 Demo`)

如果您心中有特定的游戏，请搜索游戏标题加上 Cedega 关键词，以开始寻找可行的配置。即使没有官方支持，也有许多热衷于特定游戏的用户为特定游戏开发了解决方案和补丁。

在 Cedega 4.0.1 中，TransGaming 增加了几个新的 Point2Play 功能。Point2Play 提供了一个图形窗口，用于在您的计算机上安装、配置和测试 Cedega。它还允许您安装和组织游戏，以便您可以通过图形界面启动它们。图 7-6 展示了 TransGaming Point2Play 窗口的示例：

![](img/b22364e57409c2481ba806e4e6b9309c_296_0.png)

图 7-6：使用 Point2Play 窗口检查计算机硬件以用于 Cedega 游戏。

新 Point2Play 窗口的其他功能包括能够从已安装的不同版本 Cedega 中进行选择以运行应用程序，以及单独配置每个游戏如何在 Cedega 下运行的工具。（如果游戏无法从图形用户界面运行，请尝试在终端窗口中启动它。）

要获取 Cedega 和 Point2Play 的二进制副本（即已经编译好可直接运行的版本），您需要订阅 TransGaming。有关如何成为“TransGamer”的详细信息，请单击 TransGaming 主页 (`www.transgaming.com`) 上的“Subscribe Here”链接。目前的福利包括：

- 下载最新版 Cedega。
- 访问 Cedega 支持论坛。
- 投票决定您希望 TransGaming 接下来支持的游戏。
- 订阅 Cedega 新闻通讯。

Cedega 以前被称为 WineX。如果您想构建自己的 WineX/Cedega 包，WineX 的源代码可能在不久的将来可用。要检查可用性，请尝试访问 WineX 的 SourceForge.net 项目站点 (`sourceforge.net/projects/winx`)。

### Loki Software 游戏演示版

为了鼓励人们了解其游戏，Loki 提供了一个演示程序，允许您从十几款 Loki 游戏中选择下载并试用。Loki 还提供其商业游戏的盒装套装供购买。虽然 Loki Software, Inc. 已不再经营，您仍能找到其一些游戏出售。例如，最近一次在 Amazon.com 上搜索 Loki，发现了 16 款不同的 Loki 游戏（包括此处描述的那些），其中许多售价仅为 9.99 美元。

> **警告：** 如果您尝试下载下一节中描述的任何演示版，请确保您有大量的可用磁盘空间和快速的网络连接。这些演示版中的一个通常需要数百兆字节的磁盘空间是很常见的。

用于下载演示版的 `Loki Demo Launcher` 仍然可以从 `演示版启动器页面`（`www.lokigames.com/products/demos.php`）获取。在该页面上，有链接指向您可以下载演示版启动器的 FTP 站点。您需要保存的文件是 `loki_demos-full-1.0e-x86.run`。将其保存到一个目录（例如 `/tmp/loki`），并执行以下操作：

1. 切换到您下载演示版的目录。例如：

```
# cd /tmp/loki
```

> **注意：** 您可能不需要 root 用户权限来安装这些游戏。但是，演示版启动器默认尝试写入的默认路径仅 root 用户可访问。

2. 以 root 用户身份运行以下命令（如果程序已更新，其名称可能有所不同）：

```
# sh loki_demos-full-1.0e-x86.run
```

如果您以前未使用过演示版启动器，将出现一个屏幕，要求您指定用于放置安装工具的路径。

3. 如果显示的默认位置对您来说没问题，请单击 **开始安装**（Begin Install）。

假设在写入安装目录时没有遇到问题，您应该看到一条安装完成消息。

4. 单击 **退出**（Exit）。接下来，您应该看到 **卸载工具**（Uninstall Tool）窗口。

5. 如果用于存放卸载工具的路径没问题，请单击 **开始安装**。将出现安装完成消息。

6. 单击 **退出**。出现的窗口允许您设置安装演示版包的位置。

7. 如果路径没问题，请单击 **开始安装**。

接下来，您应该看到一个显示可用不同演示版游戏的方框。当您将光标移动到每个游戏上时，会显示该游戏的磁盘空间需求。单击您想要安装的游戏，然后单击继续。将出现一个窗口，显示每个下载的进度。

8. 您可能需要单击“更新”按钮以完成更新，并单击“完成”以结束操作。现在演示版应该准备就绪，可以启动了。

9. 要么单击“播放”（Play），要么在终端窗口中输入 `loki_demos` 来启动程序。

10. 选择开始游戏，您就准备好了。

以下几节描述了一些可能仍然可用的游戏。再次强调，这些游戏可能不会可用太长时间。

#### 文明：权力召唤 (Civilization: Call to Power)
