umask of 011 sets the default permissions to 666, where a umask of 022 sets the default permissions to 644.

# ## Establishing User IDs

Just as groups have numbers associated with them, users have numbers associated with them as well. This information also comes from the `/etc/passwd`. Table 8-2 illustrates user numbers.

**TABLE 8-2 USER NUMBERS**

| User | UID |
| :--- | :--- |
| Root | 0 |
| Bin | 1 |
| Daemon | 2 |
| Adm | 3 |
| Lp | 4 |
| Sync | 5 |
| Shutdown | 6 |
| Halt | 7 |
| Mail | 8 |
| News | 9 |
| Uucp | 10 |
| Operator | 11 |
| Games | 12 |
| Man | 13 |
| Postmaster | 14 |
| ftp | 404 |
| Bob | 1000 |
| Veritech | 1001 |
| Nobody | 65534 |