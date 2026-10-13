After the downloading is complete (hopefully it didn't take too long), you can dig right into the rest of the preparation you need to have a sane, secure, and positive kernel upgrading experience.

Because you probably loaded source files with your current Linux installation, you should have a directory in which the original source tree is still installed. It would be a good idea, if your drive has the space, to save your original source tree just in case you want to go back. To do this, change to the /usr/src directory and list the contents. One of the things you'll find is a subdirectory called /usr/src/linux, which contains the Linux source tree for your present installation. Rename this directory, by using the mv command, to something other than /linux. A common renaming scheme is to add the old kernel version number to the directory's name, as in linux-2.x.x. But just make sure that there is no directory named /linux in /usr/src.

> The installation program for the Linux-Mandrake and TurboLinux distributions renames the directory to linux-2.2.x automatically. Other distributions might also do the same, but inside this directory is an /include directory that contains the directory called /linux. However, there is no need to change the name of this directory to keep the files intact. Instead, there is a symbolic link called linux in the /usr/src directory. That link points to the linux-2.x.x directory that you must rename to something other than linux.

You're now finished with the preparation phase, and it is time to get on to the action phase. To begin, you need to unpack the source code that you downloaded. To do this make sure you are in /usr/src and type

```
tar xpvf linux-2.x.x.tar.gz
```

where 2.x.x is the kernel version you downloaded. After you have untarred the source code, read the README file! The README file found with the unpacked archive files will be the most up-to-date advice that you are going to get from the people at your favorite Linux distribution. Because they were the ones who introduced their own little variations into the soup, they are the ones who know what you should most exactly do next! After you finish reading the README, the only thing left is taking the plunge.

> In Hour 2, "Installing Linux-Mandrake," it was suggested that you create a boot disk. Make sure that you have this disk before you begin. You can also create the boot disk with the mkbootdisk command.