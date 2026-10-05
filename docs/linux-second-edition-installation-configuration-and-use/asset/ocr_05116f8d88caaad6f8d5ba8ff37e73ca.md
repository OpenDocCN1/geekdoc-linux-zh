# 454 COMMAND REFERENCE

mdir accesses the diskette and reads its parameters. In future Linux versions, fdformat will probably be replaced by superformat.

# Example

user fdformat /dev/fd0 > /dev/null &
forforms an HD diskette in drive A. Through the specification of &, the process is carried out in the background, so that you can continue working immediately. Furthermore, the specification of > /dev/null redirects the output of fdformat into oblivion, so that you are not continuously disturbed by the message. Formatting n'.

```
fdisk [options][device]
```

fdisk is used to partition a hard disk. The command can only be executed by root. When no device file is specified, fdisk automatically refers to the first IDE hard disk (/dev/had). fdisk -l displays a list of all partitions on all IDE and SCSI disks. The usage of the command is extensively described in the context of Linux installation (page 33).
The command should never be used on a hard disk if one of the partitions is currently mounted into the Linux file system. If this cannot be avoided, you must restart your computer after changing the partition table to make the changes effect, fdisk issues a warning on this matter which you should definitely take seriously!
After you have configured your system, you should produce a printout of the result of fdisk -l and keep it in a place where you will be able to find it again. This information is often sufficient to restore a destroyed partition table of a hard disk.

# fg [process]

fg continues a process in the foreground. When no process is specified, fg applies to the last process interrupted or the last process started in the background. Otherwise, the process must be specified through its name or its bash-internal job number (not PID). fg is a bash command. It can also be written using the short notation xprocess. Many programs (processes) can be interrupted by means of [Ctrl]+Z.

# file file

file tries to determine the type of data in a file. To do this, the command evaluates the file /etc/magic. The result is displayed on screen (for example, data, text, executable, and so on). Warning: text files containing foreign language characters are interpreted as data (not as text).

```
find [path.specification][search_options]
```

find helps to find files in the many branches of the directory tree. Several search criteria (such as file name patterns, file size, date and time of last modification, and