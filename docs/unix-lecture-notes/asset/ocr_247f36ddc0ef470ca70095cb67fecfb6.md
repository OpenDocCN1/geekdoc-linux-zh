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