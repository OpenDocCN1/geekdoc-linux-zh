
## Specifying Shared Files

The actual files that are shared on the network are listed in the all: entry, which follows the list of configuration files. Only some of the files defined are listed as shared, those listed in the first line after all:. The remaining lines are automatically commented out (with a preceding # sign). You can add files by removing the # sign or moving their entries to the first line.

```
all: passwd group hosts rpc services netid protocols mail \
  # netgrp shadow publickey networks ethers bootparams printcap \
  # amd.home auto.master auto.home auto.local passwd.adjunct \
  # timezone locale netmasks
```

Be sure not to touch the remainder of the Makefile.

## Creating the NIS Database

You then enter the ypinit command with the -m option to create the NIS database consisting of the NIS configuration files. Your NIS server will be detected, and then you will be asked to enter the names of any slave NIS servers used on this NIS domain. If there are any, enter them. When you are finished, press CTRL-D. The NIS database files are then created.

```
ypinit -m
```

For an NIS slave server, you would use

```
ypinit -s masterhost
```

Should you receive the following error, it most likely means that your NIS server was not running. Be sure to start ypserv before you run ypinit.

```
failed to send 'clear' to local ypserv: RPC: Program not registered
```

If you later need to update your NIS server files, you would change to the /var/yp directory and issue the make command.

```
cd /var/yp
```

```
make
```

## Controlling Access

The /var/yp/secure nets file enables access by hosts to your NIS server. Hosts can be referenced by network or individually. Entries consist of a subnet mask and an IP address. For example, you could give access to all the hosts in a local network with the following entry:

```
255.255.255.0 192.168.1.0
```

For individual hosts, you can use the mask 255.255.255.255 or just the term "host," as shown here:

```
host 192.168.1.4
```

Controlling how different hosts access NIS shared data is determined in /etc/ypserv.conf.

## Netgroups

You can use NIS to set up netgroups, which allows you to create network-level groups of users. Whereas normal groups are created locally on separate hosts, an NIS netgroup can be used for network-wide services. For example, you can use NIS netgroups to control access to NFS file systems. Netgroups are defined in the /etc/netgroup file. Entries consist of a netgroup name followed by member identifiers consisting of three segments: the host, the user, and the NIS domain:

```
group  (host, user, NIS-domain) (host, user, NIS-domain) ...
```

For example, in the NIS domain myturtles.nis, to define a group called myprojects that consists of the user chris on the host rabbit, and the user george on the host lizard.mytrek.com, you would use the following:

```
myprojects (rabbit, chris, myturtles.nis) \
            (lizard.mytrek.com, george, myturtles.nis)
```

A blank segment will match on any value. The following entry includes all users on the host rabbit:

```
newgame (rabbit, , myturtles.nis)
```

If your use of a group doesn’t need either a user or a host segment, you can eliminate one or the other using a hyphen (-). The following example generates a netgroup consisting just of hostnames, with no usernames:

```
myservers (rabbit, -, ) (turtle.mytrek.com, -, )
```

You can then reference different netgroups in various configuration files by prefixing the netgroup name with an @ sign, as shown here:

```
@newgame
```

## NIS Clients

For a host to use NIS on your network, you first need to specify your NIS domain name on that host. In addition, your NIS clients need to know the name of your NIS server. If you installed Linux on a network already running NIS, you may have already entered this information during the installation process.

## Specifying the NIS Domain and Server

On Red Hat, you can specify your NIS domain name and server with the authconfig-gtk tool, which you can access from the System Settings window. In that window, select Authentication. This opens the Authentication Configuration window. On the User Information panel, click the Configure NIS button to open a dialog where you can enter the name of the NIS domain as well as the NIS server. Be sure to also enable NIS on the User Information panel. The NIS domain will be saved in the /etc/sysconfig/network file, and the NIS server, in the /etc/yp.conf file.
