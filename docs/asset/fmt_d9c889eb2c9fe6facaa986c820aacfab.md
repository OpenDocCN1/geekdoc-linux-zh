
# CVE 2017-1000112 案例研究

内核是提升权限的极佳方式，这不仅取决于内核版本，还取决于操作系统的偏好，包括 Debian、Redhat、Gentoo 等。

为了演示这种攻击向量，我们将通过检查 `/etc/issue` 文件获取有关目标的更多信息。正如模块早早部分过的，这是一个系统文本文件，在 Linux 机器的登录提示之前会打印消息或系统识别信息。

## 使用 Kali Linux 2.0 进行渗透测试

![](img/f99f528ca9845f4c256ce54e882b1345_568_0.png)

```
$ cat /etc/issue
Ubuntu 16.04.3 LTS #1 \
```

| 列表 587 - 收集目标系统信息 |

接下来，我们将使用标准系统命令检查内核版本和架构：

```
$ uname -r
4.8.0-generic
$ uname -m
x86_64
```

| 列表 588 - 从我们的 Linux 系统中收集内核和架构信息 |

我们的我们的目标系统似乎运行在 x86_64 架构上的 Ubuntu 16.04.3 LTS (4.8.0-58-generic)。利用这些信息，我们可以在本地的 Kali 系统上使用 `searchploit` 来寻找与目标匹配的内核漏洞。

```
$ searchploit kernel ubuntu 16.04
```

| 漏洞标题 | 路径 (/usr/share/exploit/) |

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

我们可以通过添加特定目标的单词和短语来提高字典列表的有效性。例如，考虑 MegaCorp，一家经营纳米科技的公司。网站 megacorp.com 列出了产品，包括 Nanobot。在假设的评估中，我们识别出了低级密码 Nanobot93。假设这是我们公司的常见格式，我们想要创建一个识别其他密码的自定义字典列表。

我们可以浏览网站并将常用术语手动添加到字典列表中，或者使用像 `cwl` 这样的工具来完成这些工作。正如 `-help` 输出所示，该工具可以通过选择多个选项进行配置，我们将关注几个关键参数。

例如，以下命令提取 megacorp.com，列出至少六个字符的单词 (`-m 6`)，并将字典列表写入 (`-w`) 自文件 (`megacorp-cwl.txt`)。

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

上面的列表显示 cwl 创建了几个产品的名称，包括 Nanobot。我们应该考虑其他产品名称也可能被用于密码的可能性。

然而，这些单词本身将是极其弱的密码，无法满足典型的密码策略规则。这类规则通常要求使用大小写字母、数字，可能还有特殊字符。根据我们发现的密码 (Nanobot93)，我们建议 megacorp 的密码策略要求密码中至少包含两个数字，并可能进一步规定（尽管这不太）数字必须位于密码末尾。

¹⁵⁴(DigNinja, 2017), http://www.digninja.org/projects/cwl.php

为了这个简单的演示，我们假设 Megacorp 的策略规定密码必须包含一个两位数字。

为了创建符合此要求的密码，我们可以编写一个 Bash 脚本。然而，我们将使用一个强大得多的工具，称为 John the Ripper (JTR)⁵。它是一个快速的密码破解器，具有生成自定义字典列表和规则变体的能力。
