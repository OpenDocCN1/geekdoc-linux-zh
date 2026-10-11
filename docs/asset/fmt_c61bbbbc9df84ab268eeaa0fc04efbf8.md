
使用枚举常量（如 `Status.WON`、`Status.LOST` 和 `Status.CONTINUE`）而不是字面值（如0、1和2）可以使程序更容易阅读和维护。`play` 方法中的第26行调用了 `rollDice`，它从1到6中选取两个随机值，显示第一个骰子的值、第二个骰子的值以及骰子的总和，然后进入第29–45行的下一个 `switch` 语句，该语句使用第26行的 `sumDice` 来判断游戏是获胜还是失败，或者是否应该继续下一次投掷。在第一次投掷中导致胜利或失败的骰子总和在第14–18行中声明为 `public int int`。它们被用于 `switch` 语句的各种。标识符名称使用了这些总和的缩写。注意这些常量与枚举常量一样，按照惯例用全大字母声明，以便在程序中醒目。第31–34行确定玩家是否在第一次投掷时通过 `SEVEN` (7) 或 `SNAKE_EYES` (12)、`TREY` (3) 获胜（注：原文此处SNAKE_EYES对应12可能为逻辑描述笔误，通常SNAKE_EYES为2）。

## 第6章 方法：深入探讨

任何代码块都可以包含变量声明。如果方法中的局部变量或参数与字段同名，则该字段会被“隐藏”，直到该代码块执行结束——这被称为遮蔽（shadowing）。在第8章中，我们将讨论如何访问被遮蔽的字段。

### 常见编程错误6.10

当在方法中重复声明局部变量时，会发生编译错误。

### 预防技巧6.3

为字段和局部变量使用不同的名称，以防止在调用方法时由于方法局部变量遮蔽了类中同名字段而导致的微妙逻辑错误。

图6.11和图6.12中的应用演示了字段和局部变量的作用域问题。当应用启动时，`ScopeTest`类的`main`方法（图6.12，第7–11行）创建一个`Scope`对象（第9行），并调用对象的`begin`方法（第10行）来产生程序的输出（如图6.12所示）。

```java
// Scope.java
// Scope 展示了字段和局部变量的作用域
public class Scope {
    // 字段对该类的所有方法可见
    private int x = 1;

    // begin 创建并初始化局部变量
    public void begin() {
        int x = 5; // 方法局部变量遮蔽了字段 x
        System.out.printf("local in method begin is %d\n", x);
        useLocalVariable(); // useLocalVariable 拥有局部 x
        useField(); // useField 使用 Scope 的字段
        useLocalVariable(); // useLocalVariable 重新初始化局部 x
        useField(); // 类 Scope 的字段保留了其值
    } 

    public void useLocalVariable() {
        int x = 25; // 每次调用 useLocalVariable 时都初始化
        System.out.printf("local x on entering methodLocalVariable is %d\n", x);
        x++; // 修改此方法的局部变量
        System.out.printf("local x before exiting methodLocalVariable is %d\n", x);
    } // end methodLocalVariable

    // 在每次调用时修改类 Scope 的字段
    public void useField() {
        x = 10; // 修改类 Scope 的字段
        System.out.printf("field x on entering methodField is %d\n", x);
        System.out.printf("field x before exiting methodField is %d\n", x);
    } // end methodField
} // end class Scope
```

**图6.11** | 展示字段和局部变量的 `Scope`。（部分1）

在 `Scope` 类中，第7行声明并初始化了字段 `x` 为1。在任何声明了名为 `x` 的局部变量的代码块（或方法）中，该字段都会被遮蔽（隐藏）。`begin` 方法（第11–23行）声明了局部变量 `x`（第13行）并将其初始化为5。输出该局部变量的值是为了显示字段 `x`（值为1）在 `begin` 方法中被遮蔽了。程序声明了另外两个方法——`useLocalVariable`（第26–35行）和 `useField`（第38–45行），它们不接受参数也不返回结果。`begin` 方法调用了每个方法两次（第17–20行）。当第一次调用 `useLocalVariable` 时（第17行），它创建了局部变量 `x`（第28行），并将其初始化为25（第28行），输出 `x` 的值（第30–31行），增加 `x`（第32行）并输出 `x` 的值（第33–34行）。当第二次调用 `useLocalVariable` 时（第19行），它重新创建了局部变量 `x` 并重新将其初始化为25，因此每次使用局部变量调用的输出都是相同的。

`useField` 没有声明任何局部变量。因此，如果它引用了 `x`，则使用的是类的字段（第7行）。当第一次调用 `useField` 方法时（第18行），它输出字段的值（1）（第40–41行），将字段乘以10（第42行），并在返回前输出字段的值（10）（第43–44行）。当在 `begin` 方法中下调用 `useField` 方法时（第20行），字段已经是其修改后的值10，因此该方法输出10，然后是100。最后，在 `begin` 方法中，程序再次输出局部变量 `x` 的值（第22行），以证明任何方法调用都没有改变 `begin` 的局部变量 `x`，因为这些方法引用的是其他作用域中名为 `x` 的变量。

## 6.2 方法重载

同一个类中可以声明同名的方法，只要它们的参数集不同。

```java
// Fig. 6.12: ScopeTest.java
// 测试类 Scope 的应用程序。
public class ScopeTest {
    // 应用启动点
    public static void main(String[] args) {
        Scope testScope = new Scope();
        testScope.begin();
    } // end main
} // end class ScopeTest
```

local x in method begin is 5

local x on entering methodLocalVariable is 25

local x before exiting methodLocalVariable is 25

field x on entering methodField is 1

field x before exiting methodField is 10

local x on entering methodLocalVariable is 25

local x before exiting methodLocalVariable is 25

field x on entering methodField is 10

field x before exiting methodField is 100

local x in method begin is 5

**图6.12** | 测试类 `Scope` 的应用程序。（部分2）

## 266 第6章 方法：深入观察

在图6.13中，第9行调用了方法 `square` 并传入参数7。字面量整数值被视为 `int`，因此第9行的方法调用了第14–19行的 `square` 版本，该版本指定了一个 `int` 参数。同样，第10行传入参数7.5调用了方法 `square`。字面量浮点值被视为 `double`，因此第10行调用了第22–27行的 `square` 版本，该版本指定了一个 `double` 参数。每个方法首先输出一行文本，以证明在种情况下都调用了正确的方法。注意，第10行和24行中的值使用格式指定符 `%f` 显示，而我们在两种情况下都没有指定指定符。默认情况下，如果未在格式指定符中指定精度，浮点值将以六位有效数字显示。

## 区分重载方法
