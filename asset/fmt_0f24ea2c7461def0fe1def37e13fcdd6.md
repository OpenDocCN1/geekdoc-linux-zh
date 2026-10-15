
`kali@kali:~$ john --rules --wordlist=/usr/share/wordlists/rockyou.txt unshadowed.txt`

```
Using default input encoding: UTF-8

Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])

Cost 1 (iteration count) is 5000 for all loaded hashes

Will run 2 OpenMP threads

Press 'q' or Ctrl-C to abort, almost any other key for status

s3cr3t (victim)

1g 0:00:00:28 DONE (2019-08-20 15:42) 0.03559g/s 2497p/s 2497c/s 2497C/s
...
```

### 列表 623 - 使用 John the Ripper 破解 Linux 密码哈希

较新版本的 `John the Ripper` 默认支持多线程，但旧版本仅使用单个 CPU 核心执行破解操作。如果你遇到的是旧版 JTR，它支持可以加速过程的替代方案。我们可以采用多个 CPU 核心，甚至多台计算机，来分配负载并加速破解过程。`--fork` 选项启用多个进程，以便在单台机器上利用更多的 CPU 核心，而 `--node` 则跨多台机器分配工作。

例如，假设我们有两台机器，每台机器都有 8 核 CPU。在第一台机器上，我们设置 `--fork=8` 和 `--node=1-8/16` 选项，指示 `John` 在此机器上创建八个进程，将提供的词表分成十六个相等的部分，并在本地处理前八部分。在第二台机器上，我们可以使用 `--fork=8` 和 `--node=9-16` 将八个进程分配给词表的后半部分。以这种方式分配工作大约可以提供 16 倍的性能提升。

> *攻击者还可以预先计算密码的哈希值（这可能花费大量时间），并将它们存储在巨大的数据库中，或者存储在彩虹表中，[585] 从而使密码破解变成简单的表查找过程。这是一种空间-时间权衡，因为这些表可能会消耗大量的空间（根据密码复杂度可达 PB 级别），但密码“破解”过程本身（技术上是一个查找过程）所花费的时间要少得多。*

虽然 `John the Ripper` 是破解密码哈希的绝佳工具，但其速度受限于专门用于该任务的 CPU 算力。近年来，图形处理器（GPU）变得极其强大，而且当然存在于每台带有显示器的计算机中。高端机器，如用于视频编辑和游戏的主机，配备了极其强大的 GPU。`Hashcat` [586] 等 GPU 破解工具利用 CPU 和 GPU 的强大功能，达到了惊人的密码破解速度。

`Hashcat` 的选项通常镜像 `John the Ripper` 的选项，并包括算法检测和密码列表变形等功能。

在此示例中，我们将在配备 GeForce GTX 1080 Ti GPU 的机器上以基准测试模式（`-b`）运行 `hashcat`：

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

Speed,Dev.#1......: 1567.9 MH/s (92.38ms) @ Accel:128 Loops:64 Thr:640 Vec:1

Hashmode: 1000 – NTLM

Speed,Dev.#1......: 65267.0 MH/s (55.66ms) @ Accel:128 Loops:1024 Thr:1024 Vec:1

Hashmode: 5500 – NetNTLMv1 / NetNTLMv1+ESS

Speed,Dev.#1......: 33504.0 MH/s (55.00ms) @ Accel:128 Loops:512 Thr:1024 Vec:1

Hashmode: 5600 – NetNTLMv2

Speed,Dev.#1......: 2761.2 MH/s (83.59ms) @ Accel:128 Loops:64 Thr:1024 Vec:1

Hashmode: 1800 – sha512crypt $6$, SHA512 (Unix) (Iterations: 5000)

Speed,Dev.#1......: 218.6 kH/s (51.55ms) @ Accel:512 Loops:128 Thr:32 Vec:1 ....
```
