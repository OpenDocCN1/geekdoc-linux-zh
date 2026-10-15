
在本节中，我将引入一个新的文件类型——PO 文件——它包含本地翻译。采用 gettext 的理想时机开发初期，而不是后期。

# 使用 Gettext

要使用 `gettext`，你需要执行以下操作：

1. 将应用程序中的文字字符串替换为符号名称；这些名称将用于索引翻译后的字符串。
2. 使用 `xgettext` 工具创建基准 PO 文件，该工具是 `gettext` 包的一部分。
3. 编辑 PO 文件，为每个项目提供翻译后的字符串。
4. 将 PO 文件编译为随应用程序发布的二进制 MO 文件。
5. 对于支持的每种语言，克隆基准 PO 文件并重复步骤 3 和 4。

步骤 1 涉及为应用程序中的字符串分配符号名称。你应该选择让翻译人员（以及你自己）在 PO 文件中定位字符串的符号名称。以下可以使用并根据需要修改的示例策略。任何符号名称的形式大致为 `class.object.attribute.value`：

- `class` 是使用该字符串的类的名称。
- `object` 非正式地标识使用该字符串的对象。
- `attribute` 是分配该字符串的对象的属性。
- `value` 是不翻译的（基准）字符串，有助于识别翻译字符串的含义。

为了清楚上述内容，确实需要几个例子。让我们看看章节之前介绍的 `Toplevel` 类中包含字符串的部分（字符串**加粗**显示）：

```cpp
Toplevel::Toplevel(const wxString& title,
const wxPoint& pos, const wxSize& size) :
wxFrame(wxFrame *)NULL, -1, title, pos, size)
{
wxBoxSizer *topSizer =
new wxBoxSizer(wxHORIZONTAL);

menuFile = new wxMenu;

menuFile->Append(ID_About, "...");
menuFile->AppendSeparator();
menuFile->Append(ID_Quit, "Quit");

wxMenuBar *menuBar = new wxMenuBar;
menuBar->Append(menuFile, "File");

SetMenuBar(menuBar);
}
```

```cpp
wxMenuBar ~menuBar = new wxMenuBar;
menuBar->Append(menuFile, "&File");
```

```cpp
wxSize dsize(300, 200);
m_colors = new ColorDialog(this, "Set Colors",
wxDefaultPosition, dsize, m_drawing);
```

```cpp
m_colors->Show(TRUE);
```

```cpp
SetSizer(topSizer);
```

```cpp
}
```

```cpp
void
TopLevel::OnAbout(wxCommandEvent& WXUNUSED(event))
{
wxMessageDialog myDlg(this,
"TopLevel wxWidgets Sample",
"About TopLevel",
wxOK | wx_ICON_INFORMATION);
myDlg.ShowModal();
}
```

如表 8-5 所示，`TopLevel` 类使用了六个不同的字面量字符串：

## 表 8-5 TopLevel 类使用的字面量字符串

| 字符串 | 用途 |
| --- | --- |
| &About... | 文件菜单“关于”菜单项标签 |
| &Quit | 文件菜单“退出”菜单项标签 |
| &File | 文件菜单标签 |
| Set Colors | ColorDialog 窗口标题栏标签 |
| TopLevel wxWidgets Sample | “关于”框中显示的消息 |
| About TopLevel | 关于框窗口标题栏标签 |

### 第 8 章 wxWidgets

根据这些字面量字符串及其描述，可以推导出以下符号名称：

- `Toplevel.MenuItem.About.Label`
- `Toplevel.MenuItem.Quit.Label`
- `Toplevel.Menu.File.Label`
- `Toplevel.ColorDialog.TitleBar.Label`
- `Toplevel.AboutBox.Message.Text`
- `Toplevel.AboutBox.TitleBar.Label`

让我们对 `ColorDialog` 类执行相同的操作。在**粗体**部分，是 `colors.cpp` 中包含字面量文本的内容：

```cpp
ColorDialog::ColorDialog(wxWindow *parent,
const wxString& title, const wxPoint& pos,
const wxSize& size, DrawingArea *drawing);
wxDialog(parent, -1, pos, size);
m_drawing(drawing)
{
```

```cpp
wxCheckbox *redCheckbox =
new wxCheckbox(this, ID_RED_CHECKBOX, "Red");
wxCheckbox *greenCheckbox =
new wxCheckbox(this, ID_GREEN_CHECKBOX, "Green");
wxCheckbox *blueCheckbox =
new wxCheckbox(this, ID_BLUE_CHECKBOX, "Blue");
```

```cpp
wxButton *applyButton =
new wxButton(this, ID_COLOR_APPLY, "Apply");
```

从上述源代码可以导出以下可能的符号名称：

- `ColorDialog.Checkbox.Red.Label`
- `ColorDialog.Checkbox.Green.Label`
- `ColorDialog.Checkbox.Blue.Label`
- `ColorDialog.Button.Apply.Label`

## wx Widgets

记住，对于 `gettext` 来说，完全遵循我的建议并不至关重要；唯一要求的是你选择的符号名称是唯一的。你可以自由地设计任何对你和你的应用程序最有意义的策略。但是，当你查看我选择的符号名称时，你应该不仅清楚这些符号名称指代什么，而且清楚你可以在源代码的哪里找到它们。因此，我希望你相信，一个良好的符号名称命名策略是非常重要的，因为它可以极大地提高文件的可读性（和可维护性）。

继续步骤 1，让我们修改源代码以使用这些符号名称。首先是 `toplevel.cpp`：

```cpp
Toplevel::Toplevel(const wxString& title,
const wxPoint& pos, const wxSize& size) :
wxFrame(wxFrame)=NULL, -1, title, pos, size)
{
wxBoxSizer *topSizer =
 wxBoxSizer(wxHORIZONTAL);

wxMenu *menuFile = new wxMenu;

menuFile->Append(ID_About,
_("Toplevel.MenuItem.About.Label"));
menuFile->AppendSeparator();
menuFile->Append(ID_Quit,
_("Toplevel.MenuItem.Quit.Label"));

wxMenuBar *menuBar = new wxMenuBar->Append(menuFile,
_("Toplevel.Menu.File.Label"));
```

```cpp
wxSize dsize(300, 200);
m_colors = new ColorDialog(this,
_("Toplevel.ColorDialog.TitleBar.Label"),
wxDefaultPosition, dsize, m_drawing);
```

```cpp
m_colors->Show(TRUE);
```

```cpp
SetSizer(topSizer);
```

```cpp
}
```

### 第 8 章 wxWidgets
