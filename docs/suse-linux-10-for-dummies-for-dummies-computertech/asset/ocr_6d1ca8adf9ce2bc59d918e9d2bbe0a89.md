![](bbox=[0.242, 0.136, 0.844, 0.55])

**Figure 6-1:** The Linux file system provides a unified view of your storage that may span multiple storage devices.

If you’re familiar with MS-DOS or Windows, you may find something missing in the Linux file system: You don’t find drive letters such as C: and D: in Linux. All disk drives and CD-ROM drives are part of a single file system.

In Linux, filenames can be long (up to 256 characters) and are case-sensitive. Often these filenames have multiple extensions, such as `sample.tar.Z`. UNIX filenames can take many forms, such as the following: `index.html`, `Makefile`, `XF86Config.install.old`, `vsftpd-2.0.1-2.i386.rpm`, `.bash_profile`, and `apache2_src.tar.gz`.

To locate a file, you need more than just the filename. You also need information about the directory hierarchy. The extended filename, showing the full hierarchy of directories leading to the file, is called the pathname. As the name implies, it’s the path to the file through the maze of the file system. Figure 6-2 shows a typical pathname for a file in Linux.