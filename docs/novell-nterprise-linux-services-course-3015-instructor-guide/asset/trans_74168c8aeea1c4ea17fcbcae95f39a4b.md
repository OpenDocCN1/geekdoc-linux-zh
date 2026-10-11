

如果您将 iFolder 服务器部署在防火墙之后，请务必记住，iFolder 使用 80 和 443 端口来进行客户端和服务器访问。管理页面和 iFolder 客户端认证将通过 443 端口进行。

## iFolder 架构

要了解 iFolder 组件和架构如何协同工作以同步并提供对个人文件的访问，您需要了解以下内容：

- Web 服务器与 iFolder
- LDAP 与 iFolder
- 身份验证与同步
- iFolder 如何同步文件

### Web 服务器与 iFolder

iFolder 服务器软件使用 Apache 作为 NetWare 和 Linux 服务器操作系统的默认 Web 服务器。在 Windows 2000 上，iFolder 使用 IIS Web 服务器。

当在 NetWare 服务器上使用基于 Apache 的解决方案运行 iFolder 时，它可以运行在操作系统空间或保护内存空间中。

由于 iFolder 需要对 Apache 特定文件进行一些配置更改，因此我们建议您将 iFolder 安装在没有其他依赖 Apache 的应用程序的服务器上。

如果您确实有其他使用 Apache 的应用程序，那么在安装 iFolder 时，这些应用程序可能无法正常工作。

### LDAP 与 iFolder

iFolder 使用 LDAP 进行用户身份验证。它使用 Novell eDirectory 或 Microsoft Active Directory（适用于 Windows 2000）作为其所有特定的 iFolder LDAP 对象的中心位置。

您可以让 iFolder 和 LDAP 运行在同一台服务器或不同的服务器上。

iFolder 使用以下 LDAP 目录：

- **全局设置 LDAP 目录。** 此目录存储有关 iFolder 系统配置的信息，并包含 iFolder 设置、iFolder 服务器和 LDAP 服务器对象。
- **用户 LDAP 目录。** 此目录用于身份验证，并为已在 iFolder 管理控制台中授权使用 iFolder 的用户对象添加 iFolder 服务器名称和磁盘配额属性。

无论您拥有多少台 iFolder 服务器，您都只有一个全局设置 LDAP。

但是，您可以拥有多达八个用户 LDAP 目录。多个 LDAP 目录有利于那些用户对象已划分为不同 LDAP 目录的公司。

例如，如果您有一个用于所有供应商的 LDAP 目录，另一个用于您的全职员工，还有一个用于您的临时雇用人员，您可以在 iFolder 中设置三个用户 LDAP 目录来处理每个目录的 iFolder 账户。

在决定是使用 LDAP over SSL（端口 636）还是明文（端口 389）连接时，请考虑以下事项：

- 如果您希望不使用 SSL 加密而使用 LDAP，或者您的 LDAP 服务器不支持 SSL，请选择端口 389。
- 如果 iFolder 和 LDAP 运行在同一台服务器上，端口 389 也是一个不错的选择。由于没有数据通过线路传输，因此不需要加密。
- 如果您希望使用 SSL，请在数据通过线路传输时为您的网络提供加密和安全性，请选择端口 636。

如果您选择端口 636，在 NetWare 6 安装完成后将需要进行一些后续配置。

> 如果您希望使用 LDAP over SSL，并且您的 LDAP 服务器与您的 iFolder 服务器不同，您需要导出 LDAP 服务器的可信根证书，然后将其复制到您的 iFolder 服务器。

### 身份验证与同步

当您登录 iFolder 时，iFolder 客户端通过互联网连接将加密的用户名和密码发送到 iFolder 服务器，从而对 iFolder 服务器进行身份验证。

> 这些凭据使用 RSA 加密并通过 HTTP 数据包发送到服务器。当服务器对用户进行身份验证时，它们之间的所有后续通信都使用 128 位 Blowfish 算法进行加密。然而，所有通信仍然通过标准 http 端口 80 进行。

iFolder 服务器使用此信息来验证用户是否存在，然后检查该用户对象是否已在 iFolder 管理控制台中启用以使用 iFolder。

在用户对象启用后，在用户可以开始在本地工作站上使用 iFolder 之前，必须在 iFolder 服务器上创建一个用户账户。用户第一次使用 iFolder 客户端登录 iFolder 服务器时，将创建该账户。

创建用户账户后，可以使用 iFolder 管理控制台对该账户进行管理。

首次登录后，用户即可开始向他的 iFolder 目录添加文件，自动同步随即开始。在首次登录时，iFolder 服务器上的用户账户将被创建，并且 iFolder 主目录会被放置在用户的桌面上。

iFolder 客户端始终了解任何本地活动，并根据您（作为网络管理员）或用户选择的同步首选项，iFolder 客户端定期向 iFolder 服务器请求下载任何新数据。

在 iFolder 服务器下载数据后，它会上传来自本地 iFolder 目录的任何更新。当您从另一台计算机访问您的账户时，iFolder 服务器会先下载任何更新，然后再上传 iFolder 客户端的更改。

![](img/d63035f3fce0eaaf97203dde900affb7_22_0.png)

有关 iFolder 组件和架构的更多详细信息，请参见位于 http://www.novell.com/documentation/ig/ifold er21 的《Novell iFolder 安装与管理指南》中的“身份验证、加密和同步深入解析”。

### iFolder 如何同步文件

以下步骤概述了本地硬盘驱动器上的文件与 iFolder 服务器之间的同步过程：

![](img/d63035f3fce0eaaf97203dde900affb7_23_0.png)

1. 用户通过 iFolder 客户端对 iFolder 服务器进行身份验证。
2. iFolder 服务器执行 LDAP 绑定，并验证用户是否在正确的服务器上。如果不是，服务器将用户重定向到正确的服务器。
3. iFolder 客户端执行调整操作，并检查用户工作站上的文件与服务器上的文件。
4. iFolder 从服务器下载任何新文件，然后上传本地 iFolder 文件夹中的任何新文件。
   - 在此过程中，iFolder 仅在 4 kb 块级别同步现有文件的已更改部分。
5. iFolder 服务器接收新文件并增加同步索引。同步索引指示文件系统的当前状态。

iFolder 服务器上的同步索引与客户端工作站上的同步索引匹配，表明没有发生更改。这是 iFolder 客户端判断是否不同步的方式。同步索引仅为 4 字节，且是一项成本极低的服务器操作。

6. 当另一个 iFolder 客户端工作站连接到 iFolder 服务器时，服务器会比较同步索引并下载任何新文件。
7. 如果有新文件，iFolder 监控文件系统并捕获该事件。
8. 然后 iFolder 将文件上传到服务器，iFolder 服务器增加同步索引。
9. 如果发生冲突，iFolder 使用时间戳进行解决，旧文件将被放置在冲突垃圾箱中。

## 目标 2 安装和配置 iFolder

您在 Linux 上安装和配置 iFolder 分为四个基本阶段：

1. 安装第一台 iFolder 服务器。
2. 配置全局设置、默认策略、LDAP 身份验证源和 iFolder 服务器。
3. 为 iFolder 用户提供配置。
4. 安装额外的 iFolder 服务器（如有需要）。

为了完成这些阶段并管理 iFolder，您需要了解以下内容：

- 在 Linux 服务器上安装的前置条件
- 如何从 NNLS 安装 iFolder
- 如何配置您的 iFolder 服务器
- 如何访问 iFolder Web 站点
- 如何安装和配置 iFolder 客户端
- 如何管理 iFolder 用户账户
- 如何管理 iFolder 服务器
- 如何管理 LDAP 服务器
- 如何监控您的 iFolder 系统
- 如何生成报告

### 在 Linux 服务器上安装的前置条件

在您使用 NNLS 安装 Novell iFolder 2.1 之前，请确保您的 Linux 服务器和企业网络环境满足以下所有前置条件：

- **iFolder 服务器要求。** 配置一个包含以下组件的企业服务器：
  - 最低 450 MHz Intel® Pentium® II 处理器。
  - 最低 512 MB RAM。如果服务器支持除 iFolder 以外的程序或服务，请增加更多 RAM。
  - 服务器软件（约 15 MB）加上所有用户 iFolder 账户的用户数据的存储容量。
  - 作为指导，请考虑预期用户数量以及分配给每个 iFolder 用户账户的存储配额。
  - 此外，还要考虑与每个参数相关的可能增长，以预测未来的存储需求。
  - 一个活跃的网络或互联网连接，根据部署情况，具有与其他网络或互联网上计算机的全双工访问权限。
- **iFolder 服务器 Linux 要求。** 在您的 iFolder 服务器上安装并配置 Red Hat Enterprise Linux AS/ES 2.1 或 SLES 8，包括所有服务包和补丁。

