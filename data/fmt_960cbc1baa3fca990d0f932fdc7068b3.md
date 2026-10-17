
2. 点击“新建”。出现“添加新打印队列”窗口。

3. 点击“向前”。出现“队列名称”窗口。

4. 输入打印机的简名和描述，并点击“向前”。

5. 点击“选择队列类型”框并选择以下之一：
   - 网络 CUPS (IPP)
   - 网络 UNIX (LPD)
   - 网络 Windows (SMB)
   - 网络 Novell (NCP)
   - 网络 JetDirect

6. 点击“向前”。

根据适用情况继续执行后续章节中的步骤。

## 添加远程 CUPS 打印机

如果您选择从打印配置窗口中添加 CUPS 打印机，你必须在出现的窗口中添加以下信息：

- **服务器 (Server)**：连接到打印机（或通过其他方式访问）的计算机主机名。这可以是计算机的 IP 地址或 TCP/IP 主机名（TCP/IP 名称可以通过您的 `/etc/hosts` 文件或 DNS 服务器访问）。
- **路径 (Path)**——远程 CUPS 打印机服务器上的打印机名称。CUPS 支持打印机实例，每个打印机可以有多组选项。如果远程 CUPS 打印机是这样配置的，您可以选择打印机的特定路径，例如 `/hp/300dpi` 或 `/hp/120dpi`。斜杠分隔打印队列名称和打印机实例。

按照处理本地打印机的方式完成剩余步骤（参见本章前面的“在 Red Hat 中添加本地打印机”部分）。

## 添加远程 UNIX 打印机

如果您选择从打印配置窗口中添加 UNIX 打印机，你必须在出现的窗口中添加以下信息：

- **服务器 (Server)**：连接到打印机（或通过其他方式访问）的计算机主机名。这是计算机的 IP 地址或 TCP/IP 名称（TCP/IP 名称可以通过您的 `/etc/hosts` 文件或 DNS 服务器访问）。
- **队列 (Queue)**——远程 UNIX 打印机服务器上的打印机名称。

按照处理本地打印机的方式完成剩余步骤（参见本章前面的“在 Red Hat 中添加本地打印机”部分）。如果发送到打印机的作业被拒绝，可能是远程服务器未允许访问。输入 `lpq -P` 查看状态。

## 添加 Windows (SMB) 打印机

启用您的计算机添加 SMB 打印机涉及在打印配置中添加条目。当您选择添加 Windows 打印机时，将显示网络上检测到的计算机列表。在此处，您可以配置：

1. 从列表中选择服务器。
2. 点击“确定”。
3. 在提示时，填写用户名和密码。

或者，您可以标识未列表中服务器。点击“指定”按钮并输入以下信息：

- **工作组 (Workgroup)**：分配给 SMB 服务器的工作组名。并非所有情况都需要填写工作组名。
- **服务器 (Server)**：计算机的 NetBIOS 名称或 IP 地址，可能与其 TCP/IP 名称相同。为了将此名称转换为访问主机所需的地址，Samba 会检查多个位置直到找到匹配项：本地 `/etc/hosts` 文件、本地 `/etc/hosts`、网络上的 WINS 服务器以及每个本地网络的广播响应。
- **共享 (Share)**：打印机与远程计算机共享的名称。它可能与打印机本地用户的名称不同。
- **用户 (User)**：SMB 系统需要用户名根据共享级或用户级访问控制为您提供 SMB 打印机访问。如果您使用共享级访问进行验证，则不需要用户名。
- **密码 (Password)**：取决于使用的访问控制类型，与 SMB 服务器或共享资源相关的密码。

当为 SMB 输入用户和密码时，信息将未加密存储在 `/etc/cups/printers.conf` 文件中。确保该文件对 root 可读。

按照处理本地打印机的方式完成剩余步骤（参见本章“在 Red Hat 中添加本地打印机”部分）。

结果是在 `/etc/cups/cupsd.conf` 和 `printers.conf` 文件产生新条目。此 `/etc/cups/printers.conf` 条目显示了刚创建的打印机条目：

```
<Printer NS1-PS>
Info Created by redhat-config-printer 0.6.x
DeviceURI smb://jjones:my9password@FREET/NS1/hp
Location HP on ns
State Idle
Accepting Yes
JobNames none none
QuotaPeriod 0
PageLimit 0
Klimit 0
</Printer>
```

# 704 第五部分 运行服务器

`DeviceURI` 行包含了关键信息。它标识了位置（一个 sm 对象）、用户名（`jjones`）、用户密码（`my9passwd`）、工作组（`FSTREET`）、服务器（`NS1`）和打印机队列（`hp`）。

`cupsd.conf` 文件的内容定义了允许可以使用此打印机的用户。

```
<Location /printers/NS1-PS>
Order Deny,Allow
Deny From All
Allow From 127.0.0.1
AuthType None
</Location>
```

根据这些示例信息，只有来自本地主机（`127.0.0.1`）的用户允许使用打印机，并且他们在使用时不需要身份验证。

如果一切配置正确，可以使用标准的 `lpr` 命令将文件打印到打印机。使用此示例，请采用以下格式进行打印：

```
$ cat file.ps | lpr -P NS1-PS
```

> 如果你收到失败信息，请确保打印目标计算机是可以访问的。对于 `NS1-PS`示例，你必须执行 `smclient -L NS1 -U jjones`。然后输入密码（在此例中为 `my9passwd`）。如果你输入密码后获得正确的查询响应，你应该看到该服务器的共享打印机和文件列表。检查名称并再次尝试打印。

# 添加 NetWeaver 打印机

要通过连接到（或由）NetWeaver 文件打印服务器管理的打印机设置你的 Linux 系统，你必须收集有关服务器、用户和密码的信息。

在打印机配置窗口（之前描述过的）中选择添加 Novell 打印机（Novell 创建了 NetWeaver），然后填写以下内容：

- **服务器** — 打印机连接（或可访问）的计算机名称。这是该计算机的 NetWeaver 服务器。
- **队列** — NetWeaver 服务器上打印队列的名称。
- **用户** — NetWeaver 系统启用访问 NetWeaver 打印机所需的用户名。
- **密码** — 与用户名关联的密码。

按照处理本地打印机的方法完成剩余步骤（请参见本章前面的“在 Red Hat 中添加本地打印机”部分）。

# 使用 CUPS 打印

CUPS Web 端管理工具和 Red Hat 的打印机配置窗口等工具有效地隐藏了底层的 CUPS 功能。有时，你可能希望直接使用与 CUPS 一带的工具和配置文件。接下来的章节描述了如何使用某些特殊的 CUPS 特性。

## 配置 CUPS 服务器 (cupsd.conf)

`cupsd` 守护进程监听对你的 CUPS 打印机的请求，并根据 `/etc/cups/cupsd.conf` 文件中的设置响应这些请求。`cupsd.conf` 文件中的配置变量与 Apache 配置文件 (`httpd.conf`) 中的格式相同。

Red Hat 的打印机配置窗口向 `cupsd.conf` 文件添加访问信息。对于其他 Linux 系统，你可能需要手动配置 `cupsd.conf` 文件。你可以逐步修改 `cupsd.conf` 文件来进一步调整你的服务器。让我们来看 `cupsd.conf` 文件中的一些设置。

默认没有设置分类。将分类设置为 `topsecret`（绝密），你可以在所有通过打印服务器的页面上显示 `Top Secret`：

`+ Classification topsecret`

你可以替换 `topsecret` 的其他分类包括 `classified`（已分类）、`confidential`（机密）、`secret`（秘密）和 `unclassified`（未分类）。

`ServerCertificate` 和 `ServerKey` 行（默认被注释）可以设置以指示证书和密钥的存储位置：

```
ServerCertificate /etc/cups/ss1/server.crt
ServerKey /etc/cups/ss1/server.key
```

如果你想进行加密连接，请激活这两行。然后将你的证书和密钥添加到指定的文件中。

浏览（Browsing）是在本地网络上广播你的打印机信息并监听其他打印机信息的功能。默认浏览针对本地 (@LOCAL)。你可以为额外的选定地址允许 CUPS 浏览器信息 (BrowseAllow)。浏览信息是广泛的，默认在地址 255.255.255.255。以下是这些默认值在 cupsd.conf 文件中的显示：

```
+ Browsing On
BrowseProtocols cups
BrowseOrder Deny,Allow
BrowseAllow from @LOCAL
BrowseAddress 255.255.255.255
Listen *:631
```
