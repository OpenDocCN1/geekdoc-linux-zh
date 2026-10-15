
# Linux 服务器安全：攻击与防御

## 关于作者

`Chris Binnie`是一位技术顾问，从事 Linux 系统工作已近二十年。在职业生涯中，他曾在云端和银行领域部署过许多服务器，并多年来一直构建自主网络。他曾为《Linux 杂志》撰稿。在工作之余，Chris 喜欢户外活动、观看利物浦队的比赛并赞美美德。

## 关于技术编辑

`Rob Shimonski` (`www.shimonski.com`) 是一位经验企业家，也是商业社区的活跃参与者。他是一位畅销书作者和编辑，在出版和发行杂志及期刊方面拥有多年经验。`Rob` 在协议捕获和分析以及 `Windows` 和 `Unix` 系统工程方面拥有深厚的专家级经验。

## 致谢

- 项目编辑：`Ada Obi Tulton`
- 业务经理：`Amy Knies`
- 技术编辑：`Rob Shimonski`
- 执行编辑：`Jim Minatel`
- 制作编辑：`Dassi Zeidel`
- 封面协调：`Brent Savage`
- 文字编辑：`Marylouise Wiack`
- 校对：`Kathy Pope, New York`
- 制作经理：`Katie Wisor`
- 索引：`Johnna VanHoose Dinse`
- 内容开发与装帧经理：`Mary Beth Wakefield`
- 封面设计：`Wiley`
- 封面图片：© `Getty Images, Inc.`
- 专业技术策略总监：`Barry Pruett`

总结 ............................................................................................ 97

# 前言

毫无疑问，有效保护系统和网络安全所需的知识需要不断保持更新。然而，并非所有技术人员都想成为全职的安全专家；相反，他们更倾向于关注其他领域，尽管他们的角色要求许多所需的技能。

# 引言

熟练的攻击者可以利用其他受损系统和服务的力量，给毫无防备的受害者带来巨大的困扰。

此外，尝试攻击的动机是多样的，有时也难以预测。它们可能包括获得黑客社区的认可、在受害者面前胜过一筹、作为新手菜手的训练练习，或者仅仅是为了获取利益。而且，考虑到其中最常见的人群，我们也不要忘记那些追求刺激的人。

如果你的服务容易受到某些类型的非愿关注，例如你的 `Web` 应用程序不断受到寻找安全漏洞的探测轰炸，那么常识告诉我们，你应该重点关注让你的开发者修复应用程序的缺陷。相反，如果你运行的是电子邮件服务，那么你绝对需要确保部署在集群中所有邮件服务器上的软件都是最新的，并且频繁且及时地打补丁。通过关注最显性的弱点，可以限制你可能向熟练攻击者展示的攻击面，并减少他们在你的其他基础设施中立足的机会。一旦你确认主要的攻击向量已得到基本安全，你就可以专注于堵住那些不那么明显的漏洞。

通过几个简单的问题来理清对安全的思考可能会有所帮助。首先，你试图保护什么？例如，是隐藏在受多个防火墙和主机保护的数据库中的敏感秘密信息，还是你在保护一个必须全年每天 24 小时对用户可用的在线服务？这个问题很重要，因为它影响了你如何加强防御，并可能改变你做出的防御选择。例如，你可能每月支付几美元购买网络流量清洗服务来防免受拒绝服务攻击的影响，而不是购买昂贵的高端硬件。

其次，你将如何控制安全泄露？如果网络上的某台服务器或设备被攻破，是否会自动导致其他主机遭受同样的命运？如果是这样，显然你的安全策略存在需要解决严重问题。

第三，你将如何从安全泄露中恢复？你可能还会担心如果攻击者发现了你的冗余机制，以及你的故障转移服务将在哪个阶段激活。如果你不知道攻击者最初是如何破解安全的，那么重建主服务器或盲目恢复网络服务可能毫无意义。你是否能够使用替代供应商的设备或软件快速恢复服务？如果是这样，你可能会减少相同攻击再次渗透你的安全防护的概率，允许你在调查攻击者如何进入的同时，恢复部分（甚至全部）服务。

# 本书的结构

书中包含的章节可以按任何顺序阅读，它们是作者多年来作为互联网用户在旅程中感兴趣的安全主题合集。

这些主题从过去、现在和未来攻击的理论，到对各种在线攻击的缓解和防御，一直到赋予读者亲自执行恶意攻击的能力（希望他们能学会防御此类攻击）。

通过将各种主题分为不同的章节，在将来可以引用并返回这些主题，以便读者详细地回顾内容。每章的内容如下：

-   `第 1 章：隐身斗篷：` 如果攻击者看不到你的服务器，并且不知道它的存在，那么从根源上说没有任何可以利用的攻击向量。我们将演示如何在不受攻击者欢迎关注的情况下继续使用生产环境的服务。

-   `第 2 章：为你的文件创建数字指纹：` 有许多方法可以监控服务器文件系统的完整性，以确保攻击者没有获得访问。在本章中，我们将查看手动方法和检查根基程序（`rootkits`）的自动工具。

-   `第 3 章：21 世纪的 Netcat：` 现代版本的 `Netcat` 历史悠久，具有许多先进功能，成为黑客的首选工具。学习当此类工具被用于你的服务器时如何进行欺骗，此外还学习如何利用其行业领先的功能。

-   `第 4 章：拒绝服务：` 这种深陷历史的现代版 `Netcat` 因其众多高级功能已成为黑客的首选工具。只有最大的互联网基础设施提供商才能承受拒绝服务攻击的破坏。在本章中，我们将详细讨论导致整个国家互联网连接中断的话题。

-   `第 5 章：Nping：` 知道主机运行哪些服务只是战斗的一半。这种强大的工具允许你检查任何主机，并使用独特的载荷构造数据包进行伪造。

-   `第 6 章：日志侦察：` 尽管针对你的服务器执行的某些探测看似无害，但毫无疑问了解它们如何运作有助于进一步保护你的服务器。我们将检查侦察的几个方面。

-   `第 7 章：Nmap 的 NSE：` 许多用户会使用 `Nmap` 进行简单的端口扫描，但很少有人知道它包含了利用远程机器的能力。我们将探索 `Nmap` 自带的许多脚本。

-   `第 8 章：恶意软件检测：` 一种多年来以非法安装软件形式困扰 `Windows` 系统的定时威胁。恶意软件对系统造成的损害从烦人的弹出窗口到整个银行账户被入侵不等。在本章中，我们将学习如何在 `Linux` 上部署复杂的反恶意软件解决方案。

-   `第 9 章：使用 Hashcat 破解密码：` 技术专业人员可能会惊讶地发现，一种密码破解工具几乎可以破解哈希值。这意味着如果获取了你的密码，攻击者看到你的明文密码只是时间问题。本章将一步步引导你完成过程。

-   `第 10 章：SQL 注入攻击：` 在一项著名的调查中，`SQL` 注入攻击被列为最常见的攻击。尽管这种攻击类型可以追溯到 90 年代，但仍大量攻击通过编程实践利用了属于企业和关键在线服务的网站。本章提供实用的历史信息，以及如何识别和利用在线服务的步骤说明。

# 谁应该读这本书

这本书是为中级管理员、软件黑客和其他 `IT` 专业人员编写的。然而，我们希望这种写作方式能让任何好奇的人都能快速判断哪些章节适用于对安全感兴趣但不一定熟悉 `Linux` 命令行的人。目标是，某些读者可能会进一步研究特定章节的主题，以增强在该主题方面的知识，而其他领域对他们的需求可能较小，并可能在以后用于参考。

换句话说，每个章节对经验水平的要求没有区别，尽管那些侧重于命令行的章节对于新手来说可能需要付出更多努力。

## 总结

让我们希望通过增加对黑客工具和心态的理解，并跟进最新的安全动态，你不会遭受一种显而易见的现实：你不再拥有自己的系统或网络的控制权，而是别人在控制。

## 第一章

## 隐身衣

想象一下，你可以从互联网上隐藏一个服务器，但仍然可以使用你互联网服务提供商（`ISP`）的高速带宽。在不进行任何更改的情况下，你就可以安全地将其作为文件仓库或其他许多用途。

你还可以将其安全地用于许多事情。在不进行任何更改的情况下，你就可以通过命令行来启动或停止任何你想要的服务。你的选择是简短运行这些服务然后关闭它们，还是让它们对外部世界运行一段时间。

这可以通过“端口敲门”（`port knocking`）技术来实现。你可以通过关闭所有网络端口来伪装你的服务器，使其变得隐形。这种单个端口的“端口敲门”可以用于 `SSH` 服务或其他服务。在本章中，你将看到如何通过某些选项创建一个隐形服务器。

## 背景

通过隐藏服务器在互联网上的存在，在最好你可以让它私密运行；最坏的情况下，如果它的存在已知，你可以通过限制开放端口来减少攻击面。

## 探测端口

在开始之前，让我们仔细看看服务器上的网络端口。如果你用过像 `Nmap` 这样的安全工具，可能已经熟悉当端口显示为关闭（`closed`）时，实际上它们并没有运行的原理。`Nmap` 区分了端口是否有后台守护进程（`daemon`）在监听。如果 `Nmap` 指向的端口没有后台守护进程但显示为开放（`open`），则意味着防火墙阻止了访问。`Nmap` 报告的这些状态包括：未过滤（`unfiltered`）、已过滤（`filtered`）和关闭（`closed`）。关于这些状态的更多信息，请访问 `https://nmap.org/port-scanning-basics`。

# 第一章：隐身衣

## 混淆端口扫描器



现在你已经知道了端口是如何呈现扫描器的，让我们来看看如何混淆返回的响应以迷惑复杂的端口扫描技术。最明显的工具选择是基于内核的防火墙 `Netfilter`，通常被称为 `iptables`。其工作原理如下：对于 `TCP` 数据包，你想要使用 `iptables` 来操纵对端口探测的响应，以生成 `REJECT` 请求。对于其他协议，你想要丢弃数据包。这种方式，当你收到 `Nmap` 的已过滤（`filtered`）响应时，根据我从大多数网上收集到的信息（这个论点是有争议的且可以改变），关闭（`closed`）端口是你可以希望的最佳响应。这是因为你并没有通过防火墙拦截任何端口，或者端口仅仅是因为后台运行着守护进程而开放。

进一步解释一下，正常情况下，无法到达的端口会生成 `ICMP` 端口不可达（`Port Unreachable`）响应。你不希望生成这些错误，因为那意味着服务器在那个端口上监听，并且会暴露你服务器的响应。你想要生成的调整后的 `REJECT` 响应如下：`--reject-with tcp-reset`。这有助于在端口未被且关闭时做出响应。你只需将此片段添加到每个 `iptables` 规则的末尾：

```
-j REJECT --reject-with tcp-reset
```

通过这种技术，你可以确保不会泄露关于系统的不必要信息。在选项中，你没有泄露关于系统的不必要信息。这是因为你并没有通过防火墙拦截任何端口。

## 安装

在 `Debian` 衍生系统中，你这样安装：

```
apt-get install knockd
```

在 `Red Hat` 衍生系统中，你通过这样安装：

```
yum install knockd
```

安装 `knockd` 后，如果你想获得有关该包的更多背景信息，`Debian Jessie` 有一个简短的 `README` 文件，可以在 `/usr/share/doc/knockd/README` 找到。这个非常有用的 `README` 文件讨论了 `knockd` 如何工作等内容。它使用了一个名为 `libcap` 的库，其他几个包也使用了它，如 `tcpdump`、`ngrep` 和 `iftop`（捕捉数据包进行检查）。得于其巧妙的设计，`knockd` 甚至不需要绑定到它正在巧妙监听的端口，即可监控原始流量。

## 修改文件系统位置

连接、断开或错误等事件会直接记录在系统的 `syslog` 中，并可能写入 `/var/log/messages` 或 `/var/log/syslog` 文件。如果你不希望这些信息被埋在其他系统日志活动中，或者不想费力解析笨肿的日志文件，你可以创建自己的自定义日志文件。我倾向于这样做，这样调试会清晰得多，我可能会使用自动化工具或自定义 `shell` 每天给自己发邮件，以便监控可疑事件。因为我将所有的 `knockd` 实例放在一个地方，信息对于脚本和其他工具来说更容易解析。

```
[options]
LogFile = /var/log/portknocking.log
```

更改日志文件的位置是一个常见的解决方案，但你也可以更改 `knockd` 服务启动时写入进程 `ID`（`PID`）文件的位置。你可以在配置文件的 `[options]` 部分更改位置，如下：

```
[options]
PidFile = /var/tmp/run/file
```

## 一些配置选项

现在你已经更好地了解了主配置文件的设置，可以检查如何根据你的需求对其进行配置。在许多其他任务中，你将考虑到某些操作的超时在设置服务器时起着作用。

## 启动服务

如果你看到显示 `knockd` 已禁用的错误信息，请不要报警。这是一项预防措施，以确保在你完成设置之前，`knockd` 不会对 `iptables` 引入不希望的更改。

在 `Debian` 上，该错误信息要求你在文件 `/etc/default/knockd` 中将以下参数更改为 `1`：

```
START_KNOCKD=1
```

显然，你只有在双击配置或确保你的带外访问（`out-of-band access`）按预期工作后才会这样做。

## 更改默认网络接口

一旦配置了首选端口序列，你可能想要调整其他参数。在配置文件 `/etc/default/knockd` 中，你有机会更改 `KNOCKD_OPTS` 设置。文件中的示例被注释掉了，这意味着你可以如下所示更改 `knockd` 监听的网络接口：

```
KNOCKD_OPTS="-i eth1"
```

这些选项将附加到 `knockd` 服务中，你需要重启服务以使更改生效，如下（在 `systemd` 机器上）：

```
systemctl restart knockd
```

## 数据包类型与计时

在 `/etc/knockd.conf` 文件中，你可以更改一些设置来精调客户端连接到你的方式。参考列表 1.1，在 `[openSSH]` 部分下，你将添加如下选项：

```
[openSSH]
tcpflags = syn
```

## 第1章：隐身斗

```
seq_timeout = 10
cmd_timeout = 15
```

`tcpflags` 选项意味着你可以预期 `knockd` 发送特定类型的 `TCP` 数据包。在这种情况下，它是 `TCP` `"SYN"`。你可以使用的 `TCP` 标志包括 `fin`、`syn`、`rst`、`psh`、`ack`、`urg`。如果没有收到指定的 `TCP` 数据包，`knockd` 将简单地忽略这些数据包。意识到这种忽略机制通常有效。正常情况下，一个错误的数据包会破坏整个敲门序列的工作，这意味着客户端必须重新开始才能连接。你可以使用逗号分隔多个 `TCP` 数据包类型，并且似乎新版本的 `knockd`（根据更新日志从 `0.5` 版本开始）使用感叹号来否定数据包类型，例如 `lock`。

回到示例中的其他选项。你可能注意到列表 1.1 中默认存在 `seq_timeout`。然而，由于你增加了序列设置中的端口数量，你将 `seq_timeout` 值从 `5` 增加到了 `10`。这是因为可能会出现连接缓慢的情况，例如在智能手机上。

示例中的最后一个选项是 `cmd_timeout`。此选项适用于 `knockd` 收到成功敲门后发生的情况。事件顺序如下：首先，一旦敲门被确认为有效，`knockd` 将运行 `start_command`（如果需要提醒请参考列表 1.1）。如果存在此设置，那么 `knockd` 执行了 `start_command`，它将在等待 `cmd_timeout` 指定的时间后运行 `stop_command` 操作。

这是打开 `SSH` 服务器访问的首选方式，然后在连接建立后立即关闭。你继续会话不应该遇到任何问题，但新连接需要再次运行敲门序列。将此操作视为在你进入后在身后关上门。你的服务器将变得不可见，只有你请求的流量是可见的。

## 测试你的安装

由于你正在处理服务器的安全性，你应该运行几次测试以确保 `knockd` 按照预期工作。理想情况下，你有另一台客户端机器来运行一些测试。为了完全确定 `knockd` 正确打开并关闭端口，我喜欢通过从不同的 `IP` 地址进行连接来测试。如果你无法访问不同 `IP` 地址的连接，你可能定期断开互联网连接，以便你的 `ISP` 分配一个新的动态 `IP` 地址进行测试。某些宽带提供商重启后这样做，你的移动运营商也可能这样做。

## 敲门客户端

你可以使用不同的客户端创建敲门序列以初始化连接并打开你的 `SSH` 端口。你甚至可以手动使用 `Nmap`、`netcat` 和 `Telnet` 等工具按顺序探测所需的端口。文档还提到，如果可用，可以使用 `hping`、`sendip` 和 `packit` 软件包。让我们看看 `knockd` 软件包带的 `knock` 命令示例。

如果你使用了列表 1.1 显示的 `openSSH` 部分，将用以下语法设置你的简单 `knock` 命令：

```
# knock [options] <host> <port [:proto]> <port [:proto]> <port [:proto]>
```

列表 1.1 中配置的 `TCP` 端口如下，你可以如下运行 `knock` 命令：

```
# knock 11.11.11.11 6:tcp 1450:tcp 8156:tcp 22045:tcp 23501:tcp 24691:tcp
```

目标 `IP` 地址为 `11.11.11.11`，你可以如下运行 `knock` 命令：

```
# knock 11.11.11.11 6:tcp 1450:tcp 8156:tcp 22045:tcp 23501:tcp 24691:tcp
```

目标 `IP` 地址为 `11.11.11.11`，你可以如下运行 `knock` 命令：

```
# knock 11.11.11.11 6:tcp 1450:tcp 8156:tcp 22045:tcp 23501:tcp 24691:tcp
```

目标 `IP` 地址为 `11.11.11.11`，你可以如下运行 `knock` 命令：

```
# knock 11.11.11.11 6:tcp 1450:tcp 8156:tcp 22045:tcp 23501:tcp 24691:tcp
```

目标 `IP` 地址为 `11.11.11.11`，你可以如下运行 `knock` 命令：


目标 IP 地址为 `11.11.11.11`，你可以如下运行 `knock` 命令：

```
# knock 11.11.11.11 6:tcp 1450:tcp 8156:tcp 22045:tcp 23501:tcp 24691:tcp
```

## 让你的服务器不可见

一旦你确定你的安装工作正常，就可以对其锁定。

拥有带外访问服务器的权限以防万一。通过以下方式阻止所有进入服务器的流量：

```
# iptables -A INPUT -j DROP
```

运行以下命令检查你的 `iptables` 规则，你将看到任何关于 `22` 端口的提及：

```
# iptables -nvL
```

然而，一旦你设置了 `cmd_timeout` 值，你将会看到规则。

如果你在此阶段遇到问题，请继续阅读以排查你的配置并增加日志级别。否则，服务器将是不可见的，如图 1.1 所示。

`nmap` 认为该 IP 地址上没有机器。![](img/0de912db8d0576072b15feaa_22.png)

## 保存 iptables 规则

为了确保 `iptables` 规则在重启后依然有效，在 Debian 衍生版中你应该安装 `iptables-persistent` 软件包：

```
# apt-get install iptables-persistent
```

然后使用如下命令保存你的规则：

```
# /etc/init.d/iptables-persistent save
```

或者，你可以通过此命令还原配置：

```
# /etc/init.d/iptables-persistent reload
```

在 Red Hat 衍生版上（在系统机器上），你可以使用此命令：

```
# /sbin/service iptables save
```

并运行此命令来恢复规则：

```
# /sbin/service iptables reload
```

## 第 1 章：隐身术

为了让上述功能在 systemd Red Hat 衍生版上工作，你可以尝试先安装软件包：

```
# yum install iptables-services
```

## 进一步考虑

还有其他几个端口敲方面可能对你有帮助。让我们现在来看这些：

### 手机客户端

在我的安卓 手机上，我首选的 SSH 应用是 JuiceSSH (https://juicessh.com)。它有一个插件允许你将端口敲序列配置为 SSH 握手的一部分。这意味着即使你出门没有电脑，也没有理由不使用端口敲。

## 故障排除

如果你在端口敲日志文件中运行命令 `-f logfile.log`，你将看到写入日志的各种阶段。这包括有效端口是否被敲击，重要的是它是否按正确的顺序被敲击。

调试选项也给了你增加 `knockd` 生成日志级别的机会。如果你仔细打开 `/etc/init.d/knockd` 文件并寻找 `OPTIONS` 行，你可以在该行的任何现有值上添加大写字符 D (Shift+d)，如下：

```
OPTIONS="d -D"
```

一旦你诊断并解决了问题，应该关闭额外的日志，以防止磁盘空间被必要的占用。如果你好奇，`-d` 意味着以守护进程方式运行 `knockd`。正常运行时应保持原样。

回到客户端一会儿。你可以通过添加 `-v` 选项来增加“`knock`”客户端生成的输出的详细程度。结合调试选项，这将从连接的客户端和服务器端为你提供有用的反馈。

### 安全考虑

当涉及服务器相关的公共信息时，请记住 ISP 不应该发布你用于服务器的 IP 地址的反向 DNS 信息。你的 IP 地址应该看起来是未使用且未分配的，这样它才是不可见的。

## 第 1 章：隐身术

即使在像 HTTP 等公共服务上，你也需要记住混淆正在使用的守护进程版本。在世界上流行的 Web 服务器 Apache 中，实现此点的常用方法是将 "ServerTokens" 更改为 "Prod"，并将 "ServerSignature" 设置为 "Off"。这些几乎不是尖端的配置更改，可能意味着当发现新的零日漏洞时，攻击会忽略你的服务器，因为你的 Apache 版本不在它的攻击数据库中。

另一个需要考虑的方面在 `knockd` 文档中讨论。它提到如果你使用 `-l` 或 `--lookup` 服务为你的日志条目解析主机名，那么可能会存在安全风险。如果你这样做，某些信息可能会泄露给攻击者。如果可以捕获你服务器的 DNS 流量，攻击者可能确定序列的第一个端口。

## 临时序列

使用不同的方法来敲击序列如何？也可以使用预定义的端口序列列表进行敲击，这些序列在使用一次后就会过期。回到列表 1.1 和你的主配置文件，你可以在打开和关闭部分中添加此内容以启用一次性序列：

```
One_Time_Sequences = /usr/local/etc/portknocking_codes
```

如果你删除了列表 1.1 中的序列行并将其替换为此代码，那么 `knockd` 将从路径指定的文件获取其序列。

`knockd` 处理一次性序列的方式很寻常。它从该文件中读取下一个可用序列，并在通过有效敲击成功连接后将该行注释掉。它只是在前面添加一个井号或井字符。

## 第 2 章：为你的文件创建数字指纹



你可能会惊讶，你几乎一直用于其他用途的东西其实可以很容易地作为安全助手。

介绍`md5`命令。在过去下载Unix类型文件时，你可能遇到过一个选项，让你通过验证这些文件的`MD5sums`来检查可能下载文件的完整性。例如，`MD5sums`通常出现在你用来下载Linux ISO文件的网站上。

如图 2.1 所示，当你从这个镜像站下载 Debian Jessie 时，面对的是以下界面：`http://ftp.debian.org/debian/dists/jjie/installer-amd64/images/`

图 2.1

你可以从该网站下载 Debian Jessie，并同时检查`MD5sums`以确保安全。

| 文件名 | 时间 | 大小 |
|---|---|---|
| `MANIFEST` | 00 05:29-16 | 1709 |
| `MANIFEST` | 00 23 07-05 | 46432 |
| `MD5SUMS` | 00 23:07-05 | 5315 |
| `SHA256SUMS` | 00 23:07-05 | 72131 |
| `udeb list` | 00 23:07-05 | 6537 |

如果你打开`MD5SUMS`，你就能看到图 2.1 的内容，其中包含了每个文件的哈希值。

### 列表 2.1 `MD5SUMS` 文件的缩略示例

```
bf0228f49751bfa8758ea3acafa106f /.hd-media/boot/img.gz
eeefacaf04b1076443cf8845cacdb1d /.hd-media/gtk/initrd.gz
19fd4fe4eb5c5eae49441b826db1b371 /.hd-media/gtk/vmlinuz
4dc2f49eb4b47feeae835527cc79a /.hd-media/initrd.gz
19fd4fe4eb5c5eae49441b826db1b371 /.hd-media/vmlinuz
2750ac5f78d08659389d3c16e379f /.netboot/debian-installer/amd64/boot-screens/adt.cfg
aca8744ba5a2716b53260286a40bb /.netboot/debian-installer/amd64/boot-screens/exitlog.cfg
2e883b65f4747ae56ae1b3460e101 /.netboot/debian-installer/amd64/boot-screens/f1.txt
e62b25d4b5cd30f0c44af3db503646 /.netboot/debian-installer/amd64/boot-screens/f10.txt
```

在列表 2.1 中，你可以看到每个文件的`MD5sum`以及右侧对应的文件名。这是为了防止他人将恶意文件替换掉合法文件，从而可能感染你干净的操作系统（OS）安装。

`MD5sums`首先计算，然后与`MD5`数字值进行比对。你可能会（以一种相对高级的方式）认为，检查`MD5sums`实际上是为每个文件创建了一个可以查询的数字指纹。

你可以很容易地尝试自己使用`MD5sums`（`md5sum`命令已包含在我机器的`couretails`软件包中，在几乎所有的发行版中都应该可以直接可用）。尝试运行类似下面的命令：

```
# md5sum /home/chrisinnie/debbie-and-ian.pdf
```

你收到的响应可能是这样的：

```
3f19f37d00f83c8ad16775293e7376 debbie-and-ian.pdf
```

回到你 Linux 发行版的文件。将`MD5sums`文件下载到与 ISO 文件相同的目录下（如果你好奇，ISO 是以 ISO 9660 文件系统命名的）。这样做，你可以省去手动检查正在使用的安装介质文件的麻烦。该文件包含了该目录下所有文件的`MD5sums`。现在你已经有了所有文件的`MD5sums`，可以使用以下命令检查它们的有效性（`-c`也代表`--check`）：

```
# md5sum -c MD5SUMS
```

列表 2.2 显示了运行`-c`选项后的结果。你可能会说`MD5sums`是二元的：结果要么是 OK 或者不是。

### 列表 2.2 使用 `-c` 选项检查我的 `MD5sums` 文件的输出示例

```
compare.png: OK
config2.png: OK
config3.png: OK
config4.png: OK
works_1.tar: OK
package_inst.jpg: OK
```

如果文件与其原始`MD5sum`不匹配，你应该注意什么？在列表 2.3 中，你可以看到警报在响了（带有警告）。

### 列表 2.3 警报在响

```
test.sh: FAILED
bootstrap: FAILED
hash.png: FAILED
```

## 第 2 章：为文件创建数字指纹

在 Debian 衍生版上：

```
# apt-get install rkhunter
```

在 Red Hat 衍生版上：

```
# yum install rkhunter
```

假设你的安装没有出现任何错误，你可以运行几个简单的命令来开始。以下命令将填充有关你机器上文件的文件属性数据库：

```
# rkhunter-propupd
```

接下来，为了扫描任何正在安装的新软件并在软件更新后触发扫描，你应该在文件`/etc/default/rkhunter`中将`APT_AUTOGEN`选项设置为`yes`。我只在带有`Apt`软件包管理器的 Debian 上验证过此选项；Red Hat 衍生版上可能会有不同的选项。

完成该更改后，你现在准备好首次运行`RootKit Hunter`了：

```
# rkhunter-check
```

请注意，版本或发行版之间存在细微差异，如果出现错误，请尝试添加`-c`或`--checkall`。

你也可以使用以下命令定期更新`rkhunter`威胁列表；如果你想跟踪最新威胁，可以创建一个特定的`cron`任务：

```
# /usr/local/bin/rkhunter-update
```

图 2.2 显示了运行此命令后生成的简略输出。输出详细列出了软件进行的初始检查。

如你所见，`RootKit Hunter`正在关注可执行文件的关键目录（在本例中为`/usr/sbin`）。这些正是二进制文件（在许多其他类型之外）最易被 rootkit 感染的。

想一下希腊人和特洛伊木马的寓言。除了立即感染二进制文件的 rootkit 之外，代码可以保持休眠一段时间，直到被合法用户执行或按计划执行。随后，系统就会被攻破。

### 图 2.2

运行`rkhunter--checkall`的输出简略显示

```
[ Rootkit Hunter version 1.4.2 ]
Checking system commands...
Performing 'strings' command checks
Checking 'strings' command
Performing 'shell binaries' checks
Checking for prohibited variables
Checking LD_LIBRARY_PATH variable
Performing file properties checks
Checking for prerequisites
/usr/bin/admadm
/usr/bin/chroot
/usr/bin/groupadd
/usr/bin/groupmod
/usr/bin/getent
/usr/bin/getpr
/usr/bin/login
/usr/bin/rsyslogd
/usr/bin/tcp
/usr/bin/useradd
/usr/bin/userdel
```

```
[ OK ]
[ None Found ]
[ None Found ]
[ Not Found ]
[ OK ]
[ OK ]
[ OK ]
[ OK ]
[ OK ]
[ OK ]
[ OK ]
[ OK ]
```

## 配置

要配置`Rootkit Hunter`文件，你可以编辑它的长配置文件，位于`/etc/rkhunter.conf`。

要接收关于机器完整性的夜间报告，你只需要编辑两个配置参数：定义接收者的电子邮件地址，如果标准的`mail`命令在你的系统中默认无法工作，则可以对第二个进行调整。

进入配置文件后，找到这些行，取消注释并根据你的需求进行调整：

```
#MAIL-ON-WARNING=me@mydomain root@mydomain
#MAIL_CMD=mail -s "[rkhunter] Warnings found for ${HOST_NAME}"
```

第一行在取消注释后，指定了报告发送到哪里（多个地址可以用空格隔开）。第二行处理邮件命令以及发送到这些地址的电子邮件报告的主题。



只需重新运行`rkhunter--check`软件来测试这些更改是否正常生效，并检查你的电子邮件收件箱。

检查帮助生成报告的`cron`任务，你可以查看`/etc/cron.daily/rkhunter`文件。在许多发行版中，`cron.daily`通常会在每天早上0100到0500之间运行。

如果你想更改邮件查看，可以在`cron.daily`文件中搜索以下行：

```bash
if [ -s "OUTFILE" -n "$REPORT_EMAIL" ]; then
  echo "Subject: [rkhunter] $(hostname -f)-Daily report"
  echo "To: $REPORT_EMAIL"
```

在修改此文件之前，创建一个副本可能是明智的。回到我从`RootKit Hunter`运行的结果。在图2.3中，你可以看到`RootKit Hunter`搜索的一些`rootkit`。

# 图 2.3

`RootKit Hunter`搜索的某些`rootkit`部分列表

| Checking for rootkits... | |
| :--- | :--- |
| Performing check of known rootkit files and directories | [ Not Found ] |
| Trojan Variant | [ Not Found ] |
| worm | [ Not Found ] |
| Ajk Rootkit | [ Not Found ] |
| Adors Rootkit | [ Not Found ] |
| afka | [ Not Found ] |
| Apache Worm | [ Not Found ] |
| Ambient (root) | [ Not Found ] |
| Balaur Rootkit | [ Not Found ] |
| Beastie Rootkit | [ Not Found ] |
| bk2 Rootkit | [ Not Found ] |
| B00 Rootkit | [ Not Found ] |
| cb Rootkit | [ Not Found ] |
| CISK (Sapper variant) | [ Not Found ] |
| Danny's Abuse Kit | [ Not Found ] |
| Devil Rootkit | [ Not Found ] |
| Dica Rootkit | [ Not Found ] |
| Dragon Rootkit | [ Not Found ] |
| Duamark Rootkit | [ Not Found ] |
| Enguix | [ Not Found ] |

如你在图2.3和2.4所示，`RootKit Hunter`检查了许多方面；检查非常全面。

# 图 2.4

另一个`rootkit`搜索的示例

| Performing additional checks | |
| :--- | :--- |
| Rootkit additional checks | OK |
| Checking for possible rootkit files and directories | [ None Found ] |
| Checking for possible rootkit strings | [ None Found ] |
| Performing malware checks | |
| Checking system processes for suspicious files | [ None Found ] |
| Checking for login backdoor | [ None Found ] |
| Checking for hidden directories | [ None Found ] |
| Checking for suffix logs | [ None Found ] |
| Suspicious Shared Memory segments | |
| Performing trojan specific checks | OK |
| Checking for Apache backdoor | [ Not Found ] |
| Performing Linux specific checks | |
| Checking kernel modules | OK |
| Checking kernel module names | OK |

# 误报

如果你收到任何误报，可以在配置文件`/etc/rkhunter.conf`中将它们加入白名单。

如果误报量太大是个问题，可以通过取消取消主文件中匹配整个目录的配置行来解决：

```
ALLOWHIDDENDIR=/dev/.initramfs
```

如果`RootKit Hunter`错误地怀疑你的某个二进制文件被脚本替换，可以使用此选项移除警告：

```
SCRIPTWHITELIST="/usr/bin/lsof"
```

对于单独的文件，你也可以使用此配置：

```
ALLOWDEVFILE="/dev/.udev.rules.99-root.rules"
```

记住，任何隐藏文件或目录（以点开头的名称）对于文件扫描器来说几乎总是可疑的。在图2.5中，你可以看到`RootKit Hunter`结果的另一个部分。

的是`RootKit Hunter`进行的全面检查是经过仔细考虑的。除了文件系统和进程表，它还会检查网络异常，如图2.6所示。

# 图 2.5

`RootKit Hunter`扫描的一部分涉及`/dev`分区以及隐藏文件和目录。

| Performing filesystem checks | |
| :--- | :--- |
| Checking /dev for suspicious file types | [ None Found ] |
| Checking for hidden files and directories | [ None Found ] |

# 图 2.6

可靠的`RootKit Hunter`还会进行许多网络检查。

| Checking the network... | |
| :--- | :--- |
| Performing checks on the network ports | [ None Found ] |
| Checking for backdoor ports | [ None Found ] |
| Checking for hidden ports | |
| Performing checks on the network Interfaces | |
| Checking for promiscuous interfaces | |
| Checking the local host... | |
| Performing system boot checks | Found |
| Checking for local host name | Found |
| Checking for startup files | |
| Checking system startup files for malware | [ None Found ] |
| Performing group and account checks | |
| Checking for password file | Found |
| Checking for non-equivalent (UID 0) accounts | [ None Found ] |
| Checking for passwordies | [ None Found ] |
| Checking for file changes | [ None Found ] |
| Checking for group file changes | OK |
| Checking post account shell history files | |
| Performing system configuration file checks | |
| Checking for an SSH configuration file | Found |
| Checking if SSH root is allowed | [ Not allowed ] |
| Checking if SSH protocol is allowed | [ Not allowed ] |
| Checking for a running system daemon | Found |

## 设计良好



Rootkit Hunter 的开发者将其描述为一种“基于主机的、被动的、事后的、基于路径的工具”。如果你在想，“被动”指的是你手动调度软件或手动运行它。“基于路径”的描述意味着它只处理文件，而不像病毒检查器那样进行启发式操作。

在 `rkhunter` 附带的文档底部有一个我非常喜欢的章节。对于任何网络安全初学者或需要复习知识的老用户来说，这都是一个编写得非常良好的入门指南。

## 第二章：为文件建立数字指纹

文档首先指出，在尝试攻击之前，总是会有某种形式的侦察，因此你应该密切关注日志文件。我记得曾经写过一个脚本，监控我一台服务器上的追踪路由（`traceroutes`）和 `ICMP` 流量。

再次重复我之前的观点，手册后面提到该工具并不是增强机器安全性的替代品。不要将其视为替代品，而应将其视为识别问题的工具。

有趣的是，`Rootkit Hunter` 的文档还向你推荐了他们的竞争对手之一——优秀的 `chkrootkit` 工具，它是一个旧版本。手册建议，在同一类工具中仅使用一种工具有时不足以获取你所需的所有信息。因此，为了完整性，你应该从同时运行 `chkrootkit` 和 `rkhunter` 的重叠中获益。这是一个适用于所有安全层面的良好观点。

最后，手册讨论了如果你发现系统被入侵且没有足够的技能来处理成功的漏洞利用该怎么办。除了 `www.cert.org` 外，你可能还想访问 `www.linuxsecurity.com/br/INFO/intruder_detection_checklist.html`，它提供了一份关于如何应对在线攻击的步骤清单。

那些具有攻击经验的人告诉我们，你应该考虑当局可以报告该漏洞，并尽快提交报告——而不是等几周或几个月——以防可以采取措施防止其他入侵。一如既往，常识是通用的。

## 总结

现在你已经拥有了对文件系统上的文件建立数字指纹的能力。因此，你可以快速比较之前的 `MD5sums` 以查看文件是否被更改过，还可以每晚或定期运行 `Rootkit Hunter`。`rootkit` 检查器的好处在于，它们还可以通过计划性扫描指出你所犯的配置错误，从而带给你安全感。你希望可以在错误导致进一步更严重的安全问题之前纠正它。

根据我所涵盖的内容，有两条规则你应该记住：

- 始终将记录的 `MD5sums`（或任何其他哈希值）保存在安全的地方（加密并受密码保护），并远离服务器。

- 不要依赖 `rootkit` 工具来减少事件发生后的工作；只需用它们来识别问题。从那里开始，在重建机器之前，先弄清楚是如何发生入侵的。花费大量时间重建机器，结果稍后同样的安全漏洞再次被利用，是没有意义的。听到这种情况发生得如此频繁，你可能会感到震惊。

在运行不太关键的服务时，只要有一定的远见，连接到互联网的机器防护通常不涉及太多工作。即使不可避免地会引入一些耗时的开销，例如在对系统更改添加夜间报告时。通过在构建机器之初采取预防措施，互联网上的黑客就可以被挡在外面，让你能够静心工作。

## 二十一世纪的 Netcat

第一个让我惊叹其功能之强大的 Linux 软件包之一是功能强大的 `netcat` ([https://nmap.org/ncat/])。多年来它出现了几个版本，每个版本的功能集都略有不同。如果你还没用过它，你将大开眼界了。它被描述为系统管理员可能需要的唯一工具，这可能有点乐观，但 `netcat` 确实是非同凡响的。

首先，它极其轻量化，文件系统占用空间微乎其微。此外，许多发行版默认都包含一个版本的 `netcat`。在你探索了一些背景知识之后，你将看到如何利用它来为自己获益。

### 历史

多年来，`netcat` 有许多实现版本。原始的 Unix/Linux 版本编写于 1995 年，1998 年由于其流行，出现了一个 Windows 版本。我曾读到过，由 `Nmap` 项目 ([https://nmap.org]) 进行的一项调查显示，在使用他们的开源安全工具 `Nmap` 之后，用户选择 `netcat` 作为第二备选工具。

`Netcat` 的功能也助推了它在犯罪分子中的流行。除了善意的白帽攻击外，它经常被用于攻击侦察以及攻击本身。因此，你可能在企业级基础设施上找不到全功能的 `netcat` 版本，因为安全担忧以及该软件包被标记为威胁。

我将尝试解释一下 `netcat` 的来源。混淆很容易发生，因为原始的 `netcat`（其可执行二进制文件为 `nc`）被 `Nmap` 项目重构，他们将其称为“二十一世纪的 Netcat”。重构的结果是一个名为 `ncat` 的二进制文件。`ncat` 的帮助页通过以下注释充分承认了原始版本：

> 原始的 `netcat` 由 "Hobbit"（`hobbit@avian.org`）编写。虽然 `Ncat` 并不是基于“传统” `netcat`（或任何其他实现）的代码构建的，但 `Ncat` 在精神和功能上大多基于 `Netcat`。

这个版本的 `netcat` (`ncat`) 自我描述（主要是）是用于“连接和重定向套接字”，但对其功能的描述被夸大了。

例如，在红帽企业 Linux (`RHEL`) 7 中提供了 `netcat` 版本，在 `Debian` 中也是如此，原始 `netcat`（名为 `nc`）在多个版本中可用。这两个“nc”版本的 `netcat` 值得注意的是，在两个版本之间使用相同的命令行选项可能会遇到困难。

### 安装包

为了清晰起见，`Debian` 和 `Ubuntu` 使用表 3.1 所示的包名。在 Red Hat 派生系统中，你可以尝试此包作为版本的 `nc`：

```bash
# yum install netcat
```

对于 `Nmap` 项目的 `ncat`，你可能尝试此包：

```bash
# yum install nmap-ncat
```

我怀疑安装一个包然后确保你阅读的是该包正确的页面（以防同一台机器上安装了两个版本的 `netcat`）将证明是成功的。

#### 表 3.1 `Debian` 和 `Ubuntu` 包名

| 包名 | 描述 |
| --- | --- |
| `netcat` | 一个用于兼容的“虚拟”包，可以安全地删除 |
| `netcat-openbsd` | 支持 `IPv6`、代理和套接字的 `OpenBSD` 版本 |
| `netcat-traditional` | 原始包，缺少 `netcat-openbsd` 中包含的许多功能 |
| `netcat-ipv6` | 原始 `netcat` 的重写，具有 `IPv6` 支持并增强了对 `UDP` 的支持 |
| `nmap` | 如果你想在 `Debian`/`Ubuntu` 上使用 `ncat`，则需要此包。 |

为了避免混淆，我将关注 `ncat`（`nc` 命令）而不是 `netcat`（`nc` 命令）。从现在起，我将交替使用 `ncat` 和 `netcat`——当然，在需要清晰时使用 `ncat`。

### 入门

让我们看看 21 世纪的 `netcat` 替代品（我指的是 `ncat`）能为你做什么，从一些基础知识开始。它包含了强大的功能，可以通过命令行操纵网络数据（数据的读取和写入）。它非常可靠，并且同时适用于 `TCP` 和 `UDP`（它也适用于 `IPv6`）。它可以在 `SSL`（安全套接字层）连接方面完成令人印象深刻的事情，并能与代理良好配合——包括 `SOCKS4` 和 `HTTP` 类型。

考虑到其中涉及的优秀编程实践，`ncat` 的质量也非常高。文档特别指出，它不仅使用了完全重写的代码（没有借用原始版本），还采用了 `Nmap` 经过实战检验的库。有了 `HTTP`，我将开始使用 `netcat` 作为 Web 浏览器。如果你输入此命令，加上你想要访问的任意网站，你就能连接到 `TCP 80` 端口：

```bash
# ncat -C www.google.com 80
```

一旦你输入此命令并按下回车键，你就需要输入以下内容，然后按两次回车：

```http
GET / 
```

请注意，如果你动作不够快，命令将超时，你必须重试。如果你以前在命令行中查询过 `HTML`，你可能会对执行后在屏幕上滚动的过量信息感到惊讶。如果你感兴趣，`-C` 选项会加入回车和换行符（`CRLF`），以便与某些网络协议兼容。

你也可以将 `netcat` 用作监听的守护进程。入侵服务器有许多方法，而保持访问开放的一种方法是让 `netcat` 监听在一个一个系统管理员可能没有察觉的冷门端口。你稍后会考虑这一点，但现在先关注 `HTTP`。`netcat` 文档提供了一个极佳的示例，说明了如何将你简单的 `netcat` 二进制文件变成基础 Web 服务器。首先，你将创建一个简单文件。你不会使用 `.html` 扩展名，因为你的文件不是纯 `HTML`；相反，它将是 `HTTP` 会话的一半。你将用列表 3.1 所示的内容命名你的 `index.http`。

#### 列表 3.1 保存在文件中的 `HTTP` 会话的一半

```http
HTTP/1.0 200 OK

<HTML>
<BODY>
Nothing to see here, move along.
</BODY>
</HTML>
```

如列表 3.1 所示，运行此命令后，你将看到 `netcat` 监听 `HTML` 内容。接下来，`netcat` 会显示客户端的请求：

```bash
# ncat -C 127.0.0.1 80 < index.http
```

## 第 3 章：21 世纪的 Netcat



然而，文档指出这种场景下的一个问题。问题在于 `Neymar` 无法向 `Lionel` 回话。正如你对功能强大的 `netcat` 所预期的那样，这里有一个通办法。当我看到这个例子时，我立刻想到了部署用于恶意目的的利用程序（稍后你就会知道为什么了）。现在看下面这些命令：

```
Neymar # ncat -l 1234 > newlog.log
Luis # ncat -l 1234 --sh-exec ncat Neymar 1234
Lionel # ncat --send-exec Luis 1234 < logfile.log
```

在我看来，这个例子中可怕的选项是 `Luis` 在接收数据时启动了新的 shell 命令。想象一下使用这种选项（启动任何命令）会造成什么样的损害。在这个例子中，`Luis` 接收到一个连接，他产生了一个新的 `netcat` 实例，并处理了 `Lionel` 和 `Neymar` 通信的所有输入和输出。这非常复杂。

这里文档中的一个端口转发示例，再次处理 `HTTP`，通过执行 shell 命令来转发流量：

```
# ncat -l localhost 80 --sh-exec "ncat www.chrisbinnie.tld 8100"
```

你只需要将发往本地机器 `TCP` 端口 `800` 的数据转发到位于 `TCP` 端口 `6100` 的另一个主机即可。

## 安全通信

我之前提到了 `SSL` 以及 `netcat` 如何与加密流量交互，尽管这是一个值得考虑的担忧可能性。我将从 `netcat` 如何加密其自身的流量的示例开始本节。你使用 `-C` 选项（有时称为连接模式）：

```
# ncat -C --ssl ssl.chrisbinnie.tld 443
```

在这里，你假设你信任的机器 `ssl.chrisbinnie.tld` 在 `TCP` 端口 `443` 上运行着 `SSL` 服务器，并且你可以连接到它。惊讶的是，对于使用证书进行身份验证的 `SSL` 服务器，强大的 `netcat` 非常有用。

你只需要在命令中使用 `--ssl-cert` 和 `--ssl-key` 选项将 `netcat` 指向你的 `PEM` 证书和私钥文件。如果你愿意，可以将这两个选项指向同一个文件。

在交换证书以及加密通信时，一个重要因素是确认（通过第三方服务的认可印章）`SSL` 服务器的身份是否有效。`Netcat` 能够通过此命令处理此类请求：

```
# ncat -C --ssl-verify ssl.chrisbinnie.tld 443
```

根据文档，`netcat` 能够按照如下方式检查 `SSL` 证书：

验证是使用 `Ncat` 附带的 `ca-bundle.crt` 证书包以及操作系统提供的任何信任证书完成的。如果你想验证到服务器的连接，其证书不是由默认认证机构之一签名，请使用 `ssl-trustfile` 指定一个包含你证书的文件。该文件必须是 `PEM` 格式。

```
https://map.org/ncat/guide/ncat-ssl.html
```

文档继续提供了 `SSL` 命令的正确语法，如下：

```bash
# ncat -C --ssl-verify --trustfile <custom-certs.pem> <server> 443
```

现在你已经确认了连接的是哪台机器，让我们看看 `netcat` 可用的另一个 `SSL` 功能。正如你在探索时将看到的，它有许多功能。

此功能被称为具有“解包”（unwrap）`SSL` 的能力。文档建议，如果你尝试从启用 `SSL` 的邮件服务器收集电子邮件，但你的邮件客户端不具备 `SSL` 能力，那么 `netcat` 可以提供帮助。

你首先将上述 `netcat` 客户端指向你的 `localhost`、你的本地机器或 `IP` 地址 `127.0.0.1`。当 `netcat` 在本地监听 `TCP` 端口 `143`（通常用于未加密的 `IMAP` 通信的端口）时，你可以将流量转发到你的邮件服务器 `TCP` 端口 `993`：

```
# ncat -l localhost 143 --sh-exec "ncat --ssl mail.chrisbinnie.tld 993"
```

你可以将此方法用于涉及两个主机的任何协议，例如 `HTTP`，涉及多个主机时效果可能不佳。

`Netcat` 甚至可以作为 `SSL` 服务器。你需要提供一个证书，与之前的例子相反，它可能由访问的客户端进行验证。

在不指定证书文件和私钥的情况下——并使用相同的选项（`--ssl-cert` 和 `--ssl-key`）——`netcat` 会自动为你生成它们。你可以使用 `-l` 选项（或其等效的 `-listen`）启动 `netcat`：

```
# ncat -v --listen --ssl
```

如图 `3.1` 所示，适配的 `netcat` 生成了一个临时密钥，让你更更容易开始。

图 `3.1`

`Netcat` 自动生成一个临时的 `SSL` 证书。

# 第 3 章：二十一世纪的 Netcat

另一个实用的技巧是，你也可以最多添加三个字母 `v`，其中 `-vvv` 在你的命令输出结果时提供最详细的输出信息（verbosity）。

与你之前使用 `netcat` 发送 `SMTP` 指令一样，强大的 `netcat` 也能发送 `Telnet` 指令。因此，如果你发现自己没有 `Telnet` 客户端的权限，那么 `netcat` 也可以提供帮助。使用 `netcat` 代替 `Telnet` 有几个显而易见的优点。首先，`netcat` 更加“安静”，除非你连接的机器发送了数据，否则它不会输出数据。它还有一些预留字符，这意味着如果你使用 `Telnet`，某些二进制数据将会损坏。此外，你可能已经注意到 `Telnet` 会在静默（空闲）连接上退出并停止运行，这可能意味着你将无法接收到整个会话的数据。`Telnet` 命令对 `UDP` 的支持也并不理想，但正如你所知道的，`netcat` 一定可以。

## 总结

在本章中，我只涵盖了 `netcat` 潜力的极小部分；其范围实在太广，无法完全介绍。

希望你理解，了解该工具的一些功能至关重要，因为这可以揭示更多关于攻击者如何对你发动攻击的信息。下次我在局域网（`LAN`）内部移动文件时，对于简单任务，依赖像 `SFTP` 这样更笨重的数据传输工具太容易了。你应该避免使用 `Telnet` 命令调试端口和连接，而始终使用 `netcat`。在我的情况下。

## 第 4 章：拒绝服务

在 `www.team-cymru.org/templates.html` 提供了一个非常受欢迎的 `NTP` 服务器模板，你可以使用它来帮助你的公网服务器避免成为此类攻击的一部分。访问该页面并点击“Secure NTP Template”（安全 `NTP` 模板）链接，你将看到针对各种平台的模板集合：`Cisco IOS`、`Juniper Nino` 和 `Unix`。

此外，关于如何配置 `IPTables` 来锁定 `NTP` 的有用提醒如下：

```
# iptables -A INPUT -s 0 -d 0 -p udp --source-port 123 -m state --state ESTABLISHED -j ACCEPT
# iptables -A OUTPUT -s 0 -d 0 -p udp --destination-port 123:123 -m state --state NEW, ESTABLISHED -j ACCEPT
```

此外，还有一条有趣的说明，如果你恐慌并决定在路由器级别阻止 `NTP` 流量进入你的网络，这可能会产生潜在的破坏性影响。只有在你完全清楚自己在做什么时，才应对 `NTP` 流量过滤 `UDP` 端口 `123`，否则关键服务将不可避免地失败。

## 攻击报告

当第一次 `NTP` 攻击发生时，云服务提供商 `CloudFlare` 宣布了记录在内的此类最大 `DDoS` 攻击。根据 `CloudFlare` 的数据，该攻击流量短于 `400 Gbps`，仅需近 `4,529` 台服务器就能跨越 `1,298` 个不同的网络产生如此大量的饱和带宽的流量。相比之下，一次广为报道的针对 `Spamhaus`（反垃圾邮件服务提供商）的攻击据报道使用了 `39,056` 个开放 `DNS` 解析器生成了 `300 Gb` 的 `DDoS` 攻击。如你所见，在单机器的影响上存在显著差异。

另一种在 `DDoS` 攻击中日益使用的协议是由 `PSINET` 在 `1988` 年创建的，`PSINET` 在被各种合并和收购吸收之前是全球 `ISP` 之一（如果不是最大的话）。

简单简单网络管理协议（`SNMP`）用于绝大多数工作设备，如交换机和路由器。这个实用的协议有助于向任何能够接收它的软件提供统计信息（如带宽使用情况）。最重要的是，启用 `SNMP` 实际上会产生一个名为“public”的团体字符串的攻击向量。即使默认配置了密码，它们也往往是简单的，例如“private”。这意味着你的宽带路由器构成了潜在风险，并可能参与 `DDoS` 攻击。还要考虑属于企业或 `ISP` 的启用 `SNMP` 的设备；单个网段上可能有几十台接入高容量带宽的强大交换机和路由器。顺便提一下，办公室里的打印机通常也与工作站和 `IP` 摄像头一起使用 `SNMP` 实现。

据，攻击者利用 `SNMP` 进行大规模反射/放大攻击。流量比例高达 `1700:1`。这一估计的准确性仍待观察，且是否存在某种恐慌成分。



2014 年 5 月，`Akamai` 的 `DDoS` 部门报告他们发现了 14 次 `SNMP` 攻击。其中不到一半在美国，约有 18% 在中国。

## 防止 SNMP 反射

在快速检查你的 `/etc/services` 文件后，你可以看到 `SNMP` 使用的默认端口的细节：

```
snmp                161/tcp                # Simple Net Mgmt Proto
snmp                161/udp                # Simple Net Mgmt Proto
snptrap             162/tcp                # SNMPTRAP
snmptrap            162/udp                snmp-trap # Traps for SNMP
```

为了防止源自你网络的 `SNMP` 流量反射，你可以遵循“默认拒绝”的原则，确保你的边界防火墙不允许此类流量流出局域网（`LAN`）并进入互联网。当然，这也适用于进入你局域网的流量。通常在匆忙设置、升级或配置设备时，默认设置往往保持不变。如果你不完全清楚自己在做什么，就应对 `NTP` 流量过滤 `UDP` 端口 123，否则关键服务将不可避免地失败。令人担忧的是，由于配置不当，宽带路由器可能会参与 `DDoS` 攻击。

![](img/0de12db8d05f76077b5b15f73eaa_53_0.png)

## DNS 解析器

在 2014 年年初，另一种攻击浮出水面。这种攻击是否真的是为了反射攻击而设计的，仍有争议，我在这里讨论它以增加你的知识，`Google` 提供。

通过捕获这些流量，你可以监控其流量以及 `DNS` 查询是否可能是合法的。

- `8.8.8.8`
- `8.8.4.4`

如果发现了不受欢迎的流量，你可能希望通过引入防火墙规则来限制那些影响你局域网的设备。防火墙为设备提供了外部访问。

白帽与其他安全专业人员的讨论表明，这些显然源自 `Google` IP 地址的攻击实际上是为了利用并击败（使用预配置为设备服务器的 IP 地址）。换句话说，攻击者可能会重新配置设备以用于非法目的，而不是拒绝其服务。

为了进一步阅读，请考虑一种攻击向量以及尝试绕过合法 `BGP` 公告（边界网关协议是连接互联网许多网络的路由协议）的 `Google DNS` 解析器；你可以在这里 `http://thehackers.com/2014/03/google-public-dns-server-traffic.html` 了解更多。

## 共谋

有一份关于限制离开你网络的伪造流量的建议。遗憾的是，经验告诉我们，无论是由于无能还是资源匮乏，总会有部分比例的网络管理员未能意识到遵循此类指南的重要性，或者他们根本没有精力关注。当然，不要忘记那些为了犯罪活动而故意留下漏洞的少数管理员。

一份较早的文档写于 2000 年，旨在引发辩论并帮助对互联网运行感兴趣的人。最佳当前实践 38 (`BCP 38`); `https://tools.ietf.org/html/bcp38`，该文档为网络管理员提供了受欢迎的建议。在其他组织中，它鼓励企业和学术机构应当加强其主机和网络设备等网络基础设施各个方面，以防止互联网周围产生连锁反应。

具体来说，我们需要花时间讨论入站过滤（ingress filtering）的重要性，如果你的网络被用作攻击工具，它可以保护外部网络免受损害。引用这一点，通过采用简单的预防措施，对来自“有效”源的攻击进行诊断和缓解，比猜测源流量的来源更为有效，正如你在之前的章节“`NTP` 反射攻击”中看到的那样。

在许多情况下，不同层次的入站过滤可以实现这一目标。所提出的观察之一是，通过减少互联网攻击的数量和频率，最终在攻击发生时会有可用资源。因此，响应将更加有效。这些开创性指南的大部分内容归功于资深的 `NANOG`（北美网络运营者小组：`https://www.nanog.org`），他们在一个流行的邮件列表中详尽地激烈讨论网络问题。

# 让一个国家瘫痪

多个地理位置分散的系统针对单一系统（例如网络或自治系统，无论其规模有多大）并使其离线的威胁，长期以来一直是企业、`ISP`（互联网服务供应商）甚至整个国家的担忧。`DDoS` 攻击可能从 20 世纪 90 年代就开始了。

2007 年有广泛报道，波罗的海国家爱沙尼亚的 `DDoS` 攻击，结合街头骚乱，几乎让政府瘫痪。显然，民众反对爱沙尼亚议会移除一座著名的战争纪念碑。加之高程度的社会动荡，这成为了转折点。来自 `DDoS` 的攻击流量不断增加，并在长时间内以持续的方式被接收。新闻机构对连接的缺失感到沮丧，因为这意味着世界其他地区无法随着国内事件的发展保持最新动态。

爱沙尼亚的 `DDoS` 攻击不断演变，据报道一度达到每秒四百万个数据包的攻击流量。这部分针对该国最大的银行，根据某些报告，它最终成功地让该银行断了网。根据国家统计数据，约 97% 的人口进行在线银行业务，这意味着该国的银行系统发生了致命性故障。如果影响还不够严重，互联网连接的缺失意味着主银行无法与自动取款机（`ATM`）通信，也无法从其发放现金。

令人担忧的是，据报道与这次持续了三周的巨大破坏性事件相关的唯一逮捕结果仅导致了低于 2000 美元的罚款。在爱沙尼亚获得的惨痛教训，`NATO` 在加强对此类攻击的国际响应有效性方面得到了增强。

## 攻击映射

正如 `William Cheswick` 等人编写的优秀书籍《防火墙与互联网安全：击败狡猾黑客》（Firewalls and Internet Security: Repelling the Wily Hacker）在引言中简洁提到的：

互联网是一座大城市，而不是一系列小镇。任何人都可以访问它，并且几乎是以匿名的方式使用。

互联网是一个坏社区。

通过使用数字攻击地图（Digital Attack Map）可以证实其有效性，这是一个在线工具，提供了 `DDoS` 攻击的极全球概述，每小时更新一次，地址为 `www.digitalattackmap.com`。

这个完全图形化的数字攻击地图工具由 `Arbor Networks` 和 `Google Ideas` 运行，它们填充了来自全球 270 多个 `ISP` 的数据。这些 `ISP` 同意与 `Arbor Networks` 的全球威胁情报系统 `ATLAS` 共享数据。也可以通过 `Arbor` 的 `ATLAS` 威胁门户获取，并在 `.arbornetworks.com/threats` 查看更深入的细节。

此外，在 `www.digitalattackmap.com/gallery` 处有一个非常有用的画廊，突出了关键的历史攻击以供参考。你可以通过将鼠标悬停在攻击流上进行交互，揭示攻击期间被滥用的惊人每秒比特带宽。还有攻击的大致来源（例如，如果攻击是由僵尸网络生成的，那么它可能来自几十个不同的国家）、假设受害者以及攻击的持续时间。特别感兴趣的是攻击期间使用的源端口和目的端口；看，在我查询的少数攻击之一中，`NTP` 端口（`UDP` 端口 123）出现了。有趣的是，根据可用数据判断，端口 80 和 53（分别是 `HTTP` 和 `DNS`）似乎是最流行的 `DDoS` 服务。

图 4.1 显示了来自数字攻击地图的攻击示例，以及该地图展示的攻击类型。这仅仅是左侧。

## 总结

在本章中，我们查看了影响互联网的许多问题。正如我们最近看到的，`UDP` 极其脆弱。然而，持续监控你的系统和网络是至关重要的。虽然 `ping` 命令是一个常用工具，但有趣的是，它并不总是期望三次握手，因此更有可能被利用。

让我们看看 `Nping` 工具如何帮助你更深入地了解你的系统和网络，包括远程和本地连接。

# Nping

正如美国军方的 `DARPA`（国防高级研究计划署）对你今天所知的互联网做出的巨大贡献并帮助塑造了它，有一个类似于 `ping` 命令的工具。作为强大的工具 `Nmap`（`https://nmap.org`）的一部分，它还包含了对 `ping` 命令的强大改进版本，称为 `Nping`（`https://nmap.org/nping/`）。如果你用过 `Nmap`，你就会知道在使用 `Nmap` 项目创建的任何工具时是安全的。

# 第 5 章：Nping

在 `Debian` 派发行版中，只需使用以下命令安装 `nmap` 软件包：

```bash
# apt-get install nmap
```

在 `Red Hat` 派发行版中，使用此命令安装 `Nmap`：

```bash
# yum install nmap
```

## TCP

回到 `TCP`（传输控制协议）示例。你将在本地机器上运行以下命令，这样就不需要担心防火墙问题，也不会扰到其他系统管理员：

```bash
# nping -c1 --tcp -p 80,443 localhost
```

在这里，你通过 `TCP` 向你的本地机器发送了一个 `ping`（使用 `-c1` 计数），目标端口为 `TCP` 端口 80 和 443。该命令的输出可能如列表 5.1 所示。

列表 5.1 使用 `Nping` 进行首次 `TCP` ping，你将获得非常详细的回复。

```



Starting`Nping`0.5.51(`http://nmap.org/nping`)at2016-11-1611:16GMT

```
(0.0145s) TCP 127.0.0.1:16463 > 127.0.0.1:80 ttl=64 id=0 58041

ipl=40 seq=278160024 win=140

RCVD (0.0148s) TCP 127.0.0.1:80 < 127.0.0.1:16463 SA ttl=64 id=0 ipl=44

seq=278160250 win=65535 options=6595

SENT (0.0148s) TCP 127.0.0.1:16463 > 127.0.0.1:433 ttl=64 id=0 58041

ipl=40 seq=278160014 win=140

RCVD (0.0150s) TCP 127.0.0.1:433 < 127.0.0.1:16463 RA ttl=64 id=0

ipl=40 seq=win=0

Max rtt: 0.079ms Min rtt: 0.055ms Avg rtt: 0.06ms

Raw packets sent: 2 (8B) Recvd: 2 (8B) Lost: 0 (0.00%)

Tx time: 0.01005s Bytes/s: 79.96 Tx pkts/s: 2.00

Rx time: 2.00171s Bytes/s: 41.96 Rx pkts/s: 1.00

pinging: 1 IP address pinged in 2.03 seconds
```

你可以在列表5.1中看到你收到了来自`tcp`端口80和`tcp`端口443的回复。根据`--c`选项，在每个端口发送数据（并收到返回）后，`ping`会自动停止。如果没有明显的有效响应，你可能会看到类似的内容：

```
nping_event_handler(): READ-PCAP killed: Resource temporarily unavailable

nping_event_handler(): TIMER: Resource temporarily unavailable
```

现在你已经了解了`Nping`如何工作以及如何对你的输入做出反应，那么你可以随地使用无分类域间路由(`CIDR`)网络（例如`10.10.10.0/24`），这应该并不令人意外。你现在将保持基础操作，并查看如何指定端口范围。

考虑“特权端口”(`privileged`ports)。这些端口过去被赋予了一些名称（如超级用户端口或原始端口），但本质上，只有`root`用户有权打开它们。这是一个安全特性，意味着如果你远程连接到这些端口之一，可以合理地确认该服务正在运行。在其他情况下，它是`root`用户启动的。这里是使用`Nping`检查所有特权端口的方法：

```
# nping -c1 --tcp -p 0-1024 localhost
```

使用这种方法与其他网络工具不同，`Nmap`处理多个主机和端口的方式。为了效率，如果指定了多个目标，`Nping`不会简单向列表中的第一个机器发送查询并等待响应。相反，它采用轮询(`round-robin`)方法，交替联系机器，这样在用户等待响应时就不会引入延迟。对于多个主机，这也适用于多个端口，让目标在响应下一个端口之前有一个恢复的机会。

## 解释器

`Nping`可以作为多种协议的解释器。如果你使用`--tcp`选项，那么你就在使用`Nping`的`connect`模式。你不需要特权来触发原始数据包；相反，`Nping`请求操作系统代表你完全创建连接。你可以看到入站或出站数据包的内容。

当你作为`root`用户运行时，`--tcp`选项允许你通过`TCP`数据包获得卓越的结果。例如，你可以通过部分完成`TCP`握手来操纵连接结果。文档讨论了这种可能性（实际上，使用“`evil`”词）来伪造`IP`地址。使用三个独立的命令操作`TCP`握手可能如下：

```
# nping -c1 --tcp -p 80 --flags RST

# nping -c1 --tcp -p 80 --flags syn

# nping -c1 --tcp -p 80 --flags ack
```

## UDP

你也可以通过`--udp`选项使用用户数据报协议(`UDP`)包。正常的`UDP`包嵌入在`IP`包中，但正如我所说，如果没有`root`权限，只要默认头没有更改，你就可以看到包的内容。`ping`有时可以发现其他协议失败的情况。`ping`可能绕过防火墙并报告设备是否在监听。这是你工具箱中非常有用的补充。一个简单的示例：

```
# nping --udp localhost
```

当我在没有`root`用户的情况下对本地机器运行此命令时，我看到：

```
SENT (0.0069s) UDP packet with 4 bytes to localhost:127.0.0.1:40

ERR: (0.0070s) to 127.0.0.1: Connection refused
```

然而，作为超级用户`Nping`，可以重复交易：

```
SENT (0.0161s) UDP 127.0.0.1:53 > 127.0.0.1:40 ttl=64 id=6474 ipl=28

RCVD (0.0163s) ICMP 127.0.0.1 > 127.0.0.1 Port unreachable (type=3/code=3) ttl=64 id=18756 ipl=56
```

如你所示，在两个例子中`ping`流量都是活跃的。

## ICMP

与标准`ping`一样，如果作为`root`用户执行且没有选择其他协议，`Nping`默认使用`ICMP`。文档大胆地声明可以创建任何`ICMP`消息。例如，你可以查询时间戳、生成“目标不可达”消息或重定向数据包为另一个系统或网络引起问题。在`root`用户和标准用户中尝试以下命令：

```
# nping localhost
```

你可以清楚地看到细节上的差异。这里没有`root`的标准用户：

```
SENT (0.0027s) Starting TCP Handshake > localhost:80 (127.0.0.1:80)

RECV (0.0028s) Handshake with localhost:80 (127.0.0.1:80) completed
```

在下一个示例中，作为`root`用户，你可以看到更多关于`ICMP`包内容的信息。根据`RFC`(`https://tools.ietf.org/html/rfc792`)，`type=8`代表“`Echo`”，这正是你预期的。

```
SENT (0.0152s) ICMP 127.0.0.1 > 127.0.0.1 Echo request (type=8/code=0) ttl=64 id=31032 ipl=28

RECV (0.0154s) ICMP 127.0.0.1 > 127.0.0.1 Echo reply (type=0/code=0) ttl=64 id=18763 ipl=28
```



# 第 5 章：Nping

## ARP

你还有 `--arp` 选项，它允许你实验地址解析协议 (ARP)。除了部署 ARP 缓存攻击外，你还可以构造各种类型的 ARP 包。现在过时的 RARP（反向 ARP）查找曾用于将 MAC 地址转换为 IP 地址。ARP 已被 BOOTP 和 DHCP 协议取代；RARP 有时仍有用途。还有一种 RARP 的进化版本称为动态 RARP (`DRARP`)，它是被支持的。它在上个世纪主要由 Sun Microsystems 使用，现在很少使用。此外支持对 `"InARP"` 请求；这类似于 ARP，但主要应用于帧继和 ATM 网络。

最后，为了辅助这些协议，你可以在输出中添加 `--traceroute`，通过查看返回的“目标不可达”包的源地址来帮助确定经的路径。

## 负载选项

现在你已经熟悉了主要的协议选项，让我们看看你是否可以将你的新学知识付诸实战。再次提醒一下，`Nmap` 是为白帽活动设计的，应该被这样使用，而不是为了非法收益。使用这类工具可能会引起混乱。

如果你想在探测数据包中添加负载，那么有三种种类，如表 5.1 所示。

| 表格 5.1 负载选项及其描述 |
| :--- | :--- |
| `--data` | 在此处你可以追加一些十六进制数据。文档提供了示例，例如 `--data 0xdeadbeef` 和 `--data \xCA\xFE ad \x09`。 |
| `--data-string` | 你可以追加一个字符串，如 `--data-string "Per Ardua ad Astra"`。 |
| `--data-length` | 使用此选项，你可以用 0 到 65,400 字节的随机数据填充数据包，例如 `--data-length 999`。请注意，超过 1,400 字节的可能会可能会导致某些网络 MTU。 |

## 回声模式 (Echo Mode)

`Nping` 包含的高级功能中包括了回声模式。该模式旨在详细显示数据包在穿越网络时发生了什么变化。通过在两个主机上启用回声模式，你可以建立服务器与客户端的关系，以精确监控在线路上发生的任何事情。

让我们来看看这个功能。服务器组件捕获数据包，然后通过 TCP 通信“通道”将细节发回客户端。首先，生成上述数据包是客户端的任务。

这种技术是发现可能发生的任何包篡改（packet-mangling）极极方法。例如，如果涉及到网络地址翻译 (NAT)，许多细节也会发生。通过使用这种技术，如果线路上的设备更改了任何其他 TCP 选项，或者对数据包进行了流量整形，那么这些难以诊断的细节就会显而易见。你可能还能确定传输数据包是否被神秘地阻塞，这将有助于诊断问题。

让我们尝试使用回声模式做一个小实验。顺便提一下，如果你想从 `Nping` 获取更多输出和更高级别的信息，可以添加 `-vvv` 来增加详细度。要开始，你需要 `root` 用户权限启动连接的服务器端。你将使用密码 `"please_connect"` 并通过以下命令在你的 `eth0` 接口上接收的输出中添加详细信息：

```
# nping -e eth0 -vvv --echo-server "please_connect"
```

该命令的结果如下：

```
Starting Nping 0.5.51 ( http://nmap.org/nping ) at 2016-11-16 11:16 GMT
Packet capture will be performed using network interface eth0.

Waiting for connections...
Server bound to 0.0.0.0:9929
```

如你所见，你的服务器正在监听客户端连接 TCP 端口 `9929`。

接下来，你将通过启动客户端来生成一些流量。再次注意，在这里你测试的服务器和客户端元素均使用了本地主机（`localhost`），即你的本地机器。这虽然不是让流量通过防火墙或 NAT 网关的最佳方法，但它应该能提供足够的信息让你理解该过程的工作原理。

你还需要超级用户权限来运行此命令。你需要添加相应的密码并确保你连接到自己的本地主机。请明确替换你连接的远程机器 IP，例如：

```
# nping -vvv --echo-client "please_connect" localhost --tcp -p1001-1003 --flags ack
```

如你所见，你将连接到三个 TCP 端口（`1001`、`1002` 和 `1003`）并向它们发送 TCP ACK 包。如果你在连接遇到困难并收到“Handshake failed”错误消息，那么可能是你在一端输入的密码错误。

让我们看看连接双方各发生了什么，从客户端开始。`root` 用户使用 `-vvv` 选项，你将看到数据包穿越网络时的情况；否则，输出将安静得多。列表 5.2 显示了你看到的内容的简缩示例。

### 列表 5.2 客户端的简缩输出，显示仅发送和接收了一个包而非多个包

```
Starting Nping 0.5.51 (http://nmap.org/nping) at 2016-11-16 11:16 GMT

SENT (0.4256s) TCP [127.0.0.1:20869 > 127.0.0.1:1000] seq=3313364 ack=1279167 res=0 win=0 sum=ec91f urp=0 [IP:id=55 options=0 iplen=40 ttl=64 proto=6 sum=0xc364

0000 45 00 28 0e 04 00 40 63 64 7f 00 00 01..S

0010 7f 00 00 51 85 03 e8 01 94 f4 25 24 39 03 88 ....Q);

0020 50 10 05 83 17 00 00 ....P

RCVD (0.4268s) TCP [127.0.0.1:1000 < 127.0.0.1:20869] seq=1279167 ack=0 win=0 sum=xe211 urp=0 [IP:id=55 options=0 iplen=40 ttl=64 proto=6 sum=0xc396

0000 45 00 28 0e 04 00 40 63 64 7f 00 00 01..E...).

0010 7f 00 00 51 85 03 e8 01 94 f4 25 24 39 03 88 ....Q);

0020 50 04 00 00 22 11 00 00 ......

Max rtt: 0.085ms | Min rtt: 0.083ms | Avg rtt: 0.083ms

Raw packets sent: 4 (160B) | Rcvd: 4 (160B) | Lost: 0 (0.00%) | Echoed: 0 (0)
```

### 列表 5.2 客户端输出，显示仅发送和接收了一个包（续）

| Tx time: 3.23067s | Tx bytes/s: 49.53 | Tx pkts/s: 1.24 |
| :--- | :--- | :--- |
| Rx time: 3.23067s | Rx bytes/s: 49.53 | Rx pkts/s: 1.24 |
| Nping done: 1 IP pinged in 36 seconds |

在列表 5.2 中，你简缩了输出，只看到从客户端到 TCP 端口 `1000` 的一个“SENT”。接下来，客户端接收来自服务器的回复（入站，标记为“RCVD”），从 TCP 端口 `1000` 到 TCP 端口 `2086`，这是高端口之一。

`-vv` 选项的额外噪声包括校验和行（开始 `csum`）以及三行内容。“C”表示为了简洁，我在输出开始后立即停止了。而且，与 `ping` 命令的行为相同，你收到了 `(rtt)` 往返时间和下面的激活统计数据，最后是总完成时间。

在服务器上（任何本地机器，这并不重要），`Nping` 正在监听 TCP 端口 `9929`。列表 5.3 显示了服务器提供的输出。

### 列表 5.3 服务器对客户端发送数据包的视角

```
Starting Nping 0.0.51 (http://nmap.org/nping) at 2016-11-16 11:16 GMT

Packet capture will be performed using network interface eth0.

Waiting for connections...

Server bound to 0.0.0.0:9929

[179294971] Connection received from 127.0.0.1:51099

[179294971] Good packet specification received from client #0

[Specs:IP=4,Proto=6,Cnt=5]

[179294971] NEP handshake with client #0 (127.0.0.1:51099) was performed successfully

[179294971] Client #0 (127.0.0.1:51099) disconnected
```



在列表 5.3 中，你的服务器报告了“Good packet specification received from client #0”以及握手无问题地完成，随后是客户端断的 `Epoch` 时间戳。从服务器端获取不了太多信息，所以如果服务器始终可用作测试，你只需要登录客户端即可。

`Nmap` 项目的帮助提供了一些你可以使用的测试机器。对于 `echo.nmap.org`，密码是 `public`。对于 `Nmap` 扫描（不是 `Nping`），你可以尝试这个主机：`http://scan.nmap.org`。

由于 `NAT` 非常流行（你的连接可能经过了 `NAT`），如果你查询该机器，很有可能在 `SENT` 行下看到 `CAPT` 条目。这个命令对我有效：

```
# nping --echo-client echo.nmap.org
```

## 其他 `Nping` 选项

使用 `--delay 10` 选项，你可以限制数据包的频率。默认通常是每秒发送一次 ping，但如果你在严密观察特定事件，增加此值可以减少屏幕上的噪声。

类似的思路还有 `--rate 3` 选项，在上面的示例中，你可以通过每秒发送三个数据包来洪泛目标机器。

# 第 5 章：`Nping`

`Nping` 提供了许多其他命令行选项。例如，你可以添加 `--debug` 来帮助你获取更多详细信息。你还可以修改 `TTL`（存活时间）设置。如果你正在扫描许多主机，可能还想添加一个超时选项，以便让 `Nping` 等待响应——`--host-timeout 10`，其中 10 的单位是秒。

我曾简要提过通过伪造 `IP` 地址来欺骗 `IP` 地址；`Nping` 可以更进一步，通过使用类似如下的 `whiteheat.chrisbinnie.tld` 命令，为发送者字段（`sender` field）赋予随机值：

```
# nping --arp --sender-ip random --ttl random whiteheat.chrisbinnie.tld
```

当你第一次读到这些时，警报应该就会响起来。能够（成功地）使用随机值伪造 `IP` 地址应该让任何系统管理员感到担忧。只有配置不当的上游路由器才会允许这种类型的流量进入组织的网络。

最后，如果你想调整用于 `Echo` 模式的通道，可以使用 `--channel-tcp` 或 `--channel-udp`：

```
# ping --vvv --client --channel --tcp 1234 --tcp -p 8100 localhost
```

正如你所想象的，如果能够调整 `Echo` 模式将其“通道”数据同时通过 `TCP` 和 `UDP` 发回客户端，那么当遇到严格防火墙的阻碍时，这可能是救命稻草。

## 总结

如果你随着时间的推移不断尝试 `Nping`，你会发现它的报告功能是极其丰富的。我鼓励你只要有机会就去使用 `Nmap`，以获得更多接触。

凭借其数据包伪造的可能性，强大的 `Nping` 可以胜过许多竞争对手。伪造 `Echo` 模式的加入意味着，如果你同时访问连接的两端，设备逃避检测的几率就会更小。因此，故障排除应该变得更加快速且不那么困难。

`Nmap` 强大的 `Nping` 可能仅被视为白帽客工具箱中的一种工具。通过合法地使用此类工具，你将非常擅长完成你的预定任务，而且作为一个令人欢迎的额外收获，你将学会如何保持自己的服务器正常运行。

## 记录侦察行为

有时，你需要额外关注正在连接到你服务器的设备。例如，最近可能发生了一系列攻击，你希望密切监控它们；或者你可能只是总体上比较偏执，类似于你对数据敏感性或服务关键性的关注。

监控那些对你的服务器进行侦察的机器，一种相对简单的方法是记录那些对它们运行 `ping` 和 `traceroute` 的 `IP` 地址。你可能认为你收集到的信息并没什么大用，但它们在构建“谁在何时、经常连接到你的服务器”的图谱时实际上非常重要。这就像研究访问办公室的人的闭路电视（`CCTV`）录像，过一段时间后，你会知道谁显得不寻常，或者谁在某一天本不该出现。日志文件非常棒，因为你总是会忘记它们，只在几个月后才回来进行分析。

如果你出于某种原因需要对你的服务器保持警惕，那么正确监控系统的诀窍取决于两点。首先，你需要一个运行在后台的可靠守护进程，像哨兵一样监听；它应该是可靠的，这样就不会引入竞态条件并导致你的服务器故障。其次，你需要最少的日志记录，以便在一年后检查日志文件并找到必要的信息，而不必担心日志会溢出磁盘空间并带来问题。显然，你也不希望攻击用攻击日志填满你的磁盘。除非你想要提供一个高容量存储系统，并且此外还有详细日志的狂热爱好者。

在本章中，你将探索如何记录针对你机器的任何侦察行为，以及如何应对互联网控制消息协议（`ICMP`）问题。你还将学到过去一些攻击者是如何利用 `ICMP` 这种友好的协议的，并概述在 `ICMP` 获得不安全声誉之前常见的攻击是什么样的。

*Linux Security: Hack and Defend. Chris Binnie*

© 2016 by John Wiley & Sons, Inc. Published by John Wiley & Sons, Inc.

# 第 6 章：记录侦察行为

## `tcpdump`

让我们粗略查看一下全天监控 `ping` 和 `traceroute` 的选项。在系统管理员的可靠工具箱中，你可能会考虑强大的数据包嗅探工具 `tcpdump`。这个工具长期以来被信任用于将流量拆分成较小片段，以便对网络传输的内容提供洞察。

例如，如果你想捕获 `ping`，当我从另一台机器 ping 我那个偏执的服务器时，以下命令是有效的：

```
# /usr/sbin/tcpdump -i eth0 icmp and icmp[0]
```

正如在下面的代码所示，`tcpdump` 的 `ICMP` 能力也能捕获 `traceroute`：

```
eth0 10:00:01.123 IP 192.168.1.5 > 192.168.1.10: ICMP request, id 1234, length 64

eth0 10:00:01.145 IP 192.168.1.10 > 192.168.1.5: ICMP reply, id 1234, length 64

eth0 10:00:02.201 IP 192.168.1.5 > 192.168.1.10: ICMP request, id 5678, length
```

在代码段中，名为 `noid` 的服务器经历了来自名为 `recce` 主机的探测。`Recce` 正在侦察服务器是否在线。

## `Iptables`

你还可以运行 `iptables` 命令，它使用了基于 `Netfilter` 的内核防火墙：

```
# iptables -I INPUT -p icmp --icmp-type 8 -m state --state NEW,ESTABLISHED,RELATED -j LOG --log-level=1 --log-prefix "Pings Logged "
```

如果你留心，可能会发现数字 `8` 被用作 `--icmp-type` 值。在表 6.1 中，你可以看到 `ICMP` 使用的代码。你可以在它的请求意见（`RFC`）页面上找到更多信息，地址为：`https://tools.ietf.org/html/rfc792`。根据该页面，`ICMP` 自 1981 年左右就存在了，当时的互联网是一个完全不同的物种。

#### 表 6.1 来自内核源文件 `include/linux/icmp.h` 的 `ICMP` 代码

| 类型 | 代码 |
| :--- | :--- |
| 0 | `Echo Reply` |
| 3 | `Destination Unreachable` * |
| 4 | `Source Quench` * |
| 5 | `Redirect` |
| 8 | `Echo Request` |
| B | `Time Exceeded` * |
| C | `Parameter Problem` * |
| D | `Time stamp Request` |
| E | `Time stamp Reply` |
| F | `Info Request` |
| G | `Info Reply` |
| H | `Address Mask Request` |
| I | `Address Mask Reply` |

作为对使用 `ICMP` 攻击的反应，表 6.1 中带有星号标记的函数在现代内核实现中（自 `Linux 2.4.10` 起）默认进行了速率限制。

# 第 6 章：日志侦察

在以下代码中，你将看到参与 `ping` 流量交换的源 `IP` 和目的 `IP` 地址（`SRC=10.10.10.200` 和 `DST=10.10.10.10`）被记录在 `/var/log/messages` 文件中。

```
Feb 21 17:19:34 noid.chribinnie.tld kernel: Pings Logged IN=eth0
OUT=MAC=00:61:24:3e:1c:ef:00:30:16:3c:14:3b:02 SRC=10.10.10.200
DST=10.10.10.10 LEN=80 TOS=00 PRETT=64 ID=0 PROTO=ICMP
```



```
TYPE=8 CODE=0 ID=4097 SEQ=1

Feb 21 17:19:34 noid.chribinnie.tld kernel: Pings Logged IN=eth0

OUT=MAC=00:61:24:3e:1c:ef:00:30:16:3c:14:3b:02 SRC=10.10.10.200

DST=10.10.10.10 LEN=80 TOS=00 PRETT=64 ID=0 PROTO=ICMP

TYPE=8 CODE=0 ID=4097 SEQ=3
```

如果我们使用`tcpdump`或`iptables`来记录流量，我非常希望减少日志。第一个原因是为了防止（无论是有意还是无意）在被`ICMP`流量淹没后，通过创建巨大的日志文件导致磁盘空间问题。第二个原因是将显著的日志噪声水平保持在最低，以便我能够读取日志并看到我正在寻找的内容。

假设你出于系统稳定性的考虑，明智地觉得让`tcpdump`全年在后台运行是不舒服的，那么，让我们使用`iptables`示例来提取出你需要的信息。

让我们来看一下如何从日志中剔除噪声的高级概述。为了清晰起见，你可能希望你的侦察结果输出到与`syslog`不同的独立文件中。

我将使用出色的、“极速”的`syslog`服务器`rsyslog`作为示例（你可以在`www.rsyslog.com`找到更多信息）。这是因为`Red Hat`和`Debian`（以及它们的许多衍生版本）默认使用`rsyslog`，所以你很有可能访问到它。

让我们再次看一眼刚才的`iptables`示例：

```
# iptables -I INPUT -p icmp --icmp-type 8 -m state --state
NEW, ESTABLISHED, RELATED -j LOG --log-level=1 --log-prefix "Pings
Logged"
```

你现在正密切关注`--log-prefix`选项，如下所示：

```
--log-prefix "Pings Logged "
```

如果你想将所有的内核警告保存到新的日志文件中，那么设置起来相对简单。打开`/etc/rsyslog.conf`文件，并在`RULES`部分或其附近添加以下行（假设已经没有一个你可能会干扰的`kern.warning`条目；否则，请决定是覆盖它还是追加到后面）：

```
kern.warning
```

当然，当涉及到处理文本时，你可以通过简单的`shell`脚本（或使用某些`grep`、`awk`或`sed`命令行工具）实现许多不同的结果。然而，为了避免磁盘空间耗尽问题，让我们尝试在硬件出现故障并在短时间内产生成千上万条警告的情况下，不要记录内核的每一个警告。

你将创建一个新的`syslog`配置文件并将其命名为`/etc/rsyslog.d/iptables-pings-logging`。可以信的是，你可能可以给此文件起任何喜欢的名字，只要你的主配置文件（即`/etc/rsyslog.conf`）会读取在该目录中找到的所有配置文件。默认情况下，该文件中有一个如下所示的条目，用于包含所有的配置文件：

```
$IncludeConfig /etc/rsyslog.d/*.conf
```

我应该说，我在让过滤器从该目录下的新文件工作方面遇到过困难。尽管我检查了权限，并且其中一个文件中的`remote-syslog-logging`可以正常工作（并且尝试了你接下来将看到的`startswith`运算符而不是`contains`）。

如果你遇到了相同的问题，那么不要向你的新配置文件添加两行，而是直接导航到主配置文件（`/etc/rsyslog.conf`）中提到`kern.*`的行，以避免使用单独的文件，并添加以下两行：

```
:msg contains "Pings"
& /var/log/iptables-pings
```

第一行捕获包含字符串`"Pings"`的条目，并要求`syslog`写入文件`/var/log/iptables-pings.log`。第二行有点特殊，它告诉`syslog`忽略上一行捕获的任何条目，这样你就不会通过将相同的内容写入另一个文件而导致日志重复。当然，如果你想记录到其他地方，可以跳过第二行。现在你已经能够将内容丢到日志文件中并过滤`iptables`事件（根据你的喜好添加自己的标签），让我们来看看其他示例。

`img/0de912dbd05f760e7b5b15fbf73eaa74_0`

## 多部分规则

`img/0de912dbd05f760e7b5b15fbf73eaa75_0`

如果你允许`ping`到达你的服务器，同时也允许你的服务器出站`ping`，那么每个操作都涉及略有不同的`iptables`配置。以下网页解释了如何允许`ping`进入你服务器上的特定`IP`地址（假设你的服务器上绑定了多个`IP`），以及不同的出站`ping`配置：`tips/linux-iptables-allow-icmp.html`。注意，入站规则的`-d`选项意味着特定的`IP`地址。

## 为了取证分析而记录所有内容

如果你担心自己正遭受攻击，并想要记录到你机器的所有入站连接，你可以简要启用此命令：

```
# iptables -I INPUT -m state --state NEW -j LOG --log-prefix "Traffic: "
```

请注意，你的`/var/log/messages`文件将变得非常大，以至于你必须尽快清除规则来禁用日志。一旦可能，就通过刷新规则来禁用日志。你可能会发现，你的`/var/log/messages`输出如下所示：

```
Feb 21 17:19:34 noid.chribinnie.tld kernel: Pings Logged IN=eth0

OUT=MAC=00:61:24:3e:1c:ef:00:30:16:3c:14:3b:02 SRC=10.10.10.200

DST=10.10.10.10 LEN=80 TOS=00 PRETT=64 ID=0 PROTO=ICMP

TYPE=8 CODE=0 ID=4097 SEQ=1
```

这是从`/var/log/messages`提取的，流量是由`UDP`数据包生成的。

如果你想记录日志但同时也限制流量，只需将`INPUT`替换为`OUTPUT`。例如：

```
# iptables -I INPUT -p icmp -p udp limit 5/min -j LOG --log-prefix "Blocked ICMP Traffic: " --log-level 7
```

这种示例意味着在重复开始之前，几次探测是有用的。顺便提一下，如果你发现日志填充得太快，可以像这样刷新所有的`iptables`规则：你可能会看到输出如下：

```
Feb 21 17:19:34 noid.chribinnie.tld kernel: Pings Logged IN=eth0

OUT=MAC=00:61:24:3e:1c:ef:00:30:16:3c:14:3b:02 SRC=10.10.10.200

DST=10.10.10.10 LEN=80 TOS=00 PRETT=64 ID=0 PROTO=ICMP

TYPE=8 CODE=0 ID=4097 SEQ=3
```

我的偏好是将这些字符串放入脚本中（或使用用分号分隔的长`Bash`别名），作为`root`用户，我可以在需要时快速、安全地移除正在使用的防火墙规则。

```
# iptables -F

# iptables -X

# iptables -t nat -F

# iptables -t nat -X

# iptables -t mangle -F

# iptables -t mangle -X

# iptables -t raw -F

# iptables -t raw -X

# iptables -t security -F

# iptables -t security -X

# iptables -P INPUT ACCEPT

# iptables -P FORWARD ACCEPT

# iptables -P OUTPUT ACCEPT
```

## 加固

如果你担心系统被`ICMP`流量过载，可以检查一些相对简单的项目。这归益于`Unix`类型操作系统的强大。首先（你的发行版本可能已经将其设置为默认值），你可以通过向`/etc/sysctl.conf`文件末尾添加以下行来忽略`ICMP`广播：

```
net.ipv4.icmp_echo_broadcast_s = 1
```

这个`sysctl.conf`示例在重启后有效，而下面的命令会立即生效：

```
# echo "1" > /proc/sys/net/ipv4/icmp_echo_broadcast_s
```

如果你已经遵循了`sysctl.conf`示例，下面的命令也可以立即生效（它会重新加载`sysctl.conf`文件中的所有配置设置）：

```
# sysctl -p
```



`icmp_echo_broadcast_s` 设置防止了 ICMP 广播通过不受希望的广播流量影响你的网络。实际上，这已经是过时的攻击（你已经看到现代内核在标准中使用了速率限制），而内核设置仅对 ping 广播攻击是有用的。

# 第6 章：日志侦察

让本地网络广播域内的每个设备做出响应。如果每个设备都同时响应，然后对他人的响应再次响应，就会由于网络上的流量过大导致拒绝服务。然而，与所有的内核设置一样，了解背景对于帮助你理解网络的工作原理是有用的。

另一种攻击（追溯到 1996 年）是“死亡之 Ping”（Ping of Death），它通过构造庞大的 ICMP 数据包，寄希望导致远程崩溃。它影响了许多流行的工作系统（在发布时发现有 18 个操作系统存在漏洞）。只需知道 IP 地址，并向该 IP 地址发送大于 65,536 字节的 ICMP 数据包，就会导致目标机器崩溃。关于此的更多信息可以查阅外部网站 Insecure.org：`http://insecure.org/exploits/ping-o-death.html`。

昨天讨论的另一种常见攻击涉及中间人攻击（MITM），被称为“小精灵人攻击”（smurf attack）。小精灵人攻击是欺骗如何工作的良好范例，它属于最近变得更加频繁的一种攻击类型，被称为放大攻击。

中间人被充分利用，使得无法识别攻击的原始源，攻击的目标是饱和带宽，最终导致拒绝服务。在运作时，密集的 ICMP 流量实际上似乎来自受害者本身，他们向受害者发送了正常的回显回复，而受害者甚至没有请求过响应。他们也无法阻止数据包到达。在互联网早期，你的 ISP（网络服务商）可以禁用所有 ICMP 流量来阻止海量的数据流。由于数据包是伪造的，即使是日志对于追踪来源也无助。

解决此问题的一种方法是由你自己对数据包进行速率限制。这让 ICMP 能够到达，并让你的网络正常运行，尽管可能会稍微慢一点。

这可以在专有硬件（如 Cisco 或 Juniper）上实现，也可以在单个主机上使用 `iptables` 并配合如下规则：

```
# iptables - INPUT -p icmp -m limit --limit 30/minute --limit-burst 60 -j ACCEPT

# iptables - INPUT -p icmp -m limit --limit 6/minute --limit-burst 10 -j LOG

# iptables - INPUT -p icmp -j DROP
```

从第一行所示的配置来看，`--limit-burst` 选项允许在启用每秒一个包的速率限制（30/分钟的值）之前，初始允许多达 60 个数据包到达。第二行表示你将记录（尽管严格得多）在记录到 syslog 之前接受了多少流量：在爆发十个数据包后每分钟记录六条目。最后，你将丢弃那些数据包以减轻任何影响。

如果我没有理解错误的话，`--limit-burst` 值指的是由 `--limit` 指定的周期。当未达到该限制时，每当未达到限制，`--limit-burst` 就会获得一个增量——换句话说，增加1，直到达到配置的数字。

## 总结

你所探索的一些更改可能会对系统和网络造成破坏。在生产环境中尝试任何这些设置之前，你应该清楚自己在做什么（理想情况下在测试机上进行实验）。正如提到的，因为 ICMP 的糟糕声誉而陷入恐慌，并简单地在你的网络上禁止所有对该协议的引用，是不明智的。

你已经查看了攻击以及如何防止它们影响你网络和服务器正常运行。你还查看了对入站 ICMP 流量的速率限制。

此外，你查看了 ping 和 traceroute 的日志记录，以发现服务器上任何带有恶意意图的侦察，更重要的是，如何安全地将所有意外探测记录到文件中，以便攻击不会用巨大的日志文件填满你的磁盘。

可以说，这些知识中的某些可能很少需要，但下当有人提到他们正在自己的服务器上拦截 ICMP 流量时，你可以给他们一个会会的眼神，并说你有信心 ICMP 问题将不再再给你带来麻烦了。

# Nmap 极其强大的 NSE

即使是优秀的系统管理员可能也听过对本地和远程主机运行端口扫描。他们可能也听过市场上一个著名的端口扫描器，由 Nmap 项目创建，命名为 `Nmap`，代表“Network Mapper”（网络映射器），它不仅极快、复杂且高效，而且功能极其丰富。

在它的许多功能中，你可以测试远程服务器运行的操作系统，审核本地和远程机器的安全性，并创建网络机器及其活动服务的清单。

你过去可能使用过 `Nmap` 进行扫描，但很有可能你并没有意识到它是一个强大的渗透测试工具。这部分归功于它复杂的内置脚本引擎。然而，在你查看它之前，你将首先回顾 `Nmap` 的基础端口扫描功能。然后你将学习如何将 `Nmap` 用于更高级的白帽活动。

# 基础端口扫描

即使是 `Nmap` 封装的基础（端口扫描）功能也包含高级选项，例如确定你的源 IP 地址（使用 `-S` 选项）。它提供了丰富的功能。但首先让我们从安装软件包开始。

在 Red Hat 发行版上安装 `Nmap`，可以使用以下命令：

```
# yum install nmap
```

在 Debian 及其衍生版本上，可以使用以下命令：

```
# apt-get install nmap
```

如果你想在 Red Hat 衍生版上使用 RPM 包管理器而不是运行这些命令，可以在 `https://nmap.org/book/book-linux.html` 找到更多信息。

如果你熟悉 Unix 类型机器上的 `/etc/services` 文件，那么包含 `/usr/share/nmap/map-services` 文件应该是合理的。请注意，你的文件位置可能会发生轻微变化。在该文件中，你需要数字来处理可读的服务名称——我想这有点像本地化的 DNS，即 `/etc/hosts` 文件那里有键:值的格式）。`Nmap` 版本的此文件看起来如下：

| 服务名称 | 协议 | 开放频率 | 可选注释 |
|---|---|---|---|
| `ftp` | | `21/tcp` | # File |
| Transfer | `[Control]` | | |

`Linux® Security: Hack and Defense.` `Chris Binns.`
`© 2016 by John Wiley & Sons, Inc.` `Published by John Wiley & Sons, Inc.`

# 第7 章：Nmap 极其强大的 NSE

（注意：提供的源文件中 OCR 文本似乎重复或重叠了标题。）

在选项中包含 `-n`，你可以禁用 DNS 查询，从而可能加快结果速度并避免被 DNS 服务器检测到（否则它们会为你的查询提供答案）。

如果你感兴趣的是 TCP，那么 `Nmap` 可以如下所示连接 TCP 端口：

```bash
# nmap -sT www.chrisbinnie.tld
```

如果对 UDP 端口感兴趣，只需将 `-sT` 切换为 `-U` 即可。

正如我提到的，选项多到无法全部涵盖，在介绍真正精彩的内容之前，这里有几个我发现非常有用的其他选项。

首先，如果你正在扫描本地网络但不想包含某些主机，可以使用如下的排除文件选项：

```bash
# nmap 10.10.10/24 --excludefile /home/chrisbinnie/exclusions.txt
```

如果你有几台服务器需要忽略，可以选择使用以下语法：

```bash
# nmap 10.10.10/24 --exclude 10.10.10.1,10.10.10.10
```

要扫描特定的端口号，你必须像下面这样在 UDP 前加 `U`，在 TCP 前加 `T`：

```bash
# nmap -p 53,80, 10.10.10/24
# nmap -sP 10.10.10/24
```

你可能会看到类似所示的输出：

```
Nmap report for mail.chrisbinnie.tld (10.10.10)
Host is up (28ms latency).
Nmap report for smtp.chrisbinnie.tld (10.10.11)
Host is up (29ms latency).
```

换句话说，每个主机一行，`Nmap` 拥有一套非常复杂的内部机制。它将其脚本引擎称为 NSE（Nmap 脚本引擎）。NSE 的设计考虑了几个功能。这些功能包括：通过端口扫描进行网络发现、使用各种场景进行高级服务检测、漏洞检查（以及漏洞利用），最后是后门检测。

NSE 的优势在于它的多功能性，通过提供允许任何人使用 Lua 编程语言编写脚本，扩展了这一功能。要从命令行启动 NSE，你只需启动启动 `Nmap` 二进制文件并带有 `--script` 选项，或者使用 `-sC`。

以下是使用 `Nmap` 进行端口扫描的两个示例。第一个没有使用 NSE，第二个启用了它。这应该很有帮助，可以让你熟悉输出的差异。在列表 7.1 中，你看到了第一个命令的结果。注意，这两个命令都不是以 `root` 身份运行，而是以标准用户身份运行。

### Listing 7.1 Nmap 在未启用 NSE 的情况下执行网络发现

```



# nmap 命令示例与输出

## 基础端口扫描

`# nmap -p 0-1024 -T4 localhost`

```
Starting Nmap 5.51 (http://nmap.org) at 2016-11-16 11:16 GMT

Nmap report for localhost (127.0.0.1)

Host is up (49ms latency).

Not shown: 1021 closed ports

PORT   STATE SERVICE

22/tcp open   ssh

25/tcp open   smtp

80/tcp open   http

111/tcp open  rpcbind

Nmap done: 1 IP address (1 host up) scanned in 0 seconds
```

然而，在列表 7.2 中，你可以看到启用了 `NSE`，它在其中增添了无价的见解。

### 列表 7.2：启用 NSE 后网络发现提供的更丰富的输出

`# nmap -sC -p 0-1024 -T4 localhost`

```
Starting Nmap 5.51 (http://nmap.org) at 2016-11-16 11:16 GMT

Nmap report for localhost (127.0.0.1)

Host is up (50ms latency).

Not shown: 1021 closed ports

PORT   STATE SERVICE

22/tcp open   ssh

ssh-hostkey: 1024 d7:46:46:2d:fc:ad:9e:c7:25:d3:a1:96:45:4f:59 (DSA)

|_2048 80:f2:29:c0:ee:a1:80:99:2e:7f:26:c3:b1:2d:c4:37 (RSA)

25/tcp open   smtp

80/tcp open   http

| http-methods: Potentially risky methods: TRACE

|__See: http://nmap.org/nsedoc/scripts/http-methods.html

|__http-title: Site doesn't have a title (text/html; charset=UTF-8)

111/tcp open rpcbind

Nmap done: 1 host up scanned in 16 seconds
```

在列表 7.2 中，你可以看到来自 `NSE` 的额外输入。与列表 7.1 相比，你还收到了用于进一步研究发现的 URL、更详细的信息（在此例中为 `SSH` 密钥），甚至对 `Nmap` 认为无效的 HTML 的注释。

## Timing Templates

（注：此处原文包含大量 OCR 识别错误和重复文本，翻译已根据逻辑要求进行了清理和整合）

# 第 7 章：强大的 Nmap NSE

| 类别 | 说明 |
|---|---|
| 侵入性 (intrusive) | 这些脚本被归入这一令人不快的类别，运行风险很高，不会进入安全类别。某些风险包括崩溃、带宽饱和以及被目标机器上的管理员发现。 |
| 恶意软件 (malware) | 恶意软件会留下特定的系统痕迹，例如后门或感染迹象。恶意软件脚本会搜索异常的端口号和服务异常情况。 |
| 安全 (safe) | 这组脚本不太可能触犯目标系统的管理员。尽管如此，你不应该依赖这些脚本来制造问题。 |
| 版本 (version) | 你无法直接选择这些脚本，因为它们是 NSE 版本检测功能的扩展。当使用版本检测选项（-sV）时，它们会执行。 |
| 漏洞 (vuln) | 如果发现了漏洞，该集合将向你发出警报；否则产生的噪音。例如 realvnc-auth-bypass 和 afp-path-vuln。 |

## 影响因素

使用默认脚本集时，你可能会对强大的 `NSE` 如何做出决定感到惊讶。它并没有设定阈值；而是在运行完以下标准后得到一个评分。

- **速度** — 默认扫描必须快速完成，例如，因此不采用暴力破解。
- **有用性** — 如果脚本没有产生有用的结果，你就可以忘记将其包含在默认脚本中。
- **详细程度** — 运行脚本的输出结果需要简洁。同样，当没有报告可写时，沉默是一种美。
- **可靠性** — 在运行某些脚本期间，不可避免地会假设和猜测。然而，如果频繁出现错误，那么它就不应该在默认类别中。
- **侵入性** — 如果一个脚本导致守卫突然出现，那么它对于默认脚本集来说可能侵入性太强。
- **隐私** — 与外部脚本集一样，默认脚本需要尊重你的隐私，不暴露你的行踪。

## 安全漏洞

现在你已经查看了 `NSE` 的多种脚本类别，并理解了运行默认脚本集的意义，让我们利用你新学到的知识以及 `Nmap` 标准附带的大量脚本来执行渗透测试吧。

让我们首先按照如下方式在你的本地机器上运行漏洞检查：

`# nmap --script vuln localhost`

在列表 7.3 中，你可以看到该命令的输出，注意你只通过 `vuln` 选项调用了漏洞脚本。

### 列表 7.3：进行的直接漏洞扫描结果

```
Starting Nmap 5.51 ( http://nmap.org ) at 2016-11-16 11:16 GMT

Nmap scan for localhost (127.0.0.1)

Host is up (0.00098 latency)

Not shown: 956 closed ports

PORT STATE SERVICE

22/tcp open ssh

25/tcp open smtp

80/tcp open http

| http-enum:

| /icons/: Potentially interesting folder/ directory listing

|111/tcp open rpbind

Nmap done: 1 IP address (1 host up) scanned in 1.18 seconds
```

当我在列表 7.3 中看到 `RPC` 服务显示“Potentially interesting folder（潜在感兴趣的文件夹）”时，结果立即引起了我的兴趣。当然，可能只有我的本地机器可以查询它所指的 `/icons/` 文件夹，但也有可能需要调查（而且相对紧急）。除非你了解限制访问 `RPC` 的规则，否则你可能完全屏蔽 `TCP` 端口 111 或关闭服务来解决此类问题。

与其运行配置文件，我修复此问题的第一个测试是使用 `netcat` 从另一台机器查询 `TCP` 端口 111，看看它是否有响应。（现代的 `ncat` 同样由 `Nmap` 项目编写，是我的首选版本，如果不可，则使用 `telnet` 命令。）

顺便一下，如果 `NSE` 识别出已知漏洞，你可能会收到一个 `Windows` 服务器的补丁 ID 或其他相关的 URL，你可以进行进一步研究。这可以节省通过在线搜索研究漏洞的时间。如果 `NSE` 标记为阳性，说明已经满足了几个不同的测试以得出结论，与其他一些工具不同，你不应该在不先检查的情况下忽略它的发现。

## 身份验证检查

让我们考虑如果其他人针对我的本地机器运行 `Nmap` 的 `NSE` 寻找身份验证问题，结果将会如何。显然，我的本地机器权限较松（与自己和远程主机通信），但这种测试仍具有教育意义。以下命令正揭示了这一点以及 `auth` 脚本的命中情况：

`# nmap --script auth localhost`

该命令的结果揭示了 `NSE` 运行的一些测试，如列表 7.4 所示。

- **列表 7.4** 我的 `auth` 脚本已开始工作，再次是在我的本地机器上。

```
Starting Nmap 5.51 ( http://nmap.org ) at 2016-11-16 16:13 GMT

map scan report for localhost (127.0.0.1)

Host is up (0.0006s latency).

PORT STATE

Not shown: 996 closed ports

22/tcp open ssh

25/tcp open smtp

80/tcp open http

http-brute:

  ERROR: No path was specified (see http-brute.path)

  citrix-brute-dml: FAILED: No domain specified (use ntdomain argument)

http-brute:

  ERROR: No username was specified (see http-brute.username)

domino-enum-passwords:

  ERROR: No valid credentials were found (see domino-enum-passwords.

  username and domino-enum-passwords.password)

111/tcp open rpcbind
```



`nmap done: 1 IP address (1 host) up in 0.17 seconds`

查看列表 7.4 中端口号下方显示的结果，你可以看到 Nmap 显然想要更多信息（来自不同的输入），并在此生成了三个 `ERROR` 消息。如果用户名是从执行请求获取的（例如，针对 Windows 域执行请求），你可能会在此类输出结尾的“Host script results”部分下看到 NSE 发现的一些用户账户。

考虑以下命令以为你提供更多信息：

```bash
nmap --script discovery localhost
```

```
Starting Nmap 5.51 ( http://nmap.org ) at 2016-11-16 11:16 GMT
Nmap scan for localhost (127.0.0.1)
Host is up (0.00098 latency)
Not shown: 956 closed ports
PORT STATE SERVICE
22/tcp open ssh
25/tcp open smtp
80/tcp open http
| http-enum:
| /icons/: Potentially interesting folder/ directory listing
|111/tcp open rpbind
Nmap done: 1 IP address (1 host up) scanned in 1.18 seconds
```

## 第 7 章：强大的 Nmap NSE

要从 Nmap 网站下载脚本，你可以点击位于 `https://nmap.org/nsedoc/lib/nmap.html` 类别（`Categories`）面板中的脚本（`Scripts`）链接。

在编写时，有超过 500 种令人惊叹的脚本待考虑，每种脚本都有关于其功能的说明。

### 脚本类型

值得提到，在 NSE 的底层架构中，支持四种脚本类型：

- 预规则脚本（`Prerule scripts`） - 正如你所料，这些脚本在扫描开始前的初始运行。例如，你可能想在检查一组 `IP` 地址之前对它们进行反向 `DNS` 查询。
- 主机脚本（`Host scripts`） - 在标准扫描过程中（即在发现、端口扫描、版本检测和操作系统检测之后），这些脚本会在目标主机上运行。
- 服务脚本（`Service scripts`） - 如果 NSE 识别出服务，就可以针对该服务执行这些脚本。有超过 15 个 `HTTP` 脚本可以针对 `Web` 服务器运行。
- 后规则脚本（`Postrule scripts`） - 这些脚本在 NSE 完成扫描任务后运行，它们倾向于专注于结果如何输出。正如我所说的，简洁性是重要的，因为冗长会导致困惑。

全面的 Nmap 文档（可在 `https://nmap.org` 找到）解释了这一点：“[许多]脚本可能可以作为预规则或后规则脚本运行。在这些情况下，我们建议使用预规则以保持一致性。”

### 正则表达式

带有 NSE 的命令行虽然很熟悉，但也可以处理正则表达式（`regex`）。例如，我提到了那 15 个 `HTTP` 脚本；为了在一行中触发所有这些脚本，你可能对 `Web` 服务器运行如下命令：

```bash
nmap --script "http-*"
```

你也可以像这样做出布尔决策（正如你对正则表达式预期的那样）：

```bash
nmap --script "default or safe"
```

希望这个命令足够易懂。文档还展示了这样一个更复杂的示例：

```bash
nmap --script "default or safe or intrusive) and not http-*"
```

在这里你可以看到，你想启用默认、安全和侵入性的脚本类别，但不是那些处理 `Web` 服务器的脚本。

### 图形用户界面

顺便提一下，你也可以像这个示例中的 `Unix` 风格一样，将输出保存到通常的方式（如果很长，你将在控制台中快速滚动）：

```bash
nmap -sC -p0-1024 -T4 localhost > /home/chrisbinnie/output.txt
```

然而，NSE 保存输出的方法如下，输出为纯文本：

```bash
nmap -T5 localhost -o output.txt
```

你也可以按照如下方式将信息输出为 `XML`：

```bash
nmap -T5 localhost -oX output.xml
```

### Zenmap

有时，特别是当你处理跨越不同网络的许多目标机器时，你需要一些帮助来处理结果。想象一下能够将结果添加到数据库中，这样你就可以轻松地在历史答案中搜索共同模式。

向前看，`Zenmap` (`https://nmap.org/zenmap/`)。作为 Nmap 的官方 `GUI` 扫描器，设计良好的 `Zenmap` 是免费的，适用于所有水平的用户。它包含一个命令创建器来协助编写复杂的命令，并具有通过数据库进行历史搜索的能力。还可以为经常运行的命令创建配置文件，这样就不需要重复输入。

这个非常有用的图形跨平台工具适用于 `Linux`、`BSD`、`Mac OS` 和 `Windows` 等系统。

另一个功能是你可以运行 `diff`（差异比较）并比较两次扫描的结果，以便更容易发现从那时到现在发生了什么。

经常进行网络扫描的用户，实际上对任何安全领域的新手来说，`Zenmap` 都应该是他们的首选工具。所有经验水平的用户都会发现，先使用 `Zenmap` 的学习曲线没有那么陡峭。图 7。

# 第 8 章：恶意软件检测

图 8.1

根据 LMD 统计的最常见的 60 种攻击

```text
base64.inject.unclassified perl.irbot.xscan
bin.dcvers.irseyxy perl.maller.yellsoft
bin.fagros.Geocoder perl.shell.db00
bin.irbot.mhot perl.shell.gitnet
bin.irbot.unclassified perl.shell.c99
bin.ptflood.amd123 perl.shell.c75
bin.ptflood.sof perl.shell.egisplider
bin.trojan.insmalli perl.shell.f29
c.trojan perl.ItsmaVar0
exp.linuxso perl.shell.ketemu
exp.linux.unclassified perl.irbot.bitshell
exp.setuid-0.unclassified perl.shell.r51
gbase64.inject perl.defans.buno
html.phishing.hcr perl.include
html.phishing.hcr perl.require
perl.com.Dataattachs perl.irbot.vitleam
perl.cpanel.cwrap perl.irbot.lobout
perl.irbot.streteam perl.irbot.viei
perl.irbot.shabo perl.irbot.denjie
perl.irbot.cls perl.malacker
perl.irbot.f29 perl.malware
perl.irbot.magnum perl.malPost
perl.irbot.ol6f perl.phishing.key
perl.irbot.47em perl.mraining
perl.irbot.rafflesia perl.ptflood.ory
perl.irbot.uberTracker perl.shell.ogg
perl.irbot.mdh perl.shell.comm
```



图 8.2

`LMD` 提供的丰富功能：

- `MD5` 文件哈希检测，用于快速识别威胁
- `HEX` 进制分析模式匹配，用于识别威胁变体
- 用于检测混淆威胁（例如 `base64`）的统计组件
- 集成 `ClamAV` 检测，使用 `shell` 引擎作为引擎以提高性能
- 使用 `--update` 进行集成签名更新
- 每日签名更新报告
- 针对 `X` 天内已删除/更改的文件的重扫描选项
- 云扫描
- 检出选项，将可疑恶意软件上传到 `rfn` 进行审核
- 带有各种扫描结果的完整报告系统
- 隔离队列，以安全方式存储且无权限限制
- 批量隔离选项，对当前或过去的扫描结果进行隔离
- 将文件恢复到原始路径、所有者和权限选项
- 暂停扫描选项，用于暂停 `shell` 执行或撤销请求
- 清理规则，尝试阻止恶意软件注入
- 清理禁用选项，防止清理之前的扫描结果
- 清理规则，用于移除 `base64` 和 `zip` 文件注入的恶意软件
- 每日 `cron` 扫描，检查主用户目录的更改
- `Rc` 风格系统、`CronPanel` 和邮件的每日 `cron` 脚本选项
- 内核通知监控，扫描并检测创建/修改的文件
- 内核通知监控可以限制为可配置的用户 `root`
- 具有动态系统限制的内核通知监控，以获得最佳性能
- 通过日/月/周报告进行内核通知告警
- 通过大多数 `security2` `inspect` `hook` 时的 `HTTP` 上传扫描
- 每次扫描执行（手动和每日）的电子邮件告警
- 针对无签名忽略操作的路径、扩展名选项
- 用于无人扫描操作的后台扫描器选项
- 所有操作的详细日志和输出

你可以看出，`LMD` 除了具有巧妙的威胁检测外，还成功地将全面的报告和威胁隔离相结合，以及许多其他功能。通过 `cron` 作业通过电子邮件每日接收摘要报告的能力，这对于确保检测系统按预期运行显然非常有用。`LMD` 接入 `Apache` 并直接监控文件上传的能力是我将要涉及的。如果这是用户将文件获取到系统的唯一方法，那么它显然是一个无懈可击的选择。

## 监控文件系统

观察变化的一种方法是使用 `notify`。不要担心，因为从 `2.6.13` 版本开始内核中已包含了 `notify`，因此大多数 `Linux` 构建都能正常工作。

复杂的 `notify` 可以实时监控单个文件或目录的更改，如果发现任何更改。捕获到某个用户发生了更改，`notify` 将其视为事件并立即报告。通过创建一个观察列表，`notify` 可以跟踪列表中的每个唯一项。虽然 `notify` 不会传递有关更改的文件或目录的详细信息，但对于大多数应用程序已经足够。如果 `notify` 不可用，通常需要通过轮询文件系统的方法手动运行。在检查网络文件系统的更改的情况下，任何配置软件将需要使用预定义的频率进行轮询。因为递归文件系统很难追踪。不幸的是，`notify` 可见 `/proc`、`sys` 和 `/dev/pts` 等伪系统。

## 安装

要在 `Debian` 和 `Red Hat` 上安装 `LMD`，首先我们将检查 `wget` 包是否安装。在 `Red Hat` 上：

```bash
# yum install
```

`Debian` 替代：

```bash
# apt-get install
```

许多发行版默认包含 `wget`，因此可能不需要它。要获取最新的 `LMD`，如果你想让 `LMD` 与 `notify` 直接交互，也可以安装 `inotify-tools`；你可以从 `https://github.com/linux-chat/inotify-tools/` 读取更多信息并下载 `inotify-tools`。

然而，如果你幸运地使用的是 `Red Hat`，可以通过软件包管理器安装它：

```bash
# yum install inotify-tools
```

对于 `Debian` 系，你应该能够运行以下命令：

```bash
# apt-get install inotify-tools
```

如果这在你的 `Debian` 版本上不起作用，请尝试以下步骤。我知道这可行，因为我想看看 `LMD` 在 `Ubuntu 14.04` 上安装有多简单。你需要将 `Universe` 仓库或成功地将 `inotify-tools` 包添加到 `/etc/apt/sources.list` 文件，如下：

```bash
deb http://archive.ubuntu.com/ubuntu trusty main
```

如果你运行其他版本，可以将 "trusty" 交换为 "precise" 或另一个 `Ubuntu` 版本。你可以使用以下命令更新软件包列表：

```bash
# apt-get update
```

然后，最后的 `Ubuntu` 命令将是：

```bash
# apt-get install inotify-tools
```

我将让你同样地实验 `Debian` 仓库（将 "trusty" 替换为你的 `Debian` 版本）。截至编写，软件包仓库中未找到 `LMD` 包，你可以按照以下方式下载并安装包：

```bash
# cd /usr/local/src/

# wget http://www.rfx.com/downloads/maldect-current.tar.gz

# tar -xzf maldetect-current.gz

# cd maldetect-*

# sh ./install.sh
```

一旦运行了 `install.sh` 脚本（如这些命令的最后一行所示），应该包含以下内容的输出：

```bash
Linux Malware Detect v1.5

(C) 2002-2015, RFX Networks <proj@rfx.org>

(C) 2015, Ryan Macdonald <ryan@example.com>
```

此程序可以根据 `GNU GPL` 的条款自由分发。

安装到 `/usr/local/maldect`
配置文件: `/usr/local/maldect/conf.maldect`
可执行文件: `/usr/local/maldect/maldect`
链接: `/usr/local/sbin/maldect`
链接: `/usr/local/sbin/lmd`
cron.daily: `/etc/cron.daily/maldect`
`maldect(6617): {signature}` 正在执行签名检查...
`maldect(6617): {signature}` 本地签名版本为 `201511202602`
`maldect(6617): {signature}` 最新签名集已安装

你的安装路径可能有所不同，或者如果你安装了 `install.sh` 脚本（特别是 `path` 变量）。你可以看到，你还会收到关于你的 `LMD` 签名更新的通知。

## 监控模式

现在你已经安装了包，让我们看看 `LMD` 在系统中可以为你监控哪些内容。一个很好的起点是考虑 `LMD` 的监控模式。

`LMD` 提供了多种监控模式，可以配置为检查文件系统的不同部分。正如你所看到的，`LMD` 使用一个名为 `Maldet` 的二进制执行文件，它是“malware detection”的缩写。

要监控系统组件，可以使用 `-m` 选项，也写为 `--monitor`。`LMD` 可以监控的内容可以细分为用户、文件和路径。网站给出了以下三种模式在命令行中可能性的示例：

```bash
# maldet --monitor users

# maldet --monitor /root/monitor_paths

# maldet --monitor /home/mike/home/ashton
```

通过使用第一个选项 `--monitor users`，`LMD` 将监控系统上大于最小 `UID` 设置的任何唯一标识 (`UID`)。可以在配置文件中设置的配置选项称为 `notify_minuid`。

第二个监控示例是一个文件，以换行分隔，其中可以包含你想监控的文件。在这种情况下，文件列表位于 `/root/monitor_paths` 文件。

对于第三种选项，你可能会通过添加一个逗号分隔的文件系统路径列表来创建一个非常长的命令行。

8.3 显示了运行以下命令的输出：

```bash
# maldet -m /home/ubuntu
```

## 第 8 章：恶意软件检测

### 图 8.3

当你要求 `LMD` 监控特定路径时你看到的内容

```bash
ubuntu maldetect-1.5 # maldetect -m /home/ubuntu

Linux Malware Detect v1.5

(C) 2002-2015, R-fx Networks <prooj@rfxn.com>

(C) 2015, Ryan McDonald <ryan@rfxn.com>

This program may be freely redistributed under the terms of the GPL v2
```

```bash
maldetect(16024): mon added /home/ubuntu to notify monitoring array

maldetect(16024): mon starting to monitor 1 paths, this might take awhile...
```



`maldetect(16024): mon notify startup successful (pid: 16723)`

`maldetect(16024): mon monitoring log: /usr/local/maldetect/logs/inotify_log`

`ubuntu maldetect-1.5 # $`

## 配置

LMD 的主配置文件是`/usr/local/maldetect/conf.maldetect`。它是为人知的，对于理解 LMD 偏好的设置方式很有帮助。

但在在你继续之前，有一个警告：LMD 配置文件不使用星号（`*`）作为通配符，而是使用问号（`?`）。因此，你应该使用`?`字符而不是`*`来替换配置选项中的多个字符。除了这个微小的注意事项外，整个过程相对顺畅。

## 排除

让我们看看如何设置 LMD。文档首先要求你考虑想要忽略的系统元素。与你刚刚看到的监控模式风格相似，你可以通过填充某些文件内容来实现这一目标。以下配置文件中的每个条目都应该单独占一行。

你可以将不想让 LMD 检查的文件路径添加到此文件中：`/usr/local/maldetect/ignore_paths`。

你也可以通过在该文件中输入类似`.jpg`的条目来排除特定的文件扩展名：`/usr/local/maldetect/ignore_file_ext`。

某些签名可能会由于某些原因导致不必要的且大量的日志条目和告警。你可以通过在此文件中添加签名（例如`php.mailer.10hack`）来禁用签名：`/usr/local/maldetect/ignore_sigs`。

最后一个选项意味着你可以使用复杂的正则表达式（`regex`）来同时匹配多个文件系统路径。你只需要将列表添加到文件`/usr/local/maldetect/ignore_notify`中，其格式如下：

```
^/home/premium-user-$
```

![](img/0de912db8d05f7607e7b5b15fbf73eaa_100_0.png)

显然，使用正则表达式`-b`后，文件匹配的可能性是无限的，它可以避免每当有新用户允许登录你的服务器时手动修改配置。这个正则表达式示例形象性地指出，你可以使用类似于`premium-user-123456`的用户名格式为一组特定的用户命名。

## 从命令行运行

LMD 的命令行界面（CLI）选项经过深思考虑，相对容易遵循。我会让你们去探索所有的选项，但现在现在将介绍一些关键选项。

正如我提到的，LMD 的可执行二进制文件名为`maldet`。让我们先从后台运行 LMD，让它检查特定的文件系统路径开始。你可以从文档中的示例看到如何在后台运行可能的大型扫描，使用：

```
# maldet -b -r /home/?/public_html 7
```

在这个示例中，`-b`用于后台扫描并检查过去七天内更改或修改的文件，通过附加字符`7`实现。该命令的语法和可选运行方式`--scan-recent PATH DAYS`。

## 报告

让我们看看 LMD 如何生成报告的。图 8.4 显示了一个生成的报告。

**图 8.4**

使用`maldet--report`命令生成的 LMD 扫描报告

```
HOST: ubuntu

SCAN ID: 151212-1648.17013

STARTED: Dec 12 2013 16:48:59 +0000

COMPLETED: Dec 12 2013 16:49:00 +0000

ELAPSED: 1s (find: 6m)

PATH:

/home/*/public_html

RANGE: 7 days

TOTAL FILES: 3

TOTAL HITS: 0

CLEANED: 0

============================

Linux Malware Detection v1.5 < proj@fxn.com >
```

要查询特定的报告，你需要一个`SCANID`。这是一个唯一的引用标识，可以在图 8.4 顶部看到，运行此命令可以给你提供最后一次运行 LMD 命令的报告：

```
# maldet --report
```

一旦你获取了 ID，你也可以按照如下方式手动将报告通过电子邮件发送给自己：

```
# maldet -e, --report SCANID chris@binnie.tld
```

（注：此处原文存在大量重复段落，译文已按要求保留逻辑并避免重复输出）

一旦你有了`SCANID`。这是一个唯一的引用标识，可以在图 8.4 顶部看到，运行此命令可以给你提供最后一次运行 LMD 命令的报告：

```
# maldet --report
```

## 隔离与清理

正如我从开始所说，更新 LMD 的签名至关重要。要手动运行更新，你使用`-u`命令。如果你好奇如何操作，请连接到`rfxn.com`网站以获取数据。尝试使用`-u`或其等效的`--update`如下：

```
# maldet -u
```

预期输出类似于：

```
maldet(19278): {sigup} performing signature update...

maldet(19278): {sigup} local signature set is version 2015112028632

maldet(19278): {sigup} latest signature set already installed
```

有一种更新当前安装版本的机制，同样来自`rfxn.com`，如下：

```
# maldet --update-ver
```

如果你愿意，这也可以被缩写为`-d`，此命令的结果可能如下：

```
maldet(19357): {update} checking for available updates...

maldet(19357): {update} hashing install files and checking against

server...

maldet(19357): {update} latest version already installed.
```

要使清理被视为成功，清理后的扫描必须在没有记录任何命中（HIT）的情况下通过。

如果你开始怀疑结果，或者不确定配置更改是否已被捕获，你可以使用以下命令清除所有的会话数据、日志和临时文件：

```
# maldet -p
```

结果应该类似于：

```
maldet(19219): {glob} logs and quarantine data cleared by user

request (-p)
```

## 扫描与停止扫描

在图 8.1 中，你看到了使用`-m`或`--monitor`选项监控特定路径的结果。让我们详细说明一下。

## 第 8 章：恶意软件检测

假设你想监控两个特定的文件系统分区，因为你的用户可能有在那里写入数据的能力。你可以按照以下方式监控路径：

```bash
# maldet -m /usr/local,/home
```

注意分隔路径的逗号。运行此命令的输出如图 8 所示。请记住，大型扫描可以使用`-b`后台选项，或者正如你之前看到的那样。

### 图 8

当 LMD 开始对启用通知（notify）的两个文件系统分区监控时你看到的内容

```text
ubuntu sess maldet -m /usr/local,/home

Linux Malware Detection v.5

(C) 2002-2015, R-fx Networks <proj@rfxn.com>

(C) 2015, Ryan McDonald <ryan@rfxn.com>

此程序可以根据 GNU GPL v2 的条款进行自由分发

maldet(20035): {mon} added /usr/local to notify monitoring array

maldet(20035): {mon} added /home to notify monitoring array

maldet(20035): {mon} initiating startup on 2 paths, this might take awhile...

maldet(20035): {mon} notify startup successful (pid: 20646)

maldet(20035): {mon} notify monitoring log: /usr/local/maldetect/logs/notify_log

ubuntu sess #
```

```bash
# maldet -a /home/?/uploads
```

在此示例中，你使用 LMD 扫描`uploads`目录（记住问号是 LMD 中的通配符字符，而不是星号）。

运行扫描命令后，你还会获得一个供以后参考的`SCANID`，格式为`(1 files) in progress...`

```text



`maldet(28566): {scan} scan of /home/*/uploads in maldet(28566): {scan} 1111/1111 files scanned: 0 hits 0 cleaned maldet(28566): {scan} scan completed on /home/*/uploads: files 1111, malware hits 0, cleaned hits 0, time 11s maldet(28566): {scan} scan report saved, to view run: maldet --report 151212-1724.28566`

如果你的任何扫描耗时超过了预期，`LMD` 也可以应对这种情况。终止开关或 `-k` 选项（也写为 `--kill`）将停止任何运行中的通知实例。如果机器负载过高或你认为某些程序运行不符合预期，那么这就是可用选项中一个非常有用的补充。

### Cron 任务

`LMD` 自带一个每日 cron 任务，位于 `/etc/cron.daily/maldet`。它将更新特征并清理扫描数据，使其保留十四天，或者按照你指定的配置进行每日扫描。

注意，会话数据和临时文件在 cron 任务之间是保留的。因此，如果你的结果不准确，你需要运行我之前提到的 `-p` 选项来清除这些文件。

你应该使用电子邮件配置参数以便在每天早上接收每日报告。每日更新对于邮件存档以及确保你的扫描每天进行且没有失败具有重要价值。

### 报告恶意软件

你已经看到 `LMD` 是多复杂且结构多精妙，因此 `LMD` 提供了一个简单的机制来上传可疑文件进行分析，这并不令人意外。如果它们被证明是未知种类的恶意软件，可能会创建新的特征并将其添加到 `LMD` 的已知威胁中，以便为其他用户识别恶意软件。将文件发送回 `LMD` 进行检查的方法是使用 `--checkout` 功能，它也写为 `-c` 选项。

```bash
# maldet -c suspicious_file.gz
```

当你执行此命令时，文件将提交到 `rfxn.com` 并在适当时候进行检查。

### Apache 集成

在本章稍早部分，我简要提到了 `LMD` 包含的一个巧妙功能。该功能是将 `LMD` 与 `Apache mod_security2` 模块集成的能力。`LMD` 文档解释说，它使用可变 Apache 模块的 `inspectFile` 功能，允许你运行验证脚本，该脚本可以判断上传是通过还是失败。例如，在你的 Apache 配置中，可能会看到如下来自文档的条目：

```apache
SecRequestBodyAccess On
SecRule FILES_TMPNAMES "@inspectFile /usr/local/maldetect/hookscan.sh"
"id:999999, log,auditlog, severity:2,phase:2,t:"
```

按照设计，用户上传的每个文件都可以被自动扫描，这应该显著减少系统上的威胁数量，特别是在许多用户频繁上传文件的情况下。

文档包含了关于默认选项中性能和准确性的详细信息。如果你对此功能感兴趣，我鼓励你查看带有的 `README` 文件以获取更多信息。

## 总结

除了查看 `LMD` 之外，我还提到了它用于实时检查文件系统变化的 `inotify` 机制。这种巧妙且高效的通知机制允许在不引入显著系统负载的情况下对恶意软件进行实时检查。

由于 `Android` 手机目前占全球市场的 80% 以上，毫无疑问对设备进行实时检查将变得至关重要。通过启用通知机制，你可以降低恶意软件感染的风险。

作为对比，你可以看看当我输入 16 位密码时会发生什么（顺便一下，我使用的是默认字符集，所以你看到的 10 位字符示例并不适用）。

## 第 9 章：密码破解

## 密钥空间

在密码学中理解密钥空间（keyspace）的概念是非常重要的。它松散地关系到密码破解工具必须付出的精力。

美国国家标准与技术研究院（NIST）将密钥空间描述为“密钥可能的所有值的总和”。密钥空间的一个组成部分是构成密钥的“字符集”。换句话说，你可以使用键盘上的可用字符。如果字符是从 0 到 9 的单个数字，那么密钥空间就是十。

你可以通过增加密码长度和字符集来增加密码的安全性。例如，一个长度为 16 位且使用 10 个字符集的密码，据报道拥有 10,000,000,000,000,000 个密钥空间，这比单个字符的 10 位密钥空间难攻击得多。

这个简单而复杂的网站使用基础术语，讨论的是可能的组合而非密钥空间。如果你点击输入框下的 `SHOW DETAILS` 链接，在输入密码后你将看到密码的安全性。例如，当我输入位长度的密码后出现了以下输出：

```text
Length 1 characters
Character Combinations 10
Calculations Per Second 4 billion
Possible Combinations 10
```

## 第 9 章：使用 Hashcat 破解密码

我输入的密码是大写字母、小写字母、数字和特殊字符的组合，如下：

```
Rx951&RTdip-2YT
```

在这种情况下，网站返回的破解时间非常“体面”，长达 412 万亿年。如如下输出所示，其中包含了一些新词汇（`for`, `at least`）。显然，`nonillion` 一词在美国是指数字后面跟着 30 个 0，在英国则指跟着 54 个 0。

```
Length 16 characters
Character Combinations 96
Calculations Per Second 4 billion
Possible Combinations 52 nonillion
```

从这个例子中，你可以清楚地推断出，标准的 8 位“复杂”密码比简单的单字符密码要好得多。

## 哈希值 (Hashes)

现在我已经涵盖了复杂密码如何极大增加攻击难度，接下来我将继续关于密码破解的讨论。不过，先给出一个解释。

顾其名，`Hashcat` 处理的是密码哈希。在密码学中，创建哈希涉及将字符字符串（如密码）转换为一组字符，其结果类似于指纹。没有任何办法可以撤销或反转哈希（嗯，更准确地说，在现实中这真的非常、非常困难）。

这里是两个 `MD5` 哈希值，第一个是单词“hello”的哈希：

```
5d1402abc4b2a76b971d9311017c592
```

第二个，大写字母“Hello”的 `MD5` 哈希是：

```
81aa9953c46112964a827abf8c47804d7
```

你可以看到，仅仅一个大写字母就产生了巨大的差异。

如果你使用另一个单词“Hello There”，你会得到：

```
32b170d923b654360f351267bf44045
```

你的 `MD5` 哈希长度与之前包含单个单词的示例相同。通过知道你的哈希值总是相同的长度，你可以判断一段看似无关的字符字符串是否符合某种标准。

此外，思考一下为什么你不会在 Linux 服务器上加密密码，并在用户登录时解密系统的密码文件。答案仅仅是因为加密数据的过程是可以被反转的，单向函数比加密密码更好。有些人读到这里会惊讶，`/etc/shadow` 文件完全不记得用户的密码，只是它的加盐哈希（`salted-hash`）版本。

为什么 Linux 上 `/etc/shadow` 文件中的条目看起来像这样？一眼看上去是某种加密。

```
chrisbinnie:$6STRYWb5$6efTm54cpV2YnC6f20b7w/
5nv8pz5FqgtWFcw3G2pKkkGsfCtWezWhWykFgrfFGMCde4HW/
12231:3|11:32::
```



用户 `chrisbinnie` 的条目长得多，是因为 `Shadow Suite` 使用了盐（salt）来增强密码强度。在用户于 `Linux` 系统输入密码后，默认会使用盐。

例如，在 `Linux` 的 `crypt` 包中，这是一个从字符集中选出的两个字符的字符串。它们可以是我的英语字符集中的任何字符（`a-z`, `A-Z`, `0-9/`）。有了盐，用于哈希用户密码的原始哈希会在 `4096` 种方式中的一种被“扰动”。盐被保存到编码后的密码中。

让我们多想一下 `Linux` 密码。现代 `Linux` 系统通过 `Shadow` 密码增强了密码安全性。以前，密码存储在 `/etc/passwd` 文件中，系统上的每个用户都可以读取。然而，只有 `root` 可以读取 `/etc/shadow` 文件，这允许执行其他策略，例如密码老化策略。

攻击密码列表的一种常见方法是提前知道许多常用密码的哈希值，并将它们与所有 `4096` 个可用的盐值相结合。这被称为字典攻击。

有人说，如今一个安全密码系统的最低规范应该包含最新的哈希算法，并且生成的哈希值必须经过加盐处理。流行的现代哈希算法包括 `SHA256`、`SHA512`、`whirlpool`、`tiger`、`ripemd` 和 `SHA3`。每种算法都有细微不同的属性。

这些算法不应与 `3DES`、`Triple DES`、`Crypt`、`Blowfish` 和 `Rijndael` 等加密算法混淆。

## 使用 Hashcat

设计良好且易于使用的 `Hashcat` 附带了大量的示例哈希和字典列表以供实验。让我们看看如何使用它们。

### Hashcat 功能

密码破解工具的通用方法往往是导入一个充满加密数据的密码文件，然后生成一个输入文件已处理过的输出文件。让我们看看 `Hashcat` 工具可用的一些选项。稍后我将提到你软件中提供的其他一些工具。

`Hashcat` 支持许多不同类型的哈希算法，例如 `MD5`、`SHA1` 和 `NTLM`。事实上，如果我没有数错，种类超过了惊人的 `90` 种。`Hashcat` 声称它可以破解热门应用程序（如 `WordPress` 和 `Cisco-ASA`）以及 `Drupal7` 密码的 `MD5` 版本。除了令人印象的算法支持外，还提供了许多不同的攻击模式，包括暴力破解、字典攻击、基于规则的攻击和指纹攻击。

### 安装

编写此时，`Hashcat` 的当前版本是 `v2.00`。要安装 `Hashcat`（假设无法在你发行版的仓库中找到它），你可以前往网站下载最新的二进制文件。`v2.00` 的直接链接是：`https://hashcat.net/files/hashcat-v2.00.7z`。

版本 `2.00` 的链接在 `https://hashcat.net/hashcat/` 网页的顶部可见。你应该检查此页面以确保下载的是最新版本。

下载完成后，只需解压 `.7z` 文件，并确保你有正确的权限向解压到的目录写入文件。如果你在 `Debian` 衍生版上解压遇到困难，可以使用以下命令安装 `7za` 包：

```
# apt-install p7zip-full
```

在 `Red Hat` 衍生版上，你可能需要添加仓库。完成后，以下命令可能会对你有效：

```
# yum install p7zip p7zip-plugins
```

接下来，运行 `7za` 文件来解压压缩文件并使用 `x` 保留目录结构：

```
# 7za x hashcat-2.00.7z
```

注意 `x` 前面没有减号，这是通常的惯例。这不是拼写错误。

完成后，你现在可以进入新创建的 `hashcat-2.00/` 目录，其中包含许多文件和子目录。特别感兴趣的是 `docs` 和 `examples` 目录，你可以尽情探索它们。不要担心，稍后你就能运行 `Hashcat` 可执行文件了。

顺便一下，如果你对最新的开发版本感兴趣，在 `GitHub` 上有一个页面：`https://github.com/hashcat/hashcat`。它还包含了文档和指向 `wiki` 的链接，这些应该会让你感兴趣。

如果你正在运行复杂的渗透测试套件 `Kali Linux`，那么你应该能够安装 `Hashcat`，因为它是内置的：

```
# apt-get install hashcat
```

## 哈希值识别

在使用 `Hashcat` 之前，有几点需要考虑。首先，你需要知道要从中恢复密码的哈希类型。

让我们思考一下 `Linux` 用户密码。默认哈希算法随时间推移而变化，并且取决于发行版。过去常见的默认值是 `MD5` 和 `DES`，但现在 `SHA512` 已不再。

如果你能识别出正在攻击的哈希类型，对 `Hashcat` 有帮助。你可以运行以下命令来发现正在使用的哈希算法：

```
# authconfig --test | grep hash
```

如果你担心机器的安全性并想升级机器 `Shadow` 密码使用的哈希算法，可以使用以下命令：

```
# authconfig --passalgo=sha512 --update
```

在这个例子中，你可以根据需要将 `sha512` 替换为 `sha256`。然而，为了让这一更改生效，你需要让用户更改他们的密码。

## 第 9 章：使用 Hashcat 破解密码

因此，它们被转换为新的哈希类型。你可以使用以下命令使用户的密码过期，强制用户在下次登录时更改密码：

```
# chage -d 0 chrisbinsinnie
```

此示例中的“change age”（更改年龄）命令将过期日期推到了 `1970` 年 `1` 月 `1` 日，这确保它始终早于系统时钟的当前设置。

让我们再次查看用户 `chrisbinsinnie` 的 `/etc/shadow` 条目：

```
chrisbinsinnie:$6STRIWb51$f6Tm54gpV2YCn6f2b7w/
5nv82psajFqTewx7FCeW3l1G2pkKasKgf1CtWhOPWykFkGrpFGcmde4HW/
:12231:3:32:
```

你不需要使用 `authconfig` 命令来确定该条目使用的是 `SHA512` 哈希。你可以参考表 9.1。

### 表 9.1 如何识别哈希算法

| 符号 | 哈希算法 |
|---|---|
| `$0` | `DES` |
| `$1` | `MD5` |
| `$2` | `Blowfish` |
| `$2A` | `Eksblowfish` |
| `$5` | `SHA256` |
| `$6` | `SHA512` |

在 `Shadow` 示例中，在用户名之后紧跟两个美元符号之间有三个字符：`$$$`。从表 9.1 可以看出，`/etc/shadow` 中的密码是 `SHA512`。这是一个好消息，因为它是一种强效的算法。

密码条目的下一个部分（即 `$6` 之后且到下一个美元符号之前的内容）是盐值（salt）。在本文情况下，盐值是 `TRIYWb51`。

密码（使用盐值加密）是美元符号之后到第一列之前的下一个部分。之后，冒号之间的其他设置为系统提供了一些相关信息，例如用户密码何时过期、最后一次更改的时间等。

为了衡量更强力算法最近被使用的频率，请考虑这一点：根据 `Fedora` 的说法，从 `Fedora 8` 开始，`glibc` 包就支持了 `SHA256` 和 `SHA512` 哈希。因此，从 `Fedora 9` 开始，已经可以使用 `SHA256` 和 `SHA512` 来处理密码。

如果你卡住了，可以查看网站 `http://verifier.insidepro.com` 来确定你想让 `Hashcat` 指向哪种哈希变体。我在这里使用的示例哈希上成功有限，因为它们是使用另一个网站的工具生成的，所以注意，识别未知类型的哈希算法可能需要一些时间。

如果有用，请尝试运行以下命令来生成一个带有盐值的 `MD5` 密码（你需要安装 `openssl`）：

从运行该命令的结果中，注意 `$1` 和 `123` 在加密后的密码处于什么位置。

我有时也会运行类似这样的 `MD5` 哈希测试（不带盐值）：

```
# echo PASSWORD | md5sum

b804be229e11c290efdcd8190a92261
```



# 第 9 章：使用 Hashcat 破解密码

手动生成密码的其他方法可以在`http://unix.stackexchange.com/questions/81240/manually-generate-password-for-etc-shadow`找到。

## 选择攻击模式

现在你已经理解了哈希的工作原理，让我们继续前进。即使你知道正在处理的哈希类型，你仍然需要考虑如何攻击你所获得的任何加密密码。

我提到过一种称为暴力攻击（`brute attack`）的常见攻击模式。这些攻击针对字符，至少会使用美国和英国字符集，并包含`a-z`、`A-Z`、`0-9`。

另一种流行的攻击模式是使用字典列表（`wordlists`）。在`Hashcat`中，这将通过预定义的列表进行。

另一种更复杂的字典列表方法是使用规则（`rules`）。在`Hashcat`中，这将通过自定义规则进行。

## 下载字典列表

如果你想获取字典列表，可以访问[http://verifier.insidepro.com](http://verifier.insidepro.com)来确定你想让`Hashcat`指向哪种哈希变体。

一旦你掌握了示例，就可以尝试对自己的`/etc/shadow`哈希值进行操作。如果你足够幸运，在运行调整后的命令后，你应该看到一个或多个哈希值以及其对应的明文密码。如果你没有获得足够的提示，请不断实验直到你对结果满意。为了让程序按预期运行，可能需要一些尝试错误：我建议先熟悉这些综合示例。如果你感到困难，请记住，并不是所有密码都能在瞬间被破解的。

尽管如此，一旦你理解了理论并尝试了它的基本功能，`Hashcat`的操作其实非常简单。从 Linux 系统管理员的角度来看，这应该是你关注的，你应该关注服务器使用的哈希算法。

我有很多选项留给你自行选择。例如，与示例命令对齐的运行规则选项就是`-r rules/specific_rule.rule`。

我向你保证你会查看一些相应的哈希值和攻击模式。哈希值的数量太多，无法一一列出，但`Hashcat`网站在`http://hashcat.net/wiki/doku.php?id=example_hashes`提供了这些内容以及实用的说明。

你可以使用的某些攻击模式（被称为“直译”，换句话说，与字典或单词列表进行匹配）在表 9.2 中，并附有相应的编号。

## 表格 9.2 Hashcat 攻击模式及其对应编号

| 编号 | 攻击模式描述 |
|---|---|
| 0 | 直译（字典和单词列表） |
| 1 | 组合（`Combination`） |
| 3 | 暴力破解（作为掩码攻击的一部分运行） |
| 6 | 混合（`Hybrid`） |

让我们简要查看暴力破解与你之前看到的字典攻击之间的区别。

两者的主要区别在于，暴力破解会遍历密钥空间以寻找密码匹配。然而，字典攻击的范围有限。因此，字典攻击的速度要快得多，但当然，它们很有可能无法破解输入的加盐哈希（`salted hashes`）。不过，至少你能迅速察觉到这种模式下的任何失败。

这与暴力破解恰相反，暴力破解会一直运行（可能持续非常、非常久），直到成功破解密码。请大家放心，只要配置设置正确，你终会在某个时刻获得密码，即使这需要一百的时间。

在`Hashcat`详细的在线文档中，提到暴力破解是一种较旧、更复杂的发现密码的路径。`Hashcat`现在将暴力破解风格的攻击（你可能在表 9.2 中注意到它）包含在它的掩码攻击（`mask attack`）中。

掩码攻击的主要原理是缩小密钥空间的大小，从而提高运行速度。文档提供的一个示例是，通过`Hashcat`的创新技术，你可以将密码“`Julia1984`”的恢复时间从大约四年缩短到惊人的几分钟。

文档指出，运行掩码攻击相比于暴力破解没有劣势，这令人鼓舞。你通过在标准命令末尾添加掩码来运行掩码攻击，如下所示：

```bash
# hashcat -m 1800 -a 0 -o discovered_passwords.txt --remove hashes.wordlist.txt -1 ?abcdef
```

在这种情况下，后添加的`-1 ?abcdef`要求`Hashcat`遍历字符`0123456789abcdef`。

根据文档，该掩码`-1 ?l?d?u`同样提供了一个完整的 7 位 ASCII 字符集，作为字母-数字-全集。选项如`?l`（代表从`a`到`z`的小写字母）和`?u`（代表从`A`到`Z`的所有大写字母）。

你可以在`https://hashcat.net/wiki/doku.php?id=mask_attack`找到更多关于掩码攻击的细节。

## oclHashcat

使用`oclHashcat`和`Hashcat`需要非常相似的知识，因为它们的操作方式几乎相同。尽管它们存在一些差异——例如，`oclHashcat`加载字典的方式与`Hashcat`相比——如果你切换到使用`oclHashcat`，可以预期将有一个平缓的学习曲线。

此外，正如我已经提到的，必要的密码破解计算是系统中一个完全不同的组件。简单来说，`oclHashcat`与显卡协同工作，而不是 CPU。有两个软件版本可供区分，每种都适用于流行的 GPU：

- `cudaHashcat`，用于 Nvidia 显卡
- `oclHashcat`，适用于 AMD 显卡

在设置正确的情况下，GPU 的运行速度比 CPU 快得多，因为它们专门设计用于快速处理数字计算，通常用于处理图形。虽然它们本身显然是为了速度设计的，但在性能方面，CPU 会被其额外的、包含性的功能集分散注意力，导致吞吐量下降。因此，GPU 是处理可以更好优化的海量数据的选择。还可以通过将它们连接成链链来几乎无缝地扩展 GPU 输出，从而更容易地利用它们的组合力量。为了让你对 GPU 的速度有多快有个直观感受，如果你使用彩虹表和密钥空间（美国键盘上可用 95 个字符），你每秒可能进行 10 万亿次明文测试！

# 第 10 章：SQL 注入攻击

由于在服务器端脚本编写上不够严谨，他们沦陷了钓鱼攻击。从 2000 年代中期开始，在短短几年内，美国联邦调查局（FBI）曾多次与我们联系，一次是一家银行，另一次是一家白帽安全服务，告知我们某个客户服务器被黑入。因此，即使在这样一个小组织中，一个热门拍卖网站的虚假副本和两个网站也被克隆，并在极短时间内对我们的网络发起了钓鱼攻击。显然，`SQLi`攻击正在那些心怀不轨的人员之间流行。

针对这种常见的安全威胁，系统管理员和开发者注意到了这一点并开始加固代码。我记得在那段时间，我在一个基于`PHP`的网站上对每个用户输入组件谨慎地进行特殊字符转义，以避免`SQLi`攻击。

## 基础 SQLi

正如我之前提到的，`SQLi`的核心原理是从数据库中非法地检索代码或向数据库中注入代码。

为了避免这些问题，你不能再通过服务器端语言向外部暴露查询，这可能会导致你的网站不再流畅且无用。如果无法做到，你可以确保攻击向量被覆盖。实现这一点的最简单方法是过滤从访问者那里接收的所有输入。换句话说，在你网站上用户可以输入数据的每一个点，都需要在代码中采取相应的预防措施。在数据发送到数据库之前，将输入解析为易于处理的格式。

关于如何保护代码的完整教程可以留到另一天再说。不过，我将使用一种流行的编程语言为你进行快速复习。在此之前，我会提醒你一些关于`SQLi`如何运作的简单示例。

正如我所说，仅仅篡改网站远不是拦截的 SQL 可能造成的唯一损害。考虑下面这个`SQLi`语句例如：

```sql
sql-server> DROP TABLE special-offers;
```

通过了解这些名称，你还没有提到从数据库中提取用户名和密码。由于有犯罪意图，成功的`SQLi`攻击无疑是值得追求的奖品。许多大型品牌已陷于防守不严的代码和`SQLi`。反复出现的雅虎、Adobe、LinkedIn 和 Sony Music 可能都将列在受害者的长长名单中。当然，作为攻击者之一，或者作为必须恢复受此类攻击影响的节点的工作人员，我只能推测这些攻击涉及`SQLi`的种程度。`SQLi`耻辱柱可以在`http://codecurdmgeon.com/wp/sql-injection-hall-of-shame/`找到。虽然列表可能不完全准确，但我确定你会同意这是一篇引人入胜的读。

刚才我提到了一种编程语言。我将使用世界上最流行的服务器端脚本语言`PHP`的报告作为示例，快速演示 SQL 是如何工作的。强大的`PHP`不仅被直接用于数百万个网站，还用于世界上最流行的内容管理系统（CMS）`WordPress`（`https://wordpress.com`）以及许多其他动态网站应用程序，如`Joomla!`（`https://www.joomla.org`）。简而言之，`PHP`遍布网络，如果被发现，它就是攻击者的易受目标。

让我们看另一个例子，`PHP`中的这段代码：

```php
$input = $variable[3];
```



`$query = "SELECT id, item, price FROM specialoffers ORDER BY id LIMIT 15 OFFSET " . $input;`

```

观察第一行，你可以看到你没有过滤名为`$input`的变量。这意味着该变量在SQL语句的某行中使用，它可能包含攻击者想要使用的任何代码。随着经过构造的注入被注入，会引起各种混乱。

另一个例子是更新管理员的密码。例如，一个正常的SQL语句PHP代码可能像这样：

```php
$query = "UPDATE credentials SET passwd='$password' WHERE userid='$id';";
```

通过向此语句附加SQL，例如像`'sysop%'`这样的用户，你的SQL变得非常不严格，让数据库搜索类似于`sysop`的其他用户名，然后更新它们的密码。

遗憾的是，还可能在SQL中包含执行shell命令。

## 在 PHP 中缓解 SQLi

正如我所说，这个主题太大，无法详细介绍，但我将简要介绍如何过滤输入来缓解SQLi攻击。多种PHP函数可以帮助你完成这一任务。在写作期间，PHP从`5.6`版本重大移动到了`7.0`。旧版本（到`5.3`）中，你的主配置文件（`php.ini`）可以通过魔法引号（`magic quotes`）过滤所有输入。这显然被废弃了因为它过度依赖它。

为了保护第一个示例中的变量，你可能想通过`addslashes`运行用户输入。示例如下：

```php
$input = addslashes($variable);
```

使用`mysqli`，它可能像这样：

```php
$input = mysqli_real_escape_string($variable);
```

为了防止不受欢迎的输入，还有`trim`用于从变量中移除空格，与`strip_tags`以相同的方式用于HTML和其他标记。这些都可以链在一起，例如：

```php
$input = strip_tags(trim($input));
```

除了PHP`5.5.0`版本，你可以使用`mysql_real_escape_string`函数来清理你的字符串：

```php
$input = mysql_real_escape_string($input);
```

然而，从`7.0.0`开始，几乎总是想要使用`mysqli`驱动（改进后的`MySQL`）来对抗SQLi。益于此增强，你可以使用更高级的方法剥离执行代码中不必要的且危险的字符。使用`mysqli`的示例与之前的不同：

```php
$input = mysqli_real_escape_string($input);
```

使用`mysqli`通过以下方法连接到数据库：

```php
$mysqli = new mysqli("localhost", "userid", "DB_Name");
```

缓解SQL攻击的另一种方法是使用预处理语句（prepared statements）。这种安全添加背后的思想是数据库引擎完全处理任何使用的参数。在这种理论下，攻击者无法向他们创建的查询注入代码。示例如下：

```php
$input = $mysqli->prepare("INSERT INTO table_name (column_name) VALUES (?)");

$input->bind_param("s", $actual_user_input);

$input->execute();

$input->close();
```

额外的帮助是这种函数只需要读取一次，所以如果在几个页面上使用多次，PHP引擎的工作就更少。

另一种方法自PHP早期版本起可用并使用PHP Data Objects (`PDO`)。这里有一个好的讨论：`https://stackoverflow.com/questions/60174/how-can-i-prevent-sql-injection-in-php`。

哪种方法最好，但`PDO`看起来非常流行。`PDO`的示例看起来如下：

```php
$input = $pdo->prepare('SELECT * FROM special_offers_table WHERE offerer = :name');

$input->execute(array('name' => $variable));
```

关于`PDO`有很好的信息位于`http://whatever.com/blog/2014/08/28/the-heart-of-darkness/`。值得一读，仅仅是为了帮助你在PHP后期版本（`7.0.0`及以后）中选择方法来对抗SQLi注入。

## 利用 SQL 漏洞

现在你已经查看了几种防御SQLi的方法，你将学习黑客可能如何攻击你的在线服务。有很多可用工具，我将关注`sqlmap` (`http://sqlmap.org`)，它是黑客、法医科学家和渗透测试人员中一种流行的开源工具。使用这种复杂的工具可能会造成混乱，因此请确保你完全意识到在自己的服务器上测试它时可能造成的损害，更不用说属于别人的服务器了。我绝对建议使用开发服务器或沙箱虚拟机以确保安全。

`sqlmap`广泛的能力让大多数反对者担心。根据其网站，`sqlmap`支持以下数据库服务器：`MySQL`, `Oracle`, `PostgreSQL`, `SQL Server`, `Microsoft Access`, `IBM DB2`, `Firebird`, `Sybase`, `SAP DBD`和`HQDB`。

让我们看看如何安装`sqlmap`。它包含在`Kali Linux`等某些安全发行版中，但如果它不在你的包管理器仓库，还有其他的安装方法。

你可以使用`Git`命令使用`GitHub`上的`sqlmap`仓库：

```bash
$ git clone https://github.com/sqlmapproject/sqlmap.git sqlmap-dev
```

从`https://github.com/sqlmapproject/sqlmap/zipball/master`还有一个Zip文件可用。

`![](img/0de912db8d05f7607e7b5b15fbf73eaa_125_0.png)`

## 第 10 章：SQL 注入攻击

你也可以从`https://github.com/sqlmapproject/sqlmap/tarball/master`下载tar包。

一旦你按照安装说明完成操作，应该能够进入运行以下命令的阶段（在运行之前的`Git`命令后，这就是你入门需要做的全部工作）：

```bash
# cd sqlmap-dev

# python ./sqlmap.py -h
```

此命令将为你提供一个选项列表。

## 启动攻击

现在让我们来看看`sqlmap`功能的核心，即攻破远程机器。

但请注意，测试你的`sqlmap`技能最耗时的方面可能是搭建你自己的易受测试服务器，或者合规地识别易受攻击的网站。你可能会对读这些内容感到惊讶，因为由于URL的构造方式，`Google`可以很容易地识别漏洞网站。希望不言而喻，我不提倡攻击通过`Google`或任何其他方法发现的任何网站。不过，为了假设可能被利用的URL，你可以输入如`inurl:website.php?id=`或`inurl:product.php?id=`这样的查询语句。第一个搜索词返回了令人担忧的`170`万条结果。

通过`Google`不专业地暴露漏洞的网站和其他在线资源获得了一个绰号——`Geogledords`（谷歌搜索出的漏洞）。有一个网站列出了其中许多站点；值得一看，可以在`www.hackersforarchy.org/ghdb/`找到。这些列表包含了许多可能的机密登录页面、敏感目录以及提到用户名的文件。请负责地使用这些信息。

顺便提一下，你可以通过`Python`运行`sqlmap`，这意味着你需要在机器上安装某种类型的`Python`实现版本。

在`10.1`节中你可以看到开发者们非常希望与非法活动保持距离。这种强大的工具总是容易被滥用。

让我们继续。看看下面的示例，使用`sqlmap`命令所需的语法非常简单：

```bash
# python sqlmap.py -u "http://www.a-vulnerable-website.com/product.php?id=1111"
```

## 图 10.1

启动`sqlmap`时的界面，包含所有权声明

```
sqlmap-dev # python sqlmap.py -u "http://www.a-vulnerable-website.com/product.php?id=1111"

(1.0-dev-aee7d3)

****** http://sqlmap.org

[i] 法律声明：未经事先许可使用 sqlmap 攻击目标是违法的。用户有责任遵守任何相关的当地、州和联邦法律。开发者不承担责任，且不对本程序的任何误用负责

[*] 启动于 16:02

[INFO] 正在测试与目标 URL 的连接
```



`[16:02:31] WARNING：连接目标 URL 或代理超时；sqlmap 将重试请求`

`[16:02:32] WARNING：如果问题阻止了检查，请确认提供的目标 URL 是否有效。如果发生这种情况，请尝试开启 --random-agent 切换或切换代理 (--ignore-proxy) 后重试。`

如果你正在使用慢速连接或遇到远程数据库服务器响应缓慢的情况，可以在命令中添加 `--time-sec 10` 来引入更真实的超时设置。与直觉相反的是，这实际上可以加快整个过程。

现在有条理地执行几个简单命令。你可以选择使用 `sqlmap` 将这些所有命令链在一起。

我的 `sqlmap` 示例包含了 `-u` 选项，在声明 `URL` 时使用。该命令将通过多种 `SQL` 注入测试对尾随参数（`id=1111`）进行漏洞检查。在那里，`sqlmap` 通常可以检测到数据库服务器版本、远程操作系统以及正在使用的数据库服务器版本。

如果你想学习网络查询中使用的数据库名称怎么办？你可以通过如下添加 `--dbs` 选项来实现：

```
# sqlmap.py -u "http://www.a-vulnerable-website.com/php?id=1111" --dbs
```

在获取有用信息后，你的下一步是发现正在使用的表名。你可以通过将你的数据库名称替换为`<database-name>` 条目来实现：

```
# sqlmap.py -u "http://www.a-vulnerable-website.com/php?id=1111" --tables -D <database-name>
```



## 第 10 章：SQL 注入攻击

该过程的最后一步是从中提取所有数据。如果你是开发者或管理员，并且你不担心这一点，那么你绝对应该担心。

再次，请负责任地使用这些技能。与其攻击他人的基础设施，不如妥善地保护自己的基础设施要满足得多。

## 索引

## A
- `ACLs` (访问控制列表), 34
- `admin`: 禁止的错误, 60
- `AIDE` (高级入侵检测环境), 13
- `amplication` (放大攻击), 39
- `MITM` 攻击 (中间人攻击), 66
- `Apache`, `LMD` 集成, 96–97
- `ARP` (地址解析协议), `ping` 与, 53
- 攻击
  - 数字化攻击地图工具, 45–46
  - 爱沙尼亚 `DDoS` 攻击, 45–46
  - 加固与, 65–67
  - 映射, 45–46
- `MITM` (中间人), 66
- 密码破解, 106
- 字典列表, 106–107
- 钓鱼攻击, 113
- 死亡之包 (`Ping` of `Death`), 66
- 反射, 38–40
- `SNMP`, 41
- 报告, 40–41
- `smurf` (蓝精灵攻击), 66
- `SQLi` (`SQL` 注入), 113–114
- `unching` (解除限制), 118–120
- `auth` 类别 (`NSE`), 74
- 认证, `NSE`, 77–78
- `clone` 命令, 117–118
- `cmd_timeout`, 6
- `CMS` (内容管理系统), 115
- 命令
  - 链式, 30–31
  - `--clean`, 93–94
  - `clone`, 117–118
  - `contrack`, 8
  - `hashcat`, 108–109
  - `iptables`, 61–63
  - `--kill`, 96
  - `knock`, 7
- `md5sum`, 14
- 通信, `netcat`, 31–33
- `conrack` 命令, 8
- `cron` 任务, `LMD`, 96
- 密码学
  - 哈希值, 101–102
  - 密钥空间, 100–101
  - `cudaHashcat`, 110

## B
- `BPC` 38 (当前最佳实践 38), 43
- `broadcast` 类别 (`NSE`), 74
- `bruce` 类别 (`NSE`), 74

## C
- `CAPT` (捕获包条目), 57
- `netcat` 中的链式命令, 30–31
- `CIDR` (无类域间路由), 51
- `--clean` 命令, 93–94
- `CLI` (命令行界面), 运行 `LMD`, 92

## D
- `DDoS` (分布式拒绝服务) 攻击, 37
- `Debian` `Jessie`, 配置文件, 3
- `default` 类别 (`NSE`), 74
- 数字化攻击地图工具, 45–46
- `discovery` 类别 (`NSE`), 74, 78–79
- `DNS` (域名系统), 37
  - 解析器, 62–63
- `dos` 类别 (`NSE`), 74
- `DRARP` (动态 `RARP`), 53
- `drop response` (丢弃响应), 2

## E
- `Echo Mode`, `Niny`, 54–57
- 爱沙尼亚 `DDoS` 攻击, 44–45
- 可执行文件, 33–34
- `exploit` 类别 (`NSE`), 74
- `external` 类别 (`NSE`), 74

## F
- 文件传输, `netcat`, 29-30
- 文件系统
  - `knocked`, 4
  - `LMD` 监控, 88
  - 安全, 13
- 过滤器 (`Filters`), 2
- 清空 `iptables` 规则, 65
- `fuzzer` 类别 (`NSE`), 74
- `iptables`, 2
  - 清空规则, 65
  - `iptables` 命令, 61-63
- `iptables-persistent` 软件包, 9
  - 规则, 9-10
  - 测试, 8-9

## G
- `GitHub`, `clone` 命令, 117–118
- `GUIs` (图形用户界面), `NSE`, 81

## K
- 密钥空间, 100–101
- `--kill` 命令, 96
- `knock` 命令, 7
  - 配置, 5-6
  - 默认设置, 3-4
  - 文件系统, 位置, 4
  - 安装, 2-4
  - 测试, 6-7
  - 网络接口, 默认, 5
  - 软件包, 3
  - 数据包, 5-6
  - 死亡之包, 38

## H
- 加固, `ICMP` 广播, 65
- `Hashcat`, 99
- 暴力破解攻击, 110
  - 能力, 103
  - `cudaHashlist`, 110
  - 哈希值, 101-103
  - 识别, 104-105
  - 安装, 103
  - 运行, 107–110
  - 影子密码, 104
  - `hashcat` 命令, 108–109
  - `hashcat-util`, 111
  - 算法, 15
  - `host` 脚本 (`NSE`), 80
  - 基于主机入侵检测, 13

## L
- `LMD` (`Linux` 恶意软件检测), 85
  - `--limit-burst` 选项, 66
  - `--clean` 命令, 93–94
  - `CLI` 选项, 92
  - `cron` 任务, 96
  - 排除, 91–92
  - `inotify-tools`, 89
  - `--kill` 命令, 96
  - `maldet`, 92
  - `Malware Registry` (恶意软件注册表项), 86
  - 监控, 模式, 90-91
  - 隔离, 93–94
  - 扫描, 94
  - 手动, 95
  - 停止, 94–96
  - 威胁, 86–87
  - 入站连接日志, 64–65
  - `--log-prefix` 选项, 62–63

## I
- `ICMP` 码, 61
  - `iptables` 与, 61-63
- `ICMP` 端口不可达 (`Port Unreachable`), 2
- `icmp_ignore_broadcasts`, 65
- 入站连接日志, 64–65
- `inotify-tools`, 89
- `intrusive` 类别 (`NSE`), 75
  - 服务器的脆弱性, 7-8

## M
- `maldet`, 92
- `malware` 类别 (`NSE`), 75
- 映射攻击, 45–46
- `md5sum` 命令, 14
- `MD5sums`, 14-16
- `MTM` (中间人) 攻击, 蓝精灵攻击, 66
- `MTU` (最大传输单元), 59

## N
- `NAT` (网络地址翻译), 54–57
- `netcat`, 26
  - 链式命令, 30-31
  - 安装软件包, 27–29
  - 通信安全, 31–33
  - 可执行文件, 33–34
  - 文件传输, 29–30
  - 选项, 34–35
  - `netcat-opensnd`, 27
  - `netcat-traditional`, 27
- `Netfilter`, 2
- `Nmap`, 1, 27–28
  - `Debian` 安装, 69
  - 端口扫描, 69–71
  - `Red Hat` 安装, 69
  - `nmap`, 27
  - `Nmap` 项目, 25
- `ping`, 49–50
  - `ARP` 与, 53
    - `--debug`, 58
    - `--delay`, 10, 57
    - `Echo Mode`, 54–57
    - `--hide-sent`, 52–53
    - `--ICMP` 与, 23–54
    - `mylocal` 与, 23–54
      - `--rate`, 3–57
  - `TCP` 与, 50
    - 解释, 51
    - `ddp` 与, 52
- `NSE` (`Nmap` 脚本引擎), 71–73
  - 认证检查, 77–78
  - 准则, 75
  - 发现, 78–79
  - `GUIs`, 81
  - `regex` (正则表达式), 80–81
  - 脚本
    - 分类, 74–75
    - `host`, 80
    - 态势, 80
    - 可修剪, 80
    - 服务, 80
    - 更新, 79–80
    - 安全问题, 75–77
    - 计时模板, 73
  - `Zenmap`, 81–82
- `NTP` (网络时间协议), 37
- 反射攻击, 38–40
- `RestrictedAccess` 服务器, 37–38

## 0
- `ocHashcat`, 110–111
- `Open Source Tripwire` (开源丝线), 13
- `OpenAccess` 服务器, 37–38

## P
- 软件包
  - `iptables-persistent`, 9
  - `knocked`, 3
  - 数据包, `knock`, 5–6
  - 密码破解, 99
- 攻击
  - `Hash` 数量, 109
  - 模式, 106
  - 字典列表, 106–107
  - 哈希值, 101–103
- 密钥空间, 100–101
- 安全性, 100
- 影子密码, 102–103
- `Shadow Suite`, 102
- `PDO` (数据对象), 17
- 钓鱼攻击, 113
- 死亡之包, 66
- `ping` 允许 `IP` 地址, 64
  - 入站, 64
  - 出站, 64
  - 漏洞, 74

## Q
- 隔离, `LMD`, 与, 93–94

## R
- 彩虹表, 107
- `RARP` (反向 `ARP`), 53
- `DRARP` (动态 `ARP`), 53
- 反射攻击, 38–40
- `SNMP`, 防止, 41
- `regex` (表达式), `NSE`, 80–81
- `REJECT` 请求, 2
  - 使用 `tcp-reset` 拒绝, 2
- 报告攻击, 40–61
  - `LMD` 与, 92–96
- `Restricted Access` 服务器, 37–38
- `Rootkit Hunter`, 13
  - 配置, 18–21
  - `Debian` 与, 18
  - 设计, 21–22
  - 误报, 21–22
  - `Red Hat` 与, 38
- `rootkits`, 13
- 往返时间 (`RTT`), 56
- `RPM` 软件包管理器, `Red Hat` 与, 69
- `rsyslog`, 62–63
- `trt`, 56

## T
- `TCP` (传输控制协议), `Nping` 与, 50–51
- `TCP RST` 数据包, 1
- `tcpdump`, 60–63
- `tcpflags`, 5–6
- 测试, `SQL`, 120–121
- 计时模板, 73
- `tripwire` 见 `Open Source Tripwire`
- 故障排除, 端口敲击, 10

## U-V
- `UDP` (用户数据报协议). `Nping` 与, 52
- `ntilities`, `Hashcat-utils`, 111
- `版本` 类别 (`NSE`), 75
- `vul` 类别 (`NSE`), 75

## W-Z
- `Web` 扫描, 120–121
- 字典列表攻击, 106–107
- `XOP` (扩展操作), 107–108
- `Zenmai`, 82

## S
- `safe` 类别 (`NSE`), 75
- `SCANID`, 92–93
