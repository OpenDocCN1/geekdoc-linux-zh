⇒ To display a full-screen backdrop slide show of all the files in the our-hawaii-vacation directory, displaying each image for thirty seconds, and pausing for one minute before repeating all over again, type:

```
$ animate -backdrop -delay 30000x60 our-hawaii-vacation/* [RET]
```

NOTES: As with all ImageMagick tools, CTRL-Q exits.

To make your own animated image files, use convert, which is also part of ImageMagick (see Recipe 18.2 [Converting Image Files], page 432).

# 17.7 Using Other Image Viewers

The following table lists other tools for viewing images.

| Avview | Displays graphics as "ASCII art." This tool can read any image format supported by the pbmplus utility suite, and has fluid zoom in/out, along with all the rendering options you'd expect from a world-class viewer.
DEB: aview
RPM: aview
WWW: http://aa-project.sourceforge.net/aview/ |
| Aatv | Displays television tuner output in any text terminal as ASCII characters.
DEB: aatv
WWW: http://n00n.free.fr/aatv/ |
| ChBg | Changes the X background image. Allows for slide shows and other effects.
DEB: chbg
RPM: chbg
WWW: http://chbg.sourceforge.net/ |
| Fbi | Displays images on Linux framebuffer consoles.
DEB: fbi
RPM: fbi
WWW: http://bytesex.org/fbi/ |