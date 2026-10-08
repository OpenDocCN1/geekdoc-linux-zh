# PRIMARY NAME SERVERS 483

+   - You want to set up new name server for an organizational zone inside an already existing domain. You must discuss this with your network administrator, otherwise your new server will not be recognized as authorized.

Your own name server, however, also has its advantages, no matter whether you are connected to the Internet or not:

+   - In a local network, all computer names are always known on all other computers.

+   - The database is always up to date and consistent on all computers. The hosts files otherwise needed on the different computers tend to become obsolete and possibly contradictory fairly quickly.

+   - Assignment of name and IP addresses is consistent.

+   - If you operate the name server yourself, you can change data without having to bring in your provider.

Listing 20.4 shows an example of the file /etc/named.conf on a primary name server. directory specifies the directory in the files of this name server are stored. A computer can be the primary and/or secondary server for several zones. The only requirements are that the primary lines are entered in the file /etc/named.conf and the corresponding data is available.

Each name server should create cache of requests and answers. This can be done by means of the keyword cache. At the start of the name server, all data from named.root that is still correct is reloaded into the cache. A name server becomes a cache-only server if no zone of the type master or slave is contained in the file named.boot.

The name server must know where to find the authoritative name server for the root domain of the network. This information is stored in the file named.root. In many documents, this file is also called root.cache, although this does not describe its purpose. The name of the file is specified in the zone type hint.