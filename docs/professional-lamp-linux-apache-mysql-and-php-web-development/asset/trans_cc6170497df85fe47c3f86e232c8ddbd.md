

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

```php
// Caption the image
public function process($gd_img)
{
    if ($this->caption and $this->fontfile)
    {
        // Get text box height
        $text_box = imagettfbbox($this->fontsize, 0, $this->fontfile, $this->caption);
        $text_height = $text_box[3] - $text_box[5];
        $text_underbaseline = $text_box[3];
        
        // Get some image dimensions
        $img_x = imagesx($gd_img);
        $img_y = imagesy($gd_img);

        // Draw background shading
        imagealphablending($gd_img, true);
        $rect_color = imagecolorallocatealpha($gd_img, 0, 0, 0, 75);
        imagefilledrectangle($gd_img,
                            0,
                            $img_y - $text_height - ($this->padding * 2),
                            $img_x,
                            $img_y,
                            $rect_color);

        // Draw caption text
        $text_color = imagecolorallocate($gd_img, 255, 255, 255);
        imagettftext($gd_img,
                     $this->fontsize,
                     0,
                     $this->padding,
                     $img_y - $text_underbaseline - $this->padding,
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
                      $img_y - $text_height - ($this->padding * 2) - 1,
                      $img_x,
                      $img_y - $text_height - ($this->padding * 2) - 1,
                      $line_color);
        }
    }
    return $gd_img;
}
?>
```

接下来，在图像上绘制一个带背景阴影的矩形框，提供一个较暗的区域，以便稍后在该方法中将白色文本叠加显示在上面。首先，通知 GD 在目标图像上正确混合透明度。然后，使用 `imagecolorallocatealpha()` 获取一个颜色资源——在这种情况下是黑色 (0,0,0)，透明度约为 60%（alpha 通道的范围是 0–127）。最后，使用半透明黑色颜色，在图像底部绘制一个填充矩形，其高度需要覆盖完整的字体高度以及可能指定的任何填充：

在背景矩形绘制到图像上之后，是时候在顶部添加标题文本了。只需为文本分配一个颜色——在这种情况下是白色——然后使用 `imagettftext()` 在图像上绘制文本：

`imagettftext()` 函数使用八个参数：要添加文本的图像资源、字体大小、文本角度、开始绘制文本的 x 位置、文本基线/底部的 y 位置、文本颜色、.ttf 字体文件名，以及要渲染的实际文本，按此顺序排列。

标题功能的最后一部分使用半透明浅灰色和 `imageline()` GD 函数，在标题框的顶部绘制一条细边框：

## 添加 Logo

你要添加到 `WebImage` 类的最后一项功能是能够在图像上放置 logo 或水印。

首先创建 `class.ImageLogo.php` 文件：

```php
<?php

class ImageLogo
{
    public $logfile;
    public $ratio = 1;
    public $location = array('x' => '', 'y' => '');
    public $padding = 0;

    public function process($gd_img)
    {
        if ($this->logfile)
        {
            require_once 'class.WebImage.php';

            // Load the logo
            $logo = new WebImage();
            $logo->load($this->logfile);

            // Resize logo if needed
            if ($this->ratio and $this->ratio != 1)
            {
                $logo->resize($this->ratio);
            }

            // Determine logo placement (x)
            switch ($this->location['x'])
            {
            case 'l':
                $logo_x = $this->padding;
                break;
            case 'r':
                $logo_x = imagexs($gd_img) -
                          $this->padding -
                          imagexs($logo->gdresource);
                break;
            default:
                $logo_x = round((imagexs($gd_img) / 2) -
                                 (imagexs($logo->gdresource) / 2));
            }

            // Determine logo placement (y)
            switch ($this->location['y'])
            {
            case 't':
                $logo_y = $this->padding;
                break;
            case 'b':
                $logo_y = imagegy($gd_img) -
                          $this->padding -
                          imagegy($logo->gdresource);
                break;
            default:
                $logo_y = round((imagegy($gd_img) / 2) -
                                (imagegy($logo->gdresource) / 2));
            }

            // Copy the logo onto the main image
            imagecopy($gd_img,
                      $logo->gdresource,
                      $logo_x,
                      $logo_y,
                      0,
                      0,
                      imagex($logo->gdresource),
                      imagey($logo->gdresource));

            return $gd_img;
        }
    }
}
?>
```

接下来，将 `logo()` 方法添加到 `WebImage` 类定义的末尾：

```php
public function logo($logofile,
                    $loc_x = null,
                    $loc_y = null,
                    $padding = null,
                    $ratio = null)
{
    require_once 'class.ImageLogo.php';

    $il = new ImageLogo();

    // Set logo file
    $il->logfile = $logofile;

    // Set location, padding, and ratio if needed
    if ($loc_x !== null)
    {
        $il->location['x'] = $loc_x;
    }
    if ($loc_y !== null)
    {
        $il->location['y'] = $loc_y;
    }
    // ... (code continues)
}
```

