```
lrwxrwxrwx 1 root root 17 13:11 S10network -> ../init.d/network
lrwxrwxrwx 1 root root 16 13:11 S30syslog -> ../init.d/syslog
lrwxrwxrwx 1 root root 14 13:32 S40con -> ../init.d/con
lrwxrwxrwx 1 root root 14 13:11 S50net -> ../init.d/net
lrwxrwxrwx 1 root root 13 13:11 S60dfs -> ../init.d/nfs
lrwxrwxrwx 1 root root 15 13:11 S70nfs -> ../init.d/lpd.init
lrwxrwxrwx 1 root root 11 13:11 S91local -> ../rc.local
```

What you’ll notice is that there are no real “files” in the directory. Everything there is a link to one of the scripts in the init.d directory. The links also have an “S” and a number at the beginning. The “S” means to start this particular script and a “K” would mean to stop it. The number is there just for ordering purposes. Init will start all the services based on the order they appear. You can duplicate numbers, but it will only confuse you somewhat. You just need to use a two digit number only, along with an upper case “S” or “K” to start or stop the services you need to.

How does init start and stop services? Simple. Each of the scripts is written to accept an argument which can be “start” and “stop”. You can execute those scripts by hand in fact with a command like:

```
/etc/rc.d/init.d/httpd.init stop
```

to stop the httpd server. Init just reads the name and if it has a “K”, it calls the script with the “stop” argument. If it has an “S” it calls the script with a “start” argument. Why all these runlevels? Some people want an easy way to set up machines to be multi-purpose. I could have a “server” runlevel that just runs httpd, sendmail, networking, etc. Then I could have a “user” runlevel that runs xdm, networking, etc.

# 10.5.2 Init Runlevels

Generally, Red Hat Linux runs in run level 3—full multiuser mode. The following runlevels are used in Red Hat Linux:

+   0 Halt.
+   1 Single user mode.
+   2 Multiuser mode, without NFS.