# 366 EMULATORS UNDER LINUX

# 12.2.1 Compilation and installation

Wine does not exist as a binary distribution. Therefore you must have the compiler installed to compile the source code. The installation of Wine also requires the X Window system to be installed together with the associated libraries and include files. An additional precondition is the libXpm library which is used for easy handling of bitmaps. The installation of Wine is as simple as that of the GNU programs and is limited to the use of ./configure and make.

Currently, in parallel with the emulator wine, the compatibility library libwine is generated as well. The general hope is that, in parallel the development of the emulator, the library can be worked upon too, thus facilitating porting of Windows programs to UNIX on any hardware platforms.

# 12.2.2 Configuration of the emulator

Prior to its first start, the emulators need to be appropriately configured. The default, the file /usr/local/etc/wine.conf is used. Individual users can configure the emulator according to their own requirements using the file ~/.wincerc. Both files have exactly the same structure. You will also find a sample configuration with the name wine.ini in the Wine directory.

An important issue for starting your first programs is the assignment of drive letters to LINUX directories, and the search path for programs and DLLs. For this purpose the file wine.conf, whose syntax recalls that of the .ini files of Windows, contains various sections:

+   The assignment of drive letters to the file system or devices such as disk drives is carried out in one Drive section per drive. You can specify both devices and directories of the LINUX directory tree.

```
[Drive C]
Path=/home/dos
Type=hd
Label=DOS-DISK
```

+   The search paths for programs, DLLs and other paths are configured in the wine section. The drives are assigned according to the specifications made in the Drive sections.

```
[wine]
Windows=c:\windows
system=c:\windows\system
Temp=c:\tmp
```