
- 攻破大厦 (`IW`) (`NSA`)

### B.9.6 盯着你的耳朵

这段 26 分钟的视频涵盖了一些非计算机的问题：

- 卓越的裁量 (`Magnificent Discretion`)
- 碎片信息 (`Bits & Pieces`)
- 仅仅是传真，先生 (`Just the Fax, Sir`)
- 盯着你的耳朵 (`Ears Looking at You`)

### B.9.7 审计师与评估员信息保证 (`IA`) CD-ROM

这个交互式 CD-ROM 对计算机犯罪示例进行了分类和详细说明，包括威胁、应对措施、机性和风险。还讨论了相关法律。

### B.9.8 事件准备与响应 CD-ROM

全名为 *Windows NT 系统管理员事件准备与响应 (`SAIPR)`*（*针对系统管理员*）。虽然它是针对 NT 管理员的，但某些主题是通用且适用的，对 Linux 系统管理员也有帮助。主题包括事件前收集信息、识别未经授权的活动、策略与程序以及调查。

它由国防部的计算机调查训练计划（`DCIPT`）制作。

### B.9.9 DOD 信息安全意识 CD-ROM

该 CD-ROM 旨在为所有使用国防部计算机系统的人提供计算机安全意识。

### B.9.10 运行信息系统安全 (`OISS`) 卷 1&2 CD-ROM

该 CD-ROM 涵盖了通用计算机安全意识。

## B.10 基于 TCP/IP 的网络卷 I、II 和 III

这是一本非常优秀且的书籍，涵盖了常用协议的细节以及如何编写客户端/服务器系统。它受到了高度评价。第一卷第四版于 2000 年 4 月出版。

*Internetworking with TCP/IP Vols. I, II, and III*

Douglas Comer

Prentice Hall, © 2000

ISBN 0-13-018380-6 (卷 I)

ISBN 0-13-973843-6 (卷 II)

ISBN 0-13-260969-X (卷 III BSD Socket)

## B.11 Linux 应用开发

这本优秀的书籍涵盖了在 Linux 上使用 C 语言编程的所有方面。第 6 章“内存调试工具”将特别引起感兴趣，因为它涵盖了调试导致缓冲区溢出以及可能导致安全漏洞的类似内存错误。

Linux Application Development

Michael K. Johnson 和 Erik W. Troan

Addison-Wesley, © 1998

ISBN 0-20-130821-5

## B.12 顾问：好的、坏的与圆滑的

在聘用顾问时，与其他来源对他们的声明进行交叉引用至关重要。许多因素超出了简历的范围。你应该要求推荐并与过去的客户交流，以确定顾问是否真的交付了承诺的内容。寻找 Linux 和 UNIX 的特定经验，并询问他们如何跟上演变的安全形势。如果一个顾问无法解释公钥加密或 TCP 与 UDP 之间的区别等基本概念，他们可能无法胜任这项任务。

## 附录 C. 网络服务与端口

程序用于网络通信的每个套接字（`socket`）都有协议类型（通常为 TCP 或 UDP）以及用于标识本地和远程系统中其它进程的端口号。端口号范围从 0 到 65535，通常以双字节无符号整数的形式以主机字节序存储并以网络字节序传输。

每个协议都有自己的一组 65536 个端口号。然而，一个组织通常会为一个端口号同时注册 TCP 和 UDP 协议。这导致许多服务显示为同时具有 TCP 和 UDP 端口，但实际上只使用了其中一个。

端口号分为三个范围，如表 C.1 所示

## 表 C.1. 端口号范围

| 范围 | 用途 |
| --- | --- |
| 0-1023 | 已知 |
| 1024-49151 | 注册 |
| 49152-65535 | 动态与私有 |

已知端口（0-1023）由 IANA（互联网分配编号机构）分配。在 Linux（以及 UNIX）上，以 root 身份运行的进程可以打开其中一个端口并进行监听。这种安全规定是为了防止如果特定服务器崩溃或未运行，恶意的普通用户无法监听该端口并获取“宇宙的秘密”。某些服务（如 `rshd`）信任请求本地服务的远程系统端口并非恶意的。

任何人都可以请求为其分配一个未使用的端口号，如果该实体能够证明其用法的合理性，就可以获得分配。其中一个端口号是应 Larry Gee 和本文作者的请求分配的。可以通过以下方式联系 IANA：

`http://www.iana.org`

`iana@iana.org`

当前的已知端口[1]列在表 C.2 中。一些最重要的注册端口列在表 C.3 中。请注意，表中仅包含了常用端口。最新的列表可以在 IANA 网站获取。

## 表 C.2. 已知端口号

| 关键字 | 端口 | 说明 |
| --- | --- | --- |
| | 0/tcp | 预留 |
| | 0/udp | 预留 |
| tcpmux | 1/tcp | TCP 端口服务多路复用 |
| tcpmux | 1/udp | TCP 端口服务多路复用 |
| rje | 5/tcp | 远程作业输入（未使用） |
| rje | 5/udp | 远程作业输入（未使用） |
| echo | 7/tcp | 回显 |
| echo | 7/udp | 回显 |
| discard | 9/tcp | 丢弃 |
| discard | 9/udp | 丢弃 |
| systat | 11/tcp | 活跃用户 |
| systat | 11/udp | 活跃用户 |
| daytime | 13/tcp | 日时间 (RFC 867[*]) |
| daytime | 13/udp | 日时间 (RFC 867) |
| qotd | 17/tcp | 每日名句 |
| qotd | 17/udp | 每日名句 |
| charger | 19/tcp | 字符生成器 |
| charger | 19/udp | 字符生成器 |
| ftp-data | 20/tcp | 文件传输 [默认数据] |
| ftp-data | 20/udp | 文件传输 [默认数据] |
| ftp | 21/tcp | 文件传输 [控制] |
| ftp | 21/udp | 文件传输 [控制] |
| ssh | 22/tcp | SSH 远程登录协议 |
| ssh | 22/udp | pcAnywhere (非官方) |
| telnet | 23/tcp | Telnet |
| telnet | 23/udp | Telnet |
| smtp | 25/tcp | 简单邮件传输协议 [Sendmail] |
| smtp | 25/udp | 简单邮件传输协议 [Sendmail] |
| time | 37/tcp | 时间 |
| time | 37/udp | 时间 |
| name | 42/tcp | 主机名服务器（非 DNS) |
| name | 42/udp | 主机名服务器（非 DNS) |
| nameserver | 42/tcp | 主机名服务器（非 DNS) |
| nameserver | 42/udp | 主机名服务器（非 DNS) |
| nickname | 43/tcp | Who Is |
| nickname | 43/udp | Who Is |
| domain | 53/tcp | 域名服务器 (DNS/named) |
| domain | 53/udp | 域名服务器 (DNS/named) |
| whois++ | 63/tcp | whois++ |
| whois++ | 63/udp | whois++ |
| sql*net | 66/tcp | Oracle SQL*NET |
| sql*net | 66/udp | Oracle SQL*NET |
| bootps | 67/tcp | 引导协议服务器 |
| bootps | 67/udp | 引导协议服务器 |
| bootpc | 68/tcp | 引导协议客户端 |
| bootpc | 68/udp | 引导协议客户端 |
| tfftp | 69/tcp | 简单文件传输协议 |
| tfftp | 69/udp | 简单文件传输协议 |
| gopher | 70/tcp | Gopher |
| gopher | 70/udp | Gopher |
| finger | 79/tcp | Finger |
| finger | 79/udp | Finger |
| http | 80/tcp | 万网 HTTP |
| http | 80/udp | 万网 HTTP (未使用) |
| www | 80/tcp | 万网 HTTP |
| www | 80/udp | 万网 HTTP (未使用) |
| www-http | 80/tcp | 万网 HTTP |
| www-http | 80/udp | 万网 HTTP |
| kerberos | 88/tcp | Kerberos |
| kerberos | 88/udp | Kerberos |
