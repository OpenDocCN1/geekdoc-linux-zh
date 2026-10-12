
## Chapter 10

Last, try out the image logo application. In this example, you’re going to place a logo in the lower-right corner of the image, on top of the caption box:

```php
<?php

require_once 'class.WebImage.php';

$img = new WebImage();
$img->load('base.png');
$img->caption('An example of plantlife found on Maui.',
		'FUJIWIDR.TTF',
		13,
		5,
		true);
$img->logo('logo.png', 'r', 'b', 5, 0.3);
$img->display();
?>
```

And now, a logo should appear, resized a little, in the lower-right corner with 5px of padding, as in Figure 10.5.

![](img/cacdd24f2926f10ee3219256ad732604_287_0.png)

As you can see, using the GD library is not hard to use and allows for quite a bit of flexibility and control over your images. There are many other more advanced functions you can use, all of which can be found at the GD section of the PHP Manual (http://www.php.net/gd).

## Ming

Ming is a third-party extension to PHP that allows a user to create Shockwave Flash files without actually having to use Macromedia’s Flash studio. The functionality that Ming provides isn’t always the same as what is available in Macromedia’s Flash, because of the nature of how the Flash files are created using PHP and Ming. Ming does provide a method to create Flash files that is low cost and allows for content to be dynamically created when it is needed.

### About Ming

The usefulness of dynamically created Flash files can sometimes be lost for some people, especially because you will not have the precise visual control over the content layout that people who use Macromedia’s Flash Studio employ. Also, the feature set of Ming is limited to that of Flash version 4, which is several versions behind the latest available. But being able to script the creation and add dynamic content to the application is something that you can’t do using Macromedia’s Flash Studio. This can be helpful in distributing content to users where you need the features of Flash but also want to personalize the content for the user.

Ming itself is actually a third-party extension that has had PHP wrapper extensions written for it, so it needs to be compiled into the PHP binary when the binary is built. Instructions for Ming installation with PHP can be found on PHP’s website (http://www.php.net/ming). More information about Ming itself can be found at Ming’s site on SourceForge.Net (http://ming.sourceforge.net). There are also many tutorials and examples available on the Internet that can help to illustrate the functionality of Ming as well as provide pieces of code that are suitable to be used as a foundation to build on for your Flash movies.

Ming is implemented in PHP as objects, so that any time you create a shockwave file with Ming in PHP you need to at least instantiate an instance of the SWFmovie object. The following is some code of a very simple file generated with Ming and PHP. To run this code, insert it into a PHP file with no other content in it, and then view that file in a web browser that has the Flash plug-in installed:

```php
<?php
header("Content-type: application/x-shockwave-flash");
$a = new SWFmovie();
$a->setDimension(100,100); //width and length in that order
$a->setBackground(0,0,255); // red, green, and blue integers
$a->output();
?>
```

This does not generate much, but it does produce a giant blue screen in your browser. Examining the code, you can see some of the necessary pieces that will need to be included in any Flash file created with Ming. The first line tells PHP to set the Content-type header so that the browser knows that it is a shockwave file and to load the appropriate plug-in for it. The next line actually creates the instance of the SWFMovie object. The next two lines are optional, but without them, it would be hard to tell that anything was generated, as they set the size of the shockwave file as well as make its background blue. The last line tells PHP to write the Ming generated file out to the browser. The only thing to really make sure to do here is set the proper header Content-type before outputting the movie as well as make sure no other content is sent to the browser, such as stray lines and white space.

There can only be one instance of the SWFMovie object, but you can include multiple mini movies in one SWFMovie object. In order to do this, you need to use another object, the SWFSprite object. This object has similar qualities and attributes to the SWFMovie object, but isn’t limited to only one per movie. The advantage to this is that you can have multiple animations showing at the same time in the same Flash movie. Each of the animations can even be running at different rates as well as be different lengths in time.

Flash files use *frames*, just like frames in a movie or animation. The objects SWFMovie and SWFSprite both have functions to add new frames to them. Frames are useful if you can display different objects to the screen by including them in specific frames. This means that if you want two or more objects to be displayed at the same time, they need to have a common frame. Once an object is added to a frame, every frame after it contains that object until the object is removed from the movie. Also, just like a movie or animation you can go forwards or backwards, as well as skipping to a specific frame using the SWFAction object. This use of frames provides a better way to group objects as well as generate timelines in your Flash movies.

Ming and Flash both use a coordinate system that may be different than what you’re used to. The unit of distance that is used by Flash is the twip. The twip is *defined* as being exactly 1/1440 of an inch or 1/20 of a point in size. This measurement usually is simplified for easy conversion to a value of 20 twip units to 1 pixel. However, this can be an arbitrary value, as the Flash player will scale the movie to the size of the player window itself. Fortunately, the SWFBitmap object included in Ming has functionality to determine what size an image is in twips. Therefore, if you need to have a movie with dimensions based on the size of an image, you simply need to create the SWFBitmap object, read its width and height values, and then set the dimensions of the movie itself based on it. The dimension of a movie does not necessarily need to be set until right before it is displayed.

### Objects in Ming

There are a total of 13 objects that PHP provides to generate Flash files with Ming. You can use a combination of these objects to create many complex Flash files with a wide variety of functionality. They are as follows:

- The SWFAction object lets you add logic and functionality beyond a simple image display to your Flash file. Using SWFAction you can move images and shapes around for things such as games, as well as read and set properties of objects in the Flash file. Also, you can include some ActionScript scripts, which is Flash’s version of JavaScript and is quite similar. This object is used commonly with the SWFButton object to perform some action when the user presses the button. Common actions used are the displaying of specific frames in a Flash movie based on a response from the user.

- The SWFBitmap object allows for images to be added to the Flash file. There are several limitations, though, as only non-progressive scan JPEG images and DBL (“define bits lossless”) images can be added this way. Any other image needs to be converted to one of these formats using either another extension, such as GD, or by making a system call to a utility. This object many times is used with SWFSprite and the SWFSpace objects.

- The SWFButton object adds a button to your Flash file. This button can be used to initiate an action of the SWFAction object. It reacts to common mouse actions such as mousedown, mouseup, and rollover. A shape can be added to the button to change its appearance.

- The SWFDisplayItem object allows a shape, text object, sprite, or button to be manipulated after being added to a movie by referencing the item using its returned handle after being added to the movie. Operations such as skewing, scaling, and moving items are all possible operations.

- The SWFFill object is generated by use of the addFill method of the SWFShape object. It allows the fill to be transformed by rotating, skewing, and scaling the fill of the shape.

- The SWFFont object loads a font for use by the SWFText object. The font can either be a font definition block (FDB) or a browser-defined font reference.

- The SWFGradient object creates a gradient that can then be used by the SWFShape method addFill().

- The SWFMorph will take two shapes and morph the first into the second shape. This can be used for some basic animation.

- The SWFMovie object is the one object that is necessary for any other objects to work correctly, as it is the object that actually writes the Flash file out, either to a file or to a browser.

- The SWFShape object generates a shape. The shape is actually drawn by passing coordinates that are drawn with an imaginary pen. With the right coordinates, almost any shape can be generated. Also, as mentioned before, this is used with the SWFBitmap object to add an image file to the movie.

- The SWFSprite object generates a “movie clip” or animation by adding frames to the object. A frame contains one of the other objects, such as SWFShape. There can be multiple SWFSprite objects in a single frame so that two animations are seen going at the same time. The advantage of adding images to a SWFSprite object compared to just a SWFMovie object is that it encapsulates the objects better for manipulation.

- The SWFText object displays text in a Flash animation. An alternative to using the SWFText object if you need to display only small amounts of static information is to just use images instead of using Flash to write the text.

- The SWFTextField is similar to a SWFText object, but with a few differences. SWFTextField objects can’t be rotated or skewed, but can function as form entries.

### Creating a Flash Display

With a few more lines of code, you can expand the earlier example to something that is slightly more interesting to look at:

```php
<?php
header('Content-type: application/x-shockwave-flash');
$movie = new SWFMovie();
$movie->setDimension(100,100); //width and length in that order
$movie->setBackground(0,0,255); // red, green, and blue integers

$shape = new SWFShape(); //generate a shape object
$shape->setLine(4, 30, 60, 100); //set the line width to 4 along
// with red, green, and blue integer values
$shape->setLeftFill($movie->addFill(300, 200, 100));
//set the color of the shape with red, green
// and integer values
$shape->movePenTo(20, 20);
```
