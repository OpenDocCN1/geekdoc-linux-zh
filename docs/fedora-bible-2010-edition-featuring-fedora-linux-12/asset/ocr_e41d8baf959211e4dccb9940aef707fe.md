so you can page through the information.) Here is an example (if you haven’t stored your password, you will be prompted to enter your password before you see any output):

```
```
# mysqladmin -u root -p variables | less
```

| Variable_name | Value |
| :--- | :--- |
| auto_increment_increment | 1 |
| auto_increment_offset | 1 |
| autocommit | ON |
| automatic_sp_privileges | ON |
| back_log | 50 |
| basedir | /usr/ |
| ... | ... |
| version | 5.1.39 |
| version_comment | Source distribution |
| version_compile_machine | i386 |
| version_compile_os | redhat-linux-gnu |
| wait_timeout | 28800 |
| warning_count | 0 |
```

If you decide that the option and variable settings that come with the default MySQL system don’t exactly suit you, you don’t have to start from scratch. Sample my.cnf files that come with the mysql package let you begin with a set of options and variables that are closer to the ones you need.

# Using sample my.cnf files

Sample my.cnf files are available in the /usr/share/doc/mysql-server* directory. To use one of these files, do the following:

+   1.  Keep a copy of the old my.cnf file:

```
```
# mv /etc/my.cnf /etc/my.cnf.old
```
```

+   2.  Copy the sample my.cnf file you want to the /etc/my.cnf file. For example, to use the my-medium.cnf file, type the following:

```
```
# cp /usr/share/doc/mysql-server*/my-medium.cnf /etc/my.cnf
```
```

+   3.  Edit the new /etc/my.cnf file (as root user), using any text editor, to further tune your MySQL variables and options.

The following list describes each of the sample my.cnf files.