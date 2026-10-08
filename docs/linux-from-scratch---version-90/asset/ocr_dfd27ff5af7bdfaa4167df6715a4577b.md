The new instance of the shell is a non-login shell, which does not read the /etc/profile or .bash_profile files, but rather reads the .bashrc file instead. Create the .bashrc file now:

```
cat ~/.bashrc << "EOF"
set +h
humask 022
LFS=/mnt/lfs
LC_ALL=POSIX
LC_TGT=$(uname -m) -lfs-linux-gnu
PATH=/tools/bin:/usr/bin
export LFS LC_ALL LFS_TGT PATH
EOF
```

The set +h command turns off bash's hash function. Hashing is ordinarily a useful feature—bash uses a hash table to remember the full path of executable to avoid searching the PATH time and again to find the same executable. However, the new tools should be used as soon as they are installed. By switching off the hash function, the shell will always search the PATH when a program is to run. As such, the shell will find the newly compiled tools in $LFS/tools as soon as they are available without remembering a previous version of the program in a different location.

Setting the user file-creation mask (umask) 022 ensures that newly created files and directories are only writable by their owner, but are readable and executable by everyone (assuming default modes are used by the open (2) system, new files will end up with permission 644 and directories with mode 755).

The LFS variable should be set to the chosen mount point.

The LC_ALL variable controls the localization of certain programs, making their messages follow the conventions of a specified country. Setting LC_ALL to "POSIX" or "C" (the two are equivalent) ensures that everything will work in the expected cho environment.

The LFS_TGT variable sets a non-default, compatible machine description for when building our cross compiler and linker and when compiling our temporary toolchain. More information is contained in Section 5.2, "Toolchain Technical".

By putting /tools/bin ahead of the standard PATH, all the programs installed in Chapter 5 are picked up by the shell immediately after their installation, combined with turning off hashing, limits the old programs that are used from the host system when available in the chapter 5 environment.

Finally, to have the environment fully prepared for the temporary tools, source the just-created user profile:

```
source ~/.bash_profile
```

# 4.5. About SBUs

Many people would like to know beforehand approximately how long it takes to compile and install each package. Linux From Scratch can be built on many different systems, it is impossible to provide accurate time estimates. The biggest package (Glibc) will take approximately 20 minutes on the fastest systems, but could take up to three days on slower systems! Instead of providing actual times, the Standard Build Unit (SBU) measure will be used instead.

The SBU method works as follows. The first package to be compiled from this book is Binutils in Chapter 5. The time it takes to compile this package is what referred to as the Standard Build Unit or SBU. All other times will be relative to this time.