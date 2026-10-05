
So you now are faced with the challenge of attaching your scanner device to your Linux box. If you are in the market for a good digital scanner, there are a few things to keep in if you want to maintain Linux-compatibility.

- A SCSI interface is your best option. Some parallel scanners are supported, and you can, at least in theory, get one of those SCSI-to-parallel to work, with luck and a lot of hacking, but if you want to keep your sanity, make sure that you get a good SCSI card to accompany your scanner.

- You should take a look at the SANE compatibility list. SANE interfacing software that is fast becoming the most frequently used and is the one you will be dealing with. You can find the list at http://www.mostang.com/sane.

- Don't be afraid to spend a little extra money. The added quality you will gain by spending a little more on a higher end scanner will be worth it. The reason: besides scan quality and durability, there is also the issue of user-adjustable scanner resolution. You will want a scanner that let you change this easily, otherwise, you might be stuck with RAM-intensive scanners at 1800 x 1600 resolution for something like your driver's license photo. This can waste a lot of time.

There are actually (not surprisingly) a lot of choices when using a scanner with Linux. However, the SANE package offers the widest variety of supported devices, as well as easy expandability and good networking support. Scanner device support is still in its developmental stages in Linux, so you will definitely want to check the compatibility list before purchasing a scanner to use explicitly with Linux.

After you have chosen, purchased, and wired your scanner, getting it picked-up under Linux isn't too difficult, provided that you do have a fairly standard scanner attached to a SCSI interface.

The first thing to do is to download the SANE distribution from www.mostang.com/sane. After installing the distribution, follow the directions as outlined in the README (./configure && make install), and you should be all set. Then you will want to start with the scanner command. This brings up the SANE dialog box, as shown in Figure 24.1. You can also use it via the command line with the scanner command (Consult the man page for more details.).

By going scanner interface in the dialog box and selecting your scanner interface model, you will be ready to scan, as long as there are no difficulties.

To scan, turn your scanner on, load your source image into the scanner, select the proper scanner interface from within xscanimage, and press OK. Your image should appear onscreen (see Figure 24.1). You can also use the Preview function to get a quick overview of the appearance of your scan.

## Using Peripherals with Linux

## FIGURE 24.1

Using a scanner device isn't too terribly difficult with the GIMP and SANE.

![](img/0183f053b347a6407a2381be231d0345_332_0.png)

Scans frequently come in at a larger size than you want to use for your final image. This is actually a good thing because editing your image, and reducing the image size usually results in a higher-quality image than if you had scanned it at the desired size to begin with.

You can use xscanimage as a GIMP plug-in by making the following symlink: `ln -s /usr/local/bin/xscanimage -/.gimp/plug-ins`

It should appear in the GIMP's Xtns menu.

Sometimes the scanned image, taken from a book or magazine, might look a little grainy. This is due to the inks printed on the medium not translating to screen. This can be countered by tinkering with the options in the NL Filters plug-in. You can use this, and to make quick work of grainy lines. Also, doing this at a larger size, and then reducing the file dimensions will also lessen the grainy effect. The SANE package also has support for some functions for the improvement of image quality, such as color intensity and gamma. You should play with these settings to find what effect works best.

SANE also comes with a command-line client, scanimage, which has a plethora of useful, if not cryptic features. You might want to read the man page or get a listing of options with `scanimage -h`.

## Digital Cameras

Getting digital cameras to work with Linux is a little more straightforward.

You can find the list at http://www.linux.org.

If you're using something such as a webcam, you can get it from gcam.org.

## Color Printers

Fortunately, printers connected directly via USB are the easiest to get working under Linux.

... 

In order to get XFree86 with another pointing device, you will need to edit your /etc/X11/X86 config file. Add the module in the modules section of the config file, like this:

```markdown
Section Modules
Load x86Wacom.so
EndSection
```

Then, X will need to set some parameters for using the module. These are set in the Xinput section, in this example:

```markdown
Section "Xinput"
Subsection "WacomStylus"
Port "/dev/ttyS0"
DeviceName "Wacom"
Mode Absolute
Suppress 15
EndSubsection
SubSection "WacomStylus"
Port "/dev/ttyS0"
DeviceName "WacomCore"
Mode Absolute
AlwaysCore
Suppress 15
EndSubsection
SubSection "WacomCursor"
Port "/dev/ttyS0"
DeviceName "CURSOR"
Mode Absolute
Suppress 15
EndSubsection
SubSection "WacomCursor"
Port "/dev/ttyS0"
DeviceName "CursorCore"
Mode Absolute
AlwaysCore
Suppress 15
EndSubsection
SubSection "WacomEraser"
Port "/dev/ttyS0"
Mode Absolute
Suppress 15
EndSubsection
```
