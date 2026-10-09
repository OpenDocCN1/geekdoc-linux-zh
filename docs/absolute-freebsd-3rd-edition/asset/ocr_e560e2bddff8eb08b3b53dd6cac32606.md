them started in this order so that my database jail is running before the web server that calls it.

```
jail_list="mariadb httpd"
```

During system shutdown, FreeBSD stops jails in the same order it starts them. Your application might not like that. In my example, I want the web server to turn off before the database backend. I'd rather have a website be flat-out unavailable than have users see the dreaded “database server is kaput” error.

```
jail_reverse_stop=YES
```

If the jail startup order is unimportant, you can start and stop all jails simultaneously.

```
jail_parallel_start="YES"
```

Now you can configure a jail.

# Jail Setup

Now that I have a host, I can install some jails. I'll start with a jail called *mariadb*, for running . . . wait for it . . . MariaDB.

Each jail needs a dedicated root directory. All of my example jails live under /jail. I normally put each jail in a directory named after the jail name—in this case, /jail/mariadb.

Each jail needs a primary IP. It can also have other IPs, as we'll see later, but let's start with one. The jail mariadb gets 203.0.113.51.

Each jail needs an internet hostname, just as if it were a real host. This jail will become mariadb.nrwl.io.

Now we can put a userland in the jail.

# Jail Userland