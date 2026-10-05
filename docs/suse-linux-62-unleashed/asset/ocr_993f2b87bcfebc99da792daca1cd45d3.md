# Networking and Internet Services
PART II

to get the subject and other header information of article numbers given as parameters.
Finally, Arts is the timeout for the NNTP command, Arts. For full details on any of these NNTP commands or NNTP files, refer to the NNTP RFC, which is included as part of the NNTPCache distribution. It should have been installed into the /usr/doc/nntpcache-1.0.7.1-1 directory and de-called rfc977.txt.

After the %BeginGroups line is where you NNTPCache retrieve articles for each set of newsgroups. NNTPCache tries to match the requested newsgroup with all entries listed, and the last match is the one that is used. With the file configurations set here, Microsoft newsgroups are to use the mnews.microsoft.com news server. For other groups, NNTPCache goes to news.mysisp.net. Again, replace that specification with your.

Now NNTPCache is configured, you have to start it. First, we have to fix some configuration problems with the nntpcache startup script. Using the editor of your choice, replace /sbin/init.d/nntpcached with the following contents:

```
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


esac
```