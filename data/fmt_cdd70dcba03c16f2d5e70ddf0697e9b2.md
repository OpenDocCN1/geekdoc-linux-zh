
```cpp
#ifndef __PASSWORD_ENTRY_DIALOG_H
#define __PASSWORD_ENTRY_DIALOG_H

#include "wx/wx.h"

class PasswordEntryDialog: public wxDialog
{
public:
    PasswordEntryDialog(wxWindow *parent,
        bool showConfirm = false,
        const wxString& caption =
            "Enter username and password",
        long style = wxOK | wxCANCEL | wxCENTRE,
        const wxPoint& pos = wxDefaultPosition);
    wxString GetUsername();
    wxString GetPassword();
    wxString GetConfirm();
private:
    void OnOK(wxCommandEvent event);
    void OnCancel(wxCommandEvent event);

    wxTextCtrl *m_usernameEntry;
    wxTextCtrl *m_passwordEntry;
    wxTextCtrl *m_confirmEntry;
    bool m_showConfirm;

DECLARE_EVENT_TABLE())
};
#endif
```

从上述列表中可以提取的重要要点是对 `wxDialog` 的继承，以及包含 `DECLARE_EVENT_TABLE()` 宏，该宏是必要的，以便我们将 UI 中的 OK 和取消按钮映射到回调函数 `OnOK()` 和 `OnCancel()`。

让我们来看看这些回调函数的实现，因为我们必须在这些回调中实现预期的模态对话框行为：

```cpp
void
PasswordEntryDialog::onOK(wxCommandEvent& event)
{
    if (IsModal() == true)
      EndModal(wxID_OK);
}
```

```cpp
void
PasswordEntryDialog::OnCancel(wxCommandEvent& event)
{
    if (IsModal() == true)
      EndModal(wxID_CANCEL);
}
```

`EndModal()` 是一个 `wxDialog` 方法，用于关闭模态对话框并导致 `ShowModal()` 返回。`EndModal()` 的参数指定了 `ShowModal()` 的返回值；它可以是任何 int 值，通常是模态对话框显示的按钮的 ID。返回 `wxID_OK` 和 `wxID_CANCEL` 而不是类特定的值，是因为这些值通常是程序期望映射到确定和取消按钮的值。然而，我使用了在 `PasswordEntryDialog` 源文件中声明的枚举中定义的 ID 值，以便确保我所使用的值是唯一的，并且不会与 `wxID_OK` 和 `wxID_CANCEL` 的值冲突（这些值应该被应用程序视为不透明的）。

模态对话框基本上就这些了。总结一下，记住以下几点：

- 模态对话框必须继承自 `wxDialog`。
- 从 `OnOK()` 或 `OnCancel()` 回调调用 `EndModal()` 来关闭对话框，传递一个 `int` 参数，供 `ShowModal()` 的调用者用于判断操作。
- 应用程序程序员将期望 `ShowModal()` 返回 `wxID_OK` 和 `wxID_CANCEL` 值（如果对话框有确定或取消按钮），因此安排 `ShowModal()` 返回这些值是一个好主意，但注意不要使用这些 ID 来定义对话框中的项，因为使用这些常量可能会导致逻辑错误。

# 非模态对话框

现在我们已经解决了模态对话框的问题，让我们关注非模态对话框。就像有些时候使用模态对话框是有意义的，有些时候使用模态对话框会限制应用程序的可用性。考虑图 8-7 所示的 GIMP 图层对话框。GIMP 图层对话框为用户提供了一组用于操作图像图层的控件。GIMP 图层对话框在留在桌面上时最有效——如果每次需要图层对话框来点击按钮或选择菜单项时，图层对话框在显示时都会占据输入焦点且不允许其他操作，那么应用程序的可用性将显著降低。由于这种情况下，从可用性的角度来看，让图层对话框是非模态的。

![](img/77f4289c07bd5e9ee38271501965d2e4_425_0.png)

图 8-7 GIMP 中的非模态对话框

# 使用非模态对话框

作为创建和使用非模态对话框的简单示例，让我们通过复选框（前文所示）修改顶层应用程序（图 8-8）。

![](img/77f4289c07bd5e9ee38271501965d2e4_426_0.png)

图 8-8 非模态对话框

需要一个继承自 `wxDialog` 的类 `ColorDialog`：

```cpp
#ifndef __COLOR_DIALOG_H
#define __COLOR_DIALOG_H

#include "wx/wx.h"

class DrawingArea;

class ColorDialog: public wxDialog
{
public:
    ColorDialog(wxWindow *parent, const wxString& title, const wxPoint& pos, const wxSize& size, DrawingArea *drawing);
    void OnRed(wxCommandEvent event);
    void OnGreen(wxCommandEvent event);
    void OnBlue(wxCommandEvent event);
    void OnApply(wxCommandEvent event);

    DECLARE_EVENT_TABLE())
};
#endif
```

# wx Widgets

该类的大部分由用户与对话框交互时调用的回调组成。`OnRed()`、`OnGreen()` 和 `OnBlue()` 在用户点击红色、绿色和蓝色框时分别调用，每个复选框的当前状态存储在 `ColorDialog` 的变量中：

```cpp
void ColorDialog::OnRed(wxCommandEvent& event)
{
    m_red = (event.IsChecked() ? 255 : 0);
}
```

```cpp
void ColorDialog::OnGreen(wxCommandEvent& event)
{
    m_green = (event.IsChecked() ? 255 : 0);
}
```

```cpp
void ColorDialog::OnBlue(wxCommandEvent& event)
{
    m_blue = (event.IsChecked() ? 255 : 0);
}
```

当用户点击应用按钮时，会调用 `DrawingArea` 控件上的方法来设置颜色，并调用 `DrawingArea` 的 `Refresh()` 方法以用新的填充颜色重新绘制圆形：

```cpp
void ColorDialog::OnApply(wxCommandEvent& event)
{
    m_drawing->SetRed(m_red);
    m_drawing->SetGreen(m_green);
    m_drawing->SetBlue(m_blue);
    m_drawing->Refresh();
}
```

上述内容让人想起我们在处理对话框时经常遇到的一种模式，无论是模态还是非模态。创建和管理对话框的类（在本例中为 `ColorDialog`）维护用户进行的所有更改，但在用户点击确定按钮（或等效按钮）“接受”对话框之前，不对这些更改进行操作。在 `OnApply()` 回调中，我们通过 `ColorDialogEntry` 中维护的 `DrawingArea` 实例指针将更改推送到。然而，

# 402

# 第 8 章 wxWidgets
