
```java
// 有性检查；将无效值置零

public void setState(int h, int m, int s) {

    hour = (h > 0 && h < 24) ? h : 0; // 验证小时

    minute = (m > 0 && m < 60) ? m : 0; // 验证分钟

    second = (s > 0 && s < 60) ? s : 0; // 验证秒

}

// 转换为通用格式 (HH:MM:SS) 的字符串

public String toUniversalString() {

    return String.format("%02d:%02d:%02d", hour, minute, second);

}

// 转换为标准格式 (H:MM:SS AM 或 PM) 的字符串

public String toString() {

    return String.format("%d:%02d:%02d %s",

        (hour == 0 || hour == 12) ? 12 : hour,

        minute, second, (hour < 12 ? "AM" : "PM"));

}

}
```

图 8.18 | 为了重用而封装 `Time1`。（2部分中的第2部分。）

对于步骤 2，我们添加了包声明（第 3 行），声明了一个名为 `com.deitel.jht7.ch08` 的包。在 Java 源文件的开头放置包声明表示文件中声明的类是指定包的一部分。只有包声明、导入声明和注释可以出现在类大括号之外。

- 1. 一个包声明（如果有）
- 2. 导入声明（如果有）
- 3. 类声明。

特定文件中只能有一个类声明是公共的。文件中的其他类位于包中，并可以被包中的其他类使用。非公共类位于包中以支持可重用类。为了给每个包提供唯一名称，Sun Microsystems 提供了一套 Java 程序员应该遵循的包命名规范。每个包名都应该以你的域名的反转开头。例如，你的域名是 `deitel.com`，那么包以 `com.deitel` 开头。对于域名 `edu`，包名应该以 `edu` 开头。如果域名是反转的，你可以为你的包选择你想要的任何其他名称。如果你属于一个拥有许多部门的部门或一所拥有许多学院的大学，你可能希望使用你的部门或学院的名称作为包中的下一个名称。

### 步骤 3：编译封装的类

步骤 3 是编译该类，使其存储在适当的包中。当编译包含包声明的 Java 文件时，生成的类文件被放置在包声明指定的目录中。命令行选项 `-d` 会导致 `javac` 编译器根据类的包声明创建目录。例如，在命令窗口中使用以下命令：

```
javac -d . Time1.java
```

`-d` 之后的点 (`.`) 代表 Windows、Linux 操作系统（以及其他系统）上的当前目录。执行编译命令后，当前目录包含一个名为 `deitel` 的目录，其中包含一个名为 `jht7` 的目录，其中包含一个名为 `ch08` 的目录。在 `ch08` 目录中，你可以找到 `Time1.class` 文件。[注意：如果不使用 `-d` 选项，你必须在编译后复制或移动文件到适当的目录。]

包名是完全限定的一部分，因此 `Time1` 的实际上是 `deitel.jht7.ch08`。你可以在程序中使用此完全限定名，也可以导入该类并使用其简单名来标识自己——`Time1`。如果另一个包也包含 `Time1` 类，可以使用完全限定名来区分程序中的类并防止名称冲突（或名称碰撞）。

### 步骤 4：导入可重用类

一旦类存储在它的包中，就可以将该类导入到程序中。在图 8.19 的 `Time1Test` 应用程序中，第 3 行指定 `Time1` 类应该被用于 `Time1Test`。`Time1Test` 位于默认包中，因为该类的 `.java` 文件不包含包声明。由于两个类位于不同的包中，因此需要第 3 行的导入来使用类 `Time1`。

```
// Fig. 8.19: TimePackageTest.java
// 在应用程序中使用 Time 对象。

import com.deitel.jht7.ch08.Time; // 导入类

public class TimePackageTest {

    public static void main(String[] args) {

        // 创建并初始化 Time 对象

        Time time = new Time(); // 调用 Time 构造函数

        // 输出时间的字符串

        System.out.print("The initial universal time is: ");

        System.out.println(time.toUniversalString());

        System.out.print("The standard time is: ");

        System.out.println(time.toString());

        System.out.println(""); // 输出空行

        // 修改时间并输出更新的时间

        time.setTime(13, 27, 6);

        System.out.print("Universal time after setTime is: ");

        System.out.println(time.toUniversalString());

        System.out.print("Standard time after setTime is: ");

        System.out.println(time.toString());

        System.out.println(""); // 输出空行

        // 使用无效值设置时间；输出更新的时间

        time.setTime(98, 99, 99);

        System.out.println("After attempting invalid settings: ");

        System.out.print("Universal time: ");

        System.out.println(time.toUniversalString());

        System.out.print("Standard time: ");

        System.out.println(time.toString());

    } // end main

} // end class TimePackageTest
```

| Output |
| :--- |
| The initial universal time is: 00:00:00 |
| The standard time is: 12:00:00 AM |
| Universal time after setTime is: 13:27:06 |
| Standard time after setTime is: 1:27:06 PM |
| After attempting invalid settings: |
| Universal time: 00:00:00 |
| Standard time: 12:00:00 AM |

**Fig. 8.19** 在应用程序中使用 Time 对象。

第 3 行被称为单类型导入声明——即该导入声明指定了要导入的一个类。当你的程序使用同一个包中的多个类时，可以使用一个导入语句导入这些类。例如，导入语句

```java
import java.util.*; // 导入 java.util 包中的类
```
