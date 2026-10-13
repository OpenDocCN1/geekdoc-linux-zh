
The first line, `errorLogFile`, determines where xdm will output error messages. This is very important when trying to troubleshoot problems with xdm. Most distributions seem to be standardizing on `/var/log/xdm-error.log`.

The second line, `_0.setup`, determines what script xdm will run before providing a login prompt. This script generally does things such as provide an attractive background and perhaps a console window. The `_0` indicates that this configuration entry is for the primary display. On machines with multiple displays, you might have a `_1.setup` line as well, but this is very rare. Unless you are debugging problems with xdm itself, it is unlikely that you will need to investigate this script.

The third line, `session`, is probably the most important. This is the script that is run once a user logs in. This is also where different distributions most start to diverge. We’ll investigate Xsession more in following text.

## KDM

kdm is the KDE Display Manager and is almost identical to xdm in configuration. In fact, kdm is based directly on xdm’s source code. kdm provides some nice features such as faces (which show available user IDs on the system), multilingual support, and a more configurable appearance. All of these advanced configurations are managed by the Control Center. The dialog’s name is Login Manager, but its exact location seems to change with every minor update to KDE. Generally it should be found under Applications, System, or just System.

Because kdm uses xdm’s configuration files, it will also call `/etc/X11/xdm/Xsession` when a user logs in.

## GDM

gdm is the GNOME display manager, and is a complete rewrite of xdm, though it generally implements the same functions (as well as the added features of kdm).

The primary gdm configuration file is `/etc/X11/gdm/gdm.conf`. This location is fairly standard, but if you cannot find gdm.conf here, try this:

```shell
$ locate gdm.conf
```

gdm configuration is actually somewhat complicated, but the following lines from gdm.conf should point you in the right directions in understanding the startup sequence:

```text
LogDir=/var/gdm
DisplayInitDir=/etc/X11/gdm/Init
PreSessionScriptDir=/etc/X11/gdm/PreSession
SessionDir=/etc/X11/gdm/Sessions/
PostSessionScriptDir=/etc/X11/gdm/PostSession/
```

Notice that most of the variables end with Dir and point to directories rather than files. This is because gdm allows extremely configurable session types. A session is the sequence of events between when a user logs in and logs out. Each session type has a name and is selected with the Session menu on the login screen of gdm. If no session type is selected, then Default is used (this is also what is used if no special rules exist for a particular session type). So, for example, if you have chosen the GNOME session, gdm will first look for the file `/etc/X11/gdm/PreSession/GNOME` and then `/etc/X11/gdm/PreSession/Default`.

The LogDir directory is where gdm will store all of its logs. This is very important if you are debugging a problem with gdm.

The DisplayInitDir variable indicates where to look for scripts to run before presenting the user a login prompt. This is the same function as the Xsetup file for xdm. In fact, `/etc/X11/gdm/Init/Default` is often symbolically linked to `/etc/X11/xdm/Xsetup_0`. Although gdm is incredibly flexible in what it allows to be done, you will find that most distributions just have it point back to what xdm does.

The PreSessionScriptDir variable indicates where to look for scripts to run after the user has logged in, but while the system is still running as root. This generally points back to `/etc/X11/xdm/GiveConsole`, and is where the user is generally given ownership of the console.

The SessionDir variable indicates where to look for scripts to run as the user. This generally points back to `/etc/X11/xdm/Xsession`. Almost all display manager configurations eventually get back to Xsession, which we’ll cover next.

The PostSessionScriptDir variable indicates where to look for scripts to run after the user has logged out and after gdm is running as root again. This generally points back to `/etc/X11/xdm/TakeConsole`, which gives the console back to root.

## Xsession

Most distributions, after the user has logged in, will run `/etc/X11/xdm/Xsession`. Although most distributions call this file the same thing, they tend to differ wildly about what it does. The only way to know is to actually read it.

In general, Xsession is going to do the following things:

- **Redirect output to `${HOME}/.xsession-errors`** — Most distributions agree on this location, and it is an important source of information for debugging all kinds of problems. This file will catch the output of any application that doesn’t have a controlling terminal, so it is a good place to look for output from applications you launch through the panel or in other ways that don’t use a terminal.
- **Load resources** — Many older applications in the X Window System are configured with resources. Resources are explained in detail in “X Resources” (see Chapter 6, “Customizing X and Controlling X Resources”), but generally they are configuration options stored in memory by the X Window System and queried by various applications. Xsession generally includes a mechanism for loading user-specific resources from a file such as `${HOME}/.Xresources`. To verify the actual name, look for parts of Xsession that call `xrdb`.
- **Run user-defined script** — Generally, the user is allowed to create her own startup scripts. Some distributions will run `${HOME}/.xsession` if it is found. If not, they might try `${HOME}/.xclients`. Which user-defined scripts Xsession will honor is somewhat distribution specific, and you should check xsession itself to be sure. Some distributions will also skip this step if the user requested a specific session through kdm or gdm. In that case, xsession might just run the desktop or window manager directly.
- **Run Xclients** — The final fallback is almost always `/etc/X11/xinit/Xclients`. This script generally figures out what desktop or window manager the user wants (sometimes by querying distribution-specific configuration files), and starts it.

## Desktop or Window Manager Startup

The final startup step is generally an “exec” command that starts a desktop (KDE or GNOME for example) or a window manager (fvwm2 or Blackbox for example). The exec instructs the script to remove itself from memory before launching the desired environment. This not only saves memory, but also ensures that the rest of the script won’t be accidentally executed when the user logs out.

KDE starts with a script called `startkde`. This script launches the various servers that KDE needs for inter-process communication. It also starts the window manager, panel, and other useful applications.

GNOME starts with a script called `gnome-session`. This script does essentially the same things as `startkde`.

Window managers are generally started by simply running the window manager’s executable.

### Variation: `startx`

Your system does not have to be in runlevel 5 to start the X Window System. If XFree86 is not running, you can start it at any time using `startx`.

`startx` has a much simpler startup sequence than the display managers, but it is basically very similar.

After starting XFree86 itself, `startx` runs `/etc/X11/xinit/xinitrc`. This script is very similar to `xsession`, except that it will generally never start a desktop or window manager itself. It generally does not honor the user’s `$HOME/.xsession` script, but will generally honor `$HOME/.Xclients`. If the user does not have a `.Xclients`, then `xinitrc` will almost always run `/etc/X11/xinit/Xclients`, which will start a desktop or window manager.

### Troubleshooting

*When XFree86 starts up, text flashes on the screen, the monitor clicks and then repeats too fast to stop it.*

In almost all cases, this indicates an error in your XF86Config file when your system is at runlevel 5.

![](img/c741b1b6b6eccaba2ad43454c979a7f8_142_0.png)
