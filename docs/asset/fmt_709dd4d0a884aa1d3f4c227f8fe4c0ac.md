
``` 
1: #include <application.h>
2: #include <widget.h>
3: #include <qdialog.h>
4: #include <qfont.h>
5:
6: class MainWindow : public QWidget
7: {
8: public:
9:     MainWindow();
10: private:
11:     QFontDialog *fdialog;
12:     QFont myFont;
13: };
14:
15: MainWindow::MainWindow()
16: {
17:     setGeometry(100, 100, 200, 50);
18:
19:     // 如果选了字体，ok 将为 TRUE
20:     bool ok;
21:
22:     // 选择一个字体并将其存储在
23:     //myFont 以供使用：
24:
25:     myFont = fdialog->getFont(&ok);
26:
27: int main(int argc, char **argv)
28: {
29:     QApplication a(argc, argv);
30:     MainWindow w;
31:     a.setWidget(&w);
32:     w.show();
33:
34:     return a.exec();
35: }
```

在第 11 行和 12 行，为 `QFontDialog` 和 `QFont` 分配了内存。在第 21 行，创建一个布尔变量。该变量在第 25 行被使用，此时调用 `QFontDialog::getFont()` 来弹出字体对话框。在第 25 行，选中的字体也存储在 `myFont` 对象中。字体对话框如图 10.3 所示。

确定用户是否选择了字体，使用布尔变量（如列表 10.3 所示），并将该变量的内存地址传递给 `QFontDialog::getFont()` 函数。在这种情况下，如果用户选择了新字体，该变量为 `TRUE`，如果点击取消按钮则 `FALSE`。

```
if( ok == TRUE )
{
  // 选了新字体，
  // 我们可以继续了。
}
if( ok == FALSE )
{
  // 用户点击了取消
  // 按钮，最好中止。
}
```

如果用户选择了新字体，你就在 `myFont` 中拥有该字体，并将其用于任何地方。例如在 `QLabel` 对象中定义字体。

### 图 10.3

Qt 提供的字体对话框。

| 字体 | 字体样式 | 大小 |
|---|---|---|
| Color [下划线] | Normal | 36 |
| Color [粗体] | Bold | 15 |
| Arial | Normal | 20 |
| Arial | Bold | 22 |
| Amsterdam | Bold | 24 |
| Amsterdam | Bold Italic | 18 |
| Back | Bold | 18 |
| Courier [斜体] | Normal | 10 |

![](img/ed4f2be9f0799d95b6f041531c9a1f14_186_0.png)

## 使用消息框

由 `QMessageBox` 类提供的消息框是预定义对话框中最简单的。它可以显示简短信息（如前面的节所示）或询问用户是否想要继续。消息框可以显示图标和最多三个按钮。列表 10.4 提供了一个示例。

### 列表 10.4 消息框

```
1: #include <qapplication.h>
2: #include <QtWidgets.h>
3: #include <qmessagebox.h>
4:
5: class MyMainWindow : public QWidget
6: {
7:   public:
8:     MyMainWindow();
9:   private:
10:      QMessageBox *mbox;
11: };
12: 
13: MyMainWindow::MyMainWindow()
14: {
15:     setMessageBox(100, 100, 200, 50), "继续?", "你想要继续吗？",
16:     mbox = new QMessageBox;
17:     QMessageBox::Critical,
18:     QMessageBox::Ok | QMessageBox::Default,
19:     QMessageBox::Cancel | QMessageBox::Escape,
20:     0);
21:     mbox->show();
22: }
23: 
24: void main(int argc, char **argv)
25: {
26:     QApplication a(argc, argv);
27:     MyMainWindow w;
28:     a.setWidget(&w);
29:     w.show();
30:     a.exec();
31: }
```

`QMessageBox` 构造函数用于创建消息框（第 16 至 20 行）。在第 21 行，调用了 `QMessageBox::show()`，这导致消息框出现在屏幕上。如你所见，向构造函数传递了许多参数。第一个参数（第 16 行）代表显示在窗口顶部的字符串（也称为窗口标题）。第二个参数（第 16 行）是显示在消息框中的文本字符串（实际消息）。第三个参数（第 17 行）是你想在消息框中显示的图标。这里有四种选择：

* `QMessageBox::NoIcon` 不显示任何图标。
* `QMessageBox::Information` 显示信息图标。
* `QMessageBox::Warning` 显示适用于警告消息的图标。
* `QMessageBox::Critical` 当你想显示某些关键信息或想让用户做出关键选择时使用。

## 理解 Qt 对话框

在本例中，使用了 `QMessageBox::Critical` 图标（第 17 行）。第四个参数（第 18 行）定义了第一个图标。在本例中，使用了 `QMessageBox::Ok` 图标。它与 `QMessageBox::Default` 结合使用使其成为默认图标（如果用户按下 Enter 或 Return 键，它将被“点击”）。第五个参数（第 19 行）定义了第二个按钮。在本例中，选择了 Cancel（取消）按钮。该按钮也与 `QMessageBox::Escape` 关联。通过这种方式，如果用户按下 Escape 键，该按钮将被“点击”。

- 你完全不需要与任何带有 `QMessageBox::Default` 或 `QMessageBox::Escape` 的按钮结合使用。

最后一个参数定义了第三个按钮。然而，此示例只使用了两个按钮，因此输入了 `0`。此代码的结果如图 10.4 所示。

图 10.4

一个带有两个按钮、一个短问题和一个图标的消息框。

![](img/ed4f2be9f0799d95b6f041531c9a1f14_188_0.png)

一旦你有了 OK 和 Cancel 按钮你有更多选择。其他选择包括 `QMessageBox::Yes`、`QMessageBox::No`、`QMessageBox::Abort`、`QMessageBox::Retry` 和 `QMessageBox::Ignore`。

## 使用进度对话框

进度对话框用于告知用户应用程序当前的状态（类似于进度条）。进度对话框与进度条的区别在于，进度对话框可以与用户交互（也就是说，用户如果他们可以取消当前任务）。示例参见列表 10.5。

### 列表 10.5 进度对话框

```
1: #include <application.h>
2: #include <qwidget.h>
3: #include <qprogressbar.h>
4:
5: class MyMainWindow : public QWidget
6: {
```

### 列表 10.5 继续

```
7: public:
8:   MyMainWindow();
9:   private:
10:    QProgressDialog *pialog;
11: };
12:
13:  MyMainWindow::MyMainWindow()
14:  {
15:     setGeometry(100, 100, 200, 50);
16:
17:     pialog = new QProgressDialog("Doing something...",
18:                             "Abort Operation", 100,
19:                             this, "pialog", TRUE);
20:
21:     pialog->show();
22:
23:     int x = 0;
24:     int i = 0;
25:     while (x <= 100)
26:     {
27:         for (i = 0; i < 1000000; i++)
28:             pialog->setProgress(x);
29:             x++;
30:     }
31: }
32: void main(int argc, char *argv)
33:  {
34:   Application a(argc, argv);
35:   MyMainWindow w;
36:   a.setWidget(&w);
37:   w.show();
38:   return a.exec();
39: }
```

总共有六个参数传递给 `QProgressDialog` 构造函数行（第 17、18 和 19 行）。第一个参数（17 行）代表进度对话框顶部的文本（不是标题）。第二个参数（第 18 行）代表“取消”按钮上的文本。第三个参数（第 18 行）是总步数。在本例中，当调用 `QProgressDialog::setProgress(100)` 时，进度条将达到 100%。最后三个参数具有预定义值，实际上可以留空。然而，如果你想让进度对话框在运行时重绘，你需要将第六个参数设置为 `TRUE`，而为了这样做，还需要定义第四和第五个参数。如果你不将第六个参数设置为 `TRUE`，取消按钮的标签将永远不可见。

为了展示如何使用进度对话框，我创建了一个循环，每次都调用 `setProgress()` 并传入一个较大的值。这绝对不是你所说的真实生活示例。然而，它确实展示了它是如何工作的（见图 10.5）。

图 10.5

![](img/ed4f2be9f0799d95b6f041531c9a1f14_190_0.png)

在这里，进度条处于激活状态，目前处于 57%。

# 创建自定义对话框

当预定义的对话框不能满足你的需求时，你需要创建自定义对话框——专门为满足你的需求而设计的对话框。Qt 提供了了一些类来简化对话框的创建：`QDialog`（所有对话框的基类）和 `QDialog`（用于创建标签页对话框）。

## 使用 QDialog 创建自定义对话框

`QDialog` 是基类——所有其他对话框类都基于它。它提供了几个用于创建对话框的基本函数。

在创建对话框时，你有两种类型可选：模态对话框（modal dialogs）和非模态对话框（modeless dialogs）。模态对话框会启动自己的循环，通过这种方式阻塞程序的其余部分，直到对话框关闭。相反，非模态对话框不会阻塞程序的其余部分。通过向构造函数传递一个布尔值来控制对话框是模态的还是非模态的：传递 `true` 表示模态，传递 `false` 表示非模态。

现在我们来看与 `QDialog` 工作的几个函数。`QDialog::setWindowTitle()` 用于设置对话框的标题。`accept()`、`reject()` 和 `done()` 函数会关闭对话框并返回。`accept()` 返回 `1`，`reject()` 返回 `0`。你可以通过向 `done()` 传递一个整数来定义返回值。事实上，你可以使用 `done(1)` 和 `done(0)` 代替 `accept()` 和 `reject()` 以获得相同的结果。`QDialog` 的另一个特性是你不需要使用 `setGeometry()` 或 `resize()` 来调整窗口大小，只需放置控件它会自动适应。

```
1: #include <qapplication.h>
2: #include <dialog.h>
3: #include <QLabel.h>
4: #include <qbutton.h>
5:
6: class Question : QDialog
7: {
8: public:
9:   Question();
10:  private:
11:   QLabel *label;
12:   QPushButton *big;
13:   QPushButton *small;
14: };
15:
16: Question::Question()
17: : QDialog(0, 0, TRUE)
18: {
19:   label = new QLabel("Do you want to see a big or small?", this);
20:   label->setGeometry(10, 10, 300, 100);
21:   label->setAlignment(Qt::AlignCenter);
22:
23:   big = new QPushButton("BIG!", this);
24:   big->setGeometry(50, 120, 90, 30);
25:   connect(big, SIGNAL(clicked()), this, SLOT(accept()));
26:
27:   small = new QPushButton("small!", this);
28:   small->setGeometry(180, 120, 90, 30);
29:   connect(small, SIGNAL(clicked()), this, SLOT(reject()));
30: }
```

列表 10.6 使用 QDialog 创建自定义对话框

```
1: #include <qapplication.h>
2: #include <dialog.h>
3: #include <QLabel.h>
4: #include <qbutton.h>
5:
6: class Question : QDialog
7: {
8: public:
9:   Question();
10:  private:
11:   QLabel *label;
12:   QPushButton *big;
13:   QPushButton *small;
14: };
15:
16: Question::Question()
17: : QDialog(0, 0, TRUE)
18: {
19:   label = new QLabel("Do you want to see a big or small?", this);
20:   label->setGeometry(10, 10, 300, 100);
21:   label->setAlignment(Qt::AlignCenter);
22:
23:   big = new QPushButton("BIG!", this);
24:   big->setGeometry(50, 120, 90, 30);
25:   connect(big, SIGNAL(clicked()), this, SLOT(accept()));
26:
27:   small = new QPushButton("small!", this);
28:   small->setGeometry(180, 120, 90, 30);
29:   connect(small, SIGNAL(clicked()), this, SLOT(reject()));
30: }
```

## 图 10.6

由列表 10.6 中的 `Question` 类创建的对话框。

![](img/ed4f2be9f0799d95b6f041531c9a1f14_193_0.png)

现在，如果你点击“BIG!”按钮，将会出现一个较大的窗口。另一方面，如果你点击“small!”按钮，将会出现一个小窗口。这些窗口分别在图 10.7 和图 10.8 中。

## 图 10.7

点击 BIG! 按钮时出现的窗口。

![](img/ed4f2be9f0799d95b6f041531c9a1f14_193_1.png)

## 图 10.8

点击 small! 按钮时出现的窗口。

![](img/ed4f2be9f0799d95b6f041531c9a1f14_193_2.png)

你现在应该对如何使用 `QDialog` 有了很好的理解。列表 10.6 中的示例也可以用 `QMessageBox` 创建。但是，既然你已经知道了如何使用 `QDialog`，你会发现创建适合你特定需求的对话框变得简单了。然而，你应该尽可能地使用预定义的对话框来节省时间工作工作。但当那些对话框无法满足你的需求时，你就必须使用 `QDialog` 自己来完成。

## 理解 Qt 对话框

## 使用标签对话框

你可以用于创建自定义对话框的另一个 Qt 类是 `QtDialog`。通过它，你可以创建所谓的标签对话框（tab dialog）。标签对话框是由多个页面组成的部件。你可能在很多应用程序中见过这种对话框。当你有很多部件并且觉得把它们放在一个页面上会很混乱时，使用标签对话框是很好的。通过使用标签对话框，你可以将它们分成类别，为每个类别在标签对话框中创建一个页面。这会让你的应用程序看起来更整洁、更容易遵循。

列表 10.7 展示了标签对话框在原始状态下（未添加任何标签时）的样子。
