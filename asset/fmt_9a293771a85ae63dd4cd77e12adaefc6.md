
# 第 2 章

| 名称 | 数量 | 响应 |
| :--- | :--- | :--- |
| 加加 | 11 | NetBIOS Response |
| 休斯顿 | 5 | Servername: SCADA <0x0> |
| ylvan湖 | 5 | WORKGROUP <0x0> |
| 本溪 | 5 | SCADA <0x1> |
| 斯德哥尔摩 | 5 | WORKGROUP <0x1> |
| | | WORKGROUP <0x1> |
| 组织 | | |
| Telus Communications | 13 | 401 Authorization |
| Nucleus Information... | 6 | 142.59.128.96 |
| Telefonica de Espana | 5 | Windows XP |
| Comcast Business... | 4 | AGT |
| Hetzner Online AG | 4 | Added on 28.02.2013 |
| 加加 | | d010-137-225.abhsla.telia.com |
| | | HTTP/1.0 401 Authorization |

## Google hacking

Google hacking 是最常见的搜索引擎侦察形式。Google hacking 使用 Google 搜索高级操作在结果中定位特定的字符串。搜索过滤器可以锁定特定版本的应用程序，或者通过 `entitle:"index of"` 操作识别包含敏感日志文件。以下截图演示了使用 Google 搜索查找可用的 Linksys 摄像头。第一张显示了执行命令后的示例结果。最后一张截图显示了使用此技术可以找到摄像头。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_61_0.png)

- Linksys Wireless-G Internet Video Camera
  - URL：`92.71.245.81:1027/main.cgi?next_file=index.htm`
  - 描述：Linksys Ver. 2.12, Home | Video | Setup | Linksys Web | Help | Exit
- Linksys Wireless-G PTZ Internet Camera with Audio
  - URL：`mam-camera.dns.alias.net/main.cgi?next_file=index.htm`
  - 描述：WWC200. Wireless-G PTZ Internet Camera with Audio, Home| View Video| Setup| Linksys Web Exit. Connected User: 0. | Copyright 2007 Cisco ...
- Linksys Web Camera
  - URL：`177.142.46.3:1028/main.cgi?next_file=index.htm`
  - 描述：Linksys Ver. 2.13, Home | Video View | Setup | Linksys Web | Help | Exit
- Linksys Wireless-G Internet Video Camera
  - URL：`72.250.149.1024/main.cgi?next_file=index.htm`
  - 描述：Linksys Ver. 2.11, Home | Video | Setup | Linksys Web | Help | Exit | You visited this page 3 times. Last visit: 3/19/13
- Linksys Wireless-G PTZ Internet Camera with Audio
  - URL：`213.67.110.1024/main.cgi?next_file=main.htm`
  - 描述：WWC200. Wireless-G PTZ Internet Camera with Audio, Home| View Video, Setup, | Linksys Web, Exit. Image Resolution, 640*480, 320*240, ...
- Linksys Wireless-G PTZ Internet Camera with Audio
  - URL：`66.11.106.28:8181/main.cgi?next_file=main.htm`
  - 描述：WWC200. Wireless-G PTZ Internet Camera with Audio, Home| View Video| Setup Linksys Webt. Image Resolution, 640*480, 320*240, Northwest ... You visited this page 3 times. Last visit: 3/19/13

- LINKSYS Cisco Systems, Inc. 分部 | WCS80N
- 无线-N 家庭监控摄像头 | 首页 | 观看视频 | 设置 | Linksys 网页 | 帮助 | 退出

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_62_0.png)

以下是一些示例查询语句：

- 识别敏感文档：`intext: classified top secret`
- 识别 Linksys 摄像头管理 GUI（注意：你可能不会喜欢你发现的内容）：`inurl:main.cgi`
- 识别 Nessus 报告以寻找漏洞系统：`inurl:NESSUSXXXXXXX`

关于 Google 黑客攻击（Google hacking）的更多信息，请查看由 Johnny Long 编写的一本非常好的书《渗透测试者的攻击指南》（Hacking for Penetration Testers），以及他的网站 http://johnny.ihackstuff.com。

## Google 黑客攻击数据库

Google 黑客攻击数据库（GHDB）由 Hackers For Charity（http://www.hackersforcharity.org/）的 Johnny Long 创建，是查询语句的权威来源。针对用户名、密码、漏洞系统和利用程序的搜索已被黑客爱好者捕获并分类。这些对 Google 搜索进行分类的爱好者被形象地称为 Google dorks（Google 狗术）。

要访问 GHDB，请访问 http://www.exploit-db.com/google-dorks/

你将在网页上看到列出的最新 GHDB 查询。你可以自己点击任何一个查询语句。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_63_0.png)

你将在页面底部找到已保存的不同搜索类别。在以下示例中，我们滚动到“漏洞文件”（Vulnerable Files）类别，并选择“ionCube Loader Wizard”查询。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_63_1.png)

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_64_0.png)

我们可以选择查询语句，它将带我们进入 Google 并执行相同的查询语句。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_64_1.png)

### 侦察

前面的示例显示 Google 找到了一些结果。ionCube Loader 显然没有配置或配置错误。ionCube Loader 实际上是一款优秀的软件，它可以保护用 PHP 编写的软件免受未经授权的计算机查看或更改。然而，在这种情况下，管理员在没有任何任何配置的情况下运行了默认向导。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_65_0.png)

当我们点击第一个链接时，进入了配置软件的主屏幕。

GHDB 本质上将 Google 变成了渗透测试者的有限 Web 应用程序扫描器。在这种情况下，可以增加性的良好软件现在可能被攻击者用于攻击 Web 服务器。

## 网络研究

许多人并不理解目标网络以发动攻击的真实目的。业余渗透测试者理解在执行渗透测试之前需要选择一个目标。毕竟，渗透测试者需要一个地方来部署他们的工具库。这些业余人员会运行 `Nmap`、`ping` 扫描或其他嘈杂的工具来确定哪些目标可用，从而干扰环境，这随后会导致产生糟糕的结果。

网络侦察的核心在于选择目标。经验丰富的网络安全专业人士会告诉你，良好的侦察在于选择一个高质量的目标，并将大部分时间花在观察而不是行动。每次渗透测试的第一步都是准确地找到并选择高质量的目标。
