# **TABLE 3.3 Options for 1spci (continued)**

| Option | Effect |
| :--- | :--- |
| -d [vendor]:[device] | Shows data on the specified device. |
| -i file | Uses the specified file to map vendor and device IDs to names. (The default is /usr/share/misc/pci.ids.) |
| -m | Dumps data in a machine-readable form, intended for use by scripts. A single -m uses a backward-compatible format, whereas doubling (-mm) uses a newer format. |
| -D | Displays PCI domain numbers. These numbers normally aren't displayed. |
| -M | Performs a scan in bus-mapping mode, which can reveal devices hidden behind a misconfigured PCI bridge. This is an advanced option that can be used only by root. |
| --version | Displays version information. |

# ## Learning about Kernel Modules

Hardware in Linux is handled by kernel drivers, many of which come in the form of *kernel modules*. These are stand-alone driver files, typically stored in the `/lib/modules` directory tree, that can be loaded to provide access to hardware and unloaded to disable such access. Typically, Linux loads the modules it needs when it boots, but you may need to load additional modules yourself.

You can learn about the modules that are currently loaded on your system by using `1smod`, which takes no options and produces output like this:

```
$ lsmod
Module          Size  Used by
isofs           35820   0
zlib_inflate    21888   1 isofs
floppy          65200   0
nls_iso8859_1    5568   1
nls_cp437       7296    1
vfAT            15680   1
```