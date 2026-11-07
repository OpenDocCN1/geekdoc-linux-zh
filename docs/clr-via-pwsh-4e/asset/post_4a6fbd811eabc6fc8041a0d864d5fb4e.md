
```csharp
} else {
    // 在线程池线程上处理 I/O 完成，
    // 在此添加自己的计算密集型算法...
    result = task.Result.Length; // 本例只是返回长度
}

// 保存结果(exception/sum)，指出 1 个操作完成
m_servers[server] = result;
m_ac.JustEnded();
}

// 调用这个方法指出结果已无关紧要
public void Cancel() { m_ac.Cancel(); }

// 所有 Web 服务器都响应、调用了 Cancel 或者发生超时，就调用该方法
private void AllDone(CoordinationStatus status) {
    switch (status) {
        case CoordinationStatus.Cancel:
            Console.WriteLine("Operation canceled");
            break;

        case CoordinationStatus.Timeout:
            Console.WriteLine("Operation timed-out");
            break;

        case CoordinationStatus.AllDone:
            Console.WriteLine("Operation completed; results below:");
            foreach (var server in m_servers) {
                Console.Write("{0} ", server.Key);
                Object result = server.Value;
                if (result is Exception) {
                    Console.WriteLine("failed due to {0}.", result.GetType().Name);
                } else {
                    Console.WriteLine("returned {0:N0} bytes.", result);
                }
            }
            break;
    }
}
```

可以看出，上述代码并没有直接使用 Interlocked 的任何方法，因为我将所有协调代码都放到可重用的 AsyncCoordinator 类中。该类会在以后详细解释。我想先说明一下这个类的作用。构造一个 MultiWebRequests 类时，会先初始化一个 AsyncCoordinator 和包含了一组服务器 URI(及其将来结果)的字典。然后，它以异步方式一个接一个地发出所有 Web 请求。为此，它首先调用 AsyncCoordinator 的 AboutToBegin 方法，向它传递要发出的请求数量。然后，它调用 HttpClient 的 GetByteArrayAsync 来初始化请求。这会返回一个 Task，我随即在这个 Task 上调用 ContinueWith，确保在服务器有了响应之后，我的 ComputeResult 方法可通过许多线程池线程并发处理结果。对 Web 服务器的所有请求都发出之后，将调用 AsyncCoordinator 的 AllBegun 方法，向它传递要在所有操作完成后执行的方法(AllDone)以及一个超时值。每收到一个 Web 服务器响应，线程池线程都会调用 MultiWebRequests

- ① 可改写代码，在 for 循环前调用一次 m_ac.AboutToBegin(m_requests.Count)，而不是每次循环迭代都调用 AboutToBegin。

这个类最重要的字段就是 **m_opCount** 字段，用于跟踪仍在进行的异步操作的数量。每个异步操作开始前都会调用 **AboutToBegin**。该方法调用 **Interlocked.Add**，以原子方式将传给它的数字加到 **m_opCount** 字段上。**m_opCount** 上的加法运算必须以原子方式进行，因为随着更多的操作开始，可能开始在线程池线程上处理 Web 服务器的响应。处理好 Web 服务器的响应后会调用 **JustEnded**。该方法调用 **Interlocked.Decrement**，以原子方式从 **m_opCount** 上减 1。无论哪一个线程恰好将 **m_opCount** 设为 0，都由它调用 **ReportStatus**。

![](img/6fa065e17c4549db7260fbfaf4fd384e_698_0.png)

> **注意**　**m_opCount** 字段初始化为 1（而非 0），这一点很重要。执行构造器方法的线程在发出 Web 服务请求期间，由于 **m_opCount** 字段为 1，所以能保证 **AllDone** 不会被调用。构造器调用 **AllBegun** 之前，**m_opCount** 永远不可能变成 0。构造器调用 **AllBegun** 时，**AllBegun** 内部调用 **JustEnded** 来递减 **m_opCount**，所以事实上撤消（undo）了把它初始化成 1 的效果。现在 **m_opCount** 能变成 0 了，但只能是在发起了所有 Web 服务请求之后。

**ReportStatus** 方法对全部操作结束、发生超时和调用 **Cancel** 时可能发生的竞态条件进行仲裁。**ReportStatus** 必须确保其中只有一个条件胜出，确保 **m_callback** 方法只被调用一次。为了仲裁赢家，要调用 **Interlocked.Exchange** 方法，向它传递对 **m_statusReported** 字段的引用。这个字段实际是作为一个 **Boolean** 变量使用的；但不能真的把它写成一个 **Boolean** 变量，因为没有任何 **Interlocked** 方法能接受 **Boolean** 变量。因此，我用一个 **Int32** 变量来代替，0 意味着 **false**，1 意味着 **true**。

在 **ReportStatus** 内部，**Interlocked.Exchange** 调用会将 **m_statusReported** 更改为 1。但只有做这个事情的第一个线程才会看到 **Interlocked.Exchange** 返回 0，只有这个线程才能调用回调方法。调用 **Interlocked.Exchange** 的其他任何线程都会得到返回值 1，相当于告诉这些线程：回调方法已被调用，你不要再调用了。

## 29.3.3 实现简单的自旋锁¹

**Interlocked** 的方法很好用，但主要用于操作 **Int32** 值。如果需要原子性地操作类对象中的一组字段，又该怎么办呢？在这种情况下，需要采取一个方法阻止所有线程，只允许其中一个进入对字段进行操作的代码区域。可以使用 **Interlocked** 的方法构造一个线程同步块：

```csharp
internal struct SimpleSpinLock {
    private Int32 m_ResourceInUse; // 0=false（默认），1=true

    public void Enter() {
        while (true) {
            // 总是将资源设为“正在使用”（1），
            // 只有从“未使用”变成“正在使用”才会返回
            if (Interlocked.Exchange(ref m_ResourceInUse, 1) == 0) return;
            // 在这里添加“黑科技”...
        }
    }

    public void Leave() {
        // 将资源标记为“未使用”
        Volatile.Write(ref m_ResourceInUse, 0);
    }
}
```

下面这个类展示了如何使用 **SimpleSpinLock**：

```csharp
public sealed class SomeResource {
    private SimpleSpinLock m_sl = new SimpleSpinLock();

    public void AccessResource() {
        m_sl.Enter();
        // 一次只有一个线程才能进入这里访问资源...
        m_sl.Leave();
    }
}
```

SimpleSpinLock 的实现很简单。如果两个线程同时调用 Enter，那么 Interlocked.Exchange 会确保一个线程将 m_resourceInUse 从 0 变成 1，并发现 m_resourceInUse 为 0，然后这个线程从 Enter 返回，使它能继续执行 AccessResource 方法中的代码。另一个线程会将 m_resourceInUse 从 1 变成 1。由于不是从 0 变成 1，所以会不停地调用 Exchange 进行“自旋”，直到第一个线程调用 Leave。

第一个线程完成对 SomeResource 对象的字段的处理之后会调用 Leave。Leave 内部调用 Volatile.Write，将 m_resourceInUse 更改回 0。这造成正在“自旋”的线程能够将 m_resourceInUse 从 0 变成 1，所以终于能从 Enter 返回，终于可以开始访问 SomeResource 对象的字段。

这就是线程同步锁的一个简单实现。这种锁最大的问题在于，在存在对锁的竞争的前提下，会造成线程“自旋”。这个“自旋”会浪费宝贵的 CPU 时间，阻止 CPU 做其他更有用的工作。因此，自旋锁只应该用于保护那些会执行得非常快的代码区域。

自旋锁一般不要在单 CPU 机器上使用，因为在这种机器上，一方面是希望获得锁的线程自旋，一方面是占有锁的线程不能快速释放锁。如果占有锁的线程的优先级低于想要获得锁的线程（自旋线程），局面还会变得更糟，因为占有锁的线程可能根本没机会运行。这会造成“活锁”情形。Windows 有时会短时间地动态提升一个线程的优先级。因此，对于正在使用自旋锁的线程，应该禁止像这样的优先级提升：请参考 **System.Diagnostics.Process** 和 **System.Diagnostics.ProcessThread** 的 **PriorityBoostEnabled** 属性。超线程机器同样存在自旋锁的问题。为了解决这些问题，许多自旋锁内部都有一些额外的逻辑；我将这些额外的逻辑称为“黑科技”(Black Magic)。这里不打算过多讲解其中的细节，因为随着越来越多的人开始研究锁及其性能，这些逻辑也可能发生变化。但我可以告诉你的是：FCL 提供了一个名为 **System.Threading.SpinWait** 的结构，它封装了人们关于这种“黑科技”的最新研究成果。

- ① 从 0 变成 1 才返回（结束自旋），从 1 变成 1 不返回（继续自旋）。——译注
- ② 本节稍后会在正文中描述“黑科技”（Black Magic）。——译注
- ③ Interlocked.Exchange 方法将一个存储位置设为指定值，并返回该存储位置的原始值。详情请参考文档。——译注
- ④ 活锁和死锁的区别请参见 29.2 节“基元用户模式和内核模式构造”。——译注

FCL 还包含一个 **System.Threading.SpinLock** 结构，它和前面展示的 **SimpleSpinLock** 类相似，只是使用了 **SpinWait** 结构来增强性能。**SpinLock** 结构还提供了超时支持。很有趣的一点是，我的 **SimpleSpinLock** 和 FCL 的 **SpinLock** 都是值类型。这意味着它们是轻量级的、内存友好的对象。例如，如果需要将一个锁同集合中的每一项关联，**SpinLock** 就是很好的选择。但一定不要到处传递 **SpinLock** 实例，否则它们会被复制，而你会失去所有同步。虽然可以定义实例 **SpinLock** 字段，但不要将字段标记为 **readonly**，因为在操作锁的时候，它的内部状态必须改变。

### 在线程处理中引入延迟

“黑科技”旨在让希望获得资源的线程暂停执行，使当前拥有资源的线程能执行它的代码并让出资源。为此，**SpinWait** 结构内部调用 **Thread** 的静态 **Sleep**，**Yield** 和 **SpinWait** 方法。在这里的补充内容中，我想简单解释一下这些方法。

线程可告诉系统它在指定时间内不想被调度。这是调用 **Thread** 的静态 **Sleep** 方法来实现的：

```csharp
public static void Sleep(Int32 millisecondsTimeout);
public static void Sleep(TimeSpan timeout);
```

这个方法导致线程在指定时间内挂起。调用 **Sleep** 允许线程自愿放弃它的时间片的剩余部分。系统会使线程在大致指定的时间里不被调度。没有错——如果告诉系统你希望一个线程睡眠 100 毫秒，那么会睡眠大致那么长的时间，但也有可能会多睡眠几秒、甚至几分钟的时间。记住，Windows 不是实时操作系统。你的线程可能在正确的时间唤醒，但具体是否这样，要取决于系统中正在发生的别的事情。

可以调用 **Sleep**，并为 **millisecondsTimeout** 参数传递 **System.Threading.Timeout.Infinite** 中的值(定义为-1)。这告诉系统永远不调度线程，但这样做没什么意义。更好的做法是让线程退出，回收它的栈和内核对象。可以向 **Sleep** 传递 **0**，告诉系统调用线程放弃了它当前时间片的剩余部分，强迫系统调度另一个线程。但系统可能重新调度刚才调用了 **Sleep** 的线程(如果没有相同或更高优先级的其他可调度线程，就会发生这种情况)。

线程可要求 Windows 在当前 CPU 上调度另一个线程，这是通过 **Thread** 的 **Yield** 方法来实现的：

```csharp
public static Boolean Yield();
```

如果 **Windows** 发现有另一个线程准备好在当前处理器上运行，**Yield** 就会返回 **true**，调用 **Yield** 的线程会提前结束它的时间片①，所选的线程得以运行一个时间片。然后，调用 **Yield** 的线程被再次调度，开始用一个全新的时间片运行。如果 **Windows** 发现没有其他线程准备在当前处理器上运行，**Yield** 就会返回 **false**，调用 **Yield** 的线程继续运行它的时间片。

**Yield** 方法旨在使“就绪”状态的、具有相等或更低优先级的线程有机会运行。如果一个线程希望获得当前由另一个线程拥有的资源，就调用这个方法。如果运气好，**Windows** 会调度当前拥有该资源的线程，而那个线程会让出资源。然后，当调用 **Yield** 的线程再次运行时就会拿到资源。

调用 **Yield** 的效果介于调用 **Thread.Sleep(0)** 和 **Thread.Sleep(1)** 之间。**Thread.Sleep(0)** 不允许较低优先级的线程运行，而 **Thread.Sleep(1)** 总是强迫进行上下文切换，而由于内部系统计时器的解析度的问题，**Windows** 总是强迫线程睡眠超过 1 毫秒的时间。

事实上，超线程 CPU 一次只允许一个线程运行。所以，在这些 CPU 上执行“自旋”循环时，需要强迫当前线程暂停，使 CPU 有机会切换到另一个线程并允许它运行。线程可调用 **Thread** 的 **SpinWait** 方法强迫它自身暂停，允许超线程 CPU 切换到另一个线程。

```csharp
public static void SpinWait(Int32 iterations);
```

调用这个方法实际会执行一个特殊的 CPU 指令；它不告诉 **Windows** 做任何事情（因为 **Windows** 已经认为它在 CPU 上调度了两个线程）。在非超线程 CPU 上，这个特殊 CPU 指令会被忽略。

要更多地了解这些方法，请参见它们的 Win32 等价函数：**Sleep**、**SwitchToThread** 和 **YieldProcessor**。另外，要想进一步了解如何调整系统计时器的解析度，请参考 Win32 **timeBeginPeriod** 和 **timeEndPeriod** 函数。

## 29.3.4　Interlocked Anything 模式

许多人在查看 **Interlocked** 的方法时，都好奇 **Microsoft** 为什么不创建一组更丰富的 **Interlocked** 方法，使它们适用于更广泛的情形。例如，如果 **Interlocked** 类能提供 **Multiple**、**Divide**、**Minimum**、**Maximum**、**And**、**Or**、**Xor** 等方法，那么不是更好吗？虽然 **Interlocked** 类没有提供这些方法，但一个已知的模式允许使用 **Interlocked.CompareExchange** 方法以

- ① 这正是 yield 一词在当前上下文中的含义，即放弃或叫停；而不是文档中翻译的“生成”或“产生”。例如，文档将 “If this method succeeds, the rest of the thread's current time slice is yielded.” 这句话翻译成“如果此方法成功，则生成该线程当前时间片的其余部分。”（参见 MSDN 的 **Thread.Yield** 方法）。我不得不说，“翻译记忆”害死人，因为它不区分上下文。相应地，C# 的 yield 关键字就确实有“生成”的意思。——译注
