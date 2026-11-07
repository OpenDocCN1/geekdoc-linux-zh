是某些状态在一个地方发生了损坏。即使 **catch** 或 **finally** 块内部抛出了异常也不是世界末日——**CLR** 的异常机制仍会正常运转，好像异常是在 **finally** 块之后抛出的一样。但是，出现这种情况时，**CLR** 不会记录对应的 **try** 块(如果有的话)中抛出的第一个异常，关于第一个异常的所有信息(例如堆栈跟踪)都将丢失。这个新异常可能(而且极有可能)不会由你的代码处理，最终变成一个未处理的异常。在这种情况下，**CLR** 会终止你的进程。这是件好事情，因为损坏的所有状态现在都会被销毁。相较于让应用程序继续运行，造成不可预知的结果以及可能的安全漏洞，这样处理要好得多！

我个人认为，C#团队应该为异常处理机制选择一套不同的语言关键字。程序员想做的是尝试(try)执行一些代码。如果发生错误，要么处理(handle)错误，以便从错误中恢复并继续；要么进行补偿(compensate)来撤销一些状态更改，并向调用者上报错误。程序员还希望确保清理操作(cleanup)无论如何都会发生。左边的代码是目前 C#编译器所支持的方式，右边的是我推荐的可读性更佳的方式：

```
```csharp
void Method() {
    try {
        ...
    }
    catch (XxxException) {
        ...
    }
    catch (YyyException) {
        ...
    }
    catch {
        ...; throw;
    }
    finally {
        ...
    }
}
```
```

```
```csharp
void Method() {
    try {
        ...
    }
    handle (XxxException) {
        ...
    }
    handle (YyyException) {
        ...
    }
    compensate {
        ...
    }
    cleanup {
        ...
    }
}
```
```

> > ### **CLS 和非 CLS 异常**
> >
> > 所有面向 **CLR** 的编程语言都必须支持抛出从 **Exception** 派生的对象，因为公共语言规范(**Common Language Specification, CLS**)对此进行了硬性规定。但是，**CLR** 实际允许抛出任何类型的实例，而且有些编程语言允许代码抛出非 **CLS** 相容的异常对象，比如一个 **String**、**Int32** 和 **DateTime** 等。**C#**编译器只允许代码抛出从 **Exception** 派生的对象，而用其他一些语言写的代码不仅允许抛出 **Exception** 派生对象，还允许抛出非 **Exception** 派生对象。
> >
> > 许多程序员没有意识到 **CLR** 允许抛出任何对象来报告异常。大多数开发人员以为只有派生自 **Exception** 的对象才能抛出。在 **CLR** 的 2.0 版本之前，程序员写 **catch** 块来捕捉异常时，只能捕捉 **CLS** 相容的异常。如果一个 **C#**方法调用了用另一种编程语言写的方法，而且那个方法抛出一个非 **CLS** 相容的异常，那么 **C#**代码根本不能捕捉这个异常，从而造成一些安全隐患。
> >
> > 在 **CLR** 的 2.0 版本中，**Microsoft** 引入了新的 **RuntimeWrappedException** 类(在命名空间 **System.Runtime.CompilerServices** 中定义)。该类派生自 **Exception**，所以它是一个 **CLS** 相容的异常类型。**RuntimeWrappedException** 类含有一个 **Object**