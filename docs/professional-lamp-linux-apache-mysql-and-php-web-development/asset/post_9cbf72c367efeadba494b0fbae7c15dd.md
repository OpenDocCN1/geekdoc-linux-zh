
# Chapter 9

The best time to performance-tune a program is before it's written. When building a site, test, experiment, and gain experience in the various ways it could be designed, and the pros and cons of each. Choosing the right framework at the beginning will have a much bigger influence on the speed of the final product than any amount of code tweaking after the fact. Keep testing, experimenting, and gaining experience, and keep looking at the big picture, because neither hardware nor software technology is standing still. Processors will be faster, memory will be cheaper, network connections will be more capacious, web servers will be more efficient, web browsers will be more sophisticated, and PHP will have more features to develop with.

## Chapter 10: PHP Extensions

Although the core of the PHP language provides functions that accomplish many commonly needed tasks, there are numerous extensions that can be added to bring a PHP configuration to a whole new level. This chapter explores some of the more useful extensions, but it only touches on the tip of the iceberg. The extensions in this chapter deal with manipulating images, creating PDF files (without the use of Adobe Acrobat), creating flash files (without the use of any commercial software), and interfacing with XML documents. Some of these extensions are already bundled and enabled for you with the default configuration, so what are you waiting for?

### PDFLib

Whether your content is academic or commercial in nature, no professionally developed website would be complete without the ability to deliver content as a PDF (Portable Document Format). While there are several Open Source libraries available to PHP developers, notably FPDF (http://www.fpdf.org/), and pdf-php (http://sourceforge.net/projects/pdf-php), PHP’s built-in PDFLib functions are arguably the most efficient means of doing so. The PDFlib functions, moved to the PHP Extension Community Library (PECL) since PHP 4.3.9, are a wrapper for the commercial PDFLib (http://www.pdflib.com/) PDF processing library. The advantage offered by PDFLib over the purely PHP-based solutions is that of speed. Compiled C code, such as PDFLib, is magnitudes of order faster than PHP code interpreted by Apache. The disadvantage is the licensing cost for commercial use.

> *The observant reader will note that this text refers to two distinct capitalizations of the subject matter: “PDFLib” and “PDFlib.” This is to differentiate the C library, named “PDFlib” by its owners, from the PHP wrapper library “PDFLib.” It is also noteworthy that the C library documentation does not rigidly adhere to this convention.*

#### Configuration

PHP's support for PDFLib has undergone significant changes recently, and like so many other features of the language and its myriad libraries, it is expected to undergo further changes, especially in light of the growing acceptance of PHP within the professional development community.

Thus, configuration is highly susceptible to the usual sticking points of architecture, operating system, PHP version, and so on. If your Apache installation is using dynamic shared objects (DSO), or dynamic link libraries (DLL) for Windows installations, then all that is required is ensuring that the appropriate file exists (libpdf_php.so or libpdf_php.dll, respectively), and is referenced properly and uncommented in the php.ini file.

If you are not using DSO, or can't, you will have to visit the PDFLib website (http://www.pdflib.com/), acquire the latest version of one of the many flavors of the PDFLib source, and build a statically linked library. For further details visit http://www.pdflib.com/products/pdflib/info/PDFlib-in-PHP-HowTo.pdf.

Regardless of how you install PDFLib, it is worthwhile to visit the PDFLib website and download the latest version of PDFLib Lite. Included with the source is a very helpful document, PDFlib-manual.pdf. The manual contains a variety of useful information, including bindings for all supported programming languages, general PDFLib programming concepts, and much more. Section 3.1.1, “PDFLib Program Structure and Function Scopes,” is a must read that will save you hours of frustration trying to eliminate “scope” errors.

#### Getting Started

The PDF document will be known to PHP as a resource type, and you create it using the `pdf_new()` function, as follows:

```php
$pdf = pdf_new();
if (!pdf_open_file($pdf, "")) {
    die("Error: Unable to output file");
}
```

Note that immediately after the resource is created, a test ensures that the resource was created and opened. Attempting to proceed with any page scope functions without this check will cause the script to fail, and will generate the following PDFLib exception:

> Function must not be called in 'object' scope

In other words, a page scope function has been called in object scope, since the document will not have been opened yet. In PHP5, it is sufficient to enclose the `pdf_new()` call within a `try/catch` block that catches a type `PDFLibException` exception.

Upon completion of the PDF document, you can call `pdf_close()` to close the document file and release any associated resources.

#### Specifying Document Information

One means of searching documents is via the metadata contained within the document information. This is achieved easily using the `pdf_set_info()` function. Section 8.9.6, "Document Information Fields" of the PDFLib manual specifies which fields are relevant. For example:

```php
pdf_set_info($pdf, "Author", $name . " <" . $row['Email'] . ">");

pdf_set_info($pdf, "Title", "Resume = " . $name);

pdf_set_info($pdf, "Subject", "The resume of " . $name . ", " . $row['DesiredPosition'] . ".");
```

This code sets the document's author, title, and subject to values pulled from a MySQL database. Note that the `pdf_set_info()` function replaces a number of deprecated functions that set fields specifically.

#### Required Elements

To render the most basic page, every PDFlib generated document requires the following elements:

- `pdf_new()`: Needed to create a new PDF resource.
- `pdf_open_file($pdf [, $filename])`: Accepts a PDF resource and an optional filename as parameters. The filename is unnecessary for buffered output, as in the example at the end of this section.
- `pdf_begin_page($pdf, $width, $height)`: Accepts a PDF resource as well as the width and height of the page in points.
- `pdf_findfont($pdf, $font, $encoding [, $embed])`: Locates a font given a PDF resource, a specific font name, and encoding as parameters. Passing a non-zero value as the optional fourth parameter will cause the font to be immediately checked, averting subsequent errors.
- `pdf_setfont($pdf, $font, $size)`: Accepts a PDF resource, a font handle (as returned by the `pdf_findfont` function above), and a font size.
- `pdf_show_xy($pdf, $text, $x, $y)`: Places the passed text within the given PDF resource at the given x and y coordinates given in points.
- `pdf_stroke($pdf)`: "Inks" or draws the text on the passed PDF resource.
- `pdf_end_page($pdf)`: Finishes the current page of the given PDF resource.
- `pdf_close($pdf)`: Closes the passed PDF resource.

The resume generator example that winds up this section uses each of these functions to return a PDF document to the browser instead of placing the file somewhere within the local file structure.

#### Helper Functions

Given that certain sections of a typical document adhere to a specific style, you may find it useful to create several helper functions to simplify code maintenance and style changes. One particularly useful function would draw a horizontal line, not a trivial matter when generating a PDF, as follows:

```php
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

The `drawHR()` function accepts a PDF resource, `$res`, as an argument. It sets the initial x and y positions of the line, using constant values and the `pdf_get_value()` function with the `texty` parameter. The third parameter of the `pdf_get_value()` function is a numeric “modifier” applied to the value specified by the second parameter. In most trivial cases, the value of this parameter will be 0. Thus, the last line of the `drawHR` function might more elegantly be written as follows:

```php
$ypos = pdf_get_value($res, "texty", (VERT_SPACING * -2));
```

A useful concept to grasp in PDF document creation is that of the `path.` The `pdf_moveto()` function positions the starting point within the document and `pdf_lineto()` draws a line along the path between the two positions. The `pdf_closepath()` and `pdf_fill()` functions close then fills the path. Finally, the y position is incremented by twice the vertical spacing constant.

Another useful function might apply similar, yet distinct styles in accordance with a passed parameter:

```php
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
            $text = "*" . $text . "*";
            break;
    }
    pdf_setfont($res, $font, 12.0);
    pdf_show_xy($res, $text, $xpos, $ypos);
    return;
}
```

As you will see in the example that wraps up this section, this code uses a `switch` control structure to set specific type faces and text positioning according to the value of the `$type` parameter.

Font selection is performed by the `pdf_findfont()` function and set via the `pdf_setfont()` function. PHP’s PDFlib implementation typically installs a few fonts by default in the “pdf-related” directory in
