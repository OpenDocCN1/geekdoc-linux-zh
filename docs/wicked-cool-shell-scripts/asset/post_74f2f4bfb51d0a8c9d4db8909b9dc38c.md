
```
newfilename="$prefix+wm.$suffix"
① composite -dissolve 75% -gravity south $wmfile "$1" "$newfilename"

echo "Created new watermarked image file $newfilename."

exit 0
```

Listing 14-3: The watermark script

## How It Works

Just about all the confusing code in this script is courtesy of ImageMagick. Yes, it's doing complicated things, but even then, there's something about how it's designed and documented that makes ImageMagick a challenge to work with. Still, don't be tempted to throw out the proverbial baby with the bathwater because the features and functionality of the various ImageMagick tools are amazing and well worth the learning curve.

The first step is to get the dimensions of the image ① so that the watermark overlay will have exactly the same dimensions. Bad things happen if they don't match!

The "%g" produces width × height, which is then given to the convert program as the size of the new canvas to produce. The convert line at ② is one we copied from the ImageMagick documentation because, quite frankly, it's tricky to get just right from scratch. (To learn more about the specifics of the convert -draw parameter language, we encourage you to do a quick online search. Or you can just copy our code!)

The new filename should be the base filename with "+wm" added, and that's what the three lines at ③ accomplish. The rev command reverses its input character by character so that the cut -d . -f1 gets the filename suffix, since we don't know how many dots are going to appear in the filename. Then the suffix is reordered the right way and "+wm" is added.

Finally, we use the composite utility ④ to pull the pieces together and make our watermarked image. You can experiment with different -dissolve values to make the overlay more or less opaque.

## Running the Script

The script takes two arguments: the name of the image to watermark and the text of the watermarking sequence itself. If the watermark will be more than a single word, make sure the entire phrase is in quotes so it transfers properly, as Listing 14-4 shows.

```
$ watermark test.png "(C) 2016 by Dave Taylor"
Created new watermarked image file test+wm.png.
```

Listing 14-4: Running the watermark script

## The Results

The result is shown in Figure 14-1.

![](img/4ffb1cc24a1b24b49254839643abedb2_349_0.png)

Figure 14-1: Image with automatically applied watermark

If you run into an unable to read font error, then you are likely missing the Ghostscript software suite (common on OS X). To remedy this, install Ghostscript with your package manager. For example, use this command to install the brew package manager on OS X:

```
$ brew install ghostscript
```

## Hacking the Script

The font size used for the watermark should be a function of the size of the image. If the image is 280 pixels wide, a 44-point watermark would be too big, but if the image is 3800 pixels wide, 44 points might be too small. Choosing an appropriate font size or text placement can be left to the user by adding it to the script as another parameter.

ImageMagick also knows the fonts on your system, so it would be helpful to allow users to specify a font by name to use as the watermark.

## #96 Framing Images

It's often useful to be able to wrap a border or fancy frame around an image, and ImageMagick has a lot of capabilities in this regard through the convert utility. The problem is, as with the rest of the suite, it's hard to figure out how to use this tool from the ImageMagick documentation.

For example, here’s the explanation of the -frame parameter:

The size portion of the geometry argument indicates the amount of extra width and height that is added to the dimensions of the image. If no offsets are given in the geometry argument, then the border added is a solid color. Offsets x and y, if present, specify that the width and height of the border are partitioned to form an outer bevel of thickness x pixels and an inner bevel of thickness y pixels.

Got it?

Maybe it would be easier to just see an example. In fact, that’s exactly what we’ll do with the usage() function in this script, as shown in Listing 14-5.

## The Code

```
#!/bin/bash
# frameit--Makes it easy to add a graphical frame around
# an image file, using ImageMagick
usage()
{
cat << EOF
Usage: $(basename $0) -b border -c color imagename
or $(basename $0) -f frame -m color imagename
EOF
exit 1
}
```

In the first case, specify border parameters as size x size or percentage x percentage followed by the color desired for the border (RGB or color name).

In the second instance, specify the frame size and offset, followed by the matte color.

```
EXAMPLE USAGE:
$(basename $0) -b 15x15 -c black imagename
$(basename $0) -b 10%x10% -c gray imagename

$(basename $0) -f 10x10+10+0 imagename
$(basename $0) -f 6x6+2+2 -m tomato imagename
```

```
#### MAIN CODE BLOCK
# Most of this is parsing starting arguments!
while getopts "b:c:f:m:" opt; do
case $opt in
```
