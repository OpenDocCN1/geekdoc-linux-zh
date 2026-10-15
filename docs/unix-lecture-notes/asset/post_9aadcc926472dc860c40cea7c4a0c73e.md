
# Cannot open foo

Instead we need to first test whether the file is a regular file or a directory. In order to do this, we need to call stat() with the file name, and check whether the file is a directory by using the S_ISDIR() macro on the st_mode member. The following is how the function should start:

```
if ( lstat(dirname, &statbuf) == -1 ) {
    perror(fname);
    return;        // stat call failed so we quit this call
}
else if ( ! S_ISDIR(statbuf.st_mode) ) {
    if ( do_longlisting )
        print_file_status(dirname, statbuf);
    else
        printf("%s\n", dirname);
    return;
}

if ( ( dir = opendir(dirname) ) == NULL )
    fprintf(stderr, "Cannot open %s\n", dirname);
else {
    ...
```

The main program needs to be modified to parse the command line, using the getopt() function that POSIX requires of a compliant UNIX system. We need to include the <unistd.h> header file to use it. For this version we have a single option letter, “l”, but the program can easily be extended to include other options. The main program is in the following listing, and the supporting functions are in the listing that follows it.

```
Listing 1 s.c Final Version of main()

void ls( char dirname[], int do_longlisting );
void print_file_status ( char *fname,
                         struct stat statbuf );
char* mode2str         ( int mode );
char *uid2name         ( uid_t uid );
char *gid2name         ( gid_t gid );

int main(int argc, char *argv[])
{
    int longlisting = 0;
    int ch;
    char options[] = "l";

    opterr = 0;  // turn off error messages by getopt()

    while (1) {
        ch = getopt(argc, argv, options);
```

```
// it returns -1 when it finds no more options
if ( -1 == ch )
    break;
switch ( ch ) {
case 'l':
    longlisting = 1;
    break;
case '?':
    printf("Illegal option ignored.\n");
    break;
default:
    printf ("getopt returned character code 0%o ??\n", ch);
    break;
}
}
if ( optind == argc )    // no arguments; use .
    ls ( ".", longlisting );
else
    while ( optind < argc ){
        ls( argv[optind], longlisting );
        optind++;
    }
return 0;
}
```

The supporting functions follow. Some functions are the same as in the previous version. Those are not listed to save space. A comment indicates this when appropriate.

```
void ls( char dirname[], int do_longlisting )
{
    DIR            *dir;        // pointer to directory struct
    struct dirent  *dp;          // pointer to directory entry
    char           fname[PATH_MAX]; // string to hold path name
    struct  stat   statbuf;      // to store stat results

    /* test if a regular file, and if so, just display it */
    if ( lstat(dirname, &statbuf) == -1 ) {
        perror(fname);
        return;     // stat call failed so we quit this call
    }
    else if ( ! S_ISDIR(statbuf.st_mode) ) {
        if ( do_longlisting )
            print_file_status(dirname, statbuf);
        else
            printf("%s\n", dirname);
        return;
    }

    if ( ( dir = opendir( dirname ) ) == NULL )
```

```
fprintf(stderr,"Cannot open %s\n", dirname);
else {
    printf("\n%s:\n", dirname);
    // Loop through directory entries
    while ((dp = readdir(dir)) != NULL) {
        if (strcmp(dp->d_name,".") == 0 ||
            strcmp(dp->d_name,"..") == 0 )
            // skip dot and dot-dot entries
            continue;

        if ( do_longlisting ) {
            // construct a pathname for the file using the
            // directory name passed to the program and the
            // directory entry
            sprintf(fname,"%s/%s",dirname, dp->d_name);

            // fill the stat buffer
            if (lstat(fname, &statbuf) == -1) {
                perror(fname);
                continue; // stat call failed but we go on
            }
            print_file_status(dp->d_name, statbuf);
        }
        else
            printf("%s\n", dp->d_name);
    }
}
```

```
void print_file_status ( char *dname,
                        struct stat statbuf )
{
    ssize_t count;
    char buf[NAME_MAX];

    /* Print out type, permissions, and number of links */
    printf("%10s", mode2str(statbuf.st_mode));
    printf("%3d", (int) statbuf.st_nlink);

    /* Print out owner's name if it is found using getpwuid() */
    printf(" %-8s", uid2name(statbuf.st_uid));

    /* Print out group name if it is found using getgrgid() */
    printf(" %-8s", gid2name(statbuf.st_gid));

    /* Print size of file */
    printf("%8jd", (intmax_t)statbuf.st_size);

    /* Print time of last modification */
    printf(" %.12s ", get_date_no_day(statbuf.st_mtime));

    /* print file name and if a link, the linked file */
    printf("%s", dname);
```
