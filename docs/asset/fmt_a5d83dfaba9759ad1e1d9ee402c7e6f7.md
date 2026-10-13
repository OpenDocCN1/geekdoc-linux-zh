
这会运行一个脚本来检查是否满足所有依赖关系以及构建环境是否正确。然后，

```
$ make
```

用于编译软件。最后，以 root 身份运行：

```
# make install
```

如果编译失败，请检查错误信息以了解原因，并在重新开始之前运行

```
$ make clean
```

。如果你不喜欢该软件，也可以运行

```
$ make uninstall
```

来移除它。

运行 `make install` 的一个替代方案是一个名为 CheckInstall 的程序，它会为你的安装生成一个 `rpm` 文件。这种方法可以让 RPM 数据库知晓并跟踪你安装的所有文件。有关更多信息，请参见关于 CheckInstall 的以下章节。

## 一个便捷的安装工具——CheckInstall

当你从源代码编译应用程序并安装它们时，它们不会出现在 RPM 数据库中，因此无法由 RPM 管理。

你可以使用一个名为 CheckInstall 的程序来为这些应用程序提供 RPM 管理。在最简单的情况下，`checkinstall` 是构建源代码过程中 `make install` 步骤的直接替代品。

例如，在从源代码编译时，传统上使用：

```
# ./configure
# make
# make install
```

使用 CheckInstall，步骤看起来像这样：

```
# ./configure
# make
# checkinstall
```

CheckInstall 会创建一个二进制 `.rpm` 包，并从该包中安装应用程序。这使得新应用程序成为 RPM 数据库的一部分。新的 `.rpm` 文件会留在 `/usr/src/redhat/RPMS/i386` 中供你使用。新应用程序稍后可以 `rpm -e` 卸载。

一些应用程序以 shell 脚本包装器的形式提供。使用 shell 脚本作为 CheckInstall 的参数将生成已安装文件的 `.rpm` 文件，并将它们添加到你的 RPM 数据库中。并非所有应用程序都能使用 CheckInstall 安装。请仔细阅读其随附文档。

CheckInstall 可以从 http://asic-linux.com.mx/~izto/checkinstall/index.php 下载。

## 相关的 Fedora Core 和 Linux 命令

在管理你的 Fedora Core Linux 系统资源和软件包时，你将使用这些命令：

- `system-config-packages` — Fedora Core GUI 包管理器。
- `rpm` — RPM 包管理器。
- `rpmbuild` — 构建 RPM 源包和二进制包。

## 参考

- http://www.rpm.org — Fedora Core 包管理器的主页。该网站提供了指向 Linux 和 X 桌面环境（如 GNOME）最新版本 RPM 软件的关键链接。
- http://www.rpm.org/max-rpm/ — 指向 Ed Bailey 的经典著作和 RPM 参考书 *Maximum RPM* 更新版本的链接。
- http://linux.tnc.edu.tw/techdoc/maximum-rpm/rpmbook/node15.html — Red Hat 包管理器的历史。
- http://www.smogesspace.com/documents/behind_the_names.html — Red Hat Linux 发布的历史，也是了解版本名称之间联系的好地方。
- http://www.gnupg.org/ — GNU Privacy Guard 的主页，这是一个无版权限制的自由替代方案，用于 Pretty Good Privacy。
- http://www.debian.org/doc/manuals/project-history/ch-detailed.en.html — Debian Linux 包系统的历史。
- http://www.nrh-up2date.org/index.html — Red Hat Up2Date 应用程序的替代品。

# 第 8 章

## 因特网：浏览网页、撰写电子邮件和阅读新闻

因特网在很短的时间内彻底改变了我们的现代文明。不久前，通过因特网进行交流还闻所未闻；如今，如果你没有电子邮件账户或即时通讯工具，就被认为落后了。本章向你介绍一些流行的软件，你可以使用它们来访问因特网、发送和接收电子邮件、阅读网络新闻、使用在线协作工具与他人协作，以及使用即时通讯甚至视频 conferencing 进行实时交谈。你将了解如何设置每个软件以访问你所需的资源。

## 选择网页浏览器

因特网永远地改变了我们获取和共享信息的方式。我们查看因特网的方式也发生了变化，并不断改进以提供更好、更丰富的体验。在本节中，我们将看看 Fedora 上可用的一些流行开源网页浏览器。

### 因特网简介

因特网本身最初是由美国国防部于 1969 年创建的。它以国防部的高级研究计划局（ARPANet）命名。旨在构建一个能够承受重大灾难的网络（当时正值冷战顶峰），它很快发展成为包含越来越多的网络，从而建立了因特网。然后，1991 年，欧洲核子研究中心（CERN）的 Tim Berners-Lee 开发了万维网（World Wide Web）的概念，包括超文本传输协议（HTTP）和超文本标记语言（HTML）。这给了我们现在所知的因特网。

### 本章内容

- 选择网页浏览器
- 选择电子邮件客户端
- 网络新闻概述
- 选择新闻阅读器
- 使用 TWiki 协作
- 因特网中继聊天
- 使用 GAIM 进行即时通讯
- 使用 GnomeMeeting 进行视频 conferencing
- 参考

## Mozilla Firefox

最受欢迎的网页浏览器之一，也是 Fedora 默认的网页浏览器，是 Mozilla Firefox（见图 8.1）。Firefox 基于从 Mozilla 套件衍生出来的坚实代码基础，为浏览因特网带来了新的活力。自 2004 年底发布以来，超过 2500 万人下载了 Firefox，并从 Internet Explorer 那里抢占了相当大的市场份额。

在 Fedora 中，你可以在屏幕顶部的“应用程序”、“因特网”菜单中找到 Firefox。不过，启动 Firefox 更简单的方法是点击“操作”菜单旁边的小地球图标。无论哪种方式，你都会打开 Firefox。

![](img/774d40fd20903495c5cd00e2efad3f33_243_0.png)

图 8.1 Mozilla Firefox——重新发现万维网。Firefox 允许你添加大量升级功能，进一步提升你的体验。

除了基本程序之外，还有大量的插件和扩展可以增强 Firefox 的功能，使其超越简单的网页浏览。像 Shockwave Flash 这样的插件和 Java 扩展是可用的，而扩展功能则为浏览体验提供了有用甚至有时有趣的补充。例如，ForecastFox 是一个扩展，可提供当地的天气状况；带宽测试器（Bandwidth Tester）是一个计算当前带宽的工具。

## Mozilla 套件

Mozilla 套件是一个高度集成的网页浏览和消息应用程序套件，是从 Netscape 衍生而来的（见图 8.2）。由于 Netscape 几年前已经停滞，Mozilla 基金会由 AOL 和其他公司成立，以继续开发如今已开源的曾经流行的浏览器。这些工作的成果可以在 Mozilla 套件中体现。默认情况下，Fedora 未安装 Mozilla；相反，你需要在安装过程中指定它，或者稍后使用 Yum 或 apt 进行安装。

请记住，如果你安装了 Mozilla，你也获得了套件的其他部分：邮件和新闻组阅读器、地址簿以及 IRC 客户端。如果你不需要所有这些功能，可能使用 Firefox 会更好。

![](img/774d40fd20903495c5cd00e2efad3f33_244_0.png)

图 8.2 Mozilla 套件，Firefox 的先驱，Netscape 的后裔。

## Epiphany

Epiphany 是随原始 Gnome 桌面提供的浏览器（见图 8.3）。非常基础，并且建立在与早期的 Firefox 和 Mozilla 相同的 Gecko 渲染引擎上，Epiphany 在多个领域已发展到目前的版本。

![](img/774d40fd20903495c5cd00e2efad3f33_245_0.png)

图 8.3 Epiphany，标准的 Gnome 网页浏览器。

## Konqueror

KDE 用户可以选择使用 Konqueror，它是 KDE 的默认浏览器（见图 8.4）。除了处理文件系统导航外，Konqueror 还可以用于浏览网页。同样，它也是基于 Firefox、Mozilla 和 Epiphany 中使用的 Gecko 渲染引擎。

![](img/774d40fd20903495c5cd00e2efad3f33_246_0.png)

图 8.4 Konqueror，标准的 KDE 网页和文件系统浏览器。

## 选择电子邮件客户端
