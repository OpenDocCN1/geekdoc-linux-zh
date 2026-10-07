# 14

# THE UNIX FILE SYSTEM constraints.

The Unix File System (UFS) is the general-purpose, disk-based file system that is shipped with Solaris. It has been the standard disk-based file system since early versions of SunOS 4.x. Over the life of Solaris, UFS has undergone extensive changes to keep pace with the required application performance, security, and reliability constraints.

# 14.1 UFS Development History

The original version of UFS is derived from the Berkeley Fast File System (FFS) work from Unix, architected by Kirk McKusick and Bill Joy in the late 1980s. The Berkeley FFS was the second major file system available for Unix and was a leap forward from the original System V file system. The System V file system was lightweight and simple but had significant shortcomings: poor performance, reliability, and lack of functionality.

During the development of SunOS 2.0, a file-system-independent interface was introduced to support concurrent, different file systems within an operating system instance. This interface, known today as the vnode/vfs interface, is the mechanism all file systems use to interface with the file-related system calls. (The vnode/vfs architecture is discussed further in "The vnode" on page 533.) At that time, UFS was modified so that it could be used within the vnode/ufs framework. Since then, UFS has been the focus of much of the file system development effort in Solaris.