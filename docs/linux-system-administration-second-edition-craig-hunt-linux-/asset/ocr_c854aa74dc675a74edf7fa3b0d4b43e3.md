| 6 | Signals the system to reboot itself. Again, do not set INITDEFAULT to this. |
| --- | --- |
| Note | The meaning of run levels between 2 and 5 is somewhat arbitrary. Although most distributions use the conventions outlined here, not all do. For example, SuSE uses run level 2 as a full multiuser mode with networking, and starts X with run level 3 rather than 5. |

In the first uncommented line, the init program is told what run level to use after a reboot. The line looks like this:

```
```code
id:3:initdefault:
```
```

The first part of this line, id, simply represents the word initdefault. The number 3 indicates that the system should start in run level 3 by default. For a system that uses the X Window System graphical environment (discussed in Chapter 13), you would instead use this command:

```
```code
id:5:initdefault:
```
```

Keep in mind that specifying an initial run level of 5 will cause an inability to log in if X has a problem that prevents it from starting. Typically, you'll see one of two things happen: Either the screen will repeatedly clear as the system tries to start X, fails, tries again, and so on; or the system will try to start X once, fail, and drop back to run level 3.

Following the run level line, the next uncommented line in Red Hat's initab file tells the init program which script to start:

```
```code
si::sysinit:/etc/rc.d/rc.sysinit
```
```

Here we've chosen to run the rc.sysinit script, which we'll look at in detail in a moment. Since the second colon-delimited field, the run level field, is empty, this script will run at boot time for all run levels. The rest of the line, /etc/rc.d/rc.sysinit, is the exact command to run.

The rc.sysinit script performs many functions. These include:

+   - Setting the path and the hostname, and checking whether networking is activated
- Mounting the /proc filesystem
- Setting the kernel parameters
- Setting the system clock
- Loading keymaps and fonts
- Starting swapping
- Initializing the USB controller (if present) along with its attached devices
- Checking the root filesystem, if required
- Setting up PPP
- Remounting the root filesystem as read-write
- Loading modules as appropriate

After the rc.sysinit file exits, the initab starts the /etc/rc.d/rc script with the appropriate run level as an argument. The rc script then executes all of the scripts pointed to by the symbolic links contained in the directory for that run level. If the run level is 3, for example, the scripts pointed to by the links in /etc/rc.d/rc3.d are run. Listing 3.4 shows this directory for a default Red Hat 7.3 installation.

Listing 3.4: The /etc/rc.d/rc3.d File Contains Links to the Scripts for Run Level 3.

| K01kdrcroot | K20rwhod | K74ypxfrd | S13portmap | S85gpm | 
| --- | --- | --- | --- | --- | 
| K05atd | K25squit | K75netfs | S17keytable | S90crond |