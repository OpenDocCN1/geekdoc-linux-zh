
# Networking and Internet Services
PART II

to get the subject and other header information of article numbers given as parameters.
Finally, Arts is the timeout for the NNTP command, Arts. For full details on any of these NNTP commands or NNTP files, refer to the NNTP RFC, which is included as part of the NNTPCache distribution. It should have been installed into the /usr/doc/nntpcache-1.0.7.1-1 directory and de-called rfc977.txt.

After the %BeginGroups line is where you NNTPCache retrieve articles for each set of newsgroups. NNTPCache tries to match the requested newsgroup with all entries listed, and the last match is the one that is used. With the file configurations set here, Microsoft newsgroups are to use the mnews.microsoft.com news server. For other groups, NNTPCache goes to news.mysisp.net. Again, replace that specification with your.

Now NNTPCache is configured, you have to start it. First, we have to fix some configuration problems with the nntpcache startup script. Using the editor of your choice, replace /sbin/init.d/nntpcached with the following contents:

```bash
#! /bin/sh
#
# nntpcache - NNTPcache server
# 20.01.98 ML
# modified 1999.10.22 Deirdre Saoirse <deirdre@deirdre.net>

  /etc/rc.config

# note: took out networking check

[ -d /etc/nntpcache ] || exit 0
[ -d /var/spool/nntpcache ] || exit 0

# See how we were called.
return=$rc_done
case "$1" in
start)
  echo -n "Starting NNTPCache server: "
  touch /var/lock/subsystems/nntpcached
  startproc /usr/sbin/nntpcached || return=$rc_failed
  echo -e "$rc"

  ;
stop)
  echo -n "Stopping NNTPCache server: "
  killproc -TERM /usr/sbin/nntpcached || return=$rc_failed
  echo -e "$rc"


reload);

```
$0 stop && $0 start || return=$rc_failed
;;
restart);
$0 stop && $0 start || return=$rc_failed
;;
status);
echo -n 'Checking for service nntpcache daemon: " 
checkproc /usr/sbin/nntpcached && echo OK !! echo No process
;;
check);
echo -n 'Cheaking active, active.times & newsgroups: " 
killproc -USR1 /usr/sbin/nntpcached
echo 'done'
;;
expire);
echo -n 'Performing an expire: " 
killproc -USR2 /usr/sbin/nntpcached
echo 'done'
;;
*)
echo "Usage: $0 {start|reload|restart|status|check|expire}"
esac
```

exit 0
You can now start nntpcache with the following command:

```bash
[root]@company /etc/nntpcache]# /sbin/init.d/nntpcache start
```
Also, whenever you restart your SuSE Linux server, it should automatically start on boot.
Now you have NNTPCache caching running; you can start your favorite newsreaders. If you are using a text-based newsreader such as tin or trn, set your NNTPSERVER environment variable to point to your NNTPCache machine:

```bash
$ export NNTPSERVER=nntpcache.mycompany.com
```
If you need more information on NNTPCache, read the documents in the /usr/doc/nntpcache-1.0.7.1-1/ directory, or visit the NNTPCache home page on the Internet.

![](img/cbac72550c7126a22162e94d91a0c360_464_0.png)

# Introduction to trn

There are many readers available for Linux systems, but trn remains the perennial favorite. This is an old package but is simple to use, as well as fast and efficient. You might not need a reader at all if you have Web services on your system. Many Web browsers allow access to newsgroups either in your own directory or through a connection to an ISP's newsfeed.

The primary advantage of trn over the earlier rn (read) news package is that trn lets you follow threads. A thread in a newsgroup is a continuing discussion with one primary subject. Before trn came along, you had to read news consecutively from first to last, trying to assemble several different conversations into logical groups as you went. When trn became available, you could start with one thread, read all the postings about that subject, and then move on to another subject, regardless of the chronological order in which the postings were made.

Threads are usually handled automatically without requiring any special user interaction, although there is work performed behind the scenes on your newsfeed. Some newsgroups do not support threading, but most do. If threads are available, you can follow the thread from start to finish, or jump out and change threads at any time.

# Installing and Configuring trn

The trn newsreader is easy to install as a binary package; an RPM is included with Linux. Type the following to see if trn is already installed on your system:

```bash
rpm q trn
```

If no package by that name is found, you can install the trn package from the directory RPM files by issuing the following command:

```bash
rpm i trn-3.6-70.i386.rpm
```

You can also install packages using YaST. First, select Adjustments of Installation from YaST's main menu. Choose Select Installation Medium and then select the correct place to find the package. Select Choose/Install Packages and install the package. This method has the advantage that there is no syntax to the RPM command to remember.

There is really no special configuration required for trn to run. When the binary is available on your system, it will check for the newsgroup information in /usr/lib/news and present it to you. In the past, trn wasn't capable of forming threads on its own. Because of this, external threading utilities such as nthreads or overview were once popular. As of version 3.0, however, trn supports direct threading without the need for external thread utilities. Most users now use trn as a standalone program.

There are many other excellent newsreaders available; search http://www.freshnews.org

# Summary

In this chapter, you learned how to install and configure Internet News, and how to set up NNTPCache. The steps involved might seem a little overwhelming, but if you take them carefully, you'll be surprised how little time it takes.

![](img/cbac72550c7126a22162e94d91a0c360_466_0.png)
