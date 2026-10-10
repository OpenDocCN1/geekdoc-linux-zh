Notice a couple of things about Figure 7.13. First, observe that the connection is to the loopback interface. Second, check out the password prompt by the remote Windows file server, which is still over the SSH tunnel. (This solves problems of NTLM weaknesses also, which will not be discussed here.) Lastly, mark the get file.txt command, which downloads the file called file.txt from the remote Windows file server to the local Unix laptop, all over the encrypted SSH session.

> **NOTE** An SSH client on Windows will not be able to forward local connections on port 445, since Windows networking does not allow SMB over TCP and another service to share port 445; thus, the SSH forward will be denied access to that local port.

This scenario allows you to use SMB over an encrypted SSH tunnel over the Internet.

# ## Secure File Sharing with NFS and SSH

To use SSH with NFS, one additional step needs to be completed on the NFS server. The /etc/exports file, the file that holds the lists of authorized clients, needs to add the SSH server’s IP address to this file. Since SSH clients will be using the SSH server to access the NFS server, it must be authorized to do so. Edit the /etc/exports file in the NFS server to the following:

```
```plain
/home 11.30.11.21 (rw, root_squash)
```
```

Once the change has been made and the services have been restarted, establish the session with the SSH server. Once the session has been established, you can attempt to log in to the Solaris NFS file server. To transfer files to and from the /home NFS share on the Solaris NFS file server, type the following command:

```
```plain
#mount -t nfs -o tcp,port=2049 ,mountport=1026 127.0.0.1:/home /nfs
```
```

Mount is the actual protocol to access the NFS server, using port 1026 in this example. The mount command has very simple syntax, where the IP address of the NFS server is separated by a colon to the NFS share, followed by the local path to mount the remote NFS share, such as /nfs in this example. This command will connect to the local port on 2049 and 1026 and then be forwarded by the SSH session. After the connection reaches the Solaris NFS file server, the NFS server will verify that you are allowed to mount this NFS share. After it verifies you, the remote NFS share should be mounted to /nfs- mount on your local Unix operating system.