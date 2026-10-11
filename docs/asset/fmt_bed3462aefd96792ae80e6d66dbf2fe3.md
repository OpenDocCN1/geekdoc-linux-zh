
`Xmountains` 程序是位于 `/Part07/Execute/Xmountains` 的标准软件包。使用 `xmountains` 命令启动它并观察其工作。`man` 页面描述了一系列你可以从命令行控制的选项。这里是基础的 `Xmountains` 图像。

![](img/35c1af90d4f3af9cd7cfd006c6b752f5_293_0.png)

## 在 Linux 上尝试 CAD

`Qcad` 是一个用于平面图、机械图和建筑视图的完整计算机辅助绘图系统。`Qcad` 使用标准的 `dxf` 格式文件，因此你可以与其他使用相同格式的绘图程序协同工作。

> 注意：`Qcad` 也运行在其他平台上，如 `Windows`。请访问 `www.qcad.org` 获取信息。

`Qcad` 软件包位于 CD 的 `/Part07/Execute/Qcad` 目录下。你可以使用标准的 `rpm` 命令安装软件包，然后从任何图形命令行使用 `qcad` 命令启动程序。

安装 `Qcad` 软件包后，你可以使用软件包包含的示例项目尝试这个强大的工具。选择 `File -> Open` 菜单项从 `/usr/libb/qcad/examples` 目录打开示例项目。在这里你可以在 `Qcad` 的主窗口看到其中一个示例项目（`example103.dxf`）。

![](img/35c1af90d4f3af9cd7cfd006c6b752f5_294_0.png)

`Qcad` 窗口右侧的列包含绘图层列表。你可以使用列表上方的按钮添加新层或更改现有层的属性（例如显示颜色）。主工具栏上的按钮让你选择是查看图层列表还是可用的库。工具栏的其他部分控制缩放选项，这些选项也可以通过 `Zoom` 菜单可用。

## 让你的系统变得有趣

选择 `Options > General Preferences` 会弹出一个对话框，其中你可以从尺寸、打印和语言等九个类别中为 `Qcad` 选择设置。`Options > Current Drawing Settings` 对话框显示了适用于当前项目的几类信息。

![](img/35c1af90d4f3af9cd7cfd006c6b752f5_295_0.png)

你在窗口右侧看到的工具栏用于绘图。当你选择某些工具时，工具集会更新以反映你的选择。例如，点击 `Edit` 按钮（在首次启动程序时出现）会导致一组新工具。如果你点击 `Arc` 工具，会出现一组新的圆弧绘制工具。

> 注意：在图纸上点击右键，可以从显示的工具集中回退上一级。

## 将 Linux 转换为 Web 服务器

![](img/35c1af90d4f3af9cd7cfd006c6b752f5_296_0.png)

# 将 Linux 转换为 Web 服务器

`Linux` 最流行的用途之一就是作为 Web 服务器。事实上，你购买的几乎任何 `Linux` 产品都会包含一个 `Apache` Web 服务器。`Apache` 是世界上最流行的 Web 服务器，占据了约 50% 的市场（如果我们可以称之为市场的话，毕竟 `Apache` 是免费的）。有关 `Apache` 优势和调查统计数据的详情，请访问 `NetCraft` 官网 `www.netcraft.com`。

然而，安装并运行 Web 服务器并不等同于将 Web 的所有力量尽在掌握。`Apache` 可以完成许多默认配置中不包含的功能。本部分描述了你可以将哪些软件添加到 `Apache` 本身或用于你的 Web 服务器上，以增强 `Apache` 的功能、收集额外的统计信息，或准备 `Apache` 用于高流量和高安全的 网站。

如果你的系统中没有最新版本的 `Apache`，光盘中包含了 1.3 版本的软件包，位于 `/Part08/Execute/Apache` 和 `/Part08/Source/Apache_1.3.x` 目录下。如果你对 `Red Hat 7` 的标准工作站安装，那么你没有 `Apache`，因为它被正确地认为是一个服务器包。你可以使用标准的 `rpm` 命令安装此书附带的光盘上的包来安装它。我建议同时安装基础 `Apache` 软件包和 `apache-manual1` 软件包。如果你想使用模块进行任何大量工作，还应该考虑安装 `Apache` 源码包（同样使用标准的 `rpm` 命令）。在后续章节中关于使用 `Apache` 源码的讨论中，假设你已经使用了这些软件包。

由于 `Apache` 的进展非常快，我还包含了最新版本的 `Apache`，这些版本比 `Red Hat 7` 包含的版本更高。这些版本位于光盘的目录 `/Part08/Source/Apache_1.3.x`（1.3 系列，当前标准）和 `/Part08/Source/Apache_2.x`（2.x 系列，仍在开发中，尚未在生产服务器上使用）。我没有直接讨论后续版本，但可以使用这些代码来探索最新的 `Apache` 特性。

要了解更多关于 `Apache` 的信息，请访问 `Apache` 项目网站 `www.apache.org`，或者查看《Apache Week》杂志，它包含许多实用的文章和一个可搜索的过期数据库——地址为 `www.apacheweek.com`。

![](img/35c1af90d4f3af9cd7cfd006c6b752f5_297_0.png)

## 使用模块扩展 Apache

Web 服务器软件最重要的进展之一是了在 `Apache` 中使用模块的能力。当 Web 页面运行 `CGI` 脚本来处理表单或准备自定义 `HTML` 页面时，`Linux` 系统需要一些开销（CPU 时间和内存）来启动并管理该作为独立程序的脚本。此外，脚本只能响应普通的浏览器请求；它无法影响 `Apache` 的行为。

通过向 Web 服务器本身添加功能来扩展 `Apache`。模块是一段代码（用 `C`、`C++` 或 `Perl` 编写），它会成为 Web 服务器的一部分，允许你自定义 `Apache` 特性。当然，并不是每个人都能编写新的 `Apache` 模块，因此本节描述了可以下载并用于 `Apache` 的几十个模块。其中许多包含在光盘中。你可以使用这些模块中的任何一个为你的 Web 服务器添加功能。

## 为你的 Apache Web 服务器添加模块

由于 `Apache` 以源代码形式免费分发，大多数认真的网站管理员都会下载 `Apache` 并编译他们自己的副本。这允许网站管理员控制 `Apache` 中包含的确切功能，并使用最新版本（从而获得所有可能的安全修复和程序增强）。

默认情况下，`Apache` 不包含源代码中包含的所有可能的模块。例如，如果你想学习编写自己的模块，应该添加一个名为 `mod_example` 的模块。模块可以通过两种方式添加到 `Apache`：

- 将模块源码与 `Apache` 源码一起包含，并将所有内容编译成单个二进制文件。
- 在 `Apache` 运行时，作为动态共享对象（`DSO`）即时地将模块添加到 `Apache`。这有点类似于使用 `Windows DLL` 或 `UNIX` 共享库。

# 将 Linux 转换为 Web 服务器

两种方法都可行，但使用 `DSO` 通常比重新编译服务器更容易。许多网站管理员选择 `DSO` 方法来尝试。我将向你展示如何使用这两种方法。使用 `DSO` 通常比处理源码简单得多。

要让模块成为 `Apache` 的一部分，你需要将它们编译到 `Apache` 中或创建一个 `DSO` 文件。`Apache` 已经知道的模块（因为它们是标准源代码的一部分）可以使用这些命令轻松编译并启用 `DSO` 文件。此示例将 `rewrite` 模块编译到 `Apache` 中，同时也作为 `DSO` 文件。它还在 `httpd.conf` 文件中添加了 `LoadModule` 行，以便 `Apache` 在启动时加载该模块。

许多其他模块可供 `Apache` 使用，如本节后文所述。在 `httpd.conf` 文件中添加 `LoadModule` 行，以便 `Apache` 在启动时加载该模块。

若要从 CD 中选择一个想要编译进 `Apache` 的模块，请使用以下命令。`--add-module` 选项告诉 `configure` 脚本查找新模块的源码：

```bash
$ ./configure --prefix=/path/to/apache \
--add-module=/path/to/mod_foo.c
```

```bash
$ make
$ make install
```

这些命令会将模块拷贝到 `Apache` 源码树的 `src/modules/extra/` 目录下并在编译 `Apache` 时激活新模块。如果您想将新模块制作为 `DSO` 文件而不是仅将其编译到 `Apache` 中，请使用这些命令。`--enable-shared` 选项导致模块被编译为 `DSO`：

```bash
$ ./configure --prefix=/path/to/apache \
--add-module=/path/to/mod_foo.c \
--enable-shared=module_name
```

```bash
$ make
$ make install
```

如果您想使用 `Apache` 包含的所有可用模块，请使用这些命令，这些命令使用了 `Apache` 在源码目录中可以找到的所有模块（但不会使用您可能想要尝试的任何额外非标准模块）：
