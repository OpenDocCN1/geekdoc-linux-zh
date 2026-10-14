If you’ve never used Linux before, trying to understand and manage the file structure can be a bit of a challenge. The Ubuntu workstation includes some tools to help with handling files, which makes life easier for novices and advanced users alike. The first part of this chapter discusses how Ubuntu handles hard drives and files so that you can figure out where your files and folders are. The second part of the chapter walks through Nautilus, the graphical file management tool provided in Ubuntu. The Nautilus application helps you navigate through the complicated Ubuntu filesystem and makes working with your files and folders much easier.

# The Linux Filesystem

If you’re new to the Linux system, you may be confused by how it references files and directories, especially if you’re used to the way the Microsoft Windows operating system does that. Before exploring the Linux system, it helps to have an understanding of how it’s laid out.

# Filepaths

The first difference you’ll notice is that Linux does not use drive letters in pathnames. In the Windows world, the physical drives installed on the PC determine the pathname of the file. Windows assigns a letter to each physical disk drive, and each drive contains its own directory structure for accessing files stored on it.

For example, in Windows you may be used to seeing filepaths such as C:\Documents and Settings\Rich\My Documents\test.doc.

This indicates that the file test.doc is located in the directory My Documents, which is under the directory Rich, which is contained under the directory Documents and Settings, which is located on the hard disk partition assigned the letter C (usually the first hard drive on the PC).

The Windows filepath tells you exactly which physical disk partition contains the file named test.doc. If you want to save a file on a floppy disk, you would click the icon for the A drive, which automatically uses the filepath A:\test.doc. This path indicates that the file is located at the root of the drive assigned the letter A, which is usually the PC’s floppy disk drive.

This is not the method used by Linux. Linux stores files within a single directory structure, called a virtual directory. The virtual directory contains filepaths from all the storage devices installed on the PC, merged into a single directory structure.

The Linux virtual directory structure contains a single base directory, called the root. Directories and files beneath the root directory are listed based on the directory path used to reach them, similar to the way Windows does it.

> You’ll notice that Linux uses a forward slash (/) instead of a backward slash (\ ) to denote directories in filepaths. The backslash character in Linux denotes an escape character and causes all sorts of problems when you use it in a filepath. This may take some getting used to if you’re coming from a Windows environment.