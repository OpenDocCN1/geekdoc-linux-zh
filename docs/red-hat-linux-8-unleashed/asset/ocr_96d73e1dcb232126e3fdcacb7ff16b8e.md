disk can be handy, especially if an error was made during the install and the boot loader fails to boot Linux.

If you choose to create a boot disk, you'll need to have a blank diskette on hand. Select Yes, insert a blank diskette when prompted, configure the boot disk, and continue the install.

# Configuring a Graphical Desktop

If you select the X Window System for installation (not really needed for server operations, but essential for a productive desktop), you're next asked to configure X to work with your PC's video card and monitor, as shown in Figure 3.25. Note that you can skip this configuration and configure a desktop for Red Hat later. See Chapter 6 for details on configuring X to work with your PC.

![](bbox=[0.206, 0.342, 0.793, 0.599])

**Figure 3.25** Use this screen to configure your video card for use with X11.

Again, note that you won't be asked to select a video card if you don't install the X software. The Red Hat installer will automatically probe your system's graphics card and monitor for hardware configuration information unless you use the linux probe boot option.

> **TIP**
You can skip X configuration and configure X after installation. This might be a better approach if the install fails to accurately probe your hardware or cannot configure X during the install, but you still desire to have X software installed. See Chapter 6 for details on configuring X to work with your PC's graphics card.

If necessary, use the Tab key to highlight a <change> button and press Enter to select a different video card or set the amount of video RAM available on your card. If you choose to change the video card, you'll see a list of cards as shown in Figure 3.26.