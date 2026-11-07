以下代码演示了如何修改 **Circle** 类型来修正这个问题：

```
```csharp
[Serializable]
internal class Circle {
    private Double m_radius;   // 半径

    [NonSerialized]
    private Double m_area;     // 面积

    public Circle(Double radius) {
        m_radius = radius;
        m_area = Math.PI * m_radius * m_radius;
    }

    [OnDeserialized]
    private void OnDeserialized(StreamingContext context) {
        m_area = Math.PI * m_radius * m_radius;
    }
}
```
```

修改过的 **Circle** 类包含一个标记了 **System.Runtime.Serialization.OnDeserializedAttribute** 定制特性的方法①。每次反序列化类型的实例，格式化器都会检查类型中是否定义了应用了该特性的方法。如果是，就调用该方法。调用这个方法时，所有可序列化的字段都会被正确设置。在该方法中，可能需要访问这些字段来执行一些额外的工作，从而确保对象的完全反序列化。

在上述 **Circle** 修改版本中，我调用 **OnDeserialized** 方法，使用 **m_radius** 字段来计算圆的面积，并将结果放到 **m_area** 字段中。这样 **m_area** 就有了我们希望的值(314.159)。

除了 **OnDeserializedAttribute** 这个定制特性，**System.Runtime.Serialization** 命名空间还定义了包括 **OnSerializingAttribute**, **OnSerializedAttribute** 和 **OnDeserializingAttribute** 在内的其他定制特性。可将它们应用于类型中定义的方法，对序列化和反序列化过程进行更多的控制。在下面这个类中，这些特性被应用于不同的方法：

```
```csharp
[Serializable]
public class MyType {
    Int32 x, y; [NonSerialized] Int32 sum;

    public MyType(Int32 x, Int32 y) {
        this.x = x; this.y = y; sum = x + y;
    }

    [OnDeserializing]
    private void OnDeserializing(StreamingContext context) {
        // 举例：在这个类型的新版本中，为字段设置默认值
    }

    [OnDeserialized]
    private void OnDeserialized(StreamingContext context) {
        // 举例：根据字段值初始化瞬时状态(比如 sum 的值)
    }
}
```
```

① 要在对象反序列化时调用一个方法，**System.Runtime.Serialization.OnDeserialized** 定制特性是首选方案，而不是让类型实现 **System.Runtime.Serialization.IDeserializationCallback** 接口的 **OnDeserialization** 方法。