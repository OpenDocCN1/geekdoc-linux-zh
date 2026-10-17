
这种情况发生在 Red Hat Linux 8.0（Psyche）上。我在 Red Hat Linux 发行版 7.3 和 7.1 上也遇到了相同的问题。但当我尝试安装 Red Hat Linux 7.0 时，它毫无痛苦地安装，没有任何喊叫和哭泣。有谁在那里（或更具体地说在 Red Hat Inc.）能请解释一下到底发生了什么，或者 Red Hat Linux 7.0 有什么特别之处，其他版本没有？我仍在试图弄清这个问题！

## Q11. 我读了上面的 PR（问题报告）。我的 PC 上也安装了 FreeBSD 和 OpenBSD 操作系统。但我想在我的系统上安装除 Red Hat 之外的 Linux 发行版。你建议哪一个？

Ans11: 如果你已经阅读并理解了上面的 PR，那么你尝试在系统上安装哪个 Linux 发行版根本毫无意义。我在尝试在测试计算机上安装 Mandrake 9.0 以及 SuSE 7.0 时也遇到了类似问题。Mandrake Linux 管理创建分区、格式化它们，但在安装软件包时也惨败。SuSE 7.0 在一开始就崩溃了！在不久的将来，我想测试 Red Hat Linux 9 在此类系统上的完整性！

## Q12. 在我的计算机上安装 FreeBSD 4.X-RELEASE 时，FreeBSD `fdisk`（或 `disklabel`）使用了 `'X'` 分区名称而不是 `/dev/ad[0-3]s[1-4]n` 标记方案。嘿！到底发生了什么？那个 `'X'` 代表什么？

Ans12: FreeBSD 操作系统软件允许每个切片 7 个分区（`c:` 保留用于整个硬盘空间）。如果你在 PC 上创建了太多分区，FreeBSD `fdisk` 会使用 `'X'` 分区而不是有效的分区名称，例如 `/dev/ad0s1a`。如果你有一个标记为 `'X'` 的分区，你必须立即删除它，而不要继续进行。如果不删除此分区，FreeBSD `disklabel` 会让你继续整个安装，然后当你最终完成完整安装后，当你的系统启动时，你会遇到错误并被放入单用户模式进行维护。因此，换句话说，如果你不删除标记为 `'X'` 的分区，FreeBSD 将无法完成启动序列。相反它会显示错误消息并进入单用户模式。

Previous    Home    Next

## 5. 结论

各位朋友，这就将我们带到了创建配置了三种现代操作系统的多启动系统的旅程的终点。假设你已按照本指南的每一步操作并且一切顺利，请允许我祝贺你的成功。如果出现问题，请确保阅读相关操作系统的文档和手册。否则你也可以随时参考在线手册和资源。

请务必浏览以下链接：

- Distribution specific Official Red Hat Linux Installation and Upgrade manuals
- Linux Kernel resources
- Linux Loader (LILO) and other boot loader questions
- Red Hat Linux Hardware questions

对于专门涉及“多启动”的在线手册，我认为以下是最好的：

- Installing and Using FreeBSD With Other Operating Systems
- An excellent page explaining booting process and methodologies.

最终，尽管如此，任何你可能发现的错误或遗漏的责任在我，我独自承担，所以请将你的不满发送到 subhasish_ghosh@linuxwaves.com。对于希望发送 PR（问题报告）的人，请确保发送足够有效且相关的信息供我使用。如果你只是发送类似“这搞砸了！”、“那不工作！”之类的邮件，我无法帮助你。尝试发送详细的 PR。你的评论、建议和更正很可能会反映在本指南的下一个版本中。谢谢！
