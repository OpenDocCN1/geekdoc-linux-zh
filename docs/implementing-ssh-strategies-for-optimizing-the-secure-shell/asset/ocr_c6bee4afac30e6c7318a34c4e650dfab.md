![](bbox=[0.11, 0.06, 0.81, 0.48])

**Figure 8.2** Sniffer capturing an RSH connection.

# ## Compromising a System with Remote Login (Rlogin)

Remote Login (Rlogin) is also a *client/server technology wherein the client, Rlogin, connects to an Rlogin server (Rlogind), usually listening on port 513. Rlogin starts a remote terminal session on a system, usually an operating system or device, running the login server. Login also uses the username and password information from the Unix password file, such as */etc/passwd* or */etc/shadow*. In addition to using the password file, Rlogin uses the *hosts* file, which has a list of IP addresses that are authorized to log in to the server. As with RSH, Rlogin has connections that are in clear-text, which allows a passive attacker to sniff the connection and access the username, password, and IP address in order to make a valid connection. Once an unauthorized user obtains the information, the system is virtually compromised. See Figure 8.3 for a sniffer program that captures the Rlogin connection.