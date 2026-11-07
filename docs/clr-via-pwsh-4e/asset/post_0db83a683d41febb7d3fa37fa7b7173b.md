
```csharp
StartServer();

// 发起大量异步客户端请求；保存每个客户端的 Task<String>
List<Task<String>> requests = new List<Task<String>>(10000);
for (Int32 n = 0; n < requests.Capacity; n++)
    requests.Add(IssueClientRequestAsync("localhost", "Request #" + n));

// 每个任务完成都继续
while (requests.Count > 0) {
    // 顺序处理每个完成的响应
    Task<String> response = await Task.WhenAny(requests);
    requests.Remove(response); // 从集合中删除完成的任务

    // 处理一个响应
    Console.WriteLine(response.Result);
}
```

上述代码创建 **while** 循环，针对每个客户端请求都迭代一次。循环内部等待 **Task** 的 **WhenAny** 方法，该方法一次返回一个 **Task<String>** 对象，代表由服务器响应的一个客户端请求。获得这个 **Task<String>** 对象后，就把它从集合中删除，然后查询它的结果以进行处理(把它传给 **Console.WriteLine**)。

## 28.9 应用程序及其线程处理模型

.NET Framework 支持几种不同的应用程序模型，而每种模型都可能引入了它自己的线程处理模型。控制台应用程序和 Windows 服务(实际上也是控制台应用程序；只是看不见控制台而已)没有引入任何线程处理模型；换言之，任何线程可在任何时候做它想做的任何事情。

但 GUI 应用程序(包括 Windows 窗体、WPF、Silverlight 和 Windows Store 应用程序)引入了一个线程处理模型。在这个模型中，UI 元素只能由创建它的线程更新。在 GUI 线程中，经常都需要生成一个异步操作，使 GUI 线程不至于阻塞并停止响应用户输入(比如鼠标、按键、手写笔和触控事件)。但当异步操作完成时，是由一个线程池线程完成 Task 对象并恢复状态机。

对于某些应用程序模型，这样做无可非议，甚至可以说正好符合开发人员的意愿，因为它非常高效。但对于另一些应用程序模型(比如 GUI 应用程序)，这个做法会造成问题，因为一旦通过线程池线程更新 UI 元素就会抛出异常。线程池线程必须以某种方式告诉 GUI 线程更新 UI 元素。

ASP.NET 应用程序允许任何线程做它想做的任何事情。线程池线程开始处理一个客户端的请求时，可以对客户端的语言文化(**System.Globalization.CultureInfo**)做出假定，从而允许 Web 服务器对返回的数字、日期和时间进行该语言文化特有的格式化处理。此外，Web 服务器还可对客户端的身份标识(**System.Security.Principal.IPrincipal**)做出假定，确保只能

① 欲知详情，请访问 http://msdn.microsoft.com/zh-cn/library/bz9tc508.aspx。注意，帮助文档将 culture 翻译成“区域性”。——译注

Task<TResult>类提供了一个 ConfigureAwait 方法，它的签名如下所示。

```csharp
// 定义这个方法的 Task
public ConfiguredTaskAwaitable ConfigureAwait(Boolean continueOnCapturedContext);

// 定义这个方法的 Task<TResult>
public ConfiguredTaskAwaitable<TResult> ConfigureAwait(Boolean continueOnCapturedContext);
```

向方法传递 true 相当于根本没有调用方法。但如果传递 false，await 操作符就不查询调用线程的 SynchronizationContext 对象。当线程池线程结束 Task 时会直接完成它，await 操作符后面的代码通过线程池线程执行。

虽然我的 GetHttp 方法不是类库代码，但在添加了对 ConfigureAwait 的调用后，死锁问题就不翼而飞。下面是修改过的 GetHttp 方法。

```csharp
private async Task<String> GetHttp() {
    // 发出 HTTP 请求，让线程从 GetHttp 返回
    HttpResponseMessage msg = await new
        HttpClient().GetAsync("http://Wintellect.com/").ConfigureAwait(false);
    // 这里能执行到了，因为线程池线程可以执行这里的代码，
    // 而非被迫由 GUI 线程执行

    return await msg.Content.ReadAsStringAsync().ConfigureAwait(false);
}
```

如上述代码所示，必须将 ConfigureAwait(false)应用于等待的每个 Task 对象。这是由于异步操作可能同步完成，而且在发生这个情况时，调用线程直接继续执行，不会返回至它的调用者；你根本不知道哪个操作要求忽略 SynchronizationContext 对象，所以只能要求所有操作都忽略它。这还意味着类库代码不能依赖于任何特定的应用程序模型。另外，也可以像下面这样重写 GetHttp 方法，用一个线程池线程执行所有操作。

```csharp
private Task<String> GetHttp() {
    return Task.Run(async () => {
        // 运行一个无 SynchronizationContext 的线程池线程
        HttpResponseMessage msg = await new HttpClient().GetAsync("http://Wintellect.com/");
        // 这里的代码真的能执行，因为某个线程池线程能执行这里的代码

        return await msg.Content.ReadAsStringAsync();
    });
}
```

在这个版本中，注意，GetHttp 不再是异步函数；我从方法签名中删除了 async 关键字，因为方法中没有了 await 操作符。但是，传给 Task.Run 的 lambda 表达式是异步函数。

## 28.10　以异步方式实现服务器

根据我多年来和开发人员的交流经验，发现很少有人知道.NET Framework 其实内建了对伸缩性很好的—些异步服务器的支持。本书限制篇幅无法一一解释，但可以列出 MSDN 文档中值得参考的地方。

- 要构建异步 ASP.NET Web 窗体，在.aspx 文件中添加 `Async="true"` 网页指令，并参考 `System.Web.UI.Page` 的 `RegisterAsyncTask` 方法。
- 要构建异步 ASP.NET MVC 控制器，使你的控制器类从 **System.Web.Mvc.AsyncController** 派生，让操作方法返回一个 **Task<ActionResult>** 即可。
- 要构建异步 ASP.NET 处理程序，使你的类从 **System.Web.HttpTaskAsyncHandler** 派生，重写其抽象 **ProcessRequestAsync** 方法。
- 要构建异步 WCF 服务，将服务作为异步函数实现，让它返回 Task 或 Task<TResult>。

## 28.11 取消 I/O 操作

Windows 一般没有提供取消未完成 I/O 操作的途径。这是许多开发人员都想要的功能，实现起来却很困难。毕竟，如果向服务器请求了 1000 个字节，然后决定不再需要这些字节，那么其实没有办法告诉服务器忘掉你的请求。在这种情况下，只能让字节照常返回，再将它们丢弃。此外，这里还会发生竞态条件——取消请求的请求可能正好在服务器发送响应的时候到来。这时应该怎么办？所以，要在代码中处理这种潜在的竞态条件，决定是丢弃还是使用数据。

为此，我建议实现一个 **WithCancellation** 扩展方法来扩展 **Task<TResult>**（需要类似的重载版本来扩展 **Task**），如下所示：

```csharp
private struct Void { } // 因为没有非泛型的 TaskCompletionSource 类

private static async Task<TResult> WithCancellation<TResult>(this Task<TResult> originalTask,
    CancellationToken ct) {

    // 创建在 CancellationToken 被取消时完成的一个 Task
    var cancelTask = new TaskCompletionSource<Void>();

    // 一旦 CancellationToken 被取消，就完成 Task
    using (ct.Register(
        t => ((TaskCompletionSource<Void>)t).TrySetResult(new Void()), cancelTask)) {

        // 创建在原始 Task 或 CancellationToken Task 完成时都完成的一个 Task
        Task any = await Task.WhenAny(originalTask, cancelTask.Task);

        // 任何 Task 因为 CancellationToken 而完成，就抛出 OperationCanceledException
        if (any == cancelTask.Task) ct.ThrowIfCancellationRequested();
    }

    // 等待原始任务（以同步方式），若任务失败，等待它将抛出第一个内部异常，
    // 而不是 AggregateException
    return await originalTask;
}
```

现在可以像下面这样调用该扩展方法。

```csharp
public static async Task Go() {
    // 创建一个 CancellationTokenSource，它在5秒后取消自己
    var cts = new CancellationTokenSource(5000); // 更快地取消请调用 cts.Cancel()
    var ct = cts.Token;

    try {
        // 我用 Task.Delay 进行测试：把它替换成返回一个 Task 的其他方法
```

另一方面，可在创建 **FileStream** 对象时指定 **FileOptions.Asynchronous** 标志。然后，可以调用 **FileStream** 的 **Read** 方法执行一个同步操作。在内部，**FileStream** 类会开始一个异步操作，然后立即使调用线程进入睡眠状态，直至操作完成才会唤醒，从而模拟同步行为。这同样效率低下。但相较于不指定 **FileOptions.Asynchronous** 标志来构造一个 **FileStream** 并调用 **ReadAsync**，它的效率还是要高上那么一点点的。

总之，使用 **FileStream** 时必须先想好是同步还是异步执行文件 I/O，并指定（或不指定）**FileOptions.Asynchronous** 标志来指明自己的选择。如果指定了该标志，就总是调用 **ReadAsync**。如果没有指定这个标志，就总是调用 **Read**。这样可以获得最佳的性能。如果想先对 **FileStream** 执行一些同步操作，再执行一些异步操作，那么更高效的做法是使用 **FileOptions.Asynchronous** 标志来构造它。另外，也可针对同一个文件创建两个 **FileStream** 对象；打开一个 **FileStream** 进行异步 I/O，打开另一个 **FileStream** 进行同步 I/O。注意，**System.IO.File** 类提供了辅助方法（**Create**、**Open** 和 **OpenWrite**）来创建并返回 **FileStream** 对象。但所有这些方法都没有在内部指定 **FileOptions.Asynchronous** 标志，所以为了实现响应灵敏的、可伸缩的应用程序，应避免使用这些方法。

还要注意，NTFS 文件系统设备驱动程序总是以同步方式执行一些操作，不管具体如何打开文件。详情参见 http://support.microsoft.com/default.aspx?scid=kb%3Ben-us%3B156932。

## 28.13　I/O 请求优先级

第 26 章“线程基础”介绍了线程优先级对线程调度方式的影响。然而，线程还要执行 I/O 请求以便从各种硬件设备中读写数据。如果一个低优先级线程获得了 CPU 时间，它可以在非常短的时间里轻易地将成百上千的 I/O 请求放入队列。由于 I/O 请求一般需要时间来执行，所以一个低优先级线程可能挂起高优先级线程，使后者不能快速完成工作，从而严重影响系统的总体响应能力。正是由于这个原因，当系统执行一些耗时的低优先级服务时（比如磁盘碎片整理程序、病毒扫描程序、内容索引程序等），机器的响应能力可能会变得非常差。①

Windows 允许线程在发出 I/O 请求时指定优先级。欲知 I/O 优先级的详情，请参考以下网址的白皮书：http://www.microsoft.com/whdc/driver/priorityio.mspx。遗憾的是，FCL 还没有包含这个功能；但未来的版本有望添加。如果现在就想使用这个功能，可以采取 P/Invoke 本机 Win32 函数的方式。以下是 P/Invoke 代码：

```csharp
internal static class ThreadIO {
    public static BackgroundProcessingDisposer BeginBackgroundProcessing(
        Boolean process = false) {

        ChangeBackgroundProcessing(process, true);
        return new BackgroundProcessingDisposer(process);
    }
}
```

① Windows SuperFetch 功能就利用了低优先级 I/O 请求。

多个线程同时对共享数据进行只读访问是没有任何问题的。例如，许多应用程序都会在它们初始化期间创建一些数据结构。初始化完成后，应用程序就可以创建它希望的任何数量的线程；如果所有线程都只是查询数据，那么所有线程都能同时查询，无需获取或释放一个锁。**String** 类型便是这样的一个例子：一旦创建好 **String** 对象，它就是“不可变”(immutable)的。所以，许多线程能同时访问一个 **String** 对象，**String** 对象没有被破坏之虞。

## 29.1 类库和线程安全

现在，我想简单地谈一谈类库和线程同步。Microsoft 的 Framework Class Library(FCL)保证所有静态方法都是线程安全的。这意味着假如两个线程同时调用一个静态方法，不会发生数据被破坏的情况。FCL 必须在内部做到这一点，因为开发不同程序集的多个公司不可能事先协商好使用一个锁来仲裁对资源的访问。Console 类包含了一个静态字段，类的许多方法都要获取和释放这个字段上的锁，确保一次只有一个线程访问控制台。

要郑重声明的是，使一个方法线程安全，并不是说它一定要在内部获取一个线程同步锁。线程安全的方法意味着在两个线程试图同时访问数据时，数据不会被破坏。**System.Math** 类有一个静态 **Max** 方法，它像下面这样实现：

```csharp
public static Int32 Max(Int32 val1, Int32 val2) {
    return (val1 < val2) ? val2 : val1;
}
```

这个方法是线程安全的，即使它没有获取任何锁。由于 **Int32** 是值类型，所以传给 **Max** 的两个 **Int32** 值会复制到方法内部。多个线程可以同时调用 **Max** 方法，每个线程处理的都是它自己的数据，线程之间互不干扰。

另一方面，FCL 不保证实例方法是线程安全的，因为假如全部添加锁定，会造成性能的巨大损失。另外，假如每个实例方法都需要获取和释放一个锁，事实上会造成最终在任何给定的时刻，你的应用程序只有一个线程在运行，这对性能的影响是显而易见的。如前所述，线程构造对象时，只有这个线程才拥有对象引用，其他线程都不能访问那个对象，所以在调用实例方法时无需线程同步。然而，如果线程随后公开了这个对象引用——把它放到一个静态字段中，把它作为状态类参数传给一个 **ThreadPool.QueueUserWorkItem** 或 **Task**——那么在多个线程可能同时进行并只读访问的前提下，就需要线程同步。

建议你自己的类库也遵循 FCL 的这个模式；也就是说，使自己的所有静态方法都线程安全，使所有实例方法都非线程安全。这个模式有一点要注意：如果实例方法的目的是协调线程，则实例方法应该是线程安全的。例如，一个线程可能调用 **CancellationTokenSource** 的 **Cancel** 方法取消一个操作，另一个线程通过查询对应的 **CancellationToken** 的 **IsCancellationRequested** 属性，检测到它应该停止正在做的事情。这两个实例成员内部通过一些特殊的线程同步代码来协调两个线程。①

① 具体地说，两个成员访问的字段被标记为 **volatile**，这是本章稍后要讨论的一个概念。
