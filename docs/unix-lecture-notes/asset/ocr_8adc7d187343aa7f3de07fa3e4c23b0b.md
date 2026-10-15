```
Listing ls.c Version 2
void print_file_status( char *, struct stat *);
void mode2str( int , char [] );
char * get_date_no_day( time_t * time );
char * uid2name( uid_t );
char * gid2name( gid_t );
void ls(char [], int);

int main(int argc, char *argv[])
{
    int i = 1;

    if ( argc == 1 )    // no arguments; use .
        ls( HERE );
    else
        while ( i < argc ){
            printf("%s:\n", argv[i]);
            ls( argv[i], 1 );
            i++;
        }
}

// Does not check whether entries are files or directories
// or . files
void ls( char dirname[], int do_longlisting )
{
    DIR           *dir_ptr;    // directory stream
    struct dirent *direntp;    // holds one entry
    struct stat   info;        // stores stat results

    if ( ( dir_ptr = opendir( dirname ) ) === NULL )
        // could not open — maybe it was not a directory
        fprintf(stderr,"ls1: cannot open %s\n", dirname);
    else {
        while ( ( direntp = readdir( dir_ptr ) ) !== NULL ) {
            if ( do_longlisting ) {
                if ( lstat(direntp->d_name, &statbuf) === -1 ) {
                    perror(direntp->d_name);
                    continue; // stat call failed but we go on
                }
                print_file_status(direntp->d_name, &statbuf);
            }
            else // not long — just print name
                printf("%s\n", direntp->d_name);
        }
        closedir(dir_ptr);
    }
}

void print_file_status( char *filename , struct stat *info_p )
{
    char      modestr[11];
    ssize_t count;
    char      buf[NAME_MAX];
```