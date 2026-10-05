
- Start an X-program on the remote server directing the display on your local screen, for example, you may start a window manager:

```
startkde -display local_machine_name:0.0 &
```

The symbol "&" puts the command in the background, so that your telnet window is still available to you.
The :0.0 means "display zero, screen 0", which is your first screen on the first display and makes sense since you have many concurrent sessions of X running on your computer with Linux.

You don't have to specify the "-display" option if your environment variable DISPLAY specifies the correct location on your current terminal, which is the case on my systems by default, but not on everybody else's as I am. You can check your DISPLAY setting using:

```
echo $DISPLAY
```

- After I finish my X session, I restore the access control to my X-server using:

```
xhost -name_of_the_remote_server
```

or

```
xhost
```

Example. This sequence of commands will run Netscape on the remote machine called marie, directing the display to the X-server with X-windows manager which runs on the local machine hacker:

```
startx
xhost marie
telnet marie
[login]
netscape -display hacker:0.0 &
[do my stuff]
[logout]
xhost -marie
```

In principle, you can run a program on any computer on the network, and display the output on any (not necessarily the one you are sitting at).

I use remote X-windowing a lot to run fat programs (kde, Word Perfect 8, and Netscape) on a slim machine (486-33, 8 MB mem) which would not be able to run those by itself. It is also a convenient and fast way to work with files on a remote system for which the nfs mount is not set up.

## 4.3.4 Can I have multiple sessions X running at the same time?

Yes, you can. When you issue the first startx command on your system, it opens the first X-session on the default display 0. The second X-session must be opened on a different display. For example, this will open a second X-session on the display 1:

```
startx -- :1
```

You can have up to 6 concurrent sessions. Use <Ctrl><Alt><F7> to switch to display 0, <Ctrl><Alt><F8> to second screen, etc. up to <Ctrl><Alt><F12>. Try startx if you need more info.

In a similar fashion, you can open another bare X-server session without a window manager. This will open one on display 2:

```
xinit -- :2
```

On this bare-bone X-display I can run a different window manager (so as to have two ones running at the same time) by typing in the X-terminal one of these:

```
fvwm2 (to run fwm2)
startkde (to run kde)
afterstep (to run afterstep)
fwm (to run fwm)
AnotherLevel (to run AnotherLevel)
gnome-session (to run Gnome)
```

Of course alternative window managers will run only if it is installed on your system. The above window managers are available on the RH5.2 CD for you to decide if you want them (with the exception of Gnome, which is not present on RH5.2 but the default on RedHat 6.0 and 6.1). I use almost exclusively KDE, although the other managers may be smaller and faster. Gnome is a famous X-windows project which is said to be more advanced and prettier than KDE, but it is still quite buggy, so perhaps not recommended unless you don't mind occasional trouble. RH6.0 and 6.1 contain both major X-windows systems, Gnome and KDE.

## 4.3.5 Can I have a GUI prompt?

To start up your X-server automatically at the start-up and display a graphical login prompt, you have to edit one character in the file /etc/inittab. This file specifies something like:

```
id:3:initdefault:
```

Change it to

```
id:5:initdefault:
```

This sets up the default runlevel to 5, which is X-Windows. The meaning of the different runlevels is explained in the same /etc/inittab file:

- 0 - halt (Do NOT set initdefault to this)
- 1 - Single user mode
- 2 - Multiuser, without NFS (The same as 3, if you do not have networking)
- 3 - Full multiuser mode
- 4 - unused
- 5 - X11
- 6 - reboot (Do NOT set initdefault to this)

You can change the runlevel from the command line with a command like this (as root):

```
init 6
```

which will reboot your computer.

## 4.4 Printer and soundcard

### 4.4.1 How to setup my soundcard?

Try to run (as root)

setup

The third button from the top ("sndconfig") sets up the sound card. Unless you have a fancy sound card, this will work for you. At the end of the setup, Linus says how he pronounces "Linux". ("sndconfig" can be also run directly from the command line--type sndconfig.)

You may want to try your soundcard and cdrom using a command line cdplayer. Put a music CD to your CDROM and type:

```
cdplay
```

If this does not work, maybe you don't have /dev/cdrom? Check if you can mount a CD as a root (look here [p 62]) and create the device /dev/cdrom by linking it to the appropriate drive (most likely /dev/hdb), for example:

```
ln -s /dev/hdb /dev/cdrom
```

If cdplay works for root, but does not work for a regular user, maybe you need to give (as root) everybody the permissions to read and write to the file /dev/cdrom:

```
chmod 666 /dev/cdrom
```

(The directory /dev is where all your devices play appear as files.)

Now, that you got hooked on cdplay, you can play third song, try:

```
cdplay 3
```

You can also use the command cdp for rudimentary command line interface to cdplay, but perhaps you prefer the interfaces available under X-windows (e.g., from KDE "K" menu, choose: Multimedia-/CD Player").

To stop the music either press the button on CDROM or issue one of these commands:

```
eject
cdplay stop
```

### 4.4.2 How do I setup my printer?

As root, start an X-windows session by typing

```
startx
```

Read here [p 74] if your X-windows is not set up properly.

Start an X-terminal (the "two-computer") button on your K-bar and type in it:

```
printtool
```

This program does a complete printer setup, you just have to fill up the information about your type of printer and where it is hooked up.

Specifying the proper printer port is the most important part. If you don't know which one is yours try:
on RedHat 5.2: lp1 (this is the first parallel port on RH5.2) or lp2 (this is the second parallel port on RH5.2) or lp3 (this is the third parallel port on RH5.2); on RedHat 6.0: lp0 (this is the first parallel port on RH6.0) or lp1 (this is the second parallel port on RH6.0) or lp2 (this is the third parallel port on RH6.0). After upgrading from RH5.2 to 6.0.

| Field | Description |
| :--- | :--- |
| \ | Field separator (separates the entries in the file). |
| \ | (at end of line) Continuation on the next line |
| lp | Name of the default lp is the name of the default printer on your machine. |
| sd=/var/spool/lpd/lp | My spool directory (sd). |
| mx#0 | Maximum size of print jobs (mx) in blocks. No limit. |
| sh | I want headers to be suppressed (sh). Header is the page with your name that prints before your job (waste of paper if you print at home). |
| rm=mars | Name of the remote machine (rm), which on my system is called "mars" (my printer is connected to a different computer). |
| rp=lp | Name of the remote printer (rp), which is the name of the printer on the remote machine "lp" on my system |
| or | The name of the device on the local machine. "/dev/lp0" is the first port on RH6.0 (it used to be /dev/lp0 on RH5.2). |
| lfilter=/var/spool/lpd/lfilter | Input filter (if). If your job will be formatted by this "filter" before it is sent to the printer. |
| sf | Suppress the form feed (sf) that is normally sent when printing is complete (use if your printer keeps an empty page at the end of each jobs). |

The printer is controlled using the command lpc (as root). Type "?" to see the options. This program is notorious for its peculiarities, so don't get discouraged easily. The printer queue can be viewed with lpcq and cleaned with lprrm,both of which work for a user (not only root). You can print from the command line using the command lpr.
