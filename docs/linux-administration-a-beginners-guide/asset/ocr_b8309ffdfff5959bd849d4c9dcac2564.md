# ## State File Handles

If a file or directory is in use by one process when another process removes the file or directory, the first process gets an error message from the server. Typically this error is "Stale NFS Filehandle." 

*Stale* file handles most often occur when you're using a system in the X-Window's environment and you have two terminal windows open. For instance, the first terminal window is in a particular directory (say, /home/user/mydir), and that directory gets removed from the second terminal window. The next time you press ENTER in the first terminal window, you'll see the error message.

+   - To fix this problem, simply change your directory to one that you know exists without using relative directories (for example, cd /tmp).

# ## Permission Denied

You're likely to see the "Permission denied" message if you're logged in as root and are trying to access a file that is NFS mounted. Typically this means that the server on which the file system is mounted is not acknowledging root's permissions. (Usually this occurs for security reasons.)

The quick way around this problem is to become the user who owns the file you're trying to control. For example, if you're root and you're trying to access a file owned by the user hdc, use the su command to become hdc:

```
```
[root@ford /root]# su - hdc
```
```

When you're done working with the file, you can exit out of hdc's shell and return to root.

Note that this workaround assumes that hdc exists as a user on the system and has the same UID on both the client and the server.

# ## Hard vs. Soft Mounts

Although we've covered hard and soft mounts in the section on configuring NFS clients, it's worth some additional comments here. When a server goes down, understanding the difference between hard and soft mounts over NFS is important to your troubleshooting efforts.

On an NFS file system that is hard mounted, the client must commit all changes to the server before allowing other operations. The client will continue trying to contact the server, until the server sends back an acknowledgement. From the user's perspective, it may look like the client system has crashed when it hasn't.

The purpose of configuring a file system as hard mounted is to make sure that data being accessed via NFS does not get lost. For crucial file systems (such as the mail spool), this is a very important attribute.

Soft mounts, on the other hand, aren't quite as persistent about getting data written to the NFS server's disk. The client will try to access the server and commit unwritten data, but after a specified time-out period (number of retries), the client will give up and return