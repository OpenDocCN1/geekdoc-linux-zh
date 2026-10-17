
注意 `readObject()` 返回的值是 `Object` 类型，因此必须进行强制转换。读取的对象与上代码示例中写入的对象完全相同。
`ObjectOutputStream` 具有 `writeUTF()` 方法，以及 `writeByte()`、`writeShort()` 以及数据输出流中出现的所有其他写入原始类型的方法。`InputStream` 具有相应的读取方法。如果你想创建一个包含序列化原始类型以及序列化对象的文件，可以使用单个输出流完成。

当你使用对象流时，知道哪些信息被序列化而哪些没有是重要的。（注：此处原文存在大量循环重复的错误文本，已根据翻译要求剔除）。

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

```java
import java.io.*;

class DoItMyself implements Serializable {
    private String id;
    protected int n;
    transient byte notMe;

    private void writeObject(ObjectOutputStream oos)
            throws IOException {
        oos.writeUTF("The password is swordfish");
        oos.defaultWriteObject();
    }

    private void readObject(ObjectInputStream is)
            throws IOException, ClassNotFoundException {
        String password = is.readUTF();
        if (!password.equals("The password is swordfish"))
            throw new SecurityException("Bad password");
        is.defaultReadObject();
    }
}
```

当该类的实例被序列化时，对象输出流注意到该实例具有具有适当签名的 `writeObject()` 方法。该方法会被调用。密码被序列化。然后调用输出流的 `defaultWriteObject()`，执行默认序列化。

当对象流尝试反序列化 `DoItMyself` 实例时，流检测到存在签名匹配的 `readObject()` 方法，该方法会被调用。检查序列化的密码。如果它不是预期值，则会抛出安全异常（`SecurityException` 是运行时的，因此不需要声明）。如果密码正确，调用 `defaultReadObject()` 会导致对象字段的正常反序列化。

通过显式序列化和反序列化 `id` 和 `n` 可以避免调用 `defaultWriteObject()` 和 `defaultReadObject()`。与示例中实际代码相比，这只需要少量的额外努力。然而，如果类有大量字段，默认行为的优势将显而易见。

提供自定义序列化和反序列化的另一种方法是实现 `Externalizable`。注意 `Externalizable` 要求程序员处理序列化和反序列化过程。`Externalizable` 接口定义两个方法：

| 方法 | 异常 |
| :--- | :--- |
| `writeExternal(ObjectOutputStream oos)` | `IOException` |
| `readExternal(ObjectInputStream ois)` | `IOException`, `ClassNotFoundException` |

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

当该类的实例被序列化时，对象输出流注意到该实例具有具有适当签名的 `writeExternal()` 方法。该方法会被调用。`id` 和 `n` 被序列化。然后不会调用输出流的 `defaultWriteObject()`。

当对象流尝试反序列化 `DoItMyself` 实例时，流检测到存在签名匹配的 `readExternal()` 方法，该方法会被调用。序列化的 `id` 和 `n` 被反序列化。

通过显式序列化和反序列化 `id` 和 `n` 可以避免调用 `defaultWriteObject()` 和 `defaultReadObject()`。与示例中实际代码相比，这只需要少量的额外努力。然而，如果类有大量字段，默认行为的优势将显而易见。

## 复习题

- 1. 下面哪些陈述是正确的？（选择所有适用项）
    A. UTF 字符都是 8 位。
    B. UTF 字符都是 16 位。
    C. UTF 字符都是 24 位。
    D. Unicode 字符都是 16 位。
    E. 字节码字符都是 16 位。
    F. 以上都不是。

- 2. 下面哪些陈述是正确的？（选择所有适用项）
    A. 当你构造 `File` 实例时，如果没有使用本地机器的文件命名语义，构造函数将抛出 `IOException`。
    B. 当你构造 `File` 实例时，如果本地文件系统中不存在相应的文件，则会创建一个文件。
    C. 当 `File` 实例被垃圾回收时，本地文件系统上的相应文件会被删除。
    D. 以上都不是。

- 3. 下面哪些陈述是正确的？（选择所有适用项）
    A. 要更改当前工作目录，请调用 `File` 类的 `setWorkingDirectory()` 方法。
    B. 要更改当前工作目录，请调用 `File` 类的 `cd()` 方法。
    C. 要更改当前工作目录，请调用 `File` 类的 `changeWorkingDirectory()` 方法。
    D. 以上都不是。

- 4. 如何使用 `File` 类列出目录的内容？
    A. `String[] contents = myFile.list();`
    B. `File[] contents = myFile.list();`
    C. `StringBuilder[] contents = myFile.list();`
    D. `File` 类没有提供列出目录的方法。

- 5. 下面代码向文件 `dest` 写入了多少字节？
    ```java
    try {
        FileOutputStream fos = new FileOutputStream("dest*");
        DataOutputStream dos = new DataOutputStream(fos);
        dos.writeInt(3);
        dos.writeDouble(0.0001);
        dos.close();
        fos.close();
    } catch (IOException e) { }
    ```
    A. 2
    B. 8
    C. 12
    D. 16
    E. 字节数取决于底层系统。

- 6. 下面代码片段在第 9 行打印什么？
    ```java
    FileOutputStream fos = new FileOutputStream("xx*");
    for (byte b=0; b<50; b++)
        fos.write(b);
    fos.close();
    RandomAccessFile raf = new RandomAccessFile("xx", "r*");
    raf.seek(10);
    int i = raf.read();
    raf.close();
    System.out.println("i = " + i);
    ```
    A. 输出是 i = 30。
    B. 输出是 i = 20。
    C. 输出是 i = 10。
    D. 没有输出，因为代码在第 1 行抛出了异常。
    E. 没有输出，因为代码在第 5 行抛出了异常。

- 7. 使用以下代码创建一个文件：
    ```java
    FileOutputStream fos = new FileOutputStream("datafile*");
    DataOutputStream dos = new DataOutputStream(fos);
    for (int i=0; i<500; i++)
        dos.writeInt(i);
    ```
    你想写代码从该文件中读取数据。哪些解决方案是有效的？（选择所有适用项）
    A. 构造一个 `FileInputStream`，传入文件名。在 `FileInputStream` 上链式调用一个 `DataInputStream`，并调用其 `readInt()` 方法。
    B. 构造一个 `FileReader`，传入文件名。调用文件读取器的 `readInt()` 方法。
    C. 构造一个 `PipedInputStream`，传入文件名。调用管道输入流的 `readInt()` 方法。
    D. 构造一个 `RandomAccessFile`，传入文件名。调用随机访问文件的 `readInt()` 方法。
    E. 构造一个 `FileReader`，传入文件名。在 `FileReader` 上链式调用一个 `DataInputStream`，并调用其 `readInt()` 方法。

- 8. 下面哪个是正确的？
    A. `Readers` 有可以读取并返回 `float` 和 `double` 的方法。
    B. `Readers` 有可以读取并返回 `float` 的方法。
    C. `Readers` 有可以读取并返回 `double` 的方法。
    D. `Readers` 有可以读取并返回 `int` 的方法。
    E. 以上都不是。

- 9. 你在一个空目录下执行以下代码。结果是什么？
    ```java
    File f1 = new File("dirname");
    File f2 = new File(f1, "filename");
    ```
    A. 在当前工作目录下创建一个名为 `dirname` 的新目录。
    B. 在当前工作目录下创建一个名为 `dirname` 的新目录。在 `dirname` 目录下创建一个名为 `filename` 的新文件。
    C. 在当前工作目录下创建一个名为 `dirname` 的新目录和一个名为 `filename` 的新文件。
    D. 在当前工作目录下创建一个名为 `filename` 的新文件。
    E. 没有创建目录，也没有创建文件。

- 10. 尝试编译并执行以下代码片段的结果是什么？假设该代码片段是一个在当前工作目录具有写权限的应用程序的一部分。
    ```java
    try {
        FileOutputStream fos = new FileOutputStream("datafile*");
        DataOutputStream dos = new DataOutputStream(fos);
        RandomAccessFile raf = new RandomAccessFile("xx", "rw");
        BufferedOutputStream bos = new BufferedOutputStream(raf);
        dos.writeInt(3);
        dos.close();
        fos.close();
        raf.close();
    } catch (IOException e) { }
    ```
    A. 2
    B. 8
    C. 12
    D. 16
    E. 字节数取决于底层系统。

- 6. 下面代码片段在第 9 行打印什么？
    ```java
    FileOutputStream fos = new FileOutputStream("xx*");
    for (byte b=0; b<50; b++)
        fos.write(b);
    fos.close();
    RandomAccessFile raf = new RandomAccessFile("xx", "r");
    raf.seek(10);
    int i = raf.read();
    raf.close();
    System.out.println("i = " + i);
    ```
    A. 输出是 i = 30。
    B. 输出是 i = 20。
    C. 输出是 i = 10。
    D. 没有输出，因为代码在第 1 行抛出了异常。
    E. 没有输出，因为代码在第 5 行抛出了异常。

- 7. 使用以下代码创建一个文件：
    ```java
    FileOutputStream fos = new FileOutputStream("datafile*");
    DataOutputStream dos = new DataOutputStream(fos);
    for (int i=0; i<500; i++)
        dos.writeInt(i);
    ```
    你想写代码从该文件中读取数据。哪些解决方案是有效的？（选择所有适用项）
    A. 构造一个 `FileInputStream`，传入文件名。在 `FileInputStream` 上链式调用一个 `DataInputStream`，并调用其 `readInt()` 方法。
    B. 构造一个 `FileReader`，传入文件名。调用文件读取器的 `readInt()` 方法。
    C. 构造一个 `PipedInputStream`，传入文件名。调用管道输入流的 `readInt()` 方法。
    D. 构造一个 `RandomAccessFile`，传入文件名。调用随机访问文件的 `readInt()` 方法。
    E. 构造一个 `FileReader`，传入文件名。在 `FileReader` 上链式调用一个 `DataInputStream`，并调用其 `readInt()` 方法。

- 8. 下面哪个是正确的？
    A. `Readers` 有可以读取并返回 `float` 和 `double` 的方法。
    B. `Readers` 有可以读取并返回 `float` 的方法。
    C. `Readers` 有可以读取并返回 `double` 的方法。
    D. `Readers` 有可以读取并返回 `int` 的方法。
    E. 以上都不是。

- 9. 你在一个空目录下执行以下代码。结果是什么？
    ```java
    File f1 = new File("dirname");
    File f2 = new File(f1, "filename");
    ```
    A. 在当前工作目录下创建一个名为 `dirname` 的新目录。
    B. 在当前工作目录下创建一个名为 `dirname` 的新目录。在 `dirname` 目录下创建一个名为 `filename` 的新文件。
    C. 在当前工作目录下创建一个名为 `dirname` 的新目录和一个名为 `filename` 的新文件。
    D. 在当前工作目录下创建一个名为 `filename` 的新文件。
    E. 没有创建目录，也没有创建文件。
