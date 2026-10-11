
术语“`LUM` 已启用”和“Linux 已启用”描述了向 eDirectory 用户和组添加标准 Linux 属性和值的过程，从而使其能够像 POSIX 用户一样运行。然而，并非所有 eDirectory 用户都需要启用 Linux 才能访问 Linux 服务器。对于使用 Novell 客户端的用户，`NCP` 服务器负责处理对 Linux 服务器的访问。由于 `NCP` 服务器与 eDirectory 紧密集成，只要用户访问存储在 `NSS` 卷上的数据，就不需要启用 Linux。但是，需要访问标准 Linux 卷和分区上数据的 Novell 客户端用户确实需要启用 Linux。

三大类 Linux 服务和实用程序需要启用 Linux 的访问权限：

- **核心 Linux 实用程序**——核心实用程序和其他 shell 命令，通过 LDAP 指定为 PAM 启用的访问，如表 14-1 所示。
- **Novell Samba 共享**——需要访问 Linux 目录的 Windows 工作组用户必须拥有启用 Linux 的 eDirectory 用户账户，因为 Samba 服务需要 POSIX 认证才能访问网络数据。
- **Linux 上的 Novell 远程管理器（NRM）**——管理员可以使用 NRM 实用程序监控和管理多个 Linux 服务器，但为此，他们必须作为以下用户类型之一进行身份验证：拥有 Linux 服务器所有权限的 `root` 用户、由 POSIX 访问权限控制的本地用户，或已启用 Linux 的 eDirectory 用户（例如 `Admin`）。

### 表 14-1 由 LUM 控制的 PAM 启用服务

| 命令 | 任务 |
| :--- | :--- |
| `ftp` | 向 SUSE Linux 服务器传输文件或从服务器接收文件 |
| `login` | 直接通过远程会话登录到 SUSE Linux 服务器 |
| `passwd` | 更改 POSIX 密码 |
| `rlogin` | 从远程主机登录到 SUSE Linux 服务器 |
| `sshd` | 从远程主机与 SUSE Linux 服务器建立安全的加密连接 |

### 创建启用 Linux 的用户和组账户

通过将用户设为启用 Linux 的组的成员，用户即可启用 Linux。默认情况下，安装 eDirectory 树中 SUSE Linux 服务器的 `Admin` 用户通过成为 `adminGroup` 的成员而自动启用 Linux。若要启用其他用户，您可以使用 `iManager` 或 `nambulkadd` 命令。虽然该命令在您需要从批处理文件中启用多个用户和组时很有用，但使用 `iManager` 通常更容易，这也是本章中您使用的方法。

当您要启用 Linux 的组时，您需要选择组内用户将要访问的 SUSE Linux 服务器。SUSE Linux 服务器的 eDirectory 对象名称为 `UNIX 工作站 - _服务器名称_`（_通用名称_ 代表 Linux 服务器的 DNS 名称），被称为 `Linux 工作站对象`。您还可以选择 `Linux 配置对象`，该对象存储了 eDirectory 树中所有 SUSE Linux 服务器的列表。这是一种快速方式，可一次性在所有 SUSE Linux 服务器上启用组成员的 Linux 功能。若要启用组的 Linux 功能，您可以使用以下步骤：

![](img/840007e8f98ea6653e5877e945c27dc6_578_0.png)

1. 登录到本地计算机或您的 SUSE Linux 服务器并启动您的 Web 浏览器。
2. 启动 `iManager` 并使用您的 eDirectory 管理用户名和密码登录。
3. 点击以展开 Linux 用户管理标题，然后点击启用组用于 LUM 链接。
4. 点击“选择要用于 LUM 的组”文本框旁边的对象选择器按钮，点击您要启用 Linux 的组，然后点击 **确定** 以显示“启用组用于 LUM”窗口（类似于图 14-2 中的窗口）。

![](img/840007e8f98ea6653e5877e945c27dc6_578_1.png)

*图 14-2 配置启用 Linux 的组*

5. 若要启用组成员访问所有 Linux 服务器，请点击“选择 **Linux 配置** 对象”文本框旁边的 **对象选择器** 按钮，并点击 **UNIX 配置** 对象。若要为选定的 SUSE Linux 服务器启用组成员的 Linux 功能，请点击“选择一个或多个 Linux 工作站对象”选项按钮，点击 **对象选择器** 按钮，并仅选择希望组成员访问的 Linux 工作站对象。
6. 点击 **确定** 以启用该组并显示成功消息。再次点击 **确定** 返回 `iManager` 主窗口。

在随后的实验中，您将在 SUSE Linux 服务器上创建一个启用 Linux 的组，创建用户，然后让其中一个用户成为该启用 Linux 组的成员。

### 实验 14-2：创建启用 Linux 的组和用户

- **所需时间：** 10 分钟
- **目标：** 使用 `iManager` 创建启用 Linux 的用户和组。
- **要求：** 使用管理账户访问 SUSE Linux 服务器，以及一台 Windows XP 或 SUSE Linux 10 计算机；您也可以从 OES Linux Enterprise Server 9 控制台执行此实验。如果使用 Linux，请使用已启用 Java 的 Firefox 或 Mozilla Web 浏览器。
- **描述：** 为了测试 SUSE Linux 服务器，Eric 希望您为 AeroDyn 部门创建一个包含具有两个测试用户的 Users OU（组织单元）的 eDirectory 结构。在此实验中，您将使用 `iManager` 在 AeroDyn 部门中创建 Users OU，然后创建一个启用 Linux 的组和用户，以便 Eric 测试服务器。

1. 如有必要，启动您的 Linux 服务器并使用 `root` 用户名和密码登录。如果您在 Windows XP 环境中工作，请使用本地用户名和密码登录到您的 Windows XP 计算机。
2. 启动您的 Web 浏览器，并通过输入 URL `https://IPaddress/nps/iManager.html`（将 `IPaddress` 替换为您的 SUSE Linux 服务器的 IP 地址）来启动 `iManager`。
3. 使用您的管理用户名和密码登录 `iManager`。
4. 按照以下步骤创建 Users OU：
   - a. 点击以展开 eDirectory 管理标题，然后点击 **创建对象** 链接。
   - b. 向下滚动并点击 **组织单元** 对象类，然后点击 **确定** 以显示创建组织单元窗口。
   - c. 在组织单元名称文本框中输入 `Users`。
   - d. 点击上下文文本框旁边的 **对象选择器** 按钮，并点击您的 `UAS` 容器。
   - e. 点击 **确定** 以创建 Users OU 并显示完成消息。
   - f. 点击 **确定** 返回 `iManager` 主窗口。
5. 按照以下步骤创建一个组并使其启用 Linux：
   - a. 点击 **创建对象** 链接以显示创建对象窗口。
   - b. 点击 **组** 对象类，然后点击 **确定** 以显示创建组窗口。
   - c. 在组名称文本框中输入 `LinuxUsers`，点击上下文文本框旁边的 **对象选择器** 按钮，并点击 `Users OU`。
   - d. 单击 **OK** 以创建 `LinuxUsers` 组并显示完成信息。
   - e. 单击 **OK** 以显示“将组启用为 LUM”窗口。
   - f. 单击“选择 Linux 配置对象”文本框旁边的 **Object Selector** 按钮，然后单击 `UNIX Config` 对象。
   - g. 单击 **OK** 以显示完成信息，然后再次单击 **OK** 以返回 `iManager` 主窗口。
6. 按照以下步骤创建名为 `LUMUser` 的用户账户：
   - a. 向下滚动，如有必要，点击以展开 **Users** 标题，然后单击 **Create User** 链接。
   - b. 在 Username 文本框中输入 `LUMUser`，在 Last name 文本框中输入 `LinuxUser`。
   - c. 单击 Context 文本框旁边的 **Object Selector** 按钮，单击 `Users OU`，然后单击 **OK**。
   - d. 在 Password 和 Retype Password 文本框中输入密码。
   - e. 单击 **OK** 以创建 `LUMUser` 账户，然后再次单击 **OK** 以返回 `iManager` 主窗口。
7. 按照以下步骤为 Linux 启用 `LUMUser` 账户：
