
**图 5-34.** 一个 X 窗口应用程序的骨架。

调用 `XCreateGC` 创建一个存储窗口属性的图形上下文。在更完整的程序中，这些属性可能会被初始化。下一个语句调用 `XSelectInput` 告诉 X 服务器程序准备好处理哪些事件。在这种情况下，它对鼠标点击、按键按下和窗口被覆盖感兴趣。在实践中，真正的程序还会对其他事件感兴趣。最后，调用 `XMapWindow` 将新窗口映射到屏幕上，使其成为最顶层窗口。此时，窗口在屏幕上变得可见。

主循环由两个语句组成，在逻辑上比 Windows 中相应的循环更简单。这里的第一个语句获取事件，第二个语句根据事件类型进行分发以处理。当某个事件指示程序已结束时，`running` 被设置为 0，循环终止。退出时，程序释放图形上下文、窗口和连接。

# 第 5.6 节 用户界面：键盘、鼠标、显示器 405

值得提到的是，并不是每个人都喜欢 GUI。许多程序员更倾向于上述第 5.6.1 节讨论的传统命令行定向界面。X 通过一个名为 `xterm` 的客户端程序来处理这一点。该程序模拟了一个老式的 VT102 智能终端，带有所有的转义序列。使用 `vi`、`emacs` 以及其他使用 `termcap` 的软件可以在这些窗口中无需修改即可运行。

## 图形用户界面

大多数电脑都提供 GUI（图形用户界面）。GUI 的缩写读作 "gooey"。

GUI 由道格拉斯·恩格尔巴特（Douglas Engelbart）及其在斯坦福研究中心的小组发明。随后它被施罗德 PARC 的研究人员复制。有一天，苹果公司的联合创始人斯蒂夫·乔布斯（Steve Jobs）在参观 PARC 时，在施罗德电脑上看到了 GUI，并说了类似“疯狂的鲭鱼”（Hacky mackerel）的话。GUI 给了他设计新电脑的灵感，变成了 Apple Lisa。Lisa 太贵了，在商业上失败了，但它的继任者 Macintosh 取得了巨大的成功。

当微软获得一台 Macintosh 原型以便在上面开发 Microsoft Office 时，它请求苹果将该界面授权给所有人，以便其成为新的行业标准。（微软从 Office 上赚的钱比从 MS-DOS 多得多，因此它愿意放弃 MS-DOS 以为 Office 提供一个更好的平台。）负责 Macintosh 的执行人让·路易斯·加西（Jean-Louis Gassée）和斯蒂夫·乔布斯不再忽视他。最终，微软获得了了界面部分元素的授权许可。这构成了 Windows 的基础。当 Windows 开始追赶苹果时，苹果起诉微软，声称微软超出了许可范围，但法官并不认同，Windows 最终反超了 Macintosh。如果加西同意苹果内部许多也想将 Macintosh 软件授权给每个人以及他叔叔的意见，苹果将在许可费上赚得惊人的数字，而 Windows 也不会存在。`WIMP` 代表 Windows（窗口）、Icons（图标）、Menu（菜单）和 pointing device（指针设备）。这是现代 GUI 的四个基本元素。窗口用于运行程序的矩形区域。图标是可以点击的小符号。菜单是包含命令的条，指针设备是用于选择项目的鼠标。

屏幕上的基本项目是包含窗口的矩形区域。窗口的位置和大小通过给出对角线顶点坐标（像素）来唯一确定。一个窗口可能包含标题栏、菜单栏、工具栏、垂直滚动条和水平滚动条。图 5-35 显示了一个典型的窗口。注意，Windows 坐标系统的原点位于左上角，y轴向下，这与数学中使用的笛卡尔坐标系不同。

当创建窗口时，参数指定了用户是否可以移动窗口、调整窗口大小或（通过拖动滚动条上的滑块）滚动。许多程序产生的窗口可能会对编写的 Windows 程序产生影响。特别是，程序必须被告知窗口大小的变化，并准备好随时重绘窗口内容，即使在它们预料到的时候。

因此，Windows 程序是消息导向的。涉及键盘或鼠标的用户操作被 Windows 捕获并转换为发送给目标窗口程序的消息。每个程序都有一个消息队列，所有与其窗口相关的消息都会发送到那里。程序的主循环由取出下一条消息并通过调用该消息类型的内部过程进行处理组成。在某些情况下，Windows 自身可能会调用这些过程，从而跳过消息队列。这种模型与 UNIX 通过系统调用与操作系统交互的过程代码模型截然不同。然而，X 是事件导向的。

# 第 5.6 节 用户界面：键盘、鼠标、显示器 407

(0, 0)

(1023, 0)

![](img/4ce80248dee7322740d1fb5538299265_437_0.png)

**图 5-35.** 位于 XGA 显示器上 (200, 100) 处的示例窗口。

为了让这个编程模型更加清晰，请考虑图 5-36 的示例。在这里我们看到了一个 Windows 主程序的骨架。它并不完整，也没有进行错误检查，但它展示了足够我们目的的细节。它首先包含了一个头文件 `windows.h`，该文件包含了 Windows 程序所需的许多宏、数据类型、常量、函数原型以及其他信息。

主程序从一个给出名称和参数的声明开始。`WINAPI` 宏是告诉编译器使用特定参数传递约定的指令，我们无需对其进一步关注。第一个参数 `hInstance` 是一个实例句柄，用于向系统的其他部分标识程序。在某种程度上，Win32 是面向面向对象的，这意味着系统对象（例如程序、文件和窗口）具有某些状态和关联的代码，称为**方法**，它们作用于该状态。对象通过句柄进行引用，在这种情况下，`hInstance` 标识了程序。第二个参数仅出于后兼容性而存在，它已不再被实际使用。第三个参数 `szCmd` 是一个以零终止的字符串，包含了启动程序的命令行，即使它不是从命令行启动的。第四个参数 `iCmdShow` 告诉初始窗口应该占据整个屏幕、部分屏幕还是不占据屏幕（任务栏）。

```c
#include <windows.h>

int WINAPI WinMain(HINSTANCE hInstance, HINSTANCE hprev, char *szCmd, int iCmdShow)
{
    WNDCLASS wndclass; /* 此窗口的类对象 */
    MSG msg; /* 传入的消息存储在此处 */
    HWND hwnd; /* 指向窗口对象的句柄（指针） */
    /* 初始化 wndclass */
    wndclass.lpWndProc = WndProc; /* 告诉调用哪个过程 */
    wndclass.lpszClassName = "Program name"; /* 标题栏的文本
    wndclass.hClIcon = LoadIcon(NULL, ID_APPLICATION); /* 加载程序图标 */
    wndclass.hCursor = LoadCursor(NULL, IDC_ARROW); /* 加载鼠标指针 */
    RegisterClass(&wndclass); /* 告诉 Windows wndclass */
    hwnd = CreateWindow ( ... ); /* 为窗口分配存储 */
    ShowWindow(hwnd, iCmdShow); /* 在屏幕上显示窗口 */
    UpdateWindow(hwnd); /* 告诉窗口重绘自己 */
    while (GetMessage(&msg, NULL, 0, 0)) { /* 从队列获取消息 */
        TranslateMessage(&msg); /* 翻译消息 */
        DispatchMessage(&msg); /* 将消息发送给适当的过程 */
    }
    return(msg.wParam);
}
```

```c
long CALLBACK WndProc(HWND hwnd, UINT wParam, LPARAM lParam)
{
    /* 声明在此处。 */
    switch (message) {
        case WM_CREATE:      return ...; /* 创建窗口 */
        case WM_PAINT:      return ...; /* 重绘窗口内容 */
        case WM_DESTROY:    return ...; /* 销毁窗口 */
    }
    return(DefWindowProc(hwnd, message, wParam, lParam)); /* 默认处理程序 */
}
```
