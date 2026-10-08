prompt, the command to execute. The following shows an example to remove all core files in /home/marty p at 9:00 P.M.:

```
$ at 9:00PM
at> find /home/marty p -name core exec rm {} \
; 
type ^d (control d)
at>
$
```

After issuing at and the time the "at>" prompt appears for you to issue the command. You then press ^d (control d) at the next prompt to return to your usual shell prompt.

# # Networking

Networking is covered extensively in Chapter 11. This is a topic on which system administrators spend a great deal of time both in setup and maintenance, so much so that there are books devoted to networking topics. Chapter 11 covers networking from a user perspective but has more of a system administration tone to it than the other chapters, because many important networking commands are covered, including ping, route, ifconfig, netstat, and others. Your system administrator has undoubtedly spent a lot of time planning how your systems fit into the network and configuring them to support this plan. You reap the benefits of this work by having the use of remote file systems mounted as if they were local to your system with NFS, by accessing other systems through remote login with rlogin, and many other important network functions. Please see the Networking chapter to view how many important networking commands are used.

![](bbox=[0.88, 0.4, 0.97, 0.49])

![](bbox=[0.88, 0.49, 0.97, 0.57])

![](bbox=[0.88, 0.57, 0.97, 0.66])

![](bbox=[0.88, 0.66, 0.97, 0.75])

# # syslog and Log Files

When your system administrator encounters a problem of some type on your system they immediately start looking through system log files. Log files are produced from a variety of sources, including utili-