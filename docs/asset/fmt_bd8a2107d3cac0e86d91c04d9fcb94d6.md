
我们正在此示例程序中添加一个新功能：一个退出按钮。我们可以直接退出，但最好先调用 `XtDestroyApplicationContext` 来清理任何共享的 X 资源。在这个示例中，我们将应用程序上下文声明为全局变量，这样 `do_quit` 函数就可以访问应用程序上下文：

```c
AppContext application_context;

void do_quit(Widget w, XtPointer unused1, XtPointer unused2) {
    XtDestroyApplicationContext(application_context);
    exit();
}
```

与之前的示例，直接在程序中定义默认资源。在这里，我们为 `Text`、`erase` 和 `display` 类定义资源。注意我们没有为 `Quit` 命令按钮定义任何默认资源，但像 `Erase` 和 `Display` 命令按钮那样定义了。`Quit` 按钮将使用默认标签——在这种情况下，它是 `Quit`。

以下代码列了如何设置应用程序资源：

```c
String app_resources[] = {
  "Text.editType: edit",
  "Text.autoFill: on",
  "Text.scrollVertical: whenNeeded",
  "erase.label: The Text widget",
  "display*label: Display the text from the Text widget",
  "Text.preferredPaneSize: 300",
  NULL
};
```

`Text` 资源属性 `autoFill` 用于控制自动换行。`Text` 控件属性 `editType` 用于将文本设置为可编辑。`preferredPaneSize` 设置了 `Pane` 控件中包含的控件所需的像素高度。`main` 函数定义了一个顶层控件，以及用于

![](img/66f6e6c242a0e6a79aeee4012c6ff547_486_0.png)

文本区域、`Erase` 命令按钮、`Display` 命令按钮和 `Quit` 命令按钮：

```c
Widget top_level, paned, text, erase, display, quit;
```

当我们初始化 `Text` 控件时，我们将使用以下内容作为初始文本：

```c
char *initial_text = "Try typing some text!\n\n";
```

我们初始化应用程序上下文（这里使用全局变量定义，以便在 `do_quit` 函数中访问它），以与之前相同的方式定义顶层控件，并创建一个 `paned` 控件：

```c
top_level = XtAppInitialize(&application_context,
                             "textwindow", NULL, 0,
                             &argc, app_resources,
                             NULL, 0);
```

```c
paned = XtCreateManagedWidget("paned", panedWidgetClass, top_level,
                               NULL);
```

我们使用 `XtCreateManagedWidget` 的参数数量来创建控件，以便通过设置文本和字符串属性来指定文本 `awAsciiString` 和初始文本：

```c
text = XtCreateManagedWidget("text", asciiTextWidgetClass, paned,
                             Xtype, XAsciiString,
                             Xtstring,
                             NULL);
```

在这里，我们使用 `paned` 作为父控件，而非顶层控件。此外，对于创建名为 `"erase"` 的 `Command` 控件，可以使用 `XtCreateManagedWidget` 的普通版本，因为我们没有设置任何属性。但是有一个支持变长参数版本的示例（使用 `pane` 作为父控件）：

```c
erase = XtCreateManagedWidget("erase", commandWidgetClass, paned,
                               NULL);
```

类似地，我们定义了 `display` 和 `erase` 控件，然后为所有三个按钮控件设置回调函数。我们使用 `paned` 作为父控件，而不是顶层控件：

```c
display = XtCreateManagedWidget("display", commandWidgetClass, paned,
                                 NULL);
```

```c
quit = XtCreateManagedWidget("quit", commandWidgetClass, paned,
                               NULL);
```

## 使用 Athena 和 Motif 控件

第 29 章

### 29.4 在 KDE 桌面运行 list.c 示例程序

![](img/66f6e6c242a0e6a79aeee4012c6ff547_485_0.png)

### Athena 简单控件

| Widget | Description |
|---|---|
| `IconButton` | Implements a Menu Button that manages the popup shell. |
| `SimpleMenu` | Popup shell and container for menu elements. |
| `Sme` | Simple menu elements that are added to simple menu. |

#### 使用 Athena 和 Motif 控件

第 29 章

程序退出函数。（请记住，函数中的非静态数据分配在调用栈上；这些存储在退出函数后就会“消失”）。我们定义了四个变量来存储在 `menu.c` 示例中创建的控件的值：

```c
Widget top_level, menu_button, menu, menu_element;
```

变量 `menu_element` 被每个菜单元素重用（例如，创建并添加到简单 `menu.c` 中的一个 `Sme` 控件）。正如我们在之前的示例中看到的，我们需要创建应用程序的控件：

```c
top_level = XtVaAppInitialize(&application_context,
    "textmenu", NULL, 0,
    &argc, argv, fallback_resources,
    NULL);

menu_button = XtCreateManagedWidget("menuButton",
    menuButtonWidgetClass,
    top_level, NULL, 0);

menu = XtCreateShell("menu", simpleMenuWidgetClass, menu_button,
    NULL, 0);
```

现在我们循环遍历每个菜单元素，创建一个新的 `Sme` 控件并将其添加到简单菜单中。我们为每个菜单元素使用回调函数：

```c
for (i = 0; i < (int)XtNumber(menu_item_names); i++) {
    menu_element = XtCreateManagedWidget(menu_item_names[i],
        smeBObjectClass,
        menu, NULL, 0);
}
XtAddCallback(menu_element, Xtcallback, do_menu_selection, NULL);
```

在这里，宏 `XtNumber` 提供了数组 `menu_item_names` 中定义的 `NULL` 字符串的数量。每个菜单元素的父控件被设置为变量 `menu`（我们的简单控件）。你可以通过切换到 `src/X/Athena` 目录并输入以下命令来运行 `menu.c` 示例：

```
make
menu
```
