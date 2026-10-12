# TABLE 20.11  continued

| Option | Meaning |
|---|---|
| -L port:host:hostport | Forward TCP port *port* to *hostport* on remote host *host*. What this does is open a local server socket on *port* and a socket on the remote host that connects to port *hostport* on *host*. All connections to *port* on the localhost will be forwarded to port *hostport* on *host*. |
| -R port:host:hostport | The reverse of -L. Forward TCP port *port* on the remote host to port *hostport* on *host*. |

# Port Forwarding

The -R and -L options deserve special mention. They are useful especially in cases where you need to make a secure “tunnel” through an insecure network (such as the Internet). Consider a case where you have a Web server in California and a database server in Florida. You want the Web server to access the database, but for security purposes you want the communication to be encrypted. Suppose the database listens by default to port 3306. You might run the following shell script on the Web server:

```
#!/bin/sh
while /bin/true
do
    ssh dbserver -L 3306:localhost:3306 sleep 87600
done
```

The while loop is needed because the ssh command (and thus the port forwarding) will run only as long as the command given on the ssh command line specifies. In this case, the sleep 87600 command simply waits for 87,600 seconds (24 hours) before exiting. This command forwards port 3306 of the Web server (where you’re running the command) to port 3306 on the localhost of the database server.

If you want to run this script on the database server, you would use the -R option and invert the two port numbers. Since they are the same, the command would be identical except for the option name.

# Authentication

This scheme poses a problem, though. The ssh command will ask for the password of the remote user. There are only two ways to automate the password login process:

+   - Using .rhosts authentication
+   - Using private/public key authentication