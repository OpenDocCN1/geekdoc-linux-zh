```
BinaryFormatter formatter = new BinaryFormatter();

// 先序列化再反序列化数组元素
formatter.Serialize(stream, a1);
stream.Position = 0;
Singleton[] a2 = (Singleton[])formatter.Deserialize(stream);

// 证明它的工作和预期的一样：
Console.WriteLine("Do both elements refer to the same object? "
    + (a2[0] == a2[1])); // "True"
Console.WriteLine("Do all elements refer to the same object? "
    + (a1[0] == a2[0])); // "True"
}
}
```

现在，我们通过分析代码来理解所发生的事情。Singleton 类型加载到 AppDomain 中时，CLR 调用它的静态构造器来构造一个 Singleton 对象，并将对它的引用保存到静态字段 s_theOneObject 中。Singleton 类没有提供任何公共构造器，这防止了其他任何代码构造该类的其他实例。

在 SingletonSerializationTest 中，我们创建包含两个元素的一个数组；每个元素都引用 Singleton 对象。为了初始化两个元素，我们调用 Singleton 的静态 GetSingleton 方法。这个方法返回对一个 Singleton 对象的引用。对 Console 的 WriteLine 方法的第一个调用显示“True”，证明两个数组元素引用同一个对象。

现在，SingletonSerializationTest 调用格式化器的 Serialize 方法序列化数组及其元素。序列化第一个 Singleton 时，格式化器检测到 Singleton 类型实现了 ISerializable 接口，并调用 GetObjectData 方法。这个方法调用 SetType，向它传递 SingletonSerializationHelper 类型，告诉格式化器将 Singleton 对象序列化成一个 SingletonSerializationHelper 对象。由于 AddValue 没有调用，所以没有额外的字段信息写入流。由于格式化器自动检测出两个数组元素都引用一个对象，所以格式化器只序列化一个对象。

序列化数组之后，SingletonSerializationTest 调用格式化器的 Deserialize 方法。对流进行反序列化时，格式化器尝试反序列化一个 SingletonSerializationHelper 对象，这是格式化器之前被“欺骗”所序列化的东西。（事实上，这正是为什么 Singleton 类不提供特殊构造器的原因；实现 ISerializable 接口时通常都要求提供这个特殊构造器。）构造好 SingletonSerializationHelper 对象后，格式化器发现这个类型实现了 System.Runtime.Serialization.IObjectReference 接口。这个接口在 FCL 中是像下面这样定义的：

```
public interface IObjectReference {
    Object GetRealObject(StreamingContext context);
}
```

如果类型实现了这个接口，格式化器会调用 GetRealObject 方法。这个方法返回在对象反序列化好之后你真正想引用的对象。在我的例子中，SingletonSerializationHelper 类型让 GetRealObject 返回对 AppDomain 中已经存在的 Singleton 对象的一个引用。所以，当格式化器的 Deserialize 方法返回时，a2 数组包含两个元素，两者都引用 AppDomain 中的 Singleton 对象。用于帮助进行反序列化的 SingletonSerializationHelper 对象立即变得“不可达”了¹。

① 没有谁引用它了。——译注