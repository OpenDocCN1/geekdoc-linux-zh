# 18.3 Windows Networking implementation

In the following chapters we’re going to cover three big areas of Windows Networking:

# 1. Machine and resource names

Windows Networking uses names, not IP numbers, as its primary reference for machines and other resources. This is the complete opposite of TCP/IP, where a machine’s IP number is the important thing and hostnames are almost an afterthought. Whereas an IP network can work perfectly well (if less conveniently for human users) without names, Windows Networking depends entirely on names for its basic operation:

+   - it uses unique names for PCs and for users, e.g. my PC’s name is **pc29** and I am logged on to it with username **administrator**
+   - it uses “group names” for certain network services or resources. A group name is shared by all machines that offer that service or resource.

Because names are fundamental to the operation of the system, how they are resolved is crucial. There are two main ways that names are resolved to machine addresses (to IP numbers in our case):

+   a. using broadcast packets. Let’s say our PC is booting, and it’s been configured with the name **alice**. It broadcasts asking if there’s a machine **alice** already on the network. If there’s no reply, it assumes the name is OK and the PC then operates as **alice**. (If some other machine says it is using the name, we’ll have to reconfigure and reboot our PC.)  
+   If **Alice** then wants to contact another Windows machine, Bob, she broadcasts a query for the name **bob**. If there is a **bob** on the network, he replies, giving his IP address
+   b. using WINS (Windows Internet Name Service). Each machine as it boots registers its name and IP number with the WINS server, and any time it wants to get the address of another machine it queries the WINS server.

We cover name resolution in detail in Chapter 19.

# 2. Authentication and security

Authentication and security are an important part of Windows Networking that was enhanced a lot in Windows-NT. NT introduced the concept of a security “domain” – a set of machines sharing a single database of usernames, passwords, and authorization information that controls who may use what and how.

Domain-based security provides ‘single sign-on:’ you log on to the network once, and that login is used to control all your accesses to resources – on this machine and elsewhere on the network. All authorization checks are performed transparently: even if this machine has to log you on to another one, it does so automatically by itself, without prompting for your username and password again.

Chapter 20 covers NT domains, authentication, and security.