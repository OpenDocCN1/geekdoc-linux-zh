```
```csharp
t.ContinueWith(task => Console.WriteLine("Sum threw: " + task.Exception.InnerException),
    TaskContinuationOptions.OnlyOnFaulted);

t.ContinueWith(task => Console.WriteLine("Sum was canceled"),
    TaskContinuationOptions.OnlyOnCanceled);
```
```

# 27.5.4 任务可以启动子任务

最后，任务支持父/子关系，如以下代码所示：

```
```csharp
Task<int[]> parent = new Task<int[]>(() => {
    var results = new int[32]; // 创建一个数组来储存结果

    // 这个任务创建并启动 3 个子任务
    new Task(() => results[0] = Sum(10000), TaskCreationOptions.AttachedToParent).Start();
    new Task(() => results[1] = Sum(20000), TaskCreationOptions.AttachedToParent).Start();
    new Task(() => results[2] = Sum(30000), TaskCreationOptions.AttachedToParent).Start();

    // 返回对数组的引用（即使数组元素可能还没有初始化）
    return results;
});

// 父任务及其子任务运行完成后，用一个延续任务显示结果
var cwt = parent.ContinueWith(
    parentTask => Array.ForEach(parentTask.Result, Console.WriteLine));

// 启动父任务，便于它启动它的子任务
parent.Start();
```
```

在本例中，父任务创建并启动三个 **Task** 对象。一个任务创建的一个或多个 **Task** 对象默认是顶级任务，它们与创建它们的任务无关。但 **TaskCreationOptions.AttachedToParent** 标志将一个 **Task** 和创建它的 **Task** 关联，结果是除非所有子任务（以及子任务的子任务）结束运行，否则创建任务（父任务）不认为已经结束。调用 **ContinueWith** 方法创建 **Task** 时，可指定 **TaskContinuationOptions.AttachedToParent** 标志将延续任务指定成子任务。

# 27.5.5 任务内部揭秘

每个 **Task** 对象都有一组字段，这些字段构成了任务的状态。其中包括一个 **Int32** ID（参见 **Task** 的只读 Id 属性）、代表 **Task** 执行状态的一个 **Int32**、对父任务的引用、对 **Task** 创建时指定的 **TaskScheduler** 的引用、对回调方法的引用、对要传给回调方法的对象的引用（可通过 **Task** 的只读 **AsyncState** 属性查询）、对 **ExecutionContext** 的引用以及对 **ManualResetEventSlim** 对象的引用。另外，每个 **Task** 对象都有对根据需要创建的补充状态的引用。补充状态包含一个 **CancellationToken**、一个 **ContinueWithTask** 对象集合、为抛出来处理异常的子任务而准备的一个 **Task** 对象集合等。说了这么多，重点在于虽然任务很有用，但它并不是没有代价的。必须为所有这些状态分配内存。如果不需要任务的附加功能，那么使用 **ThreadPool.QueueUserWorkItem** 能获得更好的资源利用率。

**Task** 和 **Task<TResult>** 类实现了 **IDisposable** 接口，允许在用完 **Task** 对象后调用 Dispose。如今，所有 Dispose 方法做的都是关闭 **ManualResetEventSlim** 对象。但可定义从 **Task** 和 **Task<TResult>** 派生的类，在这些类中分配它们自己的资源，并在它们重写的 **Dispose**