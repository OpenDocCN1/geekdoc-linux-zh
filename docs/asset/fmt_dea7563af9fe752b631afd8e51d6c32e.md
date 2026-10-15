
现在你已经了解 SFU 3.5 对我们的 Active Directory 架构将做什么，我们准备好开始。在你的 Windows 2003 DC 上安装 SFU 3.5（带有所需的选项）：

1. 启动 SFU 3.5 安装程序（`SfuSetup.msi`）。

2. 在“欢迎”界面点击“下一步”。

3. 在“客户信息”界面输入你的姓名和组织名称。

4. 在“许可证和支持信息”界面接受协议并点击“下一步”。

5. 在“安装选项”界面，选择“自定义安装”并点击“下一步”。

6. 在“选择组件”界面，进入 `Windows Services for Unix` ➤ `NFS` ➤ `Gateway for NFS`。更改默认值使该组件被额外加载，如图 3.9 所示。此外，“NFS 客户端”必须禁用，如图 3.9 所示。再次，我们需要加载 SFU 3.5 的 NIS 服务器组件用于本书。它们需要被加载以扩展架构。

7. 在“安全设置”界面，你有两个选项：“启用 Interix 程序的行为”和“将默认行为改为区分大小写”。对于我们的示例，我们不需要勾选任何一个设置。（通过这些选项，你决定了 Windows 如何处理大小写）。

8. 下一步，你将看到“用户名映射”（User Name Mapping）屏幕。我们将在下一章中使用此功能，请选择“网络信息服务 (NIS)”按钮并点击“下一步”。

9. 你将看到“用户名映射”的第 2 页屏幕。从下拉列表中选择你的 Windows 域名称（如果是“AD”的话）。留空“NIS 域名称”字段。同时也请留空“NIS 服务器名称”字段。点击“下一步”继续。

10. 在“NIS/密码同步”屏幕上，你会收到一个警告，指出架构更改是不可逆转的。为了本书的需要，你需要这些更改，因此点击“下一步”继续。

11. 在“安装位置”屏幕上，选择你想要安装 SFU 3.5 的位置。默认值是可以的（“`C:\SFU`”），因此点击“下一步”。

此时，SFU 3.5 将完成安装。完成后，你可能会被要求重启。重启后即可继续。

## 如何为你的 Active Directory 用户和组启用 Unix 权限

现在 SFU 3.5 已完全安装，你就可以为你的 Active Directory 用户和组启用 Unix 权限了。这很简单。开始之前，启动“Active Directory 用户和计算机”（Active Directory Users and Computers）。然后，要启用一个用户账户，你必须先有一个启用了 Unix 的组账户。

### 为 Active Directory 组启用 Unix

使用“Active Directory 用户和计算机”，双击我们在本节之前创建的 `SalesGroup`。你会看到一个名为“Unix Attributes”（Unix 属性）的新标签页，如图 3.10 所示。

图 3.9 避免安装“NFS ”和“密码同步”功能，但请安装“NFS 网关”。

![](img/1bd448c8019d74f469e5d7e3f033d752_188_0.png)

168 第 3 章 · 验证 Linux 客户端的 Active Directory 身份

图 3.10 为 Active Directory 组启用 Unix。

![](img/1bd448c8019d74f469e5d7e3f033d752_189_0.png)

要为该组启用 Unix，只需点击 NIS 域框中的下拉菜单并选择你的 Active Directory。当你这样做时，Active Directory 将自动为该 Active Directory 组分配一个 `GID`（组 ID），该组现在也是一个 Unix 组了。

### 为 Active Directory 用户启用 Unix

在本节较早些时候，我们在 `Sales OU` 中创建了 `salesperson1` 和 `salesperson2`。双击 `salesperson1` 账户并选择“Unix Attributes”标签页，如图 3.11 所示。

要为该用户启用 Unix，只需点击 NIS 域框中的下拉菜单并选择你的 Active Directory。当你这样做时，Active Directory 将自动为该 Active Directory 组分配一个 `UID`（用户 ID），该用户现在也是一个 Unix 用户了。

在此处停留时，你可以在“主组名/GID”字段中选择“`SalesGroup`”。此字段仅由具有 Unix 属性的 Active Directory 组填充，就像我们刚刚为 `SalesGroup` 设置的那样。

## 使用扩展的 Active Directory 进行 Linux 身份验证

在紧接的上一节中，我们通过安装 Microsoft Unix Services (SFU) 增强了我们的 Active Directory 服务器。或者你可能下载了网络附录并学习了如何使用 Windows 2003/R2 扩展架构。

### 图 3.11

你可以为用户启用 Unix 权限，并指定他们属于哪些启用了 Unix的用户。

![](img/1bd448c8019d74f469e5d7e3f033d752_190_0.png)

Active Directory 现在感知 Unix 用户 ID 和组 ID，并规定为每个用户和组账户存储这些 ID。与其他方法不同，我们可以直接针对 Active Directory 验证 Linux 客户端，而无需担心文件从一个 Linux 客户端移动到另一个时出现文件所有权不一致的问题，因为 Active Directory 是用户和组 ID 的唯一仲裁者。关于此点的完整列表（这是我们之前讨论的基于 Winbind 的方法的极大改进），请参阅标题为“Winbind 如何伪造 Linux 用户 ID（以及它如何损害你）”的侧栏。

但 Linux 客户端如何从 Active Directory 服务器获取 Unix ID (`UIDs`) 和组 ID (`GIDs`) ？由于这些字段不是传统 Windows 网络协议的一部分，Linux 的 `Winbind`（模拟协议）无法获取这些内容。对于我们来说，Active Directory 响应 `LDAP` 查询，由于我们使用 Linux 客户端向 Active Directory 发起 `LDAP` 查询，我们只需要请求那些 `UID` 和 `GID` 即可。

## 为 Active Directory/LDAP 请求和身份验证做好准备

在上一章中，我们在“验证 Linux 客户端到 Open LDAP 服务器的身份”部分验证了 Linux 客户端到 Linux LDAP 服务器的身份。当我们这样做时，`lincli1.corp` 上的 Open LDAP 客户端组件直接与 `inserv1.corp.com` 上的 Open LDAP 服务器组件联系，我们查询了用户账户并直接验证了 OpenLDAP。真棒。

170 第 3 章 · 验证 Linux 客户端的 Active Directory 身份

现在我们的目标是让新机器 `adldaplincli1.ad.corp.com` 上的 OpenLDAP 客户端组件与 `windc1.ad.corp.com` 上的 Active Directory 通信，如图 3.12 所示。

图 3.12 Linux 客户端如何向 Active Directory 验证身份 ![](img/1bd448c8019d74f469e5d7e3f033d752_191_0.png)

- 步骤 1：查找账户

- 步骤 2：向 Active Directory 验证

> 如果我们足够活跃，可以更进一步

### 关于 Kerberos 身份验证

Kerberos 用于验证用户和授权。Kerberos 在基础层面构建于 Active Directory 中，也被操作系统使用。

Kerberos 非常安全，除了简单的登录外还有其他优势。最有趣的之一是 Kerberos 让实施单点登录变得更容易，允许用户无需输入密码即可访问许多服务。

遗憾的是，大多数流行的 Linux 尚未“Kerberos 化”，因此我们从单点登录功能中获益不多。对于本书来说，Kerberos 最重要的特性是以极高安全的方式进行验证，但需要注意会有更多收益。

Kerberos 是一个复杂的机制，已经有很多本关于该协议的书。对于我们的目的，这里有三个基本要点：

- 第一，Kerberos 服务器统称为 `KDC`（密钥发行中心）。`KDC` 术语出现在身份配置对话框中，我们会尝试统一使用该术语。

- 第二，一个 `KDC` 托管一个 Kerberos“域”（realm），它有自己的名称。单个 Kerberos 服务器在理论上可以作为“中转”服务器并拥有许多不同的安全主体（只要它们属于不同的域且没有命名冲突）。在实践中，Active Directory 域的 Kerberos 域名称与 Active Directory 域名称匹配，但必须全大写。这很重要。以小写输入 Kerberos 域名称（如其在 Windows 中通常显示的方式）将无法运行。
