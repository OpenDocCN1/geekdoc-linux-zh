# RFC (continued)

The RFCs are unusual in that they are floated by technical experts acting on their own initiative and reviewed by the Internet at large rather than formally promulgated through an institution such as ANSI. For this reason, they remain as RFCs even once adopted as standards. The RFC tradition of pragmatic, experience-driven, after-the-fact standard writing by individuals or small working groups has immense advantages over the more formal, committee-driven process typical of ANSI or ISO.

# ROM

Read-only memory. A kind of nonvolatile. A data storage device that is manufactured with fixed contents. In general, ROM describes any storage system whose contents cannot be altered, as a gramophone record or printed book. When used in reference to electronics and computers, ROM describes semiconductor integrated circuit memories, of which there are several types, and CD-ROM.

ROM is nonvolatile storage—it retains its contents even after power has been removed; contrast to RAM (page 1487). ROM is often used to hold programs for embedded systems, which have a fixed purpose. ROM is also used for storage of the BIOS (page 1457) in a computer.

# root directory

The ancestor of all directories and the start of all absolute paths. The name of the root directory is /,

# root filesystem

The filesystem that is available when the system is brought up in single-user mode. The name of this filesystem is always /. You cannot unmount or remove the root filesystem. You can remount root to change its mount options (page 949).

# root login

Usually the login name of Superuser (page 1496).

# rotate

When a file, such as a log file, grows indefinitely, you may keep it from taking up too much space on the disk. Because you may need to refer to the information in the log file in the future, it is generally not a good idea to delete the contents of the file until it is aged. Toward this end you can periodically save the current log file under a new name and create a new, empty file for the current log file. You can keep a series of these files, renaming each as a new one is saved. You will then rotate the files as, for example, remove xylog.4, xylog.3→xylog.4, xylog.2→xylog.3, xylog.1→xylog.2, xylog→xylog.1, create a new xylog file. By the time you remove xylog.4, it will not contain any information more recent than you want to remove.

# router

A device, often a computer, that is connected to more than one type of network to pass data between them. See gateway on page 1469.