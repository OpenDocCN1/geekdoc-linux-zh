

### 19.4.2.1 练习

- 1. 使用 Mimikatz 从 Windows 客户端中提取管理员用户的密码哈希。
- 2. 复用该密码哈希，从你的 Kali 系统发起“传递哈希”（pass-the-hash）攻击，并在你的 Windows 客户端上获取代码执行权限。

### 19.4.3 密码破解

在密码分析学中，密码破解是指根据存储的哈希值恢复明文口令的过程。

从高层次来看，密码破解的过程相当直接。一旦我们确定了目标认证过程中所使用的哈希机制，就可以遍历词表中的每个单词并生成相应的消息摘要。如果计算出的哈希值与从目标系统获取的哈希值相匹配，我们就获得了匹配的明文密码。这通常都是借助专门的密码破解程序完成的。

> 如果认证过程中涉及盐值（salt）且我们不知道该盐值的具体内容，破解可能会变得极其复杂甚至不可能，因为我们需要使用各种盐值反复对每个潜在的明文密码进行哈希运算。尽管如此，根据我们的经验，我们几乎总能捕获到密码哈希以及盐值，无论是来自包含每记录中这两个唯一值的数据库，还是来自使用单一盐值对所有哈希值进行处理的配置文件或二进制文件。当这两个值都已知时，密码破解的复杂度会降低。

一旦我们获取了目标系统的密码哈希，就可以开始一个后台运行的密码破解会话，同时继续我们的评估。如果任何密码被破解，我们可以尝试将这些密码用于其他系统，以增加对目标网络的控制权。与其他渗透测试过程一样，这是一个迭代过程，随着我们扩大控制范围，我们会将数据反馈到早期步骤中。

为了演示密码破解，我们将再次使用 John the Ripper，因为它支持数十种密码格式，并且功能强大、灵活。

以纯暴力破解模式运行 **john**（尝试密码中所有可能的字符组合）非常简单，只需在命令行上传入包含我们密码哈希的文件名以及哈希格式即可。

在列表 619 中，我们攻击使用 mimikatz 转储的 NT 哈希（--format=NT）。

```
kali@kali:~$ cat hash.txt
WDAGUtilityAccount:0c509cca8bcd12a26acf0d1e508cb028
Offsec:2892d26cdf84d7a70e2eb3f9f05c425e

kali@kali:~$ sudo john hash.txt --format=NT
Using default input encoding: UTF-8
```

![](img/ec25e59d75726b7041242a56d3376832_586_0.png)

```
Rules/masks using ISO-8859-1
Loaded 2 password hashes with no different salts (NT [MD4 128/128 AVX 4x3])
Press 'q' or Ctrl-C to abort, almost any other key for status
```

*列表 619 - 使用 John the Ripper 进行暴力破解*

在上述输出中，JTR（John the Ripper）正确识别了哈希类型并开始对其进行破解。然而，像这样的暴力攻击基于系统速度可能需要很长时间。作为替代方案，我们可以使用 **--wordlist** 参数并提供词表的路径，这会缩短处理时间，但承诺的密码恢复率较低：

```
kali@kali:~$ john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt --format=NT
```

*列表 620 - 使用 John the Ripper 进行字典破解*

如果仍有密码未被破解，我们接下来可以尝试应用 JTR 的密码变形规则，使用 **--rules** 参数。

```
kali@kali:~$ john --rules --wordlist=/usr/share/wordlists/rockyou.txt hash.txt --format=NT
```

*列表 621 - 使用密码变形规则进行破解*

为了使用 JTR 破解基于 Linux 的哈希，我们需要首先使用 **unshadow** 工具将受攻破系统中的 **passwd** 和 **shadow** 文件合并。

```
kali@kali:~$ unshadow passwd-file.txt shadow-file.txt
victim:$6$f0S.xfbT$5c5vh3Zrk.88SbCWdUnirjgcgcYwCC/xT5Ec|SuJtrvqFk04pSWHaGxZojNy.vAqMGr8BN0b0P3pW1ybmx20IT/:1003:1003:::/:home/victim:/bin/bash

kali@kali:~$ unshadow passwd-file.txt shadow-file.txt > unshadowed.txt
```

*列表 622 - 准备 Linux 密码哈希以供破解*

现在我们可以运行 **john**，传入词表和未加盐的文本文件作为参数：

```
kali@kali:~$ john --rules --wordlist=/usr/share/wordlists/rockyou.txt unshadowed.txt
Using default input encoding: UTF-8
Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Will run 2 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
s3cr3t (victim)
1g 0:00:00:28 DONE (2019-08-20 15:42) 0.03559g/s 2497p/s 2497c/s 2497C/s
... 
```

*列表 623 - 使用 John the Ripper 破解 Linux 密码哈希*

较新版本的 John the Ripper 默认支持多线程，但旧版本仅使用单个 CPU 核心执行破解操作。如果你遇到的是旧版 JTR，它支持可以加速过程的替代方案。我们可以采用多个 CPU 核心，甚至多台计算机，来分配负载并加速破解过程。**--fork** 选项启用多个进程，以便在单台机器上利用更多的 CPU 核心，而 **--node** 则跨多台机器分配工作。

例如，假设我们有两台机器，每台机器都有 8 核 CPU。在第一台机器上，我们设置 **--fork=8** 和 **--node=1-8/16** 选项，指示 John 在此机器上创建八个进程，将提供的词表分成十六个相等的部分，并在本地处理前八部分。在第二台机器上，我们可以使用 **--fork=8** 和 **--node=9-16** 将八个进程分配给词表的后半部分。以这种方式分配工作大约可以提供 16 倍的性能提升。

> *攻击者还可以预先计算密码的哈希值（这可能花费大量时间），并将它们存储在巨大的数据库中，或者存储在彩虹表中，[585] 从而使密码破解变成简单的表查找过程。这是一种空间-时间权衡，因为这些表可能会消耗大量的空间（根据密码复杂度可达 PB 级别），但密码“破解”过程本身（技术上是一个查找过程）所花费的时间要少得多。*

虽然 John the Ripper 是破解密码哈希的绝佳工具，但其速度受限于专门用于该任务的 CPU 算力。近年来，图形处理器（GPU）变得极其强大，而且当然存在于每台带有显示器的计算机中。高端机器，如用于视频编辑和游戏的主机，配备了极其强大的 GPU。Hashcat [586] 等 GPU 破解工具利用 CPU 和 GPU 的强大功能，达到了惊人的密码破解速度。

Hashcat 的选项通常镜像 John the Ripper 的选项，并包括算法检测和密码列表变形等功能。

在此示例中，我们将在配备 GeForce GTX 1080 Ti GPU 的机器上以基准测试模式（-b）运行 hashcat：

```
C:\Users\Cracker\hashcat-4.2.1> hashcat64.exe -b
hashcat (v4.2.1) starting in benchmark mode...
...
OpenCL Platform #1: NVIDIA Corporation
=========================================
* Device #1: GeForce GTX 1080 Ti, 2816/11264 MB allocatable, 28MCU

Benchmark relevant options:
=========================================
* --optimized-kernel-enable

Hashmode: 0 - MD5

Speed.Dev.#1.....: 39354.5 MH/s (93.70ms) @ Accel:128 Loops:1024 Thr:1024 Vec:4

Hashmode: 100 - SHA1

Speed.Dev.#1.....: 13251.8 MH/s (87.49ms) @ Accel:128 Loops:512 Thr:640 Vec:1

Hashmode: 1400 - SHA-256

Speed.Dev.#1.....: 4770.8 MH/s (48.15ms) @ Accel:128 Loops:64 Thr:1024 Vec:1

Hashmode: 1700 – SHA-512

Speed,Dev.#1......: **1567.9 MH/s** (92.38ms) @ Accel:128 Loops:64 Thr:640 Vec:1

Hashmode: 1000 – NTLM

Speed,Dev.#1......: **65267.0 MH/s** (55.66ms) @ Accel:128 Loops:1024 Thr:1024 Vec:1

Hashmode: 5500 – NetNTLMv1 / NetNTLMv1+ESS

Speed,Dev.#1......: **33504.0 MH/s** (55.00ms) @ Accel:128 Loops:512 Thr:1024 Vec:1

Hashmode: 5600 – NetNTLMv2

Speed,Dev.#1......: **2761.2 MH/s** (83.59ms) @ Accel:128 Loops:64 Thr:1024 Vec:1

Hashmode: 1800 – sha512crypt $6$, SHA512 (Unix) (Iterations: 5000)

Speed,Dev.#1......: **218.6 kH/s** (51.55ms) @ Accel:512 Loops:128 Thr:32 Vec:1 ....
```

*列表 624 - 使用 GeForce GTX 1080 Ti 进行基准测试破解速度*

基准数字相当惊人，显示出 SHA1 速度超过每秒 130 亿个哈希，NTLM 速度超过每秒 620 亿个哈希，甚至非常复杂且缓慢的 sha512crypt 哈希算法也能以惊人的每秒 200,000 个哈希的速度运行。将此与我们之前在（自认较弱的）Kali 虚拟机 CPU 上运行 John the Ripper 的一些结果进行比较，那些结果的速度仅在每秒几百个哈希左右。

这些速度是由单个 GPU 实现的，但具有四个、八个或更多 GPU 的多 GPU 计算机是可用的。截至本文出版时，配备单个 GPU 的破解计算机造价约为 2000 美元，而四 GPU 系统的造价约为 6000 美元。八 GPU 系统记录的基准测试超过每秒 5000 亿个 NTLM 哈希。[587]

### 19.4.3.1 练习

（此练习不需要报告）

- 1. 为你的 Windows 机器上转储的 NTLM 哈希创建一个词表文件，并使用 John the Ripper 破解该哈希。

## 19.5 总结

现有的密码攻击工具和词表如此之多，以至于在渗透测试过程中，人们很容易想要直接跳进去并开始攻击，以寻找那个往往难以捉摸的突破点。然而，成功不仅在于深入理解每个工具的使用方法和优势，还在于学会后退一步，智慧地应用这些工具，尊重速度与精度之间的平衡，并优先考虑客户生产环境的安全性。

587 (epix0ip, 2019), https://gist.github.com/epix0ip/ace60d09981be09544fdf355005051505

