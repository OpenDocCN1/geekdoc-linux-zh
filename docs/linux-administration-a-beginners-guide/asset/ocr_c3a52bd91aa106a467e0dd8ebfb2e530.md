The Network Information Service (NIS) makes possible the sharing of critical files across the local area network. Typically, files such as /etc/passwd and /etc/group, which ideally would remain uniform across all hosts, are shared via NIS. In this way, every network machine that has a corresponding NIS client can read the data contained in these shared files and use the network versions of these files as extensions to the local versions.

The main benefit achieved from using NIS is that you can maintain a central copy of the data, and whenever that data is updated, it automatically propagates to all of the network users. To your users, NIS gives the appearance of a more uniform system--no matter what host they may be working on, all of their tools and files are always there.

If you're coming from a Windows NT background, you might think of NIS as a substantially more versatile Primary Domain Controller (PDC). In fact, NIS is actually much more in line with directory services such as PDCs.

In this chapter, we'll explore NIS, how it works, and how it can benefit you. Finally, then explain how to set up the client and server portions of the NIS configuration. Finally, we'll discuss some of the tools related to NIS.

# INSIDE NIS

The Network Information Service is really just a simple database that clients can query. It contains a series of independent tables. Each table originated as a straight text file, such as /etc/passwd, which is tabular in nature and has at least one column that is unique for every row (a database of key/ pair values). NIS keeps track of these tables by name and allows querying to happen in one of two ways:

+   Listing the entire table
+   Pulling a specific entry based on a search for a given key

Once the databases are established on the server, clients can query the server for database entries. Typically this happens when a client is configured to look to the NIS map when an entry cannot be found in the client's local database. A host may have a simple file containing only those entries needed for the system to work in single-user mode (where there is no network connectivity)--for example, the /etc/passwd file. When a program makes a request to look up user password information, the client checks its local passwd file and sees that the user doesn't exist there; the client then makes a request to the NIS server to look for a corresponding entry in the passwd table. If the NIS does have an entry, it is returned to the client and then to the program that requested the information in the first place. The program itself is unaware that NIS was used. The same is true of the NIS map returns an answer that the user passwd entry does not exist. The program would be passed the information without its knowing how much activity had happened in between.