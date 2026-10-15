
当提示时，Linux 用户需要 Windows 密码才能使用此服务。

使用 Samba 客户端服务访问 Windows 工作站时会出现 `smb: |>` 提示符。`smb: |>` 提示符是一个类似 FTP 的界面。Linux 用户可以使用 `put` 和 `get` 等命令与 Windows PC 交换文件。

初次尝试使用 `smbclient` 时，我们发现该程序 `smbclient` 并未使用默认的 Red Hat 6.0 程序安装。通过使用互联网，我们访问了名为 `RPMfind.net` 的网站。

我们进入了 `http://www.rpmfind.net/Linux/RPM` 网站，并在那里找到了由 W3C 组织托管的 rpm 文件存储库。他们拥有世界上最大的 RPM 存储库。W3C 为这些程序专门分配了大约一太字节的空间。

我们找到了 Samba 客户端的最新版本 `rpm`（Red Hat 软件包管理器）并进行了安装。然后我们使用 `Kpackage` 管理器，并通过右键单击链接，直接从 `Kfilemanager` 中的 `ftp` 站点安装程序。

管理员发现使用命令行实用程序既繁琐又耗时。一旦我们要求管理员从 Windows 共享向 Linux 服务器传输文件，他犯了几次打字错误，并发现他没有 `bash` 的灵活性。这给了我们展示 Linux 灵活性的机会。

我们要求管理员通过 `kvt` 终端窗口访问 Windows 共享。一旦他建立了连接，我们就要求他列出共享中的文件。然后我们要求他突出显示要传输的文件的文本。

令他惊讶的是，通过单击中间鼠标按钮（或同时单击两个鼠标按钮，模拟三键鼠标），文件显示在 Linux 服务器命令行上。通过在文本前键入 `get` 并按下 Enter 键，文件立即从 Windows 机器传输。管理员评论说，他们觉得这一过程将加快他们的管理任务，并为 Windows 工作站提供类似 ftp 的访问，而 Windows 工作站按设计默认没有 ftp 服务。

## Centennial 的进展

通过使用 Linux 和 Samba，技术部门可以提供一个集中的打印、文件和应用程序服务器，以便各个局域网之间能够相互通信。

除了 Samba，Linux 还实现了 Apple 计算机的网络协议 AppleTalk。Linux 服务器能够同时为 Centennial 的 Macintosh 计算机提供完整的网络服务，同时为 Microsoft 计算机提供服务。

## Internet 访问

项目计划中的下一个任务涉及为学校内部的私有网络提供 Internet 访问，同时防止 Internet 未经检查地访问学校。这需要防火墙和代理解决方案。

## 使用 IP 伪装

为了允许多台计算机通过防火墙服务器使用单一 Internet 连接，管理员需要在 Red Hat 6.0 中启用 IP 伪装。如果 Linux 主机在启用 IP 伪装的情况下连接到 Internet，则通常连接到同一局域网上的计算机也可以隐形地访问 Internet，即使它们没有正式分配的 IP 地址。

## 使用 IP 伪装的优势

Centennial 在一台 Pentium II 计算机上安装了 Red Hat 6.0，配置为 96 MB 内存和 6.5 GB 硬盘。该 Linux 主机连接到 Internet 并通过现有网络建立连接。只要服务器保持连接，其他运行 TCP/IP 的计算机就可以连接到本地网络上的 Linux 盒子以访问 Internet。

## Linux 2.2.x 内核

Centennial 技术部门尝试使用 `IPFWADM` 建立防火墙方案，该方案在之前的 Linux 内核上有效。使用 Red Hat 6.0 在线文档中有关 IP 伪装的文档，Centennial 管理员发现了如何实现其防火墙的方法。

他们还发现 `IPFWADM` 不再是用于操作 2.1.x 和 6.0.x 内核的 IP 伪装规则的防火墙工具。因此，他们使用 `IPCHAINS` 工具熟悉了 Red Hat 6.0 内核。

The administrators set reserved IP addresses (`192.168.x.x`) for each internal MASQed computer they wanted to provide with Internet access. The administrators now needed to point each internal client machine to the Linux server providing the Masquerading services, using this server as the default gateway.

The process simply involved the administrators entering the address of the Linux host as the machine's gateway address. The server's networking hardware included two Intel Pro 100 network interface cards. In setting up the network interface card, the administrators assigned an IP address to it. They obtained an IP address for the outside network interface card via DHCP (Dynamic Host Configuration Protocol) from their Internet service provider.

Client machines connected to the server required name resolution services in order to navigate the Web. By running either the `ROUTED` protocol (on smaller networks), or configuring DNS, the client machines could use the same DNS servers that the Linux server used.

## 分发生产力应用程序

As stated before, Centennial utilized the features and capabilities of the Apache Web server to distribute their productivity application. In addition, the District needed mail, file transfer capabilities, and multi-user access to applications.

### 电子邮件

Red Hat 6.0 includes the `sendmail` Mail Transfer Agent (MTA). `Sendmail` allows a Red Hat 6.0 system to complete mail services such as the following:

- `SMTP`—Simple Mail Transport Protocol. This service allows users to send email over the Internet. When someone configures a mail client on the PC or MAC, he specifies an SMTP server on his ISP's network to provide mail transport. This service is the "send" part of the email process.
- `POP3`—The POP3 server in `sendmail` allows users to retrieve their mail from the Internet. So, the sending agent and the receiving agent function on the same server and in the same mail program—`sendmail`.
- Internal Mail—On the local area networks, clients specify the Linux computer as both their internal and external mail transport agent. This allows seamless mail access internally and externally. Using the Linux computer, the administrator creates an alias in the configuration file that refers to the `sendmail` server as `mail.domain-name.com`.

The mail user agents on the local desktop specify the alias as their mail server, which provides all their email services. The user must have a mail client on his desktop that can send and receive standard Internet protocol mail.

`Sendmail` provided on the Red Hat distribution is a complete mail server and can reside on the same computer as the authentication server and the Samba application.

People have found configuring `sendmail` challenging. Red Hat provides excellent documentation on configuring `sendmail`.

Two initial configuration files Centennial used as a guide were provided in the Red Hat 6.0 distribution. These included the `/etc/sendmail.cw` file and the `/etc/sendmail.cf` file.

It should be noted as well that there exists a facility called `m4`, which makes the configuration of `sendmail`'s cryptic configuration files a more manageable task. `M4` allows the administrator to produce `sendmail` configuration files much more easily by converting these simpler text files into actual `Sendmail.cf` files.

The `sendmail` configuration Centennial used had a single machine act as a mail gateway for all the machines on the network. For example, the authentication server handled internal mail and acted as the main gateway to the Internet gateway. The Pentium II server handled all Internet mail accounts.

When the administrators added the hostnames of other machines in the District to the configuration file, mail sent to those machines were captured by the main mail server.

Then on the other machines, they edited the `/etc/sendmail.cf` file to “masquerade” as the main server when sending mail, and to forward any local mail processing to the Samba server. To do this, the administrators found the `DH` and `DM` lines in `/etc/sendmail.cf` and edited them.

## 示例：sendmail.cf 文件

```
