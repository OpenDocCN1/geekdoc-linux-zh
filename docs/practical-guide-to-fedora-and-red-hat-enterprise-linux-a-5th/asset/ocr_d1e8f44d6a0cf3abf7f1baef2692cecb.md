The root directory appears at the top of the directory hierarchy and has no parent: A process cannot access any files above the root directory (because they do not exist). If, for example, you run a program (process) and specify its root directory as /home/sam/jail/, the program would have no concept of any files in /home/sam or above: jail is the program's root directory and is labeled / (not jail).

By creating an artificial root directory, frequently called a (chroot) jail, you prevent a program from accessing or modifying—possibly maliciously—files outside the directory hierarchy starting at its root. You must set up a chroot jail properly to increase security: If you do not set up the chroot jail correctly, you can actually make it easier for a malicious user to gain access to a system than if there were no chroot jail.

# Using chroot

Creating a chroot jail is simple: Working as root, give the command /usr/sbin/chroot directory. The directory becomes the root directory and the process attempts to run the default shell. Working with root privileges from the /home/sam directory, give the following command to set up a chroot jail in the (existing) /home/sam/jail directory:

```
# /usr/sbin/chroot /home/sam/jail
/usr/sbin/chroot: cannot run command '/bin/bash': No such file or directory
```

This example sets up a chroot jail, but when it attempts to run the bash shell, the operation fails. Once the jail is set up, the directory that is named jail takes on the name of the root directory, /, so chroot cannot find the file identified by the path-name /bin/bash. In this situation the chroot jail is working but is not useful.

Getting a chroot jail to work the way you want is a bit more complicated. To have the preceding example run bash in a chroot jail, you need to create a bin directory in jail (/home/sam/jail/bin) and copy /bin/bash to this directory. Because the bash binary is dynamically linked to shared libraries, you need to copy these libraries into jail as well. The libraries go in lib.

The next example creates the necessary directories, copies bash, uses ldd to display the shared library dependencies of bash, and copies the necessary libraries into lib. The linux-gate.so.1 file is a dynamically shared object (DSO) provided by the kernel to speed system calls; you do not need to copy it to the lib directory.

```
$ pwd
/home/sam/jail
$ mkdir bin lib
$ cp /bin/bash bin
$ ldd bin/bash
    linux-gate.so.1 =>  (0x0089c000)
    libtinfo.so.5 => /lib/libtinfo.so.5 (0x00cdd000)
    libdl.so.2 => /lib/libdl.so.2 (0x00bb0000)
    libc.so.6 => /lib/libc.so.6 (0x009c9000)
    /lib/ld-linux.so.2 (0x0099a000)
$ cp /lib/libtinfo.so.5,libdl.so.2,libc.so.6,ld-linux.so.2) lib
```