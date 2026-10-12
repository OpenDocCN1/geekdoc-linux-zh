

PHP 网站上关于 PDFLib 封装的文档尤其缺乏。虽然本文章应能充当出色的入门介绍，但关于 PDFLib 库完整功能的最佳信息来源还是 PDFLib 手册。

# GD 库

如果你曾经需要搭建包含大量图片的网站，例如图片库或电子商务网站，其中最繁琐的任务之一就是对所有单独图片的操作和上传。幸运的是，PHP 配备了 GD 库，这是一个与 PHP5 捆绑提供的开源图像处理库。凭借 GD 提供的强大功能，你可以自动化网站的大部分或全部图像处理任务，这样你只需上传图片，就可以将时间花在其他事情上，而不必花数小时手动处理图像。

# 创建图像基础

GD 库的一个缺点是可用函数数量庞大，其中许多执行相同的功能，区别仅在于输入类型或输出图像格式。为了提供一些清晰度以及本章节涵盖的所有图像处理功能的基础，你将要创建一个类，用于处理最流行的几种图像文件类型——JPG、GIF 和 PNG 的基本加载和保存。

这个基础类将提供基本的加载、保存和显示功能，并作为一个调用后续将在本章节中添加的其他附加图像处理类的位置。首先，创建一个名为 class.WebImage.php 的新文件，并输入以下代码：

```php
<?php
class WebImage
{
    public $gdresource;
    public $type;

    // Release resources
    public function __destruct()
    {
        if ($this->gdresource)
        {
            imagedestroy($this->gdresource);
        }
    }

    // Load an image from a file
    public function load($file)
    {
        // Get image mimetype
        $size = getimagesize($file);
        $this->type = $size['mime'];

        // Load image based on type
        switch ($this->type)
        {
            case 'image/jpeg': $this->gdresource = imagecreatefromjpeg($file); break;
            case 'image/png': $this->gdresource = imagecreatefrompng($file); break;
            case 'image/gif': $this->gdresource = imagecreatefromgif($file); break;
        }

        // Retain the alpha information
        imagesavealpha($this->gdresource, true);
    }

    // Save the file to the local filesystem
    public function save($file)
    {
        switch ($this->type)
        {
            case 'image/jpeg': imagejpeg($this->gdresource, $file); break;
            case 'image/png': imagepng($this->gdresource, $file); break;
            case 'image/gif':
                // Convert back to palette
                if (imagistruecolor($this->gdresource))
                {
                    imagetruecolor topalette($this->gdresource, false, 256);
                }
                imagegif($this->gdresource, $file);
                break;
        }
    }

    // Display the image in the browser
    public function display()
    {
        switch ($this->type)
        {
            case 'image/jpeg': header("Content-type: image/jpeg"); imagejpeg($this->gdresource); break;
            case 'image/png': header("Content-type: image/png"); imagepng($this->gdresource); break;
            case 'image/gif':
                // Convert back to palette
                if (imagistruecolor($this->gdresource))
                {
                    imagetruecolormapalette($this->gdresource, false, 256);
                }
                header("Content-type: image/gif");
                imagegif($this->gdresource);
                break;
        }
    }
}
?>
```

这一切意味着什么？这个文件是一个简单的图像封装，你可以使用它来打开、保存和显示图像。这段代码可以处理 JPG、GIF 和 PNG 图像，但如果 GD 库支持，你也可以轻松添加更多格式。为了更好地理解正在发生的事情，请查看该类的构建方式。

前几行相对简单——你开始声明两个公开属性，一个用于保存内部 GD 图像资源，另一个用于跟踪图像操作使用的 MIME 类型。还要注意析构函数——当类被销毁时，它会确保清理 GD 为此图像消耗的任何资源。

```php
<?php
class WebImage
{
    public $gdresource;
    public $type;

    // Release resources
    public function __destruct()
    {
        if ($this->gdresource)
        {
            imagedestroy($this->gdresource);
        }
    }
```

下一段代码从服务器上的文件加载图像数据。你向该方法传入文件名，它确定图像类型，然后使用 GD 库提供的相应函数将图像加载到 GD 资源中：

```php
// Load an image from a file
public function load($file)
{
    // Get image mimetype
    $size = getimagesize($file);
    $this->type = $size['mime'];

    // Load image based on type
    switch ($this->type)
    {
        case 'image/jpeg':
            $this->gdresource = imagecreatefromjpeg($file);
            break;
        case 'image/png' :
            $this->gdresource = imagecreatefrompng($file);
            break;
        case 'image/gif' :
            $this->gdresource = imagecreatefromgif($file);
            break;
    }
```

在处理包含透明区域的图像格式（如 GIF 或 PNG）时，理解涉及的两种不同类型的透明性至关重要。第一种，也是最简单的，是索引透明性。它存在于 8 位透明 PNG 图像和所有透明 GIF 图像中，索引透明性只是将索引调色板中的一种颜色定义为透明。被分配该颜色的任何像素在屏幕上都会显示为透明。

第二种透明性是 Alpha 透明性，存在于 32 位 PNG 图像中。Alpha 透明图像通过为每个像素提供额外的值范围来实现透明性，该范围定义了特定像素的透明度。Alpha 透明性允许图像平滑地淡出至透明，或使任何颜色在特定位置部分透明——这是索引透明图像无法做到的。

在 GD 中处理包含 Alpha 透明性的图像时，你需要告知 GD 你希望保留从加载图像中获得的任何 Alpha 透明性信息：

```php
// Retain the alpha information
imagesavealpha($this->gdresource, true);
}
```

如果你计划加载或输出任何理解逐像素/Alpha 透明性的图像格式（如 32 位 PNG），你就需要这样做。如果不告诉 GD 保存 Alpha 通道，你最终可能会遇到意外背景或透明性问题。

最后两个方法 `save()` 和 `display()` 各自将内部图像资源发送到最终目的地——要么是服务器上的文件，要么是在浏览器中显示。两者之间唯一的实质性区别在于 `display()` 中使用 `header()` 函数告知浏览器预期的图像类型，以及 `save()` 中 `image___()` 函数的第二个参数，该参数告诉 GD 将图像保存到文件，而不是将输出传输到屏幕：

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
            if (imagistruecolor($this->gdresource))
            {
                imagetruecolorpalette($this->gdresource, false, 256);
            }
            imagegif($this->gdresource, $file);
            break;
    }
}
```

如果你想为 save() 方法添加额外的图像类型，只需将其作为 switch 语句中的一个 case 添加即可。对于调色板图像类型，请务必在需要时将图像从真彩色转换为调色板，例如示例中 GIF 图像的情况。

# 调整图像大小

现在，既然你可以轻松地加载和保存一些基本图像格式，是时候以某种方式实际修改它们了。你要做的第一件事是让你的 WebImage 类具备调整图像大小的功能。为此，你将创建一个处理缩放操作的类文件，并在 WebImage 类中添加一个方法，以便在需要时调用缩放函数。

首先，创建名为 class.ImageResize.php 的以下文件：

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
            if (($this->max_width/$old_width <= $this->max_height/$old_height)
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
```

