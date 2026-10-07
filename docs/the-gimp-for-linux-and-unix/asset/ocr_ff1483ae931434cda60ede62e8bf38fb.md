# CHANNELS
AND LAYER MASKS

Every image you create in the GIMP contains channels. These channels store an image's color information. The number of channels in an image depends on the color mode which the image is set. For instance, an image set in RGB mode has three default channels—a Red channel that stores red information, a Green channel that stores green information, and a Blue channel that stores blue information. If an image has more than one layer, each layer has its own set of channels.

Alpha channels are grayscale channels that you can add to an image. They are used to protect selections. Alpha channel selections are used to protect specific areas of an image from editing while changes, such as recoloring, filters, and other effects, are applied to the rest of the (unmasked, i.e., unselected) image.

Layer masks in the GIMP work in much the same way as a Halloween mask works on one's face. A Halloween mask covers the face, concealing it; but any cutouts—for eyes or mouth, for instance—leave those areas visible. Layer masks are placed on top of an image and “cutouts” are added, making those areas visible.

Layer masks control how different areas of an image are revealed. You can use layer masks as test areas for applying special effects without permanently changing an image. If you like the effects and want to make them permanent, you can then apply a mask to an image. Layer masks can be saved with a layered image in the GIMP's native .xcf file format.