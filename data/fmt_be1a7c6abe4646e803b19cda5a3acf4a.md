
下载最新版本的免费版本（或购买商业版本）。在向 Tripwire, Inc. 提供一些联系信息后，可以从以下网站下载免费版本。尽管该版本有一些限制，但该公司已经在 GPL 协议下发布了 Linux 版本的 Tripwire 源码。由于美国的出口限制和许可限制，它无法放在 CD-ROM 或网站上。请注意，你将只会获得二进制文件。他们声称仅支持 Red Hat。它不需要 RPM 且可以在其他发行版上运行。为此目的，你将在从 `www.tripwire.com/downloads/` 下载后，在一个新建的空目录（如 `tripwire`）中操作。

下载将在你的目录中留下一个 gzipped tar 文件。使用常规命令解压并提取出它：

```
gunzip Tripwire_221.tar.gz
tar -xovf Tripwire_221.tar.gz
```

或者

```
tar -xzovf Tripwire_221.tar.gz
```

以 root 身份执行命令

```bash
./install.sh
```

它将检查系统上需要的程序，如 `tar`、`awk` 和 `vi`，这些程序应该存在于每个标准的 Linux 系统中。它会要求你阅读并接受许可。然后它会向你要站点和本地的 Tripwire 密码密码（passphrases）。每个密码可能多达 1024 个字符。Tripwire 不会拒绝易于破解的密码。请选择难以破解的良好密码，正如第 41 页“密码——良好安全的关键点”中讨论的那样。在配置过程中，你会被要求多次输入密码口令，因为它会调用各种需要密码口令以确保安全的 Tripwire 程序。默认情况下，它会在 `/usr/TSS` 下创建 Tripwire 系统。它会建议你检查并移除明文形式的 Tripwire 配置文件。

```
/usr/TSS/twcfg.txt
```

然后它会突然结束，让你阅读发布说明并祝你生活愉快。策略存储在 `/usr/TSS/policies` 下。`twpol.txt` 文件控制 Tripwire 将监控哪些内容以及对每项内容的预期。它被很好地提到，它声称理解指定的日志文件会增长，此时花些时间编辑此文件是一个好主意。否则，之后的代价将是巨大的。使用以下命令安装文档：

### 17.2.2 使用 Tripwire

```
cd /usr/TSS/man
man4/* /usr/local/man/man4/
man5/* /usr/local/man/man5/
man8/* /usr/local/man/man8/
```

一旦编辑了 `twpol.txt` 文件，就是时候创建该文件的安全版本了。Tripwire 文档说“确保你正在运行的系统完整性没有被破坏”。它进一步建议操作系统（Linux）和应用程序文件应从原始介质（CD-ROM）安装以获得干净的基准；即保证没有任何木马。好吧，除非你想重新格式化磁盘并重新开始，否则现在做已经有点晚了。正如第 700 页“通过 RPM 加速检查”所讨论的，使用 RPM 来验证已安装包未被篡改。

执行命令

```bash
cd /usr/TSS/bin
twadmin --create-polfile ../policy/twpol.txt
```

以创建该文件的加密版本，并将其放在 `/usr/TSS/policy/twpol.txt`。现在，使用以下命令初始化数据库：

```bash
tripwire --init
```

使用此命令测试电子邮件：

```bash
tripwire --test --email
```

要运行文件系统检查（检查文件系统的更改），执行命令

```bash
tripwire -m c
```

或者

```bash
tripwire --check
```

它将花费几分钟时间检查系统上的所有文件，将报告输出到标准输出，并存储在 `/usr/TSS/report/hostname-date.twr`。以后任何时候都可以以下命令生成该报告的副本：

```
twprint --print-report -r report_file.twr
```

## 17.2 Tripwire 653

细节可以通过 `-t` 标志指定，参数范围在 0 到 4 之间。数字越大，细节越详细。以下内容适合 root 的 crontab 条目，在你正常到达办公室之前（在白天负载开始之前）调用：

```bash
/tripwire -m c -r /usr/TSS/report/nightly.twr \
2>&1 | mailx -s TRIPWIRE
```

在你早上查看它（如果出现了比常的日志信息）后，然后执行命令

```bash
tripwire -m u -r /usr/TSS/report/nightly.twr
```

它会“弹出”编辑器，其中每个更改的条目都有一个 `[x]` 表示默认将数据库更新为新更改的版本。如果你将 `x` 替换为空格，则不会更新该条目的数据库。对于未经授权或需要进一步研究的更改，你应该将 `[x]` 改为 `[`。如果你的配置没有允许日志文件更改，此“更新”报告将使之前的“检查”报告变得多余。

可以使用以下命令生成安全且加密策略（规则）文件的文本版本：

```
/twadmin --print-polfile ../policy/policy.txt
```

如果 Tripwire 抱怨文件丢失，请从该文件中删除它们。然后以如下方式更新默认策略：

```bash
tripwire -m p --secure-mode low ../policy/policy.txt
```

`/bin/date` 程序应该是模式 755。如果你执行命令 `chmod 711 /bin/date`，该程序会被修改但不会损坏。随后的

```bash
tripwire -m c
```

将在其报告中包含以下内容。

| 规则名称 | 严重性级别 | 增加 | 删除 | 修改 |
| --- | --- | --- | --- | --- |
| *OS 执行文件和库* | 100 | 0 | 0 | 1 |

第 17 章 • 扫描系统异常

请注意，尽管 Tripwire 知道 `/bin/date` 文件发生了变化，但它并没有费心报告具体的更改内容。相比之下，我在上一节中提供的“单行命令”反而提供了更有用的信息。

## 17.2.3 Tripwire 无法防止的威胁

早期版本的 Tripwire 提到有必要将程序和数据库保留在只读（Read/Only）介质上，以防止黑客的篡改。现在它自豪地声称，由于数据库和受信任文件经过了加密签名，这种做法不再是必要的。作者对此持不同意见。如果一个黑客足够老练，能够通过“更新” Tripwire 数据库来察觉她的木马程序，那么她就足够老练去安装一个植了木马版本的 Tripwire。这个木马版本可以在常规位置向管理员（SysAdmin）提示短语，然后修改数据库并重新签名，或者假装没有任何内容被修改过。

非常老练的黑客可以向 tripwire、`/bin/sh` 甚至内核添加木马。这种情况将无法通过 Tripwire 的标准用法（信任本地副本）检测到。当你有理由相信老练的黑客发动了攻击，或者为了以防万一进行定期检查，建议采取以下措施：创建 Tripwire 专用的救援磁盘，以第 600 页的“自定义救援磁盘”作为指南。启动救援磁盘并运行直到直到绝对受信任的 Tripwire 可执行文件和数据库。显然，这个受信任的数据库必须定期更新，而且不能简单地从硬盘上的“常规”副本中复制，因为那个副本并不是完全可信的。

## 17.2.4 Tripwire 的替代方案

有几个 Tripwire 的开源竞争对手。可以从以下地址下载 AIDE：

```
ftp://ftp.linux.her/pub/aide/
```

当前版本为：

```
aide-0.7.tar.gz
```

精简版手册可以在以下地址获取：

```
www.cs.tut.fi/~-rammer/aide/manual.html
```

如果你使用来自光盘或从地址地址的 samhain 完整性检查器，木马程序将毫无机会：

```
www.la-samhain.de/samhain.index.html
```

此外，还有 Gog&Magog，可以从以下地址下载：

```
www.multimania.com/cparisel/gog/
```

以及 Sentinel，它有一个非常好的可选 GUI 前端，位于：

```
http://zurk.sourceforge.net/zfile.html
```

SuSEAuditd 从可启动磁盘运行，提供非常安全的完整性检查。在 SuSE 中，它可以轻松移植到其他发行版。从以下地址下载：

```
www.suse.de/-marc/
```

## 17.3 检测被删除的可执行文件

黑客显然不希望你拥有一个他木马程序的副本。除了想对他的技术保密外，这可能成为让他他在标签工厂找份工作的证据。该程序还可能包含他所工作系统的 IP 地址。黑客用来防止你“捕获”可执行文件的一种常用技术是简单地将其从磁盘中删除。正如第 672 页的“寻找黑客的运行进程”中将讨论的，从磁盘中删除它不会终止已经在运行的可执行文件。
