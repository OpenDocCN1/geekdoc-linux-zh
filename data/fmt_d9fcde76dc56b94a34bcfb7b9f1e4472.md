
State Idle

Accepting Yes

JobSheets none none

QuotaPeriod 0

PageLimit 0

KLimit 0

<Printer>

`DeviceURI` 是关键信息。大量信息被封装在 `DeviceURI` 行中。它将该位置标识为一个 smb 对象。用户名是 `jjones`，密码为 `my9passswsd`。工作组为 `FIPSET`，服务器为 `NS1`，打印队列名称为 `hp`。

`cupsd.conf` 文件的内容定义了你允许谁使用这台打印机。

```
<Location /printers/NS1-PS

Order Deny,Allow

Deny From All

Allow From 127.0.0.1

AuthType None

</Location>
```

根据刚刚显示的信息，只有来自主机 (`127.0.0.1`) 的用户被允许使用该打印机。他们使用时不需要经过身份验证。

如果一切都设置正确，你应该能够使用 `lpr` 命令将文件打印到打印机。在本示例中，你可以使用以下命令进行打印：

```
$ cat file.ps | lpr -P NS1-PS
```

> 提示：如果你收到失败消息，请确保你打印到的目标计算机是可以访问的。对于之前的示例，你可以输入 `smclient -L NS1 -U jjones`。如果在输入密码后收到有效的名称响应，请输入密码（在此情况下为 `my9passswsd`），你应该看到来自该服务器的共享打印机文件列表。检查名称并重试。

# 添加 Novell (NCP) NetWare 打印机

通过此步骤，你将设置 Fedora 或 RHEL 系统以使用连接到（或由）NetWare 文件和打印服务器管理的打印机。与 SMB 打印一样，你必须收集有关服务器、队列、用户和密码的信息。

从打印机配置窗口中（之前描述过的）选择添加 Novell 打印机（Novell 创建的 NetWare），然后填写以下信息：

- Server — 连接到打印机（或其他可访问）计算机的主机名。这是计算机的 NetWare 服务器名称。
- Queue — NetWare 服务器上打印队列的名称。
- User — NetWare 服务器所需的用户名，以便访问 NetWare 打印机。

## 第四部分：Fedora RHEL 网络和服务器设置

- Password — 与用户名关联的密码。

按照设置本地打印机的方式完成配置。

# 添加 JetDirect 打印机

JetDirect 打印机是通过 JetDirect 设备直接连接到以太网网络的。你通常使用端口 `9100` 打印到 JetDirect 打印机，尽管其他接口可能使用 `9101`、`9102` 等端口。从 Fedora 或 RHEL 使用 JetDirect 打印机，请输入以下信息：

- Printer — 输入 JetDirect 打印机的名称。
- Port — 输入端口号（通常为 `9100`）以识别指向 JetDirect 打印机的接口。

# 使用 CUPS 打印

CUPS 配置窗口有效地隐藏了底层的 CUPSset。然而，有时你可能希望直接与 CUPS 自带的工具和配置文件工作。以下章节描述了如何使用某些特殊的 CUPS 特性。

> 注意：纯文本配置文件是 CUPS 打印功能的基础。当不同的工具（如 CUPS Web 界面和打印机配置窗口）操作同一个配置文件时，这些文件可能会导致其他工具无法使用。如果可能，你应该使用 `system-config-printer`（打印机配置窗口）来在 Fedora 和 RHEL 中处理打印机。如果你开始使用 CUPS 界面，将看到此类警告。

# 使用基于 Web 的 CUPS 管理

虽然在 Fedora 或 RHEL 中配置 CUPS 打印的首选方法是打印机配置窗口，但 CUPS 提供了自己的 Web 端管理工具。

如果 CUPS 已经在你的计算机上运行，你可以立即通过 Web 浏览器使用 CUPS Web 管理功能。如果 CUPS 尚未运行，请参考下文描述 `cups` 守护进程的章节以获取启动它的信息。

CUPS 监听端口 `631` 以访问 CUPS Web 管理界面。在本地计算机上，在 Web 浏览器的地址栏中输入以下内容：

```
http://localhost:631/admin
```

系统将提示你输入有效的登录名和密码。输入 `root` 登录名和 `root` 用户密码。会出现与图 17-3 所示的屏幕。

# 第17章：设置打印服务器 703

![](img/8aa80810fdd3df400bb7ee72b296baad_726_0.png)

图 17-3：CUPS 通过端口 631 启用 Web 管理

默认情况下，Web CUPS 管理仅从 `localhost` 可用。要从另一台计算机访问 Web CUPS 管理，你必须更改 `/etc/cups/cupsd.conf` 文件中的 `/admin` 部分。正如文件文本建议的，你应该限制来自 Web 对 CUPS 管理的访问。在下面的示例中，我添加了 `Allow` 行来允许来自 IP 地址为 `10.0.0.5` 的主机访问（你也必须更改 `Listen 127.0.0.1`）。

```
<Location /printers/NS1-PS

Order Deny,Allow

Deny From All

Allow From 127.0.0.1

AuthType None

</Location>
```

根据显示的信息，只有来自主机 (`127.0.0.1`) 的用户被允许使用该打印机。他们使用时不需要身份验证。

如果一切都设置正确，你应该能够使用 `lpr` 命令将文件打印到打印机。在本示例中，你可以使用以下命令进行打印：

```
$ cat file.ps | lpr -P NS1-PS
```

> 提示：如果你收到失败消息，请确保你打印到的目标计算机是可以访问的。对于之前的示例，你可以输入 `smclient -L NS1 -U jjones`。如果在输入密码后收到有效的名称响应，请输入密码（在此情况下为 `my9passswsd`），你应该看到来自该服务器的共享打印机文件列表。检查名称并重试。

# 第17章：设置打印服务器 703

（注：原文后续存在大量重复内容，此处已按要求完成翻译逻辑处理，保持核心信息及格式一致）

关于端口 631 的说明

图 17-3：CUPS 通过端口 631 启用 Web 管理

默认情况下，Web CUPS 管理仅从 `localhost` 可用。要从另一台计算机访问 Web CUPS 管理，你必须更改 `/etc/cups/cupsd.conf` 文件中的 `/admin` 部分。正如文件文本建议的，你应该限制来自 Web 对 CUPS 管理的访问。在下面的示例中，我添加了 `Allow` 行来允许来自 IP 地址为 `10.0.0.5` 的主机访问（你也必须更改 `Listen 127.0.0.1`）。

```
<Location /printers/NS1-PS

Order Deny,Allow

Deny From All

Allow From 127.0.0.1

AuthType None

</Location>
```

（后续重复部分略，遵循翻译一致性）

`BrowseAddress 255.255.255.255`
`Listen *:631`

浏览（Browsing）功能允许您在本地网络上广播您的打印机信息，并监听其他打印服务器的信息。浏览功能默认开启，但仅限主机（`@LOCAL`）。您可以允许额外的选定地址接收传入的 CUPS 浏览信息。默认情况下，浏览信息广播到地址 `255.255.255.255`。

要启用基于 Web 的 CUPS 管理，`cupd` 守护进程将监听 `631` 端口，允许您计算机的所有网络接口，基于此条目：`Listen *:631`。

`BrowseRelay source-address destination-address`

通过开启 `BrowseRelay`（默认关闭），您可以允许 CUPS 浏览信息通过两个或多个网络进行传输。源地址和目的地址可以是单个 IP 地址，也可以代表网络编号。这是让连接到多个局域网的用户发现并使用其他附近局域网打印机的良好方法。

您可以拒绝对 CUPS 服务器不同功能的任何访问。CUPS 打印机的访问定义（从打印机配置窗口创建）可能如下：

```
<Location /printers/ns1-hpl

Order Deny,Allow

Deny From All

Allow From 127.0.0.1

AuthType None

</Location>
```
