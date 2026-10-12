

# **QColor 和 QColorGroup**

QColor 类提供了颜色属性的抽象。该类处理动态的智能分配与释放，并提供了用于指定 RGB 或 HSV 颜色的构造函数。

颜色组是对小部件可能使用的常见一组颜色属性的封装。如果你想更改小部件的默认前景色、背景色等，你还需要阅读关于 QPalette 的内容。

## 一种可能的实例化

```cpp
QColor text( "blue" );
QColor bgd( "#e0e0e0" );
QColorGroup *lc = new QColorGroup();
lc->setColor( QColorGroup::Foreground, text );
lc->setColor( QColorGroup::Background, bgd );
```

## 使用示例

```cpp
QLabel *l = new QLabel( "Color Label", this );
QColor text( "blue" );
QColor bgd( "#e0e0e0" );
QColorGroup lc = l->palette().active();
lc.setColor( QColorGroup::Foreground, text );
lc.setColor( QColorGroup::Background, bgd );
QPalette *pal = new QPalette( lc );
l->setPalette( pal );
```

# **QPalette**

QPalette 封装了用于表示不同小部件状态（正常、禁用和激活）的 QColorGroup。

## 一种可能的实例化

```cpp
QPalette *pal = new QPalette( QColor( "red" ) );
```

## 使用示例

```cpp
QPalette pal( QColor( "red" ) );
QPushButton *pb = new QPushButton( "Stop!", this );
pb->setPalette( pal );
```

# 图形图像输出支持

以下类提供了必要的支持，用于将图形图像数据输出到支持使用 QPainter 的小部件，或输出到图形输出设备。

# QBitmap

QBitmap 类提供了一种离屏的单色（单比特深度）绘制机制。

## 一种可能的实例化

```cpp
QBitmap bm;
```

## 使用示例

```cpp
QBitmap bm;
bm.load("arrow.xbm", "XBM");
```

QBitmap 的用途包括：

-   光标和光标掩码
-   画笔
-   小部件掩码

光标和光标掩码在 QCursor 的在线参考文档中有介绍。画笔将在本章稍后讨论。小部件掩码的一个示例（一个椭圆形的、3D 的、动画按钮）可以在本书附带的 CD 中的 chapter-examples 目录下的 QBitmap 目录中找到。我不赞成这种“噱头”，但它仍然是一个很好的视觉演示。

# QCursor

QCursor 是鼠标光标属性的封装。几乎任何有效的 QBitmap 都可以用来创建新的鼠标光标，并且预定义了合理的平台相关默认值。

## 一种可能的实例化

```cpp
QCursor wait( QCursor::WaitCursor );
```

## 使用示例

```cpp
setCursor( QCursor( QCursor::WaitCursor ) );
```

# **QIconSet**

此类提供了一组各种尺寸的图标，并提供了表示启用或禁用视觉队列的图标。通常你将在 QToolButton 的图标中使用图标集。

## 一种可能的实例化

```cpp
QPixmap p = QPixmap( "pix.bmp" );
QIconSet ico( p );
```

## 使用示例

```cpp
#include "myicon.xpm"
QPixmap p = QPixmap( (const char **)myicon );
QToolButton *toolb = new QToolButton( p, "Save",
                         "Save this document",
                         this, SLOT(save()) ),
              mytools, 0 );
toolb->setIconSet( QIconSet( myicon ) );
connect( this, SIGNAL(pixmapSizeChanged( bool )),
         toolb, SLOT(setUsesBigPixmap( bool )) );
```

# **QImage**

QImage 是平台无关的图像表示，提供了对逐像素图像数据的直接访问。

## 一种可能的实例化

```cpp
// 创建一个 640x480 的灰度图像
QImage i( 640, 480, 1, 2 );
```

## 使用示例

```cpp
QImage i, mirror;
if( i.load( "Pix.bmp", "BMP" ) == true) {
    mirror = i.mirror( true, false );
} else {
    mirror = i;
}
```

# **QMovie**

QMovie 增量加载动画图像，并提供了用于处理在提供绘制设备的小部件上显示动画的方法。通常你将在 QLabel 上实现电影，但 QPushButton 也同样适用。

## 一种可能的实例化

```cpp
QMovie *m = new QMovie( "flix.gif" );
```

## 使用示例

```cpp
#include "world.h"

// 创建一个包含 QMovie 的标签
movieLabel = new QLabel(this );
// 使用原始 GIF 数据加载 QByteArray
barray.setRawData( (const char *)world, world_len);
movie = QMovie( barray );
movie.setSpeed( 100 );
movie.connect( &status, this,
           SLOT( animStat(int)));
movieLabel->setMovie( &movie );
movieLabel->setMargin( 0 );
movieLabel->setFixedSize( 64+movieLabel->frameWidth()*2,
                          64+movieLabel->frameWidth()*2 );
movie.pause();
```

请注意，内置的 GIF 支持并非自动提供，需要在配置你的 Qt 安装时具体包含。这是因为 GIF 图像格式是专有的，并且因为在某些国家（特别是美国）GIF 压缩算法需要获得许可。Unixys 毫无疑问会赞赏你关于软件专利法这一主题的任何反馈。

如果你不想从 Unixys 购买 Lempel-Ziv-Welch 软件许可证来实现 QMovie，你可以使用任何良好的点处理程序以 PNG 格式创建动画帧，然后使用 QPNGImagePacker 创建压缩的动画图像。

# **QPainterDevice 和 QPaintDeviceMetrics**

QPaintDevice 是一个二维空间的抽象，你可以使用 QPainter 类向其进行绘制。

QPaintDeviceMetrics 类封装了 QPaintDevice 的物理尺寸信息。

# **QPainter**

此类提供了一些在 QPaintDevice 上绘制的方法，速度非常快。

## 一种可能的实例化

```cpp
QPainter p( this );
```

## 使用示例

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

# **QPen 和 QBrush**

QPen 定义了 QPainter 的轮廓绘制样式和颜色。QBrush 定义了 QPainter 的填充样式和颜色。

# **QPicture**

QPicture 是一个类，它捕获离屏绘制设备中的 QPainter 命令，并对这些命令进行序列化，以实现平台无关的重放。Windows 程序员会认出这些是元文件。序列化数据可以保存和恢复。

## 一种可能的实例化

```cpp
QPicture *pic = new QPicture();
```

## 使用示例

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

# QPixmap

QPixmap 是一个离屏绘制设备。大多数接受图像或图标作为参数的 Qt 小部件方法都假设该参数是一个 QPixmap。

## 一种可能的实例化

```cpp
QPixmap pix = QPixmap( "forest.bmp" );
```

## 使用示例

```cpp
QPixmap pix = QPixmap( "forest.bmp" );
QLabel *l = new QLabel( this );
l->setPixmap( pix );
```

由于我花费大量时间在 Windows 2000 上编码，我通常使用 Windows 绘图程序创建图标，并以 Windows 位图格式 (.bmp) 保存它们。虽然该格式对于嵌入式图形并不直接有用，但你可以利用提供的 load() 和 save() 方法将图像转换为 XPM 格式。然后，你可以将 XPM 图像嵌入到你的代码中，如下所示：

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

# QPNGImagePacker

此类对于创建压缩的 PNG 动画图像非常有用。

## 一种可能的实例化

```cpp
QFile f( "anim.png" );
f.open( IO_WriteOnly );
QPNGImagePacker p( f, 8, 0 );
```

