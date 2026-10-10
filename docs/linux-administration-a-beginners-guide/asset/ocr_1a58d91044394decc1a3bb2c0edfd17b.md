```
srvce_name sock_type protocol [no]wait user svr_prog svr_prog_args
```

Table 9-3 explains each element of the service descriptions in *Ietc/inetd.conf*.

| Column Name | Description |
| :--- | :--- |
| **srvce_name** | The name of the service being offered. This has a correlation to the *Ietc/services* file, which maps the name of the service to the port on which it is offered. If you need to add something new to *Ietc/inetd.conf*, you'll also need to add a corresponding entry to *Ietc/services*. (Don't worry, the format of the *Ietc/services* file is inconsequential.) |
| **sock_type** | Socket type can be either *stream* or *dgram*. The stream (for example, telnet and ftp), *Ietc/inetd.conf* data streams (for example, telnet and ftp). The *dgram* value refers to datagram (UDP) streams (for example, tftp). The tftp service is a datagram-based protocol. Other protocols outside the scope of TCP/IP do exist; however, you'll rarely encounter them. |
| **protocol** | This will be a value as defined in the *Ietc/protocols* file—typically *tcp*, *udp*, or *rpc/tcp* for RPC-based TCP services, and *rpc/udp* for RPC-based UDP services. |
| **[no]wait** | May be either *wait* or *nowait*. For any stream (TCP)-based connections, you should use *nowait*. For other connections, the value depends on the type of datagram connection supported by the process. The *wait* value means the client will connect to the server and wait for a response before dropping the connection. (This is often called a “single-threaded” server because it can only handle one request at a time.) The *nowait* value means the client will disconnect once it has sent its information. |
| **user** | The process will run as the service defined in this entry. Be *very careful* with this entry—an incorrect choice may constitute a security hazard. In general, try to select services that can be run as a nonzero user. If you must run a service that has to start as root, be sure the program is well designed, and read all of its documentation to ensure that you have it configured correctly. |
| **svr_prog** | This is the full path of the program that is to be executed when connected to. |

*Table 9-3. Elements of the Service Descriptions in Ietc/inetd.conf*