
视觉效果。在过去的一年或里，这一领域取得了实质性的发展。现在公司在向客户推销使用 Linux 时，可以指出这些新的支持来源。以下是最重要的在线支持来源，包括商业支持和用户社区支持。

## 配置支持

早期 Red Hat 的用户发现，该公司提供的支持非常令人失望，仅限于安装问题，而且往往响应不及时。Red Hat 网站包含一个以前回答过的问题的数据库，但搜索引擎的问题经常导致该数据库无法检索。

在 5.1 版本发布导致销量大幅增长后，Red Hat 开始重组其支持计划。他们改进了安装支持，并重新设计了在线数据库。除了提供基于 Web 的支持，还通过电子邮件和电话提供支持。从 Red Hat 7.0 开始，这种支持在 Red Hat 的标准版（Standard Edition）、豪华版（Deluxe Edition）和专业版（Professional Edition）中提供。每个级别都提供 90 天的 Web 或电子邮件支持。此外，还有针对安装后问题的支持合同和按次支持服务。

一些第三方公司在其网站上提供可搜索的支持数据库，他们鼓励您将其作为第一级支持。许多相同的公司还提供更正式的支持形式，如 24/7 电子邮件支持、电话支持和基于 Web 的支持，每项旨在实现极快的响应。在问题解决之前，您可能需要与支持人员交换几个邮件，但这一切可以在几小时内完成。支持网站通常有基于 Web 的表单来收集所有必要数据，并将其传输给支持工程师，工程师通过电子邮件或电话进行回复。电话支持并不打算作为支持的主要渠道。

某些第三方支持网站（例如 http://linux-support.net/ 企业支持）提供按小时或按天计费的电话和基于 Web 支持，取决于解决特定问题需要多久。基于 Web 的支持通常比电话支持便宜得多。同一公司还通过 http://support.marko.net/ 的免费 Linux 支持（Free Linux Support）提供由志愿者工程师提供的支持。工程师的表现受到监控，表现最好的工程师将获得企业级 Linux 支持（Enterprise Linux Support）的付费职位。

其他第三方支持网站以及如 Red Hat (http://www.redhat.com/apps/support/) 和 Caldera (http://www.caldera.com/) 等公司提供按次计费的支持，无论解决问题花费的时间长或短，每个问题的费用都是固定的。

每次事件的费用差异很大。分发商通常在购买盒装发行版后的一段时间内提供免费的安装支持。

此外还有传统的支持合同，承诺在支付固定金额后在规定期限内支持任何问题。这些合同规定了电话服务时间以及预期的响应时间。

## 定制 Linux 开发

1998 年，LinuxCare (http://www.linuxcare.com) 开始为企业及个人提供不区分发行版的支持计划。LinuxCare 的主要业务是为企业客户开发定制的 Linux 软件。他们在 Linux 内核扩展、系统优化、设备驱动程序开发和应用程序移植方面提供帮助。他们还提供 Linux 安全、网络管理和通用项目管理领域的咨询服务。

少数几家 Web 公司，如 Linux Corporate Consulting (http://www.corplinux.com) 和 Linux Consulting (http://www.linux-consulting.com/ )，提供基于付费的支持服务，形式包括定制化的 Linux 服务器和客户端机器、Linux 系统管理工具和脚本、专用 Linux 软件以及 Linux 维护。顾问公司的数量正在快速增长。只需简单的网上搜索，就能找到开发您所需的任何 Linux 相关软件的顾问。

## 通用 Web 支持

几乎每个发行版都为该发行版的用户或其他有特定发行版问题的人提供至少一个邮件列表。消息发送到相应的列表，列表处理器根据需要将它们发送给该列表的其他成员。这是获取支持信息的一种非常有效的方法。您只需将问题通过电子邮件发送列表；其他人阅读您的帖子并将回复通过电子邮件发送回列表。有时列表处理器会创建列表的摘要版本（digest version），这意味着您不是单独接收每封邮件，而是在等待队列达到容量时收到一封组合帖子。

Red Hat 使用名为 redhat-announce-list、redhat-watch-list 和 redhat-list 的列表。该名称意味着发布影响 Red Hat 社区的事件。观察列表（watch list）向成员提醒安全问题，而红帽 列表用于通用问题。redhat-list 提供摘要格式。有关加入这些列表的信息可以在 http://www.redhat.com/mailing-lists 处获得。

Debian 发行版的列表多到无法一一列名，但您可以在 http://www.debian.org/MailingLists/subscribe 找到关于它们的信息以及如何订阅。

Core Linux 有若干个新闻组：通用（General）、硬件兼容性（Hardware Compatibility）、安装（Installation）、网络（Networking）、打印（Printing）、设置/配置（Setup/Config）、德语（German）和其他语言（Other Languages）。要了解这些新闻组的情况，请查看 http://linux.corel.com/support/online.htm 上的信息。

Slackware 有两个基本列表：slackware-announce 和 slackware-security。也都提供摘要格式。更多信息可以在 http://www.slackware.com/lists 找到。

SuSE Linux 也有几个邮件列表，包括用于发布的 suse-announce、用于通用讨论的 suse-linux-e、suse-security 以及 suse-security-announce。有关这些列表的信息可以在 http://suse.com/ 处获得。

## 命令行工具

Linux 许多命令行工具来帮助您完成管理工作。本节介绍了帮助您更有效地使用命令的命令行技术，如管道（pipes）、重定向、通配符和波浪号。正如您所看到的，所有这些功能都由 shell 提供，对于 Linux 来说，就是 Bash shell。

### Bash 命令行功能

分配给用户的 shell 是该用户会话的命令解释器。命令从标准输入读取并由 shell 以特定方式进行解释；相同的命令在不同的 shell 中可能会有不同的解释。Linux 中的默认 shell 是 Bourne Again Shell，即 Bash。Bash shell 包含了 Bourne shell、Korn shell 和 C shell 的功能。Bash 从 .bash_profile 和 .bashrc 文件中读取配置，这些文件将在第 5 章结合用户特定启动脚本的背景进行进一步讨论。

Bash 像其他 shell 一样，具有某些特性，我们在此进行讨论。这些包括它对环境变量（environment variables）、管道和重定向、通配符（wildcards）、波浪号（tilde）以及历史列表（history list）的使用。

### 环境变量

环境变量是字符串，由 Bash 或其他程序设置，使其他程序可以使用这些数据。这些字符串被称为“环境”变量，是因为它们是全局可访问的，因此是环境的一部分。在 Red Hat Linux 的 /etc/profile 文件中设置了以下变量：

```
PATH
PS1
USER
LOGNAME
MAIL
HOSTNAME
HISTSIZE
HISTFILESIZE
INPUTRC
CALENDAR_DIR
```

PATH 变量在多个级别上被重新定义，因为不同的用户需要访问不同的文件和目录。在 Bash shell 中设置环境变量有两个步骤：设置值然后将其导出（export）。有时您会看到这是两个独立的命令：

```
HISTSIZE=1000
export HISTSIZE
```

