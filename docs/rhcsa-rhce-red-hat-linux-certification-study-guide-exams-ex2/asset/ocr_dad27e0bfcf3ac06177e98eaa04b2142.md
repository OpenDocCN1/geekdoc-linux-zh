ports, to support the use of the showmount command. With fixed ports, you can configure a firewall with appropriate open ports to support an NFS server.

For that purpose, review the /etc/sysconfig/nfs file. It is already preconfigured with comments suggesting appropriate fixed port numbers. While you don't have to follow the suggested port numbers in the commented version of the file, you can. Generally, such port numbers do not cause trouble, as they do not conflict with any commonly used RHEL 6 services. For convenience, however, many administrators set up a series of consecutive unused ports for this purpose, such as 4000 through 4003.

The port numbers listed in Table 16-3 are listed in the order shown in the default version of the /etc/sysconfig/nfs file. The table does not include now-obsolete references to the rpc.lockd daemon, as that's not available for RHEL 6.

Once changes are made and saved to the /etc/sysconfig/nfs file, restart the associated service with the /etc/init.d/nfs restart command. If successful, you'll see the associated ports in the output to the rpcinfo command, which lists all communication channels associated with RPC. The following command is more precise, as it isolates actual port numbers:

```
# rpcinfo -p
```

Sample output is shown in Figure 16-1. At first glance, the lines may appear repetitive; however, every line has a purpose. Unless another RPC-related service such as the Network Information Service (NIS) is running, all of the lines shown here are required for NFS communications, when NFSv2 or NFSv3 is used. Examine the first line shown here:

```
program vers proto port service
100000 4 tcp 111 portmapper
```

# TABLE 16-3

NFS Tool User Access Options

| Port | Parameter | Description |
|------|-----------|-------------|
| 875 | RQUOTAD | Remote quota daemon |
| 892 | MOUNTD_PORT | For mount requests |
| 662 | STATD_PORT | For status requests, including locked files (port 662 is assigned to a normally unused FTP protocol) |
| 2020 | STATD_OUTGOING_PORT | Reference to outgoing communications. |