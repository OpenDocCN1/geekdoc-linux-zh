
# Wordperfect Linux 入门指南

> “这本关于 LINUX 版 WordPerfect 的第一本书籍将改变 LINUX 的格局。” —— W. Wayne Liaw，专利律师（美国/加拿大）及长期 WordPerfect 用户

Stephen E. Harris 与 Erwin Zileman 著

Corel 总裁兼首席执行官 Michael Cowland 前言

Stephen E. Harris 与 Erwin Zijleman 著

邮信箱 9384

# 鸣谢

- 收购编辑：Andy Cummings
- 文案编辑：Eric Hahn、Corey Cohen、Marti Paul
- 开发编辑：Melanie Feinberg
- 制作：IDG Books Worldwide Production
- 技术编辑：Jason Grenier、W. Wayne Liauh、Philip Rackus
- 校对与索引：York Production Services

# 关于作者

**Stephen Harris** 是 QwScreen 的创始人兼总裁，这是一家专注于软件开发和咨询的公司，致力于让计算机屏幕变得更加友好。他是畅销书籍《WordPerfect 7 圣经》和《WordPerfect Suite 8 圣经》的作者。Steve 是 Corel Beta 测试小组的自豪成员。他与妻子 Githa 住在位于马萨诸塞州西部的森林里，他们还有三只猫（Tiger、Becky 和 Chester），以及熊、鹿、火鸡和其他各种野生动物相伴而居。你可以在 http://www.qwkscreen.com 找到 Steve 本人，以及更多 WordPerfect 解决方案和链接。

Erwin Zijman 的职业始于发展社会学，专门研究第三国家（尤其是东南亚）的城市社会学和教育。他现在担任软件科学家，专门从事 PC 办公应用。Erwin 曾担任微软、Borland 和 WP Corporation 产品的 Beta 测试员。目前，Erwin 专门为 Corel 工作。他住在阿姆斯特丹附近的莱登历史中心，与他的猫（Bagu）住在一起。

本书献给开源社区的每一个人，他们通过集体爱的劳动创造了奇迹。

# 前言

当我们去年 12 月在 CNET 上发布 Linux 版免费版 Corel WordPerfect 8 时，我们预感到会引发下载潮。

但我们得到的是如山倒海般的冲击——Linux 爱好者在最初 12 小时内就尝试了 82,925 次下载。随着我们将 Linux 版 WordPerfect 8 分发到网络上流行的镜像站点，用户争相着获取这款功能强大的文字处理器，它可以在不同应用程序和平台之间无缝地处理文档。Linux 版 WordPerfect 8 不仅一而而红——它成为了年度最大的软件发布物之一，截至目前下载次数已超过 900,000 次。

这一成功是对我们 Linux 策略的巨大肯定。我们证明了 Linux 社区希望使用像 WordPerfect 这样的商业主流应用，而我们打算提供这些服务。

正当我们对将 WordPerfect 8 带到 Linux 感到兴奋时，我们也非常高兴 Steve Harris 在 Erwin Zijelman 的专业协助下，正将他畅销的 WordPerfect 指南移植到 Linux 平台。《Linux 版 WordPerfect 圣经》充满了专家技巧和示例，为你提供了掌握 Linux 版 WordPerfect 所需的 100% 内容。

为了庆祝软件和书籍的双重发布，Corel 公司已与 IDG Books Worldwide 安排，将 Linux 版 WordPerfect 8 的完整个人版（Personal Edition）与《Linux 版 WordPerfect 圣经》装订在一起——你找不到更划算的交易了！

Corel WordPerfect 8 for Linux 个人版是一个理想的办公解决方案，提供了与 Windows 版本相同的惊人功能。使用阴影光标点击并输入。单击即可快速查找（QuickFind）。实时检查拼写和语法。使用宏实现自动化。瞬间格式化表格。自动创建超链接。Corel WordPerfect 8 for Linux 个人版可以在家里、学校和办公室释放你的全部生产力潜力。

无论你是 WordPerfect 的新手，还是转到 Linux 的资深专家，《Linux 版 WordPerfect 圣经》都是一份易于使用、易读的程序强大功能的指南。Steve 和 Erwin 将向你展示如何在 Linux 版 WordPerfect 中快速上手，然后揭示他们从创建备忘录、信函、报告到格式化、处理和打印文档的所有秘诀。在这本实操教程类参考书中，他们为你提供了清晰的、分步骤的说明和大量的插图。

欢迎使用 Linux 版 WordPerfect 8 个人版，欢迎阅读《Linux 版 WordPerfect 圣经》，我强烈推荐这两本书！

Mike Cowland，总裁兼首席执行官

Corel 公司

# 前言

软件行业变化极快！人们对使用 Linux 进行桌面应用程序的兴趣急剧增长。随着 Linux 版 WordPerfect 8 的突然成功（包括它在 LinuxWorld 大会上获得的“杀手级应用”奖），我们认为世界已经准备好接受第一本关于主流 Linux 应用的书了。

我们只需要从《Windows 版 WordPerfect 圣经》中提取说明，将 Windows 截图替换为 Linux 截图，然后发送出去即可。对吧？好吧，我们原本是这样想的，但事实并非那么简单。我们需要考虑各种桌面可能性、新的安装程序，以及书中足够的变体，这使得“翻译”到 Linux 的过程成为了一次既兴奋又有时让人头皮发麻的经历。

但它就在这里了！你手里拿着的是第一本致力于 Linux 桌面用户应用的书籍。此外，这本书的 CD 光盘包含了程序本身——Linux 版 WordPerfect 8 个人版。这是一项令人兴奋的业务！

如果写电脑书不是一门艺术，我们更倾向于认为它类似于手工艺或科学。我们的目标是以易于使用、易读的格式传递大量信息。我们希望你满意。

鼠标或其他指向设备是大多数 Windows 程序的必需品。书中处处使用了标准的鼠标操作：

如果您使用手写笔设备，“点击”将变为“轻点”；如果您使用左手鼠标设置，则“左”将变为“右”，反之亦然。（某些鼠标具有实现“单击”完成的功能，而另一些鼠标则需要“双击”。）

Linux 版 WordPerfect 具有由各种图标指示的特殊文本侧边栏：

在这个行业，变化是不断的。要获取最新的更新、修复和升级，请访问我的网站 www.example.com，您可以在那里找到许多技巧和额外材料（您还可以通过 www.example.com 获取讨论组链接、剪贴画来源以及许多资源）。任何意见、建议、批评或请求？请通过 steve@example.com 发送给我。我希望这本书有所帮助！

## 致谢

尽管任何不足都是我个人的责任，但这项巨大的工作必然是一个涉及出版商、设计师、校对员、索引员、排字员，以及推广和销售人员的团队。出版是一个令人兴奋的行业，但截止日期和细致要求也带来了压力。坦率地说，无法列出这一过程中的每个人，请允许我向这个辛勤团队的每一个人致以诚挚的谢意。我想特别提到 Melanie Feinberg，感谢书中精炼部分的编辑工作。特别感谢 Andy Cummings 听取我们的想法，并充满热情的加入其中。非常感谢 W. Wayne 在他忙碌的日程中抽空应用您的技术知识。这个项目的成功很大程度上归功于 Corel 专职人员慷慨且持续的支持。感谢 Mike Cowland 帮助启动该项目，感谢 Linux 开发团队的 Nicholas Bloom 和 Stephen Hill。对于我的合著者 Erwin Zielman，没有你，我无法言表我的感激。一如既往，我必须感谢我的律师/代理 Joel L. Hecker 律师，感谢他的明智建议和支持。最后，特别感谢我的妻子 Gita，她有幸阅读新章节的草稿并忍受我疯狂的日程。我们在休假准时完成了任务！

Steve Harris

- 光盘安装说明 ................................................681
- 什么是 Linux? ........................................................................................ 3
- 指定 WordPerfect 启动选项 ....................................................... 15
- 保护你的工作 ............................................................... 97
- 调整图形框的内部或外部间距 ... 164
- 开始印刷！ ................................................................................... 218
