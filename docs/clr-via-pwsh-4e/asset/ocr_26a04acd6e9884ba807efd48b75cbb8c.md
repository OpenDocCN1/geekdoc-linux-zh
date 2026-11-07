收器在内存中移动对象。String 对象被移走了，本机代码就会向已经不包含 String 对象的字符内容的内存进行读写——导致应用程序的行为无法预测。

使用 CLR 的 P/Invoke 机制调用方法时，CLR 会自动帮你固定实参，并在本机方法返回时自动解除固定。所以，大多数时候都不必使用 GCHandle 类型来显式固定任何托管对象。只有在将托管对象的指针传给本机代码，然后本机函数返回，但本机代码将来仍需要使用该对象时，才需要显式使用 GCHandle 类型。最常见的例子就是执行异步 I/O 操作。

假定分配了一个字节数组，并准备在其中填充来自一个套接字的数据。这时应该调用 GCHandle 的 Alloc 方法，传递对数组对象的引用以及 Pinned 标志。然后，在返回的 GCHandle 实例上调用 AddrOfPinnedObject 方法。这会返回一个 IntPtr，它是已固定对象在托管堆中的实际地址。然后，将该地址传给本机函数，该函数立即返回至托管代码。数据从套接字传来时，该字节数组缓冲区在内存中不会移动；阻止移动是 Pinned 标志的功劳。异步 I/O 操作完毕后调用 GCHandle 的 Free 方法，以后垃圾回收时就可以移动缓冲区了。托管代码应包含一个缓冲区引用，这使你能访问数据。正是由于这个引用的存在，所以才会阻止垃圾回收从内存中彻底释放该缓冲区。

值得注意的是，C#提供了一个 fixed 语句，它能在一个代码块中固定对象。以下代码演示了该语句是如何使用的：

```
unsafe public static void Go() {
    // 分配一系列立即变成垃圾的对象
    for (Int32 x = 0; x < 10000; x++) new Object();

    IntPtr originalMemoryAddress;
    Byte[] bytes = new Byte[1000]; // 在垃圾对象后分配这个数组

    // 获取 Byte[] 在内存中的地址
    fixed (Byte* pbytes = bytes) { originalMemoryAddress = (IntPtr) pbytes; }

    // 强迫进行一次垃圾回收；垃圾对象会被回收，Byte[] 可能被压缩
    GC.Collect();

    // 获取 Byte[] 当前在内存中的地址，把它同第一个地址比较
    fixed (Byte* pbytes = bytes) {
        Console.WriteLine("The Byte[] did{0} move during the GC",
            (originalMemoryAddress == (IntPtr) pbytes) ? " not" : null);
    }
}
```

使用 C#的 fixed 语句比分配一个固定 GC 句柄高效得多。这里发生的事情是，C#编译器在 pbytes 局部变量上生成一个特殊的“已固定”标志。垃圾回收期间，GC 检查这个根的内容，如果根不为 null，就知道在压缩阶段不要移动变量引用的对象。C#编译器生成 IL 将 pbytes 局部变量初始化为 fixed 块起始处的对象的地址。在 fixed 块的尾部，编译器还会生成 IL 指令将 pbytes 局部变量设回 null，使变量不再引用任何对象。这样一来，下一次垃圾回收发生时，对象就可以移动了。

现在讨论一下另外两个标志，即 Weak 和 WeakTrackResurrection。它们既可用于和本机代码的互操作，也可在只有托管代码的时候使用。Weak 标志使你知道在什么时候一个对象被判定为垃圾，但这时对象的内存不一定被回收。WeakTrackResurrection 标志使你知道