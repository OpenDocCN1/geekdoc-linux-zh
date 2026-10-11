
## 运行 logcheck

你应该定期更新 `logcheck.hacking` 和 `logcheck.violations` 文件，添加新发现的日志消息模式；或者更好的做法是，确保你在所有服务器上都安装了最新版本的 logcheck。此外，花点时间为这些文件添加专门针对你的服务器和系统需求的条目。例如，如果你运行 HTTP 服务器，请添加 Apache 的消息模式；如果你运行邮件服务器，请添加 sendmail 的模式。

请注意，默认情况下，Linux 版本的 logcheck 会扫描 `/var/log/messages` 文件以获取所有事件，因此请确保该文件确实接收到了所有应用程序的日志消息。你的 `/etc/syslog.conf` 文件中应包含以下行：

```
* .info /var/log/messages
```

虽然没有真正的配置文件，但实际的 logcheck shell 脚本（`/usr/sbin/logcheck`）可读性很强，且在开头部分有一些变量定义。我建议你只将

```
SYSADMIN=root
```

这一行修改为除 root 以外的其他用户名，前提是你有一个专门用于接收日志邮件的账户。

logcheck 使用 cron 来安排定期运行。请通过发出以下命令来确保你的系统确实在运行 crond（cron 守护进程）：

```
[ramon]$ ps aux | grep cron
root 403 0.0 0.4 1284 304 ? S Sep24 0:00 crond
```

安装时，logcheck 的 RPM 发行版会在 /etc 目录下创建以下文件：

```
/etc/cron.hourly/logcheck
```

此文件强制服务器上的 cron 任务在每小时整点执行 logcheck，从而导致每小时向服务器上的 root 账户发送电子邮件消息。该电子邮件消息包含关于过去一小时记录的安全违规和任何异常系统事件的报告。

列表 3.5 展示了该每小时报告的一个示例。在此报告中，logcheck 报告称有一个 SOCKSS 客户端未能正确向本地服务器进行身份验证，以及一个普通用户（ramon）执行了 su 命令来检查 /var/log/ 下的 messages 文件。

# 第78章 第3章 系统监控与审计

## 列表 3.5 logcheck 发送给本地 root 用户的示例电子邮件

From: root <root@redhat.example.com>
Message-Id: <200010012201.SAA16387@redhat.example.com>
To: root@redhat.example.com
Subject: Redhat.example.com 10/01/00:18.01 system check
Status: RO
Content-Length: 222
Lines: 8

Security Violations
====================
Oct 1 17:28:14 redhat Socks5[16296]: Auth Failed: (204.168.33.2:1196)

Unusual System Events
====================
Oct 1 17:28:14 redhat Socks5[16296]: Auth Failed: (204.168.33.2:1196)
Oct 1 18:17:15 redhat sudo: ramon : TTY=pts/3 ; PWD=/usr/doc ; COMMAND=/usr/bin/tail /var/log/messages
logcheck-1.1.1 ; USER=root ; COMMAND=/usr/bin/tail /var/log/messages

## swatch 与 logcheck 对比

swatch 和 logcheck 在系统防御中都有一席之地。虽然 swatch 是更好的实时日志通知工具，但 logcheck 提供了一个直观、易于安装的工具，你可以用它来创建自定义报告，供管理人员定期审查。

无论选择哪种工具进行实现，至关重要的是选择一个有足够时间并愿意投入足够精力仔细阅读报告的接收者。这些工具旨在帮助解决系统安全中最繁琐的方面之一，但最终，人工审查和适当的响应是无法替代的。

## 文件完整性审计

确保系统可执行文件、配置文件和日志文件的完整性对于成功的安全防御至关重要。试想一下，如果入侵者设法用一个特洛伊木马版本替换了一个常用文件（如 login）。如果攻击者能够创建一个表现得与原文件完全一样的特洛伊木马登录程序，这种攻击可能永远不会被检测到。由于你无法轻松地“查看”可执行文件的内部，唯一能标记这种妥协的方法是将当前登录实用工具的签名与系统首次安装时获取的签名进行比较。

这些签名是加密哈希函数，其特性确保两个不同的文件绝不会产生相同的哈希值。因此，这些文件中任何最小的修改都可能导致签名截然不同。这是大多数文件完整性保证工具背后的基本原理。在系统联网之前对所有可执行文件进行签名快照，你可以创建一个基线，最好将其存储在只读多写的介质上（以确保其不被篡改）。然后你可以定期将这些签名与文件的当前状态进行比较，并适当处理任何更改。

接下来的部分将介绍 tripwire，这是最流行的 Linux 文件完整性保证实用程序，并解释其作为全面系统安全策略一部分的安装、配置和使用。

### tripwire

tripwire 诞生于 1992 年，由普渡大学的 Gene Safford 博士主持。tripwire 是文件完整性保证领域提供的第一个工具。1999 年，该工具的开发和维护工作由 Tripwire, Inc. 接手，这是一家由 Gene Kim 主导的商业机构，他是 tripwire 的原始开发者之一，当时在普度为 Safford 博士工作。

#### 安装 tripwire

尽管他们提供基于 tripwire 概念的完全支持的商业产品线，但 Tripwire, Inc. 允许免费下载其工具的 Linux 版本。你可以在 www.tripwire.com/downloads 获取包含发行版的 gnu-zip 文件。下载归档文件后，使用以下命令解压并提取生成的 .tar 文件的内容到当前目录：

```
[ramon]$ gunzip Tripwire_221_for_Linux_x86.tar.gz
[ramon]$ tar xf Tripwire_221_for_Linux_x86.tar
[ramon]$ rm Tripwire_221_for_Linux_x86.tar
[ramon]$ ls -l
total 8814
-r---r-----   1 ramon   users      9825 Jan 11  2000 license.txt
-r---r-----   1 ramon   users      7060 Jan 11  2000 README
-r---r-----   1 ramon   users     23065 Jan 11  2000 Release_Notes
-r---r-----   1 ramon   users      3300 Jan 11  2000 install.cfg
-r---xr-xr-x   1 ramon   users     31919 Jan 11  2000 install.sh
drwxr-xr-x   2 ramon   users      1024 Jan 11  2000 pkg
```

在继续安装之前，请查看 `install.cfg` 文件，该文件包含控制安装过程的多个环境变量。表 3.2 显示了你应检查的选项及其默认设置。我建议你更改 **TWROOT** 的值，将其设置为通常安装系统工具的位置（例如 `/usr/local/`*tripwire*），因为大多数其他环境变量都是基于此基础目录构建的。

> **注意** 尽管我有此建议，但在这些示例中我使用 `/usr/TSS`，以使文本与其他 *tripwire* 文档更兼容。

**表 3.2** *tripwire install.cfg* 环境变量

| 变量 | 描述 | 默认值 |
| :--- | :--- | :--- |
| **TWROOT** | 根目录 | `/usr/TSS` |
| **TWEIN** | 程序可执行文件和配置文件的位置 | `${TWROOT}/bin` |
| **TWPOLICY** | 策略文件的位置 | `${TWROOT}/policy` |
| **TWMAN** | *man* 手册页的位置 | `${TWROOT}/man` |
| **TWDB** | 数据库的位置 | `${TWROOT}/db` |
| **TWSITEKEYDIR** | 用于保护配置和策略文件的密钥位置 | `${TWROOT}/key` |
| **TWLOCALKEYDIR** | 用于保护数据库文件和报告的密钥位置 | `${TWROOT}/key` |
| **TWREPORT** | 完整性检查结果的位置 | `${TWROOT}/report` |

接下来，只需以 root 用户身份运行提供的 *install.sh* 脚本：

```
[ramon]$ sudo ./install.sh
```

在安装过程中，系统会提示你输入一个口令短语，以保护配置和策略文件的保密性和完整性。你还需要输入最终将包含你所选择监控的系统文件签名的数据库的名称。请选择一个由至少 16 个字符组成的优质口令短语。（*tripwire* 接受多达 1023 个字符的口令短语！）

