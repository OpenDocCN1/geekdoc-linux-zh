# Q It takes my system two or three minutes to boot. It seems to get stuck on sendmail or httpd. What's going on?

A Both Sendmail and Apache (httpd) have to figure out your machine's hostname; to do this, they need to do a reverse lookup against the DNS (domain name server) configured in /etc/resolv.conf (which is written out by sysinstall). This lookup will have to timeout for every configured name server before it fails and allows the startup process to proceed. Network timeouts are often fairly long, which is why networking is the most common cause of boot hangs up. One solution to this problem is to make sure that the name server listed first in /etc/resolv.conf is reachable from your FreeBSD machine; this ensures that Sendmail and Apache will be able to determine the machine's hostname and start up without delay. If this is not possible, list 127.0.0.1 (localhost) as the first name server and comment out the rest.

# Q My FreeBSD system doesn't have an /etc/rc.d directory; instead, it has a bunch of files in /etc itself with names beginning with rc... What gives?

A Your system is probably a version of FreeBSD prior to 5.0. In FreeBSD 5.0, the "next generation" resource configuration format was adopted, which is what uses the /etc/rc.d directory. Don't worry—the operation of the resource configuration scripts is almost exactly the same; it's mostly just an organizational issue.

# Q How do I create a task of my own to execute at boot time?

A You can write a shell script and put it in /usr/local/etc/rc.d; that script will be executed along with all the other scripts in that directory after the /etc/rc.d scripts have been run. For best results, make sure that your script properly handles the start and stop arguments, and also make sure that it's set to executable and has a .sh extension. Alternatively, you can put commands into /etc/rc.local, although that's a deprecated method no longer recommended.

# Q Whenever I log in as root, my terminal session keeps getting interrupted by all these weird status messages that appear on the screen. How do I get them to stop?

A Edit /etc/syslogd.conf and comment out the lines that print to either /dev/console or to root. Then restart syslogd as we discussed in this chapter.