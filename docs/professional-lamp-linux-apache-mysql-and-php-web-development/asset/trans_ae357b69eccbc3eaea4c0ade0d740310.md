

PHP 安装所在的目录。PDFLib 支持多种字体和字形。请参阅 PDFLib 文档以获取完整详细信息。

最后，`pdf_show_xy()` 函数会在指定位置显示给定的字符串。

## 关于字体和定位

在前面的代码示例中，你看到了如何通过 PHP 内置的 PDFLib 函数操作各种文本属性。同样，开发者需谨慎使用其他已弃用的函数，例如已被单一的 `pdf_get_value()` 函数替代的 `pdf_get_font()` 和 `pdf_get_fontsize()`。该函数的使用方法与前述的 `pdf_set_info()` 完全相同。PHP 文档（<http://www.php.net/manual/en/ref.pdf.php#AEN124842>）列出了已弃用的函数及其替代方案。

> *PDFLib 坐标系将文档左下角的 xy 坐标定义为 0:0。*

你通常会发现为诸如边距、制表宽度、垂直间距和页面尺寸等页面属性定义常量会很有帮助。下表列出了常见页面尺寸的点数维度，其中 1 pt = 1/72 英寸 = 0.3528 毫米。

| 格式 | 宽度 | 高度 |
|---|---|---|
| A4 | 595 | 842 |
| B5 | 501 | 709 |
| Letter | 612 | 792 |
| Legal | 612 | 1008 |

## 收尾工作

如果你只是想创建一个文档并将其放在本地主机的某个位置，完成 PDF 文件只需结束页面并关闭文档即可。但更常见的情况是，缓冲区会返回给 Web 浏览器。`pdf_get_buffer()` 函数用于检索传入的 PDF 文档。然后，通过 `header()` 函数通知浏览器即将接收到一个 PDF 文档，简单地调用 `print` 即可完成整个过程，如下所示：

```php
pdf_end_page($pdf);
pdf_close($pdf);
$buf = pdf_get_buffer($pdf);
$len = strlen($buf);
header("Content-type: application/pdf");
header("Content-Length: $len");
header("Content-Disposition: inline; filename=resume.pdf");
print $buf;
```

本部分仅简要介绍了高级 PHP 开发者可用的众多 PDF 生成功能。我们尚未涉及的其他可用功能包括书签、超文本、颜色使用、图形生成和导入，以及这里无法一一列举的更多功能。

## PDF 简历生成器

考虑以下代码：

```php
<?php

// 指定字符串常量和定位变量。
define("CASE_CATEGORY",    "Category");
define("CASE_LIST",        "List");
define("CASE_OBJECTIVE",   "Objective");
define("MARGIN",           50);
define("PAGE_HEIGHT",      792);
define("PAGE_WIDTH",       612);
define("TAB",              25);
define("VERT_SPACING",     14);

// 定义几个有用的函数。
function drawHR($res) {
    $xpos = MARGIN;
    $ypos = pdf_get_value($res, "texty", 0) - VERT_SPACING;
    pdf_moveto($res, $xpos, $ypos);
    pdf_lineto($res, PAGE_WIDTH - MARGIN, $ypos);
    pdf_closepath($res);
    pdf_fill($res);
    $ypos = pdf_get_value($res, "texty", 0) - (VERT_SPACING * 2);
}

function pdflib_show($res, $text, $type) {
    $font = pdflib_findfont($res, "Times-Roman", "winansi", 0);
    $xpos = MARGIN;
    $ypos = pdf_get_value($res, "texty", 0) - VERT_SPACING;

    switch ($type) {
        case CASE_CATEGORY:
            $font = pdf_findfont($res, "Times-Bold", "winansi", 0);
            $ypos = pdf_get_value($res, 'texty', 0) - (VERT_SPACING * 3);
            break;
        case CASE_LIST:
            $xpos = MARGIN + TAB;
            $text = "*" . $text;
            break;
        case CASE_OBJECTIVE:
            $font = pdf_findfont($res, "Times-Italic", "winansi", 0);
            $xpos = MARGIN + TAB;
            $text = "*" . $text . "*";
            break;
    }
    pdf_setfont($res, $font, 12.0);
    pdf_show_xy($res, $text, $xpos, $ypos);
    return;
}

// 创建资源。
$pdf = pdf_new();
if (!pdf_open_file($pdf, "")) {
    die("Error: Unable to open output file.");
}

// 从数据库收集头部信息。
mysql_connect("localhost", "resume_user", "resume_pw");
mysql_select_db("resume");
$sql = "SELECT * FROM biography WHERE OID = 0";
$result = mysql_query($sql);
$row = mysql_fetch_array($result, MYSQL_ASSOC);
$name = $row["NameFirst"] . " " . $row["LastName"];

// 文档信息。
pdf_set_info($pdf, "Author", $name . " " . $row["Email"] . "<>");
pdf_set_info($pdf, "Title", "Resume - " . $name);
pdf_set_info($pdf, "Subject", "The resume of " . $name . ", "
    . $row["DesiredPosition"] . ".");

// 对关键词做一些巧妙的处理。
$keywords = split(" ", $row["DesiredPosition"]);
$morewords = "";
foreach($keywords as $keyword) {
    $morewords = $morewords . $keyword . ", ";
}
pdf_set_info($pdf, "Keywords", "Resume, " . $morewords . "Apache, MySQL, PHP, PDF");

// 开始 PDF 页面。 -- 可以放在 PDF 资源实例化后的任何位置。
pdf_begin_page($pdf, PAGE_WIDTH, PAGE_HEIGHT);

// 打印姓名。
$font = pdf_findfont($pdf, "Times-Bold", "winansi", 0);
pdf_setfont($pdf, $font, 14.0);
$stringwidth = pdf_stringwidth($pdf, $name, $font, 14.0);
$xpos = (PAGE_WIDTH / 2) - ($stringwidth / 2);
pdf_show_xy($pdf, $name, $xpos, 700);
$xpos = pdf_get_value($pdf, "textx", 0);
$ypos = pdf_get_value($pdf, "texty", 0) - VERT_SPACING;

// 打印联系信息。
$font = pdf_findfont($pdf, "Times-Roman", "winansi", 0);
pdf_setfont($pdf, $font, 12.0);
$headerdata = array(
    $row["Address"],
    $row["City"] . ", " . $row["State"] . " " . $row["ZipCode"],
    $row["Phone"],
    $row["Email"]
);
foreach ($headerdata as $data) {
    $stringwidth = pdf_stringwidth($pdf, $data, $font, 12.0);
    $xpos = (PAGE_WIDTH / 2) - ($stringwidth / 2);
    $ypos = pdf_get_value($pdf, "texty", 0) - VERT_SPACING;
    pdf_show_xy($pdf, $data, $xpos, $ypos);
}

// 打印分类。
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

// 结束文档并将其返回给浏览器。
pdf_end_page($pdf);
pdf_close($pdf);
$buf = pdf_get_buffer($pdf);
$len = strlen($buf);
header("Content-type: application/pdf");
header("Content-Length: $len");
header("Content-Disposition: inline; filename=resume.pdf");
print $buf;

// 清理工作！
mysql_close();
$pdf = 0; 
?>
```

这个简洁的应用程序使用从 MySQL 数据库中提取的数据生成一个简单的 PDF 简历。除了 MySQL 连接设置和数据库查询外，这个脚本中尚未涵盖的唯一方面是使用传记数据将个人期望职位的信息拼接到文档的关键词中：

```php
$keywords = split(" ", $row["DesiredPosition"]); 
$morewords = "";
foreach($keywords as $keyword) {
  $morewords = $morewords . $keyword . ", ";
}
pdf_set_info($pdf, "Keywords", "Resume, " . $morewords . "Apache, MySQL, PHP, PDF");
```

简历的头部信息，包含个人的姓名和联系信息，被单独处理，与简历其余数据分开，以便尽可能简化辅助函数 `pdflib_show()` 的实现。简历的主体由一个 while 循环生成，该循环跟踪当前和之前的分类，当值改变时打印分类名称；否则，打印描述。剩下的工作就是关闭文档，将其返回给浏览器，并进行清理。

最后一点建议：如果 PDF 生成在你的任何项目中都扮演着重要角色，你必须阅读并理解随 PDFLib 源代码分发的文档。通常丰富的
