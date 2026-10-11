permission checking. This subject is discussed in more detail in Chapter 11, “Permissions and User and Group ID Numbers,” page 403.

The group database APIs are similar to those for the user database. The following functions are declared in <grp.h>:

```
```c
#include <sys/types.h>    XSI
#include <grp.h>

struct group *getgrent(void);
void setgrent(void);
void endgrent(void);

struct group *getgrnam(const char *name);
struct group *getgrgid(gid_t gid);
```
```

The struct group corresponds to the records in /etc/group:

```
```c
struct group {
   char    *gr_name;      /* group name */
   char    *gr_passwd;    /* group password */
   gid_t    gr_gid;       /* group id */
   char    **gr_mem;     /* group members */
};
```
```

The gr_mem field bears some explanation. While declared as a pointer to a pointer (char **), it is best thought of as an array of strings (like argv). The last element in the array is set to NULL. When no members are listed, the first element in the array is NULL.

ch06-groupinfo.c demonstrates how to use the struct group and the gr_mem field. The program accepts a single user name on the command line and prints all group records in which that user name appears:

```
```c
1 /* ch06-groupinfo.c --- Demonstrate getgrent() and struct group */
2
3 #include <stdio.h>
4 #include <sys/types.h>
5 #include <grp.h>
6
7 extern void print_group(const struct group *gr);
8
9 /* main --- print group lines for user named in argv[1] */
10
```
```