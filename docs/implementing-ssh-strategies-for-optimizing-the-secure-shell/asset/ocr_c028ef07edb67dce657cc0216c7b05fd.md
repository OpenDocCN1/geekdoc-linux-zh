# # SSH Communications

SSH Communications’ SSH client is the first I will discuss. Open the SSH client and initiate a simple SSH connection by executing the following steps:

+   1. Start Program SSH Secure Shell Secure Shell Client
+   2. File Open Quick Connect

As shown in Figure 3.1, the Host Name field is either the fully qualified DSN name for the SSH server, such as sshserver.aum.com, or the dot notation of the IP address of the SSH server, such as 172.16.11.17. The User Name field is the username on the remote SSH server. The username can either be the local account on a Windows machine or a domain account on a Windows domain, depending on how the SSH server is implemented. In Unix environments, the username is the same in the /etc/passwd file. The Port Number field is used to specify the port number. If the SSH server is listening on a nonstandard port (a port other than port 22), the appropriate port number should be placed in the port box, such as 202. Lastly, the Authentication Method specifies the type of authentication that should be used when attempting to connect to the remote SSH server. The possible values and their descriptions are in Table 3.10.

![](bbox=[0.18, 0.5, 0.75, 0.85])

**Figure 3.1** “Quick Connect” menu.