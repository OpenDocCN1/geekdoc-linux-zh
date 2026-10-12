
## Introduction to NIS Configuration

Begin by opening `/etc/nsswitch.conf` with your favorite editor. Scroll past the comments (those lines beginning with the # symbol). You should see something like this:

```text
passwd:	files nisplus nis
shadow:	files nisplus nis
group:	files nisplus nis

hosts:	files nisplus nis dns

services:	nisplus [NOTFOUND=return] files
				etc...
```

The first column indicates the file in question. In the first line, this is **passwd**. The next column indicates the source for the file. This can be one of six options listed in Table 15.1.

| Option | Description |
|---|---|
| nis | Uses NIS to determine this information. |
| yp | Uses NIS to determine this information (alias for **nis**). |
| dns | Uses DNS to determine this information (only applicable to **hosts**). |
| files | Uses the file on the local machine to determine this information (for example, `/etc/passwd`). |
| [NOTFOUND=return] | Stops searching if the information has not been found yet. |
| nisplus | Uses NIS+. |

The order in which these are placed in the `/etc/nsswitch.conf` file determines the search order used by the system. For example, in the **hosts** line, the order of the entries is **files nis dns**, indicating that hostnames are first searched for in the `/etc/hosts` file, then via NIS in the map **hosts.byname**, and finally by DNS via the DNS server specified in `/etc/resolv.conf`.

In almost all instances, you want to search the local file before searching through NIS or DNS. This allows a machine to have local characteristics (such as a special user listed in `/etc/passwd`) while still using the network services being offered. The notable exception to this is the netgroup file that by its very nature should come from NIS.

Modify the order of your searches to suit your site’s needs and save the configuration file.

## Setting Up the NIS Client

Now that all the files are in place, set up the client daemon to automatically start at boot time. You do this by creating a symbolic link from `/etc/rc3.d/S63ypbind` to `/etc/init.d/ypbind`. The exact commands are as follows:

```bash
[root@Client /root]# cd /etc/rc3.d
[root@Client rc3.d]# ln -s ../init.d/ypbind S63ypbind
```

### Testing the Client

Because of the way NIS works under Red Hat, you do not need to reboot to start NIS client functions. To see if you can communicate with the NIS server, start by setting the domain name by hand. You can do so with the following command:

```bash
[root@Client /root]# domainname nis_domain
```

`nis_domain` is the NIS domain name. In the test case, it is `audionet.domain.com`. Start the NIS client daemon, `ypbind`, with this command:

```bash
[root@Client /root]# /etc/init.d/ypbind start
```

With the NIS client and server configured, you are ready to test your work:

```bash
ypcat passwd
```

If your configuration is working, you should see the contents of your NIS server's `/etc/passwd.yp` file displayed on your screen (assuming, of course, that you chose that file to be shared via NIS for your passwd file). If you receive a message such as `No such map passwd.byname. Reason: can't bind to a server which serves domain`, you need to double-check that your files have been properly configured.

> **Tip**
> As a precautionary measure, you should schedule a reboot while you are with the machine to ensure that it does start and configure the NIS information correctly. After all, your users will not be happy if after a power failure, your machine does not come back up correctly without assistance.

## Configuring a NIS Secondary Server

After you’ve decided to configure a machine as a NIS secondary server, you start by configuring it as a NIS client machine. Verify that you can access the server maps via the ypcat command.

Now you are ready to tell the master server that a slave server exists. To do this, edit the `/var/yp/ypserver` file so that the slave server you are setting up is included in the list. Now make sure you are in `/var/yp` and then run a `make`. If you configured your master server with the name of the slave server during the `ypinit -m` phase, you do not need to do this.

On the slave server make sure that the `ypserv` daemon is installed. If it is not, you will need to install this from the RPM.

```bash
[root@Client /root]# cd /mnt/cdrom/Redhat/RPMS
[root@Client RPMS]# rpm -i ypserv*
```

You will have to make the `ypserv` daemon start at boot time. The commands to do this are

```bash
[root@Client /root]# cd /etc/rc3.d
[root@Client rc3.d]# ln -s ../init.d/ypserv S60ypserv
```

You can now initialize the slave server by running the command

```bash
/usr/lib/yp/ypinit -s master
```

`master` is the hostname for the NIS master server. In this example, it’s `vestax`. The output should look something like the following:

```text
We will need some minutes to copy the databases from vestax.
Transferring mail.aliases ...
Trying ypxfrd ... not running
Transferring services.byname ...
Trying ypxfrd ... not running
Transferring rpc.bynumber ...
Trying ypxfrd ... not running
[etc ...]
```

`denon.domain.com`’s NIS database has been set up.

If there were warnings, please figure out what went wrong, and fix it.

At this point, make sure that `/etc/passwd` and `/etc/group` have been edited so that when the NIS is activated, the databases you have just created will be used, instead of the `/etc` ASCII files.

Don't worry about the *Trying ypxfrd...not running* message. This happens because you haven't set the NIS master server to run the YP map transfer daemon `rpc.ypxfrd`. In fact, you never set it up to do so; instead, use a server push method where the NIS master server pushes the maps to all the NIS slaves whenever there is an update.

To set the NIS master to do the actual push, you need to change its makefile a little. On the master server, edit the makefile so that the line `NOPUSH="True"` is changed to read `NOPUSH="false"` and the line that reads `DOMAIN = basename \`pwd\`` is changed to `DOMAIN = /bin/domainname`.

Now for the big test: On the NIS master server, run `cd /var/yp; make all` to force all the maps to be rebuilt and pushed. The output should look something like the following:

```text
Updating passwd.byname....
Pushed passwd.byname map.
Updating passwd.byuid....
Pushed passwd.byuid map.
Updating hosts.byname...
Pushed hosts.byname.
Updating hosts.byaddr....
Pushed hosts.byaddr.
[etc...]
```

If you get an error like the following:

```text
Could not read ypservers map: 3 Can't bind to server which serves this domain
```

you will have to set up the master server as a client also. Change the `/etc/yp.conf` file to point to the server, in this case `vexsta.audionet.domain.com`. Add an entry to the `/etc/sysconfig/network` file such as `NISDOMAIN=nisdomain` where `nisdomain` is your domain, in this example `audionet.domain.com`. Don't forget to start the `ypbind` daemon also.

On the NIS slave server, change the `/etc/yp.conf` file so that the `ypserver` is set to point to the slave server. Run the command `ypcat passwd` and see whether your NIS password file is displayed. If so, you're set. The NIS slave server is configured.

If you're having problems, trace through your steps. Also be sure to reboot the machine and see if your NIS slave server still works correctly. If it doesn't come back up, be sure that the changes you made to the boot sequence when installing `ypserv` were correct.

## Tip

If your NIS client or slave server seems to have a hard time finding other hosts on the network, be sure that the `/etc/nsswitch.conf` file is set to resolve hosts by file before NIS. Then be sure that all the important hosts needed for the NIS servers to set themselves up are in their own local `/etc/hosts` file.

## Using NIS-isms in Your `/etc/passwd` File

The most popular use of NIS is to keep a global user database so that it is possible to grant access to any machine at your site to any user. Under Red Hat Linux, this behavior is implicit for all NIS clients.

Sometimes, however, you do not want everyone accessing certain systems, such as those used by `personnel`. You can fix this access by using the special token `+` in your `/etc/passwd` file. By default, NIS clients have the line `+:::` at the end of their `/etc/passwd` file, thereby allowing everyone in NIS to log in to the system. To arrange that the host remains a NIS client but does not grant everyone permission, change the line to read `+:::/bin/false`. This will allow only people with actual entries in the `/etc/passwd` file for that host (for example, `root`) to log in.

To allow a specific person to log in to a host, you can add a line to the `/etc/passwd` file granting this access. The format of the line is `+username:::` where `username` is the login of the user you want to grant access to. NIS will automatically grab the user's `passwd` entry from the NIS server and use the correct information for determining the user information (for example, UID, GID, GECOS, and so on). You can override particular fields by inserting the new value in the `+username:::` entry. For example, if the user `sshan` uses `/usr/local1/bin/tosh` as his shell but the host he needs to log in to keeps it in `/bin/tosh`, you can set his `/etc/passwd` entry to `+sshan:::/bin/tosh`.

## Using Netgroups

Netgroups are a great way to identify people and machines under nice, neat names for access control. A good example of using this feature is for a site where users are not allowed to log in to server machines. You can create a netgroup for the system administrators and let in members of the group through a special entry in the `/etc/passwd` file.
