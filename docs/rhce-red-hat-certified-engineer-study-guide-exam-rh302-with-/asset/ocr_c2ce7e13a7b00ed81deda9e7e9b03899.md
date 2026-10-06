# Network Information Service (NIS) 553

Each line, other than comment lines, names an NIS map and specifies the sources used to obtain its keys in the order in which they should be searched. Table 22.1 summarizes NIS maps, and Table 22.2 summarizes the keywords used to specify the sources.

# TABLE 22.1 NIS Maps

| NIS Map | Shared by Default | Description |
| :--- | :--- | :--- |
| aliases | no | Mail aliases |
| ethers | no | Ethernet addresses |
| group | yes | User groups |
| hosts | yes | Host names and IP numbers |
| netgroup | yes | List of hosts and users |
| networks | yes | Network names and IP numbers |
| passwd | yes | User account information |
| protocols | yes | Network protocols |
| publicckey | no | Keys used by secure_rpc |
| rpc | yes | RPC call names |
| services | yes | Network services |
| shadow | no | Shadow passwords |

# TABLE 22.2 Sources of NIS Maps

| Source | Description |
| :--- | :--- |
| compat | NIS (in a mode compatible with old versions of the standard C library) |
| db | Local database |

Copyright©2000 SYBEX, Inc., Alameda, CA www.sysex.com *