

提示：如果 CUPS 的标准安装中没有包含打印机驱动程序，则可能可以在互联网上为您的打印机找到正确的 ppd（Postscript打印机描述）驱动文件。应将适用于您的打印机的正确 ppd 驱动文件添加到 `/usr/share/cups/model` 目录。重启 CUPS 后，在添加打印机时即可使用新驱动程序。查找 ppd 驱动文件的方法有：

- 访问打印机制造商网站搜索 Linux 支持或 ppd 驱动下载。
- 购买支持 Linux 的打印软件：
  http://www.easysw.com/printpro
- 尝试 Adobe 提供的 Windows PPD 文件：
  http://www.adobe.com/products/printerdrivers/winppd.html
- 访问 CUPS 首页查看更多链接：
  http://www.cups.org

通过遵循第 221 页“使用 CUPS Web 界面创建打印机”中的步骤，使用正确的凭据添加打印机变得非常简单。

## 8.3.3 应用配置与安装

正如本章前面提到的，驻留 PC 上的主应用程序是 Adobe FrameMaker。有趣的是，Adobe 曾在以前提供过 Linux 版本，但从 6.0 版本起该版本已取消。由于客户端需要带有特殊插件的 FrameMaker 7.0 版本，因此无法在 Linux 上安装此应用程序。因此，我们必须找到一种方法处理这个“无法迁移”的应用程序（有关策略的详细讨论请参见第 99 页 4.7“无法迁移的应用程序”）。

我们在迁移后的 Linux 客户端上支持 FrameMaker 用户的解决方案是使用远程服务方法，通过 Windows Terminal Server 远程桌面协议 (RDP) 连接到运行在 WTS 主机上的应用程序会话。对于此类应用程序托管需求，存在其他终端服务解决方案，但对于这种小场景，我们认为使用 WTS 是令人的。我们的下一步是在终端服务器上安装该应用程序。

由于无法保证每个应用程序都能在终端服务器上运行，我们在不同的会话中多次启动 FrameMaker 进行了多次测试。我们发现，我们的 FrameMaker 版本并未针对此场景进行优化，因为运行在 WTS 主机上的每个 FrameMaker 应用程序实例都会消耗相同的系统内存。

> **重要：** 如果应用程序未针对终端服务器进行优化，则每个实例将消耗相同的内存。服务器需要足够的内存来处理预期的终端服务器负载。

与终端服务器的连接通过 `tsclient` 实现（rdesktop 应用程序的 GTK+ GUI）。通过桌面上的启动文件，可以在执行 `tsclient` 时使用配置文件。我们启动 `tsclient` 会话的命令语法如下：

```
tsclient -x $HOME/framemaker.tc
```

framemaker.tc 包含连接所需的所有信息，例如主机的 IP 地址和连接的用户名。

第 190 页图 8-1 显示了在 Linux 终端服务器客户端运行 FrameMaker 的示例窗口。

## 图像处理

在基于 Windows 的客户端上，我们使用 Jasc Paint Shop Pro 处理图像并进行截屏。由于 Paint Shop Pro 不支持 Linux，我们决定使用 GIMP 作为功能等效的 Linux 应用程序。该开源应用程序非常成熟，并能为该场景下 Windows 客户端所需的特定用途提供与 Paint Shop Pro 良好的功能等效方案。更多信息可以查阅：

http://www.gimp.org

GIMP 作为 Red Hat Desktop 标准安装的一部分包含，不需要额外配置。第 191 页图 8-2 显示了在迁移后的桌面上运行 GIMP 的屏幕截图。

## 浏览器

对于我们的迁移场景，我们决定使用 Mozilla Firefox 浏览器。Firefox 是 Mozilla 基金会的仅限浏览器项目。由于我们不需要邮件功能（这些功能由 Novell Evolution 提供），使用 Mozilla 提供的独立浏览器似乎是合理的。

我们建议您在迁移之前检查重要网站（尤其是 Web 客户端）与浏览器的兼容性。某些网站使用 ActiveX® 控件或特殊的 JavaScript™ 函数，这些功能仅由 Microsoft Internet Explorer 支持。由于我们的迁移客户端并非此类，因此可以很容易地切换并使用 Mozilla Firefox 代替 Internet Explorer。

## 邮件客户端

为了使我们的客户端迁移场景更贴真实，我们增加了一项需求：现有客户端使用 Microsoft Outlook，且其连接到 Microsoft Exchange 2000 服务器。我们的迁移任务包括从基于 Windows 的 Outlook 客户端迁移到基于 Linux 的消息客户端，后者提供类似的功能并能与有的 Exchange 2000 消息系统集成。

## 带有 Novell Exchange Connector 的 Novell Evolution

我们的迁移方案由使用 Novell Evolution 电子邮件客户端配合适用于 Microsoft Exchange Server 的 Novell Connector组成。该电子邮件客户端的架构支持为不同的组软件应用程序构建特殊连接器。一个针对 Microsoft Exchange 2000 和 2003 的连接器于 2004 年 5 月根据 GPL 条开发发布。启用 Exchange 连接器开发的关键因素是微软包含了 Exchange Outlook Web Access (OWA) 的 Web 界面。OWA 使用 WebDAV 与 Exchange 邮件存储通信。因此，通过实现 WebDAV 接口开发连接器变得可能，无需逆向 Exchange 的有的 MAP 协议。

> **限制：** 只有 Exchange 2000 和 2003 版本支持 WebDAV 连接。在本书编写，支持原生 Linux 客户端访问 Exchange 5.5 的连接器仍然可用。

我们安装了 Red Hat 提供的 Microsoft Exchange Connector RPM 包，发现设置服务器连接非常简单。

> **重要：** 在使用连接器之前，您需要检查先决条件。

关于 Novell Evolution 的更多信息可以查阅：

http://www.novell.com/products/evolution

关于 Microsoft Exchange Connector，需要在用户设置中启用 Outlook Web Access。

## 设置迁移

为了保持用户的生产效率，我们希望维护他们的设置和数据。用户本应将文档保留在网络共享上，因此我们不需要搜索整个硬盘。在用户将本地机器上保留某些笔记或文件的情况下，我们将移动“我的文档”和“桌面”目录。电子邮件存储在服务器 Exchange 账户信息中。用户书签和主页也应迁移。

## 手动迁移

首先，我们考虑手动执行此迁移。Windows 版 Firefox 可以从 Internet Explorer 导入书签和主页等自定义数据，而 Linux 则不能。因此，在 Windows 机器上安装并启动 Firefox 以开启该功能。接下来，如果未启用 Windows 共享则将其启用并共享“我的文档”和“桌面”目录。我们还共享 Firefox 设置目录，它是用户 Application Data 目录中 Mozilla 文件夹下的子目录。该目录在我们机器上的完整路径为：

```
C:\Documents and Settings\AUS06\Application Data\MozillaFirefox\xyjib4ms.default
```

作为 Windows 机器上的最后一步，启动 Microsoft Outlook 并确保所有邮件都存储在服务器上。如果有任何本地文件夹，我们在服务器上创建一个新文件夹并将邮件复制到服务器。

在 Linux 客户端上，我们使用 Nautilus 连接到 Windows 共享。我们将“我的文档”目录的内容复制到用户主目录下名为 Documents 的目录中。然后，我们将旧桌面共享中的所有数据文件（但不包括快捷方式）复制到用户桌面。接下来，启动 Firefox 初始化一个新的配置方案。然后我们在用户主目录的 `.mozilla` 文件夹中找到新的配置方案目录。它在我们机器上的完整路径为：

```
/home/ITSAUSNT+AUSRES06/.mozilla/firefox/xdch2a44.default
```

现在，我们将 Windows 机器上旧配置方案共享的所有文件复制到此文件夹中，覆盖当前存在的所有文件。最后，启动 Evolution 并向 Exchange 服务器添加新账户。

## 自动化迁移

由于有多位作者使用相似的环境，我们不想手动迁移每个桌面。相反，我们使用 Progression Desktop 来自动化迁移。

