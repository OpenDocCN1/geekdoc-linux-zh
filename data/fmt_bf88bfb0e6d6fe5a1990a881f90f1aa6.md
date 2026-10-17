
```java
package different;
class Complex {
    protected void apply() { //. }
}
```

图 3.2 显示了子类合法的访问类型。具有某种特定访问类型的方法可以被不同访问类型的方法重写，前提是图中存在从原始类型到新类型的路径。

## 图 3.2 合法的被重写方法访问类型

![](img/09f8389b7ae2705d1ab14be2d5e857e3_113_0.png)

- 重写规则可以总结为：
- 私有方法（`private` method）可以被私有、默认（`default`）、保护（`protected`）或公共（`public`）方法重写。
- 默认方法可以被默认、保护或公共方法重写。
- 保护方法可以被保护或公共方法重写。

图 3.3 显示了子类不法的访问类型。即使图中存在从原始类型到新类型的路径，具有某种特定访问类型的方法也不被不同访问类型的方法遮蔽。

## 图 3.3 不法的被重写方法访问类型

![](img/09f8389b7ae2705d1ab14be2d5e857e3_113_1.png)

- 不法的重写组合可以可以总结如下：
- 默认方法不能被私有方法重写。
- 保护方法不能被默认或私有方法重写。
- 公共方法不能被保护、默认或私有方法重写。

## 其他修饰符

在本节中，我们将讨论 Java 的其他修饰符，即：

- `final`
- `abstract`
- `static`
- `native`
- `transient`
- `volatile`
- `synchronized`

`transient` 和 `volatile` 修饰符在认证考试目标未提及，因此在本章中仅简要介绍。此外，`synchronized` 修饰符将在第 7 章“线程”中进行详细讨论。

与访问修饰符不同，上述列出的修饰符之间相互独立。每个修饰符对应一个不同的编程概念。一个特征可能有多个此类修饰符；在这种情况下，关键字出现的顺序并不重要。

并不是每个修饰符都能应用于每种特征。本章末尾表 3.2 总结了哪些修饰符适用于哪些特征。

## final

`final` 应用类、变量和方法。`final` 的含义随上下文而异，但核心思想是相同的：`final` 特征不能被更改。

`final` 类不能被子类。例如，下面的代码将无法编译，因为 `java.lang.Math` 类是 `final` 的：

```java
class SubMath extends java.lang.Math { }
```

编译器错误显示：“Can't subclass final classes.（无法子类 final 类）”。

`final` 变量一旦赋值就不能被修改。在 Java 中，`final` 变量的作用类似于 C++ 中的常量和 C 中的 `#define` 常量。例如，`java.lang.Math` 类有一个类型为 `double` 的 `final` 变量，称为 `PI`。显然，`pi` 不是那种在程序执行期间应该更改的值。

如果 `final` 是指向对象的引用，那么保持不变的是引用，而不是对象本身。如下面的代码所示：

```java
class Walrus {
   int weight;
   Walrus(int w) { weight = w; }
}

class Tester {
   final Walrus w1 = new Walrus(1500);
   void test() {
       w1 = new Walrus(1400); // 非法
       w1.weight = 1800; // 合法
   }
}
```

这里的 `final` 变量是第 7 行声明的 `w1`。因为它是 `final`，`w1` 无法接收新值；第 9 行是非法的。然而，`w1` 内部的数据不是 `final` 的，第 10 行是完全合。换句话说：

- 你不能更改 `final` 对象引用变量。
- 你可以更改由 `final` 对象引用变量所引的对象所属的数据。

`final` 方法不能被重写。例如，以下代码将无法编译：

```java
class Mammal {
   final void getAround() { }
}


class Dolphin extends Mammal {
   void getAround() {
```

海豚活动的方式与哺乳动物不同，因此第 7 行的编译器错误显示“Final methods cannot be overridden.（final 方法不能被重写）”。

## abstract

`abstract` 修饰符可以应用于类和方法。抽象类不能被实例化，但可以被子类化。抽象方法没有实现，必须由第一个具体的子类重写。

考虑以下抽象类的示例：

```java
abstract class Shape {
   abstract void draw();
}

class Circle extends Shape {
   void draw() {
       System.out.println("Drawing a circle");
   }
}
```
`abstract` 修饰符用于定义子类遵循的模板，确保层次结构的一致性。

`static` 修饰符可以应用于变量和方法。你可以认为静态特征属于类，而不是与实例关联。静态方法不允许使用类的非静态特征。

以下示例了一个带有静态变量的简单类：

```java
class Ecstatic {
   static int x = 0;
   Ecstatic() { x++; }
}
```

变量 `x` 是静态的；这意味着无论有多少实例，只有一个 `x`。占据 4 字节的空间在 `Ecstatic` 加载时分配。第 2 行的初始化发生在类加载时。每调用一次构造函数，静态变量增加，因此可以知道创建了多少实例。

你有两种方式引用静态变量：

- 通过类的任何实例引用
- 通过类名

第一种方法可行，但会导致代码混乱并被认为是不规范的。以下示例说明了原因：

```java
Ecstatic e1 = new Ecstatic();
Ecstatic e2 = new Ecstatic();
e1.x = 100;
e2.x = 200;
reallyImportantVariable = e1.x;
```

如果你不知道 `x` 是静态的，你可能会认为 `reallyImportantVariable` 在第 5 行变为 100。实际上，它被设置为 200，因为 `e1.x` 和 `e2.x` 指向同一个（静态）变量。引用静态变量更好的方法是通过类名。以下代码与之前的代码相同：

```java
Ecstatic e1 = new Ecstatic();
Ecstatic e2 = new Ecstatic();
Ecstatic.x = 100; // 我为什么要这么做？
Ecstatic.x = 200;
reallyImportantVariable = Ecstatic.x;
```

现在很清楚第 3 行是没用的，`reallyImportantVariable` 的值在第 5 行变为 200。通过类名而非实例引用静态特征，产生的源代码能够更清晰地描述运行时发生的情况。

类。它们可以在类的单个实例构造之前被调用。每个 Java 应用程序都是例子，因为每个应用程序都有一个静态的 `main()` 方法：

```java
class SomeClass {
static int i = 48;
int j = 1;

public static void main(String args[]) {
i += 100;
// j *= 5; 幸运的是我们这行被注释掉了
}

```

当此应用程序启动时（即当有人在命令行输入 `java SomeClass` 时），不存在 `SomeClass` 类的实例。在第 6 行，自增的 `i` 是静态的，所以即使没有实例，它也存在。如果第 7 行没有被注释，将会导致编译器错误，因为 `j` 是非静态的。

实例方法有一个名为 `this` 的隐式变量，该变量是执行该方法的对象的引用。在静态代码中，你可以引用变量或方法，而无需指定指的是哪个对象的变量或方法。编译器假设你指的是 `this`。例如，考虑以下代码：

```java
class Xyzy {
int w;

void bumpW() {
w++;
}

```

在第 5 行，程序员没有指定要自增的对象的缩写。编译器假设第 5 行是 `this.w++` 的缩写。

对于静态方法，没有 `this`。如果你尝试在静态方法中访问实例变量或调用实例方法，你将得到一条显示为“Undefined variable:”的错误消息。“执行当前方法的那个对象”这个概念没有任何意义，因为不存在这样的实例。与静态变量一样，静态方法不与其类的任何特定实例关联。

如果静态方法需要访问非静态变量或调用非静态方法，它必须指定是类中的哪一个拥有该变量或执行该方法。对于任何写过带有 GUI 应用程序的人来说，这种情况非常熟悉：

```java
import java.awt.*;

public class MyFrame extends Frame {
MyFrame() {
   setSize(300, 300);
}

   public static void main(String args[]) {
   MyFrame theFrame = new MyFrame();
   theFrame.setVisible(true);
}
}
```

在第 9 行，静态方法 `main()` 构造了 `MyFrame` 类的实例。在下一行，使用实例来执行（非静态的）方法 `setVisible()`。这种技术桥接了静态到非静态的鸿沟，在应用程序中经常见到。

例如，以下代码将无法编译：

```java
class Cattle {
   static void foo() { }
}

class Sheep extends Cattle {
   void foo() {}
}
```

编译器会在第 6 行标记消息：“Static methods can't be overridden.”如果将第 6 行改为 `static void foo() { }`，则编译将成功。静态方法看起来可以被重写——父类和子类可以拥有具有相同名称、参数和返回类型的静态方法——但技术上这不被视为重写，因为这些方法是静态的。

总结静态方法：

- 静态方法只能访问其类的静态数据；
- 静态方法只能调用其类的静态方法；它不能调用非静态方法。
- 静态方法没有 `this`。
- 静态方法不能被重写为非静态。

## 静态初始化器

类包含不存在于方法体内的静态代码是合法的。类可以有一段由大括号包围并标记为 `static` 的初始化代码块。例如：

```java
public class StaticExample {
   static double d = 1.23;

static {
  System.out.println("Static code: d=" + d);
```

第 4 行似乎缺少什么。你可能会在那里看到一个完整的方法声明：`static void bump()`，而不是只是 `static`。第 4 行是完全有效的，被称为静态初始化代码。大括号内的代码在类加载时执行一次。在类加载时，所有静态初始化（如第 2 行）和所有浮动代码（如第 4-6 行）按照在类定义中的顺序执行。

此代码的输出是：

`Static code: d=1.23`

浮动初始化代码应该谨慎使用，因为它们很容易变得难以阅读。编译器支持类中的多个初始化块，但很少有理由使用多个。

## 静态导入与访问

你在第一章“语言基础”中看到过，类的静态特性可以使用 Java 1.5 的静态导入功能导入。静态数据和方法可以是本章讨论的任何访问模式：`public`、`private`、`protected` 和 `default`。当你考虑访问模式影响静态导入时，不需要考虑子类/类的关系（例如在考虑 `protected` 特性时必须这样做）。这是因为静态导入出现在包声明之后，类定义之前。记住，导入到源文件的命名空间，而不是类的定义中。源文件可以包含一个、几个或多个类定义，或者一个类定义都没有。

因此，访问模式与静态导入之间的交互非常简单：任何非私特性都可以静态导入到同包源文件中；只有 `public` 特性可以静态导入到不同包源文件中。这在表3.1中总结。

## 表3.1 访问与静态导入

| 访问模式 | 是否可以静态导入到同包源文件 | 是否可以静态导入到不同包源文件 |
| :--- | :--- | :--- |
| Public | 是 | 是 |
| Protected | 是 | 否 |
| Default | 是 | 否 |
| Private | 否 | 否 |

## native

`native` 修饰符只能引用方法。与 `abstract` 修饰符一样，`native` 表示方法体在其他处。对于抽象方法，体在子类中；对于 native 方法，体完全位于 Java 虚拟机 (JVM) 之外的库中。

Native 代码用非 Java 语言（通常是 C 或 C++）编写并针对目标机器类型编译。（因此违反了 Java 的平台无关性。）将 Java 移植到新平台的人编写大量的 native 代码来支持 GUI 组件、网络以及许多特定平台的功能。然而，应用程序程序员很少编写 native 代码。

考虑到上一节对静态代码的讨论，有一种技术值得关注。当调用 native 方法时，包含 native 代码的库必须加载并供 JVM 使用；如果没有加载，将会产生延迟。通过调用 `System.loadLibrary("library_name")` 来加载库，为了避免延迟，尽早进行此调用。程序员经常使用以下代码示例所示的技术，假设库名为 `MyNativeLib`：

```java
class NativeExample {
native void doSomethingLocal(int i);

static {
System.loadLibrary("MyNativeLib");
}
}
```

注意第 2 行的 native 声明，它声明 `doSomethingLocal(i)` 的实现位于本地库。第 4-6 行是静态初始化代码，因此它们在加载 `NativeExample` 类时执行；这确保了有人需要时库是可用的。

native 方法的调用者不需要知道方法是 native 的。调用方式与非 native 完全相同：

```java
NativeExample natex;
natex = new NativeExample();
natex.doSomethingLocal(0);
```

许多常用方法都是 native 的，包括 `Object` 类的 `clone()` 和 `notify()` 方法。

## transient

`transient` 修饰符仅适用于变量。trans 变量不作为对象状态的一部分存储。（如果你不熟悉对象持久化，在第12章“输入和输出”中有介绍）。

许多对象（特别是实现了 `Serializable` 或 `Externalizable` 接口的类）的状态会被序列化并写入 JVM 之外。这是通过将对象传递给 `ObjectOutputStream` 类的 `writeObject()` 方法来实现的。如果流链到 `FileOutputStream`，那么对象的状态就会被写入文件。在这两种情况下，都可以通过从 `ObjectInputStream` 读取来重构对象。

某些对象包含极其敏感的信息。考虑以下类：

```java
class WealthCustomer
extends Customer implements Serializable {
private float $wealth;
private String accessCode;
)
```

一旦对象被写入 JVM 之外的目标位置，Java 的安全机制都将失效。如果该类的实例被写入文件或互联网，某些人可以嗅探到访问代码。第 4 行应该标记为 `transient` 关键字：

```java
class WealthCustomer
extends Customer implements Serializable {
private float $wealth;
private transient String accessCode;
)
```

现在，`accessCode` 的值在序列化时不会被写入。

## volatile

`volatile` 修饰符并不常用。只有变量可以是 `volatile` 的；声明它们表示此类变量可能会被异步地修改，因此编译器会采取特殊的预防措施。`volatile` 变量在多处理器环境中具有研究价值。

## synchronized

`synchronized` 修饰符用于控制多线程程序中对关键代码的访问。多线程本身是一个非常广泛的话题，将在第 7 章中介绍。

## 修饰符与特性

并不是所有的修饰符都可以应用于所有的特性。顶层类不能为 `protected`。方法不能为 `transient`。`static` 是通用的修饰符，你可以将其应用于独立的代码块。

表 3.2 显示了特性与修饰符的所有可能组合。注意，这里的类严格指代顶层类（即不是内部类）。（内部类在第 6 章中介绍。）

表 3.2 特性与修饰符的所有可能组合

| 修饰符 | 类 | 变量 | 方法 | 构造函数 | 独立代码块 |
|---|---|---|---|---|---|
| public | 是 | 是 | 是 | 是 | 否 |
| protected | 否 | 是 | 是 | 是 | 否 |
