
由于虚拟办公室主页提供对其他与 NNLS 一起安装的产品 Web 访问权限，如果你希望从虚拟办公室访问这些产品，则需要在安装过程中选择以下产品：

- eGuide™
- iFolder™
- iPrint
- NetMail™

虚拟办公室主页仅显示你所选产品的快捷按钮。

NNLS 安装程序在你选择虚拟办公室组件时会选择所有必需组件及其依赖项。它们将在同一过程中安装。

这些组件包括以下内容：

- 位于同一 NNLS 服务器上的 Apache 2.0.45
- 位于同一 NNLS 服务器上的 JVM® 1.4.1_02
- 位于同一 NNLS 服务器上的 Tomcat 4.1.24
- 网络内任意位置的 eDirectory 8.7.1 或更高版本
- iManager 2.0

请参阅表 2-4，获取成功安装尚未安装的虚拟办公室依赖项所需的信息。

### 收集所需信息

下表描述了成功安装虚拟办公室所需的信息：

| 表 9-1 | 所需配置数据 | 描述 |
| :--- | :--- | :--- |
| | eDirectory 服务器 IP 地址或主机名 | 安装虚拟办公室的 eDirectory 服务器的 IP 地址或 DNS 名称。<br><br>此服务器必须安装有 eDirectory 的主副本或读写副本。 |
| | 带上下文的 Admin 名称 | 为 iManager 指定的 eDirectory 服务器的 Admin 的完全限定名称。<br><br>必须使用带类型语法指定名称和上下文 (`cn=name.ou=organizational-unit.o=organization`)。 |
| | Admin 密码 | Admin 的密码。 |
| | NetStorage 身份验证服务器 | NetStorage 用户使用 LDAP 进行身份验证的 eDirectory 服务器的 IP 地址或 DNS 主机名。 |
| | NetStorage 代理用户 | 具有以下权限的用户对象的完全限定名称：<br>- 搜索指定为 NetStorage 身份验证服务器的 LDAP (eDirectory) 树以查找 NetStorage 用户。<br>- 如果 NetStorage 中定义了 iFolder 存储位置，则在用户首次访问存储位置时，在 eDirectory 中存储 iFolder 用户口令短语。 |
| | NetStorage 代理用户密码 | 指定为 NetStorage 代理用户的用户的密码。 |
| | NetStorage 用户上下文 | 要在 NetStorage 身份验证服务器上搜索 NetStorage 用户的上下文。（所有子上下文也会被搜索。） |
| | iFolder 服务器 IP 地址或主机名 | （可选）指定你希望创建为 NetStorage 存储位置的 iFolder 服务器的 IP 地址或主机名。这将使 iFolder 自动对虚拟办公室用户可用。 |

### 使用 NNLS 安装功能

要从 NNLS 安装虚拟办公室，请执行以下操作：

1. 执行自定义安装的步骤。

![](img/d63035f3fce0eaaf97203dde900affb7_232_0.png)

> 如有必要，请参阅第 2 节了解如何执行自定义安装的详细信息。

2. 取消选择*不想*安装的服务，选择虚拟办公室服务（以及任何你希望从虚拟办公室访问的其他服务），然后继续。

3. 接受许可协议。

4. （条件）如果提示输入 NICI 基础密钥 (NFK) 文件的位置，请输入 NFK 文件的路径。仅当之前未安装 eDirectory 时，才会询问 NICI 基础密钥。

5. 在每个提示处输入请求的信息（参见表 9-1）。

6. 查看摘要信息并进行任何必要的更正。

7. 当所有信息都正确时，完成安装。

8. 查看 readme 文件并保存安装设置日志文件。

### 定位虚拟办公室文件

安装过程中，虚拟办公室程序文件会被复制到 `/opt/novell/virtualoffice/bin`。

安装完成后，使用以下 URL 在 Web 浏览器中启动虚拟办公室：

```
http://server_DNS_address/vo
```

## 目标 3

### 配置虚拟办公室

安装虚拟办公室后，在使用该产品之前，你需要在 iManager 中配置程序设置。

一些虚拟办公室参数在虚拟办公室主页内进行配置；其他参数在 iManager 中进行配置。

在本目标中，你学习如何执行以下操作：

- 在 iManager 中管理虚拟办公室配置
- 在虚拟办公室主页中管理虚拟办公室

### 在 iManager 中管理虚拟办公室配置

在 iManager 中，你可以管理以下内容：

- 虚拟办公室服务管理
- 虚拟办公室环境管理

如果单独安装虚拟办公室（不与其他 NNLS 产品一起），你可能需要安装适当的 iManager 模块以管理虚拟办公室。

执行以下操作：

1. 在 iManager 中，选择 **Configure**（配置）。
2. 选择 **Modules**（模块）。
3. 选择 **Install**（安装）。
4. 浏览到 `/var/opt/novell/iManager/nps/packages` 并选择 `VirtualOffice.npm`。
5. 选择 **Install**（安装）。
6. 重复此过程以安装 `VirtualOfficeAdmin.npm` 模块。
7. 重启 `novell-tomcat4` 服务。

### 虚拟办公室服务管理

在 iManager 中，你可以配置以下服务：

- 公司信息服务
- NetStorage
- iPrint
- eGuide
- ZENworks®
- 书签
- **GroupWise® 配置**
- **Lotus® Notes® 配置**
- **Microsoft® Exchange 配置**
- **NetMail 配置**
- **IMAP/POP3 服务器配置**
- **公共网页**
- **更改密码**

### 公司信息服务

新闻功能允许您在主页的虚拟办公室新闻字段中发布信息。

请执行以下操作：

1. 打开 iManager。
2. 选择 **虚拟办公室管理 > 服务管理 > 公司信息**。

将显示以下内容：

![](img/d63035f3fce0eaaf97203dde900affb7_236_0.png)

![](img/d63035f3fce0eaaf97203dde900affb7_236_1.png)

3. **勾选 启用。** 如果未勾选，虚拟办公室新闻字段将不会出现在主页上。
4. **在新闻字段中输入您要发布的 *消息*。** 您可以使用纯文本或 HTML。
5. **选择 确定。**

### NetStorage

NetStorage 选项卡允许您访问 Novell NetStorage，它提供基于 Internet 的简单文件访问功能，用于访问服务器上的文件。要配置此功能，请完成以下操作：

1. **打开 iManager。**
2. **选择 *虚拟办公室管理* > *服务管理* > *NetStorage*。**

将显示以下内容：

![](img/d63035f3fce0eaaf97203dde900affb7_237_0.png)

3. **勾选 启用**。

    如果未勾选，*文件* 图标将不会出现在虚拟办公室中。

4. 执行以下其中一项操作以指定指向 NetStorage 主页的 *URL*：

    - 如果 NetStorage 位于同一服务器上，请选择 **启动到此服务器的 NetStorage 主页**。
    - 如果 NetStorage 位于远程服务器上，请指定远程服务器的 *DNS* 或 *IP 地址*。
        - 例如，`https://DNS_或_IP地址:443/NetStorage/servlet/NetStorage`
    - 输入自定义 *URL* 以启动 NetStorage。

在某些浏览器（包括 Mozilla 1.5、Internet Explorer 6.1 SP1 以及 Netscape 7.01 和 7.02）中，您在虚拟办公室服务管理插件中为 NetStorage 网页输入的 URL 不会被保存。

如果输入的 URL 未被保存，请尝试使用其他浏览器。已知 Internet Explorer 6 和 Netscape 7.1 可以正常工作。

### iPrint

iPrint 是一种软件解决方案，允许用户从任何地方向任何地方打印。

要配置此功能，请执行以下操作：

1. 打开 iManager。
2. 选择 **虚拟办公室管理 > 服务管理 > iPrint**。

将显示以下内容：

![](img/d63035f3fce0eaaf97203dde900affb7_238_0.png)

### 图 9-6

3. 勾选 **启用**。
