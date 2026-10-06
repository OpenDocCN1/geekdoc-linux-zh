# TABLE 29.1 Kernel Networking Options (continued)

| Typical Value | Option | Description |
|---|---|---|n| N | IP: Multicasting | Includes support for addressing packets to multiple computers—used, for example, by hosts connected to the MBONE, a high-speed audio-video network. |
| Y/N | IP: optimize as router not host | Disable support for copy and checksum operations that improve host performance but degrade router performance. |
| Y | IP: TCP syncookie support | Includes support for cookies that protect against a SYN flood denial-of-service attack. |
| Y | IP: transparent proxying | Enables a firewall to redirect packets that originate from the local network and are destined for a remote host to a local server (transparent proxy server). |
| M | IP: tunneling | Includes support for encapsulating packets having one protocol within packets of another protocol. |
| M | IPL ipportfw masquerade support | Includes support for port forwarding, which lets you forward packets that originate outside the local network and are destined for a specified port of the firewall to a specified port of a host on the local network. |
| M | IPVS: round-robin scheduling | Specifies that the virtual server will use round-robin scheduling. |
| M | IPVS: weighted least-connection scheduling | Specifies that the virtual server will use weighted least-connection scheduling. |
| M | IPVS: weighted round-robin scheduling | Specifies that the virtual server will use weighted round-robin scheduling. |