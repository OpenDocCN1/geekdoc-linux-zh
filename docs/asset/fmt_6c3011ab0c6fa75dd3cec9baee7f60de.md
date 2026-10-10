
### 1. 考虑这个类

```java
public class Test1 {
    public float aMethod(float a, float b) {
    }
}
```

如果在第 4 行（单独地）添加，以下哪些方法是合法的？（多选）

*   `public int aMethod(int a, int b) { }`
*   `public float aMethod(float a, float b) { }`
*   `public float aMethod(float a, float b, int c) throws Exception { }`
*   `public float aMethod(float c, float d) { }`
*   `private float aMethod(int a, int b, int c) { }`

### 2. 考虑这些定义在单独源文件中的类

```java
public class Test1 {
    public float aMethod(float a, float b)
        throws IOException ...
    }
}
```

```java
public class Test2 extends Test1 {
    
}
```

在类 `Test2` 的第 2 行（单独地）使用以下哪些方法是合法的？（多选）

*   `float aMethod(float a, float b) {...}`
*   `public int aMethod(int a, int b) throws Exception {...}`
*   `public float aMethod(float a, float b) throws Exception {...}`
*   `public float aMethod(float p, float q) {...}`

### 3. 你获得了一份用于 Java 实现的兽医注册系统设计文档。它写道：

> “宠物有一个所有者、一个注册日期和一个疫苗接截止日期。猫是一种宠物，它有一个指示其是否已绝育的标记，以及对其斑纹的文本描述。”

鉴于 `Pet` 已经定义，以下哪些字段将适合作为成员包含在 `Cat` 中？（多选）

*   `pet;`
*   `Date registered;`
*   `Date vaccinationDue;`
*   `Cat;`
*   `boolean neutered;`
*   `String markings;`

### 4. 你获得了一份用于 Java 实现的兽医注册系统设计文档。它写道：

> “宠物有一个所有者、一个注册日期和一个疫苗接截止日期。猫是一种宠物，它有一个指示其是否已绝育的标记，以及对其斑纹的文本描述。”

鉴于 `Pet` 已经定义，且你预计 `Cat` 类在整个应用程序中自由使用，你将如何编写 `Cat` 的声明（不包括第一个大括号的内容）？仅使用这些词：`boolean`, `class`, `Date`, `extends`, `Object`, `Pet`, `private`, `protected`, `public`, `String`。

*   `protected class extends Owner`
*   `public class extends Object`
*   `public class extends Pet`
*   `private class extends Pet`

### 5. 考虑以下定义在单独文件中的类

```java
public class Base {
    public void method(int i) {
    }
}

public class Sub {
    public void method(int j) {
    }
}
```

*   知道当类没有显式构造函数时，编译器会生成一个默认构造函数。当类有构造函数代码时，则不会生成默认构造函数。
*   理解对父类构造函数的调用链。每次构造函数调用都从调用父类构造函数开始。
*   知道如何创建一个调用非默认父类构造函数的构造函数。理解 `super` 关键字的使用。
*   能够识别构造正确的内部类，包括方法中的内部类和匿名内部类。这些形式的每种语法在本章之前的节中已解释。
*   知道外部类的哪些数据和方法是内部类可用的。理解内部类可以访问其外部类的所有数据和方法。
*   理解静态内部类的限制。理解静态内部类无法访问其外部类的非静态特征。
*   知道如何从外部类的静态方法使用非静态内部类。能够识别新的 `Outer().new Inner()` 格式。
*   知道如何使用枚举以及何时适合使用它们。枚举是旨在替换枚举常量的类。你应该能够识别一组（旧式的）枚举常量，并知道如何创建适当的枚举来替换这些常量的。

## 复习题

### 11. 下列哪项重写了签名名为 `void xyz(float f)` 的方法？

*   `void xyz(float f)`
*   `public void xyz(float f)`
*   `private void xyz(float f)`
*   `public int xyz(float f)`
*   `private int xyz(float f)`

### 12. 下列哪些是正确的？（选择所有适用项）

*   枚举定义应该声明它扩展了 `java.lang.Enum`。
*   枚举可以被子类化。
*   枚举可以包含公共方法定义。
*   枚举可以包含私有数据。

### 13. 下列哪些是正确的？（选择所有适用项）

*   枚举定义可以包含程序的 `main()` 方法。
*   你可以调用枚举的 `toString()` 方法。
*   你可以调用枚举的 `wait()` 方法。
*   你可以调用枚举的 `notify()` 方法。

### 14. 假设 `x` 和 `y` 的类型为 `TrafficLight`，这是一个枚举。测试 `x` 和 `y` 是否指向同一个常量的最佳方法是什么？

*   `if (x == y)`
*   `if (x.equals(y))`
*   `if (x.toString().equals(y.toString()))`
*   `if (x.hashCode() == y.hashCode())`

### 15. 下列哪些限制适用于匿名内部类？

*   它们必须定义在代码块内部。
*   它们只能读写外围类的 `final` 变量。
*   它们只能调用外围类的 `final` 方法。
*   它们不能调用外围类的 `synchronized` 方法。

### 16. 给定以下代码，下列哪项可以通过编译？

```java
enum Spice { NUTMEG, CINNAMON, CORIANDER, ROSEMARY; }
```

*   `Spice sp = Spice.NUTMEG; Object ob = sp;`
*   `Spice sp = Spice.NUTMEG; Object ob = (Object)sp;`
*   `Object ob = new Object(); Spice sp = object;`
*   `Object ob = new Object(); Spice sp = (Spice)object;`

### 17. 下列哪些是正确的？

*   匿名内部类最多可以实现一个接口。
*   匿名内部类可以实现任意多个接口。
*   匿名内部类可以扩展 `Object` 之外的父类。
*   实现一个接口的匿名内部类可以扩展 `Object` 之外的父类。
*   实现多个接口的匿名内部类可以扩展 `Object` 之外的父类。

### 18. 哪些方法返回枚举常量的名称？

*   `getName()`
*   `name()`
*   `toString()`
*   `toString()`
*   `getString()`

### 19. 假设类 `X` 包含以下方法：

```java
void doSomething(int a, float b) { ... }
```

下列方法可能出现在扩展 `X` 的类 `Y` 中？

*   `public void doSomething(int a, float b) { }`
*   `private void doSomething(int a, float b) { }`
*   `public void doSomething(int a, float b) throws java.io.IOException { }`
*   `private void doSomething(int a, float b) throws java.io.IOException { }`

### 20. 此题涉及 `IOException`、`AWTException` 和 `EOFException`。它们都是检查异常类型。`IOException` 和 `AWTException` 扩展 `Exception`，而 `EOFException` 扩展 `IOException`。假设类 `X` 包含以下方法：

```java
void doSomething() throws IOException { ... }
```

下列方法可能出现在扩展 `X` 的类 `Y` 中？

*   `void doSomething() { }`
*   `void doSomething() throws AWTException { }`
*   `void doSomething() throws EOFException { }`
*   `void doSomething() throws IOException, EOFException { }`

## 复习题答案

*   1. `A`, `C`, `E`. 在这些项中，参数列表与原始方法不同，属于重载。重载方法实际上是独立的，对访问权限、返回类型或可能抛出的异常没有限制。`B` 会是一个合法的重写方法，但它不能是 `private`。
*   2. `C`, `D`. 枚举不能扩展其他类或被子类化，但它可以包含公共方法和私有数据。
*   3. `A`, `B`, `C`, `D`. 枚举可以有 `main` 方法，并且它们继承自 `Object`，因此拥有 `toString()`、`wait()` 和 `notify()`。
*   4. `A`. 由于枚举常量是常量，`==` 运算符是比较它们最可靠且快速的方法。
*   5. `A`. 匿名内部类必须定义在块中。对于访问外围类的非 `final` 成员没有其他限制。
*   6. `A`, `B`. `Spice` 是 `Object` 的子类，因此它可以赋值给 `Object`。`C` 和 `D` 因为类型不匹配非法。
*   7. `B`, `C`, `D`. 内部类可以实现多个接口或扩展一个父类，但不能同时兼得。
*   8. `B`. `name()` 方法专门用于返回枚举常量的名称。
*   9. `A`, `B`, `C`. 重写允许更改访问级别（使其更宽）或添加异常，但不能缩小范围或移除它们。
*   10. `A`, `B`, `C`, `D`. 子类方法可以移除异常或添加更具体的异常，但不能抛出更宽泛的异常。
*   16. `A`, `B`, `D`. 枚举（`Enums`）可以像其他对象一样转换为 `Object`。因此 `A` 和 `B` 是合法的，尽管 `B` 中的强制转换是不必要的。将 `Object` 赋值给枚举需要强制转换，因此 `C` 是非法的，但 `D` 是合法的。
*   17. `A`, `C`. 匿名内部类可以实现单个接口，也可以扩展除 `Object` 以外的父类，但两者不可兼得。
*   18. `B`, `C`. `name()` 和 `toString()` 都返回常量名，`name()` 是 `final` 的，但 `toString()` 可以被重写。
*   19. `A`. 具有默认访问权限（`default access`）的方法可以被重写为默认、保护（`protected`）或公共（`public`）权限，但不能是私有（`private`）权限，因为不能用更严格的权限重写方法。重写的方法不能声明父类版本中未出现的异常类型。
*   20. `A`, `C`, `D`. 重写的方法可以抛出无限数量的异常类型，只要所有类型都与重写版本声明的异常列表中的类型相同，或者是这些类型的子类。

# 第 6 章 • 对象与类

# 第 7 章

## 线程

本章涵盖的 Java 认证目标：

*   4.1 使用 `java.lang.Thread` 和 `java.lang.Runnable` 编写代码定义、实例化并启动新线程。
*   4.2 识别线程可以存在的状态，并识别线程从一个状态转换到另一个状态的方法。
*   4.3 给定场景，编写代码合理利用对象锁来保护静态或实例变量免受并发访问问题。
*   4.4 给定场景，编写代码合理利用 `wait`、`notify` 或 `notifyAll`。

![](img/09f8389b7ae2705d1ab14be2d5e857e3_247_0.png)

线程是 Java 让单个 Java 虚拟机（`JVM`）看起来像许多同时运行的机器的方式。这种效果通常是一种幻象：实际上只有一个 `JVM` 且通常只有一个 `CPU`，`CPU` 在 `JVM` 的各种线程之间切换，从而产生有多个 `CPU` 的错觉。`JVM` 线程在后台为你工作，监听用户输入、进行垃圾回收并执行各种其他任务。

作为一名 Java 程序员，你可以在单线程和多线程范式之间选择。单线程 Java 程序只有一个入口（`main()` 方法）和一个出口。指令按顺序执行，从开始到结束。多线程程序有一个第一个入口（`main()` 方法），随后是其他方法的多个入口和出口，这些方法可能被调度为与 `main()` 方法并发运行。

Java 为你提供了创建和管理线程的工具。线程对于允许将无关、松散相关或紧密相关的工作进行分离且并发的非常有价值。

认证考试要求你熟悉 Java 的线程支持，包括线程之间创建、控制和通信的机制。本章将从线程编程的基础知识开始。之后，你将学习基础的线程控制技术，然后进入核心问题：监器编程（`monitor programming`）。

# 线程基础

Java 的线程支持存在于三个地方：

*   `java.lang.Thread` 类
*   `java.lang.Object` 类
*   Java 语言和 `JVM`

在本节中，你将学习线程编程的一些底层概念，包括线程执行时到底发生了什么、执行结束后发生了什么、基本线程状态、优先级和守护线程（`daemon threads`）。

# 线程执行的内容

要让线程执行，你需调用它的 `start()` 方法。这样做会将线程注册到一段称为线程调度器（`thread scheduler`）的系统代码中。调度器可能是 `JVM` 的一部分，也可能是宿主操作系统的一部分。

![](img/09f8389b7ae2705d1ab14be2d5e857e3_248_0.png)

调度器决定在任何给定时刻每个可用 `CPU` 上运行哪个线程。注意，调用线程的 `start()` 方法不会立即导致线程运行；它只是让线程具备运行的资格。线程仍然必须与其他所有线程争夺 `CPU` 时间。如果一切顺利，调度器将在未来的某点允许你的线程执行。

在它的整个生命周期内，线程花部分时间执行任务，部分时间处于各种状态。在本节中，我们将查看线程实际执行的内容，即 `run()` 方法。当前的问题是：当线程执行时，它在做什么？你有两个选择：

*   线程执行它自己的 `run()` 方法。
*   线程执行其他对象的 `run()` 方法。

如果你想让线程执行它自己的 `run()`，你必须继承 `Thread`。例如：

```java
public class CounterThread extends Thread {
    public void run() {
        for (int i = 1; i <= 10; i++) {
            System.out.println("Counting: " + i);
        }
    }
}
```

要启动线程，你调用 `start()` 方法。

### 等等，如果调用 `run()` 方法而不是 `start()` 会怎样？

如果你这样做，`run()` 方法就像其他方法一样被调用，并由当前线程执行，而不是由新线程。这是一个常见的错误。

另一个选择是实现 `Runnable`。例如，从 10 计数到 1：

```java
public class DownCounter implements Runnable {
    public void run() {
        for (int i = 10; i >= 1; i--) {
            System.out.println("Counting Down: " + i);
        }
    }
}
```

要启动此线程，你必须将 `Runnable` 实例传递给 `Thread` 构造函数，然后调用 `start()`:

```java
DownCounter dc = new DownCounter();
Thread t = new Thread(dc);
t.start();
```

`Runnable` 接口通常更好，因为它允许类扩展另一个类。`Runnable` 接口本身描述了一个单一方法：

```java
public interface Runnable {
    void run();
}
```

线程调度器是决定哪个线程在哪个 `CPU` 上运行的组件。调度器是 `JVM` 或宿主操作系统的一部分。调度器决定在任何给定时刻每个可用 `CPU` 上运行哪个线程。注意，调用线程的 `start()` 方法不会立即导致线程运行；它只是让线程具备运行的资格。线程仍然必须与其他所有线程争夺 `CPU` 时间。

总结来说，你可以使用两种方法来指定由线程执行哪个 `run()` 方法：
