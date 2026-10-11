
### 图 8.11 测试枚举类型。（2 部分中的第 1 部分。）

所有书籍：

| 常量 | 标题 | 年 |
| :--- | :--- | :--- |
| JAVA | Java to Program 6e | 2005 |
| C4 | C to Program 4e | 2004 |
| INTERNET | Internet & Wide Web to Program 3e | 2004 |
| CPP | C++ to Program 4e | 2003 |
| BASIC | Basic .NET to Program 2e | 2002 |
| CSHARP | C# to Program | 2002 |

枚举常量范围：

| 常量 | 标题 | 年 |
| :--- | :--- | :--- |
| JAVA | Java to Program 6e | 2005 |
| C4 | C to Program 4e | 2004 |
| INTERNET | Internet & Wide Web to Program 3e | 2004 |
| CPP | C++ to Program 4e | 2003 |

创建的每个对象都会使用各种系统资源，例如内存。为了避免“资源泄漏”，我们需要一种机制，在资源不再需要时将其归还给系统。Java 虚拟机（JVM）执行自动垃圾回收，以回收不再使用的对象所占用的内存。当一个对象不再有任何引用时，该对象会被 JVM 标记为待垃圾回收。当 JVM 执行其垃圾回收器时，该对象的内存会被回收，垃圾回收器负责检索不再被其使用的对象内存。此外，内存泄漏在 C 和 C++ 等其他语言中更为常见（因为在其他语言中内存不会被自动回收），而在 Java 中这种情况较少（但某些仍可能以微妙的方式发生）。也会发生其他类型的资源泄漏。例如，如果应用程序可以打开磁盘上的一个文件来修改其内容。如果应用程序没有关闭该文件，那么在应用程序完成文件操作之前，其他应用程序都无法使用它。

垃圾回收器在回收对象内存之前调用 `finalize` 方法来对对象执行终止清理工作。`finalize` 方法不接受参数且类型为 `void`。`finalize` 的一个问题是垃圾回收器不保证在特定时间执行。事实上，垃圾回收器在程序终止之前可能永远不会执行。因此，不清楚 `finalize` 是否会被调用以及何时被调用。由于这个原因，大多数程序员应该避免使用 `finalize`。在第 8.11 节中，我们将演示垃圾回收器调用 `finalize` 方法的情况。

## 软件工程观察 8.10

使用系统资源（如磁盘上的文件）的类应该提供一个方法最终释放资源。许多 Java API 类为此目的提供了关闭或销毁方法。例如，`Scanner` 类有 `close` 方法。

## 8.11 静态类成员

每个对象都有类中所有实例变量的副本。在某些情况下，某个变量的唯一副本应该由类的所有对象共享。在这种情况下，使用一个静态字段——称为类变量。静态变量表示类信息——该类的所有对象共享同一份数据。静态变量的声明以 `static` 关键字开始。

让我们通过示例来说明静态数据的必要性。假设我们有一个包含火星和其他太空生物的视频游戏。当火星人意识到至少有四名其他火星人在场时，每个火星人都需要表现勇敢并愿意攻击其他生物。如果在场少于五名火星人，每个人都会变得胆小。因此，每个火星人都需要知道 `martianCount`。我们可以将 `martianCount` 作为实例变量赋予火星人。如果我们这样做，每个火星人都将拥有该实例变量的独立副本，如果我们创建一个新的火星人，我们必须更新每个火星人的实例变量 `martianCount`。这浪费了存储冗余副本的空间，浪费了更新独立副本的时间，并且容易出错。相反，我们将 `martianCount` 声明为静态的，使 `martianCount` 成为类数据。每个火星人都会将 `martianCount` 视为 `Martian` 类的一个实例变量，但只维护了一份 `martianCount` 副本。这节省了空间。我们通过让火星人构造函数增加静态 `martianCount` 来节省时间——因为只有一个副本，所以我们不需要为每个火星人对象增加 `martianCount` 的独立副本。

## 软件工程观察 8.11

当类的所有对象都必须使用变量的同一副本时，使用变量。

静态变量具有作用域。类的公共静态成员可以通过该类的任何对象的引用来访问，或者通过用类名和点（`.`）限定成员名来访问，例如 `Math.random()`。类的私有静态成员只能通过类的方法访问。实际上，即使在没有类对象的情况下，静态类成员也存在——只要类在执行时加载到内存中，它们就是可用的。在没有类对象的情况下访问公共静态成员（即使在对象存在时也是如此），在静态成员名前加上类名和点（`.`），例如 `Math.PI`。在没有类对象的情况下访问私有静态成员，则必须提供一个公共静态方法，并且必须通过类名和点以及其方法名来调用该方法。

## 软件工程观察 8.12

即使该类没有实例化任何对象，静态变量和方法也存在并可以使用。

我们的下一个程序声明了两个类——`Employee` 和 `EmployeeTest`。`Employee` 类声明了私有静态变量 `count` 和公共静态方法 `getCount`。静态变量 `count` 在第 9 行初始化为零。如果静态变量未初始化，编译器将为该类型的变量分配一个默认值。变量 `count` 包含了当前留在内存中的 `Employee` 类对象的数量。这包括了已经被垃圾回收器回收的对象。

```java
// Fig. 8.12: Employee.java

// 使用静态变量来维护内存中

// Employee 对象的计数

public class Employee {

    private String firstName;

    private String lastName;

    private int count = 0; // 内存中的对象数量

    // 初始化，将静态 count 加 1 并

    // 输出构造函数被调用的字符串

    public Employee(String firstName, String lastName) {

        this.firstName = firstName;

        this.lastName = lastName;

        count++; // 增加员工的静态计数

        System.out.printf("Employee constructor: %s %s; count = %d\n",

            firstName, lastName, count);

    } // 构造函数结束

    // 当垃圾回收器

    // 调用 finalize 清理对象时减少静态 count

    // 确认 finalize 被调用

    protected void finalize() {

        count--; // 减少员工的静态计数

        System.out.printf("Employee finalizer: %s %s; count = %d\n",

            firstName, lastName, count);

    } // finalize 方法结束

    // 获取名

    public String getFirstName() {

        return firstName;

    } // getFirstName 方法结束

    // 获取姓

    public String getLastName() {

        return lastName;

    } // getLastName 方法结束

    // 获取静态计数值的静态方法

    public static int getCount() {

        return count;

    } // getCount 方法结束

} // 类结束
```
