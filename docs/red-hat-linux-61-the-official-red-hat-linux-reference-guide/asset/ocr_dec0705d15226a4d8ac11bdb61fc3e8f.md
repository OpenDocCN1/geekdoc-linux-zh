# Chapter 6. Users and Groups

| User | UID | GID | Shell |
| --- | --- | --- | --- |
| gdm | 42 | 42 | /var/qdm | /sbin/nologin |
| mysql | 27 | 27 | /var/lib/mysql | /bin/bash |
| webalizer | 67 | 67 | /var/www/html/usage | /sbin/nologin |
| mailman | 41 | 41 | /var/mailman | /bin/false |
| mailnull | 47 | 47 | /var/spool/mqueue | /sbin/nologin |
| smmsp | 51 | 51 | /var/spool/mqueue | /sbin/nologin |
| squid | 23 | 23 | /var/spool/squid | /dev/null |
| ldap | 55 | 77 | /var/lib/ldap | /bin/false |
| netdump | 34 | 34 | /var/crash | /bin/bash |
| pcap | 77 | 78 | /var/arpwatch | /sbin/nologin |
| ident | 98 | 98 | / | /sbin/nologin |
| privoxy | 100 | 101 | /etc/privoxy | / |
| radvd | 75 | 75 | / | /bin/false |
| fax | 78 | 78 | /var/spool/fax | /sbin/nologin |
| wnn | 49 | 49 | /var/lib/wnn | /bin/bash |

Table 6-1. Standard Groups

# 6.3. Standard Groups

Table 6-2 lists the standard groups configured by an "Everything" installation. Groups are stored under Red Hat Linux in the /etc/group file.

| Group | GID | Members |
| --- | --- | --- |
| root | 0 | root |
| bin | 1 | root, daemon |
| daemon | 2 | root, daemon |
| sys | 3 | root, adm |
| adm | 4 | root, adm, daemon |
| tty | 5 | |
| disk | 6 | root |
| Ip | 7 | daemon, lp |
| mem | 8 | |
| kmem | 9 | |
| wheel | 10 | root |
| mail | 12 | mail |
| news | 13 | news |