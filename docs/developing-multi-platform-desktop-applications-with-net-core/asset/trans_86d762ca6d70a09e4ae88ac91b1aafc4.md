

## 8.5.2 安装 GTK

### 8.5.2.1 在 Windows 上

自第二版（几年前）以来，GTK 工具包已不再发布二进制安装包。

尽管如此，独立的开发者通过充分利用 NullSoft 安装程序提供了这种类型的设置。当前的安装版本二进制文件可在他们的 GitHub 上获取。

![](img/3d310cc066dda6e2dfa67a650614076f_192_0.png)

此发行版（由 Tom Shoonjans 和 Alexander Shaduri 制作）集成了最新可用的 Gtk 工具包（3.24 版本）以及使其正确运行所需的所有依赖项。该最新版本于 2019 年 7 月 2 日发布，似乎是安装 GTK 工具包的一个可靠来源。您还将找到用于生成 Windows 上 GTK 运行时自定义安装程序的 NullSoft 脚本。

### 8.5.2.2 在 macOS 上

如前所述，在 macOS 上安装 GTK 可以通过使用“HomeBrew”（参见参考网页链接）并遵循下面描述的过程来完成。

![](img/3d310cc066dda6e2dfa67a650614076f_192_1.png)

如果您之前尚未安装 Brew，以下是安装它的方法，以及随后如何使用它安装 GTK 的方法。

- **A) 安装 Brew**

您可以通过在 macOS 终端提示符中执行以下命令行来安装 *brew*：

```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

结果应与描述中的一致（*图 7*）。

![](img/3d310cc066dda6e2dfa67a650614076f_193_0.png)

![](img/3d310cc066dda6e2dfa67a650614076f_193_1.png)

(*图 7*)

- **B) 安装 GTK**

安装 *Brew* 后，您可以轻松使用以下命令行（*公式*）安装 *GTK* 运行时和依赖项。这将安装 *GTK* 3 版本及其所有依赖项。

```
$ brew install gtk+3
```

如果软件包设置正确，此命令应产生以下输出。

```
Elana:~$ sudo apt-get install gtk3-3.0.18
Downloading http://launchpad-archive... 
... gtk+3.0.18 ... 
Unpacking gtk+3.0.18 ...
Processing triggers for man-db ...
...
Elana:~$ gnome-applets
Elana:~$ gtk+-3.0.18
  Total size: 1.1MB  
  Installed: 9.2MB
  
Downloading: gtk+3.0.18

Processing triggers for gde ...

Downloading: gtk+3.0.18
Installing:  
/usr/lib/x86_64-linux-gnu/gtk-3.0.18.so

Processing Gtk+
Elana:~$ ls
Desktop  Documents  Downloads  Music  Movies  Music
Nautilus  Pictures  Projects  Public
```

（图 8）

如果您未能成功安装，照例，您应修复可能出现的问题并从头开始重新安装软件包。

### 8.5.2.3 在 Ubuntu 上

GTK 原生安装在 ubuntu 桌面版本上（它是用于开发 Gnome 的工具），因此您不需要安装任何额外模块来运行 GTK GUI 应用程序。作为 ubuntu 的原生组件，GUI 的性能也将优于其他任何系统。

## 8.5.3 GTK# 介绍

现在，GTK 运行时在每个平台上都可用，我们可以开始解释如何从我们的 .NET Core 3 应用程序中使用它。GTK 运行时已有一个开发并经过验证的 .NET 包装器：GTK#。

该工具包在其最新版本中（通过采用 GTK# 的 .NET Standard 2.0）变成了多平台，因此可用于使用 .NET Core 3 开发多平台 GUI 应用程序。

GTK# 是 .NET 的图形用户界面工具包，该工具允许 .NET 开发者在 .NET 中使用 GTK+。

GtkSharp（这就是其发音方式）是 GTK 及其组件的 C# 包装器，这是之前针对 mono（以及 Gtk 2.xx）的 gtk-sharp 库的分叉版本。

最新版本的 GTK# 针对 GTK 3.22 版本，并以 .NET Standard 格式可用。其源代码采用开源许可证，并可在以下 GitHub 链接上获取。

![](img/3d310cc066dda6e2dfa67a650614076f_195_0.png)

GTK# 库也可通过 NuGet 软件包分发系统获取。除了基础的 GTK# 包装器外，还有一个专用软件包提供新的项目模板和项目项，用于使用 dotnet CLI 工具开发 GTK# 应用程序（适用于 .NET Core 3）。

![](img/3d310cc066dda6e2dfa67a650614076f_195_1.png)

这是一个非常便捷的应用程序包，它为开发者添加了使用 dotnet CLI 生成的新类型应用程序，还增加了创建新控件、窗口或对话框对象（包含 .glade 文件）的可能性。

模板软件包的安装可以使用下面描述的命令行完成（这是 dotnet CLI 安装新项目模板的标准命令行）：

```
C:\>dotnet new install GtkSharp.Template.CSharp --version 3.22.24.37
```

版本号是可选的，可以省略。这是安装此模板软件包后的结果屏幕（图 1）。

![](img/3d310cc066dda6e2dfa67a650614076f_196_0.png)

（图 1）

安装此软件包后，应可以使用“dotnet new”命令行获取 GTK 新项目模板，这些新项目包括：

- GtkSharp.Application：生成包含 .csproj、.cs、.glade 文件的完整 Gtk 应用程序。
- GtkSharp.Dialog：生成 .cs/.glade 文件，用于向现有项目添加对话框窗口。
- GtkSharp.Widget：为控件（小部件）生成 .cs/.glade 文件。
- GtkSharp.Window：生成基本 gtk.window 的 .cs/.glade 文件。

只有 GtkSharp.Application 是 .NET Core 的项目模板，其他的是用于向应用程序添加元素（Dialog、Widget、Window）的项目模板。生成的元素的默认名称是执行命令所在的文件夹名称（如果您未指定输出名称）。

您可以使用“dotnet --list”命令验证所有这些模板是否已正确安装，该命令列出了“dotnet new”命令可用的模板，如下面所述。

```
C:>dotnet new --list -lang C#
```

“-lang”选项用作筛选器，以仅选择 C# 类型的项。这是此命令的结果：

现在，您可以使用 .NET Core 3 命令行客户端创建一个新的 GTK 应用程序，如下面所述：

```
C:\>dotnet new gtkapp -n sampleGtkApp
```

此命令行将创建一个名为“sampleGtkApp”的 GTK 应用程序项目（这是新 dotnet CLI 命令的标准行为）。

创建模板应用程序使用 .glade 文件格式来描述 GUI。此格式可以加载到 Gtk.Builder 对象中（我们稍后将详细回顾这一点）。

您可以在以下参考链接中找到有关使用 GtkBuilder 的更多信息。

![](img/3d310cc066dda6e2dfa67a650614076f_199_0.png)

- http://gtkbuilder.org/
- http://gnome.org/gtkbuilder

在模板中，.cs 文件和 .glade 文件具有相同的名称，这使得开发者更容易修改窗口的两侧（前端和后端）。

生成的应用程序可以轻松修改和扩展；通过使用 Glade 编辑对应于主窗口的 xml 文件（.glade 扩展名）。

您可能注意到，此软件包生成的应用程序模板使用基于 XML 文件的 GUI 模型。但使用 GTK，您还可以通过内联 C# 代码实现 GUI，我们将在示例部分回顾这两种 GTK 实现类型。

在此之前，研究 GTK 界面设计器 Glade 是很有用的。

## 8.5.4 Glade：用户界面设计器

Glade 是一个允许在不手动编写代码的情况下设计和创建 GUI 的应用程序。该应用程序取代了 Stetic Gui 设计器（用于 Mono，跨平台 .NET 框架）。

与其前身一样，它是一个具有所见即所得（WYSIWYG）功能的快速应用程序开发（RAD）工具，使其易于开发 GTK+ GUI。Glade 是与编程语言无关的，因为它的含义是不生成任何代码，描述所设计 GUI 的文件根据标准 XML 格式进行编码。GtkBuilder 是此 XML 文件的格式。

