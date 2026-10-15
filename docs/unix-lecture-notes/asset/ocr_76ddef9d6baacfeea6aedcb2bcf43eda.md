```
/**************************************************************/
void print_path( char * abs_pathname, ino_t this_inode )
{
    ino_t            parent_inode ;
    char             its_name[BUFSIZ];

    // get inumber of parent
    get_ino("..", &parent_inode );

    // At root iff parent inum == cur inum
    if ( parent_inode != this_inode ) {
        chdir( ".." );   // cd up to parent
        // get filename of current file
        inum_to_name(this_inode, its_name, BUFSIZ);
        // recursively get path to parent directory
        print_path(abs_pathname, parent_inode );
        strcat(abs_pathname, "/");
        strcat(abs_pathname, its_name );
    }
    else
        strcat( abs_pathname, "/");
}

/**************************************************************/
void inum_to_name(ino_t inode_to_find , char *namebuf,
                   int buflen)
{
    DIR             *dir_ptr;
    struct dirent   *direntp;

    dir_ptr = opendir( "." );
    if ( dir_ptr == NULL ) {
        perror( "." );
        exit(1);
    }

    // search directory for a file with specified inum
    while ( ( direntp = readdir( dir_ptr ) ) != NULL )
        if ( direntp->d_ino == inode_to_find ) {
            strncpy( namebuf, direntp->d_name, buflen);
            namebuf[buflen-1] = '\0';
            closedir( dir_ptr );
            return;
        }
    fprintf(stderr, "\nError looking for i-node number %d\n",
            inode_to_find);
    exit(1);
}

/**************************************************************/
int get_ino( char *fname, ino_t *inum )
{
    struct stat info;
```