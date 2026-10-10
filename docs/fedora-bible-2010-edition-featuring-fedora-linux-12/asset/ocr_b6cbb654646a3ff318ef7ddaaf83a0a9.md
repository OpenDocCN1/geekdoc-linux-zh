such as choosing a *keymap* file, checking and mounting *root* and *proc* file systems, setting the clock and hostname, configuring *swap* space, cleaning up *temp* files, and loading modules. The seven following lines control the commands executed within each major run level. In each, the /etc/rc.d/rc script is called, using the desired run level as an argument. In turn, it descends into the *appropriate* directory tree (for example, the /etc/rc3.d directory is entered for run level 3).

The ctrl*altdel* action in the *inittab* file tells *init* to perform exactly what PC users would expect if the Ctrl, Alt, and Delete keys were pressed simultaneously. The system reboots itself in an orderly fashion (a switch to run level 6) after a three-second delay.

The next two lines (with their comments) deal with graceful shutdowns if you have an uninterruptible power supply (UPS) and software installed. The first line initiates a halt (a switch to run level 0) two minutes after receiving a signal from the UPS indicating a power failure. The second line cancels the shutdown in the event that power is restored.

The six *getty* lines start virtual consoles to allow logins. These processes are always running in any of the multiuser run levels. When someone connected to a virtual console logs out, that *getty* process dies, and then the *respawn* action tells *init* to start a new *getty* process. You can switch between virtual consoles by pressing Ctrl+Alt+F1, Ctrl+Alt+F2, and so on.

The last line indicates that as long as the system is in run level 5, the “preferred display manager” (*xdm*, *gnome*, *KDE*, and so on) will be running. This presents a graphical login prompt rather than the usual text-based login, and eliminates the need to run *startx* to start the GUI.

Starting with Fedora 10, the *inittab* file contains a simple one-line setting to define the default run level:

```
```text
id:5:in
default
```
```

This file specifies run level 5 as the default.

# # System Startup and Shutdown

During system startup, a series of scripts are run to start the services that you need. These include scripts to start network interfaces, mount directories, and monitor your system. Most of these scripts are run from subdirectories of /etc/rc.d. The program that starts most of these services when you boot and stops them when you shut down is the /etc/rc.d/rc script. The following sections describe run-level scripts and what you can do with them.

# ## Starting run-level scripts

As previously mentioned, the /etc/rc.d/rc script is integral to the concept of run levels. Any change of run level causes the script to be executed, with the new run level as an argument. Here’s a quick run-down of what the /etc/rc.d/rc script does:

+   - **Checks that run-level scripts are correct** — The rc script checks to find each run-level script that exists and excludes those that represent backup scripts left by rpm updates.