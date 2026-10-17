
```cpp
void MainWindow::convertFiles(const QStringList &sourceFiles) {
    stopped = false;
    updateUI();
    total = sourceFiles.count();
    done = 0;
    const QVector<int> sizes = AQP::chunkSizes(sourceFiles.count(),
        QThread::idealThreadCount());

    int offset = 0;

    foreach (const int chunkSize, sizes) {
        ConvertImageTask *convertImageTask = new ConvertImageTask(
            this, &stopped, sourceFiles.mid(offset, chunkSize),
            targetTypeComboBox->currentText());
        QThreadPool::globalInstance()->start(convertImageTask);
        offset += chunkSize;
    }
    checkIfDone();
}
```

这个版本的 `convertFiles()` 方法在结构上与我们之前看到的（252 ◀）相同。关键区别在于，对于我们要处理的每个文件块，我们都创建一个 `ConvertImageTask` 对象（`QRunnable` 子类）来执行处理。（我们传递了与传递给 `QtConcurrent::run()` 完全相同的参数来传递转换函数）。一旦 `runnable` 被创建，我们就对其调用 `QThreadPool::start()`——这会将 `runnable` 的所有权交给 Qt 的全局线程池并开始运行。

线程池会在完成后删除该 `runnable`，这正是我们想要的。我们可以通过调用 `QRunnable::setAutoDelete(false)` 来防止这种行为，在这种情况下，我们必须负责删除该 `runnable`。

```cpp
class ConvertImageTask : public QRunnable {
public:
    explicit ConvertImageTask(QObject *receiver,
        volatile bool *stopped, const QString &sourceFiles,
        const QString &targetType)
        : m_receiver(receiver), m_stopped(stopped),
        m_sourceFiles(sourceFiles),
        m_targetType(targetType.toLower()) {}

private:
    void run();
    ...
};
```

这里是 `ConvertImageTask` 的定义，除了我们省略的私有成员数据外。通过将其 `run()` 方法设为私有，我们防止该类被派生，同时也防止从实例调用 `run()`（因为 `run()` 应该只由 `QThreadPool::start()` 调用）。

```cpp
void ConvertImageTask::run() {
    foreach (const QString &source, m_sourceFiles) {
        if (*m_stopped)
            return;

        QImage image(source);
        QString target(source);
        target.chop(QFileInfo(source).suffix().length());
        target += m_targetType;
        if (m_stopped)
            return;
        bool saved = image.save(target);
        QString message = saved 
            ? QObject::tr("Saved '%1'").arg(QDir::toNativeSeparators(target))
            : QObject::tr("Failed to convert '%1'").arg(QDir::toNativeSeparators(source));
        QMetaObject::invokeMethod(m_receiver, "announceProgress",
            Qt::QueuedConnection, ARG(bool, saved),
            ARG(QString, message));
    }
}
```

该方法在结构上与我们之前看到的 `convertImages()` 函数（253）相同。唯一的区别是，我们不再使用自定义事件通信进度，而是通过调用主窗口中的槽函数来完成。

由于 `QRunnable` 不是 `QObject` 子类，因此它没有内置的信号和槽支持。一种解决方案是同时继承 `QObject` 和 `QRunnable`，但如果我们想这样做，不如直接创建一个作为 `QObject` 类的 `QThread` 子类，并定义一些常用的内置信号和槽。另一种解决方案是像上一个节那样使用自定义事件。

在这里，我们选择使用 `QMetaObject::invokeMethod()` 方法来调用槽函数。该方法接收接收者、要调用的槽名称、连接类型（对于辅助线程 `Qt::QueuedConnection` 是最好的，因为它像 `QApplication::postEvent()` 一样使用事件队列）以及要发送的参数。每个参数必须使用 Qt 的 `ARG` 宏来指定，该宏接收类型和值。`QMetaObject::invokeMethod()` 方法可以传递多达九个参数，还可以指定返回值，尽管只有在使用 `Qt::DirectConnection` 连接时使用返回值才有意义。

由于槽调用是在主（GUI）事件队列上进行的，槽的执行发生在 GUI 线程中，而不是在调用 `QMetaObject::invokeMethod()` 的辅助线程中。这对于在辅助线程中发射的信号也是如此，因为 Qt 会将信号转换为事件。

一些程序员认为使用 `QMetaObject::invokeMethod()` 比发送自定义事件更好的风格，因为它与 Qt 的信号和槽机制无缝集成，并且不需要创建自定义事件子类或重写 `QWidget` 的 `event()`。在底层，信号和槽实际上是使用 Qt 的事件机制实现的。

```cpp
void MainWindow::announceProgress(bool saved, const QString &message) {
    if (stopped)
        return;
    logEdit->appendPlainText(message);
    if (saved)
        done++;
}
```

## 线程中的过滤与映射

`QtConcurrent` 命名空间中的函数非常适用于我们大量需要以相同方式处理的数据项的情况。对于数量较少的项（例如，每个核心少于五个），我们可以为 `QtConcurrent::run()` 创建一个函数，或者使用 `QRunnable` 或 `QThread` 来处理每一个项。但当我们有大量项时——也许是成百、上千个甚至更多——为每个项创建一个线程可能会产生巨大的开销，以至于让按顺序处理数据反而更快。正如我们在上一节中看到的，一种解决方案是只创建几个线程，并让每个线程处理一组项。但在某些情况下，我们希望单独处理每个项，`QtConcurrent` 提供了支持这种操作的函数。

`QtConcurrent` 模块提供的函数分为四类：过滤（filters）、映射（mappers）、归约（reducers）——我们在本节中将涵盖这三类——以及我们在上一节介绍过的运行函数。过滤、映射和归约的用例是给它们一个待处理的项集合，然后让 Qt 分配工作并在其全局线程池的辅助线程中执行处理。

过滤和映射的概念源于函数式编程。在这种范围内，过滤器是一个高阶函数（即接受一个函数作为参数之一的函数），给定一个序列，过滤器函数会返回一个新的项序列，其中包含所有过滤器函数返回 `true` 值的项。而映射器是一个接受序列和一个映射函数的函数，它返回一个新序列，新序列中的每个项都是通过将映射函数应用于输入序列中对应的项产生的。

`QtConcurrent` 的过滤器和映射器紧密遵循函数式编程方法。因此，在 `QtConcurrent` 中，过滤器接收一个项序列和一个过滤函数，产生一个新的序列，其中仅包含原始序列中过滤函数返回 `true` 的项。这意味着结果序列可能不包含项、部分原始项或所有原始项。从概念上讲，过滤的工作原理如下：

```cpp
QList<Item> filter(QList<Item> items, FilterFunction isOK)
{
    QList<Item> results;
    foreach (Item item, items)
        if (isOK(item))
            results << item;
    return results;
}
```

尽管我们使用了 `QList`，但任何顺序容器（或通过 `begin` 和 `end` 迭代器指定的容器部分）都可以用于被过滤的项，且任何顺序容器都可以用于结果。

映射器（不要与 `QMap` 容器混淆！）接受一个项序列和一个映射函数，产生一个项数量完全相同的新序列（类型可能与原始项不同），其中原始序列中的每个项都应用了映射函数，以产生结果序列中的项。从概念上讲，映射器的工作原理如下：

```cpp
QList<Type2> mapper(QList<Type1> items, MapFunction)
{
    QList<Type2> results;
    foreach (Type1 item, items)
        results << map(item);
    return results;
}
```

在这里，`Type1` 和 `Type2` 可以是相同类型，也可以是不同类型——重要的是映射函数接受一个 `Type1` 类型的项并返回一个 `Type2` 类型的项。

归约器接受一个项序列并将其归约为单个项。例如，我们可能有一个数字序列并想要计算它们的和或平均值。`QtConcurrent` 命名空间拥有将过滤与归约以及映射与归约结合的函数。从概念上讲，它们的工作原理如下：

```cpp
// 过滤-归约
ResultType result;
foreach (Item item, items)
    if (isOK(item))
        result.merge(item);

// 映射-归约
ResultType result;
foreach (Item item, items)
    result.merge(map(item));
```

在这里我们使用 `isOK()` 作为过滤函数，使用 `map()` 作为映射函数。结果对象的 `merge()` 方法接收每个项（在映射-归约的情况下为处理后的项），并以某种方式将其合并自身。例如：

```cpp
struct ResultType
{
    ResultType() : sum(0) {}
    void merge(int item) { sum += item; }
    int sum;
};
```

如果此 `ResultType` 用于数字序列，在进行映射归约后（假设处理函数是恒等函数 `identity(int x) { return x; }`），总和可以通过 `result.sum` 获取。

当然，`QtConcurrent` 函数比这里所示的顺序处理每个项的 `for` 循环简单得多，原因在于它们在一个或多个辅助线程中执行处理，以便项可以并发处理。还需要明确的是，对于轻量级处理，开销可能毫无意义，但对于重型处理，`QtConcurrent` 函数可以提供吞吐量。

`QtConcurrent` 命名空间提供了过滤、映射和归约函数的阻塞和非阻塞（线程）版本。阻塞版本适用于现有的辅助线程内部（例如在 `QRunnable` 或 `QThread` 子类中），或者我们只需要函数行为而不关心锁的情况。在本章中我们将考虑非阻塞版本。

在编写此时，Qt 的文档表明在使用 `QtConcurrent` 函数时不需要锁定。当处理不影响其他内容的独立数据项时，这是正确的。但我们知道 Qt 没有提供锁定模型、场景或其包含的项的方法。可以通过顺序创建我们的代理项、并发处理它们并按顺序更新模型或场景来解决——当然，前提是开销被并行处理项的优势所抵消。

![](img/74b321c006b987639de42f0799cff_279_0)

|   | 31      | 32      | 33      | 34      | 35      | 37      |
|---|---------|---------|---------|---------|---------|---------|
| 36| 78231.724 | 96755.843 | 74290.502 | 72619.943 | 93846.041 | 80752.623 |
| 37| 99384.740 | 68593.237 | 82318.338 | 80004.208 | 81863.079 |         |
| 38| 79032.501 | 78231.724 | 96755.843 | 74290.502 | 72619.943 | 93846.041 |
| 39| 68032.551 | 99384.740 | 68593.237 | 82318.338 | 80004.208 | 81863.079 |
| 40| 70736.152 | 92356.146 | 79512.574 | 89217.457 | 63845.066 | 77524.031 |
| 41| 78014.567 | 73318.651 | 79812.464 | 73512.587 | 87478.461 | 80070.164 |
| 42| 92356.146 | 79512.574 | 89217.457 | 63845.066 | 77524.031 | 83478.461 |

`Number Grid` 是一个传统的窗口 `C++/Qt` 程序。它提供了一个传统的 `File` 菜单，包含 `New`、`Open...`、`Save`、`Save As...` 和 `Qt` 选项。我们不会查看其中任何一个，因为它们都是标准的。

`Edit` 菜单处理 `counts...`、`Select...`、`Apply Script` 和 `Stop`，所有都使用了 `QtConcurrent` 函数。如果用户选择计数或选择，会弹出一个对话框，用户可以通过该框设置应用的标准。对于计数，用户可以指定数值关系运算符（`<`、`<=`、`>=`、`>` 和 `≈`—表示近似相等，以及一个数值，决定是统计所有符合条件的单元格，还是仅对选中的单元格进行计数。对于选择，用户可以指定一个数值关系操作符和一个数值，这些准则将应用于网格的所有单元格。对于应用脚本，用户会看到一个对话框，可以在其中输入任意的 `JavaScript` 脚本，全局变量 `cellValue`、`cellRow` 和 `cellColumn` 是预定义的。他们可以选择将脚本应用于网格的所有单元格，或仅应用于选定的单元格。

用于执行编辑动作的槽函数为 `editCount()`、`editSelect()` 和 `editScript()`。我们将依次回顾这些槽，然后是这些槽所调用的类、方法或函数，这样我们就能构建出如何使用 `QtConcurrent` 函数的完整蓝图。尽管 `QtConcurrent` 处理的数据应该是独立的，但在一种情况下，我们使用 `QMutex` 来允许访问共享数据。在查看槽函数之前，这里是主窗口定义中数据的提取：
