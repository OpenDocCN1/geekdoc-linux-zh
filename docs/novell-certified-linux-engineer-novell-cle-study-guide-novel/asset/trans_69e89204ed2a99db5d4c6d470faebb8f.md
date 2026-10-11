

只要驱动程序就位，用户就可以提交打印任务。iPrint 客户端从 Windows 打印后台处理程序接收任务，并将其提交给 iPrint 管理器（3）。iPrint 管理器等待激光打印机变为可用，然后将任务发送给激光打印机的打印机代理（4）。随后，该任务会在打印机上打印出来。

让我们看看如何在你的 NNLS 服务器上安装和配置 iPrint。

## 安装和配置 iPrint

**涉及的测试目标：**

- 3. 安装和配置 iPrint。

与前一章中讨论的 NNLS 组件一样，CLE 目标要求你了解如何安装和配置 iPrint。就像这些其他产品一样，我们不会花太多时间讨论如何安装 iPrint 服务，因为第 5 章“NNLS 安装和管理”中已经详细介绍了 NNLS 的安装步骤和依赖关系。相反，我们将重点介绍在本章中安装 iPrint 客户端并配置 iPrint 服务。

### 安装 iPrint 服务

如果你执行的是 NNLS 快速安装，则 iPrint 已安装在你的系统上。如果你执行的是自定义安装，则你有机会选择安装 iPrint 组件。

如果在 NNLS 初始安装期间未选择 iPrint，你可以通过完成以下步骤执行安装后操作：

1. 挂载你的 NNLS ISO 映像。
2. 运行 `install.sh` 脚本。
3. 在提示时，指定自定义安装。
4. 在提示选择要安装的产品时，取消选中所有产品。
5. 选中 iPrint。
6. 按照第 5 章中的说明完成安装。

在安装过程中，iPrint 系统文件会被复制到服务器文件系统中的以下目录：

- `/var/opt/novell/iprint` — 此目录保存正在被 spooled（暂存）到 iPrint 管理器的打印任务。
- `/var/opt/novell/log` — 此目录包含 iPrint 系统日志文件（`ipsmd.log`）。

> 请注意，随 NNLS 安装的 Novell Apache Web 服务器在配置文件中启用了 **Access Logging**（访问日志记录）指令。如果你的 iPrint 系统使用非常频繁，理论上由 Web 服务器创建的日志可能会占满磁盘，从而导致系统停止运行。你应该定期删除旧的日志文件或在 conf 文件中禁用访问日志记录。

- `/var/opt/novell/httpd/htdocs/ippdocs` — 此目录包含你系统的打印机映射。
- `/etc/opt/novell/iprint/` — 此目录包含 iPrint 守护程序的配置文件（`ipsmd.conf`）。

### 安装 iPrint 客户端

如前所述，目前 Novell 只为 Windows 工作站提供 iPrint 客户端。有传闻称未来的版本中将提供适用于 Linux 的 iPrint 客户端。我们只能拭目以待看看是否真的会发生这种情况。

现在，让我们来谈谈如何在 Windows 工作站上安装 iPrint 客户端。与本书前面讨论的 iFolder 客户端一样，Novell 在 iPrint 网站上提供 iPrint 的客户端软件，该网站在你安装 NNLS 时默认安装在你的服务器上。

这使得你的管理员工作变得非常简单。你不再需要抱着一叠光盘在公司所有的 PC 间奔波，最终用户只需访问此网站即可下载所需的客户端软件。

这也让远程用户能够轻松访问所需的软件。回想一下本章开头引入的场景。很有可能，凌晨 2 点在家办公的员工手头并没有带有客户端软件的光盘。将客户端软件放在 iPrint 网站上，使得任何需要它的员工在需要时都能访问到它。

要安装 iPrint 客户端，你需要执行以下操作：

1. 在你的 Windows 工作站上，打开 Web 浏览器并导航到 **http://your_server_IP_address/ipp**。如果你没有安装 iPrint 客户端，将显示图 9.2 中的对话框。

![](img/c7771e8540507f2b00c088c7a411b57b_422_0.png)
![](img/c7771e8540507f2b00c088c7a411b57b_422_1.png)

2. 在提示安装 iPrint 客户端时，点击 **OK**（确定）。
3. 在 **File Download**（文件下载）对话框中，点击 **Open**（打开）。
4. 如果提示 Web 页面正在尝试关闭浏览器窗口，点击 **Yes**（是）。将出现 **Novell iPrint Client Setup**（Novell iPrint 客户端设置）屏幕，如图 9.3 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_422_2.png)
![](img/c7771e8540507f2b00c088c7a411b57b_422_3.png)

5. 点击 **Next**（下一步）。客户端文件如图 9.4 所示被复制。
6. 当文件复制完成后，将显示 **Install Complete**（安装完成）屏幕，如图 9.5 所示。点击 **Finish**（完成）。
7. 关闭并重启工作站。

现在让我们来谈谈如何配置你的 iPrint 实现。

**图 9.4**
iPrint 客户端文件复制。

![](img/c7771e8540507f2b00c088c7a411b57b_423_0.png)

**图 9.5**
iPrint 客户端安装完成。

![](img/c7771e8540507f2b00c088c7a411b57b_423_1.png)

## 配置 iPrint

为了配置你的 iPrint 系统，你需要完成一系列任务。包括以下内容：

- 配置驱动程序存储库
- 配置 iPrint 管理器
- 配置打印机代理
- 创建基于位置的打印映射

让我们看看第一个任务：配置你系统的驱动程序存储库。

### 配置 iPrint 驱动程序存储库

正如前面所述，iPrint 驱动程序存储库包含由你的 iPrint 管理器服务的打印机驱动程序。然而，驱动程序存储库不是在安装 iPrint 期间创建的。你必须使用 iManager 手动创建它。为此，请遵循以下步骤：

1. 打开 Web 浏览器并导航到 `https://your_server_IP_address/nps/iManager.html`。
2. 使用你的 **admin**（管理员）用户进行身份验证。
3. 在左侧框架中，向下滚动到 **iPrint** 角色，如图 9.6 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_424_0.png)

**图 9.6**
iManager 中的 iPrint 角色。

4. 选择 **Create Driver Store**（创建驱动程序存储库）。将出现图 9.7 中的屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_424_1.png)

**图 9.7**
创建驱动程序存储库。

5. 在 **Driver Store**（驱动程序存储库）名称字段中，输入你的驱动程序存储库对象在 eDirectory 树中的名称。
6. 在 **Container**（容器）名称字段中，输入你希望驱动程序存储库对象所在的容器。
7. 在 **Target Server**（目标服务器）字段中，输入你的 iPrint 服务器的 IP 地址。
8. 在 **eDir Server**（eDir 服务器）字段中，浏览并在 eDirectory 树中选择你的 NNLS 服务器的服务器对象。
9. 点击 OK（确定）。
10. 当提示驱动程序存储库对象已创建时，点击 OK（确定）。

完成此过程后，你将在 eDirectory 树中看到一个新的 *Driver Store*（驱动程序存储库）对象。在图 9.8 中，一个名为 CLEDriverStore 的 *Driver Store* 对象已在 IFCLE 容器中创建。

**图 9.8**
eDirectory 树中的驱动程序存储库对象。

![](img/c7771e8540507f2b00c088c7a411b57b_425_0.png)

创建驱动程序存储库对象后，你需要完成的下一个任务是将打印机驱动程序添加到驱动程序存储库中。默认情况下，NNLS 不提供任何打印机驱动程序，如图 9.9 所示。

**图 9.9**
驱动程序存储库中没有驱动程序。

![](img/c7771e8540507f2b00c088c7a411b57b_425_1.png)

在部署 iPrint 之前，你必须将打印机的适当驱动程序上传到驱动程序存储库对象中。使用 iManager，你可以通过两种方式上传驱动程序：

- 你可以从驱动程序软盘、CD-ROM 或从互联网下载的文件中上传驱动程序。
- 你可以直接从 Windows 操作系统的驱动程序集中上传驱动程序。

要上传驱动程序，你必须使用 Internet Explorer 访问 iManager。你不能使用 Mozilla 或 Netscape Navigator。你还必须从已安装 iPrint 客户端的工作站访问 iManager。满足这些条件后，你可以通过执行以下操作来上传驱动程序：

1. 从 Windows 工作站，打开 Internet Explorer 并导航到 `https://your_server_IP_address/nps/iManager.html`。
2. 在 iManager 中展开 **iPrint** 角色。
3. 选择 **Manage Driver Store**（管理驱动程序存储库）。将显示图 9.10 中的屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_426_0.png)

**图 9.10**
选择要管理的驱动程序存储库。

4. 在 **iPrint Driver Store name**（iPrint 驱动程序存储库名称）字段中，浏览并选择你的驱动程序存储库对象；然后点击 **OK**（确定）。将显示图 9.11 中的屏幕。

![](img/c7771e8540507f2b00c088c7a411b57b_426_1.png)

**图 9.11**
管理驱动程序存储库。

5. 选择 **Drivers**（驱动程序）选项卡。
6. 选择你要为其上传打印机驱动程序的操作系统。在图 9.12 中，显示了用于 Windows XP 驱动程序上传的屏幕。

