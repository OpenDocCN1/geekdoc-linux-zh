
+   • The sendmail file contains two variables: DAEMON and QUEUE. If the DAEMON variable is set to yes, the system starts sendmail in daemon mode (-bd) when the system boots. QUEUE tells sendmail how long to wait between queue runs (-q); the default is one hour.

## SUSE startup scripts

SUSE's startup system resembles that of Red Hat, at least in terms of its general organization. However, SUSE's scripts are well organized, robust, and well documented. The folks that maintain this part of the operating system get a gold star.

As in Red Hat, init invokes the script /etc/init.d/rc at each run level and provides the new run level as an argument. Package-specific scripts live in the /etc/init.d directory, and their configuration files live in /etc/sysconfig. An excellent introduction to the SUSE startup process can be found in /etc/init.d/README.

Although both SUSE and Red Hat concentrate their boot configuration files in /etc/sysconfig, the specific files within this directory are quite different. (For one thing, SUSE's files are generally well commented.) You invoke options by setting shell environment variables, and these variables are then referenced by the scripts within /etc/init.d. Some subsystems require more configuration than others, and those that need multiple configuration files have private subdirectories, such as the sysconfig/network directory.

The windowmanager file is a typical example from the sysconfig directory:

```
## Path:          Desktop/Window manager
## Type:          string(gnome,startkde,startkde3,startxfce4,twm)
## Default:       kde
## Config:        profiles,kde,susewm

# Here you can set the default window manager (kde, fvwm, ...)
# changes here require at least a re-login

DEFAULT_WM="gnome"

## Type:           yesno
## Default:        yes

# install the SuSE extension for new users
# (theme and additional functions)

INSTALL_DESKTOP_EXTENSIONS="yes"

## Path:           Desktop
## Description:    default mouse cursor theme
## Type:           string
## Default:

# Name of mouse cursor theme for X11. Possible themes can be found
# in /usr/share/icons/

X_MOUSE_CURSOR="DMZ"
KDE_USE_IPV6="yes"
```

Each variable is preceded by YaST-readable³ configuration information and a verbose description of the variable's purpose. For example, in the window manager file, the variable DEFAULT_WM sets the desktop window manager used by X.

SUSE also includes a chkconfig command for managing startup scripts. It's entirely different from the version provided by Red Hat, but it's an effective tool nonetheless and should be used in favor of manual script management.

## Ubuntu startup scripts and the Upstart daemon

Starting with Feisty Fawn in early 2007, Ubuntu replaced the traditional init with Upstart, an event-driven service management system that is also used by some other Linux distributions. Upstart handles transitions in system state—such as hardware changes—more elegantly than does init. It also significantly reduces boot times.

Upstart starts and stops services in response to system events such as the addition of a device or the disconnection of a network drive. For compatibility, it also emulates the traditional run levels of init. However, startup and shutdown scripts are processed in a manner that is somewhat different from that used by init.

Upstart uses job definition files in the /etc/event.d directory instead of an inittab file. A job is similar in concept to a startup script: it performs a series of commands and then returns control to Upstart. The collection of jobs on an Ubuntu system looks like this:

```
ubuntu$ ls /etc/event.d
control-alt-delete last-good-boot logd rc0 rc1 rc2 rc3 rc4 rc5 rc6
rc-default rc5 rc5-sulogin sulogin tty1 tty2 tty3 tty4 tty5 tty6
```

Over time, more startup scripts will be converted into native Upstart jobs. For now, Upstart uses run-level emulation scripts to boot the system. For example, the rc2 script executes /etc/rc2.d/rc, which runs all the startup scripts for run level 2.

Because of the need to maintain this compatibility, Ubuntu administrators should use Ubuntu's update-rc.d command to maintain links to startup scripts within the rc directories. The syntax is

```
update-rc.d service { start | stop } sequence runlevels .
```

update-rc.d accepts a sequence number (the order in which the startup script should be run) and the applicable run levels as arguments. Use a terminating dot to end parsing.

Services that start later in a run-level transition should stop sooner when the system exits that level. For example, if CUPS starts at a sequence value of 80 during boot, it should stop at a sequence value of around 20, early in the shutdown process. The update-rc.d command to add the appropriate links would be
