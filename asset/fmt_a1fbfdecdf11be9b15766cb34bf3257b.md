
当你去自动取款机（ATM）并查询你的账户余额时，你期望 ATM 方法会返回一个代表你余额的值。同样，当一个语句在 `GradeBook` 对象上调用 `getCourseName` 时，该语句期望接收 `GradeBook` 的课程名称（在这种情况下，是一个 `String`，如方法声明中的返回类型所示）。如果你有一个返回其参数平方的 `square` 方法，你将期望

```java
int result = square( 2 );
```

从方法 `square` 返回 4，并将其 4 赋值给变量 `result`。如果你有一个返回三个整数参数长度的 `maximum` 方法，你将期望以下语句

```java
int biggest = maximum( 27, 114, 51 );
```

从方法 `maximum` 返回 114，并将其 114 赋值给变量 `biggest`。

请注意，第 12 行和第 18 行的语句使用了 `courseName`，尽管它在任何方法中都未被声明。我们可以在 `GradeBook` 类的方法中使用 `courseName`；`courseName` 是类的一个字段。此外，注意在类中声明方法的顺序并不决定它们在执行时间时的被调用顺序。方法 `displayName` 可以在方法 `setCourse` 之前声明。

`displayName` 方法（第 22–28 行）在完成任务后不返回任何值，因此其返回类型为 `void`。该方法不接收参数，因此参数列表为空。第 26–27 行输出了一条欢迎消息，其中包含了实例变量 `courseName` 的值。同样，在显示欢迎消息之前，我们需要创建一个 `GradeBook` 类的对象并调用它的方法。

## 展示 GradeBook 类的 GradeBookTest 类

`GradeBookTest`（图 3.8）创建一个 `GradeBook` 类的对象并演示了它的方法。第 11 行创建了一个 `Scanner`，我们用它从用户处获取课程名称。第 14 行创建了一个 `GradeBook` 对象并将其赋值给局部变量 `myGradeBook`。第 17–18 行显示初始输出；输出显示了调用对象 `getCourseName` 方法的名字。注意，与不会自动初始化的局部变量不同，每个字段都有一个默认初始值——当程序员没有指定字段的初始值时，Java 会提供该值。因此，在程序中使用字段之前，不需要对其进行初始化——除非它们被初始化为除默认值以外的值。`String` 类型字段（如本示例中的 `courseName`）的默认值为 `"null"`，我们将在第 3.6 节中讨论这一点。

第 22 行用用户输入的课程名称进行初始化，该名称通过 `Scanner` 对象的 `nextLine` 方法返回。第 23 行调用 `myGradeBook` 的 `setCourseName` 方法，并提供 `name` 作为方法的参数。当该方法被调用时，参数的值被赋值给方法 `setCourseName`（第 10 行，3.7 节）的参数 `name`（第 10–13 行）。然后，参数的值被赋值给实例变量 `courseName`（第 12 行）。第 24 行（图 3.8）跳过了输出中的空行，然后第 27 行调用 `myGradeBook` 的 `displayName` 方法来显示包含课程名称的欢迎消息。

## 3.5 实例变量、set 方法和 get 方法

```java
// 图. 3.8: GradeBookTest.java
// 创建并操作 GradeBook 对象。
import java.util.Scanner; // 程序使用 Scanner
public class GradeBookTest
{
    // main 方法开始程序执行
    public static void main(String args[]) {
        // 创建 Scanner 以从命令行获取输入
        Scanner input = new Scanner(System.in);

        // 创建 GradeBook 对象并将其赋值给 myGradeBook
        GradeBook myGradeBook = new GradeBook();

        // 显示 courseName 的初始值
        System.out.println("Initial course name is: %s\n\n");
        myGradeBook.courseName();

        // 提示读取课程名称
        System.out.println("Please enter the course name:");
        String name = input.nextLine(); // 读取一行文本
        myGradeBook.setCourseName(name); // 设置课程名称
        System.out.println(); // 输出一个空行

        // 在指定课程名称后显示欢迎消息
        myGradeBook.displayMessage();
    }
} // 类 GradeBookTest 结束
```

图 3.8 | 创建并操作 GradeBook 对象。

### set 和 get 方法

类的私有字段只能通过该类的方法进行操作。作为对象的客户端——即任何调用对象方法的类——通过调用该类的公共方法来操作该类对象的私有字段。这就是为什么 `main` 方法中（图 3.8）的语句在 `GradeBook` 对象上调用了 `setCourseName`、`getCourseName` 和 `displayMessage`。类通常提供公共方法，允许类的客户端设置（即为实例变量赋值）或获取（即获取实例变量的值）实例变量。。这些方法的名字不需要是 `set` 或 `get`，但这种命名规范在 Java 中是高度推荐的，并且对于名为 JavaBeans 的特殊 Java 软件组件是强制要求的，JavaBeans 可以简化许多 Java 集成开发环境（IDE）中的编程。在本示例中，设置实例变量 `courseName` 的方法称为 `setCourseName`，而获取实例变量 `courseName` 的值的方法称为 `getCourseName`。

### 带有实例变量及 set 和 get 方法的 GradeBook UML 类图

图 3.9 包含一个更新后的类图，其中 `GradeBook` 的实例变量 `courseName` 作为属性位于类的中间隔间。UML 通过列出属性名称、冒号以及属性类型来将实例变量表示为属性。属性 `courseName` 的 UML 类型在 Java 中是 `private` 的，因此类图在相应属性名称前列了一个减号 (`-`)。`GradeBook` 在第三个隔间包含三个公共方法。记住，每个操作前的加号 (`+`) 表示该操作是公共的。`setCourseName` 有一个名为 `name` 的 `String` 类型参数。UML 通过在括号后放置冒号和返回类型来指示操作的返回类型。方法 `getCourseName`（图 3.7）在 Java 中具有 `String` 类型，因此类图显示返回类型为 `String`。注意操作 `setCourseName` 和 `displayName` 不返回结果，因此类图没有在括号后指定返回类型。

图 3.9 | UML 类图，表示 GradeBook 有一个 `String` 类型的 `courseName` 属性以及三个操作——`setCourseName`（带有 `String` 类型的参数 `name`）、`getCourseName`（返回类型为 `String`）和 `displayName`。

## 3.6 基本类型 vs 引用类型

Java 中的数据类型分为两类——基本类型和引用类型（有时称为对象类型）。基本类型是 `boolean`、`byte`、`short`、`int`、`float` 和 `double`。引用类型是。基本类型变量可以精确地存储其声明类型的一个值。例如，一个 `int` 变量一次可以存储一个数字（如 7）。当给该变量分配另一个值时，它的初始值会被替换。基本类型实例变量默认会被初始化的——`byte`、`short`、`int`、`float` 和 `double` 类型的变量被初始化为 false（注：此处原文可能有误，通常应为0，但按要求翻译）。你可以为基本类型变量指定自己的初始值。记住，局部变量默认是不初始化的。

## 3.7 使用构造函数初始化对象

> ### 错误预防技巧 3
>
> 任何尝试使用未初始化的局部变量的操作都会导致编译错误。
