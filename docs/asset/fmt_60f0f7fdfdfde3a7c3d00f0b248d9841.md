
### 7.8 案例研究：使用数组存储成绩的 GradeBook 类

每个成绩类别中分数的出现频率。对于数组 `lines` 中的每个成绩，第 107–108 行增加了频率数组中相应元素的值。为了确定增加哪一个元素，第 108 行使用整数除法将当前成绩除以 10。例如，如果成绩为 85，第 108 行增加 `frequency[8]` 以更新 80–89 范围内分数的计数。第 111–125 行根据数组 `frequency` 中的值打印条形图（见图 7.15）。图 7.6 的第 23–24 行、图 7.14 的第 121–122 行使用数组 `frequency` 中的值来确定每个条形中显示的星号数量。

#### 展示 GradeBook 类的 ClassGradeTest

图 7.15 的应用使用 `int` arrayArrays[]`（在第 0 行声明并初始化）创建了 `GradeBook` 类（图 7.14）的对象。第 12–13 行将课程名称和 `gradesArray` 传递给 `GradeBook` 构造函数。第 14 行显示欢迎消息，并且：

```java
// Fig 7.15: GradeBookTest.java
// 使用成绩数组创建 GradeBook 对象。

public class GradeBookTest {
    public static void main(String[] args) {
        // 学生成绩数组
        int gradesArray[] = {87, 68, 94, 100, 83, 78, 85, 91, 76, 87};

        GradeBook myGradeBook = new GradeBook(
            "CS101 Introduction to Java Programming", gradesArray);

        myGradeBook.displayMessage();
        myGradeBook.processGrades();
    }
 // end class GradeBookTest
```

Figure 7.14 | 使用数组存储测试成绩的 GradeBook 类。（4 部分中的第 3 部分。）

```java
int highGrade = grades[0]; // 假设 grades[0] 是最大的

// 遍历 grades 数组
for (int grade : grades) {
    // 如果 grade 高于 highGrade，将其赋值给 highGrade
    if (grade > highGrade) {
        highGrade = grade; // 新高分
    }
}
return highGrade; // 返回最高成绩
}
```

```java
// 确定测试的平均成绩
public double getAverage()
{
    int total = 0; // 初始化总和
    // 累加一个学生的成绩
    for (int grade : grades) {
        total += grade;
    }
    // 返回成绩的平均值
    return (double) total / grades.length;
}
```

```java
// 输出显示成绩分布的状图
public void outputBarChart()
{
    System.out.println("Grade distribution:");
    // 存储每个 10 分范围内每个成绩的频率
    int frequency[] = new int[11];
    // 对于每个成绩，增加相应的频率
    for (int grade : grades) {
        frequency[grade / 10]++;
    }
    // 对于每个成绩，在图表中打印条形
    for (int count = 0; count < frequency.length; count++) {
        // 输出条形标签 ("00-09": ", ..., "90-99": "100:")
        System.out.printf("%02d-%02d: %d\n", count * 10, count + 9, frequency[count]);
    }
}
```

```java
// 打印星号柱状图
for (int stars = 0; stars < frequency[count]; stars++) {
    System.out.print("*");
}
System.out.println(); // 开始新行输出
} // for 结束
```

```java
// 输出数组的内容
public void outputGrades()
{
    System.out.println("The grades are:");
    for (int student = 0; student < grades.length; student++) {
        System.out.printf("Student %d: %d\n", student + 1, grades[student]);
    }
} // 方法 outputGrades 结束
```

Fig. 7.14 使用数组存储测试成绩的 GradeBook 类。（4 部分中的第 4 部分。）

`MethodGrades`（第 31–57 行）包含了一系列方法调用，用于输出报告。第 40 行调用 `outputGrades` 来打印数组的内容。虽然索引从 0 开始，但教授通常会从 1 开始为学生编号。因此，135–136 行使用学生编号输出每个成绩（见图 7.15）。
