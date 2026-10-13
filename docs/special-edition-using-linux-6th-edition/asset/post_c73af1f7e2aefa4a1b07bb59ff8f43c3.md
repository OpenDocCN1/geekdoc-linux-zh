
## LISTING 7.1  DEBIAN OSS CONTROL SCRIPT

```sh
#!/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
SOUNDON=<path to your soundon>
SOUNDOFF=<path to your soundoff>
AUMIX=<path to your aumix> # remove if you don't use aumix
NAME=oss
DESC="OSS/Linux"

test -f $SOUNDON || exit 0
test -f $SOUNDOFF || exit 0

set -e

case "$1" in
  start)
    echo -n "Starting $DESC: "
    $SOUNDON
    $AUMIX # remove if you don't use aumix
    echo "$NAME."
    ;;
  stop)
    echo -n "Stopping $DESC: "
    $SOUNDOFF
    echo "$NAME."
    ;;
  restart|force-reload)
    $0 stop
    $0 start
    ;;
  *)
    N=/etc/init.d/$NAME
    echo "Usage: $N {start|stop}"
    exit 1
    ;;
esac

exit 0
```

Save this script as /etc/init.d/oss, and then run the following as root:

```sh
# chmod +x /etc/init.d/oss
# update-rc.d oss defaults 99
```

Note that the lines including AUMIX assume that you are also using aumix, described later in this chapter. If you don't use aumix, remove them.

If you ever need to unload the driver while the system is running, a companion program to soundon called soundoff takes care of this. Note that this does not need to be run before you shut your system down.

## CHANGING THE DEFAULT SOUND SETTINGS

One thing that is still bothersome about sound support on Linux is that it tends to default to rather loud settings. One method that people have employed to remedy this is to save settings in the aumix program and restore them when the sound driver is loaded. You must first establish that you have the aumix program installed, though. Running the following tells you whether you have it installed on RPM-based distributions:

`$ rpm -q aumix`

On Debian, use the following:

`$ dpkg -s aumix`

Check the status line for installed or not-installed. If it is not installed, install it.

After aumix is installed (and you are logged in as root), start it and set the controls as you want them to be every time you start your system. Then exit aumix and execute the following command:

`aumix -S`

This writes a file called .aumixrc in root’s home directory (/root). Copy this file to /etc/aumixrc. There must not be a period at the beginning of this file when it is copied to /etc. Then, in /etc/rc.d/rc.local add the following command after soundon:

`aumix -L`

This loads the settings in /etc/aumixrc non-interactively, causing your sound system to initialize with settings that are much more reasonable than the defaults.

## REALPLAYER

When it comes to streaming audio and video over networks such as the Internet, one company—RealNetworks—seems to have established the standard to which all others are compared. This is especially true on the Linux platform, where RealNetworks is currently the main show in town. Everything you need for streaming networked audio and video clients, servers, and encoders is offered for Linux.

The main attraction from RealNetworks is the RealPlayer client software. Using this, anyone with a Linux System that is connected to a network such as the Internet can receive and play audio and video served from a RealNetworks server. News, entertainment, radio broadcasts, education, and many other services are available. Best of all, it is currently available free of charge from RealNetworks.

> **Note**  
> To get a feel for what this technology can offer, browse some of the audio/video Web sites listed on the RealNetworks home Web page (http://www.real.com), or check the Live Concerts Web site (http://www.liveconcerts.com). There is bound to be something at one of these sites that interests you!

### GETTING AND INSTALLING REALPLAYER

You can get RealPlayer at the following location:

http://www.real.com

At the time of this writing, only the regular RealPlayer 7 Basic package is available for Linux. There is also currently no commercial (that is, one that costs money) version of RealPlayer for Linux.

It can be tricky to find the download page for RealPlayer 7 Basic. Most of the links will steer you toward their commercial product, RealPlayer 8 Plus. When you first arrive at the RealNetworks Web page, select the Download RealPlayer link at the top of the page, and then select RealPlayer 7 Basic near the bottom of the page. Finally, select Download RealPlayer for UNIX near the bottom of the screen. Fill out the presented form, selecting Linux 2.x (libc6 i386) RPM for RPM-based distributions, or Linux 2.x (libc6 i386) Self-Extracting for Debian. The Red Hat RPM will work fine for OpenLinux.

After downloading the RealPlayer package, install it with one of the following code snippets:

```sh
# rpm -i rp7_linux20_libc6_i386_cs1.rpm
# chmod u+x rp7_linux20_libc6_i386_cs1.bin
# ./rp7_linux20_libc6_i386_cs1.bin
```

Finally, fill out the short configuration dialogs presented, and RealPlayer will start up (as well as Netscape, taking you to their home page). Note that prompting for user input and automatically starting the application are unusual (and, many would say, inappropriate) for RPM packages.

> **Note**
> 
> The name of the file you download might be different from this. Just replace `linux20_libc6_i386_cs1.rpm` with the name of the file downloaded. Note also that instead of dots, these files have underscores in their names.
> 
> It is possible that you will need to add the option `-nodeps` or `--force` to install this RPM. RealPlayer sometimes builds its RPMs based too strongly on Red Hat systems. It should still work fine on eDesktop or other RPM-based systems.

### USING REALPLAYER

To launch RealPlayer, select RealPlayer 7 from the Application Launcher menu in KDE. If you are not using KDE, you can start RealPlayer by running `/usr/X11R6/bin/realplay`. The RealPlayer main screen is shown in Figure 7.1.

**Figure 7.1**  
Main RealPlayer window—audio and video.

![](img/c741b1b6b6eccaba2ad43454c979a7f8_168_0.png)

### The File Menu

The File menu in RealPlayer offers options that are similar to those on the file menus of Web browsers. Because most people start RealPlayer from a Web browser, this menu does not get very much traffic. But sometimes it is easier to open a RealPlayer URL manually than it is to browse to it. This is especially true when there is a RealPlayer audio/video file that you want to play sitting on your hard drive. For these situations, a File menu is available in the player software.

The following sections detail the options that are offered on this menu.

- **Open Location**  
  When you open an audio/video stream over a network, what is being opened is a location, not a file, even though the address to which you are pointing leads to a file on a remote site. You open an address that is similar to that of a Web page, and it is assumed that at the other end a RealPlayer stream is waiting to be transferred to your player. For this reason, remote audio streams must be opened with the Open Location option from the File menu.  
  If you choose this option, a window that is similar to Figure 7.2 appears.  
  **Figure 7.2**  
  The Open Location window.  
  ![](img/c741b1b6b6eccaba2ad43454c979a7f8_169_0.png)

  Only RealPlayer URLs are to be entered in this page (these are typically preceded with rtsp instead of http). Web browsers are not required for opening RealPlayer URLs.

- **Open File**  
  Contrary to what was described for the Open Location menu option, if you have a RealPlayer audio/video file that is actually sitting on your local machine and that you want to play, you open the file using the Open File option from the File menu. You do this because you are not accessing an audio/video stream residing on a remote site; the location is assumed to be on your own personal machine, so only the filename needs to be specified, or you can use the directory browser.

- **Past Locations**  
  The Past Locations numbered list contains links to your last four locations or files. This is very useful for quickly returning to a recently visited stream.

- **Exit**  
  This option terminates the RealPlayer session and exits.

### The Play Menu

This menu manages the normal playback functions of RealPlayer. These functions are similar to what you would use on a CD player or VCR.
