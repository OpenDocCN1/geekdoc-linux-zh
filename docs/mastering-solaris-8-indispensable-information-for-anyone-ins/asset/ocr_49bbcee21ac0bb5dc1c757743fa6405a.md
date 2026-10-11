# NIS and NIS+

The Network Information Service (NIS) was developed by Sun Microsystems to simplify the task of administering common files that were controlled and maintained in a central database. Clients had to contact the database server to retrieve information. NIS was given the task of keeping system-independent configuration files such as /etc/passwd current. Many of today's networks include systems supplied by different manufacturers and may run different versions of Unix or Solaris. They do have certain commonalities, however, such as directories.

One had to rename the service once called Yellow Pages because another corporation owned the copyright on the name. The names of the NIS utilities still bear a resemblance to the old name because they are still prefixed with yp. For example, ypcat displays an NIS database, and ypmatch searches for matching information.

When a utility maps a number to the corresponding group name, it queries the NIS server when it sees a + sign, as in the following example:

```
$ cat /etc/group
+::*:*
$
```

You can display the group database using the ypcat utility as in the following example:

```
$ ypcat group
sos::153:barrie,kay,steve,wendel
```

You can also search for a particular group using the ypmatch utility:

```
$ ypmatch sos group
sos::153:barrie,kay,steve,wendel
```

Filtering the output of ypcat through grep can retrieve the same information. The most efficient way, however, is to use ypmatch simply because it uses a single process and searches the database directly. The NIS database name is the same as the simple filename. It is not the full path name of the file that it replaces. The ypmatch utility will work only on the key for the table or group name. If you must match on members of the group or other fields of the map, you must use grep with ypcat.

The system administrator sets up and maintains the NIS databases. Most users on a single-user Solaris system seldom work directly with NIS and are unaware that it manages system configuration files.