![](bbox=[0.135, 0.136, 0.789, 0.314])

As Figure 6-2 shows, the pathname has the following parts:

+   - The root directory, indicated by a forward slash (`/`) character.
+   - The directory hierarchy, with each directory name separated from the previous one by a forward slash (`/`) character. A `/` appears after the last directory name.
+   - The filename, with a name and one or more optional extensions. (A period appears before each extension.)

The Linux file system has a well-defined set of top-level directories, and some of these directories have specific purposes. Finding your way around the file system is easier if you know the purpose of these directories. You also become adept at guessing where to look for specific types of files when you face a new situation. Consult Table 6-1 for a brief description of the top-level directories in the Linux file system.

**Table 6-1 — Top-level Directories in the SUSE Linux File System**

| Directory | Description |
|---|---|
| `/` | This root directory forms the base of the file system. All files and directories are contained logically in the root directory, regardless of their physical locations. |
| `/bin` | Contains the executable programs that are part of the Linux operating system. Many Linux commands, such as `cat`, `cp`, `ls`, `more`, and `tar`, are located in `/bin`. |
| `/boot` | Contains the Linux kernel and other files that the GRUB boot manager needs. (The kernel and other files can be anywhere, but placing them in the `/boot` directory is customary.) |
| `/dev` | Contains special files that represent devices attached to the system. |