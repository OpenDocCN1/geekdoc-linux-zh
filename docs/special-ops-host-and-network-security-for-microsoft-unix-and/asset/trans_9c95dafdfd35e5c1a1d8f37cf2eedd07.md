

DNS 攻击与防御 • 第 8 章

## 防御缓存中毒

缓存中毒很容易防御。所有 DNS 守护进程都有关闭缓存的选项。如果没有启用缓存，对服务器进行伪造回复将毫无意义。大多数最新的守护进程已经包含了针对中毒的补丁。

目前，接收到的带有权威记录的数据包在输入缓存之前会经过验证。

## 防止缓冲区溢出

缓冲区溢出缓解可以非常成功。已经开发了许多工具来帮助防止未经授权的渗透技术。在选定的环境中，应使用如 stackguard (www.immunix.org/products.html#stackguard) 等防缓冲区溢出编译器，结合最新的 DNS 守护进程，并限制访问以减少暴露；要真正停止缓冲区溢出，需要从底层一个安全的平台。像 OpenBSD 这样的安全操作系统以及 DJBNS 这样的守护进程是减少溢出风险的最佳选择。Theo de Raadt 的 OS 定制化和加固的 DJB 守护软件可能看起来极端，但根据它们的良好记录，它们值得投入管理上的时间和精力。

## 使用 Bogon 过滤器

## 安全安装和配置 DNS 守护进程

参与 DNS 需要一台服务器。为了从管理角度参与 DNS，你的服务器必须公开托管记录。有许多守护进程可供选择——根据需要的情况，每个都有其优势。在本中，你将详细了解三个最流行的 DNS 守护进程，并演示它们的安装和配置。

![](img/729efc56f204a2ebffb8295c3a2dfdfb_449_0.png)

BIND 基于 Unix 平台，并拥有最丰富的在线文档。由于其全球标准性，本节将对 BIND 进行最详细的介绍。

第二种流行的 DNS 服务器是 Microsoft DNS。然而，这种说法略有误导性：Microsoft DNS 在*内部*被广泛使用，尽管在外部也有一定的知名度。由于其易用性以及 Windows 平台带来的舒适性，大多数普通管理员没有机会从高级角度学习 DNS 系统。因此，正确外部使用 Microsoft DNS 并不常见。即使是 msn.com 和 microsoft.com 这样的网站，据传也托管在运行 BIND 的 DNS 服务器上。

> 注意
> Microsoft DNS 是唯一不提供免费下载的常用 DNS 守护进程。

DJBDNS 由受尊敬的数学家和计算机科学爱好者 DJ. Bernstein (http://cr.yp.to) 编写，是三个守护进程中最有趣且推荐的一个。它是目前最安全的 DNS 守护进程，但技术上也最复杂。目前，只有高级管理员在生产环境中运行它，它主要供具有高安全需求的人士使用。

## 加固 OS

在安装任何守护进程之前，OS 加固应该是一项要求。我们的示例使用了带有 grsecurity (www.grsecurity.net) 内核补丁的加固 Linux 操作系统。

在 Unix 平台上，守护进程应始终在 *chroot* 环境中运行。*chroot* 环境无法与其监狱之外的任何文件系统部分交互。在此类环境中运行 BIND 可以限制如果 BIND 被利用时，恶意攻击者可能获得的访问权限。

为了最大限度地减少 BIND 二进制文件本身的缓冲区溢出和利用，应使用安全编译器结合最新的稳定 BIND 版本。可以在互联网软件联盟 (ISC) 网站 (www.isc.org/products/BIND) 找到 BIND。

应该遵循并完全理解详细的 *chroot* 指南。由于 *chroot* 环境是在*事后*保护系统，因此此处将不再涵盖此内容。Scott Wunsch 编写的极佳 chroot BIND 教程可以在 www.linuxsecurity.com/docs/LDP/Chroot-BIND-HOWTO.html 获取。

## NOTE

> 拥有中等量的 OS 系统调用知识，有可能突破 chroot 的缺陷。要理解 chroot 的缺陷，请参阅 Anton Chuvakin 博士的《Using Chroot Securely》(www.linuxsecurity.com/feature_stories/feature-story-99.html)。

## 伯克利互联网命名域 (BIND)

BIND 是原始的 DNS 守护进程。BIND 的设计和哲学为目前所有其他 DNS 平台奠定了基础。BIND 最初基于加州伯克利本科课程的研究，然后在 4.9.3 版本期间由互联网软件联盟 (ISC) 接管。BIND 的第一个生产版本发布于 1997 年。

## 特定漏洞

多年来，BIND 被发现存在许多漏洞。缓存中毒、缓冲区溢出和远程执行为 DNS 攻击铺平了道路。目标是理解这些漏洞以便更好地防御它们。

## 安装 BIND

初始的 BIND 安装非常简单。你可以在官方互联网软件联盟 (ISC) 网站 (www.isc.org/products/BIND) 上找到最新版本的 BIND。

![](img/729efc56f204a2ebffb8295c3a2dfdfb_449_0.png)

