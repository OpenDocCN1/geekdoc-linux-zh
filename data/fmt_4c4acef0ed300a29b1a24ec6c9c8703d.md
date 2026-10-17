
# 高级网络攻击与利用

## 列表 251 - 反序列化应用程序

我们注意到已经将对象类型更改为 `ExecCMD`，并将文本标签重命名为 `cmd`。这与我们之前在 `ExecCMD` 类中看到的公共属性名对应。最后，我们将该值设置为我们想要启动的进程名称，在本例中为 `calc.exe`。如果我们再次运行我们的反序列化应用程序，将会看到以下内容：

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_228_0.png)

正如我们在这个相当平易的例子中再次看到的，只要我们能够获取所需的类信息，并且目标类可以被 `XmlSerializer` 反序列化，我们就可以实例化原始开发者可能从未意过要被反序列化的对象。这是可能的，因为在我们目前所检查的代码中，在用户提供的输入被 `XmlSerializer` 处理之前，没有实现任何对象类型验证。

在某些现实案例中，这种类型的漏洞可能会导致严重的后果。我们将详细查看一个涉及 `DotNetNuke` 平台的案例。

### 7.4.7 练习

重复上一节中列出的步骤。反序列化一个将产生 `Notepad.exe` 实例的对象。

## DotNetNuke 漏洞分析

现在我们已经有了关于 `XmlSerializer` 的基础知识，可以开始分析由 Muñoz 和 Mirosh 发现的实际 `DotNetNuke` 漏洞。

根据报告，该漏洞存在于 `DNNPersonalization` cookie 的处理中，正如名称所示，它与用户配置直接相关。有趣的是，这种漏洞可以在无需验证的情况下触发。

### 7.5.1 漏洞概述

该漏洞的入口点位于 `LoadProfile` 函数中，该函数实现在 `DotNetNuke.dll` 模块中。虽然 `DNN` 的源代码公开可用，但为了我们的分析，我们使用 `dnSpy` 调试器，因为我们稍后需要它来跟踪程序的执行。

同样，在这种情况下，我们可以使用 `DNN` 平台的官方源码，因为它是公开的，但在大多数现实场景中情况并非如此。因此，使用 `dnSpy` 进行反编译和调试将帮助我们更熟悉这些情况下的典型工作流。

开始开始，我们需要使用 `dnSpy` 的 x64 版本，因为我们稍后要调试的 `w3wp.exe` 进程位于我们的 `DotNetNuke.dll` 文件上，我们可以只需通过 `dnSpy` 的 `File > Open` 菜单浏览到它，或从资源管理器将其拖入 `dnSpy` 窗口。

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_229_0.png)

图 129：`DotNetNuke.dll` 的分解

我们现在可以导航到位于 `DotNetNuke.Services.Personalization.PersonalizationController` 命名下的目标 `LoadProfile` 函数。

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_230_0.png)

图 130：导航到 `LoadProfile` 函数

```csharp
LoadProfile(int userId, Personalization personalization)
{
    // DotNet.Services.Personalization.PersonalizationController
    public PersonalizationInfo LoadProfile(int userId, string portalId)
    {
        PersonalizationInfo personalizationInfo = new PersonalizationInfo()
        {
            UserId = userId;
            PortalId = portalId;
            IsPostified = false;
        }
        string text = null;
        if (userId != null)
        {
            string key = string.format("UserPersonalization [{0}]", portalId, userId);
            text = (string)Cache.GetOrAdd(key, CacheItemPriority.Normal, new object[] {});
        }
        else
        {
            HttpContext httpContext = HttpContext.Context;
            if (httpContext != null && httpContext.Request.Cookies["DMPersonalization"] != null)
            {
                text = httpContext.Request.Cookies["DMPersonalization"].Value;
            }
            personalizationInfo.Profile = (string.IsNullOrEmpty(text) ? new Hashtable() : Globals.DeserializeHashTable(text));
            return personalizationInfo;
    }
}
```

图 131：`DNN` 漏洞的入口点

在图 131 中，我们可以看到 `dnSpy` 中显示的 `LoadProfile` 实现。需要注意的是，正如 Muñoz 和 Mirosh 演示中指出的，每当我们访问 `DNN` 应用程序中不存在的页面时，该函数就可以被触发。我们稍后将确认这一点。

在第 24 行，函数检查传入请求中是否存在 `DNNPersonalization` cookie。如果 cookie 存在，其值被赋值给第 26 行的本地 `text` 字符串。然后，在第 29 行，该变量作为参数传递给 `DeserializeHashTable` 函数。

如果我们遵循这一执行路径，我们将看到 `DeserializeHashTable` 函数的以下实现：

```csharp
2457 // Token: 0x060040C RID: 16428 RVA: 0x00E7174 File Offset: 0x00E5374
2458 public static Hashtable DeserializeXml(string Source)
2459 {
2460     return XmlUtils.DeserializeHashTable(Source, "profile");
2461 }
```

图 132：`DeserializeXml` 的实现

> ⁷³ [https://github.com/0xd4d/dnSpy/wiki/Making-an-Image-Easy-to-Debug](https://github.com/0xd4d/dnSpy/wiki/Making-an-Image-Easy-to-Debug)
>
> ⁷⁴ [https://docs.microsoft.com/en-us/api/system.msdn.debuggableattribute.debuggingmodes?redirectfrom=MSDN&view=netframework-4.7.2](https://docs.microsoft.com/en-us/api/system.msdn.debuggableattribute.debuggingmodes?redirectfrom=MSDN&view=netframework-4.7.2)

### 7.5.2 调试 DotNetNuke

#### 程序集属性

调试 .NET 应用程序由于运行时应用的优化，可能会变得有些棘手。这些优化在调试会话中的表现之一是阻止我们在任意位置设置断点。也就是说，调试器无法将断点绑定到特定的代码行。

由于此，除了无法在想要的地方中断外，有时还无法查看该处的局部变量值。这使得调试 .NET 程序比我们想象的要困难。

幸运的是，有一种方法可以修改经过优化的目标文件。具体来说，软件是以 `Release` 版本编译并发布的，而不是 `Debug`。因此，程序集属性类似于：

```csharp
[assembly: Debuggable(DebuggableAttribute.DebuggingModes.IgnoreSymbolSequencePoints)]
```

列表 253：`Release` 版本的 .NET 程序集

为了启用调试体验，即减少运行时执行的优化，我们可以将其更改为如下形式：

```csharp
[assembly: Debuggable(DebuggableAttribute.DebuggingModes.DisableOptimizations.Default | DebuggableAttribute.DebuggingModes.IgnoreSymbolSequencePoints | DebuggableAttribute.DebuggingModes.EnableEditAndContinue)]
```

列表 254：特定的程序集可以控制运行时应用的优化

一如既往，在我们进行任何操作之前，我们应该对要操作的文件进行备份。然后我们可以使用 `dnSpy` 打开目标程序集，在程序集管理器中右键点击其名称，并从上下文菜单中选择“编辑程序集属性 (C#)”（图 134）。该选项也可以通过“编辑”菜单访问。

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_234_0.png)

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_234_1.png)

图 134：访问编辑程序集属性菜单

点击该选项将打开一个程序集属性的编辑器。

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_234_2.png)

图 135：程序集属性

在这里，我们需要将列表 253 提到的属性替换为列表 254 中找到的内容。

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_235_0.png)

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_235_1.png)

图 136：编辑程序集属性

一旦替换了相关的程序集属性，我们只需点击 `Compile`（编译）按钮，这将关闭编辑器窗口。最后，我们通过点击 `File > Save Module`（文件 > 保存模块）来保存我们的程序集，这将显示以下对话框：

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_235_2.png)

图 137：保存编辑后的程序集

我们可以接受默认值，编辑后的程序集将覆盖原始文件。此时，我们就可以开始使用 `dnSpy` 调试器了。

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_236_0.png)

#### 练习

更改 `DotNetNuke.dll` 的属性，并确保能够正确重新编译并保存程序集。

## 使用 dnSpy

正如我们在之前的模块中所做的那样，我们将再次依赖 `Burp` 代理来精确控制我们的有效负载。请注意，实验室虚拟机上的浏览器代理设置已经配置好。因此，在浏览 `DNN` 网页之前，请确保 `BurpSuite` 已经运行。

此外，我们还将使用 `dnSpy` 调试器来查看我们的有效负载是如何被处理的。虽然我们已经熟悉 `Burp` 及其设置，但我们仍然花一点时间研究 `dnSpy` 的机制。请参考相关视频以详细查看后续过程。

为了调试 `DNN`，我们需要将调试器（`Debug > Attach` 菜单）附加到 `w3wp.exe`。这是我们的 `DNN` 实例正在运行的 `IIS` 工作进程。请注意，如果你无法在 `dnSpy` 的 `Attach to Process`（附加到进程）对话框（图 138）中看到该进程，只需使用网络浏览器调试 `DNN` 实例。这将触发 `IIS` 启动适当的工作进程。之后，点击 `Refresh`（刷新）按钮，你就能在对话框中看到 `w3wp.exe` 实例。

![](img/5d1c2c08c609e4691e93ba5fa2d52a8a_236_1.png)

图 138：调试 `w3wp.exe` 进程

一旦附加到进程，我们需要做的第一件事是使用相应的 `Debug` 菜单选项或快捷菜单按钮暂停其执行。我们需要访问 `Debug > Windows > Modules` 来列出 `w3wp.exe` 进程加载的所有模块。

|  | 已优化 (`Optimized`) | 动态 (`Dynamic`) | 内存 (`InMemory`) | 顺序 (`Order`) | 时间戳 (`Timestamp`) | 地址 (`Address`) | 进程 (`Process`) | 程序域 (`AppDomain`) |
|---|---|---|---|---|---|---|---|---|
| `System.Web.Helpers.dll` | 是 | 否 | 106 | 3 | 0.20180 | 2019-01-24 15:22:13 | 00000018-b000-0000-a000-000000000000 | `w3wp.exe` | [1]/W35C... |
| `System.Web.Http.dll` | 是 | 否 | 109 | 5 | 5.20180 | 2019-01-28 15:50:54 | 00000011-a000-0000-a000-000000000000 | `w3wp.exe` | [1]/W35C... |
