
- `SWFMovie` 对象是其他对象正常运作所必需的唯一对象，因为它是实际将 Flash 文件写出到文件或浏览器的对象。
- `SWFShape` 对象生成形状。形状实际上是通过传递由一支想象中的笔绘制的坐标来绘制的。通过正确的坐标，几乎可以生成任何形状。此外，如前所述，这与 `SWFBitmap` 对象一起用于向电影添加图像文件。
- `SWFSprite` 对象通过向对象添加帧来生成“电影剪辑”或动画。帧包含其他对象之一，如 `SWFShape`。单个帧中可以包含多个 `SWFSprite` 对象，因此可以看到两个动画同时进行。与仅使用 `SWFMovie` 对象相比，向 `SWFSprite` 对象添加图像的优势在于它更好地封装对象以便操作。
- `SWFText` 对象在 Flash 动画中显示文本。如果你只需要显示少量静态信息，使用 `SWFText` 对象的替代方法是使用图像而不是使用 Flash 来写文本。
- `SWFTextField` 类似于 `SWFText` 对象，但有一些不同。`SWFTextField` 对象不能被旋转或倾斜，但可以用作表单输入。

## 创建 Flash 显示

再加几行代码，你可以将前面的示例扩展为稍微更有趣的外观：

```php
<?php
header('Content-type: application/x-shockwave-flash');
$movie = new SWFMovie();
$movie->setDimension(100,100); //width and length in that order
$movie->setBackground(0,0,255); // red, green, and blue integers

$shape = new SWFShape(); //generate a shape object
$shape->setLine(4, 30, 60, 100); //set the line width to 4 along
// with red, green, and blue integer values
$shape->setLeftFill($movie->addFill(300, 200, 100));
//set the color of the shape with red, green
// and integer values
$shape->movePenTo(20, 20);
```

## 第 10 章

//将虚拟的画笔移动到一个新位置

```php
$->drawLineTo(20, 80);
//绘制线条到一组新的点
$->drawLineTo(80, 80);
$->drawLineTo(80,20);
$->drawLineTo(20,20);
$->add($);  //将该形状添加到电影文件中
$->nextFrame();  //推进电影中的一帧
$->output();  //向浏览器输出所有内容
?>
```

该电影生成的输出内容本身并没有什么特别之处，但它演示了一些重要对象的一些基本方法。输出结果应该是一个蓝色背景，中间有一个绿色方块。

为了更深入地说明 Ming 的功能，你将使用它来生成一个幻灯片。为了使事情变得简单，你将使用所有大小和形状相同的图像，并且所有图像都有明确的名称。创建一个新文件并包含以下代码行：

```php
<?php
//创建一个电影对象
$movie = new SWFMovie();
//将背景设置为白色
$movie->setBackground(255, 255, 255);
```

在初始设置完成后，你需要添加对幻灯片中要包含的图像的引用。这里使用了一个简单的图像名称数组，但这可以扩展为直接从目录甚至数据库读取。另外，在此示例中，假设所有图像的大小都是 200 × 200 像素。为了更轻松地确定电影大小并扩展代码，创建了一个图像实例来读取其宽度和高度，尽管示例中的所有图像都应该是 200 × 200 像素。试试看：

```php
//要显示的图像
$images = array("1.jpg", "2.jpg", "3.jpg");
$bitmapImage = new SWFBitmap(SWFBinaryLoader::load("$images[1]","rb"));
$w = $bitmapImage->getWidth();
$h = $bitmapImage->getHeight();
```

创建一个 `SWFSprite`，它将作为幻灯片中的迷你电影，实际上也将由用户控制。为了防止它仅显示所有图像，为其添加了一个默认的 `stop()` 操作。此外，电影的大小是根据图像大小计算的，并额外留出空间以便在图像下方添加按钮。以下是代码：

```php
//创建一个将充当迷你电影的精灵
$Sprite = new SWFSprite();
//在第一帧添加停止操作
$Sprite->add(new SWFAction("stop();"));
//设置电影大小，为按钮预留额外空间
$movie->setDimension((1*$w),(1.5* $h)+3);
```

### PHP 扩展

现在需要将这些图像中的每一个都添加到精灵中，这可以通过遍历数组轻松实现。每个图像首先被转换为 `SWFBitmap` 对象，然后作为填充添加到 `SWFShape` 对象中。在形状周围画一条线后，将其添加到 `SWFSprite` 对象中，并且 `SWFSprite` 对象转到下一帧：

```php
//遍历所有图像
for($i=0; $i<count($images);$i++){
//从图像创建位图
$bitmapImage = new SWFBitmap(open($images[$i],"rb"));
//创建一个形状对象来容纳图像
$shape = new SWFShape();
//生成图像形状的填充
$fill = $shape->addFill($bitmapImage);
//将填充添加到形状
$shape->setRightFill($fill);
//在形状周围画线以设定大小
$shape->drawLine($w, 0);
$shape->drawLine(0, $h);
$shape->drawLine(-$w, 0);
$shape->drawLine(0, -$h);
//将形状添加到精灵以使其显示
$sprite->add($shape);
//生成新帧并转到该帧
$sprite->nextFrame();
}
```

由于精灵不会自动返回第一帧，因此需要在最后一帧添加一个操作，使其跳转到第一帧。`gotoFrame()` 操作接受一个帧号作为参数；这里使用的是 0，因为它是精灵中的第一帧。然后向精灵添加另一帧，以确保所有内容都包含在 `SWFSprite` 对象中：

```php
//跳转到第 0 帧
$sprite->add(new SWFAction("gotoFrame(0);"));
//再次生成新帧
$sprite->nextFrame();
```

现在精灵已完成，需要将其添加到 `SWFMovie` 对象中。当它被添加到电影时，它会返回一个句柄，该句柄可用于引用精灵，以便对其加以控制。为其分配一个名称，并使用句柄将精灵移动到指定位置：

```php
//添加精灵并获取其句柄
$handler = $aMovie->add($sprite);
//现在我们可以使用句柄为精灵命名
$handler->setname("images");
//我们也可以用句柄移动精灵
$handler->moveTo(0,2);
```

为了创建一个控制幻灯片的按钮，你需要创建一个新的 `SWFShape` 对象并为其添加按钮图像

```php
//再次创建一个形状
$shape = new SWFShape();
//这次创建另一个位图用于按钮图像
$bitmapImage = new SWFBitmap(open("button.jpg", "rb"));
$file = $shape->addFill($bitmapImage);
$shape->setRightFill($file);
//创建形状周围的边框
$shape->drawLine($w, 0);
$shape->drawLine(0, $h);
$shape->drawLine(-$w, 0);
$shape->drawLine(0, -$h);
```

实例化一个 `SWFButton` 对象，并将按钮形状添加到 `SWFButton` 对象中。还设置了按钮的默认标志，这允许程序根据按钮是否被按下以及鼠标是否在按钮上方来执行操作。还为按钮添加了一个操作，用于将精灵移动到下一帧。

```php
//现在实际创建一个按钮对象
$button = new SWFButton();
//将形状及其所有默认标志添加到按钮中，这些
//标志实际上都是预定义的整数值
$button->addShape($shape, SWFBUTTON_HIT |
    SWFBUTTON_UP | SWFBUTTON_DOWN |
    SWFBUTTON_OVER);
//添加一个操作以转到
//精灵的下一帧。精灵通过 "images" 引用
$button->addAction(new SWFAction("setTarget('images');
```
