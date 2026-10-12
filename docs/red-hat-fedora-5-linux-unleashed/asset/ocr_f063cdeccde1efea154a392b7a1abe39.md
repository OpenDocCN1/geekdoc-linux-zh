An examination of the man page for pnm, the portable bitmap file format, reveals no conversion utilities. It's a monochrome format and serves as the foundation of the other related formats.

# Capturing Screen Images

You can use graphics manipulation tools to capture images that are displayed on your computer screen. Although this technique was used for the production of this book, it has broader uses; there is truth to the cliche that a picture is worth a thousand words. Sometimes it is easier to show an example than it is to describe it.

A captured screen image (also called a *screen grab* or a *screenshot*) can be used to illustrate an error in the display of an application (a font problem, for example) or an error dialog that is too complex to copy down by hand. You might just want to share an image of your beautifully crafted custom desktop configuration with your friends or illustrate your written documents. In this section, you learn how to capture screen images for these and other purposes.

When using the Gnome desktop, you can take advantage of the built-in screenshot mechanism (`gnome-panel-screenshot`). Access this tool by pressing the Print Screen key. (Alt+Print Screen takes a screenshot of only the window that has focus on a desktop.) Captured images are saved in .png format.

You also can capture screen images from a remote computer using tools supported by Xserver. The `import` command (one of ImageMagick's commands) was used to take the screenshots for this book; for example, using a local computer and a remote computer on a LAN.

First, we ran `$ xhost +` on the remote computer to allow another computer access to the X server on the remote machine; the command to take the screenshot is run on our local machine like this:

```
$ import -window root -display 192.168.2.4:0 12fig07.jpg
```

This utility made a difficult task easy because the publisher required the screenshots be done from an 800x600 screen (too small to comfortably work in) to accommodate its printing and production equipment.

We could also have used the classic UNIX tool `xwd` to take screenshots. The command would have looked similar to that of `import`:

```
$ xwd -root -display 192.168.2.4:0 -out 12fig07.jpg
```

Although the screenshots could have been taken with The GIMP and saved in the appropriate format, we would have had to run The GIMP on that computer and navigate the menus every time we captured an image—the remote option of `import` was very convenient.