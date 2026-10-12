broader uses; there is truth to the cliché that a picture is worth a thousand words. Sometimes, it is easier to show an example than it is to describe it.

A captured screen image (also called a screen grab or a screenshot) can be used to illustrate an error in the display of an application (a font problem, for example) or an error dialog that is too complex to copy down by hand. You might just want to share an image of your beautifully crafted custom desktop configuration with your friends or illustrate your written documents. In this section, you learn how to capture screen images for these and other purposes.

When using the GNOME desktop, you can take advantage of the built-in screenshot mechanism (gnome-panel-screenshot). Access this tool by pressing the Print Screen key. (Alt+Print Screen takes a screenshot of only the window that has “focus” on a desktop.) Captured images are saved in .png format.

You also can capture screen images from a remote computer using tools supported by Red Hat Linux. The `import` command (one of ImageMagick's commands) was used to take the screenshots for this book, for example, using a local computer and a remote computer on a LAN.

First, we ran `xhost +` on the remote computer to allow another computer access to the X server on the remote machine; the command to take the screenshot is run on our local machine like this:

```
$ import -window root -display 192.168.2.4:0 12fig07.jpg
```

This utility made a difficult task easy because the publisher required the screenshots be done from an 800 × 600 screen (too small to comfortably work in) to accommodate their printing and production equipment.

We could also have used the classic Unix tool `xwd` to take screenshots. The command would have looked similar to that of `import`:

```
$ xwd -root -display 192.168.2.4:0 -out 12fig07.jpg
```

Although the screenshots could have been taken with The GIMP and saved in the appropriate format, we would have had to be running The GIMP on that computer and navigating the menus every time we captured an image—the remote option of `import` was very convenient.

We did not use Ksnapshot (not included in the menus, but available from the command line) because it does not support the .pcx format the publisher used to use and it must be run locally, but it can take screenshots easily and is our preferred tool for use on a single machine.