
方括号 `[]` 指定了修改搜索执行方式的准则。此示例首先测试 `dns` 源。如果 `dns` 有答案，则不再继续搜索。如果 `dns` 未提供答案，则检查 `nis`。当 `nis` 返回 `NOTFOUND`（表示它没有找到答案）时，进程停止（`NOTFOUND=return`），且不返回答案。只有当 `nis` 不返回答案也不返回 `NOTFOUND` 时，才会咨询本地文件（`/etc/hosts`）。换句话说，NIS 提供的是权威答案；当 NIS 不可用时，系统咨询本地文件。更多信息请参阅 `nsswitch.conf` 页、`NIS-HOWTO` 和 `DNS-HOWTO`。

## Internet 配置向导

![](img/aa8214d49e1cf50152c432845129fb3b_1072_0.png)

点击 Internet 配置向导，会打开“添加新设备类型”窗口（图 17-10）。添加新设备类型可以设置七种连接：

34. 尽管此选项的名称如此，但没有任何连接必须是 Internet，尽管它们通常是。

## 第17章 红 Hat Linux 系统管理

添加新设备类型

![](img/aa8214d49e1cf50152c432845129fb3b_1073_0.png)

图 17-10 添加新设备类型窗口：以太网（第 355 页），ISDN（第 355 页）...（注：原文此处存在大量重复页码描述，已按要求翻译并保持格式）。

# 配置网络服务

不要点击任何“设置默认”（Set Default）按钮。在点击窗口顶部的按钮之前，请确保在窗口中完成更改后点击“提交”（Commit）；否则 `swat` 将不会保留你的更改。

首先，点击 Samba/`swat` 主页顶部的 `GLOBALS`（图 17-11）。除了表 17-16 所示外，将所有内容保持为默认设置。

## Samba GLOBALS 的更改 || 表 17-16

| 基础选项 | |
|---|---|
| `workgroup` | 更改为你在 MS Windows 系统上的工作组名称。 |
| Security Options（安全选项）| | `hosts allow` | 输入 MS Windows 机器的主名或 IP 地址。 |

完成 `GLOBALS` 窗口的操作后，点击“提交更改”（Commit Changes）。
共享（或窗口共享）是指你通过 Samba 与另一个系统共享的目录及其子目录。接下来，点击 `SHARES` 按钮。将出现三个按钮和两个文本框。在位于“创建共享”（Create Share）按钮旁边的框中，输入你想要分配给此共享的名称。该名称可以是任何你想要的字符；它并不指定你正在共享的目录。点击“创建共享”（Create Share）。当你想要修改现有共享时，在组合框中调出共享名称，并点击“共享”（Share）。这两个操作中的任何都会显示完整的共享参数（Share Parameters）窗口。除了表 17-17 所示外，将所有内容保持为默认设置。

## Samba Shares 的更改 || 表 17-17

| 基础选项 | |
|---|---|
| `comment`（注释） | 关于此共享的用途及其在 GNU/Linux 系统上位置的可选注释可能会帮助。 |
| `path`（路径） | 将此更改为 GNU/Linux 系统上共享（目录）的绝对路径。 |
| Security Options（安全选项）| | `hosts allow` | 填写 MS Windows 系统的主名或 IP 地址。 |

完成 `SHARES` 窗口的操作后，点击“提交更改”（Commit Changes）。如果你想查看到底有多少选项，点击“高级视图”（Advanced View）。

当一切设置正确后，你应该能够在 Windows 机器上打开资源管理器窗口，点击菜单栏上的“工具”（Tools），并选择“映射网络”（Map Network），这将打开“映射网络驱动器”。从驱动器组合框中选择一个未使用的驱动器字母，并输入你创建的共享路径（MS Windows）。当你想要共享名为 `bravo` 的机器上的 `/home/jenny`，并将共享命名为 `bookkeeping`（在 `swat` 中）时，在文件夹框中输入 `swat\bravo\bookkeeping` 并点击“完成”（Finish）。假设你选择了驱动器字母 J，你应该能够在 MS Windows 机器上通过 J (`bookkeeping`) 访问位于 `bravo` 上的 `/home/jenny` 目录。

除了本地文档，`local.swat/Samba` 主页（图 17-11）还提供了大量帮助。此外还有“诊断工具”（Diagnostic Utilities）部分，其中列出了实用的实用：`smstatus` 显示 Samba 连接的报告，`testcharm` 检查 `/etc/samba/smb.conf` 文件并显示其内容（仅检查初始正确性，不检查服务可用性或正确/预期操作），`testprn` 检查打印机名称的有效性。当你点击 Samba 单词时，`swat` 会显示 Samba 手页，该页定义了每个 Samba 程序。

# DHCP 客户端

DHCP（动态主机配置协议）为局域网上的计算机动态分配 IP 地址。DHCP 服务器的管理员提供一个 IP 地址池，局域网上的每个客户端计算机都配置了 TCP/IP 软件，以向 DHCP 服务器请求 IP 地址。

当你没有被分配特定的 IP 地址时，提供商会在你每次与其建立连接时使用 DHCP 为你的机器分配一个临时 IP 地址。只要你的机器连接到提供商，地址就会保持不变，但每次连接时地址可能会不同。

客户端进程 `dhcpcd` 与服务器进程 `dhcpd` 通信，以获取它应该使用的 IP 地址、网络、广播地址等。DHCP 是基于广播的，因此客户端和服务器必须位于同一子网（第 1495 页）。要将 DHCP 作为客户端，使用 `redhat-config-services`：配置第 946 页的配置服务 II 或 `chconfig`：配置第 947 页的配置服务 III 来启动 `dhcpcd` 进程。更多信息请参考第 363 页的“静态与动态 IP 地址”。在 IPv4 下，自动配置是可选的并由 DHCP 提供。在 IPv6 下，自动配置是强制的，这使得主机轻松自动配置其 IP 地址（第 39 页）。

# OpenSSH：提供安全网络工具

| 基于字符 | `ssh` |
| --- | --- |
| 主页 | www.openssh.com |
| 帮助 | www.openssh.com/portable.html |
| 安全 | securityfocus.com (邮件列表) |
| 新闻组 | news.security.com |

OpenSSH 是 SSH 协议的免费版本，是许多安全网络工具的基础。`telnet` 和 `login` 以明文形式发送所有通信内容，而 OpenSSH 在加密所有通过网络内容的同时执行相同的功能。它的加密消灭了窃听、连接劫持和其他攻击。OpenSSH 还提供了隧道能力（第 __ 页）。

# 重构 Linux 内核 1031

GnuPG 系统的主程序是 `gpg`，是一种加密工具，能够实现安全的网络通信并保护存储期间的数据完整性和隐私。该系统可以加密和解密数据、创建和验证签名，以及管理密钥。有关安全、密钥和 GnuPG 的更多信息，请参阅附录 C（第 1410 页）。

使用 `gpg` 并不困难。以下命令加密了一条消息以便 Alex 可以读取：

```
$ gpg -ear alex@tcorp.com < infile > outfile
```
