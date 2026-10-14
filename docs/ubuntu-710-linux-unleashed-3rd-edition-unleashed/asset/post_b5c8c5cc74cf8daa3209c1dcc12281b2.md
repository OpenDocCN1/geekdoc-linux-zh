
```
status)
    rhstatus
    ;;
condrestart)
    [ -f /var/lock/subsys/smb ] && restart || :
    ;;
*)
    echo $'Usage: $0 {start|stop|restart|status|condrestart}'
    exit 1
esac
```

Although the scripts can be used to customize the way that the system runs from power-on, absent the replacement of the kernel, this script approach also means that the system does not have to be halted in total to start, stop, upgrade, or install new services.

Note that not all scripts will use this approach, and that other messages might be passed to the service script, such as restart, reload, or status. Also, not all scripts will respond to the same set of messages (with the exception of start and stop, which they all have to accept by convention) because each service might require special commands.

After all the system scripts have been run, your system is configured and all the necessary system services have been started. If you are using a runlevel other than 5, the final act of the init process is to launch the user shell—bash, tcsh, zsh, or any of the many command shells available. The shell launches and you see a login prompt on the screen.

## Controlling Services at Boot with Administrative Tools

In the Services dialog (shown in Figure 11.1) Ubuntu lists all the services that you can have automatically start at boot time. They are usually all enabled by default, but you can simply uncheck the ones you don't want and click OK. It is not recommended that you disable services randomly "to make things go faster." Some services might be vital for the continuing operation of your computer, such as the graphical login manager and the system communication bus.

## Changing Runlevels

After making changes to system services and runlevels, you can use the telinit command to change runlevels on-the-fly on a running Ubuntu system. Changing runlevels this way allows system administrators to alter selected parts of a running system in order to make changes to the services or to put changes into effect that have already been made (such as reassignment of network addresses for a networking interface).

For example, a system administrator can quickly change the system to maintenance or single-user mode by using the telinit command with its S option like this:

```
# telinit S
```

![](img/7aaa8e4f2209bf9f2fb443905096e94c_254_0.png)

FIGURE 11.1 You can enable and disable Ubuntu's boot-up services by toggling the check-boxes in the Services dialog.

The telinit command uses the init command to change runlevels and shut down currently running services.

After booting to single-user mode, you can then return to multi-user mode, like this:

```
# telinit 2
```

> TIP
> Linux is full of shortcuts: If you exit the single-user shell by typing exit at the prompt, you will go back to the default runlevel without worrying about using telinit.

## Troubleshooting Runlevel Problems

Reordering or changing system services during a particular runlevel is rarely necessary when using Ubuntu unless some disaster occurs. But system administrators should have a basic understanding of how Linux boots and how services are controlled in order to perform troubleshooting or to diagnose problems. By using additional utilities such as the dmesg | less command to read kernel output after booting or by examining system logging with cat /var/log/messages | less, it is possible to gain a bit more detail about what is going on when faced with troublesome drivers or service failure.

To better understand how to troubleshoot service problems in Ubuntu, look at the diagnosis and resolution of a typical service-related issue.

In this example, X will not start: You don’t see a desktop displayed, nor does the computer seem to respond to keyboard input. The X server might either be hung in a loop, repeatedly failing, or might exit to a shell prompt with or without an error message.

The X server only attempts to restart itself in runlevel 2, so to determine whether the X server is hung in a loop, try switching to runlevel 1.

> **TIP**
> 
> If you are working on a multi-user system and might inadvertently interrupt the work of other users, ask them to save their current work; then change to a safer runlevel, such as single user mode.

Change to runlevel 1 by running the command `telinit 1`. This switch to runlevel 1 will stop the X server from attempting to restart itself.

Now you can easily examine the error and attempt to fix it.

First, try to start the X server “naked” (without also launching the window manager). If you are successful, you will get a gray screen with a large X in the middle. If so, kill X with the Ctrl+Alt+Backspace key combination, and look at your window manager configuration. (This configuration varies according to which window manager you have chosen.)

Let us assume that X won’t run “naked.” If we look at the log file for Xorg (it’s clearly identified in the /var/log directory), we’ll pay attention to any line that begins with (EE), the special error code. We can also examine the error log file, `.xsession-error`, in our home directory if such a file exists.

If we find an error line, the cause of the error might or might not be apparent to us. The nice thing about the Linux community is that it is very unlikely that you are the first person to experience that error. Enter the error message (or better, a unique part of it) into http://www.google.com/linux and discover what others have had to say about the problem. You might need to adjust your search to yield usable results, but that level of detail is beyond the scope of this chapter. Make adjustments and retest as before until you achieve success.

Fix the X configuration and start X with `startx`. Repeat as necessary.

> **CAUTION**
> 
> Before making any changes to any configuration file, always make a backup copy of the original, unmodified file. Our practice is to append the extension `.original` to the copy because that is a unique and unambiguous identifier.
> 
> If you need to restore the original configuration file, do not rename it, but copy it back to its original name.
