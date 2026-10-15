
iFolder 使用加密技术保护数据在通过网络时免受破坏。当用户向 iFolder 认证时，他们必须提供密码和口令短语。口令短语用于加密文件，保护其免受窥探。

当用户认证时，iFolder 服务器使用 LDAP 访问 eDirectory 以检查用户的凭证。如果凭证匹配，用户将获得访问与其用户身份关联的文件的权限。iFolder 服务器可以配置为使用不安全的 LDAP 端口（`389`）或安全的 LDAP 端口（`636`）。除非你有充分的理由不这样做，否则你应始终配置 iFolder 使用安全的 `636` 端口。

使用 `636` 端口的原因是，LDAP 服务不必运行在与 iFolder 相同的服务器上（尽管可以如此）。iFolder 服务可以使用 eDirectory 树中任何服务器上的 LDAP 服务。如果你使用不安全的 LDAP 端口，并且 iFolder 和 LDAP 运行在不同的服务器上，所有认证信息，如用户名和密码，将以明文传输，从而容易被网络嗅探器捕获。

iFolder 也可以使用活动目录（Active Directory）来认证用户。

如果你在同一台服务器上运行 iFolder 和 LDAP 服务，你可以使用 `389` 端口。因为来自 iFolder 服务器的所有 LDAP 查询都在同一台机器上进行，它们不通过网络介质，无法被嗅探。然而，使用安全的 LDAP 端口（`636`）仍然是良好的做法。

如果你选择使用 `636` 端口，并且你的 LDAP 服务运行在与 iFolder 服务器不同的服务器上，你需要完成一些额外的配置步骤。例如，你需要导出 LDAP 服务器的可信根证书并将其复制到你的 iFolder 服务器。

值得注意的是，你可以配置单个 iFolder 服务器使用多达八个不同的 LDAP 服务来认证用户。如果你的组织拥有多个存储用户账户的目录服务，这将非常有用。

许多刚开始接触 iFolder 的学生在此时会问：“如果为了让 iFolder 工作必须在防火墙上打开 `80` 和 `443` 端口，我是否也应该打开 `389` 和 `636` 端口以便 LDAP 认证也能工作？”

实际上，不需要，它们通常不需要被打开。这是因为 iFolder 客户端不向 LDAP 服务发送 LDAP 请求。这是 iFolder 服务器的工作。如果 iFolder 服务和 LDAP 服务都在防火墙之后或在同一台服务器上，你不需要在防火墙配置中打开 LDAP 端口——通常情况就是这样。

如果由于某种原因，在 iFolder 服务器和运行 LDAP 服务的服务器之间存在防火墙，你需要在防火墙配置中打开 LDAP 端口。

带着这个想法，让我们快速概览一下同步过程。

## 使用 iFolder 同步文件

第一次使用 iFolder 客户端登录 iFolder 服务器时，会在 iFolder 服务器上为你的用户对象创建一个账户，并在本地 Windows 用户账户的“我的文档”目录中创建一个 iFolder 目录，如图 8.2 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_350_0.png)

**图 8.2**

iFolder 同步目录。

此外，本地 Windows 工作站用户账户的桌面上会有一个指向 iFolder 目录的快捷方式；这如图 8.3 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_350_1.png)

**图 8.3**

iFolder 快捷方式。

创建 iFolder 目录后，你可以开始使用 iFolder 同步数据。iFolder 使用以下过程来实现这一点：

1. 用户向其工作站上运行的 iFolder 客户端提供所需的登录凭证。
2. iFolder 客户端将这些凭证发送到 iFolder 服务器。
3. iFolder 服务器绑定到已配置的 LDAP 服务，并在 eDirectory 中验证用户凭证。
4. iFolder 客户端将本地 iFolder 目录中的文件与 iFolder 服务器上用户账户中的文件进行比较，并识别出不匹配的 4KB 文件块。
5. iFolder 客户端从 iFolder 服务器下载已识别的现有文件的更改。如前所述，iFolder 客户端不会下载整个文件。它仅下载数据已更改的 4KB 块。
6. iFolder 客户端上传自上次同步以来更改的任何新文件或文件块。
7. iFolder 服务器标记其已接收的文件为已同步。它使用称为同步索引号（Sync Index Number）的属性。iFolder 服务器和客户端在未来使用此属性来确定给定文件是否已同步。如果服务器和客户端版本的此属性值相同，则该文件被视为已同步。如果值不同，则该文件被视为未同步。

如果文件的两个版本具有相同的同步索引号但明显不同，则该文件被称为存在*冲突*。iFolder 然后会比较两个版本的时间戳以确定哪个版本是最新的，并使用同步更新另一个版本。

> **注意** 如果检测到冲突，iFolder 会将文件的旧版本保留在冲突箱（Conflict Bin）中，以防它是正确版本。

基于这些入门材料，让我们深入了解，以便你可以学习如何在你的服务器上安装和配置 iFolder。

## 安装和配置 iFolder

**涵盖的测试目标：**

- 2. 安装和配置 iFolder。

请注意，本章这一部分涵盖的 CLE 目标要求你安装和配置 iFolder。然而，我们不会花费大量时间回顾如何安装 iFolder。

### 安装 iFolder

与 DirXML 一样，如果你执行了快速安装，iFolder 已安装在你的系统上。如果进行了自定义安装，你有机会选择安装 iFolder 组件。

如果在 NNLS 初始安装期间未选择 iFolder，你可以按照以下步骤完成安装后操作：

1. 挂载你的 NNLS ISO 映像。
2. 运行 `install.sh` 脚本。
3. 当提示时，指定自定义安装。
4. 当提示选择要安装的产品时，取消选择所有产品。
5. 选择 iFolder。
6. 根据第 5 章“NNLS 安装和管理”中介绍的说明完成安装。

第一次访问 iFolder 管理控制台并选择全局设置时，你的 eDirectory 树的模式将被扩展。添加了以下对象类：

- **iFolder 服务器**—此对象在 eDirectory 树中表示你的 iFolder 服务器。
- **iFolder 用户 LDAP**—此对象在 eDirectory 树中表示 iFolder 将用于认证用户的 LDAP 服务器。
- **iFolder 设置**—此对象存储你的 iFolder 服务器的全局配置设置。

安装后，在服务器的文件系统中创建并填充了以下 iFolder 目录：

- `/var/opt/novell/ifolderdata/ACCOUNTS`—此目录包含与 iFolder 客户端同步的文件。
- `/opt/novell/httpd/bin/httpd`—此目录包含配置你的 Apache web 服务器以配合 iFolder 工作的配置文件。
- `/opt/novell/ifolder`—此目录包含 iFolder 系统文件。
- `/opt/novell/ifolder/DocumentRoot`—此目录包含 iFolder HTML 文件。
- `/opt/novell/ifolder/bin`—此目录包含 Apache web 服务器使用的 iFolder 服务器模块。

至此，让我们讨论如何在你的系统中配置和管理 iFolder。

### 配置和管理 iFolder

NNLS 的 iFolder 和 DirXML 组件在某种程度上相似，即它们都可以以多种方式进行配置，以满足特定的需求

你的网络。不过，对于 CLE 考试而言，你只需要知道如何完成以下 iFolder 管理任务：

- 配置用户访问
- 配置服务器参数
- 安装和配置 iFolder 客户端
- 监控 iFolder 系统

我们将在本节中介绍这些主题。让我们从配置用户访问开始。

#### 配置用户访问

在用户使用你服务器上的 iFolder 服务之前，你必须在 eDirectory 树中将用户对象配置为具有 iFolder 访问权限。为此，你必须首先定义将由 iFolder 服务器提供服务的那些上下文。只有位于这些上下文中的用户对象才能使用 iFolder。

接下来，你必须启用用户对象使用 iFolder。这两项任务都是使用 iFolder 管理控制台完成的。iFolder 管理控制台是一种基于 Web 的工具，专门用于配置服务器上的 iFolder 服务。

要访问 iFolder 管理控制台，请打开浏览器窗口并导航到 `https://*your_server_IP_address*/iFolderServer/Admin`。当你这样做时，会出现图 8.4 所示的屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_353_0.png)

**图 8.4**

iFolder 管理控制台。

使用 iFolder 管理控制台，你可以通过执行以下步骤来配置用户访问：
