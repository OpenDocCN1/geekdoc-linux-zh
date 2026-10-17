
```cpp
void MyThread::run()
{
    QMetaObject::invokeMethod(label, SLOT(const QString &),
	Q ARG(QString, "Hello"));
	....
}
```

Qt 的许多非 GUI 类（包括 `QImage`、`QString` 和容器类）使用**隐式共享**作为优化技术。虽然这种优化通常会使类变得不可重入，但在 Qt 中这不是一个问题，因为 Qt 使用原子汇编指令来实现线程安全的引用计数，使得 Qt 的隐式共享类是重入的。

Qt 的 `QtSql` 模块也可以用于多线程应用程序，但它有自己的限制，这些限制随数据库而异。详情请参阅 <http://doc.trolltech.com/4.3/sql-driver.html>。关于多线程注意事项的完整列表，请参阅 <http://doc.trolltech.com/4.3/threads.html>。

- 编写 FTP 客户端
- 编写 HTTP 客户端
- 编写 TCP 客户端-服务器应用程序
- 发送和接收 UDP 数据报

![](img/930c1c6fda99d425284503ebcbc940ea_381_0.png)

# 15. 网络

Qt 提供了 `Qftp` 和 `Qhttp` 类用于处理 FTP 和 HTTP。这些协议对于下载和上传文件非常容易，在 HTTP 的情况下，还用于向网络服务器发送请求并检索结果。

Qt 还提供了更底层的 `QtcpSocket` 和 `QUdpSocket` 类，它们实现了 TCP 和 UDP 传输协议。TCP 是一种可靠的面向连接的协议，以网络节点之间传输的数据的形式运行；而 UDP 是一种基于网络节点之间发送的离散数据包的不可靠无连接协议。两者都可创建网络节点和服务器应用程序。对于服务器，我们还需要 `QtcpServer` 类来处理入的 TCP 连接。安全的 SSL/TLS 连接可以使用 `QSSocket` 代替 `QtcpSocket`。

## 编写 FTP 客户端

`Qftp` 类在 Qt 中实现了 FTP 协议的客户端部分。它提供了各种函数来执行最常见的 FTP 操作，并允许我们执行任意 FTP 命令。

Qt 类的命令是异步工作的。当我们调用如 `get()` 或 `put()` 的函数时，它会立即返回，数据传输会在控制权传回 Qt 事件循环时发生。这确保了在执行 FTP 命令时用户界面保持响应。

我们将从一个示例开始，该示例展示了如何使用 `get()` 获取单个文件。该示例是一个名为 `ftpget` 的控制台应用程序，用于下载命令行指定的远程文件。让我们从 `main()` 函数开始：

```cpp
int main(int argc, char *argv[]){
    QCoreApplication app(argc, argv);
    QStringList args = QCoreApplication::arguments();

    if (args.count() != 2) {
        std::cerr << "Usage: ftpget url" << std::endl
        << "Example:" << std::endl
        << " ftpget http://ftp.trolltech.com/mirrors"
        << std::endl;
        return 1;
    }

    FtpGet getter;
    if (!getter.getFile(QUrl(args[1])))
        return 1;

    QObject::connect(&getter, SIGNAL(done()), &app, SLOT(quit()));
    return app.exec();
}
```

我们创建一个 `QCoreApplication` 而不是其子类 `QApplication` 是为了避免链接 `QtGui` 库。`QCoreApplication::arguments()` 函数将命令行参数作为 `QStringList` 返回，第一项是程序被调用的名称，以及任何 Qt 特有的参数（如 `-`）。

```cpp
class FtpGet : public QObject
{
    Q_OBJECT
public:
    FtpGet(QObject *parent = 0);
    bool getFile(const QUrl &url);

signals:
    void done();

private slots:
    void ftppDone(bool error);

private:
    QFtp ftp;
    QFile file;
};

FtpGet::FtpGet(QObject *parent)
    : QObject(parent)
{
    connect(&ftp, SIGNAL(done(bool)), this, SLOT(ftppDone(bool)));
}

bool FtpGet::getFile(const QUrl &url)
{
    if (!url.isValid()) {
        std::cerr << "Error: Invalid URL" << std::endl;
        return false;
    }

    if (url.scheme() != "ftp") {
        std::cerr << "Error: URL must start with 'ftp:'" << std::endl;
        return false;
    }

    if (url.path().empty()) {
        std::cerr << "Error: URL has no path" << std::endl;
        return false;
    }

    QString localFileName = QFileInfo(url.path()).fileName();
    if (localFileName.isEmpty()) {
        localFileName = "ftpgetout";
    }

    QFile file(localFileName);
    if (!file.open(QIODevice::WriteOnly)) {
        std::cerr << "Error: Cannot write file " << qPrintable(file.fileName()) << ": " << qPrintable(file.errorString()) << std::endl;
        return false;
    }

    ftp.connectHost(url.host(), url.port(21));
    ftp.get(url.path(), &file);
    file.close();
    return true;
}

void FtpGet::ftppDone(bool error)
{
    if (!error) {
        emit done();
    }
}
```

## 362 15. 网络

URL 本身没有指定任何内容。由于没有向 `login()` 函数提供用户名或密码，它将尝试匿名登录。`get()` 的第二个参数指定了输出 I/O 设备。

FTP 命令在 Qt 的事件循环中被调度和执行。所有命令的完成通过 `QFtp` 的 `done(bool)` 信号来指示，我们在构造函数中将其连接到了 `ftpDone(bool)`。

```cpp
void QFtp::ftpDone(bool error)
{
    if (error) {
        std::cerr << "Error. " << qPrintable(ftp.errorString()) << std::endl;
    } else {
        std::cerr << "File downloaded as " << qPrintable(file.fileName()) << std::endl;
    }
    file.close();
    emit done();
}
```

一旦 FTP 命令执行完毕，我们就关闭文件并发射我们自己的 `done()` 信号。在这里关闭文件而不是在 `getFile()` 函数末尾的 `ftp.close()` 调用之后关闭，可能看起来很奇怪，但请记住 FTP 命令是异步执行的，在 `getFile()` 函数返回后它们可能仍在进行中。只有当 `QFtp` 对象的 `done()` 信号发射时，我们才知道下载已完成，可以安全关闭文件。

`QFtp` 提供了若干 FTP 命令，包括 `connectToHost()`、`login()`、`close()`、`list()`、`cd()`、`get()`、`put()`、`mkdir()`、`rmdir()` 和 `rename()`。这些函数都会执行 FTP 命令并返回一个标识该命令的 ID。还可以控制传输模式（默认为被动模式）和传输类型（默认为二进制）。

可以使用 `rawCommand()` 执行任意 FTP 命令。例如，这里是使用 `SITE CHMOD` 命令的方法：

```cpp
ftp.rawCommand("SITE CHMOD 755 fortune")
```

`QFtp` 在开始执行命令时发射 `commandStarted(int)` 信号，在命令完成时发射 `commandFinished(int, bool)` 信号。参数是标识命令的 ID。如果对单个命令的执行结果感兴趣，我们可以在调度命令时存储 ID 数字。跟踪 ID 允许我们向用户提供反馈。例如：

```cpp
bool QFtp::getFile(const QUrl &url)
{
    connectId = ftp.connectToHost(url.host(), url.port(21));
    loginId = ftp.login();
    getId = ftp.get(url.path(), &file);
```

![](img/930c1c6fda99d425284503ebcbc940ea_384_0.png)

## 编写 FTP 客户端

```cpp
closeId = ftp.close();
return true;
}
void FtpGet::sendCommandStarted(int id)
{
    if (id == connectId)
        std::cerr << "Connecting..." << std::endl;
    else if (id == loginId)
        std::cerr << "Logging in..." << std::endl;
    ...
}
```

另一种提供反馈的方法是连接到 `QFtp::stateChanged()` 信号，每当连接进入新状态（`QFtp::Connecting`、`QFtp::Connected`、`QFtp::LoggedIn` 等）时，该信号就会发射。

在大多数应用程序中，我们只对命令序列的整体结果，而不是特定的命令。在这种情况下，我们可以简单地连接到 `done(bool)` 信号，每当命令队列变空时，该信号就会发射。

当发生错误时，`QFtp` 会自动清除命令队列。这意味着如果连接或登录失败，队列中后续命令将永远不会执行。如果我们在错误发生后使用同一个 `QFtp` 对象调度了新命令，这些命令将被排队并执行。

在应用程序的 `.pro` 文件中，我们需要以下行来链接 `QtNetwork` 库：

```pro
QT += network
```

我们现在来查看一个更高级的示例。蜘蛛命令行程序会下载 FTP 目录中的所有文件，递归地从该目录的所有子目录中下载。网络逻辑位于 `Spider` 类中：

```cpp
class Spider : public QObject
{
    Q_OBJECT
public:
    Spider(QObject *parent = 0);
    bool getDirectory(const QUrl &url);
signals:
    void done();

private slots:
    void ftpDone(bool error);
    void ftpListInfo(const QUrlInfo &urlInfo);

private:
    void processNextDirectory();

    QFtp ftp;
    QList<QFile *> openedFiles;
    QString currentDir;
    QString currentLocalDir;
    QStringList pendingDirs;
};
```

起始目录由 `QUrl` 指定，并使用 `getDirectory()` 函数设置。

```cpp
Spider::Spider(QObject *parent)
    : QObject(parent)
{
    connect(&ftp, SIGNAL(done()), SLOT(ftpDone()));
    connect(&ftp, SIGNAL(listInfo(const QUrl &)),
        this, SLOT(listInfo(const QUrl &)));
}
```

在构造函数中，我们建立了双槽连接。当我们在 `getDirectory()` 中请求目录列表时，对于获取的每一个文件，`QFtp` 发射 `listInfo(const QUrlInfo&)` 信号。该信号被连接到一个名为 `ftpplistInfo()` 的槽，该槽会下载与给定 URL 关联的文件。
