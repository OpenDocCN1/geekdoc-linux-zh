# PART III  FILE SHARING  213

# 9  BASIC PRINCIPLES OF FILE SHARING  215

+   Using Mount Points Effectively ........................................216
+   Partitions and Mount Points ............................................217
+   Exporting Directories ..................................................218
+   What Happens with Links ...............................................219
+   Understanding Ownership and Permissions ...............................223
+     Ownership and Permission Concepts ..................................223
+     Ownership and Permissions on Non-Linux Filesystems ..................225
+     Assignment of Ownership and Permissions by Remote Systems ..........228
+     Superuser Access to Files ..........................................229
+   Case-Sensitivity in Linux and Other OSs ...............................230
+   Serving Removable Media ...............................................231
+     Supported Filesystems ...............................................231
+     Mounting a Filesystem ...............................................232
+     Connecting to Removable Media from a Remote Host ....................236
+     Quirks of Serving Removable Media ..................................237
+   Security Considerations ...............................................237
+     The Need for Passwords ..............................................238
+     Cleartext Versus Encrypted Passwords ................................238
+   Summary ................................................................239

# 10  NFS: SHARING FILES WITH OTHER UNIXES  241

+   Kernel Configuration for NFS ........................................242
+   The NFS Daemon .......................................................242
+   Setting NFS Options ...................................................244
+     The /etc/exports File ..............................................244
+     Using nfsd Options .................................................246
+     Using linuxconf to Configure NFS ...................................246
+   How Permissions Work with NFS ........................................248
+     Remote Users and Local Users ......................................248
+     Configuring a User Map File ........................................250
+     The Special Case of root ...........................................251
+   Mounting Remote NFS Volumes in Linux ..................................251
+     Using mount with Remote Systems ...................................252
+     Configuring /etc/fstab to Allow Users to Mount Remote Volumes .......253
+     Automounting Remote Volumes ........................................253
+   Summary ................................................................254