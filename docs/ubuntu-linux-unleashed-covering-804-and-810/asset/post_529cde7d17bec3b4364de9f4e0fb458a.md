
```sh
# sysctl -A
net.ipv4.tcp_max_syn_backlog = 1024
net.ipv4.tcp_rfc1337 = 0
net.ipv4.tcp_stdurg = 0
net.ipv4.tcp_abort_on_overflow = 0
net.ipv4.tcp_tw_recycle = 0
net.ipv4.tcp_syncookies = 0
net.ipv4.tcp_fin_timeout = 60
net.ipv4.tcp_retries2 = 15
net.ipv4.tcp_retries1 = 3
net.ipv4.tcp_keepalive_intvl = 75
net.ipv4.tcp_keepalive_probes = 9
net.ipv4.tcp_keepalive_time = 7200
net.ipv4.ipfrag_time = 30
```

The items shown are networking parameters, and actually tweaking these values is beyond the scope of this book. If we wanted to change a value, however, the -w parameter is used:

```sh
# sysctl -w net.ipv4.tcp_retries2=20
```

This increases the value of that particular kernel parameter.

If you find that a particular setting is useful, you can enter it into the /etc/sysctl.conf file. The format is as follows, using the earlier example:

```sh
net.ipv4.tcp_retries2=20
```

Of more interest to kernel hackers than regular users, sysctl is a potentially powerful tool that continues to be developed and documented.

## TIP

The kernel does a good job of balancing performance for graphical systems, so there's really not a great deal you can do to tweak your desktop to run faster.

Both GNOME and KDE are “heavyweight” desktop systems: They are all-inclusive, all-singing, and all-dancing environments that do far more than browse your file system. The drawback to this is that their size makes them run slow on older systems. On the flip side, Ubuntu also comes with the Xfce desktop, which is a great deal slimmer and faster than the other two. If you find GNOME and KDE are struggling just to open a file browser, Xfce is for you.

## Apache

Despite being the most popular web server on the Internet, Apache is by no means the fastest. Part of the “problem” is that Apache has been written to follow every applicable standard to the letter, so much of its development work has been geared toward standards-compliancy rather than just serving web pages quickly. That said, with a little tweaking we can convert a $1,000 Dell server into something capable of surviving the Slashdot Effect.

## NOTE

Slashdot.org is a popular geek news website that spawned the Slashdot Effect—the result of thousands of geeks descending on an unsuspecting website simultaneously. Our $1,000 Dell server had dual 2.8GHz Xeons with 1GB of RAM and SCSI hard disks—if you have more RAM, faster chips, and a high-end network card you can kick sand in Slashdot's face.

The first target for your tuning should be the apache2.conf file in /etc/apache2, as well as the other files in /etc/apache2. The more modules you have loaded, the more load Apache is placing on your server—take a look through the LoadModule list and comment out (start the line with a #) the ones you do not want. Some of these modules can be uninstalled entirely through the Add or Remove Packages dialog.

As a rough guide, you will almost certainly need mod_mime and mod_dir, and probably also mod_log_config. The default Apache configuration in Ubuntu is quite generic, so unless you are willing to sacrifice some functionality you may also need mod_negotiation (a speed killer if there ever was one), and mod_access (a notorious problem). Both of those last two modules can and should work with little or no performance decrease, but all too often they get abused and just slow things down.

Whatever you do, when you are disabling modules you should ensure you leave either mod_deflate or mod_gzip enabled, depending on your Apache version. Your bottleneck is almost certainly going to be your bandwidth rather than your processing power, and having one of these two compressing your content will usually turn 10Kb of HTML into 3Kb for supported browsers (most of them).

Next, ensure keepalives are turned off. Yes, you read that right: turn keepalives off. This adds some latency to people viewing your site, because they cannot download multiple files through the same connection. However, in turn it reduces the number of simultaneous open connections and so allows more people to connect.

If you are serving content that does not change, you can take the extreme step of enabling MMAP support. This allows Apache to serve pages directly from RAM without bothering to check whether they have changed, which works wonders for your performance. However, the downside is that when you do change your pages you need to restart Apache. Look for the EnableMMAP directive—it is probably commented out and set to off, so you will need to remove the comment and set it on.

Finally, you should do all you can to ensure that your content is static avoid PHP if you can, avoid databases if you can, and so on. If you know you are going to get hit by a rush
