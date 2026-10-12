# ## Adding images

With the tkinter module, images in GIF or PGM/PPM file formats can be displayed on Label, Button, Text and Canvas widgets using the *PhotoImage()* constructor to create image objects. This simply requires a single *file=* argument to specify the image file. Interestingly, it also has a *subsample()* method that can scale down a specified image by stating a sample value to *x=* and *y=* arguments. For example, values of *x*=2, *y*=2 samples every second pixel – so the image object is half-size of the original.

Once an image object has been created, it can be added to a Label or Button constructor statement by an *image=* option.

Text objects have an *image_create()* method with which to embed an image into the text field. This requires two arguments to specify location and *image=*. For example, *‘1,0’* specifies the first line and first character.

Canvas objects have a *create_image()* method that requires two arguments to specify location and *image=*. Here, the location sets the x,y coordinates on the canvas at which to paint the image.

+   1. Start a new Python program by making GUI methods and attributes available, then create a window object and specify a title

```
```python
from tkinter import *
window = Tk()
window.title(‘Image Example’)
```
```

![](bbox=[0.12, 0.67, 0.23, 0.74])

tk_image.py

![](bbox=[0.12, 0.78, 0.23, 0.84])

python.gif
(200 x 200)