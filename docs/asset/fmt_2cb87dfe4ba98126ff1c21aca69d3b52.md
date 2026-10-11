
您也可以从命令提示符启动 Samba。启动 Samba 的命令是 `/usr/sbin/samba` 或 `/etc/rc.d/samba`，取决于您的发行版。启动 Samba 后，可以在本地运行 `smclient` 来获取一些配置信息。发布命令 `smclient -L localhost` 密码请求时按回车。您应该看到类似于图 34-13 所示的输出。

![](img/8a8d528a12018c6ad3bd8ada99b3dc03_713_0.png)

**图 34-13:** 在本地运行 smclient 连接 Samba

在服务器上需要做的最后一件事是创建使用共享的用户。在我的家庭网络中（在本例中），我将其命名为 nancy；在命令提示符处创建一个名为 nancy 的用户。使用 `passwd` 命令为此账户分配密码。服务器上的所有内容现在已配置，但由于您尚未设置它们，还无法连接。

## Samba 客户端

配置 Samba 客户端，按以下步骤操作：

- 从 Windows 桌面点击“开始”（Start）。
- 选择“设置”（Settings），打开“控制面板”（Control Panel）。
- 双击“网络”（Network）。在网络对话框中，勾选“文件和打印共享”（File and Printer Sharing）和“Microsoft 网络”。见下图 34-14。

如果这两个项目未安装，您将需要安装它们。要安装 Microsoft 网络，按以下步骤操作：

- 点击“添加”（Add）按钮打开选择网络对话框。
- 点击“客户端”（Client），然后在选择类型框中点击“添加”。
- 接下来，点击“Microsoft”，然后在选择网络框中点击“Microsoft 网络”。
- 点击“确定”（OK）。

图 15 显示了整个过程。

![](img/8a8d528a12018c6ad3bd8ada99b3dc03_714_0.png)

图 34-14：配置页列出了已安装组件并允许您安装其他

![](img/8a8d528a12018c6ad3bd8ada99b3dc03_714_1.png)

图 34-15：安装 Microsoft 网络

接下来您需要安装 Microsoft 网络的文件打印共享。

- 点击“添加”（Add）按钮打开选择类型对话框。
- 点击“服务”（Service），然后在选择类型框中点击“添加”。
- 点击“Microsoft”，然后在选择网络框中点击“Microsoft 网络的文件打印共享”。
- 最后，点击“确定”并重启计算机。

计算机重启后，您将看到一个要求用户名密码的网络登录窗口。现在点击“取消”（Cancel），因为还有几个项目需要设置。

有些用户（如我）不喜欢在机器启动时有密码提示。将默认登录设置为“Windows”而不是“Microsoft 网络”并删除 `.PWL` 文件会让计算机保持网络活动状态，且不会提示密码。

桌面上应该有一个“网络邻域”（Network Neighborhood）图标。右键点击此图标从下拉列表中选择“属性”（Properties）。在网络属性窗口中点击“标识”（Identification）选项卡。在此窗口中，输入计算机名称和工作组名称，如图 34-16 所示。当您浏览网络时，会出现这些名称。计算机描述未网络浏览列表中。

![](img/8a8d528a12018c6ad3bd8ada99b3dc03_715_0.png)

**图 34-16:** 标识窗口输入计算机名称及其工作组的地方

点击“访问控制”（Access Control）选项卡和“共享访问控制”（Share Level Access Control）按钮（如图 34-17 所示），然后点击“确定”。

![](img/8a8d528a12018c6ad3bd8ada99b3dc03_716_0.png)

**图 34-17:** 在访问控制窗口中选择共享访问控制

点击“配置”（Configuration）选项卡，然后点击“文件共享”（File and Sharing）按钮。在文件共享窗口中勾选两个选项（如图 34-18 所示），然后点击“确定”。

![](img/8a8d528a12018c6ad3bd8ada99b3dc03_716_1.png)

**图 34-18:** 在文件共享窗口中选择两个选项

点击网卡的 TCP/IP 列表，然后点击“属性”（Properties）按钮。在 TCP/IP 属性窗口中点击“IP 地址”（IP Address）（如果尚未选中）。点击“指定 IP 地址”（Specify an IP address）按钮，然后为此计算机填写 IP 地址和子网掩码，如图 34-19 所示。

对于计算机较少的网络，手动分配 IP 地址效果良好。对于计算机大量的网络，最好使用动态主机配置协议（DHCP）自动分配 IP 地址。

接下来，点击“WINS 配置”（WINS Configuration）选项卡，然后选择“启用 WINS 解析”（Enable WINS Resolution）。将 Samba 服务器（Linux 计算机）的 IP 地址作为“主 WINS 服务器”（Primary WINS Server），如图 34-20 所示。完成后后点击“确定”。

![](img/8a8d528a12018c6ad3bd8ada99b3dc03_717_1.png)

图 34-20：为主 WINS 服务器输入 Linux 计算机的 IP 地址

### 第34 章 + 将 Linux 集成到异构网络 689

现在点击“绑定”（Bindings）选项卡，确保“微软网络客户端”（Client for Microsoft Networks）和“微软网络文件和打印机共享”（File and printer sharing for Microsoft Networks）存在并勾选，如图 34-21 所示。点击“确定”关闭窗口。

![](img/8a8d528a12018c6ad3bd8ada99b3dc03_718_0.png)

图 34-21：检查绑定选项卡以组件存在

在“配置”（Configuration）选项卡窗口列表中突出“微软网络文件和打印机共享”。点击“属性”（Properties）按钮，并确保“浏览主”（Browse Master）设置为“否”（No），“LM 宣告”（LM Announce）设置为“否”（No），如图 34-22 所示。完成后点击“确定”。

![](img/8a8d528a12018c6ad3bd8ada99b3dc03_718_1.png)

图 34-22：设置浏览主和 LM 宣告属性

点击“确定”关闭“网络属性”窗口。系统将提示你再次重启计算机，以便 Windows 将你进行的所有更改写入注册表。

计算机重启后，打开“我的电脑”，右键点击驱动器图标。弹出菜单现在将包含一个名为“共享”（Sharing）的项。点击此项将打开一个窗口，你可以在其中输入共享驱动器的名称和访问类型。见图 34-23。

图 34-23：为共享驱动器输入名称和访问类型

如果你在 Windows 上连接了打印机并希望从 Linux 上使用它，双击“我的电脑”中的“打印机”图标，并按照我之前描述磁盘共享的方式启用打印机共享。你需要再次重启 Windows 计算机并向 Linux 添加一些关于 Windows 打印机的配置信息。你可以在 Windows 重启时进行此操作。

## 在 Linux 上使用 Windows 打印机

由于所有发行版都包含打印机配置工具，因此使用该工具帮助配置打印机非常简单。红帽 Linux 包含了 `printtool`，这就是我用来配置打印机的工具。在命令行提示符处输入 `printtool`，在程序启动后点击“添加”（Add）。然后选择 SMB/Windows95.NT 打印机并点击“确定”，如图 34-24 所示。

### 第34 章 ♦ 将 Linux 集成到异构网络 691

![](img/8a8d528a12018c6ad3bd8ada99b3dc03_720_0.png)

图 34-24：使用红帽 printintool 配置 Samba 打印机

将出现一个对话框，警告你密码和 Samba。阅读完此窗口后，点击“确定”进入打印机输入框。配置连接到 Windows 上的打印机与连接到 Linux 上的打印机非常相似——只有少数例外。打印服务器的主机是 Windows 计算机的名称。在“服务器 IP 号”框中输入 Windows 计算机的 IP 地址，然后输入打印机名称。你可以留其他框为空，完成后点击“确定”。见图 34-25。

![](img/8a8d528a12018c6ad3bd8ada99b3dc03_720_1.png)

图 34-25：输入关于 Windows 打印机的配置信息

从 `printintool` 的打印机管理器页面，突出显示你刚刚创建的打印机项。点击“测试”（Tests）并打印前两个测试页，如图 34-26 所示。

## 第五部分 + 高级系统管理和网络管理

![](img/8a8d528a12018c6ad3bd8ada99b3dc03_721_0.png)
