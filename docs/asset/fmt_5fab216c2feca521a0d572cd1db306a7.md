
接下来是简单图像功能系列中的下一项：为图像添加标题——图像底部的一个变暗区域，上面叠加了标题或简短的文字说明。这是一种微妙的方式，用于包含和显示有关图像或其上下文的一点信息，而无需将文本与图像分开，也不至于碍事。

首先，遵循 `ImageResize` 和 `ImageRotate` 的示例，创建一个名为 `class.ImageCaption.php` 的文件：

```php
<?php

class ImageCaption
{
    public $caption = '';
    public $fontfile = '';
    public $fontsize = 10;
    public $padding = 5;
    public $drawline = true;

    // 为图像添加标题
    public function process($gd_img)
    {
        if ($this->caption and $this->fontfile)
        {
            // 获取文本框高度
            $text_box = imageftbbox($this->fontsize, 0,
                $this->fontfile,
                $this->caption);
            $text_height = $text_box[3] - $text_box[5];
            $text_baseline = $text_box[3];

            // 获取某些图像尺寸
            $img_x = imagesx($gd_img);
            $img_y = imagesy($gd_img);

            // 绘制背景阴影
            imagealphablending($gd_img, true);
```
# 第 10 章

```php
$rect_color = imagecolorallocatealpha($gd_img, 0, 0, 0, 75);
imagefilledrectangle($gd_img,
0,
$img_y + $text_height - ($this->padding * 2),
$img_x,
$img_y,
$rect_color);

// Draw caption text
$text_color = imagecolorallocate($gd_img, 255, 255, 255);
imagettftext($gd_img,
$this->fontsize,
0,
$this->padding,
$img_y + $text_underbaseline - $this->padding,
$text_color,
$this->fontfile,
$this->caption);

// Draw shading border if requested
if ($this->drawline)
{
$line_color = imagecolorallocatealpha($gd_img,
200,
200,
200,
75);

imageline($gd_img,
0,
$img_y + $text_height - ($this->padding * 2) - 1,
$img_x,
$img_y + $text_height - ($this->padding * 2) - 1,
$line_color);
}

return $gd_img;
}
?>
```

然后，像之前一样，在 `WebImage` 类定义的末尾添加一个新方法，如下所示：

```php
// Add a caption to the image
public function caption($text,
$font,
$size = null,
$padding = null,
$drawline = null)
{
require_once 'class.ImageCaption.php';

$ic = new ImageCaption();
// Set size, padding, line if needed
if ($size)
{
    $ic->fontsize = $size;
}
if ($padding != null)
{
    $ic->padding = $padding;
}
if ($drawline != null)
{
    $ic->drawline = $drawline;
}
// Set font, caption
$ic->fontfile = $font;
$ic->caption = $text;
// Perform the captioning
$this->gdresource = $ic->process($this->gdresource);
}
```

当你调用 `WebImage` 的 `caption()` 方法时，最多可以使用五个参数。前两个参数是必需的，分别指定要显示在标题中的文本以及用于标题文本的 TrueType 字体（.ttf）文件名。其他参数用于设置字体大小、文本周围的像素填充量，以及是否绘制一条标题上方的细线。该方法包含所需的类定义文件，整理参数值，然后调用 `ImageCaption` 的 `process()` 方法。

`process()` 方法的作用确定要写入的文本以及目标图像本身的尺寸。为了获取渲染后的文本尺寸，使用了 `imagettfbbox()`。`imagettfbbox()` 接受四个参数：字体大小、字体角度、用于渲染文本的 TrueType 字体文件，以及文本本身。确定文本边界框信息后，将实际高度设置为 `$text_height`，并确定文本基线以下的深度——对于像小写 g 和 p 这样的字母。代码如下：
