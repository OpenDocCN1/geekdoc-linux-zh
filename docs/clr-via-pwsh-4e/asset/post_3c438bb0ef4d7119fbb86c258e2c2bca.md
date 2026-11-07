
任何静态成员。这是因为静态成员总是在调用 AppDomain 的上下文中访问。要切换到哪个 AppDomain 的信息包含在代理对象中，但调用静态成员时没有代理对象，所以不会发生 AppDomain 的切换。让类型的静态成员在一个 AppDomain 中执行，实例成员却在另一个 AppDomain 中执行，这样的编程模型未免太“丑”了！

由于第二个 AppDomain 中没有根，所以代理引用的原始对象可以被垃圾回收。这当然不理想。但另一方面，假如将原始对象不确定地(indefinitely)留在内存中，代理可能不再引用它，而原始对象依然存活；这同样不理想。CLR 解决这个问题的办法是使用一个“租约管理器”(lease manager)。一个对象的代理创建好之后，CLR 保持对象存活 5 分钟。5 分钟内没有通过代理发出调用，对象就会失效，下次垃圾回收会释放它的内存。每发出一次对对象的调用，“租约管理器”都会续订对象的租期，保证它在接下来的 2 分钟内在内存中保持存活。在对象过期后试图通过代理调用它，CLR 会抛出 System.Runtime.Remoting.RemotingException 异常。

默认的 5 分钟和 2 分钟租期设定是可以修改的，重写 MarshalByRefObject 的虚方法 InitializeLifetimeService 即可。详情参见文档的“生存期租约”主题。

## 演示 2：使用“按值封送”进行跨 AppDomain 通信

演示 2 与演示 1 很相似。和演示 1 一样，演示 2 也创建了新 AppDomain。然后调用 CreateInstanceAndUnwrap 方法将同一个程序集加载到新建 AppDomain 中，并在这个新 AppDomain 中创建 MarshalByRefType 类型的实例。CLR 为这个对象创建代理，mbrt 变量(在默认 AppDomain 中)被初始化成引用这个代理。接着用代理调用 MethodWithReturn 方法。这个方法是无参的，将在新 AppDomain 中执行以创建 MarshalByValType 类型的实例，并将一个对象引用返回给默认 AppDomain。

MarshalByValType 不从 System.MarshalByRefObject 派生，所以 CLR 不能定义一个代理类型并创建代理类型的实例；对象不能按引用跨 AppDomain 边界进行封送。

但由于 MarshalByValType 标记了自定义特性[Serializable]，所以 MethodWithReturn 方法能按值封送对象。下面具体描述了将一个对象按值从一个 AppDomain(源 AppDomain)封送到另一个 AppDomain(目标 AppDomain)的含义。欲知 CLR 序列化和反序列化的详情，请参见第 24 章“运行时序列化”。

源 AppDomain 想向目标 AppDomain 发送或返回一个对象引用时，CLR 将对象的实例字段序列化成一个字节数组。字节数组从源 AppDomain 复制到目标 AppDomain。然后，CLR 在目标 AppDomain 中反序列化字节数组，这会强制 CLR 将定义了“被反序列化的类型”的程序集加载到目标 AppDomain 中(如果尚未加载的话)。接着，CLR 创建类型的实例，并利用字节数组中的值初始化对象的字段，使之与源对象中的值相同。换言之，CLR 在目标 AppDomain 中精确复制了源对象。然后，MethodWithReturn 方法返回对这个副本的引用；这样一来，对象就跨 AppDomain 的边界按值封送了。

- 3. 当第 2 步发现的所有线程都离开 AppDomain 后，CLR 遍历堆，为引用了“由已卸载的 AppDomain 创建的对象”的每个代理对象都设置一个标志(flag)。这些代理对象现在知道它们引用的真实对象已经不在了。现在，任何代码在无效的代理对象上调用方法都会抛出一个 **AppDomainUnloadedException** 异常。
- 4. CLR 强制垃圾回收，回收由已卸载的 AppDomain 创建的任何对象的内存。这些对象的 **Finalize** 方法被调用，使对象有机会正确清理它们占用的资源。
- 5. CLR 恢复剩余所有线程的执行。调用 **AppDomain.Unload** 方法的线程将继续运行；对 **AppDomain.Unload** 的调用是同步进行的。①

① 换言之，一旦调用 Unload，只有在它返回之后，线程才能恢复运行。——译注

在 Ch22-1-AppDomains 应用程序中，所有工作都用一个线程来做。因此，任何时候只要调用 **AppDomain.Unload**，都不可能有另一个线程在要卸载的 AppDomain 中。因此，CLR 不必抛出任何 **ThreadAbortException** 异常。本章后面将进一步讨论 **ThreadAbortException**。

顺便说一句，当一个线程调用 **AppDomain.Unload** 方法时，针对要卸载的 AppDomain 中的线程，CLR 会给它们 10 秒钟的时间离开。10 秒钟后，如果调用 **AppDomain.Unload** 方法的线程还没有返回，CLR 将抛出一个 **CannotUnloadAppDomainException** 异常，AppDomain 将来可能会、也可能不会卸载。

![](img/6fa065e17c4549db7260fbfaf4fd384e_521_0.png)

> **注意**　如果调用 **AppDomain.Unload** 方法的线程不在要卸载的 AppDomain 中，CLR 会创建另一个线程来尝试卸载 AppDomain。第一个线程被强制抛出 **ThreadAbortException** 并展开 (unwind)。新线程将等待 AppDomain 卸载，然后新线程会终止。如果 AppDomain 卸载失败，新线程将抛出 **CannotUnloadAppDomainException** 异常。但是，由于我们没有写由新线程执行的代码，所以无法捕捉这个异常。

## 22.4 监视 AppDomain

宿主应用程序可监视 AppDomain 消耗的资源。有的宿主根据这种信息判断一个 AppDomain 的内存或 CPU 消耗是否超过了应有的水准，并强制卸载一个 AppDomain。还可利用监视来比较不同算法的资源消耗情况，判断哪一种算法用的资源较少。由于 AppDomain 监视本身也会产生开销，所以宿主必须将 AppDomain 的静态 **MonitoringEnabled** 属性设为 **true**，从而显式地打开监视。监视一旦打开便不能关闭，将 **MonitoringEnabled** 属性设为 **false** 会抛出一个 **ArgumentException** 异常。

监视打开后，代码可查询 **AppDomain** 类提供的以下 4 个只读属性。

- **MonitoringSurvivedProcessMemorySize**　这个 **Int64** 静态属性返回由当前 CLR 实例控制的所有 AppDomain 使用的字节数。这个数字只保证在上一次垃圾回收时是准确的。
- **MonitoringTotalAllocatedMemorySize** 这个 **Int64** 实例属性返回特定 **AppDomain** 已分配的字节数。这个数字只保证在上一次垃圾回收时是准确的。
- **MonitoringSurvivedMemorySize** 这个 **Int64** 实例属性返回特定 **AppDomain** 当前正在使用的字节数。这个数字只保证在上一次垃圾回收时是准确的。
- **MonitoringTotalProcessorTime** 这个 **TimeSpan** 实例属性返回特定 **AppDomain** 的 CPU 占用率。

下面这个类演示了如何利用这些属性检查两个时间点之间一个 AppDomain 发生的变化：

```csharp
private sealed class AppDomainMonitorDelta : IDisposable {
    private AppDomain m_appDomain;
    private TimeSpan m_thisADCpu;
    private Int64 m_thisADMemoryInUse;
    private Int64 m_thisADMemoryAllocated;

    static AppDomainMonitorDelta() {
        // 确定已打开了 AppDomain 监视
        AppDomain.MonitoringIsEnabled = true;
    }

    public AppDomainMonitorDelta(AppDomain ad) {
        m_appDomain = ad ?? AppDomain.CurrentDomain;
        m_thisADCpu = m_appDomain.MonitoringTotalProcessorTime;
        m_thisADMemoryInUse = m_appDomain.MonitoringSurvivedMemorySize;
        m_thisADMemoryAllocated = m_appDomain.MonitoringTotalAllocatedMemorySize;
    }

    public void Dispose() {
        GC.Collect();
        Console.WriteLine("FriendlyName={0}, CPU={1}ms", m_appDomain.FriendlyName,
            (m_appDomain.MonitoringTotalProcessorTime - m_thisADCpu).TotalMilliseconds);
        Console.WriteLine("   Allocated {0:N0} bytes of which {1:N0} survived GCs",
            m_appDomain.MonitoringTotalAllocatedMemorySize - m_thisADMemoryAllocated,
            m_appDomain.MonitoringSurvivedMemorySize - m_thisADMemoryInUse);
    }
}
```

以下代码演示了如何使用 **AppDomainMonitorDelta** 类：

```csharp
private static void AppDomainResourceMonitoring() {
    using (new AppDomainMonitorDelta(null)) {
        // 分配在回收时能存活的约 10MB
        var list = new List<Object>();
        for (Int32 x = 0; x < 1000; x++) list.Add(new Byte[10000]);

        // 分配在回收时存活不了的约 20MB
        for (Int32 x = 0; x < 2000; x++) new Byte[10000].GetType();

        // 保持 CPU 工作约 5 秒
        Int64 stop = Environment.TickCount + 5000;
        while (Environment.TickCount < stop) ;
    }
}
```

在我的机器上运行以上代码，得到以下输出：①

```text
FriendlyName=03-Ch22-1-AppDomains.exe, CPU=5031.25ms
    Allocated 30,159,496 bytes of which 10,085,080 survived GCs
```

① 在本书配套代码中，找到C22-1 AppDomains项目，在Main()方法中注释掉Marshalling()和FieldAccessTiming()方法调用，然后解除对 AppDomainResourceMonitoring()调用的注释。——译注

## 22.5 AppDomain FirstChance 异常通知

每个 **AppDomain** 都可关联一组回调方法；CLR 开始查找 **AppDomain** 中的 **catch** 块时，这些回调方法将得以调用。可用这些方法执行日志记录操作。另外，宿主可利用这个机制监视 **AppDomain** 中抛出的异常。回调方法不能处理异常，也不能以任何方式“吞噬”异常(装作异常没有发生)；它们只是接收关于异常发生的通知。要登记回调方法，为 **AppDomain** 的实例事件 **FirstChanceException** 添加一个委托就可以了。

下面描述了 CLR 如何处理异常：异常首次抛出时，CLR 调用向抛出异常的 **AppDomain** 登记的所有 **FirstChanceException** 回调方法。然后，CLR 查找栈上在同一个 **AppDomain** 中的任何 **catch** 块。有一个 **catch** 块能处理异常，则异常处理完成，将继续正常执行。如果 **AppDomain** 中没有一个 **catch** 块能处理异常，则 CLR 沿着栈向上来到调用 **AppDomain**，再次抛出同一个异常对象(序列化和反序列化之后)。这时感觉就像是抛出了一个全新的异常，CLR 调用向当前 **AppDomain** 登记的所有 **FirstChanceException** 回调方法。这个过程会一直持续，直到抵达线程栈顶部。届时如果异常还未被任何代码处理，CLR 只好终止整个进程。

## 22.6 宿主如何使用 AppDomain

前面已讨论了宿主以及宿主加载 CLR 的方式。同时还讨论了宿主如何告诉 CLR 创建和卸载 **AppDomain**。为了使这些讨论更加具体，下面将描述一些常见的寄宿和 **AppDomain** 使用情形。我着重解释了不同应用程序类型如何寄宿(容纳)CLR，以及如何管理 **AppDomain**。

### 22.6.1 可执行应用程序

控制台 UI 应用程序、NT Service 应用程序、Windows 窗体应用程序和 Windows Presentation Foundation(WPF)应用程序都是自寄宿(self-hosted，即自己容纳 CLR)的应用程序，它们都有托管 EXE 文件。Windows 用托管 EXE 文件初始化进程时，会加载垫片②。垫片检查应用程序的程序集(EXE 文件)中的 CLR 头信息。头信息指明了生成和测试应用程序时使用的 CLR 版本。垫片根据这些信息决定将哪个版本的 CLR 加载到进程中，CLR 加载并初始化好之后，会再次检查程序集的 CLR 头，判断哪个方法是应用程序的入口方法(**Main**)。CLR 调用该方法。

② 垫片的问题请参见 22.1 节“CLR 寄宿”。——译注

应用程序需要的程序集都会加载到一个单独的 AppDomain 中，以隔离不同 Web 应用程序的代码和对象。

ASP.NET 的一个亮点是允许在不关闭 Web 服务器的前提下动态更改网站代码。网站的文件在硬盘上发生改动时，ASP.NET 会检测到这个情况，并卸载包含旧版本文件的 AppDomain(在当前运行的最后一个请求完成之后)，并创建一个新 AppDomain，向其中加载新版本的文件。为了确保这个过程的顺利进行，ASP.NET 使用了 AppDomain 的一个名为“影像复制①” (shadow copying)的功能。

### 22.6.4 Microsoft SQL Server

Microsoft SQL Server 是非托管应用程序，它的大部分代码仍是用非托管 C++写的。SQL Server 允许开发人员使用托管代码创建存储过程。首次请求数据库运行一个用托管代码写的存储过程时，SQL Server 会加载 CLR。存储过程在它们自己的安全 AppDomain 中运行，这避免了存储过程对数据库服务器产生负面影响。

这其实是一项非同寻常的功能！它意味着开发人员可以选择自己喜欢的编程语言来编写存储过程。存储过程可以在自己的代码中使用强类型的数据对象。代码还会被 JIT 编译成本机代码执行，而不是采用解释执行的方式。开发人员可利用 FCL 或任何其他程序集中定义的任何类型。结果是我们的工作变得越来越轻松，但应用程序的表现变得越来越好。作为开发人员，我表示很知足！

### 22.6.5 更多的用法只局限于想象力

生产型应用程序(比如字处理和电子表格软件)也允许用户使用任何编程语言来编写宏。宏可以访问与 CLR 一起运行的所有程序集和类型。宏会被编译，所以执行得更快。最重要的是，宏在一个安全 AppDomain 中运行，不会骚扰到用户。你自己的应用程序也可利用这个功能。具体怎么用，只局限于你自己的想象力。

## 22.7 高级宿主控制

本节探讨与寄宿 CLR 有关的高级话题。目的是让你有一个初步的认识，帮你更多地理解 CLR 的能力。如果有兴趣，鼓励你参考其他更有针对性的参考书。

### 22.7.1 使用托管代码管理 CLR

**System.AppDomainManager** 类允许宿主使用托管代码(而不是非托管代码)覆盖 CLR 的默认行为。当然，使用托管代码使宿主的实现变得更容易。你唯一要做的就是定义自己的类，让它从 **System.AppDomainManager** 派生，重写想接手控制的任何虚方法。然后，在专用的程序集中生成类，并将程序集安装到 GAC 中。这是由于该程序集需要被授予完全信任权限，而 GAC 中的所有程序集都总是被授予完全信任权限。

然后要告诉 CLR 使用你的 **AppDomainManager** 派生类。在代码中，最佳的方法就是创建一个 **AppDomainSetup** 对象，初始化它的 **AppDomainManagerAssembly** 和 **AppDomainManagerType** 属性（均为 **String** 类型）。将前者设为定义了你的 **AppDomainManager** 派生类的那个程序集的强名称字符串，后者设为你的 **AppDomainManager** 派生类的全名。还可在应用程序 XML 配置文件中，用 **appDomainManagerAssembly** 和 **appDomainManagerType** 元素来设置 **AppDomainManager**。此外，本机宿主可查询 **ICLRControl** 接口，调用该接口的 **SetAppDomainManagerType** 函数，向它传递 GAC 安装的程序集的标识和 **AppDomainManager** 派生类的名称。

现在看看 **AppDomainManager** 派生类能做什么。**AppDomainManager** 派生类的作用是使宿主保持控制权，即使是在加载项（add-in）试图创建自己的 AppDomain 时。进程中的代码试图创建新 AppDomain 时，那个 AppDomain 中的 **AppDomainManager** 派生对象可修改安全性和配置设置。它还可决定阻止一次 AppDomain 创建，或返回对现有 AppDomain 的引用。新 AppDomain 创建好之后，CLR 会在其中创建新的 **AppDomainManager** 派生对象。这个对象也能修改配置设置、决定执行上下文如何在线程之间切换，并决定向程序集授予的权限。

### 22.7.2 写健壮的宿主应用程序

托管代码出现错误时，宿主可告诉 CLR 采取什么行动。下面是一些例子（按严重性从低到高排序）。

- 如果线程执行时间过长，CLR 可终止线程并返回一个响应。（下一节会更多地讨论这个问题。）
- CLR 可卸载 AppDomain。这会终止该 AppDomain 中的所有线程，导致有问题的代码卸载。
- CLR 可被禁用。这会阻止更多的托管代码在程序中运行，但仍然允许非托管代码运行。
- CLR 可退出 Windows 进程。首先会终止所有线程，并卸载所有 AppDomain，使资源清理操作得以执行，然后才会终止进程。

CLR 可以得体地（gracefully）或者粗鲁地（rudely）终止线程或 AppDomain。得体意味着会执行（资源）清理代码。换言之，finally 块中的代码会运行，对象的 Finalize 方法也将被执行。而

① 还可使用环境变量和注册表设置来配置一个 **AppDomainManager**。但这些机制比正文描述的方法麻烦得多。除非是在一些测试性的场合中，否则应避免使用。
