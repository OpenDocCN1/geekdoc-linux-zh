```
public DateTime LastTransaction {
    get {
        m_lock.EnterReadLock();
        // 以下代码拥有对数据的共享访问权...
        DateTime temp = m_timeOfLastTrans;
        m_lock.ExitReadLock();
        return temp;
    }
}

public void Dispose() { m_lock.Dispose(); }
```

这个构造有几个概念要特别留意。首先，**ReaderWriterLockSlim** 的构造器允许传递一个 **LockRecursionsPolicy** 标志，它的定义如下：

```
public enum LockRecursionPolicy { NoRecursion, SupportsRecursion }
```

如果传递 **SupportsRecursion** 标志，锁就支持线程所有权和递归行为。如同本章早些时候讨论的那样，这些行为对锁的性能有负面影响。所以，建议总是向构造器传递 **LockRecursionPolicy.NoRecursion**（就像本例）。reader-writer 锁支持线程所有权和递归的代价非常高昂，因为锁必须跟踪曾允许进入锁的所有 reader 线程，同时为每个线程都单独维护递归计数。事实上，为了以线程安全的方式维护所有这些信息，**ReaderWriterLockSlim** 内部要使用一个互斥的“自旋锁”，我不是在开玩笑！

**ReaderWriterLockSlim** 类提供了一些额外的方法（前面没有列出）允许一个 reader 线程升级为 writer 线程。以后，线程可以把自己降级回 reader 线程。设计者的思路是，一个线程刚开始的时候可能是读取数据。然后，根据数据的内容，线程可能想对数据进行修改。为此，线程要把它自己从 reader 升级为 writer。锁如果支持这个行为，性能会大打折扣。而且我完全不觉得这是一个有用的功能。线程并不是直接从 reader 变成 writer 的。当时可能还有其他线程正在读取，这些线程必须完全退出锁。在此之后，尝试升级的线程才允许成为 writer。这相当于先让 reader 线程退出锁，再立即获取这个锁以进行写入。

> **注意**　FCL 还提供了一个 **ReaderWriterLock** 构造，它是在 Microsoft .NET Framework 1.0 中引入的。这个构造存在许多问题，所以 Microsoft 在 .NET Framework 3.5 中引入了 **ReaderWriterLockSlim** 构造。团队没有对原先的 **ReaderWriterLock** 构造进行改进，因为他们害怕失去和那些正在使用它的应用程序的兼容性。下面列举了 **ReaderWriterLock** 存在的几个问题。首先，即使不存在有线程竞争，它的速度也非常慢。其次，线程所有权和递归行为是这个构造强加的，完全取消不了，这使锁变得更慢。最后，相比 writer 线程，它更青睐于 reader 线程，所以 writer 线程可能排起好长的队，却很少有机会获得服务，最终造成“拒绝服务”（DoS）问题。