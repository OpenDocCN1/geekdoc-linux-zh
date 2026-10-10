
`IMPLEMENT_APP` 宏也定义了应用程序的 `main()` 函数。

## 应用程序主窗口

现在让我们仔细观察 `OnInit()`。再次，这个要求的函数是你实现应用程序主窗口的地方。这里是来自“Hello World”应用程序中 `OnInit()` 的完整版本：

`MyFrame` 是由应用程序定义的继承自 `wxFrame` 的类。`MyFrame` 构造函数接受三个参数：窗口标题、窗口在屏幕上的初始位置以及窗口的初始大小。在主窗口构造完成后，调用 `Show()` 方法显示它，并返回 `TRUE` 让 wxWidgets 知道一切按计划进行。如前所述，返回 `FALSE` 会导致 wxWidgets 退出应用程序。以下是 `MyFrame` 类的声明：

```cpp
class MyFrame : public wxFrame
{
public:
    MyFrame(const wxString& title, const wxPoint& pos, const wxSize& size);
};
```

再次，构造函数接受窗口标题、窗口的 x 位置和其大小作为参数。构造函数的定义如下：

```cpp
MyFrame::MyFrame(const wxString& title, const wxPoint& pos, const wxSize& size)
    : wxFrame(wx_NULL, -1, title, pos, size)
{
    wxBoxSizer *topsizer = new wxBoxSizer(wxHORIZONTAL);
    wxBoxSizer *versizer = new wxBoxSizer(wxVERTICAL);
    wxStaticText *text = new wxStaticText(this, -1, T("Hello World!"));
    topsizer->Add(versizer, 1, wxALIGN_CENTER | wxALL, 10);
    versizer->Add(text, 1, wxALIGN_CENTER | wxALL, 10);
    SetSizer(topsizer);
}
```

这就是“Hello World”应用程序所有复杂度实现的地方。注意 `wxFrame` 的初始化。它的构造函数定义如下：

```cpp
wxFrame(wxWindow window= parent, wxWindowID id, const wxString& title, const wxPoint& pos = wxDefaultPosition, const wxSize& size = wxDefaultSize, long style = wxDEFAULT_FRAME_STYLE, const wxString& name = "frame");
```

注意，构造函数的前三个参数实际上是必须的，因为其余参数具有默认初始化。构造函数参数反映了一个设计决策，允许父窗口覆盖窗口的位置和大小；父窗口虽然没有默认初始化器支持，但始终为 `NULL`；并且应用程序不关心帧的样式，也不包含它被分配的 ID 或名称。

`MyFrame` 构造函数的大部分职责是定义帧的内容和布局。如前所述，内容是一个值为“Hello World!”的文本字符串，布局由两个 size（一个垂直，一个水平）管理，以实现在帧中居中“Hello World!”的预期效果。让我们逐步构建该函数的实现过程，从创建静态文本开始，移动到帧本身的布局。

静态文本理然地通过 `wxStaticText` 类实现。它的构造函数与 `wxFrame` 几乎相同：

要创建静态文本，在堆上分配一个 `wxStaticText` 实例，如下：

```cpp
wxStaticText *text = new wxStaticText(this, -1, _T("Hello World!"))
```

到目前为止，我们已经了：

```cpp
MyFrame::MyFrame(const wxString& title, const wxPoint& pos, const wxSize& size)
 : wxFrame(wx_NULL, -1, title, pos, size)
{
 wxStaticText *text = new wxStaticText(this, -1, _T("Hello World!"));
}
```

编译并运行此程序后，我们得到了图 8-1 所示的结果。

![](img/77f4289c07bd5e9ee3827150196d2e4_367_0.png)

**图 8-1** wxWidgets “Hello World!”

注意这里的几点。首先，由于静态文本控件由帧的 sizer 管理，当通过 `Show()` 调用 时，它会自动与帧的内容一起显示。因此，没有必要为静态文本控件调用 `Show()`。其次，wxWidgets 确保在帧被销毁时析构静态文本控件；因此，不需要保留文本实例指针来执行显式析构。（你可能由于其他原因（例如更改文本显示）而保留该指针，但并不是应用程序的要求）。

## 342 第 8 章 wxWidgets

```cpp
MyFrame::MyFrame(const wxString& title, const wxPoint& pos, const wxSize& size)
    : wxFrame(wxFrame*NULL, -1, title, pos, size)
{
    wxBoxSizer *topsizer = new wxBoxSizer(wxVERTICAL);
    wxStaticText *text = new wxStaticText(this, -1, "Hello World!");
    topsizer->Add(text, 1, wxALIGN_CENTER | wxALL, 10);
    SetSizer(topsizer);
}
```

布局器（Sizer）与静态文本控件一样是分配在堆上的。`wxBoxSizer` 构造函数的原型非常简单：

```cpp
wxBoxSizer(int orientation);
```

其中 `orientation` 是 `wxHORIZONTAL`（水平）或 `wxVERTICAL`（垂直）。垂直布局器从上到下排列子控件，而水平布局器从左到右排列子控件。`wxStaticText` 控件创建后，通过调用其 `Add()` 函数成为水平布局器的子：

```cpp
topsizer->Add(text, 1, wxALIGN_CENTER | wxALL, 10);
```
