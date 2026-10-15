
当 `Employee` 对象存在时，成员 `count` 可以在 `Employee` 对象的任何方法中使用——此示例在构造函数（第 18 行）中增加它，并在 `finalize` 方法（第 28 行）中减少它。当不存在 `Employee` 类对象时，仍然引用成员 `count`，但只能通过调用公共静态方法 `getCount`（第 46–49 行），例如 `Employee.getCount()`，它返回内存中 `Employee` 对象的数量。当对象存在时，也可以通过任何 `Employee` 对象的引用调用 `getCount` 方法，例如调用 `e1.getCount()`。

## 编程规范 8.1

> 使用类名和点（`.`）调用每个静态方法，以强调所调用的方法是静态方法。

注意 `Employee` 类有一个 `finalize` 方法（第 26–31 行）。包含此方法仅是为了显示在此程序中垃圾回收器的执行情况。

`finalize` 通常被声明为 `protected`，因此它不是类公共服务的一部分。我们将在第 9 章中详细讨论 `protected` 成员访问修饰符。

`EmployeeTest` 方法 `main`（图 8.13）实例化两个 `Employee` 对象（第 13–14 行）。当调用每个 `Employee` 对象的构造函数时，图 8.12 的第 15–16 行将 `Employee` 的名字赋值给实例变量 `firstName` 和 `lastName`。注意，这些语句并没有复制原始字符串。。实际上，Java 中的 `String` 对象是不可变的——它们在创建后就无法被修改。因此，对一个 `String` 对象拥有多个引用是安全的。这在 Java 的大多数其他类中通常不是这样的。如果 `String` 是不可变的，你可能会疑惑为什么我们能够使用 `+` 和 `+=` 运算符来拼接 `String`。字符串拼接操作实际上会产生包含拼接值的新 `String`。原始字符串不会被修改。

当 `main` 方法完成对这两个 `employee` 对象的使用后，第 31–32 行将引用 `e1` 和 `e2` 设置为 `null`。此时，引用不再指向第 13–14 行中实例化的对象。这标记了这些对象等待垃圾回收，因为程序中不再有指向这些对象的引用了。

```
// Fig. 8.13: EmployeeTest.java

// 静态成员演示。

public class EmployeeTest {

    public static void main(String args[]) {

        // 在创建 Employees 之前显示 count 为 0

        System.out.printf("Employees before instantiation: %d\n",

            Employee.getCount());

        // 创建两个 Employees; count 应该为 2

        Employee e1 = new Employee("Susan", "Baker");

        Employee e2 = new Employee("Bob", "Blue");

        // 在创建两个 Employees 后显示 count 为 2

        System.out.printf("Employees after instantiation: %d\n", Employee.getCount());

        System.out.printf("via e1.getCount(): %d\n", e1.getCount());

        System.out.printf("via e2.getCount(): %d\n", e2.getCount());

        System.out.printf("via Employee.getCount(): %d\n", Employee.getCount());

        // 获取 Employees 的名字

        System.out.printf("Employee1: %s %s\nEmployee2: %s %s\n",

            e1.getFirstName(), e1.getLastName(),

            e2.getFirstName(), e2.getLastName());

        // 在此示例中，每个 Employee 只有一个引用。

        // 因此以下两个语句会导致 JVM 将每个

        // Employee 对象标记为待垃圾回收

        e1 = null;

        e2 = null;

        System.gc(); // 请求现在进行垃圾回收

        // 显示调用垃圾回收器后的 Employee 计数；显示的

        // count 取决于回收器是否立即执行以及 Employee 对象的

        // 数量可能是 0、1 或 2

        System.out.printf("%nEmployees after System.gc():%d\n",

        Employee.getCount());

    } // end main

} // end class EmployeeTest
```

```
Employees before instantiation: 0
Employee constructor: Susan Baker; count = 1
Employee constructor: Bob Blue; count = 2

Employees after instantiation:
via e1.getCount():2
via e2.getCount():2
via Employee.getCount():2

Employee 1: Susan Baker
Employee 2: Bob Blue

Employee finalizer: Bob Blue; count = 1
Employee finalizer: Susan Baker; count = 0

Employees after System.gc(): 0
```

Fig. 8.13 | 静态成员演示。（部分 2，共 2 部分。）

最终，垃圾回收器可能会回收这些对象的内存（或者操作系统将在程序终止时回收内存）。JVM 不保证垃圾回收器会执行（也不保证是否会执行），因此此程序在第 34 行（图 8.13）使用 `System` 类（`java.lang`）的静态方法显式调用了垃圾回收器，以指示垃圾回收器尽力尝试回收符合回收条件的对象。这仅仅是“尽力而为”，意味着没有对象或符合对象的子集被回收。在图 8.13 的示例输出中，垃圾回收器执行了第 30-39 行并显示了 `Employee` 计数。最后一行表示内存中的 `Employee` 对象数量为 0。输出的倒数第三行和倒数第二行显示 Blue 的 `Employee` 对象在 Susan 的 `Employee` 对象之前被终化（`finalized`）。你系统上的输出可能不同，因为不保证调用 `System.gc()` 时垃圾回收器会执行，也不保证它会按特定顺序回收对象。

## 8.13 final 实例变量 393

```java
 // 图. 8.15: Increment.java

// 类中的 final 实例变量。

public class Increment {

    private int total = 0; // 所有累加的总和

    private final int INCREMENT; // 常量变量（未初始化）

    // 构造函数初始化 final 实例变量 INCREMENT

    public Increment(int incrementValue) {

        INCREMENT = incrementValue; // 初始化常量变量（一次）

    } // Increment 构造函数结束

    // 将 INCREMENT 加到 total 中

    public void addIncrementToTotal() {

        total += INCREMENT;

    } // addIncrementToTotal 方法结束

    // 返回 Increment 对象数据的字符串表示

    public String toString() {

        return String.format("total = %d", total);

    } // toIncrementString 方法结束

} // Increment 类结束
```

图 8.15 | 类中的 final 实例变量。

```java
 // 图. 8.16: IncrementTest.java
```
