![](bbox=[0.16, 0.06, 0.26, 0.18])

Rootfs cannot be unmounted, for more or less the same reason you can't kill the init process. Rather than having special code to check for and handle an empty list, it's simpler for the kernel to just make sure certain lists can't become empty.

Most systems just mount another filesystem over Rootfs and ignore it. An empty instance of Ramfs takes up a tiny amount of space.

After extraction, the kernel will try to locate an init program in the Rootfs filesystem. If present, Rootfs is used as the root filesystem, and the init program in it is responsible for setting up the rest of the running system (and perhaps mounting a different root filesystem on top of Rootfs). If no init program is in Rootfs, the 2.6 kernels fall back to executing older code that looks for the root filesystem via the kernel command-line root parameter or an inird mechanism.

Populating such an Ininitramfs can be done via the CONFIG_INITRAMFS_SOURCE kernel configuration option, which can be used to hardcode the location of the ininitramfs archive into the kernel binary. The option value can point to an existing gzipped CP10 archive, a directory containing files to be compressed into a new archive, or a text file that contains lines in the following syntax:

```
# a comment
file name location mode uid gid
dir name mode uid gid
nod name mode uid gid dev_type maj min
slink name target mode uid gid
pipe name mode uid gid
sock name mode uid gid
```

where the parameters have the following meanings:

name The name of the file, directory, etc. in the archive

location The location of the file in the current filesystem

target The target of a link

mode The permissions of the file in octal notation (e.g., 777 denotes full permission)

uid The user ID (0 for root)

gid The group ID (0 for root)

dev_type The device type (b for block or c for character)