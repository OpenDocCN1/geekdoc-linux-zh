# Enabling the Script on Bootup

If you wish to execute this script upon system bootup, make it executable or type the command `chmod 700 <filename>`. Now place it somewhere that it will not be easily overlooked. Then, in the `/etc/rc.d/rc.local` file, place a line that starts up the script. I placed my own `rc.firewall.local` script in the same directory as that of `rc.local` and called it in the following manner:

```
```bash
/etc/rc.d/rc.firewall.local
```
```

# Gaining Added Security

Aside from those already mentioned in this book, several other programs are available on the Internet and designed for Linux that will assist in keeping your system secure and in checking for intruders. Not all are free, either for you to use at your discretion or to distribute among others on the Internet, but the vast majority encourages users to proliferate their scripts throughout the Linux community and to make improvements or adjustments.

# Setting Off Tripwires

One commonly used program for checking the current files on your Linux system is Tripwire. This program generates a database of the existing directories and files on a newly installed system and then periodically checks for changes to the files. If any user changes a system file containing important or sensitive data, Tripwire will send you an email to notify you about the modification.

Tripwire is free for noncommercial use and is covered under the LGPL license. I have found Tripwire capable of keeping me informed of any system changes. Even those files that I modify myself or that are updated nightly are tracked and logged. For tracking individual files that are crucial to system integrity, this program and others like it are invaluable.

According to the Tripwire Web site, http://www.tripwiresecurity.com/, this program is a *system integrity checker*—a utility that compares properties of designated files and directories against information stored in a previously generated database. You should install this program immediately after installing Linux on