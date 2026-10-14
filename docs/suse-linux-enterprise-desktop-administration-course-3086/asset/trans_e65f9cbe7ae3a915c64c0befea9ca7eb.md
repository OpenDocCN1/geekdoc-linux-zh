

尽管这大大减少了服务器通信，但审计打印作业的能力就丢失了。Novell iPrint Direct 仍然支持驱动程序更新，并且打印机信息是通过 SNMP 直接从打印机收集的。

执行以下操作：

- 1. 在 Novell iManager 中，选择 **iPrint > Manage Printer**。
- 2. 浏览并选择要启用 Novell iPrint Direct 打印的 *printer*。
- 3. 选择 **Client Support > Novell iPrint Direct**。
- 4. 选择 **Enable iPrint Direct Printing** 选项。

## Manage Print Jobs

以下提供了 Novell iPrint 的打印作业管理功能信息：

- View Print Job Information
- Delete Print Jobs
- Change the Order of Print Jobs

被指定为打印机管理员或操作员的用户可以对路由到该打印机的所有作业执行这些任务；单个作业所有者只能对其自己的打印作业执行这些任务。

## View Print Job Information

您可以通过执行以下操作查看特定打印机等待处理的单个打印作业的信息：

- 1. 在 Novell iManager 中，选择 **iPrint > Manage Printer**。
- 2. 浏览并选择作业发送到的 *printer*。
- 3. 选择 **Printer Control > Jobs**。

打印作业信息将显示出来。

## Delete Print Jobs

管理员可以在作业尚未开始打印后提交时删除任何打印作业。用户只能删除自己的打印作业。

执行以下操作：

- 1. 在 Novell iManager 中，选择 **iPrint > Manage Printer**。
- 2. 浏览并选择作业发送到的 *printer*。
- 3. 选择 **Printer Control > Jobs**。
- 4. 选择要删除的作业旁边的 *check box*。
- 5. 选择 Delete。

## Change the Order of Print Jobs

有时，您可能需要将作业提前打印，排在已提交到打印机但尚未开始打印的其他作业之前。管理员、管理员和操作员可以移动任何作业在列表中的位置。用户只能移动自己的作业，并且只能将其向下移动。

执行以下操作：

- 1. 在 Novell iManager 中，选择 **iPrint > Manage Printer**。
- 2. 浏览并选择作业发送到的 *printer*。
- 3. 选择 **Printer Control > Jobs**。
- 4. 选择要修改的作业旁边的 check box。
- 5. 通过选择 **Promote** 将打印作业向上移动。

## Install the Novell iPrint Client

要使 Novell iPrint 正常工作，工作站必须安装 Novell iPrint 客户端。您可以通过多种方式将客户端分发到工作站，例如使用 Novell iPrint Printer List Web 页面、使用 ZENworks 等分发软件，或创建登录脚本。

要在 Linux 上安装 Novell iPrint 客户端，您需要了解以下内容：

- Novell iPrint Client Requirements
- Access Control to the Workstation Print System
- How to Install the Novell iPrint Client and Your First Printer on Linux

### Novell iPrint Client Requirements

要使 Novell iPrint 正常工作，Linux 工作站需要以下内容：

- SUSE Linux Enterprise Desktop 10, SuSE Open Linux 10.0 和 10.1（或更高版本）
- Konqueror 或基于 Mozilla 的浏览器，如 Epiphany、Firefox 或 Galeon

除这些要求外，您还需要了解以下内容：

- 要安装客户端，您必须拥有 root 密码或 root 权限。
- 如果在您安装打印机时 Novell iPrint 服务器繁忙，打印机尝试通信时，CUPS 会将打印机置于错误状态并保留所有打印作业。

要释放打印作业，请使用打印机管理实用程序重新启动打印机。

### Access Control to the Workstation Print System

Linux Novell iPrint 客户端打包为两种不同的专用安装，用于控制对工作站打印系统的访问。

表 12-2 解释了两种客户端之间的差异。

| Novell iPrint Client Filename | Description |
|---|---|
| `novell-iprint-client-sh-6.500.20070105-0.4.i586.rpm` | 安全高。打印系统访问受限。此客户端要求工作站用户使用 lppasswd 定义，以便在工作站上安装、删除或管理打印机。执行其中一项打印操作时，会要求用户输入密码。 |
| `novell-iprint-client-sl-6.500.20070105-0.4.i586.rpm` | 安全低。打印系统访问无限制。此客户端允许工作站的所有用户安装、删除或管理工作站上的打印机和打印作业，包括其他用户的打印机和打印作业。默认情况下，Novell iPrint Printer List Web 页面安装此 RPM。 |

**Table 12-2**

这些客户端不影响 Novell iPrint 客户端的安装或打印功能——仅影响对工作站打印系统的访问。要安装 Novell iPrint 客户端，您仍然需要 root 权限。

要从系统上传驱动程序，您需要使用 lppasswd 定义；否则，当您尝试从系统添加驱动程序时，驱动程序列表将为空。

要定义用户成为 lppasswd 的一部分，您可以使用以下命令：

```
lppasswd -a linux_user_account -g sys
```

### How to Install the Novell iPrint Client and Your First Printer on Linux

您可以使用以下方法之一在用户工作站上安装 Novell iPrint 客户端：

- Install the Client from the Novell iPrint Printer List Web Page
- Deliver the Client Using Distribution Software

#### Install the Client from the Novell iPrint Printer List Web Page

您可以从存储在 Print Manager 加载的服务器上的 Novell iPrint Printer List Web 页面下载并安装 Novell iPrint 客户端。

默认情况下，链接设置为安装低安全性的 novell-iprint-xclient-sl-6.500.20070105-0.4.i586.rpm 客户端。

您可以通过在 /var/opt/novell/htdocs 中创建符号链接来更改此设置，使用以下命令：

```
ln -sF client novell-iprint-client.rpm
```

其中 client 是表 12-2 中列出的客户端文件名。

要安装 Novell iPrint 客户端（以及您的第一台打印机），请执行以下操作：

- 1. 在 Linux 桌面的 Web 浏览器中，输入以下 Novell iPrint 服务器 URL：

```
http://server_IP_address_or_dns_name/ipp
```

例如，如果 Novell iPrint 服务器安装的 DNS 名称为 da3.digital-airlines.com，您将输入以下内容：

```
http://da3.digitalairlines.com/ipp
```

会出现类似图 12-31 的页面。

![](img/9129877170834ca9d5fdac5319bf5f12_464_0.png)

# Figure 12-31

- 2. 选择要安装的打印机。
  
  如果 Novell iPrint 客户端尚未安装在您的工作站上，您将被提示安装它。

- 3. 在提示时，将 Novell iPrint 客户端 RPM 保存到桌面或主目录。

- 4. 通过双击 RPM 安装 Novell iPrint 客户端 RPM。
  
  如果 RPM 不存在文件关联，请使用 RPM 安装程序。

- 5. 在安装第一台打印机之前，退出并重新启动 Web 浏览器。

![](img/9129877170834ca9d5fdac5319bf5f12_464_1.png)

> > 如果您使用的是 Konqueror 浏览器，您必须通过选择 **Settings > Configure Konqueror > Plug-Ins > Scan for New Plug-ins** 重新扫描插件。然后您可以重新启动 Konqueror 浏览器以安装打印机。

如果您使用的是非标准浏览器安装且插件未出现，请使用以下命令在浏览器的插件目录中创建符号链接：

```
ln -s /opt/novell/iprint/plugin/npnipp.so
```

- 6. 输入 Novell iPrint 服务器 *URL*。

- 7. 从 Novell iPrint 服务器页面，选择要安装的 *printer*。
  
  在打印机安装期间，Novell iPrint 会下载并安装与打印机关联的打印机驱动程序（如果有），并在用户工作站上安装打印机。
  
  第一次安装打印机时，打印机驱动程序会被强制推送到工作站，即使工作站包含更新的驱动程序。
  
  打印管理器会使用关联的 Driver Store 中的更新打印机驱动程序刷新其保存的打印机驱动程序副本。

![](img/9129877170834ca9d5fdac5319bf5f12_464_2.png)

