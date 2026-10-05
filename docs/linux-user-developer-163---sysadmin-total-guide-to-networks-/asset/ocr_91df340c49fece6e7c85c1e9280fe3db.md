```
mtsouk@mail:~$ ls -l /var/run/
total 36
dwxr-xr-x 2 root root      60 Dec 14 21:33 apache2
-rw-r-- 1 root root       5 Dec 14 21:33 atd.pid
dwxr-xr-x 2 avahi avahi    80 Dec 14 21:33 avahi-daemon
-rw-r-- 1 root root       5 Dec 14 21:33 0 Dec 14 21:33 cron.reboot
dwxr-xr-x 2 root root      60 Dec 14 21:33 dbus
-rw-r-- 1 root root      50 Dec 14 21:33 dbus-client.pid
drw-xr-x 25 root root     100 Dec 14 21:33 lock
drw-xr-x 3 root root      60 Dec 14 21:33 log
drw-xr-x 3 root root      80 Dec 14 21:33 mount
drw-xr-x 2 mysql mysql     100 Dec 14 21:33 mysqld
dwxr-xr-x 2 root netdev     40 Dec 14 21:33 network
-rw-r-- 1 root root       20 Dec 14 21:33 php-fpm.sock
rwxr-xr-x 1 www-data www-data  00 Dec 14 21:33 php5-fpm.sock
dwxr-xr-x 2 root root      60 Dec 24 22:04 rpcbind
-rw-r-- 1 root root       50 Dec 26 22:04 spdbid.lock
-rw-r-- 1 root root       50 Dec 26 22:04 rpcbind.pid
```

exiting your current server. After all children do, the parent reloads its configuration, it reports its logs and restarts processes. If the new configuration file has errors, it then will not restart with an error.
HUP signal allows you to restart the server as root but with a big difference: instead of waiting for the child to exit, the WINCH signal gracefully shuts down the child. This allows children to finish serving their current request, and its pid file to stop pooling without quitting. This functionality is very helpful when you are upgrading Apache but it can cause deadlocks and race conditions.

The aforementioned approach is a very common practice and ensures that all server processes follow a similar method to handle instances.
 a Debian 8 system, the process ID of Apache daemon is found in a pid file like:

```
$ cat /var/run/apache2.pid
2937
```

This helps programmers, advanced users and administrators to find the ID of Apache. As you can see in the image above, almost all modern server processes store their IDs inside /var/run.

# The Erlang approach

Erlang is a programming language developed with reliability and high availability in mind. As a result, it offers great support for server processes. In Erlang you can easily develop supervisors that restart after server process crashes. The important thing is that by writing the required Erlang code to supervise a server process, if the server

goes down reason - unexpected events are expected to occur on occasion - the supervisor process will automatically start a new server process!
Another thing to keep in mind is that the supervisor is responsible for the server process without the server process exists without the programmer having to write a single line of code inside the server project files. If you decide to write a server program, you should definitely consider writing it in Erlang in order to take advantage of the capabilities of this programming language.

# Other points of notice

A server process needs to run in hardware because it is not possible to make your hardware reliable and avoid defective.

The daemon() function allows you to manage processes from the controlling unit and run in services. However, it is not defined in POSIX so its implementation might behave differently on platforms. On Linux, Systemd only executes one forked process and does not use daemon(). Therefore, the method presented in this tutorial is better and gives more control over the process so it is supervised.
If you use C, you might need to learn some new functions from a programming language but the general principles are the same. As a rule of thumb, if you are going to write C, make your server process more robust in some way, or better. From Erlang, Go and Perl, which we have gone into in this tutorial, other good alternatives for developing efficient server processes are Python, Ruby, Haskell, Rust, Elixir and C+

Left a quick -l shows the processnIds stored inside the
var/run directory

35