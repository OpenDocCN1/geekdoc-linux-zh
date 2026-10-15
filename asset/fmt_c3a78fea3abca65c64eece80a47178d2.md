
列表 4.7：绑定两个属性。

# 第三部分

## GTK+

### 第5章

#### 5.1 `main()` 函数和 EditApp

虽然在 schema 中没有体现，但 GTK+ 应用程序的入口——正如每个 C 程序一样——是 `main()` 函数。要创建一个 GTK+ 应用，在 `main()` 中主要的事情是创建一个 `GApplication` 实例或其子类。在 schema 中我们看到 `GerritApp` 是 `GtkApplication` 的子类，因此 `main()` 函数创建了一个 `GerritApp`。

`GApplication` 是 `Gio` 库的一部分，实现了与用户界面无关的功能……图 5.1 第 61 页展示了 `gedit` 的代码架构。

¹https://wiki.gnome.org/Apps/Gedit
²https://wiki.gnome.org/Projects/GtkSourceView

![](img/078dc81c39b3622bb7d98dea523cc81_61_0.png)

图 5.1：`gedit` 编辑器的简化版代码架构

进程唯一性（Process uniqueness）有几个优点，这里举几个具体的例子：

- 对于具有标签页文档界面的应用程序，当在像 `Nautilus` 的管理器中点击文件时，可以在新标签页中打开文件，而不是为每个文件创建一个新窗口。为了这项工作，需要某种形式的进程间通信；
- 应用程序不需要同步其状态和不同进程。为了便于解释，假设在 `gedit` 中用户创建了自定义的“构建工具”，用于编译当前文件或项目。`gedit` 将自定义构建工具保存在 XML 文件中，并显示在菜单中以执行它们的命令。在 Linux 上，该 XML 文件例如保存在用户的 `~/.local/share/` 目录下。如果没有唯一性，如果其中一个 `gedit` 进程修改了自定义工具，其他 `gedit` 进程将必须重新加载 XML 文件，并且需要确保没有竞态条件（两个不同的进程同时修改同一个 XML 文件）。有了唯一性，这个问题就不存在了，`gedit` 窗口共享相同的应用程序状态，开发者可以假设每个用户只有一个进程可以修改 XML 文件³；用户仍然有手动编辑 XML 文件的可能性，但在那种情况下应用程序是单例运行的，且用户应该通过 GTK（提供这些工具）来修改工具。

`GApplication` 的另一个重要特性是运行主事件循环。`GLib` 主循环在第 2.3 节第 31 页中描述。使用 `GApplication`，这通过 `g_application_run()` 函数实现。`gedit` 中 `main()` 函数的简化版本如下：

```
int
main (int argc,
    char**argv)
{
GEditApp *app;
int status;
/* 在此处初始化 i18n (国际化)。 */
app = gedit_application_new();
status = g_application_run(G_APPLICATION (app), argc, argv);
g_object_unref(app);
return status;
}
```
