Connection closed by foreign host.
$ 
Make sure you specify the protocol number 13 after the IP number 127.0.0.1 (you can use a remote IP number, but for this testing procedure stick to 127.0.0.1). If your daytime service is running, you should get a date and time string displayed, which is followed by the message “Connection closed by foreign host.” 
If the service is not available, you will see output similar to this: 

![](bbox=[0.06, 0.24, 0.15, 0.33])

```
$ telnet 127.0.0.1 13
Trying 127.0.0.1...
telnet: Unable to connect to remote host: Connection refused
$ 
```

If you do, then this indicates that your daytime service is not running. To troubleshoot this problem, examine your /etc/inetd.conf file: 

![](bbox=[0.06, 0.39, 0.15, 0.48])

```
$ grep daytime /etc/inetd.conf
# Echo, discard, daytime, and chargen are used
#daytime stream tcp nowait root internal
#daytime dgram udp wait root internal
$ 
```

As shown in this case, the daytime service entry in the file has a # character in the first column. This effectively “comments out” the service, which makes it unavailable. This may have been done as a precaution against attacks from the Internet or other hostile users in your network (it's a general principle to disable any Internet service that you do not deem as necessary). To try out the client example program, you will need to enable the tcp daytime service entry (the udp service entry can be left commented out if it is already). 
To fix the service, edit the file /etc/inetd.conf by removing the leading # character for the daytime entry that includes the protocol tcp in it. Check it with grep again, and you should see something like the following: 

![](bbox=[0.06, 0.74, 0.15, 0.83])

```
$ grep daytime /etc/inetd.conf
# Echo, discard, daytime, and chargen are used
daytime stream tcp nowait root internal
daytime dgram udp wait root internal
$ 
```

After making changes to the /etc/inetd.conf file, you must tell the inetd daemon to re-read and reprocess the changed file. This is done as follows: 

![](bbox=[0.06, 0.89, 0.15, 0.98])

```
$ su -
Password:
# ps ax | grep inetd
313 ? S 0:00 inetd
828 pts/1 S 0:00 grep inetd
# kill -1 313
# 
```