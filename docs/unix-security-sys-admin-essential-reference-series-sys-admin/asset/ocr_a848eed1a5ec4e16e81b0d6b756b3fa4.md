`-u units` lists all users who have not logged on for more than `units`. Displayed fields are `time_last_login`, `tty_last_login`, `host_last_login`, and `unsuccessful_login_count`.

`units` is a number optionally followed by one of the letters M, h, d, w, or m, where M stands for minutes, h for hours, d for days, w for weeks, and m for month. The specified number is calculated in that unit and converted into seconds.

All conditions must be satisfied for an entry to match, and only one of the flags l, r, or u can be specified. If no flag is specified, -10 is assumed. user may be one or more user names, separated by blanks. If none is given, all user entries are checked.

# Listing 8.2 (continued)

```
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
```