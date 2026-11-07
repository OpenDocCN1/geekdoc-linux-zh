```
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
```

上述代码创建 **while** 循环，针对每个客户端请求都迭代一次。循环内部等待 **Task** 的 **WhenAny** 方法，该方法一次返回一个 **Task<String>** 对象，代表由服务器响应的一个客户端请求。获得这个 **Task<String>** 对象后，就把它从集合中删除，然后查询它的结果以进行处理(把它传给 **Console.WriteLine**)。

# 28.9 应用程序及其线程处理模型

.NET Framework 支持几种不同的应用程序模型，而每种模型都可能引入了它自己的线程处理模型。控制台应用程序和 Windows 服务(实际上也是控制台应用程序；只是看不见控制台而已)没有引入任何线程处理模型；换言之，任何线程可在任何时候做它想做的任何事情。

但 GUI 应用程序(包括 Windows 窗体、WPF、Silverlight 和 Windows Store 应用程序)引入了一个线程处理模型。在这个模型中，UI 元素只能由创建它的线程更新。在 GUI 线程中，经常都需要生成一个异步操作，使 GUI 线程不至于阻塞并停止响应用户输入(比如鼠标、按键、手写笔和触控事件)。但当异步操作完成时，是由一个线程池线程完成 Task 对象并恢复状态机。

对于某些应用程序模型，这样做无可非议，甚至可以说正好符合开发人员的意愿，因为它非常高效。但对于另一些应用程序模型(比如 GUI 应用程序)，这个做法会造成问题，因为一旦通过线程池线程更新 UI 元素就会抛出异常。线程池线程必须以某种方式告诉 GUI 线程更新 UI 元素。

ASP.NET 应用程序允许任何线程做它想做的任何事情。线程池线程开始处理一个客户端的请求时，可以对客户端的语言文化(**System.Globalization.CultureInfo**)做出假定，从而允许 Web 服务器对返回的数字、日期和时间进行该语言文化特有的格式化处理。此外，Web 服务器还可对客户端的身份标识(**System.Security.Principal.IPrincipal**)做出假定，确保只能

① 欲知详情，请访问 http://msdn.microsoft.com/zh-cn/library/bz9tc508.aspx。注意，帮助文档将 culture 翻译成“区域性”。——译注