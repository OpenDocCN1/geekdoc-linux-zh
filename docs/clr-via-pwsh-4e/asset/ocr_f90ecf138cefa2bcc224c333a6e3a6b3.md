```
```csharp
rmh => MethodBase.GetMethodFromHandle(rmh));
Show("Size of heap after re-creating MethodInfo objects");
GC.KeepAlive(methodHandles);        // 阻止缓存被过早垃圾回收
GC.KeepAlive(methodInfos);          // 阻止缓存被过早垃圾回收

methodHandles = null;               // 现在允许缓存垃圾回收
methodInfos = null;                 // 现在允许缓存垃圾回收
Show("After freeing MethodInfos and RuntimeMethodHandles");
}

private static void Show(String s) {
    Console.WriteLine("Heap size={0,12:N0} - {1}",
        GC.GetTotalMemory(true), s);
}
}
```
```

编译并运行以上程序，在我的机器上得到以下输出：

```
```
Heap size=      22,060 - Before doing anything
# of methods=52,737
Heap size=   3,996,640 - After building cache of MethodInfo objects
Heap size=   4,207,656 - Holding MethodInfo and RuntimeMethodHandle cache
Heap size=   3,847,352 - After freeing MethodInfo objects
Heap size=   4,058,336 - Size of heap after re-creating MethodInfo objects
Heap size=      81,224 - After freeing MethodInfos and RuntimeMethodHandles
```
```