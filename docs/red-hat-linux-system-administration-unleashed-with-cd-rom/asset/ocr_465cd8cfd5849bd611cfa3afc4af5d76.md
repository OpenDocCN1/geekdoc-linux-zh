# Retrieving the WREQ Code

The code for the WREQ system is available from the Duke University Web server at http://www.math.duke.edu/~yu/wreq. As noted, in order to utilize the reporting features of WREQ, you must also retrieve the GD perl interface module from http://www.genome.wi.mit.edu/ftp/pub/software/WWW/GD.html and install it.

# Installing WREQ

Once you have retrieved the code for WREQ and installed GD.pm, you can begin installation of WREQ. The first step of this installation is to unpack the distribution, which is contained in a file called wreq.tar.gz, and fix the permissions. The following session transcript demonstrates this step.

```
[root@quicksilver /root]# cd /home/httpd/cgi-bin
[root@quicksilver cgi-bin]# tar xvfz /tmp/wreq.tar.gz
wreq/index.html
wreq/req
wreq/req-common
wreq/req-config
wreq/req-convert
wreq/req-create
wreq/req-list
wreq/req-listfaq
wreq/req-login
wreq/req-mail
wreq/req-misc
wreq/req-newreq
wreq/req-null
wreq/req-search
wreq/req-show
wreq/req-showfaq
wreq/req-socket
wreq/req-status
wreq/req-time
wreq/req-tty
wreq/req-update
wreq/wreq
wreq/data/
[root@quicksilver cgi-bin]# chown -R root.root wreq
[root@quicksilver cgi-bin]# cd wreq
[root@quicksilver wreq]# ls
data    req.config  req-listfaq  req-newreq  req-showfaq  req-tty
index.html  req-convert  req-login  req-null  req-socket  req-update
```