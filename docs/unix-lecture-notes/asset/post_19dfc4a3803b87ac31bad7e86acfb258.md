
over in its cybergrave, and as far as UNIX is concerned, the new user is now the inadvertent owner. There is nothing we can do to prevent this.

What about group names? It turns out that a similar database, similar functions, and similar problems exist for groups. The /etc/group file lists all of the groups in the system, together with the users who are in each group. The file has an entry for each group consisting of the group name, the group password, the group-id and a comma-separated list of user-names, such as

```
root::9:root
other::1
bin::2:root,bin,daemon
sys::3:root,bin,sys,adm
staff::4:tbw,snw
```

From the list above you can see that root belongs to more than one group. In general, users can belong to more than one group. The primary group of a user is the group specified in the password file entry for that user. When a user creates a file, the user's primary group is made the group of the file. The owner of a file can change the group of a file with the chgrp command.

The getgrgid() system call, given a group-id, searches the list of groups and returns a pointer to the group structure of the group whose group-id matches, or NULL if no such group is found. Similarly, the getgrnam() function searches the group database by name and returns a pointer to the group structure that matches that name, or NULL. The group structure is defined in /usr/include/grp.h as

```
struct group {
    char *gr_name;      /* group name */
    char *gr_passwd;   /* group password */
    gid_t gr_gid;      /* group ID */
    char **gr_mem;     /* group members */
};
```

It is easy to write a function to convert group-ids to group-names, provided that such groups have names. The same arguments about passwords apply to groups; it is possible that the group-id will not resolve to a correct group name.

## 3.10.4 Formatting Time

In Chapter 2, we used ctime() to format time values. Here we will use strftime() and localtime() together, so that our program can behave more closely to the real ls program. The real ls program formats times differently depending upon the user's locale. In addition, for files whose time of last modification is not "recent", the format is different. The definition of "recent" is six months or less. Of course six months is different at different times of the year, so this is an approximate definition. We will use the financial sector's definition of six months – 182 days.

For files that are not recent, ls displays the month name, the day of the month, and the year. For recent files, it displays the month, the day of the month, and the hour and minute. The exact format

depends upon the locale settings. We will put this logic into a function named get_date_no_day(), since it never displays the day of the week. this function is given a time_t value and produces a pointer to a statically allocated string as its return value. If that value is not copied before the function is called again, it will be overwritten. The function's logic is

- 1. Check if the file is recent by comparing current_time - given_time to the number of seconds in 182 days.
- 2. Create a struct tm from the given_time value.
- 3. If the file is not recent, format it in the format MMM DD YYYY.
- 4. If the file is recent, first try to format it using the user's locale settings.
- 5. If that fails, format it using the format MMM DD HH:MM

The function is shown in the listing below.

```
char* get_date_no_day( time_t timeval )
{
    const int sixmonths = 15724800; /* number of secs in 182 days */
    static char outstr[200];
    struct tm *tmp;
    time_t current_time = time(NULL);
    int      recent = 1;

    if ( ( current_time - timeval ) > sixmonths )
        recent = 0;

    tmp = localtime(&timeval);
    if (tmp == NULL) {
        perror("get_date_no_day: localtime");
    }

    if ( ! recent ) {
        strftime(outstr, sizeof(outstr), "%b %e %Y", tmp);
        return outstr;
    }
    else if (strftime(outstr, sizeof(outstr), "%c", tmp) > 0)
        return outstr+4;
    else {
        printf("error with strftime\n");
        strftime(outstr, sizeof(outstr), "%b %e %H:%M", tmp);
        return outstr;
    }
}
```
