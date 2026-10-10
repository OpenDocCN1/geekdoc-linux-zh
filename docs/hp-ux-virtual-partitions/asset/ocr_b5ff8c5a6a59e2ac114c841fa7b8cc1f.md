![](bbox=[0.16, 0.09, 0.97, 0.49])

Figure 10-3 Defaults for Creating a Bootable Recovery Archive

After we progress through these basic screens, Ignite-UX begins the process of creating the archive.

The server issued the make_net_recovery command on the client in order to create the archive. The following is the output of ps -ef for only this command on the client (actappd1) for which the archive is being produced:

```
```
root@actappd1 > ps -ef | grep make
/opt/ignite/bin/make_net_recovery -i -b -P s -l 0x00306E0981D4
root@actappd1 >
```
```