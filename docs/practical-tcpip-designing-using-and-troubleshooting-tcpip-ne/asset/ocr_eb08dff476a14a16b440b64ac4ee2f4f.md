See the Notes in Chapter 18 for general references on Microsoft Windows Networking. RFC-1001 in particular gives an excellent and readable explanation of how NetBIOS name resolution works using broadcasts and also using a WINS-like name server. The *Resource Kit Networking Guide* is also good, but takes too much for granted. The Samba documents give good insights into name resolution, in particular:

+   * □ [NetBIOS.txt](#) *Definition of NetBIOS Protocol and Name Resolution Modes in the Samba distribution* or at
+   □ http://www.samba.org/samba/ftp/docs/textdocs/NetBIOS.txt

We’ve ignored NetBIOS *scope* completely. It’s a way to have separate NetBIOS “universes” on the same wire; machines with one NetBIOS scope can’t communicate (and can’t even “see”) machines with a different scope. Microsoft recommend that you don’t use it.

The resource kit contains three useful tools. We already mentioned *winsdmp* and *winscl* in Module 19.5. The third is *winschk*, which checks out your WINS configuration. It lets you verify that specified names are in specific WINS databases, check that your WINS replication configuration is OK, and continually monitor for WINS replication communications failures.

# NetBIOS name types

+   * □ MS-KB-Q119495 *List of Names Registered with WINS Service*
+   □ MS-KB-Q314104 *A List of Names That Are Registered by Windows Internet Naming Service*

The following is a much longer list:

+   □ MS-KB-Q163409 *NetBIOS Suffixes (16th Character of the NetBIOS Name)*

For an explanation of “normal group” versus “Internet group,” see:

+   * □ MS-KB-Q140064 *WINS Static Entry Descriptions*
+   □ WINS Manager Help, search for *Using Type Options* and view the link *Internet Group Type*

We have concentrated on computer and domain names in this chapter, but usernames are also registered in NetBIOS, as *username<03>*. This lets Windows send a message or alert to a particular user very easily. *username<03>* resolves to the IP number of the computer that *username* is logged onto, so Windows can send the message directly to that computer. Windows doesn’t have to do an exhaustive search of each machine to see if the user is logged on there.

# WINS architecture and implementation

Microsoft’s white paper on WINS is very readable and informative:

+   □ ftp://ftp.microsoft.com/bussys/winnt/winnt-docs/papers/winswp.doc

For information about running multiple WINS servers, how to estimate the load, and decide on the number and location of servers, and configuring database replication between them:

+   □ Resource Kit, Chapter 8