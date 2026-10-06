# CHAPTER 26 Network Information Service (NIS) 65

Continuing enter the names of any secondary NIS servers if you plan on having them. Press CTRL-d when you have added all necessary servers. These entries will be placed in the /var/yp/ypservers file for you; if needed, you can change them by editing the file later.

You will be prompted to confirm that the information you enter is correct:

```
The current list of NIS servers looks like this:
server-A.example.org
Is this correct? [y/n] y
Need a few minutes to build the databases...
Building /var/yp/nis.example.org/ypservers...
gethostbyname(): Success
Running /var/yp/Makefile...
gmake [1]: Entering directory '/var/yp/nis.example.org'
Updating passwd.byname=..
```

```
failed to send 'clear' to local yserver: RPC: Program not registeredUpdating
password.buied.
failed to send 'clear' to local yserver: RPC: Program not registeredUpdating
group.byname=..
<OUTPUT TRUNCATED>
```

server-A.example.org has been set up by a NIS master server.
You can run ypinit -s server-A.example.org on all slave servers.

(Ignore any error messages that may have resulted from this command for now.
The possible errors are discussed in more detail in the following section.)

Once you are, ypinit will run the make program automatically for you,
build the maps, and push them to all secondary servers you have indicated.
This might be a good time to make sure that the rpcbind and ypserv services are
running. Start with the commands that follow if they are not running:

```
[root@server-A #-] systemctl restart rpcbind
[root@server-A #-] systemctl restart ypserv
```

On a Debian-based distro like Ubuntu, you can start the rpcbind service and the ypserv service by running the following:

```
master@ubuntu-server-A:-$ sudo service rpcbind restart
master@ubuntu-server-A:-$ sudo service ypserv restart
```

# Makefile Errors

Any errors that have occurred from running the ypinit command in the
previous section were most likely fatal errors.
If you made a mistake in the Makefile, you may get an error when ypinit runs the make program. Don't worry if you see this error:

```
gmake [1]: *** No rule to make target '/etc/shadow', -
needed by 'passwd.byname'. Stop.
```