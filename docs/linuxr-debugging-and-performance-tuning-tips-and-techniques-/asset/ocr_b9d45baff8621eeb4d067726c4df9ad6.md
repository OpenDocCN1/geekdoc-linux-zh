```
$ ch08-statfs
/, mounted on /dev/hda2:
	f_type: EXT2
	f_bsize: 4096
	f_blocks: 1549609
	f_bfree: 316664
	f_bavail: 237946
	f_files: 788704
	f_ffree: 555483
	f_namelen: 255
...
/win, mounted on /dev/hda1:
	f_type: MSDOS
	f_bsize: 4096
	f_blocks: 2092383
	f_bfree: 1391952
	f_bavail: 1391952
	f_files: 0
	f_ffree: 0
	f_namelen: 260
```

In conclusion, whether to use statvfs() or statfs() in your own code depends on your requirements. As described in the previous section, GNU df doesn't use statvfs() under GNU/Linux and in general tends to use each Unix system's unique “get filesystem info” system call. Although this works, it isn't pretty. On the other hand, sometimes you have no choice; for example, the GLIBC problems we mentioned above. In this case, there is no perfect solution.

# 8.4 Moving Around in the File Hierarchy

Several system calls and standard library functions let you change your current directory and determine the full pathname of the current directory. More complicated functions let you perform arbitrary actions for every filesystem object in a directory hierarchy.

# 8.4.1 Changing Directory: chdir() and fchdir()

In Section 1.2, “The Linux/Unix Process Model,” page 10, we said:

> The current working directory is the one to which relative pathnames (those that don't start with a /) are relative. This is the directory you are “in” whenever you issue a `cd someplace` command to the shell.