

# 在 Kali Linux 上介绍并安装 DirBuster

> 原文：<https://blog.eldernode.com/introducing-and-install-dirbuster-on-kali/>

![Introducing and Install DirBuster On Kali Linux](img/f18c85673121e598aa7e76a89270fadf.png)

您已经学习了渗透测试工具。DirBuster 是一个渗透测试工具，用于暴力破解 Web 应用服务器上的目录和文件名。DirBuster 具有一个图形用户界面，采用 LGPL-2 协议授权。如果喜欢命令行，也可以使用 `DIRB`。

请记住，如果想在网站或应用程序上使用 DirBuster 或 `DIRB`，必须获得许可，否则就是违法行为。因此，必须在受控环境中使用，并提供特定的网址，例如 NCL 奥运会、不同的 CTF，或者与公司签订渗透测试合同。

本文介绍如何在 Kali Linux 服务器上安装 DirBuster。在 [Eldernode](https://eldernode.com/) 上选择您喜欢的软件包，以最优惠的价格和支持购买 [Linux VPS](https://eldernode.com/linux-vps/)。

## 什么是 DirBuster，它在 Kali Linux 上是如何工作的？

DirBuster 是由 OWASP 开发的多线程 Java 应用程序，旨在暴力破解 Web 应用服务器上的目录和文件名。这是一个 GUI 应用程序，附带在 Kali Linux 中。

DirBuster 会搜索 Web 服务器上的隐藏页面和目录并找到它们。作为一名开发人员，您可以保留一个可访问但未链接的页面，这正是 DirBuster 用来寻找的潜在漏洞。因此，您可以通过在 Web 服务器或应用程序中找到不需要的内容来提高应用程序的[安全性](https://blog.eldernode.com/tag/security/)。

您也将能够理解，简单地不链接到一个页面，并不意味着该页面无法被访问。它的工作方式和方法非常简单。您应该指定一个 URL 和一个端口，如 `80` 或 `443`，然后为它提供一个单词表。最后，它会向网站发送 HTTP GET 请求，并监听网站的响应。

DirBuster 的工作原理是识别应用程序内部或 Web 服务器上不需要的内容。

## 如何在 Kali Linux 上使用 DirBuster

有两种方法可以启动 DirBuster 应用程序。

1. **从 DirBuster 图标启动：** 您可以在 Kali Linux 的菜单中搜索并输入“DirBuster”，然后点击图标启动应用程序。
2. **使用终端启动：** 您也可以通过运行以下命令使用终端启动 DirBuster：

```bash
dirbuster
```

![How to use DirBuster](img/ba674a605a957f4df0037bf5f3a95e6f.png)

使用上述两种方法，都会显示一个用户界面，允许您列出来自端口 `80` 中 Web URL 的文件和目录。一旦 DirBuster 开始运行，您应该继续以下步骤：

1. 设置目标 URL 和线程数。
2. 选择可能的目录和文件列表。
3. 启动强力扫描。
4. 生成报告（可选）。

## DirBuster 功能

除了上面关于 DirBuster 的解释，使用这个简单而强大的工具还有更多好处：

1. 支持 HTTP 和 HTTPS。
2. 扫描文件和目录。
3. 递归扫描它识别的目录，提供更深入的搜索。
4. 能够在任何目录下启动。
5. 能够执行暴力扫描或基于列表的扫描。
6. 以超高速执行强力扫描。
7. 提供自己的单词列表集合。
8. 允许用户制作自己的单词表。

## 缺点

像任何其他工具一样，DirBuster 也存在一些用户认为是其缺点的行为：

- 太吵了。
- 服务可能会受到大量请求的干扰。
- 当有许多错误响应时，强力扫描可能会停止。

## 如何在 Kali Linux 上安装 DirBuster

DirBuster 默认自带于 [Kali Linux](https://blog.eldernode.com/tag/kali-linux/)。您只需要运行以下命令来安装 DirBuster 和它所依赖的任何其他软件包：

```bash
sudo apt-get install dirbuster
```

这样，您可以通过下面的路径从 Kali Linux 启动 DirBuster：

`Web 应用程序分析 >> 网络爬虫和目录蛮`

![How To Install DirBuster On Kali Linux](img/e5ab0142c0d6344a8ca562685bb6f41f.png)

## 如何在 Kali Linux 上卸载 DirBuster

任何时候您决定卸载 DirBuster，都可以运行下面的命令来删除 `DirBuster` 软件包本身：

```bash
sudo apt-get remove dirbuster
```

但是，如果您希望删除 `DirBuster` 软件包和任何其他不再需要的依赖包，请键入：

```bash
sudo apt-get remove --auto-remove dirbuster
```

此外，您可以使用下面的命令删除用于 DirBuster 的本地配置文件。您必须小心运行此命令，因为已清除的配置或数据无法通过重新安装软件包来恢复：

```bash
sudo apt-get purge dirbuster
```

或者使用类似下面的命令：

```bash
sudo apt-get purge --auto-remove dirbuster
```

## 结论

在本文中，向您介绍了 DirBuster，并学习了如何在 Kali Linux 上安装 DirBuster。如果您已经安装了此工具，请让您的朋友了解您的体验，并在 [Eldernode 社区](https://community.eldernode.com/)上添加更多详细信息。

