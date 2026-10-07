arbitrarily from one option to another, so this method is quite awkward.

**make menuconfig** Like make config, this option presents a text–based configuration tool. The make menuconfig tool uses text–mode menus, though, so you can skip from one option to another. This is a good way to configure the kernel if you’re using a text–based console login.

**make xconfig** This command also uses menus for configuration, but the menus are X–based, so you can configure the kernel using mouse clicks in X.

The kernel configuration options are arranged in groups. If you use make menuconfig or make xconfig, you can select one group to see a list of items in that group, as shown in Figure 8.2. Groups often have subgroups, so you may need to examine quite a few menus before you find a particular driver or option.

![](bbox=[0.14, 0.3, 0.77, 0.61])

Figure 8.2: Kernel compilation options are arranged hierarchically, with each main–menu option generating its own menu, which is displayed in a separate window when make xconfig is used.

**Note** A new kernel configuration tool, CML2 (http://tuxedo.org/~esr/cml2/) is under development and should be integrated into the Linux kernel as part of the 2.5.x kernel series. This may change many details of kernel configuration, but the basic principles should remain unchanged.

Describing every available kernel configuration option would be quite tedious, as well as inevitably incomplete, because options are constantly being added and changed. Therefore, Table 8.5 merely presents an overview of the main kernel headings in the 2.4.x kernel series. The 2.5.x kernel series is new enough at the time of this writing that its contents are almost certain to change in the near future.

# Kernel Version Numbers

Each Linux kernel has a version number of the form x.y.z.

+   - The *x* number is the *major version number*, and in 2002 this number is 2.

196