be converted to characters as characters. On Linux, neither od, nor cat, nor more will display the contents of a directory.

If you are wondering what system calls might work with directories, the open(), read(), and close() system calls will act on directories because they do not modify the directory, but because a directory has a specific structure, there is not much point to using them. They are not intended to be used with directories. It is better to use the specific system calls or library functions designed to open, read, modify, and close directories.

If you use a man page search to look for man pages that refer to the word "directory" you will find a long list of them. It is best to filter the output of the search, using something like

```
$ man -k directory | grep read
```

which will display just a few entries. You might see, among other things

+   readdir (2) - read directory entry
+   readdir (3) - read a directory
+   readdir (3p)- read a directory
+   readdir_r [readdir] (3p)- read a directory
+   seekdir (3) - set the position of the next
+   readdir() call in the directory stream

Different systems will deliver slightly different sets of man pages, depending on which version of UNIX they are running. All should list the readdir() system call in Section 2, and most should list a call named readdir() in Section 3 or 3P or both. On almost all systems, if you read the man page for readdir() system call in Section 2, it will advise you not to use this system call and instead to use the POSIX library function of the same name. It will refer you to the readdir() C library function whose man page is in Section 3 or 3P. You might need to use a lowercase p in your man command, as in

```
$man 3p readdir
```

Because of the wide variation among the different systems, we cannot know exactly what you will see, but all pages should have, at a minimum the following:

```
SYNOPSIS
    #include <sys/types.h>
    #include <dirent.h>

    struct dirent *readdir(DIR *dir);
DESCRIPTION
    The readdir() function returns a pointer to a dirent structure representing the next directory entry in the directory stream pointed to by dir. It returns NULL on reaching the end-of-file or if an error occurred.
```