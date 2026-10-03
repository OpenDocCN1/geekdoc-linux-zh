# TABLE 18.2 continued

# DEFAULT NIS MAPS

| Map Name | Corresponding NIS Admin File | Description |
|---|---|---|
| netmasks.byaddr | netmasks | This map contains the network masks to be used with IP subnetting. The address is the key. |
| networks.byaddr | networks | This map contains names of networks known to your system and their IP addresses. The address is the key. |
| networks.byname | networks | This map contains names of networks known to your system and their IP addresses. The name of the network is the key. |
| passwd.adjunct.byname | passwd and shadow | This map contains auditing shadow information and the hidden password information for C2 clients. |
| passwd.byname | passwd and shadow | This map contains password and shadow information. The user name is the key. |
| passwd.byuid | passwd and shadow | This map contains password and shadow information. The user ID is the key. |
| protocols.byname | protocols | This map contains the network protocols known to your network. The protocol is the key. |
| protocols.bynumber | protocols | This map contains the network protocols known to your network. The protocol number is the key. |
| rpc.bynumber | rpc | This map contains the program number and the name of Remote Procedure Calls (RPCs) known to your system. The program number is the key. |
| services.byname | services | This map lists Internet services known to your network. The key port or protocol is the key. |
| services.byservice | services | This map lists Internet services known to your network. The service name is the key. |
| ypservers | N/A | This map lists the NIS servers known to your network. It's a single column table with the system name as the key. |