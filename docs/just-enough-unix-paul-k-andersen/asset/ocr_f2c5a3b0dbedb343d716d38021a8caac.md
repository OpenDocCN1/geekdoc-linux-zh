# # 16 TUTORIAL: TRANSFERRING FILES

Both rcp (“remote copy”) and ftp (“file transfer protocol”) allow you to transfer files between two computer systems on which you have accounts. The rcp utility is designed to work with two UNIX systems; ftp can also get files from non-UNIX hosts. Moreover, ftp can be used to obtain files from public file servers.

# ## 16.1 Running rcp

In this section you will see how to use rcp to obtain a file from a remote UNIX host. For rcp to work, three conditions must be met:

+   - You must have an account on the remote UNIX host.
+   - Both hosts must “trust” each other.
+   - You must have permission to copy the file.

Assuming that these conditions are met, the procedure for copying the file is very simple:

+   - Enter the rcp command, specifying the remote host and remote file, then the local host and the new file name. For example, if you wanted to copy the file myfile from the remote UNIX host farhost.xyz.edu, you would type
+   ```bash
+   $ rcp farhost.xyz.edu:myfile .:mycopy (Return)
+   ```
+   Note that no password is needed. The rcp utility will simply refuse to work if you do not have an account on the remote host or the hosts do not trust each other.

# ## 16.2 Running ftp

In this section you will see how to use ftp to copy files from a remote host—either a UNIX or non-UNIX computer—on which you have an account.