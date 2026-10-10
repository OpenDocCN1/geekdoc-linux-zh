# Display Chipsets

The sad truth at this point, even with the increasing popularity of Linux, is that most Intel-based notebook manufacturers still cater to Microsoft's software mo- nopoly and build notebooks to run only one (and, in rare cases, two) variant(s) of Microsoft's operating systems: Windows 98 and Windows NT. At the time this chapter was written, the industry was poised for the deployment of Windows 2000, and several notebook manufacturers have certified laptops for this operating sys- tem. The fact that most, if not all, of these laptops are supported by Linux (at least in console, or text-only, mode) is an amazing testament to the determination and process of Open Source programmers.

Another negative factor is that makers of the graphics chipsets that drive modern notebooks are loath to release specifications regarding how the displays are driven. This poses severe constraints on Open Source programmers struggling to craft display driver support for new notebooks. Most, if not all, of these manufacturers are concerned only with supporting the Original Equipment Manufacturer of note- book PCs and not the end user.

With the increased power, speed, and display resolution of modern notebooks, these chipset manufacturers are in stiff competition to provide hosts of additional features, such as ever-faster three-dimensional image rendering, graphics accelera- tion, and incorporation of other notebook subsystems, such as audio. Chances are good that if you buy a recently introduced laptop with a new graphics chipset, you will run into display compatibility problems.

The graphical interface for Linux is the X Window System. Most Linux distribu- tions come with the XFree86 X11 distribution from The XFree86 Project, Inc. Although XFree86 is free, you can also purchase a commercial X11 distribution from other companies, such as Xi-Graphics or MetroLink, Inc. You'll improve your chances of compatibility if you research support for your notebook's display before purchase. However, most Linux notebook users first try XFree86 to see if it works.

# The iBook and X11

Apple iBook users need to use a special Linux kernel (at least version 2.2.14 or greater) with frame-buffer support, along with a special X11 server application named XF86_FBDev. The maximum resolution is 800×600 pixels with a color depth of at least 16bpp.