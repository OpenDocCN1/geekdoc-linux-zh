# # Installing Unreal Tournament 2004

Unreal Tournament 2004 (or *UT2004*, as it is affectionately known) from Epic natively supports Linux in both its 32-bit and 64-bit incarnations (see Figure 13.3). Be aware that if you run the 64-bit version, you need to ensure that your graphics drivers are supported under 64-bit mode.

![](bbox=[0.14, 0.22, 0.82, 0.61])

**FIGURE 13.3**  *Unreal Tournament 2004* builds on the classic deathmatch scenario with more enemies and more combatants!

Installation is easy, and there are two ways to do it. You can insert the DVD and mount it, or you can open the DVD in GNOME and double-click the `linux-installer.sh` icon. When you are asked whether you want to run it or display its contents, click **Run** in Terminal to launch the graphical installer. As with *DOOM 3*, you must read and accept the terms of the EULA before you are allowed to install *UT2004*. You are given the option of where you want to install the software; the default is in your home directory. After you select the destination directory, click **Begin Install** and *UT2004* does the rest.

The alternative way of accessing the graphical installer is via the command line. Change directory to `/media/cdrom/` and type

```
```
$ sh linux-install.sh
```
```

This brings up the graphical installer. Continue through this and, when finished, you should find *Unreal Tournament 2004* in `/home/username/ut2004`.