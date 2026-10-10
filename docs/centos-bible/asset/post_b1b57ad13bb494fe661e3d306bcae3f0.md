
# Xine Tips

Getting video and audio to work properly can sometimes be a tricky business. Here are a few quick tips to using Xine:

- **Xine Won't Start** — To work best, Xine needs an X driver that supports xvid. If there is no xvid support for your video card in X, Xine will shut down immediately when it tries to open the default Xv driver. If this happens to you, try starting the xine command with the X11 video driver (which is slower, but should work) as follows:

```bash
$ xine -v XShm
```

- **Don't Run as root** — Run xine as a regular user, instead of as root. Once Xine is installed, you should be able to run it from the Applications menu on your panel by selecting Sound & Video ► Xine Media Player. There have been recently discovered vulnerabilities of some Open Source media players related to streaming media. Although that problem was fixed, it again highlighted the fact that running applications as a regular user, whenever possible, is a good idea.

- **Run xine-check** — To get an idea of how happy Xine is running on your system, run the xine-check command (as the user who will be using Xine). It will tell you if there are problems running Xine on your current operating system, kernel, and processor, among other things.

- **Xine Playback Is Choppy** — If playback of files from your hard disk is choppy, there are a couple of settings you can check: 32-bit I/O and DMA. If these two features are supported by your hard disk, they will generally improve hard disk performance.

> **CAUTION:** Improper disk settings can result in destroyed data on your hard disk. Do this procedure at your own risk. This procedure is only for IDE hard drives (not SCSI)! Also, be sure to have a current backup and no activity on your hard disk if you change DMA or I/O settings as described here.

1. First, test the speed of hard disk reads. To test the first IDE drive, type:

```bash
# hdparm -t /dev/sda
Timing buffered disk reads: 64 MB in 19.31 seconds = 3.31 MB/sec
```

2. To see your current DMA and IO settings, as root user type:

```bash
# hdparm -c -d /dev/sda
/dev/sda:
  1/0 support  = 0 (default 16-bit)
  using_dma    = 0 (off)
```

3. This shows that both 32-bit IO and DMA are off. To turn them on, type:

```bash
# hdparm -c 1 -d 1 /dev/sda
/dev/sda:
  1/0 support  = 1 (32-bit)
  using_dma    = 1 (on)
```

4. If you have problems with the DMA setting, run the command without the `-d 1` option. Now, test the disk again:

```bash
# hdparm -t /dev/sda
Timing buffered disk reads: 64 MB in 2.2 seconds = 28.83 MB/sec
```

As you can see from this example, buffered disk reads of 64 MB went from 19.31 seconds to 2.2 seconds after changing the parameters described. Playback should be much better now.

**Xine Won't Play Particular Media** — Messages such as `no input plug-in` mean that either the file format you are trying to play is not supported or it requires an additional plug-in (as is the case with playing DVDs). If the message is `maybe xyz is a broken file`, the file may be a proprietary version of an otherwise supported format. For example, I had a QuickTime video fail that required an SVO3 codec (which is currently not supported under Linux), although other QuickTime files will play fine.

If a particular multimedia format is not supported, but you have Windows DLLs available that support it, you can add those DLL files to the `/usr/lib/win32` directory. Some of these codec DLLs are available from `www.mplayerhq.hu/design7/dload.html#binary_codecs` in a package called `essential`. Choose a mirror site from the table under the Binary Codec Packages heading.

> **NOTE** The *CrossOver Plugin* (described in Chapter 8) can be used to play a variety of content, including the version of QuickTime just mentioned.

# Using Totem Movie Player

The Totem movie player (www.gnome.org/projects/totem) comes with the GNOME desktop environment. In CentOS, Totem can play video in Theora format with Ogg Vorbis audio. Totem is based on GStreamer (`http://gstreamer.freedesktop.org`) so it can be used with other video software from that project. In particular, free and fee-based codecs that you can purchase from `www.fluendo.com` for playing a variety of commercial audio/video formats will work with Totem.

Totem also supports a Xine backend that allows it to play a wide range of video content (in other words, anything Xine supports). To play commercial DVD movies, however, you need to replace the version of Totem that comes with CentOS with the `totem-xine` package available from third-party RPM sites. You also need to add the `libdvdcss`, `libdvdnav`, and `xine-1.1b-extras-nonfree` packages (provided the software is legal where you live).

Besides common controls, you would expect with a movie player (play, pause, skip forward, skip backwards, etc.), Totem lets you create playlists, take a snapshot of the current frame, and adjust the volume. You can change preferences, which let you add proprietary plug-ins, select your DVD device, and balance color. Figure 7-12 shows an example of the Totem window.

**FIGURE 7-12**

![](img/2f265415ceec72538dd3c78ffca75c10_326_0.png)

## Using a Digital Camera

With the GNOME Volume Manager features in CentOS, getting images from a digital camera can be as easy in Linux as it is in any desktop operating system. With most digital cameras that can be connected to a USB port on your computer, simply plugging the camera into a USB port (with the camera set to send and receive) causes the GNOME Volume Manager to:

- Immediately prompt you to ask if you want to download images from your camera.
- Run the gThumb image viewer and browser program to look at, manipulate, and download the contents of your digital camera.

Although GNOME Volume Manager will open your camera's contents in an image viewer, you can treat the storage area in your camera much as you would the storage area on a hard disk or a pen drive. I describe how to use your camera to store other data as well.

## Displaying Images in gThumb

The GNOME Volume Manager mounts the contents of your USB camera, treating the memory of your camera as it would any file storage device. When I tried it with an Olympus digital camera, my images were available from the /media/usbdisk/dcim/100olyncp directory.

Figure 7-13 shows the gThumb window displaying images retrieved from a digital camera.

**FIGURE 7-13**

Download images from digital cameras with the gThumb image viewer.

![](img/2f265415ceec72538dd3c78ffca75c10_327_0.png)

With your camera connected and the gThumb window open, here are some things you can do with the images on your camera:

- **Download Images** — Click on a single image or select Edit ▶ Select All to highlight all images from your digital camera. Then select File ▶ Import Photos. From the Import Photos window, you can select the destination where you want the images to be downloaded. As an alternative, you can download selected images to a folder on the GNOME desktop.
- **View Slideshow** — Select View ▶ Slide Show. A full-screen slideshow appears on your display, with the images changing every few seconds. The toolbar that appears at the top lets you display information about the photo name, date, and size (click Image Info); go forward and back through the images; and zoom in or out.
- **Manipulate Images** — Double-click on an image to open it, and select the Image menu. That menu offers a set of tools for enhancing, resizing, cropping, or otherwise transforming the image. You can also adjust the color balance, hue/saturation, and brightness contrast.
- **Assign Categories** — With an image selected, click on the Categories button. The Categories pop-up window lets you assign the image to a category to help you organize your photos. Assign available categories (such as birthday, family, holidays, or games) or click New and add your own categories.

Once images are downloaded to your computer's hard disk, you can continue to work with them using gThumb or use any of several tools available for manipulating digital images (GIMP, KView, and Kicksbox), to name a few.

> If you have a camera that saves images to a floppy disk, just insert that disk into your disk drive, and the contents of the disk should open automatically on your desktop.
> 
> In addition, if your camera saves images to SD or CF cards, you can purchase a USB card reader and view these files from Linux.

Check the gPhoto2 web site (www.gphoto.org/proj/libgphoto2/support.php) for information on supported cameras as well as other topics related to gphoto.

## Using Your Camera as a Storage Device

As I noted with my example of an Olympus camera with a USB connector, the GNOME Volume Manager is capable of detecting that camera once it is connected, and mounting its contents as a storage device. With the contents of a digital camera mounted, you can use your camera as a USB mass storage device by:

- Opening the mounted directory in a folder window and using any File Manager features to work with the images.
- Changing to the mounted directory from the shell and using commands to copy, move, rename, or delete digital images.

Of course, with your camera mounted as a file system, you are not limited to using it only for digital images. You can use it to store any kind of files you like, essentially using the camera as a storage device. The following list is a partial summary of digital cameras that can be used as a USB storage device:

- **Casio** — Supported models: QV-2400UX, QV-2400Z, QV-3x00, QV-4000, and QV-8000
- **Fuji** — FinePix 1300, 1400Zoom, 2300Zoom, 2400Zoom, 2800Zoom, 4200Z, 4500, 4700 Zoom, 4900 Zoom, 6800 Zoom, A101, A201, and S1 Pro
- **HP** — PhotoSmart 315, 318xi, 618, and C912
- **Konica** — KD200Z, KD400Z, and Revio KD300Z
- **Kyocera** — Finecam s3
- **Leica** — Digilux 4.3
- **Minolta** — Dimage 5, Dimage 7, and Dimage X
- **Nikon** — CoolPix 2500, 885, 5000, 775, and 995
