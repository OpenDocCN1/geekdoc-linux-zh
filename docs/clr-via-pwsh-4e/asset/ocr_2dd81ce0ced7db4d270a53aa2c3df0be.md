下面是这个技术的一个很好的应用：如果类型构造器抛出异常，而且该异常未在类型构造器方法中捕捉，CLR 就会在内部捕捉该异常，并改为抛出一个新的 **TypeInitializationException**。这样做之所以有用，是因为 CLR 会在你的方法中生成代码来隐式调用类型构造器①。如果类型构造器抛出一个 **DivideByZeroException**，你的代码可能会尝试捕捉它并从中恢复，而你甚至不知道自己正在调用类型构造器。所以，CLR 将 **DivideByZeroException** 转换成一个 **TypeInitializationException**，使你清楚地知道异常是因为类型构造器失败而发生的；问题不出在你的代码。

相反，下面是这个技术的一个不好的应用：通过反射调用方法时，CLR 内部捕捉方法抛出的任何异常，并把它转换成一个 **TargetInvocationException**。这是一个让人十分讨厌的设计，因为现在必须捕捉 **TargetInvocationException** 对象，并查看它的 **InnerException** 属性来辨别失败的真正原因。事实上，使用反射时经常看到如下所示的代码：

```
private static void Reflection(Object o) {
    try {
        // 在这个对象上调用一个 DoSomething 方法
        var mi = o.GetType().GetMethod("DoSomething");
        mi.Invoke(o, null); // DoSomething 方法可能抛出异常
    }
    catch (System.Reflection.TargetInvocationException e) {
        // CLR 将反射生成的异常转换成 TargetInvocationException
        throw e.InnerException; // 重新抛出最初抛出的
    }
}
```

好消息是：使用 C# 的 **dynamic** 基元类型（参见 5.5 节“**dynamic 基元类型**”）来调用成员，编译器生成的代码就不会捕捉全部异常并抛出一个 **TargetInvocationException** 对象；最初抛出的异常对象会正常地在调用栈中向上传递。对于大多数开发人员，这是使用 C# 的 **dynamic** 基元类型来替代反射的一个很好的理由。

# 20.9 未处理的异常

异常抛出时，CLR 在调用栈中向上查找与抛出的异常对象的类型匹配的 **catch** 块。没有任何 **catch** 块匹配抛出的异常类型，就发生一个未处理的异常。CLR 检测到进程中的任何线程有未处理的异常，都会终止进程。未处理异常表明应用程序遇到了未预料到的情况，并认为这是应用程序的真正 bug。随后，应将 bug 报告给发布该应用程序的公司。这个公司也许会修复 bug，并发布应用程序的新版本。

类库开发人员压根儿用不着去想未处理的异常。只有应用程序的开发人员才需要关心未处理的异常，而且应用程序应建立处理未处理异常的策略。Microsoft 建议应用程序开发人员接受 CLR 的默认策略。也就是说，应用程序发生未处理的异常时，Windows 会向事件日志写一条记录。为了查看该记录，可打开“事件查看器”应用程序，然后打开树结构中的“Windows 日志”->“应用程序”节点，如图 20-1 所示。

① 详情参见 8.3 节“类型构造器”。