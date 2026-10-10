
### 解决密钥错误

当您尝试连接时，可能会收到如下所示的消息：

```
ssh root@137.184.176
The authenticity of host '137.184.176' can't be established.
ED25519 key fingerprint SHA256: not known by any other names
Are you sure you want to continue connecting (yes/no)?
```
此错误通常意味着权限拒绝（公钥）。您可以通过查看 `-v` 标志来获取更多信息：

## 2. Linux 基础知识

### 什么是 Linux？

Linux 这个词听起来很难完全解释。Linux 实际上指的是 Linux 内核，它是 Linux 操作系统的核心。我们将在后面的章节中详细讨论内核。Linux 最初于 1991 年 9 月由芬兰的 Ken Torvalds 发布，作为商业操作系统的免费开源替代方案。从那时，它获得了巨大的人气，世界上 90% 以上的超级计算机运行着 Linux。Linux 显然是站在巨人的肩膀上。在 Linux 开发之前，Ken Thompson 和 Dennis Ritchie 在美国贝尔实验室开发了 Unix 操作系统，以及许多进入 Linux 的工具。Linux 也受到了灵感，最初是在名为 Minix 的操作系统上开发的。Minix 由教授 Andrew Tanenbaum 开发，用于向学生教授操作系统的原理。

### 什么是开源？

在 Linux 的背景下，开源是指将操作系统的底层代码免费供任何人使用、修改和分发。这带来了一些极佳的影响。由于代码可以根据特定的用例进行修改和调整。另一个是它可以进行安全审计。此外，任何人都可以阅读 Linux 的源码。这意味着 Linux 的开发非常快，并且适用于广泛的用例。

Linux 的开源哲学确实带来庞大的社区，成千上万的开发者致力于改进 Linux、修复漏洞并开发新功能。得益于此，Linux 已成为一种在全球运行的稳定、可靠且安全的操作系统。

### Unix 与 Linux

明确指出 Unix 和 Linux 不是同一个东西是非常重要的。这对于初学者可能会困惑。Unix 是在 60 年代在贝尔实验室开发的，而

Linus Torvalds 在 90 年代开发了 Linux，那是 20 多年前的事。Linux 的大部分设计灵感来源于 Unix。Linux 甚至被称为类 Unix 系统（Unix-like）。Linus 选取了他认为有用的 Unix 部分，并舍弃了其他部分。Unix 系统今天仍在开发，并运行着许多生产系统。

### Linux 发行版 (Linux Distributions)

由于 Linux 是开源的，许多不同的开发者都对其进行过，并根据他们对操作系统如何运行的观点，将其工作分支成独立的发行版或“分发版”（distros）。分支（fork）是指软件从其他软件复制并采取不同方向的过程。每个 Linux 发行版都有自己的一套独特特性、工具和预装应用程序。

需要记住的是，Linux 实际上指的是 Linux 内核，而使用该内核的发行版被称为 Linux 操作系统。

对于本书，我们所有的示例都将使用 Debian 或 Ubuntu 的工具。让我们简要介绍一些最流行的 Linux 发行版。

### Debian

Debian 是基于 Linux 内核的最老的发行版之一。它首次发布于 1993 年，至今仍然非常有活力！Debian 有不同的“分支”，这些只是同一个操作系统的不同版本。`Stable`（稳定）、`Testing`（测试）和 `Unstable`（不稳定）是三个主要的 Debian 分支。`Stable` 是大多数人应该使用的分支，而 `testing` 和 `unstable` 的更新频率更高，其更改最终会合并到 `Stable` 中。Debian 是许多其他发行版的基础，最流行的是 Ubuntu。Debian 与许多发行版一样，利用大量的自由和开源软件。

### Ubuntu

Ubuntu 最初于 2004 发布，由一家名为 Canonical 的英国公司开发。它在初学者和专业人士中都很受欢迎。它是本书示例中将使用的发行版。Ubuntu 基于 Debian，甚至使用 Debian 的包管理系统来安装软件。Ubuntu 拥有多个版本的操作系统，适用于桌面、服务器，甚至还一个用于物联网（IoT）设备和机器人核心的版本。

Ubuntu 是我接触 Linux 的 Linux，我认为你也会喜欢使用它的。

### RHEL

RHEL，或 Red Hat Enterprise Linux（红帽企业级 Linux），由……名为 Red Hat 的公司开发。在编写本文时，红帽已归 IBM 所有。Red Hat Enterprise Linux 对其发行版有更多限制，比其他发行版更具商业性。此外，RHEL 使用与 Debian 等发行版不同的软件包安装系统，称为 `RPM` 或 Red Hat Package Manager（红帽包管理器）。

### Fedora

Fedora 在某些方面是 Red Hat Enterprise Linux 的基础和基础。Red Hat 是 Fedora 的分支。Fedora 与 Red Hat 有很多相似之处，但限制和商业协议要少得多。由于 Fedora 基于 Red Hat，因此它也使用 `RPM` 或 Red Hat Package Manager。

### Arch

Arch 在书中值得一读，尽管它在服务器上并不常用。Arch 通常安装在桌面和笔记本电脑上，供那些想要对系统拥有深度控制权的用户。Arch 在许多设计决策上非常有“主见”（opinionated）。这意味着开发者们对处理问题的方式有强烈的信念。我不建议初学者使用 Arch，但如果你愿意接受挑战，学习它可能会让你对 Linux 操作系统有更深入的。

### 什么是内核 (Kernel)？

内核是 Linux 操作系统最重要的部分。它是操作系统的大脑和核心。Linux 内核负责启动操作系统、管理进程、内存、设备、进程等许多。目前，只需理解 Linux 内核是操作系统至关重要的部分即可。

如果你想查看系统正在运行哪个版本的内核，可以运行 `uname -r`：

```
stetson@linux_rocks:~$ uname -r
5.15.0-56-generic
```
