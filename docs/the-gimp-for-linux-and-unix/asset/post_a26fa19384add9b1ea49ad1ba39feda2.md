
## Color and the GIMP

### HSV Model

The Hue, Saturation, Value (HSV) model is used in combination with the RGB model in the GIMP. Hue represents the color—green, pink, orange, etc. Saturation refers to the intensity of the color and is measured as a percentage: at 100% saturation the color appears as the full color, whereas with 10% saturation the color appears washed out. Value is the intensity of light on the color. This component is also expressed as a percentage. A value of 100% is white and of 0% is black. The color in use appears true at a value of 50%. HSV has three channels.

![](img/5164bc49fb24f10213e18cc994b7b40c_50_0.png)

**Figure 4.** This image is set in Indexed color mode. Using the custom palettes, you can create interesting color effects.

## Indexed Mode

Indexed mode sets a specific number of colors used in an image from 1 to 256. Indexed color has one channel (**Figure 4**).

The GIMP comes with many custom color palettes that can be used with an indexed color image to create interesting effects. There are palettes that contain only desert types and browns or sunset hues. There's even a B Palette that contains the 216 colors displayed in a browser. For more details about using color palettes, turn to page 47. To learn more about creating images for the Web, take a look at Chapter 17, Creating Images for the Web.

![](img/5164bc49fb24f10213e18cc994b7b40c_50_1.png)

**Figure 5.** This image is set in grayscale mode.

## Grayscale Mode

An image set in grayscale mode contains no color, only varying shades of gray. There are 256 shades of gray from black (0) to white (255). The median shade of gray on the grayscale spectrum is set at a value of 128. Grayscale has one channel (**Figure 5**).

![](img/5164bc49fb24f10213e18cc994b7b40c_50_2.png)

## Bitmap Mode

Bitmap mode is the simplest of all. It contains only black or white pixels—no color or shades of gray (**Figure 6**).

**Figure 6.** This image is set in bitmap mode. Notice that there are only black and white areas, no gray.

## Chapter 3

### Image Modes

Any GIMP image can be displayed in, edited in, and converted to any one of four image modes: bitmap, grayscale, indexed, or RGB.

### To convert an image to a bitmap:

- 1. Open the image you want to convert (Figure 7).
- 2. Right-click on the image and choose Image→Indexed from the pop-up menu (Figure 8). The Indexed Color Conversion dialog box will open (Figure 9).
- 3. Select the black/white (1-bit) palette radio button in the Palette Options area (Figure 10).
- 4. Click OK. The Indexed Color Conversion dialog box will open, and the image will convert to a bitmap (Figure 11).

![](img/5164bc49fb24f10213e18cc994b7b40c_51_0.png)

CONVERT IMAGE TO BITMAP OR INDEXED MODE

### To convert an image to indexed mode:

- 1. Open the image you want to convert (Figure 7).
- 2. Right-click on the image and choose Image→Indexed from the pop-up menu (Figure 8). The Indexed Color Conversion dialog box will open (Figure 9).

![](img/5164bc49fb24f10213e18cc994b7b40c_51_1.png)
![](img/5164bc49fb24f10213e18cc994b7b40c_51_2.png)

Palette Options

| Generate optimal palette: | # of colors: |
| --- | --- |
| | 256 |

Figure 10. Select the Use black/white (1-bit) palette radio button, then click OK.

Use WWW-optimised palette

| Use custom palette | Default |
| --- | --- |

Use black/white (1-bit) palette |

Dither Options

| Enable Floyd-Steinberg dithering |
| --- |
| OK | Cancel |

36

## Color and the GIMP

Figure 11. This is the same image shown in Figure 7, but it has been converted to bitmap.

3. In the Palette Options area, select a radio button next to one of the following:

- Generate optimal palette up to 256 colors creates a palette of the colors currently present in the image. By default, 255 is entered in the # of colors text box. If you want to create a palette with fewer colors than this, type the number in the text box. (For Web images, the fewer colors the better since file size smaller.)

![](img/5164bc49fb24f10213e18cc994b7b40c_52_0.png)

- Use WWW-optimised palette automatically changes the colors in the image to the closest matches available in the Web palette. The Web palette contains the 256 colors best displayed by Netscape Navigator.

- Use custom palette automatically changes the colors in the image to the closest matches available in the selected palette displayed on the drop-down list button. To select a different button, click the button and choose a palette from the drop-down list (Figure 12).

![](img/5164bc49fb24f10213e18cc994b7b40c_52_1.png)

Figure 12. Select the Custom palette radio button in the Palette Options area, then choose a custom palette from the drop-down list.

4. Click OK. The Indexed Color Conversion dialog box will close and the image will change (sometimes very noticeably) according to your selection (Figure 13).

Figure 13. This is the same image shown in Figure 7, but it has been converted to indexed color mode.

### Tip

- You can create custom palettes, as well as edit existing palette colors, and create new colors. For directions on how to do this, turn to pages 47–51.

![](img/5164bc49fb24f10213e18cc994b7b40c_52_2.png)

37

## Chapter 3

### Image Modes

### To convert an image to a bitmap

- 1. Open the image you want to convert (Figure 7).
- 2. Right-click on the image and choose Image→Indexed from the pop-up menu (Figure 8). The Indexed Color Conversion dialog box will open (Figure 9).
- 3. In the Palette Options area, select a radio button next to one of the following:
    - Generate optimal palette up to 256 colors creates a palette of the colors currently present in the image. By default, 255 is entered in the # of colors text box. If you want to create a palette with fewer colors than this, type the number in the text box. (For Web images, the fewer colors the better since file size smaller.)
    - Use WWW-optimised palette automatically changes the colors in the image to the closest matches available in the Web palette. The Web palette contains the 256 colors best displayed by Netscape Navigator.
    - Use custom palette automatically changes the colors in the image to the closest matches available in the selected palette displayed on the drop-down list button. To select a different button, click the button and choose a palette from the drop-down list (Figure 12).
- 4. Click OK. The Indexed Color Conversion dialog box will close and the image will change (sometimes very noticeably) according to your selection (Figure 13).

### Tip

- You can create custom palettes, as well as edit existing palette colors, and create new colors. For directions on how to do this, turn to pages 47–51.

### To convert an image to indexed mode

- 1. Open the image you want to convert (Figure 7).
- 2. Right-click on the image and choose Image→Indexed from the pop-up menu (Figure 8). The Indexed Color Conversion dialog box will open (Figure 9).
- 3. In the Palette Options area, select a radio button next to one of the following:
    - Generate optimal palette up to 256 colors creates a palette of the colors currently present in the image. By default, 255 is entered in the # of colors text box. If you want to create a palette with fewer colors than this, type the number in the text box. (For Web images, the fewer colors the better since file size smaller.)
    - Use WWW-optimised palette automatically changes the colors in the image to the closest matches available in the Web palette. The Web palette contains the 256 colors best displayed by Netscape Navigator.
    - Use custom palette automatically changes the colors in the image to the closest matches available in the selected palette displayed on the drop-down list button. To select a different button, click the button and choose a palette from the drop-down list (Figure 12).
- 4. Click OK. The Indexed Color Conversion dialog box will close and the image will change (sometimes very noticeably) according to your selection (Figure 13).

## Channels

Every GIMP image is made of one or more channels. These channels show the information about the color elements in an image. As discussed on page 34, RGB color has three channels and CMYK has four.

Color tuning can be made to an individual channel using the Channels tab on the Layers Channels box (Figure 16). But usually adjustments are made using the combined channels, affecting all channels at once.

Special grayscale channels, called alpha channels, can be added to an image and are used to save a selected area as a mask. (Channels and masks are discussed in detail in Chapter 13).

## Transparency

When working on an image in the GIMP, any area of the image can be transparent, meaning that the pixels contain no color. A transparent area in the GIMP is shown with a light and dark gray checkerboard pattern (Figure 17).

Transparency is a wonderful and important feature when working with layers. Layers are like glass windows stacked on one of the other. You can draw on one of these windows, then set whether the layer is visible, semi-transparent, or completely hidden. Transparency is set using a percentage of opacity. The more opaque a layer is, the less transparent it is. For a complete discussion of layers, turn to Chapter 7, A Layer Primer.
