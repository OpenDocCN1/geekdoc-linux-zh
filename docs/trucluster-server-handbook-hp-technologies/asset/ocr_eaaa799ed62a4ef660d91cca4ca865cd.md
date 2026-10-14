```
P00>>> wwidmgr -show adapter
Item    adapter                 WWN              Cur. Topo  Next Topo
[ 01] pga0.0.0.7.1          2000-0000-C924-7C58  FABRIC     FABRIC
[9999] All of the above.
```

In this example, we obtained the wwid for the host bus adapter for only one of the cluster’s servers. Use this same process for each server in the cluster to determine the wwid for each host bus adapter connected to the storage subsystem

+   - Next, connect to the HSG60/HSG80 controller’s command console and determine the host connections for the adapters attached to the storage subsystem.

```
HSG> show connections
Connection
Name      Operating system  Controller  Port  Address  Status
1NEWCON1  WINNT             THIS        1     011600   OL this  0
          HOST_ID=2000-0000-C924-7C58      ADAPTER_ID=1000-0000-C924-7C58
1NEWCON2  WINNT             OTHER       2     011600   OL other 100
          HOST_ID=2000-0000-C924-7C58      ADAPTER_ID=1000-0000-C924-7C58
1NEWCON3  WINNT             THIS        1     011700   OL this  0
          HOST_ID=2000-0000-C924-3514      ADAPTER_ID=1000-0000-C924-3514
1NEWCON4  WINNT             OTHER       2     011700   OL other 100
          HOST_ID=2000-0000-C924-3514      ADAPTER_ID=1000-0000-C924-3514
```

Notice that by default, the "Operating system" is noted to be WINNT even though we are using Tru64 UNIX. We will change that to something more meaningful later in our discussion, but we are currently interested in the address of the HOST_ID. It should be the same as the wwid of the host bus adapter(s) as seen from the server’s console.

Let’s change the operating system type to Tru64 UNIX and make the connection names more meaningful.

```
HSG> set !NEWCON1 TRU64_UNIX
HSG> set !NEWCON2 TRU64_UNIX
HSG> set !NEWCON3 TRU64_UNIX
HSG> set !NEWCON4 TRU64_UNIX
HSG> rename !NEWCON1 MOLR1A1
HSG> rename !NEWCON2 MOLR1B2
HSG> rename !NEWCON3 SHER1A1
HSG> rename !NEWCON4 SHER1B2
```

That’s better, now let’s see what we have in terms of host connections.