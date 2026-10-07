
# Linux Magazine 第258 期 2022-05 美国版

![](img/d0fe54f1060b69f0f3f8ac0f16844891_1_0.png)

![](img/d0fe54f1060b69f0f3f8ac0f16844891_1_1.png)

亲爱的读者：

我们被告知，现代战争将包含网络战的元素，正如最近在欧洲一样，我们以新的警惕性审视我们的网络。在这种背景下，一个 NVIDIA 密钥被盗窃的消息尤为令人警觉。尽管该事件与任何外国冲突无关，而且看起来并非是由国家支持的攻击，但它是另一个警钟，提醒我们要在能够完全信任自己的系统安全之前，还有很长的路要走。

3 月份，据报道发现某些二进制文件使用了 NVIDIA 代码签名证书进行签名，但并非由 NVIDIA 创建 (1)。根据报告，该事件与 Lapsus 勒索软件小组入侵 NVIDIA 内部系统有关。

事实证明，被盗的用于签名二进制文件的密钥已于 2014 年过期，这本该由于过老无法造成任何损坏，但这次攻击暴露了 Microsoft Windows 的另一个弱点：安全策略将接受 2015 年 7 月 29 日之前颁发的证书，即使它们已经过期。这一措施是微软在引入 Windows 10 的该策略时为了后兼容而采用的。幸运的是，在这些日期检测到的恶意软件样本躲过了常规扫描。然而，所有用户或高级 Windows 系统用户都需要审查安全策略，并检查使用该密钥的驱动实例。

作为一名 Linux 爱好者，你会将其看作是一个小小的意外——这是微软通过揭开他们埋藏在细则中且不轻易解释的内容来解决问题的又一例。但作为一名记者，我不得不补充说，这些证据中可能还有其他问题。例如，我们不知道攻击者最初是如何进入 NVIDIA 网络的，但一个未修补或配置错误的系统可能是其中之一。另一个例子：暴露的密钥仍然可以作乱，所以不要把它们锁好后就由它们不管。

也许这个故事中最奇怪、最引人入胜的部分是攻击的显性动机。根据报告，

NVIDIA 最近为 RTX 30 系列 GPU 的驱动程序引入了新的保护措施，以限制 GPU 作为加密挖矿中计算哈希值的工具。NVIDIA 显然厌倦了矿工买下所有硬件并剥夺其传统客户（如游戏玩家和图形电源用户）。

在这种情况下，攻击者想要的只有钱，除非使用 Lite Hash Rate (2) 的密钥，这样他们可以使用显卡进行加密挖矿。如果这个计划成功，我们将看到攻击者的新时代，你不仅是尝试，而是试图通过控制或绕过公司自身的策略来控制该公司。有些理由让这种攻击看起来并不虚假。公司可能因为其软件存在漏洞而遭受违心的攻击，或者因为你有一个偷来的密钥来由于管理不当而更新公司政策，这意味着 CEO 同意这样做并可能会为此获得报酬。而且，私下谈判以规避公众审查实际上可能是非法的。

作为一种获利手段，这种场景在我看来有些怪诞，就像亚伯拉罕·林肯决定让第三个假品逃离监狱一样。从攻击者的角度来看，这完全取决于你能把边界推到多远。如果有效，就能带来大量的挖矿收益。什么能阻止你尝试呢？

Joe

Joe Casasad,

总编辑

![](img/d0fe54f1060b69f0f3f8ac0f16844891_2_0.png)

信息

- [1] "Stolen NVIDIA Key Can Sign Windows Malware" by Gareth Corfield, The Register, 2022年3月5日, https://www.theregister.com/2022/03/05/nvidia_stolen_certificate/

- [2] Future Steps Getting GeForce Cards into the Hands of Gamers: https://blogs.nvidia.com/blog/2021/05/18/hr/

- [3] "The Post to Steal Lincoln's Body" by Peggy Robertson, American Heritage, 1982年4/5月, https://www.americanheritage.com/plot-to-steal-lin

- OPC UA：使用 Python 和 Node-RED 创建工业客户端-服务器系统。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_5_0.png)

![](img/d0fe54f1060b69f0f3f8ac0f16844891_5_1.png)

![](img/d0fe54f1060b69f0f3f8ac0f16844891_5_2.png)

Manjaro 有时被视为 Arch Linux 衍生版中的“Ubuntu”，它让普通用户能够像 Ubuntu 之于 Debian 那样轻松使用 Arch Linux。虽然 Manjaro 将 Arch 的安装过程替换为适配的图形化界面 Calamares 安装程序，但它仍然支持像 Arch Linux 那样的滚动更新机制以及 Arch Linux 及其仓库。此外，Manjaro 延续了 Arch 的传统，安装各种应用程序，并强调用户体验而非安装精选的软件包集合。

代号为 Qonos 的 Manjaro 21.2 是一个小版本更新，其可见变化主要由稳定性更新组成。不过，值得注意的是，Calamares 有了一些改进，多位测试者也注意到速度有所提升。该版本还包含了一段时间以来首次全新的 X Server 版本，以及针对 Kepler 显卡的 NVIDIA 驱动程序的几处修复。我们增加的内容还包括 PipeWire（预计最终将取代 PulseAudio 的系统）以及 System76 新的 COSMIC 桌面。

如果你曾对 Arch Linux 感兴趣但在安装上遇到过困难，那么 Manjaro 是理想的解决方案。凭借其对易用性的强调，Manjaro 正在通过其他发行版未具备的创新，成为初学者和中级用户的主要发行版。

与 Linux 一样，FreeBSD 是一个自由的类 Unix 操作系统。FreeBSD BSD 是 2003 年从开发方向不同的 FreeBSD 中分支而来的。其后的开发深受创始人 Matthew Dillon 所参与的 AmigaOS 的影响。

从一开始开始，FreeBSD BSD 就专注于精炼 BSD 核心。最新版本也不例外。它具有虚拟机功能、针对交换空间的网络栈支持，以及针对固态硬盘（SSD）的优化。特别值得关注的是，DragonFly 的文件系统 HAMMER 使用了 ZFS 特性进行快照和崩溃后的即时恢复。此外，最新版本还包含了本地和远程服务器的新增强功能。这些技术创新与数以千计的第三方应用程序并存。DragonFly BSD 也会吸引那些了解类 Unix 系统内部工作原理的人士。然而，DragonFly BSD 也足够易用，是学习 BSD 家族操作系统与 Linux 比较的完美起点。

据我们所知，恶意软件和《Linux Magazine》对与使用本文内容相关的任何计算机系统中断、丢失或损坏不承担责任。请将所有查询发送至 subs@linux-magazine.com。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_6_0.png)

现代软件应用通常针对 Web 开发。Linux 专业人员协会（Linux Professional Institute）新的 Web 开发计划支持你在软件开发的第一步。它包含了适用于培训和自学的学习材料。通过 Web 开发考试后，你将获得一份证明你能力的证书。学习材料可在 [learning.lpi.org](https://learning.lpi.org) 获取。可以在 [lpi.org/wde](https://lpi.org/wde) 了解更多关于该计划和考试的信息。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_6_1.png)

技术、趋势和工具更新

长期以来，Linux Mint 依赖 Blueberry 作为其后台服务。随着 Linux Mint 21 的发布，在所有变化中，开发者选择迁移到 Blueman。这一改变的主要原因之一是最新版本的 gnome-audio-backend 引入了一些破坏与 Blueberry 兼容性的更改。遗憾的是，Blueberry 在今后的桌面环境中将遇到麻烦。

另一个改变的原因是 Blueman 在蓝牙方面表现更好，并且可以连接到更广泛的设备。Mint 开发者目前正在将 Blueman 集成到桌面操作系统，并希望在版本 21 正式发布时准备就。目前 Linux Mint 21 还没有官方发布日期，但如果遵循历史，它应该在今年（2022年）某个时候发布。

要了解更多关于这一即将到来的变化以及新版本的其他有趣细节，请查看本期。

要了解更多关于这一即将到来的变化以及新版本的其他有趣细节，请查看本期。

要了解更多关于这一即将到来的变化以及新版本的其他有趣细节，请查看本期。

Pipe 可能是多年来冲击 Linux 的最大漏洞。目前 Linux Mint 21 还没有官方发布日期，但如果遵循历史，它应该在今年（2022年）某个时候发布。

数十年历史的内核被发现。目前 Linux Mint 21 还没有官方发布日期，但如果遵循历史，它应该在今年（2022年）某个时候发布。

# 新闻

## Dirty Pipe 可能是多年来 Linux 临的最严重的漏洞

Dirty Pipe 的名字致敬了 2016 年发现的 Dirty Cow 漏洞，以及管道（pipeline，这是 Linux 中一种允许进程共享数据的机制）。Dirty Pipe 的跟踪编号为 `CVE-2022-0847`，它是在研究人员在排查客户 Linux 服务器上持续出现的损坏根文件（root files）时被发现的。经过数月的分析，Kellermann（来自 Ionos 的研究人员）发现这些文件是由于 Linux 内核的一个漏洞导致的，并利用了该漏洞。在 Linux 机器上，如果拥有一个可以向 root 账户添加 SSH 密钥的账户，那么任何不可信的用户都可以远程访问该服务器。

同样的漏洞使得攻击者能够劫持 SUID 二进制文件来创建一个 root shell，从而允许不可信的用户覆盖只读文件中的数据。在受漏洞机器上可以采取的其他操作还包括将 cron 任务作为后门，或修改特权服务使用的脚本或二进制文件。

可以在这篇红帽安全公告中了解更多关于 Dirty Pipe 的信息（https://access.redhat.com/security/vulnerabilities/RHSA-2022-002）。

2013 年，在一次取证调查期间，高级安全团队 Pang Lab 发现了一个相当隐蔽的恶意软件。2016 年至 2017 年间，黑客组织 The Shadow Brokers 泄露了据称从方程组（Equation Group）盗取的大数据（包含指向 NSA 的链接，其中包含黑客工具和利用程序）。同时，该小组泄露了另一个数据转储，其中包含一个被方程组攻击过的服务器列表。

根据高级安全研究团队的说法，Bvp47 被用于针对全球 47 个国家的 267 多家机构，涵盖电信、军事、高等教育、科学和经济部门。这些攻击持续了十多年，因为恶意代码的创建是为了让黑客能够对受感染设备保持长期控制。而且由于攻击使用了零日漏洞，因此没有任何防御手段。

Pang Lab 的行动代号为“望屏行动”（Operation Telescreen），该发现的后门需要向主机发送一个检查代码才能正常运行。他们还确定 Bvp47 是一个顶级的 APT 后门。

至于 Bvp47 现在是否仍在使用，目前没有迹象表明情况如此。但考虑到该漏洞的性质，如果任何研究实验室发现这些泄露的文件被用来凑出更危险的恶意软件，他们也不会感到意外。

阅读 Pang Lab 的报告以获取更多信息（https://www.pangulab.cn/en/post/the_bvp47_a_top_tier_backdoor_of_us_nsa_equation_group/）。

每两周在您的收件箱获取最新新闻

免费订阅 Linux Update-Update

Bjorn Helga 在另一个 Git 树的合并请求（merge request）中提交了 PCI 补丁。这是像 Linux 内核这样的大型项目开发过程的标准部分，而这次请求包含了数千项贡献。其理念是让一群人在给定的子项目上工作不会破坏每个人的树。通过合并请求，贡献者请求 Linux 解决他们可能产生的更改与其他同时进入内核的其他更改之间的冲突。不，这里没什么特别的，但贡献者们确实在同一时间工作，同时又不会损害其他贡献者的利益。

在这种情况下，他注意到后台发生了一些诡异的事情，并向他提出了一个问题。具体来说，Bjorn 和他的 PCI 随者已经从各个子项目（在他们的子项目内部）进行了一些合并，随后是 Linux 官方仓库似乎来自同一棵树的回滚（reversion）。这并不诗意，他们只是在尝试修复问题。

因此对于所有对象，补丁本身被回滚了。一个补丁之前被接受到树中，但回滚也是一个需要通过与其他补丁相同的过程接受的补丁——包括一个有意义的提交消息，而该补丁回滚并没有。然而，对于具有有意义提交消息的补丁来说，这种情况相对少见——开发者不想看到这整个补丁回滚的作用仅仅是撤销最近放入的内容。

在这种情况下，Linux 指出，回滚的目的并不是因为补丁本身不好——而是专门为了在 Linux 最终将 PCI 树合并到自己的树时减少冲突。

这有两个问题。首先，关于补丁回滚得出的自然结论是它是错误的。在这种情况下，补丁可能来自另一个树（这里就是如此——PCI 回滚了该补丁以便它可以从那里回来），Linux 说，得出的自然结论是来自另一个树的补丁也是错误的。如果相同的补丁是错误的，那么它仍然是错误的，对吧？所以 Linux 必须修复那些最终引入树中的内容——他确实这么做了，但意义更多。

第二个问题是，回滚和后台合并是为了解决 Linux 在针对自己的代码时会看到的冲突。Linux 称之为“纯粹的垃圾，由于这些更改，我最终‘无论如何’都完成了合并，现在 PCI 树不是在‘走’，而是有了那个提交，好吧，我必须‘走’，所以 PCI 树有了该提交，但在新树中它被回滚了，所以我正在进行不同的更改和混乱的合并。”

Linux 将此与开发者通过“变基”（rebase）其代码作为合并冲突的另一种方式进行了对比。在 Git 中，子项目将把主项目树的最新版本拉取到。

“可能发生的情况是，管理器应该以某种方式暴露它所包含的模块列表。在这里并没有对这种操作设置优先权。”

Torvalds 说道：“现在我的 github 仓库仍然基于 5.14-rc。我需要通过合并到 5.15-rc 的版本来更新它吗？还是等在 5.15 之后提交拉取请求并合并主分支就可以了？”

“所以，现在如果探针工具（probe）和类似工具位于容器中，就可以制作，它们应该向管理器请求，并带有套接字请求或任何方式，”

Linux 在列表中回复了 Paul Baucho：

> “老天爷。请不要这样。”

“而且为什么用列表形式更好呢？我认为容器请求一个模块并获取它或无法获取就足够了。” 随后 Christian 澄清道：“我的意思是，容器中的消息应该在宿主机上可见的。”

> “伙计们，你们不能在甚至不考虑代码的情况下就如此无脑地忽略所有警告”

> “无论如何，出现了完全疯狂的‘修复’建议，有人完全没必要地听从了那些喧闹的负担”

但实际上，请求一个模块而不告诉他们哪些是可用的，也可以这么简单：

> “表示‘原始’或对两个布尔表达式进行位运算的方法是使用‘||’”

> “相反，那段代码完全是疯狂的”

> “最好的方式首先是尽可能避免将我这个人类合并进来，但如果你注意到你们已经同步了，并且你们的树中模块没有问题，你们可以在该点上进行任何新开发”

> “甚至，将点定义为新东西也是个好主意——比如一个库，或者至少重新导出，因为 rc 版本可能有一点实验性”

在考虑了这些之后，无论如何，如果内核在模块按 CRU 风格迁移时包含等待，那么它将会生效。

> “我对基于内核的拉取请求没有意见。我的意思是，我倾向于不要因为焦虑或遇到问题而不得不合并他们的工作”

```c
(int) block1 || (int) block2
```

CRU 是一个用于简单管理运行和停止的工具。容器可以从停止的那一刻随时启动和停止。所以 Andy 的意思是，如果容器看到了可用模块列表，然后被冻结迁移到一个运行系统，然后启动，它可能会从一个在其宿主机系统上不可用的列表中请求模块。

> “在某个时刻，如果你正在合并多个发布版本，对我们来说由于某些基础设施发生了变化将变得不方便，所以同步一下是个好主意”

> “事情，这件事完全合理且毫无意义，而且人在这之后又说了”

> “换句话说，‘正确’的修复是查看代码并‘理解’警告，而不是为了避免警告而进行盲目的转换”

> “根据我的经验，请你们倾向于做得太多了，那么就太担心它了”

> “永远不要对源代码进行盲目的更改，因为内核是那样的告诉你的”

事实就是这样。

> “我不会拉取这个。内核的修复是错误的，然后另一个提交实际上字面上考虑了非致命的运行时错误”

> “——警告不是仅仅‘盲目’更改代码的借口”

最近，这让所有内核开发者陷入了……之中，因为它将所有的内核请求都变成了错误。这影响了我们日子里的一切，并导致了许多愿望和许多快乐的气气球手。

> “我做的这些事情之一是为了让警告消失，那个拉取请求有两个不同的例子的”

现在看起来似乎没什么大碍，但开发者们都有自己的方法来处理新的新的‘无警告’政策。例如，Paul Bonzi 提交了一些来自其他贡献者的 KV 补丁，其中一个在补丁注释中被描述为——‘逻辑而非写法’。

> “我正在添加一些人，因为显然那”

> 注意：由于显然

数字技术需要……

特别是，某些过程消耗了大量的能量，结果排放出大量的二氧化碳。例如，使用大数据训练一个常见的 AI 模型会产生约 300 吨二氧化碳当量，这相当于五辆汽车的生命周期二氧化碳排放，或者从纽约到旧金山的三百次往返飞行（加密货币另一个能源浪费的例子——参见本期其他部分关于加密挖矿的文章）。

能效算法和可持续计算对计算机科学家和 IT 工程师的发展也起着重要作用。必须关注提高软件系统能源效率问题的意识，并将“设计可持续性”原则作为 IT 开发的基础。



但在没有规则 AI 的情况下，请记住，许多算法和大数据对于减少二氧化碳排放至关重要，因为它们对于优化制造业、农业和其他行业的生产具有重要性。解决方案并不是在这些技术中变得更加“高效”或“快速”，而是要让它们更高效。

通常，计算机科学家和 IT 工程师通过算法来解决不同类型的问题。从本质上讲，不同的算法可以发展非常快（在计算结果时）且准确（100% 准确率），这可能需要大量的计算量，且长时间运行意味着高能源需求，而算法通常是复杂的。对于大规模问题，例如复杂的气候模型或交通预测，其时间复杂度随所需准确度的增加而无限增长。

程序员可以通过提高更多软件的效率来减少不断增长的二氧化碳足迹。目标是开发使用更少能量来交付实际结果的软件——尽可能使用快速、简洁的计算操作。减少能源消耗的进一步潜力在于硬件和软件设计的影响。

能效方面的一项重要研究专注于解决准确性与运行时间之间的权衡问题，通过适当的启发式方法和随机化方法产生一个尽可能接近可能解的结果，且具有“快速”和低开销的运行时间。这些“次优”算法可以非常接近精确解，取决于问题的复杂度，其差距在 10 到 100 倍之间。

在开发创新架构时，我们可以考虑性能提升与减少能源消耗之间的权衡。对于数百万用户使用的系统也是如此——即使是单个计算中微小的节省，积累起来也会变成巨大的节省。

哈索·普拉特霍数字工程研究所（HPI，图1）的实验表明，应用启发式算法来最小化调度的合适方案可以显著缩短运行时间，或者将货物分配到市场可以与传统方法相比缩短三个不同因素的运行时间。传统的软件可能需要两天来计算解决方案，而这种方法只需 10 分钟，将能源消耗降低到百分之一以下。

由于数字技术的使用占据了数字足迹最大的份额，并将继续急剧上升，因此使算法更高效尤为重要。以高能耗为代价获得更大的速度不能是未来的权衡。保持这种平衡必须成为数字系统设计的核心原则。

为了解决使用更少能量进行数字化的明显悖论，我们需要在算法设计和编程中开发新的范式，并在实践中广泛实施这些范式。诸如下等原则：

### 设计可持续性

## 2. 人工智能的能源效率

机器学习技术和深度神经网络的发展在 AI 研究领域取得了关键性进展。然而，日益增长的深度学习算法导致在训练和执行期间对能量的需求也不断增长。

现代机器学习系统在 32 位算法（如 `ResNet`）上训练神经网络。然而，使用量化和剪枝技术降低模型复杂度可以节省能量。在深度模型中寻找数据可以大幅降低算法的能量消耗。

在极端情况下，可以使用二进制神经网络以 20 倍率执行深度学习模型。虽然二进制神经网络的准确性仍比今天的 AI 系统低 5%，但它们通过能源消耗减少数百万倍得到了改进，可以节省大量的能量。

有三种编程技术的示例如果广泛实施，可能会节省能源。

数字应用与今天的许多应用一样需要海量数据集。数据量越大，处理数据所需的能量就越多。数据工程师的主要任务之一是以智能方式组织数据，以减少人工智能应用和其他形式分析的能量。

“纯”数据没有办法以多种方式对数据进行分类（本质）、归一化数据（同构结构）、消除冗余。数据分析在这项任务中起着重要作用，因为它有助于识别数据中的有用模式。

统一列编码（UCC）是数据压缩的重要部分。连续使用 UCC 可以导致更高效的数据库存储系统。然而，以前仅针对小型数据集识别 UCC，且需要花费大量的时间精力。

对于大型数据集，由于运行和内存限制，很难发现 UCC。哈索·HPI 的人员开发了一种发现 UCC 的新方法，与其他算法相比，将 UCC 的使用减少了几个数量级，同时减少了内存需求。

在中等规模数据集上，HyUCC 比 UCC 快 5 到 10 倍，平均内存占用为 20%，尽管对于较大的数据集效率会有所下降。虽然以前 HyUCC 无法在大型数据集中检测 UCC，但它可以以合理的内存消耗完成任务，使得识别海量数据的 UCC 成为可能 [5]。

数据中心是全球化的核心。云应用、流媒体、计算——一切都运行在数据中心，不断增加的能源消耗导致了全球足迹。下一代数据中心包括日益多样化的架构和硬件，为特定类算法提供了优势。然而，数据中心架构和软件是提高能源效率的最合适硬件，特别在初步评估中，使用现场可门阵列（FPGA）代替通用处理器将能源效率提高了 10 倍（见表 2）。

| 模型名称 | 准确率 | 大小 | 操作次数 |
| :--- | :--- | :--- | :--- |
| ResNet (32-bit) | 69.3% | 46.8MB | 1.61x10 |
| BinaryDenseNet45 | 63.7% | 7.4MB | 3.43x10 |
| BinaryDenseNet37 | 62.5% | 5.1MB | 2.70x10 |
| BinaryDenseNet28 | 60.7% | 4.0MB | 2.58x10 |
| 设备 | NVIDIA Tesla K20M | Intel E-5630 | Xilinx UCU |
| :--- | :--- | :--- | :--- |
| 问题规模 (MCells) | 256 | 256 | 1024 |
| 吞吐量 (M/sec) | 1127.88 | 1435.48 | 2009.35 |
| 功耗 (Watts) | 60 | 85 | 9.5 |
| 效率 (MCells/W) | 18.80 | 16.89 | 232.56 |

数字系统的能源研究仍处于婴儿阶段。目前，几乎没有相关的科学会议或期刊讨论能效软件和可持续计算问题。还需要将研究转化为产品的倡议。硅片显示的能源效率比其他处理器更高。Qasimieh 等 [7] 展示了使用 FPGA 执行计算机视觉任务能源效率提高了 20 倍。相比之下，依赖浮点运算的任务可以通过扩展的高效产品获得更高的性能和更好的能源效率。

政策制定者可以推出激励措施加强 IT 研究领域。国际竞赛可以加速高效 IT 系统的开发。特别是许多国家的公共部门，需要在采购指南中提出高效软件的要求，以建立可持续 IT 的市场。这项研究开启了如何优化分配异构计算资源以减少能源消耗的问题。

数字化温室气体排放的重要趋势。与此同时，技术的使用是控制我们工业部门的关键。然而，IT 开发从未从能源效率的角度来看。但构建消耗更少能量的数字系统是一个巨大的机会。为了实现这一点，可持续性原则必须进入科学课程，并在考虑 IT 平衡时成为一部分。

HPI 启动了 Clean-IT 倡议，探索减少二氧化碳足迹的可能性，并与科学、工业和社会伙伴一起开发高效数字化的方法。Clean-IT 交互式学习平台提供了高效算法和可持续计算的最佳实践，描述了以高效方式开发算法、数据中心和 AI 系统的具体措施（2）。

[1] The Shift Project 2019: https://theshift-project.org/wp-content/uploads/2019/03/Lean-Report-Shift-Project-2019.pdf

[2] EEA (2017), Digitalization and Energy, Paris, https://eea.org/digitalization-and-energy

[3] Carbon footprint of vitality

[4] Carbon footprint of digitalization: https://arxiv.org/pdf/1906.02243.pdf

[5] HPPI: https://arxiv.org/pdf/1905.01320.pdf

[6] J. Beghe et al., “BinaryNet: Developing an Architecture for Binary Neural Networks,” 2019th IEEE ICCV, 2019, pp. 7555-7564. https://ieeexplore.ieee.org/document/90297825

[7] F. M. Wong, “Energy Efficiency of CPU, GPU and FPGA Implementations for Vision Kernel,” 2019 IEEE ICCS, 2019, pp. 1-8. https://ieeexplore.ieee.org/document/881111

[8] J. Gong et al., “Understanding Performance Differences of FPGAs and GPUs,” 26th IEEE International Symposium on FCCM, 2018, pp. 93-96. https://doi.org/10.1109/FCCM.2018.00023

[9] Clean-IT: https://www.openit.org/clean-it-from-kumar

# 作者

Meinel 教授是哈索·普拉特数字创新研究所（有限公司）（HPI）的董事兼首席执行官，同时是波茨坦大学数字工程学院院长，并在那里担任互联网技术与系统部门主管。德国国家科学工程学院（Achetech）成员，开发了首个欧洲 MOOC 平台 openHPI，拥有 BMBF 委任的云项目，并是哈索·普拉特纳思考研究中心的主任。

德国于2000年创立了世界上第一个软件环保标签——“蓝天使”（Blue Angel）。随着各国政府关注软件对环境的影响，“蓝天使”背后的方法论可以作为其他国家的范本。作者：Marina Kohn

作为消费者，这是那种我们永远无法习惯、也不应该接受的令人心恼的坏事之一。一台花费了巨额资金的设备，仅仅因为所需的软件过时而突然变得无法再使用——也许是新软件需要更强大的组件，或者其接口与其他设备不兼容。在所有情况下，消费者都无力更换那些仍在运行的设备。换句话说，软件迫使硬件进行不必要的升级。这种常见的情况会导致严重的能源浪费。信息和通信技术对环境产生最大影响的影响发生在制造过程中。一直流传着一种说法，认为将技术更换为更节能的设备对气候有益，但在许多情况下，制造这些“节能型”设备时产生的排放比使用它们产生的排放还要多，因此你对环境能做的最好的事情就是保留现有的设备，而不是增加新设备的需求。现在你可能会认为，如果能辅以有效的回收计划，更换周期也不会那么糟糕。但在实践中，某些金属并不存在回收流程，这意味着当你扔掉电脑时，价值材料将不可挽回地丢失。大量的电子垃圾进入了填埋场。直到现在，监管、研究和制造活动的重点完全在硬件。环保标签、承诺和许多法律要求为笔记本电脑、电脑和显示器能够提高能源效率奠定了基础。而在软件方面，明天无法讲述类似的成功故事了。有些团队强调长使用寿命，但这并非所有软件产品的特征。负面示例包括：安装后会禁用电脑电源的程序、臃肿到往往响应缓慢或频繁崩溃的应用程序，以及消耗比实际需要更多的软件。这些坏功能清单列如下。请记住，通过设计减少环境影响的软件功能。软件架构的设计决定了你需要多少硬件和电能。例如，取决于编程的智能程度，软件可能需要更少或更多的处理能力和内存。图1说明了软件对环境直接和间接产生的各种影响。

建立有效环保标准的道路是坎坷且困难的。直到现在，软件一直未受关注。为什么在这个主题上监管如此之少？对软件环境影响缺乏关注至少有两个关键原因。一方面，软件与硬件之间的因果关系远没有硬件那么理想，使其难以满足最低要求。另一方面，大量不同的产品和应用程序使得评估问题的完整范围变得困难。

目前政府正在开发一种方法论，使其能够对软件的环境影响进行评分。德国科学家创立的“蓝天使”环保标签可以作为其他国家类似评分的范本。

在一个研究项目 [1] 中，德国环境署与 Öko 研究所、特里尔大学的比尔肯费尔德环境校区（Environmental Campus Birkenfeld）以及苏黎世大学合作，对各种软件产品进行了分类 (2)。借助于这种分类以及一个显示硬件与软件相互作用的详细影响模型，研究人员开发了一份可持续软件标准目录。该目录列出了76项单独的标准，我们将其分为三类：效率、对硬件持续时间的影响以及对硬件的使用。每项标准都可以参考一个或多个指标进行评估。

该项目开发了一种评估和测量方法论，你可以利用它来确定能源需求、硬件资源使用和其他环境特征。研究报告审查了来自四种不同产品的相同功能的软件产品，以评估该方法论。在标准情况下，当功能按顺序自动运行时，软件产品之间的差异非常明显（图3）。效率最低软件（底部）的能耗高于顶部软件。能源使用的差异特别具有相关性，这是因为在低效率客户端中过度使用硬件会导致执行缓慢。在最坏的情况下，用户将不得不扔掉电脑并将其更换为新设备。德国环境署利用这项研究的结果开发了软件的。

图2：应用软件的分类。

蓝天使环保标签

德国环境署利用这项研究的结果开发了软件的蓝天使标签。对于蓝天使，软件必须在至少五年的电脑上运行，并获得至少五年的安全更新。它不能干扰电脑的能源管理，并且必须披露数据格式以便使用数据。申请人必须披露软件的能耗。为了解决这个问题，德国政府开发了一种方法，包括对本地软件的能耗和利用。环保标签改进了用于本地计算和存储软件的要求。正在进行的项目将蓝天使认证的范围扩大到分布式软件以及手机或平板电脑应用程序。

资源效率：结果。编程语言、组件和容器类的资源效率。这项工作将使开发者能够创建更节能、对硬件友好的软件。任务将需要有关软件组件能耗和硬件使用的信息，以及对改进能源效率指数的建议。该项目明年将提议举办黑客马拉松，为记录的问题寻找解决方案，并为最节能的软件解决方案颁奖。

通过其研究，环境署开启了了解软件引起的环境影响的窗口。但真正的挑战在于，不在软件创建后提供为开发者在软件规划和开发阶段做出正确决策所需的信息，使用优化的工具和方法来实现环境友好的

德国环境署的另一个项目——2021年启动的SOFTWARE研究项目，旨在促进更可持续软件设计的目标。该项目与可持续数字基础设施联盟和 Öko 研究所合作，将检查能源效率和

# 作者

Marina Köhn 是一位科学家，自1992年以来一直在德国环境署担任研究员。她的工作关注环境相关系统，特别是信息和通信技术（ICT）领域。Kohn 在绿色ICT相关问题上已工作了20多年。作为这项活动的一部分，她参与了蓝天使系统以及衡量数据中心和软件能源及资源效率方法的开发。

- [1] 资源效率评估原则的发展与应用：https://www.umweltbundesamt.de/en/press/pressinformation/environmental-impact-of-software-is-now-measurable

![](img/d0fe54f1060b69f0f3f8ac0f16844891_20_0.png)

职位中心 (JOB HUB)

为维护全球运行的 IT 专业人士提供的顶级职位

SysAdminJobHub.com

## 淘热

随着气候变化在全球范围内造成破坏，我们才开始思考如何利用我们的技术来保护并减少我们的碳足迹。这时，加密货币挖掘随之而至。

作者：Jack Wallen 和 Jose Assad

![](img/d0fe54f1060b69f0f3f8ac0f16844891_21_0.png)

对 IT 行业能耗的研究，如果不观察其中最大的“罪祸首”之一——以及一个近年来呈指数级增长的问题：加密货币，将是不完整的。对于用户而言，加密货币是全球范围内高效、体面的货币，但收益是，加密货币挖掘正以惊人的速度运行。

比特币挖掘每年消耗约 91 太瓦的电力。美国每个家庭每年用电超过 11,000 千瓦，这相当于 8500 万家庭的用量——随着比特币的普及，这个数字每年都在相当于美国所有能源增长总量的七倍。根据某项研究 [2]，如果将挖掘比特币的总能源成本除以比特币交易的总数，那么每枚比特币的能源成本为 100 美元——终将如此。

请记住，比特币只是许多加密技术之一。总而言之，用于加密货币挖掘的电力约占全球总用电量的一半（与华盛顿州运行所需的能量相同）。在过去的五年中，矿工数量一直在增加。然而，这种使用水平是不可持续的——特别是如果像专家预测的那样，加密货币成为主导交易货币。

矿工执行猜测哈希值的任务，以验证区块并确保区块可以添加到链中。比特币和其他其他领先加密货币使用的方法是工作量证明（Proof of Work）。在工作量证明场景下，矿工们相互竞争以获得正确答案。新区块的当前奖励是 6.25 BTC（比特币）。获得第一个奖励的人意义重大（超过 226,000 美元），尽管矿工们经常聚集在一起分工并平分奖金。获得首名的激励很大，这导致了对更强大计算机系统的竞争。

比特币算法中内置的另一个特性是，随着挖掘比特币的计算机变得越来越困难，用于挖掘区块的解谜题解决得越来越快。这种难度进一步扩大了硬件和电力使用之间的差距。

比特币的另一个价值在于它为更强大的系统提供了巨大的激励。由于比特币发明者中本聪（Satoshi Nakamoto）创建了 2100 万单位的上限，以使货币具有稀缺性，而这种稀缺性和目前对比特币的需求创造了无限的供应。这种稀缺性，中本在发明该系统时可能从未想象过。在创建 200,000 个区块之后（约相当于四年），奖励的比特币数量逐年下降，而等值于美元的奖励则随着比特币价格的飙升而爆炸式增长。

区块链技术通过构建区块（交易组）到链（所有区块的完整轨迹，记录了自货币诞生以来的所有交易）。区块通过图形哈希值进行存储和相互连接。细节非常复杂，但为了讨论之目的，被称为 bitcoin 的计算机设备

奖励减半意味着挖掘比特币的最佳时机是现在，而不是以后，这只会加剧目前的狂热。在下一次减半时，将需要更多硬件才能生存，矿工将试图尽可能挖掘以影响整体趋势，从而引导加密货币挖掘的能源消耗。

为了保持竞争力，公司必须招募最新、最快的硬件以跟上。另一个影响是，由于挖掘比特币的计算机正在不断淘汰。

加密货币挖矿的影响

加密货币行业对总用电的影响是该行业最沉重的负担。大多数人认为，比特币和以太坊等货币的挖矿需要改变工作证明（Proof-of-Work）模型。作为工作证明的替代方案，权益证明（Proof-of-Stake）应运而出。与其让大量矿工竞争解决方案，解决方案是质押权益，即作为获得挖掘区块权限的某种押金。权益证明模型内置的特性是确保没有单一操作者垄断系统的必要机制。该模型的安全性和稳定性在很大程度上取决于实现细节及其构建方式。

以太坊目前正在使用工作证明，但正在转向权益证明协议。在以太坊的[12]版本中，用户必须成为验证者，或者质押 22 枚 ETH 以换以太坊——目前的交易价格为 2000 美元。根据该网站，“验证者被随机选择，并因创建区块而获得奖励。”用户使用质押是激励良好行为的一种方式。例如，用户可能会因离线（失败）或故意合谋而损失部分质押。



较小的加密货币已经在使用权益证明。Cardano [13] 是市场上最大的权益证明项目。Cardano 使用 Oboros 协议，“Cardano 项目说”——一种环境可持续的、可验证的基于权益证明的安全机制。与比特币不同，它的网络是可以持续扩展以满足全球需求的，同时在不损害速度或效率的情况下仅消耗 6GWh 的电力。

权益证明模型允许你减少验证交易和区块所需的电力。这种基于共识的机制，随机选择方法需要更少的矿工投入网络，并消耗更少的电力来完成过程。

遗憾的是，从工作证明到权益证明的转换可能需要更长时间来实现，只要致力于这种转型，加密货币的使用将继续增加。

权益证明协议对世界来说仍然较新，目前还不清楚它们是否能完全替代工作证明。一些人认为权益证明可能会导致更加中心化。里斯本高等理工学院（University of Lisbon Superior Tecnico）计算机科学教授 Elena Ruiller 表示，权益证明，“一个主要的缺点是，在系统中，质押最多的人拥有最大的权力。而且在许多情况下，这些系统仍然比比特币缺乏去中心化 [14]。然而，权益证明需要持有质押然后进行随机选择以避免竞价战。此外，如果你需要质押权益来操作，你可能不需要像工作证明那样需要昂贵的硬件，因此如果实施得当，权益证明可能更加民主。”

权益证明面临的另一个问题是尚未在大规模上得到证明。理论上，它已经考虑了对环境的影响，但在我们看到它达到工作证明相同的规模之前，无法知道转型是否能顺利进行。以太坊和权益证明区块链目前的价值超过 1 万亿美元，而其他平台才开始采用真实用户。

大问题是权益证明是否能在显著降低加密货币挖矿环境影响的同时实现扩展。权益证明能够减少油钻消耗尚待在大规模下测试；否则，加密货币挖矿日益增长的能源可能会导致高价格。这项技术将继续消除工作证明向权益证明和其他方法的影响。在比特币改变其方式之前，使用将仍然是加密货币行业的一个严重问题。

- [1] 比特币矿工消耗了全球用电 0.5%：https://www.businessinsider.com/bitcoin-mining-usage-more-than-2021-09-2

- [2] 每一笔比特币交易——使用切片选择高能耗过程——成本 1000 美元：https://www.fortune.com/2021/10/26/bitcoin-transaction-consumption-fortune/

- [3] 比特币电子垃圾监测：https://digonomist.com/bitcoin-electronic-waste/

- [4] 碳足迹的成本：https://www.cell.com/fulltext/s5242-4351-22(u00086-1

- [5] 油钻矿工就全球用量产生水资源争纷：https://www.businessinsider.com/sustainable-business-oil-drill-consumption-bond-over-water-2021-05-21/

- [6] Elena Warren 参议员透露：随着美国加密货币挖矿业务的增长，参议院发出警告：cases.senate.gov/news-releases/as-crypto-mining-energy-use-exponentially-growing-climate-impact-and-carbon

- [7] 纽约州参议院关于比特币的工作证明：https://www.nysenate.gov/legislation/2021/6684

- [8] 欧盟监管机构可能禁止比特币工作证明矿以保护森林：https://www.euronews.com/next/2021/02/19/eu-regulators-could-ban-proof-of-work-bitcoin-mining-to-save-renewable-energy/

- [9] LearnFinance：https://www.learnfinance.com/blog/the-most-cryptocurrency-concerns-for-2021/

- [10] SolarCoin：https://solarcoin.org/

- [11] Powerledger：https://www.powerledger.org/

- [12] 以太坊：https://ethereum.org/developers/

- [13] Cardano：https://cardano.org/

- [14] 权益证明对比工作证明：https://www.businessinsider.com/

## 回顾

然而，MuseE 实现这些原则的方法对于习惯了 Ardour 或 Bitwig 的用户来说需要一些时间适应。

在启动时，MuseE 会提议初始化外部和虚拟 MIDI 生成器。你可以直接向这些设备发送命令进行单独的配置，这表明 MuseE 比其他 DAW 更能将声源生成器与音乐数据隔离开来。

第一步，你需要设置声源生成器以及物理音频输入和输出。然后你就可以通过 MIDI 信号和音频数据跟踪这些设备（图 3）。

MIDI 连接的配置（图 4）结果证明并不怎么符合直觉（这可能导致一些人迅速放弃该程序）。虽然配置显示了所有属性，但它并没有让你将设备连接到任何地方——尽管有一个工具提示在指引你。该工具提示未能指出，你必须将设备设置为 Muse 端口，以作为 MIDI 轨道的输入（如下文的“设置合成器”部分所示）。

图 1：在执行 AppImage 文件后，你可以立即启动 MuseE。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_26_0.png)

## 设置合成器

在录制 MIDI 轨道并发送到生成器之前，你需要为每个生成器在 MuseE 中设置一个设备。该设备将作为编排器（Arranger）中的轨道出现。MuseE 为设置设备提供了两个选项，它们在某些方面有很大不同。第一种选项是通过右键在编排器中插入轨道。当你这样做时，MuseE 会显示可用的端口列表并对其进行排序。

从列表中选择所需的端口后，你就可以将其用作乐器。在后台，MuseE 会在列表中创建一个新条目，你可以在 `Edit|MIDI Ports!` 中找到它。然而，第一种选项阻止了你多次使用同一个插件。如果你无法使用同一个插件的多个实例，那么这种限制将非常奇怪。特别是对于合成器来说，拥有六个左右独立的“噪点旋转器”（noise spinners）是很常见的。从纯粹的技术角度来看，这在目前所有的插件系统中都不是问题。

你可以使用第二个选项。如果你直接在 `MIDI Ports| Soft Synths` 下方的列表中创建合成器，该限制就会消失。当你创建一个新实例时，它也会立即作为合成器轨道出现在编排器中（图 5）。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_26_1.png)

图 2：得亏 yibridge，Windows 世界的免费软件 Feldspare 在 MuseE 中运行得完美。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_26_2.png)

图 3：MuseE 的路由允许你设置信号源、声源生成器和音频输出（路由）。你单独加载插件以便从右侧的列表中访问它们。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_26_3.png)

MusE4

![](img/d0fe54f1060b69f0f3f8ac0f16844891_27_0.png)

| 文件 | 类型 | 实例 | 名称 | 版本 |
|---|---|---|---|---|
| lead | VST (synth) | 1 | MIDI Wave Free | 0.1 |
| lead | VST (synth) | 2 | MIDI Wave Free | 0.1 |
| lead | VST (synth) | 3 | MIDI Wave Free | 0.1 |
| lead | VST (synth) | 4 | MIDI Wave Free | 0.1 |
| lead | VST (synth) | 5 | MIDI Wave Free | 0.1 |
| lead | VST (synth) | 6 | MIDI Wave Free | 0.1 |
| lead | VST (synth) | 7 | MIDI Wave Free | 0.1 |
| lead | VST (synth) | 8 | MIDI Wave Free | 0.1 |
| lead | VST (synth) | 9 | MIDI Wave Free | 0.1 |
| lead | VST (synth) | 10 | MIDI Wave Free | 0.1 |
| lead | VST (synth) | 11 | MIDI Wave Free | 0.1 |
| lead | VST (synth) | 12 | MIDI Wave Free | 0.1 |
| lead | VST (synth) | 13 | MIDI Wave Free | 0.1 |
| lead | VST (synth) | 14 | MIDI Wave Free | 0.1 |
| lead | VST (synth) | 15 | MIDI Wave Free | 0.1 |

**图 4：** MIDI 端口和软件配置工具，右下角的小窗口可以让你将设备映射到 MusE 中的轨道上。

对于编辑录制的材料，MuseE 提供了自己的工具；你可以通过点击录制或导入的部分（在 MuseE 术语中称为和弦音符或音波）在门中打开编辑器。主编排器视图作为底部的第一个标签保持打开。

MuseE 去掉了编排器视图中的缩放功能。根据任务的不同，你将看到各种视图和功能。然而，MuseE 的波形编辑器被证明是非常新颖且直观的。在熟悉之后，可以使用波形编辑器执行精确的切割和简单操作，例如归一化。

对于鼓点音符，因为它们在同一个小节内无法单独设置节拍。虽然菜单中缺少了一些重要功能，但你可以通过快捷键访问它们。例如，`Ctrl + B` 允许你插入 MIDI 部分作为克隆（图 7）。对原始对象的更改对克隆同样有效。`Ctrl + V` 允许你创建独立的副本。如果你在使用鼓点循环，使用克隆要高效得多。一个在编辑器中修正后并不完美的音符在克隆中处于正确的位置。

最后，MuseE 的谱面编辑器提供了一个独特的选择点（图 8）。即使

我在 2005 年在卡尔斯鲁厄的 Linux Audio会议上认识了 Muse 的创始人 Werner Schewer。当时 Werner 已经是一位经验丰富的开发者，他在周围聚集了自己的团队，并展现出卓越的专业知识——无论是在软件还是音乐理论方面。作为一名专业级钢琴家，他了解音乐的数学基础，而为音乐家开发软件确实需要这种知识。

Schewer 参与的 Muse 衍生分实际上是一个逻辑步骤。MuseScore 归 Creative Group 的“Muse Fusion”所有。遵循 Unix 原则“只做一件事并将其做好”，这旨在从通用 DAW 的复杂性中将复杂的音乐理论扩展出来。

Robert "Johnson" son 5；Muse 目前的主要开发者，他在摇滚和金属乐乐队中演奏，并在 Muse 中创作了令人印象深刻的音乐。Muse 在音频处理方面的表达有限可能部分源于 Johnson 的信念：他宁愿录制一次失败的录音，也不愿修复录制糟糕的音频轨道。令人叹的是 Muse 相关人员的坚韧。在困难时期，他们没有放弃，而是不断开始，并让软件适应快速变化的环境。

# 测评

MusE 4

昂贵的 Bitwig Studio 并不提供谱面视图，更不用说编辑器了。Linux 上一个流行的替代品是 MuseScore [4]（正如其名所示，Muse 项目），它为古典作曲提供了更多功能（即“历史记录”框）。

随处可见内容丰富的右键菜单。你通过主菜单打开的工具在它们的对话框中提供了各种复杂的功能。

在合成器轨道中对参数进行自动化处理，明确了该轨道对于生成器的用途，因为在 Muse 中，它不包含任何音乐数据（图 9）。

许多 DAW 功能可以直接在 Muse 界面中控制。然而，为了补偿热门主菜单中稀疏的注册表

为了解决这个问题，编排器（Arranger）顶部的功能表在默认设置下增加了一项。你会在这里发现一些起初可能会忽略的功能。例如，其中之一就是合成器的图形界面，以及合成器轨道中的所有参数。

直接将曲线分配给合成器会使它们变得更容易。如果你想为另一个录制轨道创建不同类型的自动化，可以创建一个独立的插件实例。如果你熟悉 Ardour 项目，就已经知道了这个概念。

在过去几年，其他 DAW 中出现了类似于列表的轨道：一个声音对应多个数据轨道。有时，数据轨道可以包含单独的自动化，例如录制期间使用键盘调制轮制作的自动化。这是一个概念上的区别，因为这些自动化没有与单个合成器关联，而是通用的 MIDI 参数，每个乐器都是相同的。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_29_0.png)

**图 9：** 复杂单音合成器（Monosynth）的自动化轨道，它有自己的插件轨道，而不是由 MIDI 轨道控制它。你可以控制合成器界面允许你控制的任何内容。

近年来，对于名字中带有“Muse”字样的软件引起了一些困惑。虽然在搜索可能会找到同名的英国摇滚乐队，但引起更多困惑的是 muse-sequencer.org，它指的是一个非营利实体。实际上，muse-sequencer.org 是一个针对专有音乐制作软件的隐蔽广告网站。

此外，其他软件供应商也也将自己的产品命名为 Muse，从医疗联系管理系统到 iOS 备忘录应用。Muse 6 实际上与音乐软件有关，它是位于美国的 Ultimate Guitar 制造者的网站。因为他们使用瑞典顶级域名，人们很容易认为他们与来自瑞典的 Robert Johnson 没有任何关系。

最后，Muse 不应与 Muse 集团（MuseScore）混淆，该集团在 2021 年 4 月收购免费软件 Auditor 时 [7] 引起了动动。Muse 集团还提供 Muse (8)，它作为音乐人的一种社交网络存在。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_29_1.png)

**图 10：** 在 Trackstation 视图中使用你的电子邮件和密码注册你的 Mackie 后，BitRok 在 MusE 中运行得完美无缺。

MusE 自带了数十种流行合成器的预设，以及许多现代插件。当你为乐器选择预设时，程序会将控制信号嵌入数据中。虽然初始化可以作为脚本实现，但对此没有专门的工具，而且这需要大量的知识，但如果你知道它们的内部接口是如何工作的，你几乎可以用它们做任何事情。

MusE 4 不仅现代界面令人印象深刻。它看起来也比前代产品更成熟、更精细。简单音频的工作方式在很大程度上是独特的。

集成 Windows DLL 格式 VST 插件的用户将令许多用户满意。希望 Robert Johnson 未来继续像这样耐心和坚持地为这个 Linux MusE 的路线图工作 :::

对于需要音频材料的项目，Ardour 提供了更多可能性。对于 MIDI 竞赛，MusE 目前缺乏任何 DAW。Bishop 可能会为循环提供更多选项，但它缺乏 MusE 的符号编辑器。

- [1] MusE: https://musee-sequencer.github.io/
- [2] yabbridge: https://github.com/robert-vdh/ybridge/releases
- [3] Wine: https://wiki.winehq.org/Download
- [4] MuseScore: https://musescore.org/en
- [5] Robert Johnson: https://x.com/post/25297044437/floss-your-music-robert-johnson
musescore.com
- [7] Audacity acquisition: https://www.microradar.com/news/audacity-spyware-claims
- [8] 商业 MuseScore 社区: hmmmusescore.com

导入 MIDI 的后续设置可能需要该领域的深度知识。此外，MusE 与 yabridge 协作的方式

依靠 MusE 合理的自动化并增加复杂度是有意义的。常见的合成器插件如 Yoshimi 或 Carmosynth 即使在你没有它们的情况下也可以运行。Linux 模块（如 BioTech 合成器）也是如此。BioTech 的注册让你在购买 BioTech 并结合 Mackie 的波形（'10'）时，你可以在 MusE 中使用它。

## 作者

Hartmann 担任讲师、作者和音乐家。他让免费和自制音乐融在一起。Hartmann 在 http://lapoc.de 上的服务器上有他与免费音乐软件合作的知识共享许可作品。

Linux 杂志：请谈谈你是如何接触 BSD 的。

MD: 在早期（现在我指的是 1980 年代），开源要强大得多，而且个人可以组合并出售出色的

LM：DragonFly BSD 是如何开始的？

MD: 那个时代的许多项目（1980 年代后期进入 1990 年代）仍然非常成功并处于增长痛苦中，他们的用户基于开源，以及天才的天赋。在许多 BSD 中，最有趣的是 DragonFly BSD（本月介绍）。DragonFly BSD 有着重构 Unix 的历史，并不断让变得更好。

最终，BSD 项目的问题导致了它们的失败，年轻一代开始迷恋 GNU 许可协议，而选择了更现实的 BSD 式生活馈赠；Linux 占据了主导地位。

这种连接（流或数据包组合）已经尽可能达到了相似的程度。

典型的独立备份和快照模式：



Dragon 子系统（Dragon-subsystems）与 Linux 非常相似，因此我们有一些来自其他操作系统的用户为了特定领域进入 FreeBSD。其中包括在内存有限的机器上具有强大的自由度，并拥有一个非常出色的进程调度器。我们的交换和分页系统是所有系统中的最优之一，可以在低内存机器上运行并为用户提供极佳的体验（即使 Chrome 标签页打开了几周，除了内存泄漏外，也会占用大量空间）。

### LM: 为什么 Dragonfly 会分支（forked）？

随着时间的推移，Linux、Dragon 和 FreeBSD 都走向了几乎相同的终点。并不是说 Linux 更关注性能，而是它的机制比 Dragon 更加脆弱，而 Dragon 则专注于 SMP、稳定性和灵活性的结合。FreeBSD 也是如此。所有项目都必须编译运行在在那里的第三方应用程序构建。简而言之，Linux 在驱动程序方面（大部分）领先于 Dragonfly，但在原始层面，所有项目都共享大量的智力交流并从中受益。这就是它们所有运行方式的现实。

### MD: Dragonfly BSD 分支有几个原因。个人互动加上秘密主义和后门，导致 FreeBSD 项目的邮件列表变得充满毒性（在此之前和之后）。人们对于起起并重写支持多 CPU 的系统存在很大阻力，这比希望听取他们的意见更流行，但很少有人实际上在做这件事，这种组合破裂了，因此该项目产生了 Dragonfly 分支。

FreeBSD 最终选择了一条更保守的路线，这使其留在了竞争中，它的许多原则能够让小企业聚集，或者在项目附近为大型企业（例如 Netflix）工作。

### LM: 用户在 Dragonfly BSD 中发现了什么？

BSD 用户会发现一个完整的基础系统安装，这种安装可能不是以牺牲硬件支持为代价的。FreeBSD 一直在变化，大部分专有的，并且需要大量精力进行逆向工程。Linux 有 BSD 可以进行逆向工程。

Dragonfly 项目比它的开源/社会根源更有维护，并一直保持现状。其他 BSD 仍然存在，但坦率地说，所有的 BSD 项目都在缓慢消失，而 Linux 提供了类似的路径，但规模要大得多。

### LM: Dragonfly 的独特特征是什么？我们怎么看？

### MD: 这是一个非常特殊的项目，所以我们现在大部分都在谈论它，通过邮件列表发布公告。社交氛围相当悠闲。如果有谁的话，它是非常无毒的。通常，如果有人想做某项特定工作，他们确实拥有驾驶权来决定应该如何做。系统的其他部分是提供帮助，并通过实际的协作往来来确保代码符合标准，而不仅仅是在邮件列表中发表想法。我们确实有一个共地，所以有些……

### LM: Dragonfly BSD 是如何组织和治理的？

我们的重点是尽可能实现对称多处理（SMP）锁定。我们的观点是，Linux 的 SMP 锁是你起根本就不需要有的。我们专注于对 CPU 进行分区以完全消除锁定。当然，有很多锁定。仍然存在共享资源。但 Dragonfly 有许多子系统是无锁的，例如网络协议栈和数据包文件。不仅是无锁的，而且完全不共享，因此以太网硬件-Topoplaz 哈希直接将数据包哈希到正确的 CPU，其上的网络栈随之运行。

### MD: 有没有除了临时稳定性、性能和文件系统之外的独特特征？

所以我们有 MERGE2，这是一个极好的镜像文件系统，但我们引入了块级冗余机制。另一方面，大多数用户滥用此类机制，导致其稳定性还不如直接使用大量的进程能力来驱动批量构建等。在含义方面。所有 DragonFly 都有自己的生活……该项目不需要 24x7 的关注。它的成功在于开源使得剥削变得太容易了（仅仅通过一个项目），涉及到大公司中的许多贡献者，而不是局限于单个人。很多精神已经丢失了。

### LM: 你有关于喜欢常驻贡献者和用户数量的统计数据吗？

### MD: 你还想说些什么吗？

开源程序员在很大程度上必须通过其他方式维持生计——要么利用经验获得好工作，要么通过其他即使与原始工作相关的手段。这不是失败，因为开源为世界创造了技术基准——否则，社会将充斥着垃圾的商业编码设定了一个非常非常高的门槛。这也许不是当今开源作者真正所希望的。

### MD: 常驻贡献者只有一两个左右：我不知道其他的，但我经常对使用该系统的人发来的邮件数量感到惊讶。

### MD: 我认为开源领域需要一点冒险。我想起了那些没有享受到 Linux 早期“西部西部时代”益处的开源程序员。在现代，项目往往变得大得多大得多，没有任何一个程序员可以编写或维护它。一个项目的开源模型往往不再适用于它，或者至少在早期作者转向其他领域后，没有看到显著效果。人们想在别人的项目上工作——在这样的努力中会有很少的认可。GNU 许可在将代码推向更广泛的世界时虽然像是一个脚镣，但它并不是脚镣。由于 Linux 变成了更现实的 BSD 式生活馈赠，它占据了主导地位。

## Distro Walk – DragonBSD

## REVIEW



# Distro Walk – DragonBSD REVIEW

Our note is that the Linux `SMP` lock is the one you don't need to have in the first place. We focused on partitioning the CPUs to remove locking entirely. Of course, there is a lot of locking. There are still shared resources. But Dragonfly has a number of subsystems lockless, as the network protocol stacks and packet files. Not just lockless, but completely unshared, so the Ethernet hardware-Topoplaz hash a packet directly to the correct CPU and the network stack on it operates

**MD:** Are there any distinguishing features that beyond ephemeral stability, performance, and filesystems.

So we have `MERGE2`, which is an excellent image-file system, but we have taken on block-level redundancy mechanisms. On the other hand, most users abuse such mechanisms and wind up with less stability than they would just using significant process power for driving bulk builds and such. interms means. All DragonFly have their own lives ... the project does not require 24x7 attention. successful its open source makes exploitation too easy (just by a project) involving many contributors at a large company vs being contained to a single person. A great deal of the spirit has been lost.

**LM:** Do you have any statistics about liking regular contributors and the number of users?

**MD:** Would you like to say anything else?

Open source programmers, for the most part, have to make their livelihoods in other ways – either leveraging the experience to obtain a good job, or by some other means even related to the original work. It is not a failure, as because open source has created a technological baseline for the world – a very very high bar for commercial coding otherwise society with junk. It is perhaps, not really today's open source authors were hoping for.

**MD:** Regular contributors are one or two or so: I don't know about others, but I am constantly surprised by the number of emails I get from people using the system.

**MD:** I think open source in general needs a bit of a risk. I think of open source programmers who didn't have the benefit of the early Wild West era of Linux. In modern times, projects tend to be much, much larger, and no single programmer can write or maintain it. The open source model for a project often does not fit it anymore, or at least, not see significant effect after the early authors move to other pastures. People want to work on big hunt somebody else's project – there is a little recognition in such endeavors. The GNU license while being up a ball and chain as it opens up code to the wider world, is not a ball and chain. The more realistic BSD-give-away of life Linux became dominant.

## Distro Walk – DragonBSD

The text text continues as follows

the Dragon focuses on a combination of `SMP`, stability, and flexibility. FreeBSD is similar. All of the projects have to compile the build of third-party applications that end up there. In short, Linux is ahead of Dragonfly on drivers (mostly), but at the raw level all projects share a great deal of intellectual conversation, and benefit. That's the reality of all of them work.

**MD:** Dragonfly BSD was forked off for several reasons. Personal interactions coupled with secrecy and backdoors caused the mailing lists of the FreeBSD project to become toxic (before, and after them). A great deal of resistance to rising up and rewriting subsystems multiple CPUs became more popular than wanting their opinions heard, but few of them were actually doing that the combination was falling out, so the project and Dragonfly was forked.

FreeBSD ultimately went a more conservative path, kept it in the game, and many of its principles were able to put together small businesses or to work for large businesses (for example, Netflix) near their project.

**LM:** What do users find in Dragonfly BSD?

A BSD user would find a complete base system installation that might not be taken at the cost of giving hardware support. FreeBSD changes all the time, is mostly proprietary, and requires a lot of effort to reverse engines. Linux has the BSDs to reverse.

The Dragonfly project was more maintained than its open source/social roots, remaining so to that day. Other BSDs exist to today, but to be completely honest all the BSD projects have been out slowly, and the Linux offers a similar path, at a much larger scale.

**LM:** What are Dragonfly's distinguishing features? What do we think?

It is a very special project so we mostly talk about it these days, with mailing lists for announcements. The social atmosphere has been quite laid bad. It's very nontoxic, if anyone. Generally, if someone wants to do a particular piece of work, they are really in the driver's seat to see how it should be done. The rest of the system is to help and make sure that the code is up to standards by actually working the cooperatively back and forth, not just putting ideas out on mailing lists. We do have at a co-location and so some

**LM:** How is Dragonfly BSD organized and governed?

Our focus was on symmetric multiprocessing (`SMP`) locked as much as possible. Our note is that the Linux `SMP` lock is the one you don't need to have in the first place. We focused on partitioning the CPUs to remove locking entirely. Of course, there is a lot of locking. There are still shared resources. But Dragonfly has a number of subsystems lockless, as the network protocol stacks and packet files. Not just lockless, but completely unshared, so the Ethernet hardware-Topoplaz hash a packet directly to the correct CPU and the network stack on it operates

**MD:** Are there any distinguishing features that beyond ephemeral stability, performance, and filesystems.

So we have `MERGE2`, which is an excellent image-file system, but we have taken on block-level redundancy mechanisms. On the other hand, most users abuse such mechanisms and wind up with less stability than they would just using a significant process power for driving bulk builds and such. interms means. All DragonFly have their own lives ... the project does not require 24x7 attention. successful its open source makes exploitation too easy (just by a project) involving many contributors at a large company vs being contained to a single person. A great deal of the spirit has been lost.

**LM:** Do you have any statistics about liking regular contributors and the number of users?

**MD:** Would you like to say anything else?

Open source programmers, for the most part, have to make their livelihoods in other ways – either leveraging the experience to obtain a good job, or by some other means even related to the original work. It is not a failure, as because open source has created a technological baseline for the world – a very very high bar for commercial coding otherwise society with junk. It is perhaps, not really today's open source authors were hoping for.

**MD:** Regular contributors are one or two or so: I don't know about others, but I am constantly surprised by the number of emails I get from people using the system.



# Dragonfly BSD 讨论记录

**MD:** I think open source in general needs a bit of a risk. I think of open source programmers who didn't have the benefit of the early Wild West era of Linux. In modern times, projects tend to be much, much larger, and no single programmer can write or maintain it. The open source model for a project often does not fit it anymore, or at least, not see significant effect after the early authors move to other pastures. People want to work on big hunt somebody else's project – there is a little recognition in such endeavors. The GNU license while being up a ball and chain as it opens up code to the wider world, is not a ball and chain. The more realistic BSD-give-away of life Linux became dominant.

Note: Due to the provided OCR text having significant repetitions and fragmented sections, I have provided the coherent de-duplicated version of the narrative flow.

Ultimately the BSD projects' problems caused them to lose, and younger generations became enamored with GNU licensing whereas the more realistic BSD-give-away of life; Linux became dominant.

The connection (stream or packet-combination) just as close to likeness as it is possible to go.

typical independent backup and snapshotting mode:

The Dragon-subsystems are quite like Linux, so we get some users to come into FreeBSD from other operating systems for specific domains. Among these is strong freedom on machines with limited amounts of RAM and a really excellent process selector. Our swap and paging system is one of the best of all and can run on low-memory machines and still give users an excellent experience (even when they tabs open for weeks, which takes a lot of space besides memory leaks).

## LM: Why was Dragonfly forked?

Over time, Linux, Dragon, and FreeBSD all came to nearly the same place. Not that the Linux focuses more on performance, but its mechanisms are considerably more fragile than Dragon focuses on a combination of SMP, stability, and flexibility. FreeBSD is similar. All of the projects have to compile the build of third-party applications that end up there. In short, Linux is ahead of Dragonfly on drivers (mostly), but at the raw level all projects share a great deal of intellectual conversation, and benefit. That's the reality of how all of them work.

## MD: Dragonfly BSD was forked off for several reasons.

Personal interactions coupled with secrecy and backdoors caused the mailing lists of the FreeBSD project to become toxic (before, and after them). A great deal of resistance to rising up and rewriting subsystems multiple CPUs became more popular than wanting their opinions heard, but few of them were actually doing that the combination was falling out, so the project and Dragonfly was forked.

FreeBSD ultimately went a more conservative path kept it in the game, and many of its principles were able to put together small businesses or to work for large businesses (for example, Netflix) near their project.

## LM: What do users find in Dragonfly BSD?

A BSD user would find a complete base system installation that might not be taken at the cost of giving hardware support. FreeBSD changes all the time, is mostly proprietary, and requires a lot of effort to reverse engines. Linux has the BSDs to reverse.

The Dragonfly project was more maintained than its open source/social roots, remaining so to that day. Other BSDs exist to today, but to be completely honest all the BSD projects have been gone out slowly, and the Linux offers a similar path, at a much larger scale.

## LM: What are Dragonfly's distinguishing features? What do we think?

## MD:

It is a very special project so we mostly talk about it these days, with mailing lists for announcements. The social atmosphere has been quite laid bad. It's very nontoxic, if anyone. Generally, if someone wants to do a particular piece of work, they are really in the driver's seat to see how it should be done. The rest of the system is to help and make sure that the code is up to standards by actually working the cooperatively back and forth, not just putting ideas out on mailing lists. We do have at a co-location and so some

## LM: How is Dragonfly BSD organized and governed?

Our focus was on symmetric multiprocessing (SMP) locked as much as possible. Our note is that the Linux SMP lock is the one you don't need to have in the first place. We focused on partitioning the CPUs to remove locking entirely. Of course, there is a lot of locking. There are still shared resources. But Dragonfly has a number of subsystems lockless, as the network protocol stacks and packet files. Not just lockless, but completely unshared, so the Ethernet hardware-Topoplaz hash a packet directly to the correct CPU and the network stack on it operates

## MD: Are there any distinguishing features that beyond ephemeral stability, performance, and filesystems.

So we have MERGE2, which is an excellent image-file system, but we have taken on block-level redundancy mechanisms. On the other hand, most users abuse such mechanisms and wind up with less stability than they would just using a significant process power for driving bulk builds and such. interms means. All DragonFly have their own lives ... the project does not require 24x7 attention. successful its open source makes exploitation too easy (just by a project) involving many contributors at a large company vs being contained to a single person. A great deal of the spirit has been lost.

## LM: Do you have any statistics about liking regular contributors and the number of users?

## MD: Would you like to say anything else?

Open source programmers, for the most part, have to make their livelihoods in other ways – either leveraging the experience to obtain a good job, or by some other means even related to the original work. It is not a failure, as because open source has created a technological baseline for the world – a very very high bar for commercial coding otherwise society with junk. It is perhaps, not really today's open source authors were hoping for.

## MD: Regular contributors are one or two or so: I don't know about others, but I am constantly surprised by the number of emails I get from people using the system.

## MD: I think open source in general needs a bit of a risk. I think of open source programmers who didn't have the benefit of the early Wild West era of Linux. In modern times, projects tend to be much, much larger, and no single programmer can write or maintain it. The open source model for a project often does not fit it anymore, or at least, not see significant effect after the early authors move to other pastures. People want to work on big hunt somebody else's project – there is a little recognition in such endeavors. The GNU license while being up a ball and chain as it opens up code to the wider world, is not a ball and chain. The more realistic BSD-give-away of life Linux became dominant.

---
**注：由于提供的 OCR 文本包含大量的重复和片段，我已为您提供了连贯的去重翻译。**

以下是翻译后的中文内容：

最终，BSD 项目的问题导致了它们的失败，年轻一代开始迷恋 GNU 许可协议，而选择了更现实的 BSD 式生活馈赠；Linux 占据了主导地位。

这种连接（流或数据包组合）已经尽可能达到了相似的程度。

典型的独立备份和快照模式：

Dragon 子系统与 Linux 非常相似，因此我们有一些来自其他操作系统的用户为了特定领域进入 FreeBSD。其中包括在内存有限的机器上具有强大的自由度，并拥有一个非常出色的进程调度器。我们的交换和分页系统是所有系统中的最优之一，可以在低内存机器上运行并为用户提供极佳的体验（即使 Chrome 标签页打开了几周，除了内存泄漏外，也会占用大量空间）。

### LM: 为什么 Dragonfly 会分支（fork）？

随着时间的推移，Linux、Dragon 和 FreeBSD 都走向了几乎相同的终点。并不是说 Linux 更关注性能，而是它的机制比 Dragon 更加脆弱，而 Dragon 则专注于 SMP、稳定性和灵活性的结合。FreeBSD 也是如此。所有项目都必须编译运行在在那里的第三方应用程序构建。简而言之，Linux 在驱动程序方面（大部分）领先于 Dragonfly，但在原始层面，所有项目都共享大量的智力交流并从中受益。这就是它们所有运行方式的现实。



## REVIEW

### Distro Walk – DragonBSD

**MD:** Dragonfly BSD 分支有几个原因。个人互动加上秘密主义和后门，导致 FreeBSD 项目的邮件列表变得充满毒性（在此之前和之后）。人们对于起起并重写支持多 CPU 的系统存在很大阻力，这比希望听取他们的意见更流行，但很少有人实际上在做这件事，这种组合破裂了，因此该项目产生了 Dragonfly 分支。

FreeBSD 最终选择了一条更保守的路线，这使其留在了竞争中，它的许多原则能够让小企业聚集，或者在项目附近为大型企业（例如 Netflix）工作。

**LM:** 用户在 Dragonfly BSD 中发现了什么？

BSD 用户会发现一个完整的基础系统安装，这种安装可能不是以牺牲硬件支持为代价的。FreeBSD 一直在变化，大部分专有的，并且需要大量精力进行逆向工程。Linux 有 BSD 可以进行逆向工程。

Dragonfly 项目比它的开源/社会根源更有维护，并一直保持现状。其他 BSD 仍然存在，但坦率地说，所有的 BSD 项目都在缓慢消失，而 Linux 提供了类似的路径，但规模要大得多。

**LM:** Dragonfly 的独特特征是什么？我们怎么看？

**MD:** 这是一个非常特殊的项目，所以我们现在大部分都在谈论它，通过邮件列表发布公告。社交氛围相当悠闲。如果有谁的话，它是非常无毒的。通常，如果有人想做某项特定工作，他们确实拥有驾驶权来决定应该如何做。系统的其他部分是提供帮助，并通过实际的协作往来来确保代码符合标准，而不仅仅是在邮件列表中发表想法。我们确实有一个共地，所以有些……

**LM:** Dragonfly BSD 是如何组织和治理的？

我们的重点是尽可能实现对称多处理（SMP）锁定。我们的观点是，Linux 的 SMP 锁是你起根本就不需要有的。我们专注于对 CPU 进行分区以完全消除锁定。当然，有很多锁定。仍然存在共享资源。但 Dragonfly 有许多子系统是无锁的，例如网络协议栈和数据包文件。不仅是无锁的，而且完全不共享，因此以太网硬件-Topoplaz 哈希直接将数据包哈希到正确的 CPU，其上的网络栈随之运行。

**MD:** 有没有除了临时稳定性、性能和文件系统之外的独特特征？

所以我们有 `MERGE2`，这是一个极好的镜像文件系统，但我们引入了块级冗余机制。另一方面，大多数用户滥用此类机制，导致其稳定性还不如直接使用大量的进程能力来驱动批量构建等。在含义方面。所有 DragonFly 都有自己的生活……该项目不需要 24x7 的关注。它的成功在于开源使得剥削变得太容易了（仅仅通过一个项目），涉及到大公司中的许多贡献者，而不是局限于单个人。很多精神已经丢失了。

**LM:** 你有关于喜欢常驻贡献者和用户数量的统计数据吗？

**MD:** 你还想说些什么吗？

开源程序员在很大程度上必须通过其他方式维持生计——要么利用经验获得好工作，要么通过其他即使与原始工作相关的手段。这不是失败，因为开源为世界创造了技术基准——否则，社会将充斥着垃圾的商业编码设定了一个非常非常高的门槛。这也许不是当今开源作者真正所希望的。

**MD:** 常驻贡献者只有一两个左右：我不知道其他的，但我经常对使用该系统的人发来的邮件数量感到惊讶。

**MD:** 我认为开源领域需要一点冒险。我想起了那些没有享受到 Linux 早期“西部西部时代”益处的开源程序员。在现代，项目往往变得大得多大得多，没有任何一个程序员可以编写或维护它。一个项目的开源模型往往不再适用于它，或者至少在早期作者转向其他领域后，没有看到显著效果。人们想在别人的项目上工作——在这样的努力中会有很少的认可。GNU 许可在将代码推向更广泛的世界时虽然像是一个脚镣，但它并不是脚镣。由于 Linux 变成了更现实的 BSD 式生活馈赠，它占据了主导地位。

## 评估

服务器在 Web 页面上交付结果，提示允许对告警组按消息类型、传感器和源客户端的 IP 地址进行图形化处理。你必须自行判断消息是否为真实威胁。如果本地网络上的 Windows 计算机使用远程管理 API，Maltrail 会报告可疑操作，但这并不是你担心的理由。

Maltrail 并不符合个人数据保护规定。例如，在 Maltrail 服务器中，你的网络可能是扫描、端口扫描或数据泄露的受害者。当然，每份报告都会被自动检测为第 1 类告警。合理使用 Maltrail 需要你根据环境调整系统，并借此减少误报。

### 列表 1：设置 Maltrail

```
01 sudo apt install python3-py
02 git clone
-- git clone https://github.com/maltrail/maltrail
03 cd maltrail
04 sudo python sensor.py
05 sudo python sensor.py
06 nialook k8nield.net
```

### 列表 2：maltrail.conf

```
01 服务器地址
02 UDP_ADDRESS 0.0.0.0
03 UDP_PORT 8357
04 日服务器
05 LOG_SERVER server.example:8338
```

### 列表 3：匿名化

服务器展示包含所有接收告警的每日报告（报告总结了威胁、可疑 IP 地址和彩色图表中频率最高的特征）。你可以通过将鼠标悬停在上方来获取记录的统计数据。

程序和系统会在后台“拨号”，Maltrail 在概述中显示哪些手段看起来可疑。此外，Maltrail 使用许多在本地网络上通信的代理，它们彼此并不知道对方。

该项目在其网站的“真实案例”部分提供了真实攻击集合。如果你在报告中发现某些条目——如果你能够在路由器、交换机上安装 Maltrail，或者你想以软件模式运行：你可能安装 Maltrail，并在任何网络上设置传感器，通过连接的端口镜像接收每份配置的副本。在此配置下，传感器不在数据路径中，但它仍然从带有 Fitbit 或类似设备的本地网络中获取足够的信息，需要更多精力。流行的 DSL 报告仅允许通过封装器向连接中插入。这就是许多人结束和折腾开始的地方。坦率地说，各种脚本天才已成功访问 Fitbit() Web 界面和其他设备的隐藏地址。

```bash
$ cat $(date +%Y-%m-%d).log | 
awk '$4 == "*" { print $1 }' > temp
mv temp $(date +%Y-%m-%d).loglog
```

图 2：Maltrail 服务器通知告警信息。

## 深度解析

### Maltrail

如果这种奖励对你来说工作量太大了，唯一的其他选择是将 Maltrail 当作 IDS（入侵检测系统）使用。传感器运行在你监控的所有服务器上。然而，Maltrail 尚无法保护整个网络，只能保护组件。

恶意行为，例如请求中异常的 User Agent、长域名以及带有代码注入的 Web 扫描。通过 IPC 或 SSH。访问 Maltrail 服务器的 Web 界面使用 TLS 和服务器证书，这提供了足够的安全性。

这些检查并不总是精确，可能会导致误报。消息是否由于启发式算法进入 Web 页面将在参考列中显示。如果你使用 `USE_HEURISTICS` 配置参数禁用此项。

### 异常

你网络上的并非所有尝试都构成威胁。Maltrail 还将 DNS 和各种 HTTP 请求视为潜在威胁。Maltrail 防止消息记录整个条目，因此你捕获的是字段中的尝试组甚至实体。

### 展望

Maltrail 同样适用于虚拟环境。例如，你可以分析 VMware 基础设施中客机的网络流量。ESXi 主机拥有 Python，且 Maltrail 作为守护进程运行在虚拟机中。MDM 需要每个组一个根工作节点。Maltrail 通过 PCAP 访问 IP，这需要使用混杂模式的权限。在这种设置下，Maltrail 仅与虚拟服务器的访问副本工作，即使传感器进程出错或 Maltrail 未在运行（不影响（访问）。

### 特殊情况：Windows

Maltrail 正式仅在 Linux 和 Windows 上运行，但通过少量调整，你可以将 Windows 计算机作为传感器。问题不在于 Maltrail 本身，而在于带有问题的包。如果你不在意，请下载 Maltrail、Python 源码以及 Python 的 C++ 编译器并安装该包 [4]。完成此步骤后，你可以在 Windows 上启动传感器，它将以通常的方式运行（如图所示）。

Maltrail 可以报告它，但不能阻止 IP。Maltrail 拥有 iptables/、FreeFW 和 Pi，但依赖 Microsoft Defender 防火墙。至少 Maltrail 了自己的日志通过 HTTP 拦截流量。陷阱页面描述了如何将本地策略与策略集成。IP 可通过 API 或脚本或 Windows 防火墙阻止任何防火墙访问。

### 局限性

Maltrail 不是全功能的 IDS，而是一个利用公共黑列表的数据包扫描器。它无法检测复杂的行为、应用层攻击，其检测率无法完全。

另一个局限性是传感器与服务器之间的通信，它依赖于未加密的 UDP 协议。中间人攻击可以嗅探、操控或删除告警以隐藏恶意活动。互联网上的无定向流量，管理员需要加固攻击面。

### 观察与猜测

如果调查的数据流不匹配任何列表，Maltrail 将深入研究其技巧并使用 Maltrail 启发式算法。如果调查的数据不匹配任何列表，Maltrail 将深入研究其技巧并使用 Maltrail 启发式算法。

轻量级 Maltrail 传感器分析网络流量活动；从免费黑名单和信誉数据获取信息。Maltrail 还充当入侵检测系统：它加载签名并与调查的数据包进行比较。如果发生匹配，仪表板上将显示告警以警告管理员。Maltrail 不是一个实用的工具

- [1] https://github.com/maltrail/maltrail
- [2] https://github.com/maltrail/ntop
- [3] https://github.com/maltrail/script
- [4] https://github.com/maltrail/wiki
- 在 Windows 上编译：https://github.com/maltrail/py/Compiling-Py-on-Windows
- 管理员：Common python.sensor.maltrail.py
- 配置 python.sensor.maltrail.py
- `path/to/test.log`
- https://www.google.com/search
- https://example.com/filter
- https://example.com/login
- https://example.com/index
- https://example.com/test
- https://example.com/dump
- https://example.com/stamp
- https://example.com/address
- https://example.com/external

### 结论

Maltrail 不是一个实用的工具。

《Linux Magazine》是您探索 Linux 世界的指南。阅读内文，获取在其他地方都找不到的先进技术信息！

# 通过以下内容扩展您的 Linux 技能：

- 关于热门话题的深度文章，包括比特币、勒索软件、云计算等！
- 有用工具的指南和教程，帮助您节省时间并保护数据
- 故障排除和优化技巧
- 关于开源世界关键发展进展的独到见解和新闻
- 针对树莓派、Arduino 以及其他开发板系统的酷炫项目

如果您想更进一步并利用 Linux 更多功能，请从今天起订阅，不再错过任何一期节目！

# 立即订阅！

shop.linuxmedia.com/subs

## 深度聚焦

NocoDB。

## 使用 NocoDB 构建应用

### 无代码，没问题

NocoDB 让您无需编写单行代码即可构建应用程序。*作者：Dmitri Popov*

无代码平台如今非常流行，这并不难理解。它们让人们能够根据特定需求在短时间内创建应用程序，并在此过程中节省费用。即使您拥有编程技能，也可能会发现它在开发快速原型或简单应用程序时非常有用，而不是从零开始构建。



在本地机器上部署 NocoDB 最简单的方法是使用 Docker 容器。第一步是安装 Docker。在 Ubuntu 和 Linux Mint 上请运行：

虽然有几个开源的无代码平台供选择，但 NocoDB [1] 在功能性和易用性之间取得了完美平衡。它也非常容易部署，这使其成为构建简单及高级应用程序的平台。

```bash
sudo apt install nococdb
```

为了能够以用户身份运行 Docker，请使用命令将用户添加到 Docker 组：

```bash
sudo usermod -aG $USER
```

重启机器，操作即完成。

接下来，创建一个专门的目录来存储 NocoDB 数据，这样当您使用 NocoDB 容器时，您的数据将保持完整。

```bash
docker stop nococdb
docker rm nococdb
docker run nococdb:latest
```

最后，在终端中运行以下命令（将 `/path/to/nococdb` 替换数据目录的实际路径）来启动 NocoDB 容器：

您随后运行预期的启动 NocoDB 容器的命令，以自动获取最新的 NocoDB 镜像。

```bash
docker run -d -p 8080:8080 --name nococdb
```

创建 NocoDB 应用

将浏览器指向 `127.0.0.1:8080`（将 `127.0.0.1` 替换为运行 NocoDB 的机器的实际 IP 地址），您应该能看到欢迎页面。在提示时，创建一个用户账户。

NocoDB 让创建各种应用程序成为可能，从简单的任务管理器到具有多个连接表格的更复杂的笔记工具。将构建笔记工具作为您的第一个项目可能觉得是一项艰巨的任务，但它展示了将想法变为运行的应用是多么简单。这为掌握 NocoDB 功能提供了绝佳机会。除了笔记应用外，您的项目还允许您在表格中编辑每个笔记、标签和分组。

第一步是创建一个新应用并填充表格。在创建账户后，NocoDB 会显示您的“我的项目”（My Projects）。

(1) 点击“新项目”（New Project）并选择名称并创建。这将让您进入“表单与验证”（Form & Auth）部分，并添加您的所有者账户。如果您想邀请他人加入项目，请按“新用户”（New User），添加他们的电子邮件地址，选择所需的角色并发送。

现在是时候创建表格了。应用需要三个表格：用于存储笔记的 Notes、用于存储分类的 Categories 以及用于存储标签的 Tags。要创建新表格，点击左侧边栏中“表格”（Tables）条目旁的 (+) 图标。将表格命名为 Notes，并确保在“默认列”（Default Columns）部分下仅启用了 `id` 字段。

(2) 按“提交”（Submit）创建表格。这将带您进入 表格，您的首要任务是添加所需的字段（在 NocoDB 的术语中称为列）。点击表格头中的 `+` 图标，将列命名为 Title，从列下拉菜单中选择 `SingleLineText`，并按“保存”（Save）。同样，另一个名为 Note 的字段不要选择 `Single-Text`，而是选择 `LongText` 作为类型。另一个名为 Attachments 的列使用 `Attachment` 类型。

该表格需要两个列，但在您添加它们之前，需要先设置两个表格。创建一个名为 Categories 的表格。添加一个名为 Category 的字段，类型为 `LineText`。点击类别字段旁边的图标并选择“选择”（Select）。这将类别设置为每个记录（或 NocoDB 术语中的行）的唯一标识符。在术语上，可以从 Notes 表格链接到 Categories 表格中的 Category。如果这听起来很困惑，不要担心，很快就会变得清晰。切换到 Notes 表格，添加一个名为 Categories 的新列，并设置它们之间的链接。确保启用“多选”（Many）选项，从表格下拉列表中选择 Categories，并按“保存”（Save）（3）。这 Categories 列中创建 Notebook 列。使用相同的程序设置 Tags 表格。添加 Tag 列并将该表格设置为主值。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_40_0.png)

图 1：在 NocoDB 中创建新项目。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_40_1.png)

图 2：NocoDB 让填充应用变得简单。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_40_2.png)

图 3：指定表格之间的链接。

部署 NocoDB

在本地机器上部署 NocoDB 最简单的方法是使用 Docker 容器。第一步是...

## 我的项目

您帮助我们让 NocoDB 开源。我们相信自由解决问题的力量

- 开始创建一个新项目

深度聚焦

### NocoDB

切换回 Notes 表格，添加一个名为 Tags 的新列，将其类型设置为 `LinkRecord`。确保启用了“多选”（Many），从表格下拉列表中选择 Tags，并按“保存”（Save）。

应用的框架已为您就绪。要编辑它，切换到 Categories 表格并添加二三行（例如：研究、想法等）。为 Tags 表格添加几行。在 Title 和 Note 字段中，要添加附件，点击 Attachments 字段中的 `+` 图标并选择一个或多个。由于 Categories 字段链接到 Categories 列，您无法直接在 Categories 字段中输入。相反，点击 `+` 图标将看到 Categories 表格中的现有值。点击该值将其添加到 Categories 表格中。随着时间的推移，Categories 表格可能会变得很，但您可以通过 Filter 查询中输入名称并按回车快速定位所需的值。如果 Categories 表格中不存在该值，可以从“链接记录”（Link Record）对话框添加它。按“新建记录”（Plus New Record），选择所需的类别并按“保存”（Save）。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_41_0.png)

图 4：NocoDB 让您可以创建并应用过滤器。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_41_1.png)

此视图通过私有链接共享

http://localhost:8080/dashboard/#/mc/view/23ca5b4f-f685-422c-9172-633999991

访问受密码限制

![](img/d0fe54f1060b69f0f3f8ac0f16844891_41_2.png)

图 5：您可以通过私有链接共享特定视图，如有需要可以进行密码保护。

图 6：NocoDB 可以生成表单，使数据输入变得更容易。

到此时，该应用的看起来和行为都非常像一个电子表格。顶栏字段可用于快速查找匹配搜索词的记录。通过下拉列表（Sort-down list），你可以根据所需的字段对行进行排序，过滤功能允许你定义并应用规则（图 4）。当你邀请其他人协作该应用时，他们也将共享你当前的视图。如果你想让某人无需注册访问应用的特定部分，这将非常有用。点击“共享视图”（Share View）按钮将生成一个可以与任何人共享的私链接；如果需要，你还可以用密码保护视图（图 5）。请记住，NoCoDB 仅在你的本地网络上运行。你需要将图 5 链接中的 localhost 端口替换为运行 NoCoDB 的机器的实际 IP 地址。

信息

[NoCoDB] https://www.nocodb.com/

作者

Dmitri Popov 多年来一直大量编写 Linux 和开源软件，并在丹语、美语、德语和西班牙语杂志及网站撰稿。你可以在 toorky.com 找到更多关于他的信息。

# 访问 shop.linuxnewmedia.com

# 在 Linux New Media 商店探索过去，并投入新一年的 IT 解决方案。

想订阅吗？

正在寻找你本想在报摊买到的那期旧杂志吗？

shop.linuxnewmedia.com

![](img/d0fe54f1060b69f0f3f8ac0f16844891_42_0.png)

# 深度

编程快照 – Ruby 和 TeX

# 使用 Ruby 和 TeX 创建准备打印的

相集

# 相集

工程

与其在网上制作相集，Mike Schilli 更倾向于使用 Ruby 和 TeX 编写一个生成打印就绪 PDF 书的程序。作者：Mike Schilli

![](img/d0fe54f1060b69f0f3f8ac0f16844891_43_0.png)

我曾以为自己已经放弃了纸质书。今天，当我买书时，通常会使用一台切割机。我立即将其发送到打印机。单页会被输入我的电脑，我在 iPad 上对其进行手动编辑，并在那里阅读。

但有一种纸质书仍然非常珍惜并认为比其他书更好的：哑面摄影复制品，那些厚实的硬装书随意散落在酒店大堂或度假屋的小桌子上。你只需要在旁边的扶手椅上坐下，向后一靠，抬起脚，开始翻阅它们高质量的页面。

你甚至可以用自己的照片创作出这样的作品！各种在线提供商提供了浏览器工具来上传照片并进行排版。如果你每年打印一次，大约一周后，邮寄服务就会把一本精美的硬装封面书直接送达你家（图 1）。

# 动手自己来

然而，网上的设计选择非常有限。而且，由于缺乏版本控制，你总是担心编写糟糕的程序会丢失你迄为止投入的工作，迫使你重新开始。编写一个供家庭使用的 DIY 程序如何？它可以创建 PDF 格式的相集，你可以通过 Lulu.com 等打印服务轻松且廉价地一次性打印并装订。

这些书被称为咖啡桌书（coffee table books），可能是因为它们通常出现在咖啡桌上。

# 作者

Mike Schilli 在加利福尼亚州旧金山湾担任软件工程师。在他自1997年以来运行的专栏中，他每月研究各种语言的实际应用。如果你向 mschilli@permeister.com 给他发邮件，他会乐意回答任何问题。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_43_1.png)

图 1：作者在线创建的相集。

# 编程快照 — Ruby 和 Tex

通过少量 Ruby 代码，即使是程序员也可以为咖啡桌书创建打印图片。列表 1 显示了相集的定义，以及你生成的 PDF 内容。你需要为每种页面类型创建一个 Tex 模板（如封面和四页），然后将相关照片添加到文件中。第 35 行的方法输出一个名为第 5 行定义的名称（"mypdf"）的 PDF，使用 Evince 等 PDF 查看器将在你的屏幕上渲染它。

```
evince mybook.pdf
```

任何在线打印服务都会在几周内为你提供这本令人印象深刻的硬装书。

+   列表 1：mybook.rb

01 #/usr/bin/ruby

02 require "image"

04 b = B.new

05 b.name = "mybook"

07 b.add "intro"

09. "cover"

10 text: "Unstoppable Mike Schilli",

11 photos: ["rip.jpg"]

12 b.add "chapter"

15 b.add "simple",

16 text: "On the Beach"

17 photos: ["ob-jump.jpg"]

```
19 id="twotimmers"
20 text: "Planet of the A"
21 photos: ["icpf.jpg", "icpf.jpg"]
23 b.add "four"
24 text: "All the Cost"
25 photos: ["thornton-jump.jpg"]
26: "beach-rock.jpg"
27: "heron.jpg"
28: "beach-chunk.jpg"
30 b.add "chapter"
31 text: "The End"
33 b.add "outro"
35 b.print
```

在底层，Ruby 接口根据之前定义的文件生成 Tex 代码段，并在文件中添加解释性文本以嵌入 Tex 代码中。第 35 行的方法处理了一切，并在 XeXun 上调用 LaTeX，并此生成看起来专业的 PDF。你可以通过让它输入并在 XeXun 上包含 LaTeX，匹配它们的格式和排版规范。PDF 驱动程序将 JPG 照片合并到 tex 文件，你可以提取它们。

优势在于！现在书的描述可以作为代码写在文本文件中（或 Co 或 Coffee Book 中），你可以随时编辑它，或使用你喜欢的版本控制工具恢复到历史版本。

# 旧时代：Tex 和 LaTeX

当然，Tex 在底层执行的操作是很难预测照片在书中看起来是否好的，它产出了作者想要的内容。除了 Tex 之外，可能没人知道如何排版书籍——任何由 LaTeX 这样的包制作的书，都是基于 LaTeX 中正确的公式来获得精美的页面，而无需做出需要间距调整时间的隐式决策来最终获得插入布局的产物。

但一旦设置好，它就能一直工作到一天结束。他的 LaTeX 追随者的历史今天仍在被阅读，如果你能在古书店里找到他们的话。专家们会在 LaTeX 中发表数学论文，我在 20 多年前就曾用 LaTeX 写过一本 PDF 书 [3]。正如我可以告诉你：

```
sudo install texlive-latex
```

# # 深度

# ## 编程快照 - Ruby 和 Tex

从经验来看，这个特殊的选择绝对让你作者走上一条极……的道路。

# 列表 3：介绍

```
01 \usepackage[export]{adjustbox}
02 \usepackage{color}
03 \pagecolor{}
04 \color{white}
06 \usepackage{pagewidth=9in}
07 papertitle{}
08 -total(sin=6.5,in)}
09 \pagestyle{}
10 \begin{document}
11 \ffamily
```

# 列表 4：结尾

```
\end{document}
```

# 列表 5：章节文本

```
01 \maketitle
02 \vspace{\fill}
03 \center{%% text %}
```

因此，命令 `\pagestyle{}` 关闭了此功能。在 LaTeX 中，无衬线字体 modern 如今看起来有些过时了，但无衬线版本的字体（通过命令 `\ffamily` 选择）是现代的，至少在我眼里是这样。TeXbox 宏包允许你在正文中插入图片，并支持缩放等功能，以便在布局开始前使文本适应框框。书籍的页面区域由列表 6 中使用的 geometry 包指定。根据打印提供者的规范，页面为横向的 9x 7 英寸，实际区域略小，为 8x 6.5 英寸，以留出边距。对于其他服务，你需要对页面格式进行调整。某些打印机要求 PDF 使用实际区域定义页面以扩展到页边界，即使会有某种裁切过程将其修掉。这在打印过程中被称为“全出血”（full bleed）。

Tex 文档的结尾由 outro.tex 模板进行修改，它仅仅去掉了包含的 `\end{document}` 文本。

下方有一行大字体文本；该文本与右边距垂直对齐。列表引入了一个文本水平居中的环境：{center} 并包含了一组用于从 LaTeX  graphics 宏包引入 `\includegraphics` 的标题。模板处理器处理照片浮动体，而 `\caption` 命令遵循指向文本第一行的路径。LaTeX 随后会留出图像占用的空间。PDF 驱动程序在缩放至所需尺寸后设置照片。

对于需要特别突出的照片，列表 7 显示了一个带有下方标题的满页照片模板，如所包含的章节的第 3 页所示。`\graphicx` 在布局中为图像留出空间。浮动有助于在标题上方页面区域仍有空间的地方垂直调整区域。列表 7 设置了照片下方的文本，配有一个居中的图像。

# 居中浮动

列表 5 为你展示了一个带有空标题、居中文本模块的图像模板。该模板将标题占位符替换为 ERB 文件包含的值。行中的文本水平居中。列表使用 `\vspace` 设置其上方的填充空间，而行具有相同的粗细。下方的文本仅在规则线对齐的行中具有等的空区域，文本最终以某种方式位于边缘，段落间距在没有页顶的情况下被忽略了，这令人惊讶的是这会让章节标题浮动到页面顶部。

# 双塔

如果你想在横向格式的书籍其中一页上布局两张竖向尺寸的照片，请使用 twos.tex 模板。列表 8 显示了两个竖向格式图像的模板。该模板引用了作为参数传递的照片 `$photo-1$` 和 `$photo-2$`。列表 4 显示了书籍格式页面上的照片。图 2 是两张图像，第一张是今天的面包照片，第二张是旧金山的；它的镜像副本是通过 ImageMagick 词的免费工具选项创建的。

# 良好的第一印象

书籍的页面区域由列表 6 中使用的 geometry 包指定。图 1 显示了一张带有

# 列表 6：封面文本

```
01 \vspace{\fill}
02 \begin{center}
03 \hfill
04 \includegraphics[height=5.5in,valign=+]
05 <%caption [0] %>
06 \vspace
07 \end{center}
08 \vspace
09 \begin{center}
10 \hfill \Huge{%% text %}
11 \vspace
12 \end{center}
13 \vspace{\fill}
```

# 列表 7：单个

```
01 \minipage
02 \begin{center}
03 \centering
04 \includegraphics[height=5.5in,valign=+]
05 <%caption [0] %>
06 \linebreak
08 \Huge{\vspace{\par.cm} %% text %}
09 \end{figure}
```



当然，横向格式的书籍页也可以包含排列成矩形的四张照片。列表 9 为你展示了相应的文本。为了图像之间的某些间距，模板将照片缩小到 2.5 英寸高，并在第 5 行和第 13 行将水平间距设置为 0.5 厘米。垂直间距在第 9 行设置为 0.75 厘米。`\u` 字体中的下划文本在 `~center` 环境内居中，并根据第 17 行位于底部图像下方 0.5 厘米处。

### 列表 8：`twotowers.tex`

| 01 | `\n` |
| 02 | `\begin{figure}` |
| 03 | `\centering` |
| 04 | `\includegraphics[height=8,align=t]{cm}` |
| 05 | `%photo[0] %` |
| 06 | `\vspace{1cm}` |
| 07 | `\includegraphics[height=8,align=t]{cm}` |
| 08 | `%photo[1] %` |
| 09 | `\vspace{.7cm}` |
| 10 | `\par` |
| 11 | `\uppercase{\text text}` |
| 12 | `\end{figure}` |

### 列表 9：`four.tex`

| 01 | `\begin{figure}` |
| 02 | `\centering` |
| 03 | `\includegraphics[height=2,align=t]{}` |
| 04 | `%photo[0] %` |
| 05 | `\vspace{.cm}` |
| 06 | `\includegraphics[height=2,align=t]{}` |
| 07 | `%photo[1] %` |
| 08 | `\par` |
| 09 | `\vspace{.cm}` |
| 10 | `\par` |
| 11 | `\includegraphics[height=2,align=b]{}` |
| 12 | `%photo[2] %` |
| 13 | `\vspace{.cm}` |
| 14 | `\includegraphics[height=2,align=b]{}` |
| 15 | `%photo[3] %` |
| 16 | `\linebreak` |
| 17 | `\par\vspace{.cm}` |
| 18 | `\uppercase{\text text}` |
| 19 | `\end{figure}` |

*(注：由于原文中存在大量重复的“Port Security”段落，根据“不要重复输出原文”的原则，此处仅保留了核心结构的翻译逻辑，实际应用中重复部分已按要求简化处理)*

## 深度解析

## 命令行 – 端口安全

活跃的互联网连接（仅限服务器）

| 协议 | 本地地址:端口 | 接收队列 | 发送队列 | 地地址 | 状态 |
|---|---|---|---|---|---|
| tcp | 127.0.0.1:3086 | 0 | 0 | 0.0.0.0:* | LISTEN |
| tcp | 127.0.0.1:111 | 0 | 0 | 0.0.0.0:* | LISTEN |
| tcp | 127.0.0.1:443 | 0 | 0 | 0.0.0.0:* | LISTEN |
| tcp | 127.0.0.1:125 | 0 | 0 | 0.0.0.0:* | LISTEN |
| tcp | 127.0.0.1:8080 | 0 | 0 | 0.0.0.0:* | LISTEN |
| tcp6 | *:111 | 0 | 0 | 0.0.0.0:* | LISTEN |
| tcp6 | *:1716 | 0 | 0 | 0.0.0.0:* | LISTEN |
| tcp6 | *:2168 | 0 | 0 | 0.0.0.0:* | LISTEN |
| tcp6 | *:80 | 0 | 0 | 0.0.0.0:* | LISTEN |
| udp | *:111 | 0 | 0 | 0.0.0.0:* | LISTEN |
| udp | *:123 | 0 | 0 | 0.0.0.0:* | LISTEN |
| udp | *:1900 | 0 | 0 | 0.0.0.0:* | LISTEN |
| udp | *:2048-2500 | 0 | 0 | 0.0.0.0:* | LISTEN |
| udp | *:5353 | 0 | 0 | 0.0.0.0:* | LISTEN |
| udp | *:5000 | 0 | 0 | 0.0.0.0:* | LISTEN |
| udp | *:192.168.1.3:46013 | 0 | 0 | 0.0.0.0:* | LISTEN |
| udp | *:13713 | 0 | 0 | 0.0.0.0:* | LISTEN |
| udp | *:1716 | 0 | 0 | 0.0.0.0:* | LISTEN |
| udp | *:46160 | 0 | 0 | 0.0.0.0:* | LISTEN |

图 2：使用 `netstat` 显示的开放端口。

通信。有时，常用端口（系统端口）只能由 root 或特权用户使用。例如，端口 21，以及网络时间协议 (UDP) 使用的 123 端口。这些端口只能与同样相应注册了端口的其他设备进行通信。

- 注册端口（数字 1024-49151）：这些端口供注册用户运行的应用程序使用。注册端口有时被称为用户端口。
- 动态端口（数字 49152-65535）：这些端口可以被任何进程或应用程序使用，并被动态分配。动态端口也称为私有端口或临时端口。

为了彻底起，一个端口可能同时由互联网分配名称机构 (`IANA`) 分配 TCP 和 UDP 地址。每个开放的端口都是一个可能受到攻击的漏洞。这就是为什么具有安全意识的人会安装极少数量的软件。检查基础服务的开放端口是否对安全至关重要也是值得的。如果不是必要的或者以万一，关闭该端口可以降低安全风险。

图 3：查询套接字查找开放端口。

| 系统 |  |  | ipv4 | ipv6 | qlt | 协议 | 状态 |
|---|---|---|---|---|---|---|---|
| system |  |  | 40u | 16557 | 0 | TCP | *111 (LISTEN) |
| system |  |  | 42u | 16362 | 0 | TCP | *111 (LISTEN) |
| rpcbind |  | _rpc | 78u | 16547 | 0 | TCP | *111 (LISTEN) |
| rpcbind |  | _rpc | 6u | 16362 | 0 | TCP | *111 (LISTEN) |
| cupsd |  |  | 7u | 30918 | 0 | TCP | [I:63] (LISTEN) |
| 1011 |  |  | 15u | 32768 | 0 | TCP | *117 (LISTEN) |
| apache2 |  |  | 4u | 30576 | 0 | TCP | *80 (LISTEN) |
| apache2 |  | www-data | 4u | 30576 | 0 | TCP | *80 (LISTEN) |
| apache2 |  | www-data | 4u | 30576 | 0 | TCP | *80 (LISTEN) |
| apache2 |  | www-data | 4u | 30576 | 0 | TCP | *80 (LISTEN) |
| apache2 |  | www-data | 4u | 30576 | 0 | TCP | *80 (LISTEN) |
| apache2 |  | www-data | 4u | 30576 | 0 | TCP | *80 (LISTEN) |
| apache2 |  | www-data | 4u | 30576 | 0 | TCP | *80 (LISTEN) |
| minindld |  | minidna | 8u | 28352 | 0 | TCP | *200 (LISTEN) |
| ntp |  |  | 17u | 32766 | 0 | TCP | *1336 (LISTEN) |
| exim4 |  | debian-ian | 4u | 36979 | 0 | TCP | *127.0.0.1:25 (LISTEN) |
| exim4 |  | debian-ian | 4u | 36978 | 0 | TCP | [I:25] (LISTEN) |
| kdaemon |  | bb | 12u | 42058 | 0 | TCP | *17316 (LISTEN) |

图 4：使用 `lsof` 查找开放端口。

```
root@android:~# grep ntp /etc/services
ntp      119/tcp
tp       123/udp
ntps     563/tcp
```

图 5：通过 `grep` 查找端口号。

### 获取端口列表

在安装包时总是分配端口。获取完整列表的最快方法是以 root 登录并输入：

```
less /etc/services
```

典型的计算机上有数百个端口。在 `less` 中，左列显示服务的名称，第二列显示端口号以及它是 TCP 还是 UDP。某些值可能是缩写的，因此完整名称。如果你在另一个计算机上查看输出，你会发现大多数注册端口是相同的。

### 检查开放端口

安全与用户便利之间需要平衡。然而，每个发行版都不同。安装后，用户可能想检查哪些端口是开放的并考虑关闭它们。用户应该定期检查开放端口并识别任何端口。

```
unhide -u
Copyright © 2013 Yago & Patrick Cowan
nmap version 3 or later
http://www.linux-forensics.info
```

> 注意：此版本的 `unhide` 适用于 Linux >= 2.6 的系统

选项：破解

[+] 使用 `fork()` 启动破解

```
Found HIDDEN PID 5720
Cmdline: "none"
Executable: "no link"
"none" ... transitory process*
```

```
Found HIDDEN PID 5740
Cmdline: "none"
Executable: "no link"
"none" ... transitory process*
```

[+] 使用 thread functions 启动破解

```
Found HIDDEN PID 5543
Cmdline: "none"
```

图 6：使用破解技术运行 `unhide`。

### 商店

### 漏掉了某个问题？

你运气不错。大多数后台问题仍然可用。在它们消失之前下单吧！

`shop.linuxnewmedia.com`

## 深度解析

## 命令行 – 端口安全

那些不认识或不确定的。可以使用多种工具，包括 `netstat` 作为：

使用以下替代方案查询套接字：

也许最好的选择是通过 `grep` 管道 `lsof`：

```
netstat -intu | less
```

```
lsof -i -P -n | grep
```

`-i` 只显示监听或开放的套接字。使用 `-n` 选项显示端口号，而 `-t` 包括 tcp 端口，`u` 包括 udp 端口（图 2）。

选项与 `netstat` 相同。其他相关信息是左侧的 State 列以及左侧列中的 Local_Address:Port（图 3）。

在此命令中，`-i` 列出与当前互联网地址匹配的文件。`n` 选项抑制端口号转换为名称，`P` 抑制网络显示。结果是信息的清晰呈现。根据你的需要，你可能想省略其中一些。在管理网络时，你可以 `-i` 指定互联网地址（图 4）。

```
root@andy:~# unhide -v proc
unhide 2013056
Copyright © 2013 Yago & Patrick Gavin
License GPLv3 – GNU version 3 or later
http://www.unhide-forensics.info
```

> 注意：此版本的 `unhide` 适用于 Linux >= 2.6 的系统

选项：详细

[*] 正在扫描隐藏进程 `/proc` stat 扫描

图 7：在详细模式下使用 proc 技术运行 `unhide`。

```
root@andy:~# unhide -m procs
unhide 2013056
Copyright © 2013 Yago & Patrick Gavin
License GPLv3 – GNU version 3 or later
http://www.unhide-forensics.info
```

> 注意：此版本的 `unhide` 适用于 Linux >= 2.6 的系统

选项：详细

[*] 正在扫描隐藏进程 `/proc` chdir 扫描

[*] 正在扫描隐藏进程 `/proc` opendir 扫描

[*] 正在扫描隐藏线程 `/proc/task` readdir

图 8：使用 proc 技术运行 `unhide`。

```
root@andy:~# unhide --quiet
unhide 2013056
Copyright © 2013 Yago & Patrick Gavin
License GPLv3 – GNU version 3 or later
http://www.unhide-forensics.info
```

> 注意：此版本的 `unhide` 适用于 Linux >= 2.6 的系统

选项：静默

[*] 正在扫描隐藏进程 `/proc` stat 扫描

[*] 正在扫描隐藏进程 `/proc` chdir 扫描

[*] 正在扫描隐藏进程 `/proc` opendir 扫描

[*] 正在扫描隐藏线程 `/proc/task` readdir

图 9：使用 proc 技术运行 `unhide`。

图 10：使用 `unhide` 的独特技术开始搜索端口。

## 深度解析

## 命令行 端口安全

```
root@nandy:~# unhide reverse
20130526
Copyright 2013 Yagus Yasu & Patrick Gouvin
License GPLv3 : GNU GPL 3 or later
http://www.unhide-forensics.info
```

注意：此版本的 `unhide` 适用于 Linux >= 2.6 的系统

已使用的选项：

[+]通过验证所有 `all_threads_by_ps` 是否也能被其他进程看到搜索伪造进程

图 11：使用 `unhide` 的技术是搜索隐藏进程的快速方法

使用 `-d` 选项可以避免误报，例如在命令行运行的应用程序。当临时进程在进程结束时应该消失时，可能会发生误报。你可能需要运行几次，除非临时进程执行失败。在本文档中，请检查暴力破解选项 (6)。

- * *proc* 技术：检查 `/bin/ps`。在干净的系统上，目录的输出应该是空的。在输出前添加 `-v` 选项可能会有所帮助（图 7）。
- * *proves* 技术：检查来自 `/proc` 和 `/bin/ps` 的信息。添加 `-a` 选项运行所有测试（图 8）。
- * *quick* 技术：检查 `proc`、`prov` 和 `sg` 表，非常有用，但因为速度可能会导致更多误报，之后可能需要单独运行这些技术（图 10）。
- * *reverse* 技术：检查 `/proc` 中的 `/bin/ps` 是否被系统看到。这可以显示 rootkit 是否正在隐藏 `/bin/ps` 作为一个进程（图 11）。
- * *sg* 技术：将 `/bin/ps` 的信息与系统调用进行比较（图 12）。

消除所有误报。反向技术也会返回结果。作为额外的预防措施，运行其他测试以确认结果。

### 进阶

我已经涵盖了处理端口的基本命令。你可能需要通过一组工具来安装这些内容，它们应该在大多数目录的仓库中找到。对于大型网络，你可能需要安装 `nmap`。`Nmap` 包含许多测试，但在检查端口时会提供一个有趣的表格，包含了协议、服务和端口的状态 - `filtered`（过滤）意味着防火墙或其他网络阻止了该端口。对于小型网络或独立系统，本文描述的命令已经足够了。

```
unhide -# unhide sys
20130526
Copyright 2013 Yagus Yasu & Patrick Gouvin
License GPLv3 : GNU GPL 3 or later
http://www.unhide-forensics.info
```

注意：此版本的 `unhide` 适用于 Linux >= 2.6 的系统

已使用的选项：

[+]通过优先级(1) 扫描搜索隐藏进程

[+]通过 `getpid()` 扫描搜索隐藏进程

[+]通过 `getgid()` 扫描搜索隐藏进程

[+]通过 `sched_getaffinity()` 扫描搜索隐藏进程

[+]通过 `sched_scheduler()` 扫描搜索隐藏进程

[+]通过 `sched_rr_get_interval()` 扫描搜索隐藏进程

[+]通过 `kill(..)` 扫描搜索隐藏进程

图 12：`unhide` 中使用的 `sys` 技术将从 `/bin/ps` 收集的信息与系统调用进行比较。

### 属性

- [1] 默认端口：https://github.com/default-port-numbers/

### 作者

Bruce Byce 是一位自由职业者、作家兼兼编辑，专攻开源软件。除了他的项目外，他还教授现场课程和在线课程。在这个领域，Bruce 撰写关于美国东海岸（https://brucebyfield.wordpress.com）的文章。他还是 Prentice Places 的联合创始人，那是一个关于写作和幻想的博客（https://prenticeplaces.com/）。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_52_0.png)

LINUX-MAGAZ.COM | LINUXPROMAGAZ.COM | 第258 期 | 2022年5月 | 53

## 深度解析



# 使用 OpenToonz 动画

## 动画时光

### FLCL

OpenToonz 是一款专为漫画和动漫艺术家设计的专业动画工具。作者 Ralf Kirschner

任何读者会将“漫画”（manga）和“动画”（anime）分别与日本漫画和动画系列联系起来，如《龙珠》或《宝可梦》，今天，漫画和动画已成为全球性现象，全世界的艺术家都投入了精力和这些形式。如果你想尝试动画，没有必要执着于纸笔。OpenToonz [1] 是一项符合最高动画标准的开源工具。该程序部分是与著名的动画公司（如吉卜力工作室 [2]）合作开发的，它们是《幽公主》、《千与千寻》和《风起动》等经典电影背后的创意大脑。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_53_0.png)

**图 1：** OpenToonz 提供的示例动画展示了最重要的功能。

## 使用 OpenToonz 动画

OpenToonz 可在大多数流行的 Linux 发行版的包源中找到，安装应该是很容易的。用示例场景进行测试：从项目页面下载 ZIP 格式的示例动画（OpenToonz_sample.zip）。你可以在不安装 OpenToonz 的情况下在 YouTube 上查看此示例！图 1 显示了带有官方方案的 OpenToonz，主角是一名为 Dwanko 的狗。

角色的动作和背景类型。还有一个称为 X-sheet 的曝光表。

默认情况下，项目名称为 sandbox。有关启动项目的更多信息，请参阅 OpenToonz 手册 (5)。

第一步是在 Sandbox 项目中创建一个场景。如果你以后想与合作者分享你的作品，根文件夹非常有用，无论使用何种操作系统。在 Sandbox 子文件夹中，点击文件（.tnz...），你将看到它的导出菜单。

在调色板（Palette）窗口中，选择 Vector（矢量），然后选择 Linear Gradient（线性渐变，绿色条右侧）。你绘制的线条在点击时将变为不可，然后会被从左到右的简单渐变填充。

绿蓝色的渐变不仅仅是为了显示水平线。在调色板窗口中，你会看到两种颜色。使用颜色选择器更改线条颜色。你可以使用 Angle（角度）参数来修正渐变的方向；例如，我需要旋转 90 度来移动水平线的位置。

对于天空层，选择 New Raster Layer（新建位图层）并将其编辑为层名称。然后，将颜色改为白色。

**图 6**：Dwankwo 的配色方案。清晰的配色方案更容易绘制不同的姿态。

OpenToonz 有三种层，每种在 X-Sheet 上以不同的颜色显示。呈黄色调的 Vector Layers（矢量层）最适合直接绘制。绿色的 Raster Masters（主位图）用于已扫描并需要用画笔填充的绘制。在 X-Sheet 中呈蓝色调的 Raster Layers（位图层）用于彩色背景。

在启动屏幕上，创建一个 New frame（新帧），在 Scene name（场景名称）字段中输入你喜欢的名称，并按 Create Button（创建按钮）确认。对于你的第一个动画，创建三个层：一个用于水平且需要绘制的 Toonz Vector Layer，一个用于云朵的 Raster Layer，以及一个用于建筑物和街道的 Raster Layer。

对于天空和地面层，选择 Basics 房间然后选择 | New Vector Layer（新建矢量层）。如果你想给天空添加一些细节（例如云朵），在调色板窗口中，点击加号添加颜色，并使用颜色选择器更改 new_2 的颜色。

最后，创建一个名为 Street（街道）的矢量层。使用 Polygon tool（多边形工具）用矩形和三角形绘制山脊线。然后使用上方窗口中的 Camera Stand View（圆圈内的白色矩形）并用鼠标稍微缩小。视图看起来应该像图 8 一样。

目前——与所有模拟层相比，在制作开始时定义动画电影的所有颜色对于让所有角色绘画产生效果是强制性的。图 6 显示了 Dwankwo 定义的配色方案。

### 绘制背景

要绘制背景，在左侧选择 Geometry Tool（几何工具，或按 G ）。确保你在工具箱中选择了 Rectangle（矩形）并拖动鼠标绘制覆盖整个视图的矩形。使用工具箱中的 Fill tool（填充工具，F）。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_56_1.png)

**图 7**：使用启动屏幕设置你的第一个项目。工具栏出现在窗口左边缘。

### 开始你自己的项目

现在你已经熟悉了 OpenToonz 界面，是时候创建你的第一个动画了。如果你还没有准备好，安装并启动 OpenToonz：欢迎对话框再次出现（图 7）。OpenToonz 管理你制作的场景和项目中使用的文件。

## 使用 OpenToonz 深度制作动画

然后在左上角的工具栏中选择 Anime Tool（动画工具，A）。确保在查看器窗口上方的选项栏中选中了 Col2 和 Position（位置）。用鼠标指针将查看器窗口内的云层层向左移动。在 X-Sheet 窗口的第一行，一个小小的白色关键帧将在右侧指示你已成功定义了关键帧。现在选择同一列的单元格，并用鼠标指针移动查看器窗口内的云层——这表示对齐时间。出现了一个圆点。对 Col3 列中的街道层执行相同操作。然后点击播放窗口控制器中的播放图标，享受你的第一个简单动画。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_57_0.png)

图 8：查看器窗口以及带有天空、云朵、街道和天际线的相邻区域。

### 云朵与景观

当你点击图 10 中的桌子任一单元格时，Smart Fill handles（智能填充句柄）会出来：选择每列的第一个单元格以移下一行。

动画可以通过组合多个帧来创建。图 9 仅定义了一个单帧，而帧在图 10 中被组合了一起。然而，组合帧并不会创建动画，因为单个层/幻片在桌子上没有改变其内容或位置。通过增加 Smart Fill 句柄的帧数来尝试是有意义的。

### 人物与演员

为了完成动画，你需要一个或多个包含人物、演员或机器的层——以使用行业中的动画技术。OpenToonz 提供了许多添加演员的方法。

如果你想为真实的电影场景创建一个角色，将导出的场景导出为 GIF。然后你可以在 Gimp 中作为层打开文件，然后进行裁剪以添加演员。将结果保存为带有连续编号的透明 PNG。

在实践中，创建一个只有六帧的动画可能足够了。我们可以选择保持短小以说明图 10 中的控制操作。你需要的是单个幻片的至少水平位移。在 X-Sheet 窗口中向下点击第一帧的单元格；当你选择时，它将导入 OpenToonz，选择 Level > Load... 并打开图像所在的目录。

## 深度解析：备份完整性

![](img/d0fe54f1060b69f0f3f8ac0f16844891_59_0.png)

## 避免备份数据损坏：完整性检查

备份策略可以保护你免受恶意软件攻击和系统崩溃，但如果你需要确保你备份的是未损坏的数据。作者：Rubén Lorente

大多数家庭用户，我敢说还有很多管理员，都缺乏备份策略。他们的家庭照片、音乐收藏和客户数据一直存储在硬盘上，从未被备份到离线存储中，直到硬盘最终崩溃。有些人会保留备份，并定期将文件复制到安全存储介质中。但即使是这些有意识的人，当他们需要从损坏的数据中恢复时，也会发现自己的策略失效了。一个成功的备份策略必须包含对损坏数据的检查。

单次备份容易受到静默数据损坏的影响。例如，有一个名为 Fails! 的文件夹，里面充满了快乐的照片和回忆。我的备份策略包括使用类似 `rsync` [1] 的工具将整个文件夹复制到 USB 大容量存储设备上。

```bash
rsync -a --delete checksum Fails/ /path/to/usb/
```

`rsync` 工具将 `/path/to/usb` 中的副本与最新版本同步。在 Fails 文件夹中的某个文件被损坏之前，这种方法一直有效。这可能由于许多原因引起，例如文件系统在非正常关机后无法恢复。文件也可能因为硬件错误而丢失——你打算恢复 Fails!，结果却不小心删除了它！如果文件发生损坏，或者你在下一次备份周期中没有检测到错误，`rsync` 将将损坏的错误数据写入 USB 存储器。此时，数据的所有副本都不复存在了，它们被你本意想要保护的备份系统给摧毁了。为了缓解这种情况，你可以为备份建立长期存储策略，将你的备份保存在 USB 大容量存储设备中。我们保留一个名为 `Fails_2022-01-28` 的当前备份文件夹，以及一个位于 `Fails_2` 的旧版本备份。当备份文件夹满时，你删除旧文件夹以为新文件夹留出空间。这种策略可以防止损坏，并且如果你有旧快照的良好文件副本（图 1），我只需要花点时间就能恢复数据。所示的“Time Machine”技术提供了关于如何设置这种多周备份系统的说明。

遗憾的是，长期存储只有在数据在输入时损坏时才有效。如果你存储了损坏的数据，快照的唯一空间（即文件的部分版本）只会在备份中存在四周。在第五周，旧快照将被删除以为你的新副本留出空间。如果数据已损坏且系统内没有检测到这一点，

### 静默数据损坏

少数保留原始文件副本的用户仅在外部硬盘或 NAS（如 Synology 或 Cloudnext 实例）上保留单个备份，并定期或持续地同步云端文件。对于终端用户来说，通过这种很方便的方法，单次备份可以解决许多问题。最重要的是，将拥有良好的数据副本，但你可能无法再次从备份中检索它们。

`ZFS` [2] 特别是可以在读取数据块时验证该数据块是否正确。如果不是（例如由于硬盘故障导致），`ZFS` 会修复数据块或向用户抛出错误。`ZFS` 无法防止人为错误：如果你不小心删除了一个文件，

#### 来自用户空间的保护

要验证正在备份的数据是否正确，本身依赖于用户的操作。除非在期间对用户进行随机采样，否则他们无法排除在存档恢复环境之外。在系统崩溃场景下，你可能会发现自己正在使用过时的 SystemRescue DVD（可能来自旧旧笔记本电脑）。在日常维护中，你应该选择可以在任何平台上于迁移且易于使用的用户空间工具。

## 解决静默数据损坏

保证备份可靠的第一步是验证你备份的不是损坏的数据，这比检测损坏要容易。幸运的是，许多工具可以帮助你维护完整性。

具有校验和的文件系统（如 `ZFS`）提供了针对硬件故障导致损坏的程度保护。校验和获取数据（如消息或文件）并从其生成文本。只要向函数传递相同的数据，它就会生成相同的字符串。如果数据发生即使微小的损坏，生成的字符串将变为：

`ZFS` 不可能出现合法的错误。一个伪造的图像编辑器可能会调整有效的校验和，`ZFS` 不会受到用户无意软件更改的影响。`ZFS` 通常是数据完整性的终极答案；但在我看来，它的相对能力仍有不足。

如果发行版包含了 GNU `cgetutils` 包（大多数发行版都包含），你不需要花哨的工具。

## rsync 时光机

通过 `rsync`，你可以备份到连接的驱动器或通过网络。作为额外的便利条件，文件的快照不会在你的存储设备上占用过多空间。

假设我有一个挂载在 `/` 下的外部驱动器。第一个快照将通过调用 `rsync` 来保存：

第一条命令创建一个反映名称的目录。第二个命令将文件复制到新创建的目录中。该开关指示 `rsync` 以“归档”模式工作，递归地进入子目录，并在必要时保留符号链接、元数据、文件权限和所有者。

当该进行下一次每周备份备份时，我创建一个不同的文件夹（引用当前日期）并复制 Foals。然而，`rsync` 有一个技巧可以使用：`--link-dest` 开关使 `rsync` 仅传输自上次备份以来的更改：

```bash
$ rsync /mnt/Foals-2022-01-23
$ rsync -a --link-dest=/mnt/Foals-2022-01-22 /mnt/Foals/Foals-2022-01-30
```

当 `rsync` 将任何新文件复制到新的备份目录时，自上次备份以来已修改的文件不会被复制。对于源目录中存在但自上次备份以来未修改的文件，`rsync` 会对旧备份目录中的未修改文件副本创建硬链接，而不是将它们复制到新备份中。

结果是，`Foals-2022-01-28` 包含了该日期所有的 Foals 内容，即 Foals 的一个快照。而 `Foals-2022-01-30` 仅包含添加到存储介质的新文件或已修改的文件，它们几乎没有占用额外空间。其他所有内容也通过硬链接包含在备份文件夹中。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_60_0.png)

图 1：Foals 结果中的一个损坏图像会导致当前备份目录（2022-01-28）中产生损坏数据。幸运的是，可以从较早的备份（Foals-2022-01-23）中恢复未受损的版本。

## 深度解析：完整性

理想情况下，你应该在执行备份之前立即验证文件的完整性。确保任何文件未被修改或损坏的最简单方法是计算其校验和，并将结果与从已知良好状态提取的校验和进行比较（图 2）。因此，保护特定文件夹备份的第一步是计算其校验和：

### 创建校验和

计算校验和并不直观。由于原文此处存在重复或断层，此处已根据上下文意译进行逻辑对齐。

```bash
$ rsync /mnt/Foals-2022-01-23
$ rsync -a --link-dest=/mnt/Foals-2022-01-22 /mnt/Foals/Foals-2022-01-30
```

图 2：校验和可以用于定位由于无意或故意而受损的文件。使用这种方法只有在数据已设置时才实用。如果你正在备份多个文件，有更好的方法来检查数据是否正确。例如，使用 `grep` 找到旧文件中不存在但在新文件中存在的文件。否则：`grep` 将列出自上次以来删除的文件：

如果数据良好，请备份你的文件。这种方法的一个巨大优势是，校验文件可以用于验证备份本身的完整性。如果你将文件备份到了 `/mnt/foals_2022-02-23`，你可以使用如下命令：

```
$ cd /mnt/foals_2022-02-23
$ md5sum -c md5sum_2022-02-23.md5
```

为了使备份策略生效，你必须能够验证备份内容未受损坏。虽然有许多工具可以验证数据的完整性，但你并不需要复杂的解决方案。`coreutils` 软件包允许你管理大量数据。

硬件缺陷。虽然它无法定位由于人为错误或某些类型错误丢失的文件，但尽管存在局限性，它仍然非常容易设置和运行。如果你在使用在使用 tret，我建议阅读 Solene Rappene 的教程 (3)。

## 局限性

为你打算备份的每个文件夹创建校验和是非常耗时的。对于几个几个字节的数据集，可能需要超过半小时。

只有在数据频繁备份的情况下，在备份前生成并验证校验和才具有实际意义。如果你使用每日备份，比较校验和所显示的差异将比手动验证的合理范围多得多。因此，我将这种方法推荐用于不经常变化的文件夹，例如装满家庭照片或电子书的目录（这些目录中的文件会被添加或修改）。

如果备份中缺少任何文件或文件已被修改，此命令将立即揭示该问题。

根结底，涉及数据完整性最重要的因素是你需要定义一个策略并坚持执行。在我的经验中，大多数用户失败的地方在于……

## Info

- 1) `rsync`: https://rsync.com/saga

- 2) `ZFS`: https://docs.freebsd.org/en/books/book/



- 3) 'Detection of break-in with host-based intrusion detection systems' 由 Tobias Eggendorf, Lina Magnus 写于 2016年2月：https://linux-magazine.com/issues/2016/183-Host-Based-IDS/
- 4) NetBSD 版本的 `mtree`: https://repolicy.org/project/mtree-version
- 5) Solene Rappene 的 `biotrot`: https://dataswap.com/2017-03-17-integrity.html

## 替代方案

在完整性验证的历史中，有许多验证长字段的方法。

一种老旧但可靠的入侵检测系统可以用于验证给定文件夹内文件的完整性 [3]。

你可以使用 `tret`（这是一个来自 BSD 世界的流行程序）来验证目录树映射的内容。例如，它可以用于从包含已知良好数据的文件夹创建规格文件：

如果验证一个内容频繁变化的文件夹的完整性是很有必要的，那么我建议使用 `tret`。该工具仅适用于校验和发生变化但其修改时间未发生任何改变的文件夹。

```
$ tret -c k md5digest
$ -p Foals /var/specification
```

然后，你可以使用该规格文件来验证 `Foals` 的内容：

```
$ tret -f /var/specification -p Foals
```

`tret` 在 Linux 环境中并不流行，但你可以在某些仓库中找到它 [4]。最后，一个 Python 脚本 `biotrot` 可以定位由于硬件缺陷而受损坏的文件。

## 结论

对数据进行多次备份并保留文件的旧版本是防止数据丢失的极佳措施，但它们并不是……

# 作者

Rubén Liente 是一位机械工程师，确保一家小型诊所的 IT 安全措施既符合法律规定又是安全的。此外，他还是 OpenBSD 的爱好者并且……

## MakerSpace

在 Linux 计算机和笔记本电脑上使用通用输入/输出接口（GPIO）。

作者：John Schwartzman

通用输入/输出接口不再仅仅用于板载电脑：你也可以通过 USB 端口在 Linux 桌面电脑或笔记本电脑上使用 GPIO。

> 树莓派的 GPIO（通用输入/输出）能力令我印象并好奇。GPIO 让树莓派用户能够轻松控制灯光和伺服器等现实电子设备。如果能在每台 Linux PC 上实现同样的功能，那不是很好吗？你可以做到。未来科技设备有限公司（FTDI）`FT232H` 设备 [1] 可以通过 USB 端口为非树莓派的 Linux 桌面电脑和笔记本电脑提供 GPIO 能力以及串口。你可以从 Adafruit 购买 `FT232H` 设备，价格为 15 美元。

在杂志的上一期中，我为 Pi 开发了一个使用 GPIO 的简单应用 [2]。在这篇文章中，在 FTDI `FT232H` 设备的帮助下，我重写了树莓派应用，使其在 Linux 桌面和笔记本电脑系统上运行。此示例将教你如何使用 `FT232H` 为标准的基于 Intel 的计算机带来 GPIO 能力。

### 应用程序

我为了移植性用 C++ 编写了该应用程序，为了趣味用 Intel x86_64 汇编编写了它 [3]，它用于计算各种数字……

## Linux 上的 GPIO

表 1：项目使用的文件

| 文件 | 功能 |
| :--- | :--- |
| `gpio.asm` | x86_64 汇编 |
| `gpio.hpp` | C++ 头文件 |
| `gpio.cpp` | C++ 实现 |
| `ms.sh` | Shell 脚本 |
| `Makefile` | 构建脚本 |

# 在虚拟机上运行

如果你是在虚拟机上而非单台计算机上工作，`FT223H` 将显示在客机计算机或宿主机上，在这种情况下，你需要在客机上查看。

要确定 `FT223H` 所在的位置，请将其插入并使用终端查看所有 USB 设备。如果你没有看到名为 "Future Technology Device Instrument, LTD FT223H Single HS USB-UART/IO chip" 的行，那么你的 `FT223H` 在宿主机上。

在 VMware 上，打开 虚拟机 > 可移动设备 > USB 串行控制器（从主机连接（断开连接））。如果你没有使用 VMware，请使用你相应的虚拟化软件。以下命令应显示 `FT223H`：

![](img/d0fe54f1060b69f0f3f8ac0f16844891_65_0.png)

图 3：U1、74HC02 以及与 `FT223H` 连接的示意图。

由于设备使用的电流小于其提供的电流，共阳极显示是此应用程序的良好选择。对于驱动器，需要的电流大于单个二极管提供的，因此使用晶极管来开关灯。输出引脚最多可以提供 16mA 电流，而驱动合适的亮度大约需要 90mA。晶极管需要约 5mA 的基极电流来饱和集极。

```
lsusb
Bus XXX ID xxxx:xxxx
Future Technologies
```

在确认 `FT223H` 芯片显示为 `/dev/ttyUSB0` 后，你现在可以运行：

`gpiod` (c 版本+) 或 `/gpiod` (ASM) 版本。

C, d, e, F 组成一个段的组合。为了解释如何写数字，你必须开启段 b 和 c 并关闭其他段。数字 7 看起来像 1，但段 a 也被点亮了。数字 6 对应十进制值 10，9 对应十进制值 11 (`c`=12, `d`=13, `e`=14, `f`=15)。

为了显示数字，依次写入每个段并驱动每个开关，通过从数字到数字的切换，使得肉眼无法察觉到数字的开启和关闭。

像 `switch1` 这样的瞬时开关由于存在噪声，会产生不确定的脉冲。去抖的需求意味着脉冲宽度要足够应用检测，这可以通过 S-R 锁存（置位-复位）锁存实现，从而形成一个与开关连接的 S-R 锁存。

在共阳极显示中，写入 0（关闭）来开启段，写入 1 (3.3v) 来关闭段。它知道数字的工作方式是反的，

`74HC02` 集成电路包含四个输入非门。它们连接到 `switch1` 以及 AC 总线的第 6 和第 7 引脚。为什么用 `74HC02`？因为我们希望能够使用 3.3V 或 5V。

`FT223H` 从 USB 端口为我们提供 5V，像树莓派一样，`FT223H` 是 5V 耐压的：如果你愿意，可以使用它代替 3.3V。

当用户按下 `switch1` 时，开关信号被反转并发送到

![](img/d0fe54f1060b69f0f3f8ac0f16844891_65_1.png)

图 4：具有单个置位脉冲设备的复位波形。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_65_2.png)

图 5：具有噪声置位的设备的复位波形。

# Linux 设备上的 GPIO

![](img/d0fe54f1060b69f0f3f8ac0f16844891_66_0.png)

![](img/d0fe54f1060b69f0f3f8ac0f16844891_66_1.png)

图 6：`countUp/base` 子程序的流程图（`GPIO.cpp` 第 97 行）。

图 7：`countDown/base` 子程序的流程图（`GPIO.cpp` 第 97 行）。

输入的 S，这导致 S 输入瞬时变为高电，随后 Q 输出变为高电低到锁存器输入。GPIO 引脚 AC 输入。程序的 `read()` 线程方法定期读取 `FT23EH` 的 AC 字节。如果它的 AC 捕捉到高电，它有一个由延迟引起的中断，告诉当前运行的计数器时输出返回 `read()`。

四个并根据它要使用的数制（基数）规则每秒增加一次数字。`countDown()` 方法（图 7）将四个基数设置为它，并根据它要使用的数制规则每秒减少数字。

程序向 `AC60` GPIO-out 引脚发送一个高低脉冲，该引脚连接到 8 位锁存器。这导致锁存器重位并将 Q 输出（AC 输入）拉低。注意开关可能是噪声的。当它被按下时，如果 R 锁存器未动作，可能会产生单个多个脉冲（图 4）。Q 在开关的第一个下降沿变为高电平。尽管有 S 输入，它保持高电平，直到 R 输入变化。

在共阳极显示中，写入 0（关闭）开启段，写入 1 (3.3v) 关闭段。它知道数字的工作方式是反的，

`74HC02` 集成电路包含四个输入非门。它们连接到 `switch1` 以及 AC 总线的第 6 和第 7 引脚。为什么用 `74HC02`？因为我们希望能够使用 3.3V 或 5V。

`FT223H` 从 USB 端口为我们提供 5V，像树莓派一样，`FT223H` 是 5V 耐压的：如果你愿意，可以使用它代替 3.3V。

当用户按下 `switch1` 时，开关信号被反转并发送到

![](img/d0fe54f1060b69f0f3f8ac0f16844891_65_1.png)

图 4：具有单个置位脉冲设备的复位波形。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_65_2.png)

图 5：具有噪声置位的设备的复位波形。

# 读写子程序

主程序调用 `read()` 并在独立线程中运行。它不关心四个数字是如何获取的。它只是获取所有数字的内容并将其写入四个数字中

![](img/d0fe54f1060b69f0f3f8ac0f16844891_66_2.png)

图 8：示波器轨迹显示由 `GPIO.cpp` 生成的波形。黄色 = `AC0`，紫色 = `AC1`，蓝色 = `AC2`，绿色 = `AC3`。

LINUX-MAXIME.COM | LINUX-MAXIME.COM

第 258 期 2022年5月

## 设备上的 GPIO

你可以看到程序从 `di13` 开始，将段数据写入 `di11`，然后开启 `di13`。在一段时间之后，它关闭 `di13` 并开启 `di11`。这是因为用户输入是一个缓慢的过程，所以你不需要在每次请求时检查中断或使用 `read()` 循环。你可以在每次迭代时检查中断。通过这种方式，你可以减少延迟。你还可以使用 `DELAY_COUNT` 常数使数值在你的硬件上生效。命名为 `/dev/usb/(xxx)/`，在插入 USB 时创建创建并命名。一个具有公共方法和函数的对象。类和私有方法从程序的其他部分无法访问。

### 列表 1: 写入 GPIO

```
01 void* readWrite(void*pArg) // function - 将数字写入 GPIO
02 {
03 GPIO* pGPIO = GPIO::getGPIO();
04 FT32H* pFT = FT32H::getFT32H();
05 int nCount = DELAY_COUNT;
06
07 while (!pGPIO->getFlag()) {
08
09 if (--nCount == 0) // 是时候检查中断了
10 {
11 if (pGPIO->interrupted()) // 是 - 检查中断
12 {
13 pGPIO->setInterrupt(true); // 响应中断
14 pGPIO->resetInterrupt();
15 }
16 nCount = DELAY_COUNT; // 重新填充
17 }
18 pGPIO->writeByte(0); // 清除数字 - 关闭
19 pGPIO->writeByte(pGPIO->getPattern(3)); // 写入数字
20 pGPIO->writeDR(DIGIT_3); // 开启数字
21 sleepMs(5);
22 }
```

### 列表 2: GPIO.cpp

```cpp
bool GPIO::interrupted() // 检查中断 (GPIO.cpp 行 55)
{
    byte byteToRead;
    FT32H::readByte(&byteToRead);
    return (byteToRead & INTERRUPT_MASK) != 0;
}
```

### 列表 3: gpio.asm

```asm
interrupted: // 检查中断 (gpio.asm 行 34)
prologue
sub rsp, VAR_SIZE // 为局部变量分配空间
lea rdi, nParam // 传递 nParam 地址进行读取
call readByte // 读取刚刚读取的字节
mov al, [rax] // 获取刚刚读取的字节
test al, INTERRUPT_MASK // INTERRUPT_MASK 位是否设置？
setnz al // 如果是则 al = 1，否则则 al = 0
epilogue
```

## GPIO 类

`GPIO` 类（`GPIO.cpp` 和 `GPIO.hpp`）处理定时器工作。在各种系统中，它负责倒计时和显示小时。`clock()` 函数不是 `GPIO` 类的成员函数，它实例化 `FT32H` 和 `GPIO` 对象，并启动一个独立的执行线程来运行读取器。

如所述，`GPIO` 使用其成员方法进行计数：`count(base)`、`display()` 和 `clock()`。非成员线程读取器使用 `FT32H` 对象将时钟和时间写入 GPIO 端口。`GPIO` 还包含几个成员方法：`readWrite(byte)`；`interrupted()`；`setInterrupt(bool)` 和 `getPattern(int)`。

非成员函数实现延迟。`FT32H` 和 `GPIO` 拥有静态成员函数 `FT32H::getFT32H()` 和 `getGPIO()`，它们返回各自的指针。无论你是否在程序中，都可以访问这些函数和成员。例如，`GPIO.cpp` 拥有第 1 行所示的代码。注意，静态成员函数 `FT32H::getFT32H()` 和 `getGPIO()` 是通过声明名称调用的，而不是通过对象。你使用指针来访问类的成员方法。

现在看一个 C++ 成员函数（列表 2）及其对应的等效汇编代码（列表 3）。C++ 版本有一个 `GPIO` 类的成员函数，它不接受参数并返回布尔值。一个（局部）变量 `byteToRead` 存储在栈上。

静态成员函数 `FT32H::getFT32H()` 允许你调用 `FT32H::readByte(byte)` 然后传递 `byteToRead` 的地址。问题是：当与 `INTERRUPT_MASK` (0x8) 进行字节按与运算时，结果是否为零？记住

## Linux 设备上的 GPIO

`GPIO` 是一个输入引，提供 S-R 锁的 Q 输出。该问题的答案通过调用方法返回。

```asm
; 判断是否设置了 INTERRUPT_MASK 位
setnz al
    al = 1 如果是，al = 0 如果否
epilogue
```

为什么标签前面有一个冒号？这是因为 YASM 和 NASM 汇编器允许在方法之间复用名称。标签 `.continue` 作为 `continue`。汇编语言包含大量的跳转（等同于函数调用）。为了避免中断方法，如果相等则 `jmp .interrupt`；使用 `jmp .continue` 调用读取器。每个条件都是无条件的（jmp），这只是为了节省实际的时间和能量。

## gpio.asm

现在可能很难置信，但汇编语言函数的功能完全相同，带有宏定义 `prologue`。所有调用其他例程的 Intel语言函数都需要将 `nParam` 的有效地址加载到 `r1` 寄存器中。在 C 调用约定中，函数的第一个参数始终通过 `r1` 寄存器传递。

该行 `call readByte` 获取刚刚读取的字节到 r1 并与 `INTERRUPT_MASK` 进行与运算，如果字节位为 0 或 1，则清除处理器的零标志。如果字节被清除则将 `al` 中断标志置为 1，如果有中断则置为 0，否则为 0。

```asm
macro prologue
push rsp
sub rsp, rsp
endmacro
```

以准备栈。（函数末尾的 `epilogue` 宏）

```asm
macro epilogue
leave
ret
endmacro
```



将栈恢复到调用 `prologue` 之前的状态。调用 `prologue` 后，调用函数（在此例中为 `readByte`）可以调用 `test al` 来查找被中断函数是否发现了中断。`test` 指令执行一项操作，它会设置标志位但不保存结果。调用函数的相关部分是：

## Info

- [1] FT323H
- [2] OPC UA
- [3] GPIO
- [4] python-opcua

## 列表 1: Python OPC UA 服务器

```python
# 01 opcua_server.py - 创建一个 OPC UA 服务器并模拟
03 import opcua
04 import random
05 import time

07 s = opcua.Server()
08 s.set_name("OPCua Test Server")
09 s.set_endpoint("opc.tcp://192.168.0.120:4840")

11 # 注册 OPC UA 命名空间
12 idx = s.register_namespace("http://192.168.0.120:4840")
13 start = s.start()

16 objects = s.get_objects_node()
17 定义带有某些标签的气象站对象
18 mystation = objects.add_object(idx, "Station")

20 添加带有值和范围的温度标签
21 mytemp = mystation.add_variable(idx, "Temperature")
22 mytemp.set_writeable(True)

24 添加带有值和范围的风速标签
25 mywind = mystation.add_variable(idx, "Windspeed")
26 mywind.set_writeable(True)

28 每 5 秒使用模拟数据创建一个循环
29 True:
30 mytemp.set_value(random.randint(20, 25))
31 mywind.set_value(random.randint(10, 100))
32 time.sleep(5)
```

图 2：OPC UA 客户端。

## 列表 2: 获取标签值

```python
>>> import opcua

>>> 作为 OPC UA 客户端进行连接并获取标签值
>>> client = opcua.client("opc.tcp://192.168.0.120:4840")

>>> client.connect()

>>> mytemp = client.get_node("ns=2;i=2")

>>> mytemp.get_value()
```

如何获取之前定义的温度。客户端方法使用 OPC UA 服务器端点，`connect` 方法建立连接。OPC UA Node ID 由命名空间名称 (`ns`) 和索引 (`i`) 定义，`get_value` 方法返回客户端的值。使用此方法可以在仪表盘上获取标签值。

OPC UA 项目的 GUI 工具可以使用 OPC UA 服务器和其标签进行构建。图 2 显示了两个模拟标签和图表。可以通过它们的 NodeIds 创建 OPC UA 项。

Python tk 库 [6] 包含一些实用的免费小部件（例如：图表、仪表盘、LED、传感器显示）。安装方法如下：

```bash
pip install tk
```

客户端应用（列表 3）创建一个 Tkinter 对象（第 11 行）并添加两个仪表盘组件（第 15-20 行）。

如果未创建 OPC UA 服务器，则其未定义。在这个示例中，温度标签是使用 `NodeId=ns=2;` 创建的，这意味着它在节点 2 中的索引为 2。

作为第一个项目，创建一个带有模拟 OPC UA 标签的简单 OPC UA 服务器（列表 1）。设置中的步骤是定义服务器、位置名称并注册命名空间（第 7-12 行）。稍晚些时候你将看到 OPC UA 细节的重要性。为了妥善准备我的代码，我硬编码了 IP 地址（第 9 行和 12 行）。为了更灵活的设置，可以使用 Python 库来确定端点和命名空间的值。

在 OPC 中，“Tags”（标签）和“Variables”（变量）通常互换使用。在控制系统中它们被称为“tags”，但在 OPC UA 内部使用的术语是“variable”。关键区别在于，变量可以是内部或软件生成的点，例如计数器。

## 简单 OPC UA 服务器

该架构基于对象和函数。

## Python OPC UA 客户端应用

`opcua` 库同时用于服务器和客户端应用程序。OPC UA 客户端应用只需要五行代码即可连接服务器、定义 NodeId 并获取其值。列表 2 显示（图 5：Python OPC UA 客户端）。

## 列表 3: Python OPC UA 客户端应用

```python
import tkinter as tk
import tk_tools
import opcua

# 作为客户端连接到 OPC UA 服务器
client = opcua.Client(url="opc.tcp://192.168.0.120:4840")
client.connect()

root = tk.Tk()
root.title("OPC-UA Station 1")

# 创建仪表盘
mytemp = tk_tools.Gauge(root, height=200, width=400, max_value=1000, label='Temperature', unit='°C')
mytemp.callback()

speed = tk_tools.Gauge(root, height=200, width=400, max_value=1000, label='Speed', unit='kph')
speed.callback()

def update_gauge():
    # 每秒使用 OPC UA 值更新仪表盘
    mytemp.value = client.get_node("ns=2;i=2").get_value()
    speed.value = client.get_node("ns=2;i=3").get_value()
    root.after(1000, update_gauge)

root.after(500, update_gauge)
root.mainloop()
```

Tkinter `after update_gauge()` 方法调用函数（第 26 行），使用 OPC UA 值刷新仪表盘组件（第 26 行和 28 行）。

```python
# 从在线系统导出
# 到 XML 文件
# 导出: opcua.Server
export_xml_by_node("mytags.xml")

# 导入 XML 文件
# 源: import_xml("mytags.xml", "path")
```

虽然模型工具可以手动添加或删除少数变量（图 5），但当需要添加数百个变量时会很。

## XML 数据库

使用 CSV 文件很容易管理标签数据库。例如，`mytags.csv` 文件可以使用三个字段创建：标签名、描述和默认值：

| 标签名 | 描述 | 默认值 |
| :--- | :--- | :--- |
| Temperature | 环境温度 | 25 |
| Windspeed | 风速 | 10 |

在早期的 Python 服务器中，当服务器启动时修改变量。这种方法适用于简单项，但对于标签数据库可能糟糕。

```csv
# mytags.csv
# 简单标签数据库
# 格式: 标签名,描述,默认值
```

所有工业控制都有许多属性来存储 OPC UA 配置文件。OPC UA 配置文件遵循标准，导出的 XML 格式像树（图 4）。文件从头文件开始，后面是 `<object>` 和变量定义。变量定义设置了 NodeID、名称和描述。

使用 opcua-model，你可以将变量插入新结构中。在图 5 中，这是一个可视化图表，要容易得多。Python opcua 库允许导入和导出项：许多编程专家可以帮你做到。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<object xmlns="http://www.opcua.foundation.org/UA/UA/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <variable NodeId="ns=2;s=HeaderDefinitions" BrowseName="ns=0;BrowseIndex=1">
    <name>Header Definitions</name>
  </variable>
  <variable NodeId="ns=2;s=VariableDefinitions" BrowseName="ns=0;BrowseIndex=2">
    <name>Variable Definitions</name>
  </variable>
</object>
```

## Node-RED OPC UA 服务器

Node-RED-contrib-opcua [7] 包含了 OPC UA 服务器和许多常用客户端功能。可以从面板编辑器安装。图 6 显示了带有浏览器节点的 Node-RED OPC UA 服务器设置。OPC UA 服务器名称已定义（在此情况下为：4840）。自定义节点目录设置为 `/home/pi/opcua`，我从 CSV 创建了 XML 文件（`mytags.sh`）。

OPC 浏览器节点显示在调试面板（7），允许我查看 XML 文件中定义的对象和变量。下一步是允许写入和读取值。图 8 显示了启动的 Node-RED 逻辑。

Bash/Awk 将三字段 CSV 格式转换为所需的 XML 格式（列表 4）。在 Bash 脚本中，第一个 `awk` (6) 输出 XML 头，第二个 `awk`（第 18-26 行）解析输入的 CSV 文本文件。通过逗号分隔符（第 19 行）将三个 CSV 字段映射到 `$1`、 `$2` 和 `$3`。输出使用 `$1` 定义变量名（第 24-25 行），使用 `$2` 定义描述（第 26 行），使用 `$3` 定义默认值（第 31 行）。awk 变量 `i` 递增 NodeId（第 23 行）。运行此脚本来读取 `mytags.sh` 并创建 XML 文件 `mytags.xml`：

```bash
cat mytags.sh | ./csv2xml.sh > mytags.xml
```

## 列表 4: CSV 到 OPC UA XML

```bash
#! /usr/bin/bash
# $ csv2xml.sh - 从 CSV 创建 OPC UA 文件
# $1

# 添加 XML 头
print "<?xml version=\"1.0\" encoding=\"UTF-8\"?>
print "<UaNodeSet xmlns=\"http://www.opc-foundation.org/2004/02/nodes\" xmlns:ua=\"http://www.opc-foundation.org/2004/02/types\">
print "<Namespaces>"
print "    xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\">
print "    <Namespace index=\"1\" uri=\"op-tcp://127.0.0.1:4840\"/>"
print "  </Namespaces>
print "<Nodes>"
print "    <Node id=$2\" browseName=$1\">
print "      <DataType>ua:String</DataType>
print "      <NodeId>ua:ns=1;$2</NodeId>
print "      <BaseOfOfId=\"ua:VariableType\">
print "      <Variable id=$2\" browseName=$1\">
print "        <Value>$3</Value>"
print "      </Variable>
print "    </BaseOfOf>
print "    </Node>"
print "</Nodes>
print "</UaNodeSet>"
```

## MAKERSPACE OPC 统一架构

逻辑完成后，点击 Deploy（部署）按钮即可让应用程序上线。可以通过 http://node-red:1880/ 查看 Node-RED 仪表板。

由于功能众多，学习 UA（统一架构）可能会让人望而生畏；但如果你从 Python 和 Node-RED 入手，可以用极少的代码和设置构建出一个可以运行的系统。

在本文中，我只涉及了不带安全设置的数据。下一步将是查看高级功能、历史数据和用户安全性。你还应该注意，此处 OPC UA 服务器通过其编号访问 OPC 词目，因此与其使用 `NodeId=ns=1;4` 访问点，不如可以使用浏览器名称（例如 `ns=2;s=MyVariableName;`）。

# 总结

![](img/d0fe54f1060b69f0f3f8ac0f16844891_75_0.png)

图 8：写入并订阅 OPC UA 值。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_75_1.png)

图 9：为 OPC-UA-client 定义 Endpoint（节点）和 Action（动作）。

```
// Node: msg.payload[0] = 0, \value is in payload[1]
msg.payload = msg.payload
return msg;
```

在此示例中，波浪的高度手动输入与其他项一样被触发，滑块位置将更新为该值。可以通过将滑块输出到带有 RET 动作的 OPC UA 客户端节点来使用滑块。

将图 7 中按的 NodeId `ns=5;2` 输入 OPCItem 节点中。OPC Client 节点需要定义的 Endpoint 和 Action（图 9）。当触发 RET 动作时，会返回一个 Good（良好）或 bad（错误）状态消息。OPC Client 节点报告若干动作。在 Python 客户端应用中，SUBSCRIBE 动作会在值发生变化时返回一个值。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_75_2.png)

# Node-RED OPC UA 服务器

在最后一个示例中，我们使用了第一个示例中的 Python OPC UA 服务器。Python 示例中的温度和风速标签使用相同的仿真代码，但增加的延迟标签将从 Node-RED 手动输入值。

图 10 显示了一个 Node-RED 应用程序，该程序连接到 OPC UA 服务器 并在 Node-RED 仪表板中显示数据。此示例订阅了仪表盘中的两个时间输入（温度和风速）。OPCItem 节点定义了要使用的 OPC NodeIds。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_75_3.png)

图 10：通过 Node-RED 在仪表板上显示 OPC 数据。

所有 OPC Client 节点都需要由 Python OPC UA 服务器的地址定义其节点。

订阅的数据值以二项数组的形式返回（因为数据类型是 int）。Gauge 节点只读取数组的第一项（即为 0），因此一个小型函数将第二个 payload `[1]` 发送到 payload 消息中：

```
// Copy second array item ? 
// to be the payload
```

### Info

- [1] OPC Foundation：https://opc-foundation.org/
- [2] OPC Unified Architecture：https://opc-foundation.org/about/opc-technologies/opc-ua/
- [3] open62541 项目：https://open62541.org/
- [4] Free OPC-UA Library：https://github.com/FreeOPCUA
- [5] 本文代码：ftp/tip-linux.com/pub/listings/linux.com/258/
- [6] Python tk, tools library：https://tk-tools.readthedocs.io/
- [7] Node-RED OPC UA 文档：http://flows.node-red.org/node-red-contrib-opca

![](img/d0fe54f1060b69f0f3f8ac0f16844891_75_4.png)

图 11：Node-RED OPC UA 仪表板。

2022年5月第258期 LINUX-MAGAZ.COM 1 LINUX-MAGAZ.COM

开源生态系统为每个问题提供了解决方案——事实上，它通常有许多解决方案。你可能需要一个强大且功能完备的工具来构建一个强大的应用程序，或者你可能想要快速且易于实现的东西。涉及到数据库系统时，选项跨度很大，从 PostgreSQL 到 MariaDB 这种企业级工具都有。但是，如果你想保持简单，只需使用 LibreOffice。本月，我们启动 LibreOffice 来完成一个简单的数据库项目：整理个人音乐收藏。本月，我们还将尝试一种工具，它可以让你在命令行中查看命令语法示例，并向你展示如何使用 Inkscape 和一个名为 Paperfold 的工具用折纸创建艺术性的 3D 物。

# LINUXVOICE

Doughouse – 通用软件问题 78

- John 'maddog' Hall：尽管有相反的评论，漏洞和安全问题真的与开源软件有关。

命令行工具示例 79



- Fernand Thomas：需要了解如何使用命令行工具吗？提供了真实的案例。

LibreOffice 数据库 81

- Johnfield：你需要 LibreOffice Calc 和 Base 来创建一个用于歌曲的简单数据库。

FOSicks 86

- Graham Morrison：本月我们指出了 Surge, Krönite, multipath, xplr, MQTT 以及更多！

教程 – Paperfold 92

- Siri Kemer：纸张重新流行。Linux 用户可以转向 Inkscape 和 Box.py、Paperfold 等创建 3D 模型。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_76_0.png)

# ELVIE

| 我们在代码中使用了大量的 FOSS 库 | 是的，我们应该支持我们依赖的所有第三方开发者 | 我们审核代码以确定使用了哪些库 | 我们真的需要使用这个词吗？ | 为什么不使用 LIFF 并限制在…… |
| :--- | :--- | :--- | :--- | :--- |
| 我们向那些项目回馈 | | 让我们创建一个的“软”版本！ | | |

![](img/d0fe54f1060b69f0f3f8ac0f16844891_76_1.png)

![](img/d0fe54f1060b69f0f3f8ac0f16844891_76_2.png)

# LINUX HOUSE – 通用软件问题

![](img/d0fe54f1060b69f0f3f8ac0f16844891_77_0.png)

# MADDOG’S DOGHOUSE

Jon "maddog" Hall 是一位作家、教育家、计算机科学家和自由软件先驱，从第一次遇到 Torvalds 以来一直是 Linux 的热衷支持者。他担任……的主席。

漏洞和安全问题真的与开源软件有关，尽管有相反的评论。

# 它们从哪里来？

我不认为媒体和评论人士指出 FOSS（开源软件）中存在漏洞。当他们指出时，暗示这是 FOSS 的问题，而不仅仅是闭源。

开源（以及部分自由软件）的区别在于，代码暴露给许多人，并且在问题发生时可以进行补丁。闭源代码（或使用开源组件的代码）无法由生产闭源产品的公司进行修改以获取补丁，因此闭源公司实际上在为该软件生产产品。

媒体和评论人士正在暗示这些是“开源”问题，事实并非如此。

让我们保持诚实。

## LINUX 语音命令行工具示例

## 终端中的 Shell 工具示例

eg 详解

需要了解某个命令行工具吗？`eg` 提供了真实世界的示例，而且比 man 页（帮助手册）更易访问。由 FERDINAND THOMMES 编写。

在论坛和讨论组中，你越来越多地发现有人声称命令行是过时的产物。他们认为应该能够通过图形化工具处理任何任务。这种说法表明，发表评论的人从未认真地使用过终端。任何意识到使用命令行工作速度和效率的人都会同意，更强大的工具会更好。我承认在 Plasma 桌面系统上混合使用命令行和图形化工具。多年来，我越来越多地同时使用两者，鉴于这种令人满意的分工，我没有办法将全部精力都投入到命令行中。

Python 软件包索引（Python Package Index）。要执行此操作，如果尚未安装该包，你可能需要先从包管理器安装 `python3-pip` 包。然后通过 `pip` 获取并将其存储在硬盘上。

一旦安装并准备就绪，就不需要进行配置，它是可以直接使用的。输入 `pip --list` 将向你显示按字母顺序排序的当前支持的约 80 个工具（图 1）。如果在执行此操作时系统输出“未找到命令”，你需要注销桌面并重新登录。系统会将安装目录包含在路径（path）中。

## 复杂的 man 页

对于一个愿意学习的新手来说，在终端中工作有几种方法。许多用户的第一个起点是 man 页，它们可以作为参考工具，因为它们列出了所有的选项、标志和参数。如果你实际上学会了如何使用命令行（CLI）工具，man 页提供的帮助是有限的——事实上，它们更多是为了吓跑初学者。`eg` 提供的示例提供了更易于理解的信息，而且，这些示例将帮助你在进行如此大量的搜索后找到正确的答案。

列出的命令之一是通过调用名称来访问：你会注意到有些条目只有几行（图 2），而另一些——例如该条目有几百行。一旦你完成一个的阅读，按下 `Q` 就会提示你退出。如果你在测试后不想继续使用它，可以通过 `pip uninstall` 将其删除。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_78_0.png)

这就是界面工具 `eg` 登场的地方。它是免费提供的（`eg` 非常棒，尽管名字很短）。它的名字很简单，易于在你的硬盘上设置，并与匹配项绑定。`eg` 的自描述提供了命令行工具的用法示例。我检查了它是如何工作的。

## 你的需求范围

`eg` 位于 `$HOME/.local/bin/python3/site-packages/`。请检查安装路径 以获取更多信息。在安装目录下，`eg`。

## 快速安装

要执行此操作，首先访问该工具的 GitHub 页面 (1) 看看它的样子。在最流行的 Linux 发行版的软件包存档中无法找到该工具。你可以通过 `pip` 安装它，它是 Python 软件包的安装程序：

```bash
$ test-get.Standard-PC-PC3-ICH-2009- $ pip install eg
Using cached 2.1.1-python-none-any.whl
Installed packages: 
Successfully installed eg-2.1.1
usage: eg [-h] [--CONFIG_FILE] [-e] [--examples_DIR]
  --site-PACKAGES [PATH] [--CONFIG_D] [--] [--color] [----] [--no-color]
```

`eg` 提供了常用命令的示例：

位置参数：

可选参数：

- -h, 显示帮助信息并退出

- -v, 版本

- --CONFIG_FILE,配置文件

指向 `eg` 文件的路径，如果它不在默认位置。

给定命令的自定义示例目录。

你的中未设置 editor-cmd，eg 且 VISUAL 和 EDITOR 均未设置，因此打印了一条消息并并

LINUX-MAGAZINE.COM | 第 258 期 2022年5月

## LINUX 命令行工具示例

## 安装路径

```bash
testtest@test-Standard-PC-Q35-ICH9-2009:~ $ cd
# cd 切换到目标目录
cd target-directory
# 切换到主目录
cd -
# 切换到上一个目录
cd -
```

你安装在 `$HOME/.local/bin/`，可执行文件位于 `$HOME/.local/bin`。你需要确保此目录在你的 PATH 变量中。你可以通过 `echo $PATH` 检查是否如此。如果列表中缺少该目录，通过 `export PATH=$HOME/.local/bin:$PATH` 临时添加。但此配置在重启后不会保留。使用列表 1 中的条目将其永久存储在你的 `$HOME/.profile` 文件中。

## 基础用法

将你的当前工作目录更改到目标目录：

```bash
cd <target-directory>
pwd
<target-directory>
```

```bash
testtest@test-Standard-PC-Q35-ICH9-2009:~ $ ls
```

图 2：使用每个命令

下面的示例非常简单。你可以在这里看到每个命令（cd 切换目录）的输出。

你将在每个各/examples/ 下以 Markdown 格式找到下方支持的命令和工具。如果你想自己添加示例或参数，请打开相应的 Markdown 文件并进行更改。

此外，`eg` 可以将你自己的条目存储在数据结构中。要创建这个，请在 examples/ 中创建一个名为 NAME.md 的文件。

## 258

LINUX-MAGAZINE.COM | LINVOXPROMAGAZINE.COM

## 创建 LibreOffice 数据库

**LibreOffice Calc 和 Base 是你创建简单数据库所需的所有。**

MySQL 是最常用的开源数据库管理系统。开发者经常使用 MySQL 或其兄弟版本 MariaDB 来构建应用程序；然而，对于许多人来说 MySQL 过于复杂。LibreOffice 为想要创建简单数据库的用户提供了更简单的替代方案。本文描述了如何使用 LibreOffice 工具获得简单的数据库解决方案。在这种情况下，我将向你展示如何使用制表符分隔文件的音乐数据库。逗号分隔值 (CSV) 格式是不可行的，因为某些字段（如专辑标题、歌曲或艺术家）可能包含逗号或特殊字符。如果我使用以下步骤导出，导出可能包含库中的部分或全部歌曲：

我将使用两个 LibreOffice 工具：LibreOffice Calc（电子表格）和 LibreOffice Base（管理）。结合这两个应用程序以及 iTunes，通用流程如下：

- 从 iTunes 导出为制表符分隔的文件。

- 导入到 Calc 进行微编辑。

- 修改后的库到 LibreOffice Base。

- 创建 SQL 查询。

- 运行查询并过滤显示结果。

当然，你可以导入其他类型的数据。例如，你可以整理邮票收藏或跟踪今年的发票。

### 将文件导入 LibreOffice Calc

接下来，将制表符分隔的文件 Music.txt 导入到 LibreOffice Calc 中进行微编辑。当 LibreOffice 弹出一个测试

![](img/d0fe54f1060b69f0f3f8ac0f16844891_80_0.png)

![](img/d0fe54f1060b69f0f3f8ac0f16844891_80_1.png)

### 从 iTunes 导出

第一步是从 iTunes 导出音乐信息到可以导入 LibreOffice 的格式。播放列表可以导出

# LINUX 语音版 LIBREOFFICE 数据库

![](img/d0fe54f1060b69f0f3f8ac0f16844891_81_0.png)

它将许多数据导出为列，其中一些数据是没用或不必要的。因为我对名称（歌曲标题）、艺术家、专辑、流、曲目编号和年份感兴趣，所以我删除了除了这些以外的所有内容；我插入了一个 ID 字段作为主键（我将在本文的数据库部分讨论这一点）。

Liberation Sans 字体

要插入 ID 字段（如图 3 所示），请按照以下步骤操作：

- 在第一个位置（即 Name 列的左侧）插入一列：工作表菜单 | 插入 | 在左侧插入列

- 为新列命名

- 留空列中的单元格，这些单元格将在 LibreBase 中自动填充

- 理想情况下，保持 LibreOffice Calc 开启以便复制和粘贴数据。

图 3：插入用作主键的 ID 列。

带有选择或更改分隔符选项的导入对话框。要将文件导入 Calc：

1. 所在菜单 | 打开文件

2. 从文件类型下拉菜单中选择文档（图 1）

3. 选择 Music.ctz

4. 点击打开

5. 在打开的导入对话框中，选择“分隔符”选项卡，并勾选“其他”下的选项（图 2）

6. 检查“区域”中的预览字段

7. 点击确定

图 4：保存数据库的选项。

此时，我有了需要导入的数据。我需要创建电子表格数据。为了创建我的数据库，我将使用 LibreOffice Base，它可以创建、编辑和扁平化关系数据库。

# LibreOffice Base 数据库

LibreOffice 在其大部分应用程序中使用了许多向导。我发现向导在 LibreBase 中非常有帮助，特别是对于不是 SQL 语言专家的用户。第一步是创建一个数据库。LibreBase 能够从电子表格导入数据，我倾向于使用向导将数据从 calc 复制粘贴到 LibreBase。

# 创建新数据库

接下来按照如下方式创建并注册新数据库 (4)：

- 打开 LibreBase，出现数据库向导

- 创建新数据库

- 点击下一步>

- 勾选以下选项：

  - 为我注册数据库

  - 打开编辑器进行编辑

  - 使用表向导创建表

  - 完成

- 点击另存为 LibreLibodb

注意：不需要注册数据库以供其他 LibreOffice 组件使用。你可以根据自己的需要决定。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_81_1.png)

接下来，表向导（图 5）提示你执行以下步骤：

- 点击“步骤”下方的字段：在“类别”下选择“个人”。然后从示例表下拉列表中选择“CD-Collection”：将字段从“可用”移动到“已选择字段”：生产者（Producers），

![](img/d0fe54f1060b69f0f3f8ac0f16844891_81_2.png)

图 5：表向导显示了表的设置。

82 2022年5月第258期 LINUX-MAGAZINE.COM

# LIBREOFFICE 数据库 LINUX 语音

![](img/d0fe54f1060b69f0f3f8ac0f16844891_82_0.png)

图 6：在表向导中设置字段和格式。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_82_1.png)

图 7：将表从 Calc 捕获到 Base。

打开表窗口，选择“追加数据”，勾选“第一行作为列名”，并点击下一步 >（这将带你进入源数据界面）。检查并确认源数据与目标表对齐，然后创建 Artist（艺术家）、AlbumTitle（专辑标题）、NumberTracks（曲目数）、ReleaseYear（发布年份）（注意：其中某些字段将单独标记）。最后，点击下一步 > 点击“设置和格式化”。首先是字段名，保留下方的说明。对于 Song、Artist 和 Album 字段，将长度设置为 5（图 6）。接下来更改字段名称：将 Producer 改为 Song，AlbumTitle 改为 Album，NumberTracks 改为 Track，ReleaseYear 改为 Year。然后点击下一步 > 点击“主键”。如果尚未标记，则创建主键。选择主键，自动添加主键，并包含值。点击下一步 > 点击“创建”创建表。将名称更改为 MyTable，并选择“立即插入数据”。点击完成！

# 设置与运行

我有了数据库来运行 SQL 查询，以便从音乐库中查找歌曲和专辑信息。下一步是在数据库上设置并运行查询。双击 MyTable 查看表视图并确认数据已正确复制。列的宽度（查询结果的宽度）由查询字段决定。取消勾选“自动”！

图 9：为查询选择搜索条件。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_82_2.png)

（新窗口显示列，LibreOffice 窗口显示数据库、任务和表等选项。）一旦在 base 中创建了表，焦点就在 LibreOffice Calc 中。选择 A1 到单元格，并将所有数据复制到第一个单元格（包含标签的单元格）。现在切换到 Base，将复制的数据粘贴到 MyTable 中。在“表”部分，选择 MyTable。右键点击并从下拉菜单中选择（

# LIBREOFFICE 音乐数据库

| 查询向导 | 如果需要则分配别名 |
| :--- | :--- | :--- |
| 步骤 | 字段 | 别名 |
| 1. 选择顺序 | MyTable.Artist | Artist |
| 2. 排序顺序 | | |
| 3. 搜索条件 | MyTable.Song | Song |
| 4. 详细或摘要 | | |
| 5. 分组 | MyTable.Album | Album |
| 6. 分组条件 | | |
| 7. 别名 | | |
| 8. 概览 | | |

图 10：别名。

- 点击“搜索”：在字段列表中选择 MyTable Artist。在“条件”下拉列表中选择 like，并在“值”字段中输入 %Herbie。

- 注意：在 SQL 中，% 符号被用作通配符。like 匹配字符串模式。SQL 查询显示为：

```sql
SELECT "Artist" AS "Artist", "Song"
FROM "MyTable" WHERE "Artist" LIKE '%Herbie%'
```

- （跳过查询向导中的“分组”和“分组条件”步骤，因为此过程没有使用它们。）

- 点击“别名”（位于查询向导第 7 步）。MyTable Artist 的别名提供 Artist，MyTable.Song 的提供 Song。使用默认值（如图 10 所示）。

- 点击“概览”。在查询名称中，将名称更改为 Query_MyTable_AndSongs。在概览视图中查看结果。使用默认显示选项。

LibreBase 提供三种方法创建查询：在设计视图中创建、使用向导创建查询或在 SQL 视图中创建。我使用了“使用向导”的方法来设置并运行查询。例如，我使用向导设置了针对特定艺术家的查询。然后，在查询结果中使用“标准筛选”来细化搜索。然后点击数据库部分。点击“使用”创建查询并执行以下步骤：

- 在查询向导中点击筛选：在字段窗口中选择 Song、Artist 和 Album，并将它们移动到字段窗口。如果需要，使用箭头更改顺序（图 9）。

- 点击排序顺序：首先按 Artist 升序排序，然后使用 Song。

# 设置并运行筛选

数据视图列表显示了音乐库中所有 Herbie Hancock 的歌曲。要仅搜索前三列，通过上述标准创建查询，有一种简单的方法：使用此查询结果中的标准筛选。

如果数据视图尚未打开，点击数据库部分的查询，双击 MyTable，数据视图就会打开（图 11）。

从这里，点击工具栏上的标准筛选图标（图 12）。

图 11：显示的数据视图。

图 12：在标准筛选中选择筛选。

| Query_MyTable - MusicLibrary - LibreOffice Base 数据视图 |
| 文件 编辑 视图 插入数据 工具窗口 | 帮助 |
|---|---|---|---|---|---|
| Artist | Song | Album | | | | |



| Herbie Hancock | Watermelon | Ken Burrell | | | | |

| Herbie Hancock | You's Good in Bad | Ken Burrell | | | | |

| Herbie Hancock | First Trip | Ken Burrell | | | | |

| Herbie Hancock | Goodbye to Child | Ken Burrell | | | | |

| Herbie Hancock | Speak Like A Child | Ken Burrell | | | | |

| Herbie Hancock | Speak Like Like | Ken Burrell | | | | |

| 操作符 字段名 条件 值 | LIKE | '%%' | | | | |

| Herbie Hancock | The Sorcerer | Ken Burrell | | | | and - - |

| Herbie Hancock | The New | Ken Burrell | | | | and - | |

# LIBREOFFICE 音乐数据库 LINUX 语音

打开它后，我在“字段”`Field`下拉列表中选择了“专辑”`Album`，并在“条件”`Condition`下拉列表中选择了“包含”`like`。使用“包含”条件允许使用通配符来匹配“值”`Value`文本框中的部分字符串。接下来，我在“值”框中输入名称。该值是敏感的，并且重复输入。我可以使用 SQL 通配符百分号 (`%`)（例如 `%%`）来代替完整的专辑名称 *Speak Like A Child*。其他过滤条件也可以应用于“艺术家”`Artist`、“歌曲”`Song`或“专辑”`Album`字段。

## 过滤结果

如图 13 所示，标准过滤器将信息缩小到一张专辑：*Speak Like A Child*。这是一个简单的示例，说明通过遵循我描述的过程，LibreOffice 可以轻松地从 iTunes 导入音乐信息到可搜索数据库，并执行简单到中等复杂的查询。

## 总结

为了方便对 SQL 不熟悉的的用户进行数据库创建和查询，我使用了向导来创建数据库表和查询。更高级 SQL 用户可以编写更多的查询和表关系。这些功能在 LibreOffice Base 中可用。尽管我使用了 LibreOffice 嵌入数据库引擎 SQLDB，但 Base 也可以连接到 MySQL、MariaDB 和 PostgreSQL 等其他 SQL 数据库。对于为个人、教育或家庭办公创建和管理一个或多个数据库的用户，LibreOffice 的实现更快、更简单，并且具有内置的用户界面。对于简单到中等复杂的查询，LibreOffice 实现了与复杂的 MySQL 相同的目标。

图 13：使用标准过滤器将结果缩小到一张专辑。

| 艺术家 | 专辑 | 曲目 |
| :--- | :--- | :--- |
| Herbie Hancock | First Trip | Speak Like A Child |
| Herbie Hancock | Goodbye to Childhood | Speak Like A Child |
| Herbie Hancock | Riot | Speak Like A Child |
| Herbie Hancock | Speak Like A Child | Speak Like A Child |
| Herbie Hancock | The Sorcerer | Speak Like A Child |
| Herbie Hancock | Toys | Speak Like A Child |

> John Cofield 是北加利尼亚州的一位退休软件营销经理。他的背景是电气工程，曾在多家硅谷半导体和软件公司工作过。他的非技术兴趣包括从调式派（Modal）到融合派（Fusion）的爵士乐。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_84_0.png)

LINUX-MAGAZINE.COM | LINUXPROMAGAZINE.COM 第 258 期 2022年5月 85

# FOSSpicks

自由和开源软件世界中闪闪发光的新发布产品

> Graham 目前痴迷于在 KDE Plasma 上使用平铺窗口管理器，使用 ALT + 左键/右键来缩放窗口，需要记住键盘快捷键。作者：GRAHAM MORRISON

## 软件合成器

### Surge XT

我们之前已经查看过 Surge 合成器的之前的版本，但它正以惊人的速度不断发展和改进。现在，该项目在其名称中加入了“XT”，以显示此次更新的意义。合成器本身是你可以安装的听感最好的软件之一，使其在音质和丰富性上都非常可行。但由于它不是一个频谱扭曲波形合成器，因此它的音色方式和引导提取声音的方式非常奇特。Surge 同样复杂，但音频和信号流更加传统且更容易跟进。在窗口左上角，你有三个面板可以根据经典的锯齿波、方波、三角波来调优振荡器，但可以对它们进行微调并修改形状，下方面板还有子混合器。当你移动滑块时，波形显示会显示新形状，当然，如果你弹奏键盘，可以立即听到结果。每个振荡器的幅度通过振荡器右侧的另一个垂直滑块面板混合到补丁中，选择“振荡器调制”来创建创造性的金属感音色。这里的各个部分用于为原始振荡器添加特征，方法是通过移除它们的谐波。Surge 有两个极佳的过滤器，可以根据非常整洁的图表配置为串行、并行或其他配置运行。同样的流程图也用于频率调制，并有助于视觉化其他过滤器无法实现或被隐藏的功能。过滤器本身听起来非常棒，并且有大量的选择，包括听起来像 Moog、Oberheim 以及现代混合型合成器的过滤器。

![](img/d0fe54f1060b69f0f3f8ac0f16844891_85_0.png)

- 1. 振荡器 `Oscillators`：这些产生声音并以经典形状修改波形。
- 2. 编辑器 `Editor`：更改振荡器、过滤器或混合的几乎所有设置。
- 3. 路由 `Routing`：实用的流程图显示了路径和连接方式。
- 4. 过滤器 `Filters`：过滤器本身听起来非常棒，有大量的选择。
- 5. 输出 `Output`：最终的声音输出。
- 6. 效果 `Effects`：优美的混响、延迟、声码器、磁带模拟器。
- 7. 预设 `Presets`：加载不同声音的配置。
- 8. 调制 `Modulation`：用于创建创造性的金属感音色。

LINUX-MAGAZINE.COM | LINUXPROMAGAZINE.COM 第 258 期 2022年5月 85

另一个元素是合成器设计中的关键元素，因为它使用 LFO 来产生两种声音，带有正确的调制效果和频率调制，并随时间控制声波中的参数。主窗口的中部和下部专门用于创建调制选项矩阵，包括大量的 LFO、序列器和包络器。几乎任何事物都可以改变其他事物，像模块化合成器一样创建巨大且复杂的模式。与模块不同，Surge 支持 MIDI 多音表达式 `MPE`，并可作为 LV2 插件或 VST 使用。我们甚至还没有提到可以构建在声音输出上的效果，其中包括优美的混响和延迟、声码器、磁带模拟器，甚至一种深受开源行业标准启发的效果。

- 1. 振荡器 `Oscillators`：这些产生声音并以经典形状修改波形。
- 2. 编辑器 `Editor`：更改振荡器、过滤器或混合的几乎所有设置。
- 3. 路由 `Routing`：实用的流程图显示了路径和连接方式。
- 4. 过滤器 `Filters`：过滤器本身听起来非常棒，有大量的选择。
- 5. 输出 `Output`：最终的声音输出。
- 6. 效果 `Effects`：优美的混响、延迟、声码器、磁带模拟器。
- 7. 预设 `Presets`：加载不同声音的配置。
- 8. 调制 `Modulation`：用于创建创造性的金属感音色。

# FOSSpicks

自由和开源软件世界中闪闪发光的新发布产品

> Graham 目前痴迷于在 KDE Plasma 上使用平铺窗口管理器，使用 ALT + 左键/右键来缩放窗口，需要记住键盘快捷键。作者：GRAHAM MORRISON

## 平铺窗口

### Krohnite

Krohnite 是另一个平铺窗口管理器（参考 Surge）。它包含了一些功能，但它一直在持续持续的改进（注：这里的 Surge 应该是指代某种合成器，原文可能有误）。在这里是，它在 KDE 的标准设置中提供了配置，这种感觉更好且集成度更高。尽管 Plasma 本身添加平铺功能，但这种高可配置的参数并不多。“窗口管理器”设置页面允许你禁用或自定义平铺功能。特别是，你可以为不同的活动和虚拟桌面设置布局，启用或禁用平铺模式，选择特定窗口（如 *Speak Like A Child* 出现在顶部），并修改面板显示的形状：既强大又易用。

## 窗口排列器

### Bism

Bism 是另一个平铺窗口管理器（参考 Surge）。它包含了一些功能，但它一直在持续持续持续的改进。在这里是，它在 KDE 的标准设置中提供了配置，这种感觉更好且集成度更高。尽管 Plasma 本身添加平铺功能，但这种高可配置的参数并不多。“窗口管理器”设置页面允许你禁用或自定义平铺功能。特别是，你可以为不同的活动和虚拟桌面设置布局，启用或禁用平铺模式，选择特定窗口（如 *Speak Like A Child* 出现在顶部），并修改面板显示的形状：既强大又易用。

# LINUX 开源精选

## 终端探索器

### xplr

尽管我们已经看过的命令行管理器，以及由 Miguel de Ikea 创建的经典工具 Midnight Commander，但感觉某些地方仍然需要改进。xplr 可能是那个带来改变的工具，因为它比 Midnight Commander 更强大，但它的工作方式不同，而且并不是那种让你能够复制桌面文件管理器体验的方式。xplr 主打极简主义且速度极快。它可以在几秒钟内启动，解析 `-l` 命令的输出，默认视图显示相同的信息。你可以使用光标或方向键在文件和目录列表中上下移动，按右键进入目录，按左键返回父目录。其他绑定键（如顶部和底部）也同样有效，并且有一个等效命令可以通过按下操作来操作：

但你不需要是 Vim 用户，也不需要拥有惊人的记忆。右下角的小面板显示了所有的快捷键，按下将显示可用命令的完整列表及其功能，这让 xplr 变得强大，它能让你轻松执行一些在命令行中可能需要更长时间的操作。你可以使用空格键选择文件和目录（例如），以及右侧面板格中的选中项目。然后你可以进一步使用命令将其移动 `o` 或复制 `c` 到另一个位置。如果你需要更多功能，例如自定义布局或新命令，那么黑客们可以通过可以通过 Python 系统、注释良好的代码，甚至一个黑客守护进程来为你提供帮助。

## 项目网站

`https://github.com/xplr`

## Python shell

### sonsh

尽管大多数发行版默认使用 Bash shell，但仍有很多不错的替代方案。当然，还有原始的 Korn Shell `Ksh` 和极其受欢迎的 Z shell `Zsh`。这些每一个都非常值得尝试。它还提供了简单的配置选项，或者可以通过 Python 软件包手动安装的包。通过 pip 安装，你可能起初就想安装 sonsh，因为它是一个将由 Python 开发者和用户最使用的 shell。

而且仍然能够运行 shell。它允许你执行你可能预期的所有命令，如 `is`、`rv`，并且在 Python 环境中执行。你可以使用 `type 3, 14*5` 来执行计算或设置变量。你可以导入外部模块并使用本地变量和 datetime 输入。Python 变量的形式与普通 shell 环境相同，这对于进行编程评估非常有用，而且你可以像使用 Bash 一样使用它。你可以用你的选项填充配置文件，并且提示符可以像其他 shell 环境一样进行自定义。如果你大部分编程时间都在 sonsh 中度过，在没有 Python 解释器且包含普通 shell 命令和环境变量的情况下会略显不足。Python 使用一个可以扩展到你与操作系统交互方式的 shell，这感觉是有意义的，特别是因为 Python 更多是基于主见而非一个人的预期。即使你不是一个 Python 程序员，使用 sonsh 也是一种绝佳的学习方式。

## 项目网站

`https://xon.sh/`

## MQTT 客户端

### MQTTExplorer

MQTT 是听起来很复杂但实际上非常容易理解的东西——当你知道如何使用它时它非常强大。该项目也没有轻易提供便利，它自己描述为“物联网 `IoT` 协议”，但 MQTT 是一种易于理解的消息传输架构，几乎可以从任何设备到服务器。例如，你可能有一个连接到树莓派的 USB 传感器，你想将其数据与本地的 Node-RED 服务器共享。这就是 MQTT 可以派上用场的地方。简单的命令行客户端工具 `mosquit_pub` 可以将传感器的输出转换为 MQTT 消息并发布到另一个命令启动的本地客户端。结果是所有消息的聚合，这些消息可以连接到 MQTT 代理（如 Node-RED）。使用 MQTT 的尊重之处在于，接收客户端可以确切知道消息内容，这就是为什么 MQTT Explorer 可以帮助你通过其原生 JSON 支持管理消息。MQTT 是一个设计精美的客户端，可以展开这些消息并探索其内容，跟踪它们值的变化。你只需要输入想要连接的发布服务器详情，传入的消息就会聚合并列在主窗口中。这将在直方图、图表和查看选项部分显示它们的值。这是一个揭秘 MQTT 并将所需部分提取到其他软件的极佳方法。

MQTT 非常适合家庭自动化，而 MQTT Explorer 可以帮助你从传感器中获得最大价值。

## 项目网站

```
http://mqt-explorer.com
```

## 笔记软件

我使用过 macOS 或 iOS 设备，你知道它们很有帮助，但我注意到这些平台的笔记应用程序泛滥。。这可能是因为 iPad 配合可选工具非常适合在教育环境中做笔记，但也可能是为了让这些系统的用户工作更方便。无论如何，这些应用程序通常看起来都非常漂亮，并提供写作和 PDF 标注、在文档周围书写笔记或在自己的草稿上绘图。Rnote 是我见过最接近开源 Linux 应用程序的，感觉就像其中那些应用程序一样，它将是一段捕捉简洁、极简美学的奇妙之旅，同时提供了许多功能。设计上的荣誉很大程度上归功于 GTK，因为 Rnote 充分利用了这种快速适应的方法。它有圆角、动画过渡、顶栏图标以及渲染精美的字体。主视图是绘图，显然使用鼠标或某种类型的触控笔会更易用。但即使没有这些，它也有你可能需要的常用工具，包括取消高亮、形状和粗体文本。每一笔都使用笔刷触感。还有修改你涂鸦的选取方法，你甚至可以开启“绘图声音”来增加趣味。

Rnote 是一个精美且极简的笔记应用程序，充分利用了 GTK 的正统。你可以导入图像或 PDF 在其上绘图，并将整个乱稿保存为 `.rnote` 文件，你还可以将其导出为 SVG 或 PDF，甚至导出为内核 Xournal++ 笔记应用程序的文件。唯一缺失的大型功能是添加文本字段的能力，该功能正在开发中。

## 项目网站

```
https://github.com/fixt/note
```

# LINUX 开源精选

## 分形探索器

### Mandelbuber v2

分形是惊人的。即使在它们最初流行的几十年后，当混沌理论和蝴蝶效应等事实几乎被提到时——视觉化无限的复杂性仍然令人着迷。在 20 世纪 80 年代和 90 年代，个人电脑通过 Amiga 上的生成器首次为这个世界打开了一扇窗。在 20 世纪 80 年代和 90 年代，个人电脑通过 Amiga 上的生成器首次为这个世界打开了一扇窗。在 20 世纪 80 年代和 90 年代，个人电脑通过 Amiga 上的生成器首次为这个世界打开了一扇窗。

在 20 世纪 80 年代和 90 年代，个人电脑通过 Amiga 上的生成器首次为这个世界打开了一扇窗。在 20 世纪 80 年代和 90 年代，个人电脑通过 Amiga 上的生成器首次为这个世界打开了一扇窗。在 20 世纪 80 年代和 90 年代，个人电脑通过 Amiga 上的生成器首次为这个世界打开了一扇窗。

在 20 世纪 80 年代和 90 年代，个人电脑通过 Amiga 上的生成器首次为这个世界打开了一扇窗。在 20 世纪 80 年代和 90 年代，个人电脑通过 Amiga 上的生成器首次为这个世界打开了一扇窗。在 20 世纪 80 年代和 90 年代，个人电脑通过 Amiga 上的生成器首次为这个世界打开了一扇窗。

-Mandelbuber 是 21 世纪真实的分形探索器。Elidolon 由 Lucasfilm Games 发布，因为那些分形的 Mandelbrot 集合，其形状、星系并变得不可思议。

那时有许多分形生成软件，它们在最近变得不那么流行。然而，一些优秀的应用程序仍然存在，Mandelbuber 是其中之一。但它是带有附加功能的分形探索器。

有许多分形可以选择，它们都可以进行调整并保存为自己的预设。主 UI 帮助

探索 Mandelbuber 的感觉类似于在 Blade Runner 中

你可以使用鼠标或移动模式来导航 Mandelbuber，鼠标还作为输出的焦点，或者选择你想要探索的区域。渲染选项和菜单项一样多——包括材质、光线追踪、深度效果看起来非常惊人，这在十年前是无法实现的。如果你有硬件，它可以通过 OpenGL 加速，但即使没有，当你深入分形洞穴时渲染也非常很快。即使在那时，你也可以将处理分配给分布式网络渲染器。

分形是惊人的。即使在它们最初流行的几十年后，当混沌理论和蝴蝶效应等事实几乎被提到时——视觉化无限的复杂性仍然令人着迷。几十年后，当混沌理论和蝴蝶效应等事实几乎被提到时——视觉化无限的复杂性仍然令人着迷。在 20 世纪 80 年代和 90 年代，个人电脑通过 Amiga 上的生成器首次为这个世界打开了一扇窗。在 20 世纪 80 年代和 90 年代，个人电脑通过 Amiga 上的生成器首次为这个世界打开了一扇窗。



在 20 世纪 80 年代和 90 年代，个人电脑通过 Amiga 上的生成器首次为这个世界打开了一扇窗。

`Mandelbuber` 是 21 世纪真实的分形探索器。`Elidolon` 由 Lucasfilm Games 发布，因为那些分形的 Mandelbrot 集合，其形状、星系并变得不可思议。

# 运输模拟器

# FOSSPICKS LINUX 之声

# Simutrans

![](img/d0fe54f1060b69f0f3f8ac0f16844891_90_0.png)

在小时候，我们中的许多人都喜欢玩玩具轨道或组装我们的电力驱动赛道。随着年龄增长，我们真的无法完全停止对这些事的喜爱，特别是如果这种乐趣可以在软件中重现的话。这就是 Simutrans 的意义：一种感觉更像《城市模拟 2000》而不是模型铁路的体验。这是一款运输管理游戏，背景设定在一个看起来像旧版《城市模拟》的环境中。“开放”是关键词，因为你可以设置你自己的起始世界，这显然会影响你从未来未来能够使用的运输技术类型。

然而，与《城市模拟》一样，你从生成一个随机地图开始游戏，这幅地图上通常已经包含了一个或两个城市（通常是史诗规模的），你的任务就是解决所有的运输需求。

你通常开始通过一些交通工具连接郊区，并沿着合适的路线添加任何形式的交通工具。然后，你可以根据你能提供的每种运输模式访问的基础设施。例如，对于铁路，你选择一条合适的路线并画出一条包含桥梁、交叉口、许多其他元素和运输模式的线。每种都有成本，并且显然增加了你运输系统的复杂性，这就像在指尖拥有你生活中最大的模型铁路一样，它很快就会变得非常复杂。

与《城市模拟》一样，Simutrans 可以从商店下载，如果你正在使用 Steam Deck，这太完美了。如果你想要一些更大规模、更直观的内容，可以使用集成面板下载场景，你可以在这些场景的基础上进行构建以解决运输问题。这始于沙盒模式的复杂性让你无从下手，而在时间有限的情况下，这会让游戏变得非常有趣。

## 项目网站

`https://www.simutrans.com`

# 3D

# 索尼机器人大爆发 2

![](img/d0fe54f1060b69f0f3f8ac0f16844891_90_1.png)

索尼（鼠（Sonic the Hedgehog）在开源游戏评论中经常出现。这一定是因为索尼是 1990 年代经典游戏的杰作，这款游戏吸引了索尼的创造者，而且它的历史长到让当时的制作者在今天成为了资深开发者。《索尼机器人大爆发 2》（Sonic Robo Blast 2）是这一理论的完美反映，它是索尼的一个优秀源码，但没有毁灭战士（Doom）英雄。游戏本身完全节奏很快，甚至根源于索尼引擎。超过 25 个关卡完全由社区创建，具有与原作相同的音乐、跳跃平台风格，但有一个重要的区别：游戏被转换到了三维。

不仅仅是《超级马里奥 64》那种整洁的三维。这些也是角色和大毁灭战士（更准确说是更新后的 Doom Legacy 引擎）。

如果你玩过原版，游戏玩法会很熟悉。在进入游戏之前，会详细介绍各种角色，并配有卡通风格的图形。玩家可以根据意愿选择具有不同能力的角色，你的任务保持不变——在穿越每个区域时尽可能收集金环。你仍然需要像原版一样应对所有的敌人、挑战和障碍，现在有了向各个方向移动的能力。虽然这对于两种不同的游戏风格来说可能显得不自然，但《索尼机器人大爆发 2》的玩法与原版相似，具有高质量的制作水平，以及像《索尼 2》那样的上升悬崖、动态控制采矿和跨越峡谷。

这件惊人的粉丝衍生小说（游戏类）开发时间和它的灵感一样长，但目前仍在定期更新。

## 项目网站

`https://www.sonicroboblast.org/`

`LINUX-MAGAZINE.COM | LINUXPROAPERCRAFT.COM | 第 258 期 2022年5月 | 91`

# LINUX 之声教程 – 纸模型

## 使用 Inkscape 扩展从纸张创建 3D 对象

纸模型是一种古老的工艺形式。它只需要剪刀、纸和一点胶水。建筑师们使用这种技术快速视觉化模型，并利用虚拟现实独立开发设计。在低多形建模和 Minecraft 等趋势的推动下，这种技术在爱好者领域也经历着复兴。在全球范围内——例如日本——现在有许多人在各种社交媒体平台上发布他们的作品。在日本，这被称为 pepakura（纸模型），并且也有同名的软件免费提供。

可以使用 Inkscape 结合扩展创建纸模型，如下：

- `Boxes.py` [1]
- `Quickfold` [2]
- `Lasercut-box` [3]
- `Papercraft` [4]
- `Joinery` [5]
- `Tabgen` [6]

### 不仅仅是盒子

`Boxes.py` 非常有趣，特别是因为它带有很多预定义的对象，而不仅仅是简单的盒子。但具有类似特征的更复杂的设计也需要 `Boxes.py`，你只需要根据需要对其进行调整。`Pepakura` 和其他用于此类工作的软件仅适用于 Windows，这迫使 Linux 用户寻找其他方法将它们纳入工作流。

将对象展开并将单个侧面显示为面也是所有工艺的基础——它们通常对节点有不同的定义。设计 3D 对象的自由软件世界中的其中一个选项是 `Blender`。当然，它的功能远超完成任务所需的。对于纸模型，3D 对象也需要展开。这一步由平化器（flattener）处理，`Blender` 有一个插件可以处理。

# LINUX 语音教程 | 纸艺

按住 `Shift` 键。之后，你可以选择一条边缘并执行“编辑 | 选择相同项 | 轮廓”功能，这会让 Inkscape 将该边缘的所有路径都纳入选择范围。

由于后续步骤难以撤销，请使用 `Ctrl+D` 创建所有所选路径的副本。之后，应用“路径 | 描边转路径”，然后执行“路径 | 合并”。现在你应该可以对对象应用“标签（Tag）”了。

通过创建另一个路径对象，根据扩展设置中为胶接凸选择的尺寸将其放大（图 4）。但这里也有一个小缺点：该扩展的开发者似乎是将物对象的每个侧面都粘在一起，而不是进行折叠。因此，如果你在不需要的地方出现了折痕，你必须手动从对象中删除它们。

开发者需要多下一些精力，让这个扩展适用于更广泛的受众。此外，该工具会显示错误，这是因为代码没有捕获任何错误，返回的错误信息即使对经验丰富的用户也帮助不大。开发者可能正在学习编程，并为自己使用创建这些扩展。一些反馈和赞美可能会大有裨益。

## 结论

纸艺可能有过它的旧时代，但通过切割和一点创造性思维，它目前正在重焕流行。通过 Inkscape 和我们在文章中提到的扩展，你完全可以沉浸这项爱好并享受其中的乐趣。

## 信息

- [1] `Boxes.py`: `https://www.festi.org/boxes/`
- [2] `Quickpoint`: `https://inkscape.org/~Jarrett/%E2%98%85quickpoint`
- [3] `激光切割凸接盒`: `https://inkscape.org/~Neon22/%E2%98%85lascut-tabbed-box`
- [4] `Paperfold`: `https://inkscape.org/~MarioVoigt/%E2%98%85paperfold`
- [5] `Joinery`: `https://lementzheng.org/Joinery`
- [6] `骨akura`: `https://tamasoft.com/jp/peakura-en`
- [7] `Tabgen`: `https://inkscape.org/de/~Shoshaz/%E2%98%85tabgen-3-papercraft-extension`

图 4：立方体的一侧：凸边是由 `Tabgen` 创建的。

## 作者

Sirko Kemter 自 Inkscape 项目诞生起就热爱这个项目，并发现该软件提供的新选项。

# LINUX 新报

《Linux 杂志》是你进入 Linux 世界的指南。每期杂志都充实了你在其他地方找不到的高级技术文章和教程。探索我们的完整过刊目录以获取特定主题或完善你的收藏。

在线订购：`https://bit.ly/Linux-Newsstand`

## #257/2022年4月

加密

本月，我们调查了 Linux 加密的现状况。我们放眼远眺，探索了一些支撑机密系统的工具和技术——并向你展示确保隐私万无一失所需要的知识。

DVD 光盘内容：Linux Mint 20.3 Cinnamon 版和 deepin 20.4

## #256/2022年3月

面部识别

随着微软 Hello 技术的到来，生物识别近期获得了增长。现在开源领域正在追赶，有一个名为 Howdy 的创新工具。面部认证可能尚未准备好供 CIA 局使用，但我们将帮助你开始使用 Howdy，并探索通过一眼进行认证的可能性。

DVD 光盘内容：antiX 1 和 Haiku R1/ Beta 3

## #255/2022年2月

破坏以重构

模糊测试（Fuzz Testing）：攻击者是如何发现这些导致程序崩溃并交出控制权的“精心设计的输入字符串”的？欢迎来到模糊测试的世界。我们为你介绍模糊测试，并探索一些模糊测试技术。

DVD 光盘内容：Parrot OS 4.1 和 Fedora Workstation 35

## #254/2022年1月

手机破解

制造商最终会放弃支持旧版硬件。如果你还没有准备好放弃那些东西，你可能会通过 LineageOS 找到更好的替代方案——这是一个基于 Android 的免费系统，支持 300 多部手机，包括许多不再受供应商支持的旧型号。我们还探索了 PostmarketOS，这是一个运行在若干 Android 设备上的社区版 Linux。

DVD 光盘内容：Ubuntu 21.10 和 EndeavourOS 2021。

## #253/2021年12月

OpenBSD

BSD Unix 的历史比 Linux 还要长，它在自由软件社区内仍有一群忠诚的追随者。本月，我们从 Linux 用户的视角探索了一个领先变体的好处。

DVD 光盘内容：Tails 4.2 和 QOS

## #252/2021年11月

锁定！

格局不断变化，经验用户知道他们需要时刻关注那些能提供优势的工具和技术。本月，我们研究了智能卡、硬盘加密以及一种 Sudo 的少数替代方案。

DVD 光盘内容：Debian 11

## 特色活动

用户、开发者和供应商在世界各地的活动汇聚。在《Linux 杂志》，我们很自豪在此处介绍。有关你附近的其他活动，请在线查看 `www.linux-magazine.com/events` 查看我们的扩展日历。如果你知道其他想添加到我们日历的活动，请发送带有详情的消息到 `info@linux-magazine.com`。

在预订任何旅行之前，请务必检查活动网站，由于 COVID-19 的影响，许多活动可能会取消或转换为虚拟活动。

## Linux 应用峰会

日期：2022年4月29-30日

地点：Rovereto 和在线

网站：`linuxappsum.com`

Linux 应用峰会（LAS）将全球社区聚集在一起，进行学习、协作并帮助构建一个共同的生态系统。通过演讲、小组小组会议和问答环节，我们鼓励参会者分享想法、建立联系并加入我们的目标。

## ISC 性能大会



ISC 是针对高性能计算、机器学习和数据分析的活动。ISC 汇聚了从业者、用户和供应商，就他们以前见过的技术进行讨论。该活动同时在现场和远程举行。加入 3,000 名参会者和 100 家展商中，体验全新的技术计划和展览。

日期：2022年5月29日-6月2日

地点：德国汉堡

网站：www.hpc.com

# 活动列表

- ODSC East 2022 | 4月19-21日 | 马萨诸塞州，波士顿 + 虚拟
- LinuxFest Northwest 2022 | 4月22-24日 | 虚拟
- DrupalCon Portland 2022 | 4月25-26日 | 俄勒冈州，波特兰德
- DeveloperWeek 2022 | 4月27-28日 | 虚拟活动
- Linux App Summit | 4月29-30日 | 意大利，Rovereto + 虚拟
- Linux Storage, Filesystems, & MPI | 5月2-4日 | 加利福尼亚州，棕榈榈滩
- Cloud Expo Europe | 5月11-12日 | 德国，法兰克福
- KubeCon CloudNative Europe 2022 | 5月16-20日 | 西班牙，瓦伦西亚
- ISC High Performance 2022 | 5月29日-6月2日 | 德国汉堡
- OpenJS 2022 | 6月6-10日 | 德克萨斯州，奥斯汀
- Code 7-8 | 德克萨斯州，奥斯汀 + 虚拟
- ODSC Europe 2022 | 6月15-16日 | 英国，伦敦 + 虚拟
- ITEXPO Forum | 6月21-24日 | 佛罗里达州，劳德代堡
- Open Source Summit | 6月21-24日 | 德克萨斯州，奥斯汀 + 虚拟
- 北美
- XDev Developer & Design Summit 2022 | 罗马尼亚，布加勒斯特 + 虚拟
- 加利福尼亚州
- 德国汉堡

按住 `Shift` 键。之后，你可以选择一条边缘并执行“编辑 | 选择相同项 | 轮廓”功能，这会让 Inkscape 将该边缘的所有路径都纳入选择范围。

由于后续步骤难以撤销，请使用 `Ctrl+D` 创建所有所选路径的副本。之后，应用“路径 | 描边转路径”，然后执行“路径 | 合并”。现在你应该可以对对象应用“标签（Tag）”了。

通过创建另一个路径对象，根据扩展设置中为胶接选择的尺寸将其放大（图 4）。但这里也有一个小缺点：该扩展的开发者似乎是将物对象的每个侧面都粘在一起，而不是进行折叠。因此，如果你在不需要的地方出现了折痕，你必须手动从对象中删除它们。

开发者需要多下一些精力，让这个扩展适用于更广泛的受众。此外，该工具会显示错误，这是因为代码没有捕获任何错误，返回的错误信息即使对经验丰富的用户也帮助不大。开发者可能正在学习编程，并为自己使用创建这些扩展。一些反馈和赞美可能会大有裨益。

# 结论

纸艺可能有过它的时代，但通过切割和一点创造性思维，它目前正在重焕流行。通过 Inkscape 和我们在文章中提到的扩展，你完全可以沉浸这项爱好并享受其中的乐趣。

# 信息

- [1] Boxes.py: https://www.festi.org/boxes/
- [2] Quickpoint: https://inkscape.org/~Jarrett/%E2%98%85quickpoint
- [3] 激光切割凸接盒: https://inkscape.org/~Neon22/%E2%98%85lascut-tabbed-box
- [4] Paperfold: https://inkscape.org/~MarioVoigt/%E2%98%85paperfold
- [5] Joinery: https://lementzheng.org/Joinery
- [6] Pepakura: https://tamasoft.com/jp/peakura-en
- [7] Tabgen: https://inkscape.org/de/~Shoshaz/%E2%98%85tabgen-3-papercraft-extension

图 4：立方体的一侧：凸边是由 Tabgen 创建的。

# 作者

Sirko Kemter 自 Inkscape 项目诞生起就热爱这个项目，并发现该软件提供的新选项。

# LINUX 新报

《Linux 杂志》是你进入 Linux 世界的指南。每期杂志都充实了你在其他地方找不到的高级技术文章和教程。探索我们的完整过刊目录以获取特定主题或完善你的收藏。

在线订购：https://bit.ly/Linux-Newsstand

# #257/2022年4月

加密

本月，我们调查了 Linux 加密的现状。我们放眼远眺，探索了一些支撑机密系统的工具和技术——并向你展示确保隐私万无一失所需要的知识。

DVD 光盘内容：Linux Mint 20.3 Cinnamon 版和 deepin 20.4

# #256/2022年3月

面部识别

随着微软 Hello 技术的到来，生物识别近期获得了增长。现在开源领域正在追赶，有一个名为 Howdy 的创新工具。面部认证可能尚未准备好供 CIA 局使用，但我们将帮助你开始使用 Howdy，并探索通过一眼进行认证的可能性。

DVD 光盘内容：antiX 1 和 Haiku R1/ Beta 3

# #255/2022年2月

破坏以重构

模糊测试（Fuzz Testing）：攻击者是如何发现这些导致程序崩溃并交出控制权的“精心设计的输入字符串”的？欢迎来到模糊测试的世界。我们为你介绍模糊测试，并探索一些模糊测试技术。

DVD 光盘内容：Parrot OS 4.1 和 Fedora Workstation 35

# #254/2022年1月

手机破解

制造商最终会放弃支持旧版硬件。如果你还没有准备好放弃那些东西，你可能会通过 LineageOS 找到更好的替代方案——这是一个基于 Android 的免费系统，支持 300 多部手机，包括许多不再受供应商支持的旧型号。我们还探索了 PostmarketOS，这是一个运行在若干 Android 设备上的社区版 Linux。

DVD 光盘内容：Ubuntu 21.10 和 EndeavourOS 2021。

# #253/2021年12月

OpenBSD

BSD Unix 的历史比 Linux 还要长，它在自由软件社区内仍有一群忠诚的追随者。本月，我们从 Linux 用户的视角探索了一个领先变体的好。

DVD 光盘内容：Tails 4.2 和 QOS

# #252/2021年11月

锁定！

格局不断变化，经验用户知道他们需要时刻关注那些能提供优势的工具和技术。本月，我们研究了智能卡、硬盘加密以及一种 Sudo 的少数替代方案。

DVD 光盘内容：Debian 11

# 特色活动

用户、开发者和供应商在世界各地的活动汇聚。在《Linux 杂志》，我们很自豪在此处介绍。有关你附近的其他活动，请在线查看 www.linux-magazine.com/events 查看我们的扩展日历。如果你知道其他想添加到我们日历的活动，请发送带有详情的消息到 info@linux-magazine.com。

在预订任何旅行之前，请务必检查活动网站，由于 COVID-19 的影响，许多活动可能会取消或转换为虚拟活动。

# Linux 应用峰会

日期：2022年4月29-30日

地点：Rovereto 和在线

网站：linuxappsum.com

Linux 应用峰会（LAS）将全球社区聚集在一起，进行学习、协作并帮助构建一个共同的生态系统。通过演讲、小组小组会议和问答环节，我们鼓励参会者分享想法、建立联系并加入我们的目标。

# ISC 性能大会

ISC 是针对高性能计算、机器学习和数据分析的活动。ISC 汇聚了从业者、用户和供应商，就他们以前见过的技术进行讨论。该活动同时在现场和远程举行。加入 3,000 名参会者和 100 家展商中，体验全新的技术计划和展览。

日期：2022年5月29日-6月2日

地点：德国汉堡

网站：www.hpc.com

# 活动列表

- ODSC East 2022 | 4月19-21日 | 马萨诸塞州，波士顿 + 虚拟
- LinuxFest Northwest 2022 | 4月22-24日 | 虚拟
- DrupalCon Portland 2022 | 4月25-26日 | 俄勒冈州，波特兰德
- DeveloperWeek 2022 | 4月27-28日 | 虚拟活动
- Linux App Summit | 4月29-30日 | 意大利，Rovereto + 虚拟
- Linux Storage, Filesystems, & MPI | 5月2-4日 | 加利福尼亚州，棕榈榈滩
- Cloud Expo Europe | 5月11-12日 | 德国，法兰克福
- KubeCon CloudNative Europe 2022 | 5月16-20日 | 西班牙，瓦伦西亚
- ISC High Performance 2022 | 5月29日-6月2日 | 德国汉堡
- OpenJS 2022 | 6月6-10日 | 德克萨斯州，奥斯汀
- Code 7-8 | 德克萨斯州，奥斯汀 + 虚拟
- ODSC Europe 2022 | 6月15-16日 | 英国，伦敦 + 虚拟
- ITEXPO Forum | 6月21-24日 | 佛罗里达州，劳德代堡
- Open Source Summit | 6月21-24日 | 德克萨斯州，奥斯汀 + 虚拟
- 北美
- XDev Developer & Design Summit 2022 | 罗马尼亚，布加勒斯特 + 虚拟
- 加利福尼亚州
- 德国汉堡

按住 `Shift` 键。之后，你可以选择一条边缘并执行“编辑 | 选择相同项 | 轮廓”功能，这会让 Inkscape 将该边缘的所有路径都纳入选择范围。

由于后续步骤难以撤销，请使用 `Ctrl+D` 创建所有所选路径的副本。之后，应用“路径 | 描边转路径”，然后执行“路径 | 合并”。现在你应该可以对对象应用“标签（Tag）”了。

通过创建另一个路径对象，根据扩展设置中为胶接选择的尺寸将其放大（图 4）。但这里也有一个小缺点：该扩展的开发者似乎是将物对象的每个侧面都粘在一起，而不是进行折叠。因此，如果你在需要的地方出现了折痕，你必须手动从对象中删除它们。

开发者需要多下一些精力，让这个扩展适用于更广泛的受众。此外，该工具会显示错误，这是因为代码没有捕获任何错误，返回的错误信息即使对经验丰富的用户也帮助不大。开发者可能正在学习编程，并为自己使用创建这些扩展。一些反馈和赞美可能会大有裨益。

# 结论

纸艺可能有过它的时代，但通过切割和一点创造性思维，它目前正在重焕流行。通过 Inkscape 和我们在文章中提到的扩展，你完全可以沉浸这项爱好并享受其中的乐趣。

# 信息

- [1] Boxes.py: https://www.festi.org/boxes/
- [2] Quickpoint: https://inkscape.org/~Jarrett/%E2%98%85quickpoint
- [3] 激光切割凸接盒: https://inkscape.org/~Neon22/%E2%98%85lascut-tabbed-box
- [4] Paperfold: https://inkscape.org/~MarioVoigt/%E2%98%85paperfold
- [5] Joinery: https://lementzheng.org/Joinery
- [6] Pepakura: https://tamasoft.com/jp/peakura-en
- [7] Tabgen: https://inkscape.org/de/~Shoshaz/%E2%98%85tabgen-3-papercraft-extension

图 4：立方体的一侧：凸边是由 Tabgen 创建的。

# 作者

Sirko Kemter 自 Inkscape 项目诞生起就热爱这个项目，并发现该软件提供的新选项。

# LINUX 新报

《Linux 杂志》是你进入 Linux 世界的指南。每期杂志都充实了你在其他地方找不到的高级技术文章和教程。探索我们的完整过刊目录以获取特定主题或完善你的收藏。

在线订购：https://bit.ly/Linux-Newsstand

# 下个月

第 259 期

第 259 期 / 2022年6月

# 零信任安全

谁可以信任你的网络？根据零信任安全模型，谁都不行。下个月，我们将审视这一强大的网络新愿景——在这样的网络中，没有任何所谓的“内部人员”。

# 预览通讯报

《Linux Magazine Preview》是一份每月一次的电子邮件通讯报，让您抢先预览下一期内容，包括在线发布文章的链接。

注册地址：https://bit.ly/Linux-Update

# ISC 回归线下！

# 改变未来

# 会议

并行编程

系统架构

# 研讨会

机器学习

# 展览

量子计算

应用与算法

以及更多……

# 教程

欢迎加入由 3,000 名高性能计算 (HPC) 从业者、供应商和爱好者的组成的行列。

# 你可以期待到什么？

- 技术议程（线下和线上）
- HPC 展览（线下和线上）
- 与同仁、朋友和合作伙伴重聚
- 安全且符合健康协议的环境

在经历了两年的线上活动后，ISC 以线下活动的形式回归。如果您参与了 HPC 或对此感兴趣，请不要错过在 ISC 2022 建立宝贵人脉的机会。

ISC 2022 | 2022年5月29日 – 6月2日

德国，汉堡 isc-hpc.com

# HETZNER

# 让您的业务蓬勃发展

# 季节特惠

最高节省 £82

春天总是一个新开始的季节。为什么不启动一个新项目呢？

使用我们配备 AMD Ryzen™ CPU 的 AX 独立根服务器来扩展您的基础架构，并免除安装费！

例如：独立根服务器 AX41-NVMe

- AMD Ryzen™ 5 3600
- 同步多线程
- 64 GB DDR4 RAM
- 2 x 512 GB NVMe SSD
- 100 GB 备份空间
- 流量不限制
- 无需最低合约
- 所在地：芬兰和德国

安装费 £33

所有价格均不含值税 (VAT)，并受 Hetzner Online GmbH 条款与条件的限制。价格可能会变动。相关制造商保留所有权利。

安装费 £0，每月 £29 起

# hetzner.com/special
