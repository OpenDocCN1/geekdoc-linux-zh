
## Running X Window Applications

Setting up and configuring the X Window System to your liking is the hard part. By comparison, using X to run applications is relatively easy. If you have used Microsoft Windows operating systems, you already know the most basic ways of running an application from a graphical desktop. X, however, provides a much more flexible environment for running native Linux applications.

> **CROSS-REFERENCE:** See Chapter 3 for information on setting up an X desktop.

### Starting applications from a menu

To run applications on your own desktop, most X window managers provide a menu, similar to the Microsoft Start menu, to display and select X applications. Applications are usually organized in categories. From the `GNOME` or `KDE` desktops in Fedora Core, open the red hat menu, select the category, and then select the application to run. Figure 5-1 shows an example of the Fedora Core Applications menu and the Sound & Video submenu.

![](img/b22364e57409c2481ba806e4e6b9309c_222_0.png)

Figure 5-1: Starting X applications from the Red Hat Menu.

### Starting applications from a Run Application window

Not all installed applications appear on the menus provided with your window manager. For running other applications, some window managers provide a window, similar to the Run Application window, that lets you type in the name of the program you want to run.

To access the Run Application window:

1. Open the Actions menu.
2. Click Run Application. The Run Application window appears.
3. Click Show List of Known Applications, click the program you want, and then click Run.

If the application you want isn't on the list, you can either type the command you want to run (along with any options) and click Run, or you can click Append File to browse through directories to select a program to run. If you are running a program that needs to run in a Terminal window, such as the vi command, click the Run in Terminal button before running the command. Figure 5-2 is an example of the Run Application window.

![](img/b22364e57409c2481ba806e4e6b9309c_223_0.png)

Figure 5-2: Select a program to run from the list in the Run Application window.

### Starting applications from a Terminal window

I often prefer to run an X application, at least for the first time, from a Terminal window. There are several reasons why I prefer a Terminal window to selecting an application from a menu or Run Application window:

- If there is a problem with the application, you see the error messages. Applications started from a menu or Run Application usually just fail silently.
- Applications from menus run with set options. If you want to change those options, you have to change the configuration file that set up the menu and make the changes there.
- If you want to try out a few different options with an application, a Terminal window is an easy way to start it, stop it, and change its options.

When you have found an application and figured out the options that you like, you can add it to a menu or a panel (if your window manager supports those features). In that way, you can run a program exactly as you want, instead of the way it is given to you on a menu.

Here is a procedure to run X applications from a Terminal window:

1. Open a Terminal window from your desktop (look for a Terminal icon on your Panel or a Terminal selection on a menu.)
2. Type

```
$ echo $DISPLAY
```

The result should be something similar to the following:

```
:0.0
```

This indicates that the Terminal window will, by default, direct any X application you run from this window to display 0.0 on your local system. (If you don’t see a value when you type that command, type **export DISPLAY=:0.0** to set the display value.)

3. Type the following command:

```
$ xcms &
```

The **xcms** program should appear on your desktop, ready to work with. You should note the following:

- The **xcms** command runs in the background of the Terminal window (\&). This means that you can continue to use the Terminal window while **xcms** is running.
- I encountered no errors running **xcms** on this occasion. With other applications, however, text sometimes appeared in the Terminal window after the command was run. The text may say that the command can’t find certain information or that certain fonts or colors cannot be displayed. That information would have been lost if the command were run from a menu.

4. If you want to know what options are available, type:

```
$ xcms --help
```

5. Try it with a few options. For example, if you want to begin by playing a file and you have a WAV audio file named **file.wav**, you could type:

```
$ xcms file.wav
```

6. When you are ready to close the **xcms** window, you can either do so from the **xcms** window (right-click on the **xcms** window and select **Exit**) or you can kill the process in the Terminal window. Type **jobs** to see the job number of the process. If it was job number 2, for example, you would type **kill \%2** to kill the **xcms** program.

You should try running a few other X commands. A couple of old X commands you might try are **xeyes** or **xcalc**.

### Running remote X applications

X lets you start an application from anywhere on the network and have it show up on your X display. Instead of being limited by the size of your hard disk and the power of your CPU and RAM, you can draw on resources from any computer that gives you access to those resources.

Think about the possibilities. You can work with applications launched from any other computer that can run an X application — from a small PC to a supercomputer. Given the proper permission, you can work with files, printers, backup devices, removable drives, other users, and any other resources on the remote computer as though you were on that computer.

With this power, however, comes responsibility. You need to protect the access to your display, especially in networks where the other machines and users are not known or trusted. For example, you wouldn’t want to allow anyone to display a login screen on your display, encouraging you to inadvertently give some cracker your login and password.

Traditionally, to run remote X applications, you basically only need to know how to identify remote X displays and how to use whatever security measures are put in place to protect your network resources. Using `ssh` to launch X applications is even simpler and more secure than the traditional method. Those issues are described in the following sections.

#### Traditional method to run remote X applications

If there is an X application installed on another computer on your network and you want to use it from your desktop, follow these steps:

- Open permissions to your X server so that the remote application can use your display.
- Identify your X server display to the application when it starts up.

When you run an X client on your local system, your local display is often identified as `:0`, which represents the first display on the local system. To identify that display to a remote system, however, you must add your computer’s host name. For example, if your computer were named *whatever*, your display name would be:

```
whatever:0
```

> **TIP:** In most cases, the host name is the TCP/IP name. For the computers on your local network, the name may be in your `/etc/hosts` file, or it may be determined using the Domain Name System (DNS) service. You could also use a full domain name, such as *hatbox.handsontext.com*. X does support other types of transport, although transports other than TCP/IP aren’t used much anymore.

You will probably use the display name in this form most of the time you run a remote X application. In certain cases, however, the information may be different. If your computer had multiple X displays (keyboard, mouse, and monitor), you may have numbers other than `.0` (`.1`, `.2`, and so on). It is also possible for one keyboard and mouse to be controlling more than one monitor, in which case you could add a screen number to the address, like this:

```
whatever:0.1
```

This address identifies the second screen (.1) on the first display (.0). The first screen is identified as .0 (which is the default because most displays only have one screen). Unless you have multiple physical screens, however, you can skip the screen identifier.
