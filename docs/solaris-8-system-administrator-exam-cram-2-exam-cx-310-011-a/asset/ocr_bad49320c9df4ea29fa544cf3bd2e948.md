**sgml** are passed through an SGML preprocessor before being formatted by the **nroff** command.

Any searches for a man page are basically brute force—that is, each directory containing man pages is searched until the specified man page is located. To speed up displaying and searching, you can generate and store a preformatted version of the man pages. The preformatted version is used whenever possible. As part of the preformatting process, an index of man page keywords is also generated. This index is referred to as the *windex* database. The **catman(1M)** command formats the man pages and generates the windex database. Note that depending on the speed of the system CPU and current load, the **catman** command might take a significant amount of time to format all the man pages.

In addition, having the windex database enables you to search the man pages for keywords and files. The following example shows using the **-f** command-line argument to search the man pages for references to the /etc/passwd file and the **-k** command-line argument to search for the keyword *passwd*:

```
```text
# man -f /etc/passwd
passwd          passwd (1)          - change login password and
                                      password attributes
                                      password file

passwd          passwd (4)          - password file

# man -k passwd
d passwd        d passwd (4)       - dial-up password file
getpw           getpw (3c)          - get passwd entry from UID
kpasswd         kpasswd (1)         - change a user's Kerberos
                                      password
nispasswd       nispasswd (1)       - change NIS+ password information
nispasswd       rpc.nispasswd (1m) - NIS+ password update daemon
passwd          passwd (1)          - change login password and
                                      password attributes
passwd          passwd (4)          - password file
pwconv          pwconv (1m)         - installs and updates
                                      /etc/shadow file information
                                      from /etc/passwd
rpc.nispasswd   rpc.nispasswd (1m) - NIS+ password update daemon
rpc.ypasswdd    rpc.ypasswdd (1m)  - server for modifying NIS
                                      password file
yppasswd        yppasswd (1)      - change your network password
                                      in the NIS database
yppasswdd       rpc.yppasswdd (1m) - server for modifying
                                      NIS password file
#
```
```

You can use the **-d** command-line argument to view the search process as the **man** command attempts to locate the specified man page. The following example searches the windex database. All available sections are identified in the /usr/share/man/man.cf file as a list of section identifiers defined as the contents of the **MANSECTS** variable. Each section identifier is appended