
# Part II

## Using CentOS

FIGURE 5-4

Select a program to run from the list in the Run Application window.

![](img/2f265415ceec72538dd3c78ffca75c10_233_0.png)

When you have found an application and figured out the options that you like, you can add it to a menu or a panel if your window manager supports those features. In that way, you can run a program exactly as you want, instead of the way it is given to you on a menu.

Here is a procedure to run X applications from a Terminal window:

1. Open a Terminal window from your desktop.

2. Type

```
$ echo $DISPLAY
```

The result should be something similar to the following:

```
:0.0
```

This indicates that the Terminal window will, by default, direct any X application you run from this window to display 0.0 on your local system. If you don't see a value when you type that command, type **export DISPLAY=**:0.0 to set the display value.

3. With the *xmmms* package installed, type the following command:

```
$ xmmms &
```

The *xmmms* program should appear on your desktop, ready to work with. If you do not have the xmmms command, use the command *yum install xmmms* to install the program. You should note the following:

- The *xmmms* command runs in the background of the Terminal window (&). This means that you can continue to use the Terminal window while *xmmms* is running.
- I encountered no errors running *xmmms* on this occasion. With other applications, however, text sometimes appeared in the Terminal window after the command was run.

The text may say that the command can't find certain information or that certain fonts or colors cannot be displayed. That information would have been lost if the command were run from a menu.

4. If you want to know what options are available, type:

```
$ xmus --help
```

Try it with a few options. For example, if you want to begin by playing a file and you have an Ogg Vorbis audio file named `file.ogg`, you could type:

```
$ xmus file.ogg
```

5. When you are ready to close the `xmus` window, you can either do so from the `xmus` box window by right-clicking on the `xmus` window and selecting **Exit**, or you can kill the process in the Terminal window. Type **jobs** to see the job number of the process. If it was job number 2, for example, you would type **kill %2** to kill the `xmus` program. If, instead, you want to continue running `xmus` in the background, press Ctrl+Z (to put it in the background) and **bg** (to continue running it in the background).

You should try running a few other X commands. A couple of old X commands you might try are `xeyes` or `xsclock`.

## Running Remote X Applications

X lets you start an application from anywhere on the network and have it show up on your X display. Instead of being limited by the size of your hard disk and the power of your CPU and RAM, you can draw on resources from any computer that gives you access to those resources.

Think about the possibilities. You can work with applications launched from any other computer that can run an X application — from a small PC to a supercomputer. Given the proper permission, you can work with files, printers, back-up devices, removable drives, other users, and any other resources on the remote computer as though you were on that computer.

With this power, however, comes responsibility. You need to protect the access to your display, especially in networks where the other machines and users are not known or trusted. For example, you wouldn't want to allow anyone to display a login screen on your display, encouraging you to inadvertently give some cracker your login and password.

Traditionally, to run remote X applications, you basically only need to know how to identify remote X displays and how to use whatever security measures are put in place to protect your network resources. Using `ssh` to launch X applications is even simpler and more secure than the traditional method. Those issues are described in the following sections.

### Traditional Method to Run Remote X Applications

If there is an X application installed on another computer on your network and you want to use it from your desktop, follow these steps:

1. Open permissions to your X server so that the remote application can use your display.
2. Identify your X server display to the application when it starts up.

When you run an X client on your local system, your local display is often identified as :0, which represents the first display on the local system. To identify that display to a remote system, however, you must add your computer’s hostname. For example, if your computer were named whatever, your display name would be:

```
whatever:0
```

> **TIP** In most cases, the hostname is the TCP/IP name. For the computers on your local network, the name may be in your `/etc/hosts` file, or it may be determined using the Domain Name System (DNS) service. You could also use a full domain name, such as `www.example.com`. X does support other types of transport, although transports other than TCP/IP aren’t used much anymore.

You will probably use the display name in this form most of the time you run a remote X application. In certain cases, however, the information may be different. If your computer had multiple X displays (keyboard, mouse, and monitor), you may have numbers other than :0 (:1, :2, etc.). It is also possible for one keyboard and mouse to be controlling more than one monitor, in which case you could add a screen number to the address, like this:

```
whatever:0.1
```

This address identifies the second screen (.1) on the first display (:0). The first screen is identified as .0 (which is the default because most displays only have one screen). Unless you have multiple physical screens, however, you can skip the screen identifier.

There are two ways to identify your display name to a remote X application:

- **DISPLAY Shell Variable** — The `DISPLAY` shell variable can be set to the system name and number identifying your display. After this is done, the output from any X application run from that shell will appear on the display indicated. For example, to set the `DISPLAY` variable to the first display on `whatever`, type one of the following:

```
export DISPLAY=whatever:0
```

or

```
setenv DISPLAY whatever:0
```

The first example shows how you would set the `DISPLAY` variable on a `bash` or `ksh` shell. The second example works for a `csh` shell.

- **`-display` Option** — Another way to identify a remote display is to add the `-display` option to the command line when you run the X application. This overrides the `DISPLAY` variable. For example, to open an `xterm` window on a remote system so that it appears on the first display on `whatever`, type the following:

```
xterm -display whatever:0
```

With this information, you should be able to run an X application from any computer that you can access from your local computer. The following sections describe how you may use this information to start a remote X application.

## Launching a Remote X Application

Suppose you want to run an application from a computer named remotel on your local area network (in your same domain). Your local computer is local, and the remote computer is remotel. The following steps show how to run an X application from remotel on your X display on local.

> **CAUTION**
> This procedure assumes that no special security procedures are implemented. It is the default situation and is designed for sharing applications among trusted computers (usually single-user workstations) on a local network. This method is inherently insecure and requires that you trust all users on computers to which you allow access. If you require a more secure method, refer to the section “Using SSH to Run Remote X Applications” later in this chapter.

You may need to enable your X server to support networked connections. To see if you need to enable networked connections, run the following command:

```
$ ps aux | grep Xorg
root    2141   0.0   2.1   54276   44972 tty1  Ss+   11:14   0:04 /usr/bin/Xorg :0
    -nr -verbose -auth /var/run/gdm/auth-for-gdm-09SKms/database vt1
    -nolisten tcp
erfcfj   6034   0.0   0.0     4212    724 pts/0   R+    12:21   0:00
grep Xorg
```

If you see -nolisten tcp in the Xorg command, you need to enable networked connections. To do so, edit the file /etc/gdm/custom.conf, if you are using the GNOME Display Manager. Look for the [security] section and disable the DisallowTCP option.

```
[security]
    DisallowTCP=false
```

After this, restart your system. Log in and check if the -nolisten tcp argument is still present:

```
$ ps aux | grep Xorg
root    2141   0.0   2.1   54276   44972 tty1  Ss+   12:04   0:04 /usr/bin/Xorg :0
    -nr -verbose -auth /var/run/gdm/auth-for-gdm-s2V27d/database vt1
erfcfj   4021   0.0   0.0     4212    724 pts/0   R+    13:49   0:00
grep Xorg
```

Once completed, follow these steps to enable remote applications to connect to your desktop.

1. Open a Terminal window on the local computer.
2. Allow access for the remote computer (e.g. remotel) to the local X Display by typing the following from the Terminal window:
