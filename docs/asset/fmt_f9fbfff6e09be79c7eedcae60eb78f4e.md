
```java
// 输出数组中值的方法
public String toString() {
    StringBuilder temporary = new StringBuilder();
    // 遍历数组
    for (int element : data) {
        temporary.append("\n" + element + " "); // 添加换行符
    }
    return temporary.toString();
} // end method Selection
// end class SelectionSort
```

图 16.6 `SelectionSort` 类。（2 部分中的第 2 部分）。

第 22–39 行声明了 `sort` 方法。第 24 行声明了变量 `smallest`，它将存储剩余数组中最小元素的索引。第 27–38 行循环 `data.length - 1` 次。第 29 行初始化最小元素的索引为当前元素。第 32–34 行遍历剩余元素。对于这些元素中的每一个，第 33 行将其值与最小元素的值进行比较。如果当前元素小于最小元素，第 34 行将当前元素赋值给 `smallest`。当循环结束时，`smallest` 剩余数组中最小元素的索引。第 36 行调用 `swap`（第 42–47 行）将最小元素放置在下一个位置。

16.7 的第 9 行创建一个包含 10 个元素的 `SelectionSort` 对象。第 12 行隐含的方法用于输出该对象。第 14 行调用 `sort` 方法（16.6 的第 22–39 行），使用选择排序对元素。第 16–17 行输出已排序的数组。该程序的输出使用横线来表示每轮后已排序的数组位置。在每一轮中，星号旁边的元素和横线右方的元素是交换的两个值。

# 16.3 排序算法

```java
// Fig 16.7: SelectionSortTest.java
// 测试选择排序类。
public class SelectionSortTest {
    public static void main(String[] args) {
        // 创建对象执行选择排序
        SelectionSort sortArray = new SelectionSort( 10 );

        System.out.println("Unsorted array:");
        System.out.println(sortArray); // 输出未排序数组

        sortArray.sort(); // 排序数组
        System.out.println("Sorted array:");
        System.out.println(sortArray); // 输出排序数组
    } // end main
} // end class SelectionSort
```

未排序数组：

61 87 80 58 40 50 20 13 71 45

第 1 轮后：13 87 80 58 40 50 20* 71 45

第 2 轮后：13 20 80 58 40 50 87* 61 45

第 3 轮后：13 20 40 58 50 87 61* 71*

第 4 轮后：13 20 40 45 80 50 87 61 71*

第 5 轮后：13 20 40 45 50 80* 87 61 58

第 6 轮后：13 20 40 45 50 58 87 61 80*

第 7 轮后：13 20 40 45 50 58 87 61 80

第 8 轮后：13 20 40 45 50 58 61 71 80*

第 9 轮后：13 20 40 45 50 58 61 71 80

已排序数组：

13 20 40 45 50 58 61 71 80 87

图 16.7 `SelectionSortTest` 类。

## 选择排序的效率

选择排序算法的运行复杂度为 $O(n^2)$。16.6 第 22–39 行的 `sort` 方法包含两个循环，外部循环（第 27–38 行）在第一次迭代中执行 $n-1$ 次。内部循环（第 32–34 行）寻找最小元素，在第一次迭代中迭代 $n-1$ 次，第二次迭代中 $n-2$ 次，$\dots$ 1 次。在大 O 表示法中，这是 $n(n-1)/2$。

## 16.2 插入排序

插入排序是另一种简单但效率的算法。该算法的第一次迭代获取数组的第二个元素，如果小于第一个元素，则与第一个元素交换。第二次迭代查看第三个元素。

以以下数组作为示例。[注：此数组与选择排序中使用的相同。]

34 56 4 10 77 51 93 30 5

实现插入排序的程序首先查看前两个元素 34 和 56。这两个元素已经有序，因此程序继续（如果它们无序，程序将交换它们）。

在下一次迭代中，程序存储第三个值 4。该值小于 56，因此程序将 4 存入临时变量并将 56 向右移动。程序随后检查并确定 4 小于 34，因此将 34 向右移动。程序现在到达数组开头，因此将 4 放在零索引元素位置。我们的数组现在变为：

4 34 56 10 77 51 93 30 5

在下一次迭代中，程序将值 10 存入临时变量。程序将 10 与 56 比较，因为它比 10 大，程序将 56 向右移动。程序随后将 10 与 34 比较，将 34 向右移动一个元素。程序观察到 10 大于 4，并将 10 放在元素 1 位置。数组现在变为：

4 10 34 56 77 51 93 30 5

图 16.8 声明了 `InsertionSort` 类。第 22–46 行声明了 `sort` 方法。第 24 行声明了变量 `insert`，它持有要插入的元素，在此期间我们移动其他元素。

### 16.3 排序算法 781

```java
// 图 16.8: InsertionSort.java
// 创建一个填充随机整数数组的类。
// 提供一个使用插入排序对数组进行排序的方法。
import java.util.Random;
public class InsertionSort {
    private int[] data; // 数值数组
    private static Random generator = new Random();

    // 创建指定大小的数组并填充随机整数
    public InsertionSort(int size) {
        data = new int[size]; // 为数组创建空间
        // 填充 10-99 范围内的随机整数
        for (int i = 0; i < size; i++) {
            data[i] = 10 + generator.nextInt(90);
        }
    } // InsertionSort 构造函数

    // 使用插入排序排序数组
    public void sort() {
        int insert; // 用于存储待插入元素的临时变量
        // 遍历 data.length - 1 个元素
        for (int next = 1; next < data.length; next++) {
            // 将当前元素的值存入 insert
            insert = data[next];
            // 初始化放置元素的位置
            int moveItem = next;
            // 寻找放置当前元素的位置
            while (moveItem > 0 && data[moveItem - 1] > insert) {
                // 向右移动一个位置
                data[moveItem] = data[moveItem - 1];
                moveItem--;
            }
            data[moveItem] = insert; // 放置插入元素
            printPass(next, moveItem); // 输出算法的每一轮
        }
    }

    // 打印算法的一轮
    public void printPass(int pass, int index) {
        System.out.print(String.format("after pass %2d: %s", pass));
    }
}
```

**图 16.8** | `InsertionSort` 类。（2 部分中的第 1 部分）。

# 第 16 章 查找与排序
