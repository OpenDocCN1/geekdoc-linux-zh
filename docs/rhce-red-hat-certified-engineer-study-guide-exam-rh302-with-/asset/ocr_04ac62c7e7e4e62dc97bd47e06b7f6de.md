# Configuring X 641

ask if you want to configure the system to start X at boot time. Click the Yes or No button, according to your preference.
If you can't see the small dialog box, Xconfigurator will return you to the configuration procedure after several seconds. You can specify different operating parameters and try again to start X.

Laptops are notoriously difficult to configure for X. One reason is that seemingly identical laptops may contain very different we hardware. For on-configuring Linux laptops, see the Linux Laptop Web page, www.utexas.edu/users/kharker/linux-laptop.

Now complete Exercise 26.1 to gain experience using Xconfigurator.

EXERCISE 26.1

# Using Xconfigurator

You may sometimes find it necessary to install X after installing Linux. This exercise gives you practice in doing so. Perform these steps:

+   1. Install X and the X-related packages that are required to use Xconfigurator.
2. Configure X by using Xconfigurator. Verify that the configuration works.
3. Configure X by using Xconfigurator's quickstart facility. Verify that the configuration works.

For assistance in completing this exercise, you may refer to this book and other documentation. However, before taking the RHCE exam, be sure you can install X using Xconfigurator without recourse to help.

# XF86Setup

The XFree86 Project distributes its own X configuration tool, XF86Setup. Some administrators prefer the tool to Xconfigurator because it allows use of the mouse. To do so, it uses the facilities of the VGA16 server, which is supported by a wide range of video devices.
To use XF86Setup, you should install the following packages in addition to those in the preceding section:

+   - glib10, a library of utility functions, which of some are used by the tool
- tcl, a scripting language used by CA

Copyright ©2000 SYBEX, Inc., Alameda, CA www.sybex.com