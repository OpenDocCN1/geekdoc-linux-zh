
### 列表 590 – 在 Linux 上使用 gcc 从本地 Exploit Database 归档编译漏洞利用

在目标机器上编译好漏洞利用后，我们可以运行它并使用 `whoami` 检查我们的权限级别：

![Image](img/ec25e59d75726b7041242a56d3376832_563_0.png)

*图 293：通过权限提升漏洞在 Linux 上提升权限*

图 293 显示，我们的权限已成功从 n00b（标准用户）提升到 root，这是 Linux 操作系统中权限最高的账户。

## 18.4 总结

在本模块中，我们涵盖了 Windows 和 Linux 操作系统以及不同架构上的权限提升概念。我们介绍了揭示此类攻击所需信息的手动和自动枚举技术。此外，我们演示了这两种操作系统的编译过程，并演示了若干权限

[^545] (Pentest Money, 2019), http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet
[^546] (Wikipedia, 2019), https://en.wikipedia.org/wiki/Crypt(C)

升级攻击，以及各种根本不需要软件漏洞即可实施的权限提升攻击。

## 19. 密码攻击

密码是用户账户和服务认证的最基本形式，而密码攻击的目标则是发现并利用有效凭证，以获取对用户账户或服务的访问权限。

从广义上讲，密码攻击有几种常见方法。我们可以通过字典攻击使用各种词表来尝试猜测密码，或者对密码中所有可能的字符进行暴力破解。

*   总体而言，字典攻击优先考虑速度，但提供的密码覆盖率较低；而暴力破解则优先考虑密码覆盖率，但以牺牲速度为代价。在渗透测试中，根据我们的优先事项和时间要求，这两种技术都可以有效地使用。

在某些情况下，一旦我们（通常是特权）获取了对目标的访问权限，并且能够提取密码哈希值，我们就可以利用*密码破解*攻击来获取明文凭据，或者利用*传递哈希（Pass-the-Hash）*攻击，仅使用用户名和哈希值即可向基于 Windows 的目标进行身份验证。

在本模块中，我们将详细讨论这些概念和技术，并演示它们如何在各种攻击场景中发挥作用。

### 19.1 词表

词表（有时称为*字典文件*）是包含单词的文本文件，用作设计用于测试密码的程序的输入。在考虑字典攻击时，精度通常比覆盖率更重要，这意味着创建一个包含相关密码的精简词表比创建一个巨大的通用词表更为重要。正因为如此，许多词表都基于常见的主题，例如流行文化引用、特定行业或地理区域，并被提炼为包含常用的密码。Kali Linux 在 `/usr/share/wordlists/` 目录中包含许多这样的字典文件，还有更多在线托管。

在进行密码攻击时，直接使用这些预构建列表可能很有诱惑力。然而，如果我们花些时间仔细构建自己的自定义列表，我们的方法可以更有效。在本节中，我们将研究创建有效词表的工具和方法。

#### 19.1.1 标准词表

我们可以通过添加特定于目标组织的单词和短语来提高词表的有效性。

例如，考虑 MegaCorp One 是一家涉及纳米技术的公司。该公司的网站 `www.megacorpone.com` 列出了该公司出售的各种产品，包括 Nanobot。在假设的评估中，我们识别出了低权限密码 `Nanobot93`。假设这可能是一家公司常见的密码格式，我们希望创建一个自定义词表，以识别其他具有类似模式的密码，也许使用其他产品名称。

我们可以浏览网站并手动将常用术语和产品名称添加到自定义词表中，或者我们可以使用 `cewl` 等工具来为我们完成大部分工作。如 `--help` 输出所示，可以通过指定几个选项来配置此工具，但我们只关注几个关键参数。

例如，以下命令抓取 `www.megacorpone.com` 网站，定位至少包含六个字符（`-m 6`）的单词，并将词表写入（`-w`）自定义文件（*megacorp-cewl.txt*）：

```bash
kali@kali:~$ cewl www.megacorpone.com -m 6 -w megacorp-cewl.txt

kali@kali:~$ wc -l megacorp-cewl.txt

312

kali@kali:~$ grep Nano megacorp-cewl.txt

Nanotechnology

Nanomite

Nanoprobe

Nanoprocessors

NanoTimes

Nanobot
```

*清单 591 - 使用 cewl 创建字典文件*

上述清单显示 `cewl` 定位了几个产品的名称，包括 *Nanobot*。我们应该考虑到其他产品名称也可能用于密码中。

然而，这些单词本身作为密码极其薄弱，并且不符合典型的密码强度规则。这些类型的规则通常要求使用大写字母和小写字母、数字，以及特殊字符。根据我们发现的密码（`Nanobot93`），我们可以推测 MegaCorp One 的密码强度要求至少需要在密码中使用两个数字，并且可能进一步规定（尽管可能性很低）数字必须位于密码末尾。

为了简化演示，我们假设 MegaCorp One 的政策规定密码必须以两位数字结尾。

为了创建符合此要求的密码，我们可以编写一个 Bash 脚本。但我们改用了一种功能更强大的工具，称为 John the Ripper (`JTR`)，它是一种快速密码破解器，具有多项功能，包括生成自定义词表和应用规则排列的能力。

基于我们对密码政策的假设，我们将向 JTR 配置文件（`/etc/jjohn/john.conf`）添加一条规则，该规则将变换我们的词表，在每个密码后附加两位数字。为此，我们必须找到定义词表变换规则的 `[List.Rules:Wordlist]` 段，并添加一条新规则。在本例中，我们将在词表中的每个单词后添加从 0 到 99 的两位数字序列。

我们将以 `$` 字符开始此规则，这告诉 John 向词表中的原始单词追加字符。接下来，我们指定要追加的字符类型；在这种情况下，我们要 0 到 9 之间的任何数字（`[0-9]`）。最后，为了追加双位数，我们只需重复 `[0-9]` 序列。最终规则如清单 592 所示。

```bash
kali@kali:~$ sudo nano /etc/jjohn/john.conf

 ...

# Wordlist mode rules

[List.Rules:Wordlist]

# Try words as they are

 :

# Lowercase every pure alphanumeric word

-c >3 !?X l Q

# Capitalize every pure alphanumeric word

-c (?a >2 !?X c Q

# Lowercase and pluralize pure alphabetic words

 ...

# Try the second half of split passwords

-s x_

-s-c x_ M l Q

# Add two numbers to the end of each password
$[0-9]$[0-9]

...
```

*清单 592 - 在 John the Ripper 配置文件中创建变换规则*

John the Ripper 的规则语法非常广泛且强大，但这超出了本模块的范围。如需更多信息，请花时间查阅规则文档。

现在规则已添加到配置文件中，我们可以变换目前包含 312 个条目的词表。

![John the Ripper output](img/ec25e59d75726b7041242a56d3376832_568_0.png)

为此，我们将调用 `john`，指定字典文件（`--wordlist=megacorp-cewl.txt`），激活配置文件中的规则（`--rules`），将结果输出到标准输出（`--stdout`），并将该输出重定向到一个名为 `mutated.txt` 的文件。

```bash
kali@kali:~$ john --wordlist=megacorp-cewl.txt --rules --stdout > mutated.txt

Press 'q' or Ctrl-C to abort, almost any other key for status

46446p  0:00:00:00 100.00% (2018-03-01 15:41) 663514p/s ch0c0l4te99

kali@kali:~$ grep Nanobot mutated.txt

...

Nanobot90

Nanobot91

Nanobot92

Nanobot93

Nanobot94

Nanobot95

Nanobot96
...
```
