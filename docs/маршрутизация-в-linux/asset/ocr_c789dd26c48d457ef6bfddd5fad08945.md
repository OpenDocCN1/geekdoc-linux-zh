# Table 7.4 Continued

| Option | Description |
|---|---|
| demand | Instructs pppd to operate in a dial-on-demand fashion. Should traffic be sent for the remote site, pppd will kick off the connection automatically without user interaction. This is the desired behavior for network gateways. |
| require-chap | require pap | Requires the peer to authenticate using the specified option. |

# Running pppd

pppd can be used to initiate a connection to a remote site or to wait on a connection from a remote site. When pppd is used to connect to a remote site, it is referred to as client operation, and when used to listen for a connection, it is referred to as the server. (Remember, this client/server model comes from the idea that a client initiates a session; from a protocol perspective, the two nodes are peers and not client and server.)

To initiate a PPP connection using pppd, several configuration options must be known and entered into the pppd configuration files. The following example is one that is typical for a connection to an ISP

The configuration information needed is the PAP username and password or CHAP host name and password, the access telephone number, whether the IP address is assigned dynamically or statically, and the serial port to which the modem is connected.

Let's assume the following information for the configuration:

+   PAP username: customer1
+   PAP password: customerpassword
+   Access telephone number: 800-555-5555
+   IP address: assigned dynamically
+   Serial port: /dev/ttyS0

This information must now be entered into the appropriate files. Because this configuration uses PAP authentication, the /etc/ppp/pap-secrets would have the following entry:

```
#Secrets for authentication using PAP
# client    server    secret    IP addresses
customer1   isp   customerpassword
```