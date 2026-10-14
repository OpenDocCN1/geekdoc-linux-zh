```
```ini
[Menu]
menuitem=Win, Boot Windows...
menuitem=DOS, Boot MS-DOS...
menuitem=Linux, Boot Linux...
menucolor=15,1
menudefault=Win,5
```
```

*File 9: Sample config.sys for Booting Linux (Part 1)*

Set up the boot menu items under the [Menu] label. Also set the menu's color, the time after which the default system should boot, and which one is the default.

+   2. Enter the labels [Common], [Win], [DOS], and [Linux] further below. Write the global entries under [Common]. Under the other labels, enter the specifications that should only apply to certain entries. Use the lines as in the following File:

```
```ini
[Common]
device=c:\dos\himem.sys /testmem:off
device=c:\dos\emm386.exe noems
dos=high,umb
files=30
buffers=10
shell=c:\dos\command.com

[Win]
devicehigh=c:\dos\dblspace.sys /move
devicehigh=c:\lcd\slcd.sys /D:SONY_000 /B:340 /M:P /V /C

[DOS]
devicehigh=c:\dos\dblspace.sys /move
devicehigh=c:\lcd\slcd.sys /D:SONY_000 /B:340 /M:P /V /C

[Linux]
shell=c:\loadlin\loadlin.exe c:\loadlin\linux.par

[Common]
rem Remains empty
```
```

Finally, save the file.