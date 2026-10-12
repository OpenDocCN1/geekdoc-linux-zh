PHP Extensions

# Specifying Document Information

One means of searching documents is via the metadata contained with the document information. This is achieved easily using the `pdf_set_info()` function. Section 8.9.6, "Document Information Fields" of the PDFLib manual specifies which fields are relevant. For example:

```
pdf_set_info($pdf, "Author", $name . " <" . $row['Email'] . ">\");

pdf_set_info($pdf, "Title", "Resume = " . $name);

pdf_set_info($pdf, "Subject", "The resume of " . $name . ", " .

$row['DesiredPosition'] . "\");
```

This code sets the document's author, title, and subject to values pulled from a MySQL database. Note that the `pdf_set_info()` function replaces a number of deprecated functions that set fields specifically.

# Required Elements

To render the most basic page, every PDFlib generated document requires the following elements:

+   *   `pdf_new()`: Needed to create a new PDF resource.
+   
+   *   `pdf_open_file($pdf [, $filename])`: Accepts a PDF resource and an optional filename as parameters. The filename is unnecessary for buffered output, as in the example at the end of this section.
+   
+   *   `pdf_begin_page($pdf, $width, $height)`: Accepts a PDF resource as well as the width and height of the page in points.
+   
+   *   `pdf_findfont($pdf, $font, $encoding [, $embed])`: Locates a font given a PDF resource, a specific font name, and encoding as parameters. Passing a non-zero value as the optional fourth parameter will cause the font to be immediately checked, averting subsequent errors.
+   
+   *   `pdf_setfont($pdf, $font, $size)`: Accepts a PDF resource, a font handle (as returned by the `pdf_findfont` function above), and a font size.
+   
+   *   `pdf_show_xy($pdf, $text, $x, $y)`: Places the passed text within the given PDF resource at the given x and y coordinates given in points.
+   
+   *   `pdf_stroke($pdf)`: "Inks" or draws the text on the passed PDF resource.
+   
+   *   `pdf_end_page($pdf)`: Finishes the current page of the given PDF resource.
+   
+   *   `pdf_close($pdf)`: Closes the passed PDF resource.

The resume generator example that winds up this section uses each of these functions to return a PDF document to the browser instead of placing the file somewhere within the local file structure.

# Helper Functions

Given that certain sections of a typical document adhere to a specific style, you may find it useful to create several helper functions to simplify code maintenance and style changes. One particularly useful function would draw a horizontal line, not a trivial matter when generating a PDF, as follows:

235