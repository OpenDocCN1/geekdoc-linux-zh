
SuSE 提供了从服务器到桌面的产品，从家庭用户到企业级。一如既常，我关注桌面。你可以在其网站探索完整的 SuSE 产品：`www.novell.com/products/suselin/`

SuSE 提供的桌面版本包括：

- SuSE LiveEval：随书附带的 SuSE LiveDVD。如有必要，你可以从 `www.novell.com/products/suselinux/downloads/suse_linux/` 下载此版本——只需将其刻录到 DVD 并启动即可无需安装进入 SuSE 环境。
- OpenSUSE 10：从 `opensuse.org` 提供的 SUSE Linux 免费下载。它是五个光的内容，即使你有高速连接，下载也可能需要几个小时。
- SuSE Linux 10：你可以购买的盒装版，包含了 OpenSUSE 无法包含（出于许可原因）的额外软件，以及一套厚手册。

## 使用 Ubuntu

Ubuntu Linux (`www.ubuntulinux.org`) 与本文讨论的其他发行版相比是一个新成员。大多数新发行版需要长时间才能获得广泛的支持，但 Ubuntu 人气急剧上升。这又是一个基于 Debian 的发行版，尽管它的安装过程不像其他版本那样专门针对初学者。

遗憾的是，我们随书提供的 DVD 遇到了空间问题，不得不将 Ubuntu 从 DVD 中移除。不过，选择 Ubuntu 的原因之一你可以：

- 从网站下载。如需，点击主页上的 `Download` 链接，找到标记为 `Download Sites` 的部分。在下方，点击地理位置上离你最近的位置，系统将为你提供下载文件。该发行版只有一张 CD，因此它是最容易在线获取的版本之一，只需访问网站、点击 `Download` 并按照说明操作即可。
- 在下一个版本发布时申请免费邮寄一套 CD 给你。如需，点击主页上的 `Spitit - Free CDs` 链接。创建一个新账户，创建好你的账户，登录，并完成剩余的磁盘请求过程。

### 安装 Ubuntu

Ubuntu 有两个版本：LiveCD（不需要安装）和 Install CD（需要安装）。安装版本是随书 DVD-ROM 中包含的那个，我将在这里重点介绍此版本的安装。我想重申的是，这可能是书中涵盖的所有发行版中最困难的安装。如果你对双系统启动等问题感到不适，强烈建议将此发行版安装在一台可以独用的电脑上。

要安装 Ubuntu，请按照以下步骤操作：

- 1. 将 CD-ROM 放入 CD-ROM 驱动器。
- 2. 重启你的电脑。

如果你的电脑忽略了 CD，你需要更改 BIOS，让它在查找硬盘之前检查 CD-ROM 驱动器。（更多信息请参见第 2 和第 3 章）。Ubuntu 安装界面出现。
- 3. 按 Enter 开始安装。

文本快速闪过，然后出现选择语言（Choose Language）屏幕。
- 4. 如果不想使用英语，请选择一种语言。准备好后，按 Enter。

出现选择位置（Choose Your Location）屏幕。

## 第 4 章：安装其他 Linux 发行版

- 5. 如果你不在美国，选择相应的国家并按 Enter。

出现选择键盘布局（Select A Keyboard Layout）屏幕。
- 6. 如果你有多个选项，请选择最合适的一个。准备好后按 Enter 继续。

安装程序定位你的 CD-ROM 驱动器——如果在扫描时看起来像冻住了，请等待一分钟左右，它可能会恢复——然后自动检测更多硬件。最后出现配置网络（Network）屏幕。
- 7. 如果机器还没有名称，请为它输入一个名称并按 Enter。

如果已经填写，请忽略。你的 ISP（互联网服务提供商）或网络管理员可能要求你使用特定名称，以防线路为空。（如果你没主意，可以留空或胡编一个。）按下 Enter 后，将进行更多自动检测，最终出现磁盘分区（Partition Disks）屏幕（见图 4-12）。

![](img/d01c7c9abe7acbcb8b5f8f79e6511f25_100_0.png)

图 4-12：Ubuntu 5.10 分区屏幕。
- 8. 参考你在第 2 章的笔记，选择你想使用的分区选项，然后按 Enter。

三个主要选项是：删除整个磁盘（Erase Entire Disk）、删除整个磁盘并使用 LVM（Erase Entire Disk and Use LVM），或手动编辑分区表（Manually Edit Partition Table）。如果你要删除整个磁盘，我建议尽可能选择 LVM 选项。由于你选择了手动编辑分区表选项，你可能实际上需要自己编辑分区表，因为这是困难的。

如果你选择此选项，将出现：
- 9. 如果你有足够的空间，请选择你想要删除，并按 Enter。
- 10. 如果你有足够的空间，请选择你想要删除的磁盘分区。
- 11. 如果你有足够的空间，请选择你想要。
- 12. 如果你有足够的空间，请选择你想要删除的磁盘。
- 13. 如果你有足够的空间，请选择你想要删除。
- 14. 如果你有足够的空间，请选择你想要删除的- 分区，并按 Enter。
- 15. 如果你有足够的空间，请选择你想要。
- 16. 如果你有足够的空间，请选择你想要。
- 17. 如果你有足够的空间，请选择你想要删除的- 磁盘的 分区，并按 Enter。
- 18. 如果你有足够的空间，请选择你想要。
- 19. 如果你有足够的空间，请选择你想要。
- 25. 选择完成分区并写入磁盘（Finish Partitioning and Write Changes To Disk）并按 Enter。

出现一个警告。
- 26. 仔细检查你的选择，如果满意选择 Yes，如果想返回更改则选择 No。然后按 Enter。

系统设置分区、安装 Linux，然后带你时区配置（Time Zone Configuration）屏幕。
- 27. 选择你的位置并按 Enter。

出现设置用户密码（Set Up Users And Passwords）屏幕。

### 第一部分：入门阶段

28. 输入你希望主账户拥有的真实姓名或昵称（不是管理员账户），然后按回车。

出现“设置用户和密码”（Set Up Users And Passwords）屏幕。
29. 输入你想要使用的登录账号，然后按回车。

出现“设置用户和密码”（Set Up Users And Passwords）屏幕。
30. 在你的登录密码处，按回车，然后在第二个屏幕上重复此过程。

有关如何创建强密码，请参阅第 3 章。两次完成后，安装程序会在后台进行一些设置并弹出光盘。
- 31. 将 CD-ROM 光盘从驱动器中取出并按回车，允许安装程序重启机器。

机器重启后，它将尽可能地安装软件。如果你连接了互联网，它将下载并添加相关内容。当此过程完成后，你将看到 Ubuntu 登录界面。使用你在安装过程中创建的账户登录。

## 关于不同的 Ubuntu 版本

Ubuntu 有三个版本：

- 安装版：本书的版本可以安装在你的机器上。
- LiveCD 版：有关这些是什么以及如何使用的更多信息，请参阅本章稍后部分的“使用 LiveCD 和 LiveDVD”章节。
- 组合 DVD：这些 DVD 实际上是为那些在许多不同类型的硬件上安装 Ubuntu 的人准备的。如果你只想在 PC 上安装，不需要 DVD。

## 使用 Xandros 消除挫败

Xandros (`www.xandros.com`) 是另一个商业发行版，专门为从 Windows 世界转向 Linux 的人员设计；特别是，它设计用于能与工作场所现有的 Windows 网络良好集成。它是另一个基于 Debian 的发行版，并不是为那些想要成为 Linux 极客设计的。相反，它专注于只想完成工作的人。

Xandros 还特别设计用于让从 Windows 到 Linux 的过渡尽可能简单。因此，它提供了与 Windows XP 类似的布局和功能。Xandros 引入的一个方便工具是 Xandros Networks 工具，你可以通过双击桌面访问它。Xandros Networks 让你查看 Xandros 的最新新闻，并浏览软件在线商店（某些软件对注册用户免费）。通过 Xandros Networks 下载和安装仅需几次点击。

随书附带 DVD-ROM 包含的 Xandros 版本是开放发行版（Open Circulation Edition）。你可以将此磁盘映像刻录到 CD-ROM，然后使用下一节中的说明进行安装。

如果你决定购买 Xandros，你有几个选择：

- 购买一个并让其将实体盒寄给你。
- 在商店购买盒装。你可以通过访问 `www.xandros.com/partners/channel-partners.html` 找到销售 Xandros 的地点列表。
- 购买预装了 Xandros 的电脑 (`www.xandros.com/partners/oempcs.html`)。

## 安装 Xandros

要安装 Xandros 3 的开放发行版，请按照以下步骤操作：
