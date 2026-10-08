# Runlevels in initab

When your system starts up, it uses the default runlevel as specified in the default init entry in the **/etc/initab** file. For example, if your default init runlevel is 5 (the graphical login), the default init entry in the **/etc/initab** file would be

```
id:5:initdefault:
```

You can change the default runlevel by editing the **/etc/initab** file and changing the init default entry. Editing the **/etc/initab** file can be dangerous. You should do this with great care. As an example, if your default runlevel is 3 (command line), the entry for your default runlevel in the **/etc/initab** file should look like the following:

```
id:3:initdefault:
```

You can change the 3 to a 5, to change your default runlevel from the command line interface (3) to the graphical login (5). Change only this number and nothing else.

```
id:5:initdefault:
```

> **TIP** If your /etc/initab file becomes corrupted, you can reboot and enter linux single at the boot prompt to start up your system, bypassing the initab file. You can then edit the file to fix it.

# Changing Runlevels with telinit

No matter what runlevel you start in, you can change from one runlevel to another with the telinit command. If your default runlevel is 3, you power up in runlevel 3, but you can change to, say, runlevel 5 with telinit 5. The command telinit 0 shuts down your system. In the next example, the telinit command changes to runlevel 1, the administrative state:

```
# telinit 1
```

The telinit command is really a symbolic link (another name for a command) to the init command. The init command performs the actual startup operations and is automatically invoked when your system starts up. Though you could use init to change runlevels, it is best to use telinit. When invoked as telinit, init merely changes runlevels.

One use for telinit is to shutdown the X Windows server when installing the vendor graphics drivers. Open a terminal window and enter the following:

```
telinit 3
```

This starts the command line interface where you can login and run commands. Use the following to return to the X Windows desktop:

```
telinit 5
```

Should you want to use init, you would enter the init command and the runlevel number on a command line. If you were in runlevel 3 (command line), the following would place you in runlevel 5 (graphical interface):

```
init 5
```