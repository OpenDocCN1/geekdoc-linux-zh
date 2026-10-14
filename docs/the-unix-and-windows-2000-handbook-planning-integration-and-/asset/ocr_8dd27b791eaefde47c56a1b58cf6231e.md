# boot.ini and You

The boot.ini file provides a list of installed operating systems and their locations to the Windows 2000 boot loader. Our previous example showed Windows 2000 and MS-DOS in the boot.ini file. The boot.ini file is shown here:

```
[boot loader]

timeout=30

default=multi(0)disk(0)rdisk(0)partition(1)\WINNT

[operating systems]

multi(0)disk(0)rdisk(0)partition(1)\WINNT="Microsoft Windows 2000 Server" /fastdetect

C:\="Microsoft MS-DOS 6.22"
```

This section will provide an overview of the two boot.ini sections, a description of available switches for Windows 2000, and a brief explanation of how to modify boot.ini.

# BOOT.INI SECTIONS

The boot.ini file has two sections: the [boot loader] section and the [operating systems] section. Each section is independent of the other. The following discusses the role of these sections, as well as provides an overview on how to construct an entry.

# The [boot loader] Section

The [boot loader] section has two purposes: to specify a timeout period before the default operating system is loaded and to specify the location of the default operating system. The default value for the timeout parameter is 30 seconds, but it can be any number you specify, including 0. The default parameter is typically the same as your first entry in the [operating systems] section discussed below, but can point to any valid operating system location.

# The [operating systems] Section

The [operating systems] section lists the locations and descriptions of the different operating systems installed. You can have more than one entry for a single OS if, for instance, you wish to have different switches specified