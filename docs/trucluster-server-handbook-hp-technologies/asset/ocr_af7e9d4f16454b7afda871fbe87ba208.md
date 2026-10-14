```
Device Name: dsk3
Device Type: Direct Access IO Disk
Device Status: OK
Number of Servers: 2
  Server Name: molari
  Server State: Server
  Server Name: sheridan
  Server State: Server
Access Member Name: sheridan
```

All we did was reattach the cable – the DRD did the rest, automatically and transparently. This is incredible stuff!

# 15.4 DRD Events

The DRD events are defined in the /usr/share/evm/templates/clu/drd.evt template file. Below are the registered DRD events.

```
# evmwatch -A -i -f "[name *.drd]" -t "[@priority] @name"
[200] sys.unix.clu.drd.server_add
[200] sys.unix.clu.drd.server_leave
[200] sys.unix.clu.drd.new_accessnode
[300] sys.unix.clu.drd.no_accessnode
```

# 15.5 References

+   - The TruCluster Server Technical Overview Guide.
+   - The TruCluster Server Cluster Administration Guide.
+   - Reference pages (noted within the text).