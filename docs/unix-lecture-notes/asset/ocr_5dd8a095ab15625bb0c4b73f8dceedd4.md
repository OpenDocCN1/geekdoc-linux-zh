```
```c
strcat(abs_pathname, "/");
height--;
}
else  // must be at root
    strcat(abs_pathname, "/");
}
/*************************************************************/
void ino_to_name(ino_t inode_to_find, dev_t devnum,
                 char *name, int buflen)
{
    DIR             *dir_ptr;
    struct dirent   *direntp;
    struct stat      statbuf;

    if ((NULL == (dir_ptr = opendir(".")))) {
        perror(".");
        exit(1);
    }

    while ((direntp = readdir(dir_ptr)) != NULL) {
        if (-1 == stat(direntp->d_name, &statbuf)) {
            fprintf(stderr, "could not stat");
            perror(direntp->d_name);
            exit(1);
        }
        if ((statbuf.st_ino == inode_to_find) &&
            (statbuf.st_dev == devnum)) {
            strncpy(name, direntp->d_name, buflen);
            name[buflen - 1] = '\0';  // just in case
            closedir(dir_ptr);
            return;
        }
    }
    fprintf(stderr, "Error looking for i-node %d\n",
            inode_to_find);
    exit(1);
}

/*************************************************************/
int get_deviceid_inode(const char *fname, dev_t *dev_id,
                       ino_t *inum)
{
    struct stat info;
    if (stat(fname, &info) == -1) {
        fprintf(stderr, "Cannot stat");
        perror(fname);
        return -1;
    }
    *inum = info.st_ino;
    *dev_id = info.st_dev;
    return 0;
}
```
```

This concludes the implementation of the pwd command.