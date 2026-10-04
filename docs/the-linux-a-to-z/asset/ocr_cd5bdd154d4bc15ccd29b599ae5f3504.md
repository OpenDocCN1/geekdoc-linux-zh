```
printf("Named pipe (FIFO)\n");
return 0;

case S_IFBLK:
    printf("Block device special file\n");
    return 1;

case S_IFCHR:
    printf("Character device special file\n");
    return 1;

default:
    printf("Unknown...\n");
    exit(1);
}
}
```

```
fatal(char *mess)
{
    fprintf(stderr, "Error: %s\n", mess);
    exit(1);
}
```

Notice that the program is capable of dealing with multiple file names on the command line. Typical output from the program appears as follows:

```
$ file_status /etc ./book.ps /dev/modem

File name: /dev/modem
File type: Character device special file
Permission bits: 660
File numbers: major 3, minor 65, inode 47638
Link count: 1
Device numbers: major 5, minor 64
File owner ID: 0
File group ID: 14

File name: ./book.ps
File type: Ordinary file
Permission bits: 644
File numbers: major 3, minor 66, inode 34876
Link count: 1
File size: 1049173
File owner ID: 500
```