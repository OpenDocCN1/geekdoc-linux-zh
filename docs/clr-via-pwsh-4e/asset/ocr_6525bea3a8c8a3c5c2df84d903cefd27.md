```
public void RemoveParticipants(Int32 participantCount);    // 减去参与者
public Boolean SignalAndWait(Int32 millisecondsTimeout,
    CancellationToken cancellationToken);

public Int64 CurrentPhaseNumber { get; }                  // 指出进行到哪一个阶段（从 0 开始）
public Int32 ParticipantCount { get; }                    // 参与者数量
public Int32 ParticipantsRemaining { get; }               // 需要调用 SignalAndWait 的线程数
}
```

构造 **Barrier** 时要告诉它有多少个线程准备参与工作，还可传递一个 **Action<Barrier>** 委托来引用所有参与者完成一个阶段的工作后要调用的代码。可以调用 **AddParticipant** 和 **RemoveParticipant** 方法在 **Barrier** 中动态添加和删除参与线程。但在实际应用中，人们很少这样做。每个线程完成它的阶段性工作后，应调用 **SignalAndWait**，告诉 **Barrier** 线程已经完成一个阶段的工作，而 **Barrier** 会阻塞线程（使用一个 **ManualResetEventSlim**）。所有参与者都调用了 **SignalAndWait** 后，**Barrier** 将调用指定的委托（由最后一个调用 **SignalAndWait** 的线程调用），然后解除正在等待的所有线程的阻塞，使它们开始下一阶段。

# 30.3.7 线程同步构造小结

我的建议是，代码尽量不要阻塞任何线程。执行异步计算或 I/O 操作时，将数据从一个线程交给另一个线程时，应避免多个线程同时访问数据。如果不能完全做到这一点，请尽量使用 **Volatile** 和 **Interlocked** 的方法，因为它们的速度很快，而且绝不阻塞线程。遗憾的是，这些方法只能操作简单类型。但可以像 29.3.4 节“**Interlocked Anything** 模式”描述的那样在这些类型上执行丰富的操作。

主要在以下两种情况下阻塞线程。

+   - **线程模型很简单**
+     阻塞线程虽会牺牲一些资源和性能，但可顺序地写应用程序代码，无需使用回调方法。不过，C# 的异步方法功能现在提供了不阻塞线程的简化编程模型。
+   
+   - **线程有专门用途**
+     有的线程是特定任务专用的。最好的例子就是应用程序的主线程。如果应用程序的主线程没有阻塞，它最终就会返回，造成整个进程终止。其他例子还有应用程序的 GUI 线程。Windows 要求一个窗口或控件总是由创建它的线程操作。因此，我们有时写代码阻塞一个 GUI 线程，直到其他某个操作完成。然后，GUI 线程根据需要对窗口和控件进行更新。当然，阻塞 GUI 线程会造成应用程序挂起，使用户体验变差。

要避免阻塞线程，就不要刻意地为线程打上标签。例如，不要创建一个拼写检查线程、一个语法检查线程、一个处理特定客户端请求的线程等。为线程打上标签，其实是在告诫自己该线程不能做其他任何事情。但由于线程是如此昂贵，所以不能把它们专门用于某个目的。相反，应通过线程池将线程出租相短暂时间。所以正确方式是让一个线程池线程开始拼写检查，再改为语法检查，再代表一个客户端请求执行工作，以此类推。

如果一定要阻塞线程，为了同步在不同 AppDomain 或进程中运行的线程，请使用内核对象