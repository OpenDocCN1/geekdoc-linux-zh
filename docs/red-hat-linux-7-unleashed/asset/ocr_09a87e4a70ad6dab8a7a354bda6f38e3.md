# **Caution**

If alterations are made to the `/etc/named.conf` file, the named daemon must be stopped and restarted before you can see the changes.

In any situation, if you want to make sure that all files are read and loaded, use this command:

```
```bash
# /etc/rc.d/init.d/named restart
```
```

Another great debugging technique, especially after you’ve restarted named, is to look at the system log. You can find what file contains the appropriate log by looking in `/etc/syslog.conf`. Default for Red Hat 7 is `/var/log/messages`. Because you’re interested only in recent messages, grab the tail end of the file with this command:

```
```bash
# tail -n 400 /var/log/messages | less -N
```
```

All log entries have date and time, so if need be you can read back more than 400 lines. Look especially for error, not found, no such, fail, and so on. Carefully evaluate any error messages and try to figure out what they mean and what caused them.

# # Checking Your DNS Configuration with dnsvalk

I find dnsvalk an indispensable tool. It checks your DNS configuration very thoroughly. It’s the DNS equivalent of C’s `lint` utility or Samba’s `testparm` utility. Using dnsvalk first can easily save hours of troubleshooting, so it’s worth the few minutes it takes to install and use it.

The dnsvalk utility depends on the perl-Net-DNS tool, so the latter must be installed first. When using the Red Hat distribution, the easiest installation is via rpm. First, obtain these two files from the net:

+   - `ftp://rufus.w3.org/linux/contrib/libc5/1386/perl-Net-DNS-0.12-1.1386.rpm`
+   - `ftp://rufus.w3.org/linux/contrib/noarch/noarch/dnsvalk-2.0.2-1.noarch.rpm`

Now install them with the following two commands:

```
```bash
# rpm -ivh perl-Net-DNS-0.12-1.1386.rpm
# rpm -ivh dnsvalk-2.0.2-1.noarch.rpm
```
```

# **Note**

If you prefer to compile, build, and install from source code, you can get the source at http://www.visi.com/~barr/dnsvalk/.