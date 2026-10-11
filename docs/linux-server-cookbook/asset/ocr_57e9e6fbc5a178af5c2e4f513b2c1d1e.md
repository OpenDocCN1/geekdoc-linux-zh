| | address where the requests should be sent. This service uses 111/udp or 111/tcp. This is not required on NFSv4. | | | | rpc.mountd | Used for version 2 and version 3 to implement the directory mounting from a client. Version 4 uses only nfsd. | | | | rpc.nfsd | Provides an ancillary service needed to satisfy the NFS requests by the clients. | | | | locked | It implements the Network Lock Manager (NLM) protocol, used by NFSv3, to lock files in the server. | | | | rpc.statd | It implements the Network Status Monitor (NSM) protocol, which notifies the clients when the server is restarted. | | | | rpc.idmapd | It provides to NFSv4 server and client a map between names, local user ids, and group ids. |

Table 10.1: NFS services and description

The modern **NFSv4** is updated regularly with new versions and new features. For example, version 4.1 includes **Parallel NFS (pNFS)**, and version 4.2 includes *server-side clone and copy* features. It is important to take into consideration that some clients only accept specific versions (3,4) or minor versions (4.0, 4.1) of the NFS protocol.

# NFS server

The package on the **Advanced Packet Tool (APT)** repositories, including the NFS server, is called **nfs-server**. On systems using RPM Package Manager, the server and the client is included inside the package named **nfs-utils**. In both systems, the main service on **systemd**, after installation, is named **nfs-server**.

The main file to configure the service is `/etc/nfs.conf`, where it is possible to configure different values such as the IP protocol to be used (*tcp* and/or *udp*) or the NFS versions to be enabled (2, 3, 4, 4.0, 4.1 and 4.2). The following excerpt shows the parameters specific for the *nfsd* service, which by default are commented as follows:

```
[nfsd]
# debug=0
# threads=8
# host=
# port=0
# grace-time=90
# lease-time=90
```