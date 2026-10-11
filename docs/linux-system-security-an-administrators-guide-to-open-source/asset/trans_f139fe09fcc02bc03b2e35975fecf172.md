
## 建议

我们建议在新安装的系统中运行 `tiger`，以识别在生产环境中部署之前需要加固的任何项目。此外，还应定期在运行中的系统上运行 `tiger`，以查找变更。首先通过多次从命令行运行 `tiger` 来调整其设置，直到配置符合您的要求，并且您已经完成了必要的系统更改。然后通过 `tiger.cron` 安装并运行 `tiger`。运行额外的审计工具，例如 `tripwire`。保护您的日志文件，如果可能，请使用安全服务器或只读介质。

## 总结

我们试图涵盖 `tiger` 脚本的许多配置选项。`tiger` 是一套复杂的脚本和程序，但它可以帮助您发现基本的系统漏洞。

## 延伸阅读

- Farrow, Rik, UNIX 系统安全：如何保护您的数据并防止入侵者，马萨诸塞州雷丁，Addison-Wesley，1991 年。

## `tiger` 邮件列表

要订阅 `tiger` 邮件列表，请向 `tiger-request@net.tamu.edu` 发送邮件，主题设为 `subscribe`。

## `sendmail` 资源

有关 `sendmail` 的更多信息，请阅读以下优秀书籍：

- Costales, Bryan，与 Eric Allman 合著，《sendmail》，第 2 版，马萨诸塞州剑桥，O'Reilly & Associates, Inc.，1997 年。

还可以检查相关网站：

http://www.sendmail.org/

# 第 14 章

## 设置 Tripwire

希望您在将我们讨论的所有精彩内容实施到生产环境之前（测试和玩耍是可以的），您真的需要先执行*这个*。*这个*就是 Tripwire。

Tripwire 实用程序不会动态保护您的环境，但它将作为一个极其有价值的报警系统发挥作用。其目的是捕获系统中所有重要文件和目录的图像，然后，当您以比较模式运行它时，它会告知您是否有任何更改。通过这种方式，如果未经授权的用户通过添加后门或特洛伊木马攻破了您的系统，您将在下次运行 Tripwire 时得知此事。如果您正在考虑实施少数几种工具，Tripwire（或等效功能）*必须*在其中。如果您在网关上运行防火墙，或者使用超文本传输协议 (HTTP) 或 FTP 服务器或任何其他位于边界网络中的系统，您真的应该在那些系统上实施 Tripwire。此外，任何被视为任务关键、包含重要数据、充当服务器或以其他方式与环境的重要组成部分相关的系统，都应使用 Tripwire 进行服务。

特别是，在从原始来源安装系统及其所有额外软件之后，您希望使用 Tripwire 捕获系统的原始图像。在那之后，且仅在那之后，您的系统才准备好进入生产环境。在将该系统引入生产环境后，您将希望定期运行 Tripwire，但以一种不可预测的方式进行。这样的程序加上定期阅读系统日志文件，将使您警觉于绝大多数的系统入侵。

### TRIPWIRE 概览

Tripwire 实用程序在其功能和配置方面实际上相当直观。调用时，Tripwire 读取配置文件。配置文件告诉它需要注意哪些文件和目录，以及收集关于这些目录和文件的哪些信息。一旦通过以*初始化模式*运行 Tripwire 收集信息，这些信息就被放置在一个数据库中，该数据库需要安全存储。每当再次运行 Tripwire 时，它使用在数据库中找到的信息并将其与实际系统上的信息进行对比。这被称为*比较模式*。如果发现任何差异（更改），它会向您报告。所有这些更改都应彻底检查。如果识别出未经授权的活动，您将需要恢复系统（有关进一步详情，请参阅第 18 章）。如果更改是授权活动的结果，您将有机会更新数据库，以便未来的 Tripwire 比较运行不会报告相同的差异。更新是通过 Tripwire 的*更新模式*完成的。

图 14.1 说明了 Tripwire 的整体功能。我们将在以下部分中查看每种模式和配置文件，但我们需要从获取和安装 Tripwire 开始。

![](img/7933c44717ab0711177ea7153f959fc5_423_0.png)

图 14.1 Tripwire 的功能概览

### 获取和安装 TRIPWIRE

Tripwire 由普渡大学的 Gene Kim 和 Eugene H. Spafford 开发。Tripwire 的公开版本（版本 1.2）可从多个来源获得，包括：

- http://www.cs.purdue.edu/coast/ (COAST 存档)
- http://www.redhat.com/

这两个网站都包含数字签名文件。COAST 存档中的文件仅为源代码，而 Red Hat 网站同时提供源代码和 Intel 预编译版本。如果您下载这些版本，请务必检查 PGP 签名！您可以从 Tripwire Security Systems, Inc. (TSS) 获取 Tripwire 版本 1.3（正式称为 Tripwire 学术源代码发布版 1.3），地址为：

http://www.tripwiresecurity.com/

此版本包含许多错误修复和增强功能。特别是，它修复了版本 1.2 中使用 twdb_check.pl 所必需的数据库一致性问题。否则，它与版本 1.2 在本质上相似。因此，我们的讨论将适用于这两个版本，并在适当的地方注明差异。

Tripwire 版本 2.x 最近由 TSS 重新发布。TSS 为非商业用途免费提供此产品的二进制版本。它运行在 Red Hat 5.0 或更高版本上，并且是 RPM 格式。

不幸的是，TSS 提供的文件均无数字签名。这是版本 2.x 的一个特定问题，因为 TSS 仅提供二进制文件。因此，如果您打算使用该版本，请将其放在测试系统上，在上线之前监视任何异常行为。

### Tripwire 版本 1.2

由于 Tripwire 版本 1.2 随 Red Hat 5.2/6.0 一起发布（在 Power Tools CD 上，或从 ftp://ftp.redhat.com/ 获取），我们将使用该版本。Red Hat 6.0 上有两个 RPM 包——tripwire-1.2-2.src.rpm 包含源代码，tripwire-1.2-2.i386.rpm 包含二进制文件。对于 Red Hat 5.2，这些文件将是 tripwire-1.2-1.src.rpm（源代码）和 tripwire-1.2-1.i386.rpm（二进制文件）。Red Hat 6.0 的 RPM 包含次要错误修复（详情参见第 385 页示例 14-1 中提到的 /usr/doc/tripwire-1.2/ChangeLog 文件）；因此，即使您正在运行 Red Hat 5.2，也应使用这些软件包。

即使您打算重新编译源代码，您可能仍然希望获取这些 RPM，因为 Makefile 和某些源代码文件需要修改才能在 Linux 上运行。两个 RPM 文件都包含 PGP 2.6 签名，因此请务必按如下方式验证它们：

```
# rpm -Kv tripwire-1.2-2.src.rpm
# rpm -Kv tripwire-1.2-2.i386.rpm
```

如果您没有 Red Hat PGP 公钥，它可以获取自 CD 或 Red Hat 网站。

在下载并验证这些软件包上的签名后，按如下方式安装它们：

```
# rpm -ivh tripwire-1.2-2.src.rpm
# rpm -ivh tripwire-1.2-2.i386.rpm
```

所有源文件将以以下三个文件的形式最终位于 /usr/src/redhat/SOURCES 中：

- tripwire-1.2-rhlinux.patch
- tripwire-1.2.tar.Z
- tripwire-verify

tripwire-1.2-rhlinux.patch 文件包含在 Red Hat Linux 上编译所需的修改。该文件包含一个每日 cron 条目，当您提取 tripwire-1.2-2.i386.rpm 时，该条目也会被放置在 /etc/cron.daily 中。tripwire-1.2.tar.Z 包含实际的源代码。您需要解压缩并解压此文件。这样做后，您将得到以下三个文件：

- Readme
- T1.2.tar
- T1.2.tar.asc

阅读 Readme 文件。T1.2.tar.asc 文件包含 T1.2.tar 文件的 PGP 签名和 MD5 校验和，该文件包含源代码。您需要 Eugene Spafford 的公钥（可从 http://www.cs.purdue.edu/people/spaf 获取）来验证数字签名。完成后，从 T1.2.tar 中提取文件。默认情况下，这将把所有源代码放在目录 /usr/src/redhat/SOURCES/tripwire-1.2 中。即使您不打算重新编译软件，您也需要表 14.1 中识别的脚本（其位置相对于 /usr/src/redhat/SOURCES/tripwire-1.2 引用）。

文件 tripwire-1.2-2.i386.rpm 包含 Tripwire 的二进制文件。提取该软件包将生成示例 14-1 中显示的文件。我们建议您查看 /usr/doc/tripwire-1.2 目录中的文件，因为那里有很多有用的信息。请注意，Tripwire 配置文件 tw.conf 默认位于 /etc 中。正如我们将在本章中详细讨论的那样，此文件需要重新定位到只读文件系统中。/usr/sbin/tripwire 的情况也是如此，它是 Tripwire 引擎。/var/spool/tripwire 目录是数据库的默认位置，同样需要重新定位到只读位置。/usr/bin/sigen 实用程序允许生成不同的哈希值，并接收一个文件作为输入。在某些情况下，检查一个或少数几个哈希值是合理的，证明了需要这个独立实用程序。

