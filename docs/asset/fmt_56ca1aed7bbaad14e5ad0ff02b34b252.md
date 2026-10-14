
由于 Novell iPrint 使用 CUPS 在将打印作业发送到 Print Manager 之前渲染打印作业，因此无法从服务器本身使用 CUPS 或 Novell iPrint 进行打印。

## Configure Novell iPrint

要设置和管理 Novell iPrint，您需要知道如何执行以下操作：

- Set Up and Configure the Driver Store
- Set Up and Configure the Print Manager
- Create a Print Manager
- Manage Print Jobs

## Set Up and Configure the Driver Store

Driver Store 是打印系统打印机驱动程序的存储库。当打印机的第一个用户安装该打印机时，Print Manager 会从 Driver Store 请求关联的打印机驱动程序，并将打印机驱动程序保存到磁盘以供将来使用。

定期，Print Managers 会使用其关联 Driver Store 中的更新打印机驱动程序刷新其保存的打印机驱动程序副本。

网络上只需要一个 Driver Store，但根据网络配置，您可以创建额外的 Driver Store。运行的 Driver Store 越少越好，因为您无需跟踪哪个 Driver Store 具有哪些打印机驱动程序。

要设置和配置 Driver Store，请执行以下操作：

- Create a Driver Store
- Add Printer Drivers
- Create a DNS Name for the Print Manager

### Create a Driver Store

您的打印系统只需要一个 Driver Store；但是，根据网络设置，您可以添加更多 Driver Store。您需要创建 Driver Store 才能创建 Print Manager。

创建 Driver Store 的一般步骤如下：

1. 从 Novell iManager（左侧）选择 **iPrint > Create Driver Store**。
2. 填写适当的字段。

   有关字段的说明，请选择 Help。
3. 填写完字段后，选择 **OK**。

创建 Driver Store 并在服务器上加载守护进程后，您就可以开始上传打印机驱动程序。

### Add Printer Drivers

打印机驱动程序或 PostScript Printer Description（PPD）文件是直接支持物理打印机、使其能够执行其功能的软件实体。

硬件厂商开发特定于每台打印机的打印机驱动程序和 PPD 文件。大多数打印机需要针对其交互的每个操作系统使用不同的打印机驱动程序。

您可以使用 Novell iManager 查看已上传到 Driver Store 的打印机驱动程序和 PPD 文件列表。您可以从软盘、CD 和工作站操作系统添加打印机驱动程序和 PPD 文件。

要向 Driver Store 添加资源，Driver Store 守护进程必须正在运行，并且必须安装 Novell iPrint 客户端。

要向 Driver Store 添加打印机资源，请执行以下操作：

1. 从 Novell iManager（左侧）选择 **iPrint > Manage Driver Store**；然后浏览并选择您想要的 *Driver Store*。
2. 选择 Drivers；然后选择您想要处理的 *client platform*。
3. 执行以下操作之一：

   - 通过选择 **Add from File** 从打印机驱动程序 .inf 文件或 PPD 文件添加打印机资源。
   - 从您运行 Novell iManager 的工作站中选择 System 下的 **Add** 来添加驱动程序。

     您工作站上安装的驱动程序将被提供用于上传到 Driver Store。
     您只能上传与工作站相同平台的驱动程序。
4. 选择您想要的驱动程序；然后选择 **OK**。
5. 通过选择 **OK** 保存您的更改。

![](img/9129877170834ca9d5fdac5319bf5f12_455_0.png)

您也可以使用 `iprntcmd` 命令从终端提示符安装驱动程序文件。

有关详细信息，请参阅 Novell OES iPrint Administration Guide for Linux 中第 37 页的“Using iprntcmd on Linux and Macintosh”。

您可以通过 `http://www.novell.com/documentation/oes` 或您 3086 Course DVD 2 上的 `OES_Docs` 目录访问该指南。

## 为 Print Manager 创建 DNS 名称

Print Manager 会根据 Print Manager 配置为每个打印机创建一个 URL。

当您创建 Print Manager 时，您可以为 Novell iPrint 服务指定 IP 地址或 DNS 名称。

您应始终使用 DNS 名称，因为使用 IP 地址会迫使用户在 IP 地址更改时删除并重新安装打印机。

## 设置和配置 Print Manager

Print Manager 提供了一个平台，供 Printer Agents 驻留在服务器上。Printer Agents 是实际打印机的表示。当打印作业提交到 Print Manager 时，打印作业会在打印机准备就绪时转发给打印机。

要设置和配置 Print Manager，请执行以下操作：

- 创建一个 Print Manager
- 启动 Print Manager

### 创建一个 Print Manager

您需要为打印系统创建至少一个 Print Manager；根据您的网络设置，您可以创建额外的 Print Manager（例如，跨 WAN 链路）。

Print Manager 必须正在运行才能创建打印机。

在创建 Print Manager 之前必须存在 Driver Store。

要创建 Print Manager，请执行以下操作：

1. 确保您已为 Print Manager 配置了 DNS 名称。
2. 从 Novell iManager（左侧）选择 **iPrint > Create Print Manager**。
3. 填写适当的字段。

   要查看字段的说明，请选择 Help。
4. 确保选中了 **Start Print Manager after Creation** 复选框。

   如果您未选择此选项，您必须使用 Novell iManager 中的 **Manage Print Manager > Manager Control** 启动 Print Manager，或在 shell 提示符下输入 `/etc/init.d/novell-ipsmd start`。
5. 完成后，选择 **OK**。

在 Driver Store 创建并在服务器上加载守护进程后，您就可以开始添加打印机驱动程序。

## 启动 Print Manager

从 Novell iManager 的 Print Manager Control 属性页，您可以查看 Print Manager 的状态并卸载或加载 Print Manager 守护进程。

您执行以下操作：

1. 从 Novell iManager 选择 **iPrint > Manage Print Manager**。
2. 浏览并选择您想要管理的 Print Manager。

   请参阅图 12-27 所示内容。

![](img/9129877170834ca9d5fdac5319bf5f12_456_0.png)

**Figure 12-27**
3. 通过选择 **Manager Control > Startup** 启动 Print Manager。（要停止 Print Manager，请选择 **Manager Control > Shutdown**。）
4. 选择 **OK**。

## 创建打印机

在创建了 Print Manager 后，您可以通过执行以下操作创建打印机：

1. 从 Novell iManager（左侧）选择 **iPrint > Create Printer**。
2. 按照提示填写字段。

   您可以通过选择 Help 查看字段的说明。
3. 完成后，选择 Next；然后选择此打印机的驱动程序。

![](img/9129877170834ca9d5fdac5319bf5f12_457_0.png)

如果此打印机的打印机驱动程序未列出，您仍然可以创建打印机。

在打印机创建后，将打印机驱动程序添加到 Driver Store，然后通过选择 **Manage Printer > Drivers** 将驱动程序关联到打印机。
4. 完成后，通过选择 Next 创建打印机。

## 管理打印机
