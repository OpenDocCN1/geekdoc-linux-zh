

## 图 11.1 Nessus 设置窗口

![](img/415c89a1ede71e11e5040a0038b6916c_490_0.png)

不仅了解可能存在的漏洞，而且了解可能的风险数量，对于制定修补这些漏洞的策略非常有用。此外，你还可以用这些数字向老板申请额外资源，包括额外的人力和安全相关软件。

## 主机入侵扫描器，或在入侵者之前找到漏洞

主机入侵扫描器会检查文件权限的设置是否正确。对于 UNIX，此类扫描器会搜索世界可写文件或目录权限，以及由 root 拥有 setuid 或 setgid 文件。更先进的商业扫描器会检查系统安装组件是否缺少安全补丁或存在已知漏洞。

大多数免费的主机入侵扫描器有些过时，但可以提供良好的初始检查，尤其适用于较旧的网络。这些工具包括：

- COPS，最初由 CERT 分发，最后更新于 1993 年 (http://www.fish.com/cops/)。
- Tiger: (ftp://net.tamu.edu/pub/security/TAMU)。

一些更新的免费工具是：

- Sherpa (http://www.nbank.net/~rick/sherpa)。
- Titan (http://www.fish.com/~brad/titan/Titan-Docs/TITAN_documentation.html)。

Solaris 2.7 附带了一个名为自动化安全增强工具 (ASET) 的工具，该工具旨在帮助系统管理员以自动化的方式监控和控制安全级别。最后，最完整的主机入侵扫描器之一是 ISS 的 System Scanner（可在大多数常见的 UNIX 版本下运行，并且 Windows 2000 版本正在开发中）。有关该扫描器的更多信息可在 http://www.iss.net/prod/ss.php3 上找到。

其他商业系统扫描器或有用工具包括：

- Inspector Scan (http://www.shavlik.com/products/inspect/20103.htm)。
- Webtrends security analyzer (http://www.webtrends.com/products/wsa/intro.htm)。
- DumpACL，一个用于转储文件系统、注册表、打印机和共享的权限 (DACL) 和审计设置 (SACL) 的实用程序：(http://www.systemtools.com/somarsoft/)。

## MODEMS

即使是最好的保护和预防方案，也可能因基础设施中不当安装的单个调制解调器而被破坏。调制解调器需要强身份验证并由计算机组管理，与计算机的登录屏幕没有区别。然而，由用户连接到随机工作站或服务器的调制解调器可能为入侵者提供一个简单的攻击点。应将移除不当安装的调制解调器作为安全策略中的高优先级事项。

## Nessus 报告

132.168.1.2
  domain (53/tcp)
  ftp (21/tcp)
  安全警告
  FTP 服务允许匿名登录。如果你不想与不认识的人共享数据，那么你应该停用匿名账户，因为它只会给你带来麻烦。
  在大多数 Unix 系统中，执行以下操作：
  echo ftp >> /etc/ftpusers
  将会纠正此问题。
  风险因素：低
  端口开放，但收到非标准响应
  netbios-ns (137/tcp)
  安全漏洞
  发现以下 7 个名称：
  WHITETIGER = 这是 WINS 客户端为工作站服务注册的计算机名
  WHITETIGER = 为计算机上的信使服务注册的计算机名 th
  WHITETIGER
  __MSBROWSE__
  MYGROUP = 工作组 / 域名称
  MYGROUP
  MYGROUP
  远程计算机在其适配器上的 MAC 地址如下：
  0x00 0x00 0x00 0x00 0x00 0x00
  nntp (119/tcp)
  安全警告
  201 localhost InterNetNews NNTP server INN 2.2.1 25-Aug-1999 ready (no posting)。
  general/tcp
  smtp (25/tcp)
  unknown (161/tcp)
  telnet (23/tcp)
  www (80/tcp) 。
  auth (113/tcp)
  login (513/tcp)
  unknown (810/udp)
  unknown (1024/udp)
  unknown (721/udp)
  unknown (738/udp)

![](img/415c89a1ede71e11e5040a0038b6916c_492_0.png)

图 11.3 Nessus 探测选择。

## 图 11.2

Nessus 目标配置。

![](img/415c89a1ede71e11e5040a0038b6916c_491_0.png)

## 图 11.4
Nessus 进度屏幕。

![](img/415c89a1ede71e11e5040a0038b6916c_493_0.png)

