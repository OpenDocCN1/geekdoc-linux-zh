
```c
1: #include <stdlib.h>
2: #include <stdio.h>
3: #include <X11/Intrinsic.h> /* 用于创建程序
4: #include <X11/StringDefs.h> /* 用于资源名 */
5: #include <X11/Xaw/Form.h> /* 定义表控件类 */
6: {
7: XtAppContext context;
8: Widget toplevel form;
9:
10: toplevel = XtvaAppInitialize(&context, /* "2D-Editor", /* 应用程序类名 */
11: NULL,0, /* 选项列表（未使用） */
12: );
```

# X Window应用程序的组件

## 第6 章

147

```
13:    &argc, argv, /* 命令行参数 */
14:    NULL,             /* 回退资源（未
                                     使用） */
14a:   /* 变量结束
15a:   NULL 参数列表 */
16:   );
```

该函数执行了若干项对应用程序执行至关重要的操作。

第一个参数传递了 `XtAppContext` 结构体的地址 `(&)`，我将其命名为 `appContext`。`XtAppContext` 是用于维护与应用程序相关信息的结构体。一旦通过 `xtvaInitialize` 填充 `appContext` 变量，即可满足后续 xt 函数的参数要求。

从第二个参数，`xtvaInitialize` 读取应用程序的类名，并查询服务器资源数据库，获取任何可能应用于应用程序组件的值。

### 课习

### 在应用程序中定制小部件

为了提供满足大型用户群体不同需求所需的扩展性，小部件（widgets）是高度可配置的。

配置小部件涉及更改它们可用资源的值。正如第 5 章所述，资源由单个小部件引入，并根据它们在类层次中的位置进行继承。

小部件的配置可以由程序员硬编码，在这种情况下，应用程序的用户是完全无法更改的。

此外，小部件的配置也可以完全由用户决定。这要求用户了解某些信息，即实例层次结构和应用程序的类名。记住，源代码并不总是确定这些信息的唯一依据。用户通常可以通过应用程序作者提供的默认资源文件获得关于实例层次结构的线索。

在没有默认资源文件的情况下，用户可以使用 X 编辑器（`editres`）来查看基于 Xt 的应用程序的结构。该工具对于查找和设置资源非常有用，并能够即时查看结果。此外，当程序员未提供必要信息时，`editres` 对于创建应用程序资源文件具有无价的价值。

应用程序的小部件配置（资源文件）可以存在于 X 环境中的多个位置。

Linux 通常在 `/usr/X11/app-defaults` 目录下放置一个与应用程序类名相对应的文件。该文件的每一行都包含一个特定小部件的资源/值对，用于指定所需应用程序配置的元素。

![](img/786ba9bd5cd671beb490264fd2e6aae1_169_0.png)

## 第二部分 X 的组成部分

在之前说明 `XtvaAppInitialize` 函数使用的示例中，分配给应用程序的任意类名为 `2-Editor`。因此，可以在 `app-defaults` 目录下放置一个同名文件，用于指定该应用程序的小部件配置。由于该文件在运行时由 `XtvaAppInitialize` 读取并加载，因此资源值的配置完全由维护者的决定。

偶尔，位于用户家目录下的 `.Xdefaults` 文件的内容将覆盖任何应用程序在 `app-defaults` 目录的类文件中的条目。

最后，在命令行上指定并通过 `argc` 和 `argv` 参数传递给 `XtvaAppInitialize` 的资源值将被应用于应用程序。完全传递给应用程序（即除硬编码之外）的所有资源及其值都维护在 X 服务器内部的一个名为“X 资源数据库”的数据库中。要查看当前服务器数据库中包含的值，请查看命令：

```bash
xrdb -query
```

`XtvaAppInitialize` 函数将命令行上指定的任何选项与在该应用程序 X 资源数据库中找到选项合并。

表 6.1 显示了 `XtvaAppInitialize` 函数理解的命令行选项。因此，所有这些选项适用于使用 `XtvaAppInitialize` 初始化与服务器连接的 X 应用程序。

| 表 6.1 标准 X 命令行参数 |

| 选项 | 资源文件语法 | 效果 |

| :--- | :--- | :--- |

| -bg | *background | 背景颜色 |

| -bd | *borderColor | 边框颜色 |

| -bw | *borderWidth | 边框宽度 |

| -display | *display | 要使用的 X 服务器 |

| -fg | *foreground | 前景颜色 |

| -fn | *font | 字体名称 |

| -geometry | *geometry | 尺寸和位置 |

| -iconic | *iconic | 应用程序标识的 |

| -name | *name | 应用程序名称 |

| -title | *title | 窗口标题 |

### 课习

### 唯一指定小部件路径

资源/值对的语法位于 `app-defaults` 文件或用户的 `.xdefaults` 文件（表 6.1 中）。

注意每个名称前的通配符以及用于分隔名称和值的冒号。通配符是可选语法。

在没有默认资源文件的情况下，用户可以使用 X 编辑器（`editres`）来查看基于 Xt 的应用程序的结构。该工具对于查找和设置资源非常有用，并能够即时查看结果。此外，当程序员未提供必要信息时，`editres` 对于创建应用程序资源文件具有无价的价值。

应用程序的小部件配置（资源文件）可以存在于 X 环境中的多个位置。

该字段指定（在 X 服务器支持多个显示器的情况下）应用程序应该显示的哪个显示器。

通常机器上运行一个服务器，且支持单个显示器。典型的 `displayname` 设置为：

```
machine:0
```

其中省略了屏幕，0 指机器上存在的服务器。

![](img/786ba9bd5cd671beb490264fd2e6aae1_171.png)

## 第二部分 X 的组成部分

如果 `XtvaInitialize` 函数无法与 X 服务器建立，它将不会创建 `ApplicationShell` 并返回 `NULL` 表示错误。因此，测试 `XtvaInitialize` 的返回值是非常重要的：

```c
toplevel = XtvaAppInitialize(&appContext, "2-Editor", NULL,
    &argc, argv, NULL, NULL);

if (toplevel == NULL) {
    fprintf(stderr, "Failed to connect to X server!");
    exit (1);
}
```

在连接失败的情况下，未测试 `XtvaInitialize` 的返回值会导致程序崩溃。

`XtvaInitialize` 如何知道要寻找哪个 X 服务器？

`XtvaInitialize` 首先考虑命令行参数 `-display displayname`，以确定与哪个 X 服务器建立连接。

如果没有指定 `-display` 参数，则会查询环境变量 `DISPLAY`。如果该变量在环境中设置，则其值将用于确定与哪个服务器尝试通信。

在环境变量中没有 `DISPLAY` 变量且命令行上没有 `-display` 参数的情况下，最后会寻找本地主机上的显示服务器。

连接失败的两个最常见原因是：显示名称（`displayname`）格式错误或访问被拒绝，这意味着服务器可能会拒绝请求，因为尝试连接的主机不在服务器的访问控制列表中。

访问控制列表由 `xhost` 命令管理，用于确定哪些机器可以使用 X Server 语法进行连接。

使用以下语法授予访问：

``` evenxhost +hostname
```

或通过以下方式拒绝：

```
xhost -hostname
```

启用对服务器的所有连接请求将实际上关闭访问控制列表。执行不带任何指定主机的 `xhost` 命令即可实现这一点。

```
xhost +
```

同样，通过执行命令可以拒绝所有连接请求：

```
xhost -
```

在接收由 `XtVaInitialize` 返回的有效小部件引用并成功建立了与 X Server 的连接后，你就可以继续按照应用程序语法创建图形界面了。

## 创建应用程序界面

由于一个子部件不足以完成一个复杂的图形用户界面，`ApplicationShell` 部件的唯一子部件通常是 `Composite`（管理器）类中的某个部件，例如 `Form` 部件。
