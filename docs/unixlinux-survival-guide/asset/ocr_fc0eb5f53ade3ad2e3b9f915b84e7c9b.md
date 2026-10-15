```
!/var/adm/wtmp$     # ignore the file /var/adm/wtmp
!/var/cron/log/*   #ignore /var/cron/log
/opt/sfw MyRule    # Solaris specific
/usr/openwin/bin MyRule  # Solaris specific
/usr/dt/bin MyRule  # Solaris specific
/usr/ccs/bin MyRule  # Solaris specific
/usr/ucb MyRule     # Solaris specific
#EOF
```

You can use the example in /usr/local/doc/aide/aide.conf as a starting point, but the file mentioned should not be used as a configuration file as it is. It is just an example. You could use the example in Listing 7.7 as a guide for what needs to be changed, but should use caution because not all modifications apply to all systems. This means not all modifications make sense on all systems. Some entries in the configuration in Listing 7.7 are shown in bold; these require further explanation. The entry @define TOPDIR /HO/aid defines the base directory for aide. The entries database=file:@{TOPDIR}/aide.db and database_out=file:@{TOPDIR}/aide.db.new search for an existing database and create a new one in the indicated directory, respectively. The entry MyRule = p+i+n+u+g+s+b+m+c+md5+sha1 is a defined rule, probably a little paranoid. It runs the following tests: checks the permissions; i the inode that points to the file in question; n the number of links; u the owner of the file, g the group the respective file belongs; s the size of the file; b the number of blocks that the file occupies; m the date the respective file was last modified; c the time the file was last modified; md5 creates an md5 sum; and sha1 a sha1 sum. There is no such thing as total control, but this rule should cover almost all bases. The entry !/var/log/* instructs the program to ignore the subdirectory log in /var.

You simply store the aide executable and the modified configuration file aide.conf in the location pointed to by TOPDIR. Then you need to create the initial database with the --init option of the program, as shown in Listing 7.8.

# LISTING 7.8 Creating the Initial Database

```
# ls
aide aide.conf bu
# ./aide --init -c aide.conf
# ls -l
total 2443
-rwxr-xr-x 1 root other 1093216 Sep 16 2003 aide
-rw-r--r-- 1 root other 2048 Sep 17 2003 aide.conf
-rw------- 1 root other 1380792 Aug 31 20:06 aide.db.new
#
```