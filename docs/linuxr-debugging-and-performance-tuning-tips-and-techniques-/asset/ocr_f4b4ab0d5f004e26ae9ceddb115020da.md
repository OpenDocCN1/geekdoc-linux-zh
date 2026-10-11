```
```
$ ls -l /dev/tty /dev/hda
brw-rw---
1 root disk 3, 0 Aug 31 02:31 /dev/hda
crw-rw-rw-
1 root root 5, 0 Feb 26 08:44 /dev/tty
```
```

The initial `b` represents block devices, and a `c` represents character devices. Device files are discussed further in Section 5.4, “Obtaining Information about Files,” page 139.

# 1.2 The Linux/Unix Process Model

A process is a running program.⁵ Processes have the following attributes:

+   - A unique process identifier (the PID)
+   - A parent process (with an associated identifier, the PPID)
+   - Permission identifiers (UID, GID, groupus, and so on)
+   - An address space, separate from those of all other processes
+   - A program running in that address space
+   - A current working directory (`.`)
+   - A current root directory (`/`;
+   changing this is an advanced topic)
+   - A set of open files, directories, or both
+   - A permissions-to-deny mask for use in creating new files
+   - A set of strings representing the environment
+   - A scheduling priority (an advanced topic)
+   - Settings for signal disposition (an advanced topic)
+   - A controlling terminal (also an advanced topic)

When the `main()` function begins execution, all of these things have already been put in place for the running program. System calls are available to query and change each of the above items; covering them is the purpose of this book.

New processes are always created by an existing process. The existing process is termed the *parent*, and the new process is termed the *child*. Upon booting, the kernel handcrafts the first, primordial process, which runs the program `/sbin/init`; it has process ID