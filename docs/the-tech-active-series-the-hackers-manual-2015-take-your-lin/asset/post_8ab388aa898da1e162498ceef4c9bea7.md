
## Hacks

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_136_0.png)

```
pdb.gimp_context_set_brush_size(128)
pdb.gimp_context_set_default_colors()
(160,100)
```

If you have the brush called ‘Cell 01’ available, then the above code will draw a green splodge in the middle of your canvas. If you don’t, then you’ll get an error message. You can get a list of all the brushes available to you by calling **pdb.gimp_brushes_get_list()**. The paintbrush tool is more suited to these fancy brushes than the hard-edged pencil, and if you look in the procedure browser at the function **gimp_paintbrush**, you will see that you can configure gradients and fades too. For simplicity, we have just used the defaults/current settings here. On the disc you will find a file *lines/blob.py* which will register a fully-fledged Gimp plugin, replete with a few tweaks.

For the rest of the tutorial we will describe a slightly more advanced plugin for creating bokeh effects in your own pictures. ‘Bokeh’ derives from a Japanese word meaning blur or haze, and in photography refers to the out-of-focus effects caused by light sources outside of the depth of field. It often results in uniformly coloured, blurred, disc-shaped artefacts in the highlights of the image, reminiscent of lens flare. The effect you get in each case is a characteristic of the lens

and the aperture – depending on design, one may also see polygonal and doughnut-shaped bokeh effects. For this exercise, we'll stick with just circular ones.

Our plugin will have the user pinpoint light sources using a path on their image, which we will assume to be single-layered. They will specify disc diameter, blur radius, and hue and saturation adjustments. The result will be two new layers: a transparent top layer containing the ‘bokeh discs’, and a

> “Our plugin creates a layer with ‘bokeh discs’ and another with a blurred copy of the image”

layer with a blurred copy of the original image. The original layer remains untouched beneath these two. By adjusting the opacities of these two new layers, a more pleasing result may be achieved. For more realistic bokeh effects, a part of the image should remain in focus and be free of discs, so it may be fruitful to erase parts of the blurred layer. Provided the user doesn’t rename layers, then further applications of our

- Applying our bokeh plugin has created a pleasing bokeh effect in the highlights.

plugin will not burden them with further layers. This means that one can apply the function many times with different parameters and still have all the flare-effect discs on the same layer. It is recommended to turn the blur parameter to zero after the first iteration, since otherwise the user would just be blurring the already blurred layer.

After initialising a few de rigueur variables, we set about making our two new layers. For our blur layer, we copy our original image and add a transparency channel. The bokeh layer is created much as in the previous example.

```
blur_layer = pdb.gimp_layer_copy(timg, timg[0],1)
pdb.gimp_image_insert_layer(timg, blur_layer, None, 0)
bokeh_layer = pdb.gimp_layer_new(timg, width, height, RGBA_IMAGE, "bokeh", 100, NORMAL_MODE)
pdb.gimp_image_insert_layer(timg, bokeh_layer, None, 0)
```

Our script’s next task of note is to extract a list of points from the user’s chosen path. This is slightly non-trivial since a general path could be quite a complicated object, with curves and changes of direction and allsorts. Details are in the box below, but don’t worry – all you need to understand is that the main for loop will proceed along the path in the order

drawn, extracting the coordinates of each component point as two variables x and y.

Having extracted the point information, our next challenge is to get the local colour of the image there. The PDB function for doing just that is called gimp_image_pick_color(). It has a number of options, mirroring the dialog for the Colour Picker tool. Our particular call has the program sample within a 10-pixel radius of the point x,y and select the average colour. This is preferable to just selecting the colour at that single pixel, since it may not be indicative of its surroundings.

### Bring a bucket

To draw our appropriately-coloured disc on the bokeh layer, we start – somewhat counter-intuitively – by drawing a black disc. Rather than use the paintbrush tool, which would rely on all possible users having consistent brush sets, we will make our circle by bucket filling a circular selection. The selection is achieved like so:

```
pdb.gimp_image_select_ellipse(timg, CHANNEL_OP_REPLACE, x - radius, y - radius, diameter, diameter)
```

There are a few constants that refer to various Gimp-specific

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_137_0.png)

> Quick tip
> For many, many more home-brewed plugins, check out the Gimp Plugin Registry at http://registry.gimp.org

Here are our discs. If you’re feeling crazy you could add blends or gradients, but uniform colour works just fine.

### Paths, vectors, strokes, points, images and drawables

Paths are stored in an object called vectors. More specifically, the object contains a series of strokes, each describing a section of the path. We’ll assume a simple path without any curves, so there is only a single stroke from which to wrest our coveted points. In the code we refer to this stroke as gpoints, which is really a tuple that has a list of points as its third entry. Since Python lists start at 0, the list of points is accessed as gpoints[2]. This list takes the form [x0,y0,x0,y0,x1,y1,x1,y1...]. Each point is counted

twice, because in other settings the list needs to hold curvature information. To avoid repetition, we use the range() function’s step parameter to increment by 4 on each iteration, so that we get the xs in positions 0, 4, 8 and the ys in positions 1, 5, 9. The length of the list of points is bequeathed to us in the second entry of gpoints for i in range(0,gpoints[1],4):

You will see a number of references to variables timg and tdraw. These represent the active image and layer (more correctly image and drawable) at the time our function was called. As you can imagine, they are quite handy things to have around because so many tools require at least an image and a layer to work on. So handy, in fact, that when we come to register our script in Gimp, we don’t need to mention them – it is assumed that what you want to pass them to your function. Layers and channels make up the class called drawables – the abstraction is warranted here since there is much that can be applied equally well to both.
