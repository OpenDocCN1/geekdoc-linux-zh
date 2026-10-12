# ## 19  
Windows Networking – name resolution

+   19.1	NetBIOS names and name resolution – overview
+   19.2	NetBIOS names
+   19.3	Method 1: broadcasts
+   19.4	Method 2: WINS – the NetBIOS name server
+   19.5	WINS server configuration
+   19.6	Other WINS issues: non-WINS clients; database replication
+   19.7	Method 3: using the DNS as NetBIOS name server instead of using WINS
+   19.8	Methods 4, 6: HOSTS files and NetBIOS cache
+   19.9	Method 5: LMHOSTS – the LAN Manager hosts file
+   19.10	"Node type" and NetBIOS name resolution order
+   19.11	Choosing a node type
+   19.12	Troubleshooting NetBIOS name resolution
+   		Summary

# ### Introduction

NetBIOS names are fundamental to Windows Networking because names, not IP numbers, are its primary reference for machines and resources on the network. A machine "registers" a name when it is prepared to offer a particular resource or service. It can register the name using broadcast packets, or using a special name registration server called WINS – the Windows Internet Name Service. Other machines also use broadcasts or WINS to resolve names in order to access the corresponding resources. However, a machine can also use several other mechanisms to resolve names, which can be useful in particular circumstances.