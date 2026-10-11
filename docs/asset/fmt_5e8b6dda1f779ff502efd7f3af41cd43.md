
`$jdoe@machinel john]$ tar xzvf john-1.6.tar.gz`

```

接下来，进入新目录，进入 `src` 目录并制作程序：

```bash

$jdoe@machinel john]$ cd john-1.6

$jdoe@machinel john-1.6]$ cd src

$jdoe@machinel src]$ make linux-x86-any-elf

```

这将创建一个名为 `run/john` 的二进制文件。`run` 目录可以复制到任何地方，因为它包含了 John 运行所需的文件。

# 破解 Linux：Linux 安全奥秘与解决方案

## 运行 John the Ripper
通过在命令行中传递密码文件来执行 `john`，该文件通常是 `/etc/passwd` 的一个副本。

> 如果使用了影子密码（shadow passwords，将在本章稍后讨论），可以通过执行与 `john` 分发的的 `unshadow` 程序来获取加密后的密码。由于 `/etc/shadow` 仅允许 `root` 用户读取，因此只有 `root` 用户可以执行 `unshadow`。

> 注意：由于你创建的文件将包含加密后的密码，请务确保该文件仅对 `root` 可读。

```

[@machinel run]$ unshadow /etc/passwd /etc/shadow > password.txt

[@machinel run]$ chmod 600 password.txt

```

破解出的密码将打印到终端上，并保存到名为 `run/john.pot` 的文件中。这里是运行 `john` 以及 `john` 创建的输出示例：

```

[@machinel run]$ john password.txt

Loaded 3 passwords with 3 different salts (FreeBSD MD5 [32/32])

joe (john)

student (student)

```

> 如果再次运行 `john`，`john` 会查找 `john.pot`，如果发现已破解的密码，它会再次尝试破解它。

在 `john` 运行时，可以检查当前状态：
`guesses: 2 time: 00:02:52:50 (3) c/s: 1532 trying: 2bdo`
输入 `CTRL-C` 将暂停 `john`。输入两次 `CTRL-C` 将中止而不保存。
此外，`john` 会每隔 10 分钟将其当前状态保存到名为 `run/john.ini` 的文件中，这样如果系统在运行过程中崩溃，可以恢复 `john`。（此功能显然是为 Windows 用户设计的）。
恢复被中断的会话：

```

[@machinel run]$ john -restore

```

获取已破解的密码：
`[@machinel run]$ john -show password.txt`
`jdoe:500:500:John Doe:/home/jdoe:/bin/bash`
`student:student:501:100::/home/student:/bin/bash`

已破解 2 个密码，剩余 1 个

# 第 8 章：密码破解

要获取特定用户的破解密码：

```

[jdoe@machinel run]# john -show -users:jdoe passwd.txt

jdoe:500:500:John Doe:/home/john/bin/bash

```

已破解 1 个密码，剩余 0 个

还有许多运行 `john` 的方法。更多详情请参见 John 分发中的 `doc/EXAMPLES` 文件。

# John 的模式

`john` 的模式可以通过 `run/john.ini` 中的定义进行增强。该文件包含了用户可以创建和增强许多规则和模式。`john` 支持的模式包括：

- 字典列表模式（Wordlist mode）：允许在 `FILE` 中指定单词列表，或从 `stdin.ini` 读取。这些单词将用于破解密码 [原文错误：可能应为“crack passwords”]；你也可以提供规则来修改模式。

```

[jdoe@machinel run] john -wordfile:FILE

[jdoe@machinel run] john -wordfile-stdin

```

- 单次破解模式（Single crack mode）：使用登录信息作为密码——非常快。

```

[jdoe@machinel run] john -single

```

- 增量模式（Incremental mode）：尝试所有可能的字符组合。这是最强大的模式，但可能需要很长时间。

```

[jdoe@machinel run] john -incremental

```

- 外部模式（External mode）：允许使用用无库 C 语言编写的函数进行外部模式定义。

```

[jdoe@machinel run] john -external

```

# 邮件选项

像 `Crack` 一样，`John` 有向任何密码被破解的用户发送电子邮件的能力：

```

[jdoe@machinel run]# .mailerpasswd.txt

```

此程序将向所有密码被 `john` 破解的用户发送电子邮件。

就像 `Crack` 使用脚本向使用弱密码的用户发送邮件一样，你可以使用该 `mailer` 程序来告知并教育用户使用弱密码的问题。

再次，向使用弱密码的用户发送此类电子邮件具有潜在的危险。

# 破解 Linux：Linux 安全奥秘与解决方案

# 其他破解程序

尽管 `Crack` 和 John the Ripper 是两个广为人知的密码破解工具，但还有大量的破解程序可用。访问这些程序列表的优质网站是：`http://packetstorm.security.com/`。

![](img/5dd91543c8b0283d8428002c8b00899_320_0.png)

# Viper

| 流行度 | 6 |
| --- | --- |
| 简单性 | 10 |
| 影响力 | 7 |
| 风险评分 | 7 |

`Viper` (`http://www.wilter.com/wf/`) 是一个基于 GUI 的 Windows 程序，对 `DES/crypt()` 进行暴力破解。它将 `/etc/passwd` 或 `/etc/shadow` 中的一行（本章稍后介绍）作为输入，并开始使用 1 到 12 个字符的密码进行暴力破解。`Viper` 将检查所有密码。它字面上检查从 "a" 到 "z00000000" 以及之间所有可能的组合。它只检查字母和数字，忽略标点和特殊字符。`Viper` 正在检查字母和数字的所有可能组合，执行可能需要很长时间——非常长时间。如果它检查长度为 12 的字符串中所有可能的字符组合，必须检查数十亿次。在快速机器上，这需要很长时间。`Viper` 运行非常慢，并使用处理器。此外，尝试破解密码可能需要几分钟。然而，要知道在其他平台破解 Linux 密码是可能的（如果你发现没有 Linux 机器）。

![](img/5dd91543c8b0283d8428002c8b00899_320_1.png)

# Slurpie

| 流行度 | 8 |
| --- | --- |
| 简单性 | 8 |
| 影响力 | 9 |
| 风险评分 | 8 |

`Slurpie` (`http://www.ips.net/coati/slurpie.html`) 是一种类似于 `Crack` 和 John the Ripper 的密码破解程序，可以在分布式环境中运行。由于 `Slurpie` 可以在多台计算机上同时运行，这可以加快进度。`Slurpie` 的输入是密码文件以及可选字典。它可以在单主机或多个主机上运行。要在多个主机上运行，只需在每台机器上构建 `slurpie`，并将每台机器的 `IP` 添加到 `slurpie` 分发中的 `hosts.dat` 文件中。

# 300
Linux 破解入门：Linux 安全秘密与解决方案

通过 `view` 命令查看密码是让字典攻击变得极其困难的最重要步骤。

本章的这部分将描述密码影子（password shadowing），并演示如何将非影子密码转换为影子密码。

## 影子密码详解

如果使用了密码影子机制，`/etc/passwd` 的内容将类似于：

```

root:x:0:0:root:/bin/bash

bin:x:1:1:bin:/bin/

demon:x:2:2:daemon:/sbin

adm:x:3:3:/var/adm/

lp:x:4:7:/var/spool/lpd/

mail:x:8:12:/var/spool/mail/

news:x:9:13:news:/var/spool/news

ucp:x:10:14:var/spool/ucp/

operator:x:11:12:operator:/root

gopher:x:13:13:gopher:/usr/lib/gopher-data

ftp:x:14:50:User:/home/ftp

nobody:x:99:99:nobody:/

fs:x:60:60:Server://fs/bin
```
