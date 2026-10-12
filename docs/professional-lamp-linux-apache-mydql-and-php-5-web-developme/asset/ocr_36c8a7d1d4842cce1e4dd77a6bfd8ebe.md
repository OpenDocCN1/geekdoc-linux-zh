```
```php
<?php

require_once 'class.WebImage.php';

$img = new WebImage();
$img->load('base.png');
$img->display();
?>
```
```

Load this file in your browser, and it should display your image, as in Figure 10.1.

![](bbox=[0.08, 0.31, 0.87, 0.75])

**Figure 10.1**

If you wanted to change the type of the image before saving or displaying it, you’d simply need to set the type of the image in the `WebImage` object:

```
```php
<?php

require_once 'class.WebImage.php';

$img = new WebImage();
```
```