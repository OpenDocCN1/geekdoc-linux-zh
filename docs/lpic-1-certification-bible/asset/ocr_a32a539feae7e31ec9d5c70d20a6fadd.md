The -w option is useful for discovering the location of man page entries. Using this option for the crontab utility produces the following.

```
```
# man -w crontab
/usr/man/man1/crontab.1.gz
```
```

Be sure to know the search options and their function. These include -a, -K, and -k.

# ## Searching man page sections

Linux man page information exists in a collection of files. These files are grouped into sections, with each section containing a specific type of information. Table 7-2 lists the sections and their uses.

Table 7-2 Man Page Sections

| Section | Use |
| :--- | :--- |
| 1 | User commands and applications |
| 2 | System calls and kernel errors |
| 3 | Library calls |
| 4 | Device drivers and network protocols |
| 5 | Standard file formats |
| 6 | Games and demonstrations |
| 7 | Miscellaneous files and documents |
| 8 | System administration commands |
| 9 | Obscure kernel specs and interfaces |

When an argument is passed to the man command, the sections are searched in a specific order and the first match is returned. The default search order is as follows: 1, 8, 2, 3, 4, 5, 6, 7, 9.

It is also possible to specify the man page section to search. If you wish to search section five for information on the crontab utility, you would use the following command:

```
```
# man 5 crontab
```
```