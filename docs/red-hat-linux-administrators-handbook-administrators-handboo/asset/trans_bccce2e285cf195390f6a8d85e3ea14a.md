
## Red Hat
Linux
系统管理员手册

涵盖至
Red Hat
Linux 6.1

![](img/c2419364ebb911c809b6a79991707c27_0_0.png)

![](img/c2419364ebb911c809b6a79991707c27_0_1.png)

终极实战手册

- 详细的、分步的安装、高级配置和故障排除流程
- 易于查找的、独立的解决方案——无需在各章节之间翻找答案
- 仅提供实用信息——无理论、无教程、无废话

Mohammed J. Kabir

![](img/c2419364ebb911c809b6a79991707c27_0_2.png)

## Red Hat® Linux® 系统管理员手册

![](img/c2419364ebb911c809b6a79991707c27_2_0.png)

## Red Hat® Linux® 系统管理员手册

Mohamed J. Kabir

M&T Books
IDG Books Worldwide, Inc. 的一个印记
Foster City, CA • Chicago, IL • Indianapolis, IN • New York, NY

## Red Hat Linux® 系统管理员手册

出版者
M&T Books
IDG Books Worldwide, Inc. 的一个印记
919 E. Hillsdale Blvd., Suite 400
Foster City, CA 94404
www.idgbooks.com

© 版权所有 2000 IDG Books Worldwide, Inc. 保留所有权利。
版权 © 2000 IDG Books Worldwide, Inc. 保留所有权利。本书的任何部分，包括内部设计、封面设计和图标，未经出版者事先书面许可，不得以任何形式（电子、影印、录音或其他方式）复制或传播。

Linux 企鹅 Tux 的图像由 Larry Ewing (larry@... ) 创建，随后由 Tuomas Kuosmanen (t...) 修改用于 IDG Books Worldwide 在本书封面上的使用。IDG Books Worldwide 感谢他对 Tux 的工作。

ISBN: 0-7645-4637-6
美国印刷
10 9 8 7 6 5 4 3 2 1
10/RB/QQ/QC/FQ

美国由 IDG Books Worldwide, Inc. 发行。
由 CDG Books Canada Inc. 在加拿大发行；由 Transworld Publishers Limited 在英国发行；由 IDG Books Australia Pty Ltd. 在澳大利亚和新西兰发行；由 TransQuest Publishers Pte Ltd. 在新加坡发行；由 Gotop Information Inc. 在台湾发行；由 ICG Muse, Inc. 在日本发行；由 Intersoft 在南非发行；由 Eyprecs 在法国发行；由 International Thomson Publishing 在西班牙发行；由 Distribuidora Cuspide 在阿根廷发行；由 LR International 在巴西发行；由 Galego Libros 在智利发行；由 Ediciones ZETA S.C.R. Ltda. 在秘鲁发行；由 WS Computer Publishing Corp. 在菲律宾发行；由 Contemporanea de Ediciones 在委内瑞拉发行；由 Express Computer Distributors 在加勒比海和西印度群岛发行；由 MicroMedia 在中国发行。

Computadoras S.A. de C.V. 在墨西哥发行；由 Editorial Norma de Panama S.A. 在巴拿马发行；由 American Bookshops 在芬兰发行。
有关 IDG Books Worldwide 书籍的一般信息，请联系我们的客户服务部，电话 800-762-2974。有关零售商信息，包括折扣和特价销售，请致电我们的经销商客户服务部，电话 800-762-2974。
有关在美国境外购买 IDG Books Worldwide 书籍的地点信息，请联系国际销售部，电话 317-596-5530 或传真 317-596-5932。
有关外语翻译的消费者信息，请联系我们的客户服务部，电话 800-434-3422、317-596-5692，或电子邮件 rights@idgbooks.com。
有关一般或国内版权许可信息，请致电 650-655-3000。
有关大批量销售信息，请联系特价销售部，电话 650-655-3200，或写信至上述地址。
有关在课堂上使用 IDG Books Worldwide 书籍或订购考试用书的信息，请联系教育销售部，电话 800-434-2086 或 317-596-5499。
有关新闻审阅本、作者访谈或其他宣传信息，请联系我们的公共关系部，电话 650-655-3000 或传真 650-655-3299。
有关企业、个人或教育用途的复印信息，请联系版权许可中心，地址：美国马萨诸塞州丹弗斯 Rosewood Drive 222 号，01923；电话 (508) 750-8400。
美国国会图书馆出版物编目数据
Red Hat Linux administrator's handbook / Mohammad K. Reaz.
ISBN 0-7645-4637-6 (alk. paper)
1. Linux. 2. Operating systems (Computers) I. Title.
QA76.76.L593 R43 2000
005.4'469'dc21
00-045449 CIP

责任限制/免责声明。出版者和作者在编写本书时已尽最大努力。出版者和作者不对本书内容的准确性或完整性作出任何陈述或保证，并特别声明不提供任何明示或暗示的适销性或特定用途适用性的保证。本书中包含的描述之外没有其他保证。销售代表或书面销售材料不得创设或延长任何保证。作者和出版者不对任何利润损失或任何其他商业损害负责，包括但不限于特殊、偶然、间接或后果性损害。

商标：本书中使用的所有品牌名称和产品名称均为其各自所有者的商品名称、服务标记、商标或注册商标。IDG Books Worldwide 与本书中提及的任何产品或供应商无关。

![](img/c2419364ebb911c809b6a79991707c27_5_0.png)

![](img/c2419364ebb911c809b6a79991707c27_5_1.png)

## 关于 IDG Books Worldwide

欢迎来到 IDG Books Worldwide 的世界。

IDG Books Worldwide, Inc. 是 International Data Group 的子公司，International Data Group 是全球最大的信息技术提供商。IDG 由 Patrick J. McGovern 于 30 多年前创立，目前在全球拥有超过 90,000 名员工。IDG 在 75 多个国家出版超过 290 种计算机出版物。每月有超过 9,000 万人阅读一份或多份 IDG 出版物。

IDG Books Worldwide 于 1990 年创立，今天是美国最畅销计算机图书的第 1 号出版商。我们自豪地获得了计算机新闻协会颁发的八项编辑卓越奖，以及 Computer Currents 首届读者选择奖的三项大奖。我们的畅销书系 'For Dummies®' 系列已印刷超过 5,000 万册，翻译成 31 种语言。IDG Books Worldwide 通过与 IDG 的 Hi-Tech Beijing 的合资企业，成为第一家在中华人民共和国出版计算机图书的美国出版商。在短时间内，IDG Books Worldwide 已成为全球数百万希望学习如何更好地管理其业务的读者的首选。

我们的使命很简单。我们的每一本书都旨在为读者提供额外的价值和技能培养指导。我们的书籍由为读者办事的专家撰写。我们编辑团队的知识基础来自于出版、教育和新闻业多年的经验——我们利用这些经验制作书籍，引领我们进入新千年。简而言之，我们的书籍吸引了最优秀的人才。我们特别注重受众、内部设计、图形和插图的使用。通过合资企业，我们使用高效的电子撰写、编辑和桌面出版流程，我们可以花费更多时间确保卓越的内容，而花费更少时间在制作书籍的技术细节上。

您可以信赖我们的承诺，以具有竞争力的价格提供高质量的书籍，涵盖读者今天感兴趣的主题。在 IDG Books Worldwide，我们继续在 IDG 超过 30 年的优质传统中前行。您不会在任何主题上找到比 IDG Books Worldwide 更好的书籍。

John Kilcullen
董事长兼首席执行官
IDG Books Worldwide, Inc.

Steven Berkowitz
总裁兼出版人
IDG Books Worldwide, Inc.

![](img/c2419364ebb911c809b6a79991707c27_6_0.png)

IDG 是全球领先的 IT 媒体、研究和展览公司。成立于 1964 年。IDG 1997 年收入为 10.7 亿美元，全球员工超过 9,000 人。IDG 提供覆盖 79 个国家、占全球 IT 支出 95% 的 IT 买家的最广泛的媒体选择。IDG 的多元化产品和服务组合涵盖六大关键领域，包括印刷出版、在线出版、展览和会议、市场研究、教育和培训以及信息技术。IDG 拥有 60 种杂志和 290 种报纸，包括 IDG 的领先全球品牌——Computerworld、PC World、Network World、Macworld 和 Channel World 系列出版物。IDG Books Worldwide 是全球增长最快的计算机图书出版商之一，拥有 36 种语言的 700 多种图书。仅 'For Dummies®' 系列就已印刷超过 5,000 万册。IDG 通过万维网 (http://www.idgbooks.com) 为在线用户提供全球最大的技术特定网站网络，涵盖 55 个国家超过 225 个有针对性的网站。International Data Corporation (IDC) 是全球最大的信息技术数据、分析和咨询提供商，在 41 个国家拥有 700 名分析师，在 41 多个国家拥有 300 个研究中心，全球超过 400 名研究分析师。IDG World Expo 是在 35 个国家举办全球品牌会议和展览的领先生产商，包括 13 场 Computer Expo、Macworld Expo、ComNet、Windows World Expo、ICE Internet Commerce Expo、Agenda、DEMO 和 Spotlight。IDG 的培训子公司 ExecuTrain 是全球最大的计算机培训公司，在 36 个国家拥有 70 多个地点和 785 个培训中心。IDG Marketing Services 帮助领先的 IT 公司通过 IDG 在全球的印刷、在线和展览产品建立国际品牌认知度，开发全球一体化的营销计划。有关公司的更多信息，请访问 www.idg.com。
