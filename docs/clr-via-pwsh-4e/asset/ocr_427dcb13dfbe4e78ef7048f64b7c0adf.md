生成上述代码时，编译器自动为 SomeType 生成一个类型构造器，好像源代码本来是这样写的：

```
```csharp
internal sealed class SomeType {
    private static Int32 s_x;
    static SomeType() { s_x = 5; }
}
```
```

使用 ILDasm.exe 查看类型构造器的 IL，很容易验证编译器实际生成的东西。类型构造器方法总是叫 .cctor（代表 class constructor）。

在以下代码中，可以看到 .cctor 方法是 private 和 static 的。另外，注意方法中的代码确实将值 5 加载到静态字段 s_x 中。

```
```il
.method private hidebysig specialname rtspecialname static
        void .cctor() cil managed
{
    // Code size 7 (0x7)
    .maxstack 8
    IL_0000: ldc.i4.5
    IL_0001: stsfld int32 SomeType::s_x
    IL_0006: ret
} // end of method SomeType::.cctor
```
```

类型构造器不应调用基类型的类型构造器。这种调用之所以没必要，是因为类型不可能有静态字段是从基类型分享或继承的。

> > **注意**　有的语言（比如 Java）希望在访问类型时自动调用它的类型构造器，并调用它的所有基类型的类型构造器。此外，类型实现的接口也必须调用接口的类型构造器。CLR 不支持这种行为。但是，使用由 **System.Runtime.CompilerServices.RuntimeHelpers** 提供的 **RunClassConstructor** 方法，编译器和开发人员可以实现这种行为。任何语言想要实现这种行为，可以告诉它的编译器在一个类型的类型构造器中生成代码，为所有基类型都调用这个方法。用 **RunClassConstructor** 方法调用一个类型构造器，CLR 就知道类型构造器之前是否执行过。如果是，CLR 不会再次调用它。

最后，假定有以下代码：

```
```csharp
internal sealed class SomeType {
    private static Int32 s_x = 5;

    static SomeType() {
        s_x = 10;
    }
}
```
```

在这个例子中，C#编译器只生成一个类型构造器方法。它首先将 s_x 初始化为 5，再把它修改成 10。换言之，当 C#编译器为类型构造器生成 IL 代码时，它首先生成的是初始化静态字段所需的代码，然后才会添加你的类型构造器方法中显式包含的代码。