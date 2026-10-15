```
```c
mode2str( info_p->st_mode, modesstr );
printf ( "%s" , modesstr );
printf ( "%4d " , (int) info_p->st_nlink);
printf ( "%-8s " , uid2name(info_p->st_uid) );
printf ( "%-8s " , gid2name(info_p->st_gid) );
printf ( "%8ld " , (long)info_p->st_size );
printf ( "%12s " , get_date_no_day(info_p->st_mtime));
printf ( "%s" , filename );
if ( S_ISLNK(info_p->st_mode) ) {
    if ( -1 == (count = readlink(filename, buf, NAME_MAX-1)) )
        perror("print_file_status: ");
    else {
        buf[count] = '\0';
        printf("-->%s", buf);
    }
}
printf("\n");
}

// Given user-id, return user-name if possible
char *uid2name ( uid_t uid )
{
    struct passwd *pw_ptr;
    static char numstr[10];  // must be static!

    if ( ( pw_ptr = getpwuid( uid ) ) == NULL ) {
        // convert uid to a string; using sprintf is easiest
        sprintf(numstr,"%d", uid);
        return numstr;
    }
    else
        return pw_ptr->pw_name;
}

char *gid2name ( gid_t gid )
{
    struct group *grp_ptr;
    static char numstr[10];

    if ( ( grp_ptr = getgrgid(gid) ) == NULL ) {
        // convert gid to string
        sprintf(numstr,"%d", gid);
        return numstr;
    }
    else
        return grp_ptr->gr_name;
}
```
```

# What Is Still Wrong?

+   - It still treats all arguments like directories and displays an error if given a regular file.