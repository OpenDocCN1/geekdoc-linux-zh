
如需广告信息，请拨打我们的销售部门 `1-713-344-1956` 或发送邮件至 `ads@linuxjournal.com`。`www.linuxjournal.com/advertising`

| 广告商 | 页码 | 广告商 | 页码 |
|---|---|---|---|
| APRON, LLC | 41 | USA | 79 |
| www.apron.com | | www.usemux.org/userx0 | |
| APRRO HC SOLUTIONS | C2 | Logic Soft, Inc. | 6 |
| appro.com | | www.logicsoft.com | |
| ASA Computers | 71, 91 | LPI | 67 |
| www.asacom.com | | www.lpi.org | |
| AVGEN CONSULTING | | MICROWAY | C4, 63 |
| www.avgen.com/telecomontrol | | www.microway.com | |
| CAR-NET | | Mar Tech | 45 |
| www.carnet.com | | www.outerboard.com | |
| COAD, Inc. | PO Linux | 27 |
| www.coad.com | | www.polinux.com | |
| CYBER POINT | | POLYCOMP, Inc. | 31 |
| www.cyberpoint.com | | www.poly.com | |
| EMAC, Inc. | | The Portland Group | 29 |
| www.emac.com | | www.portgroup.com | |
| EMPERILUX | 13 | QOL Soft | 5 |
| www.emperilux.com | | qolsoft.com | |
| FARCOM | | Raceway Managed Hosting | C3 |
| www.farcom.com | | www.radspace.com | |
| GINSTOR SYSTEMS, Inc. | 77 | RED TECHNOLOGIES | 15 |
| www.ginstor.com | | www.redtech.com | |
| HPC Systems, Inc. | 9 | Server Direct | 9 |
| www.hpcisystems.com | | www.serversdirect.com | |
| HURRICANE ELECTRIC | 25 | Silicon Machines | 35 |
| www-he.net | | www.siliconmachines.com | |
| INFO, TECH | 21 | SUPER COMPUTER MACHINE | 33 |
| www.info-tech.com | | www.supercomputer.com | |
| INTEL | TECHNICAL SYSTEMS | 14 |
| www.intel.com | | www.embedddsystems.com | |
| KING STAR COMPUTER | 73 | UNWIRED TECHNOLOGIES | 11 |
| www.kingstara.com | | www.unwired.com | |
| LINUX JOURNAL | 16, 93, 95 | WILEY PUBLISHING | 23 |
| www.linuxjournal.com | | www.wiley.com | |

`www.linuxjournal` november 2007 | 81

## 深度解析

诚然，这段代码很笨（（有人会说它是脑残的），但让我们假设它是真实的应用程序。如果你可以做到，我们确实会从这种优化中获益。如果你不能，那么没有比编译器更适合帮助我们的工具了——它只需要理解代码的语义来执行顺序优化。理想情况下，我们需要一个能与我们对话的编译器，帮助我们理解源代码并根据这些信息做出更合理的调整。在这里，我们的 Studio C 让我们使用：

```
$ cc -fgL3 prime.c -o prime

$ er_prime
```

源循环如下：
```
Source loop below:

35    for (int i = 2; i < N; i++) /* 测试开始！ */
```

函数从 `prime.c` 内联到代码中：
Function is inlined from source function_prime, line 14 has tag L4。

最后，编译器用通俗易懂的语言向你解释它对源代码做了哪些转换以提高速度。不仅如此，它还识别了可以嵌套并证明并行化的区域。识别并行化很棒，但如何表达并行化呢？让编译器为我们做这件事可行吗？或者我们必须使用像 GOTOs 这样的指令？无论如何，消息是使用正确的编译器是可以的。但在我们继续之前，让我们记住“并行化程序”的第三步并建立一个基准：

```bash
$ cc -fgL3 prime.c

$ ./prime 200000
```

创建实验数据 test1.er
Number of numbers between 2 and 200000 148933
`$ er_print -statistics test1.er`

整个程序的执行：

| 标签: | 表格: |
|---|---|
| 开始时间 (sec.) | 0.028 |
| 持续时间 (sec.) | 3.364 |
| 总时间 (sec.) | 3.337 |
| 平均数量: | 100 |

`-fast` 命令行选项指示 Studio C 编译器为相同的架构生成尽可能快的代码。最后两个命令实际上执行并运行 main。我们现在知道，无论对源代码做什么，结果都不应该慢于 3.336 秒。考虑到这一点，让我们尝试让编译器不仅识别并行化 `-xautopar`，还表达它 `-autopar`：

```bash
$ cc -fxoptinfo -autopar prime.c -o prime"prime.c"
```

"prime.c", line 14: 未并行，有多个出口
"prime.c", line 14: 未并行，有多个出口

所以，通过两个额外的命令行选项，编译器可以解释为什么我们的两个循环（line 31 `-autopar`）和 lines 14 and 35）可以并行化 `-autopar`。这非常令人印象深刻，但让我们获得速度提升：

```bash
$ export OPT_NUM_THREADS=4

$ ./prime 200000
```

创建实验数据 test2.er
Number of numbers between 2 and 200000 148933
`$ er_print -statistics test2.er`
持续时间 (sec.) 3.331

好在如此（没有显著加快），我们不需要通过设置 `OPT_NUM_THREADS` 环境变量让运行时系统为我们处理任何源代码。或者我们有任何比第 35 行更复杂的问题吗？如果编译器过于保守，就需要介入。但这是 OpenMP 的并行限制。OpenMP 的正式定义规定，如果平台包括 Linux 和 Windows 在所有架构上都支持共享内存并行，我愿意将 OpenMP 视为一种帮助编译器细节化的方法。当我们使用 "autopar" 时，OpenMP 是用的。如此，添加这些建议的并行选项会有并发问题吗？任何指令，如果编译器不理解，它就会跳过。此时，免费编译器可以支持 OpenMP 2.5：Intel 编译器、GCC 4.2 等，那么我们如何使用 OpenMP 来提升编译器？只需在相应行添加以下指令：

```c
#pragma omp parallel for

for (int i = 2; i < N; i++) /* 测试开始！ */

if (is_prime(i)) {
```

并且不需要在命令行选项集中添加 `-autopar`：归根结底，作为软件开发者，我们别无选择完全拥抱并行的世界观。

```bash
$ cc -fast -fxoptinfo -xautopar -xopomp prime.c -o prime

"prime.c", line 14: 未并行，有多个出口

（注：此处原文重复，翻译按要求处理）

"prime.c", line 31: 并行化，生成了串行版本

"prime.c", line 35: 并行化，使用了用户指令
```

太好了，我们让应用程序中的三个循环完全并行化了。看看当出现时看起来困难得多：

```bash
$ .prime 200000

Creating database database.3

Number of numbers between 2 and 200000: 146764

$ er_print -statistics test.3 | grep Duration

(sec.): 1.132
```

无疑，这是一个令人印象深刻的速度，但我们为什么会丢失一些质数呢？也许我们有 146,764 个，而不是 148,933 个。也许编译器没有并行化循环。所以看当我们在 OpenMP 程序中发现一个 bug 时？即使我们在应用程序的并行版本中发现了一个 bug，它也说明了并行化任何东西是多么简单。这意味着当你在正确的轨道上，回归测试变得有意义。

## 深度解析

2 到 2000000 之间的质数数量：148933
`$ er_print -thas1.er`
实验中未记录任何信息

```
$ cc -fast -loopinfo -xautopar -xopenmp prime.c -o prime

$ collect ./prime 2000000
```

创建实验数据库 test.4.er

2 到 2000000 之间的质数数量：148933

`$ er_print -statistics test.4.er | grep Duration`

Duration (sec): 1.130

奇怪。我们不仅得到了正确的结果，而且分析器也没有发现任何异常。它坏了吗？并完全不是。你看，让并发变得如此出名地难以追踪，是因为它们大多数问题都是间歇性的。由于非确定性行为有如此多的形式，它们出现和消失的速度快 2.95 倍。为了 15 分钟的工作以及额外的用于向编译器提供提示的 OpenMP 指令行！

# 并行编程的问题在于，它让你的应用程序的某些部分变得了不确定性。

# 遗留问题

OpenMP 和 `-xautopar` 对 C 语言工作得很好，但 C++ 呢？对于现代 C++ 的那种泛型和模板元编程？简单短的答案是，没有答案。但让我们通过下面的现代 C++ [juice] 示例来看看：取决于应用程序如何运行、系统还有什么在运行以及你使用哪种工具作为常规调试器。线程分析器只显示实际发生的问题。好吧，如果它确实发生了：

```cpp
#include <vector>

#include <iterator>
```

# 资源

```
$ collect -on ./prime 2000000

创建实验数据库 tha.2.er

2 到 2000000 之间的质数数量：148933

$ er_print -thas2.er

总竞态条件：2 实验：tha.2.er
```

摩尔定律：http://www.technology.com/mooreslaw/index.html

```
竞态 #1: Waddall (多个地址)

访问 1: 写入，模型来自第 34 行

[_08db34.main] = 0x00000172, line 37 in 'prime.c'

访问 2: 写入，模型来自第 34 行

[_08db34.main] = 0x00000172, line 37 in 'prime.c'

总竞态条件：1
```

Sun Studio Express: developers.sun.com/sunstudio/downloads/index/jexp

FFMPEG: ffmpeg.mplayer.hq

Intel VTune: http://www.intel.com/cd/software/products/asmo-n/239145.html

```
竞态 #2: Waddall

访问 1: 写入，模型来自第 34 行

[_08db34.main] = 0x00000189, line 38 in 'prime.c'

访问 2: 写入，模型来自第 34 行

[_08db34.main] = 0x00000189, line 38 in 'prime.c'

总竞态条件：1
```

Intel Thread Check: http://www.intel.com/cd/software/products/asmo-n/219699.html

TotalViewDebugger: http://www.totalview.com/index.html

POSIX Threads: http://www.nhpc.edu/training/workshop2/pthreads/MAIN.html

太好了！我们重现了 bug，我们的调试工具发现了竞态条件发生的实际位置：13 和 38。当两个线程找到质数并尝试更新质数数组和总变量时——这是一个竞态条件的示例。但这很容易修复。我们通过两行代码将这些线程序列化解决了这个问题。我们如何用 OpenMP 实现这一点？参见下文

OpenMP: http://www.openmp.org

有效使用 OpenMP: http://www.cmvenports.com/Sessions/GD/EffectiveUse.py

Intel Thread Building Blocks: osstbb.intel.com

```cpp
#37 #pragma omp critical

38 {

39 primes[total] = i;

40 total++;

41 } }
```

Cik: supertech.intel.com/cil

"线程问题": http://www.eeks.edu/Pub/TechRports2006/EEECS-2006-1.pdf
"免费午餐结束了：软件向并发的根本性转变": gotw.ca/publications/concurrency-ddj.html

如此，让我们看看我们的加速比是多少：84 | 2007 年 11 月 | www.linuxjournal.com

```cpp
#include <algorithm>

#include <iostream>

void standard_input_sorter() {
  namespace std;
  vector<string> v;
  copy(istream_iterator<string>(cin), istream_iterator<string>(), back_inserter(v));
  sort(v.begin(), v.end());
}
```

斐波那契数，真的是让我感到难过的事情。即将发布的 OpenMP 3.0 标准中定义的任务威胁性小得多。

## 结论

硬件正朝着并发的根本趋势发展。多核系统现在正在进入笔记本电脑和桌面电脑，除非软件工程师开始考虑这些趋势，否则现代硬件对单个应用程序所能做的非常少。当然，并行编程是困难且容易出错的，有了最新的工具和编程技术，它比 POSIX 线程要复杂得多。承认，这篇文章表明可用性足以成为许多读者的折点，让他们开始考虑在应用程序中使用并发。

```
$ cc -fast -loopinfo -xautopar -sort.cc
```
