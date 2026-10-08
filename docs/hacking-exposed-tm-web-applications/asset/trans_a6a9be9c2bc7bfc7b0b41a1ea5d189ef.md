

## 第 3 章：破解 Web 服务器

## 95

这一项实践实践可以防止许多当前和未来的安全漏洞，因此希望你可以不再需要 Web 文件夹和数字仪表板，从而在晚上睡得更安稳。

## 总结

在本章中，我们学习了针对许多重大 Web 服务器漏洞的最佳防御方法，包括跟进厂商的安全补丁、禁用 Web 服务器上不必要的功能、将私有数据留在 HTML 和脚本之外，并勤于扫描那些绕过部署前验证过程的不可避免的入侵者。请记住，如果应用程序构建在充满漏洞的 Web 服务器上，那么它是不可能安全的。

## 参考文献和延伸阅读

| 参考文献 | 链接 |
|---|---|
| 相关厂商公告和补丁 | |
| IIS Webhooks 源码泄露公告，MS000-006 | http://www.microsoft.com/technet/security/bulletin/MS00-006.asp |
| IIS Unicode 目录遍历公告，MS000-086 | http://www.microsoft.com/technet/security/bulletin/MS000-086.asp |
| IIS 5 打印机缓冲区溢出公告，MS001-023 | http://www.microsoft.com/technet/security/bulletin/MS001-023.asp |
| IIS 双代码公告，MS001-026 | http://www.microsoft.com/technet/security/bulletin/MS001-026.asp |
| IIS ida/idq “代码红”缓冲区溢出公告，MS031-033 | http://www.microsoft.com/technet/security/bulletin/MS031-033.asp |
| IIS FrontPage 服务器扩展程序 RAD 支持公告，MS031-035 | http://www.microsoft.com/technet/security/bulletin/MS031-035.asp |
| IIS 服务端包含公告，MS014-044 | http://www.microsoft.com/technet/security/bulletin/MS014-044.asp |
| IIS .idc 路径泄露 KB 文章，Q193689 | http://support.microsoft.com/directory/article.asp?ID=KB;EN-US;Q193689 |
| 微软安全公告 MS02-018 IIS 累计补丁 (Q319733) | http://www.microsoft.com/technet/security/bulletin/MS02-018.asp |

## 破解 Web 应用程序

| 相关安全公告 | 链接 |
|--- |--- |
| mod_auth*sql 告 | http://cert.uni-stuttgart.de/advisories/apache_auth.php |
| eEye 发布的 ida/ida “代码红”IIS 远程缓冲区溢出公告 | http://www.eeye.com/html/Research/Advisories/AL200107177.html |
| eEye 发布的 IIS 5_printer 远程缓冲区溢出公告 | http://www.eeye.com/Research/Advisories/AD200105011.html |
| RFP 发布的 IIS Unicode 目录遍历公告 | http://www.wiretrip.net/rfp/doc.asp/i2/d57.html |
| 安全启服发布的 IIS decode 告 | http://www.nsfocus.com/english/homepage/sa01-02.html |
| Securityfocus.com 上 Netscape Enterprise Server 目录索引漏洞 | http://online.securityfocus.com/bid/1063 |
| Netscape Enterprise Server 3.6 缓冲区溢出 | http://online.securityfocus.com/bid/1024 |
| Netscape Enterprise Server Web 发布管理界面攻击 | http://online.securityfocus.com/bid/1075 |
| Novell GroupWise 任意文件检索漏洞 | http://www.foundstone.com/knowledge/advisories-display.html?id=327 |

## **已发布的漏洞**

- dark spykit 发布的 IIS 5 打印机溢出的 jill.c http://packetstorm.widexns.nl/0105-exploits/jill.c

- dark spykit 针对 IIS 5_printer 缓冲区溢出的 jillwin32 http://defaced.alaldas.de/2001/06/17/www.hack.co.ca

- CyrusTheGreat 发布的 IIS 5 打印机溢出 iis5hack http://defaced.alaldas.de/2001/06/17/www.hack.co.ca

- isno 发布的 ida/idq “代码红”缓冲区溢出 ida.c http://www.xforos.com/exp.php?id=4

- Maceo 发布的 unicodelap cmdasp.asp http://www.securityfocus.com

- IIS Ports NT4 权限提升漏洞 hk.exe http://www.nmrcc.org/files/nt/index.html

- 针对 IIS RevertToSelf 的 iiscrack.dll 权限提升 http://www.digitaloffense.net/iiscrack/

## 第 3 章：破解 Web 服务器

| 参考文献 | 链接 |
| --- | --- |
| 针对 IIS RevertToSelf 的 ispc 漏洞 http://www.xfocus.org/ |
| Netscape Enterprise Server 索引漏洞 | http://downloads.security.com/vulnerabilities/ |

## 免费工具

- netcat
- 微软安全公告 ... http://www.microsoft.com/directory/article.asp?ID=KB;EN-US;Q193689
- Nikto
- Typhon
- AppScan
- CyberUnderstand

## 普通参考文献

## 商业工具

## 第 4 章：应用程序调查

| 页面 | 路径 | 验证? | SSL? | GET/POST | 注释 |
|---|---|---|---|---|---|
| index.html | / |  |否 | | |
| login.asp | /login/ |否 | 是 | POST | 主验证页密码 |
| company.html | /about/ |  |否 | | 公司信息 |

**表 4-1.** 用于记录 Web 应用程序结构的示例矩阵

