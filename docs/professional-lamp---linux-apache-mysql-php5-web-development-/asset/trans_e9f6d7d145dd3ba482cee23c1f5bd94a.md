

## 第 10 章

```php
$this->gdresource = imagecreatefromjpeg($file);
break;
case 'image/png':
$this->gdresource = imagecreatefrompng($file);
break;
case 'image/gif':
$this->gdresource = imagecreatefromgif($file);
break;
}
```

在处理可能包含透明区域（如 GIF 或 PNG）的图像格式时，理解所涉及的两种不同透明类型非常重要。第一种也是最简单的是索引透明。它存在于 8 位透明 PNG 图像和所有透明 GIF 图像中，索引透明仅将索引调色板中的一种颜色定义为透明。任何被分配该颜色的像素在屏幕上都会显示为透明。

第二种透明类型是 Alpha 透明，存在于 32 位 PNG 图像中。Alpha 透明图像通过为每个像素提供额外的数值范围来定义该特定像素的透明度，从而实现透明效果。Alpha 透明允许图像平滑地渐变为透明，或者在某些位置让任何颜色部分透明——这是索引透明图像无法做到的。

在 GD 中处理包含 Alpha 透明的图像时，你需要告知 GD 你希望保留从已加载图像中获取的任何 Alpha 透明信息：

```php
// Retain the alpha information
imagesavealpha($this->gdresource, true);
}
```

如果你计划加载或输出任何理解每像素/Alpha 透明的图像格式，例如 32 位 PNG，就需要这样做。如果不告诉 GD 保存 Alpha 通道，最终输出可能会遇到意外的背景或透明问题。

最后两个方法 `save()` 和 `display()` 将内部图像资源发送到最终目的地——无论是服务器上的文件，还是在浏览器中显示。两者之间唯一的实质区别在于 `display()` 中使用 `header()` 函数告知浏览器预期的图像类型，以及 `save()` 中 `image__()` 函数的第二个参数，该参数告诉 GD 将图像保存到文件，而不是将输出直接传输到屏幕：

```php
// Save the file to the local filesystem
public function save($file)
{
switch ($this->type)
{
case 'image/jpeg':
imagejpeg($this->gdresource, $file);
break;
case 'image/png':
imagepng($this->gdresource, $file);
break;
case 'image/gif':
// Convert back to palette
if (imagetruecolor($this->gdresource))
{
    imagegetcolorpalette($this->gdresource, false, 256);
    }
imagegif($this->gdresource, $file);
break;
}
}
```

如果你想在 `save()` 方法中添加更多图像类型，只需在 switch 语句中添加相应的 case 即可。对于调色板图像类型，如果必要，请确保将图像从真彩色转换为调色板，如示例中 GIF 图像的情况所示。

## 调整图像大小

现在你可以轻松加载和保存一些基本图像格式了，是时候实际以某种方式修改它们了。你要做的第一件事是让你的 WebImage 类具备调整图像大小的功能。为此，你将创建一个处理调整大小操作的类文件，并在你的 WebImage 类中添加一个方法，在需要时调用调整大小功能。

首先，创建以下名为 `class.ImageResize.php` 的文件：

```php
<?php

class ImageResize
{
    public $ratio = 1;
    public $max_width;
    public $max_height;

    // Resize the image
    public function process($gd_img)
    {
        // Set initial dimensions
        $old_width = imagesx($gd_img);
        $old_height = imagesy($gd_img);
        $new_width = 0;
        $new_height = 0;

        // New dimensions to fall within maximums provided
        if ($this->max_width and $this->max_height)
        {
            if (($this->max_width/$old_width) <= $this->max_height/$old_height)
            {
                $new_width = ceil(($this->max_width/$old_width) * $old_width);
                $new_height = ceil(($this->max_width/$old_width) * $old_height);
            }
            else
            {
                $new_width = ceil(($this->max_height/$old_height) * $old_width);
                $new_height = ceil(($this->max_height/$old_height) * $old_height);
            }
        }
        // New dimensions based on a ratio
        else if ($this->ratio)
        {
            $new_width = ceil($this->ratio * $old_width);
            $new_height = ceil($this->ratio * $old_height);
        }

        // Resize only if dimensions changed
        if ($new_width and $new_height)
        {
            // Create resize target
            $temp = imagecreatetruecolor($new_width, $new_height);

            // Set alpha parameters
            imagesavealpha($temp, true);
            imagealphablending($temp, false);

            // Resize the image
            imagecopyresampled($temp,
                               $gd_img,
                               0,
                               0,
                               0,
                               0,
                               $new_width,
                               $new_height,
                               $old_width,
                               $old_height);
            $gd_img = $temp;
        }

        return $gd_img;
    }
}
?>
```

然后，将以下方法添加到你的 WebImage 类定义的末尾：

```php
// Resize the image
public function resize()
{
    require_once 'class.ImageResize.php';

    $ir = new ImageResize();

    // Set resize parameters based on arguments
    switch (func_num_args())
    {
        case 1:
            $ir->ratio = func_get_arg(0);
            break;
        case 2:
            $ir->max_width = func_get_arg(0);
            $ir->max_height = func_get_arg(1);
            break;
    }

    // Perform the resize
    $this->gdresource = $ir->process($this->gdresource);
}
```

查看你刚刚添加到 **WebImage** 的新方法，你可以快速了解图像调整大小类是如何被调用的。首先，如果需要，引入 **ImageResize.php** 文件，并创建一个 **ImageResize** 对象。然后使用 `func_num_args()` 函数确定调用该方法时使用多少个参数。

**WebImage** 的 resize 方法可以使用一个或两个参数进行调用。如果使用一个参数，它被视为用于调整图像大小的数字比例。如果传递两个参数，它们将用作调整后的图像不得超过的最大宽度和最大高度的值。

在对象中相应地设置这些值后，调用 `process()` 方法，图像将被调整大小并返回。为了进一步理解调整大小具体是如何发生的，请仔细查看 **ImageResize** 类。

在 **ImageResize** 的核心部分，`process()` 方法中，你从相当简单的操作开始——分别使用 `imagesx()` 和 `imagesy()` 确定现有图像的宽度和高度，并将新宽度和新高度初始化为 0：

```php
// Resize the image
public function process($gd_img)
{
    // Set initial dimensions
    $old_width = imagesx($gd_img);
    $old_height = imagesy($gd_img);
    $new_width = 0;
    $new_height = 0;
```

接下来，确定调整后图像的最终尺寸。首先检查 `max_width` 和 `max_height` 的值，如果两者都存在，则计算图像尺寸以使其等于或小于这两个最大值。如果没有提供两个最大值，则检查调整大小比例值，如果存在，新图像尺寸将基于原始尺寸的设置比例：

```php
// New dimensions to fall within maximums provided
if ($this->max_width and $this->max_height)
{
    if ($this->max_width/$old_width <= $this->max_height/$old_height)
    {
        $new_width = ceil(($this->max_width/$old_width) * $old_width);
        $new_height = ceil(($this->max_width/$old_width) * $old_height);
    }
    else
    {
        $new_width = ceil(($this->max_height/$old_height) * $old_width);
        $new_height = ceil(($this->max_height/$old_height) * $old_height);
    }
}
// New dimensions based on a ratio
else if ($this->ratio)
{
    $new_width = ceil($this->ratio * $old_width);
    $new_height = ceil($this->ratio * $old_height);
}
```

方法的其余部分是实际执行调整大小的地方（如果需要）。在 GD 中调整大小时，你实际上并不是直接调整现有资源的大小，而是创建一个新的具有新尺寸的图像，并将原始图像复制到目标位置——GD 在内部处理调整大小。在这个方法中，你使用的是 `imagecopyresampled()` 函数；在使用 GD 调整图像大小时，可以使用 `imagecopyresized()` 函数或 `imagecopyresampled()` 函数。两者都能达到相同的目的，但后者在保持结果“平滑”方面做得稍好一些，而前者则会产生像素化的结果。请查看：

```php
// Resize only if dimensions changed
if ($new_width and $new_height)
{
    // Create resize target
    $temp = imagecreatetruecolor($new_width, $new_height);

    // Set alpha parameters
    imagesavealpha($temp, true);
    imagealphablending($temp, false);

    // Resize the image
    imagecopyresampled($temp,
                       $gd_img,
                       0,
                       0,
                       0,
                       0,
                       $new_width,
                       $new_height,
                       $old_width,
                       $old_height);

    $gd_img = $temp;
}

return $gd_img;
```

注意 Alpha 保存函数 `imagesavealpha()` 和 `imagealphablending()` 的使用。它们用于告知 GD 在执行调整大小时保留并使用源图像中的 Alpha 透明信息。如果忽略 Alpha 通道，透明 GIF 或 PNG 中可能存在的任何透明效果都可能会被破坏。

最后，在该方法的末尾，返回 GD 图像资源。

## 旋转图像

除了在服务器上调整图像大小外，常见的图像编辑需求还包括在上传后旋转图像的能力。为了实现此操作，你将像之前一样创建另一个图像操作类文件，并添加另一个方法将函数调用到 WebImage。

