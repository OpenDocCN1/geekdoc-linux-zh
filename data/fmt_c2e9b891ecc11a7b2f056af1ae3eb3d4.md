
## 代码示例：RSS 阅读器

### 主窗口类定义

```cpp
// mainwindow.h
class MainWindow : public QMainWindow {
    Q_OBJECT

public:
    MainWindow(QWidget *parent = nullptr);
    void showArticle(const QModelIndex& index);
    void showRss();

private:
    QHttp *http;
    QLineEdit *lineEdit;
    QTextBrowser *textBrowser;
    QTreeView *treeView;
    QBuffer *rssBuffer;
    int jobId;
};
```

### 构造函数实现

在构造函数中，我们为窗口指定了名称并在表格布局中安排子窗口。在这里，我们将行编辑框跨越一行两列，这可以在第一个 `addWidget()` 调用的第四和第五参数中看到。我们将树视图和文本浏览器插入到第二行，分别位于第一和第二列：

```cpp
// rssreader/mainwindow.cpp
#include <QtGui>
#include <QtXml>
#include <QtNetwork>
#include "mainwindow.h"
#include "rsshandler.h"

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent), jobId(0)
{
    setWindowTitle(tr("SAX RSS Reader"));
    QWidget *cw = new QWidget;
    QGridLayout *lay = new QGridLayout(cw);
    lineEdit = new QLineEdit;
    lay->addWidget(lineEdit, 0, 0, 1, 2);
    treeView = new QTreeView;
    treeView->setRootIsDecorated(false);
    lay->addWidget(treeView, 1, 0);
    textBrowser = new QTextBrowser;
    lay->addWidget(textBrowser, 1, 1);
    setCentralWidget(cw);
    rssBuffer = new QBuffer(this);
    rssBuffer->open(QIODevice::ReadWrite);
    http = new QHttp(this);
    connect(lineEdit, SIGNAL(returnPressed()), SLOT(retrieveRss()));
    connect(treeView, SIGNAL(activated(const QModelIndex&)), SLOT(showArticle(const QModelIndex&)));
    connect(treeView, SIGNAL(doubleClicked(const QModelIndex&)), SLOT(showArticle(const QModelIndex&)));
    connect(http, SIGNAL(requestFinished(int, bool)), SLOT(readResponse(int, bool)));
    statusBar()->showMessage(tr("Welcome to RSS Reader!"));
}
```

整个布局位于一个名为 `cw` 的简单部件上，我们将其作为中心部件插入主窗口中。最后，我们生成一个缓冲区并对其进行读写访问权限。

此外，我们创建了 `QHttp` 对象。该类以纯异步的方式工作，因此理论上甚至不可能将该对象放在栈上，否则会阻塞处理直到事件出现。相反，所有调用都会立即返回。当 `QHttp` 对象处理请求后，它会发送一个信号。

出于这个原因，我们在最后创建了信号/槽连接：最后一个连接与用户触发行编辑框连接，`retrieveRss()` 开始下载文件。第二个和第三个 `connect()` 调用将关键操作或双击与列表视图中的项通过 `showArticle()` 方法连接，该方法会显示相应的文章。最后，我们连接了 `requestFinished()` 信号（该信号在操作完成后触发 `QHttp`）与我们编写的槽 `readResponse()`。

### 13.2 使用 QtXml 处理 XML

在 `retrieveRss()` 中，我们将文本从行编辑框传输到 `QUrl` 中。它会尝试自动解析传递给它的 URL：

```cpp
// rssreader/mainwindow.cpp (continued)
void MainWindow::retrieveRss() {
    QUrl url(lineEdit->text());
    if (!url.isValid() || url.scheme() != "http") {
        statusBar()->showMessage(tr("Invalid URL: '%1'").arg(lineEdit->text()));
        return;
    }
    http->setHost(url.host());
    jobId = http->get(url.path(), rssBuffer);
    statusBar()->showMessage(tr("Getting RSS Feed '%1'...").arg(url.toString()));
}
```

在 `readResponse()` 槽中，我们只获取 Get 任务的结果。第二个参数指定了文件下载期间是否发生了错误，可能是因为服务器不可用或路径不对。如果不是如此，我们通过 `showRss()` 处理数据并在状态栏中发布一条三秒的成功消息。否则，将出现一段时间的错误消息：

```cpp
// rssreader/mainwindow.cpp (continued)
void MainWindow::readResponse(int id, bool error) {
    if (id == jobId) {
        if (!error) {
            showRss();
            statusBar()->showMessage(tr("RSS-Feed loaded successfully"), 3000);
        } else {
            statusBar()->showMessage(tr("Error while fetching feed!"), 3000);
        }
    }
}
```

`showRss()` 执行实际工作。在这里我们创建了一个具有两列的标准模型，随后将其传递给 `RssHandler`。

```cpp
// rssreader/mainwindow.cpp (continued)
void MainWindow::showRss() {
    QStandardItemModel *model = new QStandardItemModel(0, 2);
    RssHandler handler(model);
    QXmlSimpleReader reader;
    reader.setContentHandler(&handler);
    reader.setErrorHandler(&handler);
    QXmlInputSource source(rssBuffer);
    if (!reader.parse(source)) {
        return;
    }
    delete treeView->model();
    treeView->setModel(model);
}
```

`QXmlSimpleReader` 负责使用 `RssHandler` 解析文件。由于 `RssHandler` 继承自 `QXmlDefaultHandler`，并因此继承自所有处理器，我们只实现了 `QXmlContentHandler` 和 `QXmlErrorHandler` 的功能，因此我们必须将 `RssHandler` 同时注册为 reader 的内容处理器和错误处理器。

作为 `QXmlSimpleReader` 的文档源，使用了 `QXmlInputSource` 类，它从 `QIODevice` 获取数据。由于我们随后实例化了这样一个输入源并在实例化时将缓冲区作为参数传递，我们必须使用 `reset()` 将缓冲区读取位置设置为内部 `QByteArray` 的开头，这样才能读取出内容。`reader.parse()` 开始实际的解析过程。

如果运行成功，我们首先删除与树视图关联的任何现有模型，然后将带有新内容的模型传递给视图。

在最后一步，我们现在需要实现 `showArticle()` 槽，以便在文本浏览器中显示树视图中的条目。为了实现这一点，我们访问活动模型的 `data()`。我们从槽参数中获取当前条目的索引。由于我们选择的角色是 `Qt::UserRole`，我们之前在那里存储了 `<description>` 标签的完整内容。我们现在使用 `toString()` 将其从 `QVariant` 转换为 `QString`，并作为 HTML 传递给文本浏览器：

```cpp
// rssreader/mainwindow.cpp (continued)
void MainWindow::showArticle(const QModelIndex& index) {
    QVariant temp = treeView->model()->data(index, Qt::UserRole);
    QString content = temp.toString();
    textBrowser->setHtml(content);
}
```

现在我们的模拟读取器完成了。强制性的 `main()` 方法实例化 `QApplication`，而 `MainWindow` 对象显示窗口并将其初始大小设置为 640 × 480 像素。应用程序进入事件循环：

```cpp
// rssreader/main.cpp
#include <QtGui>
#include "mainwindow.h"

int main(int argc, char *argv[]) {
    QApplication app(argc, argv);
    MainWindow mw;
    mw.show();
    mw.resize(640, 480);
    return app.exec();
}
```

这个简单的示例已经证明了 SAX 允许解析输出相对较小的文档。但检查变得越精确，代码就越复杂。如果你想避免这种复杂性，而且你本身只处理小型文档，你应该看看文档对象模型（DOM），它遵循一种完全不同的方法。

## 13.3 DOM API

`QDom` 是 Qt 的 DOM API，是访问 XML 文件的非常方便的方法。这里的 `QDomDocument` 类表示一个完整的 XML 文件。它的 `setContent()` 方法能够从 XML 文件生成 DOM 树，反之可以将 DOM 树的内容写入 XML 文档。

DOM 树本身由 DOM 元素（`QDomElement`）组成。它们的起始标签可能包含属性。在起始标签和结束标签之间，DOM 元素可能包含文本或子元素。通过这种方式，DOM 从 XML 结构构建起来，它的元素无例外都是 DOM 节点（`QDomNode`）。

`QDomNode` 知道父子关系的原则：如果它们被插入到树的其他部分，它们不会被复制，而是改变它们在树中的位置。插入 `QDomNode` 的节点现在将作为其新的父节点。每个节点都可能拥有子节点；例如，如果你尝试给属性节点一个子节点，该对象将把新节点作为属性节点的兄弟节点插入。这偏离了 DOM 规范，规范在此时严格地要求抛出一个异常。

这里已经看出与 DOM 规范的一个通用区别：Qt 不使用异常来报告错误，而是使用返回值或选择替代行为。这就是为什么建议在调用之前通过在方法代码中尽可能多地检查来排除错误情况，并在方法调用后也检查方法的返回值。

### 13.3.1 读取处理中的 XML 文件

接下来的 HTML 文件是用 XHTML 编写的：

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
  <title>Title</title>
</head>
<body>
  <p>Example</p>
</body>
</html>
```

为了加载这个示例，我们使用 `QDom` 并对其操作。首先我们通过以下方式读取文件：

```cpp
// domparser/main.cpp
#include <iostream>
#include <QtCore>
#include <QtXml>
using namespace std;

int main(int argc, char* argv[]) {
    QCoreApplication app(argc, argv);
    QFile file("index.xml");
    if (!file.open(QIODevice::ReadOnly)) {
        cout << "Error opening file" << endl;
        return 1;
    }
    QByteArray content = file.readAll();
    QDomDocument doc;
    QString errorMessage;
    int line, col;
    if (!doc.setContent(content, &errorMessage, &line, &col)) {
        cout << "Error in line " << line << " column " << col << ": " << errorMessage.toStdString() << endl;
        return 1;
    }
}
```

为了观察文档类型的不同方面：

```cpp
// domparser/main.cpp
QDomDocumentType type = doc.doctype();
cout << "Document type: " << type.name().toStdString() << endl;
```

我们通过 `documentElement()` 方法获取根元素并保存为 `QDomElement`。

```cpp
// domparser/main.cpp
QDomElement root = doc.documentElement();
cout << "Root tag: " << root.tagName().toStdString() << endl;
if (root.hasAttribute("xmlns")) {
    QDomAttr attr = root.attributeNode("xmlns");
    cout << "xmlns: " << attr.value().toStdString() << endl;
}
if (root.hasAttribute("lang")) {
    QDomAttr attr = root.attributeNode("lang");
    cout << "lang: " << attr.value().toStdString() << endl;
}
```

我们读取根元素的所有子节点。

```cpp
QDomNode node = root.firstChild();
while (!node.isNull()) {
    if (node.isElement()) {
        QDomElement elem = node.toElement();
        cout << "Child of root: " << elem.tagName().toStdString() << endl;
        cout << "Its text: " << elem.text().toStdString() << endl;
    }
    node = node.nextSibling();
}
```

`text()` 方法将元素及其子元素的文本节点收集到一个 `QString` 中。在这里我们从 `head` 元素接收页头文本，以及从 `body` 元素下方三个引用元素 `<a>` 的文本。

我们现在用 `node` 变量填充下一个兄弟节点，并重复此过程。如果没有更多兄弟节点，`nextSibling()` 将返回一个空节点，这不再满足循环条件。因此，上述示例的输出如下：

```
Document type: html
Root tag: html
xmlns: http://www.w3.org/1999/xhtml
lang: en
Child of root: head
Its text: Title
Child of root: body
Its text: Example.comExample.netExample.org
```
