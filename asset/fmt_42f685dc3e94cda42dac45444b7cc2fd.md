
# 用户用户界面编程
## 第四部分

一个整数计数器变量的地址作为程序数据传递给此回调（或信号处理）函数。每当 `gtk_main` 中的 GTK 事件处理代码调用它时，会将该整数变量的地址作为第二个参数传递。我们在 `do_click` 函数中做的第一件事是将此抽象数据指针强制转换为类型 `(int *)`。现在 `do_click` 函数可以修改在 `main` 函数中定义的计数器变量的值。在你的 GTK 程序中，你可以为回调数据指定任何类型的数据。

```c
void do_click(GtkWidget *widget, gpointer data) {
    int * count = (int *) data;
    *count += 1;
    printf("Button clicked %d times (5 to quit)\n", *count);
    if (*count > 4) gtk_main_quit();
}
```

`simple.c` 文件定义的 `main` 函数确实简单。它使用了以下八个 GTK 工具函数：

| 函数 | 描述 |
|---|---|
| `gtk_init` | 将程序的命令行参数传递给 GTK 初始化代码。任何被处理为 GTK 选项的参数都会从列表中移除。可以在 www.gtk.org 的 GTK 教程中找到可用命令行参数的列表。 |
| `gtk_window_new` | 创建新窗口。此函数通常用于（如示例所示）创建一个顶层应用程序窗口。 |
| `gtk_container_border_width` | 此可选函数设置窗口周围小部件的内边像素数。 |
| `gtk_button_new_with_label` | 创建一个带有指定标签的新按钮。 |
| `gtk_signal_connect` | 我们在上一节中看到此函数如何为特定类型事件的小部件分配一个回调函数。 |
| `gtk_container_add` | 此函数用于将小部件添加到窗口或任何类型的容器小部件中。 |
| `gtk_widget_show` | 此函数使小部件可见。子部件将在父部件之前变为可见。 |
| `gtk_main` | 完成初始化并处理事件。 |

# 使用 GTK 进行 GUI 编程
## 第 30 章

列表 30.1 显示了 `main` 函数，并在列表之后对该代码进行了讨论。

# 列表 30.1 来自 simple.c 的 main 函数

```c
int main(int argc, char *argv[]){
    // 变量以引用
    // 窗口小部件和按钮小部件：
    GtkWidget *window, *button;
    // 用于演示封装（此变量的地址
    // 将传递给按钮的回调函数）；
    int count = 0;
    // 将命令行参数传递给 GTK 初始化函数：
    gtk_init(&argc, &argv);
    // 创建一个新的顶层窗口：
    window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    // 将小部件周围的默认宽度从 0 更改为 5 像素：
    gtk_container_border_width(GTK_CONTAINER(window), 5);
    button = gtk_button_new_label("Click to increment counter");
    // 将 'do_click' 回调函数连接到按钮小部件。
    // 我们传入变量 'count' 的地址，以便
    // 回调函数可以访问 count 的值而无需
    // 使用全局数据：
    gtk_signal_connect(GTK_OBJECT(button), "clicked",
        GTK_SIGNAL_FUNC(do_click), &count);
    // 将按钮小部件添加到窗口小部件：
    gtk_container_add(GTK_CONTAINER(window), button);
    // 在让窗口本身可见之前，让
    // 添加到窗口的小部件可见：
    gtk_widget_show(button);
    gtk_widget_show(window);
    // 处理事件：
    gtk_main();
}
```

（注：由于原文中存在大量重复的段落，译文已根据核心内容进行了去重和翻译。）

## 用户界面编程
### 第四部分

`src/GTK/expat/sample` 目录下的 `elements.c` 文件展示了如何使用基础解析器。使用 expat 解析器的应用程序定义了回调函数，当解析器看到以下三个元素之一时就会调用这些函数：

- 标签（tag）
- 标签内部的数据
- 结束标签

解析器对 XML 文件的树结构进行深度优先搜索，当遇到每种元素类型时，调用相应的回调函数。例如，`elements.c` 示例程序在 `test.xml` 上生成了以下输出：

```
markw@colossus:cat test.xml ; elements
tag name: book
tag name: title
tag data: A test title
tag name: author
tag data:
tag name: last_name
tag data: Watson
tag data:
tag name: first_name
tag data: Mark
tag name: scheme
tag data: (define fff)
tag data: (lambda x) (* x x))
tag data: (define factorial)
tag data: (lambda n)
tag data: (if n = 1)
tag data: 1
tag data: (* n (factorial - n 1)))
markw@colossus:/home/markw/MyDocs/LinuxBook/src/GTK/expat/sample >
```

## 实现 GTK XML 显示程序

现在我们已经查看了一个短 XML 文件（`src/GTK` 目录下的 `text.xml`）以及图 30.2 中 XML 程序的截图，我们将查看 XMLviewer 的实现。`XMLviewer.c` 文件部分派自光盘中 `src/GTK/expat/sample` 目录下的 James Clark 的 `elements.c` 示例程序。`XMLviewer` 程序需要三个包含文件：

```
#include <stdio.h>
#include <gtk/gtk.h>
#include "xmlparse.h"
```

## 使用 GTK 进行 GUI 编程
### 第 30 章

我们需要 `stdio.h`，因为我们从标准输入（stdin）中读取 XML 输入文件。所有的 GTK 应用程序都需要包含 `gtk.h`。`xmlparser.h` 头文件是使用 James Clark 的 expat 解析器的标准头文件。

XML 应用程序创建一个 GTK Tree 控件，并为标准输入 XML 文件中的每个 XML 元素（或标签）在正确的位置添加一个 GTK Tree Element 控件。GTK Tree 控件处理应用程序中展开和折叠子树所需的事件。然而，我们定义了 `item_signal_callback` 函数，作为在 GTK 树显示中处理鼠标选择事件的示例。`item_signal_callback` 的第一个参数是指向 GTK Tree Item 控件的指针，第二个参数是信号名称。由于我们将每个添加到树显示中的 Tree Item 控件都放置了一个 GTK 控件，因此标签（label）可以设置为该树 项标签的地址。使用 GTK 工具函数 `gtk_label_get` 来获取标签的字符以便进行打印。`item_signal_callback` 的定义如下：

```
static void item_signal_callback(GtkWidget *item, gchar *signame) {
gchar *name;
GtkLabel *label;
label = GTK_LABEL(BIN(item)->child);
/* 获取标签的文本 */
gtk_label_get(label, &name);
printf("signal name=%s, selected item name=%s\n", signame, name);
}
```

接下来，我们定义了跟踪 XML 元素处理所需的数据。这包含了指向中心 GTK Tree 控件和 Tree Item 控件的指针。

```
GtkWidget *tree;
GtkWidget *item;
```

在解析 XML 文档中的子树时，我们使用 `subtree[]` 数组存储控件指针：

```
#define MAX_DEPTH 10
GtkWidget *subtree[MAX_DEPTH];
```

`XMLviewer.c` 中的后续部分代码定义了 expat 解析器的回调函数。我们定义了以下函数：

- `handleElementData`——当包含起始标签和结束标签之间的数据时被调用。例如，在处理元素 `<author>Mark Watson</author>` 时，标签之间之间的数据是 "Mark Watson"。
- `startElement`——当标签首次被处理时调用，并传入标签名称。
- `endElement`——在调用 `handleElementData` 后调用，并传入标签名称。

## 用户界面编程

`handleElementData` 函数由 expat 解析器调用以处理标签内部的数据。该函数签名如下：

```
void handleElementData(void *userData, const char *data, int len)
```

对于本章关于 GTK 的内容，获取数据的机制并不十分有趣，但以下代码展示了如何创建 GTK Tree Item 控件：

```
int *depthPtr = userData;
tktkWidget *subitem;
cp = (char *)malloc(len + 1);
for (i=0; i<len; i++) cp[i] = data[i];
cp[len] = '0';
subitem = gtk_tree_item_new_with_label(subtree["depthPtr"]);
gtk_tree_append(GTK_OBJECT(subitem), "select");
gtk_signal_connect(GTK_OBJECT(subitem), "item_signal_callback", "tag select", NULL);
gtk_signal_connect(GTK_OBJECT(subitem), "deselect", "item_signal_callback", "tag deselect", NULL);
gtk_widget_show(subitem);
```

在这里，expat 解析器将当前深度传递给 `startElement` 函数。`startElement` 的签名是：

```
void startElement(void *userData, const char *name, const char **atts)
```

我们将 `userData` 指针转换为以访问深度：

```
int *depthPtr = userData;
*depthPtr += 1;
```

## 使用 GTK 进行 GUI 编程

`startElement` 根据当前深度执行任务。对于文档中的顶层标签，我们创建一个 GTK 树并存储该项的全局变量（我们将在后续列表后讨论此）：

```
if (*depthPtr == 1) {
item = gtk_tree_item_new_label((char*)name);
gtk_signal_connect(GTK_OBJECT(item), "select",
GTK_SIGNAL_FUNC(item_signal_callback),
"top-level select";
gtk_signal_connect(GTK_OBJECT(item), "deselect",
GTK_SIGNAL_FUNC(item_signal_callback),
"top-level deselect";
// 树项包含任意数量的项；在此添加新项：
gtk_tree_append(GTK_TREE(tree), item);
gtk_widget_show(item);
// 创建此项的子树
subtree[*depthPtr] = gtk_tree_new();
gtk_tree_set_view(GTK_TREE(subtree[*depthPtr]),
GTK_TREE_VIEW_ITEM);
gtk_tree_item_set_subtree(GTK_TREE_ITEM(item), subtree[*depthPtr]);
}
```

在处理最复杂的 XML 标签时，我们使用全局变量 `tree` 将新创建的树项添加到 GTK 树。与 `handleElementData` 函数一样，我们为 "select" 和 "deselect" 设置信号回调。一个新的 GTK 树控件被创建并存储在 `subtree` 数组中。注意，该数组在程序中作为数据结构使用，新树设置为新创建的 GTK Item 控件的子树。

如果当前解析深度大于1（例如我们没有处理 XML 文档中的顶层标签）（我们将在后续列表后讨论此代码）：

```
if (*depthPtr > 1) {
GtkWidget *subitem = gtk_tree_item_new_with_label((char*)name);
subtree[*depthPtr] = gtk_tree_new();
gtk_signal_connect(GTK_OBJECT(subitem), "select",
GTK_SIGNAL_FUNC(item_signal_callback),
"tree item select";
gtk_signal_connect(GTK_OBJECT(subitem), "deselect",
GTK_SIGNAL_FUNC(item_signal_callback),
"tree item deselect";
// 将此子树添加到其父树：
gtk_tree_append(GTK_TREE(subtree[*depthPtr] - 1), subitem);
gtk_widget_show(subitem);
gtk_tree_item_set_subtree(GTK_TREE_ITEM(subitem),
ubtree[*depthPtr]);
}
```

# 用户界面编程
## 第四部分

当 expat 属性解析器（expat parser）处理一个结束标签（例如 `</author>`）时，会调用 `endElement` 函数。该函数递减解析器的深度计数器，如下：

```c
void endElement(void *userData, const char *name) {
    int *depthPtr = userData;
    *depthPtr -= 1; // 递减栈指针
}
```

作为 XML 文档解析深度的一部分，请考虑以下 XML 数据，每行都标明了解析深度：

```xml
<book>
  <title>Kit bit the cat</title>
  <author>
    <last_name>Smith</last_name>
    <first_name>Joshua</first_name>
  </author>
</book>
```

`main` 函数负责做两件事：设置 XML 解析器和初始化 GTK 控件。我们已经看到过处理元素标签、元素文本数据和关闭元素标签的 XML 解析器回调函数的实现。这些回调（或信号处理程序）函数创建了 GTK 树元素控件，但 `main` 函数有责任创建顶部的 GTK Tree 控件和顶层窗口。下面的讨论使用了 `main` 函数实现中的代码片段。

`main` 函数使用 James Clark 的 expat 库创建一个新的 XML 解析器对象，如下：

```c
XML_Parser parser = XML_ParserCreate(NULL);
```

GTKviewer 使用一个带有滚动区域的顶层窗口。以下代码片段展示了如何设置带有滚动条的滚动区域，滚动条会在需要时自动激活。我们定义了两个变量 `scrolled_win` 作为指向 GtkWidgets 的指针，并调用了我们在之前的 GTK 示例中看到的标准 GTK `gtk_init` 函数。使用 `gtk_scrolled_window_function` 创建滚动窗口控件，并将该控件添加到由 `window` 变量引用的 `GtkWidget` 中。`gtk_scrolled_window_set_policy` 函数可用于设置滚动条的自动处理（正如我们所做的），也可以用于让滚动条始终可见。`gtk_widget_set_use_request` 函数设置滚动控件的最小尺寸。用户将无法通过调整顶层窗口的大小来使滚动窗口小于 `gtk_widget_set_size` 设置的大小。

```c
GtkWidget *window, *scrolled_win;
gtk_init(&argc, &argv);
window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
scrolled_win = gtk_scrolled_window_new(GTK_SCROLLED_WINDOW, NULL);
```
