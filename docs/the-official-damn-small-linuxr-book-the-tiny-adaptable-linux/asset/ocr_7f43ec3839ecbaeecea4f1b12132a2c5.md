+   ■ **Accessories**—Make sure that you get a power supply and battery with the laptop. Without those items, even if the machine works otherwise, you really don't have a usable machine. If you can find a power cord, you might end up paying an extra $10 or $20 (or more if it's hard to find) to get a replacement.

Sometimes, you can find a business or school selling multiple, similar laptops. If some aren't working, and you are so inclined, you can try to piece together a good, working laptop. Also, with older machines, having some spare parts isn't a bad idea.

# Evaluating a Used Laptop

If you are in a position to test out a laptop (whether you are buying it or just digging it out of your closet), Damn Small Linux itself is a great tool for evaluating whether a laptop will work for this digital media frame. For a really low-end machine, however, you might want to grab a floppy Linux distribution. I suggest having these media handy:

+   ■ **Damn Small Linux CD**—Use the CD that comes with this book or obtain one from Damnsmalllinux.org.

+   ■ **Damn Small Linux Boot Image**—Copy the bootfloppy.img to floppy disk, as described in Chapter 8. Use this in case you find a laptop that has a CD drive but the CD drive is not bootable.

+   ■ **Tom's Root Boot**—Download Tom's Root Boot floppy disk installer from http://toms.net/rb/download.html (tomsrbt-*-tar.gz). Extract the archive on a computer that has a floppy drive you can write to. Then, copy the floppy image to a blank floppy disk using the install.s script, as described in the tomsrbt.FAQ file. Use this floppy disk in case you encounter a laptop that has a floppy drive but no CD drive.

The two laptops I had available as candidates for the digital media frame serve as good ways to illustrate how to evaluate laptops with and without CD drives.

# Evaluating a Laptop with Damn Small Linux

With the Damn Small Linux CD in hand, I tried out the first of two laptops I had in my closet: a Compaq Pressario 1620 laptop. After having the screen appearance make it unusable by the default boot, I booted DSL by typing fb800x600 as the boot command (frame buffer). That came up fine, so I selected Xfdev xserver when prompted to configure X Setup.

With DSL running on my Compaq Presario, I could determine a lot of stuff about the machine. The first, and most important, thing it told me was that the