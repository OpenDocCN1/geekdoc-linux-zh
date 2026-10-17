
图 3.6 的 UML 类图显示了 `GradeBook` 类。与图 3.1 类似，这个 `GradeBook` 包含公共 `displayName`。然而，这个 `displayName` 有一个参数。UML 模型的方式与 Java 不同，它在操作名后的括号内列出参数名，随后是冒号和参数类型。UML 有自己的数据类型，与 Java 的类型相似（但正如你所见，并不是所有的 UML 数据类型与对应的 Java 类型名称相同）。

## 3.5 实例变量、set 方法和 get 方法

![](img/1df0d1e8ac6007b95647eb8ea38390af_138_0.png)

**图 3.6** | UML 类图，显示类 `GradeBook` 有一个 `displayMessage` 操作，其具有 UML 类型为 `String` 的参数 `courseName`。

`types`。UML 类型 `String` 对应于 Java 类型 `String`。`GradeBook` 方法 `displayMessage`（图 3.4）有一个名为 `courseName` 的 `String` 类型参数，图 3.6 在 `displayMessage` 后的括号中列出了 `courseName : String`。

### 关于 import 声明

注意图 3.5（第 4 行）中的 `import` 声明。这告诉编译器程序使用了 `Scanner` 类。为什么我们我们需要导入 `Scanner` 类，而不是导入 `System`、`String` 或 `GradeBook` 类呢？你在 Java 程序中使用的大多数类都会被导入。`System` 和 `String` 类位于 `java.lang` 包中，该包会被隐式导入到每个 Java 程序中，因此所有程序在无需显式导入的情况下使用 `java.lang` 的类。

在磁盘上位于同一目录下编译的类之间（例如 `GradeBook` 和 `GradeTest` 类）存在一种特殊关系。这些类被认为处于同一个包中——被称为默认包。由于类在同一个包中——因此当包中的一个类使用同包中的另一个类时，不需要 `import` 声明——例如 `GradeTest` 类使用 `GradeBook` 类时。

如果我们引用 `java.util.Scanner`，则不需要第 4 行的 `import` 声明，因为它包含了完整的包名和类名。这被称为类的**完全限定类名**（fully qualified class name）。例如，第 12 行可以写为：

```java
java.util.Scanner input = new java.util.Scanner(System.in);
```

## 软件工程观察 3.2

如果在 Java 源码中使用完全限定类名，Java 编译器就不要求文件中包含 `import` 声明。但大多数 Java 程序员认为使用完全限定名是繁琐的，他们更倾向于使用 `import` 声明。

## 3.5 实例变量、set 方法和 get 方法

在第 2 章中，我们在应用程序的 `main` 方法中声明了应用程序的所有变量。在特定方法体内声明的变量被称为**局部变量**，只能在该方法中使用。当该方法终止时，其局部变量的值就会丢失。回顾第 3.2 节，对象拥有属性，这些属性在程序中使用对象时随对象携带。此类属性在对象上调用方法之前和方法执行之后都存在。

一个类通常由一个或多个方法组成，这些方法操作属于类的某个特定对象的属性。属性在类声明中表示。这些变量被称为**字段**（fields），声明在类声明内部但在类方法声明外部。当类的每个对象都维护其属性的独立副本时，表示属性的字段也被称为**实例变量**（instance variable）——类的每个实例在内存中都有该变量的一个实例。本节的示例展示了一个 `GradeBook` 类，它包含一个 `course` 变量来表示特定 `GradeBook` 的课程名。

## 带有实例变量、set 方法和 get 方法的 GradeBook 类

在我们的下一个应用程序中（图 3.7–图 3.8），`GradeBook` 类（图 3.7）将课程名维护为一个实例变量，可以在应用程序执行期间的任何时间使用或修改。该类包含三个方法：`setCourseName`、`getCourseName` 和 `displayName`。`setCourseName` 方法在 `GradeBook` 中设置课程名。`getCourseName` 方法获取 `GradeBook` 的课程名。`displayName` 方法未指定参数，显示一条包含课程名的欢迎消息；正如你将看到的，该方法现在通过调用同类中的另一个方法——`getCourseName` 来获取课程名。

```java
// 图 3.7: GradeBook.java
// 包含 courseName 实例变量的 GradeBook 类
// 以及用于设置和获取其值的方法。

public class GradeBook
{
    private String courseName; // GradeBook 的课程名

    // 设置课程名的方法
    public void setCourseName(String name)
    {
        courseName = name; // 设置课程名
    }

    // 获取课程名的方法
    public String getCourseName()
    {
        return courseName;
    }

    // 显示向 GradeBook 的欢迎消息
    public void displayName()
    {
        System.out.printf("Welcome to the %s book!\n",
            getCourseName());
    }
}
```

图 3.7 | 包含 `courseName` 实例变量的 `GradeBook` 类，以及设置和获取其值的方法。

## 3.5 实例变量、set 方法和 get 方法

一个典型的类教授了比每个实例都有自己的课程名。第 7 行声明 `courseName` 是 `String` 类型。由于属性声明在类体中但在方法体之外（第 10–13 行、16–19 行和 22–28 行），第 7 行是一个实例变量。将 `courseName` 设置为实例变量的好处是所有方法都可以操作实例变量。

### 访问修饰符 public 和 private

大多数实例变量被声明为 `private`。像 `public` 一样，`private` 是一种访问修饰符。声明为 `private` 的变量仅对声明它们的方法可见。因此，`courseName` 只能由 `GradeBook` 的方法使用。

![](img/1df0d1e8ac6007b95647eb8ea38390af_140_0)

## 软件工程观察 3.3

在每个字段和方法声明前加上访问修饰符。作为经验法则，实例变量应该是 `private` 的，而方法应该是 `public` 的。（我们看到，如果某些方法会被内部访问，将其声明为 `private` 是合适的）。

![](img/1df0d1e8ac6007b95647eb8ea38390af_140_1)

## 良好实践 3.1

我们喜欢首先列类字段，这样在阅读代码时，在看到方法之前先看到变量的名称和类型。可以在类的任何位置列出类的字段，但散布它们会导致代码难以阅读。

![](img/1df0d1e8ac6007b95647eb8ea38390af_140_2)

## 良好实践 3.2

在方法声明之间留出空行，以分隔方法并增强程序的可读性。

使用 `private` 访问修饰符声明实例变量被称为**数据隐藏**。当程序创建（实例化）`GradeBook` 类的对象时，变量 `courseName` 被封装在对象内部，并且只能通过对象的方法访问。在 `GradeBook` 类中，`setCourseName` 和 `getCourseName` 方法操作实例变量 `courseName`。

`setCourseName` 方法（第 10–13 行）在完成任务时不返回任何值，因此它接收一个参数——`name`，代表作为参数传递给方法的课程名变量。第 12 行将 `name` 赋值给实例变量 `courseName`。

`getCourseName` 方法（第 16–19 行）返回特定 `GradeBook` 对象的 `courseName`。该方法没有参数列表，因此它不需要额外信息来执行任务。该方法指定它返回一个 `String`——这被称为方法的**返回值**。当指定了返回类型的方法被调用并完成任务时，该方法会向调用它的方法返回结果。例如，

# 第 3 章 类与对象简介
