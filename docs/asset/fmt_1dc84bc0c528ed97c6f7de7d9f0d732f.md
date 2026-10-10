
```java
public class OuterOne {
  private int x;
  public class InnerOne {
    private int y;
    public void innerMethod() {
      System.out.println("y is " + y);
    }
  }
  public void outerMethod() {
    System.out.println("x is " + x);
  }
  public void makeInner() {
    InnerOne anInner = new InnerOne();
    anInner.innerMethod();
  }
  // other methods...
}
```

当你将此与之前的版本比较时，你会发现变化。首先，`innerMethod()` 现在不仅输出 `y`（定义在 `InnerOne` 中），而且第 6 行也输出了 `x`（定义在 `OuterOne` 中）。第二个变化是第 13-14 行，代码创建了 `Inner` 类的实例并对其调用了 `innerMethod()`。

有时，你需要在静态方法或某些没有可用实例的情况下创建内部类的实例。这种情况发生在 `main()` 方法中，或者当你需要从某个无关类对象的方法创建内部类时。你可以通过像使用外部类成员一样使用 `new` 操作符来实现。当然，你需要一个外部类的实例。以下代码是一个孤立的 `main()` 方法，可以添加到代码中以产生完整的示例：

```java
public static void main(String args) {
    OuterOne.Inner i = new OuterOne().new InnerOne();
    i.innerMethod();
}
```

从内部类实例的角度来看，在行内使用两个 `new` 语句是以下操作的简化方式：

```java
public static void main(String args[]) {
    OuterOne o = new OuterOne();
    OuterOne.Inner i = o.new InnerOne();
    i.innerMethod();
}
```

如果你尝试使用新操作在没有对外部类进行前缀引用的情况下构造内部类的实例，则假设该 `this` 是该类的的前缀引用。这种行为与你在普通成员访问和方法调用中发现的行为完全相同。在成员访问和方法调用中，在你尝试使用 `this` 引用时，确保该引用是有效的是非常重要的。静态方法不包含 `this` 引用，这就是为什么在这些情况下你必须采取特殊的努力。

## 成员类 (Member Classes)

到为止，我们还没有区分直接在类作用域内定义的类——即成员类——以及在方法内部定义的类。这两个作用域之间存在重要的区别，你需要在脑中明确这些区别。首先，我们将看看成员类特有的特征。

### 访问修饰符 (Access Modifiers)

类的成员（变量、方法或嵌套类）可以标记为 `private`、`protected` 或默认访问权限。这些修饰符对于成员类的含义与其他普通方法的含义是相同的，因此我们不会在这些问题上花费时间。如果你需要重新回顾这些概念，请参阅第 3 章。

### 静态内部类 (Static Inner Classes)

与任何成员一样，内部类也可以被标记为 `static`。当应用于变量时，`static` 该变量与类相关，而不是与类的任何特定相关。当应用于内部类时，其含义相似。具体来说，静态内部类没有对外部实例的引用。因此，静态内部类的方法无法使用 `this` 关键字（无论是隐式还是显式）来访问外部类的变量；然而，这些方法可以像普通类中适用于静态方法的规则一样，访问外部类的静态变量。在需要时，你可以预期在不需要外部类当前实例的情况下获得静态内部类的实例。这种构造的语法非常简单；只需使用内部类的全限定名称——即包含外部类名称的名称，如第 5 行下划线部分所示：

```java
public class MyOuter {
  public static class MyInner {
  }
  public static void main(String[] args) {
    MyInner aInner = new MyOuter.MyInner();
  }
}
```

## 第 6 章 · 对象与类 (Chapter 6 · Objects and Classes)

结果是，静态内部类实际上只是一个修改了命名方案的顶层类。事实上，你可以将静态内部类作为打包的扩展。

你不仅可以在另一个类内部声明一个类，还可以另一个类的方法内部声明一个类。我们接下来讨论这一点。

## 在方法内部定义的类 (Classes Defined inside Methods)

在本章的开头，我们提到嵌套类可以在任何块中声明，这意味着你可以在方法内部定义一个类。这与你已经看到的非常相似，但在这种情况下，有三个特殊点需要考虑。第一点是，在方法内部声明的任何内容都不是类的成员，并且对于该方法是局部的。直接结果是，声明为方法私有（`private`）的类无法通过任何访问修饰符访问；它们也无法被标记为 `static`。如果你想这些，你会发现这些规则与你在方法中进行的任何变量声明的规则是相同的。第二点是，从方法内部的内部类创建的对象可以部分访问外部类的变量。我们稍后将查看如何实现以及适用于此的限制。

最后，可以创建一个匿名类——字面意思是，一个没有指定名称的类——在处理事件监听器时这样做可能是优雅的。我们将在讨论了控制从内部类到外部块中方法变量的访问规则后，讨论这种技术。

## 访问成员变量 (Accessing Member Variables)

控制内部类变量的规则非常简单。任何变量（无论是局部变量还是形式参数）都可以被内部类的方法访问，前提是它被标记为 `final`。`final` 实际上是一个常量，所以要点很简单：对象可以访问外部类的变量，前提是该变量是 `final`。我们稍后将查看如何实现以及适用于此的限制。

让我们看一个例子：

```java
public class Outer {
  final int x = 10;
  class Inner {
    void print() {
      System.out.println(x);
    }
  }
  public static void main(String[] args) {
    Outer outer = new Outer();
    Outer.Inner inner = new outer.Inner();
    inner.print();
  }
}
```

## 内部类 189 (Inner Classes 189)

在这个示例中，第 12 行的 `Inner` 是内部类。在内部，第 14 行的 `print()` 方法访问了 `x`。然而，第 16 行和第 18 行是非法的，因为它们尝试访问局部变量 `x` 和 `a`。第 19 行是合法的，因为 `b` 是 `final` 变量。

```java
public class Outer {
  final int x = 10;
  class Inner {
    void print() {
      System.out.println(x);
    }
  }
  public static void main(String[] args) {
    Outer outer = new Outer();
    Outer.Inner inner = new outer.Inner();
    inner.print();
  }
}

public class Outer {
  final int x = 10;
  class Inner {
    void print() {
      System.out.println(y); // Error: y is not defined
    }
  }
  public static void main(String[] args) {
    Outer outer = new Outer();
    Outer.Inner inner = new outer.Inner();
    inner.print();
  }
}

public class Outer {
  final int x = 10;
  class Inner {
    void print() {
      x = 20; // Error: cannot assign to final variable x
    }
  }
  public static void main(String[] args) {
    Outer outer = new Outer();
    Outer.Inner inner = new outer.Inner();
    inner.print();
  }
}

public class Outer {
  final int x = 10;
  class Inner {
    void print(int y) {
      System.out.println(y);
    }
  }
  public static void main(String[] args) {
    Outer outer = new Outer();
    Outer.Inner inner = new outer.Inner();
    inner.print(20);
  }
}
```

## 匿名类 (Anonymous Classes)

有些类没有名称。这是一种避免为类命名的方便方法，但应该谨慎使用该功能。下面的示例显示了匿名类的典型用法：

```java
public void aMethod() {
  button.addActionListener(
    new ActionListener() {
      public void actionPerformed(ActionEvent e) {
        System.out.println("The action occurred");
      }
  });
}
```

### 匿名类的构造与初始化 (Construction and Initialization of Anonymous Classes)

你需要理解关于匿名类构造和初始化的一些点，以便在认证考试和现实生活中取得成功。看看这些问题。

正如你已经所见，类是在同一个地方声明和实例化的，这意味着匿名类在方法作用域内是唯一的；它们与成员具有匿名性。

#### 匿名类声明

正如你所看到的，声明和构造匿名内部类的代码结构如下：

```
new Xxx() { /* 类体。 */ };
```

其中 `Xxx` 是类名或接口名。重要的一点是，理解这种形式的代码是一个向对象返回值的表达式（expression）。它本身是不完整的，但可以用在任何可以使用对象引用的地方。例如，你可能将构造对象的引用赋值给变量，如下所示：

```
Xxxx anXxxx = new Xxx() { /* 类体。 */ };
```

注意，你必须确保写一个完整的语句，包括末尾的分号。或者，你也可以将构造对象的引用作为方法的参数。在这种情况下，其整体形式为：

```
someMethod(new Xxx() { /* 类体。 */ });
```

#### 在匿名内部类的构造中传递参数

如果匿名内部类继承另一个类，且父类具有带参数的构造函数，你可以通过在构造匿名内部类时指定参数列表，来安排调用其中任何一个构造函数。接下来的是一个示例：

```java
// 假设这段代码出现在某个方法中
Button b = new Button("Anonymous Button") {
    // 按钮的行为
};
// 对按钮 b 进行一些操作...
```

在这种情况下，编译器会为你的匿名内部类构建一个构造函数，该构造函数实际上会使用提供的参数列表调用父类构造函数，类似于：

```java
// 这不是你写的代码！这演示了当你被编译类似上面的示例时，
// 内部创建的内容
class AnonymousSubclass extends Button {
    public AnonymousSubclass(String s) {
    }
}
```

这并不是实际的代码——但它传达了核心思想。

#### 初始化匿名内部类

有时你可能想在构造内部类时执行某种初始化。在普通类中，你会创建一个构造函数。在匿名内部类中，你无法这样做，但可以使用从 JDK 1 开始引入语言的初始化器功能。如果你在类作用域内提供一个未命名的块，那么它将作为构造过程的一部分被调用，如下：

```java
public MyClass {
  // 初始化器
  System.out.println("Creating an instance");
}
```

这适用于任何类，但这种技术对于内部类来说特别有用，因为它是你拥有的唯一可以对构造提供某些控制的工具。

#### 匿名类的复杂示例

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
        final Label l = new Label("Count = " + count);
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

第 19–29 行构成了初始化器并在 `Button` 上的监听器；正如我们之前提到的，我们可以任意嵌套这些内容。注意在第 14 行声明的标签变量是 `final` 的；这允许从内部类访问它。

## 合约与命名规范

在编程中，正如生活中一样，合约（contract）是关于行为的约定；每一方都同意以可预测的方式行动，并获得预期对方产生预测行为的权利。更准确地说，合约是规定某些类方法行为的约定。Java 中最常见的两个合约是 `equals` 合约和 `hashCode`。它们描述了任何 `equals()` 或 `hashCode()` 方法的预期行为。如果一个类的 `equals()` 和 `hashCode()` 遵循该合约，许多有用的类就可以受益，这在第 8 章“java.lang 和 java.util 包”中有描述。

`equals` 合约在 `java.Object` 的 API 页面上有详细描述，它包含几个部分，其中重要的有：

- 任何对象都应该等于它。
- 如果 `x` 等 `y`，则 `y` 等 `x`。
- 如果 `x` 等 `y` 且 `y` 等 `z`，则 `x` 等 `z`。

从 `Object` 继承的 `equals()` 版本使用 `==` 运算符来测试相等性。如果你重写了此行为，编译器将无法知道你的新版本是否遵循该合约。你的选择是确保它遵循合约，或者放弃（例如）`Collections` 框架带来的好处。如果你违反了合约但仍然使用集合，产生的 bug 可能非常难以追踪（这是一个有用信息：如果你有一个与将类存储在集合中相关的难以捉摸的 bug，请检查你的 `equals()` 和 `hashCode()` 方法以确保它们遵循其合约）。

`hashCode` 规定了 `hashCode()` 方法的行为。哈希码是一个表示对象唯一性的 `int`；它被那些需要高效方法判断两个对象是否包含不同值的类使用。该合约在 `java.lang.Object` 的 API 页面 `hashCode()` 方法描述中指定。它要求如果两个对象根据它们的 `equals()` 方法是相等，那么它们必须具有相同的哈希码。注意，反过来并不是合约的一部分；不等的对象具有相同的哈希码是可以的。

考虑一个 `Point3D` 类，表示三维空间中的一个点。一个合理的实现如下：
