

如果你尝试使用新操作在没有对外部类进行前缀引用的情况下构造内部类的实例，则假设该 `this` 是该类的的前缀引用。这种行为与你在普通成员访问和方法调用中发现的行为完全相同。在成员访问和方法调用中，在你尝试使用 `this` 引用时，确保该引用是有效的是非常重要的。静态方法不包含 `this` 引用，这就是为什么在这些情况下你必须采取特殊的努力。

## 成员类 (Member Classes)

到为止，我们还没有区分直接在类作用域内定义的类——即成员类——以及在方法内部定义的类。这两个作用域之间存在重要的区别，你需要在脑中明确这些区别。首先，我们将看看成员类特有的特征。

## 访问修饰符 (Access Modifiers)

类的成员（变量、方法或嵌套类）可以标记为 `private`、`protected` 或默认访问权限。这些修饰符对于成员类的含义与其他普通方法的含义是相同的，因此我们不会在这些问题上花费时间。如果你需要重新回顾这些概念，请参阅第 3 章。

## 静态内部类 (Static Inner Classes)

与任何成员一样，内部类也可以被标记为 `static`。当应用于变量时，`static` 该变量与类相关，而不是与类的任何特定相关。当应用于内部类时，其含义相似。具体来说，静态内部类没有对外部实例的引用。因此，静态内部类的方法无法使用 `this` 关键字（无论是隐式还是显式）来访问外部类的变量；然而，这些方法可以像普通类中适用于静态方法的规则一样，访问外部类的静态变量。在需要时，你可以预期在不需要外部类当前实例的情况下获得静态内部类的实例。这种构造的语法非常简单；只需使用内部类的全限定名称——即包含外部类名称的名称，如第 5 行下划线部分所示：

1. public class MyOuter {
2.   public static class MyInner {
3.   }
4.   public static void main(String[] args) {
5.     MyInner aInner = new MyOuter.MyInner();
6. }
7. }

## 第 6 章 · 对象与类 (Chapter 6 · Objects and Classes)

结果是，静态内部类实际上只是一个修改了命名方案的顶层类。事实上，你可以将静态内部类作为打包的扩展。

你不仅可以在另一个类内部声明一个类，还可以另一个类的方法内部声明一个类。我们接下来讨论这一点。

## 在方法内部定义的类 (Classes Defined inside Methods)

在本章的开头，我们提到嵌套类可以在任何块中声明，这意味着你可以在方法内部定义一个类。这与你已经看到的非常相似，但在这种情况下，有三个特殊点需要考虑。第一点是，在方法内部声明的任何内容都不是类的成员，并且对于该方法是局部的。直接结果是，声明为方法私有（private）的类无法通过任何访问修饰符访问；它们也无法被标记为 `static`。如果你想这些，你会发现这些规则与你在方法中进行的任何变量声明的规则是相同的。第二点是，从方法内部的内部类创建的对象可以部分访问外部类的变量。我们稍后将查看如何实现以及适用于此的限制。

最后，可以创建一个匿名类——字面意思是，一个没有指定名称的类——在处理事件监听器时这样做可能是优雅的。我们将在讨论了控制从内部类到外部块中方法变量的访问规则后，讨论这种技术。

## 访问成员变量 (Accessing Member Variables)

控制内部类变量的规则非常简单。任何变量（无论是局部变量还是形式参数）都可以被内部类的方法访问，前提是它被标记为 `final`。`final` 实际上是一个常量，所以要点很简单：对象可以访问外部类的变量，前提是该变量是 `final`。我们稍后将查看如何实现以及适用于此的限制。

让我们看一个例子：

1. public class Outer {
2.   final int x = 10;
3.   class Inner {
4.     void print() {
5.       System.out.println(x);
6.     }
7.   }
8.   public static void main(String[] args) {
9.     Outer outer = new Outer();
10.    Outer.Inner inner = new outer.Inner();
11.    inner.print();
12.  }
13. }

## 内部类 189 (Inner Classes 189)

在这个示例中，第 12 行的 `Inner` 是内部类。在内部，第 14 行的 `print()` 方法访问了 `x`。然而，第 16 行和第 18 行是非法的，因为它们尝试访问局部变量 `x` 和 `a`。第 19 行是合法的，因为 `b` 是 `final` 变量。

1. public class Outer {
2.   final int x = 10;
3.   class Inner {
4.     void print() {
5.       System.out.println(x);
6.     }
7.   }
8.   public static void main(String[] args) {
9.     Outer outer = new Outer();
10.    Outer.Inner inner = new outer.Inner();
11.    inner.print();
12.  }
13. }

1. public class Outer {
2.   final int x = 10;
3.   class Inner {
4.     void print() {
5.       System.out.println(y); // Error: y is not defined
6.     }
7.   }
8.   public static void main(String[] args) {
9.     Outer outer = new Outer();
10.    Outer.Inner inner = new outer.Inner();
11.    inner.print();
12.  }
13. }

1. public class Outer {
2.   final int x = 10;
3.   class Inner {
4.     void print() {
5.       x = 20; // Error: cannot assign to final variable x
6.     }
7.   }
8.   public static void main(String[] args) {
9.     Outer outer = new Outer();
10.    Outer.Inner inner = new outer.Inner();
11.    inner.print();
12.  }
13. }

1. public class Outer {
2.   final int x = 10;
3.   class Inner {
4.     void print(int y) {
5.       System.out.println(y);
6.     }
7.   }
8.   public static void main(String[] args) {
9.     Outer outer = new Outer();
10.    Outer.Inner inner = new outer.Inner();
11.    inner.print(20);
12.  }
13. }

## 匿名类 (Anonymous Classes)

有些类没有名称。这是一种避免为类命名的方便方法，但应该谨慎使用该功能。下面的示例显示了匿名类的典型用法：

1. public void aMethod() {
2.   button.addActionListener(
3.     new ActionListener() {
4.       public void actionPerformed(ActionEvent e) {
5.         System.out.println("The action occurred");
6.       }
7.   }
8. );

## 匿名类的构造与初始化 (Construction and Initialization of Anonymous Classes)

你需要理解关于匿名类构造和初始化的一些点，以便在认证考试和现实生活中取得成功。看看这些问题。

正如你已经所见，类是在同一个地方声明和实例化的，这意味着匿名类在方法作用域内是唯一的；它们与成员具有匿名性。

