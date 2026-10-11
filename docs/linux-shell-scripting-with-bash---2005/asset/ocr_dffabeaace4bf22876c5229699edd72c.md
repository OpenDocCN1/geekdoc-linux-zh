syllable stressed, as in LIH-nicks, but it is sometimes pronounced LYE-nicks (the angli-cized “Linus’ Unix”) or LEE-nicks.

Strictly speaking, Linux refers to the operating system kernel that starts and manages other programs and provides access to system resources. The various open source shells, compilers, standard libraries, and commands are a part of another project called **GNU**. The GNU project was started by the Free Software Foundation (**FSF**) as an attempt to create a free version of Unix. The main Linux C compiler, *gcc*, is a part of the GNU project.

There is also a GNU kernel project, but the Linux kernel has largely superseded this effort.

X Windows is also not strictly a part of Linux. Xfree86, the open source version of X Windows, was adapted to the Linux operating system and was released under a different license.

# Files and File Systems

Each Linux disk (or other long-term block storage device) contains a collection of files organized according to a policy or set of rules called a *file system*. Each disk can be divid-ed into *partitions* (or “slices”), whereby every partition has its own file system. Linux is not restricted to a single file system for all disks: the user can use disks created by other operating systems as if they were native Linux disks.

The standard file system is the second extended file system, or *ext2*. This is the second revision of the Minix file system with support for large disk sizes and filenames. ext2 permits partitions up to 4TB (terabytes), files up to 2GB (gigabytes), and 255-character filenames. Newer distributions use *ext3*, a version of ext2 with special features for error recovery.

Support for other file systems might be available depending on your distribution and installation options. They might include Microsoft Windows NT, Apple HFS, or journal-ing file systems.

The ext2 file system uses caching to increase performance. If an ext2 disk is not properly shut down, files can be corrupted or lost. It is vitally important that a Linux computer is shut down properly or is protected by some kind of uninterruptible power supply.

To save space, ext2 files that contain large amounts of zeros (called *sparse files*) are not actually stored on a disk. Certain shell commands provide options for creating and hand-ling sparse files.

Each file is identified by a name, and the allowed names are determined by the file system. For practicality, the names seldom exceed 32 characters and usually consist of lowercase characters, underscores, minus signs, and periods. Spaces and punctuation sym-bols, for example, are permitted, but can cause problems in shell scripts that do not expect them.