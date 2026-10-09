
# VERIO
## 托管服务
## 基于拥有
## 血统的 Linux。

- **根权限访问：** 提供你所需要的控制权。
- **高级 FairShare 技术：** 更好的资源管理意味着更好的性能。
- **真正支持性的支持服务：** 由系统管理员提供的获奖支持服务。

### 发布 Verio Linux® VPS。

在 Verio，我们对开源有着长期的承诺，这可以追溯到我们源自 FreeBSD 的历史。如今，作为虚拟专用服务器（VPS）技术的先驱，以及由全球最大电信公司的财务资源支持的主机服务提供商，我们为 Linux 带来了额外的要素：可靠性。欲了解更多信息，请致电 1-877-837-4654 或访问 www.verio.com/linuxlineage。

正确的基础无可替代。

![](img/526fd434dcfcf1b461b94c24ea170f36_14_0.png)
![](img/526fd434dcfcf1b461b94c24ea170f36_14_1.png)

Verio 及 Verio 徽标是 Verio Inc. 在美国和其他国家的商标和/或服务商标。Linux® 是 Linus Torvalds 在美国和其他国家的注册商标。所有其他名称均为各自所有者的商标或注册商标。©2007 Verio Inc. 保留所有权利。

---

# [卷首语]

## 本期 LJ 致敬 John Backus

我撰写并提交了本月的“前沿阵地”专栏，该专栏侧重于本期的主题——计算机语言，特别是 FORTRAN，这是我最初学习的第一种计算机语言。虽然在我的专栏中我指出了学习机器语言和汇编语言的好处，但我诚实地认为，如果不是因为 FORTRAN，我当初不会进入编程领域。

2007 年 3 月 20 日，在我提交文章两周后，我收到了 John Backus 于 3 月 17 日去世的悲痛消息。John 是被人们誉为“FORTRAN 之父”的人，也是被归功于发明 Backus-Naur 形式（一种用于描述语言的语言）的两人之一。我向当地的 Linux 用户组发送了消息，在接下来的一周里，该消息反复出现在各种邮件列表中。

以今天的语言和计算机水平，人们很难了解（或者对于像我们这样年纪大的人来说，甚至很难记得）那些早期的日子。今天，我们视为理所当然的概念在当时既是革命性的，在构思上也十分困难。有人认为计算机永远无法用机器代码以外的任何语言进行编程，我确信 John 和他的团队遇到了远超其份额的怀疑者，但他们坚持不懈。他们在第一个成功的高级语言上的工作，由此衍生出更多人在更多语言上的众多成功。

因此，我请《Linux 杂志》将本期关于语言的期刊奉献给 John Backus：杰出的计算机科学家和人道主义者，1924–2007。

当我们为计算机科学的未来做出贡献时，希望有一天我们也能以我们的方式做出和他一样多的贡献。

—JON “MADDog” HALL

## 小巧精致

你肯定喜欢一款专门兼容 OGG 格式并吹嘘其 Linux 友好性的 MP3 播放器（文献称其为“Linux 内核 2.4.x”）。这也解释了为什么 TrekStor 的 VibeZ 播放器在 Linux 圈子中引起了不小的轰动。

优点：你可以将其作为普通 USB 存储设备加载。它支持播放 OGG（外加 MP3、WAV、FLAC 和 WMA）。它具有线路输入和麦克风录音功能、彩色显示屏、可充电的 USB 电池（含备用电池）、设备端文件删除功能、可调播放速度以及非常时尚的非 iPod 设计。它的大小像一块肥皂——4"×2"×.7"，四角高度圆润。而且，它轻得多——仅 2.5 盎司。

![](img/526fd434dcfcf1b461b94c24ea170f36_15_0.png)

缺点：存储空间不多。价格从约 200 美元起，容量范围从 8–15GB。

—DOC SEARLS

## 创意风暴

### 硬件 OEM 厂商学习 Linux，让 Dell 的荣耀公司受益

今年早些时候，Dell 创建了一个类似 Digg 的网站，名为 Dell | IdeaStorm（“你的想法主导之地”）。该网站的理念是让读者提交对公司的想法，然后由其他读者进行投票和评论。在标题标志旁边运行着提示语，例如“科技公司如何应对气候变化？”（位于“点击此处阅读 Dell 的观点”上方）。不用说，这打开了闸门，释放了 Linux 需求的洪流。

截至 2007 年 3 月 13 日中部时间上午 8 点，前十名票数如下：

1. 108,886 票：“预装 Linux | OpenSUSE | Fedora | OpenSUSE | 多启动”
2. 73,840 票：“预装 OpenOffice.org | 作为 MS Works 和 MS Office 的替代方案”
3. 54,300 票：“精简、快速的 Linux 机器”
4. 50,653 票：“预装 Firefox 作为默认浏览器”
5. 49,990 票：“不预装操作系统”
6. 51,048 票：“无额外软件选项”
7. 35,867 票：“为所有硬件提供 Linux 驱动程序”
8. 29,041 票：“Linux 2.6.16 就绪（贴纸）”
9. 20,288 票：“国家呼叫中心”
10. 17,376 票：“使用 LinuxBIOS 代替专有 BIOS”

一小时后，Dell 自行添加了两个帖子。在 IdeaStorm 页面上，它发布了“Linux——我们在倾听——现在告诉我们更多”。在 Direct2Dell.com 页面上，它添加了“Dell 扩展 Linux 选项”。两者都指向 www.dell.com/linuxsurvey 上的调查。该调查的标题也是“Linux 洞察：我们在倾听”。

因此，就有了上面的标题。

—DOC SEARLS

---

## PGI Unified Binary™

如今，PGI™ 编译器能够生成单个 PGI Unified Binary 可执行文件，该文件针对 Intel EM64T 和 AMD64 处理器进行了全面优化，既提供了单一 x64 平台的所有好处，又使您能够利用 Intel 和 AMD 的最新创新。PGI Fortran、C 和 C++ 编译器在 Linux 和 Windows 上提供世界级的性能和统一开发环境，作为集成多核软件开发展工具套件的一部分。访问 www.pgroup.com，看看为何结构分析、计算化学、计算流体动力学和汽车碰撞测试领域的领先独立软件供应商选择 PGI 编译器和工具来构建和优化其 64 位应用程序。

![](img/526fd434dcfcf1b461b94c24ea170f36_16_0.png)

**The Portland Group**™
www.pgroup.com ++ 01 (503) 682-2806

The Portland Group, Inc. 是 STMicroelectronics 旗下公司。PGI、The Portland Group、PGI Unified Binary 是 STMicroelectronics 的商标或注册商标。其他品牌名称为其各自所有者的财产。

---

# [卷首语]

## 谁想要什么？

Google 将其庞大的 Linux 服务器群用于有趣目的之一，可以在 **trends.google.com** 上找到。在这里，你可以查看和比较从 2003 年底至今某段时间内的关键词查询情况。

除了以图表显示趋势外，Google Trends 还显示查询来源的前十个地点。这带来了一些令人惊讶的结果。

看看你是否能将左侧的搜索词与右侧的前十大搜索查询地点匹配。

答案见第 81 页。

—DOC SEARLS

**搜索词：**
1. gnome
2. kde
3. linux
4. shell
5. hat
6. hackage
7. laptop
8. widget
9. driver
10. emacs
11. vi
12. weenie
13. redbat
14. oracle
15. asterisk
16. internet
17. net
18. majoromo
19. maddog
20. vulerability

**前十大搜索查询地点：**
A. 布拉格，捷克
B. 浦那，印度
C. 奥斯陆，挪威
D. 雅典，希腊
E. 华盛顿特区
F. 檀香山，夏威夷
G. 东京，日本
H. 拉霍亚圣玛格丽塔，加利福尼亚州
I. 旧金山，加利福尼亚州
J. 斯坦福，加利福尼亚州
K. 雅加达，印度尼西亚
L. 奥斯汀，得克萨斯州
M. 利马，秘鲁
N. 伦敦，英国
O. 胡志明市，越南
P. 京都，日本
Q. 班加罗尔，印度
R. 波哥大，哥伦比亚
S. 卢布尔雅那，斯洛文尼亚
T. 河内，越南

## 他们这样说

> 当然，问题在于生活是反公式化、反制度化的……生活不能被收缩包装、关进笼子、解剖、分析或占有。生活是自由的。
>
> —Christopher Locke，《The Cluetrain Manifesto》

> 我认为，一个充满匿名垄断者的世界是一个生活其中和在其中创造都很痛苦的世界。
>
> —Mike Taht，the-edge.blogspot.com/2007/02/keeping-copyright-accessible.html

> 幸好亨利·福特在马萨诸塞州沃尔瑟姆停下来学习自行车制造，而不是在 Hobson 先生的马厍里花时间去铲那些马的粪便。
>
> —Bob Frankston，来自一封电子邮件消息

> 在孤立状态下，我们的欲望超过我们的力量。在社会中，我们的力量超过我们的欲望。
>
> —Frederic Bastiat，引自 George Jacob Holyoake 的《合作的逻辑》（*The Logic of Co-operation*），合作印刷协会，1873 年，www.citizenblog.org/node/23
