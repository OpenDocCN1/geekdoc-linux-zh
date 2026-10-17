
```
Exception in "main" java.lang.NoSuchMethodError: main
```

这在第 2 章中不是问题，因为你声明的每个类都有 `main` 方法。为了解决 `GradeBook` 的这个问题，我们必须声明一个包含 `main` 方法的独立类，或者在 `GradeBook` 类中放置一个 `main` 方法。为了帮助你准备书中和工业界会遇到的更大型程序，我们使用一个包含 `main` 方法的独立类（在本例中为 `GradeBookTest`）来测试我们创建的每个新类。

## Class GradeBookTest

`GradeBookTest` 类声明（图 3.2）包含了 `main` 方法，它将控制我们应用程序的执行。任何包含 `main` 且按第 7 行所示声明的类都可以用于执行应用程序。`GradeBookTest` 类声明从第 4 行开始，到第 16 行结束。该类只包含一个 `main` 方法，这是许多启动应用程序执行的类的典型特征。

第 7–14 行声明了 `main` 方法。回想第 2 章的内容，`main` 方法头必须如第 7 行所示出现；否则应用程序将不会执行。JVM 用于定位和调用方法以开始应用程序执行的关键部分是 `static` 关键字（第 7 行），它表示 `main` 是一个静态方法。静态方法是特殊的，因为在不先创建其被声明的类的对象的情况下，它是无法被调用的。我们将在第 6 章“方法：深层探析”中详细解释静态方法。

```java
// Fig. 3.2: GradeBookTest.java
// 创建一个 GradeBook 对象并调用其 displayMessage 方法
public class GradeBookTest {
    // main 方法开始程序执行
    public static void main(String args[]) {
        // 创建 GradeBook 对象并将其赋值给 myGradeBook
        GradeBook myGradeBook = new GradeBook();
        // 调用 myGradeBook 的 displayMessage 方法
        myGradeBook.displayMessage();
    }
} // end class GradeBookTest
```

> 欢迎来到 Grade Book！

> 创建 GradeBook 类的对象并调用其 displayMessage 方法。

在这个应用程序中，我们想调用 `GradeBook` 的 `displayMessage` 方法在命令行中显示欢迎消息。通常，正如第 10 行所示，在你创建该对象之前，你无法调用属于 `myGradeBook` 的方法。我们首先声明变量 `myGradeBook`。注意该变量的类型是 `GradeBook`——图 3.1 中声明的类。你创建的每个新类都变成一种新类型，可以用于变量并创建对象。程序员根据需要创建新类；这就是 Java 被称为可扩展语言的理由之一。

变量 `myGradeBook` 使用类实例创建表达式 `new GradeBook()` 的结果进行初始化。关键字 `new` 创建关键字右侧指定的类的类对象（即 `GradeBook`）。`GradeBook` 右侧的括号是必不可少的。正如你将在第 3.7 节中学到的，这些括号与类名结合用于调用构造方法（constructor），它类似于方法，但仅在创建对象时用于初始化对象的数据。在第 3.7 节中，你将看到数据是如何被处理的。

方法名 `displayMessage` 紧跟在小写首字母之后，名称中所有后续单词的首字母均大写。方法名后的括号表示这是一个空括号，如第 7 行所示，表示该方法不需要额外信息来执行其任务。第 7 行通常称为方法头。每个方法的体由左右括号（`{` 和 `}`）分隔，正如第 8 行和第 10 行所示。

方法的体包含执行方法任务的语句。在这种情况下，该方法包含一条语句（第 9 行），用于在命令行窗口中显示消息“Welcome to Grade Book!”，随后跟一个换行符。执行完毕后，该方法就完成了它的任务。

接下来，我们想在应用程序中使用 `GradeBook`。正如你在第 2 章中学习到的，`main` 方法开始每个应用程序的执行。包含 `main` 的类就是一个 Java 应用程序。这种类是特殊的，因为 JVM 可以使用 `main` 作为入口点来开始执行。`GradeBook` 不是一个应用程序，因为它不包含 `main`。因此，如果你尝试在命令行窗口中输入 `java GradeBook` 来执行它，你将收到一条类似下面的错误消息：

```
Exception in "main" java.lang.NoSuchMethodError: main
```

这在第 2 章中不是问题，因为你声明的每个类都有 `main` 方法。为了解决 `GradeBook` 的这个问题，我们必须声明一个包含 `main` 方法的独立类，或者在 `GradeBook` 类中放置一个 `main` 方法。为了帮助你准备书中和工业界会遇到的更大型程序，我们使用一个包含 `main` 方法的独立类（在本例中为 `GradeBookTest`）来测试我们创建的每个新类。

## Class GradeBookTest

`GradeBookTest` 类声明（图 3.2）包含了 `main` 方法，它将控制我们应用程序的执行。任何包含 `main` 且按第 7 行所示声明的类都可以用于执行应用程序。`GradeBookTest` 类声明从第 4 行开始，到第 16 行结束。该类只包含一个 `main` 方法，这是许多启动应用程序执行的类的典型特征。

第 7–14 行声明了 `main` 方法。回想第 2 章的内容，`main` 方法头必须如第 7 行所示出现；否则应用程序将不会执行。JVM 用于定位和调用方法以开始应用程序执行的关键部分是 `static` 关键字（第 7 行），它表示 `main` 是一个静态方法。静态方法是特殊的，因为在不先创建其被声明的类的对象的情况下，它是无法被调用的。我们将在第 6 章“方法：深层探析”中详细解释静态方法。

```java
// Fig. 3.2: GradeBookTest.java
// 创建一个 GradeBook 对象并调用其 displayMessage 方法
public class GradeBookTest {
    // main 方法开始程序执行
    public static void main(String args[]) {
        // 创建 GradeBook 对象并将其赋值给 myGradeBook
        GradeBook myGradeBook = new GradeBook();
        // 调用 myGradeBook 的 displayMessage 方法
        myGradeBook.displayMessage();
    }
} // end class GradeBookTest
```

> 欢迎来到 Grade Book！

> 创建 GradeBook 类的对象并调用其 displayMessage 方法。

在这个应用程序中，我们想调用 `GradeBook` 的 `displayMessage` 方法在命令行中显示欢迎消息。通常，正如第 10 行所示，在你创建该对象之前，你无法调用属于 `myGradeBook` 的方法。我们首先声明变量 `myGradeBook`。注意该变量的类型是 `GradeBook`——图 3.1 中声明的类。你创建的每个新类都变成一种新类型，可以用于变量并创建对象。程序员根据需要创建新类；这就是 Java 被称为可扩展语言的理由之一。

变量 `myGradeBook` 使用类实例创建表达式 `new GradeBook()` 的结果进行初始化。关键字 `new` 创建关键字右侧指定的类的类对象（即 `GradeBook`）。`GradeBook` 右侧的括号是必不可少的。正如你将在第 3.7 节中学到的，这些括号与类名结合用于调用构造方法，它类似于方法，但仅在创建对象时用于初始化对象的数据。在第 3.7 节中，你将看到数据是如何被处理的。

## 编译包含多个类的应用程序

在执行应用程序之前，你必须编译图 3.1 和 3.2 中的类。首先，切换到包含应用程序源文件的目录。接下来，输入命令

```
javac GradeBook.java GradeBookTest.java
```

同时编译这两个类。如果包含应用程序的目录只包含此应用程序的文件，你可以使用命令编译目录中的所有类：

```
javac *.java
```

`*.java` 中的星号 (`*`) 表示编译目录下所有以 `.java` 结尾的文件。

## GradeBook 类的 UML 类图
