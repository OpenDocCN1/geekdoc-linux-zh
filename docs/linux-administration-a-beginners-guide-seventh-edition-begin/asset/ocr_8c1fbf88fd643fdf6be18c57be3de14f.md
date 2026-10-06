# CHAPTER 14 Local Security

This will output all of the running programs with their process ID (pid), effective user (euser), real user (ruser), and command name (comm). If the effective user is different from the real user, it is likely a SetUID program.

> Some applications that are started by the root user give up their permissions to run as a privileged user to improve security. The Apache web server, for example, might be started by the root user to bind to TCP port 80 (only privileged users can bind to ports lower than 1024), but then it gives up root permissions and starts all of its threads as an unprivileged user (typically the "nobody","apache","www-data," or "www").

Very rarely, you may need to make a program as SetUID. To do this, use the chmod command. Prefix the desired permissions with a 4 to turn the SetUID bit (Using a prefix of 2 will enable the SetGID bit, which is similar to SetUID, but offers group permissions instead of user permissions.)

For example, if we have a program called myprogram and want to make it SetUID, we would do the following:

```
[root@server ~#] chown root myprogram
[root@server ~#] chmod 4755 myprogram
[root@server ~#] ls -l myprogram
-rwsr-xr-x 1 root 43160 Jul 13 2018 myprogram
```

Ensuring that your system has only the absolute minimum and necessary SetUID programs is a good housekeeping measure. A typical Linux distribution can have several files and executables that are necessarily SetUID. Going from directory to directory to find SetUID programs can be tiresome and error-prone. Instead of doing that manually, you can use the find command, like so:

```
# find / -perm -4000 -ls
```

To search for files that are SetUID, type

```
# find / -type f -perm -2000 -ls
```

To search for both SetUID and SetGID files with one find command and view the oct mode for the file permissions using the stat command,

```
# find / -type f \ -perm -4000 -o -perm -2000 \ | xargs stat -c '%A %a %n'
```

# Unnecessary Processes

When stepping through startup and shutdown scripts, you may have noticed that a standard-issue Linux system starts with a lot of processes. The question that needs to be asked is: Do I really need everything I start? You might be surprised by your answer.