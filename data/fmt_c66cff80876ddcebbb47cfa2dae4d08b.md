
此命令将你的 Personal 文件夹的内容转换为 `personal.mbox` 文件。一旦转换了邮箱，你就可以使用邮件客户端的导入功能导入你创建的邮箱文件。从 mbox 文件导入邮件在前章节中已介绍。

# 使用 readpst 迁移 Outlook 邮件

Microsoft Outlook 将其文件夹存储在 PST 格式的文件中。PST 代表“个人存储表”（Personal Storage Table）。`readpst` 工具是 `libpst` 项目的一部分，可在 Ubuntu 存储库中使用，它你读取 PST 文件；提取它们包含的邮件文件夹、联系人信息、日历项目和其他数据；并创建可以随后导入 Evolution 的文件。

`libpst` 项目最初也是 SourceForge 上 `ol2mbox` (Outlook to mbox) 项目的一部分，正如 `libdbx` 项目一样。这种需求

# 第二部分：面向桌面用户的 Ubuntu

`libpst` 更改了新的维护者，并且一段时间以来 `libpst` 的主页位于 http://alioth.debian/projects/libpst，但目前 `libpst` 最新版本的所在地位于 www.five-ten-sg.com/libpst。对于 Ubuntu 用户来说，好消息是 Ubuntu 仓库中也提供了 `readpst` 工具，你只需要使用你喜爱的包管理工具安装 `readpst` 软件包即可——无需编译！

最新版本的 `readpst`（以及整个 `libpst` 项目）既可以读取由 Outlook 2003 之前的版本生成的 32 位 PST 文件，也可以读取由 Outlook 2003 及更高版本生成的 64 位 PST 文件。

在用用 `readpst` 工具从 PST 中提取 Windows 邮件和其他数据之前，请确保你已经知道要提取的 PST 文件的位置。

如果你遵循了本章较之前标题为“迁移场景概述”章节中的建议，你将拥有一个由 Outlook“导入和导出”命令生成的 PST 文件，该文件包含你“个人文件夹”（Personal Folders）的整个层次结构和子目录。如果你正在从 Windows 系统的备份进行工作，并使用使用 Outlook 存档机制创建的标准 PST 文件，则包含 PST 文件的目录（位于你的用户目录下）的默认位置是以下之一：

Windows XP 及其他系统：

- `Local Settings\Application Data\Microsoft\Windows\Outlook`

Windows Vista 及后续系统：

- `AppData\Local\Microsoft\Outlook`

一旦你定位了其中类型的 PST 文件，请创建一个目录来存放你将提取的文件，并执行 `readpst` 命令。以下是 `readpst` 的示例命令和相关输出（使用名为 `Windows-Stuff` 的目录——该目录必须已经存在——作为提取文件的位置）：

```
$ readpst -o Windows-Stuff 2007-export-backup.pst

Opening PST file and indexes...

Processing Folder "Deleted Items"

Processing Folder "Inbox"

Processing Folder "Outbox"

Processing Folder "Sent Items"

Processing Folder "Calendar"

Processing Folder "Contacts"

Processing Folder "Journal"

Processing Folder "Notes"

Processing Folder "Tasks"

Processing Folder "Drafts"

Processing Folder "RSS Feeds"

Processing Folder "Junk E-mail"

"Personal Folders" - 12 items done, 0 items skipped.

- "Inbox" - 45 items done, 0 items skipped.

* "Contacts" - 3 items done, 0 items skipped.

Processing Folder "Popular Government Questions from USA.gov"

Processing Folder "USA.gov Updates: News and Features"

* "Tasks" - 0 items done, 1 items skipped.

Processing Folder "Microsoft at Home"

* "Popular Government Questions from USA.gov" - 0 items done, 14 items skipped.

* "Calendar" - 1 items done, 0 items skipped.

* "Sent Items" - 2 items done, 0 items skipped.

* "USA.gov Updates: News and Features" - 0 items done, 11 items skipped.

* "Microsoft at Home" - 0 items done, 57 items skipped.

Processing Folder "Microsoft at Work"

Processing Folder "MSNBC News"

* "RSS Feeds" - 5 items done, 0 items skipped.

* "Microsoft at work" - 0 items done, 55 items skipped.

* "MSNBC News" - 0 items done, 24 items skipped.
```
