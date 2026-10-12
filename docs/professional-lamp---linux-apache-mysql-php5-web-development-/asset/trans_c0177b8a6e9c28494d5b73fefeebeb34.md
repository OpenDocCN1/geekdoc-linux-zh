
## 第 10 章

```php
die("Error: Unable to open output file.");
}

// Collect header information from the database.
mysql_connect("localhost", "resume_user", "resume_pw");
mysql_select_db("resume");
$sql = "SELECT * FROM biography WHERE OID = 0";
$result = mysql_query($sql);
$row = mysql_fetch_array($result, MYSQL_ASSOC);
$name = $row["NameFirst"] . " " . $row["NameLast"];

// Document info.
pdf_set_info($pdf, "Author", "Name: < " . $row["Email"]. ">");
pdf_set_info($pdf, "Title", "Resume - " . $name);
pdf_set_info($pdf, "Subject", "The resume of " . $name . ", " .
$row["DesiredPosition"] . ".");

// Do something clever with the keywords.
$keywords = split(" ", $row["DesiredPosition"]);
$morewords = "";
foreach($keywords as $keyword) {
    $morewords = $morewords . $keyword . " , ";
}
pdf_set_info($pdf, "Keywords", "Resume, " . $morewords . "apache, mysql, php, pdf");

// Begin PDF page. -- Can be placed anywhere after the PDF
// resource has been instantiated.
pdf_begin_page($pdf, PAGE_WIDTH, PAGE_HEIGHT);

// Print name.
$font = pdf_findfont($pdf, "Times-Bold", "winansi", 0);
pdf_setfont($pdf, $font, 14.0);
$stringwidth = pdf_stringwidth($pdf, $name, $font, 14.0);
$xpos = (PAGE_WIDTH / 2) - ($stringwidth / 2);
pdf_show_xy($pdf, $name, $xpos, 700);
$xpos = pdf_get_value($pdf, "textx", 0);
$ypos = pdf_get_value($pdf, "texty", 0) - VERT_SPACING;

// Print contact information.
$font = pdf_findfont($pdf, "Times-Roman", "winansi", 0);
pdf_setfont($pdf, $font, 12.0);
$headerdata = array($row["Address"],
$row["City"] . ", " . $row["State"] . ", " . $row["ZipCode"],
$row["Phone"],
$row["Email"]);
foreach ($headerdata as $data) {
    $stringwidth = pdf_stringwidth($pdf, $data, $font, 12.0);
    $xpos = (PAGE_WIDTH / 2) - ($stringwidth / 2);
    $xpos = pdf_get_value($pdf, "textx", 0) - VERT_SPACING;
    pdf_show_xy($pdf, $data, $xpos, $ypos);
}

// Print categories.
$sql = "SELECT * FROM items WHERE BIOGRAPHY_OID = 0";
$result = mysql_query($sql);
$prevCategory = "";
while($row = mysql_fetch_array($result, MYSQL_ASSOC)) {
    $curCategory = $row["Category"];
    if (strcmp($prevCategory, $curCategory) != 0) {
        drawHR($pdf);
        pdflib_show($pdf, $row["Category"], CASE_CATEGORY);
    }
    $prevCategory = $row["Category"];
    if (strcmp($row["Category"], "Career Objective") == 0) {
        pdflib_show($pdf, $row["Description"], CASE_OBJECTIVE);
    } else {
        pdflib_show($pdf, $row["Description"], CASE_LIST);
    }
}
// Wrap up the document and return it to the browser.
pdf_end_page($pdf);
pdf_close($pdf);
$buf = pdf_get_buffer($pdf);
$len = strlen($buf);
header("Content-type: application/pdf");
header("Content-Length: $len");
header("Content-Disposition: inline; filename=resume.pdf");
print $buf;
// Clean up!
mysql_close();
$pdf = 0;
?>
```

这个直接明了的应用程序使用从 MySQL 数据库中提取的数据生成一个简单的 PDF 简历。除了 MySQL 连接设置和数据库查询外，该脚本中尚未涵盖的唯一方面是使用传记数据将个人的目标职位信息拼接到文档的关键字中：

```php
$keywords = split(" ", $row["DesiredPosition"]);
$morewords = "";
foreach($keywords as $keyword) {
    $morewords = $morewords . $keyword . ", ";
}
pdf_set_info($pdf, "Keywords", "Resume, ". $morewords . "apache, mysql, php, pdf");
```

简历的头部信息，包含个人的姓名和联系方式，是为了保持辅助函数 `pdfLib_show()` 的实现尽可能简单，从而与简历的其余数据分开处理的。简历的正文由一个 `while` 循环生成，该循环跟踪当前和上一个类别，当值发生变化时打印类别名称；否则，它打印描述。剩下的只是关闭文档，将其返回到浏览器，并进行清理。

最后的一点建议：如果 PDF 生成在你的任何项目中扮演重要角色，你必须阅读并理解随 PDFLib 源代码分发的文档。PHP 网站上通常丰富的文档在涉及 PDFLib 包装器方面尤其缺乏。虽然本文应该是一个极好的介绍，但没有比 PDFLib 手册更好的信息源来了解 PDFLib 库的完整功能。

## GD 库

如果你曾经不得不设置包含大量图片的网站，例如图片库或电子商务网站，其中最繁琐的任务之一是对所有单个图像的操作和上传。幸运的是，PHP 配备了 GD 库，这是一个开源的图像处理库，随 PHP5 捆绑提供。凭借 GD 提供的庞大功能集，你可以自动化网站图像处理的许多或所有任务，因此你只需上传图片，就可以把时间花在其他事情上，而不是长时间扮演“图像管理员”的角色。

### 创建图像基础

GD 库的一个缺点是可用函数数量众多，其中许多执行相同的功能，仅在输入类型或输出图像格式上有所不同。为了提供清晰度并作为本章涵盖的所有图像处理功能的基础，你将创建一个类，用于处理几种最流行的图像文件类型——JPG、GIF 和 PNG 的基本加载和保存。

这个基础类将提供基本的加载、保存和显示功能，并将作为稍后在章节中添加的其他附加图像处理类的调用位置。首先，创建一个名为 class.WebImage.php 的新文件，并输入以下代码：

```php
<?php

class WebImage
{
    public $gdResource;
    public $type;

    // Release resources
    public function __destruct()
    {
        if ($this->gdResource)
        {
            imagedestroy($this->gdResource);
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
            case 'image/jpeg':
                $this->gdResource = imagecreatefromjpeg($file);
                break;
            case 'image/png':
                $this->gdResource = imagecreatefrompng($file);
                break;
            case 'image/gif':
                $this->gdResource = imagecreatefromgif($file);
                break;
        }
        // Retain the alpha information
        imagesavealpha($this->gdResource, true);
    }

    // Save the file to the local filesystem
    public function save($file)
    {
        switch ($this->type)
        {
            case 'image/jpeg':
                imagejpeg($this->gdResource, $file);
                break;
            case 'image/png':
                imagepng($this->gdResource, $file);
                break;
            case 'image/gif':
                // Convert back to palette
                if (imageistruecolor($this->gdResource))
                {
                    imagergptocolorpalette($this->gdResource, false, 256);
                }
                imagegif($this->gdResource, $file);
                break;
        }
    }

    // Display the image in the browser
    public function display()
    {
        switch ($this->type)
        {
            case 'image/jpeg':
                header("Content-type: image/jpeg");
                imagejpeg($this->gdResource);
                break;
            case 'image/png':
                header("Content-type: image/png");
                imagepng($this->gdResource);
                break;
            case 'image/gif':
                // Convert back to palette
                if (imageistruecolor($this->gdResource))
                {
                    imagergbtopalette($this->gdResource, false, 256);
                }
                header("Content-type: image/gif");
                imagegif($this->gdResource);
                break;
        }
    }
}
?>
```

这一切是什么意思？这个文件是一个朴素的图像包装器，你可以用它来打开、保存和显示你的图像。此代码可以处理 JPG、GIF 和 PNG 图像，但你可以轻松添加更多，假设 GD 库支持它们。为了更好地理解正在发生的事情，请查看该类是如何构建的。

开头几行相对直接明了——你首先声明两个公共属性，一个用于保存内部 GD 图像资源，另一个用于跟踪图像操作使用的 MIME 类型。还要注意析构函数——当类被销毁时，它会确保 GD 为该图像消耗的资源被清理：

```php
<?php
class WebImage
{
    public $gdResource;
    public $type;

    // Release resources
    public function __destruct()
    {
        if ($this->gdResource)
        {
            imagedestroy($this->gdResource);
        }
    }
}
?>
```

下一段代码从服务器上的文件中加载图像数据。你向方法传递一个文件名，它确定图像类型，然后使用 GD 库提供的相应函数将图像加载到 GD 资源中：

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
            // ...
    }
}
```
