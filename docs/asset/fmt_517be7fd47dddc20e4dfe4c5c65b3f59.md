
```java
}
  public double distanceTo(Point other) {
    double dx = x - other.x;
    double dy = y - other.y;
    return Math.sqrt(dx * dx + dy * dy);
  }
```

```java
public Point(double nx, double ny) {
    x = nx;
    y = ny;
}
```

}

正如你所看到的，构造函数的定义方式与方法相似，但它的名称必须与类名相同，并且它不返回任何值（即使不返回 `void`）。

在列表 25.9 中，我们有了 `Example7`，它现在使用了我们刚刚为 `Point` 类定义的构造函数。

# 列表 25.9 示例 7

```java
public class Example7 {
  public static void main(String args[]) {
    Point a = new Point(2.3, 4.5);
    Point b = new Point(-5.2, 1.1);
    System.out.println(a.distanceTo(b));
  }
}
```

与之前的实现相比，这看起来好多了，不是吗？程序不再需要关心初始化 `Point` 的许多细节；这些细节都留给了它的构造函数。

一个类必须始终有一个构造函数。如果你不定义它，编译器就会自动为你生成一个。编译器生成的构造函数始终是一个无参数的构造函数，这允许我们在之前的示例中编写 `new Point()`。现在我们已经定义了自己的构造函数，编译器就不会再生成无参数的构造函数来用于创建新的 `Point` 实例了。如果你希望既有一个带参数的构造函数，又仍然能够使用无参数的构造函数，那么你就必须手动添加它。你可以这样定义它：

```java
public Point() {
}
```

你可以在类中拥有任意数量的构造函数。唯一的规则是，其签名——即参数的数量和类型——必须与其它构造函数的签名不同。

虽然对象本身已经是编程语言中一个强大的概念了，但另一种增加语言强大性的方法是实现对象继承，它允许你将两个不同但相似的对象联系起来。

# 继承

假设你还需要定义一个数据结构来操作地理位置的概念。地理位置由一组坐标对 `(x,y)` 和一个名称定义。你可以复制 `Point` 类的源代码并将其粘贴到名为 `Location.java` 的新文件中，然后进行你需要的更改。但有一种更好的方法：继承。

当类 `B` 继承自类 `A` 时，它自动拥有与类 `A` 相同的成员。这包括数据成员和方法成员。类 `B` 在继承类 `A` 的所有成员之外，还可以定义它自己的新成员，或者提供替代的方法定义来替换它从 `A` 继承来的定义。

# 继承示例

这是一个关于如何通过继承 `Point` 类来定义地理位置的示例：

```java
public class Location extends Point {
    public String name;
    public void print() {
        System.out.println(name + ": " + x + ", " + y + ":");
    }
    public Location(String nn, double nx, double ny) {
        super(nx, ny);
        name = nn;
    }
}
```

我们使用了 `extends` 关键字来表示 `Location` 继承自 `Point`。继承可以解释为一种“是一种”（is-a）的关系。换句话说，可以说 `Location` 是一种特殊的 `Point`。有时，我们说 `Point` 是 `Location` 的超类，`Location` 是 `Point` 的子类。我们也可以说 `Point` 是父类，`Location` 是类类

# 开发环境
第四部分

## 使用继承类

乍一看，这可能看起来很奇怪，甚至像是一个错误，但如果你仔细考虑，就会发现它是正常的。毕竟，`Location` 是 `Point`。注意，反过来并不成立：`Point` 不一定是 `Location`。创建一个 `Location` 数组并尝试将通用的 `Point` 作为其元素之一存储，会导致编译错误。

当我们要求数组中引用的每个对象进行打印时，更加神奇了，它们都会自动调用正确的 `print` 方法。当你运行程序时，得到如下输出：

```
$ java Example8
New York: (10.2, 20.3)
San Francisco: (-7.0, -4.5)
30.10078859140207
(3.0, 4.0)
New York: (10.2, 20.3)
San Francisco: (-7.0, -4.5)
```

继承是面向对象编程中最有特性之一。它允许我们创建通用程序，遍历数据结构并要求每个元素执行某些操作（例如打印自身），而无需知道数据结构中存储的所有类型。如果将来我们决定添加另一种类型的对象，只需要为它提供自己的 `print` 方法，无需修改通用程序的任何行代码即可与新对象协作。

# 静态变量

可能你还希望应用程序知道创建了多少 `Point` 对象。实现此点的最佳方法是在类本身维护一个计数器，每创建一个新的 `Point` 实例就增加一次。

列表 25.11 是修改后的 `Point.java`，用于跟踪已创建的 `Point` 数量。

+ 列表 25.11 带修订的 `Point` 类

```java
public class Point {
    public static int count;
    public double x;
    public double y;
    public void print() {
        System.out.println("(" + x + ", " + y + ")");
    }
    public double distanceTo(Point other) {
        double dx = x - other.x;
```

    continues

# 804 开发环境
第四部分

## 列表 25.11 续

```java
double dy = y - other.y;
return Math.sqrt(dx * dx + dy * dy);
public Point(double nx, double ny) {
  count++;
  x = nx;
  y = ny;
}
public Point() {
  count++;
}
```

你会注意到我们添加了一个名为 `count` 的变量，并且我们将该变量声明为 `static`（静态）。`static` 是什么意思？在这里，它表示所有 `Point` 类的实例都共享同一个 `count` 变量。如果我们不使用 `static` 关键字，那么每个 `Point` 都将拥有自己的 `count` 变量副本，这对于我们的目的来说是毫无用处的。

作为补充，每个构造函数都经过了修改，每当创建一个 `Point` 对象时，`count` 变量就会加一。

在列表 25.12 中，示例 9 显示了通过在变量名前加上类名和点运算符（`.`）来访问静态变量。换句话说，你不需要实例即可访问静态变量。有时，静态变量被称为类变量，而非静态变量则被称为实例变量。

## 列表 25.12 示例9

```java
public class Example9 {
  public static void main(String[] args[]) {
    new Point();
    new Point();
    new Location("Mexico", 10, 20);
    System.out.println(Point.count);
  }
}
```
