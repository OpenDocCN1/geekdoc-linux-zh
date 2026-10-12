# Chapter 7

```
'font_size' => 25,
    'font_path' => './',
    'font_file' => 'VeraMono.TTF'
);  
// Create a CAPTCHA object  
$cap = text_CAPTCHA::factory('Image');
// Initialize the CAPTCHA object with random text 
$r = $cap->init(250,100, null, $opts);  
// Check if CAPTCHA object is valid  
if (PEAR::isError($r))  
{  
    echo 'CAPTCHA Generation failed.';  
    exit;  
}  
// Generate the PNG CAPTCHA image  
$png = $cap->getCaptchaAsPNG();  
// Show the image in the browser  
header('Content-type: image/png');  
echo $png;  
?>
```

When you run this code in your browser, you should see something like Figure 7.1.

![](bbox=[0.16, 0.55, 0.78, 0.88])