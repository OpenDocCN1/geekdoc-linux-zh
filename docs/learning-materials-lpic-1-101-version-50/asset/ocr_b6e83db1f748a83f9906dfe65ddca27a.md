files on Linux systems. Each location has a different purpose and behavior, and it is recommended that developers follow the conventions set by the FHS when writing temporary data to disk.

# /tmp

According to the FHS, programs should not assume that files written here will be preserved between invocations of a program. The recommendation is that this directory be cleared (all files erased) during system boot-up, although this is not mandatory.

# /var/tmp

Another location for temporary files, but this one *should not be cleared* during the system boot-up. Files stored here will usually persist between reboots.

# /run

This directory contains run-time variable data used by running processes, such as process identifier files (.pid). Programs that need more than one run-time file may create subdirectories here. This location *must be cleared* during system boot-up. The purpose of this directory was once served by `/var/run`, and on some systems `/var/run` may be a symbolic link to `/run`.

Note that there is nothing which prevents a program from creating temporary files elsewhere on the system, but it is good practice to respect the conventions set by the FHS.

# ## Finding Files

To search for files on a Linux system, you can use the `find` command. This is a very powerful tool, full of parameters that can suit its behaviour and modify output exactly to your needs.

To start, `find` needs two arguments: a starting point and what to look for. For example, to search for all files in the current directory (and subdirectories) whose name ends in `.jpg` you can use:

```
```
$ find . -name '*.jpg'
./pixel_3a_seethrough_1.jpg
./Mate3.jpg
./Expert.jpg
./Pentaro.jpg
./Mate1.jpg
./Mate2.jpg
./Sala.jpg
./Hotbit.jpg
```
```