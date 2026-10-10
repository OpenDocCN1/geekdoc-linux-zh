contains a sentence or two describing most packages, making it easier to evaluate whether a program is worth keeping installed.

One of the greatest security risks involves servers you don’t know are running. The preceding approaches may locate such software, but they won’t tell you if a server is actually accessible. One method of locating such servers is to use the `netstat` command, described in Chapter 16. Specifically, the following command creates a list of all the processes that are listening for connections—that is, those that are servers:

```
$ netstat -a | grep -E "Proto\d|LISTEN" 
  Socket Proto Recv-Q Send-Q Local Address     Foreign Address (state)
  c7bc3700 tcp4    0     0    .x11            *.*    LISTEN
  c7bc3b40 tcp4    0     0    .submission    *.*    LISTEN
  c7bc3680 tcp4    0     0    .smtp          *.*    LISTEN
  c7bc21c0 tcp4    0     0    .ssh          *.*    LISTEN
  c7bc2e80 tcp4    0     0    .telnet       *.*    LISTEN
  c7bc1d80 tcp4    0     0    .ftp          *.*    LISTEN
```

This example shows six server ports in use—x11, submission, smtp, ssh, telnet, and ftp, according to the names listed under the Local Address column. These names appear in the `/etc/services` file, and if a server uses a port that’s not listed in that file, the port number appears rather than the name. If you’re a nurse, you’re a server should be running on a particular port, you should investigate it further. You can do so by using the `fstat` command, which returns information on open files and sockets. Use `grep` to filter this command’s output so that it shows information on only the socket identified in `netstat`’s `Socket` column. For instance, to investigate the submission server from the preceding example, you might type the following command:

```
$ fstat | grep -E "CMD|c7bc3b40" 
  USER    CMD PID FD MOUNT INUM MODE SIZE DV R/W
  root    sendmail 194 5* internet stream tcp c7bc3b40
```

The important information in this output comes in the first three columns, which list the user, the command, and the process ID (PID) of the program connected to this port. In this case, sendmail uses this port, in addition to port 25 (smtp). But, there’s nothing fishy about this example—assuming you intended the computer to be running all of these servers. If you believe the computer isn’t running a Telnet server, for instance, you should investigate its configuration, as described in Chapter 21.

> Note The submission port isn’t used much in 2002, but it may be used in the future. The idea is to provide separate ports for e-mail clients than for SMTP servers in order to better control how clients and other servers use a mail-server system. Thus, you might want to close off the submission port to outsiders using a firewall, but enable local users to access it.