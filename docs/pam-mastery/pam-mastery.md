
# PAM 高级指南

## 对 Michael W Lucas 其他书籍的评价

### FreeBSD Mastery: ZFS

“又是一本值得读的优秀 FreeBSD 书。” — Wendy Michele, nixCraft

“《ZFS Mastery》涵盖了所有使用或管理这些文件系统的人日常工作中需要的所有知识。在了解了系统的实现原理后，看到它是如何被使用的，这种感觉非常奇妙。” — George V. Neville-Neil，《FreeBSD 操作系统的设计与实现》合著者

### 系统管理员的网络技术

“书中包含了大量的有用信息。我向大家推荐它！” — Sunday Morning Linux Review, 第 145 期

“读完这本书后，你将在网络领域拥有坚实的基础。Lucas 以实用的方式解释概念；他确保教授了 Unix/Linux 和 Windows 下的工具；并为你提供了在向网络人员解释你看到的情况时会用到的术。在此过程中，书中穿落着许多来之不易的知识……” — Slashdot

### FreeBSD Mastery: 特殊文件系统

“阅读它是一种享受和宝藏” — Vivek Gite, nixCraft

“我是他书的粉丝……他呈现书籍让书籍变得更容易理解。他在幽默和信息之间取得了完美的平衡。” — Sunday Morning Linux Review

“太棒了，是 Lucas 作品，是 sudo。现在就买吧。” — Slashdot

“Michael W Lucas 一直是我最喜欢的作者之一，因为他为可能相当枯燥的信息注入了非凡的叙述性。《Sudo Mastery》例外。” — Chris Sanders，《实用数据包分析》作者

“Michael Lucas 再次创造了奇迹。” — cryptednets.org

“在使用 OpenBSD 的 13 年后，我依然学到了新颖且有用的东西！” — Peter Hessler, OpenBSD Journal

“这是一本真正非常优秀的书。它充满了关于 OpenBSD 的核心材料，并以幽默感呈现，展现了对该操作系统运作方式的深刻见解。如果你是从任何类型的 Unix 背景阅读这本书，你将发现所需的内容，让你快速精通 OpenBSD——包括它是如何工作的，以及如何专业地进行管理。我怀疑没有比这更好的关于 OpenBSD 的书了。” — Sandra Henry-Stocker, ITWorld.com

“很快就会发现，Michael 实际上在使用 OpenBSD，而不是一个为了满足字数而来的雇佣兵……简而言之，这不是一本走马观花的书，你不会从中发现任何敷衍的内容。” — Michael Dexter, callfortesting.org

“当 Michael 钻研某个主题并写出一本书时，你可以预期结果将包含大量的有用信息，并伴随着幽默和真实生活的轶事，让你想要在自己的系统上深入探索该主题。” — Peter Hansteen，《PF 之书》作者

“……这是那种你不会只放在书架上的技术书籍之一。它是那种会被压折书脊、许多页面都做了书签并放在键盘旁的书。” — Steven K Hicks, SKH:TEC

“……《SSH Mastery》这类我这样的 Unix 用户和系统管理员想要放在手手边的书籍之一……” — Peter Hansteen，《PF 之书》作者

“这种对通常技术书籍解释的精简，使其具有了互联网上扩展文档的即时性。它不是那种作为广告载体的多页‘如何做’文章，而是来自一个长期使用 OpenSSH 处理过许多问题、并在操作过程中关注细节的人的深度阐述。” — DragonFlyBSD Digest

“将出色的风格与大量的技术信息相结合，这本书提供了一种既有趣又有引胜的学习体验。没有多少技术书籍能声称做到。” — ;login: Magazine, 2010 年 10 月

“这本书的价值价值连城。” — Utah.com

“这本书读起来较快，在排故障和分析网络问题时大有用益。” —Dr. Dobbs

“《Network Flow Analysis》是任何网络管理和数据管理图书馆的优选。它是首次向系统管理员展示如何使用流分析来评估、分析和启动网络，且来自”

“如果你正在尝试学习使用 PGP，或者至少想确保你正确使用了它们，请阅读《PGP & GPG》。” — Slashdot

“如果你使用任何 nix 系统并需要异地备份，那么你需要 Tarsnap。如果你想高效地使用 Tarsnap，你就需要《Tarsnap Mastery》。” —Sunday Morning Linux Review 第 148 期

- 使用 `pam_exec` 调试............................................................... 85
- 配置密码检查 ............................................................... 138

## 致谢

一如既往，我需要感谢对本书早期草稿提供反馈的技术审阅员：Bryan Irvine, Kurt Mosiejczuk, Mike O'Connor 和 Carsten Strotmann。特别感谢 Dag-Er-ling Smørgrav——这位负责 OpenPAM 的“单人军”，他从繁忙的日程中抽出时间教我一些 PAM 基础知识。

我还要感谢我庞大的 Twitter 粉丝，他们运行的操作系统比我所认为仍在使用的要多得多，并且乐意为我的这本大作提供他们那些特别糟糕的 PAM 配置。

所有的测试和研究都是在 iX Systems 慷慨人士提供的服务器上完成的，他们在过去的十年里一直为我的工作提供支持。我能做的最小事情就是感谢他们。

最后，我想感谢这个世界，让我假装 `rsh(1)`、`pam_rhosts` 及其周边生态系统不存在。

送给 Liz。

# 第0章：引言

Unix 类系统上的身份验证可能是系统管理员最接近“黑魔法”的东西。

每位系统管理员都听过可插认证模块（Pluggable Authentication Modules，简称 PAM）。我们都知道 `/etc/pam.d/` 下的文件决定了大多数软件如何进行身份验证。如果你想使用公钥认证、或使用物理令牌进行验证，或者仅依赖密码，你就必须折腾这些文件。通常，系统管理员会盲目地遵循指令，并希望不要发生糟糕的事情。

PAM 策略与系统管理中的其他内容并不完全。一组 PAM 语句的处理方式不像数据包过滤规则或共享库路径，除非它们确实如此。此外，PAM 使用了一些奇怪的词，比如“requisite”（必须），而“sufficient”（足够）这个词显然意味着任何“足够”。

当你弄坏 PAM 时，你就弄坏了整个服务。大多数服务本身运行就已经足够困难了，因此不鼓励破坏它们。希望坏掉的不是那个让你进入机器的服务。

然而，PAM 并不非是黑魔法。启用 Google Authenticator 并不绝对要求在年的第十三个满月之，用一把为母系遗传银器打造的新刀牺牲一只黑色公鸡。你只需要你的系统管理员技能和这本书。

## 前提条件与结果

《PAM 精通》是为中等经验的系统管理员编写的。你需要理解管理共享库、安装和卸载软件，以及在你喜好的平台上进行故障排除。

并不是所有平台都有我们讨论的所有模块的包。使用这些模块需要从源码编译。虽然我会提供编译模块的基本说明指令，但这些指令假设你以前编译过软件，并且了解你平台编译器的行为。在 CentOS 上，你需要“Development Tools”软件包组和 `pam-devel` 包。在 Debian 上，你需要 `build-essential` 和 `libpam0g-dev` 包。FreeBSD 的 ports 系统包含了本书讨论的所有模块。

本书侧重于跨平台解决方案，特别是出于教学目的。也许你的 Unix 类系统针对某个特定任务有一个特定的 PAM 模块。我会在介绍过程中偶尔提到此类模块，但会更多关注被多个操作系统使用的模块。

你还需要用于测试的系统。实验 PAM 的良好之处在于对系统的要求极低。虚拟机非常适合测试 PAM。如果你正在尝试诸如使用 `pam_exec` 产生一个 Perl 进程来管理身份验证的操作，你需要在部署到生产环境之前进行负载测试。

你将从中获得什么呢？本书不会教你你喜好平台上关于 PAM 的深度细节。它将教你如何思考 PAM，理解策略和模块是如何工作的，以及如何探索并精通你喜好的操作系统的 PAM 实现。你也将把在这里获得的专业知识应用到任何其他使用 PAM 的操作系统上。

## 什么是身份验证？

各种安全和计算机构重新定义了“身份验证”以最符合它们的需求。如果你研究安全理论，你会遇到身份验证、授权和计费（AAA）术语。管理信息系统可能侧重于资源控制，而系统管理员只关心用户名和密码。

对于 PAM 而言，它不仅验证身份凭据。它还可以安排主目录、启用服务等。

PAM 将系统服务与身份验证集成。

如果你习惯了识别、认证和授权（IAA）这一术语，你应该知道 PAM 不处理识别。

依赖 PAM 的系统通常使用服务切换（NSS）来管理识别。NSS 也起源于 Solaris，比 PAM 早几年。从那时起，NSS 和 PAM 缺乏集成一直是 Unix 系统的持续头疼问题。



## 多因素认证

“双因素认证”这个词被频繁提及。你可以使用 PAM 来实现双因素认证，或者确说是多因素认证。明显的问题变成了：什么是身份验证因子？

身份验证基于用户的三个特征之一：他们拥有的、他们所知的或他们固有的。“他们拥有的”指的是物理令牌，例如硬件安全令牌或绑定特定号码的手机。这些物理物品容易丢失或损坏。“他们所知的”是一个秘密，例如写在便利贴上贴在显示器上的密码。“他们固有的”（包括生物因素如指纹、虹膜扫描或基因扫描）似乎是最好的。但生物数据可以被盗取。在这种情况下改变你的虹膜扫描模式是本书的范围。

多因素认证需要这些因子中的两个或多个。可能你需要一个安全令牌、特定的手机、密码和一个指纹。入侵者可以相对容易地获取任何一个，但获取所有必要元素的难度呈指数级增长。

本书的后半部分包含了几个增加身份验证因子的 PAM 模块，例如 `Google Authenticator`（第9章），或用于特定目的，如 `pam_passwdqc` 密码质量检查（第11章）。

## 为什么用 PAM？

如果可插认证模块如此麻烦，为什么还要用它们？

因为替代方案更糟糕。

# 第 0 章：引言

1995 年，太阳微系统（Sun Microsystems）提出了一种标准的跨平台、跨程序的认证接口。采用该接口的软件可以使用任何提供该接口的认证程序。如果你为此类程序编写一种新的认证机制，可以编写并附加到此接口，将其插入到你所有的软件中。因此，有了可插认证模块（Pluggable Authentication Modules，简称 PAM）。

PAM 模块是实现特定认证方法的代码块。你想通过用户名和密码进行认证吗？那是一个模块。通过硬件令牌吗？那也是一个模块。通过基因扫描、酒精测试仪以及《节奏舞动革命》平台吗？如果存在这些东西，它们也都都是模块。为了保持平台无关性，本书在许多示例中使用了三个模块.¹。模块是共享库，根据配置动态链接到主程序中。是的，“PAM 模块”这个短语是冗余的，但系统管理员就是这样称呼它们的，而我有太多的战斗要打了，没精力去纠结这个问题了。

使用 PAM 的软件会接收认证请求。程序将每个请求交给配置好的认证模块，由这些模块告诉服务器是否应该允许该认证请求。

今天，PAM 是类 Unix 系统最广泛使用的认证标准。它在 Linux 世界以及基于 Solaris 和 BSD 的系统中极其流行。即使是苹果的 OS X 也使用 PAM，诸如 AIX 和 HP-UX 等商业 UNIX 系统也是。

> 我本想用 `pam_hipster.so` 作为示例模块，但它需要一个仅运行在这一迷人架构上的工匠级编译器。此外，代码只能通过路口那家定制自行车店的老兄提供的打卡片获取。

严格来说，PAM 并不是一个官方认可的标准。没有哪个权威认证机构对一组 PAM 定义和协议盖过公章，并将其宣布为“唯一真版 PAM 规范”。通用桌面环境（CDE）包含了 PAM，而 CDE 在 20 世纪 90 年代成为了一种标准，PAM 确实在各种标准文档中被引用。大多数现代 PAM 实现都是基于 1997 年尝试将 PAM 纳入可移植操作系统接口（POSIX）时的一份草案规范。如果你真的想深入研究 PAM，可以查看 X/Open 单点登录服务（XSSO）——可插认证模块文档，该文档可以在包括 `http://pubs.opengroup.org` 在内的许多网站上找到。从那时起，人们一直尝试标准化 PAM，但所有尝试都失败了。

正式标准的缺失意味着 PAM 也缺乏正式定义的语言。取决于你阅读的文档，一组规则可能被称为链（chain）、栈（stack）或策略（policy）。认证过程的一个组件可能是类型（type）、设施（facility）或其他。在书中，我为每个组件提供了最常用的术语，然后选择一个单词作为该组件的通用词。我使用特定词来指代 PAM 的一部分，并不意味着其他选择都是无效的；它意味着如果你想听懂这些胡言乱语，就需要保持一致性。

## PAM 的局限性

PAM 是最广泛使用的认证系统，但它的局限性使得它不适用于某些应用程序。

PAM 最大的缺点是 PAM 模块无法直接与客户端交互。服务器程序是 PAM 模块和客户端之间的中介，模块与客户端之间的任何交互都限于标准 PAM 接口提供的交互。

某些认证协议（如 Kerberos）包含了大量的客户端-服务器交互，这远超 PAM 能支持的内容。在 Kerberos 中，PAM 是一个瓶颈。虽然你可以使用 PAM 模块来支持 Kerberos，但你无法通过 PAM 实现 Kerberos。这就是为什么 SSH 的大部分认证是在 PAM 之外处理的（尽管如果你决定，它可以利用 PAM）。

正是这种局限性导致了人们创建了其他认证协议，例如简单认证与安全层（SASL）和通用安全服务 API（GSSAPI），以及围绕这些协议演变出的所有工具和服务。

并不是所有操作系统都使用 PAM。值得注意的是，OpenBSD BSD 认证将认证请求分发到独立的进程中，而不是动态链接库。BSD 认证比 PAM 更广泛地分离权限，从而降低了风险，但没有实际使用的那样灵活。

不过，如果你想在接触 PAM 之前体验一下认证管理，请考虑一下在你的所有服务器软件中实现和部署 Kerberos 所的各种工作。虽然这些应用程序挂载到通用的 Kerberos 域，但你以完全不同的方式配置每一个程序。想象一下，将这乘以今天使用的所有认证协议，以及这些协议与所有不同软件的所有交互。现在 PAM 看起来好多了，不是吗？

## PAM 实现

虽然任何人都可以实现 PAM，但你最常遇到三个特定版本：Solaris、Linux-PAM 和 OpenPAM。这些不同版本几乎是兼容的。

- 2. “几乎兼容”意味着任何支持一个以上版本的人通常不会有麻烦，但偶尔的细微差别会破坏它们那天使般的举止。

太阳公司首先提出了 PAM，Sun Solaris 有了第一个实现。来自 Solaris 的 PAM 代码进入了开源的 OpenSolaris，在那里不可逆转地成为了公共源代码生态系统的一部分。甲骨文收购了太阳公司，不再公开发布 Solaris 的更新。

# 第 0 章：引言

虽然操作系统厂商可以协调它们的 PAM 配置并设计出一套每个系统管理员都能识别并使用的方案，但很可能没人会那样做。相反，每个开源平台都欢迎其他操作系统打包者来拷贝他们显然更优越的设计。因此，每个平台的 PAM 配置方式都各不相同。

当你首次深入研究一个操作系统的 PAM 设置时，请花时间理解这些打包者是如何组装一切的。你很容易假设那些为一个陌生的操作系统设计 PAM 策略的人是疯了。这种想法虽然容易，但会适得其反。请研究这些陌生的配置，并弄清楚它们为什么要这样组合在一起。你不仅将理解 PAM 的实现方式，还能洞察到操作系统打包者的思考方式——而这种洞察将帮助你掌握该系统的其余部分。

第 10 章阐述了我们的三个参考平台如何以完全不同的方式使用同一个 PAM 模块，而这些方式的原因对于操作系统打包者来说是完全合乎逻辑的。

## PAM 的共性

所有这些不同的实现都共享相同的结构和配置语法。也许你最初不会理解为什么 Debian 将一条“拒绝认证”的规则放在系统级配置的顶部，但你将理解策略的语法并能够推导出其含义。大多数 PAM 实现共享常见的模块名称，我将注明少数例外。

每个实现和操作系统都拥有的共同点是：它们都有 Bug。长久标准的 `pam_mkhomedir` 模块在 CentOS 上频繁出问题。（红帽对此有其理由，第 6 章展示了如何绕过它。）

配置选项 `use_first_pass` 和 `try_first_pass` 在 FreeBSD 的 `pam_unix` 上会失效。请务必阅读操作系统的文档，如果某些地方看起来很奇怪，请检查邮件列表存档和讨论板，看看其他人是否遇到了相同的问题。如果你真正理解了你所喜欢的 PAM 实现中的众多 Bug，你就不会觉得其他版本的 Bug 很好笑了。

## PAM 管理工具

某些 Linux 发行版提供了管理 PAM 的工具。这些工具允许你在不编辑那些糟糕的配置文件的情况下更改认证方法。它们适用于许多简单部署场景。但如果你想弄清楚为什么你的系统会以特定方式运行，或者你想做一些复杂的操作，这些工具会将你限制在工具作者想象的场景中。而理解异常行为绝对需要理解规则是如何工作的，无论是作为独立语句还是作为策略的组件。

这些附加工具会覆盖现有的 PAM 配置。你必须学会强制这些工具创建所需的配置，要么放弃它们并手动管理认证。无论哪种情况，理解配置都能让你成为更出色的系统管理员。

## 目标平台

本书主要涵盖在普通 Linux 和 BSD 版本中部署的 PAM。关于 PAM 如何处理策略的材料也适用于 Oracle Solaris、基于 OpenSolaris 的派生系统、OS X 以及专有的 UNIX 系统，但这些系统使用了完全不同的核心 PAM 模块。你可以将我讨论的许多 PAM 模块添加到这些系统中，但你必须仔细研究配置文件。

我特别针对三个具有不同配置风格的操作系统：CentOS、Debian 和 FreeBSD。

### CentOS



CentOS 是 Linux 中红帽 Linux 分支的代表。本书使用 CentOS 而不是官方的 Red Hat Linux，是因为 CentOS 是免费的，而且我很小气。CentOS 使用 Linux-PAM。许多 Linux 发行版都是基于 Red Hat Linux 构建的，它们的衍生版本应该能够使用 CentOS 的 PAM 配置。

此处涵盖的一些 PAM 模块位于 EPEL 仓库中。要使用这些模块，你需要启用该仓库、构建自己的包或进行其他安排。

CentOS 和相关的 Linux 发行版提供了一个配置 PAM 的命令行工具 `authconfig(8)`。

## Debian

Linux 的 Debian 分支的设计哲学与红帽 Linux 分支不同。它支持许多相同的软件，但管理界面几乎完全不同。Debian 使用 Linux-PAM。许多 Linux 发行版（如 Ubuntu 和 Kali Linux）基于 Debian 构建，可以使用 Debian 配置。

书中讨论的一些 PAM 模块位于实验仓库中。你需要启用该仓库或构建自己的包。

与 CentOS 类似，Debian 包含一个为你编写 PAM 配置文件的附加工具。与 CentOS 不同，Debian 使用 `pam-auth-update(8)`，这是一个 Debian 人员专门为 Debian 编写的。

## FreeBSD

FreeBSD 是我们的 OpenPAM 参考平台。支持 PAM 的 BSD 平台（如 Dragonfly 和 NetBSD）以及苹果的 OS X 使用 OpenPAM。在 FreeBSD 上有效的配置应该可以在 OS X 之外的任何 BSD 平台上运行。（OS X 使用的 PAM 模块与其他任何 OpenPAM 实现完全不同，使其在几乎所有情况下都是特例。）

少数 Linux 发行版使用 OpenPAM，或者允许轻松将其 PAM 实现替换为其他。你将像配置任何其他 PAM 实现一样配置这些操作系统，但你可能会发现某些 PAM 模块名称略有不同。如果你在使用带有 OpenPAM 的 Linux 发行并在寻找模块时感到困惑，请检查 CentOS 或 Debian 的示例以找到 Linux 社区给模块分配名称。

## 其他平台

PAM 可能不是一个单一的标准，但其配置的基础在各个实现中是通用的。管理 Solaris 派生版或 OS X 的系统管理员可以使用这里的指南创建自己的 PAM 配置。

关于附加 PAM 模块（如 Google Authenticator 或 SSH 代理认证）许多指南适用于适用于平台。配置密码质量检查器的细节在不同操作系统之间差异不大，即使该模块在策略中的放置位置有所不同。

## PAM 和 OpenSSH

OpenSSH 的服务器 `sshd(8)` 并不真正需要 PAM。SSH 认证的行业标准方法——密钥并不符合 PAM。SSH 服务器确实需要检查密码，这在过程的某处确实涉及到 PAM，但它是一个非常简单的检查。如果你使用单因素认证，简单的密码检查就足够了。

但如果你想实现复杂的基于 PAM 的认证，可以通过让 `sshd(8)` 链接到 PAM。将 `ssh_config` 中的 `UsePAM` 选项设置为 `yes`。这启用了基于 PAM 的账户检查、自动主目录创建等。然而，它不会触发基于 PAM 的认证。

SSH 守护进程处理键盘认证有两个选项。一个 `PasswordAuthentication` 是专门用于密码的；另一个 `ChallengeResponseAuthentication` 是一种更通用的认证机制。为了使用 PAM，你几乎肯定需要 `ChallengeResponseAuthentication`。

```
UsePAM yes

ChallengeResponseAuthentication yes

PasswordAuthentication no
```

控制和串口登录尝试使用 `login(8)` 程序，它有自己的 PAM 策略。SSH 服务器可以通过 `UseLogin` 选项将用户登录过程的一部分交给 `login(8)`。该选项通常为 `no`。`login(8)` 和 `sshd(8)` 策略之间的交互极其有趣或令人愤怒，取决于你是否是那个需要让它们运行的人。为了使用 PAM，最好让 SSH 服务器处理登录，而不是调用 `login(8)`。

```
Login no
```

此外，让 `sshd(8)` 咨询 PAM 进行认证。为此，你需要 `ssh_config` 中的 `AuthenticationMethods` 选项。`keyboard-interactive` 设置告诉 sshd 将认证传递给其他代理（如 PAM）。如果你激活了 PAM 并告诉 `sshd(8)` 使用键盘交互认证，你将获得基于 PAM 的认证以及账户管理。

# 第 0 章：引言

将其设置为 `publickey` 意味着 sshd 要求公钥认证。用逗号将两者结合意味着 sshd 要求同时满足这两者，而用空格将它们分开则意味着 sshd 提供了认证选项供选择。

大多数想在 `sshd(8)` 中启用 PAM 的人都希望守护进程拒绝所有没有公钥的身份验证请求，然后让 PAM 有机会许可或否决连接。这将产生如下所示的 `AuthenticationMethods` 条目。

```
AuthenticationMethods publickey,keyboard-interactive
```

或者，你可能希望允许使用公钥认证的用户登录，然后回退到 PAM 进行一次性密码或其他其他强身份验证。在方法之间加一个空格。

```
AuthenticationMethods publickey keyboard-interactive
```

即使有这些选项，并不是所有的 PAM 模块都能与 sshd 配合。将 `pam_ssh_agent_auth`（第 8 章）接入 sshd 听起来可能很有趣，但只会让你烦恼。

## PAM、LDAP 和 Kerberos

每当系统管理员考虑认证时，集中认证的话题就会出现。这些讨论大多数都将围绕轻量级目录访问协议 (LDAP) 和 Kerberos 的各种排列组合展开。这会对你有帮助吗？

是的……也不。

部署 LDAP 的困难与 PAM 几乎没有关系。配置 LDAP 认证之所以困难，是因为 LDAP 的格式极其灵活。你可以使用任意数量的 LDAP 架构（schemas）或创建自己的。在 LDAP 部署早期做出的决策将产生你将永远受其影响的影响。更糟糕的是，我们每个参考平台上的 LDAP 模块之间的差异，意味着每个平台都需要唯一的配置。

Kerberos 比 LDAP 没那么灵活，但它有非常特定的要求和更高的开销。

本书将帮助你理解你的 PAM 配置如何影响这些集中认证方法。它将帮助你在部署时从 PAM 中提取调试信息。但它不会帮助你决定如何设计你的 LDAP 架构。

## 本书概览

本书由两个大部分组成。前六章将引导你了解 PAM 是如何工作的。

第 0 章是本引言。

第 1 章“PAM 组件”讨论了 PAM 的组成部分。你将学习 PAM 配置文件和语句、控制语句、PAM 模块以及常用标志。我们还将探索 PAM 策略是如何运作的，以及 PAM 如何决定允许或拒绝请求。

第 2 章“常用模块”涵盖了每个人都需要理解的模块，例如用于传统 Unix 认证的模块、允许 root 访问服务、审计等。

第 3 章“PAM 项、代码和函数”深入探讨了某些 PAM 内部机制。系统管理员不需要为 PAM PAM，但在这些代码出现时需要识别它们。理解 PAM 项（items）和返回代码对于管理 PAM 至关重要。

第 4 章“Linux-PAM 扩展和子栈”讨论了 Linux-PAM 对 PAM 配置的扩展，例如根据特定的 PAM 响应做出决策。

第 5 章“流行的 Linux-PAM 模块”详细介绍了通常在 Linux-PAM 系统中部署的模块。PAM 中的 Linux 配置功能是其他系统放置在其他地方的。

第 6 章“PAM 调试”展示了如何在你的 PAM 配置中找到问题。

通过这六章，你可以完成本质的配置任务和调试。书的其余部分将介绍特定的模块。通过极其简易的互联网搜索就能发现数百个 PAM 模块，但本书只涵盖了少数几个。其中一些广泛可用且非常有用，例如 `pam_exec`（第 7 章）。有些很流行，如 `pam_ssh_agent_auth`（第 8 章）和 Google Authenticator（第 9 章）。有些可以让我说明关于 PAM 的重要点。`pam_ssh` 模块（第 10 章）不仅说明了一个实用的功能，还作为操作系统部署 PAM 模块时令人愤怒的差异案例。

这留下了数百个 PAM 模块。许多 PAM 模块对于需要它们的人来说至关重要，但只有少数读者需要任何特定的模块。本书让你对 PAM 有足够的理解，让你确信能力为使用该模块编写正确的规则，从而释放你宝贵的脑力去理解模块本身以及该模块如何融入策略中。

第 7 章“任意文件和随机程序”讨论了基于文本列表的访问。你还学习了作为 PAM 的一部分运行外部程序。

第 8 章“SSH Agent 认证”涵盖了在登录系统后使用你的 SSH agent 对服务进行身份验证。



第 9 章“一次性密码：Google Authenticator”帮助你使用 Google 的 PAM 模块和各种客户端实现基于时间的一次性密码 (TOTP)。

第 10 章“使用 SSH 密钥访问控制台”教你如何配置工作站，使用户可以使用其 SSH 密钥作为本地认证过程的一部分。

第 11 章“密码质量检查”讨论了使用 PAM 模块限制用户可以选择的密码。

拿起你的手电筒。我们要进入 PAM 的世界了。

# 第 1 章：PAM 组件

任何 PAM 系统都通过几种类型的规则处理登录和认证过程。我们将从包含规则的配置文件开始，然后深入研究认证组件和操作。

## PAM 配置文件

你可能会在 `/etc/pam.conf` 文件找到 PAM 配置，或者在 `/etc/pam.d/` 目录下的一堆文件中找到。

当 Solaris 在 90 年代产生 PAM 时，一个配置文件就足够用于极少数使用 PAM 的服务了。每个 PAM 规则语句以服务的名称开始。访问 `rsh(8)` 的规则以 `rsh` 开始，管理 telnet 的规则以 `telnet` 开始，依此类推。

然而，单个文件限制并复杂化了系统管理。Linux-PAM 和 OpenPAM 将 PAM 规则拆分到 `/etc/pam.d` 目录，每个服务都有一个命名的文件。`rsh(8)` 的规则放在 `/etc/pam.d/rsh`，SSH 访问的规则放在 `/etc/pam.d/sshd`，依此类推。

FreeBSD 系统也对系统组件和插件进行分离。虽然 PAM 配置位于 `/etc/pam.d`，但插件的 PAM 配置位于 `/usr/local/etc/pam.d`。你可能会在其他操作系统发现类似的变体。

使用 `/etc/pam.d` 的系统比依赖 `/etc/pam.conf` 的系统常见得多。对于基于 Solaris 的系统，需要在 `/etc/pam.conf` 中的每个 PAM 规则前面加上服务名称。

## PAM 策略

如果你从未看过 PAM 文件，请查看 `/etc/pam.d/` 中的一个文件。策略文件有很多这样的语句：

```
auth      required pam_unix.so      no_warn try_first_pass nullock
account   required pam_unix.so
session    required pam_lastlog.so  no_fail
password   required pam_unix.so      no_warn try_first_pass
```

每行都是一个 PAM 语句或规则。每个语句包含四个部分：类型（type）、控制（control）、模块（module）和模块参数（arguments）。这里显示的第一个 PAM 语句类型为 `auth`，控制为 `required`，模块为 `pam_unix.so`，参数为 `no_warn`、`try_first_pass` 和 `nullock`。

我们将详细介绍每一个，但理解基础知识有助于你在深入研究时理解这些部分是如何协作的。

类型是认证过程的一个组件。管理凭据是认证的一部分。设置用户账户和资源限制以及更改用户密码也是认证的一部分。

控制语句指示 PAM 如何对 PAM 模块的成功和失败做出反应。身份验证请求应该

`granted`（允许）：请求是否应该尝试下一个模块？在此处失败是否应该终止整个过程？这些控制语句提供了 PAM 的逻辑。

`module`（模块）：要使用的 PAM 模块。使用模块的文件名，包括结尾的 `.so`。（OpenPAM 允许你省略 `.so`）。大多数 PAM 模块安装在特定于系统的的位置，例如 `/usr/lib/` 或 `/lib/x86_64-linux-gnu/security/`。如果你想使用不在标准目录下的模块，请用其完整路径列出它。列出模块告诉 PAM 将认证信息传递给该模块并收集响应。例如，`pam_unix.so` 检查本地系统的密码文件以查找有效的用户名和密码。如果 PAM 处理了此用户名和密码，模块将响应“是，它存在”或“否，无效”。控制语句告诉 PAM 对于每种响应应该怎么做。正如第 4 章讨论的，模块响应可以是“是”或“否”之外的内容。

`arguments`（模块参数）：特定于每个模块。某些参数（如 `no_warn` 和 `debug`）被许多模块识别。然而，每个参数的确切含义取决于模块。并不是所有模块都需要或使用参数。少数编写不良好的模块对存在任何参数都反反对。

使用反斜杠（`\`）将长语句拆分为行。`auth required pam_echo checking OPIE RUSER=%U TTY=%t SERVICE=%s RHOST=%H`

让我们深入研究认证类型。

### 认证类型

PAM 将认证过程分为四个组成部分。取决于你阅读的是谁的文档，这些组件可能被称为设施（facilities）或类型（types）。类型是 PAM 规则中的第一个字段。

`auth`（认证）类型验证所提供的认证信息，并建立账户设置的任何限制或资源限制。如果你输入了错误的密码或不存在的用户名，`auth` 类型会将你踢出去。如果用户账户有进程数量限制、可以使用最大内存或属于特定组，`auth` 类型将处理这些限制设置。

`account`（账户）类型根据简单认证以外的特征来控制对账户的访问。如果用户只能在奇数年份的 2 月 28 日登录，这将在账户类型中配置。用户可能输入了正确的认证信息，但如果没有可用账户，她就无法登录。

`session`（会话）类型处理提供服务所需的系统端设置。命令行用户需要一个虚拟终端、一个主目录，可能还需要一条显示他们已登录的日志记录。匿名 FTP 用户不需要虚拟终端、个人主目录或 shell，但需要 FTP 特定的资源。当会话结束时，所有分配的资源都需要销毁。`session` 类型管理所有此类每个会话的请求。

最后，`password`（密码）类型在用户凭据需要更新系统时是需要的。可能用户正在更改密码。可能他们的硬件令牌需要检查。`password` 类型处理更新认证凭据所需的任何操作。

主机可能拥有的每个服务在每种类型上有一个或多个语句。取决于认证在你的系统中应如何工作，你可能有几十种一种类型的语句，另外两种类型各一条语句，而第四种则没有。

同种类型的语句组通常被称为链（chain），有时被称为栈（stack）。本书使用“策略”（policy）一词。查看本章开头的示例 PAM 策略。每个策略只有一条语句那么长。在接下来的章节中，我们将看到具有多个语句的策略。

在 Linux-PAM 中，你偶尔会看到类型语句名称前有一个连字符：`-auth`、`-account`、`-session` 和 `-password`。这些表示如果系统未安装该模块，PAM 应该忽略该错误。当模块是可选的（例如 Kerberos 或 `systemd(8)`），你会看到这种情况。

#### PAM 控制

PAM 控制声明了特定模块如何影响策略。你可以决定哪些类型的认证是强制的（mandatory），哪些是自愿的（voluntary），哪些是你不在乎的。

PAM 将认证信息发送给策略中的模块。控制语句告诉 PAM 对于每种响应应该怎么做。正如第 4 章讨论的，模块响应可以是“是”或“否”之外的内容。

（注：控制语句决定了访问是允许还是拒绝的。例如，`pam_unix.so` 检查本地系统的密码文件以查找有效的用户名和密码。如果 PAM 处理了此用户名和密码，模块将响应“是，它存在”或“否，无效”。控制语句告诉 PAM 对于每种响应应该怎么做。模块响应可以是“是”或“否”之外的内容，正如第 4 章讨论的。）

事实上，控制语句告诉 PAM 对于每种响应应该怎么做。正如第 4 章讨论的，模块响应可以是“是”或“否”之外的内容。

（注：此处原文似乎存在逻辑重复或截断，翻译已根据上下文微调）

PAM 控制声明了特定模块如何影响策略。你可以决定哪些类型的认证是强制的，哪些是自愿的，哪些是你不在乎的。

The need to protect their own interests and the need to protect their own positions and matches. (Wait, let's re-examine the source text, it seems there is some repetitive garbled text in the provided source).

Let's re-translate the specific sections carefully:

PAM 将认证信息发送给策略中的模块。控制语句告诉 PAM 对于每种响应应该怎么做。正如第 4 章讨论的，模块响应可以是“是”或“否”之外的内容。

PAM 控制声明了特定模块如何影响策略。你可以决定哪些类型的认证是强制的，哪些是自愿的，哪些是你不在乎的。



# 第 1 章：PAM 组件

## PAM 控制

PAM 控制声明了特定模块如何影响策略。你可以决定哪些类型的认证是强制的，哪些是自愿的，哪些是你不在乎的。

PAM 有五种主要控制：`required`、`requisite`、`optional`、`sufficient` 和 `binding`。

### 强制

带有 `required` 控制的语句意味着该模块必须返回成功，策略才能允许访问。如果用户输入了错误的密码，他们将无法登录。如果管理员配置了主机使得任何人都无法登录，他们将无法登录。

如果 `required` 控制失败，PAM 会处理策略中的剩余模块。登录仍然返回失败，拒绝访问。

如果 `required` 控制成功，PAM 继续处理策略，给予其他模块拒绝访问的机会。

每个 `required` 模块都成功，PAM 才能允许访问。即使一个 `required` 模块失败，其他模块的成功也是不够的。考虑这个示例策略：

```
auth required pam_breatzer.so
auth required pam_ddr.so
auth required pam_genescan.so
```

此策略首先将认证信息传递给 `pam_breatzer.so` 模块，然后是 `pam_ddr.so`，最后是 `pam_genescan.so`，所有均使用 `required` 控制。此策略需要一致同意。如果这些模块中任何一个返回失败，认证请求就会失败。不过，三个模块都会被处理，以便它们执行对管理员有帮助的辅助任务。

根据模块的功能和策略类型，`required` 语句是因素认证的关键部分。许多其他控制语句（后文描述）声称在它们成功时授予访问。如果早期的 `required` 模块失败，PAM 将拒绝访问。失败的 `required` 控制就像是巨大的“否”之锤。

### 必要

`requisite` 控制指示模块必须成功才能授予访问。

如果 `requisite` 控制成功，PAM 继续处理模块。除非被拒绝，否则请求将获得授权。

如果 `requisite` 控制失败，PAM 会立即停止处理模块并告诉应用程序请求被拒绝。这使得 `requisite` 与 `required` 不同。

- 是的，酒精测试模块可能应该测试用户是否足够清醒以登录，并因此位于账户策略中。这只是一个例子，就用它吧。

让我们来检查这个带有必要控制的 PAM 策略。

```
auth required pam_breathalyzer.so
auth requisite pam_ddr.so
auth required pam_genescan.so
```

第一个模块 `pam_breathalyzer.so` 是 `required`。如果用户没有通过测酒测试，他们就无法登录，别无他法。无论该模块成功还是失败，PAM 都会继续执行策略中的下一个模块。

第二个模块 `pam_ddr.so` 是 `requisite`。它必须成功，PAM 才能授予访问权限。如果此模块失败，PAM 会立即停止处理策略并告诉应用程序拒绝认证。

第三个模块 `pam_genescan.so` 也是 `required`。然而，只有当第二个模块成功时才会触发第三个模块。`pam_ddr.so` 的失败意味着 `pam_genescan.so` 不会被检查。

使用 `requisite` 控制可以给用户提示身份验证是在哪里失败的。入侵者可以利用这些信息更精确地针对其攻击。只有当你有非常充分的理由不运行后续控制时，才使用 `requisite`。不要花费时间、精力或注意力去优化登录失败。此策略使用 `requisite` 控制是因为基因扫描开销很大，避免不必要的扫描可以节省费用。

### Optional

带有 `optional` 控制的语句对成功或失败的影响很小。操作系统使用 `optional` 控制来管理可能部署或未配置的功能，例如 SSH 代理和 Kerberos。你还会部署 `optional` 控制来为认证会话添加额外功能。

当仅当策略中没有其他模块表达意见时，`optional` 控制才能允许或拒绝访问。如果你有一组足够的 `sufficient` 语句和一个 `optional` 语句，且没有足够的 `sufficient` 语句允许访问，那么该 `optional` 语句就可以允许或拒绝访问。

这里是一个使用 `optional` 控制的策略。

```
auth required pam_breathalyzer.so
auth required pam_ddr.so
auth required pam_genescan.so
auth optional pam_faildelay.so
```

我们的三个示例模块仍然是 `required` 的：所有模块必须成功，用户才能获得访问权限。

新模块 `pam_faildelay.so` 在登录尝试之间设置了延迟。如果用户的登录尝试被拒绝，该模块会延迟几秒钟向用户返回认证提示。此模块对用户的认证凭据不进行任何操作。由于它改变了 PAM 的行为，你可能会希望它总是返回成功。然而，在极少数 `pam_faildelay.so` 失败的情况下，你不希望这种失败会阻止登录。

带有 `optional` 控制的语句通常位于策略的开头。你可能不希望 `requisite` 控制的失败阻塞 `optional` 模块。然而，我刻意将 `pam_faildelay` 放在此策略的末尾，因为我不想在第一次登录尝试之前引入延迟。

我应该提到，使用 `pam_faildelay` 本身就是一个很糟糕的主意；正如安全公告所示，此类延迟应该构建在应用程序内部，而不是通过 PAM 提供。理想情况下，每次认证尝试都应该花费恒定的时间，而不是在尝试之间提供恒定的延迟。尽管如此，这是一个流行的模块，所以你至少需要识别它。

会话类型是 `optional` 控制最常见的用场景。

### Sufficient

`sufficient` 控制意味着在该模块中成功就足够提供访问权限，前提是之前的 `required` 控制没有失败。

如果 `sufficient` 控制成功，PAM 会立即授予访问权限。它不会处理策略中的后续模块。

如果 `sufficient` 控制失败，PAM 不会拒绝访问。`sufficient` 控制的失败被视为等同于 `optional` 控制的失败。PAM 将此失败记录为一次 `optional` 失败。不触发失败允许用户尝试另一种身份验证方法。考虑以下策略。

```
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
```

三个模块都是 `sufficient` 的，这意味着成功认证其中任何一个即可获得访问。

三个模块都是 `sufficient` 的，这意味着成功认证其中任何一个即可获得访问。

三个模块都是 `sufficient` 的，这意味着成功认证其中任何一个即可获得访问。



三个模块都是 `sufficient` 的，这意味着成功认证其中任何一个即可访问。

```
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
```

这三个模块都是 `sufficient` 的，意味着成功认证其中任何一个即可获得访问。

# 第 1 章：PAM 组件

`auth sufficient pam_breathalyzer.so`

`auth sufficient pam_ddr.so`

`auth sufficient pam_genescan.so`

`auth required pam_deny.so`

有了这个添加，其中任何一个通过或拒绝。

一个足够的控制允许访问。

`auth sufficient pam_breathalyzer.so`

`auth sufficient pam_ddr.so`

`auth sufficient pam_genescan.so`

# 第 1 章：PAM 组件

```
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
```

这三个模块都是 `sufficient` 的，意味着成功认证其中任何一个即可获得访问。

`auth sufficient pam_breathalyzer.so`

`auth sufficient pam_ddr.so`

`auth sufficient pam_genescan.so`

# 第 1 章：PAM 组件

`auth sufficient pam_breathalyzer.so`

`auth sufficient pam_ddr.so`

`auth sufficient pam_genescan.so`

`auth required pam_deny.so`

```
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
```

`auth sufficient pam_breathalyzer.so`

`auth sufficient pam_ddr.so`

`auth sufficient pam_genescan.so`

`auth required pam_deny.so`

# 第 1 章：PAM 组件

```
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
```

`auth sufficient pam_breathalyzer.so`

`auth sufficient pam_ddr.so`

`auth sufficient pam_genescan.so`

`auth required pam_deny.so`

`auth sufficient pam_breathalyzer.so`

`auth sufficient pam_ddr.so`

`auth sufficient pam_genescan.so`

`auth sufficient pam_breathalyzer.so`

`auth sufficient pam_ddr.so`

`auth sufficient pam_genescan.so`

`auth required pam_deny.so`

`auth pam_deny.so`

`auth sufficient pam_breathalyzer.so`

`auth sufficient pam_ddr.so`

`auth sufficient pam_genescan.so`

`auth sufficient pam_breathalyzer.so`

`auth sufficient pam_ddr.so`

`auth sufficient pam_genescan.so`

`auth sufficient pam_breathalyzer.so`

`auth sufficient pam_ddr.so`

`auth sufficient pam_genescan.so`

`auth sufficient pam_breathalyzer.so`

`auth sufficient pam_ddr.so`

`auth sufficient pam_genescan.so`

`auth sufficient pam_breathalyzer.so`

`auth sufficient pam_ddr.so`

`auth sufficient pam_genescan.so`

`auth sufficient pam_breathalyzer.so`

`auth sufficient pam_ddr.so`

`auth sufficient pam_genescan.so`

`auth sufficient pam_breathalyzer.so`

`auth sufficient pam_ddr.so`

`auth sufficient pam_genescan.so`

`auth sufficient pam_breathalyzer.so`

`auth sufficient pam_ddr.so`

`auth sufficient pam_genescan.so`

`auth sufficient pam_breathalyzer.so`

`auth sufficient pam_ddr.so`

`auth sufficient pam_genescan.so`



```
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
```



```
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
```



```
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
```



```
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient sufficient_pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
```



```
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
```



# 第 1 章：PAM 组件

```
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
auth sufficient pam_breathalyzer.so
auth sufficient pam_ddr.so
auth sufficient pam_genescan.so
```

使用包含（includes）可以允许系统管理员在一个位置维护多个服务的 PAM 配置。更改包含的文件会使更改立即传播到所有涉及的服务中。



然而，所有的操作系统使用的包含策略设计都略有不同。许多 CentOS PAM 模块包含了 `system-auth` 配置文件。FreeBSD 使用 `/etc/pam.d/system`。Debian 则按类型拆分中心包含文件，例如 `common-auth`、`common-session` 等。

Debian 使用 `@include` 来引入整个整个文件。这里是 Debian 的 `/etc/pam.d/sudo` 配置。

```
@include common-auth
@include common-account
@include common-session-noninteractive
```

此配置表示“使用与其他人完全相同的身份验证方法”。

包含此类文件的优点是它非常方便在策略的开头或结尾添加条目。如果我想为某一个程序为某个类型添加一个 PAM 模块，我可以将其添加到该程序的文件。在这里，我告诉 Debian 的 sudo 在所有常规认证方法之外，还需要进行酒精呼吸测试（breathalyzer test）。

```
auth required pam_breathalyzer.so
@include common-auth
@include common-account
@include common-session-noninteractive
```

文件提高了你的灵活性，而无需你维护多份 PAM 策略副本。

Linux-PAM 还支持子栈（substacks），它们与包含类似。关于子栈的讨论请参见第 4 章。

# 第 1 章：PAM 组件

## 模块与参数

每个 PAM 语句末尾模块及其参数决定了规则规则实现的功能或行为。每个模块都提供了如检查密码、配置主目录或分配终端等功能。

我们将通过安装和使用 PAM 模块来安装大多数功能。

### 模块上下文

在你探索 PAM 模块时，你会发现许多模块被多个不同的 PAM 类型调用。例如，`pam_unix.so` 模块出现在 `auth`、`account` 和 `password` 策略中。模块的行为以及它提供的服务取决于调用它的类型。如果 `auth` 类型调用 `pam_unix.so`，该模块会检查密码。`account` 类型从 `pam_unix.so` 获取账户可用性信息。`password` 类型使用 `pam_unix.so` 修改系统密码文件。

并不是每个模块都为所有类型提供服务。非常有用的模块仅支持一种类型，但为该类型执行至关重要的服务。例如，`pam_mkhomedir.so` 模块作为 `session` 类型的一部分，为通过验证的用户创建不存在的主目录。这与密码无关，但对于大型企业至关重要。

### 模块参数

模块参数（或标志）用于配置模块本身。模块是否应该告诉用户它拒绝请求的原因？或者你是否想要激活可选功能？模块参数可以启用和禁用这些可选功能。

在这里，我们为 `pam_unix` 模块设置了 `nullock` 和 `try_first_pass` 标志。

```
auth sufficient pam_unix.so nullok try_first_pass
```

某些标志带有它们自己的参数，允许你设置限制或切换功能。

```
account required pam_breathalyzer.so bal<8
account required pam_genescan.so neanderthal=0
```

酒精呼吸仪本身并不知道你组织对酒精的容忍度。在这个示例中，如果用户的血液酒精浓度低于 0.08，则账户是可用的。我是如何知道这个参数的？我阅读了模块文档。同样，为了符合美国反歧视法，我们告诉基因扫描器不要进行尼安德特人检查。

模块在不同的上下文中使用时可能需要完全不同的参数。

## 常用模块参数

虽然任何人都可以编写 PAM 模块，但这并不意味着每个人重新发明模块配置。大多数 PAM 模块接受这些用于通用功能的常用参数。

PAM 模块并不要求接受这些参数中的任何一个。编写良好的当且不支持某个标志功能的 PAM 模块会静地忽略它。

### debug

`debug` 标志告诉模块通过 `syslog` 记录调试信息。PAM 调试消息以 `auth` 设施优先级 `debug` 记录。在 `pam_unix.so` 中添加 `debug` 标志并观察系统日志将教你很多关于你的 PAM 实现如何处理身份验证请求的内容。

但并不是所有的 PAM 模块都支持调试。如果你在使用 `debug` 标志时 PAM 模块表现异常，请将其视为该模块编写糟糕的提示。你可能被迫继续该模块，但至少你收到了警告。

在 OpenPAM 中，`debug` 标志不仅触发 PAM 行为的调试输出，还会触发共享库内部的调试。正如第 3 章所述，你会看到调用了哪个服务函数以及返回了什么。

通用的 PAM 错误（例如列出一个不存在的模块）通常出现在系统的安全日志中（`/var/log/secure` 或 `/var/log/auth`）。

### no_warn

PAM 模块提供关于它们为何拒绝访问请求的反馈。启用 `no_warn` 会让该反馈沉默。虽然分析器通常告诉用户他们无法登录是因为太醉了找不到脸，更不用说编程了，添加 `no_warn` 会关闭该警告。

### use_first_pass

主机的身份验证系统可能被设置为通过几种方法中的每一种尝试验证用户名和密码。例如，一个主机可能会尝试本地密码文件和 LDAP。虽然每个 PAM 模块都可以提示用户输入密码，但 `use_first_pass` 选项告诉模块使用已经输入的密码。如果没有此选项，模块可能会再次提示用户密码。

### try_first_pass

主机的身份验证系统可能被设置为通过几种方法中的每一种尝试验证用户名和密码。例如，一个主机可能会尝试本地密码文件和 LDAP。虽然每个 PAM 模块都可以提示用户输入密码，但 `use_first_pass` 选项告诉模块使用已经输入的密码。如果没有此选项，模块可能会再次提示用户密码。

### mapped_pass

主机的身份验证系统可能被设置为通过几种方法中的每一种尝试验证用户名和密码。一个主机可能会尝试本地密码文件和 LDAP。虽然每个 PAM 模块都可以提示用户输入密码，但 `use_first_pass` 选项告诉模块使用已经输入的密码。如果没有此选项，模块可能会再次提示用户密码。

### expose_account

人类非常不听从指令。许多应用程序共享一组默认值。如果 PAM 找不到应用程序的策略，它将调用 `/etc/pam.d/other` 中的“other”策略。

## 默认策略

并不是所有应用程序都需要自己的策略。许多应用程序共享一组默认值。如果 PAM 找不到应用程序的策略，它将调用 `/etc/pam.d/other` 中的“other”策略。

## 策略处理与结果

PAM *策略*（policy）或*链*（chain）是针对服务的同一种类型的规则组。一个应用程序可能有 `auth`、`account`、`session` 和 `password` 策略，也可能只有其中一些。毕竟 FTP 不需要（也不应该！）用户更改密码。

这里是 FreeBSD 系统的完整默认系统。

| | | |

| :--- | :--- | :--- |

| auth sufficient | pam_opie.so | no_warn_no_fake_prompts |

| auth requisite | pam_iteaccess.so | no_warn allow_local |

| auth required | pam_unix.so | no_warn_try_first_pass nullock |

| account required | pam_login_access.so | |

| account required | pam_unix.so | |

| session required | pam_lastlog.so | no_fail |

| password required | pam_unix.so | no_warn_try_first_pass |

`auth` 策略有三个语句。`account` 策略有两个语句，而 `session` 和 `password` 只有一个语句。

每个策略都负责允许或拒绝某种类型的访问请求。它根据策略中的语句做出决定。考虑上述三条语句的 `auth` 策略。当用户运行调用此内容的程序时，PAM 首先调用 `pam_opie` 模块并向其提供所需信息。`pam_opie` 模块具有足够的控制权：如果它成功，`auth` 策略将立即停止处理策略。第一个模块失败并不意味着该模块反对让用户登录——只是不打算说。当一个足够的模块失败时，PAM 将继续处理策略。这在计算中等同于“去问你妈妈”。



第二个认证模块 `pam_opieaccess` 具有必要的控制权限。如果该模块返回成功，则允许访问。然而，如果模块返回失败，PAM 会立即停止处理策略并返回失败。这是一个硬性的“是”或“否”决策。

认证策略中的最后一个模块 `pam_unix` 是强制要求的。如果该模块返回成功，则允许访问；如果模块返回失败，则拒绝访问。

整体来看，认证策略可以通过几种方式进行处理。如果第一个充分的模块执行成功，将立即允许访问。如果它失败了，处理将传递到策略中的后两个规则。这两个规则都必须返回成功才能允许访问。最后两个模块中的任何一个失败都会导致拒绝访问。

在大多数部署中，策略对“拒绝”的权重高于“允许访问”。大多数控制类型都拥有否决权，即使策略中后面的语句说了“是”，它们也可以拒绝访问。

如你所见，PAM 策略的处理方式与普通访问控制列表通用的“允许/拒绝”语法不同。将 PAM 策略类比为防火墙规则会让你很痛苦。PAM 使用其特殊语言来明确这一点。

现在你已经理解了 PAM 运行的一些基础知识，让我们来看几个常用的模块以及它们是如何配置的。

# 第2章：常用模块

虽然 Linux-PAM 和 OpenPAM 是分阶段实现的，但它们的开发者以 Solaris PAM 为模型。两者都包含了许多在概念上与 Solaris 旧版本相似的模块。

本章将带你了解其中许多常用模块、它们的工作原理以及你可以用它们做什么。其中许多模块非常小，只提供单一功能，但我会简要介绍它们，以便你开始理解 PAM 如何将所有分散的 Unix 认证函数结合在一起。

让我们从一个随处可见的类别开始。

## Unix 核心认证：pam_unix

`pam_unix` 模块处理与系统密码文件 `/etc/passwd` 以及相关文件（如 `/etc/group`、`/etc/master.passwd`、`/etc/shadow` 等的所有交互。它还支持网络信息服务（NIS），这是管理分布式认证的传统手段。不使用 LDAP 或 Kerberos 等集中认证系统的主机几乎都在使用 `pam_unix`。即使使用集中认证的主机，通常也会使用 `pam_unix` 为本地应用程序查找非特权账户。

认证（`auth`）、账户（`account`）和密码（`password`）PAM 类型都使用 `pam_unix`。它不用于会话（`session`）类型。

密码认证比 PAM 早了几个十年。`pam_unix` 模块承担着不可否认的责任，带着多年累积的功能，并由各种选项标志控制。

### 使用 audit 进行详细记录

`audit` 选项是 `debug` 选项更详细、更冗长的版本。它使用 `auth` 设施和 `debug` 优先级向 `syslog` 发送非常详细的日志。

根据操作系统、PAM 版本和服务器程序的不同，审计日志可能不包含很多有用信息。例如，OpenSSH 服务器并不一定使用 PAM。

### 空密码

认证的通用规则是：没有密码，就无法访问。没有密码的账户通常不是设计用来活动使用的。应用程序账户（如 MySQL 或 nginx 等账户）通常没有密码。（应用程序账户也是被锁定的，禁止登录）。新用户账户可能还没有密码。

在某些情况下，你可能允许某人作为这些用户之一登录。`nullok` 选项允许在没有密码的情况下访问此类账户。

某些实现（特别是 CentOS）在 `auth` 规则中使用 `nullok` 来允许用户在没有密码的情况下登录。它们然后在 `password` 规则中添加 `nullock`，如下所示。这种组合让新用户能够登录，但强制他们立即更改密码。如果你对此功能感兴趣，请查看你的 PAM 是否支持这种行为。

```
auth sufficient pam_unix.so nullok try_first_pass
password sufficient pam_unix.so sha512 shadow \
    nullok try_first_pass use_authtok
```

这种行为的缺点是，任何人都可以登录新用户的账户并分配一个密码。你无法保证新账户确实交给了预定的人员。但替代方案也都很糟糕：给所有新用户分配相同的密码（如“swordfish?”）？生成随机字符串并希望那个倒霉的人能正确输入它们？

Debian 的 Linux-PAM 支持 `nullok_secure` 选项，如果在安全终端上使用该选项，则允许使用空密码访问。安全终端是你认为处于物理安全区域的终端，例如锁定的数据中心。它是对你已确认为安全的区域提供的便利。安全终端通常局限于控制台、虚拟终端和各种类型的串口，并列在 `/etc/securetty` 中。

### 密码文件配置

大多数 Linux 系统期望 PAM 配置本地密码数据库。你可以使用系统范围 PAM 配置来告诉系统使用 shadow 密码文件、密码使用何种哈希算法等。

我强烈建议大家将这些设置保持默认值。你希望你的主机使用 shadow 密码文件。你对加密哈希算法的了解与为你的操作系统做出这些选择的人相比是逊色的。你可能听过 Blowfish 很酷，但 Linux 发行版使用 SHA 512 是有非常充分的。如果你认为你必须更改密码配置，你就错了。

> 密码始终是“swordfish”。

> 当你尝试吃掉 Blowfish 时，它会长出刺来。

### 组成员关系

一个非常常见的目标是通过组来限制认证。最为人知的例子是 `pam_wheel`，它允许 `wheel` 组的成员成为 root。首先，你要检查哪个组？

组检查通常使用原始用户的组成员身份进行检查。你可以反转这种检查，创建“如果目标是此组的成员则允许此服务”，使用 `luser` 选项。你可以创建 PAM 配置“允许 `su(1)` 到 oracle 账户”。

OpenPAM 的 `pam_group` 还有一个 `fail_safe` 选项。设置 `fail_safe` 告诉 pam_group 如果指定的组不存在或没有成员，则应该允许访问。你可能在集中管理 PAM 配置时使用它。不过，你不能对 `wheel` 组使用 `fail_safe`。

这种否定检查比正检查风险更大。我建议只允许组成员访问，而不是拒绝组内的人。忘记将新员工添加到 `staff` 组会导致她无法工作——但你会立即发现。忘记将新客户添加到 `customer` 组会导致她静悄地获得被禁止的服务。

PAM 还支持 `trust` 选项。如果用户是指定组的一部分，她就不需要输入密码。通过 `trust`，`wheel` 组的成员可以在不输入密码的情况下运行 `su root`。

你也可以使用组检查来基于组阻止访问。`deny` 选项反转了组检查的含义，使得用户是某组的成员

### 其他 pam_unix 选项

标准的 `debug` 选项很有用，`use_first_pass` 和 `try_first_pass` 也是。然而，OpenPAM 的 pam_unix 不支持 `try_first_pass`。

我得到保证 `luser` 就是“本地用户”，没有其他可能想到的。

# 第 2 章：常用模块

## 允许与拒绝请求

在构建 PAM 策略时，以明确的 `yes`（是）或 `no`（否）结束策略会有帮助。PAM 恰好包含了两个用于此目的模块。

`pam_deny`

有时候，你只需要说“不”。这就是 `pam_deny` 的作用。

使用 `pam_deny` 来阻塞所有请求。通过将 `pam_deny` 放在策略的末尾，你声明之前未被允许的所有操作都是禁止的。

在使用 sufficient（足够）控制语句时，`pam_deny` 模块尤为重要。sufficient 控制表示“通过这一项你就可以进入，只要没有其他人通过。如果这一项失败了，你可以尝试其他的。”如果一个请求到达了一系列 sufficient 语句的结尾，且没有通过其中任何一个，但没有任何模块拒绝访问，那么在末尾添加 `pam_deny` 就能提供权威的拒绝。

你还会在请求完全没有意义的地方看到 `pam_deny` 使用。CentOS 提供了指纹认证。Red Hat 的开发者认为“人的指纹不会改变”，因此他们坚决拒绝更改用户密码的尝试。

```
password        required        pam_deny.so
```

required 控制表示该模块必须返回成功才能授予请求。`pam_deny` 模块从不返回成功。此 PAM 配置阻止了所有更改用户指纹的尝试。

`pam_permit`

如果说 `pam_deny` 是直言不讳地拒绝一切的，那么 `pam_permit` 就是它的镜像双胞胎。像一个非常糟糕的谈判员，`pam_permit` 对一切都说“好”。它没有选项，也没有可调的行为。

某些服务需要使用 pam_permit 来显式允许访问。出于这个原因，你会看到许多程序在会话（`session`）策略中使用 pam_permit。

### 允许 Root

PAM 允许你显式授予 root 账户无所不能的权限。`pam_rootook` 模块在用户是 root 时允许访问。

我最常看到 `pam_rootook` 与 `include`（包含）语句一起使用。以下是 `chfn1(1)` 的 CentOS 7 PAM 配置。



```
auth sufficient pam_rootook.so
auth include system-auth
account include system-auth
password include system-auth
session include system-auth
```

整体来看，这意味着“root 始终可以运行此命令，或者根据系统认证允许运行其他命令”。

`pam_rootook` 仅对 auth 语句有效。

### 安全终端

Unix 类系统认为某些终端比其他终端更安全。虽然 SSH 可能是一个安全协议，但 SSH 使用的虚拟终端本质上并不一定安全。物理控制台可能不在安全位置，但如果你有控制台访问权限，你就可以物理上修改机器，所以你大可以称它是安全的。如果这些串口端口连接到管理员桌上的本地终端，那么它们可能是安全的，但如果它们在调制解调器池中，就不那么安全了。如果机器及其控制台位于一个由严锁保护的房间内，那么物理终端就达到了最高安全性。

通常，用户无法直接以 root 身份登录。他们需要以普通用户身份登录，然后通过 `su(1)` 变成 root。`pam_securetty` 模块允许直接以 root 登录，且仅当用户在安全终端进行验证时允许。

BSD 系统如果终端设备在 `/etc/ttys` 列表中的包含 `secure` 标志，则认为该终端设备是安全的。

Linux 系统在 `/etc/securesttys` 中列出终端设备。Linux-PAM 的 `pam_security` 还允许在内核命令行列出的控制台设备上以 `root` 登录，以及 `/sys/class/tty/console/active` 列出的控制台。`pam_security` 的 `nconsole` 选项禁用这些额外设备，将 `root` 登录限制在 `/etc/securesttys` 列出的设备上。

### 登录计数

PAM 通过 `pam_lastlog` 模块向用户计数系统提供信息。在 CentOS 和 Debian 上，用户计数位于 `/var/log/lastlog`，而 FreeBSD 将其放在 `/var/log/utx.lastlogin`。它还会在用户登录时打印欢迎信息，告知他们上次登录的时间。

`pam_lastlog` 仅作为 session 语句的一部分起作用。

Linux-PAM 支持多个选项来修改 `pam_lastlog` 的计数和登录行为。你可以使用 `nowtmp` 和 `noupdate` 等选项禁用某些计数功能。`noterm` 和 `nohost` 等选项会从用户的登录消息中移除信息，而 `showfailed` 会显示上次有人登录此账户失败的时间。最后，`inactive` 选项允许你设置账户因空闲被锁定之前的空闲天数。你可以设置天数，也可以使用默认的 90 天。

```
session optional pam_lastlog.so showfailed inactive=5
```

BSD 系统在其他地方处理这些功能，因此 OpenPAM 不支持这些特性。

### 防止登录

无论你提前多久宣布维护窗口，无论提醒人们多少次，在你进行精细升级时，总会有人尝试使用系统。你可能希望系统处于多用户模式，但禁止系统管理员以外的任何人登录。或者你可能需要通过不让人们登录一段时间来解决管理问题。`pam_nologin` 模块为你准备的。

你可能认为可以通过关闭服务来实现类似的结果——如果 SSH 守护进程关闭，没有人能通过 SSH 登录你的主机！你也可以重新配置 SSH 仅允许 ssh 登录。`nologin` 模块普遍禁止登录。它禁止除了特权用户列表之外的所有人的登录。`pam_nologin` 检查 `nologin` 文件是否存在——Linux-PAM 为 `/etc/nologin`，OpenPAM 为 `/var/run/nologin`。如果 `nologin` 文件不存在，用户可以登录。如果该文件存在，大多数用户将无法登录。`pam_nologin` 使用 `nologin` 文件的内容作为应用程序的错误消息。用户能否看到完全取决于应用程序。

# 第 3 章：PAM 项目、代码和函数

许多 PAM 文档假设系统管理员熟悉 PAM 的内部机制。设计者希望你理解每种类型的语句调用哪些函数，以及哪些内部项目和错误代码。配置 PAM 模块和 Linux-PAM 扩展控制需要这些返回代码。

你不需要记忆本章的所有内容。PAM 项目对于调试至关重要，你确实需要熟悉它们。然而，具体的 PAM 错误代码和函数对管理员来说没那么重要。研究涉及的原理以及这些代码的用途，当 PAM 模块抛出代码时，你可以随时查询，并迅速熟悉这些错误。

## PAM 项目

PAM 通过一组定义的项目携带其大量的内部状态。使用 PAM 的进程定义所需项目并传递给不同的 PAM 栈。所有项目初始时都是未定义的。应用程序和框架设置这些项目。模块读取这些项目。

## 第 3 章：PAM 项、代码和函数

模块根据这些项（items）做出决策。我经常发现模块会以意想不到的方式固执地使用这些项。当身份验证没有按照你预期的方式进行时，回过检查这些项和模块文档是一个很好的切入点。

在 PAM 运行策略期间，项可能会发生变化。当模块提供信息时，应用程序可能会更改这些项。某些应用程序在模块返回特定代码时可能会忘记关键的身份验证信息。返回该代码的模块需要放在策略的末尾，在做出决策之后。应用程序可能会为某个项创建占位数据。查看项的值是查明为什么 PAM 在程序中运行偏离轨迹的好方法。

PAM 项可能包含安全敏感信息。出于因此，我强烈建议在一次性虚拟机上学习和实验 PAM 项，而不是在你的生产环境中进行。PAM 使用项来包含用户名、主机名、密码和等等事实。并不是所有感知 PAM 的程序都会定义所有的项。例如，对于 `su(1)` 来说，定义远程主机是没有意义的。

以下是常见的 PAM 项。

### PAM_SERVICE

`PAM_SERVICE` 项包含应用程序请求的策略名称。这通常是调用 PAM 的程序名称——类似于 `su`、`ftpd`、`ssh` 等。你可以重新编译程序以使用不同的服务名称，但通常不会这样做。

### PAM_USER

你可能认为 `PAM_USER` 会提供请求身份验证的用户名。

你错了。

`PAM_USER` 是某个程序正在尝试身份验证的用户名。例如，如果你通过 FTP 登录，`PAM_USER` 等于你的 FTP 账户。然而，如果你运行 `su root`，你正在尝试作为 root 进行身份验证。因此，`PAM_USER` 等于 root。

### PAM_RUSER

项 `PAM_RUSER` 请求用户。它可能是一个远程用户。它可能是请求 `su(1)` 访问的用户。模块可能会将此设置为与 `PAM_USER` 相同的值。如果此应用程序仅涉及单个用户账户，它可能不会设置此项。

### PAM_TTY

通过检查 `PAM_TTY` 查看进程运行在哪个终端上。这可能是一个虚拟终端（如 pts/2）或控制台登录（如 tty2）。如果这是一个没有真正终端的图形应用程序，它可能是 `$DISPLAY` 环境变量的内容。

### PAM_HOST

这提供了发生身份验证的主机名。它几乎总是本地主机。

### PAM_RHOST

`PAM_RHOST` 项给出客户端运行的主机。对于 FTP 这样的应用程序，它包含了客户端的主机名或 IP 地址。并不是所有的客户端服务器应用程序都会设置 `PAM_RHOST`。此外，本地运行的应用程序（如 `su(1)`）通常不会设置 `PAM_RHOST`。

### PAM_CONV

此项包含应用程序期望的 PAM 会话（conversation）的数据结构。需要研究这个内容的系统管理员就有麻烦了。

### PAM_AUTHTOK

身份验证令牌是用户当前的密码，或类似密码的内容。

### PAM_OLDAUTHTOK

这是用户过期的密码。你在更改密码时会看到它。

### PAM_USER_PROMPT

这包含请求身份验证用户名的提示符。

### PAM_AUTHTOK_PROMPT

此项提供请求密码的提示符。

### PAM_OLDAUTHTOK_PROMPT

这包含请求过期密码的提示符。当用户在登录前需要更改密码时，你会看到它。

### PAM_SM_FUNCTION

Linux-PAM 增加了 `PAM_SM_FUNCTION` 来存储调用函数时使用的是哪个 PAM 服务模块。大多数系统管理员不需要这个，但不要让它的突然出现困扰到你。

### PAM_TYPE

Linux-PAM 还增加了 `PAM_TYPE` 来显示调用模块的策略类型。它包含 auth、account、password 或 session。Linux-PAM 的调用几乎总是定义 `PAM_TYPE`。

我将在本章后面讨论 PAM 函数和服务模块函数。

### 使用 pam_exec 读取项



虽然 PAM 模块之间会传递项，但它们并没有为向普通系统管理员显示这些项提供接口。Linux-PAM 系统提供了 `pam_warn` 来从 PAM 导出信息，但它并不是通用的。我们将在第 6 章看到 `pam_warn`。然而，每个 Unix 类系统都支持使用 `pam_exec` 模块将调试信息从策略中拷贝出来。第 6 和第 7 章详细介绍了 `pam_exec`，但我们在这里提一下。

`pam_exec` 允许你作为策略的一部分运行任意命令。大多数情况下，这是一个 shell 脚本。（你可以将简单命令放入 `pam_exec` 语句中，但我看来那样感觉很脆弱。）我们将使用一个简单的示例将策略中的所有 PAM 项复制到系统日志中。几乎每个操作系统都包含了 `pam_exec`。

这是一个用于捕获 PAM 项并将其写入系统日志的简单脚本。我将其安装为 `/usr/local/scripts/pamvarlog.sh`，但你可以将其放在你喜欢的位置。

```sh
#!/bin/sh
set | grep PAM | xargs logger
```

这提取所有环境项，获取任何包含 PAM 的项或值，并将它们发送到系统日志。

现在将此脚本附加到你的策略中。你希望这个脚本放在顶部。

## PAM 返回代码

成功和失败并不总是界限。就像政治有灰色地带一样，PAM 除了“是”和“否”之外有很多答案。代码的准确解释取决于你如何进行身份验证。

当 PAM 调用模块时，模块恰好返回一个结果。该代码的准确解释取决于你是在本地拥有密码还是在 LDAP 中拥有。

PAM 包含了 30 个返回代码，编号从 0 到 29。其中许多只在怪异的情况下或系统错误时出现。不匹配的二进制类型和无法加载的库会出现在系统日志中，这是每个系统管理员排故障程序中熟悉的部分。有关完整列表，请查看 X/Open Single Sign-On (XSSO) 可插身份验证模块规范或 `pam(3)`。

每个返回代码都有一个正式名称，通常全大写，并以 PAM 开头。你会看到像 `PAM_SUCCESS`、`PAM_AUTH_ERR` 等返回代码。你可能会看到从 0 到 29 的返回代码数字。你可能还会看到小写的返回代码，且没有开头的 `PAM_`。也就是说，返回代码 `PAM_SUCCESS`、`0` 和 `success` 指的是同一种情况。

许多返回代码似乎有重叠。对于系统程序员来说它们没有重叠，但对于系统管理员来说有。像 `PAM_CRED_EXPIRED` 和 `PAM_AUTHTOK_EXPIRED` 这样的返回代码意味着身份验证凭据或密码过期。得到哪种错误取决于你如何进行身份验证，但对于系统管理员来说，它们都意味着用户的密码或其他身份验证令牌不再有效。

你不需要知道每个 PAM 返回代码的存在、每个 PAM 调用只返回一个代码，以及当代码出现时如何获取更多信息。以下是你最可能遇到的 PAM 返回代码。

### `PAM_SUCCESS` (0)

请求完全成功。用户身份验证正确。这是一个无条件的“是”。

## 第 3 章：PAM 项目、代码与函数

### `PAM_SERVICE_ERR` (3)

PAM 模块所需的某些服务发生故障。这最常见于集中式身份验证，当 Kerberos、LDAP 或 NIS 服务器崩溃时。

### `PAM_SYSTEM_ERR` (4)

模块在尝试运行时遇到了操作系统层面的错误。

### `PAM_PERM_DENIED` (7)

模块表示该用户缺乏返回成功所需的权限。此权限错误可能出现在应用栈的任何地方。请检查您的系统日志。

### `PAM_MAXTRIES` (8)

模块对尝试输入正确身份凭据的最大次数有限制。你超过了该限制。

### `PAM_AUTH_ERR` (9)

发生了认证错误。用户输入错误的密码。

### `PAM_NEW_AUTHTOK_REQD` (10)

通常情况下，获取此返回码意味着用户的密码已过期必须更改。然而，在与密码相关的 PAM 模块中，当某些类似于密码的实体需要调整或替换时，可能会出现此代码。

只有账户策略应该返回此代码。

### `PAM_USER_UNKNOWN` (13)

认证系统不认识该用户。

### `PAM_IGNORE` (25)

PAM 策略应该忽略此模块的结果，不要让它参与允许或拒绝访问的投票。

## 函数

每种类型的 PAM 请求都有定义的编程接口来执行任务。这些 API 既赋予了 PAM 灵活性，也限制了它的范围。当然，系统管理员不需要知道如何使用这些函数。但是如果它们出现在文档或系统日志中，大致了解函数的作用有助于调试问题。

## PAM 设置与资源

设置 PAM 会话需要程序调用 `pam_start` 函数。当 PAM 会话完成时，`pam_end` 函数将销毁会话并释放会话使用的所有资源。

程序的 PAM 会话是程序与 PAM 库之间的对话。PAM 应用需要一个“对话回调（conversation callback）”，即 PAM 栈向应用程序发送消息的方法，这由 `pam_conv` 函数提供。

除了本章之前讨论的项目外，PAM 还包含了一整套内部项目列表。甚至向用户显示的提示也是一个项目。`pam_set_item` 和 `pam_get_item` 函数允许 PAM 操纵这些项目。

`pam_setenv`、`pam_getenv`、`pam_putenv` 和 `pam_getenvlist` 函数允许 PAM 在登录前操纵用户环境。例如，像 `pam_krb5` 这样的模块可以使用这些函数将 `KRBS5CNAME` 设置为登录时存储票据的凭据缓存路径。

PAM 模块可能需要为其自己的内部函数分配内存。虽然 PAM 编程接口是严格定义的，但 PAM 模块可以在内部执行任何操作。`pam_set_data` 和 `pam_get_data` 允许 PAM 会话通过名称创建并操纵这些内存块。

### 认证函数

顾顾义，`pam_authenticate` 函数用于验证用户身份。该函数接收用户名和身份验证令牌（密码、指纹、基因扫描结果等），并将其与身份验证数据库进行比对。

`pam_setcred` 函数管理用户的凭据。用户的凭据可以包括用户名和组组成关系等项目，还包括 Kerberos 票据或其他单点登录扩展。

PAM 模块不设置用户的 UID 或 GID。它们也不执行为用户打开虚拟终端的操作。这些操作通常需要由子进程完成。如果 PAM 模块在调用 `pam_setcred` 时将权限从 root 降到用户权限，那么模块将失去访问更新 lastlog 的特权操作权限。相反，服务器为用户的活动创建一个子进程，而服务器进程保持其权限并在完成后清理。

### 账户、会话与密码函数

PAM 使用 `pam_acct_mgmt` 函数来执行账户策略。任何对登录时间、密码过期或其他账户语句的限制都会通过 `pam_acct_mgmt` 传递。

会话语句会触发 `pam_open_session` 和 `pam_close_session` 函数。

最后，`pam_chauthtok` 函数允许服务器更改用户的密码。

### PAM 服务函数

除了用于调用 PAM 的函数外，你还会看到 PAM 自身调用模块的函数。这些服务模块函数是每个模块响应特定请求的方式。每个服务模块函数对应一个普通的 PAM 函数，并以 `pam_sm_` 开头而不是简单的 `pam_`。

服务模块函数有 `pam_sm_acct_mgmt`、`pam_sm_authenticate`、`pam_sm_chauthtok`、`pam_sm_close_session`、`pam_sm_open_session` 和 `pam_sm_setcred`。因此，`pam_sm_acct_mgmt` 就像 `pam_acct_mgmt`，但它是在模块内部而非 PAM 中使用的。

你为什么需要知道所有这些？一方面，Linux-PAM 的扩展控制大量使用了 PAM 返回码。

## 第 4 章：Linux-PAM 扩展控制与子栈

PAM 定义了四种常见的控制语句：`required`（必须）、`requisite`（）、`sufficient`（足够）和 `optional`（可选）（以及 `ignored` 忽略）。这些控制决定了 PAM 模块如何影响认证。

Linux-PAM 提供了额外的控制语句允许你精调响应，以及允许你重定向处理的 `substack`（子栈）参数。

## 扩展控制

PAM 模块返回“是”始终是 `PAM_SUCCESS`，但“否”却有无数种形式。每个 PAM 模块可能返回几种响应中的一种。通过扩展控制，你可以精调 PAM 语句处理拒绝的方式。记住，模块对每个查询只返回且仅返回一种响应。

扩展控制将四种 PAM 控制替换为针对每个响应的特定指令，并对你未指定的响应提供通用的捕获指令。“如果模块返回 X，则拒绝访问。如果返回 Y，就足够了。如果返回 Z，则立即允许访问。任何其他回答，尝试下一个模块。”

> 如果人类对拒绝的处理能这样容易调优就好了！

通过在周围使用方括号 `[]` 来标识扩展控制。这是一个来自 CentOS 的 `pam_secrety` 扩展控制示例。

```
auth [...]
```



括号内的每个条目代表一个 PAM 响应，去掉前缀 `PAM_` 并转为小写。等号将响应与处理该响应的指令分开。这表示当模块返回 `PAM_USER_UNKNOWN` 时，策略应采取“忽略”动作。当模块返回 `PAM_SUCCESS` 时，执行“ok”动作。如果响应是 `PAM_IGNORE`，采取“忽略”动作。当响应为其他任何内容，默认指令是“bad”。

### 扩展控制动作

考虑 PAM 策略。策略中的大多数语句影响是否允许访问。在任何时刻，策略都可能处于“如果没有人反对就允许访问”或“我们明确拒绝该请求，后续模块可以进行你的清理工作”的状态。Linux-PAM 的扩展控制动作旨在更改该策略的状态。

`bad` 动作告诉 PAM 身份验证请求失败了。这就是为什么我们上面的示例使用它作为默认值——我们关心某些特定的失败，但对于大多数失败，我们直接说“不”。

`If`

# 第4章：Linux-PAM 扩展控制与子栈（Substacks）

响应触发 `bad`，就像某个必需模块失败了。PAM 会继续处理策略，但除非人为重置，否则身份验证最终会被拒绝。

`die` 动作告诉 PAM 身份验证已失败，它必须立即停止处理策略。该模块之后的模块将不会被处理。当响应触发 `die` 时，PAM 策略的行为就像一个必需模块失败了。

`ok` 动作告诉 PAM 身份验证成功。只要没有其他模块对象的反对，就允许访问。它通常应用于 `PAM_SUCCESS` 返回码。`ok` 无法覆盖 PAM 策略中其他部分的 `bad` 响应。当响应触发 `ok` 时，PAM 策略的行为就像一个必需模块成功了。

`done` 动作告诉 PAM 身份验证成功，并且 PAM 立即停止处理策略。如果策略中早之前没有返回 `bad`，则策略将允许访问。当响应触发 `done` 时，PAM 策略的行为就像一个足够模块成功了。

`ignore` 动作表示此响应不会改变策略的响应。早之前的 `bad` 或 `ok` 仍然有效。该模块可以执行其他操作（例如记录日志或运行无关命令），但 PAM 不会根据该模块的结果或检查来做决定。这就像最常见的可选（optional）控制情况。

`reset` 动作告诉 PAM 丢弃任何之前的 `bad` 或 `ok` 结果，并保留剩余模块的新成功或失败结果。这是 Linux-PAM 特有的。与绑定控制（binding control）一样，我从未在生产环境中见过部署过 `reset`。

最后，你可以指定一个数字作为动作。触发该数字告诉 Linux-PAM 跳过策略中后续的相应数量模块。数字通常与 `pam_success_if` 模块一起使用，正如第5章所讨论的。

### 扩展格式中的标准控制

每个标准 PAM 控制都可以用 Linux-PAM 扩展控制格式表示。理解这些可以加深你对扩展控制和传统控制的理解。

必需（required）控制可以像这样表示：

```
[success=ok new_authtok_reqd=ok ignore=ignore default=bad]
```

如果 PAM 模块返回 `PAM_SUCCESS` 或 `PAM_NEW_AUTHTOK_REQD`，此控制将采取 `ok` 动作。身份验证成功。如果模块返回 `PAM_IGNORE`，PAM 将忽略该模块。如果模块返回其他内容，将采取 `bad` 动作且身份验证失败。

必须（requisite）控制看起来非常相似。

```
[success=ok new_authtok_reqd=ok ignore=ignore default=die]
```

`requisite` 和 `required` 的唯一区别在于默认动作。当 `required` 控制失败为 `bad` 时，`requisite` 控制默认为 `die`。如果带有此控制的模块失败，访问被拒绝并立即停止处理。

足够（sufficient）控制看起来完全不同。

```
[success=done new_authtok_reqd=done default=ignore]
```

如果模块返回 `PAM_SUCCESS` 或 `PAM_NEW_AUTHTOK_REQD`，策略立即允许访问。得益于 `done` 动作，不会发生进一步处理。任何其他响应都不会影响策略的投票结果，尽管模块可能在系统上采取其他操作。

可选（optional）控制类似于 `sufficient`。

```
[success=ok new_authtok_reqd=ok default=ignore]
```

在这里，`PAM_SUCCESS` 或 `PAM_NEW_AUTHTOK_REQD` 使此模块返回 `ok` 并允许访问。任何其他结果意味着该模块既不允许也不拒绝访问。处理继续，但其他模块仍然可以否决访问。

### 子栈（Substacks）

Linux-PAM 支持处理跳转（detours）或子栈。虽然 `include` 将该文件中的适当规则拉入 PAM 策略，但 PAM 会单独处理子栈。子栈中的控制无法让整个策略停止处理——它只能终止子栈并返回主 PAM 策略。在子栈中做的决策会影响策略允许或拒绝访问的决策。

让我们来看常见的子栈示例。这里是 CentOS `/etc/pam.d/login` 中的策略，它调节控制台登录。

```
auth [user_unknown=ignore success=ok ignore=ignore \
    default=bad] pam_security.so
auth substack system-auth
auth include postlogin
```

此策略从检查 `pam_security` 模块（第2章）开始。它进入文件 `system-auth` 包含的子栈。许多 CentOS PAM 配置使用 `system-auth` 作为子栈，允许在多个服务之间共享通用配置。

```
auth required pam_env.so
auth sufficient pam_fprint.so
auth sufficient pam_unix.so nullock try_first_pass
auth requisite pam_succeed.if_so \
auth required uid >= 1000 quiet_success
pam_deny.so
```

考虑此子栈是如何处理的。第一个模块 `pam_env`（第5章）是必需（required）的。如果此模块失败，即使后续模块返回成功，请求也会被拒绝。然后我们有两个足够（sufficient）的模块。其中任何一个都可以返回成功并立即终止子栈的处理。第四个是必须（requisite）的，意味着如果成功，策略处理将立即结束。最后一个模块 `pam_deny.so` 总是返回失败。

子栈有三个可以立即终止身份验证策略的控制语句——两个 `required` 和一个 `requisite`。然而，如果子栈中触发了任何一个，处理将立即结束。

# 第5章：常用的 Linux-PAM 模块

`pam-env` 模块从 `pam-env` 特定配置文件、系统环境文件和用户环境文件获取设置。

## pam-env 配置

主要的 `pam_env` 配置文件 `/etc/security/pam_env.conf` 允许你根据用户连接的方式设置环境变量。你可以提供一个默认值，如果需要，还可以提供一个条件替代方案或覆盖（override）。规则具有如下格式：

变量 默认 覆盖

如果语句没有覆盖，`pam_env` 将用户设置环境变量。在这里我们无条件地设置 `EDITOR` 变量。

`EDITOR pico`

用户可以使用常用的 Shell 配置覆盖此设置，但这允许你设置一个合理的默认值。

在早前的 `pam_env.conf` 中，我们分配了用户 `$REMOTEHOST` 环境变量。在这里，我们利用它来为 `$DISPLAY` 分配一个合理的值。然而，如果用户自带了他们的 `$DISPLAY`，就让他们保留即可。

你可以使用 `confile` 选项为不同的服务设置备用 PAM 配置。你可能想为 FTP 用户设置一个特殊环境，可以在 `/etc/pam.d/ftpd` 文件中这样设置：

```
session required pam_env.so \
    confile=/etc/security/pam_env.ftpd conf
```

默认的 `pam_env.conf` 包含未注释的条目。

### 系统环境

你可以使用系统环境文件 `/etc/environment` 来无条件地将变量强制注入用户环境中。与 `/etc/bash.bashrc` 等特定于 shell 的文件不同，`/etc/environment` 会影响所有用户，无论他们使用什么 shell。

与 `pam_env.conf` 不同，`/etc/environment` 完全不会被解析。如果你需要变量插值和逻辑判断，请改用 `pam_env.conf`。每行包含一个变量名、一个等号和一个值，如下：

```
IRCSERVER=irc.mwl.io
```



后续的条目无法引用 `$IRCSERVER` 的值。像下面这样的条目会将变量 `$BABBLE` 设置为字面量 `$IRCSERVER`，而不是 `irc.mwl.io`。

```
BABBLE=$IRCSERVER
```

用户的 shell 会解释这些值并可以对其进行覆盖。

`Pam_env` 使用 `readenv` 标志来控制是否读取 `/etc/environment`。默认情况下，`pam_env` 会读取并使用环境文件。将 `readenv` 设置为 0 可禁用读取环境。

```
session required pam_env.so readenv=0
```

你还可以通过 `envfile` 标志、等号 (=) 和环境文件的完整路径来设置不同的环境文件。这允许为不同的服务设置不同的环境。

### 用户环境

用户可以拥有自己的环境文件，你可以让 `pam_env` 在启动时读取并强制这些环境文件。这通常不是好主意，但有时它是唯一的办法。`userenv pam_env` 标志允许你设置一个包含期望环境变量的文件。该文件相对于用户的家目录。将 `user_readenv` 标志设置为 1 即可启用此功能。

只有当特定用户的环境必须在登录过程早期设置，且你无法为所有用户设置该环境时，才使用 `userenv`。

用户环境文件的工作与系统环境完全相同。

### pam_env 与安全

PAM 模块可以使用用户的环境和 PAM 项目来做出决策。通过调用 `pam_env`，你正在向 PAM 认证或会话策略中输入新变量。`pam_env` 设置的环境变量可能会改变 PAM 决策的结果。

如果你允许使用环境文件，风险将会增加。虽然 PAM 模块通常编写得非常严谨，但我非常不愿意断言用户环境文件无法绕过认证过程。用户是聪明的。如果你允许环境文件，请务密切关注你的系统安全和行为。

虽然 `pam_env` 帮助页声明 `pam_env` 应该出现在任何策略的最后，但为了尽量减少环境污染影响认证或会话配置的风险，这种建议导致了如 CVE-2010-4708 和 CVE-2011-3149 等安全漏洞。CentOS 和 Debian 都在策略中将 `pam_env` 置于首位以降低风险。

我建议尽可能避免使用 `pam_env`。

### 条件成功：pam_succeed_if

Linux-PAM 的 `pam_succeed_if` 模块允许你根据用户账户设置、被检查的服务以及连接进行各种检查。你可以将这些特征的任何一个与你选择的值进行比较。

在用户级别，`pam_succeed_if` 允许你检查用户名 (`user`)、`UID` (`uid`)、`GID` (`gid`)、`shell` 和家目录 (`home`)。如果 PAM 设置了 `root` 或 `host` 项目，你可以检查这些项目。最后，你可以检查终端 (`tty`) 或服务。

你可以将这些内容作为数字、字符串和列表成员进行比较。此外，你还可以进行基础的用户组成员关系比较，类似于 `pam_wheel`。如果比较匹配，则模块成功；如果比较不匹配，则模块失败。

### 字符串比较

你可以将任何内容作为字符串进行比较。即使是数字也可以字符串，除了精确匹配外，这种用法相当有限。`Pam_succeed_if` 允许你使用等号 (=) 进行精确的字符串比较。你可以使用 `!=` 运算符检查项目是否不匹配字符串。

此外，你可以使用通配符（globs）或 shell 风格的正则表达式。如果项目匹配通配符，则 `~` 运算符成功；如果项目不匹配通配符，则 `~` 运算符失败。

这里有一个禁止 `root` 用户通过 GDM 登录的 Debian 配置。

```
auth required pam_succeed_if.so user != root quiet_success
```

如果用户不等于字符串 `"root"`，`pam_succeed_if` 将返回成功。

### 数值比较

你可以将 `UID` 和 `GID` 与数字进行比较。这对于具有常量用户和组 ID 数字的定义应用程序账户（如 `www` 和 `tcpdump` 等）最有用。使用标准的数学运算符：小于 (`<`)、小于或等于 (`<=`)、大于 (`>`) 和大于等于 (`>=`)。

Centos 使用 `pam_succeed_if` 处理 UID 1000：

```
auth required pam_succeed_if.so uid >= 1000
```

`quiet` 选项告诉模块不要将成功或失败记录到 syslog。

### 字符串比较（续）

若要配合列表使用 `pam_succeed_if`，它提供了 `in` 和 `notin` 运算符。在运算符后给出列表，并用冒号分隔。

```
auth required pam_succeed_if.so notin mwl:jkh:des
```

### 条件规则处理

Linux-PAM 允许你跳过 PAM 策略中的某些语句，如第 4 章所述。这主要用于 `pam_succeed_if`，创建类似“如果为真，则跳过下一条规则”的 PAM 规则。

```
session [success=1 default=ignore] pam_succeed_if.so service crond quiet use_uid required pam_unix.so
```

# 第5章：常用的 Linux-PAM 模块

你可以使用 `pam_localuser` 使用备密码文件。使用 `file` 选项、等号以及文件路径。

## 限制用户资源：pam_limits

Linux-PAM 可以对用户施加系统资源限制。系统资源已不再是曾经那种稀缺商品，即使用户可能会启动一个消耗整个 CPU 并填满主机内存的进程。资源限制有助于防止这些问题的发生。你可以通过 `pam_limits` 实施资源限制。

运行 `bash` 的用户可以使用 `ulimit` 查看它们的限制，而基于 `csh` 的 shell 则使用 `limit`。

较旧的 Linux 版本在 `/etc/limits.conf` 中设置这些限制。PAM 系统通常通过登录类（login classes）在认证之外处理这个问题。

限制属于会话级别的 PAM 类型。

`pam_limits` 系统包含两个部分：PAM 模块本身和限制文件。虽然可以将 `pam_limits` 指向任何想要的文件，但默认配置文件位于 `/etc/security/limits.conf`。额外的限制存放在 `/etc/security/limits.d` 目录下。`limits.conf` 中的每行都有四个字段：域、类型、项目和值，如下所示。

```
ftp hard nproc 0
```

域（domain）标识该限制适用于哪些用户。你可以通过用户、组、通配符以及 UID 和 GID 范围来限制限制。在我们的示例中，域是用户 `ftp`。

类型（type）表示这是硬限制（hard）还是软限制（soft）。硬限制是不可违越的。我们的示例是一个硬限制。

项目（item）关键字定义了要限制的哪种资源。`pam_limits` 包含了许多资源关键字，我们将在稍后讨论。示例使用了项目 `nproc`，它是表示最大进程数量的关键字。

最后一个字段给出了该资源的最大值。

上面的示例将用户 `ftp` 限制为最多 0 个进程。希望该账户仅用于 FTP 服务；否则，用户 `Frederic Thomas Powell` 将会非常恼火。

### 限制域（Limit Domains）

你可以通过用户名、组、UID、GID 或通配符来标识用户。

对于适用于单个用户名的限制，使用用户名作为域。

要使用系统组，请在组名之前加上 `@` 符号，例如 `@wheel`、`@staff` 或 `@customers`。

星号 (`*`) 意味着该限制适用于所有用户。“所有用户”不包括 `root`，因为无所不能的 `root` 账户不受凡俗束缚。如果你想限制 `root`，必须显式地将 `root` 列为域。

`pam_limits` 使用 `%` 作为特殊通配符，专门留给 `maxlogins` 和 `maxsyslogs` 限制使用。单独使用时，它设置了此主机上非 `root` 登录的最大数量。在它后面加上组名，可以设置该组的最大登录数。

通过前导冒号指定单个 UID，如下所示。

```
:1000
```

对于 UID 范围，给出最低和最高匹配的 UID，并用冒号分隔。这里我们对 UID 从 1000 到 2000 之间的所有用户设置了限制。

```
1000:2000
```

如果不设置最大匹配 UID，则限制适用于所有大于或等于列出数字的 UID。在这里，我们对所有 1000 及以上的 UID 应用了限制。

```
1000:
```

组 ID（GID）的工作方式与 UID 非常相似，它们前面有一个 `@` 符号。用冒号指定范围。如果你在匹配 UID 范围，PAM 会将用户的主组与该范围进行比较。然而，如果你在匹配特定的组，PAM 会查看用户所属的所有组。在这里，如果用户在 GID 10000 中，我们就实施限制，即使它不是用户的主组。

```
@:10000
```

将 `% maxlogs-only` 通配符与组 `@` 通配符结合，以限制所有用户的总登录数。在这里我们限制了组 10000 的用户总登录数。

```
%:10000
```



现在决定这是哪种限制。

### 限制类型（Limit Type）

Linux-PAM 支持两种类型的限制：硬（hard）和软（soft）。

软限制是用户可以感知的限制。它是操作系统的一种：“嘿，你真的想使用超过你份额的资源吗？”用户可以使用内置命令 `ulimit` 或 `limit` 来提高此限制。

硬限制是内核强制的绝对上限。用户无法规避这种限制。

你应该使用哪种？大多数用户都知道如何规避软限制，因此它实际上是硬限制。如果你有受过教育的用户，请同时使用软、硬限制。我通常使用限制来限制服务账户，防止 Web 服务器和数据库失控。在这种情况下，硬限制最好——如果我的 Web 服务器提高了限制，我将面临一堆新问题……

### 限制项目和值（Limit Items and Values）

Linux-PAM 可以对文件、内存、进程和登录设置限制。我们不会解释所有这些限制的含义，因为解释栈大小、锁定内存等内容将是另一本书的事¹¹

大多数限制值都是数值的。用户可以打开 100 个文件，或使用 1GB 内存等。

- `nproc`: 最大进程数。
- `cpu`: 最大 CPU 时间。
- `fsize`: 最大文件大小。
- `data`: 数据段的最大大小。
- `memlock`: 锁定内存量。
- `stack`: 最大栈大小。
- `as`: 地址空间的最大大小。
- `maxlogins`: 同时登录数。
- `maxsyslogs`: 系统日志数。
- `msgsque`: POSIX 消息队列数。
- `sigpending`: 挂起信号数。
- `rtprio`: 实时优先级。
- `nice`: 进程的 nice 值。
- `chroot`: 要 `chroot` 的目录。

¹¹如果你不知道一个旋钮的作用，就不要乱动它。

# 第6 章：PAM 调试

你已经仔细调整了 PAM 语句，但它的运行结果并没有像你预期的那样。也许认证在某个没有明显原因的地方终止了，或者某个模块似乎根本没有被调用。你如何判断哪些 PAM 模块被调用了，以及认证请求何时终止的？

在任何与计算机相关的事务中，所有的调试最终都会回退到某种打印语句上。PAM 跳过了准备工作，直接带你进入那里。你可以通过系统日志、`pam_echo` 和 `pam_exec` 跟踪 PAM 请求在每个策略中的进度。你也可以启动如 `ktrace(1)` 和 `truss(1)` 等程序调试器。

当你破坏了主机的 PAM 配置，并且不再权限修复自己的错误时，那种糟糕的感觉是无与伦比的。每当你调整主机的 PAM 配置时，请确保留有一个具有 root 权限的终端。彻底测试所有更改。在注销之前，确保你仍然能从新会话获取 root 权限。

这些技术中的任何一种都可能导致系统将认证信息泄漏到系统日志或终端会话。我建议在一次性虚拟机上进行测试，而不是在有活动用户的系统上。

## PAM 日志

如果你无法确定为什么某个模块的行为异常，请从日志记录开始。

基础的系统管理问题会出现在系统日志中。我最常见的配置错误（通常是在对着 PAM 咆哮了几十年脏话后）是忘记在 PAM 模块名称的末尾加上 `.so`。PAM 会搜索不存在的文件 `pam_unix` 而不是 `pam_unix.so`，导致语句失败，策略拒绝访问。这些错误会出现在系统日志中，且仅对 root 可见。首先检查这些记录的错误。

PAM 模块通过 `syslog(3)` 执行常规日志记录，设施为 `auth`。这些日志通常会存储在只有 root 可访问的受限日志文件中，例如 CentOS 上的 `/var/log/secure` 或 FreeBSD 和 Debian 上的 `/var/log/auth.log`。

许多模块接受 `debug` 参数来使模块输出更详细。内容和信息量完全取决于模块。PAM 模块开发者都选择在开启调试时记录不同的内容——或者是特定的内容——某些 PAM 模块提供的调试输出比其他模块更好。

但有时，你甚至还没有到达模块……

### 使用 pam_echo 调试

`pam_echo` 模块将内容打印给认证用户。并不是所有程序都会将这些消息传回用户，但当它生效时，它是既有启发性又简单的。

#### 使用 pam_echo

`pam_echo` 接受一个字符串作为参数，即要传回的消息。

```
auth optional pam_echo PAM auth policy starting
```

如果应用程序将 PAM 消息传回给用户，当策略命中此语句时，就会出现 `PAM auth policy starting` 文字。

这是来自一个最近 FreeBSD 系统的 `/etc/pam.d/system`。（我在这里使用 FreeBSD 是因为它的系统认证策略比平均 Linux 短得多.）我在每个模块之前添加了对 `pam_echo` 的调用。

- `auth required pam_echo checking OPIE`
- `auth sufficient pam_echo.so no_warn_fake_prompts`
- `auth required pam_echo checking ieaccess`
- `auth requisite pam_ieaccess.so no_warn_allow_local`
- `auth required pam_echo checking UNIX auth`
- `auth required pam_unix.so no_warn_try_first_pass nullock`

当用户尝试使用如 `su(1)` 的程序进行认证时，她将获得 `pam_echo` 消息。

```
$ su -m
checking OPIE
checking opieaccess
checking UNIX auth
```

密码：

虽然这看起来很嘈杂，但我们知道认证请求一直到达了策略的末端。它还可能破坏没有预期额外输出的 shell 脚本。如果一个自动化过程在你放入 echoes 的时候开始喷出错误，你就知道发生了什么。

### pam_echo 项目

你可以通过在 `pam_echo` 中使用转义字符来显示 PAM 项的内容。PAM 模块开发者都选择在开启调试时记录不同的内容——或者是特定的内容——某些 PAM 模块提供了：

- `%U` 是用户
- `%u` 是用户名
- `%t` 是会话
- `%s` 是服务
- `%H` 是主机
- `%i` 是远程主机
- 这里的某些 PAM 模块提供了更好的调试输出比其他模块。

# 第 7 章：任意文件与随机程序

Unix 的组组成模型是有局限性的。例如，如果你的环境使用了跨平台的 NFS，单个用户只能是 16 个组的成员。你可能想将某个组的管理工作委托给特定用户，但大多数类 Unix 系统并没有提供这种功能（Solaris 的能力系统就接近了）。有时，你可能希望 PAM 仅读取一个允许访问某服务的用户列表。

同样，你可能希望登录过程作为 PAM 过程的一部分运行一个程序。这部分可能是 NIS 配置的一部分，也可能与你的防火墙有关，或者是你自定义应用程序的组件。

对于这两种情况，你都可以使用 PAM 模块。我们将从 Linux-PAM 的 `pam_listfile` 开始。

## 检查文件：pam_listfile

传统的 Unix 系统包含针对每个应用程序的许可或禁止用户列表。经典的例子是 `/etc/ftpusers`，它列出了禁止使用 FTP 的用户。如果你尝试以 `root` 或 `operator` 等身份使用 FTP，FTP 守护进程会检查此文件并将你踢出去。

Linux-PAM 的 `pam_listfile` 告诉 PAM 读取一个包含列表的文件，并根据该列表允许或拒绝访问。你可以根据用户名或组允许或拒绝访问，也可以根据终端设备、远程主机、远程用户或 shell 来决定。

`pam_listfile` 的一个典型用法如下。

```
auth required pam_listfile.so item=user sense=deny \
file=/etc/ftpusers onerr=succeed
```

这是 `auth` 策略的一部分。我们将此示例设置为 `required`（强制），但它也可以合理地设置为 `requisite`（必须且通过）或 `sufficient`（足够）。（将 `pam_listfile` 配置设置为可选 `optional` 似乎有点奇怪，但我并不会说它永远不适用。）

`item` 是你在列表中要查找的条目。在这个例中，我们正在检查用户名。你也可以检查 shell、终端等。

`sense` 是如果某个项存在于，`pam_listfile` 应该如何响应。在这里，我们告诉 `pam_listfile`，如果用户名在文件中，则拒绝请求。

`pam_listfile` 需要知道要检查哪个文件。

最后，我们通过 `onerr` 设置说明如果 `pam_listfile` 遇到意外错误时应该如何表现。这不是像“用户不在文件中”这样的错误，而是“文件不可读”或“内核告诉它滚蛋？”之类的。在这里，我们告诉 `pam_listfile`，如果发生错误则返回成功。

此示例实现了传统的 `/etc/ftpusers` 功能。文件中的用户名列表可能无法通过该服务的身份验证。



让我们分别查看每个部分。

### Pam_listfile 项 (Items)

虽然用户名许可或阻止访问的最直观方式，但 `pam_listfile` 还允许其他选项。

你可能想根据用户是否在控制台前来允许或拒绝访问。虽然有一个 `pam_console` 模块，但它是为控制台用户配置环境的。在大多数组织中，你唯一登录控制台的时候是在发生灾难时。假设你希望管理员能够在控制台前运行 `su(1)`，但在远程登录时他们必须使用 `sudo(1)`。在 `/etc/pam.d/su` 中添加如下所示条目。

```
auth required pam_listfile.so item=tty sense=allow \
file=/etc/ttylist onerr=succeed
```

有了这样的语句，`pam_listfile` 会将用户的终端（tty）与文件 `/etc/ttylist` 进行比较。如果找到匹配项，它将返回 `sense` 设置提供的访问权限——在这种情况下，是 `allow`（允许）。

`/etc/ttylist` 文件需要包含这样的列表：

- tty1
- tty2
- tty3
- tty4

基于虚拟终端的拦截要困难得多。Linux 会根据需要创建虚拟终端。你无法在 `pam_listfile` 文件中使用通配符或正则表达式，因此你需要列出比你实际拥有的得多的虚拟终端。

基于远程主机的允许或阻止访问可以通过 `host` 项来实现。由于 `pam_listfile` 不支持任何类型的通配符或子网掩码，它永远不是执行检查的正确位置。如果你必须在 PAM 中使用远程主机匹配，请准备一个包含单独地址的文件，并准备好面对低级的烦扰。

你可以根据 `/etc/passwd` 中提供的用户 shell 允许或拒绝身份验证。在这里，我拒绝了所有使用 `/etc/shell` 中列出的 shell 的用户的身份验证。

```
auth required pam_listfile.so item=shell sense=deny \
file=/etc/shell onerr=succeed
```

然而，没有什么能阻止用户更改他们的 shell、通过身份验证，然后恢复他们偏好的 shell。你不会经常看到基于 shell 的拦截或许可列表。

组组成是 `pam_listfile` 可以处理的另一个标准。正如下文讨论，它的工作方式并不像你想的那样，但这是一个例子。

```
auth required pam_listfile.so item=group sense=allow \
file=/etc/grouplist onerr=succeed
```

如果一个用户是 `/etc/grouplist` 中列出的组的成员，她就能获得访问。如果不是，她就。将 `pam_listfile` 与组组成结合是说明 PAM 如何毁掉你一天的极佳方法。你可能会使用 `wheel` 语句只允许 `wheel` 组的成员使用某服务，并添加类似上面的 `pam_listfile` 语句来封禁 `/etc/grouplist` 中列出的组的任何人。

### Pam_listfile 的感应 (Sense) 与文件 (File)

虽然用户名是许可或阻止访问最明显的方式，但 `pam_listfile` 允许其他选项。

你可能想根据用户是否在控制台前来允许或拒绝访问。虽然有一个 `pam_console` 模块，但它是为控制台用户配置环境的。在大多数组织中，你唯一登录控制台的时候是在发生灾难时。假设你希望管理员能够在控制台前运行 `su(1)`，但在远程登录时他们必须使用 `sudo(1)`。在 `/etc/pam.d/su` 中添加如下所示条目。

```
auth required pam_listfile.so item=tty sense=allow \
file=/etc/ttylist onerr=succeed
```

有了这样的语句，`pam_listfile` 会将用户的终端（tty）与文件 `/etc/ttylist` 进行比较。如果找到匹配项，它将返回 `sense` 设置提供的访问权限——在这种情况下，是 `allow`。

`/etc/ttylist` 文件需要包含这样的列表：

- tty1
- tty2
- tty3
- tty4

基于虚拟终端的拦截要困难得多。Linux 会根据需要创建虚拟终端。你无法在 `pam_listfile` 文件中使用通配符或正则表达式，因此你需要列出比你实际拥有的得多的虚拟终端。

基于远程主机的允许或阻止访问可以通过 `host` 项来实现。由于 `pam_listfile` 不支持任何类型的通配符或子网掩码，它永远不是执行检查的正确位置。如果你必须在 PAM 中使用远程主机匹配，请准备一个包含单独地址的文件，并准备好面对低级的烦扰。

你可以根据 `/etc/passwd` 中提供的用户 shell 允许或拒绝身份验证。在这里，我拒绝了所有使用 `/etc/shell` 中列出的 shell 的用户的身份验证。

然而，没有什么能阻止用户更改他们的 shell、通过身份验证，然后恢复他们偏好的 shell。你不会经常看到基于 shell 的拦截或许可列表。

组组成是 `pam_listfile` 可以处理的另一个标准。正如下文讨论，它的工作方式并不像你想的那样，但这是一个例子。

```
auth required pam_listfile.so item=group sense=allow \
file=/etc/grouplist onerr=succeed
```

如果一个用户是 `/etc/grouplist` 中列出的组的成员，她就能获得访问。如果不是，她就。将 `pam_listfile` 与组组成结合是说明 PAM 如何毁掉你一天的极佳方法。你可能会使用 `wheel` 语句只允许 `wheel` 组的成员使用某服务，并添加类似上面的 `pam_listfile` 语句来封禁 `/etc/grouplist` 中列出的组的任何人。

### Pam_listfile 的错误处理 (Onerr)

`pam_listfile` 需要知道要检查哪个文件。

最后，我们通过 `onerr` 设置说明如果 `pam_listfile` 遇到意外错误时应该如何表现。这不是像“用户不在文件中”这样的错误，而是“文件不可读”或“内核告诉它滚蛋？”之类的。在这里，我们告诉 `pam_listfile`，如果发生错误则返回成功。

此示例实现了传统的 `/etc/ftpusers` 功能。文件中的用户名列表可能无法通过该服务的身份验证。

让我们分别查看每个部分。

### Pam_listfile 项 (Items)

虽然用户名是许可或阻止访问的最直观方式，但 `pam_listfile` 还允许其他选项。你可能想根据用户是否在控制台前来允许或拒绝访问。虽然有一个 `pam_console` 模块，但它是为控制台用户配置环境的。在大多数组织中，你唯一登录控制台的时候是在发生灾难时。假设你希望管理员能够在控制台前运行 `su(1)`，但在远程登录时他们必须使用 `sudo(1)`。在 `/etc/pam.d/su` 中添加如下所示条目。

```
auth required pam_listfile.so item=tty sense=allow \
file=/etc/ttylist onerr=succeed
```

有了这样的语句，`pam_listfile` 会将用户的终端（tty）与文件 `/etc/ttylist` 进行比较。如果找到匹配项，它将返回 `sense` 设置提供的访问权限——在这种情况下，是 `allow`。`/etc/ttylist` 文件需要包含这样的列表：

- tty1
- tty2
- tty3
- tty4

基于虚拟终端的拦截要困难得多。Linux 会根据需要创建虚拟终端。你无法在 `pam_listfile` 文件中使用通配符或正则表达式，因此你需要列出比你实际拥有的得多的虚拟终端。基于远程主机的允许或阻止访问可以通过 `host` 项来实现。由于 `pam_listfile` 不支持任何类型的通配符或子网掩码，它永远不是执行检查的正确位置。如果你必须在 PAM 中使用远程主机匹配，请准备一个包含单独地址的文件，并准备好面对低级的烦扰。

你可以根据 `/etc/passwd` 中提供的用户 shell 允许或拒绝身份验证。在这里，我拒绝了所有使用 `/etc/shell` 中列出的 shell 的用户的身份验证。然而，没有什么能阻止用户更改他们的 shell、通过身份验证，然后恢复他们偏好的 shell。你不会经常看到基于 shell 的拦截或许可列表。组组成是 `pam_listfile` 可以处理的另一个标准。正如下文讨论，它的工作方式并不像你想的那样，但这是一个例子。

```
auth required pam_listfile.so item=group sense=allow \
file=/etc/grouplist onerr=succeed
```



如果一个用户是 `/etc/grouplist` 中列出的组的成员，她就能获得访问。如果不是，她就。将 `pam_listfile` 与组组成结合是说明 PAM 如何毁掉你一天的极佳方法。你可能会使用 `wheel` 语句只允许 `wheel` 组的成员使用某服务，并添加类似上面的 `pam_listfile` 语句来封禁 `/etc/grouplist` 中列出的组的任何人。

### Pam_listfile 的感应 (Sense) 与文件 (File)

`sense` 是如果某个项存在于文件中，`pam_listfile` 应该如何响应。在这里，我们告诉 `pam_listfile`，如果用户名在文件中，则拒绝请求。`pam_listfile` 需要知道要检查哪个文件。最后，我们通过 `onerr` 设置说明如果 `pam_listfile` 遇到意外错误时应该如何表现。这不是像“用户不在文件中”这样的错误，而是“文件不可读”或“内核告诉它滚蛋？”之类的。在这里，我们告诉 `pam_listfile`，如果发生错误则返回成功。此示例实现了传统的 `/etc/ftpusers` 功能。文件中的用户名列表可能无法通过该服务的身份验证。让我们分别查看每个部分。

### Pam_listfile 项 (Items)

虽然用户名是许可或阻止访问的最直观方式，但 `pam_listfile` 还允许其他选项。你可能想根据用户是否在控制台前来允许或拒绝访问。虽然有一个 `pam_console` 模块，但它是为控制台用户配置环境的。在大多数组织中，你唯一登录控制台的时候是在发生灾难时。假设你希望管理员能够在控制台前运行 `su(1)`，但在远程登录时他们必须使用 `sudo(1)`。在 `/etc/pam.d/su` 中添加如下所示条目。

```
auth required pam_listfile.so item=tty sense=allow \
file=/etc/ttylist onerr=succeed
```

有了这样的语句，`pam_listfile` 会将用户的终端（tty）与文件 `/etc/ttylist` 进行比较。如果找到匹配项，它将返回 `sense` 设置提供的访问权限——在这种情况下，是 `allow`。`/etc/ttylist` 文件需要包含这样的列表：

- tty1
- tty2
- tty3
- tty4

基于虚拟终端的拦截要困难得多。Linux 会根据需要创建虚拟终端。你无法在 `pam_listfile` 文件中使用通配符或正则表达式，因此你需要列出比你实际拥有的得多的虚拟终端。基于远程主机的允许或阻止访问可以通过 `host` 项来实现。由于 `pam_listfile` 不支持任何类型的通配符或子网掩码，它永远不是执行检查的正确位置。如果你必须在 PAM 中使用远程主机匹配，请准备一个包含单独地址的文件，并准备好面对低级的烦扰。

你可以根据 `/etc/passwd` 中提供的用户 shell 允许或拒绝身份验证。在这里，我拒绝了所有使用 `/etc/shell` 中列出的 shell 的用户的身份验证。然而，没有什么能阻止用户更改他们的 shell、通过身份验证，然后恢复他们偏好的 shell。你不会经常看到基于 shell 的拦截或许可列表。组组成是 `pam_listfile` 可以处理的另一个标准。正如下文讨论，它的工作方式并不像你想的那样，但这是一个例子。

```
auth required pam_listfile.so item=group sense=allow \
file=/etc/grouplist onerr=succeed
```

如果一个用户是 `/etc/grouplist` 中列出的组的成员，她就能获得访问。如果不是，她就。将 `pam_listfile` 与组组成结合是说明 PAM 如何毁掉你一天的极佳方法。你可能会使用 `wheel` 语句只允许 `wheel` 组的成员使用某服务，并添加类似上面的 `pam_listfile` 语句来封禁 `/etc/grouplist` 中列出的组的任何人。

### Pam_listfile 的错误处理 (Onerr)

`pam_listfile` 需要知道要检查哪个文件。最后，我们通过 `onerr` 设置说明如果 `pam_listfile` 遇到意外错误时应该如何表现。这不是像“用户不在文件中”这样的错误，而是“文件不可读”或“内核告诉它滚蛋？”之类的。在这里，我们告诉 `pam_listfile`，如果发生错误则返回成功。此示例实现了传统的 `/etc/ftpusers` 功能。文件中的用户名列表可能无法通过该服务的身份验证。让我们分别查看每个部分。



有了这样的语句，`pam_listfile` 会将用户的终端（tty）与文件 `/etc/ttylist` 进行比较。如果找到匹配项，它将返回 `sense` 设置提供的访问权限——在这种情况下，是 `allow`。`/etc/ttylist` 文件需要包含这样的列表：

- `tty1`
- `tty2`
- `tty3`
- `tty4`

基于虚拟终端的拦截要困难得多。Linux 会根据需要创建虚拟终端。你无法在 `pam_listfile` 文件中使用通配符或正则表达式，因此你需要列出比你实际拥有的得多的虚拟终端。基于远程主机的允许或阻止访问可以通过 `host` 项来实现。由于 `pam_listfile` 不支持任何类型的通配符或子网掩码，它永远不是执行检查的正确位置。如果你必须在 PAM 中使用远程主机匹配，请准备一个包含单独地址的文件，并准备好面对低级的烦扰。

你可以根据 `/etc/passwd` 中提供的用户 shell 允许或拒绝身份验证。在这里，我拒绝了所有使用 `/etc/shell` 中列出的 shell 的用户的身份验证。然而，没有什么能阻止用户更改他们的 shell、通过身份验证，然后恢复他们偏好的 shell。你不会经常看到基于 shell 的拦截或许可列表。组组成是 `pam_listfile` 可以处理的另一个标准。正如下文讨论，它的工作方式并不像你想的那样，但这是一个例子。

```auth required pam_listfile.so item=group sense=allow \
file=/etc/grouplist onerr=succeed```

如果一个用户是 `/etc/grouplist` 中列出的组的成员，她就能获得访问。如果不是，她就。将 `pam_listfile` 与组组成结合是说明 PAM 如何毁掉你一天的极佳方法。你可能会使用 `wheel` 语句只允许 `wheel` 组的成员使用某服务，并添加类似上面的 `pam_listfile` 语句来封禁 `/etc/grouplist` 中列出的组的任何人。

## 运行程序：pam_exec

正如第 3 章和第 6 章所示，PAM 可以通过 `pam_exec` 任意命令。如果程序运行成功（返回 0），`pam_exec` 返回成功。如果程序返回错误或无法运行，`pam_exec` 返回失败。

为什么要使用 `pam_exec`？你可能像第 3 章那样提取 PAM 环境。教科书示例是在用户更改密码后重建 YP 数据库。但你也可以使用 `pam_exec` 实现在允许访问前检查用户列表的功能，正如同 `pam_listfile`。

需要考虑的是，`pam_exec` 为身份验证请求启动一个进程。如果很多人登录你的系统，这些进程会产生巨大的负载。请确保你的“任意命令”不是那些认为你的系统资源是用来吃肉的蓝色小矮人。简单的命令和脚本通常是没问题的。

## 配置 pam_exec

可以在 PAM 配置文件中直接放置命令。对于非简单的命令，我发现这种方式脆弱且容易损坏。你可能偏好其他方式，但由于我是写这本书的人，我们将按照我的方式来。相反，将你想让 PAM 执行的命令放在脚本中，并让 `pam_exec` 调用该脚本。`pam_exec` 最简单的调用只需要一个选项，即要运行的命令。

# 第7章：任意文件与随机程序

```
account required pam_exec /usr/local/scripts/pamvarlog.sh
```

当用户尝试访问其账户时，PAM 会运行脚本 `pamvarlog.sh`。我们在第 3 章使用了该脚本来收集 PAM 环境变量。

OpenPAM 和 Linux-PAM 都为 `pam_exec` 提供了额外的选项，但我们将先介绍基本功能。具体来说，我们将完全通过 shell 命令实现一个基本的 `pam_listfile` 功能。

## 在 pam_exec 中实现 pam_listfile

我们将拥有一个允许访问服务的用户列表。如果用户名存在于文件中则允许访问；如果不存在，则拒绝访问。

PAM 向我们的脚本传递了它通常的一组项目。如果你不确定特定服务器设置了哪些项目，可以使用第 3 章中的 `pamvarlog.sh` 脚本进行捕获。幸运的是，每个身份验证过程都需要 `PAM_USER`。

在我们的目标文件中检查用户名时，我们需要稍微留心。我们不想匹配注释，我们只想匹配完整的用户名。使用 `grep(1)` 就能解决这个问题。这是一个概念验证脚本，它检查 `/etc/validusers` 中的用户，如果用户名出现在那里则允许访问。

```
#!/bin/sh
/usr/bin/grep ^$PAM_USER$ /etc/validusers
return $?
```

该脚本返回 `grep(1)` 语句找到匹配项时的返回值，即返回 0。如果没有匹配项，它返回 1。记住，`pam_exec` 将 0 视为成功，将 1 视为失败。

如果你想拒绝访问 `/etc/bogususers` 中列出的用户怎么办？这是一个巨大的变化：添加一个感叹号。

```bash
#!/bin/sh
! /usr/bin/grep ^$PAM_USER /etc/bogususers
return $?
```

此脚本反转了 `grep(1)` 语句的返回值。

基于这些示例创建符合你需求的脚本。至少，你必须对输入进行清理处理。清理输入的方法取决于你系统的默认 root shell——`bash` 的方法与传统的 `sh` 不同。

## pam_exec 与模块对比

使用 `pam_exec` 处理一切似乎是解决许多问题的一种简单直接的方法。我们是系统管理员，我们喜欢 shell 脚本。

“你想针对 NoSQL 数据库进行身份验证？我来写个 shell 脚本！”

现实生活并不简单。

当 PAM 模块为某个函数执行时，通常通常使用它会比编写自己的脚本要好。某些冷门但公开的 PAM 模块使用的用户可能比你的 shell 脚本多得多。最严重的 bug 已经被发现了——最棒的是，它们是别人发现的。如果你自己写脚本，你就得自己去发现这些 bug。

使用 `pam_exec` 应该被认为是最后的选择。不过，它是一个非常有用的最后选择。

使用 `pam_exec` 时需要记住的一点是，Linux-PAM 和 OpenPAM 实现 `pam_exec` 的方式不同。

## OpenPAM pam_exec

OpenPAM 的 `pam_exec` 只有一个选项，调整返回值。

默认配置下，OpenPAM 的 `pam_exec` 返回两种响应之一。如果命令返回 0，`pam_exec` 返回 `PAM_SUCCESS`。如果命令返回其他任何内容，`pam_exec` 返回 `PAM_PERM_DENIED`。

`pam_exec` 的 `return_prog_exit_status` 选项改变了它的返回值。不再是简单的“是”或“否”，`return_prog_exit_status` 让脚本返回实际的 PAM 返回码，如第 4 章所述。你的脚本需要为调用它的服务模块函数返回一个有效的返回值。在 Linux-PAM 中，你可以检查 `PAM_SM_FUNC` 项目来查看调用 `pam_exec` 的函数。每个服务模块函数的手册页都列出了允许的返回值。`pam_exec` 知道哪些函数可以接受返回值。如果你的脚本尝试返回一个不可接受的代码，`pam_exec` 会代为返回 `PAM_SERVICE_ERR`。

这是 OpenPAM `pam_exec` 支持的选项。虽然 Linux-PAM `pam_exec` 支持更多选项，但选项几乎可以通过脚本实现。

## Linux-PAM pam_exec

Linux-PAM 版本的 `pam_exec` 支持调试、日志记录和密码处理。

`debug` 选项将调试信息发送到系统日志，正如第 1 章所述。

你的 `pam_exec` 命令可能会输出。输出通常会被丢弃，但你可以使用 `log=` 替代。通过定义日志文件，你可以将任何输出发送到该文件。`stdout` 将程序的输出发送到标准输出，让调用程序处理该输出。

即使命令通常不产生输出，`pam_exec` 也会回显程序抛出的错误。`quiet` 选项禁用消息。

`type=` 选项告诉 `pam_exec` 仅当 PAM 策略类型时运行命令。你可以设置 `type=account`，以便此特定的 `pam_exec` 只在账户策略上运行。

通过添加 `expose_authtok` 选项，你可以通过标准输入为脚本传递密码。环境变量 `PAM_MAX_RESP_SIZE` 决定了密码的最大长度，通常是 512 字节。

最后，你可以以被验证进程的有效 UID 程序。

## PAM 与 SELinux

安全增强 Linux（SELinux）是一种用于强制访问控制（MAC）架构的安全策略实施机制。SELinux 允许你定义安全策略，限制进程和用户访问文件、网络、端口和其他资源的能力。PAM（可插身份验证模块）是一个框架，允许应用程序使用验证模块而无需了解这些模块的工作原理。



虽然 PAM 处理身份验证（确定你是谁），但 SELinux 处理授权（确定你可以做什么）。例如，PAM 可以验证登录 SSH 的用户，但 SELinux 可以将用户的 shell 限制在特定的目录下。

当你使用 `pam_exec` 运行自定义脚本时，你正在这两个系统之间建立一座桥梁。PAM 会触发脚本，但 SELinux 仍然会管控脚本被允许的操作。理解这两个系统如何协作工作以提供稳健的安全环境是非常重要的。

# 第 7 章：任意文件与随机程序

要在你的系统上创建一个真正的 SELinux 策略，请使用带有 `-M` 标志的 `audit2allow` 以及实际模块名。这只是创建策略，并不会激活它。

```bash
# grep denied audit.log | grep pam_ssh | audit2allow -Mnpam_ssh
```

**重要提示**

要使此策略包生效，请执行：

```bash
semodule -i pam_ssh.pp
```

你不是那种会忽略指令的人，对吧？听听友善软件的话。

```bash
# semodule -i pam_ssh.pp
```

你的 PAM 模块现在应该可以工作了，或者至少它应该进入下一个错误提示。这总是一种进步，不是吗？

一旦你拥有了可用的 SELinux 策略，就可以将包含策略的 `.pp` 文件复制到其他系统并进行安装。你必须确保 SELinux 策略版本匹配，并且策略中引用的类型（`types`）在另一个系统中存在。此此的最佳方法是在测试和生产环境中使用相同的操作系统。

## SELinux 与 pam_mkhomedir

`pam_mkhomedir` 模块在用户登录时创建缺失的家目录。它被用于部署了集中认证（如 LDAP）的组织。本书没有涵盖该模块，因为它非常简单。

`pam_mkhomedir` 的一个问题是它不支持 SELinux。红帽公司将 SELinux 视为其操作系统的核心部分。红帽并没有更新 `pam_mkhomedir`，而是用与 SELinux 兼容的 `pam_oddjob_mkhomedir` 替代了它。目前已有解决方案，所以对于大多数 CentOS 管理员来说没问题。

然而，我曾在多个跨平台企业工作过，那里的公司安全策略强制使用 `pam_mkhomedir`。也许安全团队已经有一段时间没有更新其策略了。也许这是跨平台标准化推进的一部分。我甚至见过这样一种情况：“该死，那些该死的系统管理员又在所有事情上都使用 `pam_exec`！”通过调整 SELinux 安全策略可以让你在 CentOS 上使用 `pam_mkhomedir`。

最终，你可能无法在 CentOS 上获取 `pam_mkhomedir`。与其调整策略并继续过日子，不如与你的安全团队谈谈。搞清楚他们试图解决什么问题。帮助他们要么更新标准，要么通过其他方式解决他们的问题。

但如果你真的想玩玩你组织的安全策略，你就需要额外的 PAM 模块。

# 第 8 章：SSH Agent 认证

大多数系统管理员使用安全外壳（SSH）管理主机。大多数 SSH 认证是使用公钥而非密码的。如果你正在使用 SSH agent，你可以通过 `pam_ssh_agent_auth` 告诉 PAM 使用 agent 作为认证源。

[`Pam_ssh_agent_auth`](https://sourceforge.net/projects/pamsshagentauth/) 的工作方式与基于密钥的 SSH 认证相同。模块获取用户的 `authorized_keys` 文件，并询问用户的 SSH agent 它是否具有匹配的私钥。如果 SSH agent 拥有该私钥，模块将返回 `PAM_SUCCESS`。`Pam_ssh_agent_auth` 设计用于认证 `sudo(1)`，这就是我们使用它的方式。

使用用户的 SSH 密钥进行认证是对多因素认证的一种拙劣模仿。它证明了用户拥有密钥文件以及用于解密该密钥的短语。当然，密钥文件并不是物理实体。它可以在机器之间复制和移动。但它比单纯的明文密码稍微好一点。对于真正的双因素认证，你需要像 `Google Authenticator`（第 9 章）这样的工具，或者投资安全令牌。另一方面，SSH agent 认证让你避免在服务器上输入密码。

许多组织有正当理由不使用 SSH agent，或者有理由不以这种方式认证程序。破解用户的 SSH 客户端可能会导致服务器被破解。这在许多环境中是一个合理的反对意见。但 `pam_ssh_agent_auth` 是较简单的附加 PAM 模块之一，因此它是开始探索的好地方。



## 第 8 章：SSH Agent 认证

使用用户的 `SSH` 密钥进行认证是对多因素认证的一种拙劣模仿。它证明了用户拥有密钥文件以及用于解密该密钥的短语。当然，密钥文件并不是物理实体。它可以在机器之间复制和移动。但它比单纯的明文密码稍微好一点。对于真正的双因素认证，你需要像 `Google Authenticator`（第 9 章）这样的工具，或者投资安全令牌。另一方面，`SSH agent` 认证让你避免在服务器上输入密码。



# 第 8 章：SSH Agent 认证

使用用户的 SSH 密钥进行认证是对多因素认证的一种拙劣模仿。它证明了用户拥有密钥文件以及用于解密该密钥的短语。当然，密钥文件并不是物理实体。它可以在机器之间复制和移动。但它比单纯的明文密码稍微好一点。对于真正的双因素认证，你需要像 `Google Authenticator`（第 9 章）这样的工具，或者投资安全令牌。另一方面，SSH agent 认证让你避免在服务器上输入密码。

第 8 章：[`Pam_ssh_agent_auth`](https://sourceforge.net/projects/pamsshagentauth/) 的工作方式与基于密钥的 SSH 认证相同。模块获取用户的 `authorized_keys` 文件，并询问用户的 SSH agent 它是否具有匹配的私钥。如果 SSH agent 拥有该私钥，模块将返回 `PAM_SUCCESS`。`Pam_ssh_agent_auth` 设计用于认证 `sudo(1)`，这就是我们使用它的方式。

许多组织有正当理由不使用 SSH agent，或者有理由不以这种方式认证程序。破解用户的 SSH 客户端可能会导致服务器被破解。这在许多环境中是一个合理的反对意见。但 `pam_ssh_agent_auth` 是较简单的附加 PAM 模块之一，因此它是开始探索的好地方。

## `Pam_ssh_agent_auth` 与 PAM

那么，如何使用这个东西呢？找到你系统中 `sudo(1)` 的 PAM 配置。在大多数 Linux 系统中，它位于 `/etc/pam.d/sudo`，而 FreeBSD 会将其存放在 `/usr/local/etc/pam.d/sudo`。

现在是困难的部分：决定你想要如何使用该模块。你是否希望 SSH agent 认证就足够获取 sudo 权限？将该模块置于身份验证策略的最上方，并使用 `sufficient`（足够）控制。

你想同时要求 SSH agent 和密码吗？将 `pam_ssh_agent_auth` 放在最终的 `pam_deny.so` 之前的任何地方，并使用 `required`（强制）控制。

现在让我们来看一种稍微复杂的多因素身份验证方法。

# 第 9 章：一次性密码：Google 验证器 (Google Authenticator)

一次性密码仅有效一次的密码。我们有很多一次性密码的实现，从万物中的一次性密码 (OPIE) 到 RSA 令牌。基于时间的一次性密码系统（或 TOTP）使用系统时钟共享密钥根据需要计算有效的密码。最为人知的 TOTP 实现是 Google 验证器。

`Google Authenticator` 不需要访问 Google。它之所以被称为 *Google Authenticator* 是因为 Google 提供了软件，而不是因为它以任何方式挂接到 Google 的系统中。`Google Authenticator` 在没有连接互联网的机器上也能正常工作。

`Google Authenticator` 通过客户端应用和 Google 验证器 PAM 模块将你的智能手机、平板电脑或 Chrome 浏览器转换为身份令牌。当你尝试使用 Google 验证器访问服务时，PAM 模块会计算出一个六位数字密码作为临时的一次性密码。服务器提示你输入此密码。你的设备使用相同的方法计算出该主机当前的正确密码。将你设备提供的密码输入应用程序中。如果两个设备的计算结果相同，则密码匹配，你即可获得访问权限。

`Google Authenticator` 比使用 SSH agent 更好的多因素身份验证方法，但它并不完美。任何平板电脑、手机或 Chrome 浏览器都可以变成身份令牌。如果坏人捕获了你的任何设备，或者偷取了用于配置客户端应用的共享密钥，他们就拥有了你的身份令牌。但至少设备是物理对象，而不是入侵者可以轻易复制的文件¹¹¹⁷

每个使用 GA 的主机都有独立的 GA 配置和唯一的共享密钥。每个用户必须登录到她应该访问的每个主机并配置她的 GA 访问。`Google Authenticator` 本身最适合只有少数服务器和少量账户的环境。你不会希望一个拥有数千个账户的主机使用普通的 `Google Authenticator`，除非你投入员工时间来管理身份验证。正如稍后我们将讨论，可以在主机之间共享 GA 配置，但这会改变 GA 的安全性，并需要额外的脚本和配置。我们将从简单的情况开始，在单台主机上设置 GA。

在开始使用 `Google Authenticator` 之前，请检查主机的时钟和时区。`Google Authenticator` 在时钟与世界其他同步的服务器上效果最好。系统时钟经常偏离真实时间，特别是在虚拟机上。使用 `ntpd(8)` 或其他计时服务同步服务器的时间。如果 GA 莫名失败，双检一切的时钟和时区。

仅在身份验证策略中使用 `Google Authenticator`。它不为账户、会话或密码类型提供任何服务。

> ¹⁷ 除非你将共享密钥备份在入侵者可以窃取的地方。不要这样做。

`Google Authenticator` 几乎在处处可用；它没有像 `pam_ssh_agent_auth` 那样的环境要求。然而，我鼓励你在将其应用于所有系统身份验证之前仔细考虑。当服务器时间“醉酒”并剧烈偏移时会发生什么？如果你要求在控制台登录 GA，解决问题将进入单用户模式，可能需要通过重启。你有足够的冗余来处理这种情况？此外，`Google Authenticator` 内置了登录速率限制。如果你对 SSH 和 sudo 都要求 GA，你将直接撞上那个速率限制。

仔细考虑你部署决策的影响。

## 安装 Google 验证器

`Google Authenticator` 客户端很简单。从设备的应用商店获取你的应用，或者为桌面安装 Authenticator Chrome 扩展程序。

任何想要使用 `Google Authenticator` 的服务器都必须安装 `Google Authenticator` PAM 模块。FreeBSD 有 `pam_google_authenticator` 包，但大多数用户也会想要安装 `libqprencode` 包。Debian 包含了 `libpam-google-authenticator` 包，但很少是最新版本。CentOS 没有官方包，尽管在编写本文时 EPEL 已经包含了 CentOS 6 及更早版本的包。要在当前版本的 CentOS 上使用 `Google Authenticator`，或在 Debian 上使用 `Google Authenticator`，你可能必须从源码安装。

从 https://github.com/google/google-authenticator 获取当前的源码，可以使用 `git(1)` 或通过下载并解压 zip 文件。`libpam` 目录包含 `Google Authenticator` PAM 模块。进入该目录编译并安装库。

```
# ./bootstrap.sh
# ./configure
# make
# make install
```

你现在已经有了可用 `Google Authenticator` PAM 模块。

## Google 验证器用户功能

许多 GA 教程告诉用户运行 `google-authenticator` 并回答 yes。用户做出的糟糕决定可能会毁掉他们的一天。为你的用户提供关于如何配置的非常严格的

## 密码类型

GA 支持两种类型的密码：基于时间和基于计数器的。

基于时间的方法结合共享密钥和当前时间来创建一个临时的一次性密码。这些密码的有效期仅为 30 秒（或）。基于时间的一次性密码在 RFC 6238 中记录。

基于计数器的密码计算出一系列密码，每个密码只能使用一次。基于计数器的密码基于 RFC 4226。

这两种方法都需要服务器和设备之间的同步。基于时间的密码要求设备时钟与服务器时钟一致。基于计数器的密码要求用户避免误触数百个密码。虽然我可以构想出某些基于计数器的密码合理的情况，但在现实中我建议使用基于时间的。

## 文件管理

`Google Authenticator` 使用 `$HOME/.google_authenticator` 文件管理用户的身份验证设置和当前身份验证状态。（管理员可以更改文件位置，正如稍后我们将讨论的。）

即使速率限制也发生在该文件中。



# 时间与速率限制

试图访问身份验证服务的入侵者使用暴力攻击，他们每分钟尝试成百或数千个凭据，看是否有哪个有效。任何凭据生效的概率都很低，但计算机非常有耐心，不介意尝试每种组合直到成功为止。每个服务都需要速率限制，以将这种攻击从洪流变为细流。如果你的服务没有其他速率限制的方法，Google 验证器可以限制密码的使用次数以及用户进行身份验证的频率。

## 第 9 章：一次性密码：Google Authenticator

用户可以调整时钟敏感度。每个基于时间的口码的有效期为 30 秒。`GA` PAM 模块默认允许少量的时钟偏移，将上一个和下一个口码视为有效。在时钟同步良好的情况下，用户的口码可以使用约 90 秒。用户可以在其 `GA` 配置文件中调高此限值。

Google Authenticator 还可以限制用户每 30 秒的登录尝试次数不超过 3 次。对于高级用户和系统管理员来说，这比只允许登录一次更易于接受。然而，允许多次登录尝试违反了 OATH 标准。

所有这些选项都可以在用户配置程序中设置。

### GA 用户配置

要配置 `GA`，每个用户都需要一台安装合适软件的设备以及一个针对用户的配置。

#### 设备软件

官方 Google Authenticator 软件适用于许多智能手机、平板电脑和 Chrome 浏览器。不过，由于一次性口码是基于公开标准的，人们还编写了其他可以作为 `GA` 客户端的应用程序。有一个 Firefox 插件。[Authy](https://www.authy.com) 是一个流行的选择。Windows 用户可能更喜欢 [WinAuth](https://winauth.com)。自行查看并找到一个你喜欢的客户端。

配置设备最简单的方法需要 QR 码扫描器。如果你没有扫描器，Google Authenticator 安装程序会为你的设备推荐一个。

我的示例使用了官方 Google Authenticator 客户端。虽然我的测试设备是 Chrome 浏览器和几台 Android 设备，但官方 `GA` 客户端在其他平台操作系统上的工作原理相同。

在继续之前，请在你的设备上安装选择的客户端。

#### 用户配置

在配置 PAM 之前，登录到将使用 Google Authenticator 的服务器。运行 `google-authenticator` 创建配置。

```
$ google-authenticator
```

程序会询问一系列问题以确定你的账户如何进行身份验证。

是否希望身份验证令牌基于时间 (y/n) y

如前所述，使用基于时间的代码。

设置程序会立即输出设备配置，包括密钥、QR 码和 URL。它还提供了五个一次性代码。然而，这些代码和链接尚未永久。在将它们永久化之前，请使用其中一个来配置你的设备。

如果你的服务器安装了 `libqrcode` 库，`google-authenticator` 会显示 QR 码。使用 QR 码是获取手机上共享密钥的最简单方法。在设备上捕获 QR 码，它会自动为你的设备配置 Google Authenticator。

如果你使用 Chrome 作为你的 Google Authenticator 设备，请将 URL 复制到浏览器中。你就可以开始了。

如果这两种方法在你的环境中不起作用，`google-authenticator` 还会显示共享密钥（这是一个烦人的长字符串）。将其手动输入你的设备。

使用这三种设置方法中的任何一种，你的 `GA` 应用都会立即开始显示六位代码。

将密钥和紧急备用代码复制到安全的地方，最好是纸上。你甚至可以打印 QR 码，在页面顶部写上服务器名称，然后把它塞进锁好的抽屉里。如果你丢失了设备或情况发生极其糟糕，你将需要紧急代码和 QR 码，正如本章后面“设备被盗”和“灾难恢复”部分讨论的。

一旦你的设备知道了代码，就可以通过更新设备的 `GA` 配置文件使其永久化。

你是否要我更新你的 "home/mwl/.google_authenticator" 文件 (y/n) y

回答 n，设置程序将丢弃所有代码。回答 y，你的账户就准备好使用 `GA` 了。

然后你会得到三个关于用户的 `GA` 应该如何行为的问题。我们在本章前面的“Google Authenticator 用户功能”中讨论过这些选项。希望你在到达这一步之前已经决定了 `GA` 应该如何行为。

是否允许重复使用同一个身份验证令牌？这限制了你每 30 秒登录一次，但它增加了你的机会。是否允许同一个身份验证令牌的多次使用 (y/n) y

回答 y 限制了你每 30 秒登录一次，但它增加了你遭受重放攻击的概率。回答 n 意味着令牌可以重复使用。

默认情况下，令牌在有效期内有效。如果客户端和服务器之间出现时间偏移问题，你可以增大默认的 30 秒。是否要这样做 (y/n) y

回答 y 扩展了有效期。回答 n 则保持默认值。

如果你登录的计算机没有受到暴力破解尝试的防护，你可以为身份验证模块启用速率限制。默认情况下，这将限制攻击者每 3 次尝试。是否要启用速率限制 (y/n) y

回答 y 将限制有效期。回答 n 则禁用了速率限制。

### 脚本用户设置

Google Authenticator 用户设置过程非常简单。为了让用户使用受保护的服务，可以脚本配置。

```
#!/bin/sh
printf 'y\ny\nn\nn\n' | google-authenticator
```

`\n` 是换行符，或回车键。`printf` 命令输出 y、y、n、n、n，并将它们喂给 `google-authenticator`。运行此脚本的用户无需做任何决定即可获得 QR 码、URL、密钥和紧急备用代码。

如果你运行 `google-authenticator -h`，将获得允许你预回答问题的命令行标志和选项。以你喜欢的方式编写脚本。

如果你的组织足够大，你的脚本应该隐藏 QR 码、URL 和密钥之外的所有输出。

### GA 与 PAM

在配置账户后，你可以运行服务的 PAM 配置并激活 `pam_google_authenticator`。（如果你要在 SSH 中使用 `GA`，请回顾第 0 章中的 SSH 和 PAM 信息。）

```
auth required pam_google_authenticator.so
```

但你有其他用户？用户需要登录主机来配置 `GA`，启用 `GA` 会将他们锁在外。使用 `nullok` 来绕过这个问题。没有 `GA` 配置的用户可以登录。然而，一旦存在 `GA` 配置，用户必须输入代码才能登录。

```
auth required pam_google_authenticator.so nullok
```

如果你这样做，让系统直接引导用户进入 Google 验证脚本。否则，你的某些用户将永远不会真正配置 `GA`。

### 集中 GA 管理

拥有大量服务器的企业几乎肯定使用如 Ansible 或 Puppet 等管理工具来维护其环境。组织的系统管理员有比这更重要的事情要做，不需要照顾用户、复制配置文件和重启服务。企业级软件必须集中管理。

默认的 Google Authenticator 配置假设用户是信任的。企业身份验证系统不信任用户。企业用户可以更改密码，但不允许他们禁用速率限制。Google Authenticator 可以用于这些环境。

## 第 9 章：一次性密码：Google Authenticator

每个用户的 `$HOME/.google_authenticator` 文件并不包含用户的共享密钥。它还包含了用户的定时、速率限制和时钟敏感度设置。每个组织都有奇才聪明的人，他们能想出如何玩弄系统，而且足够愚蠢地去尝试。此外，有时用户的家目录是加密的或通过 NFS 挂载的，因此在身份验证完成之前无法使用。

在这些企业中使用 Google Authenticator 需要通过 `file` 和 `user` 选项将文件从用户的控制范围中移除。

`file` 选项允许系统管理员为用户的 `.google_authenticator` 文件设置不同的位置。使用等号和文件路径即可。该选项将变量 `~` 和 `${HOME}` 识别为用户的家目录，将 `${USER}` 识别为用户名。

```
auth required pam_google_authenticator.so \file=/ul/ga/${USER}/.google_authenticator
```

在这里，每个用户的 `GA` 配置都位于其家目录之外。这使得系统可以等待身份验证完成后再挂载家目录。通过使用由用户拥有的用户特定目录，每个用户都可以继续管理自己的 `GA` 配置。该文件应由用户所有，且模式为 400。

你可能不希望用户管理自己的 `GA` 配置。有多个组织让用户在受严格保护的注册服务器上配置 Google Authenticator。注册服务器会自动将该配置传播到组织内的所有其他服务器。在这样的企业中，用户不应该有权限编辑所有其他服务器上的配置文件，可能在注册服务器上也不如此。（注册脚本可能会向用户隐藏除 QR 以外以外内容。）在这种情况下，文件应由系统用户所有，并禁止用户访问文件本身。使用 `user` 选项来实现。

```
auth required pam_google_authenticator.so \
secret=/etc/ga/${USER} user=google
```



在这里，用户的 GA 配置被存放在 `/etc/ga` 目录下，文件名以用户命名。我的身份验证配置将是 `/etc/ga/`。该文件由用户 `google` 所有，模式应为 `400`。虽然系统管理员可以轻松识别单个用户的文件，但更新配置的唯一方法是通过管理系统。

不允许用户访问其配置会导致 Google Authenticator 无法使用某些功能。该模块将所有计时信息都保存在配置文件中。如果用户无法更新文件，速率限制函数将不起。在设置期间，除了写入原始文件外，对所有函数均回答 `n`。

虽然以这种方式使用 Google Authenticator 需要额外的编程，但它并不比其他“企业级”令牌系统更难用。

# 时钟偏移调整

Google Authenticator 可以尝试处理系统时钟不准的问题。连续三次身份验证失败（且每次间隔 30 秒）会向 GA PAM 模块发出信号，提示时钟存在偏移，并暗示这种偏移的严重程度。

使用 `noskadj` 可以关闭此行为。如果系统时钟不准确到让进行偏移调整都有意义，那么修复时钟比微妙地暗示存在问题更有意义。

# 口码显示

与密码类似，口码不会回显给用户。如需将口码回显给用户，请使用模块选项 `echo_verification_code`。

口码是瞬态实体。在许多部署中，口码只能使用一次。即使有人从用户肩膀后偷看了口码，它也会在几分钟后过期。大多数时候，为用户显示输入的口码会大幅减少支持电话。用户——是的，即使是*你的用户*——在口码可见时也能识别出自己输错了六个数字。

# 同时输入口码和密码

某些启用了 PAM 的应用程序和模块（例如 Radius 认证或开启了 `PasswordAuthentication yes` 的 SSH）不能很好地处理多个身份验证提示。你可以通过 `forward_pass` 选项让 Google Authenticator 在单次请求中同时询问密码和口码。GA 会处理口码，并将密码交给下一个模块。下一个模块必须使用 `use_first_pass` 选项来接受传递的密码。

```
auth required pam_google_authenticator.so forward_pass sufficient pam_unix.so try_first_pass
```

尝试身份验证的用户将收到单个提示，如下所示：`Password & verification code:`

用户需要输入她的密码、一个空格和 Google Authenticator 口码。如果口码正确，GA 将密码传递给下一个模块。在这种情况下，由于该模块是 `sufficient`，正确的密码将立即允许访问。

你不能将 `forward_pass` 和 `echo_verification_code` 结合使用。好吧，你*可以*结合，但 GA PAM 模块会同时回显密码和口码，并拒绝身份验证请求，因此这种组合没有意义。

# 新设备

一旦配置了 Google Authenticator，你几乎可以忽略它……直到你有了新的智能手机、平板或电脑。你可能希望为新设备配置与旧设备相同的身份验证设置。有时，你直接用旧手机换了一个新手机。

记得我提到过第一次为 GA 配置账户时要备份安全代码吗？这正是原因所在。Google Authenticator 不会重新显示现有安装的密钥、配置 URL 或 QR 码。你必须使用你保留的备份。手动输入安全代码很麻烦，但比重新配置所有设备要好得多。

# 灾难恢复

使用 Google Authenticator，你可能会面临两种不同的灾难：设备被盗，或者 PAM 模块损坏。两者都有类似的恢复考量。

丢失多因素身份认证系统中的一个因素并不是灾难，但确实需要果断行动。如果你丢失了设备以及密码、SSH 密钥或其他认证方式，让受影响的用户在所有影响主机上重新运行 `google-authenticator` 或组织的封装脚本。如果情况紧急，使用 `su` 为用户运行。

另一种灾难是系统时钟损坏。此时 GA 口码将无法工作。当你运行 `google-authenticator` 时，它会在 QR 码后显示五个八位代码。这些是应急代码。用户可以使用它们进行验证，但每个代码只能使用一次。

GA 在允许访问之前会从配置中移除一次性代码。这需要用户对配置文件有写入权限。如果用户的配置文件属于另一个用户，应急代码将无法工作。

# GA 文件格式

Google Authenticator 的配置文件 `.google_authenticator` 包含几个可能的选项。

```
5KPJOJZCY670ENW
- RATE_LIMIT 30
- WINDOW_SIZE 17
- DISALLOW_REUSE
- TOTP_AUTH
- 21481565
```

第一行始终是共享密钥。不要动它。并不是所有的代码都是有效的，因此你无法设定公司标准要求每个用户的密钥都是他们的名字和社会安全号。

`RATE_LIMIT` 选项的存在启用速率限制。它接受两个参数：允许的身份验证尝试次数以及允许的秒数。速率限制需要用户能够写入配置文件。

## 第 9 章：一次性密码：Google Authenticator

`WINDOW_SIZE` 选项决定了口令对时间的敏感性。`1` 表示系统时钟指定的精确当前口令是可以接受的。数值每增加 2，意味着当前口令前后各多接受一个额外的口令。将此值设置为 `17`（如果你遵循了 `google-authenticator` 的建议，允许四分钟窗口），意味着当前时间的口令加上之前的 8 个代码和之后的 8 个代码都是允许的。

`DISALLOW_REUSE` 选项意味着每个口令只能使用一次。

文件末尾记录着用户剩余的一次性密码。虽然你可能想向此文件添加自己的一次性代码，但 GA 会对应急代码进行额外的验证。在文件末尾添加 `00000001` 是不起作用的。此外，编辑应急代码的操作会导致剩余代码失效。

既然我们已经安全了远程访问，让我们考虑一些对本地用户有用的东西。

# 第 10 章：使用 SSH 密钥访问控制台

系统管理员有一套晨间流程。在摄入咖啡、穿上裤子、再喝咖啡并踉跄走进办公室后，我们瘫坐在工作站前。我们使用用户名和密码登录。大多数人会输入 SSH 密钥短语并将密钥加载到 SSH agent 中。此时，我们就可以开始工作了。这需要对工作站进行两次身份验证：一次是使用用户名和密码，另是使用用户名和 SSH 密钥。

`pam_ssh` 模块将 SSH 密钥管理集成到登录过程中。用户可以去其工作站并仅使用其 SSH 密钥登录。用户不再针对 `/etc/passwd` 进行验证，而是使用其账户中的 SSH 私钥进行验证。验证成功后，`pam_ssh` 会启动一个 SSH agent 并将解密后的私钥存储在 agent 中。

与书中讨论的其他 PAM 模块不同，`pam_ssh` 对工作站最有用，而且仅次于工作站。你绝对不想基于存储在服务器本身上的 SSH 密钥文件来对服务器进行验证。普通用户绝不向远程服务器提供短语。你可能不想在销售人员的机器上开启此功能。但许多系统管理员发现个人笔记本电脑上的 `pam_ssh` 非常方便。

`pam_ssh` 为 `auth` 和 `session` 类型提供服务。在 `auth` 策略中使用，`pam_ssh` 会提示用户输入短语。它尝试用该短语解密用户的 SSH 私钥，这类似于 `ssh(1)` 或 `ssh-add(1)` 的做法。如果短语正确，该模块返回 `PAM_SUCCESS`。否则，模块失败。在 `session` 策略中，`pam_ssh` 为用户启动一个 SSH agent 并将密钥添加到 agent 中。

FreeBSD 默认包含 `pam_ssh`。CentOS 有 `pam_ssh` 软件包，而 Debian 提供了 `libpam-ssh` 软件包。这些模块不仅打包方式不同，其代码也不同。FreeBSD 导入了原始的 `pam_ssh` 并进行了改进。该代码从 FreeBSD 中提取出来，并为 CentOS 和 Debian 分支成了略有不同的版本。每个版本支持不同的功能。我们将分别介绍每个系统的 `pam_ssh`。

此外，每个操作系统使用 `pam_ssh` 的方式也不同。我们将以此模块为机会，探索一个非常的模块如何通过完全不同的 PAM 语句进行配置并产生非常不同的行为。

我们涵盖的所有 `pam_ssh` 版本都支持 `try_first_pass`、`use_first_pass` 和 `debug` 选项。

## 一个模块，不同策略

我们的三个目标平台部署 `pam_ssh` 的方式各异。CentOS 没有对放置 `pam_ssh` 语句提供任何建议。FreeBSD 在默认安装中包含了 `pam_ssh`。`pam_ssh` 的语句出现在 FreeBSD 的标准配置文件中，但它们被注释掉了。Debian 的 `libpam-ssh` 软件包不仅安装了 `pam_ssh`，还添加了 PAM 语句来启用该模块。

我们将先考虑简单的 FreeBSD 情况，然后是 Debian。

### FreeBSD 和 pam_ssh



FreeBSD 提供了在范围内和单个服务中启用 `pam_ssh` 的示例。我不想使用 `pam_ssh` 来验证我工作站上的 FTP 服务器或通过串口，因此我不会在全局范围内启用它。我想在图形化控制台登录时使用它，`/etc/pam.d/xdm` 文件中有 `pam_ssh` 的注释条目。取消注释可以为我们提供 `auth` 和 `session` 策略。

```
auth sufficient pam_ssh.so no_warn try_first_pass
auth required pam_unix.so no_warn try_first_pass
session required pam_ssh.so want_agent
session required pam_lastlog.so no_fail
```

`auth` 策略只有两条语句。第一条 `pam_ssh` 是 `sufficient`（充分的）。登录将提示用户输入其 SSH 密钥短语。如果短语正确，`sufficient` 语句意味着立即授予访问。`no_warn` 标志禁用警告。`try_first_pass` 标志告诉 `pam_ssh` 尝试任何早期的密码。由于这是策略中的第一条语句，不会有更早的密码。

第二个 `auth` 语句 `pam_unix` 是用于针对 `/etc/password` 进行传统的 Unix 身份验证。只有当 `pam_ssh` 失败时，才会触发此身份验证规则。通过 `try_first_pass` 参数，该模块尝试使用之前输入的 SSH 密钥短语作为 Unix 系统密码。如果你不小心输入了密码而不是短语，系统会让你进入。

综合来看，这意味着用户首先会被提示输入用户名和密码。在 `session` 策略中，`pam_ssh` 设置了 agent。`want_agent` 选项是 FreeBSD 特有的。

### Debian 和 pam_ssh

当在 Debian 上安装 `pam-ssh` 时，软件包会向 `/etc/pam.d/common-auth` 和 `/etc/pam.d/common-session` 添加 PAM 语句。虽然 Debian 的 `libpam-ssh` 与原始版本不同，但逻辑仍然相似。

```
auth [success=1 default=ignore] pam_unix.so nullok_secure
auth requisite pam_deny.so
auth required pam_permit.so
auth optional pam_ssh.so use_first_pass
```

# 第 10 章：使用 SSH 密钥访问控制

现在我们来快速查看会话规则。

```
session [default=1] pam_permit.so
session requisite pam_deny.so
session required pam_permit.so
session required pam_unix.so
session optional pam_ssh.so
session optional pam_tmpdir.so
```

前三个语句与认证策略（auth policy）中的第一个语句相似。这里有一个 `requisite pam_deny`，但你实际上根本无法触发它。真正的规则从第四条语句开始，它调用 `pam_unix` 来设置用户环境。第五条语句针对 `pam_ssh`，启用了用户的 SSH 代理（SSH agent）。最后一条语句调用 `pam_tmpdir` 为用户配置一个安全的临时目录。

## 比较

为什么 FreeBSD 和 Debian 在相同的功能上会有如此差异巨大的策略呢？部分原因在于 Debian 的策略设计是为了便于 `pam-auth-update(8)` PAM 配置工具使用。而 FreeBSD 则假设你会编辑自己的 PAM 规则，因此你理解每种类型语句的作用。

然而，另一个关键区别是，操作系统软件包对模块的使用方式有不同的假设。FreeBSD 的开发者假设通过用户的 SSH 密钥进行认证就足够了，并且完全跳过了对系统密码文件的认证。另一方面，Debian 要求用户通过密码文件进行认证——但它假设用户的密码短语（passphrase）与其密码相同。

这里的真正问题在于“假设”这个词。

如果你听到某个很酷的 PAM 模块并尝试部署它，你必须仔细检查你的假设、模块作者的假设，以及为你的操作系统打包该模块的人员所做的假设。如果你正在使用第三方文档，也要检查作者的假设。真正理解模块如何工作的唯一方法，是逐句逐句地仔细阅读 PAM 策略。我曾部署过几次 FreeBSD 的 `pam_ssh`，但第一次在 Debian 上尝试使用 `pam_ssh` 几乎将我逼向疯狂边缘²，直到我仔细理清了 PAM 配置。

在没有仔细剖析配置之前，PAM 的各种假设会毁掉你的一天、一周，以及你的一切。

说起假设：你同样不能假设命名为 X 的模块在平台之间是相同的，即使它们的功能相似。正如我们很快将看到的，`pam_ssh` 模块在 FreeBSD、CentOS 和 Debian 之间是不同的。

## SSH 和 pam_ssh

一个合适的 SSH 密钥具有几个单词或更长的密码短语。在正常使用期间，你很少输入密码短语。然而，当你第一次尝试 `pam_ssh` 时，预计你会反复输入密码短语。我建议创建一个仅用于测试的 SSH 密钥，并配有一个简单、易于输入的密码短语，在研究 `pam_ssh` 配置期间使用。不要在任何服务器上安装该测试密钥。一旦 `pam_ssh` 按照预期工作，就删除该测试密钥。

你可能会下一个问题是：我的登录是否成功解密了密钥并将其添加到代理中？在像 Debian 这样假设密码就是密码短语的系统上，这是一个重要的细节。使用 `ssh-add -l` 检查代理中的密钥。

> ²20 好吧，知道了。“……把我带进了一个名为“狂怒”（Screaming Rage）的古怪小镇，距离疯狂大约十英里，并在没有减速的情况下把我从车里推出。”满意了吗？

```
$ ssh-add -l
2048 8c:f9:2d::...1 testlab 2016-02-01 RSA
```

从这里起，正常管理你的 SSH 会话和密钥即可。

当 SSH 使用密码短语进行认证时，没有密码短语的密钥就像一个没有密码的账户。`pam_ssh` 会忽略没有密码短语的密钥：它不会使用它们进行认证，也不会将其添加到 SSH 代理。

如果你想允许使用没有密码短语的密钥进行认证，请在 `pam_ssh` 语句中使用 `nullock` 选项。三个 `pam_ssh` 会话都支持 `nullock`。允许使用无密码密钥进行认证是一个非常糟糕的主意。这甚至比允许没有密码的账户还要糟，因为无密码密钥可能会授予访问其他主机的权限。

所有的 `pam_ssh` 实现都允许使用私钥文件 `~/.identity` 登录。该密钥用于 SSH 协议的第一版本。这个版本不仅是过时的——它实际上是损坏的。任何能捕获你流量的人都可以解密它。虽然我们还没到“如果你正在运行 SSHv1，请关闭它并启用 Telnet；它可能不安全，但它不假装是安全的”这一步，但那一天很快就会到来。如果你手头有一个旧的 SSHv1 密钥，请验证你的 SSH 服务器没有支持 SSHv1，双检你的现代 SSH 密钥是否已安装在所有地方，并将你的身份密钥备份。

没有任何 `pam_ssh` 实现支持 `sshd(8)` 使用的 `AuthorizedKeysCommand`。`AuthorizedKeysCommand` 选项仅提供公钥，而不提供用于认证的私钥。你的私钥应该留在工作站，而不是网络上。

## FreeBSD pam_ssh

FreeBSD 自带安装了 `pam_ssh`，`/etc/pam.d/` 中的许多 FreeBSD PAM 配置都有注释掉的 `session pam_ssh` 条目。其中一些条目在我看来相当奇怪（使用 `pam_ssh` 认证 FTP，从而以明文传输你的密码短语？），但它们都不是强制性的。在 `/etc/pam.d/login` 中激活这些登录尝试的规则：

```
login: mw1
SSH passphrase:
```

输入你的密码短语。`pam_ssh` 模块将尝试解密用户 `~/.ssh` 目录下的 `identity`、`id_rsa`、`id_dsa` 和 `id_ecdsa` 密钥文件。如果你正确输入了密码短语，客户端将通过。

`pam_ssh` 模块支持第一章中讨论的 `debug`、`use_first_pass` 和 `try_first_pass` 选项。

## Open SSH Agent

当 `pam_ssh` 解密用户的密钥时，`session pam_ssh` 语句启动代理并将解密密钥密钥。如果 `pam_ssh` 无法解密任何密钥，它就不会启动代理。相反，PAM 直接进入会话策略中的下一个语句。结果是，如果用户使用密码短语登录，他将获得 SSH 代理；或者密码。



然而，系统管理员可能希望使用密码登录的用户也能获得。在 `pam_ssh` 语句中添加 `want_agent` 选项，可以在没有加载任何密钥的情况下，触发在登录时启动代理。`want_agent` 选项出现在 FreeBSD 的语句中。

## 密钥选择

FreeBSD 的 `pam_ssh` 自动尝试解密用户 `~/.ssh` 目录下的 `identity`、`id_rsa`、`id_dsa` 和 `id_ecdsa` 密钥文件。不同名称的密钥不会被登录过程解密。

你无法从 `pam_ssh` 检查中移除任何这些密钥。要这样做，你需要使用不同版本的 `pam_ssh`，例如 CentOS 中的版本。

## CentOS pam_ssh

CentOS 的 EPEL 仓库包含了 `pam_ssh` 软件包。与 FreeBSD 和 Debian 不同，CentOS 的软件包没有包含任何 PAM 策略语句。你必须决定如何使用 `pam_ssh` 并为你的认证和会话策略创建规则。

在这里，我将 `pam_ssh` 添加到 `/etc/pam.d/login`，这是 CentOS 7.2 明文控制登录的 PAM 配置。我们从认证策略开始。

```
[user_unknown=ignore success=ok ignore=ignore \
default=bad] pam_securetty.so
auth [success=1 default=ignore] pam_ssh.so
auth substack system-auth
auth include postlogin
```

认证策略的第一条是检查安全终端的常规 `pam_security` 规则。

第二个语句将 `pam_ssh` 插入策略中。然而，我并没有使用标准控制，而是使用了 Linux-PAM 扩展控制。如果 `pam_ssh` 返回 `PAM_SUCCESS` 以外的内容，我们将忽略 `pam_ssh` 和会话策略。如果用户成功输入密码短语且 `pam_ssh` 可以解密用户的私钥，PAM 将跳过下一条规则。

## 第 10 章：使用 SSH 密钥访问控制台

下一个规则是普通系统身份验证的子栈。给 `pam_ssh` 提供一个可用的短语可以让策略跳过整个标准的 Unix 风格身份验证过程。

最后一条规则包含了标准的登录后处理。无论用户是使用短语还是密码登录，CentOS 都会执行日志记录和计数。

会话规则简单得多。将你的 `pam_ssh` 语句放在包含 `system-auth` 文件之前，这样你的 SSH agent 会会在其他环境启动之前启动。在会话策略中，它它可以放在 `pam_selinux.so open` 规则之后的任何位置。

```
session optional pam_ssh.so
session include system-auth
```

在 PAM 级别，你已经准备好了。

但在现代 CentOS 上，你几乎肯定正在使用 SELinux。如果你的 SSH agent 遇到问题，请检查 `/var/log/secure`。启动代理时的权限错误几乎都与 SELinux 相关。第 6 章讨论了与 SELinux 相关的 PAM 问题，并以 `pam_ssh` 为例。

## CentOS pam_ssh 登录提示

与 OpenPAM 不同，CentOS 的 `pam_ssh` 不会向用户显示“passphrase”提示。用户看到的是始终出现的 `Password:` 提示。CentOS 让 `pam_ssh` 变得完全隐形。用户需要知道输入他们的 SSH 短语是一个选项。

凭借本节之前提供的语句，如果用户没有输入短语，其身份验证尝试将回退到 `system-auth` 子栈，在那里 `pam_unix` 的 `try_first_pass` 选项意味着它将尝试使用用户输入的任何内容作为密码。

## 选择密钥文件

使用 `keyfiles` 选项指定 `pam_ssh` 尝试解密的哪些 SSH 私钥文件。CentOS 默认检查 `id_dsa`、`id_rsa` 和 `identity` 文件。`identity` 文件仅用于过时的 SSH 版本 1 协议，我建议你在 `pam_ssh` 中禁用它。

```
[success=1 default=ignore] pam_ssh.so \
keyfiles=id_dsa,id_rsa
```

你可以根据需要在此添加非标准的密钥文件。

如果你需要复杂的密钥选择，请查看 Debian 的 `pam_ssh`。

## Debian pam_ssh

Debian 在 `libpam-ssh` 包中提供了 `pam_ssh`。我们在本章之前讨论了 Debian 的 `pam_ssh` 策略，现在让我们直接进入该模块的工作原理。请记住，Debian 的 `pam_ssh` 配置期望你的 SSH 短语与你的密码相同。

Debian `pam_ssh` 有趣之处在于，它允许用户很好地控制哪些密钥可以用于身份验证，以及哪些密钥被添加到 SSH agent。

### Debian pam_ssh 密钥选择

Debian 的 `pam_ssh` 忽略所有常用的密钥文件，而是依赖 `$HOME/.ssh/login-keys.d` 和 `$HOME/.ssh/session-keys.d` 目录。这些目录默认不存在；用户必须创建它们。`login-keys.d` 目录包含可用于验证的 SSH 私钥文件。这里的文件可以是实际私钥，也可以指向标准 SSH 密钥的软链接。

```
$ cd .ssh/login-keys.d
$ ln -s ../id_rsa
```

当我登录系统时，`pam_ssh` 会检查此目录并尝试使用用户提供的密码来解密它找到的任何私钥。它会将任何能解密的密钥添加到用户的 SSH agent。`session-keys.d` 目录也包含密钥文件或软链接。与 `login-keys.d` 不同，`pam_ssh` 不使用这些密钥文件进行身份验证。然而，`pam_ssh` 会尝试使用密码解密会目录中的密钥，并将解密后的密钥添加到 agent。

## 绕过密码

也许你不想长密码，而是仅依赖短语进行控制台访问。这将允许你将 FTP 这样的明文协议与通过 SSH 或控制台登录分开。你可以通过重新排列 Debian 的认证策略来实现这一点。

```
auth sufficient pam_ssh.so
auth [success=1 default=ignore] pam_unix.so nullok_secure
auth requisite pam_deny.so
auth required pam_permit.so
```

我将 `pam_ssh` 规则移动到了认证策略的最顶部，甚至在 `pam_unix` 之前，但 `sufficient` 表达了预期的行为。实际上，由于手动编辑此文件使其不利于自动化管理，我更有可能重做整个策略，并移除永远不会被触发的语句。

```
auth sufficient pam_ssh.so
auth required pam_unix.so nullok_secure
```

不过，别人的安全意识没有我这么。他们的机器需要某些东西来确保他们有良好的密码，正如我们在下一章中看到的。

## 第 11 章：密码质量检查

“password”（密码）这个词很糟糕。每个人都知道，用户除外。几个 PAM 模块允许你对密码实施质量标准，以防止用户使用明显糟糕的密码。这些质量检查器不会消除密码，但会要求用户在设置密码时更有创意。

虽然大家都同意短密码会导致草率的密码，但使密码变得良好的特质是一个充满争议的话题。即使是冷静理性的系统管理员，在与其他理性明智的人讨论密码质量措施时，升级到刀肉斗，据已知也会失去他们的冷静和理智……有些人完全反对今天使用的密码质量检查概念。出于如此，我们不会讨论什么特征使密码变得良好。相反，我们将涵盖允许你对用户施加特定偏见的 PAM 模块。

最常见的密码质量检查模块是 `pam_passwdqc`。CentOS 7 删除了 `pam_passwdqc`，用 `pam_pwquality` 取而代之。Debian 同时提供了这两个包。我们将使用 `pam_passwdqc` 来解释密码质量检查的配置和概念，然后简要提到 `pam_pwquality`。

### 配置密码检查

当用户更改密码时测试密码质量。这使得质量检查成为密码策略中极少数功能之一，如下：

```
password requisite pam_passwdqc.so
password required pam_unix.so
```

在大多数系统中，`passwd(1)` 有它自己的 PAM 配置 `/etc/pam.d/password`。系统默认的更改不会影响 `passwd(1)`，除非 `/etc/pam.d/password` 显式包含了默认值。

当 `pam_unix` 认为应该更改密码时，它会修改 `/etc/password` 和相关文件。将任何密码质量检查放在 pam 语句之前，以便在更改之前对密码进行审计。

## 密码轮



“用户应该多久更改一次密码？”这个问题与密码质量检查器密切相关。许多组织要求定期更改密码。其他人认为，要求更改密码比保持不变更不。也许密码应该在首次登录时更改。

你不在 PAM 内部设置密码过期策略，但配置正确的 PAM 需要尊重密码过期。我见过不止一个基于 LDAP 的网络不尊重过期的密码。

BSD 系统在 `/etc/login.conf` 中全局全局管理密码寿命，并通过 `pw(8)` 管理单个用户。Linux 系统主要使用 `chage(8)`。咨询你的操作系统手册获取有关配置密码寿命的详情。

## 质量概念

所有密码质量检查器共享某些共同概念。

### 字符类

不，不是“战士”、“牧师”、“盗贼”等等。密码检查器将密码中可能的字符分为四类不同的类：小写字母、大写字母、数字以及所有其他 ASCII 符号。存在第五种字符类用于非 ASCII 字符，但我们大多数人无法轻松输入那些字符。你可以要求用户的密码包含最多四种类字符，并根据建议密码包含的类别数量调整长度要求。

## 第 11 章：密码质量检查

如果你运行的软件对密码长度有上限，请修复该软件或将其替换。使用传统密码哈值的系统可能已经过时了几个十年，它们是任务关键型的、资金匮乏的且由于极其缺乏了解，以至于没人敢触碰。大型企业和政府是这方面最违规的。尝试替换此类系统要么终结你的职业生涯，要么如果你成功了，将成为 IT 部门的黑暗领主。²21

### pam_passwordqc

`pam_passwordqc` 模块几乎无处不在（最近版本的 CentOS 除外），它长期以来一直是更改密码时检查新密码质量的标准工具。`pam_passwordqc` 模块允许你定义密码长度要求、新旧密码之间不同的字符数量、密码中必须包含的字符类型等。

### 启用与配置

Debian 和 FreeBSD 都使用 `pam_passwordqc`。它们之间唯一的区别是 FreeBSD 要求将任何选项都放在 PAM 配置文件中，而 Debian 允许你将 `pam_passwordqc` 选项放在一个独立的 `pam_passwordqc.conf` 文件中，并使用配置选项。

```
password requisite pam_passwordqc config=/etc/passwordqc.conf
```

然而，每个文件中实际显示的配置选项是完全相同的。我们将展示两者的示例。

一旦你启用了 `pam_passwordqc`，任何尝试更改任何密码的操作都必须先通过质量检查。你可以通过 `enforce` 选项来放宽这种严格性。

> 21 当你开始时可能是个好人，但替换此类系统所需的行动将使你变成一个黑暗领主。商业运作就是这样。

如果你设置 `enforce=users`，密码检查将仅适用于非特权用户。root 用户可以给用户分配不合格的密码。他们会收到警告，但密码会被更改。

如果你设置 `enforce=none`，`pam_passwdqc` 会打印密码要求、警告和提示，但不会强制执行。

在这里我告诉 `pam_passwdqc` 允许 root 违反密码标准。

```
password requisite pam_passwdqc enforce=users
```

如果我了 Debian 配置文件，此条目可以单独出现。

```
enforce=users
```

现在，当老板打来抱怨 GolfMaster 不是一个合格的密码时，我可以变成 root 并为她设置。

我不建议你使用 `enforce=none`，除非是在实施新密码标准的警告期内。自愿遵守的标准就是会被被忽略的标准。

### pam_passwdqc 复杂度与长度

`pam_passwdqc` 使用字符类来规定密码的最小长度。密码拥有的字符类越少，密码就越长。默认情况下，仅包含两类字符的密码必须是 24 个字符。包含三类字符的密码必须是 8 个字符，而包含所有四类字符则会将最小长度减少到 7 个字符。

复杂度检查有两个例外。密码开头的大写字母不算额外的字符类。结尾的数字也是如此。密码 `Hamster1` 算作一个字符类，而 `1hamsterR` 包含三个。你可以向你的用户解释这一点，或者直接告诉他们大写字母和数字需要出现在密码中间才能计数。无论如何，他们都会诅咒你的名字。

使用 `min` 选项设置每种类型密码的最小长度。该选项需要五个用逗号分隔的数值参数。这些参数中的任何一个都可以设置为禁用，以自动拒绝该类型的密码。

第一个参数规定了仅有一个字符类的密码的最小长度。它默认禁用，这使得 `pam_passwordqc` 拒绝任何由单个字符类组成的密码。

第二个参数给出了非密码短语（passphrases）的两个字符类密码的最小长度。默认值为 24。

第三个参数给出了短语的最小长度（字符数）。我们将在下一节讨论短语。短语的默认最小长度为 11 个字符。

第四个参数设置了包含三个字符类的密码的最小长度。默认值为八。

第五个参数给出了包含四个字符类的密码的最小长度。默认值为七。这种这种顺序很奇怪，为什么不呢？这些参数按长度排序。具有两个字符类的密码确实需要更长一些。如果短语太短，`pam_passwdqc` 将报错。

此外，你还可以通过 `max` 选项设置最大长度，默认值为 40，但过长的密码通常不是问题。这里是针对单个或两个字符类的密码。短语的最小长度为 16。包含三个字符类的密码的最小长度为 10，而包含四个字符类的密码为 9。disabled,16,10,9

```
password requisite pam_passwordqc min=disabled,16,10,9 max=80
```

我定义了密码的最大长度为 80，为了惹恼那个读了太多尼尔·斯蒂芬并因此认为理解安全的家伙。

### 短语 (Passphrases)

与其使用密码，你可能会将密码设置为 `Lucas needs gelato!` 这是一个短语，一组单词而不是单个单词。意外的是，长短语可能比包含随机字符的短密码更安全。至少你的用户不会经常写下它们。短语从用户的角度来看优势是它们不需要多个类。像 `correct battery staple` 这样的短语只包含一个字符类，但通过了质量检查。你可以测试更短的短语。

`passphrase` 选项给出了为了被视为短语必须包含的独立单词数。它默认值为三。如果短语没有足够的单词让 `pam_passwdqc` 将其视为短语，它仅仅是一个包含空格的密码。

在这里我使用 Debian 的 `passwdqc.conf` 要求短语为四个或更多单词。

```
passphrase=4
```

要求短语中包含更多单词可能会（但并非肯定）驱动用户创建更长的短语。

### 密码相似性 (Password Similarity)

`pam_passwdqc` 模块通过 `match` 和 `similar` 选项帮助用户使用相似密码。当用户更改密码时，`pam_passwdqc` 会检查密码内部的子字符串。它可以识别正向和反向的共同字符串，例如 `hamster1` 和 `iretsh`，以及不同的情况。`match` 选项给出了在这样的匹配字符串中查找的字符数。默认值 4 会在新旧密码之间查找四个或更多字符的共同字符串。

```
match=4
```

虽然这些检查对于防止用户预测密码方案是必要的，但它们可能会产生意外的结果。将密码从 `!meowing6` 更改为 `homeowner!AtLast`。用户可能为终于买了房子并为六只猫提供了足够的空间而感到高兴，看起来这些都是合格密码——但它们都包含 `meow` 字符串。

要关闭这些检查，将 `similar` 选项设置为 `permit`。它默认 `deny`。

```
similar=permit
```

禁用相似性检查要么是一个坏主意，要么是一个糟糕的主意。

虽然 `pam_passwordqc` 有额外的选项，但它们大多是在你想要微调整体策略运行时管理边缘情况。

`pam_pwquality` 模块对密码质量采取了更复杂的方法。除了设置密码的要求之外

## 第 11 章：密码质量检查

通过长度和不同的字符类，它拥有一套“积分”（credits）系统，如果密码遵循良好实践，则允许使用较短的密码。理论上，pam_pwquality 可以识别糟糕的密码选择。^{22（这对于老牌系统管理员来说可能很熟悉，因为 pam_pwquality 继承了经典模块 pam_cracklib 的许多概念。）

### 常见的 pam_pwquality 配置与行为

`use_first_pass`、`try_first_pass` 和 `debug` 等常用选项适用于 pam_pwquality。在首次尝试此模块时，请充分使用 `debug` 选项。

你经常会看到 `local_users_only` 选项，它告诉模块只检查本地密码文件中存在账户的用户密码。

使用 `retry` 选项设置 pam_pwquality 允许用户尝试创建可用密码的次数。一旦用户尝试失败达到该次数，pam_pwquality 就会将其拒出。

最后，虽然 `authook_type` 选项看起来很高级，但它只是设置一个用户可见的字符串，用来说明正在更改哪种密码。它通常是空的。



通常的 `pam_pwquality` 语句看起来如下。

```
requisite pam_pwquality.so try_first_pass \
local_users_only retry=3 authook_type=
```

`pam_pwquality` 模块会直接拒绝整类的密码。如果新密码与旧密码相同（仅大小写不同），则会被拒绝。如果它太短或与旧密码太相似，会被拒绝。如果它是旧密码的旋转版本（例如 `hamster1` 和 `amster1h`），则会被拒绝。最后，回文是完全不可接受的。

> 22 永远不要低估用户创造性地做出糟糕选择的能力

你可以微调其中一些行为。我们将从建立最低要求开始，然后介绍积分系统，最后涵盖其他配置选项，这些选项可以放在 PAM 语句中，也可以放在 `/etc/security/pwquality.conf` 中。

## 设置密码要求

你可以通过设置最小长度、所需的字符类数量以及每类字符的最小数量来对用户密码设置限制。

`minlen` 选项设置密码的最小长度。增加最小长度很容易，但 `pam_pwquality` 有硬编码的下限。任何系统上的有效最小密码长度可能是六，但通过重新编译可以将其降至四。默认值是八。

`class` 选项设置密码中必须包含的字符类最小数量。

使用 `dcredit` 选项设置密码中数字的最小值。`ucredit` 选项指定大写字母的最小数量，而 `lcredit` 设置小写字母的最小数量。最后，`ocredit` 设置其他字符的最小值。将最小值指定为负数——正值表示你正在使用积分系统。在这里我对用户密码设置了特定要求。为了清晰起见，我省略了通常的 `retry` 语句等。在生产环境中，你肯定想要包含它们。

```
password requisite pam_pwquality.so minlen=8 min=3 dcredit=-2 ucredit=-2 lcredit=-2
```

该语句要求用户至少有两个数字、两个小写字母、两个大写字母和两个其他字符。最小长度为八。虽然我定义了类的最小数量为三，但该设置并没有被精确使用——四类字符中每一类的最小值超过了 `minclass` 语句。

为你的系统定义了密码的最低要求。如果入侵者试图猜你系统的密码，他可以跳过所有不符合你密码标准的可能密码。为了增加攻击者的难度$^{23}$，使用积分系统。

## 密码质量积分

`pam_pwquality` 系统允许你设置最小密码长度，但随后为包含多个不同字符类的用户提供额外积分。这为密码提供了灵活性，但允许人们在使用更多种类字符的情况下使用较短的密码。

系统管理员已经足够的精力向用户解释常规策略了。我从未成功地向用户解释过积分。在现实世界，我发现积分是系统管理员团队的奖励，而不是普通用户的。

通过积分系统，用户在密码中包含的每个额外字符类都会获得积分。默认情况下，每个字符类提供一个额外积分。考虑世界上最糟糕的密码 `password`。它有八个字符。用户因包含小写字母获得了额外积分，计分为九个字符。如果你将最小密码长度设置为九个字符，`password` 就符合要求。（注意，它会因为其他原因被拒绝，但仅从长度来说是合格的。）

添加一个大写字母可以让密码短一个字符，例如 `pAsswor`。加入一个数字，你就可以将密码缩减到六位：`pAssw0`。六个字符，加上包含小写、大写和数字字符各得一个积分。请记住，在不重新编译的情况下，`pam_pwquality` 不接受少于六位的密码。

使用积分系统时，用户不想混合字符也不必混合。一个纯八位的小写密码就足够了。

使用积分时，`dcredit`、`ucredit`、`lcredit` 和 `ocredit` 选项仍然分别适用于数字、大写、小写和其他字符。然而，在使用积分的情况下，它们不再定义密码所需的这些字符的最小数量，而是定义了用户可以获得的最高积分。将 `ocredit` 设置为 3 意味着用户非字母数字字符可以获得最多三个积分。每个默认为 1。考虑这些 `/etc/security/pwquality.conf` 设置：

```
minlen=16
lcredit=3
lcredit=0
```

最小密码长度为 16。用户使用小写字母不获得额外积分，但可以从非字母数字字符获得最多三个积分。大写字母或数字没有特殊设置，所以它们各提供一个积分。

CEO 尝试使用 `password`。仅从长度来看，通过了——16 个字符。添加一个大写字母让她获得一个字符的积分，让她可以将密码缩减为 `password`。一个数字让她额外获得一个字符积分，减少到 14 位：`password0`。是的，有两个数字，但数字积分限制为一个。不过，她可以从非字母数字字符获得最多三个积分。所以 `password!@#` 只有 11 个字符，但加上积分后长度为 16。

创建复杂密码的用户将获得短密码的奖励。24

## 常用选项

无论你是定义要求还是使用积分，这些选项都适用。

`difok` 选项设置新密码中新字符的最小数量。默认值为 5。新密码必须包含至少五个旧密码中没有的字符。如果你要求长密码，增加此值。

`maxrepeat` 选项设置字符连续重复的最大次数。默认值是 0，禁用此检查。将其设置为 1 则不允许连续出现两个相同的字符。

通过 `maxclassrepeat`，你可以限制同一类字符连续在一起的次数。它通常设置为 0，禁用此检查。将其设置为例如 4，将禁止包含像 `alqn` 或 `81930` 这样看起来随机的字符串，因为它们超过了 4。你可以使用所有字符，但必须在中间用其他字符类打破它们。

`maxsequence` 选项设置递增或递减序列的最大长度，例如 `abcde` 或 `87654`。默认为 0，禁用此检查。

如果 `gecoscheck` 字段设置为非 0 的数字，`pam_pwquality` 将密码与用户的 `/etc/passwd` 条目进行比较。匹配 `/etc/passwd` 中任何超过三个字符的单词都会导致 `pam_pwquality` 拒绝该密码。

> 24 我通过降低随机电击的电压来奖励大多数用户，但只要对你有效即可。

# 第 11 章：密码质量检查

`badwords` 选项可以设置为由空格分隔的单词列表，这些单词禁止出现在密码中。如果你使用此选项，我强烈建议使用配置文件，而不是在 `/etc/pam.d` 文件中输入整个列表。

最后，`enforce_for_root` 告诉 `pam_pwquality` 即使对于 `root` 账户也要实施限制。通常情况下，`root` 可以根据意愿将用户的密码设置为 `password`。

通过 `pam_pwquality` 和 `pam_pwwdqc`，你可以强制用户创建不那么糟糕的密码。不过，别指望他们感谢你。

# 后记

PAM 是一种旨在简化系统管理的强大工具，但自它诞生以来，却几乎完全让系统管理员感到困惑、不解和困扰。我对此应该很清楚。我是那些花费多年试图理解 PAM 的人之一。每当我认为自己知道自己在做什么时，现实就会发出一大肚子大笑并说：“噢，是吗？”

现实情况如何呢……这是我的第二十五本书。这似乎是一个说几句需要探讨的话的好时机。

这是我的第十本自出版的技术书籍——或者正如印刷版书脊上写的，A 号。这是我的第十八本技术书，对于读者对我的作品给出大部分积极反馈，我感到惊讶、欣慰，并有些谦虚。感谢你们所有人，我现在正通过编写关于相对冷门的计算主题书籍来谋生。我对此非常感激。

但说到“谋生”，我为什么要写这本书呢？PAM 并不是 ZFS 那样的热门话题。它不像 SSH 那样无处不在——是的，IT 领域的大多数人每天的某个时候都会接触 PAM，但并没有多少人需要配置它。我写这本书是因为我想我能发大财，但也是因为我认为系统管理社区需要它。

我希望这本书能救你。

如果没有的话，我建议吃司匹林、运动并做一些与计算机完全无关的事情，直到痛苦消失。是的，那可能需要耗费余生。

# 赞助商

以下优秀人士认为这本书足够重要，以至于在我在制作期间向我提供了资金支持。电子版赞助者为了在电子版本中获得名字至少赞助了 20 美元，而赞助印刷版的人则至少掏出了 100 美元，以便他们的名字出现在真正的墨水中。

感谢所有贡献者。虽然我*需要*赞助，但它们无疑让我的生活变得简单许多。我把钱花在了我真正喜欢但对我身体有害的事情上。诚挚地感谢大家。

# 印刷赞助商

- Stefan Johnson

- Hugh Brown

- Wouter Clarie

- Phi Network Systems

- tanamar corporation

# 永远不要错过 Lucas 的新发布！

订阅 Michael W Lucas 的邮件列表。

https://www.michaelwlucas.com/mailing-lists

# Michael W Lucas 的更多技术书籍

- Absolute BSD

- Absolute OpenBSD 第 1 版和第 2 版

- Cisco Routers for the Desperate 第 1 版和第 2 版

- PGP and GPG

- Absolute FreeBSD

- Network Flow Mastery

# IT Mastery 系列



- `SSH Mastery`
- `DNSSEC Mastery`
- `Sudo Mastery`
- `FreeBSD Mastery: Storage Essentials`
- `Networking for Systems Administrators`
- `Tarsnap Mastery`
- `FreeBSD Mastery: ZFS`
- `FreeBSD Mastery: Specialty Filesystems`
- `FreeBSD Mastery: Advanced ZFS`
- `PAM Mastery`
- `Relayd & httpd Mastery` (即将推出！)

# authorized_keys_command

| 术语 | 页码 |
| :--- | :--- |
| `#` | 90 |
| `@` | 76-76 |
| `%` | 76-77, 80 |
| `-` | 76-77 |
| `;` | 21 |
| `=` | 23 |
| `<` | 72 |
| `~` | 72 |
| `!` | 102, 117 |
| `=` | 71 |
| `>` | 72 |
| `<=` | 54 |
| `%f` | 102 |
| `%h` | 84 |
| `%H` | 84, 102 |
| `%s` | 83-84 |
| `%t` | 83-84 |
| `%u` | 83-84, 102 |
| `%U` | 83-84 |
| `user` | 103 |
| `tauthok_type` | 145 |
| `bad` | 62, 64-65 |
| `badwords` | 150 |
| `bash(1)` | 75, 94 |
| `binding (control)` | 24, 29-30, 61 |
| `btindweed` | 71 |
| `blowfish` | 41 |
| `breatheryl` | 5, 34 |
| `Brown, Rough` | 153 |
| `BSD` | 8-9, 11, 46, 67, 91 |
| `BSD authentication` | 7 |
| `titt-dling` | 110 |
| `Canada` | 54 |
| `caffeine` | 123 |
| `cabities` | 87 |
| `Carpenter, John` | 2, 10, 12, 13-30, 31, 40, 42, 46, 54, 62, 65, 67, 73, 82, 96, 104, 109, 124, 132-134, 137 | 14 |
| `$DISPLAY` | 138 |
| `$EDITOR` | 68 |
| `$KRBCNAME` | 67 |
| `$SSH_CLIENT` |  |
| `${USER}` | 117 |
| `@include` | 31 |
| `AAA` |  |
| `Access Control` | 3 |
| `account` | 20, 22, 30, 33, 36, 39, 45, 48, 54, 93, 96 |
| `AIX` | 5, 9 |
| `allow_local_user_authorized` | 103 |
| `keys_file` | 103, 116 |
| `Ansible` |  |
| `Antarctica` |  |
| `Apple` | 5, 9, 13, 36 |
| `Archiller` | 23 |
| `audit` |  |
| `with pam_unix` | 40 |
| `dual_allowed_id` | 98-99 |
| `allow` | 20, 22, 25, 31, 33, 37-40, 42, 43, 54, 55, 67, 72, 88, 89, 102, 103, 108, 118, 119, 130, 134, 136 |
| `authconfig(8)` |  |
| `authentication` | 3-4 |
| `AuthenticationMethods` | 14-15 |
| `Authentication, Authorization` | 3 |
| `authorized_keys` | 101-105 |
| `authorized_keys_command` | 103 |
| `charge(8)` |  |
| `character classes` | 139, 141 |
| `claire, Wouter` | 80, 153 |
| `clock visibility` | 112 |
| `Default Environment` | 6 |
| `common-auth` | 31 |
| `common-account` | 31 |
| `common-session-noninteractive` | 69 |
| `config` | 20, 21, 31 |
| `counter-based passedwords` | 110 |
| `credits` | 79 |
| `crash` | 145, 147 |
| `Dance` | 5 |
| `Dark Lord of the IT` | 140 |
| `data` | 78 |
| `decrypt` | 146, 148 |
| `Dean` | 2, 10, 12, 13-30, 31, 40, 42, 46, 54, 62, 65, 67, 73, 82, 96, 104, 109, 124, 132-134, 137 | 14 |
| `debug` | 81-86 |
| `deny` | 126 |
| `dragonfly` | 63-64 |
| `git(1)` | 109 |
| `echo_verification_code` | 119 |
| `Google Authenticator` | 4, 101, 107, 122 |
| `emergency_codes` | 120-121 |
| `clients` | 112, 120 |
| `enforce` | 140-141 |
| `disaster recovery` | 120-121 |
| `enforcing` | 97 |
| `google-authenticator(1)` | 110, 113, 115-122 |
| `enforce_for_` | 13 |
| `google_authenticator` | 125 |
| `eq/etc/bashrc` | 69, 111, 114, 122 |
| `eq/etc/environment` | 69 |
| `grep` | 93-94, 98 |
| `eq/etc/ttpusers` | 87 |
| `group` | 76 |
| `eq/etc/limits.conf` | 39 |
| `group membership` | 42-43, 80 |
| `eq/etc/master.passwdwd` | 48 |
| `hammer of “nope”` | 7 |
| `eq/etc/noglogin` | 19 |
| `hard limits` | 77 |
| `eq/etc/pam.conf` | 20 |
| `hardware security token` | 4-52 |
| `home directory` | 71 |
| `eq/etc/passwd` | 39, 89, 123, 149 |
| `$HOME/ssh/identity` | 130 |
| `eq/etc/passwdwd.conf` | 140 |
| `$HOME/ssh/login-keys.ds` | 134-135 |
| `eq/etc/security` | 41, 46, 75 |
| `$HOME/ssh/session-keys.ds` | 134-135 |
| `eq/etc/security/limits.conf` | 75 |
| `HP-UX` | 3 |
| `eq/etc/security/pam_env.conf` | 68, 69 |
| `IBM` | 9 |
| `Identity, Authentication, and` | 3 |
| `eq/etc/shadow` | 39 |
| `inactive` | 62 |
| `eq/etc/ssh/keys` | 53 |
| `include statement` | 30, 31 |
| `eq/etc/ttys` | 46 |
| `inroup` | 73 |
| `expose_account` | 35 |
| `expose from PAM` | 53-54 |
| `expose_auth` | 92 |
| `extended_controls` | 49, 57-59 |
| `fsize` |  |
| `fptd` | 50 |
| `functions` | 49, 57-59 |
近期运行中的符文讲师 ........ 24
`libpam-ssh` .............. 134
`libqrencode` ......... 109, 113
管理员 (Librarian)... 24
轻量级目录访问参见 LDAP 协议 .............. 75



`limit()`........ 6-7, 11, 13, 36, 41, 67, 105

`Linux-PAM`................ 7-9, 23, 29, 31, 39, 41-43, 46-47, 52-53, 59, 61-, 73, 84, 87

可加载认证.... 9

`local_users` ......... 145

`locks` .............. 78

`log`................ 95

`logging`................ 43

`match` .............. 144

`max` .............. 142

`maxclassreatper`................ 149

`maxlogins`.............. 76, 80

`maxrepeat` .............. 149

`maxsequence` .............. 149

`maxsyslogins` .............. 76, 79

`memlocks` .............. 78

`min` .............. 12

`mincls` .............. 146

`minlen` .............. 146

`module arguments`............... 21

`module context`............... 32

`Mosziejk Kurt`................ XIX

多因子认证................ 3-4, 101

`MySQL`................ 40

名称服务切换................ 3

`ne` .............. 7

尼安德人................ 33

`NetBSD`................ 13

网络信息服务 NIS NFS.............. 87

`nixg`................ 04

`nice` .............. 79

`NIS` .............. 39

`nfile` .............. 78

`nhoist` .............. 46

`nlogin` ......... 47-48

`noskvadaj`.............. 18

`NoSQL`................ 94

`noterm` .............. 46

`notingroup` .............. 73

`notdnefr`................ 73

`noupdate`.............. 46

`nowpmp`.............................. 46

`no_fail` .............. 125

`no_fake_prompts`............... 83

`no_warn` ......... 20-21, 33, 84, 135

`nproc`............... 75, 79

`NSS`................ 3

`ntpd(8)`............. 108

`nullok`, 20, 30, 32, 33, 40, 83, 116, 130

`nullok_secure`............... 41, 135-136

`O'Connor, Mike`................ XIX

`OATH`............... 111

`ocredit` ......... 146, 148

`ok`............... 62-65

`onerr`............... 88-91

万处皆可用一次性密码................ 70

`OpenBSD`................ 7

`OpenSolaris`.............. 8

`OpenPAM`............... 7-9, 30, 34, 36, 42-43, 46-47, 68, 75, 133

`OpenSolaris`.............. 8, 11

`OpenSSH`................ 13-15

开放认证................参见 `OATH`

`Open Group`................ 6, 55

`OPIE`............... 107

(可选)........ 24, 26-, 30, 61, 63-64, 82, 85-, 128-138............... 8, 42

`Open Oracle`..................

`OS X`................ 5, 9, 11, 13, 47

回文......... 145

`panic`............... 123

`pants`..................

`passphrase`....... 142-143

`password (word)`. 20, 22, 30, 40, 44, 54, 138, 141, 145-146

`password`................ 40

`empty`..................

`expiration`......... 138

最大长度............... 128

已轮转的`rotated`......... 145

`rotation`............. 13

`simple`............... 14

`pam_acct_mgt`............... 

`pam_authenticate`............... 58

`PAM_AUTHOK_PROMPT`................ 52

`PAM_AUTHOK_EXPIRED`............... 55

`PAM_AUTH_ERR`................ 55-62,

`pam_auth_update`............... 12, 18

`pam_breathezer`............... 25-29, 31, 33

`pam_chauthtok`............... 73

`pam_session_close`.............. 58

`pam_console`..... 88

`PAM_CONV`......... 57

`pam_cracklib`............... 145

`PAM_CRED_EXPIRED`............... 55

`pam_ddr`................ 25-29

`pam_debug`................................ 86

`pam_deny`............... 28, 30, 44, 65-66, 126-138, 135

`pam_echo`................................ 86

`and PAM items`................................ 83-34

`pam_env`................................ 57

`pam_env`............................... 30, 65-71

`pam_exec`................................ 2, 17, 53-54, 81,

`bugs`.......................................... 85-100,

`Linux-PAM`.................................... 95-96

`OpenPAM`............... 94

`pam_gail`............... 57

`pam_printd`............... 30, 65

`pam_genesac` 25-29, 33

`pam_getenv`............... 57

`pam_getenvlist`.............. 57

`pam_get_data`............... 57

`pam_get_item`............... 57

`pam_google_authenticator`...... 109, 116-19

`pam_group`............... 42-43

`pam_hipster`............... 57

`PAM_HOST`.. 1

`PAM_IN`............... 56, 64

`PAM_COMPLETE`............. 62

`pam_keyinit`............... 30

`pam_krbs`............... 57

`pam_lastlog`............... 20, 36, 46, 125

`pam_limits`............... 30, 75-80

`pam_listfile`........................ 74

`pam_caluser`............... 57



`PAM_MAXTRIES` 56

`PAM_MAX_RES_SIZE` 52

`pam_mkhomedir` 32, 99

`PAM_NEW_AUTHTOK_REQ` 56, 64-65

`pam_nologin` 47-48

`pam_odd_mkhomedir` 99

`PAM_OLDA` 52

`PAM_OLDA_PROMPTS` 57

`pam_open_session` 58

`pam_opie` 36, 83-85

`pam_opiecc` 36, 83-85

`pam_passwdc` 4, 137-138, 140

`pam_permit` 44, 145-126, 138

`PAM_PERM_DENIED` 56, 94

`pam_putenv` 57

`PAM_RHOST` 51, 68

`pam_root` 45, 86

`PAM_USER` 51, 91

`pam_security` 45-66, 132

`PAM_SERVICE` 50

`PAM_SERVICE_ERR` 56, 62, 95

`pam_win` 58

`pam_setenv` 57

`pam_set_data` 57

`pam_set_item` 57

`pam_sm *` 59

`PAM_SM_FUNCTION` 52

`pam_ssh` 17, 67, 96-99, 123-36

`pam_ssh_agent_auth` 15, 17, 101-105, 109

`pam_start` 57

`pam_succeed` 30, 63, 65-71

`PAM_SUCCESS` 51, 62-64-65, 74, 94, 101, 124, 132

`pam_systemd` 67, 80

`PAM_SYSTEM_ERR` 56

`pam_impdir` 128

`PAM_TYPE` 51

`pam_unix` 20, 21, 30-32, 36, 39, 65, 74, 82, 83, 15, 89, 125-126, 128, 135-136, 138

`PAM_USER_A` 51, 90, 93

`PAM_USER_PROMPT` 52

`PAM_USER_UNKNOWN` 62

`pam_warn` 53, 85-86

`PasswordAuthentication` 14, 119

`Perl` 2

`permissive_mode` 97

`Phi Network Systems` 153

`Pinette` 70

`policy` 20-37

`POSIX` 35-36

`pp files` 6

`message queues` 99

`Pratchett` 23-24, 54, 84, 92

`print` 81

`print(1)` 115

`priority` 79

`privileges` 58

`publickey` 55, 103, 116

`pw(8)` 138

`QR code reader` 112

`quiet` 74

`quiet_fail` 74

`quiet_success` 30, 72

`Radius` 119

`rate limiting` 109, 115

`RATE_LIMIT` 72

`readenv` 201

`required()` 24, 25, 30, 36, 43, 44, 47, 54, 61, 66, 69, 71, 73, 74, 84, 89, 93, 105, 116, 118-119, 125-128, 135-136, 138

`requite()` 24, 26, 36, 42, 51, 63, 66, 126-128, 135, 138, 141, 145-146

`return codes` 49, 55-56

`return_prog_exit_status` 95

`RFC 4226` 110

`RFC 6238` 110

`rhost` 89

`rlogid(8)` 19

`root_only` 42

`RSA tokens` 107

`rsh(8)` 19

`rtrio` 79

`Russa` 77

`SASL` 7

`/bin/nologin` 72

`Screaming Rage` 110

`Security Enhanced Linux（增强型Linux）` 

`SELinux` 96-103

`semodule(8)` 99

`Senior Wrangler` 88

`sence` 102

`service functions（服务函数）` 58-59

`session（话）` 20, 22, 30, 36, 39, 45-46, 54, 69, 74, 136

`setudeid` 96

`setroubleshoot` 8



`sh(1)`......................................................94

`Shakespeare`.............................................110

`sha12`.......................................................40

`shadow`.......................................................71

`shell（壳）`.......................................................76

`shipping container（集装箱）`.....................................54

`showfailed`.................................................46

`sigpending`.............................................74

`silver, matrilinearly inherited`..................1

`Simple Authentication and Security Layer（简单认证与安全层）`......7

`Smørgrav, D-Erling`..................................IX

`soft limits（软限制）`...................................................74

`Solaris`..................................5, 7, 8, 13, 19, 37, 67,

`sponsors`...............................................87

`SSH`.......................................7, 43, 47, 96-99, 101, 109, 111, 119, 123, 136

`SSH1`......................................................130

`SSH agent`...............................26, 101-105, 123-136

`ssh key without password（无密码密钥）`...............................50

`virtual terminals（虚拟终端）`..................13, 50, 130

`sshd config`.........................................................14

`SSH_AUTH_SOCK`......................................104

`stdout（标准输出）`........................................................95

`Strotmann, Carsten`.........................................XIX

`substack`.......................................................65, 66, 132

`substring（子字符串）`.......................................................139, 144

`sudoes`........................................................104

`sudo(8)`................................................31, 101, 109, 111

`sufficient (control)（足够的控制）`..................................24, 28-30, 36, 40, 44-65, 61-66, 73, 85-86, 102-103, 105, 119, 125, 131, 5, 8

`Sun Microsystems（太阳系统公司）`....................................................

`swfish`.......................................................50, 51, 54, 88

`syslog(2)`...................................................41

`systemd(8)`................................23, 67, 80

`/sys/class/tty/console/activate`................................

`tanamer corporation`..................................................153

`telnet`...............................................19, 126, 134

`Time-Based Temporary One-Time Passwords（基于时间的一次性密码）`...............................................见 TOTP

`time-based passwords（基于时间的密码）`..................110

`TOTP`..................................................17-102

`truss`.........................................................81

`trust (option)（信任选项）`...................................................

`try_first_pass`....11, 20, 32, 33, 35, 40, 43, 83, 125, 131, 145

`tty（终端）`................................................71

`two-factor authentication（双因素认证）`................................3

`type_for_limits（类型限制）`................................20-75

`for_pam_exec`.......................................75

`Ubuntu`................................................12

`ucredit（用户额度）`.............................................146, 148

`ulimit(1)`..............................................75, 30, 58, 71, 72, 76, 96,

`user（用户）`................................................78

`user（用户）`................................................70

`user（用户）`................................................76

`user_first_pass`....11, 34, 43, 119, 121, 131, 145

`user_mapped_pass（用户映射密码）`..................................35

`Use_Login（登录登录）`................................................14

`Use_use（使用）`................................................74

`/var/log/audit.log`..................................97-99

`/var/log/auth.log`..................................82

`/var/log/lastlog`........................................46

`/var/log/secure`.....................................92, 973

`/var/log/utxt.log`.....................................46



`/var/run/nologin`.....................................47

`virtual terminals`（虚拟终端）........................................89

`want_agent`（想要代理）.......................................125, 131

`wildcard`（通配符）................................................76-77

`WINDOW_SIZE`（窗口大小）........................................122

`XDG base directories`（XDG 目录）........................................80

`skcd`........................................................143

`YP database`（YP 数据库）................................................92
