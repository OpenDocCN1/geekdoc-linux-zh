described in detail in the following sections.) You then select the kind of encryption you want to use. This can either be manual or use IKE, letting racoon automatically manage the encryption and authentication process.

You then will configure both your local and remote connections, starting with the local settings. For a host-to-host connection, you need only enter the IP address for the remote host. For a VPN, you will have to enter corresponding addresses for the local and remote networks. For the local network, you will need to enter the IP addresses for the local network, the local network's gateway computer, and the local network's netmask. For the remote VPN connection, you will need the remote IP address, the remote network's address, its netmask, and its gateway address. Finally, you will enter the authentication key. Click the Generate button to create one.

A final screen will display your entries. Click Apply to save them. Your connection will appear in the IPsec panel, showing its type, destination, and nickname. To establish a connection, select the IPsec connection and click Activate. This will run the /etc/sysconfig/network-scripts directory, which will execute IPsec tools such as setkey and racoon to establish your connection. Configuration data will be kept in the /etc/sysconfig/networking/devices directory, using the name of the IPsec connections. For example, configuration information on the myipsec IPsec connection is kept in the ifcfg-myipsec file. Corresponding keys for each connection are kept in the keys files, including keys-myipsec. A sample configuration for a VPN is shown here. The IKE method is a private shared key (PSK). The destination (remote) gateway is 10.0.0.1, and the source (local) gateway is 192.168.0.1. The destination (remote) network address is 10.0.0.0/24, and the source (local) address is 192.168.0.0/24. The destination host is 10.0.0.2.

```
ONBOOT=no
IKE_METHOD=PSK
DSTGW=10.0.0.1
SRCGW=192.168.0.1
DSTNET=10.0.0.0/24
SRCNET=192.168.0.0/24
DST=10.0.0.2
TYPE=IPSEC
```

# Configuring Connections with setkey

To configure your IPsec connections, you can use the setkey tool. This tool contains several instructions for managing rules in the IPsec policy and security databases. You use the add instruction to add a security association to the security database (SAD), and the spadd instruction to add a policy to the policy database (SPD). The ah term designates that the instruction is being applied to the authentication header (AH), and esp indicates the encryption to be implemented by the encryption security payload (ESP). To implement setkey operations, it is best to use a script invoking setkey with the -f option and listing the setkey instructions. The following example creates a simple script to add authentication and encryption instructions for a particular connection, as well as create a security policy for it:

```
#!/sbin/setkey -f
add 192.168.0.2 192.168.0.5 ah 15700 -A hmac-md5 "secret key";
```