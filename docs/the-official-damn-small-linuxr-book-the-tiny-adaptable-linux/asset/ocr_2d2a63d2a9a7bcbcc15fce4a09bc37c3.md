system, which might run a bit slower, but will recover better if your digital media frame is not shut down properly. I always use ext3, but that’s your choice.

After the installation is complete, pop out the CD and reboot the laptop, as suggested. In fact, turn it off and turn it back on again. When the machine boots up, you will see the Grub boot screen. In my case, the default boot command wouldn’t work, so I used the arrow keys to move to the fb800x600 entry to use the framebuffer X driver with 800×600 screen resolution.

When asked to enter a password for the root and ds1 users, I just pressed Enter. Having a blank password allows the laptop to boot directly to DSL (as the ds1 user) without entering a password. You are also asked to select your X driver. Because you installed DSL to hard disk, all these settings are restored automatically, without having to back them up (as you would if you ran DSL from read-only media, such as a CD).

With DSL installed, I only used about 160MB of disk space. I still had 1.8GB of space remaining for software and digital media content (images, video, and music).

Before proceeding, be sure to assign your swap area and turn it on. In my case, the swap partition was hda2 (yours may be different). Open a terminal window as root and type the following:

```
# mkswap /dev/hda2
# swapon /dev/hda2
```

Next, shutdown your laptop and remove the CD. Then restart the laptop from hard disk.

# Adding Multimedia Player and Networking Software

If everything went well to this point, you should have a version of Damn Small Linux running from your laptop’s hard disk. Now, you need to add some software to be able to play your digital media from the frame.

With a traditional hard disk install, you don’t need to save your MyDSL extensions for the next reboot. Provided you use .dsl extensions, you can simply install the software extensions you want and they will be on your hard disk the next time you reboot.

Next, from the DSL desktop, select the MyDSL icon and add the following software using the MyDSL Extension Tool:

+   ■ GQview—From the Apps menu, select the gqview package. This package can be used to play slideshows of digital images.