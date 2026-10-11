![](bbox=[0.08, 0.09, 0.63, 0.4])

**Figure 3: The default MX Linux Wildflower desktop.**

name of the latest release) and not the abstract patterns that have become the norm in many distributions (Figure 3). Otherwise, the MX Linux desktop as a whole seems less polished than most, without the unity of design that has become common on other distributions during the past decade. Utility windows, for example, are not consistently the same size, nor do all the icons seem designed as sets. Instead, aesthetics seem a distant second to functionality – perhaps not surprising in a relatively recent distribution. 

The emphasis on function is evident in the design choices. Taking a cue from Ubuntu's old Unity desktop, the panel is positioned by default on the left of the screen, maximizing the screen space for windows. The panel's contents seem meant to be system tools, al- though apps can be dragged to it (or the desktop) from the menu. If desired, users can make the panel into a dock. In other words, the only unusual thing about the panel is that, except for the default position, there is nothing

![](bbox=[0.08, 0.8, 0.35, 0.88])

**Figure 4: Systemd can be enabled from the boot manager.**

unusual about the panel. It's like that seen in most distributions, and for that reason, it is easy to learn. The same can be said for the Whisker menu (although for some reason the developers saw fit to give it a name). 

Behind the scenes, MX Linux is a rela- tively secure distribution, with many system utilities accessible only by the root users and prominent warnings of the possible consequences of possible actions. It depends on the Debian stable and stable-updates repositories, making it a reliable but far from cutting-edge dis- tribution, though its own developed packages are stored in the **mx.list** repos- itory. In fact, the manual specifically warns against trying to install Ubuntu's experimental Personal Package Archives (PPAs) or leaving other repositories permanently en- abled, rightly warning that doing so "will likely result in sys- tem instabilities

and lead to a re-installation." But per- haps the most unusual aspect of MX Linux is its neutral position on systemd. By default, MX Linux uses the more con- servative SysVinit. However, systemd is also installed and can be activated from the Advanced Options in the boot man- ager (Figure 4). Once systemd is in- stalled, SysVinit can be removed with the command **systemd-sys**. The Snapshot and Live USB persistence features will not work with systemd, but the rest of MX Linux should.

# # Desktop Tools

The emphasis on functionality is most apparent in the array of desktop tools. Together, they make MX Linux one of the distributions that is easiest to ad- minister from the desktop without re- sorting to the command line in the most common cases. Versions of some of these tools (such as Conky or Tweak) are common in many distributions.

![](bbox=[0.65, 0.44, 0.92, 0.67])

**Figure 5: Bash Config provides a GUI for several command-line actions.**

![](bbox=[0.65, 0.72, 0.92, 0.88])

**Figure 6: Boot Repair helps to restore the boot manager.**