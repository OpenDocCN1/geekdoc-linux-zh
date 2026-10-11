
图 19.8 使用 `sort` 算法按升序排列 `List` 的元素（第 20 行）。回想一下，`List` 是一个泛型类型，接受一个参数来指定列表元素类型——第 15 行将 `list` 声明为 `List<String>`。注意，第 18 行和第 23 行分别使用对 `List` 的 `toString` 方法的隐式调用，按输出中第二行和第四行所示的格式输出列表内容。

### 降序排序

图 19.9 对图 19.8 中使用的相同字符串列表进行降序排序。示例引入了 `Comparator` 接口，它用于以不同的顺序对集合元素进行排序。第 21 行调用 `Collections` 的 `sort` 方法对 `List` 进行降序排序。静态的 `Collections.reverse` 方法返回一个 `Comparator`，按反向顺序排列集合元素。

```java
// 图 19.8: Sort1.java
// 使用算法 sort。
import java.util.List;
import java.util.Arrays;
import java.util.Collections;

public class Sort1 {
    private static final String suits[] = {
        {"Hearts", "Diamonds", "Clubs", "Spades"};

    // 显示数组元素
    public void printElements() {
        List<String> list = Arrays.asList(suits); // 创建 List

        // 输出列表
        System.out.printf("Unsorted array elements:\n%s\n", list);
        Collections.sort(list); // ArrayList ArrayList

        // 输出列表
        System.out.printf("Sorted array elements:\n%s\n", list);
    }
    public static void main(String[] args) {
        Sort1 sort1 = new Sort1();
        sort1.printElements();
    } // end main
} // end class Sort1
```

Unsorted array elements:

[Hearts, Diamonds, Clubs, Spades]

Sorted array elements:

[Clubs, Diamonds, Hearts, Spades]

图 19.8 | Collections 方法 `sort`。

```java
// 图 19.9: Sort2.java
// 使用 Comparator 对象配合算法 sort。
import java.util.List;
import java.util.Arrays;
import java.util.Collections;

public class Sort2 {
{
```

## 904 第19 章 集合

```java
private static final String suits[] =
    { "Hearts", "Diamonds", "Clubs", "Spades" };

// 输出 List.elements
public void printElements() {
    List<String> list = Arrays.asList(suits); // 创建 List

    // 输出 List elements
    System.out.printf("Unsorted array:\n%s\n", list);

    // 使用比较器对列表进行倒序
    Collections.sort(list, Collections.reverseOrder());

    // 输出 List elements
    System.out.printf("Sorted list elements:\n%s\n\n", list);
} // 结束方法 printElements
public static void main(String args[]) {
    Sort2 sort2 = new Sort2();
    sort2.printElements();
} // 结束 main
// 结束类 Sort2
```

未排序数组元素：

[Hearts, Diamonds, Clubs, Spades]

排序后的列表元素：

[Spades, Hearts, Diamonds, Clubs]

图 19.9 | 使用 `Comparator` 对象的 `Collections` 方法 `sort`。（2部分中的2部分。）

## 使用 Comparator 排序

图 19.10 创建了一个名为 `TimeComparator` 的自定义比较器，它实现了 `Comparator` 接口以比较两个 `Time2` 对象。在图8.5中声明的 `Time2` 类表示带有小时、分、秒的时间。

`TimeComparator` 类实现了 `Comparator` 接口，这是一个接受一个参数（在本例中为 `Time2`）的泛型类型。`compare` 方法（第7–26行）执行 `Time2` 对象之间的比较。如果小时不同（第12行），我们返回此值。如果此值为正，则第一个大于第二个，第一个时间也大于第二个时间。如果此值为负，则第一个小时小于第二个，第一个时间也小于第二个时间。如果此值为零，说明小时相同，我们必须测试分钟（可能还需秒）来确定哪个时间更大。

图 19.11 展示了一个使用自定义比较器类 `TimeComparator` 的列表。第11行创建了一个 `Time2` 对象的 `ArrayList`。记得 `ArrayList` 和 `List` 都是泛型类型，接受一个指定集合元素类型的类型参数。第13–17行创建了五个 `Time2` 对象并将它们添加到列表中。第23行调用 `sort` 方法，并传递了我们的 `TimeComparator` 类的对象（图19.10）。

## 19.6 集合算法

```java
// 图 19.10: TimeComparator.java
// 比较两个 Time2 对象的自定义比较器类。
import java.util.Comparator;
public class TimeComparator implements Comparator<Time2> {
    public int compare(Time2 time1, Time2 time2) {
        int hourCompare = time1.getHour() - time2.getHour(); // 比较小时
        // 测试第一个小时
        if ( hourCompare != 0 )
            return hourCompare;
        int minuteCompare = time1.getMinute() - time2.getMinute(); // 比较分钟
        // 测试分钟
        if ( minuteCompare != 0)
            return minuteCompare;
        int secondCompare = time1.getSeconds() - time2.getSeconds(); // 比较秒
        return secondCompare; // 比较秒的结果
    } // 结束方法 compare
} // 结束类 TimeComparator
```

**图 19.10** | 比较两个 `Time2` 对象的自定义比较器类。
