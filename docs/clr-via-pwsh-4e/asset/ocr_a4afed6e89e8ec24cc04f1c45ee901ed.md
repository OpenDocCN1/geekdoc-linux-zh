费更多线程，但可以用更少的时间生成最终结果。同步 I/O 操作在客户端应用程序中没什么问题，但我强烈建议不要在服务器应用程序中执行同步 I/O 操作。

PLINQ 分析一个查询，然后决定如何最好地处理它。有的时候，顺序处理一个查询可以获得更好的性能，尤其是在使用以下任何操作时：Concat，ElementAt(OrDefault)，First(OrDefault)，Last(OrDefault)，Skip(While)，Take(While)或 Zip。使用 Select(Many)或 Where 的重载版本，并向你的 selector 或 predicate 委托传递一个位置索引时也是如此。然而，可以调用 WithExecutionMode，向它传递某个 ParallelExecutionMode 标志，从而强迫查询以并行方式处理：

```
```csharp
public enum ParallelExecutionMode {
    Default = 0,          // 让并行 LINQ 决定处理查询的最佳方式
    ForceParallelism = 1  // 强迫查询以其并行方式处理
}
```
```

如前所述，并行 LINQ 让多个线程处理数据项，结果必须再合并回去。可调用 WithMergeOptions，向它传递以下某个 ParallelMergeOptions 标志，从而控制这些结果的缓冲与合并方式：

```
```csharp
public enum ParallelMergeOptions {
    Default       = 0,  // 目前和 AutoBuffered 一样(将来可能改变)
    NotBuffered   = 1,  // 结果一旦就绪就开始处理
    AutoBuffered  = 2,  // 每个线程在处理前缓冲一些结果
    FullyBuffered = 3   // 每个线程在处理前缓冲所有结果
}
```
```

这些选项使你能在某种程度上平衡执行速度和内存消耗。NotBuffered 最省内存，但处理速度慢一些。FullyBuffered 消费较多的内存，但运行得最快。AutoBuffered 介于 NotBuffered 和 FullyBuffered 之间。说真的，要想知道应该为一个给定的查询选择哪个并行合并选项，最好的办法就是亲自试验所有选项，并对比其性能。也可以“无脑”地接受默认值，它对于许多查询来说都工作得非常好。请参见以下博客文章，进一步了解 PLINQ 如何在 CPU 内核之间分配工作：

+   - http://blogs.msdn.com/pfxteam/archive/2009/05/28/9648672.aspx
+   - http://blogs.msdn.com/pfxteam/archive/2009/06/13/9741072.aspx

# ## 27.8 执行定时计算限制操作

System.Threading 命名空间定义了一个 Timer 类，可用它让一个线程池线程定时调用一个方法。构造 Timer 类的实例相当于告诉线程池：在将来某个时间(具体由你指定)回调你的一个方法。Timer 类提供了几个相似的构造器：

```
```csharp
public sealed class Timer : MarshalByRefObject, IDisposable {
    public Timer(TimerCallback callback, Object state, Int32 dueTime, Int32 period);
    public Timer(TimerCallback callback, Object state, UInt32 dueTime, UInt32 period);
    public Timer(TimerCallback callback, Object state, Int64 dueTime, Int64 period);
    public Timer(TimerCallback callback, Object state, TimeSpan dueTime, TimeSpan period);
```
```