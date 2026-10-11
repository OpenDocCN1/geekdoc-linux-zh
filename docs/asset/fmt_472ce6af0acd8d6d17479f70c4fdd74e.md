
*图 14-11 卷属性窗口*

e. 单击以选中 **目录配额、救援** 和 **用户空间配额** 选项，并记录挂载点信息：
- ______________________________

f. 单击 **完成** 以创建卷并返回到卷窗口。

g. 单击 **挂载** 按钮以挂载 `AEROVOL` 卷。

7. 退出 `iManager`，并保持系统运行以进行下一个活动。

### 活动 14-7：处理 NSS 卷

- **所需时间：** 15 分钟
- **目标：** 将驱动器映射到 Linux NSS 卷并进行受托人分配。
- **要求：** 完成活动 14-6 并在你的 Linux 服务器上拥有第二块硬盘
- **描述：** 为了进一步测试 Linux 上的 NSS 文件系统，Eric 要求你将驱动器映射到新的 `AEROVOL` 卷，并创建一个所有 AeroDyn Users OU 用户都可以访问的 ISS 目录。在此活动中，你将创建 ISS 目录，授予 AeroDyn Users OU 权限，并创建一个登录脚本。

1. 在你的 Windows XP 计算机上，使用你的管理员用户名和密码登录 `eDirectory`。

2. 打开命令提示符窗口。键入以下命令，每输入一条后按 **Enter** 键，将驱动器映射到你的 `AEROVOL` 卷并创建一个 ISS 目录：
```
F:
MAP G:=AEROVOL:
G:
md ISS
```

3. 键入 `exit` 并按 **Enter** 键关闭命令提示符窗口。

4. 在我的电脑中，双击 **G:** 驱动器。右键单击 **ISS** 目录，并单击 **受托人权限**。

5. 单击 **用户** OU，然后单击 **添加** 以添加用户 OU，并授予 **读取** 和 **文件扫描** 权限。

6. 单击以选择除“Supervisor”和“Access Control”之外的所有权限。

7. 单击 **确定** 以保存更改。

8. 启动 `iManager`，并按照以下步骤为 Users OU 创建映射到 ISS 目录的登录脚本：
- a. 单击以展开 **eDirectory Administration** 标题，然后单击 **Modify Object** 链接。
- b. 单击 **Object Selector** 按钮，然后单击 **Users** OU。
- c. 单击 **确定** 以显示“修改对象”窗口。
- d. 单击 **Login Script** 选项卡，并输入 `MAP ROOT G:=AEROVOL\ISS` 命令。
- e. 单击 **确定** 保存更改，然后退出 `iManager`。

9. 注销，然后使用您在 Users OU 中创建的用户账户重新登录 `eDirectory`。

10. 打开“我的电脑”并记录您的驱动器映射：__________________

11. 关闭所有打开的窗口，然后注销。

### 使用 Samba 服务

**Samba** 是一种开源软件，使 Microsoft 客户端能够使用 `CIFS` 访问 Linux 服务器上的数据。图 14-12 展示了在 SUSE Linux 服务器上如何使用 Samba。请注意，Windows 用户账户必须存在于 `eDirectory` 中并启用了 Linux 权限。当用户尝试使用 `CIFS` 访问 Linux 服务器时，`Samba` 服务将处理请求并使用 `eDirectory` 验证用户的姓名和密码。然后，用户可以访问 Linux 文件和目录。

在使用 Samba 之前，您需要在 `iManager` 中启用通用密码作为 SUSE Linux 服务器上的密码管理选项，并为用户账户创建主目录。此外，需要访问 Linux 文件的 `eDirectory` 账户必须启用 Samba 访问权限。在以下活动中，您将学习如何使用 `iManager` 来启用通用密码并为用户账户启用 Samba 访问权限。

![](img/840007e8f98ea6653e5877e945c27dc6_589_0.png)

#### 活动 14-8：启用通用密码和 Samba 访问

**所需时间：** 10 分钟

**目标：** 使用 `iManager` 启用通用密码。

**要求：** 一台 Windows XP 计算机

**描述：** AeroDyn 部门的几名员工将使用未安装 Novell 客户端的 Windows XP 访问 SUSE Linux 服务器上的数据。Eric 希望您使用 Samba 测试此操作是否可行。在此活动中，您通过启用通用密码和为用户账户启用 Samba 访问权限为此任务做准备。

1. 登录到您的 Windows XP 计算机。

2. 启动 Web 浏览器，启动 `iManager`，并使用您的管理用户名和密码登录 `iManager`。

3. 展开 **Passwords** 标题，并单击 **Password Policies** 链接以显示现有的密码策略（参见图 14-13）。

![](img/840007e8f98ea6653e5877e945c27dc6_590_0.png)

**图 14-13** 密码策略窗口

4. 单击 **Edit** 按钮以显示图 14-14 中所示的策略摘要选项卡。验证所有通用密码设置是否已设为 true，除了“设置通用密码时移除 NDS 密码”选项，该选项应设为 false。

![](img/840007e8f98ea6653e5877e945c27dc6_590_1.png)

**图 14-14** 查看当前密码策略的摘要

5. 单击 **Policy Assignment** 选项卡。

6. 如有必要，单击 Assign to 文本框旁边的 **Object Selector** 按钮。单击您的 **UAS** 容器，然后单击 **确定** 将此对象添加到策略分配中。

7. 单击 **确定** 保存分配并返回到密码策略窗口。

8. 现在，既然您已进行所有密码策略更改，请单击 **取消** 返回到 `iManager` 主窗口。

9. 按照以下步骤为用户账户启用 Samba 访问权限：
- a. 在 Samba Management 标题下，单击 **Enable Linux User for Samba** 链接。
- b. 单击 **Object Selector** 按钮，导航至并单击您之前创建的 **LUMUser** 账户。
- c. 单击 **确定** 以启用 `LUMUser` 账户的 Samba 访问权限，并返回到 `iManager` 主窗口。

10. 退出 `iManager`，并保持在本地计算机上登录状态。

11. 从您的 Windows 计算机注销。

#### 为启用 Linux 权限的用户创建主目录

由于 Samba 使用 Linux 目录结构而不是 NCP 卷，从 Windows 客户端访问 Linux 服务器的用户必须启用 Linux 权限，并且应由 Linux 创建其主目录。在第 13 章中，您使用 `adduser` 命令和 `-m` 参数创建了一个新的用户账户以及 `/home` 结构中该用户的主目录。为 `eDirectory` 用户账户创建 Linux 主目录需要不同的技术。要为启用 Linux 权限的用户创建主目录，您可以使用以下步骤：

![](img/840007e8f98ea6653e5877e945c27dc6_591_0.png)

1. 使用 `iManager` 在 `eDirectory` 中创建一个新的用户账户，但此时不要创建主目录。使用 `iManager` 创建的主目录是通过 Novell 核心协议访问的，无法直接从使用 Linux ReiserFS 文件系统的 Samba 访问。

2. 使用 `iManager` 为该用户账户启用 Linux 权限。

3. 从服务器控制台使用 Linux `su` 命令切换到新的用户账户。首次使用此命令切换到启用 Linux 权限的用户账户时，Linux 系统会在 `/home` 结构中为该用户创建主目录。

在以下活动中，您将学习如何在 SUSE Linux 服务器上为您的启用 Linux 权限的用户创建主目录，然后使用 Windows 客户端测试对这些目录的访问。

![](img/840007e8f98ea6653e5877e945c27dc6_591_1.png)

#### 活动 14-9：创建 Linux 主目录

**所需时间：** 10 分钟

**目标：** 为启用 Linux 权限的用户账户创建主目录。

**要求：** 访问 SUSE Linux 服务器控制台

**描述：** 在此活动中，您将在 SUSE Linux 服务器上为您的启用 Linux 权限的用户创建主目录。

1. 使用 `root` 用户名和密码登录到您的 SUSE Linux 服务器。

2. 打开一个终端会话。
