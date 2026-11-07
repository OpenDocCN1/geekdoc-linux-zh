```
```csharp
private readonly String m_SomeReadOnlyField = "2";    // 4
private static Int32 s_SomeReadWriteField = 3;         // 5

// 类型构造器
static SomeType(){}                                      // 6

// 实例构造器
public SomeType(Int32 x) { }                             // 7
public SomeType() { }                                    // 8

// 实例方法和静态方法
private String InstanceMethod() { return null;}          // 9
public static void Main(){}                              //10

// 实例属性
public Int32 SomeProp{                                    //11
    get{ return 0; }                                      //12
    set{ }                                                 //13
}

// 实例有参属性（索引器）
public Int32 this[String s] {                             //14
    get{return 0;}
    set{}
}

// 实例事件
public event EventHandler SomeEvent;                      //17
}
```
```

编译这个类型，用 ILDasm.exe 查看元数据，将得到如图 6-1 所示的输出。

![](bbox=[0.157, 0.508, 0.872, 0.784])

图 6-1　用 ILDasm.exe 查看 SomeType 的元数据

注意，源代码中定义的所有成员都造成编译器生成元数据。事实上，有的成员还造成编译器生成额外的成员和额外的元数据。例如，事件成员(17)造成编译器生成一个字段、两个方法和一些额外的元数据。目前不理解这些内容没有关系。但在学习后面几章时，希望你能回头看看这个例子，体会成员是如何定义的，它们对编译器生成的元数据有何影响。