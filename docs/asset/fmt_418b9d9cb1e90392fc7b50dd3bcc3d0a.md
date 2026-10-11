
枚举可以在任何可以使用常量的地方，例如 `switch` 语句的 `case` 标签以及增强 `for` 循环。图 8.10 展示了如何在枚举类型中声明实例变量、构造函数和方法。枚举声明（第 5–37 行）包含两个部分——枚举常量和枚举的其他成员。第一部分（第 8–13 行）声明了枚举常量。每个枚举后面跟着传递给枚举构造函数的参数（第 20–24 行）。正如在在类中所看到的，枚举构造函数可以指定任意数量的参数并可以重载。在本例中，枚举构造函数接受两个 `String` 参数。第二部分（第 16–36 行）声明了枚举类型的其他成员——实例变量（第 16–17）、构造函数（第 20–24）和方法（第 27–33）。

```java
// Fig. 8.10: Book.java
// 带有构造函数和实例字段的枚举类型
// 字段的访问器
public enum Book {
    // 枚举类型的常量
    JAVA("Java to Program 6e", "2005"),
    C4("C to Program 4e", "2004"),
    INTERNET("Internet & Wide Web to Program 3e", "2004"),
    CPP("C++ to Program 4e", "2003"),
    BASIC("Basic .NET to Program 2e", "2002"),
    CSARP("C# to Program", "2002");

    // 实例字段
    private final String title;
    private final String copyrightYear;

    // 枚举构造函数
    Book(String bookTitle, String year) {
        title = bookTitle;
        copyrightYear = year;
    } // end enum constructor
```

**图 8.10** 带有实例字段、构造函数和方法。（2 部分中的第 1 部分）

```java
// 字段 title 的访问器
public String getTitle() {
    return title;
} // end method getTitle

// 字段 copyrightYear 的访问器
public String getCopyrightYear() {
    return copyrightYear;
} // end method getCopyrightYear
```

8.11 测试了图 8.10 中声明的枚举类型，并展示了如何遍历常量范围。对于每个枚举，编译器都会生成一个静态方法 `values`（在第 12 行调用），返回按声明顺序排列的常量数组。回想第 7.6 节中的增强 `for` 语句

```java
// Fig. 8.11: EmployeeTest.java
// 测试枚举类型。

import java.util.EnumSet;

public class EmployeeTest {

    public static void main(String[] args) {

        System.out.println("All books:");

        // 打印枚举中的所有书籍

        for (Book book : Book.values()) {

            System.out.printf("%-10s%45s\n", book, book.getTitle(), book.getCopyrightYear());

        }

        System.out.println("\nDisplay range of enum constants:");

        // 打印范围书籍

        for (Book book : EnumSet.range(Book.JAVA, Book.CSHARARP)) {

            System.out.printf("%-10s%45s\n", book, book.getTitle(), book.getCopyrightYear());

        }

    } // end EmployeeTest
```
