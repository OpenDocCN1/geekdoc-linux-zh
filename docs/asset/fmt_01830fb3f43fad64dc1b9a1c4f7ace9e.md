
`symlinks` [] 是一个用于清理绝对链接的工具，例如通过将绝对链接转换为相对链接并删除损坏链接。它有两个参数 `-r` 和 `-v`，分别告诉 `symlinks` 递归搜索目录并输出关于链接的详细信息。列表 7 显示了一个示例目录，它找到了一个被分类为损坏（“dangling”）的链接以及两个链接。在运行时，列表 1 和列表 3 之间没有显著区别。要仅过滤损坏链接，只需将 `symlinks` 与 `egrep` 结合（列表 8）。

基于 GUI 的 `Fslant` [] 工具基于 `find()` 命令行工具（位于 `find` 软件包中），与 `symlinks` 属于同一类别。如果你发现任何其他参数，它遵循当前链接并逐个打印匹配项。列表 9 显示了调用的结果，实际上与列表 2 和列表 8 的结果完全相同。仔细观察后，`findbnd` 的行为变得更加清晰：它是一个搜索链接的简单脚本。

我使用了 `readlink` [] 和 `chase` [] 工具作为 (`Shredder`, `rslant` 的图形化前端) 方法，它们在 `rslant` 网站上看起来很真实，但我无法 GNU/Linux 中实现它们。与 `Fslant` 类似，`rslant` 旨在发现并修复文件系统中条目的不一致之处，检测损坏链接。你可以在列表 10 的一行代码中完成操作。

`-w` 选项会告诉你结果；`bi` 是“broken links（损坏链接）”的缩写。`-o` 选项决定输出格式，`prept stat` 值为你提供特权显示。图 2 显示了一个包含 `relink` 的示例。

![](img/31162a00ee46c5d590c544cb2d944405_91_0.png)

图 2：示例的 `rslant` 结果。

```
dd@debian:~$ rmlink -T bl -o prept:stdt cod-software/
# Bad symlinks:
rm /home/cod-software-test/test2/v2/no-clue
rm /home/cod-software-test/broken/
```

# 教程 — 检测损坏链接

`modules os as Line` 第 1 行将它们导入到当前命名空间。第 3 行定义了一个名为 `walk()` 的函数，该函数遍历作为顶层参数传递的目录并检查其中的所有条目。在第 22 行调用了 `walk()`，在此之前评估了第 21 行作为参数传递的目录。

首先，程序创建搜索结果（第 4 行到第 7 行）。如果发生错误，`walk()` 函数在此处终止。然后，代码检查目录中的每个条目，以判断它是文件（第 11 行）、链接（第 13 行）还是目录（第 15 行）。该程序跳过文件。例如，`walk()` 函数被递归调用，再次以目录名作为参数。

然而，对于链接，来自第 16 行的 `readlink()` 函数会搜索目标。如果它是空的，则是一个损坏的链接，函数返回相应的错误消息。在检查完目录中的所有条目后，函数返回到调用点。如果你在目录树中运行脚本，你将看到包含列表 2 中两个条目的输出。

`relink` 检测到两个损坏的链接（它就是这样工作的）。`echo` 输出名称并显示链接目标。`chase` 还执行了一项令人兴奋的任务：追踪符号别名指向的文件，如果目标不存在，在情况下返回 1。列表 10 的第 2 行显示了对旧引用的调用，我们的结果是文件名。请记住符号链接可以跨越系统边界。你唯一的选择是检查文件系统中的每一个条目。

# 结论

在结构中可靠地检测损坏链接需要开销，但这是可以实现的。这里讨论的工具将帮助你轻松处理此问题：

## 避免错误

你如何从根本上防止损坏链接出现？坦率地说，这里的唯一建议是更加小心（此外没有一个存储所有链接的地方）。我没有知晓任何后台搜索来确保链接保持完好，你可能会无意中破坏链接。在删除文件之前，使用本文讨论的任何工具检查是否存在符号链接是有意义的。如果你只有对 `find` 和 `readlink` 的访问权限，请参考列表 11 所示的步骤。调用列出了这两个组件和链接目标 `-side`。为了做到这一点，`find` 使用了 `-ls` 选项。

## 列表 10：`rmlink` 和 `chase`

```
01 $ rmlink -T bl -o prept:stdout
02 $ chase old
03 /project/version
```

## 列表 11：`find` and `readlink`

```
$ find -type 1 -exec echo -n {} ';' -exec readlink {}
./project/version2/data/dataset3 -> project/version1/data/dataset3
./project/old -> project/version1
./project/current -> project/version2
+   1 tree: https://mama.instate.edu/users/tree/
2 symlinks: https://packages.debian.org/
3 Fslint: https://www.pixelbeat.org/fslint/
4 rmlink: https://rmlink.io/latest/
5 chase: https://packages.debian.org/bullseye
```

## 作者

Frank Hofmann 是一位柏林的开发者、培训师，是《Debian 包管理》(http://www.dpm.org/) 的合著者。

## FOSS LIFE

新闻 • 职业 • 生活 • 技能 • 资源 FOSSlife.org

## Linux NEWSSTAND

Linux 杂志是你的 Linux 世界指南。每月杂志都包含了在其他地方找不到的高级文章和教程。浏览我们的完整目录完成合集。

## 隐私

如果你真的重视隐私，你需要学习处理浏览器的跟踪。那些需要匿名的人依赖 Tor 网络 - 为监控国家提供安全浏览。我们还查看了 Portmaster，一个具有实用隐私功能的应用程序防火墙。

光盘：Ubuntu 22.04 和 Fedora Workstation 3

## 零信任

二十年前，每个人认为网关防火墙就是你保持安全的全部，但信任有一个不同的故事。今天，最好的建议是：不要信任任何人。你的内部网络可能和互联网一样危险。

光盘：Zorin OS 16.1 Core 和 Super GRUB2

## 清洁 IT

大多数人可以通过更换灯泡来节能，但你知道你可以通过更高效的软件来节能吗？本月我们研究了为 IT 行业带来可持续性的努力。

光盘：Manjaro 21.2 Qonos 和 DragonBSD 6.2.1

## 加密

本月，我们调查了 Linux 的加密状态。我们超越基础，探索支撑秘密系统的工具和技术——并向你展示如何确保你的加密是私密的。

光盘：Linux Mint 20.3 Cinnamon 和 deep 20.4

## 面部识别

生物识别最近因 Microsoft Hello 技术的到来而增强。我们看到开源世界正在追赶，有一项创新的工具叫做 Howdy。脸认证可能还没有为 CIA 准备好，但我们将帮助你开始使用 Howdy 并探索一眼认证的可能性。

光盘：antix 21 和 Haiku R1/Beta 3

## 破以完美

模糊测试：你是否好奇攻击者是如何发现导致程序崩溃并放弃控制权的“精心构造的输入字符串”的？我们为你介绍模糊测试的世界、模糊测试的艺术并探索一些领先的模糊测试技术。

光盘：Parrot OS 4.11 和 Fedora Workstation 35

## 特选活动

用户、开发者和供应商在全球各地的 Linux 活动中汇聚。《Linux 杂志》很荣幸向大家展示此处列出的特选活动。关于您附近的其他活动，请访问我们的在线详尽日历查看：https://www.linux-magazine.com/

如果您知道任何您希望我们加入日历的 Linux 活动，请将带有详细信息的邮件发送至 info@linux-magazine.com。

![](img/31162a00ee46c5d590c544cb2d944405_95_0.png)

## 通知

在预订任何行程之前，请务必检查网站，由于新冠（COVID-19）的影响，许多活动正在取消或转换为虚拟活动。

## 2022年存储开发者会议

**日期：** 2022年9月12-15日
**地点：** 加利福尼亚州，弗里蒙特
**网站：** https://storeddeveloper.org/

欢迎于9月12-15日加入我们在 SNIA 的 SDC21。紧跟最新技术可以节省大量的资金和时间。参加 SDC 是一种极具性价比的方式，可以通过教程、会议、主旨演讲以及参与同地插件活动的机会，获取许多不同领域的培训。请抓住这次机会，在同一地点向专家学习。

## 2022年布拉格 DrupalCon

**日期：** 2022年9月20-23日
**地点：** 捷克，布拉格
**网站：** https://events.drupal.org/prague2022

由 Drupal 协会提供的“Drupal 走进世界”，Drupal Europe 将于9月20-23日在布拉格举行。加入其中，推动 Drupal 项目的发展，并与其他成员建立联系。参与面对面的同行讨论、主旨演讲和会议。不要错过这次机会！

## 活动列表

- USENIX ATC '22 & OSDI '22 | 7月11-13日 | 加利福尼亚州，卡尔斯巴 | https://www.usenix.org/conference/
- 开源行业会议 | 7月19-20日 | 德国，柏林 | https://statconf.io/
- GUADEC 2022 | 7月20-25日 | 墨西哥，瓜达拉哈拉 | https://events.gnome.org/event/77/
- Icamping 柏林营-2022 | 7月21日 | 德国，柏林 | https://icamping.com/community/events/camping-berlin-2022/
- SCALE 19a | 7月28-31日 | 加利福尼亚州，洛杉矶 | https://www.calllinuxexpo.org/scale19a
- USENIX SECURITY '22 | 8月10-12日 | 马萨诸塞州，波士顿 | https://www.usenix.org/security22
- 伦敦开源峰会 | 8月23-24日 | 虚拟活动 | https://events.linuxfoundation.org/
- 拉美地区 | 9月7-8日 | 爱尔兰，都柏林 | https://odsc.com/apac/
- KVM 论坛 | 9月12-14日 | 爱尔兰，都柏林 + 虚拟 | https://events.linuxfoundation.org/
- 存储开发者会议 (SDC22) | 9月12-15日 | 加利福尼亚州，弗里蒙特 | https://storeddeveloper.developer/?source=LinuxMagazine&Event-Calendar
- 欧洲开源峰会 | 9月13-16日 | 爱尔兰，都柏林 + 虚拟 | https://events.linuxfoundation.org/
- 欧洲 Linux 安全峰会 | 9月15-18日 | 爱尔兰，都柏林 + 虚拟 | https://events.linuxfoundation.org/
- 布拉格 DrupalCon | 9月20-23日 | 捷克，布拉格 | https://events.drupal.org/
- 开源主机峰会 | 9月1-22日 | 宾夕法尼亚州，费城 | https://.com
- 2022 学院 | 10月1-7日 | 西班牙，巴塞罗那及 虚拟 | https://akademy.org/2022

## 征稿

我们正在寻找关于 Linux 和 Linux 环境工具的高质量文章。我们将考虑任何主题，但以下主题我们特别感兴趣：

- 系统管理
- 有用的技巧和工具
- 安全性，包括新闻和技术
- 产品评测，特别是来自实战经验
- 社区需求和项目

如果您有想法，请将带有长度预估、背景描述和联系信息的提案发送至 edit@linux-magazine.com。

文章的技术水平应与您平时在《Linux 杂志》上阅读的内容一致。请记住，《Linux 杂志》在许多国家阅读，您的文章可能会被翻译成我们姐妹出版物之一。因此，最好避免可能让所有读者无法理解的俚语和成语。

在提及未来的日期或事件时要小心。从您提交到最终稿件到达读者手中，可能会过去好几周。发送邮件或消息时，请在邮件主题行中使用特定的主题，帮助我们识别您的信息为文章提案。随时欢迎截图和其他支持材料。

更多信息请见：http://www.linux-magazine.com/

更多信息请见：http/31162a00ee46c5d590c544cb2d944405_99_0)

| 作者 | 页面 |
|---|---|
| Erik Casad | 16 |
| Jack Brown | 12 |
| Bruce Fieldfield | 24 |
| Mark Gomez | 67 |
| Marco Fisher | 26 |
| Jon Hoffman | 70 |
| Herman Met | 32 |
| Vincent Hill | 69 |
| Peter Miller | 54 |
| Graham Morrison | 78 |
| Daniel Schiff | 36 |
| Jane Wall | 84 |
| Amy Pettie | 48 |
| Audrey Walden | 68 |
| Rita Sooby | 20 |
| Jan Clark | 52 |
| Gwen Clark | 74 |
| Lori F | 62 |
| Sarah S | 90 |
| Julia K | 18 |
| Casad | 5 |
| Julia Kvasha, 123
| Editor.
4840 Parkway,
Lincoln, SK 68504
Publisher
Brian Gomez
Customer Service | Subscription
For USA and Canada:
sail@linux-magazine.com
(For Toll Free from the USA)
For other countries:
www.linux-magazine.com North America

## 下个月

26期

## 超越 5G

下个月我们将为您介绍开放无线接入网络 (`O-RAN`) 以及确保下一代 6G 移动技术的努力。![](img/31162a00ee46c5d590c544cb2d944405_97_0)

| 地区 | 日期 |
|---|---|
| 英国 / 欧洲 | 8月6日 |
| 美国 / 加拿大 | 9月2日 |
| 澳大利亚 | 10月3日 |

## 注意日期

请注意：销售日期为预计日期，可能会因物流问题延迟。

## 预览邮件

《Linux 杂志预览》是一封每月邮件，让您提前预览下期内容，包括文章链接。

注册：https://bit.ly/Linux-Update

图片 © Julia Kvasha, 123

## 像专家一样思考
## Linux Shell 手册 2022版

这个新版本包含了用于系统配置和排除故障的最重要工具。![](img/31162a00ee46c5d590c544cb2d944405_98_0.png)

- 以下是您将发现的部分内容：
- 定制 Bash
- 正则表达式
- systemd
- Bash 脚本
- 网络工具
- 以及更多！

在线购买：shop.linuxnewmedia.com/specials

## DrupalCon
PRAGUE2022
9月20-23

访问我们的网站 https://events.drupal.org/prague2022 获取更多信息。

![](img/31162a00ee46c5d590c544cb2d944405_99_0.png)

在为太晚之前忘记注册！

![](img/31162a00ee46c5d590c544cb2d944405_99_1.png)

查看
日程安排

我想成为 DrupalCon Prague 2022
志愿者

我想成为
赞助商

我有问题
drupal@kuonitumlare.com
