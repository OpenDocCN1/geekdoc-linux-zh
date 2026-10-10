
`connect(&ftp, SIGNAL(done(bool)), this, SLOT(ftpDone(bool)));`

`}`

在构造函数中，我们将 `QFtp::done(bool)` 信号连接到我们的私有槽 `ftpDone(bool)`。当 `QFtp` 完成所有请求时会发射 `done(bool)`。`bool` 参数指示是否发生了错误。

代码视图：

```cpp
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

    if (url.path().isEmpty()) {
        std::cerr << "Error: URL has no path" << std::endl;
        return false;
    }

    QString localFileName = QFileInfo(url.path()).fileName();

    if (localFileName.isEmpty())
        localFileName = "ftpget.out";

    file.setFileName(localFileName);

    if (!file.open(QIODevice::WriteOnly)) {
        std::cerr << "Error: Cannot write file "
        << qPrintable(file.fileName()) << ": "
        << qPrintable(file.errorString()) << std::endl;
        return false;
    }

    ftp.connectToHost(url.host(), url.port(21));

    ftp.login();

    ftp.get(url.path(), &file);

    ftp.close();

    return true;
}
```

`getFile()` 函数首先检查传递的 URL。如果遇到问题，函数将向 `cerr` 打印错误消息并返回 `false`。

我们没有强制用户指定本地文件名，而是尝试使用 URL 本身创建一个合理的名称，回退值为 `ftpget.out`。如果打开文件失败，我们打印错误消息并返回 `false`。

接下来，我们使用我们的 `QFtp` 对象执行一系列 FTP 命令。`url.port(21)` 调用返回 URL 中指定的端口号，如果 URL 本身未指定，则返回 21。由于没有给 `login()` 函数提供用户名或密码，将尝试匿名登录。`get()` 的第二个参数指定了 I/O 设备。FTP 命令在 Qt 的事件循环中被队列并执行。`QFtp` 的 `done(bool)` 信号指示所有命令的完成，我们在构造函数中连接了 `ftpDone(bool)`。

```cpp
void FtpGet::ftpDone(bool error)
{
    if (error) {
        std::cerr << "Error: " << qPrintable(ftp.errorString()) << std::endl;
    } else {
        std::cerr << "File downloaded as " << qPrintable(file.fileName()) << std::endl;
    }

    file.close();

    emit done();
}
```

一旦 FTP 命令执行完毕，我们就关闭文件并发射 `done()` 信号。在 `getFile()` 函数结束处调用 `ftp.close()` 看起来很奇怪，但记住 FTP 命令是异步执行的，在 `getFile()` 返回后可能仍在进行。只有当 `QFtp` 对象的 `done()` 信号发射时，我们才知道下载已完成且关闭文件是安全的。

`QFtp` 提供了几个 FTP 命令，包括 `connectToHost()`、`login()`、`list()`、`get()`、`put()`、`mkdir()`、`rmdir()` 和 `rename()`。所有这些函数都会调度 FTP 命令并返回一个标识命令的 ID 数字。也可以控制传输模式（默认是被动）和传输类型（默认是二进制）。可以使用 `rawCommand()` 执行任意 FTP 命令。例如此处执行 `SITE CHMOD` 命令：

```cpp
ftp.rawCommand("SITE CHMOD 755");
```

`QFtp` 在开始执行命令时发射 `commandStarted(int)` 信号，并在命令完成时发射 `commandFinished(int, bool)` 信号。`int` 参数是标识命令的 ID。如果我们对单个命令感兴趣，可以在调度命令时存储 ID 数字。跟踪 ID 数字允许我们向用户提供详细的反馈。例如：

```cpp
bool FtpGet::getFile(const QUrl &url)
{
    ...

    connectId = ftp.connectToHost(url.host(), url.port(21));

    loginId = ftp.login();

    getId = ftp.get(url.path(), &file);

    closeId = ftp.close();

    return true;
}

void FtpGet::ftpCommandStarted(int id)
{
    if (id == connectId) {
        std::cerr << "Connecting..." << std::endl;
    } else if (id == loginId) {
        std::cerr << "Logging in..." << std::endl;
    }
...
}
```

提供反馈的另一种方法是连接 `QFtp` 的 `stateChanged()` 信号，每当连接进入新状态时（`QFtp::Connecting`、`QFtp::Connected`、`QFtp::LoggedIn` 等），该信号就会发射。在大多数应用程序中，我们只关心整个命令序列的命运，而不是特定的命令。在这种情况下，我们可以简单地连接到命令队列为空时发射的 `done(bool)` 信号。

发生错误时，`QFtp` 会自动清空命令队列。这意味着如果连接或登录失败，队列中的后续命令将永远不会执行。如果在错误发生后使用同一个 `QFtp` 对象调度新命令，这些命令将被队列并执行。

在应用程序的 `.pro` 文件中，我们需要以下行来链接 `QtNetwork` 库：

```
QT += network
```

我们现在查看一个更高级的示例。`spider` 命令行程序下载 FTP 目录中的所有文件，并递归地从所有子目录下载。网络逻辑位于 `Spider` 类中：

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

    QList<QFile*> openedFiles;

    QString currentDir;

    QString currentLocalDir;

    QStringList pendingDirs;
};
```

起始目录被指定为 `QUrl` 并使用 `getDirectory()` 函数设置。

```cpp
Spider::Spider(QObject *parent)
 : QObject(parent)
{
    connect(&ftp, SIGNAL(done(bool)), this, SLOT(ftpDone(bool)));

    connect(&ftp, SIGNAL(listInfo(const QUrlInfo &)), this, SLOT(ftpListInfo(const QUrlInfo &)));
}
```

在构造函数中，我们建立了两个信号与槽连接。当我们为它检索的每个文件请求目录列表（在 `getDirectory()` 中）时，`QFtp` 会发射 `listInfo(const QUrlInfo &)` 信号。该信号被连接到名为 `ftpListInfo()` 的槽，该槽下载与给定的 URL 关联的文件。

```cpp
path = "/";

pendingDirs.append(path);

processNextDirectory();

return true;
}
```

当调用 `getDirectory()` 函数时，它首先开始一些健壮性检查，如果一切正常，它将尝试建立 FTP 连接。它会跟踪必须处理的路径，并调用 `processNextDirectory()` 开始下载根目录。

```cpp
void Spider::processNextDirectory()
{
 if (!pendingDirs.isEmpty()) {
 currentDir = pendingDirs.takeFirst();
 currentLocalDir = "downloads/" + currentDir;
 QDir(".").mkpath(currentLocalDir);
 ftp.cd(currentDir);
 ftp.list();
 } else {
 emit done();
 }
}
```

`processNextDirectory()` 函数从 `pendingDirs` 列表中取出第一个远程目录，并在本地文件系统中创建一个对应的目录。然后，它告诉 `QFtp` 对象切换到获取的目录并列出其文件。对于 `list()` 处理的每一个文件，它都会发射 `listInfo()` 信号，导致 `ftpListInfo()` 槽被调用。

如果没有更多需要处理的目录，该函数将发射 `done()` 信号表示下载已完成。

```cpp
void Spider::ftpListInfo(const QUrlInfo &urlInfo)
{
 if (urlInfo.isFile()) {
 if (urlInfo.isReadable()) {
 QFile *file = new QFile(currentLocalDir + "/" + urlInfo.name());
 if (!file->open(QIODevice::WriteOnly)) {
 std::cerr << "Warning: Cannot write file "
 << qPrintable(QDir::toNativeSeparators(
file->fileName()))
 << ": " << qPrintable(file->errorString())
 << std::endl;
 return;
 }
 ftp.get(urlInfo.name(), file);
 openedFiles.append(file);
 }
 } else if (urlInfo.isDir() && !urlInfo.isSymLink()) {
 pendingDirs.append(currentDir + "/" + urlInfo.name());
 }
}
```

`ftpListInfo()` 槽的 `urlInfo` 参数提供了有关远程文件的详细信息。如果该文件是普通文件（不是目录）且可读，我们调用 `get()` 来下载它。用于下载的 `QFile` 对象使用 `new` 分配，其指针被存储在 `openedFiles` 列表中。

如果 `QUrlInfo` 包含一个不是符号链接的远程目录详细信息，我们将该目录添加到 `pendingDirs` 列表中。我们跳过符号链接，因为它们很容易导致无限递归。

```cpp
void Spider::ftpDone(bool error)
{
 if (error) {
 std::cerr << "Error: " << qPrintable(ftp.errorString())
 << std::endl;
 } else {
 std::cout << "Downloaded " << qPrintable(currentDir) << " to "
 << qPrintable(QDir::toNativeSeparators(
QDir(currentLocalDir).canonicalPath())) <<
 }
 qDeleteAll(openedFiles);
 openedFiles.clear();
 processNextDirectory();
}
```

`ftpDone()` 槽在所有 FTP 命令完成或发生错误时被调用。我们删除 `QFile` 对象以防止内存泄漏并关闭每个文件。最后，我们调用 `processNextDirectory()`。如果留有任何目录，整个过程将从列表中的下一个目录重新开始；否则，下载停止并发射 `done()`。

如果没有错误，FTP 命令和信号的序列如下：

`connectToHost(host, port)`

`login()`

`cd(directory_1)`

`list()`

`emit listInfo(file_1_1)`

`get(file_1_1)`

`emit listInfo(file_1_2)`

`get(file_1_2)`

...

`emit done()`

...

`cd(directory_N)`

`list()`

`emit listInfo(file_N_1)`

`get(file_N_1)`

`emit listInfo(file_N_2)`

`get(file_N_2)`

...

`emit done()`

如果一个文件实际上是一个目录，它会被添加到 `pendingDirs` 列表中。当当前 `list()` 命令的最后一个文件下载完成后，将发布一个新的 `cd()` 命令，紧接着是针对下一个待处理目录的 `list()` 命令，整个过程将从新目录重新开始。此过程不断重复，下载新文件并将新目录添加到 `pendingDirs` 列表中，直到每个目录中的每个文件都下载完毕，此时 `pendingDirs` 列表最终将为空。

如果在下载目录中的 20 个文件中的第 5 个时发生网络错误，剩余的文件将不会下载。如果我们希望尽可能下载文件，一种解决方案是一次调度一个 `GET` 操作，并在等待 `done(bool)` 信号后再调度新的 `GET` 操作。在 `listInfo()` 中，我们只需将文件名添加到 `QStringList` 中，而不是立即调用 `get()`，而在 `done(bool)` 中我们对 `QStringList` 中的下一个要下载的文件调用 `get()`。执行顺序将像如下所示：

代码视图：

`connectToHost(host, port)`

`login()`

`cd(directory_1)`

`list()`

...

`cd(directory_N)`

`list()`

`emit listInfo(file_1_1)`

`emit listInfo(file_1_2)`

`emit listInfo(file_N_1)`

`emit listInfo(file_N_2)`

`emit done()`

`get(file_1_1)`

`get(file_1_2)`

`get(file_N_1)`

`get(file_N_2)`

另一种解决方案是每个文件使用一个 FTP 对象。这将允许我们通过单独的连接下载文件。

```cpp
int main(int argc, char *argv[])
{
 QCoreApplication app(argc, argv);

 QStringList args = QApplication::arguments();

if (args.count() != 2) {
 std::cerr << "Usage: spider url" << std::endl;
 << "Example:" << std::endl;
 << "spider ftp://trolltech.com/freebies/"
return 1;
}

 Spider spider;

 if (!spider.getDirectory(QUrl(args[1]))) {
 return 1;
 }

 QObject::connect(&spider, SIGNAL(done()), &app, SLOT(quit()));

 return app.exec();
}
```
