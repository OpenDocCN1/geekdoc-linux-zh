版的著作，比如我和 Christophe Nasarre 合写的 *Windows via C/C++*(Microsoft Press, 2007)①。

**注意** 在.NET Framework 的早期岁月，CLR 团队认为有朝一日 CLR 会提供不一定会映射到 Windows 线程的逻辑线程。但大约在 2005 年的时候，这个尝试宣告失败，CLR 团队放弃了在这方面的努力。所以，今天的 CLR 线程完全等价于 Windows 线程。但.NET Framework 仍然留下了一些能看出当年努力成果的一些东西。例如，**System.Environment** 类公开了 **CurrentManagedThreadId** 属性，返回线程的 CLR ID；而 **System.Diagnostics.ProcessThread** 类公开了 **Id** 属性，返回同一个线程的 Windows ID。**System.Thread** 类的 **BeginThreadAffinity** 和 **EndThreadAffinity** 方法则处理 CLR 线程没有映射到 Windows 线程的情况。

**注意** Microsoft 为 Windows Store 应用移除了和线程处理有关的一些 API，因为它们鼓励不好的编程实践(就像 26.3 节“停止疯狂”描述的那样)，或者是因为它们不利于达成 Microsoft 为 Windows Store 应用设立的目标。例如，整个 **System.Thread** 类都不开放给 Windows Store 应用，因为其中有许多不好的 API(比如 **Start**、**IsBackground**、**Sleep**、**Suspend**、**Resume**、**Join**、**Interrupt**、**Abort**、**BeginThreadAffinity** 和 **EndThreadAffinity**)。我个人赞成这个做法，而且认为早就该这么做。所以，第 26 章到第 30 章讨论了适合桌面应用但不适合 Windows Store 应用的一些 API 和功能。阅读过程中能清楚地认识到为何有一些 API 不适合 Windows Store 应用。

# ### 26.6 使用专用线程执行异步的计算限制操作

本节展示如何创建线程来执行异步的计算限制(compute-bound)操作。虽然会展示完整过程，但强烈建议避免使用这个技术。而且事实上，由于 **Thread** 类不可用，所以构建 Windows Store 应用时根本用不了这个技术。相反，应尽量使用线程池来执行异步的计算限制操作，这方面的详情将在第 27 章“计算限制的异步操作”讨论。

但极少数情况下，你可能想显式创建线程来专门执行一个计算限制的操作。如果执行的代码要求线程处于一种特定状态，而这种状态对于线程池线程来说是非同寻常的，就可考虑创建专用线程。例如，满足以下任何条件，就可显式创建自己的线程。

+   - 线程需要以非普通线程优先级运行。所有线程池线程都以普通优先级运行；虽然可以更改这个优先级，但不建议那样做。另外，在不同的线程池操作之间，对优先级的更

> > ① 简体中文版是《Windows 核心编程(第 5 版)》，繁体中文版是《Windows 应用程序开发经典》。分别由清华大学出版社和悦知文化出版。我参与了它的翻译。——译注