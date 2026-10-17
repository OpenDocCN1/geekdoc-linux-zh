
```java
public class SetTest {

    private static final String colors[] = { "red", "white", "blue",

        "green", "gray", "orange", "tan", "white", "cyan",

        "peach", "gray", "orange" };

    // 创建并输出 ArrayList

    public SetTest() {

        List<String> list = Arrays.asList(colors);

        System.out.printf("ArrayList: %s\n", list);

        printNonDuplicates(list);

    }

    // 从数组创建集合以消除重复

    private void printNonDuplicates(Collection<String> collection) {

        // 创建一个 HashSet

        Set<String> set = new HashSet<String>(collection);

        System.out.println("\Nonduplicates are: ");

        for (String s : set) {

            System.out.printf("%s ", s);

        }

        System.out.println();

    }

    public static void main(String[] args) {

        new SetTest();

    }

}
```

`ArrayList`: [red, white, blue, green, gray, orange, tan, white, cyan, peach, gray, orange]
Nonduplicates are:
red cyan white tan gray green orange blue peach

**图 19.18** | 使用 `HashSet` 从字符串数组中移除重复值。

集合框架还包括 `SortedSet`（继承自 `Set`），用于保持元素按排序顺序排列的集合——可以是元素的自然顺序（例如，数字按升序排列），或由 `Comparator` 指定的顺序。`TreeSet` 类的项在添加到 `TreeSet` 时就会进行排序。图 19.19 中的程序将字符串放入 `TreeSet` 中。此示例还演示了范围视图方法，允许程序查看集合的一部分。

第 16–17 行创建了一个包含 `String` 的 `TreeSet`。

```java
// Fig. 19.19: SetTest.java
// 使用 TreeSet 和 SortedSet。

import java.util.Arrays;
import java.util.SortedSet;
import java.util.TreeSet;

public class SortedTest {

    private static final String names[] = {"yellow", "green", "tan", "red", "white", "orange"};

    // 创建并输出 TreeSet

    public SortedTest() {

        SortedSet<String> tree = new TreeSet<>(Arrays.asList(names));

        System.out.println("Sorted set: " + tree);

        for (String s : tree) {

            System.out.printf("%s ", s);

        }

        System.out.println();

    }

    public static void main(String[] args) {

        new SortedTest();

    }

}
```

## 性能提示 19.7

哈希表中的负载因子是内存空间/执行时间权衡的经典示例。通过增加负载因子，我们可以获得更好的内存利用率，但由于哈希冲突的增加，程序运行速度会变慢。通过减少负载因子，我们可以获得更快的速度，但由于哈希表很大一部分保持为空，内存利用率会较低。

哈希表的编程非常复杂。计算机科学在名为“数据结构”和“算法”的课程研究哈希方案。Java 提供了 `HashMap` 和 `Map` 类，让程序员能够在无需实现哈希表机制的情况下使用哈希。这个概念在我们学习面向对象编程时非常重要。正如前面的章节所述，类封装并隐藏了复杂性（即实现细节），并且对用户友好。正确设计类以表现出这种行为是面向对象编程领域最有价值的技能之一。图 19.20 使用 `HashMap` 来统计字符串中每个单词出现的次数。

第 17 行创建一个具有默认初始容量（16 个元素）和默认负载因子（0.75）的空 `HashMap`——这些默认值被构建在 `HashMap` 的实现中。当 `HashMap` 中被占用槽的数量超过容量时，容量会自动翻倍。注意，`HashMap` 是一个泛型类，接受两个类型参数。第一个指定键的类型（即 `String`），第二个指定值的类型（即 `Integer`）。记住，传递给泛型类的类型参数必须是引用类型，第二个类型参数是 `Integer` 而不是 `int`。第 18 行创建一个 `Scanner` 来从标准输入读取内容。第 19 行调用方法 `createMap`（第 24–46 行），该方法使用映射来存储字符串中每个单词出现的次数。第 27 行调用扫描器的 `nextLine` 方法来获取用户输入，第 30 行创建一个 `StringTokenizer` 将输入字符串拆分为：

```java
// Fig. WordTypeCount.java
// 程序统计字符串中每个单词出现的次数

import java.util.StringTokenizer;
import java.util.Map;
import java.util.HashMap;
import java.util.Set;
import java.util.TreeSet;
import java.util.Scanner;

public class WordCount {

    private Map<String, Integer> map;

    private Scanner scanner;

    public WordCount() {

        map = new HashMap<String, Integer>(); // create HashMap

        scanner = new Scanner(System.in); // create scanner
```

图 19.20 | `HashMaps` 和 `Maps`。（3 部分中的第 I 部分）

```java
    19 createMap(); // 根据用户输入创建 map
    20 displayMap(); // 显示 map 内容
    21 } // WordCount 构造函数结束

    23 // 从用户输入创建 map
    24 private void createMap()
    25 {
    26 System.out.println(" Enter a string: "); // 提示用户输入
    27 String input = scanner.nextLine();
    28 
    29 //为输入创建 StringTokenizer
    30 StringTokenizer tokenizer = new StringTokenizer(input );
    31 
    32 // 处理输入文本
    33 while ( tokenizer.hasMoreTokens()) { // 当有更多输入时循环
    34 
    35 String word = tokenizer.nextToken().toLowerCase(); // 获取单词
    36 
    37 // 如果 map 包含该单词
    38 if (map.containsKey( word )) // 单词是否在 map 中
    39 {
    40 int count = map.get(word); // 获取当前计数
    41 map.put(word, count + 1); // 计数加1
    42 } // if 结束
    43 else
    44 { map.put(word, 1); // 向 map 添加计数为 1 的新单词
```
