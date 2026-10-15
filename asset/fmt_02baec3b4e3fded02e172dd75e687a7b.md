
`tr("发生了 %1 个错误:%n", "", errorInfo.count())`

`.arg(errors.join("\n")), "", tr("&n继续")))`

`}`

## 使用 QThread 进行多线程处理

本章介绍了 `QThread` 类，它提供了对线程的精细控制，以及对 Qt 信号槽机制的支持。与上一节一样，它假设你具备线程的基础知识，特别是 Qt 线程。本章还假设你至少阅读了上一节的开头。

如果我们有少量项目（或少量的项目组）要在后台处理，并且我们想要跟踪进度和完成情况，通常最好的解决方案是创建一个 `QThread` 子类。Qt 的 `QThread` 类（以及 `Runnable`）是基于 Java 的 `Thread` 类设计的，具有类似的整体设计——例如，要求子类重写 `run()` 方法，并通过调用 `start()` 方法启动线程执行。

`QThread` 和 `Runnable` 之间的关键区别是 `QThread` 是 `QObject` 子类，因此我们可以使用信号槽来监控进度——事实上，`QThread` 提供了一些我们可以连接的有用信号槽。图 8.1 提供了如何使用和创建多个 `QThread` 实例的示意图。

在本章中，我们将查看使用 `QThread` 的不同应用程序：一个使用辅助线程处理独立项目因此不需要锁，另一个填充共享数据结构则需要锁确保安全访问。

## 处理独立项目

在本节中，我们将审查图 8.2 所示的交叉淡应用程序（fader）。该应用程序允许用户选择两个图像，并创建用户指定数量的中间图像以产生一系列交叉淡图像。例如，如果用户选择三个交叉淡图像，他们将得到一个包含五个图像的序列，比例为（第一张图像 (100:0)，交叉淡图像 1 (75:25)，交叉淡图像 2 (50:50)，交叉淡图像 3 (25:75)，第二张图像 (0:100)）。

*(注：原始文本中关于“交叉淡的效果”的句子重复了多次，此处已仅保留核心描述：使用中间图像进行交叉淡的效果在图 8.2 的截图中所示。)*

## 处理独立项目

```cpp
void MainWindow::generateOrCancelImages({
    if (generateOrCancelButton->text() == tr("G&generate")) {
        generateOrCancelButton->setEnabled(false);
        statusBar->showMessage(tr("Generating..."));
        canceled = false;
        cleanup();
        QImage firstImage(firstLabel->text());
        QImage lastImage(lastLabel->text());
        for (int i = 0; i < numberSpinBox->value(); ++i) {
            createAndRunAcrossFader(i, firstImage, lastImage);
            generateOrCancelButton->setText(tr("Canc&el"));
        }
    } else {
        canceled = true;
        cleanup();
        generateOrCancelButton->setText(tr("G&generate"));
    }
    updateUI();
}
```

此槽函数在点击 `generateOrCancelButton` 时调用，但其行为取决于按钮是用于启动图像生成还是取消。

如果用户点击了“生成（Generate）”，我们会执行一些界面相关的操作，例如更新状态栏并将 `canceled` 设为 `false`。我们还会调用 `cleanup()` 以确保没有辅助线程在运行，并删除在进度小部件中布局的任何标签和进度条，为重新开始做准备工作。

然后，我们为用户想要的每个交叉淡化图像创建一个交叉淡化器（crossfader），并将 `generateOrCancelButton` 更改为“取消（Cancel）”按钮。

另一方面，如果用户点击了“取消（Cancel）”，我们将 `canceled` 设为 `true`，以便主窗口方法知道生成已取消。然后我们进行清理，并将按钮恢复为“生成（Generate）”按钮。

在任何情况下，最后我们都会调用 `updateUI()` 方法（未显示）；该方法简单根据用户是否选择了两个文件名来启用或禁用“生成”按钮。

如往常，键盘快捷键会自动设置，在本例中是在构造函数中创建部件后，通过调用 `AQP::accelerateWidget(this)` 设置的。但 `generateOrCancelImages` 方法依赖于获取“生成/取消”按钮所使用的文本，而我们无法确定 `AQP::accelerateWidget()` 会将取位符 `&` 放在哪里。一种解决方案是在去掉 `&` 之后比较按钮文本，例如 `generateOrCancelButton->text().replace("&","") == tr("Generate")`。但我们选择在两个文本中都手动放置 `&`，以确保按钮具有相同的快捷键（Alt+E），无论它显示的是“生成”还是“取消”。关于 `accelerate<>()` 函数的更多信息，请参阅 `alt_key.hpp` 模块或“键盘快捷键”侧栏；

现在是时候审查 `cleanup()` 方法了。该方法在生成一组新图像、生成被取消或程序终止时调用。为了方便解释，我们将该方法分为两个部分进行审查。事实上，我们将首先展示第一部分的朴素（naive）实现方式，然后讨论该方法存在的问题，接着审查一个避免了该问题的实现方案。之后我们将查看第二部分，它在两个部分中都是相同的。

`cleanup()` 方法的第一部分负责停止任何运行中的交叉淡化器。我们将从朴素版本开始：

```cpp
mainWindow::cleanup(StopState stopState)
{
    foreach (CrossFader *crossfader, crossFaders) { // 朴素实现！
        crossfader->stop();
        crossfader->wait();
        crossfader->deleteLater();
    }
    crossFaders.clear();
}
```

这是最简单的方法。我们遍历所有的 `crossFaders` 并对每一个调用 `crossfader::stop()`。这几乎不花费时间，因为方法所做的只是将布尔值设为 `true`。下次调用 `QThread::wait()`——当交叉淡化器必须停止时，遇到 `if (stopped)` 语句。`QThread::wait()` 的返回告诉我们线程已完成，因此我们让它删除自己。由于 `crossFaders` 包含了悬空指针，这种方法非常简单，我们不需要使用 `QPointer`，因为普通指针足够了。但它有一个潜在的缺点：它会轮流等待每个线程停止，因此总停止时间是所有线程停止时间之和。如果我们准备使用更复杂的算法，就可以避免这个问题，并将停止时间缩短到接近最慢线程的时间。在实际测试中，更复杂的算法相比简单方法在某些情况下上并没有明显优势。然而，如果我们使用简单方法，可能使用两个独立的循环（一个用于停止，一个用于等待和删除）会更好，这是我们在讨论复杂方法时将看到的。

## 处理独立项目

交叉淡化器的源码包含了两种实现方式，取决于 `#define`。这里是默认使用的实现的第一部分：

```cpp
const int StopWait = 100;

void MainWindow::cleanUp(StopState stopState) {
    foreach (CrossFader *crossfader, crossFaders) {
        crossfader->stop();
        while (crossFaders.count()) {
            QMutableListIterator<QPointer<CrossFader>> i(crossFaders);
            while (i.hasNext()) {
                CrossFader *crossfader = i.next();
                if (crossfader) {
                    if (crossfader->wait(StopWait)) {
                        delete crossfader;
                        i.remove();
                    }
                } else {
                    i.remove();
                }
            }
        }
    }
}
```

方法的第一件事是告诉每个交叉淡化器停止。正如之前提到的，`CrossFader::stop()` 的调用是非常快的，因为每次调用只涉及将布尔值设为 `true`。因此在该循环结束时，每个交叉淡化器都必须停止。

下一个循环是等待交叉淡化器实际停止以便删除它们。为什么要使用两个循环？因为如果我们先调用 `stop()` 然后调用 `wait()`（它是阻塞的），每个交叉淡化器将按顺序而非并发停止，总停止时间将是所有停止时间之和。我们想要实现的是总停止时间接近最慢线程的停止时间。因此我们在一个循环中告诉线程停止，在另一个循环中等待它们停止。

我们用于停止线程的算法是持续遍历所有的交叉淡化器并获取每一个。如果交叉淡化器已由于 `QPointer` 被删除，它将为空，我们可以直接从列表中移除。否则，我们什么都不做，并在下一次循环中重试。如果线程仍然存在，我们会调用 `QThread::wait()`，但这里我们只等待100毫秒。如果线程已完成，`wait()` 将返回 `true`，在这种情况下我们删除该线程。这种方法有效地给了每个线程停止所需的多个时间片。它也意味着如果某个线程耗时很长，它不会延迟我们停止其他线程。这使得整体停止时间更接近最慢线程，而不是所有停止时间之和。

在这种情况下，更复杂的算法相比简单方法优势并不大。这是因为 `UIImage::save()` 方法是阻塞的（与处理相比，磁盘访问缓慢），任何正在保存图像的线程必须等待保存完成，即使我们告诉它停止。所以，时间片划分的好处并没有我们预期的那样大。

无论我们使用哪种算法来停止线程，`cleanup()` 方法的第二部分都是相同的；现在我们审查这一部分。

```cpp
if (stopState == Terminating)
  return;
  foreach (QProgressBar *progressBar, progressBarForFilename)
    if (progressBar)
      progressBar->deleteLater();
    progressBarForFilename.clear();
  foreach (QLabel *progressLabel, progressLabels)
    if (progressLabel)
      progressLabel->deleteLater();
    progressLabels.clear();
```

一旦所有线程停止，如果应用程序正在终止，我们就完成了所有必要操作并返回。但如果清理是为了准备另一次图像生成，或者是生成取消的结果，我们还需要移除用于显示上一次生成进度的（任何）标签和进度条。

删除操作是直观的：我们遍历所有的进度条和标签，对于仍然存在的，安排它们在事件循环处理后删除自己，然后清除它们所持有的容器。如果应用程序正在终止，我们不必费忙于此，因为所有标签和进度条都在布局中——这意味着它们都有父部件，当它们的父部件（进度小部件）被删除时，Qt 会以正常方式删除它们。

在需要时创建新的进度条和进度小部件，比复用它们的效率低。但复用需要更多代码——例如，隐藏那些已创建但不再需要的（由于生成的图像比上一次少），或者创建额外的（由于生成的图像比上一次多）。而且，如果用户从

## 处理独立项目

如果需要 14 张图像，意味着我们将保留 9 个不需要的标签和进度条。通过删除它们，我们以时间为代价最小化了内存占用。这似乎是一个合理的权衡，因为创建一个淡入图像的时间可能远大于删除和创建标签及进度条的时间。

每个淡入器都是在 `generateOrAcrossFader()` 方法中调用 `createAndRunAcrossFader()` 方法创建并启动的——我们现在分两个短部分进行回顾。

```cpp
void MainWindow::createAndRunAcrossFader(int number,
    const QImage&firstImage, const QImage&lastImage)
{
    QString filename = QString("%1.png").arg(baseNameEdit->text())
        .arg(number + 1, 2, 10, QChar('0'));
    QLabel *progressLabel = new QLabel(filename);
    progressLabels << progressLabel;
    QProgressBar *progressBar = new QProgressBar();
    progressBar->setRange(0, 100);
    progressBarForFilename[filename] = progressBar;
    QLayout *layout = object_cast<QLayout*>((
        progressWidget->layout()));
    Q_ASSERT(layout);
    layout->addWidget(progressLabel, number, 0);
    layout->addWidget(progressBar, number, 1);
}
```

传入此处的数字是待创建的淡入图像的零索引。我们首先为图像创建一个合适的名称（如 `Image-01.png`，`Image-02.png` 等），使用从 1 开始的两位十进制数字，必要时在前面补 0。然后我们创建一个新标签并将其添加到标签列表中，创建一个新的进度条并将其添加到进度条映射中（使用文件名作为键）。我们获取进度部件的布局——得益于之前的 `cleanup()` 调用，该布局应该是空的——然后将标签和进度条都添加到图像编号对应的行中。

```cpp
double firstWeight = (number + 1) /
    static_cast<double>(progressSpin->value() + 1);
double secondWeight = 1.0 - firstWeight;
CrossFader *crossFader = new CrossFader(filename, firstImage,
    firstWeight, lastImage, secondWeight, this);
crossFaders << crossFader;
connect(crossFader, SIGNAL(progress(int)),
    progressBar, SLOT(setValue(int)));
connect(crossFader, SIGNAL(saving(const QString&)),
    this, SLOT(saving(const QString&)));
```

## 第 8 章 使用 QThread 进行多线程

```cpp
connect(crossFader, SIGNAL(saved(bool, const QString&)),
    this, SLOT(saved(bool, const QString&)));
connect(crossFader, SIGNAL(finished())),
    this, SLOT(finished()));
crossFader->start();
```

用户界面设置完成后，我们转向创建并启动创建淡入图像的线程。首先我们计算要使用的“权重”——例如，如果图像按 (60:40) 的比例创建，权重将为 0.6 和 0.4。创建 `CrossFader` 对象时，我们给它要保存的文件名、以及使用的图像和权重。然后我们将淡入器添加到淡入器列表中，以便后续清理。

由于 `CrossFader` 是 `QThread` 的子类（本身也是一个 `Q` 子类），我们可以利用它的信号和槽，而不需要像上一章的示例中那样创建自定义事件或手动调用槽。

在这里，我们直接将淡入器的自定义 `progress()` 信号连接到进度条，并将其他自定义信号以及 `QThread::finished()` 信号连接到相应的主窗口槽。最后，我们调用 `QThread::start(this)` 来启动线程。

```cpp
const int setTimeout = QApp::MSecPerSecond * 10;

void MainWindow::saving(const QString &filename)
{
    statusBar->showMessage(tr("正在保存 '%1'").arg(filename),
        StatusTimeout);
    if (QProgressBar *progressBar = progressForFileName[filename])
}
```
