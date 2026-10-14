The Linux Cookbook: Tips and Techniques for Everyday Use:

+   - To view the PhotoCD file `driveby-001.pcd`, type:

```
```shell
$ xpcd driveby-001.pcd RET
```
```

> **NOTE:** You can also use `display` to view a `.pcd` PhotoCD image file (see section [Viewing an Image in X](#)).

See [Extracting PhotoCD images](#) for another recipe for extracting PhotoCD images.

# 18.6 Additional Image Viewers

The following table lists other tools for viewing images.

| TOOL | DESCRIPTION |
|---|---|
| `animate` | Part of the ImageMagick suite; use animate to display an animated slide-show sequence of images in X. On Debian: `imagemagick`; [ftp://ftp.wizards.dupont.com/pub/ImageMagick/](#) |
| `xwud` | Displays files in the special X Window Dump file format, as created by xwd. On Debian: `xbase-clients`; [http://www.xfree86.org/](#) |
| `showpicture` | Views an image sent as an email attachment; requires xloadimage. On Debian: `metamail`; [ftp://ftp.bellcore.com/pub/mb/](#) |
| `xli` | Basic image viewer for X. On Debian: `xli` |
| `xloadimage` | Nice graphics viewer for X that contains tools for viewing images in the root window. On Debian: `xloadimage` |
| `aview` | View graphics as “ASCII art.” This tool can view any image format supported by the pbmplus utility suite, and has fluid zoom in/out and all the rendering options you'd expect from a world-class viewer. On Debian: `aview`; [http://ftp.ta.jcu.cz/pub/aa](#) |