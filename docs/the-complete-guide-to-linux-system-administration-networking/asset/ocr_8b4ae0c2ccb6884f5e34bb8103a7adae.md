+   - **mailq**: Displays a list of messages waiting to be sent out. Messages wait in the queue while you are not connected to the Internet, while sendmail waits for a domain name to be resolved, or a message has not been accepted by a remote mail server (by default, sendmail will try again later).
+   - **mailstats**: Displays a summary of the amount of e-mail traffic that sendmail has handled. Fields in the output of *mailstats* include messages received, bytes received, messages sent, bytes sent, messages rejected, and messages discarded.

# Using Superservers for Network Services

On a Linux system providing many network services, it can be wasteful to have 30 or more different services running at the same time. Many services are only needed occasionally. Yet you still want client requests for each service to be handled without you intervening to start the needed service. The solution is the **superserver** (also called a **metaserver**), which listens on multiple network ports and starts the appropriate service when a client connection arrives for that port. The most widely used superserver program is called **inetd**, for Internet daemon. Another superserver that is gaining in popularity is **xinetd**, for extended Internet daemon. *xinetd* is used by default on Red Hat Linux and Fedora.

![](bbox=[0.08, 0.51, 0.18, 0.62])

> Some network services do not rely on the superserver mechanism; they are designed to run in **standalone mode**, without being started by *inetd* or *xinetd* as new client requests arrive.

Examples of network services that often rely on a superserver are FTP, Telnet, SSH, and standard e-mail servers. The mapping of services to default port numbers is done via the **/etc/services** file.

Many different programs refer to */etc/services* to determine which port to use for a particular network service. The superserver daemons use the port numbers in */etc/services* to determine which ports to watch for client connections. When a client tries to connect to a given port number, the superserver starts the appropriate network service to handle the client's request. After that request has been handled, the network service exits, so its resources are freed for other programs. The only program that has to be running all the time is the superserver itself.

Both *inetd* and *xinetd* are configured using text files within */etc*. The configuration files indicates to which ports the superserver should listen and which program the superserver should start if a client request arrives on one of those ports. *xinetd* has a more complex configuration model and better security, though *inetd* is perfectly adequate when used in conjunction with certain security measures you'll learn about in the next section.

# Using xinetd

The *xinetd* program is a revised version of *inetd* that focuses on creating a more secure environment, and happens to be more sound in its configuration architecture as well. *xinetd*