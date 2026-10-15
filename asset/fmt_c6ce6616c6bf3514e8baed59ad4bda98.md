
`testPopInteger();` // 从 `intStack` 弹出

} // 结束方法 `Tests`

// 测试双精度栈的 `push` 方法

`public void testPushDouble()`

{

// 将元素推入栈

try

{

`System.out.println("\nPushing elements onto doubleStack");`

// 将元素推入 `Stack`

for ( `double element` : `doubleElements` )

`System.out.printf("%.1f ", element);` // 推入 onto `doubleStack`

} // 结束 `for`

} // 结束 `try`

catch ( `FullStackException fullException` )

{

`System.err.println();`

`fullStackException.printStackTrace();`

} // 结束 `catch FullException`

} // 结束方法 `testPushDouble`

// 测试双精度栈的 `pop` 方法

`public void testPopDouble()`

// 从栈中弹出元素

try

{

`System.out.println("\nPpopping elements from doubleStack");`

`double popValue;` // 存储从栈移除的元素

// 从 `Stack` 中移除所有元素

while (true)

{

`popValue = doubleStack.pop();` // 从 `doubleStack` 弹出

`System.out.printf("%.1f ", popValue);`

} // 结束 `while`

} // 结束 `try`

catch ( `EmptyStackException emptyStack` )

{

`System.err.println();`

`emptyStackException.printStackTrace();`

} // 结束 `catch EmptyStackException`

} // 结束方法 `testPopDouble`

图. 18.10 | 泛型类 `Stack` 测试程序。（4/4 部分）。

```
Pushing elements onto doubleStack
1.1 2.2 3.3 4.4 5.5 6.6
FullElementException: Stack is full, cannot push 6.6
at StackTest.push(StackTest.java:30)
at StackTest.testPushDouble(StackTest.java:36)
at StackTest.testStacks(StackTest.java:18)
at StackTest.main(StackTest.java:117)
Popping elements off doubleStack
5.5 4.4 3.3 2.2 2.1
EmptyStackException: Stack is empty, cannot pop
at StackTest.pop(StackTest.java:40)
at StackTest.testPopDouble(StackTest.java:58)
at StackTest.testStacks(StackTest.java:19)
atat StackTest.main(StackTest.java:117)
Pushing elements onto integerStack
1 2 3 4 5 6 7 8 9 10 11
FullElementException: Stack is full, cannot push 11
at StackTest.push(StackTest.java:30)
at StackTest.testPushInteger(StackTest.java:81)
at StackTest.testStacks(StackTest.java:20)
at StackTest.main(StackTest.java:117)
Popping elements from integerStack
10 9 8 7 6 5 4 3 2 1
EmptyStackException: Stack is empty, cannot pop
at StackTest.pop(StackTest.java:40)
at StackTest.testPopInteger(StackTest.java:103)
at StackTest.testStacks(StackTest.java:21)
at StackTest.main(StackTest.java:117)
```

图. 18.10 | 泛型类栈 测试程序。（3/4 部分）。

图. 18.10 | 泛型类栈 测试程序。（4/4 部分）。

注意，方法 `testPushDouble` 和 `testPushInteger` 中的代码在分别向 `Stack<Double>` 或 `Stack<Integer>` 推入值时几乎是相同的，而方法 `testPopDouble` 和 `testPopInteger` 中的代码在分别从 `Stack<Double>` 或 `Stack<Integer>` 弹出时也几乎是相同的。这为使用泛型方法提供了另一个机会。图 18.11 定义了泛型方法 `testPush`（26–46行用于用于与图 18.10 中 `testPushDouble` 和 `testPushInteger` 相同的任务——即将值推入 `Stack<T>`。同样，泛型方法 `testPop`（49–69行）执行与图 18.10 中 `testPopDouble` 和 `testPopInteger` 相同的任务——即从 `Stack<T>` 中弹出值。请注意，图 18.11 的输出与图 18.10 的输出一致。

```
// 图 18.11: StackTest2.java
// Stack 泛型类测试程序
public class StackTest2
{
    private Double[] doubleElements = { 1.1, 2.2, 3.3, 4.4, 5.5, 6.6 };
    Integer[] integerElements = { 2, 3, 4, 5, 6, 7, 8, 9, 10, 11 };
    private Stack<Double> doubleStack; // 存储 Double 对象
    private Stack<Integer> integerStack; // 存储 Integer 对象
    // 测试 Stack 对象
    public void testStacks()
    {
        doubleStack = new Stack<Double>( 5 ); // Double 栈
        integerStack = new Stack<Integer>( 10 ); // Integer 栈
        testPush("doubleStack", doubleStack, doubleElements);
        testPop("doubleStack", doubleStack);
        testPush("integerStack", integerStack, integerElements);
        testPop("integerStack", integerStack);
    } // 结束方法 testStacks
    // 泛型方法 testPush 将元素推入栈
    public < T > void testPush(String name, Stack< T > stack,
        T[] elements)
    {
        // 将元素推入栈
        try
        {
