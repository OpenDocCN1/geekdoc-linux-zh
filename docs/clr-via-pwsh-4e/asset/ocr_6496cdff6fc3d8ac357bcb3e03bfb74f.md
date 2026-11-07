成员。三个方法用不同的方式做相同的事情。

+   - **BindToMemberThenInvokeTheMember** 方法演示了如何绑定到成员并调用它。
+   - **BindToMemberCreateDelegateToMemberThenInvokeTheMember** 方法演示了如何绑定到一个对象或成员，然后创建一个委托来引用该对象或成员。通过委托来调用的速度很快。如果需要在相同的对象上多次调用相同的成员，这个技术的性能比上一个好。
+   - **UseDynamicToBindAndInvokeTheMember** 方法演示了如何利用 C#的 **dynamic** 基元类型(参见第 5 章“基元类型、引用类型和值类型”)简化成员访问语法。此外，在相同类型的不同对象上调用相同成员时，这个技术还能提供不错的性能，因为针对每个类型，绑定都只会发生一次。而且可以缓存起来，以后多次调用的速度会非常快。用这个技术也可以调用不同类型的对象的成员。

```
```csharp
using System;
using System.Reflection;
using Microsoft.CSharp.RuntimeBinder;
using System.Linq;

// 该类用于演示反射机制，
// 其中定义了一个字段、构造器、方法、属性和一个事件
internal sealed class SomeType {
    private Int32 m_someField;
    public SomeType(ref Int32 x) { x *= 2; }
    public override String ToString() { return m_someField.ToString(); }
    public Int32 SomeProp
    {
        get { return m_someField; }
        set {
            if (value < 1)
                throw new ArgumentOutOfRangeException("value");
            m_someField = value;
        }
    }
    public event EventHandler SomeEvent;
    private void NoCompilerWarnings() { SomeEvent.ToString(); }
}

public static class Program {
    public static void Main()
    {
        Type t = typeof(SomeType);
        BindToMemberThenInvokeTheMember(t);
        Console.WriteLine();

        BindToMemberCreateDelegateToMemberThenInvokeTheMember(t);
        Console.WriteLine();

        UseDynamicToBindAndInvokeTheMember(t);
        Console.WriteLine();
    }

    private static void BindToMemberThenInvokeTheMember(Type t) {
        Console.WriteLine("BindToMemberThenInvokeTheMember");

        // 构造实例
        Type ctorArgument = Type.GetType("System.Int32&");    // 或者 typeof(int32).MakeByRefType();
        ConstructorInfo ctor = t.GetTypeInfo().DeclaredConstructors.First(
            c => c.GetParameters()[0].ParameterType == ctorArgument);
        Object[] args = new Object[] { 12 }; // 构造器的实参
```
```