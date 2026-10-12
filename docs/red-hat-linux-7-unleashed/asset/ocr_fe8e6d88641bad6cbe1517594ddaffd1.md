+   Unmounting a Filesystem ........................................516
+   Configuring the /etc/fstab File to Mount Filesystems Automatically ................................517
+   Exporting Filesystems with linuxconf ...........................519
+   Complete Sample Configuration Files ....................521
+   Summary ............................522

# **17  Samba  523**

+   Installing Samba ........................................525
+   Getting a Simple Samba Setup Running .........525
+   - Testing with a Linux Client ...........................527
+   - Testing with a Windows Client ........................528
+   Configuring Samba ....................................532
+   - The [global] Section ................................533
+   - The [homes] Section ..................................534
+   - The [printers] Section .................................536
+   Configuring a Samba File Server with linuxconf 539
+   Sharing Files and Print Services ................540
+   Optimizing Samba Performance ............................541
+   Testing Your Configuration .............................543
+   - Testing with smbstatus .............................544
+   Running the Samba Server ..............................545
+   Accessing Shares ................................545
+   - Using smbclient on a Linux Client .....................545
+   - Mounting Shares on a Linux Client ...........................548
+   Common smb.conf Options .............................549
+   Special Conventions .....................................549
+   - read only= Versus writeable= Versus writable= ............550
+   - Versus write ok= (S) .............................550
+   - valid users= (S) ......................................550
+   - invalid users= (S) ................................550
+   - read list= (S) .....................................551
+   - write list= (S) .....................................551
+   - path= (S) ........................................551
+   - create mask= and create mode= (S) ......................552
+   - browseable= (S) ...................................552
+   - printable= (S) .......................................553
+   - hosts allow= Versus hosts deny= Versus allow hosts=
+   - Versus deny hosts= (S) ............................553
+   - public= and guest ok= (G) .....................553
+   - comment= (S) and server string= (G) ...................554
+   - domain logons= (G) ..............................554
+   - encrypt passwords= and smb passwd file= (G) ....554
+   - config file= (G) ................................554