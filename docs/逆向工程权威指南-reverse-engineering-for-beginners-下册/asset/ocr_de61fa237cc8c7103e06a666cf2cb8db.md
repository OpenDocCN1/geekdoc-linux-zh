```
10: iastore
11: dup
12: iconst_2
13: iconst_3
14: iastore
15: dup
16: iconst_3
17: iconst_4
18: iastore
19: dup
20: iconst_4
21: iconst_5
22: iastore
23: invokestatic #4 // Method f:([I]V
26: return
```

main()函数通过newarray指令创建了一个数组，接着填充了这个数组，随后调用了f()函数。

虽然newarray属于某种虚拟机函数，但是在main()结束后对象没有被析函数释放。实际上Java没有回收机制。JVM具有自动的垃圾回收机制。

另外，main()退出后，对象的值其实是未消失的。实在在JAVA环境中就没有清除这个指令，因为JAVA的内存机制会自动清理不需要的存储，当然是在认为必要时才进行。

系统自带的format()方法是如何处理可变参数的呢？它把输入参数为了字符串和数组型对象这两大部分：

```
public PrintStream format(String, Object... args)
```

参考链接：nhttp://oracle.com/javase/tutorial/java/data/numberformat.html

我们来看看下面的例子：

public static void main(java.lang.String[] args) 
{
    int i=123;
    double d=123.456;
    System.out.format("int: %d double: %f\n", i, d);
}
public static void main(java.lang.String[] args) 
{
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=7, locals=4, args_size=1