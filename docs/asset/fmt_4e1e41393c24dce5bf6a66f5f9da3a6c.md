
| 方法签名 (signature of a method) |  |
| 模拟 (simulation) |  |
| 软件重用 (software reuse) |  |
| 栈 (stack) |  |
| 栈帧 (stack frame) |  |
| 栈溢出 (stack overflow) |  |
| 字符串拼接 (string concatenation) |  |

## 自测练习题

- 6.1 为下列陈述填空：

a) 方法通过 a(n) _________ 调用。

b) 仅在声明它的方法内部的变量被称为 a(n) __________。

c) 被调用方法中的 __________ 语句可将异常值传回调用方法。

d) 关键字 __________ 表示该方法不返回结果。

e) 数据可以从栈的 __________ 中添加或删除。

f) 栈被称为数据结构——最后推入（插入）到栈顶的项是第一个从栈中弹出（移除）的项。

g) 从方法返回控制权给调用者的三种方法是 __________, ________ 和 ________。

h) __________ 类的对象产生随机数。

i) 程序执行栈包含了每次方法调用的局部变量。这些存储作为程序执行栈一部分的数据被称为方法调用的 __________ 或 __________。

j) 如果程序执行栈上可以调用的方法多于，则会发生 a(n) __________。

k) 声明的 __________ 是可以引用声明中实体的部分。

## 自测练习

- 1) 在 Java 中，可能存在多个同名的方法来处理不同类型的数据。这种特征被称为方法重载。程序执行栈也被称为栈。图 6.9 所示 `Craps` 类的实体实体：

a) 变量 `Numbers`

b) 变量 `die`

c) 方法 `roll`

d) 方法 `play`

2 编写一个测试 6.2 所示 `Math` 类示例的应用程序。

3 给下列方法的头部：

a) `hypotenuse`，接受双精度浮点数。

b) `smallest`，接受三个整数 `x`, `y` 和 `z`。

c) 不接受任何参数并返回整数。

d) 接受一个整数参数并返回浮点结果。

4 找出下列程序段中的错误。解释如何修复：

a) 
```java
int g() {
    System.out.println("Inside method g");
}
```

b) 
```java
int sum(int x, int y) {
    int result;
    result = x + y;
}
```

c) 
```java
int h() {
    System.out.println("Inside method h");
}
```

d) 
```java
void f(float a) {
    float a;
    System.out.println(a);
}
```

e) 
```java
void product() {
    int a = 6, b = 5, c = 4, result;
    result = a * b * c;
    System.out.printf("Result is %d\n", result);
}
```

5 编写一个完整的 Java 应用程序打印球的半径，并调用方法计算并显示体积。使用以下语句：`double volume = (4.0 / 3.0) * Math.pow(radius...`

## 第6章 方法：深入观察

## 自测练习答案

6.1 a) 方法调用。b) 局部变量。c) `return`。d) `void`。e) 栈。f) `(LIFO)`。g) `return`, `return` 和 `exception`。h) `Random`。i) 栈或调用。j) 栈溢出。k) 作用域。l) 方法重载。m) 方法调用。

6.2 a) 类体。b) 定义 `roll` 的体。c) 类体。d) 类体。e) 定义 `play()` 的体。

6.3 下列代码演示了 6.2 中的数学方法：

```java
// Exercise 6.3 MathTest.java
// Testing the Math methods.
public class MathTest {
    public static void main(String[] args) {
        System.out.printf("Math.abs( 23.7 ) = %f\n", Math.abs(23.7 }));
        System.out.printf("Math.abs( 0.0 ) = %f\n", Math.abs(0.0 }));
        System.out.printf("Math.abs( -23.7 ) = %f\n", Math.abs(-23.7 }));
        System.out.printf("Math.ceil( 9.2 ) = %f\n", Math.ceil(9.2 }));
        System.out.printf("Math.ceil( -9.8 ) = %f\n", Math.ceil(-9.8)));
        System.out.printf("Math.cos( 0.0 ) = %f\n", Math.cos(0.0 }));
        System.out.printf("Math.exp( 1.0 ) = %f\n", Math.exp(1.0 }));
        System.out.printf("Math.exp( 2.0 ) = %f\n", Math.exp(2.0 }));
        System.out.printf("Math.floor( 9.2 ) = %f\n", Math.floor(9.2 }));
        System.out.printf("Math.floor( -9.8 ) = %f\n", Math.floor(-9.8)));
        System.out.printf("Math.log( Math.E ) = %f\n", Math.log(Math.E }));
        System.out.printf("Math.log( Math.E * Math.E ) = %f\n", Math.log(Math.E * Math.E }));
        System.out.printf("Math.max( 2.3, 12.7 ) = %f\n", Math.max(2.3, 12.7 }));
        System.out.printf("Math.max( -2.3, -12.7 ) = %f\n", Math.max(-2.3, -12.7 }));
        System.out.printf("Math.min( 2.3, 12.7 ) = %f\n", Math.min(2.3, 12.7 }));
        System.out.printf("Math.min( -2.3, -12.7 ) = %f\n", Math.min(-2.3, -12.7 }));
        System.out.printf("Math.pow( 2.0, 7.0 ) = %f\n", Math.pow(2.0, 7.0 }));
        System.out.printf("Math.pow( 9.0, 0.5 ) = %f\n", Math.pow(9.0, 0.5)));
    } // end main
} // end class MathTest
```

```
Math.abs(23.7) = 23.700000
Math.abs(0.0) = 0.000000
Math.abs(-23.7) = 23.700000
Math.ceil(9.2) = 10.000000
Math.ceil(-9.8) = -9.000000
Math.exp(0.0) = 1.000000
Math.exp(2.0) = 7.389056
Math.floor(9.2) = 9.000000
Math.floor(-9.8) = -10.000000
Math.log(Math.E) = 1.000000
Math.log(Math.E * Math.E) = 2.000000
Math.max(2.3, 2.7) = 2.700000
Math.max(-2.3, -12.7) = -2.300000
Math.min(2.3, 12.7) = 2.300000
Math.min(-2.3, -12.7) = -12.700000
Math.pow(2.0, 7.0) = 128.000000
Math.pow(9.0, 0.5) = 3.000000
Math.sin(0.0) = 0.000000
Math.sqrt(900.0) = 30.000000
Math.sqrt(9.0) = 3.000000
Math.tan(0.0) = 0.000000
```

- 6.4 a) `double hypotenuse(double side1, double side2)`

- b) `int smallest(int x, int y, int z)`

- c) `void instructions()`
