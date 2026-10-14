# 3.3 NFS Servers

An NFS server allows you to share files on a Linux machine across a network of Unix machines. While its performance is mediocre (and Linux NFS servers tend to lag behind those in other Unix variants), an NFS server comes in handy for spreading files over the network, especially if the files are small. There is no restriction on what you may share with NFS—you can even export a floppy disk if you like.

# Essentials

The essential programs for NFS servers are portmap, mountd, and nfsd; /etc/exports is the main configuration file.

portmap maps RPC (remote procedure call) programs to regular network ports. RPC is a communications system that NFS, NIS, and a few other services use. mountd (or rpc.mountd) handles incoming mount requests—it is the only program that reads /etc/exports. Finally, the program that does the actual file transfers is nfsd (or rpc.nfsd).

To start an NFS server, you’ll first need an appropriate /etc/exports file. If portmap isn’t running, start it (as root), then start mountd and nfsd. If you make changes to /etc/exports, you’ll need to send mountd a HUP (hang-up) signal:

```
# kill -HUP `cat /var/run/mountd.pid`
```

Here is an example of the /etc/exports file on the machine called mikado.example.com (used as a server in the client section above):

```
/u25        *.example.com
/u40        *.example.com(rw) @other_hosts(ro)
/data2      pacific.example.com(ro)
```

We’re assuming that example.com is the local domain. When mountd starts up, it allows all hosts in example.com to read and write to /u25 and /u40; /data2 is only available to pacific.example.com, and then with read-only access. In addition, the hosts in the netgroup other_hosts have read-only access to /u40 (netgroups are an NIS concept, and we’ll talk about them in Section 3.4).

The rw and ro in this example are options that apply to mountd and nfsd. Other options include the following:

noaccess Removes access for a directory. In the previous example, if we didn’t want /data2/foo available to anyone, we’d put

```
/data2/foo    (noaccess)
```

at the end of the exports file.