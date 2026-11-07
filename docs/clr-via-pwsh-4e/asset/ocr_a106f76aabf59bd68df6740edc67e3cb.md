方法的每一个调用都强迫调用线程从托管代码转换为内核代码，再转换回来——这是不好的地方。但在存在竞争的时候，输掉的线程会被内核阻塞，不会在那里“自旋”，从而浪费 CPU 时间——这是好的地方。还要注意，构造 **AutoResetEvent** 对象并在它上面调用 **Dispose** 也会造成从托管向内核的转换，对性能造成负面影响。这些调用一般很少发生，所以一般不必过于关心它们。

为了更好地理解性能上的差异，我写了一些代码：

```
```csharp
public static void Main() {
    Int32 x = 0;
    const Int32 iterations = 10000000;  // 1000 万

    // x 递增1000万次，要花多长时间？
    Stopwatch sw = Stopwatch.StartNew();
    for (Int32 i = 0; i < iterations; i++) {
        x++;
    }
    Console.WriteLine("Incrementing x: {0:N0}", sw.ElapsedMilliseconds);

    // x 递增1000万次，加上调用一个什么都不做的方法的开销，要花多长时间？
    sw.Restart();
    for (Int32 i = 0; i < iterations; i++) {
        M(); x++; M();
    }
    Console.WriteLine("Incrementing x in M: {0:N0}", sw.ElapsedMilliseconds);

    // x 递增1000万次，加上调用一个无竞争的 SpinLock 的开销，要花多长时间？
    SpinLock sl = new SpinLock(false);
    sw.Restart();
    for (Int32 i = 0; i < iterations; i++) {
        Boolean taken = false; sl.Enter(ref taken); x++; sl.Exit();
    }
    Console.WriteLine("Incrementing x in SpinLock: {0:N0}", sw.ElapsedMilliseconds);

    // x 递增1000万次，加上调用一个无竞争的 SimpleWaitLock 的开销，要花多长时间？
    using (SimpleWaitLock swl = new SimpleWaitLock()) {
        sw.Restart();
        for (Int32 i = 0; i < iterations; i++) {
            swl.Enter(); x++; swl.Leave();
        }
        Console.WriteLine("Incrementing x in SimpleWaitLock: {0:N0}", sw.ElapsedMilliseconds);
    }
}

[MethodImpl(MethodImplOptions.NoInlining)]
private static void M() { /* 这个方法什么都不做，直接返回 */ }
```
```

在我的机器上运行上述代码，得到以下输出：

```
```
Incrementing x: 8                              最快
Incrementing x in M: 69                        约慢 9 倍
Incrementing x in SpinLock: 164                约慢 21 倍
Incrementing x in SimpleWaitLock: 8854          约慢 1107 倍
```
```

由此可以看到，单纯递增 x 只需 8 毫秒。递增前后多调用一个方法，就要多花约 9 倍的时间。然后，在用户模式的构造中执行递增，代码变慢了 21 倍(164 / 8)。最后，如果使用内核模式的构造，程序更是慢得可怕，慢了大约 1107 倍(8864 / 8)！所以，线程同步能避免就尽量避免。如果一定要进行线程同步，就尽量使用用户模式的构造。内核模式的构造要尽量避免。