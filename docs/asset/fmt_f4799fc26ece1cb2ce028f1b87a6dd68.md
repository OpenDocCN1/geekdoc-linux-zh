
`getFile()` 函数首先检查传入的 URL。如果遇到问题，函数将向 `cerr` 打印错误消息并返回 `false` 以表示下载失败。

我们没有强迫用户创建一个本地名称，而是使用 URL 本身创建一个合理的名称，并以 `ftpget.out` 作为备选方案。如果我们无法打开文件，将打印错误消息并返回 `false`。

接下来，我们使用 `QFtp` 对象执行系列的一四个 FTP 命令。`url.port(21)` 调用返回 URL 中指定的端口号，如果 URL 本身未指定，则返回端口 21。由于没有为 `login()` 函数提供用户名或密码，因此将尝试匿名登录。`get()` 的第二个参数指定了输出 I/O 设备。

FTP 命令被队列并在 Qt 的事件循环中执行。所有命令的完成通过 Qt 的 `done(bool)` 信号指示，我们在构造函数中将其连接到了 `ftpDone(bool error)`。

```cpp
void FtpGet::ftpDone(bool error)
{
    if (error) {
        cerr << "Error: " << qPrintable(ftp.errorString()) << endl;
    } else {
        cerr << "File downloaded as " << qPrintable(file.fileName()) << endl;
    }
    file.close();
    emit done(error);
}
```

一旦所有 FTP 命令执行完毕，我们就会关闭文件并发出自己的 `done()` 信号。在这里关闭文件而不是在 `getFile()` 函数末尾的 `ftp.close()` 调用之后关闭文件，可能看起来很奇怪，但因为 FTP 命令是异步执行的，在 `get()` 函数返回后可能仍在进行中。只有当 `QFtp` 对象的 `done` 信号发出时，我们才知道下载已完成，并且关闭文件是安全的。

`Ftp` 提供了几个 FTP 命令，包括 `connectToHost()`、`login()`、`close()`、`list()`、`cd()`、`get()`、`put()`、`remove()`、`mkdir()`、`rmdir()` 和 `rename()`。这些函数中没有一个是执行 FTP 命令并返回的。

```cpp
void Spider::processNextDirectory()
{
```

## 编写 FTP 客户端

`processNextDirectory` 函数从 `pendingDirs` 列表中取出第一个远程目录，并在本地文件系统中创建对应的目录。接着，它告诉 Qt 对象切换到已获取的目录并列出其文件。对于 `list()` 处理的每一个文件，它都会发射一个 `listInfo()` 信号，导致 `listInfo()` 槽被调用。

如果没有更多需要处理的目录，该函数将发射 `done()` 信号，表示下载已完成。

```cpp
void Spider::ftpListInfo(const QUrl &urlInfo) {
    if (urlInfo.isFile()) {
        if (urlInfo.isReadable()) {
            QFile *file = new QFile(currentLocalDir + "/"
                + urlInfo.name());

            if (file->open(QIODevice::WriteOnly)) {
                cerr << "Warning: Cannot open file "
                    << qPrintable(
                        QDir::convertSeparators(file->fileName()))
                    );

                return;
            }

            ftp.get(urlInfo.name(), file);
            openedFiles.append(file);
        }
    } else if (urlInfo.isDir() && urlInfo.isSymLink()) {
        pendingDirs.add(currentDir + "/" + urlInfo.name());
    }
}
```

`listInfo()` 槽的 `urlInfo` 参数提供了关于远程文件的详细信息。如果它是一个普通文件（不是目录）且可读，我们调用 `get()` 来下载它。用于下载的 `QFile` 对象通过 `new` 分配，其指针被存储在 `openedFiles` 列表中。

如果 `QUrl` 包含一个非符号链接的远程目录详情，我们将该目录添加到 `pendingDirs` 列表中。我们跳过符号链接，因为它们很容易导致无限递归。

```cpp
void Spider::ftpDone(bool error) {
```

## 14. 网络编程

```cpp
if (error) {
    cerr << "Error: " << qPrintable(ftp.errorString()) << endl;
} else {
    cout << "Downloaded " << qPrintable(currentDir) << " to "
        << qPrintable(QDir::convertSeparators(
        QDir(currentDir).canonicalPath()));
}

qDeleteAll(openedFiles);
openedFiles.clear();
```

`ftpDone()` 槽在 FTP 命令完成或发生错误时被调用。我们删除 `QFile` 对象以防止内存泄漏，并关闭每个文件。最后，我们调用 `processNextDirectory()`。如果还有剩余的目录，将从列表中的下一个目录重新处理；否则，下载停止并发射 `done()`。

如果没有错误，FTP 命令和信号的执行序列如下：

```
connectHost(host, port)
login()

cd(directory_1)
list()
    emit listInfo(file_1_1)
    get(file_1_1)
    emit listInfo(file_1_2)
    get(file_1_2)
...
emit done()
n...
```

```
cd(directory_N)
list()
    emit listInfo(file_N_1)
    get(file_N_1)
    emit listInfo(file_N_2)
    get(file_N_2)
...
emit done()
```

如果一个文件实际上是一个目录，它会被添加到 `pendingDirs` 列表中。当当前 `list()` 命令的最后一个文件下载完成后，将发出一个新的 `cd()` 命令，随后是针对下一个目录的新 `list()` 命令，整个过程将从新目录重新开始。此过程会不断重复，下载新文件并将新目录添加到 `pendingDirs` 列表中，直到每个目录中的每个文件都下载完毕，此时 `pendingDirs` 列表将最终变为空。

## 编写 FTP 客户端

如果在下载某个目录中（ 20 个文件中的第 5 个文件时发生网络错误，剩余的文件将不会被下载。如果我们想下载尽可能的文件，一种解决方案是一次性调度所有的 `GET` 操作，并等待 `done(bool)` 信号出现后再调度新的 `GET` 操作。在 `listInfo()` 中，我们只需将文件名追加到 `QString` 中，而不是立即调用 `get()`；而在 `done(bool)` 中，我们将对 `QStringList` 中的下一个待下载的文件调用 `get()`。执行执行顺序将像如下所示：

```
connectToHost(host, port)
login()

cd(directory_1)
list()

cd(directory_N)
list()
    emit listInfo(file_1_1)
    emit listInfo(file_1_2)
    ...
    emit listInfo(file_N_1)
    ...
```

另一种解决方案是为每个文件使用一个 `QFtp` 对象。这将允许我们并行下载文件。

```cpp
int main(int argc, char *argv[])
{
    QCoreApplication app(argc, argv);
    QStringList args = app.arguments();

    if (args.count() != 2) {
        cerr << "Usage: spider url" << endl;
        cerr << "Example:" << endl;
        return 1;
    }
```

## 14. 网络编程

一旦 HTTP 请求完成，我们将关闭文件，如果发生错误则通知用户。

`main()` 函数与 `tpgetget` 中使用的非常相似：

```cpp
int main(int argc, char *argv[])
{
    QCoreApplication app(argc, argv);
    QStringList args = app.arguments();

    if (args.count() != 2) {
        cerr << "Usage: httpget url" << endl;
        cerr << "Example:" << endl;
        cerr << "http://doc.trolltech.com/qq/index.html"
             << endl;
        return 1;
    }

    HttpGet getter;
    if (!getter.getFile(args[1])) {
        return 1;
    }

    QObject::connect(&getter, SIGNAL(done()), &app, SLOT(quit()));

    return app.exec();
}
```

`Http` 类执行了许多操作，包括 `host()`、`get()`、`post()` 和 `head()`。如果网站需要身份验证，可以使用 `setUser()` 提供用户名和密码。`Http` 可以使用程序提供的套接字而不是内部的 `QtSocket`（作为 Trolltech 的一种 Qt 解决方案），来实现基于 SSL 的 HTTP。

要向 CGI 脚本发送“name=value”列表，我们可以使用 `post()`：

```cpp
http.setHost("www.example.com");
http.post("/cgi/somecript.py","x=200&y=320&file");
```

我们可以通过 8 位字符串或通过传递一个 `QIODataDevice` 对象（如 `QFile`）来传递数据。为了为了进一步的控制，我们可以使用 `request(int)` 函数，它接受任意的 HTTP 头部和数据。

```cpp
HttpRequest header("POST","/search.html");
header.setValue("Host","www.trolltech.com");
header.setContentType("application/x-www-form-urlencoded");
http.setHost("www.trolltech.com");
http.request("qt-internet=on&search=opengl");
```

`Http` 在开始执行请求时会发出 `request(int)` 信号，并在请求完成后会发出 `requestfinished(int, bool)` 信号。`int` 参数是一个标识请求的 ID 数字。如果我们对单个请求的命运感兴趣，可以在调度请求时存储这些 ID 数字。跟踪这些 ID 数字允许我们向用户提供详细的反馈。

## 编写 HTTP 客户端

在大多数应用程序中，我们只想知道整个请求序列是否成功完成。通过连接到 `done(bool)` 信号很容易实现，当请求队列为空时会发出该信号。

当发生错误时，请求队列会自动清空。如果在错误发生后使用同一个 `HTTP` 对象调度了新请求，这些请求将按 usual入队并发送。

与 `QHttp` 类似，`QHttp` 也提供了 `readyRead()` 信号以及 `read()` 和 `readAll()` 函数，可以使用它们来代替指定 I/O 设备。

## 编写 TCP 客户端服务器应用程序

`TcpSocket` 和 `QTcpServer` 类可以实现 TCP 客户端和服务器。TCP 是一种传输协议，它是大多数应用层网络协议（包括 FTP 和 HTTP）的基础，也可以用于自定义协议。

TCP 是一个面向流的协议。对于应用程序来说，数据看起来是一个长流，就像一个巨大的扁平文件。构建在 TCP 之上的高层协议通常是面向行或面向块的：

- 面向行的协议以文本行的形式传输数据，每行都以换行符结束。
- 面向块的协议以二进制数据块的形式传输数据。每个块由一个 own字段和随后的数据组成。

`TcpSocket` 通过 `QObject` 继承自 `AbstractSocket`，因此可以使用 `QDataStream` 或 `QTextStream` 进行读取和写入。与从文件读取数据相比，从网络读取数据时的一个显著区别是，在使用 `>>` 运算符之前，我们必须确保已经从对端接收了足够的数据。这样做可能会导致未定义行为。

在本节中，我们将回顾一个使用自定义面向块协议的客户端和服务器代码。客户端被称为 `Trip Planner`（旅行计划器），允许用户规划下一次火车旅行。服务器被称为 `Trip Server`（旅行服务器），并为客户端提供行程信息。我们将从编写 `Trip Planner` 开始。

`Trip Planner` 提供了一个出发地（From）字段、一个目的地（To）字段、一个日期（Date）字段以及两个单选按钮，用于选择哪个近似时间是出发或到达时间。当用户点击“搜索”（Search）时，应用程序会向服务器发送请求，服务器将返回符合用户标准的火车行程列表。该列表显示在 `Trip Planner` 窗口的 `QTableWidget` 中。窗口的最底部由一个 `QLabel` 占据，显示最后一次操作的状态，以及 `QProgressBar`。

## 14. 网络编程

![](img/34bd675de80edd220dc2d53b429caf78_341_0.png)

图 14.1. `Trip Planner` 应用程序

`Trip Planner` 的用户界面是用 Qt Designer 在名为 `tripplanner.ui` 的文件中创建的。在这里，我们将重点关注实现应用程序功能的 `QDialog` 类的源代码：

```cpp
#include "ui_tripplanner.h"

class TripPlanner : public QDialog, public Ui::TripPlanner
{
    Q_OBJECT

public:
    TripPlanner(QWidget *parent = 0);

    private slots:
    void connectToServer();
    void requestServer();
    void updateTableWidget();
    void stopSearch();
    void connectionClosed();
    void error();

private:
    void closeConnection();

    QTcpSocket *tcpSocket;
    int nextBlockSize;
};
```

`TripPlanner` 类继承自 `Ui::TripPlanner`（由 uic 生成）。`tcpSocket` 成员封装了连接。`nextBlockSize` 变量用于解析从服务器接收的块。
