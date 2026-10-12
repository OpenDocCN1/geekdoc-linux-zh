
当然，这些是简单的 SHA1 加密哈希，使用较新的加密或加盐密码的哈希破解起来要花费更长的时间。加盐密码使用唯一的值或盐来加密每个密码，因此没有任何两个密码哈希是相同的。但不管你信不信，今天找到使用未加盐密码的公开密码泄露数据仍然非常普遍。再加上 Hashcat 的新版本将最大可破解的密码长度从 32 增加到 256 的事实，这会让你重新考虑公司的密码长度和复杂度策略。

基于视频 GPU 的破解工具和基于 CPU 的工具之间存在巨大的速度差异。Hashcat 是最受欢迎的“世界上最快”的基于 GPU 的破解工具之一。John the Ripper 是最受欢迎的基于 CPU 的破解器之一。我们将查看两者，首先，John the Ripper！

## JOHN THE RIPPER

**工具作者**：Solar Designer 和社区

**工具网站**：[https://www.openwall.com/john/](https://www.openwall.com/john/)

John the Ripper，或 John（或 JTR）是一个速度非常快的基于 CPU 的密码破解器。它非常易于使用，通常是在尝试破解密码时使用的首选工具。John 在破解短密码方面非常擅长，所以我通常先使用 John 来获取低垂的果实或简单的密码，然后转向 Hashcat 进行更复杂的破解。因此，我们将只快速介绍 John。

### JOHN THE RIPPER 概述

John the Ripper 是一款开源的密码破解软件，广泛用于渗透测试、道德黑客和取证分析。由 Solar Designer 开发，由于其有效性和灵活性，该工具已成为网络安全社区的常用工具。

**密码哈希破解**

John the Ripper 擅长破解各种类型的密码哈希。它支持数百种哈希和加密算法，包括 DES、MD5、SHA-1、SHA-256、Bitlocker、归档（ZIP、RAR）等。这种通用性使其适合处理各种攻击安全（Offensive Security）和取证用途。

**词表混合攻击**

John 支持使用词表的字典攻击，允许用户利用常用密码或基于特定标准创建自定义列表。此外，它可以执行混合攻击，将词表与暴力破解方法结合起来，以增加成功的可能性。

**多平台支持**

John the Ripper 与平台无关，可在各种操作系统上运行，包括 Unix、Linux、Windows 和 macOS。这种灵活性使其成为在多样化环境中工作的安全专业人士的宝贵资产。

**常用开关**

为了充分发挥 John the Ripper 的潜力，安全专业人士利用各种命令行开关来定制和优化他们的密码破解工作。以下是一些常用开关及其示例。

（更多示例请见 [https://www.openwall.com/john/doc/OPTIONS.shtml](https://www.openwall.com/john/doc/OPTIONS.shtml)）

**--format**

指定密码文件中使用的哈希算法。John the Ripper 自动检测许多格式，但此开关允许用户明确定义模糊情况的格式。

```
$ john --format=md5 hashed_passwords $
```

**--fork**

允许使用多个 CPU 的 Linux 选项

```
$ john --fork 4 $
```

**--wordlist**

指定词表文件的路径。此开关对于字典攻击至关重要，有助于定义要测试的潜在密码集。

```
$ john --wordlist=/path/to/wordlist.txt hashed_password $
```

**--rules**

启用基于规则的密码生成，允许用户将转换规则应用于词表中的单词。规则可以包括排列、大小写修改和字符替换。

```
$ john --wordlist=/path/to/wordlist.txt --rules=Jumbo hashed_passwords $
```

**--incremental**

启动增量暴力破解攻击，系统地测试所有可能的密码组合。用户可以自定义字符集和密码长度以匹配特定场景。

```
$ john --incremental=alnum hashed_passwords $
```

**--show**

在破解过程中显示已破解的密码。此开关提供实时反馈，对于监控进度非常有用。破解完成后，你还可以再次运行此命令来显示已破解的密码。

```
john --show hashed_passwords
```

### JOHN THE RIPPER 实战应用

John 使用起来非常简单，只需输入“john”以及要破解的密码文件，John 便会开始运行。John 会尝试自动检测密码文件中的哈希值。如果无法自动检测，它会提示你使用“`--format=`”命令输入正确的加密格式。下图是使用 John 破解大型 SHA1 密码转储文件的示例：

```
$ john [password_hash_list] --format=Raw-SHA1
```

![](img/4a03f08556c51a14a3b88fe549a54ca8_97_0.png)

如前所述，对于基于 CPU 的破解器而言，John 的速度很快。在上例中，我向 John 提供了超过 1600 万个哈希值的列表。它在大约 15 分钟内就找到了我正在尝试破解的 200 多万个密码。之后，它便空转且没有实质进展。此时，我本可以使用 John 的一些高级功能来破解该列表，但我转而去使用 Hashcat 了。

当你确实破解了一个密码哈希文件时，任何恢复的凭据都会存储在 John 的 pot 文件中。pot 文件位于你的 `~/.john/`（隐藏）目录中：

```
$ cd .john
(kali@kali):~/.john$ ls
john.log   john.pot   john.rec
```

如果你打开 pot 文件，可以看到密码哈希值，已破解的密码位于右侧：

![](img/4a03f08556c51a14a3b88fe549a54ca8_98_0.png)

你也可以使用“`john [password_hash_list] --show`”来查看已破解的密码。如果你退出 John 破解会话，状态将自动保存。你可以使用“`john [password_hash_list] --restore`”来恢复已保存或退出的会话。

### 结语

这只是对 John 的非常简要的介绍。在安全测试中，我通常先对能够恢复的小型哈希值组使用 John。这就是我使用 John 的程度。如果你恢复了单个哈希值并需要快速破解它，或者你有一大批基础哈希值列表，John 是一个很好的工具。对于任何大型或更复杂的情况，我都会立即切换到 Hashcat。与任何工具一样，试着使用它，看看如何将其纳入你的工具箱。你可能会比 Hashcat 更喜欢 John。无论如何，熟悉两者都是有好处的。

![](img/4a03f08556c51a14a3b88fe549a54ca8_99_0.png)

John the Ripper 的 Wiki 包含大量教程和操作指南

如需更多信息，包括从基础到高级的教程、综合用户指南和使用文章，请访问该工具的 Wiki [https://openwall.info/wiki/john](https://openwall.info/wiki/john)。

## 第 6 章

### Hashcat

**工具作者**：Jens Steube 和 Hashcat 开发团队  

**工具网站**：[https://hashcat.net/hashcat/](https://hashcat.net/hashcat/)  

**工具 Wiki**：[https://hashcat.net/wiki/](https://hashcat.net/wiki/)

Hashcat 是一款通用密码破解器，可以基于你的显卡处理器（GPU）或 CPU 运行。Hashcat 被誉为世界上最快、最先进的密码破解器。该工具是一个多线程破解器，如果你的 CPU 可以运行多个线程，它将会使用它们。但真正的速度优势在于使用 GPU 时，即你显卡上的处理器。你的 GPU 专为计算能力而设计，所有的算力都用于破解密码。你甚至可以利用多张显卡的 GPU 来打造一台强大的破解工作站。

密码破解是我的爱好。在过去的 10 多年里，我个人使用 Hashcat 破解了数亿个密码。当我破解的密码数量达到四十种不同语言后，我就停止统计了。我使用它恢复了无数真实世界的密码，甚至还包括大量打包在公开密码转储文件中、由超过一百个字符组成的无意义字符串，使其看起来规模更大。没有任何密码破解工具能让我像 Hashcat 这样推崇备至。它快速、高效，并且令人惊叹！

以下是我最近使用 Hashcat 破解的一些真实世界密码的示例：

```
–_+)&#33*;)*LSGMsd34sglIOC55^
cV1so@7f3*tw9lb_
spongebobs_only_wifey
Sahana_forever<3
```

Henry2009å,¬
