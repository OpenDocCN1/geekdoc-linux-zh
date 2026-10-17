
| `wxCHANGE_DIR` | 将当前目录更改为文件所在的目录。 |

# 433

# wx Widgets

显示文件选择对话框只需创建一个 `wxFileDialog` 实例，调用它的 `ShowModal()` 方法，如果 `ShowModal()` 返回 `wxID_OK`，则检索用户选择的文件（如果是多次选择则为文件）。以下是演示如何使用 `wxFileDialog` 的菜单回调实现。此函数的文件选择对话框允许用户选择 C++ 源文件和头文件，或所有文件。（用户可以通过从下拉框中选择每个文件类型来控制。）示例中的通配符字符串

`"C++ Source Files (*.cpp,*.h)|*.cpp;h|All Files|.*"`包含了两个逻辑部分：一个定义下拉框中 C++ Source Files 项目的标签和掩码，另一个提供 All Files 项目的标签和掩码。上述通配符字符串中的 `|` 字符起着双重作用，它不仅分离了两个通配符组件：

```
C++ Source Files (*.cpp,*.h)|*.cpp;h
```

以及

```
All Files|.*
```

而且在每个组件内部将标签与掩码分离。因此，通配符字符串的通用格式如下：

```
"label-1 | mask-1 | label-2 | mask-2 | label-3 | mask-3 | | label-n | mask-n"
```

虽然 `|` 字符的双重用法初看起来可能会让人困惑，但只需记住以下：

- 通配符字符串的每个组件都通过 `|` 分离。
- 每个组件由标签和掩码组成，它们也通过 `|` 分离。

在下面的列表中，你可以看到如果 `ShowModal()` 返回 `wxID_OK`，我们用户点击了文件选择对话框中的打开按钮。检查样式是否包含 `wxMULT` 的检查是多余的，但如果我们决定从传递给 `wxFileDialog` 构造函数的样式参数中移除该标志，它可以起到保护作用。

# 408

# 第8章 wxWidgets

```cpp
void Toplevel::OnFile(wxCommandEvent& wxUNUSED(event))
{
    char *cwd = ::getcwd(NULL, 0);
    wxFileDialog myFileDialog(this, "Choose a file",
        cwd, "toplevel.cpp",
        "C++ Source Files (*..*)|*.cpp;*.h\nAll Files (*..*)", wxOPEN | wxMULTIPLE);

    if (myFileDialog.ShowModal() == wxID_OK) {
        if (myFileDialog.GetStyle() == wxMULTIPLE) {
            wxArrayString paths;
            wxArrayString files;
            myFileDialog.GetPaths(paths);
            myFileDialog.GetFilenames(files);
            for (int i = 0; i < paths.Count(); i++) {
                printf("%d %s\n", i,
                    paths[i].c_str(),
                    files[i].c_str());
            }
        } else {
            wxString path = myFileDialog.GetPath();
            wxString filename = myFileDialog.GetFilename();
            printf("%s %s\n", path.c_str(),
                filename.c_str());
        }
    }
    free(cwd);
}
```

`wxFileDialog` 提供了两方法用于从 `wxFileDialog` 控件中获取用户选择。如果样式为单选，则使用其中一组：`GetPath()` 返回所选文件的完整路径，而 `GetFilename()` 返回路径中的文件名部分。两者都返回 `wxString` 引用，并可以使用 `wxString::c_str()` 获取 C 风格的字符串。如果样式包含 `wxMULTIPLE`，应该使用 `GetPaths()` 和 `GetFilenames()` 方法，而不是 `GetPath()` 和 `GetFilename()`。这两者都返回一个 `wxArrayString` 对象的引用。上面的列表显示了如何遍历 `wxArrayString` 对象并获取路径和文件名。实验表明，`GetFilenames()` `wxArrayString` 对象的第 $i$ 个条目与 `GetPaths()` 返回的 `wxArrayString` 对象的第 $i$ 个条目对应。例如，如果上一个列表 `paths` 的第二个项是 `/home/myd/main.cpp`，那么 `files` 的第二个项将是 `main.cpp`。

# wxColourDialog

本书讨论的最后一个 wxWidgets 复合控件类是 `wxColourDialog`。`wxColourDialog` 实现了一个特定平台的颜色选择器，如图 8-11 所示在 Mac OS X 上显示的样式。

![](img/77f4289c07bd5e9ee38271501965d2e4_435_0.png)

**图 8-11** `wxColourDialog`

由于 `wxColourDialog` 在某些方面与 `wxFontDialog` 相似；辅助对象（在此情况下为 `wxColorData`）被传递给构造函数以初始化颜色选择器最初显示的颜色；从 `ShowModal()` 返回时，应用程序查询 `wxColorData` 对象的引用，进而可以查询用户选择颜色的 RGB 分量。以下是 `wxColourDialog` 的构造函数：

```cpp
wxColourDialog(wxWindow* parent,
wxColorData* data = NULL);
```

正如我们一直以来所的那样，菜单项回调说明了 `::wxColourDialog` 控件的创建和使用：

```cpp
void TopLevel::OnColor(wxCommandEvent& wxUNUSED(event))
{
    wxColorData* data;
    int red, green, blue;

    red = m_drawing->GetRed();
    green = m_drawing->GetGreen();
    blue = m_drawing->GetBlue();

    wxColor color(red, green, blue);
    data->SetColor(color);
    wxColourDialog myColorDialog(this, &data);

    if (myColorDialog.ShowModal() == wxID_OK)
data = myColorDialog.GetColourData();
color = data.GetColour();
m_drawing->SetRed(color.Red());
m_drawing->SetGreen(color.Green());
m_drawing->SetBlue(color.Blue());
m_drawing->Refresh();
}
```

上述列表的几行代码从 `DrawingArea` 控件提取当前的填充颜色分量值（`DrawingArea` 之前介绍过）。构造一个 `wxColour` 对象并用这些值初始化；该对象用于初始化我们最终通过引用传递给 `wxColourDialog` 构造函数的 `wxColourData` 对象的颜色分量。

遵循 `wxFontDialog` 和 `wxFileDialog` 展示的模式，我们查询 `wxColourDialog` 对象以获取用户选择，但仅当 `ShowModal()` 返回 `wxID_OK` 时。`GetColourData()` 方法检索 `wxColourData` 对象的引用，可以通过用户选择颜色的红、绿、蓝分量进行查询。正如前面的列表所示，获取的颜色随后直接传递给 `DrawingArea` 对象并调用其 `Refresh()` 方法，导致 `DrawingArea::OnPaint()` 函数使用分配的颜色绘制。

# 国际化与本地化

wxWidgets 使用基于目录的国际化（i18n）方法，该方法基于 GNU 的 `gettext` 包。开发基于 i18n 的应用程序实际上需要这些工具，如后文所示。
