```
FTSENT *fts_read(FTS *ftsp);
FTSENT *fts_children(FTS *ftsp, int options);
int     fts_set(FTS *ftsp, FTSENT *f, int options);
int     fts_close(FTS *ftsp);
```

The paradigm for using fts is that we begin by calling fts_open(), passing an array of strings representing the roots of trees that we wish to traverse, an integer encoding options, and a function to be used for determining the order in which files are visited. It returns a handle, i.e., a pointer to an FTS structure that is then passed to fts_read(). Each time that fts_read() is called, it visits a file. Each file in the tree is visited just once, except for directories, which are visited before and after their children. fts_read() returns a pointer to an FTSENT structure for each file that it visits. Files and FTSENT structures are in one-to-one correspondence. FTSENT structures have a member that allows them to be linked together; the function fts_children() returns a pointer to a linked list of these, representing all of the children in a directory, exactly which will be explained below. The fts_set() function allows a file to be reprocessed after it has been returned by a call to fts_read(). When one is completely finished processing the directory tree passed to fts_open(), it should be closed with fts_close().

There is no need to know the internal structure of a DIR structure because the application should treat it opaquely. However, we do need to know the content of the FTSENT structure, because that is what characterizes each visited file. The two structures are defined in the header file <fts.h>, found in the standard directory, /usr/include. Their definitions (omitting some macros here) are

```
typedef struct {
    struct _fts ent *fts_cur;        /* current node */
    struct _fts ent *fts_child;      /* linked list of children */
    struct _fts ent **fts_array;     /* sort array */
    dev_t fts_dev;                   /* starting device # */
    char *fts_path;                  /* path for this descent */
    int fts_rfd;                     /* fd for root */
    int fts_pathlen;                 /* sizeof(path) */
    int fts_nitems;                  /* elements in the sort array */
    int (*fts_compar) (const void *, const void *); /* compare fn */
    int fts_options;                 /* fts_open options, global flags */
} FTS;
typedef struct _fts ent {
    unsigned short fts_info;         /* flags for FTSENT structure */
    char *fts_accpath;               /* access path */
    char *fts_path;                  /* root path */
    short fts_pathlen;               /* strlen(fts_path) */
    char *fts_name;                  /* filename */
    short fts_namelen;               /* strlen(fts_name) */
    short fts_level;                 /* depth (-1 to N) */
    int fts_errno;                   /* file errno */
    long fts_number;                 /* local numeric value */
    void *fts_pointer;               /* local address value */
    struct fts ent *fts_parent;      /* parent directory */
    struct fts ent *fts_link;        /* next file structure */
```