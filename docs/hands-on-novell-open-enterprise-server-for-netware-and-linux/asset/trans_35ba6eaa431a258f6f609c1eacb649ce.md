

## 活动 14-10：创建存储位置对象

**所需时间：** 15 分钟

**目标：** 使用 iManager 创建一个存储位置对象。

**要求：** 来自 Windows XP 的 Internet Explorer 或来自 SUSE Linux 10 的支持 Java 的 Firefox

**说明：** Eric 希望用户能够通过网络存储（NetStorage）访问他们的用户主目录。在此活动中，您使用 iManager 创建用于用户主目录的存储位置对象，从而使用户主目录可用。

- 使用您的本地管理员用户名和密码登录到您的 Windows XP 系统，或使用 root 用户名和密码登录到您的 SUSE Linux 服务器。
- 启动您的 Web 浏览器，启动 iManager，并使用您的管理员用户名和密码登录到 iManager。
- 展开 **文件访问 (NetStorage)** 标题，并点击 **新建存储位置** 链接以显示如图 14-16 所示的 *存储位置：创建对象* 窗口。
- 在 *对象名称* 文本框中，输入 **storLoc_hostname**（将 *hostname* 替换为 SUSE Linux 服务器的名称）。
- 在 *显示名称* 文本框中，输入 **home**。这是显示在用户的 NetStorage 窗口中的名称。
- 在 *目录位置* 文本框中，输入 **ssh:/IPaddress/home**（将 *IPaddress* 替换为您的 SUSE Linux 服务器的 IP 地址）。
- 点击 Context 文本框旁边的 **对象选择器** 按钮，导航到并点击您的 **UAS** 容器。
- 点击 **创建** 以创建该对象并返回 iManager 主窗口。
- 退出 iManager，并保持登录状态，以便进行下一个活动。

![](img/840007e8f98ea6653e5877e945c27dc6_593_0.png)

图 14-16 创建一个存储位置对象

## 活动 14-11：访问 NetStorage

**所需时间：** 15 分钟

**目标：** 使用 NetStorage 访问 SUSE Linux 服务器。

**要求：** 完成活动 14-8 以及一台 Windows XP 或 SUSE Linux 10 计算机

**说明：** 在此活动中，您使用您的 Web 浏览器通过 LUMUser 用户名和密码登录来测试 NetStorage。

- 如有必要，使用您的本地管理员用户名和密码登录到您的 **Windows XP** 系统，或使用 root 用户名和密码登录到您的 **SUSE Linux** 服务器。
- 启动您的 Web 浏览器并输入 URL `https://IPaddress/NetStorage`（将 *IPaddress* 替换为您的 SUSE Linux 服务器的 IP 地址）。
- 使用您的 LUMUser 用户名和密码登录到 NetStorage。
- 列出您可以看到的文件和目录：_______________________________
- 退出 NetStorage，并保持您的系统运行以便进行下一个活动。

## SUSE LINUX 中的 IPRINT 服务

如图 14-17 所示，iPrint 系统既可以用于 SUSE Linux，也可以用于 NetWare 6.5。可以使用 HTTP 或本地操作系统的原生打印机安装，在 Linux、Windows 或 Macintosh 计算机上安装打印机。当使用 HTTP 时，计算机上的 Web 浏览器将请求定向到安装在 iPrint 服务器上的打印机页面。OES 服务器随后使用 Linux 中的 Driver Store（驱动程序存储库）对象或 NetWare 中的 Broker（中介）对象，将正确的打印机驱动程序发送到计算机。

安装打印机后，打印作业通过 IPP 协议发送到 Print Manager（打印管理器）软件，该软件使用打印 spooler（假脱机）将打印作业定向到网络连接的打印机。Linux 和 NetWare 中 iPrint 的主要区别在于，您必须在 SUSE Linux 系统上创建一个 **Driver Store**（驱动程序存储库）对象来存储打印驱动程序。此对象取代了 NetWare 中使用的 Broker（中介）对象。在 SUSE Linux 中设置 iPrint 的基本步骤如下：

- 创建一个 Driver Store（驱动程序存储库）。
- 从 Windows 平台向 Driver Store（驱动程序存储库）添加打印驱动程序。
- 创建一个 Print Manager（打印管理器）对象。
- 创建 iPrint 打印机对象。

在以下活动中，您将在您的 SUSE Linux 系统上设置 iPrint。

![](img/840007e8f98ea6653e5877e945c27dc6_594_0.png)

**图 14-17 在 SUSE Linux 中使用 iPrint**

## 活动 14-12：创建驱动程序存储库

**所需时间：** 10 分钟

**目标：** 使用 iManager 设置 iPrint 服务。

**要求：** 来自 Windows XP 的 Internet Explorer 或来自 SUSE Linux 10 的支持 Java 的 Firefox

**说明：** AeroDyn 部门需要从公司网络内部和外部访问多个网络打印机。在此活动中，您将学习如何创建驱动程序存储库，以在 SUSE Linux 服务器上设置 iPrint。

- 如有必要，使用您的管理员或 root 用户名和密码登录到您的 Windows XP 或 SUSE Linux 计算机。
- 启动您的 Web 浏览器，启动 iManager，并使用您的管理员用户名和密码登录到 iManager。
- 按照这些步骤创建一个用于容纳打印驱动程序的 Driver Store（驱动程序存储库）对象：
  - 展开 **iPrint** 标题，并点击 **创建驱动程序存储库** 链接以显示如图 14-18 所示的 *创建驱动程序存储库* 窗口。

![](img/840007e8f98ea6653e5877e945c27dc6_595_0.png)

**图 14-18** *创建驱动程序存储库* 窗口

  - 如有必要，通过点击容器名称文本框旁边的 **对象选择器** 按钮并点击您的 **UAS** 容器来输入一个容器名称。
  - 在驱动程序存储库名称文本框中，输入 **UASPrint_Drivers**。
  - 在目标服务器文本框中输入您的 Linux 服务器的 IP 地址。
  - 点击 eDir 服务器名称文本框旁边的 **对象选择器** 按钮，并点击您的 SUSE Linux 服务器。
  - 点击 **确定** 以创建驱动程序存储库并显示完成消息。

> **注意** 以下步骤需要在一台 Windows XP 客户端上执行。

- 如有必要，使用以下步骤在您的 Windows XP 计算机上安装 iPrint 客户端。（如果您在第 8 章中安装了 iPrint 客户端，则可以跳过至活动 14-13。）
  - 如有必要，登录到您的 Windows XP 计算机并点击 **仅工作站** 复选框。
  - 启动 Internet Explorer 并输入 URL `http://IPAddress/ipp`（将 *IPAddress* 替换为您的 SUSE Linux 服务器的 IP 地址）。
  - 点击 **安装 iPrint 客户端** 链接。
  - 点击 **打开** 选项以启动安装向导。
  - 当显示“安装 iPrint 客户端”窗口时，点击 **下一步** 以开始安装过程。
  - 客户端安装完成后，点击 **完成** 返回 iPrint 窗口。关闭您的 Web 浏览器。
- 保持 iManager 打开状态，以便进行下一个活动。

## 活动 14-13：创建打印管理器对象

**所需时间：** 10 分钟

**目标：** 使用 iManager 设置 iPrint 服务。

**要求：** 一台 Windows XP 或 SUSE Linux 10 计算机；完成活动 14-12

**说明：** 在此活动中，您将学习如何创建打印管理器，以在您的 SUSE Linux 系统上设置 iPrint。

- 如有必要，展开 **iPrint** 标题，然后点击 **创建打印管理器** 链接以显示“创建打印管理器”窗口（见图 14-19）。

![](img/840007e8f98ea6653e5877e945c27dc6_596_0.png)

- 在打印管理器名称文本框中输入 **OES_PMgr**。
- 点击 eDir 服务器名称文本框旁边的 **对象选择器** 按钮，并点击您的 SUSE Linux 服务器。
- 点击驱动程序存储库名称文本框旁边的 **对象选择器** 按钮，并点击您在活动 14-12 中创建的 **UASPrint_Drivers** 对象。
- 点击 **IP 地址** 选项按钮，并在文本框中输入您的 SUSE Linux 服务器的 IP 地址。
- 点击 **确定** 以创建打印管理器对象，并保持 iManager 打开状态以便进行下一个活动。

## 活动 14-14：创建打印机对象

**所需时间：** 10 分钟

**目标：** 使用 iManager 设置 iPrint 服务。

**要求：** 完成活动 14-13

**说明：** 在此活动中，您将学习如何创建打印机对象，这些对象可用于在您的 SUSE Linux 系统上设置 iPrint。

- 如有必要，展开 **iPrint** 标题，然后点击 **创建打印机** 链接以显示如图 14-20 所示的“创建打印机”窗口。
- 在打印机名称文本框中，输入 **OES_P1**。
- 为您的打印机输入适当的信息，并点击 **下一步** 以创建打印机对象。
- 关闭所有打开的窗口，并注销。

