
```bash
#!/bin/bash
echo -n "Enter first number:"
read x
echo -n "Enter second number:"
read y
(( sum=x+y ))
echo "The result of addition=$sum"
```

使用 `bash` 脚本添加数字非常简单明了。

# 多个数字相加

将多个数字相加可能有点棘手，您将不得不使用循环。让我们看一个例子。

```bash
#!/bin/bash

sum=0

for (( counter=1; counter<5; counter++ ))
do
    echo -n "Enter Your Number:"
    read n
    (( sum+=n ))
    #echo -n "$counter "
done

printf "\n"
echo "Result is: $sum"
```

运行此脚本，看看该脚本允许你加多少个数字后才打印总和。

Linux shell 脚本可用于在 Linux 操作系统上执行您希望完成的任何任务。它具有无限潜力，您用它能实现的事情实际上没有上限。我们鼓励您练习本章中提供的每个 `bash` 脚本，甚至对其进行修改，看看输出如何变化。

# 结论

Linux 操作系统及其发行版非常安全，因此如今受到全球个人和企业的青睐。就个人用户而言，Ubuntu 等 Linux 发行版有助于用户从任何其他操作系统无缝过渡到 Linux。由于安装免费且具有开源性质，Linux 已被证明对学生非常有益。

只需少量的资金投入，用户就可以拥有一个功能齐全的操作系统，并用于日常所有任务。Linux 的各种发行版几乎满足了世界上每个用户的需求。就企业和公司而言，用户数据是最重要的实体，数据丢失可能会大规模影响企业的品牌形象。

多年来，Linux 已被证明是一个安全且稳定的操作系统，企业可以运行其应用程序并存储关键客户数据。Linux 操作系统的安全补丁发布速度也比任何其他操作系统都更快。这使得 Linux 成为任何以安全为主要顾虑的企业的理想操作系统。我们在本书中还阅读了多个章节，这些章节表明，与其他操作系统相比，Linux 提供的许多功能是无可比拟的。

我们在本书中讨论了 Linux 的 Ubuntu 发行版，我们希望这个发行版能让你对进入 Linux 世界的旅程充满热情。Ubuntu 只是你接触 Linux 的开始，通过选择 Linux 作为首选操作系统，在计算机科学领域中还有更多东西值得探索。一旦你习惯了作为 Linux 桌面用户，我们鼓励你探索其他 Linux 发行版，如 Kali Linux、Red Hat Enterprise Linux 等。

Red Hat Enterprise Linux 将帮助你进入一个被称为 Linux 系统管理的领域。使用 Linux 服务器的企业始终需要有人管理服务器，以确保服务器始终保持运行状态，从而保证他们的业务在互联网上始终运行。

Kali Linux 由拥有渗透测试团队的企业用于测试的服务器是否存在任何安全漏洞。因此，从网络安全的角度来看，这个发行版应运而生。

除了这两个发行版之外，还有许多其他口味的 Linux 等待着你，使用 Linux 的潜力是无限的。

## 参考文献

- 10 Things To Do After Installing Ubuntu 20.04 LTS. (2020, April 23). OMG! Ubuntu! https://www.omgubuntu.co.uk/2020/04/things-to-do-after-installing-ubuntu
- An introduction to the Linux boot and startup processes. (n.d.). Opensource.com. https://opensource.com/article/17/2/linux-boot-and-startup
- Chawla, V. (2020, October 8). Windows Vs macOS Vs Linux: Best OS For Cybersecurity. Analytics India Magazine. https://analyticsindiamag.com/windows-vs-macos-vs-linux-for-cybersecurity/
- How to Install Ubuntu 20.04 LTS {With Screenshots}. (2020, May 25). Knowledge Base by PhoenixNAP. https://phoenixnap.com/kb/install-ubuntu-20-04
- Kiario, J. (n.d.). 10 Linux Distributions and Their Targeted Users. Www.tecmint.com. https://www.tecmint.com/linux-distro-for-power-users/
- Linux History - javatpoint. (n.d.). Www.javatpoint.com. https://www.javatpoint.com/linux-history
- Prakash, A. (n.d.). 16 Things to do After Installing Ubuntu 20.04 - It’s FOSS. Https://Itsfoss.com/. https://itsfoss.com/things-to-do-after-installing-ubuntu-20-04/
- Shell Scripting Tutorial for Linux/Unix Beginners. (2019, November 21). Guru99.com. https://www.guru99.com/introduction-to-shell-scripting.html
- What is Linux? - Linux.com. (2018). Linux.com. https://www.linux.com/what-is-linux/
- What’s new in Ubuntu Desktop 20.04 LTS? (n.d.). Ubuntu. https://ubuntu.com/blog/whats-new-in-ubuntu-desktop-20-04-lts

# Linux

# Linux 命令行

# 与 Shell 脚本

安迪·维克兰

## 引言

这本关于 Linux 命令行和 Shell 脚本的书籍，提供了经过验证的步骤和策略，教你如何使用键盘输入命令以及编写 Shell 脚本来创建你定制的程序。Linux 比 Windows 和 Mac 操作系统更难驾驭，它是三者中安全性最高的。当你学会了 Linux，你就可以创建定制软件并使用它来完成常见的日常任务。你可以自定义你希望计算机运行的方式。

Linux 操作起来很有趣，但并不简单。与拥有图形界面的 Windows 不同，Linux 拥有命令行。如果你不熟悉什么是命令行，可以参考 Windows 中的 Dos 或命令提示符。那是一个黑色的屏幕，你需要在上面输入命令来完成你的日常任务。

我写这本书分为两部分：第一部分处理命令，第二部分处理 Shell 脚本。除非你很好地掌握了 Linux 命令和 Shell 脚本，否则你无法熟练地操作系统。我在书中打包了你需要用到的最常用且重要的命令。我还包含了一些你在命令行中输入命令后可以看到的结果。

Shell 脚本部分可能比较难。如果你有编程背景，读起来会很有趣。为了练习脚本编写，你需要在编辑器中工作，但别担心，你会在本书后面的章节中找到关于 Linux 编辑器的内容。你可以编写自己的脚本，或者复制我的脚本并粘贴到编辑器中练习。为了方便，我包含了每个脚本的结果，以便你可以进行比较。我还包含了许多关于如何使用命令的基本脚本示例。

## 第一章

### 什么是 Linux？

作为一名 Linux 学生，你首先应该了解 Linux 的起源，以理解这个操作系统背后的概念。Linux 是计算机操作系统中硬件和软件之间的软件层。它允许你在计算机上进行生产性活动并创建定制程序。简单来说，操作系统是软件和计算机系统硬件之间的媒介。操作系统允许你将数据存储在存储设备上，如硬盘、固态硬盘和 USB 驱动器。它管理数据从一个元素到另一个元素的传输；例如，它监督数据从操作系统流向办公室或家庭中的打印机。如果你在计算机系统中安装了普通的 Windows 环境，例如微软 Windows 操作系统，Windows 操作系统将运行硬件。它控制鼠标、键盘、打印机、扫描仪和其他附件。根据你的需要，你将不得不安装 Microsoft Office、Adobe 阅读器、pdf 转换器和其他软件。你需要为每个程序付费并在系统中安装它们。
