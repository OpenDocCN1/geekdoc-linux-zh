| Run-Level Scripts | What Does It Do? |
| --- | --- |
| lpd | Controls the lpd line printer daemon that handles spooling printing requests. |
| netfs | Mounts or unmounts network (NFS, SMB, and NCP) file systems. |
| network | Starts or stops all configured network interfaces and initializes the TCP/IP and IPX protocols. |
| nfs | Starts or stops the NFS-related daemons (rpc.nfsd, rpc.mountd, rpc.statd, and rpc.rquotad) and exports shared file systems. |
| pcmcia | Loads or unloads modules, drivers, and programs (including the cardmgr daemon) to support PCMCIA cards (Ethernet adapters, modems, memory cards, etc.) in laptop computers. |
| portmap | Starts or stops the portmap daemon, which manages programs and protocols that utilize the Remote Procedure Call (RPC) mechanism. |
| random | Loads or saves the current state of the machine's random number generator's random seed to ensure more random randomness. |
| reconfig | Runs the anaconda reconfiguration screens during certain start-up situations (such as a reconfig request from the LILO boot prompt). |
| routed | Starts or stops the routed daemon, which controls dynamic-routing table updates via the Router Information Protocol (RIP). |
| rstatd | Starts or stops the rpc.rstatd daemon, which enables others on the network to probe the machine for performance statistics. |
| rusersed | Starts or stops the rpc.rusersed daemon, which enables others on the network to locate users on the machine. |
| rwhod | Starts or stops the rwhod daemon, which enables others on the network to obtain a list of all currently logged-in users. |
| sendmail | Controls the sendmail daemon, which handles incoming and outgoing SMTP (Simple Mail Transport Protocol) mail messages. |
| single | Terminates all running processes and enters run level 1 (single-user mode). |