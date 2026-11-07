后，当所有这些任务完成后，可以用另外一个或多个 **Task** 对象继续。和本章展示的大量构造相比，任务具有下述许多优势。

+   - 任务使用的内存比线程少得多，创建和销毁所需的时间也少得多。
+   - 线程池根据可用 CPU 数量自动伸缩任务规模。
+   - 每个任务完成一个阶段后，运行任务的线程回到线程池，在那里能接受新任务。
+   - 线程池是站在整个进程的高度观察任务。所以，它能更好地调度这些任务，减少进程中的线程数，并减少上下文切换。

锁很流行，但长时间拥有会带来巨大的伸缩性问题。如果代码能通过异步的同步构造指出它想要一个锁，那么会非常有用。在这种情况下，如果线程得不到锁，可直接返回并执行其他工作，而不必在那里傻傻地阻塞。以后当锁可用时，代码可恢复执行并访问锁所保护的资源。我当年在为客户解决一个重大的伸缩性问题时有了这个思路，并于 2009 年将专利权卖给了 Microsoft，专利号是 7603502。

**SemaphoreSlim** 类通过 **WaitAsync** 方法实现了这个思路，下面是该方法的最复杂的重载版本的签名。

```
public Task<Boolean> WaitAsync(Int32 millisecondsTimeout, CancellationToken cancellationToken);
```

可用它异步地同步对一个资源的访问（不阻塞任何线程）。

```
private static async Task AccessResourceViaAsyncSynchronization(SemaphoreSlim asyncLock)
{
    // TODO: 执行你想要的任何代码...

    await asyncLock.WaitAsync(); // 请求获得锁来获得对资源的独占访问
    // 执行到这里，表明没有别的线程正在访问资源
    // TODO: 独占地访问资源...

    // 资源访问完毕就放弃锁，使其他代码能访问资源
    asyncLock.Release();

    // TODO: 执行你想要的任何代码...
}
```

**SemaphoreSlim** 的 **WaitAsync** 方法很有用，但它提供的是信号量语义。一般创建最大计数为 1 的 **SemaphoreSlim**，从而对 **SemaphoreSlim** 保护的资源进行互斥访问。所以，这和使用 **Monitor** 时的行为相似，只是 **SemaphoreSlim** 不支持线程所有权和递归语义（这是好事）。

但 reader-writer 语义呢？.NET Framework 提供了 **ConcurrentExclusiveSchedulerPair** 类。

```
public class ConcurrentExclusiveSchedulerPair {
    public ConcurrentExclusiveSchedulerPair();

    public TaskScheduler ExclusiveScheduler { get; }
    public TaskScheduler ConcurrentScheduler { get; }

    // 未列出其他方法...
}
```