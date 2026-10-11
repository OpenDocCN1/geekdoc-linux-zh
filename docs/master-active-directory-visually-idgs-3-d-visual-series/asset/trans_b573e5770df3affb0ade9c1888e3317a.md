
# 精通活动目录（Active Directory）可视化

分步操作说明
1000张截图
革命性的学习方式

![](img/763d5ae436311371600c0952a3da9094_0_0.png)

作者：Curt Simmons，MCSE，MCT

# 精通活动目录

![](img/763d5ae436311371600c0952a3da9094_2_0.png)

![](img/763d5ae436311371600c0952a3da9094_2_1.png)

TOGEX 第四视觉系列
第 105 号
2001 年

Hikaru Takeda
出版方
东京：J-City, Inc.
日本东京涩谷 1-2-8

# 精通活动目录可视化

![](img/763d5ae436311371600c0952a3da9094_4_0.png)

作者：Curt Simmons

IDG 视觉系列

![](img/763d5ae436311371600c0952a3da9094_4_1.png)

**IDG BOOKS**
源自
maranGraphics

IDG Books Worldwide, Inc.
国际数据集团（International Data Group）旗下公司
加利福尼亚州福斯特市 • 印第安纳波利斯 • 芝加哥 • 纽约

## 精通活动目录™ 可视化™

出版方
IDG Books Worldwide, Inc.
国际数据集团（International Data Group）旗下公司
加利福尼亚州福斯特市 E. Hillsdale 大道 919 号，400 室，邮编 94404
www.IDGbooks.com（IDG Books 全球网站）
文字和插图版权所有 © 2000 IDG Books Worldwide, Inc.
5755 Copiers Avenue
加拿大安大略省密西沙加市
L4Z 1R0
版权所有。未经出版商事先书面许可，不得以电子、摄影、录音或其他方式复制、传播本书的任何部分（包括内部设计、封面设计和图标）。
国会图书馆编目卡号：00-105128
ISBN: 0-7645-3432-5
美国印刷
10 9 8 7 6 5 4 3 2 1
1/VR/QZ/4ZZZN

### 商标致谢

活动目录（Active Directory）是微软公司的商标。
maranGraphics 徽标是 maranGraphics, Inc. 的商标。Visual、Visual 徽标、Tusk You're VISUALLY、Master VISUALLY、Simplified 及相关商业外观是在美国和其他国家注册的 IDG Books Worldwide, Inc. 的注册商标或商标，未经书面许可不得使用。其他所有商标均为其各自所有者的财产。IDG Books Worldwide, Inc. 和 maranGraphics, Inc. 与本书中提到的任何产品或供应商没有关联。

为了说明本书中描述的概念和技术，作者创建了一些姓名、公司名称、邮寄地址、电子邮件地址和电话号码，这些都是虚构的。这些虚构的名称、邮寄地址、电子邮件地址和电话号码与任何实际人员、公司和/或组织的相似之处纯属巧合，并非有意为之。

IDG Books Worldwide 在编写本书时已尽力而为。由于网站经常变化，本书中的一些网站地址可能已经移动或不再存在。
IDG Books Worldwide 不对因本书所含信息导致的任何损失或损害承担责任。
IDG Books Worldwide 也不支持本书所含网站中表达的观点。

分销商：加拿大由 IDG Books Canada Inc. 负责；英国由 Transworld Publishers Limited 负责；挪威由 IDG Norge Books 负责；瑞典由 IDG Sweden Books 负责；澳大利亚和新西兰由 IDG Books Australia Publishing Corporation Pty. Ltd. 负责；新加坡、马来西亚、泰国、印度尼西亚和香港由 TransQuest Publishers Pte Ltd. 负责；台湾由 Group Information Inc. 负责；日本由 IDG Muse Inc. 负责；南非由 Intelsoft 负责；法国由 Tyroles 负责；德国、奥地利和瑞士由 International Thomson Publishing 负责；阿根廷由 Distribubooks Cupside 负责；以色列由 LR International 负责；智利由 Calliber Libre 负责；秘鲁由 Ediciones ZETA S.C.R. Ltda. 负责；菲律宾由 WS Computer Publishing Corporation, Inc. 负责；委内瑞拉由 Computransepsa de Ediciones 负责；加勒比海地区和西印度群岛由 Express Computer Distributors 负责；墨西哥由 Mirrorsa Media Distributor, Inc. 负责；墨西哥由 Chips Computadoras S.A. de C.V. 负责；巴拿马由 Editorial Norma De Panama S.A. 负责；芬兰由 American Bookshops 负责。
如需团体销售，请致电 maranGraphics：800-460-6616。

如需了解 IDG Books Worldwide 在美国出版的书籍的一般信息，请致电我们的客户服务部：800-762-2974。如需转售商信息（包括折扣和高级销售），请致电我们的转售商客户服务部：800-434-3422。
如需了解在美国以外地区购买 IDG Books Worldwide 书籍的途径，请致电我们的国际销售部：317-572-3503，或传真：317-572-4002。
如需了解外语翻译的客户信息，请致电我们的客户服务部：1-800-434-3422，传真：317-572-4002，或发送邮件至 rights@idgbooks.com。
如需了解外国或国内版权许可信息，请致电：1-650-653-7598。
如需查询批量采购的销售事宜和特价，请联系我们的订单服务部：800-434-3422，或寄信至上述地址。
如需了解在课堂中使用 IDG Books Worldwide 书籍或订购考试副本的信息，请致电我们的教育销售部：800-434-2686，或传真：317-572-4002。
如需索取媒体审阅本、作者采访或其他公关信息，请致电我们的公共关系部：650-653-7000，或传真：650-653-7500。
如需获得机构、个人或教育用途的复印授权，请联系版权清除中心（Copyright Clearance Center）：马萨诸塞州丹弗斯 Rosewood 大道 222 号，邮编 01923，或传真：978-750-4470。
本书中显示的屏幕截图基于预发布软件，可能会有变动。

### 版权许可

![](img/763d5ae436311371600c0952a3da9094_5_0.png)

是由国际数据集团（International Data Group, Inc.）独家授权给 IDG Books Worldwide, Inc. 的注册商标。

> 责任限制/免责声明：出版商和作者在编写本书时已尽力而为。出版商和作者不对本书内容的准确性或完整性作出任何陈述或保证，并特别否认任何关于适销性或特定用途适用性的默示保证。除本段所述内容外，不存在其他保证。销售代表或书面/销售材料不得创建或扩展任何保证。此处提供的信息和意见的准确性和完整性，以及此处陈述的观点，并不保证或担保能产生任何特定结果。此处包含的建议和策略可能不适合您的情况。出版商和作者不对任何利润损失或其他任何间接的、偶然的、间接的或特殊的、偶然的、间接的或其他损害承担责任。每个优惠券提供的履行责任由提供方承担。

### 美国企业销售

请联系 maranGraphics
电话：(800) 460-6616
或传真：(905) 890-9434

### 美国贸易销售

请联系 IDG Books
电话：(800) 434-3422
或 (650) 653-7000

## 关于 IDG BOOKS WORLDWIDE

欢迎进入 IDG Books Worldwide 的世界。

IDG Books Worldwide, Inc. 是国际数据集团（International Data Group）的子公司，该集团是全球最大的计算机相关信息出版商，也是全球领先的信息技术信息服务提供商。IDG 由 Patrick J. McGovern 于 30 多年前创立，目前在全球拥有超过 9,000 名员工。IDG 在 75 多个国家出版了超过 290 种计算机出版物。每月有超过 9000 万人阅读一份或多份 IDG 出版物。

IDG Books Worldwide 于 1990 年创立，如今已成为美国最畅销的计算机书籍出版商。我们很高兴获得计算机出版协会（Computer Press Association）颁发的八项奖项，以表彰我们在编辑方面的卓越表现，以及 Computer Current 首届读者选择奖的三项奖项。我们畅销的……For Dummies® 系列已有超过 5000 万册印刷量，并翻译成 31 种语言。IDG Books Worldwide 通过与 IDG 高技术北京（IDG's Hi-Tech Beijing）的合资，成为第一家在中国出版计算机书籍的美国出版商。最近，IDG Books Worldwide 已成为全球数百万希望学习如何更好管理业务的读者的首选。

我们的使命很简单：我们的每本书都旨在为读者带来额外的价值和技能构建说明。我们的书由您了解并关心的专家撰写。我们编辑团队的知识库源于在出版、教育和新闻领域的多年经验——我们利用这些经验在新千禧年的细节上精益求精。简而言之，我们关心书籍，因此吸引了最优秀的人才。我们对受众、内部设计、图标使用和插图等细节特别关注。而且，由于我们采用电子方式进行书籍的撰写、编辑和桌面出版的 efficient 流程，我们可以花更多时间确保优质内容，而较少关注制作书籍的技术细节。

您可以信赖我们承诺以有竞争力的价格提供您感兴趣话题的高质量书籍。在 IDG Books Worldwide，我们继续传承 IDG 30 多年来提供质量的传统。您会发现没有比 IDG Books Worldwide 的书更好的主题书籍了。

![](img/763d5ae436311371600c0952a3da9094_6_0.png)

Patrick J. McGovern
董事长兼首席执行官
IDG Books Worldwide, Inc.

IDG 是全球领先的 IT 媒体、研究和展览公司。IDG 成立于 1964 年，1997 年收入为 20.5 亿美元，在全球拥有超过 9,000 名员工。IDG 提供了最广泛的媒体选择，覆盖 75 个国家的 IT 买家，占全球 IT 支出的 95%。IDG 多样化的产品和服务组合涵盖六个关键领域，包括印刷出版、在线出版、展览和会议、市场研究、教育和培训以及全球营销服务。超过 9000 万人阅读 IDG 的 290 本杂志和报纸中的一份或多份，包括 IDG 的主要全球品牌——Computerworld、PC World、Network World、Macworld 和 Channel World 系列出版物。IDG Books Worldwide 是全球增长最快的计算机书籍出版商之一，拥有 36 种语言的 700 多种书籍。仅“...For Dummies”系列就有超过 5000 万册印刷量。IDG 通过 IDG.net (http://www.idg.net) 为全球在线用户提供最大规模的技术特定网站网络，该网络由全球 55 个国家的 225 多个目标网站组成。国际数据公司（IDC）是全球最大的信息技术数据、分析和咨询提供商，在 41 多个国家设有研究中心，全球拥有超过 400 名研究分析师。IDG World Expo 是在包括 E3（电子娱乐展）、Macworld Expo、Com/Net、Windows World Expo、ICE（互联网商务展）、Agenda、DEMO 和 Spotlight 在内的 35 个国家举办 168 场全球品牌会议和展览的主要举办方。IDG 的培训子公司 ExecuTrain 是全球最大的计算机培训公司，在全球拥有超过 230 个办事处和 785 门培训课程。IDG 营销服务通过 IDG 的印刷、在线和展览计划制定全球综合营销项目，帮助行业领先的 IT 公司建立国际品牌知名度。

![](img/763d5ae436311371600c0952a3da9094_6_1.png)

![](img/763d5ae436311371600c0952a3da9094_6_2.png)

![](img/763d5ae436311371600c0952a3da9094_6_3.png)

![](img/763d5ae436311371600c0952a3da9094_6_4.png)

