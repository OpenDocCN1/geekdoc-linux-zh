
Another method of running the program is to type its absolute path. If browser is located in /home/keir, for example, it could be run by typing /home/keir/browser.

## Useful everyday commands

Table 5-1 lists typical commands that are commonly used day-to-day in Ubuntu, along with popular command options. It's only a brief list, and emphasis is placed on file manipulation commands.

Software management commands are not included—those are listed separately in Chapter 6.

Table 5-1. Useful day-to-day commands.

| Command | Description |
|---|---|
| ls | List files and folders.<br>Typical example: ls -l<br>- l : Long listing (show permissions, ownerships etc.)<br>- a : Show all files, including hidden files<br>- h : Show KB, MB etc., rather than bytes |
| cd | Change folder. Type cd .. to change to parent folder.<br>Typical example: cd Documents |
| cp | Copy file or folder; first specify file (and path if necessary), then specify destination.<br>Typical example: cp myfile.doc Desktop/<br>- r : Copy folders too, including contents (otherwise folders will be ignored) |
| mv | Move file or folder; can also be used to rename files/folders if a new destination isn't specified. Note that, unlike cp, it is not necessary to specify the -r option in order to move folders.<br>Typical example: (moving) mv myfile.doc Desktop/<br>Typical example: (renaming) mv old.doc new.doc |
| rm | Delete file(s) or folder(s); multiple files/folders can be specified.<br>Typical example: rm -rf myfolder<br>- r : Delete folder; must be used if a folder is to be deleted<br>- f : Force deletion; don't prompt user for confirmation when deleting (useful when deleting lots of folders, but must be used with care) |
| ln | Create a link to a file (similar to a shortcut under Windows); first specify the file (including path if necessary), and then the location where the link should be created. A different filename may be specified for the new link.<br>*Typical example:* `ln -s myfile.doc ~/Desktop/`<br>`-s` : Create symbolic link, rather than hard link. In nearly all situations, a symbolic link is preferable, making this practically a prerequisite command option |
| less | Open specified plain text file in a viewer (use cursor keys to scroll; hit Q to quit). Useful for viewing configuration files.<br>*Typical example:* `less myfile.txt` |
| df | Show amount of free disk space on all attached filesystems.<br>*Typical example:* `df -h`<br>`-h` : Show KB, MB, GB etc. rather than bytes |
| free | Show amount of free memory.<br>*Typical example:* `free -mt`<br>`-m` : Show output in megabytes, rather than kilobytes<br>`-g` : Show output in gigabytes<br>`-t` : Show totals column |
| grep | Search through specified file for a word or phrase. First, specify the phrase, and then the file to be searched through.<br>*Typical example:* `grep -i wireless myfile.txt`<br>`-i` : Ignore upper/lowercase when searching |
| man | View the manual (man) page for specified command. A man page is built-in technical documentation—see Appendix B.<br>*Typical example:* `man ls` |
| nano | Simple text editor that's ideal for creating, editing or viewing files (particularly configuration files); hit Ctrl+J to re-justify current line should you create a line-break during editing.<br>*Typical example:* `sudo nano /etc/fstab` |
| umount | Unmount attached storage device. Not a typo! The command is `umount` and not `unmount`. Needs root powers. Specify the mount point.<br>*Typical example:* `sudo umount /media/cdrom` |
| locate | Find specified file; relies on a background database that is periodically and automatically updated. The database can be manually updated by typing the `sudo updatedb` command.<br>*Typical example:* `locate filename.doc`<br>`-i` : Ignore upper/lowercase when searching |

## Working with root powers

It's generally discouraged under Ubuntu to log in as the root user. Therefore, administrative tasks are carried out by ordinary users who "borrow" the root user's powers.

### Using sudo

At the command-line, you can force a command to run with root powers by preceding it with sudo (short for super-user do). For example, to install software using the dpkg command (discussed in Chapter 6), root powers are needed, so to use dpkg you would type something similar to the following:

- sudo dpkg -i package.deb

You'll be prompted for your password. Once this is entered, the command will complete.

If you run a graphical application from the command-line it's necessary to precede it with gksu instead of sudo. To most intents and purposes, gksu is identical to sudo. For example, to start the Synaptic software installation application, you would type gksu synaptic.

> NOTE If you're using Kubuntu, the kdesu command is used instead of gksu. It's identical in function to gksu. Under Xubuntu the gksu command is used, as with the main Ubuntu release.

### Temporarily switching to root

Despite the desire of Ubuntu's developers to stop you logging in as root, it's possible to temporarily switch to the root user account. This is useful if you have a lot of administrative work to do, where typing sudo before each command can become annoying.

To switch to the root user temporarily, type the following:

- sudo su

After typing your password, you'll see that the command-prompt changes to a hash symbol, to indicate that you have root powers.

When you've finished your work and want to return to your ordinary user account, just type exit, or hit Ctrl+D.

### Enabling root login

It's also possible to enable the root login account. This will make Ubuntu just like most other versions of Linux and Unix. The main
