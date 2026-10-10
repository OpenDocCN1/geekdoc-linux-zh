# OPTIONS

-w wtmp (5)-file
This specifies an alternate wtmp (5) file, instead of /var/log/wtmp. The special na "none" disables writing records to the wtmp (5) file.

-u utmp (5)-file
This specifies an alternate utmp (5) file, instead of /var/run/utmp. The special na "none" disables writing records to the utmp (5) file.

-L lastlog-file
This specifies an alternate lastlog file, instead of /var/log/lastlog, if the platform supports lastlog files. The special na "none" disables writing records to the lastlog file.

-l line-na
This describes the "line" na of the entry. For terminal sessions, this is the final pathna segnt of the terminal device fileName (e.g. ttyd0). For X sessions, it should probably be the local display na given to the users session (e.g. :0). If none is specified, the terminal na will be determined with (3) and stripped of leading components.

-h host-na
This is set to indicate that the session was initiated from a remote host. In typical xdm usage, this options is not used.

-s slot-nuer
Each potential session has a unique slot nuer in BSD systems, most are identified by the position of the line-na in the /etc/ttysfile. This option overrides the default position determined with (3). This option is inappropriate for use with xdm, the -x option is more useful. This option is accepted for compatibility, but does nothing in this version of sessreg.

-x Xservers-file
As X sessions are one-per-display, and each display is entered in this file, this options sets the slot-nuer to be the nuer of lines in the ttys-file plus the index into this file that the line-na is found. This option is accepted for compatibility, but does nothing in this version of sessreg.

-t ttys-file
This specifies an alternate file which the -x option will use to count the nuer of terminal sessions on a host. This option is accepted for compatibility, but does nothing in this version of sessreg.

-V
This option causes the command to print its version and exit.

-a
This session should be added to utmp/wtmp.

-d
This session should be deleted from utmp/wtmp. One of -a/-d st be specified.