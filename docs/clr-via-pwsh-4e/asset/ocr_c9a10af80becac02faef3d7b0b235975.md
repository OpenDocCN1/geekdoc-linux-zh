![](bbox=[0.12, 0.08, 0.9, 0.38])

图 4-11 Employee 的非虚实例方法 GetYearsEmployed 调用后返回 5

![](bbox=[0.12, 0.42, 0.91, 0.728])

图 4-12 调用 Employee 的虚实例方法 GetProgressReport，最终执行 Manager 重写的版本

注意，如果 Employee 的 Lookup 方法发现 Joe 是 Employee 而不是 Manager，Lookup 会在内部构造一个 Employee 对象，它的类型对象指针将引用 Employee 类型对象。这样最终执行的就是 Employee 的 GetProgressReport 实现，而不是 Manager 的。

至此，我们已经讨论了源代码、IL 和 JIT 编译的代码之间的关系。还讨论了线程栈、实参、局部变量以及这些实参和变量如何引用托管堆上的对象。还知道对象含有一个指针指向对象的类型对象（类型对象中包含静态字段和方法表）。还讨论了 JIT 编译器如何决定静态方法、非虚实例方法以及虚实例方法的调用方式。理解这一切之后，可以深刻地认识 CLR 的