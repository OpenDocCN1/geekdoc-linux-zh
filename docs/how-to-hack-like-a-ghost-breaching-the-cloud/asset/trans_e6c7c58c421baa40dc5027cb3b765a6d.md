
理想情况下，跳板服务器应用于托管 Terraform、Docker 和 Ansible 等管理工具，这些工具稍后将帮助我们构建多个攻击基础设施。图 1-1 展示了该架构的高层概述。

![](img/961e81aef23040d0fbe348f58c055860_28_0.png)

图 1-1：黑客基础设施概述

我们的跳板服务器永远不会与目标交互。连一声响都没有。因此，我们可以在切换前让它们多保留一段时间——几周或几个月——而不会带来显著风险。尽管如此，专门的调查团队可能会找到一种方法将这些系统与用于与目标交互的系统关联起来，因此定期删除并重新创建跳板服务器是个好主意。

## 攻击基础设施

我们的攻击基础设施的波动性远高于跳板服务器，应仅保留几天。如果可能，它应针对每次操作或目标而唯一。我们最不想看到的就是调查人员通过同一个 IP 攻击的不同目标拼凑出各种线索。

攻击基础设施通常由前端和后端系统组成。前端系统可能会向目标发起连接、扫描机器等等。在反向 shell 的情况下，它也可以用于将传入数据包通过 Web 代理路由并适当地传递到后端系统，通常是像 Metasploit 或 Empire 这样的 C2 框架。只有部分请求会被转发到 C2 后端；其他页面则返回平淡无奇的内容，如图 1-2 所示。

![](img/961e81aef23040d0fbe348f58c055860_28_1.png)

图 1-2：数据包路由到后端

这种数据包路由可以用 Nginx 或 Apache 等常规 Web 代理完成，它充当过滤器：来自受感染计算机的请求被直接路由到相应的后端 C2 实例，而剩余的请求——例如来自好奇分析人员的请求——则显示一个无害的网页。后端 C2 框架实际上是攻击基础设施的脊髓，执行受感染机器上的命令、检索文件、投递漏洞利用等等。

你希望你的基础设施是模块化的，可以随时替换。绕过 IP 封禁应该像发送一条命令来生成新的代理一样简单。C2 后端出现问题？输入一条命令，你就拥有一个配置完全相同的新的 C2 后端在运行。

实现这种自动化程度并不是为了尝试最流行的工具和编程技术而异想天开。部署完全配置好的攻击服务器越容易，我们犯的错误就越少，尤其是在压力情况下。这是一个很好的借口，让我们深入了解 DevOps 人员的工作，学习他们的技艺，并将其扭曲以满足我们自己的需求。希望这能让我们了解到一些缺陷，我们稍后将在黑客冒险中利用这些缺陷。下一章将重点介绍构建此后端。

## 资源

- 想了解爱德华·斯诺登在情报界的生活和冒险的精彩记述，请阅读爱德华·斯诺登所著的《永久记录》（Macmillan，2019）。
- 在此搜索 darkAudax 关于破解 WEP 加密通信的教程 https://aircrack-ng.org/。
- 在 https://hakin9.org/ 找到 Brannon Dorsey 关于使用 Aircrack-ng 和 Hashcat 破解 WPA/WPA2 Wi-Fi 路由器的教程
- 在 https://www.howtoforge.com/ 搜索 Muhammad Arul 关于在 Linux 机器上设置 Zsh 的指南。

## 2

## 命令与控制的回归

![](img/961e81aef23040d0fbe348f58c055860_31_0.png)

让我们通过从任何攻击者的基本工具开始来构建攻击基础设施：命令与控制（C2）服务器。我们将研究三个框架，并在我们用作目标的虚拟机上测试每个框架。首先，我们将看看命令与控制过去是如何完成的，以了解我们是如何走到今天的。

### 命令与控制的传统

在过去十年的大部分时间里，C2 框架中无可争议的冠军——提供最广泛、最多样化的漏洞利用、stagers 和反向 shell 的框架——是臭名昭著的 Metasploit 框架（https://www.metasploit.com/）。快速搜索一次渗透测试或黑客教程，我敢打赌第一个链接会指向一篇描述如何在 Linux 机器上设置 meterpreter——Metasploit 使用的自定义有效载荷的名称——以实现完全控制的帖子。当然，文章不会提到该工具的默认设置自 2007 年以来已被每个安全产品标记，但让我们不要太愤世嫉俗。

Metasploit 是在没有讨厌的防病毒软件来搅局的情况下控制 Linux 主机时绝对的首选。连接非常稳定，框架拥有大量模块，而且与许多即兴教程所暗示的相反，你可以——事实上应该——自定义用于构建 stager 和漏洞利用的可执行模板的每一个细节。Metasploit 在 Windows 上的表现较差：它缺乏其他框架中 readily 可用的大量 post-exploit 模块，而且 meterpreter 使用的技术是每个防病毒软件清单上的首要项目。

Windows 是一个不同的野兽，我过去更喜欢 Empire 框架（https://github.com/EmpireProject/Empire/），它提供了专门为 Active Directory 设计的详尽的模块、漏洞利用和横向移动技术列表。可惜的是，Empire 已不再由原团队维护，原团队以其 Twitter 账号为人所知：@harmj0y、@sixdub、@enigma0x3、@rvrsh3ll、@killswitch_gui 和 @xorrior。他们在 Windows 黑客社区掀起了一场真正的革命，值得我们最真诚的赞赏。幸运的是，在我们所有人的喜悦中，Empire 被 BC Security 的人重新带回了生命，他们在 2019 年 12 月发布了 3.0 版本。我理解停止维护 Empire 的决定背后的理由：整个框架的诞生基于这样一个前提，即 PowerShell 允许攻击者在 Windows 环境中畅行无阻，不受防病毒软件和监控等卑鄙的预防措施的限制。随着 Windows 10 的功能如 PowerShell 阻止日志记录和 AMSI 对这一假设提出了挑战，停止该项目以支持新一代攻击（如使用 C#，例如 SharpSploit：https://github.com/cobbr/SharpSploit/）是有意义的。

注意 Antimalware Scan Interface（AMSI）是 Windows 10 中引入的一个组件，它拦截对关键 Windows 服务——用户账户控制（UAC）、JScript、PowerShell 等——的 API 调用，以扫描已知威胁并最终阻止它们：https://docs.microsoft.com/en-us/windows/win32/amsi/how-amsi-helps。

### 寻找新的 C2

随着 Empire 项目不再是选择，我开始寻找潜在的替代品。我担心不得不退回到 Cobalt Strike，就像 99% 的将钓鱼活动伪装成红队工作的咨询公司一样。我对这个工具没有任何意见——它很棒，提供很棒的模块化，并配得上它取得的成功。只是看到这么多假公司仅仅因为买了 3,500 美元的 Cobalt Strike 许可证就搭上红队业务的顺风车，令人疲惫和沮丧。

然而，我很高兴地发现，在 Empire 留下的真空中，出现了如此多的开源 C2 框架。以下是一些引起我注意的有趣框架的简要介绍。我将相当快速地介绍许多与我们当前场景不太相关的高级概念，并演示每个框架的有效载荷执行。如果你不完全理解某些有效载荷的工作原理，不用担心。我们稍后会回到我们需要的那些。

### Merlin

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

如果我们直接编译一个标准代理，任何执行简单字符串查找以查找一般显眼术语的常规防病毒代理都会立即将其查出，因此我们需要进行一些调整。我们将重命名可疑函数，如 ExecuteShell，并删除对原始包名 github.com/Ne0nd0g/merlin 的引用。我们将使用经典的 find 命令来查找包含这些字符串的源代码文件，并将其通过管道传输到 xargs，后者将调用 sed 用任意单词替换这些可疑术语：

```bash
root@Lab:~/# find . -name '*.go' -type f -print0 | xargs -0 sed -i 's/ExecuteShell/MiniMice/g'
root@Lab:~/# find . -name '*.go' -type f -print0 | xargs -0 sed -i 's/executeShell/miniMice/g'
root@Lab:~/# find . -name '*.go' -type f -print0 | xargs -0 sed -i 's/Ne0nd0g\/merlin\/mini\/heyho//g'
root@Lab:~/# sed -i 's/Ne0nd0g\/merlin\/mini\/heyho//g' go.mod
```
