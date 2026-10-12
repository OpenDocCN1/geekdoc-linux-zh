# Chapter 10

```
```
    }
    return $gd_img;
})
```
```

# ### Adding a Logo

The final bit of functionality you're going to add to the `WebImage` class is the ability to place a logo or watermark on an image.

Start by creating the `class.ImageLogo.php` file:

```
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
```
```