```
/* unlink the file relative to dirfd */
if ( -1 == unlinkat(dirfd, argv[2], 0) ) {
    fprintf( stderr, "could not unlink %s/%s\n", argv[1], argv[2]);
    exit(1);
}
return 0;
```

A descriptor for the directory supplied as the first argument to the program is obtained and stored in dirfd. If this is successful then unlinkat() is called with this descriptor and the name of a file relative to that directory, which is supplied in the second argument to the program.

At the user level, the commands to create new links and remove old links are link and unlink. There is also ln:

```
/usr/sbin/link existing-file new-file
/usr/sbin/unlink file
/usr/bin/ln [ -fns ] source_file [ target ]
```

Consult their man pages for details.

# 3.13.4 Owner and Group of a File

The owner and group of a file are established when the file is created. Remember, you as a user do not create any files. The kernel does. Whether you use the shell to create a file, or vi, or any other program, the program makes a request to the kernel, sooner or later, by calling creat(). The kernel uses the effective-user-id and the effective group-id of the process that issued the creat() call as the owner and group of the file. Sometimes though, it uses the group-id of the parent directory.

The owner and group of a file are changed only by the chown() and chgrp() system calls or their command equivalents. It is very unusual for anyone other than the super-user to change ownership of a file. The chown command or system call changes who owns a file. You cannot change the ownership of a file that you do not already own. You should consult the man pages for the details.

# 3.13.5 Size of a File

A file increases in size as data is written to it using the write() system call. Its size is set to zero by the creat() call. There is no call to reduce the size of a file other than to zero it. In other words, files can grow and can be reset to zero size, but nothing else. The lseek() system call may be used to reposition a file pointer beyond the physical end of the file. This by itself does not change the size of the file. Only actual writes can do that. If data is written to this position, the file's stored size will be increased, with a hole in its middle. The number of disk blocks that it uses will be the number actually required to store data excluding the hole. The following listing illustrates.

```
Listing file_hole.c
#include <stdlib.h>
#include <fcntl.h>
```