
Bear in mind that Wine stands for *wine is not an emulator*, so do not start thinking of it as such—the community can get quite touchy about it!

![](img/7aaa8e4f2209bf9f2fb443905096e94c_212_0.png)

*FIGURE 9.1*   Sliding around corners in the high-speed Torc.

A major gripe of Linux users has been the difficulty involved in getting modern 3D graphics cards to work. Thankfully, both ATI and Nvidia support Linux, albeit by using closed-source drivers. This means that Ubuntu does not ship with native 3D drivers for either graphics card. It is fairly easy to get a hold of these drivers and install them using either synaptic or apt.

## Installing Proprietary Video Drivers

Unfortunately, both Nvidia and ATI still produce proprietary drivers, meaning that the source code is not open and available for developers to look at. This means that it is hard for some Linux distros to include them as part of their standard package manifest. However, Ubuntu have taken the pragmatic approach of including both Nvidia and ATI drivers within the main Ubuntu distro, albeit disabled by default. That way the end user can, if they so wish, activate those drivers to take advantage of them.

## Linux Gaming

185

> **NOTE**
> 
> Don’t think that proprietary drivers are the only way on Linux, as there is a lot of development going into providing totally free and open source drivers for slightly older graphics cards. Ubuntu will automatically select the best “free” driver for your system and allow you to switch the proprietary driver should you want to. Although the open source drivers will provide 3D acceleration, this support doesn’t always extend to the more recent graphics cards.

It’s very easy to activate the proprietary driver if you need to; all you have to do is use the Restricted Drivers Manager found under System, Administration and which is shown in Figure 9.2.

![](img/7aaa8e4f2209bf9f2fb443905096e94c_213_0.png)

**FIGURE 9.2**  Use the Restricted Drivers Manager to activate or deactivate the appropriate proprietary graphics driver for your graphics card.

You will be prompted for your password before you proceed, as you will be setting a system-wide option. Once the Restricted Drivers Manager has opened up, look for the entry that says ATI (or Nvidia) Accelerated Graphics Driver and check the box. Ubuntu will confirm that you want to use the proprietary driver and, if you agree, will automatically download and configure the relevant driver. To activate the driver, you will need to log out of GNOME by going to System, Log Off. The next time you log in, Ubuntu will automatically switch to the proprietary driver.

## Installing Games in Ubuntu

In this section, we’ll take a look at how to install some of the more popular games for Ubuntu. Alongside the usual shoot-em-up games, you’ll also find one or two strategy focused titles.

### DOOM 3

The follow-up to the infamous DOOM and DOOM II was released in the second half of 2004 (see Figure 9.3), and it provides a way to run it under Linux. You still have to purchase the Windows version because you need some of the files that are on the CDs. The rest of the files are available from id Software at http://zerowing.idsoftware.com/linux/doom. You can find other information about graphics cards there, too.

![](img/7aaa8e4f2209bf9f2fb443905096e94c_214_0.png)

FIGURE 9.3 Descending into the pits of hell. DOOM 3 is one of the most graphic computer games available.

You can download the file doom3-linux-*.run from the id Software FTP server or by using BitTorrent. When that’s finished, open a terminal and change to the directory in which you saved the file. Type the following command:

```
# sh doom3-linux-*.run
```

This begins the installation of the demo. As with other commercial games, you must agree to an EULA before you can install. Follow the installation procedure. When it finishes, you need to get the Windows CDs ready.

The files you need to copy across are the following:

- `pak000.pk4`
- `pak001.pk4`
- `pak002.pk4`
- `pak003.pk4`
- `pak004.pk4`

They must be saved in the `/usr/local/games/doom3/base/` directory. After you copy the files, you can start the game by typing `doom3` or start the dedicated server for multiplayer games by typing `doom3-dedicated`.

### Unreal Tournament 2004

*Unreal Tournament 2004* (or *UT2004*, as it is affectionately known) from Epic natively supports Linux in both its 32-bit and 64-bit incarnations (see Figure 9.4). Be aware that if you run the 64-bit version, you need to ensure that your graphics drivers are supported under 64-bit mode.

![](img/7aaa8e4f2209bf9f2fb443905096e94c_215_0.png)

**FIGURE 9.4**　Unreal Tournament 2004 builds on the classic deathmatch scenario with more enemies and more combatants!
