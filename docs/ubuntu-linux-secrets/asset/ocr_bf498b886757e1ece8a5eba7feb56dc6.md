What’s in a name? Plenty, if you’re a Montague or are using the Internet. How would you react if your favorite product was advertised on television stating, “Just visit our web site at 198.182.196.56 for more information”? Unfortunately, humans do not process numbers as well as computers do. To compensate for that, systems administrators use names to identify their computer systems. The domain name system (DNS) was developed to help humans easily locate computer names on the Internet. If you choose to let your ISP handle your domain name and email, you may not need to know the details about DNS configurations, but it might not be a bad idea to know how DNS works in general (just in case of any problems). This chapter discusses where DNS came from, why it is so vital to email and web operations, and how you can configure your Ubuntu server to utilize it either as a client or as a DNS server.

# History of Computer Names

Back in the old days when the Internet was small (just a few hundred computers) it was not too complicated to locate another computer. Each Internet computer had a database of hostnames and IP addresses. Internet hostnames could be anything the administrator desired—Fred, Barney, Acct1, anything. There was a central clearinghouse for keeping track of new computer names and addresses. Once a week or so, a systems administrator would download a new copy of the current database from the clearinghouse.

Of course, this system did have its drawbacks. When someone brought a new computer online they needed to search the database to make sure nobody had already used the clever new hostname they wanted to use. It didn’t take systems administrators long to figure out that this method was on a collision course with progress.

As the Internet grew, so did the database. As the database grew, so did the time it took to download and search it. It was also starting to get difficult coming up with a unique hostname for new systems. Something had to change, and it did.

# Domain Names

The method agreed on was the domain name system (DNS). DNS uses a hierarchical, distributed database to break up the hostnames database. That’s a catchy way of saying that no single computer has to maintain the entire database of Internet devices. The database is distributed among multiple computers, called DNS servers, on the Internet. For client computers to locate another computer on the Internet, they need only find the nearest DNS server and query for the IP address of a hostname.

To implement this system, developers invented a new protocol to pass the DNS information from the DNS server to the client, as well as develop software for DNS servers to implement the new database system.

This section describes in detail the DNS server that Ubuntu uses.

# DNS Structure

The structure of a hierarchical database is similar to an organization chart, with nodes connected in a tree-like manner (the hierarchical part). The top node is called the root. The root node does not explicitly show up in addresses, so it’s called the nameless node. Multiple categories were created under the root level to divide the database into pieces called domains.