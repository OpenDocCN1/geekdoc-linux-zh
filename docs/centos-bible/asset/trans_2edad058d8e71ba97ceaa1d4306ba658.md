
## 设置打印机和打印

**提示** 如果收到失败消息，请确保你要打印到的计算机是可访问的。对于前面的示例，你可以输入 `smbclient -L NS1 -U jwilson`。输入密码（在本例中为 my9password）。如果在输入密码后收到积极的名字查询响应，你应该看到来自该服务器的共享打印机和文件列表。检查名称，然后再次尝试打印。

### 添加 JetDirect 打印机

JetDirect 打印机（AppSocket/HP JetDirect）是通过 JetDirect 设备直接连接到以太网网络的打印机。通常使用 9100 端口向 JetDirect 打印机打印，但其他接口可能使用 9101、9102 等端口。要从 CentOS 使用 JetDirect 打印机，请键入以下信息：

-   **主机** — 输入 JetDirect 打印机的名称。
-   **端口号** — 输入端口号（通常为 9100）以识别到 JetDirect 打印机的接口。

### 使用基于 Web 的 CUPS 管理

打印机配置窗口实际上隐藏了底层的 CUPS 功能。然而，有时你可能希望直接操作随 CUPS 提供的工具和配置文件。以下各节描述了如何使用这些特殊的 CUPS 功能。

> **注意** 明文配置文件是 CUPS 打印功能的基础。当不同的工具（如基于 Web 的 CUPS 接口和打印机配置窗口）操作相同的配置文件时，这些文件可能对另一个工具变得不可用。在可能的情况下，你应该使用系统配置打印机（打印机配置窗口）在 CentOS 中管理打印机。如果你开始使用 CUPS 接口，你会看到相关的警告。

尽管在 CentOS 中配置 CUPS 打印的首选方式是使用打印机配置窗口，但 CUPS 提供了自己的基于 Web 的管理工具。

如果 CUPS 已经在你的计算机上运行，你可以立即通过 Web 浏览器使用基于 Web 的 CUPS 管理。如果 CUPS 尚未运行，请参阅描述 cupsd 守护进程的下一节，以获取有关启动它的信息。

CUPS 监听 631 端口，以提供对基于 Web 的 CUPS 管理接口的访问。在本地计算机上，在 Web 浏览器的地址栏中键入以下内容：

```
http://localhost:631/admin
```

会出现类似于图 16-3 所示的屏幕。

默认情况下，基于 Web 的 CUPS 管理仅可从本地主机访问。若要来自其他计算机访问基于 Web 的 CUPS 管理，你必须更改 `/etc/cups/cupsd.conf` 文件中的 `/admin` 部分。正如该文件文本中建议的那样，你应该限制从 Web 对 CUPS 管理的访问。还要记住，密码是以明文传输的，因此网络嗅探者可能会看到你的密码。如果你希望在不安全的网络上进行 CUPS 管理，请考虑通过 SSH 隧道访问此服务。

### 图 16-3

CUPS 通过 631 端口启用基于 Web 的管理。

![](img/2f265415ceec72538dd3c78ffca75c10_701_0.png)

在下面的示例中，我告诉 CUPS 在其 LAN 接口上监听外部连接（在此示例中，eth0 的 IP 地址为 `10.0.0.20`）。我将 `BrowseAllow` 更改为 `ALL`。然后，我添加了 `Allow` 行，以允许来自 IP 地址 `10.0.0.5` 的主机访问服务器根目录（`/`）、`/admin` 和 `/admin/conf`，如下面的示例所示。

```
Listen 10.0.0.20
BrowseAllow ALL

<Location />
  Order allow,deny
  Allow @LOCAL
  Allow 10.0.0.5
</Location>

<Location /admin>
  Encryption Required
  Order allow,deny
  Allow localhost
  Allow 10.0.0.5
</Location>

<Location /admin/conf>
  AuthType Basic
  Require user @SYSTEM
  Order allow,deny
  Allow localhost
  Allow 10.0.0.5
</Location>
```

在地址为 10.0.0.5 的计算机上，我在 Web 浏览器中输入了与图 16-3 中显示的相同地址行（将 CUPS 服务器的名称或 IP 地址替换为本地主机）。当被提示时，我输入了 root 用户名和密码。

现在，在显示管理屏幕后，你可以按以下方式设置打印机：

1.  单击“添加打印机”按钮。将出现添加新打印机屏幕。
2.  输入打印机的名称、位置和描述，然后单击“继续”。
3.  选择打印机所连接的设备。打印机可以直接通过计算机上的并行、SCSI、串行或 USB 端口本地连接。或者，你可以为 CUPS 选择网络连接类型（例如 AppSocket/HP JetDirect）、互联网打印协议（HTTP 或 IPP）或 Windows 打印机（使用 SAMBA 或 SMB）。
4.  如果被提示进一步的信息，你可能需要进一步描述到打印机的连接。例如，你可能需要输入串行端口的波特率和奇偶校验，或者可能需要输入 IPP 或 Samba 打印机的网络地址（设备 URI）。
5.  选择打印机驱动程序的制造商。（如果未列出打印机的制造商，请选择 PostScript 打印机或 PCL 打印机。）对于你选择的制造商，你将能够选择特定的型号。如果该打印机有可用选项，将出现“设置打印机选项”屏幕。
6.  根据打印机驱动程序，你的打印机可能只有少量或大量可用选项。例如，你可以选择页面大小、手动进纸、打印质量和其他功能。在你选择好所需的设置后，选择“设置打印机选项”。
7.  如果打印机添加成功，你看到的下一页应显示指向该打印机描述的链接。单击该链接。从新的打印机页面，你可以打印测试页或修改打印机配置。

一旦你能够从 CUPS 打印，你可以返回到 CUPS 基于 Web 的管理页面，并进一步处理你的打印机。以下是一些示例：

-   **列出打印任务** — 单击“管理任务”以查看当前由配置到此服务器的任何打印机活动的打印任务。单击“显示已完成的任务”以查看已打印任务的信息。
-   **创建打印机类** — 单击“添加类”；然后为打印机类指定名称、位置和描述。然后，从服务器上的打印机列表中，选择哪些打印机将加入此类，并单击“添加类”。
-   **查看打印机** — 你可以单击“管理打印机”并查看你配置的打印机。对于显示的每个打印机，你可以单击“停止打印机”（停止打印机打印，但仍接受队列中的打印任务）、“拒绝任务”（暂时不接受任何打印任务）或“打印测试页”（打印一页）。这些以及其他你可以从打印机页面执行的操作显示在图 16-4 中。

### 图 16-4

从打印机页面暂时停止打印或打印测试页。

![](img/2f265415ceec72538dd3c78ffca75c10_703_0.png)

## 配置 CUPS 服务器 (cupsd.conf)

cupsd 守护进程监听发往你的 CUPS 打印服务器的请求，并根据 `/etc/cups/cupsd.conf` 文件中的设置响应这些请求。cupsd.conf 文件中的配置变量与 Apache 配置文件（httpd.conf）的形式相同。更改 cupsd.conf 后，请重新启动服务器以使更改生效。

打印机配置窗口向 cupsd.conf 文件添加访问信息。你可以逐步检查 cupsd.conf 文件以进一步调整你的 CUPS 服务器。以下是一些建议：

*分类* 绝密

默认情况下未设置分类。通过将分类*设置为绝密*，你可以让*绝密*显示在所有通过打印服务器的页面上。你可以替换*绝密*的其他分类包括*机密*、*秘密*、*保密*和*非密*。

```
ServerCertificate /etc/cups/ssl/server.crt
ServerKey /etc/cups/ssl/server.key
```

`ServerCertificate` 和 `ServerKey` 行（默认未设置）可以设置以分别指示证书和密钥的存储位置。如果你想进行加密连接，请激活这两行。然后根据你的证书和密钥添加到指定的文件中。请记住，这些密钥用于 CUPS Web 接口，不用于发送打印任务。

```
Browse On
BrowseProtocols cups
BrowseOrder Deny,Allow
BrowseAllow from @LOCAL
BrowseAddress 255.255.255.255
Listen *:631
```

**浏览**是在本地网络上广播有关打印机的信息并监听其他打印服务器信息的功能。**浏览**默认开启，但仅针对本地主机（**@LOCAL**）。你可以允许来自其他选定地址的传入 CUPS 浏览信息。默认情况下，浏览信息在地址 255.255.255.255 上广播。

为了启用基于 Web 的 CUPS 管理，*cupsd* 守护进程基于此条目 `Listen *:631` 在你的计算机的所有网络接口上监听 631 端口。

```
BrowseRelay source-address destination-address
```

通过开启 `BrowseRelay`（默认关闭），你可以允许 CUPS 浏览信息在两个或多个网络之间传递。*source-address* 和 *destination-address* 可以是单个 IP 地址，也可以代表网络编号。这是允许多个连接局域网上的用户发现并使用附近其他局域网上的打印机的好方法。

你可以允许或拒绝访问 CUPS 服务器的不同功能。CUPS 打印机（从打印机配置窗口创建）的访问定义可能如下所示：

```
<Location /printers/nsl-hpl>
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
AuthType None
</Location>
```

在此，仅允许本地主机（127.0.0.1）上的用户打印到 `nsl-hpl` 打印机。不需要密码（*AuthType None*）。若要与任何可以访问它的远程机器共享此打印机，你可以在 `</Location>` 行之前添加 `Allow From All`。

