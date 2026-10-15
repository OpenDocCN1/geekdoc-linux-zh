The -c option points to the configuration file in the current directory. The program created a new database based on the entries in the configuration file called aide.db.new. The information stored in the database is the base for all checks of the indicated directories. You need to change the name of this database to aide.db, as indicated in the configuration file.

If you want to run a check on the directories indicated in the configuration file, you use the option --check as shown in Listing 7.9.

# LISTING 7.9 Checking the Directories for Changes

```
# ./aide --check -c aide.conf
AIDE found differences between database and filesystem!!
Start timestamp: 2004-08-31 22:04:24
Summary:
Total number of files=3804, added files=1, removed files=0, changed files=1

Added files:
added:/opt/sfw/bin/test_whoami
Changed files:
changed:/opt/sfw/bin
Detailed information about changes:

Directory: /opt/sfw/bin
Mtime  : 2004-08-20 15:35:29        , 2004-08-31 22:03:24
Ctime  : 2004-08-20 15:35:29        , 2004-08-31 22:03:24
```

The output in Listing 7.9 indicates that a new file named test_whoami was found in /opt/sfw/bin and reports the time and date the modification took place.

If you should apply patches or updates to this system or should have installed new software, then you need to update the database as well by using the option -update. If you use this option to update the database, aide reports all files and directories that have changed since the last run, as shown in Listing 7.10.

# LISTING 7.10 Updating the aide Database

```
# ./aide --update -c aide.conf
AIDE found differences between database and filesystem!!
Start timestamp: 2004-08-31 22:12:08
Summary:
Total number of files=3804, added files=1, removed files=0, changed files=1
```