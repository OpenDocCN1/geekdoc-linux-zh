
20. The following command copies all files with the `.doc` extension from a DOS floppy to the current directory on the hard disk:

    `mcopy "a:\*\*.doc"`

## **Saturday Evening Review Answers**

1. You can customize the look and feel of the GNOME desktop by using the **GNOME Control Center**.

2. Sawfish is a window manager. It is the default window manager in GNOME. To configure Sawfish, select **Desktop** `↔` **Window Manager** from the **GNOME Control Center** menu.

3. To change the default desktop from GNOME to KDE, select the **Main menu** `↔` **System** `↔` **Desktop Switching Tool**, and then select **KDE** as the desktop. To change the default desktop back to GNOME from KDE, use the same desktop switching tool.

4. Use the **KDE Control Center** to customize various aspects of the KDE desktop. You can customize the background, the window manager, or select a theme for the user interface (UI).

5. To select and try out a screensaver from the GNOME desktop, start the **GNOME Control Center** by clicking on the toolbox icon on the **GNOME Panel**, and then select **Desktop** `↔` **Screensaver** from the Tree menu in the **Control Center**.

6. Select **K** `↔` **KDE Control Center**. Then select **Desktop** `↔` **Screensaver** from the Tree menu in the **KDE Control Center**. From there you can select and configure a screen saver.

7. To play the GNOME games, select **Main Menu** `↔` **Programs** `↔` **Games** while using the GNOME desktop. AisleRioit, Gnome-Stones, and GNOME Mahjongg are some games in GNOME. AisleRioit is a card-playing program that can play 30 different card games, including well-known ones, such as Freecell and Klondike.

8. Minesweeper, Patience, and Shisen-Sho are some games in KDE. To use them, select **K** `↔` **Games** while using the KDE desktop.

9. Select **Main Menu** `↔` **KDE Menus** `↔` **Games**.

10. Use `/usr/sbin/sndconfig` to start the sound card configuration program, and then follow the program’s prompts to configure the sound card.

11. To play audio CDs in Red Hat Linux, you can use `xmcd` or the GNOME or KDE CD players.

12. To allow a normal user to play audio CDs, log in as root and type `chmod 666 /dev/cdrom`.

13. CDDB is a CD database on the Internet. The GNOME CD player gets the song titles from CDDB if your Red Hat Linux system has an active Internet connection.

14. The GIMP and Xpaint are two image manipulation programs that come with Red Hat Linux. The GIMP is a program for viewing images and performing tasks such as photo retouching, image composition, and image creation. Xpaint is a bitmap painting program patterned after MacPaint.

15. Ghostscript is a nearly complete implementation of the PostScript language that enables you to print PostScript documents on many non-PostScript devices.

16. The name of the spreadsheet application is Gnumeric. Gnumeric’s default file format is XML (eXtensible Markup Language). Gnumeric can exchange files with Microsoft Excel.

17. You would use the command `aspell check report.txt` to check the spelling of a text file named `report.txt`.

18. The Red Hat Network is a system management tool consisting of Software Manager. Software Manager provides several services, including a software update subscription service, automatic RPM updates, and e-mail notification of bugs and security alerts.

19. First, you must create a system profile, and then register it with the Red Hat Network by sending the file to Red Hat. Next, you have to log in to the Red Hat Network and activate your Software Manager subscription.

20. Log in as root, and select Main Menu `↔` Programs `↔` System `↔` Update Agent from the GNOME desktop. Then select the updates, if any are available, that you wish to install on your system. Start the download and installation process by following Update Agent’s prompts.

## Sunday Morning Review Answers

1. The X server is a process that manages a bitmapped display, a keyboard, and a mouse. The X server controls the monitor, the keyboard, and the mouse on behalf of X clients requesting some sort of input or output activity using those devices, such as a request to open a window.

2. The X configuration file is `/etc/X11/XF86Config-4`. You can use `xf86config`, `X86cfg`, or `Kconfigurator` to create a new X configuration file.

3. The X graphical screen is partially working, press `Ctrl+Alt+F1` to switch to the text console and log in as root at the text login prompt. Then type `telinit 3` to kill the running X server. Next, create a new X configuration file, and type `telinit 5` to restart the graphical display manager. Finally, type `Ctrl+Alt+Backspace` to kill the X server and run it to restart with the new configuration file.

4. The init runs all other processes on the system. It starts at boot time and is primarily responsible for starting system daemons that provide essential services, and mounting file systems. The contents of `/etc/inittab` file control init’s behavior.

5. Look for the line with the keyword `initdefault` in the third field of `/etc/inittab` file; the fields are separated by colons (:). The second field of this line specifies the default run level.

6. The init process runs the `/etc/rc.d/rc.sysinit` script. This script, in turn, runs many other scripts from the subdirectories in `/etc/rc.d`, especially `/etc/rc.d/init.d`.

7. RPM refers to the Red Hat Package Manager, a system for packaging all the necessary files for a software product into a single file known as an RPM file, or simply an RPM. Red Hat Linux and the bundled applications are distributed in the form of a large number of RPMs.

8. To see if a specific RPM is installed on your system, type the command `rpm -q package_name` where `package_name` is the name of the RPM. For example, to see if the `samba` RPM is installed, type `rpm -q samba`.

9. Assuming that the RPM is in the current working directory, type the command `rpm -ivh fortune-mod-1.3.4-59.i386.rpm`.

10. Use the `rpm -e <package>` command or `GnoRPM`, the GNOME graphical RPM tool, to remove an installed RPM.

11. A few reasons to rebuild the Linux kernel are to bring the compiled version up to date after patching the kernel sources, to add SCSI support directly into the kernel, and to add support for hardware that was unsupported when you originally installed Red Hat Linux.

12. First, install the kernel source code. Next, configure the kernel, compile the kernel, compile the modules, and install the modules and kernel and a few other files.

13. Use the `at` command to submit commands to be executed at a future time. In some cases, the `crontab` facility can be used to run programs automatically at regular intervals.

14. Use `cron` and the `crontab` command to schedule jobs to run at regular intervals.

15. The `30 23 * * * $HOME/backup.sh` command schedules a job named `$HOME/backup.sh` to run every night of the week at 11:30 p.m.

16. The `/etc/cron.allow` file lists the names of the users who are allowed to use `cron`. `/etc/cron.deny` lists users forbidden to use `cron`.

17. You can back up files to floppy disks, Zip disks, and SCSI tape drives.

18. To use the `tar` utility to back up the `/home` file system to a SCSI tape drive, you can type: `tar cvf /dev/st0 /home`

19. To back up several large files in the `/home/share` directory onto multiple floppies, use `tar`’s `-M` option, which creates multi-volume archives, as shown in the following command: `tar -cMvf /dev/fd0 /home/share`

20. To store multiple backup archives on a single tape, use a non-rewinding tape device with a command such as `tar cvf /dev/nst0 /home` and use similar `tar` commands to create one archive after another. Rewind the tape with the following command: `mt -f /dev/nst0 rewind`. Skip over an archive with the following command: `mt -f /dev/nst0 fsf 1`

## Sunday Afternoon Review Answers

1. Many open source software packages are distributed in source code form without any executable binaries. Before you can use such software, you have to build the executable binary files. That’s why it’s important to learn how to build software from source files.

2. Open source software is typically distributed in compressed tar archives, also known as compressed tarballs. You can download the file using anonymous FTP or through a Web browser. To unpack it, use a command of the form `tar zxvf tarball_name` where `tarball_name` is the name of the file you downloaded.

3. After downloading and unpacking the source files, look for files with the names resembling `README` or `INSTALL` for instructions on how to build and install the software.

4. First download the file using anonymous FTP. Then use the `tar zxvf` command to unpack the file. Next, check the `README` or `INSTALL` files, if any, for instructions. In most cases, type `./configure` to configure the software; `make` to build the software; and `make install` to install it.

5. The `Xmms` package is the X Multimedia System, a graphical X application for playing MP3 and other multimedia files. Build and install `Xmms` with the command `./configure; make; make install`.

6. Look for information such as CPU usage, physical memory and swap space usage, and hard disk usage to monitor your system’s performance.

7. Red Hat Linux includes tools such as the `Gnome System Monitor`, and the `top` and `vmstat` commands to monitor system performance.

8. The **system load average** is the average number of processes that were ready to run in the last 1, 5, and 15 minutes.

9. The `vmstat 60 10` command line displays 60-second averages and prints a total of 10 lines of output. The first line of output from `vmstat` shows the averages since the last reboot.

10. The purpose of `/proc` is to allow users to access information about the Linux kernel and the processes that are currently running on the system.

11. The **security policy** provides the rules you use when setting up your Red Hat Linux system’s security. The security policy should address areas such as how users are authenticated, what various users can do, what data must be protected, which Internet services are allowed to run, and who is responsible for maintaining and auditing security.

12. The general steps are to install only those packages that you need, create user accounts with strong passwords, enable only the necessary Internet services, and periodically check log files for signs of break-in attempts. You should also keep up with security news and install upgrades from Red Hat.

13. Shadow passwords and the use of MD5 encryption are two ways in which passwords are made more secure in Red Hat Linux.

14. The `chage -M 30 marys` command line forces the user named *marys* to change her password every 30 days.
