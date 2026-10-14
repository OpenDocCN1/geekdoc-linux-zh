Extracted PhotoCD images are sometimes known to have a kind of "green haze" over them; to remove it, open the image in the GIMP and adjust the color levels with the Auto Levels function. This technique works well for improving any scanned or imported image.

⇒ To remove the green haze from a PhotoCD image, do the following:

+   1. Open the extracted image in the GIMP (see Recipe 18.3 [Using the GIMP], page 434).
+   2. Click through the Image menu to the Colors submenu and then to the Levels submenu, and choose Auto Levels.
+   3. Click OK in the Levels window to accept the changes.

# 19.4 Turning Text into an Image

Sometimes you might like an image file of some text—for example, to use as a header on a Web page. You can always make the text image in an image editor, but there are several other quick and easy ways to go about doing this, such as using convert, or import, or the pnmtext filter, all methods described here. Another tool for making images from plain text is Gozer, mentioned in Recipe 16.5 [Using Other Font Tools], page 403.

# METHOD #1

Enscript
DEB: enscript
RPM: enscript
WWW: http://www.iki.fi/~mtr/genscript/

ImageMagick
DEB: imagemagick
RPM: ImageMagick
WWW: http://www.imagemagick.org/

One way to make an image from some text is to convert the text to PostScript (see Recipe 15.2 [Outputting Text to PostScript], page 359), and then use convert to convert the PostScript to the image format of your choosing, where you can crop and edit it as desired.