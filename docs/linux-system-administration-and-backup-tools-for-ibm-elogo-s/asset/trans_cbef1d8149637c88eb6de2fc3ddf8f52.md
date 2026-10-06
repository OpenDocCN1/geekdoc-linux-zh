

## 4.7.3 Yast2: NFS 配置

![](img/4e6a76e57a4105be55d8a1cc0750b023_120_0.png)

Yast2 允许你配置系统上 NFS 的工作方式。它可以作为服务器（允许你与其他机器之间共享文件），也可以作为客户端（从服务器请求共享内容）。你有机会使用 Yast2 NFS 模块配置这两种模式。

要创建挂载 NFS 共享的配置，选择 **Mount NFS directories**（挂载 NFS 目录）并点击 **Next**（下一步）。要从系统中删除所有 NFS 挂载，选择 **Remove all NFS mount from fstab**（从 fstab 移除所有 NFS 挂载）。

如果你选择了 **Mount NFS directories**，将看到图 113；否则将看到图 114。

第 4 章 SuSE Linux 基础系统管理 109

表格包含了所有将写入 /etc/fstab 的 NFS 条目。你可以向 Fstab 条目输入新项，并使用 Add 按钮将其添加到表格中。Choose 可以帮助你获取 NFS 服务器的名称。双击表格中的某行会将信息复制到 Fstab 字段，删除按钮可以删除 /etc/fstab 中选中的行。

/etc/fstab 中的 NFS 相关条目

| 服务器 远程文件系统 | 挂载点 | 选项 |
| :--- | :--- | :--- |
| netfinity | /mounts/work/justin | /home/justin/work | defaults |
| Fstab 条目 NFS 服务器主机名: | | |
| netfinity | | |
| 远程文件系统: 挂载点（本地）: | | |
| /mounts/work/justin | /home/justin/work | |
| 选项: | | |
| defaults | | |

![](img/4e6a76e57a4105be55d8121_0.png)

图 113 是允许你配置系统挂载 NFS 共享的窗口。

你必须在此窗口中输入所有相关信息并按 Add 启用共享。重复此过程，直到输入所有你想要使用的 NFS 共享。

条目如下：

- NFS 服务器主机名 - 这是你想要挂载目录的 NFS 服务器的 IP 地址或主机名。
- 远程文件系统 - 这是你请求的服务器上的远程目录。它必须是从根目录 (/) 开始的完全限定目录名。
- 挂载点（本地） - 这是你希望挂载远程目录下的本地目录。
- 选项 - 这允许你为挂载点设置某些选项。请查看 mount (8) 手页获取可用选项的详情。

110 IBM @server xSeries 和 Netfinity Linux 系统管理与备份

一旦你输入了所有想要使用的挂载点，按 Next 按钮继续。

![](img/4e6a76e57a4105be55d8a1cc0750b023_122_0.png)

图 114. Yast2: 启动 NFS 服务器

现在你有机会启动 NFS 服务器，以便你与网络上的其他计算机共享目录。如果你不想与其他机器共享任何目录，选择 Do not start NFS Server（不启动 NFS 服务器）并按 Next 继续。如果你想与其它计算机共享 NFS 挂载内容，选择 Start NFS server（启动 NFS 服务器），并按 Next 继续。

![](img/4e6a76e57a4105be55d8a1cc0750b023_123_0.png)

要将目录导出到其他机器，你必须告诉服务器你想共享的目录、谁允许访问该目录以及在什么限制下访问。图 15 显示了如何输入这些数据。

与上一个示例一样，你必须在继续配置之前输入共享的所有相关数据并按 **Add**。唯一的区别是有两个 Add 按钮。

在导出 NFS 共享时，允许你显式指定哪些主机允许访问共享目录。Vast2 允许你不断添加允许访问指定共享的主机（在左窗格中）。在对谁可以使用该共享实施限制之前，你首先允许所有人配置该共享。对此只有一个选项，即 **Directory**（目录）。directory 语句直接告诉 NFS 服务器你想共享的哪个目录。确保该目录存在；否则服务器将表现异常。

一旦你分配了一个目录进行共享，你就可以开始分配共享限制。

112 IBM @xSeries 和 Netfinity Linux 系统管理与备份

NFS 服务器允许使用通配符允许特定网络访问共享。在我们的案例中，我们通过指定 *.ibm.com 为允许的主机，启用了 IBM 网络访问这些共享。

options 部分告诉你限制如何应用于 NFS 客户端的挂载。这仅适用于每个限制，而不是访问 NFS 共享的每个客户端。例如，如果我们在限制表中添加 .suse.de，我们可以允许 IBM 的所有人对该共享具有写权限（选项 rw），但对 SuSE 的所有人对同一共享具有只读权限（选项 ro）。

其他可用选项请查看 mount(5)。

一旦你添加了所有想要导出的挂载点，点击 Next 继续。系统将要求你确认想要使用这些设置。点击 Next。

## 4.7.4 Yast2: 网络配置

![](img/4e6a76e57a4105be55d8a1cc0750b023_124_0.png)

第 4 章 SuSE Linux 基础系统管理 113

你可以通过选择 Off 来停止 inet 运行。你可以使用 default 启动 inet。或者你可以通过选择 On 自己配置 inet。

我们将引导你进行 inet 配置以添加或删除服务。

![](img/4e6a76e57a4105be55d8a1cc0750b023_125_0.png)

图 17. Yaast2: 服务配置

你有四个选项来添加新服务：

- **Create**（创建）允许你向服务器添加新服务。
- **Delete**（删除）将从系统中删除该服务。
- **Edit**（编辑）允许你编辑当前选中的项。
- **Activate/Deactivate**（激活/禁用）将停止该服务但不删除它。这与删除条目的效果相同。如果激活服务，则允许其运行。

114 IBM @server 和 Netfinity Linux 系统管理与备份

## 编辑服务条目

| 服务 | 协议 |
| :--- | :--- |
| [x] service is active | |
| pop3 | tcp |
| Type | Flags |
| stream | nowait |
| User | |
| root | |
| Comment | |

如果你点击图 17 中的 Add 或 Edit 按钮，将加载图 18。它允许你添加服务条目或编辑现有的条目。两种配置类型的选项完全相同：

- Service（服务） - 这是在 /etc/services 中定义的服务名称。该文件持有有关特定服务的信息，例如端口号、服务类型、服务名称等。你应该在此处输入已存在的服务名称（在 /etc/services 中定义）。
- Protocol（协议） - 定义了该服务使用的协议。最流行的协议类型是 TCP、UDP 和 ICMP。定义的协议必须存在于 /etc/protocols 中。
- Type（类型） - 定义将使用的连接类型。这可以是 stream（流类型）、dgram（数据报类型）、raw（原始套接字类型）、rdm（可靠传输消息类型）或 seqpacket（顺序数据包类型）之一。
- Flags（标志） - 此项有两个选项。对于使用 stream 服务器，通常选择 nowait。它允许服务在处理其他请求的同时接受新请求。该服务被称为“多线程”的。Wait 则用于一次只允许一个连接到...

要创建一个有效的条目（即 inetd 的服务），该条目将包含字段：

* service name
* socket type
* protocol
* wait[nowait|max]
* user[group]
* server program
* server arguments

要指定基于 Sun-RPC 的服务，该条目将包含：

之前的代码块：inetd.conf 中的注释

Pop et al

![](img/4e6a76e57a4105be55d8a1cc0750b023_126_0.png)

