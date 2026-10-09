much documentation exists on how to do so, STARTTLS enhancements are also available for Qmail (page 715) and Postfix (page 715) and other popular MTAs. It is important to recognize that this capability provides encryption between two mail servers but not necessarily between your machine and the mail server. Also, the advantages of using TLS are negated if the email must pass through a relay that does not support TLS.

# # MUAS (MAIL USER AGENTS)

Many popular mail user agents, such as *mutt*, *elm*, Thunderbird, and *emacs*, include the ability to use PGP or GnuPG for encryption. Evolution, the default Ubuntu Linux MUA, has built-in GnuPG support. This approach has become the default way to exchange email securely.

# # NETWORK SECURITY

Network security is a vital component for ensuring the security of a computing site. However, without the right infrastructure, providing network security is difficult, if not impossible. For example, if you run a shared network topology, $^{4}$ such as Ethernet, and have in public locations jacks that allow anyone to plug in to the network at will, how can you prevent someone from plugging in a machine and capturing all the *packets* (page 1164) that traverse the network$^{5}$? You cannot—so you have a potential security hole. Another common security hole relates to the use of `telnet` for login. Because `telnet` sends and receives *clear text*, anyone "listening in" on the line can easily capture usernames and passwords, compromising security.

Do not allow any *unauthenticated* PC (any PC that does not require users to supply a local name and password) on a network. With a Windows 9x PC, any user on the network is effectively working with *root* privileges for the following reasons:

+   * A PC does not recognize the concept of **root** privileges. All users, by default, have access to and can watch the network, capture packets, and send packets.
+   * On UNIX/Linux, only a user working with **root** privileges can put the network interface in promiscuous mode and collect packets. On UNIX and Linux, ports numbered less than 1024$^{6}$ are privileged—that is, normal user protocols cannot bind to these ports. This is an important but regrettable means of security for some protocols, such as NIS, NFS, RSH, and

> 4. Shared network topology: A network in which each packet may be seen by machines other than its destination. "Shared" means that the 100 megabits per second bandwidth is shared by all users.
> 5. Do not make the mistake of assuming that you have security just because you have a switch. Switches are designed to allocate bandwidth, not to guarantee security.
> 6. The term *port* has many meanings; here it is a number assigned to a program. This number links incoming data with a specific service. For example, port 21 is used by FTP traffic, and port 23 is used by TELNET.