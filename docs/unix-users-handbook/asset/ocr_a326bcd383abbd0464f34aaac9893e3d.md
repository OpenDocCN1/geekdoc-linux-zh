other password sources, including the NIS maps passwd.byname and passwd.bygid and the NIS+ table passwd. Programs use the getpwnam(3C) routines to access this information.

Each passwd entry is a single line of the form:

```text
username:password:uid:gid:gcos-field:home-dir:login-shell
```

where

We haven’t yet covered some of the commands used in this example, however, all you need to know is that a **passwd.1** and a **passwd.4** were found under the “man” pages.

The “man” page for **passwd** from section 1 is the same as the one used in an earlier example. The “man” page for **passwd** from section 4 is for the **/etc/passwd** file. These are two different “man” pages, one for the **passwd** command and one for the **/etc/passwd** file. It is not uncommon to have multiple “man” pages for the same keyword. By default, the first section in which an occurrence of a “man” page appears is used if no section number is specified.

Some UNIX variants, such as Linux, use a capital “S” for specifying the section number. In our example we used a lowercase “s.” As I will point out throughout the book there are many differences among UNIX variants for the ways in which commands are used, the outputs of commands, and in some cases the commands themselves. Please keep in mind that you may encounter such differences in your work, so don’t hesitate to use the “man” pages on your system as a reference.

Rather than issuing the **find** command to see what “man” pages cover the **passwd** command, we could have used the **man** command with the “-k” option. This “-k” option combined with a *keyword*, such as *password* in our example, searches all the “man” page descriptions for *passwd*. One-line summaries are produced wherever *passwd* is found. The following example shows what is produced for such a *keyword* search:

```
# man -k passwd

d_passwd          d_passwd (4) - dial-up password file
getpw             getpw (3c) - get passwd entry from UID
```