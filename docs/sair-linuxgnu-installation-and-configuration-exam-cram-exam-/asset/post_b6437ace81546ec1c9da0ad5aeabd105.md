
Type "linux single" at this prompt, and Linux automatically boots into single-user mode. You then have access to all Linux commands in superuser mode without having to log in to Linux.

> If you forget the password for the root or superuser, you can use this technique to delete the root password. Don't forget to set a new password once you've rebooted into Linux without the boot disk.

If you need your boot floppy to start Linux, review the technique discussed in the next section.

## Restoring Passwords with a Boot Floppy

One disaster that can happen with Linux is when nobody can log in to the computer. A common cause of this problem is a corrupt or deleted /etc/passwd file. A Linux boot floppy allows you to start Linux as the root user without requiring a login. Once you've mounted your hard drive, you can then restore the password file from a backup.

If you don't have a backup password file, you need to create a new version of this file. Every user on your system then has to log in again and set up passwords of their choice.

## Dynamic Library Modules

Dynamic libraries are a convenience for developers, because they allow the reuse of the same code, or programming instructions, for different commands. If you can't run some basic commands in your shell, you may have a problem with one or more dynamic library modules.

When you start Linux from the boot floppy, you gain access to some of these critical shell commands. You can then restore the appropriate dynamic library module from a different source, such as the Linux installation CD.

## Printer Problems

If you're having trouble printing, there are several steps that you can follow to troubleshoot your problems. These steps include checks on physical connections, logical connections, system logs, and configuration files. You can try to print again after each of these steps:

- 1. Always check physical connections first. In other words, check power to your printer as well as the cable that connects the printer to the computer. If your printer is located on another computer, check your network connections as well.
- 2. Check for error messages. If you have an error on a currently running print job, you'll be able to find an error message in the /var/spool/lpd/lp/status file. (You can review other errors in the lp system log file as defined in your version of /etc/syslog.conf.)

*Note: If you have more than one printer, each printer should have a different name. Substitute accordingly for lp in each of the following steps.*

- 3. If your physical connections work, check for a lock file. If you have a file like /var/spool/lpd/lp/lock, you can't print on the lp printer. If you don't currently have a running print job, delete this file. Lock files are temporary devices designed to keep more than one program from printing simultaneously.
- 4. If you don't have a lock file, check for a control file (cf) and a data file (df) in your /var/spool/lpd/lp directory. When you print a job, the request is sent to the spool directory associated with your printer. The line printer daemon (lpd) creates a cf with information on the print job and a df with the information to be printed.
- 5. If you don't have any of the files discussed in the previous steps, check the main printer configuration file, /etc/printcap. Make sure it still conforms to the parameters you need for your printer, as discussed in Chapter 9.
- 6. Check basic output to your printer. Run the lptest > /dev/lp command. (If your printer goes by a different name than lp, substitute accordingly.) The lptest command sends a generic "ripple test" pattern to your printer.
- 7. Check text output to your printer. Select a text file of your choice and send it to your printer device using the cat file > /dev/lp command. Substitute for file and lp accordingly.
- 8. If you have a serial port printer, check the devices linked to each serial port with the ls -l /dev/ttyS* command. Make sure your printer still has control of the appropriate serial device.
- 9. Check your environment variables with the env command. Make sure there are no environment variables, such as PRINTER, redirecting output to another file or printer.

## Other Problems

There are a number of other problems that you can solve fairly easily. You can address keyboard issues related to graphics, repeat rate, and the Num Lock key. You can synchronize your clock with a site on the Internet. You can also address memory problems, including those related to the X Window.

## Weird Characters

Before the development of graphics adapters, Unix used pseudographics mode to simulate simple pictures, such as lines and letters to illustrate the squares and pieces in a chess game. If you can't start the graphical user interface (GUI) from a CLI, you're sent to a strange mode where you see strange characters on a CLI screen. You can type the reset command to switch out of this graphics mode, or you can switch to another virtual console and kill the shell associated with the pseudographics mode console.

## Num Lock

By default, the numeric keypad is off when you install Linux. This is probably preferred if you're using a laptop computer without a dedicated numeric keypad. When you turn on the Num Lock key on a laptop, numbers supersede several letters on your keyboard.

On the other hand, many people use the numeric keypad on a standard keyboard. If you want the Num Lock key to be set on by default when you boot Linux, set up the following shell script, make it executable, and copy it to the /etc/rc.local or another /etc/rc.d directory associated with booting Linux:

```
for n in 1 2 3 4 5 6 7
 do
     setleds +num < /dev/tty$n > /dev/null
 done
```

This script activates the Num Lock key for all virtual terminals associated with the variable n, using the setleds utility.

## Keyboard Repeat Rate

When you press a character key on your keyboard and keep it pressed in a CLI, the character eventually repeats itself. The rate of repetition is known as the keyboard repeat rate. You can set this rate with some BIOS menus, or you can set it using the kbdrate command. For example, if you want to set a repeat rate of 20 characters per second, run the following command:

```
/sbin/kbdrate -r 20
```

## Synchronizing Time

The time reported on your computer may not be accurate. Some BIOS clocks run fast. Alternately, if the battery associated with your BIOS does not have enough power, your BIOS clock may be slow.

If you're running several computers on a network, you may have applications where it's important that all of your computers have the same clock time. The TCP/IP protocol suite includes a Network Time Protocol (NTP), which allows you to synchronize the time on all of your computers. For example, if you want to synchronize with the time server at the Internet Software Consortium (ISC), run the following command:

```
ntpdate clock.isc.org
```

Other "official" NTP time servers are available worldwide. For more information, refer to the time WWW server Web page at www.eecis.udel.edu/~ntp, sponsored by the University of Delaware.

## X Window Thrashing

When you don't have enough RAM, your computer spends a lot of time exchanging information between RAM and the swap partition on your hard drive. (The swap partition is your virtual memory, which extends the amount of "RAM" available to Linux.) This phenomenon is also known as thrashing, which characterizes constant activity on a hard drive.

One common cause of thrashing is the demands of the X Window. If everything slows down when you start the X Window, you probably have a memory problem and should follow the guidelines discussed in Chapter 3 for RAM requirements.

## Problem Opening the X Window

If you try to open the X Window and Linux doesn't bring you into the GUI, you may receive an error message like the following:

```
cannot open display:0.0
```

In this case, you need to configure the DISPLAY variable. DISPLAY can be either an environment variable or a shell variable. DISPLAY is an environment variable if you see it in the output to the env command; it is a shell variable if you see it in the /etc/profile configuration file. If DISPLAY is an environment variable, you need to set it. If it is a shell variable, you should export it so it works with other shells.

In either case, you need to set this variable to localhost:0.0, which sets up the local computer to work locally or with remote clients. You can set DISPLAY to this value with the following command:

```
DISPLAY=localhost:0.0
```
