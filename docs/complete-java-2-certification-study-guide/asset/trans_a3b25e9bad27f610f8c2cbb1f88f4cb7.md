

## 第 4 章 • 转换与强制转换

假设所需的强制转换通过了编译，则必须在运行时进行第二次检查。第二次检查确定被转换的对象的类是否与新类型兼容。（这在编译时无法完成，因为被转换的对象在当时还不存在。）这里，“兼容”意味着该类可以根据之前节讨论的转换规则进行转换。以下规则涵盖了常见的运行时情况：

- 如果 Newtype 是一个类，则被转换表达式的类必须是 Newtype 或继承自 Newtype。
- 如果 Newtype 是一个接口，则被转换表达式的类必须实现 Newtype。

现在是时候看些例子了！再次看一眼你在本章之前看到的 Fruit/Citrus（水果/柑橘类）层次结构，它在图 4.10 中重复出现。
考虑以下代码：

```java
1. Grapefruit g, gl;
2. Citrus c;
3. Tangelo t;
4. g = new Grapefruit(); // 类为 Grapefruit
5. c = g; // 合法的赋值转换，
   // 不需要强制转换
6. g = (Grapefruit)c; // 合法的强制转换
7. t = (Tangelo)c; // 非法强制转换
   // 抛出异常
```

## 图 4.10 水果层次结构（重复）

![](img/09f8389b7ae2705d1ab14be2d5e857e3_152_0.png)

## 对象引用转换

这段代码有四个引用但只有一个对象。对象 c 是 Grapefruit，因为在第 4 行调用了 Grapefruit 的构造函数。第 5 行的赋值 `c = g` 是一个完全合法的赋值转换（向上继承层次结构），因此不需要显式强制转换。在第 6 行和第 7 行中，Citrus 被强制转换为 Grapefruit 和 Tangerelo。记住，在类之间进行强制转换时，两者中的一个（哪一个都行）必须是另一个的子类。第一次转换是从 Citrus 到其子类 Grapefruit；第二次是在编译时从 Citrus 到其子类 Tangerelo。因此，这两种强制转换都是合法的——但编译器无法确定 `c` 引用的对象，所以它接受了这两种强制转换，并让命运在运行时决定结果。

当代码执行时，JVM 最终决定执行第 6 行：`g = (Grapefruit)c;`。`c` 的类被确定为 Grapefruit，并没有对象将 Grapefruit 转换为 grapefruit。

第 7 行尝试（在运行时）将 `c` 强制转换为 Tangerelo 类型。`c` 的类仍然是 Grapefruit，而 Grapefruit 无法强制转换为 Tangerelo。为了使强制转换合法，`c` 的类必须是 Tangerelo 本身或其子类。由于情况并非如此，会抛出一个运行时异常 (java.lang.ClassCastException)。

现在来看一个对象为接口类型的例子。首先考虑以下代码：

```java
1. Grapefruit g, g1;
2. Squeezeable s;
3. g = new Grapefruit();
4. s = g; // 将 Grapefruit 转换为 Squeezeable (OK)
5. g1 = s; // 将 Squeezeable 转换为 Grapefruit
// (编译错误)
```

这段代码无法编译。第 5 行尝试将接口（Squeezeable）转换为类（Grapefruit）。Grapefruit 实现了 Squeezeable 并不重要。隐式将接口转换为类永远是不被允许的；这是你必须使用显式强制转换来告诉编译器你知道自己在做什么的情况之一。加上强制转换后，第 5 行变为：

```java
5. g = (Grapefruit)s;
```

添加强制转换会让编译器感到高兴。在运行时，JVM 检查 `s` 的类（即 Grapefruit）是否可以转换为 Grapefruit。它显然可以，所以这种操作是被允许的。对于最后一个涉及数组的例子，请看以下代码：

```java
1. Grapefruit g[];
2. Squeezeable s[];
3. Citrus c[];
4. g = new Grapefruit[500];
5. s = g; // 将 Grapefruit 数组转换为
// Squeezeable 数组 (OK)
6. c = (Citrus[])s; // 将 Squeezeable 数组转换为 Citrus
// 数组 (OK)
```

第 6 行将 Squeezeable 数组 (s) 强制转换为 Citrus 数组 (c)。如果转换数组元素是合法的（且元素类型是引用而不是基本数据类型），则数组是合法的。在这个例子中，问题是 Squeezeable（数组 s 的元素类型）是否可以强制转换为 Citrus（强制转换数组的元素类型）。上一个例子已经显示这是一个合法的强制转换。

## 总结

基本类型值和对象引用是两种不同的数据类型。它们都可以进行转换（隐式）或强制转换（显式）。基本类型的更改是由赋值转换、方法调用转换、算术提升转换或显式强制转换引起的。

基本类型只有在转换缩小了数据范围时才能进行转换。只要旧类型和新类型都不是布尔类型，基本类型就可以通过强制转换来缩小范围。

对象引用可以进行转换或强制转换；控制这些操作的规则非常广泛，因为必须涵盖许多情况组合。通常情况下，“向上”继承树可以通过转换隐式地完成，而“向下”移动树移动则需要显式强制转换。对象引用类型的更改是由赋值转换、方法调用转换或显式强制转换引起的。

## 考试要点

理解基本类型转换何时发生。当新类型与旧类型相同时，会发生赋值转换和方法调用转换。理解算术提升何时发生。理解何时需要强制转换。

理解基本类型转换何时发生。当新类型与旧类型相同时，会发生赋值转换和方法调用转换。理解算术提升何时发生。理解何时需要强制转换。

理解基本类型转换何时发生。当新类型与旧类型相同时，会发生赋值转换和方法调用转换。理解算术提升何时发生。理解何时需要强制转换。

## 总结

## 复习题

1. 下列哪种陈是正确的？（选择一个。）
- A. 只有基本类型被转换；以更改类型。
- B. 只有对象引用被转换；以更改类型。
- C. 基本类型和对象引用都可以转换。
- D. 需要强制转换。
- E. 对象引用的强制转换需要运行时检查。

2. 以下代码中的哪一行无法编译？

```java
1. byte b = 5;
2. char c = '5';
3. short s = 5;
4. int i = 5;
5. float f = 5.1f;
6. b = s;
7. i = c;
8. if (f)
9. f = i;
```

A. 第 1 行
B. 第 2 行
C. 第 3 行
D. 第 4 行
E. 第 5 行
F. 第 6 行
G. 第 7 行
H. 第 8 行
I. 第 9 行

3. 以下代码可以编译吗？

```java
1. byte b = 2;
2. byte b1 = 3;
3. b = b1;
```

A. 是
B. 否

4. 在以下代码中，`result` 的可能类型是什么？（选择完整的答案。）

```java
1. byte b = 11;
2. short s = 3;
3. result = b;
```

A. byte, short, int, float, double
B. boolean, short, char, int, float, double
C. byte, short, char, int, float, double
D. byte, short
E. int, float, double

5. 考虑以下类：

```java
class Cruncher {
void crunch(int i) {
    System.out.println("int version");
}
void crunch(String s) {
    System.out.println("String version");
}
public static void main(String args[]) {
    Cruncher crun = new Cruncher();
    char ch = 'p';
    crun.crunch(ch);
}
```

以下哪种陈述正确？（选择一个。）

A. 第 5 行无法编译，因为方法不能重写。
B. 第 12 行无法编译，因为没有接收 char 参数的 crunch 版本。
C. 代码可以编译，但在 12 行会抛出异常。
D. 代码可以编译并输出：int version。
E. 代码可以编译并输出：String version。

6. 下列哪种陈述是正确的？（选择一个。）
- A. 对象引用可以在赋值中转换，但在方法调用中不能。
- B. 对象引用可以在方法调用中转换，但在赋值中不能。
- C. 对象引用可以在方法调用和赋值中进行转换，但控制这些转换的规则非常不同。
- D. 对象引用可以在方法调用和赋值中进行转换，且控制这些转换的规则是相同的。
- E. 对象引用永远无法转换。

7. 考虑以下代码。哪一行无法编译？

```java
1. Object ob = new Object();
2. String[] stringarr = new String[50];
3. Float floater = new Float(3.14f);
4. ob = stringarr;
5. ob = stringarr[5];
6. floater = ob;
7. ob = floater;
```

A. 第 4 行
B. 第 5 行
C. 第 6 行
D. 第 7 行

问题 8–10 参考下方图形所示类层次结构。

8. 考虑以下代码：

```java
1. Dog rover, fido;
2. Animal anim;
```

