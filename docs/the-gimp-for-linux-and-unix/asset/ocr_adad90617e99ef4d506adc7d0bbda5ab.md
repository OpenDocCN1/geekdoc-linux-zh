# Channels

Every GIMP image is made of one or more channels. These channels show the information about the different color elements in an image. As discussed on page 34, RGB color has three channels and CMYK color has four.

Color tuning can be made to an individual channel using the Channels tab page on the Layers & Channels dialog box (Figure 16). But usually adjustments are made using the combined channels, affecting all the channels at once.

Special grayscale channels, called alpha channels, can be added to an image and are used to save a selected area as a mask. (Channels and masks are discussed in detail in Chapter 13, Channels and Layer Masks).

Channels can be added to any type of image, RGB, Indexed, grayscale, or bitmap. An image in the GIMP can have as many channels as you want, though this does considerably the file size.

# Transparency

When working on an image in the GIMP, any area of the image can be transparent, meaning that the pixels contain no color. A transparent area in the GIMP is shown with a light and dark gray checkerboard pattern (Figure 17).

Transparency is a wonderful and important feature when working with layers. Layers are like clear glass windows stacked on one of the other. You can draw on one of these windows, then set whether the layer is visible, semi-transparent, or completely hidden. Transparency is set using a percentage of opacity. The more opaque a layer is, the less transparent it is. For a complete discussion of layers, turn to Chapter 7, A Layer Primer.

![](bbox=[0.073, 0.037, 0.473, 0.317])

Figure 16. Channels show the information about the different color elements in an image. Every image in the GIMP has at least 1 channel. The RGB image whose channels shown here 3 channels.

![](bbox=[0.073, 0.457, 0.473, 0.647])

Figure 17. Transparent areas in an image are shown with a checkerboard pattern.

Transparent area

# How Many Channels are There?

The default number of channels for each image is as follows:

| CHANNELS | MODES |
| --- | --- |
| 1 | Bitmap, Grayscale, Indexed |
| 3 | RGB, HSV |
| 4 | CMYK |

39

CHANNELS: TRANSPARENCY