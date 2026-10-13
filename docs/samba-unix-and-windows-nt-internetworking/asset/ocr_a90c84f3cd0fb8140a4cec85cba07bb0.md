![](bbox=[0.14, 0.15, 0.86, 0.62])

Figure 8.3: WINS point-to-point name registration

# Samba Name Service

Now we're ready to take a close look at the various roles Samba can play regarding NetBIOS Name Service. It turns out that Samba is extremely flexible when it comes to name service options. At one extreme, Samba can be configured to use host tables to describe a simple workgroup world. At the other extreme, Samba can act as a WINS server or hybrid WINS/DNS proxy agent interacting with large Windows domains.

# LMHOSTS

The easiest way to integrate Samba resources into a small workgroup is by adding the Samba server to the workgroups LMHOSTS table and making a copy of the table available to the Samba `nmbd` daemon. This is done by indicating the directory path to the LMHOSTS file as an argument to the `-H` option when starting `nmbd` (Example 8.3). The default location for LMHOSTS is the same directory that contains the Samba `smb.conf` configuration file.

Note that LMHOSTS information is only available to the local machine. The contents are not used by Samba to resolve broadcast queries from other clients. There are also a few differences between the Samba and Windows versions of LMHOSTS. Most importantly, NetBIOS name entries can include a suffix of a `#` character followed by a two digit resource type (Example 8.4). Other strings following a "#" character are treated as comments. The entry for host Wizard in the Windows LMHOSTS table (Example 8.2) and the Samba LMHOSTS table (Example 8.4) indicate that Wizard is a PDC using the respective table syntax.