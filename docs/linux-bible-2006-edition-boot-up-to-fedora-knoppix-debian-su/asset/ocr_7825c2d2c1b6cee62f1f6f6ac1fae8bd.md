# 336 Part III ♦ Choosing and Installing a Linux Distribution

You can install packages that are selected by default in the OpenSUSE install process from the OpenSUSE 10.0 disk #1 image that comes with this book. If you want to install additional packages, you need to get them CDs 2–5 yourself or install the packages over the network after the initial install is complete.

Choose group selection to select the specific packages in each group. Check boxes indicate which packages you want to install. It is a good idea to look through this to see what you are getting. If you change any of the selections, click the Check Dependencies box to make sure that all packages that depend on are being installed. Figure 10-3 shows the YaST module for adding, removing, and finding out software packages.

![](bbox=[0.218, 0.345, 0.782, 0.623])

Figure 10-3: Install and remove software using the YaST software module.

The YaST software module used during installation is the same one used on a running SUSE system (In Figure 10-3, it's shown on a running SUSE system). In either case, you can find out of information about packages that interest you. With a package selection, click tabs in the bottom-right corner of the screen to see its description, technical data (its size, package, and so on), dependencies, and version numbers.

# 12. Booting. Selecting Booting to see the information that is added to your boot loader (GRUB, by default, but you can use the LILBO boot loader as well). The boot loader includes the information needed to boot Linux: the boot loader, default operating system to boot, and other information.