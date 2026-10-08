2. The same man page from a Sun workstation is quite different:

```
% man mkdir
MKDIR(1)                USER COMMANDS                MKDIR(1)
```

NAME

```
mkdir - make a directory
```

SYNOPSIS

```
mkdir [-p] dirname...
```

DESCRIPTION

mkdir creates directories. Standard entries, '.', '..', for the directory itself, and '..' for its parent, are made automatically.

- -p flag allows missing parent directories to be created as needed.

With the exception of the set-gid-bit, the current umask(2V) determines the mode in which directories are created. The new directory inherits the set-gid bit of the parent directory. Modes may be modified after creation by chmod(2V).

mkdir requires permission in the parent directory.

SEE ALSO

chmod(1V), rm(1), mkdir(2V), umask(2V)

Sun Release 4.1                Last change: 22 August 1989

Notice that there is a new flag in this section of mkdir, the -p flag. Importantly, that the flag is shown in square brackets within the SYNOPSIS section. By convention, square brackets in this section mean that the flag is optional. You can see that the engineers at Sun have a very different idea about what commands might be worth viewing!

+   3. One I always forget on Sun systems is the command that lets me format a floppy disk. That's exactly where the apropos comes in:

```
% apropos floppy
- disk driver for Floppy Disk Controllers
fd(4S)
```

That's not what I want, unfortunately. Because it's in Section 4 (note that the word in parentheses is 4S, not 1), this document will describe the disk driver rather than any command to work with floppy disks.

I can look up disk command instead:

```
% -k disk
acctdisk, acctdusg, accton, acctwmp (8) - overview of accounting and - create a diskless network bootable NFS client on
misecellaneous accounting commandsnadd_client (8)
```

![](bbox=[0.065, 0.883, 0.137, 0.963])