structures represent the same i-node, by testing both the device IDs and i-numbers:

```
```
#define SAME_INODE(s1, s2)  ((s1).st_dev == (s2).st_dev &&\
                             (s1).st_ino == (s2).st_ino)
```
```

We’ll use this macro twice in the getcwdx function:

```
```c
char *getcwdx(void)
{
    struct stat stat_child, stat_parent, stat_entry;
    DIR *sp = NULL;
    struct dirent *dp;
    struct pathlist_node *head = NULL;
    int dirfd = -1, rtn;
    char *path = NULL;

    ec_neg1( dirfd = open(".", O_RDONLY) )
    ec_neg1( lstat(".", &stat_child) )
    while (true) {
        ec_neg1( lstat("..", &stat_parent) )

        /* change to parent and detect root */
        if (((rtn = chdir("..")) == -1 && errno == ENOENT) ||
            SAME_INODE(stat_child, stat_parent)) {
            if (head == NULL)
                ec_false( push_pathlist(&head, ".") )
                ec_null( path = get_pathlist(head) )
                EC_CLEANUP
        }
        ec_neg1( rtn )

        /* read directory looking for child */
        ec_null( sp = opendir(".") )
        while (errno = 0, (dp = readdir(sp)) != NULL) {
            ec_neg1( lstat(dp->d_name, &stat_entry) )
            if (SAME_INODE(stat_child, stat_entry)) {
                ec_false( push_pathlist(&head, dp->d_name) )
                break;
            }
        }

        if (dp == NULL) {
            if (errno == 0)
                errno = ENOENT;
            EC_FAIL
        }
        stat_child = stat_parent;
    }
}
```
```