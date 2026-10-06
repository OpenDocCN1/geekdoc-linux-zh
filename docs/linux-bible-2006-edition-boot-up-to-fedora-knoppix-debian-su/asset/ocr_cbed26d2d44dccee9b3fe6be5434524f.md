# Choosing Different Install Modes

Most computers enable you to install Fedora in the default mode (graphical), there may be times when your video card does not support that mode. Also, although the install process detects most computer hardware, there may be times when your hard disk, Ethernet card, or critical piece of hardware cannot be detected and will require you to enter some information at boot time.

The following is a list of commands that you can type at the installation boot prompt to change installation modes to start the Fedora Core process. You typically try these modes only if the default mode fails (that is, if the screen is garbled or installation fails at some point). For a list of other supported modes, refer to the /usr/share/doc/anaconda*/command-line.txt file or press F2 to see short descriptions of some of these types.

| Command | Description |
|---|---|n| linux text | Runs installation in a text-based mode. Do this if installation doesn't seem to recognize your graphics card. |
| linuxres | Runs installation in 640 × 480 screen resolution for graphics cards that can't support the higher resolution. |
| linux nofb | Turns off frame buffer. |
| linux noprobe | Installation won't probe to determine your hardware; you must load any special drivers that might be needed to install it. Normally, install auto-probes to determine what hardware you have on your computer. |
| linux mediacheck | Check your DVD or CDs before installing. Because media checking is done next in the normal installation process, do this only to test the media on a computer that you are not installing. |
| linux rescue | Boots from CD, mount your hard disk, and lets you access utilities to correct problems that are preventing your Linux system from operating properly. (Not really an installation mode.) |
| linux expert | Bypasses probing so you can choose your mouse, video memory, and other values that would otherwise be chosen for you. If you believe that the installation process is not properly auto-probing your hardware. |
| linux askmethod | Has the installation process ask whether to install from (local CD, NFS image, FTP, HTTP, or hard disk). |
| linux updates | To install from an update disk. |