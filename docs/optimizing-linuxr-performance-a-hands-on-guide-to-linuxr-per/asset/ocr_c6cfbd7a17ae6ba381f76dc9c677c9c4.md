# 10.8. Jump to the Web

Now that we have found GIMP functions are used for much of the time, we have to figure out exactly what these functions are and possibly optimize our time.

First, we search the Web for pixel_rgn_get_pixel and try to determine what it does. After a few false starts, the following link and information revealed in Listing 10.11 confirm our suspicions about what pixel_rgn_get_pixel does.

# Listing 10.11.

```
"There are calls for pixel_rgn_get_pixel, row, col, and rect,
which grab
data from the image and dump it into a buffer that you've
pre-allocated.
And there are set calls to match. Look for "Pixel Regions" in
gimp.h"
(from
http://gimp-plugin-ins.sourceforge.net/doc/Writing/html/sect-image.html )
```

In addition, the information in Listing 10.12 suggests that it is a good idea to avoid using pixel_rgn_get_calls.

# Listing 10.12.

```
"Note that these calls are relatively slow, they can easily be
the slowest thing in your plugin-in. Do not get (or set) pixels one
at a time
using pixel_rgn_[get|set]_pixel if there is any other way.\"
(from
http://www.home-unix.org/simon/gimp/gaud2002/gimp-plugin/html/imagedata.html)"
```

In the Web, we search yield information about the gimp_rgb_set_uchar function by simply turning up the source for the function. As shown in Listing 10.13, this puts back the red, and blue values into a GimpRGB structure that represents a single color.

# Listing 10.13.

```
void
gimp_rgb_set_uchar (GimpRGB *rgb,
guchar r,
guchar g,
guchar b)
{
	g_return_if_fail (rgb != NULL);
n
rgb->r = (double) r / 255.0;
rgb->g = (double) g / 255.0;
rgb->b = (double) b / 255.0;
}
```