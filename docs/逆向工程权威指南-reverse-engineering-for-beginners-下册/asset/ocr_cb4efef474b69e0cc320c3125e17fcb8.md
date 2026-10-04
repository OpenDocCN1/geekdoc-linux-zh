# 第23章 函数指针

函数指针和其他指针之间没有太大区别。它代表的地址为函数代码段的起始地址。

在函数指针（地址）以函数参数的形式传递给另一个函数，继被用来调用该指针所指向的函数时，这种函数指针的所指向的函数就是“回调函数”/callback function。[1]

此类指针主要应用场景：

+   * 标准C函数库里的qsort()函数和atexit函数[2]。

+   *NIX系统里的信号(Signals)[3]。

+   * 启动线程的CreateThread(windows函数)和pthread_create()(POSIX函数)。

+   * Win32的多种函数，例如EnumWindows()[4]。

+   * Linux内核。例如，Linux以callback的方式调用文件系统的驱动函数：http://lxr.free-electrons.com/source/include/linux/fs.h?v=3#L1525。

+   * GCC插件：https://www.gnu.org/linedocs/gccint/Plugin-API.html#Plugin-API。

+   * Linux窗口管理程序定义快捷方式的dwm键。当键盘接收到可匹配的特定键时，对应的快捷方式就通过callback调用相应的函数。请参见GitHub (https://github.com/cdown/dwm/ )