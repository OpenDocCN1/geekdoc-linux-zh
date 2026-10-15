
```php
// Copy the logo onto the main image

imagecopy($gd_img,
    $logo->gdresource,
    $logo_x,
    $logo_y,
    0,
    0,
    imagesx($logo->gdresource),
    imagegy($logo->gdresource));
}

return $gd_img;
}
```

请注意，这里使用的是 `imagecopy()` 而不是 `imagecopymerge()`。`imagecopymerge()` 函数似乎更适合此任务，它甚至提供了合并标志并设置透明度的功能——这对于某些水印效果非常有用。不幸的是，`imagecopymerge()` 有一个讨厌的习惯，会破坏源标志图像本身的大部分透明信息，因此如果你想为图像制作一个淡淡的半透明水印，最好直接在标志图像本身添加透明度，并使用 `imagecopy()`，而不是使用不透明图像和 `imagecopymerge()`。

## 测试运行

为了全面测试这一系列图像处理代码，你需要几样东西：一个要处理的主图像、一个用作标志叠加的图像，以及一个 TrueType 字体文件。准备好这三样东西后，创建一个 PHP 脚本，使用你创建的类来操作这些图像。首先只需加载你的图像，并在浏览器中显示它：

```php
<?php
require_once 'class.WebImage.php';
$img = new WebImage();
$img->load('base.png');
$img->display();
?>
```

在浏览器中加载此文件，它应该显示你的图像，如图 10.1 所示。

![](img/ab27c6ac898db1f934d39fa127b14657_283_0.png)

**图 10.1**

如果你想在保存或显示之前更改图像的类型，只需在 `WebImage` 对象中设置图像类型即可：

```php
<?php
require_once 'class.WebImage.php';
$img = new WebImage();
$img->load('base.png');
$img->type = 'image/gif';
$img->display();
?>
```

要调整图像大小，请调用 `WebImage` 的 `resize()` 函数。以下代码使用了 0.75 的比例：

```php
<?php
require_once 'class.WebImage.php';
$img = new WebImage();
$img->load('base.png');
$img->resize(0.75);
$img->display();
?>
```

输出的一个示例如图 10.2 所示。

![](img/ab27c6ac898db1f934d39fa127b14657_284_0.png)

接下来，旋转你的图像。以下代码使用 180 度进行旋转：

```php
<?php
require_once 'class.WebImage.php';
$img = new WebImage();
$img->load('base.png');
$img->rotate(180);
$img->display();
?>
```

在浏览器中加载脚本，其外观如图 10.3 所示。

![](img/ab27c6ac898db1f934d39fa127b14657_285_0.png)

**图 10.3**

现在，为图像添加标题。此示例使用字体“Fuji Wide Normal”，但你可以使用任何你手头可用的字体，只要它是 TrueType 字体文件 `.ttf`：

```php
<?php
require_once 'class.WebImage.php';
$img = new WebImage();
$img->load('base.png');
$img->caption('An example of plantlife found on Maui.',
    'FUJIWIDR.TTF',
    15,
    5,
    true);
$img->display();
?>
```

如果一切按计划进行，你应该会看到类似图 10.4 的效果。

![](img/ab27c6ac898db1f934d39fa127b14657_286_0.png)

**图 10.4**

# 第 10 章

最后，尝试应用图像标志。在此示例中，你将在图像的右下角放置一个标志，位于标题框之上：

```php
<?php
require_once 'class.WebImage.php';
$img = new WebImage();
$img->load('base.png');
$img->caption('An example of plantlife found on Maui.',
	'FUJIWIDR.TTF',
	13,
	5,
	true);
$img->logo('logo.png', 'e', 'b', 5, 0.3);
$img->display();
?>
```

现在，应该会显示一个标志，略微缩放，位于右下角，带有 5px 的填充量，如图 10.5 所示。

![](img/ab27c6ac898db1f934d39fa127b14657_287_0.png)

**图 10.5**

由此可见，使用 GD 库并不难，它允许你对图像拥有相当多的灵活性和控制权。还有许多其他更高级的功能可以使用，所有这些都可以在 PHP 手册的 GD 部分找到（http://www.php.net/gd）。

## Ming

`Ming` 是一个第三方 PHP 扩展，允许用户在不实际使用 Macromedia Flash 工作室的情况下创建 Shockwave Flash 文件。`Ming` 提供的功能并不总是与 Macromedia Flash 中可用的功能相同，这是因为使用 PHP 和 `Ming` 创建 Flash 文件的方式特性所致。`Ming` 确实提供了一种低成本创建 Flash 文件的方法，并允许在需要时动态创建内容。

### 关于 Ming

动态创建的 Flash 文件的实用性有时可能会被人忽视，特别是因为你无法像使用 Macromedia Flash Studio 的人那样对内容布局进行精确的视觉控制。此外，`Ming` 的功能集仅限于 Flash 4 版本，这比最新可用版本落后了好几个版本。但是，能够编写脚本来创建应用并为其添加动态内容，这是使用 Macromedia Flash Studio 无法做到的。这在需要 Flash 功能但又希望为用户个性化内容的分发场景中非常有用。

`Ming` 本身实际上是一个第三方扩展，已经为它编写了 PHP 包装扩展，因此在构建二进制文件时需要将其编译到 PHP 二进制文件中。关于如何在 PHP 中安装 `Ming` 的说明可以在 PHP 网站上找到（http://www.php.net/ming）。有关 `Ming` 本身的更多信息可以在 SourceForge.Net 上的 `Ming` 站点找到（http://ming.sourceforge.net）。互联网上还有许多教程和示例，可以帮助说明 `Ming` 的功能，并提供适合用作构建 Flash 影片基础的代码片段。

`Ming` 在 PHP 中实现为对象，因此在 PHP 中任何时候使用 `Ming` 创建 shockwave 文件时，至少需要实例化一个 `SWFmovie` 对象。以下是使用 `Ming` 和 PHP 生成的一个非常简单的文件的代码。要运行此代码，请将其插入到一个没有其他内容的 PHP 文件中，然后在安装了 Flash 插件的 web 浏览器中查看该文件：

```php
<?php
header('Content-type: application/x-shockwave-flash');
$a=new SWFmovie();
$a->setDimension(100,100); //width and length in that order
$a->setBackground(0,0,255); // red, green, and blue integers
$a->output();
?>
```
