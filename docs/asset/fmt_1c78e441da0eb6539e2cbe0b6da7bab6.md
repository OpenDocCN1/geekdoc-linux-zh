
现在我们遍历每个菜单元素名称，创建一个新的 Sme 部件并将其添加到简单菜单。我们还为每个元素分配了我们的回调函数：

```c
for (i = 0; i < (int)XtNumber(menu_item_names); i++) {
    menu_element = XtCreateManagedWidget(menu_item_names[i],
        smeBSObjectClass,
        menu, NULL, 0);
    XtAddCallback(menu_element, Xtcallback, menu_selection, NULL);
}
```

在这里，宏 `XtNumber` 提供了数组 `menu_item_names` 中定义的非空字符串数量。每个菜单元素的父级（Parent）被设置为变量 `menu`（我们的简单菜单）。你可以切换到 `src/X/Athena` 目录并输入以下命令来运行 `menu.c` 示例：

```bash
make
menu
```

## 使用 Motif 部件

本章中的程序是免费提供的 LessTif 克隆（访问 www.lestif.org）和商业 Metro Link Motif 产品（访问 www.metrolink.com）开发并测试的。我要感谢 Metro Link 为我提供他们的 Linux 版商业 Motif 产品。我们将在本节中使用三个示例程序（它们位于 `src/X/Motif` 目录）：

| 程序 | 描述 |
| --- | --- |
| label.c | 介绍 Motif。 |
| list.c | 显示如何处理事件。 |
| text.c | 将面板容器与文本和命令按钮部件结合。 |

我们学到的关于使用 Athena 部件的大部分内容对 Motif 程序也将很有用。使用 Motif 最大的区别在于使用 Motif Strings 而不是 8 位字符字符串。另一个区别在于部件资源的命名和定义。部件头文件为头文件中定义的部件定义了新的资源类型。Motif 部件资源的名称定义在包含头文件 `XmDefs.h` 中。以下是一些 Motif 资源名称：

```motif
#XmAlignment 'alignment'
#XmNOverlap 'allowOverlap'
#XmResize 'allowResize'
#XmClientData 'clientData'
#XmClip 'clipWindow'
#XmColumns 'columns'
#XmCommand 'command'
```

接下来，我们为 Motif Strings 数组的每个元素定义值，并在创建 Motif List 小部件时使用该数组：

```c
motif_strings[0] = XmStringCreateSimple("list item at index 0");
motif_strings[1] = XmStringCreateSimple("list item at index 1");
motif_strings[2] = XmStringCreateSimple("list item at index 2");
```

```c
XtSetArg(arg[0], XmitemCount, 3);
XtSetArg(arg[1], Xmitems, motif_strings);
XtSetArg(arg[2], XmVisibleItemCount, 3); // all list elements
XtSetArg(arg[3], XmSelectionPolicy, XMSINGLE_SELECT);
```

```c
list = XmCreateList(top_level, 'list', arg, 4);
```

我们为创建 List widget 指定了四个参数：

- 列表元素的数量
- 列表元素的数据
- 应该可见的列表元素数量
- 一次只能选择一个项目

如果我们允许多项选择，那么我们就必须重写回调函数 `function_do_list_click` 来处理获取多个选择。在创建 List widget 后，我们为该 widget 指定回调函数 `do_list_click`，使 List widget 和 Top-level widget 可见，并处理 X 事件：

```c
XtAddCallback(list, XmSelectionCallback,
    (XtCallbackProc)do_list_click, NULL);
XtManageChild(list);
XtRealizeWidget(top_level);
XtMainLoop();
```

图 29.6 显示了在 KDE 桌面环境下运行的 `list.c` 示例程序。

![](img/69b363a7d7f58dc8d0b8c78c0052826f_520_0.png)

图 29.6 
Motif List widget 示例。

你可以通过切换目录到 `src/X/Motif` 并输入命令来构建并运行此程序：

```
make
Motif
```

使用 Motif widget 比使用 Athena widget 稍微复杂一点，但通常 Motif widget 提供的选项更多。在过去的 10 年里，我同样使用 Athena 和 Motif widget，根据应用程序需求和客户偏好来选择使用哪种 widget。

# Motif Text Widget

本节的示例程序位于 `src/X/Motif` 目录下的 `text.c` 文件。此示例引入了使用面板容器（panel container）来容载其他 widget。该示例使用了一个 Text widget 和两个 Push Button widget。此示例只需要两个文件：一个用于核心 Motif 定义，另一个用于定义 Motif Text widget。我们使用实用函数来创建 Motif Push Button widget 和面板窗口（Pained Window widget），因此不需要单独的文件来支持这些 widget 类型：

```c
#include <Xm.h>
#include <Xm/Text.h>
```

此示例使用了两个回调函数——每个 Push Button widget 各一个。第一个回调函数用于显示 Text widget 的文本：

```c
void do_get_text(Widget widget, caddr_t client_data, caddr_t call_data) {
    Widget text = (Widget)client_data;
    char *string = XmTextGetString(text);
    printf("The Motif example Text widget contains:\n%s\n", string);
    XtFree(string);
}
```

这是我们第一次使用第二个参数的回调示例。当我们将此回调函数绑定到“display text”Push Button widget 时，我们指定了 Text widget 应该作为 client data 传递给回调函数。查看后续示例代码：

```c
Widget text = XmCreateText(pane, "text", NULL, 0);
Widget display_button = XmCreatePushButton(pane, "Display", NULL, 0);
XtAddCallback(display_button, XmActivateCallback,
    (XtCallbackProc)do_get_text, text);
```

在这里，Widget 的值被指定为回调函数的 client data。

第二个回调更简单；它调用系统函数 `exit` 来终止程序：

```c
void do_quit(Widget widget, caddr_t client_data, caddr_t call_data) {
    exit(0);
}
```

该函数定义了五个要要使用的 widget：

```c
Widget top_level, pane, text, display_button, quit;
```

## 使用 Athena 和 Motif Widgets

`pane` widget 将添加到 Top-Level Application widget 中。所有剩余 widget 将被添加到 `pane` 中，它将垂直布局文本和 Push Button widget：

```c
top_level = XtInitialize(argv[0], "test", NULL, 0, &argc, argv);
pane = XmCreatePaneWindow(top_level, "pane", NULL, 0);
```

在此示例中，在创建 Text widget 之前，我们为 Text widget 的五个资源设置了值：

```c
XtSetArg(arg[0], XWidth, 400);
XtSetArg(arg[1], XHeight, 400);
XtSetArg(arg[2], XmWrap, TRUE);
XtSetArg(arg[3], XmEditMode, XMULTI_LINE_EDIT);
text = XmCreateText(pane, "text", arg, 5);
```

我们想要指定文本区域的大小。Panel widget 将根据其包含的 widget 的偏好大小自动调整自身 own。Text widget 的宽度设置为 400 像素实际上使得 Panel widget 宽度变为 400 像素，因为除非创建时标签非常长，否则两个 Push Button widget 的偏好宽度将是 400 像素。我们指定 Text widget 的行会自动换行到下一行文本。在这里，我们将两个推按钮定义为 pane widget 的回调，并指定了它们的回调函数：

```c
display_button = XmCreatePushButton(pane, "Display", NULL, 0);
quit_button = XmCreatePushButton(pane, "Quit", NULL, 0);
```

```c
XtAddCallback(display_button, XmActivateCallback,
    (XtCallbackProc)do_get_text, text);
XtAddCallback(quit_button, XmActivateCallback,
    (XtCallbackProc)do_quit, NULL);
```

等待，我漏掉了一些：如前所述，我们将 Text widget 的值作为 client data 传递给“display”按钮的回调函数。在此示例中，我们在添加 Top-level widget 之前单独管理每个 widget。我们可以看到通过 `XtMainLoop` 处理事件：

```c
XtManageChild(text);
XtManageChild(display_button);
XtManageChild(quit_button);
XtManageChild(pane);
XtRealizeWidget(top_level);
XtMainLoop();
```

图 29.7 显示了在 KDE 环境运行的 `text.c` 示例程序的截图。

![](img/69b363a7d7f58dc8d0b8c78c0052826f_522_0.png)

图 29.6 
Motif List widget 示例。

![](img/69b363a7d7f58dc8d0b8c78c0052826f_523_0.png)

你可以通过切换目录到 `src/X/Motif` 并输入命令来构建并运行此程序：

```
make text
```

此示例展示了 Motif 应用程序的标准结构：我们创建一个包含应用程序中所有其他 widget 的 Pane widget。这个 pane widget 将在用户缩放主窗口时处理 widget 的缩放。另一种方法是将 Child widget 直接放置在 Main Application widget 中，并指定每个 widget 的 x-y 位置和大小。

# 编写自定义 widget

许多 X Windows 程序员不需要编写自定义 widget，但定义新 widget 的能力是封装应用程序数据和行为的强大技术。在本节中，我们将创建一个名为 URLWidget 的 widget，它显示来自 URL 地址的文本。编写新 widget 似乎是一项艰巨的任务；但通过找到类似 widget 的源代码并对其修改，可以使工作变得更容易。对于此示例，我们将从 X 联盟的 Template widget 开始。你可能还会查看我们的网站 http://www.x.org。

URLWidget 的源代码和测试程序 `test.c` 位于 `src/X/URLWidget` 目录。原始的模板示例（你可能想将其作为编写你自己的 Athena widget 的起点）位于 `src/X/URLWidget/templates` 目录。URLWidget 是一个简单的 widget，它根据 URL 地址从文件中获取文本，并作为字符串存储在 widget 的私有数据中。每当 widget 需要重绘自身时，该字符串会被解析以提取单独的行，然后在 widget 的可绘制区域中绘制。实现此 widget 使用四个文件：

| 文件 | 描述 |
| :--- | :--- |
| fetch_url.c | 连接 Web 服务器并请求文件的套 代码 |
| URL.h | 当你想创建 URLWidget 时包含的公共头文件 |
| URLP.h | 私有头文件 |
| URL.c | URLWidget 的实现 |

我们基于 Template.h、TemplateP.h 和 Template.c 开发了 URL.h、URLP.h 和 URL.c，这些文件带有版权所有：

> /* X Consortium: Template.c, v 2 88/10/25 17:40:25 */
> /* Copyright Massachusetts Institute of Technology 1987, 1988 */

X 联盟在保留所有版权声明的情况下允许免费使用他们的软件。

## 使用 fetch_url.c 文件

位于 `src/X/URLWidget` 目录下的 `fetch_url.c` 实现远程 Web 工具源自 `src/IPC/SOCKETS` 目录下的 `web_client.c`。此示例程序在第 19 章讨论过。该工具函数的签名如下：

```c
char * fetch_url(char *url_name);
```

以下是示例用法：

```c
char * mark_home_page1 = fetch_url("www.markwatson.com");
char * mark_home_page2 = fetch_url("http://www.markwatson.com");
char * mark_home_page3 = fetch_url("http://www.markwatson.com/index.html");
```

对该工具的后续讨论非常短；你可能也想参考第 19 章。Web 服务器默认监听端口 80：

```c
int port = 80;
```

![](img/69b363a7d7f58dc8d0b8c78c0052826f_524_0.png)

# 用户界面编程
第四 部分

以下数组被用于处理：

| 数组 | 描述 |
| --- | --- |
| char * buf = (char *)malloc(50000) | 用于存储返回的数据。 |
| char message[256] | 用于向 Web 服务器构建 "GET" 消息。 |
| char host_name[200] | 用于从 URL 中构造正确的主机名。 |
| char file_name[200] | 用于 URL 末尾的最优文件名。 |
| char *error_string | 用于构造正确的错误信息。 |

此实用程序函数分配了返回给调用者的内存块，但调用者有责任释放这部分内存。以下代码确定了正确的主机名以及 URL 句尾的最优文件名：

```c
char *sp1, *sp2;
sp1 = strstr(url, "http://");
if (sp1 == NULL)
    printf(host_name, "%s", url);
else
    printf(host_name, "%s", &url[7]);
printf("1. host_name=%s\n", host_name);
sp1 = strstr(host_name, "//");
if (sp1 == NULL)
    // 没有文件名，所以使用 index.html：
    printf(file_name, "index.html");
else
    printf(file_name, "%s", (char *)(sp1 + 1));
    *sp1 = "\0";
printf("2. host_name=%s, file_name=%s\n", host_name, file_name);
```

与 Web 服务器建立连接：

```c
if ((nlp_host = gethostbyname(host_name)) == 0) {
    error_string = (char *)malloc(128);
    printf(error_string, "Error resolving local host\n");
    return error_string;
}
bzero(&pin, sizeof(pin));
pin.sin_family = AF_INET;
```
