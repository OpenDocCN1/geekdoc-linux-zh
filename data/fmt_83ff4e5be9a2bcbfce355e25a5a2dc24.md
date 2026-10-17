
`class MyApp: public wxApp`

{

    virtual bool `OnInit()`();

};

```cpp
class MyFrame: public wxFrame

{

public:

    MyFrame(const wxString& title, const wxPoint& pos, const wxSize& size);

    void OnClick(wxCommandEvent& event);

    void OnDoubleClick(wxCommandEvent& event);

private:

    wxButton *m_clickButton;

DECLARE_EVENT_TABLE();

};
```

对 `MyFrame` 类的一个重要修改是引入了名为 `DECLARE_EVENT_TABLE` 的 wxWidgets 宏。事件表是事件分发到应用程序中对象的依据。事件表既支持从底层工具接收的低级事件（如窗口调整大小和鼠标移动），也支持更抽象的事件（如菜单选择和按钮按下）。使用 `DECLARE_EVENT_TABLE` 宏在类中声明事件表是使类成为任一类型事件槽的第一步。以下是 wxWidgets 中 `DECLARE_EVENT_TABLE` 宏的定义：

```cpp
#define DECLARE_EVENT_TABLE() \
protected:
    static const wxEventEntry sm_eventEntries[];
    static const wxEventTable*_eventTable;
    virtual const wxEventTable* GetEventTable() const;
```

让我们详细查看此宏。事件表（`sm_eventTable`）只是包含两个字段的结构体。一个字段指向基类（在本例中为 `wxFrame`）。另一个字段指向 `sm_eventEntries` 成员变量，该变量紧接上方被声明为私有成员变量。当事件进入时（例如，鼠标按下），wxWidgets 使用类提供的 `GetEventTable()` 函数获取该类事件表的指针。注意 `GetEventTable()` 是虚函数；wxWidgets 的期望是 `MyFrame` 将提供一个实现。拿到此表后，wxWidgets 遍历 `sm_eventEntries`，在表中查找实现正在处理的事件的处理程序的元素。如果在表中找到匹配项，wxWidgets 将直接调用该条目中存储的处理函数。如果在表中未找到匹配项，wxWidgets 将通过查看基类的事件表（使用事件表中存储的基类指针）继续搜索处理函数。

如果基类没有提供处理函数，搜索将通过继承层次结构继续。

如果在继承层次中没有找到处理函数，且事件是 `wxCommandEvent` 派生事件（`wxCommandEvent` 已定义），则搜索窗口包含层次结构。窗口包含层次结构表示 wxWidgets 类之间的嵌套关系，`wxButton` 可能是 `wxFrame` 实例的子。如果 `wxButton` 实例（及其父类）没有实现按钮按下的事件处理程序，wxWidgets 将查询 `wxFrame` 实例，如果它处理了该事件，其事件处理程序将被调用。在本节稍后描述的代码正展示了上述的包含层次结构。通过在 `MyFrame`（派自 `wxFrame`）中处理 `wxButton` 事件，我们的代码避免了需要一个派自 `wxButton` 的类，而这在 `wxButton` 级别实现按钮按下事件是需要的。

在继续之前，我需要描述 `wxCommandEvent` 事件。`wxCommandEvent` 是一种抽象事件，对应于涉及控件的操作，例如按下按钮或选择菜单项。不派自 `wxCommandEvent` 的事件对应于系统级事件，例如鼠标移动、键盘按下、窗口调整大小等。大多数应用程序并不关心底层的

## 第8章 wxWidgets

事件，并将大部分精力集中在处理由 `wxCommandEvent` 派生的事件上。在包含层次结构中进行传播仅针对 `wxCommandEvent` 派生事件，这是合逻辑的。只有实现与非 `wxCommandEvent` 事件相关的窗口的控件需要知道该事件。窗口大小被调整或发生低级鼠标事件等，只对创建该窗口的控件感兴趣。它需要决定如何处理该事件；如果处理过程中需要与继承层次结构或类层次结构中的其他控件进行通信，则由处理事件的控件来确保执行所需的任何通信。

接线事件处理程序的第二步是在表中添加条目，以便你希望的每个事件在发生时由 wxWidgets 分发。这是通过在文件作用范围内定义类内部通过 `DECLARE_EVENT_TABLE` 宏所声明的事件表来实现（注意，事件表被声明为静态，因此它需要在类外部进行定义），并为类实例所需的每个事件向表中添加条目。为了定义事件表，wxWidgets 提供了 `BEGIN_EVENT_TABLE` 和 `END_EVENT_TABLE` 宏：

```cpp
#define BEGIN_EVENT_TABLE(theClass, baseClass) \
const wxEventTable::\
&theClass::GetEventTable() const \
{ return &theClass::sm_eventTable; }; \
const wxEventTable theClass::sm_eventTable = \
&baseClass::sm_eventTableEntries[0]}; \
const wxEventTableEntry \
theClass::sm_eventTableEntries[] = {\
```

```cpp
#define END_EVENT_TABLE() DECLARE_EVENT_TABLE_ENTRY(wxNULL, 0, 0, 0, 0, 0);)
```

接下来的代码说明了这些宏的使用：

```cpp
BEGIN_EVENT_TABLE(MyFrame, wxFrame)
EVT_MENU(ID_Quit, MyFrame::OnQuit)
EVT_BUTTON(ID_CLICK_ME, MyFrame::OnClickMe)
END_EVENT_TABLE()
```

`BEGIN_EVENT_TABLE` 宏的第一个参数是处理事件表中列出的事件的具体类名称（`MyFrame`），第二个参数是基类名称（`wxFrame`），如果在事件表中查找具体类时结果为空，则将搜索基类。`END_EVENT_TABLE` 宏通过添加结束标记来终止事件表的定义；当到达此结束标记时，事件表条目的迭代停止。

在 `BEGIN_EVENT_TABLE` 和 `END_EVENT_TABLE` 宏之间，将特定事件映射到由 `MyFrame` 类实现的处理函数。前面的代码说明了这些宏中的两个。第一个 `EVT_MENU` 用于映射菜单项事件，第二个 `EVT_BUTTON` 用于映射 `wxButton` 控件实例的点击事件。这些宏的每个第一个参数是正在指定映射的控件的窗口 ID，第二个参数是事件发生时将要调用的类成员函数的引用。窗口 ID 由应用程序作为实例化控件的函数的参数来指定，正如我稍后演示的那样。窗口 ID 通常来自程序员在同一源文件中（在声明事件表之前）提供的枚举，或者在头文件中：

```cpp
enum
{
    ID_Quit,
    ID_CLICK_ME,
};
```

所使用的值并不重要，除非它们必须是唯一的（并且由于控件不包含其他控件，因此在实践中唯一性不是问题）。

wxWidgets 定义了的一百多个 `EVT_` 宏。在讨论它们支持的控件类时，我会描述其中的许多个。

现在要做的就是为处理函数 `OnClickMe()` 和 `OnQuit()` 提供实现。首先，我们需要继续查看一些源代码。以下几行在本章之前描述的“Hello World”应用程序中应该是熟悉的：

```cpp
IMPLEMENT_APP(MyApp)
bool MyApp::OnInit()
{
    MyFrame *frame = new MyFrame("Click Me Demo", wxPoint(50,50), wxSize(450,340));
    frame->Show(TRUE);
    SetTopWindow(frame);
    return TRUE;
}
```

## 创建用户界面

我们在 `MyFrame` 类的构造函数中创建 UI。我们必须创建的 UI 项目之一是带有标有“Exit”（退出）菜单项的文件菜单。以下代码说明了菜单的创建，这涉及创建 File 菜单（`wxMenu` 的实例）、在 File 菜单上添加 Exit 菜单项、创建一个菜单栏，最后将 File 菜单添加到菜单栏中。最后一步是通过调用 `SetMenuBar()` 使与 `MyFrame` 实例关联的窗口菜单栏激活状态；

```cpp
MyFrame::MyFrame(const wxString& title, const wxPoint& pos, const wxSize& size)
```
