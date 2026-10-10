
## 使用 NetWare Administrator

为了操作目录树，您需要熟悉 Novell 的管理实用程序。在 NetWare 的早期版本中，创建和管理 eDirectory 树需要在安装了 Novell Client 的计算机上运行 NetWare Administrator 实用程序。在 NetWare 5.0 中，Novell 推出了 ConsoleOne 实用程序，它是用 Java 语言编写的，因此可以在包括 NetWare 服务器控制台在内的多个平台上运行。随着 NetWare 6.0 的发布，Novell 推出了一种名为 iManager 的新型网络管理工具。尽管 iManager 1 版只能执行有限的任务，但网络管理员可以使用它通过 Web 浏览器管理他们的 eDirectory 树，而不必依赖安装了 Novell Client 的计算机。由于 iManager 不需要在基于 Windows 的计算机上运行 Novell 客户端，因此它现在是 Novell NetWare 愿景的重要组成部分，使得可以从连接网络上的任何客户端计算机进行网络管理。默认情况下，只有 Admin 用户有权使用 iManager。其他用户若要运行 iManager，需要通过 Novell 的基于角色的服务（RBS）为其分配 iManager 角色。您将在第 7 章中学习更多关于使用 RBS 的内容。

每种实用程序都有其优缺点。例如，ConsoleOne 是一种基于 Java 的实用程序，可以在包括服务器控制台在内的多个操作系统上运行。NetWare Administrator 的优势在于在旧版基于 Windows 的计算机上提供高性能，而 iManager 的优势在于可以通过标准 Web 浏览器从任何网络计算机使用。由于这些实用程序具有不同的功能，CNA（Novell Certified Administrator）应熟悉所有这三种工具。虽然 iManager 是本章中用于处理 eDirectory 对象的主要实用程序，但您还将学习如何使用 NetWare Administrator 和 ConsoleOne 执行网络任务。在第 4 章中，您学习了如何使用 iManager 访问和创建 eDirectory 树中的对象。在接下来的章节中，您将学习如何安装 ConsoleOne 和 NetWare Administrator，然后使用这些实用程序访问您在第 4 章中创建的 eDirectory 树结构。

### 活动 5-1：创建 NetWare Administrator 快捷方式

**所需时间：** 5 分钟

**目标：** 安装并配置 NetWare Administrator。

**要求：** 要执行此活动，您需要具备以下条件：

-   来自第 4 章且已安装 Novell Client 的 Windows XP 计算机
-   专用服务器或与其他学生共享的课堂服务器和 eDirectory 树。记录您的实验环境以下信息：
    -   服务器名称：
    -   eDirectory 树名称：
    -   分配给您的管理用户名：
    -   您的 UAS 组织（Organization）的名称和上下文（context）：

**描述：** 作为网络管理员，Eric Kenton 在从旧版 Windows 桌面工作时，经常使用 NetWare Administrator 来设置和维护 UAS 网络系统。为了更轻松地启动 NetWare Administrator，Eric 创建了一个 Windows 桌面快捷方式，然后将 NetWare Administrator 添加到开始菜单中。在此活动中，您将学习如何在您的桌面和开始菜单中添加 NetWare Administrator 快捷方式。

1.  如有必要，启动您的 Windows XP 计算机，并使用您的管理用户名和密码登录到 eDirectory。
2.  按照以下步骤打开 `F:\Public\Win32` 文件夹：
    a.  双击**我的电脑**。
    b.  双击 **F:** 驱动器。
    c.  双击 **Public** 文件夹，然后双击 **Win32** 文件夹。
3.  右键单击 **Nwadm32** 程序，然后单击**发送到桌面 (创建快捷方式)** 以在桌面上创建快捷方式。
4.  关闭 Win32 对话框。此时桌面上应出现 Nwadm32 的快捷方式。
5.  要将 Nwadm32 添加到您的开始菜单，右键单击**开始**，然后单击**打开**以打开开始菜单窗口。
6.  右键单击桌面上的 **Nwadm32** 快捷方式，并将其拖拽到开始菜单窗口。
7.  释放鼠标右键，然后在该快捷方式上出现的菜单中单击**复制到这里**，以便将快捷方式的副本放置在您的开始菜单中。
8.  关闭开始菜单窗口，并保持登录状态以进行下一个活动。

### 活动 5-2：使用 NetWare Administrator 进行浏览

**所需时间：** 10 分钟

**目标：** 使用 NetWare Administrator 浏览 eDirectory 树，查看对象属性并创建新对象。

**要求：** 同活动 5-1，且已完成活动 4-1 和 4-2

**描述：** 由于其良好的性能以及能够打开多个浏览窗口的功能，Eric 定期使用 NetWare Administrator 来管理他的树结构。在此活动中，您将学习如何启动 NetWare Administrator，打开多个浏览窗口，更改上下文以及查看 eDirectory 树中的对象。

1.  通过单击**开始，所有程序，指向 Nwadm32 的快捷方式** 来启动 NetWare Administrator。NetWare Administrator 实用程序拥有许多用于不同任务的工具栏按钮，如图 5-1 所示。如有必要，阅读“欢迎使用 NetWare Administrator”窗口中的提示，然后单击**关闭**。
2.  启动 NetWare Administrator 后，您将看到一个类似于图 5-2 中的浏览窗口。
3.  通过单击**关闭**按钮关闭浏览窗口。
4.  按照以下步骤打开指向树根部的浏览窗口：
    a.  要打开一个新的浏览窗口，从菜单中单击**工具，NDS 浏览器** 以打开“设置上下文”对话框。请注意，上下文文本框显示了您在 UAS_Tree 中的计算机当前上下文。

![](img/840007e8f98ea6653e5877e945c27dc6_187_0.png)

图 5-1 NetWare Administrator 工具栏

![](img/840007e8f98ea6653e5877e945c27dc6_187_1.png)

图 5-2 NetWare Administrator 浏览窗口

    b.  单击上下文文本框旁边的**浏览**按钮，以打开图 5-3 中显示的“选择对象”对话框。右侧的“浏览上下文”部分用于更改您的当前上下文。左侧的“可用对象”部分列出所选上下文中的对象。

![](img/840007e8f98ea6653e5877e945c27dc6_188_0.png)

**图 5-3** NetWare Administrator 选择对象对话框

    c.  要将当前上下文提升一级，请在“浏览上下文”部分中双击**上箭头**。然后，“可用对象”部分将显示树中 [Root] 容器中的所有对象。
    d.  要将“浏览上下文”部分的上下文设置为树的根部，请双击“可用对象”部分中的 [Root] 对象。
    e.  单击**确定** 以保存新的上下文设置。此时浏览窗口应显示所有组织（Organization）容器。
    f.  记录浏览窗口中显示的所有组织对象的名字和类型：
        \_\_\_\_\_\_
        \_\_\_\_\_\_
        \_\_\_\_\_\_
5.  查看 UAS 容器中的所有对象。如果您使用的是专用服务器，只需在浏览窗口中双击 **UAS**。如果您使用的是共享的课堂服务器，请展开 **CLASS** 组织，然后双击 **UAS** OU（组织单元）。记录 UAS 容器中所有组织单元对象的名字：
    \_\_\_\_\_\_
    \_\_\_\_\_\_
    \_\_\_\_\_\_
6.  记录 UAS 组织中所有组对象的名字：
    \_\_\_\_\_\_
    \_\_\_\_\_\_
    \_\_\_\_\_\_
7.  双击 **UAS** 容器将其折叠。
8.  通过从菜单中单击**对象，退出** 来关闭 NetWare Administrator，并保持登录状态以进行下一个活动。

## 使用 ConsoleOne

ConsoleOne 仍然是管理 NetWare 6.5 eDirectory 树大多数方面的主要基于 Windows 的实用程序。除了安装 Novell Client 外，ConsoleOne 还需要至少 128 MB 的 RAM 和 300 MHz 的处理器才能有效运行。虽然可以直接从 NetWare 6.5 服务器的 SYS 卷运行 ConsoleOne 软件，但通过网络加载 ConsoleOne 文件的速度较慢且占用网络带宽。如果在本地计算机上安装，启动 ConsoleOne 会快得多。在接下来的活动中，您将在 Windows 桌面上安装 ConsoleOne，然后练习使用它来浏览 Universal AeroSpace 树。

