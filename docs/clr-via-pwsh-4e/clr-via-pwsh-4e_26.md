## 第二十二章 CLR 寄宿和 AppDomain

**本章内容：**

- CLR 寄宿
- AppDomain
- 卸载 AppDomain
- 监视 AppDomain
- AppDomain FirstChance 异常通知
- 宿主如何使用 AppDomain
- 高级宿主控制

本章主要讨论两个主题：寄宿和 AppDomain。这两个主题充分演示了 Microsoft .NET Framework 的巨大价值。寄宿(hosting)使任何应用程序都能利用 CLR 的功能。特别要指出的是，它使现有的应用程序至少能部分使用托管代码编写。另外，寄宿还为应用程序提供了通过编程来进行自定义和扩展的能力。

允许可扩展性意味着第三方代码可在你的进程中运行。在 Windows 中将第三方 DLL 加载到进程中意味着冒险。DLL 中的代码很容易破坏应用程序的数据结构和代码。DLL 还可能企图利用应用程序的安全上下文来访问它本来无权访问的资源。CLR 的 AppDomain 功能解决了所有这些问题。AppDomain 允许第三方的、不受信任的代码在现有的进程中运行，而 CLR 保证数据结构、代码和安全上下文不被滥用或破坏。

程序员经常将寄宿和 AppDomain 与程序集的加载和反射一起使用。这 4 种技术一起使用，使 CLR 成为一个功能极其丰富和强大的平台。本章重点在于寄宿和 AppDomain。下一章则会将重点放在程序集加载和反射上。学习并理解了所有这些技术后，会发现今天在.NET Framework 上面的投资，将来必会获得丰厚回报。

### 22.1 CLR 寄宿

.NET Framework 在 Windows 平台的顶部运行。这意味着.NET Framework 必须用 Windows 能理解的技术来构建。首先，所有托管模块和程序集文件都必须使用 Windows PE 文件格式，而且要么是 Windows EXE 文件，要么是 DLL 文件。

开发 CLR 时，Microsoft 实际是把它实现成包含在一个 DLL 中的 COM 服务器。也就是说，利用 **GetInterface** 方法获得 **ICLRRuntimeHost** 接口。宿主应用程序可调用该接口定义的方法来做下面这些事情。

> 注：本章描述的是 .NET Framework 的寄宿模型（`mscoree.dll`、`ICLRRuntimeHost` 等）。PowerShell 5.1 运行在 .NET Framework 上，这些接口仍然存在；PowerShell 7 运行在 .NET Core / .NET 5+ 上，托管入口改为 `hostfxr`/`nethost`，`ICLRRuntimeHost` 不可用，AppDomain 也只剩默认那一个（见 22.2 节的注释）。阅读本章时应把“CLR”具体化为宿主进程实际使用的运行时。

- 设置宿主管理器。告诉 **CLR** 宿主想参与涉及以下操作的决策：内存分配、线程调度/同步以及程序集加载等。宿主还可声明它想获得有关垃圾回收启动和停止以及特定操作超时的通知。
- 获取 **CLR** 管理器。告诉 **CLR** 阻止使用某些类/成员。另外，宿主能分辨哪些代码可以调试，哪些不可以，以及当特定事件(例如 AppDomain 卸载、CLR 停止或者堆栈溢出异常)发生时宿主应调用哪个方法。
- 初始化并启动 **CLR**。
- 加载程序集并执行其中的代码。
- 停止 **CLR**，阻止任何更多的托管代码在 **Windows** 进程中运行。

> **注意** Windows 进程完全可以不加载 CLR，只有在进程中执行托管代码时才进行加载。在 .NET Framework 4 之前，CLR 只允许它的一个实例寄宿在 Windows 进程中。换言之，在一个进程中，要么不包含任何 CLR，要么只能包含 CLR v1.0，CLR v1.1 或者 CLR 2.0 之一。每进程仅一个版本的 CLR 显然过于局限。例如，这样 Microsoft Office Outlook 就不能加载为不同版本的 .NET Framework 生成和测试的两个加载项了。
>
> 但是，随着 .NET Framework 4 的发布，Microsoft 支持在一个 Windows 进程中同时加载 CLR v2.0 和 v4.0，为 .NET Framework 2.0 和 4.0 写的不同组件能同时运行，不会出现任何兼容性问题。这是一个令人激动的功能，因为它极大扩展了 .NET Framework 组件的应用场合。可利用 ClrVer.exe 工具检查给定的进程加载的是哪个(哪些)版本的 CLR。
>
> 一个 CLR 加载到 Windows 进程之后，便永远不能卸载；在 **ICLRRuntimeHost** 接口上调用 **AddRef** 和 **Release** 方法是没有作用的。CLR 从进程中卸载的唯一途径就是终止进程，这会造成 Windows 清理进程使用的所有资源。

### 22.2 AppDomain

CLR COM 服务器初始化时会创建一个 AppDomain。AppDomain 是一组程序集的逻辑容器。CLR 初始化时创建的第一个 AppDomain 称为“默认 AppDomain”，这个默认的 AppDomain 只有在 Windows 进程终止时才会被销毁。

> 注：PowerShell 会话就运行在这唯一的默认 AppDomain 中。`[System.AppDomain]::CurrentDomain` 可取得它，`FriendlyName` 在 PowerShell 7 中返回 `pwsh`（Windows PowerShell 5.1 返回 `DefaultDomain`）。脚本无法创建辅助 AppDomain：`[System.AppDomain]::CreateDomain(...)` 在 .NET Core 上抛出 `PlatformNotSupportedException`（“Secondary AppDomains are not supported on this platform.”）。脚本级别需要隔离时，PowerShell 提供的是 `Start-Job`、`Start-ThreadJob` 和运行空间（runspace），它们都不是 AppDomain。

除了默认 AppDomain，正在使用非托管 COM 接口方法或托管类型方法的宿主还可要求 CLR 创建额外的 AppDomain。AppDomain 是为了提供隔离而设计的。下面总结了

> 注：原文在此处被截断。“下面总结了”之后本应列出 AppDomain 提供的隔离项（静态字段、类型对象、程序集加载上下文、安全设置等），该列表及图 22-1 的引导段落均已缺失，下文直接从图 22-1 的说明接续。

![](img/6fa065e17c4549db7260fbfaf4fd384e_509_0.png)

除此之外，每个 AppDomain 都加载了一些程序集。AppDomain #1（默认 AppDomain）有三个程序集：MyApp.exe，TypeLib.dll 和 System.dll。AppDomain #2 有两个程序集：Wintellect.dll 和 System.dll。

如图 22-1 所示，两个 AppDomain 都加载了 System.dll 程序集。如果这两个 AppDomain 都使用了来自 System.dll 的一个类型，那么两个 AppDomain 的 Loader 堆会为相同的类型分别分配一个类型对象；类型对象的内存不会由两个 AppDomain 共享。另外，一个 AppDomain 中的代码调用一个类型定义的方法时，方法的 IL 代码会进行 JIT 编译，生成的本机代码单独与每个 AppDomain 关联，而不是由调用它的所有 AppDomain 共享。

不共享类型对象的内存或本机代码显得有些浪费。但 AppDomain 的设计宗旨就是提供隔离；CLR 要求在卸载某个 AppDomain 并释放其所有资源时不会影响到其他任何 AppDomain。复制 CLR 的数据结构才能保证这一点。另外，还保证多个 AppDomain 使用的类型在每个 AppDomain 中都有一组静态字段。

有的程序集本来就要由多个 AppDomain 使用。最典型的例子就是 MSCorLib.dll。该程序集包含了 System.Object，System.Int32 以及其他所有与 .NET Framework 密不可分的类型。CLR 初始化时，该程序集会自动加载，而且所有 AppDomain 都共享该程序集中的类型。为了减少资源消耗，MSCorLib.dll 程序集以一种“AppDomain 中立”的方式加载。也就是说，针对以“AppDomain 中立”的方式加载的程序集，CLR 会为它们维护一个特殊的 Loader 堆。该 Loader 堆中的所有类型对象，以及为这些类型定义的方法 JIT 编译生成的所有本机代码，都会由进程中的所有 AppDomain 共享。遗憾的是，共享这些资源所获得的收益并不是没有代价的。这个代价就是，以“AppDomain 中立”的方式加载的所有程序集永远不能

> 注：原文在此处缺失了一大段正文：从“永远不能”到下面的演示代码之间，本应说明这类程序集为何不能被卸载、为何必须用强名称标识，以及演示 1（按引用封送）的完整步骤和 `Marshalling` 方法的开头。下面的代码块因此从演示 1 的中段（调用代理方法）开始，之后直接衔接演示 2、演示 3 的片段。

```csharp
// mbrt 引用一个有效的代理对象；代理对象引用一个无效的 AppDomain

try {
    // 在代理类型上调用一个方法。AppDomain 无效，造成抛出异常
    mbrt.SomeMethod();
    Console.WriteLine("Successful call.");
}
catch (AppDomainUnloadedException) {
    Console.WriteLine("Failed call.");
}

// *** DEMO 2: 使用 Marshal-by-Value 进行跨 AppDomain 通信 ***
Console.WriteLine("{0}Demo #2", Environment.NewLine);

// 新建一个 AppDomain（从当前 AppDomain 继承安全性和配置）
ad2 = AppDomain.CreateDomain("AD #2", null, null);

// 将我们的程序集加载到新 AppDomain 中，构造一个对象，把它
// 封送回我们的 AppDomain（实际得到对一个代理的引用）
mbrt = (MarshalByRefType)
    ad2.CreateInstanceAndUnwrap(exeAssembly, "MarshalByRefType");

// 对象的方法返回所返回对象的副本；
// 对象按值（而非按引用）封送
MarshalByValType mbvt = mbrt.MethodWithReturn();

// 证明得到的不是对一个代理对象的引用
Console.WriteLine("Is proxy={0}", RemotingServices.IsTransparentProxy(mbvt));

// 看起来是在 MarshalByValType 上调用一个方法，实际上也是如此
Console.WriteLine("Returned object created " + mbvt.ToString());

// 卸载新的 AppDomain
AppDomain.Unload(ad2);
// mbvt 引用有效的对象；卸载 AppDomain 没有影响

try {
    // 我们是在对象上调用一个方法；不会抛出异常
    Console.WriteLine("Returned object created " + mbvt.ToString());
    Console.WriteLine("Successful call.");
}
catch (AppDomainUnloadedException) {
    Console.WriteLine("Failed call.");
}

// *** DEMO 3: 使用不可封送的类型进行跨 AppDomain 通信 ***
Console.WriteLine("{0}Demo #3", Environment.NewLine);

// 新建一个 AppDomain（从当前 AppDomain 继承安全性和配置）
ad2 = AppDomain.CreateDomain("AD #2", null, null);
// 将我们的程序集加载到新 AppDomain 中，构造一个对象，把它
// 封送回我们的 AppDomain（实际得到对一个代理的引用）
mbrt = (MarshalByRefType)
    ad2.CreateInstanceAndUnwrap(exeAssembly, "MarshalByRefType");

// 对象的方法返回一个不可封送的对象；抛出异常
NonMarshalableType nmt = mbrt.MethodArgAndReturn(callingDomainName);
// 这里永远执行不到...
}

// 该类的实例可跨越 AppDomain 的边界“按引用封送”
public sealed class MarshalByRefType : MarshalByRefObject {
    public MarshalByRefType() {
        Console.WriteLine("{0} ctor running in {1}",
            this.GetType().ToString(), Thread.GetDomain().FriendlyName);
    }

    public void SomeMethod() {
        Console.WriteLine("Executing in " + Thread.GetDomain().FriendlyName);
    }

    public MarshalByValType MethodWithReturn() {
        Console.WriteLine("Executing in " + Thread.GetDomain().FriendlyName);
        MarshalByValType t = new MarshalByValType();
        return t;
    }

    public NonMarshalableType MethodArgAndReturn(String callingDomainName) {
        // 注意：callingDomainName 是可序列化的
        Console.WriteLine("Calling from '{0}' to '{1}'.",
            callingDomainName, Thread.GetDomain().FriendlyName);
        NonMarshalableType t = new NonMarshalableType();
        return t;
    }
}

// 该类的实例可跨越 AppDomain 的边界“按值封送”
[Serializable]
public sealed class MarshalByValType : Object {
    private DateTime m_creationTime = DateTime.Now; // 注意:DateTime 是可序列化的

    public MarshalByValType() {
        Console.WriteLine("{0} ctor running in {1}, Created on {2:D}",
            this.GetType().ToString(),
            Thread.GetDomain().FriendlyName,
            m_creationTime);
    }

    public override String ToString() {
        return m_creationTime.ToLongDateString();
    }
}

// 该类的实例不能跨 AppDomain 边界进行封送
// [Serializable]
public sealed class NonMarshalableType : Object {
    public NonMarshalableType() {
        Console.WriteLine("Executing in " + Thread.GetDomain().FriendlyName);
    }
}
```

生成并运行 Ch22-1-AppDomains 应用程序，获得以下输出结果：①

① 在本书配套代码中，找到 C22-1 AppDomains 项目，在 Main()方法中解除对 Marshalling()方法调用的注释。——译注

```text
Default AppDomain's friendly name=Ch22-1-AppDomains.exe
Main assembly=Ch22-1-AppDomains, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null

Demo #1
MarshalByRefType ctor running in AD #2
Type=MarshalByRefType
Is proxy=True
Executing in AD #2
Failed call.

Demo #2
MarshalByRefType ctor running in AD #2
Executing in AD #2
MarshalByValType ctor running in AD #2, Created on 2014 年 5 月 14 日
Is proxy=False
Returned object created 2014 年 5 月 14 日
Returned object created 2014 年 5 月 14 日
Successful call.

Demo #3
MarshalByRefType ctor running in AD #2
Calling from 'Ch22-1-AppDomains.exe' to 'AD #2'.
Executing in AD #2

未经处理的异常： System.Runtime.Serialization.SerializationException: 程序集“Ch22-1-AppDomains, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null”中的类型“NonMarshalableType”未标记为可序列化。
   在 MarshalByRefType.MethodArgAndReturn(String callingDomainName)
   在 Program.Marshalling()
   在 Program.Main()
```

> 注：跨 AppDomain 的“按引用封送/按值封送”依赖 .NET Remoting（`System.Runtime.Remoting`），该技术在 .NET Core / PowerShell 7 中已被移除。`MarshalByRefObject` 类型本身仍在，但透明代理、`CreateInstanceAndUnwrap`、`RemotingServices.IsTransparentProxy` 都不再可用，上述演示只能在 PowerShell 5.1（.NET Framework）上运行。

现在来讨论以上代码以及 CLR 所做的事情。

Marshalling 方法首先获得一个 AppDomain 对象引用，当前调用线程正在该 AppDomain 中执行。在 Windows 中，线程总是在一个进程的上下文中创建，而且线程的整个生存期都在该进程的生存期内。但线程和 AppDomain 没有一对一关系。AppDomain 是一项 CLR 功能；Windows 对 AppDomain 一无所知。由于一个 Windows 进程可包含多个 AppDomain，所以线程能执行一个 AppDomain 中的代码，再执行另一个 AppDomain 中的代码。从 CLR 的角度看，线程一次只能执行一个 AppDomain 中的代码。线程可调用 System.Threading.Thread 的静态方法 GetDomain 向 CLR 询问它正在哪个 AppDomain 中执行。线程还可查询 System.AppDomain 的静态只读属性 CurrentDomain 获得相同的信息。

AppDomain 创建后可被赋予一个友好名称。它是用于标识 AppDomain 的一个 String。友好名称主要是为了方便调试。由于 CLR 要在我们的任何代码执行前创建默认 AppDomain，所以使用可执行文件的文件名作为默认的 AppDomain 友好名称。Marshalling 方法使用 System.AppDomain 的只读 FriendlyName 属性来查询默认 AppDomain 的友好名称。

接着，Marshalling 方法查询默认 AppDomain 中加载的程序集的强命名标识，这个程序集定义了入口方法 Main(其中调用了 Marshalling)。程序集定义了几个类型：Program、MarshalByRefType、MarshalByValType 和 NonMarshalableType。现在已准备好研究上

> 注：原文在此处被截断，“现在已准备好研究上”之后缺失了演示 1 的说明（新建 AppDomain、调用 `CreateInstanceAndUnwrap`、CLR 为 `MarshalByRefType` 生成透明代理等）。下文直接从“有两个办法可证明调用线程已从默认 AppDomain 切换至新 AppDomain”接续。

有两个办法可证明调用线程已从默认 AppDomain 切换至新 AppDomain。首先，我在 SomeMethod 方法中调用了 Thread.GetDomain().FriendlyName。这将返回“AD #2”(参见输出)，这是由于线程当前在新 AppDomain 中运行，而这个新 AppDomain 是通过调用 AppDomain.CreateDomain 方法，并传递“AD #2”作为友好名称参数来创建的。其次，在调试器中逐语句调试代码，并打开了“调用堆栈”窗口，那么“[外部代码]”行会标注一个线程在什么位置跨越 AppDomain 边界。请参见图 22-2 底部的“调用堆栈”窗口。

![](img/6fa065e17c4549db7260fbfaf4fd384e_516_0.png)

图 22-2 调试器的“调用堆栈”窗口显示了一次 AppDomain 切换

真实的 SomeMethod 方法返回后，会返回至代理的 SomeMethod 方法，后者将线程切换回默认 AppDomain。线程继续执行默认 AppDomain 中的代码。

> **注意** 一个 AppDomain 中的线程调用另一个 AppDomain 中的方法时，线程会在这两个 AppDomain 之间切换。这意味着跨 AppDomain 边界的方法调用是同步执行的①。任何时刻一个线程只能在一个 AppDomain 中，而且要用那个 AppDomain 的安全和配置设置来执行代码。如果希望多个 AppDomain 中的代码并发执行，应创建额外的线程，让这些线程在你希望的 AppDomain 中执行你希望的代码。

① 一个 AppDomain 的方法执行完毕，才能执行另一个 AppDomain 的方法。不能多个 AppDomain 的代码并发执行。——译注

Ch22-1-AppDomains 应用程序接着做的事情是调用 AppDomain 类的公共静态 Unload 方法，这会强制 CLR 卸载指定的 AppDomain(包括加载到其中的所有程序集)，并强制执行一次垃圾回收，以释放由卸载的 AppDomain 中的代码创建的所有对象。这时，默认 AppDomain 的 mbrt 变量仍然引用一个有效的代理对象。但代理对象已不再引用一个有效的 AppDomain(因为它已经卸载了)。

当默认 AppDomain 试图使用代理对象调用 SomeMethod 方法时，调用的是该方法在代理中的实现。代理的实现发现包含真实对象的 **AppDomain** 已卸载。所以，代理的 **SomeMethod** 方法抛出一个 **AppDomainUnloadedException** 异常，告诉调用者操作无法完成。

显然，Microsoft 的 CLR 团队不得不做大量的工作来确保 AppDomain 的正确隔离，但这是他们必须做的。跨 AppDomain 访问对象的功能正在被大量地使用，开发人员对这个功能的依赖性正在日益增加。不过，使用“按引用封送”的语义进行跨 AppDomain 边界的对象访问，会产生一些性能上的开销。所以，一般应尽量少用这个功能。

前面我承诺会更多地讨论实例字段。从 **MarshalByRefObject** 派生的类型可定义实例字段。但这些实例字段不会成为代理类型的一部分，也不会包含在代理对象中。写代码对派生自 **MarshalByRefObject** 的类型的实例字段进行读写时，JIT 编译器会自动生成代码，分别调用 **System.Object** 的 **FieldGetter** 方法(用于读)或 **FieldSetter** 方法(用于写)来使用代理对象(以找到真正的 AppDomain/对象)。这些方法是私有的，而且没有在文档中记录。简单地说，这些方法利用反射机制获取或设置字段值。因此，虽然能访问派生自 **MarshalByRefObject** 的一个类型中的字段，但性能很差，因为 CLR 最终要调用方法来执行字段访问。事实上，即使要访问的字段在你自己的 AppDomain 中，性能也好不到哪里去。①

① 如果 CLR 要求所有字段都必须私有(为了获得好的数据封装，我强烈建议这样做)，那么 **FieldGetter** 和 **FieldSetter** 方法根本没有存在的必要，从方法中总是能够直接访问字段，避免(因为还要经由中间的 getter 或 setter 方法)造成性能损失。

#### 访问实例字段时的性能问题

我用以下代码演示性能损失的程度：

```csharp
private sealed class NonMBRO : Object { public Int32 x; }
private sealed class MBRO : MarshalByRefObject { public Int32 x; }

private static void FieldAccessTiming() {
    const Int32 count = 100000000;
    NonMBRO nonMbro = new NonMBRO();
    MBRO mbro = new MBRO();

    Stopwatch sw = Stopwatch.StartNew();
    for (Int32 c = 0; c < count; c++) nonMbro.x++;
    Console.WriteLine("{0}", sw.Elapsed); // 00:00:00.4073560

    sw = Stopwatch.StartNew();
    for (Int32 c = 0; c < count; c++) mbro.x++;
    Console.WriteLine("{0}", sw.Elapsed); // 00:00:02.5388665
}
```

我运行以上代码，访问从 Object 派生的 NonMBRO 类的实例字段只花了约 0.4 秒，但访问从 MarshalByRefObject 派生的 MBRO 类的实例字段却花了 2.54 秒。也就是说，访问从 MarshalByRefObject 派生的一个类的实例字段要多花约 6 倍的时间！

从好不好用(usability)的角度说，派生自 **MarshalByRefObject** 的类型真的应该避免定义任何静态成员。这是因为静态成员总是在调用 AppDomain 的上下文中访问。要切换到哪个 AppDomain 的信息包含在代理对象中，但调用静态成员时没有代理对象，所以不会发生 AppDomain 的切换。让类型的静态成员在一个 AppDomain 中执行，实例成员却在另一个 AppDomain 中执行，这样的编程模型未免太“丑”了！

由于第二个 AppDomain 中没有根，所以代理引用的原始对象可以被垃圾回收。这当然不理想。但另一方面，假如将原始对象不确定地(indefinitely)留在内存中，代理可能不再引用它，而原始对象依然存活；这同样不理想。CLR 解决这个问题的办法是使用一个“租约管理器”(lease manager)。一个对象的代理创建好之后，CLR 保持对象存活 5 分钟。5 分钟内没有通过代理发出调用，对象就会失效，下次垃圾回收会释放它的内存。每发出一次对对象的调用，“租约管理器”都会续订对象的租期，保证它在接下来的 2 分钟内在内存中保持存活。在对象过期后试图通过代理调用它，CLR 会抛出 System.Runtime.Remoting.RemotingException 异常。

默认的 5 分钟和 2 分钟租期设定是可以修改的，重写 MarshalByRefObject 的虚方法 InitializeLifetimeService 即可。详情参见文档的“生存期租约”主题。

#### 演示 2：使用“按值封送”进行跨 AppDomain 通信

演示 2 与演示 1 很相似。和演示 1 一样，演示 2 也创建了新 AppDomain。然后调用 CreateInstanceAndUnwrap 方法将同一个程序集加载到新建 AppDomain 中，并在这个新 AppDomain 中创建 MarshalByRefType 类型的实例。CLR 为这个对象创建代理，mbrt 变量(在默认 AppDomain 中)被初始化成引用这个代理。接着用代理调用 MethodWithReturn 方法。这个方法是无参的，将在新 AppDomain 中执行以创建 MarshalByValType 类型的实例，并将一个对象引用返回给默认 AppDomain。

MarshalByValType 不从 System.MarshalByRefObject 派生，所以 CLR 不能定义一个代理类型并创建代理类型的实例；对象不能按引用跨 AppDomain 边界进行封送。

但由于 MarshalByValType 标记了自定义特性[Serializable]，所以 MethodWithReturn 方法能按值封送对象。下面具体描述了将一个对象按值从一个 AppDomain(源 AppDomain)封送到另一个 AppDomain(目标 AppDomain)的含义。欲知 CLR 序列化和反序列化的详情，请参见第二十四章“运行时序列化”。

源 AppDomain 想向目标 AppDomain 发送或返回一个对象引用时，CLR 将对象的实例字段序列化成一个字节数组。字节数组从源 AppDomain 复制到目标 AppDomain。然后，CLR 在目标 AppDomain 中反序列化字节数组，这会强制 CLR 将定义了“被反序列化的类型”的程序集加载到目标 AppDomain 中(如果尚未加载的话)。接着，CLR 创建类型的实例，并利用字节数组中的值初始化对象的字段，使之与源对象中的值相同。换言之，CLR 在目标 AppDomain 中精确复制了源对象。然后，MethodWithReturn 方法返回对这个副本的引用；这样一来，对象就跨 AppDomain 的边界按值封送了。

### 22.3 卸载 AppDomain

> 注：原文在此处缺了 22.3 节的标题及开头正文，包括卸载过程的第 1、2 步（让线程离开 AppDomain 等），编号列表直接从第 3 步开始。

> 注：.NET Core / PowerShell 7 不支持卸载 AppDomain：`[System.AppDomain]::Unload($ad)` 会抛出 `PlatformNotSupportedException`（“Operation is not supported on this platform.”），后文涉及的 `ThreadAbortException`、`CannotUnloadAppDomainException` 在 .NET Core 上也不可用。本节内容只适用于 PowerShell 5.1（.NET Framework）。

- 3. 当第 2 步发现的所有线程都离开 AppDomain 后，CLR 遍历堆，为引用了“由已卸载的 AppDomain 创建的对象”的每个代理对象都设置一个标志(flag)。这些代理对象现在知道它们引用的真实对象已经不在了。现在，任何代码在无效的代理对象上调用方法都会抛出一个 **AppDomainUnloadedException** 异常。
- 4. CLR 强制垃圾回收，回收由已卸载的 AppDomain 创建的任何对象的内存。这些对象的 **Finalize** 方法被调用，使对象有机会正确清理它们占用的资源。
- 5. CLR 恢复剩余所有线程的执行。调用 **AppDomain.Unload** 方法的线程将继续运行；对 **AppDomain.Unload** 的调用是同步进行的。①

① 换言之，一旦调用 Unload，只有在它返回之后，线程才能恢复运行。——译注

在 Ch22-1-AppDomains 应用程序中，所有工作都用一个线程来做。因此，任何时候只要调用 **AppDomain.Unload**，都不可能有另一个线程在要卸载的 AppDomain 中。因此，CLR 不必抛出任何 **ThreadAbortException** 异常。本章后面将进一步讨论 **ThreadAbortException**。

顺便说一句，当一个线程调用 **AppDomain.Unload** 方法时，针对要卸载的 AppDomain 中的线程，CLR 会给它们 10 秒钟的时间离开。10 秒钟后，如果调用 **AppDomain.Unload** 方法的线程还没有返回，CLR 将抛出一个 **CannotUnloadAppDomainException** 异常，AppDomain 将来可能会、也可能不会卸载。

![](img/6fa065e17c4549db7260fbfaf4fd384e_521_0.png)

> **注意**　如果调用 **AppDomain.Unload** 方法的线程不在要卸载的 AppDomain 中，CLR 会创建另一个线程来尝试卸载 AppDomain。第一个线程被强制抛出 **ThreadAbortException** 并展开 (unwind)。新线程将等待 AppDomain 卸载，然后新线程会终止。如果 AppDomain 卸载失败，新线程将抛出 **CannotUnloadAppDomainException** 异常。但是，由于我们没有写由新线程执行的代码，所以无法捕捉这个异常。

### 22.4 监视 AppDomain

宿主应用程序可监视 AppDomain 消耗的资源。有的宿主根据这种信息判断一个 AppDomain 的内存或 CPU 消耗是否超过了应有的水准，并强制卸载一个 AppDomain。还可利用监视来比较不同算法的资源消耗情况，判断哪一种算法用的资源较少。由于 AppDomain 监视本身也会产生开销，所以宿主必须将 AppDomain 的静态 **MonitoringEnabled** 属性设为 **true**，从而显式地打开监视。监视一旦打开便不能关闭，将 **MonitoringEnabled** 属性设为 **false** 会抛出一个 **ArgumentException** 异常。

> 注：PowerShell 7 中 `[System.AppDomain]::CurrentDomain.MonitoringIsEnabled = $true` 可以执行，`MonitoringTotalAllocatedMemorySize`、`MonitoringSurvivedMemorySize`、`MonitoringTotalProcessorTime` 也能读取（实测可用）；但进程里只有当前这一个 AppDomain，静态的 `MonitoringSurvivedProcessMemorySize` 实测返回 `$null`。PowerShell 5.1 上这些成员按本章所述工作。把 `MonitoringIsEnabled` 设回 `$false` 同样会失败，PowerShell 7 中的错误消息是“Argument must be true.”。

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

① 在本书配套代码中，找到 C22-1 AppDomains 项目，在 Main()方法中注释掉 Marshalling()和 FieldAccessTiming()方法调用，然后解除对 AppDomainResourceMonitoring()调用的注释。——译注

### 22.5 AppDomain FirstChance 异常通知

每个 **AppDomain** 都可关联一组回调方法；CLR 开始查找 **AppDomain** 中的 **catch** 块时，这些回调方法将得以调用。可用这些方法执行日志记录操作。另外，宿主可利用这个机制监视 **AppDomain** 中抛出的异常。回调方法不能处理异常，也不能以任何方式“吞噬”异常(装作异常没有发生)；它们只是接收关于异常发生的通知。要登记回调方法，为 **AppDomain** 的实例事件 **FirstChanceException** 添加一个委托就可以了。

下面描述了 CLR 如何处理异常：异常首次抛出时，CLR 调用向抛出异常的 **AppDomain** 登记的所有 **FirstChanceException** 回调方法。然后，CLR 查找栈上在同一个 **AppDomain** 中的任何 **catch** 块。有一个 **catch** 块能处理异常，则异常处理完成，将继续正常执行。如果 **AppDomain** 中没有一个 **catch** 块能处理异常，则 CLR 沿着栈向上来到调用 **AppDomain**，再次抛出同一个异常对象(序列化和反序列化之后)。这时感觉就像是抛出了一个全新的异常，CLR 调用向当前 **AppDomain** 登记的所有 **FirstChanceException** 回调方法。这个过程会一直持续，直到抵达线程栈顶部。届时如果异常还未被任何代码处理，CLR 只好终止整个进程。

> 注：PowerShell 中可以订阅该事件：`$id = [System.AppDomain]::CurrentDomain.add_FirstChanceException({ param($sender, $e) ... })`，取消订阅用 `remove_FirstChanceException($id)`。实测 PowerShell 7 上可用，但 PowerShell 内部产生的异常会让回调触发多次，回调里只应做日志记录，且不能再抛异常。这只是通知，不改变脚本 `try/catch` 的处理结果。

### 22.6 宿主如何使用 AppDomain

前面已讨论了宿主以及宿主加载 CLR 的方式。同时还讨论了宿主如何告诉 CLR 创建和卸载 **AppDomain**。为了使这些讨论更加具体，下面将描述一些常见的寄宿和 **AppDomain** 使用情形。我着重解释了不同应用程序类型如何寄宿(容纳)CLR，以及如何管理 **AppDomain**。

### 22.6.1 可执行应用程序

控制台 UI 应用程序、NT Service 应用程序、Windows 窗体应用程序和 Windows Presentation Foundation(WPF)应用程序都是自寄宿(self-hosted，即自己容纳 CLR)的应用程序，它们都有托管 EXE 文件。Windows 用托管 EXE 文件初始化进程时，会加载垫片②。垫片检查应用程序的程序集(EXE 文件)中的 CLR 头信息。头信息指明了生成和测试应用程序时使用的 CLR 版本。垫片根据这些信息决定将哪个版本的 CLR 加载到进程中，CLR 加载并初始化好之后，会再次检查程序集的 CLR 头，判断哪个方法是应用程序的入口方法(**Main**)。CLR 调用该方法。

② 垫片的问题请参见 22.1 节“CLR 寄宿”。——译注

> 注：Windows PowerShell 的 `powershell.exe` 是 .NET Framework 托管 EXE，走文中描述的垫片（shim）机制；PowerShell 7 的 `pwsh.exe` 运行在 .NET Core 上，由 apphost + `hostfxr` 启动运行时，不再经过 Windows 垫片，也不读取程序集里的 CLR 版本头来决定运行时版本（版本由 `runtimeconfig.json` 决定）。

### 22.6.2 Microsoft ASP.NET

> 注：原文在此处缺了 22.6.2 的标题和开头正文（ASP.NET 如何为每个 Web 应用程序创建独立 AppDomain 等），下面的段落直接从图/小节的中段开始。

应用程序需要的程序集都会加载到一个单独的 AppDomain 中，以隔离不同 Web 应用程序的代码和对象。

ASP.NET 的一个亮点是允许在不关闭 Web 服务器的前提下动态更改网站代码。网站的文件在硬盘上发生改动时，ASP.NET 会检测到这个情况，并卸载包含旧版本文件的 AppDomain(在当前运行的最后一个请求完成之后)，并创建一个新 AppDomain，向其中加载新版本的文件。为了确保这个过程的顺利进行，ASP.NET 使用了 AppDomain 的一个名为“影像复制①” (shadow copying)的功能。

> 注：原文此处还缺了 22.6.3 节（内容涉及 Microsoft Internet Explorer 通过 `AppDomainManager` 为托管加载项建立隔离的机制）的标题和全部正文，因此下文直接跳到 22.6.4。

### 22.6.4 Microsoft SQL Server

Microsoft SQL Server 是非托管应用程序，它的大部分代码仍是用非托管 C++写的。SQL Server 允许开发人员使用托管代码创建存储过程。首次请求数据库运行一个用托管代码写的存储过程时，SQL Server 会加载 CLR。存储过程在它们自己的安全 AppDomain 中运行，这避免了存储过程对数据库服务器产生负面影响。

这其实是一项非同寻常的功能！它意味着开发人员可以选择自己喜欢的编程语言来编写存储过程。存储过程可以在自己的代码中使用强类型的数据对象。代码还会被 JIT 编译成本机代码执行，而不是采用解释执行的方式。开发人员可利用 FCL 或任何其他程序集中定义的任何类型。结果是我们的工作变得越来越轻松，但应用程序的表现变得越来越好。作为开发人员，我表示很知足！

### 22.6.5 更多的用法只局限于想象力

生产型应用程序(比如字处理和电子表格软件)也允许用户使用任何编程语言来编写宏。宏可以访问与 CLR 一起运行的所有程序集和类型。宏会被编译，所以执行得更快。最重要的是，宏在一个安全 AppDomain 中运行，不会骚扰到用户。你自己的应用程序也可利用这个功能。具体怎么用，只局限于你自己的想象力。

### 22.7 高级宿主控制

本节探讨与寄宿 CLR 有关的高级话题。目的是让你有一个初步的认识，帮你更多地理解 CLR 的能力。如果有兴趣，鼓励你参考其他更有针对性的参考书。

### 22.7.1 使用托管代码管理 CLR

**System.AppDomainManager** 类允许宿主使用托管代码(而不是非托管代码)覆盖 CLR 的默认行为。当然，使用托管代码使宿主的实现变得更容易。你唯一要做的就是定义自己的类，让它从 **System.AppDomainManager** 派生，重写想接手控制的任何虚方法。然后，在专用的程序集中生成类，并将程序集安装到 GAC 中。这是由于该程序集需要被授予完全信任权限，而 GAC 中的所有程序集都总是被授予完全信任权限。

> 注：`System.AppDomainManager`、GAC 和 `ICLRControl` 都只存在于 .NET Framework 的宿主模型中。.NET Core / PowerShell 7 不提供 `AppDomainManager`，也没有 GAC；PowerShell 7 的宿主定制走的是引擎 API、`InitialSessionState` 和运行空间，与本节机制无关。

然后要告诉 CLR 使用你的 **AppDomainManager** 派生类。在代码中，最佳的方法就是创建一个 **AppDomainSetup** 对象，初始化它的 **AppDomainManagerAssembly** 和 **AppDomainManagerType** 属性（均为 **String** 类型）。将前者设为定义了你的 **AppDomainManager** 派生类的那个程序集的强名称字符串，后者设为你的 **AppDomainManager** 派生类的全名。还可在应用程序 XML 配置文件中，用 **appDomainManagerAssembly** 和 **appDomainManagerType** 元素来设置 **AppDomainManager**。此外，本机宿主可查询 **ICLRControl** 接口，调用该接口的 **SetAppDomainManagerType** 函数，向它传递 GAC 安装的程序集的标识和 **AppDomainManager** 派生类的名称。

① 还可使用环境变量和注册表设置来配置一个 **AppDomainManager**。但这些机制比正文描述的方法麻烦得多。除非是在一些测试性的场合中，否则应避免使用。

现在看看 **AppDomainManager** 派生类能做什么。**AppDomainManager** 派生类的作用是使宿主保持控制权，即使是在加载项（add-in）试图创建自己的 AppDomain 时。进程中的代码试图创建新 AppDomain 时，那个 AppDomain 中的 **AppDomainManager** 派生对象可修改安全性和配置设置。它还可决定阻止一次 AppDomain 创建，或返回对现有 AppDomain 的引用。新 AppDomain 创建好之后，CLR 会在其中创建新的 **AppDomainManager** 派生对象。这个对象也能修改配置设置、决定执行上下文如何在线程之间切换，并决定向程序集授予的权限。

### 22.7.2 写健壮的宿主应用程序

托管代码出现错误时，宿主可告诉 CLR 采取什么行动。下面是一些例子（按严重性从低到高排序）。

- 如果线程执行时间过长，CLR 可终止线程并返回一个响应。（下一节会更多地讨论这个问题。）
- CLR 可卸载 AppDomain。这会终止该 AppDomain 中的所有线程，导致有问题的代码卸载。
- CLR 可被禁用。这会阻止更多的托管代码在程序中运行，但仍然允许非托管代码运行。
- CLR 可退出 Windows 进程。首先会终止所有线程，并卸载所有 AppDomain，使资源清理操作得以执行，然后才会终止进程。

CLR 可以得体地（gracefully）或者粗鲁地（rudely）终止线程或 AppDomain。得体意味着会执行（资源）清理代码。换言之，finally 块中的代码会运行，对象的 Finalize 方法也将被执行。而粗鲁地终止意味着清理代码不会执行。换言之，finally 块中的代码可能不会运行，对象的 Finalize 方法也可能不会执行。如果得体地终止，当前正在一个 catch 块或 finally 块中的线程无法终止。但如果粗鲁地终止，就能终止 catch 块或 finally 块中的线程。遗憾的是，非托管代码或者约束执行区（Constrained Execution Region，CER）中的线程完全无法终止。

宿主可设置所谓的升级策略（escalation policy），从而告诉 CLR 应该如何处理托管代码的错误。例如，SQL Server 就告诉 CLR 在执行托管代码时，假如遇到未处理的异常应该如何处理。线程遇到未经处理的异常时，CLR 首先尝试将该异常升级成一次得体的线程终止。如果线程在指定时间内没有终止，CLR 就尝试将得体的终止升级成粗鲁的终止。

刚才描述的是最常见的情况。但如果线程在一个临界区（critical region）遇到了未处理的异常，策略就有所不同。位于临界区的线程是指进入线程同步锁的线程，该锁必须由同一个线程释放（例如最初调用 Monitor.Enter 方法，调用 Mutex 的 WaitOne 方法，或者调用 ReaderWriterLock 的 AcquireReaderLock 或 AcquireWriteLock 方法的那个线程①）。成功等待一个 AutoResetEvent、ManualResetEvent 或者 Semaphore 不会造成线程进入临界区，因为另一个线程可通知这些同步对象。线程在临界区时，CLR 认为线程访问的数据是由同一个 AppDomain 中的多个线程共享的。毕竟，这才是导致线程跑去获取一个锁的原因。直接终止正在访问共享数据的线程是不合适的，因为其他线程随后得到的就可能是已损坏的数据，造成 AppDomain 的运行变得无法预测，甚至可能留下安全隐患。

① 所有这些锁都在内部调用 Thread 的 BeginCriticalRegion 和 EndCriticalRegion 方法，指出它们要进入和离开临界区。如有必要，你的代码也可调用这些方法。但一般只有在和非托管代码进行互操作时才有必要。

所以，位于临界区的线程遭遇未处理的异常时，CLR 首先尝试将异常升级成一次得体的 AppDomain 卸载，从而摆脱（清理）当前正在这个 AppDomain 中的所有线程以及当前正在使用的数据对象。如果 AppDomain 未能在指定时间内卸载，CLR 就将得体的 AppDomain 卸载升级成粗鲁的 AppDomain 卸载。

### 22.7.3 宿主如何拿回它的线程

宿主应用程序一般都想保持对自己的线程的控制。以一个数据库服务器为例。当一个请求抵达数据库服务器时，线程 A 获得请求，并将该请求派发（dispatch）给线程 B 以执行实际工作。线程 B 可能要执行并不是由数据库服务器的开发团队创建和测试的代码。例如，假定一个请求到达数据库服务器，要执行由运行服务器的公司用托管代码写的存储过程。数据库服务器要求存储过程在自己的 AppDomain 中运行，这个设计自然是极好的，因为能保障安全，防止存储过程访问其 AppDomain 外部的对象，还能防止代码访问不允许访问的资源（比如磁盘文件或剪贴板）。

但是，如果存储过程的代码进入死循环怎么办？在这种情况下，数据库服务器把它的一个线程派发给存储过程代码，但这个线程一去不复返。这便将数据库服务器置于一个危险的境地；服务器未来的行为变得不可预测了。例如，由于线程进入死循环，所以服务器的性能可能变得很糟。服务器是不是应该创建更多的线程？这样会消耗更多的资源（比如栈空间），而且这些线程本身也可能进入死循环。

为了解决这些问题，宿主可利用线程中止功能。图 22-3 展示了旨在解决失控（runaway）线程问题的宿主应用程序的典型架构。其具体工作方式如下（编号和图的圆圈中的编号对应）：

> 注：`Thread.Abort`、`ThreadAbortException` 和 `Thread.ResetAbort` 在 .NET Core / PowerShell 7 上均不受支持，实测调用 `Abort()` 会抛出 `PlatformNotSupportedException`。因此本节这套“强制中止失控线程”的方案只适用于 .NET Framework（PowerShell 5.1）。PowerShell 7 中限制失控代码只能靠进程隔离，例如另起 `pwsh` 进程或使用作业，而不能从外部中止线程。

![](img/6fa065e17c4549db7260fbfaf4fd384e_528_0.png)

图 22-3　宿主应用程序如何拿回它的线程

1. 客户端向服务器发送请求。
2. 服务器线程获得请求，把它派发给一个线程池线程来执行实际工作。
3. 线程池线程获得客户端的请求，执行由构建并测试宿主应用程序的那个公司写的可信代码（trusted code）。
4. 可信代码进入一个 **try** 块。从这个 **try** 块中，跨越一个 **AppDomain** 的边界进行调用（通过派生自 **MarshalByRefObject** 的一个类型）。**AppDomain** 中包含的是不可信代码（可能是存储过程），这些代码不是由制作宿主应用程序的那个公司生成和测试的。在这个时候，服务器相当于把它的线程的控制权交给了一些不可信的代码。服务器感到有点儿“紧张”了。
5. 宿主会记录接收到客户端请求的时间。不可信代码在管理员设定的时间内没有对客户端做出响应，宿主就会调用 **Thread** 的 **Abort** 方法要求 CLR 中止线程池线程，强制它抛出一个 **ThreadAbortException** 异常。
6. 这时，线程池线程开始展开（unwind），调用 **finally** 块，使清理代码得以执行。最后，线程池线程穿越 **AppDomain** 边界返回。由于宿主的存根代码是从一个 **try** 块中调用不可信代码，所以宿主的存根代码有一个 **catch** 块捕捉 **ThreadAbortException**。
7. 为了响应捕捉到的 **ThreadAbortException** 异常，宿主调用 **Thread** 的 **ResetAbort** 方法。稍后将介绍该调用的目的。
8. 现在，宿主的代码已捕捉到 **ThreadAbortException** 异常。因此，宿主可向客户端返回

> 注：原文在此处被截断，第 8 步的后半句及 22.7.3 节的收尾（包括对 `Thread.ResetAbort` 用途的说明）缺失，本章至此结束。
