```
public static Int32 WaitAny(WaitHandle[] waitHandles, TimeSpan timeout);
public const Int32 WaitTimeout = 258; // 超时就从 WaitAny 返回这个

// Dispose 内部调用 Win32 CloseHandle 函数 - 自己不要调用
public void Dispose();
}
```

这些方法有几点需要注意。

+   - 可以调用 **WaitHandle** 的 **WaitOne** 方法让调用线程等待底层内核对象收到信号。这个方法在内部调用 Win32 **WaitForSingleObjectEx** 函数。如果对象收到信号，返回的 **Boolean** 是 **true**；超时就返回 **false**。
+   - 可以调用 **WaitHandle** 的静态 **WaitAll** 方法，让调用线程等待 **WaitHandle[]** 中指定的所有内核对象都收到信号。如果所有对象都收到信号，返回的 **Boolean** 是 **true**；超时则返回 **false**。这个方法在内部调用 Win32 **WaitForMultipleObjectsEx** 函数，为 **bWaitAll** 参数传递 **TRUE**。
+   - 可以调用 **WaitHandle** 的静态 **WaitAny** 方法让调用线程等待 **WaitHandle[]** 中指定的任何内核对象收到信号。返回的 **Int32** 是与收到信号的内核对象对应的数组元素索引；如果在等待期间没有对象收到信号，则返回 **WaitHandle.WaitTimeout**。这个方法在内部调用 Win32 **WaitForMultipleObjectsEx** 函数，为 **bWaitAll** 参数传递 **FALSE**。
+   - 在传给 **WaitAny** 和 **WaitAll** 方法的数组中，包含的元素数不能超过 64 个，否则方法会抛出一个 **System.NotSupportedException**。
+   - 可以调用 **WaitHandle** 的 **Dispose** 方法来关闭底层内核对象句柄。这个方法在内部调用 Win32 **CloseHandle** 函数。只有确定没有别的线程要使用内核对象才能显式调用 **Dispose**。你需要写代码并进行测试，这是一个巨大的负担。所以我强烈反对显式调用 **Dispose**；相反，让垃圾回收器（GC）去完成清理工作。GC 知道什么时候没有线程使用对象，会自动进行清理。从某个角度看，GC 是在帮你进行线程同步！

> **注意**　在某些情况下，当一个 COM 单线程套间线程阻塞时，线程可能在内部醒来以 pump 消息。例如，阻塞的线程会醒来处理发自另一个线程的 Windows 消息。这个设计是为了支持 COM 互操作性。对于大多数应用程序，这都不是一个问题——事实上，反而是一件好事。然而，如果你的代码在处理消息期间获得另一个线程同步锁，就可能发生死锁。如第 30 章所述，所有混合锁都在内部调用这些方法。所以，使用混合锁存在相同的利与弊。

不接受超时参数的那些版本的 **WaitOne** 和 **WaitAll** 方法应返回 **void** 而不是 **Boolean**。原因

① 套间(apartment)定义了一组对象的逻辑组合，这些对象共享同一组并发性和重入限制。一个线程要想使用 COM，必须先进入一个套间。COM 规定，只有运行在对象套间中的线程才能访问该对象。COM 的两种套间分别是：STA(单线程套间)和 MTA(多线程套间)。——译注