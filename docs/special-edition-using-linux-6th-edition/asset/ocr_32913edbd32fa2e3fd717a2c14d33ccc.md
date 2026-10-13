At the time of this writing, only the regular RealPlayer 7 Basic package is available for Linux. There is also currently no commercial (that is, one that costs money) version of RealPlayer for Linux.

It can be tricky to find the download page for RealPlayer 7 Basic. Most of the links will steer you toward their commercial product, RealPlayer 8 Plus. When you first arrive at the RealNetworks Web page, select the Download RealPlayer link at the top of the page, and then select RealPlayer 8 Basic near the bottom of the page. Finally, select Download RealPlayer for UNIX near the bottom of the screen. Fill out the presented form, selecting Linux 2.x (libc6 i386) RPM for RPM-based distributions, or Linux 2.x (libc6 i386) Self-Extracting for Debian. The Red Hat RPM will work fine for OpenLinux.

After downloading the RealPlayer package, install it with one of the following code snippets:

```
# rpm -i rp7_linux20_libc6_i386_cs1_rpmRealPlayer-8.0.1.i386.rpm
# chmod u+x rp7_linux20_libc6_i386_cs1.bin
# ./rp7_linux20_libc6_i386_cs1.bin
```

Finally, fill out the short configuration dialogs presented, and RealPlayer will start up (as well as Netscape, taking you to their home page). Note that prompting for user input and automatically starting the application are unusual (and, many would say, inappropriate) for RPM packages.

> **Note**
> 
> The name of the file you download might be different from this. Just replace `linux20_libc6_i386_cs1.rpm` with the name of the file downloaded. Note also that instead of dots, these files have underscores in their names.
> 
> It is possible that you will need to add the option `-nodeps` or `--force` to install this RPM. RealPlayer sometimes builds its RPMs based too strongly on Red Hat systems. It should still work fine on eDesktop or other RPM-based systems.

# USING REALPLAYER

To launch RealPlayer, select RealPlayer 7 from the Application Launcher menu in KDE. If you are not using KDE, you can start RealPlayer by running `/usr/X11R6/bin/realplay`. The RealPlayer main screen is shown in Figure 7.1.

**Figure 7.1**
Main RealPlayer window—audio and video.

![](bbox=[0.204, 0.791, 0.464, 0.965])