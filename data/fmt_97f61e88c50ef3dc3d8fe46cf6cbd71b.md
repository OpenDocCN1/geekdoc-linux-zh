
存储这些关联关系的文件名必须具有`.mime`扩展名，并且在`/usr/share/mime-info`目录必须是唯一的（对于此示例，`Backprop.mime`是一个不错的选择）。在某些情况下，使用正则表达式来识别文件更为合适。为了支持这一点，你可以使用`regex:`字段。例如，接下来的内容将所有以`.wgt`、`.net`等结尾的文件与MIME类型`application/x-backprop`关联起来，这等同于之前使用`ext:`字段的`backprop.mime`文件：

```
application/x-backprop

regex: .wgt

regex: .net

regex: .exm

regex: .WGT

regex: .NET

regex: .EXM
```

另一个示例，下面的内容将所有以`README.`开头的文件关联到MIME类型`text/x-readme`：

```
text/x-readme

regex: README..*
```

你可以参考文件`/usr/share/mime-info/gnome.mime`以获取更多示例。

事实证明（正如你可能观察到的那样），根据文件名识别文件内容是一项风险业务。没有什么禁止用户将Microsoft Word文件重命名为`myimage.jpg`，或将图像文件重命名为`foo.txt`，从而导致对文件内容的识别不准确。因此，系统在运行上述描述的MIME类型关联之前，会尝试检查文件内容以确定内容类型。只有当这无法识别文件时，才会使用文件名。

GIF文件提供了使用“魔数”辅助识别文件的一个著名示例。每个GIF文件都会在偏移量0处存储ASCII码`GIF8`。PNG文件也类似，在处理程序中存储`PNG`，例如`GIMP`和`Photoshop`等程序在尝试确定用户打开的图像文件的编码时会寻找这些字符串。

魔数映射是在两个文件之一中：`/etc/gnome-vfs-mime-magic`或`/etc/mime-magic`。截至本文，像`Backprop`这样的新应用程序还没有指定魔数映射的机制。然而，目前你至少应该检查这两个文件，以确定你是否正在编写这些文件中定义的任何映射。（检查冲突的简单方法是在如`Nautilus`等文件管理器中查看由你的程序生成的其中一个文件）

GIF文件提供了使用“魔数”辅助识别文件的一个著名示例。每个GIF文件都会在偏移量0处存储ASCII码`GIF8`。PNG文件也类似，在处理程序中存储`PNG`，例如`GIMP`和`Photoshop`等程序在尝试确定用户打开的图像文件的编码时会寻找这些字符串。

魔数映射是在两个文件之一中：`/etc/gnome-vfs-mime-magic`或`/etc/mime-magic`。截至本文，像`Backprop`这样的新应用程序还没有指定魔数映射的机制。然而，目前你至少应该检查这两个文件，以确定你是否正在编写这些文件中定义的任何映射。（检查冲突的简单方法是在如`Nautilus`等文件管理器中查看由你的程序生成的其中一个文件）

### 与文件关联图标

在描述了MIME类型映射之后，下一步是将MIME类型与图标关联。为了实现这一点，必须创建一个`.keys`文件。让我们看看`gnumeric`的keys：

| MIME类型 | 打开 | 查看 | 图标路径 |
| :--- | :--- | :--- | :--- |
| application/x-ms-excel | gnumeric %f | gnumeric %f | /usr/share/pixmaps/gnome-application-x-ms.png |
| application/vnd-lotus-2-3 | gnumeric %f | gnumeric %f | /usr/share/pixmaps/gnome-application-vnd-lotus-2-3.png |
| application/x-applix-spreadsheet | gnumeric %f | gnumeric %f | /usr/share/pixmaps/gnome-application-x-applix-spreadsheet.png |
| application/x-ole | gnumeric %f | gnumeric %f | /usr/share/pixmaps/gnome-application-x-ole.png |
| application/x-generic-spreadsheet | gnumeric %f | gnumeric %f | /usr/share/pixmaps/gnome-application-x-generic-spreadsheet.png |

如你所示，`gnumeric`文件包含多个格式如下的章节：

```
mime type

open=command

view=command

icon-filename=path
```

对于`Backprop`，我们将从中学习并为支持的每种文件创建新的MIME类型（`.net`、`.wgt`和`.xem`），然后为每种类型指定图标。首先，让我们如下修改`backprop.mime`：

```
# mime types for backprop ...

application/x-backprop-network

extext: net NET

application/x-backprop-weights

extext: wgt WGT

application/x-backprop-exemplar

extext: em EXM
```

# 186 第 4 章 安装与部署

```
application/x-backprop-network:

open-backprop -n %f

view-backprop -n %f

icon-filename=/usr/share/pixmaps/

backprop-application-x-network.png
```

```
application/x-backprop-weights:

open-backprop -w %f

view-backprop -w %f

icon-filename=/usr/share/pixmaps/

backprop-application-x-weights.png
```

```
application/x-backprop-exemplar:

open-backprop -e %f

view-backprop -e %f

icon-filename=/usr/share/pixmaps/

backprop-application-x-exemplar.png
```

此时，该文件的内容应该是自而易见的。图像文件的大小应该是48 x 48。

## 手页 (Man Pages)

帮助页可以追溯到UNIX早期。`man`命令从命令行发出，用于生成有关命令、文件或编程接口的基本信息。UNIX手册分为几个部分，包括（但不限于）第1部分的命令（例如`cat`）、第2部分的系统调用API（例如`open()`）、第3部分的库API（例如`fopen()`）以及第5部分的文件（例如`/etc/passwd`）。上述示例的命令行如下所示：

```
$ 1 cat

$ 2 open

$ 3 fopen

$ 5 passwd
```

当帮助页章节不具有歧义时（除`passwd`以外的所有情况如此），可以省略手册编号参数。例如：

```
$ man cat
```

## 第 15 项：为原生安装程序提供支持

如果你不确定命令的，或者不确定它在哪个手册页中，你可以指定`-k`参数，这将导致`man`报告所有包含你提供的文本的页面。例如，假设我想找到一个从C语言程序读取目录内容的系统。我可能会执行以下命令：

```
$ -k directory

<此处省略了多行输出>

pawd (1) - 打印自动挂载的工作目录

pax (1) - 读取和写入文件归档并

复制目录层次结构

pwd (1) - 打印当前/工作目录的名字

pwd (n) - 返回当前工作目录

readdir (2) - 读取目录条目

readdir (3) - 读取目录

<此处省略了多行输出>
```

从这里，我可以看到`readdir(2)`和`readdir(3)`都描述了能够读取目录内容的API。假设我想查看第2部分的系统调用接口，然后可以执行以下命令：

```
$ man 2 readdir

READDIR(2) Linux 程序员手册 READDIR(2)

NAME

readdir - 读取目录条目

SYNOPSIS

#include <unistd.h>

#include <linux/dirent.h>

#include <linux/unistd.h>

_syscall(3, readdir, uint, fd, \

struct dirent *, dirp, uint, count);
```
