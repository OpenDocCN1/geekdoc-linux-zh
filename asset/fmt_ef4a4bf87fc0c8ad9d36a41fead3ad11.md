
- 2. 输入您的管理用户名和密码，然后单击 `Login` 按钮以显示如图 3-32 所示的 iManager 主窗口。（如果您看到“Secret Store is currently locked”消息，请在 Old Password 文本框中输入您的管理密码并单击 `Continue`。如果此消息第二次出现，请单击 `Close`。）

![](img/840007e8f98ea6653e5877e945c27dc6_128_1.png)

图 3-32 iManager 主窗口

- 3. 向下滚动“角色和任务”窗格，然后单击展开 `NMAS`。

- 4. 单击 `NMAS Login Methods` 链接以打开如图 3-33 所示的 NMAS 登录方法窗口。

- 5. 通过以下步骤查看您 NMAS 登录配置容器的当前状态：
    - a. 在“选择登录方法”下拉列表中，单击 `Simple Password` 选项。
    - b. 单击 `View Login Method Properties` 按钮以显示简单密码配置窗口。在以下行中记录支持的平台：
    ____________________________________________________________
    ____________________________________________________________

![](img/840007e8f98ea6653e5877e945c27dc6_129_0.png)

- 6. 按照以下步骤在您的 Admin 帐户上启用简单密码：
    - a. 单击 `NMAS Users` 链接以显示“选择用户”窗口。
    - b. 单击 `Object Selector` 按钮，单击您的 `Admin` 帐户，然后单击 `OK` 以显示 NMAS 用户窗口，类似于图 3-34。

![](img/840007e8f98ea6653e5877e945c27dc6_129_1.png)
    - c. 单击 `Simple Password` 选项，然后在“设置简单密码”和“确认简单密码”文本框中输入新密码。
    - d. 单击 `OK` 返回 iManager 主窗口。

- 7. 单击 `Exit` 按钮以结束您的 iManager 会话。您的 Admin 用户以及您创建的任何新用户现在应该能够使用相同的密码从 Microsoft 或 Novell 客户端登录。

### 使用通用接口文件系统（CIFS）客户端

访问其他基于 Windows 的计算机上的共享资源和服务需要 Microsoft 客户端。Microsoft 客户端在 Windows 9x 上是可选的，但在 Windows 2000 和 XP 中会自动安装。由于 Microsoft 客户端在台式计算机上非常普遍，因此它是访问无需额外 Novell 服务的计算机上的 NetWare 文件服务的自然选择。例如，在 UAS 网络中，装运和收货部门的计算机只需要文件和打印服务来访问 NetWare 服务器上的库存文件并打印装运标签。因此，Eric 决定通过仅使用 Microsoft 客户端来简化这些计算机的配置。

如你在第 1 章中所了解，在对等网络中，Windows 服务器被组织到工作组中。为了让 Microsoft 客户端访问 NetWare 服务器，`NFAP` 使 NetWare 6.5 服务器在 Windows 客户端看来就像工作组中的另一台 Windows 服务器。在安装期间，会自动为 NetWare 6.5 服务器分配一个 Microsoft 服务器名称和工作组，以及要与 Microsoft 客户端共享的卷。默认方法是共享所有卷，并将 NetWare 服务器放置在 `WORKGROUP` 工作组中，使用包含 NetWare 服务器名称后跟下划线字符和“W”的 Microsoft 服务器名称。例如，UASHOST 的 Microsoft 服务器名称为 `UASHOST_W`。可以使用第 6 章中描述的 ConsoleOne 更改默认的 CIFS 参数。

Windows 用户可以通过在 Windows 资源管理器中浏览网络或输入数据卷的统一命名约定（UNC）路径来访问 NetWare 服务器上的数据卷。`路径`通过列出通向对象（如文件或目录）的组件来定义对象的位置。例如，到文件的完整路径通常由服务器名称、卷名称和目录名称组成。UNC 路径在服务器名称前有两个反斜杠，并用一个反斜杠分隔服务器和共享卷名称。例如，`UASHOST_W` 服务器上 `CORP` 卷的名称为 `\\UASHOST_W\CORP`。在活动 3-8 中，你使用 UNC 路径将驱动器映射到 `UASHOST_W` 服务器的 `CORP` 卷。

当运行 Microsoft 客户端的计算机尝试访问运行 `NFAP` 的 NetWare 服务器时，Windows 客户端会以与尝试登录 Microsoft 服务器相同的方式将其本地用户名和密码提交给 NetWare 服务器。如果用户帐户和密码存在于 NetWare 服务器上，则授予访问权限。如果 NetWare 服务器上的用户帐户和密码与登录 Microsoft 客户端的用户帐户和密码不匹配，则会打开“输入网络密码”对话框，提示用户输入 `UASHOST_W` 服务器的用户名和密码。

### 活动 3-8：从 Windows 访问 NetWare 文件系统

所需时间：10 分钟

**目标：** 从 Windows XP 客户端计算机映射网络驱动器。

**要求：** 一台 Windows XP 计算机，以及除活动 3-1 获取的 NetWare 信息外，还需要 Windows XP 本地用户名和密码。

**描述：** Eric 希望你通过映射驱动器到 `CORP` 卷，然后将文件复制到 `Apps` 目录来测试网络文件系统。

- 1. 如有必要，启动你的 Windows XP 计算机，并使用分配给你的本地用户名和密码登录到本地计算机。
- 2. 按照以下步骤将网络驱动器映射到你分配的卷：
  - a. 打开 Windows 资源管理器。
  - b. 右键单击 `我的电脑`，然后单击 `映射网络驱动器` 以打开映射网络驱动器对话框。
  - c. 记录默认的驱动器字母：
- d. 单击文件夹文本框旁边的 `浏览` 按钮，以打开浏览文件夹对话框。
- e. 如有必要，单击以展开 `整个网络` 和 `Microsoft Windows 网络`。
- f. 单击以展开名为 `WORKGROUP` 的工作组。
- g. 右键单击你分配的服务器名称，然后单击 `资源管理器` 以打开 `连接到 ASH:HOST-W` 对话框。
- h. 输入你分配的用户名和密码，然后单击 `确定` 登录到服务器。
- i. 右键单击你分配的服务器，然后单击 `扩展` 以显示可用卷。
- j. 单击你分配的卷名称，然后单击 `确定` 将网络路径放入文件夹文本框中。记录文件夹文本框中的内容：________________________
- k. 单击以清除 `在登录时重连` 复选框。
- l. 单击 `完成` 以映射网络驱动器。
- 3. 将 `Mspaint.exe` 文件从 `Windows\System32` 目录复制到你的 `Apps` 目录。
- 4. 在你的 `Forms` 目录中创建以下文本文件（在创建每个文件后刷新屏幕）：`Expense.doc`、`Absentee.txt`、`Junk.txt` 和 `Salvage.txt`。
- 5. 删除 `Salvage.txt` 文件。
- 6. 关闭所有窗口，并为下一个活动保持登录状态。

### 使用 AppleTalk 文件协议（AFP）客户端

安装了 `NFAF` 并配置了密码后，你的 `NetWare 6.5 Open Enterprise` 服务器已准备好允许 Macintosh 用户访问 NetWare 文件系统。他们可以使用熟悉的 `选择器（Chooser）` 应用程序或 `前往（Go）` 菜单来查看网络文件，甚至创建别名。使用 `NFAF`，Macintosh 用户可以从 NetWare 文件系统中打开、复制、移动、保存和删除文件，就像操作任何本地 Macintosh 驱动器一样。`AFP` 服务会自动启动，但你可以通过 NetWare 服务器控制台使用 `AFPSTOP` 和 `AFPSTART` 命令在必要时停止和启动该服务。与 Windows 一起使用的同一 `Cxf.cfg` 搜索文件也用于在 `eDirectory` 中查找 Macintosh 用户名。你还可以重命名 NetWare 卷，以便它们以不同的名称出现在 Macintosh 用户那里。要重命名 NetWare 卷，可以按照以下步骤操作：

![](img/840007e8f98ea6653e5877e945c27dc6_131_0.png)

- 1. 在 NetWare 服务器的 `SYS:etc` 目录中创建一个名为 `Afvpol.cfg` 的文件，其中包含你想使用的卷和特殊的 Macintosh 名称。
