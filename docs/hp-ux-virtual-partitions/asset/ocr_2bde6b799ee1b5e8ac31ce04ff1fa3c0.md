# # Host Name Mapping

The most important decision related to networking is how host name mapping is implemented on your system in ARPA. Three techniques are available for host name mapping:

+   * Berkeley Internet Named Domain (BIND)
+   * Network Information Service (NIS)
+   * UNIX file /etc/hosts

The most common and simplest way to implement host name mapping is with /etc/hosts, so I cover this technique in the next section. Keep in mind that there are probably networking manuals for your UNIX variant devoted to many networking topics including NFS, ARPA, and others. These manuals serve as good reference material if you need to know more about networking than is covered here.

Using the /etc/hosts file, as you are about to see, becomes very difficult for environments where there are many systems deployed. With this solution there is one /etc/hosts file that must be kept up-to-date and propagated to all other systems.

The Domain Name System (DNS) is widely used in large environments. DNS uses Berkeley Internet Name Domain Service (BIND) to resolve names to addresses. There are name servers that fill a request for name data. This is the server side to BIND. There is a client side to BIND, called the resolver, that accesses the name server(s) to resolve names. Using this client/server model, it is much easier to maintain naming information, because it only needs to be kept in a few places as opposed to on each system.

Clients use a file called /etc/resolv.conf to configure the resolver. The name server and its corresponding address are the keys to resolving information.

This solution makes it much easier to maintain system names and addresses in large environments. DNS and BIND are primarily a system administration exercise to setup. From a user standpoint, you don't need to know much about them. What I will instead focus on in the upcoming sections are some of the programs in which users are more interested. I will supply some background so that the way in which the programs are used has more meaning. In general, though, I'll concentrate on the user aspect of