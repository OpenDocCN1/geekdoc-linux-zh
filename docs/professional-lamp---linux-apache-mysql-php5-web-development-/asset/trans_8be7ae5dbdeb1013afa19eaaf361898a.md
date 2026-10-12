
## 指定文档信息

搜索文档的一种方式是通过文档信息中包含的元数据。使用 `pdf_set_info()` 函数可以轻松地实现这一点。PDFLib 手册第 8.9.6 节“文档信息字段”指定了哪些字段是相关的。例如：

```php
pdf_set_info($pdf, "Author", $name . " <" . $row["Email"] . ">");
pdf_set_info($pdf, "Title", "Resume: " . $name);
pdf_set_info($pdf, "Subject", "The resume of " . $name . " " .
                               $row["DesiredPosition"] . "");
```

此代码将文档的作者、标题和主题设置为从 MySQL 数据库中获取的值。请注意，`pdf_set_info()` 函数取代了众多用于专门设置字段的已弃用函数。

## 必需元素

要渲染最基本的页面，每个由 PDFlib 生成的文档都需要以下元素：

-   `pdf_new()`：用于创建新的 PDF 资源。
-   `pdf_open_file($pdf [, $filename])`：接受一个 PDF 资源和一个可选的文件名作为参数。对于缓冲输出（如本节末尾的示例所示），文件名不是必需的。
-   `pdf_begin_page($pdf, $width, $height)`：接受一个 PDF 资源以及以点（points）为单位的页面宽度和高度。
-   `pdf_findfont($pdf, $font, $encoding [, $embed])`：根据给定的 PDF 资源、特定字体名称和编码参数来定位字体。将非零值作为可选的第四个参数传递，会导致立即检查该字体，从而避免后续错误。
-   `pdf_setfont($pdf, $font, $size)`：接受一个 PDF 资源、一个字体句柄（由上述 pdf_findfont 函数返回）以及一个字体大小。
-   `pdf_show_xy($pdf, $text, $x, $y)`：在指定的 PDF 资源中，将传入的文本放置在给定的 x 和 y 坐标处（以点为单位）。
-   `pdf_stroke($pdf)`：在传入的 PDF 资源上“着墨”或绘制文本。
-   `pdf_end_page($pdf)`：结束给定 PDF 资源的当前页。
-   `pdf_close($pdf)`：关闭传入的 PDF 资源。

本结尾处的简历生成器示例使用这些函数中的每一个，将 PDF 文档返回给浏览器，而不是将文件放置在本地文件结构的某个位置。

## 辅助函数

鉴于典型文档的某些部分遵循特定样式，您可能认为创建几个辅助函数以简化代码维护和样式变更很有用。一个特别有用的函数是绘制水平线，这在生成 PDF 时并非易事，如下所示：

```text
function drawHR($res) {
    $xpos = MARGIN;
    $ypos = pdf_get_value($res, "texty", 0) - VERT_SPACING;
    pdf_moveto($res, $xpos, $ypos);
    pdf_lineto($res, PAGE_WIDTH - MARGIN, $ypos);
    pdf_closepath($res);
    pdf_fill($res);
    $ypos = pdf_get_value($res, "texty", 0) - (VERT_SPACING * 2);
}
```

`drawHR()` 函数接受一个 PDF 资源 `$res` 作为参数。它使用常量值和带有 `texty` 参数的 `pdf_get_value()` 函数来设置线条的初始 x 和 y 位置。`pdf_get_value()` 函数的第三个参数是一个应用于由第二个参数指定的值的数字“修饰符”。在最简单的情况下，该参数的值为 0。因此，`drawHR` 函数的最后一行可以更优雅地写为：

```text
$ypos = pdf_get_value($res, "texty", (VERT_SPACING * -2));
```

在创建 PDF 文档时，需要掌握的一个有用概念是“路径”（path）。`pdf_moveto()` 函数在文档内定位起点，`pdf_lineto()` 在两个位置之间的路径上绘制线条。`pdf_closepath()` 和 `pdf_fill()` 函数分别闭合并填充路径。最后，y 位置增加了两倍垂直间距常数的值。

另一个有用的函数可以根据传入的参数应用相似但不同的样式：

```text
function pdflib_show($res, $text, $type) {
    $font = pdf_findfont($res, "Times-Roman", "winansi", 0);
    $xpos = MARGIN;
    $ypos = pdf_get_value($res, "texty", 0) - VERT_SPACING;
    switch ($type) {
        case CASE_CATEGORY:
            $font = pdf_findfont($res, "Times-Bold", "winansi", 0);
            $ypos = pdf_get_value($res, "texty", 0) - (VERT_SPACING * 3);
            break;
        case CASE_LIST:
            $xpos = MARGIN + TAB;
            $text = "* " . $text;
            break;
        case CASE_OBJECTIVE:
            $font = pdf_findfont($res, "Times-Italic", "winansi", 0);
            $xpos = MARGIN + TAB;
            $text = "\"" . $text . "\"";
            break;
    }
    pdf_setfont($res, $font, 12.0);
    pdf_show_xy($res, $text, $xpos, $ypos);
    return;
}
```

如您将在本节结尾的示例中看到，此代码使用 switch 控制结构根据 `$type` 参数的值设置特定的字体样式和文本位置。

字体选择由 `pdf_findfont()` 函数执行，并通过 `pdf_setfont()` 函数设置。PHP 的 PDFlib 实现通常默认在安装 PHP 的目录内的“pdf-related”目录中安装几种字体。PDFLib 支持各种各样的字体和样式。完整详情请参阅 PDFLib 文档。

最后，`pdf_show_xy()` 函数在指定位置显示给定的字符串。

## 关于字体和定位

在前面的代码示例中，您看到了如何通过 PHP 内置的 PDFLib 函数操纵各种文本属性。再次提醒开发人员，避免使用其他已弃用的函数，例如已被单个 `pdf_get_value()` 函数取代的 `pdf_get_font()` 和 `pdf_get_fontsize()`。该函数的用法与前述的 `pdf_set_info()` 函数相同。PHP 的文档 ([http://www.php.net/manual/en/ref.pdf.php#AEN124842](http://www.php.net/manual/en/ref.pdf.php#AEN124842)) 列出了已弃用的函数及其替代方案。

> PDFLib 坐标系将 x:y 坐标 0:0 定义为文档的左下角。

您可能觉得定义常量以表示此类页面属性会有帮助，例如边距和制表位宽度、垂直间距以及页面尺寸。下表列出了更常见的页面尺寸的点数（points）维度，其中 1 pt = 1/72 英寸 = 0.3528 毫米。

| 格式 | 宽度 | 高度 |
|---|---|---|
| A4 | 595 | 842 |
| B5 | 501 | 709 |
| Letter | 612 | 792 |
| Legal | 612 | 1008 |

## 收尾工作

如果您只是想创建一个文档并将其放置在本地主机的某处，完成 PDF 文件所需做的只是结束页面并完全关闭它。不过，更常见的是，向 Web 浏览器返回一个缓冲区。`pdf_get_buffer()` 函数检索传入的 PDF 文档。然后通过 `header()` 函数通知浏览器预期接收一个 PDF 文档，简单的打印调用即可完成整个过程，如下所示：

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

本节仅简要提及了高级 PHP 开发者可用的众多 PDF 生成功能。我们未涉及的其他可用方面包括书签、超文本、颜色使用、图形生成和导入，以及太多无法在此一一列举的功能。

## PDF 简历生成器

请考虑以下代码：

```php
<?php

// Specify string constants and positioning variables.
define("CASE_CATEGORY", "Category");
define("CASE_LIST", "List");
define("CASE_OBJECTIVE", "Objective");
define("MARGIN", 50);
define("PAGE_HEIGHT", 792);
define("PAGE_WIDTH", 612);
define("TAB", 25);
define("VERT_SPACING", 14);

// Define a couple useful functions.
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
    $font = pdf_findfont($res, "Times-Roman", "winansi", 0);
    $xpos = MARGIN;
    $ypos = pdf_get_value($res, "texty", 0) - VERT_SPACING;

    switch ($type) {
        case CASE_CATEGORY:
            $font = pdf_findfont($res, "Times-Bold", "winansi", 0);
            $ypos = pdf_get_value($res, "texty", 0) - (VERT_SPACING * 3);
            break;
        case CASE_LIST:
            $xpos = MARGIN + TAB;
            $text = "*" . $text;
            break;
        case CASE_OBJECTIVE:
            $font = pdf_findfont($res, "Times-Italic", "winansi", 0);
            $xpos = MARGIN + TAB;
            $text = "\"" . $text . "\"";
            break;
    }
    pdf_selectfont($res, $font, 12.0);
    pdf_show_xy($res, $text, $xpos, $ypos);
    return;
}

// Create resource.
$pdf = pdf_new();
if (!pdf_open_file($pdf, "")) {
```

