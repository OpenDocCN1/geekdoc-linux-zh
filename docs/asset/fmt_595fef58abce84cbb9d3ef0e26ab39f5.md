
是否循环应该开始（或继续）执行。决策符号和合并符号可以通过“入”转换和“出”转换的数量来区分。一个决策符号有一个指向菱形的转换箭头，有两个或多个指向外部的转换。

# 140 第 4 章 控制语句：第一部分

```java
I // 图 4.6: GradeBook.java
II // GradeBook 类，使用计数器控制循环解决
III // 类平均分问题。
IV import java.util.Scanner; // 程序使用类 Scanner 类
V public class GradeBook
VI {
VII private String course; // 此 GradeBook 表示的课程名称

IX // 构造函数初始化 courseName
public GradeBook(String name)
XII {
course = name; // 初始化 courseName
XIII } // 结束构造函数
XIV // 设置课程名称的方法
public void setCourseName(String name)
XVII {
course = name; // 存储课程名称
XIX } // 结束方法 setCourseName
XX // 获取课程名称的方法
public String getCourseName()
XXII {
return course;
XXIV } // 结束方法 getCourseName
XXVI // 向 GradeBook 用户显示欢迎信息
public void displayMessage()
XXVII {
XXIX // getCourseName 获取课程
System.out.printf("Welcome to the grade book\n%s!\n\n", getCourseName());
XXX } // 结束方法 displayMessage
XXXI // 根据用户输入的 10 个成绩确定类平均分
public void determineClassAverage()
XXXIII {
// 创建 Scanner 从命令行窗口获取输入
Scanner input = new Scanner(System.in);
int total; // 用户输入的成绩总和
int gradeCounter; // 下一个要输入的成绩计数
int grade; // 用户输入的成绩值
int average; // 成绩平均值
// 初始化阶段
total = 0; // 初始化总和
gradeCounter = 1; // 初始化循环计数器
// 处理阶段
while (gradeCounter <= 10) // 循环 10 次
{
```

```
图 4.6 计数器控制循环：类平均分问题。（2 部分中的第部分）。
```

## 4.8 制定算法：计数器控制循环

```java
    System.out.print("Enter grade: "); // 提示

    grade = input.nextInt(); // 输入下一个成绩

    total = total + grade; // 将成绩加到总和

    gradeCounter = gradeCounter + 1; // 计数器加 1

} // 结束 while

    // 终止阶段

    average = total / 10; // 整数除产生结果

    // 显示成绩的总和平均值

    System.out.printf("\ntotal of all 10 grades is %d\n", total);

    System.out.printf("Class average is %d\n", average);

} // 结束方法 determineClassAverage

} // 结束类 GradeBook
```

**图 4.6** 计数器控制循环：类问题。（2 部分中的第 2 部分。）

局部变量声明必须在方法中使用该变量之前出现。局部变量无法在声明它的方法之外访问。

在本章的 `GradeBook` 类版本中，我们简单地读取并处理一组成绩。平均值计算是在 `determineClassAverage` 方法中使用局部变量完成的——我们没有在类的实例变量中保留任何关于学生成绩的信息。在类的后续版本中（在第 7 章“数组”中），我们使用一个指向名为“数组”的数据结构的实例变量在内存中维护成绩。这使得 `GradeBook` 对象能够对成绩集执行各种计算，而不需要要求用户多次输入成绩。

## 良好的编程实践 4.5

在方法中使用空行将声明与其他语句分开，以提高可读性。

第 48–49 行的赋值将 `total` 初始化为 0，将 `gradeCounter` 初始化为 1。注意，这些初始化发生在变量用于计算之前。变量 `grade` 和 `average`（分别用于用户输入和计算的平均值）不需要初始化——它们的值在输入或在方法稍后被计算出来时才被赋值。

## 常见编程错误 4.4

在初始化局部变量之前读取其值会导致编译错误。局部变量在表达式中读取其值之前必须进行初始化。

## 错误预防提示 4.1

在声明中或在赋值语句中初始化每个计数器和总和。总和通常初始化为 0。计数器通常初始化为 0 或 1，取决于它们的用法（我们将展示何时使用 0 以及何时使用 1 的示例）。

第 52 行表示，`while` 语句只要 `gradeCounter` 的值小于或等于 10，就应该继续循环（迭代）。只要该条件仍然，该语句就会反复执行限定其体的大括号下的语句（第 54–57 行）。

第 54 行显示提示“Enter grade:”并将其赋值给变量 `grade`。然后第 56 行将用户输入的新成绩加到 `total`，并将结果赋值给 `total`，从而替换其之前的值。第 57 行将 `gradeCounter` 加 1，表示程序已处理了一个成绩并准备好接受下一个成绩。`gradeCounter` 的增加最终会导致 `gradeCounter` 超过 10，此时 `while` 循环终止，因为其条件（第 52 行）变为假。当循环终止时，第 61 行执行平均值计算并将结果赋值给变量 `average`。第 64 行使用 `System.out.printf` 显示“Total of all 10 grades is ”后跟 `total` 的值。第 65 行使用 `printf` 显示“Class average is ”后跟 `average` 的值。第 66 行之后，`determineClassAverage` 方法返回到调用方法（即图 4.7 中的 `GradeBookTest` 中）。

## GradeBookTest

`GradeBookTest`（图 4.7）创建 `GradeBook` 对象（图 4.6）并调用其 `determineAverage` 方法。第 11 行将字符串“CS101 Introduction to Java”传递给构造函数（图 4.6）。第 13 行调用 `myGrade.displayMessage()` 显示欢迎信息。第 14 行调用 `myGrade.determineClassAverage()` 允许用户输入 10 个成绩，图 4.6 中的方法计算并打印平均分。图 4.7 显示了 `GradeBookTest`。

```java
// 图 4.7: GradeBookTest.java

// 创建 GradeBook 对象并调用 determineAverage 方法。

public class GradeBookTest {

    public static void main(String args[]) {

        // 创建 GradeBook 对象并

        // 传递课程

        GradeBook myGrade = new GradeBook(

            "CS101 Introduction to Java"

        );

        myGrade.displayMessage(); // 显示欢迎信息

        myGrade.determineClassAverage(); // 计算 10 个成绩的平均值

    }

} // 结束类 GradeBookTest
```

图 4.7 测试创建了 `GradeBook` 类对象（图 4.6）并调用其 `determineAverage` 方法。（2 部分中的第一部分）。

## 4.9 制定算法：哨兵控制循环

```
Welcome to the grade book

CS101 Introduction to Java!

Enter grade: 67

Enter grade: 78

Enter grade: 89

Enter grade: 67

Enter grade: 87

Enter grade: 93

Enter grade: 85

Enter grade: 82

Enter grade: 100

Total of all 10 grades is 846
```
