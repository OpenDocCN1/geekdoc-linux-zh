
## OPTIONS (CONT.)

| Use This Option | To Do This |
| :--- | :--- |
| `-compose` _type_ | **out**: Source image 2 with the shape of source image 1 cut out.<br>**over**: The union of the two images.<br>**plus**: The sum of the image data.<br>**replace**: Source image 1 replaced by source image 2.<br>**subtract**: Source image 2 minus source image 1 with underflow wrapping.<br>**xor**: Shows only the image data that is outside the overlap region. Overlap areas are blank. |
| `-compress` _type_ | Set the type of compression. The options are None, BZip, Fax, Group4, JPEG, LZW, RunlengthEncoded, or Zip. |
| `-density` _width x height_ | Set the vertical and horizontal resolution in pixels. |
| `-displace` _horizontal scale x vertical scale_ | Shift image pixels as defined by a displacement map. |
| `-dispose` _type_ | Use the specified type of GIF disposal. The options are:<br>0 No disposal.<br>1 Do not dispose between frames.<br>2 Overwrite frame with background color.<br>3 Overwrite with previous frame. |
| `-dither` | Apply Floyd/Steinberg error diffusion to the image. |
| `-font` _font_ | Set the font for normal text. |
| `-geometry` _width x height [% \| !]_ | Set the width and height of the image in pixels. Append a percentage sign to adjust the width and height by percentage. Append an exclamation point to force the exact size. |
| `-gravity` _type_ | Set the direction to which the image gravitates. The options are NorthWest, North, NorthEast, West, Center, East, SouthWest, South, SouthEast. |
| `-interlace` _type_ | Set the type of interlacing scheme. The options are None, Line, Plane, or Partition. |
| `-label` "string" | Use the string as a label. Be sure to surround the string with double quotes. |
| `-matte` | Store the matte channel information if the image has one. |
| `-monochrome` | Transform the image to black and white. |
| `-negate` | Replace every pixel with its complementary color. |
| `-page` _width x height [% \| !]_ | Set the width and height of the image canvas in pixels. Append a percentage sign to adjust the width and height by percentage. Append an exclamation point to force the exact size. For PostScript pages, the available widths and heights correspond to page sizes, as follows. |

### Page Sizes

| Page Size | Width | Height |
| :--- | :--- | :--- |
| 11x17 | 792 | 1224 |
| A0 | 2380 | 3368 |
| A1 | 1684 | 2380 |
| A2 | 1190 | 1684 |
| A3 | 842 | 1190 |
| A4 | 595 | 842 |
| A4Small | 595 | 842 |
| A5 | 421 | 595 |
| A6 | 297 | 421 |
| A7 | 210 | 297 |
| A8 | 148 | 210 |
| A9 | 105 | 148 |
| A10 | 74 | 105 |
| ArchA | 648 | 864 |
| ArchB | 864 | 1296 |
| ArchC | 1296 | 1728 |
| ArchD | 1728 | 2592 |
| ArchE | 2592 | 3456 |
| B0 | 2836 | 4008 |
| B1 | 2004 | 2836 |
| B2 | 1418 | 2004 |
| B3 | 1002 | 1418 |
| B4 | 709 | 1002 |
| B5 | 501 | 709 |
| C0 | 2600 | 3677 |
| C1 | 1837 | 2600 |
| C2 | 1298 | 1837 |
| C3 | 918 | 1298 |
| C4 | 649 | 918 |
| C5 | 459 | 649 |
| C6 | 323 | 459 |
| F1sa | 612 | 936 |
| F1se | 612 | 936 |
| HalfLetter | 396 | 612 |
| Ledge | 1224 | 792 |
| Legal | 612 | 1008 |
| Letter | 612 | 792 |
| LetterSmall | 612 | 792 |

| Use This Option | To Do This |
| :--- | :--- |
| `-quality` _value_ | Set the JPEG, MIFF or PNG compression level. |
| `-size` _width x height [% \| !]_ | Set the width and height of RAW images with unknown dimensions. Append a percentage sign to adjust the width and height by percentage. Append an exclamation point to force the exact size. |
| `-stegano` | Hide a watermark in the image. |
| `-stereo` | Combine two images to create a stereo anaglyph. |
| `-tile` | Repeat a composite operation across the image. |
| `-treedepth` 0 \| 1 | Set a tree depth of 0 or 1. You must also use the `-colors` option. |
| `-verbose` | Display all messages. |

## EXAMPLE

- **This Command**
  
  Combines `compose bumpmap image1.jpg image2.jpg combined.jpg`

- **Does the Following**
  
  Combines the specified input files (`image1.jpg` and `image2.jpg`) into a composite image (`combined.jpg`) in which `image1.jpg` transparently shades `image2.jpg`.

## convert

`convert [ option ] input file output file`

Converts the specified input file (a graphic file) into the specified output file. This utility automatically recognizes a wide variety of image formats. To specify the format of the converted file, append a recognized suffix to the output filename (such as `.jpg` or `.bmp`). This utility is part of the ImageMagick package, which is downloadable from `http://www.imagemagick.org`.

*See also combine, identify, montage.*

### OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| `despeckle` | Reduce speckles in the image. |
| `–dispose` _type_ | Use the specified type of GIF disposal. The options are:<br>0 No disposal.<br>1 Do not dispose between frames.<br>2 Overwrite frame with background color.<br>3 Overwrite with previous frame. |
| `–dither` | Apply Floyd/Steinberg error diffusion to the image. |
| `–draw` _string_ | Annotate an image with one or more graphic primitives. The primitives include the following: circle, color, ellipse, fillCircle, fillEllipse, fillPolygon, fillRectangle, image, line, matte, point, polygon, rectangle, and text. |
| `–edge` _factor_ | Detect edges in an image using the specified enhancement factor (a percentage). |
| `–enhance` | Enhance a noisy image. |
| `–equalize` | Perform histogram equalization. |
| `-filter` _type_ | Use the specified filter type when resizing the image with `-geometry`. The following filters are available: Bessel, Blackman, Box, Catrom, Cubic, Gaussian, Hamming, Hanning, Hermite, Lanczos (the default), Mitchell, Point, Quadratic, Sinc, Triangle. |
| `-flip` | Create a mirror image by reversing scan lines vertically. |
| `-flop` | Create a mirror image by reversing scan lines horizontally. |
| `-font` _font_ | Set the font for normal text. |
| `-frame` _width x height + outer-bevel width + inner-bevel width_ | Use an ornamental border with the specified width, height, outer-bevel width, and inner-bevel width. |
| `-fuzz` _distance_ | Combine colors in the specified distance. |
| `-gamma` _n_ | Use the specified level (n) of gamma correction, where n is a level from 0.8 to 2.3. |
| `-geometry` _width x height [% \| !]_ | Create the image with the specified maximum width and height while maintaining the original image's aspect ratio. Append `%` (a percentage sign) to adjust the width and height by a percentage. To force the dimensions you specify, append `!` (an exclamation point). |
| `-gravity` _type_ | Set the direction to which the image gravitates. The options are NorthWest, North, NorthEast, West, Center, East, SouthWest, South, SouthEast. |
| `-implode` _factor_ | Implose image pixels about the center by the specified factor. The options are implosion (0-99.9%) or explosion (-99.9-0%). |
| `-interlace` _type_ | Set the type of interlacing scheme. The options are None, Line, Plane, or Partition. |
| `--label` "string" | Use the specified string as a label. Be sure to surround the string with double quotation marks. |
| `--layer` _type_ | Set the type of layer. The options are Red, Green, Blue, or Matte. |
| `--linewidth` _n_ | Set the width of a line to _n_ pixels. |
| `--loop` _n_ | Repeat the GIF animation _n_ times. Specify 0 to loop forever. |
| `--map` _filename_ | Obtain the color set from the specified filename. |
| `--matte` | Store the matte channel information if the image has one. |
| `--modulate` _brightness, saturation, hue_ | Vary the brightness, saturation, and hue by specifying percentage increases or decreases. Omit the percentage sign. |
| `--monochrome` | Transform the image to black and white. |
| `--morph` _image sequence_ | Morph the image sequence. |
| `--negate` | Replace every pixel with its complementary color. |
| `--noise` _type_ | Add or reduce noise using the specified filter type. The options are Uniform, Gaussian, Multiplicative, Impulse, Laplacian, and Poisson. |
| `--normalize` | Transform the image and enhance the contrast by spanning the full range of color values. |
| `--opaque` _color_ | Use the specified color for the pen (see `--pen`). |
| `--page` _width x height [% \| !]_ | Set the width and height in pixels of the image canvas. Append a percentage sign to adjust the width and height by percentage. Append an exclamation point to force the exact size. For PostScript pages, the available widths and heights correspond to page sizes as follows: |

### Page Sizes (Continued)

| Page Size | Width | Height |
| :--- | :--- | :--- |
| 11x17 | 792 | 1224 |
| A0 | 2380 | 3368 |
| A1 | 1684 | 2380 |
| A2 | 1190 | 1684 |
