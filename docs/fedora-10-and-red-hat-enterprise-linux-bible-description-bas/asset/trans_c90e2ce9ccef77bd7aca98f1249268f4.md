

## 第 7 章：在 Fedora 和 RHEL 29 中游戏

## 使用更多控制和动作

现在你已经对控制和动作有了些了解，游戏就可以开始向许多不同的方向发展。以下是接下来可能发生的一些以及你可以做的事情：

- 在完成之旅后，计算机也有机会进行游戏。在它玩的过程中，会向你报告动作。你可以对这些动作做出决定。选择游戏（Game）-> 消息选项（Message Options）。会出现消息选项窗口，其中列出了可能来自服务器的不同类型的消息，以及它们将如何呈现给你。
- 在探索过程中，你会遇到其他探险者，最终会遇到其他文明。通过在数字键盘上选择方向继续探索。
- 在定居者（Settler）完成道路后，一个一个地移动它。（当定居者可用时它会再次闪烁）点击回合（Turn）。
- 此时，你将看到一条消息，显示你的城市完成了战士（Warriors）的建造。建筑和单位完成后，你通常会查看发生了什么。点击与城市相关的消息，然后弹出城市（City）。出现城市窗口，显示你有了额外的人口。食物储备可能会出现，但新城市正在努力增加食物和贸易。你可能会看到一个额外的战士单位。
- 此时可能还会出现科学顾问（science advisory），让你选择城市的研发目标。点击更改（Change）并选择写作（Writing）作为你的新研究目标。你也可以也可以选择一个不同的长期目标。完成后点击。
- 如果你的战士现在正在闪烁，按 `s` 键为战士分配哨兵模式（sentry mode）。

到此时，你应该已经熟悉 Freecv 的一些动作了。要学习游戏的一些基本策略，请查看帮助（Help）-> 玩游戏（Playing）。

## 极限 Tuxracer

使用 Extreme Tuxracer（`yum install extremuxracer`），你引导企鹅（Linux 标志）尽可能快地沿着积雪的山坡下山。Extreme Tuxracer（`etracer` 命令或游戏（Games）-> Extreme Tuxracer）是 TuxRacer 的开源（GPL）版本，该游戏曾是免费的，但后来被 Sunfire Studios 制造成了商业游戏。

要在 Extreme Tuxracer 中前进，你需要在规定时间内完成课程，同时克服出现的任何障碍（收集鱱或谈判旗帜）。你移动到不同的课程并获得更高级别的奖杯。图 7-4 显示了 Extreme Tuxracer 的截图。

## 第二部分：使用 Fedora 和 RHEL

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_343_0.png)

图 7-4：让企鹅 Tux 跳下山。

## 商业 Linux 游戏

当 Loki Software, Inc. 在几年前关闭大门时，商业游戏的格局发生了变化。Loki 生产热门游戏的 Linux 端口，包括《神话 II》（Myth II）和《文明：力量之召唤》等，许多人希望它能帮助 Linux 成为首选游戏平台。今天，原生运行的商业游戏由 Loki Games Demo 和 id Software（在下一节介绍）的几款热门游戏领先。

尽管 Loki Software, Inc. 已经不存在，但某些 Loki Games 仍然可以在网上购买。虽然它们以原价的一小部分出售，但如果它们无法工作，你只能自顾其力，因为 Loki Software 不再支持它们了。如果 Loki 想在特定的 Loki Games 消失之前感受一下它，我将在本章稍后部分描述如何找到和打包 Loki Games。

在 Loki 灭亡后，TransGaming Technologies 一直致力于一种将热门游戏引入 Linux 的方法，该方法依赖于 WINE Cedega（以前称为 WineX）。在大多数情况下，而不是为热门游戏制作不同的端口（像 Loki 那样），TransGaming 通过调整 Cedega 以适应每个需要微调的游戏，使用户在 Linux 中运行现 Windows 游戏。但对于许多 Windows 玩家来说，性能还没有达到可接受的水平。

虽然自本书早期版本以来，Linux 游戏状态有所改善，但 Linux 仍然作为一个游戏平台正在兴起。Linux 拥有支持高级游戏的一些技术，但技术和开发者支持尚未真正到位。

## 第 7 章：在 Fedora 和 RHEL 297 中游戏

大多数玩家仍然保留一个 Windows 分区以支持他们的游戏习惯。根据顶尖游戏开发者的说法，有重大的障碍——技术和经济上的——阻碍了 Linux 游戏的开发。特别是 Linux 游戏市场规模相对较小，意味着克服技术问题的动力并不特别强。然而，这些限制并不是不可逾越的。正如你在本章后面将看到的，即使是硬核玩家也能成功使用 Linux。

## 在 Linux 中开始商业游戏

你如何开始 Linux 游戏取决于你对它的认真程度。如果你只是想玩几个游戏来打发时间，我已经描述了将 X Windows 游戏重定向到 Linux。如果你想玩更强大的商业游戏，你可以从以下选项中选择：

- **微软游戏 (Cedega 6.0)** —— 许多为 Windows 操作系统创建的最热门游戏将在 Linux 中运行。
- **独立 Linux 开发者** —— 有一些小公司正在为 Linux 开发游戏。
- **针对 Linux 的游戏 (id Software 及其他)** —— 某些热门游戏提供了 Linux 版本。

## 在 Linux 中玩商业游戏

要让你在 Linux 中玩商业游戏，你可以从 Linux Games（http://www.linuxgames.com）或 Linux  FAQ（http://iculus.org/linuxfaq）等网站开始运行商业游戏。在大多数情况下，你需要：

- 购买游戏的许可。

以下是一些在 Linux 上运行的商业游戏示例：

- **针对 Linux 的 Duke 3D (3D Realms)** —— 迪克回到地球面对外星人。访问 3D Realms 获取有关（http://www.3drealms.com）的官方信息。访问 http://iculus/duke3d 获取。
- **Unreal Tournament 2003 (Epic Games)** —— 未来的多人决斗，战士使用武器互相对抗。访问 Go（http://www.epicgames.com）或 Unreal Tournament 网站（http://www.unrealtnament.com）获取官方信息。
- **Unreal Tournament 2004 (Epic Games)** —— 为 2003 版本增加了新的地图、角色、车辆、武器和游戏模式。

