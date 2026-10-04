

-   可以使用 `canvasName coords` 命令访问或修改可绘制项的坐标。

    语法：`canvasName coords tagOrId ?x1 y1? ... xn yn?`

-   可以使用 `canvasName` 命令在画布上移动可绘制项。

    语法：`canvasName move tagOrId xoffset yoffset`

-   通过 `canvasName bbox` 命令返回可绘制项占据的空间。

    语法：`canvasName bbox tagOrId`

-   通过 `canvas-Name find` 命令返回符合搜索标准的项项列表。

    语法：`canvasName find searchSpec`

-   可以使用 `canvasName raise` 命令和 `canvasName lower` 命令修改可绘制项在显示列表中的位置。

    语法：`canvasName raise tagOrId ?abovetagOrId?`

    语法：`canvasName lower tagOrId ?belowtagOrId?`

-   通过 `font families` 命令返回可用字体列表。

    语法：`font families ?-displayof windowName`

-   通过 `font measure` 命令返回在特定字体中显示字符串所需的水平空间。

    语法：`font measure font ?-display windowName? text`

-   通过 `font actual` 命令返回与请求字体最匹配的字体。

    语法：`font actual font ?-displayof windowName?`

-   可以使用 `bind` 命令将动作绑定到组件的事件上。

    语法：`bind widgetName eventType script`

-   可以使用 `canvasName bind` 将动作绑定到画布组件内可绘制项的事件上。

    语法：`canvasName bind tagOrId eventType script`

## 9.8 底部总结

可以使用 `image create` 命令创建双色（位图）和多色（照片）图像。

语法：`image create type ?name? ?options?`

-   可以使用 `image delete` 命令删除图像。

    语法：`image delete name ?name?`

-   通过 `image height`、`image width` 和 `image type` 命令返回关于图像的信息。

    语法：`image height name`

    语法：`image width name`

    语法：`image type name`

-   通过 `image names` 命令返回脚本中当前定义的图像列表。

    语法：`image names names`

-   可以使用 `imageName copy` 命令将照片图像像素数据从一个图像复制到另一个图像。

    语法：`imageName copy sourceImage ?options?`

-   可以使用 `imageName get` 和 `imageName put` 命令访问或修改照片图像像素数据。

    语法：`imageName get x y`

    语法：`imageName put data ?to x1 y1 ?x2 y2??`

-   `canvas create bitmap` 命令和 `image create` 命令不同，但可以实现等的效果。

| canvas create bitmap | image create bitmap |
| :--- | :--- |
| 可以访问内部位图 | 可以使用脚本内定义的数据 |
| 可以通过以下方式引用数据文件： | 可以通过以下方式引用数据文件：-file |
| @filename | |

可以通过以下方式修改前景色颜色：

```
cvsName create bitmap \
-foreground $color
imageHandle configure \
-foreground $color
```

## text 组件和 html_library

输入（entry）和标签（label）组件适用于具有短提示和少量待输入数据的应用程序，即类似于填写表单的程序。然而，某些应用程序需要允许用户显示、输入或编辑大量文本。text 组件支持了这些需求。

text 组件支持：

-   emacs 风格的编辑。
-   滚动条。
-   单份文档中的多种字体。
-   对单个字符或多个字符的字符串进行标记（类似于将标签应用于画布对象的方式）。
-   标记文本中的位置。
-   在文本显示中插入其他 Tk 组件或图像。
-   将事件绑定到单个字符或多字符字符串。

## 第 10 章 text 组件和 html_library

使用 text 组件构建的包之一是 Stephen Uhler 编写的 `html_library`。它不是 Tcl/Tk 分发版的一部分，但可以通过以下地址 获取：

ftp.smli.com:/pub/tcl/html_library-0.3.tar.gz。

该扩展程序将渲染 html 文本，并为链接和图像提供钩子。

本章介绍了 text 组件和 html 库。

## 10.1 text 组件概述

应用程序可以创建多个文本窗口，这些窗口可以显示在帧（frame）、画布或另一个 text 组件中。

text 组件的内容通过行和字符位置进行寻址。

text 组件的内容维护为一组列表。每个列表包含要显示的文本字符串，以及与该文本字符串相关的任何标签、标记、图像注释和窗口注释。

如果文本字符串大于 text 组件的宽度，可以将组件配置为将文本换行到多行（在单词边界处或行尾容纳的最后一个字符处）或截断行。请注意，允许文本换行到多行会导致显示的行数与文本内部表示中的文本字符串数量不同。在引用 text 组件内的位置时，行和字符位置指的是文本的内部表示，可能并未显示。

当滚动条连接到 text 组件时，用户可以修改屏幕上显示的行数。这不会影响 text 组件的内容，行和字符位置仍然反映文本的内部表示，而不是显示的文本。例如，如果用户滚动到文档底部，行和字符位置...

