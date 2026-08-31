
# 教程：在 RDP Admin 2016 上安装 IIS Web 服务器

> 原文：<https://blog.eldernode.com/tutorial-install-iis-web-server-on-the-rdp-admin-2016/>

![Tutorial install IIS web server on the RDP admin 2016](img/ebe508ca384ef4b9d2617cd71b1275bd.png)

本教程将指导您如何在 RDP Admin 2016 Windows 服务器上安装 IIS Web 服务器。为了能够向他人展示您的网站，您肯定需要一个网络服务器。如果您正在使用 RDP 管理，`IIS` 是最好的解决方案。IIS 在 RDP 管理中的版本与之前的版本有很大不同，并且添加了许多新功能，包括安全功能。互联网信息服务（IIS）是微软提供的一项服务，通过启动这项服务，您可以在 Windows 服务器上托管您的文件或网站。在本文中，我们打算教您如何在 RDP Admin 2016 上安装 IIS Web 服务器。您可以通过访问 [Eldernode](https://eldernode.com/) 中的 [购买 RDP](https://eldernode.com/buy-rdp/) 管理页面查看和购买各种套餐。

在速度和性能方面，微软已经能够与强大的 Linux Web 服务器 Apache 竞争。随着 IIS 引入多个新特性和功能，微软向其 Web 服务器的发展迈出了一大步，我们将提到其中三个特性：

**1. 模块化结构：** 在以前版本的 IIS 中，要么所有组件必须一起安装，要么什么都不安装。但在新版本中，您只能选择和安装需要的模块，这可以显著提升系统负载和性能。

**2. 管理界面：** IIS 拥有与之前版本完全不同的管理界面，使得单独管理各个网站变得容易得多。您可以轻松配置任何网站，而无需更改其他网站。此外，在这个版本中，您可以通过一个配置文本文件一次编辑所有网站。

**3. 与网站所有者共享任务：** 如果您的服务器托管多个网站，您可以轻松使用服务器委托功能，为程序员或网站管理员划分任务。

## 在 RDP Admin 2016 上安装 IIS Web 服务器

首先，使用您的访问信息，通过**远程桌面**连接到您的服务器。通过远程桌面登录后，按照以下步骤在 RDP Admin 2016 上安装 IIS：

**1.** 从**开始菜单**，选择**管理工具**，然后点击**服务器管理器**。

![install iis web server in server manager](img/3104147c42730f0a9a32529d42d11fe5.png)

**2.** 在服务器管理器的**仪表板**部分，点击**添加角色和功能**。

![add roles and features in server manager](img/adb0a823f627069162ca861c049c5123.png)

**3.** 点击上述选项后，将打开以下页面。选择**下一步**选项。

![add roles and features wizard](img/a2a97dff61cc5b674e3f91edccb9ec93.png)

**4.** 在下一步中，不做任何更改，再次点击**下一步**。

![how to select installation type in server manager](img/652601154d04aa84d6937df8510e3323.png)

*（此处有一个分页符）*

![server selection in server manager](img/b36ee5127ff13ab0d1f01d40fa32e941.png)

**5.** 勾选 **Web 服务器（IIS）**，然后点击**下一步**。

![how to select Web Server (IIS)](img/559e48869a61a7a38cfcf5dd9f3d328f.png)

**6.** 将打开以下窗口，点击**添加功能**选项。

![add features in server manager](img/b6f8833f3553e7fbe5dfa51780d4ea87.png)

**7.** 显示此窗口后，这是此安装步骤中的最后一步，点击**安装**选项。

![confirm installation selections](img/017e0bc24adc732ea4a8f47f3afe0bb7.png)

**8.** 等待安装过程完成，然后点击**关闭**。

![install IIS web server on the RDP admin 2016](img/7d8baaa57a72bcbf27cfcf82f6f6391f.png)

恭喜！您已成功在 RDP Admin 2016 中安装了 IIS Web 服务器。

要使用此服务并托管您的文件，请通过**我的电脑**或**此电脑**访问 `C` 驱动器，然后依次进入 `inetpub` 文件夹和 `wwwroot` 文件夹，将您希望放置的文件放入该路径中。

![where is wwwroot folder](img/37d16696a3e4749aae6b14e75b5a15f7.png)

从现在开始，通过输入服务器的 IP 地址和文件名，您可以从服务器中下载所需文件。

**例如：** `http://my.server.ip/filename.mp3`

### 如何访问 IIS 部分并安装网站

在**服务器管理器**窗口中，进入**工具**菜单，然后点击**互联网信息服务**。您将看到类似于下图的界面：

![iis manager](img/0e5124e50386e90d2c25016d13ee4ad6.png)

**接下来，让我们进行网站安装：**

**1.** 从开始菜单，进入**管理工具**部分，点击**互联网信息服务（IIS）管理器**。

**2.** 当 IIS 管理控制台打开时，展开 **Web 服务器**部分。然后打开“站点”文件夹。右键点击**网站**文件夹，选择**添加网站**。

**3.** 在**添加网站**部分，有一系列用于静态网站的基本设置，我们逐一解释：

- **网站名称：** 您的网站名称或域名，例如 `https://eldernode.com`
- **物理路径：** 指定网站相关文件的物理路径。如果该路径尚未创建，您可以直接在同一控制台中创建它，并将网站相关文件放入其中。
- **类型：** 如果您的站点使用 SSL 安全系统，此部分应指定是否使用 HTTPS 协议。
- **IP 地址：** 从下拉列表中，指定网站所需的 IP 地址。如果不确定，请选择“所有未分配”作为默认选项。
- **域名：** 如果希望网站响应其他名称，可以在此指定。

完成设置后，您的 Web 服务器已准备就绪。您只需将网站相关文件放置在“物理路径”中指定的位置，并将首页文件命名为 `index.html`，即可通过分配的 IP 地址或域名访问网站。

## 结论

IIS 是一个 Web 服务提供程序，可作为服务器角色安装在 Windows Server 上。本文旨在教您如何在 RDP Admin 2016 上安装 IIS Web 服务器。
