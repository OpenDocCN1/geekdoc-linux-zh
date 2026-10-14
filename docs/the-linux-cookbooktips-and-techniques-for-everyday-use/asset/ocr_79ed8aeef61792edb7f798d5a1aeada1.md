# 18.4 Viewing an Image in a Web Browser

If you have a graphical Web browser, such as `mozilla`, you can use it to view a graphic image. While viewing images in a browser doesn't offer much flexibility (you can't zoom in on a portion of the image, or get information about the image resolution and other details), if you simply want to quickly view an image file while you are in X, and you have a Web browser running, it can be a quick and easy way to do it.

To view an image file in a Web browser, specify a [file:](#) URL pointing to the file name of the image in the `Location` field of the browser.

+   To view the file `/usr/share/images/mondrian-15.jpeg`, type:

```
file:/usr/share/images/mondrian-15.jpeg RET
```

Notice that the given [file:](#) URL only has one preceding slash, pointing to the root directory, and not two, as in [http://](#).

[<] [>] [<<] [Up] [>>] [Top] [Contents] [Index] [?]

# 18.5 Browsing PhotoCD Archives

```
@sf(Debian): `xpcd'
@sf(Debian): `xpcd-gimp'
@sf(www): http://user.cs.tu-berlin.de/~kraxel/linux/xpcd/
```

The xpcd tool is an X client for viewing and browsing collections of Kodak PhotoCD images. To browse the images on a Kodak PhotoCD, mount the CD-ROM (see section [Mounting a CD-ROM](#)), and then give the mount point as an argument to xpcd.

+   To browse the images on the PhotoCD disc mounted on `/cdrom`, type:

```
$ xpcd /cdrom RET
```

The preceding example will open two new windows—a small xpcd command bar window, and a larger window containing thumbnails of all PhotoCD images on the disc.

To open a copy of an image in a new window, left-click its thumbnail image. When you do, xpcd will open the image at the second-smallest PhotoCD resolution, 256x384; to view it at another size, right-click the image and choose the size to view. Once the new window is drawn, you can right-click on this new image to save it as a JPEG, PPM, or TIFF format image.

To view an individual `.pcd` file with xpcd, give the name of the file as an argument.