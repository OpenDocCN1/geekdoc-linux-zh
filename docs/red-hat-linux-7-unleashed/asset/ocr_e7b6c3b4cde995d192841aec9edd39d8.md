Now that all the files are in place, set up the client daemon to automatically start at boot time. You do this by creating a symbolic link from `/etc/rc.3/$63ypbind` to `/etc/init.d/ypbind`. The exact commands are as follows:

```
[root@Client /root]# cd /etc/rc3.d
[root@Client rc3.d]# ln -s ../init.d/ypbind 563ypbind
```

# Testing the Client

Because of the way NIS works under Red Hat, you do not need to reboot to start NIS client functions. To see if you can communicate with the NIS server, start by setting the domain name by hand. You can do so with the following command:

```
[root@Client /root]# domainname nis_domain
```

`nis_domain` is the NIS domain name. In the test case, it is `audionet.domain.com`. Start the NIS client daemon, `ypbind`, with this command:

```
[root@Client /root]# /etc/init.d/ypbind start
```

With the NIS client and server configured, you are ready to test your work:

```
ypcat passwd
```

If your configuration is working, you should see the contents of your NIS server's `/etc/passwd.yp` file displayed on your screen (assuming, of course, that you chose that file to be shared via NIS for your passwd file). If you receive a message such as No such map `passwd.byname`. Reason: `can't bind to a server which serves domain`, you need to double-check that your files have been properly configured.

> **Tip**
> As a precautionary measure, you should schedule a reboot while you are with the machine to ensure that it does start and configure the NIS information correctly. After all, your users will not be happy if after a power failure, your machine does not come back up correctly without assistance.