
# 第 4 章 Novell eDirectory 服务

为了实现和维护 eDirectory 树，你需要熟悉 Novell 的管理工具。在之前的 NetWare 版本中，实现和管理 eDirectory 树需要在安装了 Novell 客户端的计算机上运行 `Console One` 或 `NetWare Administrator` 工具。在 NetWare 6.0 中，Novell 引入了一种新的网络管理工具，称为 `iManager`。与 `Remote Manager` 类似，`iManager` 工具设计为可从任何桌面操作系统的 Web 浏览器运行，使管理员可以从任何位置执行网络管理任务。在本章中，你将使用 `iManager` 为 UAS eDirectory 树设置容器和叶对象。在第 5 章中，你将学习如何在 Windows 环境中使用 `Console One` 和 `NetWare Administrator` 来管理 eDirectory 树。

## 使用 iManager 工具

正如我们在第 1 章所学到的，Novell 在 OneNet 战略中的一个目标是在任何计算机上更容易地管理和维护组织网络，无论你正在使用的计算机类型或其连接的网络系统。在第 2 章和第 3 章中，你学习了如何使用 `Remote Manager` 通过 Web 浏览器管理 NetWare 6.5 服务器。除了 `Remote Manager`，NetWare 6.5 还附带了 `iManager 2.5` 工具，这使得通过 Web 浏览器管理和维护 eDirectory 成为可能。要运行 `iManager`，启动你的 Web 浏览器，然后输入 `iManager` URL "`/nps/iManager.html`" 。例如，如果你的服务器分配的 IP 地址是 172.20.0.65，你输入 "`https://172.20.0.65/nps/iManager.html`"。"`https`" 告诉浏览器使用安全套接层 (`SSL`) 的安全连接，而 "`/nps/iManager.html`" 指示 NetWare Web 服务器打开图 4-14 所示的 Novell `iManager` 登录窗口。

138 第 4 章 Novell eDirectory 服务

![](img/840007e8f98ea6653e5877e945c27dc6_159_0.png)

图 4-14 Novell iManager 登录窗口

在显示 `iManager` 登录窗口之前，你可能会看到一个安全警报消息，告知你即将通过安全连接查看页面。点击“确定”继续。你可能会看到另一个安全警报消息，告知你安全证书是由一家你未选择信任的公司颁发的。安全证书伴随服务器发送到客户端的密钥，用于在通过 Internet 发送之前加密数据。证书在第 11 章中有更详细的描述。

成功登录后，`iManager` 显示图 4-15 所示的主窗口。

![](img/840007e8f98ea6653e5877e945c27dc6_159_1.png)

图 4-15 Novell iManager 主窗口

在练习 4-1 中，你使用 `iManager` 设置如图 4-13 所示的 eDirectory 结构。在创建结构后，你在练习 4-2 中使用 `iManager` 创建一个别名对象，在练习 4-3 中创建用户账户。

### 活动 4-1：在 iManager 中创建 eDirectory 结构

**所需时间：** 10 分钟

**目标：** 使用 `iManager` 创建 eDirectory 组件。

**需求：**

- Windows XP 或 SUSE Linux 10 系统，使用 Internet Explorer 或启用 Java 的 Firefox
- 访问 NetWare 6.5 服务器的权限
- 管理员的区分名（distinguished user name）和密码。如果您使用的是专用服务器，您的区分名应为 `Admin.UAS`。如果您使用的是标准配置的教学服务器，您的区分名应为 `##Admin.CLASS`（## 代表分配给您的学生编号）。在此记录您的管理员账户的区分名：
  -------------------------------------------
- 您的 UAS 容器的路径。如果您使用的是标准配置的教学服务器，路径应为 `##UAS.CLASS`（## 代表分配给您的学生编号）。在此记录您的 UAS 容器的路径：
  -------------------------------------------

**注意：** 在某些 Linux Web 浏览器中，`iManager` 中的步骤执行可能需要稍长的时间。

**说明：** Eric 要求您创建一个简化的 UAS eDirectory 结构，用于测试 NetWare 6.5 服务器。在本活动中，您将使用 `iManager` 设置前文图 4-13 中所示的 eDirectory 结构。

1. 如有必要，启动您的系统并登录到本地计算机。如果您使用的是带有 Novell Client 的 Windows XP Professional 计算机，请勾选 **`仅工作站`** 复选框，以防止登录到 eDirectory 树。
2. 启动您的 Web 浏览器，并输入 URL `https://IPAddress/nps/iManager.html` 以显示 `iManager` 登录窗口。
3. 输入您的管理用户名、密码和树信息，然后单击 **登录** 按钮以显示前文图 4-15 中所示的 Novell `iManager` 窗口。
4. 在左侧的“角色和任务”窗格中，单击以展开 **eDirectory 管理** 标题。在此记录六个 eDirectory 管理选项（每行两个）：
   -------------------------------------------
   -------------------------------------------
5. 按照以下步骤在分配的容器中创建 Engineering OU：
   - a. 单击 **创建对象** 链接以显示图 4-16 中所示的“创建对象”窗口。
   - b. 在“可用对象类”列表框中，向下滚动并单击 **组织单元**，然后单击 **确定** 以显示图 4-17 中所示的“创建组织单元”窗口。

**注意：** 如果您使用的是 Linux，可能需要在使用 `iManager` 执行步骤 4 之前，使用“角色和任务”标题下方的下拉列表选择“所有类别”。有关在 Linux 上使用 `iManager` 的更多信息，请参阅附录 B。

![](img/840007e8f98ea6653e5877e945c27dc6_161_0.png)

图 4-16 创建对象窗口

![](img/840007e8f98ea6653e5877e945c27dc6_161_1.png)

图 4-17 创建组织单元窗口

   - c. 在组织单元名称文本框中输入 **`Engineering`**。
   - d. 单击 Context 文本框旁边的 **对象选择器** 按钮，使用以下两种选项之一输入分配给您的容器的路径：
     - ■ 如果您使用的是教学服务器，请导航到您在“需求”部分中记录的 UAS 容器路径。
     - ■ 如果您使用的是自己的服务器，请导航到 UAS 组织容器。
   - e. 单击 **确定** 以显示完成消息，然后单击 **确定** 返回到 Novell `iManager` 主窗口。
6. 按照步骤 5 中的过程创建 `IT` OU。
7. 按照以下步骤在 `Engineering` 容器内创建 `Mfg` OU：
   - a. 单击 **创建对象** 链接以显示“创建对象”窗口。
   - b. 在“可用对象类”列表框中，单击 **组织单元**，然后单击 **确定** 以显示“创建组织单元”窗口。
   - c. 在组织单元名称文本框中输入 **`Mfg`**。
   - d. 单击 Context 文本框旁边的 **对象选择器** 按钮，选择您在步骤 5 中创建的 `Engineering` 容器的路径。
   - e. 单击 **确定** 以显示完成消息，然后单击 **确定** 返回到 Novell `iManager` 主窗口。
8. 保持 `iManager` 打开，以便进行下一个活动。

### 活动 4-2：在 iManager 中创建叶对象

**所需时间：** 10 分钟

**目标：** 使用 `iManager` 创建 eDirectory 组件。

**需求：**

- Windows XP 或 SUSE Linux 10 系统，可访问 NetWare 6.5 服务器
- 具有在 `iManager` 中创建对象权限的 NetWare 6.5 用户名和密码
- 成功完成活动 4-1
- 您的 `UASHOST` 服务器的上下文。如果您使用的是共享教学服务器，推荐的上下文是 `##UAS.CLASS`。如果您使用的是专用服务器，上下文应为 `_UAS`。在此记录您的 `UASHOST` 服务器的上下文： ________________________
