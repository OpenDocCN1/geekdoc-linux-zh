
现在，需要将每个图像都添加到精灵中，这可以通过遍历数组轻松实现。首先，每个图像都被转换为 SWFBitmap 对象，然后作为填充色添加到 SWFShape 对象中。在图形周围画好一条线后，将其添加到 SWFSprite 对象中，然后 SWFSprite 对象进入下一帧：

```php
//loop through all of the images
for($i=0; $i<count($images);$i++){

//create a bitmap from an image
$bitmapImage = new SWFBitmap(open($images[$i], "rb"));

//create a shape object to hold the image
$shape = new SWFShape();
//generate the fill for the shape of the image
$fill = $shape->addFill($bitmapImage);
//add the fill to the shape
$shape->setRightFill($fill);

//draw a line around the shape to set the size
$shape->drawLine($w, 0);
$shape->drawLine(0, $h);
$shape->drawLine(-$w, 0);
$shape->drawLine(0, -$h);
//add the shape to the sprite so that it is displayed
$sprite->add($shape);
//generate a new frame and go to it
$sprite->nextFrame();
}
```

由于精灵不会自动返回到第一帧，因此需要在最后一帧添加一个动作，使其跳转到第一帧。`gotoFrame()` 动作接受一个帧号作为参数；这里使用 `frame 0`，因为它是精灵中的第一帧。随后，为了确保持完整内容都包含在 SWFSprite 对象中，还会向精灵添加另一帧：

```php
//goto frame 0
$sprite->add(new SWFAction('gotoFrame(0);'));
//again generate a new frame
$sprite->nextFrame();
```

现在精灵已创建完成，需要将其添加到 SWFMovie 对象中。当它被添加到电影时，会返回一个句柄，该句柄可作为对精灵的引用，以便对其进行控制。为其分配一个名称，并使用该句柄将精灵移动到指定位置：

```php
//add the sprite and get its handler
$handler = $movie->add($sprite);
//we can name the sprite now with the handler
$handler->setName("images");
//we can move the sprite also with the handler
$handler->moveTo(0,2);
```

## 第 10 章

为了创建一个用于控制幻灯片放映的按钮，你需要创建一个新的 SWFShape 对象，并为其添加一个按钮图像。

```php
//create a shape again
$shape = new SWFShape();
//create another bitmap this time for a button image
$btmMapImage = new SWFBitmap(open("button.jpg", "rb"));
$fill = $shape->addFill($btmMapImage);
$shape->setRightFill($fill);
//create the border around the shape
$shape->drawLine(0, 0);
$shape->drawLine(0, $h);
$shape->drawLine(-$w, 0);
$shape->drawLine(0, -$h);
```

实例化一个 SWFButton 对象，并将按钮形状添加到该 SWFButton 对象中。同时，也为按钮设置了默认标志，这允许程序根据按钮是否被按下以及鼠标是否悬停在按钮上来执行操作。此外，还为按钮添加了一个动作，用于将精灵移动到下一帧。

```php
//now actually create a button object
$button = new SWFButton();
//add the shape to the button with all of its default flags which are
//all actually predefined integer values
$button->addShape($shape, SWFBUTTON_HIT |
SWFBUTTON_UP | SWFBUTTON_DOWN |
SWFBUTTON_OVER);
//add an action to go to the next frame
//on the sprite. The sprite is referenced by "/images"
$button->addAction(new SWFACTION("setTarget('/images')
;nextFrame();"), SWFBUTTON_MOUSEDOWN);
```

随后，该按钮被添加到电影中，并返回其句柄。接着，将按钮移动到图像下方，并向电影添加一个新帧。然后生成必要的浏览器头信息，并输出电影：

```php
//add the button to the movie and save the returned handler
$handler = $aMovie->add($button);
//use the handler to move the button below the images
$handler->moveTo(0, $h+3);
$aMovie->nextFrame();
//send the appropriate header to the browser
header('Content-Type:application/x-shockwave-flash');
//output the movie to the browser
?>
$aMovie->output();
?>
```

在使用 Ming 时，有几点需要记住。首先，当你直接输出到浏览器时，必须在调用 SWFMovie 对象的 output() 方法之前发送 Content-Type 头。这会发送正确的 HTTP 头，以便浏览器知道加载 Shockwave Flash 插件。这会导致另一个可能出现的错误：输出 Content-Type 头以外的任何内容，例如空行。输出头部和电影文件本身以外的内容会导致文件损坏，从而使得浏览器无法正确显示该文件。此外，对最终输出样式有一个大致的布局规划也会有帮助。为了协助使用 Ming 创建的 Flash 电影的布局，你可以使用提供坐标系图形程序，或者仅仅使用方格纸。

### SimpleXML

如今 XML 无处不在，因此拥有一个简单的方法来检索和解析这些文件也就合情合理了。幸运的是，PHP 提供给我们了一个用于利用 XML 数据简单易用的扩展：SimpleXML。SimpleXML 默认已安装，但如果你不打算使用它，建议在 php.ini 中禁用它。需要指出的是，SimpleXML 还需要 PHP5。

顾名思义，该扩展的目的是在非常基本的层面上访问 XML 文档。为了说明实现此目的有多简单，创建一个虚构的 XML 文件，其中包含海滨租住的信息（此文件将在所有示例中使用）：

```xml
<?xml version="1.0"?>
<rentals>
    <description>
        <name>The Bayfront</name>
        <type>condo</type>
        <view>oceanfront</view>
        <space>1200 square feet</space>
        <location>Wrightsville Beach</location>
        <price>1000 per week</price>
        <bed_bath>3 bedrooms, 2 bathrooms</bed_bath>
    </description>
    <description>
        <name>Paradise</name>
        <type>house</type>
        <view>oceanfront</view>
        <space>1000 square feet</space>
        <location>Wrightsville Beach</location>
        <price>900 per week</price>
        <bed_bath>2 bedrooms, 2 bathrooms</bed_bath>
    </description>
</rentals>
```

既然已经有了 XML 文件，获取信息并将其放入对象中（使用 `simplexml_load_file()` 函数），以便对其进行操作：

```php
<?php
    if (file_exists('beachfront.xml')) {
        $data = simplexml_load_file('beachfront.xml');
        print_r($data);
    }
?>
```

你可以遍历该对象并美观地显示结果（或者至少是以更易读的格式显示）。在 `simple.php` 中添加以下更改：

```php
if (file_exists('beachfront.xml')) {
    $data = simplexml_load_file('beachfront.xml');

    foreach($data as $main) {
        echo "<hr>";
        foreach ($main as $k => $v) {
            echo $k . ":" . $v . "<br />";
        }
    }
}
```

除了 simplexml_load_file() 之外，还有很多其他函数与 SimpleXML 扩展配套使用。simplexml_load_string() 将 XML 文档作为字符串加载。你首先需要将其内容赋值给一个变量；然后可以使用 simplexml_load_string() 函数将变量的内容解析为对象以供使用。如果你想要操作对象，然后将内容以 XML 文件的形式输出回浏览器，你可以使用 $objectname->asXML() 函数。如果你需要查看元素的属性或对象任何节点的子节点，attributes() 和 children() 函数非常有用。如果你想从 DOM 文档中获取一个 DOM 节点并将其转换为 SimpleXMLElement 对象，simplexml_import_dom() 函数很有帮助。

xpath() 函数允许你通过 XML 文档搜索特定的字符串。它使用 W3C 的路径来评估 XML 文档中的每个节点，并被称为“XPath”，因为搜索关键字类似于文件的路径，因为每个元素都类似嵌套。如果你想进一步了解 XPath，请访问 W3C 关于此主题的资料 http://www.w3.org/TR/xpath。

如果你想执行最简单的查询，这是足够的，如下例所示：

```php
if (file_exists('beachfront.xml')) {
    $data = simplexml_load_file('beachfront.xml');

    //find and list all the 'locations' in our XML file
    //*locations* are under *descriptions* which are under *rentals*
    $find = $data->xpath('/rentals/description/location');

    while (list(, $v) = each($find)) {
        echo $v. "\n";
    }
}
```

此脚本将为你提供 XML 文件中名为“location”节点的所有值。如果你想进一步扩展查询，你必须使用另一种方法。记住这是 SimpleXML，而不是 ComplexXML。

SimpleXML 提供了一种非常快速且直接的方式来访问简单的 XML 文档。它允许的功能有限，且仅适用于最简单的 XML 文件。例如，你尝试在包含 HTML 代码内容的 XML 文件上运行这些函数时会遇到问题。否则，与其他可用的 XML/PHP 接口相比，处理起来要简单得多。

