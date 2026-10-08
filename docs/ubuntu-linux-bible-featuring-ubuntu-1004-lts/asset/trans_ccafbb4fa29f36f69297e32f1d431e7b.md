

# 将 MailScanner、SpamAssassin 和 ClamAV 与 Postfix 集成

MailScanner 是一款快速且强大的工具，用于扫描传入邮件中的垃圾邮件，并可以可选配置扫描传入邮件中的病毒。Ubuntu MailScanner 软件包要求系统中已安装 SpamAssassin 软件包（在第 7 章的“自动检查垃圾邮件”节中讨论过），以便它在执行完自己的垃圾邮件检查后调用 SpamAssassin 软件包，从而最大限度地捕获并标记传入的垃圾邮件。

# 注意

MailScanner 软件包始终声称它正在扫描病毒，即使它并没有这样做。这是因为配置文件中包含一个你想要使用的病毒扫描器设置，该设置默认为“无（none）”。别担心；我会解释如何修复它。

我在本章的“安装 Postfix 及其伙伴”节中曾建议你安装 MailScanner 和 ClamAV 病毒扫描软件包。如果你还没有安装，请返回该节以查看有关如何安装这些软件包的信息。

一旦安装完成，将 MailScanner 添加到 Postfix 链链中将非常简单：

-   在你的 Postfix 主配置文件 `main.cf` (/etc/postfix/main.cf) 的末尾添加以下行：

```
header_checks = regexp:/etc/postfix/header_checks
```

-   使用你喜爱的文本编辑器创建文件 `/etc/postfix/header_checks`，内容如下：

```
^Received:/ / HOLD
```

此行告诉 Postfix 扫描每条传入邮件，检查行开头是否存在字符串 "Received:" 实例，并且将任何匹配的邮件（即所有邮件）投递到 HOLD 队列。HOLD 队列是一个临时暂存区域，你将在该区域扫描传入的邮件。保存此文件并继续下一步。

-   使用你喜爱的文本编辑器打开 MailScanner 配置文件 (/etc/MailScanner/MailScanner.conf)，以便配置 MailScanner 使其与你 Ubuntu 系统上安装的 Postfix 正常工作。（默认情况下，Ubuntu MailScanner 软件包的配置类似于 Debian 系统，因此它的配置是为配合 exim 邮件服务器使用的。）

-   找到 `Run As User` 条目，删除 `Run As User = postfix` 行开头的井号（#），并确保任何其他以 `Run As User` 开头的行开头都有井号。这些条目现在应该像像所示：

```
# Run As User = mail
Run As User = postfix
# Run As User = Debian-exim-
```

-   找到 `Run As Group` 条目，删除 `Run As Group = postfix` 行开头的井号，并确保任何其他以 `Run As Group` 开头的行开头都有井号。这些条目现在应该像所示：

```
# Run As Group = mail
Run As Group = postfix
# Run As Group = Debian-exim
```

-   找到 `Incoming Queue Dir` 条目，将其值更改为 `/var/spool/postfix/hold`。该条目现在应该像所示：

```
Incoming Queue Dir = /var/spool/postfix/hold
```

-   找到 `Outgoing Queue Dir` 条目，将其值更改为 `/var/spool/postfix/incoming`。该条目现在应该像所示：

```
Outgoing Queue Dir = /var/spool/postfix/incoming
```

-   找到 `MTA` 条目，将其值更改为 `postfix`。该条目现在应该像所示：

```
MTA = postfix
```

-   找到 `Virus Scanners` 条目，将其值设置为 `clamav`。该条目现在应该像所示：

```
Virus Scanners = clamav
```

-   保存 `/etc/MailScanner/MailScanner.conf` 文件，并继续下一步。

-   使用以下命令确保 Postfix 用户和用户组拥有 MailScanner 工作目录以及它存储（隔离）疑似含有病毒文件的目录的所有权，以便 Postfix 邮件服务器可以向这些目录写入：

```
sudo chown -R postfix:postfix /var/spool/MailScanner
```

# 第三部分：面向系统管理员的 Ubuntu

12. 使用你喜爱的文本编辑器修改文件 `/etc/default/mailscanner`，并删除包含 `run_mailscanner` 变量行开头的井号。该行应该像所示：

```
run_mailscanner=1
```

启用此变量将导致你的系统在下次启动时自动启动 MailScanner。保存文件并退出文本编辑器。

现在，使用以下命令首次启动 MailScanner：

```
sudo check_mailscanner
```

现在，要么重启 Postfix 服务器（使用 `sudo /etc/init.d/postfix restart`），要么使用 `postfix reload` 命令，使活动中的 Postfix 进程加载你对配置文件的更改。

要测试 MailScanner 是否正确与你的邮件服务器集成，通过你的邮件服务器给自己发送一封邮件。如果 MailScanner 工作正常（且邮件不是垃圾邮件且不含病毒），你应该会在邮件底部看到以下横幅：

> This message has been scanned for viruses and dangerous content by MailScanner, and is believed to be clean.

恭喜！你现在正在进行大量的垃圾邮件过滤，并且还在检查邮件服务器收到的任何邮件中的病毒！

# 提示

如之前提到的，SpamAssassin 是一款强大的工具，用于扫描传入邮件中的垃圾邮件，并可以可选配置扫描传入邮件中的病毒。

