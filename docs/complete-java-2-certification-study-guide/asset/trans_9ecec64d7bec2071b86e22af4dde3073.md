

# 匿名类声明

正如你所看到的，声明和构造匿名内部类的代码结构如下：

```
new Xxx() { /* 类体。 */ };
```

其中 Xxx 是类名或接口名。重要的一点是，理解这种形式的代码是一个向对象返回值的*表达式*（expression）。它本身是不完整的，但可以用在任何可以使用对象引用的地方。例如，你可能将构造对象的引用赋值给变量，如下所示：

```
Xxxx anXxxx = new Xxx() { /* 类体。 */ };
```

注意，你必须确保写一个完整的语句，包括末尾的分号。或者，你也可以将构造对象的引用作为方法的参数。在这种情况下，其整体形式为：

```
someMethod(new Xxx() { /* 类体。 */ });
```

# 在匿名内部类的构造中传递参数

如果匿名内部类继承另一个类，且父类具有带参数的构造函数，你可以通过在构造匿名内部类时指定参数列表，来安排调用其中任何一个构造函数。接下来的是一个示例：

```
// 假设这段代码出现在某个方法中
Button b = new Button("Anonymous Button") {
    // 按钮的行为
};
对按钮 b 进行一些操作...
```

在这种情况下，编译器会为你的匿名内部类构建一个构造函数，该构造函数实际上会使用提供的参数列表调用父类构造函数，类似于：

```
// 这不是你写的代码！这演示了当你被编译类似上面的示例时，
// 内部创建的内容
class AnonymousSubclass extends Button {
    public AnonymousSubclass(String s) {
    }
}
```

这并不是实际的代码——但它传达了核心思想。

# 初始化匿名内部类

有时你可能想在构造内部类时执行某种初始化。在普通类中，你会创建一个构造函数。在匿名内部类中，你无法这样做，但可以使用从 JDK 1 开始引入语言的初始化器功能。如果你在类作用域内提供一个未命名的块，那么它将作为构造过程的一部分被调用，如下：

```java
public MyClass {
  // 初始化器
  System.out.println("Creating an instance");
}
```

这适用于任何类，但这种技术对于内部类来说特别有用，因为它是你拥有的唯一可以对构造提供某些控制的工具。

# 匿名类的复杂示例

现在让我们来看一个遵循之前示例的完整示例。这个示例使用了两个内部类（一个嵌套在另一个内部）；一个初始化器；以及一个带参数的构造函数：

```java
import java.awt.*;
import java.awt.event.*;

class X extends Frame {
    private int count;

    public static void main(String[] args[]) {
        X x = new X();
        x.pack();
        x.setVisible(true);
        final l = new Label("Count = " + count);
        add(l, BorderLayout.SOUTH);
        add(new ActionListener() {
            public void actionPerformed(ActionEvent ev) {
                count++;
                l.setText("Count = " + count);
            }
        }, BorderLayout.NORTH);
        add(new MouseAdapter() {
            public void mousePressed(MouseEvent ev) {
                // ...
            }
        });
    }
}
```

第 19–29 行构成了初始化器并在 Button 上的监听器；正如我们之前提到的，我们可以任意嵌套这些内容。注意在第 14 行声明的标签变量是 `final` 的；这允许从内部类访问它。

# 合约与命名规范

在编程中，正如生活中一样，合约（contract）是关于行为的约定；每一方都同意以可预测的方式行动，并获得预期对方产生预测行为的权利。更准确地说，合约是规定某些类方法行为的约定。Java 中最常见的两个合约是 `equals` 合约和 `hashCode`。它们描述了任何 `equals()` 或 `hashCode()` 方法的预期行为。如果一个类的 `equals()` 和 `hashCode()` 遵循该合约，许多有用的类就可以受益，这在第 8 章“java.lang 和 java.util 包”中有描述。

`equals` 合约在 java.Object 的 API 页面上有详细描述，它包含几个部分，其中重要的有：

- 任何对象都应该等于它。
- 如果 x 等 y，则 y 等 x。
- 如果 x 等 y 且 y 等 z，则 x 等 z。

从 Object 继承的 `equals()` 版本使用 `==` 运算符来测试相等性。如果你重写了此行为，编译器将无法知道你的新版本是否遵循该合约。你的选择是确保它遵循合约，或者放弃（例如）Collections 框架带来的好处。如果你违反了合约但仍然使用集合，产生的 bug 可能非常难以追踪（这是一个有用信息：如果你有一个与将类存储在集合中相关的难以捉摸的 bug，请检查你的 `equals()` 和 `hashCode()` 方法以确保它们遵循其合约）。

`hashCode` 规定了 `hashCode()` 方法的行为。哈希码是一个表示对象唯一性的 `int`；它被那些需要高效方法判断两个对象是否包含不同值的类使用。该合约在 java.lang.Object 的 API 页面 `hashCode()` 方法描述中指定。它要求如果两个对象根据它们的 `equals()` 方法是相等，那么它们必须具有相同的哈希码。注意，反过来并不是合约的一部分；不等的对象具有相同的哈希码是可以的。

考虑一个 `Point3D` 类，表示三维空间中的一个点。一个合理的实现如下：

```java
public class Point3D {
    private int x, y, z;

    public boolean equals(Object ob) {
        Point3D that = (Point3D) ob;
        return this.x == that.x &&
               this.y == that.y &&
               this.z == that.z;
    }

    public int hashCode() {
        return x + y + z;
    }
}
```

该类的两个实例如果它们的 x、y 和 z 值匹配，则是相等的。显然，哈希码被遵循了。注意，不等的实例可能具有相同的哈希码。例如，一个实例的值可能是 (100, 200, 300)，而另一个的值可能是 (600, 1, -1)。这是可以接受的。但是，请注意，集合类在处理具有相同哈希码的不等对象时可能会变慢。

一个哈希码算法会在检测唯一性和高效运行之间取得一个合理的平衡。你可以通过编写对唯一性非常严谨的 `hashCode()` 方法来避免缓慢的冲突，但如果你严谨的 `hashCode()` 方法效率低下，那么提高集合效率也无济于事。例如，你可能会考虑以下 Point3D 的替代备用 `hashCode()` 版本：

```java
public int hashCode() {
    return (int)(Math.pow(2, x) +
                 Math.pow(3, y) +
                 Math.pow(5, z));
}
```

这个版本不太可能为不等的对象返回相同的代码，因此包含 Point3D 实例的集合将是高效的，但那三次幂运算将使 `hashCode()` 方法运行过缓慢。

