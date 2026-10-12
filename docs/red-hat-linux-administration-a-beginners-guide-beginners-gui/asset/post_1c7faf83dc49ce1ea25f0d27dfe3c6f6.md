
[root@arrakis yp]# /usr/lib/yp/ypinit -m

Here, the `-m` option tells `ypinit` to set the system up as a master NIS server. Assuming we are running this on a system named `arrakis.example.com`, we would see the system respond as follows:

```
At this point, we have to construct a list of the hosts that will run NIS servers. arrakis.example.com is in the list of NIS server hosts. Please continue to add the names for the other hosts, one per line. When you are done with the list, type a <control-D>.
    next host to add: arrakis.example.com
    next host to add:
```

Continue entering the name of all the secondary NIS servers. Press `CTRL-D` when you have added all necessary servers. These entries will be placed in the `/var/yp/ypservers` file for you; if needed, you can change them by editing the file later.

Once you are done, `ypinit` will run the `make` program automatically for you, to build the maps and push them to any secondary servers you have indicated.

## Makefile Errors

If you made a mistake in the makefile, you may get an error when `ypinit` runs the `make` program. If you see this error:

```
gmake[1]: *** No rule to make target `/etc/shadow', needed by `passwd.byname'.
  Stop.
```

don’t worry about it. This means you have specified a file to share that doesn’t exist (in this error message, the file is `/etc/shadow`). You can either create the file or go back and edit the makefile so that the file is not shared. (See the previous section “What Gets Shared: The all Entry.”)

Another common error message is

```
failed to send 'clear' to local ypserv: RPC: Program not registered
Updating passwd.byuid...
failed to send 'clear' to local ypserv: RPC: Program not registered
gmake[1]: *** No rule to make target `/etc/gshadow', needed by `group.byname'.
  Stop.
gmake[1]: Leaving directory `/var/yp/arrakis.example.com'
```

There are actually two error messages here. You can ignore the first one, which indicates that the NIS server hasn’t been started yet. The second error message is the same one described in the preceding paragraph. Once you’ve fixed it, type in the following command to rebuild the maps, as described in the next section:

```
[root@arrakis yp]# cd /var/yp; make
```

## Updating NIS Maps

If you have updated the files configured to be shared with NIS with the rest of your network, you need to rebuild the map files. (For example, you may have added a user to the /etc/passwd file.) To rebuild the maps, use the following **make** command:

```
[root@arrakis /root]# cd /var/yp; make
```

![](img/ec2066d370d3af1a767664d36aa7ddfe_512_0.png)

- 1. When installing the NIS server, what script can be run to initialize NIS?
- 2. Name an advantage of merging the /etc/shadow file and /etc/passwd?

### **CRITICAL SKILL** **17.3**
Configuring an NIS Client

Thankfully, NIS clients are much easier to configure than NIS servers! To set up an NIS client, you need to do the following:

- 1. Edit the /etc/yp.conf file.
- 2. Set up the startup script.
- 3. Edit the /etc/nsswitch.conf file.

## Editing the /etc/yp.conf File

The /etc/yp.conf file contains the information necessary for the client-side daemon, ypbind, to start up and find the NIS server. You need to make a decision regarding how the client is going to find the server, by either using a broadcast or by specifying the host name of the server.

The broadcast technique is appropriate when you need to move a client around to various subnets and you don’t want to have to reconfigure the client so long as an NIS server exists in the same subnet. One downside to this technique, of course, is that you must make sure that there is an NIS server in every subnet. (There are security issues with broadcasts as well, but as noted elsewhere, NIS is not the most secure system to begin with and should really only be used on trusted networks.)

- 1. To initialize NIS, you can run the following command:
  - `/etc/init.d/ypserv start`
- 2. An advantage of merging the /etc/shadow file and the /etc/passwd file is that it allows NIS to be able to authenticate the user.

## NOTE

When you use the broadcast method, you must have an NIS server in every subnet because broadcasts do not span multiple subnets. If you are uncertain whether a particular NIS server is in the same subnet, you can find out by pinging the broadcast address. If the NIS server is one of the hosts that responds, then you know for sure that the broadcast method will work.

The other technique for client-to-server contact is specifying the host name of the server. This method works well when you need to subnet your network, but you don’t need an NIS server in every subnet. This allows a client to move anywhere inside your network and still be able to find the NIS server—however, if you need to change a client so that it points to another NIS server (to balance the network load), you’ll need to change that yourself.

- ● Broadcast Method: If you choose the broadcast technique, edit the /etc/yp.conf file so that it reads as follows:

```
domain my.nis.domainname broadcast
```

where my.nis.domainname is the name of your NIS domain. Remember that if you need failover support, you will need to have two NIS servers in every subnet in order for broadcast to find the second server.

- ● Server Hostname Method: If you want to specify the name of the NIS server directly, edit the /etc/yp.conf file so that it reads as follows:

```
domain my.nis.domainname server servername
```

where my.nis.domainname is the name of your NIS domain and servername is the name of the NIS server to which you want this client to refer. You can specify this option more than once if you want to point to redundant servers. If you specify both one or more servers by name and a broadcast option, ypbind will attempt to use the named servers first and fall back on the broadcast option only as a last resort.

## NOTE

Remember that you also have an entry for servername in the /etc/hosts file. At the time NIS is started, you may not yet have access to DNS, and you most certainly don’t have access to the NIS hosts table yet! For this reason, the client must be able to do the host name-to-IP resolution without the aid of any other services.

## Setting Up the Startup Script

The NIS client runs a daemon called **ypbind** in order to communicate with the server. Typically, this is started in the */etc/init.d/ypbind* startup script. This can be set to automatically start on boot using the **redhat-config-services** tool and selecting the **ypbind** entry. The equivalent symlinks for the `rc` directories would be S27ypbind and K73ypbind.

- To start the daemon without having to reboot, use this command:
  - If you need to stop the daemon, type

```
[root@caladan /root]# /etc/init.d/ypbind start
[root@caladan /root]# /etc/init.d/ypbind stop
```

## Editing the /etc/nsswitch.conf File

The */etc/nsswitch.conf* file is responsible for telling the system the order in which to search for information. The format of the file is as follows:

```
filename:  servicename
```

where *filename* is the name of the file that needs to be referenced and *servicename* is the name of the service to use to find the file. Multiple services can be listed, separated by spaces. Here are the most important service entries:

| Service | Description |
|---|---|
| files | Use the actual file on the host itself. |
| nis | Use NIS to perform the lookup. |
| yp | Use NIS to perform the lookup (nis is an alias for **yp**). |
| compat | This is a compatibility mode to enable features from earlier NIS implementations. (This applies only to **passwd**, **shadow**, and **group** entries.) See "Using NIS in Configuration Files," later in this module. |
| dns | Use DNS for the lookup (applies only to hosts). |
| [NOTFOUND=return] | Stop searching if the preceding entry resulted in a "not found" response. See the following text for more information. |
| nisplus | Use NIS+ (if you're on a network that requires it). |

Here is an example entry in the */etc/nsswitch.conf* file:

```
passwd:      files nis
```
