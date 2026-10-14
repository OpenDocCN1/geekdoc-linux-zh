

正如程序的输出所示，它强制发生十个异常，所有异常都得到了正常处理。然而在第十次之后，程序会产生一个更严重的错误，导致自定义处理器退回处理该问题。最后，程序会优雅地降级并显示一条错误消息——尽管出现了意外的异常，但没有产生核心转储。这些操作模拟了一种典型情况，即一个错误导致另一个错误，进而导致另一个错误，最终引发各种问题。

为了跟踪已发生的错误数量，程序在列表末尾附近的 Error 类构造函数会递增类的静态 count 变量。因为 count 是静态的，所以所有 Error 对象只有一个副本的其值。Error 中还包含一个函数 Say()，用于显示 count 的值。

在构造 Error 对象的过程中，如果 count 等于或超过常量 MAXERR，构造函数会抛出类型为 MaxError 的异常。因为程序没有捕获这种类型的错误，所以此操作会触发自定义处理器。这模拟了调用第三方库中的函数时可能发生的情况，这些函数可能会抛出未知类型的异常。即使在你自己的代码中，如果你忽略捕获特定类型的异常，也可能发生这种情况。

> Note
> 
> 当构造函数抛出异常时，对象不会被构造。有关此主题的更多信息，请参阅本章后面的“Exceptions and Constructors”。

unexpect.cpp 程序中的 Function main()（请参阅 Listing 16.4）安装了替换默认 unexpected() 和 terminate() 函数的处理器。程序随后执行一个 Do-Forever for 循环，其中 try 块调用一个本地函数 run()。该函数故意抛出类型为 Error 的异常，由 main() 中的 catch 语句捕获。前十次发生这种情况时，程序通过调用 Error 对象的 Say() 成员函数来显示一条消息。然而在第十次错误之后，Error 类的构造函数放弃了这场好斗，并通过执行以下语句抛出类型为 MaxError 的异常：

```
count++;
if (count >= MAXERR)
    throw MaxError();
```

这模拟了一种严重情况，即对象无法被构造。在这种情况下，问题甚至比正常情况更严重，因为它发生在 Error 类对象的构造函数中。因为 main() 的 try-catch 语句不识别类型为 MaxError 的错误，所以此操作会导致 main() 结束，并将控制权传递给我们的 guest unexpected 异常处理器。在该函数中，执行了两个语句：

```
cout << "Inside custom_unexpected function" << endl;
throw Error;    // Continues program
```

第一个语句只是为了让你能够观察到何时调用自定义处理器。第二个语句展示了如何在此阶段继续程序。在现实情况下，unexpected 处理器可能会检查程序的状态并采取措施，允许用户关闭文件或重新建立网络通信——无论需要做什么才能恢复正常。自定义处理器现在有两个选项：

- 它可以调用 terminate()，在这种情况下程序进入其关键关闭阶段，或
- 它可以抛出已知类型的异常。

第二种措施是你抵御意外异常的第一道防线。从 unexpected 异常处理器内部抛出异常，实际上是将未知异常转换为已知类型。通常，main() 中的一个循环会捕获该类型的异常，以便程序在执行其恢复逻辑后可以继续运行。

然而在这种情况下，抛出 Error 对象会导致另一个未知异常被发射出去。这模拟了即使在尝试从问题中恢复后，程序也无法继续的严重情况。其结果是调用自定义 terminate() 函数，该函数显示一条错误消息并通过调用 exit() 结束：

```
cout << "Inside terminate function" << endl;
cout << "Exiting program" << endl;
exit(1); // Exits program
```

尽管简单，但演示程序模拟了导致程序无法继续的极端条件。但至少它尽可能优雅地结束。

对程序进行一个简单的更改也可以演示如何处理意外异常并仍允许程序继续。只有当程序不再能够构造 Error 对象时，我们的 terminate 函数才会结束表演。要进行此更改，请重写 run() 函数以抛出字符串对象：

```
void run() throw(Error)
{
    throw "An unknown exception object";
}
```

使用与之前相同的命令编译并运行修改后的 unexpect.cpp 程序：

```
$ g++ unexpect.cpp
$ ./a.out
Inside custom_unexpected function
Error: count = 1
Error: count = 1
Inside custom_unexpected function
Error: count = 10
Inside custom_unexpected function
Inside terminate function
Exiting program
```

这次，因为 main() 不识别类型为 const char * 的异常，所以每个 Error 异常都会导致我们的自定义 unexpected 异常处理器被调用。实际上，处理器将意外异常转换为已知类型，即 Error 类的对象。这允许程序在存在意外条件的情况下继续运行。然而，最终 Error 类超过了其最大计数，其构造函数抛出类型为 MaxError 的错误。unexpected 处理器不会接收这种类型的异常——相反，terminate 函数被调用，程序结束。

