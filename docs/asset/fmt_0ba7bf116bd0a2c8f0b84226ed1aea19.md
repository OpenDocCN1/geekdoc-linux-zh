
```
Toplevel::Toplevel(const wxString& title,
    const wxPoint& pos, const wxSize& size)
    : wxFrame(wxFrame=NULL, -1, title, pos, size)
```

```
wxBoxSizer *topSizer =
    new wxBoxSizer(wxHORIZONTAL);
```

```
wxMenu *menuFile = new wxMenu;
```

```
menuFile->Append(ID_About, _T("About..."));
menuFile->AppendSeparator();
menuFile->Append(ID_Quit, _T("Quit"));
```

```
wxMenuBar *menuBar = new wxMenuBar;
menuBar->Append(menuFile, _T("File"));
```

```
SetMenuBar(menuBar);
```

```
DrawingArea->drawing = new DrawingArea(this);
```

```
topSizer->Add(drawing, 1, wxEXPAND | wxALL, 0);
```

```
wxBoxSizer *controlSizer =
    new wxBoxSizer(wxVERTICAL);
```

```
topSizer->Add(controlSizer, 0,
wxEXPAND | wxALL, 5);
```

```
wxSize size(200,100);
slider = new wxSlider(this,
ID_RADIUS_SLIDER, 50, 0, 100,
wxDefaultPosition, size, wxLABELS);
```

```
controlSizer->Add(slider, 0,
wxALL, 5);
```

```
wxBoxSizer *colorSizer =
    new wxBoxSizer(wxVERTICAL);
```

```
controlSizer->Add(colorSizer, 0,
EXPAND | wxALL, 5);
```

```
redCheckbox = new wxCheckbox(this,
ID_RED_CHECKBOX, "Red");
greenCheckbox = new wxCheckbox(this,
ID_GREEN_CHECKBOX, "Green");
blueCheckbox = new wxCheckbox(this,
ID_BLUE_CHECKBOX, "Blue");
```

```
colorSizer->Add(redCheckbox, 0, wxALL, 5);
colorSizer->Add(greenCheckbox, 0, wxALL, 5);
colorSizer->Add(blueCheckbox, 0, wxALL, 5);
```

```
applyButton = new wxButton(this,
ID_COLOR_APPLY, "Apply");
```

```
colorSizer->Add(applyButton, 0,
ALIGN_CENTER | wxALL, 5);
```

```
SetSizer(topSizer);
```

上述更改的结果在原理上与将第二个 `DrawingArea` 控件添加到 `TopLevel` 的水平 sizer 时不同。我们用一个垂直 sizer（命名为 `controlSizer`）替换了第二个 `DrawingArea` 控件。它是 sizer 管理的第二个子控件。控件的内容对于 sizer 而言并不重要，sizer 需要子控件的大小以便正确计算布局。你可能会奇怪为什么为 `wxSlider` 实例指定了大小。似乎 Gtk 版本的 wxWidgets 在报告给 sizer 时存在 bug。以下是 `SetRadiusPercent()` 和 `GetRadiusPercent()` 成员函数的实现。`GetRadiusPercent()` 从 `DrawingArea::OnPaint()` 调用以检索半径百分比，如下：

```
class DrawingArea : public wxWindow
{
public:

    void SetRadiusPercent(int percent)
    {
        m_percent = percent; Refresh();
    }
    int GetRadiusPercent() { return m_percent; }
private:

    int m_percent;
};
```

红、绿蓝复选框通过 `EVT_CHECKBOX(id, func)` 宏连接到回调函数。在这些回调函数中，会调用 `DrawingArea` 对象以告知颜色值；如果勾选，颜色值设为 255，如果取消勾选，则设为 0。需要一些代码更改来支持这一点。首先，我们必须在 `DrawingArea` 中添加成员变量来存储复选框的值，我们还需要定义 setter 和 getter 函数分别设置和读取这些值：

```
class DrawingArea : public wx
{
public:
...
    void SetRed(int value) { m_red = value; }
    void SetGreen(int value) { m_green = value; }
    void SetBlue(int value) { m_blue = value; }

    int GetRed() { return m_red; }
    int GetGreen() { return m_green; }
    int GetBlue() { return m_blue; }
private:

    int m_red;
    int m_green;
    int m_blue;
};
```

接下来，事件表需要映射到 `Toplevel` 中处理这些事件的成员函数：

# 390 第 8 章 wxWidgets

```
BEGIN_EVENT_TABLE(Toplevel, wxFrame)
...
EVT_CHECKBOX(ID_RED_CHECKBOX, Toplevel::OnRed)
EVT_CHECKBOX(ID_GREEN_CHECKBOX, Toplevel::OnGreen)
EVT_CHECKBOX(ID_BLUE_CHECKBOX, Toplevel::OnBlue)
...
END_EVENT_TABLE()
```

这些函数的实现非常直观。使用 `IsChecked()` 函数判断对应颜色复选框是否被勾选。调用对应颜色的 setter 函数；如果复选框被勾选，颜色值将设为强度（255）；否则，将其设为 0：

```
void Toplevel::OnRed(wxCommandEvent& event)
{
    m_drawing->SetRed(event.IsChecked() ? 255 : 0);
}
```

```
void Toplevel::OnGreen(wxCommandEvent& event)
{
    m_drawing->SetGreen(event.IsChecked() ? 255 : 0);
}
```

```
void Toplevel::OnBlue(wxCommandEvent& event)
{
    m_drawing->SetBlue(event.IsChecked() ? 255 : 0);
}
```

最后，`Apply` 按钮通过 `EVT_BUTTON(id, func)` 宏连接到其回调函数；在回调函数中，我们只需调用 `wxWindow::Refresh()` 导致 `DrawingArea` 的 `OnPaint()` 函数被调用：

```
void Toplevel::OnApply(wxCommandEvent& event)
{
m_drawing->Refresh();
}
```

现在我们只需要查看 `DrawingArea` 构造函数中的代码。`OnPaint()` 函数中唯一更改是需要检索半径和颜色值用于绘制圆。我们还需要更改 `DrawingArea` 构造函数以提供初始化

用于半径百分比 (`m_percent`) 和颜色成员变量。对 DrawingArea 的更改在下面的列表中以**粗体**显示：

```cpp
#include "wx/wx.h"
#include "drawing.h"
```

```cpp
BEGIN_EVENT_TABLE(DrawingArea, wxWindow)
EVT_PAINT(DrawingArea::OnPaint)
END_EVENT_TABLE()
```
