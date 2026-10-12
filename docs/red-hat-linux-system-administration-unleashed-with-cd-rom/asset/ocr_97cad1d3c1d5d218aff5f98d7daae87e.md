```
peer bb.home.vix.com {
    hostname: bb.home.vix.com
    max-connections: 20 # he can really cook.
}
}
```

There are three types of entries in incoming.conf:

+   - Key/value
+   - Peer
+   - Group

The key/value entries set parameters for the current peer or group entry. If the key/value pair is not in any other entry, it is a global value. In the preceding example, max-connections: 5 is an example of a global value. This says that unless otherwise specified, peers can open at most five connections.

The uunet peer definition is a simple peer entry. This entry allows the host usenet1.uu.net to connect to our news server to feed us news. You can see the vixie entry has an override for the max-connections value. The vixie server can open 10 connections.

The group entry provides a way to simplify the file when you have more than one server with similar characteristics. The group entry acts just like an incoming.conf file within the incoming.conf file. In the fast-sites group, all peers can have 15 connections. This max-connections entry acts just like the global value above, but its effect runs out at the end of the group. You may notice the group data.ramona.vix.com doesn't have a host defined, yet the peer name looks suspiciously like a hostname. If there is no hostname value in a peer entry, the hostname defaults to the peer name.

# cycbuff.conf (Required Only if Using the CNFS Article Storage Method)

CNFS stores articles in logical objects called metacycbuffs. Each of the metacycbuffs is in turn composed of one or more physical buffers called cycbuffs. As articles are written to the metacycbuff, each article is written to the next cycbuff in the list in a round-robin fashion. This is so that you can distribute the individual cycbuffs across multiple physical disks and balance the load between them.

Now you need to decide on the sizes of your cycbuffs and metacycbuffs. You'll probably want to separate the heavy-traffic groups (alt.binaries.* and maybe even the rest of alt.*) into their own metacycbuff so that they don't overrun the server and push out