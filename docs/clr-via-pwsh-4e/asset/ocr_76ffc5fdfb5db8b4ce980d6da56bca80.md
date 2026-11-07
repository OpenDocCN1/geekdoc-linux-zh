记录好出错的应用程序有关的信息后，Windows 显示一个消息框，允许用户将与出错的应用程序有关的信息发送给 Microsoft 的服务器。①这称为“Windows 错误报告”(Windows Error Reporting)，详情请访问 Windows Quality 网站(http://WinQual.Microsoft.com)。

作为公司，可以向 Microsoft 注册查看与它们自己的应用程序和组件有关的信息。注册是免费的，但要求程序集使用 VeriSign ID(也称为 Software Publisher Digital ID for Authenticode)进行签名。

当然也可以开发自己的系统，将未处理异常的信息传回给你自己，以便修正代码中的 bug。应用程序初始化时，可告诉 CLR 当应用程序中的任何线程发生一个未处理的异常时，都调用一个方法。

遗憾的是，Microsoft 的每种应用程序模型都有自己的与未处理异常打交道的方式。需要在文档中查阅以下成员的信息。

+   - 对于任何应用程序，查阅 **System.AppDomain** 的 **UnhandledException** 事件。Windows Store 应用和 Microsoft Silverlight 应用程序访问不了该事件。
+   - 对于 Windows Store 应用，查阅 **Windows.UI.Xaml.Application** 的 **UnhandledException** 事件。
+   - 对于 Windows 窗体应用程序，查阅 **System.Windows.Forms.NativeWindow** 的 **OnThreadException** 虚方法、**System.Windows.Forms.Application** 的 **OnThreadException** 虚方法以及 **System.Windows.Forms.Application** 的 **ThreadException** 事件。
+   - 对于 Windows Presentation Foundation(WPF)应用程序，查阅 **System.Windows.Application** 的 **DispatcherUnhandledException** 事件和 **System.Windows.Threading.Dispatcher** 的 **UnhandledException** 和 **UnhandledExceptionFilter** 事件。
+   - 对于 Silverlight，查阅 **System.Windows.Application** 的 **UnhandledException** 事件。
+   - 对于 ASP.NET Web 窗体应用程序，查阅 **System.Web.UI.TemplateControl** 的 **Error** 事件。**TemplateControl** 是 **System.Web.UI.Page** 类和 **System.Web.UI.UserControl** 类的基类。另外，还要查阅 **System.Web.HttpApplication** 的 **Error** 事件。
+   - 对于 Windows Communication Foundation 应用程序，查阅 **System.ServiceModel.Dispatcher.ChannelDispatcher** 的 **ErrorHandlers** 属性。

结束本节的讨论之前，最后讲一下分布式应用程序(例如 Web 站点或 Web 服务)中发生的未处理异常。理想情况下，服务器应用程序发生未处理异常，应该先把它记录到日志中，再向客户端发送通知，表明所请求的操作无法完成，最后终止服务器应用程序。遗憾的是，我们并非生活在理想世界中。因此，也许不可能向客户端发送失败通知。对于某些“有状

① 要想禁止显示这个消息框，可以通过 P/Invoke 来调用 Win32 函数 SetErrorMode，向函数传递 SEM_NOGPFAULTERRORBOX。