
![](img/af53325d7f38f1cdafca9f44568e4ab8_323_0.png)

## Changing the Bootloader

The bootloader defines the kernel to boot and any options you want to pass to the kernel. For this example, I used the Grub boot loader. You can change the Grub boot loader by editing the /boot/grub/menu.lst file. Changes to that file are automatically picked up when you reboot.

The following shows how I edited the existing menu.lst file (I removed comment lines for clarity):

```
default 2
timeout 15

title DSL
kernel /boot/linux24 root=/dev/hda1 quiet vga=normal noacpi noapm nodma
noscsi frugal

title DSL fb800x600
kernel /boot/linux24 root=/dev/hda1 quiet vga=788 noacpi noapm nodma
noscsi frugal
```

```
title DSL fb800x600-F
kernel /boot/linux24 root=/dev/hda1 quiet vga=788 noacpi noapm nodma
noscsi frugal desktop=frame
```

The changes to the menu.lst file are shown in bold. For the default value, I changed 0 to 2 so that the third entry (DSL fb800x600-F) is booted by default. I then copied the DSL fb800x600 entry and created a new third entry (calling it DSL fb800x600-F). After that, I added the desktop=frame option. The desktop=frame option tells DSL that instead of running Fluxbox or jwm as the window manager, it should start a window manager definition called frame (which we will define in the next section).

There are other options you can set as well. If you set up a static IP address for your media frame (which is a good idea), add the nodhcp option to the boot prompt. For example, if your laptop supports higher resolution, you could set fb1024x768 or fb1280x1024 as the default boot entries.

Keep in mind that at this point, your laptop will try to boot directly to the slideshow viewer. Therefore, if you need the DSL desktop to make further changes, be sure to select one of the other entries on the boot screen.

## Modifying .xinitrc to Start Player

The way that Damn Small Linux is configured, with no password set for the DSL user, DSL logs in the ds1 user automatically and starts the desktop. How the desktop starts is directed by the contents of the /home/ds1/.xinitrc file. By adding a new desktop entry for your frame desktop, you can set the GQview application (gqview command) to start immediately when the desktop starts.

Open the /home/ds1/.xinitrc file using any text editor. Then, add an entry for the frame desktop as shown:

```
# put X windows programs that you want started here.
# Be sure to add at the end of each command the &
.
case $DESKTOP in
frame )
/usr/bin/gqview -s -f /var/mediaframe/pics
;;
fluxbox )
fluxter &>/dev/null &
wmsvallow -geometry 70x80 docked docked.lua &
exec fluxbox 2>/dev/null
;;
jwm )
./.background
```

```
sleep 2
    exec jwm 2>/dev/null
    ;;
    * )
        exec fluxbox 2>/dev/null
    ;;
esac
```

The text shown in bold illustrates the entry added to the $DESKTOP case statement when the boot option desktop=frame is used. With the X display already started at this point, instead of starting a window manager, the frame entry starts the gqview command with the -s option (slideshow), -f option (full screen), and the name of the directory containing the images to play (/var/mediaframe/pics).

## Adding Digital Content

At this point, the laptop is all set up to start playing digital images. You need to find a way to add them to your digital media frame on an ongoing basis. There are two basic ways for adding images to your digital media frame:

- **Removable media**—If you don’t have a network interface to the digital media frame, you can add content via a CD, USB flash drive, or other removable medium. This is not a good long-term solution, because after the keyboard is removed, you don’t have a way to copy files from those media to your hard disk. It might also be hard to access removable drives after everything is tucked inside the frame.

In the meantime, however, you could copy a bunch of images onto a USB flash drive and then plug that drive into your laptop, mount the partition (probably /dev/sda1), and copy files to the /var/mediaframe/pics directory. You could also configure DSL to automatically mount the USB flash drive at boot time and have gqview use a directory on the drive for images (such as /mnt/sda1/images). That way, you wouldn’t need a network connection at all to change content. You could just change images on the drive, plug it back in, and reboot.

- **Network interface**—Having a network connection to your media frame is important for being able to add images easily and make any ongoing changes to DSL and your media content. As I noted earlier, I connected a USB Ethernet adapter to my laptop and plugged a standard RJ-45 Ethernet cable into that and my network switch.

Configure your network interface with a static IP address. For a wired Ethernet interface, run the netcardconfig command (or select System, followed by Net Setup
