

# 9.7 image 对象

图像对象可以进行缩放、放大、下采样以及从一个图像对象移动到另一个图像对象。图像对象可以显示在包括按钮、标签和文本框在内的其他部件中。

标准的 Tk 分发版支持 X-Bitmap、GIF、便位图（Portable Pixmap）和便灰度图（Portable GrayMap）格式定义的图像。存在一些扩展提供了对 JPEG 和 PNG 等格式的支持。（请参见第 13 章关于 Jan Nijmans 为 Tk 增加更多图像支持的补丁。）本节节将解释如何创建和使用图像对象。

## 9.7.1 image 命令

为了在画布（canvas）上创建图像项，必须先创建一个图像对象。`image` 命令支持在 Tk 解释器中创建、删除和获取图像对象的信息。

`create` 命令从文件或内部数据创建图像对象，并返回访问该对象的句柄。

语法：`image create type ?name ?options?`

`image create` 创建指定类型的图像对象，并返回一个引用该对象的句柄。

**type** 将创建的图像类型。Tk 8.0 和 8.1 版本支持：
- photo- 一种彩色图形。
- bitmap- 一种双图形。

**?name?** 该图像的名称。如果留空，系统将分配一个格式为 `imageX` 的名称，其中 X 是唯一的数字值。

**?options?** 这些是特定于所创建图像类型类型的选项。我将讨论 bitmap 和 photo 的适当选项。

可以使用 `image delete` 命令删除图像。

语法：`image delete name ?name?`

`image delete` 删除命名的图像。

**name** 由 `image create` 命令返回的句柄。

`image` 命令可以获取单个图像或解释器中存在的所有图像的信息。

语法：`image height name`

语法：`image width name`

语法：`image type name`

`image height` 返回命名图像的高度。

`image width` 返回命名图像的宽度。

`image type` 返回命名图像的类型。

**name** 由 `image create` 返回的句柄。

语法：`image names`

`image names` 返回对象名称的列表。

当使用 `image create` 命令创建图像时，也会创建一个与该图像同名的命令。此图像对象可以通过其 `cget` 和 `configure` 命令来操作对象。这些命令的行为与其他部件的 `cget` 和 `configure` 命令相同。可以使用 `configure` 修改的配置选项取决于所创建的图像类型，并且与该命令提供的选项相同。

## 9.7.2 Bitmap 图像

位图图像（与画布项不同）通过前面描述的 `image create bitmap` 创建。该命令支持的选项包括：

- -background color 位图的背景颜色。如果此处留空（默认），则像素将是透明的。
- -foreground color 图像的前景颜色。默认为黑色。
- -data 定义图像的数据。必须与 X Window System 位图文件的格式相同。
- -file filename 包含数据的文件。X Window System 位图文件非常简单。它设计用于包含在 C 程序中，看起来如下：

```c
#define name_width width
#define name_height height
static unsigned char name_bits[] = {
    data, ...
};
```

好消息是这非常简单且易于构建。Unix 系统上的程序将让你构建位图文件，或者你可以使用 imagemick 转换 Windows 或 Mac 位图文件。

## 9.7.3 Photo 图像

photo 图像的数据可以是 PPM、PGM 或 GIF。数据可以是二进制格式，也可以在脚本中编码为 base64 数据。Base64 编码是一种将二进制数据转换为扩展最小的可打印 ASCII 字符的技术。所有支持 MIME 扩展的系统（大多数现代程序）都使用这种格式。虽然听起来很奇怪，将文件从二进制转换为 base64 最可移植的方法是将其保存，然后从保存文件中提取数据。

如果你在 Unix 系统上运行，可能安装了 `mmencode`。这些是 MIME 支持的一部分。CD-ROM 包含一个 Tcl 脚本，可以编码和解码 base64 文件。该脚本名为 `binary264.tcl`，位于示例目录下。该脚本使用了 Jan Wieck 开发的 `b64tools.tcl` 包，该包也在该目录下。

`image create photo` 命令支持多个选项，包括：
- -data string 定义此图像的 base64 编码数据。
- -file filename 包含二进制格式图像数据的文件。
- -format 图像数据的格式。Tk 默认尝试确定图像类型。在 8.0 版本中，此选项的可能值为 gif、pgm 和 ppm。

与 `image create bitmap` 命令一样，此命令会创建一个与新图像同名的命令，可以通过 `cget` 和 `configure` 命令来操作图像。photo 类型图像支持其他子命令，包括：

语法：`image copy sourceImage ?options?`

`image copy` 从 `sourceImage` 将图像数据复制到图像。选项包括：
- -from x1 y1 x2 y2 从源图像复制的区域。坐标定义了矩形的对角线点。
- -to x1 y1 x2 y2 复制到目标图像的区域。
- -shrink 如果必要，缩小图像以适应可用空间。
- -zoom 如果必要，放大图像以适应可用空间。

**语法：** `image get x y`

`image get` 返回坐标 x, y 处像素的值。颜色以三个整数返回，即红、绿、蓝强度。

**语法：** `image put data ?-to x1 y1 ?x2 y2?]`

`image put` 将新的像素数据放入图像对象中。数据是颜色值的字符串，可以是颜色名称或 #rgb 格式。默认情况下，这些像素将从左上角开始，跨越每一行，然后跨越下一行。

-to x1 y1 x2 y2 声明放置数据的位置。如果只定义了 x1, y1，则为图像的起始点；如果定义了 x1, y1 和 x2, y2，则为矩形的对角线点。

# 示例 9.7.1

```tcl
# 创建一个画布
canvas c -height 100 -width 300 -background white
# 创建一个 gif 格式的图像（使用 base64 编码的像素）
set img "R0lGODlhAQABIASUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVR422mP8z8BwAEQGAhCB0C7wAAAABJRU5ErkJggg====" 
# 注意：上面的 base64 字符串只是示例，实际应用中应为有效数据
# 假设 img 是 "R0lGODG4AAQAAAKEAP///AAADZ4NAD/ywAAAAQAAAC/8/8/8/8/8="
# 我们创建一个图像
image create photo i -data $img
```

# 示例 9.7.2

