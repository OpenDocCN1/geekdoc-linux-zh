
Linux 诞生于互联网，正是因为互联网，Linux 才成长到今天的程度。这种增长的例子可以在 Linux 内核的几乎每个部分和各种发行版中找到。如果没有互联网作为媒介，就不可能有来自世界各地的人们贡献的丰富代码。也无法进行构建发行版并将其交付给今天全球估计 700 万至 1000 万 Linux 用户所需的协作。正因如此，互联网上一般以及特别是在万维网上有大量资源可供 Linux 用户使用。本节介绍一些对 Linux 系统系统管理员将有极大帮助的资源。这里选用的网站只是其中一小部分。要了解更多关于网络上的 Linux 资源，请查看你喜欢的搜索引擎，或查看此处描述的网站上的链接页面。

### Linux 文档项目

所有系统管理员都应该熟悉的一个网站是位于北卡罗来纳大学的 Linux 文档项目网站，网址为 http://metalab.unc.edu/LDP/。Linux 文档项目，简称 LDP，是一项旨在制作可通过互联网自由分发的 Linux 文档的项目，就像 Linux 本身一样自由分发。LDP 有志愿者创建诸如《Linux 安装和入门指南》、《网络管理员指南》、《系统管理员指南》以及几乎任何可想象主题的丰富 howto 文档。从选择兼容硬件到设置 PPP，甚至设置系统以中文显示信息，都由那些花时间学习某项流程步骤的人记录下来。通过这样做，其他人受益于他们的经验。此外，LDP 还维护 Linux 手册页、常见问题列表和 Linux Gazette。

图 2.6

Linux 文档项目主页。

![](img/4886c42c7629f445c7f7f3011ffbf3c3_70_0.png)

你在 Linux 文档项目网站上找到的大多数文档都可在 Red Hat 安装介质上获得，默认安装在 `/usr/doc/HOWTO` 和 `/usr/doc/LDP` 下，格式包括 HTML、PostScript、DVI、文本和 SGML 等。许多文档还已被翻译成英语以外的语言，包括西班牙语、德语、韩语、意大利语和日语，仅举几例。访问 LDP 网站以查找 HOWTO 的更新并寻找新的翻译。这些更新会在 `comp.os.linux.announce` 新闻组上宣布。

### Linux 内核归档和 Kernelnotes

如果任由其发展，跟上 Linux 内核的变化可能是一项全职工作，但通过利用以下两个网站，你可以及时了解变化的发生情况，并在查找 Linux 信息时拥有一个有用的起点。

在网络上查找新内核发布的权威地点是 Linux 内核归档，网址为 http://www.kernel.org/（见图 2.7）。这是 Linus Torvalds 的内核新版本发布的官方网站。但内核源代码并不是你在这里找到的信息的全部。你还可以找到指向 Linux 内核国际密码学补丁的链接、Linux 的定义，以及最重要的是，Linux 内核源代码的镜像站点列表。我之所以说最重要，是因为当发布新内核版本时，由于流量高，几乎不可能连接到网站。幸运的是，Linux 源代码的镜像非常多，如果你愿意等待一天左右，就能轻松获取最新的补丁。

## 图 2.7

Linux 内核档案。

![](img/4886c42c7629f445c7f7f3011ffbf3c3_71_0.png)

除了内核源代码之外，Linux 用户中很受欢迎的站点是 Kernelnotes，前身为 LinuxHQ。该站点维护了大量与 Linux 内核相关的信息，包括

- 用于内核最新稳定版和开发分支的源代码浏览器
- 描述有哪些新奇特功能的补丁摘要
- 指向尚未进入主流内核的补丁的补丁仓库指针

还有大量指向其他信息来源的链接，包括 Alan Cox 作为旧稳定源代码树维护者的主页；Linux 文档项目页面的镜像；以及各种 Linux 邮件列表的存档，包括 linux-kernel，所有关键内核开发者都在那里。你可以在 http://kernelnotes.com/ 访问这个精彩的网站（见图 2.8）。

## 图 2.8

Kernelnotes.org 站点。

![](img/4886c42c7629f445c7f7f3011ffbf3c3_72_0.png)

## Linuxcare

Linux 系统系统管理员的另一个宝贵资源是 Linux 世界中的相对新来者，但由一些长期 Linux 支持者支持。Linuxcare 提供一系列服务，包括

- 技术支持
- 教育与培训
- 咨询
- 开源开发

除此之外，Linuxcare 还维护一个可搜索的 Linux 知识库。他们还将为你的开源项目提供问题跟踪，并提供你可以参与的 Linux 论坛。更不用说，Linuxcare 是一个 Linux 门户网站，提供最新的 Linux 新闻和信息。最后，你可以找到戴尔、康柏和 IBM 等主要厂商认证可运行 Linux 的硬件信息。你可以在网上找到他们，网址为 http://linuxcare.com/（见图 2.9）。

## 图 2.9

Linuxcare 主页。

![](img/4886c42c7629f445c7f7f3011ffbf3c3_73_0.png)

## Linux Today

Web 上另一个 Linux 资源是 Linux Today 站点。该站点为你做了大部分的网页浏览工作。它从整个网络的新闻来源收集信息，包括关于 Linux 的文章、安全公告和内核的新版本。除了新闻发布之外，你还可以阅读 Linux Today 员工的原创社论，并利用反馈选项与 Linux 社区互动。如果你正在寻找关于谁在做什么与 Linux 相关的最新消息，Linux Today 是最佳去处。除了突发新闻之外，Linux Today 还提供查找或发布与 Linux 相关的职位的地方。通过其姊妹站点 Linux PR，你可以找到关于 Linux 相关产品或支持 Linux 的公司的新闻稿。Linux Today 可在网上找到，网址为 http://linuxtoday.com，Linux PR 可在 http://linuxpr.com 找到。在 Linux Today 可以找到的信息类型的示例可在图 2.10 中看到，其中显示了其主页。

## 图 2.10

Linux Today 主页。

![](img/4886c42c7629f445c7f7f3011ffbf3c3_74_0.png)

## 其他感兴趣的网站

已经提到的站点只是系统管理员可能用得上的众多站点中的一小部分。还有大量其他站点，既有通用目的的，也有针对 Linux 特定方面的。这些站点太多无法一一列举，但以下是我的一些个人最爱：

- http://www.slashdot.org/ Slashdot 是开发者和系统管理员可以来讨论当天技术新闻的地方。
- http://www.linux.com/ 这是一个门户站点，包含对管理员在系统调优方面特别感兴趣的部分。
- http://www.freshmeat.org/ Freshmeat 是一个优秀的站点，可以在那里找到最新的开源软件并与开发者讨论。

## 其他信息来源

除了在网上找到的资源之外，互联网为 Linux 社区提供了更多内容。其中一些资源包括携带 Linux 软件的 FTP 站点、开发者可以在其中相互交流并开发 Linux 最新功能的邮件列表，以及任何人都可以提问并分享他们对 Linux 的热情的新闻组。以下是其中一些资源的简要介绍。

## 邮件列表

如果你想与 Linux 开发人群，尤其是内核开发者交往，聚集地就是 Linux 用户可用的各种邮件列表。涵盖从硬核内核开发到将 Linux 作为商业解决方案推广等主题，Linux 邮件列表是一种订阅服务，你可以根据心情加入或离开，前提是你遵守列表所有者的规则。与新闻组和网络不同，每个人都可以按自己意愿参与，邮件列表限制稍多一些。这样做是为了保持高信噪比。列表所有者或版主可以自行决定将你从列表订阅中移除。下表列出了一些邮件列表及其提交地址：

| 邮件列表 | 提交地址 |
|---|---|
| linux-kernel | linux-kernel@vger.rutgers.edu |
| linux-smp | linux-smp@vger.rutgers.edu |
| linux-net | linux-net@vger.rutgers.edu |
| linux-gcc | linux-gcc@vger.rutgers.edu |
| linux-raid | linux-raid@vger.rutgers.edu |
| linux-scsi | linux-scsi@vger.rutgers.edu |

要订阅这些由 Majordomo 管理的列表，请发送电子邮件至 `<listname>-request@vger.rutgers.edu`，并在邮件正文中写上 subscribe。例如，要订阅 linux-kernel 邮件列表，你可以发出以下命令：

```
echo subscribe | mail linux-kernel-request@vger.rutgers.edu
```
