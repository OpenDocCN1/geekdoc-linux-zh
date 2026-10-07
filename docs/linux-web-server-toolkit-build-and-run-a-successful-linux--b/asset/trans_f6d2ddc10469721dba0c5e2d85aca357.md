

# LINUXn Web 服务器工具包

![](img/e01f1106dd2902613fa07890c8baa7e6_0_0.png)

构建并运行基于 LINUX 的成功网站

- 规划
- 安装
- 服务器配置
- 网络连接
- 内容创建
- 管理
- 安全
- 灾难恢复

CD-ROM 包含：
- Caldera OpenLinux Lite Linux 发行版
- Apache Web 服务器
- 超过 1,000 个工具和程序

Nicholas Wells

# Linux® Web 服务器工具包

Nicholas Wells

IDG Books Worldwide, Inc.
国际数据集团（International Data Group）公司
加州福斯特市 ◆ 伊利诺伊州芝加哥 ◆ 印第安波利斯 ◆ 德克萨斯州南湖

# Linux® Web 服务器工具包

出版于
IDG Books Worldwide, Inc.
国际数据集团公司
919 Hillsdale, Suite 400
Foster City, CA 94404

www.idgbooks.com [IDG Books Worldwide 网站]

版权 © 1998 IDG Books Worldwide, Inc. 版权所有。未经出版者事先书面许可，本书的内容（包括内部设计、封面设计和图标）不得以任何形式通过任何方式（电子、复印、录制或其他）进行复制或传输。

美国国会图书馆目录号：97-77806

ISBN: 0-7645-3167-0

印于美国

1098765432

18/US/OSY/ZYC

由美国 IDG Books Worldwide, Inc. 分发
加拿大由 Macmillan Canada 分发；英国由 Transword Publishers Limited 分发；挪威由 IDG Norge Books 分发；瑞典由 IDG Books 分发；新西兰由 Woodland Enterprises Ltd. 分发；新加坡、马来西亚、泰国和印度尼西亚由 Longman Singapore Publishers Ltd. 分发；巴西由 Livraria Cuspe 分发；厄瓜多尔由 Edciencia S.A. 分发；墨西哥由 Addison-Wesley Publishing Inc. 分发；法国由 Nathan Publishing 分发；委内内瑞拉由 Contemporanea de Ediciones 分发；秘鲁由 Computer Book & Magazine Store 分发；加勒比和西印度群岛由 Express Publishers 分发。

有关美国 IDG 全球书籍的一般信息，请致电我们的客户服务部门 800-762-3774。更多信息（包括折扣和优质服务，请致电我们的客户服务部门 800-834-3422。

有关在美国境外购买 IDG Books Worldwide 书籍的信息，请联系我们的国际服务部门 650-655-3200 或传真至 650-655-3295。

有关语言翻译的信息，请联系我们的外语及子版权部门 650-655-3021 或 650-655-3281。

咨询批量采购的特殊定价，请联系我们的销售部门 650-655-3200 或致信至下方地址。

有关在课堂上使用 IDG Books Worldwide 书籍或订购考试副本的信息，请联系我们的教育支持部门 800-434-2066 或传真至 817-251-8174。

有关媒体评论稿副本、作者或其他信息，请联系我们的公共关系部门 650-655-3000 或 650-655-3299。

如需许可打印、个人或教育用途的复印物品，请联系许可中心（Clearance Center），222 River Street, Menlo Park, CA 94025，或传真至 978-750-4470。

> 责任限制/免责声明：作者和出版者在准备本书时已努力，IDG BOOKS WORLD, INC. 对本书的质量或完整性不作任何陈述或保证，并明确放弃任何关于畅销性或适用于特定用途的暗示保证。本段描述之外不提供任何其他保证。任何其他陈明的、口头的或书面说明均不构成或暗示保证。此处提供的信息的准确性和完整性以及此处述的观点不保证能产生任何特定结果，此处包含的策略可能不适用于每个人。IDG BOOKS WORLDWIDE, INC. 和作者均不对任何直接、间接、特殊或商业损害负责，包括但不限于偶然的、后果性的或其他损害。商标：本书中使用的所有品牌名称和产品名称均为其所有者的商品名称或注册商标。IDG Books Worldwide 与书中提到的任何供应商均无关联。

![](img/e01f1106dd2902613fa07890c8baa7e6_5.png)

# 关于 IDG 全球

IDG Books Worldwide, Inc. 是国际数据集团（International Data Group）的子公司，全球最大的计算机相关信息出版商，也是信息技术信息服务的领先全球提供商。IDG 成立于 25 多年前，在全球雇用了超过 8,500 名员工。IDG 在 45 个国家出版 275 多种计算机书籍（见下文）。每月有超过 6000 万人阅读 IDG 出版物。IDG Books Worldwide 出于 1990 年，如今是美国最畅销计算机书籍出版商。我们自豪地收到了来自计算机出版社协会（Computer Press Association）的八项优秀奖，以及三项年度读者选择奖。“自呆系列”（For Dummies）已以 30 种语言印刷了超过 3 亿份。IDG Books Worldwide 通过与 IDG 高科技北京的合资经营，成为首家进入中华人民共和国的美国出版商。以创性的速度，IDG Books Worldwide 已成为人们管理业务的首选。

我们的使命是确保我们的每本书都能带来额外价值。我们的书籍由理解并关心读者的专家编写。我们编辑团队的知识库源于出版、教育和新闻领域的多年经验——几十年来，我们利用经验制作书籍。当我们谈论书籍时，我们吸引了最优秀的人才。我们特别关注受众、内部设计、图标的使用和插图等细节。由于我们采用了高效的审核、编辑和出版书籍的方法，我们可以花费更多时间来确保优质内容，而减少在书籍制作技术细节上的时间。您可以信任我们的承诺，即以竞争性的价格提供您想阅读主题的高质量书籍。在 IDG Books Worldwide，我们继续传承 IDG 的传统。

> John Kilcullen
首席执行官
IDG Books Worldwide.

> Steven Berkowitz
总裁兼出版经理
IDG Books Worldwide, Inc.

![](img/e01f1106dd2902613fa07890c8baa7e6_6_0.png)
> Anne Hamilton
收购编辑

> 图形与制作
专家
> Ellen L. Dendy
> Kerrie Klein
> Maureen Moore
> E. A. Pauw

> 质量控制
专家

> 技术编辑
> Jim Freeman (James N.)
> Mark Schumann

> 插画师
> Pamela Drury Wattenmaker

> 拷贝编辑
> Gill Kent
> Carolyn Welch

> 校对
> Annie Sheldon

> 制作协调
> Susan Parini

> 索引编
> Richard Shrout

# 致谢

收购编辑
Anne Hamilton

图形与制作
专家

开发编辑
Ellen L. Dendy
Kerrie Klein
Maureen Moore
E. A. Pauw

质量控制
专家

技术编辑
Jim Freeman (James N.)
Mark Schumann

插画师
Pamela Drury Wattenmaker

拷贝编辑
Gill Kent
Carolyn Welch

校对
Annie Sheldon

制作协调
Susan Parini

索引编
Richard Shrout

# 翻译
奥地利, 丹麦, 芬兰, 德国, 希腊, 匈牙利, 冰兰, 香港, 印度, 以色列, 意大利, 日本, 韩国, 拉脱维亚, 立陶宛, 卢森堡, 马来西亚, 马尔他, 墨西哥, 摩纳哥, 荷兰, 挪威, 巴基斯坦, 新西兰, 波兰, 葡萄牙, 罗马尼亚, 南韩国, 俄罗斯, 西班牙, 新加坡, 沙特阿拉伯, 斯洛伐克, 斯洛文尼亚, 瑞典, 瑞士, 台湾, 泰国, 土耳其, 乌克兰, 美国, 乌根圭, 越南, 西德意志, 南斯拉维亚。
（注：此处为国家列表）

奥地利, 丹麦, 芬兰, 德国, 希腊, 匈牙利, 冰兰, 香港, 印度, 以色列, 意大利, 日本, 韩国, 拉脱维亚, 立陶宛, 卢森堡, 马来西亚, 马尔他, 墨西哥, 摩纳哥, 荷兰, 挪威, 巴基斯坦, 新西兰, 波兰, 葡萄牙, 罗马尼亚, 南韩国, 俄罗斯, 西班牙, 新加坡, 沙特阿拉伯, 斯洛伐克, 斯洛文尼亚, 瑞典, 瑞士, 台湾, 泰国, 土耳其, 乌克兰, 美国, 乌根圭, 越南, 西德意志, 南斯拉维亚。

# 关于作者

Nicholas D. Wells 管理 Caldera 的文档、培训和网站。Nick 曾为 Sytex 和网络专业人士杂志撰写 NetWare 文章，并广泛过 NetWare 安全。

在加入 Novell 之前，Nick 在 Novell 担任技术作家和编辑，并是 Corsair 团队的一员，该团队开始创建一个新的基于 Linux 的桌面操作系统。在加入 Novell 担任作家之前，Nick 开发了十年的教育软件和小型企业应用程序。

