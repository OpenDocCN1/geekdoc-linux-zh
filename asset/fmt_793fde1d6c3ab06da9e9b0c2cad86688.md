
创建完所有 Storage Location 对象后，接下来您需要创建 *Storage Location Lists*（存储位置列表），用于将 Storage Location 对象与 eDirectory 用户、组或容器对象关联。通过此类列表关联的用户在登录 NetStorage 时，将看到列表中显示的存储位置。

要创建 Storage Location List，请完成以下步骤：

- 在 iManager 中，选择 **File Access (NetStorage)**（文件访问（NetStorage））下的 **Storage Location: Create/Modify List**（存储位置：创建/修改列表）任务。将显示图 8.47 中所示的屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_401_0.png)

![](img/c7771e8540507f2b00c088c7a411b57b_401_1.png)

- 在 **Object**（对象）字段中，浏览并选择您想要与 Storage Location 对象关联的用户、组或容器对象。

  - 如果您选择用户对象，仅该用户将有权访问存储位置。如果您选择组对象，该组的所有成员将有权访问。如果您选择容器，位于该容器内的所有用户将有权访问。

- 点击 **OK**（确定）。将显示图 8.48 中的屏幕。

- 在 **Storage Location Objects**（存储位置对象）字段中，浏览并选择您想要与列表关联的 Storage Location 对象。您可以选择多个对象。

![](img/c7771e8540507f2b00c088c7a411b57b_402_0.png)

**图 8.48**

将存储位置与存储位置列表关联。

- 5. 单击“确定”。

- 6. 当提示列表已创建时，单击“确定”。

此时，Samba 共享可供已与存储位置列表关联且已启用 LUM/Samba 的 NetStorage 用户访问。

> 在 CLE 考试中，考生犯的一个常见错误是忘记为与存储位置列表关联的用户启用 LUM/Samba。

要通过 NetStorage 访问该共享，请完成以下步骤：

- 1. 打开 Web 浏览器并导航至 `https://your_server_IP_address/NetStorage`。此时将出现图 8.49 中所示的屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_402_1.png)

**图 8.49**

向 NetStorage 进行身份验证。

- 2. 作为之前创建的存储位置列表所关联的用户进行身份验证。您必须使用该用户的可区分名称（Distinguished Name），例如 `CGrayson.IFCLE`。

- 3. 单击**确定**。

- 4. NetStorage 界面将显示出来。

在图 8.50 中，创建了一个名为 **Test** 的存储位置对象。该存储位置对象指向我们在实验练习 8.2 中创建的 `[tmp]` 共享。

创建了一个存储位置列表，并将其与 Test 存储位置对象以及 eDirectory 树中的 IFCLE 容器关联起来。由于 `CGrayson` 存在于 IFCLE 容器中，因此他有权访问 Test 存储位置。

**图 8.50**

NetStorage 中的 Samba 共享。

![](img/c7771e8540507f2b00c088c7a411b57b_403_0.png)

进入 NetStorage 后，您可以使用“文件”菜单创建新文件夹、删除文件或文件夹、重命名文件或文件夹、将文件上传到 NetStorage 服务器、下载文件、通过电子邮件发送文件、清除已删除的文件、撤销删除文件、归档文件以及设置文件属性。如图 8.51 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_404_0.png)

**图 8.51**

在 NetStorage 中管理文件。

使用“编辑”菜单，您可以移动和复制文件。如图 8.52 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_404_1.png)

**图 8.52**

在 NetStorage 中使用“编辑”菜单。

使用“查看”菜单，您可以刷新 NetStorage 显示内容并显示已删除的文件。如图 8.53 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_405_0.png)

**图 8.53**

在 NetStorage 中使用“查看”菜单。

现在让我们讨论一下如何配置 NetStorage 服务器本身。

### 配置 NetStorage 服务器

默认情况下，出厂的 NetStorage 服务器配置在大多数部署中运行完美。您可能不需要实际更改任何设置。然而，如果需要更改，NetStorage 服务器设置是通过 iManager 配置的。要配置 NetStorage 参数，请执行以下操作：

- 1. 打开 Web 浏览器并导航至 `https://your_server_IP_address/nps/iManager.html`。

- 2. 作为 `admin` 用户进行身份验证。

- 3. 向下滚动至 **File Access (NetStorage)** 角色。

- 4. 从以下配置任务中选择：

    - **Authentication Domains**——此任务允许您添加 NetStorage 用于对用户进行身份验证的 eDirectory 服务器。通过单击 **Add Domain**，您可以添加多个 eDirectory 服务器。此任务还允许您配置由 NetStorage 服务的 eDirectory 上下文。如图 8.54 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_405_1.png)

**图 8.54**

配置身份验证域。

    - **Current Sessions**——此任务显示当前正在使用 NetStorage 的用户列表。示例报告如图 8.55 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_406_0.png)

**图 8.55**

查看当前会话。

    - **General**——此任务允许您配置 NetStorage 代理用户、位置、安全证书、超时值和 LDAP 端口。此屏幕如图 8.56 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_406_1.png)

**图 8.56**

配置 NetStorage 常规设置。

    - **iFolder Storage Provider**——此任务允许您使用 iFolder 服务器的 IP 地址配置 NetStorage，如图 8.57 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_407_0.png)

**图 8.57**

配置 NetStorage iFolder 提供程序设置。

    - **Resource Usage**——此任务显示 NetStorage 服务器资源利用率的详细报告，如图 8.58 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_407_1.png)

**图 8.58**

NetStorage 资源使用。

    - **Statistics**——此任务显示 NetStorage 服务器各项统计数据的详细报告，如图 8.59 所示。

- 5. 如果进行了任何更改，保存后需要重新启动 NNLS Apache Web 服务器。方法是打开终端会话，输入 `/etc/init.d/novell-httpd` `stop`，然后输入 `/etc/init.d/novell-httpd` `start`。

![](img/c7771e8540507f2b00c088c7a411b57b_408_0.png)

**图 8.59**

NetStorage 统计数据。

至此，让我们花些时间动手操作 NetStorage。

### 实验练习 8.3：使用 NetStorage

在本实验中，您将使用浏览器通过 NetStorage 访问 Samba 共享。

> **警告** 本实验假设您已完成第 6 章中的实验以及本章中前面的实验。如果没有完成，请务必先回去完成这些实验。

请完成以下步骤：

- 1. 通过执行以下操作测试 NetStorage 中的默认共享文件夹：

    - a. 打开 Web 浏览器并导航至 `https://your_server_IP_address/NetStorage`。

    - b. 在 **User Name** 字段中，输入 `JJackson.IFCLE`。

    - c. 在 **Password** 字段中，输入 `novell`。

    - d. 单击 **确定**。NetStorage 屏幕将显示出来。
