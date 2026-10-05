
# TEXT 679

- The character weight is bold. (Other alternative would be normal, medium, black, extrabol etc.).
- The slant is o (oblique, that is, inclined). (Other options are r (roman, that is, upright), or i (italic).
- The width of the character set is not specified. (Some character sets use condensed, extended, and other widths.)
- The character size is 10 points.
- The spacing type is p (proportional). (Other alternatives are e or m for character or monospaced. Both mean all characters of that font have equal width: an example for this the Courier font.)
- The characters are coded according to Iso-Latin 1. (This coding covers all characters of the Western European language area.)

You can see from the above list that X provides more possibilities for describing character sets than, for example, Windows. (It may be the case that you have installed two Courier typefaces produced by different manufacturers. These type also look different; you may decide to use the one that pleases you.)

However, this multitude makes dialog somewhat laborious than one would wish. When you are looking for a suitable typeface, you should enter some characters in the text field at the bottom. Then you choose the desired size. Finally, you select the required typeface and, if necessary, changing the remaining options. The * setting means Gimp selects the first variation in alphabetical order.

> Tip: Character sets are shown by default in italics. Just set SLANT to r to obtain the upright variation.

After changing the type set, you need to press the Tab key to Gimp accept the change. Please note that under X character sets are only available in a series of predefined sets (typically 10, 11, 12, 14, 17, 18, 20, 24, 25, and 34 points). Such character sets can also be represented in all other sizes, but will look rather ugly.

> Tip: For representation of text, Gimp resorts to the character sets provided by the X Window System. Basic information and tips for the installation of additional character sets can be found on page 250. If you have installed the common fonts and no font server, at least the charter, courier, and utopia typefaces should be available in all sizes and in a reasonable quality.

# Antialiasing, border

Two Gimp-specific settings of the text dialog tell an explanation: ANTIALIASING AND BORDER. The ANTIALIASING option causes the borders of the inserted text to be displayed in grayscales or colored tints. On screen, this makes the text look sharper and less pixely. This option should only be deactivated if you use very small character sizes and later want to print the resulting image.

# GIMP - THE PHOTOSHOP ALTERNATIVE

![](img/b30873dd3d753687a59253fb9ad26a0b_707_0.png)

Figure 20.12 Gimp font selection.

If you specify a numeric value in the BORDER field, border of the floating selection that surrounds the text is enlarged by this number of pixels. There are two reasons for this: without this option, text is cut off in some fonts (for example the first italicized letter, or descenders as in the letter g). Second, this makes it possible to enlarge the selected part of the floating selection in further processing steps. (The border of the floating selection can also be enlarged at a later stage with the aid of the LAYERS dialog.)

# 20.6 Selections

Application of paint tools to the entire image is an exception. Usually, most operations are to be applied only to well-defined parts of the image. The problem is now to select the required part of the image as precisely as possible. (This is particularly difficult in a photograph if, for example, a person or an object is to be separated from the background.)

The selected area is marked by a flashing border. (In the GUM, this border is called marching ants, for obvious reasons.) Before we really start, here are some indispensable keyboard shortcuts:

Processing selections

- Ctrl+T toggles between showing and hiding the flashing selection border; the selection itself is preserved
- Ctrl+I inverts the selection, that is, everything that was outside is now inside
- Ctrl+A selects the whole image
- Shift+Ctrl+A deselects the selection.

# SELECTIONS 681

There are two types of selection, normal ones and so-called floating selections. The difference is described on page 686. Just a brief remark in advance: some paint tools work differently depending on the type of selection. Thus, for example, in a normal selection BUCKET FILL no longer considers the pixel color of the affected area, but fills the selection with a pattern or color. Only in a floating selection does the tool work again as described on page 673.

Selections (with the exception of floating selections) can be permanently saved and later restored by means of SELECT | SAVE TO CHANNEL. Handling of channels is, however, only described on page 691. Channels are often an alternative to selections.

# Rectangular and elliptical selections

Rectangular, elliptical, and circular selections are drawn with the RECTANGULAR (R) and ELLIPTICAL SELECT (E) tools and the mouse. During the selection, the following keys can be pressed in addition to the left mouse button:

# Influencing selection shapes

- Shift constrain selection to square or circle
- Ctrl starting point is not a corner, but the center
- Shift+Ctrl square/circle around the center point

To make selections surround an object as closely as possible, you should draw guides beforehand. If you want to select the border of a rectangle or ellipse, you can either subtract two objects from another (see below) or use SELECT | BORDER (page 686).

# Combining selections

Sometimes you may wish to combine several parts – for example, a circle and two rectangles. Maybe you would also wish to cut out a part of this. If a selection already exists, the Shift and Ctrl keys have the following meaning at the beginning of:

- Shift add to selection
- Ctrl subtract from selection
- Shift+Ctrl intersection of selection

Maybe this looks to you as a contradiction of the previous table which described the meaning of Shift and Ctrl. However, the only thing that counts is the moment at which Shift and Ctrl are pressed!

If, for example, you want to produce the selection shown in 20.13, you select the rectangle. Then you press E, move the mouse to the center of the rectangle, press Ctrl (subtraction), and begin the selection. While you are drawing the ellipse, you additionally press Shift (The key combination Shift+Ctrl now causes selection around the starting point.) The change of Shift+Ctrl during the selection, that is, while the left mouse button is depressed, requires some practice, but then works out right.

![](img/b30873dd3d753687a59253fb9ad26a0b_709_0.png)

Figure 20.13 Combining selections.

> To reiterate, another survival rule: if you want to abort an already started selection, you keep the left mouse button depressed and, in addition, press the right mouse button. Then you first release the left mouse button, followed by the right mouse button. Some hours of exercise with Gimp – and you have the dexterity of a pianist!

# Lasso (Free / Shape Selection)

With the lasso function (FREE SELECTION, F), you simply select the area surrounding it with the mouse with button kept depressed. (If the area is not entirely enclosed, Gimp joins the start and end points with a line.)

The SHAPE SELECTION (S) function goes one step further as FREE SELECTION, you draw the shape with the mouse. Gimp subsequently tries to improve the selection on the basis of the image contents. (For this reason, the tool is also INTEIGENT SCISSORS.) Several experiments with this function have, however, been deceptive: in none of the cases, Gimp was able to guess what should really have been selected. The numerous slide rulers of the corresponding dialog cannot change the selection a posteriori, which makes experimenting largely impossible. The most attractive alternative seems to be the possibility of subsequently
