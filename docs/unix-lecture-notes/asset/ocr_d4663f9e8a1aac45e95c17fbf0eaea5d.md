```
31 void show_info( struct utmp *utbufp )
32 // displays the contents of the utmp struct only if a user
33 // login, with time in human readable form, and host if
34 // not null
35 {
36     if ( utbufp->ut_type != USER_PROCESS )
37         return;
38
39     printf("% -8s", utbufp->ut_name); /* the logname */
40     printf("_");
41     printf("% -8s", utbufp->ut_line); /* the tty     */
42     printf("_");
43     show_time( utbufp->ut_time );      /* login time  */
44     printf("_");
45     if ( utbufp->ut_host[0] != '\0' ) /* the host    */
46         printf("_(%)s", utbufp->ut_host);
47     printf("\n");
48 }
49
50 void show_time( long timeval )
51 // displays time in a format fit for human consumption
52 // uses ctime to build a string then picks parts out of it
53 // Note: %12.2s prints a string 12 chars wide and LIMITS
54 // it to 12 chars.
55 {
56     char* timestr = ctime(&timeval);
57     // string looks like "Sat Sep  3 16:43:29 EDT 2011"
58
59     // print 12 chars starting at char 4
60     printf("%12.12s", timestr + 4 );
61 }
```

# 2.6.7 A Third Version of who

The preceding versions of who read the data from the utmp file using the read() system call, reading one utmp struct at a time. An alternative method of accessing the data in the file is to take advantage of a data abstraction layer that the API makes available. When we did the man page search for man pages related to the utmp file, we ignored the functions found on the page named getutent:

+   endutent [getutent] (3) - access utmp file entries
+   getutent (3) - access utmp file entries
+   getutid [getutent] (3) - access utmp file entries
+   getutline [getutent] (3) - access utmp file entries
+   pututline [getutent] (3) - access utmp file entries
+   setutent [getutent] (3) - access utmp file entries
+   utmpxname [getutent] (3) - access utmp file entries