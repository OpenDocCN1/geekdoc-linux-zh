# LAYERS, MASKS, AND CHANNELS 693

dialog to move the layers upwards and downwards, change the OPACITY of individual layers, and so on.

> No matter layers are displayed: all processing commands only to the currently active layer – even if it is momentarily invisible. You will inevitably change visibility of layers, and then nevertheless work on a still active. invisible layer. Therefore, please check that the correct layer is highlighted.

> Selections are independent from layers. You may select something on one layer, then activate a different layer, and continue to use the selection there.

# (Renaming layers

All you need to give a new name is a double click on the layer in the LAYERS dialog. (In this way, you can also turn a floating selection into a normal layer – simply give it a new name.)

# Combining layers

Three commands are available for combining layers into a new one. ANCHOR unites a floating selection with the last active layer. MERGE VISIBLE LAYERS combines all visible layers (that is, all layers for the eye icon is shown). FLATTEN IMAGE all layers (no matter whether they are or not).

> You should always store the image in the XCF backup file before you combine the layers. More often than not, you may no longer modify an image you thought had been completed. If at that point you no longer have any layer information left, many changes become practically impossible.

# Transparency (Keep Trans.)

The KEEP TRANS. option always refers to the currently active layer. It specifies whether pair or filter operations are restricted to the visible part of the layer. This is very useful in many cases. If, for example, a layer only contains a text, and you wish to change the color of this text, the option must be activated. If, instead, you wish to insert further text, patterns, and so on, in this layer, you must switch the option off. (If your changes are ignored, one possible cause is an incorrect setting of the KEEP TRANS. option, option.)

> The transparent part of a layer or a whole image is represented by a gray chessboard pattern. Both the shadescale and the size of the chessboard pattern can be set in the FILE | PREFERENCES dialog.

In the FILE | PREFERENCES dialog, you can also change the size of the layer preview icon displayed in the LAYERS dialog.