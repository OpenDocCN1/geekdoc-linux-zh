
在用户能够使用其 eDirectory 用户名和密码登录之前，您必须使用 Linux User Management 组件配置 SUSE Linux Enterprise Desktop 工作站。

您可以在 SUSE Linux Enterprise Desktop 安装期间设置 eDirectory 身份验证，也可以在安装后随时使用 YaST 设置它。

要在 SUSE Linux Enterprise Desktop 安装期间安装和配置 LUM，请执行以下操作：

- 1. 从图 13-16 所示的用户身份验证方法页面中，选择 eDirectory LDAP。

![](img/9129877170834ca9d5fdac5319bf5f12_508_0.png)

**图 13-16**

2. **（条件）** 如果尚未安装，将提示您安装 `yast2-linux-user-mgmt` 软件包。

要在已运行的工作站上安装和配置 LUM，请执行以下步骤：

- 1. 从工作站启动 YaST 控制中心：

  a. **GNOME：** 选择 **计算机 > 更多应用程序 > 系统 > YaST**。

  b. **KDE：** 选择 **K 菜单** 按钮，然后选择 **系统 > YaST（管理员设置）**。

- 2. 选择 **安全和用户 > Linux User Management**。

  如果缺少此模块，请使用 YaST 软件管理模块安装 `yast2-linux-user-mgmt` 软件包。然后关闭 YaST 并重新启动它。

- 3. 指定 eDirectory 是否在计算机本身上运行（**本地系统**）或在网络上的另一台计算机上运行（**远程系统**）。

- 4. 如果 eDirectory 在远程系统上运行，请指定远程系统的 *IP地址*。

- 5. （可选）指定 eDirectory *管理员名称*、*上下文* 和 *密码*，然后选择 **下一步**。

  管理员名称和上下文必须以 LDAP 语法输入，该语法使用逗号而不是句点（例如，`cn=admin,o=novell`）。

![](img/9129877170834ca9d5fdac5319bf5f12_509_0.png)

如果您没有在 eDirectory 树中创建对象的权限，请将这些字段留空。您需要联系您的 eDirectory 管理员，提供客户端的主机名，并请他/她为您创建一个具有您主机名的 LUM Workstation 对象。

您还应询问管理员您可以在哪里获取 LDAP 服务器的 CA 证书副本。您需要将此证书放在 `/var/lib/novell-lum/` 目录中。

CA 证书的名称与 `/etc/nam.conf` 文件中首选服务器条目的名称匹配，并具有 `.der` 扩展名。您可以输入 `nameconfig.get preferred-server` 来获取名称。

- 6. 指定 Linux/UNIX Config 对象的 *位置*。

Linux/UNIX Config 对象存储网络上 Linux/UNIX Workstation 对象所在位置（上下文）的列表。它还控制在创建用户和组对象时分配 UID 和 GID 的数字范围。

此对象在 eDirectory 服务器上配置 LUM 时创建，通常位于 eDirectory 树的上层容器中（例如，`o=novell`）。请联系您的 eDirectory 管理员获取上下文。

![](img/9129877170834ca9d5fdac5319bf5f12_509_1.png)

有关更多信息，请参阅 *Novell Linux User Management Technology Guide* 中的“Understanding eDirectory Objects and Linux”，网址为 http://www.novell.com/documentation/oes/lumdg/data/bx3sbv9.html。它也包含在 3086 课程 DVD 2 中，目录为 OESDocs。

- 7. （可选）指定 LUM Workstation 对象的 *位置*。

  LUM Workstation 对象代表用户登录的实际计算机。

  如果您有权在 eDirectory 树中创建对象，则此对象将在工作站配置过程中自动创建，通常放置在 eDirectory 树的组织（O）或组织单位（OU）容器中。

  您也可以通过在 Novell iManager 中选择 **Linux User Management > Create Linux Workstation Object** 来创建 LUM Workstation 对象。

- 8. （可选）如果您已禁用对 LDAP 服务器的匿名绑定，请指定具有 LDAP 树权限的用户 *代理用户名、上下文* 和 *密码*。

- 9. 选择下一步。

- 10. 选择应使用 eDirectory 进行身份验证的 *登录访问方法*。

- 11. 选择完成。

安装和配置 LUM 技术可将 SUSE Linux Enterprise Desktop 工作站设置为根据存储在 eDirectory 中的用户帐户信息验证登录请求。在用户可以登录之前，他们必须使用 Novell iManager 创建 eDirectory 用户帐户并为 LUM 扩展，并且他们的 User 对象必须与他们将登录的工作站关联。

### 使用 Novell iManager 启用用户以进行 eDirectory 身份验证

当 Linux User Management 组件正确安装后，您可以使用 eDirectory 和 Novell iManager 指定哪些用户可以访问网络上的 SUSE Linux Enterprise Desktop 计算机。

Novell iManager 是用于管理 eDirectory 对象的基于浏览器的实用程序。它在 Mozilla Firefox、Netscape Navigator 或 Internet Explorer 等网络浏览器中运行。

当您在 Novell iManager 中创建用户或组帐户时，会提示您“为 Linux 启用”User 对象或 Group 对象。您还可以使用 Novell iManager 为 Linux 启用现有的 User 或 Group 对象。

每次为 eDirectory 身份验证配置 SUSE Linux Enterprise Desktop 工作站时，在 eDirectory 中已启用 LUM 的用户必须与工作站关联后才能从该工作站登录。

要使用 Novell iManager 启用用户以进行 eDirectory 身份验证，请执行以下操作：

- 1. 启动 Novell iManager：

  a. 在网络浏览器的地址字段中输入

  b. 使用 *管理员* 用户的完整上下文和 *密码* 登录。

- 2. 通过单击顶部按钮栏，确保您处于“角色和任务”视图中，然后从左侧窗格中选择 Linux User Management。

- 3. 选择为 Linux 启用用户。

- 4. 选择要启用的 *用户对象*，然后选择下一步。

```
http://target_server/nps/iManager
```

当 eDirectory User 对象被扩展以保存 Linux 用户登录属性时，它被称为已启用 LUM 或已为 Linux 启用。

![](img/9129877170834ca9d5fdac5319bf5f12_510_0.png)

启用 Linux 后，用户只需使用 Telnet、SSH 或其他受支持的方法访问 Linux 计算机并输入其用户名和密码即可。

访问请求将被重定向以查找存储在 eDirectory 中的适当用户名和登录信息。

扩展到 Linux 后，eDirectory 用户对象保存 Linux 相关属性，例如用户 ID、主组 ID、主组名称、主目录位置和首选 shell。

- 5. 将用户分配到一个组；然后选择下一步。

  组及其对应的组 ID（GID）将被分配为用户的首要 GID。如果所选用户帐户已具有首要 GID，则该组的 GID 将被分配给用户作为次要组。

  您可以选择以下任一方式将用户分配到组：

  - *现有的 eDirectory 组*—如果 Group 对象尚未为 Linux 启用，则其属性将被扩展以包含 Linux 登录属性。您可以单击对象选择器图标以浏览树以查找现有组。

  - *现有的 Linux 启用组*—此选项允许您选择现有的 eDirectory Group 对象。如果您使用对象选择器进行浏览，则只能查看和选择已扩展 Linux 登录属性的 Group 对象。

  - *创建新的 Linux 启用组*—此选项允许您创建新的 eDirectory Group 对象。创建时，Group 对象将被扩展以包含 Linux 登录属性。

- 6. 选择用户组中的用户应有权访问的 *工作站*；然后选择下一步。

- 7. 应用更改并继续，选择完成；然后选择确定。

用户现在应该能够使用其 eDirectory 用户登录凭据登录到其 SUSE Linux Enterprise Desktop 工作站。
