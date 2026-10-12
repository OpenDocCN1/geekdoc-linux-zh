
这些槽与应用程序将拥的功能列表密切相关。我们可以按照几乎任意的顺序实现这些槽，但必须先编写数据库连接代码。设置部分完全独立于数据库；我们将简要提到一下设置框，因为它主要由纯 GUI 组件组成，额外的代码较少。

让我们查看主窗口，我们以与上一章相同的方式打开它：

```cpp
MainWindow::MainWindow() : QMainWindow(0, "dvdstore") {
  setWindowTitle("DVDstore");
  m_pStoreMenu = new QPopupMenu(this);
}
```

在这里，我们使用窗口标题并为我们的主栏创建一个新菜单。我们使用 `QPopupMenu` 类来实现这一点，它也可以用于创建上下文敏感的弹出菜单；当我们在讨论搜索对话框时，我们将看到如何创建这样的菜单。

像往常一样，我们通过将主窗口对象传递给 `QPopupMenu` 构造函数来指定父对象。为了连接数据库，我们需要一个菜单项和一个工具栏按钮。

### 菜单项

首先，我们创建菜单项：

```cpp
m_ConnectItem = m_pStoreMenu->insertItem(
  "&Connect...",
  this,
  SLOT(connectDatabase()));
```

该函数返回插入项的标识符。你通常可以忽略它，但在这种情况下我们没有。

# 使用 KDE/Qt DVD 商店 GUI

![](img/930f7611cac03a5cd5573f4bb94fd7b9_518_0.png)

### 事务日志

应当尽一切努力确保事务日志的安全

我们将在主窗口的析构函数中使用日志文件保存功能。我们将使用 `QFile` 类，并让一个文本流 `QTextStream` 来处理文件。这是处理文件的常用方法。Qt 也有一个处理二进制数据的 `QDataStream`。我们将使用一个简单的 ASCII 文本文件作为日志。

```cpp
MainWindow::MainWindow()
{
    QString logfile = SettingManager::instance()->getString("logfile");
    if(logfile == "")
        logfile = "logfile.txt";
    QFile f(logfile);
    if(f.open(IO_WriteOnly | IO_Read | IO_Append))
    {
        QTextStream s(&f);
        s << m_log->text();
        s << "\n";
        f.close();
    }
}
```

析构函数检查是否指定了日志文件名称（如果没有则使用默认名称），并将其传递给 `QFile` 构造函数，该构造函数以“写入”和“追加”模式打开文件，且不带任何缓冲

如你所见，流的操作与标准 I/O 流的工作方式相同。你可能会问为什么要选择 Qt 类。原因之一是可移植性，除了我们使用的数据库库外，我们的应用程序可以在不修改任何代码的情况下在 Windows 上编译！另一个原因是，如果你坚持使用 Qt，你就不需要链接其他库，因为你可能在 Qt 中已拥有所需的一切。

# 第 14 章

你可能会发现扩展 Qt 流更加容易，因为 Qt 运行在 `QIODeviceDevice` 类上，该类可以被子类，而标准的 `iostream` 不能在该类上工作。创建 `cin`、`cout` 和 `cerr` 包装器只需要：

```cpp
QTextStream cout(stdout, IO_WriteOnly);
QTextStream cin(stdin, IO_ReadOnly);
QTextStream cerr(stderr, IO_WriteOnly);
```

如果你需要，你也可以配合流类处理 `QString` 对象和字节数组。

### 成员对话框 (Member Dialog)

这是我们向应用程序添加成员的地方，这需要访问数据库后端。我们使用了在第 4 章实现的 C 语言库。由于我们使用 C++，我们会在 `dvd.h` 头文件周围添加一个薄封装。我们将其命名为 `qdvd.h`：

```cpp
#ifndef _cplusplus
extern "C"
#endif
#include "qdvd.h"
#ifdef _cplusplus
#endif
```

`memberdialog.h` 如下所示：

```cpp
#include <qdvd.h>
#include <qlineedit.h>
```

```cpp
class MemberDialog : public QDialog{
    Q_OBJECT
public:
    MemberDialog(const char *m_member_no, QWidget *parent = 0, const char *name = 0);
    virtual ~MemberDialog();
```

private slots:
    void okay();

private:

QLineEdit *m_pTitle;
QLineEdit *m_pFirstName;
QLineEdit *m_pLastName;
QLineEdit *m_pHouseNum;
QLineEdit *m_pkddri;
QLineEdit *m_pkddri;
QLineEdit *m_pTown;
QLineEdit *m_pState;
QLineEdit *m_pZip;
QLineEdit *m_pPhone;
QString *m_MemberNo;

# 使用 KDE/Qt DVD 商店 GUI

在 `okay` 槽函数中，我们将复制行编辑框中的所有文本并将其放入一个结构中，并将该结构传递给数据库。`memberdialog.cpp`：

```cpp
MemberDialog::MemberDialog(
    const char *member_no,
    QWidget *parent,
    const char *name)
    : QDialog(parent, name, true)
)
```

我们将 `true` 作为 `QDialog` 构造函数的最后一个参数，这意味着成员对话框将是模态的。这使得我们的工作变得更加简单，尽管非模态的方案可能会给用户更大的灵活性。

我们选择了一个垂直布局来放置小部件，带有 4 像素的边框以及内容之间 4 像素的间距：

```cpp
QVBoxLayout *main = new QVBoxLayout(this, 4, 4);
```

成员通过姓名和地址识别。为了用户友好的 GUI，我们希望强调这种自然的分组。我们希望在每个组周围有一个边框，实现的方法是使用 `QGroupBox` 或其派生类。我们将使用水平方向的 `QGroupBox`：

```cpp
QGroupBox *namebox = new QGroupBox("Name", this);
```

在该框内部，我们希望左侧有一列标签，描述右侧列的单行编辑字段。我们希望它们对齐齐，因此我们选择使用网格，具体来说是使用 `QGrid`。我们不能在组框内使用布局：

```cpp
QGrid *topgrid = new QGrid(2, namebox);
topgrid->setSpacing(4);
```

我们通过让 `namebox` 框成为网格的父对象，在框内创建了一个两列（任意数量行）的网格。我们将网格中组件之间的间距设置为 4 像素。

我们通过简单地让每个小部件以网格为父对象来填充它：

```cpp
(void) new QLabel("Title:", topgrid);
m_pTitle = new QLineEdit(topgrid);
```

在这里我们填充网格的一行：

| Label | Field |
|---|---|
| Title | 1 |
| FirstName | 2 |
| LastName | 3 |
| HouseNum | 4 |
| Address1 | 5 |
| Address2 | 6 |
| Town | 7 |
| State | 8 |
| Zipcode | 9 |
| Phone | 10 |

注意我们不需要存储标签对象，因为当用户点击 OK 按钮时，我们将 GUI 中的值填充成员结构：

| Label | Field |
|---|---|
| Title | 1 |
| FirstName | 2 |
| LastName | 3 |
| HouseNum | 4 |
| Address1 | 5 |
| Address2 | 6 |
| Town | 7 |
| State | 8 |
| Zipcode | 9 |
| Phone | 10 |

现在我们有了成员结构，必须检查它是现有成员还是新成员。变量 `m_MemberNumber` 包含成员编号，任何更改均构造函数给出：
