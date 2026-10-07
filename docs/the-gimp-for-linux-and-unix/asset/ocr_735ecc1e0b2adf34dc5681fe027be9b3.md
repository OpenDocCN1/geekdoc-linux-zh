# Is the GIMP Installed?
(And What to Do if it Isn't)

# Working with Scanners,
Digital and Video Cameras,
and Drawing Tablets

Whether the GIMP was installed or not depends on the selections you made during installation of your Linux/Unix distribution. A missing menu item does not necessarily indicate the absence of the GIMP; it may not have been added to the menu. Below are some steps to find the GIMP; These steps assume you are using the RedHat Linux 6 distribution; if you're using another distribution, refer to the documentation that came with your distribution or check the Web site that supports your favor of Unix.

Scanners, cameras, pens, and other pointing devices are great for creating digital images that you can use in the GIMP. Unfortunately, you can't just plug a peripheral and have it automatically work with the GIMP. You need to install drivers and compile programs. Compilation is easiest for programmers to achieve, involves a number of tricky steps, and is different for each hardware platform and operating system. As such, compilation is beyond the scope of this book, but I will give a brief description of what's needed for each peripheral and where you can get help with compilation if you need to do it.

+   - Look on the menus on your desktop. If you find a GIMP item, select it to launch the GIMP.

+   - If a menu item isn't present, use File Manager to find a file gimp is present in the /usr/bin/ directory. If the gimp file is there, double-click to start the GIMP.

+   - If a menu item is not present and you can't find the GIMP file in /usr/bin, then the GIMP probably has not been installed. You can check this by running GnoPRM and seeing whether the GIMP package is installed. It should be listed with the Multimedia packages in the Applications hierarchy.

+   - If the GIMP is not installed, then you will have to install it from the RedHat Linux 6 CD-ROM.

+   - If all else fails, you can download the most recent stable version of the GIMP from http://www.gimp.org/download.html. Instructions for installing the GIMP can be found at http://www.gimp.org/install_help.html

Digital scanners as either parallel or SCSI interfaces, though a scanner with a SCSI interface is the easiest to configure and use with the GIMP. SANE (Scanner Access Easy) is the universal scanner interface that is most frequently used with the GIMP. To find out which scanners are supported by SANE, and how to compile, install SANE, go to http://www.mostang.com.

Digital and video cameras with a camera hooked up to a parallel port and the appropriate driver installed, the GIMP can be used to capture digital and video snapshots. To find out what's supported, go to http://metalab.unc.edu/pub/Linux/video/!index.html.

Wacom pen and other drawing tablets needs to be recognized by X Windows before the GIMP can use this device. In addition, you'll need to have a recent version of the GIMP Toolkit (GTK) installed on your computer so the GIMP supports Input. For Wacom driver, go to http://www.lepied.com/xfree86/. Check out http://www.gtk.org/ for the latest version of the GTK.