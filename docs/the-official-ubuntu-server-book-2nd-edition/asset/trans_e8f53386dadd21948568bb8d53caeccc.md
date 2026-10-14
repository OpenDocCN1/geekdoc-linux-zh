

host。你可能还会看到像 ADVANCED USAGE、EXAMPLES、OPTIONS 和 SUMMARY 这样的章节，如果存在的话，每一个都非常有用。

文档文件是一个很好的资源，尤其是在你安装了新软件包并且不确定下一步该做什么的时候。许多系统管理员在 Ubuntu 服务器上安装新程序时做的第一件事就是阅读 /usr/share/doc/<packagename> 下的 README.Debian.gz 文件。例如，你可以使用 sudo zless /usr/share/doc/apache2.2-common/README.Debian.gz 来阅读 Apache 2.2 通用文档，并在完成后按 Q 退出。对于某些程序和软件包，可能只有一两个文档可用，但其他软件包有很多优秀的文档，有时在子目录中，就像在 /usr/share/doc/apache2.2-common/examples/apache2/apache2.conf.gz 找到的 apache2.conf 文件示例一样。

每当你有疑问时，花点时间挖掘一下，你可能会在不必向任何人提问甚至在服务器之外查找文档的情况下发现答案。

## Local Community Teams

有些人更喜欢面对面的互动。这种选择对于非专业用途来说既有趣又实用，例如在家中拥有服务器的业余爱好者级别的爱好者，或是希望找到一起学习的人的大学生。Local Community，或 LoCo Teams，在世界各地运营。它们的许多规划和协调都是通过各自的邮件列表、IRC 频道和论坛在线进行的（通常作为前面讨论的主要 Ubuntu 论坛中的子论坛）。在许多地方，LoCo Teams 使用其他语言运营，这可能更适合母语非英语的用户。

LoCo Teams 通常会安排聚会来讨论新发展、互相帮助解决技术问题，或只是为了与有相似兴趣的人一起度过愉快的时光。许多团队会在新的 Ubuntu 版本发布前后举行特别聚会，称为“发布派对”或“安装节”，以庆祝完成一个发布周期，同时安装或升级他们的操作系统，并帮助用户在需要时将 Ubuntu 安装到他们的设备上。有关 LoCo Teams 的更多信息可以在 https://wiki.ubuntu.com/LoCoTeamList 找到。

## Other Languages

前面提到的几个资源为不以英语为母语的人提供了其他语言选项。Ubuntu 作为一个发行版的初始和持续重点之一就是让尽可能多的人在全球范围内使用 Ubuntu，这意味着将软件界面翻译成其他语言，并为非英语使用者提供在其母语中找到优质支持的途径。

工作尚未完成，但 Ubuntu 在非常多的语言中提供支持和安装选项。前面列出的大多数资源在其网页上都包含其他语言选项。这些包括论坛、IRC 频道、LoCo Teams 等等。更多信息请查看 www.ubuntu.com/support/community/local/language。

## Tech Answers System (Launchpad)

Canonical 还参与了 Ubuntu 之外的项目，包括他们的出色协作和代码托管平台服务 Launchpad（https://launchpad.net），该平台被大量软件项目使用，包括 Ubuntu。Launchpad 为代码开发、错误报告甚至问答提供了一个中心位置。它不如网络论坛那样完整或用户友好，但对于更高级的用户来说是一个极好的资源。

以下是 Ubuntu 相关问题的网址：https://answers.launchpad.net/ubuntu。

## Bug Reporting

有时你会遇到任何文档中都未涵盖且似乎找不到帮助的问题。这可能是你发现了程序中的缺陷或错误。恭喜！为了帮助开发人员完成他们的任务并使 Ubuntu 尽可能正常工作，你可以提交错误报告。这将直接通知维护特定软件包的人员有关问题。他们随后会检查报告，尝试重现该行为，如果确认是问题，就会着手尝试修复它。

