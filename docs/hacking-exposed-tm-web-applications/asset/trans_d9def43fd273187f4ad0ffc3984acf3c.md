

这本书为使 Web 成为更安全的业务场所做出了巨大努力。
—Mark Carvey，开放 Web 应用安全项目（OWASP）负责人

# Web 应用黑客攻防揭秘

Web 应用安全秘密与解决方案

Joel Scambray
Mike Shema

> 原版《黑客攻防》（Hacking Exposed）的畅销书合著者

# 黑客攻防™：Web 应用篇

JOEL SCAMBRAY
MIKE SHEMA

McGraw-Hill/Osborne
纽约 芝加哥 旧金山
里斯本 伦敦 马德里 墨西哥城 米兰
新德里 圣胡安 首尔 新加坡 悉 上海

# 关于作者

## Joel Scrum

Joel Scrum 是《Hacking Exposed》(http://www.hackingexposed.com) 的合著者，这是一本国际畅销的网络安全类书籍，该书于 2001 年 10 月出版第三版。他还是《Hacking Exposed Windows 2000》的作者，这是对微软产品安全的权威内部分析，该书于 2001 年 9 月出版，目前已翻译成第二种外语。Joel 的出版物包括共同创立 *InfoWorld* 的 Security Watch、担任 *InfoWorld* 测试中心分析师，以及微软 TechNet Ask About...Security 格式的创始作者。

Joel 的写作主要源于他多年担任 IT 顾问的经验，客户涵盖从财富 500 强企业到初创公司，在这些工作中，他获得了对多种安全技术的广泛且经过实战的知识，并对各种应用程序和产品的安全架构进行了分析。Joel 的经历也为他在管理和备份方面提供了坚实的基础，他曾个人管理过几项创业项目和跨国项目，并在过去五年中维持了多家年收入巨大且规模各异的安全企业。他还拥有自己的测试实验室，在其中继续研究信息安全的前沿。

Joel 经常为计算机安全协会（CSI）、ISSA、ISACA、私营公司和政府机构等组织进行信息安全演讲。他目前 Foundstone Inc. (http://www.foundstone.com) 的执行合董事，此前曾任职于安永信、InfoWorld 以及一家大型商业房地产公司的 IT 总监。Joel 的学术背景包括来自加州大学戴维斯分校和洛洛矶矶分校（UCLA）的高级学位，并且是注册信息安全专业人员（CISSP）。

> —Joel Scrum 可以通过 @webhackingexposed.com 联系联系。

## Mike Shema

Mike Shema 是 Foundstone Inc. 的首席顾问，他为财富 100 强客户、金融机构和软件开发公司进行过数十次 Zeus 审查。他针对多种 Web 应用平台对方法论进行了实测，并开发了支持工具以自动化测试的许多方面。他的工作导致发现了商业 Web 软件中的漏洞。Mike 还为 Security Focus 和 DevX 写过关于 Web 服务器安全的技术专栏。他还作为《反黑客工具包》（The Anti-Hacker Toolkit）的合著者。在空闲时间，Mike 是一个活跃的角色扮演玩家。他拥有宾夕尼亚州立大学电气工程和法语学士学位。

> —Mike Shema 可以通过 mike@webhackingexposed.com 联系联系。

# 关于贡献作者

## 陈彦明 (Yen-Ming Chen)

陈彦明（CISSP, MCSE）是 Foundstone 的首席顾问，在那里他为客户提供安全服务。陈彦明拥有多年管理 UNIX 和 Internet 服务器的经验。他在无线网络、密码学、入侵检测和生存性领域拥有广泛知识。他的文章发表在 *SysAdmin*、*UnixReview* 以及其他技术杂志上。在加入 Foundstone 之前，陈彦明在卡内基梅隆大学（CMU）CMRI 网络安全中心工作，负责基于代理的入侵检测系统“snort”，这是一种轻量级网络入侵检测系统。陈彦明拥有台湾国立中央大学数学学士学位和卡内基梅隆大学信息网络硕士学位。陈彦明还是《黑客攻防》第三版的贡献作者。

## David Wong

David 是一位计算机安全专家，是 Foundstone 的首席顾问。David 曾在一家大型电信公司担任安全工程师职位，在那里进行安全产品审查、渗透测试以及网络监控。David 还是《Hacking Exposed 2000》和《黑客攻防》第三版的贡献作者。

McGraw-Hill/Osborne
2600 Tenth Street
Berkeley, California 94710

黑客攻防™：Web 应用

版权所有 2002 Joel Scambray 和 Mike Shea。保留所有权利。由 Corel VENTURA™ 制作。

书中信息从 McGraw-Hill/Osborne 认为可靠的来源获得。然而，由于存在人为或机械错误的可能性，McGraw-Hill/Osborne 对使用此类信息可能产生的任何结果的准确性、充分性或完整性不负责。未经 McGraw-Hill/Osborne 书面许可，本书任何部分不得以任何形式复制、传播、存储在数据库或以计算机程序形式执行，但 1976 年版权法允许的例外除外。如需安排范围外的批量折扣、促销或捐赠，请联系上述地址的 McGraw-Hill/Osborne。

ISBN 0-07-222438-

| 角色 | 姓名 |
| :--- | :--- |
| **发行** | Brandon A. Nordin |
| **执行发行** | Scott Rogers |
| **高级编辑** | Jane Brown |
| **项目编辑** | Patty Mon |
| **采购协调员** | Claireslan |
| **技术编辑** | Yen Chen |
| **校对** | Paul Tyler |
| **索引** | Valerie Perry |
| **插画师** | Elizabeth Jang, Melinda Moore |
| **系列设计** | Dick Schwartz, Peter F. Hancik |
| **封面设计** | Dodie Shoemaker |

在美国印刷。

# 致谢

致那些每一分钟、每天都在奋斗的人。
—Joel Scambray

给我的父母，他们为我开启了许多门；给我的兄弟 David 和 Steven，他们比他们想象的更有启发。
—Mike Shema

本页故意留白。

# 概览

| 第一部分 侦察 |
| :--- | :--- |
| * 1 Web 应用与安全简介 | 3 |
| * 2 分析 | 25 |
| * 3 攻击 Web 服务器 | 41 |
| * 4 调查应用程序 | 99 |

| 第二部分 攻击 |
| :--- | :--- |
| * 5 身份验证 | 131 |
| * 6 授权 | 161 |
| * 7 攻击会话管理 | 177 |
| * 8 输入验证攻击 | 201 |
| * 9 攻击 Web 数据存储 | 225 |
| * 10 攻击 Web 服务 | 243 |
| * 11 攻击 Web 应用管理 | 261 |
| * 12 Web 客户端攻击 | 277 |
| * 13 案例研究 | 299 |

| 第三部分 附录 |
| :--- | :--- |
| * A 网站安全检查清单 | 311 |
| * B Web 攻击工具与技巧速查 | 317 |
| * C 使用 Libwhisker | 333 |
| * D UrlScan 安装与配置 | 345 |
| * E 关于辅助网站 | 371 |

索引 ... 373

