

无论视频内存的多少以及可能的平面数如何，我们都可以将所有类型的屏幕归纳为以下三种基本类别之一：

- 单色单平面系统
- 单色灰度系统
- 彩色系统

就 X 彩色图形编程而言，通常只需确定哪一类最能描述你的系统即可。在第一种情况下，客户端可以对所有颜色使用黑白。然而，如果客户端需要超过两种颜色，则别无选择，只能显示错误信息并退出。在第二种情况下，客户端应用程序可以用灰度颜色值代替其通常的颜色。在第三种情况下，程序可以使用 X 服务器数据库中提供的颜色值。

> Note
> 
> 调查可用视频系统类型的方法多种多样，但在大多数情况下，最好只是让用户能够自行选择颜色值，也许使用命令行选项或来自设置文件。X 中的彩色图形编程涉及一定程度的猜测，可能无法编写在运行 UNIX 和 Linux 的所有可能硬件上完全相同的软件。

## THE X COLOR DATABASE

在大多数情况下，通过使用标准颜色名称，你的程序最有可能产生可预测的彩色图形。颜色定义在存储在文件 rgb.txt 中的数据库中。该文件包含 X 服务器所知的颜色名称集合以及相关的 RGB 值。该文件中还包含以 gray0 到 gray100（或 grey0 到 grey100）为符号表示的灰度级别，按单整数步进。你可以在彩色或单色灰度系统上使用这些“颜色”。表 28.1 按声明顺序显示了来自 rgb.txt 数据库中的一些颜色。许多颜色有同义词——例如，hot pink 和 HotPink 是同一种颜色。一些权威资料指出该文件存储在路径 /usr/X11R6/lib/X11 中，但在我的系统上，我发现它在 /usr/X11R6/lib/X11 中，所以你可能需要寻找它。X 服务器使用该文件的编译版本——它实际上并不读取文本。

TABLE 28.1 SELECTED X COLOR NAMES FROM RGB.TXT

| snow | DarkSlateGrey | LightCoral |
| ghost white | dim gray | tomato |
| GhostWhite | DimGray | orange red |
| white smoke | navy blue | OrangeRed |
| WhiteSmoke | NavyBlue | red |
| antique white | cornflower blue | hot pink |
| AntiqueWhite | CornflowerBlue | HotPink |
| papaya whip | cyan | violet |
| PapayaWhip | light cyan | plum |
| blanched almond | LightCyan | blue violet |
| BlanchedAlmond | dark sea green | BlueViolet |
| bisque | DarkSeaGreen | purple |
| peach puff | sea green | medium purple |
| PeachPuff | SeaGreen | MediumPurple |
| seashell | forest green | thistle |
| honeydew | ForestGreen | gray0 |
| mint cream | sandy brown | grey0 |
| MintCream | SandyBrown | gray1 |
| azure | tan | grey1 |
| dark slate gray | chocolate | gray100 |
| DarkSlateGray | firebrick | grey100 |
| dark slate grey | light coral |  |

使用来自 rgb.txt 的颜色名称并不能保证客户端的图形以任何特定色调显示。然而，使用标准名称将选择实际颜色的责任放在系统管理员和用户身上。例如，在单色系统上，每种颜色都可以赋予灰度级别，尽管在这种情况下，让客户端本身选择 grayN（或 greyN）符号以确保相邻图形有区别仍然是好主意。更重要的是，由于实际颜色在不同显示器之间会有所不同，数据库给了系统管理员适当调整颜色值的机会——这一过程有时模糊地被称为“伽马校正”。因此，使用来自 rgb.txt 的颜色名称有助于确保 ForestGreen 真正看起来像它应该的那样郁郁葱葱，即使该颜色的实际 RGB 值在不同系统之间可能有所不同。

## ALLOCATING COLORS

调色板中的每个条目称为一个 colorcell。每个 colorcell 可以是两种类型之一——只读，或读写。只读 colorcell 可以在两个或多个客户端之间共享。读写 colorcell 只能由分配该单元的客户端使用。顾名思义，读写 colorcell 是可变的，但只能由分配的客户端更改。只读 colorcell 以类似方式由客户端分配，但可以被多个客户端共享。一旦分配，只读 colorcell 就永远不能被更改。更改只读 colorcell 的唯一方法是删除它，分配一个新的颜色，并重绘客户端的图形。

许多程序员认为读写 colorcell 更可取，因为它们可以轻松更改，但通常并非如此。因为读写 colorcell 不能在客户端之间共享，它们会占用调色板中宝贵的空间，并可能导致系统

