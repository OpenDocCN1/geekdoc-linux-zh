

# 附录 B：Web 攻击工具与技术速查表

| 任务 | 工具/技术 | 资源 |
|---|---|---|
| 识别与美国组织相关的 IP 地址范围 | ARIN 网站 | http://www.arin.net |
| 识别注册到某机构的 DNS 域名 | whois SamSp | 大多数操作系统内置，或访问 http://samspade.org |
| DNS 探测问：识别活动主机、监听端口和服务横幅 | nslookup | 大多数操作系统内置 http://www.foundstone.org |
| 识别活动主机、监听端口和服务横幅 | nmap | http://www.insecure.org/ |

| 参考资料 | 链接 |
|---|---|
| 欧洲 IP 地址分配 | http://www.ripe.net/ |
| 亚太地区 IP 地址分配 | http://www.apnic.net |
| 美国军 IP 地址分配 | http://whois.nic.mil |
| 美国政府 IP 地址分配 | http://whois.nic.gov |
| 经的域名注册服务提供商 | http://www.internic.net/regist.html |
| 国家代码（双字母）顶级域的 Whois 信息 | http://www.uwhois.com. |

# 攻破 Web 应用程序 (Hacking Exposed Web Applications)

# 分析中常用的端口

| 协议 | 端口 | 服务 |
|---|---|---|
| TCP | 21 | FTP |
| TCP | 22 | SSH |
| TCP | 23 | Telnet |
| TCP | 25 | SMTP |
| TCP | 53 | DNS |
| TCP | 80 | HTTP |
| TCP | 110 | POP |
| TCP | 111 | RPC |
| TCP | 139 | NetBIOS 服务 |
| TCP | 389 | LDAP |
| TCP | 443 | SSL |
| TCP | 1433 | MS SQL Server |
| TCP | 1521 | Oracle |
| TCP | 2049 | NFS |
| TCP | 3306 | MySQL |
| TCP | 3389 | Terminal Server |
| TCP | 5432 | PostgresSQL |
| TCP | 8007 | JSP Engine |
| TCP | 8080 | JSP Engine |
| TCP | 8443 | JSP Engine |
| UDP | 53 | DNS |
| UDP | 69 | TFTP |
| UDP | 137 | NetBIOS 名称 |
| UDP | 138 | UDP 数据报 |
| UDP | 161 | SNMP |
| UDP | 500 | IKE |

# 攻击 Web 服务器

| 任务 | 工具/技术 | 资源 |
|---|---|---|
| Apache 长斜杠目录列表 | GET /directory/[大量末尾斜杠] | http://online.securityfocus.com/bid/2503 |
| Apache 多视图目录列表 | GET /directory?M=D | http://www.securityfocus.com/bid/3009 |

# 附录 B：Web 攻击工具与技术速查表

# 攻击 Web 服务器（续）

| 任务 | 工具/技术 | 资源 |
|---|---|---|
| JSP 目录列表 | GET/%3f.jsp | http://online.securityfocus.com/advisories/3689 |
| JSP 源码泄露 | GET /file.js70 | http://securitytracker.com/alerts/2001/Mar/1001207.html |
| IIS 缓冲区溢出 | jill (及变体) | http://packetstorm.widess.nl/0105-exploits/jill.c |
| IIS+ htr 源码泄露 | GET /file+.htr | http://www.microsoft.com/technique/bullet/MS01-04.asp |
| IIS Unicode 目录遍历 | GET /scripts/%%0af/.../winint/system32/cmd.exe?+c+dir:\* | http://www.microsoft.com/technique/bullet/MS00-86.asp |
| IIS 双解码遍历 | GET /scripts/%%25%.../winint/system32/cmd.exe?+c+dir:\* | http://www.microsoft.com/technique/bullet/MS01-026.asp |
| 通过 IIS 目录遍历上传文件 | Roel Telming 提供的 Unicode.pl | http://www.securityfocus.com |
| 通过 IIS 目录遍历执行命令 | Mace 提供的 cmddasp.asp | http://www.dogmile.com |
| IIS 4 权限提升 | Todd Sabin 提供的 hk.exe | http://www.nmrc.org/nt/index.html |
| IIS 5 权限提升 | 来自 Anonymous 的 iisrack | http://www.digitaloffense.net/iisrack/ |
| IIS 5 权限提升 | isno@xfocus 提供的 ispc | http://www.xfocus.com/ |
| IIS 攻措施措施 | 带有 UrlScan 的 IISLockdown 工具 | http://www.microsoft.com/windows2000/downloads/urlscan/ |

# Web 服务器/应用程序扫描器

（此处省略了后续重复的表格翻译，格式与上述一致。由于原文存在大量完全重复的区块，实际应用中通常仅保留一份逻辑部分。）

