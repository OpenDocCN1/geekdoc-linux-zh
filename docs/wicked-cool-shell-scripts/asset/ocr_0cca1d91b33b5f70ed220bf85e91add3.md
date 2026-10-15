# #95 Watermarking Images

If you're looking to protect your images and other content when you post online, you're bound to be disappointed. Anything online is open to copying, no matter if you have a password, use a strong copyright notice, or even add code to your website that tries to inhibit users from saving individual images. The fact is that for a computer to be able to render anything online, it has to use the image buffer on the device, and that buffer can then be duplicated through a screen capture or similar tool.

But all is not lost. You can do two things to protect your online images. One is to only post small image sizes. Look at professional photographers' sites and you'll see what we mean. Usually they share only thumbnails because they want you to buy the larger image file.

Watermarking is another solution, though some artists balk at the work of adding a copyright image or other identifying information directly to the photograph. But with ImageMagick, adding watermarks is easy, even in bulk, as shown in Listing 14-3.

# The Code

```
#!/bin/bash
# watermark --Adds specified text as a watermark on the input image,
#   saving the output as image+wm
wmfile="/tmp/watermark.$$ .png"
fontsize="44"                # Should be a starting arg
trap "$(which rm) -f $wmfile" 0 1 15   # No temp file left behind

if [ $# -ne 2 ] ; then
  echo "Usage: $(basename $0) imagefile \"watermark text\"" >&2
  exit 1
fi

if [ ! -r "$1" ] ; then
  echo "$(basename $0): Can't read input image $1" >&2
  exit 1
fi

# To start, get the dimensions of the image.
● dimensions=$(identify -format "%G" "$1")

# Let's create the temporary watermark overlay.
● convert -size $dimensions xc:none -pointsize $fontsize -gravity south \
  -draw "fill black text 1,1 '$2'" -draw "fill white text 2,2 '$2'" \
  $wmfile

# Now let's composite the overlay and the original file.
● suffix="$(echo $1 | rev | cut -d . -f1 | rev)"
prefix="$(echo $1 | rev | cut -d . -f2- | rev)"
```