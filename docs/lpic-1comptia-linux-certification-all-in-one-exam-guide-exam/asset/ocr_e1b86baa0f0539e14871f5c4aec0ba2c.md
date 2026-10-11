For example, you could limit the tracy user to a maximum of two concurrent logins by entering the following in the file:

```
rtracy hard maxlogins 2
```

You can also use the ulimit command to configure limits on system resources that are applied to programs launched from the shell prompt. The syntax for using ulimit is ulimit options limit

You can use the following options with ulimit:

+   - -c Sets a limit on the maximum size of core files in blocks
+   - -f Sets a limit on the maximum size (in blocks) of files created by the shell
+   - -n Sets a limit on the maximum number of open file descriptors
+   - -t Sets a limit on the maximum amount of cpu time (in seconds) a process may use
+   - -u Sets a limit on the maximum number of processes available to a single user
+   - -d Sets a limit on the maximum size (in KB) of a process' data segment in RAM
+   - -m Sets a limit on the maximum resident size (in KB) of a process in RAM
+   - -s Sets a limit on the maximum stack size (in KB)
+   - -H Sets a hard resource limit
+   - -S Sets a soft resource limit

I then reviewed how you can completely disable user logins to the Linux system. You can use the w command to view a list of all currently logged-in users. You can then use the pkill --KILL --user_name command to brute-force log each user out. At this point, you can disable all future logins by creating a file in /etc named nologin. As long as this file exists, no one but root is allowed to log in.

In addition to disabling user login, another user security–related issue you need to be familiar with is auditing files that have SUID or SGID root permissions set. You can search for files on your Linux system that have SUID permissions set using the following command at the shell prompt as your root user:

```
find / -type f -perm -u+s -ls
```

You can also identify any files with the SGID permission set using the following command:

```
find / -type f -perm -g+s -ls
```

I then shifted our focus to the threat from network attacks. I pointed out that connecting your network to the Internet exposes your Linux systems to a host of network attacks. To mitigate these threats, you need to stay abreast of current threats. One excellent resources to do this include the www.cert.org and http://us-cert.gov web sites.

You should also check your system to see if any unneeded daemons are running. You can do this using the chkconfig and nmap utilities. Unnecessary services can be