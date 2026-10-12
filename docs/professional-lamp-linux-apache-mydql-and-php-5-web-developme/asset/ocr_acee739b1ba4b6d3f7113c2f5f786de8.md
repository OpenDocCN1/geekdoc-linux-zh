documentation on the PHP website is particularly lacking where the PDFLib wrapper is concerned. While this text should serve as an excellent introduction, there is no better source of information about the full capabilities of the PDFLib library than the PDFLib manual.

# GD Library

If you've ever had to set up a website containing large amounts of image, such as an image gallery or commerce site, one of the most tedious tasks involved is the manipulation and uploading of all the individual images. Fortunately for you, PHP is equipped with the GD library, an open source image manipulation library that comes bundled with PHP5. With the vast amount of functionality provided by GD, you can automate many or all of your website image processing tasks, so you can simply upload the images, and spend time working on other things, instead of playing image jockey for hours on end.

# Creating the Image Base

One of the downsides to the GD library is the large number of functions available, many of which perform the same function, differing only in the type of input or the output image format. To provide some clarity and a base for all of the image manipulation functionality this part of the chapter covers, you'll create a class that handles the basic loading and saving of a couple of the most popular image file types— JPC, GIF, and PNG.

This base class will provide basic load, save, and display capabilities, and will serve as a place to call other add-on image manipulation classes that you'll add later in the chapter. First, create a new file called class.WebImage.php, and enter the following code:

```
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
```
```