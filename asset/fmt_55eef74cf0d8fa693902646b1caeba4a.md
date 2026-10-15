
| 操作 | 缓冲区 | 占用 |
| --- | --- | --- |
| 生产者写入 1 | 1 | true |
| 生产者尝试写入。缓冲区满。生产者等待。 | 1 | true |

**图 23.23** | 两个线程操作一个同步缓冲区。（2 部分之 1）。

| 操作 | 缓冲区 | 占用 |
| --- | --- | --- |
| 消费者读取 1 | 1 | false |
| 生产者写入 2 | 2 | true |
| 生产者尝试写入。缓冲区满。生产者等待。 | 2 | true |
| 消费者读取 2 | 2 | false |
| 生产者写入 3 | 3 | true |
| 消费者读取 3 | 3 | false |
| 生产者写入 4 | 4 | true |
| 消费者读取 4 | 4 | false |
| 消费者尝试读取。缓冲区空。消费者等待。 | 4 | false |
| 生产者写入 5 | 5 | true |
| 消费者读取 5 | 5 | false |
| 消费者尝试读取。缓冲区空。消费者等待。 | 5 | false |
| 生产者写入 6 | 6 | true |
| 消费者读取 6 | 6 | false |
| 生产者写入 7 | 7 | true |
| 消费者读取 7 | 7 | false |
| 生产者写入 8 | 8 | true |
| 消费者读取 8 | 8 | false |
| 生产者写入 9 | 9 | true |
| 消费者读取 9 | 9 | false |
| 生产者写入 10 | 10 | true |

图 23.23 | 两个线程操作一个同步缓冲区。（2 部分之 2）。

# 23.11 带 GUI 的多线程

Swing 应用为多线程编程带来了一系列独特的挑战。所有的 Swing 应用都只有一个线程，称为事件分发线程（event dispatch thread），用于处理与 GUI 组件的交互。所有需要与应用程序 GUI 交互的任务都放在事件队列中，并由事件分发线程顺序执行。

Swing GUI 组件不是线程安全的——它们不能被多个线程操作，否则会有产生错误结果的。与本章中的其他示例不同，GUI 应用中的线程安全性不是通过同步操作来实现，而是通过确保从单个线程（即事件分发线程）访问 Swing 组件来实现。这种技术被称为线程限制（thread confinement）。

通常，在事件分发线程上顺序执行 Swing 组件操作的同时进行简单的计算就足够了。如果应用程序需要响应用户界面交互而执行耗时计算，那么当该线程正在计算时，事件分发线程无法处理事件队列中的其他任务。这会导致 GUI 组件变得无响应。较好的是在单独线程中处理耗时计算，释放事件分发线程以继续其他 GUI 交互。当然，为了根据计算结果更新 GUI，你必须从事件分发线程更新 GUI，而不是从执行计算的工作线程。

## SwingWorker 类

Java SE 6 提供了 `SwingWorker` 类（位于 `javax.swing` 包中），用于在工作线程中执行耗时计算，并根据结果从事件分发线程更新 Swing 组件。`SwingWorker` 实现了 `Runnable` 接口，这意味着 `SwingWorker` 对象可以被调度在单独线程中执行。`SwingWorker` 类提供了几个方法，以简化在工作线程中执行计算并将结果提供供 GUI 显示的过程。一些 `SwingWorker` 方法如图 23.24 所示。

图 23.24 | 常用的 `SwingWorker` 方法。

### 23.11 带 GUI 的多线程 1083

#### 23.11.1 在工作线程中执行计算

在下一个示例中，GUI 提供了组件，允许用户输入数字 `$n$` 并获取第 `$n$` 个 斐波那契数，我们使用第 15.4 节讨论的递归算法进行计算。由于递归算法对于较大的值非常耗时，我们使用一个 `SwingWorker` 对象在工作线程中执行计算。GUI 还提供了另一组组件，每点击一次按钮，就会获取序列中的下一个斐波那契数，从 `beforeEach(1)` 开始。这组组件直接在事件分发线程中执行短时间计算。

`BackgroundCalculator` 类（图 23.25）在工作线程中执行递归斐波那计算。该类继承自 `SwingWorker`（第 8 行），重写了 `doInBackground` 和 `done` 方法。`doInBackground` 方法（第 21–25 行）在工作线程中计算第 `$n$` 个 斐波那契数并返回结果。`done` 方法（第 28–34 行）将结果显示在 `JLabel` 中。

```java
// BackgroundCalculator.java

// SwingWorker 类用于在后台线程中计算斐波那契数。

import javax.swing.SwingWorker;

import javax.swing.JLabel;

import java.util.concurrent.ExecutionException;

public class BackgroundCalculator extends SwingWorker<String, Object> {

    private final int n; // 要计算的斐波那契数

    private final JLabel resultJLabel; // 显示结果的 JLabel

    // 构造函数

    public BackgroundCalculator(int number, JLabel label) {

        n = number;

        resultJLabel = label;

    } // end BackgroundCalculator构造函数

    // 在工作线程中运行的长时代码

    public String doInBackground() {

        long nthFib = fibonacci(n);

        return String.valueOf(nthFib);

    } // end method doInBackground

    // 完成后在事件分发线程上运行的代码

    protected void done() {

        try {

            // 获取 doInBackground 的结果并显示

            resultJLabel.setText(get());

        } catch (InterruptedException ex) {

            resultJLabel.setText("等待结果时被中断.");

        } // end catch

        catch (ExecutionException ex) {

            resultJLabel.setText("执行计算时遇到错误.");

        } // end catch

    } // end method done

    // 递归方法 fibonacci；计算第 n 个斐波那契数

    public long fibonacci(long number) {

        if (number == 0 || number == 1)

            return number;

        else

            return fibonacci(number - 1) + fibonacci(number - 2);

    } // end method

} // class BackgroundCalculator
```
