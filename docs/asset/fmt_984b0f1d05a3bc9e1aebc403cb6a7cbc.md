
这些工具并不会阻止你常用的 UNIX 工具（如 `passwd`, `adduser`, `idisk`, `groupadd` 或 `mke2fs` 等）或手动编辑系统文件（例如 `/etc/passwd`）。但由于发行版提供的工具还会检查与其他受影响系统文件的依赖关系，你的管理工作可能会变得容易得多。

不要忘记监控一些日志日志：

- Red Hat Linux, TurboLinux: `/var/log/messages` `/var/log/dmsg`
- SuSE Linux: `/var/log/messages` `/var/log/lastlog` `/var/log/ferlog`
- TurboLinux: `/var/log`

许多知名的 UNIX 和 Linux 出版社都有关于 Linux 系统管理的书籍。此外，作为 Linux 文档项目（LDP）的一部分，你还可以找到涵盖该领域的文档，例如《适用于 IBM @server xSeries 和 Netivity 的 Linux 系统管理与备份》。

由 Lars Wirzenius 和 Joanna Oja 编写的《Linux 系统管理员指南》，以及 Steve Frampton 编写的《Linux 管理简易教程》。您可以在 `http://www.linuxdoc.org` 或 `http://www.sunsite.unc.edu/LDP/` 找到 LDP 的主页。

每个 Linux 发行版可用的系统管理工具列于表 1 所示：

表 1. 发行版及其管理工具

| 发行版 | 管理工具 |
|---|---|
| Caldera OpenLinux | Caldera Open管理系统 (COAS) |
| Red Hat Linux | `Linuxconf` |
| SuSE Linux | `YaST` (文本模式), `YaST2` (图形界面) |
| TurboLinux | `turboXXXcfg` (XXX: apache, fs, fpt, net, print, sound, time, user) `turbopkg` `turboservice` |

### 1.1.1 Caldera Open管理系统 (COAS)

`COAS` 帮助用户更好地管理他们的 Linux 系统。管理工具包括以下内容：

- 用于管理的多个用户界面
- 模块化管理工具
- 灵活、强大的管理工具
- 易于使用的管理工具

管理系统将为每个管理工具提供多个用户界面。这些界面包括命令行、`curses`、`X` 和 `Java`。有关有关 `COAS` 的更多信息，请访问以下网站：

`http://www.coas.org/index.html`

### 1.1.2 Red Hat Linux

`Linuxconf` 是红帽操作系统使用的一种复杂的管理系统。在许多方面，`Linuxconf` 与 UNIX 操作系统以及大多数其他系统上的管理方案不同。

`Linuxconf` 是一个配置实用程序（配置任务的用户界面）和一个激活器。`Linuxconf` 参与到您的 Linux 服务器或工作站的操作中。大多数情况下，它具有这些功能确保您配置的内容正在有效运行。不同的接口包括：

- 文本界面

在启动的早期，`Linuxconf` 就会接管控制，此时尚未开启很多，特别是 `X-Windows` 系统。因此需要一个文本界面。该界面可以在控制台、终端、使用 `Telnet` 会话或通过简单的调制解调器登录时工作。

- Web 界面

可以使用您喜爱的 Web 浏览器操作 `Linuxconf`。Web 浏览器的功能如书签、多页面和热链接让管理变得如梦般轻松。您不需要安装 `HTTP` 服务器本身，它是从 `inetd` 服务器启动的。

- 图形界面

`Linuxconf` 有两个 `GUI` 前端。一个用 `Java` 编写，并预计可以独立运行或从浏览器运行。另一个使用 `xxWT` 工具包，并且已经可以运行。`Linuxconf` 预计将随着一些监控和诊断功能而演进。

- 命令行界面

命令行界面很少被使用，在某些操作系统中甚至不存在。在执行特殊任务期间，没有什么能比得上脚本。一个很好的例子是 `Linuxconf` 中提供的 `DNS` 管理。

### 1.1.3 SuSE Linux

在 `SuSE` Linux 中使用的系统管理工具是 `YaST`，它是 "Yet another Setup Tool"（又一个设置工具）的缩写。它是用于配置和管理操作系统的程序。`YaST` 赋予您安装和删除系统及用户软件的能力，并执行基本的系统管理任务。对于系统管理活动列表，`YaST` 允许您执行以下操作：

- 将硬件集成到系统中的
- 内核和引导配置
- 网络配置
- 配置活动文件系统 `CD-ROM`
- 登录配置
- 设置 `usewm`（Windows 管理器）
- 用户管理
- 组管理
- 创建备份
- 系统安全设置
- 配置 `XFree86`
- 修改 `YaST` 配置文件

### 1.1.4 TurboLinux

`TurboLinux` 易于使用的 `TurboTools` 可以快速配置网络、打印机、`X-Windows`、页面更新、用户账户以及各种其他系统设置，一旦这些设置运行，将使管理变得简单。

这些工具列于表 1 中。

本章将向您概述如何在 `Caldera` OpenLinux 服务器 2 上执行最常见的管理任务。`Caldera` OpenLinux 2 具有这些设置，一旦这些设置运行，将使管理变得简单。在接下来的章节中我们将描述如何在图形环境中使用一些基础工具，特别是如何使用 `COAS` 配置您的 `Caldera` OpenLinux 系统。

> 提示

> 我们建议为 `XFree86` 设置使用 8bpp 颜色定义；否则在打开更多程序时会出现颜色问题。

![](img/4e6a76e57a4105be55d8a1cc0750b023_23_0.png)

图 7. 访问 `COAS` 工具

点击 `COAS` 图标后，你将看到一个与图 8 类似的窗口。

![](img/4e6a76e57a4105be55d8a1cc0750b023_23_1.png)

图 8. `COAS` 工具

你可以看到有几个可用的工具。我们将在接下来的章节中讨论它们。

12 用于 IBM @server xSeries 和 Netfinity 的 Linux 系统管理与备份

## 2.5 使用 kpackage 添加和删除软件包

如果你想在安装 `Caldera` OpenLinux 后添加或删除软件，或者只是检查软件是否已安装，可以使用 `kpackage` 工具来实现。你可以通过从 `COAS` 工具菜单中选择 `kpackage` 来启动它，如图 9 所示。

![](img/4e6a76e57a4105be55d8a1cc0750b023_24_0.png)

图 9. 启动 `kpackage`

启动 `kpackage` 后，你将看到一个与图 10 类似的窗口。

![](img/4e6a76e57a4105be55d8a1cc0750b023_25_0.png)

### 2.5 卸载包

如果你想卸载一个包，请选择所需的包并点击“卸载”。你将看到一个与图 11 类似的窗口。

![](img/4e6a76e57a4105be55d8a1cc0750b023_25_1.png)

11. 卸载包

14 用于 IBM @server xSeries 和 Netfinity 的 Linux 系统管理与备份

在卸载包之前，你可以更改选项，但我们建议保持默认设置不变。调整好设置后，点击“卸载”继续。检查依赖项后，软件包将将被卸载。

### 2.5.2 安装包

要安装包，点击“文件 > 打开”，你将看到一个与图 12 类似的窗口。

![](img/4e6a76e57a4105be55d8a1cc0750b023_26_0.png)

图 12. 选择要安装的包

在这里，你可以从任何可用的系统目录中选择你想要安装的包。

> 注意

> 如果你想从 `CD-ROM` 安装包，必须先挂载 `CD-ROM` 才能访问其上的文件。这可以通过在命令行提示符执行命令：`/mnt/cdrom` 完成。

第 2 章 `Caldera` OpenLinux 基础系统管理 15

选择好包后，点击“确定”继续。你将看到一个与图 13 类似的窗口。

![](img/4e6a76e57a4105be55d8a1cc0750b023_27_0.png)

在此窗口中，你可以看到包的描述。选择`文件列表`选项可以查看该包包含哪些文件。在实际安装包之前，你可以调整安装选项。选项包括：

- `升级` - 如果你正在安装一个已安装的包，则使用此项。
- `替换文件` - 如果相同位置已存在文件，将被自动替换。
- `替换包` - 在包数据库中更新包。
- `检查依赖项` - 检查是否满足了所有依赖项。
- `测试（不安装）` - 执行测试安装。

选择好选项后，点击`安装`来安装该包。安装完成后，它将出现在包列表中，如图 14 所示。

16 用于 IBM @server xSeries 和 Netfinity 的 Linux 系统管理与备份
