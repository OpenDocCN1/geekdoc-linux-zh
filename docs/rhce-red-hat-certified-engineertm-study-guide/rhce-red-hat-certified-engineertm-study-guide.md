# RHCE：红帽认证工程师认证学习指南





- 副出版人：Jordan Gold
- 合同与许可经理：Kristine O'Callaghan
- 收购与开发编辑：Ellen L. Dendy
- 编辑：Julie Sakaue, Suzanne Goraj, Sarah Lemaire
- 制作编辑：Dennis Fitzgerald
- 技术编辑：Randolph Russell
- 书籍设计：Bill Gibson
- 图形插画师：Tony Jonick
- 电子出版专家：Susie Hendrickson, Judy Fung, Jill Niles
- 校对：Carol A. Burbo, Nanette Duffy, Mae Lum, Nathan Whiteside
- 索引编制：Ted Laux
- CD 协调员：Kara Eve Schwartz
- CD 技术员：Keith McNeil
- 封面设计：Archer Design
- 封面摄影：Tony Stone

## 软件许可协议：条款与条件

随本书附带的介质和/或任何在线材料包含目前可用或将来包含的程序和/或文本文件（简称“软件”），用于配合本书使用。SYBEX 特此授予您使用该软件的许可，但须遵守以下条款。您购买、接受或使用该软件即表示您接受上述条款。

除非另有说明，软件汇编是 SYBEX 的财产，并受 SYBEX 或介质文件中指明的其他版权所有者（简称“所有者”）的版权保护。特此授予您一项单用户许可，仅限将软件用于个人、非商业用途。未经 SYBEX 及本介质中所含任何组件软件的特定版权所有者的事先书面同意，您不得复制、转载、出售、分发、出版、传播或商业利用该软件或其任何部分。

如果软件或组件包含特定的许可协议或最终用户许可协议、条款条件、免责声明、限制或保证（简称“最终用户许可”），则这些最终用户许可在涉及该特定软件组件时将取代本协议的条款和条件。您购买、接受或使用该软件将构成您对该等最终用户许可的接受。

通过购买、使用或接受该软件，您进一步同意遵守美国的所有出口法律法规以及不时可能存在的其他法律法规。

## 软件支持

补充软件的组件及其相关优惠可能由该材料的特定软件所有者提供支持，但 SYBEX 可能不提供支持。有关任何可用支持的信息，可以通过适当的 read-me 文件中提供的信息或介质上列出的其他信息从所有者处获得。

如果制造商或其他所有者停止提供支持或拒绝履行任何保证，SYBEX 不承担此责任。关于软件支持的通知仅供您参考。SYBEX 不是所有者的代理人或委托人，SYBEX 在任何情况下均不负责为软件提供任何支持，也不对所有者提供或未提供任何支持承担法律责任。

## 保证

SYBEX 保证所附介质在购买后九十 (90) 天内无物理缺陷。除随书附带或发布在 www.sybex.com 上的形式或介质外，SYBEX 不提供该软件的其他形式或介质。如果您在此保证期内发现介质缺陷，可以通过将缺陷介质（预付邮资）连同购买证明发送至以下地址，免费获得相同格式的替换件：

SYBEX Inc.
Customer Service Department
1151 Marina Village Parkway
Alameda, CA 94501
(510) 523-8233
Fax: (510) 523-2373
e-mail: info@sybex.com
WEB: HTTP://WWW.SYBEX.COM

90 天期限过后，在提供缺陷磁盘、购买证明以及支付给 SYBEX 的 10 美元支票或汇票的情况下，您可以获得内容相同的替换介质。

## 免责声明

SYBEX 对软件及其内容、质量、性能、适销性或针对特定用途的适用性不作任何明示或暗示的保证或陈述。在任何情况下，SYBEX 及其贡献者、员工、代理或被许可人均不对您或任何其他方因使用或无法使用软件及其内容而导致的直接、间接、特殊、偶然、后果性或其他损害承担责任，即使已被告知发生此类损害的可能性。如果软件包含更新功能，SYBEX 进一步声明，除了初始发布外，不对在任何特定期限内提供此功能承担任何义务。

某些州不允许排除暗示保证。因此，上述排除条款可能不适用于您。本保证为您提供特定的法律权利；您可能还拥有随州而异的其他权利。购买随附软件的本书反映了本条款与条件协议中所包含的所有风险协议和责任限制。

## 共享软件分发

本软件可能包含作为共享软件分发的各种程序。版权法同时适用于共享软件和普通商业软件，版权所有者保留所有权利。如果您试用了共享软件程序并继续使用，则应对其进行注册。不同程序的试用期、注册和付款细节有所不同。请遵守相关文件中的要求。

## 复制保护

软件的全部或部分可能已获得版权保护或加密，也可能没有。但在任何情况下，未经授权转售或重新分发这些文件均被明确禁止，除非所有者在此特别规定。



## 致谢

这是我的第十本书，而我仍然觉得写致谢是写书过程中最困难的部分。这让人倍感挫败，因为致谢部分很少有人阅读，或者至少在我看来是这样。你看，我白天是一名教师，我发现我的学生对我不在场时购买的书中包含的致谢内容几乎没什么意识，也很少关注。也许虚构作品中的致谢会有更好的待遇，但我内心那个悲观的人对此表示怀疑。我不明白为什么会这样，因为我是那种会一直盯着电影演职员表看，直到看到版权符号出现的人。好吧，说实话，当看到制作会计的名字出现时，我经常会跳过，但那已经很接近结尾了，不是吗？

尽管致谢周围笼罩着这种被忽视的阴谋，但我必须坚持认为它们很重要。是的，我承认不太可能有人是因为阅读了致谢而购买书籍。而且，这似乎表明致谢不如书的核心内容重要。但事实并非如此。

毕竟，书是由人创造并为人们服务的：重要的是人，而不是书。而在致谢部分，我有机会偿还许多参与本书工作的人们的情分。在电影中，许多人有时会在演职员表中占据显眼的位置——通常在电影标题之上——包括制片人、导演、男演员和女演员。但在出版业，书的封面通常只包含出版公司和作者的名字。（天哪，这么一想，我还没见过这本书的封面：我只是假设我的名字会在封面上。）

这完全不对，我想给你一个帮助改变它的机会：我想请你复印这一页——不要撕下来或做其他粗鲁的事——然后把它贴在你的这本书的封面上。结果可能在视觉上不够美观，但当我想到这次为了本书的演职员而发起的对抗匿名的微小反叛时，我的精神为之振奋。

现在，我最好快点进入正题，否则所有这些人的名字都会出现在这一页的背面，那样会破坏整个构思，不是吗？让我们从文学经纪人 Margot Maley-Hutchison（把她看作制片人）和收购与开发编辑 Ellen Dendy（把她看作导演）开始。然后是技术编辑 Randy Russell 和 Utilman（把他们看作将我那无法拍成电影的小说改编成剧本的编剧，因为这大约能体现他们贡献的巨大程度）以及技术编辑协调员 Ellen Bliss（把她看作有智慧选择 Randy 和 Utilman 来写剧本的编剧经理）。主演包括制作编辑 Dennis Fitzgerald（把他看作今年的最佳男主角）；编辑 Julie Sakaue（把她看作今年的最佳女主角）；以及编辑 Sarah Lemaire 和 Suzanne Goraj（把她们看作今年的最佳女配角）。这些人每一个人都配得上一座奥斯卡奖杯——或者两座——仅仅是因为他们忍受了我的古怪、日益衰退的记忆力以及对细节的忽视。

另外几位没有直接参与本书工作的人也值得特别提及。我的家庭团队——Jennifer, Patrick 和 Sara——现在似乎已经习惯了我的写书习惯。感谢他们在我就职于写作爱好期间，帮我处理账单、搬动家具和操持家务。最后，我郑重地感谢我的主和救主耶酥基督，祂比任何人都更了解我的许多缺陷和弱点，但仍然耐心地包容我，因为祂知道——虽然我不知道怎么做——祂仍然能让我变得卓越。我迫不及待了！

## 介绍

像 Linux 社区的许多人一样，你可能听说过红帽认证工程师 (RHCE) 计划以及相关的 RHCE 考试，这两者均由 Red Hat, Inc. 创建。你可能听说过 RHCE 考试具有挑战性，或者听说它并不难。你可能听说过该考试专注于 Red Hat Linux，且 Unix 或除 Red Hat Linux 以外的 Linux 发行版的知识对你通过考试没有帮助。最重要的是，你可能在想 RHCE 认证如何能提升你的职业生涯，或者如果你是一名招聘经理，RHCE 认证是否能帮你找到合格的员工。我写这本书就是为了回答这些及类似的问题，并提供全面的材料和练习，旨在帮助你准备并通过 RHCE 考试。

### 这本书适合你吗？

如果你想学习如何管理 Red Hat Linux 系统，那么这本书就是为你准备的。在书中，你会找到关于你需要理解的概念以及你需要能够执行的步骤的清晰且全面的解释。

如果你计划参加 RHCE 考试，你会发现这本书更有价值，因为它专注于 Red Hat, Inc. 认定的 RHCE 考试核心主题。书中包含许多练习题和练习，将帮助你准备并评估你参加 RHCE 考试的就绪程度。书中同时包含问题和练习，因为 RHCE 考试有两种测试：笔试和基于性能的实操考试。问题部分为你准备 RHCE 考试的笔试部分，而练习部分则为你准备实操部分。一旦你掌握了这些问题和练习，你将能够充满自信地面对 RHCE 考试。

然而，RHCE 考试和这本书并非适合所有人。RHCE 考试主要是一项动手操作考试，旨在评估你的系统管理技能。本书将帮助你学习并精炼这些技能，但除非你具有一些 Unix 或 Linux 经验，否则你可能无法在很大程度上理解本书或 RHCE 考试。为了取得成功，你不需要成为 Unix 或 Linux 专家——当然，如果你是专家当然没有坏处——但你至少应该是一个在系统安装和管理方面有一定经验的 Unix 或 Linux 高级用户。如果你已经在多个系统上安装过 Linux，并花时间研究了一些系统管理命令（如 `mount` 和 `umount`），那么你可以期待能够理解本书的内容。

## 本书涵盖的内容？

我尽力涵盖了对 Red Hat Linux 系统管理员重要的每一个主题，特别是强调了那些可能出现在 RHCE 考试中的主题。我必须写成 *尽力涵盖*，因为像我一样参加过 RHCE 考试的人受保密协议的约束，不能泄露考试内容。此外，Red Hat, Inc. 会定期用新的问题和练习更新 RHCE 考试。因此，任何 RHCE 考试的学习计划都不能且无法替代真正的知识。但是，本书可以帮助你培养通过 RHCE 考试所需的恰好那种类型和程度的真实知识。涵盖的核心主题包括以下内容：

- RHCE 认证和 RHCE 考试
- PC 硬件、Unix 和网络回顾，帮助你填补已有知识的空白
- Red Hat Linux 安装
- Red Hat Linux 系统和网络管理
- 网络服务器管理
- X Window 系统管理
- Red Hat Linux 安全管理
- 系统故障排除和修复

在撰写本书时，Red Hat, Inc. 刚刚发布了 Red Hat Linux 6.2，并正在更新 RHCE 考试以反映 Red Hat Linux 6.2 的新特性和变更特性。因此，本书是基于 Red Hat Linux 6.2 以及针对 Red Hat Linux 6.2 的 RHCE 考试而编写的。

**注意：** 如果你通过了 RHCE 考试，你的认证在一年内保持有效，无论期间发布了哪个新版本的 Red Hat Linux。

## 如何参加 RHCE 考试？

RHCE 考试测试你对 Red Hat Linux 系统管理任务的概念理解和执行技能。考试大约需要七个小时，包括一小时的午休。考试具有挑战性：目前大约每三个考生中就有一个未能通过。然而，适当的准备可以显著增加你成功的可能性。

Red Hat, Inc. 大约每月在其北卡罗来纳州达勒姆总部举行一次 RHCE 考试，在加利福尼亚州圣克拉拉设施举行的次数较少。在撰写本书时，Red Hat, Inc. 刚刚宣布很快将在欧洲和东亚提供 RHCE 考试。RHCE 考试还由 Red Hat, Inc. 的培训合作伙伴（包括 Global Knowledge 和 IBM Global Services）在其他几个城市提供。

你可以参加 RHCE 考试，或者参加一个特殊的四天 RHCE 考试准备课程（其价格包含次日进行的考试）。在撰写本书时的 Red Hat, Inc. 课程编号和费用如下：

- **仅 RHCE 考试**：RH302 ($749)
- **RHCE 考试及准备课程**：RH300 ($2,498)

要注册由 Red Hat, Inc. 在美国地点提供的 RHCE 考试或 RHCE 考试准备课程，请致电 (800) 454-5502 或发送电子邮件至 `training@redhat.com`。同时，请查看以下网站获取最新细节和额外的注册信息：

- **Red Hat, Inc.**：`www.redhat.com/services/training/training.html`
- **Global Knowledge**：`db.globalknowledge.com/olm/go.asp?find=redhat`
- **IBM Global Services**：`www.ibm.com/services/learning/spotlight/linux.html`

**注意：** 第 1 章“红帽认证”和第 31 章“RHCE 考试”提供了关于 RHCE 认证和 RHCE 考试的更多信息。



## 如何使用本书

本书包含相当多的章节——准确地说是 31 章。大多数章节都较为简短且重点突出，以便您可以快速查找和复习相关主题。短章节还有助于您掌控学习进度，从而避免产生倦怠感。少数章节（例如关于安装 Red Hat Linux 的章节）比大多数章节要长，但通常其长度是因为包含了大量屏幕截图，这些截图将帮助您在执行该章节解释的步骤时不会迷失方向。因此，即使是较长的章节，您可能也不会觉得过于疲劳。

> 请务必阅读本书的扉页，其中讨论了配套 CD 的内容。

由于章节较短，本书被组织成若干部分，将相关的章节分在一起：

- **第一部分：背景** 第 1-5 章解释了 RHCE 认证，并复习了关于 PC 硬件、Unix、TCP/IP 网络和 Linux 的基础材料。您可能已经熟悉其中大部分内容，因此可以随意浏览这些章节，仅将它们用于填补记忆和理解中的空白。
- **第二部分：安装** 第 6-8 章描述了安装 Red Hat Linux 的步骤，包括安装前规划和高级安装技术。
- **第三部分：配置与管理** 第 9-20 章描述并解释了 Red Hat Linux 的系统管理，包括用户账户、磁盘配额和 RPM 软件包等主题。
- **第四部分：网络服务管理** 第 21-25 章描述并解释了网络服务的管理。其中包含关于 Apache、NFS、Squid 以及各种其他服务器的材料，此外还有关于网络安全和系统日志的内容。
- **第五部分：X Window 系统管理** 第 26-28 章涉及 X Window 系统，即 Unix 标准的图形用户界面。
- **第六部分：网络管理** 第 29 和 30 章涵盖路由器和防火墙。
- **第七部分：RHCE 考试 (RH302)** 第 31 章详细描述了 RHCE 考试，并为在考试中取得好成绩提供建议。

# 附录 A

附录 A 是一套练习考试，供您在准备 RHCE 考试时使用。

仅仅阅读——或者更糟糕的是，随意浏览——本书不足以让您为 RHCE 考试做好准备。相反，您应该遵循一个有条理、有组织的过程，例如：

1. 进行评估测试，以确定您擅长的领域以及需要花更多时间学习的领域。努力从错误和成功中共同学习。
2. 学习一个章节。顺便提一下，学习不仅仅是阅读；它还包括与文本互动、向自己提问，以及通过探究来发现所读内容的后果。
3. 完成章节中的练习。请记住，RHCE 考试要求您证明自己的技能，而技能只能通过实践获得，而非通过教条。这些练习可能是您能找到的最接近真实 RHCE 考试的体验。如果您计划通过考试，它们非常值得去做。
4. 回答章节末尾的复习题。这些问题与 RHCE 考试的笔试部分体验非常相似。
5. 复习与任何错题相关的章节主题。确保您知道正确答案以及为什么其他选项是错误的。
6. 以这种方式逐章学习，完成整本书。
7. 当您认为准备就绪时，参加附录 A 中的练习考试，然后评估您的表现。
8. 参加 CD 中包含的奖励考试，进一步测试您对实战的准备情况。如果您表现良好，请根据个人喜好报名参加 RHCE 考试或 RHCE 准备课程。如果您表现不佳，请重复步骤 1-8，直到您能够自信地通过练习考试。
9. 使用本书配套 CD 上的 Flashcard（闪卡）问题，在等待 RHCE 考试期间保持敏锐的状态。

## 评估测试

1. 哪个 `/etc/conf.modules` 行指定要保留默认模块路径信息？
    A. default-path
    B. hold
    C. keep
    D. retain

2. 以下哪些是 Linux 操作系统的组成部分？
    A. 最初由 Linus Torvalds 创建的内核
    B. GNU 工具和程序
    C. MINIX 工具和程序
    D. Unix 工具和程序

3. 以下哪个协议是一种流行的外部协议？
    A. BGP-4
    B. EGP
    C. OSPF-2
    D. RIP-2

4. 要检查本地主机访问运行在 server 上的 X 服务器的权限，应执行以下哪个命令？
    A. export DISPLAY=server:0.0
       xhost
    B. export DISPLAY=server:0.0
       xhost +
    C. export DISPLAY=server:0.0
       xhosts
    D. export DISPLAY=server:0.0
       xhosts +

6. 以下哪个运行级别对应于没有网络的多用户操作？
    A. 1
    B. 2
    C. 3
    D. 4

7. 以下哪个程序用于转换为 MD5 密码加密？
    A. md5conv
    B. md5unconv
    C. pwconv
    D. 以上都不是

8. 以下哪个命令正确地创建了用于系统启动时的初始 ramdisk？
    A. mkinitrd /boot/initrd-version
    B. mkinitrd /boot/initrd-version version
    C. mkinitrd /boot/initrd-version.img
    D. mkinitrd /boot/initrd-version.img version

9. 哪些以下文件系统类型支持配额（Quotas）？
    A. dos
    B. ext2
    C. iso9660
    D. vfat

10. 以下哪个文件指定了用户的窗口管理器？
    A. ~/.wm_style
    B. ~/.wmanager
    C. ~/.Xclients
    D. ~/.Xsession

11. 以下哪些是 Red Hat Linux 的安装类型？
    A. Expert
    B. Graphical
    C. Text
    D. Upgrade

12. 以下哪个命令激活用户配额？
    A. quotaon -a
    B. quotaon -ag
    C. quotaon -au
    D. quotaon -aug

13. 以下哪个操作应该首先执行？
    A. 创建配额文件。
    B. 设置默认配额。
    C. 设置个人配额。
    D. 开启配额。

14. 与 SMTP 协议关联的端口号是多少？
    A. 22
    B. 25
    C. 50
    D. 110

15. 要确定 Linux 内核是否支持防火墙，您应该检查以下哪个文件的存在？
    A. /proc/net/ip_always_defrag
    B. /proc/net/ip_fwchains
    C. /proc/sys/net/ipv4/ip_always_defrag
    D. /proc/sys/net/ipv4/ip_fwchains

16. 要伪装（masquerade）来自本地受保护网络的数据包，应指定以下哪个 `ipchains` 命令？
    A. `ipchains -A forward -i eth0 \ -s 192.168.1.0/24 -j MASQ`
    B. `ipchains -A input -i eth0 \ -s 192.168.1.0/24 -j MASQ`
    C. `ipchains -A local -i eth0 \ -s 192.168.1.0/24 -j MASQ`
    D. `ipchains -A output -i eth0 \ -s 192.168.1.0/24 -j MASQ`

17. 以下哪个与 24 位的网络地址相关？
    A. 网络地址 192.168.1.0/8
    B. 网络地址 192.168.1.0/24
    C. 子网掩码为 255.0.0.0 的 IP 地址
    D. 子网掩码为 255.255.255.0 的 IP 地址

18. 以下哪个目录包含 ping 命令？
    A. /bin
    B. /sbin
    C. /usr/bin
    D. /usr/sbin

19. 与 Linux 版本 2.2.15 相关的模块可能驻留在哪里？
    A. /lib/2.2.15
    B. /lib/modules/2.2.15-2
    C. /modules/2.2.15
    D. /modules/2.2.15-2

20. 以下哪个是 rc.sysinit 执行的最后一步操作？
    A. 激活交换分区。
    B. 加载键映射（keymap）。
    C. 设置日志级别。
    D. 存储启动消息。

21. 以下哪个日志配置文件条目将记录优先级为 critical 的 FTP 登录相关消息？
    A. auth.alert: /var/log/messages
    B. auth.err: /var/log/messages
    C. auth.info: /var/log/messages
    D. auth.*: /var/log/messages

22. 以下哪个键序列将键盘和视频系统从虚拟控制台切换到 X？
    A. Ctrl+Alt+F1
    B. Ctrl+Alt+F3
    C. Ctrl+Alt+F7
    D. Ctrl+Alt+F8

23. 要指定 gpm 服务应在运行级别 3 下执行，应执行哪个命令？
    A. chkconfig --level 3 gpm
    B. chkconfig --level 3 gpm on
    C. chkconfig --levels 3 gpm
    D. chkconfig --levels 3 gpm on

24. 要以读写模式重新挂载根文件系统，应执行以下哪个命令？
    A. mount -t ext2 /dev/hda1 / -o defaults,ro
    B. mount -t ext2 /dev/hda1 / -o defaults,rw
    C. mount -t ext2 /dev/hda1 / -o defaults,remount,ro
    D. mount -t ext2 /dev/hda1 / -o defaults,remount,rw

25. 以下哪个命令将停止系统？
    A. init 0
    B. halt
    C. shutdown -h now
    D. telinit 0



26. 以下哪一项允许您在 Linux 下运行 Windows 9x？

A. 您可以将系统配置为多启动操作。
B. 您可以安装 LILO。
C. 您可以安装 VMware。
D. 您可以安装 WINE。

27. 以下哪个时间规格定义了一个在奇数月份的第一天晚上 8:00 执行的 cron 任务？

A. 0 20 1 1-9/2,11 *
B. 0 20 1 1-11/2 *
C. 0 20 1 1,3,5,7,9,111 *
D. 0 20 1 jan,mar,may,jul,sep,nov *

28. 当您修改 `/etc/crontab` 文件时，会发生以下哪种情况？

A. cron 立即识别更改
B. 您必须重启系统
C. 您必须执行 `touch` 命令以更新 `/var/spool/cron` 目录的修改时间
D. 您必须重启 cron 系统

29. 以下哪类用户登录后会收到 shell 提示符？

A. 普通用户
B. POP 用户
C. PPP 用户
D. SLIP 用户

30. 以下哪个文件建立了用户的路径（path）？

A. /etc/bashrc
B. /etc/profile
C. ~/.bashrc
D. ~/.bash_profile

31. 以下哪项正确地将虚拟控制台与其安装程序功能配对？

A. 2, shell 提示符
B. 3, 安装程序消息
C. 4, 系统消息
D. 5, 其他消息

32. 安装程序使用哪个程序来配置 X？

A. Xcfg
B. Xconfig
C. Xconfigurator
D. Xconfiguration

33. 以下哪些是必须存在的 Apache 配置文件？

A. access.conf
B. httpd.conf
C. modules.conf
D. srm.conf

34. 要在没有初始进程的情况下以单用户模式启动系统，在响应启动提示时应输入什么？

A. linux
B. linux emergency
C. linux s
D. linux single

35. 以下哪个程序不是 PAM 感知的（PAM-aware）？

A. ftp
B. login
C. rlogin
D. telnet

36. 为了允许客户端主机远程访问打印机，可以将客户端主机列在：

A. /etc/hosts
B. /etc/hosts.equiv
C. /etc/hosts.lpd
D. /etc/printcap

37. 以下哪个选项正确指定了编译后的 Linux 内核位置？

A. /usr/src/linux/arch/i386/boot/bzImage
B. /usr/src/linux/arch/i386/boot/kernel
C. /usr/src/linux/arch/i386/boot/vmlinux
D. /usr/src/linux/arch/i386/boot/vmlinuz

38. 要指定所有者组的成员可以读取文件数据，您应输入哪个命令？

A. chmod 727 data
B. chmod 717 data
C. chmod g+r data
D. chmod uo+r data

39. LILO 提示符 `LIL` 表示什么？

A. LILO 第一阶段已加载。
B. LILO 第二阶段已加载。
C. LILO 第二阶段已启动。
D. LILO 第三阶段已加载。

40. 要更新共享库配置，您必须执行以下哪个命令？

A. ld
B. ld.so
C. ldconfig
D. ldd

41. 标准救援模式（rescue mode）的补充命令集中包含以下哪个命令？

A. kill
B. pico
C. sync
D. vi

42. 关于 Red Hat Linux 文本模式安装过程，以下哪项是正确的？

A. 对于初学者来说，它比图形模式安装过程更容易使用。
B. 它比图形模式安装过程更快。
C. 它比图形模式安装过程更可靠。
D. 它比图形模式安装过程需要的系统资源（如 RAM）更少。

43. 以下哪些是禁用动态路由的方法？

A. echo "0" > /proc/sys/net/ipv4/dynamic_routing
B. 编辑 /etc/sysconfig/network-scripts
C. linuxconf Gated Daemon 界面
D. linuxconf Routed Daemon 界面

44. 要指定与 NetWare 共享相对应的文件系统类型，请使用：

A. ipx
B. ncp
C. ncpfs
D. netware

45. 在安装过程中，选择要安装的软件包的通常最佳方法是：

A. 选择 Everything 选项。
B. 安装完成后再安装软件包。
C. 选择所需的组件。
D. 选择所需的软件包。

46. 动态加载器的缓存驻留在以下哪个文件中？

A. /etc/ld.so.cache
B. /etc/ld.so.conf
C. /lib/ld.so.cache
D. /lib/ld.so.cache

47. 若要尽可能地非交互式地使用 Xconfigurator，您应该使用哪个标志调用程序？

A. --auto
B. --expert
C. --kickstart
D. --probe

48. 运行以下哪个工具可能会损坏显示器？

A. SuperProbe
B. xf86config
C. xinitrc
D. xvidtune

49. 要配置 XDM 为任何请求主机提供一个包含 server1 和 server2 的选择器，应指定哪个 CHOOSER 指令？

A. * CHOOSER server1 server2
B. server1 server2 CHOOSER *
C. ALL CHOOSER server1 server2
D. server1 server2 CHOOSER ALL

50. 构建 Linux 内核的命令是以下哪个？

A. make clean bzImage modules
B. make clean dep bzImage modules
C. make dep bzImage modules
D. make dep clean bzImage modules

## 评估测试答案

1. C. `keep` 行指定 `/etc/conf.modules` 中的路径信息是对默认信息的补充。详情请参阅第 17 章。

2. A, B. Linux（有时被称为 GNU/Linux）是 Torvalds 的内核与 GNU 实用程序及程序的结合。详情请参阅第 5 章。

3. A. OSPF-2 和 RIP-2 是内部路由协议。EGP 已经不再流行。详情请参阅第 29 章。

4. A. 在没有参数的情况下，`xhost` 命令可以在客户端或服务器上运行。详情请参阅第 28 章。

5. A. `timeconfig` 程序用于配置时区。详情请参阅第 9 章。

6. B. 运行级别 1 是单用户模式。运行级别 3 是带有网络功能的多用户模式。运行级别 4 基本上与运行级别 3 相同。详情请参阅第 9 章。

7. D. 您无法方便地转换为 MD5 密码加密；必须在安装期间指定。详情请参阅第 9 章。

8. D. 您应该指定 `.img` 扩展名、内核版本和额外版本代码。详情请参阅第 18 章。

9. B. 只有 ext2 文件系统支持磁盘配额。详情请参阅第 11 章。

10. A. `~/.Xclients-default` 脚本会检查 `~/.wm_style` 文件的内容。详情请参阅第 27 章。

11. D. Upgrade（升级）是一种安装类型；其他选项是安装模式。详情请参阅第 7 章。

12. A, C, D. `-a` 选项激活用户和组配额，除非给出了 `-g` 或 `-u`，在这种情况下它仅激活指定的配额类型。详情请参阅第 11 章。

13. A. 在设置或开启配额之前，必须先创建配额文件。详情请参阅第 11 章。

14. B. SMTP 协议使用端口 25。详情请参阅第 21 章。

15. B. `ip_fwchains` 的存在表明支持防火墙；在提供防火墙的系统上应启用 `ip_always_defrag` 选项。详情请参阅第 30 章。

16. A. 要对本地网络进行伪装（masquerade），请将适当的规则附加到 forward 链。详情请参阅第 30 章。

17. B, D. IP 地址 192.168.1.0/24 具有 24 位网络地址和 8 位主机地址。掩码 255.255.255.0 有 24 个 1，表示 24 位网络地址。详情请参阅第 4 章。

18. A. `ping` 命令有时由普通用户执行，因此必须驻留在 `/bin` 而不是 `/sbin` 中。它是一个基本的故障排除工具，因此驻留在 `/bin` 而不是 `/usr/bin` 中。更多信息请参阅第 13 章。

19. B. 模块驻留在 `/lib/modules` 的子目录中，并以与其关联的内核版本和构建版本命名。更多信息请参阅第 13 章。

20. D. 启动消息被存储为最后一次操作，这样就不会丢失任何消息。详情请参阅第 14 章。

21. B, C, D. `crit` 优先级高于 `err` 和 `info`，但低于 `alert`。`*` 优先级匹配所有消息优先级。详情请参阅第 24 章。

22. C. 虚拟控制台 7 与 X 关联。详情请参阅第 27 章。

23. B. 该标志是 `level` 而不是 `levels`，并且需要 `on` 参数。详情请参阅第 14 章。

24. D. `remount` 选项允许您重新挂载已挂载的文件系统。更多信息请参阅第 15 章。

25. A, B, C, D. 任何一个替代方案都可行。更多信息请参阅第 15 章。



26. C. 只有 VMware 允许你在 Linux 下运行 Windows 9x。WINE 仅允许你运行某些 Windows 应用程序。更多信息请参阅第 8 章。

27. A, B, C. 你不能指定日期或月份的名称列表。更多信息请参阅第 16 章。

28. A. cron 系统会跟踪 `/etc/crontab` 文件的修改时间，并知道该文件何时被更改。更多信息请参阅第 16 章。

29. A, C, D. Pop 用户仅访问 POP 服务器；他们不需要关联的命令解释器，因为他们不会接收 shell 提示符。更多信息请参阅第 10 章。

30. B, D. 请参阅本章中提供的列表和描述，以验证 `/etc/bashrc` 和 `~/.bashrc` 文件设置了路径。更多信息请参阅第 10 章。

31. A, B, C, D. 表 7.1 总结了安装程序对虚拟控制台的使用。更多信息请参阅第 7 章。

32. C. 安装程序使用 `Xconfigurator` 来配置 X。更多信息请参阅第 7 章。

33. B. 仅 `httpd.conf` 文件必须存在。更多信息请参阅第 21 章。

34. B. 响应 `linux emergency`、`linux s` 和 `linux single` 都会以单用户模式启动系统。但只有 `linux emergency` 会省略 initl 进程。更多信息请参阅第 20 章。

35. D. `telnet` 程序不需要（且事实也并非）感知 PAM，因为它调用感知 PAM 的 `login` 程序来建立登录会话。更多信息请参阅第 22 章。

36. B, C. 如果远程主机与本地主机处于相同的管理控制之下，则可以将远程主机列在 `/etc/hosts.equiv` 中；否则，应将其列在 `/etc/hosts.lpd` 中。主机名必须是可解析的，但主机不需要列在 `/etc/hosts` 中；例如，主机名可以通过 DNS 或 NIS 解析。更多信息请参阅第 23 章。

37. A. 编译后的 Linux 内核被放置在 `/usr/src/linux/arch/i386/boot/bzImage`。更多信息请参阅第 17 章。

38. C. 命令 `chmod g+r` 为所有组的成员启用读取权限。更多详情请参阅第 3 章。

39. A, B, C. LILO 没有第三阶段。LILO 提示符表示在执行第二阶段期间出现问题。更多信息请参阅第 8 章。

40. C. `ldconfig` 命令重建加载器的共享库缓存。更多信息请参阅第 19 章。

41. B, C. 在标准救援模式环境下，`kill` 和 `vi` 都不可用。更多信息请参阅第 20 章。

42. B, C, D. 图形模式安装过程通常对初学者更易用，但需要更多资源，因此运行速度可能不如文本模式安装过程，特别是在 RAM 有限的系统上。文本模式安装过程更有可能从问题中恢复，且需要的系统资源较少。更多信息请参阅第 6 章。

43. D. `/proc` 文件系统不提供禁用 gated 的选项，且 `/etc/sysconfig/network-scripts` 是一个目录而非文件。更多信息请参阅第 29 章。

44. B, C. 虽然文件系统类型报告为 `ncpfs`，但可以指定为 `ncp` 或 `ncpfs`。更多信息请参阅第 23 章。

45. C. 通常最好指定所需的组件。选择 Everything 会安装不需要的软件包，而选择单个软件包又太繁琐。更多信息请参阅第 6 章。

46. A. 缓存文件是 `/etc/ld.so.cache`；配置文件是 `/etc/ld.so.conf`。更多信息请参阅第 19 章。

47. C. `--kickstart` 标志在可能的情况下指定非交互式操作。`--expert` 标志允许你覆盖探测到的信息。更多信息请参阅第 26 章。

48. B, D. `xvidtune` 和 `xf86config` 工具允许你设置可能损坏显示器的无效运行特性。在 `xf86config` 的情况下，任何损坏都会在工具运行后发生，因为该工具本身仅在文本模式下运行。更多信息请参阅第 26 章。

49. A. 你可以使用通配符来指定客户端主机。服务器在 CHOOSER 关键字之后指定。更多信息请参阅第 28 章。

50. B, D. `clean` 参数删除之前构建的结果，`dep` 参数传播配置信息。两者可以先后发生；且两者都应在 `bzImage` 之前。选项 A 未能通过源代码树传播配置，选项 C 未能删除之前构建的结果。在特殊情况下 A 或 C 可能会奏效，但通常你应该使用 B 或 D 中给出的命令。更多信息请参阅第 18 章。

## 背景

# 第一部分

# 第 1 章：红帽认证

**本章涵盖的 RHCE 准备主题：**

- 了解并理解认证的益处。
- 了解并理解成为红帽认证工程师（RHCE）的意义。
- 了解并理解 RHCE 认证流程。
- 了解并理解红帽认证课程的内容。
- 了解并理解 RHCE 考试的总体结构和内容。
- 评估你对 RHCE 考试的准备情况。
-制定通过 RHCE 考试的策略。

虽然 *Red Hat Certified Engineer* (RHCE) 考试不包含本章所呈现材料的相关问题，但它是本书中最重要的章节。在这里，你将了解认证，特别是红帽认证。你将了解在通往红帽认证之路上必须采取的步骤和可用选项。你将学习如何评估自己是否准备好参加 RHCE 考试。此外，你还将学习如何制定通过 RHCE 考试的策略。

## 红帽认证工程师

本节介绍 *RHCE* 认证。它简要描述了 *Linux*、*Red Hat, Inc.* (Red Hat) 和 Red Hat Linux。RHCE 认证非常重要，因为 Linux 是最强大且最流行的互联网操作系统之一，而 Red Hat Linux 是美国领先的 Linux 发行版。因此，RHCE 的需求量很大。

### Linux

Linux 是一个操作系统，是一个提供标准环境以运行应用程序软件的程序，它与 *Unix* 密切相关，后者是 20 世纪 70 年代由 AT&T 贝尔实验室开发的一款具有影响力的操作系统。尽管 Unix 仍在不断演进并保持其流行度（尤其是作为强大的网络服务器操作系统），但许多 Unix 变体都是专有的。相比之下，Linux 是一个开源操作系统，可以从互联网站点免费下载。

Linux 的源代码很容易获得，任何具备相应技术能力的人都可以对其进行修改或改进。此外，Linux 是可以自由重新分发的。只要你遵守几项简单的版权限制，你就可以制作 Linux 的额外副本并将其赠送或出售给他人。这些特性使 Linux 对许多顾问来说比 Unix 更具吸引力，并解释了它作为领先互联网操作系统的流行原因。

> 注意：第 5 章“Linux 历史”将更详细地描述 Linux 操作系统。

### Red Hat 和 Red Hat Linux

Red Hat 成立于 1994 年，提供美国最流行的 Linux 发行版——Red Hat Linux。它的 Linux 发行版与其它供应商的类似，包括 Linux 操作系统、用于安装和维护它的实用程序以及有用的应用程序。Red Hat Linux 赢得了许多奖项，包括三次被命名为 *Infoworld* 年度产品。除了 Linux 发行版，Red Hat 还提供 Linux 服务，包括支持、咨询和培训。

### 认证

对熟练技术人员的高需求促使许多组织赞助认证计划。寻求认证的技术人员参加考试，如果表现足够好，他们将被授予一份证明其能力的证书。在最受欢迎的技术认证计划中，包括微软认证系统工程师 (MCSE) 和思科认证互联网专家 (CCIE) 计划。

三类主要群体可以从技术认证计划中获益：

- 员工可以从认证提供的增强职业机会中获益，因为在其他条件相同的情况下，潜在雇主可能会更倾向于选择一名获得认证的候选人，而非未获得认证的人。
- 雇主可以获益，因为他们可以获得候选人技能的客观指标，从而做出更好的招聘决定。



- 赞助商可以通过提供认证培训课程和认证考试所获得的收入获益。他们还可以通过在行业内提高知名度而获益。

## 红帽认证工程师计划

1998年期间，红帽（Red Hat）为红帽认证工程师（RHCE）开发了一套认证计划，称为 RHCE 计划。1999年，他们开始提供 RHCE 备考课程和认证考试。与其他技术认证计划一样，RHCE 计划旨在为技术人员和雇主提供一个衡量技能和知识的有用标准。红帽还将 RHCE 计划作为希望与红帽合作的公司的一种筛选机制。这些公司必须在员工中拥有 RHCE，以确保其技术人员具备与红帽成功协作所需的技能和经验。

RHCE 考试的一个不寻常之处在于它是*基于性能的（performance-based）*。其他认证计划主要依靠笔试来衡量知识和技能，而 RHCE 考试包含一系列练习，要求候选人执行典型的系统和网络管理任务，如软件安装、配置和故障排除。RHCE 考试还包括笔试部分；然而，常见的情况是候选人在笔试部分表现良好，但在性能部分表现不佳，甚至不及格。红帽认为，*基于性能的考试*比组成大多数认证计划的选择题考试能更可靠地衡量候选人的技能。

除了测试候选人对 Linux 和网络的一般知识外，RHCE 考试还评估候选人执行以下操作的能力：

- 安装和配置 Red Hat Linux
- 配置文件系统和网络
- 配置 X（在 Unix 和 Linux 系统上使用的图形用户界面）
- 配置基础安全
- 配置网络服务
- 执行日常维护
- 执行诊断和故障排除

由于红帽定期更新其 Linux 发行版，因此 RHCE 认证并非永久有效。然而，根据红帽的政策，RHCE 认证至少在一年内保持有效。

> **注意**
>
> 红帽已宣布计划提供更高水平的认证——RHCE II，重点关注服务器管理、网络、集成和安全。RHCE II 不会取代 RHCE。相反，红帽预计许多候选人将把 RHCE 认证作为获得 RHCE II 认证的敲门砖。在撰写本文时，红帽尚未公布关于 RHCE II 的进一步细节。您应查看红帽官网 `www.redhat.com` 以获取关于 RHCE II 的最新信息。

### RHCE 课程与考试

作为 RHCE 计划的一部分，红帽提供了几门旨在帮助候选人准备 RHCE 考试的课程。候选人必须参加 RH302 课程，该课程即为考试本身。不过，候选人可以选择不参加、部分参加或全部参加其他课程。

本节介绍了红帽提供的 RHCE 课程以及 RH302 考试。接下来的章节将帮助您评估参加 RHCE 考试的准备情况，并帮助您制定考试成功的策略。

红帽在美国和英国的多个地点提供课程。当前的课程时间表可在其网站 `www.redhat.com` 上获取，该网站还提供了每门课程的当前学费。

### RH033：Red Hat Linux 简介 I, II

RH033 是一门为期四天的课程，面向没有 Unix 或 Linux 经验的用户。不过，学生应具备之前的计算机使用经验，包括使用鼠标和图形用户界面。完成课程后，学生应能够使用并自定义 GNOME 桌面，并能够使用 Linux 命令 shell。在撰写本文时，RH033 的学费为 1,998 美元。

## RH133：Red Hat Linux 系统管理 I, II

RH133 是一门为期四天的课程，面向熟悉 Red Hat Linux 的用户。在参加此课程之前，学生应完成 RH033 或具备同等经验。完成课程后，学生应能够安装和配置 Red Hat Linux、X 以及各种网络服务和客户端，如 DHCP、NIS、 NFS 和 Samba。学生还应能够执行基础故障排除并从源代码重新构建 Linux 内核。在撰写本文时，RH133 的学费为 2,098 美元。

## RH253：Red Hat Linux 网络与安全管理

RH253 是一门为期四天的课程，面向 Unix 或 Linux 系统管理员。在参加此课程之前，学生应完成 RH133 或具备同等经验。完成课程后，学生应能够安装和配置网络服务，如 Apache、DHCP、DNS、FTP、Samba、NFS、sendmail 和 IMAP4/POP3 邮件。学生还应能够建立并管理安全策略，包括密码安全、内核安全、公钥/私钥加密、Kerberos、安全外壳（secure shell）和防火墙等元素。在撰写本文时，RH253 的学费为 2,198 美元。

## RH300：RHCE

RH300 是一门为期五天的课程，其中包含 RH302（RHCE 考试）作为课程的有机组成部分。在参加此课程之前，学生应完成 RH253 或具备同等经验，并具有担任 Unix 或 Linux 系统或网络管理员的经验。

该课程由四天的教学组成，第五天专门用于 RHCE 考试。完成课程后，学生应准备好管理一个提供常见 TCP/IP 服务（如 FTP 和 HTTP）的 Red Hat Linux 系统。

该课程包含八个教学单元，每个单元都有一个或多个与以下主题相关的动手实验：

- 硬件与安装（x86 架构）
- 配置与管理
- 替代安装方法
- 内核服务与配置
- 标准网络服务
- X Window 系统
- 用户与主机安全
- 路由器、防火墙、集群与故障排除

在撰写本文时，RH300 的学费为 2,498 美元，其中包含 RH302（RHCE 考试）的价格。

## RH302：RHCE 考试

虽然红帽将其称为“课程”，但 RH302 并非通常意义上的课程。相反，RH302 是 RHCE 考试，时长为一天。RH302 是 RHCE 候选人必须参加的唯一课程。考试由以下三个闭卷部分组成：

- 诊断与故障排除实验（2.5 小时）
- 安装与配置实验（2.5 小时）
- 选择题考试（1 小时）

这些部分的呈现顺序并不总是相同。担任监考员的课程讲师将决定顺序并在当天早些时候宣布。三个部分的权重相同，每部分 100 分。最低合格分数为 240 分（即 80%）。然而，候选人必须在每个考试部分中至少获得 50 分（50%）才能通过考试。

在撰写本文时，RH302 的学费为 749 美元。不过，对于参加 RH300 的学生，RH302 的价格已包含在 RH300 的价格中。红帽会在考试后 10 个工作日内通过电子邮件通知候选人的考试分数。

本书的第七部分详细介绍了 RHCE 考试，并就如何应对考试及其三个部分给出了具体建议。

### 评估您的准备情况

本书随附的 CD-ROM 包含一个评估测试，您可以使用它来确定参加 RHCE 考试的准备情况。除了参加评估测试外，您还可以在阅读本书之前通过考虑以下问题来预估自己的准备情况。

1. 您是否参加过 Unix 系统管理课程或阅读过相关书籍？
2. 您是否参加过 TCP/IP 网络课程或阅读过相关书籍？
3. 您是否参加过 Linux 课程或阅读过相关书籍？
4. 您是否安装、配置并管理过 Unix 或 Linux 系统？
5. 您是否安装、配置并管理过各种 Unix 或 Linux 网络服务和应用程序，如 Apache、NFS 和 Samba？

如果对每个问题的回答都是“是”，那么您可能已经准备好参加 RHCE 考试了。尽管如此，本书仍将帮助您回顾重点并填补知识空白。

如果您对前三个问题中的任何一个回答为“否”，您需要仔细阅读本书中介绍陌生材料的章节。您可能还需要通过这些章节末尾列出的其他资料来补充学习。

如果您对问题 4 或 5 的回答为“否”，您需要额外的练习才能成功通过 RHCE 考试的基于性能的部分。本书的相关章节包含建议的动手练习，您应当执行这些练习以准备 RHCE 考试。

### 制定您的认证策略

您可以通过以下一种或多种方式准备 RHCE 考试：

- 您可以参加红帽或其他机构的课程。
- 您可以独立学习本书及其他书籍和文档。
- 您可以作为小组的一部分学习本书及其他书籍和文档。



让我们详细看看每个选项。

## 参加红帽课程

准备 RHCE 认证最有效的方法之一是参加相应的红帽课程。如果你的雇主愿意承担全部或大部分课程费用，这种方法尤其具有吸引力。

然而，如表 1.1 所示，如果你是 Unix 和 Linux 的新手，这种方法的费用可能会非常昂贵。而且，除非你住在红帽培训地点附近，否则你还必须在已经相当高昂的课程费用基础上，加上交通、住宿和饮食的开销。对于许多人来说，参加课程的时间和金钱成本是难以承受的。幸运的是，还存在其他选择。

### 表 1.1 红帽课程的大致学费

| 课程 | 学费 |
|---|---|
| RH033 | $1,998 |
| RH133 | $2,098 |
| RH253 | $2,198 |
| RH300 | $2,498 |
| 总计 | $8,792 |

> **注意** 在美国，你可能可以将参加认证课程的部分或全部费用从你的应纳税收入中扣除。在某些情况下，你甚至可能有资格获得税收抵免。详情请咨询你的税务顾问。

## 自学

如果你具备相应的背景和经验，可以通过自学准备 RHCE 考试。本书旨在帮助你学习或回顾通过 RHCE 考试所需的所有知识。如果你不确定自己是否能够有效地独立学习，可以考虑仅参加 RH300 课程（该课程包含 RHCE 考试）。在为期四天的课程结束时，你可能会清楚地知道在次日的考试前需要重点补习哪些主题。

> 请参阅“前言”部分，了解关于本书功能及其最有效使用方法的重要信息。

## 学习小组

虽然你可以通过自学准备 RHCE 考试，但你可能会发现，如果作为小组的一部分进行准备，效率会更高，效果更好，而且更有趣。小组员通常拥有个人优势，可以成为小组的资源。例如，小组中一名成员可能特别擅长计算机安全。该成员可以向其他成员简述计算机安全知识，澄清计算机安全中令人困惑的方面，并帮助成员评估他们的计算机安全专业知识。

即使小组成员在组成小组之前不具备独特的专业知识，小组也可以将学习内容分成若干片段。然后，小组可以将每个片段分配给一名成员，由其指导小组学习该片段，并监督成员在该片段上的进展。

伴随小组工作的问责机制和友好的竞争可以激励成员取得比自学可能获得更高的成就。因此，如果你能找到其他对 RHCE 认证感兴趣的人，请组建一个学习小组。

## 实践

由于 RHCE 考试是基于实际操作的，因此你拥有（或培养）使用 Unix 或 Linux 及相关网络服务的经验至关重要。本书的各章节提供了实践练习。这些练习可能很耗时，你可能会觉得它们是不必要的。然而，除非你有丰富的实践经验，否则你应该完成每一个练习。通常，练习会引导你发现那些仅通过阅读练习说明而无法察觉的细微之处。

如果你使用 Unix 和 Linux 的实践经验较少，你应该构建并执行自己的额外练习。RHCE 考试测试的水平相当于大约两年的 Linux 和网络经验。通过勤奋的努力，你可以在几周内积累这些经验。然而，这样做要求你在任何环节都不能偷懒。

## 本章小结

在本章中，你学习了关于 Linux、认证以及 RHCE 认证的知识。以下是本章涵盖的最重要主题：

- **认证的益处** 作为一名技术人员，认证可能会带来更好的职业机会。
- **Linux** Linux 是 Unix 操作系统的一个可自由分发的开源后裔。
- **红帽与红帽 Linux** 红帽销售红帽 Linux，这是美国最受欢迎的 Linux 版本。红帽还提供 Linux 支持和咨询服务，并赞助 RHCE 认证计划。
- **红帽课程** 红帽提供多门课程，培训学生使用和管理红帽 Linux。其中一门课程 RH302 即为 RHCE 考试。
- **RHCE 考试** RHCE 考试是一场为期一天的考试，包括多项选择题和基于操作的组件，用于衡量候选人关于红帽 Linux 的知识和技能。
- **基于操作的考试** 基于操作的考试是一种要求候选人演示技能而非仅仅是记忆和理解的考试。
- **制定认证策略** 你可以单独参加 RH302 考试，也可以同时参加额外的红帽课程。你也可以独立学习本书和其他资料，或者作为学习小组成员一起学习。最后，你可以通过本书中的实践练习来增加经验，为 RHCE 考试的操作组件做准备。

### 关键术语

在继续下一章之前，请确保你熟悉以下术语：

- certification（认证）
- Linux
- performance-based exam（基于操作的考试）
- Red Hat Certified Engineer (RHCE)（红帽认证工程师）
- Red Hat, Inc.（红帽公司）
- Unix

## 其他信息来源

如果你想进一步了解本章介绍的主题，可以参考以下来源：

- 关于红帽认证计划的官方信息来源是红帽官网 `www.redhat.com`。
- Global Knowledge 是红帽的合作伙伴，在整个北美提供 RHCE 培训和其他培训。请访问其网站 `www.globalknowledge.com`。
- 红帽并不是唯一赞助 Linux 认证计划的公司。其他提供 Linux 认证的公司和组织包括：
    - Brainbench (`www.brainbench.com`)
    - Cyber Tech Institute (`www.getcertified.com`)
    - Linux Professional Institute (`www.lpi.org`)
    - Prosoft Training (`www.prosofttraining.com`)
    - Sair, Inc. (`www.linuxcertification.org`)

## 复习题

1. 认证在以下各项中以指明的方式带来益处，除了：
    A. 雇主：改进招聘决策
    B. 赞助者：提高产品质量
    C. 赞助者：增加收入
    D. 工作者：增强职业机会

2. 关于 Linux，以下哪项是正确的？
    A. Linux 是 Unix 的亲属。
    B. Linux 是一个开源软件系统。
    C. Linux 是一个操作系统。
    D. Linux 是免费的。

3. 以下哪项是美国最受欢迎的 Linux 发行版？
    A. Caldera Open Linux
    B. Red Hat Linux
    C. Slackware Linux
    D. SuSE Linux

4. RHCE 必须完成以下哪门红帽课程？
    A. RH253
    B. RH300
    C. RH302
    D. RH310

5. 基于操作的 RHCE 考试通过要求你执行以下哪项来测试你的能力？
    A. 回答论述题。
    B. 回答多项选择题。
    C. 演示网络管理技能。
    D. 演示系统管理技能。

6. 要通过 RHCE 考试，你应该能够执行以下哪些操作？
    A. 使用 Linux 和 X
    B. 安装和配置 Linux
    C. 安装和配置网络服务
    D. 排除故障并修复 Linux 系统

## 复习题答案

1. B. 技术人员的认证并不会直接导致其认证产品的质量提高。

2. A, B, C, 和 D。Linux 的架构基于 Unix。Linux 内核和红帽 Linux 发行版都可以从互联网上免费下载。

3. B. 红帽 Linux 被公认为美国最受欢迎的发行版；SuSE 在欧洲很受欢迎，并在美国变得越来越受欢迎。

4. C. RH302 是 RHCE 考试，而 RH300 是包含 RH302 的考试准备课程。每个 RHCE 都完成了 RH302；但有些 RHCE 在没有参加 RH300 的情况下通过了 RH302。

5. B, C, 和 D。RHCE 考试不包含论述题。

6. A, B, C, 和 D。RHCE 考试要求你能够使用和管理 Linux 及相关服务，并能够排除其运行中的故障。



# 第 2 章：硬件基础

本章涵盖的 RHCE 准备主题：

- **理解 Linux 对计算机系统的支持。
    - 理解并使用 Red Hat 硬件兼容性列表。
    - 理解 Red Hat 的硬件检测工具 kudzu。
    - 理解 Linux 对 CPU 和 SMP 的支持。
    - 理解 Linux 对 RAM 的支持。

- 理解 Linux 对字符设备的支持。
    - 理解设备配置并能够配置设备。
    - 理解 Linux 对串口和并口的支持并能够配置它们。
    - 理解 Linux 对常见外设的支持并能够配置它们。
    - 理解 Linux 对视频的支持。

- 理解 Linux 对块设备的支持。
    - 理解块设备接口。
    - 理解磁盘寻址。
    - 理解磁盘分区并能够选择合适的分区结构。
    - 理解启动过程。

Linux 支持极其多样化的计算机系统和设备。尽管如此，它并不能支持所有设备。即使 Linux 支持某个特定的系统或设备，在 Linux 能够访问该设备之前，你必须对其进行正确配置。

本章讨论 Linux 对硬件的支持。在 Unix 世界中，硬件设备被分为两个类别之一：

**字符设备** *字符设备* 每次读取或写入的数据不超过一个字符。

**块设备** *块设备* 每次读取或写入的数据包含几个——甚至很多个——字符。

在现实世界中，这两个类别有时会重叠，但它们是将关于设备的思考方式组织起来的一种有效方法。

本章首先描述 Linux 对系统的支持，然后描述 Linux 对字符设备的支持，最后以描述 Linux 对块设备的支持结束。

## Linux 对系统的支持的系统

虽然 Linux 运行在多种平台上，但 Red Hat Linux 目前仅支持以下三种：

- Compaq（原 DEC）Alpha 架构
- Intel 架构
- Sun SPARC（可扩展处理器架构）

RHCE 考试仅涵盖 *Intel 架构* PC 的 Red Hat Linux 管理，因此本章仅描述该架构。请注意，除 Intel 公司之外，许多公司也生产与 Intel 架构兼容的硬件。

> 有关非 Intel 架构的更多信息，请参阅 www.redhat.com/support/hardware 上的 Red Hat 硬件兼容性列表。

## 硬件兼容性

关于与 Linux 兼容的硬件，主要有两个信息来源。本节将描述这些来源。

### Linux 硬件兼容性 HOWTO

Linux 文档项目（www.linuxdoc.org）旨在“创建一套权威的免费 Linux 文档”。为此，他们发布了一系列非常有用的 HOWTO、指南和 man 页面。其中最重要且最实用的文档之一是 *Linux Hardware Compatibility HOWTO*，也称为 *Hardware-HOWTO*。该 HOWTO 识别了与 Linux 兼容的硬件设备和组件，并为选择兼容硬件及其使其正常工作提供暗示和技巧。

从 Red Hat Linux 6.2 发行版开始，HOWTOs 提供十几种语言和多种格式，包括文本、HTML 和 PDF。你可以在文档 CD-ROM 上找到 HOWTOs，而不是在安装 CD-ROM 上。它们足够方便且紧凑，你应该将它们复制到系统硬盘的 `/usr/doc/HOWTO` 目录中。为此，挂载 CD-ROM 并执行以下命令：

```
# mkdir /usr/doc/HOWTO
# cd /mnt/cdrom/HOWTOS
# cp -R *.HOWTO *.htm mini /usr/doc/HOWTO
```

如果 `/usr/doc/HOWTO` 目录已存在，`mkdir` 命令将失败；不必担心。如果你将 CD-ROM 挂载在 `/mnt/cdrom` 以外的挂载点，你应该相应地修改第二个命令。你可以在 `HOWTOS/translations` 目录中找到非英语 HOWTOs，并在 `HOWTOS/other-formats` 目录中找到 HTML 和 PDF 格式的 HOWTOs。

在后续章节中，假设你已经安装了 HOWTOs，因此对特定 HOWTO 的引用均假设文件位于 `/usr/doc/HOWTO`。如果你选择不安装 HOWTOs，则需要在 CD-ROM 上查找。

### Red Hat 硬件兼容性列表

Red Hat, Inc. 维护自己的支持硬件列表，这大致是 *Hardware-HOWTO* 中列出的设备和组件的一个子集。*Red Hat 硬件兼容性列表* 位于网页 `www.redhat.com/support/hardware`。在为 Red Hat Linux 系统选择硬件或在现有系统上安装 Red Hat Linux 时，请检查 Red Hat 硬件兼容性列表，以确保你要安装的设备受 Red Hat Linux 支持。

Red Hat 硬件兼容性列表根据以下四个类别对硬件设备进行分类：

- **Tier 1** Red Hat Linux 可以检测并可靠使用的硬件。
- **Tier 2** Red Hat Linux 应该能够检测并使用的硬件；但某些用户在使用此类硬件时会遇到问题。
- **Tier 3** 有问题的硬件，或者目前仅存在实验性驱动程序的硬件。Red Hat, Inc. 提供有关 Tier 3 硬件的信息，但不提供支持。
- **Incompatible** 已知无法在 Red Hat Linux 上运行的硬件。

Red Hat Linux 6.1 及更高版本包含 kudzu，这是一个在启动时运行并识别新安装硬件的工具。当 kudzu 检测到新硬件时，它会显示一个方便的对话框，允许你配置新硬件或推迟配置。kudzu 工具在处理未包含在 Red Hat 硬件兼容性列表中的硬件时可能无法正常工作。

## CPU 架构与对称多处理

虽然 Linux 最初是为 Intel x86 中央处理器 (CPU) 架构实现的，但现在它运行在多种架构上，包括：

- Acorn
- ARM
- Compaq (DEC) Alpha
- Motorola 68k
- MIPS
- Power Mac
- PowerPC
- Sun SPARC

然而，Red Hat Linux 仅支持 Compaq Alpha、Intel 和 SPARC 架构。

Linux 还支持*对称多处理* (SMP)，即单个系统包含多个 CPU。然而，标准 Red Hat Linux 内核未启用 SMP。如果你的系统支持 SMP，安装程序将同时安装标准内核和特殊的 SMP 内核；即使只存在一个 CPU，SMP 内核也将被启用。

Linux SMP 最多支持 16 个处理器；然而，Intel 架构最多支持 8 个。图 2.1 展示了 SMP 性能如何随处理器数量的变化而变化。如你所见，在增加四个处理器之后，性能增长速度放缓。

**图 2.1** SMP 性能

SMP 并不会提高进程的执行速度；它仅仅是让多个进程能够并发运行。运行在单个处理器上的单线程应用程序无法从 SMP 中获益。

## 内存

随 Red Hat Linux 6.2 发行的 Linux 2.2 内核通常会自动检测安装的 RAM（随机存取存储器）容量。然而，标准内核无法自动检测或使用超过 1GB 的 RAM。要启用对 1GB 以上 RAM 的支持，你必须修改 `include/asm-i386/page.h` 头文件并重新编译内核。你可能还需要向 `lilo` 传递一个 `mem` 参数，指示 `lilo` 忽略由无法检测和报告 64MB 以上 RAM 的系统 BIOS 报告的物理内存大小。

在 Intel 架构 CPU 上运行时，Red Hat Linux 允许系统访问最多 4GB 的虚拟内存，包括物理内存和交换内存。例如，一个可以访问 2GB 物理内存的系统只能访问 2GB 的交换内存。

## CPU 与总线

Red Hat Linux 支持 Intel CPU 家族及其兼容产品，包括 AMD、Cyrix 和 Winchip 制造的产品。表 2.1 总结了 Red Hat Linux 支持的 CPU。

### 表 2.1 支持的 CPU

| 支持级别 | CPU |
|---|---|
| Tier 1 | Intel Celeron |
| Tier 1 | Intel Pentium |
| Tier 1 | Intel Pentium II |
| Tier 1 | Intel Pentium III |
| Tier 1 | Intel Pentium SMP |
| Tier 1 | AMD K6-2 |
| Tier 1 | AMD K6-3 |



### 表 2.1 支持的 CPU（续）

| 支持级别 | CPU |
|---|---|
| 第二梯队 (Tier 2) | AMD Athlon <br> Cyrix 6x86 <br> AMD K5 <br> AMD K6 <br> Winchip |
| 第三梯队 (Tier 3，不支持) | Cyrix MediaGX |

PC 的*总线*（bus）*用于将设备连接到 CPU 和内存，尤其是通过扩展槽安装的设备。所使用的总线类型决定了系统可以容纳的设备和扩展卡类型。Red Hat Linux 支持以下总线接口：

- **AGP** (Accelerated Graphics Port)，高性能视频接口
- **EISA** (Extended Industry Standard Architecture) 总线，现已不常用
- **ISA** (Industry Standard Architecture) 总线，在旧型计算机（如 IBM PC-AT）中可见的 16 位总线
- **PCI** (Peripheral Component Interconnect) 总线，在大多数近期制造的计算机中可见的 32 位总线
- **PCMCIA** (Personal Computer Memory Card International Association) 总线，也称为 PC Card 总线
- **VESA** (Video Electronics Standards Association) 总线，也称为 VL 总线

Red Hat Linux 并不支持所有 PCMCIA 控制器，但它支持几种流行的控制器以及多种类型的卡。PCMCIA 卡的一个便捷特性是它们支持热插拔；无需关闭系统电源即可插入或移除。

Red Hat Linux 不支持以下总线接口：

- **IEEE 394** 也称为 Firewire。这是本章后面介绍的 SCSI 接口的潜在竞争对手。
- **MCA** (Micro Channel Architecture)。虽然 Linux 与 MCA 兼容，但 Red Hat Linux 不支持它。
- **USB** (Universal Serial Bus)。

Linux 内核对 Firewire、MCA 和 USB 的支持尚未完成。Linux 2.4 内核将包含对 USB 的额外支持，但 USB 设备驱动程序可能无法立即获得。Red Hat Linux 计划支持 Firewire、MCA 和 USB。

## 系统资源

大多数设备需要系统资源才能运行。虽然某些设备可以共享系统资源，但许多设备则不能。配置设备的一个重要部分是以不产生冲突的方式分配系统资源。最重要的三种系统资源是 IRQ、I/O 端口和 DMA，将在以下小节中详细说明。

### IRQs

IRQ（或硬件中断）是一种通知 CPU 发生重要事件（如输入/输出 (I/O) 操作完成）的信号。大多数设备需要一个专用 IRQ，必须通过手动或系统 BIOS 分配。PC 的 IRQ 数量有限，其中大多数有标准分配，如表 2.2 所示。

### 表 2.2 标准 IRQ 分配

| IRQ | 分配 |
|---|---|
| 0 | 为不可屏蔽中断 (NMI) 保留，用于标记奇偶校验错误 |
| 1 | 为系统定时器保留 |
| 2 | 为级联到第二个中断控制器 (IRQ 8-15) 保留 |
| 3 | 如果启用，则为串口 ttyS1 和 ttyS3；否则可用 |
| 4 | 如果启用，则为串口 ttyS0 和 ttyS2；否则可用 |
| 5 | 如果启用，则为并行端口 lp1；否则可用；常用于声卡或调制解调器 |
| 6 | 软盘驱动器控制器 |
| 7 | 如果启用，则为并行端口 lp0；否则可用 |
| 8 | 为实时时钟保留 |
| 9 | 可用 |
| 10 | 可用：常用于网络适配器 |
| 11 | 可用：常用于 SCSI 适配器 |
| 12 | 如果启用，则为 PS/2 鼠标；否则可用 |
| 13 | 为浮点处理器保留 |
| 14 | 如果启用，则为 IDE 硬盘控制器 1；否则可用 |
| 15 | 如果启用，则为 IDE 硬盘控制器 2；否则可用 |

### I/O 端口

如前所述，大多数设备需要一个 IRQ，以便它们可以向 CPU 发出信号，通知其 I/O 操作已完成。大多数设备还需要一系列专用的单字节内存区域，称为 I/O 端口，用于将数据从设备移动到系统内存，或从系统内存移动到设备。某些设备需要多组 I/O 端口。

一组 I/O 端口有时被称为设备的基 I/O 地址。I/O 端口由 0x0-0xFFFF 范围内的十六进制（基 16）数字标识。

### DMAs

大多数设备依赖 CPU 将数据从内存移动到设备。然而，一些高速设备能够直接访问内存。这使得 CPU 在 I/O 操作进行时可以空闲出来处理其他任务，这种技术称为直接内存访问 (DMA)。

系统具有有限数量的通道，称为 DMA 通道或简称 DMAs，DMA 可在这些通道上发生。使用 DMA 的设备必须被分配一个（有时是两个）DMA 通道。表 2.3 总结了这些通道及其标准分配。

### 表 2.3 标准 DMA 分配

| DMA | 分配 |
|---|---|
| 0 | 通常为内存刷新保留 |
| 1 | 可用 (8-bit) |
| 2 | 为软盘驱动器保留 |
| 3 | 可用 (8-bit) |
| 4 | 为 DMA 控制器 1 保留 |
| 5 | 可用 (16-bit) |
| 6 | 可用 (16-bit) |
| 7 | 可用 (16-bit) |

## 操作适配卡

配置适配卡涉及指定设备使用的 IRQ、I/O 端口和 DMA。根据您拥有的适配卡类型，可以通过以下三种方式中的一种或多种进行配置：

- **跳线卡 (Jumpered Cards)** 较旧的适配卡通常包含跳线，允许您物理地设置配置。
- **无跳线卡 (Jumperless Cards)** 更现代的卡允许您使用软件程序来设置配置。
- **即插即用卡 (Plug-and-Play Cards)** 一些卡可以通过 BIOS 或兼容即插即用的操作系统自动配置。

### 配置跳线卡

虽然配置跳线卡可能不方便，但它很直接。您只需设置跳线以指定卡所需的资源，确保资源分配不与其他卡冲突。您可能还需要指定能够识别分配给该卡资源的设备驱动程序选项。

### 配置无跳线卡

如果 Linux 设备驱动程序提供了适当的选项，配置无跳线卡就很简单。在模块配置文件 `/etc/conf.modules` 中指定所需的选项。当设备的模块加载时，它会获取您指定的选项并相应地设置卡的配置。

然而，某些设备驱动程序可能不支持您需要的配置选项。在这种情况下，您可以配置系统以引导 DOS 或 Linux。要配置该卡，请引导至 DOS 并运行配置该卡的 DOS 程序。然后，通过例如使用 `loadlin` 工具引导 Linux，该工具允许 Linux 从 DOS 启动。

### 配置即插即用卡

大多数现代 PC 使用 PCI 总线，它支持一项称为*即插即用 (plug-and-play)* 的功能。即插即用旨在简化硬件配置。所有 PCI 卡都支持即插即用。一些 ISA 卡支持即插即用，但仅在插入即插即用系统时才支持。

在运行过程中，即插即用首先探测卡以确定它们支持哪些资源配置。然后，它分配资源，使每张卡都能访问其所需的资源。

PCI 设备的即插即用配置可以由 BIOS 或操作系统执行。目前，Linux 并不完全支持即插即用。因此，如果您的系统 BIOS 支持即插即用，您应该通过将 BIOS 选项 `PnP Aware OS` 或任何类似选项设置为 No 来配置它。

您可以使用 Linux `isapnp` 工具来配置 ISA 即插即用设备，这些工具在第 15 章“理解配置文件和脚本”中介绍。

## 对字符设备的支持

本节介绍了 Red Hat Linux 对字符设备的支持。字符设备通常一次读写一个字符的设备。大多数网络适配器是块设备。然而，它们的配置与字符设备比与块设备更相似。因此，它们与字符设备一起被包含在本节中。



## 端口

大多数 PC 都配备了串行端口（每次读写一个位）和并行端口（每次读写一个字符）。本小节将解释 Red Hat Linux 对串行和并行端口的支持情况。

### 串行端口

标准 Red Hat Linux 内核包含对 192 个串行端口的支持。然而，默认情况下，在安装 Red Hat Linux 期间仅创建设备文件 `/dev/ttyS0`、`/dev/ttyS1`、`/dev/ttyS2` 和 `/dev/ttyS3`。Linux 文档有时会提到 `/dev/cua0` 等设备；但这是一个过时的、已被弃用的串行端口命名方式。您可以通过修改 `drivers/char/serial.c` 文件并重新编译内核来增加端口数量。

通常可以使用 BIOS 来配置与串行端口 `ttyS0` 和 `ttyS1` 相关联的 IRQ 和 I/O 端口。要配置额外的端口，可以使用 `setserial` 命令，如下所示：

```
setserial /dev/ttySn irq x port y skip_test autoconfig
```

其中 `ttySn` 指定串行端口，`x` 指定要分配的 IRQ，`y` 指定要分配的 I/O 端口。

请参阅 `setserial` 命令的手册页，以了解设置波特率和其他运行参数的其他选项。

### 并行端口

标准 Red Hat Linux 内核包含对 8 个并行端口的支持。然而，默认情况下，在安装 Red Hat Linux 期间仅创建设备文件 `/dev/lp0`、`/dev/lp1` 和 `/dev/lp2`。您可以通过修改头文件 `drivers/char/lp.c` 并重新编译内核来增加端口数量。通常可以使用 BIOS 来配置与并行端口 `lp0` 和 `lp1` 相关联的 IRQ 和 I/O 端口。配置两个以上的并行端口并不常见。

## 外设

本小节描述 Red Hat Linux 对常见外设的支持，包括键盘、鼠标、调制解调器、网络适配器、声卡和显卡。

### 键盘

Red Hat Linux 将 AT 型和 PS/2 型键盘均作为第一层级（Tier 1）设备支持。

### 鼠标

Red Hat Linux 包含对标准串行和 PS/2 鼠标的支持，这些通常在第一层级获得支持。总线鼠标（Bus mice）通常在第二层级（Tier 2）获得支持。最近的微软串行鼠标使用一种特殊的协议，尚未获得完全支持。微软的 IntelliMouse（滚轮鼠标）被列为第三层级（Tier 3）设备。

### 调制解调器

Red Hat Linux 在第一层级支持大多数外接调制解调器，以及基于 Lucent Venus 芯片组的内置 PCI 调制解调器。遗憾的是，整类被称为 `WinModems` 的调制解调器需要特殊的软件驱动程序才能运行。制造商将 Win32 软件与这些调制解调器捆绑在一起，但他们不分发其他操作系统的软件。因此，Red Hat Linux 不支持此类调制解调器。此外，即插即用的内置调制解调器也被列为不兼容，尽管可以使用 `isapnp` 或 `setserial` 对其进行配置（即便有些不便）。

### 网络适配器

Red Hat Linux 支持多种以太网卡和几种令牌环（Token Ring）卡。在被列为第三层级或不兼容设备的以太网卡中包括以下型号：

- 3Com 3C501
- 3Com 3C905B, 3C905C（尽管 3Com 最近提供的驱动程序可能会缓解该问题）
- 3Com ISA Etherlink XL (3Com 3C515)
- General Instruments SB1000
- Intel EtherExpress 100plus
- Intel EtherExpress Pro/10 PCI（不兼容）
- Intel EtherExpress Pro/100B
- Linksys Fast 10/100 tulip clones
- SeaLevel Systems 4012, 4021
- Silicon Integrated System Corporation Sis 900 PCI
- 使用 MX987x5 芯片组的 Macronix, Inc. 显卡
- Xircom 以太网适配器（不兼容）

### 声卡

Red Hat Linux 发行版对声卡的支持在所有 Linux 发行版中是最优秀的。然而，声卡支持仍然是 Linux 的弱点。目前没有声卡在第一层级获得支持。以下声卡在第二层级获得支持：

- Acer Notebook Sound
- AdLib
- Advance Logic ALS-007
- Compaq Deskpro XL sound
- Creative/Ensoniq Audio PCI 1371
- Crystal CS423x 声卡芯片
- Ensoniq Audio PCI 1370 (SoundBlaster 64/128 PCI)
- Ensoniq SoundScape
- ESS1688 AudioDrive
- ESS1886 AudioDrive
- ESS688 AudioDrive
- Gravis UltraSound
- Gravis UltraSound MAX
- Gravis UltraSound PnP
- Logitech SoundMan 16
- Logitech SoundMan Games (非 SM16 或 SM Wave)
- MAD16 Pro (OPTI 82C929/82C930)
- MediaTrix AudioTrix Pro (MT-0002-PC 控制芯片)
- MediaVision Jazz16 (ProSonic, SoundMan Wave)
- miroSOUND PCM12
- Mozart/MAD16 (OPTI 82C928)
- OPL3-SA1 声卡芯片
- OPL3-SA2/3/x 声卡芯片
- Pro Audio Spectrum/Studio 16
- PSS (Orchid SW32, Cardinal DSP16)
- S3 SonicVibes
- Sound Blaster
- Sound Blaster 16/PNP
- Sound Blaster 32/64 AWE
- Sound Blaster DS
- Sound Blaster Pro
- Turtle Beach MultiSound Classic/Monterey/Tahiti
- Turtle Beach MultiSound Pinnacle/Fiji
- Windows Sound System (AD1848/CS4248/CS4231)

这些卡的克隆版，或被列为与这些卡兼容的卡，不一定受到支持。

### 显卡

XFree86 项目提供了一个可免费重新分发的 X Window 系统（也称为 X）实现。Red Hat Linux 发行版使用了 XFree86 的 X 实现，因此通常支持 XFree86 实现所支持的显卡。然而，存在几种例外情况，因此您应该参考 [Red Hat 硬件兼容性列表](www.redhat.com/support/hardware)，而不是 XFree86 项目发布的受支持显卡列表。受支持和不受支持的显卡列表太长，无法在此汇总。在 Red Hat Linux 支持存在问题的显著显卡中，包括笔记本电脑显卡，制造商通常会针对笔记本电脑的 LCD 进行定制。

笔记本电脑带来了影响 Linux 兼容性的特殊复杂情况。例如，笔记本电脑制造商经常在具有相同型号的笔记本电脑中使用各种不同的硬件组件。总的来说，确定笔记本电脑是否与 Red Hat Linux 兼容的唯一方法是在该笔记本上成功安装、配置并运行 Linux。这种情况已开始改善，因为少数制造商现在开始出厂预装 Linux 的笔记本电脑。然而，此类笔记本电脑并不一定受到 Red Hat Linux 的官方支持。

### 其他外设

Red Hat Linux 支持或兼容的其他字符设备包括以下设备：

- 红外设备
- 操纵杆（Joysticks）
- 多端口串行设备
- 打印机
- 无线电卡
- 扫描仪
- 通过并行端口连接的各种设备，如 Iomega Zip 驱动器

有关这些外设的更多详情，请参阅 Red Hat 硬件兼容性列表。

## 块设备支持

块设备是指每次读写超过一个字符的设备。块设备的示例包括软盘驱动器、硬盘驱动器、CD-ROM 驱动器、CD-R 驱动器和其他设备。本节描述 Red Hat Linux 对块设备的支持。

### 驱动器与驱动器接口

块设备可以通过多种方式连接到系统。然而，最常见的方式是通过软盘接口、IDE 或 EIDE 接口，或 SCSI 接口。本小节描述 Red Hat Linux 对这些接口的支持。

### 软盘驱动器

软盘驱动器接口很少出现问题。除了少数拥有古怪软盘控制器的母板外，您不应预期软盘驱动器会出现困难。它们通常由内核自动检测，无需特殊配置。

### IDE 和 EIDE 接口

Pentium 母板上大多数板载 IDE 控制器都得到了完全支持。当配置为 UDMA/33 运行模式时，UDMA/66 控制器受到支持。大多数其他 IDE 和 EIDE 控制器在第二层级获得支持。最多支持 8 个 IDE 设备，尽管只有两个接口（最多四个驱动器）会被自动探测。可以通过指定启动参数来探测额外的接口，例如：

```
ide2=0x1e8,0x3ee,11 ide3=0x168,0x36e,10
```

Linux 2.2 内核并不完全支持 UDMA/66 控制器，因此 Red Hat Linux 也不支持。同样，Linux 2.2 内核也不支持 Promise Ultra/66 和 HPT66。

> Linux 2.4 内核预计将支持 UDMA/66 以及 Promise Ultra/66 和 HPT66 控制器。

### IDE 和 EIDE 驱动器

Red Hat Linux 完全支持几乎所有内部 IDE/EIDE 驱动器，包括容量大于 33.8GB 的 IDE 驱动器（由 Red Hat Linux 内核 2.2.14-5 及更高版本支持）。某些驱动器要求通过启动参数将几何结构指定给内核，例如：

```
linux hda=1023,63,255
```

少数驱动器与 Linux 兼容但不受支持。其中包括：

- 内部 Iomega IDE Zip 驱动器
- SuperDisk LS-120 可移动介质驱动器（在 Linux 安装期间无法正常工作，但稍后可以配置）

少数驱动器与 Linux 不兼容。这包括大多数可移动介质 IDE 驱动器，包括 Syquest 制造的驱动器。

### SCSI 接口

Red Hat Linux 支持多种 SCSI（以及 RAID）控制器。然而，某些控制器在第二层级获得支持，且有几个控制器完全不受 Red Hat Linux 支持。SCSI 控制器列表太长，无法在此汇总。详情请参阅 [Red Hat 硬件兼容性列表](www.redhat.com/support/hardware)。



## SCSI 驱动器

当 SCSI 设备连接到支持的控制器时，Red Hat Linux 提供完全支持。这包括可移动介质驱动器，例如 Iomega SCSI Zip 和 Jaz 驱动器，以及 Syquest 制造的驱动器。请注意，Iomega 并口 Zip 驱动器使用 SCSI 接口，且由 Red Hat Linux 完全支持。

## 硬盘

访问硬盘所采用的技术可能会对驱动器可存储的数据量产生限制。同样，将硬盘划分为*分区*的方式也会影响其使用方法。本小节将解释这些注意事项。

### 磁盘几何结构

硬盘的*磁盘几何结构*（disk geometry）描述了存储和访问数据时可能采用的地址。磁盘地址可以采用以下两种形式之一：

- **物理地址**：数据通过包含它们的柱面（cylinder）、磁头（head）和扇区（sector）进行寻址。
- **逻辑块地址 (LBA)**：数据通过一个相对扇区号进行寻址。

每种寻址方案都有其自身的限制。许多 BIOS 驱动程序在通过物理地址访问硬盘时，只能访问前 1024 个柱面（柱面 0-1023）。Linux 加载程序 `lilo` 仅在启动期间使用 BIOS 访问硬盘。但如果 BIOS 无法访问柱面 1024 或其之后的区域，则无法启动存储在（例如）柱面 1025 上的内核。避免此问题的一种简单方法是通过分区确保 Linux 内核存储在柱面 1024 之下。

*逻辑块寻址* 具有类似的限制。最大相对扇区号使得只有大约 8GB 的磁盘空间可寻址。同样，此限制仅在启动过程中影响 Linux，因为启动后不再使用 BIOS。

### 分区

通常最好（虽然并非绝对必要）将硬盘空间划分为多个分区。分区的主要好处是，损坏或崩溃通常仅限于单个分区，从而可以轻松地从其余分区中恢复数据。

IDE 磁盘驱动器的设备名称如 `/dev/hda`、`/dev/hdb` 等。SCSI 磁盘驱动器的设备名称如 `/dev/sda`、`/dev/sdb` 等。分区由从 1 开始的数字指定，并附加在驱动器名称之后。因此，第一个 IDE 驱动器上的第一个分区被命名为 `/dev/hda1`，而第二个 SCSI 驱动器上的第三个分区被命名为 `/dev/sdb3`。

### 主分区、扩展分区和逻辑分区

一块硬盘只能有四个普通分区，称为主分区。然而，其中一个主分区可以被指定为扩展分区。扩展分区不包含文件系统；相反，它可以包含多达 12 个其他分区，称为逻辑分区。第一个逻辑分区始终被指定为分区 5，即使定义的主分区少于四个。图 2.2 显示了一个典型的硬盘分区结构。

**图 2.2 典型的硬盘分区结构**

![](img/4eef9c6f2f52b608eba628cf4e2793ce_62_0.png)

### 分区类型

Linux 使用的分区主要分为以下两种类型：

- **Linux 原生 (Linux Native)**：用于存放包含程序和数据文件的标准 Linux 文件系统。
- **Linux 交换区 (Linux Swap)**：用于临时存放从物理内存交换到硬盘的内存内容。

Red Hat Linux 还支持多种其他*分区类型*，包括 MS-DOS、VFAT、HPFS 和 NTFS。然而，标准 Red Hat Linux 内核无法访问 HPFS 和 NTFS 文件系统；如果您需要此支持，必须重新编译内核。

Linux 内核支持高达 2GB 的交换分区。最多可以定义八个交换分区。

### 挂载点

与 UNIX 类似，Linux 将块设备的分区作为统一文件系统中的子目录进行挂载。持有分区内容的目录称为其*挂载点*。以下两个通过挂载点识别的分区尤为重要：

- `/`：根文件系统
- `/boot`：启动分区，包含 Linux 内核

根分区在系统初始化过程开始时，在内核本身加载到内存后被挂载。内核必须知道其标识，在 Red Hat Linux 系统中，该标识通常由 `lilo` 引导加载程序传递给内核。其他分区通过被挂载为根文件系统的子目录而集成到系统中。

启动分区是一个小分区，用于规避影响许多系统 BIOS 的 1024 柱面限制。通过将启动分区定位在前 1024 个柱面内，可以确保 BIOS 能够访问 Linux 内核。

## 总结

在本章中，您了解了 Linux 对各种硬件设备的支持。本章涵盖的最重要主题如下：

- **硬件兼容性**：Red Hat, Inc. 发布了一份与 Red Hat Linux 兼容且受其支持的硬件列表。
- **硬件配置**：硬件设备通常必须被分配一个唯一的 IRQ 和基 I/O 地址。某些设备还必须被分配一个唯一的 DMA。
- **适配卡**：配置大多数 PCI 适配卡非常简单。配置其他类型的卡，尤其是 ISA 即插即用卡，可能会更加困难。
- **设备支持**：Red Hat Linux 在几个级别上支持设备。第一层（Tier 1）设备完全支持。第二层（Tier 2）设备部分支持。第三层（Tier 3）设备兼容但不支持。其他设备可能与 Red Hat Linux 不兼容。
- **硬盘**：BIOS 可以通过物理地址或逻辑块地址访问硬盘。每种方法都对 Linux 内核的位置施加了限制。
- **分区**：最多可以定义四个主分区。此外，一个主分区可以被指定为扩展分区，并用于存放多达 12 个逻辑分区。
- **分区类型**：最重要的 Linux 分区类型是存放程序和数据文件的 Linux 原生分区，以及存放临时交换到硬盘的物理内存内容的 Linux 交换区。
- **挂载点**：Linux 通过将每个分区与挂载点关联，将分区集成在单个文件系统中。

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- 基 I/O 地址 (base I/O address)
- 块设备 (Block devices)
- 总线 (bus)
- 字符设备 (Character devices)
- 直接内存访问 (DMA)
- 磁盘几何结构 (disk geometry)
- 扩展分区 (extended partition)
- Intel 架构 (Intel architecture)
- I/O 端口 (I/O ports)
- IRQ
- 逻辑块寻址 (Logical block addressing)
- 逻辑分区 (logical partitions)
- 挂载点 (mount point)
- 分区 (partitions)
- 分区类型 (partition types)
- 即插即用 (plug-and-play)
- 主分区 (primary partitions)
- Red Hat 硬件兼容性列表 (Red Hat Hardware Compatibility List)
- 对称多处理 (symmetric multiprocessing)
- WinModems

## 其他信息来源

如果您想进一步了解本章介绍的主题，请参考以下资料：

- *The Complete PC Upgrade & Maintenance Guide*, 第 11 版, Mark Minasi 著 (Sybex, 2000)
- Linux HOWTOs
    - *Busmouse-HOWTO*, Chris Bagwell 著
    - *Ethernet-HOWTO*, Paul Gortmaker 著
    - *Ftape-HOWTO*, Claus-Justus Heine 著
    - *IR-HOWTO*, Werner Heuser 著
    - *Modem-HOWTO*, David S. Lawyer 和 Greg Hankins 著
    - *Multi-Disk-HOWTO*, Stein Gjoen 著
    - *PCMCIA-HOWTO*, David Hines 著
    - *Plug-and-Play-HOWTO*, David S. Lawyer 著
    - *Serial-HOWTO*, David S. Lawyer 和 Greg Hankins 著
    - *Sound-HOWTO*, Jeff Tranter 著
    - *UPS-HOWTO*, Harvey J. Stein 著
- Linux mini-HOWTOs，例如 *Alsa-sound* 和 *Cable-Modem mini-HOWTOs*

## 复习题

1. 在配置设备时，通常必须分配以下哪项？
    A. 总线 (Bus)
    B. DMA
    C. I/O 端口 (I/O port)
    D. IRQ

2. 以下哪种适配卡类型最容易配置？
    A. EISA
    B. ISA
    C. ISA 即插即用 (ISA plug-and-play)
    D. PCI

3. 哪种寻址方法通常要求 Linux 内核位于硬盘的前 1024 个柱面内？
    A. 逻辑块 (Logical block)
    B. 逻辑字节 (Logical byte)
    C. 物理 (Physical)
    D. 虚拟 (Virtual)

4. 以下哪些与 Red Hat, Inc. 支持的设备相关？
    A. 第一层 (Tier 1)
    B. 第二层 (Tier 2)
    C. 第三层 (Tier 3)
    D. 不兼容 (Incompatible)



5. 在 32 位 Intel 架构系统上运行的 Red Hat Linux 可以访问的最大物理内存是多少？

- A. 2GB
- B. 4GB
- C. 8GB
- D. 64GB

6. Linux 系统可以访问的最大交换内存（swap memory）是多少？

- A. 2GB
- B. 4GB
- C. 16GB
- D. 64GB

## 复习题答案

1. B, C, 和 D。设备连接到总线，但总线不必分配给该设备。
2. D. PCI 卡是即插即用的，通常可以由 BIOS 自动配置。
3. C. 逻辑块寻址 (LBA) 要求内核位于硬盘的前 8GB 范围内。逻辑字节和虚拟（virtual）不是磁盘寻址形式。
4. A 和 B，Tier 3 设备与 Linux 兼容，但不受 Red Hat, Inc. 支持。不兼容的设备不受 Red Hat Linux 支持。
5. B. 当 Red Hat Linux 在 32 位 Intel 架构系统上运行时，它最多可以访问 4GB 的 RAM。
6. A. 一个交换分区最大可达 2GB，而一个 Linux 系统最多可以有八个交换分区。然而，当 Red Hat Linux 在 32 位 Intel 架构系统上运行时，它最多可以访问 4GB 的虚拟内存。由于部分虚拟内存必须代表物理内存，因此最佳答案是 2GB。

# 第 3 章：Unix 基础

**本章涵盖的 RHCE 准备主题：**

- **使用 Unix 命令行。**
    - 有效地使用基础 Unix 命令。
    - 理解并使用文件所有权和权限。
    - 理解 Linux 文件系统结构。
    - 使用并操作路径。
    - 编辑文本文件。
    - 打印文件。

- **管理文件系统。**
    - 备份和恢复文件。
    - 挂载和卸载文件系统。
    - 使用可移动介质，如软盘。
    - 创建文件系统。
    - 对硬盘进行分区。
    - 检查文件系统。

- **使用 Unix 命令设施。**
    - 使用流重定向和过滤器。
    - 使用正则表达式指定命令选项和参数。
    - 编写采用环境变量和控制结构的 shell 脚本。

RHCE 考试的安装和故障排除部分并不专门测试你在使用 Unix 命令行方面的知识和技能。然而，除非你精通使用 Unix 命令行，否则你将无法完成这些考试部分。本章将回顾使用 Unix 命令的基础知识，然后进入对系统管理员至关重要的特殊主题，包括文件系统管理和 shell 脚本。

如果你缺乏之前的 Unix 使用经验，你应该在学习本章之外进一步研究 Unix。虽然本章涵盖了许多重要的 Unix 主题，但单一的章节无法描述 Unix 命令的每一个特性，甚至无法描述每一个重要特性。

另一方面，那些熟悉 Linux 以外的其他 Unix 变体的人可能会发现本章并不特别困难。例如，许多 Unix 系统使用标准的 Linux shell —— bash shell，它是原始 Bourne shell 的衍生版本。因此，本章经常提到 Unix 而非 Linux，因为其内容具有广泛的适用性，即使没有 X 窗口系统也可以使用。

## 使用 Unix 命令行

那些仅使用图形用户界面 (GUI) 的人有时会惊讶地发现，Unix 的图形用户界面 X 并非总是可用。某些 Unix 系统，特别是网络服务器，可能根本没有安装 X。此外，即使安装了 X，如果系统配置错误，X 也可能无法运行。因此，Red Hat Linux 管理员必须熟悉 Unix 命令行。

## 基础 Unix 命令

虽然 Red Hat Linux 提供了 1,000 多个命令，但你不需要全部掌握。熟悉十几个命令就足以让你执行最常见的任务。表 3.1 总结了最重要的 Unix 命令。接下来的小节将详细解释这些命令。

**表 3.1 基础 Unix 命令**

| 命令 | 功能 |
| :--- | :--- |
| cd | 更改当前工作目录。 |
| cp | 复制文件。 |
| find | 查找文件。 |
| less | 每次分页滚动浏览文本文件。 |
| ls | 列出文件及其特性。 |
| man | 描述命令和配置文件。 |
| mkdir | 创建目录。 |
| mv | 将文件移动到另一个文件夹或重命名文件。 |
| pwd | 显示当前工作目录的名称。 |
| rm | 删除文件。 |
| rmdir | 删除目录。 |
| touch | 调整文件的修改日期。 |

### cd

Unix 目录类似于 GUI 中使用的文件夹。目录可以包含文件和其他目录。

每个 Unix 用户或进程都与一个目录相关联，称为 *当前工作目录* (current working directory)，或者简单地称为 *当前目录* (current directory)。当引用一个文件时，除非明确指定路径信息，否则假定该文件位于当前工作目录中。这一特性使得引用当前目录中的文件变得非常方便。

你可以通过执行 `cd` 命令来更改当前目录。例如，以下命令

```
cd /home/fred
```

将 `/home/fred` 目录设为当前目录。请注意，Unix 目录使用正斜杠 (`/`) 来分隔路径的组成部分。你很快就会学习更多关于 Unix 目录的知识。如果你在执行 `cd` 命令时不带参数，你的主目录将成为当前工作目录。

### cp

`cp` 命令用于复制文件。你可以用它来复制单个文件。例如，以下命令

```
cp filex filey
```

将 `filex` 复制为 `filey`。你也可以使用 `cp` 命令来复制一组文件。例如，以下命令

```
cp filex filey folder1
```

将 `filex` 和 `filey` 复制到 `folder1` 中。

### find

`find` 命令帮助你定位文件。`find` 命令提供了多种查找文件的方法，但最常用的是通过文件名查找。当你拥有许多目录且不确定哪个目录包含该文件时，这非常有用。例如，以下命令

```
find /home/fred -name filex
```

将告知你 `/home/fred` 目录下的哪个文件夹包含 `filex` 文件。如果你不知道文件的完整名称，但知道文件名中包含的某个字符串，你可以使用如下命令：

```
find /home/fred -name '*file*'
```

该命令将查找位于 `/home/fred` 及其子目录下，且文件名包含字符 `ile` 的所有文件。

### less

`less` 命令允许你分页浏览文本文件，就像 `man` 命令允许你分页浏览 man 手册页一样。你使用相同的字符来控制这两个程序。例如，要分页浏览 `/etc/hosts` 文件，请执行命令

```
less /etc/hosts
```

### ls

`ls` 命令列出文件及其特性。它有许多选项和参数；本节仅描述最常用的部分。

在没有任何选项或参数的情况下，`ls` 命令会列出当前目录中文件的名称。如果你想列出其他目录，请执行如下命令

```
ls /home/bob
```

这将列出 `/home/bob` 目录中文件的名称。例如，你可能会看到如下输出：

```
Desktop My Documents Sara.wab WAB.EXE sara.blt sounds
```

正如后面解释的，如果你缺乏访问指定目录的适当权限，该命令将向你显示错误消息。

`ls` 命令的一个重要选项是使其在列出文件名的同时列出文件的特性。例如，以下命令

```
ls -l /home/bob
```

可能会产生如下输出：

```
total 137
drwxr-xr-x  5 bob  bob  1024 Nov 26 10:35 Desktop
drwxr-xr-x 14 bob  bob  1024 Nov 26 10:38 My Documents
-rwxr----  1 bob  bob 115030 Nov 26 13:15 Sara.wab
-rwxr---   1 bob  bob  14768 Mar 13  1997 WAB.EXE
-rw-r--r-- 1 bob  bob  2089 Nov 26 10:36 sara.blt
drwxr-xr-x  2 bob  bob  2048 Nov 26 10:39 sounds
```

第一行告诉你 `/home/bob` 目录中的文件总共占用了 137 个磁盘块。随后的每一行描述其中一个文件。



第一列宽 10 个字符，指定该特定文件的文件权限。您很快就会详细了解它们。目前，只需知道如果文件权限以 `d` 开头，则该行描述的是一个目录；否则，它描述的是一个文件。例如，`Desktop` 是一个目录，而 `Sara.wab` 是一个文件。

第二列给出了文件或目录所使用的目录块（inodes）数量。例如，目录 `Desktop` 使用了五个块。

第三列给出了拥有该文件的用户的名称。这通常是创建该文件的用户。用户 `bob` 拥有列出的所有文件。

第四列给出了拥有该文件的用户组名称。Red Hat Linux 为每个用户建立一个组，该用户是其唯一成员。作为系统管理员，您可以根据需要建立额外的组并分配成员。组 `bob` 拥有列出的所有文件。

第五列给出了文件的大小（字节）或目录项的大小（字节）。例如，文件 `Sara.wab` 的大小为 115030 字节。

第六到第八列给出了文件最后修改的日期和时间。如果文件长时间未被修改，则仅显示日期。例如，文件 `Sara.wab` 在去年 11 月 26 日下午 1:15 被修改。

最右侧的列提供了该行所描述的文件名称。

### man

`man` 命令用于描述命令和配置文件。您可以使用此命令来了解命令选项和参数。要查看某个命令的 man 页，请执行如下命令：

```bash
man find
```

该命令会显示 `find` 命令的选项和参数，并描述该命令的操作。

当 man 页较长时，`man` 命令通过提供一个简单的分页设施来帮助您，您可以使用它滚动查看输出页面。通过输入以下字符之一，您可以控制 `man` 命令的输出：

- **Space**：向前翻一页。
- **b**：向后翻一页。
- **q**：终止命令。

### mkdir

`mkdir` 命令用于创建目录。例如，命令

```bash
mkdir newfolder
```

会创建一个名为 `newfolder` 的目录。新目录是当前目录的子目录。如果您想将新目录放在其他地方，请使用如下命令：

```bash
mkdir /tmp/newfolder
```

这会创建 `/tmp` 的一个子目录，且 `/tmp` 必须已经存在。

### mv

您可以使用 `mv` 命令重命名文件。例如，命令

```bash
mv filex filey
```

将 `filex` 重命名为新文件名 `filey`。您还可以使用 `mv` 命令将一个或一组文件从一个目录移动到另一个目录。例如，命令

```bash
mv filex filey /home/bob
```

将文件 `filex` 和 `filey` 从当前工作目录移动到 `/home/bob` 目录。

### pwd

`pwd` 命令显示当前工作目录的名称。此命令不需要选项或参数。

### rm

`rm` 命令用于删除文件。例如，命令

```bash
rm filex filey
```

会删除 `filex` 和 `filey`。通常，文件一旦被删除就无法恢复，因此在使用 `rm` 命令时应非常小心。您可以通过指定如下命令来删除一个目录及其包含的所有文件：

```bash
rm -rf dir
```

### rmdir

`rmdir` 命令用于删除目录。例如，命令

```bash
rmdir folderx foldery
```

会删除位于当前目录中的 `folderx` 和 `foldery` 目录。这些目录必须为空，否则命令将失败。要删除包含文件的目录，请使用 `rm -rf` 命令。

### touch

`touch` 命令用于更新与文件相关的访问时间和修改时间。例如，命令

```bash
touch mydata
```

将文件 `mydata` 的访问和修改时间设置为当前时间。如果您 `touch` 一个不存在的文件，Unix 将创建一个具有指定文件名的空文件。

现在尝试练习 3.1，看看您是否已经掌握了刚刚介绍的一些基础 Unix 命令。

## 练习 3.1：基础 Unix 命令

1. 以非 root 用户身份登录。
2. 将当前工作目录更改为 /tmp。
3. 将当前工作目录更改为您的主目录。
4. 通过执行以下命令创建文件 ex3.1：`touch ex3.1`
5. 将该文件复制为文件 ex3.1.SAVE。
6. 将文件 ex3.1.SAVE 重命名为 ex3.1.BACKUP。
7. 创建一个名为 testdir 的目录。
8. 将文件 ex3.1 移动到 testdir 目录中。
9. 删除文件 ex3.1.BACKUP。
10. 删除目录 testdir 及其内容。
11. 查找文件 /passwd 的位置。

## 文件所有权与权限

`ls` 命令显示指定目录中文件的 *文件所有权* 和 *文件权限*；如果未指定目录，则显示当前目录中的文件。您可以通过执行若干命令来操作这些文件特性。

您可以通过执行 `chown` 命令来更改文件或一组文件的所有者。例如，命令

```bash
chown bill filex filey
```

使用户 `bill` 成为文件 `filex` 和 `filey` 的所有者。只有系统管理员 `root` 才能使用 `chown` 命令更改文件的所有权；普通用户可以使用该命令更改其所拥有文件的组所有权。

同样，您可以通过执行 `chgrp` 命令来更改文件的组所有权。例如，命令

```bash
chgrp bill filex filey
```

使组 `bill` 成为文件 `filex` 和 `filey` 的新组所有者。使用 `chgrp` 命令不需要是系统管理员。您可以将您所拥有文件的组所有权更改为您所属的任何组。

系统管理员可以通过执行 `chown` 命令来更改文件的所有权和组所有权。例如，命令

```bash
chown bill.bob filex
```

使 `bill` 成为文件 `filex` 的所有者，`bob` 成为组所有者。

文件权限决定了谁可以读取、写入和执行文件。目录权限还决定了谁可以向目录中添加和删除文件、列出目录中的文件名以及访问目录中的文件。每种操作都与一个字符相关联，如表 3.2 所示。

### 表 3.2 文件和目录访问权限

| 权限 | 文件权限 | 目录权限 |
| :--- | :--- | :--- |
| r | 允许读取文件 | 允许列出目录内容 |
| w | 允许写入文件 | 允许在目录内创建和删除文件 |
| x | 允许执行文件 | 允许访问目录内的文件 |
| - | 不允许访问 | 不允许访问 |

Unix 为文件的所有者、组所有者和其他用户分别分配一套权限。`ls` 命令按此顺序显示权限。例如，权限 `rw-r-----` 允许对文件进行以下操作：

- **所有者 (rw-)**：文件的所有者可以读取和写入，但不能执行该文件。
- **组 (r--)**：拥有该文件的组成员可以读取，但不能写入或执行该文件。
- **其他 (---)**：其他用户不能访问该文件。

您可以使用 `chmod` 命令的两种形式之一来操作文件或目录权限。第一种形式将权限表示为数字，如表 3.3 所示。

### 表 3.3 数字形式的文件和目录访问权限

| 权限 | 数字 |
| :--- | :--- |
| r | 4 |
| w | 2 |
| x | 1 |
| - | 0 |

要形成一个权限值，需将这些数字相加。例如，权限 `rwx` 的值为 7，权限 `r-x` 的值为 5。然后按以下顺序指定权限总和：用户，

组（group）以及其他人（other）。例如，权限 `rw-r-----` 将被指定为 640。以下 `chmod 命令使用数字来指定文件权限：

```bash
chmod 640 filex
```

此命令将文件 `filex` 的权限设置为 `rw-r-----`。`chmod` 命令支持另一种指定权限的方式，即将字母与用户关联，如表 3.4 所示。

### 表 3.4 用于指定权限的用户标识

| 用户 | 标识 |
| :--- | :--- |
| 所有者 (owner) | u |
| 组所有者 (group owner) | g |
| 其他人 (other) | o |

这些标识与表 3.2 中显示的字母结合使用，用于向文件或目录添加或删除权限。例如，要确保组员可以读取某个文件，请执行如下命令：

```bash
chmod g+r filex
```

此命令允许文件的所有者以及拥有该文件的组成员读取该文件。要确保其他人无法访问该文件，请执行如下命令：

```bash
chmod o-rwx filex
```

此命令禁用了除所有者和组成员以外的其他用户对该文件的读取、写入和执行权限。

当你创建文件时，其访问权限是根据 `umask` 命令指定值的补码来设置的。你可以通过用 7 减去每个数字来计算补码。例如，如果你执行以下命令：

```bash
umask 027
```

则 `umask` 值的补码为 750。然而，一个新创建的文件永远不会被自动设置为可执行，因此有效值为 640。因此，在 `umask` 值为 027 的情况下，你将能够读写任何你创建的文件，你的默认组成员将能够读取这些文件，而其他人将无法以任何方式访问这些文件。当然，在创建文件后，你可以执行 `chmod` 命令来为该特定文件建立你想要的精确权限。请参阅练习 3.2 以确认你理解如何分配文件和目录的所有权及权限。

## 练习 3.2：文件和目录的所有权与权限

- 1. 以 root 身份登录。
- 2. 通过执行命令 `touch ex3.2` 创建文件 ex3.2。
- 3. 使用 `ls` 命令确定谁被允许读取该文件，谁被允许写入该文件，以及谁被允许执行该文件。
- 4. 将文件的所有者更改为 `bin`。
- 5. 将文件的组所有者更改为 `nobody`。
- 6. 设置文件权限，使 `bin` 能够读取并执行该文件。
- 7. 设置文件权限，允许 `nobody` 组的成员执行该文件。
- 8. 设置文件权限，允许其他用户读取该文件。

## 理解 Red Hat Linux 文件系统

表 3.5 总结了组成 Red Hat Linux *文件系统* 的主要目录。请确保你熟悉每个目录及其内容。

### 表 3.5 重要的 Red Hat Linux 目录

| 目录 | 内容 |
|---|---|
| / | 系统根目录 |
| /bin | 常用命令和程序 |
| /boot | Linux 内核及引导相关文件 |
| /dev | 设备文件 |
| /etc | 配置文件 |
| /home | 用户主目录 |
| /lib | 共享库 |
| /lost+found | 损坏的文件 |
| /mnt | 文件系统的挂载点 |
| /proc | 系统状态信息 |
| /root | root 用户的主目录 |
| /sbin | 系统管理命令和程序 |
| /tmp | 临时文件 |
| /usr/X11R6 | X 命令和程序 |
| /usr/bin | 常用命令和程序 |
| /usr/doc | 文档 |
| /usr/games | 游戏 |
| /usr/include | 头文件 |
| /usr/info | 在线文档 |
| /usr/lib | 共享库 |
| /usr/local | 本地安装的文件 |
| /usr/man | 手册页 |
| /usr/sbin | 系统管理命令和程序 |
| /usr/share | 共享信息 |
| /usr/src | 源代码 |
| /var | 日志文件、打印队列文件和其他动态文件 |

按照练习 3.3 中的步骤，学习表 3.5 中列出的每个目录中包含哪些类型的文件和子目录。

## 练习 3.3：遍历 Linux 文件系统

- 1. 从计算机系统的根目录开始。
- 2. 参考表 3.5，移动到列出的每个目录，并使用 `ls -l` 命令列出其内容。
- 3. 注意其中存在的文件和子目录类型。

## 使用和操作路径 (Path)

Unix 命令存储在多个目录中。Shell 拥有一个目录列表，称为路径（path），存储在 PATH 环境变量中。当你执行一个 Unix 命令时，Shell 会在路径中搜索你调用的命令并运行它。

你可以通过执行以下命令来查看路径：

```bash
echo $PATH
```

你将看到类似于以下内容的输出：

```
/usr/bin:/bin:/bin:/usr/X11R6/bin
```

在这种情况下，路径由三个目录组成：/usr/bin、/bin 和 /usr/X11R6/bin。每个条目之间用冒号 (:) 分隔。

你可以通过执行如下命令将目录添加到路径中：

```bash
export PATH=/sbin:$PATH
```

这将把目录 /sbin 添加到路径的最前面，以便首先搜索它。要将目录添加到路径的末尾，请执行如下命令：

```bash
export PATH=$PATH:/sbin
```

你可以通过执行如下命令来查找命令所在的目录（假设该命令位于路径中的某个目录中）：

```bash
which ls
```

`which` 命令会报告 `ls` 命令的位置。

请参阅练习 3.4 以验证你理解如何查看路径内容并查找其中存在的目录。

## 练习 3.4：查看路径

- 1. 查看你的路径内容。其中存在哪些目录？

## 编辑文件

要编辑文本文件，你需要使用文本编辑器。两种流行的 Unix 编辑器是 `vi` 和 `pico`。这两个文本编辑器都比较紧凑，这意味着即使在系统硬盘空间很少或没有空间的情况下也可以使用。`vi` 编辑器功能更强大，但精通 `vi` 需要大量的练习。

`pico` 编辑器（与流行的电子邮件客户端 `pine` 一起使用）学习和使用起来简单得多。要使用 `pico` 编辑文件，请执行如下命令：

```bash
pico file
```

或者，要创建新文件，只需在不带参数的情况下执行 `pico` 命令：

```bash
pico
```

`pico` 启动后，你将看到如图 3.1 所示的屏幕。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_83_0.png)

大多数 `pico` 命令要求你按住 Ctrl 键并输入一个表示要执行操作的字母。屏幕底部的菜单会提醒你最常用的命令；脱字符 (^) 表示使用 Ctrl 键。表 3.6 总结了最重要的 `pico` 命令。光标导航键、Enter 键、Backspace 键和 Delete 键具有其常用的含义。

### 表 3.6 重要的 pico 命令

| 命令 | 功能 |
| :--- | :--- |
| ^G | 获取帮助。 |
| ^J | 两端对齐一段文本。 |
| ^K | 剪切文本。 |
| ^O | 将编辑缓冲区写入文件。 |
| ^R | 读取文件并将其内容插入编辑缓冲区。 |
| ^U | 粘贴剪切的文本。 |
| ^V | 向下翻页。 |
| ^X | 退出程序。 |
| ^Y | 向上翻页。 |

请参阅练习 3.5 以检查你现在是否理解如何使用文本编辑器查看文件内容并创建新文件。

## 练习 3.5：使用文本编辑器

- 1. 使用文本编辑器查看 `/etc/passwd` 文件的内容。不要更改此文件的内容。
- 2. 使用文本编辑器创建一个名为 `ex3.5` 的文件。将你当前的待办事项列表输入到该文件中。

## 打印文件

要打印文件，请执行如下命令：

```bash
lpr filex
```

这将打印文件 `filex`。要将文件打印到特定的打印机，请执行如下命令：

```bash
lpr -P lj4 filex
```

其中 `lj4` 是已配置打印机的名称。

请参阅练习 3.6 以检查你现在是否理解如何打印文件。

## 练习 3.6：打印文件

- 1. 打印你在练习 3.5 步骤 2 中创建的文件。

## 管理文件系统

系统管理员必须能够执行普通用户通常不执行的各种操作。这些操作包括备份和还原文件、挂载和卸载文件系统、分区磁盘、创建文件系统以及检查文件系统。本节将解释如何执行这些操作。本节中的大多数命令只能由 `root` 执行。如果命令执行失败，请检查确保你指定正确。如果正确，请尝试以 `root` 身份重新执行该命令。

### 备份和还原文件

有几个 Unix 命令可以备份和还原文件。最流行的备份和还原命令是 `tar`。要使用 `tar` 备份文件或目录，请执行如下命令：

```bash
tar cvf tarfile.tar filex filey dirz
```

此命令备份文件 `filex`、`filey` 和目录 `dirz`，并将备份存储在文件 `tarfile.tar` 中。

要还原备份，请执行如下命令：

```bash
tar xvf tarfile.tar
```



您可以压缩备份文件，以减少存储它所需的磁盘空间。在创建备份时，若要指定压缩，请执行如下命令：

```bash
tar zcvf tarfile.tgz filex filey dirz
```

其中 `z` 表示压缩。如果备份文件被压缩过，在还原文件时必须使用 `z` 选项：

```bash
tar zxvf tarfile.tgz
```

现在，请通过完成练习 3.7 来测试您对备份和还原文件步骤的理解。

## 练习 3.7：备份和还原文件

- 1. 使用 `tar` 命令备份主目录中的文件和目录。
- 2. 移动到 `/tmp` 目录并还原备份，从而复制主目录中的文件。
- 3. 使用 `rm -rf` 命令删除还原的文件。

## 挂载和卸载文件系统

在访问文件系统包含的文件之前，必须先挂载该文件系统。要挂载文件系统，请执行如下命令：

```bash
mount -t ext2 /dev/hdb1 /mnt/data
```

该命令将位于分区 `/dev/hdb1` 上的 `ext2` 文件系统挂载为 `/mnt/data` 目录（该目录在执行命令前必须已存在）。可以指定 `ext2` 以外的文件系统类型；例如，要挂载 MS-DOS (FAT-16) 文件系统，请将文件系统类型指定为 `msdos`。您可以通过指定 `ro` 选项来以只读方式挂载文件系统：

```bash
mount -t ext2 /dev/hdb1 /mnt/data -o ro
```

当您完成对文件系统的访问后，可以通过执行如下命令将其卸载：

```bash
umount /dev/hdb1
```

或者

```bash
umount /mnt/data
```

> 如果文件系统正在被使用，您将无法卸载它。如果您的当前工作目录（或另一位用户的工作目录）是已挂载文件系统中的某个目录，那么该文件系统就在使用中，您将无法卸载它。在尝试卸载之前，请将当前工作目录更改为文件系统之外的目录。

现在请完成练习 3.8，尝试自行挂载和卸载文件系统。

## 练习 3.8：挂载和卸载文件系统

- 1. 如果 CD-ROM 已挂载，请将其卸载。
- 2. 将 Red Hat Linux CD-ROM 光盘挂载到 `/redhat` 目录。
- 3. 将一个文件从 CD-ROM 光盘复制到您的主目录。
- 4. 删除复制的文件。
- 5. 卸载 CD-ROM 光盘。

## 使用可移动介质介

熟悉 MS-DOS 的用户可能习惯于随意插入和取出可移动介质（如软盘）。然而，在 Unix 下，可移动介质上的文件系统必须被挂载才能被访问。反之，在取出介质之前，应先卸载该文件系统。未能卸载文件系统可能会导致数据损坏或文件系统崩溃。

> GNOME 和 KDE 环境提供了操作可移动介质的便捷方式。在挂载和卸载介质时，您可能会更倾向于在图形界面环境下操作。

## 创建文件系统

要创建 Linux 文件系统，请执行 `mke2fs` 命令：

```bash
mke2fs /dev/hdb2
```

指定文件系统所在的分区（例如 `/dev/hdb2`）。

要初始化交换分区，请执行以下命令：

```bash
mkswap /dev/hdb3
```

指定交换分区（例如 `/dev/hdb2`）。

**警告**：创建文件系统或初始化交换分区会破坏该分区上任何现有的文件系统。请务必指定正确的分区。

请参阅练习 3.9 以检查您是否已理解如何创建文件系统。

### 练习 3.9：创建文件系统

- 1. 将一张 MS-DOS 格式的软盘放入软驱。
- 2. 在软盘上创建一个 `ext2` 文件系统。
- 3. 将该文件系统挂载到您选择的挂载点。
- 4. 将 `/etc/passwd` 文件复制到软盘的文件系统中。
- 5. 卸载软盘。

## 硬盘分区

Red Hat Linux 安装程序提供了一个基于文本的界面，允许您将硬盘划分为*分区*（partitions），即磁盘空间上的连续区域，您可以在其上创建文件系统。这个过程被称为*磁盘分区*（disk partitioning）。或者，在安装期间和安装之后，您可以使用 `fdisk` 命令对硬盘进行分区。要启动 `fdisk` 工具，请执行 `fdisk` 命令并指定您希望分区的硬盘作为参数。例如，以下命令：

```bash
fdisk /dev/hdb
```

允许您对第二个 IDE 硬盘进行分区。一旦 `fdisk` 启动，它会显示一个提示符，告知您已准备就绪：

```
Command (m for help):
```

表 3.7 总结了最重要的 `fdisk` 命令。

### 表 3.7 重要的 fdisk 命令

| 命令 | 动作 |
| :--- | :--- |
| a | 切换活动分区标志。 |
| d | 删除分区。 |
| l | 列出已知的分区类型。 |
| n | 添加新分区。 |
| o | 创建一个新的空分区表。 |
| p | 打印（显示）分区表。 |
| q | 退出且不保存更改。 |
| t | 设置分区类型。 |
| u | 将显示单位在柱面（cylinders）和扇区（sectors）之间切换。 |
| v | 验证分区表。 |
| w | 将分区表写入磁盘并退出。 |

通常，启动 `fdisk` 后的第一步是执行 `p` 命令来显示分区表。结果应类似于以下输出：

```
Disk /dev/hda: 255 heads, 63 sectors, 2489 cylinders
Units = cylinders of 16065 * 512 bytes

Device Boot Start End Blocks Id System
/dev/hda1 * 1 127 1020096 6 FAT16
/dev/hda2 128 2489 18972765 5 Extended
/dev/hda5 128 132 40131 83 Linux
/dev/hda6 133 387 2048256 83 Linux
/dev/hda7 388 898 4104576 83 Linux
/dev/hda8 899 962 514048+ 83 Linux
/dev/hda9 963 1090 1028128+ 83 Linux
/dev/hda10 1091 1157 538146 82 Linux swap
/dev/hda11 1158 2489 10699258+ 83 Linux
```

该输出中的数据含义如下：

- Device 列指示该行数据所描述的 Linux 分区名称。
- Boot 列包含一个星号，指示活动分区，即由 MS-DOS 引导程序启动的分区。
- Start 和 End 列给出了分区的起始和结束柱面编号。
- Blocks 列给出了分区的大小（以 1024 字节块为单位）。
- Id 和 System 列指定分区的类型，前者给出数值代码，后者给出描述性名称。

如果您使用的是逻辑块寻址（LBA）而非物理寻址，可以通过执行 `u` 命令将显示切换为扇区而非柱面编号。

要删除分区，请执行 `d` 命令，然后指定您希望删除的分区编号。

要创建新分区，请执行 `n` 命令并指定分区类型（主分区、扩展分区或逻辑分区）以及起始和结束值。然后，执行 `t` 命令并指定分区的数值类型。交换分区使用类型 82，普通分区使用类型 83。

当您指定完所有分区后，执行 `w` 命令写入修改后的分区表并退出程序。有时，分区表的更改需要您重启系统。如果收到此指示，请重启系统。

## 检查文件系统

要检查 Linux 文件系统的完整性，请执行如下命令：

```bash
e2fsck -f /dev/hdb2
```

指定您要检查的分区（例如 `/dev/hdb2`）。若要指定检查应包含坏块测试并自动修复错误，请像以下命令那样分别添加 `-c` 和 `-p` 选项：

```bash
e2fsck -f -c -p /dev/hdb2
```

## Unix 命令设施

本节将回顾重要的 Unix 命令设施，包括流重定向、正则表达式和 shell 脚本。关于 Unix 命令设施已有数本专著，因此这里无法涵盖所有细节。本节重点介绍这些设施中最实用的方面。如果您不熟悉本节的内容，请参阅本章末尾给出的参考资料。

### 使用流重定向

每个 Unix 进程都有以下三个标准流：

- **标准输入 (Standard Input)**：命令输入
- **标准输出 (Standard Output)**：命令输出
- **标准错误 (Standard Error)**：错误消息

表 3.8 总结了重要的流重定向操作符，它们允许您重定向这些输入和输出流。例如，以下命令：

```bash
ls -l > filelist
```

将 `ls` 命令的输出发送到文件 `filelist` 中。

#### 表 3.8 重要的重定向操作符

| 操作符 | 含义 |
| :--- | :--- |
| `< file` | 从 `file` 获取标准输入。 |
| `> file` | 将标准输出写入 `file`。 |
| `>> file` | 将标准输出追加到 `file`。 |



#### 表 3.8 重要重定向运算符（续）

| 运算符 | 含义 |
| :--- | :--- |
| >&2 | 将标准输出流写入标准错误流。 |
| 2> file | 将标准错误流写入 `file`。 |
| 2>&1 | 将标准错误流写入标准输出流。 |
| x \| y | 进程 y 将进程 x 的输出作为其输入。 |

## 使用正则表达式

Unix 的文件名通配（globbing）功能比 DOS 的通配符更强大，因为 Unix 采用了更强大的表达式，即*正则表达式*，来指定一组文件。表 3.9 总结了重要的 Unix 文件名元字符。

### 表 3.9 重要文件名元字符

| 元字符 | 匹配... |
| :--- | :--- |
| * | 任意长度（零个或多个字符）的字符串。 |
| ? | 任意单个字符。 |
| [abc...] | 任何指定的字符。可以使用连字符指定一个字符范围。例如，0-9 匹配任何数字。 |
| [!abc...] | 除指定字符外的任何字符。 |
| ~user | 指定用户的主目录。 |

如果你在元字符前加上反斜杠 (\)，该元字符的特殊含义将被忽略。同样，如果你将包含元字符的文本用单引号括起来，该元字符的特殊含义也会被忽略。然而，出现在双引号内的元字符仍保留其特殊含义。

## 创建和使用 Shell 脚本

Unix 命令行最重要的一点或许在于其命令语言是可扩展的：你可以编写自己的 shell 脚本，它们可以像任何其他 Unix 命令一样被执行。本小节将探讨与 shell 脚本相关的几个重要主题，包括 shell 脚本的结构、shell 脚本的控制结构以及环境变量。

### Shell 脚本的结构

Shell 脚本是包含 shell 命令的普通文本文件。最重要的 shell 命令之一是注释。任何以井号 (#) 开头的 shell 脚本行都被视为注释。

Shell 脚本的第一行应该是一个特殊的注释，它由注释字符 (#) 开头，紧随其后是一个感叹号 (!)，然后是 Unix 应该用来处理该 shell 脚本中命令的程序的路径名，通常是 /bin/bash。bash shell 是最常用的 Linux shell。

表 3.10 总结了 shell 脚本中使用的重要命令形式。

### 表 3.10 重要命令形式

| 形式 | 含义 |
| :--- | :--- |
| `cmd &` | 在后台执行 `cmd`。 |
| `cmd1 ; cmd2` | 执行 `cmd1`，随后执行 `cmd2`。 |
| `( cmd1 ; cmd2 )` | 将 `cmd1` 和 `cmd2` 视为一个命令组，依次执行。 |
| `cmd1 \`cmd2\`` | 将 `cmd2` 的输出作为 `cmd1` 的参数。 |
| `cmd1 && cmd2` | 执行 `cmd1`；仅在 `cmd1` 成功时执行 `cmd2`。 |
| `cmd1 \|\| cmd2` | 执行 `cmd1`；仅在 `cmd1` 失败时执行 `cmd2`。 |
| `{ cmd1 ; cmd2 }` | 在当前环境中依次执行 `cmd1` 和 `cmd2`。 |

## 环境变量

在 shell 脚本中，你可以使用被称为*环境变量*的变量。要为环境变量赋值，可以使用如下命令：

```
x=y
```

此赋值将值 `y` 放入环境变量 `x` 中。你可以通过如下命令将一个环境变量的值赋给另一个环境变量：

```
x=${y}
```

此赋值将环境变量 `y` 的值放入环境变量 `x` 中。花括号用于限定环境变量的名称，有时可以省略：

```
x=$y
```

关于花括号在何时至关重要的一个例子，请考虑以下命令：

```
x=${y}es
```

此赋值将环境变量 `y` 的值与字符串 `es` 拼接，并将结果放入环境变量 `x` 中。如果将命令写成：

```
x=$yes
```

则会将环境变量 `yes` 的值放入环境变量 `x` 中。要抵消用于引用环境变量的语法的特殊含义，请将表达式用单引号括起来，如下所示：

```
x=' $y'
```

此赋值将值 `$y` 放入环境变量 `x` 中。或者，你可以在元字符 `$` 前加上反斜杠，如下所示：

```
x=\$y
```

默认情况下，环境变量仅在直接的本地环境中可用。为了使从本地环境启动的程序和进程能够访问某个环境变量，请在 `export` 命令中指定该变量的名称，例如：

```
export x,y,z
```

或者

```
export x=$y
```

### 控制结构

可以使用几个命令来改变 shell 脚本命令标准的自上而下执行顺序。其中最重要的是 `if` 命令。本小节将解释 `if` 命令和其他几个重要的控制结构。

#### if 命令

每个 Unix 命令在完成时（无论正常终止还是异常终止）都会发布一个退出码。值 0 表示成功完成；其他值表示各种错误情况。`if` 命令测试一个命令的完成值。在其最简单的形式中，`if` 命令仅在被测试的命令成功时才执行一系列命令：

```
if test-command
then
    commands
fi
```

`if` 命令的另一种形式是根据被测试命令的成功或失败，在两组命令之间做出选择：

```
if test-command
then
    commands
else
    commands
fi
```

通常使用 `test` 命令作为 `if` 命令的被测命令。例如，以下命令：

```
if test -e /etc/hosts
```

用于测试文件 /etc/hosts 是否存在。表 3.11 总结了 `test` 命令的重要参数。

#### 表 3.11 重要 test 命令参数

| 条件 | 含义 |
| :--- | :--- |
| `-d file` | `file` 是一个目录。 |
| `-e file` | `file` 存在。 |
| `-f file` | `file` 是一个普通文件。 |
| `-r file` | `file` 可读。 |
| `-s file` | `file` 的大小大于 0。 |
| `-w file` | `file` 可写。 |
| `-x file` | `file` 可执行。 |
| `file1 -nt file2` | `file1` 比 `file2` 新。 |
| `file1 -ot file2` | `file1` 比 `file2` 旧。 |
| `s1 = s2` | 字符串 `s1` 与字符串 `s2` 完全相同。 |
| `s1 != s2` | 字符串 `s1` 与字符串 `s2` 不相同。 |
| `n1 -eq n2` | 整数 `n1` 等于整数 `n2`。 |
| `n1 -ge n2` | 整数 `n1` 大于或等于整数 `n2`。 |
| `n1 -gt n2` | 整数 `n1` 大于整数 `n2`。 |
| `n1 -le n2` | 整数 `n1` 小于或等于整数 `n2`。 |
| `n1 -lt n2` | 整数 `n1` 小于整数 `n2`。 |
| `n1 -ne n2` | 整数 `n1` 不等于整数 `n2`。 |
| `! cnd` | 当且仅当条件 `cnd` 为假时，结果为真。 |

#### 表 3.11 重要 test 命令参数（续）

| 条件 | 含义 |
| :--- | :--- |
| `cnd1 -a cnd2` | 如果条件 cnd1 和条件 cnd2 同时为真，则结果为真。 |
| `cnd1 -o cnd2` | 如果条件 cnd1 或条件 cnd2 其中之一为真，则结果为真。 |

#### case 命令

`if` 命令提供单向分支，`if` 命令与 `else` 命令的组合提供双向分支，而 `case` 命令则提供多路分支：

```
case string
    in
        pattern1)
            commands
            ;;
        pattern2)
            commands
            ;;
        (etc.)
esac
```

#### while 和 until 命令

`while` 命令执行一系列命令，直到关联的测试命令被测试并发现为假为止：

```
while
    test-command
do
    commands
done
```

类似的 `until` 命令执行一系列命令，直到关联的测试命令被测试并发现为真为止：

```
until
    test-command
do
    commands
done
```

#### for 命令

`for` 命令迭代地执行一系列命令，为指定列表中的每个成员执行一次：

```
for list
do
    commands
done
```

`for` 命令的另一种形式是将当前列表成员的值赋给一个指定的变量：

```
for x in list
do
    commands
done
```

在每次迭代期间，变量 x 保存当前列表成员的值。

#### break 命令

`break` 命令可用于 `for`、`while` 或 `until` 命令的主体中。执行时，它会立即终止循环。

#### continue 命令

`continue` 命令可用于 `for`、`while` 或 `until` 命令的主体中。执行时，它会立即结束循环的当前迭代。

#### exit 命令

`exit` 命令终止 shell 脚本的执行，并将退出码设置为其参数所指定的数值：

```
exit 0
```



## 总结

在本章中，你学习了最常用的 Unix 命令。涵盖的最重要主题包括：

- **基础 Unix 命令** 虽然 Linux 拥有超过一千条命令，但你只需要掌握十几个常用的命令即可。
- **文件所有权和权限** 文件拥有所有者和组所有者。所有者、组所有者和其他用户被分配了读取、写入或执行文件的访问权限。
- **Red Hat Linux 文件系统** Red Hat Linux 建立了大约二十个标准目录，每个目录包含特定类型的程序或文件。
- **PATH 环境变量** PATH 环境变量指定了 shell 搜索程序以定位程序的目录。
- **编辑文件** `pico` 编辑器是一个简单的编辑器，适用于系统管理。
- **备份和还原文件** `tar` 命令对于备份和还原文件非常有用。
- **文件系统** `mke2fs` 命令用于创建 Linux 文件系统。`mount` 和 `umount` 命令分别用于挂载和卸载文件系统。
- **分区** `fdisk` 程序允许你建立硬盘分区。
- **重定向** 你可以重定向 Unix 命令的输入和输出。
- **正则表达式** 你可以使用正则表达式来指定文件名和一组文件名。
- **环境变量** 你可以使用环境变量来存储数值。
- **控制结构** Shell 脚本可以包含有条件地或迭代地执行系列命令的指令。

### 关键术语

在进入下一章之前，请确保你熟悉以下术语：

- 当前目录 (current directory)
- 当前工作目录 (current working directory)
- 环境变量 (environment variables)
- 文件所有权 (file ownership)
- 文件权限 (file permissions)
- 文件系统 (file system)
- 分区 (partitions)
- 路径 (path)
- 正则表达式 (regular expressions)

## 其他信息来源

如果你想进一步了解本章中介绍的主题，可以参考以下资源：

- *Unix Complete*, Peter Dyson, Stan Kelly-Bootle, John Heilborn (Sybex, 1999)

## 复习题

1. 哪个 Unix 命令用于重命名文件？
    A. cp
    B. mv
    C. rename
    D. rn

2. 对于权限为 `rwxr------;` 的文件，可以执行哪些操作？
    A. 任何用户都可以读取
    B. 其所有者可以读取
    C. 其所有者及其所属组的成员可以读取
    D. 无法读取

3. 哪个命令用于从压缩备份中还原文件？
    A. tar cvf
    B. tar xvf
    C. tar zcvf
    D. tar zxvf

4. 哪个命令用于创建 Linux 文件系统？
    A. fdisk
    B. mke2fs
    C. mkswap
    D. mount

5. 要将命令 x 的输出重定向为命令 y 的输入，应该使用哪个命令？
    A. x < y
    B. x > y
    C. x >> y
    D. x | y

6. 要将环境变量 x 的值设置为环境变量 y 的值，应该使用哪个命令？
    A. x=y
    B. x=$y
    C. x=${y}
    D. export x=$y

## 复习题答案

1. B. `mv` 命令将文件从一个名称或目录移动到另一个。`mv` 命令也可以用来重命名文件。

2. B 和 C. 该文件可由其所有者读取、写入和执行；它也可由其所属组的成员读取。

3. D. `tar zxvf` 从压缩的 (z) 备份中提取 (x) 文件。

4. B. `mke2fs` 命令创建标准的 Linux 文件系统。

5. D. 管道操作符 (`|`) 将一个命令的输出流连接到另一个命令的输入流。

6. B, C 和 D. 命令 `x=y` 将环境变量 x 的值设置为字符串 y，而不是环境变量 y 的值。

# 第 4 章：网络基础

本章涵盖的 RHCE 准备主题：

- 理解主机和网络的 IP 编址。
- 理解 TCP/IP 网络模型及其主要协议和服务。
- 理解 TCP/IP 路由。
- 理解常见 Linux 服务的功能。
    - 理解熟知的 TCP/IP 端口及相关的 TCP/IP 服务。
    - 理解 Red Hat Linux 如何启动和停止服务。
    - 知道如何启动和停止常见的 Linux 服务。

为了通过 RHCE 考试，你必须熟悉 TCP/IP 网络和常见的 TCP/IP 网络服务。本章回顾了 TCP/IP 网络和服务的 fundamentals。

如果你对本章的内容感到陌生，你应该参考其他资料，以便为 RHCE 考试做好充分准备。本章末尾列出了一些推荐书籍。

## TCP/IP 网络

曾经有多种协议在争夺主导地位。基于 TCP/IP（传输控制协议/网际协议）协议族的互联网的出现，基本上结束了这场竞争。除了封闭的私有网络外，如今大多数网络都使用 TCP/IP 作为其主协议。

本节描述 TCP/IP 主机和网络是如何编址的。接下来的章节将描述 TCP/IP 网络如何运作以及 TCP/IP 网络提供的服务。

### IP 地址

TCP/IP 网络由互连的计算机系统（称为主机）组成。每台主机有一个或多个 *IP 地址*，通常主机上安装的每个网络接口都有一个地址。TCP/IP 地址是 32 位数字，通常以点分十进制表示为 *四个八位组*（8 位值）的序列。例如，一个 TCP/IP 主机的 IP 地址可能是 192.168.1.1，这等同于 32 位整数 3,232,235,777 ($192 \times 256^3 + 168 \times 256^2 + 1 \times 256 + 1$)。

某些主机拥有一个或多个永久分配的 IP 地址，称为 *静态 IP 地址*。其他主机被分配一个临时 IP 地址，称为 *动态 IP 地址*。动态 IP 地址通常用于移动主机（如笔记本电脑）和拨入客户端。为其他主机提供服务的主机通常被分配一个静态 IP 地址，以便客户端能够使用一致的 IP 地址引用它们。正如你在本章后面将看到的，IP 地址是一种相对稀缺的资源。动态 IP 地址所需的 IP 地址池只需与活动主机的数量相当，而不需要涵盖主机的总数。

### 网络类

组织不会要求互联网管理机构为其分配单个 IP 地址。相反，他们请求一系列连续的 IP 地址，以便分配给其网络内的主机。IP 地址从三个类别中选择，通过第一个八位组的值来区分：

- 1.0.0.0—126.0.0.0 A 类网络地址
- 128.0.0.0—191.0.0.0 B 类网络地址
- 192.0.0.0—223.0.0.0 C 类网络地址

一个 IP 地址由两部分组成：*网络地址* 和 *主机地址*。网络地址是构成一个网络的所有直接连接主机的共同部分。主机地址将单个主机与网络上的其他主机区分开来。网络地址取自 IP 地址的高位，主机地址取自低位。网络地址的大小根据网络类而变化：

- A 类：8 位（1 个八位组）
- B 类：16 位（2 个八位组）
- C 类：24 位（3 个八位组）

由于 A 类地址的网络地址仅 8 位长，因此有 24 位可用作指定主机地址。因此，一个 A 类网络可以包含超过 1600 万台主机。相比之下，C 类网络的网络地址长 24 位；只有 8 位可用作指定主机地址。因此，一个 C 类网络只能包含 254 台主机（IP 地址 xxx.xxx.xxx.0 和 xxx.xxx.xxx.255 分配给了网络，因此只有 xxx.xxx.xxx.1—xxx.xxx.xxx.254 可用于主机）。

C 类网络看起来可能不如 A 类网络理想。然而，因为 A 类网络的网络地址仅由 8 位组成，因此只可能存在 126 个 A 类网络地址。所有这些地址早已被分配完毕，所以尽管你可能更倾向于 A 类地址，但你不太可能获得一个。C 类地址的 24 位网络地址可产生超过 1600 万个可能的网络地址。不幸的是，即使是 C 类地址也变得稀缺了。

> **注意** 一个新的 TCP/IP 标准 IPv6 将提供 128 位的 IP 地址。Linux 内核已经为 IPv6 提供了实验性支持。然而，IPv6 要在广泛支持和使用之前还需要好几年时间。

几个 IP 地址范围被专门分配：

- `127.0.0.0-127.255.255.255` 用于引用本地主机和网络（*回环地址*）。
- `224.0.0.0-239.0.0.0` 保留给组播协议使用。
- `240.0.0.0-255.0.0.0` 保留（请勿使用）。
- `10.0.0.0-10.255.255.255` 保留给私有网络。
- `172.16.0.0-172.31.255.255` 保留给私有网络。
- `192.168.0.0-192.168.255.255` 保留给私有网络。

你可以自由地从分配给私有网络的范围中分配 IP 地址。但是，你必须采取特殊步骤（例如实施 IP 伪装或网络地址转换，这些在第 30 章“使用 `ipchains` 配置防火墙”中有所描述），以使具有私有 IP 地址的主机能够访问其本地网络之外的主机。

### 子网划分

假设你有两个小型网络，每个网络大约包含十几个主机。你可以为每个网络请求一个 C 类网络地址。然而，C 类网络地址提供的 IP 地址远比你需要的多。如果你能以某种方式拥有一个（例如）26 位而非 24 位的网络地址，你就可以在构成单个 C 类网络地址的 IP 地址范围内托管多个网络。IP 地址中剩余的 6 位将允许你为每个网络分配多达 31 台主机。



子网划分（Subnetting）允许您在任何您喜欢的位置将 IP 地址拆分为网络地址和主机地址组件，而不仅仅是在字节边界处。您通过指定网络掩码（netmask）来指定构成网络地址的 IP 地址部分。网络掩码是一个 32 位字符串，在属于网络地址的每个位置上为 1，其他位置为 0。您使用与 IP 地址相同的点分十进制表示法来编写网络掩码。例如，一个标准的 C 类地址具有 255.255.255.0 的网络掩码：前三个字节全部为 1，最后一个字节全部为 0。要指定一个 26 位的网络地址，您可以使用 255.255.255.192 的网络掩码，其中最后一个字节的两个最高位为 1。

要理解主机 IP 地址的意义，您必须知道相关的网络。否则，您将无法确定哪些主机与该主机处于同一个本地网络中。

某些程序允许您将 IP 地址和网络掩码作为一对来指定。您先写 IP 地址，后面跟一个斜杠，然后写网络掩码中的位数。例如，192.168.1.100/24 指定了一个 IP 地址为 192.168.1.100 的主机，且该主机处于一个具有 24 位（类 C）网络掩码的网络中。子网化 IP 地址是指网络位数不是 8 的整数倍的地址，例如 192.168.1.100/26。

### 超网（Supernetting）

正如您所预料的，超网与子网划分相关。子网划分允许您将一个网络拆分为几个较小的网络，而超网则允许您将连续编号的网络合并为一个更大的网络。例如，假设您被分配了 256 个 C 类网络地址，范围涵盖从 192.192.0.0 到 192.192.255.255。通过指定 255.255.0.0 的网络掩码，您可以将这些 C 类网络地址视为单个 B 类地址：16 位用于网络地址，16 位用于主机地址。

## 主机名和域名

大多数人发现记忆 IP 地址很麻烦。因此，主机通常会被分配主机名以及 IP 地址。将 Web 浏览器指向 www.redhat.com 比指向 206.132.41.202 要容易得多。

就像组织向互联网管理机构申请网络地址而不是单个主机地址一样，它们申请的是域名而不是单个主机名。域名由至少两部分组成：顶级域（top-level domain）和子域（subdomain）。各部分由点 (.) 分隔。

有时会使用额外的子域，每个子域之间用点分隔。已经建立了几个顶级域，包括以下内容：

- com：由商业公司运营的网络
- edu：由学校运营的网络
- gov：由美国政府机构运营的网络
- mil：由美国军方运营的网络
- net：由互联网服务提供商 (ISP) 运营的网络

此外，世界上大多数国家都有指定的顶级域。例如，英国的域名是 uk。

组织向互联网管理机构注册其域名（或多个域名）。然后，它分配包含该域名的主机名。作为一个简单的例子，主机名 `www.redhat.com` 由以下部分组成：

- 一个主机名，`www`
- 一个域名，`redhat.com`，它由以下部分组成：
    - 一个子域，`redhat`
    - 一个顶级域，`com`

网络内部的主机通常通过主机名相互引用，而无需引用它们隐含的共同域名。主机名和域名的组合被称为 *完全限定域名 (FQDN)*。

## TCP/IP 模型

上一节描述了 TCP/IP 主机是如何命名和编号的。本节描述 TCP/IP 网络如何运行以及它们通常提供的服务类型。

通常通过引用开放系统互连 (OSI) 参考模型来解释协议族，该模型将网络功能分为七层。然而，TCP/IP 协议族并不严格符合 OSI 模型。将 TCP/IP 视为由四个协议层组成更为方便，如图 4.1 所示。接下来的小节将详细解释这些层。

**图 4.1 TCP/IP 协议层**

![](img/4eef9c6f2f52b608eba628cf4e2793ce_110_0.png)

### 网络访问协议

最底层的协议是网络访问协议，它包括访问物理网络介质并将数据传输到本地网络主机所需的所有功能。通常，TCP/IP 与以太网（Ethernet）结合使用，以太网是一种提供这些功能的协议。

网络访问协议倾向于在硬件中实现。例如，典型的网络适配器卡能够识别以太网协议。因此，网络访问层很少是 Linux 系统管理员关注的主要问题。

### 互联网协议

互联网协议层将 IP 地址确立为 TCP/IP 主机寻址的标准手段。该层还处理发往本地网络以外主机的消息路由。

主机可以通过将数据定向到目标主机的 IP 地址，将数据发送到本地网络上的另一台主机。或者，网络主机可以发送 *广播消息*，该消息可到达本地网络上的每台主机。

连接到多个网络的主机可以配置为在网络之间传递数据。这种主机被称为 *路由器*。

每台能够访问本地网络以外主机的主机必须配置 *默认路由*，该路由指定一个特殊的主机路由器——称为 *网关*——用于在本地网络内外传递信息。主机还可以配置额外的路由以访问特定的网络或主机。

路由信息可以通过 *静态路由* 指定，静态路由硬编码在配置文件中。或者，主机可以使用 *动态路由*。能够进行动态路由的路由器会发送广播消息，宣传其将数据路由到特定网络的能力。配置为动态路由的主机监听此类消息，并在路由器状态发生变化时自动更新其配置。

互联网协议层包含两个主要协议：IP (Internet Protocol) 和 ICMP (Internet Control Message Protocol)。

#### IP

*IP 协议负责数据的路由和交付*。它是一个 *无连接协议*，这意味着在主机之间交换数据之前不需要进行握手。

IP 协议被称为 *不可靠协议*。这并不意味着它不能被信任来交付数据，而仅仅是指 IP 缺乏错误检测和恢复机制。这些功能在 TCP/IP 中并非缺失，而是由传输层协议提供的。

#### ICMP

ICMP 协议在主机之间传递控制消息。这些控制消息执行以下功能：

- 调节数据流，以免接收主机过载。
- 将不可达的目标告知发送主机。
- 将新路由和关闭的路由告知主机。
- 使主机能够检查远程主机的状态。

### 传输协议

传输层协议用于在主机之间传递应用程序数据，使用的是网络访问层和互联网层协议提供的服务。两种主要的传输协议是用户数据报协议 (UDP) 和传输控制协议 (TCP)。

#### UDP

UDP 使应用程序能够将有限长度的消息从一台主机发送到另一台主机。与 IP 类似，UDP 是一种无连接的、不可靠的协议。它的主要优点是开销低，因此适用于简短、不频繁的主机间交互，以及偶尔丢失一条消息并不比快速发送数据更重要的交互。当需要错误检测和恢复时，则使用 TCP。

#### TCP

TCP 使应用程序能够将数据流从一台主机发送到另一台主机。与 IP 和 UDP 不同，TCP 是一种 *面向连接的协议*。在主机通过 TCP 交换数据之前，需要启动一个会话。会话通过对组成数据流的离散消息进行序列检查等手段提供错误控制。创建会话以及执行错误检查和恢复会产生一定的开销；因此，只有在这些考虑因素很重要时，才会优先选择 TCP 而非 UDP。

### 应用协议

TCP/IP 提供了许多应用协议，称为 *服务*。此外，程序员可以很容易地基于 UDP 或 TCP 协议创建新服务。一个服务与一个 *端口* 相关联，端口是一个 16 位的数字，用于标识该服务。UDP 端口和 TCP 端口是不同的；基于 UDP 的服务可以与基于 TCP 的服务拥有相同的端口而不会产生混淆。

在 UNIX 下访问 0–1023 端口需要 *root* 权限。因此，这些端口被称为 *特权端口*。其余端口被称为 *非特权端口*。

某些端口根据长期惯例与特定服务相关联。例如，端口 7 与 *echo 服务*（由 `ping` 命令使用）相关联。此类端口被称为 *周知端口 (well-known ports)*。在 UNIX 下，`/etc/services` 文件标识了周知端口。表 4.1 总结了重要的 TCP/IP 服务及其端口号。您可以在 Red Hat Linux 分发的 `/etc/services` 文件中找到更多列出的服务。



并非所有这些服务，以及表 4.1 中列出的服务，都可能在某个给定的主机上可用。

### 表 4.1 重要的 TCP/IP 服务及其端口号

| 端口 | 底层协议 | 服务 | 描述 |
| :--- | :--- | :--- | :--- |
| 7 | UDP/TCP | echo | 确定远程主机是否可访问。 |
| 9 | UDP/TCP | discard | 提供一个丢弃其输入内容的服务。 |
| 11 | TCP | systat | 显示当前活跃用户。 |
| 13 | UDP/TCP | daytime | 以 ASCII 字符串形式提供本地时间。 |
| 15 | TCP | netstat | 提供网络性能统计数据。 |
| 17 | TCP | qotd | 提供“每日一句”名言。 |
| 18 | UDP/TCP | msp | 向用户发送简单的消息。 |
| 19 | UDP/TCP | chargen | 发送字符流。 |
| 20 | TCP | ftp-data | 由文件传输协议 (FTP) 服务用于发送数据。 |
| 21 | TCP | ftp | 由 FTP 服务用于发送控制信息。 |
| 22 | UDP/TCP | ssh | 提供对安全外壳 (secure shell) 服务的访问。 |
| 23 | TCP | telnet | 提供对 telnet 远程 shell 服务的访问。 |
| 25 | TCP | smtp | 提供对简单邮件传输协议 (SMTP) 的访问。 |
| 37 | UDP/TCP | time | 以二进制值提供时间。 |
| 43 | TCP | whois | 提供名称和地址信息。 |
| 53 | UDP/TCP | domain | 提供对域名服务 (DNS) 的访问。 |
| 67 | UDP/TCP | bootps | 由引导协议 (bootp) 服务器使用。 |
| 68 | UDP/TCP | bootpc | 由引导协议 (bootp) 客户端使用。 |
| 69 | UDP | tftp | 提供对简单文件传输协议 (TFTP) 服务的访问。 |
| 70 | UDP/TCP | gopher | 提供对 Gopher 信息检索服务的访问。 |
| 79 | TCP | finger | 提供对 finger 服务的访问，该服务用于描述用户。 |
| 80 | UDP/TCP | www | 提供对 HTTP (Web) 服务的访问。 |
| 88 | UDP/TCP | kerberos | 提供对 Kerberos 身份验证服务的访问。 |
| 109 | UDP/TCP | pop-2 | 提供对邮局服务（版本 2）的访问。 |
| 110 | UDP/TCP | pop-3 | 提供对邮局服务（版本 3）的访问。 |
| 111 | UDP/TCP | sunrpc | 提供对远程过程调用 (RPC) 服务的访问。 |
| 113 | TCP | auth | 提供对 BSD identd 身份验证服务的访问。 |
| 119 | TCP | nntp | 提供对网络新闻传输协议 (NNTP) 服务的访问。 |
| 123 | UDP/TCP | ntp | 提供对网络时间协议 (NTP) 服务的访问。 |
| 137 | UDP/TCP | netbios-ns | 提供对 NetBIOS 名称服务的访问。 |
| 138 | UDP/TCP | netbios-dgm | 提供对 NetBIOS 数据报服务的访问。 |
| 139 | UDP/TCP | netbios-ssn | 提供对 NetBIOS 会话服务的访问。 |
| 143 | UDP/TCP | imap2 | 提供对交互式邮件访问服务（版本 2）的访问。 |
| 161 | UDP | snmp | 提供对简单网络管理协议 (SNMP) 服务的访问。 |
| 162 | UDP | snmp-trap | 提供对 SNMP 服务的访问。 |
| 177 | UDP/TCP | xdmcp | 提供对 X 显示管理器控制协议 (XDMCP) 服务的访问。 |
| 179 | UDP/TCP | bgp | 提供对边界网关协议 (BGP) 服务的访问。 |
| 194 | UDP/TCP | irc | 提供对互联网中继聊天 (IRC) 服务的访问。 |
| 213 | UDP/TCP | ipx | 提供对 IPX (Novell 网络协议族) 服务的访问。 |
| 220 | UDP/TCP | imap3 | 提供对交互式邮件访问服务（版本 3）的访问。 |
| 443 | UDP/TCP | https | 提供对安全 HTTP (Web) 服务的访问。 |
| 512 | UDP | biff | 提供一个通知用户邮件到达的服务。 |
| 512 | TCP | exec | 提供对远程执行 (REXEC) 服务的访问。 |
| 513 | UDP | who | 提供一个维护用户数据库的服务。 |
| 513 | TCP | login | 提供对远程登录 (rlogin) 服务的访问。 |
| 514 | UDP | syslog | 提供对系统日志 (SYSLOG) 服务的访问。 |
| 514 | TCP | shell | 提供对远程 shell (RSH) 服务的访问。 |
| 515 | TCP | printer | 提供对远程打印 (LPR/LPD) 服务的访问。 |
| 517 | UDP | talk | 提供对聊天服务的访问。 |
| 518 | UDP | ntalk | 提供对聊天服务的访问。 |
| 749 | TCP | kerberos-adm | 提供对 Kerberos 身份验证服务器管理服务的访问。 |

## 守护进程 (Daemons)

在 UNIX 下，TCP/IP 服务可以通过以下三种方式中的任何一种来支持：

- 由 UNIX 内核支持
- 由一个持续运行的进程支持
- 由 `inetd` 进程在客户端请求服务时启动的进程支持

只有少数服务由内核直接支持。大多数服务由持续运行的进程支持，或者在需要时由 `inetd` 进程启动。这类进程被称为 *守护进程 (daemons)*，因为它们在运行期间不与控制台终端关联。有时守护进程也被称为 *后台进程*。表 4.2 描述了通常持续运行的重要 Linux 守护进程，表 4.3 描述了通常仅在由 `inetd`（有时被称为 *Internet 超级服务器*）启动时才运行的重要 Linux 守护进程。

### 表 4.2 重要的 Linux 守护进程

| 守护进程 | 描述 |
| :--- | :--- |
| amd | 自动挂载和卸载 NFS 文件系统。 |
| apmd | 管理操作系统的高级电源管理 (APM) 功能与 BIOS 之间的接口。 |
| arpwatch | 跟踪 IP 地址和以太网地址的配对。 |
| atd | 将作业排队以进行计划执行。 |
| autofs | 自动挂载和卸载文件系统。 |
| bootparamd | 为无盘客户端提供启动信息。 |
| crond | 执行计划命令。 |
| dhcpd | 为主机提供动态 IP 地址和网络信息。 |
| diald | 通过电话线自动建立和断开远程 IP 连接。 |
| gated | 管理网络路由。 |
| gpm | 在控制台上启用鼠标剪切和粘贴操作。 |
| httpd | Web 服务器。 |
| innd | 处理传入的 USENET 新闻馈送。 |
| linuxconf | Red Hat Linux 系统管理工具。 |
| lpd | 缓存并提交本地和远程打印作业。 |
| mars-nwe | 与 Novell NetWare 兼容的文件和打印服务器。 |
| mcserv | 提供对 Midnight Commander 文件管理器的远程访问。 |
| named | 提供域名服务。 |
| nmbd | NetBIOS 名称服务器。 |
| nfs | 提供对文件的远程访问。 |
| nscd | 用于身份验证设施的缓存服务。 |
| pcmcia | 管理 PC 卡设备。 |
| portmap | 管理远程过程调用 (RPC) 连接。 |
| postgresql | 提供对 Postgres 数据库的访问。 |
| routed | 管理小型简单网络的网络路由。 |
| rstatd | 提供系统性能度量。 |
| usersd | 在其他网络主机上定位用户。 |
| rwalld | 在活跃的终端上显示消息。 |
| rhod | 提供活跃用户列表。 |
| sendmail | 邮件传输代理。 |
| smbd | 与 SMB 兼容的文件、打印和登录服务器。 |
| snmpd | 提供网络管理服务。 |
| squid | 互联网对象 (HTTP, FTP 和 Gopher) 缓存。 |
| sshd | 安全外壳服务。 |
| syslog | 提供对系统日志的访问。 |
| xfs | 为 X 提供字体。 |
| xntpd | 提供时间同步服务。 |
| ypbind | 将 NIS 客户端绑定到其域。 |
| yppasswd | 允许 NIS 用户更改其密码。 |
| ypserv | 提供一个全网范围的主机、用户和其他信息的数据库。 |

### 表 4.3 使用 inetd 的重要 Linux 守护进程

| 守护进程 | 描述 |
| :--- | :--- |
| auth | 识别用户 (identd)。 |
| bootps | 提供 IP 地址和其他启动信息。 |
| comsat | 通知用户有新邮件到达。 |
| exec | 执行远程提交的命令。 |
| finger | 提供对 finger 命令的远程访问。 |
| ftp | 在远程主机之间传输文件。 |
| imap | 提供对邮件的交互式访问。 |
| linuxconf | Linux 系统管理工具。 |
| login | 提供远程登录。 |
| netbios-ns | 提供 NetBIOS 名称服务。 |
| netbios-ssn | 提供 NetBIOS 会话服务。 |
| netstat | 提供网络性能数据。 |
| ntalk | 提供远程用户通信。 |
| pop-2 | 提供对邮件的远程访问。 |
| pop-3 | 提供对邮件的远程访问。 |



### 表 4.3 使用 inetd 的重要 Linux 守护进程（续）

| 守护进程 | 描述 |
| :--- | :--- |
| shell | 提供远程 shell 服务。 |
| swat | 为 Samba 软件包提供基于 Web 的管理。 |
| systat | 提供进程性能数据。 |
| talk | 提供远程用户通信。 |
| telnet | 提供远程登录。 |
| tftp | 以极低的认证和开销在远程主机之间传输文件。 |

您可以通过执行以下命令来确定当前正在运行哪些守护进程：

```
ps x
```

该命令的输出包括每个守护进程相关的进程 ID (PID) 和命令：

```
PID TTY STAT TIME COMMAND
  1 ? S 0:03 init
391 ? S 0:17 syslog -m 0
402 ? S 0:00 klogd
430 ? S 0:00 crond
444 ? S 0:00 inetd
458 ? S 2:37 arpwatch -i eth1
472 ? S 0:18 named
478 ? S 0:28 /usr/sbin/sshd -p 23
491 ? SL 0:14 xntpd -A
506 ? S 0:00 lpd -l
521 ? S 0:06 /usr/sbin/dhcpd
556 ? S 0:00 sendmail: accepting connections on port 25
571 ttyS0 S 0:00 gpm -t MouseMan
585 ? S 0:00 httpd
602 ? S 0:00 logger
 685 tty3    SW   0:00 [mingetty]
 686 tty4    SW   0:00 [mingetty]
 688 tty6    S    0:00 /sbin/mingetty tty6
 690 ?        S    0:04 update (bdflush)
 723 tty2    S    0:00 /sbin/mingetty tty2
 726 tty1    S    0:00 /sbin/mingetty tty1
 1110 ?       S    0:00 [smbd]
 1121 ?       S    0:09 nmbd -D
 1124 ?       S    0:00 [nmbd]
 2803 ?       SW   0:00 [rpcbind]
 2804 ?       SW   0:00 [lockd]
 5873 tty5    S    0:00 /sbin/mingetty tty5
 15739 pts/1  R    0:00 ps x
```

要确定哪些守护进程当前正在运行，或者哪些守护进程将由 inetd 启动，请执行以下命令：

```bash
netstat -ap -- inet | grep LISTEN
```

该命令会报告相关服务的端口号或名称，以及当前在该端口上监听的进程号和进程名称。如果监听进程是 inetd，这表明该服务将在需要时由 inetd 启动，如下面 **netstat** 命令的输出所示：

```
tcp 0 0 *:1047               *:*    LISTEN  -
tcp 0 0 *:netbios-ssn        *:*    LISTEN  1110/
tcp 0 0 *:www                *:*    LISTEN  585/httpd
tcp 0 0 *:smtp               *:*    LISTEN  556/
=>sendmail: accep
tcp 0 0 *:printer            *:*    LISTEN  506/lpd
tcp 0 0 *:telnet            *:*    LISTEN  478/sshd
tcp 0 0 router:domain        *:*    LISTEN  472/named
tcp 0 0 www:domain           *:*    LISTEN  472/named
tcp 0 0 localhost:domain     *:*    LISTEN  472/named
tcp 0 0 *:linuxconf          *:*    LISTEN  444/inetd
tcp 0 0 *:imap2              *:*    LISTEN  444/inetd
tcp 0 0 *:pop-3              *:*    LISTEN  444/inetd
tcp 0 0 *:ftp                *:*    LISTEN  444/inetd
tcp 0 0 *:sunrpc             *:*    LISTEN  344/portmap
```

现在完成练习 4.1，以获得监控运行中守护进程的经验。

## 练习 4.1
### 列出守护进程

要查看系统中运行哪些守护进程，请执行以下步骤：

- 1. 在 Linux 系统上运行 `ps` 命令，并识别正在运行的守护进程。
- 2. 在 Linux 系统上运行 `netstat` 命令，并识别正在运行的守护进程以及将由 inetd 启动的守护进程。

大多数服务可以配置为持续运行或仅在由 inetd 启动时运行。然而，出于性能考虑，某些服务应当持续运行。例如，安全外壳服务 (SSH) 在启动时必须计算加密密钥。在 inetd 的控制下运行 SSH 意味着每次客户端连接时都要运行这个耗时的计算。通常，让 SSH 持续运行更好，这样客户端可以获得快速的服务。

### 控制守护进程

Red Hat Linux 为每个安装的守护进程提供了一个脚本。该脚本可以执行以下操作：

- 启动守护进程
- 停止守护进程
- 重启守护进程
- 显示与该守护进程相关的状态信息

执行这些功能的脚本存储在 `/etc/rc.d/init.d` 目录中。该目录中的并非所有脚本都与持续运行的守护进程相关。例如，由 inetd 启动的一些守护进程在该目录中也可能有脚本。同样，该目录中的某些脚本涉及的是系统启动任务而非守护进程。您通常可以通过名称来区分控制守护进程的脚本，其名称与表 4.2 和 4.3 中列出的守护进程名称相似。您还可以检查脚本中的注释以了解其用途。

### 启动守护进程

要启动守护进程，请执行以下步骤：

- 1. 进入 `/etc/rc.d/init.d` 目录。
- 2. 执行命令 `. /xxx start`，其中 `xxx` 是与该守护进程相关联的文件名。
- 3. 检查系统日志 `/var/log/messages` 以查看是否有错误信息。

### 停止守护进程

要停止守护进程，请执行以下步骤：

- 1. 进入 `/etc/rc.d/init.d` 目录。
- 2. 执行命令 `. /xxx stop`，其中 `xxx` 是与该守护进程相关联的文件名。
- 3. 检查系统日志 `/var/log/messages` 以查看是否有错误信息。

### 重启守护进程

要重启守护进程，请执行以下步骤：

- 1. 进入 `/etc/rc.d/init.d` 目录。
- 2. 执行命令 `. /xxx restart`，其中 `xxx` 是与该守护进程相关联的文件名。
- 3. 检查系统日志 `/var/log/messages` 以查看是否有错误信息。

某些守护进程（如 `nfsd`）有时可能无法正常重启。在这种情况下，您可能更倾向于先停止然后再启动该守护进程。

### 显示守护进程状态

要显示守护进程的状态信息，请执行以下步骤：

- 1. 进入 `/etc/rc.d/init.d` 目录。
- 2. 执行命令 `. /xxx status`，其中 `xxx` 是与该守护进程相关联的文件名。

现在，完成练习 4.2 以探索运行中守护进程的状态。

## 练习 4.2
### 控制守护进程

为了获得控制守护进程的经验，请执行以下步骤：

- 1. 使用前几节中的指令来显示 Linux 系统上运行的守护进程状态。
- 2. 如果 Linux 系统提供了非关键服务，请停止、启动并重启一个无人使用的服务。

> 在 Red Hat Linux 6.2 中，不再需要进入 /etc/rc.d/init.d 目录来执行控制服务的命令。相反，请执行如下格式的命令：`service daemon operation`。参数 `daemon` 标识与该守护进程关联的 /etc/rc.d/init.d 文件，参数 `operation` 指定您要执行的操作，例如 start 或 stop。

## 总结

在本章中，您学习了 TCP/IP 网络和服务的 fundamentals。涵盖的最重要主题包括：

- **IP 地址**：TCP/IP 主机通过 IP 地址来识别，通常使用点分十进制表示法。IP 地址由网络地址和主机地址组成。
- **网络类**：互联网管理机构根据请求的网络类分配 IP 地址块，网络类反映了网络中的主机数量。
- **子网划分和超网划分**：可以使用掩码来指定一个长度不是 8 位整数倍的网络地址。
- **主机名**：TCP/IP 主机通常通过其主机名来引用，主机名比 IP 数字更容易记忆。包含域名的主机名被称为全限定域名 (FQDN)。

**TCP/IP 协议族**：TCP/IP 可以被认为由四个协议层组成：网络访问层、Internet 层、传输层和应用层。最重要的 Internet 协议是 IP 和 ICMP。最重要的传输协议是 UDP 和 TCP。

**TCP/IP 服务**：服务与端口相关联，端口可以是特权端口或非特权端口。某些端口是众所周知的，并列在 `/etc/services` 文件中。服务可以由内核提供，也可以由守护进程提供，守护进程可以持续运行，或者由 `inetd` 服务按需启动。您可以使用位于 `/etc/rc.d/init.d` 的脚本来控制 Red Hat Linux 的 TCP/IP 服务。

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- 背景进程 (background process)
- 广播消息 (broadcast message)
- 面向连接的协议 (connection-oriented protocol)
- 无连接协议 (connectionless protocol)
- 守护进程 (daemons)
- 默认路由 (default route)
- 域名 (domain name)
- 点分十进制表示法 (dotted quad notation)
- 动态 IP 地址 (dynamic IP address)
- 动态路由 (dynamic routing)
- 全限定域名 (fully qualified domain name, FQDN)
- 网关 (gateway)
- 主机地址 (host address)
- 主机名 (host name)
- 主机 (hosts)
- Internet 超级服务器 (Internet super server)



- IP 地址
- 回环地址
- 子网掩码
- 网络地址
- 网络类
- 非特权端口
- 八位组
- 端口
- 特权端口
- 路由器
- 服务
- 静态 IP 地址
- 静态路由
- 子网划分
- 超网划分
- TCP
- 顶级域名
- UDP
- 不可靠协议
- 知名端口

## 其他信息来源

如果您想进一步了解本章介绍的主题，可以参考以下资料：

- *TCP/IP 24seven*, Gary Govanus (Sybex, 1999)
- *Network+ Study Guide*, David Groth, with Ben Bergersen and Tim Catura-Houser (Sybex, 1999)

## 复习题

1. 为什么 IP 被认为是一种不可靠协议？
    A. 因为高层协议执行错误控制。
    B. 因为它不包含错误检查。
    C. 因为它不包含错误恢复。
    D. 因为它使用不可靠的硬件协议。

2. 以下关于动态 IP 地址的描述，哪些是正确的？
    A. 它总是在启动时分配。
    B. 它由互联网管理机构分配给主机。
    C. 它今天可能属于一台主机，明天可能属于另一台。
    D. 它克服了路由障碍。

3. 主机名和域名相结合被称为什么？
    A. 一个完整主机名 (A full host name)
    B. 一个全限定域名 (A fully qualified domain name)
    C. 一个全限定主机名 (A fully qualified host name)
    D. 一个主机名 (A host name)

4. 以下哪个网络类在单个网络中提供最多的主机数量？
    A. A 类
    B. B 类
    C. C 类
    D. D 类

5. 哪项陈述适用于 23 端口？
    A. 它是一个动态端口。
    B. 它是一个非特权端口。
    C. 它是一个特权端口。
    D. 它是一个知名端口。

6. 以下哪些可以提供 TCP/IP 服务？
    A. 一个持续运行的守护进程
    B. 一个在需要时启动的守护进程
    C. 内核
    D. 一个伪终端 (pseudo-tty)

## 复习题答案

1. A, B, C. IP 没有错误检查或恢复功能；TCP 增加了这些功能。
2. C. 动态 IP 地址通常在建立网络连接时分配。它来自系统管理员指定的 IP 地址池。
3. B, D. 带有明确域名的主机名被称为全限定域名或主机名。
4. A. A 类网络具有 8 位网络地址，支持超过 1600 万个网络主机。
5. C, D. 23 端口是一个与 `telnet` 服务相关的特权端口。
6. A, B, C. 服务可以由内核、持续运行的守护进程或由 `inetd` 在需要时启动的守护进程提供。

# 第 5 章：Linux 历史

本章涵盖的 RHCE 准备主题：

- 了解 Linux 的历史。
- 了解 GNU 项目的历史。
- 理解开源软件的特点。
- 了解 Red Hat Linux 的历史。
- 理解 Red Hat Linux 的主要特点。
- 了解如何定位和使用重要的 Linux 资源。

本章描述了 Unix 和 Linux 的历史、GNU 项目、开源软件以及 Red Hat Linux。它解释了开源软件的本质和特点，并介绍了重要的 Linux 资源及其访问方式。有些人觉得历史很枯燥。如果你是其中之一，欢迎跳过本章。但请记住，RHCE 考试可能会包含一些关于 Linux 历史的问题。如果你计划参加 RHCE 考试，你应该熟悉 Linux 的历史，特别是 Red Hat Linux 的历史。

## Unix

虽然 Linux 在操作系统领域出现较晚，但作为 Unix 的子嗣，它拥有显赫的血统，而 Unix 可能是最具影响力的操作系统。要充分理解 Linux，你需要了解其父辈的一些历史。在 20 世纪 60 年代，AT&T 的贝尔实验室与麻省理工学院 (MIT) 和通用电气合作开发了一个名为 Multics 的多用户计算机操作系统。两名贝尔实验室的研究员——丹尼斯·里奇 (Dennis Ritchie) 和肯·汤普森 (Ken Thompson) 参与了该项目，直到贝尔实验室退出。

在 Multics 项目期间，里奇和汤普森通过玩 Space Travel（一款在 Multics 下运行的早期多用户计算机游戏）来娱乐自己。在贝尔实验室退出项目后，他们无法再通过在星系中穿梭来缓解工作压力。他们决定通过将 Space Travel 重新移植到他们可以使用的一台不常用的 DEC PDP-7 计算机上来解决这个问题。

这个新项目要求他们为 PDP-7 实现一个新的操作系统，他们将其命名为 Unics，这是对 Multics 的一个谐音双关。由于拼写不够严谨，他们最终不知怎么地将操作系统的名称改成了 Unix。Unix 的独特之处之一是里奇和汤普森使用里奇开发的新编程语言 C 来实现它。用 C 语言实现 Unix 使得将其移植到其他计算机比之前的操作系统（通常用汇编语言编写）要容易得多。

当他们的工作传到其他人耳中时，里奇和汤普森开始收到索要 Unix 副本的请求。请求者主要是对操作系统研究感兴趣还是对 Space Travel 感兴趣，这仍然是个开放性问题。无论如何，Unix 被广泛分发，尤其是到各大学。全球的计算机科学家和学生研究 Unix，寻找改进方法，并将代码发回给里奇和汤普森，由他们整合进 Unix。结果，Unix 迅速成长和完善，成为了最重要的计算机操作系统之一。

## GNU 项目和自由软件基金会

在 20 世纪 80 年代初，AT&T 开始意识到 Unix 的商业价值。因此，他们主张对其拥有所有权，并开始收取高额的许可费。许多向 Unix 贡献代码的人认为 AT&T 不公平地挪用了他们的贡献。MIT 研究员理查德·斯托曼 (Richard Stallman) 不满足于仅仅抱怨，他发起了 GNU (GNU is not Unix) 项目，旨在创建一个可以自由分发的类 Unix 操作系统。为了支持 GNU，斯托曼和其他人在 1984 年创建了自由软件基金会 (FSF)。

FSF 推广的是“自由 (free)”的软件，但这种软件并不一定是指“免费 (cost free)”的软件。FSF 所指的 free 是在“自由”的意义上的。自由软件是指你可以对其进行以下操作的软件：

- 用于任何目的
- 研究以学习其工作原理，并进行改编以满足你的需求
- 复制和重新分发
- 作为改进软件系统的一部分进行分发

## GNU 通用公共许可证 (GPL)

GNU 项目最重要的贡献或许就是名为 GNU 通用公共许可证，或简称为 *GNU 公共许可证* (GPL) 的许可证。GPL 是一种版权形式，被称为 *copyleft*（左版），旨在保护——而非排除——使用、研究、复制和分发软件的权利。本质上，GPL 规定，只要用户不试图损害他人使用软件的权利，就有权使用该软件程序。当前版本 GPL 的全文在随附光盘中。

## Linux 内核

在 Unix 的早期，大学将 Unix 作为向计算机科学学生教授操作系统的工具。当 AT&T 主张其对 Unix 的所有权时，大学需要一个替代品。安德鲁·塔嫩鲍姆 (Andrew Tannenbaum) 创建了一个名为 *MINIX* 的类 Unix 操作系统，它作为教学工具而流行。然而，与 UNIX 不同，MINIX 主要是作为教学工具设计的，性能相对较差。

1990 年，芬兰计算机科学专业的学生林纳斯·托瓦兹 (Linus Torvalds) 开始为 Intel 架构的 PC 开发内存管理器。在某个时刻，他意识到他的工作可以扩展为运行一个 *Unix 内核*。1991 年 8 月，他将正在进行的工作发布在互联网新闻组 `comp.os.minix` 上，邀请他人提出希望实现的功能：

```
From: torvalds@klaava.Helsinki.FI (Linus Benedict Torvalds)
Newsgroups: comp.os.minix
Subject: What would you like to see most in minix?
Summary: small poll for my new operating system
Message-ID: <1991Aug25.205708.9541@klaava.Helsinki.FI>
Date: 25 Aug 91 20:57:08 GMT
Organization: University of Helsinki
```



各位正在使用 minix 的朋友们，你们好 -
我正在为 386(486) AT 兼容机开发一个（免费的）操作系统（只是出于爱好，不会像 gnu 那样规模宏大且专业）。这个项目从四月份就开始酝酿，现在已经开始准备就绪了。我想听听大家对 minix 中喜欢或不喜欢的功能的反馈，因为我的操作系统在某些方面与它有些相似（出于实际原因，采用了相同的文件系统物理布局等）。

目前我已经移植了 bash(1.08) 和 gcc(1.40)，且运行情况良好。这意味着在几个月内我将获得一些实用的成果，我想知道大多数人希望拥有哪些功能。欢迎任何建议，但我不能保证一定会实现它们 :-)

Linus (torvalds@kruuna.helsinki.fi)

另外。是的 - 它不包含任何 minix 代码，并且拥有一个多线程的文件系统。它不是可移植的（使用了 386 任务切换等），而且可能永远不会支持除 AT 硬盘以外的任何设备，因为这是我仅有的设备 :-

Torvalds 将他的操作系统内核命名为 Linux，意为“Linus 的 Minix”。Unix 程序员们热心地提供帮助以开发 Linux。由于 Stallman 的 GNU 项目已经完成了类 Unix 操作系统所需的所有组件（除了内核），Linux 和 GNU 成了天然的结合。1994 年，在 Torvalds 发布帖子大约三年后，Linux 1.0 根据 GPL 条款发布。当时，Linux 已经拥有约 100,000 名用户。

由于 GNU 对 Linux 的发展至关重要——至今依然如此——许多人喜欢将 Linux 称为 **GNU/Linux**。

Linux 内核使用奇偶系统进行编号。偶数编号的内核——例如 Linux 2.2——被称为 *稳定版内核 (stable kernel)*。稳定版内核的更改通常仅用于修复 bug 和问题。奇数编号的内核——例如 Linux 2.3——被称为 *开发版内核 (development kernel)*。开发版内核是处于开发中的作品，有时包含 bug，其中一些较为严重。大多数 Linux 用户使用稳定版内核，并保留备用计算机用于测试开发版内核。在编写本书时，Linux 2.2 是最新的稳定版内核。

当 Linux 刚问世时，搭建一个可运行的 Linux 系统是一件相当麻烦的事。然而，Linux 粉丝很快创建了 *Linux 发行版 (Linux distributions)*，即一组软件套件，使得安装、配置和使用 Linux 变得相对容易。最早的两个发行版是 Soft Landing Systems (SLS) 和 Slackware；Slackware 直到今天仍然可用。

Red Hat, Inc. 由 Bob Young 和 Marc Ewing 于 1994 年创立。不久之后，在 1995 年，Red Hat, Inc. 创建了一个名为 Red Hat Linux 的 Linux 发行版。与当时的其他发行版不同，Red Hat Linux 是一个基于软件包的发行版，这意味着组件程序包含在软件包文件中，文件中还包含了描述这些程序的信息。一个名为 Red Hat 软件包管理器 (RPM) 的实用程序被用于安装软件包。由于 RPM 维护了一个描述已安装软件包的数据库，它使得更新 Linux 系统变得简单，鉴于 Linux 软件的快速变化率，这是一项至关重要的能力。如今，几乎每个 Linux 发行版都是基于软件包的；大多数 Linux 发行版使用 RPM 作为其软件包管理器。

Red Hat Linux 是主导地位的 Linux 发行版。它连续三年获得 **Infoworld** 奖项，这是一项前所未有的成就。由 Young 和 Ewing 创立的 Red Hat, Inc. 现在是一家上市公司，资本价值达数十亿。除了 Red Hat Linux，该公司还提供电话支持、现场咨询、开发人员培训、认证计划和优先更新访问等服务。

## Linux 资源

Linux 每天都在进步，因此跟上 Linux 的步伐需要获取并使用每天更新的信息。本节列出了一些将帮助您了解 Linux 最新动态的网站和新闻组。

### Linux 信息

- Groups of Linux Users Everywhere (GLUE), `www.linuxjournal.com/glue`
- Linux Documentation Project, `metalab.unc.edu/LDP`
- Linux HOWTOs, `howto.tucows.com`
- Linux International, `www.li.org`
- Linux Knowledge Base, linuxkb.cheek.com
- Linux OnLine, www.linux.org
- Linux Start, www.linuxstart.com
- Linux.com, www.linux.com
- Red Hat, Inc., www.redhat.com

### 主要 Linux 发行商

- Caldera Systems, Inc., www.caldera.com
- Corel, www.corellinux.com
- Debian GNU-Linux, www.debian.org
- Linux Mandrake, www.mandrake.com
- Red Hat, Inc., www.redhat.com
- Slackware, www.cdrom.com
- Storm Linux, www.stormlinux.com
- SuSE, www.suse.com
- TurboLinux, www.turbolinux.com

### 其他 Linux 供应商

- ASL, Inc., www.aslab.com
- Cheap Bytes, www.cheapbytes.com
- Infomagic, www.infomagic.com
- Linux Central, www.linuxcentral.com
- Linux General Store, www.linuxgeneralstore.com
- Linux Mall, www.linuxmall.com
- Linux System Labs, www.ls1.com
- LinuxCare, www.linuxcare.com
- VA Linux Systems, www.valinux.com

### Linux 新闻

- FileWatcher, `filewatcher.org`
- Freshmeat, `www.freshmeat.net`
- Kernel Traffic, `kt.linuxcare.com`
- Linux Gazette, `www.ssc.com/lg`
- Linux Information HQ, `www.linuxhq.com`
- Linux Journal, `www.linuxjournal.com`
- Linux Kernel, `www.kernel.org`
- Linux Magazine, `www.linux-mag.com`
- Linux Radio Show, `www.linuxradio.net`
- Linux Show, `www.thelinuxshow.com`
- Linux Today, `linuxtoday.com/index.html`
- Linux Weekly News, `www.lwn.net`
- Linux World, `www.linuxworld.com`
- Linux-2000 Online, `www.linux-2000.org`
- Slashdot, `www.slashdot.org`

### Linux 新闻组

- `comp.os.linux.announce` (经过审核)
- `comp.os.linux.answers`
- `comp.os.linux.hardware`
- `comp.os.linux.misc`
- `comp.os.linux.setup`
- `comp.os.linux.x`

## 总结

在本章中，您了解了 Linux 的历史、GNU 项目和开源软件。您还了解了 Red Hat Linux 的特点以及在哪里获取更多关于 Linux 的信息。涵盖的最重要主题是：

- **Unix** Linux 基于 AT&T 的 Dennis Ritchie 和 Ken Thompson 在其 Unix 操作系统中最初实现的概念。
- **GNU 和 FSF** Richard Stallman 创立了 FSF 和 GNU 项目以确保软件自由。GNU 项目的目标是创建一个免费的类 Unix 操作系统。
- **GPL** GNU 通用公共许可证是一种版权形式，旨在保护软件自由，包括使用、修改和分发软件的权利。
- **Linux** Linux 是一个根据 GPL 条款分发的类 Unix 操作系统。Linux 包含由 Linus Torvalds 最初创建的内核，以及由 GNU 项目最初创建的实用程序和程序。
- **Red Hat Linux** Red Hat, Inc. 分发领先的 Linux 发行版 Red Hat Linux。

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- copyleft（左版）
- development kernel（开发版内核）
- FSF (Free Software Foundation)（自由软件基金会）
- GNU
- GPL (General Public License)（通用公共许可证）
- kernel（内核）
- Linux distributions（Linux 发行版）
- OSS (Open Source Software)（开源软件）
- stable kernel（稳定版内核）

## 复习题

1. 以下哪一项是 Linux 的操作系统祖先？
   A. C
   B. GNU
   C. Solaris
   D. Unix

2. 以下哪一项是 Linux 内核的主要作者？
   A. Dennis Ritchie
   B. Andrew Tannenbaum
   C. Ken Thompson
   D. Linus Torvalds

3. 以下哪一项是自由软件基金会 (FSF) 和 GNU 项目的创始人？
   A. Marc Ewing
   B. Richard Stallman
   C. Linus Torvalds
   D. Bob Young

4. 以下哪个版本号表示一个稳定版 Linux 内核？
   A. 1.1
   B. 1.2
   C. 2.1
   D. 2.2

5. 以下哪个特点使 Red Hat Linux 优于其他 Linux 发行版？
   A. 成本
   B. 效率
   C. 可维护性
   D. 可扩展性

6. Linux 最初是为哪种类型的计算机实现的？
   A. Intel 286
   B. Intel 386/486
   C. Intel Pentium
   D. Motorola 68000



## 复习题答案

- 1. D. C 和 GNU 不是操作系统，尽管 GNU 的目标是有一天成为一个操作系统。Solaris 不是 Linux 的祖先。
- 2. D. 林纳斯·托瓦兹（Linus Torvalds），一名芬兰计算机科学专业的学生，编写了最初的 Linux 内核。
- 3. B. 理查德·斯托曼（Richard Stallman），一名前 MIT 研究员，创立了 FSF 和 GNU 项目。
- 4. B, D. 版本号的小数部分对于稳定版内核为偶数，对于开发版内核为奇数。
- 5. C. 软件包使得 Red Hat Linux 比其他 Linux 发行版更易于维护，因为更新系统更加简单。
- 6. B. 林纳斯·托瓦兹为 Intel 386/486 实现了 Linux。

### 安装

# 第二部分

# 第 6 章：安装规划

本章涵盖的 RHCE 准备主题：

- 理解确定系统需求的必要性。
- 了解安装过程中可能需要哪些信息。
- 了解如何选择安装用户界面。
- 了解如何选择安装类别和类型。
- 了解如何设计分区结构。
- 了解如何使用 `fips` 来拆分 MS-DOS 分区。
- 了解如何选择和准备安装介质。
- 了解如何选择安装介质。
- 了解如何选择组件和软件包。

规划是实现有效且高效执行的重要组成部分，在系统管理中与在其他努力中一样重要。本章描述了在安装 Red Hat Linux 之前您应该执行的任务和应该做出的决定。如果您遵循本章给出的指令，您可以期待 Red Hat Linux 的安装过程顺利进行，仅偶尔出现异常。

## 确定需求

安装规划的第一步是确定系统必须满足的需求。例如，一名将系统用作图形处理工作站的员工，其需求与一名计划将系统主要用作 FTP 服务器的系统管理员截然不同。一旦您知道系统必须完成什么，您就可以决定需要什么样的硬件以及如何安装和配置 Red Hat Linux。

## 收集信息

如果您收集了目标系统硬件的相关信息，安装过程将会更加顺利。如果您有选择硬件的灵活性，请优先选择列在 Red Hat 硬件兼容列表 (HCL) 中的硬件，而非其他硬件。要警惕具有私有接口的设备（如 CD-ROM 驱动器）。同时也要警惕 WinModems 和 WinPrinters。

在开始安装之前，请准备好以下信息：

- CPU：类型和速度。
- 主板：总线类型（ISA, EISA, VESA, PCI, MCA 等）。
- 驱动器控制器：接口类型和使用的芯片组。
- 驱动器：每个驱动器的品牌、型号及其在控制器上的驱动器号或 SCSI ID。
- 系统 RAM：容量。
- 网络适配器：品牌和型号。对于非 PCI 网卡，需了解所使用的 IRQ、DMA 和 I/O 端口。
- 调制解调器：内置调制解调器所使用的 IRQ、DMA 和 I/O 端口，或外置调制解调器所连接的串口号。
- 声卡：品牌和型号，所使用的 IRQ、DMA 和 I/O 端口。
- 串口和并口：所使用的 IRQ 和 I/O 端口。
- 鼠标：类型（串口, PS2 或总线）和按钮数量。对于串口鼠标，需了解其连接的串口号。
- 显卡：品牌、型号、芯片组、RAM 容量以及支持的色彩深度。
- 显示器：品牌、型号、水平同步范围和垂直同步范围。

对于系统中安装的任何其他硬件设备，您也应拥有类似的信息。

如果您的系统将连接到网络，您应该准备好以下信息：

- IP 地址分配方式：静态, DHCP, BOOTP。

对于静态定义的主机，您应该准备好以下信息：

- IP 地址
- 子网掩码 (Netmask)
- 网关 (Gateways)
- 全限定域名 (FQDN)

在某些情况下，还需要额外的信息。但通常情况下，这些信息足以让您完成安装过程。安装过程完成后，您可以根据需要配置特殊选项。

除了目标系统的硬件信息外，您还应准备好 *Red Hat Linux 安装指南* 和其他 Linux 文档，尤其是 HOWTOs。如有必要，您可以使用另一个 Linux 系统或 Microsoft Windows 系统来阅读存储在文档 CD-ROM 上的文档，或者访问提供相关信息的网站和新闻组。准备好这些信息将有助于您完成安装过程；否则，您可能会发现有必要终止安装过程，获取所需信息，然后重新开始安装。

## 选择安装用户界面

Red Hat Linux 支持两种**安装类型**：安装 (Install) 和升级 (Upgrade)。当在目前没有安装 Red Hat Linux 的目标系统上安装 Linux 时，应选择“安装”。当目标系统已经安装了较早版本的 Red Hat Linux 时，请选择“升级”。升级过程会保存现有的配置文件，而不是将其覆盖。现有文件会被重命名并添加扩展名 `.rpmsave`。

Red Hat Linux 6.1 引入了基于 X 的*图形模式安装程序*。安装程序的初始屏幕允许您选择新的图形模式安装程序或*文本模式安装程序*。

初学者通常发现图形模式安装程序更容易使用。然而，出于以下原因，您可能会更倾向于文本模式安装：

- 如果目标系统具有异常的视频特性（例如旧的或不常见的显卡），图形模式安装程序可能会失败。
- 文本模式安装程序可以从某些错误中恢复（例如磁盘空间不足），而这些错误会导致图形模式安装程序失败。
- 在处理器速度慢或 RAM 容量小的计算机上，文本模式安装的运行效果比图形模式安装更好且更快。
- 图形模式安装仅支持挂载为文件系统的介质，例如现有的硬盘分区、CD-ROM 或通过 NFS 提供的介质。

## 选择安装类别

Red Hat Linux 安装程序提供了三种默认的*安装类别*或配置：

- GNOME 工作站 (GNOME Workstation)
- KDE 工作站 (KDE Workstation)
- 服务器 (Server)

工作站类别是快速启动 Red Hat Linux 系统的快捷方式。两种工作站类别都会安装最常用的软件包。此外，GNOME 工作站类别安装 GNOME 桌面管理器，而 KDE 工作站类别安装 KDE 桌面管理器。

工作站类别对于构建双启动系统特别有用，因为只要有足够的未分配磁盘空间，它们就不会干扰任何非 Linux 分区。但是，它们会删除所有现有的 Linux (ext2) 分区。它们会建立三个标准分区：

- 一个 64MB 的交换分区 (swap)
- 一个 16MB 的启动分区 (`/boot`)
- 一个使用剩余可用磁盘空间的根分区 (`/`)

两种工作站安装类别均需要约 600MB 的可用磁盘空间。

与工作站类别相比，服务器安装类别会删除所有现有分区，包括 DOS/Windows 分区。服务器安装类别需要约 1.6GB 的磁盘空间。默认情况下，服务器安装缺少以下组件（这些组件包含在其中一个工作站安装中）：

- 作者/出版 (Author/Publishing)
- DOS/Windows 连通性
- GNOME 或 KDE
- 图形处理 (Graphics manipulation)
- 多媒体支持
- X Window 系统

然而，服务器安装包含以下组件，而这些组件不包含在任何一个工作站安装中：

- 匿名 FTP 服务器
- DNS 域名服务器
- IPX/NetWare 连通性
- NFS 服务器
- 网络管理工作站
- 新闻服务器 (News server)
- Postgres (SQL) 服务器
- SMB (Samba) 服务器
- Web 服务器

服务器安装会创建更复杂的分区结构，包括：

- 一个 64MB 的交换分区 (swap)
- 一个 16MB 的启动分区 (/boot)
- 一个 256MB 的根分区 (/)
- 一个 256MB 的 /var 分区

另外两个分区将平分剩余的可用磁盘空间：

- /home
- /usr

如果工作站类别和服务器安装类别都不能满足您的需求，您可以指定“自定义 (Custom)”安装。自定义安装类别没有预定义的特性。您可以根据选择对硬盘驱动器进行分区并安装组件和软件包。

## 硬盘分区

如果您选择了任何一个工作站安装类别或服务器安装类别，安装程序将自动对您的硬盘驱动器进行分区。但是，如果您选择了自定义安装类别，则必须手动对硬盘进行分区。



分区可以提高系统数据的完整性，并能提高系统数据的安全性。如果硬盘受损，损坏通常被限制在单个分区内。恢复单个分区可能比恢复整个驱动器更简单、更快捷。此外，还可以将分区挂载为只读。通过将不需要更改的数据组织为一个分区并将其挂载为只读，可以提高数据的完整性和安全性。无法写入的分区比挂载为读写的分区更不容易损坏。而且，对于黑客来说，在只读分区上秘密修改数据比在读写分区上更困难。

在设计分区结构时，以下目录应保留在单个分区中：

- /
- /etc
- /lib
- /bin
- /sbin
- /dev

这些目录及其子目录包含系统正常运行所必需的程序和文件。它们必须始终存在，因此应成为所谓的根分区的一部分，并挂载为 /。

非自定义安装类别会创建一个 16MB 的引导分区，挂载为 /boot。通常，你的设计应包含这样一个分区。通过将引导分区放置在系统 BIOS 可寻址的 1024 柱面区域内，可以确保内核在启动时能够被访问。

通常，你应该包含一个或多个交换分区。根据经验法则，交换分区的总大小应为安装 RAM 大小的 2-3 倍。例如，一个拥有 16MB RAM 的系统应具有 32-48MB 的交换空间。定义的交换分区不能超过 8 个；总交换空间不能超过 4GB。

经常被设为独立分区挂载点的目录包括：

- /home
- /opt
- /tmp
- /usr
- /usr/local
- /var

为了将你对分区的理解应用于实际问题，请完成练习 6.1。

## 练习 6.1
### 设计分区结构

为一个拥有两个磁盘驱动器（每个容量为 5GB）的系统设计一个分区结构。为用户的家目录提供至少 1GB 的空间，为安装在 /opt 目录下的商业应用程序提供 2GB 的空间。

### 使用 fips

通常，目标系统没有足够的剩余磁盘空间来安装 Linux。如果 MS-DOS (FAT 或 FAT32) 分区包含未使用空间，你可以使用 `fips` 来拆分该分区，创建一个用于安装 Linux 的空分区。

要使用 `fips`，请遵循以下步骤：

1. 使用 `scandisk` 检查分区是否有错误。
2. 使用 `defrag` 将文件移动到分区的低端。
3. 使用“系统控制面板”小程序禁用虚拟内存。
4. 使用“添加/删除程序”控制面板小程序创建 MS-DOS 引导软盘。
5. 将以下文件从安装 CD-ROM 复制到软盘：
    - \dosutils\fips20\restorrb.exe
    - \dosutils\fips20\fips.exe
    - \dosutils\fips20\errors.txt
6. 将 `autoexec.bat` 和 `config.sys` 分别重命名为 `autoexec.fips` 和 `config.fips`，这样启动程序就不会写入硬盘。
7. 从软盘启动并运行 `fips`。
8. 让 `fips` 在软盘上创建分区表的备份。
9. 指定你要拆分的分区编号以及新分区应开始的柱面编号。
10. 输入 `y` 保存更改并退出。
11. 启动 MS-DOS 并运行 `scandisk` 以确保磁盘正常。
12. 重新启用虚拟内存，并将 `autoexec.bat` 和 `config.sys` 文件还原为原始名称。

有关更多信息，请参阅安装 CD-ROM 上的 `fips` 文档。

为了获得使用 `fips` 的经验，请完成练习 6.2。

## 练习 6.2
### 使用 fips

使用 `fips` 将一个 MS-DOS 分区拆分为两个分区。在使用 `fips` 之前，请务必备份所有重要文件或程序。

## 选择并准备引导介质

为了安装 Red Hat Linux，你必须使用特殊的 Linux 内核引导目标系统。你可以从安装 CD-ROM 引导系统，或者从使用 CD-ROM 上的文件创建的软盘引导。本节将解释这些替代方案，以便你在开始安装时准备好合适的材料。

### 从安装 CD-ROM 引导

大多数最近制造的 PC 都可以从包含适当引导信息的 CD-ROM 引导，例如 Red Hat Linux 安装 CD-ROM 中包含的信息。要从 CD-ROM 引导，系统 BIOS 必须指定系统在尝试从硬盘驱动器或软盘驱动器引导之前，先尝试从 CD-ROM 引导。通常，此 BIOS 设置被标记为 Boot Sequence 或类似名称。

如果系统被设置为引导 DOS，即使系统无法直接从 CD-ROM 引导，你可能也可以使用 CD-ROM 上的文件来引导。文件 `dosutils/autoboot.bat` 会调用 Linux 的 `loadlin` 程序，该程序使用 DOS 系统调用来引导位于硬盘或 CD-ROM 驱动器上的 Linux 内核。

要使用 `autoboot.bat`，请将系统引导进入 DOS 而非 Microsoft Windows。如果系统运行 Microsoft Windows，请使用“关机”对话框以 MS-DOS 模式重启系统。当系统进入 DOS 后，切换到与 CD-ROM 关联的驱动器。然后，通过执行以下命令启动引导序列：

```
dosutils/autoboot.bat
```

系统应该会加载并执行 Linux 内核。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_152_0.png)

DOS 必须被设置为允许访问 CD-ROM，否则此过程将失败。有时 Microsoft Windows 系统存在驱动程序问题或病毒感染，导致无法访问 CD-ROM。你必须纠正这种情况才能启动引导序列。

为了获得引导 Red Hat Linux 的经验，请完成练习 6.3。

## 练习 6.3
### 从 CD-ROM 引导

1. 从 Red Hat Linux CD-ROM 引导系统。
2. 使用 `autoboot.bat` 文件引导系统。

### 从引导软盘引导

如果你无法从 CD-ROM 引导系统，且系统未设置为引导 DOS，你必须准备一个引导软盘来引导系统。最简单的方法是使用 Linux 系统将 CD-ROM 上的镜像文件复制到软盘。镜像文件包含软盘的精确副本。通过将镜像文件复制到磁盘，你创建了用于制作该镜像文件的磁盘的副本。

通过执行以下命令挂载 Red Hat Linux 安装 CD-ROM：
`mount -t iso9660 /dev/cdrom /mnt/cdrom -o ro`

将格式化后的软盘放入软盘驱动器并执行命令：
`dd if=/mnt/cdrom/images/boot.img of=/dev/fd0H1440 obs=18k`

将镜像写入软盘可能需要一分钟左右。当活动停止时，取出磁盘，现在可以使用该磁盘引导目标系统。

> **注意** 如果你计划通过网络而非 CD-ROM 安装 Linux，请复制镜像文件 bootnet.img 而非 boot.img。

如果你在安装过程中需要访问 PCMCIA 设备，则需要第二张软盘。使用类似的命令从 pcmcia.img 文件创建软盘。

如果你无法便捷地访问 Linux 系统，可以使用 DOS 程序 `rawrite` 从镜像文件制作软盘，该程序位于 CD-ROM 的 dosutils 目录中。`rawrite` 程序可以从 DOS 或 Microsoft Windows 的 MS-DOS 提示符窗口运行。该程序会提示输入包含软盘的驱动器盘符（通常为 a:）和镜像文件的路径（通常为 d:\images\boot.img）。

为了获得创建引导软盘的经验，请完成练习 6.4。

## 练习 6.4
### 制作引导软盘

1. 使用 `dd` 命令制作引导软盘。
2. 使用 `rawrite` 制作引导软盘。

## 选择安装介质

大多数用户从安装 CD-ROM 安装 Red Hat Linux。然而，如果你经常安装 Linux，你可能更倾向于设置一个服务器，通过网络提供安装文件。你可以通过以下方法访问 Red Hat Linux 安装文件：

- FTP
- NFS
- HTTP

![](img/4eef9c6f2f52b608eba628cf4e2793ce_154_0.png)

你也可以访问位于本地硬盘上的安装文件。但是，Red Hat Linux 目前不支持通过 Samba 服务器共享的文件进行安装。

## 选择组件和软件包

Red Hat Linux 将相关的程序、配置文件和数据文件组合成一个称为 *软件包*（package）的单元，该单元包含在一个单一文件中。通过将软件包视为一个单元，Red Hat Linux 使安装、更新或卸载程序变得相对简单。软件包包含 *依赖信息*，用于识别正常运行所需的程序或库。通常，除非软件包的依赖关系得到满足，否则 Red Hat Linux 不允许你安装该软件包。这有助于确保安装的程序能够正确运行。

在安装过程中，指定要安装在目标系统上的软件包。你可以通过以下几种方式之一指定软件包：

- 选择 Everything 选项，这表示安装所有可用的软件包。如果你是从安装 CD-ROM 安装，通常不应选择此选项，因为它会安装许多你不太可能用到的软件包。
- 从列表中选择组件。*组件*（component）是一组相关的软件包。例如，GNOME 组件由三十多个对 GNOME 桌面管理器必要或有用的软件包组成。
- 从列表中选择单个软件包。这让你对安装的软件包拥有高度的控制权。



通常，最方便的方法是选择所需的组件，然后根据需要选择或取消选择单个软件包。组件仅在安装过程中定义。Red Hat Linux 没有提供在完成安装过程之后安装组件的机制。一旦安装过程完成，您必须安装单个软件包而不是组件。不过，您可以通过检查安装 CD-ROM 上的 `RedHat/base/comps` 文件来发现构成某个组件的软件包。以下是 Red Hat Linux 6.2 定义的组件列表。

- 匿名 FTP 服务器
- 创作/发布
- 基础
- 开发
- 拨号工作站
- DNS 名称服务器
- DOS/Windows 连通性
- Emacs
- 游戏
- GNOME
- 图形处理
- IPX/NetWare 兼容性
- KDE
- 内核开发
- 邮件/WWW/新闻工具
- 多媒体支持
- 网络管理工作站
- 网络工作站
- 新闻服务器
- NFS 服务器
- Postgres (SQL) 服务器
- 打印机支持
- SMB (Samba) 服务器
- 实用程序
- Web 服务器
- X Window 系统

`rpm` 程序使得在安装完成后安装软件包变得非常简单。因此，在安装期间不一定要精确地选择正确的组件或软件包。

## 总结

在本章中，您学习了在系统中准备安装 Linux 所需的所有知识。涵盖的最重要主题包括：

**安装规划** 如果在开始安装之前收集适当的信息，安装将更加高效且更有成效。

**安装用户界面** 经验丰富的用户可能更倾向于使用文本模式安装用户界面而非图形模式安装用户界面，因为文本模式安装用户界面更可靠且需要的系统资源更少。

**安装类别** Red Hat Linux 让您可以轻松创建 GNOME 或 KDE 工作站或服务器。此外，您还可以指定自定义安装。

**分区结构** 您通常应该定义一个交换分区、一个引导分区和一个根分区。定义额外的分区可能会很有用。

**fdisk 程序** 您可以使用 `fdisk` 分割一个 MS-DOS 分区，从而为安装 Linux 获得可用空间。

**启动 Linux** 您可以使用 Red Hat Linux 安装 CD-ROM 启动 Linux 安装过程，或者利用 CD-ROM 上的文件创建启动软盘。

**安装文件** 安装过程可以访问存储在 CD-ROM 磁盘或硬盘上的安装文件。它还可以通过 FTP、HTTP 或 NFS 访问文件。

**选择组件和软件包** 您可以选择组件（即软件包集）安装到目标系统。此外，您还可以选择或取消选择单个软件包。

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- 组件 (component)
- 依赖信息 (dependency information)
- 图形模式安装过程 (graphical mode installation procedure)
- 镜像文件 (image file)
- 安装类别 (installation classes)
- 安装类型 (installation types)
- `loadlin`
- 软件包 (package)
- `rawrite`
- 根分区 (root partition)
- 文本模式安装过程 (text mode installation procedure)

## 补充信息来源

如果您想进一步了解本章中介绍的主题，应参考以下来源：

- *Red Hat Linux Installation Guide*（Red Hat Linux 安装指南），包含在 Red Hat Linux 安装 CD-ROM 中
- `fdisk` 和 `rawrite` 的文档文件，包含在 Red Hat Linux 安装 CD-ROM 中
- *Linux Partition mini HOWTO*（Linux 分区简易 HOWTO），位于 `/usr/doc/HOWTO/mini` 目录

## 复习题

1. 在为 Red Hat Linux 系统选择硬件时，通常应避免以下哪项？
   A. 具有异常私有接口的 CD-ROM 驱动器
   B. 未列在硬件兼容性列表（HCL）第一级或第二级中的设备
   C. WinModems
   D. WinPrinters

2. 安装过程的图形模式安装用户界面支持以下哪种安装介质来源？
   A. FTP
   B. HTTP
   C. NFS
   D. SMB (Samba)

3. 以下哪个组件由“服务器”安装类别安装，但不由“工作站”安装类别安装？
   A. 匿名 FTP
   B. 多媒体支持
   C. NFS 服务器
   D. SSH 服务器

4. Linux 系统可使用的最大交换空间是多少？
   A. 512MB
   B. 1GB
   C. 4GB
   D. 8GB

5. 以下哪些服务器可以提供 Red Hat Linux 安装过程所需的文件？
   - A. FTP
   - B. HTTP
   - C. NFS
   - D. SMB (Samba)

6. 您应该使用哪个命令来创建 Linux 启动软盘？
   - A. autoboot
   - B. dd
   - C. pcmcia
   - D. rawrite

## 复习题答案

1. A, B, C, D。有问题的 CD-ROM 驱动器、WinModems 和 WinPrinters 将不会被列在 Red Hat Linux 硬件兼容性列表的第一级或第二级中。
2. C。图形模式安装用户界面仅支持 NFS。
3. A, C。服务器安装类别不安装 SSH 服务器；它也不安装由工作站类别安装的多媒体支持。
4. C。Linux 系统可访问的交换空间不超过 4GB。
5. A, B, C。Red Hat Linux 目前不支持通过 Samba 访问安装文件。
6. B, D。在 Linux 下，您使用 dd 命令创建启动软盘；在 DOS 下，您使用 `rawrite` 命令创建启动软盘。

# 第 7 章：安装 Red Hat Linux

本章涵盖的 RHCE 准备主题：

- 理解并能够执行 Red Hat Linux 安装过程。

本章讲解如何安装 Red Hat Linux。讨论重点是图形模式安装，它使大多数 Red Hat Linux 的安装变得快速而简单。接下来的章节将介绍几种特殊的安装选项和设施，包括双启动、网络安装和 Kickstart 安装。

## 安装概述

本节介绍了 Red Hat Linux 安装过程的概述。它讲解了如何使用安装程序的用户界面、如何查看报告安装进度的日志，以及安装过程执行的操作顺序。

### 安装用户界面

安装程序允许您在两种用户界面之间进行选择：图形模式用户界面和文本模式用户界面。

#### 图形模式用户界面

图形模式用户界面的操作类似于人们熟悉的“点选”界面：

- 您可以使用鼠标选择控件（如按钮或文本字段），以及操作复选框和单选按钮。
- 如果您愿意，可以使用 Tab 键在控件之间移动，直到到达您想要选择的控件。
- 您使用键盘输入文本。

#### 文本模式用户界面

文本模式用户界面不是命令行界面，而是一个无需鼠标的低分辨率图形用户界面。它包含熟悉的控件，如文本框、复选框、滚动条和按钮。由于文本模式界面无需鼠标，其使用方式与常见的图形用户界面有所不同。该界面的工作方式如下：

- 您使用 Tab 和 Alt+Tab 在控件之间移动。
- 您按下空格键来选择或取消选择复选框。
- 您使用左、右、上、下键移动光标。
- 您按下 Enter 或空格键来点击高亮的按钮。
- 您按下 Enter 键从列表中选择一项。

## 控制台与消息日志

安装程序使用 Linux 虚拟控制台来显示各种信息。虚拟控制台允许您将键盘和显示器与多个任务中的任何一个关联起来，在文本模式下执行类似于图形模式中使用窗口的功能。虚拟控制台比拥有多个物理控制台更方便，因为它们不需要额外的桌面空间，并且可以轻松地在彼此之间切换。表 7.1 总结了安装期间使用的虚拟控制台。

**表 7.1 安装期间使用的虚拟控制台**

| 控制台 | 按键 | 内容 |
| :--- | :--- | :--- |
| 1 | Ctrl+Alt+F1 | 基于文本的安装过程 |
| 2 | Ctrl+Alt+F2 | Shell 提示符 |
| 3 | Ctrl+Alt+F3 | 来自安装程序的的消息 |
| 4 | Ctrl+Alt+F4 | 内核消息 |
| 5 | Ctrl+Alt+F5 | 其他消息，包括文件系统创建消息 |
| 7 | Ctrl+Alt+F7 | 图形安装过程 |



指定的按键允许您切换到给定的控制台。通过切换到控制台，您可以查看有助于诊断和排除安装问题的消息。控制台 2 提供了一个 shell 提示符，您可以使用它发出命令来解决问题。

## 安装过程概述

安装程序执行的操作如下：

- 开始安装过程
    - 安装模式
    - 语言
    - 键盘
    - 鼠标
    - 安装介质（可选）
    - 安装路径
- 分区和 LILO 安装（可选）
- 网络配置（可选）
- 设置时区
- 指定身份验证选项（可选）
- 指定用户账户
- 选择软件包（可选）
- 配置 X Windows 系统（可选）
- 安装软件包
- 创建启动磁盘（可选）

如您所见，其中若干操作是可选的。可选操作的执行由用户选择、检测到的硬件以及检测到的安装介质决定。本章的其余部分将详细描述安装过程。

## 开始安装过程

要开始安装过程，您必须使用特殊的 Red Hat Linux 安装内核引导目标系统。您可以采用前一章所述的几种方式之一来引导系统。为了引导系统，您必须提供合适的引导介质（例如，引导软盘）。

您还必须配置目标系统的 BIOS，使其从引导介质引导。通常，BIOS 被设置为从内部硬盘引导系统，必须重新配置为从软盘或 CD-ROM 引导。

### 安装模式

系统启动时，将显示如图 7.1 所示的“Welcome to Red Hat Linux”界面。此屏幕允许您选择安装模式：图形（graphical）、文本（text）或专家（expert）。图形模式安装最易于使用。文本模式安装更健壮，但使用起来稍显笨拙。专家模式安装会抑制自动设备探测，并让您几乎完全控制安装过程。专家模式主要在自动设备探测导致系统挂起时有用。否则，通常使用图形或文本模式更为方便。

**图 7.1** 欢迎界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_165_0.png)

```
Welcome to Red Hat Linux 6.2!

o To install or upgrade a system running Red Hat Linux 2.0
  or later in graphical mode, press the <ENTER> key.

o To install or upgrade a system running Red Hat Linux 2.0
  or later in text mode, type text <ENTER>.

o To enable expert mode, type: expert <ENTER>. Press <F3> for
  more information about expert mode.

o To enable rescue mode, type: linux rescue <ENTER>. Press <F5>
  for more information about rescue mode.

o If you have a driver disk, type: linux dd <ENTER>.

o Use the function keys listed below for more information.

[F1-Main] [F2-General] [F3-Expert] [F4-Kernel] [F5-Rescue]
boot: _
```

### 语言

如果您选择了图形模式安装且安装程序检测到 Red Hat Linux CD-ROM，它将立即进入图形模式。否则，即使您选择了图形模式，接下来的几个界面也将以文本模式呈现。

“语言选择”屏幕允许您指定安装程序显示指令的语言。图 7.2 显示了此屏幕的图形模式版本；文本模式版本的功用与之相似，尽管外观有所不同。

**图 7.2** 语言选择界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_166_0.png)

所选语言也将成为目标系统的默认语言。包括语言在内的安装选项可以在安装完成后进行更改。第 9 章“安装后配置安装时选项”解释了如何更改安装选项。

### 键盘

“键盘配置”屏幕允许您选择系统的键盘类型。此屏幕的图形模式版本如图 7.3 所示。图形模式屏幕允许您通过在屏幕底部的文本框中输入字符来测试您的选择。

**图 7.3** 键盘配置界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_167_0.png)

### 鼠标

“鼠标配置”屏幕允许您指定系统的鼠标类型。此屏幕的图形模式版本如图 7.4 所示。“端口（Port）”和“设备（Device）”选项仅在执行串口鼠标配置时需要；对于 PS/2 或总线鼠标，请勿指定这些选项。如果鼠标只有两个按钮，您通常应指定“模拟 3 按钮（Emulate 3 Buttons）”选项。*三键鼠标模拟* 允许您同时按下两键鼠标的两个按钮，以模拟按下缺失的中间鼠标按钮。如果您找不到更匹配的选项，请使用“通用（Generic）”鼠标类型。

**图 7.4** 鼠标配置界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_168_0.png)

### 安装介质

如果您选择了除图形模式以外的安装模式，或者安装程序未能检测到 Red Hat Linux CD-ROM，则会出现如图 7.5 所示的“安装方法”屏幕。此屏幕允许您指定安装介质，可以是 CD-ROM 或本地硬盘上的文件。您还可以通过 FTP、HTTP 或 NFS 安装 Red Hat Linux。但是，您必须使用支持网络安装的特殊引导软盘；第 8 章“高级安装”解释了网络安装。

**图 7.5** 安装方法界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_169_0.png)

如果您选择了图形模式安装，则会出现第二个欢迎屏幕，如图 7.6 所示。此屏幕不包含选项；它仅解释在哪里可以找到介绍安装过程的文档以及如何注册 Red Hat Linux。

**图 7.6** 欢迎使用 Red Hat Linux 界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_169_1.png)

### 安装路径

接下来，您将被提示选择*安装路径*，这定义了安装的类型（*安装* 或 *升级* 类型）和类别（*GNOME 工作站*、*KDE 工作站*、*服务器* 或 *自定义*）。图 7.7 显示了“安装路径”屏幕的图形版本，允许您指定安装路径。

**图 7.7** 安装路径界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_170_0.png)

⚠️ **警告**：如果您为安装类型指定的是“安装（Install）”而非“升级（Upgrade）”，安装程序将删除系统中存在的所有 Linux 分区。

⚠️ **警告**：如果您为安装类别指定的是“服务器（Server）”，安装程序将删除系统中存在的所有分区，包括非 Linux 分区。

💡 **提示**：GNOME 工作站或 KDE 工作站类别不会覆盖现有的非 Linux 分区，除非可用空闲磁盘空间不足。

## 硬盘分区

如果您选择了 GNOME 工作站、KDE 工作站或服务器安装类别，安装程序将提供对系统硬盘进行自动分区的选项。自动分区屏幕的图形模式版本如图 7.8 所示。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_171_0.png)

**图 7.8** 自动分区界面

如果您更倾向于手动分区，请勾选“手动分区（Manually Partition）”复选框。如果您这样做，安装程序将显示“分区（Partitions）”屏幕，允许您访问 Disk Druid（Red Hat Linux 的分区程序）或 `fdisk`（标准 Linux 分区程序）。Disk Druid 屏幕的图形版本如图 7.9 所示。

**图 7.9** 分区界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_172_0.png)

“分区”屏幕显示现有分区（如果有），并提供以下信息：

| 字段 | 描述 |
| :--- | :--- |
| **挂载点 (Mount Point)** | 设备将被挂载的目录名称。使用“编辑”按钮来指定挂载点。交换分区没有挂载点。 |
| **设备 (Device)** | 分区所在设备的名称。 |
| **请求 (Requested)** | 分区的原始大小。您不能更改分区的大小；必须删除该分区并添加一个新分区。 |
| **实际 (Actual)** | 分配给分区的空间量。 |
| **类型 (Type)** | 分区的类型。 |

“分区”屏幕还汇总了每个硬盘驱动器的状态，提供驱动器几何结构、总空间、可用空间和已分配空间。这里有允许您添加、编辑和删除分区的按钮。点击“重置 (Reset)”按钮将 Disk Druid 恢复到原始状态。您可以使用图 7.9 分区窗格右下角所示的“创建 RAID 设备 (Make RAID Device)”按钮来创建软件 RAID 设备。



点击“Add”（添加）按钮将打开一个对话框，允许您添加新分区。该对话框的图形化版本如图 7.10 所示。对话框包含以下字段：

- **Mount Point**（挂载点）允许您指定分区挂载的目录。您不应为交换分区指定挂载点。
- **Size**（大小）分区的容量，单位为 MB。
- **Grow to Fill Disk**（扩展至填满磁盘）指定分区大小应增加，直到分配所有可用空闲空间。
- **Partition Type**（分区类型）分区类型。
- **Allowable Drives**（允许的驱动器）您愿意让 Disk Druid 在放置分区时从中选择的一个或多个驱动器。

**图 7.10** “Add Partition”（添加分区）对话框
![](img/4eef9c6f2f52b608eba628cf4e2793ce_173_0.png)

一旦分区通过自动或手动方式建立，安装程序将显示“Choose Partitions to Format”（选择要格式化的分区）界面，允许您指定哪些分区需要被格式化。图 7.11 显示了该界面的图形模式版本。

**图 7.11** “Choose Partitions to Format”（选择要格式化的分区）界面
![](img/4eef9c6f2f52b608eba628cf4e2793ce_174_0.png)

**警告** 格式化分区会破坏该分区上的所有数据。请务必不要格式化包含有用数据或程序的分区。

## 配置 LILO

如果您指定了“Custom”（自定义）安装类，安装程序将显示 LILO 配置界面。该界面的图形模式版本如图 7.12 所示。

**图 7.12** LILO 配置界面
![](img/4eef9c6f2f52b608eba628cf4e2793ce_175_0.png)

您可以使用 LILO 配置界面指定安装程序跳过创建引导磁盘或安装 LILO。您还可以指定 LILO 应该安装在主引导记录（MBR）上，还是安装在引导分区的第一个扇区。除非系统已经安装了引导管理器（例如 Windows NT loader 或 OS/2 引导管理器），且您希望使用该引导管理器来启动 Linux，否则您应该将 LILO 安装在 MBR 上。

LILO 配置界面允许您禁用线性块寻址（LBA）；为此，请取消勾选“Use Linear Mode”（使用线性模式）复选框。该界面还允许您指定传递给 LILO 或内核的参数。例如，如果您知道一个或多个系统设备无法被自动探测，因此需要内核参数，您可以使用此功能。

LILO 配置界面列出了可引导的分区，并允许您将引导标签与分区关联，以便您可以使用 LILO 引导该分区。您还可以指定一个默认分区，如果在启动时未指定分区，则引导该分区。

## 网络配置

如果安装程序确定系统具有网络适配器，则会显示网络配置界面。该界面的图形模式版本如图 7.13 所示。

**图 7.13** 网络配置界面
![](img/4eef9c6f2f52b608eba628cf4e2793ce_176_0.png)

如果系统有多个网络适配器，网络配置界面将包含允许您选择每个适配器的选项卡。该界面允许您指定以下网络配置信息：

- **Configure Using DHCP**（使用 DHCP 配置）指定在系统启动时从 DHCP 服务器获取网络配置。如果您启用此选项，则无需指定其他网络配置选项或参数。
- **Activate on Boot**（启动时激活）指定在系统启动时启用网络。
- **IP Address**（IP 地址）系统的静态 IP 地址。
- **Netmask**（网络掩码）系统的静态网络掩码。
- **Network Address**（网络地址）系统的静态网络地址。
- **Broadcast Address**（广播地址）系统的静态广播地址。
- **Hostname**（主机名）系统的全限定域名 (FQDN)。
- **Gateway**（网关）系统使用的默认网关。
- **Primary, Secondary, and Ternary DNS Servers**（第一、第二、第三 DNS 服务器）一个或多个用于将主机名解析为 IP 地址的 DNS 服务器。

## 设置时区

时区选择界面（如图 7.14 所示）允许您指定与系统位置相关的时区。您可以使用世界地图或指定与协调世界时 (UTC) 的偏移量来指定时区。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_177_0.png)
**图 7.14** 时区选择界面

您可以指定将系统时钟设置为 UTC。然而，其他操作系统可能不支持此功能，因此如果系统配置为双启动，请在指定此选项时小心。

## 创建用户账户

账户配置界面允许您指定 *root* 用户的密码。该界面的图形化版本如图 7.15 所示。此界面还允许您添加其他用户账户。对于每个账户，您需要指定用户 ID、密码和全名。

**图 7.15** 账户配置界面
![](img/4eef9c6f2f52b608eba628cf4e2793ce_178_0.png)

## 指定身份验证选项

如果您指定了“Custom”（自定义）安装类，则会出现身份验证配置界面。该界面的图形模式版本如图 7.16 所示。

**图 7.16** 身份验证配置界面
![](img/4eef9c6f2f52b608eba628cf4e2793ce_179_0.png)

除非您计划使用网络密码，否则您可以采用安装程序提出的默认值。否则，您必须输入 NIS 域。您也可以输入 NIS 服务器。通常您应该启用 MD5 和 shadow 密码，因为这些选项可以提高系统安全性。

## 选择软件包

如果您选择了“Server”（服务器）或“Custom”（自定义）安装类，则会出现软件包组选择界面。该界面的图形模式版本如图 7.17 所示。

**图 7.17** 软件包组选择界面
![](img/4eef9c6f2f52b608eba628cf4e2793ce_180_0.png)

此界面允许您选择要安装的 *软件包组*（也称为 *组件*）。您也可以取消选择不想安装的软件包组。为了更精确地控制软件包选择，您可以指定“Select Individual Packages”（选择单个软件包）选项。这将导致“Individual Package Selection”（单个软件包选择）界面出现。该界面的图形版本如图 7.18 所示。

**图 7.18** 个别软件包选择界面
![](img/4eef9c6f2f52b608eba628cf4e2793ce_180_1.png)

“Individual Package Selection”界面允许您选择要安装的软件包。您也可以取消选择特定的软件包。点击软件包图标会使安装程序显示关于所选软件包的信息。安装程序使用 Red Hat 软件包管理器 (RPM) 来确定所选软件包是否需要由未选软件包提供的支持。如果是这样，安装程序将显示“Unresolved Dependencies”（未解决的依赖关系）界面。该界面的图形版本如图 7.19 所示。

**图 7.19** “Unresolved Dependencies”（未解决的依赖关系）界面
![](img/4eef9c6f2f52b608eba628cf4e2793ce_181_0.png)

“Unresolved Dependencies”界面允许您指定安装程序是否在您未选择的情况下自动安装所需的软件包。

## 配置 X Window 系统

如果您选择了 X Window 系统的一部分软件包，安装程序将显示 X 配置界面，允许您配置 X。该界面的图形版本如图 7.20 所示。

**图 7.20** X 配置界面
![](img/4eef9c6f2f52b608eba628cf4e2793ce_182_0.png)

安装程序使用 Xconfigurator 来探测并确定系统上显卡和显示器的类型。如果 Xconfigurator 无法识别您的显卡或显示器，它将显示一个硬件列表供您选择。列表中列出了数百种显卡和显示器；向下滚动列表即可找到您的设备。如果您的硬件未列出，您可能仍然能够配置 X。选择“Unlisted Card”（未列出的显卡），并指定您显卡的特性。或者，选择“Custom Monitor”（自定义显示器），并指定显示器的水平和垂直同步范围。

您可以测试配置以确认其是否正常工作。为此，点击“Test This Configuration”（测试此配置）。您还可以选择自定义分辨率或色彩深度。为此，点击“Customize X Configuration”（自定义 X 配置）。

勾选“Use Graphical Login”（使用图形登录）复选框，使 Linux 在系统启动时显示 X 登录界面。如果您更倾向于基于文本的登录，请取消勾选“Use Graphical Login”复选框。

如果您无法配置 X 或不愿尝试，可以通过选择“Skip X Configuration”（跳过 X 配置）来推迟配置。



## 安装软件包

最后，安装程序将显示“即将安装”界面。该界面的图形模式版本如图 7.21 所示。到此为止，您指定的配置更改已存储在 RAM 内存中。此时您可以直接启动，而不会影响目标系统的配置。然而，点击“下一步”将提交这些更改。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_183_0.png)

**图 7.22 安装软件包界面**

![](img/4eef9c6f2f52b608eba628cf4e2793ce_184_0.png)

“安装软件包”界面允许您监控软件包安装的进度。“下一步”按钮在软件包安装完成之前处于禁用状态。

#### 创建启动盘

除非您指定不需要启动盘，否则安装程序将显示“创建启动盘”界面。该界面的图形版本如图 7.23 所示。

**图 7.23 创建启动盘界面**

![](img/4eef9c6f2f52b608eba628cf4e2793ce_185_0.png)

您可以通过点击“跳过创建启动盘”然后点击“下一步”来跳过启动软盘的创建。然而，在大多数情况下，您不应该这样做；如果您发现无法从硬盘启动 Linux，启动盘将非常有用。要创建启动软盘，请将一张空白软盘放入软盘驱动器，然后点击“下一步”。

## 完成安装

接下来，安装程序将显示“恭喜”界面，这标志着安装的完成。该界面的图形版本如图 7.24 所示。

**图 7.24 恭喜界面**

![](img/4eef9c6f2f52b608eba628cf4e2793ce_186_0.png)

如果您创建了启动盘，应将其从软盘驱动器中取出，然后点击“退出”。计算机将自动重启。不过，您可能需要设置系统的 BIOS，以便系统从硬盘启动。现在，通过完成练习 7.1 来实践安装 Red Hat Linux。

### 练习 7.1：安装 Red Hat Linux

执行以下安装操作，尝试多种选项，以便了解它们的作用：

- GNOME 工作站的图形模式安装
- 服务器的文本模式安装
- 图形模式的自定义安装
- 专家模式安装

在每次安装完成后，检查安装日志并熟悉其典型内容。了解日志应有的样子将有助于您发现实际安装中的问题。

## 总结

在本章中，您学习了如何安装 Red Hat Linux。涵盖的最重要主题包括：

- **安装模式**：您可以使用图形模式、文本模式或专家模式安装 Linux。
- **虚拟控制台**：您可以使用 Linux 虚拟控制台来监控安装过程。
- **操作顺序**：安装过程中的若干步骤是可选的。它们可以根据用户输入、检测到的硬件和检测到的安装介质而被跳过。
- **安装路径**：安装路径定义了安装类型和类别。
- **分区**：硬盘可以自动分区或手动分区。
- **网络配置**：通过将系统配置为使用 DHCP 服务器（可用时），网络配置可以在启动时自动执行。
- **选择软件包**：您可以按组件选择软件包。您也可以选择单个软件包。GNOME 工作站、KDE 工作站和服务器安装类别会自动为您选择软件包。
- **X 配置**：安装程序通常可以识别并为您的显卡硬件自动配置 X。如果您愿意，可以推迟配置 X。
- **启动盘**：您通常应该创建启动盘，如果您的 Linux 系统无法从硬盘启动，这会非常方便。

### 关键术语

在参加 RHCE 考试之前，请确保您熟悉以下术语：

- components（组件）
- Custom installation class（自定义安装类别）
- GNOME Workstation installation class（GNOME 工作站安装类别）
- installation path（安装路径）
- Install installation type（安装安装类型）
- KDE Workstation installation class（KDE 工作站安装类别）
- package groups（软件包组）
- Server installation class（服务器安装类别）
- three-button mouse emulation（三键鼠标模拟）
- Upgrade installation type（升级安装类型）

## 其他信息来源

如果您想进一步了解本章介绍的主题，应参考以下来源：

- 《官方 Red Hat Linux 安装指南》
- 《官方 Red Hat Linux 入门指南》
- 《官方 Red Hat Linux 参考指南》

这些文档可在 Web 上的 `www.redhat.com/support/manuals` 获取。

## 复习题

1. 以下哪些是 Red Hat Linux 的安装模式？
   A. 专家 (Expert)
   B. 图形 (Graphical)
   C. 文本 (Text)
   D. 升级 (Upgrade)

2. 关于图形模式安装，以下哪项是正确的？
   A. 您可以使用 Tab 键选择控件。
   B. 您可以使用键盘输入文本。
   C. 您可以使用鼠标从列表中选择一项。
   D. 您可以使用鼠标选择控件。

3. 关于文本模式安装，以下哪项是正确的？
   A. 您可以使用 Tab 键选择控件。
   B. 您可以使用键盘输入文本。
   C. 您可以使用鼠标从列表中选择一项。
   D. 您可以使用鼠标选择控件。

4. 专家模式的主要目的是什么？
   A. 给同事和朋友留下深刻印象
   B. 省略设备探测
   C. 指定启动参数
   D. 支持网络安装

5. 以下哪个选项正确地将虚拟控制台与其安装程序功能配对？
   A. 1，基于文本的安装程序
   B. 2，shell 提示符
   C. 3，安装程序消息
   D. 4，内核消息

6. 以下哪些安装功能是可选的？
   A. 分区
   B. 网络配置
   C. 设置时区
   D. 身份验证配置

7. 关于两键鼠标，以下哪项是正确的？
   A. 它是一个总线鼠标。
   B. 它是一个 PS/2 鼠标。
   C. 它是一个串行鼠标。
   D. 对于两键鼠标，您通常应该启用三键模拟。

8. 自动分区是为哪种安装类别执行的？
   A. 专家安装类别
   B. GNOME 工作站安装类别
   C. KDE 工作站安装类别
   D. 服务器安装类别

9. 什么是挂载点？
   A. 与可移动设备关联的设备文件
   B. 与可挂载设备关联的目录
   C. 插入驱动器的软盘的一面
   D. 您插入安装介质的时间

10. 在其他分区已经分配的情况下，您应该怎么做才能使某个分区尽可能大？
    A. 输入一个很大的数字作为分区大小。
    B. 输入一个负数作为分区大小。
    C. 启用“Allowable Type”选项。
    D. 启用“Grow to Fill”选项。

11. 如果您计划双启动 OS/2 和 Linux，应该在哪里安装 LILO？
    A. 在内存中
    B. 在 CD-ROM 上
    C. 在 Linux 启动分区的第一个扇区
    D. 在主引导记录 (MBR) 上

12. 当您将系统配置为使用 DHCP 时会发生什么？
    A. 在启动时执行身份验证。
    B. 在启动时执行 LILO 安装。
    C. 在启动时执行网络配置。
    D. 在启动时执行分区。

13. 如果您使用“时区”界面指定系统时钟设置为 UTC，会发生什么？
    A. 双启动操作系统可能会出现故障。
    B. 时间将保持得更准确。
    C. 时间将保持得稍微不那么准确。
    D. 您不需要指定时区。

14. 通常应该设置以下哪个身份验证选项？
    A. MD5 密码
    B. NIS 域名
    C. NIS 服务器
    D. Shadow 密码

15. “未解决的依赖关系”界面何时会出现？
    A. 当磁盘几何结构不合适时。
    B. 当您指定安装的软件包需要额外软件包时。
    C. 当您输入含糊不清的信息时。
    D. 当系统资源不足时。



16. 安装程序使用哪个程序来配置 X？

**A.** Xconfig
**B.** Xconfigurator
**C.** XF86Config
**D.** XF86Setup

17. 如果无法使用系统的 CD-ROM 驱动器启动安装程序，以下哪个是合适的应对措施？

**A.** 修改 BIOS 设置以允许从 CD-ROM 启动。
**B.** 安装内存升级。
**C.** 从启动软盘启动。
**D.** 使用 `autoboot.bat` 启动。

18. 为什么你应该创建启动盘？

**A.** 创建启动盘可以证明 Linux 已正确安装。
**B.** 你可以用它来启动系统。
**C.** 在安装完成之前，你无法从硬盘启动系统。
**D.** 安装完成后你无法创建启动盘。

## 复习题答案

- 1. A, B, C。升级（Upgrade）是一种安装类型，而不是安装模式。
- 2. A, B, C, 和 D。在图形模式安装期间，你可以使用多种技术。
- 3. A, B。在文本模式安装期间，你不能使用鼠标。
- 4. B。专家模式安装让你能够避免可能会导致系统挂起的设备探测。
- 5. A, B, C, D。表 7.1 总结了安装程序对虚拟控制台的使用。
- 6. A, B, D。分区可以自动执行。仅在存在网络适配器时才执行网络配置。身份验证配置仅在自定义安装期间发生。
- 7. D。使用 X 时首选三键鼠标。如果你使用的是两键鼠标，通常应启用三键模拟。
- 8. B, C, D。没有“专家”安装类。除自定义（Custom）以外的安装类都会被自动格式化。
- 9. B。挂载点是通过 mount 命令将挂载设备绑定到的目录。
- 10. D。当你启用“扩容至填满”（Grow to Fill）选项时，安装程序会将分区尽可能地扩大。
- 11. C。你应该使用 OS/2 启动管理器，通过从启动分区获取 LILO 来加载 Linux。
- 12. C。DHCP 服务器可以在启动时向系统提供网络配置信息。
- 13. A。另一个操作系统可能不支持将系统时钟设置为 UTC。将时钟设置为 UTC 对精度没有影响。系统必须知道本地时区，因此必须设置时区。
- 14. A, D。仅当你计划使用网络密码时，才指定 NIS 域或服务器。
- 15. B。“未解决的依赖关系”（Unresolved Dependencies）屏幕会告知你可能需要安装额外的软件包。
- 16. B。安装程序使用 `Xconfigurator` 来配置 X。
- 17. A, C, D。许多系统——尤其是旧系统——无法从 CD-ROM 驱动器启动。
- 18. B。如果系统的启动信息损坏，启动盘会非常方便。

# 第 8 章：高级安装

本章涵盖的 RHCE 准备主题：

- 理解并在兼容的笔记本电脑上安装 Red Hat Linux。
- 理解并在多启动（multi-boot）配置中安装 Red Hat Linux。
- 理解如何配置和排除 Linux 加载程序 LILO 的故障。
- 理解并在安装期间需要 PCMCIA 支持的计算机上安装 Red Hat Linux。
- 理解并能够使用网络服务器提供安装介质访问权限来安装 Red Hat Linux。
- 理解并能够执行 Red Hat Linux 的自动化（kickstart）安装。

本章涵盖了一些与安装相关的琐碎内容。它解释了如何处理几种不寻常的安装类型，如何配置和排除几种 Linux 设施的故障，以及如何利用网络服务器执行安装。尽管其中一些主题看起来重要性较低，但考试问题很容易涉及这些主题。请务必投入足够的时间掌握本章，特别注意不熟悉的主题。

## 在笔记本电脑上安装 Linux

在笔记本电脑上安装 Linux 经常会出现复杂情况。最大的障碍是笔记本电脑制造商通常不会在给定型号的笔记本电脑中使用标准化的组件。例如，在不同时间或地点制造的笔记本电脑可能配备不同的声卡。因此，一名笔记本电脑用户在安装 Linux 时可能没什么困难，但另一名拥有相同型号笔记本电脑并遵循相同安装步骤的用户可能无法正确配置 Linux。更复杂的是，笔记本电脑技术的进步速度比台式机技术更快，制造商每隔几个月就会推出新机型。

第二个障碍是笔记本电脑比台式机更倾向于使用不广泛使用的集成组件和芯片组。支持此类组件和芯片组的 Linux 驱动程序有时无法获得。例如，许多笔记本电脑使用的视频硬件不受 XFree86 支持，或者声音硬件不受标准 Linux 内核和驱动程序支持。你可能可以获得商业 X 服务器或声卡驱动程序来支持不寻常的硬件。例如，请参阅 Metro Link 的 Metro-X X Server (www.metrolink.com) 和 4Front Technologies 的 Open Sound System (www.opensound.com)。

笔记本电脑比台式机更可能使用 PCMCIA 和高级电源管理（APM）。Red Hat Linux 支持 PCMCIA 和 APM，但你可能需要配置这些设施以使用所有可用设备并优化系统性能；这给安装和配置过程增加了几个步骤。本章随后的章节将解释如何在安装期间访问 PCMCIA 设备。第 15 章“理解配置文件和脚本”解释了如何配置和使用 PCMCIA 及 APM。

一些笔记本电脑制造商已经开始提供预装 Red Hat Linux 的笔记本电脑。如果你能选择笔记本电脑，你可能会发现选择其中一台很方便。否则，请参考 Linux on Laptops 网页：www.cs.utexas.edu/users/kharker/linux-laptop。该网页包含丰富的资源，包括：

- 在特定笔记本型号上运行 Linux 的笔记链接
- 关于配置 XFree86 以在 LCD 显示器上工作的信息链接
- 关于典型笔记本组件（如 PCMCIA）的信息链接
- 关于在笔记本电脑上运行 Linux 的文章和演示文稿链接
- 在笔记本电脑上运行 Linux 时有用的特殊 Linux 软件链接
- 讨论 Linux 笔记本问题的论坛链接

你还应该参考 Linux Laptop HOWTO (home.snafu.de/wehe/howtos.html)。该 HOWTO 还包含了在掌上电脑和其他设备（如手机和计算器）上使用 Linux 的信息。

## 执行多启动安装

许多 Linux 用户希望在单台计算机上托管多个操作系统，这被称为*多启动配置*（multi-boot configuration）。配置为多启动操作的计算机通常不会直接启动某个操作系统，而是启动一个名为“启动加载程序”（boot loader）的特殊程序，允许用户选择已安装的操作系统，然后加载用户的选择。台式机用户经常将系统配置为启动 Microsoft Windows 或 Linux。然而，也可以配置支持 Windows NT 和其他操作系统（如 IBM 的 OS/2）的多启动配置。

在多启动配置中，每次启动系统时，你都会选择想要启动的操作系统。不过，与其将系统配置为多启动操作，你可以安装特殊软件，让你同时使用 Windows 程序和 Linux。例如，WINE 项目 (www.winehq.com) 正在 Linux 下实现 Win32 API。现在，你已经可以使用 WINE 在 Linux 下运行许多常见的 Windows 程序。

在 Linux 下运行 Windows 程序的另一种方法是 VMware, Inc. 的产品 VMware，它允许你在 Linux 下运行 Windows 9x 或 Windows NT 操作系统。或者，Windows NT 版本的 VMware 允许你在 Windows NT 下运行 Linux。该公司的网站是 www.vmware.com。VMware 最有用的功能之一是能够在单台计算机上同时运行多个版本的 Linux。通过这样做，你可以在不干扰运行中的服务器的情况下，安装、配置和测试新版本的 Linux 及其软件。

本节将解释用于配置多启动系统的*多启动安装*。前几个小节描述了 Linux 加载程序 LILO 的使用、配置和故障排除。随后的章节解释了在多启动配置中安装 Linux 的步骤。

### 使用和配置 LILO

Linux 加载程序 LILO 可以充当*主启动加载程序*（primary boot loader）或*次启动加载程序*（secondary boot loader）。当用作主启动加载程序时，LILO 被安装在硬盘的主引导记录（MBR）中，以便系统 BIOS 在系统启动时加载 LILO。随后 LILO 控制 Linux 和其他已安装操作系统的启动。

一些操作系统有相关的启动加载程序。例如，Windows NT 有一个名为 NT Loader 的启动加载程序，IBM 的 OS/2 有一个名为 Boot Manager 的启动加载程序。通常，使用其相关的启动加载程序来启动操作系统会更容易。常见的启动加载程序也可以配置为启动 Linux。为此，请将 LILO 安装在 `/boot` 分区的引导扇区中，并为 Linux 创建一个指向 `/boot` 分区的启动加载程序条目。在这种配置中，LILO 充当次启动加载程序：它提供了启动 Linux 的手段，但不启动任何其他操作系统。



## 执行多启动安装

当配置为主引导加载程序时，LILO 在加载后通常会立即显示 `LILO:` 提示符。该提示符被称为*引导提示符（boot prompt）*，它提供了一个机会来选择要启动的引导镜像，或者输入控制引导和启动过程的 Linux 引导参数。如果 LILO 被配置为不显示提示符，按下 Shift 或 Caps Lock 键将强制显示 `LILO:` 提示符。

如果在响应 LILO 提示符时按下 Tab 键，LILO 将显示其配置的可引导镜像。要启动某个镜像，请输入 LILO 显示的标签并按下 Enter 键。通常，标签 `dos` 指的是 Microsoft Windows，标签 `linux` 指的是 Linux。不过，如接下来的小节所述，您可以配置 LILO 来显示您选择的标签。例如，您可能更愿意将标签 `Win95` 与 Microsoft Windows 95 操作系统相关联。

通常，LILO 被配置为如果在定义的时间段内用户未能选择引导镜像，则自动启动默认引导镜像。如果有默认引导镜像，它就是您在响应提示符按下 Tab 键时列出的第一个。您可以通过按下 Shift 或 Caps Lock 键来禁用自动启动功能。如果您想立即启动默认引导镜像，请在响应 LILO 提示符时按下 Enter 键。不过，如果您愿意，也可以配置 LILO 忽略这些 Shift 和 Caps Lock 功能。

引导*参数（arguments）*允许您控制引导和启动过程。许多引导参数采用 `name=value` 形式。LILO 识别并处理几种此类参数，但如果 LILO 不识别某个 `name=value` 参数，或者参数具有其他形式，LILO 会将该参数传递给内核。随后，内核将尝试识别并处理该参数。如果内核不识别该参数，它会将其传递给第一个进程，通常是 `init`。内核将 `name=value` 参数作为环境变量传递，而使用其他形式的参数来调用第一个进程。

引导参数最常见的用途是以单用户模式启动系统。在单用户模式下启动时，系统仅挂载根文件系统，并仅启动与运行级别 1 相关的系统进程。以单用户模式引导系统可能有利于故障排除和修复。

要以单用户模式启动系统，请在操作系统名称后面输入 `S`、`single` 或 `1`。例如，您可以按如下方式以单用户模式启动 Linux：

```
LILO: linux S
```

请参阅练习 8.1 以获得 LILO 提示符的操作经验。

### 练习 8.1：使用 LILO 提示符

为了更好地熟悉多个引导镜像以及以单用户模式引导 Linux，请在配置了多启动操作的系统上执行以下每个步骤。

- 1. 使用 Tab 键查看有哪些可用的引导镜像。
- 2. 引导每个可用的操作系统。
- 3. 以单用户模式引导 Linux。

## 配置 LILO

安装程序通常会代表您正确配置 LILO。然而，在为多启动操作配置系统时，您可能会发现有必要在安装后微调 LILO 配置。为此，您可以使用 `linuxconf` 程序。不过，RHCE 考试可能会包含测试您手动配置 LILO 能力的问题或练习。本小节将解释 LILO 的配置文件及其使用方法。

LILO 的配置文件是 `/etc/lilo.conf`。要安装新的 LILO 配置，请使用文本编辑器修改配置文件，然后运行 LILO 映射安装程序 `/sbin/lilo`。以下是一个 LILO 配置文件示例，它展示了最重要的配置选项：

```
boot=/dev/hda
map=/boot/map
install=/boot/boot.b
prompt
delay=50
timeout=3000
default=dos

image=/boot/vmlinuz-2.2.12-20
	label=old
	root=/dev/hda4
	read-only

image=/boot/vmlinuz-2.2.12-20b1
	label=linux
	root=/dev/hda4
	read-only

other=/dev/hda1
	label=dos
```

该配置文件包含四个节（stanzas）。第一节由前六行组成，指定了全局参数。表 8.1 描述了同一配置中出现的全局参数。每个剩余的节描述了 LILO 应提供引导的引导镜像。前两个引导镜像与 Linux 相关，最后一个引导镜像与 Microsoft Windows 相关。表 8.2 描述了用于指定引导镜像的参数。

请注意，两个 Linux 引导镜像都指向同一个分区。这种安排允许您选择用于引导系统的内核，在安装新内核时非常有用。如果新内核无法正常工作，您可以使用 LILO 提示符加载旧内核。

**表 8.1 LILO 全局参数**

| LILO 全局参数 | 描述 |
| :--- | :--- |
| boot | 指定写入引导信息的设备或分区。若要将 LILO 安装到 MBR（此时它将作为主引导加载程序），请指定设备（例如 `/dev/hda`）。或者，若要将 Linux 安装到分区的引导扇区（此时它将作为次级引导加载程序），请指定分区（例如 `/dev/hda3`）。 |
| default | 指定默认引导镜像。 |
| delay | 指定 LILO 在引导默认引导镜像之前等待的时间量（单位为 0.1 秒）。 |
| install | 指定安装为新引导扇区的文件。 |
| map | 指定映射文件的名称，其中包含引导镜像的名称和位置。 |
| prompt | 指定 LILO 将显示引导提示符。 |
| timeout | 指定 LILO 在引导默认引导镜像之前等待键盘输入的时间量（单位为 0.1 秒）。 |

**表 8.2 LILO 引导镜像参数**

| LILO 全局参数 | 描述 |
| :--- | :--- |
| image | 指定与引导镜像相关的 Linux 内核（Linux 引导镜像必填）。 |
| label | 指定与引导镜像相关的标签。 |
| other | 指定包含可引导非 Linux 镜像的分区（非 Linux 引导镜像必填）。 |
| read-only | 指定根分区最初应作为只读分区挂载。 |
| root | 指定与 Linux 引导镜像相关的根分区（Linux 引导镜像必填）。 |

现在尝试练习 8.2，看看您是否理解如何配置 LILO。

### 练习 8.2：配置 LILO

- 1. 为您的系统创建启动盘，以便即使 LILO 配置错误，您也能启动系统。
- 2. 修改 LILO 配置以指定不同的超时时间（timeout）、延迟时间（delay）和默认镜像（default）。
- 3. 修改与引导镜像相关的标签。
- 4. 运行 `/sbin/lilo` 以更新引导映射并安装引导扇区。
- 5. 引导系统，验证您的更改是否按计划生效。

### LILO 错误信息

LILO 实际上分两个阶段加载。LILO 的第一阶段位于 MBR 或分区的引导扇区中，具体取决于 LILO 是安装为主引导加载程序还是次级引导加载程序。LILO 的第二阶段位于 `/boot/boot.b` 文件中。LILO 在加载时逐字显示其提示符。因此，不完整的 LILO 提示符可以提供有关出错位置的有用信息。LILO 有时会显示一个表示错误状态的修改后的提示符。表 8.3 描述了 LILO 的错误信息。

**表 8.3 LILO 错误信息**

| 提示符 | 含义 |
| :--- | :--- |
| 无内容 | LILO 未加载。 |
| L | 第一阶段已加载。 |
| LI | 第二阶段已加载。 |
| LIL | 第二阶段已启动。 |
| LIL? | 第二阶段加载到了错误的地址。 |
| LIL- | 描述符表损坏。 |
| LILO | LILO 已正确加载。 |

## Windows 9x

配置一个同时引导 Microsoft Windows 9x 和 Linux 的多启动系统非常简单。如果可能，您应该在安装 Linux 之前安装 Microsoft Windows。然后，如果您执行 Red Hat Linux 的“工作站（Workstation）”或“自定义（Custom）”安装，安装程序可以自动配置系统以引导这两个操作系统。只需确保安装程序的 LILO 配置对话框中列出了包含 Microsoft Windows 的分区即可。



如果您必须先安装 Linux 然后再安装 Microsoft Windows，请务必为 Windows 分区留出空间，该分区必须位于硬盘的可引导区域（通常在 1024 柱面以下）。此外，请务必创建 Linux 启动盘，因为 Windows 的安装过程会覆盖 MBR，从而破坏 LILO。Windows 安装完成后，使用启动盘引导 Linux，修改 LILO 配置以包含 Windows 启动镜像，并运行 `/sbin/lilo` 来重新安装 LILO。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_204_0.png)

您可能会发现使用 BIOS 关闭 ISA 插槽的即插即用（plug-and-play）功能很有帮助。否则，Windows 可能会使用即插即用来更改与设备相关的系统资源，导致该设备在 Linux 中无法使用，直到您重新配置该设备。

请参阅练习 8.3，以确认您已理解如何配置一个可引导 Linux 和 Windows 9x 的多启动系统。

## 练习 8.3
### 配置可引导 Linux 和 Windows 9x 的系统

- 1. 配置一个使用 Windows 9x 和 Linux 的多启动操作系统。
- 2. 如果您有一台 Windows 9x 笔记本电脑，请在笔记本上安装 Linux 并将其配置为多启动操作。请务必尝试安装并配置 XFree86。

## Windows NT

配置一个可引导 Windows NT 和 Linux 的多启动系统比配置一个可引导 Windows 9x 和 Linux 的多启动系统要稍微困难一些。同样，如果您在安装 Linux 之前先安装 Windows NT，任务会更容易。然而，Linux 安装程序不会像对待 Windows 9x 那样自动配置系统以引导 Windows NT。

您可以使用 Windows NT 加载程序来引导 Linux。Windows NT 加载程序的配置存储在隐藏文件 `c:\boot.ini` 中。以下是一个 NT 加载程序配置文件的示例：

```
[boot loader]
timeout=60
default=multi(0)disk(0)rdisk(1)partition(1)\WINNT
```

```
[operating systems]
multi(0)disk(0)rdisk(1)partition(1)\WINNT="Windows NT Workstation Version 4.00"
multi(0)disk(0)rdisk(1)partition(1)\WINNT="Windows NT Workstation Version 4.00 [VGA mode] " /basevideo /sos
c:\="Microsoft Windows 95"
```

该配置文件包含两个由方括号内的标题分隔的节（stanza）。第一个节标题为 `[boot loader]`。它包含两行：一行指定超时时间，另一行指定默认引导镜像。该超时时间的工作方式与 LILO 的超时时间非常相似。如果在指定的时间段内没有收到对提示的响应，NT 将自动引导默认镜像。默认引导镜像由其磁盘号（rdisk）和分区号（partition）指定，两者都相对于 0 编号。示例配置中的默认引导镜像位于指定分区的文件系统的 `\WINNT` 目录下。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_205_0.png)

`boot.ini` 文件的 multi 和 disk 参数用于 SCSI 磁盘。为了准备 RHCE 考试，您不需要学习这些与 NT 相关的细节。

第二个节标题为 `[operating systems]`。该节的每一行指定一个引导镜像和一个相关的标签（由双引号括起来）。出现了两种指定形式：一种用于指定 NT 引导镜像，另一种用于指定非 NT 引导镜像。在示例配置中，前两行指定了 NT 引导镜像，第三行指定了非 NT 引导镜像。

要配置 NT 引导 Linux，请使用 LILO 作为二级引导加载程序安装 Linux。请务必创建启动盘，以便在重新配置 NT 加载程序之前能够引导 Linux。

假设 `/dev/hda3` 分区是 Linux 挂载为 `/boot` 的分区。引导 Linux 并执行以下命令：

```
dd if=/dev/hda3 of=/boot/linux.ldr bs=512 count=1
```

该命令将 Linux 引导扇区从 `/boot` 分区复制到文件 `/boot/linux.ldr` 中。

将 MS-DOS 格式的软盘插入软驱，并执行以下命令：

```
mount -t msdos /dev/fd0 /mnt/floppy
cp /boot/linux.ldr /mnt/floppy
umount /dev/fd0
```

取出软盘，引导 NT。插入软盘，将 `linux.ldr` 文件从软盘复制到 `c:\` 目录。使用文本编辑器将以下行添加到 `boot.ini` 文件中：

```
c:\linux.ldr="Linux"
```

当您引导 NT 时，NT 加载程序会显示一行标有 Linux 的新选项。只需突出显示该新行并按 Enter 键即可引导 Linux。

请注意，如果 Windows NT 系统使用的是 FAT 而非 NTFS 文件系统，您可以直接将 `/boot/linux.ldr` 文件复制到正确的 Windows NT 文件系统中，而无需使用软盘。只需挂载文件系统，复制文件，然后卸载文件系统即可。另请注意，如果您愿意，也可以使用 LILO 引导 Windows NT。只需将 Windows NT 系统添加到 LILO 配置文件中，指定 `other` 和 `label 1` 指令。然后，运行 `/sbin/lilo` 以更新引导映射并安装修改后的引导扇区。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_206_0.png)

如果您重新编译 Linux 内核，必须运行 `/sbin/lilo`，然后重复引导扇区安装步骤。否则，NT 加载程序将无法找到并加载新内核。

请参阅练习 8.4，以检查您现在是否理解如何配置一个可引导 Linux 和 Windows NT 的多启动系统。

## 练习 8.4
### 配置可引导 Linux 和 Windows NT 的系统

配置一个使用 Windows NT 和 Linux 的多启动操作系统。

## 其他操作系统

您可以配置 Linux 引导其他操作系统，或被其他操作系统引导，包括 OS/2、FreeBSD 和 NetBSD。配置过程通常类似于 Windows NT 或 Windows 9x 的配置，具体取决于您倾向于将 LILO 用作主引导加载程序还是二级引导加载程序。请查阅相关操作系统的文档以确定如何操作。您可能会发现 USENET 新闻组在解决遇到的任何问题和疑问方面很有帮助。

## 特殊安装

本节将解释如何执行几种特殊类型的安装：

- **PCMCIA 安装**：必须访问 PCMCIA 硬件才能执行的安装。
- **网络安装**：访问由网络服务器提供的分发文件的安装。
- **Kickstart 安装**：在脚本控制下基本自动进行安装。

### 执行 PCMCIA 安装

如果在 Linux 安装期间需要访问 PCMCIA 硬件，必须使用特殊的启动盘。特殊启动盘的镜像位于 Red Hat Linux CD-ROM 的 images 目录下的 `pcmcia.img` 文件中，与普通 `boot.img` 文件在同一位置。

使用第 6 章“安装规划”中描述的步骤从该镜像文件创建启动盘。要开始安装程序，请使用该磁盘引导系统。

**警告**：为了安装旧版本的 Red Hat Linux，您需要使用标准启动盘和一个补充 PCMCIA 磁盘。部分 Red Hat 文档尚未更新以反映新流程。

**警告**：部分 Red Hat CD-ROM 包含错误的安装镜像。如果在使用 PCMCIA 时遇到安装问题，请检查 Red Hat FTP 服务器以获取更新的镜像。

现在请尝试练习 8.5，自行执行一次 PCMCIA 安装。

| 练习 8.5 |
| :--- |
| **执行 PCMCIA 安装** |
| 如果您可以使用 PCMCIA CD-ROM 驱动器，请使用它安装 Linux。 |

## 执行网络安装

安装 Red Hat Linux 的一种常用方法是通过分发 CD-ROM。但是，您也可以从驻留在 FTP、HTTP (Web) 或 NFS 服务器上的分发介质安装 Red Hat Linux。这被称为 *网络安装*。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_208_0.png)

Red Hat Linux 曾经支持通过 Samba (SMB) 进行网络安装，但现在不再支持。

在 Red Hat Linux 6.2 之前，解析包含服务器在内的域的主机名的 DNS 服务器必须能够为服务器提供反向名称查找。DNS 服务器必须能够将服务器的 IP 号映射到服务器的主机名。在 Red Hat Linux 6.2 中，这不再必要。

如果服务器通过多种服务提供对分发介质的访问，那么仅存储一次介质会很有用。以下命令序列创建了一个分发介质的副本，该副本可通过 FTP 和 HTTP 访问：

```
cp -a /mnt/cdrom/RedHat /home/ftp/pub
ln -s /home/ftp/pub/RedHat /home/httpd/html/RedHat
```

要通过 NFS 提供对介质的访问，请在 `/etc/exports` 文件中包含以下行以导出 `/home/ftp/pub/RedHat` 目录：

```
/home/ftp/pub/RedHat (ro)
```

有关设置 FTP、HTTP 和 NFS 服务的更多信息，请参阅第 21 章“安装和配置主要网络服务”。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_208_1.png)

您可以通过 NFS 执行图形模式安装，但不能通过 FTP 或 HTTP 执行。

要通过网络服务器安装 Red Hat Linux，请使用分发 CD-ROM 的 `images` 目录中的镜像文件 `bootnet.img` 创建启动盘。然后，通过此磁盘引导以开始安装程序。请注意，网络安装使用文本模式而非图形模式，因此安装菜单不会为您提供执行图形模式安装的选项。在您选择语言和键盘后，将出现如图 8.1 所示的“安装方法”屏幕。选择将提供安装介质访问权限的服务，然后点击 OK。



### 图 8.1 安装方法界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_209_0.png)

请记住，在执行文本模式安装时，不需要使用鼠标点击按钮。请使用导航键选择按钮，然后按 Enter 键或空格键进行点击。

如果您选择 NFS，将出现如图 8.2 所示的 NFS 设置界面。在此界面中指定 NFS 服务器的主机名（或 IP 地址）以及包含发行版 CD-ROM 中 `RedHat` 子目录的导出目录名称。

### 图 8.2 NFS 设置界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_209_1.png)

如果您选择 FTP，将出现如图 8.3 所示的 FTP 设置界面。在此界面中指定 FTP 服务器的主机名（或 IP 地址）以及包含发行版 CD-ROM 中 RedHat 子目录的目录名称。

### 图 8.3 FTP 设置界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_210_0.png)

如果您选择 HTTP，将出现如图 8.4 所示的 HTTP 设置界面。在此界面中指定 HTTP 服务器的主机名（或 IP 地址）以及包含发行版 CD-ROM 中 RedHat 子目录的目录名称。

### 图 8.4 HTTP 设置界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_210_1.png)

在指定了服务器的主机名（或 IP 地址）以及包含发行介质的目录后，将出现如图 8.5 所示的配置 TCP/IP 界面。如果客户端可以通过 BOOTP 或 DHCP 获取其网络配置，请选择“使用动态 IP 配置”并点击 OK。否则，请指定客户端应使用的 IP 地址、网络掩码、网关和 DNS 服务器，然后点击 OK。

### 图 8.5 配置 TCP/IP 界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_211_0.png)

一旦您指定了 TCP/IP 信息，安装程序将通过服务器访问发行介质。此后，安装将照常进行。

现在尝试练习 8.6，自行执行 FTP、HTTP 和 NFS 网络安装。

### 练习 8.6：执行网络安装

如果您可以使用网络服务器，请执行以下安装。

- 1. 执行 FTP 安装。
- 2. 执行 HTTP 安装。
- 3. 执行 NFS 安装。

否则，在阅读完第 21 章后，配置一个合适的服务器，然后再执行这些安装。

## 执行 Kickstart 安装

*Kickstart 安装* 是一种特殊的安装类型，其中对安装对话框的响应来自脚本而非用户输入。当脚本存储在软盘上时，其名称为 `ks.cfg`；当通过 NFS 访问脚本时，您可以指定其名称。您可以编写自己的 kickstart 脚本，但使用 `mkkickstart` 程序根据已完成的安装创建脚本会简单得多。然后您可以根据需要修改该脚本。

### 使用 mkkickstart

`mkkickstart` 程序默认不安装，因此通常的第一步是使用以下命令安装 `mkkickstart` 软件包：

```bash
rpm -Uvh /mnt/cdrom/RedHat/RPMS/mkkickstart*.rpm
```

安装 `mkkickstart` 软件包后，按照如下方式运行 `mkkickstart` 程序：

```bash
mkkickstart >ks.cfg
```

请注意 `mkkickstart` 程序的输出被重定向到了文件 `ks.cfg` 中。`mkkickstart` 程序可能会显示一条警告，提醒您在配置文件中设置静态 IP 地址；这是正常现象。

这是一个 `ks.cfg` 文件示例：

```text
lang us
#network --static --ip 10.0.0.2 --netmask 255.255.255.0
-->gateway 10.0.0.1 --nameserver 10.0.0.1
cdrom
device ethernet 3c90x
keyboard us
zerombr yes
clearpart --linux
part swap --size 526
part /space --size 10449
part /boot --size 40
part /usr --size 2001
part /home --size 4009
part /var --size 503
part / --size 1005
install
mouse genericps/2
timezone US/Pacific
xconfig --server "SVGA" --monitor "viewsonic17gs"
auth --useshadow --enablemd5
lilo --location mbr --linear
%packages
setup
filesystem
basesystem
...and so on...
%post
```

### 编辑配置文件

配置文件在可以使用之前需要进行一些修改。请注意 `network` 行被注释掉了。您应该删除注释字符 (#) 并修改 IP 地址、网络掩码和网关。如果您希望系统通过 BOOTP 或 DHCP 获取网络配置，请指定以下指令：

```
network --bootproto BOOTP
```

或

```
network --bootproto DHCP
```

表 8.4 描述了同一配置中显示的其它指令以及一些您可能会觉得有用的附加指令。请参阅文档 CD-ROM 上的 kickstart 文档，特别是 *The Official Red Hat Linux Reference Guide*，以详细了解这些及其他 kickstart 指令。

### 表 8.4 Kickstart 指令

| 指令 | 含义 |
|---|---|
| `auth --useshadow --enablemd5` | 指定使用 shadow 密码和 MD5 加密。 |
| `cdrom` | 指定安装介质位于本地 CD-ROM 上。 |
| `clearpart --all` | 指定应删除所有现有分区。 |
| `clearpart --linux` | 指定应删除所有现有 Linux 分区。 |
| `device ethernet device [--opts 'options']` | 指定系统具有指示类型的以太网适配器。当安装程序无法通过探测成功识别网络设备时，会参考此指令。 |
| `device scsi device [--opts 'options']` | 指定系统具有指示类型的 SCSI 适配器。当安装程序无法通过探测成功识别 SCSI 接口时，会参考此指令。 |
| `install` | 指定安装类型为“安装”而非“升级”。 |
| `keyboard us` | 指定键盘类型为 US。 |
| `lang us` | 指定安装程序在请求信息时所使用的对话框语言。 |
| `lilo --append "anything-needed"` | 指定要追加到 LILO 配置文件中的选项。 |
| `mouse genericps/2` | 指定鼠标类型为 ps/2。 |
| `network --bootproto bootp` | 指定通过 BOOTP 获取网络配置。 |
| `network --bootproto dhcp` | 指定通过 DHCP 获取网络配置。 |
| `network --static-ip ip --netmask mask --gateway gw --nameserver dns` | 指定静态网络配置。 |
| `part /mount --size size` | 指定应创建一个指定大小（以 MB 为单位）的 Linux 分区，并将其挂载到指示的目录。 |
| `part swap --size size` | 指定应创建一个指示大小（以 MB 为单位）的交换分区。 |
| `rootpw --iscrypted password` | 使用加密文本指定 root 密码。该指令历史上存在问题，最好避免使用。 |
| `%packages` | 指定接下来的行名为要安装的软件包。 |
| `%post` | 指定接下来的行是安装后要执行的 shell 命令。 |
| `timezone US/Pacific` | 指定时区为 US/Pacific。 |
| `upgrade` | 指定安装类型为“升级”而非“安装”。 |
| `xconfig --server "server" --monitor "monitor"` | 指定应使用指定的 X 服务器和显示器配置 XFree86。 |
| `zerombr yes` | 指定应移除任何现有的启动加载程序。 |

### 设置服务器

您可以使用 DHCP 服务器提供 kickstart 文件，而不是将其包含在启动介质中。为此，在 `/etc/dhcpd.conf` 文件中指定：

```
filename "/home/ftp/pub/ks.cfg";
```

如果您愿意，可以将 kickstart 文件存储在 `/home/ftp/pub` 以外的目录中；只需相应地修改 `filename` 指令即可。

如果您希望为每个客户端系统准备单独的 kickstart 文件，请指定该指令：

```
filename "/home/ftp/pub/kickstart";
```



然后，在 `/home/ftp/pub/kickstart` 目录中放置 kickstart 文件，这些文件的名称必须符合 `xxx.xxx.xxx.xxx-kickstart` 的格式，其中 `xxx.xxx.xxx.xxx` 是客户端系统的 IP 地址。

当安装程序通过 DHCP 获取 kickstart 文件时，它会假设应该从 NFS 服务器进行网络安装。默认情况下，它会尝试挂载由回答 DHCP 查询的同一主机导出的 NFS 目录。如果您想使用不同的主机来处理 NFS 请求，请在 `/etc/dhcpd.conf` 文件中包含以下指令：

```
next-server nfsserver;
```

其中 `nfsserver` 是存放 kickstart 文件的目标 NFS 服务器的主机名或 IP 地址。要指定安装介质的位置，您可以指定如下格式的 kickstart 指令：

```
nfs --server server directory
```

其中 `server` 指定 NFS 服务器，`directory` 指定 NFS 导出的目录。

> 有关设置 DHCP 服务器的更多信息，请参阅第 23 章“理解辅助网络服务”。

## 执行 Kickstart 安装

要开始 kickstart 安装，请在 LILO 提示符处指定 `ks` 参数。如果 kickstart 文件将从 DHCP 或 NFS 服务器获取，请使用命令：

```
linux ks
```

如果 kickstart 文件位于启动软盘的根目录中，请使用命令：

```
linux ks=floppy
```

如果 kickstart 安装需要某些在 kickstart 指令中找不到的信息，它将使用非 kickstart 安装时出现的对话框提示输入该信息。

现在，请尝试练习 8.7 来测试您对 kickstart 安装的理解。

### 练习 8.7：执行 Kickstart 安装

执行一次 kickstart 安装，在另一台计算机上复制一个现有的 Linux 系统。

## 本章小结

在本章中，您学习了如何在一些特殊情况下安装 Red Hat Linux。涵盖的最重要主题包括：

- **笔记本电脑**：在笔记本电脑上安装 Red Hat Linux 可能会出现特殊的兼容性问题。
- **多启动安装**：使用 LILO——或另一个提供类似功能的引导加载程序——您可以配置系统以启动多个操作系统。
- **特殊安装：PCMCIA 硬件**：您可以在从 PCMCIA 硬件启动的系统上安装 Red Hat Linux。
- **特殊安装：网络安装**：您可以从位于 FTP、HTTP 或 NFS 服务器上的介质安装 Red Hat Linux。
- **特殊安装：Kickstart 安装**：您可以使用 `mkkickstart` 程序安装 Red Hat Linux，该程序允许您将安装过程自动化。

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- boot arguments（启动参数）
- boot loader（引导加载程序）
- boot prompt（启动提示符）
- kickstart installation（kickstart 安装）
- multi-boot installation（多启动安装）
- network installation（网络安装）
- primary boot loader（主引导加载程序）
- secondary boot loader（次级引导加载程序）

## 更多信息来源

如果您想了解本章所述主题的更多信息，应参考以下来源：

- `/usr/doc/lilo-*` 中的 LILO 文档文件
- *The Official Red Hat Linux Installation Guide*（Red Hat Linux 官方安装指南）
- *The Official Red Hat Linux Reference Guide*（Red Hat Linux 官方参考指南）
- *The Red Hat Linux Kickstart HOWTO*（Red Hat Linux Kickstart HOWTO 指南）
- *The Win95 + WinNT + Linux Multiboot Using LILO Mini-HOWTO*（使用 LILO 实现 Win95 + WinNT + Linux 多启动 Mini-HOWTO）

## 复习题

1. 关于 Linux 笔记本电脑安装，以下哪些说法是正确的？
    - A. 配置声音很少有问题。
    - B. 配置视频很少有问题。
    - C. 同一型号的不同笔记本电脑可能需要不同的硬件配置。
    - D. 笔记本电脑安装通常比台式机安装更容易。

2. 关于 Linux 多启动安装，以下哪些说法是正确的？
    - A. Linux 可以与 Windows 95 和 Windows 98 共存。
    - B. Linux 可以与 Windows NT 共存。
    - C. 一次只能运行一个操作系统。
    - D. 您必须将 Linux 引导加载程序 LILO 安装在 MBR 上。

3. 关于 Linux 引导加载程序 LILO，以下哪些说法是正确的？
    - A. 当安装在分区的引导扇区时，LILO 作为次级引导加载程序运行。
    - B. 当安装在分区的引导扇区时，LILO 作为主引导加载程序运行。
    - C. 当安装在 MBR 时，LILO 作为次级引导加载程序运行。
    - D. 当安装在 MBR 时，LILO 作为主引导加载程序运行。

4. 非 Linux 分区的 LILO 配置必须包含什么？
    - A. `image` 选项
    - B. `label` 选项
    - C. `other` 选项
    - D. `root` 选项

5. LILO 提示符出现 `L` 表示什么？
    - A. LILO 的第一阶段已加载。
    - B. LILO 的第二阶段已加载。
    - C. LILO 的第二阶段已启动。
    - D. LILO 的第三阶段已加载。

6. 以下哪个是 Windows NT 引导加载程序的配置文件？
    - A. boot.ini
    - B. boot.nt
    - C. loader.ini
    - D. loader.boot

7. 您可以使用以下哪些服务执行网络安装？
    - A. FTP
    - B. HTTP
    - C. NFS
    - D. SMB

8. 要执行网络安装，服务器的 DNS 条目必须允许什么？
    - A. 将主机名映射到 IP 地址
    - B. 将主机 IP 地址映射到主机名
    - C. 将主机 IP 地址映射到 DHCP 服务器
    - D. 将主机名映射到 DHCP 服务器

9. 关于 `mkki` kickstart 程序，以下哪些说法是正确的？
    - A. 该程序生成一个包含运行该程序之系统 kickstart 指令的脚本。
    - B. 默认安装类不安装该程序。
    - C. 该程序将脚本写入其标准输出流。
    - D. 它生成的脚本应该进行编辑。

10. 您应该将 shell 命令放在哪里，以便在 kickstart 安装过程中自动执行 shell 命令？
    - A. 在 `%packages` 指令之后
    - B. 在 `%post` 指令之后
    - C. 作为 `shell` 指令的参数
    - D. 在 `ks.com` 文件中

11. 如果您未能在一个 kickstart 指令中指定信息会发生什么？
    - A. 安装程序将提示输入缺失的信息。
    - B. 安装程序异常终止。
    - C. 安装程序使用默认值。
    - D. 安装失败。

12. 在 LILO 提示符处应该输入什么，以开始一个从 DHCP 服务器获取 kickstart 文件的 kickstart 安装？
    - A. `linux ks`
    - B. `linux ks=dhcp`
    - C. `linux ks=floppy`
    - D. `linux ks=network`

## 复习题答案

1. C 笔记本电脑硬件各异；声音和视频硬件尤其容易出现问题。
2. A, B, C. Linux 基本上可以与任何 PC 操作系统共存，包括那些需要在 MBR 中拥有自己的引导加载程序的系统。
3. A, D. 主引导加载程序必须安装在 MBR 上。
4. C. 仅 `image` 选项是必需的，但通常也会指定 `label` 选项。
5. A. LILO 没有第三阶段。`l` 提示符表示在加载 LILO 第二阶段期间出现问题。
6. A. 其他文件不存在，或不被 Windows NT 使用。
7. A, B, C. 通过 SMB 进行的网络安装已不再支持。
8. A. 正向查询必须成功；反向查询已不再必要。不需要 DHCP 服务器。
9. A, B, C, D. 该程序通常在运行前必须安装。它向标准输出流发送一系列针对运行该程序的系统的指令。您应该编辑脚本以指定合适的网络配置。
10. B. 将命令放在 `%post` 指令之后。
11. A. 在准备脚本时，您不必指定您不知道的信息，因为安装程序会提示您输入缺失的信息。
12. A. 如果您指定了 `ks` 参数，安装程序将尝试通过 DHCP 获取 kickstart 文件。

# 第三部分：配置与管理



# 第 9 章：安装后配置安装时选项

### 本章涵盖的 RHCE 准备主题：

- 理解并实现安装时选项的安装后配置。
- 能够配置键盘。
- 能够配置鼠标。
- 能够设置系统时间。
- 能够配置声音。
- 能够配置运行级别（runlevel）。
- 能够配置身份验证。
- 能够配置基础网络。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_225_0.png)

Red Hat Linux 安装程序提供了一系列对话框，使配置许多设备和选项变得简单。然而，您可能不时地需要重新配置某个设备或选项。您可以重新安装 Red Hat Linux，但这没必要且既困难又耗时。相反，您可以使用相应的配置程序或工具，从而在不干扰其他系统配置的情况下重新配置该设备或选项。

本章介绍了在安装完成后可用于配置设备和选项的几个配置程序和工具。本章的重点是最基础的设备和选项；后续章节将介绍适用于更复杂需求的程序和工具。

## 配置键盘

要配置系统的键盘，请执行命令 `kbdconfig`。
随后将出现如图 9.1 所示的“配置键盘”屏幕。要指定键盘类型，请在列表中突出显示该键盘并点击 OK。

**图 9.1 配置键盘屏幕**
![](img/4eef9c6f2f52b608eba628cf4e2793ce_226_0.png)

> 注意：在使用文本模式程序时，您不能使用鼠标点击按钮。请使用导航键选择按钮，然后按 Enter 或空格键点击。

## 配置鼠标

要配置系统的鼠标，请执行命令 `mouseconfig`。该命令会启动如图 9.2 所示的“配置鼠标”屏幕。

**图 9.2 配置鼠标屏幕**
![](img/4eef9c6f2f52b608eba628cf4e2793ce_227_0.png)

要指定鼠标类型，请在列表中突出显示该鼠标。如果您不确定连接到系统的鼠标类型，请选择 Generic Mouse (serial) 或 Generic Mouse (PS/2)。如果鼠标有两个按钮，您通常应该启用 Emulate 3 Buttons 选项。点击 OK 以接受更改。

## 设置系统时区

要设置系统时区，请执行命令 `timeconfig`。
该命令会启动如图 9.3 所示的“配置时区”屏幕。如果硬件时钟设置为 UTC/GMT，请启用 Hardware Clock Set to GMT 选项。从列表中选择时区并点击 OK 以接受更改。

**图 9.3 配置时区屏幕**
![](img/4eef9c6f2f52b608eba628cf4e2793ce_228_0.png)

## 配置声音

要配置声音系统，请执行命令 `sndconfig`。

该命令会启动一个屏幕，说明该命令将探测即插即用（plug-and-play）声卡。点击 OK。如果探测到了声卡，程序将显示描述该声卡的信息。

否则，会出现一条消息告诉您没有找到声卡。点击 OK 关闭消息框。随后将出现如图 9.4 所示的“声卡类型”屏幕。从列表中选择正确的声卡类型，然后点击 OK。随后出现“声卡设置”屏幕，您可以指定该声卡使用的 I/O 端口、IRQ 和 DMA。指定正确的值，然后点击 OK。

您可能会收到通知，提示文件 `/etc/conf.modules` 将被覆盖；如果是这样，请点击 OK 以继续。

**图 9.4 声卡类型屏幕**
![](img/4eef9c6f2f52b608eba628cf4e2793ce_229_0.png)

最后，程序会播放一段样本声音。如果您能听到声音，就说明声卡已正确配置。如果声音配置程序确定您的声卡支持 MIDI（乐器数字接口），程序还会播放一段 MIDI 样本。

## 使用 linuxconf

Red Hat Linux 包含一个通用的系统管理工具 `linuxconf`，您可以将其用于执行多种任务。`linuxconf` 工具可以在虚拟控制台或 X 环境中运行。要启动 `linuxconf`，请执行命令：

```
linuxconf
```

随后将出现 `linuxconf` 屏幕。图 9.5 显示了 `linuxconf` 屏幕的图形版本。

**图 9.5 linuxconf 屏幕**
![](img/4eef9c6f2f52b608eba628cf4e2793ce_230_0.png)

`linuxconf` 屏幕的左侧包含一个充当菜单的树形控件。点击叶子项（分支末端的项）即可在屏幕右侧显示相应的对话框。文本模式屏幕的工作方式类似；但是，文本模式的分辨率低于图形模式，因此文本模式无法同时显示树形控件和对话框。在文本模式下，您必须退出对话框才能查看树形控件。

无论在文本模式还是图形模式下，您都可以通过点击相关的 + 图标来展开树的分支，或者通过点击相关的 – 图标来折叠树的分支。屏幕底部的按钮允许您退出程序、激活您指定的任何更改或访问帮助。

> **注意** `linuxconf` 的帮助功能尚未完全完成；某些主题缺少帮助条目。

`linuxconf` 一个较为混乱的地方在于，某些配置更改在您接受后会立即生效，而其他配置更改则仅在您显式激活后才会生效。本章中名为“激活更改”的小节解释了 `linuxconf` 这样设计的原因，并告诉您如何激活待处理的更改。通常，您应该在退出 `linuxconf` 之前激活待处理的更改。

以下小节描述了您可以使用 `linuxconf` 执行的一些常用操作。您可以执行比此处描述更多的操作；后续章节将介绍额外的 `linuxconf` 功能。

## 配置运行级别

要更改系统运行级别，请执行命令：

```
init n
```

其中 *n* 是所需的新运行级别。表 9.1 总结了 Red Hat Linux 使用的运行级别。

**表 9.1 Red Hat Linux 运行级别**

| 运行级别 | 定义 |
| :--- | :--- |
| 0 | 保留：设置此运行级别将停止系统。 |
| 1 | 保留：设置此运行级别将进入单用户模式。 |
| 2 | 无网络的多用户模式。 |
| 3 | 带网络的多用户模式。 |
| 4 | 未使用：基本上与运行级别 3 相同。 |
| 5 | 基于 X 的登录。 |
| 6 | 保留：设置此运行级别将重启系统。 |

您可以使用 `linuxconf` 来选择系统启动时采用的初始运行级别。为此，请选择 Config $\succ$ Miscellaneous Services $\succ$ Initial System Services。随后将出现“Init 默认运行级别”屏幕。图 9.6 显示了该屏幕的图形版本。点击与所需默认运行级别对应的单选按钮，然后点击 Accept。下次启动系统时，它应该会进入指定的运行级别。

**图 9.6 Init 默认运行级别屏幕**
![](img/4eef9c6f2f52b608eba628cf4e2793ce_232_0.png)

## 配置身份验证

Red Hat Linux 安装程序允许您配置多个身份验证选项。在安装过程中，您可以实现以下选项：

- 启用或禁用 shadow 密码
- 为 `root` 用户设置密码
- 启用或禁用 MD5 密码的创建

安装后，您仍然可以轻松地启用或禁用 shadow 密码，为 `root` 设置新密码，或启用或禁用 MD5 密码的创建。以下部分展示了如何实现这些操作。

### Shadow 密码

您可以在安装完成后将密码转换为 shadow 密码或从中转换回来。请记住，当启用 shadow 密码时，加密的密码存储在一个只有 `root` 才能读取的文件 (`/etc/shadow`) 中。`/etc/shadow` 文件除了加密密码外还包含几个字段，包括：

- 账户被禁用的日期，表示自 1970 年 1 月 1 日以来经过的天数
- 密码上次更改的日期，表示自 1970 年 1 月 1 日以来经过的天数
- 密码必须更改的天数
- 密码允许更改的最早天数
- 密码过期前警告用户的天数
- 密码过期后禁用账户的天数

启用 shadow 密码可以提高系统安全性。然而，如果启用了 shadow 密码，少数旧的 UNIX 程序可能无法正常运行。

要启用 shadow 密码，请执行命令：

```
pwconv
```

要禁用 shadow 密码，请执行命令：

```
pwunconv
```

### 更改 root 密码

您可以使用 `linuxconf` 轻松更改 `root` 密码。为此，请选择 Config $\Rightarrow$ Users Accounts $\Rightarrow$ Normal $\Rightarrow$ Change `root` Password。随后将出现“更改密码”屏幕。图 9.7 显示了该屏幕的图形版本。



**图 9.7** 更改密码界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_234_0.png)

您必须先输入当前的 root 密码并点击 Accept。如果您输入了正确的密码，程序将提示输入新密码。输入新密码并点击 Accept。程序会要求您再次输入新密码，以确认您的选择。执行此操作并点击 Accept 即可设置新密码。

> **注意** 如果您更倾向于使用命令行，可以通过执行 `passwd` 命令来更改 root 密码，该命令会提示您两次输入新密码。

## 配置 LILO

您可以直接使用 `linuxconf` 来配置 LILO，而无需编辑 `/etc/lilo.conf` 文件。要编辑 LILO 默认设置，请从 `linuxconf` 的菜单树中选择 Config $\succ$ Boot Mode $\succ$ LILO $\succ$ Configure LILO Defaults。随后将出现 LILO Defaults 界面；图 9.8 显示了该界面的图形版本。

**图 9.8** LILO Defaults 界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_235_0.png)

LILO Defaults 界面提供了与 LILO 全局选项相对应的配置选项，这些选项会影响每个启动镜像。例如，您可以使用此界面指定 LILO 的安装位置、启动延迟和提示超时时间。该界面不包含允许您指定默认启动镜像的控件。本小节后面介绍的另一个界面提供了该选项的访问权限。

### 配置 Linux 启动镜像

要添加、更改或删除 Linux 启动镜像，请从 `linuxconf` 的菜单树中选择 Config $\succ$ Boot Mode $\succ$ LILO $\succ$ Configure LILO Linux Configurations。随后将出现 LILO Linux Configurations 界面；图 9.9 显示了该界面的图形版本。

**图 9.9** LILO Linux Configurations 界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_235_1.png)

您可以通过点击 Add 来添加一个新的 Linux 启动镜像。要编辑或删除现有的 Linux 启动镜像，请选择该镜像并按 Enter。随后将出现 Linux Boot Configuration 界面。要删除启动镜像，请点击 Delete 按钮。要编辑启动镜像，请进行所需的更改并点击 Accept。该界面提供了前一章所述的 LILO 启动镜像选项以及几个较少使用的选项。

### 配置非 Linux 启动镜像

要添加、更改或删除非 Linux 分区，请从 `linuxconf` 的菜单树中选择 Config $\Rightarrow$ Boot Mode $\Rightarrow$ LILO $\Rightarrow$ Configure LILO Other OSs Configurations。随后将出现 LILO Other OS Configurations 界面；图 9.10 显示了该界面的图形版本。

**图 9.10** LILO Other OSs Configurations 界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_236_0.png)

您可以通过点击 Add 来添加一个新的非 Linux 启动镜像。要编辑或删除现有的非 Linux 启动镜像，请选择该镜像并按 Enter。随后将出现 Other Operating System Setup 界面。要删除启动镜像，请点击 Delete 按钮。要编辑启动镜像，请进行所需的更改并点击 Accept。Other Operating Systems Setup 界面提供了前一章所述的 `label` 和 `other` 选项。标记为 Partition to Boot 的文本字段对应于 `other` 选项。

### 配置默认启动镜像

要指定默认启动镜像，请从 `linuxconf` 的菜单树中选择 Config $\blacktriangleright$ Boot Mode $\blacktriangleright$ LILO $\blacktriangleright$ Change Default Boot Configuration。随后将出现 Default Boot Configuration 界面；图 9.11 显示了该界面的图形版本。

**图 9.11** Default Boot Configuration 界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_237_0.png)

要指定不同的默认启动镜像，请点击与所需默认启动镜像相对应的单选按钮，然后点击 Accept。

### 配置启动选项

您可以使用 `linuxconf` 来配置启动选项。为此，请从 `linuxconf` 的菜单树中选择 Config $\blacktriangleright$ Boot Mode $\blacktriangleright$ Mode $\blacktriangleright$ Default Boot Mode。随后将出现 Boot Mode Configuration 界面；图 9.12 显示了该界面的图形版本。

**图 9.12** Boot Mode Configuration 界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_238_0.png)

您可以使用此界面启用或禁用 LILO 的启动菜单，并指定启动延迟和提示超时时间。后两个选项在 LILO Defaults 界面中同样可用。您还可以使用 Boot Mode Configuration 界面来指定系统是以文本模式（运行级别 3）还是图形模式（运行级别 5）启动。

## 配置网络

您可以使用 `linuxconf` 来配置基础和高级网络选项。本小节将解释如何配置基础选项；随后的章节——特别是第 15 章“理解配置文件和脚本”——将解释如何配置高级选项。

### 配置主机名

要配置主机名，请从 `linuxconf` 的菜单树中选择 Config $\rightarrow$ Networking $\rightarrow$ Client Tasks $\rightarrow$ Basic Host Information。随后将出现 This Host Basic Configuration 界面；图 9.13 显示了该界面的图形版本。

**图 9.13** This Host Basic Configuration 界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_239_0.png)

图形化的 This Host Basic Configuration 界面包含几个选项卡，允许您在不同窗口之间进行选择。如果在图形界面中看不到 Host Name 界面，请点击 Host Name 选项卡。要指定主机名，请将其输入文本框中并点击 Accept。

### 配置网络适配器

要配置网络适配器，请从 `linuxconf` 的菜单树中选择 Config $\rhd$ Networking $\rhd$ Client Tasks $\rhd$ Basic Host Information。随后将出现 This Host Basic Configuration 界面。该图形界面包含几个选项卡，允许您在不同窗口之间进行选择。如果在图形界面中看不到 Adapter 1 界面，请点击 Adapter 1 选项卡。随后将出现 Adapter 1 界面；图 9.14 显示了该界面的图形版本。

如果您使用的是 `linuxconf` 的文本版本，只需滚动查看 This Host Basic Configuration 界面中关于 Adapter 1 的部分。`linuxconf` 程序最多可提供 5 个网络适配器的配置选项。

**图 9.14** Adapter 1 界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_240_0.png)

通过 Adapter 1 界面或其他适配器界面，您可以启用或禁用适配器，并指定其配置是静态的，还是通过 DHCP 或 BOOTP 获取。如果配置是静态的，您可以使用标记为 Primary Name + Domain 的文本框指定一个完全限定域名 (FQDN)。您还可以指定 IP 地址、网络掩码以及包括设备选项在内的其他几个选项。点击 Accept 以保存您的更改。

### 配置名称服务器

要配置名称服务器，请从 `linuxconf` 的菜单树中选择 Config $\succ$ Networking $\succ$ Client Tasks $\succ$ Name Server Specification。随后将出现 Resolver Configuration 界面；图 9.15 显示了该界面的图形版本。

**图 9.15** Resolver Configuration 界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_240_1.png)

如果正常运行不需要 DNS，请禁用 DNS Is Required for Normal Operation。否则，请指定默认域名以及与系统关联的主名称服务器的 IP 地址（数字）。您最多可以指定两个额外的名称服务器和六个额外的搜索域。点击 Accept 以保存您的更改。

### 配置默认网关

要配置默认网关，请从 `linuxconf` 的菜单树中选择 Config $\succ$ Networking $\succ$ Client Tasks $\succ$ Routing and Gateways $\succ$ Set Defaults。随后将出现 Defaults 界面；图 9.16 显示了该界面的图形版本。

**图 9.16** Defaults 界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_241_0.png)

指定默认网关的 IP 地址。如果您希望该系统充当路由器，请开启 Enable Routing。有关配置路由的更多信息，请参阅第 29 章“配置 Linux 路由器”。

### 激活更改

如前所述，当您使用 `linuxconf` 更改配置选项时，更改可能会立即生效，也可能会处于待定状态直到更改被激活。虽然配置文件会立即更新，但大多数系统服务在服务被...

重启。当你指示 `linuxconf` 激活待处理的更改时，它会重启那些你更改了配置的服务。

要激活待处理的更改，请点击 Act/Changes。随后将出现“系统状态（Status of the System）”屏幕；图 9.17 展示了该屏幕的图形化版本。

**图 9.17** 系统状态屏幕

![](img/4eef9c6f2f52b608eba628cf4e2793ce_242_0.png)

如果你想知道有哪些待处理的更改，请点击 Preview What Has to Be Done。`linuxconf` 程序将显示待处理的更改。要激活这些更改，请点击 Activate the Changes。若要在不激活任何待处理更改的情况下退出系统状态屏幕，请点击 Quit。

通常你应该在退出 `linuxconf` 之前激活待处理的更改。如果你忽略了这一步，`linuxconf` 将提示你确认是否要在不激活指定更改的情况下退出。

## 总结

在本章中，你学习了在安装完成后配置安装时选项的方法。涵盖的最重要主题包括：

- **键盘** 安装后，你可以使用 `kbdconfig` 程序来配置键盘。
- **鼠标** 安装后，你可以使用 `mouseconfig` 程序来配置鼠标。
- **时区** 安装后，你可以使用 `timeconfig` 程序来配置时区。
- **声音** 安装后，你可以使用 `sndconfig 程序来配置声音。
- **默认运行级别** 安装后，你可以使用 `linuxconf` 程序来配置默认运行级别。
- **认证** 安装后，你可以使用 `pwconv` 或 `pwunconv` 程序来配置 shadow 密码，或者使用 `linuxconf` 程序更改 `root` 密码。
- **LILO 选项** 安装后，你可以使用 `linuxconf` 程序来配置 LILO 选项。
- **网络** 安装后，你可以使用 `linuxconf` 程序来配置网络。

### 关键术语

在进入下一章之前，请确保你熟悉以下术语：

Runlevel（运行级别）

## 补充信息源

如果你想了解本章所呈现主题的进一步信息，你应该参考以下来源：

- *Official Red Hat Linux Reference Guide*（红帽 Linux 官方参考指南）
- 本章中描述的程序和工具的 man 手册页

## 复习题

请注意，你可能会觉得其中几个问题非常简单，因为它们纯粹是回忆类问题。但是，这类问题有时会出现在笔试中。在键盘前回答它们很简单，但在闭卷考试中可能会很麻烦。我为了考试死记硬背了它们，现在我发现自己得回头检查答案！即使在键盘前，你也可能浪费宝贵的几分钟来寻找一个重要实用程序的名称，因此最好记住所有在基于性能的考试中可能用到的程序名称。这样，你就可以将精力集中在更重要的问题上。

1. 以下哪个程序用于配置键盘？
   A. kbconfig
   B. kbdconfig
   C. keyconfig
   D. keyboardconfig

2. 以下哪个程序用于配置鼠标？
   A. mousecfg
   B. mouseconfig
   C. mseconfig
   D. mousetest

3. 以下哪个程序用于配置声音？
   A. soundcfg
   B. sndconfig
   C. soundcfg
   D. soundconfig

4. 哪个运行级别导致系统启动时出现基于 X 的登录界面？
   A. 2
   B. 3
   C. 4
   D. 5

5. 关于 `linuxconf`，以下哪项是正确的？
   A. 可以通过执行 `linuxconf` 命令启动。
   B. 它在图形模式下运行。
   C. 它在文本模式下运行。
   D. 必须有鼠标才能操作它。

6. 使用 `linuxconf` 时，什么时候必须显式激活待处理的更改？
   A. 如果另一个用户正在运行 `linuxconf`
   B. 如果必须重启一个或多个系统服务才能使更改生效
   C. 如果更改影响用户账户
   D. 如果更改较为复杂

## 复习题答案

1. B. `kbdconfig` 程序用于配置键盘。
2. B. `mouseconfig` 程序用于配置鼠标。
3. B. `sndconfig` 程序用于配置声音系统。
4. D. 运行级别 2 是没有网络的单用户模式。运行级别 3 是带网络的单用户模式。运行级别 4 基本上与运行级别 3 相同。
5. A, B 和 C。`linuxconf` 程序在文本模式和图形模式下均可运行；它不需要鼠标。
6. B. `linuxconf` 程序不会自动重启你更改了配置的服务，直到你指示它这样做。

# 第 10 章：管理用户账户和组

**本章涵盖的 RHCE 准备主题：**

- 理解并掌握如何创建不同类型的用户账户。
- 理解并掌握如何配置用户环境。
- 熟悉系统和用户的 bash 配置文件。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_248_0.png)

Linux 系统管理员的主要任务之一就是创建和配置用户账户。Red Hat Linux 提供了几种类型的用户账户，因此 Red Hat Linux 系统管理员必须知道如何为特定用户选择合适的账户类型，并知道如何创建和配置该账户。与用户账户相关的是组（groups），组定义了一组用户，你可以向其扩展特权和权限。本章将解释 Red Hat Linux 提供的用户账户类型以及创建和配置用户账户与组的步骤。

## 用户账户

`/etc/passwd` 文件定义了 Linux 用户账户。文件中的每一行描述一个用户。这是一个典型的 `/etc/passwd` 文件：

```text
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:
daemon:x:2:2:daemon:/sbin:
adm:x:3:4:adm:/var/adm:
lp:x:4:7:lp:/var/spool/lpd:
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:
news:x:9:13:news:/var/spool/news:
uucp:x:10:14:uucp:/var/spool/uucp:
operator:x:11:0:operator:/root:
games:x:12:100:games:/usr/games:
gopher:x:13:30:gopher:/usr/lib/gopher-data:
ftp:x:14:50:FTP User:/home/ftp:
nobody:x:99:99:Nobody:/:
xfs:x:100:233:X Font Server:/etc/X11/fs:/bin/false
bill:x:500:500:Bill McCarty:/home/bill:/bin/bash
```

每行包含几个字段，由冒号分隔。以下是这些字段的列表及详细说明。

- **用户名** 与用户账户关联的登录名称。
- **密码** 与用户账户关联的登录密码（如果启用了 shadow 密码，则仅出现占位符 x）。
- **用户 ID** 与用户账户关联的唯一数字 ID。
- **组 ID** 与用户的主组关联的数字 ID。Red Hat Linux 为每个用户账户定义了一个个人组。
- **全名** 用户的全名。
- **主目录** 设置为登录时当前目录的目录。
- **Shell** 用户通过命令行界面登录时加载的命令解释器；用户通过 X 登录时不会加载 shell。

由于 `/etc/passwd` 的所有行都具有相同的结构，你可以说 Linux 仅提供了一种用户账户。然而，Red Hat Linux 认可以下几种类型的用户账户：

- 普通用户账户，也称为 shell 账户
- PPP 账户，用于通过 PPP 登录的用户
- SLIP 账户，用于通过 SLIP 登录的用户
- UUCP 账户，用于通过 UUCP 登录的用户
- POP 账户，用于通过 POP 访问邮件但不实际登录的用户
- 虚拟 POP 账户，用于在提供虚拟电子邮件域的服务器上通过 POP 访问邮件的用户

管理用户账户涉及创建、配置和删除用户账户。你可以使用 `user-conf` 工具或命令行来管理用户账户。



下一节将解释如何通过 `userconf` 工具管理用户账户。随后的章节将解释如何通过命令行管理用户账户。

### 通过 `userconf` 工具管理用户账户

管理用户账户最简单的方法是通过 `userconf` 工具，因为它会自动执行若干原本繁琐的操作。您可以通过执行以下命令启动 `userconf` 工具：

```
userconf
```

图 10.1 显示了在控制台中运行的 `userconf` 菜单。如果您愿意，也可以在 X 环境下运行 `userconf`，在这种情况下，菜单的外观会有所不同。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_250_0.png)

`linuxconf` 配置程序提供了另一种访问 `userconf` 的方式。要通过 `linuxconf` 访问 `userconf`，请执行命令：

```
linuxconf
```

然后，在 `linuxconf` 菜单中选择 Config $\succ$ Users Accounts，导航到用户账户菜单。图 10.2 显示了 `linuxconf` 的用户账户（Users Accounts）菜单。

> **注意** 本章中的说明假设您使用的是 userconf；不过，您也可以轻松地使用 linuxconf 来执行所述的任何操作。

**图 10.2** Linuxconf 用户账户菜单

![](img/4eef9c6f2f52b608eba628cf4e2793ce_251_0.png)

要管理特定类型的用户账户，请突出显示您想要管理的类型并按 Enter 键。但是，如果您使用的是 X 环境，只需点击您感兴趣的账户类型即可。接下来的几个小节将解释如何管理各种类型的账户。

#### 创建普通用户账户

普通用户账户（通常称为 shell 账户）允许用户登录并使用系统。要创建普通用户账户，请按照以下步骤操作：

- 1. 启动 `userconf`。
- 2. 选择 Users Accounts 并按 Enter 键。如果您使用的是 X 环境，请点击 Users Accounts。随后将出现如图 10.3 所示的用户账户屏幕。如果您使用的是 X 环境，此屏幕及随后的屏幕外观将有所不同。

根据过滤器设置（在 Control $\succ$ Features 中），您可能会看到一个过滤器（Filter）对话框。使用该对话框将显示的用户限制为您想要查看的用户，或者点击 Accept 查看所有账户。

**图 10.3** 用户账户屏幕

![](img/4eef9c6f2f52b608eba628cf4e2793ce_252_0.png)

- 3. 点击 Add 按钮。随后将出现如图 10.4 所示的用户账户创建屏幕。
- 4. 填写参数字段。除非您使用的是非常大的窗口，否则某些字段可能不可见；只需滚动屏幕即可查看。有关每个字段的信息，请参考表 10.1 和 10.2。权限字段可以具有以下三个值之一：
    - Denied，表示用户缺乏该权限
    - Granted，表示用户拥有该权限，但必须通过输入登录密码来确认授权
    - Granted/silent，表示用户拥有该权限，且无需通过输入密码来确认授权

**图 10.4** 用户账户创建屏幕

![](img/4eef9c6f2f52b608eba628cf4e2793ce_252_1.png)

**表 10.1 用户账户参数**

| 参数 | 描述 |
|---|---|
| The account is enabled | 如果勾选，用户可以登录。 |
| Login name | 用户账户的登录名。登录名不应包含除连字符 (-) 或下划线 (_) 以外的特殊字符。登录名长度最多可达 256 个字符；不过，大多数系统管理员分配的登录名长度不超过 8-10 个字符。 |
| Full name | 用户的全名（可选）。 |
| Group | 用户主组的数字 ID（可选）。默认情况下，会创建一个与登录名同名的个人组。 |
| Supplementary groups | 用户所属的其他附加组（可选）。默认情况下，不分配附加组。 |
| Home directory | 用户的主目录（可选）。默认分配目录 `/home/login_name`，其中 `login_name` 是用户的登录名。 |
| Command interpreter | 命令解释器（shell），默认为 `/bin/bash`（可选）。 |
| User ID | 数字用户 ID（可选）。默认情况下，分配下一个顺序数字 ID。 |
| Must keep # days | 用户必须保持密码不变的天数，如果密码可以立即更改，则为 -1。 |
| Must change after # days | 用户必须更改密码的天数，如果密码永不过期，则为 99999。 |
| Warn # days before expiration | 密码过期前给出的警告天数，如果不给警告，则为 -1。 |
| Account expire after # days | 账户过期前的天数，如果账户永不过期，则为 -1。 |
| Expiration date | 账户的过期日期，如果指定了“账户在 # 天后过期”参数，则为空。 |
| Redirect messages to | 此账户的电子邮件转发至的用户账户（可选）。 |
| Email alias | 应定向到此账户的电子邮件地址（登录名除外）（可选）。 |

**表 10.2 用户权限参数**

| 权限 | 描述 |
| :--- | :--- |
| May use linuxconf | 用户可以访问任何 linuxconf 屏幕。但是，除非用户被明确授予激活配置更改的权限，否则用户不能执行此操作。 |
| May activate config changes | 用户可以激活 linuxconf 配置更改。 |
| May shutdown | 用户可以关闭系统。即使没有此权限，用户也可以通过在控制台按下 Ctrl+Alt+Del 来关闭系统。 |
| May switch network mode | 用户可以更改系统运行级别。 |
| May view system logs | 用户可以查看系统日志。 |
| SuperUser equivalence | 用户可以执行特权命令。 |
| Apache administration | 用户可以配置 Apache Web 服务器。 |
| Mail to Fax manager | 用户可以配置邮件转传传真服务。 |
| Samba administration | 用户可以配置 Samba。 |
| Message of the day | 用户可以修改当日消息（MOTD）。 |
| POP accounts manager | 用户可以管理 POP 账户。 |
| PPP accounts manager | 用户可以管理 PPP 账户。 |
| UUCP manager | 用户可以管理 UUCP 账户。 |

- 5. 点击 Accept 按钮。随后将出现如图 10.5 所示的更改密码对话框。

**图 10.5** 更改密码屏幕

![](img/4eef9c6f2f52b608eba628cf4e2793ce_255_0.png)

- 6. 输入所需的密码，然后点击 Accept 按钮。更改密码对话框将再次出现。
- 7. 通过重新输入来确认您之前输入的密码。点击 Accept 按钮。用户账户屏幕将再次出现。
- 8. 完成用户账户管理后，点击 Quit 按钮。

既然您已经了解了如何使用 `userconf` 创建普通用户账户，现在应该完成练习 10.1。

#### 练习 10.1：创建普通用户账户

系统管理员经常需要创建新用户账户。本练习旨在测试您完成此操作的能力。如有必要，请回顾使用 userconf 的逐步操作步骤。但请记住，RHCE 考试是闭卷的，因此在 RHCE 考试期间被要求执行此操作时，您将无法查阅参考资料。

- 1. 使用 `userconf` 创建一个登录名为 test101 的普通用户账户。
- 2. 验证您可以通过控制台以 test101 身份登录。

#### 修改普通用户账户

要修改普通用户账户，请按照以下步骤操作：

- 1. 启动 `userconf`。
- 2. 选择 User Accounts 并按 Enter 键；或者，如果您使用的是 X 环境，请点击 User Accounts。用户账户屏幕将再次出现。
- 3. 突出显示您要修改的账户并按 Enter 键；或者，如果您使用的是 X 环境，只需点击该账户即可。
- 4. 根据需要修改字段。
- 5. 点击 Accept 按钮。

根据过滤器设置（在 Control $\succ$ Features 中），您可能会看到一个过滤器（Filter）对话框。使用该对话框将用户账户限制为您想要查看的账户，或者点击 Accept 查看所有账户。



既然您已经了解了如何修改普通用户账户，请完成练习 10.2，以便确保您能够独立执行此操作。

#### 练习 10.2：修改普通用户账户

RHCE 考试很可能会要求您修改用户账户。本练习旨在测试您在此方面的能力。如果需要，请回顾分步操作步骤。但在继续之前，请确保您能够在不参考本书的情况下修改普通用户账户：因为在 RHCE 考试期间，您将无法使用本书。

- 1. 使用 `userconf` 将用户 test101 的全名修改为“Test User”。
- 2. 通过以 test101 身份登录并执行 `finger` 命令来验证您的更改是否正确。

## 创建和修改 PPP 用户账户

PPP 用户账户由从远程位置通过 PPP 登录的用户使用。PPP 用户账户的默认命令解释器是 `/usr/lib/linuxconf/lib/ppplogin`。默认情况下，PPP 用户是 `pppusers` 组的成员。要创建 PPP 用户账户，请遵循以下步骤：

- 1. 启动 `userconf`。
- 2. 选择 PPP Accounts 并按 Enter；或者，如果您使用的是 X 窗口系统，请点击 PPP Accounts 并点击 Special Accounts 选项卡。随后会出现 User Accounts 屏幕。
  根据筛选设置（在 Control $\triangleright$ Features 中），您可能会看到一个 Filter 对话框。使用该对话框将用户账户限制为您想要查看的账户，或按 Accept 查看所有账户。
- 3. 点击 Add 按钮。随后会出现如图 10.6 所示的 User Account Creation 屏幕。

### 图 10.6 User Account Creation 屏幕
![](img/4eef9c6f2f52b608eba628cf4e2793ce_258_0.png)

- 4. 填写参数字段。有关每个字段的信息，请参考表 10.1 和 10.2。
- 5. 点击 Accept 按钮。随后会出现 Changing Password 对话框。
- 6. 输入所需的密码，然后点击 Accept 按钮。Changing Password 对话框将再次出现。
- 7. 通过重新输入来确认之前输入的密码。点击 Accept 按钮。Users Accounts 屏幕将再次出现。
- 8. 完成 PPP 用户账户的管理后，点击 Quit 按钮。

要修改 PPP 用户账户，请遵循以下步骤：

- 1. 启动 `userconf`。
- 2. 选择 PPP Accounts 并按 Enter；或者，如果您使用的是 X 窗口系统，请点击 PPP Accounts。随后会出现 Users Accounts 屏幕。
  根据筛选设置（在 Control $\triangleright$ Features 中），您可能会看到一个 Filter 对话框。使用该对话框将用户账户限制为您想要查看的账户，或按 Accept 查看所有账户。
- 3. 突出显示要修改的账户并按 Enter；或者，如果您使用的是 X 窗口系统，只需点击该账户即可。
- 4. 根据需要修改字段。
- 5. 点击 Accept 按钮。

## 创建和修改 SLIP 用户账户

SLIP 用户账户由从远程位置通过 SLIP 登录的用户使用。SLIP 用户账户的默认命令解释器是 `/sbin/diplogin`。默认情况下，SLIP 用户是 `slipusers` 组的成员。要创建 SLIP 用户账户，请遵循以下步骤：

- 1. 启动 `userconf`。
- 2. 选择 SLIP Accounts 并按 Enter；或者，如果您使用的是 X 窗口系统，请点击 SLIP Accounts。随后会出现 Users Accounts 屏幕。
  根据筛选设置（在 Control $\triangleright$ Features 中），您可能会看到一个 Filter 对话框。使用该对话框将用户账户限制为您想要查看的账户，或按 Accept 查看所有账户。
- 3. 点击 Add 按钮。随后会出现 User Account Creation 屏幕。
- 4. 填写参数字段。有关每个字段的信息，请参考表 10.1 和 10.2。
- 5. 点击 Accept 按钮。随后会出现 Changing Password 对话框。
- 6. 输入所需的密码，然后点击 Accept 按钮。Changing Password 对话框将再次出现。
- 7. 通过重新输入来确认之前输入的密码。点击 Accept 按钮。Users Accounts 屏幕将出现。
- 8. 完成 SLIP 用户账户的管理后，点击 Quit 按钮。

要修改 SLIP 用户账户，请遵循以下步骤：

- 1. 启动 `userconf`。
- 2. 选择 SLIP Accounts 并按 Enter；或者，如果您使用的是 X 窗口系统，请点击 SLIP Accounts。随后会出现 Users Accounts 屏幕。
  根据筛选设置（在 Control $\triangleright$ Features 中），您可能会看到一个 Filter 对话框。使用该对话框将用户账户限制为您想要查看的账户，或按 Accept 查看所有账户。
- 3. 突出显示要修改的账户并按 Enter；或者，如果您使用的是 X 窗口系统，只需点击该账户即可。
- 4. 根据需要修改字段。
- 5. 点击 Accept 按钮。

## 创建和修改 UUCP 用户账户

在互联网出现之前，UUCP 是 Unix 计算机之间通信的主要方式；如今仍有少数 Linux 站点使用 UUCP。UUCP 用户账户由从远程位置通过 UUCP 登录的进程使用。UUCP 用户账户的默认命令解释器是 `/usr/sbin/uucico`。默认情况下，UUCP 用户是 `uucp` 组的成员。UUCP 用户的默认主目录是 `/var/spool/uucppublic`。

要创建 UUCP 用户账户，请执行以下操作：

- 1. 启动 `userconf`。
- 2. 选择 UUCP Accounts 并按 Enter；或者，如果您使用的是 X 窗口系统，请点击 UUCP Accounts。
- 3. 随后会出现 Users Accounts 屏幕。
  根据筛选设置（在 Control $\triangleright$ Features 中），您可能会看到一个 Filter 对话框。使用该对话框将用户账户限制为您想要查看的账户，或按 Accept 查看所有账户。
- 4. 点击 Add 按钮。随后会出现 User Account Creation 屏幕。
- 5. 填写参数字段。有关每个字段的信息，请参考表 10.1 和 10.2。
- 6. 点击 Accept 按钮。随后会出现 Changing Password 对话框。
- 7. 输入所需的密码，然后点击 Accept 按钮。Changing Password 对话框将再次出现。
- 8. 通过重新输入来确认之前输入的密码。点击 Accept 按钮。Users Accounts 屏幕将再次出现。
- 9. 完成 UUCP 用户账户的管理后，点击 Quit 按钮。

要修改 UUCP 用户账户，请执行以下操作：

- 1. 启动 `userconf`。
- 2. 选择 UUCP Accounts 并按 Enter；或者，如果您使用的是 X 窗口系统，请点击 UUCP Accounts。随后会出现 Users Accounts 屏幕。
  根据筛选设置（在 Control $\triangleright$ Features 中），您可能会看到一个 Filter 对话框。使用该对话框将用户账户限制为您想要查看的账户，或按 Accept 查看所有账户。
- 3. 突出显示要修改的账户并按 Enter；或者，如果您使用的是 X 窗口系统，只需点击该账户即可。
- 4. 根据需要修改字段。
- 5. 点击 Accept 按钮。

## 创建和修改 POP 用户账户

POP 用户账户由从远程位置通过 POP 访问邮件的用户使用。POP 用户实际上并不登录系统，因此 POP User Accounts Creation 屏幕不包含 Command Interpreter（命令解释器）字段。默认情况下，POP 用户是 `popusers` 组的成员。

要创建 POP 用户账户，请执行以下操作：

- 1. 启动 `userconf`。
- 2. 选择 POP Accounts 并按 Enter；或者，如果您使用的是 X 窗口系统，请点击 POP Accounts。随后会出现 Users Accounts 屏幕。
  根据筛选设置（在 Control $\triangleright$ Features 中），您可能会看到一个 Filter 对话框。使用该对话框将用户账户限制为您想要查看的账户，或按 Accept 查看所有账户。
- 3. 点击 Add 按钮。随后会出现 User Account Creation 屏幕。
- 4. 填写参数字段。有关每个字段的信息，请参考表 10.1 和 10.2。
- 5. 点击 Accept 按钮。随后会出现 Changing Password 对话框。
- 6. 输入所需的密码，然后点击 Accept 按钮。Changing Password 对话框将再次出现。
- 7. 通过重新输入来确认之前输入的密码。点击 Accept 按钮。Users Accounts 屏幕将再次出现。
- 8. 完成 POP 用户账户的管理后，点击 Quit 按钮。

要修改 POP 用户账户，请遵循以下步骤：

- 1. 启动 `userconf`。
- 2. 选择 POP Accounts 并按 Enter；或者，如果您使用的是 X 窗口系统，请点击 POP Accounts。随后会出现 Users Accounts 屏幕。
  根据筛选设置（在 Control $\triangleright$ Features 中），您可能会看到一个 Filter 对话框。使用该对话框将用户账户限制为您想要查看的账户，或按 Accept 查看所有账户。



- 3. 突出显示您想要修改的账户并按 Enter；或者，如果您使用的是 X，可以直接点击该账户。
- 4. 根据需要修改字段。
- 5. 点击 Accept 按钮。

## 启用和禁用用户账户

如果您想锁定某个用户，可以禁用该用户的账户。如果用户账户被禁用，该用户将无法登录或访问 POP 服务器。要禁用用户账户，请执行以下步骤：

- 1. 启动 userconf。
- 2. 选择 User Accounts 并按 Enter；或者，如果您使用的是 X，点击 User Accounts。随后将出现 Users Accounts 界面。
- 3. 选择您想要禁用的用户账户并按 Enter；或者，如果您使用的是 X，可以直接点击该用户账户。随后将出现用户信息界面。
- 4. 取消勾选标有 The Account Is Enabled 的复选框。点击 Accept 按钮。

要启用已禁用的用户账户，请遵循类似的步骤：

- 1. 启动 userconf。
- 2. 选择 User Accounts 并按 Enter；或者，如果您使用的是 X，点击 User Accounts。随后将出现 Users Accounts 界面。
- 3. 选择您想要启用的用户账户并按 Enter；或者，如果您使用的是 X，可以直接点击该用户账户。随后将出现 User Information 界面。
- 4. 勾选标有 The Account Is Enabled 的复选框。点击 Accept 按钮。

## 删除用户账户

如果某个用户账户不再需要，最好将其删除而不仅仅是禁用。通过删除账户，您可以释放用户主目录及其内容所占用的磁盘空间。

要删除用户账户，请执行以下步骤：

- 1. 启动 userconf。
- 2. 选择 User Accounts 并按 Enter；或者，如果您使用的是 X，点击 User Accounts。随后将出现 Users Accounts 界面。
- 3. 选择您想要删除的用户账户并按 Enter；或者，如果您使用的是 X，可以直接点击该用户账户。随后将出现 User Information 界面。
- 4. 要删除账户，请点击 Del 按钮。随后将出现如图 10.7 所示的 Deleting Account 界面。

**图 10.7** Deleting Account 界面

![](img/4eef9c6f2f52b608eba628cf4e2793ce_263_0.png)

- 5. 选择以下所需选项之一：
    - Archive the Account's Data（存档账户数据）
    - Delete the Account's Data（删除账户数据）
    - Leave the Account's Data in Place（保留账户数据原处）

默认选项 Archive the Account's Data 会将用户从 `/etc/passwd` 中删除，并在 `/home/oldaccounts` 目录下创建一个 gzip 压缩存档（如果该目录不存在则会自动创建）。该文件的命名格式为：

`user-yyyy-mm-dd-xxx.tar.gz`

其中 *user* 是用户 ID，*yyyy-mm-dd* 是当前日期，*xxx* 是执行删除操作的进程 ID。Delete the Account's Data 选项则会删除用户的主目录及其内容。

- 6. 点击 Accept 按钮。

在学习完删除用户账户的步骤后，请完成练习 10.3，该练习将测试您执行此操作的能力。

用户可能在用户主目录以外的目录中拥有文件。如果您删除了用户账户，这些文件仍然存在。此类文件被称为孤儿文件（orphan files），它们由已删除用户账户的用户 ID 拥有。如果您创建了一个具有该删除账户用户 ID 的新账户，那么新用户账户将成为这些孤儿文件的所有者。

### 练习 10.3：删除用户账户

当用户账户不再使用时，应及时将其删除，以免被企图破坏系统安全的人员（cracker）利用。本练习测试您删除用户账户的能力。如有必要，您可以回顾操作步骤，但请记住，在 RHCE 考试期间您将没有机会这样做。

- 1. 使用 userconf 创建一个登录名为 test101 的普通用户账户。
- 2. 删除您创建的用户账户。
- 3. 检查 `/etc/passwd` 以验证账户已被删除。

## 通过命令行管理用户账户

一些管理员更喜欢使用命令行来管理用户账户。掌握相关命令非常有帮助，因为您可以使用它们构建脚本，从而简化常见的系统管理任务。管理用户最重要的命令如下：

- `useradd`：创建用户账户
- `userdel`：删除用户账户
- `usermod`：修改用户账户
- `chfn`：更改与用户账户关联的全名（full name）字段

全名字段包含所谓的 gecos 信息，包括姓名、办公室位置、电话号码等。

- `chsh`：更改与用户账户关联的命令解释器（shell）

在本章稍后部分，您将学习其他有助于管理用户账户相关密码的命令。

### useradd 命令

`useradd` 命令（与 `adduser` 命令为同一个程序）用于创建新用户账户。该命令的基本形式为：

`useradd -d home -e expire -f inactive -g group -G groups -m -s shell -u uid username`

仅最后一个参数（username，指定登录名）是必需的。其余参数的含义如下：

- `-d home` 指定用户的主目录。
- `-e expire` 指定账户的过期日期。格式为 mm/dd/yy。
- `-f inactive` 指定密码过期后账户被禁用的天数。默认值为 -1，防止账户被禁用。
- `-g group` 指定用户的主组名称或编号。默认值为 100。与 -n 标志配合使用。
- `-G groups` 以逗号分隔的组名或编号列表，指定用户将加入的附加组。
- `-m` 指定自动创建用户的主目录。
- `-n` 指定不创建私有用户组。
- `-s shell` 指定用户的 shell。如果未指定，系统将在用户登录时启动默认 shell。
- `-u uid` 用户的数值 ID。如果未指定，系统将选择下一个可用的用户 ID。

有关 `useradd` 命令的更多信息，请参阅其 man 手册页。

> 当您创建用户账户时，账户最初没有密码。您应该使用本章后面介绍的 `passwd` 命令为用户账户关联密码。

### userdel 命令

`userdel` 命令用于删除用户账户。该命令的形式为：

`userdel user`

其中 `user` 是要删除用户的登录名。如果您想删除用户的主目录及其内容，请执行以下形式的命令：

`userdel -r user`

有关 `userdel` 命令的更多信息，请参阅其 man 手册页。

> 用户可能在用户主目录以外的目录中拥有文件。如果您删除了用户账户，这些文件仍然存在。此类文件被称为孤儿文件（orphan files），它们由已删除用户账户的用户 ID 拥有。如果您创建了一个具有该删除账户用户 ID 的新账户，那么新用户账户将成为这些孤儿文件的所有者。

### usermod 命令

`usermod` 命令允许您修改现有的用户账户。其形式与 `useradd` 命令类似：

`usermod -d home -e expire -f inactive -g group -G groups -l login -s shell -u uid username`

除最后一个参数外，所有参数都是可选的；但必须至少指定一个附加参数。参数 `-l login` 允许您更改与账户关联的登录名。用户主目录的名称不受此更改的影响。

有关 `usermod` 命令的更多信息，请参阅其 man 手册页。

### chfn 命令

`chfn` 命令允许您更改与用户账户关联的全名。该命令的形式为：

```bash
chfn user
```

其中 `user` 是要修改账户的登录名。该命令将提示输入以下信息（即 gecos 信息）：

- Name（姓名）
- Office（办公室）
- Office phone（办公室电话）
- Home phone（家庭电话）

如果您不想为提示的字段指定值，只需按 Enter 即可。您也可以在非交互模式下使用 `chfn` 命令。有关此项及其他信息的详细内容，请参阅其 man 手册页。

### chsh 命令

`chsh` 命令允许您更改与用户账户关联的命令解释器。该命令的形式为：

```bash
chsh -s shell user
```

其中 `shell` 指定所需的命令解释器路径，`user` 指定要修改的用户账户登录名。只能指定 `/etc/shells` 中列出的经批准的命令解释器。

有关 `chsh` 命令的更多信息，请参阅其 man 手册页。

现在您应该完成练习 10.4，该练习要求您通过 Linux 命令行执行各种用户管理任务。

**练习 10.4**

## 通过命令行管理用户账户

一些 Linux 用户只知道执行特定任务的一种方法。当系统损坏或配置错误时，某些执行任务的方法可能无法使用；例如，如果 X 窗口系统无法工作，那么基于 X 的工具将无法使用。本练习测试您使用命令行执行常见用户管理任务的能力。此时，您可以回顾相关步骤，但在参加 RHCE 考试时，您将无法参考书籍或笔记。



### 练习 10.4（续）

- 1. 使用命令行创建一个登录名为 test101 的普通用户账户。
- 2. 使用命令行修改该账户，将其关联的全名为 goner。
- 3. 使用命令行删除你创建的用户账户。
- 4. 检查 `/etc/passwd` 以验证该账户已被删除。

## 通过 *userconf* 管理组

用户组（通常简称为“组”）允许你将一组用户（称为成员）关联在一起。你可以使用熟悉的 Unix `chmod` 命令来指定所有者、所属组员以及其他用户访问文件和目录所需的权限。

`/etc/group` 文件定义了 Linux 用户组。文件中的每一行描述一个组。以下是一个典型的 `/etc/group` 文件：

```
root::0:root
bin::1:root,bin,daemon
daemon::2:root,bin,daemon
sys::3:root,bin,adm
adm::4:root,adm,daemon
tty::5:
disk::6:root
lp::7:daemon,lp
mem::8:
kmem::9:
wheel::10:root
mail::12:mail
news::13:news
uucp::14:uucp
man::15:
games::20:
gopher::30:
dip::40:
ftp::50:
nobody::99:
users::100:
floppy:x:19:
console:x:101:
utmp:x:102:
ppusers:x:230:
popusers:x:231:
slipusers:x:232:
slocate:x:21:
xfs:x:233:
bill:x:500:
```

每行包含以下字段，由冒号分隔：

- **组名 (Group name)** `/etc/group` 文件中该行定义的组名称。
- **密码 (Password)** 与该组关联的加密密码。在 Linux 中，组密码并不常用。
- **组 ID (Group ID)** 与该组关联的数字 ID。
- **成员 (Members)** 组员的登录名称。

你可以使用 `linuxconf` 或 `userconf` 来创建组、更改组员身份以及删除组。你也可以通过命令行完成这些操作。本节将解释如何使用 `userconf` 管理组；下一节将解释如何使用命令行管理组。

### 创建组

要使用 `userconf` 创建组，请按照以下步骤操作：

- 1. 启动 `userconf`。
- 2. 选择 Group Definitions 并按 Enter；或者，如果你使用的是 X 窗口系统，点击 Group Definitions。

根据过滤器设置（在 Control $\succ$ Features 中），你可能会看到一个 Filter 对话框。使用该对话框将用户组限制为你想要查看的组，或按 Accept 查看所有组。随后将出现如图 10.8 所示的 Users Groups 屏幕。

**图 10.8 User Groups 屏幕**
![](img/4eef9c6f2f52b608eba628cf4e2793ce_270_0.png)

- 3. 点击 Add 按钮。随后将出现如图 10.9 所示的 Group Specification 屏幕。

**图 10.9 Group Specification 屏幕**
![](img/4eef9c6f2f52b608eba628cf4e2793ce_270_1.png)

- 4. 填写参数字段。关于每个字段的信息请参考表 10.3。
- 5. 点击 Accept 按钮。

**表 10.3 组参数**

| 参数 | 描述 |
|---|---|
| Group name | 组的名称。 |
| Group ID | 数字组 ID。 |
| Alternate members | 组员的用户名，由一个或多个空格分隔（可选）。 |

### 删除组

要使用 `userconf` 删除组，请按照以下步骤操作：

- 1. 启动 `userconf`。
- 2. 选择 Group Definitions 并按 Enter；或者，如果你使用的是 X 窗口系统，点击 Group Definitions。

根据过滤器设置（在 Control $\succ$ Features 中），你可能会看到一个 Filter 对话框。使用该对话框将用户组限制为你想要查看的组，或按 Accept 查看所有组。随后将出现 Users Groups 屏幕。

- 3. 选择你想要删除的组并按 Enter；或者，如果你使用的是 X 窗口系统，点击该组。随后将出现 Group Specification 屏幕。
- 4. 要删除该组，点击 Del 按钮。一个对话框会要求你确认操作；点击 Yes 删除该组，或点击 No 取消删除。

### 修改组员身份

你可以通过修改每个受影响的用户账户或通过修改组来更改组员身份。通常，修改组会更方便。操作步骤如下：

- 1. 启动 `userconf`。
- 2. 选择 Group Definitions 并按 Enter；或者，如果你使用的是 X 窗口系统，点击 Group Definitions。

根据过滤器设置（在 Control $\succ$ Features 中），你可能会看到一个 Filter 对话框。使用该对话框将用户组限制为你想要查看的组，或按 Accept 查看所有组。随后将出现 Users Groups 屏幕。

- 3. 选择你想要修改的组并按 Enter；或者，如果你使用的是 X 窗口系统，点击该组。随后将出现 Group Specification 屏幕。
- 4. 根据需要修改 Alternate Members 字段，然后点击 Accept 按钮。

在继续之前，请完成练习 10.5，该练习将测试你执行常见组管理任务的能力。

## 练习 10.5
### 管理组

本练习要求你添加并删除一个用户组。如有必要，请回顾分步操作步骤。但在参加 RHCE 考试之前，请确保能够无需帮助地执行组管理操作。

- 1. 定义登录名为 test01、test02 和 test03 的新用户。
- 2. 定义一个名为 testgroup 的新组。
- 3. 将每个新用户添加到该组中。
- 4. 通过检查 `/etc/group` 来验证你的操作。
- 5. 将 test03 用户从该组中删除。
- 6. 通过检查 `/etc/group` 来验证你的操作。

## 通过命令行管理组

你可以使用命令行来管理用户组。命令允许你创建组、删除组或修改组员身份。

### 创建组

要通过命令行创建组，请执行 `groupadd` 命令，其形式如下：

```
groupadd -g groupid group
```

你必须指定要创建的组名 `group`。如果你没有指定组 ID，将使用下一个可用的组 ID。如果你想创建一个系统组（组 ID 小于 500），请在组名前指定 `-r` 作为参数。有关更多信息，请参阅 `groupadd` 的 man 手册页。

### 删除组

要通过命令行删除组，请执行 `groupdel` 命令，其形式如下：

```
groupdel group
```

有关更多信息，请参阅 `groupdel` 的 man 手册页。

### 修改组名

要通过命令行修改组的名称，请执行 `groupmod` 命令，其形式如下：

```
groupmod -n newname group
```

有关更多信息，请参阅 `groupmod` 的 man 手册页。

### 修改组员身份

要通过命令行修改组的成员身份，你必须手动编辑 `/etc/group` 或执行 `usermod` 命令来调整每个受影响用户的组身份。通常这意味着你必须多次执行该命令；因此，通过 `userconf` 修改组员身份通常比通过命令行更方便。`usermod` 命令在本章前面部分已有描述。

为了检查你对通过命令行管理组的理解，请完成练习 10.6。

## 练习 10.6
## 通过命令行管理组

本练习测试你使用命令行执行组管理任务的能力。如果需要帮助，你可以回顾 `usermod` 命令的解释。但在继续之前，请确保你无需参考本章内容即可完成练习。否则，你将无法为 RHCE 考试做好充分准备。

执行练习 10.5 中给出的操作，但使用命令行而非 `userconf`。

## 数据共享

通常，用户需要共享一些不希望其他人访问或修改的数据。实现这一点的一个简单方法是为每组想要共享数据访问权限的用户创建一个组，将相关文件或目录的组所有权分配给该新组，然后分配访问权限，允许组员执行授权操作，但排除其他用户。

例如，假设 `tom`、`dick` 和 `harry` 想要访问目录 `bigdeal`，但想禁止其他人访问。你可以创建一个名为 `tdandh` 的组（作为成员的提醒），并将 `bigdeal` 目录的组所有权设置为 `tdandh`。为该目录分配 770 的权限，即可达到预期效果。

练习 10.7 将测试你使用访问权限在两个用户之间共享数据的能力。

## 练习 10.7
## 数据共享

本练习要求你创建一个用户组和一个目录，然后设置访问权限，使该组对该目录具有特殊访问权。如果你需要复习 `chmod` 命令，请回顾第三章“Unix 基础”。在继续之前，请确保你能无需协助地完成该练习。



## 练习 10.7（接上页）

1. 创建一个名为 project 的目录。
2. 设置一个包含用户 ftp 和 lp 的用户组。
3. 设置该目录的权限，使 ftp 和 lp 可以对其进行读写，但其他用户只能读取。

## 用户配置文件自定义

当用户登录时，命令解释器会执行几个用于配置用户环境的文件。这些文件包含设置环境变量、调整路径、创建命令别名等操作的命令。通过修改这些文件，您可以配置用户的环境。

### 全局用户配置文件

当 shell 为 BASH 的用户登录时，执行的文件包括以下内容：

- `/etc/bashrc`：一个用于建立别名和函数的文件。
- `/etc/profile`：一个用于设置环境变量并执行其他操作的文件，包括执行 `/etc/profile.d` 目录下的文件。
- `/etc/profile.d`：一个包含若干小型脚本的目录。文件名以 `.sh` 结尾的文件由 `/etc/profile` 执行。

以下是一个典型的 `/etc/bashrc` 文件：

```
# /etc/bashrc

# System wide functions and aliases
# Environment stuff goes in /etc/profile

# For some unknown reason bash refuses to inherit
# PS1 in some circumstances that I can't figure out.
# Putting PS1 here ensures that it gets loaded every time.
PS1="[\u@\h \W]\$ "
```

以下是一个典型的 `/etc/profile` 文件：

```
# /etc/profile

# System wide environment and startup programs
# Functions and aliases go in /etc/bashrc

PATH="$PATH:/usr/X11R6/bin"
PS1="[\u@\h \W]\$ "

ulimit -c 1000000
if [ `id -gn` = `id -un` -a `id -u` -gt 14 ]; then
    umask 002
else
    umask 022
fi

USER=`id -un`
LOGNAME=$USER
MAIL="/var/spool/mail/$USER"

HOSTNAME=`/bin/hostname`
HISTSIZE=1000
HISTFILESIZE=1000

INPUTRC=/etc/inputrc
export PATH PS1 HOSTNAME HISTSIZE HISTFILESIZE USER LOGNAME MAIL INPUTRC

for i in /etc/profile.d/*.sh ; do
    if [ -x $i ]; then
        . $i
    fi
done

unset i
export MPAGE="-2 -Plp"
```

`/etc/profile.d` 中的文件包括以下内容：

- `kde.csh`：为 C shell 用户设置 KDE 环境。
- `kde.sh`：为 BASH shell 用户设置 KDE 环境。
- `ang.sh`：设置国际化设施使用的环境变量。
- `mc.csh`：为 C shell 用户设置 Midnight Commander 环境。
- `mc.sh`：为 BASH shell 用户设置 Midnight Commander 环境。

您可以修改 `/etc/profile.d` 目录的内容，或添加和删除文件，以自定义用户登录时执行的操作。

### 用户配置文件

当您使用 `userconf` 或使用带有 `-m` 参数的 `useradd` 创建用户账户时，`/etc/skel` 的内容将被复制到用户的主目录中。

`/etc/skel` 中的文件和目录通常是隐藏文件和目录，其名称以点 (.) 开头。默认文件包括以下内容：

- `.xdefaults`：一个用于建立各种 X 选项的文件。
- `.bash_logout`：一个在用户退出初始 BASH shell 时清除屏幕的文件。
- `.bash_profile`：一个调用 `.bashrc` 并建立路径和其他环境变量的文件。
- `.bashrc`：一个调用 `/etc/bashrc` 的文件。
- `.kde`：一个包含多种子目录和文件的目录，这些文件是 KDE 桌面环境和 KDE 应用程序（如 KWM 窗口管理器）的一部分。
- `.kderc`：一个指定 KDE 选项的文件。
- `Desktop`：一个包含配置用户 KDE 桌面的文件的目录。

您可以修改 `/etc/skel` 的内容，或添加和删除文件与目录。这样做可以实现对用户环境的自定义。

现在，完成练习 10.8 以检查您对用户配置文件的理解。

### 练习 10.8：自定义用户配置文件

默认安装的用户配置文件往往无法满足个人偏好。然而，许多用户不知道如何自定义他们的配置文件。

检查您主目录中用户配置文件的内容。调整一个或多个选项以更好地适应您的偏好。如果您想不起相关文件的名称，请回顾本小节给出的解释；但在进入下一节之前，请确保您能够在不寻求帮助的情况下识别这些文件。

## 其他用户管理程序

要更改与用户账户关联的密码，请执行以下步骤：

1. 启动 `userconf`。
2. 选择 User Accounts 并按 Enter；或者，如果您使用的是 X，请点击 User Accounts。随后将出现 User Accounts 屏幕。

根据过滤器设置（在 Control $\rhd$ Features 中），您可能会看到一个 Filter 对话框。使用该对话框将用户账户限制在您想要看到的范围内，或按 Accept 查看所有账户。

3. 高亮显示您想要修改的账户并按 Enter；或者，如果您使用的是 X，可以直接点击该账户。
4. 点击 Password 按钮。随后将出现 Changing Password 对话框。
5. 输入所需的密码并点击 Accept 按钮。Changing Password 对话框将再次出现。
6. 通过重新输入来确认您之前输入的密码。点击 Accept 按钮。Users Accounts 屏幕将重新出现。

您还可以使用命令行更改与用户账户关联的密码。执行 `passwd` 命令，其格式如下：

```
passwd user
```

程序将提示输入两次密码，以确保您输入正确。

`mkpasswd` 程序是一个非常有用的实用工具，它可以生成随机密码或为用户账户分配随机密码。要生成随机密码，请执行命令：

```
mkpasswd
```

程序将生成并显示密码。要自动为用户账户分配随机密码，请执行命令：

```
mkpasswd user
```

该命令将分配并显示密码。

练习 10.9 是本章的最后一个练习。您应该完成它，以测试您管理密码的能力。

## 练习 10.9：管理密码

更改用户密码是最频繁的系统管理任务之一，因此，您应该能够流畅地执行此任务。使用 `passwd` 命令更改与您的登录账户关联的密码。如果您想不起如何操作，可以回顾本节给出的解释。但请记住，在 RHCE 考试期间，您将无法查阅书籍或笔记。

## 总结

在本章中，您学习了管理用户账户和组。涵盖的最重要主题有：

**用户账户类型** Red Hat Linux 支持多种用户账户类型，包括普通用户账户、PPP 用户账户、SLIP 用户账户、UUCP 用户账户和 POP 用户账户。

**配置用户账户** 您可以使用 `userconf` 程序或命令行来配置用户账户。

**禁用用户账户** 禁用用户账户可防止其被使用；您可以使用 `userconf` 程序禁用用户账户。

**删除用户账户** 删除用户账户将其从系统中移除；您可以使用 `userconf` 程序删除用户账户。该程序允许您删除或归档账户主目录中的文件，或者将文件保留在原处。

**用户组** 您可以使用 `userconf` 命令管理用户组。

**共享数据** 您可以使用用户组和 Linux 文件权限方案来帮助您管理对文件和目录的访问。

**用户配置文件** 您可以通过修改 `/etc/bashrc`、`/etc/profile` 以及位于 `/etc/profile.d` 和 `/etc/skel` 中的脚本来管理用户配置文件。

**其他用户管理程序** 其他用户管理程序包括允许您更改用户账户密码的 `passwd`，以及生成并分配随机密码的 `mkpasswd`。

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- ordinary user（普通用户）
- POP user（POP 用户）
- PPP user（PPP 用户）
- SLIP user（SLIP 用户）
- user account（用户账户）
- user group（用户组）
- UUCP user（UUCP 用户）



## 补充信息来源

如果您想进一步了解本章中介绍的主题，请参考以下来源：

- *The Official Red Hat Linux Reference Guide*（红帽 Linux 官方参考指南）
- 本章所述命令的 man 手册页

## 复习题

1. 以下哪些是 Red Hat Linux 的用户账户类型？
   A. POP 账户
   B. PPP 账户
   C. SLIP 账户
   D. Usenet 账户

2. `userconf` 和 `linuxconf` 之间的关系是什么？
   A. 您可以使用 `linuxconf` 来调用 `userconf`。
   B. 您可以使用 `userconf` 来调用 `linuxconf`。
   C. 在调用 `userconf` 之前，必须调用 `linuxconf`。
   D. 在调用 `linuxconf` 之前，必须调用 `userconf`。

3. 具有使用 `linuxconf` 权限的用户可以执行以下哪些任务？
   A. 可以进行配置更改
   B. 可以激活配置更改
   C. 可以给予他人使用 `linuxconf` 的权限
   D. 可以给自己任何想要的权限

4. 当您使用 `useradd` 创建用户账户时，关于初始密码，以下哪项是正确的？
   A. 已锁定
   B. 随机选择
   C. 与登录名相同
   D. 与您的登录名相同

5. 分配给新用户账户的默认组名称是以下哪个？
   A. Null
   B. 与登录名相同
   C. 与创建该用户账户的用户名相同
   D. Users

6. 哪个命令可以生成随机密码？
   A. genpass
   B. mkpasswd
   C. newpass
   D. passwd

## 复习题答案

1. A, B, C。虽然有 UUCP 账户类型，但没有 Usenet 账户类型。
2. A. 您可以从命令行调用 `userconf`，或者通过 `linuxconf` 调用它。
3. A, C. 除非被明确授予权限，否则具有使用 `linuxconf` 权限的用户不能激活配置更改。
4. A. 密码最初被锁定；在通过将密码更改为可用密码解锁账户之前，用户无法登录。
5. B. Red Hat Linux 将新用户分配到一个与用户登录名同名的个人组中。
6. B. `mkpasswd` 命令用于生成随机密码。

# 第 11 章：实现用户和组磁盘空间配额

### 本章涵盖的 RHCE 准备主题：

- 理解配额并能够实现用户和组配额。

多用户系统的管理员有点像操场监督员：两者都花费大量时间制定和执行旨在促进共享的策略。当资源充足时，共享是一件简单的事，但当用户必须争夺稀缺资源时，共享就变得复杂了。计算机资源中最稀缺的资源之一就是磁盘空间：曾有人打趣说，一个人永远不会太富有，永远不会太苗条，也不会拥有太多的磁盘空间。

磁盘空间配额是一种旨在促进磁盘空间共享的策略机制。管理员可以为用户或组分配固定数量的磁盘空间，用户不能超过此限额。通过限制用户（或组）可以消耗的磁盘空间量，管理员可以防止贪婪的用户占用超过其应得的份额。本章将解释磁盘空间配额以及如何实现它们。

## 配额概念

磁盘空间配额限制了用户或组可以使用磁盘空间的数量。在 `/etc/fstab` 文件中，您需要指定启用了磁盘配额的分区。只有 Linux ext2 分区支持磁盘配额；您无法为其他文件系统类型启用配额。

配额设施使用存储在启用配额的文件系统根目录中的一对文件：

- `quota.user`，存储分配给用户的配额
- `quota.group`，存储分配给组的配额

例如，如果一个分区被挂载为 `/home`，那么文件将被命名为 `/home/quota.user` 和 `/home/quota.group`。`quotacheck` 命令会更新这些文件的内容以反映实际的磁盘空间使用情况。如果文件不存在，该命令将创建它们。

这些文件包含二进制信息，不能直接编辑。要为用户或组建立配额，请使用 `edquota` 命令。您可以通过执行 `repquota` 命令来查看文件的内容。

配额跟踪在系统启动时启动。`/etc/rc.d/rc.sysinit` 脚本中的命令会更新使用数据并开启配额检查。可以为单个用户或组建立配额。可以定义两种类型的限制：

- 软限制（Soft limits）：当运行 `warnquota` 程序时，超过软限制的用户或组将收到电子邮件通知。
- 硬限制（Hard limits）：超过硬限制的用户或组将被禁止使用额外的磁盘空间。

您可以定义一个与软限制配合使用的宽限期。如果用户在宽限期届满后仍继续超过软限制，则该用户将被禁止使用额外空间。您可以指定对所使用磁盘块数、所使用文件数（inodes）或两者的限制。请考虑以下示例。假设用户 `bob` 具有以下限制：

- 软磁盘空间限制：10000 blocks
- 硬磁盘空间限制：12000 blocks
- 软 inode 限制：100
- 硬 inode 限制：120

最后，假设一个七天的宽限期正在生效，且 `bob` 目前使用了 5000 blocks 的磁盘空间和 50 个 inodes。如果 `bob` 将其磁盘使用量增加到 11000 blocks，他将收到类似这样的一封电子邮件：

你好，

我们注意到您违反了本系统使用的配额系统。我们发现了以下违规情况：

块限制 | 文件限制
---|---
(见下方) | (见下方)

```
Filesystem used soft hard grace used soft hard grace
/dev/hdc 11000 10000 12000 7 days 50 100 120 7 days
```

我们希望您在宽限期届满前进行清理。基本上，这意味着系统认为您在上述分区上使用了超过允许的磁盘空间。如果您在宽限期届满前没有删除文件并将使用量降低到配额以下，系统将阻止您创建新文件。

如需进一步帮助，请通过 support@localhost 联系我们，或拨打电话 (xxx) xxx-xxxx 或 (xxx) xxx-xxxx。

如果 bob 未能在七天内减少块数，或者将其使用量增加到 12000 blocks，他将被禁止使用额外的磁盘空间，直到他将使用量降低到软配额以下。

请注意配额违规电子邮件中被遮蔽的电话号码。电子邮件的内容硬编码在源文件 `warnquota.c` 中。为了方便用户，您应该安装源代码 RPM 包，修改消息以更好地适应您的本地环境，然后重新编译并重新安装软件包。但是，要完成此操作，您必须至少具备一定的 C 语言编程技能。

## 实现配额

要实现配额，请遵循以下步骤：

- 配置内核
- 安装 quota 软件包
- 修订 /etc/fstab
- 建立配额文件
- 设置配额
- 开启配额检查

以下小节将解释这些步骤。

## 配置内核

为了支持配额，系统的内核必须经过正确配置。具体来说，内核在编译时必须启用了 `CONFIG_QUOTA` 选项。标准 Red Hat Linux 内核包含此选项；但是，如果您编译自己的内核，必须启用它，否则将无法使用配额。有关编译 Linux 内核的更多信息，请参阅第 18 章“配置、构建和安装自定义内核”。

### 安装 `quota` 软件包

quota 软件包是 Red Hat Linux 基础组件的一部分，通常在安装过程中安装。要检查该软件包是否已安装，请执行命令：

```bash
rpm -qi quota
```

该命令将打印软件包的简短描述，或者一条 stating 该软件包未安装的消息。

要安装 `quota` 软件包，请移动到包含该软件包的目录并执行命令：

```bash
rpm -Uvh quota*.rpm
```

`/etc/rc.d/rc.sysinit` 文件在系统启动时执行以下步骤：

- 在根文件系统上运行 `quotacheck`
- 在所有其他本地文件系统上运行 `quotacheck`
- 开启配额检查

### 修订 `/etc/fstab`

要指定某个分区支持磁盘配额，您必须修订 `/etc/fstab` 中对该分区的描述。以下是一个示例行文件：

```text
/dev/hda8  /             ext2   defaults      1 1
/dev/hda5  /boot         ext2   defaults      1 2
/dev/hda6  /home         ext2   defaults      1 2
/dev/hdc    /mnt/cdrom    iso9660 noauto,owner,ro  0 0
```



| 设备 | 挂载点 | 文件系统 | 选项 | Dump Pass |
| :--- | :--- | :--- | :--- | :--- |
| /dev/hda7 | /usr | ext2 | defaults | 1 2 |
| /dev/fd0 | /mnt/floppy | ext2 | noauto,owner | 0 0 |
| none | /proc | proc | defaults | 0 0 |
| none | /dev/pts | devpts | gid=5,mode=620 | 0 0 |

要指定 `/home` 分区支持用户磁盘配额，请将该行修改如下：

```
/dev/hda6  /home  ext2 defaults,usrquota 1 2
```

要指定 `/home` 分区支持组磁盘配额，请将该行修改如下：

```
/dev/hda6  /home  ext2 defaults,grpquota 1 2
```

要指定 `/home` 分区同时支持用户和组磁盘配额，请将该行修改如下：

```
/dev/hda6  /home  ext2  defaults,usrquota,grpquota 1 2
```

修改分区选项后，必须重新挂载该分区。例如，要重新挂载 `/home` 分区，请执行命令：

```
mount -o remount /home
```

如果你愿意，可以使用 linux-conf 来指定 usrquota 或 grpquota 选项。选择 Config $\rhd$ File Systems $\rhd$ Access Local Drive，选择所需的分区，并在 Volume Specification 界面上指定所需的选项。

## 建立配额文件

一旦指定了支持磁盘配额的分区，就必须在每个此类分区中建立配额文件 `quota.user` 和 `quota.group`。为此，请执行 `quotacheck` 命令：

```
quotacheck -avug
```

该命令可能需要几分钟时间来完成累计和存储每个用户账户及组所使用磁盘空间记录的任务。

为了避免拒绝服务攻击，你应该验证创建的 `quota.user` 和 `quota.group` 文件仅对其所有者（应当是 root）具有读写权限。

> quotacheck 维护的文件必须与文件系统保持同步。如果系统未正常关机，系统在重启时将自动运行 quotacheck。

## 设置配额

现在你可以为用户或组设置配额了。请记住，你只能为那些支持配额的分区设置配额。此外，你只能设置该分区所配置的配额类型。例如，如果你配置分区支持用户配额，则只能设置用户配额，而不能设置组配额。

### 设置默认配额

在为特定用户或组设置配额之前，你可能希望设置默认配额。默认配额适用于任何尚未设置配额的用户或组。要设置默认配额，请执行以下步骤：

- 1. 启动 `linuxconf`。
- 2. 选择 Config $\rightarrow$ File Systems $\rightarrow$ Set Quota Defaults。随后将出现如图 11.11 所示的“用户和组默认配额”界面。如果你使用的是 X，界面外观会略有不同。
- 3. 指定所需的默认限制和宽限期。零 (0) 限制意味着没有限制。点击 Accept 按钮保存更改。

> 警告：使用 linuxconf 设置默认配额会覆盖手动输入的限制。最好在设置特定用户配额之前，仅设置一次默认配额。

### 设置用户配额

要为用户设置配额，请执行命令：

```
edquota -u user
```

其中 user 是用户的登录名。edquota 命令会启动默认编辑器（由 `$EDITOR` 环境变量指定），显示一系列类似于以下内容的行：

```
Quotas for user bill:
/dev/hda6: blocks in use: 1236, limits (soft = 0, hard = 0)
inodes in use: 235, limits (soft = 0, hard = 0)
```

要指定限制，请更改相应的数字，保存文件并退出编辑器。零 (0) 限制意味着没有限制。例如，你可以将用户 bill 的限制修改如下：

```
Quotas for user bill:
/dev/hda6: blocks in use: 1236, limits (soft = 8000, hard = 10000)
inodes in use: 235, limits (soft = 0, hard = 0)
```

要验证配额是否已设置，请执行命令：

```
quota -u user
```

其中 user 是用户的登录名。你应该能看到通过编辑器输入 Same 的相同信息。

### 设置组配额

要指定组配额，请执行命令：

```
edquota -g group
```

其中 *group* 是组的名称。`edquota` 命令会启动默认编辑器（由 `$EDITOR` 环境变量指定），显示一系列类似于以下内容的行：

> Quotas for group users:
> /dev/hda6: blocks in use: 12436, limits (soft = 0, hard = 0)
>           inodes in use: 2135, limits (soft = 0, hard = 0)

要修改限制，请更改相应的数字，保存文件并退出编辑器。零 (0) 限制意味着没有限制。

要验证配额是否已设置，请执行命令：

```
quota -g group
```

其中 *group* 是组的名称。你应该能看到通过编辑器输入 Same 的相同信息。

### 设置宽限期

要设置宽限期，请执行命令：

```
edquota -t
```

`edquota` 命令会启动默认编辑器（由 `$EDITOR` 环境变量指定），显示一系列类似于以下内容的行：

> Time units may be: days, hours, minutes, or seconds
> Grace period before enforcing soft limits for users:
> /dev/hda6: block grace period: 7 days, file grace period: 7 days

要修改限制，请更改相应的数字或时间单位，保存文件并退出。

### 为多个用户设置配额

你可以使用一个用户账户作为模板来为其他账户设置配额。为此，请按照以下步骤操作：

- 1. 执行命令 `edquota -p user`，其中 `user` 是你想要用作模板的用户账户登录名。这将把指定的用户账户建立为模板。
- 2. 执行命令 `edquota user`，其中 `user` 是你想要用作模板的用户账户登录名。`edquota` 命令将启动默认编辑器。设置所需的限制，保存文件并退出编辑器。这将为模板用户账户建立所需的配额。
- 3. 执行命令 `edquota -p user user1 user2 ...`，其中 `user` 是你想要用作模板的用户账户登录名，其余参数是你希望拥有与模板账户相同配额的用户账户登录名。

### 开启配额检查

最后，你可以正式开启配额检查了。配额检查将在系统启动时开启。不过，你也可以在不重启的情况下通过执行以下命令来开启配额检查：

```
quotaon -av
```

此命令将同时开启用户和组配额。若仅开启用户配额，请执行命令：

```
quotaon -avu
```

同样，若仅开启组配额，请执行命令：

```
quotaon -avg
```

要关闭配额，请执行命令：

```
quotaoff -av
```

此命令将同时关闭用户和组配额。若仅关闭用户配额，请执行命令：

```
quotaoff -avu
```

同样，若仅关闭组配额，请执行命令：

```
quotaoff -avg
```

## 管理配额

配额设置完成后，你可以使用报告配额状态的命令。本节的第一小节将解释如何操作，第二小节将解释如何为通过 NFS 导出的分区设置配额。

### 配额报告

要查看分配给某个用户的配额，请执行命令：

```
quota -u user
```

其中 *user* 是用户的登录名。生成的报告将类似于：

```
Disk quotas for user test (uid 510):
 Filesystem blocks quota limit grace files quota limit grace
 /dev/hda 804 150000 200000 152 0 0
```

用户可以通过执行类似的命令查看自己的配额：

```
quota
```

但是，只有 root 可以查看其他用户的配额。要查看多个用户的配额，请执行命令：

```
repquota -a
```

生成的报告类似于：

```
Block limits                    File limits
User      --  used      soft      hard grace used soft hard grace
root      --  1232356   0         0       7102  0    0   0
jczarnec  --  11860     150000    200000        143  0   0
khahn     --  180       150000    200000        45   0   0
mhall     +-  192308    150000    200000  7days 247  0   0
plin      --  28672     150000    200000        216  0   0
mtuinstr  --  184       150000    200000        46   0   0
rtc       --  3420      150000    200000        350  0   0
rlee      +-  173336    150000    200000  none  852  0   0
dchan     --  252       150000    200000        62   0   0
```

请注意，违反配额的用户（例如 mhall）会被标记一个加号 (+)。

### 配额与 NFS

如果你通过 NFS 导出目录，可以建立磁盘配额来限制 NFS 用户使用的磁盘空间或 inode。只需将所需的限制应用于 NFS 将远程用户映射到的本地用户账户。例如，如果远程用户被映射到本地用户 nfsuuser，请在 nfsuuser 账户上设置配额。有关 NFS 的更多信息，请参阅第 21 章“安装和配置主要网络服务”。

现在你已经了解了配额以及如何建立配额，请完成练习 11.1，该练习将测试你设置配额的能力。

### 练习 11.1：设置配额

本练习要求你运用关于磁盘配额的知识来设置配额检查。你可以回顾本章中的解释和步骤。但在进入下一章之前，请确保你在不借助帮助的情况下能够设置磁盘配额，因为在 RHCE 考试期间你将无法获得帮助。

- 1. 在系统的 /home 或 root 分区上建立用户和组配额。
- 2. 为磁盘空间使用建立默认的软限制和硬限制。
- 3. 建立五天的宽限期。



## 练习 11.1（续）

- 4. 指定至少一名没有磁盘空间限制的用户，以及另一名限制低于默认限制的用户。
- 5. 开启配额检查。
- 6. 使用 `repquota` 命令验证你的工作。
- 7. 通过故意超出磁盘空间的软限制来验证你的工作。为了以可控的方式超出配额，请执行如下形式的命令：

```
dd if=/dev/zero of=test count=n
```

其中 n 是将要写入名为 test 的文件的数据块数量。

## 总结

在本章中，你学习了关于磁盘空间配额的知识。涵盖的最重要主题包括：

**磁盘配额 (Disk Quotas)** 磁盘配额允许你限制用户所分配的磁盘空间量和 inode 数量。磁盘配额可以分配给用户或用户组。

**硬限制和软限制 (Hard and Soft Limits)** 当超出硬限制时，用户将被禁止分配额外的磁盘空间或 inode。当超出软限制时，用户会收到通知。

**实施配额 (Implementing Quotas)** 要实施配额，必须安装 quota 软件包，该包包括 `quotacheck`、`edquotaon`、`quotaoff` 和 `quota` 命令。

**quotacheck 程序** `quotacheck` 程序用于建立配额控制文件 `quota.user` 和 `quota.group`。

**edquota 程序** `edquota` 程序允许你建立或修改与用户或用户组关联的配额。

**quotaon 和 quotaoff 程序** `quotaon` 和 `quotaoff` 程序分别用于开启和关闭配额。

**quota 程序** `quota` 程序允许你打印显示磁盘配额状态的报告。

### 关键术语

在进入下一章之前，请确保你熟悉以下术语：

- 宽限期 (grace period)
- 组配额 (group quota)
- 硬限制 (hard limit)
- 软限制 (soft limit)
- 用户配额 (user quota)

## 其他信息来源

如果你想进一步了解本章介绍的主题，请参考以下资源：

- *The Quota Mini-HOWTO*，作者 Albert M.C. Tam
- 本章中提及的命令的 man 手册页

## 复习题

- 1. 你可以将配额与以下哪些项关联？
    A. 目录
    B. 组
    C. 分区
    D. 用户

- 2. 如果磁盘空间硬限制为零，以下哪个说法是正确的？
    A. 用户可以创建无限数量的文件。
    B. 用户可以使用无限量的磁盘空间。
    C. 用户无法创建磁盘文件。
    D. 用户违反了磁盘空间限制。

- 3. 假设一名用户拥有 150 个 inode，且软限制为 100，硬限制为 200。如果宽限期尚未过期，以下哪个说法正确？
    A. 用户不能再创建更多文件。
    B. 用户不能向现有文件追加数据。
    C. 用户在删除某些文件之前无法注销。
    D. 用户将收到一封关于违规的电子邮件通知。

- 4. 假设一名用户拥有 150 个 inode，且软限制为 100，硬限制为 200。如果宽限期已过期，以下哪个说法正确？
    A. 用户不能再创建更多文件。
    B. 用户不能向现有文件追加数据。
    C. 用户在删除某些文件之前无法注销。
    D. 当运行 `warnquota` 时，用户将收到一封关于违规的电子邮件通知。

- 5. 以下哪个命令允许你设置用户的配额？
    A. `edquota`
    B. `edquota user`
    C. `edquota -p user`
    D. `edquota -u user`

- 6. 使用组配额时创建的文件名称是什么？
    A. `quota`
    B. `quota.group`
    C. `quota.user`
    D. `quotas`

## 复习题答案

- 1. B, C, D。为用户或组建立的配额是应用于分区的；你不能为单个目录建立配额。
- 2. B。磁盘空间限制约束的是磁盘空间的大小，而不是文件的数量。零限制意味着用户可以使用无限的空间。
- 3. D。在宽限期过期之前，用户可以自由地超过软限制。
- 4. A, D。一旦宽限期过期，用户必须遵守软限制；在用户释放一些 inode 之前，不能创建新文件。
- 5. D。设置用户配额时需要 `-u` 参数。
- 6. B。当为分区指定了组配额时，`quotacheck` 命令会创建 `quota.group` 文件。

# 第 12 章：使用 RPM 软件包

**本章涵盖的 RHCE 准备主题：**

- 理解并能够使用 `rpm` 命令及其开关，特别是与软件包安装和查询相关的开关。
- 理解源码 (*.src.rpm) RPM 软件包的基本元素。

Red Hat, Inc. 对 Linux 社区最显著的贡献之一就是对 Red Hat 软件包管理器 (RPM) 开发的支持。在 RPM 出现之前，安装 Linux 软件很大程度上取决于运气：安装一个应用程序经常会导致另一个应用程序瘫痪。得益于 RPM，Linux 系统管理员现在可以自信地安装应用程序，确保这些应用程序能够正确运行且不会与其他应用程序产生冲突。本章将解释 RPM 设施的运行方式，并描述如何执行常见的 RPM 操作。

## Red Hat 软件包管理器 (RPM)

在 RPM 出现之前，Linux 系统管理员（就像其他 Unix 系统管理员一样）通过下载 TAR 文件、解包并编译源代码来安装程序。程序在共用文件的使用上经常产生冲突，且软件开发人员经常对文件的位置以及命令和库的可用性做出假设。因此，系统管理员经常需要花费大量加班时间来勉强让程序运行。

RPM 通过跟踪已安装软件程序的信息来管理软件安装过程。因此，系统管理员很少发现安装一个程序导致另一个程序损坏。RPM 由三个组件组成，它们管理系统文件的情况如图 12.1 所示：

- 软件包文件 (Package files)
- RPM 数据库 (The RPM database)
- `rpm` 命令

**图 12.1 RPM 设施**

以下小节将详细解释这些组件。

### 软件包文件

软件包文件取代了在 RPM 出现之前使用的 TAR 文件。与 TAR 文件一样，软件包文件包含必须安装的文件。与 TAR 文件不同的是，软件包文件包含描述该包中包含的应用程序或服务的信息。例如，软件包文件会标识为了正确安装和运行而必须安装的任何能力（capabilities），如库或其他软件包。这种信息被称为依赖信息 (dependency information)。存储在软件包中的其他信息包括：

- 软件包的名称和版本
- 构建日期和构建主机
- 软件包的描述
- 每个包含文件的大小和 MD5 校验和
- 构建该软件包的人员或组织身份
- 该软件包所属的软件包组

软件包文件的名称具有特定的结构，类似于以下形式：

```
package-version-buildarchitecture.rpm
```

其中：

- `package` 是文件中包含的软件包名称。这允许你缩写文件名，以适应 DOS 或其他限制文件名字符数的文件系统的限制。
- `version` 是软件包的版本号。
- `build` 是软件包的构建号。
- `architecture` 是该软件包设计的计算机架构。

例如，软件包文件名 `gnorpm-0.9-10.i386.rpm` 表示该文件包含名为 `gnorpm` 的软件包的 0.9 版本、第 10 次构建，且适用于 i386 (Intel 386) 架构。

### RPM 数据库

一旦软件包被安装，关于该包的信息就会存储在位于 `/var/lib/rpm` 的 RPM 数据库中。当你执行 `rpm` 命令（例如安装软件包或卸载软件包的命令）时，RPM 设施会检查软件包文件和 RPM 数据库。因此，RPM 设施能够判断执行该命令是否会导致系统处于不一致状态。如果会，RPM 设施将拦截该命令并警告用户潜在的危险。

### `rpm` 命令

`rpm` 命令是 RPM 设施的可执行组件。它拥有大量的开关和参数，使你能够执行以下操作：

- 安装软件包
- 更新软件包
- 移除软件包
- 查询 RPM 数据库
- 查询软件包文件
- 从源代码构建软件包文件
- 验证软件包
- 验证软件包文件

在安装、更新或移除软件包时，`rpm` 命令会进行多项检查，旨在确保系统保持在一致状态。例如，在安装软件包时，`rpm` 会检查：

- 是否有足够的可用磁盘空间来容纳该软件包
- 软件包所需的任何能力（依赖项）是否已安装
- 软件包的安装是否会覆盖现有文件



特殊的开关允许您覆盖这些检查，以便应对异常情况。本章的其余部分将在您需要掌握的常用操作上下文中，解释 `rpm` 的运行方式。

## 添加软件包

要安装软件包，请执行具有以下形式的命令：

```
rpm -i package_file_name
```

其中 `package_file_name` 指定了包含您要安装的软件包的文件名。如果您愿意，可以列出多个软件包名称，或使用 shell 元字符（如 `*`）来指定一组文件。例如，这是一个典型的命令：

```
rpm -i gnorpm-0.9-10.i386.rpm gnome-linuxconf-0.23-1.i386.rpm
```

该命令安装了包含在软件包文件 `gnorpm-0.9-10.i386.rpm` 中的 `gnorpm` 软件包，以及包含在软件包文件 `gnome-linuxconf-0.23-1.i386.rpm` 中的 `gnome-linuxconf` 软件包。当然，命令首先会执行前面描述的检查；如果任何一项检查失败，命令将终止且不会安装任何指定的软件包。

许多系统管理员喜欢包含 `-v` 和 `-h` 标志，例如：

```
rpm -ivh gnorpm-0.9-10.i386.rpm gnome-linuxconf-0.23-1.i386.rpm
```

`-v` 标志使命令在执行时打印状态信息；当您指定多个文件时，这尤其有用，因为 `rpm` 在开始安装每个文件时都会打印一条消息。`-h` 标志使 `rpm` 在安装每个软件包时显示 50 个井号（#），帮助您直观地查看每个软件包安装的进度。以下是一个包含这些标志的典型 `rpm` 调用：

```
# rpm -ivh gnorpm-0.9-10.i386.rpm gnome-linuxconf-0.23-1.i386.rpm
gnorpm
##################################################
gnome-linuxconf
####################################
```

使用 `-vh` 的优点之一是能够非常清晰地看到哪些软件包实际上已被安装。RPM 一个令人恼火的缺陷是，如果软件包已经安装，它将以错误退出。如果没有 `-vh`，有时很难判断在 RPM 中止之前，软件包列表中的哪些软件包已经被安装。

RPM 的另一个便捷功能是对存储在 FTP 服务器上的文件的支持。您无需先下载软件包文件再进行安装，而是可以通过执行以下形式的命令直接从 FTP 服务器安装：

```
ftp://server/path
```

其中 `server` 是匿名 FTP 服务器的主机名或 IP 地址，`path` 指定了软件包文件的路径。例如，以下命令安装驻留在 Red Hat 匿名 FTP 服务器上的软件包：

```
rpm -ivh ftp://contrib.redhat.com/i386/RedHat/RPMS/gnorpm-0.9-10.i386.rpm
```

如果您需要通过特定账户访问 FTP 服务器，请执行以下形式的命令：

```
ftp://user:pass@server/path
```

其中 `user` 和 `pass` 指定用户 ID 和密码，其余标记的含义与前述相同。如果服务器监听的是非标准端口，您可以使用此命令形式：

```
ftp://user:pass@server:port/path
```

其中 `port` 是服务器监听的端口号。

Red Hat Linux 6.2 及更高版本的 RPM 支持文件名通配（globbing），允许您包含通配符。例如，安装 `gnorpm` 的 RPM 命令可以写成：

```
rpm -ivh ftp://contrib.redhat.com/i386/RedHat/RPMS/gnorpm*
```

RPM 的另一个便捷功能是您不需要以任何特定顺序指定软件包文件，即使一个或多个指定的软件包依赖于另一个软件包的功能。`rpm` 命令会自动检测任何依赖关系，并以适当的顺序安装软件包。

如果软件包需要某种*功能（capability）*，且该功能既未由同一命令中指定的软件包提供，也未由已安装的软件包提供，则 `rpm` 命令会打印错误消息。例如：

```
# rpm -i gnorpm-0.9-10.i386.rpm
error: failed dependencies:
    usermode >= 1.13 is needed by gnorpm-0.9-10
    librpm.so.0 is needed by gnorpm-0.9-10
```

要解决*依赖关系（dependency）*，您必须安装提供所需功能的相应软件包，或将现有软件包升级到更高版本。例如，上述错误消息指出需要更高版本的 `usermode` 软件包以及名为 `librpm.so.0` 的库。在本章稍后部分，您将学习如何发现一个软件包提供了哪些功能，从而确定例如哪个软件包提供了 `librpm.so.0` 库。

如果您尝试安装一个与现有软件包或文件冲突的软件包，您将看到类似这样的错误消息：

```
# rpm -i gnorpm-0.9-10.i386.rpm
file /usr/bin/gnorpm from install of gnorpm-0.9-10 conflicts with file from package gnoway-0.8-5
file /usr/share/gnome/apps/System/gnorpm.desktop from install of gnorpm-0.9-10 conflicts with file from package gnoway-0.8-5
file /usr/share/gnome/help/gnorpm/C/gnorpm.html from install of gnorpm-0.9-10 conflicts with file from package gnoway-0.8-5
```

如果您尝试安装的软件包磁盘空间不足，您将看到另一种类型的错误消息。

假设您安装了一个通过 TAR 文件分发的软件程序。后来，该软件发布了新版本，并使用 RPM 进行分发。当您安装新软件包时，RPM 确定它将覆盖现有文件。对于 RPM 识别为配置文件的文件，它不会直接覆盖，而是通过在文件名后附加 `.rpmsave` 来保存每个现有的配置文件。

为了克服错误和其他异常情况，您偶尔可能需要以下特殊的 `rpm` 参数：

- `--force`：覆盖较新的软件包或现有文件
- `--nodeps`：跳过依赖检查
- `--replacefiles`：替换由另一个软件包拥有的文件

例如，尽管存在依赖问题但仍要安装 `gnorpm` 软件包，您可以执行以下命令：

```bash
rpm -i --nodeps gnorpm-0.9-10.i386.rpm \
  gnome-1-linuxconf-0.23-1.i386.rpm
```

无论是否存在依赖问题，该命令都将执行成功；但是，除非所需文件实际上存在，否则安装的程序将无法运行。现在您已经知道如何使用 `rpm` 命令添加软件包，请完成练习 12.1，该练习将测试您使用此命令的能力。

### 练习 12.1：添加软件包

RHCE 考试几乎肯定会要求您安装一个或多个软件包。为了确保您掌握该操作，请使用 `rpm` 命令向您的系统添加一个软件包。请确保选择一个尚未安装的软件包。如有必要，请回顾本章的示例，但在参加 RHCE 考试之前，请务必确保您知道如何使用 `rpm` 命令添加软件包。

## 移除软件包

要移除已安装的软件包，请执行以下形式的命令：

```bash
rpm -e package_name
```

其中 `package_name` 是已安装软件包的名称。如果您将此操作视为“擦除（erase）”而非“移除（remove）”软件包，可能会更容易记住这个命令形式，因为 `erase` 中的 `e` 正好对应 `-e` 标志。如果您愿意，也可以指定 `--uninstall` 标志，其含义与 `-e` 标志相同。

不熟悉 `rpm` 命令的用户经常在需要软件包文件名的位置指定软件包名称，反之亦然。请仔细注意每种命令形式具体需要哪一项。

当 `rpm` 命令移除软件包时，它会检查该软件包是否提供了其他软件包所需的功能。如果是，它将抑制执行并向您发出警告。如有必要，您可以通过指定 `--nodeps` 标志来覆盖此检查。

当 `rpm` 命令移除软件包时，它还会保存任何被修改过的配置文件。因此，当您需要额外的磁盘空间来应对某些紧急情况时，可以轻松地移除并在以后重新安装某些软件包。现在，请完成练习 12.2，该练习要求您移除一个软件包。

### 练习 12.2：移除软件包

系统管理员经常需要释放系统上的磁盘空间。一种方便的方法是删除一个软件包，在可用磁盘空间增加后再重新安装。为了验证您移除软件包的能力，请使用 `rpm` 命令移除您在之前练习中添加的软件包。像往常一样，您可以参考本章寻求帮助；但在参加 RHCE 考试之前，请确保您可以在没有书籍或笔记帮助的情况下移除软件包。

## 执行更新和修复

不时会有新版本的软件包发布。这些版本通常包含重要的错误修复或新功能。RPM 使安装新版本的软件包变得简单。为此，请执行以下形式的命令：

```bash
rpm -Uvh package_file_name
```

其中 `package_file_name` 是包含新版本软件包的文件名。如果您愿意，可以省略 `-v` 和 `-h` 标志。`-U` 标志使 `rpm` 命令先移除现有软件包（就像您执行了 `rpm -e` 一样），然后安装新软件包（就像您执行了 `rpm -i` 一样）。

当 `rpm` 命令移除旧软件包时，它会保存任何被修改过的配置文件，并在其名称后附加 `.rpmsave` 进行重命名。如果指定文件中包含的软件包当前尚未安装，`rpm` 命令则会直接安装它。因此，许多系统管理员使用 `-U` 标志来代替 `-i` 标志；如果软件包不存在，`rpm -U` 将安装它；如果已存在，则将其更新。



一个相关的标志 `-F` 允许你仅在软件包已存在时才对其进行更新。例如，以下命令：

```bash
rpm -Fvhn gnorpm-0.9-10.i386.rpm
```

将仅在 gnorpm 软件包已安装的情况下更新该软件包。`-F` 标志有助于保持系统的最新状态。Red Hat 在 www.redhat.com/support/errata 维护着一份更新软件包列表。你应该监控该列表，并使用 `-F` 标志应用你认为对系统运行至关重要的任何修复补丁。

现在，完成练习 12.3，该练习要求你更新一个 RPM 软件包。

### 练习 12.3
#### 更新软件包

如前所述，勤勉的系统管理员会监控 Red Hat Errata 页面并应用有用的修复补丁。为了检查你执行此操作的能力，请使用 `rpm` 命令，利用从 Red Hat Errata 页面下载的修复补丁来更新一个软件包。在练习过程中你可以参考本章寻求帮助，但请记住，在 RHCE 考试期间你将没有这个机会。

## 识别已安装的软件包

你可以使用 RPM 来了解已安装软件包的版本号和构建号。为此，请执行如下形式的命令：

```bash
rpm -q package_name
```

其中 `package_name` 是已安装软件包的名称。输出由单行组成，给出软件包名称、版本号和构建号——例如：

```bash
gnorpm-0.9-10
```

要了解每个已安装软件包的版本号和构建号，请执行命令：

```bash
rpm -qa
```

为了验证你对 `rpm` 命令 `-q` 和 `-qa` 标志的理解，请完成练习 12.4。

### 练习 12.4
#### 识别软件包

通常，能够确定系统中安装了哪些软件包是非常方便的。为了检查你执行此操作的能力，请使用 `rpm` 命令列出系统中安装的软件包的版本号和构建号。如有必要可以回顾本章，但在参加 RHCE 考试时，请准备好在没有帮助的情况下执行此操作。

## 确定文件所有权

你可以使用 RPM 来了解哪个软件包（如果有的话）拥有某个特定文件。为此，请执行如下形式的命令：

```bash
rpm -qf filename
```

其中 `filename` 是文件名，且必须包含完整路径。例如，要求 RPM 报告 `/etc/inittab` 文件的所有权，会产生如下输出：

```bash
# rpm -qf /etc/inittab
initscripts-4.16-1
```

现在，完成练习 12.5，该练习要求你使用 `rpm` 命令的 `-qf` 标志。

### 练习 12.5
## 确定文件所有权

为了检查你对 `rpm` 命令 `-qf` 标志的理解，请使用 `rpm` 命令确定哪个软件包拥有 `/etc/inetd.conf` 文件。在做这个练习时你可以参考本章，但在 RHCE 考试期间，请准备好在没有书籍或笔记帮助的情况下使用 `-qf` 标志。

## 查询和验证软件包内容

`rpm` 命令允许你查询和验证软件包内容。例如，你可以执行以下操作：

- 打印软件包的描述信息
- 列出软件包中包含的文件
- 打印安装或卸载软件包时执行的脚本
- 验证软件包内容的完整性和真实性

接下来的几个小节将解释这些操作。

### 打印软件包描述

要打印已安装软件包的描述信息，请执行如下形式的命令：

```bash
rpm -qi package_name
```

其中 `package_name` 是已安装软件包的名称。例如，打印已安装软件包 `gnorprm` 的描述会产生类似于以下内容：

```text
# rpm -qip gnorprm-0.9-10.i386.rpm
Name                : gnorprm             Relocations: (not relocateable)
Version             : 0.9                 Vendor: Red Hat Software
Release             : 10                  Build Date: Sat Sep 25 13:51:53 1999
Install date: (not installed)             Build Host: porky.devel.redhat.com
Group               : Applications/System  Source RPM: gnorprm-0.9-10.src.rpm
Size                : 434375               License: GPL
Packager            : Red Hat Software
                      <http://developer.redhat.com/bugzilla/>
Summary             : A graphical front-end to RPM for GNOME.
Description :
GnoRPM is a graphical front-end to the Red Hat Package
Manager (RPM). GnoRPM is similar to Glint, but is written
using the GTK+ widget set and the GNOME libraries. GnoRPM
is currently in development, so some features are missing,
but you can currently query, install, upgrade, uninstall and verify packages using a GUI interface.
```

如果要为软件包文件打印此信息，请执行如下形式的命令：

```bash
rpm -qip package_file_name
```

其中 `package_file_name` 是软件包文件的名称。

### 列出包含的文件

要列出已安装软件包中包含的文件，请执行如下形式的命令：

```bash
rpm -ql package_name
```

其中 `package_name` 是已安装软件包的名称。例如，列出 `gnorpmn` 软件包的文件会产生如下输出：

```text
# rpm -ql gnorpmn
/etc/pam.d/gnorpmn-auth
/etc/security/console.apps/gnorpmn-auth
/usr/bin/gnorpmn
/usr/bin/gnorpmn-auth
/usr/doc/gnorpmn-0.9
/usr/doc/gnorpmn-0.9/AUTHORS
/usr/doc/gnorpmn-0.9/NEWS
/usr/doc/gnorpmn-0.9/README
/usr/share/gnome/apps/System
/usr/share/gnome/apps/System/gnorpmn.desktop
/usr/share/gnome/help/gnorpmn/C/find-win.html
/usr/share/gnome/help/gnorpmn/C/gnorpmn.html
/usr/share/gnome/help/gnorpmn/C/index.html
/usr/share/gnome/help/gnorpmn/C/install-win.html
/usr/share/gnome/help/gnorpmn/C/main-win.html
/usr/share/gnome/help/gnorpmn/C/other-uses.html
/usr/share/gnome/help/gnorpmn/C/preferences-win.html
/usr/share/gnome/help/gnorpmn/C/query-win.html
etc.
```

要列出软件包文件中包含的文件，请执行类似的如下形式的命令：

```bash
rpm -qlp package_file_name
```

### 打印脚本

要打印与软件包文件相关的安装前和安装后脚本，请执行如下形式的命令：

```bash
rpm -qp --scripts package_file_name
```

其中 *package_file_name* 是包含软件包的文件名称。例如，列出 `at` 软件包的脚本会产生如下输出：

```bash
# rpm -qp --scripts at-3.1.7-11.i386.rpm
postinstall script (through /bin/sh):
touch /var/spool/at/.SEQ
chmod 600 /var/spool/at/.SEQ
chown daemon.daemon /var/spool/at/.SEQ
/sbin/chkconfig --add atd
preuninstall script (through /bin/sh):
if [ "$1" = 0 ] ; then
/sbin/chkconfig --del atd
fi
```

### 验证软件包内容

RPM 为已安装软件包中的每个文件维护一条记录。该记录包含每个文件的文件大小、所有权、权限、MD5 校验和以及其他信息。如果文件是一个符号链接，记录中包含链接指向的路径；如果文件是一个设备文件，记录中包含关联的主设备号和次设备号。

通过这些记录，你可以通过执行如下形式的命令来确定自软件包安装以来哪些文件（如果有的话）被修改了：

```bash
rpm -V package_name
```

其中 *package_name* 是已安装软件包的名称。输出为每个文件一行。每行有三个字段：

- 状态（Status），指示文件的状态。表 12.1 描述了用于指示状态的标志。
- 配置（Configuration），如果文件是配置文件则包含 `c`，否则为空格。
- 文件名（Filename），给出文件的路径和名称。

#### 表 12.1 软件包验证标志

| 代码 | 含义 |
| :--- | :--- |
| . | 无变化。 |
| S | MD5 校验和已更改。 |
| D | 设备主号或次号已更改。 |
| G | 所有组已更改。 |
| L | 链接路径已更改。 |
| M | 文件模式（权限）已更改。 |
| S | 文件大小已更改。 |
| T | 修改时间已更改。 |
| U | 所有用户已更改。 |

这是一个显示 `setup` 软件包内容状态的示例：

```text
# rpm -V setup
S.5....T c /etc/exports
S.5....T c /etc/hosts.allow
S.5....T c /etc/hosts.deny
S.5....T c /etc/printcap
S.5....T c /etc/profile
S.5....T c /etc/services
etc.
```

如果你愿意，也可以针对软件包文件而非数据库进行比较。如果你怀疑数据库可能损坏，此选项非常有用。为此，请执行如下形式的命令：

```bash
rpm -Vp package_file_name
```

其中 `package_file_name` 是软件包文件的名称。



您还可以验证每个已安装软件包的状态。为此，请执行以下命令：

```
rpm --verify -a
```

## 验证软件包真实性

GNU Privacy Guard (GPG) 是一个开源程序，类似于更广为人知的 Pretty Good Privacy (PGP) 程序，它允许您对电子文档进行身份验证。RPM 软件包的作者可以用 GPG 密钥对他们的工作进行签名。如果您已经安装了 GPG 软件包，就可以验证已签名软件包文件的真实性。为此，请执行如下形式的命令：

```
rpm -K package_file_name
```

其中 `package_file_name` 是软件包文件的名称。您需要下载并安装 Red Hat, Inc. 的 GPG 密钥；您可以在其网站 `www.redhat.com` 的联系页面（Contacts page）上找到该密钥。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_317_0.png)

由于美国出口限制，Red Hat Linux 不包含 PGP。您必须从其他来源获取，例如 `www.zedz.net`。

## 执行高级查询

`rpm` 命令包含一个选项，允许您查询 RPM 数据库以获取特定的信息项，您可以通过 `--queryformat` 标志来指定。例如，以下命令将打印每个已安装软件包的名称和大小，并按名称排序：

```
# rpm -qa --queryformat "%-32(%{NAME})\t%10(%{SIZE})\n" | sort
AfterStep              4248520
AfterStep-APPS        1104878
AnotherLevel            295682
ElectricFence            45648
ImageMagick           3098379
MAKEDEV                 35719
MySQL               16898048
MySQL-client          7172590
MySQL-devel           2188430
MySQL-shared           569920
ORBit                  892530
SysVinit 172531
xVMware 10788833
X11R6-contrib 485824
XFree86 14611173
XFree86-100dpi-fonts 1258246
etc.
```

`--queryformat` 参数的语法类似于 C 语言的 `printf` 库函数。如果您不熟悉 C 语言，可能会觉得这种语法相当令人生畏，但您在 RHCE 考试中可能不需要使用它。要了解与 RPM 数据库项对应的标签，请执行以下命令：

```bash
rpm --querytags
```

一个特别有用的查询是列出软件包及其提供的能力（capabilities）。您可以使用此类查询来了解例如哪个软件包提供了 `librpm.so.0` 库：

```bash
# rpm -qp --queryformat "%{NAME}\t%{PROVIDES}\n" ➜*.rpm | \grep librpm.so.0
rpm librpm.so.0
```

单行输出显示 `rpm` 软件包提供了 `librpm.so.0` 库，正如人们预期的那样。

Red Hat Linux 6.2 及更高版本包含 `rpmdb-redhat` 软件包，其中包含一个描述发行版内容的备用 RPM 数据库。如果您安装此软件包，可以使用 `rpm` 命令的特殊 `--redhatprovides` 标志来确定哪个软件包拥有某个特定文件。这项功能在解决依赖关系时非常有用。例如，假设您尝试安装一个软件包，但收到一条错误消息，指出需要一个特定的库——比如 `libsample.so.1`。以下命令可以识别包含该缺失库的软件包：

```bash
rpm -q --redhatprovides libsample.so.1
```

## 处理源码 RPM 软件包

普通的 RPM 软件包包含二进制可执行文件。RPM 还支持源码 RPM 文件，其中包含源代码，因此在安装之前必须进行编译。您可以在 Red Hat Linux 发行版附带的辅助 CD-ROM 中找到源码 RPM；您也可以从 `ftp://contrib.redhat.com` 和其他站点下载。某些 RPM 的名称形式为：

`package-version-build.src.rpm`

如您所见，源码 RPM 的名称与二进制 RPM 的不同之处在于它以 `.src.rpm` 结尾，而不仅仅是 `.rpm`。

当您安装源码 RPM 时，其文件被安装在 `/usr/src/redhat` 目录树下，该目录树包含以下子目录：

- **BUILD**：源码 RPM 在此处解压缩、解包并打补丁。
- **RPMS**：当您编译源码 RPM 时，新的二进制 RPM 将保存在此处。该目录包含针对每个支持架构的子目录。
- **SOURCES**：源代码（通常包含在 TAR 文件中）和补丁存放于此处。
- **SPECS**：此目录包含 SPEC 文件，其中列出了与源码 RPM 相关的软件包源、补丁、编译时选项、安装后步骤和软件包信息。
- **SRPMS**：当您创建新的源码 RPM 时，它将保存在此处。

要从源码 RPM 构建二进制 RPM，请移至 SPECS 目录并执行如下形式的命令：

`rpm -bb spec_file`

其中 `spec_file` 是与源码 RPM 关联的 SPEC 文件的名称。表 12.2 描述了与源码 RPM 相关的其他有用 `rpm` 命令标志。

### 表 12.2 rpm 命令的源码文件标志

| 标志 | 含义 |
| :--- | :--- |
| -bp | %prep 阶段：解包并为源码打补丁 |
| -bl | %files 阶段：检查文件是否存在 |
| -bc | %build 阶段：执行 make install |
| -bb | 构建二进制软件包 |
| -ba | 构建二进制和源码软件包 |
| --test | 检查 SPEC 文件的语法 |

如果 SPEC 文件包含在 TAR 文件中，您不需要解包 TAR 文件。相反，请将 -b 标志替换为 -t，并指定包含 SPEC 文件的 TAR 文件。`rpm` 命令同时支持未压缩和 gzip 压缩的 TAR 文件。

您不需要安装源码 RPM 即可编译它。只需指定如下形式的命令：

```bash
rpm --recompile source_package_file
```

其中 `source_package_file` 是源码 RPM 的名称。要编译未安装的 SRPM、构建相应的二进制 RPM 并清理源文件，请执行如下形式的命令：

```bash
rpm --rebuild source_package_file
```

其中 `source_package_file` 是源码 RPM 的名称。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_320_0.png)

当前的 RHCE 指南仅要求对源码 RPM 及相关 `rpm` 命令有概念上的理解。您不需要成为处理源码 RPM 的专家。

## GnoRPM

许多桌面 Linux 用户更喜欢图形用户界面（GUI）而不是命令行用户界面（CLI）。GnoRPM 为这类用户提供了一个易于使用的工具来操作 RPM 软件包。图 12.2 展示了 GnoRPM 工具。

**图 12.2** GnoRPM 工具
![](img/4eef9c6f2f52b608eba628cf4e2793ce_321_0.png)

作为系统管理员，您可能需要在缺乏 **X** 的系统上执行软件包操作，而 **GnoRPM** 需要 **X** 才能运行。例如，假设您想在系统上安装 **X**；您不能使用需要 **X** 的 **GnoRPM** 来安装 **X**。尽管如此，您应该熟悉 **GnoRPM**，以便协助那些更喜欢使用它而不是命令行的用户。**GnoRPM** 允许您执行以下操作：

- 安装软件包
- 升级软件包
- 查询软件包
- 验证软件包
- 卸载软件包

此外，**GnoRPM** 包含一个 `rpmfind` 命令的界面，可帮助您在互联网 FTP 站点上查找存储的软件包。

您会发现 **GnoRPM** 非常易于使用。如果您需要帮助理解其更高级的功能，请参阅其文档文件，文档位于 `/usr/doc/gnorprm`。

现在您应该完成练习 12.6，该练习要求您使用 GnoRPM 移除一个软件包。

## 练习 12.6：移除软件包

普通用户通常更喜欢使用 GnoRPM 而非 RPM，但即使是系统管理员也会使用 GnoRPM 来操作软件包。本练习测试您使用 GnoRPM 移除软件包的能力。GnoRPM 的点选界面可能足够直观，以至于您不需要查阅文档。但如果您觉得 GnoRPM 令人困惑，请查阅本章中提到的文档文件。请记住，在 RHCE 考试期间您可能无法查阅文档。

1. 使用 `rpm` 命令安装 GnoRPM。
2. 使用 GnoRPM 检查几个已安装的软件包和未安装的软件包文件。

## 总结

在本章中，您学习了软件包和红帽软件包管理器 (RPM)。涵盖的最重要主题包括：

- **红帽软件包管理器 (RPM)**：RPM 帮助您安装、卸载和管理软件程序。RPM 设施由软件包文件、RPM 数据库和 `rpm` 命令组成。
- **软件包文件**：软件包文件可包括程序、配置文件和数据文件。软件包文件包含关于其内容的详细信息，包括版本和依赖信息。
- **依赖关系**：当软件包的正常运行需要外部资源时，该软件包被认为与该外部资源具有依赖关系。
- **能力 (Capabilities)**：提供另一个软件包所需资源的软件包被认为提供了一项“能力”。
- **RPM 数据库**：RPM 数据库位于 `/var/lib/rpm`，包含描述每个已安装软件包的信息。



**`rpm` 命令** `rpm` 命令`允许您执行多种操作，包括安装软件包、更新软件包、删除软件包、查询 RPM 数据库、查询软件包文件、从源代码构建软件包文件、验证软件包以及验证软件包文件。

**源码 RPM 包** 与包含二进制代码的普通 RPM 包不同，源码 RPM 包包含的是源代码。

**GnoRPM 程序** GnoRPM 为 `rpm` 命令提供了一个基于 X 的图形用户界面。

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- 构建版本号 (build number)
- 能力 (capability)
- 依赖 (dependency)
- 依赖信息 (dependency information)
- 软件包 (package)
- 软件包文件 (package files)
- 版本号 (version number)

## 其他信息来源

如果您想进一步了解本章中介绍的主题，请参考以下来源：

- Edward C. Bailey 的 *Maximum RPM* (Red Hat Press, 1997)
- `rpm` 命令的人页 (man page)
- *The Official Red Hat Linux Reference Guide*
- 由 Donnie Barnes 编写的 *RPM HOWTO* (`/usr/doc/HOWTO/RPM-HOWTO`)
- GnoRPM 的文档，`/usr/doc/gnorp*`

## 复习题

1. 以下哪个选项存储了关于 RPM 软件包的信息？
    A. 软件包文件
    B. `install` 命令
    C. `rpm` 命令
    D. RPM 数据库

2. 以下哪个命令可以卸载软件包 xyz？
    A. `rpm -e xyz`
    B. `rpm -i xyz`
    C. `rpm -u xyz`
    D. `rpm --uninstall xyz`

3. 要了解哪个软件包拥有文件 /etc/hosts，请执行命令：
    A. `rpm -qf hosts`
    B. `rpm -qf /etc/hosts`
    C. `rpm -qF hosts`
    D. `rpm -qF /etc/hosts`

4. -V 标志会导致 RPM 报告被修改的文件。如果配置文件的内容已被更改，输出中会出现以下哪个标志？
    A. 5
    B. c
    C. S
    D. T

5. 要列出每个已安装软件包的名称，请执行命令：
    A. `rpm -q` 
    B. `rpm -qa` 
    C. `rpm -qi` 
    D. `rpm -qp`

6. 为 RPM 提供图形用户界面的程序是：
    A. GoRPM 
    B. GnoRPM 
    C. GnomeRPM 
    D. GnomRPM

## 复习题答案

1. A, D。软件包文件和 RPM 数据库都存储了关于 RPM 软件包的信息。
2. A, D。`-e` 和 `--uninstall` 标志均可卸载指定的软件包。
3. B。`-qf` 标志使 RPM 报告文件的所有权；必须指定文件的完整路径。
4. A, B, D。即使文件内容发生了变化，文件大小也可能没有改变。
5. B。`-qa` 标志使 RPM 列出每个已安装软件包的名称。
6. B。GnoRPM 是为 RPM 提供图形用户界面的工具。

# 第 13 章：理解 Red Hat Linux 文件系统布局

### 本章涵盖的 RHCE 准备主题：

- 了解并理解 Red Hat Linux 文件系统布局。

一个典型的 Red Hat Linux 系统包含许多目录和文件。为了高效地管理这样一个系统，您必须知道重要文件存储在何处以及存储的是什么类型的文件。本章描述了 Red Hat Linux 的文件系统布局，该布局通常遵循文件系统层次结构标准 (File System Hierarchy Standard) 的建议。

## Red Hat Linux 文件系统

与其他 Unix 系统一样，Red Hat Linux 采用分层文件系统。文件系统的最顶层目录（称为根目录）包含其他几个目录，有时被称为子目录。这些目录反过来通常又包含子目录和文件。

目录结构并非随意而定。为了使软件包正常工作，重要文件和目录的位置必须标准化。文件系统层次结构标准将通用实践编纂成册，并为目录结构建议了改进的实践。可以通过 Web 访问文件系统层次结构标准，网址为 `pathname.com/fhs`。

虽然该标准是考虑到 Linux 系统而设计的，但它普遍适用于 Unix 系统。Linux 发行版通常遵循文件系统层次结构标准的建议。然而，该标准在某种程度上较为宽松，且存在解释空间。因此，两个都声称遵循该标准的发行版，其文件系统的结构仍可能存在显著差异。Red Hat Linux 严格遵循该标准。*Official Red Hat Linux Reference Guide* 解释了该标准以及 Red Hat Linux 如何实现该标准的建议。

本章的其余部分将描述 Red Hat Linux 系统的标准目录。

## 根目录

Linux 系统的根目录 (/) 是包含所有其他目录和文件的目录。其他目录可能会被单独挂载，因此在系统启动时可能存在，也可能不存在。因此，包含根目录的文件系统必须包含在单用户模式下运行系统所需的所有文件。根目录还包含关闭、恢复或修复系统所需的所有文件。

以下目录至关重要，必须是根文件系统的一部分：

- `/bin`，包含系统管理员和其他用户使用的二进制文件
- `/dev`，包含设备文件
- `/etc`，包含主机特定的配置数据
- `/lib`，包含系统库
- `/sbin`，包含系统管理员使用的二进制文件

启动或救援软盘的根文件系统中可能仅包含这些基本目录，而这可能是介质上包含的唯一文件系统。然而，Linux 系统通常还包括其他几个目录，这些目录可以用作非根文件系统的挂载点，或者包含驻留在根文件系统上的目录和文件。一些常用的目录包括：

- `/boot`，包含系统启动时引导加载程序所需的文件。这些文件可以放在根分区中。但是，Red Hat, Inc. 建议将它们放在单独的分区中，以克服通用 PC BIOS 对启动数据位置的限制。
- `/home`，包含用户的家目录
- `/lost+found`，包含在文件系统重建期间恢复的文件
- `/mnt`，包含临时挂载文件系统的挂载点
- `/proc`，包含系统信息
- `/root`，包含 root 用户的家目录
- `/tmp`，包含临时文件
- `/usr`，包含对基本系统操作非必要的共享文件
- `/var`，包含对基本系统操作非必要的非共享文件

## /bin：基本二进制文件

/bin 目录包含在单用户模式下运行至关重要的二进制文件。这些文件通常是命令，可由系统管理员和用户使用。不需要在单用户模式下使用的类似文件被放置在 /usr/bin 中。表 13.1 列出了 /bin 目录中的文件。其中一些文件是提供备用文件名的符号链接。例如，/bin/csh 是指向 /bin/tcsh 的符号链接。

**表 13.1 /bin 中的文件**

| | | | | |
| --- | --- | --- | --- | --- |
| arch | df | igawk | netstat | sort |
| ash | dmesg | ipcalc | nice | stty |
| ash.static | dnsdomainname | kill | nisdomainname | su |
| awk | doexec | ksh | ping | sync |
| basename | domainname | linuxconf | ps | tar |
| bash | echo | ln | pwd | tcsh |
| bash2 | ed | loadkeys | red | touch |
| bsh | egrep | login | remadmin | true |
| cat | ex | ls | rm | umount |
| chgrp | false | mail | rmdir | uname |
| chmod | fgrep | mkdir | rpm | userconf |
| chown | fsconf | mknod | rvi | usleep |
| consolechars | gawk | mktemp | rview | vi |
| cp | gawk-3.0.3 | more | sed | view |
| cpio | grep | mount | setserial | ypdomainname |
| csh | gunzip | mt | sfxload | zcat |
| date | gzip | mv | sh | zsh |
| dd | hostname | netconf | sleep | |

## /boot：引导加载程序文件

如第 2 章“硬件基础”所述，许多 PC 包含的 BIOS 代码除非引导记录存储在磁盘驱动器的给定柱面（通常为 1024）以下，否则无法加载引导记录。Red Hat 建议您将引导加载程序文件放在单独的分区中，并将该分区放在 BIOS 可访问的磁盘区域，以避免启动问题。

/boot 分区通常在其 MBR 中包含 Linux 加载程序 (LILO) 的第一阶段，位于分区的第一个柱面上。它还包含以下文件：

- LILO 的第二阶段，驻留在文件 boot.b 中
- Linux 内核，通常命名为 vmlinuz*
- 通过名称标识系统模块的模块信息
- 记录内核模块和符号位置的系统映射文件 (system map file)
- 加载程序在安装期间覆盖的磁盘区域的副本

## /dev：设备文件

Linux /dev 目录包含各种设备文件。并非每个设备文件都对应一个已安装的设备；安装脚本 (`/dev/MAKEDEV`) 会创建一组设备文件，无论相关设备是否已安装。

表 13.2 总结了一些最重要的常用设备文件。此外，还有对应于以下内容的设备文件：

- 各种鼠标（例如 `/dev/psaux`）
- 内存和 I/O 端口（例如 `/dev/mem`）
- 各种音频和多媒体设备（例如 `/dev/audio`）



- 专用串口卡（例如，`/dev/ttyC`）
- 专有 CD-ROM 驱动器（例如，`/dev/cdu31a`）

### 表 13.2 重要设备文件

| 设备文件 | 设备 |
| :--- | :--- |
| console | 系统控制台 |
| cua* | 已弃用——最初指串口 |
| fd* | 软盘驱动器 |
| hd* | IDE 硬盘或 CD-ROM |
| lp* | 并口 |
| md* | RAID 阵列 |
| null | 空输出设备 |
| ramdisk | RAM 磁盘 |
| sd* | SCSI 硬盘 |
| sr* | SCSI CD-ROM |
| st* | SCSI 磁带 |
| tpqic*, ntpqic*, rft*, nrft* | QIC 磁带 |
| tty* | 终端或伪终端 |
| ttyS* | 串口 |
| vc* | tty 设备的内容，例如虚拟控制台 |
| zero | 全二进制 0 输入设备 |

## /etc：主机特定配置文件

`/etc` 目录包含特定于本地主机的文件和目录。传统上，一些二进制文件位于 `/etc` 中；现在这些文件被移至 `/sbin` 和 `/usr/sbin`。其中一些最重要的文件和子目录分别汇总在表 13.3 和 13.4 中。

### 表 13.3 /etc 中的重要文件

| 文件 | 内容 |
| :--- | :--- |
| adjtime | 时间同步数据 |
| fdprm | 软盘参数 |
| fstab | 文件系统表 |
| gettydefs | 登录终端特性 |
| group | 用户组 |
| inittab | 系统启动配置 |
| ld.so.conf | 系统库缓存 |
| lilo.conf | Linux 加载器配置 |
| motd | 今日消息 (Message of the day) |
| mtab | 已挂载文件系统表 |
| nsswitch.conf | 用户、主机、网络和服务信息的源列表 |
| mtools.conf | mtools 工具配置 |
| passwd | 用户账户 |
| profile | Shell 初始化脚本 |
| securetty | 安全登录终端列表 |
| shadow | 用户账户加密密码（如果启用了 shadow 密码） |
| shells | 批准的 Shell 列表 |
| syslog.conf | 系统日志配置 |
| exports | NFS 导出列表 |
| ftp* | FTP 配置文件 |
| host.conf | 主机名解析配置（另见 resolv.conf） |
| hosts | 已知主机列表 |
| hosts.allow | 允许访问服务的主机列表 |
| hosts.deny | 禁止访问服务的主机列表 |
| hosts.equiv | 受信任主机列表 |
| inetd.conf | Internet 超级服务器 inetd 的配置 |
| networks | 已知网络列表 |
| printcap | 打印机配置 |
| protocols | 已知协议列表 |
| resolv.conf | 主机名解析配置（另见 host.conf） |
| rpc | RPC 服务列表 |
| services | TCP/IP 服务列表 |

### 表 13.4 /etc 的重要子目录

| 子目录 | 内容 |
| :--- | :--- |
| cron* | cron 服务配置 |
| httpd | http (Web) 服务配置 |
| pam.d | PAM（Red Hat 安全库）配置 |
| pcmcia | PCMCIA 插槽和设备配置 |
| ppp | PPP 服务配置 |
| rc.d | 系统初始化文件 |
| security | 安全配置 |
| skel | 用户环境模板文件 |
| sysconfig | 系统配置 |
| X11 | X Window 系统配置，包括 XF86Config 文件 |

## /home：用户主目录

`/home` 目录包含除 root 以外的用户主目录（root 的主目录是 `/root`）。默认情况下，用户的主目录是 `/home` 的一个子目录，其名称与用户的登录名相同。然而，特别是当系统拥有许多用户账户时，您可能希望以不同的方式构建 `/home` 目录。例如，大学可能会将学生的主目录放在 `/home/student` 下，将教职员工的主目录放在 `/home/faculty` 下，并在这些挂载点挂载磁盘卷。

## /lib：共享库和内核模块

`/lib` 目录包含启动系统以及运行位于 `/sbin` 和 `/bin` 目录中程序所需的库和模块；其他库位于 `/usr/lib`、`/usr/X11R6/lib` 等地。模块位于 `/lib/modules` 的子目录中；每个子目录根据与其关联的内核的版本和构建号命名。例如，Linux 2.2.9 内核构建版本 15 的模块可能位于 `/lib/modules/2.2.9-15`。

## /lost+found：恢复的文件

当您恢复文件系统时，文件和文件数据可能会被部分恢复。例如，恢复工具可能会恢复文件的内容但无法恢复文件名。此类文件会被工具放置在文件系统根目录的 `/lost+found` 子目录中。

## /mnt：临时挂载文件系统的挂载点

`/mnt` 目录作为一组用于临时挂载文件系统的目录的标准父目录。标准子目录包括 `cdrom`（CD-ROM 文件系统的挂载点）和 `floppy`（位于软盘上的文件的挂载点）。

## /proc：系统信息虚拟文件系统

Linux 的 `/proc` 目录是由内核提供的一个伪文件系统，其中包含允许系统管理员和程序员访问系统信息的文件和目录。`/proc` 目录中的某些信息可以通过修改来配置系统运行。

`/proc` 目录中一些最重要的文件和子目录汇总在表 13.5 中。有关 `/proc` 目录内容的更多信息，请参阅 proc 的 man 手册页。

### 表 13.5 /proc 的重要文件和子目录

| 文件或子目录 | 内容 |
| :--- | :--- |
| `[number]` | 一个包含描述与目录名 ID 相同的进程的文件和子目录的目录 |
| `cpuinfo` | 各种依赖于架构的信息 |
| devices | 主设备号和设备组 |
| dma | 正在使用的已注册 ISA DMA 通道 |
| filesystems | 内核支持的文件系统类型 |
| interrupts | 中断和 IRQ 的信息 |
| ioports | 已注册的输入/输出端口 |
| kcore | 系统物理内存内容 |
| kmsg | 内核消息日志 |
| ksyms | 内核导出的符号和定义 |
| loadavg | 运行队列中的平均作业数 |
| meminfo | 内存分配信息 |
| modules | 已加载模块列表 |
| net | 网络状态信息 |
| pci | PCI 设备配置 |
| scsi | SCSI 输入/输出系统状态 |
| self | 访问 /proc 文件系统的进程信息 |
| stat | 内核和系统统计数据 |
| sys | 内核变量，其中一些可以修改以配置内核运行 |
| uptime | 系统运行时间和空闲时间 |
| version | 正在运行的内核版本号 |

## /sbin：必要的系统二进制文件

`/sbin` 目录包含系统管理员使用的必要系统二进制文件；也就是说，*启动、关机以及在单用户模式下运行系统所需的文件*。表 13.6 列出了 `/sbin` 中最重要的文件。

### 表 13.6 /sbin 中的文件

| | | | | |
|---|---|---|---|---|
| accton | getty | ksyms | netreport | rpcdebug |
| adjtimex | halt | ldconfig | nwmsg | rrestore |
| arp | hdparm | lilo | pam_filter | runlevel |
| askrunlevel | hwclock | loglevel | pcinitrd | sash |
| badblocks | ifconfig | losetup | pidof | scsi_info |
| cardctl | ifdown | lsmod | plipconfig | service |
| cardmgr | ifport | lspci | pnpdump | setpcpi |
| cfdisk | ifup | mailconf | portmap | setsysfont |
| chkconfig | ifuser | mgetty | poweroff | sfdisk |
| clock | init | mingetty | probe | shapecfg |
| ctrlaltdel | initlog | minilogd | pump | shutdown |
| debugfs | insmod | mkbootdisk | pwdb_chkpwd | slttach |
| depmod | insmod.static | mkdosfs | quotacheck | sln |
| dhcpcd | install-info | mke2fs | quotaoff | stinit |
| dnsconf | installkernel | mkfs | quotaon | sulogin |
| dump | ipchains | mkfs.ext2 | raidhotadd | swapoff |
| dumpe2fs | ipchains-restore | mkfs.minix | raidhotremove | swapon |
| e2fsck | ipchains-save | mkfs.msdos | raidstart | telinit |

## 表 13.6 /sbin 中的文件（接上页）

| | | | | |
|---|---|---|---|---|
| e2label | ipfwadm-wrapper | mkinitrd | raidstop | tune2fs |
| fdisk | ipmaddr | mkpv | rarp | update |
| fixperm | iptunnel | mkraid | rdump | ugetty |
| fsck | ipx_configure | mkswap | reboot | vgetty |
| fsck.ext2 | ipx_internal_net | modinfo | restore | ypbind |
| fsck.minix | isapnp | modprobe | rrmod | |
| ftl_check | kbdate | mount_ncp | rrmod.static | |
| ftl_format | kerneld | mount.ncpfs | rmt | |
| gensyms | killalls | | route | |

## /tmp：临时文件

`/tmp` 目录包含临时文件和子目录，当这些文件在指定时间段内（默认 10 天）未被使用时，会被 `tmpwatch` 工具自动删除。

## /usr：可共享文件

`/usr` 文件系统可能不可用，因此它不包含系统运行所必需的文件或目录。系统的正常运行不需要修改 `/usr` 中的文件，因此其内容是可共享的；例如，`/usr` 分区通常是一个驻留在远程系统上的 NFS 导出分区。表 13.7 总结了 `/usr` 的一些重要子目录。

### 表 13.7 /usr 的重要子目录

| 子目录 | 内容 |
|---|---|
| /usr/X11R6 | X Window 系统二进制文件 |
| /usr/bin | 普通用户使用的命令 |
| /usr/dict | 字典 |
| /usr/doc | 文档 |
| /usr/games | 游戏相关二进制文件 |
| /usr/include | 头文件 |
| /usr/info | Texinfo 文档文件 |
| /usr/lib | 编程库 |
| /usr/local | 不属于操作系统的本地文件 |
| /usr/man | Man 手册页 |
| /usr/sbin | 不需要用于启动、关机或以单用户模式运行系统的系统二进制文件 |
| /usr/share | 与架构无关的文件 |
| /usr/src | 源代码 |

## /var：不可共享文件

与 `/usr` 文件系统类似，`/var` 文件系统可能不可用，因此它不包含必需的文件或目录。但与 `/usr` 不同的是，`/var` 包含在系统运行期间会被修改的文件——例如日志文件。表 13.8 总结了 `/var` 的重要子目录。

### 表 13.8 /var 的重要子目录

| 子目录 | 内容 |
|---|---|
| /var/cache | 应用程序缓存文件 |
| /var/lock | 锁文件 |
| /var/log | 日志和计费文件 |
| /var/run | 系统信息文件 |
| /var/spool | Spool 文件，包括 cron、lpd 和 sendmail 的文件 |
| /var/tmp | 临时文件 |
| /var/yp | NIS 文件 |

## 总结

在本章中，您了解了 Red Hat Linux 的文件系统布局。涵盖的最重要主题包括：

- **文件系统层次结构标准 (FHS)** 文件系统层次结构标准规定了重要 Linux 目录的标准位置和内容。
- **根目录 (/)** 根目录包含所有其他目录。
- **/bin 目录** `/bin` 目录包含系统管理员和普通用户使用的基本二进制文件。
- **/boot 目录** `/boot` 目录包含启动 Linux 所需的文件以及有助于调试内核的文件。相关文件系统存储在通常包含 LILO 的分区中，用于启动 Linux。
- **/dev 目录** `/dev` 目录包含与硬件设备相对应的特殊文件。
- **/etc 目录** `/etc` 目录包含内容针对本地主机的文件和目录，特别是配置信息。
- **/home 目录** `/home` 目录通常包含用户的家目录。
- **/lib 目录** `/lib` 目录包含库文件和可加载模块。
- **/lost+found 目录** `/lost+found` 目录包含由文件系统工具恢复（或部分恢复）的文件。
- **/mnt 目录** `/mnt` 目录为文件系统提供标准的挂载点。
- **/proc 目录** `/proc` 目录是一个伪文件系统的根目录，允许您查看和修改系统信息。
- **/sbin 目录** `/sbin` 目录包含主要由系统管理员使用的基本二进制文件。
- **/tmp 目录** `/tmp` 目录包含临时文件，如果在指定期间内未被使用，这些文件将被自动删除。
- **/usr 目录** `/usr` 目录包含各种非必需目录。
- **/var 目录** `/var` 目录包含在系统运行期间被修改的不可共享文件。

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- 设备文件 (device file)
- 临时文件 (temporary file)

## 额外信息来源

如果您想进一步了解本章介绍的主题，可以参考以下资源：

- *《Red Hat Linux 官方参考指南》*
- *《文件系统层次结构标准》*，`www.pathname.com/fhs`
- 文件 `/usr/doc/kernel-doc`/proc.txt，其中解释了 `/proc` 文件系统

## 复习题

1. 以下哪些是必需的系统目录？
    A. /bin
    B. /etc
    C. /usr/bin
    D. /var/log

2. 包含 Linux 内核的默认目录是什么？
    A. /
    B. /boot
    C. /dev
    D. /sbin

3. 哪个文件包含系统启动信息？
    A. /etc/inetd.conf
    B. /etc/inittab
    C. /usr/etc/inetd.conf
    D. /usr/etc/inittab

4. 以下哪个目录可能是登录名为 red 的用户的家目录？
    A. /home/chicago/red
    B. /home/red
    C. /home/staff/red
    D. /home/swingshift/red

5. 以下哪个文件对应于系统控制台？
    A. /dev/console
    B. /dev/operator
    C. /dev/ttyS1
    D. /dev/vc1

6. 以下哪个目录包含编译 Linux 内核所需的 C 头文件？
    A. /usr/c
    B. /usr/header
    C. /usr/include
    D. /usr/src/header

## 复习题答案

1. A, B。`/usr` 和 `/var` 文件系统是非必需的。
2. B。Linux 内核驻留在 `/boot` 目录中。
3. B。系统启动信息驻留在 `/etc/inittab` 中。
4. A, B, C, D。系统管理员几乎可以以任何方式构建 `/home` 目录。
5. A。系统控制台被称为 `/dev/console`。
6. C。`/usr/include` 目录包含 C 头文件。

# 第 14 章：系统初始化

**本章涵盖的 RHCE 准备主题：**

- 熟悉并能够配置系统初始化脚本。

当 Red Hat Linux 启动时，它会自动执行各种检查，然后启动指定的服务。Red Hat Linux 管理员必须能够配置执行哪些检查以及启动哪些服务。深入了解系统初始化对于系统故障排除和恢复也至关重要。本章将解释系统初始化脚本以及您可以用来配置这些脚本的几种工具。

## 系统初始化

Red Hat Linux 通常遵循 AT&T SysV Unix 引入的系统初始化程序。当 Red Hat Linux 系统启动时，系统会执行两个主要脚本：

- /etc/rc.d/rc.sysinit
- /etc/rc.d/rc

基本上，`/etc/rc.d/rc.sysinit` 脚本初始化文件系统和设备。这是一个调用许多命令的大型脚本。如果存在 `/etc/rc.d/rc.serial` 脚本，它也会调用该脚本。`/etc/rc.d/rc.serial` 脚本用于初始化串口；当需要执行特殊初始化时使用——例如，安装了多口串口卡时。

基本上，`/etc/rc.d/rc` 脚本初始化服务。它在系统启动时以及每次系统运行级别更改时被调用。它会调用一组相应的运行级别脚本，用以启动和停止设施与服务。在系统启动时，它会在所有其他运行级别脚本执行完毕后调用 `/etc/rc.d/rc.local` 脚本。`/etc/rc.d/rc.local` 脚本的内容是本地定义的；您可以使用它来执行特殊的初始化操作。



系统初始化脚本可能会记录错误消息。如果系统未能正常启动，您应该检查 `/var/log/messages` 以查找相关的错误消息。

本章的其余部分将更详细地解释了这些脚本及其运行方式。它们还将解释如何配置在给定运行级别下运行的服务。

## /etc/rc.d/rc.sysinit 脚本

如前所述，`/etc/rc.d/rc.sysinit` 脚本负责初始化文件系统和设备。它还执行其他若干操作。以下是该脚本执行操作的指南；它可以：

- 检查是否存在 `/etc/sysconfig/network` 脚本，该脚本设置描述网络配置的环境变量。如果 `/etc/sysconfig/network` 脚本存在，则执行它；否则，设置关闭网络并将主机名设置为 localhost 的环境变量。
- 引入 (Source) 文件 `/etc/rc.d/init.d/functions`，其中包含一组 shell 函数。这些函数被 `/etc/rc.d/init.d` 目录中的脚本调用。包含的函数有：
    - 启动程序
    - 停止程序
    - 查找程序的进程 ID
    - 显示程序状态
    - 显示有助于跟踪程序启动的成功和失败消息
    - 记录启动、关机、错误和其他消息
    - 请求对敏感操作的确认
- 显示欢迎横幅，其中包含交互式启动的提示
- 设置日志记录级别。
- 挂载 `/proc` 文件系统，使用 `sysctl` 配置内核参数，并设置系统时钟。
- 如果 `/etc/sysconfig/console/default.kmap` 存在，则加载默认键盘映射表；否则加载 `/etc/sysconfig/keyboard` 中指定的键盘映射表。
- 运行 `/sbin/setsysfont` 脚本，该脚本设置默认系统字体。
- 激活 `/etc/fstab` 中指定的交换分区。
- 设置主机名和 NIS 域名（如果适用）。
- 以只读模式重新挂载根文件系统，并在根文件系统出现问题时检查其状态。如果发现严重错误，脚本将启动一个 shell，允许您尝试修复损坏的文件系统。
- 设置已配置的 ISA 即插即用设备。
- 以读写模式重新挂载根文件系统。
- 检查根文件系统上的磁盘配额。
- 设置 `/etc/mtab`（列出已挂载的文件系统）和 `/etc/HOSTNAME`（标识主机）。
- 设置对可加载内核模块的支持。
- 如果 `/etc/conf.modules` 中指定了声卡，则加载声音模块；如果 `/etc/conf.modules` 中指定了 MIDI 接口，则加载 MIDI 模块。
- 加载 `/etc/raidtab` 中指定的 RAID 设备。
- 检查非根文件系统。如果发现严重错误，脚本将启动一个 shell，允许您尝试修复损坏的文件系统。否则，脚本检查非根文件系统上的磁盘配额，并将 `/etc/fstab` 中指定为自动可挂载的文件系统进行挂载。如果安装了磁盘配额软件包，则开启磁盘配额检查。
- 删除各种不需要的临时文件，例如锁文件。
- 如果 `/etc/rc.d/rc.serial` 脚本存在，则通过运行该脚本来初始化串口。`/etc/rc.d/rc.serial` 脚本通常包含用于配置串口设备的 `setserial` 命令。通常不需要配置标准 PC 串口，包含此项主要是为了与旧版本 Linux 兼容。
- 如果存在 SCSI 磁带驱动器，则加载 SCSI 磁带模块。
- 在某些情况下，创建头文件 `/boot/kernel.h`。
- 为 `/boot/System.map-kernel_version` 创建符号链接。
- 将启动消息复制到 `/var/log/dmesg`，以便可以使用 `dmesg` 命令读取。

在系统启动期间，init 进程调用 `/etc/rc.d/rc.sysinit`，然后调用 `/etc/rc.d/rc`。第 15 章详细描述了这一过程。为了准备 RHCE 考试，您通常应该熟悉 `/etc/rc.d/rc.sysinit` 脚本执行的步骤。现在您已经浏览了 `/etc/rc.d/rc.sysinit` 脚本，请完成练习 14.1，该练习要求您更详细地研究此脚本。

### 练习 14.1：/etc/rc.d/rc.sysinit 脚本

1. 理解 `/etc/rc.d/rc.sysinit` 脚本有助于解决各种系统启动问题。为了进一步了解该脚本，请检查它并找到本节中确定的每项操作是在何处执行的。
2. 该脚本还执行了一些不太重要的操作。请查找并识别这些操作。

## /etc/rc.d/rc 脚本

`/etc/rc.d/rc` 脚本设置一个新的运行级别，然后运行一系列与指定运行级别相关的脚本。这些脚本包含在以下目录中：

- /etc/rc.d/rc0.d
- /etc/rc.d/rc1.d
- /etc/rc.d/rc2.d
- /etc/rc.d/rc3.d
- /etc/rc.d/rc4.d
- /etc/rc.d/rc5.d
- /etc/rc.d/rc6.d

每个目录的名称与相关运行级别的名称相对应。表 14.1 总结了 Red Hat Linux 使用的运行级别。

### 表 14.1 运行级别摘要

| 运行级别 | 描述 |
|---|---|
| 0 | 系统停止 |
| 1 | 单用户模式 |
| 2 | 多用户模式，无 NFS |
| 3 | 全多用户模式 |
| 4 | 未使用 |
| 5 | 全多用户模式，带 X-based 登录 |
| 6 | 系统重启 |

### 运行级别脚本

每个 /etc/rc.d/rc?.d 子目录包含一系列指向 /etc/rc.d/init.d 目录中脚本的符号链接，这些脚本被称为“运行级别脚本”。用于启动和停止系统服务的最常见运行级别脚本汇总在表 14.2 中。如果您安装了可选软件包，除了表 14.2 中描述的脚本外，您可能还会发现其他脚本。使用符号链接引用脚本的目的是让多个符号链接可以指向同一个脚本文件。如果脚本需要修改，只需更改一个文件即可，这比更改多个文件更方便且更不容易出错。

### 表 14.2 常见运行级别脚本描述

| 脚本 | 描述 |
| :--- | :--- |
| anacron | 在指定的时间间隔运行命令；与 crond 不同，它不假设系统是连续运行的。 |
| apmd | 高级电源管理服务，用于监控电池电量。 |
| atd | AT 服务器，处理通过 at 命令指定的命令。 |
| autofs | 自动挂载文件系统。 |
| crond | CRON 服务器，在用户指定的时间间隔运行命令。 |
| gpm | 文本模式程序的鼠标支持。 |
| halt | 重启或停止系统。 |
| httpd | Apache Web 服务器。 |
| inet | 各种基础 TCP/IP 服务；在 inetd 的控制下运行。 |
| keytable | 加载键盘映射表。 |
| killall | 杀死运行中的服务。 |
| kudzu | 在启动时检查硬件变更。 |
| linuxconf | 一个钩子，允许 linuxconf 在系统启动和关闭时执行指定操作。 |
| local | /etc/rc.d/rc.local 脚本，包含本地指定的内容。 |
| lpd | LP 服务，提供对远程打印机的访问。 |
| named | DNS 服务器，提供主机名和 IP 地址查询。 |
| netfs | 挂载网络文件系统。 |
| network | 激活和禁用网络接口。 |
| nfs | 网络文件系统 (NFS) 服务器，提供文件共享。 |
| pcmcia | 激活和禁用 PCMCIA 支持。 |
| portmap | 管理 RPC 连接，例如被 NFS 和 NIS 使用。 |
| postgresql | 数据库管理系统。 |
| random | 保存和恢复随机数生成器的状态，以产生质量更好的随机数。 |
| reboot | 指向 halt 脚本的符号链接。 |
| routed | RIP 客户端和服务器，自动更新路由。 |
| rstatd | RSTAT 服务器，提供性能指标。 |
| rusersd | RUSERS 服务器，帮助定位用户。 |
| rwhod | RWHO 服务器，列出已登录用户。 |
| sendmail | 邮件服务器。 |
| single | 将系统置于单用户模式。 |
| smb | Samba (SMB) 服务器，提供身份验证以及文件和打印机共享。 |
| sound | 保存和恢复声卡混音设置。 |
| sshd | SSH 服务器，提供安全登录和远程命令执行。 |
| syslog | 启动和停止系统日志记录。 |
| xfs | X Window 系统的字体服务器。 |



既然你已经熟悉了最常见的运行级别脚本，请完成练习 14.2 以进一步学习。

### 练习 14.2：运行级别脚本

大多数 Linux 系统还使用了表 14.2 中未列出的其他脚本。要了解安装在你的系统上的脚本，请检查 `/etc/rc.d/init.d` 目录，并识别出任何未在表 14.2 中出现的脚本。检查这些脚本的内容以了解它们的功能。大多数脚本都包含解释其功能的注释。

大多数脚本都接受控制其运行的参数。最常见的参数是：

- start，使脚本启动相关服务
- stop，使脚本停止相关服务
- restart，使脚本重启相关服务
- reload，使脚本重新读取其配置文件
- status，使脚本报告相关服务的状态

`linuxconf` 程序使用这些脚本来启动和停止服务。你也可以手动调用它们来控制服务。例如，你可以通过执行以下命令来关闭 Web 服务器（httpd 服务）：

```
/etc/rc.d/init.d/httpd stop
```

或者，你可以通过执行以下命令来重启服务器：

```
/etc/rc.d/init.d/httpd restart
```

使用 `/etc/rc.d/init.d` 中的脚本而不是通过其他方式控制服务是非常重要的。例如，可以通过执行命令 `/usr/sbin/httpd` 来启动 Web 服务器。然而，如果你这样做，当你关闭服务时，Linux 将无法清理锁定文件和进程标识文件。更糟糕的是，除非使用运行级别脚本，否则你可能会无意中启动该服务器的多个实例。

## /etc/rc.d/rc?.d 中的符号链接

`/etc/rc.d/rc?.d` 中的符号链接名称类似于 K05keytable 和 S40atd。名称以 K 开头的链接在被 `/etc/rc.d/rc` 执行时会被传递 stop 参数；名称以 S 开头的链接则会被传递 start 参数。通常，与给定运行级别相关的目录将为每个安装的服务包含一个 K 脚本或一个 S 脚本。

脚本名称中的两位数字称为优先级（priority），它表示给定目录中脚本运行的顺序；例如，脚本 K10xfs 在脚本 K15gpm 之前运行。表 14.3 根据执行时所在的运行级别总结了常见的运行级别脚本。

### 表 14.3 按运行级别划分的常见运行级别脚本总结

| 脚本 | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| K00linuxconf | X | X | | | | | X |
| K05keytable | X | X | | | | | X |
| K10xfs | X | X | | | | | X |
| K15gpm | X | X | | X | X | X | X |
| K15httpd | X | X | X | X | X | X | X |
| K15sound | X | X | X | | | | X |
| K20nfs | X | X | X | | | | X |
| K20rstatd | X | X | X | X | X | X | X |
| K20usersd | X | X | X | X | X | X | X |
| K20rhod | X | X | X | X | X | X | X |
| K30sendmail | X | X | | X | X | X | X |
| K35smb | | | | X | | X | |
| K45named | X | X | X | | | | X |
| K45sshd | X | X | X | | | | X |
| K50inet | X | | X | X | | | X |
| K55routed | X | X | X | X | X | X | X |
| K60atd | X | X | X | | | | X |
| K60crond | X | X | | | | | X |
| K60lpd | X | X | | | | | X |
| K80random | X | | | | | | X |
| K85netfs | X | X | X | | | | X |
| K89portmap | X | X | X | | | | X |
| K90killall | X | | | | | | X |
| K90mysql | X | X | | | | | X |
| K90network | X | X | | | | | X |
| K92apmd | X | X | | X | X | X | X |
| K96pcmcia | X | X | | X | X | X | X |
| K99syslog | X | X | | | | | X |
| S00halt | X | | | | | | |
| S00single | | X | | | | | |
| S00reboot | | | | | | | X |
| S05apmd | | | X | | | | |
| S10network | | | X | X | X | X | |
| S11portmap | | | | X | X | X | |
| S15netfs | | | | X | X | X | |
| S20random | | X | X | X | X | X | |
| S30syslog | | | X | X | X | X | |
| S40atd | | | | X | X | X | |
| S40crond | | | X | X | X | X | |
| S45pcmcia | | | X | | | | |
| S50inet | | | | X | X | X | |
| S55named | | | | X | X | X | |
| S55sshd | | | | X | X | X | |
| S60lpd | | | X | X | X | X | |
| S60nfs | | | | X | X | X | |
| S75keytable | | | X | X | X | X | |
| S85sound | | | X | X | X | X | |
| S85gpm | | | X | | | | |
| S90mysql | | | X | X | X | X | |
| S90xfs | | | X | | X | X | |
| S90xfs | | | | X | | | |
| S99linuxconf | | | X | X | X | X | |
| S99local | | | X | X | | X | |

当运行级别脚本终止时，它会报告完成状态。完成状态的可能值为：

- OK，表示脚本成功启动了相关服务
- Passed，表示脚本遇到了错误，但能够恢复并成功启动相关服务
- Failed，表示脚本无法启动相关服务

完成值在系统启动期间显示在控制台上。

## /etc/rc.d/rc 脚本的运行机制

如前所述，`/etc/rc.d/rc` 脚本设置指定的运行级别，并调用适用于指定新运行级别的运行级别脚本。以下是它执行操作的详细分步指南：

1. 加载（Source）文件 `/etc/rc.d/init.d/functions`，其中包含一组 shell 函数。这些函数被 `/etc/rc.d/init.d` 目录中的脚本使用。
2. 确定当前运行级别和之前的运行级别。
3. 检查并记录是否设置了用户确认模式。
4. 将运行级别设置为指定值。
5. 将当前运行级别告知 `linuxconf`。
6. 查找 `/rc/rc.d/rcn.d` 目录，其中 *n* 是新运行级别。
7. 为每个正在运行的服务运行 `kill` 脚本。
8. 为每个尚未运行的服务运行 `start` 脚本。

在系统启动期间，init 进程在完成 `/etc/rc.d/rc.sysinit` 之后，根据 `/etc/inittab` 文件的配置调用 `/etc/rc.d/rc`。第 15 章详细描述了这一过程。

## 将服务与运行级别关联

原则上，你可以通过在 `/etc/rc.d/rc?.d` 目录中创建和操作符号链接来将服务与其运行级别关联。然而，由于这种过程既繁琐又容易出错，因此提供了几种实用程序来简化该任务。其中包括：

- chkconfig，一个命令行实用程序
- ksysv，一个基于 KDE 的实用程序
- ntsysv，一个文本模式图形实用程序
- tksysv，一个基于 X 的实用程序

在这些工具中，最重要的是 `chkconfig`；其他工具需要诸如 X 之类的支持，而在配置服务时这些支持可能不可用。`chkconfig` 工具允许你：

- 列出已安装的服务
- 添加服务
- 删除服务
- 将服务与运行级别关联

### 列出服务

要列出已安装的服务及其关联的运行级别，请执行命令：

```bash
chkconfig --list
```

输出将类似于以下内容：

```
httpd 0:off 1:off 2:off 3:off 4:off 5:off 6:off
apmd 0:off 1:off 2:on 3:off 4:off 5:off 6:off
atd 0:off 1:off 2:off 3:on 4:on 5:on 6:off
named 0:off 1:off 2:off 3:on 4:on 5:on 6:off
keytable 0:off 1:off 2:on 3:on 4:on 5:on 6:off
gpm 0:off 1:off 2:on 3:off 4:off 5:off 6:off
netfs 0:off 1:off 2:off 3:on 4:on 5:on 6:off
network 0:off 1:off 2:on 3:on 4:on 5:on 6:off
random 0:off 1:on 2:on 3:on 4:on 5:on 6:off
pcmcia 0:off 1:off 2:on 3:off 4:off 5:off 6:off
nfs 0:off 1:off 2:off 3:on 4:on 5:on 6:off
linuxconf 0:off 1:off 2:on 3:on 4:on 5:on 6:off
lpd 0:off 1:off 2:on 3:on 4:on 5:on 6:off
inet 0:off 1:off 2:off 3:on 4:on 5:on 6:off
portmap 0:off 1:off 2:off 3:on 4:on 5:on 6:off
sound 0:off 1:off 2:off 3:on 4:on 5:on 6:off
routed 0:off 1:off 2:off 3:off 4:off 5:off 6:off
rstatd 0:off 1:off 2:off 3:off 4:off 5:off 6:off
rusersd 0:off 1:off 2:off 3:off 4:off 5:off 6:off
rhwod 0:off 1:off 2:off 3:off 4:off 5:off 6:off
smb 0:off 1:off 2:off 3:off 4:off 5:off 6:off
sendmail 0:off 1:off 2:on 3:off 4:off 5:off 6:off
syslog 0:off 1:off 2:on 3:on 4:on 5:on 6:off
crond 0:off 1:off 2:on 3:on 4:on 5:on 6:off
xfs 0:off 1:off 2:on 3:on 4:on 5:on 6:off
ypbind 0:off 1:off 2:off 3:off 4:off 5:off 6:off
sshd 0:off 1:off 2:off 3:on 4:on 5:on 6:off
mysql 0:off 1:off 2:on 3:on 4:on 5:on 6:off
```

每个服务被列出，后面跟着它在每个可能运行级别下的状态。你可能会发现执行以下命令更方便，该命令将按服务名称对输出进行排序：

```bash
chkconfig --list | sort
```

### 添加服务

要添加服务，首先必须确保相关的 init.d 脚本包含特殊的注释。第一个注释是一行，告诉 `chkconfig` 该服务应在哪些运行级别启动，以及启动和停止的优先级数字。该注释行包含标记 `# chkconfig:`，然后列出运行级别。例如，以下注释指定某服务在运行级别 2 和 5 运行，启动优先级为 20，停止优先级为 80：

```
# chkconfig: 25 20 80
```

第二个注释由一行或多行组成，用于描述该服务。除最后一行外，每行必须以反斜杠 (`\`) 结尾，它是注释的续行符。例如，这是一个描述 random 服务的典型注释：

```
# description: Saves and restores system entropy pool for \
```



更高质量的随机数生成。

要添加服务，请执行以下命令：

```bash
chkconfig --add name
```

其中 *name* 是服务的名称。`chkconfig` 程序会根据 `init.d` 脚本中的注释创建所需的符号链接。

### 删除服务

要删除服务，请执行以下命令：

```bash
chkconfig --del name
```

其中 *name* 是服务的名称。`chkconfig` 程序将删除相关的符号链接。

## 将服务与运行级别关联

要将服务与一个或多个运行级别关联，请执行以下命令：

```bash
chkconfig name reset
```

其中 *name* 是服务的名称。`chkconfig` 程序会根据 `init.d` 脚本中的注释创建所需的符号链接。如果您愿意，也可以显式地设置服务在特定级别运行或不运行，而无需考虑相关 `init.d` 脚本的内容。要指定服务应该运行的级别，请执行以下命令：

```bash
chkconfig --level levels name on
```

其中 *name* 是服务的名称，*levels* 是一系列指定运行级别的数字。例如，以下命令：

```bash
chkconfig --level 35 lunch on
```

指定 `lunch` 服务将在级别 3 和 5 运行。

要指定服务不应该运行的级别，请执行以下命令：

```bash
chkconfig --level levels name off
```

其中 *name* 是服务的名称，*levels* 是一系列指定运行级别的数字。例如，以下命令：

```bash
chkconfig --level 24 lunch off
```

指定 lunch 服务在级别 2 和 4 不运行。

现在，尝试练习 14.3，该练习要求您使用 chkconfig。

### 练习 14.3：将服务与运行级别关联

RHCE 考试可能会要求您配置服务在指定级别运行。请执行以下操作以验证您的能力：

- 1. 使用 chkconfig 确定哪些服务在哪些运行级别运行。
- 2. 使用安装了 Apache 的系统，将 httpd 服务配置为仅在运行级别 5 运行。
- 3. 使用 init 命令更改当前运行级别，以便验证您的更改是否成功。

如果需要，可以回顾本章内容，但请准备好在 RHCE 考试期间在没有帮助的情况下使用 chkconfig。

## /etc/rc.d/rc.local 脚本

`/etc/rc.d/rc.local` 脚本是一个特殊的脚本，由与运行级别 2、3 和 5 相关联的目录中的符号链接运行。其启动优先级为 99，这意味着它在所有其他运行级别脚本之后运行。默认情况下，它创建：

- `/etc/issue` 文件
- `/etc/issue.net` 文件

当用户使用本地控制台登录时，会显示 `/etc/issue` 文件。默认情况下，该文件报告 Red Hat Linux 的发行版本和内核版本：

```
Red Hat Linux release 6.0 (Hedwig)
Kernel 2.2.5-15 on an i686
```

当用户使用远程控制台登录（例如，通过启动 Telnet 会话）时，会显示 `/etc/issue.net` 文件。默认情况下，该文件报告 Red Hat Linux 的发行版本和内核版本：

```
Red Hat Linux release 6.0 (Hedwig)
Kernel 2.2.5-15 on an i686
```

修改 `/etc/issue.net` 的内容被认为是一种良好的做法，这样潜在的黑客可以获得关于您系统的更少信息。您可能还希望显示一个横幅，声明系统使用的任何限制。

您可以轻松地修改 `/etc/rc.d/rc.local` 脚本，以便在 `/etc/issue.net` 中放入不同的消息，或执行其他特定于主机的初始化。由于该脚本最后执行，因此当脚本执行时，与当前运行级别相关的所有其他系统服务都应该是可运行状态。

要了解更多关于 `rc.local` 脚本的信息，请完成练习 14.4。

### 练习 14.4：/etc/rc.d/rc.local 脚本

系统管理员经常修改 `rc.local` 脚本以自定义系统启动。要了解更多关于系统启动的信息，请检查一个已配置的 Red Hat Linux 系统的 `/etc/rc.d/rc.local` 脚本，看看系统管理员对该脚本做了哪些修改（如果有）。

## 总结

在本章中，您学习了系统初始化。涵盖的最重要主题是：

- **系统初始化** 当系统启动时，它运行脚本 `/etc/rc.d/rc.d/rc.sysinit`（初始化文件系统和设备），然后运行脚本 `/etc/rc.d/rc.d/rc`（初始化服务）。
- ** /etc/rc.d/rc.d/rc.sysinit 脚本** `/etc/rc.d/rc.sysinit` 脚本执行约二十项操作，范围从设置网络到保存启动日志。
- ** /etc/rc.d/rc 脚本** `/etc/rc.d/rc` 脚本运行一系列与默认运行级别相关的脚本。这些脚本由位于 `/etc/rc.d/rc?.d` 目录中的符号链接指向，其中 `?` 是默认运行级别。
- **运行级别** Red Hat Linux 定义了七个运行级别，编号从 0 到 6。系统运行通常在运行级别 3 或 5 下进行。其他级别对于故障排除和修复很有用。
- **运行级别脚本** 运行级别脚本位于 `/etc/rc.d/init.d`。它们通常接受 `start`、`stop`、`restart` 和 `status` 参数。
- **运行级别脚本的符号链接** 运行级别脚本的符号链接名称形式为 `XNNService`，其中 `X` 的值为 K 或 S，`NN` 决定脚本运行的顺序，`Service` 指定相关服务。K 脚本用于停止服务，S 脚本用于启动服务。
- **函数** 脚本 `/etc/rc.d/init.d/functions` 包含几个有用的函数。该文件被其他运行级别脚本调用（sourced）。
- **配置服务** 您可以使用几种实用程序将服务与运行级别关联，包括 `chkconfig`、`ksysv`、`ntsysv` 和 `tksysv`。
- ** `/etc/rc.d/rc.local` 脚本** `/etc/rc.d/rc.local` 脚本用于执行本地指定的初始化操作。

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- Priority（优先级）
- Runlevel（运行级别）
- Runlevel script（运行级别脚本）

## 其他信息源

如果您想进一步了解本章介绍的主题，请参考 *《The Official Red Hat Linux Reference Guide》*。

## 复习题

- 1. 以下哪个文件系统最先被挂载？
    A. 非根文件系统，只读模式
    B. 非根文件系统，读写模式
    C. 根文件系统，只读模式
    D. 根文件系统，读写模式

- 2. 哪个脚本调用运行级别脚本？
    A. `/etc/rc.d/rc`
    B. `/etc/rc.d/rc.local`
    C. `/etc/rc.d/rc.serial`
    D. `/etc/rc.d/rc.sysinit`

- 3. 如果以下所有脚本都在同一个目录下，哪个脚本会最先执行？
    A. `K05alpha`
    B. `K10beta`
    C. `S01delta`
    D. `S05gamma`

- 4. 要查看与服务 `grub` 关联的运行级别，必须执行哪个命令？
    A. `chkconfig`
    B. `chkconfig grub`
    C. `chkconfig --grub`
    D. `chkconfig --list`

- 5. 以下哪个工具只能在 X 窗口系统下使用？
    A. chkconfig
    B. ksysv
    C. ntsysv
    D. tksysv

- 6. 要更改 /etc/issue.net 中的信息，应该修改哪个文件？
    A. /etc/rc.d/rc
    B. /etc/rc.d/rc.local
    C. /etc/rc.d/rc.serial
    D. /etc/rc.d/rc.sysinit

## 复习题答案

- 1. C. 系统首先以只读模式挂载根文件系统；随后，它以读写模式挂载所有文件系统。
- 2. A. rc 脚本调用 /etc/rc.d/rc?.d 目录中的脚本。
- 3. A. Kill 脚本在 Start 脚本之前执行；在同一类型中，脚本按优先级执行。
- 4. D. --list 命令使 chkconfig 列出服务及其关联的运行级别。
- 5. B, D. ksysv 程序需要 X。tksysv 程序使用 TK 控件集且仅在 X 下运行。
- 6. B. rc.local 文件构建 /etc/issue.net 文件。



# 第 15 章：理解配置文件和脚本

### 本章涵盖的 RHCE 准备主题：

- 理解 `/etc/sysconfig` 目录下脚本和配置文件的作用。
- `/etc/sysconfig/network-scripts` 目录下脚本和配置文件的作用。
- 理解包括声卡在内的即插即用（Plug-and-Play）卡的配置方式。
- `/etc/inittab` 的作用和内容。
- `/etc/fstab` 的作用和内容。

除了 AT&T SysV Unix 风格的启动脚本外，Red Hat Linux 在系统初始化期间还使用另外几组脚本。本章将描述这些脚本，并解释如何使用它们来配置系统启动。

## /etc/sysconfig 网络文件和脚本

当 `/etc/rc.d/init.d/network` 网络启动脚本运行时，它会启动配置的网络接口设备。它通过调用存储在 `/etc/sysconfig/network-scripts` 目录中的一组脚本来实现。表 15.1 总结了这些脚本，除了启动网络接口外，它们还可以执行多种操作。

**表 15.1 /etc/sysconfig/network-scripts 中的脚本**

| 脚本 | 描述 |
|---|---|
| chat-* | 用于 PPP 和 SLIP 连接的聊天脚本 |
| ifcfg-* | 存储相关接口的配置；例如，ifcfg-eth0 存储第一个以太网卡的配置，ifcfg-lo 存储 TCP/IP 虚拟回环设备的配置 |
| ifdhcp-done | 如果使用 DHCP，则配置 /etc/resolv.conf |
| ifdown-* | 关闭相关协议；例如，ifdown-ppp 关闭 PPP |
| ifdown-post | 关闭指定的设备 |
| ifup-* | 启动相关协议；例如，ifup-ppp 启动 PPP |
| ifup-aliases | 为指定设备添加 IP 别名 |
| ifup-post | 启动指定设备，添加静态路由和别名并设置主机名 |
| ifup-routes | 为指定设备添加静态路由 |

### ifcfg-* 脚本

每个 `ifcfg-*` 脚本存储一个网络接口的配置。`/sbin/ifup` 和 `/sbin/ifdown` 脚本分别使用这些配置脚本来启动或关闭接口。例如，具有以太网网络接口的系统将把接口配置存储在 `/etc/sysconfig/network-scripts/ifcfg-eth0` 中；如果系统有第二个以太网网络接口，则接口配置将存储在 `/etc/sysconfig/network-scripts/ifcfg-eth1` 中，依此类推。要启动第一个以太网卡，您可以执行命令：

```
/sbin/ifup ifcfg-eth0
```

或者简单地执行：

```
/sbin/ifup eth0
```

如果您省略了 `ifcfg-` 前缀，命令会自动补全它。

`ifup` 和 `ifdown` 脚本使用 `ifconfig` 命令（在下文的小节中描述），这是一个特权命令。因此，普通用户无法执行 `ifup` 和 `ifdown` 脚本，除非您指定相关的接口是用户可控制的。然而，非特权用户可能需要比 `ifup` 和 `ifdown` 脚本提供的更简单的用户界面。这类用户可能更倾向于使用 `usernet` 和 `usernetctl` 命令，如果接口是用户可控制的，他们就可以使用这些命令。详情请参阅 `usernet` 和 `usernetctl` 的 man 手册页。

`ifcfg-`* 脚本包含设置指定网络配置的环境变量值的命令。例如，这是一个典型的 `ifcfg-eth0` 脚本：

```
DEVICE="eth0"
IPADDR="192.168.1.3"
NETMASK="255.255.255.0"
ONBOOT="yes"
BOOTPROTO="none"
```

如果您使用 `linuxconf` 来建立网络配置，该文件可能会包含设置各种 IPX 相关环境变量的语句，即使您的系统并未配置 IPX。上述示例配置对应于静态以太网配置。它包括：

- 设备名称，`DEVICE=eth0`
- IP 地址，`IPADDR=192.168.1.3`
- 网络子网掩码，`NETMASK=255.255.255.0`
- 表示设备应在系统启动时启动的参数，`ONBOOT=yes`
- 表示配置为静态的参数，`BOOTPROTO=none`

静态以太网配置还可能包括：

- 网络地址，`NETWORK=192.168.1.0`
- 网络广播地址，`BROADCAST=192.168.1.255`

如果您将接口配置为通过 DHCP 获取配置，文件的内容会有所不同。它包括以下内容：

- 设备名称，`DEVICE=eth0`
- 启动协议，`BOOTPROTO=dhcp`
- 表示设备应在系统启动时启动的参数，`ONBOOT=yes`

您可以通过 `linuxconf` 或 `netcfg` 修改网络配置，或者使用文本编辑器直接修改文件。

### /etc/sysconfig/network 脚本

影响每个接口的全局网络配置信息存储在 `/etc/sysconfig/network` 中。这是一个典型的 `/etc/sysconfig/network` 文件。

```
NETWORKING=yes
FORWARD_IPV4="yes"
HOSTNAME="athlon.azusapacific.com"
GATEWAY="192.168.1.1"
GATEWAYDEV="eth1"
```

该文件表明网络已激活且系统将进行数据包路由。系统的主机名为 `athlon.azusapacific.com`；其默认网关为 `192.168.1.1`，可通过名为 `eth1` 的以太网接口访问。如果系统使用了 NIS，该文件还会指明其关联的 NIS 域。

现在，请完成练习 15.1，该练习要求您研究网络配置文件。

### 练习 15.1：网络配置脚本

对于 RHCE 考试，了解如何在有无配置工具的情况下配置网络非常重要。要在不使用配置工具的情况下配置网络，您必须知道每个网络配置文件的名称和功能。为了进一步了解这些文件，请检查一台运行中的 Linux 服务器的网络配置文件。确认您理解每个文件的作用和内容。目前，您可以随意参考本书和其他文档。但在参加 RHCE 考试之前，请确保您能够在不查阅任何文档的情况下找到每个文件并解释其功能。

## 网络管理命令

有几个命令可以帮助您管理网络。其中最重要的包括：

- ifconfig
- netstat
- arp

本节将解释这些命令的操作。

### ifconfig 命令

`ifconfig` 命令报告网络接口的状态，并允许您添加或删除接口。它被 `/etc/sysconfig/network-scripts` 中的 `ifup` 和 `ifdown` 脚本调用。

#### 报告网络接口状态

要获取网络接口状态的报告，请执行命令：

```
ifconfig
```

命令的输出将类似于以下内容：

```
eth0 Link encap:Ethernet HWaddr 00:40:05:68:02:30
  inet addr:192.168.100.2 Bcast:192.168.100.255
  Mask:255.255.255.0
  UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
  RX packets:1601111 errors:0 dropped:0 overruns:0
  frame:0
  TX packets:1549740 errors:49 dropped:0 overruns:0
  carrier:98
  collisions:952 txqueuelen:100
  Interrupt:10 Base address:0x6100

eth1 Link encap:Ethernet HWaddr 00:A0:CC:25:8A:EC
  inet addr:192.168.1.1 Bcast:192.168.1.255
  Mask:255.255.255.0
  UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
  RX packets:2063495 errors:0 dropped:0 overruns:0
  frame:0
  TX packets:2181226 errors:0 dropped:0 overruns:0
  carrier:0
  collisions:37470 txqueuelen:100
  Interrupt:11 Base address:0x60000

lo Link encap:Local Loopback
  inet addr:127.0.0.1 Mask:255.0.0.0
  UP LOOPBACK RUNNING MTU:3924 Metric:1
  RX packets:75545 errors:0 dropped:0 overruns:0
  frame:0
  TX packets:75545 errors:0 dropped:0 overruns:0
  carrier:0
  collisions:0 txqueuelen:0
```

示例输出显示了两块以太网卡 eth0 和 eth1，以及 TCP/IP 虚拟回环设备 lo。表 15.2 描述了报告中包含的字段。

**表 15.2 ifconfig 输出中的字段**

| 字段 | 描述 |
|---|---|
| Link encap | 接口类型 |
| Hwaddr | 接口的硬件地址 (MAC) |
| inet addr | 接口的 IP 地址 |
| Bcast | 网络的广播地址 |
| Mask | 子网的掩码 |
| Status | 接口状态（例如，UP BROADCAST RUNNING MULTICAST） |
| MTU | 最大传输单元大小（字节） |
| Metric | 接口度量值，被某些路由协议使用 |
| RX packets | 接收到的数据包数量，以及发生的错误数、丢包数、溢出数和坏帧数 |



## 表 15.2 ifconfig 输出中的字段（续

| 字段 | 描述 |
|---|---|
| TX packets | 发送的数据包数量，以及发生的错误数、丢弃包数、溢出数和载波丢失数 |
| collisions | 以太网冲突次数 |
| txqueuelen | 发送队列长度 |
| Interrupt | 接口的 IRQ（中断请求） |
| Base address | 接口的 I/O 端口地址 |

如果您想获取特定网络接口的状态报告，请执行如下形式的命令：

```
ifconfig if
```

其中 `if` 是接口的名称。例如，以下命令：

```
ifconfig eth0
```

会报告 eth0 接口的状态。

现在，完成练习 15.2，以熟悉 ifconfig 命令的输出。

#### 练习 15.2：查看网络状态

ifconfig 命令是最基础且最重要的网络命令之一。为了进一步了解它，请使用 ifconfig 命令查看一台运行中的 Linux 服务器的状态。确保您能解释每个输出字段的含义。在进行此练习时，如有必要请参考表 15.2，但在参加 RHCE 考试之前，请务必彻底熟悉其输出格式。

### 添加和删除网络接口

要添加一个接口，请指定如下形式的命令：

```
ifconfig device ipaddr
```

其中 *device* 是设备名称，*ipaddr* 是接口的 IP 地址。例如，以下命令：

```
ifconfig eth0 192.168.1.1
```

将建立一个 IP 地址为 192.168.1.1 的以太网接口。您还可以指定几个额外的选项。例如，以下命令：

```
ifconfig eth0 192.168.1.1 netmask 255.255.255.0 broadcast 192.168.1.255
```

将建立一个 IP 地址为 192.168.1.1、网络子网掩码为 255.255.255.0 且网络广播地址为 192.168.1.255 的以太网接口。有关其他选项，请参阅 ifconfig 的 man 手册页。

要删除一个接口，请指定如下形式的命令：

```
ifconfig device down
```

其中 *device* 是设备名称。例如，以下命令：

```
ifconfig eth0 down
```

将停用 eth0 接口。

当您使用 ifconfig 重新配置接口时，系统重启后您的更改将会丢失，因为系统初始化脚本会使用网络配置文件中指定的参数值来执行 ifconfig 命令。您应当掌握 ifconfig 命令，以便理解这些脚本的运行方式。您执行 ifconfig 命令的主要目的是为了排除网络故障以及进行其他临时网络重配置。要永久更改网络配置，您应该使用配置工具或编辑网络配置文件。

### netstat 命令

netstat 命令可报告各种网络相关信息。例如，以下命令：

```bash
netstat -r -n
```

会报告内核的路由表。netstat 命令的输出类似于以下内容：

```text
Kernel IP routing table
Destination     Gateway Genmask        Flags MSS Window irtt
Iface
192.168.1.3     *       255.255.255.255 UH    0 0    0 eth1
192.168.100.3   *       255.255.255.255 UH    0 0    0 eth0
192.168.100.0   *       255.255.255.0   U     0 0    0 eth0
192.168.1.0     *       255.255.255.0   U     0 0    0 eth1
127.0.0.0       *       0.0.0.0         U     0 0    0 lo
default 192.168.1.1 0.0.0.0            UG    0 0    0 eth1
```

输出显示了几个可通过网络接口访问的目的地。在示例中，前两行描述了系统中安装的接口。接下来的两行描述了通过这些接口可用的网络；Genmask 列给出了与每个网络关联的网络掩码。倒数第二行描述了回环网络（loopback network），它与虚拟回环设备相关联。最后一行显示了默认路由，用于不匹配任何定义目的地址的网络地址。表 15.3 描述了输出第四列中出现的标志（flags）。

#### 表 15.3 netstat 报告的标志

| 标志 | 描述 |
|---|---|
| G | 该路由建立了一个网关。 |
| U | 相关联的接口处于启用（up）状态。 |
| H | 该路由指定的是到单个主机的路由，而非网络。 |
| D | 该条目是响应 ICMP 消息而创建的。 |
| M | 该条目是响应 ICMP 消息而修改的。 |

`netstat` 命令的另一种实用形式可报告与伪装网络（masqueraded network）外部主机的连接。要查看此报告，请执行命令：

```
netstat -M
```

输出类似于以下内容：

```text
IP masquerading entries
prot expire source destination ports
tcp 14:53.71 bigtop.azusapacific.com home.apu.edu 1047
--> ssh (63685)
```

输出显示了协议 (TCP)、伪装连接的过期时间 (14:53.71)、本地主机 (`bigtop.azusapacific.com`)、目的地 (`home.apu.edu`)、端口 (1047) 以及服务 (ssh)。

现在，完成练习 15.3 以获得使用 `netstat` 命令的经验。

#### 练习 15.3：查看网络状态

netstat 命令方便地提供了关于网络状态的有用信息。为了获得使用 netstat 命令的经验，请使用 `netstat -n -r` 命令查看一台运行中的 Linux 服务器的网络状态。根据本章及其他文档需要，解释输出的每个字段。但是，在参加 RHCE 考试之前，请确保您能够在无需帮助的情况下解读 netstat 命令的输出。

### arp 命令

`arp` 命令允许您查看或修改内核的 *地址解析协议 (ARP)* 表，该表将 IP 地址映射到接口的硬件地址 (*MAC 地址*)。`arp` 命令在检测和处理重复 IP 地址时尤其有用。但是，主机只有在发送过以太网数据包之后才会出现在 ARP 表中。

要查看 ARP 表，请执行命令：

```
arp -a
```

该命令的输出类似于以下内容：

```text
bigtop.azusapacific.com (192.168.1.90) at
00:E0:98:77:08:40
[ether] on eth1
```

报告指示了本地可访问网络上系统的主机名、IP 地址、以太网地址以及相关联的接口。

要删除某个主机的 ARP 条目，请执行如下形式的命令：

```
arp -d host
```

其中 host 是您想从表中删除的系统的主机名。要为某个主机指定 ARP 条目，请执行如下形式的命令：

```
arp -s host mac_addr
```

其中 host 是您想要关联的系统的主机名，mac_addr 是您想要与该主机关联的硬件 (MAC) 地址。例如，要为 MAC 地址为 00:E0:98:77:08:41 的主机 happy 指定一个 ARP 条目，请执行命令：

```
arp -s happy 00:E0:98:77:08:41
```

## 其他 /etc/sysconfig 文件

除了 network 脚本和 network-scripts 子目录外，/etc/sysconfig 目录还包含各种系统设施配置的脚本。表 15.4 对此进行了总结。

### 表 15.4 /etc/sysconfig 中的文件和目录

| 文件/目录 | 描述 |
| :--- | :--- |
| apmd | 包含高级电源管理 (APM) 配置 |
| clock | 包含时钟配置，指示时钟是否设置为协调世界时 (UTC) |
| console | 包含控制台配置，包括键映射（目录） |
| init | 包含系统启动配置，包括应如何报告服务启动状态 |
| keyboard | 包含键盘配置，包括默认键映射的标识 |
| mouse | 包含鼠标配置，包括鼠标类型以及是否需要三键仿真 |
| network | 包含网络配置，包括主机名和网关 |
| network-scripts | 包含网络配置脚本（目录） |
| pcmcia | 包含 PCMCIA 配置，包括启动时是否加载 PCMCIA |
| sendmail | 包含 sendmail 配置，包括 sendmail 是否作为守护进程运行 |
| soundcard | 包含声音配置，包括声卡类型 |
| static-routes | 包含静态路由，包括相关设备、网络地址和网关 |

linuxconf 程序允许您配置大多数这些设施。如果您愿意，大多数文件可以使用文本编辑器安全地修改。但声音配置是一个例外。您应该使用 sndconfig 工具来配置声音；不应手动编辑 /etc/sysconfig/soundcard 文件。

接下来的小节将提供关于高级电源管理、PCMCIA、即插即用设备以及声音的更多信息。



## 高级电源管理 (APM) 配置

高级电源管理 (APM) 有助于节省电能。它对于笔记本电脑等电池供电的计算机尤为有用；不过，许多现代台式机也支持 APM，你可以用它来关闭未使用的外设。当在笔记本电脑上使用 APM 且检测到低电量状态时，它会调暗显示屏、降低 CPU 时钟频率并关闭外设以节省电量。文件 `/etc/sysconfig/apmd` 包含 APM 配置，该配置被脚本 `/etc/rc.d/init.d/apmd` 引用。有关配置和使用 APM 的更多信息，请参阅 The Battery-Powered Linux Mini-HOWTO。

## PCMCIA 配置

PCMCIA 服务管理 PCMCIA 卡。文件 `/etc/sysconfig/pcmcia` 包含 PCMCIA 服务的配置信息，该信息被脚本 `/etc/rc.d/init.d/pcmcia` 引用。PCMCIA 设备的配置信息位于 `/etc/pcmcia`。如果你重新编译使用 PCMCIA 系统的 Linux 内核，则必须同时重新编译并安装 PCMCIA 软件包。有关 PCMCIA 的更多信息，请参阅 Linux PCMCIA 网站 `pcmcia.sourceforge.org`。

## 即插即用 (Plug-and-Play) 配置

如第 2 章所述，即插即用设备旨在通过 BIOS 和操作系统的协作来自动配置。然而，Linux 并不完全支持 ISA 接口卡的即插即用。当在支持即插即用的 BIOS 上使用 Linux 时，请将 BIOS 设置为指示操作系统不支持即插即用。然后，你可以按照以下步骤配置 ISA 即插即用卡：

- 1. 执行命令 `pnpdump >/etc/isapnp.conf`。该命令将每个已安装的即插即用卡的配置转储到指定文件 `/etc/isapnp.conf` 中。
- 2. 使用文本编辑器修改 `/etc/isapnp.conf` 文件。该文件包含每个即插即用设备每种可能配置的注释行。你必须取消每个设备所需配置行的注释。你还必须取消设备配置末尾指定设备处于激活状态的那一行的注释。
- 3. 执行命令 `isapnp /etc/isapnp.conf`。该命令根据 `/etc/isapnp.conf` 中给出的配置来配置已安装的即插即用卡。Linux 启动序列在系统启动期间执行此命令以配置即插即用设备。

有关 Linux 对即插即用支持的更多信息，请参阅 `www.roe-stock.demon.co.uk/isapnptools`。

## 声音配置

`sndconfig` 命令可检测并配置大多数即插即用声卡。该命令将声音配置信息存放在 `/etc/conf.modules`、`/etc/isapnp.conf` 以及 `/etc/sysconfig/soundcard` 中。

如果你在 X 窗口环境下使用 GNOME 桌面管理器，GNOME 声音管理器 `esd` 将管理你的声卡，并允许多个应用程序同时访问它。但是，如果你执行一个不感知 `esd` 的应用程序，它可能会与其他应用程序产生冲突。为了避免这种情况，请使用 `esddsp` 包装器调用该应用程序。通过执行以下命令启动应用程序：

`esddsp application`

其中 `application` 是应用程序的名称或路径。KDE 应用程序 `kaudioserver` 执行的功能与 `esd` 类似。

## /etc/fstab 文件

`/etc/fstab` 文件描述了与 Linux 系统关联的文件系统。以下是一个典型的 `/etc/fstab` 文件的内容：

```
/dev/hda1 /dos msdos defaults 0 2
/dev/hda5 /boot ext2 defaults 1 2
/dev/hda6 /usr ext2 defaults 1 2
/dev/hda7 /home ext2 defaults 1 2
/dev/hda8 /var ext2 defaults 1 2
/dev/hda9 / ext2 defaults 1 1
/dev/hda10 swap swap defaults 0 0
/dev/hda11 /space ext2 defaults 1 2
/dev/fd0 /mnt/floppy ext2 noauto 0 0
/dev/cdrom /cdrom1 iso9660 noauto,ro 0 0
/dev/hdd /cdrom2 iso9660 noauto,ro 0 0
none /proc proc defaults 0 0
none /dev/pts devpts mode=0622 0 0
```

文件中的每一行描述一个文件系统。各字段如下：

- 设备文件。
- 挂载点。
- 文件系统类型。表 15.5 总结了 Linux 支持的文件系统类型。
- 挂载选项。表 15.6 总结了可用选项。
- Dump 标志。值 1 表示该文件系统应自动包含在系统 dump 中；值 0 表示不应包含。
- 文件系统检查顺序。值 1 表示根文件系统；值 2 表示应自动检查的非根文件系统；值 0 表示不应自动检查的文件系统。

### 表 15.5 Linux 文件系统类型

| 文件系统类型 | 描述 |
| :--- | :--- |
| adfs | Acorn RisCOS 文件系统 |
| affs | AmigaOS 文件系统 |
| coda | Coda，一种类似于 NFS 的高级网络文件系统 |
| devpts | 伪终端的虚拟文件系统 |
| ext2 | 标准 Linux 文件系统 |
| hfs | Apple Macintosh 文件系统 |
| hpfs | IBM OS/2 文件系统 |
| iso9660 | 标准 CD-ROM 文件系统 |
| minix | Tannenbaum 的 MINIX 文件系统 |
| msdos | 未压缩的 MS-DOS 文件系统 |
| ncpfs | Novell NetWare 文件系统 |
| nfs | Unix 网络文件系统 |
| ntfs | Microsoft Windows NT 文件系统 |
| proc | /proc 虚拟文件系统 |
| qnx4fs | QNX 文件系统 |
| romfs | RAM 磁盘的只读文件系统 |
| smbfs | Microsoft SMB (LAN Manager) 文件系统 |
| sysv | SCO, Xenix 和 Coherent 文件系统 |
| ufs | BSD, SunOS, FreeBSD, NetBSD, OpenBSD 和 NeXTstep 文件系统 |
| umsdos | 运行在 MS-DOS 文件系统之上的 Linux 文件系统 |
| vfat | Microsoft Windows 9x 文件系统 |

### 表 15.6 挂载选项

| 选项 | 描述 |
| :--- | :--- |
| async | 异步执行所有输入和输出。 |
| atime | 更新文件系统上的 inode 访问时间。 |
| auto | 响应 `mount -a` 时自动挂载文件系统。 |
| defaults | 启用 rw, suid, dev, exec, auto, nouser 和 async 选项。 |
| dev | 解析文件系统上的字符或块特殊设备。 |
| exec | 允许执行文件系统上的二进制文件。 |
| noatime | 不更新文件系统上的 inode 访问时间。 |
| noauto | 响应 `mount -a` 时不自动挂载文件系统。 |
| nodev | 不解析文件系统上的字符或块特殊设备。 |
| noexec | 不允许执行文件系统上的二进制文件。 |
| nosuid | 文件系统文件的 setuid 和 setgid 权限不生效。 |
| nouser | 普通用户不得挂载文件系统（默认）。 |
| remount | 重新挂载已挂载的文件系统以启用一组不同的选项。常用于将只读文件系统重新挂载为读写模式。 |
| ro | 以只读模式挂载文件系统。 |
| rw | 以读写模式挂载文件系统。 |
| suid | 文件系统文件的 setuid 和 setgid 权限生效。 |
| sync | 同步执行所有输入和输出。 |
| user | 允许普通用户挂载文件系统。隐含 noexec, nosuid 和 nodev 选项。 |

你可以使用 `linuxconf` 修改 `/etc/fstab` 文件的内容，或者如果你愿意，也可以使用文本编辑器。现在，请通过完成练习 15.4 来尝试配置文件系统。

### 练习 15.4：配置文件系统

配置文件系统是一项重要且常见的系统管理任务，很可能会出现在 RHCE 考试中。为了在备考过程中磨练技能，请修改 `/etc/fstab` 文件，指定一个非根分区以只读模式挂载。启动系统并验证你的更改是否正确。恢复原始配置并重启系统。

在做练习时，如有必要，你可以参考本书。但在参加 RHCE 考试之前，请做好在没有书籍或文档帮助的情况下执行此类操作的准备。

## init 进程与 /etc/inittab 文件

*init* 进程负责生成登录进程并管理系统*运行级别 (runlevel)*。其配置文件 `/etc/inittab` 决定了在每个定义的运行级别中应该激活的服务。



## 管理运行级别（Runlevels）

您可以通过执行以下命令来确定当前的运行级别：

```
runlevel
```

该命令的输出由之前的运行级别和当前的运行级别组成。例如，输出内容为

```
5 3
```

表示之前的运行级别是 5，当前的运行级别是 3。要更改运行级别，请执行命令：

```
init n
```

其中 n 是目标运行级别。以下形式的命令具有相同的效果：

```
telinit n
```

`telinit` 的独特之处在于它能够指定在特定时间间隔后才执行运行级别更改。例如，命令

```
telinit -t 60 3
```

指定在延迟 60 秒后将运行级别设置为 3。您可以通过以下任何一种方式切换到运行级别 6（这将导致系统重启）：

- 执行命令 `telinit 6` 或 `init 6`
- 执行命令 `shutdown -r now`
- 执行命令 `reboot`
- 按下 Ctrl+Alt+Del

`shutdown` 命令提供了几个有用的选项。在 `now` 处，您可以包含一个 `+min` 形式的参数，其中 `min` 指定距离重启发生还需要多少分钟。您还可以包含一个 `-t sec` 形式的参数；此选项使命令在关机发生前 `sec` 秒向用户发出警告。

您可以通过以下任何一种方式切换到运行级别 0（这将导致系统停止）：

- 执行命令 `telinit 0` 或 `init 0`
- 执行命令 `shutdown -h now`
- 执行命令 `halt`

`+min` 和 `-t sec` 选项可以与 `shutdown` 命令的 `-h` 参数一起使用。

### /etc/inittab 文件

`/etc/inittab` 文件决定了在每个运行级别中应该处于活动状态的进程。文件中的行具有以下形式：

```
id:runlevels:action:process
```

各字段定义如下：

- id，一个 1-4 个字符的唯一标识符。对于登录进程，id 应为相应 tty 的 tty 后缀。
- runlevels，应执行该操作的运行级别列表。如果省略，则在每个运行级别都执行该操作。
- action，指定要执行的操作。表 15.7 总结了可用的操作。
- process，指定要执行的程序。

以井号 (#) 开头的行将被忽略。

#### 表 15.7 /etc/inittab 中可指定的动作

| Action | 描述 |
| :--- | :--- |
| boot | 指定的进程在系统启动期间执行。运行级别（runlevels）字段被忽略。 |
| bootwait | 进程在系统启动期间执行；init 将等待其终止。运行级别字段被忽略。 |
| ctrlaltdel | 当 init 收到 SIGINT 信号时执行该进程，这意味着系统控制台上有人按下了 Ctrl+Alt+Del 组合键。 |
| initdefault | 指定系统启动后进入的初始运行级别。进程（process）字段被忽略。 |
| kbrequest | 当 init 收到来自键盘处理程序的信号，表明控制台键盘上按下了特殊组合键时执行该进程。 |
| off | 不采取任何操作。 |
| once | 当进入指定的运行级别时，该进程执行一次。 |
| ondemand | 每当调用指定的运行级别（a, b 或 c）时，就会执行该进程。但是，不会发生运行级别更改。 |
| powerfail | 电源断开时执行该进程。init 进程不会等待该进程完成。 |
| powerfail now | 当 init 被告知外部不间断电源 (UPS) 的电池快耗尽时，执行此进程。 |
| powerokwait | 当 init 被通知电源已恢复时，执行此进程。 |
| powerwait | 电源断开时执行该进程。init 进程将等待该进程完成。 |
| respawn | 每当进程终止时，它将被重新启动。 |
| sysinit | 进程在系统启动期间执行，在任何 boot 或 bootwait 条目之前。运行级别字段被忽略。 |
| wait | 当进入指定的运行级别时，该进程执行一次；init 将等待其终止。 |

以下是一个典型的 `/etc/inittab` 文件的内容：

```
id:3:initdefault:

si::sysinit:/etc/rc.d/rc.sysinit

10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6

ud::once:/sbin/update

ca::ctrlaltdel:/sbin/shutdown -t3 -r now

pf::powerfail:/sbin/shutdown -f -h +2 "Power Failure; System Shutting Down"

pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"

1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6

x:5:respawn:/etc/X11/prefdm -nodaemon
```

如果您更改了 `/etc/inittab` 的内容，必须指示 `init` 进程重新读取该文件。为此，请执行命令：

```
init q
```

## 总结

在本章中，您学习了配置文件和脚本。涵盖的最重要主题包括：

**`/etc/sysconfig` 目录** `/etc/sysconfig` 目录包含各种持有配置信息的文件，包括高级电源管理 (APM)、PCMCIA 卡、即插即用卡以及声音的配置信息。`network-scripts` 子目录包含用于启动、关闭和配置网络连接的脚本。

**`ifcfg-*` 脚本** `ifcfg-*` 脚本存储网络接口配置信息。

**`/etc/sysconfig/network` 脚本** `/etc/sysconfig/network` 脚本存储全局网络配置信息——即适用于每个网络接口的配置信息。

**网络管理命令** 最重要的网络管理命令包括 `ifconfig`（允许您配置网络接口）、`netstat`（允许您查看网络状态信息）以及 `arp`（允许您查看和修改系统的地址解析协议 (ARP) 表）。

**`/etc/fstab` 文件** `/etc/fstab` 文件包含系统配置选项。

**`/etc/inittab` 文件** `/etc/inittab` 文件包含 init 的配置选项，init 是负责登录进程和运行级别管理的守护进程。

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- 地址解析协议 (Address Resolution Protocol, ARP)
- 高级电源管理 (Advanced Power Management, APM)
- MAC 地址 (MAC addresses)
- 运行级别 (runlevel)

## 其他信息来源

如果您想进一步了解本章中提出的主题，应参考以下来源：

- *The Official Red Hat Linux Reference Guide* (红帽 Linux 官方参考指南)
- *The Battery-Powered Linux Mini-HOWTO* (电池供电 Linux 微型指南)
- Linux PCMCIA 网页，`pcmcia.sourceforge.org`
- Linux ISA 即插即用网页，`www.roestock.demon.co.uk/isapnptools`
- 初始化脚本文档文件，`/usr/doc/initscripts#/*`

## 复习题

1. 要添加 IP 地址为 192.168.1.1 的以太网设备 `eth1`，应执行以下哪个命令？
    A. `ifconfig -ip 192.168.1.1 eth1`
    B. `ifconfig 192.168.1.1 eth1`
    C. `ifconfig eth1 192.168.1.1`
    D. `ifconfig eth1 -ip 192.168.1.1`

2. 要关闭设备 `eth1`，应执行以下哪个命令？
    A. `ifconfig eth1 down`
    B. `ifconfig ifcfg-eth1 down`
    C. `/sbin/ifdown eth1`
    D. `/sbin/ifdown ifcfg-eth1`

3. 要查看内核的路由表，应执行以下哪个命令？
    A. `netstat -i`
    B. `netstat -m`
    C. `netstat -M`
    D. `netstat -r`

4. 以下哪个命令可以启动设备 `eth2`？
    A. `ifup eth2`
    B. `ifup ifcfg-eth2`
    C. `ifup /etc/sysconfig/eth2`
    D. `ifup /etc/sysconfig/network-scripts/eth2`



5. 以下哪个命令可以正确挂载 Windows 95 文件系统？

- **A.** `mount -t fat32 /dev/hda1 /dos -o ro`
- **B.** `mount -t msdos /dev/hda1 /dos -o ro`
- **C.** `mount -t vfat /dev/hda1 /dos -o ro`
- **D.** `mount -t win95 /dev/hda1 /dos -o ro`

6. 以下哪个命令将重启系统？

- **A.** `init 6`
- **B.** `reboot`
- **C.** `shutdown -r now`
- **D.** `telinit 6`

## 复习题答案

1. C. 要添加设备，请指定设备名称和 IP 地址。
2. A, C, D. 您可以使用 `/sbin/ifdown` 或 `ifconfig` 来关闭设备；但是，`ifconfig` 不接受脚本名称 `ifcfg-eth1` 作为参数。
3. D. `-r` 标志使 `netstat` 命令报告路由表。
4. A, B. 该命令需要设备名称；不能指定路径。
5. C. Windows 95 文件系统的类型为 vfat。可以将 Windows 95 文件系统挂载为 `msdos` 文件系统，但这样做可能会破坏您操作的文件长文件名。
6. A, B, C, D. 任何一种替代方案都有效；此外，按下 Ctrl+Alt+Del 也会重启系统。

# 第 16 章：使用 *cron* 系统

**本章涵盖的 RHCE 准备主题：**

- 理解 cron 系统并能够使用 cron 和 anacron 调度任务。

`cron` 系统允许系统管理员和普通用户调度任务，使其在指定的时间间隔和时间自动执行。默认情况下，Red Hat Linux 系统运行多个 `cron` 任务以方便系统管理。作为 Red Hat Linux 系统管理员，您需要知道如何管理 `cron` 系统。您还需要了解 `cron` 为您自动配置运行的任务。本章将介绍 `cron` 系统及其运行的默认任务。

## *cron* 系统

`cron` 系统允许用户调度任务在指定的时间和间隔自动执行。任务使用所有者用户的登录身份运行；默认情况下，任务结果通过电子邮件发送给所有者用户。一个实用程序允许用户运行文本编辑器来指定运行哪些任务以及何时运行。

`cron` 系统由以下组件组成：

- `/usr/sbin/crond`，`cron` 服务，持续运行
- `/etc/crontab`，系统 `cron` 表，指定 Red Hat 定义的默认任务
- `/usr/bin/crontab`，允许用户创建和管理 `cron` 表条目的程序
- `/var/spool/cron`，存放用户创建的 `cron` 文件的目录
- `/etc/cron.d`，存放由软件包安装脚本创建的 `cron` 文件的目录
- `/etc/cron.allow` 和 `/etc/cron.deny`，允许您限制访问 `cron` 系统的文件

下一节将解释用户 `cron` 表及其使用方法。接下来的章节将解释系统 `cron` 表；本章的其余部分将解释系统 `cron` 表中包含的默认任务。

### 用户 crontabs

当用户访问 `cron` 系统时，系统会创建文件 `/var/spool/cron/user`，其中 `user` 是用户的登录名。这个文件（被称为 `cron 文件`、`cron 表` 或 `crontab`）包含指定运行哪些任务以及何时运行的条目。

默认情况下，普通用户被允许访问 `cron` 系统。然而，系统管理员可以限制这一特权。如果文件 `/etc/cron.allow` 存在，则只有在该文件中列出的用户才能访问 `cron` 系统。同样，如果文件 `/etc/cron.deny` 存在，则在该文件中列出的任何用户都不能访问 `cron` 系统。

被允许访问 `cron` 系统的用户可以执行以下操作：

- 修改 `crontab` 中的条目。
- 列出现有的 `cron` 任务。
- 删除 `crontab`。

以下小节将详细解释这些操作。

#### 编辑用户 crontab

用户可以通过执行以下命令来编辑其 `crontab` 条目：

```bash
crontab -e
```

同样，`root` 用户可以通过执行以下形式的命令来编辑某个用户的 `crontab` 条目：

```bash
crontab -u user -e
```

其中 `user` 是要编辑其 `crontab` 的用户登录名。

响应 `crontab -e` 命令时，`cron` 系统将启动默认的系统编辑器。如果您希望使用不同的编辑器，可以在执行 `crontab` 命令之前设置环境变量 `EDITOR`。例如：

```bash
export EDITOR=/usr/bin/pico
crontab -e
```

允许用户使用 `pico` 编辑器编辑 `crontab`。

用户可以通过执行以下命令完全删除其 `crontab`：

```bash
crontab -r
```

`root` 用户可以通过执行以下形式的命令来删除某个用户的 `crontab`：

```bash
crontab -u user -r
```

其中 `user` 是要删除其 `crontab` 的用户登录名。`crontab` 条目以特殊格式的行指定；下一小节将解释它们必须呈现的格式。

#### crontab 文件的格式

`crontab` 文件可能包含以下类型的行：

- 注释行
- 环境设置
- cron 命令

在行内，开头的空格和制表符会被忽略。空白行和以井号 (#) 开头的行被视为注释行，被 `cron` 系统忽略。

#### 指定环境设置

环境设置行的形式为：

```
name = value
```

此类行指定环境变量名称及其关联的值。`cron` 任务可以访问这些环境变量。以下环境变量无需显式定义即可使用：

- SHELL 绑定到 /bin/sh
- LOGNAME 绑定到用户的登录名
- HOME 绑定到用户在 /etc/passwd 中指定的主目录

您可以为 SHELL 或 HOME 环境变量指定新值。但是，您不能为 LOGNAME 环境变量指定新值。

默认情况下，cron 任务的输出通过电子邮件发送给所有者用户。但是，您可以通过为 MAILTO 环境变量指定值来覆盖此操作。通过这样定义变量：

```
MAILTO=" "
```

将不会发送任何输出。如果您将 MAILTO 环境变量绑定到电子邮件地址，输出将发送到指定地址。例如，如果您指定：

```
MAILTO="admin@bigtop.azusapacific.com"
```

cron 任务的输出将通过邮件发送到 admin@bigtop.azusapacific.com。

#### 指定 cron 命令

crontab 中的命令行具有以下形式：

```
minute hour day_of_month month day_of_week command
```

这些行包含六个字段，每个字段与相邻字段之间由一个或多个空格分隔。表 16.1 描述了前五个字段，它们指定了执行指定命令的时间间隔或时间。

cron 系统每分钟检查一次其 crontab 文件，并执行时间规范与当前日期和时间匹配的条目。包含星号 (*) 的字段匹配任何值。请注意，后续章节将介绍更多选项。

#### 表 16.1 crontab 文件中的日期字段

| 字段 | 描述 |
|---|---|
| minute | 0 到 59 之间的值，或 * |
| hour | 0 到 23 之间的值，或 * |
| day_of_month | 1 到 31 之间的值，或 * |
| month | 1 到 12 之间的值（1 表示一月），或 * |
| day_of_week | 0 到 7 之间的值（0 或 7 表示星期日），或 * |

当分钟和小时字段与当前时间匹配，且月份字段与当前月份匹配时，`crontab` 条目被认为与当前时间匹配。当月份日期字段与当前月日期匹配，或星期字段与当前星期匹配时，条目被认为与当前日期匹配：不需要月份日期和星期同时匹配。如果时间和日期都与当前时间日期匹配，则执行指定命令。表 16.2 描述了一些 `crontab` 条目的示例。

#### 表 16.2 crontab 文件中的时间规范示例

| 时间规范 | 含义 |
| :--- | :--- |
| `5 12 * * *` | 每天中午 12 点 05 分运行。 |
| `5 * * * *` | 每小时的第 5 分钟运行。 |
| `15 17 1 * *` | 每月 1 日下午 5:15 运行。 |
| `45 16 * * 5` | 每个星期五下午 4:45 运行。 |
| `00 15 * 12 5` | 12 月每个星期五下午 3:00 运行。 |

您还可以指定数字范围和列表。例如，小时字段中的 8–10 将匹配上午 8:00、9:00 和 10:00。同样，小时字段中的 8–10, 13 将匹配上午 8:00、9:00、10:00 和下午 1:00。

您可以指定步长值，步长值与范围一起使用。例如，小时字段中的 0–10/2 指的是凌晨 0:00、上午 2:00、4:00、6:00、8:00 和 10:00。规范 `/2` 表示指定命令应每两小时执行一次。

如果您愿意，可以在月份和星期字段中使用名称。为此，请使用月份或日期的前三个字母，不区分大小写。例如：

```
0 19 * dec fri
```

指定在 12 月的每个星期五晚上 7:00 执行。您不能在月份或日期名称中使用范围或列表；如果您想指定范围或列表，必须使用数字。



每个 crontab 行的最后一个字段指定了要执行的命令。如果你在命令中包含百分号 (%)，则只有百分号之前的字段部分会被执行。命令中剩余的所有字符将作为标准输入发送给该命令；随后的百分号将被替换为换行符。若要在命令中嵌入百分号，请在其前面加上反斜杠 (\)，这样可以转义百分号的特殊含义。

例如，以下来自 crontab 手册页的命令会向用户发送邮件：

```
mail -s "It's 10pm" joe%Joe,%%Where are your kids%?
```

其中的百分号被发送为换行符，用作对 `mail` 命令提示符的响应。

要进一步学习如何使用 cron，请完成练习 16.1。

## 练习 16.1
### 编辑你的 cron 表

这是一个简单的练习，旨在让你练习定义 cron 任务。请以普通用户身份登录，并使用 `crontab` 命令创建一个 cron 任务，使其在每晚 12:05 A.M. 运行 `w` 命令。在第二天早上检查，验证输出是否已发送到你的电子邮件收件箱中。

你可以回顾本章的内容来帮助你完成该练习。但在参加 RHCE 考试之前，请确保你在没有书籍或笔记帮助的情况下能够执行此类操作。

### 列出用户 crontab

用户可以通过执行以下命令列出其 crontab 的内容：

```
crontab -l
```

输出将以 crontab 的格式列出，具体格式在前面的小节中已有说明。例如，你可能会看到典型的如下输出：

```
crontab -l
# DO NOT EDIT THIS FILE - edit the master and reinstall.
# /tmp/crontab.4014 installed on Tue Apr 18 09:40:56 2000)
# (Cron version -- $Id: crontab.c,v 2.13 1994/01/17 03:20:37
# vixie Exp $)
5 0 * * * w
```

输出显示了位于 `/var/spool/cron` 中的 crontab 的创建日期；示例输出中提到的文件 `/tmp/crontab.4014` 仅仅是 crontab 的一个临时副本。请注意，输出中包含一条警告，禁止直接编辑 crontab；要编辑 crontab，必须遵循前一个小节中给出的步骤。

root 用户可以通过执行以下形式的命令来列出某个用户的 crontab 内容：

```
crontab -u user -l
```

其中 `user` 是要列出 crontab 的用户的登录名。现在，请完成练习 16.2，该练习将测试你列出 cron 表的能力。

## 练习 16.2
### 列出你的 cron 表

使用 cron 相当简单，但练习将帮助你确定你的熟练程度。为了衡量你对 cron 的理解，请以普通用户身份登录，并使用 `crontab` 命令查看你的 cron 表。除非你之前已经创建过，否则你应该会看到一条消息，提示不存在 cron 条目。

你可以回顾本章的内容来帮助你完成该练习。但在参加 RHCE 考试之前，请确保你在没有书籍或笔记帮助的情况下能够列出你的 cron 表。

## 系统 crontab

除了存储在 `/var/spool/cron` 中的用户 crontab 文件外，cron 系统还有一个系统 cron 文件，存储在 `/etc/crontab` 中。以下是一个典型的 `/etc/crontab` 文件的内容：

```
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/

# run-parts
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
```

`/etc/crontab` 文件的格式与用户 crontab 文件略有不同。它包含一个 `user`（用户）ID 字段，用于指定运行相关命令的用户 ID。用户 `id` 字段是每行的第六个字段，位于 `command`（命令）字段之前。

默认的 Red Hat Linux `/etc/crontab` 文件包含四行命令，每行都指定 `run-parts` 脚本为要运行的命令。`run-parts` 脚本接受一个参数，即一个目录。该脚本会执行指定目录中包含的所有文件。`/etc/crontab` 文件使用 `run-parts` 来执行每小时、每天、每周和每月任务。因此，无需编辑 `/etc/crontab` 文件；你只需将要执行的脚本（或指向该脚本的符号链接）放置在 `/etc/cron.*` 目录之一中即可。不过，作为 root 用户，你可以使用文本编辑器编辑该文件，而不需要使用 `crontab` 命令。

> 提示：如果你修改了 `/etc/crontab` 文件，cron 系统将检测到该文件的修改日期已更改。你不需要重启或向 cron 守护进程发送信号。

Red Hat Linux 还有一组存储在 `/etc/cron.d` 中的系统 crontab 文件；这些文件是由软件包安装脚本创建的。它们的格式与 `/etc/crontab` 相同。例如，`modutils` 软件包会安装文件 `/etc/cron.d/kmod`。以下是一个典型的 `/etc/cron.d/kmod` 文件的内容：

```
# rrmod -a is a two-hand sweep module cleaner
*/10 * * * * root /sbin/rrmod -as
```

该文件每 10 分钟运行一次 `rrmod` 命令，以卸载未使用的模块。接下来的几个章节将描述由 Red Hat Linux `cron` 系统执行的标准每小时、每天、每周和每月任务。

### 每小时 cron 任务

`/etc/crontab` 文件将 `/etc/cron.hourly` 目录指定为每小时执行脚本的存放位置。默认情况下，该目录为空。不过，你可以将自己的每小时脚本添加到该目录中。

### 每日 cron 任务

默认情况下，Red Hat Linux 运行以下每日 cron 任务：

- logrotate
- makewhatis
- locate
- tmpwatch

RHCE 考试不需要对这些任务有深入的了解。以下小节将对它们进行简要描述。

#### logrotate 任务

每日 logrotate 任务是一个简单的脚本，用于调用 `logrotate` 命令：

```bash
#!/bin/sh
/usr/sbin/logrotate /etc/logrotate.conf
```

`logrotate` 命令允许对日志文件进行自动轮转、压缩、删除和邮件发送。你可以查阅其手册页了解详细信息，特别是其配置文件的格式。

#### makewhatis 任务

`whatis` 命令提供了访问手册页中关键字数据库的功能。例如，如果你执行命令：

```
whatis rm
```

该命令会响应：

```
rm (1) - remove files or directories
```

同一个数据库还支持 `apropos` 命令，该命令可列出与指定主题相关的手册页。例如，如果你执行命令：

```
apropos cron
```

该命令会响应：

```
cron(8) - daemon to execute scheduled commands
crontab(1) - maintain crontab files for individual users
crontab(5) - tables for driving cron
```

你还可以使用以下命令形式调用 `apropos` 命令：

```
man -k topic
```

其中 *topic* 指定你感兴趣的主题。

为了维护 `whatis` 和 `apropos` 使用的数据库，必须定期运行 `makewhatis` 命令。为此，默认的 Red Hat Linux `cron` 系统每天运行一次 `/etc/cron.daily/makewhatis.cron` 脚本：

```bash
#!/bin/bash
LOCKFILE=/var/lock/makewhatis.lock

# the lockfile is not meant to be perfect, it's just in case
# the two makewhatis cron scripts get run close to each
# other to keep them from stepping on each other's toes.
# The worst that will happen is that they will temporarily
# corrupt the database...
[ -f $LOCKFILE ] && exit 0
touch $LOCKFILE
makewhatis -u -w
rm -f $LOCKFILE
exit 0
```

`-u` 选项使 `makewhatis` 将新手册页的信息添加到数据库中。你可以查阅 `makewhatis` 手册页了解详细信息。

#### locate 程序

`locate` 命令使得在给定文件名或匹配文件名的模式的情况下，能够找到文件所在的目录。例如，要查找包含文件名中包含字符 `linux.words` 的目录，请执行命令：

```
locate linux.words
```



命令的输出类似于以下内容：

```
/usr/dict/linux.words
/usr/doc/words-2/README.linux.words
/usr/doc/words-2/README2.linux.words
```

与提供类似功能的 `find` 命令不同，`locate` 命令使用数据库。与 `find` 命令相比，数据库加快了 `locate`locate` 命令的执行速度。然而，为了使其发挥作用，数据库必须定期更新，并且不会反映自最近一次更新以来新增的文件。

默认的 Red Hat Linux `cron` 系统每天运行脚本 `/etc/cron.daily/slocate.cron`：

```
#!/bin/sh
NETMOUNTS=`mount -t nfs,smbfs,ncpfs | cut -d ' ' -f 3`
NETPATHS=`echo $NETMOUNTS | sed -e 's|.|,|g'`

if [ -n "$NETPATHS" ]; then
    /usr/bin/slocate -u -e "$NETPATHS,/tmp,/var/tmp,/usr/tmp,/afs, /net,/proc"
else
    /usr/bin/slocate -u -e "/tmp,/var/tmp,/usr/tmp,/afs,/net,/proc"
fi
```

符号链接 `/usr/bin/slocate` 指向 `/usr/bin/updatedb`，这是一个用于重建 `locate` 命令所使用数据库的实用程序。您可以参考 `locate` 和 `updatedb` 的 man 手册获取详细信息；不过，为了准备 RHCE 考试，您不需要掌握这些命令的详细知识。

### tmpwatch 任务

由 `cron` 系统承担的另一个每日任务是删除过期的临时文件。每天执行的脚本 `/etc/cron.daily/tmpwatch` 会调用以下命令：

```
/usr/sbin/tmpwatch 240 /tmp /var/tmp /var/catman/cat?
```

`tmpwatch` 命令会删除 10 天（240 小时）内未被访问且位于 `/tmp`、`/var/tmp` 和 `/var/catman/cat?` 目录中的文件。您可以参考 `tmpwatch` 的 man 手册获取详细信息；不过，为了准备 RHCE 考试，您不需要掌握这些命令的详细知识。

### 每周 cron 任务

Red Hat Linux cron 系统默认执行一个每周任务：`/etc/cron.weekly/makewhatis.cron`。以下是一个典型的 `/etc/cron.weekly/makewhatis.cron` 文件的内容：

```bash
#!/bin/bash
LOCKFILE=/var/lock/makewhatis.lock

# the lockfile is not meant to be perfect, it's just in case
# the two makewhatis cron scripts get run close to each other
# other to keep them from stepping on each other's toes.
# The worst that will happen is that they will temporarily
# corrupt the database...
[ -f $LOCKFILE ] && exit 0
touch $LOCKFILE
makewhatis -w
rm -f $LOCKFILE
exit 0
```

此脚本类似于上述每日脚本，它运行带有 -u 选项的 `makewhatis` 命令。由于缺少 -u 选项，`makewhatis` 命令将针对每个 man 页更新数据库，而不仅仅是新页。因此，每周任务比每日任务稍微耗时。您可以参考 `makewhatis` 的 man 手册获取详细信息；不过，为了准备 RHCE 考试，您不需要掌握 `makewhatis` 命令的详细知识。

### 每月 cron 任务

`/etc/crontab` 文件将 `/etc/cron.monthly` 目录指定为每月执行脚本的位置。默认情况下，该目录为空。但是，您可以将自己的每月脚本添加到该目录中。

## 桌面任务调度程序：anacron

`cron` 工具假设系统是持续通电的。如果您在断续通电的桌面系统上安装 `cron`，您可能会发现 `cron` 任务很少被执行。例如，计划在凌晨 2:00 运行的 `cron` 任务只有在此时系统通电的情况下才会运行。然而，当您启动安装了 `anacron` 的系统时，`anacron` 将执行在系统关机期间被跳过的任何任务。

`anacron` 工具不如 `cron` 灵活。它不能调度间隔小于一天的任务，也无法保证任务运行的确切时间。此外，它不作为守护进程持续运行；它必须在启动脚本中执行、手动启动或定义为一个 `cron` 任务。

要启动 `anacron`，请执行命令：

```bash
anacron -s
```

`-s` 标志指定顺序执行，它使 `anacron` 一次启动一个任务。这可以避免大量积压的任务堵塞系统。安装 `anacron` 软件包时，一个名为 `anacron` 的 System V 初始化脚本会被放置在 `/etc/rc.d/init.d` 目录中。您可以使用 `/linuxconf` 或其他配置工具配置 `anacron` 在系统启动时启动。

`anacron` 工具的配置文件 `/etc/anacrontab` 通常由手工编辑。其格式比 `crontab` 文件简单，如下所示的典型 `anacrontab` 文件：

```text
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# These entries are useful for a Red Hat Linux system.
1    5    cron.daily    run-parts /etc/cron.daily
7    10   cron.weekly   run-parts /etc/cron.weekly
30   15   cron.monthly  run-parts /etc/cron.monthly
```

该文件可以包含为环境变量分配值的行；示例中的前两行设置了 SHELL 和 PATH 环境变量的值。指定 `anacron` 任务的行有四个字段：

- **period**（周期），指定执行间隔（单位为天）
- **delay**（延迟），指定任务启动前的延迟时间（单位为分钟）
- **job identifier**（任务标识符），一个唯一标识 anacron 任务的字符串
- **command**（命令），指定要执行的命令及其任何命令参数

有关 anacron 的更多信息，请参阅 anacron 和 anacrontab 的 man 手册。

## 总结

在本章中，您学习了 cron 系统。涵盖的最重要主题包括：

- **cron 系统**：cron 系统允许您调度任务，以便在指定的时间或间隔后续执行。
- **系统 cron 表**：系统 cron 表位于 /etc/crontab。它指定了 /etc/cron.hourly、/etc/cron.daily、/etc/cron.weekly 和 /etc/cron.monthly 目录中脚本的定期执行。
- **用户 cron 表**：用户 cron 表位于 /var/spool/cron。
- **软件包相关 cron 表**：软件包相关的 cron 表位于 /etc/cron.d。
- **限制对 cron 的访问**：您可以通过其配置文件 /etc/cron.allow 和 /etc/cron.deny 来限制对 cron 的访问。
- **cron 表行的格式**：cron 表行的字段顺序为：分钟、小时、日期、月份、星期。
- **由 cron 控制的重要任务**：由 cron 控制的重要任务包括 logrotate、makewhatis、locate 和 tmpwatch。

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- anacron
- anacrontab 文件
- cron
- crontab 文件

## 附加信息来源

如果您想进一步了解本章介绍的主题，应参考 `crond`、`crontab(1)` 和 `crontab(5)` 的 man 手册。

## 复习题

1. 以下哪个时间规范定义了一个在每周日下午 4:15 执行的 cron 任务？
    A. 15 16 * * 0
    B. 15 16 * * * 7
    C. 15 16 * * sun
    D. 15 16 * * SUN

2. 以下哪个时间规范定义了一个在每月 1 日、15 日以及每周五晚上 8:00 执行的 cron 任务？
    A. 0 20 * * *
    B. 0 20 * * 5
    C. 0 20 1,15 * *
    D. 0 20 1,15 * 5

3. 在 crontab 文件中可以设置以下哪个环境变量？
    A. EDITOR
    B. HOME
    C. LOGNAME
    D. SHELL

4. 要在 cron 命令中嵌入换行符，必须指定以下哪个符号？
    A. 插入符 (^)
    B. 井号 (#)
    C. 换行转义序列 (\n)
    D. 百分号 (%)

5. 如果一个软件包需要 `cron` 服务，其 `crontab` 位于哪里？
    A. `/etc/cron.d`
    B. `/etc/cron.hourly` 或每日、每周、每月 `cron` 目录
    C. `/etc/crontab`
    D. `/var/spool/cron`

6. 要指定一个新的系统 `crontab` 条目，您应该怎么做？
    A. 编辑 `/etc/crontab` 文件
    B. 执行命令 `crontab -e`
    C. 以 root 身份执行命令 `crontab -e`
    D. 在 `/etc/cron.*` 目录中放置一个脚本或符号链接



## 复习题答案

- 1. A, B, C, D。星期几可以用数字或名称指定，且不区分大小写。数值 0 和 7 都表示星期日。
- 2. D。当月份或星期其中之一匹配时，命令就会执行。
- 3. A, B, D。HOME、LOGNAME 和 SHELL 具有默认值。LOGNAME 的值无法更改。你可以自由定义额外的环境变量，例如 EDITOR。
- 4. D。cron 命令中的百分号会被替换为换行符。
- 5. A。软件包将个人 crontab 文件安装在 `/etc/cron.d` 中。
- 6. A, D。系统管理员不使用 crontab 来修订系统 crontab 文件。

# 第 17 章：理解内核

## 本章涵盖的 RHCE 准备主题：

- 理解基本的内核概念，例如宏内核与模块化内核。
- 能够安装用于重新构建 Linux 内核的内核源码和开发工具。

Red Hat Linux 的核心组件是 Linux 内核。本章解释了基本的内核概念，如宏内核（monolithic）和模块化内核（modular）。它还解释了操作可加载内核模块的基本命令，并识别和描述了重新构建 Linux 内核所需的软件包和工具。本章应与下一章结合阅读，下一章将解释如何重新构建 Linux 内核。

## 内核基础

Linux 操作系统以其内核——Linux 内核命名。内核是操作系统的最基本组件。典型内核的大部分内容始终驻留在内存中，而其他操作系统组件则在需要时加载，随后被丢弃。内核管理处理器、内存和设备等系统资源，并提供其他操作系统组件所使用的服务。

与大多数商业操作系统的内核不同，Linux 内核以源码形式分发。这使得系统管理员能够编译自定义内核，以紧密匹配主机系统的独特需求。能够构建自定义内核有望提高系统效率和性能，但如果想实现这些优势，系统管理员必须理解 Linux 内核。

本节解释了基础内核概念，包括：

- 内核版本和版本号
- 内核类型（宏内核和模块化内核）
- 内核相关文件
- 内核源码树及其结构
- 如何从 Linux 内核存档（Linux Kernel Archives）获取并安装非 Red Hat 内核

接下来的章节将解释 Linux 内核模块。

### 内核版本

Linux 内核的发布由三个数字指定——例如，Linux 2.4.3。这些数字被称为：

- 主版本号 (2)
- 次版本号 (4)
- 补丁级别 (3)

新的 *主版本* 每隔几年发布一次，在内核能力和性能方面提供显著改进。然而，由于内核架构可能会随着新主版本的发布而改变，为之前的主版本设计的非内核软件可能需要重新配置甚至修改。

*次版本* 的发布频率比主版本更高。软件通常不需要重新配置或修改即可在内核的新版本上运行。

在任何时间，都有两个 Linux 版本正在开发中。次版本号为偶数的版本被称为 *稳定版本（stable release）*——例如，Linux 2.4.3。稳定内核的开发重点在于修复缺陷而非添加新功能。次版本号为奇数的版本被称为 *开发版本（developmental release）*——例如，Linux 2.5.10。该版本的开发重点是新功能，有时甚至是实验性功能。因此，正如发布名称所暗示的，开发版本往往不如稳定版本稳定。系统管理员通常不在提供非关键功能的计算机上安装开发版本。

构成内核版本号的第三个数字是 *补丁级别（patch level）*。补丁版本的发布频率甚至高于次版本，尤其是开发版本的补丁发布。有时一周内会发布多个补丁。

Linux 内核通过 Linux 内核存档网站 `www.kernel.org` 发布。Red Hat 公司下载发布的内核并将其重新打包为 RPM，以便于分发和安装。Red Hat 公司还对内核进行了特殊配置，并应用了修改和扩展功能的补丁。

除了 Linux 内核的主-次-补丁版本控制外，Red Hat 公司鼓励使用他们所谓的 *额外版本代码（extraversion code）*，用于区分同一内核发布版本的不同配置。正如在下一章中解释的那样，在构建 Red Hat Linux 内核时可以指定一个额外版本代码。额外版本代码的形式为一个顺序数字和一个简短的描述性名称。例如，支持 SMP 的 Linux 2.4.6 内核的第 20 次构建可能被命名为 `2.4.6-20smp`。使用额外版本代码方便在单个系统上拥有多个 Linux 内核。当你构建新内核时，可以在系统中保留旧内核的副本。这样，如果新内核无法正常运行，你可以简单地使用旧内核重启系统，而无需执行更复杂的恢复操作。

许多 Red Hat Linux 用户和系统管理员从不编译 Linux 内核。相反，他们以软件包形式下载并安装内核更新。然而，出于以下原因，你可能希望构建自定义内核：

- 你想配置一个极其安全的系统，因此想禁用可能带来安全风险的不需要的功能。例如，你计划将 Linux 系统用作路由器，因此不需要或不想要标准 Red Hat Linux 内核中的某些功能。
- 你想启用标准 Red Hat Linux 内核中不可用的功能，例如高级路由选项。
- 你想更改运行期间无法配置的运行参数。例如，你想使用超过 1GB 的 RAM，因此需要重新配置用户空间和内核空间内存之间的平衡。
- 你好奇想了解更多关于 Linux 内核的知识。构建自定义内核是一个很好的学习方式。

### 内核类型

最初，Linux 内核是一个 *宏内核（monolithic）*，即驻留在单个文件中的内核。如果你选择，仍然可以构建宏内核，但现在大多数 Linux 内核都是 *模块化（modular）* 内核，驻留在一组被称为 *模块（modules）* 的文件中。模块化 Linux 内核可以在需要时加载模块，并在不再需要时卸载它们。通常，启动期间不需要的任何模块都被编译为模块，而不是整合到内核中。此类模块包括外围设备驱动程序、辅助文件系统等。

表 17.1 总结了宏内核和模块化 Linux 内核的特点。模块化内核更大的灵活性通常超过了宏内核稍快执行速度和稍高安全性带来的优势。

**表 17.1 宏内核与模块化内核**

| 宏内核 | 模块化内核 |
| :--- | :--- |
| 执行速度稍快 | 启动速度稍快 |
| 安全性稍高 | 所需 RAM 较少 |
| | 灵活性更高 |
| | 内核重新构建频率较低 |

> 如果你选择构建并使用宏内核，你应该从 `/etc/rc.d/rc.sysinit` 中删除所有设备探测，并删除模块清理脚本 `/etc/cron.d/kmod`。

### 内核相关文件

即使是宏 Linux 内核也需要几个支持文件。本小节描述了与 Linux 内核相关的主要文件。这些包括：

- 系统启动所需的启动文件
- 安装或构建内核所需的 RPM 软件包文件
- 包含构建内核所需实用工具的 RPM 软件包文件



## 引导文件

Linux 引导文件位于 `/boot` 文件系统中，以便能够被无法访问大容量硬盘上每个扇区的 PC BIOS 代码访问。主要的 Linux 引导文件包括：

- vmlinuz：Linux 内核，可以具有任意名称。通常，名称包含 vmlinuz 或 vmlinuz。如果使用 LILO 引导系统，内核文件名将在 `/etc/lilo.conf` 文件中被引用。
- boot.b：LILO 的第二阶段引导程序。
- initrd：包含 RAM 磁盘的文件，其中包含内核在引导时可用的驱动程序（模块）。从 SCSI 硬盘引导时通常需要它；否则，在正常的系统运行中通常不需要。
- boot.nnnn：在安装 LILO 之前的原始主引导记录（MBR）的备份副本。正常系统运行不需要该文件。名称中的 nnnn 部分是硬盘的十六进制设备号——例如，boot.0300 或 boot.0305。
- System.map：读取 `/proc` 文件系统的实用程序以及用于调试内核的工具所需要的文件。

为了加强对 `/boot` 目录的理解，请完成练习 17.1。

### 练习 17.1
### 检查 /boot 目录

学习 `/boot` 目录的一个好方法就是研究它。检查您系统的 `/boot` 目录，并找到本小节中提到的每个文件。

## 内核 RPM 包

如前所述，Red Hat, Inc. 发布包含 Linux 内核的 RPM 包。Red Hat Linux 的标准安装包括内核软件包，其中包含一个预编译的模块化内核及其相关模块。在 Intel 386 平台上，标准安装还包括 `kernel-pcmcia-cs` 软件包，其中包含支持 PCMCIA 卡所需的守护进程和驱动程序。

要构建自定义内核，您必须安装两个包含内核源码的软件包：

- `kernel-source`
- `kernel-headers`

要安装这些软件包，请进入包含它们的目录并执行以下命令：

```bash
rpm -Uvh kernel-source-*.i386.rpm kernel-headers-*.i386.rpm
```

安装后，这些软件包的文件位于 `/usr/src/linux-version` 中，其中 `version` 是软件包中所含 Linux 内核的版本。如果您想在不安装体积较大的内核源码和头文件的情况下查看内核文档，可以安装 `kernel-doc` 软件包。该软件包包含通常位于 `/usr/src/linux/Documentation` 的内核文件，但它将它们放置在 `/usr/doc` 中。

如果您更喜欢使用源码 RPM 包进行操作，可以安装 `kernel-source-version.src.rpm` 软件包，其中 `version` 是软件包中所含 Linux 内核的版本号。该软件包包含在 `www.kernel.org` 上发布的源码文件，以及 Red Hat, Inc. 应用的补丁。该软件包将源码文件安装在 `/usr/src/redhat` 目录中。

要详细了解内核源码，请完成练习 17.2。

### 练习 17.2
### 安装内核源码

为了进一步了解 Linux 内核源码，您应该安装并研究它们。

1. 如果您之前尚未安装 Linux 内核源码，请安装 `kernel-source`、`kernel-headers` 和 `kernel-doc` 软件包。
2. 检查 `/usr/src/linux` 目录及其子目录。

## 实用工具

要构建 Linux 内核，您必须拥有 C 编译器、特定的软件开发实用工具和特定的库。所需的软件包包括：

- `egcs-version.i386.rpm`：GNU C 编译器
- `cpp-version.i386.rpm`：GNU C 预处理器
- `dev86-version.i386.rpm`：80x86 汇编器和链接器
- `make-version.i386.rpm`：GNU make 实用工具
- `glibc-devel-version.i386.rpm`：标准 C 库的头文件和库
- `ncurses-version.i386.rpm`：ncurses 库，为字符模式视频显示提供独立于终端的应用编程接口
- `ncurses-devel-version.i386.rpm`：使用 ncurses 开发所需的头文件和库（仅在使用 `menuconfig` 实用工具构建内核时需要）

在每种情况下，*version* 代表软件包的版本号。要安装这些软件包，请进入包含它们的目录并执行以下命令：

```bash
rpm -Uvh egcs-*.i386.rpm \
cpp-*.i386.rpm \
dev86-*.i386.rpm \
make-*.i386.rpm \
glibc-devel-*.i386.rpm \
ncurses-*.i386.rpm \
ncurses-devel-*.i386.rpm
```

现在，通过完成练习 17.3 为构建内核做好准备。

### 练习 17.3
### 安装构建内核所需的工具

在本章的剩余部分，您将学习如何构建一个新内核。为了准备构建内核，您应该安装必要的工具。

1. 确定构建内核所需的工具中，哪些已经存在于您的系统中。
2. 安装任何尚未安装的工具。

目前，您可以回顾识别软件包并展示如何安装它们的 `rpm` 命令。但在参加 RHCE 考试之前，请确保能够无需参考书籍或备忘单即可安装这些工具。

## 内核源码树

如前所述，包含 Linux 内核源码的 RPM 软件包将其文件安装在 `/usr/src` 目录中。二进制 RPM 将其文件放在 `linux-version` 子目录中（例如 `linux-2.4.2`），而（可选的）源码 RPM 将其文件放在 `redhat` 子目录中。为了方便起见，`kernel` 软件包的安装脚本创建了符号链接 `/usr/src/linux`，它指向 `/usr/src/linux-version` 目录。该目录包含大约二十个文件和目录；表 17.2 描述了其中几个最重要的部分。

| 文件或目录 | 描述 |
| :--- | :--- |
| `arch/i386/config.in` | 当前内核配置选项，由内核配置程序或脚本编写 |
| `arch/i386/boot/bzImage` | 编译后的内核镜像 |
| Documentation | 包含各种有用文档的目录 |
| README | Linux 内核的 README 文件 |

现在花几分钟时间完成练习 17.4，它将引导您探索 Linux 源码树。

### 练习 17.4
### 探索 Linux 源码树

知道如何找到重要文件将在 RHCE 考试期间为您节省大量时间。请按照以下步骤让自己更熟悉 Linux 源码树：

1. 如果您之前尚未安装 Linux 内核源码，请安装 `kernel-source`、`kernel-headers` 和 `kernel-doc` 软件包。
2. 检查 `/usr/src/linux` 目录及其子目录。找到表 17.2 中列出的每个文件和目录。

## 安装内核 `tar` 文件

如果您想从尚未被 Red Hat, Inc. 封装为 RPM 的源码构建内核，可以从 Linux 内核存档网站 `www.kernel.org` 下载 `tar` 文件。将文件下载到 `/usr/src` 目录，然后通过执行以下命令进行安装：

```bash
cd /usr/src
mkdir linux-version
rm linux
ln -s linux-version linux
tar zxvf linux-version.tar.gz
```

其中 `version` 是 `tar` 文件中所含 Linux 内核的版本。文件安装完成后，您可以按照下一章给出的步骤构建内核。

一些内核存档使用 BZIP 工具压缩内核，这可以产生更小的存档文件。有关使用 BZIP 工具的说明，请参阅其 man 手册页。

## 内核模块

内核模块是包含动态可加载内核组件（如设备驱动程序）的文件。Linux 2.0 需要外部协助来加载和卸载模块；然而，Linux 2.2 引入了 `kmod` 线程，可以在需要时自动加载模块。

本节描述了内核模块所在的位置、内核模块配置文件 `/etc/conf.modules` 以及管理内核模块的主要命令：

- `depmod`：创建描述模块依赖关系的数据库
- `lsmod`：列出已加载的模块
- `modprobe`：加载内核模块
- `rmmod`：卸载内核模块



### 模块位置

要查看运行内核的版本号和额外版本号（extraversion code），请执行以下命令：

```bash
uname -r
```

该命令的输出仅包含内核版本号和额外版本号。例如：

```
2.4.5-15
```

与该示例内核相关的模块位于 `/lib/modules/2.4.5-15`。

内核模块目录包含几个子目录。通常包括：

- **block**：包含与块设备相关的模块
- **cdrom**：包含与 CD-ROM 设备相关的模块
- **fs**：包含与文件系统相关的模块
- **ipv4**：包含与 TCP/IP 网络相关的模块
- **misc**：包含多种类型的模块
- **net**：包含与网络相关的模块
- **pcmcia**：包含与 PCMCIA 支持相关的模块
- **scsi**：包含与 SCSI 设备相关的模块
- **video**：包含与视频及其设备相关的模块

内核模块子目录本身可能包含一个或多个子目录。

### 列出已加载模块：lsmod

要查看当前加载了哪些模块，请执行 `lsmod` 命令，它会列出常驻内存的模块。以下是 `lsmod` 命令的典型输出：

```bash
# lsmod
Module              Size  Used by
vmnet               14856 3
vmppuser           5156 0 (unused)
parport_pc        5012 0 [vmppuser]
parport           7092 0 [vmppuser parport_pc]
vmmon           16180 0
nfsd           150936 8 (autoclean)
lockd            30856 1 (autoclean) [nfsd]
sunrpc           52356 1 (autoclean) [nfsd lockd]
3c90x            21596 2 (autoclean)
nls_cp437         3548 1 (autoclean)
msdos             8220 1 (autoclean)
fat              25664 1 (autoclean) [msdos]
emu10k1          59490 0
soundcore         2372 4 [emu10k1]
```

该命令的输出报告了：

- 每个模块的名称
- 每个模块的大小
- 模块被使用的计数
- 引用该模块的其他模块名称

既然你已经了解了 lsmod 命令，请完成练习 17.5。

#### 练习 17.5：查看已加载模块

lsmod 命令使用简单，且在管理模块时非常有帮助。为了更好地熟悉该命令，请使用它来识别你系统中常驻的模块。

### 卸载空闲模块：rmmod

当一个模块空闲时间不超过 10 分钟时，`/etc/cron.d/kmod` 定时任务将卸载它（除非你禁用了该任务）。不过，你可以随时通过执行以下命令来卸载空闲模块：

```
rmmod module
```

其中 *module* 是你想要卸载的空闲模块的名称。你可以指定多个模块，每个模块名之间用一个或多个空格分隔。指定多个模块的顺序无关紧要；`rmmod` 命令会同时移除这些模块。如果一个模块正在被使用或被已加载的模块引用，则无法将其移除。要移除所有空闲模块，请执行命令：

```
rmmod -a
```

为了获得操作模块的实践经验，请完成练习 17.6。

#### 练习 17.6：卸载声音驱动

通常不需要卸载模块，但对于 RHCE 考试来说，知道如何操作非常重要。如果你的系统包含已配置的声卡，你可以执行以下步骤来进一步了解模块：

1. 确保没有应用程序正在使用声音适配器。
2. 使用 `lsmod` 识别常驻模块。查看模块名称，判断哪些可能是声音模块。
3. 使用 `rmmod` 卸载声音模块。由于某些模块被其他模块使用，你可能会发现无法以任意顺序卸载模块。如果某个模块无法卸载，请尝试另一个。持续尝试直到删除所有声音模块。

### 加载模块：modprobe 和 insmod

要加载模块，请执行如下形式的命令：

```
modprobe module.o
```

或者更简单地：

```
modprobe module
```

其中 *module.o* 是包含已编译模块的对象文件名。如果模块接受或需要参数，请在命令行中包含它们——例如：

```
modprobe fancycard.o irq=11 align=no
```

如果指定的模块需要其他模块，`modprobe` 将通过搜索由 `depmod` 命令（在后续小节中描述）构建的数据库，自动找到并加载它们。

`modprobe` 命令有两种主要操作模式。一种是可以使用单个模块名或一系列候选模块名进行探测。当你指定一个序列且 `modprobe` 成功加载了一个候选模块时，它将停止探测。要启动探测，请执行如下形式的命令：

```
modprobe -t dir pattern
```

其中 *dir* 指定 `/lib/modules/version` 的一个子目录，*pattern* 是指定候选模块文件名称的正则表达式。例如，在当前运行内核版本为 `2.4.5-15` 时，要从 `/lib/modules/2.4.5-15/net` 目录加载模块，请执行命令：

```
modprobe -t net '.*'
```

在另一种主要操作模式中，`modprobe` 命令尝试加载特定目录中包含的每一个候选模块。例如，要尝试加载 `/lib/modules/2.4.5-15/misc` 目录中的每个模块，请执行命令：

```
modprobe -a -t misc '.*'
```

当然，你不太可能想要尝试加载所有模块。相反，你应该指定一个仅能识别相关模块文件的模式。

与 `modprobe` 命令类似，`insmod` 命令也可以加载内核模块。然而，`insmod` 命令不会尝试加载依赖模块。因此，`modprobe` 命令更为常用，除非在那些以自己的方式处理模块依赖而非依赖 `modprobe` 的脚本中（例如在系统启动期间执行的脚本，此时模块依赖数据库可能尚未更新）。如果你的 Linux 系统包含声音适配器，请完成练习 17.7 以获得加载驱动的实践经验。

#### 练习 17.7：加载驱动程序

为了配置 Linux 系统以使用新的硬件设备，通常必须加载一个充当该设备驱动程序的模块。有时需要加载一个提供特殊功能的模块，例如 FTP 传输的 IP 伪装（IP masquerading）。如果你的系统有声音适配器，你可以进行此练习，练习操作模块。

你可以回顾本章内容和练习 17.6 的结果来获得帮助。但在参加 RHCE 考试之前，请确保你知道如何在没有书籍或笔记帮助的情况下加载模块。

### 更新模块依赖数据库：depmod

`modprobe` 命令能够正确识别依赖于其他模块的模块并将它们作为一组加载，这非常方便。然而，正常运行依赖于拥有一个最新的模块列表，该列表标识了每个模块所需的其他模块。`depmod` 命令构建一个包含此信息的数据库。`/etc/rc.d/rc.sysinit` 脚本在系统启动时每次都会调用 `depmod` 命令来建立这样一个数据库。执行的命令形式为：

```
depmod -a
```

这将完全重建模块数据库。

### 配置模块：/etc/conf.modules 文件

`/etc/conf.modules` 文件允许你指定各种参数来控制 `depmod` 和 `modprobe` 的运行。例如，你可以指定：

- 别名（Aliases），让你能用更方便的名称来引用模块
- 模块加载时要传递的默认参数
- 模块加载或卸载时要执行的 Shell 命令

这是一个典型的 `/etc/conf.modules` 文件：

```
alias sound emu10k1
alias parport_lowlevel parport_pc
alias eth0 3c90x
alias eth1 3c90x
options opl3 io=0x388
pre-install emu10k1 insmod soundcore
post-remove emu10k1 rmmod soundcore
```

该文件定义了四个别名。例如，它允许将 emu10k1 模块引用为 `sound`。它定义了加载 opl3 模块时传递的一个选项；该选项指定输入/输出端口为 0x388。最后，它指定了 emu10k1 模块加载时（`pre-install`）和卸载时（`post-remove`）执行的命令。

`/etc/conf.modules` 文件可以包含以下类型的行：

- 形式为 `parameter = value` 的参数定义行。参数定义行定义一个参数并将其绑定到指定值。允许以下类型的参数定义：
    - `depfile=directory`：指定由 `depmod` 生成的模块依赖数据库的位置。
    - `path=directory`：指定用于搜索模块的目录。
    - `path[type]=directory`：指定包含指定类型模块的目录。`type` 的值可与 `modprobe` 命令的 `-t` 参数一起使用。

默认情况下，模块配置包含以下列表所示的路径和选项。

#### 默认模块配置选项

```
depfile=`/lib/modules/`uname -r`/modules.dep
path[boot]=/lib/modules
path[fs]=/lib/modules/`uname -r`
path[misc]=/lib/modules/`uname -r`
path[net]=/lib/modules/`uname -r`
path[scsi]=/lib/modules/`uname -r`
path[cdrom]=/lib/modules/`uname -r`
path[ipv4]=/lib/modules/`uname -r`
path[ipv6]=/lib/modules/`uname -r`
path[sound]=/lib/modules/`uname -r`
path[fs]=/lib/modules/default
path[misc]=/lib/modules/default
```



```
path[net]=/lib/modules/default
path[scsi]=/lib/modules/default
path[cdrom]=/lib/modules/default
path[ipv4]=/lib/modules/default
path[ipv6]=/lib/modules/default
path[sound]=/lib/modules/default
path[fs]=/lib/modules
path[misc]=/lib/modules
path[net]=/lib/modules
path[scsi]=/lib/modules
path[cdrom]=/lib/modules
path[ipv4]=/lib/modules
path[ipv6]=/lib/modules
path[sound]=/lib/modules
```

- 形式为 `options module symbol=value` 的选项行，其中 `module` 指定模块名称，`symbol` 指定模块已知的参数，`value` 指定该参数的值。选项行指定要发送给模块的参数。可以指定多组符号和值；每组之间用一个或多个空格隔开。

- 形式为 `alias alias_name actual_name` 的别名行。别名行为模块建立一个别名或替代名称。

- 形式为 `pre-install module command` 的预安装行。预安装行指定在安装指定模块之前要执行的命令。

- 形式为 `install module command` 的安装行。安装行指定用于安装指定模块的执行命令。

- 形式为 `post-install module command` 的后安装行。后安装行指定在安装指定模块之后要执行的命令。

- 形式为 `pre-remove module command` 的预卸载行。预卸载行指定在移除指定模块之前要执行的命令。

- 形式为 `remove module command` 的卸载行。卸载行指定用于移除指定模块的执行命令。

- 形式为 `post-remove module command` 的后卸载行。后卸载行指定在移除指定模块之后要执行的命令。

- 形式为 `keep` 的保持行。保持行表示由参数行指定的任何路径应作为默认模块路径的补充，而不是替代。

`/etc/conf.modules` 文件还可以包含注释。空行以及井号 (#) 之后的所有文本都会被忽略。

现在，完成练习 17.8，该练习将探讨 `/etc/conf.modules` 文件。

#### 练习 17.8：检查 /etc/conf.modules 文件

检查系统中的 `/etc/conf.modules` 文件。确保你理解并能够解释其内容。根据需要参考本章和其他信息（如内核文档）。在参加 RHCE 考试之前，请确保你大致理解 `/etc/conf.modules` 文件的功能和结构。

## 总结

在本章中，你学习了 Red Hat Linux 内核。涵盖的最重要主题包括：

- **Linux 内核编号**：Linux 内核有一个形式为 x.y.z 的相关编号，其中 x 是主版本号，y 是次版本号，z 是补丁级别版本。
- **内核类型**：次版本号为偶数的内核是稳定版内核。次版本号为奇数的内核是开发版内核。
- **额外版本代码 (Extraversion Code)**：Red Hat 公司建议使用形式为 x.y.z-c 的内核编号，其中 x 是主版本号，y 是次版本号，z 是补丁级别，c 是额外版本代码。额外版本代码让你能够区分主版本号、次版本号和补丁号相同但编译选项不同的内核。
- **内核类型**：单体内核 (Monolithic kernel) 由单个加载模块组成。模块化内核 (Modular kernel)，如 Linux 内核，包含可在需要时加载的模块。模块化内核比单体内核更紧凑、更灵活。
- **内核相关文件、目录和软件包**：可引导的 Linux 内核及其相关文件通常位于 `/boot`。Linux 内核的源代码位于 `/usr/src/linux`。内核配置选项存储在 `/usr/src/linux/arch/i386/config.in` 文件中，编译后的内核被写入到 `/usr/src/linux/arch/i386/boot/bzImage`。

要编译 Linux 内核，你应该安装几个软件包，包括 `kernel-source`、`kernel-headers`、`egcs`、`cpp`、`dev86`、`make`、`glibc-devel`、`ncurses`、`ncurses-devel`。

**内核模块**：内核模块配置文件是 `/etc/conf.modules`。处理内核模块的重要命令包括 `depmod`、`lsmod`、`modprobe`、`rmmod` 和 `uname`。

### 关键术语

在进入下一章之前，请确保你熟悉以下术语：

- 开发发行版 (developmental release)
- 额外版本代码 (extraversion code)
- 主版本 (major versions)
- 次版本 (minor versions)
- 模块化的 (modular)
- 模块 (modules)
- 单体 (monolithic)
- 补丁级别 (patch level)
- 稳定发行版 (stable release)

## 补充信息来源

如果你想了解本章所呈现主题的更多信息，应参考以下来源：

- `/usr/src/linux/Documentation` 中的 Linux 内核文档
- 操作模块的命令手册页：`lsmod`、`rmmod`、`modprobe`、`depmod`

## 复习题

1. 与模块化 Linux 内核相比，关于单体 Linux 内核，以下哪项通常是正确的？
   A. 启动速度更快。
   B. 执行速度更快。
   C. 占用更少的 RAM。
   D. 更加灵活。

2. Linux 2.4.5-6 的次版本号是多少？
   A. 2
   B. 4
   C. 5
   D. 6

3. 以下哪个内核是稳定发行版开发树的一部分？
   A. 2.4.5-test
   B. 2.4.6-stable
   C. 2.5.5-test
   D. 2.5.6-stable

4. 哪个命令可以显示正在运行的 Linux 内核的版本号？
   A. dmesg
   B. motd
   C. uname
   D. w

5. 以下哪个命令加载名为 heavy 的模块？
   A. depmod heavy
   B. insmod heavy
   C. load heavy
   D. modprobe heavy

6. 以下哪个正确指定了 Linux 内核的常用名称？
   A. /boot/bzImage
   B. /boot/kernel
   C. /boot/vmlinuz
   D. /boot/vmlinux

7. 以下哪个 `/etc/conf.modules` 行指定了加载模块时要使用的命令？
   A. path=
   B. pre-install
   C. install
   D. post-install

## 复习题答案

1. B. 单体内核不使用可加载模块与设备通信，因此执行速度比模块化内核稍快。但它们体积更大，因此启动速度较慢。而且灵活性差得多。

2. B. 主版本号是 2。次版本号是 4。补丁级别是 5。额外版本代码是 6。

3. A, B. 稳定版内核的次版本号为偶数。

4. C. `uname -r` 命令显示内核版本信息。

5. B, D. `insmod` 或 `modprobe` 命令均可用于加载模块。然而，`insmod` 命令不会自动加载指定模块所需的其他模块。

6. C. Linux 内核的常用名称是 `/boot/vmlinuz`；不过，文件名是任意的。

7. C. `install` 行指定了用于加载模块的命令。

# 第 18 章：配置、构建和安装自定义内核

本章涵盖的 RHCE 准备主题：

- 能够从源码配置、构建和安装 Linux 内核及模块。
- 熟悉与将 Red Hat Linux 用作路由器相关的内核配置问题。

曾几何时，构建自定义内核是 Unix 系统管理员的必经之路。如今，构建 Linux 内核相对简单。本章解释了配置、构建和安装自定义 Linux 内核的步骤。

## 配置内核

本节及其后续章节将解释配置、构建和安装 Linux 内核的步骤。为了帮助你掌握进度，在流程上重要的子章节都标有步骤编号，指示其在以下整体过程中的位置：

1. 切换到内核源码目录。
2. 恢复默认配置（可选）。
3. 定义额外版本代码。
4. 指定内核配置选项。
5. 构建内核和模块。
6. 安装内核和模块。
7. 创建引导驱动 RAM 磁盘 (ramdisk)。
8. 修订 LILO 配置。
9. 创建新的引导磁盘。



### 步骤 #1：切换到内核源码目录

配置内核（就像构建和安装内核一样）是在内核源码树的根目录 `/usr/src/linux` 中完成的。要开始配置内核，您应该切换到该目录：

```bash
cd /usr/src/linux
```

### 步骤 #2：恢复默认配置

如果您已经在本地主机上构建过内核，您可能只想微调内核配置。但是，如果您之前从未构建过内核，则应恢复默认的 Red Hat Linux 内核配置。为此，请执行以下命令：

```bash
cp configs/kernel arch/i386/defconfig
make mrproper
make oldconfig
```

其中 `kernel` 是 configs 目录中与您希望作为新内核基础的标准内核相对应的文件名。`make mrproper` 命令会删除旧的配置文件和之前构建的结果。`make oldconfig` 命令会加载 `config.in` 文件，并参考 `defconfig` 文件来确定参数的默认值。

### 步骤 #3：定义 Extraversion 代码

如前一章所述，Red Hat, Inc. 建议您定义一个 `extraversion` 代码，用于区分相同版本但配置不同的内核。为此，请编辑 `/usr/src/linux/Makefile` 文件。该文件的前几行应类似于以下内容：

```text
VERSION = 2
PATCHLEVEL = 2
SUBLEVEL = 12
EXTRAVERSION = -20
```

在第四行的 `-20` 之后添加一些描述性文本，该数字指定了 Red Hat 的构建版本号。例如，如果新内核支持无线访问协议 (WAP)，您可以将该行修改为：

```text
EXTRAVERSION = -20WAP
```

extraversion 代码由 `uname` 报告，并决定内核模块安装到 `/lib/modules` 的哪个子目录中，从而防止相似内核的模块之间发生冲突。

### 步骤 #4：指定内核配置选项

内核配置选项位于 `/usr/src/linux/.config` 文件中。原则上，您可以使用文本编辑器修改此文件。然而，Linux 提供了三个实用程序，使内核配置变得简单得多：

- config
- menuconfig
- xconfig

要使用其中一个实用程序，请执行如下形式的命令：

```bash
make utility
```

其中 `utility` 是这三个实用程序之一的名称。

`config` 实用程序是三者中最古老的。它是一个基于文本的问答式实用程序，包含在许多 Linux 发行版中。然而，大多数用户发现它使用起来很笨拙。一个显著的缺点是 `config` 没有办法在输入响应后进行修改。因此，如果您发现响应错误，必须退出该过程（通过输入 Ctrl+C）并重新开始。`config` 提供的对话框类似于以下内容：

```text
# make config
rm -f include/asm
( cd include ; ln -sf asm-i386 asm)
/bin/sh scripts/Configure arch/i386/config.in
#
# Using defaults found in .config
#
*
* Code maturity level options
*
Prompt for development and/or incomplete code/drivers
(CONFIG_EXPERIMENTAL) [Y/n/?]
*
* Processor type and features
*
Processor family (386, 486/Cx486, 586/K5/586/i686,
Pentium/K6/TSC, PPro/6x86MX] [386]
  defined CONFIG_M386

Maximum Physical Memory (1GB, 2GB) [1GB]
  defined CONFIG_1GB

Math emulation (CONFIG_MATH_EMULATION) [Y/n/?] n

MTRR (Memory Type Range Register) support (CONFIG_MTRR) [Y/n/?]

Symmetric multi-processing support (CONFIG_SMP) [N/y/?]

*
* Loadable module support
*

Enable loadable module support (CONFIG_MODULES) [Y/n/?]

Set version information on all symbols for modules
(CONFIG_MODVERSIONS) [Y/n/?]

Kernel module loader (CONFIG_KMOD) [Y/n/?]

*
* General setup
*

Networking support (CONFIG_NET) [Y/n/?]

PCI support (CONFIG_PCI) [Y/n/?]

PCI access mode (BIOS, Direct, Any) [Any]
  defined CONFIG_PCI_GOANY

PCI quirks (CONFIG_PCI_QUIRKS) [Y/n/?]

PCI bridge optimization (experimental)
(CONFIG_PCI_OPTIMIZE) [N/y/?]

Backward-compatible /proc/pci (CONFIG_PCI_OLD_PROC) [Y/n/?]

MCA support (CONFIG_MCA) [N/y/?]

SGI Visual Workstation support (CONFIG_VISWS) [N/y/?]

System V IPC (CONFIG_SYSVIPC) [Y/n/?]

BSD Process Accounting (CONFIG_BSD_PROCESS_ACCT) [Y/n/?]

Sysctl support (CONFIG_SYSCTL) [Y/n/?]

Kernel support for a.out binaries (CONFIG_BINFMT_AOUT) [M/n/y/?]

Kernel support for ELF binaries (CONFIG_BINFMT_ELF) [Y/m/n/?]

Kernel support for MISC binaries (CONFIG_BINFMT_MISC) [M/n/y/?]

Kernel support for JAVA binaries (obsolete)
(CONFIG_BINFMT_JAVA) [M/n/y/?]

Parallel port support (CONFIG_PARPORT) [M/n/y/?]
```

当然，这只是实际对话的一小部分。

`menuconfig` 实用程序是系统管理员的最爱。与 `config` 一样，它具有基于文本的界面，因此可以远程使用——例如，通过 `telnet` 或 `ssh` 连接。然而，正如其名，`menuconfig` 提供了基于菜单的界面，让您能够循环浏览配置选项，直到达到您认可的配置。因此，它比 `config` 实用程序好用得多。它还包含一个非常有用的帮助设施，用于解释所选的配置选项。图 18.1 显示了 `menuconfig` 实用程序的主屏幕。

#### 图 18.1 menuconfig 的主菜单
![](img/4eef9c6f2f52b608eba628cf4e2793ce_442_0.png)

如果主机系统支持 X，您可以使用 `xconfig` 实用程序。`xconfig` 实用程序具有美观且易于使用的界面，完全支持鼠标或其他 X 支持的指针设备。与 `menuconfig` 一样，它也提供了帮助设施。图 18.2 显示了 `xconfig` 实用程序的主屏幕。

#### 图 18.2 xconfig 屏幕
![](img/4eef9c6f2f52b608eba628cf4e2793ce_443_0.png)

本节的其余子章节将简要解释 Linux 内核提供的配置选项。将相对更多地关注您更可能接触到的配置选项，特别是那些您在 RHCE 考试练习中可能需要用到的选项。

许多配置选项提供三种选择：

- Yes，将该选项的支持插入内核
- No，省略该选项的支持
- Module，编译一个提供该选项支持的可加载模块

响应通常简写为 *y* (yes)、*n* (no) 和 *m* (module)。通常，对于启动时需要的选项应响应 *y*，对于运行期间需要或未来可能需要的选项响应 *m*，对于其他选项响应 *n*。如果您响应 *y* 或 *m*，则认为该选项已启用。

## 代码成熟度级别 (Code Maturity Level)

图 18.3 显示了 `xconfig` 的代码成熟度级别选项屏幕。如果您使用 `config` 或 `menuconfig`，也可以访问相同的选项。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_444_0.png)

您通常应该启用“Prompt for Development and/or Incomplete Code/Drivers”。一些 Linux 设施（如 NFS）如果没有开发代码提供的支持，可能无法正常运行。

## 处理器类型和特性 (Processor Type and Features)

`xconfig` 的处理器类型和特性屏幕如图 18.4 所示。您通常应该：

- 选择包含您系统 CPU 的最高处理器系列。
- 关闭数学模拟 (math emulation)，除非您的 CPU 是 386 或 486SX。
- 关闭对称多处理支持 (SMP)，除非您的系统主板安装了多个 CPU。

如果您不必要地启用了数学模拟或 SMP，您的内核可能会需要更多的内存，或者您的系统运行速度可能会略微变慢。

### 图 18.4 处理器类型和特性
![](img/4eef9c6f2f52b608eba628cf4e2793ce_444_1.png)

## 可加载模块支持 (Loadable Module Support)

图 18.5 显示了 `xconfig` 的可加载模块支持屏幕。您通常应使用它来启用可加载模块支持。

### 图 18.5 可加载模块支持
![](img/4eef9c6f2f52b608eba628cf4e2793ce_445_0.png)

## 常规设置 (General Setup)

图 18.6 显示了 `xconfig` 的常规设置屏幕。如果您的系统有一个或多个网络接口，您通常应该启用 Networking 选项。如果您的系统主板支持 PCI，您通常应该启用 PCI 支持。



### 图 18.6 常规设置

![](img/4eef9c6f2f52b608eba628cf4e2793ce_446_0.png)

### 即插即用支持

图 18.7 显示了 xconfig 的即插即用（Plug-and-Play）支持界面。如果您的系统包含即插即用卡或并行端口，通常应启用即插即用支持。如果存在或可能存在并行端口设备，请启用对其的支持。

#### 图 18.7 即插即用支持

![](img/4eef9c6f2f52b608eba628cf4e2793ce_446_1.png)

## 块设备

图 18.8 显示了 xconfig 的块设备（Block Devices）界面。使用该界面来启用对已安装或可能安装的块设备（硬盘、CD-ROM 驱动器等）的支持。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_447_0.png)

## 网络选项

图 18.9 显示了 xconfig 的网络选项（Networking Options）界面。使用该界面来启用系统必须支持的网络设施和协议。主要的 IP 相关选项包括：

- 数据包套接字 (Packet socket)
- 内核/用户 netlink 套接字 (Kernel/User netlink socket)
- 路由消息 (Routing messages)
- Netlink 设备仿真 (Netlink device emulation)
- 网络防火墙 (Network firewalls)
- 套接字过滤 (Socket filtering)
- Unix 域套接字 (Unix domain sockets)
- TCP/IP 网络 (TCP/IP networking)
- IP：多播 (IP: multicasting)
- IP：高级路由器 (IP: advanced router)
- IP：内核级自动配置 (IP: kernel level autoconfiguration)
- IP：防火墙 (IP: firewalling)
- IP：防火墙数据包 netlink 设备 (IP: firewall packet netlink device)
- IP：透明代理支持 (IP: transparent proxy support)
- IP：伪装 (IP: masquerading)
- IP：ICMP 伪装 (IP: ICMP masquerading)
- IP：伪装特殊模块支持 (IP: masquerading special modules support)
- IP：ipautofw 伪装支持（实验性）(IP: ipautofw masq support (EXPERIMENTAL))
- IP：ipportfw 伪装支持（实验性）(IP: ipportfw masq support (EXPERIMENTAL))
- IP：ip fwmark 伪装转发支持（实验性）(IP: ip fwmark masq-forwarding support (EXPERIMENTAL))
- IP：伪装虚拟服务器支持（实验性）(IP: masquerading virtual server support (EXPERIMENTAL))
- IP：伪装 VS 表大小（2 的 N 次方）(IP: masquerading VS table size (the Nth power of 2))

您可以使用 `menuconfig` 或 `xconfig` 的帮助功能来详细了解这些选项。如果您计划将主机用作路由器而不是桌面或服务器系统，则应启用 `IP: Advanced Router` 选项；否则，应禁用该选项。

### 图 18.9 网络选项

![](img/4eef9c6f2f52b608eba628cf4e2793ce_448_0.png)

### QoS 和/或公平队列

此选项在 `menuconfig` 中显示在网络选项的末尾，而 `xconfig` 将其显示为一个单独的界面。此选项允许您安装非标准的 IP 数据包调度程序，建议“仅限专家”使用。

### SCSI 支持

图 18.10 显示了 `xconfig` 的 SCSI 支持（SCSI Support）界面。如果系统包含 SCSI 设备，您应该启用相应的选项。

#### 图 18.10 SCSI 支持

![](img/4eef9c6f2f52b608eba628cf4e2793ce_449_0.png)

#### SCSI 低级驱动程序

图 18.11 显示了 `xconfig` 的 SCSI 低级驱动程序（SCSI Low-Level Drivers）界面。这些选项在 `menuconfig` 中作为 SCSI 支持界面的一部分。如果系统包含一个或多个 SCSI 接口，您应该启用相应的支持。如果系统必须从 SCSI 设备启动，您可能更倾向于将支持直接编译进内核而不是作为模块；否则，您必须使用 `mkinitrd` 来准备一个合适的 ramdisk，详见本章后续内容。

#### 图 18.11 SCSI 低级驱动程序

![](img/4eef9c6f2f52b608eba628cf4e2793ce_450_0.png)

## 网络设备支持

图 18.12 显示了 xconfig 的网络设备支持（Network Device Support）界面。如果系统包含一个或多个网络接口，您应该启用相应的支持。

### 图 18.12 网络设备支持

![](img/4eef9c6f2f52b608eba628cf4e2793ce_450_1.png)

##业余无线电支持

业余无线电支持（Amateur Radio Support）界面允许您配置对分组无线电（packet radio）的支持。通常不需要这些选项。

## IrDA 子系统支持

xconfig 的 IrDA 子系统支持（IrDA Subsystem Support）界面如图 18.13 所示，允许您配置对通过红外线与系统通信的设备的支持。通常不需要这些选项。

### 图 18.13 IrDA 子系统支持

![](img/4eef9c6f2f52b608eba628cf4e2793ce_451_0.png)

### 红外端口设备驱动程序

`xconfig` 的红外端口设备驱动程序（Infrared-Port Device Drivers）界面如图 18.14 所示，允许您配置通过红外线与系统通信的设备驱动程序。这些选项在 `menuconfig` 中作为 IrDA 子系统支持界面的一部分，通常不需要。

#### 图 18.14 红外端口设备驱动程序

![](img/4eef9c6f2f52b608eba628cf4e2793ce_452_0.png)

## ISDN 子系统

图 18.15 显示了 `xconfig` 的 ISDN 子系统（ISDN Subsystem）界面。除非系统连接到 ISDN 设备，否则应禁用此选项。许多现代 ISDN 调制解调器通过以太网连接到系统；此类调制解调器不需要 ISDN 支持。

### 图 18.15 ISDN 子系统

![](img/4eef9c6f2f52b608eba628cf4e2793ce_453_0.png)

## 旧版 CD-ROM 驱动程序

图 18.16 显示了 xconfig 的旧版 CD-ROM 驱动程序（Old CD-ROM Drivers）界面。除非系统包含一个或多个使用私有接口（即既不是 IDE 也不是 SCSI）的旧版 CD-ROM 驱动程序，否则应禁用此选项。

### 图 18.16 旧版 CD-ROM 驱动程序

![](img/4eef9c6f2f52b608eba628cf4e2793ce_453_1.png)

## 其他选项

还有几个其他配置选项界面可用，包括：

- 字符设备选项 (Character Device Options)。`menuconfig` 工具将其显示为单个界面；`xconfig` 将其显示为一系列界面：
    - 字符设备 (Character Devices)：允许您配置与虚拟终端、多口串口卡和其他字符模式设备相关的选项。
    - 鼠标 (Mice)：允许您配置鼠标选项。
    - 看门狗卡 (Watchdog Cards)：允许您配置特殊看门狗定时器卡的选项。
    - Linux 视频 (Video for Linux)：允许您配置无线电和电视卡的选项。
    - 摇杆支持 (Joystick Support)：允许您配置摇杆选项。
- 软盘磁带支持 (Floppy Tape Support)：允许您配置对使用软盘接口的磁带驱动器的支持。`menuconfig` 工具将这些选项作为块设备界面的一个部分。
- 文件系统和分区选项 (File System and Partition Options)。`menuconfig` 工具将其显示为单个界面；`xconfig` 将其显示为一系列界面：
    - 文件系统 (File Systems)：允许您配置对文件系统的支持。
    - 网络文件系统 (Network File Systems)：允许您配置对网络文件系统的支持。
    - 分区类型 (Partition Types)：允许您配置对非 Linux（即非 MS-DOS）分区表的支持。
    - 本地语言支持 (Native Language Support)：允许您配置对本地语言扩展的支持。
- 控制台驱动程序 (Console Drivers)：允许您配置与控制台和帧缓冲设备相关的选项。
- 声音 (Sound)：允许您配置对声音的支持。`menuconfig` 工具将其显示为单个界面；`xconfig` 将其显示为两个界面：
    - 声音 (Sound)：允许您配置对声音的支持。
    - 附加低级声音驱动程序 (Additional Low-Level Sound Drivers)：允许您配置声卡驱动程序。
- 内核黑客 (Kernel hacking)：允许您配置对内核测试的支持。启用此选项会降低安全性，因此通常不应启用。

## 步骤 #5：构建内核和模块

要构建内核和模块，请执行以下命令序列：

```
make bzImage
make modules
```

这些命令执行以下操作：

- `make bzImage` 编译内核
- `make modules` 编译可加载模块

这些命令通常需要一些时间执行。因此，您可能更愿意将它们作为一个单条命令执行，这样您就无需一直监控系统以确定何时输入下一条命令。具体操作如下：

```
make bzImage modules
```

在第一次构建内核之后，您可以使用一套替代命令。首先，通过常规方式使用 `make config`、`make menuconfig`、`make xconfig` 或 `make oldconfig` 创建您的内核配置。然后，执行命令：

```
make dep
make clean
make bzImage
make modules
```

或者执行单条命令：

```
make dep clean bzImage modules
```

`make dep` 命令将您的配置选择传播到整个源码树，而 `make clean` 命令则删除之前构建的结果。这两个命令的执行顺序并不重要。其余两条命令具有其通常的作用。



## 第 6 步：安装内核和模块

构建完成后，通过执行以下形式的命令来安装内核和模块：

```
cp /usr/src/linux/arch/i386/boot/bzImage ~/boot/vmlinuz-version
make modules_install
cp /usr/src/linux/System.map /boot/System.map-version
cp /usr/src/linux/.config /boot/config-version
```

其中 *version* 是与新内核关联的版本号和额外版本号（extraversion code）。最后一条命令并非绝对必要，但将内核配置副本与内核一起存储会非常方便。

## 第 7 步：创建启动驱动盘 RAM 磁盘文件

如果系统在启动期间使用 SCSI 或 RAID 设备，您应该创建一个包含相应驱动程序的 RAM 磁盘文件。内核在启动过程中加载 RAM 磁盘文件并根据需要访问驱动程序。

要创建 RAM 磁盘文件，请执行以下形式的命令：

```
mkinitrd /boot/initrd-version.img version
```

其中 *version* 是与新内核关联的版本号和额外版本号。`mkinitrd` 命令会检查模块库 lib，自动选择合适的模块，创建 RAM 磁盘文件，并将模块打包到该文件中。

## 第 8 步：修改 LILO 配置

要启动新内核，通常必须修改 LILO 配置。使用文本编辑器，将以下形式的行添加到 `/etc/lilo.conf` 中：

```
image=/boot/vmlinuz-version
label= vmlinuz-version
root=/dev/xxx
initrd=/boot/initrd-version.img
read-only
```

其中 *version* 是与新内核关联的版本号和额外版本号，*xxx* 是 Linux 系统的根分区。如果您偏好其他标签文本，请为 `label` 指定不同的值。

保存修改后的文件后，运行 LILO 启动映射安装程序：

```
/sbin/lilo -v
```

## 第 9 步：创建新的启动盘

每当您安装新内核时，都应该创建一张包含该内核的新启动盘。为此，请执行以下形式的命令：

```
mkbootdisk -device /dev/fd0 -verbose version
```

其中 *version* 是与新内核关联的版本号和额外版本号。如果您想将内核写入除 `/dev/fd0` 以外的软驱，请指定所需软驱的设备文件；例如 `/dev/fd1`。

创建启动盘后，使用 LILO 启动系统并检查其是否正常运行。如果您无法使用新内核启动系统，请在响应 LILO 提示时指定旧内核的标签，从而使用旧内核启动系统。

现在您可以按照练习 18.1 的步骤来制作自定义内核了。

## 练习 18.1：制作自定义 Linux 内核

创建自定义内核曾是 Linux 用户的“成年礼”。但在学习了本章之后，您应该能够在不丧失理智的情况下编译自定义内核。您应该遵循的流程如下：

- 1. 创建一个 Linux 启动盘并进行测试，确保它能成功启动您的系统。
- 2. 根据您的喜好配置 Linux 内核选项，只要这些选项与您的系统硬件不冲突即可。
- 3. 构建并安装内核，为新内核创建 RAM 磁盘和启动盘。
- 4. 在 LILO 配置中安装新内核，并保留新内核。
- 5. 检查新内核，确保您可以启动它且系统运行正常。
- 6. 检查您是否可以使用 LILO 启动旧内核。

根据需要，回顾本章和其他文档，特别是关于内核选项的描述。如果新内核无法工作，请使用 LILO 或包含原始内核的启动盘来恢复您的系统。

在参加 RHCE 考试之前，您应该能够在不需要查阅本书或其他帮助的情况下构建自定义内核。

## 总结

在本章中，您学习了如何构建自定义内核。涵盖的最重要课题包括：

**编译和安装内核** 编译和安装内核涉及的步骤为：

- 1. 切换到内核源码目录。
- 2. 恢复默认配置（可选）。
- 3. 定义额外版本号（extraversion code）。
- 4. 指定内核配置选项。
- 5. 构建内核和模块。
- 6. 安装内核和模块。
- 7. 创建启动驱动 RAM 磁盘。
- 8. 修改 LILO 配置。
- 9. 创建新的启动盘。

**内核配置选项** 内核配置选项的主要类别包括：

- 代码成熟度级别 (Code Maturity Level)
- 处理器类型和特性 (Processor Type and Features)
- 可加载模块支持 (Loadable Module Support)
- 通用设置 (General Setup)
- 即插即用支持 (Plug-and-Play Support)
- 块设备 (Block Devices)
- 网络选项 (Networking Options)
- QoS 和/或公平队列 (QoS and/or Fair Queueing)
- SCSI 支持 (SCSI Support)
- SCSI 低级驱动程序 (SCSI Low-Level Drivers)
- 网络设备支持 (Network Device Support)
-业余无线电支持 (Amateur Radio Support)
- IrDA 子系统支持 (IrDA Subsystem Support)
- 红外端口设备驱动程序 (Infrared-Port Device Drivers)
- ISDN 子系统 (ISDN Subsystem)
- 旧版 CD-ROM 驱动程序 (Old CD-ROM Drivers)
- 其他选项 (Other Options)

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- 内核 (kernel)
- 额外版本号 (extraversion code)

## 附加信息来源

如果您想进一步了解本章介绍的课题，应参考以下来源：

- *《红帽 Linux 官方参考指南》(The Official Red Hat Linux Reference Guide)*
- Linux 内核存档网站 `www.kernel.org`。
- 内核源码树中的文档文件，特别是 `/usr/src/linux/Documentation` 中的文件。
- Brian Ward 编写的 *《Linux 内核 HOWTO》(The Linux Kernel HOWTO)*，路径为 `/usr/doc/HOWTO/Kernel1-HOWTO`（虽然有些过时，但仍有价值）。

## 复习题

- 1. 内核配置存储在以下哪个文件中？
    A. `/usr/src/linux/.config`
    B. `/usr/src/linux/config.in`
    C. `/usr/src/linux/config`
    D. `/usr/src/linux/linux.cfg`

- 2. 以下哪个内核配置工具可以通过 telnet 连接使用？
    A. `make config`
    B. `make linux`
    C. `make menuconfig`
    D. `make xconfig`

- 3. 如果您对设备驱动程序的提示响应 *m*，结果是什么？
    A. 驱动程序被编译为可加载模块。
    B. 驱动程序被编译为内核的一部分。
    C. 驱动程序不被编译。
    D. 您不能对设备驱动程序的提示响应 *m*。

- 4. 要优化内核使其作为路由器而非主机运行，您应该启用哪个选项？
    A. IP: Advanced Router
    B. IP: Host off
    C. IP: Optimize as Router, Not Host
    D. IP: Router Only

- 5. 定义额外版本号（extraversion code）值的文件是以下哪个？
    A. `/usr/src/linux/make`
    B. `/usr/src/linux/Make`
    C. `/usr/src/linux/makefile`
    D. `/usr/src/linux/Makefile`

- 6. 以下用于安装新内核的典型命令中，哪些是必要的？
    A. `cp /usr/src/linux/.config /boot/config-2.4.5-1r1`
    B. `cp /usr/src/linux/arch/i386/boot/bzImage /boot/vmlinuz-2.4.5-1r1`
    C. `cp /usr/src/linux/System.map /boot/System.map-2.4.5-1r1`
    D. `make modules_install`

- 7. 要创建新的启动盘，您应该执行以下哪个命令？
    A. `mkbootdisk -device /dev/fd0 -verbose 2.4.5`
    B. `mkbootdisk -device /dev/fd0 -verbose 2.4.5-10`
    C. `mkbootdisk /dev/fd0 -verbose 2.4.5`
    D. `mkbootdisk /dev/fd0 -verbose 2.4.5-10`

## 复习题答案

- 1. A. 内核配置存储在隐藏文件 `.config` 中。文件 `config.in` 是作为 `scripts/Configure` 的参数提供的。如果文件 `.config` 不存在，则由 `arch/i386/defconfig` 提供默认值。Red Hat Linux 内核的默认配置存储在 `configs` 中。

- 2. A, C. `config` 和 `menuconfig` 都具有基于文本的用户界面。

- 3. A. 响应 `m` 将驱动程序或其他功能编译为可加载内核模块。

- 4. C. 要配置内核作为路由器而非主机运行，您应该启用 `IP: Optimize as Router, Not Host` 选项。这将禁用主机通常需要但路由器不需要的默认支持。

- 5. D. 额外版本号的值在 `/usr/src/linux/Makefile` 中定义。

- 6. B, C, D. 您必须安装内核、系统映射表（system map）和模块，但不需要安装配置（此处逻辑是指引导必需组件与可选文档的区别）。

- 7. B. 您必须包含 `-device` 参数。版本参数应包含额外版本号，以便命令能够定位正确的内核镜像。



# 第 19 章 管理共享库

### 本章涵盖的 RHCE 准备主题：

- 理解并能够修改加载器配置文件 `/etc/ld.so.conf`。

除了内核和模块，Linux 系统中最重要的部分就是动态加载器及其共享库。几乎每个程序在加载时，都会使用由加载器提供的一个或多个库例程。如果加载器配置错误，程序——甚至是对于系统运行至关重要的 `ls` 等基础命令——都将无法运行。本章将解释共享库以及配置加载器的步骤。

## 共享库概念

C 语言是最常用的编写 Linux 程序的语言。然而，程序员编写的 C 程序不能立即执行，因为计算机不能直接处理 C 程序。相反，计算机要求程序以一种被称为机器语言的形式表达。一台计算机型号所接受的机器语言与其内部架构密切相关，因此通常与其他计算机接受的机器语言不兼容。因此，计算机程序在执行前必须经过转换——通常是一系列转换。图 19.1 展示了这一过程。

> **注意**：用 Perl、Python 或 bash shell 等脚本语言编写的程序可以立即执行。这就是脚本语言与普通编程语言的主要区别。

**图 19.1** 创建并运行程序

程序员编写的程序形式被称为 *源代码*。一个被称为 *编译器* 的特殊程序将源代码转换为被称为 *目标代码* 的形式。目标代码与机器语言非常相似，但与源代码一样，它不可执行。程序员通常不会编写处理通用操作的代码，例如计算文本字符串中的字符数；否则，程序员将不得不一遍又一遍地编写相同的代码。

相反，通用操作被编写一次并组织成 *库*。当程序员需要执行其中一项操作时，只需写入对该库例程的引用即可。这加快了编程过程并减少了编程错误。

一个被称为 *链接器* 的特殊程序将目标代码与必要的库例程结合起来，创建一个 *静态链接* 的可执行程序。静态链接的可执行文件可以直接运行。

静态链接程序有几个缺点。例如，每个使用计算文本字符串字符数库例程的可执行程序都必须包含执行此操作的机器语言指令。如果一个系统包含数千个使用了数十或数百个库例程的程序，那么冗余存储这些例程将浪费大量的磁盘空间。此外，假设在某个库例程中发现了一个错误：每个使用该例程的程序都包含该错误代码。修复此缺陷需要将每个使用错误例程的程序重新链接到修正后的库。

通常，更好的方法是 *动态链接* 程序。动态链接程序不包含其引用的库例程，而是包含特殊的 *存根 (stubs)*，用于指定程序所需的库例程。当动态链接程序加载时，一个特殊的 *动态加载器* 会解析程序的库引用。系统在虚拟内存中保留一份动态加载例程的副本；所有使用该例程的程序共享对该副本的访问权限。

动态链接程序节省了磁盘空间，因为程序不包含库例程的冗余副本。此外，修复有缺陷的库例程只需替换包含它的库即可；随后对该例程的所有引用都将解析到修正后的副本。动态链接程序的运行速度确实稍慢，但这种差异很少显著。

使用 Motif 库的 X 程序通常以静态链接形式分发，但这与性能无关。Motif 库的软件许可限制了其分发。静态链接的可执行文件不会违反该许可。

## Linux 共享库

Linux 可执行程序文件通常使用一种称为 *ELF*（可执行与链接格式）的结构。然而，较旧的可执行文件有时使用一种称为 `.out` 的格式。这种不一致性导致的一个复杂情况是，一些系统库同时以 ELF 和 `.out` 两种格式独立存在。最终，对 `.out` 的支持可能会消失。

Linux 链接器被称为 `/usr/bin/ld`。曾经，Linux 为 `a.out` 文件 (`/lib/ld.so`) 和 ELF 文件 (`/lib/ld-linux.so-1`) 分别设有不同的动态加载器。然而，现在 Linux 使用单一的动态加载器 `/lib/ld-version.so` 来支持这两种文件格式。为了兼容性，Red Hat Linux 同时包含了 Linux 动态加载器的旧版本和新版本。

## 库位置与文件名

Linux 共享库存储在几个目录中，例如：

- `/lib`，主共享库
- `/usr/lib`，补充共享库
- `/usr/i486-linux-libc5/lib`，用于旧版本 C 标准库 `libc5` 的共享库
- `/usr/X11R6/lib`，与 XFree86 相关的共享库
- `/usr/i486-linuxaout/lib`，`a.out` 共享库

静态库文件的名称形式为 `libname.a`，其中 `libname` 是库的名称。动态库文件的命名方式旨在实现与新版本共享库的向上兼容。共享库的名称通常具有 `libname-major.minor.patch.so` 的形式，其中：

- `libname` 是库的名称
- `major` 是库的主版本号
- `minor` 是库的次版本号
- `patch` 是库的补丁级别
- `so` 表示该文件是一个共享库

例如，标准 C 库可能驻留在名为 `libc-2.1.1.so` 的文件中。如果一个库是刚刚发布的，补丁级别或次版本号可能会被省略，文件名将具有 `libname-major.minor.so` 或 `libname-major.so` 的形式。

除了库文件外，还有两个指向库文件的符号链接：

- `libname.so`
- `libname.so.major`

程序是链接到这两个符号链接之一，而不是直接链接到库文件。因此，即使补丁级别或次版本号发生变化，加载器仍能定位所需的库。

## 查看库引用

要确定程序所需的动态库，请运行如下形式的命令：

```
ldd programfile
```

其中 *programfile* 是程序的名称。例如，要确定 `rm` 命令所需的动态库，请运行该命令：

```bash
# ldd /bin/rm
  libc.so.6 => /lib/libc.so.6 (0x40019000)
  /lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
```

示例输出显示 `rm` 命令需要 `libc` 的第 6 版本，并且加载器将此引用解析为 `/lib/libc.so.6`。输出还显示当前 Linux 动态加载器的版本是第 2 版。与例如 `linuxconf` 命令（引用了六个库）相比，`rm` 命令所需的库支持相对较少：

```bash
# ldd /bin/linuxconf
  libm.so.6 => /lib/libm.so.6 (0x40019000)
  libncurses.so.4 => /usr/lib/libncurses.so.4 (0x40035000)
  libdl.so.2 => /lib/libdl.so.2 (0x40072000)
  libcrypt.so.1 => /lib/libcrypt.so.1 (0x40075000)
  libgd.so.1 => /usr/lib/libgd.so.1 (0x400a3000)
  libc.so.6 => /lib/libc.so.6 (0x400d9000)
  /lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x40000000)
```



现在请完成练习 19.1，这将让你获得使用 `ldd` 命令的经验。

## 练习 19.1

## 查看库引用

这是一个简单的谜题，将为你提供使用 `ldd` 命令的机会。使用 `ldd` 命令查看与 `/bin`bin 目录和 `/usr/bin` 目录中任意可执行文件相关的库引用。你能否发现某种能够区分这些可执行文件来源的模式？

### 指定库路径

如果加载器（loader）无法定位程序所需的库，它会打印一条错误消息并停止加载过程。如果该库存在于系统中，你可以通过设置环境变量 `LD_LIBRARY_PATH` 来告知加载器其位置。例如，要指定加载器在 `/usr/local/lib` 和 `/usr/local/otherlib` 目录中搜索所需的库，请执行以下命令：

```bash
export LD_LIBRARY_PATH="/usr/local/lib:/usr/local/otherlib"
```

指定的一个或多个目录将在默认目录之外被搜索，因此无需显式指定默认目录。

### 安装共享库

当你安装包含共享库的 RPM 软件包时，安装脚本应自动更新共享库配置。然而，如果你安装的是非 RPM 软件包，则可能需要手动修改共享库配置。

共享库配置位于 `/etc/ld.so.conf` 文件中，该文件包含一个包含共享库的目录列表，每行一个目录。以下是一个典型的 `ld.so.conf` 文件的内容：

```
/usr/lib
/usr/i486-linux-libc5/lib
/usr/X11R6/lib
/usr/i486-linuxauto/lib
```

请注意，主共享库目录 `/lib` 未列在其中；如果找不到该目录，基本上没有任何命令（包括更新共享库配置所需的命令）能够工作。因此，该库的位置被内置在加载器中，无需在配置文件中指定。

要向共享库配置中添加目录，请使用文本编辑器在 `/etc/ld.so.conf` 中添加一行指定目录名称。然后，执行以下命令：

```bash
ldconfig -v
```

该命令是必要的，因为加载器在 `/etc/ld.so.cache` 文件中保留了目录和库名称的缓存。缓存可以提高性能，但必须通过 `ldconfig` 命令重新构建，以便加载器开始搜索新指定的目录。

### 查找包含共享库的软件包

在安装 RPM 软件包时，你可能会遇到一条错误消息，告知你某个所需的库不可用。不幸的是，包含所需库的软件包名称可能并不明显：在这种情况下，以下这个相当晦涩的命令可能会有所帮助：

```bash
rpm -qp --filebypkg *.rpm \
|grep '\.so' |sort > /tmp/liblist
```

该命令将当前目录下软件包文件中包含的共享库文件列表放入 `/tmp/liblist` 文件中。

在随附光盘中可以找到的“共享库文件所有权表”总结了在 Red Hat Linux 发行版光盘的 RPMs 目录内容上运行此命令的结果。为了准备 RHCE 考试，你不需要熟悉该表的内容，但它将加快需要库支持的软件包的安装速度。

在 Red Hat Linux 6.2 下，你可以通过安装 `rpmdb-redhat` 软件包更简单地访问共享库文件的所有权信息。然后，你可以通过执行以下命令查询替代 RPM 数据库以获取此信息：

```bash
rpm -q --redhatprovides <library pathname>
```

## 总结

在本章中，你学习了关于共享库的知识。涵盖的最重要主题包括：

**程序形式** 程序员编写源代码，编译器将其翻译成目标代码。目标代码可以存储在库中以便重复使用。

**程序链接** 链接器将目标代码模块组合起来创建一个可执行程序。静态链接程序不引用外部库。动态链接程序引用外部库，这些库在程序运行时必须存在。

**Linux 可执行文件** 大多数 Linux 可执行文件使用名为 ELF（可执行与链接格式）的结构组织。较旧的可执行文件可能使用已过时的 `a.out` 结构。

**共享库** 最重要的共享库包括：

- `/lib` 主共享库
- `/usr/lib` 补充共享库
- `/usr/i486-linux-glibc5/lib` 用于旧版本 C 标准库 libc5 的共享库
- `/usr/X11R6/lib` 与 XFree86 相关的共享库
- `/usr/i486-linuxauto/lib` `a.out` 共享库

**`ldd` 命令** `ldd` 命令可让你确定程序引用了哪些共享库。

**库路径** 环境变量 `LD_LIBRARY_PATH` 指定了库的搜索路径。

**共享库配置** 文件 `/etc/ld.so.conf` 包含共享库配置，由已安装库的列表组成。如果你安装非 RPM 软件包或未打包的软件，可能需要修改该文件。

**查询 RPM 软件包文件** 你可以查询 RPM 软件包文件，以确定哪个文件（如果有）包含特定的共享库。

### 关键术语

在进入下一章之前，请确保你熟悉以下术语：

- a.out
- 编译器 (compiler)
- 动态加载器 (dynamic loader)
- 动态链接 (dynamically linked)
- ELF
- 库 (library)
- 链接器 (linker)
- 机器语言 (machine language)
- 目标代码 (object code)
- 源代码 (source code)
- 静态链接 (statically linked)
- 存根 (stubs)

## 其他信息来源

如果你想进一步了解本章介绍的主题，应参考以下资源：

- Daniel Barlow 编写的 *The ELF-HOWTO*，路径为 `/usr/doc/HOWTO/ELF-HOWTO`
- `ldd` 和 `ldconfig` 的 man 手册页

## 复习题

1. 与动态链接相比，静态链接的优点是以下哪个？
    A. 库例程中的错误更容易纠正。
    B. 可执行文件占用更少的磁盘空间。
    C. 库的许可限制可能不适用。
    D. 程序运行速度更快。

2. Linux 可执行文件的主要形式是以下哪个？
    A. a.out
    B. COFF
    C. ELF
    D. iBCS

3. 以下哪个名称是共享库标准符号链接的正确形式？
    A. library.so
    B. library.so.3
    C. library.so.3.2
    D. library.so.3.2.1

4. 以下哪个名称是共享库名称的正确形式？
    A. library.so.1
    B. library.so.1.2
    C. library-1.2.so
    D. library-1.2.3.so

5. 要确定程序访问了哪些共享库，必须执行哪个命令？
    A. ld
    B. ld.so
    C. ldconfig
    D. ldd

6. 建立一组补充库路径的环境变量是以下哪个？
    A. LD_LIBRARY_PATH
    B. LD_SO_PATH
    C. LIBRARY_PATH
    D. SO_PATH

7. 以下哪个目录**没有**出现在共享库配置文件中？
    A. /lib
    B. /lib/i486-linux-libc5/lib
    C. /usr/lib
    D. /usr/lib/lib/X11R6/lib

## 复习题答案

1. C, D。静态链接程序可能不受影响相关库的许可限制。它们的运行速度比动态链接程序略快，但差异很少显著。

2. C。Linux 可执行文件的主要形式是 ELF；一些较旧的可执行文件使用 `a.out` 格式。

3. A, B。符号链接包含库名或库名和主版本号；它不包含次版本号或补丁级别。

4. C, D。共享库的名称必须以 `.so` 结尾，可以省略对次版本号或次版本号和补丁级别的引用。

5. D。`ldd` 命令打印可执行文件所绑定的共享库。

6. A。设置补充共享库搜索路径的环境变量是 `LD_LIBRARY_PATH`。

7. A。`/lib` 目录是必不可少的，因此没有在共享库配置文件中显式列出。



# 第 20 章：在单用户模式和救援模式下工作

本章涵盖的 RHCE 准备主题：

- 能够使用单用户模式和救援模式进行系统恢复。

RHCE 考试的大部分内容要求你能够排除故障并修复损坏的系统配置。为此，你必须以单用户或救援模式启动系统，找到问题并加以解决。本章将解释单用户模式和救援模式的操作，并提供系统故障排除的一般步骤。

## 系统恢复

有时，你尝试启动 Linux 系统，却发现系统无法启动。你可能会看到指向以下问题的错误消息：

- LILO 安装缺失或损坏
- 内核恐慌（Kernel panic）
- 内核缺失或损坏
- 文件系统损坏
- 无法进入运行级别 2、3 或 5
- 根密码未知

要修复系统，你必须能够启动它。除非系统存在硬件问题，否则你可能能够使用单用户模式或救援模式来启动。一旦成功启动系统，你就可以研究其配置文件和日志以确定问题原因，修复问题并重启系统。下一节将解释单用户模式及其恢复步骤。随后的章节将解释救援模式及其恢复步骤。

## 单用户模式

单用户模式提供了一种简单的方法来恢复那些不影响 LILO、内核或根文件系统的问题。非根文件系统、运行级别以及服务失效等问题通常可以在单用户模式下修复。

### 进入单用户模式

要进入单用户模式，在启动提示符处输入 `linux single` 或 `linux emergency`，其中 `linux` 是 LILO 配置文件中与内核关联的标签。如果你更喜欢简短的响应，可以输入 `linux s`，这等同于 `linux single`。

启动参数 `-s`、`single` 或 `emergency` 会传递给 init 进程，系统启动完成后，init 将系统置于单用户模式。如果你指定 `emergency` 参数，`init` 还会省略初始进程的加载；如果你的 `/etc/inittab` 文件配置错误，此选项非常有用。

系统不会提示输入密码，而是直接为你提供一个具有 root 权限的 shell。

由于任何能够访问系统控制台的人都可以以单用户模式启动系统并获得特权访问，因此你应该保持计算机系统良好的物理安全性。或者，你可以配置系统 BIOS 仅从硬盘启动，限制对系统 BIOS 的访问，锁定系统机箱，并配置 LILO 以限制对单用户模式的访问。

### 单用户模式环境

当你按照前一小节所述进入单用户模式时，只有根文件系统被挂载，且 PATH 环境变量可能未设置为其通常的值。因此，你可能需要输入要执行命令的完整路径名。例如，你最初无法访问存储在 `/usr/bin` 和 `/usr/sbin` 中的命令；只有位于 `/bin` 和 `/sbin` 中的命令可用。

### 需检查的配置文件

通常，当系统无法正常启动时，是因为配置错误。你（或另一位系统管理员）在修改配置文件或使用 `linuxconf` 或其他配置实用程序时犯了错误。在寻找问题时，你应该检查以下配置文件：

- `/etc/conf.modules`
- `/etc/fstab`
- `/etc/inittab`
- `/etc/lilo.conf`
- `/etc/rc.d/*`
- `/etc/yp.conf`（如果系统使用网络信息服务 NIS）

请特别注意 `/etc/fstab` 和 `/etc/lilo.conf`，这两个文件如果配置错误，是导致系统启动问题的常见原因。

### 单用户模式的一般步骤

以下是单用户模式的一般故障排除步骤：

1. 通过在启动提示符处输入 `linux s` 进入单用户模式，其中 `linux` 表示要加载的内核镜像关联的标签。
2. 系统启动后，你将进入一个 `bash` shell 会话，此时仅挂载了根分区。
3. 识别可用分区：`fdisk -l`。
4. 检查非根文件系统：`e2fsck -y /dev/xxx`，其中 `xxx` 是根文件系统所在的分区（注：此处原文可能为笔误，应指检查其他分区）。
5. 如果 LILO 损坏或丢失，挂载 `/boot` 分区：`mount /dev/xxx /boot`，其中 `xxx` 是 `/boot` 所在的分区。
6. 查找并修复任何配置错误的文件。务必检查 `/etc/lilo.conf` 和 `/etc/fstab`。
7. 如果 `/etc/lilo.conf` 或内核发生了更改，运行 `lilo` 映射安装程序：`/sbin/lilo`。
8. 重启计算机：`shutdown -r now`。

现在通过完成练习 20.1 来练习在单用户模式下工作。

### 练习 20.1：使用单用户模式

熟练使用单用户模式非常重要，这在 RHCE 考试的故障排除部分可能会非常有用。为了获得使用单用户模式的经验，请执行以下步骤：

1. 以单用户模式启动系统。
2. 识别可用的磁盘分区。
3. 检查非根文件系统的完整性。
4. 挂载 `/boot` 分区并运行 LILO 映射安装程序。
5. 重启系统。

如果你需要回顾本章或查阅其他文档，请随意操作。但在参加 RHCE 考试之前，请确保你能够在不寻求帮助的情况下执行这些操作。

## 救援模式

当你即使在单用户模式下也无法启动系统时，救援模式非常有用。救援模式提供了一个从 ramdisk 镜像获取的根文件系统，因此即使系统硬盘上的任何分区都无法挂载，你依然可以使用常见的 shell 命令。凭借技巧和洞察力，你可以使用这些命令来查找并修复问题。

### 准备救援模式介质

在 Red Hat Linux 6.1 之前，发行版介质中包含 `rescue.img` 文件，其中包含一个适用于挂载为根文件系统的 ramdisk 镜像。要进入救援模式，你必须创建一张包含该 ramdisk 镜像的软盘。在响应特殊的启动提示后，该软盘会被加载为根文件系统。

然而，在 Red Hat Linux 6.1 及更高版本中，标准安装介质已提供救援模式，因此不再需要特殊的软盘。尽管如此，许多 Red Hat Linux 用户仍然偏好 Red Hat Linux 6.0 的救援模式方法。如果你有 Red Hat Linux 6.0 的发行版 CD-ROM，可以按照下一小节的步骤使用 Red Hat Linux 6.0 的救援功能。

要使用 Red Hat Linux 6.1 的救援功能，请使用安装软盘或安装 CD-ROM 启动系统。在启动提示符处，回复 `linux rescue`。

救援功能将要求你选择语言和键盘样式。然后，它将尝试定位 Red Hat Linux 发行版介质的 `RPMS` 和 `base` 目录。如果系统的 CD-ROM 驱动器中包含发行版 CD-ROM，系统将进入救援模式。否则，救援功能将提示你输入这些目录的位置，这可以是 CD-ROM 驱动器或本地硬盘。通常，你应该在 CD-ROM 驱动器中插入安装 CD-ROM，并将救援模式功能指向该设备。但是，如果系统包含一个持有 `RPMS` 和 `base` 目录的可读文件系统，你可以将救援功能指向该文件系统所在的分区。

> 你可以使用 `bootnet.img` 软盘作为救援盘，从配置适当的 NFS 服务器获取救援环境。

### 使用 Red Hat Linux 6.0 救援功能

Red Hat Linux 6.2 及更高版本不再支持 Red Hat Linux 6.0 的救援功能。因此，在 RHCE 考试期间不再允许使用 Red Hat Linux 6.0 的救援功能。但是，如果你负责管理 Red Hat Linux 6.0 系统，你需要知道如何使用此功能。

要使用 Red Hat Linux 6.0 的救援功能，你必须从 Red Hat Linux 发行版 CD-ROM 上的镜像创建启动盘和救援盘。或者，你可以使用系统的启动盘，仅创建救援盘。

#### 创建启动盘

要从 Red Hat Linux 发行版 CD-ROM 上的镜像创建启动盘，请插入介质，将 CD-ROM 挂载为 `/mnt/cdrom`，并执行以下命令：

```
dd if=/mnt/cdrom/images/boot.img of=/dev/fd0
```



引导磁盘包含启动系统所需的内核和所有模块。如果您愿意，可以通过执行 `mkbootdisk` 命令，使用从您的系统创建的引导磁盘。

#### 创建救援磁盘

要从 Red Hat Linux 发行版 CD-ROM 上的镜像创建救援磁盘，请插入介质，将 CD-ROM 挂载为 `/mnt/cdrom`，然后执行以下命令：

```bash
dd if=/mnt/cdrom/images/rescue.img of=/dev/fd0
```

ramdisk 镜像包含一个支持重要恢复命令的根文件系统。

### 以救援模式启动

要启动使用 Red Hat Linux 6.0 的系统，请将引导磁盘插入软盘驱动器并启动系统。在响应引导提示时，输入 `linux rescue`。当收到提示时，将引导磁盘更换为救援磁盘。启动完成后，您将进入一个单用户 shell，该 shell 与当前 Red Hat Linux 救援模式提供的 shell 类似。

### 救援模式环境

救援模式中可用的命令是 Red Hat Linux 下通常可用命令的一个小子集。它们包括：

| | | | |
|---|---|---|---|
| anaconda | gzip | mkfs.ext2 | ps |
| badblocks | head | mknod | python |
| bash | hwclock | mkraid | python1.5 |
| cat | ifconfig | mkswap | raidstart |
| chatter | init | mlabel | raidstop |
| chmod | insmod | mmd | rcp |
| chroot | less | mmount | rlogin |
| clock | ln | mmove | rm |
| collage | loader | modprobe | rmmod |
| cp | ls | mount | route |
| cpio | lsattr | mpartition | rpm |
| dd | lsmod | mrd | rsh |
| ddcprobe | mattrib | mread | sed |
| depmode | mbadblocks | mren | sh |
| df | mcd | mshowfat | sync |
| e2fsck | mcopy | mt | tac |
| fdisk | mdel | mtools | tail |
| fscn | mdeltree | mtype | tar |
| fsck.ext2 | mdir | mv | touch |
| ftp | mdu | mzip | raceroute |
| genhdlst | mformat | open | unmount |
| gnome-pty-helper | minfo | pico | uncpio |
| grep | mkdir | ping | uniq |
| gunzip | mke2fs | probe | zcat |

本小节重点介绍几个特别有用的命令，并解释它们在故障排除和恢复中的作用。

### fdisk 命令

fdisk 命令将告知您本地硬盘上存在哪些分区。您需要了解此信息，以便知道需要检查并挂载哪些分区。要报告本地硬盘上现有的分区，请执行命令：

```
fdisk -l
```

分区类型将帮助您确定感兴趣的分区。以下是 fdisk 的典型输出：

```
Disk /dev/hda: 255 heads, 63 sectors, 2489 cylinders
Units = cylinders of 16065 * 512 bytes
```

| 设备 | 启动 | 起始 | 结束 | 块数 | ID | 系统 |
|---|---|---|---|---|---|---|
| /dev/hda1 | * | 1 | 127 | 1020096 | 6 | FAT16 |
| /dev/hda2 | | 128 | 2489 | 18927295 | 5 | Extended |
| /dev/hda5 | | 128 | 132 | 40131 | 83 | Linux |
| /dev/hda6 | | 133 | 387 | 2048256 | 83 | Linux |
| /dev/hda7 | | 1091 | 1157 | 538146 | 82 | Linux swap |

在示例中，分区 `hda5` 和 `hda6` 是您想要检查并可能挂载的 Linux 分区。

### e2fsck 命令

`e2fsck` 命令用于检查 Linux 文件系统是否损坏，并可选择性地修复简单损坏。要检查文件系统，请执行如下形式的命令：

```
e2fsck -y /dev/xxx
```

其中 `xxx` 是包含该文件系统的分区。`-y` 标志指示 `e2fsck` 自动尝试修复损坏，而不是在发现每个错误时向您询问；如果没有该标志，当文件系统包含大量错误时，该命令会变得非常繁琐。

Linux 将关于文件系统的信息存储在称为 `superblocks`（超级块）的特殊区域中。如果文件系统损坏，有时可以通过指示 Linux 使用备用超级块来恢复它。通常，这些超级块以 8192 个块为间隔写入，因此第一个备用超级块很可能位于块 8193 中。要指示 `e2fsck` 尝试使用超级块 8193 恢复文件系统，请执行如下形式的命令：

```
e2fsck -b 8193 -y /dev/xxx
```

其中 `xxx` 是包含该文件系统的分区。

在创建大型文件系统时，可能会使用稀疏超级块（sparse superblocks）。稀疏超级块以 32768 个块为间隔写入。因此，第一个备用稀疏超级块位于块 32769 中。

您可以使用 `dumpe2fs` 命令来获知未损坏文件系统备用超级块的位置。如果您担心文件系统损坏的可能性，应该在每个文件系统上运行该命令并保留输出，以便在恢复过程中使用。以下是 `dumpe2fs` 命令的典型输出：

```
dumpe2fs 1.14, 9-Jan-1999 for EXT2 FS 0.5b, 95/08/09
Filesystem volume name:  boot
Last mounted on:       <not available>
Filesystem UUID:       c10e5c68-c58-d5a7-11d3-93c2-8a83fd607d
Filesystem magic number: 0xEF53
Filesystem revision #:   0 (original)
Filesystem features:    (none)
Filesystem state:        not clean
Errors behavior:         Continue
Filesystem OS type:      Linux
Inode count:             10040
Block count:             40131
Reserved block count:    2006
Free blocks:             36575
Free inodes:              10016
First block:             1
Block size:               1024
Fragment size:           1024
Blocks per group:        8192
Fragments per group:     8192
Inodes per group:        2008
Inode blocks per group:   251
Last mount time:          Fri Mar 3 11:54:29 2000
Last write time:          Wed Apr 19 14:21:06 2000
Mount count:              1
Maximum mount count:      20
Last checked:             Fri Mar 3 11:45:58 2000
Check interval:          15552000 (6 months)
Next check after:         Wed Aug 30 12:45:58 2000
Reserved blocks uid:     0 (user root)
Reserved blocks gid:     0 (group root)

Group 0: (Blocks 1 -- 8192)
  Block bitmap at 3 (+2), Inode bitmap at 4 (+3)
  Inode table at 5 (+4)
  5657 free blocks, 1984 free inodes, 2 directories
  Free blocks: 2521-2536, 2552-8192
  Free inodes: 25-2008
Group 1: (Blocks 8193 -- 16384)
  Block bitmap at 8195 (+2), Inode bitmap at 8196 (+3)
  Inode table at 8197 (+4)
  7937 free blocks, 2008 free inodes, 0 directories
  Free blocks: 8448-16384
  Free inodes: 2009-4016
Group 2: (Blocks 16385 -- 24576)
  Block bitmap at 16387 (+2), Inode bitmap at 16388 (+3)
  Inode table at 16389 (+4)
  7937 free blocks, 2008 free inodes, 0 directories
  Free blocks: 16640-24576
  Free inodes: 4017-6024
Group 3: (Blocks 24577 -- 32768)
  Block bitmap at 24579 (+2), Inode bitmap at 24580 (+3)
  Inode table at 24581 (+4)
  7937 free blocks, 2008 free inodes, 0 directories
  Free blocks: 24832-32768
  Free inodes: 6025-8032
Group 4: (Blocks 32769 -- 40130)
  Block bitmap at 32771 (+2), Inode bitmap at 32772 (+3)
  Inode table at 32773 (+4)
  7107 free blocks, 2008 free inodes, 0 directories
  Free blocks: 33024-40130
  Free inodes: 8033-10040
```

每个组的第一个块都是一个超级块。因此，示例输出中显示的文件系统在块 1、8193、16385、24577 和 32769 处具有超级块。如果位于块 1 的主超级块损坏，其中一个备用超级块可能是完好的。

### lilo 命令

lilo 命令安装 LILO 引导加载程序并更新引导映射。通常，您可以通过执行以下命令来执行这些操作：

```
/sbin/lilo
```

然而，在救援模式下运行操作时，本地硬盘的根文件系统并未挂载为根目录。以通常方式运行 lilo 将无法正确更新本地硬盘的 /boot 目录。相反，您应该执行如下形式的命令：

```
/sbin/lilo -r path
```

其中 path 是本地硬盘根文件系统的当前挂载点。例如，如果本地硬盘的根文件系统挂载为 /mnt/hd，请执行命令：

```
/sbin/lilo -r /mnt/hd
```

或者，您可以使用 `chroot` 命令建立一个更改根环境，然后以普通方式执行 `lilo` 命令：

```
chroot /mnt/hd
/sbin/lilo
```

### sync 命令

在救援模式下操作时，通常无法使用 `shutdown` 命令以通常的有序方式关闭系统。但是，如果您突然断电或重置系统，可能会损坏一个或多个文件系统。因此，必须使用一种修改后的关机步骤。

当您准备重启系统时，请执行以下形式的一系列命令：

```
sync
sync
sync
cd /
umount fs1 fs2 ...
```

其中 `fs1, fs2, ...` 代表本地硬盘上已挂载的文件系统。当 `umount` 命令完成后，您可以断电或重置系统。

> **警告**：救援模式环境中的 `/dev` 目录可能不包含您想要访问的设备的设备文件。救援模式挂载命令有时会自动创建正确的设备文件；但如果您在访问设备时遇到困难，可能需要执行 `mknod` 命令来创建正确的设备文件。

### 需检查的配置文件

建议在单用户模式下检查的文件同样适用于救援模式下的检查：

- `/etc/conf.modules`
- `/etc/fstab`
- `/etc/inittab`



- `/etc/lilo.conf`
- `/etc/rc.d/*`
- `/etc/yp.conf`（如果系统使用 NIS）

与单用户模式一样，请特别注意 `/etc/fstab` 和 `/etc/lilo.conf`，如果这两个文件配置错误，通常会导致系统启动问题。

### 通用救援模式恢复步骤

以下是救援模式的通用故障排除步骤：

1. **从系统启动盘或安装 CD-ROM 启动。** 在提示输入启动镜像标签时，响应 `linux rescue`。系统启动后，您将进入一个 `bash` shell 会话，此时没有挂载本地文件系统——也就是说，没有挂载来自硬盘的文件系统。
2. **为本地文件系统创建挂载点：** `mkdir /mnt/hd`。
3. **识别可用分区：** `fdisk -l`。
4. **检查根文件系统：** `e2fsck -y /dev/xxx`，其中 `xxx` 是根文件系统所在的分区。您可能需要先通过执行命令 `mknod /dev/xxx` 来创建设备文件。
5. **挂载根文件系统：** `mount /dev/xxx /mnt/hd`，其中 `xxx` 是根文件系统所在的分区。
6. **建立更改根目录（changed-root）环境，使操作更方便：** `chroot /mnt/hd`。
7. **如果 LILO 损坏或丢失，挂载 `/boot` 分区：** `mount /dev/xxx /boot`，其中 `xxx` 是根文件系统所在的分区。
8. **使用 `pico` 编辑器修复任何配置错误的服务。** 请务必检查 `/etc/lilo.conf` 和 `/etc/fstab`。
9. **如果 `/etc/lilo.conf` 或内核发生了更改，运行 `lilo` 映射安装程序：** `/sbin/lilo`。
10. **提交更改：** `sync; sync; sync`。
11. **卸载所有已挂载的文件系统：** `cd / ; umount /boot`。
12. **重启计算机。**

现在完成练习 20.2，以获得在救援模式下工作的经验。

### 练习 20.2：使用救援模式

配置正确的 Linux 系统很少出现故障。但一旦出现故障，熟练使用救援模式对于排除故障和修复问题至关重要。为了获得在救援模式下工作的经验，请执行以下步骤：

1. 以救援模式启动系统。
2. 识别可用的磁盘分区。
3. 检查根文件系统的完整性，然后将其挂载。
4. 检查非根文件系统的完整性。
5. 挂载 `/boot` 分区，并运行 LILO 映射安装程序。
6. 提交更改并重启系统。

您可以使用本书和其他帮助资料来完成此练习。但在参加 RHCE 考试之前，请确保您能够在不参考书籍或笔记的情况下执行此类操作。

## 总结

在本章中，您学习了如何在单用户模式和救援模式下工作。涵盖的最重要课题包括：

**单用户模式** 您可以通过在 LILO 提示符处输入 `linux s`、`linux single` 或 `linux emergency` 来在单用户模式下启动 Linux。单用户模式用于排除系统故障或修复系统。系统必须在根文件系统完好的情况下才能成功在单用户模式下启动。

**救援模式** 您可以通过从安装介质启动并在启动提示符处输入 `rescue` 来在救援模式下启动 Linux。在 Red Hat Linux 6.1 之前，您必须使用特殊的救援盘启动。救援模式仅提供有限的一组可用程序。

**重要文件** 当系统无法正常启动时，您可以以单用户模式启动并检查以下配置文件，寻找可能导致问题的原因：

- /etc/conf.modules
- /etc/fstab
- /etc/inittab
- /etc/lilo.conf
- /etc/rc.d/*
- /etc/yp.conf（如果系统使用 NIS）

**检查文件系统** 要检查 Linux 原生文件系统的错误或修复错误，请使用 `e2fsck` 工具。当使用适当的选项调用 `fsck` 工具时，它会调用 `e2fsck`。

**离开救援模式** 在救援模式下无法使用常规的关机命令。在关闭运行于救援模式的系统之前，您必须执行 `sync` 和 `umount` 命令。

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- rescue mode（救援模式）
- single-user mode（单用户模式）
- superblocks（超级块）

## 其他信息来源

如果您想进一步了解本章介绍的课题，应参考 *《The Official Red Hat Linux Reference Guide》*。

## 复习题

1. 以下哪个文件最可能是导致系统无法正常启动的配置错误源？
    A. /etc/fstab
    B. /etc/hosts
    C. /etc/inittab
    D. /etc/lilo.conf

2. 要关闭运行在单用户模式下的系统，应该怎么做？
    A. 执行 `shutdown` 命令
    B. 执行 `sync` 和 `umount` 命令
    C. 按系统重启按钮
    D. 关闭电源

3. 在救援模式下更新 LILO 启动映射，应该执行以下哪个命令？
    A. /sbin/lilo
    B. /sbin/lilo -v
    C. /sbin/lilo -r /mnt/boot
    D. /sbin/lilo /etc/lilo.conf

4. 要列出本地硬盘的现有分区，应该执行以下哪个命令？
    A. fdisk -l
    B. fdisk -p
    C. fdisk -lp
    D. fdisk -r

5. 要检查 Linux 分区 /dev/hdb2 的错误，应该执行以下哪个命令？
    A. `e2fsck /dev/hdb2` 
    B. `e2fsck -y /dev/hdb2` 
    C. `e2fsck -y -b /dev/hdb2` 
    D. `e2fsck -y -b 8193 /dev/hdb2` 

6. 在使用救援模式恢复系统时，何时应该挂载 `/boot` 分区？
    A. 总是挂载 
    B. 仅当它位于第一块硬盘上时 
    C. 仅当需要检查其文件系统时 
    D. 仅当需要运行 LILO 启动映射安装程序时

7. 除非使用稀疏超级块（sparse superblocks），否则 Linux 文件系统通常将备份超级块存储在哪个块中？
    A. 1 
    B. 4097 
    C. 8193 
    D. 16385

## 复习题答案

1. A, C, D。`/etc/hosts` 文件不太可能阻止系统正常启动，尽管它可能会影响正常运行。
2. A。`sync` 和 `umount` 命令用于关闭运行在救援模式下的系统。您不应通过关闭电源或重启系统来关闭 Linux 系统。
3. C。您必须使用 `-r` 标志来告知 `lilo` 本地硬盘的根目录未被挂载为当前根目录。
4. A。`-l` 参数指示 `fdisk` 报告本地硬盘情况。
5. A, B, D。`-b` 标志需要一个指定备用超级块的参数。它指示 `e2fsck` 尝试使用备用超级块进行恢复。
6. D。您不需要为了检查文件系统而挂载它；仅在需要更新启动映射时才挂载 `/boot` 文件系统。
7. C。超级块通常每 8192 个块存储一个；主超级块在块 1 中。在使用稀疏超级块时，超级块每 32K 出现一次，因此备份超级块位于 32769。

# 网络服务管理
# 第四部分

# 第 21 章：安装与配置主要网络服务

**本章涵盖的 RHCE 准备课题：**

- 理解并能够安装和配置：Apache、BIND (DNS)、FTP、邮件 (sendmail 和 pop/imap)、NFS 和 Samba。
- 足够熟悉主要网络服务的功能、配置和日志记录，以能够进行基本的故障排除。

从准备 RHCE 考试的角度来看，本章是本书最重要的章节之一——甚至是 ter 最重要的一章。RHCE 考试的三个组成部分之一要求您安装并配置一组指定的网络服务。您在该考试部分能否脱颖而出，取决于您对本章内容的掌握程度，本章解释了主要网络服务以及如何安装、配置和排除故障。

本章以及 RHCE 考试相关部分的钥匙在于章末练习。您应该下定决心完成本章每个练习的每一个步骤。有时练习会引导您去研究 man 手册或其他文档。这是练习中至关重要的一部分。访问和解读系统文档的能力将资深系统管理员与新手区分开来。您使用文档的技巧将帮助您应对 RHCE 考试期间出现的意外问题。

本章的第一节提供了关于 TCP/IP 服务的基础信息。随后的章节将解释主要的 Linux TCP/IP 服务。

## TCP/IP 服务

所有主要的 Linux 网络服务都是 TCP/IP 服务——也就是说，它们是基于 TCP/IP 协议族的服务。一个 TCP/IP 服务有一个关联的数字，称为*端口（port）*；端口的编号范围是从 0 到 65535。



常见的 TCP/IP 服务被称为 *众所周知的端口*（well-known ports）；`/etc/services` 文件包含这些端口的列表，如表 21.1 所示。

### 表 21.1 众所周知的服务及其端口

| 服务 | 端口/类型 | 注释 |
|---|---|---|
| tcpmux | 1/tcp | TCP 端口服务复用器 |
| rtmp | 1/ddp | 路由表维护协议 |
| nbp | 2/ddp | 名称绑定协议 |
| echo | 4/ddp | AppleTalk 回显协议 |
| zip | 6/ddp | 区域信息协议 |
| echo | 7/tcp | |
| echo | 7/udp | |
| discard | 9/tcp | 丢弃（空接收） |
| discard | 9/udp | 丢弃（空接收） |
| systat | 11/tcp | 用户状态 |
| daytime | 13/tcp | |
| daytime | 13/udp | |
| netstat | 15/tcp | |
| qotd | 17/tcp | 每日语录 |
| msp | 18/tcp | 消息发送协议 |
| msp | 18/udp | 消息发送协议 |
| chargen | 19/tcp | 字符生成源 |
| chargen | 19/udp | 字符生成源 |
| ftp-data | 20/tcp | |
| ftp | 21/tcp | |
| fsp | 21/udp | fspd |
| ssh | 22/tcp | SSH 远程登录协议 |
| ssh | 22/udp | SSH 远程登录协议 |
| telnet | 23/tcp | |
| smtp | 25/tcp | 邮件 |
| time | 37/tcp | 时间服务器 |
| time | 37/udp | 时间服务器 |
| rlp | 39/udp | 资源定位 |
| nameserver | 42/tcp | 名称 (IEN 116) |
| whois | 43/tcp | nicname |
| re-mail-ck | 50/tcp | 远程邮件检查协议 |
| re-mail-ck | 50/udp | 远程邮件检查协议 |
| domain | 53/tcp | 名称服务器 |
| domain | 53/udp | 名称服务器 |
| mtp | 57/tcp | 已弃用 |
| bootps | 67/tcp | BOOTP 服务器 |
| bootps | 67/udp | |
| bootpc | 68/tcp | BOOTP 客户端 |
| bootpc | 68/udp | |
| tftp | 69/udp | |
| gopher | 70/tcp | Internet Gopher |
| gopher | 70/udp | |
| rje | 77/tcp | netrjs |
| finger | 79/tcp | |
| www | 80/tcp | http |
| www | 80/udp | 超文本传输协议 |
| link | 87/tcp | ttylink |
| kerberos | 88/tcp | kerberos5 krb5 |
| kerberos | 88/udp | kerberos5 krb5 |
| supdup | 95/tcp | |
| linuxconf | 98/tcp | |
| hostnames | 101/tcp | 主机名 |
| iso-tsap | 102/tcp | tsap |
| csnet-ns | 105/tcp | cso-ns |
| csnet-ns | 105/udp | cso-ns |
| poppassd | 106/tcp | Eudora |
| poppassd | 106/udp | Eudora |
| rtelnet | 107/tcp | 远程 Telnet |
| rtelnet | 107/udp | |
| pop-2 | 109/tcp | 邮局 |
| pop-2 | 109/udp | |
| pop-3 | 110/tcp | POP 第 3 版 |
| pop-3 | 110/udp | |
| sunrpc | 111/tcp | 端口映射器 |
| sunrpc | 111/udp | 端口映射器 |
| auth | 113/tcp | 身份验证 tap ident |
| sftp | 115/tcp | |
| uucp-path | 117/tcp | |
| nntp | 119/tcp | readnews untp |
| ntp | 123/tcp | |
| ntp | 123/udp | 网络时间协议 |
| netbios-ns | 137/tcp | NETBIOS 名称服务 |
| netbios-ns | 137/udp | |
| netbios-dgm | 138/tcp | NETBIOS 数据报服务 |
| netbios-dgm | 138/udp | |
| netbios-ssn | 139/tcp | NETBIOS 会话服务 |
| netbios-ssn | 139/udp | |
| imap2 | 143/tcp | imap |
| imap2 | 143/udp | imap |
| snmp | 161/udp | 简单网络管理协议 |
| snmp-trap | 162/udp | snmptrap |
| cmip-man | 163/tcp | 基于 IP 的 ISO 管理 (CMOT) |
| cmip-man | 163/udp | |
| cmip-agent | 164/tcp | |
| cmip-agent | 164/udp | |
| mailq | 174/tcp | Zmailer 邮件传输队列 |
| xdmcp | 177/tcp | X 显示管理器控制协议 |
| xdmcp | 177/udp | |
| nextstep | 178/tcp | NeXTStep NextStep |
| nextstep | 178/udp | NeXTStep NextStep |
| bgp | 179/tcp | 边界网关协议 |
| bgp | 179/udp | |
| prospero | 191/tcp | Cliff Neuman 的 Prospero |
| prospero | 191/udp | |
| irc | 194/tcp | 因特网中继聊天 |
| irc | 194/udp | |
| smux | 199/tcp | SNMP Unix 复用器 |
| smux | 199/udp | |
| at-rtmp | 201/tcp | AppleTalk 路由 |
| at-rtmp | 201/udp | |
| at-nbp | 202/tcp | AppleTalk 名称绑定 |
| at-nbp | 202/udp | |
| at-echo | 204/tcp | AppleTalk 回显 |
| at-echo | 204/udp | |
| at-zis | 206/tcp | AppleTalk 区域信息 |
| at-zis | 206/udp | |
| qmtp | 209/tcp | 快速邮件传输协议 |
| qmtp | 209/udp | 快速邮件传输协议 |
| z3950 | 210/tcp | wais # NISO Z39.50 数据库 |
| z3950 | 210/udp | wais |
| ipx | 213/tcp | IPX |
| ipx | 213/udp | |
| imap3 | 220/tcp | 交互式邮件访问 |
| imap3 | 220/udp | 协议 v3 |
| rpc2portmap | 369/tcp | |
| rpc2portmap | 369/udp | Coda 端口映射器 |
| codaauth2 | 370/tcp | |
| codaauth2 | 370/udp | Coda 身份验证服务器 |
| ulistserv | 372/tcp | Unix Listserv |
| ulistserv | 372/udp | |
| https | 443/tcp | MCom |
| https | 443/udp | MCom |
| snpp | 444/tcp | 简单网络寻呼协议 |
| snpp | 444/udp | 简单网络寻呼协议 |
| ssmtp | 465/tcp | 基于 SSL 的 SMTP |
| saft | 487/tcp | 简单异步文件传输 |
| saft | 487/udp | 简单异步文件传输 |
| exec | 512/tcp | |
| biff | 512/udp | comsat |
| login | 513/tcp | |
| who | 513/udp | whod |
| shell | 514/tcp | cmd |
| syslog | 514/udp | |
| printer | 515/tcp | spooler |
| talk | 517/udp | |
| ntalk | 518/udp | |
| route | 520/udp | router routed |
| timed | 525/udp | 时间服务器 |
| tempo | 526/tcp | newdate |
| courier | 530/tcp | rpc |
| conference | 531/tcp | chat |
| netnews | 532/tcp | readnews |
| netwall | 533/udp | 用于紧急广播 |
| gdomap | 538/tcp | GNUstep 分布式对象 |
| gdomap | 538/udp | GNUstep 分布式对象 |
| uucp | 540/tcp | uucpd |
| afpovertcp | 548/tcp | 基于 TCP 的 AFP |
| afpovertcp | 548/udp | 基于 TCP 的 AFP |
| remotefs | 556/tcp | rfs_server rfs |
| klogin | 543/tcp | Kerberized rlogin |
| kshell | 544/tcp | krcmd |
| snews | 563/tcp | 基于 SSL 的 NNTP |
| npmp-local | 610/tcp | dqs313_qmaster |
| npmp-local | 610/udp | dqs313_qmaster |
| npmp-gui | 611/tcp | dqs313_execd |
| npmp-gui | 611/udp | dqs313_execd |
| hmmp-ind | 612/tcp | dqs313_intercell |
| hmmp-ind | 612/udp | dqs313_intercell |
| ssl-ldap | 636/tcp | 基于 SSL 的 LDAP |
| kerberos-adm | 749/tcp | Kerberos kadmin |
| kerberos4 | 750/udp | kerberos-iv kdc |
| kerberos4 | 750/tcp | kerberos-iv kdc |
| kerberos_master | 751/udp | Kerberos 身份验证 |
| kerberos_master | 751/tcp | Kerberos 身份验证 |
| passwd_server | 752/udp | Kerberos 密码服务器 |
| krb_prop | 754/tcp | Kerberos 从属传播 |
| krbupdate | 760/tcp | kreg |
| kpasswd | 761/tcp | kpwd |
| webster | 765/tcp | 网络字典 |
| webster | 765/udp | |
| omirr | 808/tcp | omirrd |
| omirr | 808/udp | omirrd |
| supfilesrv | 871/tcp | SUP 服务器 |
| rsync | 873/tcp | rsync |
| rsync | 873/udp | rsync |
| simap | 993/tcp | 基于 SSL 的 IMAP |
| spop3 | 995/tcp | 基于 SSL 的 POP-3 |
| socks | 1080/tcp | socks 代理服务器 |
| socks | 1080/udp | socks 代理服务器 |
| kpop | 1109/tcp | 带 Kerberos 的 Pop |
| supfiledbg | 1127/tcp | SUP 调试 |
| rmtcfg | 1236/tcp | Gracilis Packeten 远程配置服务器 |
| xtel | 1313/tcp | 法国 minitel |
| ingreslock | 1524/tcp | |
| ingreslock | 1524/udp | |
| prospero-np | 1525/tcp | Prospero 非特权 |
| prospero-np | 1525/udp | |
| support | 1529/tcp | GNATS |
| datametrics | 1645/tcp | 旧版 radius |
| datametrics | 1645/udp | 旧版 radius |
| sa-msg-port | 1646/tcp | 旧版 radacct |
| sa-msg-port | 1646/udp | 旧版 radacct |
| radius | 1812/tcp | Radius |
| radius | 1812/udp | Radius |
| radacct | 1813/tcp | Radius 计费 |
| radacct | 1813/udp | Radius 计费 |
| cfinger | 2003/tcp | GNU Finger |
| knetd | 2053/tcp | Kerberos 解复用器 |
| zephyr-srv | 2102/udp | Zephyr 服务器 |
| zephyr-clt | 2103/udp | Zephyr serv-hm 连接 |
| zephyr-hm | 2104/udp | Zephyr 主机管理器 |
| eklogin | 2105/tcp | Kerberos 加密 rlogin |
| ninstall | 2150/tcp | ninstall |
| ninstall | 2150/udp | ninstall |
| cvspserver | 2401/tcp | CVS 客户端/服务器操作 |
| cvspserver | 2401/udp | CVS 客户端/服务器操作 |
| venus | 2430/tcp | codacon 端口 |
| venus | 2430/udp | Venus 回调/wbc 接口 |
| venus-se | 2431/tcp | tcp 副作用 |
| venus-se | 2431/udp | udp sftp 副作用 |



## 表 21.1 知名服务及其端口（接前页）

| 服务 | 端口/类型 | 注释 |
| :--- | :--- | :--- |
| codasrv | 2432/tcp | 不使用 |
| codasrv | 2432/udp | 服务器端口 |
| codasrv-se | 2433/tcp | tcp 副作用 |
| codasrv-se | 2433/udp | udp sftp 副作用 |
| afbackup | 2988/tcp | Afbackup 系统 |
| afbackup | 2988/udp | Afbackup 系统 |
| icp | 3130/tcp | 互联网缓存协议 (Squid) |
| icp | 3130/udp | 互联网缓存协议 (Squid) |
| mysql | 3306/tcp | MySQL |
| mysql | 3306/udp | MySQL |
| fax | 4557/tcp | FAX 传输服务（旧） |
| hylafax | 4559/tcp | HylaFAX 客户端-服务器协议（新） |
| rfe | 5002/tcp | Radio Free Ethernet |
| rfe | 5002/udp | 实际上仅使用 UDP |
| cfengine | 5308/tcp | CFengine |
| cfengine | 5308/udp | CFengine |
| noclog | 5354/tcp | 使用 TCP 的 noclogd |
| noclog | 5354/udp | 使用 UDP 的 noclogd |
| hostmon | 5355/tcp | hostmon 使用 TCP |
| hostmon | 5355/udp | hostmon 使用 TCP |
| postgres | 5432/tcp | POSTGRES |
| postgres | 5432/udp | POSTGRES |
| ircd | 6667/tcp | 互联网中继聊天 |
| ircd | 6667/udp | 互联网中继聊天 |
| bbs | 7000/tcp | BBS 服务 |
| webcache | 8080/tcp | WWW 缓存服务 |
| webcache | 8080/udp | WWW 缓存服务 |
| tproxy | 8081/tcp | 透明代理 |
| tproxy | 8081/udp | 透明代理 |
| mandelspawn | 9359/udp | mandelbrot |
| amanda | 10080/udp | amanda 备份服务 |
| kamanda | 10081/tcp | amanda 备份服务 (Kerberos) |
| kamanda | 10081/udp | amanda 备份服务 (Kerberos) |
| amandaidx | 10082/tcp | amanda 备份服务 |
| amidxtape | 10083/tcp | amanda 备份服务 |
| isdnlog | 20011/tcp | isdn 日志系统 |
| isdnlog | 20011/udp | isdn 日志系统 |
| vboxd | 20012/tcp | 语音信箱系统 |
| vboxd | 20012/udp | 语音信箱系统 |
| binkp | 24554/tcp | Binkley |
| binkp | 24554/udp | Binkley |
| asp | 27374/tcp | 地址搜索协议 |
| asp | 27374/udp | 地址搜索协议 |
| tfido | 60177/tcp | Ifmail |
| tfido | 60177/udp | Ifmail |
| fido | 60179/tcp | Ifmail |
| fido | 60179/udp | Ifmail |

在 Linux 中，只有特权用户才能访问 0 到 1023 端口，因此这些端口被称为 *特权端口 (privileged ports)*。这一限制通过防止非特权用户用伪造服务替换真实服务，从而提高了系统安全性。当客户端访问绑定到特权端口的服务时，客户端可以确信该服务未被篡改。

为了理解端口号如何使用，可以考虑你如何给住在公寓里的人寄信：你会写街道地址和公寓号。在这个类比中，IP 地址类似于街道地址：绑定到该 IP 地址的主机上可能有许多可用服务。端口号标识一个特定的服务，就像公寓号标识公寓大楼内的一个特定单元一样。

当客户端访问服务时，客户端会使用客户端主机上的一个端口。为了向客户端传递信息，服务器会使用客户端主机的 IP 地址和客户端的端口号。因此，客户端和服务器之间的通信涉及四个要素：

- 服务器主机 IP 地址
- 服务器端口
- 客户端主机 IP 地址
- 客户端端口

这些要素统称为 *套接字 (socket)*。访问服务涉及一个标准过程，称为 *绑定-监听-连接-接受 (bind-listen-connect-accept)* 过程：

1. 服务器进程将自身绑定到服务器主机的一个端口，并开始监听客户端请求。
2. 客户端进程请求客户端主机上的一个可用端口，并使用该端口通过服务器进程的端口连接到服务器进程。
3. 服务器进程通过请求服务器主机上的一个可用端口并通知客户端使用该端口进行通信，从而接受连接。

图 21.1 展示了绑定-监听-连接-接受过程。

### 图 21.1 绑定-监听-连接-接受过程

![](img/4eef9c6f2f52b608eba628cf4e2793ce_510_0.png)

TCP/IP 服务可以通过两种方式之一运行：

- 独立运行 (stand-alone)
- inetd

独立服务作为守护进程持续运行。`inetd` 服务在 `inetd` 进程的控制下运行，仅在客户端请求到达时才启动。该服务仅在满足请求所需的时间内运行，然后终止。如果一个服务被频繁使用或需要相对较长的启动时间，最好将其作为独立服务运行。然而，很少使用且启动迅速的服务可以更高效地作为 `inetd` 服务运行，因为它们仅在运行时才消耗内存等资源。

要指定服务作为 `inetd` 服务运行，请在 `inetd` 的配置文件 `/etc/inetd.conf` 中指定该服务。`inetd` 服务将自身绑定到服务的指定端口并监听客户端请求。当收到请求时，`inetd` 服务会启动相应的服务器并将请求移交。

本章的其余部分将介绍主要的 Linux 网络服务：

- Apache Web 服务器
- Berkeley 互联网名称域名 (BIND) 服务器
- 文件传输协议 (FTP) 服务器
- 邮件服务器 (`sendmail`、POP 和 IMAP)
- 网络文件系统 (NFS) 服务器

## Apache Web 服务器

Apache 是一个广泛使用的、符合 HTTP 1.1 标准的开源 Web 服务器。2000 年 3 月的 Netcraft 调查 (`www.netcraft.com`) 显示，超过 780 万个网站（约占调查网站的 61%）运行的是 Apache；相比之下，只有约 21% 的网站运行的是微软的 Internet Information Server。

Apache 快速且可靠。此外，有许多扩展其功能的第三方模块可用。你可以从 Apache 模块注册表网站 `modules.apache.org` 获取这些模块的信息。最受欢迎的 Apache 模块包括：

- `mod_auth` 及相关模块，用于执行用户身份验证
- `mod_frontpage`，为微软的 Front Page 扩展提供服务器端支持
- `mod_include`，提供服务器端包含 (SSI)
- `mod_info`，允许你通过 Web 浏览器查看服务器配置
- `mod_perl`，将 Perl 功能集成到服务器中
- `mod_php3`，将 PHP 功能集成到服务器中
- `mod_rewrite`，允许你操纵 URL
- `mod_speling`，将拼写检查器集成到服务器中

美国出口法限制采用加密技术的软件的进出口。为了避免 Apache 分发的限制，Apache 不包含对安全套接字层 (SSL) 的支持，SSL 是一种实现安全交易的重要 Web 技术。不过，你可以从 Apache-SSL 项目网站 `www.apache-ssl.org` 或 `ftp.zedz.net` 获取 Apache-SSL（一个包含 SSL 支持的 Apache 版本）。或者，你可以使用 Apache SSL 模块 `mod_ssl`，或购买提供 SSL 支持的商业版 Apache（例如 Red Hat 销售的版本）。

### 安装

要安装标准版本的 Apache，请进入包含 RPM 包的目录并执行以下命令：

```bash
rpm -Uvh apache-[^"d"]*.rpm
```

如果你需要能够编译 Apache 模块，还应安装 `apache-devel` 包：

```bash
rpm -Uvh apache-devel*.rpm
```

安装 apache 包命令中的 `[^"d"]` 是为了防止误安装 `apache-devel` 包。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_512_0.png)

如果你倾向于从本地硬盘而非通过 Web 访问 Apache 文档，可以安装 `apache-manual` 包，它会将重要的 Apache 文档放置在 `/home/httpd/html/manual/` 中。

### 基础配置

Apache 的配置文件位于 `/etc/httpd/conf`。它们分别是：

- `access.conf`
- `httpd.conf`
- `srm.conf`

曾经，每个文件包含特定类型的指令。较新版本的 Apache 放宽了对文件内容的限制，因此这三个文件的存在可以被视为一种历史产物。

当前版本的 Red Hat Linux 将所有配置信息都放在 `httpd.conf` 文件中；其他两个文件仅包含注释行（第一个非空字符为井号 #）。`httpd.conf` 文件有三个主要部分，由注释标记：

- 第一部分：全局环境



- 第 2 部分，主服务器配置
- 第 3 部分，虚拟主机配置

第 1 部分中包含的指令影响服务器的整体运行，包括主配置和所有虚拟主机配置。第 2 部分中的指令仅影响主服务器配置。第 3 部分中的指令（如果存在）仅影响其所属的虚拟主机配置。接下来的几个小节将更详细地探讨 `httpd.conf` 文件及其指令。

#### 第 1 部分：全局环境

第 1 部分中的指令允许您指定影响所有服务器配置的配置选项，例如：

- 配置类型：独立运行（stand-alone）或 `inetd`（通常为独立运行）
- 可用 Apache 模块的名称和位置
- 要启动的服务器进程数量以及要维持的最小和最大数量

除非您希望在 `inetd` 模式下运行服务器、安装自定义模块或修改服务器进程数量，否则您可能不需要修改第 1 部分中的指令。您可以参考 Apache 官方在线文档 `www.apache.org` 以帮助理解不清楚的指令。

#### 第 2 部分：主配置

`httpd.conf` 文件的第 2 部分包含仅影响服务器主配置运行的指令；这些指令不影响虚拟主机的运行（如果配置了虚拟主机的话）。主要配置项包括：

- 服务器的主机名
- 服务器监听的端口号（通常为端口 80）
- 守护进程运行的用户和组 ID（通常为 `nobody`）
- 所需的日志类型：按 IP 地址或主机名记录日志（通常按 IP 地址记录，效率更高）
- 根目录的位置（通常为 `/home/httpd/html`）
- 用户 HTML 子目录的名称（通常为 `~/public_html` 或 `~/www`）
- CGI 脚本存放的路径
- 格式化目录索引时使用的图标位置
- 特殊内容处理程序的配置选项

通常，您应该修改 `ServerName` 指令（用于指定与服务器关联的主机名称）和 `ServerAdmin` 指令（用于指定服务器管理员的电子邮件地址）。根据您的需求，您可能需要更改其他指令。

#### 第 3 部分：虚拟主机配置

虚拟主机（Virtual hosting），也称为多宿主（multi-homing），是 Apache 的一项重要功能，允许单个 Web 服务器响应多个 IP 地址或主机名。例如，可以将单个 Apache 实例配置为响应指向 `www.able.com` 和 `www.baker.com` 的查询。虚拟主机允许两个或多个组织共享同一个 Web 服务器。如果您想配置 Apache 以支持虚拟主机，必须修改 `httpd.conf` 文件第 3 部分中的指令。您需要指定：

- 虚拟主机的 IP 地址（一个或多个）
- 每个虚拟主机管理员的电子邮件地址
- 每个虚拟主机的主机名
- 与每个虚拟主机关联的日志文件名
- 每个虚拟主机的文档根目录（document root）和 CGI 目录的位置

这是一个为两个主机（`www.firsthost.com` 和 `www.secondhost.com`）配置的典型虚拟主机配置，两者都被分配了 IP 地址 192.169.100.1：

```
NameVirtualHost 192.169.100.1

<VirtualHost firsthost.com>
    ServerAdmin webmaster@firsthost.com
    DocumentRoot /home/httpd/html/firsthost/
    ServerName www.firsthost.com
    ErrorLog logs/firsthost-error-log
    TransferLog logs/firsthost-access-log
    ScriptAlias /cgi-bin/ /home/httpd/cgi-bin/firsthost/
</VirtualHost>

<VirtualHost secondhost.com>
    ServerAdmin webmaster@secondhost.com
    DocumentRoot /home/httpd/html/secondhost/
    ServerName www.secondhost.com
    ErrorLog logs/secondhost-error-log
    TransferLog logs/secondhost-access-log
    # other options here, e.g., <Directory>
    ScriptAlias /cgi-bin/ /home/httpd/cgi-bin/secondhost/
</VirtualHost>
```

> 如果 `NameVirtualHost` 中的 IP 地址是该主机的唯一 IP 地址，您应该包含一个描述主配置的 `VirtualHost` 条目。

### 管理

Apache 的服务器管理脚本为 `/etc/rc.d/init.d/httpd`。通过使用适当的参数调用此脚本，您可以控制服务器的运行。

#### 启动和重启服务

要启动 Apache Web 服务器，请执行命令：

```
/etc/rc.d/init.d/httpd start
```

要重启 Apache Web 服务器，请执行命令：

```
/etc/rc.d/init.d/httpd restart
```

> 如果服务器配置为 `inetd` 运行，您不需要——且不应该——启动或重启它。

#### 停止服务

要停止 Apache Web 服务器，请执行命令：

```
/etc/rc.d/init.d/httpd stop
```

> 如果服务器配置为 `inetd` 运行，您无法使用 `httpd` 脚本停止它；您必须重新配置 `inetd`。

#### 重新加载配置文件

要使 Apache 重新加载其配置文件，请执行命令：

```
/etc/rc.d/init.d/httpd reload
```

在保存修改后的文件版本后，您应该指示 Apache 重新加载其配置文件。在可能的情况下，重新加载配置文件比停止并重启服务更好。

#### 检查服务状态

要检查 Apache Web 服务器的状态，请执行命令：

```
/etc/rc.d/init.d/httpd status
```

> **注意** 如果服务器配置为 `inetd` 运行，您无法使用 `httpd` 脚本检查其状态。

#### 服务故障排除

要排除 Apache 的故障，请检查系统日志 (`/var/log/messages`) 和 Apache 日志文件 (`/var/log/httpd/*`) 以查找相关的错误消息。要检查虚拟主机配置，请执行命令：

```
/usr/sbin/httpd -S
```

服务器应报告主服务器以及每个已配置虚拟主机的主机名和端口号。

有关 Apache 的更多信息，请参阅 Apache 网站 `www.apache.org/docs` 上的在线文档。如果您安装了 `apache-manual` 软件包，可以访问存储在 `/home/httpd/html/manual` 目录中 HTML 格式的本地文档。

现在请花时间完成练习 21.1，该练习涉及 Apache 的安装和配置。

### 练习 21.1：安装和配置 Apache

为了获得 Apache 的实践经验，请安装 `apache` 和 `apache-manual` 软件包。配置两个共享单个 IP 地址的虚拟主机。使用浏览器，您可以验证是否能够访问每个虚拟主机。通过修改根文档使其内容截然不同，确保每个主机访问的是其自己的根文档。

您可能需要参考本章和 Apache 文档来完成此练习。但在参加 RHCE 考试之前，请确保您能够在不使用外部文档的情况下执行这些及类似操作。

## BIND 名称服务器

Berkeley Internet Name Daemon (BIND) 将 IP 地址解析为主机名，将主机名解析为 IP 地址。这项服务通常被称为域名服务 (DNS)。互联网上绝大多数 DNS 服务器运行的都是作为 Red Hat Linux 一部分分发的相同服务器软件。许多服务器的名称与其关联的程序名称相似；然而，BIND 的关联程序 `/usr/sbin/named` 的命名较为奇特。Red Hat Linux 帮助您配置两种类型的 DNS：

- 仅缓存（caching-only）DNS 服务器
- 普通 DNS 服务器

仅缓存 DNS 服务器可以提高与互联网连接速度较慢的主机的 DNS 性能。仅缓存名称服务器通过联系普通名称服务器来解析 IP 地址和主机名。但一旦 IP 地址或主机名被解析，仅缓存名称服务器就会存储结果，以便以后在引用该 IP 地址或主机名时无需查询名称服务器即可解析。

### 安装

Red Hat Linux 包含以下 BIND 相关软件包：

- `bind`：提供普通 DNS 服务器
- `bind-utils`：一套用于管理 BIND 的实用工具
- `caching-nameserver`：将 BIND 配置为提供仅缓存名称服务器

此外，它还包含 `bind-devel` 软件包，仅在开发调用 BIND 应用程序编程接口 (API) 的程序时才需要。

要安装 BIND，请进入包含软件包的目录并执行以下命令：

```
rpm -Uvh bind-*.rpm
```

如果您想配置仅缓存名称服务器，请同时执行以下命令：

```
rpm -Uvh caching-nameserver-*.rpm
```

### BIND 基础配置

要建立域名服务 (DNS)，您必须配置主 DNS 配置文件 `/etc/named.conf`。通常，您还必须配置一组被称为区域文件（zone files）的文件，这些文件通常位于 `/var/named`。区域文件分为：

- 正向区域文件：用于将主机名映射到 IP 地址
- 反向区域文件：用于将 IP 地址映射到主机名
- 提示文件（hint file）：用于标识负责回答所有注册域名 DNS 查询的根名称服务器



如果您需要一个仅用于缓存的名称服务器，安装 `caching-nameserver` 软件包即可正确配置 BIND。不过，您可以通过修改默认的缓存名称服务器配置，在 `/etc/named.conf` 中添加 forwarders 语句来提高名称查询的效率。forwarders 语句的形式为 `forwarders {IP_address}`，其中 `IP_address` 指定了一个 DNS 服务的 IP 地址，该服务将响应无法从缓存中解析的查询。如果需要，您可以指定多个服务器的 IP 地址，只需用分号将它们隔开即可。

`/etc/named.conf` 文件定义了每个区域（zone）文件。如果该区域文件是正向区域文件，`/etc/named.conf` 将定义该区域文件适用的域名；如果该区域文件是反向区域文件，`/etc/named.conf` 将定义该区域文件适用的网络。`/etc/named.conf` 文件还指明本地 DNS 是该区域的主 DNS（master DNS）还是从 DNS（slave DNS）。主 DNS 是其区域的主要名称服务器，被称为该区域的 *起始授权机构（start of authority）*。从 DNS 从主 DNS 获取信息，它会定期联系主 DNS 以保持信息的最新状态。

以下是一个典型的 `/etc/named.conf` 文件，其格式在 named 的 man 手册页中有所描述：

```
options {
	directory "/var/named";
};
zone "." {
	type hint;
	file "named.ca";
};
zone "azusapacific.com." {
	type master;
	file "named.azusapacific.com";
};
zone "0.0.207.in-addr.arpa" {
	type master;
	file "named.local";
};
zone "1.168.192.in-addr.arpa" {
	type master;
	file "named.reverse";
};
```

正确的 `named.ca` 提示文件内容可以通过 FTP 从 `ftp://ftp.rs.internic.net/domain/named.root` 获取。其余文件必须手动编写。正向区域文件通常指定：

- 作为该区域起始授权机构 (SOA) 的主机
- 负责该区域的管理者的电子邮件地址
- 该区域内主机名到 IP 地址的映射

此外，区域文件还可以指定次级名称服务器、邮件交换记录和主机别名（称为 *规范名称* 或 CNAME）。以下是一个典型的正向区域文件：

```
@		IN	SOA	azusapacific.com.
			root.azusapacific.com. (
			200002051	; serial time
			43200		; refresh time
			3600		; retry time
			3600000	; expire time
			2419200	; default_ttl
		)
@		IN	NS	azusapacific.com.
@		IN	MX	10	azusapacific.com.
localhost	IN	A	127.0.0.1
azusapacific.com. IN	A	192.168.1.1
bill		IN	A	192.168.1.2
toshiba		IN	A	192.168.1.99
router		IN	CNAME	azusapacific.com.
www		IN	CNAME	azusapacific.com.
ftp		IN	CNAME	azusapacific.com.
mail		IN	CNAME	azusapacific.com.
```

请注意，区域管理员的电子邮件地址 (`root.azusapacific.com`) 以及域名 (`azusapacific.com.`) 之后使用了不寻常的点号。其基本概念是，在区域文件和其他 DNS 配置文件中指定的所有主机名（无论是否为全限定域名）都以点号结尾。该文件的格式在 `named` man 手册页中有更详细的描述。

SOA 记录中的一系列数字指定了：

- 从服务器用于确定信息何时更改的序列号
- 从服务器应检查序列号的刷新间隔（以秒为单位）
- 刷新失败后，从服务器应重试的间隔（以秒为单位）
- 在刷新持续失败的情况下，丢弃缓存信息的间隔（以秒为单位）
- 缓存负面响应的默认间隔（以秒为单位）

以下是一个典型的反向区域文件：

```
@	IN	SOA	azusapacific.com.
root.azusapacific.com. (
	2000032502 ; serial
	43200 ; refresh
	3600 ; retry
	3600000 ; expire
	2419200 ; default_ttl
)
@	IN	NS	azusapacific.com.
1	IN	PTR	wall.azusapacific.com.
2	IN	PTR	p3.azusapacific.com.
3	IN	PTR	p2.azusapacific.com.
99	IN	PTR	laptop.azusapacific.com.
```

### 管理

named 的服务器管理脚本是 `/etc/rc.d/init.d/named`。通过调用该脚本并传递适当的参数，您可以控制服务器的运行。

#### 启动和重启服务

要启动 BIND，请执行命令：

```
/etc/rc.d/init.d/named start
```

要重启 BIND，请执行命令：

```
/etc/rc.d/init.d/named restart
```

#### 停止服务

要停止 BIND，请执行命令：

```
/etc/rc.d/init.d/named stop
```

#### 检查服务状态

要检查 BIND 的状态，请执行命令：

```
/etc/rc.d/init.d/named status
```

#### 强制数据库重新加载

每当您更改 BIND 配置文件时，应指示 BIND 重新加载其数据库。要指示 BIND 重新加载数据库，请执行命令：

```
/etc/rc.d/init.d/named reload
```

#### 日志

默认情况下，BIND 将消息记录到系统日志 `/var/log/messages` 中。如果 BIND 运行不正常，请检查日志中指向问题的错误消息。

### 进一步信息

关于 BIND 的详细文档可在 `/usr/doc/bind-*` 中找到。您还可以在 Web 上，在 Internet Software Consortium 的网站 `www.isc.org` 找到相关信息。

现在请花时间完成练习 21.2，这将为您提供配置 BIND 的实际经验。

### 练习 21.2：安装和配置 BIND

除 SENDMAIL 外，BIND 可能是 Unix 服务中最难配置的。不过，您不需要成为 BIND 专家才能通过 RHCE 考试。执行以下步骤以获得使用 BIND 的经验：

1. 安装 BIND。
2. 为一个假设的域名创建一组区域文件。使用预留地址块的 IP 地址，例如 192.168.1.0-192.168.1.255。
3. 配置 `/etc/named.conf` 以引用您的区域文件。
4. 启动 BIND 并验证其是否能够解析正向和反向引用。您可以使用 ping 命令通过主机名或 IP 地址进行 ping 来验证 BIND 的运行情况。请注意，在 Red Hat 6.2 中，将 IP 地址指定为 ping 命令的目标会导致该命令对指定 IP 地址执行反向查询。如果您不需要此行为，可以指定 `-n` 标志。

在执行此练习时，您可能需要一些帮助，因此请随时回顾本章并参考其他文档。不过，在参加 RHCE 考试之前，请确保您能够在不需要查阅书籍、笔记或其他帮助的情况下执行此类操作。

## FTP

华盛顿大学（圣路易斯）FTP 服务器是互联网上最广泛使用的 FTP 服务器。它允许用户上传和下载文件及目录。FTP 守护进程名为 `/usr/sbin/in.ftpd`；然而，其 man 手册页名为 `ftpd`。

提供了三个级别的 FTP 访问权限：

- 用户访问（User access）：由在服务器主机上拥有登录账户的用户访问。此级别的访问赋予用户由其用户 ID 定义的常规访问权限。
- 访客访问（Guest access）：由拥有特殊访客账户的用户访问，该账户仅提供 FTP 访问。此级别的访问赋予用户专门定义的访问权限。
- 匿名访问（Anonymous access）：由在服务器主机上没有定义账户的用户访问。此级别的访问仅允许用户访问指定目录及其子目录（通常为 `/home/ftp`）。此限制是通过 chrooted 环境强制执行的。

华盛顿大学 FTP 服务器可以记录所有访问。它还提供了一些功能，允许客户端传输压缩文件或使用单个命令传输整个目录。

### 安装

华盛顿大学 FTP 服务器以两个软件包的形式分发：

- `wu-ftpd`：包含 FTP 服务器
- `anonftp`：包含匿名 FTP 服务器

如果您需要匿名 FTP 服务，应安装这两个软件包。但是，如果您不需要匿名 FTP 服务，则只需安装 `wu-ftpd` 软件包。不必要地安装匿名 FTP 可能会使您的系统在一定程度上更容易受到黑客的攻击。

### 基本配置

FTP 服务有三个基本配置文件：

- `/etc/ftpaccess`：指定全局选项和用户权限
- `/etc/ftphosts`：指定可以或不可以访问 FTP 服务的客户端主机
- `/etc/ftpusers`：指定 *不能* 访问 FTP 服务的用户。通常，该文件包含 root, bin, daemon, adm, lp, sync, shutdown, halt, mail, news, uucp, operator, games 和 nobody 的条目

以下是一个典型的 ftpaccess 文件内容：

```
class all real,guest,anonymous *

email root@localhost

loginfails 5

readme README* login
readme README* cwd=*

message /welcome.msg login
message .message cwd=*

compress yes all
tar yes all
chmod no guest,anonymous
delete no guest,anonymous
overwrite no guest,anonymous
rename no guest,anonymous

log transfers anonymous,real inbound,outbound
```



```
shutdown /etc/shutmsg
```

```
passwd-check rfc822 warn
```

请查阅 `ftpaccess` 和 `ftphosts` 的 man 手册页以获取有关配置指令格式的信息。

### 管理

默认情况下，FTP 服务作为 `inetd` 服务运行。因此，不需要启动、重启或停止该服务。

FTP 服务将日志条目记录在系统日志 `/var/log/messages` 中。如果 FTP 服务运行不正常，请检查系统日志的内容，寻找指向问题的日志条目。

一个常见的需求是使一组目录可以通过匿名 FTP、HTTP 和 NFS 进行访问。FTP 服务器不跟踪符号链接，因此这些目录必须是被指定为 `ftp` 用户主目录的子目录，通常是 `/home/ftp` 目录。为了通过 HTTP 提供访问，请建立指向这些目录的符号链接。为了通过 NFS 提供访问，只需导出这些目录即可。

## 更多信息

您可以在 `ftp` 和 `ftpd` 的 `man` 手册页、`ftpaccess` 和 `ftphosts` 的手册页，以及 Web 网站 `www.wu-ftp.org` 上找到关于 FTP 的更多信息。要尝试安装和配置 FTP，请完成练习 21.3。

### 练习 21.3：安装 FTP

FTP 是一项流行的服务，因此您应当确保熟悉其安装、配置和运行。为了获得第一手经验，请执行以下步骤：

- 1. 安装 wu-ftpd 和 anonftp 软件包。
- 2. 验证您可以使用定义的用户账户登录并执行传输。
- 3. 验证您可以使用匿名方式登录并执行传输。

在完成练习时，您可以参考本书和其他帮助资料。但是，在参加 RHCE 考试之前，请确保您能够在没有帮助的情况下安装、配置和使用 FTP。

## 邮件

邮件涉及两种设施：邮件传输和邮件访问。Red Hat Linux 的邮件传输代理 (MTA) 是 `sendmail`，它是互联网上最流行的 MTA。Red Hat Linux 通过邮局协议 (POP) 或中间邮件访问协议 (IMAP) 提供邮件访问。`sendmail` 程序极其灵活，但相对较大且复杂。其特性包括：

- 能够解码和处理多种目的地址格式
- 支持虚拟邮件域和用户别名
- 广泛的安全和反垃圾邮件设施

### 邮件工作原理

用户通常通过邮件客户端应用程序撰写邮件。流行的客户端包括 Linux 和非 Linux 程序，例如：

- Eudora
- Mutt
- Netscape Communicator
- Microsoft Outlook
- Pegasus
- Pine

在撰写完邮件消息后，用户发送该消息，由简单邮件传输协议 (SMTP) 服务器进行传输。这可以通过多种方式实现。一些邮件客户端（包括大多数 Linux 客户端）会产生一个 `sendmail` 进程来传输消息；其他客户端则依赖于远程 SMTP 服务器的可用性。

如果使用 `sendmail`，则绑定到 25 端口的 `sendmail` 进程将使用 DNS 获取与目标主机相关的邮件交换 (MX) 信息，该信息指定了发送至目标主机的邮件消息应通过的邮件网关主机。随后，`sendmail` 进程使用 SMTP 将消息传输到邮件网关主机。网关主机再将消息传输到目标主机。目标主机的 SMTP 服务器根据服务器配置接受或拒绝该消息。例如，服务器可能会拒绝来自无法解析的域名发送的消息，这可能表明该消息是由 *spammer*（垃圾邮件发送者，即为了传输大量垃圾邮件而破坏不安全邮件服务器的未经授权用户）发送的。图 21.2 展示了邮件传输过程。

**图 21.2** 邮件传输过程
![](img/4eef9c6f2f52b608eba628cf4e2793ce_527_0.png)

一旦消息被投递，收件人可以在登录到目标主机时访问该消息。或者，用户可以从远程主机访问该消息，远程主机会联系目标主机上的 POP 或 IMAP 服务器。IMAP 协议较新，且通常优于 POP 协议。例如，POP 始终以明文形式在互联网上发送密码；而 IMAP 可以对其进行加密。

### 安装

`sendmail` 程序包含在多个软件包中：

- `sendmail`：包含程序本身
- `sendmail-cf`：包含修改 `sendmail` 配置所需的文件
- `sendmail-doc`：包含 `sendmail` 文档

可选软件包 `sendmail-cf` 和 `sendmail-doc` 合计仅需约 2MB 的磁盘空间。因此，通常建议安装所有三个软件包。要安装 `sendmail`，请进入包含软件包的目录并执行命令：

```
rpm -Uvh sendmail-*.rpm
```

POP3 和 IMAP 服务器都位于 `imap` 软件包中。要安装它们，请进入包含该软件包的目录并执行命令：

```
rpm -Uvh imap-*.rpm
```

`sendmail` 程序有几个主要的配置文件：

- `/etc/sendmail.cf`：包含邮件配置指令
- `/etc/sendmail.cw`：指定服务器将代表其接受邮件的主机
- `/etc/aliases`：指定用户邮件别名

您可以通过以下几种方式之一修改 `sendmail` 配置：

- 使用 `linuxconf` 工具的 `mailconf` 子系统。这通常是最简单且最佳的方法。
- 使用 `m4` 宏处理器生成修改后的配置。文件 `/usr/doc/sendmail/README.cf` 解释了该过程。
- 手动编辑 `/etc/sendmail.cf` 文件，此方法仅推荐给 `sendmail` 专家。

### IMAP 配置

您通常不需要配置 IMAP 或 POP。然而，这两项服务都通过 `inetd` 运行，而 `inetd` 的默认配置不适用于运行这些服务。`/etc/inetd.conf` 文件包含引用 POP 和 IMAP 服务的行，但在分发的配置中，这些行是被注释掉的：

```
#pop-2 stream tcp nowait root /usr/sbin/tcpd ipop2d
#pop-3 stream tcp nowait root /usr/sbin/tcpd ipop3d
#imap    stream  tcp    nowait  root    /usr/sbin/tcpd imapd
```

要正确配置 `inetd`，只需找到这些行，删除行首的井号 (#)，并保存修改后的文件。然后通过执行以下命令重启 `inetd`：

```
killall -HUP inetd
```

### sendmail 的管理

sendmail 的服务器管理脚本是 `/etc/rc.d/init.d/sendmail`。通过使用正确的参数调用此脚本，您可以控制服务器的运行。

#### 启动和重启服务
要启动 sendmail，请执行命令：
```
/etc/rc.d/init.d/sendmail start
```
要重启 sendmail，请执行命令：
```
/etc/rc.d/init.d/sendmail restart
```

#### 停止服务
要停止 sendmail，请执行命令：
```
/etc/rc.d/init.d/sendmail stop
```

#### 检查服务状态
要检查 sendmail 的状态，请执行命令：
```
/etc/rc.d/init.d/sendmail status
```

#### 日志
除了发布到系统日志 (`/var/log/messages`) 的日志条目外，sendmail 还保留自己的日志文件 `/var/log/maillog`。如果邮件服务运行不正常，请检查这两个日志文件以寻找问题来源的线索。

## 更多信息

有关 `sendmail` 的更多信息，请参阅 `sendmail` 网站 `www.sendmail.org`、位于 `/usr/doc/sendmail` 的 `sendmail-doc` 软件包内容，以及以下 man 手册页：

- aliases
- mailstats
- makemap
- newaliases
- praliases
- rmail
- sendmail

有关 IMAP 和 POP 的更多信息，请参阅 `/usr/doc/imap-*` 中的文档文件以及 `imapd` 和 `pop3` 的手册页。

现在请完成练习 21.4，以获得 Linux 邮件服务的实际操作经验。

### 练习 21.4：安装和配置邮件服务

邮件服务无处不在，因此每位系统管理员必须熟悉邮件的安装和配置。请执行以下步骤以获得邮件服务的第一手经验：

- 1. 安装所有三个 sendmail 软件包以及 IMAP/POP 软件包。
- 2. 使用 `mailconf` 指定将接受邮件的系统。
- 3. 使用 `mailconf` 指定几个用户邮件别名。
- 4. 使用邮件客户端（如 `pine`）验证您的邮件配置是否运行正常。

在配置邮件时，您可以参考本书寻求帮助。然而，在参加 RHCE 考试之前，请确保您能够在没有书籍或笔记帮助的情况下，执行像这样简单的邮件配置操作。



## NFS

网络文件系统 (NFS) 提供了对文件和目录的共享访问。在运行过程中，NFS 服务器将一个或多个目录指定为客户端可用。这些指定的目录被称为*共享 (shares)*，也可以说是由服务器*导出 (exported)* 的。一旦被 NFS 服务器导出，客户端系统就可以像挂载本地文件系统一样挂载 NFS 共享。Linux 的 NFS 实现与在其他 Unix 系统上可用的 NFS 实现功能相似，其客户端在很大程度上与 NFS 3.0 版本兼容。

NFS 服务器运行三个与 NFS 相关的守护进程：

- `portmap`：将客户端请求转发给正确的 NFS 进程
- `rpc.nfsd`：将远程文件访问请求转换为本地文件访问请求
- `rpc.mountd`：负责文件系统的挂载和卸载

一台主机可以既是 NFS 服务器又是客户端，在这种情况下，它将运行所有三个守护进程。

### 安装

在 Red Hat Linux 6.2 中，大部分 NFS 代码已集成在 Linux 内核中。要使用 NFS，您只需要以下软件包：

- `nfs-utils`：包含使用 NFS 所需的实用工具
- `portmap`：包含与 `portmap` 相关的文件，供 NFS 服务器使用

要安装 NFS，请进入包含软件包的目录并执行命令：

```bash
rpm -Uvh nfs-utils-*.rpm portmap-*.rpm
```

### 服务器配置

NFS 服务器的配置文件是 `/etc/exports`，其中的每一行都是一个指令，用于指定一个共享（即导出的目录）及其相关的访问权限。以下是一个典型的 `/etc/exports` 文件中的行：

```
/exports/database fred.azusapacific.com bob.azusapacific.com
```

该指令的一般形式为：

```
path host_list
```

其中 `path` 是共享目录的绝对路径，`host_list` 是可以访问该共享的一个或多个主机的列表。每个主机之间应由一个或多个空格隔开。

可以通过以下几种方式指定主机：

- 使用主机名（如果该主机属于本地域）
- 使用完全限定域名 (FQDN)
- 使用包含通配符 (*) 的主机名
- 使用 IP 地址
- 使用网络地址，例如 192.168.1.0/255.255.255.0

通配符最多匹配主机名的单个组件。例如，主机名指定符 `*.azusapacific.com` 匹配 `www.azusapacific.com` 但不匹配 `www.science.azusapacific.com`。通配符可以匹配主机名组件的一部分。例如，主机指定符 `dtc*.azusapacific.com` 匹配 `dtc01.azusapacific.com`、`dtc02.azusapacific.com` 等。

默认情况下，客户端被允许对共享进行只读访问，尽管 `exports` 的帮助页（man page）中可能有相反的信息。要允许读写访问，请在主机指定符后加上 `(rw)`。例如，这是一个典型的读写共享：

```
/exports/database fred.azusapacific.com(ro) bob.azusapacific.com(rw)
```

主机 `fred` 被允许只读访问，而主机 `bob` 被允许读写访问。请注意，不要在主机指定符和权限之间插入空格。

默认情况下，如果客户端以 `root` 身份登录，客户端不会被授予对共享文件的 root 访问权限；相反，此类请求将被映射到用户 ID 65535。如果您想允许 `root` 访问，请指定 `no_root_squash` 选项。例如：

```
/exports/database bob.azusapacific.com(rw,no_root_squash)
```

`/etc/exports` 文件很容易手动编辑。不过，如果您愿意，`linuxconf` 提供了一个管理 NFS 共享的工具。

### 客户端配置

如前所述，客户端可以将导出的目录视为本地文件系统。要挂载共享目录，可以使用 `mount` 命令的一种特殊形式。例如：

```
mount -t nfs server:/exports/databases /mnt/database
```

此命令将由名为 server 的主机导出的目录 /exports/databases 挂载为本地目录 /mnt/database。特殊语法 `server:` 用于指定提供共享的 NFS 服务器，文件系统类型指定为 `nfs`。

脚本 `/etc/rc.d/init.d/netfs` 在启动时运行，自动挂载 `/etc/fstab` 中指定的 NFS 目录。如果您希望 NFS 共享在启动时自动挂载，只需将其包含在 `/etc/fstab` 文件中。例如：

```
server:/exports/database /mnt/database nfs defaults 0 2
```

几个挂载选项可以让你控制 NFS 共享的运行：

- `hard, intr` 允许您杀死或中断被不可用服务器阻塞的请求。
- `nolock` 禁用文件锁定，以便 NFS 客户端可以访问缺乏锁定功能的 NFS 服务器。
- `rsize=8192` 和 `wsize=8192` 分别分配大于默认大小的读和写缓冲区，从而显著提高 NFS 的吞吐量。

您可以使用 `linuxconf` 来挂载 NFS 共享，或指定要包含在 `/etc/fstab` 中的 NFS 共享。启动 `linuxconf`，然后从菜单中选择 Access NFS Volume $\rightarrow$ Add。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_533_0.png)

`nfslock` 服务为 NFS 客户端提供文件锁定服务。如果您的 NFS 客户端需要锁定文件，请确保启用 `nfslock` 服务。

Red Hat Linux 还提供了 `autofs` 服务，您可以将其配置为根据需求挂载 NFS 共享。`autofs` 服务包含在同名的可选软件包中。有关更多信息，请参阅 `auto.master`、`autofs(5)`、`autofs(8)` 和 `automount` 的帮助页。

### NFS 管理

NFS 的主要服务器管理脚本是 `/etc/rc.d/init.d/portmap` 和 `/etc/rc.d/init.d/nfs`。通过使用正确的参数调用这些脚本，您可以控制 NFS 服务器的运行。

#### 启动和重启 NFS

要启动 NFS 服务器，执行以下命令：

```
/etc/rc.d/init.d/portmap start
/etc/rc.d/init.d/nfs start
```

要重启 NFS 服务器，执行以下命令：

```
/etc/rc.d/init.d/portmap restart
/etc/rc.d/init.d/nfs restart
```

#### 停止 NFS 服务器

要停止 NFS 服务器，执行以下命令：

```
/etc/rc.d/init.d/nfs stop
/etc/rc.d/init.d/portmap stop
```

#### 控制 NFS 服务器运行

`exportfs` 命令允许您控制本地主机上 NFS 服务器的运行：

- `exportfs -v` 列出共享目录及相关选项
- `exportfs -a share` 导出指定的共享
- `exportfs -a` 导出 `/etc/exports` 中列出的所有共享
- `exportfs -u share` 取消导出指定的共享
- `exportfs -ua` 取消导出所有共享
- `exportfs -r` 刷新共享列表

特别是在对 `/etc/exports` 文件进行任何修改后，您应该执行以下命令：

```
exportfs -r
```

#### 检查服务状态

在登录服务器主机时，要检查 NFS 服务器的状态，请执行以下命令：

```
/etc/rc.d/init.d/nfs status
/etc/rc.d/init.d/portmap status
```

要检查远程 NFS 服务器的状态，请执行命令：

```
rpcinfo -p server
```

其中 `server` 是 NFS 服务器的主机名。

要列出服务器导出的共享，请执行命令：

```
showmount -e server
```

其中 `server` 是 NFS 服务器的主机名。

#### 日志记录

NFS 设施将消息记录到系统日志文件 `/var/log/messages` 中。如果 NFS 运行不正常，请检查指向问题源头的系统日志消息。

现在请花时间完成练习 21.5，这将使您获得操作 NFS 的经验。

### 练习 21.5：安装和配置 NFS

NFS 是一项重要的网络服务，尤其是在 Unix 系统流行的环境下。为了获得操作 NFS 的经验，请执行以下步骤：

1. 在一台主机上安装 NFS 服务器软件包，在另一台主机上安装 NFS 客户端软件包。
2. 使用默认权限导出 NFS 服务器的 `/tmp` 目录。
3. 从客户端主机访问共享目录并尝试读取一个文件。操作应成功完成。
4. 从客户端主机访问共享目录并尝试写入一个文件。操作应失败。
5. 修改共享权限以允许读写访问。
6. 从客户端主机访问共享目录并尝试写入一个文件。操作应成功完成。

在执行此练习时，您可以参考本书和 NFS 文档。但在参加 RHCE 考试之前，请确保您可以在不使用书籍或其他外部文档的情况下执行此类操作。



## Samba

Samba 是 Microsoft Windows 9x 和 NT 所使用的 System Message Block (SMB) 服务的开源实现，该服务有时也被称为通用互联网文件系统 (CIFS)。Samba 在 Unix 和 Linux 社区中被广泛使用。Samba 起源于 Andrew Tridgell 的工作，他对 SMB 协议进行了反向工程。随后，一个全球团队成立，用于维护和增强 Samba。

Samba 使 Windows 客户端能够通过 Windows 文件管理器的“网络邻居”功能来访问 Linux 文件系统和打印机。Unix 和 Linux 客户端也可以访问共享的文件系统和打印机。即使在缺乏 Windows 客户端的计算环境中，Samba 也很受欢迎，因为它的身份验证机制优于 NFS。

SMB 是构建在微软 NetBIOS 协议之上的高级协议，可以通过 TCP/IP 网络运行。NetBIOS 复制了几个 TCP/IP 功能。例如，它拥有自己的主机名解析服务，即 Windows 互联网名称服务 (WINS)。

Samba 实际上有两个相关的服务：

- `smbd`：负责对客户端进行身份验证，授权客户端访问共享，并提供对文件和打印机的共享访问。
- `nmbd`：提供浏览功能，允许客户端发现服务器及其共享。它还充当 WINS 服务器，将 NetBIOS 主机名解析为 IP 地址。

在任何时间，一个 SMB 服务器在由 SMB 服务的网络中充当*浏览主控 (browse master)*。浏览主控（有时也被称为主浏览器，master browser）维护可用服务器和共享的信息，并响应客户端尝试发现服务器和共享的查询。符合条件的 SMB 服务器通过*选举 (election)* 来决定谁成为浏览主控。Samba 服务器可以配置为参与此类选举，或者覆盖选举，即使存在其他候选服务器也能成为浏览主控。

Linux 客户端可以通过两种方式访问 SMB 共享。`smbclient` 程序提供了类似 FTP 的方式来访问共享文件和打印机，而 `smbmount` 命令允许你像挂载本地文件系统一样挂载共享文件系统。标准的 `printtool` 工具允许你配置对 Samba 打印机的访问。

### 安装

Samba 包含在三个软件包中：

- `samba-common`：包含 Samba 客户端和服务器需要的文件
- `samba`：包含 Samba 服务器
- `samba-client`：包含 Samba 的 `smbclient`、`smbmount` 和 `smbprint` 程序以及相关文件和文档

Samba 更新频繁；你应该考虑从 Samba 官方网站 `www.samba.org` 下载最新的软件包，而不是安装 Red Hat Linux 发行版介质中包含的软件包。

要安装 Samba 服务器，请移动到包含软件包的目录并执行命令：

```bash
rpm -Uvh samba-*.rpm
```

此命令将安装 Samba 服务器和 Samba 客户端，这对于调试服务器非常有帮助。如果只想安装 Samba 客户端，请移动到包含软件包的目录并执行命令：

```bash
rpm -Uvh samba-common-*.rpm samba-client-*.rpm
```

### 基础服务器配置

Samba 的主配置文件是 `/etc/smb.conf`，该文件在 man 手册页 `smb.conf`、位于 `/usr/doc/samba*` 的文档文件以及 Samba 网站 `www.samba.org/docs` 中有详细描述。配置文件包含两种类型的指令：

- 全局指令：用于配置服务器
- 服务指令：用于配置共享文件和打印机

本节将解释 Samba 配置文件的内容。你可以使用文本编辑器通过修改文件内容来配置 Samba。如果你更喜欢使用图形化工具来配置 Samba，可以使用 `linuxconf`。此外，`swat` 软件包提供了一个基于 Web 的界面用于配置 Samba。

#### Samba 全局指令

以下是一个简单的 Samba 配置中所包含的全局指令：

```ini
# 指定工作组名称
workgroup = MYGROUP

# 指定与服务器相关联的描述性文本
# 并由网络邻居和 net view 功能显示
comment = Router

# 指定可以访问服务器的主机
hosts allow = 192.168.107. 0.0.0.

# 指定在用户级别实施安全性
security = user

# 自动共享 printcap 文件中定义的所有打印机
load printers = yes

# 将密码无效的用户映射到访客用户 ID
map to guest = Bad User

# 指定日志文件名 —— 为每个客户端主机使用单独的日志
log file = /var/log/samba/samba-log.%m

# 指定最大日志文件大小（单位：kbytes）
max log size = 50

# 设置套接字选项以调整性能
socket options = TCP_NODELAY

# 指定 printcap 文件名
printcap name = /etc/printcap

# 指定用户登录时下载并运行的批处理文件
logon script = %u.bat

# 作为 Windows 9x 客户端的登录服务器
domain logons = Yes

# 设置浏览选举级别，以确保 Samba 获胜
os level = 69

# 强制进行选举以确定主浏览器
preferred master = Yes

# nmbd 应该收集浏览列表
domain master = Yes

# 指定 nmbd 将充当 WINS 服务器
wins support = Yes

# 指定如何确定打印机状态信息
printing = bsd

# 检查每次访问的锁定情况
strict locking = Yes
```

你应该根据本地需求调整以下指令（以及其他需要的指令）：

- workgroup
- comment
- hosts allow

`hosts allow` 指令定义了允许访问服务器的客户端主机。本地主机地址 127.0.0.1 通常应包含在主机列表中。允许使用多种格式：

- IP 地址 —— 例如 192.168.1.0
- IP 地址和子网掩码 —— 例如 192.168.1.0/255.255.255.0
- 部分 IP 地址 —— 例如 192.168.（注意末尾的点）
- 主机名 —— 例如 `client.azusapacific.com`
- 域名或子域名 —— 例如 `.azusapacific.com`（注意没有通配符且有前导点）

对于 Windows 9x 和 NT 客户端，通常应将 `security` 参数的值指定为 `user`。但是，如果你希望在每个共享的基础上处理授权，请指定值为 `share`。或者，如果你希望授权由另一个服务器处理（例如，Windows NT 主域控制器 (PDC)），请指定值为 `server`。如果客户端参与 NT 域，请指定值为 `domain`。

#### Samba 服务指令

这里是一组用于设置共享目录的典型服务指令：

```ini
[cdrom]
comment = CDROM mounted in /mnt/cdrom
path = /mnt/cdrom
read only = Yes
browseable = Yes
valid users = fred, bob
```

这些指令建立了一个名为 `cdrom` 的共享，它提供了对 Samba 服务器 `/mnt/cdrom` 目录的只读访问。只有用户 `fred` 和 `bob` 可以访问该共享。如果你想创建一个公开可用的共享，请省略 `valid users` 指令并指定 `public = yes`。如果你想授予组内所有成员的访问权限，请指定 `@group`，其中 `group` 是组的名称。

如果你希望用户能够向共享写入，请省略 `read only` 指令并指定 `writable = yes`。如果你不希望该共享在浏览列表（如 Windows 网络邻居）中可见，请指定 `browseable = No`。以下是一个打印机共享示例：

```ini
[printers]
comment = All Printers
path = /var/spool/samba
public = yes
guest ok = yes
admin users = bob
create mask = 0700
print ok = Yes
browseable = Yes
printable = yes
```

Samba 允许你方便地为用户建立主目录。为此，请使用 `smb.conf` 文件的 `homes` 部分。例如：

```ini
[homes]
comment = Home Directories
read only = No
create mask = 0750
browseable = No
```

如果你希望 Samba 充当登录服务器，你应该定义一个 `netlogon` 共享。例如：

```ini
[netlogon]
comment = Samba Network Logon Service
```



```
path = /home/netlogon
guest ok = Yes
browseable = No
locking = No
```

### 客户端配置与使用

如果 Samba 服务器配置正确，您应该能够在 Windows 9x 客户端的“网络邻居”中查看可浏览的共享，将它们映射到驱动器盘符，并以通常的方式拖放文件。

要在 Linux 主机上访问 Samba 共享或 Windows 9x/NT 共享，请执行如下形式的命令：

```
smbmount //server/share /mount_point
```

其中 `server` 是服务器的主机名，`share` 是共享名称，`mount_point` 是应成为挂载点的本地目录。共享将使用执行 `smbmount` 命令的用户所关联的权限进行挂载。为了允许非特权用户挂载共享，您可以修改 `smbmnt` 和 `smbmount` 的权限以包含 setuid（模式 4755）。不过，您可能更倾向于安装 `smbclient` 并指导用户如何使用；这是一种虽然不太方便但更安全的方法。要使用 `smbclient` 访问共享，请执行如下形式的命令：

```
smbclient //server/share
```

其中 `server` 是服务器的主机名，`share` 是共享名称。

### 高级服务器配置

运行 Windows 95 OSR2、Windows 98 以及安装了 Service Pack 3 及更高版本的 Windows NT 的计算机上的 SMB 客户端使用加密密码，这与 Samba 的默认配置不兼容。您可以通过以下几种方式来适配此类客户端：

- 配置客户端主机使用明文密码。但这样做可能会损害安全性。
- 使用 Windows NT 主域控制器 (PDC) 进行身份验证和授权，并配置 Samba 使用加密密码。
- 配置 Samba 使用加密密码，并维护一个包含加密密码的文件。

有关配置 Samba 使用加密密码的信息，请参阅位于 `/usr/doc/samba/*/docs` 下的 `ENCRYPTION.txt` 文件。

### 管理

Samba 的主服务器管理脚本是 `/etc/rc.d/init.d/smb`。通过使用正确的参数调用此脚本，您可以控制 Samba 服务器的运行。

#### 启动和重启 Samba

要启动 Samba 服务器，请执行命令：

```
/etc/rc.d/init.d/smb start
```

要重启 Samba 服务器，请执行命令：

```
/etc/rc.d/init.d/smb restart
```

#### 停止 Samba

要停止 Samba 服务器，请执行命令：

```
/etc/rc.d/init.d/smb stop
```

#### 检查 Samba 状态

要检查 Samba 服务器的状态，请执行命令：

```
/etc/rc.d/init.d/smb status
```

#### 日志

Samba 的启动和关闭记录在系统日志文件 `/var/log/messages` 中。此外，Samba 将消息记录在自己的日志文件中。Samba 日志文件的位置和名称在 `/etc/smb.conf` 文件中配置。不过，它们通常位于 `/var/log/samba`。如果 Samba 运行不正常，请检查这些日志文件以寻找问题的线索。

#### 服务故障排除

Samba 包含了几个用于诊断和故障排除的工具。在修改 Samba 配置文件后，您应该执行命令：

```
testparm
```

该命令会检查 Samba 配置文件是否存在错误。为了确保可靠运行，您应该在启动 Samba 之前纠正这些错误。

要列出服务器上的可用共享，请执行如下形式的命令：

```
smbclient -L server -N
```

其中 `server` 是服务器的主机名。例如，要列出本地主机上的可用共享，请执行命令：

```
smbclient -L localhost -N
```

如果没有可见的共享，可能是 WINS 服务器没有响应。要进行调查，请执行如下形式的命令：

```
nmblookup -B server _SAMBA_
```

其中 `server` 是服务器的主机名。该命令应显示指定主机的 IP 地址。您还应检查 SMB 客户端是否已正确配置为使用 WINS。为此，请执行命令：

```
nmblookup -d 2 ""
```

本地网络上的客户端主机应响应其 IP 地址。有关 Samba 故障排除的更多信息，请参阅位于 `/usr/doc/samba/docs` 下的 `DIAGNOSIS.txt` 文件。

现在完成练习 21.6，这将为您提供 Samba 的实际操作经验。

### 练习 21.6

#### 安装与配置 Samba

Samba 比 NFS 更安全，在 Unix 社区中具有相当高且不断增长的普及度。要获得 Samba 的经验，请执行以下步骤：

1. 安装 Samba 服务器软件包。
2. 配置 Samba 以提供：
    - 一个只读文件共享
    - 一个读写文件共享
    - 一个打印机共享
3. 使用 Windows 95 OSR1 客户端访问这些共享以进行测试。

在进行此练习时，您可以访问任何可用的文档。但在参加 RHCE 考试之前，请做好在没有外部文档协助的情况下执行这些操作的准备。

## 总结

在本章中，您学习了安装和配置主要的网络服务。涵盖的最重要主题包括：

**网络服务** 网络服务及其关联的端口列在 `/etc/services` 中。

**端口** 0-1023 端口是特权端口，仅能由用户 ID 为 0（即 **root** 用户）的进程访问。

**绑定-监听-连接-接受过程** 绑定-监听-连接-接受（bind-listen-connect-accept）过程是 TCP 客户端和服务器进行通信的过程。

**配置 Apache Web 服务器** Apache Web 服务器有三个配置文件：

- `/etc/httpd/conf/access.conf`
- `/etc/httpd/conf/httpd.conf`
- `/etc/httpd/conf/srm.conf`

Red Hat Linux 将所有 Apache 指令放在 `/etc/httpd/conf/httpd.conf` 文件中，该文件分为三个部分：

- **第一部分** 全局环境
- **第二部分** 主服务器配置
- **第三部分** 虚拟主机配置

**为虚拟主机配置 Apache** 要为虚拟主机配置 Apache，必须指定：

- 虚拟主机的 IP 地址
- 每个虚拟主机管理员的电子邮件地址
- 每个虚拟主机的主机名
- 与每个虚拟主机关联的日志文件名
- 每个虚拟主机的文档根目录和 CGI 目录位置

**Berkeley Internet Name Daemon (BIND)** BIND 提供域名服务 (DNS)。相应的守护进程是 `/usr/sbin/named`。

**文件传输协议 (FTP)** FTP 实现了系统间的文件传输。FTP 定义了三类用户：

- 普通用户
- 访客用户
- 匿名用户

**邮件** 邮件系统包括将邮件投递到邮箱的邮件传输代理 (MTA)，以及访问邮箱并发送邮件（通常通过单独的 MTA）的邮件访问客户端。标准 Red Hat Linux MTA 是 `sendmail`；Red Hat Linux 提供了多种邮件客户端，支持访问 Post Office Protocol (POP) 和 Interim Mail Access Protocol (IMAP) 邮箱。

**网络文件系统 (NFS)** NFS 是一种支持共享文件和目录的 Unix 设施。Red Hat Linux 提供了一个与 Sun 的 NFS 3.0 大部分兼容的 NFS 实现。

**Samba** Samba 是一个开源的服务器实现，与微软的文件和打印机共享设施（ variously known as LAN Manager 或 Common Internet File System (CIFS)，基于 System Message Block (SMB) 协议）大部分兼容。Samba 可以在微软与 Unix/Linux 服务器及客户端之间提供文件和打印机共享。Samba 还可以执行 Microsoft Windows NT 主域控制器 (PDC) 的许多功能，包括用户身份验证。

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- bind-listen-connect-accept process（绑定-监听-连接-接受过程）
- browse master（浏览主控）
- canonical names（规范名称）
- election（选举）
- forward zone file（正向区域文件）
- port（端口）
- privileged ports（特权端口）
- reverse zone file（反向区域文件）
- shares（共享）
- socket（套接字）
- spammer（垃圾邮件发送者）
- start of authority（权限开始/SOA）
- well-known ports（周知端口）
- zone files（区域文件）

## 其他信息来源

如果您想了解本章所呈现主题的更多信息，应参考以下来源：

- 有关 NFS 的更多信息，请参阅 man 手册页：
    - exportfs
    - exports
    - mount
    - nfsstat
    - portmap
    - rquotad
    - showmount

- 另请参阅 Nicolai Langfeldt 编写的 *NFS HOWTO*，路径为 /usr/doc/HOWTO/NFS-HOWTO。

- *Official Guide to Red Hat Linux* 也提供了有关配置和使用 NFS 的信息。

- 有关 Samba 的更多信息，请参阅 man 手册页：
    - lmhosts
    - make_smbcodepage
    - nmbd
    - nmblookup
    - samba
```



- smb.conf
- smbclient
- smbd
- smbmnt
- smbmount
- smbpasswd
- smbrun
- smbspool
- smbstatus
- smbtar
- swat
- testparm
- testprns

- 另请参阅位于 /usr/doc/samba* 以及 Samba 官方网站 `www.samba.org/docs` 上的文档文件。
- *Linux Apache Web Server Administration*，作者 Charles Aulds, (Sybex, 2000)
- *Linux DNS Server Administration*，作者 Craig Hunt, (Sybex, 2000)
- *Linux Samba Server Administration*，作者 Roderick W. Smith, (Sybex, 2000)

## 复习题

1. 以下哪个是特权端口号？
   A. 1
   B. 100
   C. 10000
   D. 100000

2. 指定虚拟主机 IP 地址的 Apache 指令是以下哪个？
   A. AddressVirtualHost
   B. NameVirtualHost
   C. ServerName
   D. ServerIP

3. 反向区域文件（reverse zone file）的作用是什么？
   A. 将 IP 地址映射到主机名。
   B. 将 IP 地址映射到 NetBIOS 主机名。
   C. 将主机名映射到 IP 地址。
   D. 将 NetBIOS 主机名映射到 IP 地址。

4. 要托管 NFS 服务器，必须安装以下哪个软件包？
   A. knfsd
   B. knfsd-clients
   C. netfs
   D. portmap

5. 匿名 FTP 用户可以访问哪些文件？
   A. 用户 `ftp` 主目录中的文件和目录
   B. 任何全球可读目录中的文件
   C. `/tmp` 目录中的文件
   D. 通过用户帐户可读的文件

6. 在 Samba 配置文件的 `hosts allow` 指令中，以下哪个可以指定主机？
   A. `*.example.com`
   B. `.example.com`
   C. `www`
   D. `www.example.com`

7. 要列出可用的 Samba 共享，您可以发出以下哪个命令？
   A. `nmblookup -B server`
   B. `nmblookup -d server`
   C. `smbclient -L server -N`
   D. `testparm`

## 复习题答案

1. A, B。特权端口的编号为 0–1023。
2. B。`NameVirtualHost` 指令指定虚拟主机的 IP 地址；`ServerName` 指令指定虚拟的主机名。
3. A。反向区域文件将 IP 地址映射到主机名；正向区域文件将主机名映射到 IP 地址。
4. C, D。需要 `knfsd`、`knfsd-clients` 和 `portmap` 软件包。或者，您可以安装 `nfs-utils` 软件包，它提供了所有需要的功能。
5. A。匿名 FTP 用户只能访问 `ftp` 用户主目录中的文件和目录。符号链接不会被跟踪。匿名 FTP 用户不需要有用户帐户。
6. B, C, D。`hosts allow` 指令的主机指定符中不使用通配符。
7. C。`smbclient` 命令可以列出可用共享。

# 第 22 章：限制对主要网络服务的访问

本章涵盖的 RHCE 准备主题：

- 熟悉并能够实现对主要网络服务的访问限制。
- 理解 NIS 的基本概念以及与 NIS 和 LDAP 相关的组件。
- 理解 PAM 子系统的目的并能够实现基本的 PAM 配置更改。

通常，网络中的主机比独立主机面临更频繁、更严重的安全威胁。而且，通常规模较大的网络比规模较小的网络面临更大的安全风险。例如，一台 Internet 主机面临着多种威胁。然而，通过控制对网络主机的访问，您可以降低其暴露在安全威胁下的风险。

Red Hat Linux 提供了三种控制主机访问的主要机制：

- **TCP Wrappers**：通过配置 `TCPwrappers`，您可以限制允许访问主机服务的远程主机。
- **可插拔身份验证模块 (PAM) 设施**：通过配置可插拔身份验证模块 (`PAM`) 设施，您可以限制允许登录主机的用户。
- **ipchains 防火墙**：您可以通过配置 `ipchains` 防火墙来限制对服务所用端口的访问。

本章解释前两种机制：TCP wrappers 和 PAM 设施（通常简称为 PAM）。此外，本章还将解释网络信息服务 (NIS) 和轻量级目录访问协议 (LDAP)，这两种机制允许您集中控制用户帐户和其他系统信息。第 30 章“使用 `ipchains` 配置防火墙”将解释第三种机制。

## `inetd` 服务

TCP wrappers 设施与 `inetd` 服务协同工作。本节解释 `inetd` 服务；下一节将解释如何配置与 `inetd` 服务配合工作的 TCP wrappers。

如前一章所述，服务可以独立运行或在 `inetd` 的控制下运行，`inetd` 有时被称为超级服务器（Super Server）。在 `inetd` 控制下运行的服务在空闲时不会消耗内存或处理器资源；因此，在 `inetd` 控制下运行服务可以提高系统效率。使用频率较低且启动快速的服务是运行在 `inetd` 控制下的理想选择。使用频率较高的服务在没有 `inetd` 带来的额外开销时运行效率更高，而启动缓慢的服务在 `inetd` 控制下运行效果较差。

在运行过程中，`inetd` 守护进程监控其控制下的服务端口。当收到客户端请求时，`inetd` 启动该服务以满足客户端请求。

`inetd` 配置文件为 `/etc/inetd.conf`。提高系统安全性的一种简单方法是禁用不必要的服务。对于在 `inetd` 控制下运行的服务，禁用服务只需将 `/etc/inetd.conf` 中相关的行注释掉即可。

以下是一个典型的 `inetd.conf` 文件的内容：

```
#echo	stream	tcp	nowait	root	internal
#echo	dgram	udp	wait	root	internal
#discard	stream	tcp	nowait	root	internal
#discard	dgram	udp	wait	root	internal
#daytime	stream	tcp	nowait	root	internal
#daytime	dgram	udp	wait	root	internal
#chargen	stream	tcp	nowait	root	internal
#chargen	dgram	udp	wait	root	internal
#time	stream	tcp	nowait	root	internal
#time	dgram	udp	wait	root	internal
#
# These are standard services.
#
ftp	stream	tcp	nowait	root	/usr/sbin/tcpd
	in.ftpd -l -a
telnet	stream	tcp	nowait	root	/usr/sbin/tcpd
	in.telnetd
#
# Shell, login, exec, comsat and talk are BSD protocols.
#
shell	stream	tcp	nowait	root	/usr/sbin/tcpd
	in.rshd
login	stream	tcp	nowait	root	/usr/sbin/tcpd
	in.rlogind
#exec	stream	tcp	nowait	root	/usr/sbin/tcpd
	in.rexecd
#comsat	dgram	udp	wait	root	/usr/sbin/tcpd
	in.comsat
talk	dgram	udp	wait	root	/usr/sbin/tcpd
	in.talkd
ntalk	dgram	udp	wait	root	/usr/sbin/tcpd
	in.ntalkd
#dtalk	stream	tcp	wait	nobody	/usr/sbin/tcpd
	in.dtalkd
#
# Pop and imap mail services et al
#
#pop-2	stream	tcp	nowait	root	/usr/sbin/tcpd
	ipopd
#pop-3	stream	tcp	nowait	root	/usr/sbin/tcpd
	ipop3d
#imap	stream	tcp	nowait	root	/usr/sbin/tcpd
	imapd
#
# The Internet UUCP service.
#
#uucp	stream	tcp	nowait	uucp	/usr/sbin/tcpd
# /usr/lib/uucp/uucico	-l
#
# Tftp service is provided primarily for booting. Most
# sites run this only on machines acting as "boot servers.
# " Do not uncomment this unless you "need" it.
#
#tftp	dgram	udp	wait	root	/usr/sbin/tcpd
	in.tftpd
#bootps	dgram	udp	wait	root	/usr/sbin/tcpd
	bootpd
#
# Finger, systat and netstat give out user information
# which may be valuable to potential "system crackers."
# Many sites choose to disable some or all of these
# services to improve security.
#
finger	stream	tcp	nowait	root	/usr/sbin/tcpd
	in.fingerd
#cfinger	stream	tcp	nowait	root	/usr/sbin/tcpd
	in.cfingerd
#systat	stream	tcp	nowait	guest	/usr/sbin/tcpd
	/bin/ps -auwwx
#netstat	stream	tcp	nowait	guest	/usr/sbin/tcpd
	/bin/netstat -f inet
#
# Authentication
#
auth	stream	tcp	nowait	nobody	/usr/sbin/tcpd
	in.identd -l -e -o
```

请注意，许多行以井号 (#) 开头。这些是注释行，被 inetd 服务器忽略。其余行的通用格式为：

```
service socket_type protocol wait_option userid program_path arguments
```

其中：

- `service` 是在 `/etc/services` 中列出的服务
- `socket_type` 对于 TCP 服务的值为 `stream`，对于 UDP 服务的值为 `dgram`（其他有时使用的值请参阅 `inetd.conf` 手册页）
- `protocol` 为 `tcp` 或 `udp`
- `wait_option` 对于 UDP 服务是 `wait`，否则为 `nowait`（其他有时使用的值请参阅 `inetd.conf` 手册页）
- `userid` 指定运行该服务的用户 ID（用户 ID 通常为 root）
- `program_path` 指定可执行文件的路径。（当使用 `TCP wrappers` 时，`program_path` 指定 tcpd 程序的路径，详见下一节。）请注意，许多 TCP 服务的程序名以 `in.` 开头
- `arguments` 是程序使用的参数



示例文件仅启用了以下服务：

- telnet
- ftp
- talk
- ntalk
- shell
- login
- finger
- auth

除 auth 之外，所有这些服务都使用 TCP wrappers 运行，具体在下一节中介绍。

当你修改 inetd.conf 文件时，必须提示 inetd 重新读取该文件。为此，请执行以下命令：

```
killall -HUP inetd
```

有关 inetd 的更多信息，请参阅 Terry Dawson 和 Alessandro Rubini 编写的 NET-3-HOWTO，路径为 /usr/doc/HOWTO/NET-3-HOWTO。

为了亲身体验 inetd 的工作方式，请完成练习 22.1。

### 练习 22.1：配置 inetd

许多（甚至大多数）提供网络服务的 Linux 系统都使用了 inetd 设施。因此，熟悉 inetd 对你来说非常重要。为了观察 inetd 配置更改的效果，请执行以下步骤：

1. 注释掉 inetd.conf 中引用 telnet 的那一行。
2. 提示 inetd 重新加载其配置。
3. 尝试 telnet 到本地主机。客户端请求将不被接受。
4. 识别 inetd.conf 中启用的每项服务。禁用任何实际不需要的服务。

目前，你可以回顾本章和其他资料来帮助你执行这些操作。但在参加 RHCE 考试之前，请确保你能够在不参考考试期间无法提供的资料的情况下操作 inetd。

## TCP Wrappers

tcpd 程序可以控制在 inetd 下运行的服务访问。要使用 tcpd 控制特定服务的访问，请将 tcpd 指定为在收到该服务的客户端请求时应运行的程序。提供该服务的程序名称（以及你想传递给程序的任何运行时参数）作为 tcpd 命令的参数指定。以这种方式运行的服务被称为使用 TCP wrapper 运行。在前面给出的示例 inetd.conf 文件中，telnet 和大多数其他服务都是使用 TCP wrapper 运行的。

tcpd 程序使用两个配置文件：/etc/hosts.allow 和 /etc/hosts.deny。/etc/hosts.allow 文件包含指定服务及其允许使用这些服务的主机的指令；/etc/hosts.deny 文件包含类似的指令，用于指定服务及其禁止使用这些主机的主机。当主机尝试访问具有 TCP wrapper 的服务时，授权过程如下：

1. 如果 /etc/hosts.allow 文件包含一行指定该主机允许访问该服务，则 tcpd 授权访问。
2. 如果 /etc/hosts.deny 文件包含一行指定该主机禁止访问该服务，则 tcpd 拒绝访问。
3. 在所有其他情况下，tcpd 授权访问。

### /etc/hosts.allow 文件

如前所述，如果 /etc/hosts.allow 文件包含一行指定某主机允许访问某服务，则 tcpd 授权访问。文件中的行具有以下通用形式：

```
service: host_list
```

其中 `service` 标识一个服务，其名称与 `/etc/inetd.conf` 和 `/etc/services` 文件中使用的名称相同，而 `host_list` 指定一个或多个允许访问该服务的主机。每个主机之间用逗号分隔。

主机可以通过以下几种方式之一指定：

- 通过 IP 地址，例如 192.168.1.1
- 作为网络地址/掩码对，例如 192.168.1.0/255.255.255.0

![](img/4eef9c6f2f52b608eba628cf4e2793ce_558_0.png)

你还可以通过指定一个不完整的 IP 地址后接一个点来指定一个地址范围。例如，192.168.1. 指的是与 192.168.1.0/255.255.255.0 相同的 IP 地址范围。

- 通过主机名，例如 `www.azusapacific.com`
- 通过域名或子域名，例如 `.azusapacific.com`（注意前面的点）
- 通过关键字 LOCAL，表示本地主机

![](img/4eef9c6f2f52b608eba628cf4e2793ce_558_1.png)

由于实现中的一个 quirk（古怪之处），关键字 LOCAL 匹配任何没有点的主机名。例如，LOCAL 将匹配在 `/etc/hosts` 中输入的没有点的主机名。如果你使用关键字 LOCAL，请确保不会无意中给非本地主机授予特殊权限。

- 通过关键字 ALL，表示所有主机

你还可以使用关键字 EXCEPT 来指定通用规则的例外。例如，以下指令：

```
in.ftpd: ALL EXCEPT 192.168.1.0/192.168.1.255
```

指定除了 192.168.1.0 到 192.168.1.255 范围内的主机外，所有主机都可以访问 FTP 服务。

你可以使用 ALL 和 EXCEPT 关键字来指定服务以及主机。例如，以下指令：

```
ALL EXCEPT in.telnetd: www.azusapacific.com
```

指定主机 `www.azusapacific.com` 可以访问除 telnet 以外的所有服务。

> **警告**
> 即使在 inetd.conf 文件中没有提到，portmap 服务也被配置为使用 TCP wrappers。但是，你不能使用主机名或域名来指定对 portmap 服务的访问；请仅使用 IP 地址或 ALL 和 EXCEPT 关键字。

### /etc/hosts.deny 文件

如前所述，如果 `/etc/hosts.deny` 文件包含一行指定某主机禁止访问某服务，除非该访问被 `/etc/hosts.allow` 文件中的某一行授权，否则 tcpd 将拒绝访问。`/etc/hosts.deny` 文件中的行形式与 `/etc/hosts.allow` 文件中的行相同。如果访问没有被 `/etc/hosts.allow` 文件明确授权，也没有被 `/etc/hosts.deny` 文件禁止，则该访问被授权。

> **警告**
> 即使在 inetd.conf 文件中没有提到，portmap 服务也被配置为使用 TCP wrappers。但是，你不能使用主机名或域名来指定对 portmap 服务的访问；请仅使用 IP 地址或 ALL 和 EXCEPT 关键字。请注意，通过 ALL 关键字拒绝所有服务的访问可能会隐式地拒绝对 portmap 的访问，这将破坏网络文件系统 (NFS) 和其他依赖 portmap 的服务。

### 检查 TCP Wrappers

TCP wrappers 背后的正向/反向逻辑很容易让人混淆。`tcpdchk` 命令可以帮助你确定是否正确配置了 TCP wrappers。执行命令：

```
tcpdchk -v
```

该命令将通过列出你指定的规则来响应，如下所示：

```
Using network configuration file: /etc/inetd.conf

>>> Rule /etc/hosts.allow line 6:
    daemons: ALL
    clients: .apu.edu 216.128.177.244 127.0.0.1
    access: granted
```

你可以检查输出，以确定 `tcpd` 对你规范的理解是否与你一致。

另一个有用的命令是 `tcpdmatch`。执行如下形式的命令：

```
tcpdmatch service host
```

其中 `service` 指定一个配置为使用 TCP wrappers 的服务，`host` 指定一个真实或假设的主机。该命令将确定你的配置是否允许指定的主机访问指定的服务，并报告结果。以下是此类结果的一个示例。

```
tcpdmatch in.ftpd www.example.net
client: address 192.168.1.1
server: process in.ftpd
access: granted
```

### 使用 twist 替换服务

`twist` 指令可用于 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件，以用替代服务替换请求的服务。例如，`/etc/hosts.allow` 中的这一行：

```
in.telnetd : .example.net : twist /usr/local/sbin/telnet
```

对于 `example.net` 域中的客户端主机，用程序 `/usr/local/sbin/telnet` 替换通常的 `telnet` 服务。

你也可以在 `/etc/hosts.deny` 文件中使用 `twist` 指令。例如，以下指令：

```
in.telnetd : .example.net : twist /bin/echo Hosts from example.net not welcome
```

为 `example.net` 域中的客户端主机显示自定义的欢迎词（不欢迎消息）。

### 进一步信息

有关 TCP wrappers 的更多信息，请参阅 man 页 hosts_access (5) 和 hosts_options (5)。现在，通过完成练习 22.2 来看 TCP wrappers 是如何工作的。

### 练习 22.2：指定 TCP Wrappers

TCP wrappers 是网络安全策略的重要组成部分，通常应为连接到非本地网络的主机实施。为了观察 TCP wrappers 的工作方式，请执行以下步骤：

1. 指定一个 TCP wrapper，拒绝本地主机访问 telnet。验证本地主机的访问被拦截，但其他地方未被拦截。
2. 指定一个 TCP wrapper，拒绝除本地主机以外的所有主机访问 telnet。验证本地主机的访问未被拦截，但其他地方被拦截。

在执行所需操作时，你可以参考本章和其他资料。但在参加 RHCE 考试之前，请确保你能够在不需要此类帮助的情况下实现 TCP wrappers。

## 网络信息服务 (NIS)

Red Hat Linux 包含了 Sun Microsystems (Sun) 网络信息服务 (NIS) 第 2 版的实现，该服务以前被称为 Yellow Pages (YP)。NIS 通过让你集中管理用户帐户、邮件别名、主机、网络等信息，方便了局域网的管理。由 NIS 管理的网络称为 NIS 域，必须包含一个主服务器，也可以包含从服务器。包含网络信息的数据库被称为 map（映射）。map 中包含的信息元素（例如网络的名称和 IP 地址）称为 key（键）。

NIS 的安全性不高；例如，拥有 NIS 服务器访问权限的用户可以获取该服务器 NIS map 的完整内容。Sun 较新的 NIS+ 设施更加安全。然而，Red Hat Linux 仅支持 NIS+ 客户端，不支持 NIS+ 服务器。



与 NIS 相关的 Red Hat 软件包管理器 (RPM) 包有：

- `ypbind`，NIS 客户端
- `ypserv`，NIS 服务器
- `yp-tools`，有用的 NIS 工具和实用程序

此外，NIS 需要 `portmap` 服务。
`/etc/nsswitch.conf` 文件指定了 NIS 配置。NIS 服务器将域信息存储在 `/var/yp/domain` 中；NIS 客户端将缓存信息存储在 `/var/yp/binding` 中。
您可以轻松地判断一台主机是否由 NIS 管理。请执行以下命令：

```
domainname
```

如果该主机属于一个 NIS 域，该命令将报告该域的名称。

### NIS 命令

NIS 客户端使用的最重要命令和程序包括：

- **ypbind** 查找 NIS 信息并将其存储在 `/var/yp/binding` 中
- **ypwhich** 返回 NIS 服务器的名称
- **ypcat** 打印指定映射（map）中的键
- **yppoll** 打印指定映射的版本号，并识别该映射所在的服务器
- **ypmatch** 打印指定映射中选定的键
- **yppasswd** 更改 NIS 密码

NIS 服务器使用的最重要命令和程序包括：

- **ypserv** NIS 守护进程的可执行文件名
- **makedbm** 从文本文件创建映射数据库
- **yppush** 通知从服务器映射已更新
- **yppasswdd** 处理 NIS 密码更改的守护进程

有关这些命令的更多信息，请参阅相关的 man 手册页。

### NIS 配置

主要的 NIS 配置文件是 `/etc/nsswitch.conf`。以下是 Red Hat Linux 发行版中该文件的内容：

```
# /etc/nsswitch.conf
#
# An example Name Switch Service config file. This file
# should be sorted with the most-used services at the
# beginning.
#
# The entry '[NOTFOUND=return]' means that the search for an
# entry should stop if the search in the previous entry
# turned up nothing. Note that if the search failed due to
# some other reason (like no NIS server responding) then
# the search continues with the next entry.
#
# Legal entries are:
#
#	nisplus or nis+	Use NIS+ (NIS version 3)
#	nis or yp	Use NIS (NIS version 2),
#			also called YP
#	dns		Use DNS (Domain Name
#			Service)
#	files		Use the local files
#	db		Use the local database
#			(.db) files
#	compat		Use NIS on compat mode
#	[NOTFOUND=return]	Stop searching if not found
#			so far
#
#
# To use db, put the "db" in front of "files" for entries
# you want to be looked up first in the databases
#
# Example:
#passwd:  db files nisplus nis
#shadow:  db files nisplus nis
#group:   db files nisplus nis
passwd: files nisplus nis
shadow: files nisplus nis
group: files nisplus nis

#hosts: db files nisplus nis dns
hosts: files nisplus nis dns

services: nisplus [NOTFOUND=return] files
networks: nisplus [NOTFOUND=return] files
protocols: nisplus [NOTFOUND=return] files
rpc: nisplus [NOTFOUND=return] files
ethers: nisplus [NOTFOUND=return] files
netmasks: nisplus [NOTFOUND=return] files
bootparams: nisplus [NOTFOUND=return] files

netgroup: nisplus

publickey: nisplus

automount: files nisplus
aliases: files nisplus
```

第二个重要的 NIS 配置文件是 `/etc/yp.conf`。以下是 Red Hat Linux 发行版中 `/etc/yp.conf` 文件的内容。

```
# /etc/yp.conf - ypbind configuration file
# Valid entries are
#
#domain NISDOMAIN server HOSTNAME
# Use server HOSTNAME for the domain NISDOMAIN.
#
#domain NISDOMAIN broadcast
# Use broadcast on the local net for domain
# NISDOMAIN
#
#ypserver HOSTNAME
# Use server HOSTNAME for the local domain. The
# IP-address of server must be listed in /etc/hosts.
#
```

除注释行外，每行指定一个 NIS 映射，并按搜索顺序指定用于获取其键的源。表 22.1 总结了 NIS 映射，表 22.2 总结了用于指定源的关键字。

#### 表 22.1 NIS 映射

| NIS 映射 | 默认共享 | 描述 |
| :--- | :--- | :--- |
| aliases | 否 | 邮件别名 |
| ethers | 否 | 以太网地址 |
| group | 是 | 用户组 |
| hosts | 是 | 主机名和 IP 地址 |
| netgroup | 是 | 主机和用户列表 |
| networks | 是 | 网络名称和 IP 地址 |
| passwd | 是 | 用户账户信息 |
| protocols | 是 | 网络协议 |
| publickey | 否 | secure_rpc 使用的密钥 |
| rpc | 是 | RPC 调用名称 |
| services | 是 | 网络服务 |
| shadow | 否 | Shadow 密码 |

#### 表 22.2 NIS 映射的源

| 源 | 描述 |
| :--- | :--- |
| compat | NIS（处于与旧版本标准 C 库兼容的模式） |
| db | 本地数据库 |
| dns | DNS |
| files | 本地文件 |
| nis | NIS |
| nisplus | NIS+ |

有关 NIS 的更多信息，请参阅 Thorsten Kukuk 编写的 *NIS HOWTO*，路径为 `/usr/doc/HOWTO/NIS-HOWTO`。

## 轻量级目录访问协议 (LDAP)

轻量级目录访问协议 (LDAP) 提供了可以存储任意信息的数据库。因此，LDAP 可以用于多种用途。其中，LDAP 与安全套接字层 (SSL) 结合时，可以提供比 NIS 更安全的替代方案。例如，带有 SSL 的 LDAP 具有加密的数据传输和访问控制列表 (ACL)，用于指定哪些用户可以访问存储在 LDAP 数据库中的信息。与依赖刷新间隔来通知从主机存储映射更改的 NIS 不同，LDAP 可以将数据库更新推送到客户端。

LDAP 包含在 `openldap` 软件包中，该包提供：

- `slapd` 运行在 389 端口的 LDAP 守护进程
- `slurpd` 复制 LDAP 数据库的 LDAP 守护进程

主要的 LDAP 配置文件是 `/etc/openldap/slapd.conf`。有关 LDAP 的更多信息，请参阅 `/usr/doc/openldap-*` 中的文件以及 LDAP 网站 `www.openldap.org` 上的文档。另请参阅以下与 LDAP 相关的 man 手册页：

- centipede
- chlog2replog
- edb2ldif
- fax500
- go500
- go500gw
- in.xfingerd
- ldap.conf
- ldapadd
- ldapd
- ldapdelete
- ldapfilter.conf
- ldapfriendly
- ldapmodify
- ldapmodrdn
- ldappasswd
- ldapsearch
- ldapsearchprefs.conf
- ldaptemplates.conf
- ldbmcat
- ldif
- ldif2id2children
- ldif2id2entry
- ldif2index
- ldif2ldbm
- mail500
- rcpt500
- slapd
- slapd.conf
- slapd.replog
- slurpd
- ud
- ud.conf

## 可插拔认证模块 (PAM) 设施

Red Hat Linux 的可插拔认证模块 (PAM) 设施通常简称为 PAM。PAM 允许您为各种程序配置安全策略。每个支持 PAM 的程序都有一个位于 `/etc/pam.d` 的配置文件。与程序关联的文件内容决定了该程序如何授权对其功能的访问。通过使用 PAM，您可以在不修改和重新编译程序的情况下配置授权策略。

PAM 由一系列动态加载的库模块组成。支持 PAM 的程序的配置文件决定了用于验证授权的模块，从而决定了采取的操作。以下是一些最重要的 PAM 模块列表：

- **pam_access.so** 该模块限制可以访问服务的远程主机。
- **pam_console.so** 该模块通过将通过控制台登录的用户设为特殊动态组 **console** 的成员，从而授予他们特殊权限。通过这种方式，控制台用户能够访问软盘驱动器、声音子系统和操纵杆，并能执行重启和关闭系统等特权操作。
- **pam_listfile.so** 该模块查阅指定的文件以确定授权情况。FTP 服务使用此模块拒绝 `/etc/ftpusers` 中列出的用户访问 FTP。
- **pam_nologin.so** 当 `/etc/nologin` 文件存在时，该模块阻止除 **root** 以外的用户登录。
- **pam_securetty.so** 这禁止从 `/etc/securetty` 中列出的 tty 设备以外的设备以 root 身份登录。
- **pam_time.so** 该模块根据日期或一天中的时间限制用户访问服务的时间。



### PAM 感知程序

支持 PAM（可插拔认证模块）的程序包括：

- chfn
- chsh
- ftp
- gnorpm-auth
- halt
- imap
- kde
- linuxconf
- linuxconf-pair
- login
- passwd
- pop
- poweroff
- ppp
- reboot
- rexec
- rlogin
- rsh
- samba
- shutdown
- ssh
- su
- sudo
- xdm
- xscreensaver
- xserver

### PAM 配置文件

PAM 配置文件指定了一系列应当被加载和执行的模块，用于授权访问相关的设施。一个模块通常返回一个通过/失败的值。由一系列模块返回的值将用于决定是授予还是拒绝访问。

PAM 配置文件中包含的指令具有以下通用格式：

`module_type control_flag module_path arguments`

`module_type` 字段指示执行的授权类型。可以执行的授权类型有：

- **account** 表示访问受密码有效期、时间、可用资源或用户位置的限制。
- **auth** 表示用户需要经过身份验证，例如通过提示输入密码。
- **password** 表示如果合适，可以更新用户的认证信息，例如用户更改其密码时。
- **session** 表示在用户被授予访问权限之前或之后应当执行的任务。

`control_flag` 字段指示模块的返回值如何影响最终结果。控制标志的值可以是以下任何一个：

- optional
- required
- requisite
- sufficient

所有控制标志值为 `required` 和 `requisite` 的模块必须返回通过；否则，授权被拒绝。通常情况下，所有模块都会被执行；但是，如果一个控制标志值为 `requisite` 的模块失败，访问将被立即拒绝。同样，如果一个控制标志值为 `sufficient` 的模块成功，访问将被立即授予。控制标志值为 `optional` 的模块不影响最终结果。

*module_path* 字段指定要执行的模块位置。请参阅 `/usr/doc/pam-*` 中的文档文件，以获取可用模块的完整列表及其功能和操作说明。

*arguments* 字段指定以下值之一：

- **debug** 表示调试信息应发送到系统日志。
- **no_warn** 表示模块不应发出警告消息。
- **use_first_pass** 表示模块应使用之前输入的密码，而不是提示输入。
- **try_first_pass** 表示模块应使用之前输入的密码，而不是提示输入。但是，如果之前输入的密码失败，模块将提示输入新密码。
- **use_mapped_pass** 表示模块应使用之前输入的响应来生成用于存储或检索密码的加密或解密密钥。

现在，完成练习 22.3 以获得操作 PAM 的实践经验。

### 练习 22.3：配置 PAM

每个 Red Hat Linux 系统都预配置了使用 PAM。除非你对默认配置感到满意，否则你需要具备一定的 PAM 操作技能，以便建立改进的配置。执行以下步骤以获得操作 PAM 的经验：

1. 修改 FTP 的 PAM 配置文件，允许 root 用户访问 FTP 服务。验证 root 是否可以这样做。
2. 修改相应的 PAM 配置文件，允许 root 用户进行远程登录。验证 root 是否可以远程登录。
3. 恢复原始的 PAM 配置，以避免可能的安全漏洞。

在完成此练习时，你可以参考本章内容和 PAM 文档。但在参加 RHCE 考试之前，请确保你熟练使用 PAM，能够在不参考书籍、笔记或其他帮助的情况下执行此类操作。

## 总结

在本章中，你学习了如何限制对网络服务的访问。涵盖的最重要主题包括：

**`inetd` 服务** `inetd` 服务调解对 TCP 服务的请求，在收到客户端请求时启动相应的服务器。该服务的配置文件是 `/etc/inetd.conf`。

**TCP Wrappers** `tcpd` 守护进程可以限制对由 `inetd` 控制的服务访问。`/etc/hosts.allow` 和 `/etc/hosts.deny` 配置文件标识了允许或禁止访问服务的主机。相关的 `twist` 程序可用于通过将指定程序替换为原本将要启动的服务来响应客户端请求。

**网络信息服务 (NIS)** NIS 提供了一组中心化数据库（称为 `maps`），有助于在网络中管理用户账户、邮件别名、主机、网络和其他信息。NIS 存在若干安全缺陷，目前已不被广泛使用。

**可插拔认证模块 (PAM) 设施** PAM 设施是 Red Hat Linux 的一项功能，允许你配置 PAM 感知程序的安全相关选项。例如，你可以使用 PAM 设施来定制限制有效密码形式的策略。PAM 感知程序的 PAM 配置位于 `/etc/pam.d`。

### 关键术语

在进入下一章之前，请确保你熟悉以下术语：

- key
- LDAP
- maps
- NIS
- PAM
- TCP wrappers

## 其他信息来源

有关限制访问主要网络服务的更多信息，请参阅：

- LDAP 文档 `/usr/doc/openldap-*` 以及 LDAP 网站 `www.openldap.org`
- Terry Dawson 和 Alessandro Rubini 编写的 `NET-3-HOWTO`，路径 `/usr/doc/HOWTO/NET-3_HOWTO`
- Thorsten Kukuk 编写的 `NIS HOWTO`，路径 `/usr/doc/HOWTO/NIS-HOWTO`
- PAM 文档文件 `/usr/doc/pam-*`

## 复习题

1. 以下哪个是用于配置 TCP wrappers 的配置文件？
   A. `/etc/allow`
   B. `/etc/hosts`
   C. `/etc/hosts.allow`
   D. `/etc/tcpwrapper`

2. 对于 `inetd.conf` 中指定的 UDP 服务，通常应设置以下哪个选项？
   A. `nowait`
   B. `stream`
   C. `udp`
   D. `wait`

3. 假设 `/etc/hosts.deny` 禁止所有访问，以下哪个 `/etc/hosts.allow` 条目仅允许本地主机访问 FTP 服务？
   A. `ftpd: LOCAL`
   B. `ftpd: LOCAL ONLY`
   C. `in.ftpd: LOCAL`
   D. `in.ftpd: LOCAL ONLY`

4. 以下哪个是合理的 `/etc/hosts.allow` 指令？
   A. `imapd: 192.168.1.1`
   B. `imapd: www.example.net`
   C. `portmap: 192.168.1.1`
   D. `portmap: www.example.net`

5. 以下哪个为网络信息管理提供了安全的环境？
   - A. 带有 SSL 的 LDAP
   - B. NIS
   - C. NIS+
   - D. SSL

6. 实现 LDAP 应该安装哪个 RPM 软件包？
   - A. ldap
   - B. ldapis
   - C. ldapssl
   - D. openldap

## 复习题答案

1. C. 文件 /etc/inetd.conf, /etc/hosts.allow 和 /etc/hosts.deny 用于配置 TCP wrappers。

2. C, D. UDP 服务通常应在 `udp` 协议选项之外地接收 `wait` 选项。

3. C. FTP 服务在 inetd 中被识别为 in.ftpd。`LOCAL` 关键字指定对本地主机的访问。

4. A, B, C. `portmap` 服务不应使用需要 DNS 解析的主机名来指定。

5. A, C. NIS 不是一个高度安全的服务。SSL 本身不提供网络信息管理，但它可以与 LDAP 结合使用来实现此目的。

6. D. `openldap` 软件包包含对 LDAP 的支持。

# 第 23 章：理解次要网络服务

**本章涵盖的 RHCE 准备主题：**

- 熟悉 Red Hat Linux 支持的次要网络服务，如 DHCP、IPX、lpd、Internet news、squid 和时间同步。



除了第 21 章中涵盖的主要网络服务外，Red Hat Linux 还支持许多其他附加服务。本章将介绍几个最重要且最常用的次要网络服务。Red Hat, Inc. 为 Red Hat 认证工程师（RHCE）考试设定的学习重点仅要求对这些次要网络服务有概念上的熟悉。因此，本章重点讨论与次要网络服务相关的基本概念；不过，它也包含了一些旨在帮助您安装、配置和使用这些服务的实用技巧。

## 动态主机配置协议 (DHCP)

动态主机配置协议 (DHCP) 服务器可以帮助您管理网络的 IP 地址空间。Red Hat Linux 的 DHCP 服务器与一些 Unix 环境中仍在使用的老旧 BOOTP 协议兼容。如果您的网络中包含间歇性连接或在不同位置间移动的计算机（例如笔记本电脑），DHCP 将特别有用。

当运行 DHCP 客户端的主机启动时，它会联系 DHCP 服务器。DHCP 服务器可以分配如下的主机相关信息：

- IP 地址
- 主机名和域名
- 网络 IP 地址
- 广播 IP 地址
- 默认网关 IP 地址
- DNS 服务器 IP 地址
- WINS 服务器 IP 地址

DHCP 服务器可以配置为提供静态信息、动态信息或两者兼有。静态配置根据分配给客户端网络接口的媒体访问控制 (MAC) 地址以及客户端网络连接点的子网地址，为客户端提供一个固定 IP 地址。因此，主机标识和位置的组合决定了所分配的配置。

动态配置从一个或多个范围中随机分配 IP 地址。这可以节省 IP 地址，因为只有处于活动状态的主机才拥有关联的 IP 地址。然而，主机每次启动时关联的 IP 地址可能会有所不同。DHCP 配置可以同时是动态和静态的，为指定主机提供静态配置，为其他主机提供动态配置。

### 安装 DHCP

DHCP 服务器包含在 `dhcp` 软件包中。要安装 DHCP，请进入包含该软件包的目录并执行命令：

```bash
rpm -Uvh dhcp-*.rpm
```

DHCP 要求相关的网络接口支持并配置为广播和多播操作。要确定网络接口是否配置正确，请执行命令：

```bash
ifconfig -a
```

关于典型网络接口的输出应类似于以下内容：

```text
eth1 Link encap:Ethernet HWaddr 00:A0:CC:25:8A:AC
    inet addr:192.168.1.1 Bcast:192.168.1.255
    Mask:255.255.255.0
    UP BROADCAST RUNNING PROMISC MULTICAST MTU:1500
    Metric:1
    RX packets:4648466 errors:0 dropped:0 overruns:0
    frame:0
    TX packets:679303 errors:0 dropped:0 overruns:0
    carrier:0
    collisions:33062 txqueuelen:100
    Interrupt:11 Base address:0x6000
```

注意输出第三行中出现的关键词 BROADCAST 和 MULTICAST。如果这些关键词不存在，DHCP 将无法正常运行。要解决此问题，您可能需要执行以下操作中的一项或全部：

- 使用 `ifconfig` 命令重新配置接口。
- 将网络接口更换为支持 MULTICAST 的网卡。

### 配置 DHCP

DHCP 配置文件是 `/etc/dhcpd.conf`。这是一个典型的配置，其中包含动态和静态信息：

```text
default-lease-time 64800;
max-lease-time 64800;

option subnet-mask 255.255.255.0;
option broadcast-address 192.168.1.255;
option routers 192.168.1.1;
option domain-name-servers 192.168.1.1;
option domain-name "azusapacific.com";

subnet 192.168.1.0 netmask 255.255.255.0 {
    server-identifier 192.168.1.1;

    host sara {
        hardware ethernet 00:50:04:d2:3f:15;
        fixed-address 192.168.1.33;
        default-lease-time 2592000;
    }

    range 192.168.1.20 192.168.1.29;
}

subnet 192.168.100.0 netmask 255.255.255.0 {
```

该配置将 IP 地址 192.168.1.33 分配给 MAC 地址为 00:50:04:d2:3f:15 的接口。其他 DHCP 客户端被分配 192.168.1.20 到 192.168.1.29 范围内的 IP 地址。有关 `/etc/dhcpd.conf` 文件内容的更多信息，请参阅 man 手册页 `dhcpd.conf`。在启动 DHCP 服务之前，您必须创建文件 `/var/state/dhcp/dhcpd.leases`；否则，DHCP 服务器在启动后会立即终止。要创建该文件，请执行以下命令：

```bash
touch /var/state/dhcp/dhcpd.leases
```

某些版本的 Red Hat Linux 要求您将 dhcpd.leases 文件放置在 /etc 中。

一旦 DHCP 服务启动，它会将其做出的分配（称为 *租约*，leases）存储在 `dhcpd.leases` 文件中，您可以使用例如 `more` 命令或文本编辑器来查看该文件。以下是此类租约的示例：

```text
lease 192.168.1.20 {
    starts 6 2000/02/12 09:20:15;
    ends 2 2000/05/09 13:58:16;
    hardware ethernet 00:0e:98:77:08:40;
    uid 01:00:0e:98:77:08:40;
    client-hostname "OEMComputer";
}
lease 192.168.1.24 {
    starts 0 2000/03/12 18:20:23;
    ends 0 2000/03/12 18:20:23;
    hardware ethernet 00:50:56:be:01:03;
}
lease 192.168.1.23 {
    starts 6 2000/03/11 21:52:29;
    ends 6 2000/03/11 23:52:29;
    hardware ethernet 00:50:56:a0:01:03;
}
lease 192.168.1.22 {
    starts 6 2000/03/11 21:46:24;
    ends 6 2000/03/11 23:46:24;
    hardware ethernet 00:50:56:b9:01:03;
}
lease 192.168.1.21 {
    starts 6 2000/03/11 18:17:53;
    ends 6 2000/03/11 18:18:39;
    hardware ethernet 00:50:56:a7:01:03;
}
```

租约在 `/etc/dhcpd.conf` 中指定的一段时间内有效，之后必须由客户端续租。要启动配置好的 DHCP 服务器，请执行命令：

```bash
/etc/rc.d/init.d/dhcpd start
```

当使用 Microsoft Windows 客户端配合 DHCP 时，DHCP 应添加一条到主机 255.255.255.255 的路由；该路由是与 Microsoft DHCP 客户端通信所必需的。检查系统日志以获取指示 DHCP 状态的消息。您可以通过执行以下命令来实现：

```bash
tail /var/log/messages
```

结果应类似于以下内容：

```text
May 9 07:18:45 www dhcpd: Internet Software Consortium
DHCPD $Name:
V2-BETA-1-PATCHLEVEL-6 $
May 9 07:18:45 www dhcpd: Copyright 1995, 1996, 1997, 1998
The Internet Software Consortium.
May 9 07:18:45 www dhcpd: All rights reserved.
May 9 07:18:45 www dhcpd: Listening on
Socket/eth1/192.168.1.0
May 9 07:18:45 www dhcpd: Sending on
Socket/eth1/192.168.1.0
May 9 07:18:45 www dhcpd: Listening on
Socket/eth0/192.168.100.0
May 9 07:18:45 www dhcpd: Sending on
Socket/eth0/192.168.100.0
May 9 07:19:33 www dhcpd: dhcpd shutdown succeeded
```

### DHCP 客户端

标准的 Red Hat Linux DHCP 客户端是一个名为 `pump` 的程序，包含在同名的软件包中。`pump` 软件包是 Red Hat Linux 标准基础安装的一部分。

要配置 Red Hat Linux 主机使用 DHCP 来确定其网络配置，请启动 `linuxconf` 并选择 配置 $\rightarrow$ 网络 $\rightarrow$ 客户端任务 $\rightarrow$ 基本主机信息。选择与您要配置的网络接口（适配器）相对应的段落或选项卡。设置以下选项：

- Enabled（已启用）
- Config Mode = DHCP（配置模式 = DHCP）

选择 接受 $\rightarrow$ 退出 $\rightarrow$ 激活更改以安装新配置。图 23.1 显示了图形模式下相关的 `linuxconf` 屏幕。

#### 图 23.1 linuxconf 主机基本配置屏幕
![](img/4eef9c6f2f52b608eba628cf4e2793ce_583_0.png)

您可以通过执行以下命令检查 `pump` 的状态：

```bash
/sbin/pump -s
```

要强制立即续租，请执行命令：

```bash
/sbin/pump -i eth0 -R
```

### 关于 DHCP 和 pump 的更多信息

有关 DHCP 的更多信息，请参阅：

- DHCP 网页 `www.isc.org`
- Vladimir Vuksan 编写的 `DHCP mini-HOWTO`，位于 `/usr/doc/dhcp-*`
- `/usr/doc/dhcp-*` 中的 DHCP 文档

有关 `pump` 的更多信息，请参阅其 man 手册页。



## IPX 协议

Red Hat Linux 包含了 `mars-nwe` 软件包。该软件包为基于 IPX 协议的 Novell 网络提供文件和打印机共享。相关的 `ipxutils` 软件包包含实用的 IPX 实用程序。如果您在基于 IPX 的网络环境下工作，建议安装这两个软件包。

`mars-nwe` 软件包允许您使用 `ncpmount` 命令或使用指定文件系统类型为 `ncp` 的 `mount` 命令来挂载 IPX 文件系统。您也可以在 `/etc/fstab` 文件中指定 IPX 文件系统。

`mount` 命令将文件系统类型报告为 `ncpfs`；但您可以在 `mount` 命令的参数以及 `/etc/fstab` 文件中指定 `ncp` 或 `ncpfs`。

有关在 Linux 下使用 IPX 的更多信息，请参阅 `/usr/doc/mars-nwe-*` 中的 `mars_nwe` 文档和 `/usr/doc/ipxutils-*.` 中的 `ipxutils` 文档。另请参阅以下 man 手册页：

- ipx_cmd
- ipx_configure
- ipx_interface
- ipx_internal_net
- ipx_route
- ncopy
- ncpmount
- nprint
- nsend
- nwauth
- nwbcreate
- nwbols
- nwboprops
- nwborm
- nwbpadd
- nwbpcreate
- nwbprm
- nwbpset
- nwbpvalues
- nwclient
- nwdir
- nwfsctrl
- nwfsinfo
- nwfstime
- nwgrant
- nwmsg
- nwpasswd
- nwpurge
- nwrevoke
- nwrights
- nwsfind
- nwtrustee
- nwuserlist
- nwvolinfo
- pqlist
- pqrm
- pqstat
- pserver
- slist

## 通过 lpd 远程访问打印机

您可以轻松地远程访问 Red Hat Linux 打印机。当然，您必须首先配置服务器和客户端系统。要配置服务器系统，请在 `/etc/hosts.lpd` 中列出每个客户端主机。如果客户端主机与服务器处于相同的管理控制之下，根据您的偏好，您也可以将该主机列在 `/etc/hosts.equiv` 中。此外，请确保客户端主机的主机名可以解析为 IP 地址；如有必要，请在 `/etc/hosts` 中添加一行。

要配置客户端，请在客户端的 `/etc/printcap` 文件中添加如下格式的条目：

```
remlp1:
:lp=rm:host=printer:sd=dir
```

在此条目中，*host* 是服务器的主机名，*printer* 是目标打印机在服务器 `/etc/printcap` 文件中列出的名称，*dir* 是客户端将要使用的 spool 目录。spool 目录通常是 `/var/spool` 的一个子目录。

一旦服务器和客户端配置完成，您应该可以通过在客户端主机上发出命令来访问服务器的打印机。例如，您可以使用 `lpr` 命令打印文件，并使用 `lpq` 命令检查打印队列。

## 互联网新闻 (Internet News)

`inn` 软件包提供了 `innd` 和其他支持 *网络新闻传输协议 (NNTP)* 和互联网新闻的程序。互联网新闻用于向互联网新闻组传输和接收帖子，在 Web 出现之前，这是用户之间多向互动的主导方式。如今，Web 论坛提供了一种更简单的多向用户交互支持方式。然而，互联网新闻仍然是一项受欢迎的服务，尽管其操作复杂且需要大量资源。您可以使用 `inn` 来支持本地新闻组或提供对互联网新闻组的访问。为了充分支持互联网新闻组，主机系统必须拥有数 GB 的可用硬盘空间和高速互联网连接。

与电子邮件一样，互联网新闻也成为了传输垃圾邮件的手段。为了抑制垃圾新闻文章，您可以安装 `cleanfeed` 软件包。

## 时间同步

Red Hat Linux 提供了两种同步系统时间的方法：

- rdate，同步到另一个主机的时钟
- xntp3，同步到协调世界时 (UTC)

包含在 `rdate` 软件包中的 `rdate` 程序是一种较旧且较简单的时间同步方法。要将本地主机的时钟同步到另一个系统，请发出如下形式的命令：

```bash
rdate -p -s host
```

其中 `host` 是远程主机的主机名。通常，此类命令被放置在 `/etc/rc.d/rc.local` 文件中，以便在系统启动时执行。一旦同步，时钟往往会产生漂移；`rdate` 命令没有提供持续同步的机制。

包含在 `xntp3` 软件包中的 `xntpd` 程序根据从远程服务器获取的时间数据，将系统时钟持续同步到 UTC 的精确估计值。您可以配置 `xntpd` 服务在所需的运行级别下运行。或者，您可以使用 `cron` 设施定期运行 `ntpdate`（`xntp3` 软件包中的另一个程序）；当被调用时，`ntpdate` 会调整系统时钟然后终止。`xntpd` 和 `ntpdate` 都使用 RFC 1305 中描述的 *网络时间协议 (NTP)*。通常，主机被配置为与多个主机同步，这样即使某个主机无法联系，同步也可以继续。

NTP 主机排列成一个层级结构。处于层级顶端附近的服务器——称为 *stratum 1* 服务器——从高精度的地面源接收时间信息，例如由原子钟发送的无线电信号。stratum 2 的服务器同步到一个或多个 stratum 1 服务器，依此类推。

NTP 持续调整系统时间，精度通常可达毫秒级。NTP 永远不会将时钟向后调整；如有必要，它会减慢时钟速度，直到真实时间追上偏差的时钟。

在某些 `xntp3` 软件包版本中，主要 NTP 命令 `ntpdate` 和其他 NTP 程序的 man 手册页缺失。以下是 `ntpdate` 的 man 手册页：

```text
ntpdate - set the date and time via NTP
SYNOPSIS
ntpdate [ -bdos ] [ -a key# ] [ -e authdelay ] [ -k
=>keyfile ]
[ -p samples ] [ -t timeout ] server ...
DESCRIPTION
Ntpdate sets the local date and time by polling the Network
```

时间协议服务器（作为参数给出的主机），以确定正确的时间。它必须在本地主机上以 root 身份运行。从每个指定的服务器获取若干样本，并应用标准 NTP 时钟过滤和选择算法来选择其中最佳的一个。通常，ntpdate 可以插入到 /etc/rc.local 启动脚本中，以便在启动时设置当天时间，且/或可以通过 cron(8) 定期运行。请注意，随着服务器数量的增加，ntpdate 的可靠性和精度将大幅提高。虽然可以使用单个服务器，但通过提供至少三四个或更多服务器，可以获得更好的性能以及对任何单个服务器异常情况更强的抵抗力。

ntpdate 通过两种方式之一进行时间调整。如果 ntpdate 确定您的时钟偏差超过 0.5 秒，它将直接通过调用 settimeofday(2) 来步进时间。然而，如果误差小于 0.5 秒，默认情况下，它将通过调用 adjtime(2) 并带上偏移量来平滑调整 (slew) 时钟时间。当偏移量较小时，后一种技术干扰较小且更准确，且在每小时或每两小时由 cron (8) 运行 ntpdate 时效果很好。后一种情况下的调整实际上比测量到的偏移量大 50%，因为这将倾向于使严重漂移的时钟更加准确（虽然是以牺牲一定的稳定性为代价，但这种权衡通常是有利的）。但在启动时，通常最好始终步进时间。可以通过在命令行指定 -b 开关在所有情况下强制执行此操作。-s 开关告诉 ntpdate 通过 syslog(3) 设施而非标准输出记录其操作，这是从 cron(8) 运行程序时的有用选项。

-d 标志可用于确定 ntpdate 将执行的操作，而无需实际执行。还将打印出对常规调试有用的信息。默认情况下，ntpdate 在其传出数据包中声称自己是 NTP 版本 2 实现。由于某些旧软件将拒绝响应版本 2 查询，可以使用 -o 开关强制程序作为版本 1 实现进行轮询。

ntpdate 从每个服务器获取的样本数量可以使用 -p 开关设置为 1 到 8 之间（含）。默认值为 4。等待响应的时间可以使用 -t 开关设置，并将被四舍五入到

0.2 秒的倍数。默认值为 1 秒，该值适用于局域网（LAN）内的轮询。

如果需要，Ntpdate 将对其事务进行身份验证。-a 开关指定所有数据包都应使用指示的密钥编号进行身份验证。-k 开关允许将读取密钥的文件名从默认的 `/etc/ntp.keys` 进行修改。该文件的格式应如 xntpd(8) 中所述。-e 选项允许指定身份验证处理延迟（以秒为单位，详见 xntpd(8)）。对于 ntpdate 的用途而言，这个数值通常小到可以忽略不计，不过指定该值可能会提高在极慢 CPU 上的计时精度。

如果在同一主机上运行着 NTP 服务器守护进程（例如 xntpd(8)），Ntpdate 将拒绝设置日期。如果使用 cron(8) 定期运行 ntpdate 以替代运行守护进程，每隔一两个小时运行一次即可实现足够精确的计时，从而避免时钟步进（stepping the clock）。

## 文件 (FILES)

`/etc/ntp.keys` 包含 ntpdate 使用的加密密钥。

除 xntpd 和 ntpdate 之外，其他 NTP 命令还包括：

- /usr/sbin/ntpdate
- /usr/sbin/ntpq
- /usr/sbin/ntptime
- /usr/sbin/ntptrace
- /usr/sbin/tickadj
- /usr/sbin/xntpd
- /usr/sbin/xntpdc

有关更多信息，请参阅这些 NTP 命令的 man 手册页。NTP 的主配置文件是 `/etc/ntp.conf`。以下是一个典型的 `/etc/ntp.conf` 文件的内容：

```
# Undisciplined Local Clock. This is a fake driver intended
# for backup and when no outside source of synchronized time
# is available. The default stratum is usually 3, but in
# this case we elect to use stratum 0. Since the server line
# does not have the prefer keyword, this driver is never
# used for synchronization, unless no other
# synchronization source is available. In case the local
# host is controlled by some external source, such as an
# external oscillator or another protocol, the prefer
# keyword would cause the local host to disregard all other
# synchronization sources, unless the kernel modifications
# are in use and declare an unsynchronized condition.

server 128.173.14.71 # vt.edu
server 140.247.60.28 # harvard.edu
server 165.227.1.1 # scruz.net
server 131.216.16.9 # unlv.edu
server 127.127.1.0 # local clock
fudge 127.127.1.0 stratum 10

restrict default ignore
restrict 199.184.237.129
restrict 128.173.14.71
restrict 140.247.60.28
restrict 165.227.1.1
restrict 131.216.16.9
restrict 192.168.0.0 mask 255.255.0.0
restrict 127.0.0.0 mask 255.255.0.0
```

```
# Drift file. Put this in a directory which the daemon can
# write to. No symbolic links allowed, either, since the
# daemon updates the file by creating a temporary in the
# same directory and then rename()ing it to the file.

driftfile /etc/ntp/drift
```

```
#multicastclient # listen on default
224.0.1.1
#broadcastdelay 0.008
```

```
# Authentication delay. If you use, or plan to use
# someday, the authentication facility you should make the
# programs in the auth_stuff directory and figure out what
# this number should be on your machine.

authenticate no
```

```
# Keys file. If you want to diddle your server at run
# time, make a keys file (mode 600 for sure) and define the
# key number to be used for making requests.
```

有关 NTP 的更多信息，请参阅 `/usr/doc/xntp3*` 中的文档。另请访问 NTP 网站 `www.ntp.org`。

在选择用于同步的 NTP 服务器时请谨慎。一项研究发现，大量 NTP 服务器配置不当，因此报告了错误的时间值。

## Squid 代理服务器

Squid 代理服务器是一个与 FTP、HTTP 和 SSL 兼容的缓存代理服务器。它直接处理 HTTP 和 FTP 请求，并将 SSL 请求转发到另一个服务器或代理。例如，它可以用于：

- 减少由于多次请求热门网页而产生的带宽需求。
- 通过访问控制列表 (ACLs) 控制对外部网站的访问。
- 加速 HTTP 服务器。

该代理通过缓存经由其请求的 HTTP 数据并提供缓存响应来工作，而不是重复地从远程服务器检索热门数据。它能智能地将动态内容的请求转发到远程服务器；例如，CGI（通用网关接口）页面能得到正确处理。为了加速 HTTP 服务器，代理通常运行在 80 端口（标准的 HTTP 端口）。然后，它将缓存中未找到的请求转发到运行在另一个端口或系统上的 Web 服务器。

代理实例可以参与到一个被称为 Harvest Cache 的缓存站点层级结构中。Harvest Cache 项目的初衷源于 1993 年的一项研究，该研究表明，通过布置几个位置合理的缓存，NFSNET 主干网的 FTP 流量可以减少 44%。有关 Harvest Cache 的更多信息，请参阅项目网站 `ircache.nlannr.net`。

该代理包含在软件包 `squid-2.2.STABLE4-8.1386.rpm` 中，随附一个 1900 行的默认主配置文件 `/etc/squid/squid.conf`。默认配置文件足以满足许多应用需求，因此 squid 通常在安装后即可立即使用。要启动服务，请执行以下命令：

```
/etc/rc.d/init.d/squid
```

要配置 Web 浏览器使用 `squid`，请将浏览器的代理主机设置为运行 `squid` 的系统主机名，并将代理端口设置为 `squid` 运行的端口（通常为 3128）。

有关 `squid` 的更多信息，请参阅 `/usr/doc/squid-*` 中的文档文件以及 `squid` 网站 `squid.nlannr.net` 上的信息。

## 使用加密的服务

美国限制导出加密强度超过 56 位的软件的出口法律近期有所放宽。但是，几种重要的加密算法受到专利保护。因此，Red Hat Linux 不包含一些使用强加密的热门软件。特别是 `ssh`（`telnet` 和 `rsh` 的更安全替代品）和 `scp`（`rcp` 的更安全替代品）未被包含在内。

您可以从 `www.zedz.net` 网站获取使用强加密的热门应用的 `RPM` 软件包。

从这些站点，您还可以获取 GNUPG 程序 `gnupg`，它是热门的 Pretty Good Privacy (PGP) 程序的 GNU 实现。GNUPG 特别有用，因为 Red Hat, Inc. 使用其 GNUPG 公钥对其创建的 `RPM` 软件包进行签名。因此，您可以使用 GNUPG 来验证声称由 Red Hat, Inc. 构建的 `RPM` 软件包的来源。Red Hat Linux 6.2 将 GNUPG 作为标准发行版的一部分包含在内。

Red Hat, Inc. 曾经使用 PGP 程序对 RPM 软件包进行签名。然而，现在软件包改用 GNUPG 进行签名。

要验证 RPM 软件包的来源，您必须下载 GNUPG 软件包。进入包含该软件包的目录，并执行以下命令安装软件包：

```
rpm -Uvh gnupg-*.rpm
```

然后，通过执行以下命令生成密钥对：

```
gpg --gen-key
```

随后的对话将类似于以下内容：

```
gpg (GnuPG) 1.0.1; Copyright (C) 1999 Free Software
Foundation, Inc.
This program comes with ABSOLUTELY NO WARRANTY.
This is free software, and you are welcome to redistribute
it under certain conditions. See the file COPYING for
details.

Please select what kind of key you want:
  (1) DSA and Elgamal (default)
  (2) DSA (sign only)
  (4) Elgamal (sign and encrypt)
Your selection? 1
DSA keypair will have 1024 bits.
About to generate a new ELG-E keypair.
    minimum keysize is 768 bits
    default keysize is 1024 bits
highest suggested keysize is 2048 bits
What keysize do you want? (1024) 1024
Requested keysize is 1024 bits
Please specify how long the key should be valid.
  0 = key does not expire
  <n> = key expires in n days
  <n>w = key expires in n weeks
  <n>m = key expires in n months
  <n>y = key expires in n years
Key is valid for? (0) 0
Key does not expire at all
Is this correct (y/n)? y
```

您需要一个 User-ID 来标识您的密钥；软件将根据真实姓名、注释和电子邮件地址按以下形式构建用户 ID：

```
"Heinrich Heine (Der Dichter) <heinrichh@duesseldorf.d>"
```

真实姓名：**Bill McCarty**



电子邮件地址：`bmccarty@azusapacific.com` 
注释： 
您选择了此用户 ID： 
`"Bill McCarty <Bmcarty@apu.edu>`

更改 (N)ame 姓名，(C)omment 注释，(E)mail 电子邮件 或 (O)kay 确定/(Q)uit 退出？ o
您需要一个 Passphrase（密码短语）来保护您的私钥。
`thisisatest`

我们需要生成大量随机字节。在生成质数期间，执行一些其他操作（在另一个窗口工作、移动鼠标、利用网络和磁盘）是一个好主意；这能让随机数生成器有更好的机会获得足够的熵。
`+++++ ++++++ +++++++ ++++++++++ +++++++ ++++++` 
`++++++ ++++++++ ++++++++ ++++++++ ++++++++ +++++++ +++++++` 
`++++++ +++++++ +++++++ ++++++++++ +++++++ +++++++ ++++++++` 
`++++++ +++++++ ++++++ ++++++++ +++++++ +++++++ +++++++ +++++++` 
`++++++ ++++++++ ++++++ ++++++` 

公钥和私钥已创建并签名。

您还必须下载并安装 Red Hat, Inc. 用于对 RPM 软件包签名的公钥。该密钥可在 `www.redhat.com/about/contact.html` 获取。将密钥下载到文件 `redhat2.asc` 中，然后通过执行以下命令进行安装：

```bash
gpg --import redhat2.asc
```

命令输出将类似于以下内容：

```text
gpg (GNUPG) 0.4.0; Copyright (C) 1998 Free Software
Foundation, Inc.
This program comes with ABSOLUTELY NO WARRANTY.
This is free software, and you are welcome to redistribute
it under certain conditions. See the file COPYING for details.

gpg:redhat2.asc: key DB42A60E: public key imported
```

要验证 RPM 软件包的签名，请执行以下形式的命令：

```bash
rpm -K package_file
```

例如，您可以执行以下命令来验证 basesystem 软件包的签名：

```bash
rpm -K basesystem-6.0-4.noarch.rpm
```

如果签名匹配，输出将类似于以下内容：

```text
basesystem-6.0-4.noarch.rpm: md5gpg OK
```

有关 GNUPG 的更多信息，请参阅 GNUPG 网站 www.gnupg.org。

## 总结

在本章中，您学习了辅助网络服务。涵盖的最重要主题包括：

- **动态主机配置协议 (DHCP)** DHCP 允许您配置客户端在系统启动期间获取其网络配置信息。DHCP 配置文件为 /etc/dhcpd.conf。可以将 DHCP 服务器配置为向给定主机提供固定信息，服务器通过主机的媒体访问控制 (MAC) 地址来识别该主机。或者，DHCP 服务器可以从池中提供一个可用的配置。
- **DHCP 客户端** Linux DHCP 客户端名为 pump。使用 linuxconf 或 netconf，您可以配置 Linux 系统在系统启动时通过 pump 协议获取其网络配置。
- **IPX 协议** IPX 协议是 Novell NetWare 系统的原生协议。Red Hat Linux 的 mars-nwe 软件包提供了与 Novell IPX 协议的文件和打印机共享兼容性。
- **远程打印机访问** Red Hat Linux 的远程打印机访问由 lpd 服务提供。要定义远程打印机，您可以使用 printtool 或修改 /etc/printcap 文件。要为远程主机启用打印机访问，请将该远程主机列在 /etc/hosts.lpd 或 /etc/hosts.equiv 文件中。
- **互联网新闻** 互联网新闻由 inn 软件包提供。互联网新闻相对难以配置，且需要较多的计算资源，尤其是磁盘空间。
- **时间同步** 您可以使用 rdate 或 xntp3 来同步系统时间。xntp3 设施使用网络时间协议 (NTP)，在这两个设施中更为复杂，并提供更精确的时间同步。该设施的主要配置文件是 /etc/ntp.conf。
- **squid 代理服务器** squid 代理服务器是一个与 FTP、HTTP 和 SSL 兼容的缓存代理服务器。它可以用于：
    - 减少因多次请求热门网页而产生的带宽需求
    - 通过访问控制列表 (ACLs) 控制对外部网站的访问
    - 加速 HTTP 服务器
- **加密软件** 美国法律限制导出使用强加密（即密钥长度超过 56 位的加密）的软件。几个流行的 Unix 和 Linux 程序使用了强加密，因此未包含在 Red Hat Linux 发行版中。您可以从 `www.zedz.net` 下载使用强加密的流行程序的 RPM 软件包。

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- BOOTP
- 动态主机配置协议 (DHCP)
- 网络新闻传输协议 (NNTP)
- 网络时间协议 (NTP)
- stratum (层级)

## 其他信息来源

如果您想进一步了解本章介绍的主题，应参考以下来源：

- DHCP 网页，`www.isc.org`
- Vladimir Vuksan 编写的 *DHCP Mini-HOWTO*，`/usr/doc/dhcp-*`
- `/usr/doc/dhcp-*` 中的 DHCP 文档
- `/usr/doc/mars-nwe-*` 中的 `mars_nwe` 文档
- `/usr/doc/ipxutils-*` 中的 `ipxutils` 文档
- `/usr/doc/squid-*` 中的 squid 文档文件
- GNUPG 网站，`www.gnupg.org`

## 复习题

1. 以下哪些内容可以由 DHCP 服务器提供？
    A. 主机名
    B. DNS 服务器 IP 地址
    C. IP 地址
    D. WINS 服务器 IP 地址

2. 常用于支持 NNTP 的软件包是：
    A. cleanfeed
    B. inn
    C. rdate
    D. xntp3

3. 以下哪个程序会持续同步时间？
    A. ntpdate
    B. rdate
    C. setclock
    D. xntpd

4. `squid` 通常运行在哪个端口上？
    A. 80
    B. 3128
    C. 8080
    D. 不适用：`squid` 不需要端口

5. Red Hat, Inc. 使用以下什么方式对 RPM 软件包进行签名：
    A. GNUPG
    B. MD5
    C. PGP
    D. RPMSIGN

6. 以下哪个是同步时间最准确的 stratum（层级）？
    A. Stratum 0
    B. Stratum 1
    C. Stratum 2
    D. Stratum 3

## 复习题答案

1. A, B, C, D。DHCP 服务器基本上可以提供完整网络配置的所有元素。

2. A, B。`inn` 软件包提供了 NNTP 守护进程 `innd`；`cleanfeed` 软件包提供了在运行 `innd` 时有用的垃圾邮件过滤器。

3. D。`rdate` 和 `ntpdate` 程序仅在执行时设置一次时间。

4. B。squid 代理可以运行在任何可用端口上；但默认情况下，它运行在端口 3128。

5. A。Red Hat, Inc. 以前使用 PGP 对 `RPM` 软件包进行签名，但现在使用 GNUPG。

6. B。Stratum 1 是同步层级中的最高级别；stratum 0 不存在。

# 第 24 章：管理日志

本章涵盖的 RHCE 准备主题：

- 理解并能够管理系统日志。

Red Hat Linux 将重要事件记录到磁盘文件中。作为系统管理员，您需要能够分析这些文件，这可以帮助您预测、预防或排除系统问题。您还需要能够配置系统日志记录并管理日志文件，因为随着时间的推移，尤其是当系统繁忙时，日志文件会变得很大。您应该在合理的时间段内保留系统日志文件；通常，确定某种不熟悉的日志条目是否异常的最简单方法，就是发现它已经出现了多久。

## 系统日志记录进程

Red Hat Linux 系统有两个系统日志记录进程：

- 主系统日志记录进程
- 记录内核消息的进程

以下子节描述了这些进程。

### syslogd 进程

主系统日志记录进程是 `syslogd`。`syslogd` 进程在系统启动时由初始化脚本 `/etc/rc.d/init.d/syslog` 启动。当发生重要事件且应用程序需要记录消息时，它将消息发送给 `syslogd`，由 `syslogd` 将其记录下来。通常，记录消息意味着将其写入 `/var/log/messages` 文件中。然而，`syslogd` 可以采取多种其他日志记录操作。例如，`syslogd` 可以将事件记录到 `/var/log/messages` 以外的文件中，在系统控制台上显示消息，向已登录的用户发送消息，等等。`syslogd` 配置文件为 `/etc/syslog.conf`。“配置系统日志记录”部分解释了如何配置 `syslogd` 进程。



## `klogd` 进程

另一个重要的系统日志进程还包括 `klogd`，它负责处理内核消息。`klogd` 进程通常将接收到的消息传递给 `syslogd`，由后者以常规方式进行记录。不过，通过指定适当的命令行参数，如果您愿意，也可以配置 `klogd` 将内核消息记录到指定文件中。`klogd` 进程由启动 `syslogd` 进程的同一个 `/etc/rc.d/init.d/syslog` 脚本启动。

## 系统日志文件与条目

默认情况下，大多数消息类型都被记录到系统日志文件 `/var/log/messages` 中。您可以通过执行以下形式的命令来查看系统日志文件中的最新条目：

```
tail -n [number] /var/log/messages
```

其中 `[number]` 是您想要查看的行数。系统日志通常包含多种类型的消息。以下是一些典型的条目：

```
May 10 15:09:59 www named[474]: listening on [127.0.0.1].53 (lo)
May 10 15:09:59 www named[474]: listening on [192.168.100.2].53 (eth0)
May 10 15:09:59 www named[474]: listening on [192.168.1.1].53 (eth1)
May 10 15:10:00 www named[474]: Forwarding source address is [0.0.0.0].1024
May 10 15:10:00 www named: named startup succeeded
May 10 15:10:00 www named[475]: Ready to answer queries.
May 10 15:10:00 www sshd[481]: log: Server listening on port 23.
May 10 15:10:00 www sshd[481]: log: Generating 768 bit RSA key.
May 10 15:10:01 www xntpd: xntpd startup succeeded
May 10 15:10:01 www xntpd[496]: xntpd 3-5.93e Wed Apr 14 20:23:29 EDT 1999 (1)
May 10 15:10:01 www xntpd[496]: tickadj = 5, tick = 10000, tvu_maxslew = 495, est . hz = 100
May 10 15:10:01 www xntpd[496]: precision = 13 usec
May 10 15:10:02 www xntpd[496]: read drift of -94.732 from /etc/ntp/drift
May 10 15:11:49 www dhcpd: DHCPREQUEST for 192.168.1.90 from 00:e0:98:77:08:40 via eth1
May 10 15:11:49 www dhcpd: DHCPACK on 192.168.1.90 to 00:e0:98:77:08:40 via eth1
May 10 15:17:26 www lpd[11305]: www.azusapacific.com requests printjob lp
May 10 15:17:27 www kernel: parport0: PC-style at 0x3bc [SPP,PS2]
May 10 15:17:27 www kernel: parport0: Printer, Hewlett-Packard HP LaserJet 2100 Series
May 10 15:17:27 www kernel: lp0: using parport0 (polling). (serial 2000050901)
May 11 11:34:05 sbmserver lpd[22139]: sbmserver.azusapacific.com requests printjob lp
May 11 13:15:09 sbmserver ftpd[22243]: ACCESS DENIED (not in any class) To usr57-dialup119.mix2.Atlanta.cw.net [166.62.189.121]
May 11 13:15:09 sbmserver ftpd[22243]: FTP LOGIN REFUSED (access denied) FROM usr57-dialup119.mix2.Atlanta.cw.net [166.62.189.121], anonymous
May 11 13:15:10 sbmserver ftpd[22243]: FTP session closed
May 11 23:01:56 sbmserver ftpd[21811]: FTP LOGIN FROM pool1209.dialup.earthlink.net [209.179.138.189], jczarnec
May 11 23:05:29 sbmserver ftpd[21811]: FTP session closed
```

每个条目的通用格式为：
`[date time] [hostname] [application][pid]: [message]`

其中：
- `[date time]` 是接收到消息的日期和时间
- `[hostname]` 是产生消息的主机名
- `[application]` 是发送消息的应用程序名称
- `[pid]` 是发送消息的应用程序的进程号
- `[message]` 是消息内容

一些常见的消息类型包括：
- 授权失败
- `su` 命令执行失败
- 硬件错误（如超时）
- 通过 FTP、SSH 和 TELNET 登录
- 邮件活动
- 进程和服务的启动与关闭

如果您在大型日志文件中寻找特定类型的日志消息，`grep` 命令会非常有用。请执行如下形式的命令：

```bash
grep "string" /var/log/messages | more
```

其中 `"string"` 是您感兴趣的该类型日志消息中常见的字符串。`grep` 命令将仅显示包含指定文本的日志条目。

现在，花几分钟时间完成练习 24.1，这将让您进一步熟悉系统日志。

### 练习 24.1：检查系统日志

为了获得操作系统日志的经验，请执行以下步骤：

1. 使用 `more` 命令显示系统日志文件的每一行。
2. 研究每一行以辨析其含义和重要性。
3. 通常，对系统日志的研究会揭露之前未知的、需要关注的问题。如果您发现了问题，请尝试解决它们。

您可以查阅本书或参考其他文档来获取完成此练习的帮助。但在参加 RHCE 考试之前，请确保您能够在无需此类帮助的情况下操作系统日志。

## 配置系统日志

文件 `/etc/syslog.conf` 包含系统日志配置。文件中的每个条目指定了一类日志消息以及相应的记录操作。条目的通用格式为：
`facility.priority action`

其中：
- `facility`（设施）指定产生消息的应用程序类别。您可以通过用逗号 (,) 分隔来指定多个设施。
- `priority`（优先级）指定与消息相关的优先级。
- `action`（操作）指定针对给定设施且具有给定优先级的消息所采取的操作。

表 24.1 总结了用于指代产生日志消息的设施的关键字。表 24.2 总结了用于指代消息优先级的关键字和符号。表 24.3 总结了用于指定记录操作的关键字和符号。

**表 24.1 设施及其定义**

| 设施定义 | 描述 |
| :--- | :--- |
| auth | 来自用户授权设施的消息 |
| authpriv | 来自特权用户授权设施的消息；普通用户不应看到这些消息 |
| cron | 来自 cron 设施的消息 |
| daemon | 来自守护进程和 TCP 服务的消息 |
| kern | 来自内核的消息 |
| lpr | 来自打印设施的消息 |
| mail | 来自邮件设施的消息 |
| news | 来自互联网新闻的消息 |
| syslog | 来自系统日志记录的消息 |
| user | 来自用户定义设施的消息 |
| uucp | 来自 Unix-to-Unix Copy Program (UUCP) 的消息 |
| local0-local7 | 来自本地定义设施的消息 |
| * | 来自任何设施的消息 |

**表 24.2 消息优先级定义**

| 消息优先级 | 优先级等级 | 描述 |
| :--- | :--- | :--- |
| debug | 1 | 记录 debug 消息及更高优先级的消息。 |
| info | 2 | 记录 info 消息及更高优先级的消息。 |
| notice | 3 | 记录 notice 消息及更高优先级的消息。 |
| warning | 4 | 记录 warning 消息及更高优先级的消息。 |
| err | 5 | 记录 err 消息及更高优先级的消息。 |
| crit | 6 | 记录 crit 消息及更高优先级的消息。 |
| alert | 7 | 记录 alert 消息及更高优先级的消息。 |
| emerg | 8 | 记录 emerg 消息及更高优先级的消息。 |
| * | N/A | 记录所有消息，无论优先级如何。 |
| = | N/A | 仅记录指定优先级的消息。 |
| ! | N/A | 忽略指定优先级及更高优先级的消息。 |
| != | N/A | 记录除指定优先级以外的所有消息。 |

**表 24.3 记录操作定义**

| 操作定义 | 描述 |
| :--- | :--- |
| `/path/to/file` | 将消息记录到指定文件。 |
| `/dev/console` 或 `/dev/tty` | 将消息记录到指定终端。 |
| `@hostname` | 将消息记录到远程主机。 |
| `user` | 如果该用户已登录，则将消息发送给指定用户。您可以通过用逗号分隔来指定多个用户 ID。 |
| `*` | 通过 `wall` 命令将消息发送给所有已登录用户。 |

以下是一个典型的 `/etc/syslog.conf` 文件的内容：

```
# Log all kernel messages to the console.
# Logging much else clutters up the screen.
kern.* /dev/console

# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;authpriv.none /var/log/messages
```



```
# The authpriv file has restricted access.
authpriv.*
    /var/log/secure

# authpriv 文件的访问权限受限。

# Log all the mail messages in one place.
mail.*
    /var/log/maillog# 将所有邮件消息记录在同一个地方。

# Everybody gets emergency messages
*.emerg *# 所有人都会收到紧急消息

# Save mail and news errors of level err and higher in a
# special file.
uucp,news.crit
    /var/log/spooler# 将级别为 err 及以上的邮件和新闻错误保存到
# 一个特殊文件中。
```

请注意，`authpriv` 消息被发送到 `/var/log/secure`，该文件仅由 `root` 可读。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_608_0.png)

Linux 远程日志记录对于备份日志和集中化日志文件以方便分析非常有用。然而，远程日志记录在某种程度上存在一些 Bug。

为了对系统日志记录进行一些实验，请完成练习 24.2。

### 练习 24.2：配置系统日志记录

为了进一步了解系统日志记录，请临时重新配置授权消息 (auth) 的日志记录，以观察某些不寻常的日志记录方法产生的影响。将系统设置为运行级别 3，并执行以下操作：

- 1. 配置系统日志记录，将授权消息发送到文件 `/var/log/auth.log`。验证配置是否生效。
- 2. 配置系统日志记录，将授权消息发送到系统控制台。验证配置是否生效。
- 3. 配置系统日志记录，将授权消息发送给 root 用户。验证配置是否生效。为了接收这些消息，你需要以 root 身份登录，而不仅仅是通过执行 `su` 命令来获取 root 权限。
- 4. 配置系统日志记录，将授权消息发送给所有用户。验证配置是否生效。
- 5. 恢复原始的系统日志记录配置。

在完成此练习时，你可以参考外部帮助。但在参加 RHCE 考试之前，请确保你在不需要查阅书籍、笔记或其他帮助的情况下能够执行此类操作。

## 启动日志

Linux 内核启动时，会在系统控制台上显示启动消息。这些消息存储在内核环形缓冲区 (kernel ring buffer) 中，当缓冲区满时会被覆盖。你可以通过执行以下命令来查看内核环形缓冲区：

```
dmesg
```

为了防止丢失潜在的重要启动消息，初始化脚本会将内核环形缓冲区的内容保存到启动消息文件 `/var/log/dmesg` 中，可以通过执行以下命令查看：

```
more /var/log/dmesg
```

以下是该命令的典型输出：

```
Linux version 2.2.5-15 (root@porky.devel.redhat.com) (gcc
  version
  egcs-2.91.66 19990314/Linux (egcs-1.1.2 release)) #1
  Mon Apr 19 23:00:46 EDT 1999
Detected 548955270 Hz processor.
Console: colour VGA+ 80x25
Calibrating delay loop... 547.23 BogoMIPS
Memory: 64152k/66565k available (996k kernel code, 412k
  reserved, 936k data, 60k init)
VFS: Diskquotas version dquot_6.4.0 initialized
CPU: AMD AMD-K7(tm) Processor stepping 02
Checking 386/387 coupling... OK, FPU using exception 16 error reporting.
Checking 'hlt' instruction... OK.
POSIX conformance testing by UNIX
mtrr: v1.26 (19981001) Richard Gooch (rgooch@atnf.csiro.au)
PCI: PCI BIOS revision 2.10 entry at 0xfdb01
PCI: Using configuration type 1
PCI: Probing PCI hardware
PCI: Enabling I/O for device 00:00
Linux NET4.0 for Linux 2.2
Based upon Swansea University Computer Society NET3.039
NET4: Unix domain sockets 1.0 for Linux NET4.0.
NET4: Linux TCP/IP 1.0 for NET4.0
IP Protocols: ICMP, UDP, TCP, IGMP
Initializing RT netlink socket
Starting kswapd v 1.5
Detected PS/2 Mouse Port.
Serial driver version 4.27 with MANY_PORTS MULTIPORT SHARE_IRQ enabled
ttyS00 at 0x03f8 (irq = 4) is a 16550A
pty: 256 Unix98 ptys configured
apm: BIOS version 1.2 Flags 0x03 (Driver version 1.9)
Real Time Clock Driver v1.09
RAM disk driver initialized: 16 RAM disks of 4096K size
VP_IDE: IDE controller on PCI bus 00 dev 39
VP_IDE: not 100% native mode: will probe irqs later
ide0: BM-DMA at 0xffa0-0xffa7, BIOS settings: hda:DMA, hdb:pio
ide1: BM-DMA at 0xffa8-0xffaf, BIOS settings: hdc:pio, hdd:DMA
hda: Maxtor 92048DB, ATA DISK drive
hdd: CD-ROM Drive/FSB, ATAPI CDROM drive
ide0 at 0x1f0-0x1f7, 0x3f6 on irq 14
ide1 at 0x170-0x177, 0x376 on irq 15
hda: Maxtor 9204, 19531MB w/1024Kb Cache, CHS=2489/255/63
hdd: ATAPI 48X CD-ROM drive, 128Kb Cache
Uniform CDROM driver Revision: 2.54
Floppy drive(s): fd0 is 1.44M
FDC 0 is a post-1991 82077
md driver 0.90.0 MAX_MD_DEVS=256, MAX_REAL=12
raid5: measuring checksumming speed
raid5: using high-speed MMX checksum routine
  pII_mmx     : 1444.752 MB/sec
  p5_mmx      : 1559.052 MB/sec
  8regs       : 734.949 MB/sec
  32regs      : 639.318 MB/sec
  using fastest function: p5_mmx (1559.052 MB/sec)
scsi : 0 hosts.
scsi : detected total.
md.c: sizeeof(mdp_super_t) = 4096
Partition check:
hda: hda1 hda2 < hda5 hda6 hda7 hda8 hda9 hda10 hda11 >
autodetecting RAID arrays
autorun ...
... autorun DONE.
VFS: Mounted root (ext2 filesystem) readonly.
Freeing unused kernel memory: 60k freed
Adding Swap: 538140k swap-space (priority -1)
Creative SBLive! detected
```

系统启动日志在排除与设备驱动程序相关的问题时特别有用。如果硬件设备无法正常工作，请检查系统启动日志，查看驱动程序是否加载并初始化且没有错误。

## 日志轮转

如果系统很繁忙，其日志文件可能会迅速增长，导致处理起来非常繁琐。为了控制系统日志的大小，cron 设施运行一个每日任务来轮转日志文件，路径为 `/etc/cron.daily/logrotate`。在 Red Hat Linux 中分发的 logrotate 脚本内容如下：

```
#!/bin/sh
/usr/sbin/logrotate /etc/logrotate.conf
```

`logrotate` 命令可以用多种方式操作日志文件。例如，它可以执行以下任务：

- 轮转日志文件
- 压缩日志文件以最小化磁盘空间占用
- 将日志文件发送给指定用户

轮转日志文件涉及建立一系列日志文件。当当前日志文件达到指定的时长时，它会被重命名而不是被删除。这样，当前日志文件始终保持在可管理的大小。通过使用日志轮转，可以保留几代日志文件以便方便访问。`logrotate` 的配置文件是 `/etc/logrotate.conf`。默认情况下，日志每周轮转一次，除了当前日志外，还保留四周的日志。以下是一个典型的 `/etc/logrotate.conf` 文件的内容：

```
# 详情请参阅 "man logrotate"
# 每周轮转一次日志文件
weekly

# 保留 4 周的备份日志
rotate 4

# 将错误发送给 root
errors root

# 轮转旧文件后创建新（空）日志文件
create

# 如果你想压缩日志文件，请取消此行的注释
#compress

# RPM 软件包将日志轮转信息放入此目录
include /etc/logrotate.d

# 没有软件包拥有 lastlog 或 wtmp -- 我们在这里轮转它们
/var/log/wtmp {
    monthly
    create 0664 root utmp
    rotate 1
}

/var/log/lastlog {
    monthly
    rotate 1
}

# 特定于系统的日志可以在这里配置
```

Red Hat Linux 还使用 `logrotate` 工具来维护系统日志以外的日志。相关配置文件位于 `/etc/logrotate.d`；该目录的名称在 `/etc/logrotate.conf` 文件中指定。

现在完成练习 24.3，该练习要求你尝试一些实际的日志轮转方案。

### 练习 24.3：配置 logrotate

很少需要调整 Red Hat Linux 使用的默认日志轮转方案。但是，除非你了解其细节，否则你不会知道该方案是否需要调整。为了熟悉它，请检查安装在系统上的以下每个应用程序的 logrotate 配置：apache、FTP、samba、squid、sudo 和 syslog。

## swatch 工具

当系统繁忙时，日志文件会迅速变大，因此手动检查会非常耗时。`swatch` 工具（作为 Red Hat PowerTools 集合的一部分分发）可以监控日志文件，并在记录特定类型的事件消息时采取指定操作。例如，`swatch` 可以发送电子邮件消息、呼叫寻呼机等等。

另一个类似的工具 `logwatch` 同样作为 Red Hat PowerTools 集合的一部分分发。`logwatch` 工具可以处理 Samba 日志以及系统日志。



## 总结

在本章中，您学习了系统日志记录。涵盖的最重要主题包括：

**系统日志进程** 系统日志进程包括内核日志进程 `klogd` 和系统日志进程 `syslogd`。默认情况下，`klogd` 使用 `syslogd` 来处理其日志请求。系统日志配置文件是 `/etc/syslog.conf`。

**系统日志文件** 系统日志进程将大多数日志条目发送到 `/var/log/messages`。包含可能危及用户帐户或系统安全信息的日志消息被发送到 `/var/log/secure`，该文件仅 root 用户可读。可以使用常见的 Linux 命令（如 `tail`）查看日志文件。启动消息记录在 `/var/log/dmesg` 中。

**日志条目内容** 一个日志条目包含以下信息：

- 接收消息的日期和时间
- 发送消息的主机名称
- 发送消息的应用程序名称
- 发送消息的应用程序的进程号
- 消息内容

**日志条目类型** 常见的日志条目类型包括以下内容：

- 授权失败
- `su` 命令失败
- 硬件错误，例如超时
- 通过 FTP、SSH 和 TELNET 登录
- 邮件活动
- 进程和服务的启动与关闭

**日志轮转** 日志轮转（Log rotation）控制日志文件所消耗的磁盘空间量。`logrotate` 工具的配置存储在 `/etc/logrotate.conf` 中，它决定了日志文件的保留时间以及当日志文件达到指定年龄或大小时采取的操作。

**实用工具** `swatch` 工具可以帮助您自动定期审查和分析系统日志。

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- 日志轮转 (log rotation)

## 补充信息源

如果您想进一步了解本章中介绍的主题，应参考以下资源：

- `syslog.conf`、`klogd`、`sysklogd`、`syslogd` 和 `logrotate` 的 man 手册页
- `/usr/doc/sysklogd*` 中的文档文件

## 复习题

1. 以下哪个是主要的系统日志进程？
   A. klogd
   B. linuxlog
   C. syslog
   D. syslogd

2. 以下哪个是系统日志的主要配置文件？
   A. /etc/klog.conf
   B. /etc/klogd.conf
   C. /etc/syslog.conf
   D. /etc/syslogd.conf

3. 用于查看内核环形缓冲区的命令是以下哪个？
   A. bootmesg
   B. dmesg
   C. logmesg
   D. sysboot

4. 以下哪个操作内置在 `logrotate` 命令中？
   A. 压缩
   B. 删除
   C. 轮转
   D. 通过邮件发送

5. 以下哪个是分析日志文件的有用工具？
   A. logman
   B. logrotate
   C. logwatch
   D. swatch

6. 默认情况下，Red Hat Linux 保留系统日志多长时间？
   A. 1 天
   B. 1 周
   C. 4 周
   D. 16 周

## 复习题答案

1. D. 主要的系统日志进程是 `syslogd`；`klogd` 进程记录内核消息，通常是通过将它们传递给 `syslogd` 来实现的。

2. C. `/etc/syslog.conf` 文件是 `syslogd` 进程的配置文件。

3. B. `dmesg` 命令显示内核环形缓冲区的内容。

4. A, B, C, D. 在轮转期间，最旧的日志文件会被删除。

5. C, D. `swatch` 和 `logwatch` 工具作为 Red Hat PowerTools 集合的一部分分发。`logman` 和 `logrotate` 都不分析日志文件。

6. C. `logrotate` 程序每周轮转一次日志文件，除了当前的日志文件外，还保留四个世代的日志文件。

# 第 25 章：安全管理

**本章涵盖的 RHCE 备考主题：**

- 理解基本的安全问题，并能够保护系统免受常见的安全威胁。

一台保存在锁在办公室中且只有用户持有钥匙的独立计算机对安全威胁具有很强的抵御能力。然而，很少有用户愿意为了提高安全性而放弃网络访问。作为系统管理员，您可能同时负责工作站和服务器，而这些设备就其本质而言必须连接到网络。保护联网的多用户系统需要技巧和勤勉。本章解释了计算机安全的基础知识，并就如何避免常见安全威胁以及从中恢复提供了指导。

## 安全基础

计算机安全的挑战在于，系统的安全性仅取决于其最薄弱的点。因此，警觉至关重要；如果后门敞开，那么前门加了两把锁并锁上链条也无关紧要。然而，警觉必须与洞察力和技巧相结合。即使是一个警觉的系统管理员也必须具备能够正确引导警觉的洞察力，因为方向错误的警觉毫无意义。同样，警觉的系统管理员必须具备在面对潜在和真实威胁时采取适当行动的技能，因为面对危险不采取行动会导致灾难。

计算机安全可以从许多角度来看待。一个有用的视角是关注哪些内容处于风险之中。安全漏洞可能导致以下内容的丢失：

- 有形财产，如计算机设备
- 信息
- 服务，例如无法访问邮件服务器

保护有形财产比保护信息或服务更让人熟悉，因为我们大多数人都有房子和汽车，并且理解如何使用锁和钥匙来保护它们。保护有形财产是保护信息和服务的先决条件：如果入侵者能够访问系统的控制台，那么入侵者很可能会设法将系统引导至单用户模式并获得特权访问权限。

另一种看待安全的方式是考虑意图问题。安全漏洞可能是无意的，也可能是蓄意的。以 root 身份登录时，无意的安全漏洞尤为严重。很容易因为输错命令而丢失数据。例如，假设您想删除名称以 a 开头的文件。您打算输入 `rm a*`，但结果输入了 `rm a *`。a 和星号之间的空格导致命令删除了所有文件，而不仅仅是名称以 a 开头的文件。

蓄意的安全漏洞来自两个来源：授权用户和非授权用户。通常，人们投入大量精力防止非授权的系统访问；但安全漏洞被信任的授权用户突破，甚至比被未知的黑客突破更容易。有效的安全性必须限制即使是授权用户执行可能危及信息或服务的操作。

Linux 系统的安全堡垒是受密码保护的用户账户系统，以及相关的限制用户访问已分配权限的文件和目录的能力。如果密码或用户账户被泄露，安全性很快就会被突破。然而，完美的安全性是一个幻想：经验表明，无论投入多少精力和资金，都无法保证系统的绝对安全。系统管理员不应追求完美，而应追求有效性。一个有效的安全策略会给潜在的入侵者带来超过其通过突破安全所能获得收益的成本。在某个时间点，理性的入侵者会认定破解一个安全系统所需付出的努力超过其价值，从而寻求一个更脆弱的目标。然而，一些潜在的入侵者并非出于经济动机；例如，他们可能将破解视为一种消磨时间的有趣方式。排除此类入侵者需要比排除经济动机黑客更复杂的安全策略。



一个良好的安全策略必须在安全机制的成本与这些机制所提供的收益之间取得平衡，因为安全机制通常会在一定程度上给用户带来不便。

本章的接下来的章节将更详细地讨论系统和网络安全，重点在于防止安全漏洞。本章的最后一节将侧重于检测安全漏洞及从中恢复。虽然物理安全是计算机安全的基础，但本章不涉及此内容；RHCE 考试不会测试您关于物理安全的知识。

## 系统安全

系统安全始于使用已知真实的发行版介质安装系统。谨慎的系统管理员会对网络安装保持警惕，因为网络安装会给潜在的入侵者提供引入恶意软件的机会。谨慎的 Red Hat Linux 系统管理员会监控 Red Hat Linux 邮件列表以及其他传输安全修复信息的列表，并及时安装相应的修复程序以关闭公开已知的漏洞。他们对于安装从不可信站点下载的软件也十分谨慎。此类软件可能包含漏洞甚至恶意代码，从而导致安全漏洞。

### root 账户

如果管理和使用不当，该账户可能会为入侵者提供破坏您安全的手段。为了避免安全漏洞，您应仅在必要时使用该账户。例如，不要长时间打开一个以 root 身份登录的终端窗口。同样，在以 root 身份登录时，请留意当前终端窗口是 root 会话还是非 root 会话，并尽可能使用与非 root 会话关联的窗口。默认情况下，root 用户接收特殊的命令行提示符 `#`，而非 root 用户接收的命令行提示符为 `$`。

以 root 身份执行命令时要非常小心。正如前面所示，误输入一个命令并导致非预期的后果实在是太容易了。

通常，最好只有一名用户知道并使用系统的 root 账户。同样，通常最好不要使用像 `su` 这样允许非 root 用户临时获得访问权限的程序。通过限制对 root 账户的访问，您可以确保拥有该账户访问权限的人员了解当前的系统配置，并能够评估拟议的配置更改对系统安全可能产生的影响。

良好的实践包括在 root 用户的 `PATH` 中仅指定标准系统目录，如 `/bin`、`/sbin`、`/usr/bin` 和 `/usr/sbin`。特别是，当前目录和主目录不应包含在 `PATH` 中。在 `PATH` 中省略这些目录有助于避免无意中执行由入侵者植入的恶意代码。同样，非 root 用户的默认 `PATH` 应当省略当前目录和主目录，或者将它们置于 `PATH` 的末尾，这样例如 `ls` 将指向 `/bin/ls`，而不是入侵者植入用户主目录中的特洛伊木马。

### 用户账户与密码

在安装新系统时，您应该启用 shadow 密码机制，这可以防止普通用户读取与用户账户关联的加密密码。否则，潜在的入侵者可以使用类似 `crack` 的程序来破解密码。

默认情况下，可插拔认证模块（PAM）被配置为强制执行相关规则，以防止用户选择过于容易被猜测或破解的密码。通常，您不应放宽或禁用此机制；相反，您应该考虑对密码施加进一步的限制。请参阅文件中关于 PAM 模块的信息。

您还应定期清除不再使用的用户账户，因为这些账户可能会提供破坏安全的漏洞。此类账户主目录的内容应当被擦除或在存档后擦除，因为它们可能包含恶意代码、文件或全球可写的目录。

### setuid 和 setgid 文件与目录

文件可以被设置为 setuid 或 setgid。当用户执行一个 setuid 文件时，该程序将以文件所有者的有效用户 ID 运行，而非执行该用户的 ID。同样，当用户执行一个 setgid 文件时，该程序将以文件组所有者的有效组 ID 运行，而非执行该用户的 ID。

要启用 setuid 或 setgid，请执行如下形式的 `chmod` 或 `chown` 命令：

```
chmod u+s files
chmod g+s files
```

要禁用 setuid 或 setgid，请执行如下形式的命令：

```
chmod u-s files
chmod g-s files
```

目录也可以这样处理。为目录启用或禁用 setgid 的命令与为文件启用或禁用 setgid 的命令相同。当用户在非受限目录中创建文件时，文件的组所有权被设置为该用户的组 ID。然而，当用户在受限目录中创建文件时，文件的组所有权被设置为该目录的组所有者。

Red Hat Linux 利用这一特性来方便文件和目录的共享。与大多数其他类 UNIX 操作系统不同，Red Hat Linux 将每个用户分配到一个与用户账户同名的 *用户私有组（user private group）*；顾名思义，该用户是其私有组的唯一成员。此外，Red Hat Linux 分发的默认 umask 脚本为普通用户分配的默认 GID 为 002，而非更常见的 022。002 的 GID 值会产生 775 的默认权限，这意味着拥有该文件的组成员不仅可以读取和执行，还可以写入新创建的文件。然而，由于用户是其私有组的唯一成员，写权限并不会被不合理地扩大。

当用户必须共享文件或目录的写访问权限时，用户私有组和不寻常的 GID 值的作用就显现出来了。以下是实现共享的步骤：

- 1. 创建一个代表需要共享写权限的部门、项目或组织的组。
- 2. 将每个相关用户放入该组中。
- 3. 创建一个目录用于存放共享文件和目录。
- 4. 将该目录的组所有权设置为步骤 1 中创建的组。
- 5. 为该目录启用 setgid。

当该组成员在目录中创建文件时，新文件的组所有者将被设置为该目录的组所有者。并且，由于用户的 umask 值为 002，文件权限被设置为 775。因此，该组成员可以读取、写入和执行该文件。然而，非组成员只能读取和执行该文件。当然，用户可以执行 `chmod` 命令来根据需要限制或放宽访问权限；特别是，用户可以将文件权限更改为禁止非组成员访问。

现在，请通过完成练习 25.1 来实际创建一个共享目录。

#### 练习 25.1：建立共享目录

Red Hat 的共享目录惯例是 Red Hat 社区的一大骄傲。因此，在参加 RHCE 考试之前，您应该熟悉这一惯例。为了获得共享目录的实际操作经验，请执行以下步骤：

- 1. 为包含用户 "alice" 和 "bob" 的 "staff" 组创建一个共享目录。
- 2. 验证组成员可以写入共享文件，而其他用户则不能。

在进行此练习时，请回顾本书并在需要时参考其他帮助。但在参加 RHCE 考试之前，请确保您能够在不依赖任何帮助的情况下执行此类操作。

### 为服务选择用户 ID

作为一项原则，守护进程（daemon processes）应该使用普通用户账户或特殊的 `nobody` 用户账户运行。它们通常不应以 root 身份运行，因为进程中的漏洞可能会为潜在的入侵者提供以 root 身份执行命令的手段。如果进程以普通用户身份运行，入侵者可能会攻破该用户账户。然而，如果进程以 root 身份运行，入侵者可能会攻破 root 账户，从而危及整个系统。

`/etc/passwd` 文件包含几个创建好的用户账户，用于避免使用 root 账户运行进程。以下是一个典型的 `/etc/passwd` 文件的内容：

```
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/sbin/nologin
```



特别是，`account` 没有关联的家目录或 shell，因此无法登录系统。例如，`process` 使用 `account` 运行。一个攻破该账户的入侵者可能会造成显著损害（例如通过杀死进程），但其造成的损害远低于通过攻破一个具有完整权限的 `account` 所能造成的损害。

## 网络安全

如果计算机系统连接到网络，除了前一节所述的措施外，您还应考虑以下额外的安全措施。

首先，您不应运行 `telnet`、`rlogin` 或 `rsh servers`；相反，您应该安装 `ssh server`。与 `telnet`、`rlogin`、`rsh` 和 `rcp servers` 不同，后者在网络上传输密码时使用的是明文。除非您使用 `ssh`，否则运行数据包嗅探器的人可以轻松获取重要的系统密码，并利用它们攻破您的系统。出于同样的原因，除非必要，否则您不应安装 `ftp server`，尤其是匿名 `ftp server`。如果您需要 `ftp` 提供的功能，但不需要 `ftp` 本身，您可以使用基于 `ssh` 的 `sftp`。

您应该从 `/etc/xinetd.conf` 中删除不需要的服务，并配置 TCP wrappers 以保护保留在 `/etc/xinetd.conf` 中的服务。通过从 `/etc/xinetd.conf` 中删除不需要的服务，您可以消除这些服务被利用来攻破系统的可能性。通常，删除 `finger`、`rwho` 和 `talk` 也是个好主意，因为它们可能会为潜在的入侵者提供关于您系统的有用信息。另一方面，您应该运行 `tcpd`，它可以地通过确认请求 TCP 服务的用户账户身份来帮助追踪入侵者。

最后，您应该从网络中删除任何能够识别您系统硬件和软件配置的信息。潜在的入侵者可能会利用这些信息来确定可能存在的漏洞。第 30 章“使用 iptables 配置防火墙”解释了为什么要构建防火墙以及如何构建防火墙，以帮助您的系统防御来自网络的攻击。

## 检测与修复

预防安全漏洞比应对安全漏洞要好。但并非所有漏洞都能被预防。因此，了解如何检测漏洞并从中恢复至关重要。

### 检测漏洞

检测真实或尝试性漏洞的一种好方法是定期审查系统日志。异常的日志条目或记录信息的缺失可能指向漏洞。但请记住，聪明的入侵者可能会篡改系统日志，擦除漏洞证据。

Red Hat Linux 的 RPM 设施可以帮助您检测漏洞。您可以使用它来验证 RPM 软件包所拥有文件的文件大小、修改日期、权限和 MD5 校验和。然而，为了使这种方法有效，您必须保护 RPM 数据库 `/var/lib/rpm` 免受篡改。除非数据库很小，否则它无法放入标准软盘中。不过，您可以将 RPM 数据库中的文件复制到离线介质中（如 ZIP 磁盘）。将文件复制到本地网络上的另一个主机通常更方便；但如果该主机被攻破，入侵者仍可能篡改 RPM 数据库。因此，最好保留一份数据库的离线副本。

有几种应用程序提供了更先进的设施来检测实际和潜在的安全漏洞，其中包括：

- AIDE ("Advanced Intrusion Detection Environment")，基于 GNU 通用公共许可证
- COPS ("Change Detection System")，免费且开源
- Gog&Magog，免费且开源
- Tripwire，是一款商业授权产品，但在某些情况下可以免费使用

这些应用程序检测文件更改的方式与 RPM 设施非常相似，但它们还可以监控不属于 RPM 软件包的文件。COPS 应用程序还会检查系统配置中可能导致安全漏洞的常见错误和遗漏。强烈建议使用此类应用程序。

### 从漏洞中恢复

从漏洞中恢复最安全的方法是还原在漏洞发生之前的备份。然而，如果原始漏洞未被发现并修复，系统可能会很快再次被攻破。此外，很难可靠地确定某个备份不包含已被攻破后的镜像；更糟糕的是，还原备份会导致备份之后添加或更改的数据丢失。

因此，从漏洞中恢复通常涉及“原位恢复”，即尝试寻找并修复原始漏洞以及入侵者留下的任何特洛伊木马、后门或其他恶意代码。以下是一些需要记住的注意事项：

- 您应该将受损主机从网络中移除；否则，入侵者可能会挫败您的恢复工作。
- 您应该考虑入侵者可能已经攻破了网络上其他主机的安全性。
- 您应该保留日志文件和其他证据的副本，这些证据可能有助于识别入侵者或确定漏洞范围。
- 您应该确定被用来攻破系统的手段，以便确定损坏范围并消除漏洞。
- 您应该从可信介质重新安装操作系统。
- 您应该检查每一个由 root 拥有的文件，尤其是可执行文件。确保这些文件没有被篡改；如果您不确定，请删除并替换该文件。
- 您应该通知黑客在攻破您的系统时可能使用过的其他主机的管理员。您还应该联系您或您的组织所属的安全组织。

## 总结

在本章中，您学习了系统和网络安全。涵盖的最重要主题包括：

**安全漏洞** 安全漏洞可由授权用户或未经授权用户造成。漏洞可能是蓄意的或无意的，并可能导致以下损失：
- 有形财产
- 信息
- 服务

**系统安全** 系统安全依赖于良好的密码安全、root 账户的正确使用、对 `su` 和二进制文件的受控使用，以及为服务选择合适的用户 ID。

**网络安全** 网络安全依赖于消除不需要的服务、避免使用不安全的服务端，以及使用配置正确的防火墙。

**检测与修复** 没有任何安全策略能预防所有漏洞。因此，拥有检测安全漏洞的机制和从漏洞中恢复的设施至关重要。

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- security policy (安全策略)
- user private group (用户私有组)

## 附加信息来源

如果您想进一步了解本章介绍的主题，请参考以下资源：

- *The Linux Security HOWTO*, 作者 Kevin Fenzi 和 Dave Wreski
- *The Linux Administrator's Security Guide*, 作者 Kurt Seifried
- The Root Shell 网站，提供有关安全漏洞和漏洞利用的新闻与信息

## 复习题

1. 系统和网络应该防范哪些类型的安全漏洞？
   A. 授权用户造成的漏洞
   B. 未经授权用户造成的漏洞
   C. 蓄意漏洞
   D. 无意漏洞

2. 关于安全策略，以下哪项是正确的？
   A. 完美的安全性至关重要。
   B. 完美的安全性是不可能的。
   C. 安全性是以牺牲便利性为代价的。
   D. 安全性应该是有效的。

3. 关于 root 账户，以下哪项是正确的？
   A. 应该始终有一个可用的终端窗口登录到该账户。
   B. 通常，只能有一个用户拥有该账户的访问权限。
   C. 像 `su` 这样的程序能提高系统安全性。
   D. 该账户与特殊的提示符符号 # 相关联。

4. 关于密码安全，以下哪项是正确的？
   A. 您应该禁用 PAM。
   B. 您应该启用 shadow 密码。
   C. 在清除关联账户后，您应该保留未使用的用户目录。
   D. 您应该定期清除未使用的用户账户。



5. 当加载一个 ________ 可执行文件时，进程的有效用户 ID 是以下哪项？

- **A.** 拥有该可执行文件的组的组 ID
- **B.** ________
- **C.** 拥有该可执行文件的用户的用户 ID
- **D.** 运行该程序的用户的用户 ID

6. 以下哪个 TCP 服务通常不应使用？

- **A.** ________
- **B.** ________
- **C.** ________
- **D.** ________

## 复习题答案

1. A, B, C, D。安全策略应尝试防御全范围的威胁。

2. B, C, D。没有任何安全策略能排除每一个潜在威胁。安全会消耗资源，因此安全性考量必须与便利性等其他考量之间取得平衡。

3. B。理想情况下，该账户应仅在必要时使用，且仅由一名用户使用。该账户与特殊的提示符符号相关联。

4. B, D。你应该考虑使用 PAM 来增强密码安全性。你应该启用影子密码（shadow passwords）和 MD5 加密。你应该定期清理未使用的用户账户以及相关的文件和目录。

5. C。该权限导致进程使用文件所有者的用户 ID 运行，该所有者可能是原用户或另一个用户。

6. A, B, C, D。你通常应该改为使用 instead。

# 第五部分：X 窗口系统管理

# 第 26 章：安装与配置 X

**本章涵盖的 RHCE 准备主题：**

- 总体理解 X，特别是 XFree86 X 服务器。
- 能够安装和配置 X。

X 窗口系统（或简称 X）是随 Red Hat Linux 分发的图形用户界面。X 有多种实现方式；随 Red Hat Linux 分发的实现是由 XFree86 Project, Inc. 制作的。他们的 X 实现被称为 XFree86，是可以自由重新分发的。本章将讲解 X 的基本运行、安装和配置。接下来的两章将讲解如何配置和使用更高级的 X 功能，包括窗口管理器、桌面管理器以及远程 X 客户端。

## X 基本概念

X 包括 X 服务器和 X 客户端；然而，在 X 的语境下，这些术语具有特殊的含义。*X 服务器（X server）* 是针对一组特定视频设备的视频驱动程序。*X 客户端（X client）* 是一个使用 X 服务器提供的图形用户界面运行的程序或应用程序。X 服务器提供的服务是视频输出。

X 服务器和客户端通过名为 X 协议的适当协议进行通信。X 是一个分布式的客户端/服务器系统：X 客户端不需要与相关的 X 服务器运行在同一台主机上。例如，一个 X 服务器可以托管运行在多个主机上的 X 客户端。同样，一台主机可以运行与多个远程主机上的 X 服务器相关联的 X 客户端。

除了服务器和客户端，X 还具有窗口管理器。*窗口管理器（window manager）* 与 X 服务器协作，为所有使用该服务器的客户端提供标准化的图形外观和界面行为。例如，窗口管理器绘制窗口标题栏，并在用户点击窗口关闭按钮时提供适当的响应。窗口管理器还提供移动、调整大小、图标化和置顶窗口的方法。

X 还具有桌面管理器。*桌面管理器（desktop manager）* 与窗口管理器协作，提供大多数用户需要的一组基本功能和特性。例如，典型的桌面管理器提供桌面图标、文件管理器、任务栏等。最常用的 Linux 桌面管理器是 KDE 和 GNOME。

X 本身没有实际用途；启动 X 通常意味着启动一个窗口管理器和一个或多个客户端。如果你在没有窗口管理器或客户端的情况下启动 X，你看到的将是一个没有任何特征的屏幕。

## 安装 X

要安装 X，必须安装一组包含以下内容的软件包：

- 一个合适的 X 服务器
- 字体服务器和一套合适的字体
- 通用 X 代码
- 一个 X 配置工具
- 库文件
- `xinitrc` 脚本

此外，你通常会选择安装：

- 一个窗口管理器
- 一个桌面管理器
- 一个或多个 X 客户端

安装 X 最简单的方法是在系统安装期间安装。这允许你指定想要安装的 X 组件，而不是单个软件包。指定组件比指定单个软件包更方便且更准确。

如果你愿意，也可以在系统安装完成后安装 X。然而，如果没有帮助，你可能会发现识别和安装正确的软件包有些繁琐。在系统安装后安装 X 是一个分两步走的过程：

1. 确定合适的 X 服务器。
2. 安装正确的软件包。

接下来的两个小节将描述系统安装后安装 X 的步骤。

要确定给定的安装组件中包含哪些软件包，请查阅 Red Hat Linux 发行版 CD-ROM 上的 `RedHat/base/comps` 文件。

### X 服务器选择

如果你愿意，可以安装发行介质上可用的所有 X 服务器，尽管系统只需要一个。XFree86 仅包含 15 个服务器，且每个相关的 RPM 文件大小仅约 1MB，因此安装不需要的服务器不会浪费大量磁盘空间。无论安装多少个服务器，你必须确定哪个服务器适用于你系统的视频设备。

确定正确的 X 服务器有时很麻烦，因为可能根本没有合适的服务器。虽然 XFree86 定期更新，但它经常缺乏对最新视频硬件的支持。不过，一些视频硬件供应商已开始为其产品分发与 XFree86 兼容的 X 服务器。

有关与 Red Hat Linux 兼容的视频设备列表，请参阅 `www.redhat.com/corp/support/hardware/index.html`。有关 XFree86 支持的视频设备列表，请参阅 `xfree86.org/cardlist.html` 上的 XFree86 显卡和 X 服务器列表。目前支持 500 多个视频设备。此外，许多未被 XFree86 完全支持的视频设备可以通过使用合适的 XFree86 服务器在 SVGA、VGA 或单色模式下运行。当然，如果这样做，最佳的视频分辨率和色彩深度可能会低于设备的完整能力。

表 26.1 总结了目前作为 XFree86 一部分分发的 X 服务器。请查阅该表以确定支持你的视频设备的服务器。

#### 表 26.1 X 服务器

| X 服务器 RPM 软件包名称 | 描述 |
| :--- | :--- |
| XFree86-3d1abs | 适用于围绕 3DIabs GLINT 和 PERMEDIA 芯片组构建的设备的服务器，包括带有 IBM RGB526 RAMDAC 的 GLINT 500TX，带有 IBM RGB526 或 IBM RGB640 RAMDAC 的 GLINT MX，带有 IBM RGB526 RAMDAC 的 PERMEDIA，以及 PERMEDIA 2a, 2v, 2 和 2 Classic。 |
| XFree86-8514 | 适用于 IBM 8514 显卡及其兼容产品（如 ATI 制造的显卡）的服务器。 |
| XFree86-AGX | 适用于 AGX 显卡的服务器。 |
| XFree86-FBDev | 适用于通用帧缓冲区（frame buffer）设备的服务器。 |
| XFree86-I128 | 适用于 Number Nine Imagine 128 等设备的服务器。 |
| XFree86-Mach32 | 适用于围绕 Mach32 芯片构建的设备的服务器。 |
| XFree86-Mach64 | 适用于围绕 Mach64 芯片构建的设备的服务器。 |
| XFree86-Mach8 | 适用于围绕 Mach8 芯片构建的设备的服务器。 |
| XFree86-Mono | 通用单色服务器，几乎适用于所有 VGA 设备。 |
| XFree86-P9000 | 适用于围绕 Weitek P9000 芯片构建的设备的服务器。 |
| XFree86-S3 | 适用于围绕 S3 芯片构建的设备的服务器，包括大多数 Number Nine 显卡、许多 Diamond Stealth 显卡、Orchid Fahrenheits、Miro Crystal 8S、大多数 STB 显卡，以及一些带有内置图形加速器的主板（如 IBM ValuePoint PC）。 |
| XFree86-S3V | 适用于围绕 S3 ViRGE 芯片构建的设备的服务器。 |
| XFree86-SVGA | 适用于简单帧缓冲区 SVGA 设备的服务器，包括由 ET4000 芯片、Cirrus Logic 芯片、Chips and Technologies 笔记本芯片、Trident 8900 和 9000 芯片以及 Matrox 芯片构建的显卡。它还适用于 Diamond Speedstar、Orchid Kelvins、STB Nitros 和 Horizons、Genoa 8500VL、大多数 Actix 板卡以及 Spider VLB Plus。它也适用于许多其他 SVGA 设备。 |
| XFree86-VGA16 | 通用 16 色服务器，几乎适用于所有 VGA 设备。 |



## 表 26.1 X 服务器（续）

| X 服务器 RPM 软件包名称 | 描述 |
|---|---|
| XFree86-W32 | 适用于基于 ET4000/W32 芯片构建的设备的服务器，包括 Genoa 8900 Phantom 32i、Hercules Dynamite、LeadTek WinFast S200、Sigma Concorde、STB LightSpeed、TechWorks Thunderbolt 和 ViewTop PCI。 |
| XFree86-Xvfb | X 虚拟帧缓冲 (Virtual Frame Buffer) 服务器，无需显示硬件和输入设备即可运行。 |

## 安装软件包

一旦确定了包含适用于您系统的 X 服务器的软件包名称，就可以准备安装 X 了。在安装过程中，您还应该安装以下附加软件包：

- freetype，包含一个用于渲染 TrueType 字体的库
- gtk+，包含一个被 X 客户端使用的库
- X11R6-contrib，包含许多有用的 X 客户端
- Xconfigurator，包含用于配置 X 的 Red Hat Linux 程序
- XFree86-libs，包含主要的 XFree86 库
- XFree86，包含 XFree86 公共代码
- XFree86-75dpi-fonts，包含用于 X 的标准西欧字体
- XFree86-xfs，包含 X 字体服务器
- xinitrc，包含一个用于启动窗口管理器的脚本

不要尝试逐个安装这些软件包。其中几个软件包依赖于其他软件包，因此安装可能会因为依赖关系未满足而失败。相反，请进入包含软件包的目录，并执行一条安装所有软件包的单一 `rpm` 命令。该命令的形式应为：

```
rpm -Uvh freetype-*.rpm gtk+-*.rpm X11R6-contrib-*.rpm \
Xconfigurator-*.rpm XFree86-libs-*.rpm XFree86-*.rpm \
XFree86-75dpi-fonts-*.rpm XFree86-xfs-*.rpm \
xinitrc-*.rpm XFree86-server-*.rpm
```

其中 `XFree86-server` 是包含正确 X 服务器的软件包名称。

如果您愿意，可以安装额外的字体。表 26.2 总结了随 Red Hat Linux 分发的其他字体软件包。

### 表 26.2 附加字体软件包

| 软件包名称 | 描述 |
|---|---|
| urw-fonts | 35 种标准 Adobe Postscript 字体的免费版本 |
| XFree86-100dpi-fonts | 用于高分辨率 100 dpi 显示器的字体 |
| XFree86-cyrillic-fonts | 西里尔字母字体 |
| XFree86-ISO8859-2-Type1-fonts | 中欧 Type1（可缩放）字体 |
| XFree86-ISO8859-7-Type1-fonts | 希腊 Type1（可缩放）字体 |
| XFree86-ISO8859-2-75dpi-fonts | 中欧 75 dpi 字体 |
| XFree86-ISO8859-7-75dpi-fonts | 希腊 75 dpi 字体 |
| XFree86-ISO8859-9-75dpi-fonts | 土耳其欧洲 75 dpi 字体 |
| XFree86-ISO8859-2-100dpi-fonts | 中欧 100 dpi 字体 |
| XFree86-ISO8859-7-100dpi-fonts | 希腊欧洲 100 dpi 字体 |
| XFree86-ISO8859-9-100dpi-fonts | 土耳其欧洲 100 dpi 字体 |

您可能会发现内容相当详尽的 XFree86 文档很有帮助。该软件包需要 11MB 略多的磁盘空间。要安装它，请进入包含软件包的目录并执行命令：

```
rpm -Uvh XFree86-doc-*.rpm
```

## 配置 X

主要的 X 配置文件是 `/etc/X11/XF86Config`。您可以手动编辑此文件；然而，大多数系统管理员更倾向于使用工具来配置 X。流行的工具包括以下几种：

- **Xconfigurator** Red Hat Linux 的 X 配置工具，可在基于文本的安装期间以及基于文本或图形的安装之后使用
- **XF86Setup** XFree86 的 X 配置工具
- **xf86config** 一个基于文本的 X 配置工具

本节将解释这些工具的使用方法。此外，本节还将介绍另外两个有用的工具：

- **SuperProbe** 一个基于文本的工具，可帮助您获取有关系统显卡的信息
- **xvidtune** 一个基于文本的工具，可帮助您调整 X 以获得最佳图像

### Xconfigurator

大多数 Red Hat Linux 管理员似乎比其他 X 配置工具更喜欢使用 `Xconfigurator`。这种偏好原因之一是熟悉度：`Xconfigurator` 被用于基于文本的 Red Hat 安装过程中，因此许多 Red Hat Linux 管理员习惯于使用该工具。`Xconfigurator` 支持的显卡和显示器比 `XF86Setup` 更多——目前支持超过 600 种显卡和 900 种显示器。

要启动 `Xconfigurator`，请执行命令：

```
Xconfigurator
```

`Xconfigurator` 可以使用一种特殊的非交互式“kickstart”模式，在这种模式下，它会自动探测信息，尝试在无需人工干预的情况下配置显卡。要使用 kickstart 模式，请执行命令：

```
Xconfigurator --kickstart
```

或者，`Xconfigurator` 可以使用专家模式 (expert mode)，在这种模式下，用户能够覆盖探测到的值。要使用专家模式，请执行命令：

```
Xconfigurator --expert
```

接下来的分步说明假设您在普通模式下使用 `Xconfigurator`——即既不是 kickstart 模式也不是专家模式。图 26.1 显示了启动 `Xconfigurator` 时出现的欢迎屏幕。`Xconfigurator` 不支持使用鼠标。相反，您通过键盘与程序进行交互。以下按键具有特殊含义：

- Tab、Up（上）、Down（下）、Right（右）和 Left（左）用于在各个字段之间导航；当前字段是高亮显示的那个。
- 空格键用于切换单选按钮或复选框。
- Enter 键用于点击高亮显示的按钮。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_642_0.png)
**图 26.1** Xconfigurator 欢迎屏幕

要继续配置，请使用导航键高亮显示 OK 按钮，并按下 Enter 键点击它。随后将出现图 26.2 所示的“选择显卡 (Choose a Card)”屏幕。

**图 26.2** Xconfigurator 选择显卡屏幕
![](img/4eef9c6f2f52b608eba628cf4e2793ce_643_0.png)

您可以从列表中选择一张显卡并点击 OK 按钮，或者选择最后一个条目“未列出显卡 (Unlisted Card)”。Xconfigurator 将尝试为选定的显卡确定合适的 X 服务器。如果无法确定，它将显示图 26.3 所示的“选择服务器 (Pick a Server)”屏幕。

**图 26.3** Xconfigurator 选择服务器屏幕
![](img/4eef9c6f2f52b608eba628cf4e2793ce_643_1.png)

使用导航键高亮显示合适的服务器，然后点击 OK 按钮。如果您不确定选择哪个服务器，可以考虑选择 SVGA、VGA16 或 Mono，因为这些服务器支持多种显卡。然而，这些服务器提供的分辨率和色彩深度有限；使用通用服务器可能无法充分利用系统视频设备的性能。选定后，点击 OK 按钮。随后将出现图 26.4 所示的“显示器设置 (Monitor Setup)”屏幕。

**图 26.4** Xconfigurator 显示器设置屏幕
![](img/4eef9c6f2f52b608eba628cf4e2793ce_644_0.png)

使用导航键高亮显示合适的显示器；如果您找不到您的显示器，请选择“自定义 (Custom)”。点击 OK 按钮。

**警告** 显示器的品牌和型号选择必须与您的显示器完全匹配。*不要选择一个仅仅是相似而非完全相同的显示器。* 通常，型号数字相近的显示器其运行特性可能截然不同。选择错误的显示器可能会对您的显示器造成永久性损坏。如果有疑问，请选择“Custom”并直接输入运行参数。

如果您选择 Custom，将出现图 26.5 所示的“自定义显示器设置 (Custom Monitor Setup)”屏幕；否则，将出现图 26.8 所示的“屏幕配置 (Screen Configuration)”屏幕。点击 OK 按钮继续。随后将出现图 26.6 所示的“自定义显示器设置（续）”屏幕。

**图 26.5** Xconfigurator 自定义显示器设置屏幕
![](img/4eef9c6f2f52b608eba628cf4e2793ce_645_0.png)

正如自定义显示器设置屏幕告知您的那样，水平同步率 (horizontal sync rate) 和垂直刷新率 (vertical refresh rate) 是关键参数。为其中任何一个参数输入错误的值都可能永久损坏显示器。请从可靠来源（如用户手册或制造商网站）获取这些值。现代的多同步显示器比旧款显示器更耐损，但并非完全免疫。无论如何，不要让显示器在显示花屏图像的状态下停留超过必要的时间；请立即关闭电源并重新配置运行参数。

**图 26.6** Xconfigurator 自定义显示器设置（续）屏幕
![](img/4eef9c6f2f52b608eba628cf4e2793ce_645_1.png)



为您的显示器选择一个合适的*水平同步率*。如果不确定正确的值，请保守选择以避免损坏显示器。选中正确的同步率后，点击 OK 按钮。随后将出现第二个“自定义显示器设置（续）”屏幕，如图 26.7 所示。

### 图 26.7 Xconfigurator 自定义显示器设置（续）屏幕
![](img/4eef9c6f2f52b608eba628cf4e2793ce_646_0.png)

为您的显示器选择一个合适的*垂直刷新率*。如果不确定正确的值，请保守选择以避免损坏显示器。选中正确的同步率后，点击 OK 按钮。随后将出现“屏幕配置”屏幕，如图 26.8 所示。

#### 图 26.8 Xconfigurator 屏幕配置屏幕
![](img/4eef9c6f2f52b608eba628cf4e2793ce_646_1.png)

该屏幕允许您避免探测显卡，因为探测有时会导致系统挂起。通常，您应该选择“探测”并让 `Xconfigurator` 探测显卡；如果您遇到问题，可以重启 `Xconfigurator` 并跳过探测。

如果您选择“探测”并点击 OK 按钮，一个对话框将确认您的操作并要求您点击 OK 以继续。如果探测成功，将出现“探测即将开始”屏幕，如图 26.13 所示。如果您选择“不探测”或探测失败，系统将提示您输入所需信息。例如，可能会出现“显存”屏幕，如图 26.9 所示。

#### 图 26.9 Xconfigurator 显存屏幕
![](img/4eef9c6f2f52b608eba628cf4e2793ce_647_0.png)

选择您的视频设备上可用的显存量，然后点击 OK 按钮。随后将出现“时钟芯片配置”屏幕，如图 26.10 所示。

#### 图 26.10 Xconfigurator 时钟芯片配置屏幕
![](img/4eef9c6f2f52b608eba628cf4e2793ce_648_0.png)

通常，您应该选择“无时钟芯片”设置，因为 X 服务器可以通过探测来确定时钟芯片设置。然而，某些显卡无法成功探测；此屏幕允许您解决该问题。选中正确的时钟芯片设置后，点击 OK 按钮。如果您选择了“无时钟芯片”，将出现“时钟探测”屏幕，如图 26.111 所示；否则，将出现“选择视频模式”屏幕，如图 26.12 所示。

#### 图 26.11 Xconfigurator 时钟探测屏幕
![](img/4eef9c6f2f52b608eba628cf4e2793ce_648_1.png)

在“时钟探测”屏幕中，点击 OK 按钮开始探测。随后将出现“选择视频模式屏幕，如图 26.12 所示。

#### 图 26.12 Xconfigurator 选择视频模式屏幕
![](img/4eef9c6f2f52b608eba628cf4e2793ce_649_0.png)

选择一个或多个所需的的分辨率和色彩深度。如果您选择了多种模式，可以在 X 运行期间使用 Ctrl+Alt++ 在它们之间循环切换。但是，您必须使用数字键盘上的 + 键；普通 + 键在此用途下将不起作用。选中所需模式后，点击 OK 按钮。随后将出现“探测即将开始”屏幕，如图 26.13 所示。

#### 图 26.13 Xconfigurator 探测即将开始屏幕
![](img/4eef9c6f2f52b608eba628cf4e2793ce_649_1.png)

点击 OK 按钮以测试您的 X 配置。如果配置正确，您将看到一个询问“你能看到这条消息吗？”的小对话框。如果您能看到该对话框，请点击 Yes 按钮。第二个对话框将询问您是否希望配置系统在启动时启动 X。根据您的偏好点击 Yes 或 No 按钮。

如果您看不到那个小对话框，`Xconfigurator` 将在几秒钟后将您返回到配置步骤。您可以指定不同的运行参数并再次尝试启动 X。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_650_0.png)

众所周知，笔记本电脑的 X 配置非常困难。原因之一是看似相同的笔记本电脑可能包含截然不同的视频硬件。有关配置 Linux 笔记本电脑的帮助，请参阅 Linux 笔记本电脑网页：`www.cs.utexas.edu/users/kharker/linux-laptop`。

现在完成练习 26.1 以获得使用 `Xconfigurator` 的经验。

#### 练习 26.1：使用 Xconfigurator

有时您可能会发现有必要在安装 Linux 后安装 X。本练习将让您练习此操作。请执行以下步骤：

- 1. 安装 X 以及使用 `Xconfigurator` 所需的 X 相关软件包。
- 2. 使用 `Xconfigurator` 配置 X。验证配置是否有效。
- 3. 使用 `Xconfigurator` 的快速启动功能配置 X。验证配置是否有效。

为了获得完成此练习的帮助，您可以参考本书和其他文档。但在参加 RHCE 考试之前，请确保您能够在不寻求帮助的情况下使用 `Xconfigurator` 安装 X。

### XF86Setup

XFree86 项目分发其自带的 X 配置工具 `XF86Setup`。一些管理员更喜欢这个工具而非 `Xconfigurator`，因为它允许使用鼠标。为此，它使用了 VGA16 服务器的功能，该服务器由广泛的视频设备支持。

要使用 `XF86Setup`，除了前一小节提供的软件包外，您还应安装以下软件包：

- `glib10`：实用函数库，其中部分函数被该工具使用
- `tcl`：该工具使用的脚本语言
- `tk`：tcl 使用的组件集
- `XFree86-VGA16`：VGA16 服务器
- `XFree86-XF86Setup`：工具本身

要安装这些软件包，请进入包含它们的目录并执行命令：

```
rpm -Uvh glib10-*.rpm tcl-*.rpm tk-*.rpm \
XFree86-VGA16-*.rpm XFree86-XF86Setup-*.rpm
```

要启动 XF86Setup，请执行命令：

```
XF86Setup
```

随后将出现 XF86Setup 介绍屏幕，如图 26.14 所示。

#### 图 26.14 XF86Setup 介绍屏幕
![](img/4eef9c6f2f52b608eba628cf4e2793ce_651_0.png)

该屏幕顶部提供了六个按钮：

- 鼠标（Mouse）按钮允许您配置鼠标。
- 键盘（Keyboard）按钮允许您配置键盘。
- 显卡（Card）按钮允许您配置视频设备。
- 显示器（Monitor）按钮允许您配置显示器。
- 模式选择（Mode Selection）按钮允许您配置色彩深度和视频分辨率。
- 其他（Other）按钮允许您配置若干 X 选项。

要配置鼠标，点击鼠标按钮。随后将出现一个帮助屏幕，解释各种与鼠标相关的选项。在浏览完信息后，点击 Dismiss 关闭窗口。随后将出现鼠标屏幕，如图 26.15 所示。

#### 图 26.15 XF86Setup 鼠标屏幕
![](img/4eef9c6f2f52b608eba628cf4e2793ce_652_0.png)

选择所需的鼠标选项。点击 Apply 按钮立即应用鼠标配置。当鼠标正常工作时，点击键盘按钮。随后将出现键盘屏幕，如图 26.16 所示。

#### 图 26.16 XF86Setup 键盘屏幕
![](img/4eef9c6f2f52b608eba628cf4e2793ce_653_0.png)

选择所需的键盘选项。点击 Apply 按钮立即应用键盘配置。当键盘正常工作时，点击显卡按钮。随后将出现显卡屏幕，如图 26.17 所示。

#### 图 26.17 XF86Setup 显卡屏幕

从列表中选择正确的显卡。如果列表中没有该显卡，请点击详细设置（Detailed Setup）按钮手动输入配置。随后将出现详细显卡屏幕，如图 26.18 所示。

#### 图 26.18 XF86Setup 详细显卡屏幕
![](img/4eef9c6f2f52b608eba628cf4e2793ce_655_0.png)

为显卡选择正确的配置。如果您愿意，可以点击显卡列表（Card List）按钮返回到显卡屏幕。配置正确后，点击显示器按钮。随后将出现显示器屏幕，如图 26.19 所示。

#### 图 26.19 XF86Setup 显示器屏幕
![](img/4eef9c6f2f52b608eba628cf4e2793ce_656_0.png)

输入显示器的水平同步率和垂直刷新率。或者，如果您愿意，选择与显示器特性相对应的列表项。点击模式选择按钮。随后将出现模式选择屏幕，如图 26.20 所示。



#### 图 26.20 XF86Setup 模式选择屏幕

![](img/4eef9c6f2f52b608eba628cf4e2793ce_657_0.png)

选择您偏好的模式（或多个模式以及色彩深度。仅选择视频设备支持的值。完成选择后，点击 Other 按钮。随后将出现如图 26.21 所示的 Other 屏幕。

#### 图 26.21 XF86Setup Other 屏幕

![](img/4eef9c6f2f52b608eba628cf4e2793ce_658_0.png)

Other 屏幕允许您启用或禁用若干 X 选项。选好您偏好的配置后，点击 Done 按钮。XF86Setup 会构建您指定的配置并将其存储在 `/etc/X11/XF86Config` 文件中。有关 XF86Setup 的更多信息，请参阅其 man 手册页。

现在完成练习 26.2 以获得使用 XF86Setup 的经验。

#### 练习 26.2：使用 XF86Setup

相比 Xconfigurator，XF86Setup 工具能让您更精细地控制 X 配置。要获得使用 XF86Setup 的经验，请执行以下步骤：

- 1. 安装 X 以及使用 XF86Setup 所需的 X 相关软件包。
- 2. 使用 XF86Setup 配置 X。验证配置是否生效。

在完成此练习时，您可以参考本书和其他文档寻求帮助。但在参加 RHCE 考试之前，请确保您能够在不借助帮助的情况下使用 XF86Setup 安装 X。

### xf86config

第三个 X 配置工具 `xf86config` 是一个基于文本的工具，它使用提示/回答对话框来配置 X。因此，该工具使用起来有些繁琐。但它非常灵活且包含在 XFree86 软件包中。因此，在其他工具需要安装额外软件包的地方，`xf86config` 可能会发挥作用。

`xf86config` 对话框中的步骤与 Xconfigurator 和 `XF86Setup` 类似，因为它们收集的信息本质上是一样的。基本步骤为：

- 1. 介绍
- 2. 鼠标配置
- 3. 键盘配置
- 4. 显示器配置
- 5. 显卡配置
- 6. 服务器选择
- 7. 模式选择
- 8. 配置文件生成

现在完成练习 26.3 以获得使用 `xf86config` 的经验。

#### 练习 26.3：使用 xf86config

`xf86config` 工具的用户界面不如 Xconfigurator 或 XF86Setup 精美，但它能为您提供极高程度的 X 配置控制权。要获得使用 `xf86config` 的经验，请执行以下步骤：

- 1. 安装 X。
- 2. 使用 `xf86config` 配置 X。验证配置是否生效。

在完成此练习时，您可以参考本书和其他文档寻求帮助。但在参加 RHCE 考试之前，请确保您能够在不借助帮助的情况下使用 `xf86config` 安装 X。

### SuperProbe

SuperProbe 工具可以帮助您确定视频设备的类型和运行特性。该工具包含在 XFree86 软件包中。要运行 SuperProbe，请输入命令：

```
SuperProbe
```

输出应类似于以下内容：

```
SuperProbe Version 2.18 (22 December 1998)
(c) Copyright 1993,1994 by David Wexelblat
<dwex@xfre86.org>
(c) Copyright 1994-1998 by The XFree86 Project, Inc
```

> 本作品衍生自 Finn Thoegersen 制作并获得所有相关许可后发布的 'vgadoc2.zip' 和 'vgadoc3.zip' 文档包。其他信息获取自 Richard Ferraro 的 'Programmer's Guide to the EGA and VGA, 2nd ed' 以及制造商的数据手册。

欢迎发送 Bug 报告至 XFree86@XFree86.org。特别是对于该程序未能正确检测到的芯片组报告，我们将不胜感激。

在提交报告之前，请确保您拥有最新版本的 SuperProbe（参见 http://www.xfree86.org/FAQ）。

```
WARNING - THIS SOFTWARE COULD HANG YOUR MACHINE.
READ THE SuperProbe.1 MANUAL PAGE BEFORE
RUNNING THIS PROGRAM.
```

```
INTERRUPT WITHIN FIVE SECONDS TO ABORT!
First video: Super-VGA
Chipset: Matrox Millennium (PCI Probed)
RAMDAC: TI ViewPoint3026 24-bit TrueColor DAC w/cursor,
pixel-mux,clock (with 6-bit wide lookup tables (or in
6-bit mode)
```

请注意，该工具会警告它可能会导致某些系统挂起。您可以在探测启动前按下 Ctrl+C 中断程序。
现在通过完成练习 26.4 来练习使用 SuperProbe。

#### 练习 26.4：使用 SuperProbe

SuperProbe 是一个有用但并非万能的工具。为了获得经验，请在您的系统上运行它。输出内容是否正确陈述了您系统视频设备的类型和特性？

### xvidtune

xvidtune 工具可以帮助您微调 X 配置。它允许您交互式地调整视频模式和扫描率，以获得最佳性能。该工具是 XFree86 软件包的一部分。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_661_0.png)

如果您指定了不正确的扫描率，xvidtune 工具可能会损坏显示器。请务必仅提供正确的值。

## 重要的 X 目录与文件

`/usr/X11R6/bin` 目录包含 X 的二进制文件。为了使 X 程序正常运行，`/usr/X11R6/bin` 目录应出现在存储在 `PATH` 环境变量中的程序路径中。

另一个重要的 X 目录是 `/etc/X11`。该目录及其子目录包含 X 配置。符号链接 `/etc/X11/X` 指向当前选定的 X 服务器，该服务器位于 `/usr/X11R6/bin` 中。

`/etc/X11` 目录还包含 `XF86Config` 文件，这是主要的 X 配置文件，通常使用 Xconfigurator 或 XF86Setup 构建。有关 `/etc/X11/XF86Config` 文件的更多信息，请参阅 XF86Config man 手册页。

现在完成练习 26.5，该练习要求您研究主 X 配置文件。

### 练习 26.5：检查 /etc/X11/XF86Config 文件

由于视频特性的差异，X 配置在不同系统之间可能会有显著不同。将正确配置的 X 安装环境中的 XF86Config 文件与本小节所示的配置进行比较。您发现了哪些相似之处和不同之处？

## 总结

在本章中，您学习了 X 的安装和配置。涵盖的最重要主题包括：

**X 窗口系统** (X) 提供了 Red Hat Linux 使用的图形用户界面。X 的实现版本适用于多种 Unix 和非 Unix 平台。随 Red Hat Linux 分发的 X 版本由 XFree86 项目发布。

**服务器与客户端** 管理用户界面的 X 程序称为 X 服务器。使用用户界面的应用程序或其他程序称为 X 客户端。

**安装 X** 安装 X 涉及安装多个软件包。其中最重要的是包含 X 服务器的软件包，必须根据系统中安装的视频适配器类型进行选择。

**配置 X** 您可以使用多种工具配置 X，包括以下工具：

- Xconfigurator
- XF86Setup
- xf86config
- SuperProbe
- xvidtune

**X 目录与文件** `/usr/X11R6/bin` 目录包含 X 二进制文件。`/etc/X11` 目录及其子目录包含 X 配置。符号链接 `/etc/X11/X` 指向当前选定的 X 服务器。`/etc/X11` 目录还包含 `XF86Config` 文件，即主 X 配置文件。

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- 桌面管理器 (desktop manager)
- 水平同步率 (horizontal sync rate)
- 垂直刷新率 (vertical refresh rate)
- 窗口管理器 (window manager)
- X 客户端 (X client)
- X 服务器 (X server)

## 其他信息来源

如果您想进一步了解本章介绍的主题，应参考以下来源：

- XFree86 FAQ, www.xfree86.org/FAQ
- XFree86-doc 软件包中的 XFree86 文档
- 官方 Red Hat Linux 参考指南

## 复习题

- 1. 以下哪个是 X 中负责与视频硬件接口的组件？
    - A. 客户端
    - B. 桌面管理器
    - C. 服务器
    - D. 窗口管理器

- 2. 以下哪个 X 服务器支持的视频设备类型最多？
    - A. XFree86-AGX
    - B. XFree86-S3
    - C. XFree86-SVGA
    - D. XFree86-W32

- 3. 以下哪种配置 X 的方法在 Red Hat 社区中最受欢迎？
    - A. vi
    - B. Xconfigurator
    - C. xf86config
    - D. XF86Setup

- 4. 为了避免损坏显示器，您应该准确指定什么？
    - A. 色彩深度
    - B. 水平同步率
    - C. 分辨率
    - D. 视频 RAM 容量



5. 下面哪个目录存放 X 的二进制文件？
A. /etc/X11
B. /etc/X11R6/bin
C. /usr/X11R6
D. /usr/X11R6/bin

6. 关于当前配置的 X 服务器，以下哪项是正确的？
A. 它与其它 X 二进制文件位于同一个目录中。
B. 链接 /etc/X11 指向它。
C. 链接 /etc/X11/X 指向它。
D. 链接 /etc/X11/XServer 指向它。

## 复习题答案

1. C. 服务器充当设备驱动程序，代表应用程序（称为客户端）提供图形服务。

2. C. `SVGA` 服务器支持许多 SVGA 设备。只有 VGA16 和 Mono 服务器支持更多。

3. B. `Xconfigurator` 程序由 Red Hat, Inc. 编写，并在基于文本的安装过程的一部分将其调用。`xf86config` 和 `XF86setup` 均由 XFree86 Project, Inc. 作为 XFree86 的一部分分发。

4. B. 水平同步率（以及在较小程度上的垂直刷新率）是关键的运行特性。

5. D. X 二进制文件位于 `/usr/X11R6/bin`。

6. A, C. X 服务器与其它 X 二进制文件一起位于 `/usr/X11R6/bin`。链接 `/etc/X11/X` 指向它。

# 第 27 章：理解与使用窗口管理器和桌面

### 本章涵盖的 RHCE 准备主题：

- 熟悉 Red Hat Linux 下可用的窗口管理器和桌面环境，并了解如何选择它们。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_668_0.png)

一组程序协同工作以提供 X 环境。这些程序包括：

- *窗口管理器*（window manager），负责绘制边框、标题栏、菜单栏和窗口操作按钮
- *桌面管理器*（desktop manager），提供桌面环境，包括文件管理器、帮助系统和虚拟桌面
- X 客户端，即您运行的应用程序

此外，如果您通过 X 登录，*显示管理器*（display manager）将使用 PAM 机制验证您的身份。本章将向您介绍窗口管理器、桌面管理器和显示管理器，并解释如何选择和配置它们。

## 桌面环境

Red Hat Linux 允许您在两种主要桌面环境之间进行选择：

- GNOME
- KDE

默认情况下，GNOME 环境包括 GNOME 桌面管理器和 Enlightenment 窗口管理器。KDE 环境包括 KDE 桌面管理器和 KWM 窗口管理器。本节将描述这些桌面环境，解释如何在两者之间做出选择，以及如何配置它们以配合备选的窗口管理器工作。

### GNOME 桌面管理器

开源的 GNOME 桌面环境是使用 CORBA（公共对象请求代理架构）和 GIMP（GNU 图像编辑程序）工具集（GTK+）编写的。GNOME 的开发得到了 Red Hat, Inc. 通过 RHAD Labs 的慷慨资助。图 27.1 显示了一个典型的 GNOME 桌面。

**图 27.1** GNOME 桌面管理器
![](img/4eef9c6f2f52b608eba628cf4e2793ce_669_0.png)

符合 GNOME 规范的应用程序具有会话感知能力，这意味着当您退出 GNOME 时，它们会保存自己的状态。当您重新进入 GNOME 时，会话感知应用程序会重新打开之前打开的文档，将光标重新定位到原来的位置，并通常帮助您从上次离开的地方恢复工作。GNOME 开发者计划最终通过 CORBA 提供一种类似于微软对象链接与嵌入（OLE）的功能。

GNOME 经常与 Enlightenment 窗口管理器一起使用，后者是专门为与 GNOME 配合使用而设计的。不过，它也可以与其他窗口管理器配合使用。一些窗口管理器已经经过修订以更好地与 GNOME 协作，包括 Window Maker 和 IceWM，它们被认为是符合 GNOME 规范的。其他窗口管理器的作者（包括 AfterStep 和 FVWM）通常也在致力于实现 GNOME 兼容性。有关最新信息，请参阅 GNOME FAQ `www.gnome.org/gnomefaq`。

GNOME 包含许多有用的功能和设施，例如：

- 一个支持拖放操作的文件管理器 `gnome-fm`（或 `gnic`）
- 代表程序和目录的桌面图标
- 一个可以超过物理屏幕尺寸的虚拟桌面
- 一个允许您在虚拟桌面中导航的分页器（pager）
- 一个提供类似于 Microsoft Windows 任务栏功能的面板（panel）
- 允许您通过点击鼠标启动应用程序的启动器（launchers）
- 允许您选择协调视觉外观的主题（themes）

有关 GNOME 的更多信息，请访问 GNOME 网站 `www.gnome.org`。有关 GNOME 主题的信息，请访问 `gtk.themes.org`；Enlightenment 有自己的主题网站 `e.themes.org`。

### KDE 桌面管理器

KDE 桌面管理器提供了与 GNOME 类似的功能和设施。与使用独立 Enlightenment 窗口管理器的 GNOME 不同，KDE 拥有自己的窗口管理器 KWM，这是与 KDE 配合使用最受欢迎的窗口管理器；不过，KDE 也兼容 AfterStep、Enlightenment 和 WindowMaker 等窗口管理器。图 27.2 显示了一个典型的 KDE 桌面。

**图 27.2** KDE 桌面管理器
![](img/4eef9c6f2f52b608eba628cf4e2793ce_670_0.png)

KDE 是使用 Qt 工具集编写的，该工具集由挪威软件开发公司 Troll Tech 开发。最初 Qt 工具集的许可协议较为严格，这减缓了开源社区对 KDE 的接受速度。

近期，Qt 的许可限制已解除，KDE 获得了更广泛的追随者。

KDE 的文件管理器被称为 KFM。KDE 包含大量有用的桌面应用程序。有关 KDE 的进一步信息，请访问 KDE 网站 `www.kde.org`。

### 切换桌面管理器

要指定所需的桌面管理器，请使用 `xterm` 通过执行以下命令来调用 `switchdesk` 工具：

```bash
/usr/bin/switchdesk
```

该程序会显示一个小的对话框，如图 27.3 所示。选择所需的桌面管理器，然后点击 OK 按钮。支持以下桌面管理器：

- GNOME
- KDE
- AnotherLevel，一个类似于曾经在 NeXTStep 操作系统中使用的桌面管理器

更改不会立即生效。您必须退出 X 并重新进入，以加载指定的桌面管理器。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_671_0.png)

运行 `switchdesk` 时，它会创建两个配置文件（实际上是脚本），这些文件位于运行用户的主目录中：

- `.Xclients`，它调用 `.Xclients-default` 或一个与特定主机相关的特殊 `.Xclients` 文件
- `.Xclients-default`，用于启动窗口和桌面管理器

以下是一个典型的 `.Xclients` 脚本的内容：

```bash
#!/bin/bash

# Created by Red Hat Desktop Switcher

if [ -e "$HOME/.Xclients-$HOSTNAME$DISPLAY" ]; then
    exec $HOME/.Xclients-$HOSTNAME$DISPLAY
else
    exec $HOME/.Xclients-default
fi
```

现在，通过完成练习 27.1 来实践选择桌面管理器。

#### 练习 27.1：选择桌面管理器

选择桌面管理器非常简单。通过执行以下步骤亲自尝试：

1. 如果 GNOME 或 KDE 尚未安装，请安装它。
2. 在 X 环境下，使用 `switchdesk` 将 GNOME 指定为桌面管理器。退出并重新进入 X 以验证您的选择是否正常工作。
3. 使用 `switchdesk` 将 KDE 指定为桌面管理器。退出并重新进入 X 以验证您的选择是否正常工作。

下一小节将解释如何选择窗口管理器。

### 选择窗口管理器

如前所述，窗口管理器提供边框、标题栏、菜单栏、窗口操作按钮和其他视觉元素。一些流行的窗口管理器包括：

- AfterStep，类似于 NeXTStep 操作系统之前使用的 GUI。
- Enlightenment，GNOME 偏好的窗口管理器。Enlightenment 是一个功能丰富的窗口管理器，需要相当多的系统资源。
- FVWM，一个相当古老但非常高效的窗口管理器，可以模仿 Windows 95 或 Motif。FVWM 是为 Linux 使用而开发的，且依然受欢迎。
- Sawfish，原名 Sawmill，一个新型且很大程度上符合 GNOME 规范的窗口管理器，以其相对于 Enlightenment 较低的资源需求而著称。在 Red Hat Linux 6.2 中，它以 `sawmill` 和 `sawmill-gnome` 软件包形式分发。
- WindowMaker，一个流行且高效的窗口管理器，类似于 NeXTStep GUI。

如果 `~/.Xclients` 脚本存在，它将决定运行哪个窗口管理器。如果没有 `~/.Xclients` 脚本，则由 `/etc/X11/xinit/Xclients` 脚本决定运行哪个窗口管理器。以下是标准 `/etc/X11/xinit/Xclients` 脚本的内容：

```bash
#!/bin/bash
# (c) 1999, 2000 Red Hat, Inc.

# check to see if the user has a preferred desktop
PREFERRED=
if [ -f /etc/sysconfig/desktop ]; then
    if [ -n `grep -i GNOME /etc/sysconfig/desktop` ]
    then
        PREFERRED=gnome-session
    elif [ -n `grep -i KDE /etc/sysconfig/desktop` ]
    then
        PREFERRED=startkde
    elif [ -n `grep -i AnotherLevel` /etc/sysconfig/desktop` ]
```



```bash
then
then
    PREFERRED=AnotherLevel
fi
fi

if [ -n "$PREFERRED" -a "$PREFERRED" != "AnotherLevel" ] \
    && which $PREFERRED >/dev/null 2>&1; then
    PREFERRED=`which $PREFERRED`
    exec $PREFERRED
fi

# now if we can reach here, either they want AnotherLevel
# or there was no desktop file present and the PREFERRED
# variable is not set.

if [ -z "$PREFERRED" ]; then

    GSESSION=gnome-session
    STARTKDE=startkde

    # by default, we run GNOME.
    if which $GSESSION >/dev/null 2>&1; then
        exec `which $GSESSION`
    fi

    # if GNOME isn't installed, try KDE.
    if which $STARTKDE >/dev/null 2>&1; then
        exec `which $STARTKDE`
    fi
fi

# Last, try AnotherLevel

# these files are left sitting around by TheNextLevel.
rm -f $HOME/Xrootenv.0
rm -f /tmp/fvwmrc* 2>/dev/null
```

```bash
# First thing - check the user preferences
if [ -f $HOME/.wm_style ] ; then
  WMSTYLE=`cat $HOME/.wm_style`
  case "$WMSTYLE" in
    Afterstep | AfterStep)
      exec /usr/X11R6/bin/RunWM --AfterStep
      ;;
    WindowMaker | Windowmaker | WMaker | wmaker)
      exec /usr/X11R6/bin/RunWM --WindowMaker
      ;;
    Fvwm95 | fvwm95)
      exec /usr/X11R6/bin/RunWM --Fvwm95
      ;;
    Mwm | MWM | Lesstif)
      exec /usr/X11R6/bin/RunWM --FvwmMWM
      ;;
  esac
fi

# Argh! Nothing good is installed. Fall back to fvwm2
# (win95-style) or twm
/usr/X11R6/bin/RunWM --Fvwm95 || (
  # gosh, neither fvwm95 nor fvwm2 is available;
  # fall back to failsafe settings
  xclock -geometry 100x100+5-5 &
  xterm -geometry 80x50-50+150 &
  if [ -f /usr/bin/netscape \
      -a -f /usr/doc/HTML/index.html ]
  then
    netscape /usr/doc/HTML/index.html &
  fi
  if [ -f /usr/X11R6/bin/fvwm ]; then
    exec fvwm
  else
    exec twm
  fi
)
```

该脚本会检查包含要运行的窗口管理器名称的 `~/.wm_style` 文件，并启动指定的窗口管理器。如果该文件不存在，脚本将启动 FVWM95 窗口管理器。如果脚本无法启动 FVWM95 窗口管理器（可能是因为未安装），它将启动 FVWM 或 TWM（一个作为 XFree86 软件包的一部分安装的非常小且高效的窗口管理器）。

现在进行练习 27.2，该练习要求你选择一个窗口管理器。

## 练习 27.2
### 选择窗口管理器

如前所述，`~/.wm_style` 文件指定了窗口管理器的名称。请执行以下步骤尝试更改窗口管理器：

- 1. 如果未安装 FVWM95，请安装它。
- 2. 使用 `~/.wm_style` 将 FVWM95 指定为你的窗口管理器。退出并重新进入 X 以验证你的选择是否正常运行。

你可以参考本书或其他文档来帮助完成此练习。但在参加 RHCE 考试之前，请确保你能够在不参考书本或笔记的情况下选择窗口管理器。

## 显示管理器

Red Hat Linux 允许你在三种显示管理器中进行选择：

- GDM，与 GNOME 相关的显示管理器
- KDM，与 KDE 相关的显示管理器
- XDM，作为 XFree86 一部分分发的显示管理器

所有这三种显示管理器都可以与多种桌面环境配合使用。例如，你可以将 GDM 显示管理器与 AnotherLevel、GNOME 或 KDE 配合使用。GDM 和 KDM 都具有高度的可配置性。XDM 显示管理器的可配置性不高，但在支持远程 X 登录时比 GDM 或 KDM 更稳健，远程 X 登录将在第 28 章“配置和使用远程 X 服务器与客户端”中介绍。

要选择显示管理器，请按如下方式修改 `/etc/sysconfig/desktop` 文件：

- 若要使用 GDM 显示管理器，请指定 GNOME。
- 若要使用 KDM 显示管理器，请指定 KDE。
- 若要使用 XDM 显示管理器，请指定 AnotherLevel。

现在完成练习 27.3，以获得选择显示管理器的经验。

## 练习 27.3
### 选择显示管理器

在 Red Hat Linux 6.2 中，选择显示管理器非常简单。请通过执行以下步骤尝试选择显示管理器：

- 1. 配置系统使用 `gdm` 显示管理器。登录以验证你的选择是否正常运行。
- 2. 配置系统使用 `kdm` 显示管理器。登录以验证你的选择是否正常运行。
- 3. 配置系统使用 `xdm` 显示管理器。登录以验证你的选择是否正常运行。

如需完成此练习的帮助，你可以参考本书或其他文档。但在参加 RHCE 考试之前，请确保你能够在不参考书本或笔记的情况下选择显示管理器。

## 启动 X

你可以将系统设置为提供控制台登录或 X 登录。`/etc/inittab` 文件包含以下行：

```
id:n::initdefault:
```

其中 *n* 是默认运行级别。将 *n* 设置为 3 以提供控制台登录；将 *n* 设置为 5 以提供 X 登录。X 的启动过程取决于你指定的运行级别。

如果你指定运行级别 3，你应该通过执行以下命令启动 X 会话：

```
startx
```

如果 `~/.xinitrc` 文件存在，X 将加载该文件；否则，X 将加载 `/etc/X11/xinit/xinitrc` 文件。相应地，该文件如果存在 `~/.Xclients` 则加载它，否则加载 `/etc/X11/xinit/Xclients`。在 Red Hat Linux 6.2 中，该文件还会加载 `/etc/X11/xinit/xinitrc.d` 中的所有脚本。

如果你指定运行级别 5，X 将显示登录提示。当你登录时，如果 `~/.xsession` 文件存在，X 将加载它。用户可以修改 `~/.xsession` 文件，因此它可以启动另一个窗口或桌面管理器。如果 `~/.xsession` 不存在，X 将加载 `~/.Xclients`（如果存在），否则加载 `/etc/X11/xinit/Xclients`。

现在完成练习 27.4，该练习要求你定制 X 环境。

## 练习 27.4
### 设置 X 环境

由于 X 的运行基于脚本，你可以按照自己的喜好定制 X 的运行方式。为了获得设置 X 环境的经验，请配置 X 为所有用户默认启动 GNOME，但为某个特定用户启动 KDE。

你可以参考本书或其他文档来帮助完成此练习。但在参加 RHCE 考试之前，请确保你能够在不参考书本或笔记的情况下执行此练习所要求的操作。

## 使用 X 客户端

在启动 X 客户端时，你可以指定决定客户端外观的选项。表 27.1 总结了一些最常用的选项。例如，要启动一个黑底绿字的 X 终端，请执行命令：

```
xterm –foreground green –background black
```

### 表 27.1 X 客户端常用选项

| 选项 | 描述 |
| :--- | :--- |
| `-background color` 或 `-bg color` | 设置窗口背景颜色。 |
| `-bordercolor color` | 设置窗口边框颜色。 |
| `-borderwidth width` | 设置窗口边框宽度（以像素为单位）。 |
| `-display [server]:n.m` | 设置显示，其中 *server* 是主机，*n* 是显示编号，*m* 是屏幕编号。第一个显示和屏幕被指定为 0.0。 |
| `-font font` | 设置窗口中使用的默认字体。 |
| `-foreground color` 或 `-fg color` | 设置窗口前景色。 |
| `-geometry widthxheight+x+y` | 设置窗口的大小和位置（以像素为单位），其中 *width* 是窗口宽度，*height* 是窗口高度，*x* 是窗口左上角的水平偏移量，*y* 是窗口左上角的垂直偏移量。 |
| `-title string` | 设置窗口标题。 |

你可以通过键盘输入控制序列来控制 X 的运行。表 27.2 描述了几个最常用的控制序列。

### 表 27.2 有用的控制序列

| 控制序列 | 描述 |
| :--- | :--- |
| Ctrl+Alt++ | 切换视频模式（必须使用数字键盘上的 + 键）。 |
| Ctrl+Alt+Backspace | 退出 X。 |
| Ctrl+Alt+Fn | 切换到文本模式虚拟终端，*n*=1 到 6。 |
| Ctrl+Alt+F7 | 从文本模式虚拟终端切换回 X。 |



## 总结

在本章中，你学习了 X 窗口管理器、桌面管理器和显示管理器。涵盖的最重要主题包括：

**桌面环境（Desktop Environment）** 一个典型的桌面环境提供桌面图标、用于启动程序的菜单、用于选择窗口的菜单、文件管理器、帮助设施以及各种其他功能。Red Hat Linux 允许你选择两种桌面环境之一，一种由 GNOME 桌面管理器提供，另一种由 KDE 桌面管理器提供。你可以在系统安装期间或安装之后选择桌面环境。

**窗口管理器（Window Managers）** 窗口管理器控制窗口的外观和行为。在 Red Hat Linux 支持的任何桌面环境中，你都可以使用多种窗口管理器。然而，大多数用户倾向于使用与其选择的桌面环境紧密集成的窗口管理器：GNOME 搭配 Enlightenment，或 KDE 搭配 KWM。你可以通过修改 `~/.wm_style` 配置文件来选择新的窗口管理器。

**显示管理器（Display Managers）** 显示管理器管理对 X 服务器的访问并提供一个基于 X 的登录界面。Red Hat Linux 支持三种显示管理器：XDM、GDM 和 KDM。使用远程窗口的用户可能会发现 XDM 比其他两种显示管理器更稳健。

**X 登录（X Logins）** 默认运行级别为 5 的系统将自动显示基于 X 的登录界面。要禁用基于 X 的登录，请将默认运行级别设置为 3。

**X 客户端（X Clients）** X 客户端支持多种参数，允许你自定义它们的外观和行为。

**键盘控制序列（Keyboard Control Sequences）** 你可以使用键盘控制序列在 X 和虚拟控制台之间进行切换。

### 关键术语

在进入下一章之前，请确保你熟悉以下术语：

- 桌面管理器 (desktop manager)
- 显示管理器 (display manager)
- 窗口管理器 (window manager)

## 附加信息源

如果你想进一步了解本章介绍的主题，应参考以下资源：

- X 的 man 手册页
- XFree86 文档，`/usr/doc/XFree86-*`
- GNOME 文档，`/usr/doc/gnome-*`
- GNOME 和 KDE 官方网站，www.gnome.org 和 www.kde.org

## 复习题

1. 以下哪些是 Red Hat Linux 的主要桌面环境？
   A. AfterStep
   B. FVWM
   C. GNOME
   D. KDE

2. 哪个窗口管理器是第一个兼容 GNOME 的窗口管理器？
   A. AfterStep
   B. Enlightenment
   C. FVWM
   D. WindowMaker

3. 通常与 KDE 搭配使用的是哪个窗口管理器？
   A. AfterStep
   B. FVWM
   C. KWM
   D. WindowMaker

4. 用于指定桌面管理器的实用程序是：
   A. control-panel
   B. switchdesk
   C. xdm
   D. xinitrc

5. 如果通过 `startx` 启动 X，X 将尝试加载以下哪个文件？
   A. `~/.startx`
   B. `~/.xinitrc`
   C. `~/.xrc`
   D. `~/.Xsession`

6. 要指定 X 客户端显示红色文本，应指定以下哪个选项？
   A. `-background red`
   B. `-bordercolor red`
   C. `-font red`
   D. `-foreground red`

## 复习题答案

1. C, D。GNOME 和 KDE 是 Red Hat Linux 的主要桌面环境。
2. B。Enlightenment 是第一个兼容 GNOME 的窗口管理器；现在其他几个窗口管理器在不同程度上也符合 GNOME 标准。
3. C。KDE 通常与 KWM 搭配使用。
4. B。`switchdesk` 实用程序允许你指定桌面管理器。
5. B。如果通过 `startx` 启动 X，它将加载 `~/.xinitrc` 文件（如果该文件存在）。
6. D。`-foreground` 选项设置文本颜色。

# 第 28 章：配置和使用远程 X 服务器与客户端

**本章涵盖的 RHCE 准备主题：**

- 理解并能够配置和使用 X 的远程功能，包括远程客户端和远程登录。

X 最有用的功能之一是它对远程 *客户端（clients）* 和 *远程登录（remote logins）* 的支持。利用这一特性，你可以在一台主机上运行 X 客户端，并在另一台主机上显示该客户端的用户界面。例如，你可以在远程超级计算机上运行程序，但通过自己的桌面控制该程序并查看其输出。本章介绍了配置和使用远程客户端与服务器的步骤。

## X 安全性

X 实现了一种简单的 *基于主机的安全性（host-based security）* 方案，用于防止未经授权的主机访问 X 服务器。此外，还支持更复杂的基于用户的身份验证方案。

基于主机的 X 安全性通过 `xhost` 命令进行配置。你可以通过执行以下命令查看当前的安全性设置：

```bash
xhost
```

该命令将报告当前访问控制是启用还是禁用，并列出访问列表中的主机。例如，以下输出表明访问控制当前已禁用，并且如果启用访问控制，则只有主机 dale 和 roy 能够连接：

```text
access control disabled, clients can connect from any host
INET:dale
INET:roy
```

你可以执行 `xhost` 命令来查询本地或远程 X 服务器。远程执行该命令可以让你验证本地主机是否有权限访问由 `DISPLAY` 环境变量值标识的远程服务器。例如，以下命令检查本地主机访问在主机 `bigger` 上运行的 X 服务器的权限：

```bash
export DISPLAY=bigger:0.0
xhost
```

其他形式的 `xhost` 命令必须在本地执行——即在运行 X 服务器的主机上执行。要启用基于主机的安全性，请执行命令：

```bash
xhost -
```

要禁用主机安全性，使所有主机都能访问本地 X 服务器，请执行命令：

```bash
xhost +
```

要扩展客户端访问本地 X 服务器的权限，请执行如下形式的命令：

```bash
xhost +client
```

其中 `client` 是客户端的 IP 地址或主机名。要拒绝客户端访问本地 X 服务器的权限，请执行如下形式的命令：

```bash
xhost -client
```

其中 `client` 是客户端的 IP 地址或主机名。X 服务器在访问列表中存储的是主机的 IP 地址而非主机名。因此，DNS 必须能够对你指定的任何主机名执行正向和反向解析。

## 启动远程客户端

启动远程客户端非常简单，可以通过几种方式实现。一种方法是使用大多数 X 客户端提供的 `display` 参数。例如，以下命令启动 X 客户端 `xeyes`，使其使用主机 `bigger` 上的 X 服务器运行：

```bash
xeyes –display bigger:0.0 &
```

图 28.1 展示了正在运行的 `xeyes` 客户端，它显示一对跟随鼠标移动的眼睛。

**图 28.1** xeyes 客户端

xeyes 程序的功能很简单。但正因为如此，它非常适合用于测试和排除 X 的故障。

启动远程 X 客户端的通用命令格式为：

`xclient –display server[:m[.n]] [xclient_args]`

其中：

- `xclient` 和 `xclient_args` 是客户端及其可选参数。
- `server` 是 X 服务器的主机名或 IP 地址。
- `m` 是可选的服务器显示编号（默认值为 0）。
- `n` 是可选的服务器屏幕编号（默认值为 0）。此参数用于服务器单个显示关联多个屏幕的较为罕见的情况。

如果你计划启动多个 X 客户端，可能会发现设置 `DISPLAY` 环境变量更方便。随后，当你启动 X 客户端时，`DISPLAY` 环境变量的值将决定所使用的 X 服务器。例如，以下命令序列启动 `xeyes` 和 `xclock` 以使用主机 `bigger` 上的 X 服务器运行；它还启动了第二个 `xeyes` 实例在 `biggest` 上运行：

```bash
export DISPLAY=bigger:0.0
xeyes &
xclock &
xeyes -display biggest:0.0 &
```

如果 X 服务器的主机身份验证功能处于激活状态，客户端主机必须获得授权才能访问 X 服务器。否则，客户端程序将失败并显示如下消息：

```text
Xlib: connection to 'bigger:0.0' refused by server
Xlib: Client is not authorized to connect to Server
Error: Can't open display: bigger:0.0
```

如果你希望 shell 立即返回新的提示符，请在启动 X 客户端的命令后面加上和符号 (&)。

假设你当前登录到主机 `workstation`，你想在主机 `server` 上运行一个程序（例如 `xterm`），但希望在本地主机 `workstation` 上接收其输出。以下命令序列可以实现该目标：

```bash
[user@workstation]$ xhost +server
[user@workstation]$ telnet server
(log in dialog omitted)
[user@server]$ export DISPLAY=workstation:0.0
[user@server]$ xterm &
```

现在请完成练习 28.1，通过该练习你将获得操作基于主机的 X 安全性的经验。

### 练习 28.1：为远程客户端配置 X 安全性

基于主机的 X 安全性虽然不能对远程客户端提供精细的控制，但配置和使用简单。为了获得操作基于主机的 X 安全性的经验，请执行以下步骤：

1. 在服务器上，启用基于主机的 X 安全性，使其排除某些客户端主机。



## 练习 28.1 (续)

- 2. 从客户端主机尝试登录到服务器，或在服务器上打开一个 X 窗口。结果如何？
- 3. 在不禁用基于主机的安全设置的情况下，扩展客户端连接到服务器的权限。
- 4. 从客户端主机尝试登录到服务器，或在服务器上打开一个 X 窗口。结果如何？

您可以通过运行两个 X 实例在单台计算机上完成此练习。不过，您可能会发现使用两台计算机要简单得多。您可以参考本书和其他文档来帮助完成此练习。但在参加 RHCE 考试之前，请确保您能够在没有帮助的情况下执行此类操作。

## 配置远程登录

除了远程运行 X 客户端外，您还可以远程登录到运行 X 显示管理器（display manager）的主机。显示管理器将显示一个对话框（如图 28.2 所示），允许您指定登录用户名和密码。某些显示管理器提供的对话框还允许您指定所需的窗口管理器或其他选项。

图 28.2 X 登录对话框
![](img/4eef9c6f2f52b608eba628cf4e2793ce_690_0.png)

### 远程登录

要登录到运行 X 显示管理器的主机，请执行如下形式的命令：

```
X -query server
```

其中 *server* 是运行显示管理器的远程主机的主机名或 IP 地址。要登录到本地网络上的任意主机，请执行命令：

```
X -broadcast
```

某些主机被配置为提供*选择器（chooser）*，这是一个特殊的菜单，允许您选择想要登录的主机。图 28.3 显示了一个典型的选择器。要请求选择器，请执行如下形式的命令：

```
X -indirect server
```

其中 *server* 是配置为提供选择器的远程主机的主机名或 IP 地址。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_691_0.png)

### 选择显示管理器

正如第 27 章“理解并使用窗口管理器和桌面”中所解释的，Red Hat Linux 允许您在三种 X 显示管理器中选择其一：

- XDM，由 XFree86 项目分发的显示管理器
- GDM，随 GNOME 分发的显示管理器
- KDM，随 KDE 分发的显示管理器

如果您希望能够提供选择器，应将 XDM 配置为首选显示管理器；GDM 和 KDM 都有某些特性限制了它们与选择器的协作能力。例如，GDM 不响应选择器消息，因此不会出现在选择器菜单中。KDM 显示管理器虽然响应选择器消息，但有时无法提供选择器。

### 配置 xdm 提供选择器

要配置 XDM 以提供选择器，您必须修改 xdm 配置文件 `/etc/X11/xdm/Xaccess`，添加一个或多个 `chooser` 指令。这些指令的格式如下：

```
client CHOOSER server_list
```

其中 `client` 指定将提供选择器的客户端主机，`server_list` 指定将出现在选择器中的服务器。

可以使用通配符来指定客户端主机。请参考以下配置示例：

```
workstation	CHOOSER server1 server2
*.azusapacific.com	CHOOSER server3
*			CHOOSER server4
```

第一行规定主机 `workstation` 将获得一个显示主机 `server1` 和 `server2` 的选择器。第二行规定 `azusapacific.com` 域中的所有主机将获得一个显示主机 `server3` 的选择器。最后一行规定所有主机都将获得一个显示主机 `server4` 的选择器。如果一个主机名匹配多个 `CHOOSER` 行，则使用首先出现的那一行。在示例配置中，主机 `workstation.azusapacific.com` 将获得一个显示 `server1` 和 `server2` 的选择器，尽管该主机名同时也匹配第 2 行和第 3 行。

您可以使用关键字 BROADCAST 动态地指定服务器列表。例如，考虑以下指令：

```
* CHOOSER BROADCAST
```

BROADCAST 关键字会促使显示管理器通过发送特殊的广播消息，来汇总本地网络上的 X 服务器列表。所有响应广播消息的服务器都将被包含在选择器中。

默认情况下，XDM 会忽略选择器请求。要配置 XDM 以做出响应，您必须注释掉或删除 `/etc/X11/xdm/xdm-config` 中的最后一行：

```
DisplayManager.requestPort: 0
```

![](img/4eef9c6f2f52b608eba628cf4e2793ce_693_0.png)

如果您更倾向于使用 KDM 作为显示管理器并希望它提供选择器，可以使用与 XDM 相同的步骤来配置 KDM。要配置 gdm 提供选择器，您必须在 `/etc/X11/gdm/gdm.conf` 文件的 `[xdmcp]` 部分设置 `Enable=1`，并通过执行命令 `killall -HUP gdm` 强制 gdm 重新读取该文件。

现在，完成练习 28.2 以获得配置 X 远程登录的经验。

## 练习 28.2
### 配置 X 远程登录

为了练习配置远程 X 登录，请执行以下步骤：

- 1. 在服务器上，将 XDM 配置为首选显示管理器，并配置 XDM 为本地网络上的任何主机提供选择器。
- 2. 从客户端主机通过选择器登录到服务器。结果如何？
- 3. 在服务器上，将 GDM 配置为首选显示管理器。
- 4. 从客户端主机尝试通过选择器登录到服务器。结果如何？
- 5. 在服务器上，将 KDM 配置为首选显示管理器。
- 6. 从客户端主机尝试通过选择器登录到服务器。结果如何？

您可以参考本书和其他文档来帮助完成此练习。但在参加 RHCE 考试之前，请确保您能够在没有帮助的情况下执行此类操作。

## Xnest 程序

有时，在只有一个视频适配器的单台主机上运行多个 X 服务器会很有用。例如，您可能想在已经运行本地 X 服务器的同时，测试一个新的窗口管理器或通过 X 登录到远程服务器。Xnest 程序提供了一个运行在当前运行的 X 服务器所属窗口中的 X 服务器。您可以运行多个 Xnest 实例，并像使用普通 X 服务器一样使用它提供的每个 X 服务器。例如，要使用 Xnest 创建第二个 X 服务器，请执行以下命令：

```
Xnest :1 &
```

同样，要使用 Xnest 创建第三个 X 服务器，请执行以下命令：

```
Xnest :2 &
```

要创建第二个 X 服务器并用它登录到指定主机，请执行如下形式的命令：

```
Xnest -query server :1 &
```

其中 server 是您想要登录的主机的主机名或 IP 地址。同样，您可以使用 Xnest 登录到任意主机或获取选择器：

```
Xnest -broadcast :1 &      # 登录到本地网络上的任何主机
Xnest -indirect server :1 &   # 通过 server 提供的选择器登录
```

除非 Xnest 系统和远程系统安装了完全相同的字体，否则 Xnest 将运行失败。这大大限制了 Xnest 的适用性。

现在完成练习 28.3 和 28.4，以获得使用 Xnest 的经验。

## 练习 28.3
### 使用 Xnest

Xnest 的一个常见用途是在单台主机上运行多个 X 服务器。执行以下步骤来尝试此类配置：

- 1. 启动一个 X 会话，然后使用 Xnest 在同一主机上创建第二个 X 服务器。
- 2. 启动一个使用第二个 X 服务器的 X 客户端（例如 eyes）。

您可以参考本书和其他文档来帮助完成此练习。但在参加 RHCE 考试之前，请确保您能够在没有帮助的情况下配置 Xnest。

## 练习 28.4
### 运行多个窗口管理器

Xnest 的另一个常见用途是在单台主机上运行多个桌面管理器。请尝试通过使用 Xnest 在单台主机上同时运行 GNOME 和 KDE 来亲身体验。

## X 字体服务器

默认情况下，每个配置运行 Red Hat Linux 的系统都运行自己的 X 字体服务器副本 `xfs`，它提供对本地存储字体的访问，包括 True Type 字体。不过，如果您愿意，可以将系统重新配置为访问远程 X 字体服务器。

为此，请修改每个客户端系统的 `/etc/X11/XF86Config` 文件中的 `FontPath` 指令。默认情况下，该指令的形式为：

```
FontPath "unix/:/-1"
```



要访问远程字体服务器，请将指令修改为以下形式：

```
Font Path "tcp/server:7100"
```

其中 `server` 是运行字体服务器的主机名或 IP 地址。您还必须修改 `/etc/rc.d/init.d/xfs` 文件。将这一行

```
daemon xfs -droppriv -daemon -port -1
```

改为

```
daemon xfs -droppriv -daemon -port 7100
```

![](img/4eef9c6f2f52b608eba628cf4e2793ce_696_0.png)

默认情况下，X 字体服务器监听 7100 端口。不过，如果您愿意，也可以分配另一个端口。为此，请修改字体服务器配置文件 `/etc/X11/fs/config` 以及字体服务器 SysVinit 文件 `/etc/rc.d/init.d/xfs`。详情请参阅 xfs 手册页。

现在，通过完成练习 28.5 来配置一个远程字体服务器。

### 练习 28.5：配置客户端使用远程 X 字体服务器

为了测试您对 xfs 的理解，请配置一个客户端主机以使用运行在远程服务器上的 X 字体服务器。

您可以参考本书和其他文档来帮助您完成此练习。但在参加 RHCE 考试之前，请确保您能够在没有帮助的情况下配置远程 X 字体服务器。

## 本章小结

在本章中，您学习了如何配置和使用远程 X 服务器和客户端。涵盖的最重要主题包括：

- **X 安全性**：X 实现了一个简单的基于主机的安全系统。您可以使用 `xhost` 命令配置哪些主机被允许访问 X 服务器。
- **远程 X 客户端**：`DISPLAY` 环境变量指定了 X 服务器，它可以驻留在远程主机上。
- **远程 X 登录**：您可以通过几种方式通过 X 登录到远程主机：
    - 您可以指定登录主机的主机名或 IP 地址。
    - 您可以向本地网络广播一条消息，并登录到第一个响应的主机。
    - 您可以查询一个配置了提供 chooser（选择器）的主机，它可以让您从登录主机菜单中进行选择。
- **Xnest 程序**：`Xnest` 程序允许您运行一个与窗口（而非视频适配器）相关联的 X 服务器。`Xnest` 让您可以在仅有一个视频适配器的系统上运行多个 X 服务器。
- **X 字体服务器**：X 可以从本地硬盘或通过网络访问的字体服务器获取字体。X 配置中的 `FontPath` 指令指定了 X 字体的来源。

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- chooser（选择器）
- font server（字体服务器）
- host-based security（基于主机的安全性）
- remote logins（远程登录）

## 附加信息来源

如果您想了解本章所呈现主题的更多信息，应查阅 X 的手册页，包括 `X`、`XF86Config`、`XFree86`、`xauth`、`xdm`、`xfs` 和 `xhost`。

## 复习题

1. 要禁用基于主机的 X 安全性，应执行以下哪个命令？
    A. `xhost +`
    B. `xhost -`
    C. `xhosts +`
    D. `xhosts -`

2. 以下哪个命令启动 xclock 客户端并在 server 的 display 0 上运行？
    A. `xclock -display server`
    B. `xclock -display server:0`
    C. `xclock -display server:0.0`
    D. `xclock -display server:0:0`

3. 要登录到主机 server 上的 X 服务器，应执行以下哪个命令？
    A. `X -broadcast server`
    B. `X -indirect server`
    C. `X -query server`
    D. `X server`

4. 要通过 chooser 登录到 X 服务器，应执行以下哪个命令？
    A. `X -broadcast server`
    B. `X -indirect server`
    C. `X -query server`
    D. `X server`

5. 要使用 Xnest 创建第二个 X 服务器，应执行以下哪个命令？
    A. `Xnest &`
    B. `Xnest :0 &`
    C. `Xnest :1 &`
    D. `Xnest :2 &`

6. 要指定主机应访问主机 server 上的 X 字体服务器而非本地字体服务器，应指定哪个指令？
    A. `FontPath tcp/server`
    B. `FontPath tcp/server:5100`
    C. `FontPath tcp/server:7100`
    D. `FontPath tcp/server:9100`

## 复习题答案

1. A. `xhost +` 命令允许任何主机访问 X 服务器。

2. A, B, C. display 参数的语法为 `server:m.n`，其中 `server` 是服务器的主机名或 IP 地址，`m` 是显示器编号（默认为 0），`n` 是屏幕编号（默认为 0）。

3. C. `-query` 选项允许您指定登录主机。

4. B. `-indirect` 选项请求指定的主机提供一个 chooser。

5. C. 第一个服务器与 display 0 相关联；因此，第二个服务器与 display 1 相关联。

6. C. 默认情况下，X 字体服务器监听 7100 端口。

# 第六部分：网络管理

# 第 29 章：配置 Linux 路由器

### 本章涵盖的 RHCE 准备主题：

- 熟悉将 Red Hat Linux 用作路由器相关的配置问题，包括路由选项、IP 转发和内核配置。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_703_0.png)

Red Hat Linux 不仅可以作为服务器或工作站，还是一个功能强大的路由器。Red Hat Linux 与路由器相关的功能包括：

- 支持 WAN 协议，如 X.25、帧中继 (frame relay) 和 PPP
- 支持 LAN 功能，如 IP 转发、防火墙和伪装 (masquerading)
- 高级路由能力，如服务质量 (QoS)、基于策略的路由和透明代理

本章将讲解路由功能和静态路由的配置。对动态路由的概念性理解足以应对 RHCE 考试。

## 路由基础

只有具有多个网络地址的主机才能执行路由。最基本的路由操作是转发，即将从一个网络接口接收到的数据包转发到另一个网络接口。路由是根据数据包源地址、数据包目的地址和其他相关信息转发数据包的过程。路由 (route) 是数据包采取的路径。路由器 (router) 是执行路由的主机或设备。Red Hat Linux 主机既可以作为专用路由器，也可以在作为服务器或工作站的同时执行路由功能。图 29.1 显示了一个典型的路由器配置，它将从一个网络接口进入的数据包路由到两个网络接口中的一个。路由器经常以这种方式用于连接网络和子网络。

**图 29.1 数据包转发与路由**
![](img/4eef9c6f2f52b608eba628cf4e2793ce_704_0.png)

Red Hat Linux 可以执行*静态路由*和*动态路由*。在静态路由中，支配数据包路径的规则是固定的，只能手动调整。在动态路由中，规则会自动调整。具有动态路由功能的网络在某个或多个网络组件失效时，有时仍能继续运行；其余组件会自动调整其路由规则以绕过失效组件。当然，如果连接到给定主机的唯一连接失效，则无法访问该主机。因此，动态路由网络通常具有冗余路由的主机和网络；如果一条路由失效，路由规则可以调整为使用剩余的可操作路由。

### 静态路由

静态路由比动态路由更容易配置和使用。大多数拥有几十台主机的小型网络都配置为使用静态路由。要设置静态路由，您必须启用 IP 转发并正确配置路由表。此外，必须配置内核以支持所需的路由选项。标准 Red Hat Linux 内核支持最常用的路由选项。不过，您可以选择重新编译内核以启用额外的选项或禁用不需要的选项。

### IP 转发

除非您启用 IP 转发，否则主机不会转发 IP 数据包。可能的结果是网络操作失败并显示消息 "host unreachable"（主机不可达）。

您可以通过几种方式启用 IP 转发。最简单的方法是使用 `linuxconf`（或 `netconf`）。从 `linuxconf` 菜单中选择 Config $\Rightarrow$ Networking $\Rightarrow$ Client Tasks $\Rightarrow$ Routing and Gateways $\Rightarrow$ Defaults。此时将出现图 29.2 所示的 Routing Defaults 屏幕。要启用 IP 转发，请点击 Enable Routing 按钮，然后点击 Accept 按钮。

**图 29.2 Routing Defaults 屏幕**
![](img/4eef9c6f2f52b608eba628cf4e2793ce_705_0.png)

> **警告** 在 Red Hat Linux 6.2 的早期版本中，`linuxconf` 不能正确更新 `/etc/sysctl.conf` 文件。因此，在这些版本中，您不能使用 `linuxconf` 来启用数据包转发。

如果您愿意，可以通过编辑 `/etc/sysctl.conf` 文件并添加以下行来启用 IP 转发：

```
net.ipv4.ip_forward=1
```



另一种启用 IP 转发的方法是操作 /proc 文件系统。执行以下命令：

```
echo "1" >/proc/sys/net/ipv4/ip_forward
```

这种方法的缺点是，每次重启系统后，您都必须重新执行该命令。

## 路由配置

配置路由需要使用 `route` 命令，该命令包含在标准安装过程中自动安装的 `net-tools` 软件包中。您可以直接使用 `route` 命令；但许多 Red Hat Linux 系统管理员更倾向于使用 `linuxconf` 来配置路由，后者会根据您在对话框中提供的信息来调用 `route`。

从概念上讲，路由配置由一张包含路由规则的表组成。每条规则包含两个或三个组件：

- 目标 IP 地址，可以是指向一台主机、一个子网或一个网络。
- 接口，是指向一个网络适配器。
- 可选的网关 IP 地址，是指向一台将数据包路由到指定目标的主机、子网或网络的路由器（主机）。如果省略网关 IP 地址，则假设目标 IP 地址可以通过指定的接口直接访问。

> PPP 和 SLIP 设备始终充当网关。对于可通过 PPP 或 SLIP 访问的目标，您不需要（也不应该）指定网关地址。

### 使用 linuxconf 指定路由规则

若要使用 `linuxconf` 指定访问网络的路由规则，请从 `linuxconf` 菜单中选择 配置 (Config) $\Rightarrow$ 网络 (Networking) $\Rightarrow$ 客户端任务 (Client Tasks) $\Rightarrow$ 路由与网关 (Routing and Gateways) $\Rightarrow$ 网络其他路由 (Other Routes to Networks)。随后将出现如图 29.3 所示的“网络其他路由”屏幕。请指定目标 IP 地址以及（可选的）网络掩码。同时指定本地网络中提供该网络访问权限的网关主机的 IP 地址。

#### 图 29.3 “网络其他路由”屏幕

![](img/4eef9c6f2f52b608eba628cf4e2793ce_707_0.png)

您也可以通过类似的方法指定访问主机的路由规则。从 linuxconf 菜单中选择 配置 (Config) $\triangleright$ 网络 (Networking) $\triangleright$ 客户端任务 (Client Tasks) $\triangleright$ 路由与网关 (Routing and Gateways) $\triangleright$ 主机其他路由 (Other Routes to Hosts)。除非某个主机是该网络中您唯一想要访问的主机，否则通常指定一条网络路由规则比为该网络中的每台主机分别指定路由规则更为方便。

> 文件 /etc/sysconfig/static-routes 存储了通过 linuxconf 输入的网络和主机路由。如果您愿意，可以直接编辑此文件。

### 使用 route 指定路由规则

您可以直接使用 `route` 命令而不是使用 linuxconf 来建立路由规则。然而，当您重启系统时，必须重新建立使用 `route` 创建的路由规则。因此，通常使用 linuxconf 会方便得多。

若要使用 `route` 指定网络路由规则，请执行如下格式的命令：

```
route add -net ip_address netmask mask_address interface
```

其中 *ip_address* 是网络的 IP 地址，*mask_address* 是网络的网络掩码地址，*interface* 是用于访问该网络的网络设备。例如，执行以下命令：

```
route add -net 192.168.1.0 netmask 255.255.255.0 eth0
```

会为网络 192.168.1.0 添加一条路由规则，该网络可通过接口 eth0 访问。若要指定主机路由规则，请执行如下格式的命令：

```
route add -host ip_address interface
```

其中 *ip_address* 是主机的 IP 地址，*interface* 是用于访问该主机的网络设备。

#### 禁用动态路由

在使用静态路由时，您应该禁用 routed 守护进程。为此，启动 `linuxconf` 并从 `linuxconf` 菜单中选择 配置 (Config) $\triangleright$ 网络 (Networking) $\triangleright$ 客户端任务 (Client Tasks) $\triangleright$ 路由与网关 (Routing and Gateways) $\triangleright$ Routed 守护进程 (The Routed Daemon)。随后将出现如图 29.4 所示的“Routed 守护进程”屏幕。点击“不导出任何路由（静默）”(Does Not Export Any Routes (Silent)) 按钮，然后点击“接受”(Accept) 按钮。

#### 图 29.4 “Routed 守护进程”屏幕

![](img/4eef9c6f2f52b608eba628cf4e2793ce_708_0.png)

## 网络示例

图 29.5 显示了一个示例网络，该网络由两个通过路由器相互连接并连接到互联网的子网组成。与该示例网络对应的 `route` 命令为：

```
route add -net 192.168.1.0 netmask 255.255.255.0 eth0
route add -net 192.168.100.0 netmask 255.255.255.0 eth1
route add -net 1.1.1.0 netmask 255.255.255.0 eth2
route add default gw 10.1.1.2 eth2
```

![](img/4eef9c6f2f52b608eba628cf4e2793ce_709_0.png)

如果您在不带参数的情况下执行 `route` 命令，它将报告当前的路由规则。以下是与示例网络对应的输出：

**内核 IP 路由表 (Kernel IP routing table)**

| 目标 (Destination) | 网关 (Gateway) | 通用掩码 (Genmask) | 标志 (Flags) | 度量 (Metric) | 引用 (Ref) | 使用接口 (Use Iface) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 192.168.1.1 | * | 255.255.255.255 | UH | 0 | 0 | eth0 |
| 192.168.100.1 | * | 255.255.255.255 | UH | 0 | 0 | eth1 |
| 10.1.1.1 | * | 255.255.255.255 | UH | 0 | 0 | eth2 |
| 192.168.1.0 | * | 255.255.255.0 | U | 0 | 0 | eth0 |
| 192.168.100.0 | * | 255.255.255.0 | U | 0 | 0 | eth1 |
| default | router | 0.0.0.0 | UG | 0 | 0 | eth2 |
| 127.0.0.0 | * | 255.0.0.0 | U | 0 | 0 | lo |

`Flags` 字段可以包含如下值：

- U，表示网络链路已启动 (up)
- H，表示目标地址是指向一台主机而非一个网络
- G，表示该路由规则指定了一个网关

除非使用动态路由，否则 `Metric`、`Ref` 和 `Use` 字段无关紧要。

现在完成练习 29.1，以获得网络配置的实际操作经验。

### 练习 29.1：网络配置

如果您可以使用三台连接到网络的计算机，请将其中一台配置为将另外两台主机连接在一起的路由器。然后，尝试使用 `linuxconf` 和 `route` 指定各种路由规则，直到您能够熟练地操作路由表。

完成此练习时，请参考本章和其他资源。但在参加 RHCE 考试时，请准备好在没有帮助的情况下执行类似操作。

## 内核配置

Linux 内核提供了多种与网络相关的选项。您可以在图 29.6 中看到其中大部分选项，该图显示了包含网络相关选项的 `make menuconfig` 页面的顶部部分。表 29.1 总结了最重要的选项。有两个特别重要的选项可将 Red Hat Linux 优化为路由器使用：`IP: advanced router` 和 `IP: optimize as router not host`（后者在图 29.6 中不可见）。如果 Linux 系统主要或专门用作路由器，您应该指定这些选项并重新编译其内核。

#### 图 29.6 内核网络选项

![](img/4eef9c6f2f52b608eba628cf4e2793ce_711_0.png)

#### 表 29.1 内核网络选项

| 典型值 | 选项 | 描述 |
|---|---|---|
| Y/N | IP: advanced router | 如果主机主要用作路由器，请指定为 Y。 |
| Y | IP: aliasing support | 包含为单个网络接口分配多个 IP 地址的支持；通常用于支持多宿主 (multihosting)、虚拟域或虚拟主机。 |
| N | IP: ARP daemon support | 包含对用户空间 ARP 守护进程的支持，该进程可以维护足够大的表以处理非常大型的交换网络（超过几百台主机）。 |
| M | IP: autofw masquerade support | 包含对缺乏自身协议辅助程序的协议进行伪装 (masquerading) 的支持。 |
| Y/N | IP: broadcast GRE over IP | 包含使用通用路由封装 (GRE) 构建广播广域网 (WAN) 的支持，其运行方式类似于普通的局域网 (LAN)。 |
| Y | IP: firewall packet netlink device | 包含允许您创建字符设备文件的支持，该文件接收匹配指定标准的数据包副本；用于监控网络流量并检测可能的攻击。 |
| Y | IP: firewalling | 包含内核对防火墙和伪装的支持。 |
| M | IP: GRE tunnels over IP | 包含对 GRE 的支持，允许在 IPv4 之上封装 IPv4 和 IPv6 数据包。此支持比 `IP: tunneling` 选项与 Cisco 路由器的兼容性更好。 |
| Y | IP: ICMP masquerading | 包含支持防火墙将源自本地网络并目的地为远程主机的 ICMP 数据包进行转换，使其看起来像是源自防火墙主机。例如，用于允许只有私有 IP 地址的主机访问互联网。 |



## 表 29.1 内核网络选项（续）

| 典型值 | 选项 | 描述 |
| :--- | :--- | :--- |
| M | IP: ipmarkfw masquerade support | 包含对防火墙标记转发（Firewall Mark Forwarding）的支持，这是一种类似于端口转发的功能。 |
| N | IP: kernel level autoconfiguration | 在内核启动期间启用网络接口 IP 地址和路由表的自动配置；用于支持通过网络启动的无盘主机。 |
| Y | IP: masquerading | 包含支持使防火墙能够将源自本地网络并目的地为远程主机的 UDP 和 TCP 数据包进行转换，使其看起来像是源自防火墙主机。例如，用于允许仅具有私有 IP 地址的主机访问 Internet。 |
| Y | IP: masquerading special modules support | 包含对能够修改伪装规则的模块的支持；被 ipautofw 等模块以及端口转发所使用。 |
| M | IP: masquerading virtual server support | 包含允许您构建由两个或更多真实服务器组成的虚拟服务器的支持。 |
| 12 | IP: masquerading VS table size | 指定用于管理活动连接的哈希表的大小；实际表大小为 2^n，其中 n 为指定的值。 |
| N | IP: multicast routing | 包含对组播 IP 数据包（即具有多个目的地址的数据包）路由的支持。 |
| N | IP: Multicasting | 包含将数据包发送到多台计算机的支持——例如，被连接到 MBONE（高速视音频网络）的主机使用。 |
| Y/N | IP: optimize as router not host | 禁用那些能提高主机性能但会降低路由器性能的复制和校验和操作支持。 |
| Y | IP: TCP syncookie support | 包含用于防御 SYN 洪水拒绝服务攻击的 cookie 支持。 |
| Y | IP: transparent proxying | 包含支持使防火墙能够将源自本地网络并目的地为远程主机的数据包重定向到本地服务器（透明代理服务器）。 |
| M | IP: tunneling | 包含支持将一种协议的数据包封装在另一种协议的数据包之中的功能。 |
| M | IP: ipportfw masquerade support | 包含对端口转发的支持，允许您将源自本地网络外部并目的地为防火墙主机指定端口的数据包转发到本地网络上主机的指定端口。 |
| M | IPVS: round-robin scheduling | 指定虚拟服务器将使用轮询调度。 |
| M | IPVS: weighted least-connection scheduling | 指定虚拟服务器将使用加权最小连接调度。 |
| M | IPVS: weighted round-robin scheduling | 指定虚拟服务器将使用加权轮询调度。 |
| Y | Kernel/User netlink socket | 包含通过字符设备特殊文件在内核和用户进程之间进行通信的支持。 |
| Y | Netlink device emulation | 一项很快将被删除的向后兼容功能。 |
| Y | Network firewalls | 包含基于数据包过滤的防火墙和伪装支持。 |
| Y | Packet socket | 包含对数据包协议的支持，该协议被 tcpdump 等程序用于直接与网络设备通信。 |
| Y | Routing messages | 包含对特殊文件 `/dev/route` 的支持，允许您读取网络相关信息。 |
| Y | Socket filtering | 包含允许用户程序过滤数据包（除 TCP 数据包外）的支持。 |
| Y | TCP/IP networking | 包含对 TCP/IP 协议的支持。 |
| Y | Unix domain sockets | 包含对 Unix 域套接字的支持，即使是未连接到网络的主机也会使用。 |

## 动态路由

Red Hat Linux 提供了两个支持动态路由的守护进程。如果您需要动态路由，应该安装并配置其中之一。`routed` 守护进程通过路由信息协议 (RIP) 提供基本的动态路由。功能更强大的 `gated` 守护进程支持多种路由协议，例如：

- RIP 和 RIP-2
- 中继系统到中继系统 (IS-IS)
- 开放最短路径优先 (OSPF-2)
- 外部网关协议 (EGP)
- 边界网关协议 (BGP-4)

RIP、IS-IS 和 OSPF-2 是 *内部路由协议*，适用于在单个网络或一组自治网络内部使用。RIP 是一种 *距离矢量路由协议*，它仅将其路由表告知邻居。IS-IS 和 OSPF-2 是 *链路状态路由协议*，这类协议要求每个路由主机维护一份网络地图。当网络链路状态发生变化时，广播消息会通知路由器。RIP 适用于管理局域网 (LAN)；OSPF-2 适用于管理大型网络。

EGP 和 BGP-4 是 *外部路由协议*，适用于在自治网络之间使用。特别是 BGP-4（一种距离矢量协议）是 Internet 上使用的协议，因此被 ISP 广泛使用。EGP 是一个相当古老的协议，已不再流行。

表 29.2 总结了这些协议。

### 表 29.2 Red Hat Linux 支持的路由协议

| 协议 | 内部/外部 | 类型 |
|---|---|---|
| BGP-4 | 外部 | 距离矢量 |
| EGP | 外部 | 距离矢量 |
| IS-IS | 内部 | 链路状态 |
| OSPF-2 | 内部 | 链路状态 |
| RIP, RIP-2 | 内部 | 距离矢量 |

## 小结

在本章中，您学习了如何配置 Linux 路由器。涵盖的最重要主题包括：

**路由 (Routing)** 路由将数据包从一个网络主机转发到另一个主机。最基本的路由操作是转发，它接收从一个网络接口进入的数据包，并通过正确的网络接口将其重新发送。要启用路由，请使用 `linuxconf` 设置 IP 转发网络配置选项。

**路由表 (The Routing Table)** Linux 内核维护一张路由表，其中指定了每个本地接口的网络地址，以及可通过该接口访问的网络和主机。

**静态路由与动态路由 (Static and Dynamic Routing)** 在静态路由中，路由表由人工建立和维护。在动态路由中，路由表会自动更新以适应变化的情况（例如设备故障）。

**配置路由 (Configuring Routing)** 路由可以通过 `/etc/rc.netconf` 或通过 `ifconfig` 和 `route` 命令进行配置。

**配置路由的内核选项 (Configuring Kernel Options for Routing)** Linux 内核支持多种路由选项。要将系统配置为路由器而非服务器或工作站，请启用内核选项 `IP: advanced router` 和 `IP: optimize as router not host`。

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- 距离矢量路由协议 (distance-vector routing protocol)
- 动态路由 (dynamic routing)
- 外部路由协议 (exterior routing protocols)
- 转发 (forwarding)
- 内部路由协议 (interior routing protocol)
- 链路状态路由协议 (link-state routing protocol)
- 路由 (route)
- 路由器 (router)
- 路由 (routing)
- 静态路由 (static routing)

## 其他信息来源

如果您想了解本章所述主题的更多信息，请参考以下来源：

- David Ranch 和 Ambrose Au 编写的 *Linux IP Masquerade HOWTO*，`members.home.net/ipmasq`
- *Linux IP Masquerade Resource*，`ipmasq.cjb.net`
- Terry Dawson 和 Alessandro Rubini 编写的 *NET-3-HOWTO*，`/usr/doc/HOWTO/NET-3-HOWTO`
- Daniel Lopez Ridruejo 编写的 *Linux Networking Overview HOWTO*，`/usr/doc/HOWTO/Networking-Overview-HOWTO`
- `ifconfig`、`netstat` 和 `route` 的 man 手册页
- Craig Hunt 编写的 *Linux Network Servers 24seven* (Sybex, 1999)

## 复习题

1. 关于配置为 IP 路由器的 Red Hat Linux 主机，以下哪项是正确的？
   A. 该主机既可以作为服务器或工作站，也可以作为路由器。
   B. 该主机转发数据包。
   C. 该主机拥有多个 IP 地址。
   D. 该主机执行动态路由。

2. 以下哪项必须是每条路由规则的一部分？
   A. 目的 IP 地址
   B. 网关 IP 地址
   C. 源 IP 地址
   D. 一个接口

3. 以下哪个命令可以建立网络路由？
   A. `route add -host 192.168.100.0 \ 
      netmask 255.255.255.0 eth0`
   B. `route add -net 192.168.100.0 \ 
      netmask 255.255.255.0 eth0`
   C. `route -add host 192.168.100.0 \ 
      netmask 255.255.255.0 eth0`
   D. `route -add net 192.168.100.0 \ 
      netmask 255.255.255.0 eth0`



4. 如果一台主机主要被用作路由器，以下哪个内核选项可能会有所帮助？

- A. IP: advanced router
- B. IP: no host
- C. IP: optimize as router not host
- D. IP: router

5. 作为路由器运行需要以下哪些选项？

- A. IP: advanced router
- B. IP: firewalling
- C. TCP/IP networking
- D. Unix domain sockets

6. 以下哪些是链路状态协议？

- A. BGP-4
- B. IS-IS
- C. OSPF-2
- D. RIP

## 复习题答案

1. A, B, C. 路由器必须能够转发数据包，并且除了执行路由功能外，还可以充当服务器或工作站。为了转发数据包，主机必须拥有多个 IP 地址。主机可以执行静态路由而非动态路由。

2. A, D. 路由规则永远不包含源 IP 地址。路由规则可以包含（但不需要包含）网关地址。

3. B. `-net` 参数指定该规则是网络规则而非主机规则。`add` 标志必须指定为 `add` 而非 `-add`。

4. A, C. `IP: no host` 和 `IP: router` 选项并不存在。

5. C, D. `IP: advanced router` 和 `IP: firewalling` 选项虽然经常有用，但并非必须。除非启用 `TCP/IP networking` 选项，否则主机无法连接到 IP 网络。除非启用 `Unix domain sockets` 选项，否则主机——即使是不连接到网络的主机——也无法执行诸如日志记录等基本功能。

6. B, C. RIP 和 BGP-4 是距离向量协议。

# 第 30 章：使用 *ipchains* 配置防火墙

### 本章涵盖的 RHCE 准备主题：

- 能够使用 ipchains 实现基础的防火墙策略。

![](img/4eef9c6f2f52b608eba628cf4e2793ce_723_0.png)

第 25 章“管理安全”描述了旨在保护系统免受未经授权使用的管理措施。除了这些在系统层面实施的保护措施外，大多数系统管理员还会采用在网络层面实施的额外措施。一种流行的措施是 *firewall*（防火墙），它过滤进出数据包，仅允许授权的数据包进入和离开网络。

许多站点购买专门的硬件单元来充当防火墙或防火墙/路由器。然而，Red Hat Linux 允许您在 PC 或其他 Red Hat Linux 支持的平台上配置一台路由器。本章将解释 Linux 防火墙的基本概念以及如何实现简单的防火墙。

## 防火墙概念

防火墙阻止未经授权的数据包进入或离开网络。Linux 内核 2.2 版本包含了对 `ipchains` 设施的支持，该设施可用于构建 IP 防火墙——即过滤 TCP/IP 数据包的防火墙。早期的某些 Linux 内核版本支持 `ipfwadm` 设施，这是一个灵活性较低且现已过时的设施。图 30.1 显示了一个典型的防火墙配置。在示例配置中，所有进入和离开受保护本地网络的数据包必须经过 Linux 防火墙。基于一组 *firewall rules*（防火墙规则），防火墙会拦截可疑且未经授权的数据包。

**图 30.1 典型的防火墙**

![](img/4eef9c6f2f52b608eba628cf4e2793ce_724_0.png)

为了支持防火墙，Linux 内核必须在编译时选择相应的选项：

- Network firewalls
- IP: firewalling
- /proc filesystem

标准 Red Hat Linux 内核支持这些选项。要确定内核是否支持必要的选项，请检查文件 /proc/net/ip_fwchains；如果该文件存在，则表示支持这些选项。

> 提示：某些防火墙文档指出必须配置内核选项 IP: always defragment。现在可以通过在 /etc/sysctl.conf 文件中包含 `net.ipv4.ip_always_defrag=1` 这一行来动态启用此选项。

## 伪装（Masquerading）

伪装与防火墙功能密切相关，Red Hat Linux 系统通常被配置为同时提供这两项功能。在伪装中，离开受保护网络的数据包会被重写，使其看起来像是源自防火墙主机。同样，从受保护网络外部到达的相关数据包会被防火墙主机重写，以指定实际的目标主机。伪装通常用于隐藏受保护网络内主机的身份。例如，网络内的主机可以被分配私有 IP 地址——如 192.168.1.0 C 类网络中的地址——但仍然可以访问包括互联网在内的外部网络。图 30.2 显示了一个典型的伪装防火墙。

**图 30.2 伪装防火墙**

![](img/4eef9c6f2f52b608eba628cf4e2793ce_725_0.png)

伪装 Linux 主机的内核除了需要支持防火墙的选项外，还应编译以下选项：

- IP: transparent proxy support
- IP: masquerading
- IP: masquerading special modules support
- IP: ipfortfw masq support

标准 Red Hat Linux 内核包含了这些选项。

## ipchains 设施

ipchains 设施允许您控制 IP 数据包在 Linux 内核中的传递过程。图 30.3 显示了内核数据包路径。

**图 30.3 内核数据包路径**

![](img/4eef9c6f2f52b608eba628cf4e2793ce_726_0.png)

`ipchains` 设施允许您指定可以拦截、分流或重写 IP 数据包的规则。这些规则可以根据以下内容区分数据包：

- 源主机或网络 IP 地址
- 源端口
- 目标主机或网络 IP 地址
- 目标端口
- 协议
- 连接类型 (SYN)

默认实现了三类过滤器，称为 *chains*（链）：

- 输入链（input chain），控制接收哪些数据包
- 输出链（output chain），控制发送哪些数据包
- 转发链（forward chain），控制将哪些数据包转发到另一个网络接口

## 使用 *ipchains* 实现防火墙

防火墙由三组 *ipchains packet filter*（ipchains 数据包过滤）规则组成，每组对应一个数据包链：input、output 和 forward。要使用 *ipchains* 设施实现防火墙，可以通过执行 *ipchains* 命令来指定过滤规则，其通用格式为：

```
ipchains command chain [rule] [target]
```

*command* 参数允许您：

- 向指定链添加规则
- 从指定链删除规则
- 从指定链删除所有规则
- 列出指定链中的规则
- 为指定链指定默认策略

例如，要列出与输入链相关的规则，请执行命令：

```
ipchains -L input
```

同样，要清除与输出链相关的规则，请执行命令：

```
ipchains -F input
```

表 30.1 总结了 `command` 参数可以指定的值。

**表 30.1 ipchains 命令**

| 命令 | 描述 |
| :--- | :--- |
| -A | 将指定的规则追加到指定链的末尾。 |
| -D | 从指定链中删除指定的规则。 |
| -L | 列出指定链中的规则。 |
| -F | 删除指定链中的所有规则。 |
| -P | 将指定链的默认策略设置为指定的目标。 |
| -h | 显示命令帮助。 |

表 30.2 总结了 `target` 参数可以指定的值。要指定输入链上数据包的默认策略为 DENY，请执行命令：

```
ipchains -P INPUT DENY
```

![](img/4eef9c6f2f52b608eba628cf4e2793ce_728_0.png)

将默认策略设置为 DENY 通常是一个良好的实践。如果一个数据包没有匹配到指定其他目标的规则，该数据包将被拒绝——也就是说，被丢弃。因此，规则集中的任何遗漏都会导致数据包被丢弃；数据包的丢弃很可能会被察觉，从而修复规则集。如果默认策略是 ACCEPT，规则集的遗漏将允许不恰当的数据包穿过防火墙，从而可能导致安全漏洞。

**表 30.2 ipchains 目标**

| 目标 | 描述 |
| :--- | :--- |
| ACCEPT | 允许数据包通过。 |
| DENY | 拒绝数据包，且不向发送者发送错误消息。 |



## 表 30.2 ipchains 目标（续）

| 目标 | 描述 |
| :--- | :--- |
| REJECT | 拒绝数据包并向发送者发送错误消息。 |
| MASQ | 出站数据包被重写，使其看起来像是来自防火墙主机。入站数据包则进行反向伪装——即重写为正确的目的主机。 |
| REDIRECT | 无论指定的数据包目的地如何，入站数据包都被重定向到一个端口。 |
| RETURN | 对于内置链，数据包使用该链的默认规则进行处理。对于用户定义链，数据包被发送回调用链。 |

表 30.3 总结了规则参数的形式。地址可以使用多种形式来指定。例如，您可以指定源主机 IP 地址：

```
-s 192.168.1.0
```

或者指定目的网络 IP 地址：

```
-d 192.168.1.0/24
```

`/24` 指定网络掩码由 24 位组成；因此，相关的网络地址是一个网络掩码为 255.255.255.0 的 C 类网络地址。

### 表 30.3 ipchains 规则

| 规则 | 描述 |
| :--- | :--- |
| -d address [port] | 指定目的 IP 地址，或地址和端口。 |
| -i interface | 指定接收输入数据包或发送输出数据包的接口。 |
| -j target | 指定目标操作。 |
| -p protocol | 指定协议（TCP, UDP, ICMP 或 ALL）。 |
| -s address [port] | 指定源 IP 地址，或地址和端口。 |
| -y | 指定 TCP SYN 数据包，用于与服务器发起连接。 |

您可以在地址中指定端口或端口范围。例如，规则

```
-d 192.168.1.0/24 25
```

指定发送到 192.168.1.0 网络上主机 25 端口（SMTP 端口）的数据包。更通用的规则

```
-d 192.168.1.0/24 0:1023
```

指定发送到 192.168.1.0 网络上主机任何特权端口的数据包。

规则中可以指定几个特殊值。例如，值 `any` 指代任何 IP 地址，值 `0/0` 同样如此。此外，您可以在规则前加上 `!` 来否定该规则的含义。例如，规则 `! -y` 指的是除 TCP SYN 数据包以外的数据包。

您可以组合多个规则来形成复合规则。例如，命令

```
ipchains -A input -d 192.168.1.0/24 -p UDP -j DENY
```

包含一条指向发往 192.168.1.0 网络主机的 UDP 数据包的规则；此外，它指定此类数据包应被丢弃。大多数 `ipchains` 规则包含一个 `-j` 参数，用于指定相关的目标操作。

如果匹配数据包的规则包含 `-l` 标志，`ipchains` 命令会记录数据包。日志条目的来源为 `kern`（指内核）且优先级为 `info`。因此，默认情况下，它们被发送到 `/var/log/messages`。有关 `ipchains` 命令的更多信息，请参阅其 man 页。有关 `ipchains` 防火墙的完整示例，请参阅下一节。

## 使用 ipchains 实现伪装（Masquerading）

伪装是网络地址转换 (NAT) 的一种形式，通常用于将私有 (RFC 1918) IP 地址转换为防火墙主机的地址，以便防火墙后的主机可以访问外部网络（包括 Internet）。

要使用 `ipchains` 指定伪装，请在 forward 链中添加一个或多个指定 `MASQ` 目标的条目。例如，假设 192.168.1.0/24 网络是一个受保护的本地网络，且接口 `eth2` 是该网络防火墙主机的外部接口——即连接到外部网络的接口。命令

```bash
ipchains -A forward -i eth2 -s 192.168.1.0/24 -j MASQ
```

建立了一条转发规则，用于伪装源自受保护网络 (192.168.1.0/24) 并在外部接口 (`eth2`) 上出现的数据包。

特殊的内核模块支持常用协议的伪装。您应该加载必要的模块，以便协议正常运行。这些模块及其相关协议是：

- `ip_masq_cuseeme` (CUSEEME)
- `ip_masq_ftp` (FTP)
- `ip_masq_irc` (IRC)
- `ip_masq_quake` (Quake)
- `ip_masq_raudio` (Real Audio)
- `ip_masq_vdolive` (VDO Live)

Red Hat 提供了一个示例防火墙服务脚本，您可以在 Web 上查看：www.redhat.com/support/docs/tips/firewall/firewallservice.html。该脚本根据 GNU 通用公共许可证的条款分发，因此您可以自由使用和重新分发。该脚本并不适用于每一种防火墙场景，但您可以将其作为创建自定义防火墙的起点。

## 保存和恢复 ipchains 规则

许多系统管理员会创建 `/etc/rc.d/rc.firewall` 脚本，用于执行 `ipchains` 命令和其他命令。通常，他们会修改 `/etc/rc.d/rc.local` 脚本来调用 `/etc/rc.d/rc.firewall`。这种实现防火墙的技术允许您在 `ipchains` 命令之间插入注释，使防火墙更容易理解和修改。

不过，如果您愿意，也可以使用 `ipchains-save` 和 `ipchains-restore` 命令来实现防火墙。`ipchains-save` 命令将当前的防火墙规则转储到 `stdout`，而 `ipchains-restore` 命令从 `stdin` 加载防火墙。通过将 `stdout` 重定向到文件，您可以让 `ipchains-save` 将当前防火墙规则转储到磁盘文件。Red Hat Linux 6.2 脚本 `/etc/rc.d/init.d/ipchains` 会测试名为 `/etc/sysconfig/ipchains` 的文件是否存在；如果文件存在，该脚本将对该文件运行 `ipchains-restore`。

现在尝试通过完成练习 30.1 来亲手构建一个防火墙。

**练习 30.1：构建一个基础防火墙**

配置一个简单的防火墙来伪装一个受保护的网络。仅允许 HTTP 和 FTP 流量流入和流出该受保护的网络。在受保护的网络内部，允许数据包无限制地流动。

在完成此练习时，您可以参考本书和其他帮助。但在参加 RHCE 考试之前，请确保您能够在不参考外部帮助的情况下构建一个基础防火墙。

## 总结

在本章中，您学习了如何使用 `ipchains` 构建防火墙。涵盖的最重要主题包括：

- **防火墙**：防火墙通过参考一组匹配未经授权数据包并指定其处理方式的规则，来拦截未经授权的数据包。

- **伪装（Masquerading）**：伪装是一种重写数据包的功能，使其看起来像是源自或目的地为指定主机。伪装有多种用途。最常见的一种是为被分配了私有 IP 地址的主机提供 Internet 访问。伪装还用于通过向外部隐藏网络结构来增强网络安全性。

- **`ipchains` 功能**：`ipchains` 功能允许您指定内核应用于其输入、输出和转发 TCP/IP 链上数据包的规则。该功能还允许您处理用户定义的链。`ipchains` 规则可以通过以下特征识别数据包：
    - 源主机或网络 IP 地址
    - 源端口
    - 目的主机或网络 IP 地址
    - 目的端口
    - 协议
    - 连接类型

匹配的数据包将按照规则指定的处理方式进行处理。可能的处理方式包括接受数据包、拦截数据包或将数据包重定向到指定端口。

- **保存和恢复防火墙配置**：`ipchains-save` 和 `ipchains-restore` 命令可用于将规则集保存到磁盘文件并从磁盘文件恢复规则集。然而，许多系统管理员更喜欢将 `ipchains` 规则编写为脚本文件，其中可以包含解释性注释，以便于理解和维护防火墙。

### 关键术语

在进入下一章之前，请确保您熟悉以下术语：

- chains（链）
- firewall（防火墙）
- firewall rules（防火墙规则）
- masquerading（伪装）
- packet filter（数据包过滤器）



## 附加信息来源

如果您想进一步了解本章介绍的主题，请参考以下资料：

- Mark Grennan 编写的 *Firewalling and Proxy Server HOWTO*，路径 `/usr/doc/HOWTO/Firewall-HOWTO`
- Paul Russell 编写的 *IPCHAINS HOWTO*，路径 `/usr/doc/HOWTO/IPCHAINS-HOWTO`
- Ambrose Au 和 David Ranch 编写的 *Linux IP Masquerade Mini HOWTO*，路径 `/usr/doc/HOWTO/mini/IP-Masquerade`
- `ipchains` 手册页

## 复习题

1. Red Hat Linux 的防火墙功能是通过哪个命令实现的？
    A. `firewall` 命令
    B. `ipchains` 命令
    C. `ipfwadm` 命令
    D. `ipportfw` 命令

2. 为了支持来自伪装网络（masqueraded network）的 FTP，您应该加载以下哪个模块？
    A. `ip_masq`
    B. `ip_masq_all`
    C. `ip_masq_ftp`
    D. `ip_masq_tcp`

3. 要列出与输入链（input chain）相关联的规则，您应该执行以下哪个命令？
    A. `ipchains -A input`
    B. `ipchains -F input`
    C. `ipchains -L input`
    D. `ipchains -P input`

4. 要清除与输出链（output chain）相关联的所有规则，您应该执行以下哪个命令？
    A. `ipchains -A output`
    B. `ipchains -F output`
    C. `ipchains -L output`
    D. `ipchains -P output`

5. 要拦截试图向 199.199.199.0/24 网络主机建立传入 TELNET 连接的数据包，应执行以下哪个 ipchains 命令？

- **A.** `ipchains -A forward -p tcp -d 199.199.199.0/24 23 -j DENY`
- **B.** `ipchains -A forward -p tcp ! -d 199.199.199.0/24 23 -j DENY`
- **C.** `ipchains -A input -p tcp -d 199.199.199.0/24 23 -j DENY`
- **D.** `ipchains -A input -p tcp ! -d 199.199.199.0/24 23 -j DENY`

6. 要丢弃数据包并向发送者发送错误消息，应指定哪个目标（target）？

- **A.** DENY
- **B.** REDIRECT
- **C.** REJECT
- **D.** RETURN

## 复习题答案

1. B. `ipfwadm` 命令在某些早期的 Linux 内核版本中受到支持。
2. C. 列出的其他模块名称均不对应实际模块。
3. C. `-L` 参数指示 `ipchains` 列出与指定链相关联的规则。
4. B. `-F` 参数指示 `ipchains` 刷新（清除）与指定链相关联的规则。
5. C. 此类数据包将位于输入链上，且目的地为 23 端口。
6. C. DENY 目标不发送错误消息；其余目标则不会丢弃数据包。

## RHCE 考试 (RH302)

## 第七部分

# 第 31 章：RHCE 考试

RHCE 考试并非易事：总体而言，大约三分之一的考生未能通过 RHCE 考试。因此，勤奋的准备和复习至关重要。本书的前几章已经介绍了您为准备 RHCE 考试所需的 Red Hat Linux 知识；本章则描述 RHCE 考试本身。虽然在本章中您不会学到关于 Red Hat Linux 的新知识，但本章非常重要。研究一贯表明，焦虑是决定考试表现的主要因素，没有理由认为 RHCE 考试是这个结论的例外。通过告诉您在 RHCE 考试中会遇到什么，本章将帮助您管理压力，从而帮助您获得最高分数。

## RHCE 考试

RHCE 考试分为三个部分：

- 选择题考试（1 小时）
- 服务器安装与网络服务配置考试（2.5 小时）
- 调试（Debug）考试（2.5 小时）

本节概括地描述 RHCE 考试，包括考试结构和考试协议。接下来的三个章节将详细描述考试的三个组成部分。

### RHCE 考试结构

RHCE 考试的三个部分 each 均按 100 分制评分。要通过考试，您必须总共获得 240 分，即每部分考试平均得 80 分。此外，您在每个部分考试中必须至少获得 50 分。

选择题考试类似于您在高中或大学参加的考试。您有一小时时间回答 40-50 个技术问题。有些题目可能需要判断正误；有些可能需要您从一组选项中识别出所有正确答案，或者从中选择最佳答案。

考试的其余两个部分是基于实际操作的，要求您安装、配置或排除实际系统的故障。如果您从未参加过实操考试，您可能会感到焦虑。然而，这种焦虑是没有必要的。与笔试不同，实操考试没有陷阱题。您将被要求执行系统管理员在工作中执行的同类系统管理任务。如果您具备必要的经验和专业知识，您就能掌控实操考试。

Red Hat, Inc. 表示，许多考生在选择题考试中得分很高，但在实操考试中表现不佳，从而导致考试失败。这使得一些人认为实操考试比选择题考试更难。情况可能确实如此。但也有可能，由于实操考试不熟悉的格式以及由较高失败率引起的忧虑，阻碍了学生的发挥。通过更多地了解 RHCE 考试，特别是其实操考试，您可以最大限度地减少考试焦虑，并增加通过考试的可能性。

### 考试协议

RHCE 考试大约需要七个小时。考试的三个部分总共需要六小时。另外一小时被分配为午休时间。

您应计划提前到达，以避免因交通等不可预见的情况而迟到。请携带至少两种身份证明，包括带有照片的身份证件。除此之外，请尽量少携带个人物品：在考试期间，您不允许使用除监考人员提供的材料以外的任何材料。您可以预期收到以下物品：

- 钢笔或铅笔
- 空白纸
- 一份保密协议

在相关考试部分开始前，您可以预期收到以下物品：

- 实操考试的任务分配单
- 调试考试的救援磁盘
- 服务器安装与网络服务配置考试的安装介质

您必须签署保密协议，在协议中您同意不泄露关于 RHCE 考试的信息；如果不签署，您将不被允许参加考试。

保密协议旨在维护考试过程的完整性。由于 RHCE 认证的价值在于准确评估考生的知识和技能，因此遵守保密协议的条款符合您以及 Red Hat, Inc. 的共同利益。

考场将配备 PC。监考人员将为您分配一台 PC，您将使用它参加考试。

考试有时间限制；正如监考人员将宣布的那样，在监考人员指示您开始之前，您不得打开材料或开始考试。

考试的三个部分将按监考人员选择的顺序进行。例如，监考人员可能会选择以下日程：

- 10:00 - 12:30 服务器安装与网络服务配置考试
- 12:30 - 1:30 午餐
- 1:30 - 2:30 选择题考试
- 2:30 - 5:00 调试考试

在考试期间，请勿与其他考生交流或尝试交流。如果您违反此项或监考人员解释的其他协议，您将立即被判定为考试失败。

### 选择题考试

选择题考试测试您对 Red Hat Linux、Linux 和 Unix 的知识。题目涵盖 Linux 命令、命令重定向和系统管理等主题。在考试期间，您不能查阅基于计算机的文档或其他资源，如笔记或书籍。您最多有一小时时间完成这项考试，其中包含约 50 道题。一道题可能要求您通过以下方式回答：

- 将该项分类为正确或错误
- 从一组选项中识别出正确答案
- 从一组选项中识别出最佳答案

请确保您清楚地理解每道题对应的正确回答方式。

在参加考试时，您可能会注意到一些本书或 RH300 课程（如果您参加了的话）中没有涉及的题目。请记住，考试的目的是认证一个人是否具备担任 Red Hat Linux 系统管理员的准备就绪程度。Red Hat, Inc. 对考试的描述故意保持概括和模糊，以避免将那些仅了解考试技巧但并不精通系统管理的人认证为 RHCE。与某些说法相反，考试中并没有充斥着陷阱题。相反，这是 Red Hat, Inc. 为了识别并认证具备 Red Hat Linux 系统管理技能的考生而做出的真诚努力。如果您具有适当的经验并勤奋准备，您应当能够通过考试。

以下是一些可以提高选择题得分的技巧：

- 如果您在回忆怀疑会出现在测试中的信息时遇到困难，请在考试前复习这些信息。在允许开始考试后，立即将您能回忆起的所有信息写在监考人员提供的空白纸上。然后，您可以在考试期间参考您的笔记。

为了避免被误认为作弊，您应该告知监考人员您打算以这种方式使用空白纸。确保对方清楚您没有将小抄偷带进考场。



- 请务必仔细阅读每个问题；你可能会发现将每个问题阅读两遍是非常值得的。
- 请务必阅读每一个选项。不要在看到第一个似乎正确的选项时就立即标记，因为另一个选项可能更好。这也许是所有考试提示中最重要的一个。
- 仔细阅读选项。像 *not*（不/非）这样的小词很容易被忽略，但它们会显著改变选项的含义。
- 迅速排除任何明显错误的选项，将注意力集中在剩余选项上，寻找最佳答案。
- 如果你不能自信地确定最佳选项，请记录下该题号并继续前进。在回答完简单的问题之前，不要在单个问题上浪费太多时间。
- 完成简单问题后，返回到你记录的问题上。运气好的话，其他某些问题可能唤醒了你的记忆，那些最初看起来困难的问题现在变得清晰了。然而，如果你仍然无法排除所有干扰项，请做出你的最佳猜测。

随本书附带的 CD-ROM 中的练习考试和奖金考试是准备多项选择题考试的绝佳资料。在参加 RHCE 考试之前，请务必完成练习考试和奖金考试；如果可能的话，请在接近 RHCE 考试条件的环境下进行。也就是说，给自己计时，并且不允许查阅笔记或其他帮助。

## 服务器安装与网络服务设置考试

这场时长 2.5 小时的“服务器安装与网络服务设置”考试要求你安装并配置一个满足一组给定要求的 Red Hat Linux 系统。本书中的许多练习都类似于你在服务器安装与网络服务设置考试中可能遇到的要求。例如，你可能会被要求：

- 安装 Red Hat Linux
- 编译并安装一个配置为支持特定选项的内核
- 设置用户账户
- 安装并配置网络服务，如 Apache、NFS 和 Samba
- 配置用户环境
- 建立限制对文件或服务访问的安全措施

监考人员将使用自动化脚本来验证你的工作，因此完整性和准确性对于获得高分至关重要。在服务器安装与网络服务设置考试中，你不应该期待会出现出格的难题或奇怪的要求。因此，你的得分将很大程度上取决于你对时间的利用以及对工作的仔细检查。

如果你能规划好工作，你可以预见到会有剩余的时间。在开始工作之前，花几分钟仔细阅读要求。然后决定：

- 哪些要求你认为容易满足，哪些要求你认为难以满足
- 你完成这些要求的顺序

很有可能，你会发现某些要求必须在开始其他工作之前完成。例如，在赋予用户指定的文件访问权限之前，你必须先建立用户账户。你可能会发现某些要求涉及耗时较长的任务，例如编译内核；在这些任务进行时，你可以尝试完成其他要求。

在阅读要求时，你可能会发现记录一些提醒事项很有用，这样在实现要求时能让你保持在正确轨道上。

一旦开始工作，不要在尝试满足一个困难的要求上陷入泥潭，除非完成它是在满足其他要求之前的前提条件。相反，记录下这个问题并继续满足剩余的要求。稍后，在时间允许的情况下，你可以回到那个困难的要求，解决问题并将其完成。

在服务器安装与网络服务设置考试期间，你将被允许自由访问 man 页和其他在线文档，因此请务必安装任何你认为可能有用的文档软件包。

每完成一项要求就将其勾掉，以免不小心遗漏。当你满足所有要求后，将剩余的规定时间用于检查和复核你的工作。在确认已正确完成每项要求之前，不要停止工作。

## 调试考试

与服务器安装与网络服务设置考试一样，调试考试是一场 2.5 小时的基于性能的考试。你会得到一系列 2-4 个练习，除非你首先识别并解决一个或多个系统配置问题，否则无法完成这些练习。例如，你可能会被要求将系统配置为启动到运行级别 5，但系统可能根本无法启动，或者 `/usr` 文件系统可能无法挂载。

当你完成一个练习时，监考人员将验证你的工作并为你提供下一个练习。你被要求记录解决练习时采取的步骤日志，并且在你的操作流程不清晰的情况下，应准备好解释你的步骤，以证明你已正确完成练习。

你被允许查阅安装在系统上的文档，但与考试的其他部分一样，你不能参考书籍或笔记。而且，你将被禁止通过重新安装软件包来修复问题。对于某些练习，你会获得一个系统救援磁盘。

调试考试可能是三场考试中压力最大的，因为你无法提前规划你的步骤。相反，你必须遵循一个区分“症状”和“问题”的解决流程：

- 识别症状。
- 发现导致症状的问题。
- 修复问题。
- 执行任何要求的配置更改。

以下是一个通用流程，你可以根据具体练习的需求进行调整，特别是那些涉及启动相关问题的练习：

1. 启动系统。如果系统无法正常启动，你可能需要以单用户模式或使用救援磁盘启动。
2. 挂载所需的文件系统。你可能需要检查 `/etc/fstab` 或使用 `fdisk` 检查分区表，以识别分区和文件系统。你可能需要运行 `fsck` 来检查或修复文件系统。
3. 根据需要执行修复并进行配置更改。
4. 为系统重启做准备。在重启之前，你可能需要重新安装 `lilo` 引导映射或 `umount` 文件系统。在某些情况下，你可能需要使用 `sync` 命令将输出缓冲区刷入磁盘。
5. 重启系统并检查你的工作。

在这场考试中保持冷静尤为重要。在监考人员的允许下，可以使用硬糖或其他放松辅助手段。如果系统运行不符合预期，请考虑你可利用的资源；发挥想象力，想办法绕过问题。

## 更多信息

有关 RHCE 考试的更多信息，请参阅 Red Hat, Inc. 网站 `www.redhat.com/services/training/training.html`。关于 RHCE 考试和 RHCE 认证的观点和评论，请参阅各种互联网新闻组和论坛，例如 `www.slashdot.org`。

# 附录 A

## 练习考试

1. 在单个硬盘上定义的分区最大数量是多少？
    A. 4
    B. 12
    C. 15
    D. 16

2. Linux 系统中必须存在以下哪个挂载点？
    A. /
    B. /boot
    C. /usr
    D. /var

3. 要打印文件数据，你应该输入哪个 Red Hat Linux 命令？
    A. lp data
    B. lpr data
    C. pr data
    D. print data

4. 要使环境变量 x 的值在直接本地环境之外可访问，你应该输入哪个命令？
    A. assign x
    B. export x
    C. global x
    D. import x

5. 哪个服务为 X Window 系统提供字体？
    A. xf
    B. xfonts
    C. xfontserver
    D. xfs

6. 以下哪个陈述适用于 IP 地址 192.168.0.1？
    A. 它可以被随意分配给私有网络上的主机。
    B. 它不能被分配给访问互联网的主机。
    C. 它是指定用于组播传输的。
    D. 它是预留地址。

7. 什么是 GNU 通用公共许可证 (GPL)？
    A. 一种版权形式
    B. 一种用于 copyleft 软件的机制
    C. 一种防止软件被复制的机制
    D. 一种防止软件被申请版权的机制

8. 以下哪些是 Linux 操作系统的组成部分？
    A. 最初由 Linus Torvalds 创建的内核
    B. GNU 工具和程序
    C. MINIX 工具和程序
    D. UNIX 工具和程序

9. 关于 Red Hat Linux 基于文本的安装过程，以下哪项是正确的？
    A. 对于初学者来说，它比图形安装过程更容易使用。
    B. 它比图形安装过程更快。
    C. 它比图形安装过程更可靠。
    D. 与图形安装过程相比，它需要的系统资源（如 RAM）更少。



10. 在具有 PCMCIA 网络适配器的系统上，从 CD-ROM 开始 Linux 安装需要以下哪个镜像文件？

**A.** autoboot.bat
**B.** boot.img
**C.** bootnet.img
**D.** pcmcia.img

11. 关于 MD5 密码，以下哪项是正确的？

**A.** 它们提高了系统安全性。
**B.** 它们构成了安全隐患。
**C.** 它们应该与 NIS 配合使用。
**D.** 它们不应与 NIS 配合使用。

12. 安装过程中用于配置 X 的程序是以下哪个？

**A.** Xcfg
**B.** Xconfig
**C.** Xconfigurator
**D.** Xconfiguration

13. 在具有 PCMCIA 网卡的计算机上，应如何从 CD-ROM 安装 Linux？

**A.** 您应该使用网络启动盘。
**B.** 您应该使用 PCMCIA 启动盘。
**C.** 您应该使用 PCMCIA 补充盘。
**D.** 您应该使用标准启动盘。

14. 必须如何执行 kickstart 安装？

**A.** 您必须使用网络启动盘启动。
**B.** 您必须使用 mkkickstart 创建脚本。
**C.** 您必须在启动提示符处指定 ks 参数。
**D.** 您必须将发行版介质存储在 FTP 服务器上。

15. 以下哪个运行级别对应于没有网络功能的多用户操作？

- A. 1
- B. 2
- C. 3
- D. 4

16. 以下哪个程序用于启用 MD5 密码加密？

- A. md5conv
- B. md5unconv
- C. pwconv
- D. 以上都不是

17. 以下哪个文件建立了用户的路径（path）？

- A. /etc/bashrc
- B. /etc/profile
- C. ~/.bashrc
- D. ~/.bash_profile

18. 哪些方法可以用于修改组会员身份？

- A. groupmod 命令
- B. linuxconf 命令
- C. useradd 命令
- D. userconf 命令

19. 以下哪个命令可以激活用户配额（quotas）？

**A.** quotaon -a
**B.** quotaon -ag
**C.** quotaon -au
**D.** quotaon -aug

20. 以下哪个操作应该首先执行？

**A.** 创建配额文件
**B.** 设置默认配额
**C.** 设置个人配额
**D.** 开启配额

21. 如果软件包 xyz 已经安装，以下哪个命令将替换该软件包？

**A.** rpm -i xyz
**B.** rpm -f xyz
**C.** rpm -F xyz
**D.** rpm -U xyz

22. 当您发出 `rpm -bb` 命令时，必须指定什么样的文件作为参数？

**A.** 二进制 RPM 文件
**B.** 软件包文件
**C.** SPEC 文件
**D.** TAR 文件

23. 与 Linux 内核 2.2 版本相关的模块可能存储在何处？

**A.** /lib/2.2.15
**B.** /lib/modules/2.2.15-2
**C.** /modules/2.2.15
**D.** /modules/2.2.15-2

24. 以下哪个文件可用于识别已安装的 PCI 设备？

**A.** /proc
**B.** /proc/ioports
**C.** /proc/devices
**D.** /proc/pci

25. 您应该发出以下哪个命令来重启 lpd 服务？

**A.** /etc/rc.d/init.d/lp restart
**B.** /etc/rc.d/init.d/lp start
**C.** /etc/rc.d/init.d/lpd restart
**D.** /etc/rc.d/init.d/lpd start

26. 您应该发出以下哪个命令来指定 gpm 服务应在运行级别 3 下执行？

**A.** chkconfig --level 3 gpm
**B.** chkconfig --level 3 gpm on
**C.** chkconfig --levels 3 gpm
**D.** chkconfig --levels 3 gpm on

27. 以下哪个命令将停止系统？

**A.** init 0
**B.** halt
**C.** shutdown -h now
**D.** telinit 0

28. 您应该发出以下哪个命令来告知 init 进程其配置文件已更改？

- A. init q
- B. init -q
- C. kill -HUP init
- D. killall -HUP init

29. 当您修改 `/etc/crontab` 文件时，以下哪项是正确的？

- A. cron 立即识别更改。
- B. 您必须立即重启系统。
- C. 您必须发出 touch 命令以更新 `/var/spool/cron` 目录的修改时间。
- D. 您必须重启 cron 系统。

30. 以下哪些 cron 任务每天执行一次？

- A. logrotate
- B. makewhatis
- C. rmmod
- D. slocate.cron

31. `/etc/conf.modules` 中的哪一行指定要保留默认模块路径信息？

- A. default-path
- B. hold
- C. keep
- D. retain

32. 以下哪个命令正确创建了用于系统启动期间的初始 ramdisk？

- A. mkinitrd /boot/initrd-version
- B. mkinitrd /boot/initrd-version version
- C. mkinitrd /boot/initrd-version.img
- D. mkinitrd /boot/initrd-version.img version

33. 以下哪个文件包含动态加载器的缓存？

- A. /etc/ld.so.cache
- B. /etc/ld.so.conf
- C. /lib/ld.so.cache
- D. /lib/ld.so.cache

34. 若要在没有初始进程的情况下以运行级别 1 启动系统，在启动提示符处应输入什么？

- A. linux
- B. linux emergency
- C. linux s
- D. linux single

35. 以下哪些是必须存在的 Apache 配置文件？

- A. access.conf
- B. httpd.conf
- C. modules.conf
- D. srm.conf

36. 以下哪个程序不具有 PAM 感知能力（not PAM-aware）？

- A. in.ftp
- B. in.rlogin
- C. in.telnetd
- D. login

37. 为了允许某个主机远程访问打印机，应在哪个文件中列出该主机？

- A. /etc/hosts
- B. /etc/hosts.equiv
- C. /etc/hosts.lpd
- D. /etc/printcap

38. 默认情况下，什么样的日志消息会被发送到 `/var/log/secure` 文件？

- A. alert
- B. auth
- C. authpriv
- D. emerg

39. 一个新创建的普通用户的默认组包含多少个成员？

- A. 1
- B. 2
- C. 4
- D. 8

40. 通常不应使用以下哪个 TCP 服务？

- A. finger
- B. identd
- C. netstat
- D. sysstat

41. 应该使用哪个标志来非交互式地调用 *Xconfigurator*？

- A. --auto
- B. --expert
- C. --kickstart
- D. --probe

42. 以下哪个程序可能会损坏显示器？

**A.** SuperProbe
**B.** xf86config
**C.** xinitrc
**D.** xvidtune

43. 使用 AnotherLevel 桌面环境时，指定用户窗口管理器的文件是以下哪个？

**A.** ~/.wm_style
**B.** ~/.wmanager
**C.** ~/.Xclients
**D.** ~/.Xsession

44. 以下哪个键序列通常用于从虚拟控制台切换到 X？

**A.** CTRL-ALT-F1
**B.** CTRL-ALT-F3
**C.** CTRL-ALT-F7
**D.** CTRL-ALT-F8

45. 以下哪个操作尝试登录到本地网络上的任意 X 服务器？

**A.** X -all
**B.** X -broadcast
**C.** X -indirect
**D.** X -query

46. 以下哪个指令配置 `xdm` 为任何请求主机提供一个包含 `server1` 和 `server2` 的选择器？

- A. `* CHOOSER server1 server2`
- B. `server1 server2 CHOOSER *`
- C. `ALL CHOOSER server1 server2`
- D. `server1 server2 CHOOSER ALL`

47. 以下哪些是禁用动态路由的方法？

- A. `echo "0" > /proc/sys/net/ipv4/dynamic_routing`
- B. 编辑 `/etc/sysconfig/network-scripts`
- C. `linuxconf` 的 Gated Daemon 界面
- D. `linuxconf` 的 Routed Daemon 界面

48. 以下哪个协议是一种流行的外部协议（exterior protocol）？

- A. BGP-4
- B. EGP
- C. OSPF-2
- D. RIP-2

49. 要支持伪装（masquerading），需要以下哪个内核选项？

- A. `IP: firewalling`
- B. `IP: masquerading`
- C. `IP: masquerading special modules support`
- D. `IP: transparent proxy support`

50. 以下哪个命令可用于伪装来自本地保护网络的数据包？

- A. `ipchains -A forward -i eth0 \ -s 192.168.1.0/24 -j MASQ`
- B. `ipchains -A input -i eth0 \ -s 192.168.1.0/24 -j MASQ`
- C. `ipchains -A local -i eth0 \ -s 192.168.1.0/24 -j MASQ`
- D. `ipchains -A output -i eth0 \ -s 192.168.1.0/24 -j MASQ`

## 模拟考试答案

- 1. D. 一个硬盘可以有 4 个主分区和 12 个逻辑分区。然而，只有 3 个主分区和 12 个逻辑分区可以存放文件系统。更多信息请参阅第 2 章。

- 2. A. 如果硬盘容量较小、`/` 分区较小或系统 BIOS 不受寻址限制，则不需要 `/boot` 分区。`/usr` 和 `/var` 分区永远不是必需的。更多信息请参阅第 2 章。

- 3. B. Red Hat Linux 打印文件的命令是 `lpr`。更多详情请参阅第 3 章。

- 4. B. `export` 命令将环境变量标记为在本地环境之外可访问。更多详情请参阅第 3 章。

- 5. D. X 字体服务器名为 `xfs`。更多信息请参阅第 4 章。

- 6. A. 您可以将此 IP 地址分配给私有网络上的主机，并使用网络地址转换（NAT）使该主机能够访问 Internet。更多信息请参阅第 4 章。

- 7. A, B. GPL 是一种版权形式——称为 copyleft——它保证了使用、修改、复制和重新分发软件的权利。更多信息请参阅第 5 章。

- 8. A, B. Linux（有时称为 GNU/Linux）是 Torvalds 的内核与 GNU 工具和程序的结合。更多信息请参阅第 5 章。

- 9. B, C, D. 图形安装过程通常对初学者来说更容易使用，但它需要更多资源，因此运行速度可能不如基于文本的安装过程，尤其是在 RAM 有限的系统上。基于文本的安装过程更有可能从问题中恢复，且所需的系统资源较少。更多信息请参阅第 6 章。

- 10. B. `boot.img` 文件包含一个适用于从 CD-ROM 盘或包含安装文件的本地硬盘分区进行安装的镜像。仅在安装期间使用 PCMCIA 设备时才需要 `pcmcia.img` 文件中的镜像。更多信息请参阅第 6 章。



11. A, C. MD5 密码提高了安全性，通常应当使用。更多信息请参阅第 7 章。

12. C. 安装程序使用 `Xconfigurator` 来配置 X。更多信息请参阅第 7 章。

13. D. 仅在安装过程中访问 PCMCIA 设备时才需要 PCMCIA 启动盘。PCMCIA 补充盘已不再存在。更多信息请参阅第 8 章。

14. C. 只要 `ks.cfg` 文件和发行版介质位于本地设备上，您就可以使用标准启动盘进行启动。您可以手动创建 kickstart 脚本。您不能使用 FTP 服务器进行 kickstart 安装；仅支持 NFS。更多信息请参阅第 8 章。

15. B. 运行级别 1 是单用户模式。运行级别 3 是带网络功能的多用户模式。运行级别 4 基本上与运行级别 3 相同。更多信息请参阅第 9 章。

16. D. 您无法方便地使用这些工具中的任何一个来启用 MD5 密码加密；`authconfig` 程序允许您启用 MD5 密码。更多信息请参阅第 9 章。

17. A, C. 请参阅第 10 章中提供的列表和描述，以验证 `/etc/bashrc` 和 `~/.bashrc` 文件是否设置了路径。更多信息请参阅第 10 章。

18. B, C, D. `groupmod` 命令可用于更改组名。更多信息请参阅第 10 章。

19. A, C, D. `-a` 选项会激活用户和组配额，除非指定了 `-g` 或 `-u`，在这种情况下，它仅激活指定类型的配额。更多信息请参阅第 11 章。

20. A. 在设置或开启配额之前，必须先创建配额文件。更多信息请参阅第 11 章。

21. C, D. 如果软件包尚未安装，`-i` 命令将安装该软件包；在此上下文中，`-f` 标志没有有效含义。更多信息请参阅第 12 章。

22. B. 命令 `rpm -bb` 从源码 RPM 构建二进制 RPM。更多信息请参阅第 12 章。

23. A, B. 模块位于 `/lib/modules` 的一个子目录中，该子目录以其关联的内核版本和构建版本命名。更多信息请参阅第 13 章。

24. C. `/proc/pci` 目录用于识别已安装的 PCI 设备。更多信息请参阅第 13 章。

25. C. 服务名称为 `lpd`，且 `restart` 参数是合适的。更多信息请参阅第 14 章。

26. B. 该标志是 `level` 而不是 `levels`，且需要 `on` 参数。更多信息请参阅第 14 章。

27. A, B, C, D. 任何备选方案都可行。更多信息请参阅第 15 章。

28. A. 使用 `init` 命令；其 `q` 参数前不能有破折号 (-)。更多信息请参阅第 15 章。

29. A. `cron` 系统跟踪 `/etc/crontab` 文件的修改时间，并知道文件何时被更改。更多信息请参阅第 16 章。

30. A, B, D. `rmmod` 作业每 10 分钟执行一次。更多信息请参阅第 16 章。

31. C. keep 行指定 `/etc/conf.modules` 中的路径信息是对默认信息的补充。更多信息请参阅第 17 章。

32. D. 您应该指定 `img` 扩展名以及内核版本和额外版本代码。更多信息请参阅第 18 章。

33. A. 缓存文件是 `/etc/ld.so.cache`；配置文件是 `/etc/ld.so.conf`。更多信息请参阅第 19 章。

34. B. 响应 `linux emergency`、`linux s` 和 `linux single` 都会使系统在运行级别 1 中启动。但是，只有 `linux emergency` 会省略初始进程。更多信息请参阅第 20 章。

35. A, B, D. 所有三个 Apache 配置文件必须存在；然而，指令可以放在任何文件中。更多信息请参阅第 21 章。

36. C. `in.telnetd` 程序不需要（且事实上也没有）具备 PAM 感知能力，因为它通过调用具备 PAM 感知能力的 `login` 程序来建立登录会话。更多信息请参阅第 22 章。

37. B, C. 如果远程主机与本地主机处于相同的管理控制下，则可以将远程主机列在 `/etc/hosts.equiv` 中；否则，应将其列在 `/etc/hosts.lpd` 中。主机名必须是可解析的，但主机不必列在 `/etc/hosts` 中；例如，主机名可以通过 DNS 或 NIS 解析。更多信息请参阅第 23 章。

38. C. 默认情况下，`authpriv` 消息被发送到 `/var/log/secure`，以便普通用户无法查看。更多信息请参阅第 24 章。

39. A. Red Hat Linux 将每个普通用户放入编号为 1 的用户私有组中。更多信息请参阅第 25 章。

40. A, C, D. 这些服务可能会向破解者泄露有用信息。`identd` 服务可以帮助您在网络中验证用户身份。更多信息请参阅第 25 章。

41. C. `--kickstart` 标志在尽可能范围内指定非交互式操作。`--expert` 标志允许您覆盖探测到的信息。更多信息请参阅第 26 章。

42. B, D. `xvidtune` 和 `xf86config` 工具允许您设置可能损坏显示器的无效特性。在 `xf86config` 的情况下，任何损坏都会在工具运行之后发生，因为该工具本身仅在文本模式下运行。更多信息请参阅第 26 章。

43. A. `~/.Xclients-default` 脚本会检查 `~/.wm_style` 文件的内容。更多信息请参阅第 27 章。

44. C. 虚拟控制台 7 与 X 相关联。更多信息请参阅第 27 章。

45. B. `--broadcast` 关键字会导致 X 发送广播消息并向响应服务器提供登录界面。更多信息请参阅第 28 章。

46. A. 您可以使用通配符来指定客户端主机。服务器在 CHOOSER 关键字之后指定。更多信息请参阅第 28 章。

47. D. `/proc` 文件系统不提供禁用 gated 的选项，且 `/etc/sysconf/network-scripts` 是一个目录而非文件。更多信息请参阅第 29 章。

48. A. OSPF-2 和 RIP-2 是内部协议。EGP 已不再流行。更多信息请参阅第 29 章。

49. A, B, C, D. 列出的每个选项都是支持伪装（masquerading）所必需的。更多信息请参阅第 30 章。

50. A. 要伪装本地网络，请将适当的规则附加到 forward 链。更多信息请参阅第 30 章。

## 共享库文件所有权表

本表汇总了对 Red Hat Linux 发行版 CD-ROM 磁盘的 RPMs 目录内容运行 `rpm -qp --filesbypkg *.rpm | grep '\.so' | sort > /tmp/liblist` 命令的输出结果。命令的输出经过编辑，仅包含库文件名，而非完整路径。

| 库 | 软件包 |
| :--- | :--- |
| ANSI_X3.110 | glibc |
| ASMO_449 | glibc |
| B | perl |
| BALTIC | glibc |
| BIG5 | glibc |
| CP1250 | glibc |
| CP1251 | glibc |
| CP1252 | glibc |
| CP1253 | glibc |
| CP1254 | glibc |
| CP1255 | glibc |
| CP1256 | glibc |
| CP1257 | glibc |
| CP1258 | glibc |
| CP737 | glibc |
| CP775 | glibc |
| CSN_369103 | glibc |
| CWI | glibc |
| DB_File | perl |
| DEC-MCS | glibc |
| Dumper | perl |
| EBCDIC-AT-DE | glibc |
| EBCDIC-AT-DE-A | glibc |
| EBCDIC-CA-FR | glibc |
| EBCDIC-DK-NO | glibc |
| EBCDIC-DK-NO-A | glibc |
| EBCDIC-ES | glibc |
| EBCDIC-ES-A | glibc |
| EBCDIC-ES-S | glibc |
| EBCDIC-FI-SE | glibc |
| EBCDIC-FI-SE-A | glibc |
| EBCDIC-FR | glibc |
| EBCDIC-IS-FRISS | glibc |
| EBCDIC-IT | glibc |
| EBCDIC-PT | glibc |
| EBCDIC-UK | glibc |
| EBCDIC-US | glibc |
| ECMA-CYRILLIC | glibc |
| EUC-CN | glibc |
| EUC-JP | glibc |
| EUC-KR | glibc |
| EUC-TW | glibc |
| Fcntl | perl |
| GDBM_File | perl |
| GOST_19768-74 | glibc |
| GREEK-CCITT | glibc |
| GREEK7 | glibc |
| GREEK7-OLD | glibc |
| HP-ROMAN8 | glibc |
| IBM037 | glibc |
| IBM038 | glibc |
| IBM1004 | glibc |
| IBM1026 | glibc |
| IBM1047 | glibc |
| IBM256 | glibc |
| IBM273 | glibc |
| IBM274 | glibc |
| IBM275 | glibc |
| IBM277 | glibc |
| IBM278 | glibc |
| IBM280 | glibc |
| IBM281 | glibc |
| IBM284 | glibc |
| IBM285 | glibc |
| IBM290 | glibc |
| IBM297 | glibc |
| IBM420 | glibc |
| IBM423 | glibc |
| IBM424 | glibc |
| IBM437 | glibc |
| IBM500 | glibc |
| IBM850 | glibc |



| 库 | 所有者 |
|---|---|
| IBM851 | glibc |
| IBM852 | glibc |
| IBM855 | glibc |
| IBM857 | glibc |
| IBM860 | glibc |
| IBM861 | glibc |
| IBM862 | glibc |
| IBM863 | glibc |
| IBM864 | glibc |
| IBM865 | glibc |
| IBM866 | glibc |
| IBM868 | glibc |
| IBM869 | glibc |
| IBM870 | glibc |
| IBM871 | glibc |
| IBM874 | glibc |
| IBM875 | glibc |
| IBM880 | glibc |
| IBM891 | glibc |
| IBM903 | glibc |
| IBM904 | glibc |
| IBM905 | glibc |
| IBM918 | glibc |
| IEC_P27-1 | glibc |
| INIS | glibc |
| INIS-8 | glibc |
| INIS-CYRILLIC | glibc |
| IO | perl |
| ISO-2022-JP | glibc |
| ISO-2022-KR | glibc |
| ISO-IR-197 | glibc |
| ISO646 | glibc |
| ISO8859-1 | glibc |
| ISO8859-10 | glibc |
| ISO8859-11 | glibc |
| ISO8859-13 | glibc |
| ISO8859-14 | glibc |
| ISO8859-15 | glibc |
| ISO8859-2 | glibc |
| ISO8859-3 | glibc |
| ISO8859-4 | glibc |
| ISO8859-5 | glibc |
| ISO8859-6 | glibc |
| ISO8859-7 | glibc |
| ISO8859-8 | glibc |
| ISO8859-9 | glibc |
| ISO_10367-BOX | glibc |
| ISO_2033 | glibc |
| ISO_5427 | glibc |
| ISO_5427-EXT | glibc |
| ISO_5428 | glibc |
| ISO_6937 | glibc |
| ISO_6937-2 | glibc |
| JOHAB | glibc |
| KOI-8 | glibc |
| KOI8-R | glibc |
| KOI8-U | glibc |
| LATIN-GREEK | glibc |
| LATIN-GREEK-1 | glibc |
| Leak | mod_perl |
| MAC-IS | glibc |
| MAC-UK | glibc |
| MACINTOSH | glibc |
| Magick | ImageMagick-devel |
| NATS-DANO | glibc |
| NATS-SEFI | glibc |
| NDBM_File | perl |
| Opcode | perl |
| POSIX | perl |
| Pg | postgresql-perl |
| SAMI-WS2 | glibc |
| SDBM_File | perl |
| SJIS | glibc |
| Socket | perl |
| Symbol | mod_perl |
| SysV | perl |
| T.61 | glibc |
| TIS-620 | glibc |
| UHC | glibc |
| _appletmodule | pygnome |
| _cappletmodule | pygnome |
| _gdkimlibmodule | pygtk |
| _gnomemodule | pygnome |
| _gnomeuimodule | pygnome |
| _gtkmodule | pygtk |
| _gtkxmhtmlmodule | pygnome |
| _libglademodule | pygtk-libglade |
| _pgmodule | postgresql-python |
| _snackmodule | newt |
| _tkinter | tkinter |
| _zvtmodule | pygnome |
| apache | linuxconf |
| arraymodule | python |
| attrs | perl |
| autoinc | postgresql-test |
| binascii | python |
| bsddbmodule | python |
| cPickle | python |
| cStringIO | python |
| cmathmodule | python |
| constraints | postgresql-test |
| copy | postgresql-test |
| create | postgresql-test |
| create_function_1 | postgresql-test |
| create_function_2 | postgresql-test |
| cryptmodule | python |
| cursesmodule | python |
| dbmmodule | python |
| dhcpd | linuxconf |
| dialout | linuxconf |
| dnsconf | linuxconf |
| errnmodule | python |
| fcntlmodule | python |
| firewall | linuxconf |
| gdbmmodule | python |
| global1.bki | postgresql-server |
| grpmodule | python |
| imap | php-imap |
| inittab | linuxconf |
| install_plpgsql | postgresql-test |
| ld | ld |
| ld-2.0.7 | compat-glibc |
| ld-2.1.2 | glibc |
| ld-linux | compat-glibc |
| ld-linux | glibc |
| ld-linux | ld |
| ldap | php-ldap |
| libApiTestOpts | pxe |
| libBLT | blt |
| libBrokenLocale | compat-glibc |
| libBrokenLocale | glibc |
| libBrokenLocale | glibc-devel |
| libBrokenLocale-2.0.7 | compat-glibc |
| libBrokenLocale-2.1.2 | glibc |
| libBootstrapOpts | pxe |
| libCNS | glibc |
| libFnlib | fnlib |
| libFnlib | fnlib-devel |
| libGB | glibc |
| libICE | XFree86-devel |
| libICE | XFree86-libs |
| libICE | compat-libs |
| libICE | libc |
| libIDL | ORBit-devel |
| libIDL-0.6 | ORBit |
| libIIOP | ORBit |
| libIIOP | ORBit-devel |
| libImlib | imlib |
| libImlib | imlib-devel |
| libJIS | glibc |
| libKSC | glibc |
| libMagick | ImageMagick |
| libMagick | ImageMagick-devel |
| libNoVersion | glibc |
| libNoVersion-2.1.2 | glibc |
| libORBit | ORBit |
| libORBit | ORBit-devel |
| libORBitCosNaming | ORBit |
| libORBitCosNaming | ORBit-devel |
| libORBitutil | ORBit |
| libORBitutil | ORBit-devel |
| libOSS | xmms |
| libPEX5 | XFree86-devel |
| libPEX5 | XFree86-libs |
| libPEX5 | compat-libs |
| libPEX5 | libc |
| libPropList | libPropList |
| libQwSpriteField | kdesupport |
| libSM | XFree86-devel |
| libSM | XFree86-libs |
| libSM | compat-libs |
| libSM | libc |
| libSegFault | glibc |
| libX11 | XFree86-devel |
| libX11 | XFree86-libs |
| libX11 | compat-libs |
| libX11 | libc |
| libXIE | XFree86-devel |
| libXIE | XFree86-libs |
| libXIE | compat-libs |
| libXIE | libc |
| libXaw | XFree86-devel |
| libXaw | XFree86-libs |
| libXaw | compat-libs |
| libXaw | libc |
| libXaw3d | Xaw3d |
| libXaw3d | Xaw3d-devel |
| libXaw3d | libc |
| libXext | XFree86-devel |
| libXext | XFree86-libs |
| libXext | compat-libs |
| libXext | libc |
| libXi | XFree86-devel |
| libXi | XFree86-libs |
| libXi | compat-libs |
| libXi | libc |
| libXmu | XFree86-devel |
| libXmu | XFree86-libs |
| libXmu | compat-libs |
| libXmu | libc |
| libXp | XFree86-devel |
| libXp | XFree86-libs |
| libXp | compat-libs |
| libXp | libc |
| libXpm | compat-libs |
| libXpm | libc |
| libXpm | xpm |
| libXpm | xpm-devel |
| libXt | XFree86-devel |
| libXt | XFree86-libs |
| libXt | compat-libs |
| libXt | libc |
| libXtst | XFree86-devel |
| libXtst | XFree86-libs |
| libXtst | compat-libs |
| libXtst | libc |
| libamu | am-utils |
| libart_lgpl | gnome-libs |
| libart_lgpl | gnome-libs-devel |
| libaudiopfile | audiofile |
| libaudiopfile | audiofile-devel |
| libawt | kaffe |
| libawt-1.0b4 | kaffe |
| libbfd | binutils |
| libbfd | compat-binutils |
| libbfd-2.9.1.0.23 | compat-binutils |
| libbfd-2.9.1.0.24 | binutils |
| libbscope | xmms |
| libbuffy | gtk-engines |
| libbz2 | bzip2 |
| libc | compat-glibc |
| libc | glibc |
| libc | glibc-devel |
| libc | libc |
| libc-2.0.7 | compat-glibc |
| libc-2.1.2 | glibc |
| libcapplet | control-center |
| libcapplet | control-center-devel |
| libcdaudio | xmms |
| libcfont | console-tools |
| libcom_err | e2fsprogs |
| libcom_err | e2fsprogs-devel |
| libconsole | console-tools |
| libcrack | cracklib |
| libcrypt | compat-glibc |
| libcrypt | glibc |
| libcrypt | glibc-devel |
| libcrypt-2.0.7 | compat-glibc |
| libcrypt-2.1.2 | glibc |
| libcsv | gnumeric |
| libctutils | console-tools |
| libcurses | ncurses-devel |
| libdb | compat-glibc |
| libdb | glibc |
| libdb | glibc-devel |
| libdb | libc |
| libdb-2.0.7 | compat-glibc |
| libdb-2.1.2 | glibc |
| libdb1 | glibc |
| libdb1 | glibc-devel |
| libdb1-2.1.2 | glibc |
| libdisk_writer | xmms |
| libdl | compat-glibc |
| libdl | glibc |
| libdl | glibc-devel |
| libdl | ld |
| libdl-2.0.7 | compat-glibc |
| libdl-2.1.2 | glibc |
| libe2p | e2fsprogs |
| libe2p | e2fsprogs-devel |
| libecho | xmms |
| libecpg | postgresql |
| libesd | esound |
| libesd | esound-devel |
| libesddsp | esound |
| libesddsp | esound-devel |
| libesdout | xmms |
| libexpect5.28 | expect |
| libext2fs | e2fsprogs |
| libext2fs | e2fsprogs-devel |
| libfbm | libgr |
| libfbm | libgr-devel |
| libfish_applet | gnome-core |
| libform | compat-libs |
| libform | libc |
| libform | ncurses |
| libform | ncurses-devel |
| libform | ncurses3 |
| libg++ | libc |
| libg++ | libstdc++ |
| libgck | gimp-libgimp |
| libgd | gd |
| libgd | gd-devel |
| libgdbm | gdbm |
| libgdbm | gdbm-devel |
| libgdk | gtk+-devel |
| libgdk | gtk+10 |
| libgdk-1.2 | gtk+ |
| libgdk_imlib | imlib |
| libgdk_imlib | imlib-devel |
| libgdkcardimage | gnome-games |
| libgdkcardimage | gnome-games-devel |
| libghttp | libghttp |
| libghttp | libghttp-devel |
| libgif | libungif |
| libgif | libungif-devel |
| libgimp | gimp-libgimp |
| libgimpui | gimp-libgimp |
| libgkb_applet | gnome-core |
| libglade | libglade |
| libglade | libglade-devel |
| libglade | libglade |
| libglade-gnome | libglade-devel |
| libglib | glib-devel |
| libglib | glib10 |
| libglib-1.2 | glib |
| libgmodule | glib-devel |
| libgmodule-1.2 | glib |
| libgmp | gmp |



| 库 | 软件包 |
| :--- | :--- |
| libgmp | gmp-devel |
| libgnome | gnome-libs |
| libgnome | gnome-libs-devel |
| libgnome-stones | gnome-games |
| libgnomekoban | gnome-games |
| libgnomesupport | gnome-libs | gnome-libs |
| libgnomesupport | gnome-libs-devel |
| libgnomeui | gnome-libs |
| libgnomeui | gnome-libs-devel |
| libgnorba | gnome-libs |
| libgnorba | gnome-libs-devel |
| libgnorbagtk | gnome-libs |
| libgnorbagtk | gnome-libs-devel |
| libgpmn | gpm |
| libgpmn | gpm-devel |
| libgthread | glib-devel |
| libgthread-1.2 | glib |
| libgtk | gtk+-devel |
| libgtk | gtk+1.0 |
| libgtk-1.2 | gtk+ |
| libgtkxmhtml | gnome-libs |
| libgtkxmhtml | gnome-libs-devel |
| libgtop | libgtop |
| libgtop | libgtop-devel |
| libgtop_common | libgtop |
| libgtop_common | libgtop-devel |
| libgtop_guile | libgtop |
| libgtop_guile | libgtop-devel |
| libgtop_guile_names | libgtop |
| libgtop_guile_names | libgtop-devel |
| libgtop_names | libgtop |
| libgtop_names | libgtop-devel |
| libgtop_suid_common | libgtop |
| libgtop_suid_common | libgtop-devel |
| libgtop_sysdeps | libgtop |
| libgtop_sysdeps | libgtop-devel |
| libguile | guile |
| libguile | guile-devel |
| libhistory | readline |
| libhistory | readline-devel |
| libhtml | gnumeric |
| libidcin | xmms |
| libimlib-bmp | imlib |
| libimlib-gif | imlib |
| libimlib-jpeg | imlib |
| libimlib-png | imlib |
| libimlib-ppm | imlib |
| libimlib-ps | imlib |
| libimlib-tiff | imlib |
| libimlib-xpm | imlib |
| libio | kaffe |
| libio-1.0b4 | kaffe |
| libir | xmms |
| libirda | irda-utils |
| libitcl | itcl |
| libitcl3.0 | itcl |
| libitk | itcl |
| libitk3.0 | itcl |
| libjoy | xmms |
| libjpeg | libjpeg |
| libjpeg | libjpeg-devel |
| libjpeg | libjpeg6a |
| libjs | netscape-common |
| libjavascript | kdelibs |
| libjavascript | kdelibs-devel |
| libjsd | kdelibs |
| libkab | kdelibs-devel |
| libkab | kaffe |
| libkaffevm | kaffe |
| libkaffevm-1.0b4 | kdelibs |
| libkdecore | kdelibs-devel |
| libkdecore | kdelibs |
| libkdeui | kdelibs-devel |
| libkdeui | kdelibs |
| libkfile | kdelibs-devel |
| libkfile | kdelibs |
| libkfm | kdelibs-devel |
| libkfm | kdelibs |
| libkhtmlw | kdelibs-devel |
| libkhtmlw | kdelibs |
| libkimgio | kdelibs-devel |
| libkimgio | kdelibs |
| libksirclistbox | kdenetwork |
| libkspell | kdelibs |
| libkspell | kdelibs-devel |
| liblber | openldap |
| liblber | openldap-devel |
| libldap | openldap |
| libldap | openldap-devel |
| liblotus | gnumeric |
| libm | compat-glibc |
| libm | glibc |
| libm | glibc-devel |
| libm | libc |
| libm-2.0.7 | compat-glibc |
| libm-2.1.2 | glibc |
| libmanagement | kaffe |
| libmanagement-1.0b4 | kaffe |
| libmath | kaffe |
| libmath-1.0b4 | kaffe |
| libmd5 | w3c-libwww |
| libmd5 | w3c-libwww-devel |
| libmediatool | kdelibs |
| libmediatool | kdelibs-devel |
| libmenu | compat-libs |
| libmenu | libc |
| libmenu | ncurses |
| libmenu | ncurses-devel |
| libmenu | ncurses3 |
| libmetal | gtk-engines |
| libmikmod | mikmod |
| libmimelib | kdesupport |
| libmpg123 | xmms |
| libnative | kaffe |
| libnative-1.0b4 | kaffe |
| libncp | ncpfs |
| libncurses | compat-libs |
| libncurses | libc |
| libncurses | ncurses |
| libncurses | ncurses-devel |
| libncurses | ncurses3 |
| libndbm | compat-glibc |
| libndbm | glibc-devel |
| libnet | kaffe |
| libnet-1.0b4 | kaffe |
| libnewt | newt |
| libnewt | newt-devel |
| libnotif | gtk-engines |
| libnotif2 | gtk-engines |
| libnsl | compat-glibc |
| libnsl | glibc |
| libnsl | glibc-devel |
| libnsl-2.0.7 | compat-glibc |
| libnsl-2.1.2 | glibc |
| libnss1_compat | glibc |
| libnss1_compat | glibc-devel |
| libnss1_compat-2.1.2 | glibc |
| libnss1_db | glibc |
| libnss1_db | glibc-devel |
| libnss1_db-2.1.2 | glibc |
| libnss1_dns | glibc |
| libnss1_dns | glibc-devel |
| libnss1_dns-2.1.2 | glibc |
| libnss1_files | glibc |
| libnss1_files | glibc-devel |
| libnss1_files-2.1.2 | glibc |
| libnss1_nis | glibc |
| libnss1_nis | glibc-devel |
| libnss1_nis-2.1.2 | glibc |
| libnss_compat | compat-glibc |
| libnss_compat | glibc |
| libnss_compat | glibc-devel |
| libnss_compat-2.0.7 | compat-glibc |
| libnss_compat-2.1.2 | glibc |
| libnss_db | compat-glibc |
| libnss_db | glibc |
| libnss_db | glibc-devel |
| libnss_db-2.0.7 | compat-glibc |
| libnss_db-2.1.2 | glibc |
| libnss_dns | compat-glibc |
| libnss_dns | glibc |
| libnss_dns | glibc-devel |
| libnss_dns-2.0.7 | compat-glibc |
| libnss_dns-2.1.2 | glibc |
| libnss_files | compat-glibc |
| libnss_files | glibc |
| libnss_files | glibc-devel |
| libnss_files-2.0.7 | compat-glibc |
| libnss_files-2.1.2 | glibc |
| libnss_hesiod | glibc |
| libnss_hesiod | glibc-devel |
| libnss_hesiod-2.1.2 | glibc |
| libnss_ldap | nss_ldap |
| libnss_ldap-2.1.1 | nss_ldap |
| libnss_nis | compat-glibc |
| libnss_nis | glibc |
| libnss_nis | glibc-devel |
| libnss_nis-2.0.7 | compat-glibc |
| libnss_nis-2.1.2 | glibc |
| libnss_nisplus | glibc |
| libnss_nisplus | glibc-devel |
| libnss_nisplus-2.1.2 | glibc |
| libnullplugin | netscape-common |
| libobex | irda-utils |
| libobgnome | gnome-objc |
| libobgnome | gnome-objc-devel |
| libobgtk | gnome-objc |
| libobgtk | gnome-objc-devel |
| libopcodes | binutils |
| libopcodes | compat-binutils |
| libopcodes-2.9.1.0.23 | compat-binutils |
| libopcodes-2.9.1.0.24 | binutils |
| libp2c | p2c |
| libpalistbox | kdenetwork |
| libpam | pam |
| libpam_misc | pam |
| libpanel | compat-libs |
| libpanel | libc |
| libpanel | ncurses |
| libpanel | ncurses-devel |
| libpanel | ncurses3 |
| libpanel_applet | gnome-core |
| libpanel_applet | gnome-core-devel |
| libpbm | libgr |
| libpbm | libgr-devel |
| libpbutton | kdenetwork |
| libperl | mod_perl |
| libpframe | kdenetwork |
| libpgm | libgr |
| libpgm | libgr-devel |
| libpgtcl | postgresql-tcl |
| libphp3 | php |
| libpisock | pilot-link |
| libpisock | pilot-link-devel |
| libpixmap | gtk-engines |
| libpkfiledialog | kdenetwork |
| libplabel | kdenetwork |
| libplined | kdenetwork |
| libplistbox | kdenetwork |
| libpmenudta | kdenetwork |
| libpng | libpng |
| libpng | libpng-devel |
| libpnm | libgr |
| libpnm | libgr-devel |
| libpobjfinder | kdenetwork |
| libppm | libgr |
| libppm | libgr-devel |
| libppopmenu | kdenetwork |
| libpprogress | kdenetwork |
| libppushbt | kdenetwork |
| libpq | postgresql |
| libpq++ | postgresql |
| libproc | procps |
| libproxy | apache |
| libpsqlodbc | postgresql-odbc |
| libptabdialog | kdenetwork |
| libptablevw | kdenetwork |
| libpthread | compat-glibc |
| libpthread | glibc |
| libpthread | glibc-devel |
| libpthread-0.7 | compat-glibc |
| libpthread-0.8 | glibc |
| libpuke | kdenetwork |
| libpwdb | pwdb |
| libpxeParser | pxe |
| libpxeTester | pxe |
| libpxelib | pxe |
| libpython | gnumeric |
| libqimgio | qtlx |
| libqimgio | qtlx-devel |
| libqt | qt |
| libqt | qt-devel |
| libqt | qtlx |
| libqt | qtlx-devel |
| libreadline | readline |
| libreadline | readline-devel |
| libredmond95 | gtk-engines |
| libresolv | compat-glibc |
| libresolv | glibc |
| libresolv | glibc-devel |
| libresolv-2.0.7 | compat-glibc |
| libresolv-2.1.2 | glibc |
| librle | libgr |
| librle | libgr-devel |
| librpm | rpm |
| librpm | rpm-devel |
| librpmbuild | rpm |
| librpmbuild | rpm-devel |
| librt | glibc |
| librt | glibc-devel |
| librt-2.1.2 | glibc |
| libsample | gnumeric |
| libsanalyzer | xmms |
| libslang | slang |
| libslang | slang-devel |
| libsnmp | ucd-snmp |
| libsnmp | ucd-snmp-devel |
| libsong_change | xmms |
| libsrndecho | xmms |
| libss | e2fsprogs |
| libss | e2fsprogs-devel |
| libstat | gnumeric |
| libstdc++ | compat-egcs-c++ |
| libstdc++ | egcs-c++ |
| libstdc++ | libc |
| libstdc++ | libstdc++ |
| libstdc++-2-libc6.1-1-2.9.0 | egcs-c++ |
| libstdc++-2-libc6.1-1-2.9.0 | libstdc++ |
| libstereo | xmms |
| libtcl | tcl |



| 库 | 软件包 |
| :--- | :--- |
| libltc18.0 | tcl |
| libtclx | tclx |
| libtclx8.0.4 | tclx |
| libtermcap | compat-libs |
| libtermcap | libc |
| libtermcap | libtermcap |
| libtermcap | libtermcap-devel |
| libtext | gnumeric |
| libthinice | gtk-engines |
| libtiff | libtiff |
| libtiff | libtiff-devel |
| libtix | tix |
| libtix4.1.8.0 | tix |
| libtixsam4.1.8.0 | tix |
| libtk | tk |
| libtk8.0 | tk |
| libtkx | tclx |
| libtkx8.0.4 | tclx |
| libttf | freetype |
| libttf | freetype-devel |
| libungif | libungif |
| libungif | libungif-devel |
| libutempter | utempter |
| libutil | compat-glibc |
| libutil | glibc |
| libutil | glibc-devel |
| libutil-2.0.7 | compat-glibc |
| libutil-2.1.2 | glibc |
| libuuid | e2fsprogs |
| libuuid | e2fsprogs-devel |
| libuutilib | kdesupport |
| libvga | libc |
| libvga | svgalib |
| libvga | svgalib-devel |
| libvgagl | libc |
| libvgagl | svgalib |
| libvgagl | svgalib-devel |
| libvoice | xmms |
| libwav | xmms |
| libwraster | WindowMaker |
| libwwwapp | w3c-libwww |
| libwwwapp | w3c-libwww-devel |
| libwwwcache | w3c-libwww |
| libwwwcache | w3c-libwww-devel |
| libwwwcore | w3c-libwww |
| libwwwcore | w3c-libwww-devel |
| libwwwdir | w3c-libwww |
| libwwwdir | w3c-libwww-devel |
| libwwwfile | w3c-libwww |
| libwwwfile | w3c-libwww-devel |
| libwwwftp | w3c-libwww |
| libwwwftp | w3c-libwww-devel |
| libwwwgopher | w3c-libwww |
| libwwwgopher | w3c-libwww-devel |
| libwwwhtml | w3c-libwww |
| libwwwhtml | w3c-libwww-devel |
| libwwwhttp | w3c-libwww |
| libwwwhttp | w3c-libwww-devel |
| libwwinit | w3c-libwww |
| libwwinit | w3c-libwww-devel |
| libwwmime | w3c-libwww |
| libwwmime | w3c-libwww-devel |
| libwwmux | w3c-libwww |
| libwwmux | w3c-libwww-devel |
| libwwnews | w3c-libwww |
| libwwnews | w3c-libwww-devel |
| libwwstream | w3c-libwww |
| libwwstream | w3c-libwww-devel |
| libwwtelnet | w3c-libwww |
| libwwtelnet | w3c-libwww-devel |
| libwwtrans | w3c-libwww |
| libwwtrans | w3c-libwww-devel |
| libwwutils | w3c-libwww |
| libwwutils | w3c-libwww-devel |
| libwwwxml | w3c-libwww |
| libwwwxml | w3c-libwww-devel |
| libwwwzip | w3c-libwww |
| libwwwzip | w3c-libwww-devel |
| libxbase | gnumeric |
| libxml | libxml |
| libxml | libxml-devel |
| libxml | libxml110 |
| libxmlparse | w3c-libwww |
| libxmlparse | w3c-libwww-devel |
| libxmltok | w3c-libwww |
| libxmltok | w3c-libwww-devel |
| libxmms | xmms |
| libxmms | xmms-devel |
| libz | libc |
| libz | zlib |
| libz | zlib-devel |
| libzip | kaffe |
| libzip-1.0b4 | kaffe |
| libzvt | gnome-libs |
| libzvt | gnome-libs-devel |
| local1_template1.bki | postgresql-server |
| lookup_file | autofs |
| lookup_nisplus | autofs |
| lookup_program | autofs |
| lookup_yp | autofs |
| mailconf | linuxconf |
| mathmodule | python |
| md5module | python |
| misc | postgresql-test |
| mod_glass | apache |
| mod_actions | apache |
| mod_alias | apache |
| mod_asis | apache |
| mod_auth | apache |
| mod_auth_anon | apache |
| mod_auth_db | apache |
| mod_auth_ldap | auth_ldap |
| mod_autoindex | apache |
| mod_bandwidth | apache |
| mod_cern_meta | apache |
| mod_cgi | apache |
| mod_digest | apache |
| mod_dir | apache |
| mod_env | apache |
| mod_example | apache |
| mod_expires | apache |
| mod_headers | apache |
| mod_imap | apache |
| mod_include | apache |
| mod_info | apache |
| mod_log_agent | apache |
| mod_log_config | apache |
| mod_log_referer | apache |
| mod_mime | apache |
| mod_mime_magic | apache |
| mod_mmap_static | apache |
| mod_negotiation | apache |
| mod_php | phpfi |
| mod_rewrite | apache |
| mod_setenvif | apache |
| mod_speling | apache |
| mod_status | apache |
| mod_unique_id | apache |
| mod_userdir | apache |
| mod_usertrack | apache |
| mod_vhost_alias | apache |
| modemconf | linuxconf |
| motd | linuxconf |
| mount_afs | autofs |
| mount_autofs | autofs |
| mount_ext2 | autofs |
| mount_generic | autofs |
| mount_nfs | autofs |
| mpzmodule | python |
| mrtg | linuxconf |
| netadm | linuxconf |
| newmodule | python |
| nismodule | python |
| nss_ldap | nss_ldap |
| operator | python |
| pam_access | pam |
| pam_console | pam |
| pam_cracklib | pam |
| pam_deny | pam |
| pam_env | pam |
| pam_filter | pam |
| pam_ftp | pam |
| pam_group | pam |
| pam_lastlog | pam |
| pam_ldap | pam_ldap |
| pam_limits | pam |
| pam_listfile | pam |
| pam_mail | pam |
| pam_nologin | pam |
| pam_permit | pam |
| pam_pwdb | pam |
| pam_radius | pam |
| pam_rhosts_auth | pam |
| pam_rootok | pam |
| pam_securetty | pam |
| pam_shells | pam |
| pam_stress | pam |
| pam_tally | pam |
| pam_time | pam |
| pam_unix | pam |
| pam_unix_acct | pam |
| pam_unix_auth | pam |
| pam_unix_passwd | pam |
| pam_unix_session | pam |
| pam_userdb | pam |
| pam_warn | pam |
| pam_wheel | pam |
| pam_xauth | pam |
| parse_sun | autofs |
| parsermodule | python |
| pex5 | XFree86 |
| pgsql | php-pgsql |
| plpgsql | postgresql-server |
| pltcl | postgresql-tcl |
| pppdialin | linuxconf |
| pwdmodule | python |
| rarp | linuxconf |
| re | perl |
| readline | python |
| redhat | linuxconf |
| redhatppp | linuxconf |
| refint | postgresql-test |
| regress | postgresql-test |
| resource | python |
| rotormodule | python |
| rpmmodule | rpm |
| samba | linuxconf |
| selectmodule | python |
| shamodule | python |
| socketmodule | python |
| squid | linuxconf |
| status | linuxconf |
| stropmodule | python |
| structmodule | python |
| syslogmodule | python |
| termios | python |
| timemodule | python |
| timingmodule | python |
| treemenu | linuxconf |
| usermenu | linuxconf |
| uucp | linuxconf |
| wuftpd | linuxconf |
| xf86AceCad | XFree86 |
| xf86Calcomp | XFree86 |
| xf86Dial | XFree86 |
| xf86Dyna | XFree86 |
| xf86Elo | XFree86 |
| xf86Jstk | XFree86 |
| xf86MuTouch | XFree86 |
| xf86Summa | XFree86 |
| xf86Wacom | XFree86 |
| xie | XFree86 |
| xterminals | linuxconf |
| zlibmodule | python |

## GNU 通用公共许可证

版本 2, 1991 年 6 月
版权所有 (C) 1989, 1991 自由软件基金会, Inc.
59 Temple Place, Suite 330, Boston, MA 02111-1307 USA
任何人都被允许逐字复制并分发本许可证文档，但不允许对其进行修改。

### 序言

大多数软件的许可证旨在剥夺您分享和修改软件的自由。相比之下，GNU 通用公共许可证旨在保证您分享和修改自由软件的自由——以确保软件对所有用户都是自由的。本通用公共许可证适用于自由软件基金会的大部分软件，以及任何作者承诺使用该许可证的其他程序。（自由软件基金会的某些其他软件则由 GNU 库通用公共许可证覆盖。）您也可以将其应用于您的程序。

当我们谈论自由软件时，我们指的是自由，而不是价格。我们的通用公共许可证旨在确保您拥有分发自由软件副本的自由（如果您愿意，可以为此服务收费），确保您能收到源码或在需要时获得源码，确保您可以修改软件或将其片段用于新的自由程序，并且确保您知道自己可以执行这些操作。

为了保护您的权利，我们需要制定限制，禁止任何人剥夺您的这些权利或要求您放弃这些权利。如果您分发软件副本或对其进行修改，这些限制将转化为您的某些责任。

例如，如果您分发此类程序的副本（无论是免费还是收费），您必须向接收者提供您所拥有的所有权利。您必须确保他们也能收到或获得源码。而且您必须向他们展示这些条款，以便他们了解自己的权利。

我们通过两个步骤来保护您的权利：(1) 对软件进行版权保护，以及 (2) 向您提供本许可证，给予您复制、分发和/或修改软件的法律许可。

此外，为了保护每位作者以及我们自己，我们希望确保每个人都明白，此自由软件不提供任何担保。如果软件被他人修改并传递，我们希望接收者知道他们所获得的是非原版，以便他人引入的任何问题不会影响原作者的声誉。



最后，任何自由程序都时刻受到软件专利的威胁。我们希望避免自由程序的再发行者分别获得专利许可，从而在事实上使该程序变成私有化的危险。为了防止这种情况，我们明确规定，任何专利必须许可给所有人自由使用，或者完全不予许可。

接下来的内容是关于复制、发行和修改的具体条款和条件。

### 复制、发行和修改的条款和条件

- 1. 本许可证适用于任何包含版权持有者放置的通知，且该通知声明该程序可根据本通用公共许可证条款进行发行的程序或其他作品。下文中的“程序”是指任何此类程序或作品，而“基于该程序的作品”是指该程序或版权法下的任何衍生作品；也就是说，包含该程序或其一部分的作品，无论是原样保留、经过修改和/或翻译成另一种语言。（在此，翻译无限制地包含在“修改”一词中。）每位被许可者被称为“您”。

除复制、发行和修改之外的活动不受本许可证的涵盖；它们在其实施范围之外。运行程序的行为不受限制，且只有当程序的输出内容构成了基于该程序的作品时（无论是否是通过运行程序产生），该输出才受本许可证涵盖。这是否成立取决于程序的具体功能。

- 2. 您可以按照接收到的形式，通过任何介质复制并发行程序的源代码原件，前提是在每份副本上醒目且恰当地发布相应的版权声明和免责声明；保持所有提及本许可证且声明无担保的通知完整；并将本许可证的副本随程序一起交给任何其他接收者。

您可以为转移副本的物理行为收取费用，并且您可以选择以收费方式提供担保保护。

- 3. 您可以修改您拥有的程序副本或其任何部分，从而形成一项基于该程序的作品，并根据上述第 1 条的条款复制和发行此类修改或作品，前提是您还必须满足以下所有条件：

    - a) 您必须使修改后的文件带有醒目的通知，声明您修改了这些文件以及任何修改的日期。
    - b) 您必须使您发行或发布的、全部或部分包含或衍生自该程序或其任何部分的任何作品，整体地根据本许可证的条款向所有第三方免费许可。
    - c) 如果修改后的程序在运行时通常以交互方式读取命令，那么在以最普通的方式启动此类交互式运行过程时，您必须使其打印或显示一条公告，包括相应的版权通知和免责声明（或者声明您提供担保），并告知用户可以在这些条件下再发行该程序，以及告知用户如何查看本许可证的副本。（例外：如果程序本身是交互式的但通常不打印此类公告，则您基于该程序的作品不需要打印公告。）

这些要求适用于修改后的作品整体。如果该作品中可识别的部分并非衍生自该程序，且可以合理地被认为是独立且分离的作品，那么当您将其作为独立作品发行时，本许可证及其条款不适用于这些部分。但当您将相同的部分作为基于该程序的整体作品的一部分发行时，整体的发行必须遵守本许可证的条款，其对其他被许可者的许可延伸至整个整体，因此延伸至每一个部分，无论是由谁编写的。

因此，本节的目的并不是要主张权利或争夺您完全由您编写的作品的权利；相反，其目的是行使控制基于该程序的衍生作品或集合作品发行的权利。

此外，仅仅将不基于该程序的另一个作品与该程序（或基于该程序的作品）聚集在同一个存储卷或发行介质上，并不会使另一个作品进入本许可证的范围。

- 4. 您可以根据上述第 1 条和第 2 条的条款，以目标代码或可执行文件形式复制并发行该程序（或根据第 2 条基于其的作品），前提是您必须执行以下操作之一：

    - a) 随附完整的相应机器可读源代码，且该源代码必须根据上述第 1 条和第 2 条的条款，在通常用于软件交换的介质上发行；或者，
    - b) 随附一份有效期至少三年的书面承诺，向任何第三方提供一份完整的机器可读相应源代码副本，费用不超过您执行源代码发行的物理成本，且该源代码必须根据上述第 1 条和第 2 条的条款，在通常用于软件交换的介质上发行；或者，
    - c) 随附您收到的关于发行相应源代码的承诺信息。（此替代方案仅允许非商业发行，且仅在您收到目标代码或可执行文件形式的程序时且随附有符合上述 b 小节的承诺的情况下才允许。）

作品的源代码是指对其进行修改的首选形式。对于可执行作品，完整的源代码是指其包含的所有模块的所有源代码，加上任何相关的接口定义文件，以及用于控制可执行文件编译和安装的脚本。然而，作为一个特殊例外，发行的源代码不必包含通常随可执行文件运行的操作系统主要组件（编译器、内核等）一起发行的任何内容（无论是源代码还是二进制形式），除非该组件本身随可执行文件一起提供。

如果可执行代码或目标代码的发行是通过提供从指定地点复制的访问权限来实现的，那么提供从同一地点复制源代码的同等访问权限即被视为发行源代码，即使第三方并不被强迫在复制目标代码的同时复制源代码。

- 5. 除本许可证明确规定外，您不得复制、修改、分许可或发行该程序。任何其他复制、修改、分许可或发行该程序的尝试均无效，并将自动终止您在本许可证下的权利。然而，根据本许可证从您这里获得副本或权利的一方，只要其保持完全合规，其许可证将不会被终止。

- 6. 您无需接受本许可证，因为您没有签署它。然而，没有其他任何东西授予您修改或发行该程序及其衍生作品的权限。如果您不接受本许可证，这些行为将被法律禁止。因此，通过修改或发行该程序（或任何基于该程序的作品），即表示您接受本许可证以进行此类操作，并接受其关于复制、发行或修改该程序或基于该程序的作品的所有条款和条件。

- 7. 每当您再发行该程序（或任何基于该程序的作品）时，接收者自动从原始许可方获得一份许可证，以根据这些条款和条件复制、发行或修改该程序。您不得对接收者行使本协议授予的权利施加任何进一步的限制。您不对第三方遵守本许可证的情况负责。

- 8. 如果由于法院判决、专利侵权指控或任何其他原因（不限于专利问题），您被强加了（无论是通过法院命令、协议还是其他方式）与本许可证条件相矛盾的条件，这些条件并不能免除您遵守本许可证条件的义务。如果您无法在同时满足本许可证义务和任何其他相关义务的情况下进行发行，那么结果就是您完全不能发行该程序。例如，如果一项专利许可不允许所有直接或间接通过您接收副本的人免费再发行该程序，那么您能同时满足该专利许可和本许可证的唯一方法就是完全停止发行该程序。

如果本节的任何部分在任何特定情况下被判定为无效或不可执行，则本节的其余部分旨在继续适用，且本节整体旨在其他情况下适用。

本节的目的不是诱导您侵犯任何专利或其他财产权利主张，或争论任何此类主张的有效性；本节的唯一目的是保护自由软件发行系统的完整性，该系统是通过公共许可证实践实现的。许多人依赖该系统的一致应用，为通过该系统发行的广泛软件做出了慷慨贡献；作者/捐赠者有权决定他或她是否愿意通过任何其他系统发行软件，而被许可者不能强加这种选择。



本节旨在详尽阐明被认为是本许可证其余部分的推论。

- 9. 如果本程序的分发和/或使用在某些国家因专利或版权接口而受到限制，将本程序置于本许可证下的原版权持有人可以增加明确的地理分发限制，排除这些国家，从而使得分发仅在未被排除的国家境内或国家之间进行。在这种情况下，本许可证将该限制纳入其中，视同其写在本许可证的正文内。

- 10. 自由软件基金会可能会不时发布通用公共许可证的修订版和/或新版本。此类新版本在精神上将与当前版本相似，但在细节上可能会有所不同，以解决新出现的问题或顾虑。

每个版本都被赋予一个区分性的版本号。如果本程序指定了适用于它的本许可证版本号以及“任何后续版本”，则您可以选择遵守该版本或自由软件基金会发布的任何后续版本的条款和条件。如果本程序未指定本许可证的版本号，您可以选择自由软件基金会发布过的任何版本。

- 11. 如果您希望将本程序的某些部分合并到分发条件不同的其他自由程序中，请致信作者请求许可。对于由自由软件基金会拥有版权的软件，请致信自由软件基金会；我们有时会对这种情况做出例外处理。我们的决定将以两个目标为指导：保持我们自由软件所有衍生版本的自由状态，以及促进软件的通用共享和重用。

### 无担保

- 1. 由于本程序是免费许可的，在适用法律允许的范围内，本程序不提供任何担保。除非另有书面说明，版权持有人和/或其他方按“原样”提供本程序，不提供任何形式的明示或暗示担保，包括但不限于对适销性和特定用途适用性的暗示担保。关于本程序的质量和性能的所有风险由您承担。如果本程序被证明有缺陷，您需承担所有必要的服务、修理或纠正的费用。

- 2. 除非适用法律要求或书面同意，否则在任何情况下，任何版权持有人或任何其他可能按上述许可修改和/或重新分发本程序的方，均不对您造成的损害承担责任，包括因使用或无法使用本程序而产生的任何一般性、特殊、偶然或后果性损害（包括但不限于数据丢失或数据变得不准确，或您或第三方遭受的损失，或本程序无法与其他任何程序协同运行），即使该持有人或其他方已被告知发生此类损害的可能性。

条款和条件结束

### 如何将这些条款应用于您的新程序

如果您开发了一个新程序，并且希望它能为公众提供最大的效用，最好的方法是将其变为自由软件，让每个人都能根据这些条款重新分发和修改它。

为此，请在程序中附上以下通知。最安全的方法是将它们附在每个源文件的开头，以便最有效地传达免责声明；且每个文件应至少包含“版权”行以及指向完整通知所在位置的指针。

> <用一行文字给出程序的名称及其功能的简要介绍。>
> Copyright (C) 19yy <作者姓名>
> 
> 本程序是自由软件；您可以根据自由软件基金会发布的 GNU 通用公共许可证的条款重新分发和/或修改它；可以是本许可证的第 2 版，或者（由您选择）任何后续版本。
> 
> 本程序的分发是希望它会是有用的，但没有任何担保；甚至没有关于适销性或特定用途适用性的暗示担保。详见 GNU 通用公共许可证。
> 
> 您应该随本程序收到一份 GNU 通用公共许可证的副本；如果没有，请致信自由软件基金会，Inc., 59 Temple Place, Suite 330, Boston, MA 02111-1307 USA

同时请添加通过电子邮箱和纸质邮件联系您的信息。

如果程序是交互式的，请在它以交互模式启动时输出如下简短通知：
Gnomovision version 69, Copyright (C) 19yy 作者姓名
Gnomovision 绝对没有任何担保；详情请输入 ‘show w’。

这是自由软件，欢迎您在某些条件下重新分发它；详情请输入 ‘show c’。

假设的命令 ‘show w’ 和 ‘show c’ 应该显示通用公共许可证的相应部分。当然，您使用的命令可以叫其他名字，而不仅仅是 ‘show w’ 和 ‘show c’；它们甚至可以是鼠标点击或菜单项——只要适合您的程序即可。

如果必要，您还应该让您的雇主（如果您作为程序员工作）或您的学校（如果有）为该程序签署一份“版权放弃声明”。这里有一个示例，请修改其中的名称：
Yoyodyne, Inc. 特此声明放弃对 James Hacker 编写的程序 ‘Gnomovision’（该程序会对编译器进行尝试）的所有版权权益。
<Ty Coon 的签名>, 1989 年 4 月 1 日
Ty Coon, 总裁

本通用公共许可证不允许将您的程序合并到专有程序中。如果您的程序是一个子程序库，您可能会认为允许专有应用程序与该库链接会更有用。如果您想这样做，请使用 GNU 库通用公共许可证而非本许可证。

## 术语表

### A

**a.out** `a.out` 格式是一种在早期 Linux 版本中很流行的对象文件格式。

### B

**base i/o address** (基础 I/O 地址) 基础 I/O 地址是用于与设备接口通信的内存缓冲区的起始地址。

**bind-listen-connect-accept process** (绑定-监听-连接-接受过程) 绑定-监听-连接-接受过程是 TCP 服务器遵循的一个过程，用于监听并处理客户端请求。

**block device** (块设备) 块设备是响应单个输入输出请求时发送多个字符的设备。常见的块设备包括硬盘和 CD-ROM。参见 *character device*。

**boot argument** (启动参数) 启动参数是在启动时提供并由 `/proc` 提升，或由 `init` 传递给内核或 `init` 进程的参数。

**boot loader** (启动加载程序) 启动加载程序是一个程序（例如 `lilo` 启动加载程序），它将操作系统的第一阶段加载到内存中。

**boot prompt** (启动提示符) 启动提示符是由启动加载程序（如 `lilo`）提供的提示，用户可以通过它指定要加载的启动镜像和要处理的启动参数。

**BOOTP** BOOTP 是一种通用协议，允许服务器为客户端主机分配 IP 地址和其他网络配置信息。

**broadcast message** (广播消息) 广播消息是发送给本地网络上所有主机的消息。

**browse master** (浏览主服务器) 浏览主服务器是网络上的 SMB (System Message Block) 服务器，它向客户端提供可用服务器和共享的信息。

**build number** (构建版本号) 构建版本号是一个指示软件构建顺序号的数字，因此它标志着在构建程序时应用的补丁和指定的选项。

**bus** (总线) 总线是连接计算机组件的数字路径。例如，总线将 CPU 与 RAM 内存和接口适配器卡连接起来。

### C

**canonical name** (规范名称) 规范名称是在域名服务器 (DNS) 配置中指定的主机名别名。

**capability** (能力/特性) 能力是由 RPM 软件包提供或其所需的资源或功能。

**certification** (认证) 认证是将个人识别为能够执行指定功能或功能的各种过程。红帽认证工程师 (Red Hat Certified Engineer) 的认证提供了作为红帽 Linux 系统管理员所需技能的证据。

**character device** (字符设备) 字符设备是响应输入输出请求时发送单个字符或相对较少字符的设备。参见 *block device*。

**chooser** (选择器) 选择器是由 X 显示管理器提供的一个对话框，允许用户选择登录主机以及可能的其他选项。

**compiler** (编译器) 编译器是一个将源代码翻译成目标代码的程序，例如 C 编译器。

**component** (组件) 组件是一组具有相关功能或目的的软件包。

**connectionless protocol** (无连接协议) 无连接协议是一种在数据交换之前不进行握手的协议。

**copyleft** (写左/版权左移) Copyleft 是一种旨在确保软件自由的特殊版权形式。参见 `GPL`。

**cron** `cron` 服务器允许用户调度在指定时间启动的任务。

**crontab file** (crontab 文件) `crontab` 文件是包含 `cron` 程序配置信息的文件。

**current working directory** (当前工作目录) 当前工作目录是隐式前缀到相对路径的目录名称。

### D

**daemon** (守护进程) 守护进程是一个在后台运行的程序，也就是说，它没有连接的控制台。

**default route** (默认路由) 默认路由是指在不存在更具体的目标路由时，数据包被发送的路由。



## 术语表

**dependency**（依赖）依赖是指软件包之间的一种关系，其中一个软件包需要另一个软件包提供的资源或功能。

**dependency information**（依赖信息）依赖信息是存储在软件包文件中的信息，用于指示该软件包提供以及需要的资源和功能。

**desktop manager**（桌面管理器）桌面管理器是一个 X 客户端，提供桌面图标、任务栏、分页器、文件管理器或其他常见的桌面功能。

**development kernel**（开发内核）开发内核是正处于重大开发阶段的内核版本。请参阅 *stable kernel*（稳定内核）。

**device file**（设备文件）设备文件是与硬件设备相关联的特殊文件。

**DHCP** 动态主机配置协议 (DHCP) 是一种允许服务器向客户端主机提供 IP 地址和其他配置信息的协议。

**disk geometry**（磁盘几何结构）磁盘几何结构是指与磁盘驱动器相关联的扇区数、磁头数和柱面数。

**display manager**（显示管理器）显示管理器是一个特殊的 X 客户端，提供了通过 X 会话登录系统的手段。

**distance-vector protocol**（距离向量协议）距离向量协议是一种路由协议，路由器通过该协议将其路由表的内容告知其相邻主机。

**DMA** 直接内存访问 (DMA) 是一种通过允许设备直接访问系统内存来加速设备输入和输出的设施。

**domain name**（域名）域名是由组织在互联网管理机构注册并由属于该组织的主机共享的名称。一个组织可以注册多个域名。主机名和域名的组合构成了完全限定域名，它可以唯一地标识一台主机。

**dynamic IP address**（动态 IP 地址）动态 IP 地址是指动态分配的 IP 地址，例如在主机启动时分配。请参阅 *static IP address*（静态 IP 地址）。

**dynamic linking**（动态链接）动态链接是在程序加载时执行的链接。链接将对象模块与其使用的库成员相结合，以形成一个完整的程序。请参阅 *static linking*（静态链接）。

**dynamic loader**（动态加载器）动态加载器是一个能够进行 *dynamic linking*（动态链接）的加载器。

**dynamic routing**（动态路由）动态路由是一种路由技术，其中路由表的内容随网络状况的变化而自动更新。请参阅 *static routing*（静态路由）。

### E

**election**（选举）选举是 SMB (System Message Block) 服务器通过竞争来确定哪个服务器将充当 *master browser*（主浏览器）的过程。

**ELF** ELF 是目前 Linux 系统使用的对象文件格式。

**environment variable**（环境变量）环境变量是与 Linux shell 相关联的变量，可用于设置应用程序选项并在应用程序之间传递数据。

**extended partition**（扩展分区）扩展分区是一种可以包含其他分区的分区类型。

**exterior routing protocol**（外部路由协议）外部路由协议是一种旨在用于自治网络之间通信的路由协议。

**extraversion code**（额外版本号）额外版本号是添加到 Linux 内核版本号的一串字符。它唯一地限定了版本号，以避免共享相同版本号的内核实例的模块之间发生冲突。

### F

**file ownership**（文件所有权）文件的文件所有权是指拥有该文件的用户账户。

**file permissions**（文件权限）文件权限是指授予用户、文件所有者组、文件所有者以及普通用户的权限（读、写和执行）。

**file system**（文件系统）文件系统是为了数据存储和检索而组织的分区。

**firewall**（防火墙）防火墙是一个阻止未经授权的流量进入或离开网络的系统或设备。

**forward zone file**（正向区域文件）正向区域文件是一个域名服务 (DNS) 配置文件，将主机名映射到 IP 地址。请参阅 *reverse zone file*（反向区域文件）。

**forwarding**（转发）转发是指将从一个网络接口接收到的数据包路由到正确的传出网络接口的过程。

**FSF** 自由软件基金会 (FSF) 赞助 GNU 项目和其他开源软件项目。

**fully qualified domain name**（完全限定域名）完全限定域名是主机名和域名的组合。它可以唯一地标识一台主机。

### G

**gateway**（网关）网关是一个提供访问网络或互联网途径的路由器。

**GNU project**（GNU 项目）GNU (GNU is not Unix) 项目旨在创建一个类似于 Unix 的开源操作系统。Linux 在分发时包含许多在 GNU 项目支持下开发的程序。

**GPL** GPL (GNU Public License) 旨在保留使用、复制和修改软件的自由。

**grace period**（宽限期）当用户超过了分配的磁盘配额时，用户可能会有一个宽限期，在此期间不强制执行配额。然而，宽限期结束后，用户无法再分配额外的磁盘空间。

**graphical mode installation procedure**（图形模式安装程序）Red Hat Linux 可以通过使用提供点选界面的图形模式安装程序来安装。

**group quota**（组配额）组配额是分配给一个组而非单个用户的磁盘空间配额。

### H

**hard limit**（硬限制）硬限制是用户可以分配的最大磁盘空间量。

**horizontal sync rate**（水平同步率）监视器的水平同步率是一个关键的运行参数。以不适当的水平同步率运行可能会损坏监视器。

**host address**（主机地址）系统的主机地址（或 IP 地址）唯一地标识该系统。

**host name**（主机名）系统的主机名是由系统管理员分配的名称。主机名在域内必须是唯一的。

### I

**image file**（镜像文件）镜像文件是包含可用作写入磁盘（尤其是启动盘）内容数据的文件。

**installation class**（安装类别）Red Hat Linux 允许您从四种安装类别中选择：GNOME 工作站、KDE 工作站、服务器或自定义。

**installation path**（安装路径）Red Hat Linux 允许您从两种安装路径中选择：安装或升级。

**installation type**（安装类型）Red Hat Linux 允许您从两种安装类型中选择：图形界面和文本界面。

**Intel architecture**（Intel 架构）具有所谓 Intel 架构的计算机通常被称为 IBM PC 兼容机。

**interior routing protocol**（内部路由协议）内部路由协议是一种旨在用于自治网络内部的路由协议。

**i/o port**（I/O 端口）I/O 端口是 IBM 兼容 PC 为与硬件设备通信而保留的特殊内存地址。

**IP address**（IP 地址）IP 地址是一个 32 位的数字，唯一地标识一台互联网主机。

**IRQ** 中断请求队列 (IRQ) 是一种能够处理设备发送信号的硬件设施。

### K

**kernel**（内核）内核是操作系统的核心组件。Red Hat Linux 以其内核——Linux 内核而命名。

**key**（密钥）密钥是加密程序用作访问代码的一串文本。

**kickstart installation**（Kickstart 安装）Kickstart 安装在尽可能范围内无需人工干预即可进行。由一个特殊的脚本控制安装过程。

### L

**LDAP** 轻量级目录访问协议 (LDAP) 可用于集中存储和管理与网络相关联的用户账户。

**library**（库）库是一个包含对象模块（称为库成员）的文件，这些模块可以与其他对象模块相结合以形成程序。

**linker**（链接器）链接器是一个可用于将对象模块和库结合起来形成程序的程序。

**link-state protocol**（链路状态协议）链路状态协议是一种维护网络地图（或至少是部分地图）的路由协议。

**Linux** Linux 是一个在很大程度上兼容 POSIX 的开源操作系统内核，它包括 Linux 内核以及 GNU 程序和实用工具。

**loadln** `loadln` 程序在 MS DOS 下运行，可以在无需系统 BIOS 帮助的情况下启动 Linux。

**log rotation**（日志轮转）日志轮转是一个管理用于日志文件的磁盘空间量过程。日志轮转涉及保留一系列跨越指定时间段的日志文件。

**logical block address**（逻辑块地址）逻辑块地址是一个表示磁盘驱动器扇区的数字。某些磁盘驱动器的几何结构使得 Linux 使用逻辑块地址比使用柱面-磁头-扇区地址访问更高效。

**logical partition**（逻辑分区）逻辑分区是包含在扩展分区中的分区。请参阅 *primary partition*（主分区）。

### M

**machine language**（机器语言）机器语言是给定处理器模型能够理解的操作码集，或者更广泛地说，是某种处理器模型能够理解的任何操作码集。

**major version**（主版本号）Linux 内核的主版本号变化速度比次版本号慢。目前 Linux 内核的主版本号是 2。

**map**（映射表）包含网络信息的 NIS (Network Information Service) 数据库被称为 map。

**masquerading**（伪装/网络地址转换）伪装是指用一个指定的 IP 地址替换 IP 数据包中发现的 IP 地址。

**minor version**（次版本号）Linux 内核的次版本号变化速度比主版本号快。偶数的次版本号分配给稳定内核，奇数的次版本号分配给开发内核。

**modular kernel**（模块化内核）模块化内核由多个称为模块的组件组成，其中一些模块可以动态加载。请参阅 *monolithic kernel*（单体内核）。

**module**（模块）模块是 Linux 内核的一部分（例如设备驱动程序），可以动态加载。

**monolithic kernel**（单体内核）单体内核由一个一次性全部加载的单一单元组成。请参阅 *modular kernel*（模块化内核）。

**mount point**（挂载点）挂载点是与可挂载文件系统相关联的目录。

**multi-boot installation**（多启动安装）多启动安装是指允许您在启动时从多个操作系统中选择其中一个的安装方式。

### N

**network address**（网络地址）网络地址是 IP 地址中对于给定网络上的所有主机都相同的部分。

**network class**（网络类）网络类是一种描述如何从 IP 地址中推导出网络地址的定义。例如，C 类网络的 IP 地址的前 24 位构成了网络地址。

**network installation**（网络安装）网络安装是指分发介质位于远程服务器上的安装方式。

**NIS** 网络信息服务 (NIS) 集中存储和维护网络信息，例如用户账户。

**NNTP** 网络新闻传输协议 (NNTP) 是一种用于传输互联网新闻组文章的协议。

**non-privileged port**（非特权端口）非特权端口是指端口号在 1024 到 65535 之间的端口。任何进程都可以访问可用的非特权端口。

**NTP** 网络时间协议 (NTP) 是一种同步系统时间的方法。

### O

**object code**（对象代码）对象代码是源代码和机器语言之间的一种中间形式。



## 6 术语汇表

**octet**（八位组）八位组是指由八个二进制位（bits）组成的序列。

**ordinary user**（普通用户）普通用户是指非特权用户，即 root 以外的用户。

**OSS** 开源软件 (OSS) 是以分发源代码形式发布的软件，以便人们能够理解并对其进行修改。

### P

**package**（软件包）软件包是一组文件的集合——包括程序、配置文件和数据文件——它们构成了一个软件程序，或一组相关程序，并作为一个单元进行安装。

**package file**（软件包文件）软件包文件是包含软件包的文件。

**package group**（软件包组）软件包组是一组在某种程度上相关的软件包。

**packet filter**（数据包过滤器）数据包过滤器是一种用于选择性地拦截符合特定标准的数据包的设施。

**PAM** 可插拔认证模块 (PAM) 是 Red Hat Linux 的一项设施，使得配置 PAM 感知程序的安全相关选项成为可能。

**partition**（分区）分区是分配用于存放文件系统的磁盘空间区域。

**partition type**（分区类型）分区类型是一个数字，代表该分区预期存放的文件系统类型。

**kernel patch**（内核补丁）程序或 Linux 内核的补丁级别是指最新应用的补丁的顺序编号。

**path**（路径）路径是一系列目录；路径中的每个目录都包含该序列中的下一个目录。

**performance-based exam**（基于操作的考试）基于操作的考试要求考生演示一项技能，而不是回答问题。

**plug and play**（即插即用）即插即用是一种 BIOS 和操作系统设施，旨在简化设备的安装。

**POP user**（POP 用户）POP 用户是指被授权通过 POP 访问电子邮件，但未被授权登录的用户。

**port**（端口）端口是用于 TCP/IP 通信的设施。端口的编号范围为 0–65535。

**PPP user**（PPP 用户）PPP 用户是指被授权通过 PPP 登录的用户。

**primary boot loader**（主引导加载程序）主引导加载程序是系统启动时执行的第一个加载程序。

**primary partition**（主分区）主分区被分配用于存放文件系统。参见 *extended partition*（扩展分区）和 *logical partition*（逻辑分区）。

**priority**（优先级）优先级是一个指定启动脚本执行顺序的数字，或者是一个决定在准备就绪的进程集中，哪个进程将获得处理器访问权并执行的数字。

**privileged port**（特权端口）特权端口是指编号为 0–1023 的端口；只有特权进程才能访问特权端口。参见 *port*（端口）和 *non-privileged port*（非特权端口）。

### R

**rawrite** `rawrite` 程序是一个 DOS 程序，允许您根据镜像文件写入磁盘镜像。

**Red Hat Certified Engineer (RHCE)**（红帽认证工程师）红帽认证工程师通过了 RHCE 考试，该考试评估执行基础 Red Hat Linux 系统管理任务的技能。

**Red Hat Hardware Compatibility List**（红帽硬件兼容性列表）红帽硬件兼容性列表标识了与 Red Hat Linux 兼容的硬件，并定性描述了兼容程度。

**Red Hat, Inc.** Red Hat, Inc. 是创建并分发 Red Hat Linux 的公司。

**regular expression**（正则表达式）正则表达式是一个字符串，用于指定一组被认为与该正则表达式匹配的字符串。

**Rescue mode**（救援模式）救援模式是一种特殊模式，提供帮助您修复损坏系统的设施。

**reverse zone file**（反向区域文件）一种将 IP 地址映射到主机名的域名服务 (DNS) 配置文件。参见 *forward zone file*（正向区域文件）。

**root partition**（根分区）根分区是其文件系统包含 /bin、/sbin 和其他必需目录的分区。

**route**（路由）路由是从源主机到目的主机的数据包传输路径。

**router**（路由器）路由器是一个将数据包沿适当路由转发的系统或设备。

**routing**（路由/路由选择）路由是将数据包沿路由传输的过程。

**runlevel**（运行级别）运行级别指定了当前处于激活状态的本地服务和网络服务的类型。

**runlevel script**（运行级别脚本）运行级别脚本是一个与程序或服务相关的脚本，在运行级别更改时运行，以便正确配置该程序或服务。

### S

**secondary boot loader**（次级引导加载程序）次级引导加载程序是一个将操作系统加载到内存并将其控制权移交给操作系统的程序。次级引导加载程序由主引导加载程序启动。

**service**（服务）服务是一个监听客户端请求并提供信息或采取指定操作的程序。

**share**（共享）共享是指提供给指定用户或主机的文件、目录或打印机。

**single-user mode**（单用户模式）单用户模式是一种旨在帮助系统管理员修复损坏系统的特殊模式。

**SLIP user**（SLIP 用户）SLIP 用户是指被授权通过 SLIP 登录的用户。

**socket**（套接字）套接字是一个由一对端口组成的 TCP/IP 通信设施。

**soft limit**（软限制）软限制是指可以暂时超过的磁盘配额。

**source code**（源代码）源代码是程序员工作的程序形式。

**stable kernel**（稳定内核）一个主要旨在修复漏洞且仅进行有限开发的内核。参见 development kernel（开发内核）。

**start of authority**（权威起始点）权威起始点是指对特定区域的域名服务 (DNS) 信息负有主要责任的主机。

**static IP address**（静态 IP 地址）静态 IP 地址是分配给主机的固定 IP 地址。参见 *dynamic IP address*（动态 IP 地址）。

**static linking**（静态链接）静态链接是将对象模块与所有必需的库成员进行链接，这样在加载生成的程序时，就不再需要引用库或动态链接成员。参见 *dynamic linking*（动态链接）。

**static routing**（静态路由）静态路由是一种手动执行路由表更改的路由技术。参见 *dynamic routing*（动态路由）。

**stratum**（层）层是一组相对于高精度时间基准具有相似逻辑网络距离的系统集合。

**stub**（存根）存根是一段充当占位符的代码。

**subnetting**（子网划分）子网划分是将一个网络划分为几个较小网络的方案。

**superblock**（超级块）超级块是一个特殊的数据块，描述了文件系统的内容和结构。

**supernetting**（超网划分）超网划分是将几个网络组合成一个单一、更大网络的方案。

**symmetric multiprocessing**（对称多处理）对称多处理是一种计算机可以包含多个处理器的方案，每个处理器执行相似的功能。

### T

**TCP** 传输控制协议 (TCP) 是构成互联网基础的协议族。

**TCP wrappers**（TCP 包装器）TCP wrappers 是 inetd 守护程序的一项设施，通过它可以将对服务的访问限制在指定主机内。

**temporary file**（临时文件）临时文件是指在较短时间内需要且在使用后可以删除的文件。

**text-based installation procedure**（基于文本的安装程序）Red Hat Linux 提供了一种基于字符模式图形和键盘的基于文本的安装程序。参见 *graphical mode installation procedure*（图形模式安装程序）。

**three-button emulation**（三键仿真）三键仿真是一项 X 设施，允许用户使用双键鼠标来访问与鼠标中键相关的函数。

**top-level domain name**（顶级域名）顶级域名是一组特殊域名之一，其中一个会被包含在每个域名中，例如 `.com`、`.edu` 和 `.gov`。

### U

**UDP** 用户数据报协议 (UDP) 是一种低级别的、无连接的 TCP/IP 协议。

**Unix** Unix 是一族具有共同特征的操作系统。Linux 是 Unix 家族的一员。

**unreliable protocol**（不可靠协议）不可靠协议是指执行有限或不执行错误检查的协议。此类协议的开销相对较低。

**user account**（用户账户）用户账户代表与计算机系统或网络授权用户相关的身份和权限。

**user group**（用户组）用户组是指一组指定的用户。文件所有权和权限可以分配给用户组。

**user private group**（用户私有组）用户私有组是一个只有一个成员的组，该成员与同名的用户账户相同。

**user quota**（用户配额）用户配额是与用户账户关联的磁盘空间配额。

**UUCP user**（UUCP 用户）UUCP 用户是指被授权访问 UUCP 服务，但未被授权登录到系统的用户。

### V

**version number**（版本号）程序的版本号是一个序数，指示该程序构建的近早程度。

**vertical refresh rate**（垂直刷新率）监视器的垂直刷新率是一个关键的运行参数。以不恰当的垂直刷新率运行可能会损坏监视器。

### W

**well-known port**（周知端口）周知端口是通常与某些 TCP/IP 服务关联的端口。周知端口列在 `/etc/services` 中。

**window manager**（窗口管理器）窗口管理器是一个 X 客户端，负责显示窗口的视觉外观和行为的许多方面，例如标题栏和关闭按钮。

### X

**X** *X，或 X Window System*，是随 Linux 分发的图形用户界面。

**X client**（X 客户端）X 客户端是以 X 作为用户界面的程序。

**X server**（X 服务器）X 服务器是与 X Window System 关联的视频驱动程序。

### Z

**zone file**（区域文件）一个将主机名映射到 IP 地址或反之的域名服务 (DNS) 文件。参见 *forward zone file*（正向区域文件）和 *reverse zone file*（反向区域文件）。
