
`Aborted (core dumped)` 消息意味着 `ch12-assert` 创建了一个核心文件；即进程死亡前其地址空间的快照。² 这个文件稍后可以与调试器一起使用；参见第 15.3 节，“GDB 基础”，第 570 页。创建核心文件是 `assert()` 的一个有意副作用；假设是出了大问题，你将希望使用调试器检查该进程以确定原因。

你可以通过使用命令行选项 `-DNDEBUG` 编译程序来禁用断言。如果在包含 `<assert.h>` 之前定义了此宏，`assert()` 宏将展开为不执行任何操作的代码。例如：

```bash
$ gcc -DNDEBUG ch12-assert.c -o ch12-assert
Compile with -DNDEBUG
$ ch12-assert
Run it
Segmentation fault (core dumped)
What happened?
```

在这里，我们得到了真正的核心转储！我们知道断言已被禁用；没有“断言失败”消息。那么发生了什么？考虑 `lsearch()` 的第 15 行，当从 `main()` 的第 37 行调用时。在这种情况下，`array` 变量为 `NULL`。通过 `NULL` 指针访问内存是一个错误。（从技术上讲，各种标准将解引用 `NULL` 指针时发生的情况留为“未定义”。大多数现代系统所做的与 `GNU/Linux` 相同；它们通过发送 `SIGSEGV` 信号来终止进程；这反过来会产生核心转储。此过程在第 10 章“信号”，第 347 页中描述。）

> ² 如第 10.2 节“信号操作”，第 348 页所述，一些 `GNU/Linux` 发行版禁用了核心文件的创建。要重新启用它们，请将行 `ulimit -S -c unlimited` 放入你的 `~/.profile` 文件中。

这个案例提出了关于断言的一个重要观点。程序员经常错误地使用断言来 `替代` 运行时错误检查。在我们的情况下，对 `array != NULL` 的测试应该是运行时检查：

```c
if (array == NULL)
  return -1;
```

对 `size > 0` 的测试（第 13 行）问题较小；如果 `size` 为 0 或小于 0，循环永远不会执行，并且 `lsearch()` （正确地）返回 `-1`。（实际上，这个断言是不必要的，因为代码正确地处理了 `size <= 0` 的情况。）

禁用断言背后的逻辑是，额外的检查可能会减慢程序性能，因此它们应该在程序的生产版本中禁用。然而，`C.A.R. Hoare`³ 指出了这一点：

> 最后，在调试运行时进行复杂的安全检查，此时并不信任结果，然后在生产运行时移除它们，此时错误的结果可能代价高昂或灾难性，这是荒谬的。如果一位帆船爱好者在陆地训练时穿着救生衣，但一进入海上就把它脱掉，我们会怎么看他？

鉴于这些观点，我们的建议是有深思熟虑地使用断言：首先，对于任何给定的断言，考虑它是否应该改为运行时检查。其次，小心地放置你的断言，这样你才不会介意保留断言检查处于启用状态，即使在程序的生产版本中也是如此。

最后，我们将注明 `GNU/Linux` `assert(3)` manpage 的“BUGS”部分中的以下内容：

> `assert()` 实现为一个宏；如果测试的表达式有副作用，程序行为将取决于是否定义 `NDEBUG`。这可能会产生海森堡虫（Heisenbugs），即在开启调试时消失的 Bug。

海森堡著名的物理不确定原理表明，你确定粒子速度的精度越高，确定其位置的精度就越低，反之亦然。用通俗的话说，它表示仅仅观察粒子的行为就会影响它。

³ **编程语言设计提示**，`C.A.R. Hoare`，斯坦福大学计算机科学技术报告 `CS-73-403` (`ftp://reports.stanford.edu/pub/catc/reports/cs/rr/73/403/CS-TR-73-403.pdf`)，1973 年 12 月。

编程中也发生了类似的现象，与粒子物理无关：为调试编译程序，或启用调试运行它可以改变程序的行为。特别是，原始的 bug 可能会消失。这种 bug 俗称 `海森堡虫`（heisenbug）。

manpage 警告我们不要在 `assert()` 调用中放入有副作用的表达式：

```c
assert(*p++ == '\n');
```

这里的副作用是 `p` 指针作为测试的一部分被递增。当定义 `NDEBUG` 时，表达式参数从源代码中 `消失`；它永远不会被执行。这可能导致意外的失败。然而，一旦在准备调试时重新启用断言，事情就开始正常工作了！这类问题很难追踪。

## 12.2 底层内存：`memXXX()` 函数

有几个函数提供用于处理任意内存块的底层服务。它们的名称都以前缀 `mem` 开头：

```c
#include <string.h>                    ISO C

void *memset(void *buf, int val, size_t count);
void *memcpy(void *dest, const void *src, size_t count);
void *memmove(void *dest, const void *src, size_t count);
int memcmp(const void *buf1, const void *buf2, size_t count);
void *memchr(const void *buf, int val, size_t count);
```

### 12.2.1 设置内存：`memset()`

`memset()` 函数将值 `val`（作为 `unsigned char` 处理）复制到 `buf` 的前 `count` 个字节中。它对于将动态内存块清零特别有用：

```c
void *p = malloc(count);
if (p != NULL)
  memset(p, 0, count);
```

然而，`memset()` 可用于任何类型的内存，而不仅仅是动态内存。其返回值是第一个参数：`buf`。

### 12.2.2 复制内存：`memcpy()`、`memmove()` 和 `mempcpy()`

三个函数将一个内存块复制到另一个内存块。前两个函数在如何处理 `重叠` 内存区域方面有所不同；第三个函数复制内存，但在看到特定值时停止。

```c
void *memcpy(void *dest, const void *src, size_t count)
```

这是最简单的函数。它从 `src` 复制 `count` 个字节到 `dest`。它不处理重叠的内存区域。它返回 `dest`。

```c
void *memmove(void *dest, const void *src, size_t count)
```

类似于 `memcpy()`，它也从 `src` 复制 `count` 个字节到 `dest`。然而，它确实处理重叠的内存区域。它返回 `dest`。

```c
void *mempcpy(void *dest, const void *src, int val, size_t count)
```

注意：此处原文参数似乎有误（`mempcpy` 标准签名通常为 `mempcpy(dest, src, count)`，但原文描述了类似 `mempcpy` 寻找特定值的行为，可能作者指的是某种变体或笔误，但根据指示翻译原文内容）：

这从 `src` 复制字节到 `dest`，在复制 `val` 到 `dest` `或` 复制 `count` 个字节之后 `任一` 情况下停止。如果它找到了 `val`，它返回指向 `dest` 中 `val` 放置位置之后的指针。否则，它返回 `NULL`。

现在，重叠内存有什么问题？考虑图 12.1。

```c
struct xyz { ... } data[8];
mempcpy(&data[3], data, sizeof(data[0]) * 4);
```

对比。

```c
memmove(&data[3], data, sizeof(data[0]) * 4);
```

![](img/766b5597246d532412fad21b1c59ccec_465_0.png)

#### 图 12.1 重叠复制

目标是将 `data[0]` 到 `data[3]` 中的四个 `struct xyz` 实例复制到 `data[3]` 到 `data[6]`。`data[3]` 是这里的问题；从 `data[0]` 在内存中向前逐字节复制会在 `data[3]` 被安全复制到 `data[6]` 之前将其覆盖！（也可能出现通过内存向后复制破坏重叠数据的情况。）

`memcpy()` 函数最初是 System V 用于复制内存块的 API；对于重叠内存块的行为，并未以特定方式加以明确规定。在 1989 年 C 标准制定时，委员会认为这种未定义的行为是一个问题；因此，他们发明了 `memmove()`。为了保持历史兼容性，`memcpy()` 保持不变，其针对重叠内存的行为被明确声明为未定义，而 `memmove()` 则被创造出来，以提供一个能够正确处理问题情况的例程。
