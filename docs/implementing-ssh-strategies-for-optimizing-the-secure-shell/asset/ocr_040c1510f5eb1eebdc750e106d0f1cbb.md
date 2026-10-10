The third example will assume that the SSH server is a Unix machine running SSH Communications’ SSH server, that the SSH client is SecureCRT running on a Windows platform for the remote administrators, and that the management clients are a Terminal Services client, VNC client, and a pcAnywhere client.

> **NOTE** Any SSH server and SSH client can be used; my example is a random selection from the different SSH applications I have discussed thus far.

# Setting Up the SSH Server

Since I am using the SSH Communications’ SSH server on a Unix platform, no special changes are required. The service will automatically port forward all connections to/from the SSH server. Nevertheless, as with the first example, some specific rules need to be implemented on the adjacent firewall to ensure that port-forwarding communications will be allowed. First, the firewall’s external interface (the interface that faces the Internet) must allow connections from the outside Internet to the SSH server, specifically port 22 on IP address 11.30.11.21. Second, the firewall’s DMZ interface (the interface that connects to the SSH server) needs to allow connections from the SSH server to the internal management servers. Specifically, the rules need to allow the SSH server (11.30.11.21) on any source port to port 3389 on the Windows Terminal server (10.1.0.100), allow the SSH server (11.30.11.21) on any source port to port 5901 on the Linux VNC server (10.1.0.150), and allow the SSH server (11.30.11.21) on any source port to port 5631 and 5632 on the pcAnywhere server 10.1.0.200). Table 7.2 shows an example of the firewall rules.

After the SSH server has been completely installed and the firewall rules are in place, the SSH server is ready for the secure management architecture.

# Table 7.2 Firewall Rules That Need to Be Enabled

| RULE NUMBER | SOURCE | DESTINATION | SERVICE | ACTION |
|---|---|---|---|---|
| 1 | Any | SSH server | Port 22 | Allow |
| 2 | SSH server | Windows Terminal server | Port 3389 | Allow |
| 3 | SSH server | Linux VNC server | Port 5901 | Allow |
| 4 | SSH server | pcAnywhere server | Port 5631 Port 5632 | Allow |
| 5 | Any | Any | Any | Deny |