any memory not being used by a process is used for buffering to allow the system to react more quickly. As a result, the output from the free command might be confusing. Listing
4.8 shows an example.

# Listing 4.8 Output of the free Command

| total | used | free | shared | buffers | cached |
| Mem: | 127808 | 124668 | 3140 | 105668 | 3264 | 65716 |
| -/+ buffers/cache: | | | 55688 | 72120 | | |
| Swap: | 265032 | 20504 | 244528 | | |

You see in the free output that there is a total of 127,808KB (128MB) of memory but only 3140KB is listed as free. Some of the memory usage is normal but much of it is due to the Linux use of chip memory for buffers and cache. The -/+ buffers/cache line shows the memory used and free (respectively), not counting disk cache—in other words, it reflects memory used by the kernel, programs, and data, but not memory used by buffers and disk cache. The best indicator of whether you need more memory is the swap usage displayed. In this example, the system is using only 20,504KB of 265,032KB of the available swap space. Since so little swapping is being done, it is clear that this system has sufficient memory—at least for the current level of operations.

```
umask [-S] [mode]
```

The umask command sets the permission mode assigned to a file created by the initiating user. The mode is interpreted as octal if it begins with a number and symbolic if it begins with a letter. To print the current umask as octal, simply call umask with no arguments. The umask command may be run with only a -S argument if you want the output in symbolic-mode.

# uname

```
uname [options]
```

The uname command prints out system information including the hardware type, the hostname, the operating system's name, release, and version number, and the processor type.

# uptime

```
uptime
```