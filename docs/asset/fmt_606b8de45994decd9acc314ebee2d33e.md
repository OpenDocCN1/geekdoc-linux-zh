
Windows 用户仅向 Samba 进行身份验证（通过配置的任何方式）。如果 Samba 与 CUPS 运行在同一主机上，你只需允许“localhost”进行打印。如果它们运行在不同的机器上，你需要确保 Samba 主机能够访问 CUPS 上的打印功能。

### 21.8 网络 PostScript RIP

本节讨论在客户端使用具有 CUPS-PPD 的 PostScript 驱动程序的服务器配置中，CUPS 过滤器的使用。

PPD 可以控制所有打印设备选项。如果你拥有 PostScript 打印机，制造商通常会提供这些文件；也就是说，PPD 文件始终是 MS Windows 或 Apple Mac OS 系统上 PostScript 打印机驱动程序的一个组成部分。它们是包含用户可选打印选项的 ASCII 文件，并映射为适用于目标打印机的相应 PostScript、PCL 或 Pjl 命令。打印机驱动程序的 GUI 对话框会将这些选项“即时”转换为用户可选择的按钮和下拉列表。

CUPS 可以从任何 Windows（建议使用 NT）PostScript 驱动程序加载 PPD 文件，无需任何转换，并处理这些选项。有一个网络浏览器界面用于打印选项（选择 `<http://localhost:631/printers/>` 并点击其中一个 `配置打印机` 按钮即可查看），或者有一个命令行界面（参见 `man lpoptions` 或查看你的系统是否有 `lphpel`）。在 Linux/UNIX 上还有一些不同的 GUI 前端，它们可以向用户展示 PPD 选项。通常，PPD 选项旨在由真实 PostScript 打印机上的 PostScript RIP 进行评估。

#### 21.8.1 UNIX 上非 PS 打印机的 PPD

CUPS 在使用 PPD 时并不局限于“真实”的 PostScript 打印机。CUPS 开发者扩展了 PPD 概念的范围，使其也可以通过 CUPS-PPD 描述非 PostScript 打印机可用的设备和驱动程序选项。

这是合乎逻辑的，因为 CUPS 包含一个功能完备的 PostScript 解释器（RIP）。该 RIP 基于 Ghostscript。它可以处理从客户端接收到的所有 PostScript（以及许多其他文件格式）。所有面向非 PostScript 打印机的 CUPS-PPD 都包含一个以关键字 `*cupsFilter` 开头的额外行。该行告知 CUPS 打印系统使用哪个打印机特定过滤器来解释提供的 PostScript。因此，CUPS 使所有打印机在客户端看来都像 PostScript 设备，因为它可以作为这些打印机的 PostScript RIP，将接收到的 PostScript 代码处理为合适的点阵打印格式。

#### 21.8.2 Windows 上非 PS 打印机的 PPD

CUPS-PPD 也可以用于 Windows 客户端，叠加在“核心”PostScript 驱动程序之上（现在推荐使用用于 Windows NT/2000s/XP 的 CUPS PostScript 驱动程序；你也可以使用 Adobe 的驱动程序，但有限制）。此功能使 CUPS 能够执行其他作业排队系统无法做到的几项操作：

- 作为网络 PostScript RIP，以统一的方式处理来自所有客户端平台的打印文件。
- 作为中央会计和计费服务器，因为所有文件都通过 postps 过滤器传递，因此会被记录在 CUPS `page.log` 文件中。*注意*：对于“raw”打印作业，这种情况不会发生，因为它们按定义始终未被过滤。
- 使客户端能够使用单一的 PostScript 驱动程序进行整合，即使目标打印机种类众多。

在 Windows 客户端上使用 CUPS PPD 使它们能够像 UNIX 客户端一样控制所有打印任务设置。

## 21.9 将 Windows 终端服务器 (WTS) 作为 CUPS 客户端

这种设置可能对在 WTS 环境中遇到严重问题的人们特别感兴趣。WTS 通常需要安装大量非 PostScript 驱动程序才能运行其客户机种类繁多的不同打印机型号。这往往伴随着系统稳定性大幅下降的代价。

### 21.9.1 运行在“内核模式”下的打印机驱动程序导致许多问题

运行在“内核模式”下的 Windows NT 打印机驱动程序，如果驱动程序本身不够稳定且未充分测试，会给系统稳定性带来高风险。而市面上存在大量质量低劣的驱动程序！特别臭名昭著的是那个 PCL 打印机驱动程序的例子，它额外包含一个声音模块，通过声卡通知用户其任务已完成。我还需要说它经常可靠地导致“蓝屏死机”吗？

PostScript 驱动程序通常经过充分测试。尽管它们也运行在内核模式下，但已知它们不会导致任何问题。这可能是因为到目前为止只有两种不同的 PostScript 驱动程序：Adobe 的和 Microsoft 的。两者都经过充分测试，在 Windows 上具有你所能想象的最高的稳定性。CUPS 驱动程序源自 Microsoft 的驱动程序。

### 21.9.2 变通方法带来严重限制

为了尝试绕过问题，站点管理员已不得不将 WTS 上允许的已安装驱动程序限制为一个通用 PCL 驱动程序和一个 PostScript 驱动程序。然而，这限制了客户端可用的打印机选项数量。通常，从一个标准纸盒中他们只能获得单面打印，而如果使用不同的驱动程序，他们的设备本可以表现得更好！

### 21.9.3 CUPS：一块“魔石”？

使用通过 CUPS-PPD 启用的 PostScript 驱动程序，似乎是克服所有这些缺点的一种非常优雅的方式。根据你使用的 Windows OS 版本，现在最多有三种不同的 PostScript 驱动程序可供选择：Adobe、Microsoft 和 CUPS PostScript 驱动程序。已知它们都不会在 WTS 上造成重大的稳定性问题（即使与许多不同的 PPD 一起使用）。客户端将能够（再次）选择纸盒、双面打印和其他设置。然而，这也有一定的代价：作为客户端的 PostScript RIP 的 CUPS 服务器，比你仅仅作为“raw 排队”设备时需要更多的 CPU 和 RAM。此外，虽然最初的反馈看起来很有希望，但这种设置尚未经过广泛测试。

### 21.9.4 即使在核心模式下也没有重大问题的 PostScript 驱动程序

在 W200x 和 XP 上更近期的打印机驱动程序不再运行在内核模式（与 Windows NT 不同）。然而，这两个操作系统仍可使用运行在内核模式的 NT 驱动程序（你大致可以通过“W32X86”子目录中“2”目录下的驱动程序是“旧”驱动程序来判断）。正如之前所说，Adobe 和 Microsoft 的 PostScript 驱动程序均已知不会导致任何稳定性问题。CUPS 驱动程序源自 Microsoft 的驱动程序。这样做有一个简单的原因：用于 Windows NT 的 MS DDK（设备开发套件）（曾经免费提供给 Visual Studio 许可方，“Classical Printing NT”曾经免费提供给 Visual Studio 20. 许可方）包含 Microsoft 驱动程序的源代码，并且 Visual Studio 的许可方被允许将其用于和修改于他们自己的驱动程序开发工作。这就是 CUPS 团队所做的。许可证不允许他们公布全部源代码。然而，他们已在 GPL 下发布了“diff”（差异文件），如果你是“用于 Windows NT 的 MS DDK”的所有者，你可以自己检查驱动程序。

## 21.10 配置 CUPS 以用于驱动程序下载

正如我们之前所说，所有以前已知的在 Samba 服务器上准备客户端打印机驱动程序以下载并与 Point`print` 共存的 Windows 工作站的方法，在 CUPS 中同样有效。这些方法在第 20 章“传统打印支持”中描述过。实际上，这是纯粹的 Samba 事务，仅涉及 Samba-Windows 客户端关系。

### 21.10.1 cupsaddsm：未知的实用程序

`cupsaddsm` 实用程序（随所有当前 CUPS 版本提供）是将打印机驱动程序传输到 Samba `[p*r*i*n*t*s]` 共享的一种替代方法。记住，这个共享是客户端期望存放并设置用于下载和安装的驱动程序的地方。它使得共享任何（或所有）已安装的 CUPS 打印机变得非常简单：`cupsaddsm` 可以使用 Adobe PostScript 驱动程序，也可以使用新开发的用于 Windows NT/W200x/XP 的 CUPS PostScript 驱动程序。`cupsaddsm` 不适用于任意供应商的打印机驱动程序，但只适用于其 man 页面中命名的确切驱动程序文件。

CUPS 打印机驱动程序可从 CUPS 下载站点获取。其包名称为 `cups-samba-[version].tar.gz`。它优于 Adobe 驱动程序，因为它具有一系列优势：

- 它支持更精确的页面会计。
- 它支持在所有打印机上打印横幅页和页面标签。
- 它支持设置一系列任务 IPP 属性（如任务优先级、页面标签和任务计费）。
