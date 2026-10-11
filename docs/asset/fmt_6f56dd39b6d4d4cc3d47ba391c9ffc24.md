
WINE 目前处于开发阶段，并且在运行 Windows 程序方面已取得成功。大多数 Windows 3x 程序都能在没有问题的情况下下运行，但 Win32 程序（Windows 9x 和 NT 程序）的效果参差不齐。例如，据报道 Microsoft PowerPoint 2000 在 WINE 下运行得完美，但 Microsoft Outlook 完全无法工作。要获取最新的兼容 Windows 程序的程序列表，请访问 http://www.wineq.com/apps/query.cgi。

Linux 的 Windows 仿真器还不能用于生产环境，尽管它们正在迅速改进。请关注 Wine。Core 一直支持 WINE 项目，并正在开发允许 Windows 应用程序在 Windows 上运行得更好的库。Core 目前正在使用 WINE 将其 WordPerfect 办公件移植到 Linux。按照目前的开发速度，它最终将足以在没有问题的情况下运行大多数 Windows 程序。

## VMware

VMware 是一个允许 PC 在另一个操作系统内部运行另一个操作系统的程序。它目前可在 Windows NT、Windows 2000 和 Linux 下运行。这不是仿真，而是另一个操作系统的真实会话。操作系统（客户 OS）作为主操作系统（主机 OS）内部的一个独立会话运行。

启动 VMware 时，它会打开一个带有启动界面的窗口。它看起来像 PC 启动一样，带有 BIOS 设置（见图 4.1）。然后它会进入客户操作系统的运行会话（见图 4.2）。这是通过 VMware 虚拟平台实现的，它在主机操作系统内部仿真了 PC 的 BIOS。这种仿真允许在该虚拟平台之上安装任何 PC 操作系统。如果你在安装过程中遇到问题，请查看“VMware 已知问题”章节。

VMware 的 Linux 和 Windows 版本均易于安装。完整的安装说明可在 http://www.vmware.com/support/doc/（Linux）和 http://www.vmware.com/support/win/doc/（Windows）获取。

![](img/a1ad58e4259f15e8b2826ecf57a28362_46_0.png)

![](img/a1ad58e4259f15e8b2826ecf57a28362_46_0.png)

![](img/a1ad58e4259f15e8b2826ecf57a28362_50_0.png)

图 4.3 进入全局偏好界面。

你可以通过按下 `<CTRL>--ALT-<ESC>` 从全屏切换回窗口模式。但是，如果你正在使用 Direct Draw 模式，切换时光标可能会变成一个黑色方块。如果这是一个问题，你可以通过全局偏好中的“显示（Display）”选项卡切换回 GDI 模式（见图 4.4）。

# 第 4 章 • 模拟器

![](img/a1ad58e4259f15e8b2826ecf57a28362_51_0.png)

**图 4.4** 在全局偏好界面中将图形（Graphics）选项设置为 Direct Draw。

你还可以通过“优先级（Priority）”选项卡调整客操作系统的优先级（见图 4.5）。如果客操作系统使用了过多资源，可以降低优先级；也可以提高优先级以提高客操作系统的响应速度。

## VMware

![](img/a1ad58e4259f15e8b2826ecf57a28362_52_0.png)

**图 4.5** 在全局偏好中调整客操作系统的优先级。

另一个需要注意的是：如果你在 VMware 中运行 DOS 会话，即使它处于空闲状态也会占用 CPU 周期。可以通过安装 Cpuid 程序来解决，该程序可以在 http://www.bugcomputer.com/cpuidle/ 下载。请按照随附说明进行安装，不要使用 `--cpu` 选项。启用此选项可能会在某些系统上引起问题。

此外，确保在客操作系统和主机操作系统中都禁用 CD-ROM 自动播放。自动播放会不断扫描 CD 驱动器以自动播放文件，这会严重降低性能。

## FreeMW

FreeMW 是一个允许在 Linux 中打开 Windows 窗口的开源项目。虽然它目前处于早期测试阶段，但它承诺提供 VMware 的开源替代方案。它还根据 LGPL（较小的 GNU 公共许可证）授权。LGPL 和 GPL 之间的主要区别是 LGPL 对再分发的限制较少。有关 LGPL 的更多信息，请访问 http://www.gnu.org/copyleft/lesser.htm。有关 FreeMW 的更多信息，请访问 http://www.freeware.org。

## Win4Lin

Win4Lin 是“新秀”。它允许 Linux 用户在 Linux 中运行 Windows 会话，但反之不行。它比 VMware 更快，内存内存更少（只需 32 MB 内存即可轻松运行），而且售价约为 40 美元。

我有机会尝试过它的早期版本，它看起来更快，但没有 VMware 那么稳定。为它辩护，我查看的是一个测试版本，这些 应该随着时间的推移而解决。

## 结论

目前，在 Intel Linux 平台上运行 Windows 程序的最佳方法是使用 VMware。大多数 Windows 程序都能在 VMware 上无问题运行。缺点是它是闭源商业软件。它还需要你购买一份 Windows 拷贝版来运行 Windows 程序。不过，由于大多数电脑都捆带了 Windows，这可能不是一个问题。

FreeMW 是一个很有前景的开源项目，但目前开发程度尚不足以供正常使用。

WINE 项目目前只能运行有限的 Windows 程序。然而，它是免费开源的（遵循 GPL），并且进展迅速。

# 第 5 章

## 互联网应用程序

互联网已经从 20 世纪 60 年代后期政府机构的通信网络发展为 20 世纪 90 年代后期驱动美国经济的引擎。Linux 和 Windows 的不同优势使得混合环境不仅可行，而且非常有吸引力。

## FrontPage 扩展

FrontPage 是一款流行的微软网页制作工具。在网页上需要 FrontPage 扩展才能利用 FrontPage 的功能，例如：

- 允许多个用户在同一个网站和 Web 服务器上进行协作（多用户制作）。
- 允许用户通过互联网从世界上任何地方使用 PC 或笔记本电脑通过 Microsoft FrontPage 直接写入 Web 服务器（远程制作）。
- 允许用户在其网站上使用表单，并指定表单结果的处理方式，而无需用户编写自己的脚本。
- 允许用户在其网站上包含讨论组。
- 允许用户在其网站上包含访问计数器。

当然，所有这些功能可以在没有 FrontPage 扩展的情况下完成。

只有在 Microsoft FrontPage 中利用这些功能才需要 FrontPage 扩展。

微软的 IIS 会自动安装 FrontPage 扩展。Apache 不包含 FrontPage 扩展，但可以 http://www.rtr.com/fpsupdownload.html 下载。在 Linux 的 Apache 上安装 FrontPage 扩展的说明请参见 http://www.e-gineer.com/instructions/install-frontpage-extensions-for-apache-on-linux.phtml。

## 在 Web 上使用 Microsoft Office 文件

Microsoft Office 程序经常用于创建网页文档。所有的标准 Office 程序（Word、Excel 和 PowerPoint）都有“另存为 HTML”选项。这对于快速创建 HTML 文档非常方便，但 Office 倾向于在 HTML 中放入非标准字符。这些文档在非微软浏览器查看时效果很差。

用 Office 创建的 HTML 文档具有以下非标准之处：

- 数字字符末缺少分号（例如 &#061;&#061;）。
- 特殊字符的数字渲染（例如 &lt; &gt; &amp;）。
- 包含非字母数字字符的未引号 `<table>` 标签。
- PowerPoint 错误地嵌套了 `<font>` 和 `<strong>` 标签。
- PowerPoint 使用 `<ul>` 和 `</ul>` 标签来完成段落换行。
- Office 在纯文本行中缺少了 `<tr>` 标签。
- Office 在标题中放置了额外的 `<p>` 标签。
- Office 使用“段落行”，导致行溢页面。
