![](bbox=[0.14, 0.09, 0.67, 0.31])

Figure 7.12 Local port-forwarding connections listening on ports 445, 2049, and 1026.

# ## Secure File Sharing with SMB and SSH

Once the SSH connection has been established, you can attempt to log in to the Windows SMB file server. To transfer files to and from the c share on the Windows file server, type the following command on the Unix SSH client:

```
``` 
#smbclient \\[\\127.0.0.1\c -U username -P 445
```
```

smbclient has very simple syntax: -U is for the username; -P is for the port number. This command will connect to the local port on 445 and then be forwarded by the SSH session. After the connection reaches the Windows file server, you should be prompted for a password. Use your Windows file server password given to you by your Windows administrator and log in. After you have entered the correct password, you will now be able to upload and download files from the Windows file server using simple Get and Put commands. The results should look like Figure 7.13.

![](bbox=[0.14, 0.85, 0.7, 0.95])

Figure 7.13 The results of file sharing with SSH with SMB and smbclient.