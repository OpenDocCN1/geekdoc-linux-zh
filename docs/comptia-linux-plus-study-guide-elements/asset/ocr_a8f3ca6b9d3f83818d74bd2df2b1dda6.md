+   12. To reset a *root* password that you’ve forgotten, you blank the second field in *root*’s entry in `/etc/shadow`. What should you do then?
+      A. Copy `/etc/shadow` so that you don’t forget the password again.
+      B. Type `shadow-update` to update the shadow passwords.
+      C. Delete the entry for *root* in `/etc/passwd`.
+      D. Use `passwd` to set a new password for *root*.

+   13. Which of the following is the *most* useful information in locating an X driver for a video card?
+      A. The interrupt used by the video card under Microsoft Windows
+      B. The name of the driver used by the card under Microsoft Windows
+      C. Whether the card uses the ISA, VLB, PCI, or AGP bus
+      D. The name of the video card’s manufacturer

+   14. Which of the following summarizes the organization of the `xorg.conf` file?
+      A. The file contains multiple sections, one for each screen. Each section includes subsections for individual components (keyboard, video card, and so on).
+      B. Configuration options are entered in any order desired. Options relating to specific components (keyboard, video card, and so on) may be interspersed.
+      C. The file begins with a summary of individual screens. Configuration options are preceded by a code word indicating the screen to which they apply.
+      D. The file is broken into sections, one or more for each component (keyboard, video card, and so on). The end of the file has one or more sections that define how to combine the main sections.

+   15. In what section of `xorg.conf` do you specify the resolution that you want to run?
+      A. In the `Screen` section, subsection `Display`, using the `Modes` option
+      B. In the `Monitor` section, using the `Modeline` option
+      C. In the `Device` section, using the `Modeline` option
+      D. In the `DefaultResolution` section, using the `Define` option

+   16. Which of the following features do KDM and GDM providing XDM doesn’t?
+      A. An encrypted remote X-based access ability, improving network security
+      B. The ability to accept logins from remote computers, once properly configured
+      C. The ability to select the login environment from a menu on the main login screen
+      D. A login screen that shows the username and password simultaneously rather than sequentially