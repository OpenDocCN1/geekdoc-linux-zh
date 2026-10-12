historical and can be removed, e.g. the UDP entries for HTTP and POP3. And, except on test systems you could remove **echo**, **discard**, **systat**, **daytime**, and **chargen** on UDP and TCP. (Leaving unnecessary entries in the file uses no resources, so most people don't bother editing the file but it is good security practice to disable or remove anything you don't need.)

# ## 3. The inetd "super-server" and the /etc/inetd.conf file

A server machine can be providing many different services simultaneously, e.g. one of our internal machines provides more than 30. Running 30 large processes even when there's no network activity is a waste of CPU, memory, and processes, so instead of running a separate server for each service, Linux runs a single "super-server" that listens on all the necessary ports simultaneously. This server is called **inetd** ("Internet daemon") and the file **/etc/inetd.conf** controls which ports it listens on. Below is a line from our **inetd.conf** with the important fields annotated. (See the **inetd.conf(5)** manpage for details of other fields.)

```
service name                  transport           run server as     name of server
(from/etc/services)                              this user            program

pop-3               stream    tcp       nowait    root    /usr/sbin/ipop3d
```

The service name is exactly as entered in **/etc/services**, and **inetd** looks up the name in that file to find out which port to listen on, and whether it's a UDP or TCP port. (If you spell the service name incorrectly, your server won't be run.) When **inetd** starts up, it listens on all the specified ports, waiting for connections, as shown below: the **netstat -n -p -a -t** command shows which programs are listening on which ports. (-t: TCP; -a: all, including listening ports; -n: print ports as numbers rather than names; -p: show name of program using this port.)

```
tcp   0  0 0.0.0.0:113     0.0.0.0:*    LISTEN  215/inetd
tcp   0  0 0.0.0.0:79      0.0.0.0:*    LISTEN  215/inetd
tcp   0  0 0.0.0.0:110     0.0.0.0:*    LISTEN  215/inetd
tcp   0  0 0.0.0.0:109     0.0.0.0:*    LISTEN  215/inetd
tcp   0  0 0.0.0.0:119     0.0.0.0:*    LISTEN  215/inetd
tcp   0  0 0.0.0.0:143     0.0.0.0:*    LISTEN  215/inetd
tcp   0  0 0.0.0.0:25      0.0.0.0:*    LISTEN  215/inetd
tcp   0  0 0.0.0.0:512     0.0.0.0:*    LISTEN  215/inetd
tcp   0  0 0.0.0.0:513     0.0.0.0:*    LISTEN  215/inetd
tcp   0  0 0.0.0.0:514     0.0.0.0:*    LISTEN  215/inetd
tcp   0  0 0.0.0.0:43      0.0.0.0:*    LISTEN  215/inetd
tcp   0  0 0.0.0.0:23      0.0.0.0:*    LISTEN  215/inetd
tcp   0  0 0.0.0.0:37      0.0.0.0:*    LISTEN  215/inetd
tcp   0  0 0.0.0.0:13      0.0.0.0:*    LISTEN  215/inetd
tcp   0  0 0.0.0.0:9       0.0.0.0:*    LISTEN  215/inetd
tcp   0  0 0.0.0.0:7       0.0.0.0:*    LISTEN  215/inetd
```

When **inetd** receives an incoming connection request, **inetd** uses the port number it came in on to decide which server program to run to service the connection. **inetd** accepts the connection call and forks as already described; the child process then executes the respective server program to service the client connection.