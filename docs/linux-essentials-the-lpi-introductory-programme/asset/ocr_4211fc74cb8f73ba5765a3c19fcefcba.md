You can get locate to return existing files only by using the "-e" option, but this negates locate's speed advantage.

The updatedb program constructs the database for locate. Since this may take considerable time, your system administrator usually sets this up to run when the system does not have a lot to do, anyway, presumably late at night.

The cron service which is necessary for this will be explained in detail in Advanced Linux. For now, remember that most Linux distributions come with a mechanism which causes updatedb to be run every so often.

As the system administrator, you can tell updatedb which files to consider when setting up the database. How that happens in detail depends on your distribution: updatedb itself does not read a configuration file, but takes its settings from the command line and (partly) environment variables. Even so, most distributions call updatedb from a shell script which usually reads a file like /etc/updatedb.conf or /etc/sysconfig/locate, where appropriate environment variables can be set up.

You may find such a file, e.g., in /etc/cron.daily (details may vary according to your distribution).

You can, for instance, cause updatedb to search certain directories and omit others; the program also lets you specify "network file systems" that are used by several computers and that should have their own database in their root directories, such that only one computer needs to construct the database.

An important configuration setting is the identity of the user that runs updatedb. There are essentially two possibilities:

+   - updatedb runs as root and can thus enter every file in its database. This also means that users can ferret out file names in directories that they would not otherwise be able to look into, for example, other users' home directories.

+   - updatedb runs with restricted privileges, such as those of user nobody. In this case, only names within directories readable by nobody end up in the database.

The slocate program—an alternative to the usual locate—circumvents this problem by storing a file's owner, group and permissions in the database in addition to the file's name. It outputs a file name only if the user who runs slocate can, in fact, access the file in question. slocate comes with an updatedb program, too, but this is merely another name for slocate itself.

In many cases, slocate is installed such that it can also be invoked using the locate command.

# Exercises

6.25 [1] README is a very popular file name. Give the absolute path names of all files on your system called README.

6.26 [2] Create a new file in your home directory and convince yourself by calling locate that this file is not listed (use an appropriately outlandish file name to make sure). Call updatedb (possibly with administrator privileges). Does locate find your file afterwards? Delete the file and repeat these steps.

6.27 [1] Convince yourself that the slocate program works, by searching for files like /etc/shadow as normal user.