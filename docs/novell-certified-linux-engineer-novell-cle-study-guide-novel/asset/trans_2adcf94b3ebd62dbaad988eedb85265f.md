

![](img/c7771e8540507f2b00c088c7a411b57b_396_0.png)

图 8.43
NetStorage 主页。

在这种情况下，iFolder 无法提供协助。由于该文件不是同步的 iFolder 目录，因此无法使用 iFolder 工具访问它。然而，如果在服务器上运行配置正确的 NetStorage 服务，用户可以通过浏览器访问 Samba 共享，从而获取其文件。

NetStorage 利用 CIFS 协议，使得在使用 Web 浏览器访问 Samba 共享时强制执行用户权限。因此，在用户能够通过 NetStorage 访问 Samba 共享之前，您必须在 eDirectory 中启用 LUM/Samba 用户。

如前所述，NetStorage 还允许用户在浏览器窗口中访问 iFolder 服务器上的 iFolder 文件。与 Samba 一样，用户必须先启用 iFolder 才能执行此操作。

如您所见，NetStorage 真正补充了 iFolder 和 Samba，而不是重复它们的功能。有时，新接触 NNLS 的学生会对使用浏览器协议通过互联网（甚至在其组织网络中）传输文件表达安全顾虑。

我们都听说过关于被劫持的 FTP 和 Telnet 会话的恐怖故事。使用 NetStorage，您无需担心。您可以配置 NetStorage 使用 SSL 加密文件传输。接下来，让我们讨论一下 NetStorage 的存储位置。

## NetStorage 存储位置

回顾图 8.43，请注意有一个名为 **shared** 的文件夹。默认情况下，NetStorage 为所有 NetStorage 用户提供一个共享存储位置，即使他们未启用 LUM/Samba 或 iFolder。此共享文件夹默认位于服务器文件系统中的 `/var/opt/novell/netstorage/shared` 目录。

再次参考图 8.43，请注意有一个用于用户 iFolder 账户的文件夹。如果用户已启用 iFolder，他们可以从 iFolder 服务器访问其 iFolder 文件。

当用户点击 iFolder 文件夹时，系统会提示其提供 iFolder 密码短语。这如图 8.44 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_397_0.png)

![](img/c7771e8540507f2b00c088c7a411b57b_397_1.png)

在练习 8.1 中，您为 DNelson.IFCLE 用户对象配置了 iFolder。作为练习的一部分，您创建了一个名为 MyFile.doc 的目录并输入了一些文本。使用 NetStorage，您可以访问位于 iFolder 服务器上的该文件的同步版本。这如图 8.45 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_398_0.png)

图 8.45
在 NetStorage 中访问 iFolder 文件。

我之前提到，NetStorage 还可以访问 Samba 共享。对此类存储的访问是通过 *Storage Location*（存储位置）对象配置的。

Storage Location 对象是 eDirectory 树中的一个指针对象，它指示 NetStorage 指向已在 `smb.conf` 文件中定义的 Samba 共享。用户与 Storage Location 对象相关联，从而通过 NetStorage Web 界面访问 Samba 共享。由于 Storage Location 对象依赖于 Samba，NetStorage 用户必须已启用 LUM/Samba。

如果您想要在 Linux 文件系统中创建一个目录并让 NetStorage 用户访问它，您必须首先在 `smb.conf` 文件中为该目录定义共享并重启 novell-smb 服务。让我们看看这是如何完成的。

## 配置 NetStorage

涵盖的测试目标：

- 6. 安装和配置 NetStorage。

与 iFolder 和 Samba 一样，CLE 考试目标规定您能够安装和配置 NetStorage。正如我们之前所做的那样，我们将只简要介绍 NetStorage 的安装，因为第 5 章的大部分篇幅都用于讨论 NNLS 安装过程。

### 安装 NetStorage

关于 NetStorage，您需要牢记的唯一关键事实是它不能单独安装。如果您执行自定义 NNLS 安装，您会注意到组件选择屏幕上没有 NetStorage 选项。

要安装 NetStorage，您必须安装 NNLS Virtual Office 组件。在 NNLS 早期的测试阶段，情况并非如此。当时 NetStorage 可以单独安装。在产品中期测试阶段，这一情况发生了变化，NetStorage 被合并到了 Virtual Office 产品中。当时我有机会与 NetStorage 的程序员交谈，并询问他们为什么要这样做。

他们解释说，它只是 Virtual Office 的一个非常核心的组成部分，因此将这两个产品合并到单个安装中是有意义的。当我们稍后在这本书中介绍 Virtual Office 时，我想您会同意这个决定是合理的。

与 iFolder 一样，如果您执行了快速安装，NetStorage 已安装在您的系统上。如果您执行了自定义安装，您有机会选择安装 Virtual Office 组件。

如果在 NNLS 初始安装过程中未选择 Virtual Office（进而未选择 NetStorage），您可以通过完成以下步骤执行安装后配置：

- 挂载您的 NNLS ISO 映像。
- 运行 install.sh 脚本。
- 当提示时，指定自定义安装。
- 当提示选择要安装的产品时，取消选择所有产品。
- 选择 Virtual Office。
- 按照第 5 章中说明的指令完成安装。

让我们花本章剩余的时间讨论如何配置 NetStorage。

### 配置 NetStorage

回顾图 8.43，请注意通过 NetStorage 可用的唯一存储是用户的 iFolder 目录和公共共享目录。这是因为 eDirectory 树中尚未为 NetStorage 配置 Storage Location 对象。

### 配置存储

要创建 Storage Location 对象，请完成以下步骤：

- 在 Linux 文件系统中创建您希望 NetStorage 用户能够访问的目录。
- 编辑您的 smb.conf 文件，为步骤 1 中创建的目录创建 Samba 共享。
- 重启您的 novell-smb 服务。
- 打开 Web 浏览器并导航至 `https://your_server_IP_address/nps/iManager.html`。
- 作为您的 admin 用户进行身份验证。
- 向下滚动到 File Access (NetStorage)（文件访问（NetStorage））角色，并选择 Storage Location: Create task（存储位置：创建任务）。Storage Locations: Create Object（存储位置：创建对象）屏幕将出现，如图 8.46 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_400_0.png)

图 8.46
创建 Storage Location 对象。

- 在 **Object Name**（对象名称）字段中，输入 Storage Location 对象的名称。
- 在 **Display Name**（显示名称）字段中，输入您希望用户在 NetStorage 中看到的 Storage Location 对象的名称。
- 在 **Directory Location**（目录位置）字段中，输入该目录在 Linux 文件系统中的位置。

第一次配置 Storage Location 对象时，这一步经常让许多人陷入困境（至少在我第一次尝试创建 Storage Location 对象时是这样）。字段名称听起来似乎可以输入一个简单的目录路径，但事实恰恰相反。

在此字段中，您必须输入一个 URL，而不是像 /tmp 这样的路径。如果您指向 Linux 服务器上的目录，URL 的格式如下：

`cifs://server IP address/Samba_share`

例如，如果您的共享名称是 tmp（如本章前面创建的那样），并且您的服务器 IP 地址是 192.168.1.36，您将输入以下内容：

`cifs://192.168.1.36/tmp`

> **提示**
> 如果您恰好指向 NetWare 服务器，请按照 `ncp://server IP address/volume name/path` 的格式输入 URL。

- 在 **Context**（上下文）字段中，输入 Storage Location 对象在 eDirectory 树中所在的上下文。
- 点击 **Create**（创建）。
- 当提示对象已创建时，点击 **OK**（确定）。

创建完所有 Storage Location 对象后，接下来您需要创建 *Storage Location Lists*（存储位置列表），用于将 Storage Location 对象与 eDirectory 用户、组或容器对象关联。通过此类列表关联的用户在登录 NetStorage 时，将看到列表中显示的存储位置。

要创建 Storage Location List，请完成以下步骤：

- 在 iManager 中，选择 **File Access (NetStorage)**（文件访问（NetStorage））下的 **Storage Location: Create/Modify List**（存储位置：创建/修改列表）任务。将显示图 8.47 中所示的屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_401_0.png)

![](img/c7771e8540507f2b00c088c7a411b57b_401_1.png)

- 在 **Object**（对象）字段中，浏览并选择您想要与 Storage Location 对象关联的用户、组或容器对象。
  - 如果您选择用户对象，仅该用户将有权访问存储位置。如果您选择组对象，该组的所有成员将有权访问。如果您选择容器，位于该容器内的所有用户将有权访问。
- 点击 **OK**（确定）。将显示图 8.48 中的屏幕。
- 在 **Storage Location Objects**（存储位置对象）字段中，浏览并选择您想要与列表关联的 Storage Location 对象。您可以选择多个对象。

