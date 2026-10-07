
序列化一个线程并没有很有帮助或意义。同样，`java.io` 包中的低级输出和输入流没有实现 `Serializable`，因为它们与底层硬件进行交互。

当你创建一个可能被序列化的类时，该类应该实现 `Serializable`。这是因为该接口根本没有定义任何方法。你只需要在类声明中实现 `java.io.Serializable` 即可。像 `Serializable` 这样的空接口被称为标记接口（tagging interfaces）。它们用于标识具有某些属性的实现类，而不需要这些类实际实现任何方法。基本类型数组或可序列化对象的数组本身是可以序列化的。

反序列化涉及许多复杂的后台操作。对象流为被反序列化的对象创建一个空白实例，然后设置其字段值。为了实现这一点，必须应用一个特殊的构造函数。考虑对象的类层次结构：对象本身实现了 `Serializable`；对象的父类可能实现也未实现 `Serializable`。当你处理继承层次结构时，最终会遇到第一个不可序列化的父类。该父类必须有一个无参构造函数。通常，第一个不可序列化的类是 `Object`，它具有相应的构造函数。如果不满足该条件，`readObject()` 将抛出 `InvalidClassException`。异常信息显示为“valid constructor”。

```java
private void writeObject(ObjectOutputStream oos)
throws IOException
private void readObject(ObjectInputStream ois)
throws IOException, ClassNotFoundException
```

注意访问权限。当对象流执行其 `writeObject()` 方法时，它会检查对象是否具有签名匹配的 `writeObject` 方法。如果是这种情况，流将跳过其默认行为（即序列化对象的非 transient 字段），并直接调用该类的 `writeObject()` 方法。同样，当输入流执行其 `readObject()` 方法时，它会检查对象是否具有签名匹配的 `readObject()` 方法，如果是，则跳过普通的反序列化，转而调用 `readObject()` 方法。

如果一个类希望其 `readObject()` 方法在执行默认序列化行为之外还采取特殊操作，它可以调用输出流的 `defaultWriteObject()` 方法，该方法会序列化对象的非 transient 字段。正如你所预期的，`ObjectInputStream` 类有一个 `defaultReadObject()` 方法，它可以从对象输入流中反序列化出当前对象。这是一个提供自定义序列化代码的可序列化类的示例：

import java.io.*;

```java
class DoItMyself implements Serializable {
```

```java
private String id;
protected int n;
transient byte notMe;
```

```java
private void writeObject(ObjectOutputStream oos)
throws IOException {
  oos.writeUTF("The password is swordfish");
  oos.defaultWriteObject();
}
```

```java
private void readObject(ObjectInputStream is)
throws IOException, ClassNotFoundException {
  String password = is.readUTF();
  if (!password.equals("The password is swordfish"))
    throw new SecurityException("Bad password");
  is.defaultReadObject();
}
```

当该类的实例被序列化时，对象输出流注意到该实例具有具有适当签的 `writeObject()` 方法。该方法会被调用。密码被序列化。然后调用输出流的 `defaultWriteObject()`，执行默认序列化。

当对象流尝试反序列化 `DoItMyself` 实例时，流检测到存在签名匹配的 `readObject()` 方法，该方法会被调用。检查序列化的密码。如果它不是预期值，则会抛出安全异常（`SecurityException` 是运行时的，因此不需要声明）。如果密码正确，调用 `defaultReadObject()` 会导致对象字段的正常反序列化。

通过显式序列化和反序列化 `id` 和 `n` 可以避免调用 `defaultWriteObject()` 和 `defaultReadObject()`。与示例中实际代码相比，这只需要少量的额外努力。然而，如果类有大量字段，默认行为的优势将显而易见。

提供自定义序列化和反序列化的另一种方法是实现 `Externalizable`。注意 `Externalizable` 要求程序员处理序列化和反序列化过程。`Externalizable` 接口定义两个方法：

| 方法 | 异常异常 |
| :--- | :--- |
| writeExternal(ObjectOutputStream oos) | IOException |
| readExternal(ObjectInputStream ois) | IOException, ClassNotFoundException |

当类实现 `Externalizable` 时，必须有一个公共的无参构造函数。这是因为 JVM 在调用 `readExternal()` 之前需要创建对象的实例。这是一个 `Externalizable` 类的示例：

```java
import java.io.*;

class DoItMyself implements Externalizable {
    private String id;
    protected int n;
    transient byte notMe;

    public DoItMyself() {}

    public void writeExternal(ObjectOutputStream oos) throws IOException {
        oos.writeUTF(id);
        oos.writeInt(n);
    }

    public void readExternal(ObjectInputStream ois) throws IOException, ClassNotFoundException {
        id = ois.readUTF();
        n = ois.readInt();
    }
}
```

当该类的实例被序列化时，对象输出流注意到该实例具有具有适当签名的 `writeExternal()` 方法。该方法会被调用。`id` 和 `n` 被序列化。然后**不会**调用输出流的 `defaultWriteObject()`。

当对象流尝试反序列化 `DoItMyself` 实例时，流检测到存在签名匹配的 `readExternal()` 方法，该方法会被调用。序列化的 `id` 和 `n` 被反序列化。

通过显式序列化和反序列化 `id` 和 `n` 可以避免调用 `defaultWriteObject()` 和 `defaultReadObject()`。与示例中实际代码相比，这只需要少量的额外努力。然而，如果类有大量字段，默认行为的优势将显而易见。
