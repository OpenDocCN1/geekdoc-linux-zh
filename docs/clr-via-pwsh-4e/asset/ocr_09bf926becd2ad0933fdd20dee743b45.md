```
Red
}
```

编译器会报告以下错误：

```
error CS0579: 重复的"Flags"特性。
```

但少数几个特性确有必要多次应用于同一个目标。FCL 特性类 ConditionalAttribute 允许将它的多个实例应用于同一个目标元素。不将 AllowMultiple 明确设为 true，特性就只能向选定的目标元素应用一次。

AttributeUsageAttribute 的另一个属性是 Inherited，它指出特性在应用于基类时，是否同时应用于派生类和重写的方法。以下代码演示了特性的继承：

```
```csharp
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method,
    Inherited=true)]
internal class TastyAttribute : Attribute
{
}

[Tasty][Serializable]
internal class BaseType
{
    [Tasty] protected virtual void DoSomething() { }
}

internal class DerivedType : BaseType
{
    protected override void DoSomething() { }
}
```
```

在上述代码中，DerivedType 及其 DoSomething 方法都被视为 Tasty，因为 TastyAttribute 类被标记为可继承。但 DerivedType 不可序列化，因为 FCL 的 SerializableAttribute 类被标记为不可继承。

注意，.NET Framework 只认为类、方法、属性、事件、字段、方法返回值和参数等目标元素是可继承的。所以，定义特性类型时，只有在该特性应用于上述某个目标的前提下，才应该将 Inherited 设为 true。注意，可继承特性不会造成在托管模块中为派生类型生成额外的元数据。18.4 节“检测定制特性”将进一步讨论这方面的问题。

![](bbox=[0.065, 0.666, 0.127, 0.71])

> **注意**　定义自己的特性类时，如果忘记向自己的类应用 AttributeUsage 特性，编译器和 CLR 将假定该特性能应用于所有目标元素，向每个目标元素都只能应用一次，而且可继承。这些假定模仿了 AttributeUsageAttribute 类中的默认字段值。

# 18.3　特性构造器和字段/属性数据类型

定制特性类可定义构造器来获取参数。开发人员在应用特性类的实例时必须指定这些参数。还可在类中定义非静态公共字段和属性，使开发人员能为特性类的实例选择恰当的设置。

定义特性类的实例构造器、字段和属性时，可供选择的数据类型并不多。具体地说，只允