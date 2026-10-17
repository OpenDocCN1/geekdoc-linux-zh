
这个简洁的应用程序使用从 MySQL 数据库中提取的数据生成一个简单的 PDF 简历。除了 MySQL 连接设置和数据库查询外，这个脚本中尚未涵盖的唯一方面是使用传记数据将个人期望职位的信息拼接到文档的关键词中：

```php
$keywords = split(" ", $row["DesiredPosition"]); 
$morewords = "";
foreach($keywords as $keyword) {
  $morewords = $morewords . $keyword . ", ";
}
pdf_set_info($pdf, "Keywords", "Resume, " . $morewords . "Apache, MySQL, PHP, PDF");
```

简历的头部信息，包含个人的姓名和联系信息，被单独处理，与简历其余数据分开，以便尽可能简化辅助函数 `pdflib_show()` 的实现。简历的主体由一个 `while` 循环生成，该循环跟踪当前和之前的分类，当值改变时打印分类名称；否则，打印描述。剩下的工作就是关闭文档，将其返回给浏览器，并进行清理。

最后一点建议：如果 PDF 生成在你的任何项目中都扮演着重要角色，你必须阅读并理解随 PDFLib 源代码分发的文档。通常丰富的

## GD 库

关于 PHP 网站上 PDFLib 封装器的文档特别匮乏。虽然本文可以作为一篇极佳的入门介绍，但若要全面了解 PDFLib 库的功能，没有比 PDFLib 手册更好的信息来源了。

如果你曾经需要建立一个包含大量图片的网站，例如图片画廊或电商网站，那么最繁琐的任务之一就是处理并上传所有单张图片。幸运的是，PHP 配备了 GD 库，这是一个随 PHP5 捆绑提供的开源图像处理库。凭借 GD 提供的丰富功能，你可以自动执行网站图像处理任务中的许多甚至全部步骤，这样你只需上传图片，将时间花在其它工作上，而不必整日忙着搬运图片。

### 创建图像基础

GD 库的一个缺点在于其可用的函数数量庞大，其中许多功能相同，仅在输入类型或输出图像格式上有所不同。为了提供清晰度以及本章涵盖的所有图像处理功能的基础，你将创建一个类，该类处理几种最流行图像文件类型 —— JPG、GIF 和 PNG —— 的基本加载和保存。

这个基础类将提供基本的加载、保存和显示功能，并将作为后续章节中你将添加的其他附加图像处理类调用的中心位置。首先，创建一个名为 `class.WebImage.php` 的新文件，并输入以下代码：

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
        // Get image mime type
        $size = getimagesize($file);
        $this->type = $size['mime'];

        // Load image based on type
        switch ($this->type)
        {
            case 'image/jpeg':
                $this->gdresource = imagecreatefromjpeg($file);
                break;
            case 'image/png':
                $this->gdresource = imagecreatefrompng($file);
                break;
            case 'image/gif':
                $this->gdresource = imagecreatefromgif($file);
                break;
        }

        // Retain the alpha information
        imagesavealpha($this->gdresource, true);
    }

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
                if (imageistruecolor($this->gdresource))
                {
                    imagergtopalette($this->gdresource, false, 256);
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
            case 'image/jpeg':
                header('Content-type: image/jpeg');
                imagejpeg($this->gdresource);
                break;
            case 'image/png':
                header('Content-type: image/png');
                imagepng($this->gdresource);
                break;
            case 'image/gif':
                // Convert back to palette
                if (imageistruecolor($this->gdresource))
                {
                    imagergtopalette($this->gdresource, false, 256);
                }
                header('Content-type: image/gif');
                imagegif($this->gdresource);
                break;
        }
    }
}
?>
```

这一切意味着什么？这个文件是一个朴素的图像封装器，你可以用它来打开、保存和显示图像。这段代码可以处理 JPG、GIF 和 PNG 图像，但假设 GD 库支持的话，你完全可以轻松添加更多类型。为了更好地理解正在发生的事情，请查看该类是如何构建的。

开头几行相对简单明了——你通过声明两个公共属性开始，一个用于保存内部 GD 图像资源，另一个用于跟踪图像操作要使用的 MIME 类型。同时注意析构函数——当类被销毁时，它会确保清理 GD 为该图像消耗的任何资源。

下一部分代码从服务器上的文件加载图像数据。你向该方法传递文件名，它会确定图像类型，然后使用 GD 库提供的相应函数将图像加载到 GD 资源中：
