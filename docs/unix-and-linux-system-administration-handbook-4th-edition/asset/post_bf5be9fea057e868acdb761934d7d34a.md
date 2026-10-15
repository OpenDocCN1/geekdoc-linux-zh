
## Table 6.2 Standard directories and their contents

| Pathname | OS | Contents |
|---|---|---|
| `/bin` | All | Core operating system commandsᵇ |
| `/boot` | LS | Kernel and files needed to load the kernel |
| `/dev` | All | Device entries for disks, printers, pseudo-terminals, etc. |
| `/etc` | All | Critical startup and configuration files |
| `/home` | All | Default home directories for users |
| `/kernel` | S | Kernel components |
| `/lib` | All | Libraries, shared libraries, and parts of the C compiler |
| `/media` | LS | Mount points for filesystems on removable media |
| `/mnt` | LSA | Temporary mount points, mounts for removable media |
| `/opt` | All | Optional software packages (not consistently used) |
| `/proc` | LSA | Information about all running processes |
| `/root` | All | Home directory of the superuser (often just `/`) |
| `/sbin` | All | Commands needed for minimal system operabilityᶜ |
| `/stand` | H | Stand-alone utilities, disk formatters, diagnostics, etc. |
| `/tmp` | All | Temporary files that may disappear between reboots |
| `/usr` | All | Hierarchy of secondary files and commands |
| `/usr/bin` | All | Most commands and executable files |
| `/usr/include` | All | Header files for compiling C programs |
| `/usr/lib` | All | Libraries; also, support files for standard programs |
| `/usr/lib64` | L | 64-bit libraries on 64-bit Linux distributions |
| `/usr/local` | All | Software you write or install; mirrors structure of `/usr` |
| `/usr/sbin` | All | Less essential commands for administration and repair |
| `/usr/share` | All | Items that might be common to multiple systems |
| `/usr/share/man` | All | On-line manual pages |
| `/usr/src` | LSA | Source code for nonlocal software (not widely used) |
| `/usr/tmp` | All | More temporary space (preserved between reboots) |
| `/var` | All | System-specific data and configuration files |
| `/var/adm` | All | Varies: logs, setup records, strange administrative bits |
| `/var/log` | LSA | Various system log files |
| `/var/spool` | All | Spooling directories for printers, mail, etc. |
| `/var/tmp` | All | More temporary space (preserved between reboots) |

a. L = Linux, S = Solaris, H = HP-UX, A = AIX.

b. On HP-UX and AIX, `/bin` is a symbolic link to `/usr/bin`.

c. The distinguishing characteristic of commands in `/sbin` is usually that they’re linked with “static” versions of the system libraries and therefore don’t have many dependencies on other parts of the system.

## 6.4 FILE TYPES

Most filesystem implementations define seven types of files. Even when developers add something new and wonderful to the file tree (such as the process information under `/proc`), it must still be made to look like one of these seven types.

![](img/14d78e3cecac4581d37024baf1e94cca_195_0.png)

- Regular files
- Directories
- Character device files
- Block device files
- Local domain sockets
- Named pipes (FIFOs)
- Symbolic links

You can determine the type of an existing file with **ls -ld**. The first character of the ls output encodes the type. For example, the following command demonstrates that **/usr/include** is a directory:

```
$ ls -ld /usr/include
 drwxr-xr-x 27 root root 4096 Jul 15 20:57 /usr/include
```

**ls** uses the codes shown in Table 6.3 to represent the various types of files.

**Table 6.3 — File-type encoding used by ls**

| File type | Symbol | Created by | Removed by |
|---|---|---|---|
| Regular file | - | editors, cp, etc. | rm |
| Directory | d | mkdir | rmdir, rm -r |
| Character device file | c | mknod | rm |
| Block device file | b | mknod | rm |
| Local domain socket | s | socket(2) | rm |
| Named pipe | p | mknod | rm |
| Symbolic link | l | ln -s | rm |

As Table 6.3 shows, **rm** is the universal tool for deleting files. But how would you delete a file named, say, -f? It’s a legitimate filename under most filesystems, but **rm -f** doesn’t work because **rm** interprets the -f as a flag. The answer is either to refer to the file by a longer pathname (such as ./-f) or to use **rm --** argument to tell it that everything that follows is a filename and not an option (i.e., **rm -- -f**).

Filenames that contain control characters present a similar problem since reproducing these names from the keyboard can be difficult or impossible. In this situation, you can use shell globbing (pattern matching) to identify the files to delete. When you use pattern matching, it’s a good idea to get in the habit of using the **-i** option to **rm** to make **rm** confirm the deletion of each file. This feature protects you against deleting any “good” files that you pattern inadvertently matches. For example, to delete a file named foo<Control-D>bar, you could use

```
$ ls
foo?bar    foose    kde-root

$ rm -i foo*
rm: remove ‘foo\004bar’? y
rm: remove ‘foose’? n
```
