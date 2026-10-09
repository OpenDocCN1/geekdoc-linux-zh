+   2. Change to the /usr/src/linux directory.
3. Uncompress the file. If you downloaded the patch with the `.bz2` extension, use the `bunzip2 patch-2.4.21` command. If you downloaded the patch with the `.gz` extension, use the `gunzip patch-2.4.21` command.
4. The file `patch-2.4.21` should be in the directory. To apply the patch to the kernel source tree, use the `patch -p1 < patch-2.4.21` command.

# Configuring the Kernel

Configuring the kernel is your chance to customize the modules that are available for your system. You configure the kernel by using a menu-driven utility to pick the modules you want to include with your kernel. For example, you can select sound modules, video modules, ISDN modules, and others. The menu can be displayed from the CLI or from the GUI. From the `/usr/src/linux` directory, execute the `make menuconfig` command for the CLI menu interface.

The kernel configuration menu is displayed (Figure 13-11). To select a menu item, use the up and down arrow keys to highlight the selection and then press Enter. Use the space bar to enable or disable an item. Use the left and right arrow keys to choose Select, Exit, or Help. The instructions are onscreen.

FIGURE 13-11
menuconfig.

![](bbox=[0.31, 0.4, 0.85, 0.65])

To use the GUI configuration menu, from the `/usr/src/linux` directory, type the command `make xconfig`. The Linux Kernel Configuration dialog box is displayed (Figure 13-12). Use mouse movements to select what you want to configure and enable or disable items by using mouse clicks on option buttons.

FIGURE 13-12
xconfig.

![](bbox=[0.31, 0.77, 0.85, 0.97])