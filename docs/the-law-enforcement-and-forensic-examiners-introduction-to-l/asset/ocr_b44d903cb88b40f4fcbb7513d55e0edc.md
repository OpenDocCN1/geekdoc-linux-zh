v:4.33
A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

```
barry@forensic1:-$ python WinTime.py `xxd -s 128 -l8 -l8 -ps nmap.pf.123`nThu Apr 6 15:07:20 2017
```

Given enough information about the format, you could spend a lot of time parsing thenfile. There's other information stored within, including libraries and other files accessed whennthe executable is started. But from here we'll use sccainfo from libssca to view the prefetchncontents, which is quite extensive.

```
barry@forensic1:-$ sccainfo nmap.pf.123nsccainfo 20170105
```

+   Windows Prefetch File (PF) information:
Format version : 23
Prefetch hash : 0x69b77167
Executable filename : NMAP.EXE
Run count : 9
Last run time : Apr 06, 2017 15:07:22.470652700 UTC

+   Filenames:
Number of filenames : 53
Filename: 1 : \DEVICE\HARDDISKVOLUME2\WINDOWS\SYSTEM32\NTDLL.DLL
Filename: 2 : \DEVICE\HARDDISKVOLUME2\WINDOWS\SYSTEM32\
KERNEL32.DLL
Filename: 3

\DEVICE\HARDDISKVOLUME2\USERS\ALBERTE\DOWNLOADS\NMAP-7.40-WIN32\NMAP-7.40\NMAP-OS-\nDB

+   Volumes:
Number of volumes : 1

+   Volume: 1 information:
Device path : \DEVICE\HARDDISKVOLUME2
Creation time : Apr 06, 2017 04:48:55.209910400 UTC
Serial number : 0x5019050c

There are numerous utilities available to Linux users that can be found to assist innparsing files, artifacts and other data recovered from computers running operating systemsnother than Linux. There are, in fact, too many to list here. Sometimes it's simply a matter of
finding a comparable open source project: like using LibreOffice to view Microsoft Office or
Visio files. There are also the simple utilities that are either pre-installed or easily installed on

299