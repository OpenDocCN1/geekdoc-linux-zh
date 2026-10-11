
要创建存储位置列表，请执行以下操作：

1.  启动浏览器，并输入以下内容以启动 iManager：**https://IP_or_DNS/nps/iManager**
2.  输入您的*用户名*和*密码*登录。
3.  在左侧**文件访问（NetStorage）**下，选择**存储位置：创建/修改列表**。
4.  选择**对象选择器**按钮；然后浏览并选择要为其创建列表的用户、组、配置档案或容器对象。
5.  完成后，选择**确定**。
6.  选择**对象选择器**按钮；然后选择要包含在此列表中的*存储位置对象*。
   -   您可以在对象选择器窗口中选择多个存储位置对象。当您选择多个存储位置对象时，它们将显示在已选对象列表中。
   -   如果列表中已包含存储位置对象且您想添加更多，请在选择确定之前确保原始对象仍在列表中。
   -   您可以通过在选择确定之前从列表中删除现有存储位置的名称来移除它们。
7.  完成创建或修改列表后，选择**确定**。

## 访问 NetStorage 文件和文件夹

根据 NetStorage 的配置方式，NetStorage 网页将显示您可以访问的网络文件和文件夹。

最初，您可能只能看到您的 iFolder 目录和 Linux 服务器上的本地共享目录。访问 Linux 服务器上的文件和目录需要存储位置对象，这些对象也可以用于 NetWare 服务器。

对于 NetWare 服务器，NetStorage 读取您的 NetWare 登录脚本以确定驱动器映射，读取 eDirectory 用户对象属性以确定您的主目录，然后根据映射的驱动器和主目录显示文件和文件夹列表。

如果您通常登录到多个 eDirectory 树，您可能可以访问不同 eDirectory 树中的其他主目录。

如果您拥有 Novell iFolder 帐户，也会显示 iFolder 目录。但是，某些 NetStorage 功能（如下载以供编辑）在 Novell iFolder 中不可用。

NetStorage 仅从安装过程中指定的主要 eDirectory 服务器读取容器、配置档案和用户登录脚本，并仅根据这些登录脚本显示用户的驱动器映射。

用户可能对网络中的某些文件和文件夹具有特定的 eDirectory 权限，但如果未创建存储位置对象、不存在指向这些文件夹的登录脚本驱动器映射，或者这些文件和文件夹不在用户的主目录中，他们将无法使用 NetStorage 访问这些文件和文件夹。

如果您希望允许用户通过 NetStorage 访问特定文件夹，您可能需要在那条登录脚本（容器、配置档案或用户）中添加指向该文件夹的驱动器映射命令。

要从工作站访问 NetStorage，请执行以下操作：

- 启动浏览器并指定 NetStorage 的以下 URL：`https://IP_or_DNS/NetStorage`
  - 用于访问 NetStorage 的工作站的日期和时间应与运行 NetStorage 的服务器的日期和时间大致相近（在几小时内），以避免冲突。
- 输入您的*用户名*和*密码*。
  - NetStorage 使用您的 Novell eDirectory 用户名和密码，因此您无需记住或使用单独的用户名或密码。
  - 您可以使用许多与 Windows 资源管理器中可用的展开和收缩文件夹以及打开文件相同的约定。
  - 要通过浏览器创建新文件夹，或复制、删除、重命名、移动或下载现有文件，请选择**文件**菜单上的选项。
  - 在浏览器窗口中选择文件夹视图按钮可在另一列中显示文件夹，并允许您展开和收缩文件夹。
  - 文本视图仅显示当前目录中的文件和文件夹，不允许展开或收缩文件夹。
  - 本地文件和文件夹无法通过 NetStorage 访问。此外，您不能从 NetStorage 映射驱动器或更改登录脚本。
- 完成后，关闭 Web 浏览器。

## 配置 NetStorage

使用 Novell iManager，您可以在将 NetStorage 安装到 Linux 服务器后更改其 NetStorage 配置。

![](img/d63035f3fce0eaaf97203dde900affb7_117_0.png)

更改任何设置后，必须重新启动 Apache Web 服务器。

要重新启动 Apache Web 服务器，请转到 `/etc/init.d` 目录并输入 **/novell-httpd restart** 以停止并启动 Web 服务器。

要配置 NetStorage，请执行以下操作：

1.  从 Web 浏览器启动并登录到 iManager。
   -   用于访问 NetStorage 的工作站的日期和时间应与运行 NetStorage 的服务器的日期和时间大致相近（在几小时内），以避免冲突。
2.  在左列中，找到要更改的 NetStorage 配置选项。

### 图 6-20

以下图示说明了这些选项：

![](img/d63035f3fce0eaaf97203dde900affb7_118_0.png)

提供以下配置选项：

-   **身份验证域**。允许您更改或添加 NetStorage 所需的 eDirectory 服务器 URL 和上下文。这允许您访问两个或多个 eDirectory 树。此页面还允许您更改指定为主要 eDirectory 服务器的 eDirectory 服务器。
-   **浏览文件**。显示 NetStorage 网页。
-   **当前会话**。显示包含当前 NetStorage 会话信息的报告。
-   **常规**。允许您配置位置、证书名称、会话超时、清理级别和 LDAP 端口等项目。
-   **iFolder 存储提供程序**。如果您在 Linux 服务器上安装了 Novell iFolder，您可以查看或编辑诸如根目录、口令短语表单协议、iFolder 服务器和安全端口等配置设置。
-   **NetWare 存储提供程序**。允许您查看或编辑诸如主名称、驱动器名称和容器搜索高度等配置设置。
-   **资源使用情况**。显示 NetStorage 资源利用率的详细报告。
-   **统计信息**。显示包含服务器正常运行时间、登录失败次数、NetStorage 会话数等信息的报告。
-   **存储位置**。允许您创建存储位置对象，以在通过 Web 浏览器显示的 NetStorage 目录访问列表中为网络目录显示指定名称。
-   **WebDAV 提供程序设置**。允许您配置 NetStorage WebDAV 提供程序（Moniker）的位置以及 HTML 接口的目录。
3.  完成后，关闭 Web 浏览器。

> 有关设置这些配置选项和故障排除 NetStorage 的详细信息，请参阅 http://www.novell.com/documentation 上的 NetStorage 管理指南。

### 练习 6-5 配置和测试 NetStorage

![](img/d63035f3fce0eaaf97203dde900affb7_120_0.png)

作为您的 Digital Airlines 办公室的网络管理员，您被分配为刚刚成立的效率项目组配置 NetStorage 服务。

您还被要求为团队负责人 SRIfe 创建一个个人文件夹。

效率项目组由 ACCTUSERS 组组成。

您将在 3 个部分中完成此任务。

- 第一部分：测试默认 NetStorage 配置
- 第二部分：配置团队负责人使用个人文件夹
- 第三部分：创建一个项目组可用于共享文件的项目文件文件夹

#### 第一部分：测试默认 NetStorage 配置

在此练习部分，您将通过不修改 smb.conf 文件且不将 eDirectory 用户转换为 LUM 或 Samba 来测试默认的 NetStorage 配置。

通过这样做，您将看到默认配置并未提供您被分配创建的 NetStorage 服务。

为此，请执行以下操作：

1.  访问默认**共享**文件夹并上传文件到其中：
   a. 在 Windows XP 工作站上，启动**Internet Explorer**。
   b. 输入 `https://your_server_DNS/NetStorage`。
   c. 当提示时，使用密码 `novell` 以 `kfullmer` 的身份进行身份验证；然后选择**确定**。
   d. 展开**NetStorage** 文件夹。

