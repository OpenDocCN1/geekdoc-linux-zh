The port on the remote server that will be used for the server end of the tunnel (in this case, 110)

You don’t have to use port 2345. You can use the same port on both ends if desired. However, be aware that you will need to switch to the root user if you want to use a port number less than 1024 on the client side of the tunnel. These are called *privileged* ports.

+   10. With the tunnel established, configure the local e-mail client program to retrieve mail from the local system on the port you configured for the client end of the SSH tunnel. In this example, you would configure it to get mail from the local system’s IP address on port 2345. An example of how to do this with the Evolution e-mail client is shown in Figure 18-6. Note that I used the host name of the local host, not the POP3 server, in the Server field. I also added the port number of the workstation end of the tunnel to the end of the host name.

At this point, when the client uses the POP3 protocol to download new messages, the SSH client on the local system will encrypt the request and forward it to the SSH server through the SSH tunnel you established. The SSH server will receive the request, decrypt it, and then pass the data on to the local port 110, where the POP3 daemon is listening. The cool thing about this process is that it is completely transparent to the e-mail client software. As far as it’s concerned, it’s retrieving e-mail from a local POP3 server.

You can test the tunnel you created using the telnet command from the client end of the tunnel. The syntax is **telnet localhost client_tunnel_port**. For example,

```
telnet localhost 2345
```

When you do, you should see a connection established with the remote system where the POP3 daemon is running. An example is shown in Figure 18-7.

You can also tunnel your X server traffic to remote X clients using an SSH connection. This is important because unencrypted X traffic provides an attacker with a gold mine of information that he or she can use to compromise your systems.

![](bbox=[0.05, 0.69, 0.85, 0.95])

![](bbox=[0.05, 0.7, 0.22, 0.79])