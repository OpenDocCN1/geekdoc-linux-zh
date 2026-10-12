
```
PenguinApp.setMainWindow(Editor);

Editor->show();

Voice.say(Editor->text());

PenguinApp.exec();

}
```

列表 9-2 中的程序由四个主要对象组成。`KApplication`、`KClipboard` 和 `KEdit` 是框架类。`Voice` 是集合对象。`Voice` 对象使用了 Festival 文本转语音系统。

> 注意 Festival 是爱堡大学开发的文本转语音系统，适用于 Linux。

`KApplication` 类是 KDE 应用程序的基类。`KApplication` 类提供了简单的 X Windows 骨架。`KEdit` 类是一个简单的编辑器。`KClipboard` 类封装了 X Windows 系统剪贴板。注意框架类在列表 9-2 中执行了大部分工作。`KEdit` 类 `Editor` 通过向 `Clipboard` 对象发送消息从系统剪贴板获取文本：

```
Editor->setText(Clipboard.text());
```

`Clipboard` 对象接收消息并使用其 `text()` 方法返回系统剪贴板上的文本。`Editor` 对象使用其 `setText()` 方法将文本插入到其编辑区域。由于编辑器是主部件，文本被放在屏幕上。一旦编辑器对象从剪贴板对象（`Clipboard`）接收到文本，它就会通过调用 Voice 的 `say()` 方法向 Voice 合组发送消息：

```
Voice.say(Editor->text());
```

该语句：

```
Editor->setText(Clipboard.text());
```

是 `KEdit` 对象与 `KClipboard` 对象之间的连接。这些对象属于应用程序框架类。该语句：

```
Voice.say(Editor->text());
```

是 `KEdit` 对象与 `Voice` 对象之间的连接。在这种情况下，`Voice` 对象是合组的一部分。该语句导致 `Voice` 对象读取剪贴板上的任何文本。方法调用是将应用程序框架连接到合组的简单方法。包图显示 `Voice` 对象与 K 应用程序类 `KApplication`、`KEdit` 或 `KClipboard` 无关。

![](img/859df50987094e32dd2f5bb576f82bce_302_0.png)

**图 9-4：** 显示 `KApplication`、`KEdit`、`KClipboard` 和 `Voice` 的包图。

`Voice` 对象与 `KApplication` 类无关这一事实非常重要，因为这表明合组不需要通过继承或包含与应用程序框架相关。`Voice` 对象存在于应用程序框架对象之外，它们通过方法调用（对象消息传递）进行通信。这种技术并不总是有效。有时，应用程序框架类与合组之间需要进行更多交互。程序员可能需要对合组与框架之间的交互顺序有更强的控制力。

例如，列表 9-2 中的程序使用一个名为 `Voice` 的文本对象来读取系统剪贴板上的任何内容。在 `PenguinApp` 调度其 `exec()` 方法之前，消息被发送到 `Voice` 对象以读取文本。这导致 `Voice` 对象在主窗口出现之前开始读取剪贴板内容。这意味着用户在看到剪贴板的同时，文本显示应该同时发生。如果我们无法让这些事件同时发生，那么至少，我们希望在听到文本之前看到来自剪贴板的文本。

在列表 9-2 的示例中，文本在被看到之前就被读取了。在实际应用程序中，这是不可接受的。框架和合组之间需要更多的控制。我们可以将应用程序拆分为线程或子进程，并使用互斥锁或信号量来解决问题，但在这种情况下，信号和槽（signals and slots）提供了一种控制合组与框架之间交互顺序的简单方法。

方法调用（对象消息传递）允许框架与合组之间完全独立，而信号和槽机制要求合组中的至少一个类派生自 `QObject`。这允许合组发送和接收信号。在此背景下，信号和消息不是一回事。消息是请求对象执行其一个方法的方法。信号是 X Windows 分发器向一个或多个注册为接收者的对象的广播。为了使信号生效，需要使用 `object::connect()` 或 `connect()` 函数建立信号与接收者之间的连接。对象消息传递的方法调用技术不涉及 `QObject::connect()` 或 `connect()` 函数。`connect()` 函数建立了发送者与接收者之间的连接：

```
connect(sender, SIGNAL(doThis()), receiver, SLOT(doThis()));
```

这里，发送者有一个名为 `doThis()` 的方法，接收者有一个名为 `done()` 的方法。`connect` 语句建立了这两个对象之间的通信，每当发送者发送 `doThis()` 信号时，接收者的 `done()` 方法就会被执行。注意的是，`connect` 语句并没有立即调用 `doThis()` 或 `done()` 函数进行执行。`connect` 语句只是建立了一个通信链路。`doThis()` 和 `done()` 方法将在程序执行期间响应某些用户操作时被调用。

## 第 9 章 应用程序框架：深入观察

使用信号和槽方法解决了列表 9-2 程序中的问题。我们可以在应用程序进入事件循环之前，在 `KEdit` 对象和 `Voice` 对象之间建立连接。应用程序在执行 `exec()` 方法之前进入事件循环。一旦连接建立，`KEdit` 对象就可以向 `Voice` 对象发送信号，以从剪贴板读取信息。`KEdit` 对象可以在更新了其编辑区域后发送此信号。信号和槽机制允许我们在准备好之前延迟调用 `Voice.say()` 方法。然而，还存在一些我们将不会涉及的时机问题。

为了建立一个我们对信号和槽具有完全控制权的 `KEdit` 对象，我们需要通过继承从 `KMainWindow` 派生一个新类。这将允许我们定义任何需要的信号和槽。新类将命名为 `k_clipboardReader`，声明如下：

```
class k_clipboardReader : public KMainWindow(

Q_OBJECT

public:

    k_clipboardReader();

    ~k_clipboardReader();

signals:

    void clipboardText(char *X);

public slots:

    void clipboardQuit(void);

    void clipboardRead(void);

private:

    KClipboard clipboard;

    KEdit *clipboardView;

    QpopupMenu *menu;

}
```

`k_clipboardReader` 类将 `clipboardText(char *X)` 声明为信号。此方法将用于与 `Voice` 对象通信。注意 `k_clipboardReader` 类还包含一个 `KClipboard` 对象、一个 `KEdit` 对象和一个 `QPopupMenu` 对象。

### 列表 9-3 (继续)

```cpp
k_clipboardReader::~k_clipboardReader(void)
{
    delete ClipboardView;
    delete MainMenu;
}
```

```cpp
void k_clipboardReader::clipboardQuit(void)
{
    close();
}
```

```cpp
void k_clipboardReader::clipboardRead(void)
{
    ClipboardView->setText(Clipboard.text());
    ClipboardView->repaint();
    qApp->syncX();
    emit(clipboardText(ClipboardView->text()));
}
```

`Voice` 对象可以接收信号，因为它被声明为 `QObject` 的派类。`voice` 类需要派自 `QObject` 才能接收信号。我们建议在设置接收信号的类时使用继承。而不是修改 `voice`，我们创建一个继承自 `voice` 和 `QObject` 的新类。这种技术通过添加一个中间类，维持了整体（ensemble）与框架（framework）的分离。在这种情况下，新类命名为 `voice_interface`，定义如下：

```cpp
class voice_interface : public QObject, public voice{
    Q_OBJECT

public:

    voice_interface(void);

    public slots:

        void sayText(char *X);

}
```
