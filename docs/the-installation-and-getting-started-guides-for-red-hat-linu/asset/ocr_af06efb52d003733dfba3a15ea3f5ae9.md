# Standard Users

Table 133 lists the standard users set up by the installation process (this is essentially the /etc/passwd file). The group id (GID) in this table is the primary group for the user. See User Private Groups for details on how groups are used.

| User | UID | GID | Home Directory | Shell |
|---|---|---|---|---|
| root | 0 | 0 | /root | /bin/bash |
| bin | 1 | 1 | /bin |  |
| daemon | 2 | 2 | /sbin |  |
| adm | 3 | 4 | /var/adm |  |
| lp | 4 | 7 | /var/spool/lpd |  |
| sync | 5 | 0 | /sbin | /bin/sync |
| shutdown | 6 | 0 | /sbin | /sbin/shutdown |
| halt | 7 | 0 | /sbin | /sbin/halt |
| mail | 8 | 12 | /var/spool/mail |  |
| news | 9 | 13 | /var/spool/news |  |
| uucp | 10 | 14 | /var/spool/uucp |  |
| operator | 11 | 0 | /root |  |
| games | 12 | 100 | /usr/games |  |
| gopher | 13 | 30 | /usr/lib/gopher-data |  |
| ftp | 14 | 50 | /home/ftp |  |
| nobody | 99 | 99 | / |  |

Figure 11-1: Standard Users