
## 了解 Qt Widgets：第三节课

```cpp
public:
    MyMainWindow();
private:
    QListView *listview;
    QListViewItem *topic1;
    QListViewItem *topic2;
    QListViewItem *topic3;
    QListViewItem *item;
};

MyMainWindow::MyMainWindow()
{
    setGeometry(100, 100, 300, 300);

    // 创建列表视图：
    listview = new QListView(this);
    listview->setGeometry(0, 0, 400, 0);
    // 让下箭头可见：
    listview->setRootDecorated(true);
    // 添加三列：
    listview->addColumn("Book");
    listview->addColumn("Sold Copies");
    listview->addColumn("Price");

    // 添加三个项目：
    topic1 = new QListViewItem(listview, "Topic 1");
    topic2 = new QListViewItem(listview, "Topic 2");
    topic3 = new QListViewItem(listview, "Topic 3");

    // 为每个项目添加三个子项目：
    item = new QListViewItem(topic1, "Book 1", "21,000", "$29.99");
    item = new QListViewItem(topic1, "Book 2", "19,000", "$24.99");
    item = new QListViewItem(topic1, "Book 3", "14,000", "$39.99");

    item = new QListViewItem(topic2, "Book 4", "38,000", "$34.99");
    item = new QListViewItem(topic2, "Book 5", "16,000", "$19.99");
    item = new QListViewItem(topic2, "Book 6", "9,000", "$29.99");

    item = new QListViewItem(topic3, "Book 7", "32,000", "$39.99");
    item = new QListViewItem(topic3, "Book 8", "25,000", "$37.99");
    item = new QListViewItem(topic3, "Book 9", "13,000", "$44.99");
}

void main(int argc, char **argv)
{
    QApplication a(argc, argv);
    MyMainWindow w;
    a.setWidget(&w);
    w.show();
    return a.exec();
}
```

## 第8 小时

添加项目的过程与创建菜单的过程非常相似。首先，在第 22 到 29 行创建了实际的列表视图。第 25 行调用 `QListView::setRootIsDecorated(TRUE)` 确保顶层项目左侧的箭头可见，这样用户可以显示子项目。然后，在第 27、28 和 29 行，使用 `QListView::addColumn()` 创建了三列。该函数的参数代表列名。在第 32、33 和 34 行，创建了三个顶层项目。这是通过 `QListWidgetItem` 类实现的。`QListWidgetItem` 构造函数接受三个参数；第一个是应该插入这些项目的 `QListWidgetItem` 对象。第二个参数代表项目名称。在第 37 到 43 行，向每个 `QListWidgetItem` 构造函数中添加了子项目。这两个参数代表子项目的第二列和第三列。该程序的运行如图 8.3 所示。

图 8.3

一个按主题排序的几本书的列表视图。

| 标题 | 销量 | 价格 |
|---|---|---|
| 书 1 | 21,800 | $23.99 |
| 书 2 | 19,500 | $34.99 |
| 书 3 | 14,000 | $39.99 |
| 书 4 | 36,000 | $34.99 |
| 书 5 | 16,900 | $15.99 |
| 书 6 | 5,000 | $39.99 |
| 书 7 | 32,000 | $53.99 |
| 书 8 | 25,000 | $37.99 |
| 书 9 | 13,000 | $44.99 |

> 注意，不需要调用 `insertItem()` 或类似的函数。相反，它依赖父子层级。如果你点击其中一个列标题，列表将进行排序。

`QListView` 提供了许多在前示例中未使用的其他函数。其中一些在表 8.1 中描述。为了完全控制并利用 `QListView` 类，你需要学习如何使用它们。虽然你可能在每个项目中都不需要所有它们，但了解你有哪些选项是有好的。

### 表 8.1 有用的 QListView 成员函数

| 函数 | 描述 |
|---|---|
| `setColumnCount()` | 此方法确定是否应该设置列宽。它接受两个参数：第一个是表示列的整数，第二个是可以设置为 Maximum 或 Minimum 的枚举值。 |

*(注：此处原文描述似乎与函数名不符，已按字面翻译)*

*(注：由于原文文本中存在函数名与描述的错位或逻辑混乱，翻译严格遵循了原文的对应结构)*

[注：由于提供的原文文本在表 8.1 部分部分内容存在错位（描述与函数名不匹配），以下翻译基于原文文本的对应关系：]

| `setColumnCount()` | 此方法确定是否应该设置列宽。它接受两个参数：第一个是表示列的整数，第二个是可以设置为 Maximum 或 Minimum 的枚举值。 |
| (此处省略) |  |
| `itemAt()` | 此函数接受一个 `QObject` 指针。它返回该位置的项目。 |
| `firstChild()` | 返回列表视图中的第一个项目。 |
| `itemBelow()` | 返回项目下方的项目。 |
| `itemAbove()` | 此函数决定是否选中项目。它接受两个参数：第一个是 `QListViewItem` 指针，第二个是布尔值（`TRUE` 或 `FALSE`）。使其选中。 |
| `setCurrentItem()` | 给指定的项目设置键盘焦点。 |
| `currentItem()` | 返回当前选中项目的指针。 |
| `selectionChanged()` | 当选择改变时发出的信号（即，当你选择了另一个项目或取消选择当前项目）。它还会发送新选中项目的指针。 |
| `currentChanged()` | 当当前项目改变时发出的信号。它发送新项目的指针。 |

### 表 8.1 续

| 函数 | 描述 |
|---|---|
| `doubleClicked()` | 当用户双击项目时发出的信号。它包含了双击的 `QListViewItem` 指针。 |
| `returnPressed()` | 当用户按下 Enter 或回车键时发出的信号。它还会发送具有焦点的项目。 |
| `rightButtonClicked()` | 当释放鼠标右键（在按下后）时发出的信号。此信号会向槽发送三个参数：项目指针（可以为空）、点击坐标以及代表影响列的整数值。 |

学习了这个表后，你可能想知道当前项目和选中项目之间的区别。当前项目一次只有一个；即具有焦点的项目。然而，如果你通过调用 `setMultiSelection(TRUE)` 开启了多选，你可以同时选择多个项目。在这种情况下，当前项目是选中项目中的一个，而某个特定的选中项目可以是当前项目，但也可以仅仅是选中项目。

现在，我们将看到一个进一步开发列表 8.2 程序的示例。假设你想实现一个新功能，当你在列表视图双击某本书时，弹出它的描述。为此，你会创建一个槽并将其连接到 `doubleClicked()` 信号。列表 8.3 显示了该函数的简单实现。在这个示例中，槽 `MainWindow::ShowDescription()` 被实现了。每当你双击一个项目时，该槽就会弹出一个信息窗口。信息窗口是由第 10 章“理解 Qt 对话框”中的 `QMessageBox` 类创建的。

## 列表 8.3 带有信息的列表视图

```cpp
#include <application.h>
#include <widget.h>
#include <qlistview.h>
#include <qmessagebox.h>

// 忘记为类声明单独创建一个 .h 文件
// 然后
```

## 了解 Qt 控件：第三课

```cpp
8: //对它使用元对象编译器（moc）。
9: class MyMainWindow : public QWidget
10: {
11:     Q_OBJECT
12:     public:
13:         MyMainWindow();
14:     private:
15:         QListView *listview;
16:         QListWidgetItem *topic1;
17:         QListWidgetItem *topic2;
18:         QListWidgetItem *topic3;
19:         QListWidgetItem *item;
20:         QMessageBox *box;
21:     public slots:
22:         void ShowDescription();
23:     };
24: 
25: // 这是我们的新槽：
26: void MyMainWindow::ShowDescription()
27: {
28:     box = new QMessageBox("Box Info", "在这里，我们可以显示一些关于
29:                         你刚刚双击的简短
30:                         信息文本。",
31:                         QMessageBox::Information, QMessageBox::Ok, 0, 0);
32:     box->show();
33: }
34: 
35: MyMainWindow::MyMainWindow()
36: {
37:     setGeometry(100, 100, 300, 300);
38: 
39:     listview = new QListView(this);
40:     listview->setGeometry(0, 0, 400, 400);
41:     listview->setRootIsAbstract(true);
42: 
43:     listview->addItem("Book");
44:     listview->addItem("Sold Copies");
45:     listview->addItem("Price");
46: 
47:     topic1 = new QListWidgetItem(listview, "Topic 1", "$21,000");
48:     topic2 = new QListWidgetItem(listview, "Topic 2", "$19,000");
49:     topic3 = new QListWidgetItem(listview, "Topic 3", "$34,000");
50: 
51:     item = new QListWidgetItem(topic1, "Book 1", "$29.99");
52:     item = new QListWidgetItem(topic1, "Book 2", "$19.99");
53:     item = new QListWidgetItem(topic1, "Book 3", "$14.99");
54:     item = new QListWidgetItem(topic2, "Book 4", "$38.00");
55:     item = new QListWidgetItem(topic2, "Book 5", "$14.99");
56:     item = new QListWidgetItem(topic2, "Book 6", "$9,000");
57:     item = new QListWidgetItem(topic3, "Book 7", "$32,000");
58:     item = new QListWidgetItem(topic3, "Book 8", "$25,000");
```

## 代码列表 8.3 继续

```cpp
59:    item = new QListWidgetItem(topic3, "Book 9", "13,000", "44.99");
60: 
61:    connect(listview, SIGNAL(doubleClicked(QWidgetItem *)),
62:             this, SLOT(ShowDescription(int)));
63: }
64: 
65: void main(int argc, char **argv) {
66: {
67:     QApplication a(argc, argv);
68:     MyMainWindow w;
69:     a.setMainWindow(&w);
70:     w.show();
71:     a.exec();
72: }
```

在第 22 行，声明了 `ShowDescription()` 槽。它的实现可以在第 26 到 33 行找到。如你所见，在第 28 到 31 行使用了 `QMessageBox` 类来创建一个在双击项目时弹出的小信息窗口。这是 Qt 的对话框类之一，将在第 10 小时介绍。图 8.4

## 图 8.4

点击了标记为“Book 4”的项目以使信息框出现。点击信息框上的 OK 使其消失。

| 书 | 数量 | 价格 |
|---|---|---|
| Book 1 | 21,000 | $29.99 |
| Book 2 | 15,000 | $24.99 |
| Book 3 | 14,000 | $39.99 |
| Book 4 | 10,000 | $34.99 |
| Book 5 | 16,000 | $19.99 |
| Book 6 | 12,000 | $29.99 |

这一节应该让你对如何在程序中使用列表视图产生一些思路。

## 使用进度条

进度条是一种向用户提供程序当前状态信息的控件。例如，当程序准备执行耗时较的任务时，显示进度条是非常用的，你可以给用户提示他们预计需要多长时间（同时向用户保证程序没有停止）。

Qt 提供了 `QProgressBar` 来创建进度条。另一个类 `QInputDialog` 也可以用于此类任务。`QDialog` 将在第 10 小时讨论。`QProgressBar` 的创建和显示与其他任何 Qt 类一样。为了让进度条工作，你还需要执行其他任务（例如，你需要定义进度条何时更新）。你可以在代码列表 8.4 中找到一个简单的示例。

## 代码列表 8.4 滑块控制进度条

```cpp
1: #include <application.h>
2: #include <widget.h>
3: #include <qslider.h>
4: #include <progressbar.h>
5: 
6: class MainWindow : public QMainWindow
7: {
8: public:
9:     MainWindow();
10: private:
11:     QProgressBar *bar;
12:     QSlider *slider;
13: };
14: 
15: MainWindow::MainWindow()
16: {
17:     setGeometry(100, 100, 300, 300);
18: 
19:     bar = new QProgressBar(this);
20:     bar->setGeometry(100, 50, 200, 30);
21: 
22:     slider = new QSlider(0, this);
23:     slider->setGeometry(10, 100, 180, 30);
24:     slider->Orientation(Horizontal);
25: 
26:     // 连接进度条和滑块，
27:     // 以便滑块控制进度条的进度：
28:     connect(slider, SIGNAL(valueChanged(int)),
29:             bar, SLOT(setProgress(int)));
30: }
31: 
32: void main(int argc, char **argv) {
33:     QApplication a(argc, argv);
```

## 代码列表 8.4 继续

```cpp
35: MyMainWindow w;
36: a.setMainWidget(&w);
37: w.show();
38: a.exec();
39: }
```
