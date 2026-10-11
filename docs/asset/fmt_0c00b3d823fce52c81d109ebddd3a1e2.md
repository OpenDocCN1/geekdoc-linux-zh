
```java
modifyElement(array[ 3 ] ); // attempt to modify array[ 3 ]
System.out.printf(
"array[3] after modifyElement: %d\n", array[ 3 ]);
}// end main
```

```java
// multiply each element of array 2
public static void modifyArray( int array2[])
{
    for ( int counter = 0; counter < array2.length; counter++)
    array2[counter] *= 2;
} // end modifyArray
```

```java
// multiply each element of array 2
public static void modifyElement( int element)
{
    element *= 2;
    System.out.printf("Value of element in modifyElement: %d\n", element);
} // end modifyElement
```

Effects of passing array to entire array:

The values of the modified array are:

Effects of passing array element value:
array[3] before modifyElement: 8
array[3] after modifyElement: 8

图 7.13 将数组和单个数组元素传递给方法。（2 部分中的。）

**关于参数传递的注意事项**

许多语言中传递参数的两种方式是按值传递和按引用传递。按值传递参数时，被调用的方法仅与拷贝工作，被调用的方法不会影响调用者中的原始值。

当按引用传递参数时，被调用的方法可以直接访问参数并在需要时进行修改。与其他语言不同，Java 不允许程序员选择按值或按引用。方法可以传递两种类型的值——基本值的拷贝（例如 `int` 和 `double` 值）以及对象的拷贝（包括引用）。

当方法修改基本类型时，参数的变化不会影响调用者中的原始值。例如，当图 7.13 中 `main` 方法的第 30 行将 `array[3]` 传递给 `modifyElement` 时，第 45 行使 `element` 翻倍不会影响 `array[]`。

虽然对象的引用是按值传递的，但方法仍然可以使用该引用。由于存储在参数中的引用是作为参数传递的引用的拷贝，调用方法中的参数引用内存中的相同对象。例如，在图 7.13 中，`modifyArray` 中的 `array2` 和 `main` 中的 `array` 引用内存中的相同对象。使用 `array2` 进行的任何更改都在作为参数传递的变量所引用的对象上执行。在图 7.13 中，`modifyArray` 中使用 `array2` 进行的更改影响了 `main` 中 `array` 所引用数组的内容。

性能提示 7.1

出于性能考虑，按引用传递数组是合理的。如果按值传递数组，则会传递每个元素的拷贝。对于频繁传递的大数组，这将浪费时间并为数组拷贝消耗大量存储空间。

## 7.8 案例研究：使用数组存储成绩的 GradeBook 类

本节进一步演化了第 3 章引入并在第 4–5 章扩展的 GradeBook 类。回想一下，该类代表教授存储和分析一组学生成绩的成绩单。之前的类版本可以执行用户输入的一组成绩，但没有在类的实例变量中维护单独的成绩值。因此，在重复使用学期数据时需要重复计算。解决此问题的方法是将输入的每个成绩存储在类的某个单独实例中。例如，我们可以在 `GradeBook` 类中创建实例变量 `grade1`、`grade2` 到 `grade10` 来存储 10 个学生的成绩。然而，计算总和和确定平均分的代码将非常繁琐，而且类一次无法处理超过 10 个成绩。在本节中，我们通过在数组中存储成绩来解决这个问题。

### 在 GradeBook 类中使用数组存储学生

这里提供的 `GradeBook` 类版本（图 7.14）使用整数数组来存储多个学生在某次考试中的成绩。这消除了重复输入同一组成绩的需要。数组在第 7 行被声明为实例变量——因此，每个 `GradeBook` 对象都维护自己的成绩集。该类的构造函数（第 10–14 行）有两个参数——名称和成绩数组。当应用程序（例如图 7.15 中的 `GradeBookTest` 类）创建 `GradeBook` 对象时，应用程序将数组的引用赋值给实例变量 `grades`（第 13 行）。数组的大小由将数组传递给构造函数的类决定。因此，`GradeBook` 对象可以处理任意数量的成绩。传递数组中的成绩值可以从用户输入，也可以从磁盘上的文件读取（如第 14 章所述）。在我们的测试应用程序中，我们简单地用一组成绩值来初始化数组（图 7.15，第 10 行）。一旦成绩存储在 `GradeBook` 的实例变量 `grades` 中，该类的所有方法都可以根据需要访问 `grades` 的元素以执行各种计算。

```java
// Fig. 7.14: GradeBook.java
// 使用数组存储测试成绩的成绩单。
public class GradeBook {
    private String courseName; //此 GradeBook 的课程名称
    private int grades[]; // 学生成绩数组
    // 双参数构造函数初始化 courseName 和 grades
    public GradeBook(String name, int gradesArray[]) {
        courseName = name; // 初始化 courseName
        grades = gradesArray; // 存储成绩
    } // 双参数 GradeBook 构造函数
```
图 7.14 | 使用数组存储测试成绩的 GradeBook 类。（4 部分中的第 1 部分。）

```java
// 设置课程名称的方法
public void setCourseName( String name )
{
    courseName = name; // 存储课程名称
} // 方法 setCourseName 结束
// 获取课程名称的方法
public String getCourseName()
{
    return courseName;
} // 方法 getCourseName 结束
//向 GradeBook 用户欢迎消息
public void displayMessage()
{
    // getCourseName 获取课程名称
    System.out.printf("Welcome to the grade book\n%s!\n\n",
    getCourseName());
} // 方法 displayMessage 结束
// 对数据执行各种操作
public void processGrades()
{
    // 输出成绩数组
    outputGrades();
    // 调用方法 Average 计算平均分
    System.out.printf("InClass average is %.2f\n", getAverage());
    // 调用方法 getMinimum 和 getMaximum
    System.out.printf("Lowest grade is %d\nHighest grade is %d\n",
    getMinimum(), getMaximum());
    // 调用 outputChart 打印成绩分布图
    outputBarChart();
} // 方法 processGrades 结束
// 寻找最低成绩
public int getMinimum()
{
    int lowGrade = grades[0]; // 假设 grades[0] 是最小的
    // 遍历 grades 数组
    for (int grade : grades)
    {
        // 如果 grade 低于 lowGrade，将其赋值给 lowGrade
        if (grade < lowGrade)
            lowGrade = grade; // 新低分
    }
    return lowGrade; // 返回最低成绩
} // 方法 getMinimum 结束
```
图 7.14 使用数组存储测试成绩的 GradeBook 类。（4 部分中的第 2 部分。）

```java
// 寻找最高成绩
public int getMaximum()
{
```
