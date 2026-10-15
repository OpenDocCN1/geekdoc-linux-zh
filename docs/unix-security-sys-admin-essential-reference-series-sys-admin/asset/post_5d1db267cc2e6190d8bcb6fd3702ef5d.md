
`-u units` lists all users who have not logged on for more than `units`. Displayed fields are `time_last_login`, `tty_last_login`, `host_last_login`, and `unsuccessful_login_count`.

`units` is a number optionally followed by one of the letters M, h, d, w, or m, where M stands for minutes, h for hours, d for days, w for weeks, and m for month. The specified number is calculated in that unit and converted into seconds.

All conditions must be satisfied for an entry to match, and only one of the flags l, r, or u can be specified. If no flag is specified, -10 is assumed. user may be one or more user names, separated by blanks. If none is given, all user entries are checked.

## Listing 8.2 (continued)

```c
if( argv[optind] ){
    char *endptr;
    errno = 0;
    /*
    ** Check if number is not too big for us to handle
    */
    epoch = strtol(argv[optind], &endptr, 10);
    if( errno == ERANGE ){
        fprintf(stderr, "%s: parameter %s out of range\n", Prog, argv[optind]);
        exit(2);
    }
    /*
    ** If parameter epoch doesn't start with a digit or doesn't
    ** entirely consist of digits print an error and give up.
    */
    if( strlen(argv[optind]) == 0
        || strlen(argv[optind]) != strspn(argv[optind], "0123456789") ){
        fprintf(stderr, "%s: parameter '%s' is invalid\n", Prog, argv[optind]);
        exit(3);
    }
}
/*
** Default format is output of the date command
*/
if( format == NULL )
    format = "%c%n";
}else{
    if( format == NULL ){
        /* Just print current time in seconds since epoch */
        printf("%ld\n", epoch);
        return 0;
    }

    /* Convert time to human readable format */
    tmpt = localtime(&epoch);
    strftime(buf, sizeof buf, format, tmpt);
    printf("%s", buf);
    return 0;
}
```

terminallist and hostlist are mapped against unsuccessful terminal or host names if flag -r is specified in the following example.

```
User  FailedDate  Time    Tty     Host
guest1  08-Jul-94 10:30 pts/0 os2box
adm     0   22-Aug-94 16:01 pts/3 9.20.183.155
root    0   29-Aug-94 13:29 hft/0 tiger
richter 0   8-Sep-94 16:58 hft/0 tiger
```

The output of lastlogin -u10 -htiger is as follows.

```
User  FailedDate  Time    Tty     Host
root    0   29-Aug-94 13:29 hft/0 tiger
```

## Time Conversion

/etc/security/lastlog stores the time in seconds since epoch. cvttime.c (Listing 8.2) converts seconds since epoch to a user-readable format, similar to the output of the date command. Invoked without any parameters, it returns the current time in seconds since epoch. An optional flag, -f, determines which parts of the time and date should be printed. The format is the same as for the C library function strftime.

## Logfiles Maintenance

The logins shell script (Listing 8.3) is invoked by cron once a day. It checks if a compressed file for the last month, sulog.MM.Z or wtmp.MM.Z (where MM stands for month), already exists in the directory /var/adm/local. If this file does not exist or was created last year, the corresponding file /var/adm is compressed and stored in directory /var/adm/local. The original is then reduced to size zero. Note that these files must exist for entries to be made.

If the size of /etc/security/failedlogin is greater than zero, the file's content is mailed to the system administrator. The file is then also reduced to size zero.

## Summary

These tools keep the login log files small and also maintain a backup copy of recent months for reference. lastlogin enables system administrators to query user account login data and to automatically monitor user accounts.

## References

+ 1. Wood, Patrick H., and Stephen G. Kochman. *UNIX System Security*, Indianapolis, IN: Hayden Books, 1985.
+ 2. Farrow, Rik. *UNIX System Security*. Reading, MA: Addison Wesley, 1991.
+ 3. IBM. "File Reference (IBM RISC System/6000)", GC23-2200-04. 1988.

## Password Verification
in AIX v4

Thomas Richter

AIX v4 introduces new and expanded tools for controlling system access. It allows system administrators to write their own password verification functions and to extend the system login procedure to call those new functions for user password verification. It lets system administrators specify allowed and denied login times, terminals, and ports for each user and permits an account to be locked after a certain number of failed login attempts. Ports can be monitored independently of accounts: a port may be locked for a specified time period after a failed login attempt and may be shut down completely after exceeding a threshold of failed login attempts in a given interval. A locked port can be enabled automatically after being unused for some time. These features prevent a password cracking program from probing different user IDs on the same port.

With v4, password history is available. The system prevents reuse of passwords within a given time frame and within a cycle of passwords. For example, a password cannot be reused if it is in a list of recently used passwords. The size of the list is configurable, and dictionaries can be specified to check new passwords.

This chapter explores the login configuration and user verification features introduced in v4, then explains how to write and implement system password verification functions.
