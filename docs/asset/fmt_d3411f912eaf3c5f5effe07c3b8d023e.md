
# 并行处理与密码破解

`dispy` 模块有许多替代方案（`https://wiki.python.org/moin/ParallelProcessing`），但它被选中是因为它非常适合我们这种分布式哈希的简单并行。如果您想仅使用多核机器来研究并行处理，您应该查看 Python 原生的 `multiprocessing` 库。这使得设置共享变量比在进程非本地时更容易、更一致。如果您想更深入地探索并行处理的兔子洞，您应该掌握消息解析接口（`MPI`）。

## John the Ripper

`John the Ripper` 是一个流行的开源密码破解器。还有一个社区增强版，提供了 GPU 破解支持，以及一些额外的哈希和密码类型。该版本（代号 `Jumbo`）的源代码可在项目网站 `www.openwall.com/john` 上获得。我们可以在 Pi 上从源代码编译它。`Raspbian` 默认包含 `gcc`，但我们

## 其他 Bramble 项目

### Office document cracking (10 Raspberry Pis)

`http://bit.ly/10PICluster`

Shane 的项目使用 JiT 的一个补丁版本来破解受密码保护的 MS Office、LibreOffice 和 PDF 文档。MS Office 2007 引入了 128 位密钥的 AES 加密，ouch！

### Tower of Pi (10 Raspberry Pis)

`http://bit.ly/10PITower`

这使用了 9 台 RPi 从节点和 1 台 Cubie 板作为 `MPI` 处理的主控制器。它有一个漂亮的 16x2 RGB 显示屏用于状态信息。现在它已被重新用作 32 节点的 Cubical Monolith 项目。

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_57_0.png)

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_57_1.png)

此外还需要 `libssl` 和 `libcrypto` 头文件。以下命令将在 `Raspbian` 上安装这些，前提是你有可用的互联网连接：

```
$ apt-get update
```

```
$ apt-get install libssl-dev
```

从网站下载源代码，然后解压并像这样开始漫长的编译过程：

```
$ tar -xzvf john-8VER-jumbo-SREL.tar.gz
```

```
$ cd john/src
```

```
$ make generic
```

这在标准频率的 Pi 上大约需要半小时。构建完成后，我们可以使用以下命令测试安装：

```
$ cd ../run
```

```
$ ./john -test
```

我们新挤出的二进制文件将对其所有可用算法进行基准测试。`RawMD5` 在我们的设备上得分约为 330kH/s，比我们的 Python 实现高出约 50 倍。对于 `SHA-1`（`--mode=raw-sha`），`John` 实现了令人尊敬的 190kH/s。现在制作一个文本文件 `target.md5`，其中包含一行我们之前使用的目标 MD5 哈希，以 392b2 开头。我们可以通过使用增量模式和 Alnum 字符集来实现仅字母数字的字符集。

```
$ ./john --incremental=alnum --length=6 --format=raw-md5 target.md5
```

这在普通的 Raspberry Pi 上可能需要大约两天才能完成，而且仍然找不到所需的原像。这仍然是留给您，亲爱的读者，一个挑战。然而，您的挑战因 JTR 极其有用的 `--node` 选项而变得更容易，这使您能够实现一些原始并行。例如，如果我们用五台 Pi 饱和我们的交换机，我们可以在

the previous code, replacing n with the number of the Raspberry Pi on which it is being run. This will cause John to work on only the relevant fifth of the possible inputs, so that we could realistically expect to get through all six-character alphanumeric passwords in about 10 hours.

您可以使用 `md5sum` 命令生成 MD5 哈希。例如：

```
$ echo -n "test"|md5sum
096f6bcd4621d373cade4e832627b4f6 -
```

将此结果粘贴到文件 `test.md5` 中，不要包含末尾的空格和破折号（`md5sum` 最常用于哈希文件，文件名通常会放在这些字符之后 – 如果这让你困扰，可以添加 `|cut -d ' ' -f1`）。现在运行以下命令来说服自己 John 确实能够正确处理这些哈希。

```
$ ./john --incremental=alnum --length=4 --format=raw-md5 test.md5
```

## 单词有效

不提及 JTR 更智能的词表模式是不合适的。网站上有许多词表可用，你也可以定义用于组合它们的变形规则。甚至可以使用混合模式结合一些增量字符，以在宇宙终结前最大化成功几率。截至撰写时，最令人印象深刻的 MD5 基准接近 2GH/s（这是借助 16 块 Radeon 7550 的结果）。凭借如此强大的性能，使用我们一直在使用的 62 个字符的八字符密码可能在一周内就能恢复。更快的技术总是近在咫尺，因此八字符密码是安全的这一老说法不再成立。总之：给自己找一个密码管理器并保持安全，孩子们。

## David Gull's 40-Pi cluster

`http://bit.ly/40PiCluster`

David 的目标是制作一个行为完全像真品的模型超级计算机。这台大家伙有 12 个 1TB 驱动器和 6 个外部以太网端口。CNC 激光切割机用于制作时尚的外壳。

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_58_0.png)

## Southampton University Iridis-Pi Lego Supercomputer (64 Pis)

`http://bit.ly/64PISuperComputer`

整个东西仅花费 £2,500 建造，并在所有 12 个节点上运行 `HPL` 矩阵求逆基准测试时达到 1.14Gflops/s。它使用较旧的 256MB 型号，因此内存稀缺。

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_58_1.png)

## 免费的 Android

Android 变得越来越不开源了吗？我们认为它正朝这个方向漂移，并调查 Linux 社区对此能做些什么。

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_59_0.png)

我们喜欢把 Android 吹捧为开源在商业世界取得成功的例子，而且是在一个竞争极其激烈的领域。关于“今年会是 Linux 桌面之年吗？”的种种讨论逐渐淡去，因为一个基于 Linux 的操作系统，尽管不是我们熟悉的 GNU/Linux，却开始一家手机一家手机地接管世界。

然而，我们想得较少的是，虽然 Android 使用开源内核，而且操作系统的大部分也是开源的，但其中越来越多的部分正在变成闭源，而它所依赖的网络服务也是如此。

智能手机和平板电脑是联网设备——当不联网时它们的功能严重受限，而 Android 手机默认使用 Google 服务。这些服务不是开源的——`GPL` 对通过网络提供的服务并不适用，因为软件并未被分发，只有其输出被分发。因此，你的开源手机依赖于运行闭源服务的服务器群。是的，你可以选择使用不同的邮件提供商来代替 Gmail，但 Google 地图和导航有没有开源替代品呢？`OpenStreetMap` 做得不错，但无论是覆盖范围还是精致程度都无法与 Google 地图和导航相比。

> “你的开源手机依赖于运行闭源服务的服务器。”

再见了。

### 开源与闭源

2007 年 Google 开源 Android 是明智之举：苹果 iPhone 已经发布，它希望避免移动生态系统像桌面几乎发生的那样被一个操作系统主导。因此它将 Android 作为开源发布，并且迅速成长。现在 Android 已成为主导的操作系统，Google 想要收回控制权。它无法对内核以及从外部获得的任何其他开源组件做什么，但它一直在逐步将自己的软件转为闭源，一次‘更新’一次。
