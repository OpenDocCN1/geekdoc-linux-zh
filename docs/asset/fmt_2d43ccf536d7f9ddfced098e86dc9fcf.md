
图 3.3 展示了图 3.1 中 `GradeBook` 类的 UML 类。回想第 1.16 节，UML 是程序员用于标准化方式表示面向对象系统的图形语言。在 UML 中，每个类在类图中被建模为带有三个部分的矩形。顶部部分包含居中对齐的粗体类名。中间部分包含属性，对应 Java 中的实例变量。在图 3.3 中，中间部分是空的，因为图 3.1 中的 `GradeBook` 类没有任何属性。底部部分包含类的操作，对应 Java 中的方法。UML 通过列出带有访问修饰符前缀的操作名称以及一组参数来建模操作。`GradeBook` 类有一个方法 `displayMessage`，图 3.3 的底部部分列出了此名操作。`displayMessage` 方法不需要额外信息来执行

| 图号 | 描述 |

| :--- | :--- |

| 3.3 | UML 类图，表示 `GradeBook` 类有一个公开的 `displayMessage` 操作。 |

根据其任务，类图中方法名后面的括号是空的，这就像在图 3.1 第 7 行的方法声明中那样一样。操作名称前的加号 `+` 表示 `displayName` 是 UML 中的一个公共操作，即 Java 中的一个公共方法。我们经常使用 UML 类来总结一个类的属性和操作。

## 3.4 声明带有参数的方法

在第 3.2 节的汽车类比中，我们讨论了按下汽车油门板会向汽车发送一条消息，以执行某项任务——让汽车行驶得更快。汽车应该加速到多快？如你所知，油门踩得越快，汽车加速得越快。因为发送给汽车的消息实际上包含了要执行的任务以及有助于执行任务的额外信息。这些额外信息被称为**参数**——参数的值帮助汽车确定以多快的速度加速。同样，方法可能需要一个或多个参数来表示其执行任务所需的额外信息。方法为每个方法的每个参数调用值——即**参数**。例如，`System.out.println` 需要一个参数来指定在命令行窗口中输出的数据。同样，要向银行账户存款，存款方法指定了一个代表存款金额的参数。当调用存款方法时，一个代表存款金额的参数会被赋值给方法的参数。然后方法执行该金额的存款。

下一个示例声明了 `GradeBook`，它包含一个 `displayName` 方法，该方法将课程名称作为欢迎消息的一部分。新的 `displayName` 方法需要一个代表输出的课程名称的参数。

在讨论 `GradeBook` 类的新功能之前，让我们看看如何在 `GradeBookTest` 类的 `main` 方法中运行这个新类。第 12 行创建了一个名为 `input` 的 `Scanner` 用于从用户处读取课程名称。第 15 行创建了 `GradeBook` 类的对象并将其赋值给变量 `myGradeBook`。第 18 行提示用户输入课程名称。第 19 行使用 `Scanner` 方法 `next()` 执行输入，从用户处读取名称并赋值给变量 `nameOfCourse`。用户输入课程名称并按回车键将课程名称提交给提示。注意，按回车键会在用户输入的字符末尾插入一个换行符。

```java
// 带有参数的方法方法的类声明
public class GradeBook {
  // 向 GradeBook 用户显示欢迎消息
  public void displayName(String courseName) {
    System.out.printf("Welcome to the grade book for\n%s!\n", courseName);
  } // 方法 displayName 
} // 类 GradeBook 
```

**图 3.4** 带有一个参数方法的类声明。

```java
// Fig 3.5: GradeBookTest.java
// 创建 GradeBook 对象并向其
// displayMessage 方法传递一个 String 类型。
import java.util.Scanner; // 程序使用 Scanner
public class GradeBookTest {
    // main 方法开始程序执行
    public static void main(String args[]) {
        // 创建 Scanner 从命令行窗口获取输入
        Scanner input = new Scanner(System.in);

        // 创建 GradeBook 对象并将其赋值给 my GradeBook
        GradeBook myGradeBook = new GradeBook();

        // 提示输入课程名称
        System.out.println("enter the course name:");
        String nameOfCourse = input.nextLine(); // 读取一行文本
        System.out.println(); // 输出一个空行

        // 调用 myGradeBook 的 displayMessage 方法
        // 并将 nameOfCourse 作为参数传递
        myGradeBook.displayName(nameOfCourse);
    }
} // 类 GradeBookTest
```

请输入课程名称：

CS101 Introduction to Java Programming

Welcome to the grade book for

CS101 Introduction to Java Programming

**图 3.5** 创建一个 GradeBook 对象并向其 displayMessage 方法传递一个 String。

方法 `nextLine` 读取用户输入的字符，直到遇到换行符，然后返回一个包含换行符之前所有字符的 String。换行符被丢弃。`Scanner` 类提供了一个类似的方法——读取单个单词。当用户在输入内容后按回车键时，方法读取字符，直到遇到空白字符，如空格、制表符或换行符，然后返回一个包含空白字符之前所有字符的 String，空白字符会被丢弃。第一个空白字符之后的所有信息都不会丢失——它可以由程序中调用 Scanner 方法的其他语句读取。

第 24 行调用了 `myGradeBook` 的 `displayName` 方法。括号中的变量名 `nameOfCourse` 是传递给 `displayName` 方法的参数，以便该方法执行其任务。变量 `nameOfCourse` 的值变成了 3.4 第 7 行中 `courseName` 的值。当你执行此应用程序时，注意方法 `displayName` 会将你输入的名称作为欢迎消息的一部分输出。

### 软件工程观察 3.1

通常，对象是用 `new` 创建的。异常是包含在引号中的字符串字面量，例如 `"hello"`。字符串字面量是对 Java 隐式创建的 String 对象的引用。

### 关于参数和形参更多信息

当你声明一个方法时，必须指定该方法是否需要数据来执行其任务。为了这样做，你需要在方法名后的括号中放置额外信息。参数列表可以包含任意数量的参数，也可以完全没有。方法名后的空括号，如图 3.1 第 7 行所示，表示该方法不需要任何参数。在图 3.4 中，第 7 行的参数列表声明需要一个参数。每个参数必须指定一个类型，`displayName` 需要一个 String 类型。当方法被调用时，参数值会被赋值给方法头中的参数，在本例中为 `courseName`。方法体使用 `courseName` 来访问该值。图 3.4 的第 9-10 行使用 `printf` 的格式字符串 `%s` 显示 `courseName`。注意，参数变量名，图 3.4 第 7 行，可以与参数名，图 3.5 第 24 行，相同也可以不同。

方法可以通过逗号分隔每个参数来指定多个参数，我们将在第 6 章看到此示例。方法调用中的参数数量必须与方法声明中的参数数量匹配。此外，参数类型必须与方法声明中相应参数的类型一致，在随后的章节中你了解到，参数类型与其相应的参数类型不需要完全相同。在我们的示例中，方法传递了一个 String 类型的参数，在图 3.5 第 19 行 `nameOfCourse` 定义为 String，而方法声明了一个 String 类型的参数，图 3.4 第 7 行。因此在该示例中，方法的参数类型与方法头中的参数类型完全匹配。

#### 编程错误 3.2

如果方法调用中的参数数量与方法声明中的参数数量不匹配，则会导致编译错误。

#### 编程错误 3.3

如果方法调用中的参数类型与方法声明中相应参数的类型不一致，则会导致编译错误。

## GradeBook 类更新 UML 类图
