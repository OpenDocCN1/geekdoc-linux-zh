
如果这些权限会导致安全风险，您可能不希望将 CN 属性分配给 `[Public]` 对象。

如果您的 iFolder 服务器位于防火墙外部，并且不希望在 NDS 树中的所有对象上分配 CN 属性，还可以使用 LDAP 代理用户名来搜索树的子容器。

e. (条件) 如果要添加要搜索的额外上下文，请选择 **添加**。

f. 通过选择 **更新** 保存这些默认用户身份验证设置。

在不同上下文中具有相同 CN 的多个用户会阻止用户成功验证到 iFolder 服务器。只有具有唯一 CN（通用名称）的用户才能进行身份验证。

### 4. 启用用户访问 iFolder

在用户可以在其本地工作站上使用 iFolder 之前，您必须首先在 iFolder 管理控制台中启用其用户对象。

用户只能将一个帐户关联到一个给定的用户 ID。但是，用户可以拥有多个不同用户 ID 下的帐户。

启用用户对象后，指示用户登录到 iFolder 服务器以创建 iFolder 帐户。

用户首次通过 iFolder 客户端、iFolder 网站登录页面上的 Java 小程序或 NetDrive 登录到 iFolder 服务器时，会创建 iFolder 帐户。

a. 从 iFolder 管理控制台，选择 **高级搜索**；然后选择要用于查找刚安装 iFolder 的服务器上的所有用户的标准。确保指定了正确的用户 LDAP 上下文。您可以使用名称、名、姓、电子邮件地址、用户类型、iFolder 服务器和用户 LDAP 上下文等搜索标准。

b. 通过选择 **搜索** 开始搜索。

将出现匹配搜索标准的用户列表：

**图 6-6**

![](img/d63035f3fce0eaaf97203dde900affb7_39_0.png)

c. 选择所有想要拥有 iFolder 帐户的用户；然后执行以下任一操作：

- 选择 **启用** 按钮，位置在“将已选用户作为 iFolder 用户”。
*或*
- 选择 **启用** 按钮，位置在“将所有列出的用户作为 iFolder 用户”。

如果您的第一个 iFolder 服务器也运行 LDAP，则 iFolder 配置已完成。在用户登录以创建其 iFolder 帐户后，您可以开始管理他们的帐户。

### 如何访问 iFolder 网站

在服务器上安装和配置 iFolder 后，您的用户可以下载并安装 iFolder 客户端，然后登录到 iFolder 服务器。

用户首次使用 iFolder 客户端登录时，如果他们帐户已在 iFolder 管理控制台中启用，他们将激活其 iFolder 帐户。

在服务器上安装 iFolder 后，您可以访问以下网站：

- **iFolder 网站。** 要访问默认 iFolder 网站，请在 Web 浏览器中输入以下 URL：

  `https://IP_or_domain/iFolder`

  其中 `IP_or_domain` 是您的 iFolder 服务器的 IP 地址或域名。

将出现以下内容：

![](img/d63035f3fce0eaaf97203dde900affb7_41_0.png)

![](img/d63035f3fce0eaaf97203dde900affb7_41_1.png)

该网站包含 Novell iFolder 2.1 用户指南、iFolder 2.1 快速入门以及有关 Novell iFolder 的其他重要信息。

该网站是用户下载 iFolder 客户端的地方。如果用户使用未安装 iFolder 客户端的计算机，他们也可以使用“登录”链接通过浏览器（使用 Java 小程序）访问其 iFolder 文件。

用户必须先通过 iFolder 客户端建立其 iFolder 帐户，然后才能使用 Java 小程序访问该帐户。

iFolder Java 小程序仅适用于 Internet Explorer，不受任何其他浏览器支持。

要从 Linux 工作站访问 iFolder 中的文件，请使用 NetStorage，这将在后面的章节中介绍。

若要直接访问 Web 浏览器登录页面，请输入：

```
https://IP_or_domain/iFolder/Myfiles
```

您可以修改此页面以适应公司的内部需求。

- **iFolder 管理控制台。** 您可以使用它管理用户的 iFolder 账户以及 iFolder 和 LDAP 服务器。

要访问 iFolder 管理控制台，请打开浏览器并输入以下内容：

```
https://IP_or_domain/iFolderServer/Admin
```

其中 `IP_or_domain` 是 iFolder 服务器的 IP 地址或 DNS 域名。

如果在安装时指定了不同的端口，请在服务器 IP 地址后添加冒号，然后跟上端口号。例如：

```
https://192.168.1.1:81/iFolderServer/Admin
```

## 更改 iFolder 数据目录

如果在安装 iFolder 之后，您需要更改 iFolder 数据目录的位置，请执行以下操作：

1. 在新位置创建一个 `ifolderdata` 文件夹。例如，如果您想将位置更改为 `/home/ifolderdata`，请输入以下命令：

```bash
mkdir /home/ifolderdata
```

2. 将 `/var/opt/novell/ifolderdata` 的内容复制到新位置。

3. 通过更改 `iFolderServerRoot` 参数来指示新目录位置，从而修改 `/etc/opt/novell/ifolder/httpd_ifolder_unix.conf` 文件。

例如：`iFolderServerRoot "/home/ifolderdata"`

4. 对新父目录应用必要的属主和权限。指定的属主应为 `novell`，指定的组应为 `novell`。权限应为 `700`。

例如，请输入以下命令：

- `ls -l /home/ifolderdata`（用于查看当前的属主和权限设置）
- `chown novell:novell /home/ifolderdata`
- `chmod 700 /home/ifolderdata`
- `ls -l /home/ifolderdata`（用于查看对属主和权限设置所做的更改）

5. 通过输入以下内容重启 `novell-httpd`：

```bash
/etc/init.d/novell-httpd restart
```

## 如何安装和配置 iFolder 客户端

您需要在使用的一台桌面或笔记本电脑上安装 Novell iFolder 客户端软件。iFolder 客户端专为以下 Microsoft® 操作系统环境中的工作站设计：

- Windows 98/ME
- Windows XP 家庭版和专业版
- Windows 2000 专业版

您需要在工作站上安装 iFolder 客户端才能利用 iFolder 的自动同步功能。但是，您可以使用任何计算机、Web 浏览器和活动的 Internet 连接访问 iFolder 服务器上的文件。

在安装客户端之前，请确保您的工作站满足以下先决条件：

- 已安装 Internet Explorer (IE) 5.0 或更高版本
- 已激活 Internet 连接

要在工作站上安装并配置 iFolder 客户端，请执行以下操作：

1. 通过 Web 浏览器，输入以下内容以访问您的 iFolder 网站：

```
https://IP_or_domain/iFolder
```

其中 `IP_or_domain` 是 iFolder 服务器的 IP 地址或域名。

iFolder 主页将会显示。

2. 在右侧的 *iFolder Windows Client* 下，选择 **Download**（下载）；然后选择 **Save**（保存）。

3. 将 iFolder 客户端安装文件保存到您的桌面上。

将显示 *Download complete*（下载完成）对话框。

4. 通过选择 **Open**（打开）开始安装。

5. 在 *Novell iFolder Setup*（Novell iFolder 安装程序）欢迎窗口中，选择 **Next**（下一步）。

6. 选择您的语言；然后选择 **Next**（下一步）。

*License Agreement*（许可协议）将在浏览器窗口中显示。

7. 关闭浏览器窗口；然后通过选择 **Yes**（是）接受许可协议。

8. 通过选择 **Next**（下一步），将 iFolder 客户端安装在默认文件夹（`C:\Program Files\Novell\iFolder`）中。

9. 选择 **Finish**（完成）。

浏览器窗口中将显示 readme 文件。

10. 查看 readme 文件；然后关闭窗口。

11. 执行以下操作之一：
