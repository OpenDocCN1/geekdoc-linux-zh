Networking is extremely important for many of today's computer functions. Unfortunately, networking brings risks because networks of any size are likely to host malicious individuals. Such people may attack your computer in many different ways, and if their attacks are successful, they may destroy your data, use your system to attack others, or otherwise cause problems. For this reason, understanding network security is critical to operating a computer on a network. Indeed, Chapter 29 is devoted to this topic. This chapter is dedicated to a particular type of network security tool: the *firewall*. This is a tool that can be used to restrict remote access to one computer or group of computers from another computer or group of computers.

To configure a firewall, you must first understand the nature of the security threat that a firewall is designed to counter. This chapter therefore begins with coverage of this topic. It moves on to a description of the types of firewalls that exist, and an overview of the FreeBSD tools that implement these firewall types. Finally, this chapter concludes with information on how to create a particular type of firewall (known as a *packet-filter firewall*) in FreeBSD. Such a firewall can protect a single computer or (when implemented on a router) an entire network.

# ## Understanding the Threat

At its core, a firewall is a network access control tool: it's designed to block access based on computer names, IP addresses, or other criteria. The premise upon which firewalls are built is that some individuals have ill intentions and may try to abuse the servers that run on your computers. Whenever possible, therefore, you should limit access to your servers. It's also true that individuals on a computer or network you administer may try to launch attacks against others. Firewalls are therefore often configured to block such attacks. Even if no individual who uses a computer you control is a “bad apple,” it's possible that a virus or worm could take over one of your computers, leading to such attacks originating from your network.

> Caution
> 
> *Firewalls most frequently block access between networks, but security within a network can be important, as well. Proper configuration of local servers can help reduce the risk of entirely local attacks, as can use of local network security tools such as Kerberos (http://web.mit.edu/kerberos/www).*

# ## Outsiders Trying to Get In

When the words “network security” come up, most people tend to think of malicious outsiders attempting to gain access to a network's internal computers. There are a huge number of examples of this sort of abuse, but some common examples include the following:

+   - **Break-ins of login servers** Login servers (described in Chapter 21) enable users to run programs from a remote site. Crackers sometimes abuse such servers to cause problems for you or others.