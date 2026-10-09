```
# showmount -e
/usr/lpp/info/En_US alph, lisa
/n1    softy
/n0    softy
/usr/local/gnu   asimov
/usr/local/lib    asimov
/usr/local/bin    asimov
```

NFS I/O statistics can be reset and displayed using the nfsstat command. Statistics include the number and success of RPC and NFS calls for both servers and clients. Check to see if you have a high number of time-outs and retransmissions. You may need to increase the number of nfsd and biod threads on the server and client using chnfs command.

RPC errors like “Application Not Registered” are related to the portmap daemon. Check to see that the portmap daemon is running on both the local and remote systems. You can also verify the application, version, protocol, and port data maintained by local and remote portmap daemons using the rpcinfo -p -hostname command.

Verify that the ncmstsr daemon is aware of the current NFS and NIS subsystems' and sub-servers' states. Erratic behavior will occur if the NRC environment is out of sorts. Subsystem and subserver states can be displayed using the lssrc command.

```
# lssrc -g nfs
```

Subsystem Group PID Status
biod nfs 9034 active
nfed nfs 9296 active
rpc.mountd nfs 9554 active
rpc.statd nfs 10580 active
rpc.lockd nfs 10838 active

Since small deltas in client/server response times can add up quickly for large NFS environments, you may want to closely monitor traffic between systems. You can easily collect statistics with network sniffer or by using a public domain package like nfswatch.

To display and set the NFS options in the kernel, use the nfsd command; nfsd -a displays the configurable NFS options and their current values.

# HIGHLY AVAILABLE SERVERS

If you have been dealing with IBM for any number of years, you have surely heard of “Reliability, Availability, and Serviceability” (RAS). To remain competitive in the glass-house environments, UNIX must provide the same 7×24 availability that has been the hallmark of operating systems like MVS. The proliferation of X stations and diskless workstations in departmental computing environments means that there are a whole lot of folks out there who are depending on those R5/6000 and pSeries servers to be ready whenever they are.