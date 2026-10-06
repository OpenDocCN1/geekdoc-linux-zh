

## 11.5. 安装和配置性能工具

排查的下一步是安装调查问题所需的性能工具。正如我们在对 GIMP 进行性能排查时所的那样，我们将同时安装 profile 和 ltrace。在这种情况下，我们还将下载并安装 gdb（如果尚未安装的话）。gdb 允许我们查看运行应用程序的某些动态方面。

## 11.6. 运行应用程序和性能工具

接下来，我们运行应用程序并使用性能工具进行测量。由于我们已经怀疑许多进程和库的复杂相互作用可能是问题的原因，我们将从 profile 开始，看看它能显示什么内容。

由于我们只希望在打开弹出菜单时让 profile 测量事件，我们将使用如列表 11.3 所示的命令行，在运行打开和关闭 100 个弹出菜单的脚本 (`script.sh`) 之前和之后立即启动并进行性能分析。

# 列表 11.3。

```
opcontrol -start ; ./script.sh opcontrol -stop
```

在收集到分析数据后运行 oreport，我们可以得到列表 11.4 所示的信息。

# 列表 11.4.

```
CPU: CPU with timer interrupt, speed 0 MHz (estimated)
Profiling through timer interrupt
TIMER:0
samples |%
----------|-------
3134 27.1460 /usr/lib/libobject-2.0.so.0.400
1840 19.5376 /usr/lib/libglib-2.0.so.0.400
1303 11.2863 /lib/tls/libc-2.3.3.so
1048 9.0775 /usr/lib/tls/lpthread-01.6.so
900 7.7156 /usr/lib/libgtk-tk1-2.0.so.0.400
810 7.0160 /usr/X11R6/bin/Xorg
719 6.2278 /usr/lib/libgdk-x11-2.0.so.0.400
334 2.8930 /usr/lib/libpango-1.0.so.399.1
308 2.6768 /lib/ld-2.3.3.so
298 2.5812 /usr/X11R6/libX11.so.6.2
228 1.9749 /usr/lib/libbonobui-2.so.0.0
152 1.3166 /usr/X11R6/libXft.so.2.1.1.2
```

如你所见，函数分布在许多不同的库中。完全不清楚哪个应用程序负责产生这些调用。特别是，我们完全不知道哪些进程调用了 libobject。幸运的是，profile 提供了一种记录应用程序在运行期间使用的共享库函数的方法。列表 11.5 显示了如何配置 profile 的收集以按库分离样本，这将会将共享库中的样本归类到调用的程序上。

# 列表 11.5。

```
opcontrol -p library; opcontrol --reset
```

在我们运行命令后（如列表 11.3 所示），oreport 会按应用程序划分库样本，

# 列表 11.6。

## 11.7. 编译并检查源码

现在我们对哪个应用程序消耗了所有时间有了初步了解，我们将下载源码并编译它。到目前为止，我们所有的分析都是使用 Red Hat 提供的二进制包完成的。然而，现在我们需要深入源代码，检查为什么这些热点函数被调用，当我们弄清楚后，将对源码进行修改以缓解性能问题。正如我们为 GIMP 执行的那样，在调用 configure 之前，通过设置 CFLAGS -g 来生成调试符号。

在这种情况下，我们下载并安装了 Red Hat 的 nautilus rpm 包，这会将 nautilus 的源码放置在 `/usr/redhat/SOURCES/` 中。使用 Red Hat 的源码包，我们拥有 Red Hat 创建包中二进制文件时使用的源码和补丁。调查我们用于创建被调查二进制文件的源码至关重要，因为另一个版本可能具有不同的性能特征。提取源码后，我们就可以开始弄清楚 `bonobo_window_add_popup` 在哪里被调用。我们可以使用列表 11.9 搜索 nautilus 目录中的所有文件。

# 列表 11.9。

```
nautilus -type f | xargs grep bonobo_window_add_popup
./src/file-manager/fm-directory-view.c:
bonobo_window_add_popup(
(get_bonobo_window(view), menu, popup_path);
```

幸运的是，`bonobo_window_add_popup` 似乎只从一个函数 `create_popup_menu` 中调用，如列表 11.10 所示。

# 列表 11.10。

```c
static GtkMenu *create_popup_menu(GtkTreeView *view, const char *popup_path)
{
    GtkMenu *menu;
    menu = gtk_menu_new();
    ...
    bonobo_window_add_popup(get_bonobo_window(view), menu, popup_path);
    ...
    return menu;
}
```

## 11.8. 使用 gdb 生成调用栈轨迹

为了解决这个问题，可以使用 gdb 的功能之一：gdb 可以在遇到断点时执行一组命令。通过使用该命令，我们可以告诉 gdb 在每次遇到断点时执行 `bt; cont`。现在，每次遇到断点时都会显示回溯并且应用程序继续运行。

现在我们需要查看实际的轨迹。我们可以在 nautilus 启动处的 `g_type_check_is_a` 中设置断点，当我们在创建弹出菜单并调用它时，gdb 将显示追踪信息。我们需要将追踪限制在仅弹出弹出时。要做到这一点，我们在 `fm_directory_view_pop_up_context_menu` 函数的开头和结尾各设置一个断点。当我们到达第一个断点时，在 `g_type_check_is_a` 中开始追踪；当我们到达第二个断点时，停止调试器。这会将回溯限制在在我们创建弹出菜单时生成的轨迹。最后，我们需要能够保存这些回溯信息以供事后处理。我们可以使用 gdb 的 log 将其输出到文件中，如列表 11.12 所示。

# 列表 11.12.

```
# 防止 gdb 停止输出满屏内容
set height 0
# 开启日志到文件（默认: gdb.txt）
# 关闭到屏幕输出
set logging redirect on
# 在即将创建弹出菜单时停下
break fm-directory-view.c:5730
```

