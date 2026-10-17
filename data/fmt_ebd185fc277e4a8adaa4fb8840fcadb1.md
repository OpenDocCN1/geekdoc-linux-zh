
以下列表已不再维护。关于通过 Linux IP 伪装工作的应用程序的信息，请参阅 http://dijon.nais.com/~nevo/masq/，更多细节请参阅 IP Masquerade Resource（http://ipmasq.cjb.net/）。

通常，使用 TCP 和 UDP 的应用程序应该能正常工作。如果你有任何关于 IP 伪装应用程序的建议、提示或问题，请访问 Lee Nevo 维护的 http://dijon.nais.com/~nevo/masq/。

### 可工作的客户端

#### 通用客户端

- `HTTP`：所有支持的平台，浏览网页
- `POP/SMTP`：所有支持的平台，电子邮件客户端
- `Telnet`：所有支持的平台，远程会话
- `FTP`：所有支持的平台，需加载 `ipmasqftp.o` 模块（并非所有网站都能与某些客户端配合工作；例如，某些网站无法使用 wstftp32 访问，但可以使用 Netscape）
- `Archie`：所有支持的平台，文件搜索客户端（并非所有 archie 客户端都受支持）
- `NNTP (USENET)`：所有支持的平台，USENET 新闻客户端
- `VRML`：Windows（可能包括所有支持的平台），虚拟现实浏览
- `traceroute`：主要适用于基于 Unix 的平台，某些变体可能无法工作
- `ping`：所有平台，需使用 ICMP 补丁
- 基于 IRC 的任何工具：所有支持的平台，需使用 `ipmasqirc.o` 模块
- `Gopher` 客户端：所有支持的平台
- `WAIS` 客户端：所有支持的平台

#### 多媒体客户端

- `Real Audio Player`：Windows，网络流式音频，需加载 `ipmasqradio` 模块
- `True Speech Player 1.1b`：Windows，网络流式音频
- `Internet Wave Player`：Windows，网络流式音频
- `Worlds Chat 0.9a`：Windows，客户端-服务器 3-D 聊天程序
- `Alpha Worlds`：Windows，客户端-服务器 3-D 聊天程序
- `Internet Phone 3.2`：Windows，点对点音频通信，只有在你发起呼叫时人们才能联系到你，但人们不能拨打你的电话
- `Powwow`：Windows，点对点文本、音频和白板通信，只有在你发起呼叫时人们才能联系到你，但人们不能拨打你的电话
- `CU-SeeMe`：所有支持的平台，需加载 `cuseeme` 模块，详情请参阅 IP Masquerade Resource（http://ipmasq.cjb.net/）
- `VDOlive`：Windows，需使用 `vdolive` 补丁

#### 其他客户端

- `NCSA Telnet 2.3.08`：DOS，包含 Telnet、FTP、Ping 等在内的工具套件
- `PC-anywhere for windows 2.0`：MS-Windows，通过 TCP/IP 远程控制 PC，仅当它作为客户端工作时有效，不能作为主机
- `Socket Watch`：使用 NTP –（网络时间协议）
- `Linux net-acc t` 包：Linux，网络管理-账户包

### 不可工作的客户端

- `Intel Internet Phone Beta 2`：可以连接，但语音仅单向（输出）传输
- `Intel Streaming Media Viewer Beta 1`：无法连接到服务器
- `Netscape CoolTalk`：无法连接到对端
- `talk, ntalk`：无法工作——需要编写内核代理。
- `WebPhone`：目前无法工作（它对地址做了无效的假设）
- `X`：未测试，但我认为除非有人构建 X 代理，否则无法工作，这通常是伪装代码之外的外部程序。实现这一点的一种方法是使用 ssh 作为链接，并使用内部 X 代理。

### 在其他机器上测试过的平台/操作系统

- Linux
- Solaris
- Windows 95
- Windows NT（工作站和服务器版）
- Windows For Workgroup 3.11（带有 TCP/IP 包）
- Windows 3.1（带有 Chameleon 包）
- Novell 4.01 服务器
- OS/2（包括 Warp v3）
- Macintosh OS（带有 MacTCP 或 Open Transport）
- DOS（带有 NCSA Telnet 包，DOS Trumpet 部分工作）
- 带有 AmiTCP 或 AS225-stack 的 Amiga
- 带有 UCX（VMS 的 TCP/IP 堆栈）的 VAX 工作站 3520 和 3100
- 运行 Linux/Redhat 的 Alpha/AXP
- SCO OpenServer（v3.2.4.2 和 5）
- 运行 AIX 的 IBM RS/6000

基本上所有操作系统平台都支持 TCP/IP，并允许你指定网关/路由器如何与 IP 伪装一起工作。

### IP 防火墙管理 (`ipfwadm`)

本节提供了使用 `ipfwadm` 的更深入的指南。

以下是在具有静态 PPP 地址的 PPP 链接后方的防火墙/伪装系统的配置。一个受信任的接口是 `192.168.255.1`；PPP 接口已被修改以保护当事人隐私。我分别列出了每个传入和传出接口，以捕获 IP 欺骗以及填充路由和/或伪装。此外，任何未明确允许的内容都是禁止的！
