them in quotes. display makes thumbnails of the specified images, and displays them in a new window, which it calls a visual image directory.

⇒ Here are two ways to use this.

+   - To browse through the image files that have a .gif extension and are in the /usr/doc/imagemagick/examples directory, type:
+     $ display 'vid:/usr/doc/imagemagick/examples/*.gif' [RET]
+   - To browse through all image files in the current directory, type:
+     $ display 'vid:*' [RET]

In the preceding example, only those files with image formats supported by display are read and displayed.

NOTES: If the title bar indicates that there is more than one page to the visual image directory, press [SPACEBAR] to advance to the next one (pressing [SPACEBAR] on the last page wraps back to the beginning).

To open an image at its normal size, right-click the image and choose Load: the thumbnail will be replaced by its full-size image. To return to the thumbnail directory, press [SPACEBAR].

# 17.1.2 Putting an Image in the Root Window

One way to put an image in the root window (the background behind all other windows) is to use display and give ‘root’ as an argument to the -window option.

⇒ To put the image tetra.jpeg in the root window, type:
$ display -window root tetra.jpeg [RET]

# 17.2 Browsing Images in a Console

Zgv
DEB: zgv
RPM: zgv
WWW: http://freshmeat.net/projects/zgv/

Use zgv to view images in a virtual console (not in X). You can use zgv to browse through the filesystem and select images to view, or you can give the names of specific image files to view as arguments. It recognizes many image formats, including GIF, JPEG, PNG, PBM/PNM/PPM, TGA, and PCX; one of its nicest features is that it fills the entire screen with an image.