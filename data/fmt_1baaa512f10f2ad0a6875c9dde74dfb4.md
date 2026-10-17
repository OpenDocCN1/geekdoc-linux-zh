
进入 `/path/to/xxx` 目录，找到 `xxx.json`。

在地址为 `10.0.0.5` 的计算机上，我在 Web 浏览器中输入了与图 17-4 相同的地址行（用 CUPS 服务器名称或 IP 地址替换 `localhost`）。在提示时，我输入了根名称和密码。

1. 现在，显示 Admin 界面，你可以按照以下步骤设置打印机：
2. 点击 `Add Printer`（添加打印机）按钮。出现 `New Printer`（新打印机）屏幕。
3. 为打印机输入 `Name`（名称）、`Location`（位置）和 `Description`（描述），并点击 `Continue`（继续）。
4. 选择打印机连接的设备。打印机可以直接本地连接到并行、SCSI、串口或 USB 端口。或者，你可以选择网络连接类型（`AppSocket/HP JetDirect`）、Internet 协议（`http` 或 `IPP`）或 Windows 打印机（使用 `SAMBA`）。
5. 如果提示更多信息，你可能需要进一步描述与打印机的连接。例如，你可能需要为串口连接输入基波特和校验，或者可能被要求提供 IP 或 Samba 打印机的网络地址（`Device URI`）。
6. 选择驱动程序的品牌（如果列表中没有你的打印机制造商，请为 PostScript 打印机选择 `PostScript` 或为 PCL 打印机选择 `HP`）。对于你选择的品牌，你将可以选择特定型号。如果该打印机有可用选项，将出现 `Set Printer Options`（设置打印机选项）屏幕。
7. 根据打印机驱动程序，你的打印机可能有几个或许多可用选项。例如，你可能可以选择页面大小、手动进纸、打印质量和其他功能。在你选定所需的设置后，选择 `Set Printer Options`。

# 第四部分：Fedora RHEL 网络和服务器设置

8. 如果打印机添加成功，你将看到的下一个页面将显示一个指向打印机描述的链接。点击该链接。你可以从打印机打印测试页面或修改打印机配置。

在从 CUPS 打印后，你可以返回 CUPS Web 管理页面并对打印机进行进一步操作。以下是几个示例：
- `List print jobs`（列出打印任务）：点击 `Manage Jobs`（管理任务）查看服务器配置的任何打印机当前活跃的打印任务。`Show Completed Jobs`（显示完成的任务）查看已打印的任务。
- `Create printer class`（创建打印机类）：点击 `Add`；识别打印机的名称、位置和描述。然后，从服务器配置的打印机列表中选择一个进入此类并点击 `Add`。
- `View printers`（查看打印机）：你可以点击 `Manage Printers` 查看你配置的打印机。点击打印机进行控制。你可以点击 `Pause Print`（暂停打印但仍接受打印任务）、`Reject Jobs`（不接受任何打印任务）或 `Test Page`（打印页面）。这些操作出现在 Printers 页面，如图 17-5 所示。

![](img/1ccbe2b8efb451392a781396103b1e4e_0.png)

图 17-5：从 Printers 页面临时停止或打印测试页面。

# 第 17 章：设置打印服务器 747

## 配置 CUPS 服务器 (`cupsd.conf`)

`cupsd` 守护进程监听 CUPS 打印服务器的请求，并根据 `/etc/cups/cupsd.conf` 文件中的设置做出响应。`cupsd.conf` 中的配置与 Apache 配置 (`httpd.conf`) 相同。更改 `cupsd.conf` 后，重启服务器使更改生效。`Printer Configuration` 窗口会将信息添加到 `cupsd.conf` 文件。你可以通过 `cupsd.conf` 进一步调整你的 CUPS 服务器。

## Classification

默认没有分类。通过分类 `secret`，你可以在所有打印页面上显示 `Secret`。其他分类可以替换 `secret`：`classified`、`confidential` 和 `unclassified`。

```
ServerCertificate /etc/cups/server.crt

ServerKey /etc/cups/server.key
```

`ServerCertificate` 和 `ServerKey` 行（默认关闭）可以设置证书和密钥存储的位置。如果你想使用加密连接，请激活这些行。注意这些用于 CUPS Web 界面，而不是用于发送打印任务。

```
Browsing On

BrowseProtocols cups

BrowseOrder Deny,Allow

BrowseAddress 255.255.255

Listen *:631
```

浏览功能是关于你的本地网络和其他服务器的打印机信息。默认开启，但仅用于本地主机 (`@LOCAL`)。你可以允许额外地址的传入浏览信息。默认在地址 `255.255.255` 上广播。为了启用基于 Web 的 CUPS 管理，`cupsd` 守护进程根据 `Listen *:631` 为所有网络接口监听端口 `631`。

## BrowseRelay `source-address-destination-address`

开启 `BrowseRelay`（默认关闭），你可以允许 CUPS 浏览信息在两个或多个网络之间传递。`source-address` 和 `destination-address` 可以是 IP 地址或网络编号。这是允许连接局域网的用户发现并使用其他局域网打印机的好方法。

# 第四部分：Fedora RHEL 网络和服务器设置 748

你可以允许或拒绝访问 CUPS 服务器的不同功能。从 `Printer Configuration` 窗口创建的 CUPS 打印机访问定义如下：

```
<Location /printers/nsl-hpl>

Order Deny,Allow

Deny From All

Allow 127.0.0.1

AuthType None

</Location>
```

在这里，仅允许主机 (`127.0.0.1`) 打印 `nsl-hpl` 打印机。任何访问它的远程机器不需要密码，你可以在 `</Location>` 行之前添加 `Allow From`。

如果你更改了 `cupsd` 文件中的任何设置，必须重载 CUPS 服务使更改生效。作为 root 用户，输入 `service reload`。（`reload` 在不重启守护进程的情况下读取新配置。）

## 配置 CUPS 打印机选项

当从 `Printer Configuration` 窗口创建新打印机时，打印机在 `/etc/cups/printers.conf` 中定义。以下是 `printers.conf` 中打印机定义的示例：

```
<Printer hp2100

Info HP LaserJet 2100M

Location HP LaserJet 2100M in hall closet

DeviceURI hp:/par/hp/LaserJet_2100_Series?device=/dev/port0

State Idle

Accepting Yes

Shared Yes

Jobsheets none none

QuotaPeriod 0

PageLimit 0

Limit 0

OpPolicy default

ErrorPolicy stop-printer

</printer>
```

这是一个作为本地系统默认打印机的本地打印机示例。有趣的信息与 `DeviceURI` 相关，它显示打印机连接到并行 `/dev/port0`。`State` 是 `Idle`（准备好接受打印任务），`Accepting` 是 `Yes`（打印机默认接受任务）。

`DeviceURI` 有几种识别打印机设备名称的方法，反映了打印机连接的位置。以下是 `printers.conf` 文件列出的示例：

```
DeviceURI parallel:/dev/lp1

DeviceURI serial:/dev/ttyUSB1?baud=38400+size=8+parity=none+flow=soft

DeviceURI scsi:/dev/scsi/scld0
```

# 第 17 章：设置打印服务器 749

```
DeviceURI socket://hostname:port

DeviceURI tftp://hostname/path

DeviceURI ftp://hostname/path

DeviceURI http://hostname[:port]/path

DeviceURI ipp://hostname/path

DeviceURI smb://hostname/printer
```
