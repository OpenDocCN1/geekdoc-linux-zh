6. Use the ls -C -F command to list all the directories contained at this point in the file system. Beware, though; on large systems, this directory could easily have hundreds of different directories. On one system I, there are almost 550 different directories one level above my home directory in the file system!

| ls -C -F | | |
| armstrong/ | christine/ | guest/ | laura/ | matthew/ | shake/ |
| bruce/ | david/ | higiggins/ | mac/ | rank/ | taylor/ |
| cedric/ | green/ | kane/ | mark/ | shalini/ | vicky/ |

Try using a combination of cd and pwd to move about your file system, and remember that without any arguments, cd zips right back to your home directory.

![](bbox=[0.156, 0.313, 0.226, 0.333])

# Summary

This hour has focused on the UNIX file system, how UNIX differs from Macintosh and DOS systems, and how UNIX remembers preferences with its hidden dots. This hour has also explained the difference between relative and absolute filenames, and you've learned about the "." and ".." directories. You've learned three new commands: env to list your current environment, cd to change directories, and pwd to find out your present working directory location.

# Workshop

The Workshop summarizes the key terms you learned and poses some questions about the topics presented in this chapter. It also provides you with a preview of what you will learn in the next.

# Key Terms

**absolute filename** Any filename that begins with a leading slash (/); these uniquely describe a single file in the file system.

**binary** A file format that is intended for the computer to work with rather than for humans to peruse. See also **executable**.

**device driver** All peripherals attached to the computer are called devices in UNIX, and each has a control program always associated with it, called a *device driver*. Examples are the device drivers for the display, keyboard, mouse, and all hard disks.

**directory** A type of UNIX file used to group other files. Files and directories can be placed inside other directories, to build a hierarchical system.

![](bbox=[0.063, 0.893, 0.128, 0.966])