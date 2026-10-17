
![](img/c7771e8540507f2b00c088c7a411b57b_503_3.png)

- 3. 默认情况下，`eGuide Link（eGuide 链接）` 行上的 `Enable（启用）` 复选框应已勾选。如果未勾选，请选择 `Enable` 以开启 eGuide 集成。
- 4. 如果您希望在用户的虚拟办公室主页上显示 eGuide 快速搜索框，请在 `Home Page eGuide Quick Search（主页 eGuide 快速搜索）` 行上勾选 `Enable`。
- 5. 默认情况下，应已勾选 `Launch to this Server's eGuide Home Page（启动到此服务器的 eGuide 主页）` 选项。这将配置虚拟办公室连接到安装了虚拟办公室的同一服务器上的 eGuide 服务。如果您希望连接到不同服务器上的 eGuide 服务，请勾选 `Launch to a Remote Server's eGuide Home Page（启动到远程服务器的 eGuide 主页）` 按钮，并输入 eGuide 服务器的 IP 地址或 DNS 名称。
- 6. 点击 `OK（确定）`。

接下来，让我们看看如何配置虚拟办公室的书签服务。

### 配置虚拟办公室书签

虚拟办公室允许用户保存重要书签。这些书签可以在两个位置访问。首先，虚拟办公室在用户主页顶部提供一个图标，用户可以通过该图标维护书签列表。该图标如图 11.19 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_504_0.png)

您还可以配置虚拟办公室在用户主页的一个字段中显示用户的书签。此效果如图 11.20 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_504_1.png)

要在您的虚拟办公室部署中配置书签服务，您需要执行以下操作：

- 1. 在 iManager 中，选择 `Services Administration（服务管理）` 任务。
- 2. 选择 `Bookmarks（书签）` 选项卡。此时将显示图 11.21 中的屏幕。

**图 11.21**

配置虚拟办公室书签服务。

![](img/c7771e8540507f2b00c088c7a411b57b_505_0.png)

- 3. 默认情况下，`Bookmarks Link（书签链接）` 行上的 `Enable（启用）` 复选框应已勾选。如果未勾选，请选择 `Enable` 以在虚拟办公室界面中显示 `Bookmarks` 图标。
- 4. 如果您希望在用户的虚拟办公室主页上显示 `Bookmarks` 字段，请在 `Home Page Bookmarks（主页书签）` 行上勾选 `Enable`。
- 5. 默认情况下，已定义了一个指向 Novell 网站的书签。`Current Bookmarks（当前书签）` 字段中定义的所有书签都将显示在所有虚拟办公室用户的书签列表中。您可以通过完成以下步骤来配置将显示给所有虚拟办公室用户的其他书签：

![](img/c7771e8540507f2b00c088c7a411b57b_504_2.png)

![](img/c7771e8540507f2b00c088c7a411b57b_504_3.png)

   a. 在 `Current Bookmarks` 下，点击 `Add（添加）`。此时将显示图 11.22 中的屏幕。

**图 11.22**

添加书签。

![](img/c7771e8540507f2b00c088c7a411b57b_505_1.png)

   b. 在 `Name（名称）` 字段中，输入书签的名称。
   c. 在 `URL` 字段中，输入您想要收藏的网页的 URL。
   d. 点击 `OK（确定）`。新书签将出现在 `Current Bookmarks` 字段中。
- 6. 点击 `OK（确定）`。

配置好书签服务后，您需要做的下一件事是将虚拟办公室与 NNLS 服务器上的 NetMail 服务进行集成。

### 将 NetMail 与虚拟办公室集成

与 eGuide、NetStorage 和 iPrint 一样，您也可以将 NNLS 服务器上的 NetMail 邮件服务与虚拟办公室集成。在虚拟办公室主页顶部，您可以配置显示一个 NetMail 图标。该图标如图 11.23 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_506_0.png)

当最终用户点击此图标时，虚拟办公室会启动一个新窗口，并使用 NetMail 的模块化 Web 代理显示用户的收件箱，如图 11.24 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_506_1.png)

此外，虚拟办公室可以配置为在用户的主页上显示其最近的电子邮件消息。这被称为简化的电子邮件视图（Reduced eMail View）。简化的电子邮件视图如图 11.25 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_506_2.png)

要在虚拟办公室中集成 NetMail，您需要完成以下步骤：

- 1. 在 iManager 中，选择 `Services Administration（服务管理）` 任务。
- 2. 选择 `eMail` 选项卡。此时将显示图 11.26 中的屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_507_0.png)

**提示**

虚拟办公室还可以与 GroupWise、Lotus Notes 或 Microsoft Exchange 邮件服务器集成。它也可以与任何支持 IMAP 或 POP3 协议的其他邮件服务器集成。执行此操作的步骤与集成 NetMail 所需的步骤几乎相同。

- 3. 默认情况下，`eMail Link（eMail 链接）` 行上的 `Enable（启用）` 复选框已勾选。如果未勾选，请点击 `Enable` 以在虚拟办公室界面中显示 `eMail` 图标。
- 4. 在 `Email Server（邮件服务器）` 下拉列表中，选择 `NetMail`。
- 5. 点击 Edit。此时将显示图 11.27 中的屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_507_1.png)

- 6. 在 NetMail URL 字段中，默认显示 URL `https://%*serverdnsport%:52443`。文本 `%*serverdnsport%` 是一个变量，将被替换为正在运行虚拟办公室的同一服务器的地址。如果您的 NetMail 服务运行在另一台服务器上，请在此字段的 URL 中输入其 IP 地址或 DNS 名称，包括您的 NetMail 服务器使用的端口号。
- 7. 如果 NetMail 服务配置为使用与您的虚拟办公室服务器相同的 eDirectory 树（通常如此），请勾选 `Synchronized with the Virtual Office Tree（与虚拟办公室树同步）`。当用户在虚拟办公室中选择 eMail 链接时，系统将使用提供给虚拟办公室进行身份验证的用户名和密码，自动为用户进行 NetMail 身份验证。
- 8. 如果 NetMail 服务配置为使用与您的虚拟办公室服务器不同的 eDirectory 树，请勾选 `Different than the Virtual Office Tree（不同于虚拟办公室树）`。这将要求用户在虚拟办公室主页中选择 eMail 链接时，提供用户名和密码以进行 NetMail 身份验证。
- 9. 点击 OK。
- 10. 如果您希望在用户的虚拟办公室主页上显示简化的电子邮件字段，请完成以下操作：

**注意**

简化的电子邮件视图小部件不像之前配置的 eMail 链接那样使用 NetMail 的模块化 Web 代理。相反，它使用 POP3 或 IMAP 协议访问您的 NetMail 服务器。为此，您需要确保已为 NetMail 服务器配置了 POP 或 IMAP 代理。

   a. 在 `Home Page Reduced eMail View（主页简化 eMail 视图）` 行上勾选 `Enable`。
   b. 点击 `Edit（编辑）`。此时将显示图 11.28 中的屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_508_0.png)

   c. 在 `Mail Server Type（邮件服务器类型）` 下，选择用于访问您的 NetMail 服务器的协议。您的选择取决于您已部署的 NetMail 代理。
