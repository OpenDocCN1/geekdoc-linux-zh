
The -m option sorts by modification time, -s, by size, and -l turns on long listings. The program listing below omits the helper functions already displayed in previous versions of ls, as well as almost all comments.

```
Listing ls_fts.c
#include <sys/types.h>
#include <err.h>
#include <errno.h>
#include <fnmatch.h>
#include <fts.h>
#include <string.h>
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/stat.h>
#include <pwd.h>
#include <grp.h>
#include "utils.h"

#define BYTIME 1
#define BYNAME 2
#define BYSIZE 3
#define HERE " "
#define TRUE 1
#define FALSE 0

int entcmp(const FTSENT **a, const FTSENT **b)
{
    return strcoll((*a)->fts_name, (*b)->fts_name);
}

int mtimecmp(const FTSENT **s1, const FTSENT **s2)
{
    return (int) (((*s1)->fts_statp)->st_mtime - ((*s2)->fts_statp)->st_mtime);
}

int szcmp(const FTSENT **s1, const FTSENT **s2)
{
    return (int) (((*s1)->fts_statp)->st_size - ((*s2)->fts_statp)->st_size);
}

void ls ( char dir[], int do_longlisting, int sortflag )
{
    FTS *tree;
    FTSENT *f;
    char *argv[] = { dir, NULL };

    switch ( sortflag ) {
    case BYTIME:
        tree = fts_open(argv, FTS_LOGICAL , mtimecmp);
        break;
    case BYNAME:
        tree = fts_open(argv, FTS_LOGICAL , entcmp);
        break;
```

```
case BYSIZE:
    tree = fts_open(argv, FTS_LOGICAL, szcmp);
    break;
}

if (tree == NULL)
    perror("fts_open");

f = fts_read(tree);
if ( NULL == f ) {
    perror("fts_read");
    return;
}

f = fts_children(tree, 0);
if ( NULL == f )
    if ( errno != 0 )
        perror("fts_children");
    else
        fprintf(stderr, "empty directory\n");

while ( f != NULL ) {
    switch (f->fts_info) {
    case FTS_DNR:  /* Cannot read directory */
        fprintf(stderr, "Could not read %s\n", f->fts_path);
        continue;
    case FTS_ERR:  /* Miscellaneous error */
        fprintf(stderr, "Error on %s\n", f->fts_path);
        continue;
    case FTS_NS:  /* stat() error */
        fprintf(stderr, "Could not stat %s\n", f->fts_path);
        continue;
    case FTS_DP:
        /* Returned to directory for second time as part of
           post-order visit to directory, so skip it. */
        continue;
    }
    if ( do_longlisting )
        print_file_status(f->fts_name, f->fts_statp);
    else
        printf("%s\n", f->fts_name);

    f = f->fts_link;
}
if (errno != 0)
    perror("fts_read");

if (fts_close(tree) < 0)
    perror("fts_close");
}

/*********************  Main Program *********************************/
int main(int argc, char* argv[])
```

```
{
    int longlisting = 0;
    int howtosort  = BYNAME;
    int ch;
    char options[] = ":lms";
    opterr = 0;

    while (TRUE) {
        ch = getopt(argc, argv, options);
        if ( -1 == ch )
            break;
        switch ( ch ) {
        case 'l':
            longlisting = 1;
            break;
        case 'm':
            if ( howtosort != BYSIZE )
                howtosort = BYTIME;
            else {
                printf("usage: %s [-l] [-m|-s] [files]\n", argv[0]);
                return 1;
            }
            break;
        case 's':
            if ( howtosort != BYTIME )
                howtosort = BYSIZE;
            else {
                printf("usage: %s [-l] [-m|-s] [files]\n", argv[0]);
                return 1;
            }
            break;

        case '?':
            printf("Illegal option ignored.\n");
            break;
        default:
            printf("??? getopt returned character code 0%o ??\n", ch);
            break;
        }
    }

    if ( optind == argc )    /* no arguments; use . */
        ls( HERE, longlisting, howtosort );
    else
        /* for each command line argument, display file */
        while ( optind < argc ) {
            ls( argv[optind], longlisting, howtosort );
            optind++;
        }
    return 0;
}
```

## Notes.

- The main program does the option parsing and prevents the user from choosing to sort by both size and modification time, because sorting by both implies having to resort the linked list returned by `fts_children()`.
- The main program calls `ls()` for each command line argument rather than assembling them into an array of strings, because `ls()` is designed to display a single directory's contents only.
- The `mtimecmp()` and `szcmp()` functions use arithmetic rather than conditional evaluation. This makes them work faster, but on a non-POSIX system, the time subtraction may not work. Both work by accessing the `stat` structure pointed to by the `FTSENT` structure's `fts_statp` member. No check is made that it is `NULL`.
- `ls()` begins by calling `fts_open()`. It then calls `fts_read()` so that the directory object will be the last object read by a call to `fts_read()`, ensuring that `fts_children()` will return a pointer to the list of children of that directory, if it is non-empty.
- Unlike the previous program, this does not repeatedly call `fts_read()`. It traverses the linked list of `FTSENT` structures until it reaches a `NULL` link and then terminates.

This is just a short overview of the `fts` functions. It does not show how to use the hooks provided to the application inside the `FTSENT` structure.

## Exercise.

A good exercise would be to implement the `du` command using fts, taking advantage of the members of the `FTSENT` structure available to the application, and the parent pointers.
