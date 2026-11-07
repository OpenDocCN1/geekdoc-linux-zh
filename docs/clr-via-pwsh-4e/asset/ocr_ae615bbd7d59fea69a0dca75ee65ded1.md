使用自旋锁的线程，应该禁止像这样的优先级提升：请参考 **System.Diagnostics.Process** 和 **System.Diagnostics.ProcessThread** 的 **PriorityBoostEnabled** 属性。超线程机器同样存在自旋锁的问题。为了解决这些问题，许多自旋锁内部都有一些额外的逻辑；我将这些额外的逻辑称为“黑科技”(Black Magic)。这里不打算过多讲解其中的细节，因为随着越来越多的人开始研究锁及其性能，这些逻辑也可能发生变化。但我可以告诉你的是：FCL 提供了一个名为 **System.Threading.SpinWait** 的结构，它封装了人们关于这种“黑科技”的最新研究成果。

FCL 还包含一个 **System.Threading.SpinLock** 结构，它和前面展示的 **SimpleSpinLock** 类相似，只是使用了 **SpinWait** 结构来增强性能。**SpinLock** 结构还提供了超时支持。很有趣的一点是，我的 **SimpleSpinLock** 和 FCL 的 **SpinLock** 都是值类型。这意味着它们是轻量级的、内存友好的对象。例如，如果需要将一个锁同集合中的每一项关联，**SpinLock** 就是很好的选择。但一定不要到处传递 **SpinLock** 实例，否则它们会被复制，而你会失去所有同步。虽然可以定义实例 **SpinLock** 字段，但不要将字段标记为 **readonly**，因为在操作锁的时候，它的内部状态必须改变。

# 在线程处理中引入延迟

“黑科技”旨在让希望获得资源的线程暂停执行，使当前拥有资源的线程能执行它的代码并让出资源。为此，**SpinWait** 结构内部调用 **Thread** 的静态 **Sleep**，**Yield** 和 **SpinWait** 方法。在这里的补充内容中，我想简单解释一下这些方法。

线程可告诉系统它在指定时间内不想被调度。这是调用 **Thread** 的静态 **Sleep** 方法来实现的：

```
public static void Sleep(Int32 millisecondsTimeout);
public static void Sleep(TimeSpan timeout);
```

这个方法导致线程在指定时间内挂起。调用 **Sleep** 允许线程自愿放弃它的时间片的剩余部分。系统会使线程在大致指定的时间里不被调度。没有错——如果告诉系统你希望一个线程睡眠 100 毫秒，那么会睡眠大致那么长的时间，但也有可能会多睡眠几秒、甚至几分钟的时间。记住，Windows 不是实时操作系统。你的线程可能在正确的时间唤醒，但具体是否这样，要取决于系统中正在发生的别的事情。

可以调用 **Sleep**，并为 **millisecondsTimeout** 参数传递 **System.Threading.Timeout.Infinite** 中的值(定义为-1)。这告诉系统永远不调度线程，但这样做没什么意义。更好的做法是让线程退出，回收它的栈和内核对象。可以向 **Sleep** 传递 **0**，告诉系统调用线程放弃了它当前时间片的剩余部分，强迫系统调度另一个线程。但系统可能重新调度刚才调用了 **Sleep** 的线程(如果没有相同或更高优先级的其他可调度线程，就会发生这种情况)。

线程可要求 Windows 在当前 CPU 上调度另一个线程，这是通过 **Thread** 的 **Yield** 方法来实现的：

```
public static Boolean Yield();
```