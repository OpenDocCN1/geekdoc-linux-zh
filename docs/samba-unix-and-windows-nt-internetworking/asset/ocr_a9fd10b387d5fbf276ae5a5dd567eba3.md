parameters determine whether Samba will act as a client or a server and if the latter, how it will influence the master browser election process. At this point let's assume we are running within a workgroup on a single subnet or flat network.

# Browser Client

First, we'll assume that Samba should announce its shares but will not maintain browse lists (Figure 9.2). Let somebody else do the work of the local master and backup browsers. Disable the domain master, local master, and preferred master parameters. Set the os level to zero. This configuration will inhibit Samba from becoming a master browser:

```
domain master = no
local master = no
preferred master = no
os level = 0
```

![](bbox=[0.13, 0.48, 0.87, 0.83])

Figure 9.2: Samba as a browser client

# Local Master Browser

If you would like Samba to do its share of the work and maintain and serve browse lists as a master or backup browser (Figure 9.3), then enable the browse lists and local master parameters. The preferred master parameter will help Samba edge out contenders if there is a tie in os level values. The browse lists parameter indicates that Samba will serve lists when it receives a NetServerEnum call.