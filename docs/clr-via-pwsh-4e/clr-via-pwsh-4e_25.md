## 第二十一章 托管堆和垃圾回收

本章内容：

- 托管堆基础
- 代：提升性能
- 使用需要特殊清理的类型
- 手动监视和控制对象生存期

本章要讨论托管应用程序如何构造新对象，托管堆如何控制这些对象的生存期，以及如何回收这些对象的内存。简单地说，本章要解释 CLR 中的垃圾回收器是如何工作的，还要解释相关的性能问题。另外，本章讨论了如何设计应用程序来最有效地使用内存。

### 21.1 托管堆基础

每个程序都要使用这样或那样的资源，包括文件、内存缓冲区、屏幕空间、网络连接、数据库资源等。事实上，在面向对象的环境中，每个类型都代表可供程序使用的一种资源。要使用这些资源，必须为代表资源的类型分配内存。以下是访问一个资源所需的步骤。

- 1. 调用 IL 指令 newobj，为代表资源的类型分配内存（一般使用 C# new 操作符来完成）。
- 2. 初始化内存，设置资源的初始状态并使资源可用。类型的实例构造器负责设置初始状态。
- 3. 访问类型的成员来使用资源（有必要可以重复）。
- 4. 摧毁资源的状态以进行清理。
- 5. 释放内存。垃圾回收器独自负责这一步。

如果需要程序员手动管理内存（例如，原生 C++ 开发人员就是这样的），这个看似简单的模式就会成为导致大量编程错误的“元凶”之一。想想看，有多少次程序员忘记释放不再需要的内存而造成内存泄漏？又有多少次试图使用已经释放的内存，然后由于内存被破坏而造成程序错误和安全漏洞？而且，这两种 bug 比其他大多数 bug 都要严重，因为一般无法预测它们的后果或发生的时间①。如果是其他 bug，一旦发现程序行为异常，改正出问题的代码行就可以了。

> ① 例如，访问越界的 bug 可能取回不相干的数据，使程序结果变得不正确。而且错误没有规律，让人捉摸不定。——译注

现在，只要写的是可验证的、类型安全的代码（不要用 C# unsafe 关键字），应用程序就不可能会出现内存被破坏的情况。内存仍有可能泄漏，但不像以前那样是默认行为。现在内存泄漏一般是因为在集合中存储了对象，但不需要对象的时候一直不去删除。

> 注：PowerShell 里没有 `unsafe` 关键字，脚本本身也无法做指针运算，所以托管堆不会因脚本代码而被破坏。风险来自通过 `Add-Type` 编译的 C# 代码或 P/Invoke 拿到原生句柄：不安全代码被带进进程后，PowerShell 无法替它做类型安全检查。脚本中的内存泄漏表现为变量、事件订阅或 `[System.Collections.Generic.List[object]]` 等集合长期持有对象引用。

为了进一步简化编程，开发人员经常使用的大多数类型都不需要步骤 4（摧毁资源的状态以进行清理）。所以，托管堆除了能避免前面提到的 bug，还能为开发人员提供一个简化的编程模型：分配并初始化资源并直接使用。大多数类型都无需资源清理，垃圾回收器会自动释放内存。

使用需要特殊清理的类型时，编程模型还是像刚才描述的那样简单。只是有时需要尽快清理资源，而不是非要等着 GC① 介入。可在这些类中调用一个额外的方法（称为 Dispose），按照自己的节奏清理资源。另一方面，实现这样的类需要考虑到较多的问题（21.4 节会详细讨论）。一般只有包装了本机资源（文件、套接字和数据库连接等）的类型才需要特殊清理。

#### 21.1.1 从托管堆分配资源

CLR 要求所有对象都从托管堆分配。进程初始化时，CLR 划出一个地址空间区域作为托管堆。CLR 还要维护一个指针，我把它称作 **NextObjPtr**。该指针指向下一个对象在堆中的分配位置。刚开始的时候，**NextObjPtr** 设为地址空间区域的基地址。

> 注：PowerShell 中新建对象同样走这条分配路径，只是入口不同：`[System.Text.StringBuilder]::new()`、`New-Object System.Text.StringBuilder` 或 `[pscustomobject]@{}` 都会在托管堆上创建对象并由 GC 管理，脚本无法指定分配位置，也拿不到 `NextObjPtr`。`[pscustomobject]` 本质上是 `PSObject` 包装的 `PSCustomObject` 实例，同样受 GC 管理。

一个区域被非垃圾对象填满后，CLR 会分配更多的区域。这个过程一直重复，直至整个进程地址空间都被填满。所以，你的应用程序的内存受进程的虚拟地址空间的限制。32 位进程最多能分配 1.5 GB，64 位进程最多能分配 8 TB。

C# 的 **new** 操作符导致 CLR 执行以下步骤。

- 1. 计算类型的字段（以及从基类型继承的字段）所需的字节数。
- 2. 加上对象的开销所需的字节数。每个对象都有两个开销字段：类型对象指针和同步块索引。对于 32 位应用程序，这两个字段各自需要 32 位，所以每个对象要增加 8 字节。对于 64 位应用程序，这两个字段各自需要 64 位，所以每个对象要增加 16 字节。
- 3. CLR 检查区域中是否有分配对象所需的字节数。如果托管堆有足够的可用空间，就在 **NextObjPtr** 指针指向的地址处放入对象，为对象分配的字节会被清零。接着调用类型的构造器（为 **this** 参数传递 **NextObjPtr**），**new** 操作符返回对象引用。就在返回这个引用之前，**NextObjPtr** 指针的值会加上对象占用的字节数来得到一个新值，即下个对象放入托管堆时的地址。

图 21-1 展示了包含三个对象（A、B 和 C）的一个托管堆。如果要分配新对象，它将放在 **NextObjPtr** 指针指向的位置（紧接在对象 C 后）。

![](img/6fa065e17c4549db7260fbfaf4fd384e_465_0.png)

图 21-1　新初始化的托管堆，其中构造了 3 个对象

对于托管堆，分配对象只需在指针上加一个值——速度相当快。在许多应用程序中，差不多同时分配的对象彼此间有较强的联系，而且经常差不多在同一时间访问。例如，经常在分配一个 **BinaryWriter** 对象之前分配一个 **FileStream** 对象。然后，应用程序使用 **BinaryWriter** 对象，而后者在内部使用 **FileStream** 对象。由于托管堆在内存中连续分配这些对象，所以会因为引用的“局部化”（locality）而获得性能上的提升。具体地说，这意味着进程的工作集会非常小，应用程序只需使用很少的内存，从而提高了速度。还意味着代码使用的对象可以全部驻留在 CPU 的缓存中。结果是应用程序能以惊人的速度访问这些对象，因为 CPU 在执行大多数操作时，不会因为“缓存未命中”（cache miss）而被迫访问较慢的 RAM。

根据前面的描述，似乎托管堆的性能天下无敌。但先别激动，刚才说的有一个大前提——内存无限，CLR 总是能分配新对象。但内存不可能无限，所以 CLR 通过称为“垃圾回收”（GC）的技术“删除”堆中你的应用程序不再需要的对象。

#### 21.1.2 垃圾回收算法

应用程序调用 **new** 操作符创建对象时，可能没有足够地址空间来分配该对象。发现空间不够，CLR 就执行垃圾回收。

> **重要提示** 前面的描述过于简单。事实上，垃圾回收是在第 0 代满的时候发生的。本章后面会解释“代”。在此之前，先假设堆满就发生垃圾回收。

至于对象生存期的管理，有的系统采用的是某种引用计数算法。事实上，Microsoft 自己的“组件对象模型”（Component Object Model，COM）用的就是引用计数。在这种系统中，堆上的每个对象都维护着一个内存字段来统计程序中多少个“部分”正在使用对象。随着每一“部分”到达代码中某个不再需要对象的地方，就递减对象的计数字段。计数字段变成 0，对象就可以从内存中删除了。许多引用计数系统最大的问题是处理不好循环引用。例如在 GUI 应用程序中，窗口将容纳对子 UI 元素的引用，而子 UI 元素将容纳对父窗口的引用。这种引用会阻止两个对象的计数器达到 0，所以两个对象永远不会删除，即使应用程序本身不再需要窗口了。

鉴于引用计数垃圾回收器算法存在的问题，CLR 改为使用一种引用跟踪算法。引用跟踪算法只关心引用类型的变量，因为只有这种变量才能引用堆上的对象；值类型变量直接包含值类型实例。引用类型变量可在许多场合使用，包括类的静态和实例字段，或者方法的参数和局部变量。我们将所有引用类型的变量都称为根。

CLR 开始 GC 时，首先暂停进程中的所有线程。这样可以防止线程在 CLR 检查期间访问对象并更改其状态。然后，CLR 进入 GC 的标记阶段。在这个阶段，CLR 遍历堆中的所有对象，将同步块索引字段中的一位设为 0。这表明所有对象都应删除。然后，CLR 检查所有活动根，查看它们引用了哪些对象。这正是 CLR 的 GC 称为引用跟踪 GC 的原因。如果一个根包含 null，CLR 忽略这个根并继续检查下个根。

任何根如果引用了堆上的对象，CLR 都会标记那个对象，也就是将该对象的同步块索引中的位设为 1。一个对象被标记后，CLR 会检查那个对象中的根，标记它们引用的对象。如果发现对象已经标记，就不重新检查对象的字段。这就避免了因为循环引用而产生死循环。

图 21-2 展示了一个堆，其中包含几个对象。应用程序的根直接引用对象 A、C、D 和 F。所有对象都已标记。标记对象 D 时，垃圾回收器发现这个对象含有一个引用对象 H 的字段，造成对象 H 也被标记。标记过程会持续，直至应用程序的所有根都检查完毕。

![](img/6fa065e17c4549db7260fbfaf4fd384e_466_0.png)

检查完毕后，堆中的对象要么已标记，要么未标记。已标记的对象不能被垃圾回收，因为至少有一个根在引用它。我们说这种对象是可达（reachable）的，因为应用程序代码可通过仍在引用它的变量抵达（或访问）它。未标记的对象是不可达（unreachable）的，因为应用程序中不存在使对象能被再次访问的根。

CLR 知道哪些对象可以幸存，哪些可以删除后，就进入 GC 的压缩（compact）①阶段。在这个阶段，CLR 对堆中已标记的对象进行“乾坤大挪移”，压缩所有幸存下来的对象，使它们占用连续的内存空间。这样做有许多好处。首先，所有幸存对象在内存中紧挨在一起，恢复了引用的“局部化”，减小了应用程序的工作集，从而提升了将来访问这些对象时的性能。其次，可用空间也全部是连续的，所以这个地址空间区段得到了解放，允许其他东西进驻。最后，压缩意味着托管堆解决了本机（原生）堆的空间碎片化问题。

> ① 此压缩非彼压缩，这里只是按照约定俗成的方式将 compact 翻译成“压缩”。不要以为“压缩”后内存会增多。相反，这里的“压缩”更接近于“碎片整理”。事实上，compact 正确的意思是“变得更紧凑”。但事实上，从上个世纪 80 年开始，人们就把它看成是 compress 的近义词而翻译成“压缩”，以讹传讹至今。——译注

在内存中移动了对象之后有一个问题亟待解决。引用幸存对象的根现在引用的还是对象最初在内存中的位置，而非移动之后的位置。被暂停的线程恢复执行时，将访问旧的内存位置，会造成内存损坏。这显然是无法容忍的，所以作为压缩阶段的一部分，CLR 还要从每个根减去所引用的对象在内存中偏移的字节数。这样就能保证每个根还是引用和之前一样的对象；只是对象在内存中变换了位置。

压缩好内存后，托管堆的 **NextObjPtr** 指针指向最后一个幸存对象之后的位置。下一个分配的对象将放到这个位置。图 21-3 展示了压缩阶段之后的托管堆。压缩阶段完成后，CLR 恢复应用程序的所有线程。这些线程继续访问对象，就好像 GC 没有发生过一样。

![](img/6fa065e17c4549db7260fbfaf4fd384e_467_0.png)

如果 CLR 在一次 GC 之后回收不了内存，而且进程中没有空间来分配新的 GC 区域，就说明该进程的内存已耗尽。此时，试图分配更多内存的 **new** 操作符会抛出 **OutOfMemoryException**。应用程序可捕捉该异常并从中恢复。但大多数应用程序都不会这么做；相反，异常会成为未处理异常，**Windows** 将终止进程并回收进程使用的全部内存。

作为程序员，应注意本章开头描述的两个 **bug** 不复存在了。首先，内存不可能泄漏，因为从应用程序的根②访问不了任何对象，都会在某个时间被垃圾回收。其次，不可能因为访问被释放的内存而造成内存损坏，因为现在只能引用活动对象；非活动的对象是引用不了的。

> **重要提示** 静态字段引用的对象一直存在，直到用于加载类型的 **AppDomain** 卸载为止。内存泄漏的一个常见原因就是让静态字段引用某个集合对象，然后不停歇地向集合添加数据项。静态字段使集合对象一直存活，而集合对象使所有数据项一直存活。因此，应尽量避免使用静态字段。

#### 21.1.3 垃圾回收和调试

一旦根离开作用域，它引用的对象就会变得“不可达”，GC 会回收其内存；不保证对象在方法的生存期中自始至终地存活。这会对应用程序产生有趣的影响。例如以下代码：

```csharp
using System;
using System.Threading;

public static class Program {
    public static void Main() {
        // 创建每 2000 毫秒就调用一次 TimerCallback 方法的 Timer 对象
        Timer t = new Timer(TimerCallback, null, 0, 2000);

        // 等待用户按 Enter 键
        Console.ReadLine();
    }

    private static void TimerCallback(Object o) {
        // 当调用该方法时，显示日期和时间
        Console.WriteLine("In TimerCallback: " + DateTime.Now);

        // 出于演示目的，强制执行一次垃圾回收
        GC.Collect();
    }
}
```

在命令行上，不用任何特殊编译器开关编译代码。运行可执行文件，会发现 TimerCallback 方法只被调用了一次！

> 注：这个实验在 PowerShell 中不能照搬。把脚本块强转为 `[System.Threading.TimerCallback]` 并传给 `[System.Threading.Timer]`，回调会在没有运行空间的线程池线程上执行，实测抛出 `PSInvalidOperationException`（“此线程中没有可用于运行脚本的运行空间”）并直接终止 PowerShell 进程。脚本中要用定时器，应使用 `System.Timers.Timer` 配合 `Register-ObjectEvent`（回调会排队到当前运行空间），例如：
>
> ```powershell
> $timer = [System.Timers.Timer]::new(2000)
> $timer.AutoReset = $true
> Register-ObjectEvent -InputObject $timer -EventName Elapsed -Action {
>     Write-Host "In TimerCallback: $(Get-Date)"
>     [System.GC]::Collect()
> } | Out-Null
> $timer.Start()
> [Console]::ReadLine()
> ```
>
> 另外，`$timer` 变量本身就是强根，`[System.GC]::Collect()` 不会回收它，所以“Timer 被回收后停止触发”的现象在脚本里不会出现。

观察代码，可能以为 TimerCallback 方法每隔 2000 毫秒调用一次。毕竟，代码创建了一个 Timer 对象，而且有一个变量 t 引用该对象。只要计时器对象存在，计时器就应该一直触发。但要注意，TimerCallback 方法调用 GC.Collect() 强制执行了一次垃圾回收。

回收开始时，垃圾回收器首先假定堆中的所有对象都是不可达的(垃圾)；这自然也包括 Timer 对象。然后，垃圾回收器检查应用程序的根，发现在初始化之后，Main 方法再也没有用过变量 t。既然应用程序没有任何变量引用 Timer 对象，垃圾回收自然会回收分配给它的内存；这使计时器停止触发，并解释了为什么 TimerCallback 方法只被调用了一次。

现在，假定用调试器单步调试 Main，而且在将新 Timer 对象的地址赋给 t 之后，立即发生了一次垃圾回收。然后，用调试器的“监视”窗口查看 t 引用的对象，会发生什么事情呢？因为对象已被回收，所以调试器无法显示该对象。大多数开发人员都没有料到这个结果，认为不合常理。所以，Microsoft 提出了一个解决方案。

使用 C# 编译器的 /debug 开关编译程序集时，编译器会应用 System.Diagnostics.DebuggableAttribute，并为结果程序集设置 DebuggingModes 的 DisableOptimizations 标志。运行时编译方法时，JIT 编译器看到这个标志，会将所有根的生存期延长至方法结束。在我的例子中，JIT 编译器认为 Main 的 t 变量必须存活至方法结束。所以在垃圾回收时，GC 认为 t 仍然是一个根，t 引用的 Timer 对象仍然“可达”。Timer 对象会在回收中存活，TimerCallback 方法会被反复调用，直至 Console.ReadLine 方法返回而且 Main 方法退出。

这很容易验证，只需在命令行中重新编译程序，但这一次指定 C# 编译器的 /debug 开关。运行可执行文件，会看到 TimerCallback 方法被反复调用。注意，C# 编译器的 /optimize+ 编译器开关会将 DisableOptimizations 禁止的优化重新恢复，所以实验时不要指定该开关。

JIT 编译器这样做的目的是帮助进行 JIT 调试。现在可以用正常方式启动应用程序(不用调试器），方法一经调用，JIT 编译器就会将变量的生存期延长至方法结束。以后，如果决定为进程连接一个调试器，可在先前编译好的方法中添加一个断点，并检查根变量。

你现在知道了如何构建在 **Debug** 生成中正常工作的应用程序，但它在 **Release** 生成中还是不正常。没人喜欢只有调试时才正常的应用程序，所以应该修改程序，使它在任何时候都能正常工作。

可试着像下面这样修改 **Main** 方法：

```csharp
public static void Main() {
    // 创建每 2000 毫秒就调用一次 TimerCallback 方法的 Timer 对象
    Timer t = new Timer(TimerCallback, null, 0, 2000);

    // 等待用户按 Enter 键
    Console.ReadLine();

    // 在 ReadLine 之后引用 t(会被优化掉)
    t = null;
}
```

但编译上述代码(无/debug+开关)，并运行可执行文件，会看到 **TimerCallback** 方法仍然只被调用了一次。问题在于，JIT 编译器是一个优化编译器，将局部变量或参数变量设为 null，等价于根本不引用该变量。换言之，JIT 编译器会将 t = null;整行代码删除(优化掉)。所以，程序仍然不会按期望的方式工作。下面才是 **Main** 方法的正确修改方式：

```csharp
public static void Main() {
    // 创建每 2000 毫秒就调用一次 TimerCallback 方法的 Timer 对象
    Timer t = new Timer(TimerCallback, null, 0, 2000);

    // 等待用户按 Enter 键
    Console.ReadLine();

    // 在 ReadLine 之后引用 t(在 Dispose 方法返回之前，t 会在 GC 中存活)
    t.Dispose();
}
```

现在编译代码(无/debug+编译器开关)并运行可执行文件，会发现 **TimerCallback** 方法被正确地重复调用，程序终于得到修正。现在发生的事情是，t 引用的对象必须存活，才能在它上面调用 **Dispose** 实例方法(t 中的值要作为 this 实参传给 **Dispose**)。真是讽刺，要显式要求释放计时器，它才能活到被释放的那一刻。

> **注意** 读完本节的内容后，不必担心对象被过早回收这个问题。这里讨论之所以使用 **Timer** 类，是因为它具有其他类不具有的特殊行为。**Timer** 类的特点(和问题)在于，堆中存在的一个 **Timer** 对象会造成别的事情的发生：一个线程池线程定期调用一个方法。其他任何类型都不具有这个行为。例如，内存中存在的一个 **String** 对象不会造成别的事情的发生；字符串就那么“傻傻地呆在那里”。所以，我用 **Timer** 展示根的工作原理以及对象生存期与调试器的关系，讨论的重点并不是如何保持对象的存活。所有非 **Timer** 的对象都会根据应用程序的需要而自动存活。

> 注：PowerShell 中变量的“根”由运行时的变量表、脚本块作用域和管道对象维持，不能像 C# 那样用 `t = null` 提前放弃引用；只要 `$t` 在当前作用域里仍有值，`[System.Threading.Timer]` 对象就存活。脚本里若必须显式释放，调用 `$t.Dispose()`。另外，PowerShell 的 `$null` 赋值同样只是把变量置空，是否回收仍取决于运行时。

### 21.2　代：提升性能

> 注：原文此处缺失 21.2 节开头的若干段正文（对“代”的定义及图 21-4、图 21-5），直接从图 21-6 的说明接续。补足上下文：CLR 把托管堆中的对象按存活时间分为第 0、1、2 三代，新对象总分配在第 0 代，每次垃圾回收后幸存的对象被提升到更高一代。

> 注：本节的“预算”“提升”描述的是 .NET Framework 时代 GC 的典型行为；.NET Core / PowerShell 7 仍是三代模型且沿用分代假设，但各代预算由运行时自调节，不是固定数值。脚本中可用 `[System.GC]::MaxGeneration` 查询最大代数（返回 2），用 `[System.GC]::CollectionCount(0)` 查询第 0 代已发生的回收次数。

![](img/6fa065e17c4549db7260fbfaf4fd384e_471_0.png)

图 21-6 第 0 代分配了新对象：第 1 代有垃圾产生

现在，假定分配新对象 L 会造成第 0 代超出预算，造成必须启动垃圾回收。开始垃圾回收时，垃圾回收器必须决定检查哪些代。前面说过，CLR 初始化时会为第 0 代对象选择预算。事实上，它还必须为第 1 代选择预算。

开始一次垃圾回收时，垃圾回收器还会检查第 1 代占用了多少内存。在本例中，由于第 1 代占用的内存远少于预算，所以垃圾回收器只检查第 0 代中的对象。回顾一下基于代的垃圾回收器做出的假设。第一个假设是越新的对象活得越短。因此，第 0 代包含更多垃圾的可能性很大，能回收更多的内存。由于忽略了第 1 代中的对象，所以加快了垃圾回收速度。

显然，忽略第 1 代中的对象能提升垃圾回收器的性能。但对性能有更大提振作用的是现在不必遍历托管堆中的每个对象。如果根或对象引用了老一代的某个对象，垃圾回收器就可以忽略老对象内部的所有引用，能在更短的时间内构造好可达对象图(graph of reachable object)。当然，老对象的字段也有可能引用新对象。为了确保对老对象的已更新字段进行检查，垃圾回收器利用了 JIT 编译器内部的一个机制。这个机制在对象的引用字段发生变化时，会设置一个对应的位标志。这样，垃圾回收器就知道自上一次垃圾回收以来，哪些老对象(如果有的话)已被写入。只有字段发生变化的老对象才需检查是否引用了第 0 代中的任何新对象。①

① 有人想知道更多的细节，这里便满足他们的好奇心。当 JIT 编译器生成本机(native)代码来修改对象中的一个引用字段时，本机代码会生成对一个 write barrier 方法的调用(译注：write barrier 方法是在有数据向对象写入时执行一些内存管理代码的机制)。这个 write barrier 方法检查字段被修改的那个对象是否在第 1 代或第 2 代中。如果在，write barrier 代码就在一个所谓的 card table 中设置一个 bit。card table 为堆中的每 128 字节的数据都准备好了一个 bit。GC 下一次启动时会扫描 card table，了解第 1 代和第 2 代中的哪些对象的字段自上次 GC 以来已被修改。任何被修改的对象引用了第 0 代中的一个对象，被引用的第 0 代对象就会在垃圾回收过程中“存活”。GC 之后，card table 中的所有 bit 都被重置为 0。向对象的引用字段中写入时，write barrier 代码会造成少量性能损失(对应地，向局部变量或静态字段写入便不会有这个损失)。另外，如果对象在第 1 代或第 2 代中，性能会损失得稍微多一些。

> **注意** Microsoft 的性能测试表明，对第 0 代执行一次垃圾回收，所花的时间不超过 1 毫秒。Microsoft 的目标是使垃圾回收所花的时间不超过一次普通的内存页面错误(page fault)的时间。

基于代的垃圾回收器还假设越老的对象活得越长。也就是说，第 1 代对象在应用程序中很有可能是继续可达的。如果垃圾回收器检查第 1 代中的对象，很有可能找不到多少垃圾，结果是回收不了多少内存。因此，对第 1 代进行垃圾回收很可能是浪费时间。如果真的有垃圾在第 1 代中，它将留在那里。此时的堆如图 21-7 所示。

![](img/6fa065e17c4549db7260fbfaf4fd384e_472_0.png)

图 21-7　经过两次垃圾回收之后，第 0 代的幸存者被提升至第 1 代（第 1 代的大小增加）；第 0 代又空出来了

如你所见，所有幸存下来的第 0 代对象都成了第 1 代的一部分。由于垃圾回收器没有检查第 1 代，所以对象 B 的内存并没有被回收，即使它在上一次垃圾回收时已经不可达。同样，在一次垃圾回收后，第 0 代不包含任何对象，等着分配新对象。假定应用程序继续运行，并分配对象 L 到对象 O。另外，在运行过程中，应用程序停止使用对象 G、L 和 M，使它们变得不可达。此时的托管堆如图 21-8 所示。

![](img/6fa065e17c4549db7260fbfaf4fd384e_472_1.png)

图 21-8　新对象分配到第 0 代中；第 1 代产生了更多的垃圾

假设分配对象 P 导致第 0 代超过预算，垃圾回收发生。由于第 1 代中的所有对象占据的内存仍小于预算，所以垃圾回收器再次决定只回收第 0 代，忽略第 1 代中的不可达对象（对象 B 和 G）。回收后，堆的情况如图 21-9 所示。

![](img/6fa065e17c4549db7260fbfaf4fd384e_472_2.png)

图 21-9　经过三次垃圾回收，第 0 代的幸存者被提升至第 1 代（第 1 代的大小再次增加）；第 0 代空出来了

从图 21-9 可以看到，第 1 代正在缓慢增长。假定第 1 代的增长导致它的所有对象占用了全部预算。这时，应用程序继续运行（因为垃圾回收刚刚完成），并分配对象 P 到对象 S，使第 0 代对象达到它的预算容量。这时的堆如图 21-10 所示。

![](img/6fa065e17c4549db7260fbfaf4fd384e_472_3.png)

图 21-10　新对象分配到第 0 代；第 1 代有了更多的垃圾

应用程序试图分配对象 T 时，由于第 0 代已满，所以必须开始垃圾回收。但这一次垃圾回收器发现第 1 代占用了太多内存，以至于用完了预算。由于前几次对第 0 代进行回收时，第 1 代可能已经有许多对象变得不可达（就像本例这样）。所以这次垃圾回收器决定检查第 1 代和第 0 代中的所有对象。两代都被垃圾回收后，堆的情况如图 21-11 所示。

![](img/6fa065e17c4549db7260fbfaf4fd384e_473_0.png)

图 21-11　经过 4 次垃圾回收后，第 1 代的幸存者提升至第 2 代，第 0 代的幸存者提升至第 1 代，第 0 代空出来了

和之前一样，垃圾回收后，第 0 代的幸存者被提升至第 1 代，第 1 代的幸存者被提升至第 2 代，第 0 代再次空出来了，准备好迎接新对象的到来。第 2 代中的对象经过了 2 次或更多次检查。虽然到目前为止已发生过多次垃圾回收，但只有在第 1 代超出预算时才会检查第 1 代中的对象。而在此之前，一般都已经对第 0 代进行了好几次垃圾回收。

托管堆只支持三代：第 0 代、第 1 代和第 2 代。没有第 3 代①。CLR 初始化时，会为每一代选择预算。然而，CLR 的垃圾回收器是自调节的。这意味着垃圾回收器会在执行垃圾回收的过程中了解应用程序的行为。例如，假定应用程序构造了许多对象，但每个对象用的时间都很短。在这种情况下，对第 0 代的垃圾回收会回收大量内存。事实上，第 0 代的所有对象都可能被回收。

如果垃圾回收器发现在回收 0 代后存活下来的对象很少，就可能减少第 0 代的预算。已分配空间的减少意味着垃圾回收将更频繁地发生，但垃圾回收器每次做的事情也减少了，这减小了进程的工作集。事实上，如果第 0 代中的所有对象都是垃圾，垃圾回收时就不必压缩（移动）任何内存；只需让 NextObjPtr 指针指回第 0 代的起始处即可。这样回收可真快！

> **注意**　如果应用程序的一些线程大多数时候都在栈顶闲置，垃圾回收器工作起来就尤其“得心应手”。在这种情况下，线程有事做就会被唤醒，创建一组短期存活的对象，返回，然后继续睡眠。许多应用程序都是这样建构的。例如，GUI 应用程序大多数时候都让 GUI 线程处在一个消息循环中。用户偶尔产生一些输入（触摸、鼠标或键盘事件），线程被唤醒，处理输入并回到消息条。然后，为了处理输入而创建的大多数对象都会成为垃圾。
>
> 类似地，对于服务器应用程序，线程在池里呆着，等着客户端请求进入。有客户端请求进入后，线程创建新对象，代表客户端执行工作。结果发回客户端后，线程将回到线程池，创建的所有对象现在都成了垃圾。

另一方面，如果垃圾回收器回收了第 0 代，发现还有很多对象存活，没有多少内存被回收，就会增大第 0 代的预算。现在，垃圾回收的次数将减少，但每次进行垃圾回收时，回收的内存要多得多。顺便说一句，如果没有回收到足够的内存，垃圾回收器会执行一次完整回收。如果还不足够，就抛出 OutOfMemoryException 异常。

① System.GC 类的静态 MaxGeneration 方法返回 2。

到目前为止，只是讨论了每次垃圾回收后如何动态调整第 0 代的预算。但垃圾回收器还会用类似的启发式算法调整第 1 代和第 2 代的预算。这些代被垃圾回收时，垃圾回收器会检查有多少内存被回收，以及有多少对象幸存。基于这些结果，垃圾回收器可能增大或减小这些代的预算，从而提升应用程序的总体性能。最终的结果是，垃圾回收器会根据应用程序要求的内存负载来自动优化——这非常“酷”！

以下 GCNotification 类在第 0 代或第 2 代回收时引发一个事件。可以利用该事件在发生一次回收时响铃，计算两次回收的间隔时间，计算两次回收之间分配了多少内存等。可以通过这个类方便地检测应用程序，更好地理解应用程序的内存使用情况。

```csharp
public static class GCNotification {
    private static Action<Int32> s_gcDone = null; // 事件的字段

    public static event Action<Int32> GCDone {
        add {
            // 如果之前没有登记的委托，就开始报告通知
            if (s_gcDone == null) { new GenObject(0); new GenObject(2); }
            s_gcDone += value;
        }
        remove { s_gcDone -= value; }
    }

    private sealed class GenObject {
        private Int32 m_generation;
        public GenObject(Int32 generation) { m_generation = generation; }
        ~GenObject() { // 这是 Finalize 方法
            // 如果这个对象在我们希望的(或更高的)代中，
            // 就通知委托一次 GC 刚刚完成
            if (GC.GetGeneration(this) >= m_generation) {
                Action<Int32> temp = Volatile.Read(ref s_gcDone);
                if (temp != null) temp(m_generation);
            }

            // 如果至少还有一个已登记的委托，而且 AppDomain 并非正在卸载，
            // 而且进程并非正在关闭，就继续报告通知
            if ((s_gcDone != null)
                && !AppDomain.CurrentDomain.IsFinalizingForUnload()
                && !Environment.HasShutdownStarted) {
                // 对于第 0 代，创建一个新对象；对于第 2 代，复活对象，
                // 使第 2 代在下次回收时，GC 会再次调用 Finalize
                if (m_generation == 0) new GenObject(0);
                else GC.ReRegisterForFinalize(this);
            } else { /* 放过对象，让其被回收 */ }
        }
    }
}
```

#### 21.2.1 垃圾回收触发条件

前面说过，CLR 在检测第 0 代超过预算时触发一次 GC。这是 GC 最常见的触发条件，下面列出其他条件。

- **代码显式调用 System.GC 的静态 Collect 方法**  
  代码可显式请求 CLR 执行回收。虽然 Microsoft 强烈反对这种请求，但有时情势比人强。详情参见本章稍后的 21.2.4 节“强制垃圾回收”。

- **Windows 报告低内存情况**：CLR 内部使用 Win32 函数 **CreateMemoryResourceNotification** 和 **QueryMemoryResourceNotification** 监视系统的总体内存使用情况。如果 Windows 报告低内存，CLR 将强制垃圾回收以释放死对象，减小进程工作集。
- **CLR 正在卸载 AppDomain**：一个 AppDomain 卸载时，CLR 认为其中一切都不是根，所以执行涵盖所有代的垃圾回收。AppDomain 将在第二十二章讨论。
- **CLR 正在关闭**：CLR 在进程正常终止时关闭。关闭期间，CLR 认为进程中一切都不是根。对象有机会进行资源清理，但 CLR 不会试图压缩或释放内存。整个进程都要终止了，Windows 将回收进程的全部内存。

#### 21.2.2 大对象

还有另一个性能提升举措值得注意。CLR 将对象分为大对象和小对象。本章到目前为止说的都是小对象。目前认为 85000 字节或更大的对象是大对象。CLR 以不同方式对待大小对象。

- 大对象不是在小对象的地址空间分配，而是在进程地址空间的其他地方分配。
- 目前版本的 GC 不压缩大对象，因为在内存中移动它们代价过高。但这可能在进程中的大对象之间造成地址空间的碎片化，以至于抛出 **OutOfMemoryException**。CLR 将来的版本可能压缩大对象。
- 大对象总是第 2 代，绝不可能是第 0 代或第 1 代。所以只能为需要长时间存活的资源创建大对象。分配短时间存活的大对象会导致第 2 代被更频繁地回收，会损害性能。大对象一般是大字符串（比如 XML 或 JSON）或者用于 I/O 操作的字节数组（比如从文件或网络将字节读入缓冲区以便处理）。

可在很大程度上视大对象若无物。可忽略它们的存在。仅在出现解释不了的情况时（比如地址空间碎片化）才对它们进行特殊处理。

> 注：85000 字节只是当前实现的阈值，不是规范常数。需要压缩大对象堆时，可在 PowerShell 中设置 `[System.Runtime.GCSettings]::LargeObjectHeapCompactionMode = [System.Runtime.GCLargeObjectHeapCompactionMode]::CompactOnce`，它只对下一次完整 GC 生效（实测 PowerShell 7 支持）。脚本里应尽量避免反复拼接超长字符串或反复创建接近该阈值的大 `byte[]`。

#### 21.2.3 垃圾回收模式

CLR 启动时会选择一个 GC 模式，进程终止前该模式不会改变。有两个基本 GC 模式。

① 与之相反的是从外部终止，比如通过任务管理器。

② 未来 CLR 可能更改大对象的标准。85000 不是常数。

- **工作站**：该模式针对客户端应用程序优化 GC。GC 造成的延时很低，应用程序线程挂起时间很短，避免使用户感到焦虑。在该模式中，GC 假定机器上运行的其他应用程序都不会消耗太多的 CPU 资源。
- **服务器**：该模式针对服务器端应用程序优化 GC。被优化的主要是吞吐量和资源利用。GC 假定机器上没有运行其他应用程序（无论客户端还是服务器应用程序），并假定机器的所有 CPU 都可用来辅助完成 GC。该模式造成托管堆被拆分成几个区域（section），每个 CPU 一个。开始垃圾回收时，垃圾回收器在每个 CPU 上都运行一个特殊线程；每个线程都和其他线程并发回收它自己的区域。对于工作者线程（worker thread）行为一致的服务器应用程序，并发回收能很好地进行。这个功能要求应用程序在多 CPU 计算机上运行，使线程能真正地同时工作，从而获得性能的提升。

应用程序默认以“工作站”GC 模式运行。寄宿①了 CLR 的服务器应用程序（比如 ASP.NET 或 Microsoft SQL Server）可请求 CLR 加载“服务器”GC。但如果服务器应用程序在单处理器计算机上运行，CLR 将总是使用“工作站”GC 模式。

> 注：脚本里可直接查询当前模式：`[System.Runtime.GCSettings]::IsServerGC`。选择模式要在进程启动前决定，PowerShell 进程启动后无法切换；在工作站（客户端）GC 下，脚本里 `[GC]::Collect()` 的停顿通常比服务器 GC 短。若要给 PowerShell 进程启用服务器 GC，可在 .NET Core / PowerShell 7 使用的 `runtimeconfig.json` 中设置 `"System.GC.Server": true`；下文提到的 `gcServer` / `gcConcurrent` 元素属于 .NET Framework 的 `app.config`，对 PowerShell 7 不生效（PowerShell 5.1 随 .NET Framework 运行时，才读取这些元素）。

① hosts（动词）。注意，本书将 host 的动词形式统一翻译成“寄宿”，名词形式翻译成“宿主”。但在作动词用时，理解成“容纳”更佳。——译注

独立应用程序可创建一个配置文件②告诉 CLR 使用服务器回收器。配置文件要为应用程序添加一个 **gcServer** 元素。下面是一个示例配置文件：

② 第二章“生成、打包、部署和管理应用程序及类型”和第三章“共享程序集和强命名程序集”都有讲到应用程序配置文件的问题。

```xml
<configuration>
    <runtime>
        <gcServer enabled="true"/>
    </runtime>
</configuration>
```

应用程序运行时，可查询 **GCSettings** 类的只读 **Boolean** 属性 **IsServerGC** 来询问 CLR 它是否正在“服务器”GC 模式中运行：

```csharp
using System;
using System.Runtime; // 这个命名空间包含了 GCSettings

public static class Program {
    public static void Main() {
        Console.WriteLine("Application is running with server GC=" +
                          GCSettings.IsServerGC);
    }
}
```

除了这两种主要模式，GC 还支持两种子模式：并发（默认）或非并发。在并发方式中，垃圾回收器有一个额外的后台线程，它能在应用程序运行时并发标记对象。一个线程因为分配对象造成第 0 代超出预算时，GC 首先挂起所有线程，再判断要回收哪些代。如果要回收第 0 代或第 1 代，那么一切如常进行。但是，如果要回收第 2 代，就会增大第 0 代的大小（超过其预算），以便在第 0 代中分配新对象。然后，应用程序的线程恢复运行。

应用程序线程运行时，垃圾回收器运行一个普通优先级的后台线程来查找不可达对象。找到之后，垃圾回收器再次挂起所有线程，判断是否要压缩（移动）内存。如决定压缩，内存会被压缩，根引用会被修正，应用程序线程恢复运行。这一次垃圾回收花费的时间比平常少，因为不可达对象集合已构造好了。但垃圾回收器也可能决定不压缩内存：事实上，垃圾回收器更倾向于选择不压缩。可用内存多，垃圾回收器便不会压缩堆；这有利于增强性能，但会增大应用程序的工作集。使用并发垃圾回收器，应用程序消耗的内存通常比使用非并发垃圾回收器多。

为了告诉 CLR 不要使用并发回收器，可创建包含 **gcConcurrent** 元素的应用程序配置文件。下面是配置文件的一个例子：

```xml
<configuration>
    <runtime>
        <gcConcurrent enabled="false"/>
    </runtime>
</configuration>
```

GC 模式是针对进程配置的，进程运行期间不能更改。但是，你的应用程序可以使用 **GCSettings** 类的 **GCLatencyMode** 属性对垃圾回收进行某种程度的控制。这个读/写属性能设为 **GCLatencyMode** 枚举类型中的任何值，表 21-1 对此进行了总结。

表 21-1　GCLatencyMode 枚举类型定义的符号

| 符号名称 | 说明 |
|---|---|
| **Batch**（“服务器”GC 模式的默认值） | 关闭并发 GC |
| **Interactive**（“工作站”GC 模式的默认值） | 打开并发 GC |
| **LowLatency** | 在短期的、时间敏感的操作中（比如动画绘制）使用这个延迟模式。这些操作不适合对第 2 代进行回收 |
| **SustainedLowLatency** | 使用这个延迟模式，应用程序的大多数操作都不会发生长的 GC 暂停。只要有足够内存，它将禁止所有会造成阻塞的第 2 代回收动作。事实上，这种应用程序（例如需要迅速响应的股票软件）的用户应考虑安装更多的 RAM 来防止发生长的 GC 暂停 |

**LowLatency** 模式有必要多说几句。一般用它执行一次短期的、时间敏感的操作，再将模式设回普通的 **Batch** 或 **Interactive**。在模式设为 **LowLatency** 期间，垃圾回收器会全力避免任何第 2 代回收，因为那样花费的时间较多。当然，调用 **GC.Collect()** 仍会回收第 2 代。此外，如果 Windows 告诉 CLR 系统内存低，GC 也会回收第 2 代。（参见本章前面的 21.2.1 节“垃圾回收触发条件”。）

在 **LowLatency** 模式中，应用程序抛出 **OutOfMemoryException** 的机率会大一些。所以，处于该模式的时间应尽量短，避免分配太多对象，避免分配大对象，并用一个约束执行区域(CER)①将模式设回 **Batch** 或 **Interactive**。另外注意，延迟模式是进程级的设置，而可能有多个线程并发运行。在一个线程使用该设置期间，其他线程可能试图更改这个设置。所以，假如有多个线程都要操作这个设置，可考虑更新某种计数器(更新计数器要通过 **Interlocked** 的方法来进行)。以下代码展示了如何正确地使用 **LowLatency** 模式：

```csharp
private static void LowLatencyDemo() {
    GCLatencyMode oldMode = GCSettings.LatencyMode;
    System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions();
    try {
        GCSettings.LatencyMode = GCLatencyMode.LowLatency;
        // 在这里运行你的代码...
    }
    finally {
        GCSettings.LatencyMode = oldMode;
    }
}
```

#### 21.2.4 强制垃圾回收

**System.GC** 类型允许应用程序对垃圾回收器进行一些直接控制。例如，可读取 **GC.MaxGeneration** 属性来查询托管堆支持的最大代数；该属性总是返回 2。

还可调用 **GC** 类的 **Collect** 方法强制垃圾回收。可向方法传递一个代表最多回收几代的整数、一个 **GCCollectionMode** 以及指定阻塞(非并发)或后台(并发)回收的一个 **Boolean** 值。以下是最复杂的 **Collect** 重载的签名：

```csharp
void Collect(Int32 generation, GCCollectionMode mode, Boolean blocking);
```

> 注：PowerShell 可直接调用这些静态方法，例如 `[System.GC]::MaxGeneration` 返回 2，`[System.GC]::Collect()` 强制执行一次回收，`[System.GC]::Collect(2, [System.GCCollectionMode]::Optimized, $true)` 对应上面的三参数重载。注意不要用 `Collect` 来“清理变量”，它作用于整个进程，脚本无法据此提前释放某个对象。

表 21-2　GCCollectionMode 枚举类型定义的符号

| 符号名称 | 说明 |
|---|---|
| **Default** | 等同于不传递任何符号名称。目前还等同于传递 **Forced**，但 CLR 未来的版本可能对此进行修改 |
| **Forced** | 强制回收指定的代(以及低于它的所有代) |
| **Optimized** | 只有在能释放大量内存或者能减少碎片化的前提下，才执行回收。如果垃圾回收没有什么效率，当前调用就没有任何效果 |

大多时候都要避免调用任何 **Collect** 方法；最好让垃圾回收器自行斟酌执行，让它根据应用程序的行为调整各个代的预算。但如果写一个 CUI(console user interface，控制台用户界面)或 GUI(graphical user interface，图形用户界面)应用程序，应用程序代码将拥有进程和那个进程中的 CLR。对于这种应用程序，你可能希望建议垃圾回收的时间；为此，请将 GCCollectionMode 设为 Optimized 并调用 Collect。Default 和 Forced 模式一般用于调试、测试和查找内存泄漏。

例如，假如刚才发生了某个非重复性的事件，并导致大量旧对象死亡，就可考虑手动调用一次 Collect 方法。由于是非重复性事件，垃圾回收器基于历史的预测可能变得不准确。所以，这时调用 Collect 方法是合适的。例如，在应用程序初始化完成之后或者在用户保存了一个数据文件之后，应用程序可强制执行一次对所有代的垃圾回收。由于调用 Collect 会导致代的预算发生调整，所以调用它不是为了改善应用程序的响应时间，而是为了减小进程工作集。

对于某些应用程序(尤其是喜欢在内存中容纳大量对象的服务器应用程序)，如果对包括第 2 代在内的对象执行完全的垃圾回收，花费的时间可能过长。如果一次回收要花很长时间才能完成，客户端请求可能超时。为了满足这种应用程序的需求，GC 类提供了一个 RegisterForFullGCNotification 方法。利用这个方法和一些额外的辅助方法 (WaitForFullGCApproach，WaitForFullGCComplete 和 CancelFullGCNotification)，应用程序会在垃圾回收器将要执行完全回收时收到通知。然后，应用程序可调用 GC.Collect，在更恰当的时间强制回收。也可与另一个服务器通信，对客户端请求进行更好的负载平衡。欲知详情，请在文档中查找这些方法和“垃圾回收通知”主题。注意，WaitForFullGCApproach 和 WaitForFullGCComplete 方法必须成对调用，CLR 内部把它们当作一对儿进行处理。

#### 21.2.5 监视应用程序的内存使用

可在进程中调用几个方法来监视垃圾回收器。具体地说，GC 类提供了以下静态方法，可调用它们查看某一代发生了多少次垃圾回收，或者托管堆中的对象当前使用了多少内存。

```csharp
Int32 CollectionCount(Int32 generation);
Int64 GetTotalMemory(Boolean forceFullCollection);
```

> 注：PowerShell 对应写法为 `[System.GC]::CollectionCount(0)` 和 `[System.GC]::GetTotalMemory($true)`（单位是字节）。`GetTotalMemory($true)` 会先强制一次完整回收再统计，代价较高，只宜用于测量；`[System.GC]::GetGeneration($obj)` 则可查询某个对象当前已被提升到第几代。

为了评估(profile)特定代码块的性能，我经常在代码块前后写代码调用这些方法，并计算差异。这使我能很好地把握代码块对进程工作集的影响，并了解执行代码块时发生了多少次垃圾回收。数字太大，就知道应该花更多的时间调整代码块中的算法。

还可以了解单独的 AppDomain(而非整个进程)使用了多少内存。欲知这方面的详情，请参见 22.4 节“监视 AppDomain”。

安装.NET Framework 时会自动安装一组性能计数器，为 CLR 的操作提供大量实时统计数据。这些统计数据可通过 Windows 自带的 PerfMon.exe 工具或者“系统监视器” ActiveX 控件来查看。访问“系统监视器”最简单的方式就是运行 PerfMon.exe，单击“+”工具栏按钮，随后会显示“添加计数器”对话框，如图 21-12 所示。

为了监视 CLR 的垃圾回收器，请选择“.NET CLR Memory”性能对象。然后，从下方的实例列表框中选择一个具体的应用程序。最后，选定想监视的计数器集合，单击“添加”，再单击“确定”。随后，“性能监视器”会图示实时统计数据。要知道特定计数器的含义，请选定该计数器，然后勾选“显示描述”。

还有一个很出色的工具可分析内存和应用程序的性能，它的名字是 **PerfView**。该工具能收集“Windows 事件跟踪”（Event Tracing for Windows，ETW）日志并处理它们。获取该工具最好的办法是网上搜索 PerfView。最后还应该考虑一下 SOS Debugging Extension（SOS.dll），它对于内存问题和其他 CLR 问题的调试颇有帮助。对于内存有关的行动，SOS Debugging Extension 允许检查进程中为托管堆分配了多少内存，显示在终结队列中登记终结的所有对象，显示每个 AppDomain 或整个进程的 GCHandle 表中的记录项，并显示是什么根保持对象在堆中存活。

![](img/6fa065e17c4549db7260fbfaf4fd384e_480_0.png)

图 21-12　PerfMon.exe 显示了 .NET CLR Memory 计数器

### 21.3 使用需要特殊清理的类型

你现在基本了解了垃圾回收和托管堆的情况，包括垃圾回收器如何回收对象的内存。幸好，大多数类型有内存就能正常工作。但有的类型除了内存还需要本机资源。

例如，**System.IO.FileStream** 类型需要打开一个文件（本机资源）并保存文件的句柄。然后，类型的 **Read** 和 **Write** 方法用句柄操作文件。类似地，**System.Threading.Mutex** 类型要打开一个 Windows 互斥体内核对象（本机资源）并保存其句柄，并在调用 **Mutex** 的方法时使用该句柄。

包含本机资源的类型被 GC 时，GC 会回收对象在托管堆中使用的内存。但这样会造成本机资源（GC 对它一无所知）的泄漏，这当然是不允许的。所以，CLR 提供了称为**终结**（finalization）的机制，允许对象在被判定为垃圾之后，但在对象内存被回收之前执行一些代码。任何包装了本机资源（文件、网络连接、套接字、互斥体）的类型都支持终结。CLR 判定一个对象不可达时，对象将终结它自己，释放它包装的本机资源。之后，GC 会从托管堆回收对象。

终极基类 **System.Object** 定义了受保护的虚方法 **Finalize**。垃圾回收器判定对象是垃圾后，会调用对象的 **Finalize** 方法（如果重写）。Microsoft 的 C# 团队认为 **Finalize** 在编程语言中需要特殊语法(类似于 C#要求用特殊语法定义构造器)。因此，C#要求在类名前添加~符号来定义 **Finalize** 方法，如下例所示：

> 注：PowerShell 没有析构器/终结器语法，脚本无法重写 `Finalize`。要包装本机资源，只能在 `Add-Type` 中用 C# 声明类型（派生 `System.Runtime.InteropServices.SafeHandle` 或实现 `IDisposable`），或者直接使用 FCL 已有的类型（`FileStream`、`SafeWaitHandle` 等）。脚本能做的是显式调用它们的 `Dispose()`，而不是定义终结逻辑。

```csharp
internal sealed class SomeType {
    // 这是一个 Finalize 方法
    ~SomeType() {
        // 这里的代码会进入 Finalize 方法
    }
}
```

编译上述代码，用 ILDasm.exe 检查得到的程序集，会发现 C#编译器实际是在模块的元数据中生成了名为 **Finalize** 的 **protected override** 方法。查看 **Finalize** 的 IL，会发现方法主体的代码被放到一个 **try** 块中，在 **finally** 块中放入了一个 **base.Finalize** 调用。

> **重要提示**  如果熟悉 C++，会发现 C# **Finalize** 方法的特殊语法非常类似于 C++析构器。事实上，在 C#编程语言规范的早期版本中，真的是将该方法称为析构器。但 **Finalize** 方法的工作方式和 C++析构器完全不同，这会使从一种语言迁移到另一种语言的开发人员产生混淆。
>
> 问题在于，这些开发人员可能错误地以为使用 C#析构器语法意味着类型的实例会被确定性析构，就像在 C++中那样。但 CLR 不支持确定性析构，而作为面向 CLR 的语言，C#也无法提供这种机制。

被视为垃圾的对象在垃圾回收完毕后才调用 **Finalize** 方法，所以这些对象的内存不是马上被回收的，因为 **Finalize** 方法可能要执行访问字段的代码。可终结对象在回收时必须存活，造成它被提升到另一代，使对象活得比正常时间长。这增大了内存耗用，所以应尽可能避免终结。更糟的是，可终结对象被提升时，其字段引用的所有对象也会被提升，因为它们也必须继续存活。所以，要尽量避免为引用类型的字段定义可终结对象。

另外要注意，**Finalize** 方法的执行时间是控制不了的。应用程序请求更多内存时才可能发生 GC，而只有 GC 完成后才运行 **Finalize**。另外，CLR 不保证多个 **Finalize** 方法的调用顺序。所以，在 **Finalize** 方法中不要访问定义了 **Finalize** 方法的其他类型的对象；那些对象可能已经终结了。但可以安全地访问值类型的实例，或者访问没有定义 **Finalize** 方法的引用类型的对象。调用静态方法也要当心，这些方法可能在内部访问已终结的对象，导致静态方法的行为变得无法预测。

CLR 用一个特殊的、高优先级的专用线程调用 **Finalize** 方法来避免死锁①。如果 **Finalize** 方法阻塞(例如进入死循环，或等待一个永远不发出信号的对象)，该特殊线程就调用不了任何更多的 **Finalize** 方法。这是非常坏的情况，因为应用程序永远回收不了可终结对象占用的内存——只要应用程序运行就会一直泄漏内存。如果 **Finalize** 方法抛出未处理的异常，则进程终止，没办法捕捉该异常。

① CLR 将来的版本可能用多个终结器线程提升性能。



综上所述，**Finalize** 方法问题较多，使用须谨慎。记住它们是为释放本机资源而设计的。强烈建议不要重写 **Object** 的 **Finalize** 方法。相反，使用 Microsoft 在 FCL 中提供的辅助类。这些辅助类重写了 **Finalize** 方法并添加了一些特殊的 CLR “魔法”（以后会慢慢讲述）。你从这些辅助类派生出自己的类，从而继承 CLR 的“魔法”。

创建封装了本机资源的托管类型时，应该先从 **System.Runtime.InteropServices.SafeHandle** 这个特殊基类派生出一个类。该类的形式如下（我在方法中添加了注释，指明它们做的事情）：

```csharp
public abstract class SafeHandle : CriticalFinalizerObject, IDisposable {
    // 这是本机资源的句柄
    protected IntPtr handle;

    protected SafeHandle(IntPtr invalidHandleValue, Boolean ownsHandle) {
        this.handle = invalidHandleValue;
        // 如果 ownsHandle 为 true，那么这个从 SafeHandle 派生的对象被回收时，
        // 本机资源会被关闭
    }

    protected void SetHandle(IntPtr handle) {
        this.handle = handle;
    }

    // 可调用 Dispose 显式释放资源
    // 这是 IDisposable 接口的 Dispose 方法
    public void Dispose() { Dispose(true); }

    // 默认的 Dispose 实现 (如下所示) 正是我们希望的。强烈建议不要重写这个方法
    protected virtual void Dispose(Boolean disposing) {
        // 这个默认实现会忽略 disposing 参数；
        // 如果资源已经释放，那么返回；
        // 如果 ownsHandle 为 false，那么返回；
        // 设置一个标志来指明该资源已经释放；
        // 调用虚方法 ReleaseHandle；
        // 调用 GC.SuppressFinalize(this) 方法来阻止调用 Finalize 方法；
        // 如果 ReleaseHandle 返回 true，那么返回；
        // 如果走到这一步，就激活 releaseHandleFailed 托管调试助手(MDA)。
    }

    // 默认的 Finalize 实现 (如下所示) 正是我们希望的。强烈建议不要重写这个方法
    ~SafeHandle() { Dispose(false); }

    // 派生类要重写这个方法以实现释放资源的代码
    protected abstract Boolean ReleaseHandle();

    public void SetHandleAsInvalid() {
        // 设置标志来指出这个资源已经释放
        // 调用 GC.SuppressFinalize(this) 方法来阻止调用 Finalize 方法
    }

    public Boolean IsClosed {
        get {
            // 返回指出资源是否释放的一个标志
        }
    }

    public abstract Boolean IsInvalid {
        // 派生类要重写这个属性
        // 如果句柄的值不代表资源 (通常意味着句柄为 0 或 -1)，实现应返回 true
        get;
    }

    // 以下三个方法涉及安全性和引用计数，本节最后会讨论它们
    public void   DangerousAddRef(ref Boolean success) {...}
    public IntPtr DangerousGetHandle() {...}
    public void   DangerousRelease() {...}
}
```

**SafeHandle** 类有两点需要注意。其一，它派生自 **CriticalFinalizerObject**；后者在 **System.Runtime.ConstrainedExecution** 命名空间定义。CLR 以特殊方式对待这个类及其派生类。具体地说，CLR 赋予这个类以下三个很酷的功能。

- 首次构造任何 **CriticalFinalizerObject** 派生类型的对象时，CLR 立即对继承层次结构中的所有 **Finalize** 方法进行 JIT 编译。构造对象时就编译这些方法，可确保当对象被确定为垃圾之后，本机资源肯定会得以释放。不对 **Finalize** 方法进行提前编译，那么也许能分配并使用本机资源，但无法保证释放。内存紧张时，CLR 可能找不到足够的内存来编译 **Finalize** 方法，这会阻止 **Finalize** 方法的执行，造成本机资源泄漏。另外，如果 **Finalize** 方法中的代码引用了另一个程序集中的类型，但 CLR 定位该程序集失败，那么资源将得不到释放。
- CLR 是在调用了非 **CriticalFinalizerObject** 派生类型的 **Finalize** 方法之后，才调用 **CriticalFinalizerObject** 派生类型的 **Finalize** 方法。这样，托管资源类就可以在它们的 **Finalize** 方法中成功地访问 **CriticalFinalizerObject** 派生类型的对象。例如，**FileStream** 类的 **Finalize** 方法可以放心地将数据从内存缓冲区 flush①到磁盘，它知道此时磁盘文件还没有关闭。
- 如果 **AppDomain** 被一个宿主应用程序(例如 **Microsoft SQL Server** 或者 **Microsoft ASP.NET**)强行中断，CLR 将调用 **CriticalFinalizerObject** 派生类型的 **Finalize** 方法。宿主应用程序不再信任它内部运行的托管代码时，也利用这个功能确保本机资源得以释放。

其二，**SafeHandle** 是抽象类，必须有另一个类从该类派生并重写受保护的构造器、抽象方法 **ReleaseHandle** 以及抽象属性 **IsInvalid** 的 get 访问器方法。

多数本机资源都用句柄(32 位系统是 32 位值，64 位系统是 64 位值)进行操作。所以 **SafeHandle** 类定义了受保护 **IntPtr** 字段 **handle**。在 Windows 中，大多数值为 0 或 -1 的句柄都是无效的。**Microsoft.Win32.SafeHandles** 命名空间包含 **SafeHandleZeroOrMinusOneIsInvalid** 辅助类，如下所示：

```csharp
public abstract class SafeHandleZeroOrMinusOneIsInvalid : SafeHandle {
    protected SafeHandleZeroOrMinusOneIsInvalid(Boolean ownsHandle)
        : base(IntPtr.Zero, ownsHandle) {
    }

    public override Boolean IsInvalid {
```

> 注：原文此处的代码块被截断，`IsInvalid` 的属性体与类的结尾缺失。按 FCL 中的实现，该属性为 `get { return handle == IntPtr.Zero || handle == new IntPtr(-1); }`，随后以 `}` 结束类。紧跟其后的 `SomeType` 示例也缺少引导段落，其内容是对比 P/Invoke 原型返回 `IntPtr` 与返回 `SafeWaitHandle` 两种写法的健壮性。

```csharp
internal static class SomeType {
    [DllImport("Kernel32", CharSet=CharSet.Unicode, EntryPoint="CreateEvent")]
    // 这个原型不健壮
    private static extern IntPtr CreateEventBad(
        IntPtr pSecurityAttributes, Boolean manualReset,
        Boolean initialState, String name);

    // 这个原型是健壮的
    [DllImport("Kernel32", CharSet=CharSet.Unicode, EntryPoint="CreateEvent")]
    private static extern SafeWaitHandle CreateEventGood(
        IntPtr pSecurityAttributes, Boolean manualReset,
        Boolean initialState, String name);

    public static void SomeMethod() {
        IntPtr          handle = CreateEventBad(IntPtr.Zero, false, false, null);
        SafeWaitHandle  swh    = CreateEventGood(IntPtr.Zero, false, false, null);
    }
}
```

在上述代码中，**CreateEventBad** 方法的原型是返回一个 **IntPtr**，这会将句柄返回给托管代码。但以这种方式与本机代码交互是不健壮的。调用 **CreateEventBad**（该方法创建本机事件资源）之后，在将句柄赋给 **handle** 变量之前，可能抛出一个 **ThreadAbortException**。虽然这很少发生，但一旦发生，托管代码将造成本机资源的泄漏。这时只有终止整个进程才能关闭事件。

**SafeHandle** 类修正了这个潜在的资源泄漏问题。注意，**CreateEventGood** 方法的原型是返回一个 **SafeWaitHandle**（而非 **IntPtr**）。调用 **CreateEventGood** 方法时，CLR 会调用 Win32 **CreateEvent** 函数。**CreateEvent** 函数返回至托管代码时，CLR 知道 **SafeWaitHandle** 是从 **SafeHandle** 派生的，所以会自动在托管堆构造 **SafeWaitHandle** 的实例，向其传递从 **CreateEvent** 返回的句柄值。新 **SafeWaitHandle** 对象的构造以及句柄的赋值现在是在本机代码中发生的，不可能被一个 **ThreadAbortException** 打断。托管代码现在不可能泄漏这个本机资源。**SafeWaitHandle** 对象最终会被垃圾回收，其 **Finalize** 方法会被调用，确保资源得以释放。

**SafeHandle** 派生类最后一个值得注意的功能是防止有人利用潜在的安全漏洞。问题起因是一个线程可能试图使用一个本机资源，而另一个线程试图释放该资源。这可能造成句柄循环使用漏洞。**SafeHandle** 类防范这个安全隐患的办法是使用引用计数。**SafeHandle** 类内部定义了私有字段来维护一个计数器。一旦某个 **SafeHandle** 派生对象被设为有效句柄，计数器就被设为 1。每次将 **SafeHandle** 派生对象作为实参传给一个本机方法（非托管方法），CLR 就会自动递增计数器。类似地，当本机方法返回到托管代码时，CLR 自动递减计数器。例如，Win32 **SetEvent** 函数的原型如下：

```csharp
[DllImport("Kernel32", ExactSpelling=true)]
private static extern Boolean SetEvent(SafeWaitHandle swh);
```

现在，调用这个方法并传递一个 **SafeWaitHandle** 对象引用，CLR 会在调用前递增计数器，调用后递减计数器。当然，对计数器的操作是以线程安全的方式进行的。那么安全性如何得以保障？当另一个线程试图释放 **SafeHandle** 对象包装的本机资源时，CLR 知道它实际上不能释放资源，因为该资源正在由一个本机（非托管）函数使用。本机函数返回后，计数器递减为 0，资源才会得以释放。

如果编写或调用代码将句柄作为一个 **IntPtr** 来操作，可以从 **SafeHandle** 对象中访问它，但就要显式操作引用计数器。这是通过 **SafeHandle** 的 **DangerousAddRef** 和 **DangerousRelease** 方法来完成的。另外，可通过 **DangerousGetHandle** 方法访问原始句柄。

**System.Runtime.InteropServices** 命名空间还定义了一个 **CriticalHandle** 类。该类除了不提供引用计数器功能，其他方面与 **SafeHandle** 类相同。**CriticalHandle** 类及其派生类通过牺牲安全性来换取更好的性能（因为不用操作计数器）。和 **SafeHandle** 相似，**CriticalHandle** 类也有自己的几个派生类型，其中包括 **CriticalHandleMinusOneIsInvalid** 和 **CriticalHandleZeroOrMinusOneIsInvalid**。由于 Microsoft 倾向于建立更安全而不是更快的系统，所以类库中没有提供从这两个类派生的类型。自己写程序时，建议只有在必须追求性能的时候才使用派生自 **CriticalHandle** 的类型。如果降低安全性不会有什么严重的后果，就选择从 **CriticalHandle** 派生的一个类型。

### 21.3.1 使用包装了本机资源的类型

你现在知道了如何定义包装了本机资源的 **SafeHandle** 派生类，接着说说如何使用它。以常用的 **System.IO.FileStream** 类为例，可利用它打开一个文件，从文件中读取字节，向文件写入字节，然后关闭文件。**FileStream** 对象在构造时会调用 Win32 **CreateFile** 函数，函数返回的句柄保存到 **SafeFileHandle** 对象中，然后通过 **FileStream** 对象的一个私有字段来维护对该对象的引用。**FileStream** 类还提供了几个额外的属性（例如 **Length，Position，CanRead**）和方法（例如 **Read，Write，Flush**）。

假定要写代码来创建一个临时文件，向其中写入一些字节，然后删除文件。开始可能会像下面这样写代码：

```powershell
# 等效 PowerShell 写法
# 创建要写入临时文件的字节
[byte[]]$bytesToWrite = 1, 2, 3, 4, 5

# 创建临时文件
$fs = [System.IO.FileStream]::new('Temp.dat', [System.IO.FileMode]::Create)

# 将字节写入临时文件
$fs.Write($bytesToWrite, 0, $bytesToWrite.Length)

# 删除临时文件（文件仍打开，Windows 上抛 IOException）
Remove-Item Temp.dat
```

遗憾的是，生成并运行上述代码，它也许能工作，但大多数时候都不能。问题在于删除操作要求 Windows 删除一个仍然打开的文件（原书用 File 的静态 Delete 方法，上例改用 Remove-Item）。所以删除会抛出 System.IO.IOException 异常，并显示以下字符串消息：**文件"Temp.dat"正由另一进程使用，因此该进程无法访问此文件。**

但某些情况下，文件可能“误打误撞”地被删除！如果另一线程不知怎么造成了一次垃圾回收，而且这次垃圾回收刚好在调用 Write 之后、调用 Delete 之前发生，那么 FileStream 的 SafeFileHandle 字段的 Finalize 方法就会被调用，这会关闭文件，随后 Delete 操作也就可以正常运行。但发生这种情况的概率很小，上述代码无法运行的可能性在 99%以上。

> 注：PowerShell 版同样会失败，`Remove-Item Temp.dat` 会报“文件正由另一进程使用”。区别在于 PowerShell 默认把这类错误当作非终止错误：显示后继续执行，不会像 C# 那样中断脚本；若要让脚本能 `try/catch` 捕获，需写成 `Remove-Item Temp.dat -ErrorAction Stop`。

类如果想允许使用者控制类所包装的本机资源的生存期，就必须实现如下所示的 IDisposable 接口。

```csharp
public interface IDisposable {
    void Dispose();
}
```

> **重要提示** 如果类定义的一个字段的类型实现了 dispose 模式，那么类本身也应实现 dispose 模式。Dispose 方法应 dispose 字段引用的对象。这就允许类的使用者在类上调用 Dispose 来释放对象自身使用的资源。

幸好，FileStream 类实现了 IDisposable 接口。在实现中，会在 FileStream 对象的私有 SafeFileHandle 字段上调用 Dispose。现在就能修改代码来显式关闭文件，而不是等着未来某个时候 GC 的发生。下面是修改后的源代码。

```csharp
using System;
using System.IO;

public static class Program {
    public static void Main() {
        // 创建要写入临时文件的字节
        Byte[] bytesToWrite = new Byte[] { 1, 2, 3, 4, 5 };

        // 创建临时文件
        FileStream fs = new FileStream("Temp.dat", FileMode.Create);

        // 将字节写入临时文件
        fs.Write(bytesToWrite, 0, bytesToWrite.Length);
```

> 注：原文此处的代码块被截断，`fs.Dispose()`、`File.Delete("Temp.dat")` 及 `Main` 方法的结尾缺失。要点是：先调用 `Dispose()` 显式关闭文件，再调用 `Delete` 才能成功。其后两个脚注说明 dispose 模式的译名问题。

- ① 实现了 IDisposable 接口，就实现了 dispose 模式。——译注
- ② 文档将 disposal 和 dispose 翻译成“释放”。这里解释一下为什么不赞成这个翻译。在英语中，这个词的意思是“摆脱”或“除去”（get rid of）一个东西，尤其是在这个东西很难除去的情况下。之所以认为“释放”不恰当，除了和 release 一词冲突，还因为 dispose 强调了“清理”和“处置”，而且在完成（对象中包装的）资源的清理之后，对象占用的内存还暂时不会释放。所以，“dispose 一个对象”真正的意思是：清理或处置对象中包装的资源（比如它的字段引用的对象），然后等着在一次垃圾回收之后回收该对象占用的托管堆内存（此时才释放）。为避免误解，本书保留了 dispose 和 disposal 的原文。——译注

> 注：PowerShell 没有 C# 的 `using` 语句（PowerShell 7 的 `using` 关键字仅用于导入命名空间/模块，与资源释放无关）。释放实现 `IDisposable` 的对象应写 `try { ... } finally { $fs.Dispose() }`。PowerShell 脚本的局部变量在作用域结束时即失去引用，但像 `FileStream` 这种包装了文件句柄的对象不会因此及时关闭文件，必须显式调用 `Dispose()`。



> 注：原文在此处缺了小节标题和若干段过渡正文（说明本机资源占用与托管内存不成比例、GC 因此低估实际内存压力的问题）。以下讨论的 `GC.AddMemoryPressure`/`GC.RemoveMemoryPressure` 和 `HandleCollector` 就是为这种情形提供的辅助 API。

例如，一个进程可以在执行垃圾回收之前分配数百个位图（它们用的托管内存太少了）。但如果进程操作许多位图，进程的内存消耗将以一个恐怖的速度增长。为了修正这个问题，GC 类提供了以下两个静态方法：

```csharp
public static void AddMemoryPressure(Int64 bytesAllocated);
public static void RemoveMemoryPressure(Int64 bytesAllocated);
```

如果一个类要包装可能很大的本机资源，就应该使用这些方法提示垃圾回收器实际需要消耗多少内存。垃圾回收器内部会监视内存压力，压力变大时，就强制执行垃圾回收。

有的本机资源的数量是固定的。例如，Windows 以前就限制只能创建 5 个设备上下文。应用程序能打开的文件数量也必须有限制。同样地，从 CLR 的角度看，一个进程可以在执行垃圾回收之前分配数百个对象（每个对象都使用极少的内存）。但是，如果这些本机资源的数量有限，那么一旦试图使用超过允许数量的资源，通常会导致抛出异常。为了解决这个问题，命名空间 **System.Runtime.InteropServices** 提供了 **HandleCollector** 类：

```csharp
public sealed class HandleCollector {
    public HandleCollector(String name, Int32 initialThreshold);
    public HandleCollector(String name, Int32 initialThreshold,
        Int32 maximumThreshold);
    public void Add();
    public void Remove();

    public Int32 Count { get; }
    public Int32 InitialThreshold { get; }
    public Int32 MaximumThreshold { get; }
    public String Name { get; }
}
```

如果一个类要包装数量有限制的本机资源，就应该使用该类的实例来提示垃圾回收器实际要使用资源的多少个实例。该类的对象会在内部监视这个计数，计数太大就强制垃圾回收。

> **注意**　在内部，**GC.AddMemoryPressure** 和 **HandleCollector.Add** 方法会调用 **GC.Collect**，在第 0 代超过预算前强制进行 GC。一般都强烈反对强制开始一次垃圾回收，因为它会对应用程序性能造成负面影响。但是，类之所以调用这些方法，是为了保证应用程序能用上有限的本机资源。本机资源用光了，应用程序就会失败。对于大多数应用程序，性能遭受一些损失总胜于完全无法运行。

以下代码演示了内存压力方法及 **HandleCollector** 类的使用和效果：

```csharp
using System;
using System.Runtime.InteropServices;

public static class Program {
    public static void Main() {
        MemoryPressureDemo(0);                    // 0 导致不频繁的 GC
        MemoryPressureDemo(10 * 1024 * 1024);     // 10MB 导致频繁的 GC

        HandleCollectorDemo();
    }

    private static void MemoryPressureDemo(Int32 size) {
        Console.WriteLine();
        Console.WriteLine("MemoryPressureDemo, size={0}", size);

        // 创建一组对象，并指定它们的逻辑大小
        for (Int32 count = 0; count < 15; count++) {
            new BigNativeResource(size);
        }

        // 出于演示目的，强制一切都被清理
        GC.Collect();
    }

    private sealed class BigNativeResource {
        private Int32 m_size;

        public BigNativeResource(Int32 size) {
            m_size = size;
            // 使垃圾回收器认为对象在物理上比较大
            if (m_size > 0) GC.AddMemoryPressure(m_size);
            Console.WriteLine("BigNativeResource create.");
        }

        ~BigNativeResource() {
            // 使垃圾回收器认为对象释放了更多的内存
            if (m_size > 0) GC.RemoveMemoryPressure(m_size);
            Console.WriteLine("BigNativeResource destroy.");
        }
    }

    private static void HandleCollectorDemo() {
        Console.WriteLine();
        Console.WriteLine("HandleCollectorDemo");
        for (Int32 count = 0; count < 10; count++) {
            new LimitedResource();
        }

        // 出于演示目的，强制一切都被清理
        GC.Collect();
    }

    private sealed class LimitedResource {
        // 创建一个 HandleCollector，告诉它当两个或者更多这样的对象
        // 存在于堆中时，就执行回收
        private static readonly HandleCollector s_hc =
            new HandleCollector("LimitedResource", 2);

        public LimitedResource() {
            // 告诉 HandleCollector 堆中增加了一个 LimitedResource 对象
            s_hc.Add();
            Console.WriteLine("LimitedResource create. Count={0}", s_hc.Count);
        }

        ~LimitedResource() {
            // 告诉 HandleCollector 堆中移除了一个 LimitedResource 对象
            s_hc.Remove();
            Console.WriteLine("LimitedResource destroy. Count={0}", s_hc.Count);
        }
    }
}
```

编译并运行上述代码，会得到和下面相似的输出。

```text
MemoryPressureDemo, size=0
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.

MemoryPressureDemo, size=10485760
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource create.
BigNativeResource create.
BigNativeResource create.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.
BigNativeResource destroy.

HandleCollectorDemo
LimitedResource create. Count=1
LimitedResource create. Count=2
LimitedResource create. Count=3
LimitedResource destroy. Count=3
LimitedResource destroy. Count=2
LimitedResource destroy. Count=1
LimitedResource create. Count=1
LimitedResource create. Count=2
LimitedResource create. Count=3
```

> 注：原文在此处缺了“终结的内部工作原理”一节的标题和开头正文（终结列表 finalization list、图 21-13 的说明，以及对象 B～J 的初始状态），下文直接从扫描终结列表的中间过程开始，所以 B～J 出现得很突然。补足上下文：可终结对象在构造时被登记到终结列表中；GC 判定对象不可达后，若其类型重写了 `Finalize`，就把对它的引用从终结列表移到 `freachable` 队列，对象暂时“复活”，待专用终结线程执行完 `Finalize` 后，下一次 GC 才真正回收其内存。

> 注：PowerShell 中可以用 `[System.GC]::WaitForPendingFinalizers()` 等待终结队列清空，用 `[System.GC]::SuppressFinalize($obj)` 在显式调用 `Dispose()` 后阻止终结。脚本本身不能定义终结器，这些方法只对 FCL 中已有的可终结对象有意义。

垃圾回收开始时，对象 B，E，G，H，I 和 J 被判定为垃圾。垃圾回收器扫描终结列表以查找对这些对象的引用。找到一个引用后，该引用会从终结列表中移除，并附加到 **freachable** 队列。**freachable** 队列（发音是“F-reachable”）也是垃圾回收器的一种内部数据结构。队列中的每个引用都代表其 **Finalize** 方法已准备好调用的一个对象。图 21-14 展示了回收完毕后的托管堆。

![](img/6fa065e17c4549db7260fbfaf4fd384e_496_0.png)

图 21-14 在托管堆中，一些指针从终结列表移至 **freachable** 队列

从图 21-14 可以看出，对象 B，G 和 H 占用的内存已被回收，因为它们没有 **Finalize** 方法。但对象 E，I 和 J 占用的内存暂时不能回收，因为它们的 **Finalize** 方法还没有调用。

一个特殊的高优先级 CLR 线程专门调用 **Finalize** 方法。专用线程可避免潜在的线程同步问题。（使用应用程序的普通优先级线程就可能发生这个问题。）**freachable** 队列为空时（这很常见），该线程将睡眠。但一旦队列中有记录项出现，线程就会被唤醒，将每一项都从 **freachable** 队列中移除，同时调用每个对象的 **Finalize** 方法。由于该线程的特殊工作方式，**Finalize** 中的代码不应该对执行代码的线程做出任何假设。例如，不要在 **Finalize** 方法中访问线程的本地存储。

CLR 未来可能使用多个终结器线程。所以，代码不应假设 **Finalize** 方法会被连续调用。在只有一个终结器线程的情况下，可能有多个 CPU 分配可终结的对象，但只有一个线程执行 **Finalize** 方法，这造成该线程可能跟不上分配的速度，从而产生性能和伸缩性方面的问题。

终结列表和 **freachable** 队列之间的交互很有意思。首先，让我告诉你 **freachable** 队列这个名称的由来。“f”明显代表“终结”（finalization）；**freachable** 队列中的每个记录项都是对托管堆中应调用其 **Finalize** 方法的一个对象的引用。“reachable”意味着对象是可达的。换言之，可将 **freachable** 队列看成是像静态字段那样的一个根。所以，**freachable** 队列中的引用使它指向的对象保持可达，不是垃圾。

简单地说，当一个对象不可达时，垃圾回收器就把它视为垃圾。但是，当垃圾回收器将对象的引用从终结列表移至 **freachable** 队列时，对象不再被认为是垃圾，不能回收它的内存。对象被视为垃圾又变得不是垃圾，我们说对象被复活了。

标记 **freachable** 对象时，将递归标记对象中的引用类型的字段所引用的对象；所有这些对象也必须复活以便在回收过程中存活。之后，垃圾回收器才结束对垃圾的标识。在这个过程中，一些原本被认为是垃圾的对象复活了。然后，垃圾回收器压缩（移动）可回收的内存，将复活的对象提升到较老的一代（这不理想）。现在，特殊的终结线程清空 **freachable** 队列，执行每个对象的 **Finalize** 方法。

下次对老一代进行垃圾回收时，会发现已终结的对象成为真正的垃圾，因为没有应用程序的根指向它们，**freachable** 队列也不再指向它们。所以，这些对象的内存会直接回收。整个过程中，注意，可终结对象需要执行两次垃圾回收才能释放它们占用的内存。在实际应用中，由于对象可能被提升至另一代，所以可能要求不止进行两次垃圾回收。图 21-15 展示了第二次垃圾回收后托管堆的情况。

![](img/6fa065e17c4549db7260fbfaf4fd384e_497_0.png)

图 21-15　第二次垃圾回收后托管堆的情况

#### 21.3.5 手动监视和控制对象的生存期

CLR 为每个 AppDomain 都提供了一个 GC 句柄表（GC Handle table），允许应用程序监视或手动控制对象的生存期。这个表在 AppDomain 创建之初是空白的。表中每个记录项都包含以下两种信息：对托管堆中的一个对象的引用，以及指出如何监视或控制对象的标志（flag）。应用程序使用如下所示的 **System.Runtime.InteropServices.GCHandle** 类型在表中添加或删除记录项。

```csharp
// 该类型在 System.Runtime.InteropServices 命名空间中定义
public struct GCHandle {
    // 静态方法，用于在表中创建一个记录项
    public static GCHandle Alloc(object value);
    public static GCHandle Alloc(object value, GCHandleType type);

    // 静态方法，用于将一个 GCHandle 转换成一个 IntPtr
    public static explicit operator IntPtr(GCHandle value);
    public static IntPtr ToIntPtr(GCHandle value);

    // 静态方法，用于将一个 IntPtr 转换为一个 GCHandle
    public static explicit operator GCHandle(IntPtr value);
    public static GCHandle FromIntPtr(IntPtr value);

    // 静态方法，用于比较两个 GCHandle
    public static Boolean operator ==(GCHandle a, GCHandle b);
    public static Boolean operator !=(GCHandle a, GCHandle b);

    // 实例方法，用于释放表中的记录项（索引设为 0）
```

> 注：原文此处的代码块被截断，`Free`、`AddrOfPinnedObject`、`Target` 等实例成员声明及类的结尾缺失，紧随其后的正文也缺了“为什么需要固定（Pinned）对象”的引导段落。补足上下文：`GCHandle.Alloc(value, GCHandleType.Pinned)` 把对象钉在堆上，`AddrOfPinnedObject()` 返回其真实地址，`Free()` 解除固定。

> 注：PowerShell 可以通过类型字面量使用这些 API，例如 `$h = [System.Runtime.InteropServices.GCHandle]::Alloc($bytes, [System.Runtime.InteropServices.GCHandleType]::Pinned)`、`$h.AddrOfPinnedObject()`、`$h.Free()`。但脚本没有 `fixed` 语句，也没有指针类型；只有通过 `Add-Type` 编译的 C# 或 P/Invoke 声明才需要显式固定。`GCHandle` 是值类型，把它赋给另一个变量会复制句柄值，`Free()` 时务必对最初的那个变量调用。

垃圾回收器在内存中移动对象。String 对象被移走了，本机代码就会向已经不包含 String 对象的字符内容的内存进行读写——导致应用程序的行为无法预测。

使用 CLR 的 P/Invoke 机制调用方法时，CLR 会自动帮你固定实参，并在本机方法返回时自动解除固定。所以，大多数时候都不必使用 GCHandle 类型来显式固定任何托管对象。只有在将托管对象的指针传给本机代码，然后本机函数返回，但本机代码将来仍需要使用该对象时，才需要显式使用 GCHandle 类型。最常见的例子就是执行异步 I/O 操作。

假定分配了一个字节数组，并准备在其中填充来自一个套接字的数据。这时应该调用 GCHandle 的 Alloc 方法，传递对数组对象的引用以及 Pinned 标志。然后，在返回的 GCHandle 实例上调用 AddrOfPinnedObject 方法。这会返回一个 IntPtr，它是已固定对象在托管堆中的实际地址。然后，将该地址传给本机函数，该函数立即返回至托管代码。数据从套接字传来时，该字节数组缓冲区在内存中不会移动；阻止移动是 Pinned 标志的功劳。异步 I/O 操作完毕后调用 GCHandle 的 Free 方法，以后垃圾回收时就可以移动缓冲区了。托管代码应包含一个缓冲区引用，这使你能访问数据。正是由于这个引用的存在，所以才会阻止垃圾回收从内存中彻底释放该缓冲区。

值得注意的是，C#提供了一个 fixed 语句，它能在一个代码块中固定对象。以下代码演示了该语句是如何使用的：

```csharp
unsafe public static void Go() {
    // 分配一系列立即变成垃圾的对象
    for (Int32 x = 0; x < 10000; x++) new Object();

    IntPtr originalMemoryAddress;
    Byte[] bytes = new Byte[1000]; // 在垃圾对象后分配这个数组

    // 获取 Byte[] 在内存中的地址
    fixed (Byte* pbytes = bytes) { originalMemoryAddress = (IntPtr) pbytes; }

    // 强迫进行一次垃圾回收；垃圾对象会被回收，Byte[] 可能被压缩
    GC.Collect();

    // 获取 Byte[] 当前在内存中的地址，把它同第一个地址比较
    fixed (Byte* pbytes = bytes) {
        Console.WriteLine("The Byte[] did{0} move during the GC",
            (originalMemoryAddress == (IntPtr) pbytes) ? " not" : null);
    }
}
```

使用 C#的 fixed 语句比分配一个固定 GC 句柄高效得多。这里发生的事情是，C#编译器在 pbytes 局部变量上生成一个特殊的“已固定”标志。垃圾回收期间，GC 检查这个根的内容，如果根不为 null，就知道在压缩阶段不要移动变量引用的对象。C#编译器生成 IL 将 pbytes 局部变量初始化为 fixed 块起始处的对象的地址。在 fixed 块的尾部，编译器还会生成 IL 指令将 pbytes 局部变量设回 null，使变量不再引用任何对象。这样一来，下一次垃圾回收发生时，对象就可以移动了。

> 注：PowerShell 没有 `fixed` 语句、指针类型和 `unsafe` 上下文，无法实现上面这种“局部变量自带已固定标志”的做法。等价效果只能通过 `[System.Runtime.InteropServices.GCHandle]::Alloc($obj, [System.Runtime.InteropServices.GCHandleType]::Pinned)` 加 `AddrOfPinnedObject()` 获得，或者把这段逻辑放进 `Add-Type` 编译的 C# 代码里。

现在讨论一下另外两个标志，即 Weak 和 WeakTrackResurrection。它们既可用于和本机代码的互操作，也可在只有托管代码的时候使用。Weak 标志使你知道在什么时候一个对象被判定为垃圾，但这时对象的内存不一定被回收。WeakTrackResurrection 标志使你知道在什么时候对象的内存已被回收。两个标志中 Weak 更常用。事实上，我还没有见过任何人在真正的应用程序中用过 WeakTrackResurrection 标志。

假定 Object-A 定时在 Object-B 上调用一个方法。但由于 Object-A 有一个对 Object-B 的引用，所以阻止了 Object-B 被垃圾回收。在极少数情况下，这可能并不是你希望的；相反，你可能希望只要 Object-B 仍然存活于托管堆中，Object-A 就调用 Object-B 的方法。为此，Object-A 要调用 GCHandle 的 Alloc 方法，向方法传递对 Object-B 的引用和 Weak 标志。Object-A 现在只需保存返回的 GCHandle 实例，而不是保存对 Object-B 的引用。

在这种情况下，如果没有其他根引用 Object-B(保持其存活状态)，Object-B 就可以被垃圾回收。Object-A 每次想调用 Object-B 的方法时，都必须查询 GCHandle 的只读属性 Target。如果该属性返回非 null 的值，就表明 Object-B 依然存活。然后，Object-A 的代码会将返回的引用转型为 Object-B 的类型，并调用方法。如果 Target 属性返回 null，表明 Object-B 已被回收，Object-A 不再尝试调用方法。在这个时候，Object-A 的代码也许还要调用 GCHandle 的 Free 方法来释放 GCHandle 实例。

由于使用 GCHandle 类型有些繁琐，而且要求提升的安全性才能在内存中保持或固定对象，所以 System 命名空间提供了一个 WeakReference<T>类来帮助你。

> 注：PowerShell 可直接使用泛型弱引用，例如 `$wr = [System.WeakReference[object]]::new($obj)`。取值时 `TryGetTarget` 的 `out` 参数要先用 `[ref]` 传入且变量必须已初始化：`$target = $null; if ($wr.TryGetTarget([ref]$target)) { $target }`。注意同一作用域内若仍保留对 `$obj` 的引用，对象就不会被回收，弱引用始终有值；脚本里的变量作用域本身就是强引用。

```csharp
public sealed class WeakReference<T> : ISerializable where T : class {
    public WeakReference(T target);
    public WeakReference(T target, Boolean trackResurrection);
    public void SetTarget(T target);
    public Boolean TryGetTarget(out T target);
}
```

这个类其实是包装了一个 GCHandle 实例的面向对象包装器(wrapper)：逻辑上说，它的构造器调用 GCHandle 的 Alloc 方法，TryGetTarget 方法查询 GCHandle 的 Target 属性，SetTarget 方法设置 GCHandle 的 Target 属性，而 Finalize 方法(这里未显示，因为是受保护方法)则调用 GCHandle 的 Free 方法。此外，代码无需特殊权限即可使用 WeakReference<T>类，因为该类只支持弱引用；不支持 GCHandleType 设为 Normal 或 Pinned 的 GCHandle 实例的行为。WeakReference<T>类的缺点在于它的实例必须在堆上分配。所以，WeakReference 类比 GCHandle 实例更“重”。

开发人员经常需要将一些数据和另一个实体关联。例如，数据可以和一个线程或 AppDomain 关联。另外，可用 System.Runtime.CompilerServices.ConditionalWeakTable<TKey,TValue> 类将数据和单独的对象关联，如下所示：

```csharp
public sealed class ConditionalWeakTable<TKey, TValue>
    where TKey : class where TValue : class {
    public ConditionalWeakTable();
    public void Add(TKey key, TValue value);
    public TValue GetValue(TKey key, CreateValueCallback<TKey, TValue>
        createValueCallback);
    public Boolean TryGetValue(TKey key, out TValue value);
    public TValue GetOrCreateValue(TKey key);
    public Boolean Remove(TKey key);

    public delegate TValue CreateValueCallback(TKey key); // 嵌套的委托定义
}
```

> 注：PowerShell 中构造该类型要写出两个类型实参：`$cwt = [System.Runtime.CompilerServices.ConditionalWeakTable[object,string]]::new()`，然后可用 `$cwt.Add($key, 'value')`、`$cwt.TryGetValue($key, [ref]$value)`、`$cwt.Remove($key)`。`GetValue` 需要传入嵌套委托 `CreateValueCallback`，而 `[System.Runtime.CompilerServices.ConditionalWeakTable[object,string]+CreateValueCallback]` 这种嵌套泛型类型字面量在 PowerShell 中无法解析（报“特性或类型文本末尾缺少 ]”），脚本里通常避开它，改用上面几个成员。

> **重要提示**　开发人员刚开始学习弱引用时，会马上想到它们在缓存情形中的用处。例如，他们会想到构造包含大量数据的一组对象，并创建对这些对象的弱引用。程序需要数据时就检查这些弱引用，看看包含这些数据的对象是否依然“健在”。对象还在，程序就直接使用对象；这样程序就会有较好的性能。但如果发生垃圾回收，包含数据的对象就会被销毁。而一旦需要重新创建数据，程序的性能就会受到影响。
>
> 这个技术的问题在于：垃圾回收不是在内存满或接近满时才发生的。相反，只要第 0 代满了，垃圾回收就会发生。所以，对象在内存中被回收的频率比预想的高得多，应用程序的性能将大打折扣。
>
> 弱引用在缓存情形中确实能得到高效应用。但构建良好的缓存算法来找到内存消耗与速度之间的平衡点十分复杂。简单地说，你希望缓存保持对自己的所有对象的强引用，内存吃紧就开始将强引用转换为弱引用。目前，CLR 没有提供一个能告诉应用程序内存吃紧的机制。但已经有人通过定时调用 Win32 `GlobalMemoryStatusEx` 函数并检查返回的 `MEMORYSTATUSEX` 结构的 `dwMemoryLoad` 成员成功做到了这一点。如果该成员报告大于 80 的值，内存空间就处于吃紧状态。然后可以开始将强引用转换为弱引用——可依据的算法包括：最近最少使用算法（Least-Recently Used algorithm，LRU）、最频繁使用算法（Most-Frequently Used algorithm，MFU）以及某个时基算法（time-base algorithm）等。

任意数据要和一个或多个对象关联，首先要创建该类的实例。然后调用 **Add** 方法。为 **key** 参数传递对象引用，为 **value** 参数传递想和对象关联的数据。试图多次添加对同一个对象的引用，**Add** 方法会抛出 **ArgumentException**；要更改和对象关联的值，必须先删除 **key**，再用新值把它添加回来。注意这个类是线程安全的，多个线程能同时使用它（虽然这也意味着类的性能并不出众）；应测试好这个类的性能，验证它是否适合你的实际环境。

当然，表对象在内部存储了对作为 **key** 传递的对象的弱引用（一个 **WeakReference** 对象）；这样可保证不会因为表的存在而造成对象“被迫”存活。但是，**ConditionalWeakTable** 类最特别的地方在于，它保证了只要 **key** 所标识的对象在内存中，值就肯定在内存中。这使其超越了一个普通的 **WeakReference**，因为如果是普通的 **WeakReference**，那么即使 **key** 对象保持存活，值也可能被垃圾回收。**ConditionalWeakTable** 类可用于实现 XAML 的依赖属性（dependency property）机制。动态语言也可在内部利用它将数据和对象动态关联。

以下代码演示了 **ConditionalWeakTable** 类的使用。它允许在任何对象上调用 **GCWatch** 扩展方法并传递一些 **String** 标签（在程序中作为通知消息显示）。然后，在特定对象被垃圾回收时，它通过控制台窗口发出通知：

```csharp
internal static class ConditionalWeakTableDemo {
    public static void Main() {
        Object o = new Object();
        o.GCWatch("My Object created at " + DateTime.Now);
        GC.Collect();       // 此时看不到 GC 通知
        GC.KeepAlive(o);    // 确定 o 引用的对象现在还活着
        o = null;           // o 引用的对象现在可以死了

        GC.Collect();       // 此时才会看到 GC 通知
        Console.ReadLine();
    }
}

internal static class GCWatcher {
    // 注意：由于字符串留用(interning) 和 MarshalByRefObject 代理对象，所以
    // 使用 String 要当心
    private readonly static ConditionalWeakTable<Object, NotifyWhenGCd<String>> s_cwt =
        new ConditionalWeakTable<Object, NotifyWhenGCd<String>>();

    private sealed class NotifyWhenGCd<T> {
        private readonly T m_value;

        internal NotifyWhenGCd(T value) { m_value = value; }
        public override string ToString() { return m_value.ToString(); }
        ~NotifyWhenGCd() { Console.WriteLine("GC'd: " + m_value); }
    }

    public static T GCWatch<T>(this T @object, String tag) where T : class {
        s_cwt.Add(@object, new NotifyWhenGCd<String>(tag));
        return @object;
    }
}
```
