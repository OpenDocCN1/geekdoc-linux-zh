![](bbox=[0.12, 0.07, 0.54, 0.28])

**Figure 9.8** SOCKS connection with the SOCKSrv utility.

# # Dynamic Port Forwarding and SOCKS

Dynamic port forwarding is another powerful feature of SSH in the port-forwarding architecture. Dynamic port forwarding offers the benefit of SOCKS proxy servers, described in the previous section, on a local port on an SSH client machine. Dynamic port forwarding uses a local port on the loopback address (127.0.0.1) that mimics a SOCKS server while performing the functions of a regular SOCKS service. For example, if an SSH connection has been established between an SSH client and an SSH server, instead of using the traditional local port-forwarding options, where each specific local port is matched to a specific port on the remote server, dynamic port forwarding can specify a local port to act like a SOCKS server that can be used by local applications, including mail, FTP, and Web clients. Many applications support the use of a SOCKS server; however, instead of specifying a real SOCKS server on a remote machine, you can specify the local machine (127.0.0.1) with the dynamic port-forwarding SOCKS server port, 1080 by default.

To set up dynamic port forwarding with SOCKS on an SSH client machine, complete the following steps:

+   1. From the SSH client, connect to the SSH server using the appropriate command-line client:
+      ```
+      OpenSSH    ssh <sshserver> -p <port> -l <username> -D 1080
+      SSH        ssh2 <sshserver> -p <port> -l <username> -L socks/1080
+      ```

+   2. On the SSH client; configure any relevant applications to use a SOCKS server for outbound connections. Enter the loopback address (127.0.0.1) for the IP address and port number 1080. Figure 9.9 and Figure 9.10 show example configurations of Internet Explorer and Netscape Messenger, respectively.