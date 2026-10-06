# 90 | Master of Linux Commands

```
root@kemal:~# ls -l fotolar.tar.gz
-rw-r--r-- 1 root root 172687366 Agu 2 09:35 fotolar.tar.gz
root@kemal:~#
```

Finally, lets give /etc -name "*.conf" | xargs ls -l example and finish this section.

```
root@kemal:~# find /etc -name "*.conf" -xargs ls -l
-rw-r--r-- 1 root root 2981 Agu 11 11:07 /etc/adduser.conf
-rw-r--r-- 1 root root 7135 Agu 1 23:27 /etc/apache2/apache.conf
-rw-r--r-- 1 root root 315 Agu 1 23:27 /etc/apache2/conf-available/
harset.conf
-rw-r--r-- 1 root root 127 Ten 29 2013 /etc/apache2/conf-available/j
avescript-common.conf
-rw-r--r-- 1 root root 3224 Agu 1 23:27 /etc/apache2/conf-available/l
ocalized-error-pages.conf
-rw-r--r-- 1 root root 189 Agu 1 23:27 /etc/apache2/conf-available/o
ther-access-log.conf
-rw-r--r-- 1 root root 2190 Agu 1 23:27 /etc/apache2/conf-available/s
ecurity.conf
-rw-r--r-- 1 root root 455 Agu 1 23:27 /etc/apache2/conf-available/s
erve-alias.conf
lrwxxr-x 1 root root 30 Kas 22 10:35 /etc/apache2/conf-enabled/cha
rset.conf -> ../conf-available/charset.conf
```

§