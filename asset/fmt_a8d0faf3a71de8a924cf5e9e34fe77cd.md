
85: `invokirtual` #4 // Method

88: `goto` 99

91: `getstatic` #2 // Field `java/lang/System.out:Ljava/io/PrintStream;`

94: `ldc` #9 // String `unknown`

96: `invokirtual` #4 // Method

99: `return`

如果输入值是 0，则显示为 `zero`；如果输入值是 1，则显示为 `one`；如果输入值是 2，则显示为 `two`；如果输入值是 3，则显示为 `three`；如果输入值是 4，则显示为 `four`；如果以上的种，则显示字符串 `unknown`。

## 54.13 数组

### 54.13.1 简单的例子

我们先创建一个有 10 元素的整型数组，然后逐渐填入 0~9：程序如下：

```java
public static void main(String[] args)
{
    int a[] = new int[10];
    for (int i=0; i<10; i++)
        a[i]=i;
}
```

```java
public static void main(java.lang.String args[]) {
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=3, locals=3, args_size=1
0: bipush 10
2: newarray int
4: astore_1
5: iconst_0
6: istore_2
7: iload_2
8: bipush 10
10: if icne 23
13: aload_1
14: iload_2
15: istore_2
16: iastore
17: iinc
20: goto 7
23: invokirtual #4 // Method
27: return
}
```

### 54.13.2 数组元素求和

```java
public class ArraySum
{
    public static int f(int[] a)
    {
        int sum=0;
        for (int i=0; i<a.length; i++)
            sum+=a[i];
        return sum;
    }
}
```

```java
public static int f(int[]);
flags: ACC_PUBLIC, ACC_STATIC
Code:
stack=3, locals=3, args_size=1
0: iconst_0
1: istore_1
2: iconst_0
3: istore_2
4: iload_2
5: aload_0
6: arraylength
7: ificmpge 2
10: iload_1
11: aload_0
12: iload_2
13: iadd
14: istore_1
15: iinc 2, 1
19: goto 4
22: iload_1
23: return
}
```

```java
java/io/PrintStream.print:(Ljava/lang/String;)V
8: getstatic #2 // Field
java/lang/System.out:Ljava/io/PrintStream:
11: aload_0
12: icost_1
13: aoad
14: invokevirtual #4 // Method
java/io/PrintStream.print:(Ljava/lang/String;)V
17: getstatic #2 // Field
java/lang/System.out:Ljava/io/PrintStream:
20: ldc #5 // String . How are you?
22: invokevirtual #6 // Method
java/io/PrintStream.println:(Ljava/lang/String;)V
25: return
```

偏移值为11的指令`aload_0`加载了`LVA`（局部变量数组）的第0个存储单元。索引`main()`的唯一参数值通过偏移量为12和13的`icost_1`和`aoad`指令的作用是获取数组第一个元素的引用指针（也就是索引号为0的元素首地址）。偏移量为14的指令通过`TOS`被调用函数传递字符串的引用指针，这个引用指针起始就是`println`方法的输入变量。

### 54.13.4 预初始化的数值

```java
class
{
    public static String[] months =
    {
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December"
    };
    public String get_month(int i)
    {
        return months[i];
    }
}
```

我们在这个列表中列举了一个有预赋值的数组，它的元素是字符串型的，其值是从一月到十二月的英文单词，分别是`January`, `February`, `March`, `April`, `May`, `June`, `July`, `August`, `September`, `October`, `November`和`December`。

函数`get_month`的功能比较简单，它是输入一个整型的数，从而能在数组对应位置输出相应月份的字符串。

```java
public java.lang.String get_month(int i);
flags: ACC_PUBLIC
Code:
stack=2, locals=2, args_size=2    // Field months:
0: getstatic #2
java/lang/String;
3: iload_1
4: aload
5: return
```

`aload`指令从`TOS`取出数组的指针和索引号，将指定元素推入栈。在Java的概念中，字符串是对象数据（确切的指针则是头部前面的指令）。同理，后面的`return`指令返回的是字符串的引用指针。另一个问题是：`months[]`是如何初始化的？也就是说，数组的初始值到十二月份的字符串是如何被赋值到数组的相关位置的？

```java
static {}
flags: ACC_STATIC
Code:
stack=4, locals=0, args_size=0
0: bipush #12 // class java/lang/String
2: anew
3: dup
5: iconst_0
7 ldc // January
9: astore
10: dup
11: iconst_1 // February
12: ldc
14: astore
15: dup
16: iconst_2 // March
17: ldc
19: astore
20: dup
21: iconst_3 // April
22: ldc
24: astore
25: dup
26: iconst_4 // May
27: ldc
29: astore
30: dup
31: iconst_5 // June
32: ldc #9
34: astore
35: dup
36: bipush 6
38: ldc #10 // July
40: astore
41: dup
42: bipush 7
44: ldc #11 // August
46: astore
47: dup
48: bipush 8
50: ldc #12 // September
52: astore
53: dup
54: bipush 9
56: ldc #13 // October
58: astore
59: dup
60: bipush 10
62: ldc #14 // November
64: astore
65: dup
66: iconst_11
68: ldc #15 // December
70: astore
71: putstatic #2 // Field months:
java/lang/String;
74: return;
```
