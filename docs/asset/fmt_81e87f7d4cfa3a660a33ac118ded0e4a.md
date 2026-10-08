
- `_Q_OS_BSDI`
- `_Q_OS_IRIX`
- `_Q_OS_OSF`
- `_Q_OS_UNIXWARE`
- `_Q_OS_CYGWIN`
- `_Q_OS_LINUX`
- `_Q_OS_QNX6`
- `_Q_OS_WIN32`
- `_Q_OS_DUGX`
- `_Q_OS_LYNX`
- `_Q_OS_QNX`
- `_Q_OS_RELANT`
- `_Q_OS_FREEBSD`
- `_Q_OS_NETBSD`
- `_Q_OS_SCO`

我们可以假设这些符号中至少有一个定义。为了方便起见，当检测到 Win32 或 Win64 时，Qt 还会定义 `_Q_OS_WIN`，检测到 Unix 时定义 `_Q_OS_UN`。在运行时，我们可以通过这些符号来区分不同的操作系统。

## 在 Windows 上使用 ActiveX

![](img/34bd675de80edd220dc2d53b429caf78_438_0.png)

**图 20.4.** `QAxContainer` 模块的继承树

COM 数据类型会自动转换为对应的 Qt 类型，如图 20.5 所示。例如，类型为 `VARIANT_BOOL` 的输入参数变为 `bool`，而类型为 `VARIANT_BOOL` 的输出参数变为 `bool &`。如果结果类型是 Qt 类（如 `QString`、`DateTime` 等），则输入参数为常量引用（例如 `const QString &`）。

| COM 类型 | Qt 类型 |
|---|---|
| `VARIANT_BOOL` | `bool` |
| `char`, `short`, `int`, `long` | `int` |
| `unsigned char`, `unsigned short`, `unsigned int`, `unsigned long` | `uint` |
| `float`, `double` | `double` |
| `CYLONG` | `long`, `qulong` |
| `BSTR` | `QString` |
| `DATE` | `QDateTime`, `QDate`, `QTime` |
| `OLE_COLOR` | `QColor` |
| `SAFEARRAY (VARIANT)` | `QList<QVariant>` |
| `SAFEARRAY (BSTR)` | `QStringList` |
| `SAFEARRAY (BYTE)` | `QByteArray` |
| `VARIANT` | `QVariant` |
| `IFontDesc` | `IFont` |
| `IPictureDisp` | `QPixmap` |
| `User defined type` | `QRect`, `QSize`, `QPoint` |

**图 20.5.** COM 类型与 Qt 类型之间的关系

要获取 `QAxObject` 或 `QAxWidget` 中所有可用属性、信号和槽，调用 `QAxBase::generateDocumentation()` 或使用 Qt 的 `dumpdoc` 工具，它位于 `tools\qt\dumpdoc` 目录。

让我们继续 `PlayerWindow` 构造函数：

```
wmp->setProperty("ShowControls", false);
wmp->setSizePolicy(QSize::Expanding, QSize::Expanding);
```

## 422 平台特定特性

```
connect(wmp, SIGNAL(PlayStateChange(int, int)), this, SLOT(onPlayStateChange(int, int)));
connect(wmp, SIGNAL(ReadyStateChange(ReadyStateConstants)), this, SLOT(onReadyStateChange(ReadyStateConstants)));
connect(wmp, SIGNAL(PositionChange(double, double)), this, SLOT(onPositionChange(double, double)));
```

在调用 `QWidget::setControl()` 后，我们调用 `QObject::setProperty()` 将 Windows Media Player 的 `ShowControls` 属性设置为 false，因为我们有自己的按钮来控制。`QObject::setProperty()` 可用于 COM 属性和 Qt 属性。它的第二个参数是 `Variant`。

接下来，我们调用 `setLayoutPolicy()` 让 ActiveX 控件占据所有可用空间，并将 COM 事件连接到槽。

```
stopButton = new QPushButton;
stopButton->setText(tr("&Stop"));
stopButton->setEnabled(false);
connect(stopButton, SIGNAL(clicked()), wmp, SLOT(Stop()));
```

`PlayerWindow` 的其余部分遵循通常模式，连接某些信号到 COM 对象提供的槽（`Play()`、`Stop()`）。由于我们只显示了 Stop 按钮的实现。

让我们创建构造函数并查看 `timerEvent()` 函数：

```
void PlayerWindow::timerEvent(QEvent *event)
{
	if (event->timerId() == updateTimer) {
	double curPos = wmp->property("CurrentPosition").toDouble();
	onPositionChange(-1, curPos);
	} else {
	QObject::timerEvent(event);
	}
}
```

`timerEvent()` 函数在媒体片段播放期间定期调用。我们使用它来更新滑块。这是通过调用 ActiveX 控件上的 `property()` 获取 `CurrentPosition` 属性的 `QVariant` 值，并调用 `toDouble()` 将其转换为 `double` 实现的。我们还调用 `onPositionChange()` 执行更新。

我们将不再回顾代码的其他部分，因为大部分与 ActiveX 无关。代码包含在 CD。

在 `.pro` 文件中，我们需要此项来链接 `QAContainer` 模块：

## 在 Windows 上使用 ActiveX

```
CONFIG += qaxcontainer
```

处理 COM 对象时的一个频繁需求可以直接调用 COM 方法（而不是连接 Qt 信号）。最简单的方法是调用 `QAxBase::dynamicCall()`，将方法的名称和签名作为第一个参数，并将方法的参数作为额外参数。例如：

```
wmp->dynamicCall("Play(uint)", 6);
```

`dynamicCall()` 函数接受最多八个 `QVariant` 参数并返回一个 `QVariant`。如果我们需要这种方式传递 `IDispatch` 或 `IUnknown*`，可以将组件封装在 `QAxObject` 中并对其调用 `variant()` 将其转换为 `QVariant`。如果我们需要调用返回 `IDispatch` 或 `IUnknown` 的 COM 方法，或者我们需要访问这些类型之一的 COM 属性，使用 `querySubObject()`：

```
QAxObject *session = outlook.querySubObject("Session");
QAxObject *defaultContacts = session->querySubObject("GetDefaultFolder(DefaultFolders)");
```

如果我们想调用参数中有不支持的数据类型的方法，使用 `QAxBase::queryInterface()` 获取 COM 接口并直接调用方法。与 COM 通常一样，在完成接口后必须调用 `Release()`。如果经常需要调用此类方法，可以派生 `QAxObject` 并提供封装 COM 接口的成员函数。请注意，`QAxObject` 和 `QWidget` 子类不能定义自己的属性、信号或槽。

我们现在回顾 `QAxServer` 模块。该模块允许我们将一个标准的 Qt 程序转换为 ActiveX 服务器。服务器可以是共享库，也可以是独立应用程序。构建为库的服务器通常称为进程内服务器；独立应用程序称为进程外进程。

我们的第一个 `QAxServer` 示例是一个进程内服务器，提供了一个显示球左右跳动的小部件。我们还将看到如何在 Internet Explorer 中嵌入该控件。

这里是 `AxBouncer` 控件类定义的开头：

```
class AxBouncer : public QWidget, public QAxBindable\{
    Q_OBJECT
    Q_ENUM(SpeedValue)
    Q_PROPERTY(QColor color READ WRITE setColor)
    Q_PROPERTY(SpeedValue speed READ WRITE setSpeed)
    Q_PROPERTY(int radius READ WRITE setRadius)
    Q_PROPERTY(bool running READ isRunning)
}
```

`AxBouncer` 同时继承自 `QWidget` 和 `QAxBindable`。`QAxBindable` 类提供了控件与 ActiveX 客户端之间的接口。任何 `QWidget` 都可以导出为 ActiveX 控件，但通过派生 `QAxBindable`，我们可以在属性值变化时通知客户端，并实现 COM 接口来补充 QServer 已经实现的接口。

![](img/34bd675de80edd220dc2d53b429caf78_441_0.png)

**图 20.6.** Internet Explorer 中的 AxBouncer 控件

在进行涉及 `QObject` 类的多重继承时，我们必须将 `QObject` 派生类放在第一个，以便 moc 识别它。

我们声明了三个读写属性和一个只读属性。`Q_ENUM` 宏告诉 moc `SpeedValue` 类型是一个枚举。该枚举定义在类的公共部分：

```
public:
    enum SpeedValue { Slow, Normal, Fast };
    AxBouncer(QWidget *parent = 0);
    void setSpeed(SpeedValue newSpeed);
    SpeedValue speed() const { return ballSpeed; }
    void setRadius(int newRadius);
    int radius() const { return ballRadius; }
    void setColor(const QColor &newColor);
    bool isRunning() const { return myTimerId != 0; }
    QSize sizeHint(int) const;
    QAxAggregated *createAggregate();
```

## 在 Windows 上使用 ActiveX

```
public slots:
    void start();
    void stop();
```

```
signals:
    void bouncing();
```

`AxBouncer` 构造函数是控件的标准构造函数，带有一个父参数。`QAXFACTORY_DEFAULT()` 宏（我们将使用它来导出组件）期望一个具有此签名的构造函数。

`createAggregate()` 函数是从 `QAxBindable` 重写的。我们将在 `main` 中解释它。

```
protected:
    void paintEvent(QPaint *event);
    void timerEvent(QTimer *event);
```

```
private:
    int intervalInMilliseconds const;

    QColor ballColor;
    SpeedValue ballSpeed;
    int ballRadius;
    int myTimer;
    int x;
    int delta;
;
```

`AxBouncer` 构造函数初始化了类的私有变量。

类的保护和私有部分与我们假设这是一个标准 Qt 控件时是一样的。

```
AxBouncer::AxBouncer(QWidget *parent)
: QWidget(parent)
{
ballColor = Qt::blue;
ballSpeed = Normal;
ballRadius = 15;
myTimer = 0;
x = 
delta = 2;
}
```

## 426 20. 平台特定特性

不寻常之处在于对 `requestPropertyChange()` 和 `propertyChanged()` 的调用。这些函数继承自 `QAxbindable`，理想情况下，每当我们更改属性时都应该调用它们。`requestPropertyChange()` 请求客户端更改属性的权限，如果客户端允许更改，则返回 `true`。`propertyChanged()` 函数通知客户端属性已更改。

`setSpeed()` 和 `setRadius()` 设置器也遵循这一模式，并且 `start()` 和 `stop()` 槽也是如此，因为它们改变了运行中属性的值。

仅剩下一个 `AxBouncer` 接口成员函数：

```
QAxAggregated *AxBouncer::createAggregate() {
    return new ObjectSafetyImpl();
}
```

`createAggregate()` 函数是从 `QAxbindable` 重新实现的。它允许我们实现 `QIServer` 模块尚未实现的 COM 接口，或者绕过 `QIServer` 的默认 COM 接口。在这里，我们这样做是为了提供 `IObjectSafety` 接口，Internet Explorer 使用它来访问组件的安全选项。这是消除 Internet Explorer 臭名昭昭的“对象对脚本不安全”错误消息的标准技巧。

是实现 `IObjectSafety` 接口的类的定义：

```cpp
class ObjectSafetyImpl : public QAxAggregated, public IObjectSafety
public:
    long queryInterface(const QUuid &iid, void **iface);

    QAXAGG_UNKNOWN

    HRESULT WINAPI GetSafetyOptions(REFIID riid,
        DWORD *dwSupportedOptions, DWORD *dwEnabledOptions);
    HRESULT WINAPI SetSafetyOptions(REFIID riid,
        DWORD dwSupportedOptions, DWORD *dwEnabledOptions);
```

`ObjectSafetyImpl` 同时继承了 `QAxAggregated` 和 `IObjectSafety`。`QAxAggregated` 是一个用于额外 COM 接口实现的抽象类。`QAxAggregated` 扩展的 COM 对象可以通过 `controllingIUnknown()` 访问。该 COM 对象由 `QAxServer` 模块在后台创建。

`QAXAGG_UNKNOWN` 提供了 `Interface()`、`AddRef()` 和 `Release()` 的标准实现。这些实现仅仅是在控制的 COM 对象上调用相同的函数。

```cpp
long ObjectSafetyImpl::queryInterface(const QUuid &iid, void **iface)
{
    if (*iid == IID_IUnknown) //
    if (iid == IID_IObjectSafe) {
        *iface = static_cast<IObjectSafety *>(this);
    } else {
        return E_NOINTERFACE;
    }
    AddRef();
    return S_OK;
}
```

`queryInterface` 函数是 `QAxAggregated` 的纯虚函数。它由控制 COM 对象调用，以便访问 `QAxAggregated` 子类提供的接口。对于我们没有实现的接口以及 `IUnknown`，我们必须返回 `E_NOINTERFACE`。

```cpp
HRESULT WINAPI ObjectSafetyImpl::InterfaceSafetyOptions(
    /* rid */, DWORD *pddwSupportedOptions,
    DWORD *pddwEnabledOptions)
{
    *pddwSupportedOptions = INTERFACESAFE_FOR_UNTRUSTED_DATA
    | INTERFACESAFE_FOR_UNTRUSTED_CALLER;
    *pddwEnabledOptions = *pddwSupportedOptions;
    return S_OK;
}
```
