第一行代码创建了匿名类型，我没有在 new 关键字后指定类型名称，所以编译器会自动创建类型名称，而且不会告诉我这个名称具体是什么（这正是匿名的含义）。这行代码使用上一节讨论的“对象初始化器”语法来声明属性，同时初始化这些属性。另外，由于我（开发人员）不知道编译时的类型名称，也就不知道变量 o1 声明为什么类型。但这是问题，因为可以像第 9 章讨论的那样使用 C# 的“隐式类型局部变量”功能(var)。它的作用是告诉编译器根据赋值操作符(=)右侧的表达式推断类型。

现在，让我们将注意力放在编译器实际做的事情上。遇到下面这样的一行代码时：

```
var o = new { property1 = expression1, ..., propertyN = expressionN };
```

编译器会推断每个表达式的类型，创建推断类型的私有字段，为每个字段创建公共只读属性，并创建一个构造器来接受所有这些表达式。在构造器的代码中，会用传给它的表达式的求值结果来初始化私有只读字段。除此之外，编译器还会重写 Object 的 Equals、GetHashCode 和 ToString 方法，并生成所有这些方法中的代码。最终，编译器生成的类看起来像这样：

```
```csharp
[CompilerGenerated]
internal sealed class <>f__AnonymousType0<...> : Object {
    private readonly t1 f1;
    public t1 p1 { get { return f1; } }

    ...

    private readonly tn fn;
    public tn pn { get { return fn; } }

    public <>f__AnonymousType0<...>(t1 a1, ..., tn an) {
        f1 = a1; ...; fn = an; // 设置所有字段
    }

    public override Boolean Equals(Object value) {
        // 任何字段不匹配就返回 false，否则返回 true
    }

    public override Int32 GetHashCode() {
        // 返回根据每个字段的哈希码生成的一个哈希码
    }

    public override String ToString() {
        // 返回“属性名=值”对的以逗号分隔的列表
    }
}
```
```

编译器会生成 Equals 和 GetHashCode 方法，因此匿名类型的实例能放到哈希表集合中。属性是只读的，而非可读可写，目的是防止对象的哈希码发生改变。如果对象在哈希表中作为键使用，更改它的哈希码会造成再也找不到它。编译器会生成 ToString 方法来帮助进行调试。在 Visual Studio 调试器中，可将鼠标指针放在引用了匿名类型实例的一个变量上方。随后，Visual Studio 会调用 ToString 方法，并在一个提示窗口中显示结果字符串。顺便说一句，在编辑器中写代码时，Visual Studio 的“智能感知”功能会提示属性名，这是非常好用的一个功能。