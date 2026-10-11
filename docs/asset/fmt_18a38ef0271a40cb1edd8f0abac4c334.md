
```java
// 图 16.5: BinarySearchTest.java
// 使用二分搜索在数组中定位项。
import java.util.Scanner;
public class BinarySearchTest {
    public static void main(String[] args) {
        // 创建 Scanner 对象以输入数据
        Scanner input = new Scanner(System.in);
        // 创建数组
        int[] data = {10, 23, 34, 42, 50, 60, 70, 80, 90, 100};
        // 搜索键
        int searchElement = 23;
        int low = 0;
        int high = data.length - 1;
        int location = -1;
        
        while (
}
```

**图 16.5** `BinarySearchTest` 类。（2 部分中的 1。）

# 16.3 排序算法

排序是将数据按照特定的顺序重新排列的过程。本节将介绍三种常见的排序算法。

## 16.3.1 选择排序

选择排序是一种简单但效率较低的算法。算法的第一次迭代选择数组中的最小元素，并将其与第一个元素交换。

```java
    for (int i = 0; i < data.length - 1; i++) {
        int min = i;
        for (int j = i + 1; j < data.length; j++) {
            if (data[j] < data[min]) {
                min = j;
            }
        }
        int temp = data[i];
        data[i] = data[min];
        data[min] = temp;
    }
```

选择排序的时间复杂度复杂度为 $O(n^2)$，这意味着对于大数据集它的性能并不理想。

## 16.3.2 插入排序

插入排序类似于我们整理扑牌的方式。它每次取一个元素，并将其“插入”到前面已经排序好的部分的正确位置。

```java
    for (int i = 1; i < data.length; i++) {
        int key = data[i];
        int j = i - 1;
        while (j >= 0 && data[j] > key) {
            data[j + 1] = data[j];
            j--;
        }
        data[j + 1] = key;
    }
```

插入排序在最坏情况下同样是 $O(n^2)$，但当数据已经部分有序时，它的表现非常出色。

## 16.3.3 归并排序

归并排序是一种基于分治策略的算法。它将数组划分为两部分，递归地对这两个部分进行排序，然后将排序后的两个部分合并。

```java
    public static void mergeSort(int[] data, int low, int high) {
        if (low < high) {
            int mid = (low + high) / 2;
            mergeSort(data, low, mid);
            mergeSort(data, mid + 1, high);
            merge(data, low, mid, high);
        }
    }
```

归并排序的时间复杂度为 $O(n \log n)$，这使其在处理大量数据时比选择排序和插入排序快得多。

```java
// Fig 16.6: SelectionSort.java
// 创建一个填充随机整数数组的类。
// 提供一个使用选择排序对数组排序的方法。
import java.util.Random;
public class SelectionSort {
    private int[] data; // 值的数组
    private static Random generator = new Random();

    // 创建指定指定的数组并填充随机整数
    public SelectionSort(int size) {
        data = new int[size]; // 为数组创建空间

        // 用 10-99 范围内的随机整数填充数组
        for (int i = 0; i < size; i++) {
            data[i] = 10 + generator.nextInt(90);
        }
    } // SelectionSort 构造函数

    // 使用选择排序排序数组
    public void sort() {
        int smallest; // 最小元素的索引
        // 遍历 data - 1 个元素
        for (int i = 0; i < data.length - 1; i++) {
            smallest = i; // 剩余数组的第一个索引
            // 循环寻找最小元素的索引
            for (int index = i + 1; index < data.length; index++) {
                if (data[index] < data[smallest])
                    smallest = index;
            }
            swap(i, smallest); // 将最小元素交换到当前位置
            printPass(i, smallest); // 输出算法的步骤
        } // end for
    } // end sort 方法

    // 交换两个元素之间值的辅助方法
    public void swap(int first, int second) {
        int temporary = data[first]; // 将第一个值存入临时变量
        data[first] = data[second]; // 用第二个替换第一个
        data[second] = temporary; // 将临时变量放入第二个
    } // end swap

    // 打印算法的一轮执行
    public void printPass(int pass, int index) {
        System.out.println(String.format("after pass %2d: %s", pass, index));
    }
}
```

图 16.6 | `SelectionSort` 类。（ 2 部分中的第 1 部分）。

# 第 16 章 搜索与排序

```java
// 输出直到被选定的元素
for (int i = 0; i < index; i++) {
    System.out.print(data[i] + " ");
}
System.out.print(data[index] + " * "); // 明交换
// 完成数组输出
for (int i = index + 1; i < data.length; i++) {
    System.out.print(data[i] + " ");
}
System.out.print("\n"); // 用于对齐
// 明已排序的数组部分
for (int j = 0; j < pass; j++) {
    System.out.print("-- ");
}
System.out.println("\n"); // 添加换行
// end methodSelection
```
