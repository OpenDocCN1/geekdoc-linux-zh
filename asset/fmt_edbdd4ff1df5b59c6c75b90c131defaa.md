
该程序使用流水线（pipeline）来生成素数。流水线中的每个线程都需要一个用于检查的输入队列、一个它负责的素数，以及一个用于汇总检查失败数字的输出队列。如果线程持有一个检查失败的数字且没有子线程，则该线程找到了一个新的素数。在这种情况下，会为该素数创建一个新的子线程并将其挂在流水线的末端。

这听起来可能比实际要复杂，所以让我们逐段分析这个程序，看看它的作用。（对于那些可能正在试图回忆切什么是素数的人，它是一个只能被自身和 1 整除的数字）。

大部分工作由 `check_num()` 子程序完成，它接收输入队列的引用和一个它负责的素数。在存入输入队列和素数后，子程序开始进行检查（第 11 行），我们创建一个新队列（第 13 行），并为之后可能创建的线程留出一个标量（第 12 行）。

从 14 行到 26 行的循环从输入队列中获取一个标量，并与该线程负责的素数进行对比。对于每次检查是否存在一个不能被 `num` 整除的数字的操作，我们将待检查的队列除以该素数。如果有一个，就发送到我们已经创建的下一个线程（第 17 行），如果我们还没有创建，则创建一个新线程。

新创建的线程位于第 20 行。在传递给我们创建的队列引用之前，传递我们找到的素数。在第 21 行到 24 行之间，我们检查新线程是否已获取到数字，如果没有，则停止队列中剩余的数字。

最后，一旦循环因为从队列收到 `0 undef`（这用作终止信号）而终止，我们将通知传递给子线程，并且如果我们创建了子线程，则等待它退出（第 27 行和第 30 行）。

同时，回到主线程，我们创建一个队列（第 33 行），并填充从 3 到 1000 的数字进行检查，外加一个终止节点。然后，我们只需要为了让程序运行起来，只需将队列和第一个素数传递给 `check_num()` 子程序（第 34 行）。

这就是它的工作原理。它和许多 Perl 程序一样非常简单，解释比程序还要长。

# 线程的不同实现方式

从操作系统的角度来看线程实现的背景。线程基本分为三类：用户态线程、内核线程和多处理器内核线程。

用户态线程是完全存在于程序及其库中的线程。在这种模型中，操作系统对线程一无所知。对于操作系统来说，你的进程只是一个进程。

这是实现线程最简单的方法，由于操作系统对线程一无所知，如果其中一个线程阻塞，所有线程都会阻塞。典型的阻塞活动包括大多数系统调用、大多数 I/O 以及像 `sleep()` 这样的操作。

内核线程是线程演变的下一步。操作系统感知内核线程并为它们留出空间。内核线程和用户态线程之间的主要区别在于阻塞。对于内核线程，阻塞单个线程的线程不会阻塞其他线程。用户态线程则不然，因为内核阻塞的是进程级而不是线程级。

这是一个巨大的进步，可以为线程化程序带来比非线程化程序的性能提升。例如，执行 I/O 的阻塞线程不会阻塞正在执行其他事情的线程。无论系统有多少个 CPU，每个进程仍然只有一个线程同时运行。

由于内核线程可以随时中断线程，它们将揭示你在程序中可能做出的隐式锁定假设。例如，像 `$x = $x + 2` 这样简单的操作，如果 `$x` 对其他线程可见，在内核线程中可能是不可预测的，因为另一个线程可能在它从右侧获取 `$x` 的时间之间更改了 `$x`。

多处理器内核线程是最后一步。有了多处理器内核线程，线程可以在不同的 CPU 上同时运行。

## 系统库的线程安全性

各种库调用在 Perl 的控制之外是否是线程安全的，这往往是不确定的。通常不是线程安全的调用包括：`localtime()`、`gettime()`、获取用户、组和网络信息的函数（例如 `getgetent()`、`gethostname()`、`getname()` 等）、`readdir()`、`rand()` 以及 `srand()`。总而言之，这些都是依赖于某些全局外部状态的调用。

如果系统 Perl 在编译时使用了此类调用的线程安全变体，则将使用它们。除此，Perl 取决于这些调用的线程安全性或不安全性。请查阅您的 C 库调用文档。

在某些平台上，如果结果缓冲区太小，线程安全的库接口可能会失败（例如，用户组数据库可能非常大，而重入接口可能必须携带这些数据库的完整快照）。Perl 将从一个小的缓冲区开始，但会不断重试并增大结果缓冲区，直到结果符合大小为止。如果这种无限制的增长从安全或资源消耗的角度听起来不好，您可以在重新编译 Perl 时定义 `PERL_REENTRANT_MAXSIZE` 为您允许的最大字节数。

## 结论

一个完整的线程教程可以写满一本书（而且已经写过很多次），但根据我们在介绍中涵盖的内容，您已经在成为线程化 Perl 专家的道路上了。

## 另请

关于线程的注释版 POD：`<%field=Module&na=threads>`

CPAN 上 threads 的最新版本：`< >`

关于 threads::shared 的注释版 POD：`<%field=Module&na=threads%3A%3Ashared>`

CPAN 上 threads::shared 的最新版本：`< >`

Perl 线程邮件列表：`< >`

## 参考文献

以下是受 Julian Christoffel 感谢提供的简短参考文献：

### 入导性文本

- Birrell, Andrew D. *An Introduction to Programming with Threads*. Digital Equipment Corporation, 1989, DEC-SRC Research Report #35 在线（强烈推荐）
- Robbins, Kay. A., and Steve Robbins. *Practical Unix Programming: A Guide to Concurrency, Communication, and Multithreading*. Prentice-Hall, 1996.
- Lewis, Bill, and Daniel J. Berg. *Multithreaded Programming with Pthreads*. Prentice Hall, 1997, ISBN 0-13-44368-9（关于线程的极佳介绍）。
- Nelson, Greg (编辑). *Systems Programming with Modula-3*. Prentice Hall, 1991, ISBN 0-1590464-1.
- Nichols, Bradford, Dick Butlar, and Jacqueline Proulx Ferrell. *Pthreads Programming*. O’Reilly & Associates, 1996, ISBN 156592-115-1（涵盖 POSIX 线程）。

### 操作系统相关参考

- Boykin, Joseph, David Kirschen, Alan Langerman, and Susan LoVerso. *Programming under Mach*. Addison-Wesley, 1994, ISBN 0-201-52739-1.
- Tanenbaum, Andrew S. *Distributed Operating Systems*. Prentice Hall, 1995, ISBN 0-13-219908-4（优秀的教材）。
- Silbersatz, Abraham, and Peter B. Galvin. *Operating System Concepts*, 4th ed. Addison-Wesley, 1995, ISBN 0-201-59292-4

### 其他参考

- Arnold, Ken and Jas Gosling. *The Java Programming Language*, 2nd ed. Addison-Wesley, 1998, ISBN 0-201-3106-6.
- comp.programming.threads FAQ，`< >`
- Le Sergent, T. and B. Berthomieu. “Incremental MultiThreaded Garbage Collection on Virtually Shared Memory Architectures” in Memory Manager: Proc. of the International Workshop IWMM 92, St. Malo, France, September 1992, Yves Bekkers and Jacques Cohen, eds. Springer, 1992, ISBN 3540-55940-X（真实的线程应用）。
- Artur Bergman, “Where Wizards Fear To Tread”, 2002年6月11日，`< >`

## 致谢

感谢（不分先后顺序）Chaim Frenkel、Steve Fink、Gurusamy Sarathy、Ilya Zakharevich、Benjamin Sugars、Julian Christoffel、Joshua Pritikin 和 Alan Burlison，感谢他们在核实事实和润色本文方面提供的帮助。非常感谢 Tom Christiansen 对打印机生成器的重写。

# 作者

Dan Sugalski >>

由 Arthur Bergman 略微修改以适应新的线程模型/模块。

由 Joao Walter >> 稍微重写，使关于 Perl 代码线程性的描述更加简洁。

由 Elizabeth Mattijsen >> 稍微重新安排，以减少对 `yield()` 的强调。

## 版权

本文最初最早于 *The Perl Journal #10*，版权所有 1998 *The Perl Journal*。感谢 Jon Orwant 和 *The Perl Journal*。此文档可以按照 Perl 本身相同的条款分发。

## PERLTIE

### 名字

perltie - 如何在简单变量中隐藏对象类

## 概要

```
