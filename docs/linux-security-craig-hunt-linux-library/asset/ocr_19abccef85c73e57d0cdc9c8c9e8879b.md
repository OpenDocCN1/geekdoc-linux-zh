poking tiny holes in your system security. Linux uses the umask configuration setting to control default file permissions. Its usage is

```
umask AAA
```

where AAA is the octal complement of a default permissions mask of 666 (777 for directories). For instance, a umask of 022 would yield a default permission of 644 for files (the result of subtracting 022 from 666). Let's look at an example in Listing 2.4.

# Listing 2.4 umask configuration examples

```
```console
[ramon]$ umask 000
[ramon]$ touch example1
[ramon]$ ls -l example1
-rw-rw-rw- 1 ramon users 0 Sep 25 22:08 example1
[ramon]$ umask 022
[ramon]$ touch example2
[ramon]$ ls -l example2
-rw-r--r-- 1 ramon users 0 Sep 25 22:08 example2
[ramon]$ umask 66
[ramon]$ touch example3
[ramon]$ ls -l example3
-rw------- 1 ramon users 0 Sep 25 22:08 example3
```
```

I recommend that you edit your /etc/profile file to assign a mask of 066 to the root user and assign a mask of 022 to your regular users. This ensures that root-created files have no permissions for group and others, while any other files are created with world-read permissions only.

# Limiting Core Dump Size

A common means for a local user to gain root privileges is to force a setuid/setgid program to dump a core file (upon crashing) in a specific location within the filesystem. By using this method to overwrite arbitrary files anywhere on the server, including /etc/passwd, /etc/hosts.equiv, or .rhosts, intruders can effectively create for themselves a user with root privileges. With today's servers having gigabytes of physical memory available, these core files could potentially fill an entire disk, which would result in a denial of service (DoS) attack for other users relying on the same filesystem.

There is an effective way to keep core files under control. Using the ulimit command, you can control the resource utilization limits of any user, including the maximum size of a core dump file. You should simply set this size to 0, using the following command:

```
 ulimit -c 0
```

You can include this command in the global /etc/profile configuration file also.