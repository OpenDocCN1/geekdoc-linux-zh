
If you accidentally use one of these characters and your shell does not return you to the normal prompt, simply press the `Ctrl` and `c` keys in combination with your current command to cancel.

![](img/c27875544958897d817484d558c208c8_93_0.png)

There are some circumstances in which you might need to use a metacharacter in a command and prevent the shell from interpreting its special meaning. To do this, simply enclose the metacharacters in single quotation marks `'`. Single quotation marks protect those metacharacters from being interpreted specially by the shell (that is, a `$` is interpreted as a `$` character and not a variable identifier). You can also use double quotation marks `"` to perform the same task; however, double quotation marks do not protect `$`, `\`, `\(`, and `` \` `` characters. If only one character needs to be protected from shell interpretation, you can precede that character by a `\` rather than enclosing it within quotation marks. An example of this type of quoting follows:

```
[root@server1 root]# echo My Shell is $SHELL
My Shell is /bin/bash
[root@server1 root]# echo 'My Shell is $SHELL'
My Shell is $SHELL
[root@server1 root]# echo "My Shell is $SHELL"
My Shell is /bin/bash
[root@server1 root]# echo My Shell is \$SHELL
My Shell is $SHELL
[root@server1 root]# _
```

As shown in Table 2-7, not all quote characters protect characters from the shell. The back quote characters `` ` `` can be used to perform command substitution; anything between back quotes is treated as another command by the shell, and its output is substituted in place of the back quotes. Take the expression `` `date` `` as an example:

```
[root@server1 root]# echo Today is `date`
Today is Tue Mar 29 09:28:11 EST 2015
[root@server1 root]# _
```

## Getting Command Help

Most distributions of Linux contain more than 1000 different Linux commands in their standard configurations, and thus it is impractical to memorize the syntax and use of each command. Fortunately, Linux stores documentation for each command in central locations so that it can be accessed easily. The most common form of documentation for Linux commands is **manual pages** (commonly referred to as **man pages**). Simply type the `man` command followed by a command name, and extensive information about that Linux command is displayed page-by-page on the terminal screen. This information includes a description of the command and its syntax, as well as available options, related files, and related commands. For example, to receive information on the format and usage of the `whoami` command, you can use the following command:

```
[root@server1 root]# man whoami
```

The manual page is then displayed page by page on the terminal screen. You can use the cursor (arrow) keys on the keyboard to scroll through the information or press `q` to quit. The manual page for `whoami` is similar to the following:

> WHOAMI(1)		User Commands		WHOAMI(1)

### NAME

`whoami` - print effective userid

### SYNOPSIS

```
whoami [OPTION]...
```

### DESCRIPTION

Print the user name associated with the current effective user id. Same as `id -un`.

```
  --help    display this help and exit
  --version output version information and exit
```

### AUTHOR

Written by Richard Mlynarik.

### REPORTING BUGS

Report bugs to <bug-coreutils@gnu.org>.

GNU coreutils home page: <http://www.gnu.org/software/coreutils/>

General help using GNU software: <http://www.gnu.org/gethelp/>

Report `whoami` translation bugs to <http://translationproject.org/>

### COPYRIGHT

Copyright©2013 Free Software Foundation, Inc. License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>.

This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

### SEE ALSO

The full documentation is maintained as a Texinfo manual. If the `info` and `whoami` programs are installed at your site, the command

```
info coreutils 'whoami invocation'
```

should give you access to the complete manual.

GNU coreutils 8.21			August 2013

```
[root@server1 root]#_
```

| Manual Page Section | Description |
|:---|:---|
| 1 | Commands that any user can execute |
| 2 | Linux system calls |
| 3 | Library routines |
| 4 | Special device files |
| 5 | File formats |
| 6 | Games |
| 7 | Miscellaneous |
| 8 | Commands that only the root user can execute |
| 9 | Linux kernel routines |
| n | New commands not categorized yet |

**Table 2-8  Manual page section numbers**

Note that the `whoami` command is displayed as WHOAMI(1) at the top of the preceding manual page output. The (1) denotes a section of the manual pages; section (1) means that `whoami` is a command that can be executed by any user. All manual pages contain certain section numbers that describe the category of the command in the manual page database; you can find a list of the different manual page section numbers in Table 2-8.

Sometimes, there is more than one command, library routine, or file that has the same name. If you run the `man` command with that name as an argument, Linux returns the manual page with the lowest section number. For example, if there is a file called `whoami` as well as a command named `whoami` and you type `man whoami`, the manual page for the `whoami` command (section 1 of the manual pages) is displayed. To display the manual page for the `whoami` file format instead, you simply type `man 5 whoami` to display the `whoami` file format (section 5 of the manual pages).

Recall that many commands are available to the Linux user; thus, it might be cumbersome to find the command that you need to perform a certain task without using a Linux command dictionary. Fortunately, you have the ability to search the manual pages by keyword. To find all of the commands that have the word “usb” in their names or descriptions, type the following:

```
[root@server1 root]# man -k usb
```

This command produces the following output:

fxload (8) - Firmware download to EZ-USB devices
usb (8) - list USB devices
sane-canon630u (5) - SANE backend for the Canon 630u USB flatbed scanner
sane-cardscan (5) - SANE backend for Corex CardScan usb scanners
sane-epjitsu (5) - SANE backend for Epson-based Fujitsu USB scanners.

sane-find-scanner (1) - find SCSI and USB scanners and their device files

sane-genesys (5) - SANE backend for GL646, GL841, GL843, GL847 and GL124 based USB flatbed scanners

sane-gt68xx (5) - SANE backend for GT-68XX based USB flatbed scanners

sane-kvs1025 (5) - SANE backend for Panasonic KV-S102xC USB ADF scanners .

sane-kvs20xx (5) - SANE backend for Panasonic KV-S20xxC USB/SCSI ADF scanners .

sane-kvs40xx (5) - SANE backend for Panasonic KV-S40xxC USB/SCSI ADF scanners .

sane-ma1509 (5) - SANE backend for Mustek BearPaw 1200F USB scanner

sane-mustek_usb (5) - SANE backend for Mustek USB flatbed scanners

sane-mustek_usb2 (5) - SANE backend for SQ113 based USB flatbed scanners

sane-plustek (5) - SANE backend for LM983[1/2/3] based USB flatbed scanners

sane-sm3600 (5) - SANE backend for Microtek scanners with M011 USB chip

sane-sm3840 (5) - SANE backend for Microtek scanners with SCAN08 USB chip

sane-u12 (5) - SANE backend for Plustek USB flatbed scanners, based on older parport designs

sane-usb (5) - USB configuration type for SANE

usb-devices (1) - print USB device details

usb_modeswitch (1) - switch mode of "multi-state" USB devices

usb_modeswitch_dispatcher (1) - dispatcher not intended for direct invocation.

ushid-dump (8) - dump USB HID device report descriptors and streams

```
[root@server1 root]#
```

After you find the command needed, you can simply run the `man` command on that command without the `-k` option to find out detailed information about the command.

![](img/c27875544958897d817484d558c208c8_96_0.png)

You can also use the `apropos usb` command to perform the same function as the `man -k usb` command. Both commands yield the exact same output on the terminal screen.

If you do not see any output from the `man -k` or `apropos` command following a Linux installation, you might need to run the `mandb` command to index the manpage database.

Another utility, originally intended to replace the `man` command in Linux, is the GNU info pages. You can access this utility by typing the `info` command followed by the name of the command in question. The `info` command returns an easy-to-read description of each command and also contains links to other information pages (called hyperlinks). Today,
