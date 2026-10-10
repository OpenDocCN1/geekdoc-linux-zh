1. As root user from a Terminal window, open the /etc/auto.master file and look for a line that appears as follows:

```
/net
-hosts
```

This causes the /net directory to act as the mount point for the NFS shared directories you want to access on the network. (If there is a comment character at the beginning of that line, remove it.)

2. Start the autofs service by typing the following as root user:

```
# service autofs start
```

3. Set up the autofs service to restart every time you boot your system:

```
# chkconfig autofs on
```

Believe it or not, that's all you have to do. Provided that you have a network connection to the NFS servers from which you want to share directories, you can try to access a shared NFS directory. For example, if you know that the /usr/local/share directory is being shared from the computer on your network named shuttle, do the following:

1. Type the following:

```
$ cd /net/shuttle
```

If the computer named shuttle has any shared directories that are available to you, you will be able to successfully change to that directory. Another thing to note is that you could use an IP address instead of a hostname (for example, cd /net/10.0.0.1).

2. Type the following:

```
$ ls
usr
```

You should be able to see that the usr directory is part of the path to a shared directory. If there are shared directories from other top-level directories, you should see those as well (such as /var or /home). Of course, seeing any of those directories is dependent on how security is set up on the server.

3. Next, you could try going straight to the shared directory. For example:

```
$ cd /net/shuttle/usr/local/share
$ ls
info man music television
```

At this point, the ls should reveal the contents of the /usr/local/share directory on the computer named shuttle. What you can do with that content depends on how that content was configured for sharing by the server.