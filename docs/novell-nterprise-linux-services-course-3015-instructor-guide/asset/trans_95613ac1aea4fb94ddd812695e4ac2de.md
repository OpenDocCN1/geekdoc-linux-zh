
## 查找 iPrint 文件

在默认安装过程中，将创建以下 iPrint 目录和文件：

1.  `/var/opt/novell/http/htdocs/ippdocs`
2.  `/var/opt/novell/iprint`
3.  `/var/opt/novell/log/ipsmd.log`
4.  `/etc/opt/novell/iprint/ipsmd.conf`

`/var/opt/novell/http/htdocs/ippdocs` 目录包含诸如可用打印机驱动列表（`iprint.ini`）和打印机映射等项。

`ipsmd.log` 和 `ipsmd.conf` 文件是 iPrint 守护进程（`ipsmd`）的日志文件和配置文件。

## 在 Windows 工作站上安装 iPrint 客户端

要在 Windows 工作站上安装 iPrint 客户端，请执行以下操作：

1.  在 Internet Explorer 中输入以下 URL：
    `http://server_ip_address/ipp`
2.  选择 **安装 iPrint 客户端**（**Install iPrint Client**）。
3.  按照步骤安装客户端。
4.  重启您的 Windows 工作站。

## 创建并启动驱动库

要创建并启动驱动库，请执行以下操作：

1.  打开 **iManager**：
    a.  在 iManager URL 中输入 `https://server_ip_address/nps/iManager.html`。此时将出现登录页面。
    b.  输入您的用户名和密码。
    c.  选择 **登录**（**Login**）。

    片刻之后，将出现 Novell iManager 主页。

2.  在左侧 **iPrint** 下，选择 **创建驱动库**（**Create Driver Store**）。
3.  输入驱动库名称。
4.  输入驱动库所在的容器，或浏览到该容器并选择它。
5.  在 **目标服务器**（**Target Server**）字段中，输入将托管该驱动库的服务器的 DNS 名称或 IP 地址。
6.  在 **eDir 服务器**（**eDir Server**）字段中，输入您的 eDir 服务器的上下文。
7.  确保已选中 **创建后启动驱动库**（**Start Driver Store after Creation**）。
8.  选择 **确定**（**OK**）。

## 向驱动库添加打印机驱动

**iPrint** 允许您通过 .inf 文件中的驱动程序或 Windows 工作站上当前的驱动程序，将驱动程序上传到您的驱动库。

要向驱动库添加驱动程序，请执行以下操作：

1.  在 **iManager** 的 **iPrint** 下，选择 **管理驱动库**（**Manage Driver Store**）。
2.  浏览到并选择您要添加打印驱动程序的驱动库。
3.  选择 **确定**（**OK**）。
4.  选择 **驱动程序**（**Drivers**）选项卡。
5.  选择您要处理的平台（**XP、2000、NT 4 或 95/98/Me**）的选项卡。
6.  执行以下操作之一：
    -  通过选择 **从文件添加**（**Add from File**）从打印驱动程序 .inf 文件添加驱动程序。
    -  或者，通过选择 **从系统添加**（**Add from System**）从正在运行 iManager 的 Windows 工作站客户端添加驱动程序。

![](img/d63035f3fce0eaaf97203dde900affb7_146_0.png)

> 如果您选择 **从系统添加**（**Add from System**），则只能上传与您正在使用的工作站属于同一平台的驱动程序。
>
> 例如，如果您使用的是 Windows 2000 计算机，则只能上传您 Windows 2000 计算机上的驱动程序。

7.  选择您要添加的打印机驱动程序。
8.  选择该驱动程序的打印机驱动程序语言（PDL）。
9.  选择 **确定**（**OK**）。
10. 重复步骤 7 至 9，直到添加完所有打印机驱动程序。
11. 选择 **确定**（**OK**）。

## 创建并启动 iPrint 管理器

要创建并启动 iPrint 管理器，请执行以下操作：

1.  在 iManager 的 iPrint 下，选择 **创建打印管理器**（**Create Print Manager**）。
2.  输入管理器名称。
3.  输入您希望 iPrint 管理器的对象驻留的 *容器*。
4.  在目标服务器字段中，输入将托管该 iPrint 管理器的服务器的 *DNS 名称* 或 *IP 地址*。
5.  在 eDir 服务器字段中，输入您的 eDirectory 服务器的 *上下文*。
6.  在驱动库字段中，浏览到并选择您的驱动库对象。
7.  确保已选中 **创建后启动打印管理器**（**Start print manager after creation**）。
8.  选择 **确定**（**OK**）。

## 创建打印机对象

要为打印机创建打印机对象，请执行以下操作：

1.  在 iManager 的 iPrint 下，选择 **创建打印机**（**Create Printer**）。
2.  输入您希望分配给新打印机的名称。

![](img/d63035f3fce0eaaf97203dde900affb7_147_0.png)

3.  在容器名称字段中，浏览到并选择您希望打印机驻留的 *容器*。
4.  在管理器名称字段中，浏览到并选择您希望分配给此打印机的 iPrint 管理器。
5.  在 DNS 名称或 IP 地址字段中，输入打印机的 *DNS 名称* 或 *IP 地址*。

安全打印使用 443 端口从客户端向服务器发送安全数据。

非安全打印使用 631 端口从客户端向服务器发送明文。

![](img/d63035f3fce0eaaf97203dde900affb7_148_0.png)

由于 iPrint 通过 LPR（行式打印机远程）将数据从服务器发送到打印机，因此服务器和打印机之间的所有打印数据均非安全。LPR 不处理身份验证或安全性，因此是明文。

6.  （可选）输入描述打印机位置的信息。
7.  （可选）输入打印机的描述。
8.  选择“下一步”（**Next**）。
9.  选择要为每个 Windows 平台安装的默认打印驱动程序。
10. 选择“下一步”（**Next**）。
11.  （可选）若要创建额外的打印机对象，请选择“重复任务”（**Repeat Task**）并重复上述所有步骤以创建打印机对象。
12. 选择“确定”（**OK**）。

## 配置工作站和/或用户打印机的网络

在配置工作站和/或用户打印机的网络之前，您需要了解它们各自的定义：

-   **工作站打印机**（**Workstation Printer**）。这是在 Windows NT/2000/XP 机器上安装并可让登录到该 Windows 机器的任何人使用的打印机。只有具有管理员或高级用户权限的用户才能在 Windows NT/2000/XP 机器上创建工作站打印机。
-   **用户打印机**（**User Printer**）。这是在 Windows NT/2000/XP 机器上安装且仅对安装它的用户可用的打印机。网络中的任何用户都可以创建用户打印机。

要确定网络上创建了哪些类型的打印机，请执行以下操作：

1.  浏览到位于您的 Linux 服务器 `/var/opt/novell/http/htdocs/ippdocs` 文件夹中的 `iprint.ini` 文件。
2.  右键单击 `iprint.ini` 文件；然后选择“打开方式 > gedit”（**Open With > gedit**）。
3.  将 AllowUserPrinters 值配置为以下值之一：
    -   0（默认值）表示只有具有足够权限（管理员权限或高级用户权限）的用户才能将打印机安装到桌面。当打印机安装到桌面时，它将是一个工作站打印机。
    -   1 表示如果当前用户没有权限将其添加为工作站打印机，它将被添加为用户打印机。
    -   2 表示所有添加的打印机，无论用户权限如何，都将是用户打印机。
4.  完成后，选择“保存”（**Save**）。
5.  选择“退出”（**Exit**）。

![](img/d63035f3fce0eaaf97203dde900affb7_149_0.png)

Windows 9x 会忽略这些值，并且只创建工作站打印机。

## 创建基于位置打印的 Web 页面

基于位置的打印允许用户通过使用以下方法之一，根据位置选择打印机：

-   列表视图（**List View**）
-   地图（**Maps**）

### 列表视图

**iPrint 管理器** 在默认 iPrint 页面（`http://server_IP_address/ipp`）上创建您的打印机列表。

若要创建包含自定义列表的 Web 页面，您必须使用 HTML 编辑器并创建指向打印机 URL 的链接。

要查看打印机的 URL，请执行以下操作：

1.  在 **iManager** 的 **iPrint** 下，选择 **管理打印机**（**Manage Printer**）。
2.  在 **iPrint 打印机名称**（**iPrint Printer name**）字段中，浏览到并选择您要查看的打印机。
3.  选择 **确定**（**OK**）。
4.  选择 **客户端支持 > iPrint 支持**（**Client Support > iPrint Support**）。

打印机的 URL 显示在 **已接受的 IPP URL**（**Accepted IPP URL**）下。

### 地图

您可以创建带有打印机图标的地图，这些图标代表打印机在工作环境中的位置。这使用户能够轻松选择要使用的打印机，并下载该打印机的正确驱动程序。

Novell 创建了一个 iPrint 地图设计器工具，该工具利用拖放技术帮助您创建自己的基于位置的地图。

若要使用 iPrint 地图设计器创建和配置基于位置的地图，必须具备以下条件：

-   Internet Explorer 5.5 或更高版本
-   Windows 95/98/Me 或 Windows NT/2000/XP
-   工作站上已安装 iPrint 客户端
-   用于放置打印机的地图

