
# 会话管理

`commitData()` 函数在用户注销时调用。我们可以重新实现它，弹出一个消息框警告用户可能会丢失数据。默认实现会关闭所有顶层部件，其行为与用户通过点击标题栏上的关闭按钮一个一个关闭窗口的行为相同。在第 3 章中，我们看到过如何重新实现 `closeEvent()` 来捕获此操作并弹出消息框。

为了本示例的目的，我们重新实现了 `commitData()`，并在游戏正在进行且会话管理器允许我们与用户交互时，弹出一个消息框请求用户确认注销（见图 23.9）。如果用户点击“是”，我们调用 `release()` 告诉会话管理器继续注销；如果用户点击“否”，我们调用 `cancel()` 取消注销。

**图 23.9. “你真的想退出吗？”**

![](img/1bc72df8c60cf85926d3aefcc273027d_923_0.png)

现在让我们来看 `TicTacToe` 类：

代码视图：

```cpp
class TicTacToe : public QWidget
{
 Q_OBJECT
public:
    TicTacToe(QWidget *parent = 0);
    bool gameInProgress() const;
    QString saveState() const;
    QSize sizeHint() const;
protected:
    void paintEvent(QPaintEvent *event);
    void mousePressEvent(QMouseEvent *event);
private:
    enum { Empty = '-', Cross = 'X', Nought = 'O' };
    void clearBoard();
    void restoreState();
    char board[3][3];
    int turnNumber;
};
```

`TicTacToe` 类派自 `QWidget`，并重新实现了我们在 `Application` 类中使用的 `sizeHint()`、`paintEvent()` 和 `mousePressEvent()`。

```cpp
TicTacToe::TicTacToe(QWidget *parent) : QWidget(parent)
{
    clearBoard();
    if (qApp->isSessionRestored())
        restoreState();
    setWindowTitle(tr("Tic-Tac-Toe"));
}
```

在构造函数中，我们清空棋盘，如果调用应用程序时带有 `-session` 选项，我们就调用 `restoreState()`。

```cpp
void TicTacToe::clearBoard()
{
    for (int row = 0; row < 3; ++row) {
        for (int column = 0; column < 3; ++column) {
            board[row][column] = Empty;
        }
    }
    turnNumber = 0;
}
```

在 `saveState()` 中，我们将棋盘的状态写入磁盘。格式非常直观，用 `'X'` 表示交叉，`'O'` 表示圆，`'-'` 表示空单元。

```cpp
QString TicTacToe::saveState() const
{
    QFile file(sessionFileName());
    if (file.open(QIODevice::WriteOnly)) {
        QTextStream out(file);
        for (int row = 0; row < 3; ++row) {
            for (int column = 0; column < 3; ++column) {
                out << board[row][column];
            }
        }
    }
    return file.fileName();
}
```

`sessionFileName()` 私有函数返回当前会话 ID 和键的文件名。

```cpp
QString TicTacToe::sessionFileName() const
{
    return QDir::homePath() + "/.tactoe_" + qApp->sessionId() + "_" + qApp->sessionKey();
}
```

在 `restoreState()` 中，我们加载对应于恢复会话的文件并填充棋盘。我们根据棋盘上 X 和 O 的数量推断 `turnNumber` 的值。

```cpp
void TicTacToe::restoreState()
{
    QFile file(sessionFileName());
    if (file.open(QIODevice::ReadOnly)) {
        QTextStream in(file);
        for (int row = 0; row < 3; ++row) {
            for (int column = 0; column < 3; ++column) {
                in >> board[row][column];
                if (board[row][column] != Empty)
                    ++turnNumber;
            }
        }
    }
    update();
}
```

测试和调试会话管理可能会令人沮丧，因为我们需要频繁地登录和注销。避免这种情况的一种方法是使用 X11 提供的标准 `xsm` 工具。当我们第一次调用 `xsm` 时，它会弹出一个会话窗口和一个终端。从该终端启动的所有应用程序都将使用 `xsm` 作为会话管理器，而不是通常的系统级会话管理器。然后我们可以使用 `xsm` 的窗口来结束、重启或丢弃会话，并观察应用程序的行为是否符合预期。有关如何操作的详细信息，请参见 [http://doc.trolltech.com/4.3/session.html](http://doc.trolltech.com/4.3/session.html)。

# 24. 嵌入式编程

![](img/1bc72df8c60cf85926d3aefcc273027d_926_0.png)

## 快速上手 Qt/Embedded Linux

- 定制 Qt/Embedded Linux
- 将 Qt 集成到 Qtopia 中
- 使用 Qtopia API

在 PDA 和手机等移动设备上开发运行的软件可能是非常有挑战性的，因为与桌面计算机相比，嵌入式系统通常具有更慢的处理器、更少的永久性存储（闪存内存或硬盘）、更小的内存以及更小的显示屏。

Qt/Embedded Linux（也称为 Qtopia Core）是针对嵌入式 Linux 优化的 Qt 版本。Qt/Embedded Linux 与桌面版 Qt（Qt/Windows、Qt/X11 和 Qt/Mac）相同的 API 和工具，并增加了嵌入式编程所需的类和工具。通过双重许可，它既适用于开源开发也适用于商业开发。

Qt/Embedded Linux 可以运行在任何运行 Linux 的硬件上——包括 Intel x86、MIPS、ARM、StrongARM、Motorola/Freescale 68000 和 PowerPC 架构。

与 Qt/X11 不同，它不需要 X Window 系统；相反，它实现了自己的窗口系统 QWS，从而实现了显著的存储和内存节省。为了进一步减少其内存占用，可以重新编译 Qt/Embedded Linux 以排除未使用的功能。如果能够预先知道设备上使用的应用程序和组件，可以将它们一起编译成单个可执行文件，并对 Qt/Embedded Linux 库进行静态链接。

* 从 4.4 版本开始，Qt 预计也将运行在 Windows CE 上。

Qt/Embedded Linux 还受益于桌面版 Qt 包含的各种功能，包括广泛使用隐式数据共享（“写时复制”）作为一种节省内存的技术、通过 `QStyle` 对自定义小部件样式的支持，以及一个能够调整以最充分利用可用屏幕空间的布局系统。

Qt/Embedded Linux 是 Trolltech 嵌入式产品的基础，该产品还包括 Qtopia Platform、Qtopia PDA 和 Qtopia Phone。这些产品提供了专为便携设备设计的类和应用程序，并可以与多个第三方 Java 虚拟机集成。

### 快速上手 Qt/Embedded Linux

可以在任何配备适当工具链的平台上开发 Qt/Embedded Linux 应用程序。最常见的选项是在 Unix 系统上构建 GNU C++ 交叉编译器。这一过程通过 Dan Kegel 在 [http://kegel.com/crosstool/](http://kegel.com/crosstool/) 提供的脚本和一组补丁得以简化。在本章中，我们使用了 [http://www.trolltech.com/products/qtopia/opensource/](http://www.trolltech.com/products/qtopia/opensource/) 提供的 Qtopia 开源版本 4.2。该版本仅适用于 Linux，并包含了它自己的 Qt/Embedded Linux 4.2，以及支持在桌面 PC 上进行 Qtopia 编程的额外工具。

Qt/Embedded Linux 的配置系统通过 `configure` 脚本的 `-embedded` 和 `-xplatform` 选项支持交叉编译。例如，为 ARM 架构构建，我们需要输入：

```
./configure -embedded arm -xplatform qws/linux-arm-g++
```

我们可以通过向 Qt 的 `mkspecs/qws` 目录添加新文件来创建自定义配置。

Qt/Embedded Linux 直接绘制到 Linux 帧缓冲区（与视频显示相关的内存区域）。图 24.1 所示的虚拟帧缓冲区是一个 X11 应用程序，它逐像素地模拟真实的帧缓冲区。要访问帧缓冲区，你可能需要赋予 `/dev/fb0` 设备写入权限。

**图 24.1. 在虚拟帧缓冲区运行的 Qt/Embedded Linux**

![](img/1bc72df8c60cf85926d3aefcc273027d_928_0.png)

要运行 Qt/Embedded Linux 应用程序，我们必须首先启动一个进程作为 GUI 服务器。该服务器负责为客户端分配屏幕区域并生成鼠标和键盘事件。任何 Qt/Embedded Linux 应用程序都可以通过在命令行中指定 `-qws` 或通过将 `QApplication::GuiServer` 作为第三参数传递给 `QApplication` 构造函数来变成服务器。

客户端应用程序使用共享内存和 Unix 管道与 Qt/Embedded Linux 服务器通信。

## 入门使用 Qt/Embedded Linux

Qt/Embedded Linux 应用程序可以在配备了适当工具链的平台上进行开发。最常见的选项是在 Unix 系统上构建一个 GNU C++ 交叉编译器。这一过程通过 Dan Kegel 在 [http://kegel.com/crosstool/](http://kegel.com/crosstool/) 提供的脚本和一组补丁得以简化。对于本章节，我们使用了从 [http://www.trolltech.com/products/qtopia/opensource/](http://www.trolltech.com/products/qtopia/opensource/) 获取的 Qtopia 开源版 4.2 版本。该版本仅适用于 Linux，并包含了其自持的 Qt/Embedded Linux 4.2 副本，以及用于在桌面级 PC 上进行 Qtopia 编程的额外工具。

Qt/Embedded Linux 的配置系统通过 `configure` 脚本的 `-embedded` 和 `-xplatform` 选项支持交叉编译。例如，要为 ARM 架构构建，我们需要输入：

```
./configure -embedded arm -xplatform qws/linux-arm-g++
```

我们可以通过向 Qt 的 `mkspecs/qws` 目录中添加新文件来创建自定义配置。

Qt/Embedded Linux 直接绘制到 Linux 帧缓冲区（与视频显示相关的内存区域）。图 2.1 所示的虚拟缓冲区是一个 X11 应用程序，它逐像素地模拟了实际帧缓冲区。要访问帧缓冲区，你可能需要赋予 `/dev/fb0` 设备读写权限。

**图 24.1. 在虚拟缓冲区中运行的 Qt/Embedded Linux**

![](img/1bc72df8c60cf85926d3aefcc273027d_932_0.png)

为了运行 Qt/Embedded Linux 应用程序，我们必须首先启动一个作为 GUI 服务器的进程。该服务器负责为客户端分配屏幕区域，并生成鼠标和键盘事件。任何 Qt/Embedded Linux 应用程序都可以通过在命令行中指定 `-qws` 或通过向 `QApplication` 构造函数传递 `QApplication::GuiServer` 作为第三个参数来变成服务器。

客户端应用程序使用共享内存和 Unix 管道与 Qt/Embedded Linux 服务器通信。在后台，客户端将自己绘制到 Linux 帧缓冲区中，并负责绘制自己的窗口装饰。客户端可以使用 QCOP（Qt 通信协议）进行相互通信。客户端可以通过创建一个 `QCopChannel` 对象并连接到其 `received()` 信号来监听命名通道。例如：

```cpp
QCopChannel *channel = new QCopChannel("System", this);
connect(channel, SIGNAL(received(const QString &, const QByteArray &)), this, SLOT(received(const QString &, const QByteArray &)));
```

一个 QCOP 消息由一个名称和一个可选的 `QByteArray` 组成。静态函数 `QCopChannel::send()` 在通道上广播消息。例如：

```cpp
QByteArray data;
QDataStream out(&data, QIODevice::WriteOnly);
out << QDateTime::currentDateTime();
QCopChannel::send("System", "clockSkew(QDateTime)", data);
```

前面的示例说明了一种常用的用法：我们使用 `QDataStream` 编码数据，并在消息名称中对数据格式进行混处理（就像它是 C++ 函数一样），以确保接收端正确解释 `QByteArray`。各种环境变量会影响 Qt/Embedded Linux 应用程序。最重要的变量是 `QWS_MOUSE_PROTO` 和 `QWS_KEYBOARD`，它们指定了鼠标设备和键盘类型。完整的环境变量列表请参见 [http://doc.trolltech.com/4.2/qtopiacore-envvars.html](http://doc.trolltech.com/4.2/qtopiacore-envvars.html)。

如果我们使用 Unix 作为开发平台，我们可以使用 Qt 虚拟缓冲区 (`qvfb`) 来测试应用程序，这是一种模拟实际帧缓冲区的 X11 应用程序。这大大加快了开发周期。若要在 Qt/Embedded Linux 中启用虚拟缓冲区支持，请向 `configure` 脚本传递 `-qvfb` 选项。请注意此选项并非用于生产环境。虚拟缓冲区应用程序位于 `tools` 目录下，调用方式如下：

```
qvfb -width 320 -height 480 -depth 32
```

使用虚拟缓冲区的替代方案是使用 VNC（虚拟网络计算）。要在 Qt/Embedded Linux 中启用 VNC 支持，向 `configure` 传递 `-gfx-vnc` 选项。通过 `-display` 运行 Qt/Embedded Linux 应用程序时指定显示大小和深度可以通过设置环境变量 `QWS_SIZE` 和 `QWS_DEPTH` 实现（例如 `QWS_SIZE=320x480`）。

# 自定义 Qt/Embedded Linux

在安装 Qt/Embedded Linux 时，我们可以指定想要减少的内存占用的特性。Qt/Embedded Linux 包含了上百种可配置的特性，这些特性列在 `src/corelib/global/features.txt` 中。Qt/Embedded Linux 提供了五种示例配置（small、medium、large 和 dist），存储在 `src/corelib/global/` 目录中。可以使用 `configure` 脚本的 `-qconfig` 选项指定这些配置，例如：

```
./configure -qconfig small
```

要创建自定义配置，我们可以手动提供 `qconfig*.h` 文件并将其作为配置使用。或者，我们可以使用位于 Qt 子目录下的 `qconfig` 工具。Qt/Embedded Linux 提供了以下类用于与输入输出设备交互以及自定义窗口的外观：

- **`QScreen`**: 屏幕驱动（`QScreenPlugin` 屏幕驱动插件）
- **`QMouseHandler`**: 鼠标驱动（`QMousePlugin` 鼠标驱动插件）
- **`QKeyboardHandler`**: 键盘驱动（`QKbdDriverPlugin` 键盘驱动插件）
- **`QInputMethod`**: 输入方法
- **`QDecoration`**: 窗口装饰样式（`QDecorationPlugin` 窗口样式插件）

要获取预定义的驱动程序、输入方法和窗口装饰样式列表，请带 `-help` 选项运行 `configure` 脚本。
