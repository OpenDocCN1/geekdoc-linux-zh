
`QPaintDevice` 是一个二维空间的抽象，你可以使用 `QPainter` 类向其进行绘制。

`QPaintDeviceMetrics` 类封装了 `QPaintDevice` 的物理尺寸信息。

### `QPainter`

此类提供了一些在 `QPaintDevice` 上绘制的方法，速度非常快。

#### 一种可能的实例化
```cpp
QPainter p( this );
```

#### 使用示例
```cpp
QPushButton *pb = new QPushButton( this );
QPixmap pm = QPixmap( "ButtonBgd.bmp" );
pb->setPixmap( pm );
QPainter p( &pm, pb );
p.begin();
p.drawText( pb->rect(), AlignCenter, "Click Me" );
p.end();
```

提供了许多常用绘制形状（包括文本）。Qt 文档中包含许多示例。

#### `QPen` 和 `QBrush`

`QPen` 定义了 `QPainter` 的轮廓绘制样式和颜色。`QBrush` 定义了 `QPainter` 的填充样式和颜色。

#### `QPicture`

`QPicture` 是一个类，它捕获离屏绘制设备中的 `QPainter` 命令，并对这些命令进行序列化，以实现平台无关的重放。Windows 程序员会认出这些是元文件。序列化数据可以保存和恢复。

#### 一种可能的实例化
```cpp
QPicture *pic = new QPicture();
```

#### 使用示例
```cpp
// 创建并保存一个新图片
QPicture *pic = new QPicture();
QPainter p;
p.begin( pic );
p.drawText( pb->rect(), AlignCenter, "Some Text" );
p.end();
pic->save( "some_text.pic" );

// 加载并显示该图片
QLabel *l = new QLabel( this );
QPicture newpic;
newpic.load( "some_text.pic" );
QPainter np;
np.begin( l );
np.drawPicture( newpic );
np.end();
```

## `QPixmap`

`QPixmap` 是一个离屏绘制设备。大多数接受图像或图标作为参数的 Qt 小部件方法都假设该参数是一个 `QPixmap`。

#### 一种可能的实例化
```cpp
QPixmap pix = QPixmap( "forest.bmp" );
```

#### 使用示例
```cpp
QPixmap pix = QPixmap( "forest.bmp" );
QLabel *l = new QLabel( this );
l->setPixmap( pix );
```

由于我花费大量时间在 Windows 2000 上编码，我通常使用 Windows 绘图程序创建图标，并以 Windows 位图格式 `.bmp` 保存它们。虽然该格式对于嵌入式图形并不直接有用，但你可以利用提供的 `load()` 和 `save()` 方法将图像转换为 XPM 格式。然后，你可以将 XPM 图像嵌入到你的代码中，如下所示：
```cpp
#ifndef NEED_CVT
#include "pixmaps/new_icon.xpm"
#endif
QPixmap new_ico;
#ifdef NEED_CVT
new_ico.load( "new_icon.bmp" );
new_ico.save( "pixmaps/new_icon.xpm", "XPM" );
#else
new_icon = QPixmap( (const char **)new_icon );
#endif
```
这种方法使得通过条件编译即可批量转换整套新的工具栏图标变得非常容易，极大地简化了项目部署。

## `QPNGImagePacker`

此类对于创建压缩的 PNG 动画图像非常有用。

#### 一种可能的实例化
```cpp
QFile f( "anim.png" );
f.open( IO_WriteOnly );
QPNGImagePacker p( f, 8, 0 );
```

#### 使用示例
```cpp
QFile f( "anim.png" );
f.open( IO_ WriteOnly );
QPNGImagePacker p( f, 8, 0 );
QImage img = myLabel->pixmap().convertToImage();
p.packImage( img );
```

鉴于 Unisys Corporation 对 LZW 压缩使用态度的限制，我建议使用 PNG 图像格式用于动画，以避免在某些国家所需的授权问题。

## `QPrinter`

`QPrinter` 是用于打印机的绘图设备。在 Microsoft Windows 系统上，`QPrinter` 使用现有的打印机驱动器和原生 spooler。在 Linux 系统上，`QPrinter` 生成 PostScript 输出，并将其发送到您选择的 spooler。

#### 可能的实例化
```cpp
QPrinter *p = new QPrinter();
```
在线文档提供了详细的示例。

## `QRegion`

`QRegions` 定义了 `QPainter` 的剪裁区域。

#### 可能的实例化
```cpp
QRegion r( QRect(10, 10, 50, 50), QRegion::Ellipse );
```

#### 使用示例
```cpp
QLabel *l = new QLabel( this );
QPixmap pic = QPixmap( "my_square_pic.bmp" );
QRegion r( QRect( 0, 0, pic.width(), pic.height()), QRegion::Ellipse );
QPainter p;
p.begin( l );
p.setClipRegion( r );
p.drawPixmap( 0, 0, pic );
p.end();
```

## 文本支持

以下类提供支持文本显示所需的数据和方法。

### `QFont`, `QFontInfo` 和 `QFontMetrics`

`QFont` 提供针对平台相关文本字体的封装。`QFontInfo` 提供关于指定字体的一般信息。`QFontMetrics` 提供关于字体的度量信息。

#### 使用示例
```cpp
QFont f( "Helvetica", 10 );
setFont( f );
int fw = fontMetrics().width( "Hello" );
int fh = fontMetrics().height();
QLabel *l = new QLabel( "Hello", this );
l->setFixedWidth( fw );
```

### `QSimpleRichText`

`QSimpleRichText` 封装了 Qt 简化版富文本的实现。您主要将使用它来为自定义控件添加富文本绘制支持。

#### 可能的实例化
```cpp
QSimpleRichText rt( "<b>Boldly</b> going", font() );
```

#### 使用示例
```cpp
QLabel *l = new QLabel( this );
QSimpleRichText rt( "<b>Boldly</b> going", font() );
QPainter p;
p.begin( l );
rt.draw( &p, 0, 0,
         QRegion( QRect( 0, 0, rt.widthUsed() ),
                  rt.height() ),
         palette());
p.end();

// 更简单的方法：
l->setRichText( "<b>Boldly</b> going" );
```
如上述示例所示，Qt 控件的一个有限子集支持 Qt 富文本实现。这肯定会随时间发生变化。在此期间，您可以使用 `QSimpleRichText` 在任何绘图设备上实现 Qt 富文本。

### `QStyleSheet`

`QStyleSheet` 提供了用于 Qt 简化富文本渲染机制的基本样式集合。

#### 可能的实例化
```cpp
QStyleSheet *ns = QStyleSheet::defaultSheet();
```
通过向样式表添加 `QStyleSheetItems`，您正在为该样式表添加新的标签支持。

## 输出控件

以下控件仅用于输出或显示目的。

### `QFrame`

框架（Frame）是控件周围的图形边框，或者它可以呈现为垂直或水平线。`QFrame` 是那些具有框架或具有可选框架（如 `QLabel`）的控件的基类。
