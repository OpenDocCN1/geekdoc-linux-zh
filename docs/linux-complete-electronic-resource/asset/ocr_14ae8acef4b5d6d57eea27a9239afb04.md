# ## Using the Root Disk

After booting the boot disk, you will be prompted to enter the root disk or disks. At this point you should remove the boot disk from the drive and insert the root disk. Then press Enter to go on. You may have to load a second root disk.

What’s actually happening here is this: the boot disk provides a miniatur e operating system that (because the hard drive isn’t prepared) uses a portion of your RAM as a virtual disk (called, logically enough, a *ram disk*).

The root disk loads onto the ram disk a small set of files and installa- tion tools, which you’ll use to prepare your hard drive and install a pro- duction Linux on it from your CD-ROM.

# ## Choosing EGA or X Installation

Older kinds of Linux (including Slackware) gave you a shell at this point and required you to enter installation commands by hand in a prescribed sequence. This is still possible, but newer ones start by running a screen- oriented installation program that tries to interactively walk you through these steps, giving lots of help.

You will probably get the option to try to configure X right away so the installation program can have a graphical look. If you choose this route, the installation program will quiz you about your mouse and monitor type before getting to the installation proper. Once you get your produc- tion Linux installed, these settings will be saved for you. You will be able to tune your monitor’s performance later, so at this stage it makes sense to settle for a basic 640x480 SVGA mode.

X isn’t necessary for installation, but (assuming you can get past the mouse and monitor configuration) many people find the graphical inter- face easier to use. And you’re going to want to bring up X anyway, so try- ing it early makes some sense.

Just follow the prompts in the program. It will take you through the steps necessary to prepare your disk, create initial user accounts, and install software packages off the CD-ROM.

In the following subsections we’ll describe some of the tricky areas in the installation sequence as if you were doing them by hand. This should help you understand what the installation program is doing and why.