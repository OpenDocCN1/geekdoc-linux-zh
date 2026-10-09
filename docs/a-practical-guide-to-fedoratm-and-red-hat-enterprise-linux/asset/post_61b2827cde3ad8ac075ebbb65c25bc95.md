
these filesystems, repairing them as needed. Make note of any ordinary files or directories that you repair (and can identify), and inform their owners that these files might not be complete or correct. Look in the lost+found directory (page 502) in each filesystem for missing files. After successfully running fsck, if the system entered single-user mode automatically, type exit to exit from the single-user shell and resume booting the system; otherwise, give a reboot command.

## Back up a badly damaged filesystem before running fsck on it

When a filesystem is badly broken, fsck sometimes makes the situation worse while trying to repair it. In these cases, it might be possible to recover more data by copying the readable data from the broken filesystem before attempting to repair it. When a damaged filesystem holds important data, use dd (dd man page) to make a full binary backup of an unmounted filesystem before attempting to repair it using fsck.

If files are not correct or are missing altogether, you might have to re-create them from a backup copy of the filesystem. For more information refer to “Backing Up Files” on page 602.

## REINSTALLING THE MBR

To reinstall the MBR, as is necessary when it gets overwritten by a Windows installation, boot the system from an Install or Network Image and select Troubleshooting -> Rescue a Fedora system. Then mount the system image as described in “Rescue an Installed System” below and run grub2-mkconfig (page 593) to regenerate the grub.cfg file and grub2-install (page 594) to install it on the appropriate device:

```
# chroot /mnt/sysimage
# grub2-mkconfig -o /boot/grub2/grub.cfg
# grub2-install /dev/sda
```

Exit from the rescue shell and reboot the system.

## WHEN THE SYSTEM DOES NOT BOOT

When a system will not boot from the hard disk, boot the system to rescue an installed system (next) or single-user/rescue mode (page 450). If the system comes up, run fsck (page 525) on the root filesystem on the hard disk and try booting from the hard disk again. If the system still does not boot, you might have to regenerate the grub.cfg file and reinstall the master boot record (previous).

## RESCUE AN INSTALLED SYSTEM

When you rescue an installed system you can fix a system that does not boot normally: You can change or replace configuration files, check and repair partitions using fsck (page 525), rewrite boot information, and more. To rescue an installed system, boot the system from an Install or Network Image and select Troubleshooting from the Image Boot menu (Figure 3-4, page 61) and Rescue a Fedora system from the Troubleshooting menu (Figure 3-5, page 61). When the system comes up it displays the pseudographical Rescue screen (Figure 10-3).

![](img/243613168ac865b539f12460d966088e_513_0.png)
Figure 10-3 The Rescue screen

This screen gives you the choice between having the system look for and mount an existing Linux installation, and simply displaying a shell prompt. Because it is not a true graphical screen, the mouse does not work on the Rescue screen. Use **TAB** to move the highlight between buttons and **SPACE** to select the highlighted button.

Select **Continue** or **Read-Only** to have the system search for an existing system; select **Skip** to not have it search. If you have the system search and it finds an existing system, **Continue** then mounts the system in read-write mode; **Read-Only** mounts it read-only. If the mount is successful, the next two screens tell you that the existing system was mounted under `/mnt/sysimage`. Select **OK** two times. The next screen allows you to start a shell, run a diagnostic, or reboot. Use the ARROW keys to highlight **Start shell** and press **RETURN**.

With the existing installation mounted, once the system displays a shell prompt (similar to `bash-4.2#`), you can give the command **chroot /mnt/sysimage** to access the existing installation as it would be if you had booted normally, with the existing installation’s root directory available as / (root). See page 487 for more information on **chroot**. At this point you can reinstall the MBR if necessary (previous page). If you choose not to mount the existing installation, you are running a rescue system with standard tools mounted in standard locations (`/usr/bin`, `/usr/sbin`, and so on). You can fix or mount partitions from the local installation. When you exit from the rescue shell, you can reboot the system. Remove the installation medium if you want to boot from the hard drive.

### AVOIDING A TROJAN HORSE

A *Trojan horse* is a program, usually embedded in or masquerading as another program. The program does something destructive and/or disruptive to a system while appearing to be benign. Because of the way it is disguised, a user typically runs it without realizing what it is doing. As an example, you could store the following script in an executable file named `mkfds`:

```
while true
do
    echo 'Good Morning Mr. Jones. How are you? Ha Ha Ha.' /dev/console
done
```

If you are working with **root** privileges when you run this command, it will continuously write a message to the console. If the programmer were malicious, it could do worse. The only thing missing in this plot is **access permissions**.

A malicious user could implement this Trojan horse by changing **root's** **PATH** variable to include a publicly writable directory at the start of the **PATH** string. (The catch is that you need to be able to write to `/etc/profile` or `/root/.bash_profile`—where the **PATH** variable is set for **root**—and only a user working with **root** privileges can do that.) Then you would need to put the bogus `mkfds` program file in that directory. Because the fraudulent version appears in a directory mentioned earlier than the real one in **PATH**, the shell would run it rather than the real version. Thus, the next time a user working with **root** privileges tries to run `mkfds`, the fraudulent version would run.

Trojan horses that lie in wait for and take advantage of the misspellings most people make are among the most insidious types. For example, you might type `sl` instead of `ls`. Because you do not regularly execute a utility named `sl` and you might not remember typing the command `sl`, it is more difficult to track down this type of Trojan horse than one that takes the name of a more familiar utility.

A good way to help prevent the execution of a Trojan horse is to make sure your **PATH** variable does not contain a single colon (`:`) at the beginning or end of the **PATH** string or a period (.) or double colon (`::`) anywhere in the **PATH** string. This precaution helps ensure that you will not execute a file in the working directory by accident.

To check for a possible Trojan horse, examine the filesystem periodically for files with `setuid` (page 196) permission. The following command lists these files:

![](img/243613168ac865b539f12460d966088e_514_0.png)

- `find / -perm /4000 -exec ls -lh {} \; 2> /dev/null`
    - `-rwsr-xr-x. 1 root root 53K Jun 11 11:48 /usr/bin/crontab`
    - `-rwsr-xr-x. 1 root root 32K Jun 13 02:48 /usr/bin/su`
    - `-rwsr-xr-x. 1 root root 23K May 29 07:52 /usr/bin/pkexec`
    - `-rwsr-xr-x. 1 root root 28K Jun 21 17:51 /usr/bin/passwd`
    - `-rwsr-xr-x. 1 root root 24K Jun 13 02:48 /usr/bin/chsh`
    - `---S-x-x-x. 1 root root 124K Feb 28 04:55 /usr/bin/sudo`
    - `-rwsr-xr-x. 1 root root 44K Jun 13 02:48 /usr/bin/mount`
    - `-rwsr-xr-x. 1 root root 37K Mar 19 12:59 /usr/bin/newgrp`
    - `-rwsr-xr-x. 1 root root 77K Mar 19 12:59 /usr/bin/gpasswd`
    - ...

This command uses *find* (page 229) to locate all files that have their setuid bit set (mode 4000). The slash preceding the mode causes *find* to report on any file that has this bit set, regardless of how the other bits are set. The output sent to standard error is redirected to */dev/null* so it does not clutter the screen.

- Listing setgid files

You can display all files with setgid permission (page 196) by substituting 2000 for 4000 in the preceding command.

- Run software only from sources you trust.

Another way a Trojan horse can enter a system is via a tainted *~/.bashrc* (page 502) file. A bogus *sudo* command or alias in this file can capture a user's password, which might then be used to gain *root* privileges. Because a user has write permission to this file, any program the user executes can easily modify it. The best way to prevent this type of Trojan horse from entering a system is to run software only from sources you trust.

You can set up a program, such as AIDE (Advanced Intrusion Detection Environment; *aide* package), that will take a snapshot of the system and periodically check files for changes. For more information see aide.sourceforge.net.

## X Window System

When you start an X Window System (graphical) session, you set up a *client/server environment*. One process, called the *X server*, displays a desktop and windows under *X*. Each application program and utility that makes a request of the *X server* is a *client* of that server. Examples of *X clients* include *xterm*, *CompiX*, *gnome-calculator*, and such general applications as word processing and spreadsheet programs. A typical request from a client is to display an image or open a window.

### The roles of X client and server might be counterintuitive

> The terms *client* and *server*, when referring to *X*, have the opposite meanings of how you might think of them intuitively: The server runs the mouse, keyboard, and display; the application program is the *client*.

This disparity becomes even more apparent when you run an application program on a remote system. You might think of the system running the program as the server and the system providing the display as the client, but in fact it is the other way around. With *X*, the system providing the display is the server, and the system running the program is the client.

- Events

The server also monitors keyboard and mouse actions (*events*) and passes them to the appropriate client. For example, when you click the border of a window, the server sends this event to the window manager (client). Characters you type into a terminal emulation window are sent to that terminal emulator (client). The client takes appropriate action when it receives an event-for example, making a window active or displaying the typed characters on the server.

Separating the physical control of the display (the server) from the processes needing access to the display (the client) makes it possible to run the server on one computer and the client on another computer. Most of the time, this book discusses running the *X server* and client applications on a single system. “Remote Computing and Local Displays” on the next page describes using *X* in a distributed environment.
