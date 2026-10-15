

# Windows+BSD+Linux 安装指南

# Subhasish Ghosh

subhasish_ghosh@linuxwaves.com 版本：v1.1 最后更新：2003年8月21日

# 修订历史：

- v1.0：初始发布，由Linux文档项目（LDP）审阅。做了一些结构性更改和小的修正；新增了“故障排除”和“安装OpenBSD 3.2-RELEASE”两章。
- v1.1：进行了修正并添加了信息。FreeBSD -RELEASE的信息已更新至4.8-RELEASE。新增“安装NetBSD 1.6.1”一章，并对本指南做了一些小的修改。

> 欢迎！本文档说明了如何在一台计算机的同一块硬盘上安装和配置三种不同的操作系统。读者可以从以下组合中选择：Microsoft Windows 95/98（第二版）/Millennium版（ME）/NT/2K/XP + FreeBSD 4.8-RELEASE/OpenBSD 3.2-RELEASE/NetBSD 1.6.1 + Linux。本文仅讨论Intel架构的多重引导，并且GNU GRUB是首选引导加载程序。如果您有任何问题或评论，欢迎通过电子邮件与我联系，邮箱地址：subhasish_ghosh@linuxwaves.com。谢谢！

注意：在“内容组织”部分，读者必须选择执行第3章、第4章或第5章。

## 1. 引言

- 1.1 本指南的目的
- 1.2 什么是多重引导？
- 1.3 多重引导的优缺点
- 1.4 前提假设列表
- 1.5 致谢
- 1.6 法律声明
- 1.7 关于作者

## 2. 常见问题解答（FAQ）

## 3. 内容组织

- 3.1 第1章：关于操作系统
  - 3.1.1 Microsoft Windows
  - 3.1.2 Linux
  - 3.1.3 FreeBSD
  - 3.1.4 OpenBSD
  - 3.1.5 NetBSD
- 3.2 第2章：安装Microsoft Windows
  - 第A节：安装MS Windows 95

## 4. 故障排除

## 5. 结论

- 第B节：安装MS Windows 98（SE）
- 第C节：安装MS Windows Millennium（ME）
- 第D节：安装MS Windows NT（4.0）
- 第E节：安装MS Windows 2000（专业版）
- 第F节：安装MS Windows XP（家庭版/专业版）
- 实际步骤摘要

- 3.3 第3章：安装FreeBSD 4.8-RELEASE
  - 1. FreeBSD中的切片
  - 2. FreeBSD中的文件系统
  - 3. 安装步骤摘要

- 3.4 第4章：安装OpenBSD 3.2-RELEASE
  - 安装步骤摘要

- 3.5 第5章：安装NetBSD 1.6.1
  - 安装步骤摘要

- 3.6 第6章：安装Red Hat Linux 7.3
  - 1. Linux中的磁盘驱动器和分区命名
  - 2. Linux中的文件系统
  - 3. 安装步骤摘要

- 3.7 第7章：挂载文件系统
  - 1. 在FreeBSD中挂载文件系统
  - 2. 在Linux中挂载文件系统

## 1. 引言

### 1.1 本指南的目的

虽然我们中的许多人在日常工作中更喜欢在个人电脑上只使用一个操作系统，但有时我们可能希望在同一台计算机上安装两个或更多的操作系统。假设您需要使用MATLAB 6.0进行工程应用；使用PHP设计、编程和实现一个网站，并使用MySQL作为后端数据库（作为企业级公寓开发项目的一部分）；同时还要学习如何使用IPFW配置包过滤防火墙。恰巧，MATLAB软件运行在Microsoft Windows平台上，您想将MySQL数据库部署在Linux操作系统上，最后但同样重要的是，您大学的教授正在使用FreeBSD操作系统软件教授“如何使用IPFW配置包过滤防火墙”。在这种情况下，您可以放心地采用“多重引导”机制，当然也可以不时参考本指南。

本文档以指南的形式呈现，旨在帮助那些信奉“在做中学”方法的Windows、Linux和FreeBSD/OpenBSD/NetBSD用户。多系统引导并非一门精确的科学。你偶然发现一篇文档，阅读它，觉得有趣，自己动手实践，犯错误，然后最终达到预期的目标。这就是你应该学习的方式。我就是这样学会的。Unix专家们很久以前也是这样学会的。当读者读完本指南时，他将会清楚地理解在同一台计算机的硬盘上成功安装和配置三种不同操作系统所需的基本主题。我已尽最大努力以清晰、易于理解的简单语言来描述每一个主题。

互联网上提供的大多数安装HOWTO和指南（适用于Linux、FreeBSD和OpenBSD操作系统）都不完整，因为它们预设了太多的前提，让读者自己去做大部分困难的工作。在本指南中，我逐步演示每一个步骤，从而使整个过程变得简单易懂。

### 1.2 什么是多重引导？

Bryan Pfaffenberger编著的《韦氏新世界计算机词典》（第9版）将“双引导”一词定义为：“一台允许用户在启动时从两个操作系统之间进行选择的计算机”。确实如此。将此定义作为我们的基础，我们可以构建自己对“多重引导”（简称多引导）系统的定义，即：一台允许用户在启动时从两个以上操作系统之间进行选择的计算机。

本文档说明了如何在同一台计算机的硬盘上成功安装和配置三种不同的操作系统，从而使其成为“多引导”系统。本说明所选的操作系统包括：Microsoft Windows 95/98（第二版）/Millennium版（ME）/NT/2K/XP、FreeBSD 4.8-RELEASE/OpenBSD 3.2-RELEASE/NetBSD 1.6.1和Red Hat Linux 7.3。

我将首先安装Microsoft Windows操作系统，然后安装FreeBSD 4.8-RELEASE或

