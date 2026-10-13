
在一个下拉菜单中选择远程条目。）对于远程 Linux 或 Unix 打印机，选择 Networked Unix (LPD)。这会显示一个用于配置远程打印机的对话框，其中包含服务器和队列的条目。对于服务器，输入控制打印机的系统的主机名。对于队列，输入该主机上打印机的设备名称。Networked Novell (NCP) 屏幕将添加用户和密码的条目。Networked Windows (SMB) 屏幕将具有不同连接打印机的条目。要添加一个，请单击 Specify 按钮以打开一个窗口，在其中可以输入共享名称、主机 IP 地址、工作组、用户和密码。Networked CUPS (IPP) 将具有 CUPS 服务器及其目录的条目。

Windows (SMB share) 打印机是位于 Windows 网络上的打印机。要访问 SMB 共享远程打印机，您需要安装 Samba 并使用 smbd 守护进程启用 Server Message Block 服务。反过来，Windows 网络上必须启用打印机共享。在打印机配置实用程序中，您需要输入共享的名称、其 IP 地址、打印机工作组的名称以及用户名和密码。共享是主机名和打印机名称的格式为 \\hostname\\printername。服务器是打印机所在的计算机。用户名和密码可以是打印机资源本身的，也可以是特定用户的访问权限。然后您可以使用打印客户端 lpr 将文件打印到 Windows 打印机。lpr 将调用 Samba 客户端 smbclient 将打印作业发送到 Windows 打印机。

**Tip** 要写入 CD-R/RW 驱动器，您可以使用 cdrecord 工具或任何几种 CD 烧录应用程序，如 KonCD。要写入 DVD-R/RW 驱动器，您可以使用 dvdrecord，这是 cdrecord 的增强版本。对于 DVD+R/RW 驱动器，您需要使用 dvd+rw 工具，如 growisofs 和 dvd+rw-format。请参阅第 30 章了解更多详情。

## X Window 系统配置：redhat-config-xfree86

如果您在 X Window 系统配置方面遇到问题，可以使用 redhat-config-xfree86 重新配置它。如果您更改了显卡，此工具也有助于更新您的 X Window 系统。只需再次运行该工具并选择适当的显卡即可。您可以通过在系统设置窗口或菜单中选择“显示”来运行 redhat-config-xfree86。redhat-config-xfree86 工具首先打开一个显示设置窗口（见图 4-4），其中包含用于选择分辨率和颜色深度的弹出菜单。

![](img/32a48d8db4c23e6e2eb70d1e5034c976_68_0.png)

图 4-4：redhat-config-xfree86 显示设置窗口

您的当前设置将已选定，同时显示此监视器和显卡信息。要更改监视器或显卡设置，请单击“高级”。这将打开一个带有标签面板的窗口，一个用于监视器，另一个用于显卡，还有一个用于多头（用于支持多显示器的显卡）。显卡面板将列出受支持的显卡，其中当前显卡被选中。在这里您还可以手动选择视频内存。监视器面板列出受支持的监视器，并提供手动输入水平和垂直频率的框。redhat-config-xfree86 工具随后生成一个名为 /etc/X11/XF86Config 的 X Window 系统配置文件。这是 X Window 系统启动时使用的文件。将在 /etc/X11/XF86Config.backup 中创建备份。

## 使用 RHN、Yum 和 APT 更新 Red Hat 和 Fedora Linux

Red Hat Fedora 的新版本每隔几个月发布一次，而 Red Hat Enterprise 则每年左右发布一次。与此同时，针对特定软件包的新更新不断准备。这些更新作为您可以从软件仓库下载并安装到系统上的更新发布。这些包括应用程序、服务器甚至内核的新版本。此类更新可能从单个软件包到整个组件不等——例如，当 GNOME、KDE 或 XFree86 发布新版本时发布的所有核心、应用程序和开发包。

更新您的 Linux 系统已成为一个非常简单的过程，使用自动更新工具。对于 Fedora Core，您可以通过访问支持 Yum（Yellowdog Update, Modified）或 apt-rpm（Advanced Package Tool RPM）更新方法的软件仓库来更新系统。Yum 使用 RPM 头来确定需要更新哪些包。您可以在 linux.duke.edu/projects/yum 了解有关 Yum 的更多信息，包括 Yum 仓库列表。APT 是一种更复杂的更新方法，最初为 Debian Linux 实现。

更新 Fedora 的最简单方法是选择系统工具菜单中的 Red Hat Network（RHN）条目启动 Red Hat Update Agent（up2date）。虽然保留给 Red Hat Enterprise Linux 使用，但在 Fedora Core 上您可以使用 Red Hat Update Agent 访问 Fedora Core Yum 仓库，让您快速更新到最新的软件版本。提供两个通道，一个用于 Fedora 发布版，一个用于更新。您可以添加第三个测试通道用于最新发布（替换 Rawhide 发布）。将显示可以更新的包列表，您可以从中选择要更新的包。要访问其他 Yum 仓库，您可以配置 /etc/sysconfig/rhn sources 文件以使用 Red Hat Update Agent 访问它们。您也可以使用 yum 命令，在 /etc/yum.conf 文件中指定 Yum 仓库。当前 Fedora Yum 仓库在此列出，随着每次发布版本号会发生变化，

- fedora.redhat.com/releases/fedora-core-1
- fedora.redhat.com/updates/released/fedora-core-1
- fedora.redhat.com/updates/testing/fedora-core-1

要更新到新的 Fedora Core 发布版，您可以从 fedora.redhat.com/releases/fedora-core 下载 Fedora Core CD-ROM ISO 映像。ISO 映像也可以使用 rpmfind 的 BitTorrent 服务下载（见 rpmfind.net/BitTorrent）。BitTorrent 提供了一种非常快速的下载 ISO 映像的方法。

对于 Red Hat Enterprise Linux，您可以通过作为 Red Hat Network 的一部分注册来自动更新系统。Red Hat Network 服务现在仅支持 Red Hat Enterprise Linux，不支持 Fedora Core Linux（尽管可以配置 RHN 工具以访问 Fedora 仓库）。使用 Red Hat Network Registration 客户端注册并配置对 Red Hat Network 的访问是一个非常简单的过程。Red Hat Network 是随您购买企业包而包含的订阅服务。一旦您在 Red Hat Network 上注册，您就可以使用 Red Hat Update Agent 几乎自动地下载和安装 Red Hat Enterprise 更新。

**Tip** 如果您安装了 Ximian Desktop（见第 6 章），您可以使用 Ximian 的 Red Carpet 更新实用程序来更新系统。

![](img/32a48d8db4c23e6e2eb70d1e5034c976_70_0.png)

## ABC Amber CHM Converter 试用版

请注册以移除此横幅。

http://www.processestext.com/abcchm.html

## 安装软件包

现在您知道如何启动 Linux 并访问 root 用户帐户，您可以安装任何其他想要的软件包。安装软件是由 root 用户执行的管理员功能。除非您在安装期间选择安装所有包，否则仅在您的系统上安装了 Linux 用户可用的众多应用程序和实用程序中的一些。在 Red Hat 上，您可以使用 redhat-config-packages 工具或 rpm 命令轻松地从系统中安装或删除软件。或者，您可以通过下载并编译其源代码来安装软件。使用源代码安装软件的程序已简化为只需几个命令，尽管您在根据特定系统定制应用程序方面具有很大的灵活性。

许多发行版，包括 Red Hat、Mandrake 和 SuSE，都使用 Red Hat Package Manager（RPM）将 Linux 软件组织成可自动安装或删除的包。RPM 软件包就像软件应用程序自己的安装程序一样运行。Linux 软件应用程序通常由必须安装在不同目录中的多个文件组成。程序本身很可能放置在名为 /usr/bin 的目录中，在线手册文件放在另一个目录中，库文件放在另一个目录中。此外，安装可能需要修改系统上的某些配置文件。RPM 软件包会为您执行所有这些任务。此外，如果您后来决定不想要特定应用程序，您可以卸载包以从系统中删除所有文件和配置信息（有关更多详细信息，请参阅第 29 章）。

您 CD-ROM 上的软件包尽管很丰富，但仅代表 Linux 可用软件包的一小部分。您可以从 sourceforge.net 等在线软件站点下载其他软件。sourceforge.net 站点不仅分发软件，而且还是大量开源软件项目的首要开发站点。在过去几年中，许多 Linux 软件项目已迁移到 sourceforge.net。您也可以从 freshmeat.net 或 rpmfind.net 找到许多最新的 Linux 应用程序。在这里，您可以链接到这些应用程序的原始开发站点并下载最近版本的文档。表 4-2 列出了几个 Linux 软件站点。对于支持 RPM 包的 SuSE、Mandrake 和 Red Hat 等发行版，您可以在在线仓库 rpmfind.net 上找到软件的 RPM 包版本。这里的包按发行版、组和名称编入索引。这包括每个发行版的包，包括这些发行版的以前版本。

表 4-2：Linux 软件站点

| 互联网站点 | 描述 |
|---|---|
| ftp.redhat.com | Red Hat 发行版 RPM 包 |
| rpmfind.net | RPM 包仓库 |
| sourceforge.net | Source Forge 开源软件仓库和开发站点 |
| freshmeat.net | 新 Linux 软件 |
| apps.kde.com | KDE 软件应用程序 |
| www.gnome.org | GNOME 软件应用程序 |

### 使用 redhat-config-packages 安装包

redhat-config-packages 工具为管理您 Red Hat 发行版提供的 Red Hat RPM 包提供了一个有效且易于使用的界面，无论您是从 CD-ROM、DVD-ROM、硬盘还是网络安装的。它在任何窗口管理器上运行，包括 GNOME 和 KDE。您可以使用系统设置窗口中的“添加/删除应用程序”图标访问 redhat-config-packages。这将打开一个“添加和删除软件”窗口，显示左侧面板栏，其中包含“安装软件”和“删除软件”图标，以及一个面板，根据所选图标显示要安装的软件或要删除的软件。最初将显示“安装软件”图标，显示包含可安装包的软件组列表。视图菜单将让您在组视图和单个包视图之间切换。如果您知道要安装的单个包的名称，您可以使用该包
