```
sock->sk = NULL;
sock->file = NULL;
sockets_in_use[smp_processor_id()].counter++;
return sock;
}
```

Of course, we also need to be able to return these identifiers to the pool of free ones.

**Figure 5.68** Glue-free a socket inode: linux/net/socket.c.

```
/*
 * sock_release - close a socket
 * @sock: socket to close
 * 
 * The socket is released from the protocol stack if it has a release
 * callback, and the inode is then released if the socket is bound to
 * an inode is not a file.
 */
void sock_release(struct socket *sock) {
	if (sock->ops) {
		sock->ops->release(sock);
	}
	if (sock->fasync_list) {
		printk(KERN_ERR "sock_release: fasync list not empty!\n");
	}
	sockets_in_use[smp_processor_id()].counter--;
	if (sock->file) {
		put(sock->inode);
		return;
	}
	sock->file=NULL;
}
```

This was all for the convenience of the operating system so that we have a single unified interface between the system call code and various lower-level services, both filesystems and interprocess communication, including a unified set of identifiers.

# Back to the VFS Socket Code Instances

Now we return to looking at more instances of socket functions that implement virtual filesystem systems—here is the code for accessing the open() call.