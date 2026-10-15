
在本章中，我们将介绍 Linux 和 Ubuntu。我们将从讨论 Linux 的创建开始。然后，我们将深入 Ubuntu，看看它是如何开始的，理解 Ubuntu 的发布，并涵盖 Ubuntu 的不同版本。最后，我们将介绍其他 Linux 发行版以及它们与 Ubuntu 的区别。此外，我们将讨论构成 Linux 栈的组成。

我们鼓励你在本章结束时创建一个博客页面并注册账户，以便准备好书中后续的章节。

## 结构

在本章中，我们将涵盖以下主题：

- Linux 历史
- Linux 栈
- Linux 的使用和统计
- Ubuntu 历史
- Ubuntu 发布
- Ubuntu 版本
- 其他 Linux 发行版
- 创建 GitHub 和 blogger 账户

## 目标

在本章结束时，我们将理解 Linux 是如何产生的以及 Linux 栈的不同部分是如何组合在一起的。我们还将理解不同 Linux 版本以及 Ubuntu 是如何版本化和发布的。

## Linux 历史

Linux 是 Linus Torvalds 在 1991 年在赫尔辛基大学担任计算机科学学生时（21岁时）创建的。最初，Linus 将这项发明命名为 Freax，但上传项目的 FUNET 管理员不喜欢这个名字，将其重命名为 Linux。

Tux，如图 1.1 所示的企鹅吉祥物，是 Linus 在访问悉尼动物和水族馆被一只小企鹅咬后选择的。

今天，你可以在 GitHub 上找到 Linux 内核开发：https://github.com/torvalds/linux 并在那里开发，目前 Linux 内核有超过 13 万贡献者。参考以下链接：https://en.wikipedia.org/wiki/Ubuntu

## Linux 栈

Linux 内核是所有 Linux 操作系统的基础。它是启动并添加所有驱动程序的。如果汽车品牌是 Ubuntu，那么引擎就是 Linux 内核。

现在，如果你想把 Linux 系统作为桌面电脑使用，你还需要某种窗口管理器。在这本书中，我们将更多地查看窗口管理器 `i3` 以及 Ubuntu 默认的窗口管理器 `gnome`。

## 使用和统计

Linux 和 Ubuntu 的使用增长迅速。今天，Linux 是我们超级计算机使用的主要操作系统。它运行在 NASA 服务器上，也是物联网（IoT）设备最常用的操作系统。

在云端，它是主导性操作系统，所有运行的操作系统中有 90% 都是 Linux。Linux 驱动着 Kubernetes 集群，而该集群正成为托管应用程序的默认平台。

根据最新的 Linux 发行版统计，Ubuntu 是最流行的 Linux 发行版 (32.8%)，其次是 Debian (14.4%) 和 CentOS (10.8%)。

## Ubuntu 历史

最常用的操作系统之一是 Debian，而 Ubuntu 是基于 Debian 的。Ubuntu 由英国 Canonical 公司构建，旨在成为一个友好且易用的 Linux 系统。第一个版本 Ubuntu 4.10 发布于 2004 年 10 月。如今，情况已经发生了许多变化，Ubuntu 现在已经发布了 22.04 版本。

Ubuntu 有一个基础版本。Ubuntu Desktop 是适用于笔记本电脑、办公和家庭电脑的带有 GUI 的桌面版本。Ubuntu Server 同时运行在云端和物理机上，而 Ubuntu Core 则用于运行 IoT 设备。

https://en.wikipedia.org/wiki/Ubuntu

## Ubuntu 发布

Ubuntu 每年发布两次，分别在 4 月 4 日和 10 月 10 日发布版本。发布版本的名称包含年份。Ubuntu 22.10 将于 2022 年 10 月发布。那么，一个版本的支持周期多久呢？这取决于具体情况。Ubuntu 提供长期支持 (LTS) 版本，LTS 版本受支持十年。如果你计划搭建一个运行时间较长的服务器或用于工作的桌面电脑，请考虑使用 LTS 版本。然而，如果你想要最新的内核和工具，可以查看最新的发布版本。在书中，我们建议安装 LTS 版本。Ubuntu 还提供了从 LTS 升级到下一个版本的工具。

更多关于 Ubuntu 发布可以通过 https://ubuntu.com/about/release-cycle。

## Ubuntu 版本

Ubuntu 和 Linux 内核都是开源的，这导致许多开发者创建了他们自己的 Ubuntu 版本。人们希望在学校或音乐工作室等特定特定版本的 Ubuntu 上使用另一种图形桌面环境。

Ubuntu 的一些不同版本如下：

### Mint

Linux Mint 基于 Ubuntu 和 XFCE 桌面。Linux Mint 预装了许多标准工具，以便你在安装后能够快速开始并工作。

Linux Mint 是一种适用于台式机和笔记本电脑的操作系统。它旨在开箱即用，并完整配备了大多数人需要的应用程序。

你可以在 https://linuxmint.com/ 找到关于 Mint Linux 的更多信息和下载链接。

### Pop

System76 是一家构建 Linux 电脑的公司，其操作系统基于 Ubuntu。

Pop!OS 专为快速导航、易于工作组织以及流畅便捷的工作流而设计。你的操作系统应该鼓励发现，而不是阻碍。

你可以在 https://pop.system76.com/ 找到关于 Pop Linux 的更多信息和下载链接。

### LXLE

LXLE 是 Ubuntu 的轻量版。我们使用了那些资源较低但仍需要以安全和更新的方式使用的计算机。

LXLE 的开发者将其描述为“资源占用少、功能强大”。LXLE 基于 Ubuntu，启动速度极快。

你可以在 https://lxle.net/ 找到关于 LXLE 的更多信息和下载链接。

## 其他 Linux 发行版

Ubuntu 基于名为 Debian 的 Linux 发行版，但 Linux 操作系统比 Ubuntu 多。Raspberry Pi OS 是另一个基于 Debian 的著名操作系统。然而，还有更多。Kali Linux 是一个为黑客专门构建的 Linux 操作系统。它包含了黑客所需的所有工具，并可以从 USB 内存轻松运行。

但我们的 Linux 发行版不仅限于 Debian 家族。还有更多的 Linux 家族。

Red Hat（红帽）拥有许多公司使用的 Red Hat Enterprise发行版。它包含了开源软件和 Red Hat 自己的软件。Fedora Linux 将是下一个红帽 Linux。在 Fedora 中，我们可以看到最新的软件和内核版本。如果你开始使用 Docker，你将接触 Alpine Linux。Alpine 是一个非常适合构建小型 Docker 镜像的极简 Linux，https://www.alpinelinux.org。

关于 Kubernetes，新的 Linux 发行版发布了用于运行容器的独特构建。最著名的 Flatcar 和 CoreOS，其中 Flatcar 是 CoreOS 的分支。AWS 也发布了自己的用于容器的 Linux 构建，称为 Bottlerocket。

一个新项目是 Talos Linux，这是一个专门为运行 Kubernetes 设计的特殊 Linux 发行版。Talos Linux 的一个特殊之处是它没有任何外部访问，所有的配置都通过 API 调用完成。

要阅读更多内容并获取特殊 Linux 发行版的安装说明，请访问章节参考部分中的链接。

让我们了解 Linux 版本之间的区别：

这完全取决于你如何使用你的计算机和服务器。在你的笔记本电脑上运行 Ubuntu LTS，在我的家庭服务器上运行 Ubuntu LTS。这样你就可以复用工具和脚本，例如设置备份和访问。

然而，flatcar Linux 运行在 Kubernetes 集群中，这有利于运行容器和 Kubernetes。

我们可能有一些运行 Red Hat 的服务器，其区别在于，例如包管理器。在 Ubuntu 中，正如你将在书中学到的，包工具称为 `apt`。

在 Ubuntu/Debian Linux 上安装 apache 的命令：

- `apt-get install apache`

然而，在 Red Hat 服务器上，你的包管理器名为 `yum`。所以，要安装 Apache Web 服务器，你需要运行。

- `yum install httpd`

它们都会安装 Apache Web 服务器，但你输入安装 Apache 的命令的方式是不同的。在 Alpine Linux 中相同的命令如下：

- `apk add apache`

这种方式上存在一些差异，但正如你将在书中学习如何使用 `apt`，迁移到基于红帽的 Linux 是简单的，而且安装包的基础是相同的。你只需要找到正确的命令即可。

## 创建 GitHub 和 blogger 账户
